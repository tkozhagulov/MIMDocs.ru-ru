---
title: Поддерживаемые платформы ПО | Документация Майкрософт
description: Поиск продуктов и версий, совместимых с каждым из компонентов MIM 2016
keywords: ''
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 02/22/2019
ms.topic: article
ms.prod: microsoft-identity-manager
ms.assetid: 4978f60d-044d-4e84-8d93-65801fce1144
ms.reviewer: ''
ms.suite: ems
ms.custom: mim
ms.openlocfilehash: c6da739349f8c4ba4016635e326ed30d5f5954c6
ms.sourcegitcommit: 67e2de99f86e762125979233f6ee80afcd78dc4d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/25/2019
ms.locfileid: "56795423"
---
# <a name="supported-platforms-for-mim-2016"></a>Поддерживаемые платформы для MIM 2016

В этой таблице приведены поддерживаемые платформы и версии каждого компонента Microsoft Identity Manager 2016. Версии, отмеченные звездочкой (*), поддерживаются только в MIM 2016 с пакетом обновления 1 и последним исправлением.  Версии, отмеченные аббревиатурой "НР", поддерживаются, но не рекомендуются к использованию, если запускается новое развертывание этой платформы для MIM.


| **Компонент MIM** | **Платформа** | **Версия** |
|-------------------|--------------|--------------|
| **Синхронизация MIM** | Windows Server | Windows Server 2008 R2 с пакетом обновления 1 (SP1) (НР)<br/>Windows Server 2012 (НР)<br/>Windows Server 2012 R2<br/>Windows Server 2016* |
| | Режим работы Active Directory для подготовки пользователей, PCNS и синхронизации GAL | Windows 2000 (НР)<br/>Windows Server 2003<br/>Windows Server 2008<br/>Windows Server 2008 R2<br/>Windows Server 2012<br/>Windows Server 2012 R2<br/>Windows Server 2016*
| | База данных синхронизации MIM | SQL Server 2008 R2 с пакетом обновления 3 (SP3) (НР)<br/>SQL Server 2012 с пакетом обновления 2 (SP2)<br/>SQL Server 2014 с пакетом обновления 1 (SP1) <br/> SQL Server 2016* |
| | Active Directory для подготовки пользователей, PCNS и синхронизации GAL (необязательно)|Windows Server 2008 R2 с пакетом обновления 1 (SP1)<br/>Windows Server 2012<br/>Windows Server 2012 R2 <br/> Windows Server 2016* |
| | Exchange для подготовки почтовых ящиков и синхронизации GAL (необязательно)|Exchange Server 2010 с пакетом обновления 3 (SP3) (НР)<br/>Exchange Server 2013 с пакетом обновления 1 (SP1)<br/>Exchange Server 2016 * |
| | Среда разработки (необязательно) | Visual Studio 2012<br/>Visual Studio 2013 <br/> Visual Studio 2015 <br/> Visual Studio 2017 * |
| | Дополнительная подключенная система (необязательно) | Доменные службы Active Directory<br/>Active Directory<br/>Службы облегченного доступа к каталогам<br/>SQL Server 2008 или более поздней версии<br/>SharePoint Server 2013<br/> SharePoint Server 2016* <br/> Другие продукты сторонних производителей |
| **Служба и портал MIM** | Windows Server | Windows Server 2008 R2 с пакетом обновления 1 (SP1) (НР)<br/>Windows Server 2012 (НР)<br/>Windows Server 2012 R2 <br/> Windows Server 2016* |
| |Сценарий PAM:  Windows Server | Windows Server 2012 R2 (НР) <br/> Windows Server 2016* |
| |Сценарий PAM: Active Directory для леса PAM в среде бастиона | Windows Server 2012 R2 (НР) <br/> Windows Server 2016* |
| |Сценарий PAM: Active Directory для существующих лесов (CORP) сценария PAM | Windows Server 2008 <br/> Windows Server 2008 R2 * <br/> Windows Server 2012 * <br/> Windows Server 2012 R2 * <br/> Windows Server 2016* |
| | База данных службы MIM | SQL Server 2008 R2 с пакетом обновления 3 (SP3) (НР)<br/>SQL Server 2012 с пакетом обновления 2 (SP2)<br/>SQL Server 2014 с пакетом обновления 1 (SP1) <br/> SQL Server 2016 |
| | SharePoint | SharePoint Foundation 2010 (NR)<br/>SharePoint Foundation 2013 с пакетом обновления 1 (SP1) <br/> SharePoint 2016* |
| | Почтовый сервер для утверждения службы MIM и сообщений электронной почты для управления группами (необязательно) | Exchange Server 2010 с пакетом обновления 3 (SP3)<br/>Exchange Server 2013 с пакетом обновления 1 (SP1) <br/> Exchange Server 2016 * <br/> Exchange Online * (только уведомления) до сборки [4.4.1749.0](https://docs.microsoft.com/microsoft-identity-manager/reference/version-history#version-4417490) |
| | Браузер | Все основные поддерживаемые браузеры * (ограничено мобильными устройствами)|
| **Отчеты службы MIM** | Windows Server |  Windows Server 2008 R2 с пакетом обновления 1 (SP1) (НР)<br/>Windows Server 2012 (НР) <br/>Windows Server 2012 R2 <br/> Windows Server 2016* |
| | Хранилище данных | System Center 2012 Service Manager <br/> Диспетчер служб System Center 2012 R2 <br/> System Center 2016 Service Manager * (с версией 4.4.1459)<br/> [Совместимость версий SQL Server для System Center 2016](https://docs.microsoft.com/system-center/scsm/upgrade-to-sm-2016) |
| **Порталы сброса пароля и регистрации MIM** | Windows Server | Windows Server 2008 R2 с пакетом обновления 1 (SP1) (НР)<br/>Windows Server 2012 (НР)<br/>Windows Server 2012 R2 <br/> Windows Server 2016* |
| | веб-браузер | Все основные поддерживаемые браузеры |
| **Надстройки и расширения MIM** | Windows | Windows 7<br/>Windows 8<br/>Windows 8.1<br/>Windows 10 |
| | Интеграция с Outlook (необязательно) | Outlook 2010 (в Windows, за исключением технологии "нажми и работай")<br/>Outlook 2013 (в Windows, за исключением технологии "нажми и работай") <br/> Outlook 2016 (в Windows 10, за исключением технологии "нажми и работай") * |
| | Командлеты запрашивающей стороны PAM PowerShell (необязательно) | Windows 8.1<br/>Windows 10 |
| **Управление сертификатами MIM** (интеграция с сервером и ЦС) | Windows server | Windows Server 2008 R2 с пакетом обновления 1 (SP1) (НР)<br/>Windows Server 2012 R2 <br/> Windows Server 2016* |
| | Центр сертификации | Windows Server 2008 R2 с пакетом обновления 1 (SP1) (НР)<br/>Windows Server 2012<br/>Windows Server 2012 R2 <br/> Windows Server 2016* |
| | База данных MIM CM | SQL Server 2008 R2 с пакетом обновления 3 (SP3) (НР)<br/>SQL Server 2012 с пакетом обновления 2 (SP2)<br/>SQL Server 2014 с пакетом обновления 1 (SP1) <br/> SQL Server 2016* |
| **Управление сертификатами MIM** (приложение) | Windows | Windows 8<br/>Windows 8.1<br/>Windows 10 |
| **Управление сертификатами MIM** (пакетный клиент) | Windows | Windows 7 |
| **Управление сертификатами MIM** (смарт-карта на основе клиента ActiveX) | Windows | Windows 7 <br/> Windows 8 <br/> Windows 8.1 <br/> Windows 10 |
| **MIM BHOLD Suite** | Windows Server | Windows Server 2008 R2 с пакетом обновления 1 (SP1) (НР)<br/>Windows Server 2012 R2 <br/> Windows Server 2016* |
| | База данных BHOLD | SQL Server 2008 R2 с пакетом обновления 3 (SP3) (НР)<br/>SQL Server 2012 с пакетом обновления 2 (SP2) <br/> SQL Server 2014* <br/> SQL Server 2016* |
| | Почтовый сервер (необязательно) | Exchange Server 2010 с пакетом обновления 3 (SP3)<br/>Exchange Server 2013 с пакетом обновления 1 (SP1) <br/> Exchange Server 2016 * |
| | веб-браузер | Поддерживаемые Internet Explorer браузеры с Silverlight |
