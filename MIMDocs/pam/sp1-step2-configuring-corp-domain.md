---
title: "Шаг 2. Настройка домена CORP"
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
ms.openlocfilehash: b7acc475c505b29559c510fd3fa350fed1c3157b


---

# <a name="step-2-configuring-the-corp-domain"></a>Шаг 2. Настройка домена CORP

>[!div class="step-by-step"]
[Шаг 1](sp1-step1-configuring-priv-domain.md)
[Шаг 3](sp1-step3-installing-configuring-sql.md)

Когда файл SIDs.txt скопирован в контроллер домена CORP (**не требуется для развертываний, в которых используется только домен PRIV**), сделайте следующее:

1. Войдите в контроллер домена CORP от имени администратора.
2. Запустите PowerShell от имени администратора.
3. cd $env:SYSTEMDRIVE\PAM.
4. .\PAMDeployment.ps1.
5. Выберите в меню второй пункт (Конфигурация леса CORP).

>[!div class="step-by-step"]
[Шаг 1](sp1-step1-configuring-priv-domain.md)
[Шаг 3](sp1-step3-installing-configuring-sql.md)



<!--HONumber=Nov16_HO2-->


