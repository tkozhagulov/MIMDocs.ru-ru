---
title: "Шаг 3. Настройка SQL"
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
ms.openlocfilehash: a7d456b1c2baf31ef2d7ca801a567cf42eaef52e


---
# Шаг 3. Настройка SQL

Перед выполнением описанных ниже процедур убедитесь, что вы используете SQL Server 2012 как минимум с пакетом обновления 1 (SP1) или SQL Server 2014. Если сервер присоединен к домену, войдите в систему с учетной записью MIMAdmin. В противном случае войдите с учетной записью локального администратора.
1. Запустите PowerShell от имени администратора.
2. cd $env:SYSTEMDRIVE\PAM.
3. .\PAMDeployment.ps1.
4. Выберите пункт меню 3 (Настройка SQL Server).

  Если сервер не присоединен к домену PRIV, появится запрос на ввод учетных данных, чтобы присоединить сервер к домену.
  После присоединения к домену компьютер будет перезагружен. После успешной перезагрузки войдите на сервер с учетной записью MIMAdmin.

1. Запустите PowerShell от имени администратора.
2. cd $env:SYSTEMDRIVE\PAM.
3. .\PAMDeployment.ps1.
4. Выберите пункт меню 3 (Настройка SQL Server).

При появлении запроса введите пароль для учетной записи службы MIMAdmin, после чего установка продолжится. После завершения перейдите к шагу 4.



<!--HONumber=Sep16_HO4-->


