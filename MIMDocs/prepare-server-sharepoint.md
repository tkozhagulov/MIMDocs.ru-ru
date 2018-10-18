---
title: Настройка SharePoint для Microsoft Identity Manager 2016 | Документация Майкрософт
description: Установите и настройте SharePoint Foundation для размещения страницы портала MIM.
keywords: ''
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 04/26/2018
ms.topic: get-started-article
ms.prod: microsoft-identity-manager
ms.assetid: c01487f2-3de6-4fc4-8c3a-7d62f7c2496c
ms.reviewer: mwahl
ms.suite: ems
ms.openlocfilehash: 466f5eb7d4aee27336948e15f96087d6ba898170
ms.sourcegitcommit: 7de35aaca3a21192e4696fdfd57d4dac2a7b9f90
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/16/2018
ms.locfileid: "49358641"
---
# <a name="set-up-an-identity-management-server-sharepoint"></a>Настройка сервера управления удостоверениями: SharePoint

> [!div class="step-by-step"]
> [" SQL Server 2016](prepare-server-sql2016.md)
> [Exchange Server "](prepare-server-exchange.md)
> 
> [!NOTE]
> В этом пошаговом руководстве используются примеры имен и значений для компании Contoso. Замените их своими значениями. Пример.
> - Имя контроллера домена — **corpdc**
> - Имя домена — **contoso**.
> - Имя сервера службы MIM — **corpservice**
> - Имя сервера синхронизации MIM — **corpsync**
> - Имя SQL Server — **corpsql**
> - Пароль — <strong>Pass@word1</strong>


## <a name="install-sharepoint-2016"></a>Установка **SharePoint 2016**

> [!NOTE]
> Чтобы установщик скачал необходимые компоненты, требуется подключение к Интернету. Если компьютер находится в виртуальной сети без доступа к Интернету, добавьте на компьютер дополнительный сетевой интерфейс, который предоставляет доступ к Интернету. Это можно отключить после завершения установки.

Выполните следующие действия для установки SharePoint 2016. После завершения установки сервер будет перезагружен.

1.  Запустите **PowerShell** с использованием доменной учетной записи с правами локального администратора на **corpservice** и **sysadmin** на сервере базы данных SQL, используя **contoso\miminstall**.

    -   Перейдите в каталог, в который был извлечен SharePoint.

    -   Введите следующую команду:

        ```
        .\prerequisiteinstaller.exe
        ```

2.  После предварительной установки необходимых для **SharePoint** компонентов установите **SharePoint 2016**, введя следующую команду:

    ```
    .\setup.exe
    ```

3.  Выберите полный тип сервера.

4.  После завершения установки запустите мастер.

## <a name="run-the-wizard-to-configure-sharepoint"></a>Использование мастера для настройки SharePoint

Выполните действия, указанные в **мастере настройки продуктов SharePoint** , чтобы настроить SharePoint для работы с MIM.

1. На вкладке **Подключение к ферме серверов** создайте новую ферму серверов.

2. Обозначьте этот сервер как сервер баз данных **corpsql** для базы данных настроек, а *Contoso\SharePoint* используйте в качестве учетной записи для доступа к базе данных в SharePoint.
3. Создайте пароль для парольной фразы фермы.

4. В мастере настройки рекомендуется выбрать тип [MinRole](https://docs.microsoft.com/sharepoint/install/overview-of-minrole-server-roles-in-sharepoint-server-2016) для **Внешнего интерфейса**

5. Когда мастер настройки завершит задание конфигурации 10 из 10, нажмите кнопку "Готово", после чего откроется веб-браузер.

6. Чтобы продолжить, при появлении запроса пройдите проверку подлинности с использованием учетной записи *Contoso\miminstall* (или аналогичной учетной записи администратора) во всплывающем окне Internet Explorer.

7. В веб-мастере настройки (в самом веб-приложении) щелкните **Cancel/Skip** (Отмена/Пропустить).


## <a name="prepare-sharepoint-to-host-the-mim-portal"></a>Подготовка SharePoint для размещения портала MIM

> [!NOTE]
> Изначально протокол SSL не будет настроен. Обязательно настройте протокол SSL или его аналог, прежде чем разрешать доступ к порталу.

1. Запустите **командную консоль SharePoint 2016** и выполните следующий сценарий PowerShell, чтобы создать **веб-приложение SharePoint 2016**.

    ```
    New-SPManagedAccount ##Will prompt for new account enter contoso\mimpool 
    $dbManagedAccount = Get-SPManagedAccount -Identity contoso\mimpool
    New-SpWebApplication -Name "MIM Portal" -ApplicationPool "MIMAppPool" -ApplicationPoolAccount $dbManagedAccount -AuthenticationMethod "Kerberos" -Port 80 -URL http://mim.contoso.com
    ```

    > [!NOTE]
    > Появится предупреждение о том, что используется классический метод проверки подлинности Windows, и для выполнения завершающей команды может потребоваться несколько минут. По завершении в выходных данных будет указан URL-адрес нового портала. Не закрывайте окно **командной консоли SharePoint 2016**, чтобы перейти к нему позже.

2. Запустите командную консоль SharePoint 2016 и выполните следующий сценарий PowerShell, чтобы создать **семейство веб-сайтов SharePoint**, связанное с веб-приложением.

   ```
    $t = Get-SPWebTemplate -compatibilityLevel 15 -Identity "STS#1"
    $w = Get-SPWebApplication http://mim.contoso.com/
    New-SPSite -Url $w.Url -Template $t -OwnerAlias contoso\miminstall -CompatibilityLevel 15 -Name "MIM Portal"
    $s = SpSite($w.Url)
    $s.CompatibilityLevel
   ```

   > [!NOTE]
   > Убедитесь, что для переменной *CompatibilityLevel* установлено значение 15. Если результат не равен 15, то семейство веб-сайтов не соответствует действующей версии программы, поэтому удалите это семейство веб-сайтов и создайте его еще раз.

3. Отключите **SharePoint Server-Side Viewstate** (Просмотр состояния сервера SharePoint на стороне сервера), а также задачу "Анализ работоспособности SharePoint (каждый час, Microsoft SharePoint Foundation Timer, все серверы)", выполнив следующие команды PowerShell в **Консоли управления SharePoint 2016**:

   ```
   $contentService = [Microsoft.SharePoint.Administration.SPWebService]::ContentService;
   $contentService.ViewStateOnServer = $false;
   $contentService.Update();
   Get-SPTimerJob hourly-all-sptimerservice-health-analysis-job | disable-SPTimerJob
   ```

4. На сервере управления идентификаторами откройте новую вкладку веб-браузера, перейдите к http://mim.contoso.com/ и войдите под именем *contoso\miminstall*.  Откроется пустой сайт SharePoint под названием *Портал MIM* .

    ![Портал MIM показан на рис. http://mim.contoso.com/](media/prepare-server-sharepoint/MIM_DeploySP1new.png)

5. Скопируйте URL-адрес, а затем в Internet Explorer откройте **Свойства браузера**, перейдите на вкладку **Безопасность**, выберите **Местная интрасеть** и нажмите кнопку **Сайты**.

    ![Изображение для свойств браузера](media/MIM-DeploySP2.png)

6. В окне **Локальная интрасеть** нажмите кнопку **Дополнительно** и вставьте скопированный URL-адрес в текстовое поле **Добавить в зону следующий узел**. Нажмите кнопку **Добавить** и закройте окна.

7. Откройте средство **Администрирование**, перейдите в раздел **Службы**, найдите службу администрирования SharePoint и запустите ее, если она еще не запущена.

> [!div class="step-by-step"]  
> [" SQL Server 2016](prepare-server-sql2016.md)
> [Exchange Server "](prepare-server-exchange.md)
