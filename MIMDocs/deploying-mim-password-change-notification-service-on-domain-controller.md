---
title: "Развертывание службы уведомлений о смене паролей | Документация Майкрософт"
description: "Получите шаги для установки и настройки службы уведомлений о смене паролей MIM на контроллере домена."
keywords: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 03/23/2017
ms.topic: article
ms.service: microsoft-identity-manager
ms.technology: security
ms.assetid: 97edae12-6f86-4f9f-8620-a95a096e482a
ms.reviewer: mwahl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 54d03fbd03f6c44298139324ea2dc7d945f008bc
ms.openlocfilehash: 1929703baffad4177ea7ea058cb07f44a9c71667
ms.lasthandoff: 01/24/2017


---

# <a name="deploy-the-mim-password-change-notification-service-on-a-domain-controller"></a>Развертывание службы уведомлений о смене паролей MIM на контроллере домена

## <a name="install-the-password-change-notification-service"></a>Установка службы уведомлений о смене паролей
Служба уведомлений о смене паролей (PCNS) устанавливается на контроллерах доменов и позволяет синхронизировать пароли из MIM с другими системами, например сервером каталогов от другого поставщика. Для синхронизации паролей установите PCNS на сервере каждого контроллера домена.

1.  От имени администратора домена войдите на сервер под управлением Windows Server с ролью доменных служб Active Directory.

2.  Скопируйте папку установки службы уведомления о смене паролей на компьютер.

3.  Найдите файл *Password Change Notification Service.msi* , щелкните его правой кнопкой мыши и создайте ярлык.

4.  Найдите файл ярлыка, щелкните его правой кнопкой мыши и выберите пункт **Свойства**.

5.  В поле "Объект" добавьте приставку *msiexec.exe /i* перед путем к MSI-файлу и суффикс *SCHEMAONLY=TRUE* после пути. Например, если папка установки — *C:\PCNS*, то команда для запуска будет выглядеть следующим образом: (все в одной строке).

    ```
    msiexec.exe /i "C:\PCNS\x64\Password Change Notification Service.msi" SCHEMAONLY=TRUE
    ```

6.  Сохраните изменения в файле ярлыка.

7.  Откройте файл ярлыка, чтобы запустить установку службы PCNS в режиме расширения схемы. На следующем экране нажмите кнопку **Далее**.

8.  Вы получите уведомление о том, что программа установки обновит схему Active Directory для службы уведомления о смене паролей. Нажмите кнопку **ОК** , чтобы продолжить обновление схемы.

9. Когда расширение схемы будет завершено и откроется следующий экран, нажмите кнопку **Готово**.

10. Снова откройте файл *Password Change Notification Service.msi* , на этот раз напрямую (строка запуска не требуется).  На следующем экране нажмите кнопку **Далее**.

11. Примите лицензионное соглашение и нажмите кнопку **Далее**.

12. Щелкните, чтобы начать установку.

13. Когда установка будет завершена и откроется следующий экран, нажмите кнопку **Готово**.

14. Перезагрузите компьютер, чтобы изменения службы уведомления о смене паролей MIM вступили в силу. Для этого можно нажать кнопку **Да** в появившемся всплывающем окне или перезагрузить компьютер позже.

## <a name="configuring-the-password-change-notification-service"></a>Настройка службы уведомлений о смене паролей
Когда вы заново подключитесь к серверу DC от имени администратора домена, перейдите в папку *C:\Program Files\Microsoft Password Change Notification.* Запустите программу *pcnscfg.exe*.
