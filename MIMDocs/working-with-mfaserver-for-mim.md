---
title: Активация сценариев PAM или SSPR и с помощью пакета SDK для сервера многофакторной идентификации Azure | Документация Майкрософт
description: Пакет SDK для сервера Многофакторной идентификации Azure можно настроить в качестве второго уровня безопасности при активации ролей в сценариях Privileged Access Management (PAM) и самостоятельного сброса пароля (SSPR).
keywords: ''
author: fimguy
ms.author: billmath
manager: mtillman
ms.date: 09/02/2018
ms.topic: article
ms.service: microsoft-identity-manager
ms.technology: security
ms.assetid: 94a74f1c-2192-4748-9a25-62a526295338
ms.openlocfilehash: 7191e445688cc9e3c5c02b9c6852c869a28a937a
ms.sourcegitcommit: ad0690bd57e3d056397108bf1c8417965d69a32c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/05/2018
ms.locfileid: "43772684"
---
# <a name="use-azure-multi-factor-authentication-server-to-activate-pam-or-sspr"></a>Активация сценариев PAM или SSPR с помощью сервера Многофакторной идентификации
В следующем документе описывается процедура настройки сервера Многофакторной идентификации Azure в качестве второго уровня безопасности при активации ролей в сценариях Privileged Access Management (PAM) и самостоятельного сброса пароля (SSPR).

> [!IMPORTANT]
> В соответствии с объявлением о прекращении поддержки пакета SDK для службы "Многофакторная идентификация Microsoft Azure" этот пакет SDK будет поддерживаться для существующих клиентов до даты прекращения использования — 14 ноября 2018 г. Новые и текущие клиенты больше не смогут скачать этот пакет SDK с классического портала. Чтобы скачать его, вам потребуется обратиться в службу поддержки клиентов Azure и получить созданный для вас пакет учетных данных службы MFA. <br> Группа разработки Майкрософт работает над внесением изменений в MFA путем интеграции с пакетом SDK для сервера MFA.

В этой статье содержатся сведения об обновлении конфигурации и приводятся действия по переходу с пакета SDK для Azure MFA на пакет SDK для сервера Многофакторной идентификации. Эта возможность будет включена в очередное исправление. Следите за объявлениями в разделе с [журналом версий](/reference/version-history.md). 

## <a name="prerequisites"></a>Предварительные условия

Чтобы использовать сервер Многофакторной идентификации с Azure, вам потребуются следующие возможности и компоненты.

- Доступ к Интернету из каждой службы MIM или сервера MFA, предоставляющих PAM или SSPR, для связи со службой Azure MFA.
- Подписка Azure
- Сервер, установленный с помощью пакета SDK для Azure MFA
- Лицензии Azure Active Directory Premium для пользователей-кандидатов или альтернативные средства лицензирования Azure MFA
- Номера телефонов всех пользователей-кандидатов
- Исправление MIM 4.5 или более поздней версии — объявления см. в [журнале версий](/reference/version-history.md)

## <a name="azure-multi-factor-authentication-server-configuration"></a>Настройка сервера Многофакторной идентификации Azure 
> [!NOTE] 
> Для настройки потребуется действительный сертификат SSL, установленный для пакета SDK. 

### <a name="step-1-download-azure-multi-factor-authentication-server-from-the-azure-portal"></a>Шаг 1. Скачивание сервера Многофакторной идентификации Azure на портале Azure 
Войдите на [портал Azure](https://portal.azure.com/) и скачайте сервер MFA Azure.
![working-with-mfaserver-for-mim_downloadmfa](media/working-with-mfaserver-for-mim/working-with-mfaserver-for-mim_downloadmfa.PNG)

### <a name="step-2-generate-activation-credentials"></a>Шаг 2. Создание учетных данных активации
Чтобы создать учетные данные активации, воспользуйтесь ссылкой **Создать учетные данные активации для начала работы**. Сохраните созданные данные для использования в будущем.

### <a name="step-3-install-the-azure-multi-factor-authentication-server"></a>Шаг 3. Установка сервера Многофакторной идентификации Azure
Скачав сервер, [установите](https://docs.microsoft.com/en-us/azure/active-directory/authentication/howto-mfaserver-deploy#install-and-configure-the-mfa-server) его.  Для этого потребуются учетные данные активации. 

### <a name="step-4-create-your-iis-web-application-that-will-host-the-sdk"></a>Шаг 4. Создание веб-приложения IIS, в котором будет размещен пакет SDK
1. Откройте диспетчер служб IIS ![working-with-mfaserver-for-mim_iis.PNG](media/working-with-mfaserver-for-mim/working-with-mfaserver-for-mim_iis.PNG).
2.  Создайте веб-сайт с именем "MIM MFASDK", свяжите его с пустым каталогом. ![working-with-mfaserver-for-mim_sdkweb.PNG](media/working-with-mfaserver-for-mim/working-with-mfaserver-for-mim_sdkweb.PNG)
3. Откройте консоль многофакторной идентификации и щелкните пакет SDK для веб-службы. ![working-with-mfaserver-for-mim_sdkinstall.PNG](media/working-with-mfaserver-for-mim/working-with-mfaserver-for-mim_sdkinstall.PNG)
4. В мастере выполните конфигурацию, выберите "MFASDK MIM" и пул приложений.

> [!NOTE] 
> В мастере будет выведен запрос на создание группы администраторов. Дополнительные сведения см. в документации по серверу Многофакторной идентификации Azure.

5. Далее нужно импортировать учетную запись службы MIM. Откройте консоль многофакторной идентификации и выберите "Пользователи". а. Щелкните "Импорт из Active Directory". б. Перейдите к учетной записи службы "contoso\mimservice". в. Нажмите кнопки "Импортировать" и "Закрыть". ![working-with-mfaserver-for-mim_importmimserviceaccount.PNG](media/working-with-mfaserver-for-mim/working-with-mfaserver-for-mim_importmimserviceaccount.PNG) 
6. Для учетной записи службы выберите параметр включения в консоли многофакторной идентификации. ![working-with-mfaserver-for-mim_enableserviceaccount.PNG](media/working-with-mfaserver-for-mim/working-with-mfaserver-for-mim_enableserviceaccount.PNG)
7. Обновите проверку подлинности служб IIS на веб-сайте "MFASDK MIM". Сначала отключите параметр "Анонимная проверка подлинности", а затем — "Включить проверку подлинности Windows". ![working-with-mfaserver-for-mim_iisconfig.PNG](media/working-with-mfaserver-for-mim/working-with-mfaserver-for-mim_iisconfig.PNG)
8. Последний шаг. Добавьте учетную запись службы MIM в группу "Администраторы PhoneFactor". ![working-with-mfaserver-for-mim_addservicetomfaadmin.PNG](media/working-with-mfaserver-for-mim/working-with-mfaserver-for-mim_addservicetomfaadmin.PNG)

## <a name="configuring-the-mim-service-for-azure-multi-factor-authentication-server"></a>Настройка службы MIM для сервера Многофакторной идентификации Azure 

### <a name="step-1-patch-server-to-452020"></a>Шаг 1. Обновление сервера до версии 4.5.202.0
 
### <a name="step-2-backup-and-open-the-mfasettingsxml-located-in-the-cprogram-filesmicrosoft-forefront-identity-manager2010service"></a>Шаг 2. Резервное копирование и открытие файла MfaSettings.xml, расположенного в папке "C:\Program Files\Microsoft Forefront Identity Manager\2010\Service"

### <a name="step-3-update-the-following-lines"></a>Шаг 3. Обновление строк
1. Удалите или очистите следующие строки записей конфигурации: <br>
<LICENSE_KEY></LICENSE_KEY><br>
<GROUP_KEY></GROUP_KEY><br>
<CERT_PASSWORD></CERT_PASSWORD><br>
<CertFilePath></CertFilePath><br>

2. Обновите или добавьте следующие строки в файл MfaSettings.xml: <br>
`<Username>mimservice@contoso.com</Username>` <br>
`<LOCMFA>true</LOCMFA>`<br>
`<LOCMFASRV>https://CORPSERVICE.contoso.com:9999/MultiFactorAuthWebServiceSdk/PfWsSdk.asmx</LOCMFASRV>`

3. Перезапустите службу MIM и протестируйте функциональные возможности с помощью сервера Многофакторной идентификации Azure.

> [!NOTE] 
> Чтобы отменить изменения, замените файл MfaSettings.xml файлом резервной копии, созданным на шаге 2.


## <a name="next-steps"></a>Дальнейшие действия

-    [Приступая к работе с сервером Многофакторной идентификации Azure](https://docs.microsoft.com/en-us/azure/active-directory/authentication/howto-mfaserver-deploy)
- [Что такое Azure Multi-factor Authentication?](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication)
- [Активация сценариев PAM или SSPR с помощью сервера Многофакторной идентификации](Working-with-custommfaserver-for-mim.md)
- [Журнал выпуска версий MIM](./reference/version-history.md)