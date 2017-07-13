---
title: "Поддерживаемые платформы ПО | Документация Майкрософт"
description: "Поиск продуктов и версий, совместимых с каждым из компонентов MIM 2016"
keywords: 
author: fimguy
ms.author: fimguy
manager: femila
ms.date: 06/06/2017
ms.topic: article
ms.service: microsoft-identity-manager
ms.technology: security
ms.assetid: 4978f60d-044d-4e84-8d93-65801fce1144
ms.reviewer: mwahl
ms.suite: ems
ms.custom: mim
ms.openlocfilehash: e8f1d72930cd5998b5d9957e8b8f5dbd958f8342
ms.sourcegitcommit: 02fb1274ae0dc11288f8bd9cd4799af144b8feae
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/13/2017
---
# Поддерживаемые платформы для MIM 2016
<a id="supported-platforms-for-mim-2016" class="xliff"></a>

В этой таблице приведены поддерживаемые платформы и версии каждого компонента Microsoft Identity Manager 2016. Версии, отмеченные звездочкой (*), поддерживаются только в MIM 2016 с пакетом обновления 1.


| **Компонент MIM** | **Платформа** | **Версия** |
|-------------------|--------------|-------------|
| **Синхронизация MIM** | Windows Server | Windows Server 2008 R2 с пакетом обновления 1 (SP1)<br/>Windows Server 2012<br/>Windows Server 2012 R2<br/>Windows Server 2016* |
| | База данных синхронизации MIM | SQL Server 2008 R2 с пакетом обновления 3 (SP3)<br/>SQL Server 2012 с пакетом обновления 2 (SP2)<br/>SQL Server 2014 с пакетом обновления 1 (SP1) <br/> SQL Server 2016* |
| | Active Directory для подготовки пользователей, PCNS и синхронизации GAL (необязательно)|Windows Server 2008 R2 с пакетом обновления 1 (SP1)<br/>Windows Server 2012<br/>Windows Server 2012 R2 <br/> Windows Server 2016* |
| | Exchange для подготовки почтовых ящиков и синхронизации GAL (необязательно)|Exchange Server 2010 с пакетом обновления 3 (SP3)<br/>Exchange Server 2013 с пакетом обновления 1 (SP1)<br/>Exchange Server 2016* |
| | Среда разработки (необязательно) | Visual Studio 2012<br/>Visual Studio 2013 <br/> Visual Studio 2015 <br/> Visual Studio 2017* |
| | Дополнительная подключенная система (необязательно) | Доменные службы Active Directory<br/>Active Directory<br/>Службы облегченного доступа к каталогам<br/>SQL Server 2000 или более поздней версии<br/>SharePoint Server 2013<br/> SharePoint Server 2016* <br/> Другие продукты сторонних производителей |
| **Служба и портал MIM** | Windows Server | Windows Server 2012<br/>Windows Server 2012 R2 <br/> Windows Server 2016* |
| | Active Directory для леса PAM в среде бастиона | Windows Server 2012 R2 <br/> Windows Server 2016* |
| | Active Directory для существующих лесов | Windows Server 2008 <br/> Windows Server 2008 R2 * <br/> Windows Server 2012 * <br/> Windows Server 2012 R2 * <br/> Windows Server 2016* |
| | База данных службы MIM | SQL Server 2008 R2 с пакетом обновления 3 (SP3)<br/>SQL Server 2012 с пакетом обновления 2 (SP2)<br/>SQL Server 2014 с пакетом обновления 1 (SP1) <br/> SQL Server 2016* |
| | SharePoint | SharePoint Foundation 2010<br/>SharePoint Foundation 2013 с пакетом обновления 1 (SP1) <br/> SharePoint 2016* |
| | Почтовый сервер для утверждения службы MIM и сообщений электронной почты для управления группами (необязательно) | Exchange Server 2010 с пакетом обновления 3 (SP3)<br/>Exchange Server 2013 с пакетом обновления 1 (SP1) <br/> Exchange Server 2016 * <br/> Exchange Online * (только уведомления) |
| | Браузер | Все основные браузеры * |
| **Отчеты службы MIM** | Windows Server | Windows Server 2012 <br/> Windows Server 2016* |
| | Хранилище данных | System Center 2012 Service Manager <br/> Диспетчер служб System Center 2012 R2 </br> System Center 2016 Service Manager * (с версией 4.4.1459)<br/> [Совместимость версий SQL Server для System Center 2016](https://docs.microsoft.com/system-center/scsm/upgrade-to-sm-2016)
 |
| **Порталы сброса пароля и регистрации MIM** | Windows Server | Windows Server 2008 R2 с пакетом обновления 1 (SP1)<br/>Windows Server 2012<br/>Windows Server 2012 R2 <br/> Windows Server 2016* |
| | веб-браузер | Все основные браузеры |
| **Надстройки и расширения MIM** | Windows | Windows 7<br/>Windows 8<br/>Windows 8.1<br/>Windows 10 |
| | Интеграция с Outlook (необязательно) | Outlook 2007 с пакетом обновления 2 (SP2)<br/>Outlook 2010<br/>Outlook 2013 <br/> Outlook 2016 (в Windows 10)* |
| | Командлеты запрашивающей стороны PAM PowerShell (необязательно) | Windows 8.1<br/>Windows 10 |
| **Управление сертификатами MIM** (интеграция с сервером и ЦС) | Windows server | Windows Server 2008 R2 с пакетом обновления 1 (SP1)<br/>Windows Server 2012 R2 <br/> Windows Server 2016* |
| | Центр сертификации | Windows Server 2008 R2 с пакетом обновления 1 (SP1)<br/>Windows Server 2012<br/>Windows Server 2012 R2 <br/> Windows Server 2016* |
| | База данных MIM CM | SQL Server 2008 R2 с пакетом обновления 3 (SP3)<br/>SQL Server 2012 с пакетом обновления 2 (SP2)<br/>SQL Server 2014 с пакетом обновления 1 (SP1) <br/> SQL Server 2016* |
| **Управление сертификатами MIM** (приложение) | Windows | Windows 8<br/>Windows 8.1<br/>Windows 10 |
| **Управление сертификатами MIM** (клиент и массовый клиент) | Windows | Windows 7 |
| **MIM BHOLD Suite** | Windows Server | Windows Server 2008 R2 с пакетом обновления 1 (SP1)<br/>Windows Server 2012 R2 <br/> Windows Server 2016* |
| | База данных BHOLD | SQL Server 2008 R2 с пакетом обновления 3 (SP3)<br/>SQL Server 2012 с пакетом обновления 2 (SP2) <br/> SQL Server 2014* <br/> SQL Server 2016* |
| | Почтовый сервер (необязательно) | Exchange Server 2010 с пакетом обновления 3 (SP3)<br/>Exchange Server 2013 с пакетом обновления 1 (SP1) <br/> Exchange Server 2016 * |
| | веб-браузер | Internet Explorer 7, 8, 9, 10 или 11 с Silverlight |
