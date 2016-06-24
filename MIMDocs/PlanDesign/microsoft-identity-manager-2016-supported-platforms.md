---
# required metadata

title: Поддерживаемые платформы для MIM 2016 | Microsoft Identity Manager
description: Поиск продуктов и версий, совместимых с каждым из компонентов MIM 2016
keywords:
author: kgremban
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-manager-2015
ms.service: microsoft-identity-manager
ms.technology: security
ms.assetid: 4978f60d-044d-4e84-8d93-65801fce1144

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: mwahl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Поддерживаемые платформы для MIM 2016

| **Компонент MIM** | **Платформа** | **Версия** |
|-------------------|--------------|-------------|
|**Синхронизация MIM**|Windows Server | Windows Server 2008 R2 с пакетом обновления 1 (SP1)<br/>Windows Server 2012<br/>Windows Server 2012 R2|
||База данных синхронизации MIM |SQL Server 2008 R2 с пакетом обновления 3 (SP3)<br/>SQL Server 2012 с пакетом обновления 2 (SP2)<br/>SQL Server 2014 с пакетом обновления 1 (SP1) |
||Active Directory для подготовки пользователей, PCNS и синхронизации GAL (необязательно)|Windows Server 2008 R2 с пакетом обновления 1 (SP1)<br/>Windows Server 2012<br/>Windows Server 2012 R2 |
||Exchange для подготовки почтовых ящиков и синхронизации GAL (необязательно)|Exchange Server 2007 с пакетом обновления 3 (SP3)<br/>Exchange Server 2010 с пакетом обновления 3 (SP3)<br/>Exchange Server 2013 с пакетом обновления 1 (SP1) |
|| Среда разработки (необязательно) | Visual Studio 2012<br/>Visual Studio 2013 |
|| Дополнительная подключенная система (необязательно) | Доменные службы Active Directory<br/>Active Directory<br/>Службы облегченного доступа к каталогам<br/>SQL Server 2000 или более поздней версии<br/>SharePoint Server 2013<br/>Другие продукты сторонних производителей |
| **Службы MIM** (за исключением сценария PAM) | Windows Server | Windows Server 2008 R2 с пакетом обновления 1 (SP1)<br/>Windows Server 2012<br/>Windows Server 2012 R2 |
|| База данных службы MIM | SQL Server 2008 R2 с пакетом обновления 3 (SP3)<br/>SQL Server 2012 с пакетом обновления 2 (SP2)<br/>SQL Server 2014 с пакетом обновления 1 (SP1) |
|| Exchange для утверждения службы MIM и сообщений электронной почты для управления группами (необязательно) | Exchange Server 2007 с пакетом обновления 3 (SP3) (с установленной консолью управления Exchange)<br/>Exchange Server 2010 с пакетом обновления 3 (SP3)<br/>Exchange Server 2013 с пакетом обновления 1 (SP1) |
| **Служба и портал MIM** (только для сценария PAM)| Windows Server | Windows Server 2012<br/>Windows Server 2012 R2 |
|| Active Directory для леса PAM в среде бастиона | Windows Server 2012 R2 |
|| Active Directory для существующих лесов | Windows Server 2008 или более поздней версии |
|| База данных службы MIM | SQL Server 2008 R2 с пакетом обновления 3 (SP3)<br/>SQL Server 2012 с пакетом обновления 2 (SP2)<br/>SQL Server 2014 с пакетом обновления 1 (SP1) |
|| SharePoint | SharePoint Foundation 2010<br/>SharePoint Foundation 2013 с пакетом обновления 1 (SP1) |
|| Почтовый сервер для утверждения службы MIM и сообщений электронной почты для управления группами (необязательно) | Exchange Server 2007 с пакетом обновления 3 (SP3) (с установленной консолью управления Exchange)<br/>Exchange Server 2010 с пакетом обновления 3 (SP3)<br/>Exchange Server 2013 с пакетом обновления 1 (SP1) |
|| Браузер | Internet Explorer 8, 9, 10 или 11 |
| **Отчеты службы MIM** | Windows Server | Windows Server 2012 |
|| Хранилище данных | Диспетчер служб System Center 2012 с пакетом обновления 1 (SP1) |
|| База данных хранилища данных | SQL Server 2008 R2 с пакетом обновления 3 (SP3)<br/>SQL Server 2012 с пакетом обновления 2 (SP2) |
| **Порталы сброса пароля и регистрации MIM** | Windows Server | Windows Server 2008 R2 с пакетом обновления 1 (SP1)<br/>Windows Server 2012<br/>Windows Server 2012 R2 |
|| веб-браузер | Internet Explorer 7, 8, 9, 10 или 11<br/>Другие веб-браузеры |
| **Надстройки и расширения MIM** | Windows | Windows 7<br/>Windows 8<br/>Windows 8.1<br/>Windows 10 |
|| Интеграция с Outlook (необязательно) | Outlook 2007 с пакетом обновления 2 (SP2)<br/>Outlook 2010<br/>Outlook 2013 |
|| Командлеты запрашивающей стороны PAM PowerShell (необязательно) | Windows 8.1<br/>Windows 10 |
| **Управление сертификатами MIM** (интеграция с сервером и ЦС) | Windows server | Windows Server 2008 R2 с пакетом обновления 1 (SP1)<br/>Windows Server 2012 R2 |
|| Центр сертификации | Windows Server 2008 R2 с пакетом обновления 1 (SP1)<br/>Windows Server 2012<br/>Windows Server 2012 R2 |
|| База данных MIM CM | Windows Server 2008 R2 с пакетом обновления 1 (SP1)<br/>Windows Server 2012<br/>Windows Server 2012 R2 |
| **Управление сертификатами MIM** (приложение) | Windows | Windows 8<br/>Windows 8.1<br/>Windows 10 |
| **Управление сертификатами MIM** (клиент и массовый клиент) | Windows | Windows 7 |
| **MIM BHOLD Suite** | Windows Server | Windows Server 2008 R2 с пакетом обновления 1 (SP1)<br/>Windows Server 2012 R2 |
|| База данных BHOLD | SQL Server 2008 R2 с пакетом обновления 3 (SP3)<br/>SQL Server 2012 с пакетом обновления 2 (SP2) |
|| Почтовый сервер (необязательно) | Exchange Server 2007 с пакетом обновления 3 (SP3)<br/>Exchange Server 2010 с пакетом обновления 3 (SP3)<br/>Exchange Server 2013 с пакетом обновления 1 (SP1) |
|| веб-браузер | Internet Explorer 7, 8, 9, 10 или 11 с Silverlight |


<!--HONumber=Apr16_HO2-->


