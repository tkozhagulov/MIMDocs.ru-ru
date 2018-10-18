---
title: Что такое гибридные отчеты в Azure AD | Документация Майкрософт
description: Гибридные отчеты о действиях аудита в Azure Active Directory позволяют просматривать облачные и локальные события аудита.
keywords: ''
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 02/20/2018
ms.topic: article
ms.prod: microsoft-identity-manager
ms.assetid: 7320f014-8b60-4866-92de-cfbd3e6edc48
ms.suite: ems
ms.openlocfilehash: dd87f00fb3faded60671a47a0ba1dab7e4c2a531
ms.sourcegitcommit: 7de35aaca3a21192e4696fdfd57d4dac2a7b9f90
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/16/2018
ms.locfileid: "49358182"
---
# <a name="hybrid-identity-management-audit-reporting-in-azure-active-directory"></a>Гибридные отчеты об аудите управления удостоверениями в Azure Active Directory
Отчеты о действиях аудита Azure Active Directory (Azure AD) позволяют отслеживать действия управления удостоверениями и локально, и в облаке. Управляя данными удостоверений и доступа при помощи одного отчета, можно сэкономить время и сократить общие затраты.

## <a name="what-is-azure-active-directory-hybrid-reporting"></a>Что такое гибридные отчеты Azure Active Directory?
Гибридные отчеты аудита помогают ИТ-специалистам устранять распространенные проблемы с отчетами об управлении удостоверениями, например:

* **Сбор данных об управлении удостоверениями в разных системах.** Гибридные отчеты предоставляют сведения об управлении удостоверениями в Azure AD и Identity Manager.

* **Экспорт данных отчетов и создание настраиваемых отчетов.** Кроме возможности просматривать отчеты на портале Azure, можно экспортировать данные для создания собственных настраиваемых представлений.

* **Снижение стоимости инфраструктуры для системы отчетности.** Гибридные отчеты в облаке позволяют исключить расходы на локальную инфраструктуру хранилища данных.

## <a name="how-does-it-work"></a>Как это работает?

Чтобы собирать локальные данные, сначала необходимо установить агент создания отчетов на сервере Identity Manager 2016. [Скачайте агент гибридных отчетов Microsoft Identity Manager](https://www.microsoft.com/download/details.aspx?id=55112).

Гибридные отчеты создаются следующим образом:
1. После установки агента отчетов данные о действиях в Identity Manager отправляются в журнал событий Windows.
2. Агент отчетов обрабатывает разностные события каждые 10 минут или при перезагрузке службы журнала событий Windows. Затем агент отправляет данные событий на портал Azure.
3. На портале Azure полученные данные обрабатываются в течение одного часа с момента получения.
4. Данные о действиях хранятся в Azure один месяц.
5. Данные отчетов аудита извлекаются и отображаются в колонке отчетов аудита Azure.

## <a name="next-steps"></a>Дальнейшие шаги
Дополнительные сведения
- [Работа с гибридными отчетами Identity Manager](working-with-identity-manager-hybrid-reporting.md)
- [Отчеты о действиях аудита на портале Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs)
- [Политики хранения отчетов](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-retention)
- [Интеграция журналов Microsoft Azure (SIEM)](https://docs.microsoft.com/azure/security/security-azure-log-integration-overview)
- [API отчетов Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-api-getting-started)
