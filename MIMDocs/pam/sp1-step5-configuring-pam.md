---
title: "Шаг 5. Установка и настройка PAM"
description: "В этой статье описывается шаг 5 настройки диспетчера привилегированных удостоверений с помощью скриптов и рассматриваются действия по развертыванию на сервере PAM."
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
ms.openlocfilehash: 862f62ab9bac87bcee31c35e249db34740e9fb14
ms.lasthandoff: 01/10/2017


---
# <a name="step-5-installingconfiguring-pam"></a>Шаг 5. Установка и настройка PAM

>[!div class="step-by-step"]
[« Шаг 4](sp1-step4-configuring-sharepoint.md)
[Шаг 6 »](sp1-step6-setup-pam-trust.md)

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

>[!div class="step-by-step"]
[« Шаг 4](sp1-step4-configuring-sharepoint.md)
[Шаг 6 »](sp1-step6-setup-pam-trust.md)

