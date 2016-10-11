---
title: "Шаг 6. Настройка доверия PAM"
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
ms.sourcegitcommit: 689c2ef0e4e4a681a398ba7e94fb3def525937ea
ms.openlocfilehash: 46afda513e849e457f5f3644a46f244161467e50


---

# Настройка доверия PAM

**Описанные действия можно не выполнять в среде, в которой есть только домен PRIV.** Войдите на сервер PAMServer с учетной записью MIMAdmin.

1. Войдите на сервер PAMServer с учетной записью MIMAdmin.
2. Запустите PowerShell от имени администратора.
3. cd $env:SYSTEMDRIVE\PAM.
4. .\PAMDeployment.ps1.
5. Выберите пункт меню 6 (Настройка доверия PAM).

  При появлении запроса введите учетные данные администратора CORP. После ввода учетных данных будет установлено отношение доверия. На этом настройка будет завершена.



<!--HONumber=Sep16_HO4-->


