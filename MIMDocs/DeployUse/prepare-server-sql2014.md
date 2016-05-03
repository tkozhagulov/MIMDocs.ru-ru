---
# required metadata

title: Настройка сервера управления удостоверениями&#58; SQL Server 2014 | Microsoft Identity Manager
description: Установка SQL Server 2014 в рамках подготовки к установке MIM 2016.
keywords:
author: kgremban
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-manager-2015
ms.service: microsoft-identity-manager
ms.technology: security
ms.assetid: 297df3b3-192e-4ed9-82ed-c95eb5297c84

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: mwahl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Настройка сервера управления удостоверениями: SQL Server 2014

>[!div class="step-by-step"]
["Windows Server 2012 R2](prepare-server-ws2012r2.md)
[SharePoint"](prepare-server-sharepoint.md)

> [!NOTE]
> Во всех примерах ниже **mimservername** представляет имя контроллера домена, **contoso** — имя домена, а **Pass@word1** — пример пароля.

## Установка **SQL Server 2014 (стандартный выпуск)**

1. Запустите **PowerShell** от имени администратора домена.

2. Перейдите в каталог, где находится программа установки SQL Server.

3. Введите следующие команды:

    ```
    .\setup.exe /Q /IACCEPTSQLSERVERLICENSETERMS /ACTION=install /FEATURES=SQL,SSMS /INSTANCENAME=MSSQLSERVER /SQLSVCACCOUNT="contoso\SqlServer" /SQLSVCPASSWORD="Pass@word1"   /AGTSVCSTARTUPTYPE=Automatic /AGTSVCACCOUNT="NT AUTHORITY\Network Service" /SQLSYSADMINACCOUNTS="contoso\Administrator"
    ```

>[!div class="step-by-step"]  
["Windows Server 2012 R2](prepare-server-ws2012r2.md)
[SharePoint"](prepare-server-sharepoint.md)


<!--HONumber=Apr16_HO2-->


