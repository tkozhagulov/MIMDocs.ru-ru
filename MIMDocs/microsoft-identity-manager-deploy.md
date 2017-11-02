---
title: "Шаги по развертыванию Microsoft Identity Manager 2016 | Документация Майкрософт"
description: "Получите полный список действий, связанных с развертыванием Microsoft Identity Manager 2016 — от подготовки среды до настройки порталов."
keywords: 
author: billmath
ms.author: barclayn
manager: mbaldwin
ms.date: 10/12/2017
ms.topic: article
ms.service: microsoft-identity-manager
ms.technology: security
ms.assetid: fa0af422-b5e9-4599-9d9b-cb6c18ea07f9
ms.reviewer: mwahl
ms.suite: ems
ms.openlocfilehash: 2730c41d9b95d3c6e44c12dc734a0e9e13792a32
ms.sourcegitcommit: f077508b5569e2a96084267879c5b6551e1e0905
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/12/2017
---
# <a name="deploy-mim-2016"></a>Развертывание MIM 2016
Статьи в этом разделе содержат пошаговые инструкции по развертыванию Microsoft Identity Manager (MIM) 2016 для сценариев самообслуживания пользователей на новом сервере, где FIM и MIM ранее не развертывались.

> [!NOTE]
> Топология развертывания, описанная в этом разделе, предназначена только для начала работы и изучения MIM.  В [руководстве по планированию ресурсов](capacity-planning-guide.md) приведены более подробные сведения о топологиях рабочего развертывания.  Рекомендуем ознакомиться с этой документации перед развертыванием MIM для использования в рабочей среде.

Сценарий управления привилегированным доступом развертывается иначе, чем другие сценарии MIM, поскольку для его выполнения требуется выделенная среда леса-бастиона.  Чтобы узнать больше о развертывании MIM для управления привилегированными пользователями, см. статью [Настройка среды MIM для управления привилегированными пользователями](./pam/configuring-mim-environment-for-pam.md).

Процесс развертывания MIM 2016 почти такой же, как и его предшественника, FIM 2010 R2. Документацию по FIM см. в [руководстве по развертыванию Forefront Identity Manager 2010 R2](https://technet.microsoft.com/library/jj134310).

## <a name="first-prepare-a-domain"></a>Первый этап: подготовка домена
MIM работает с Active Directory (AD), поэтому выполните следующие действия, чтобы настроить контроллер домена AD.
- [Настройка домена](preparing-domain.md)

## <a name="next-prepare-an-identity-management-server"></a>Следующий этап: подготовка сервера удостоверений
После создания и настройки домена подготовьте корпоративный сервер управления удостоверениями. Сюда входят следующие задачи:
- [Windows Server 2012 R2](prepare-server-ws2012r2.md)
- [SQL Server 2014](prepare-server-sql2014.md)
- [SharePoint](prepare-server-sharepoint.md)
- [Exchange Server](prepare-server-exchange.md) (необязательно).

## <a name="finally-install-microsoft-identity-manager-2016-components"></a>Последний этап: установка компонентов Microsoft Identity Manager 2016
После настройки домена и сервера вы можете установить компоненты MIM и настроить их для синхронизации с AD.
- [Служба синхронизации MIM](install-mim-sync.md)
- [Служба и портал MIM](install-mim-service-portal.md)
- [Синхронизация баз данных Active Directory и службы MIM](install-mim-sync-ad-service.md)
