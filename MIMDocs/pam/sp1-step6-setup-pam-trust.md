---
title: "Шаг 6. Настройка доверия PAM"
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
ms.openlocfilehash: 5bcf4f4ef201236746ec1bf75c1c8900841a6c79


---

# <a name="step-6-set-up-the-pam-trust"></a>Шаг 6. Настройка доверия PAM

>[!div class="step-by-step"]
[« Шаг 5](sp1-step5-configuring-pam.md)
[Шаг 7 »](sp1-step7-setup-sidhistory-sidfiltering.md)

**Описанные действия можно не выполнять в среде, в которой есть только домен PRIV.** Войдите на сервер PAMServer с учетной записью MIMAdmin.

1. Войдите на сервер PAMServer с учетной записью MIMAdmin.
2. Запустите PowerShell от имени администратора.
3. cd $env:SYSTEMDRIVE\PAM.
4. .\PAMDeployment.ps1.
5. Выберите пункт меню 6 (Настройка доверия PAM).

  При появлении запроса введите учетные данные администратора CORP. После ввода учетных данных будет установлено отношение доверия. На этом настройка будет завершена.

>[!div class="step-by-step"]
[« Шаг 5](sp1-step5-configuring-pam.md)
[Шаг 7 »](sp1-step7-setup-sidhistory-sidfiltering.md)



<!--HONumber=Nov16_HO2-->


