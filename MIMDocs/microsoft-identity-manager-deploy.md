---
title: Шаги по развертыванию Microsoft Identity Manager 2016 | Документация Майкрософт
description: Получите полный список действий, связанных с развертыванием Microsoft Identity Manager 2016 — от подготовки среды до настройки порталов.
keywords: ''
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 10/12/2017
ms.topic: article
ms.prod: microsoft-identity-manager
ms.assetid: fa0af422-b5e9-4599-9d9b-cb6c18ea07f9
ms.reviewer: mwahl
ms.suite: ems
ms.openlocfilehash: fdf3745979be2d911c9cc1c245149328311e7ad8
ms.sourcegitcommit: 7de35aaca3a21192e4696fdfd57d4dac2a7b9f90
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/16/2018
ms.locfileid: "49358148"
---
# <a name="deploy-microsoft-identity-manager-2016-sp1"></a>Развертывание Microsoft Identity Manager 2016 с пакетом обновления 1 (SP1)
Статьи в этом разделе содержат пошаговые инструкции по развертыванию Microsoft Identity Manager (MIM) 2016 для сценариев самообслуживания пользователей на новом сервере, где FIM и MIM ранее не развертывались.

> [!NOTE]
> Топология развертывания, описанная в этом разделе, предназначена только для начала работы и изучения MIM.  В [руководстве по планированию ресурсов](capacity-planning-guide.md) приведены более подробные сведения о топологиях рабочего развертывания.  Рекомендуем ознакомиться с этой документации перед развертыванием MIM для использования в рабочей среде.

Сценарий управления привилегированным доступом развертывается иначе, чем другие сценарии MIM, поскольку для его выполнения требуется выделенная среда леса-бастиона.  Чтобы узнать больше о развертывании MIM для управления привилегированными пользователями, см. статью [Настройка среды MIM для управления привилегированными пользователями](./pam/configuring-mim-environment-for-pam.md).

Процесс развертывания MIM почти такой же, как и у его предшественника, FIM 2010 R2. Документацию по FIM см. в [руководстве по развертыванию Forefront Identity Manager 2010 R2](https://technet.microsoft.com/library/jj134310).

## <a name="first-prepare-a-domain"></a>Первый этап: подготовка домена
MIM работает с Active Directory (AD), поэтому выполните следующие действия, чтобы настроить контроллер домена AD.
- [Настройка домена](preparing-domain.md)

## <a name="next-prepare-an-identity-management-servers"></a>Следующий этап: подготовка серверов управления удостоверениями
После создания и настройки домена подготовьте корпоративный сервер управления удостоверениями. Сюда входят следующие задачи:
- [Windows Server 2016](prepare-server-ws2016.md)
- [SQL Server 2016](prepare-server-sql2016.md)
- [SharePoint 2016](prepare-server-sharepoint.md)
- [Exchange Server](prepare-server-exchange.md) (необязательно).

## <a name="finally-install-microsoft-identity-manager-2016-sp1-components"></a>Последний этап: установка компонентов Microsoft Identity Manager 2016 с пакетом обновления 1 (SP1)
После настройки домена и сервера вы можете установить компоненты MIM и настроить их для синхронизации с AD.
- [Служба синхронизации MIM](install-mim-sync.md)
- [Служба и портал MIM](install-mim-service-portal.md)
- [Синхронизация баз данных Active Directory и службы MIM](install-mim-sync-ad-service.md)
- [Поддерживаемые платформы для MIM 2016 или более поздней версии](microsoft-identity-manager-2016-supported-platforms.md)
