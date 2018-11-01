---
title: Шаг 7. Настройка ведения журнала и фильтрации идентификаторов безопасности
description: В этой статье описывается шаг 7 настройки диспетчера привилегированных удостоверений с помощью скриптов. Этот шаг включает настройку журнала и фильтрации идентификаторов безопасности.
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
ms.openlocfilehash: f85dd4eff32d5207948ec332bf2e9850b14a86fe
ms.sourcegitcommit: 44a2293ff17c50381a59053303311d7db8b25249
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/31/2018
ms.locfileid: "50379334"
---
# <a name="step-7-set-up-sid-historysid-filtering"></a>Шаг 7. Настройка ведения журнала и фильтрации идентификаторов безопасности

> [!div class="step-by-step"]
> [« Шаг 6](sp1-step6-setup-pam-trust.md)
> [Шаг 8 »](sp1-step8-pam-deployment-verification.md)

**Описанные действия можно не выполнять в среде, в которой есть только домен PRIV.** Войдите на сервер PAMServer с учетной записью MIMAdmin.

1. Войдите в контроллер домена CORP от имени администратора.
2. Запустите PowerShell от имени администратора.
3. cd $env:SYSTEMDRIVE\PAM.
4. .\PAMDeployment.ps1.
5. Выберите пункт меню 8 (Настройка ведения журнала и фильтрации идентификаторов безопасности).

Если все прошло успешно, появится следующее сообщение.<br/></br>
Для фильтрации идентификаторов безопасности: <br/></br>
"Настройка доверия для невыполнения фильтрации SID" или "Фильтрация SID не включена для этого доверия". </br></br>
Для ведения журнала идентификаторов безопасности: </br></br>
"Включение журнала идентификаторов безопасности для этого доверия" или "Журнал идентификаторов безопасности для этого доверия уже включен".

> [!div class="step-by-step"]
> [« Шаг 6](sp1-step6-setup-pam-trust.md)
> [Шаг 8 »](sp1-step8-pam-deployment-verification.md)
