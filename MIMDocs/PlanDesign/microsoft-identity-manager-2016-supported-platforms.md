---
title: "Поддерживаемые платформы ПО | Документация Майкрософт"
description: "Поиск продуктов и версий, совместимых с каждым из компонентов MIM 2016"
keywords: 
author: kgremban
ms.author: kgremban
manager: femila
ms.date: 03/28/2017
ms.topic: article
ms.service: microsoft-identity-manager
ms.technology: security
ms.assetid: 4978f60d-044d-4e84-8d93-65801fce1144
ms.reviewer: mwahl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: f1faed3a09023e288a68a8950dae43725f19eb3e
ms.openlocfilehash: 33c84afa4d6fd2ed7bde33de39dd151f83f07fd4
ms.lasthandoff: 04/12/2017


---

# <a name="supported-platforms-for-mim-2016"></a>Поддерживаемые платформы для MIM 2016

В этой таблице приведены поддерживаемые платформы и версии каждого компонента Microsoft Identity Manager 2016. Версии, отмеченные звездочкой (*), поддерживаются только в MIM 2016 с пакетом обновления 1.


| **Компонент MIM** | **Платформа** | **Версия** |
|-------------------|--------------|-------------|
| **Синхронизация MIM** | Windows Server | Windows Server 2008 R2 с пакетом обновления 1 (SP1)<br/>Windows Server 2012<br/>Windows Server 2012 R2<br/>Windows Server 2016* |
| | База данных синхронизации MIM | SQL Server 2008 R2 с пакетом обновления 3 (SP3)<br/>SQL Server 2012 с пакетом обновления 2 (SP2)<br/>SQL Server 2014 с пакетом обновления 1 (SP1) <br/> SQL Server 2016* |
| | Active Directory для подготовки пользователей, PCNS и синхронизации GAL (необязательно)|Windows Server 2008 R2 с пакетом обновления 1 (SP1)<br/>Windows Server 2012<br/>Windows Server 2012 R2 <br/> Windows Server 2016* |
| | Exchange для подготовки почтовых ящиков и синхронизации GAL (необязательно)|Exchange Server 2010 с пакетом обновления 3 (SP3)<br/>Exchange Server 2013 с пакетом обновления 1 (SP1)<br/>Exchange Server 2016* |
| | Среда разработки (необязательно) | Visual Studio 2012<br/>Visual Studio 2013 <br/> Visual Studio 2015 <br/> Visual Studio 2017* |
| | Дополнительная подключенная система (необязательно) | Доменные службы Active Directory<br/>Active Directory<br/>Службы облегченного доступа к каталогам<br/>SQL Server 2000 или более поздней версии<br/>SharePoint Server 2013<br/> SharePoint Server 2016* <br/> Другие продукты сторонних производителей |
| **Службы MIM** (за исключением сценария PAM) | Windows Server | Windows Server 2008 R2 с пакетом обновления 1 (SP1)<br/>Windows Server 2012<br/>Windows Server 2012 R2 <br/> Windows Server 2016* |
| | База данных службы MIM | SQL Server 2008 R2 с пакетом обновления 3 (SP3)<br/>SQL Server 2012 с пакетом обновления 2 (SP2)<br/>SQL Server 2014 с пакетом обновления 1 (SP1) <br/> SQL Server 2016* |
| | Exchange для утверждения службы MIM и сообщений электронной почты для управления группами (необязательно) | Exchange Server 2010 с пакетом обновления 3 (SP3)<br/>Exchange Server 2013 с пакетом обновления 1 (SP1) <br/> Exchange Server 2016 * <br/> Exchange Online * (только уведомления) |
| **Служба и портал MIM** (только для сценария PAM)| Windows Server | Windows Server 2012<br/>Windows Server 2012 R2 <br/> Windows Server 2016* |
| | Active Directory для леса PAM в среде бастиона | Windows Server 2012 R2 <br/> Windows Server 2016* |
| | Active Directory для существующих лесов | Windows Server 2008 <br/> Windows Server 2008 R2 * <br/> Windows Server 2012 * <br/> Windows Server 2012 R2 * <br/> Windows Server 2016* |
| | База данных службы MIM | SQL Server 2008 R2 с пакетом обновления 3 (SP3)<br/>SQL Server 2012 с пакетом обновления 2 (SP2)<br/>SQL Server 2014 с пакетом обновления 1 (SP1) <br/> SQL Server 2016* |
| | SharePoint | SharePoint Foundation 2010<br/>SharePoint Foundation 2013 с пакетом обновления 1 (SP1) <br/> SharePoint 2016* |
| | Почтовый сервер для утверждения службы MIM и сообщений электронной почты для управления группами (необязательно) | Exchange Server 2010 с пакетом обновления 3 (SP3)<br/>Exchange Server 2013 с пакетом обновления 1 (SP1) <br/> Exchange Server 2016 * <br/> Exchange Online * (только уведомления) |
| | Браузер | Все основные браузеры |
| **Отчеты службы MIM** | Windows Server | Windows Server 2012 <br/> Windows Server 2016* |
| | Хранилище данных | System Center 2012 Service Manager <br/> Диспетчер служб System Center 2012 R2 </br> System Center 2016 Service Manager * (с версией 4.4.1459)<br/> [Совместимость версий SQL Server для System Center 2016](https://technet.microsoft.com/en-us/system-center-docs/system-requirements/sql-server-version-compatibility)
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

