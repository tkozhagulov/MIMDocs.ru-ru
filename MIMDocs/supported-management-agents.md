---
title: Поддерживаемые соединители | Документация Майкрософт
description: Используйте соединители для управления передачей данных между MIM и вашими подключенными источниками данных.
keywords: ''
author: fimguy
ms.author: fimguy
manager: bhu
ms.date: 1/24/2018
ms.topic: article
ms.service: microsoft-identity-manager
ms.technology: security
ms.assetid: 8bc2f6d2-9f53-4db6-aee6-a937ae468163
ms.reviewer: ''
ms.suite: ems
ms.openlocfilehash: 7b685ffb6f2a52bd2782395e4c1f26501ffe3101
ms.sourcegitcommit: c773edc8262b38df50d82dae0f026bb49500d0a4
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/05/2018
ms.locfileid: "34479355"
---
# <a name="connect-to-your-directories"></a>Подключение к каталогам

Соединители связывают конкретные источники данных с Microsoft Identity Manager (MIM) с пакетом обновления 1 (SP1). Соединитель перемещает данные из подключенного источника данных в MIM. При изменении данных в MIM соединитель может также экспортировать данные в подключенный источник данных для синхронизации с MIM. Обычно для каждого подключенного каталога существует по меньшей мере один соединитель.

В Forefront Identity Manager соединители назывались агентами управления. Этот термин по-прежнему используется в некоторых статьях или компонентах продукта, но оба термина относятся к одной концепции.

В этой статье рассказывается о соединителях, включенных и поддерживаемых в MIM, однако соединитель для Extensible Connectivity 2.0 позволяет подключиться к еще большему количеству источников данных. Некоторые партнеры таким образом создали собственные соединители; полный список доступен на вики-сайте [FIM 2010: агенты управления от партнеров](http://social.technet.microsoft.com/wiki/contents/articles/1589.fim-2010-management-agents-from-partners.aspx).

## <a name="supported-connectors-in-mim-2016-sp1"></a>Поддерживаемые соединители в MIM 2016 с пакетом обновления 1 (SP1)

| Название | Поддерживаемые версии подключенного источника данных и ссылки на техническую документацию |
| ---- | ----------------------------------------------- |
| Доменные службы Active Directory | Active Directory 2012, 2016 |
| Службы Active Directory облегченного доступа к каталогам (ADLDS) | Службы Active Directory облегченного доступа к каталогам (ADLDS) |
| Глобальный список адресов Active Directory (GAL) | Глобальный список адресов Active Directory (GAL) — Exchange 2013, 2016 |
| Extensible Connectivity 2.0 | Любой источник данных на основе вызовов или файлов |
| Служба FIM | Версия агента управления службы FIM (служба синхронизации) должна совпадать с версией установленной службы Forefront Identity Manager. |
| Универсальная база данных IBM DB2 | IBM DB2 версии 9.5 или 9.7; IBM DB2 OLEDB версии 9.5 FP5 или версии 9.7 FP1 |
| Сервер каталогов IBM | Сервер каталогов IBM Tivoli 6.x |
| Novell eDirectory | Novell eDirectory версии 8.7.3, 8.8.5 и 8.8.6 |
| База данных Oracle | База данных Oracle 10g или 11g; 64-разрядный клиент |
| Microsoft SQL Server | SQL Server 2012, 2014, 2016 |
| Серверы каталогов Oracle (ранее Sun и Netscape) | Сервер каталогов Sun 6.x, 7.x и Oracle 11 |
| [Соединитель Windows PowerShell для FIM 2010 R2](https://msdn.microsoft.com/library/dn640417.aspx) | Windows PowerShell 2.0 или более поздней версии |
| [Соединитель Microsoft Azure Active Directory для FIM 2010 R2](https://msdn.microsoft.com/library/dn511001.aspx) | Microsoft Azure Active Directory |
| [Универсальный соединитель LDAP для FIM 2010 R2](https://msdn.microsoft.com/library/dn510997.aspx) | [Сервер LDAP v3 (совместимый с RFC 4510)](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnectsync-connector-genericldap) |
| [Универсальный соединитель SQL для FIM 2010 R2 или MIM](https://msdn.microsoft.com/library/dn510997.aspx) | [Все 64-разрядные драйверы ODBC поддерживают соединитель](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnectsync-connector-genericsql) |
| [Соединитель для Lotus Domino](https://msdn.microsoft.com/library/hh859750.aspx) | Заметки о выпуске Lotus 8.5.x |
| [Соединитель служб SharePoint Services для UPA](https://msdn.microsoft.com/library/dn511003.aspx) | SharePoint Server 2013 или 2016 с приложением службы профиля пользователя (UPA) |
| [Соединитель для веб-служб](https://www.microsoft.com/en-us/download/details.aspx?id=51495) | [SAP ECC 5.0 или 6.0; Oracle PeopleSoft 9.1; Oracle eBusiness 12.1](https://docs.microsoft.com/microsoft-identity-manager/reference/microsoft-identity-manager-2016-ma-ws) |
| [Текстовый файл пар "атрибут-значение"](https://technet.microsoft.com/library/cc708644(v=ws.10).aspx) | Текстовые файлы пары «атрибут-значение» |
| [Текстовый файл с разделителями](https://technet.microsoft.com/library/cc720612(v=ws.10).aspx) | Текстовые файлы с разделителями |
| [Язык разметки службы каталогов (DSML)](https://technet.microsoft.com/library/cc720660(v=ws.10).aspx) | Язык разметки службы каталогов (DSML) 2.0 |
| [Текстовый файл с фиксированной шириной](https://technet.microsoft.com/library/cc720633(v=ws.10).aspx) | Текстовые файлы с фиксированной шириной |
| [Формат обмена данными LDAP (LDIF)](https://technet.microsoft.com/library/cc708662(v=ws.10).aspx) | Формат обмена данными LDAP (LDIF) |

## <a name="related-topics"></a>См. также

[Агенты управления в FIM 2010 R2](https://technet.microsoft.com/library/jj133885.aspx)
