---
title: "Шаг 1. Настройка домена PRIV"
description: "Подготовка домена CORP с существующими или новыми удостоверениями, которыми будет управлять диспетчер привилегированных удостоверений, с использованием скриптов"
keywords: 
author: barclayn
ms.author: barclayn
manager: MBaldwin
ms.date: 08/18/2017
ms.topic: article
ms.service: microsoft-identity-manager
ms.technology: active-directory-domain-services
ms.assetid: 4b524ae7-6610-40a0-8127-de5a08988a8a
ms.reviewer: 
ms.suite: ems
ms.openlocfilehash: 40822bb7702cf3d7ac23ecd6e98ac392f2d3a480
ms.sourcegitcommit: 8edd380f54c3e9e83cfabe8adfa31587612e5773
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/19/2017
---
# <a name="step-1-configuring-the-priv-domain"></a>Шаг 1. Настройка домена PRIV

>[!div class="step-by-step"]
[Шаг 2 "](sp1-step2-configuring-corp-domain.md)

1. Войдите в систему PRIVDC от имени администратора.
  * Если в этой среде только PRIV, войдите в систему CORPDC.
2. Запустите PowerShell от имени администратора.
3. cd $env:SYSTEMDRIVE\PAM.
4. .\PAMDeployment.ps1.
5. Выберите параметр меню 1 (Конфигурация леса PRIV).


Учетные записи службы, необходимые для управления SQL, SharePoint и MIM, создаются автоматически, если в домене их еще нет. Вам будет предложено ввести пароли для создания этих учетных записей служб в процессе выполнения сценария.
Если домен PRIV работает под управлением Windows Server 2016 и настроен уровень функциональности Windows Server 2016 Technical Preview 5, сценарий предложит включить необязательную функцию Privileged Access Management службы Active Directory, которая обязательна для сервера PAM. Для подтверждения и продолжения нажмите "Да".
Если заданный уровень функциональности ниже Windows Server 2016, пропустите предупреждение о том, что дополнительная настройка не будет выполнена. После того как администратор повысит уровень функциональности до Windows Server 2016, нужно будет повторно запустить PAMDeployment.ps1 и конфигурацию леса PAM.

>[!NOTE]
>Следующие шаги не являются обязательными для конфигураций PRIVOnly.

Скопируйте файл SIDs.txt, созданный в $env: SYSTEMDRIVE\PAM, в аналогичную папку на CORPDC. Это требуется для CORPDC, чтобы настроить разрешения на чтение свойств пользователей CORP для пользователей PRIV.
После выполнения сценария вам будет предложено перезагрузить компьютер, чтобы изменения вступили в силу.

>[!div class="step-by-step"]
[Шаг 2 "](sp1-step2-configuring-corp-domain.md)
