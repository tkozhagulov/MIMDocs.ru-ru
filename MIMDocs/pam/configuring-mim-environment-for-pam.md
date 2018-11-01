---
title: Настройка MIM 2016 для Privileged Access Management | Документация Майкрософт
description: Руководство по установке MIM и настройке Privileged Access Management.
keywords: ''
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 08/31/2017
ms.topic: article
ms.prod: microsoft-identity-manager
ms.assetid: c4ca5b58-ad0c-48af-a9eb-b71b22d0c67c
ms.reviewer: mwahl
ms.suite: ems
ms.openlocfilehash: fd444f9c67f1daeaf33883a988f54a97e12e685c
ms.sourcegitcommit: 44a2293ff17c50381a59053303311d7db8b25249
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/31/2018
ms.locfileid: "50379521"
---
# <a name="configure-the-mim-environment-for-privileged-access-management"></a>Настройка среды MIM для Privileged Access Management

При настройке среды для доступа между лесами, установки и настройки Active Directory и Microsoft Identity Manager, а также демонстрации своевременного запроса доступа необходимо пройти семь этапов.

Эти этапы описаны таким образом, чтобы вы могли построить тестовую среду с нуля. Если вы применяете PAM к существующей среде, вместо создания новых контроллеров доменов, соответствующих примерам, можете использовать собственные контроллеры доменов или учетные записи пользователей.

1. Подготовьте сервер *CORPDC* как контроллер домена, а *CORPWKSTN* — как участвующую рабочую станцию.

2. Подготовьте сервер *PRIVDC* как контроллер домена.

3.  Подготовьте сервер *PAMSRV* в лесу *PRIV* .

4.  Установите компоненты MIM на сервере *PAMSRV* , а командлеты — на рабочей станции из леса *CONTOSO* , и подготовьте их к управлению привилегированным доступом.

5.  Установите отношения доверия между лесами *PRIV* *CONTOSO* .

6.  Подготовьте привилегированные группы безопасности, предоставив им доступ к защищенным ресурсам и учетным записям участников для своевременного управления привилегированным доступом.

7.  Продемонстрируйте отправку запросов, их получение и использование повышенных прав привилегированного доступа к защищенному ресурсу.

> [!div class="step-by-step"]
> [Начало "](step-1-prepare-corp-domain.md)
