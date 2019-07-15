---
title: Использование альтернативного поставщика многофакторной идентификации с помощью API для активации сценариев PAM или SSPR | Документация Майкрософт
description: Настраиваемый API MFA можно задать в качестве второго уровня безопасности при активации ролей в сценариях Privileged Access Management (PAM) и самостоятельного сброса пароля (SSPR).
keywords: ''
author: billmath
ms.author: billmath
ms.reviewer: fimguy
manager: mtillman
ms.date: 09/04/2018
ms.topic: article
ms.prod: microsoft-identity-manager
ms.openlocfilehash: 7fb111520f94541672fc56d0fd2ee95bfcd3a49e
ms.sourcegitcommit: f58926a9e681131596a25b66418af410a028ad2c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/09/2019
ms.locfileid: "67690750"
---
# <a name="use-a-custom-multi-factor-authentication-provider-via-an-api-during-pam-role-activation-or-in-sspr"></a>Использование настраиваемого поставщика многофакторной идентификации с помощью API при активации роли PAM или в сценарии SSPR

Клиенты Azure AD Premium или Azure MFA могут интегрировать Azure MFA в двух сценариях MIM — активация роли Privileged Access Management (PAM) и самостоятельный сброс пароля (SSPR).

Клиентам MIM доступны два дополнительных варианта действий.

 - Использовать настраиваемый поставщик доставки одноразового пароля, который применим только в сценарии MIM SSPR и описан в руководстве [Настройка самостоятельного сброса пароля с помощью шлюза OTP SMS](https://docs.microsoft.com/en-us/previous-versions/mim/hh824692(v=ws.10)).
 - Использовать настраиваемый поставщик служб телефонии для многофакторной идентификации. Этот вариант подходит для сценариев MIM SSPR и PAM, приведенных в этой статье.

В этой статье описывается, как использовать MIM с настраиваемым поставщиком многофакторной идентификации с помощью API и пакета SDK интеграции, разработанного клиентом.  

## <a name="prerequisites"></a>Предварительные условия

Чтобы использовать API настраиваемого поставщика многофакторной идентификации с MIM, вам потребуются следующие компоненты.

- Номера телефонов всех пользователей-кандидатов
- Исправление MIM [4.5.202.0](https://www.microsoft.com/download/details.aspx?id=57278) или более поздней версии — объявления см. в [журнале версий](reference/version-history.md)
- Служба MIM, настроенная для SSPR или PAM

## <a name="approach-using-custom-multi-factor-authentication-code"></a>Подход с использованием пользовательского кода многофакторной идентификации

### <a name="step-1-ensure-mim-service-is-at-version-452020-or-later"></a>Шаг 1. Использование службы MIM версии 4.5.202.0 или более поздней

Скачайте и установите исправление MIM [4.5.202.0](https://www.microsoft.com/download/details.aspx?id=57278) или более поздней версии.

### <a name="step-2-create-a-dll-which-implements-the-iphoneserviceprovider-interface"></a>Шаг 2. Создание библиотеки DLL, реализующей интерфейс IPhoneServiceProvider

Библиотека DLL должна содержать класс, который реализует три метода.

- `InitiateCall`: этот метод будет вызываться службой MIM. Служба передает телефонный номер и идентификатор запроса в качестве параметров.  Метод должен вернуть значение `PhoneCallStatus`, равное `Pending`, `Success` или `Failed`.
- `GetCallStatus`: служба MIM вызовет этот метод, если предыдущий вызов `initiateCall` вернул `Pending`. Этот метод также возвращает значение `PhoneCallStatus`, равное `Pending`, `Success` или `Failed`.
- `GetFailureMessage`: служба MIM вызовет этот метод, если предыдущий вызов `InitiateCall` или `GetCallStatus` вернул `Failed`. Этот метод возвращает диагностическое сообщение.

Реализации этих методов должны быть потокобезопасными. Более того, в реализации `GetCallStatus` и `GetFailureMessage` не должно предполагаться, что эти методы будут вызываться тем же потоком, который ранее вызывал метод `InitiateCall`.

Сохраните DLL в каталоге `C:\Program Files\Microsoft Forefront Identity Manager\2010\Service\`.

Ниже приведен пример кода, который можно скомпилировать с помощью Visual Studio 2010 или более поздней версии.

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using System.Text;
using Microsoft.IdentityManagement.PhoneServiceProvider;

namespace CustomPhoneGate
{
    public class CustomPhoneGate: IPhoneServiceProvider
    {
        string path = @"c:\Test\phone.txt";
        public PhoneCallStatus GetCallStatus(string callId)
        {
            int res = 2;
            foreach (string line in File.ReadAllLines(path))
            {
                var info = line.Split(new char[] { ';' });
                if (string.Compare(info[0], callId) == 0)
                {
                    if (info.Length > 2)
                    {
                        bool b = Int32.TryParse(info[2], out res);
                        if (!b)
                        {
                            res = 2;
                        }
                    }
                    break;
                }
            }
            switch(res)
            {
                case 0:
                    return PhoneCallStatus.Pending;
                case 1:
                    return PhoneCallStatus.Success;
                case 2:
                    return PhoneCallStatus.Failed;
                default:
                    return PhoneCallStatus.Failed;
            }       
        }
        public string GetFailureMessage(string callId)
        {
            string res = "Call ID is not found";
            foreach (string line in File.ReadAllLines(path))
            {
                var info = line.Split(new char[] { ';' });
                if (string.Compare(info[0], callId) == 0)
                {
                    if (info.Length > 2)
                    {
                        res = info[3];
                    }
                    else
                    {
                        res = "Description is not found";
                    }
                    break;
                }
            }
            return res;            
        }
        
        public PhoneCallStatus InitiateCall(string phoneNumber, Guid requestId, Dictionary<string,object> deliveryAttributes)
        {
            // Here should be some logic for performing voice call
            // For testing purposes we just write details in file             
            string info = string.Format("{0};{1};{2};{3}", requestId, phoneNumber, 0, string.Empty);
            using (StreamWriter sw = File.AppendText(path))
            {
                sw.WriteLine(info);                
            }
            return PhoneCallStatus.Pending;    
        }
    }
}
```
### <a name="step-3-backup-the-mfasettingsxml-located-in-the-cprogram-filesmicrosoft-forefront-identity-manager2010service"></a>Шаг 3 Резервное копирование файла MfaSettings.xml, расположенного в папке "C:\Program Files\Microsoft Forefront Identity Manager\2010\Service"

### <a name="step-4-edit-the-mfasettingsxml-file"></a>Шаг 4. Изменение файла MfaSettings.xml

Измените или очистите следующие строки:

- Удалите или очистите все строки записей конфигурации. 

- Обновите или добавьте следующие строки в файл MfaSettings.xml для настраиваемого поставщика служб телефонии. <br>
`<CustomPhoneProvider>C:\Program Files\Microsoft Forefront Identity Manager\2010\Service\CustomPhoneGate.dll</CustomPhoneProvider>`

### <a name="step-5-restart-mim-service"></a>Шаг 5. Перезапуск службы MIM

После перезапуска службы используйте SSPR и (или) PAM для проверки функциональных возможностей с помощью настраиваемого поставщика удостоверений.

> [!NOTE] 
> Чтобы отменить изменения, замените файл MfaSettings.xml файлом резервной копии, созданным на шаге 3.


## <a name="next-steps"></a>Дальнейшие действия

- [Приступая к работе с сервером Многофакторной идентификации Azure](https://docs.microsoft.com/en-us/azure/active-directory/authentication/howto-mfaserver-deploy)
- [Что такое Azure Multi-factor Authentication?](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication)
- [Журнал выпуска версий MIM](./reference/version-history.md)
