---
title: Настройка соединителя Microsoft Identity Manager для Microsoft Graph для B2B | Документы Майкрософт
author: billmath
description: Соединитель Microsoft Graph — это средство, которое позволяет управлять жизненным циклом учетных записей Active Directory для внешних пользователей. Мы рассмотрим сценарий, в котором организация пригласила гостей в каталог Azure AD и намерена предоставить им доступ к локальным приложениям, поддерживающим встроенную проверку подлинности Windows или Kerberos.
keywords: ''
ms.author: billmath
manager: mtillman
ms.date: 10/02/2018
ms.topic: article
ms.prod: microsoft-identity-manager
ms.assetid: 94a74f1c-2192-4748-9a25-62a526295338
ms.openlocfilehash: 139c58510117ad422529a4ff0facd23040023713
ms.sourcegitcommit: 7de35aaca3a21192e4696fdfd57d4dac2a7b9f90
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/16/2018
ms.locfileid: "49358777"
---
<a name="azure-ad-business-to-business-b2b-collaboration-with-microsoft-identity-managermim-2016-sp1-with-azure-application-proxy"></a>Совместная работа Azure Active Directory B2B с Microsoft Identity Manager (MIM) 2016 с пакетом обновления 1 (SP1) и Azure Active Directory Application Proxy
============================================================================================================================

Основной сценарий применения — управление жизненным циклом учетных записей Active Directory для внешних пользователей.   Мы рассмотрим сценарий, в котором организация пригласила гостей в каталог Azure AD и намерена предоставить им доступ к локальным приложениям, поддерживающим встроенную проверку подлинности Windows или Kerberos, используя [Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-publish) или другие шлюзовые механизмы. Для Azure AD Application Proxy требуется, чтобы каждый пользователь применял собственную учетную запись доменных служб Active Directory для идентификации и делегирования.

## <a name="scenario-specific-guidance"></a>Указания по сценарию

При настройке B2B с MIM и Azure AD Application Proxy предполагается следующее.

-   Вы уже развернули локальную среду Active Directory и установили Microsoft Identity Manager. Вы также настроили базовые конфигурации службы MIM, портала MIM, агента управления Active Directory (ADMA) и агента управления FIM (FIM MA).
    <https://docs.microsoft.com/microsoft-identity-manager/microsoft-identity-manager-deploy>

-   Вы уже выполнили инструкции в статье о скачивании и установке [соединителя Graph](microsoft-identity-manager-2016-connector-graph.md).

-   У вас настроено средство Azure AD Connect для синхронизации пользователей и групп с Azure AD.

-   У вас настроено средство Azure AD Connect с целью синхронизации Групп Office для управления приложением [с локальными доменными службами Active Directory](http://robsgroupsblog.com/blog/how-to-write-back-an-office-group-in-azure-active-directory-to-a-mail-enabled-security-group-in-an-on-premises-active-directory).

-   Вы уже настроили соединители прокси приложения и группы соединителей. Если это не так, воспользуйтесь [этими инструкциями](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-enable#install-and-register-a-connector) для их установки и настройки.

-   Вы уже опубликовали одно или несколько приложений, использующих встроенную проверку подлинности Windows или отдельные учетные записи AD через Azure AD App Proxy.

-   Вы пригласили или приглашаете одного или нескольких гостей, вследствие чего в Azure AD <https://docs.microsoft.com/azure/active-directory/active-directory-b2b-self-service-portal> создаются один или несколько пользователей.



## <a name="b2b-end-to-end-deployment-example-scenario"></a>Пример сценария комплексного развертывания B2B

Это руководство основано на описанном ниже сценарии.

Компания Contoso Pharmaceuticals сотрудничает с Trey Research Inc. в области исследований и разработок. Сотрудникам компании Trey Research нужен доступ к приложению для создания отчетов по исследованиям, которое предоставляет Contoso Pharmaceuticals.

-   Компания Contoso Pharmaceuticals использует собственный клиент и настроила в нем личный домен.

-   Кто-то пригласил внешнего пользователя в клиент Contoso Pharmaceuticals.
    Этот пользователь принял приглашение и теперь может обращаться к совместно используемым ресурсам.

-   Компания Contoso Pharmaceuticals опубликовала приложение посредством App Proxy. В этом случае примером приложения является портал MIM. Это дает возможность пользователю-гостю принимать участие в процессах MIM, например в сценариях службы технической поддержки, или запрашивать доступ к группам в MIM.


## <a name="configure-ad-and-azure-ad-connect-to-exclude-users-added-from-azure-ad"></a>Настройка Active Directory и Azure AD Connect для исключения пользователей, добавленных из Azure AD

По умолчанию средство Azure AD Connect предполагает, что пользователей без прав администратора в Active Directory необходимо синхронизировать с Azure AD.  Если средство Azure AD Connect находит в Azure AD пользователя, который соответствует пользователю в локальной среде Active Directory, оно сопоставляет эти две учетные записи, предполагает, что синхронизация пользователя была выполнена ранее, и делает локальную среду Active Directory заслуживающим доверия источником.  Однако такое поведение по умолчанию не подходит для процессов B2B, в рамках которых источником учетной записи пользователя является Azure AD. 

Поэтому пользователей, которые переносятся в доменные службы Active Directory диспетчером MIM из Azure AD, необходимо сохранять так, чтобы служба Azure AD не пыталась снова синхронизировать их.
Один из способов добиться этого — создать подразделение в доменных службах Active Directory и исключить его в Azure AD Connect.  

Дополнительные сведения см. в статье [Синхронизация Azure AD Connect: настройка фильтрации](https://docs.microsoft.com/en-us/azure/active-directory/connect/active-directory-aadconnectsync-configure-filtering). 
 

## <a name="create-the-azure-ad-application"></a>Создание приложения Azure AD 


Примечание. Прежде чем создавать агент управления синхронизацией MIM для соединителя Graph, ознакомьтесь с руководством по развертыванию [соединителя Graph](microsoft-identity-manager-2016-connector-graph.md) и создайте приложение с идентификатором клиента и секретом.
Убедитесь в том, что приложению предоставлено по крайней мере одно из следующих разрешений: `User.Read.All`, `User.ReadWrite.All`, `Directory.Read.All` или `Directory.ReadWrite.All`. 

## <a name="create-the-new-management-agent"></a>Создание агента управления


В пользовательском интерфейсе Synchronization Service Manager выберите **Соединители** и **Создать**.
Выберите **Graph (Microsoft)** и присвойте описательное имя.

![](media/microsoft-identity-manager-2016-graph-b2b-scenario/d95c6b2cc7951b607388cbd25920d7d0.png)

### <a name="connectivity"></a>Подключение

На странице "Подключение" необходимо указать версию API Graph. Готовая к использованию в рабочей среде версия — **1.0**; не предназначенная для рабочей среды версия — **бета-версия**.

![](media/microsoft-identity-manager-2016-graph-b2b-scenario/6fabfe20af0207f1556f0df18fd16f60.png)

### <a name="global-parameters"></a>Глобальные параметры

![](media/microsoft-identity-manager-2016-graph-b2b-scenario/84c4dd62f63b82239cd0cf63d14fc671.png)

### <a name="configure-provisioning-hierarchy"></a>Настройка иерархии подготовки

Эта страница используется для сопоставления компонента DN, например подразделения, c типом подготавливаемого объекта, например organizationalUnit. В данном сценарии этого не требуется, поэтому оставьте значение по умолчанию и нажмите кнопку "Далее".

![](media/microsoft-identity-manager-2016-graph-b2b-scenario/80016dc45b50a0b1b08ea51ad8b37977.png)

### <a name="configure-partitions-and-hierarchies"></a>Настройка разделов и иерархий

На странице разделов и иерархий выберите все пространства имен, которые содержат объекты для импорта и экспорта.

![](media/microsoft-identity-manager-2016-graph-b2b-scenario/72f0adc789ed78c66d066768146fb874.png)

#### <a name="select-object-types"></a>Выбор типов объектов

На странице "Типы объектов" выберите типы объектов для импорта. Необходимо выбрать по крайней мере тип "Пользователь".

![](media/microsoft-identity-manager-2016-graph-b2b-scenario/e18921f65a0d0e4acf0775c8a01ac009.png)

#### <a name="select-attributes"></a>Выбор атрибутов

На экране "Выбор атрибутов" выберите атрибуты Azure AD, которые будут необходимы для управления пользователями B2B в Active Directory. Атрибут ID является обязательным.  Атрибуты `userPrincipalName` и `userType` будут использоваться далее в этой конфигурации.  Остальные атрибуты являются необязательными, включая

-   `displayName`

-   `mail`

-   `givenName`

-   `surname`

-   `userPrincipalName`

-   `userType`

![](media/microsoft-identity-manager-2016-graph-b2b-scenario/58da80f5475cf01a97a6843dd279385c.png)

#### <a name="configure-anchors"></a>Настройка привязок

На странице "Настройка привязки" настройка атрибута привязки является обязательным шагом. По умолчанию для сопоставления пользователя используется атрибут ID.

![](media/microsoft-identity-manager-2016-graph-b2b-scenario/9377ab7b760221517a431384689c8c76.png)

#### <a name="configure-connector-filter"></a>Настройка фильтра соединителя

На странице настройки фильтра соединителя MIM позволяет отфильтровать объекты с помощью фильтра по атрибутам. В нашем сценарии работы с B2B нужно добавлять только тех пользователей, у которых атрибут `userType` имеет значение `Guest`, а не `member`.

![](media/microsoft-identity-manager-2016-graph-b2b-scenario/d90691fce652ba41c7a98c9a863ee710.png)

#### <a name="configure-join-and-projection-rules"></a>Настройка правил соединения и проекции

В этом руководстве предполагается, что вы создаете правило синхронизации.  Настройка правил соединения и проекции выполняется правилом синхронизации, а значит, вам не нужно определять соединения и проекции для самого соединителя. Сохраните значения по умолчанию и щелкните "ОК".

![](media/microsoft-identity-manager-2016-graph-b2b-scenario/34896440ae6ad404e824eb35d8629986.png)

#### <a name="configure-attribute-flow"></a>Настройка потока атрибута

В этом руководстве предполагается, что вы создаете правило синхронизации.  Проекция не требуется для определения потока атрибутов, так как он обрабатывается правилом синхронизации, которое мы создадим позднее. Сохраните значения по умолчанию и щелкните "ОК".

![](media/microsoft-identity-manager-2016-graph-b2b-scenario/b7cd0d294d4f361f0551bf2cb774d5f5.png)

#### <a name="configure-deprovision"></a>Настройка отзыва

Настройка отзыва позволяет настроить удаление объекта при синхронизации MIM, если удаляется объект метавселенной. В этом сценарии мы используем разъединители, так как нам нужно сохранить их в Azure AD. Кроме того, мы ничего не экспортируем в Azure AD, и соединитель настраивается только для импорта.

![](media/microsoft-identity-manager-2016-graph-b2b-scenario/2394ad4d11546c6a5c69a6dad56fe6ca.png)

#### <a name="configure-extensions"></a>Настройка расширений

Настройка расширений для этого агента управления возможна, но не является обязательной, так как мы используем правило синхронизации. Если бы ранее в потоке атрибутов мы выбрали расширенное правило, у нас появилась бы возможность определить расширение правила.

![](media/microsoft-identity-manager-2016-graph-b2b-scenario/74513d95b10f6ce47b7ac75fe7ab9889.png)

## <a name="extending-the-metaverse-schema"></a>Расширение схемы метавселенной


Прежде чем создавать правило синхронизации, нам нужно с помощью конструктора метавселенной создать атрибут userPrincipalName, связанный с объектом пользователя.

В клиенте синхронизации выберите конструктор метавселенной.

![](media/microsoft-identity-manager-2016-graph-b2b-scenario/db3c1d353168a09aaa68678d39ea4f09.png)

Теперь выберите тип объекта Person (Пользователь).

![](media/microsoft-identity-manager-2016-graph-b2b-scenario/b5e3db86398aed558a481dd64be4f5db.png)

В разделе "Действия" щелкните "Добавить атрибут".

![](media/microsoft-identity-manager-2016-graph-b2b-scenario/47d0056eb496edd2e7b5da11a2c04718.png)

Затем укажите следующие данные.

Имя атрибута: **userPrincipalName**.

Тип атрибута: **String (Indexable)** (Строковый, индексируемый).

Indexed (Индексированный) = **True** (Да).

![](media/microsoft-identity-manager-2016-graph-b2b-scenario/9fba1ff9feefb17b82478ac7010edbfa.png)

## <a name="creating-mim-service-synchronization-rules"></a>Создание правил синхронизации для службы MIM

На следующих шагах мы начнем сопоставлять гостевую учетную запись B2B с потоком атрибутов. Также здесь предполагается, что вы уже настроили агент управления Active Directory и передачу пользователей агентом FIM MA в службу и на портал MIM.

![](media/microsoft-identity-manager-2016-graph-b2b-scenario/e389ee78beac3bf469ddd97bddb5e9d5.png)

Для следующих шагов необходимо добавить минимальную конфигурацию FIM MA и ADMA.

Дополнительные сведения об этой настройке можно найти в статье <https://technet.microsoft.com/library/ff686263(v=ws.10).aspx> — How Do I Provision Users to AD DS (Как подготовить пользователей для AD DS).

### <a name="synchronization-rule-import-guest-user-to-mv-to-synchronization-service-metaverse-from-azure-active-directorybr"></a>Правило синхронизации. Импорт гостевого пользователя в MV и метавселенную службы синхронизации из Azure Active Directory<br>

Перейдите на портал MIM, выберите "Правила синхронизации" и щелкните "Создать".  Создайте правило синхронизации входящего трафика для процесса B2B посредством соединителя Graph.
![](media/microsoft-identity-manager-2016-graph-b2b-scenario/ba39855f54268aa824cd8d484bae83cf.png)

![](media/microsoft-identity-manager-2016-graph-b2b-scenario/de059b93474c39763f0b27874b716e15.png)

На этапе "Критерии связи" выберите "Создать ресурс в FIM".
![](media/microsoft-identity-manager-2016-graph-b2b-scenario/9bc4a92136be1557d3596fa2eaa63e61.png)

![](media/microsoft-identity-manager-2016-graph-b2b-scenario/0ac7f4d0fd55f4bffd9e6508b494aa74.png)

Настройте указанные ниже правила потока атрибутов для входящего трафика.  Обязательно задайте атрибуты `accountName`, `userPrincipalName` и `uid`, так как они будут использоваться позднее в этом сценарии.

| **Только исходный поток** | **Использовать как проверку существования** | **Поток (Исходное значение ⇒ Атрибут FIM)**                          |
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

Это правило синхронизации создает пользователя в Active Directory.  Поток для `dn` должен помещать пользователя в подразделение, которое было исключено из Azure AD Connect.  Кроме того, измените поток для `unicodePwd` в соответствии с политикой паролей Active Directory — пользователю не потребуется знать пароль.  Обратите внимание на то, что в значении `262656` для `userAccountControl` закодированы флаги `SMARTCARD_REQUIRED` и `NORMAL_ACCOUNT`.

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
| **Y**                 |                           | ["CN="+uid+",OU=B2BGuest,DC=contoso,DC=com"⇒dn](javascript:void(0);) |
| **Y**                 |                           | [RandomNum(0,999)+userPrincipalName⇒unicodePwd](javascript:void(0);)  |
| **Y**                 |                           | [262656⇒userAccountControl](javascript:void(0);)                      |

### <a name="optional-synchronization-rule-import-b2b-guest-user-objects-sid-to-allow-for-login-to-mim"></a>Необязательное правило синхронизации. Импорт идентификатора безопасности из объектов гостевых пользователей B2B для поддержки входа в MIM 

Это правило синхронизации входящего трафика передает атрибут идентификатора безопасности пользователя из Active Directory обратно в MIM, чтобы пользователь мог получать доступ к порталу MIM.  Портал MIM требует, чтобы в базе данных службы MIM были заполнены атрибуты пользователя `samAccountName`, `domain` и `objectSid`.

Настройте `ADMA` в качестве исходной внешней системы, так как Active Directory будет автоматически задавать атрибут `objectSid` при создании пользователя диспетчером MIM.
 
Обратите внимание на то, что, если вы настраиваете создание пользователей в службе MIM, они не должны входить в наборы, предназначенные для правил политики управления самостоятельным сбросом паролей сотрудниками.  Вам может потребоваться изменить настроенные определения, исключив пользователей, созданных потоком B2B. 

![](media/microsoft-identity-manager-2016-graph-b2b-scenario/263df23fd588c4229b958aee240071f3.png)


![](media/microsoft-identity-manager-2016-graph-b2b-scenario/047ebc3084999246bdd44b1f05ca02b3.png)

![](media/microsoft-identity-manager-2016-graph-b2b-scenario/acc0a871c0bf6f45ee928bed5abd9861.png)

![](media/microsoft-identity-manager-2016-graph-b2b-scenario/80fb9d563ec088925477a645f19b0373.png)


| **Только исходный поток** | **Использовать как проверку существования** | **Поток (Исходное значение ⇒ Атрибут FIM)**                          |
|-----------------------|---------------------------|-----------------------------------------------------------------------|
|                       |                           | [sAMAccountName⇒accountName](javascript:void(0);)                     |
|                       |                           | ["CONTOSO"⇒domain](javascript:void(0);)                            |
|                       |                           | [objectSid⇒objectSid](javascript:void(0);)                                      |


## <a name="run-the-synchronization-rules"></a>Выполнение правил синхронизации

Далее нам нужно пригласить пользователя и выполнить правила синхронизации агента управления в следующем порядке:

-   полный импорт и синхронизация для агента управления `MIMMA`;  таким образом обеспечивается настройка актуальных правил синхронизации для синхронизации MIM;

-   полный импорт и синхронизация для агента управления `ADMA`;  таким образом обеспечивается согласованность MIM и Active Directory;  на этом этапе еще нет ожидающих выполнения операций экспорта для гостей;

-   полный импорт и синхронизация для агента управления B2B Graph;  в результате пользователи-гости передаются в метавселенную;  на этом этапе ожидается экспорт одной или нескольких учетных записей для `ADMA`;  если ожидающих выполнения операций экспорта нет, проверьте, были ли пользователи-гости импортированы в пространство соединителя и были ли настроены правила для назначения им учетных записей в Active Directory;

-   экспорт, разностный импорт и синхронизация для агента управления `ADMA`;  если операции экспорта выполнить не удалось, проверьте конфигурацию правил и определите, выполнены ли все требования к схеме; 

-   экспорт, разностный импорт и синхронизация для агента управления `MIMMA`;  по завершении этого этапа ожидающих выполнения операций экспорта оставаться не должно.

![](media/microsoft-identity-manager-2016-graph-b2b-scenario/506f0a093c8b58cbb62cc4341b251564.png)


## <a name="optional-application-proxy-for-b2b-guests-logging-into-mim-portal"></a>Необязательный шаг. Настройка Application Proxy для входа пользователей-гостей B2B на портал MIM

Итак, у нас готовы все правила синхронизации в MIM. Теперь определите в конфигурации Application Proxy принцип использования облака, чтобы разрешить KCD для Application Proxy.
Также вам нужно вручную добавить пользователя для управления пользователями и группами. В MIM добавлена возможность не отображать пользователей до их создания, что позволяет добавлять гостевого пользователя в офисную группу сразу после его подготовки. Но этот вариант требует более сложной настройки и не рассматривается в этом документе.

![](media/microsoft-identity-manager-2016-graph-b2b-scenario/d0f0b253dbbc5edaf22b22f30f94dd3b.png)

![](media/microsoft-identity-manager-2016-graph-b2b-scenario/a284e69bb14ca19217954881ba860cf2.png)

![](media/microsoft-identity-manager-2016-graph-b2b-scenario/0c2361d137f3efcad9139069c0abcb4d.png)


Завершив настройку, попробуйте войти от имени пользователя B2B и обратиться к нужному приложению.

![](media/microsoft-identity-manager-2016-graph-b2b-scenario/275fc989d20d2598df55cde4b4524dca.png)

![](media/microsoft-identity-manager-2016-graph-b2b-scenario/e1a9d7b8c87021de4e43a3501826fa81.png)

<a name="next-steps"></a>Дальнейшие действия
----------

[Как подготовить пользователей в AD DS](https://technet.microsoft.com/library/ff686263(v=ws.10).aspx)

[Справочник по функциям для FIM 2010](https://technet.microsoft.com/library/ff800820(v=ws.10).aspx)

[Как обеспечить безопасный удаленный доступ к локальным приложениям](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-get-started)

[Страница для скачивания соединителя Microsoft Identity Manager для Microsoft Graph](http://go.microsoft.com/fwlink/?LinkId=717495)
