---
title: Шаг 5. Установка и настройка PAM
description: В этой статье описывается шаг 5 настройки диспетчера привилегированных удостоверений с помощью скриптов и рассматриваются действия по развертыванию на сервере PAM.
keywords: ''
author: barclayn
ms.author: barclayn
manager: MBaldwin
ms.date: 08/18/2017
ms.topic: article
ms.prod: microsoft-identity-manager
ms.technology: active-directory-domain-services
ms.assetid: 4b524ae7-6610-40a0-8127-de5a08988a8a
ms.reviewer: ''
ms.suite: ems
ms.openlocfilehash: e3e0d45f01f651400842b52e275ca4b6939f78c4
ms.sourcegitcommit: ace4d997c599215e46566386a1a3d335e991d821
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/15/2018
ms.locfileid: "49333842"
---
# <a name="step-5-installingconfiguring-pam"></a>Шаг 5. Установка и настройка PAM

> [!div class="step-by-step"]
> [« Шаг 4](sp1-step4-configuring-sharepoint.md)
> [Шаг 6 »](sp1-step6-setup-pam-trust.md)

Если сервер PAMServer присоединен к домену, войдите в систему с учетной записью MIMAdmin. В противном случае войдите с учетной записью локального администратора.
1. Запустите PowerShell от имени администратора.
2. cd $env:SYSTEMDRIVE\PAM.
3. .\PAMDeploymnet.ps1.
4. Выберите пункт меню 5 (Настройка PAM в MIM).

>[!NOTE]
>Если компьютер не присоединен к домену PRIV, появится запрос на ввод учетных данных. После присоединения к домену компьютер будет перезагружен.

После перезагрузки PAMServer войдите в систему с учетной записью MIMAdmin.

1. Запустите PowerShell от имени администратора.
2. cd $env:SYSTEMDRIVE\PAM.
3. .\PAMDeployment.ps1.
4. Выберите пункт меню 5 (Настройка PAM в MIM).

   При появлении запроса введите пароли для таких учетных записей: службы мониторинга MIM, компонента MIM, агента управления MIM, службы MIM, администратора MIM, SharePoint.
   После завершения установки компьютер будет перезагружен.

> [!div class="step-by-step"]
> [« Шаг 4](sp1-step4-configuring-sharepoint.md)
> [Шаг 6 »](sp1-step6-setup-pam-trust.md)
