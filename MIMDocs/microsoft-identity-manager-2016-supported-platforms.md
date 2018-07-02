---
title: Поддерживаемые платформы ПО | Документация Майкрософт
description: Поиск продуктов и версий, совместимых с каждым из компонентов MIM 2016
keywords: ''
author: fimguy
ms.author: davidste
manager: davidste
ms.date: 04/11/2017
ms.topic: article
ms.service: microsoft-identity-manager
ms.technology: security
ms.assetid: 4978f60d-044d-4e84-8d93-65801fce1144
ms.reviewer: ''
ms.suite: ems
ms.custom: mim
ms.openlocfilehash: 1054d611ae0b230005a0f79be69f5c6c2bba7af2
ms.sourcegitcommit: c773edc8262b38df50d82dae0f026bb49500d0a4
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/05/2018
ms.locfileid: "34479304"
---
# <a name="supported-platforms-for-mim-2016"></a>Поддерживаемые платформы для MIM 2016

В этой таблице приведены поддерживаемые платформы и версии каждого компонента Microsoft Identity Manager 2016. Версии, отмеченные звездочкой (*), поддерживаются только в MIM 2016 с пакетом обновления 1 и последним исправлением.


| **Компонент MIM** | **Платформа** | **Версия** |
|-------------------|--------------|--------------|
| **Синхронизация MIM** | Windows Server | Windows Server 2008 R2 с пакетом обновления 1 (SP1)<br/>Windows Server 2012<br/>Windows Server 2012 R2<br/>Windows Server 2016* |
| | Режим работы Active Directory для подготовки пользователей, PCNS и синхронизации GAL | Windows 2000 <br/>Windows Server 2003<br/>Windows Server 2008<br/>Windows Server 2008 R2<br/>Windows Server 2012<br/>Windows Server 2012 R2<br/>Windows Server 2016*
| | База данных синхронизации MIM | SQL Server 2008 R2 с пакетом обновления 3 (SP3)<br/>SQL Server 2012 с пакетом обновления 2 (SP2)<br/>SQL Server 2014 с пакетом обновления 1 (SP1) <br/> SQL Server 2016* |
| | Active Directory для подготовки пользователей, PCNS и синхронизации GAL (необязательно)|Windows Server 2008 R2 с пакетом обновления 1 (SP1)<br/>Windows Server 2012<br/>Windows Server 2012 R2 <br/> Windows Server 2016* |
| | Exchange для подготовки почтовых ящиков и синхронизации GAL (необязательно)|Exchange Server 2010 с пакетом обновления 3 (SP3)<br/>Exchange Server 2013 с пакетом обновления 1 (SP1)<br/>Exchange Server 2016* |
| | Среда разработки (необязательно) | Visual Studio 2012<br/>Visual Studio 2013 <br/> Visual Studio 2015 <br/> Visual Studio 2017* |
| | Дополнительная подключенная система (необязательно) | Доменные службы Active Directory<br/>Active Directory<br/>Службы облегченного доступа к каталогам<br/>SQL Server 2008 или более поздней версии<br/>SharePoint Server 2013<br/> SharePoint Server 2016* <br/> Другие продукты сторонних производителей |
| **Служба и портал MIM** | Windows Server | Windows Server 2008 R2 с пакетом обновления 1 (SP1)<br/>Windows Server 2012<br/>Windows Server 2012 R2 <br/> Windows Server 2016* |
| |В сценарии PAM: Windows Server | Windows Server 2012 R2 <br/> Windows Server 2016* |
| |В сценарии PAM: Active Directory для леса PAM в среде бастиона | Windows Server 2012 R2 <br/> Windows Server 2016* |
| |В сценарии PAM: Active Directory для существующих лесов PAM (CORP) | Windows Server 2008 <br/> Windows Server 2008 R2 * <br/> Windows Server 2012 * <br/> Windows Server 2012 R2 * <br/> Windows Server 2016* |
| | База данных службы MIM | SQL Server 2008 R2 с пакетом обновления 3 (SP3)<br/>SQL Server 2012 с пакетом обновления 2 (SP2)<br/>SQL Server 2014 с пакетом обновления 1 (SP1) <br/> SQL Server 2016 |
| | SharePoint | SharePoint Foundation 2010<br/>SharePoint Foundation 2013 с пакетом обновления 1 (SP1) <br/> SharePoint 2016* |
| | Почтовый сервер для утверждения службы MIM и сообщений электронной почты для управления группами (необязательно) | Exchange Server 2010 с пакетом обновления 3 (SP3)<br/>Exchange Server 2013 с пакетом обновления 1 (SP1) <br/> Exchange Server 2016 * <br/> Exchange Online * (только уведомления) до сборки [4.4.1749.0](https://docs.microsoft.com/microsoft-identity-manager/reference/version-history#version-4417490) |
| | Браузер | Все основные поддерживаемые браузеры * (ограничено мобильными устройствами)|
| **Отчеты службы MIM** | Windows Server |  Windows Server 2008 R2 с пакетом обновления 1 (SP1)<br/>Windows Server 2012 <br/>Windows Server 2012 R2 <br/> Windows Server 2016* |
| | Хранилище данных | System Center 2012 Service Manager <br/> Диспетчер служб System Center 2012 R2 </br> System Center 2016 Service Manager * (с версией 4.4.1459)<br/> [Совместимость версий SQL Server для System Center 2016](https://docs.microsoft.com/system-center/scsm/upgrade-to-sm-2016)
 |
| **Порталы сброса пароля и регистрации MIM** | Windows Server | Windows Server 2008 R2 с пакетом обновления 1 (SP1)<br/>Windows Server 2012<br/>Windows Server 2012 R2 <br/> Windows Server 2016* |
| | веб-браузер | Все основные поддерживаемые браузеры |
| **Надстройки и расширения MIM** | Windows | Windows 7<br/>Windows 8<br/>Windows 8.1<br/>Windows 10 |
| | Интеграция с Outlook (необязательно) | Outlook 2010<br/>Outlook 2013 <br/> Outlook 2016 (в Windows 10)* |
| | Командлеты запрашивающей стороны PAM PowerShell (необязательно) | Windows 8.1<br/>Windows 10 |
| **Управление сертификатами MIM** (интеграция с сервером и ЦС) | Windows server | Windows Server 2008 R2 с пакетом обновления 1 (SP1)<br/>Windows Server 2012 R2 <br/> Windows Server 2016* |
| | Центр сертификации | Windows Server 2008 R2 с пакетом обновления 1 (SP1)<br/>Windows Server 2012<br/>Windows Server 2012 R2 <br/> Windows Server 2016* |
| | База данных MIM CM | SQL Server 2008 R2 с пакетом обновления 3 (SP3)<br/>SQL Server 2012 с пакетом обновления 2 (SP2)<br/>SQL Server 2014 с пакетом обновления 1 (SP1) <br/> SQL Server 2016* |
| **Управление сертификатами MIM** (приложение) | Windows | Windows 8<br/>Windows 8.1<br/>Windows 10 |
| **Управление сертификатами MIM** (пакетный клиент) | Windows | Windows 7 |
| **Управление сертификатами MIM** (смарт-карта на основе клиента ActiveX) | Windows | Windows 7 </br> Windows 8 </br> Windows 8.1 </br> Windows 10 |
| **MIM BHOLD Suite** | Windows Server | Windows Server 2008 R2 с пакетом обновления 1 (SP1)<br/>Windows Server 2012 R2 <br/> Windows Server 2016* |
| | База данных BHOLD | SQL Server 2008 R2 с пакетом обновления 3 (SP3)<br/>SQL Server 2012 с пакетом обновления 2 (SP2) <br/> SQL Server 2014* <br/> SQL Server 2016* |
| | Почтовый сервер (необязательно) | Exchange Server 2010 с пакетом обновления 3 (SP3)<br/>Exchange Server 2013 с пакетом обновления 1 (SP1) <br/> Exchange Server 2016 * |
| | веб-браузер | Поддерживаемые Internet Explorer браузеры с Silverlight |
