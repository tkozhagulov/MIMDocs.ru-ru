---
title: "Шаг 3. Настройка SQL"
description: "В этой статье описан шаг 3 из серии статей, посвященных настройке диспетчера привилегированных удостоверений с помощью скриптов, а также приведены действия по настройке SQL Server."
keywords: 
author: barclayn
ms.author: barclayn
manager: MBaldwin
ms.date: 01/10/2017
ms.topic: article
ms.service: microsoft-identity-manager
ms.technology: active-directory-domain-services
ms.assetid: 4b524ae7-6610-40a0-8127-de5a08988a8a
ms.reviewer: 
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: f08b0197341351bd5f33552f26b96132b1356239
ms.openlocfilehash: 93ae9f198d73d21ae966fe3c3b22e47435bd5608
ms.lasthandoff: 01/10/2017


---
# <a name="step-3-configuring-sql"></a>Шаг 3. Настройка SQL

>[!div class="step-by-step"]
[« Шаг 2](sp1-step2-configuring-corp-domain.md)
[Шаг 4 »](sp1-step4-configuring-sharepoint.md)

Перед выполнением описанных ниже процедур убедитесь, что вы используете SQL Server 2012 как минимум с пакетом обновления 1 (SP1) или SQL Server 2014. Если сервер присоединен к домену, войдите в систему с учетной записью MIMAdmin. В противном случае войдите с учетной записью локального администратора.
1. Запустите PowerShell от имени администратора.
2. cd $env:SYSTEMDRIVE\PAM.
3. .\PAMDeployment.ps1.
4. Выберите пункт меню 3 (Настройка SQL Server).

  Если сервер не присоединен к домену PRIV, появится запрос на ввод учетных данных, чтобы присоединить сервер к домену.
  После присоединения к домену компьютер будет перезагружен. После успешной перезагрузки войдите на сервер с учетной записью MIMAdmin.

1. Запустите PowerShell от имени администратора.
2. cd $env:SYSTEMDRIVE\PAM.
3. .\PAMDeployment.ps1.
4. Выберите пункт меню 3 (Настройка SQL Server).

При появлении запроса введите пароль для учетной записи службы MIMAdmin, после чего установка продолжится. После завершения перейдите к шагу 4.

>[!div class="step-by-step"]
[« Шаг 2](sp1-step2-configuring-corp-domain.md)
[Шаг 4 »](sp1-step4-configuring-sharepoint.md)

