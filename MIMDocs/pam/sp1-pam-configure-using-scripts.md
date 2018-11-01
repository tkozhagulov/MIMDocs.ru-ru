---
title: Настройка управления привилегированным доступом (PAM) с помощью сценариев
description: Эта статья входит в серию, посвященную настройке PAM с помощью скриптов. Здесь рассматриваются изменения XML-файла, который будет использоваться в скриптах развертывания PAM.
keywords: ''
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 07/20/2017
ms.topic: article
ms.prod: microsoft-identity-manager
ms.assetid: 4b524ae7-6610-40a0-8127-de5a08988a8a
ms.reviewer: ''
ms.suite: ems
ms.openlocfilehash: 28e8f5c28cd38ad820c6a1f12385dffbd0641ddd
ms.sourcegitcommit: 44a2293ff17c50381a59053303311d7db8b25249
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/31/2018
ms.locfileid: "50379539"
---
# <a name="configure-pam-using-scripts"></a>Настройка управления привилегированным доступом (PAM) с помощью сценариев

Если вы решили установить SQL и SharePoint на отдельных серверах, необходимо настроить их в соответствии с приведенными ниже инструкциями. Если компоненты SQL, SharePoint и PAM устанавливаются на одном компьютере, указанные ниже действия необходимо выполнить с этого компьютера.

Предполагается, что домен PRIV уже установлен и вы можете приступать непосредственно к выполнению описанных действий. Инструкции по настройке домена PRIV содержатся в приложении в конце этого документа.

Пошаговая инструкция

1. Загрузить [Сценарии развертывания PAM](https://www.microsoft.com/download/details.aspx?id=53941)
2. Распакуйте сжатый файл PAMDeploymentScripts.zip в папку %SYSTEMDRIVE%\PAM на всех компьютерах.
3. На одном из компьютеров откройте файл **PAMDeploymentConfig.xml** и обновите сведения с помощью приведенной ниже таблицы или руководства, содержащегося в самом XML-файле. Если леса CORP и PRIV уже установлены, вам нужно только лишь обновить параметры **DNSName** и **NetbiosName.**
4. В разделе "Роли" обновите **учетную запись службы**, **сведения о компьютере** и **расположение двоичных файлов установки** для ролей SQL, SharePoint и MIM.
    1. Расположение двоичных файлов MIM должно указывать на каталог, содержащий папку "Service and Portal" (Служба и портал). Расположение двоичных файлов клиента должно указывать на каталог, содержащий файл с надстройками и расширениями "Add-ins and Extensions.msi".

5. Если используется среда PRIVOnly, для тега PRIVOnly должно быть установлено значение True.
    1. При использовании сред PRIVOnly необходимо обновить параметры **DNSName** и **NetbiosName** домена PRIV, чтобы они совпадали с аналогичными параметрами домена CORP. Проверьте правильность суффиксов всех компьютеров, на которых установлены компоненты SQL, SharePoint и MIM, так как файл шаблона по умолчанию предполагает использование конфигураций CORP и PRIV.
    2. Подробные сведения о средах PRIVOnly см. здесь.

6. Скопируйте тот же файл PAMDeploymentConfig.xml в папки %SYSTEMDRIVE%\PAM на всех компьютерах, контроллерах доменов CORP и PRIV, серверах PAM Server, SQL Server и SharePoint.


## <a name="deployment-worksheet"></a>Журнал развертывания

Прежде чем приступить к развертыванию, обновите файл PAMDeploymentConfig.xml и разместите его обновленную копию на всех компьютерах.

### <a name="setup"></a>Настройка

|Компьютер   | Запуск от имени   |Команды   |
|---|---|---|
|  Контроллер домена PRIV |Администратор домена PRIV   | .\PAMDeployment.ps1. Выберите в меню пункт 1 (Конфигурация леса PRIV)   |
|   |   |  При выполнении указанного выше действия создается файл SIDs.txt. Скопируйте этот файл в папку $envDrive:PAM на CORPDC, прежде чем перейти к следующему этапу. |
| Контроллер домена CORP  |Администратор домена CORP   | .\PAMDeployment.ps1. Выберите в меню пункт 2 (Конфигурация леса CORP)   |
| Сервер PAMServer (или SQL Server)   |Администратор домена CORP   |  .\PAMDeployment.ps1. Выберите в меню пункт 2 (Конфигурация леса CORP)  |
|  Сервер PAMServer |  Локальный администратор (после присоединения к домену — администратор MIM) |  .\PAMDeployment.ps1. Выберите в меню пункт 4 (Настройка SharePoint)  |
| Сервер PAMServer  | Локальный администратор (после присоединения к домену — администратор MIM)  | .\PAMDeployment.ps1. Выберите в меню пункт 5 (Настройка PAM в MIM)   |
|  Сервер PAMServer |Администратор MIM   | .\PAMDeployment.ps1. Выберите в меню пункт 6 (Настройка доверия в PAM) .\PAMDeployment.ps1. Выберите в меню пункт 6 (Настройка доверия в PAM) |

### <a name="validation"></a>Проверка

|  Компьютер | Запуск от имени   | Команды   |
|---|---|---|
| Клиент домена CORP  | Пользователь домена CORP (локальный администратор)  |   .\PAMDeployment.ps1. Выберите в меню пункт 7 (Настройка клиента PAM в MIM)  |
| Контроллер домена CORP  | Администратор домена CORP   | Import-module .\PAMValidation.psm1 ; Create-PAMValidationCORPDCConfig   |
| Сервер PAMServer   | Администратор MIM  | Import-module .\PAMValidation.psm1 ; Move-PAMValidationUsersToPAM  |
| Клиент домена CORP  | Пользователь домена CORP (локальный администратор)   |   Import-module .\PAMValidation.psm1 ; Enable-PAMUsersCORPClientRemote |
|  Клиент домена CORP | <PRIV>Пользователь \PRIV.pamRequestor. При использовании PRIVOnly: <CORP>\pamrequestor   | Import-module .\PAMValidation.psm1 ; Test-PAMValidationScenarioNoApprovalRequest  |


> [!div class="step-by-step"]
> [Начало "](sp1-step1-configuring-priv-domain.md)
