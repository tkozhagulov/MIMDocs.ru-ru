---
title: "Настройка SQL Server для Microsoft Identity Manager 2016 | Документация Майкрософт"
description: "Установка SQL Server 2014 в рамках подготовки к установке MIM 2016."
keywords: 
author: billmath
ms.author: barclayn
manager: mbaldwin
ms.date: 10/12/2017
ms.topic: get-started-article
ms.service: microsoft-identity-manager
ms.technology: security
ms.assetid: 297df3b3-192e-4ed9-82ed-c95eb5297c84
ms.reviewer: mwahl
ms.suite: ems
ms.openlocfilehash: 8a33e09719b8c806de43531d12ea4b65b5cb443a
ms.sourcegitcommit: f077508b5569e2a96084267879c5b6551e1e0905
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/12/2017
---
# <a name="set-up-an-identity-management-server-sql-server-2014"></a>Настройка сервера управления удостоверениями: SQL Server 2014

>[!div class="step-by-step"]
[« Windows Server 2012 R2](prepare-server-ws2012r2.md)
[SharePoint »](prepare-server-sharepoint.md)

> [!NOTE]
> В этом пошаговом руководстве используются примеры имен и значений для компании Contoso. Замените их своими значениями. Пример.
> - Имя контроллера домена — **mimservername**.
> - Имя домена — **contoso**.
> - Пароль — **Pass@word1**

## <a name="install-sql-server-2014-standard-edition"></a>Установка **SQL Server 2014 (стандартный выпуск)**

1. Запустите **PowerShell** от имени администратора домена.

2. Перейдите в каталог, где находится программа установки SQL Server.

3. Введите следующие команды:

    ```
    .\setup.exe /Q /IACCEPTSQLSERVERLICENSETERMS /ACTION=install /FEATURES=SQL,SSMS /INSTANCENAME=MSSQLSERVER /SQLSVCACCOUNT="contoso\SqlServer" /SQLSVCPASSWORD="Pass@word1"   /AGTSVCSTARTUPTYPE=Automatic /AGTSVCACCOUNT="NT AUTHORITY\Network Service" /SQLSYSADMINACCOUNTS="contoso\Administrator"
    ```

>[!div class="step-by-step"]  
[« Windows Server 2012 R2](prepare-server-ws2012r2.md)
[SharePoint »](prepare-server-sharepoint.md)
