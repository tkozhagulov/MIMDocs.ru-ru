---
title: "Поддерживаемые соединители | Документация Майкрософт"
description: "Используйте соединители для управления передачей данных между MIM и вашими каталогами."
keywords: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 03/11/2017
ms.topic: article
ms.service: microsoft-identity-manager
ms.technology: security
ms.assetid: 8bc2f6d2-9f53-4db6-aee6-a937ae468163
ms.reviewer: mwahl
ms.suite: ems
ms.openlocfilehash: b26fe7bc56ab8229054afb1409c3652e81464a3d
ms.sourcegitcommit: 02fb1274ae0dc11288f8bd9cd4799af144b8feae
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/13/2017
---
# <a name="connect-to-your-directories"></a>Подключение к каталогам

Соединители связывают конкретные источники данных с Microsoft Identity Manager (MIM). Соединитель перемещает данные из подключенного источника данных в MIM. При изменении данных в MIM соединитель может также экспортировать данные в подключенный источник данных для синхронизации с MIM. Обычно для каждого подключенного каталога существует по меньшей мере один соединитель.

В Forefront Identity Manager соединители назывались агентами управления. Этот термин по-прежнему используется в некоторых статьях или компонентах продукта, но оба термина относятся к одной концепции.

В этой статье рассказывается о соединителях, включенных в MIM, однако соединитель для Extensible Connectivity 2.0 позволяет подключиться к еще большему количеству источников данных. Некоторые партнеры таким образом создали собственные соединители; полный список доступен на вики-сайте [FIM 2010: агенты управления от партнеров](http://social.technet.microsoft.com/wiki/contents/articles/1589.fim-2010-management-agents-from-partners.aspx).

## <a name="supported-connectors-in-mim-2016"></a>Поддерживаемые соединители в MIM 2016

| Название | Поддерживаемые версии подключенного источника данных |
| ---- | ----------------------------------------------- |
| Доменные службы Active Directory | Active Directory 2000, 2003, 2003 R2, 2008, 2008 R2, 2012 |
| Службы Active Directory облегченного доступа к каталогам (ADLDS) | Службы Active Directory облегченного доступа к каталогам (ADLDS) |
| Глобальный список адресов Active Directory (GAL) | Глобальный список адресов Active Directory (GAL) — Exchange 2000, 2003, 2007, 2010, 2013 |
| Extensible Connectivity 2.0 | Любой источник данных на основе вызовов или файлов |
| Служба MIM | Microsoft Docs 2016 |
| Универсальная база данных IBM DB2 | IBM DB2 версии 9.1, 9.5 или 9.7; IBM DB2 OLEDB версии 9.5 FP5 или версии 9.7 FP1 |
| Сервер каталогов IBM | Сервер каталогов IBM Tivoli 6.x |
| Novell eDirectory | Novell eDirectory версии 8.7.3, 8.8.5 и 8.8.6 |
| База данных Oracle | База данных Oracle 10g или 11g; 64-разрядный клиент |
| Microsoft SQL Server | SQL Server 2000, 2005, 2008, 2008 R2, 2012 |
| Серверы каталогов Oracle (ранее Sun и Netscape) | Сервер каталогов Sun 6.x, 7.x и Oracle 11 |
| [Соединитель Windows PowerShell для FIM 2010 R2](https://msdn.microsoft.com/en-us/library/dn640417.aspx) | Windows PowerShell 2.0 или более поздней версии |
| [Соединитель Microsoft Azure Active Directory для FIM 2010 R2](https://msdn.microsoft.com/en-us/library/dn511001.aspx) | Microsoft Azure Active Directory |
| [Универсальный соединитель LDAP для FIM 2010 R2](https://msdn.microsoft.com/en-us/library/dn510997.aspx) | Сервер LDAP v3 (совместимый с RFC 4510) |
| [Соединитель для Lotus Domino](https://msdn.microsoft.com/en-us/library/hh859750.aspx) | Заметки о выпуске Lotus v8.0.x или v8.5.x |
| [Соединитель служб SharePoint Services для FIM 2010 R2](https://msdn.microsoft.com/en-us/library/dn511003.aspx) | SharePoint Server 2013 или 2016 с приложением службы профиля пользователя (UPA) |
| [Соединитель для веб-служб](https://www.microsoft.com/en-us/download/details.aspx?id=51495) | SAP ECC 5.0 или 6.0; Oracle PeopleSoft 9.1; Oracle eBusiness 12.1 |
| Текстовый файл пары «атрибут-значение» | Текстовые файлы пары «атрибут-значение» |
| Текстовый файл с разделителями | Текстовые файлы с разделителями |
| Язык разметки службы каталогов (DSML) | Язык разметки службы каталогов (DSML) 2.0 |
| Текстовый файл с фиксированной шириной | Текстовые файлы с фиксированной шириной |
| Формат обмена данными LDAP (LDIF) | Формат обмена данными LDAP (LDIF) |

## <a name="related-topics"></a>См. также

[Агенты управления в FIM 2010 R2](https://technet.microsoft.com/library/jj133885.aspx)
