---
title: Шаг 3. Настройка SQL
description: В этой статье описан шаг 3 из серии статей, посвященных настройке диспетчера привилегированных удостоверений с помощью скриптов, а также приведены действия по настройке SQL Server.
keywords: ''
author: barclayn
ms.author: barclayn
manager: MBaldwin
ms.date: 08/18/2017
ms.topic: article
ms.service: microsoft-identity-manager
ms.technology: active-directory-domain-services
ms.assetid: 4b524ae7-6610-40a0-8127-de5a08988a8a
ms.reviewer: ''
ms.suite: ems
ms.openlocfilehash: 1196d16e03eed13056877584626e3ea7ab4739d6
ms.sourcegitcommit: 35f2989dc007336422c58a6a94e304fa84d1bcb6
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/20/2018
ms.locfileid: "36289253"
---
# <a name="step-3-configuring-sql"></a>Шаг 3. Настройка SQL

> [!div class="step-by-step"]
> [« Шаг 2](sp1-step2-configuring-corp-domain.md)
> [Шаг 4 »](sp1-step4-configuring-sharepoint.md)

Перед выполнением описанных ниже процедур убедитесь, что вы используете SQL Server 2012 как минимум с пакетом обновления 1 (SP1) или SQL Server 2014. Если сервер присоединен к домену, войдите в систему с учетной записью MIMAdmin. В противном случае войдите с учетной записью локального администратора.
1. Запустите PowerShell от имени администратора.
2. cd $env:SYSTEMDRIVE\PAM.
3. .\PAMDeployment.ps1.
4. Выберите пункт меню 3 (Настройка SQL Server).

   Если сервер не присоединен к домену PRIV, появится запрос на ввод учетных данных, чтобы присоединить сервер к домену.
   После присоединения к домену компьютер будет перезагружен. После успешной перезагрузки войдите на сервер с учетной записью MIMAdmin.

5. Запустите PowerShell от имени администратора.
6. cd $env:SYSTEMDRIVE\PAM.
7. .\PAMDeployment.ps1.
8. Выберите пункт меню 3 (Настройка SQL Server).

При появлении запроса введите пароль для учетной записи службы MIMAdmin, после чего установка продолжится. После завершения перейдите к шагу 4.

> [!div class="step-by-step"]
> [« Шаг 2](sp1-step2-configuring-corp-domain.md)
> [Шаг 4 »](sp1-step4-configuring-sharepoint.md)
