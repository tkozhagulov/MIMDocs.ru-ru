---
title: Шаг 5. Установка и настройка PAM
description: В этой статье описывается шаг 5 настройки диспетчера привилегированных удостоверений с помощью скриптов и рассматриваются действия по развертыванию на сервере PAM.
keywords: ''
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 08/18/2017
ms.topic: article
ms.prod: microsoft-identity-manager
ms.assetid: 4b524ae7-6610-40a0-8127-de5a08988a8a
ms.reviewer: ''
ms.suite: ems
ms.openlocfilehash: 03c5b1cb52f16090e6b241d588bbded6be4c6687
ms.sourcegitcommit: 44a2293ff17c50381a59053303311d7db8b25249
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/31/2018
ms.locfileid: "50379368"
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
