---
title: "Развертывание PAM. Шаг 7 — пользовательский доступ | Microsoft Identity Manager"
description: "На завершающем этапе предоставьте временный доступ привилегированному пользователю, чтобы продемонстрировать успешное развертывание Privileged Access Management."
keywords: 
author: kgremban
manager: femila
ms.date: 07/15/2016
ms.topic: article
ms.prod: microsoft-identity-manager
ms.service: microsoft-identity-manager
ms.technology: active-directory-domain-services
ms.assetid: 5325fce2-ae35-45b0-9c1a-ad8b592fcd07
ms.reviewer: mwahl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 9b5b7460e6307ab38b1b9356a638eb0200fd97d1
ms.openlocfilehash: 009091a65dba31de2066e45930e438442fcd89a0


---

# Шаг 7. Повышение прав доступа пользователя

>[!div class="step-by-step"]
[« Шаг 6 ](step-6-transition-group-to-pam.md)


На этом шаге показано, как пользователь может запросить доступ к роли с помощью MIM.

## Проверка того, что Jen не может получить доступ к привилегированному ресурсу
Без повышенных прав Jen не может получить доступ к привилегированному ресурсу в лесу CORP.

1. Выйдите из CORPWKSTN, чтобы удалить все открытые кэшированные подключения.
2. Войдите на компьютер CORPWKSTN как *CONTOSO\Jen* и переключитесь на **представление рабочего стола**.
3. Откройте командную строку DOS.
4. Введите команду `dir \\corpwkstn\corpfs`. Должно появиться сообщение об ошибке **Доступ запрещен**.
5. Не закрывайте окно командной строки.

## Запросите привилегированный доступ в MIM.
1. На компьютере CORPWKSTN также под именем CONTOSO\Jen введите следующую команду.

    ```
    runas /user:Priv.Jen@priv.contoso.local powershell
    ```

2. При появлении запроса введите пароль для учетной записи PRIV.Jen. Появится новое окно командной строки.
3. Когда откроется окно Windows PowerShell, введите следующие команды:

    > [!NOTE]
    > После выполнения этих команд все перечисленные ниже действия имеют ограничения по времени.

    ```
    Import-module MIMPAM
    $r = Get-PAMRoleForRequest | ? { $_.DisplayName –eq "CorpAdmins" }
    New-PAMRequest –role $r
    klist purge
    ```

4. Затем закройте окно PowerShell.
5. В окне командной строки DOS введите следующую команду:

    ```
    runas /user:Priv.Jen@priv.contoso.local powershell
    ```

6. Введите пароль для учетной записи PRIV.Jen. Появится новое окно командной строки.

## Проверьте повышенные права доступа.
В новом окне введите следующие команды.

```
whoami /groups
dir \\corpwkstn\corpfs
```

Если команда dir вызывает ошибку **Доступ запрещен**, проверьте отношения доверия.

## Активация привилегированной роли
Выполните активацию, запросив привилегированный доступ на примере портала PAM.

1. На компьютере CORPWKSTN выполните вход под именем CORP\Jen.
2. В окне командной строки DOS введите следующую команду:

    ```
    runas /user:Priv.Jen@priv.contoso.local "c:\program files\Internet Explorer\iexplore.exe"
    ```

3. При появлении запроса введите пароль для учетной записи PRIV.Jen. Появится новое окно браузера.
4. Перейдите по адресу http://pamsrv.priv.contoso.local:8090 и убедитесь, что отображается веб-страница примера портала.
5. В Internet Explorer выберите **Сервис** > **Свойства браузера** и перейдите на вкладку **Безопасность**.
6. Выберите пункт **Зона местной интрасети** > **Сайты** > **Дополнительно** и добавьте веб-сайт в эту зону.
7. Закройте диалоговое окно **Свойства браузера** .
8. На левой вкладке нажмите кнопку **Активировать**. Выберите **Роль PAM** и нажмите кнопку **Активировать**.

> [!Note]
> В этой среде также можно попробовать разрабатывать приложения, которые используют API REST PAM, описанный в [Справочнике по API REST системы управления привилегированным доступом (PAM)](/microsoft-identity-manager/reference/privileged-access-management-rest-api-reference).

## Сводка
Выполнив действия, описанные в этом руководстве, вы сможете воспроизвести сценарий управления привилегированным доступом, в котором права пользователя повышаются на ограниченное время, что позволяет пользователю получить доступ к защищенным ресурсам под отдельной привилегированной учетной записью. Сразу после окончания сеанса повышение прав привилегированная учетная запись теряет доступ к защищенному ресурсу. Решение о том, какие группы безопасности представляют привилегированные роли, принимает администратор PAM. После переноса прав доступа в систему управления привилегированным доступом ранее возможный доступ с исходной учетной записью пользователя предоставляется только при входе с помощью специальной привилегированной учетной записи и только по запросу. В результате членства в группах для привилегированных групп действуют ограниченное время.

>[!div class="step-by-step"]
[« Шаг 6 ](step-6-transition-group-to-pam.md)



<!--HONumber=Jul16_HO4-->

