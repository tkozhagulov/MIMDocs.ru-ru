---
title: "Настройка SharePoint для Microsoft Identity Manager 2016 | Документация Майкрософт"
description: "Установите и настройте SharePoint Foundation для размещения страницы портала MIM."
keywords: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 03/23/2017
ms.topic: get-started-article
ms.service: microsoft-identity-manager
ms.technology: security
ms.assetid: c01487f2-3de6-4fc4-8c3a-7d62f7c2496c
ms.reviewer: mwahl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 3623bffb099a83d0eba47ba25e9777c3d590e529
ms.openlocfilehash: 2af432036033f8914d00228cd3d2d1af84f13054
ms.lasthandoff: 01/24/2017


---

# <a name="set-up-an-identity-management-server-sharepoint"></a>Настройка сервера управления удостоверениями: SharePoint

>[!div class="step-by-step"]
[« SQL Server 2014](prepare-server-sql2014.md)
[Exchange Server »](prepare-server-exchange.md)

> [!NOTE]
> В этом пошаговом руководстве используются примеры имен и значений для компании Contoso. Замените их своими значениями. Пример.
> - Имя контроллера домена — **mimservername**.
> - Имя домена — **contoso**.
> - Пароль — **Pass@word1**


## <a name="install-sharepoint-foundation-2013-with-sp1"></a>Установка **SharePoint Foundation 2013 с пакетом обновления 1 (SP1)**

> [!NOTE]
> Чтобы установщик скачал необходимые компоненты, требуется подключение к Интернету. Если компьютер находится в виртуальной сети без доступа к Интернету, добавьте на компьютер дополнительный сетевой интерфейс, который предоставляет доступ к Интернету. Это можно отключить после завершения установки.

Выполните следующие действия, чтобы установить SharePoint Foundation 2013 с пакетом обновления 1 (SP1). После завершения установки сервер будет перезагружен.

1.  Запустите **PowerShell** от имени администратора домена.

    -   Перейдите в каталог, в который был извлечен SharePoint.

    -   Введите следующую команду:

        ```
        .\prerequisiteinstaller.exe
        ```

2.  После установки необходимых для **SharePoint** компонентов установите **SharePoint Foundation 2013 с пакетом обновления 1 (SP1)** , введя следующую команду:

    ```
    .\setup.exe
    ```

3.  Выберите полный тип сервера.

4.  После завершения установки запустите мастер.

## <a name="run-the-wizard-to-configure-sharepoint"></a>Использование мастера для настройки SharePoint

Выполните действия, указанные в **мастере настройки продуктов SharePoint** , чтобы настроить SharePoint для работы с MIM.

1. На вкладке **Подключение к ферме серверов** создайте новую ферму серверов.

2. Укажите этот сервер как сервер баз данных для базы данных конфигурации, а *Contoso\SharePoint* — как учетную запись доступа к базе данных для SharePoint.

3. Создайте пароль для парольной фразы фермы.

4. Когда мастер настройки завершит задание конфигурации 10 из 10, нажмите кнопку "Готово", и откроется веб-браузер.

5. Чтобы продолжить, во всплывающем окне Internet Explorer выполните вход с использованием *Contoso\Administrator* (или аналогичной учетной записи администратора домена).

6. Запустите мастер (в веб-приложении), чтобы настроить ферму SharePoint.

7. Выберите использование имеющейся управляемой учетной записи (*Contoso\SharePoint*) и нажмите кнопку **Далее**.

8. В окне **Создание семейства веб-сайтов** нажмите кнопку **Пропустить**.  Затем нажмите кнопку **Готово**.

## <a name="prepare-sharepoint-to-host-the-mim-portal"></a>Подготовка SharePoint для размещения портала MIM

> [!NOTE]
> Изначально протокол SSL не будет настроен. Обязательно настройте протокол SSL или его аналог, прежде чем разрешать доступ к порталу.

1. Запустите **командную консоль SharePoint 2013** и выполните следующий сценарий PowerShell, чтобы создать **веб-приложение SharePoint Foundation 2013**.

    ```
    $dbManagedAccount = Get-SPManagedAccount -Identity contoso\SharePoint
    New-SpWebApplication -Name "MIM Portal" -ApplicationPool "MIMAppPool" -ApplicationPoolAccount $dbManagedAccount -AuthenticationMethod "Kerberos" -Port 82 -URL http://corpidm.contoso.local
    ```

    > [!NOTE]
    > Появится предупреждение о том, что используется классический метод проверки подлинности Windows, и для выполнения завершающей команды может потребоваться несколько минут. По завершении в выходных данных будет указан URL-адрес нового портала. Не закрывайте окно **командной консоли SharePoint 2013**, чтобы перейти к нему позже.

2. Запустите командную консоль SharePoint 2013 и выполните следующий сценарий PowerShell, чтобы создать **семейство веб-сайтов SharePoint**, связанное с веб-приложением.

  ```
  $t = Get-SPWebTemplate -compatibilityLevel 14 -Identity "STS#1"
  $w = Get-SPWebApplication http://corpidm.contoso.local:82
  New-SPSite -Url $w.Url -Template $t -OwnerAlias contoso\Administrator
  -CompatibilityLevel 14 -Name "MIM Portal" -SecondaryOwnerAlias contoso\BackupAdmin
  $s = SpSite($w.Url)
  $s.AllowSelfServiceUpgrade = $false
  $s.CompatibilityLevel
  ```

  > [!NOTE]
  > Убедитесь, что в переменной *CompatibilityLevel* содержится результат "14". Если результат равен "15", то семейство веб-сайтов не было создано для версии 2010. Удалите семейство веб-сайтов и создайте его заново.

3. Отключите **состояние просмотра на стороне сервера SharePoint Server** и задачу SharePoint "Задание анализа работоспособности (каждый час, Microsoft SharePoint Foundation Timer, все серверы)", выполнив следующие команды PowerShell в **командной консоли SharePoint 2013**:

  ```
  $contentService = [Microsoft.SharePoint.Administration.SPWebService]::ContentService;
  $contentService.ViewStateOnServer = $false;
  $contentService.Update();
  Get-SPTimerJob hourly-all-sptimerservice-health-analysis-job | disable-SPTimerJob
  ```

4. На сервере управления удостоверениями откройте новую вкладку веб-браузера, перейдите по адресу http://localhost:82/ и войдите в качестве *contoso\Administrator*.  Откроется пустой сайт SharePoint под названием *Портал MIM* .

    ![Изображение для портала MIM по адресу http://localhost:82/](media/MIM-DeploySP1.png)

5. Скопируйте URL-адрес, а затем в Internet Explorer откройте **Свойства браузера**, перейдите на вкладку **Безопасность**, выберите **Местная интрасеть** и нажмите кнопку **Сайты**.

    ![Изображение для свойств браузера](media/MIM-DeploySP2.png)

6. В окне **Локальная интрасеть** нажмите кнопку **Дополнительно** и вставьте скопированный URL-адрес в текстовое поле **Добавить в зону следующий узел**. Нажмите кнопку **Добавить** и закройте окна.

7. Откройте средство **Администрирование**, перейдите в раздел **Службы**, найдите службу администрирования SharePoint и запустите ее, если она еще не запущена.

>[!div class="step-by-step"]  
[« SQL Server 2014](prepare-server-sql2014.md)
[Exchange Server »](prepare-server-exchange.md)

