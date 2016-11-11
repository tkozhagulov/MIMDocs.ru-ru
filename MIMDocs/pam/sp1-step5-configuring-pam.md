---
title: "Шаг 5. Установка и настройка PAM"
description: "Подготовка домена CORP с существующими или новыми удостоверениями, которыми будет управлять диспетчер привилегированных удостоверений, с использованием скриптов"
keywords: 
author: barclayn
ms.author: barclayn
manager: MBaldwin
ms.date: 10/25/2016
ms.topic: article
ms.service: microsoft-identity-manager
ms.technology: active-directory-domain-services
ms.assetid: 4b524ae7-6610-40a0-8127-de5a08988a8a
ms.reviewer: 
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 365989693f844f117f76ee2b69db85df82f06f35
ms.openlocfilehash: c641865548f753a609ccee8dbf12c329bb6a1c9f


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



<!--HONumber=Nov16_HO2-->


