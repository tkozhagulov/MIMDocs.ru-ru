---
title: "Развертывание PAM. Шаг 3 — сервер PAM | Документация Майкрософт"
description: "Подготовьте сервер PAM, где будет размещаться SQL и SharePoint для развертывания Privileged Access Management."
keywords: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 03/15/2017
ms.topic: article
ms.service: microsoft-identity-manager
ms.technology: active-directory-domain-services
ms.assetid: 68ec2145-6faa-485e-b79f-2b0c4ce9eff7
ROBOTS: noindex,nofollow
ms.reviewer: mwahl
ms.suite: ems
ms.translationtype: Human Translation
ms.sourcegitcommit: bfc73723bdd3a49529522f78ac056939bb8025a3
ms.openlocfilehash: 9a262a256062688542040827653a7df8d82e1044
ms.contentlocale: ru-ru
ms.lasthandoff: 07/10/2017


---

<a id="step-3--prepare-a-pam-server" class="xliff"></a>
# Шаг 3. Подготовка сервера PAM

>[!div class="step-by-step"]
[« Шаг 2](step-2-prepare-priv-domain-controller.md)
[Шаг 4 »](step-4-install-mim-components-on-pam-server.md)

<a id="install-windows-server-2012-r2" class="xliff"></a>
## Установка Windows Server 2012 R2
Установите Windows Server 2012 R2, а именно Windows Server 2012 R2 Standard (сервер с графическим интерфейсом пользователя) x64, на третьей виртуальной машине, чтобы создать компьютер *PAMSRV*. Поскольку на этом компьютере будут установлены SQL Server и SharePoint 2013, требуется как минимум 8 ГБ ОЗУ.

1. Выберите редакцию **Windows Server 2012 R2 Standard (сервер с графическим интерфейсом пользователя) x64**.

    ![Выбор Windows Server Standard с графическим интерфейсом пользователя — снимок экрана](media/PAM_GS_Select_WS2012.png)

2. Просмотрите и примите условия лицензионного соглашения.

3.  Поскольку диск будет пустым, выберите **Выборочная: установка только Windows** и используйте **неинициализированное дисковое пространство**.

4.  Войдите на новый компьютер от имени его администратора.  С помощью панели управления присвойте ему статический IP-адрес в виртуальной сети, настройте этот сетевой интерфейс для отправки запросов DNS на IP-адрес PRIVDC и задайте имя компьютера *PAMSRV*.  Для этого потребуется перезагрузить сервер.

5.  Если в виртуальной сети нет доступа к Интернету, добавьте на компьютер дополнительный сетевой интерфейс, который предоставляет доступ к Интернету.  Это потребуется для установки SharePoint. По завершении этого этапа интерфейс можно отключить.

6.  После перезагрузки сервера войдите от имени администратора. С помощью панели управления настройте компьютер для проверки обновлений и установите все необходимые обновления.  Для этого может потребоваться перезагрузка сервера.

7.  После перезагрузки сервера войдите в систему как администратор, откройте панель управления и присоедините PAMSRV к домену PRIV (priv.contoso.local).  Для этого потребуется указать имя пользователя и учетные данные администратора домена PRIV, например PRIV\Administrator. Когда появится приветствие, закройте диалоговое окно и перезагрузите сервер.


<a id="add-the-web-server-iis-and-application-server-roles" class="xliff"></a>
### Добавление ролей веб-сервера (IIS) и сервера приложений
Добавьте роли Web Server (IIS) и Application Server, компоненты .NET Framework 3.5, модуль Active Directory для Windows PowerShell и другие компоненты, необходимые SharePoint.

1.  Выполните вход как администратор домена PRIV (PRIV\Administrator) и запустите PowerShell.

2.  Введите следующие команды: Обратите внимание, что может потребоваться указать другое расположение исходных файлов для компонентов .NET Framework 3.5. Эти компоненты обычно отсутствуют при установке Windows Server, но доступны в папке параллельного размещения (SxS), находящейся в папке sources на установочном диске ОС, например "d:\Sources\SxS\".

    ```
    import-module ServerManager
    Install-WindowsFeature Web-WebServer, Net-Framework-Features,
    rsat-ad-powershell,Web-Mgmt-Tools,Application-Server,
    Windows-Identity-Foundation,Server-Media-Foundation,
    Xps-Viewer –includeallsubfeature -restart -source d:\sources\SxS
    ```

<a id="configure-the-server-security-policy" class="xliff"></a>
### Настройка политики безопасности сервера
Настройте политику безопасности сервера так, чтобы новые учетные записи могли работать как службы.

1.  Запустите программу **локальной политики безопасности** .   
2.  Перейдите в раздел **Локальные политики** > **Предоставление прав пользователям**.  
3.  В области сведений щелкните правой кнопкой мыши команду **Вход в качестве службы**и выберите пункт **Свойства**.  
4.  Нажмите кнопку **Добавить пользователя или группу** и введите в разделе "Имена пользователей и групп" *priv\mimmonitor; priv\MIMService; priv\SharePoint; priv\mimcomponent; priv\SqlServer*. Щелкните **Проверить имена** и нажмите кнопку **ОК**.  

5.  Нажмите кнопку **ОК**, чтобы закрыть окно "Свойства".  
6.  В области сведений щелкните правой кнопкой мыши команду **Отказать в доступе к этому компьютеру из сети** и выберите пункт **Свойства**.  
7.  Нажмите кнопку **Добавить пользователя или группу**, введите в разделе "Имена пользователей и групп" *priv\mimmonitor; priv\MIMService; priv\mimcomponent* и нажмите кнопку **ОК**.  
8.  Нажмите кнопку **ОК**, чтобы закрыть окно "Свойства".  

9. В области сведений щелкните правой кнопкой мыши команду **Запретить локальный вход** и выберите пункт **Свойства**.  
10. Нажмите кнопку **Добавить пользователя или группу**, введите в разделе "Имена пользователей и групп" *priv\mimmonitor; priv\MIMService; priv\mimcomponent* и нажмите кнопку **ОК**.  
11. Нажмите кнопку **ОК**, чтобы закрыть окно "Свойства".  
12. Закройте окно "Локальная политика безопасности".  

13. Откройте панель управления и выберите пункт **Учетные записи пользователей**.  
14. Щелкните **Предоставить общий доступ к этому компьютеру**.  
15. Нажмите кнопку **Добавить**, введите имя пользователя *MIMADMIN* в домене *PRIV*, а на следующем экране мастера нажмите кнопку **Добавить этого пользователя с правами администратора**.  
16. Нажмите кнопку **Добавить**, введите имя пользователя *SharePoint* в домене *PRIV*, а на следующем экране мастера нажмите кнопку **Добавить этого пользователя с правами администратора**.  
17. Закройте панель управления.  

<a id="change-the-iis-configuration" class="xliff"></a>
### Изменение конфигурации IIS
Изменить конфигурацию IIS для того, чтобы приложения могли использовать режим проверки подлинности Windows, можно двумя способами. Войдите в систему как MIMAdmin, а затем выберите один из следующих вариантов.

Если вы хотите использовать PowerShell:
1.  Щелкните PowerShell правой кнопкой мыши и выберите пункт **Запуск от имени администратора**.  
2.  Остановите службы IIS и разблокируйте параметры узла приложения с помощью этих команд:  
    ```
    iisreset /STOP
    C:\Windows\System32\inetsrv\appcmd.exe unlock config /section:windowsAuthentication -commit:apphost
    iisreset /START
    ```

Если вы хотите использовать текстовый редактор, например Блокнот:   
1. Откройте файл **C:\Windows\System32\inetsrv\config\applicationHost.config**   
2. Прокрутите файл вниз до строки 82. Тег **overrideModeDefault** должен иметь значение **<section name="windowsAuthentication" overrideModeDefault="Deny" />**  
3. Измените значение **overrideModeDefault** на *Разрешить*  
4. Сохраните этот файл и перезапустите IIS с помощью команды PowerShell `iisreset /START`

<a id="install-sql-server" class="xliff"></a>
## Установите SQL Server
Если в среде бастиона еще не присутствует SQL Server, установите SQL Server 2012 (пакет обновления 1 или более поздней версии) или SQL Server 2014. Ниже предполагается, что используется SQL 2014.

1. Выполните вход как MIMAdmin.
2. Щелкните PowerShell правой кнопкой мыши и выберите пункт **Запуск от имени администратора**.   
3. Перейдите в каталог, где находится программа установки SQL Server.  
4. Введите следующую команду:  
    ```
    .\setup.exe /Q /IACCEPTSQLSERVERLICENSETERMS /ACTION=install /FEATURES=SQL,SSMS /INSTANCENAME=MSSQLSERVER /SQLSVCACCOUNT="PRIV\SqlServer" /SQLSVCPASSWORD="Pass@word1" /AGTSVCSTARTUPTYPE=Automatic /AGTSVCACCOUNT="NT AUTHORITY\Network Service" /SQLSYSADMINACCOUNTS="PRIV\MIMAdmin"
    ```

<a id="install-sharepoint-foundation-2013" class="xliff"></a>
## Установка SharePoint Foundation 2013

С помощью установщика SharePoint Foundation 2013 с пакетом обновления 1 (SP1) установите необходимое программное обеспечение для SharePoint на компьютере PAMSRV.

> [!NOTE]
> Чтобы установщик скачал необходимые компоненты, требуется подключение к Интернету. После их установки сервер перезагрузится.

1. Щелкните PowerShell правой кнопкой мыши и выберите пункт **Запуск от имени администратора**.  
2. Перейдите в каталог, в который был извлечен SharePoint.  
3. Введите команду `.\prerequisiteinstaller.exe`.

После установки необходимых для SharePoint компонентов установите SharePoint Foundation 2013 с пакетом обновления 1 (SP1).

1.  Щелкните PowerShell правой кнопкой мыши и выберите пункт **Запуск от имени администратора**.  
2.  Перейдите в каталог, в который был извлечен SharePoint.  
3.  Введите команду `.\setup.exe`.  
4.  Выберите **полный тип сервера** .  
5.  После завершения установки запустите мастер.  

<a id="configure-sharepoint" class="xliff"></a>
### Настройка SharePoint
Запустите мастер настройки продуктов SharePoint, чтобы настроить SharePoint.

1.  На вкладке "Подключение к ферме серверов" выберите пункт **Создать ферму серверов**.  
2.  Укажите **PAMSRV** как сервер баз данных для базы данных конфигурации, а **PRIV\\SharePoint** как учетную запись доступа к базе данных для SharePoint.  
3.  В качестве пароля введите парольную фразу фермы (он не будет использоваться в этом пошаговом руководстве).  
4.  А пока примите остальные значения по умолчанию мастера настройки SharePoint, чтобы создать ферму из одного сервера.    
5.  Когда мастер настройки завершит задание конфигурации 10 из 10, нажмите кнопку **Готово** и откроется веб-браузер.  
6.  Чтобы продолжить, во всплывающем окне Internet Explorer пройдите проверку подлинности как администратор домена (PRIV\MIMAdmin).  
7.  Запустите мастер в веб-приложении, чтобы настроить ферму SharePoint.  
8.  Выберите использование существующей управляемой учетной записи (PRIV\SharePoint), снимите флажки, чтобы отключить все дополнительные службы, и нажмите кнопку **Далее**.  
9. В окне создания семейства веб-сайтов нажмите кнопку **Пропустить**, а затем **Готово**.  

<a id="create-a-sharepoint-foundation-2013-web-application" class="xliff"></a>
## Создание веб-приложения SharePoint Foundation 2013
После завершения работы мастера создайте с помощью PowerShell веб-приложение SharePoint Foundation 2013 для размещения портала MIM. Поскольку это пошаговое руководство предназначено для демонстрации, SSL не включается.

1.  Щелкните консоль управления SharePoint 2013 правой кнопкой мыши, выберите пункт **Запуск от имени администратора** и запустите следующий сценарий PowerShell:

    ```
    $dbManagedAccount = Get-SPManagedAccount -Identity PRIV\SharePoint
    New-SpWebApplication -Name "MIM Portal" -ApplicationPool "MIMAppPool"            -ApplicationPoolAccount $dbManagedAccount -AuthenticationMethod "Kerberos" -Port 82 -URL http://PAMSRV.priv.contoso.local
    ```

2. Появится предупреждение о том, что используется классический метод проверки подлинности Windows, и для выполнения завершающей команды может потребоваться несколько минут.  По завершении в выходных данных будет указан URL-адрес нового портала.

> [!NOTE]
> Не закрывайте окно командной консоли SharePoint 2013 — оно вам потребуется на следующем шаге.

<a id="create-a-sharepoint-site-collection" class="xliff"></a>
## Создание семейства веб-сайтов SharePoint
Создайте семейство веб-сайтов SharePoint, связанное с этим веб-приложением, для размещения портала MIM.

1.  Запустите **командную консоль SharePoint 2013**, если она еще не открыта, и выполните следующий сценарий PowerShell:

    ```
    $t = Get-SPWebTemplate -compatibilityLevel 14 -Identity "STS#1"
    $w = Get-SPWebApplication http://pamsrv.priv.contoso.local:82
    New-SPSite -Url $w.Url -Template $t -OwnerAlias PRIV\MIMAdmin                -CompatibilityLevel 14 -Name "MIM Portal" -SecondaryOwnerAlias PRIV\BackupAdmin
    $s = SpSite($w.Url)
    $s.AllowSelfServiceUpgrade = $false
    $s.CompatibilityLevel
    ```

    Убедитесь, что переменная **CompatibilityLevel** имеет значение *14*. Если выдается значение *15*, то семейство веб-сайтов не было создано для версии 2010. Удалите семейство веб-сайтов и создайте его заново.

2.  В **командной консоли SharePoint 2013** выполните следующие команды PowerShell: Это приведет к отключению состояния просмотра на стороне сервера SharePoint Server и задачам SharePoint **Задание анализа работоспособности (каждый час, Microsoft SharePoint Foundation Timer, все серверы)**.

    ```
    $contentService = [Microsoft.SharePoint.Administration.SPWebService]::ContentService;
    $contentService.ViewStateOnServer = $false;
    $contentService.Update();
    Get-SPTimerJob hourly-all-sptimerservice-health-analysis-job | disable-SPTimerJob
    ```

<a id="change-update-settings" class="xliff"></a>
## Изменение параметров обновления

1. Откройте панель управления, перейдите к разделу **Центр обновления Windows** и щелкните **Изменить параметры**.  
2. Измените параметры так, чтобы получать обновления центра обновления Windows и обновления других продуктов из центра обновления Майкрософт.  
3. Прежде чем продолжить, повторно проверьте наличие обновлений и убедитесь, что все имеющиеся важные обновления установлены.

<a id="set-the-website-as-the-local-intranet" class="xliff"></a>
## Настройка веб-сайта для локальной интрасети

1. Запустите Internet Explorer и откройте новую вкладку веб-браузера.
2. Перейдите по адресу http://pamsrv.priv.contoso.local:82/ и войдите в систему как PRIV\MIMAdmin.  Откроется пустой сайт SharePoint с именем "Портал MIM".  
3. В Internet Explorer откройте **Свойства браузера**, перейдите на вкладку **Безопасность**, выберите пункт **Местная интрасеть** и добавьте веб-сайт `http://pamsrv.priv.contoso.local:82/`.

Если войти не удается, может потребоваться обновить имена участников-служб Kerberos, созданных ранее на [шаге 2](step-2-prepare-priv-domain-controller.md).

<a id="start-the-sharepoint-administration-service" class="xliff"></a>
## Запуск службы администрирования SharePoint

В разделе **Службы** (в разделе "Средства администрирования") запустите службу **Администрирование SharePoint**, если она не запущена.

На шаге 4 начнется установка компонентов MIM на сервере PAM.

>[!div class="step-by-step"]
[« Шаг 2](step-2-prepare-priv-domain-controller.md)
[Шаг 4 »](step-4-install-mim-components-on-pam-server.md)

