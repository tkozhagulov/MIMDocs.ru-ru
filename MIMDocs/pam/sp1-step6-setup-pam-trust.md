---
title: Шаг 6. Настройка доверия PAM
description: Шаг 6 настройки PAM с помощью скриптов. В этом разделе рассматривается настройка необходимых отношений доверия между доменами CORP и PRIV.
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
ms.openlocfilehash: ad1482718693c9ae7004a71334013de68f7c20da
ms.sourcegitcommit: 44a2293ff17c50381a59053303311d7db8b25249
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/31/2018
ms.locfileid: "50379385"
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
