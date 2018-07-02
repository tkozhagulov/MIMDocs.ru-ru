---
title: Агент управления Microsoft Identity Manager для Microsoft Graph | Документация Майкрософт
author: fimguy
description: Microsoft Graph (предварительная версия) — это средство, которое позволяет управлять жизненным циклом учетных записей Active Directory для внешних пользователей. Мы рассмотрим сценарий, в котором организация пригласила гостей в каталог Azure AD и намерена предоставить им доступ к локальным приложениям, поддерживающим встроенную проверку подлинности Windows или Kerberos.
keywords: ''
ms.author: davidste
manager: bhu
ms.date: 04/25/2018
ms.topic: article
ms.service: microsoft-identity-manager
ms.technology: security
ms.assetid: 94a74f1c-2192-4748-9a25-62a526295338
ms.openlocfilehash: a66d424e8388005855ac8e64623f5a00f89682e9
ms.sourcegitcommit: c773edc8262b38df50d82dae0f026bb49500d0a4
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/05/2018
ms.locfileid: "34479372"
---
<a name="the-microsoft-identity-manager-management-agent-for-microsoft-graph-public-preview"></a>Агент управления Microsoft Identity Manager для Microsoft Graph (общедоступная предварительная версия)
=======================================================================================

<a name="summary"></a>Сводка 
=======

[Агент управления Microsoft Identity Manager для Microsoft Graph (предварительная версия)](http://go.microsoft.com/fwlink/?LinkId=717495) позволяет применять расширенные сценарии интеграции для клиентов Azure AD Premium.

[Azure AD Connect](https://www.microsoft.com/en-us/download/details.aspx?id=47594) интегрирует локальные каталоги с Azure AD и предоставляет пользователям единые удостоверения и согласованную аутентификацию во всех доменных службах Active Directory, Office 365, Azure и приложениях SaaS, интегрированных с AAD. Эта служба синхронизирует пользователей и группы из локальных каталогов в AAD.   Развернув агент управления, вы получите ряд специализированных возможностей для управления удостоверениями и доступом в дополнение к синхронизации пользователей и групп с Azure AD.  Этот агент управления предоставляет доступ к дополнительным объектам в метавселенной синхронизации MIM, которые создаются через [API Microsoft Graph](https://developer.microsoft.com/en-us/graph/) версии 1 или бета-версии. 

<a name="scenarios-covered"></a>Поддерживаемые сценарии
=================

<a name="b2b-account-lifecycle-management"></a>Управление жизненным циклом учетной записи B2B
--------------------------------

Основной сценарий работы в предварительной версии агента управления Microsoft Identity Manager для Microsoft Graph — это управление жизненным циклом учетной записи внешнего пользователя AD. Мы рассмотрим сценарий, в котором организация пригласила гостей в каталог Azure AD и намерена предоставить им доступ к локальным приложениям, поддерживающим встроенную проверку подлинности Windows или Kerberos, используя [Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-publish) или другие шлюзовые механизмы. Для Azure AD Application Proxy требуется, чтобы каждый пользователь применял собственную учетную запись доменных служб Active Directory для идентификации и делегирования.

В будущем могут быть добавлены дополнительные сценарии. Документация по ним публикуется [здесь](./microsoft-identity-manager-2016-graph-b2b-scenario.md).

<a name="determining-your-deployment-topology"></a>Определение топологии развертывания
====================================


<a name="preparing-to-use-the-management-agentma-for-microsoft-graph"></a>Подготовка к использованию агента управления для Microsoft Graph
=============================================================

<a name="authorizing-the-ma-to-manage-your-azure-ad-directory"></a>Авторизация агента управления для управления каталогом Azure AD
----------------------------------------------------

1.  Для работы агента управления Graph нужно создать веб-приложение или приложение API в Azure AD.

![](media/microsoft-identity-manager-2016-ma-graph/724d3fc33b4c405ab7eb9126e7fe831f.png)

Изображение 1. Регистрация нового приложения

2.  Откройте созданное приложение и примените идентификатор приложения (например, идентификатор клиента) на странице подключения агента управления.

![](media/microsoft-identity-manager-2016-ma-graph/ecfcb97674790290aa9ca2dcaccdafbc.png)

Изображение 2. Идентификатор приложения

2.  Создайте секрет клиента, открыв "Все параметры" -\> "Ключи". Введите описание ключа и требуемую длительность его действия. Сохраните изменения. Значение секрета станет недоступным после того, как вы покинете эту страницу.

![](media/microsoft-identity-manager-2016-ma-graph/fdbae443f9e6ccb650a0cb73c9e1a56f.png)

Изображение 3. Новый секрет клиента

3.  Добавьте в приложение API Microsoft Graph, открыв раздел "Необходимые разрешения".

![](media/microsoft-identity-manager-2016-ma-graph/908788fbf8c3c75101f7b663a8d78a4b.png)

Изображение 4. Добавление нового API

Для API Microsoft Graph следует добавить следующие разрешения.

| Операции с объектом | Требуемое разрешение                                                                  | Тип разрешения |
|-----------------------|--------------------------------------------------------------------------------------|-----------------|
| Импорт группы          | User.Read.All или Group.ReadWrite.All                                                | Приложение     |
| Импорт пользователя           | User.Read.All или User.ReadWrite.All либо Directory.Read.All или Directory.ReadWrite.All | Приложение     |

Дополнительные сведения о требуемых разрешениях можно найти [здесь](https://developer.microsoft.com/en-us/graph/docs/concepts/permissions_reference).

1.  Создайте соединитель, указав идентификатор приложения и созданный ранее секрет клиента. Для каждого агента управления нужно создать собственное приложение в AzureAD, чтобы избежать параллельных операций импорта в одном приложении. Соединитель Graph поддерживает объекты следующих типов.

-   User (Пользователь)

    -   Полный или разностный импорт

    -   Экспорт (добавление, обновление и удаление)

-   Group

    -   Полный или разностный импорт

    -   Экспорт (добавление, обновление и удаление)


Список поддерживаемых типов атрибутов:

-   Edm.Boolean

-   Edm.String

-   Edm.DateTimeOffset (строка в пространстве соединителя);

-   microsoft.graph.directoryObject (ссылка из пространства соединителя на объект любого поддерживаемого типа);

-   microsoft.graph.contact.

Атрибуты с множественными значениями (коллекции) также поддерживаются для любого типа, указанного в списке выше.

Соединитель Graph использует атрибут id для привязки и различающееся имя для всех объектов.

Сейчас переименование не поддерживается, поскольку API Graph не разрешает изменять атрибут id для существующего объекта.

<a name="access-token-lifetime"></a>Время существования маркера доступа
=====================

Приложению Graph требуется маркер доступа, чтобы получить доступ к API Graph. Соединитель запрашивает новый маркер доступа для каждой новой итерации импорта (их количество зависит от размера страниц). Пример.

-   Azure AD содержит 10 000 объектов.

-   В соединителе настроен размер страницы 5000.

В этом случае каждая операция импорта будет включать две итерации, каждая из которых возвращает службе синхронизации 5000 объектов. Это означает, что маркер доступа будет запрашиваться дважды.

Обратите внимание, что в процессе экспорта новый маркер доступа запрашивается для каждого добавляемого, обновляемого или удаляемого объекта.

<a name="installing-the-connector"></a>Установка соединителя
========================

Прежде чем использовать соединитель, обеспечьте наличие следующих компонентов на сервере синхронизации: платформа Microsoft .NET 4.5.2 или более поздней версии, Microsoft Identity Manager 2016 с пакетом обновления 1 (SP1), обязательно с исправлением 4.4.1642.0 [KB4021562](https://www.microsoft.com/en-us/download/details.aspx?id=55794) или более поздней версии.

Соединители для Microsoft Identity Manager 2016 SP1 и соединитель Graph можно скачать из [Центра загрузки Майкрософт](https://www.microsoft.com/en-us/download/details.aspx?id=51495).

<a name="connector-configuration"></a>Конфигурация соединителя
=======================

Страница "Подключение":

![](media/microsoft-identity-manager-2016-ma-graph/77c2eb73bab8d5187da06293938f5fd9.png)

Изображение 5. Страница "Подключение"

Страница подключения (изображение 1) содержит используемые версии API Graph и имя клиента. Идентификатор клиента и секрет клиента обозначают идентификатор приложения и значение ключа для приложения WebAPI, которое нужно создать в Azure AD.

Страница "Глобальные параметры":

![](media/microsoft-identity-manager-2016-ma-graph/e22d4ee99f2bb825704dd83c1b26dac2.png)

Изображение 6. Страница "Глобальные параметры"

Страница глобальных параметров содержит следующие настройки.

Формат даты и времени, который используется для любого атрибута с типом Edm.DateTimeOffset. Во время импорта все даты преобразуются в строки на основе этого формата. Настроенный формат применяется для любого атрибута, который сохраняет дату.

Время ожидания HTTP (в секундах), которое используется при каждом HTTP-вызове к приложению WebAPI.

Force change password for created user at next sign (Принудительное изменение пароля для созданного пользователя при следующем входе) — этот параметр применяется к тем пользователям, которые создаются в процессе экспорта. Если этот параметр включен, свойство [forceChangePasswordNextSignIn](https://developer.microsoft.com/en-us/graph/docs/api-reference/v1.0/resources/passwordprofile) получает значение true, в противном случае — false.

<a name="troubleshooting"></a>Диагностика
===============

**Включить ведение журналов**

Если в Graph возникнут любые проблемы, журналы помогут определить их. Соединитель Graph использует тот же источник, что и все остальные универсальные соединители. Это позволяет включать трассировки [так же, как для универсальных соединителей](https://social.technet.microsoft.com/wiki/contents/articles/21086.fim-2010-r2-troubleshooting-how-to-enable-etw-tracing-for-connectors.aspx) (ссылка на вики-сайт). Также вы можете просто добавить следующий текст в файл miiserver.exe.config (в раздел system.diagnostics/sources):

\<source name="ConnectorsLog" switchValue="Verbose"\>

\<listeners\>

>   \<add initializeData="ConnectorsLog" type="System.Diagnostics.EventLogTraceListener, System, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" name="ConnectorsLogListener" traceOutputOptions="LogicalOperationStack, DateTime, Timestamp, Call stack" /\>

\<remove name="Default" /\>

\</listeners\>

\</source\>

Внимание! Если включен параметр "Run this management agent in a separate process" (Запустить этот агент управления в отдельном процессе), следует использовать файл dllhost.exe.config вместо miiserver.exe.config.

**Ошибка из-за истечения срока действия маркера доступа**

Соединитель может вернуть ошибку HTTP 401 (доступ запрещен) с сообщением "Access token has expired" (Истек срок действия маркера доступа).

![](media/microsoft-identity-manager-2016-ma-graph/ce9e23ffe17e3dac79b58bba31cb5a8d.png)

Изображение 7. Ошибка "Access token has expired" (Истек срок действия маркера доступа) Ошибка

Эта проблема может быть вызвана настройками срока действия для маркера доступа на стороне Azure. По умолчанию срок действия маркера доступа истекает через 1 час. Чтобы увеличить это время, воспользуйтесь инструкциями из [этой статьи](https://docs.microsoft.com/azure/active-directory/active-directory-configurable-token-lifetimes).

Пример для [общедоступной предварительной версии модуля PowerShell для Azure AD](https://www.powershellgallery.com/packages/AzureADPreview).

![](media/microsoft-identity-manager-2016-ma-graph/a26ded518f94b9b557064b73615c71f6.png)

New-AzureADPolicy -Definition \@('{"TokenLifetimePolicy":{"Version":1, **"AccessTokenLifetime":"5:00:00"**}}') -DisplayName "OrganizationDefaultPolicyScenario" -IsOrganizationDefault \$true -Type "TokenLifetimePolicy"

<a name="next-steps"></a>Дальнейшие действия
----------
- [Обозреватель Graph (отлично подходит для устранения неполадок в HTTP-вызовах)]( https://developer.microsoft.com/en-us/graph/graph-explorer)
- [Политики поддержки и внесения критических изменений в Microsoft Graph, а также доступные версии](https://developer.microsoft.com/en-us/graph/docs/concepts/versioning_and_support)
- [Страница для скачивания агента управления Microsoft Identity Manager для Microsoft Graph (предварительная версия)](http://go.microsoft.com/fwlink/?LinkId=717495)

<a name="scenario-specific-supported-guides"></a>Рекомендации по конкретным поддерживаемым сценариям
----------------------------------
[Комплексное развертывание MIM B2B]( ~/microsoft-identity-manager-2016-graph-b2b-scenario.md)
