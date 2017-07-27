---
title: "Шаг 7. Настройка ведения журнала и фильтрации идентификаторов безопасности"
description: "В этой статье описывается шаг 7 настройки диспетчера привилегированных удостоверений с помощью скриптов. Этот шаг включает настройку журнала и фильтрации идентификаторов безопасности."
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
ms.openlocfilehash: e608593f40759e3bc995daa56c4575510a71e987
ms.sourcegitcommit: 02fb1274ae0dc11288f8bd9cd4799af144b8feae
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/13/2017
---
# <a name="step-7-set-up-sid-historysid-filtering"></a>Шаг 7. Настройка ведения журнала и фильтрации идентификаторов безопасности

>[!div class="step-by-step"]
[« Шаг 6](sp1-step6-setup-pam-trust.md)
[Шаг 8 »](sp1-step8-pam-deployment-verification.md)

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

>[!div class="step-by-step"]
[« Шаг 6](sp1-step6-setup-pam-trust.md)
[Шаг 8 »](sp1-step8-pam-deployment-verification.md)
