---
# required metadata

title: Развертывание MIM 2016 | Microsoft Identity Manager
description: Получите полный список действий, связанных с развертыванием Microsoft Identity Manager 2016 — от подготовки среды до настройки порталов.
keywords:
author: kgremban
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-manager-2015
ms.service: microsoft-identity-manager
ms.technology: security
ms.assetid: fa0af422-b5e9-4599-9d9b-cb6c18ea07f9

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: mwahl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Развертывание MIM 2016
Статьи в этом разделе содержат пошаговые инструкции по развертыванию Microsoft Identity Manager (MIM) 2016 для сценариев самообслуживания пользователей на новом сервере, где FIM и MIM ранее не развертывались.

> [!NOTE]
> Топология развертывания, описанная в этом разделе, предназначена только для начала работы и изучения MIM.  В [руководстве по планированию ресурсов](/microsoft-identity-manager/plan-design/capacity-planning-guide) приведены более подробные сведения о топологиях рабочего развертывания.  Рекомендуем ознакомиться с этой документации перед развертыванием MIM для использования в рабочей среде.

<!---
Comment: Restore after PAM content is included

The privileged access management scenario is deployed differently than other MIM scenarios, as it requires a dedicated bastion forest environment.  If you want to learn more about deploying MIM for Privileged Identity Management, see [Getting Started with Privileged Access Management](privileged-access-management-get-started.md).
--->

## Первый этап: подготовка домена
MIM работает с Active Directory (AD), поэтому выполните следующие действия, чтобы настроить контроллер домена AD.
- [Настройка домена](preparing-domain.md)

## Следующий этап: подготовка сервера удостоверений
После создания и настройки домена подготовьте корпоративный сервер управления удостоверениями. Сюда входят следующие задачи:
- [Windows Server 2012 R2](prepare-server-ws2012r2.md)
- [SQL Server 2014](prepare-server-sql2014.md)
- [SharePoint](prepare-server-sharepoint.md)
- [Exchange Server](prepare-server-exchange.md) (необязательно).

## Последний этап: установка компонентов Microsoft Identity Manager 2016
После настройки домена и сервера вы можете установить компоненты MIM и настроить их для синхронизации с AD.
- [Служба синхронизации MIM](install-mim-sync.md)
- [Служба и портал MIM](install-mim-service-portal.md)
- [Синхронизация баз данных Active Directory и службы MIM](install-mim-sync-ad-service.md)


<!--HONumber=Apr16_HO4-->


