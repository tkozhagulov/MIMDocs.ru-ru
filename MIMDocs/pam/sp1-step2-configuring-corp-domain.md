---
title: Шаг 2. Настройка домена CORP
description: В этой статье описывается второй этап настройки домена CORP, предусматривающий запуск скрипта после копирования файла sids.txt в контроллер домена CORP.
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
ms.openlocfilehash: 775abc1546bc9eb93842b69edf64ac032518d66c
ms.sourcegitcommit: 35f2989dc007336422c58a6a94e304fa84d1bcb6
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/20/2018
ms.locfileid: "36289784"
---
# <a name="step-2-configuring-the-corp-domain"></a>Шаг 2. Настройка домена CORP

> [!div class="step-by-step"]
> [« Шаг 1](sp1-step1-configuring-priv-domain.md)
> [Шаг 3 »](sp1-step3-installing-configuring-sql.md)

Когда файл SIDs.txt скопирован в контроллер домена CORP (**не требуется для развертываний, в которых используется только домен PRIV**), сделайте следующее:

1. Войдите в контроллер домена CORP от имени администратора.
2. Запустите PowerShell от имени администратора.
3. cd $env:SYSTEMDRIVE\PAM.
4. .\PAMDeployment.ps1.
5. Выберите в меню второй пункт (Конфигурация леса CORP).

> [!div class="step-by-step"]
> [Шаг 1](sp1-step1-configuring-priv-domain.md)
> [Шаг 3](sp1-step3-installing-configuring-sql.md)
