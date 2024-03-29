---
title: Руководство по основным понятиям Microsoft BHOLD Suite | Microsoft Docs
description: Начните работу с компонентами MIM 2016, установив и настроив службу синхронизации.
keywords: ''
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 09/14/2017
ms.assetid: ''
ms.prod: microsoft-identity-manager
ms.openlocfilehash: 32bd77140cf70047eaa02d363a1348e73783f87a
ms.sourcegitcommit: 7de35aaca3a21192e4696fdfd57d4dac2a7b9f90
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/16/2018
ms.locfileid: "49358845"
---
# <a name="microsoft-bhold-suite-concepts-guide"></a>Руководство по основным понятиям Microsoft BHOLD Suite

Microsoft Identity Manager 2016 (MIM) позволяет организациям управлять всем жизненным циклом удостоверений пользователей и связанных учетных данных. Этот компонент можно настроить для синхронизации удостоверений, централизованного управления сертификатами и паролями и подготовки пользователей в разнородных системах. С помощью MIM ИТ-отделы могут определять и автоматизировать процессы, используемые для управления удостоверениями, начиная от создания и заканчивая списанием.

Microsoft BHOLD Suite расширяет эти возможности MIM благодаря добавлению управления доступом на основе ролей. BHOLD позволяет организациям определять роли пользователей и управлять доступом к конфиденциальным данным и приложениям. Доступ определяется разрешениями, подходящими для этих ролей. BHOLD Suite включает службы и инструменты, упрощающие моделирование связей ролей в организации. BHOLD сопоставляет роли с правами, проверяя правильность применения определений ролей и связанных прав к пользователям. Эти возможности полностью интегрированы с MIM, что обеспечивает удобство работы конечных пользователей и ИТ-специалистов.

Это руководство поможет вам понять принципы взаимодействия BHOLD Suite с MIM. В нем рассматриваются следующие темы:

- контроль доступа на основе ролей;
- Аттестация
- Аналитика
- Отчеты
- Соединитель управления доступом
- Интеграция с MIM

## <a name="role-based-access-control"></a>контроль доступа на основе ролей;

Наиболее распространенный способ управления доступом пользователей к данным и приложениям — управление доступом на уровне пользователей (DAC). В наиболее распространенных реализациях каждый значимый объект имеет идентифицированного владельца. Владелец может предоставлять или блокировать доступ к объекту для других пользователей, как на индивидуальном уровне, так и в зависимости от членства в группе. На практике реализация DAC обычно приводит к созданию множества групп безопасности: одни из них отражают организационную структуру, другие представляют собой функциональные группы (например, по типам должности или назначениям проекта), третьи основаны на временных коллекциях пользователей и устройств. По мере роста организации управлять членством в этих группах становится все сложнее. Например, если сотрудник переходит из одного проекта в другой, группы, которые используются для управления доступом к ресурсам проектов, приходится изменять вручную. В таких случаях часто возникают ошибки, которые могут отрицательно сказаться на безопасности проекта или производительности труда.

MIM включает функции, которые помогают устранить эту проблему, предоставляя возможности автоматического управления группами и членством в группах рассылки. Но эти функции не позволяют устранить изначальные сложности, связанные с растущим числом группы, связь которых друг с другом необязательно имеет структурированный характер.

Одним из способов значительно сократить рост групп является развертывание управления доступом на основе ролей (RBAC). Компонент RBAC не заменяет функции DAC.  Функции RBAC основаны на управлении доступом на уровне пользователей и обеспечивают инфраструктуру для классификации пользователей и ИТ-ресурсов. Это позволяет явно объявить связи между ними и соответствующие права доступа согласно такой классификации. Например, назначив пользователю атрибуты, определяющие должность и назначения проекта, ему можно предоставить доступ к инструментам, необходимым для его работы, и данным, которые потребуются для участия в конкретном проекте. Когда пользователь получает другую должность и назначения проекта, изменение атрибутов, определяющих должность и проекты пользователя, автоматически блокирует его доступ к ресурсам, которые требовались только для выполнения предыдущих обязанностей пользователя.

Так как одни роли могут содержаться в других ролях в иерархии (например, роли менеджера продаж и торгового представителя могут содержаться в более общей роли "Продажи"), назначение соответствующих прав конкретным ролям упрощается, обеспечивая при этом необходимые права всем пользователям, роли которых входят в роль более высокого уровня. Например, в больнице всему медицинскому персоналу может быть предоставлено право на просмотр записей пациентов, но только врачам (подроль роли "Медицинский персонал") могут быть предоставлены права на создание рецептов для пациентов. Аналогичным образом пользователям, принадлежащим к роли "Администрация", может быть запрещен доступ к записям пациентов, за исключением сотрудников, выставляющих счета (подроль роли "Администрация"), которым можно предоставить доступ к тем частям записей пациентов, которые требуются для выставления счетов за услуги, предоставляемые медицинским учреждением.

Дополнительным преимуществом RBAC является возможность определять и применять разделение обязанностей. Это позволяет организациям задавать комбинации ролей, предоставляющих разрешения, которые не должны принадлежать одному пользователю, чтобы этому пользователю нельзя было назначить роли, позволяющие ему, например, инициировать платеж и авторизовать его. RBAC предоставляет возможность автоматически применять такие политики, вместо того чтобы оценивать эффективную реализацию политики для каждого отдельного пользователя.

### <a name="bhold-role-model-objects"></a>Объекты модели ролей BHOLD

Используя BHOLD Suite, можно указать и организовать роли в организации, сопоставить пользователей и роли, а также сопоставить соответствующие разрешения для ролей. Эта структура называется моделью ролей и содержит и объединяет пять типов объектов. 

- Подразделения
- Users
- Роли
- Разрешения
- Приложения

#### <a name="organizational-units"></a>Подразделения

Подразделения — это основные средства, с помощью которых пользователи организуются в модели ролей BHOLD. Каждый пользователь должен принадлежать по крайней мере одному подразделению. (Фактически, когда пользователя удаляют из последнего подразделения в BHOLD, запись данных этого пользователя удаляется из базы данных BHOLD.)

> [!Important]
> Подразделения в модели ролей BHOLD не следует путать с подразделениями в доменных службах Active Directory (AD DS). Как правило, структура подразделений в BHOLD зависит от организации и политик компании, а не от требований сетевой инфраструктуры.

Несмотря на то, что это необязательно, в большинстве случаев структура подразделения в BHOLD представляет иерархическую структуру фактической организации, аналогично приведенной ниже.

![](media/bhold-concepts-guide/org-chart.png)

В этом примере модель ролей будет представлять подразделение organizationalganizatinal для организации в целом (представленную президентом, так как президент не является частью подразделения mororganizationalganizatinal), кроме того, для этих целей может использоваться корневое подразделение BHOLD (которое всегда существует). Подразделения, представляющие отделы компании, возглавляемые вице-президентами, будут объединены в подразделение corporate. Далее, подразделения, соответствующие директорам по продажам и маркетингу, будут добавлены в подразделения маркетинга (marketing) и продаж (sales), а подразделения, представляющие региональных руководителей отделов продаж, будут добавлены в подразделение для руководителя отдела продаж в регионе "восток" (east). Продавцы-консультанты, которые не управляют другими пользователями, станут членами подразделения руководителя отдела продаж в регионе "восток". Обратите внимание, что пользователи могут быть членами подразделения на любом уровне. Например, помощник администратора, который не является руководителем и подчиняется непосредственно вице-президенту, будет членом подразделения вице-президента.

Помимо представления организационной структуры, подразделения можно использовать для группирования пользователей и других подразделений согласно функциональным критериям, таким как проекты или специализация. На следующей схеме показано, каким образом подразделения можно использовать для группирования продавцов-консультантов в зависимости от типа клиента.

![](media/bhold-concepts-guide/org-chart-02.png)

В этом примере каждый продавец-консультант принадлежит двум подразделениям: одно представляет положение сотрудника в структуре управления организации, а второе — клиентскую базу сотрудника (розничные и корпоративные клиенты). Каждому подразделению можно назначить разные роли, которым, в свою очередь, можно назначить разные разрешения для доступа к ИТ-ресурсам организации. Кроме того, роли могут наследоваться от родительских подразделений, что упрощает процесс назначения ролей пользователям. С другой стороны, наследование конкретных ролей можно запретить, чтобы гарантировать, что конкретная роль будет связана только с соответствующими подразделениями.

Подразделения могут создаваться в BHOLD Suite с помощью веб-портала BHOLD Core или с помощью генератора моделей BHOLD.

#### <a name="users"></a>Users

Как упоминалось выше, каждый пользователь должен принадлежать по крайней мере одному подразделению. Так как подразделения представляют собой основной механизм связывания пользователей с ролями, в большинстве организаций данный конкретный пользователь принадлежит нескольким подразделениям, что упрощает связывание ролей с этим пользователем. В некоторых случаях, тем не менее, может потребоваться связать роль с пользователем, за пределами любого подразделения, к которому принадлежит пользователь. Следовательно, пользователю можно назначить роль напрямую в дополнение к ролям, получаемым из подразделения, к которому этот пользователь принадлежит.

Когда пользователь неактивен в организации (например, находится на больничном), назначения пользователя могут быть приостановлены, то есть, все разрешения пользователя будут отозваны без необходимости удалять пользователя из модели ролей. Когда пользователь вернется к своим обязанностям, его назначения будут повторно активированы, а все разрешения, предоставленные этой роли пользователя, — восстановлены.

Объекты для пользователей в BHOLD можно создавать по отдельности на веб-портале BHOLD Core. Кроме того, их можно импортировать в пакетном режиме, используя генератор моделей BHOLD или соединитель управления доступом в службе синхронизации FIM для импорта сведений о пользователях из таких источников, как доменные службы Active Directory или приложение для работы с кадрами.

Пользователей можно создавать напрямую в BHOLD, не используя службу синхронизации FIM. Это может быть удобно при моделировании ролей в подготовительной или тестовой среде. Можно также разрешить назначение ролей внешним пользователям (например, сотрудникам субподрядчика) и, таким образом, предоставить им доступ к ИТ-ресурсами без добавления в базу данных сотрудников. При этом такие пользователи не смогут использовать возможности самообслуживания BHOLD.

#### <a name="roles"></a>Роли

Как было отмечено выше, в рамках модели управления доступом на основе ролей (RBAC) разрешения связаны с ролями, а не с отдельными пользователями. Это дает возможность предоставить каждому пользователю разрешения, необходимые для выполнения обязанностей пользователя путем изменения роли пользователя, а не предоставления или отзыва его отдельных разрешений. Как следствие, назначение разрешений больше не требует участия ИТ-отдела и может осуществляться в процессе управления компанией. Роли могут объединять разрешения для доступа к разным системам, напрямую или с помощью подролей, что дополнительно сокращает участие ИТ-отдела в управлении разрешениями пользователей.

Важно отметить, что роли являются компонентом собственно модели RBAC; как правило, роли не подготавливаются для целевых приложений. Это позволяет использовать RBAC наряду с существующими приложениями (которые не поддерживают использование ролей или изменение определений ролей), позволяя решать требования меняющихся бизнес-моделей без необходимости изменять сами приложения. Если целевое приложение поддерживает использование ролей, роли в модели BHOLD можно связать с соответствующими ролями приложения, обрабатывая роли приложения как разрешения.

В BHOLD можно назначить роль пользователю с помощью двух механизмов:

- путем назначения роли подразделению, членом которого является пользователь;
- путем назначения роли пользователю напрямую.

Роль, назначенная родительскому подразделению, при необходимости может наследоваться дочерними подразделениями. Если роль назначена подразделению или унаследована им, она называется действующей или предлагаемой ролью. Если это действующая роль, она назначается всем пользователям в подразделении. Если это предлагаемая роль, ее необходимо активировать для каждого пользователя или члена подразделения, чтобы она стала действующей для такого пользователя или членов подразделения. Это дает возможность назначить пользователям набор ролей, связанных с подразделением, вместо автоматического назначения всех ролей подразделения всем его членам. Кроме того, для ролей можно задать начальную и конечную даты и ограничить долю пользователей в подразделении, для которых эта роль может быть действующей.

Схема ниже иллюстрирует назначение роли отдельному пользователю в BHOLD.

![](media/bhold-concepts-guide/org-chart-flow.png)

На этой схеме роль A назначается подразделению как наследуемая роль и поэтому наследуется дочерними подразделениями и всеми пользователями внутри этих подразделений. Роль B назначается как предлагаемая роль для подразделения. Ее необходимо активировать, прежде чем пользователям в подразделении можно будет предоставить разрешения этой роли. Роль C — это действующая роль, поэтому ее разрешения немедленно применяются ко всем пользователям в подразделении. Роль D связана непосредственно с пользователем, и поэтому ее разрешения применяются немедленно для этого пользователя.

Кроме того, роль можно активировать для пользователя на основе атрибутов пользователя. Дополнительные сведения см. в разделе "Авторизация на основе атрибутов".

#### <a name="permissions"></a>Разрешения

Разрешение в BHOLD соответствует авторизации, импортированной из целевого приложения. Таким образом, когда система BHOLD настроена для работы с приложением, она получает список авторизаций, которые можно связать с ролями. Например, при добавлении доменных служб Active Directory (AD DS) в BHOLD в качестве приложения, система получает список групп безопасности, которые, как назначения BHOLD, могут быть связаны с ролями в BHOLD.

Разрешения определяются приложениями. BHOLD обеспечивает единое унифицированное представление разрешений, что позволяет связывать разрешения с ролями, не требуя от диспетчеров ролей понимания деталей реализации разрешений. На практике разные системы могут применять разрешения по-разному. Соединитель конкретного приложения (из службы синхронизации FIM в приложение) определяет, каким образом изменения разрешений для конкретного пользователя предоставляются этому приложению. 

#### <a name="applications"></a>Приложения

BHOLD реализует метод применения управления доступом на основе ролей (RBAC) для внешних приложений. То есть, при добавлении в систему BHOLD пользователей и разрешений из приложения BHOLD может связать эти разрешения с пользователями, назначив пользователям роли, а затем связав с ролями разрешения. Фоновый процесс приложения может затем сопоставить правильные разрешения с пользователями, основываясь на сопоставлении ролей и разрешений в BHOLD.

### <a name="developing-the-bhold-suite-role-model"></a>Разработка модели ролей BHOLD Suite

Чтобы помочь вам в разработке модели ролей, BHOLD Suite включает генератор модели — инструмент, который удобен и прост в использовании.

Прежде чем использовать генератор моделей, необходимо создать ряд файлов, которые определяют объекты, используемые генератором моделей для построения модели ролей. Сведения о создании этих файлов см. в техническом справочнике Microsoft BHOLD Suite.

Первым этапом работы с генератором моделей BHOLD является импорт этих файлов для загрузки базовых стандартных блоков в генератор моделей. После успешной загрузки файлов можно указать критерии, которые генератор моделей будет использовать для создания нескольких классов ролей:

- роли с членством, назначаемые пользователю в зависимости от подразделений, к которым он принадлежит;
- роли с атрибутами, назначаемые пользователю на основе атрибутов пользователя в базе данных BHOLD;
- предлагаемые роли, связанные с подразделением, которые, тем не менее, должны быть активированы для конкретного пользователя;
- роли с владением, предоставляющие пользователю контроль над подразделениями и ролями, для которых владелец не указан в импортированных файлах.

> [!Important]
> При отправке файлов установите флажок **Сохранить существующую модель** только в тестовых средах. В рабочих средах необходимо использовать генератор моделей для создания первоначальной модели ролей. Его нельзя использовать для изменения существующей модели ролей в базе данных BHOLD.

Когда генератор модели создаст роли в модели ролей, вы можете экспортировать модель ролей в базу данных BHOLD в виде XML-файла.

### <a name="advanced-bhold-features"></a>Дополнительные возможности BHOLD

В предыдущих разделах описаны основные компоненты управления доступом на основе ролей (RBAC) в BHOLD. В этом разделе рассматриваются дополнительные возможности в BHOLD, обеспечивающие дополнительную защиту и гибкость для реализации RBAC в вашей организации. В этом разделе приводится обзор следующих функций BHOLD.

- Кратность
- Разделение обязанностей
- Адаптируемые к контексту разрешения
- Авторизация на основе атрибутов
- Гибкие типы атрибутов


#### <a name="cardinality"></a>Кратность

*Кратность* относится к реализации бизнес-правил, позволяющих ограничить число событий связывания двух объектов друг с другом. Что касается BHOLD, правила кратности можно установить для ролей, пользователей и разрешений.

Для ролей можно настроить следующие ограничения:

- максимальное число пользователей, для которых может быть активирована предлагаемая роль;
- максимальное число подролей, которые могут быть связаны с ролью;
- максимальное число разрешений, которые могут быть связаны с ролью.

Для разрешений можно настроить следующие ограничения:

- максимальное число ролей, которые могут быть связаны с разрешением;
- максимальное число пользователей, которым может быть предоставлено разрешение.

Для пользователей можно настроить следующие ограничения:

- максимальное число ролей, которые могут быть связаны с пользователем;
- максимальное число разрешений, которые могут быть назначены пользователю с помощью назначений ролей.

#### <a name="separation-of-duties"></a>Разделение обязанностей

Разделения обязанностей (SoD) — это деловой принцип, который позволяет предотвратить получение одним лицом возможности выполнять действия, которые не должны быть доступны для одного лица. Например, один сотрудник не должен иметь возможность запросить платеж и авторизовать его. Принцип разделения обязанностей позволяет организациям реализовать систему проверок и противовесов, чтобы свести к минимуму риск ошибок или злоумышленных действий сотрудников.

В BHOLD принцип разделения обязанностей реализуется путем определения несовместимых разрешений. При определении таких разрешений система BHOLD применяет принцип разделения обязанностей, блокируя создание ролей, связанных с несовместимыми разрешениями (напрямую или через наследование), и запрещая назначать пользователям несколько ролей, которые, в случае объединения, могут предоставить несовместимые разрешения (также напрямую или через наследование). При необходимости конфликты можно переопределять.

#### <a name="context-adaptable-permissions"></a>Адаптируемые к контексту разрешения

Создание разрешений, которые можно автоматически изменять на основе атрибутов объекта, позволяет сократить общее количество разрешений, которыми необходимо управлять. Адаптируемые к контексту разрешения (CAP) позволяют определить формулу как атрибут разрешения, который изменяет порядок применения разрешения приложением, связанным с разрешением. Например, можно создать формулу, которая изменяет разрешение на доступ к папке (с помощью группы безопасности, связанной со списком управления доступом этой папки) в зависимости от того, принадлежит ли пользователь подразделению, содержащему сотрудников с полной или частичной занятостью. Если пользователь перемещается из одного подразделения в другое, новое разрешение применяется автоматически, а старое — отключается. 

Формула адаптируемых к контексту разрешений может запрашивать значения атрибутов, которые были применены к приложениям, разрешениям, подразделениям и пользователям.

#### <a name="attribute-based-authorization"></a>Авторизация на основе атрибутов

Один из способов контроля того, что роль, связанная с подразделением, активируется для определенного пользователя в подразделении, — использование авторизации на основе атрибутов. С помощью авторизации на основе атрибутов можно автоматически активировать роль только в случае выполнения определенных правил на основе атрибутов пользователя. Например, можно связать роль с подразделением, активируя ее для пользователя только в том случае, если название должности пользователя соответствует должности в правиле авторизации на основе атрибутов. Это избавляет от необходимости вручную активировать предлагаемую роль для пользователя. Вместо этого можно активировать роль для всех пользователей в подразделении, значение атрибута которых соответствует правилу авторизации на основе атрибутов. Правила можно объединять, чтобы роль активировалась только в том случае, если атрибуты пользователя удовлетворяют всем правилам авторизации, указанным для этой роли.

Важно отметить, что результаты проверок правил авторизации ограничиваются параметрами кратности. Например, если параметр кратности правила указывает, что роль можно назначить максимум двум пользователям, а правила авторизации предполагают активацию роли для четырех пользователей, роль будет активирована только для первых двух пользователей, которые прошли проверку авторизации на основе атрибутов.

#### <a name="flexible-attribute-types"></a>Гибкие типы атрибутов

Система атрибутов в BHOLD поддерживает расширение. Можно определить новые типы атрибутов для таких объектов, как пользователи, подразделения и роли. Атрибутам можно задавать значения, которые являются целыми числами, логическими значениями (да/нет), буквами и цифрами, датами, временем и адресами электронной почты. Атрибуты могут быть заданы как одиночные значения или списки значений.

## <a name="attestation"></a>Аттестация

BHOLD Suite включает средства, которые можно использовать для проверки того, что отдельным пользователям предоставлены соответствующие разрешения для выполнения их рабочих задач. Администратор может использовать портал, предоставляемый модулем аттестации BHOLD, для разработки процесса аттестации и управления им.

Процесс аттестации осуществляется с помощью кампаний, в рамках которых администраторам кампании предоставляется возможность и средства для проверки наличия у вверенных им пользователей доступа к управляемым приложениями BHOLD и соответствующих разрешений в этих приложениях. В системе назначается владелец кампании, который отвечает за кампанию и ее должное выполнение. Кампанию можно создать для однократного или регулярного выполнения.

Как правило, администратором кампании назначается руководитель, который подтверждает права доступа пользователей, принадлежащих к одному подразделению или нескольким, за которые он отвечает. Администраторы могут автоматически выбираться для пользователей, подтвержденных в кампании на основе атрибутов пользователя, кроме того, их можно определить, указав в файле, в котором каждый пользователь, подтвержденный в кампании, сопоставляется с администратором.

Когда кампания начинается, система BHOLD отправляет по электронной почте уведомление администраторам и владельцу кампании, а затем отправляет периодические напоминания, помогая отслеживать ход выполнения кампании. Администраторы направляются на портал кампании, где они могут просмотреть список пользователей, за которых они отвечают, и роли, назначенные этим пользователям. Затем администраторы могут проверить, отвечают ли они за всех пользователей в списке, и утвердить или отозвать права доступа для всех таких пользователей.

Владельцы кампании также используют портал для отслеживания хода выполнения кампании, а мероприятия в ее рамках регистрируются в журнале, чтобы владельцы кампании могли проанализировать их.

## <a name="analytics"></a>Аналитика

Одним из наиболее важных аспектов при внедрении системы управления доступом на основе ролей (RBAC) является баланс, позволяющий обеспечить должный уровень контроля и не возводить ненужные (и даже нежелательные) ограничения. Попытки поддержать такой баланс часто приводят к формированию структуры управления доступом, которая настолько сложна, что непредвиденные взаимодействия между правилами почти неизбежны.

Именно поэтому важно иметь возможность анализировать влияние политик управления доступом, прежде чем они будут фактически развернуты. Модуль аналитики BHOLD Suite дает вам возможность выполнить такой анализ, позволяя разработать правила, отражающие нужные политики, а затем вывести список пользователей, разрешения которых соответствуют правилу или конфликтуют с ним. По результатам анализа можно настроить политику или изменить роли и разрешения для устранения конфликтов с политикой.

На портале аналитики BHOLD можно создавать наборы правил, которые состоят из одного правила или нескольких, создаваемых для тестирования конкретной политики или группы политик. Правило состоит из следующих основных компонентов:

- название и описание, которые позволяют определить правило;
- состояние, которое указывает, готово ли правило к проверке, проходит ли оно проверку или утверждено;
- набор элементов (например, пользователей или разрешений), для проверки которых предназначено это правило;
- дополнительные фильтры набора, являющиеся выражениями, которые можно использовать для выбора соответствующей подгруппы проверяемого элемента;
- один фильтр правил или несколько, являющиеся выражениями, представляющими тестируемую политику.

Правило можно проверять один из следующих наборов элементов.

- Users
- Подразделения
- Роли
- Разрешения
- Приложения
- Учетные записи

На следующей схеме показано простое правило, состоящее из двух правил наборов и двух правил фильтра.

![](media/bhold-concepts-guide/rules.png)

Обратите внимание на разницу в неуспешном применении фильтра набора и фильтра правила: если не пройден фильтр набора, объект элемента удаляется из тестирования последующими фильтрами, но если не пройден фильтр правила, объект объявляется несоответствующим. Только те объекты, которые прошли все фильтры наборов и правил, считаются соответствующими.

Каждый фильтр состоит из типа, оператора (который зависит от типа), ключа (один из элементов) и значения, по которому ключ проверяется с помощью оператора. Например, следующий фильтр проверяет, превышает ли число пользователей в наборе элементов значение "10":


|   |   |   |   |   |
|---|---|---|---|---|
|**Тип:**   | Количество   |
| **Ключ:**  | Users  |
| **Оператор**  | >  |
| **Значение:** | 10 |

Фильтры правил делятся на три типа и используют операторы, характерные для данного типа, как указано.

- Атрибут
  - < и >
  - = и !=
  - **содержит**
  - **не содержит**
- Количество
  - < и >
  - = и !=
- Ограничение
  - **Должен иметь любые и все**
  - **Может иметь любые и не может иметь все**
  - **Может иметь только любые и может иметь только все**
  - **Исключительно имеет любые и исключительно имеет все**

> [!Note]
> Ограничительные фильтры могут использовать указанные операторы для проверки ключей по набору нескольких значений.

Например, если вы хотите проверить реализацию политики разделения обязанностей, в которой задано, что пользователь с разрешением на запрос платежа не может иметь разрешение на утверждение платежа, необходимо создать правило следующим образом.

|   |  |
|---|--|
|Имя.| Проверка разделения обязанностей при платеже|
|Элемент:| Users|
|Фильтр набора:| имеет любое разрешение на запрос платежа|
|Фильтр правила: | не может иметь любое разрешение на утверждение платежа|

При запуске этого правила модуль аналитики BHOLD отображает количество пользователей в выбранном наборе (пользователи с разрешением на запрос платежа), количество пользователей, соответствующих правилу, и количество пользователей, которые не соответствуют правилу. Затем можно вывести на экран несоответствующих пользователей, чтобы исправить несоответствие.

Помимо отображения результатов, можно также сохранить отчет как CSV- или XML-файл для последующего анализа результатов. Кроме того, можно настроить результирующий отчет для отображения дополнительных сведений, которые помогут лучше понять влияние политики. Например, при тестировании пользователей можно вывести на экран (или добавить в отчет) учетные записи соответствующих и несоответствующих пользователей, чтобы определить приложения, которые затрагивает политика.

Так как правило может содержать несколько фильтров, можно подключить фильтры для проверки существования определенного сочетания условий. По умолчанию результат представляет собой результат логического теста И всех фильтров, но можно задать выполнение теста ИЛИ для комбинации фильтров.

Например, если политика требует, чтобы руководителям назначалось разрешение на изменение платежа или утверждение платежа, можно проверить соответствие этой политике, создав следующее правило.


|  |  |
|--|--|
|Имя. | Проверка разделения обязанностей "Изменение платежа"|
|Элемент: | Users |
|Фильтр набора: | руководитель с любой ролью|
| Фильтры правила: |должен иметь любое разрешение на изменение платежа </br> должен иметь любое разрешение на утверждение платежа|

По умолчанию любой пользователь, который является руководителем с разрешением на изменение и разрешением на утверждение платежа будет считаться соответствующими. Но политика требует, чтобы у руководителя было одно из разрешений, но не обязательно оба. Чтобы проверить фактическое соответствие политике, необходимо использовать логический оператор ИЛИ с правилом, чтобы определить наличие руководителей, у которых нет разрешения на изменение платежа и разрешения на утверждение платежа.

В отличие от других операторов, операторы **Исключительно имеет любые** и **Исключительно имеет все** означают соответствие для объектов, которые в противном случае были бы исключены фильтром набора. Например, для тестирования политики, требующей, чтобы все руководители (и только руководители) имели разрешение на утверждение проверок, правило необходимо создать следующим образом.

|  |  |
|--|--|
|Имя. | Тест утверждения проверки|
|Элемент: | Users|
| Фильтр набора: | руководитель с любой ролью
|Фильтр правила: | исключительно имеет любое разрешение на утверждение проверок|

Это правило определит как соответствующих пользователей, которые являются руководителями и имеют разрешение на утверждение проверок, и пользователей, не являющихся руководителями и не имеющих разрешения на утверждение проверок. И наоборот, руководители, у которых нет этого разрешения, и пользователи, которые не являются руководителями, но имеют это разрешение, будут определены как несоответствующие требованиям.

Как отмечалось ранее, можно объединить правила в набор правил, упрощая классификацию правил и управление ими для удовлетворения бизнес-требований.

Можно также определить набор глобальных фильтров, которые, при включении, будут применяться к любому проверяемому правилу. Если вам часто требуется исключать определенный набор записей при проверке правил в разных наборах правил, можно указать глобальные фильтры, которые можно включать и отключать по мере необходимости.

## <a name="reporting"></a>Отчеты

Модуль создания отчетов BHOLD дает возможность просматривать данные в модели ролей в виде разнообразных отчетов. Модуль создания отчетов BHOLD предоставляет широкий набор встроенных отчетов, а также включает мастер, с помощью которого можно создавать как базовые, так и расширенные пользовательские отчеты. При запуске отчета можно немедленно просмотреть результаты или сохранить их в файле Microsoft Excel (XLSX). Чтобы просмотреть этот файл с помощью Microsoft Excel 2000, Microsoft Excel 2002 или Microsoft Excel 2003, можно скачать и установить пакет обеспечения совместимости Microsoft Office для форматов файлов Word, Excel и PowerPoint.


Модуль создания отчетов BHOLD преимущественно используется для составления отчетов, основанных на текущих сведениях о ролях. Если вам требуются отчеты для аудита изменений в данных удостоверений, можно воспользоваться функцией создания отчетов Forefront Identity Manager 2010 R2 для службы FIM, которая реализуется в хранилище данных System Center Service Manager. Дополнительные сведения о создании отчетов FIM см. в документации по Forefront Identity Manager 2010 и Forefront Identity Manager 2010 R2 в технической библиотеке Forefront Identity Management.

Категории, охватываемые встроенными отчетами, включают следующие.

- Administration
- Аттестация
- Элементы управления
- Внутреннее управление доступом
- Logging
- Модель
- Статистика
- Рабочий процесс

Можно создавать отчеты и добавлять их в эти категории, кроме того, можно определить собственные категории для размещения пользовательских и встроенных отчетов.

При создании отчета мастер позволяет указать следующие параметры:

- идентификационные данные, включая имя, описание, категорию, сферу применения и аудиторию;
- поля, отображаемые в отчете;
- запросы, которые задают анализируемые элементы;
- порядок сортировки строк;
- поля, используемые для разбиения отчета на разделы;
- фильтры для уточнения элементов, которые возвращаются в отчете.

На каждом этапе работы мастера можно просмотреть отчет в текущем состоянии и сохранить его, если не требуется указывать дополнительные параметры. Также можно вернуться к предыдущим шагам, чтобы изменить параметры, ранее заданные в мастере.

## <a name="access-management-connector"></a>Соединитель управления доступом

Модуль соединителя управления доступом BHOLD Suite поддерживает первоначальную и текущую синхронизацию данных с BHOLD. Соединитель управления доступом работает со службой синхронизации FIM, перемещая данные между базой данных BHOLD Core, метавселенной MIM и целевыми приложениями и хранилищами удостоверений.

В предыдущих версиях BHOLD для управления потоками данных между MIM и таблицами промежуточных баз данных BHOLD требовалось несколько агентов управления. В BHOLD Suite с пакетом обновления 1 (SP1) соединитель управления доступом позволяет определять в MIM агенты управления, которые будут обеспечивать передачу данных напрямую между BHOLD и MIM.

## <a name="mim-integration"></a>Интеграция с MIM

Важным и эффективным компонентом Forefront Identity Manager 2010 и Forefront Identity Manager 2010 R2 является портал самообслуживания, который позволяет конечным пользователям просматривать сведения об удостоверениях и членстве и управлять ими. Интеграция с MIM расширяет портал MIM, обеспечивая самостоятельное управление ролями. Например, с помощью функций BHOLD на портале MIM пользователь может запросить назначение роли и просмотреть активные роли и ожидающие запросы. Делегированным администраторам могут быть предоставлены дополнительные возможности, такие как возможность запросить назначения ролей для других пользователей.

Важно отметить, что расширения BHOLD для портала MIM поддерживают самостоятельное управление ролями и рабочими процессами, а также создание отчетов. Другие функции администрирования BHOLD, а также аттестация, предоставляются веб-порталами модулей BHOLD, размещаемыми отдельно от портала MIM.

## <a name="next-steps"></a>Дальнейшие шаги

- [Руководство по установке BHOLD](bhold-installation-guide.md)
- [Справочник разработчика BHOLD](../reference/mim2016-bhold-developer-reference.md)
- [Журнал версий BHOLD](../reference/version-bhold-history.md)
