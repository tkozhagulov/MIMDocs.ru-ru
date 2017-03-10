---
title: "Настройка Windows Server 2012 R2 для MIM 2016 | Документация Майкрософт"
description: "Пошаговые инструкции и сведения о минимальных требованиях для подготовки Windows Server 2012 RS к работе с MIM 2016."
keywords: 
author: kgremban
ms.author: kgremban
manager: femila
ms.date: 01/23/2017
ms.topic: get-started-article
ms.service: microsoft-identity-manager
ms.technology: security
ms.assetid: 51507d0a-2aeb-4cfd-a642-7c71e666d6cd
ms.reviewer: mwahl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 3623bffb099a83d0eba47ba25e9777c3d590e529
ms.openlocfilehash: 1cb0d6cd310372ecaeff47c9cc4461ebc43b3390


---

# <a name="set-up-an-identity-management-server-windows-server-2012-r2"></a>Настройка сервера управления удостоверениями: Windows Server 2012 R2

>[!div class="step-by-step"]
[« Подготовка домена](preparing-domain.md)
[SQL Server 2014 »](prepare-server-sql2014.md)

> [!NOTE]
> В этом пошаговом руководстве используются примеры имен и значений для компании Contoso. Замените их своими значениями. Пример.
> - Имя контроллера домена — **mimservername**.
> - Имя домена — **contoso**.
> - Пароль — **Pass@word1**

## <a name="join-windows-server-2012-r2-to-your-domain"></a>Присоединение Windows Server 201  R2 к домену

Создайте машину Windows Server 2012 R2 не менее чем с 8 ГБ ОЗУ. При установке выберите редакцию "Windows Server 2012 R2 Standard (сервер с графическим интерфейсом пользователя) x64".

1. Войдите на новый компьютер от имени администратора.

2. С помощью панели управления назначьте компьютеру статический IP-адрес в сети. Настройте этот сетевой интерфейс для отправки запросов DNS на IP-адрес контроллера домена из предыдущего шага и задайте имя компьютера **corpIDM**.  Для этого потребуется перезагрузить сервер.

3. Откройте панель управления и присоедините компьютер к домену *contoso.local*, настроенному в предыдущем шаге.  Для этого требуется указать имя пользователя и учетные данные администратора домена, например *Contoso\Administrator*.  Когда появится приветствие, закройте диалоговое окно и снова перезагрузите сервер.

4. Войдите на компьютер *CorpIDM* в качестве администратора домена, например *Contoso\Administrator*.

5. Откройте окно PowerShell от имени администратора и введите следующую команду, чтобы обновить компьютер согласно параметрам групповой политики.

    ```
    gpupdate /force /target:computer
    ```

    Не позже чем через минуту обновление будет завершено с сообщением "Обновление политики для компьютера успешно завершено".

6. Добавьте роли **Веб-сервер (IIS** и **Сервер приложений**, компоненты **.NET Framework** 3.5, 4.0 и 4.5, а также модуль **Active Directory для Windows PowerShell**.

    ![Изображение для компонентов PowerShell](media/MIM-DeployWS2.png)

7. В PowerShell введите следующие команды: Обратите внимание, что может потребоваться указать другое расположение исходных файлов для компонентов **.NET Framework** 3.5. Эти компоненты обычно отсутствуют при установке Windows Server, но доступны в папке параллельного размещения (SxS), находящейся в папке sources на установочном диске ОС, например "*d:\Sources\SxS\*".

    ```
    import-module ServerManager
    Install-WindowsFeature Web-WebServer, Net-Framework-Features,rsat-ad-powershell,Web-Mgmt-Tools,Application-Server,Windows-Identity-Foundation,Server-Media-Foundation,Xps-Viewer –includeallsubfeature -restart -source d:\sources\SxS
    ```

## <a name="configure-the-server-security-policy"></a>Настройка политики безопасности сервера

Настройте политику безопасности сервера так, чтобы новые учетные записи могли работать как службы.

1. Запуск программы локальной политики безопасности

2. Перейдите в раздел **Локальные политики > Предоставление прав пользователям**.

3. В области сведений щелкните правой кнопкой мыши команду **Вход в качестве службы**и выберите пункт **Свойства**.

    ![Изображение для локальной политики безопасности](media/MIM-DeployWS3.png)

4. Щелкните **Добавить пользователя или группу**, после чего в текстовом поле введите `contoso\MIMSync; contoso\MIMMA; contoso\MIMService; contoso\SharePoint; contoso\SqlServer; contoso\MIMSSPR`, нажмите кнопку **Проверить имена**, а затем **ОК**.

5. Нажмите кнопку**ОК** , чтобы закрыть окно свойств **Вход в качестве службы**.

6.  В области сведений щелкните правой кнопкой мыши команду **Отказать в доступе к этому компьютеру из сети** и выберите пункт **Свойства**.

7. Щелкните **Добавить пользователя или группу**, после чего введите `contoso\MIMSync; contoso\MIMService` в текстовом поле и нажмите кнопку **ОК**.

8. Нажмите кнопку **ОК**, чтобы закрыть окно свойств **Отказать в доступе к этому компьютеру из сети**.

9. В области сведений щелкните правой кнопкой мыши команду **Запретить локальный вход** и выберите пункт **Свойства**.

10. Щелкните **Добавить пользователя или группу**, после чего введите `contoso\MIMSync; contoso\MIMService` в текстовом поле и нажмите кнопку **ОК**.

11. Нажмите **ОК** , чтобы закрыть окно свойств **Запретить локальный вход**.

12. Закройте окно "Локальная политика безопасности".


## <a name="change-the-iis-windows-authentication-mode"></a>Измените режим проверки подлинности Windows для служб IIS.

1.  Откройте окно PowerShell.

2.  Остановите службы IIS с помощью команды *iisreset /STOP*.

    ```
    iisreset /STOP
    C:\Windows\System32\inetsrv\appcmd.exe unlock config /section:windowsAuthentication -commit:apphost
    iisreset /START
    ```

>[!div class="step-by-step"]  
[« Подготовка домена](preparing-domain.md)
[SQL Server 2014 »](prepare-server-sql2014.md)



<!--HONumber=Jan17_HO4-->


