---
title: "Шаг 8. Проверка развертывания PAM"
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
ms.openlocfilehash: 743ba586374ccc04e9ddafff759a00574e13f6ac


---

# Шаг 8. Проверка развертывания PAM

Пакет развертывания поставляется со сценариями проверки, способными выполнять сценарий PAM для подтверждения того, что развертывание PAM работает, как ожидалось.
Чтобы использовать проверку развертывания, измените раздел PAMDeploymentConfig.xml с названием <PamValidation/>.

>[!Note] Для проверки требуется присоединенный к домену CORP домен клиентского компьютера с установленными клиентскими компонентами PAM. Сценарии по установке клиента представлены в Приложении.

Имя клиентского компьютера следует обновить в теге <PAMValidationClient/> файла PAMDeploymentConfig.xml. Остальные данные на узле <PAMValidation/> подлежат изменению только в том случае, если у них возникает конфликт с существующими пользователями или группами, поскольку данная проверка попытается создать их.
Чтобы выполнить проверку, сделайте следующее.

Шаг 1.

1. Войдите в домен CORPDC от имени администратора домена CORP.
2. Запустите PowerShell от имени администратора.
3. cd $env:SYSTEMDRIVE\PAM.
4. Import-module.\PAMValidation.psm1
5. Create-PAMValidationonCORPDCConfig

В результате этого будут созданы группы и пользователи, необходимые для проверки

Шаг 2.

1. Войдите на сервер PAM как MIMAdmin.
2. Запустите PowerShell от имени администратора.
3. cd $env:SYSTEMDRIVE\PAM.
4. import-module.\PAMValidation.psm1
5. move-PAMVAlidationUsersToPAM

На этом этапе пользователи и группы перемещаются в среду PAM.

Шаг 3

1. Войдите на клиент CORP с правами локального администратора.
2. Запустите PowerShell от имени администратора.
3. cd $env:SYSTEMDRIVE\PAM.
4. import-module.\PAMValidation.psm1
5. Enable-PAMUsersCORPClientRemote


На этом этапе вам будет предложено указать учетные данные CORPAdmin. Затем необходимые пользователи будут добавлены в группы "Пользователи удаленного рабочего стола" и "Пользователи удаленного управления".
На клиенте CORP используйте следующую команду, чтобы открыть PowerShell от имени пользователя PRIV, в отношении которого выполняется проверка. </br></br>
**Runas /u:<PRIV domain>\PRIV.pamRequestor powershell.exe**  </br></br>
В окне PowerShell введите следующее:

1. cd $env:SYSTEMDRIVE\PAM.
2. import-module.\PAMValidation.psm1
3. test-PAMValidationScenarioNoApprovalRequest


  Отобразится состояние запроса.
  Изначально у пользователя не будет доступа к ресурсу. После своевременного добавления пользователя к роли ему предоставляется доступ. По истечении срока действия запроса у пользователя снова не будет доступа.
  В сценарии используется срок действия запроса по умолчанию (11 минут).



<!--HONumber=Sep16_HO4-->


