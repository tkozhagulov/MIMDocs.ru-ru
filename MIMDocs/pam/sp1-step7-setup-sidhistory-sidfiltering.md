---
title: "Шаг 7. Настройка ведения журнала и фильтрации идентификаторов безопасности"
description: "Подготовка домена CORP с существующими или новыми удостоверениями, которыми будет управлять диспетчер привилегированных удостоверений, с использованием скриптов"
keywords: 
author: barclayn
manager: MBaldwin
ms.date: 09/27/2016
ms.topic: article
ms.prod: microsoft-identity-manager
ms.service: microsoft-identity-manager
ms.technology: active-directory-domain-services
ms.assetid: 4b524ae7-6610-40a0-8127-de5a08988a8a
ms.reviewer: 
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: bc56b57a06592527bab13aad879ca13466e968b3
ms.openlocfilehash: 4ad5d755de100ad598c6cebd209296edd361e8c5


---

# Шаг 7. Настройка ведения журнала и фильтрации идентификаторов безопасности

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



<!--HONumber=Oct16_HO1-->


