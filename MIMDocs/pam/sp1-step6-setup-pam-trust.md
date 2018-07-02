---
title: Шаг 6. Настройка доверия PAM
description: Шаг 6 настройки PAM с помощью скриптов. В этом разделе рассматривается настройка необходимых отношений доверия между доменами CORP и PRIV.
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
ms.openlocfilehash: 5e3bed084b655535b0ac7b8b4252cdf541f6121f
ms.sourcegitcommit: 35f2989dc007336422c58a6a94e304fa84d1bcb6
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/20/2018
ms.locfileid: "36288781"
---
# <a name="step-6-set-up-the-pam-trust"></a>Шаг 6. Настройка доверия PAM

> [!div class="step-by-step"]
> [« Шаг 5](sp1-step5-configuring-pam.md)
> [Шаг 7 »](sp1-step7-setup-sidhistory-sidfiltering.md)

**Описанные действия можно не выполнять в среде, в которой есть только домен PRIV.** Войдите на сервер PAMServer с учетной записью MIMAdmin.

1. Войдите на сервер PAMServer с учетной записью MIMAdmin.
2. Запустите PowerShell от имени администратора.
3. cd $env:SYSTEMDRIVE\PAM.
4. .\PAMDeployment.ps1.
5. Выберите пункт меню 6 (Настройка доверия PAM).

   При появлении запроса введите учетные данные администратора CORP. После ввода учетных данных будет установлено отношение доверия. На этом настройка будет завершена.

> [!div class="step-by-step"]
> [« Шаг 5](sp1-step5-configuring-pam.md)
> [Шаг 7 »](sp1-step7-setup-sidhistory-sidfiltering.md)
