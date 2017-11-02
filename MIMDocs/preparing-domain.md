---
title: "Настройка домена для Microsoft Identity Manager 2016 | Документация Майкрософт"
description: "Создание контроллера домена Active Directory перед установкой MIM 2016"
keywords: 
author: billmath
ms.author: barclayn
manager: mbaldwin
ms.date: 10/26/2017
ms.topic: get-started-article
ms.service: microsoft-identity-manager
ms.technology: security
ms.assetid: 50345fda-56d7-4b6e-a861-f49ff90a8376
ms.reviewer: mwahl
ms.suite: ems
ms.openlocfilehash: 816e816111b27d1cc7dd4f7da2c5a810e7aa22fd
ms.sourcegitcommit: 9e854a39128a5f81cdbb1379e1fa95ef3a88cdd2
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/26/2017
---
# <a name="set-up-a-domain"></a>Настройка домена

>[!div class="step-by-step"]
[Windows Server 2012 R2 "](prepare-server-ws2012r2.md)

Microsoft Identity Manger (MIM) работает с доменом Active Directory (AD). Служба AD должна быть уже установлена. Кроме того, в вашей среде должен быть контроллер для домена, которым вы можете управлять.

В этой статье рассматриваются действия по подготовке домена для работы с MIM.

## <a name="create-user-accounts-and-groups"></a>Создание учетных записей пользователей и групп

Всем компонентам развертывания MIM требуются собственные удостоверения в домене. Сюда входят такие компоненты MIM, как служба и модуль синхронизации, а также SharePoint и SQL.

> [!NOTE]
> В этом пошаговом руководстве используются примеры имен и значений для компании Contoso. Замените их своими значениями. Пример.
> - Имя контроллера домена — **mimservername**.
> - Имя домена — **contoso**.
> - Пароль — **Pass@word1**

1. Войдите в контроллер домена в качестве администратора (*например Contoso\Administrator*).

2. Создайте следующие учетные записи пользователей для служб MIM: Запустите PowerShell и введите следующий скрипт PowerShell, чтобы обновить домен.

    ```PowerShell
    import-module activedirectory
    $sp = ConvertTo-SecureString "Pass@word1" –asplaintext –force
    New-ADUser –SamAccountName MIMMA –name MIMMA
    Set-ADAccountPassword –identity MIMMA –NewPassword $sp
    Set-ADUser –identity MIMMA –Enabled 1 –PasswordNeverExpires 1
    New-ADUser –SamAccountName MIMSync –name MIMSync
    Set-ADAccountPassword –identity MIMSync –NewPassword $sp
    Set-ADUser –identity MIMSync –Enabled 1 –PasswordNeverExpires 1
    New-ADUser –SamAccountName MIMService –name MIMService
    Set-ADAccountPassword –identity MIMService –NewPassword $sp
    Set-ADUser –identity MIMService –Enabled 1 –PasswordNeverExpires 1
    New-ADUser –SamAccountName MIMSSPR –name MIMSSPR
    Set-ADAccountPassword –identity MIMSSPR –NewPassword $sp
    Set-ADUser –identity MIMSSPR –Enabled 1 –PasswordNeverExpires 1
    New-ADUser –SamAccountName SharePoint –name SharePoint
    Set-ADAccountPassword –identity SharePoint –NewPassword $sp
    Set-ADUser –identity SharePoint –Enabled 1 –PasswordNeverExpires 1
    New-ADUser –SamAccountName SqlServer –name SqlServer
    Set-ADAccountPassword –identity SqlServer –NewPassword $sp
    Set-ADUser –identity SqlServer –Enabled 1 –PasswordNeverExpires 1
    New-ADUser –SamAccountName BackupAdmin –name BackupAdmin
    Set-ADAccountPassword –identity BackupAdmin –NewPassword $sp
    Set-ADUser –identity BackupAdmin –Enabled 1 -PasswordNeverExpires 1
    ```

3.  Создайте группы безопасности во всех группах.

    ```PowerShell
    New-ADGroup –name MIMSyncAdmins –GroupCategory Security –GroupScope Global –SamAccountName MIMSyncAdmins
    New-ADGroup –name MIMSyncOperators –GroupCategory Security –GroupScope Global –SamAccountName MIMSyncOperators
    New-ADGroup –name MIMSyncJoiners –GroupCategory Security –GroupScope Global –SamAccountName MIMSyncJoiners
    New-ADGroup –name MIMSyncBrowse –GroupCategory Security –GroupScope Global –SamAccountName MIMSyncBrowse
    New-ADGroup –name MIMSyncPasswordReset –GroupCategory Security –GroupScope Global –SamAccountName MIMSyncPasswordReset
    Add-ADGroupMember -identity MIMSyncAdmins -Members Administrator
    Add-ADGroupmember -identity MIMSyncAdmins -Members MIMService
    ```

4.  Добавление имен субъектов-служб для включения проверки подлинности Kerberos для учетных записей служб

    ```CMD
    setspn -S http/mimservername.contoso.local Contoso\SharePoint
    setspn -S http/mimservername Contoso\SharePoint
    setspn -S FIMService/mimservername.contoso.local Contoso\MIMService    
    ```

>[!div class="step-by-step"]
[Windows Server 2012 R2 "](prepare-server-ws2012r2.md)
