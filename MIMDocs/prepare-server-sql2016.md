---
title: Настройка SQL Server для Microsoft Identity Manager 2016 с пакетом обновления 1 (SP1) | Документация Майкрософт
description: Установка SQL Server 2016 в рамках подготовки к установке MIM 2016.
keywords: ''
author: billmath
ms.author: barclayn
manager: mbaldwin
ms.date: 04/26/2018
ms.topic: get-started-article
ms.service: microsoft-identity-manager
ms.technology: security
ms.assetid: 297df3b3-192e-4ed9-82ed-c95eb5297c84
ms.reviewer: mwahl
ms.suite: ems
ms.openlocfilehash: e2006ca2a74f8c974f6019004aeaefdc73069fa6
ms.sourcegitcommit: 32d9a963a4487a8649210745c97a3254645e8744
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/27/2018
---
# <a name="set-up-an-identity-management-server-sql-server-2016"></a>Настройка сервера управления удостоверениями: SQL Server 2016

>[!div class="step-by-step"]
[« Windows Server 2016](prepare-server-ws2016.md)
[SharePoint »](prepare-server-sharepoint.md)

> [!NOTE]
> В этом пошаговом руководстве используются примеры имен и значений для компании Contoso. Замените их своими значениями. Пример.
> - Имя контроллера домена — **corpdc**
> - Имя домена — **contoso**.
> - Имя сервера службы MIM — **corpservice**
> - Имя сервера синхронизации MIM — **corpsync**
> - Имя SQL Server — **corpsql**
> - Пароль — **Pass@word1**

## <a name="install-sql-server-2016-standardenterprise-edition"></a>Установка **SQL Server 2016 (Выпуск Enterprise или Standard)**

1. Запустите **PowerShell** от имени администратора домена.

2. Перейдите в каталог, где находится программа установки SQL Server.

3. Введите следующие команды:

    ```
    .\setup.exe /Q /IACCEPTSQLSERVERLICENSETERMS /ACTION=install /FEATURES=SQL /INSTANCENAME=MSSQLSERVER /SQLSVCACCOUNT="contoso\SqlServer" /SQLSVCPASSWORD="Pass@word1"   /AGTSVCSTARTUPTYPE=Automatic /AGTSVCACCOUNT="NT AUTHORITY\Network Service" /SQLSYSADMINACCOUNTS="contoso\Administrator"

More info SQL deployment accounts and services can be found [here](https://docs.microsoft.com/en-us/sql/database-engine/configure-windows/configure-windows-service-accounts-and-permissions?view=sql-server-2017)
> [!NOTE]
> SSMS is no longer included in SQL 2016 downlaod details can be found [here](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-2017)    ```

>[!div class="step-by-step"]  
[« Windows Server 2016](prepare-server-ws2016.md)
[SharePoint »](prepare-server-sharepoint.md)
