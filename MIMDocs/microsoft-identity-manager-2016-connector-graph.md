---
title: Соединитель Microsoft Identity Manager для Microsoft Graph | Документы Майкрософт
author: fimguy
description: Соединитель Microsoft Identity Manager для Microsoft Graph позволяет управлять жизненным циклом учетных записей Active Directory для внешних пользователей. Мы рассмотрим сценарий, в котором организация пригласила гостей в каталог Azure AD и намерена предоставить им доступ к локальным приложениям, поддерживающим встроенную проверку подлинности Windows или Kerberos.
keywords: ''
ms.author: billmath
manager: mtillman
ms.date: 10/02/2018
ms.topic: article
ms.prod: microsoft-identity-manager
ms.assetid: 94a74f1c-2192-4748-9a25-62a526295338
ms.openlocfilehash: 2e376bcc88518b911f93ce9cd4ab920eb428815b
ms.sourcegitcommit: 7de35aaca3a21192e4696fdfd57d4dac2a7b9f90
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/16/2018
ms.locfileid: "49358658"
---
<a name="microsoft-identity-manager-connector-for-microsoft-graph"></a>Соединитель Microsoft Identity Manager для Microsoft Graph
=======================================================================================

<a name="summary"></a>Сводка 
=======

[Соединитель Microsoft Identity Manager для Microsoft Graph](http://go.microsoft.com/fwlink/?LinkId=717495) позволяет применять расширенные сценарии интеграции для клиентов Azure AD Premium.  Он предоставляет доступ к дополнительным объектам в метавселенной синхронизации MIM, которые создаются через [API Microsoft Graph](https://developer.microsoft.com/en-us/graph/) версии 1 или бета-версии.

<a name="scenarios-covered"></a>Поддерживаемые сценарии
=================

<a name="b2b-account-lifecycle-management"></a>Управление жизненным циклом учетной записи B2B
--------------------------------

Основной сценарий использования соединителя Microsoft Identity Manager для Microsoft Graph — это управление жизненным циклом учетных записей Active Directory для внешних пользователей. В этом сценарии организация синхронизирует данные сотрудников с Azure AD из доменных служб Active Directory с помощью Azure AD Connect, а также пригласила гостей в каталог Azure AD. Приглашение гостя приводит к тому, что в каталоге Azure AD организации появляется объект внешнего пользователя, который отсутствует в доменных службах Active Directory организации. Затем организации требуется предоставить гостям доступ к локальным приложениям, поддерживающим встроенную проверку подлинности Windows или Kerberos, используя [Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-publish) или другие шлюзовые механизмы. Для Azure AD Application Proxy требуется, чтобы каждый пользователь применял собственную учетную запись доменных служб Active Directory для идентификации и делегирования.  

Чтобы получить сведения о том, как настроить синхронизацию MIM для автоматического создания и обслуживания учетных записей AD DS для гостей, после изучения инструкций в этой статье обратитесь к статье [Совместная работа Azure Active Directory B2B с MIM 2016 с пакетом обновления 1 (SP1) и Azure Active Directory Application Proxy](~/microsoft-identity-manager-2016-graph-b2b-scenario.md).  В этой статье представлены правила синхронизации, необходимые для соединителя.

<a name="other-identity-management-scenarios"></a>Другие сценарии управления удостоверениями
---------------

Соединитель можно использовать и для других задач управления удостоверениями, включая создание, чтение, обновление и удаление объектов пользователей, групп и контактов в Azure AD, помимо синхронизации пользователей и групп с Azure AD. При оценке возможных сценариев имейте в виду следующее: соединитель нельзя применять в сценариях, которые приводят к перекрытию потоков данных, фактическим или потенциальным конфликтам синхронизации с развертыванием Azure AD Connect.  [Azure AD Connect](https://www.microsoft.com/en-us/download/details.aspx?id=47594) — рекомендуемое решение для интеграции локальных каталогов с Azure AD путем синхронизации пользователей и групп из локальных каталогов с Azure AD.  Azure AD Connect обладает гораздо более широкими возможностями синхронизации и обеспечивает такие сценарии, как обратная запись паролей и устройств, которые не поддерживаются для объектов, создаваемых с помощью MIM. Например, если данные переносятся в доменные службы Active Directory, убедитесь в том, что Azure AD Connect не будет пытаться снова сопоставить их с каталогом Azure AD.  Соединитель также нельзя использовать для внесения изменений в объекты Azure AD, которые были созданы с помощью Azure AD Connect.



<a name="preparing-to-use-the-connector-for-microsoft-graph"></a>Подготовка к использованию соединителя для Microsoft Graph
=============================================================

<a name="authorizing-the-connector-to-retrieve-or-manage-objects-in-your-azure-ad-directory"></a>Авторизация соединителя для получения объектов или управления ими в каталоге Azure AD
----------------------------------------------------

1.  Соединитель требует создания веб-приложения или приложения API в Azure AD. Это позволит ему получить необходимые разрешения для работы с объектами Azure AD посредством Microsoft Graph.

![](media/microsoft-identity-manager-2016-ma-graph/724d3fc33b4c405ab7eb9126e7fe831f.png)

Изображение 1. Регистрация нового приложения

2.  На портале Azure откройте созданное приложение и на странице подключения агента управления сохраните идентификатор приложения как идентификатор клиента для дальнейшего использования.

![](media/microsoft-identity-manager-2016-ma-graph/ecfcb97674790290aa9ca2dcaccdafbc.png)

Изображение 2. Идентификатор приложения

3.  Создайте секрет клиента, открыв "Все параметры" -\> "Ключи". Введите описание ключа и требуемую длительность его действия. Сохраните изменения. Значение секрета станет недоступным после того, как вы покинете эту страницу.

![](media/microsoft-identity-manager-2016-ma-graph/fdbae443f9e6ccb650a0cb73c9e1a56f.png)

Изображение 3. Новый секрет клиента

4.  Добавьте в приложение API Microsoft Graph, открыв раздел "Необходимые разрешения".

![](media/microsoft-identity-manager-2016-ma-graph/908788fbf8c3c75101f7b663a8d78a4b.png)

Изображение 4. Добавление нового API

Чтобы приложение могло использовать API Microsoft Graph, в зависимости от сценария ему необходимо предоставить следующее разрешение.

| Операции с объектом | Требуемое разрешение                                                                  | Тип разрешения |
|-----------------------|--------------------------------------------------------------------------------------|-----------------|
| Импорт группы          | `Group.Read.All` или `Group.ReadWrite.All`                                                | Приложение     |
| Импорт пользователя           | `User.Read.All`, `User.ReadWrite.All`, `Directory.Read.All` или `Directory.ReadWrite.All` | Приложение     |

Дополнительные сведения о требуемых разрешениях можно найти [здесь](https://developer.microsoft.com/en-us/graph/docs/concepts/permissions_reference).

5. Предоставьте приложению необходимые разрешения.


<a name="installing-the-connector"></a>Установка соединителя
========================

6.  Перед установкой соединителя убедитесь в том, что на сервере синхронизации имеются следующие компоненты. 

 - Microsoft .NET Framework 4.5.2 или более поздней версии
 - Microsoft Identity Manager 2016 с пакетом обновления 1 (SP1) и исправлением 4.4.1642.0 [KB4021562](https://www.microsoft.com/en-us/download/details.aspx?id=55794) или более поздней версии

7. Соединитель для Microsoft Graph, также как и другие соединители для Microsoft Identity Manager 2016 с пакетом обновления 1 (SP1), можно скачать из [Центра загрузки Майкрософт](https://www.microsoft.com/en-us/download/details.aspx?id=51495).

8.  Перезапустите службу синхронизации MIM.
 
<a name="connector-configuration"></a>Конфигурация соединителя
=======================


9.  В пользовательском интерфейсе Synchronization Service Manager выберите **Соединители** и **Создать**.
Выберите **Graph (Microsoft)**, создайте соединитель и присвойте ему описательное имя.

![](media/microsoft-identity-manager-2016-graph-b2b-scenario/d95c6b2cc7951b607388cbd25920d7d0.png)


10. В пользовательском интерфейсе службы синхронизации MIM укажите идентификатор приложения и созданный секрет клиента. Для каждого агента управления, настроенного в рамках синхронизации MIM, нужно создать собственное приложение в AzureAD, чтобы избежать параллельных операций импорта в одном приложении.


![](media/microsoft-identity-manager-2016-ma-graph/77c2eb73bab8d5187da06293938f5fd9.png)

Изображение 5. Страница "Подключение"

Страница подключения (рис. 5) содержит используемую версию API Graph и имя клиента. Идентификатор клиента и секрет клиента представляют идентификатор приложения и значение ключа для приложения WebAPI, которое нужно создать в Azure AD.

11. Внесите необходимые изменения на странице глобальных параметров.

![](media/microsoft-identity-manager-2016-ma-graph/e22d4ee99f2bb825704dd83c1b26dac2.png)

Изображение 6. Страница "Глобальные параметры"

Страница глобальных параметров содержит следующие настройки.

- Формат даты и времени, который используется для любого атрибута с типом Edm.DateTimeOffset. Во время импорта все даты преобразуются в строки на основе этого формата. Настроенный формат применяется для любого атрибута, который сохраняет дату.

 - Время ожидания HTTP (в секундах), которое используется при каждом HTTP-вызове к приложению WebAPI.

 - Force change password for created user at next sign (Принудительное изменение пароля для созданного пользователя при следующем входе) — этот параметр применяется к тем пользователям, которые создаются в процессе экспорта. Если этот параметр включен, свойство [forceChangePasswordNextSignIn](https://developer.microsoft.com/en-us/graph/docs/api-reference/v1.0/resources/passwordprofile) получает значение true, в противном случае — false.

<a name="configuring-the-connector-schema-and-operations"></a>Настройка схемы и операций соединителя
=========================

12.   Настройте схему.  Соединитель поддерживает объекты перечисленных ниже типов.

-   User (Пользователь)

    -   Полный или разностный импорт

    -   Экспорт (добавление, обновление и удаление)

-   Group

    -   Полный или разностный импорт

    -   Экспорт (добавление, обновление и удаление)


Список поддерживаемых типов атрибутов:

-   `Edm.Boolean`

-   `Edm.String`

-   `Edm.DateTimeOffset` (строка в пространстве соединителя)

-   `microsoft.graph.directoryObject` (ссылка из пространства соединителя на объект любого поддерживаемого типа)

-   `microsoft.graph.contact`

Атрибуты с множественными значениями (коллекции) также поддерживаются для любого типа, указанного в списке выше.

Соединитель использует атрибут `id` для привязки и различающееся имя для всех объектов.  По этой причине переименование не требуется, так как API Graph не разрешает изменять атрибут id для объекта.


<a name="access-token-lifetime"></a>Время существования маркера доступа
=====================

Приложению Graph требуется маркер доступа, чтобы получить доступ к API Graph. Соединитель запрашивает новый маркер доступа для каждой новой итерации импорта (их количество зависит от размера страниц). Пример.

-   Azure AD содержит 10 000 объектов.

-   В соединителе настроен размер страницы 5000.

В этом случае каждая операция импорта будет включать две итерации, каждая из которых возвращает службе синхронизации 5000 объектов. Это означает, что маркер доступа будет запрашиваться дважды.

В процессе экспорта новый маркер доступа запрашивается для каждого добавляемого, обновляемого или удаляемого объекта.

<a name="troubleshooting"></a>Диагностика
===============

**Включить ведение журналов**

Если в Graph возникнут любые проблемы, журналы помогут определить их. Это позволяет включать трассировки [так же, как для универсальных соединителей](https://social.technet.microsoft.com/wiki/contents/articles/21086.fim-2010-r2-troubleshooting-how-to-enable-etw-tracing-for-connectors.aspx). Также вы можете просто добавить следующий текст в файл `miiserver.exe.config` (в раздел `system.diagnostics/sources`).


\<source name="ConnectorsLog" switchValue="Verbose"\>

\<listeners\>

>   \<add initializeData="ConnectorsLog" type="System.Diagnostics.EventLogTraceListener, System, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" name="ConnectorsLogListener" traceOutputOptions="LogicalOperationStack, DateTime, Timestamp, Call stack" /\>

\<remove name="Default" /\>

\</listeners\>

\</source\>

>[!NOTE]
>Если включен параметр "Запустить этот агент управления в отдельном процессе", следует использовать файл `dllhost.exe.config` вместо `miiserver.exe.config`.

**Ошибка из-за истечения срока действия маркера доступа**

Соединитель может вернуть ошибку HTTP 401 (доступ запрещен) с сообщением "Access token has expired" (Истек срок действия маркера доступа).

![](media/microsoft-identity-manager-2016-ma-graph/ce9e23ffe17e3dac79b58bba31cb5a8d.png)

Изображение 7. Ошибка "Access token has expired" (Истек срок действия маркера доступа) Ошибка

Эта проблема может быть вызвана настройками срока действия для маркера доступа на стороне Azure. По умолчанию срок действия маркера доступа истекает через 1 час. Чтобы увеличить это время, воспользуйтесь инструкциями из [этой статьи](https://docs.microsoft.com/azure/active-directory/active-directory-configurable-token-lifetimes).

Пример для [общедоступной предварительной версии модуля PowerShell для Azure AD](https://www.powershellgallery.com/packages/AzureADPreview).

![](media/microsoft-identity-manager-2016-ma-graph/a26ded518f94b9b557064b73615c71f6.png)

New-AzureADPolicy -Definition \@('{"TokenLifetimePolicy":{"Version":1, **"AccessTokenLifetime":"5:00:00"**}}') -DisplayName "OrganizationDefaultPolicyScenario" -IsOrganizationDefault \$true -Type "TokenLifetimePolicy"

<a name="next-steps"></a>Дальнейшие шаги
----------
- [Обозреватель Graph (отлично подходит для устранения неполадок в HTTP-вызовах)]( https://developer.microsoft.com/en-us/graph/graph-explorer)
- [Политики поддержки и внесения критических изменений в Microsoft Graph, а также доступные версии](https://developer.microsoft.com/en-us/graph/docs/concepts/versioning_and_support)
- [Страница для скачивания соединителя Microsoft Identity Manager для Microsoft Graph](http://go.microsoft.com/fwlink/?LinkId=717495)

<a name="scenario-specific-guides"></a>Руководства по сценариям
----------------------------------
[Комплексное развертывание MIM B2B]( ~/microsoft-identity-manager-2016-graph-b2b-scenario.md)
