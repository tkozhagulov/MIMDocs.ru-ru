---
title: "Сведения о гибридных отчетах | Документация Майкрософт"
description: "Гибридные отчеты о действиях аудита в Azure Active Directory позволяют просматривать облачные и локальные события аудита."
keywords: 
author: fimguy
ms.author: fimguy
manager: bhu
ms.date: 09/28/2017
ms.topic: article
ms.service: microsoft-identity-manager
ms.technology: security
ms.assetid: 7320f014-8b60-4866-92de-cfbd3e6edc48
ms.reviewer: fimguy
ms.suite: ems
ms.openlocfilehash: 151fbd26011ca76901d181131a88ded8a718a27a
ms.sourcegitcommit: 0f99de31fe6b52ec692b3886073909f549a451d6
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/29/2017
---
# <a name="hybrid-identity-management-audit-reports-in-azure-active-directory---public-previewrefresh"></a>Отчеты аудита управления гибридными удостоверениями в Azure Active Directory — общедоступная предварительная версия (обновление)
Отчеты о действиях аудита Azure Active Directory (AD) позволяют просматривать единый отчет для мониторинга управления удостоверениями и локально, и в облаке. Эта функция позволяет управлять всеми удостоверениями и просматривать данные в одном месте, что экономит время и сокращает общие затраты.

## <a name="what-is-azure-active-directory-hybrid-reporting"></a>Что такое гибридные отчеты Azure Active Directory?
Гибридные отчеты аудита помогают ИТ-специалистам устранить распространенные проблемы с отчетами об управлении удостоверениями.

1. **Сбор данных об управлении удостоверениями в разных системах.** Гибридные отчеты предоставляют сведения об управлении удостоверениями в Azure AD и Identity Manager.

2. **Экспорт данных отчетов и создание настраиваемых отчетов.** Помимо просмотра отчетов на портале Azure, можно также экспортировать данные для создания собственных настраиваемых представлений.

3. **Снижение стоимости инфраструктуры системы отчетности.** Возможность создания гибридных отчетов в облаке позволяет обойтись без локальной инфраструктуры хранилища данных отчетов.

## <a name="how-does-it-work"></a>Как это работает?

Чтобы собирать локальные данные, сначала необходимо установить агент создания отчетов на сервере Identity Manager 2016. Агент создания отчетов можно скачать в [Центре загрузки Майкрософт](https://www.microsoft.com/en-us/download/details.aspx?id=55112).

Процесс создания гибридных отчетов состоит из следующих этапов:
1. После установки агента создания отчетов данные о действиях Identity Manager отправляются в журнал событий Windows.
2. Агент создания отчетов обрабатывает разностные события каждые 10 минут или при перезагрузки службы в журнале событий Windows и отправляет их на портал Azure.
3. Портал Azure обрабатывает полученные данные в течение 1 часа после получения.
4. Данные о действиях хранятся в Azure один месяц.
5. Портал Azure извлекает данные отчетов аудита и отображает их как аудит в колонке отчетов аудита Azure.

## <a name="next-steps"></a>Дальнейшие действия
- Дополнительные сведения см. в статье [Работа с гибридными отчетами диспетчера удостоверений](working-with-identity-manager-hybrid-reporting.md).
- Дополнительные сведения см. в статье [Отчеты о действиях аудита на портале Azure Active Directory](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-reporting-activity-audit-logs)
- Дополнительные сведения о [политиках хранения отчетов](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-reporting-retention)
- Дополнительные сведения об [интеграции журналов Microsoft Azure (SIEM)](https://docs.microsoft.com/en-us/azure/security/security-azure-log-integration-overview)
- Дополнительные сведения об [API отчетов Azure Active Directory](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-reporting-api-getting-started)
