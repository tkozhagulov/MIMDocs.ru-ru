---
title: Настройка SQL Server для Microsoft Identity Manager 2016 с пакетом обновления 1 (SP1) | Документация Майкрософт
description: Установка SQL Server 2016 в рамках подготовки к установке MIM 2016.
keywords: ''
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 04/26/2018
ms.topic: get-started-article
ms.prod: microsoft-identity-manager
ms.assetid: 297df3b3-192e-4ed9-82ed-c95eb5297c84
ms.reviewer: mwahl
ms.suite: ems
ms.openlocfilehash: 141aabff13bf38c83f35efb2aad5de8c8d732eca
ms.sourcegitcommit: 869239972877b2905758aba4bb6b028dd09f9390
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/14/2018
ms.locfileid: "51635202"
---
# <a name="set-up-an-identity-management-server-sql-server-2016"></a>Настройка сервера управления удостоверениями: SQL Server 2016

> [!div class="step-by-step"]
> [« Windows Server 2016](prepare-server-ws2016.md)
> [SharePoint »](prepare-server-sharepoint.md)
> 
> [!NOTE]
> В этом пошаговом руководстве используются примеры имен и значений для компании Contoso. Замените их своими значениями. Пример.
> - Имя контроллера домена — **corpdc**
> - Имя домена — **contoso**.
> - Имя сервера службы MIM — **corpservice**
> - Имя сервера синхронизации MIM — **corpsync**
> - Имя SQL Server — **corpsql**
> - Пароль — <strong>Pass@word1</strong>

## <a name="install-sql-server-2016-standardenterprise-edition"></a>Установка **SQL Server 2016 (Выпуск Enterprise или Standard)**

1. Запустите **PowerShell** от имени администратора домена.

2. Перейдите в каталог, где находится программа установки SQL Server.

3. Введите следующие команды:

    ```
    .\setup.exe /Q /IACCEPTSQLSERVERLICENSETERMS /ACTION=install /FEATURES=SQL /INSTANCENAME=MSSQLSERVER /SQLSVCACCOUNT="contoso\SqlServer" /SQLSVCPASSWORD="Pass@word1"   /AGTSVCSTARTUPTYPE=Automatic /AGTSVCACCOUNT="NT AUTHORITY\Network Service" /SQLSYSADMINACCOUNTS="contoso\Administrator"

More info SQL deployment accounts and services can be found [here](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-windows-service-accounts-and-permissions?view=sql-server-2017)
> [!NOTE]
> SSMS is no longer included in SQL 2016. Download details can be found [here](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-2017)    ```
> 
> [!div class="step-by-step"]  
> [« Windows Server 2016](prepare-server-ws2016.md)
> [SharePoint »](prepare-server-sharepoint.md)
