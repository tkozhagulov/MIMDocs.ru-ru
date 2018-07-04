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
ms.openlocfilehash: ac11a4dfb23944d50dbbcf0b0d70c915f186c159
ms.sourcegitcommit: c773edc8262b38df50d82dae0f026bb49500d0a4
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/05/2018
ms.locfileid: "34479168"
---
<a name="azure-ad-business-to-business-b2b-collaboration-with-microsoft-identity-managermim-2016-sp1-with-azure-application-proxy-public-preview"></a>Совместная работа Azure Active Directory B2B с Microsoft Identity Manager (MIM) 2016 с пакетом обновлений 1 (SP1) и прокси приложения Azure (общедоступная предварительная версия)
============================================================================================================================

Основной сценарий применения этой предварительной версии — управление жизненным циклом учетных записей Active Directory для внешних пользователей.   Мы рассмотрим сценарий, в котором организация пригласила гостей в каталог Azure AD и намерена предоставить им доступ к локальным приложениям, поддерживающим встроенную проверку подлинности Windows или Kerberos, используя [Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-publish) или другие шлюзовые механизмы. Для Azure AD Application Proxy требуется, чтобы каждый пользователь применял собственную учетную запись доменных служб Active Directory для идентификации и делегирования.

## <a name="scenario-specific-supported-guidance"></a>Рекомендации по конкретным поддерживаемым сценариям

Мы рассмотрим сценарий, в котором организация пригласила гостей в каталог Azure AD и намерена предоставить им доступ к локальным приложениям, поддерживающим встроенную проверку подлинности Windows или Kerberos, используя [Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-publish) или другие шлюзовые механизмы. Для Azure AD Application Proxy требуется, чтобы каждый пользователь применял собственную учетную запись доменных служб Active Directory для идентификации и делегирования.

При настройке B2B с MIM и прокси приложения Azure предполагается следующее:

-   Вы уже установили [агент управления Graph](microsoft-identity-manager-2016-connector-graph.md).

-   У вас настроены локальная служба AD и Azure AD с синхронизацией пользователей и групп в Azure AD.

    -   Office Groups управляет доступом к приложениям через [Azure AD Connect](http://robsgroupsblog.com/blog/how-to-write-back-an-office-group-in-azure-active-directory-to-a-mail-enabled-security-group-in-an-on-premises-active-directory).

-   Вы уже настроили соединители прокси приложения и группы соединителей. Если это не так, воспользуйтесь [этими инструкциями](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-enable#install-and-register-a-connector) для их установки и настройки.

-   Опубликованы одно или несколько приложений, использующие встроенную проверку подлинности Windows или индивидуальные учетные записи AD через Azure AD Application Proxy.

-   Вы уже пригласили или будете приглашать одного или нескольких гостей, созданных в Azure AD <https://docs.microsoft.com/azure/active-directory/active-directory-b2b-self-service-portal>.

-   Вы установили Microsoft Identity Manager, а также настроили базовые конфигурации службы, портала и агента управления Active Directory.
    <https://docs.microsoft.com/microsoft-identity-manager/microsoft-identity-manager-deploy>

## <a name="b2b-end-to-end-deployment"></a>Комплексное развертывание B2B

Сценарий

Компания Contoso Pharmaceuticals сотрудничает с Trey Research Inc. в области исследований и разработок. Сотрудникам компании Trey Research нужен доступ к приложению для создания отчетов по исследованиям, которое предоставляет Contoso Pharmaceuticals.

-   Contoso Pharmaceuticals использует независимый клиент и настроила в нем пользовательский домен.

-   Внешний пользователь приглашен в клиент Contoso Pharmaceuticals.
    Этот пользователь принял приглашение и теперь может обращаться к совместно используемым ресурсам.

-   Для этого примера через прокси приложения опубликовано приложение, которое использует службу и портал MIM для организации участия гостевого пользователя в процессе MIM и примерах взаимодействия со службой поддержки.

## <a name="create-the-graph-management-agent"></a>Создание агента управления Graph

Примечание. Прежде, чем создавать соединитель, проверьте наличие [агента управления Graph](microsoft-identity-manager-2016-connector-graph.md).

В пользовательском интерфейсе Synchronization Service Manager выберите **Соединители** и **Создать**.
Выберите **Graph (Microsoft)** (Graph (Майкрософт)) и присвойте ему описательное имя.

![](media/microsoft-identity-manager-2016-graph-b2b-scenario/d95c6b2cc7951b607388cbd25920d7d0.png)

### <a name="connectivity"></a>Подключение

На странице "Подключение" необходимо указать версию API Graph: готовая к использованию в рабочей среде **версия 1.0** или не предназначенная для рабочей среды **бета-версия**.

![](media/microsoft-identity-manager-2016-graph-b2b-scenario/6fabfe20af0207f1556f0df18fd16f60.png)

### <a name="capabilities"></a>Характеристики

На странице глобальных параметров следует настроить для DN журнал разностных изменений и дополнительные функции LDAP. Эта страница заполняется сведениями от сервера LDAP.

![](media/microsoft-identity-manager-2016-graph-b2b-scenario/84c4dd62f63b82239cd0cf63d14fc671.png)

### <a name="global-parameters"></a>Глобальные параметры

На странице глобальных параметров следует настроить для DN журнал разностных изменений и дополнительные функции LDAP. Эта страница заполняется сведениями от сервера LDAP.

![](media/microsoft-identity-manager-2016-graph-b2b-scenario/84c4dd62f63b82239cd0cf63d14fc671.png)

### <a name="configure-provisioning-hierarchy"></a>Настройка иерархии подготовки

Эта страница используется для сопоставления компонента DN, например подразделения, c типом подготавливаемого объекта, например organizationalUnit. Сохраните здесь значение по умолчанию и щелкните "Далее".

![](media/microsoft-identity-manager-2016-graph-b2b-scenario/80016dc45b50a0b1b08ea51ad8b37977.png)

### <a name="configure-partitions-and-hierarchies"></a>Настройка разделов и иерархий

На странице разделов и иерархий выберите все пространства имен, которые содержат объекты для импорта и экспорта.

![](media/microsoft-identity-manager-2016-graph-b2b-scenario/72f0adc789ed78c66d066768146fb874.png)

#### <a name="select-object-types"></a>Выбор типов объектов

На странице разделов и иерархий выберите все пространства имен, которые содержат объекты для импорта и экспорта.

![](media/microsoft-identity-manager-2016-graph-b2b-scenario/e18921f65a0d0e4acf0775c8a01ac009.png)

#### <a name="select-attributes"></a>Выбор атрибутов

На экране "Выбор атрибутов" выберите необходимые атрибуты для управления пользователями B2B. Атрибут id является обязательным.

-   id

-   displayName

-   mail

-   givenName

-   surname

-   userPrincipalName

-   userType

![](media/microsoft-identity-manager-2016-graph-b2b-scenario/58da80f5475cf01a97a6843dd279385c.png)

#### <a name="configure-anchors"></a>Настройка привязок

Если выбрана настройка привязок, далее следует обязательный шаг настройки привязок. По умолчанию для сопоставления используется атрибут id.

![](media/microsoft-identity-manager-2016-graph-b2b-scenario/9377ab7b760221517a431384689c8c76.png)

#### <a name="configure-connector-filter"></a>Настройка фильтра соединителя

На странице настройки фильтра соединителя вы можете отфильтровать объекты с помощью фильтра по атрибутам. В нашем сценарии работы с B2B нужно добавлять только тех пользователей, у которых userType имеет значение Guest, а не Member.

![](media/microsoft-identity-manager-2016-graph-b2b-scenario/d90691fce652ba41c7a98c9a863ee710.png)

#### <a name="configure-join-and-projection-rules"></a>Настройка правил соединения и проекции

Настройка правил соединения и проекции выполняется правилом синхронизации, а значит вам не нужно определять соединения и проекции для самого соединителя. Сохраните значения по умолчанию и щелкните "ОК".

![](media/microsoft-identity-manager-2016-graph-b2b-scenario/34896440ae6ad404e824eb35d8629986.png)

#### <a name="configure-attribute-flow"></a>Настройка потока атрибута

Так же как для соединений и проекции, вам не нужно определять поток атрибутов, поскольку он обрабатывается правилом синхронизации, которое мы создадим позднее. Сохраните значения по умолчанию и щелкните "ОК".

![](media/microsoft-identity-manager-2016-graph-b2b-scenario/b7cd0d294d4f361f0551bf2cb774d5f5.png)

#### <a name="configure-deprovision"></a>Настройка отзыва

Настройка отзыва позволит удалять объекты при удалении объекта метавселенной. В этом тестовом примере мы используем разъединители, так как нам нужно сохранить их в Azure. Кроме того, мы используем только операции импорта и ничего не экспортируем в Azure.

![](media/microsoft-identity-manager-2016-graph-b2b-scenario/2394ad4d11546c6a5c69a6dad56fe6ca.png)

#### <a name="configure-extensions"></a>Настройка расширений

Настройка расширений для этого агента управления возможна, но не является обязательной, так как мы используем правила синхронизации. Если бы ранее в потоке атрибутов мы выбрали расширенное правило, здесь у нас появилась бы возможность определить его.

![](media/microsoft-identity-manager-2016-graph-b2b-scenario/74513d95b10f6ce47b7ac75fe7ab9889.png)

## <a name="creating-mim-service-synchronization-rules"></a>Создание правил синхронизации для службы MIM

На следующих шагах мы начнем сопоставлять гостевую учетную запись B2B с потоком атрибутов. Также здесь предполагается, что вы уже настроили агент управления Active Directory и взаимодействие между FIM MA и службой и порталом MIM.

Прежде чем создавать правило синхронизации, нам нужно с помощью конструктора метавселенной создать атрибут userPrincipalName, связанный с объектом пользователя.

В клиенте синхронизации выберите конструктор метавселенной.

![](media/microsoft-identity-manager-2016-graph-b2b-scenario/db3c1d353168a09aaa68678d39ea4f09.png)

Теперь выберите тип объекта Person (Пользователь).

![](media/microsoft-identity-manager-2016-graph-b2b-scenario/b5e3db86398aed558a481dd64be4f5db.png)

В разделе "Действия" щелкните "Добавить атрибут".

![](media/microsoft-identity-manager-2016-graph-b2b-scenario/47d0056eb496edd2e7b5da11a2c04718.png)

И наконец, укажите следующие данные.

Имя атрибута: **userPrincipalName**.

Тип атрибута: **String (Indexable)** (Строковый, индексируемый).

Indexed (Индексированный) = **True** (Да).

![](media/microsoft-identity-manager-2016-graph-b2b-scenario/9fba1ff9feefb17b82478ac7010edbfa.png)

![](media/microsoft-identity-manager-2016-graph-b2b-scenario/e389ee78beac3bf469ddd97bddb5e9d5.png)

Для следующих шагов необходимо настроить минимальную конфигурацию агента управления службы FIM и агента управления доменных служб Active Directory.

Дополнительные сведения об этой настройке можно найти в статье <https://technet.microsoft.com/library/ff686263(v=ws.10).aspx> — How Do I Provision Users to AD DS (Как подготовить пользователей для AD DS).

### <a name="synchronization-rule-import-guest-user-to-mv-to-synchronization-service-metaverse-from-azure-active-directorybr"></a>Правило синхронизации. Импорт гостевого пользователя в MV и метавселенную службы синхронизации из Azure Active Directory<br>

Перейдите к разделу MIM Service and Portal (Служба и портал MIM), выберите "Правила синхронизации" и щелкните "Создать".
![](media/microsoft-identity-manager-2016-graph-b2b-scenario/ba39855f54268aa824cd8d484bae83cf.png)

![](media/microsoft-identity-manager-2016-graph-b2b-scenario/de059b93474c39763f0b27874b716e15.png)Выбор действия "Создать ресурс в FIM"![](media/microsoft-identity-manager-2016-graph-b2b-scenario/9bc4a92136be1557d3596fa2eaa63e61.png)

![](media/microsoft-identity-manager-2016-graph-b2b-scenario/0ac7f4d0fd55f4bffd9e6508b494aa74.png)

Правила потока:

| **Только исходный поток** | **Использовать как проверку существования** | **Поток (значение FIM ⇒ атрибут назначения)**                          |
|-----------------------|---------------------------|-----------------------------------------------------------------------|
|                       |                           | [displayName⇒displayName](javascript:void(0);)                        |
|                       |                           | [Left(id,20)⇒accountName](javascript:void(0);)                        |
|                       |                           | [id⇒uid](javascript:void(0);)                                         |
|                       |                           | [userType⇒employeeType](javascript:void(0);)                          |
|                       |                           | [givenName⇒givenName](javascript:void(0);)                            |
|                       |                           | [surname⇒sn](javascript:void(0);)                                     |
|                       |                           | [userPrincipalName⇒userPrincipalName](javascript:void(0);)            |
|                       |                           | [id⇒cn](javascript:void(0);)                                          |
|                       |                           | [mail⇒mail](javascript:void(0);)                                      |
|                       |                           | [mobilePhone⇒mobilePhone](javascript:void(0);)                        |

### <a name="synchronization-rule-create-guest-user-account-to-active-directory"></a>Правило синхронизации. Создание учетной записи для гостевого пользователя в Active Directory 

Это правило синхронизации создает пользователя в Active Directory.

![](media/microsoft-identity-manager-2016-graph-b2b-scenario/3463e11aeb9fb566685e775d4e1b825c.png)

![](media/microsoft-identity-manager-2016-graph-b2b-scenario/e53c7ac0f376382d890e79dad597c284.png)

![](media/microsoft-identity-manager-2016-graph-b2b-scenario/1c4fad7aa68dc9697fda8f811e9ad37b.png)

Правила потока:

| **Только исходный поток** | **Использовать как проверку существования** | **Поток (значение FIM ⇒ атрибут назначения)**                          |
|-----------------------|---------------------------|-----------------------------------------------------------------------|
|                       |                           | [accountName⇒sAMAccountName](javascript:void(0);)                     |
|                       |                           | [givenName⇒givenName](javascript:void(0);)                            |
|                       |                           | [mail⇒mail](javascript:void(0);)                                      |
|                       |                           | [sn⇒sn](javascript:void(0);)                                          |
|                       |                           | [userPrincipalName⇒userPrincipalName](javascript:void(0);)            |
| **Y**                 |                           | ["CN="+uid+",OU=B2BGuest,DC=scontoso,DC=com"⇒dn](javascript:void(0);) |
| **Y**                 |                           | [RandomNum(0,999)+userPrincipalName⇒unicodePwd](javascript:void(0);)  |
| **Y**                 |                           | [262656⇒userAccountControl](javascript:void(0);)                      |

### <a name="synchronization-rule-import-b2b-guest-user-objects-sid-to-allow-for-login-to-mim"></a>Правило синхронизации. Импорт идентификатора безопасности из объектов гостевых пользователей B2B для поддержки входа в MIM 

Это правило синхронизации создает пользователя в Active Directory.

![](media/microsoft-identity-manager-2016-graph-b2b-scenario/263df23fd588c4229b958aee240071f3.png)


![](media/microsoft-identity-manager-2016-graph-b2b-scenario/047ebc3084999246bdd44b1f05ca02b3.png)

![](media/microsoft-identity-manager-2016-graph-b2b-scenario/acc0a871c0bf6f45ee928bed5abd9861.png)

![](media/microsoft-identity-manager-2016-graph-b2b-scenario/80fb9d563ec088925477a645f19b0373.png)

Теперь нам нужно пригласить пользователя и выполнить действия управления в следующем порядке:

-   полный импорт и синхронизация для агента управления MIMMA;

-   полный импорт и синхронизация для агента управления ADMA_SCONTOSO_B2B;

-   полный импорт и синхронизация для агента управления B2B Graph;

-   экспорт, разностный импорт и синхронизация для агента управления ADMA_SCONTOSO_B2B;

-   экспорт, разностный импорт и синхронизация для агента управления MIMMA.

![](media/microsoft-identity-manager-2016-graph-b2b-scenario/506f0a093c8b58cbb62cc4341b251564.png)

## <a name="finally-application-proxy-with-b2b-guest-and-logging-into-mim"></a>Последний шаг: настройка прокси приложения для гостевого пользователя B2B и настройка входа в MIM

Итак, у нас готовы все правила синхронизации в MIM. Теперь определите в конфигурации прокси приложения принцип использования облака, чтобы разрешить KCD для прокси приложения.
Также вам нужно вручную добавить пользователя для управления пользователями и группами. В MIM добавлена возможность не отображать пользователей до их создания, что позволяет добавлять гостевого пользователя в офисную группу сразу после его подготовки. Но этот вариант требует более сложной настройки и не рассматривается в этом документе.

![](media/microsoft-identity-manager-2016-graph-b2b-scenario/d0f0b253dbbc5edaf22b22f30f94dd3b.png)

![](media/microsoft-identity-manager-2016-graph-b2b-scenario/a284e69bb14ca19217954881ba860cf2.png)

![](media/microsoft-identity-manager-2016-graph-b2b-scenario/0c2361d137f3efcad9139069c0abcb4d.png)

| **Только исходный поток** | **Использовать как проверку существования** | **Поток (значение FIM ⇒ атрибут назначения)**                          |
|-----------------------|---------------------------|-----------------------------------------------------------------------|
|                       |                           | [sAMAccountName⇒accountName](javascript:void(0);)                     |
|                       |                           | ["CONTOSO"⇒domain](javascript:void(0);)                            |
|                       |                           | [objectSid⇒objectSid](javascript:void(0);)                                      |

После подготовки всех элементов

Попробуйте войти от имени пользователя B2B и обратиться к нужному приложению

![](media/microsoft-identity-manager-2016-graph-b2b-scenario/275fc989d20d2598df55cde4b4524dca.png)

![](media/microsoft-identity-manager-2016-graph-b2b-scenario/e1a9d7b8c87021de4e43a3501826fa81.png)

<a name="next-steps"></a>Дальнейшие действия
----------

[Как подготовить пользователей в AD DS](https://technet.microsoft.com/library/ff686263(v=ws.10).aspx)

[Справочник по функциям для FIM 2010](https://technet.microsoft.com/library/ff800820(v=ws.10).aspx)

[Как обеспечить безопасный удаленный доступ к локальным приложениям](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-get-started)

[Страница для скачивания агента управления Microsoft Identity Manager для Microsoft Graph (предварительная версия)](http://go.microsoft.com/fwlink/?LinkId=717495)
