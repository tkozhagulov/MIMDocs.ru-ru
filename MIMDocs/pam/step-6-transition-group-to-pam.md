---
title: "Развертывание PAM. Шаг 6 — перемещение группы | Документация Майкрософт"
description: "Перенесите группу в лес PRIV, чтобы применить к ней Privileged Access Management."
keywords: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 03/15/2017
ms.topic: article
ms.service: microsoft-identity-manager
ms.technology: active-directory-domain-services
ms.assetid: 7b689eff-3a10-4f51-97b2-cb1b4827b63c
ms.reviewer: mwahl
ms.suite: ems
ms.translationtype: Human Translation
ms.sourcegitcommit: bfc73723bdd3a49529522f78ac056939bb8025a3
ms.openlocfilehash: aeffca2c4e5467ec039c2077a88f36a652493e90
ms.contentlocale: ru-ru
ms.lasthandoff: 07/10/2017


---

<a id="step-6--transition-a-group-to-privileged-access-management" class="xliff"></a>
# Шаг 6. Перевод группы в управление привилегированных доступом (PAM)

>[!div class="step-by-step"]
[« Шаг 5 ](step-5-establish-trust-between-priv-corp-forests.md)
[Шаг 7 »](step-7-elevate-user-access.md)

Привилегированная учетная запись создается в лесу PRIV с помощью командлетов PowerShell. Они выполняют следующие действия.

- Создайте в лесу PRIV новую группу с таким же идентификатором безопасности (SID), как у группы в лесу CORP.  
- Создайте в базе данных службы MIM объект, соответствующей группе в лесу PRIV.  
- Для каждой учетной записи пользователя создаются два объекта в базе данных службы MIM, соответствующие данному пользователю в лесу CORP и новой учетной записи пользователя в лесу PRIV.  
- Создают объект роли PAM в базе данных службы MIM.  

Эти командлеты необходимо выполнить один раз для каждой группы и один раз для каждого члена группы. Командлеты миграции не меняют каких-либо пользователей или группы в лесу CORP, впоследствии администратор PAM должен будет сделать это вручную.

1. Войдите в PAMSRV напрямую или с рабочей станции PRIV как *PRIV\MIMAdmin*.

2.  Запустите PowerShell и введите следующие команды:

    ```
    Import-Module MIMPAM
    Import-Module ActiveDirectory
    ```

3.  В PRIV создайте соответствующую учетную запись для пользователя в существующем лесу в целях демонстрации.

    В PowerShell введите следующие команды:  Если вы не использовали имя *Jen* для создания пользователя в contoso.local ранее, измените параметры команды соответствующим образом. Пароль 'Pass@word1' указан для примера. Его необходимо заменить уникальным значением.

    ```
    $sj = New-PAMUser –SourceDomain CONTOSO.local –SourceAccountName Jen
    $jp = ConvertTo-SecureString "Pass@word1" –asplaintext –force
    Set-ADAccountPassword –identity priv.Jen –NewPassword $jp
    Set-ADUser –identity priv.Jen –Enabled 1
    ```

4. Для целей демонстрации скопируйте группу и ее члена Jen из CONTOSO в домен PRIV.

    Выполните следующие команды, указав пароль администратора домена CORP (CONTOSO\Administrator) при появлении запроса:

        ```
        $ca = get-credential –UserName CONTOSO\Administrator –Message "CORP forest domain admin credentials"
        $pg = New-PAMGroup –SourceGroupName "CorpAdmins" –SourceDomain CONTOSO.local                 –SourceDC CORPDC.contoso.local –Credentials $ca
        $pr = New-PAMRole –DisplayName "CorpAdmins" –Privileges $pg –Candidates $sj
        ```

    Команду **New-PAMGroup** можно использовать со следующими параметрами:

        -   The CORP forest domain name in NetBIOS form  
        -   The name of the group to copy from that domain  
        -   The CORP forest Domain Controller NetBIOS name  
        -   The credentials of an domain admin user in the CORP forest  

5.  На компьютере CORPDC удалите учетную запись Jen из группы **CONTOSO CorpAdmins**, если она все еще присутствует (по желанию).  Она нужна только для демонстрации, чтобы показать, как сопоставить разрешения с учетными записями, созданными в лесу PRIV.

    1.  Войдите на компьютер CORPDC как *CONTOSO\Administrator*.

    2.  Запустите PowerShell, выполните следующую команду и подтвердите изменение.

        ```
        Remove-ADGroupMember -identity "CorpAdmins" -Members "Jen"
        ```


Если вы хотите проверить действительность прав доступа между лесами для административной учетной записи пользователя, перейдите к следующему шагу.

>[!div class="step-by-step"]
[« Шаг 5 ](step-5-establish-trust-between-priv-corp-forests.md)
[Шаг 7 »](step-7-elevate-user-access.md)

