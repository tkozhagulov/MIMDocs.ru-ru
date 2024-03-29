---
title: Планирование среды бастиона | Документация Майкрософт
description: ''
keywords: ''
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 09/13/2017
ms.topic: article
ms.prod: microsoft-identity-manager
ms.assetid: bfc7cb64-60c7-4e35-b36a-bbe73b99444b
ms.reviewer: mwahl
ms.suite: ems
ms.openlocfilehash: f8fd71d2244760d3a6561c6f55bf676e6f42561a
ms.sourcegitcommit: 44a2293ff17c50381a59053303311d7db8b25249
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/31/2018
ms.locfileid: "50380074"
---
# <a name="planning-a-bastion-environment"></a>Планирование среды бастиона

Добавление в Active Directory среды бастиона с выделенным административным лесом позволяет организациям легко управлять административными учетными записями, рабочими станциями и группами в среде с более высоким уровнем управления безопасностью, чем у существующей рабочей среды.

Эта архитектура предоставляет ряд элементов управления, невозможных или с трудом настраиваемых в архитектуре с одним лесом. Такой подход включает подготовку учетных записей обычных, непривилегированных пользователей в административном лесу, имеющем высокий уровень привилегий в рабочей среде, что обеспечивает более эффективную техническую реализацию управления. Эта архитектура позволяет также использовать функцию выборочной проверки подлинности доверия для разрешения входа (и раскрытия учетных данных) только на авторизованные узлы. В ситуациях, где для производственного леса желателен более высокий уровень надежности без увеличения стоимости и сложности, необходимых для полного перестроения леса, административный лес может предоставить среду, которая повышает уровень надежности рабочей среды.

Вместе с выделенным административным лесом можно использовать дополнительные методы. К ним относятся ограничение того, где предоставляются учетные данные администратора, ограничение привилегий ролей пользователей в этом лесу и запрет на выполнение административных задач на узлах, используемых для выполнения действий обычного пользователя (например, работы с электронной почтой и просмотра веб-страниц).

## <a name="best-practice-considerations"></a>Советы и рекомендации

Выделенный административный лес — это стандартный лес Active Directory с одним доменом, используемый для управления Active Directory. Преимущество использования административных лесов и доменов состоит в том, что они способны обеспечить более высокий уровень безопасности, чем производственные леса, ввиду ограниченных вариантов их использования. Более того, поскольку этот лес отделен и не доверяет существующим лесам организации, нарушение безопасности в другом лесу не распространится на выделенный лес.

При проектировании административного леса следует иметь в виду следующие аспекты.

### <a name="limited-scope"></a>Ограниченная область применения

Предназначение административного леса — высокий уровень безопасности и сокращение возможных направлений атак. В лесу могут размещаться дополнительные функции и приложения управления, но любое такое расширение области применения увеличивает возможные направления атак леса и его ресурсов. Это сделано для того, чтобы ограничить функции леса и максимально сократить уязвимость.

В соответствии с [многоуровневой моделью](tier-model-for-partitioning-administrative-privileges.md) разделения прав администратора по уровням учетные записи в выделенном административном лесу должны находиться на одном уровне, обычно на уровне 0 или 1. Если лес находится на уровне 1, его можно ограничить определенной областью применения (например, финансовыми приложениями) или сообществом пользователей (например, внешними поставщиками ИТ).

### <a name="restricted-trust"></a>Ограниченное доверие

Производственный лес *CORP* должен доверять административному лесу *PRIV*, но не наоборот. Это может быть доверие домена или доверие леса. Домену административного леса для управления Active Directory не требуется доверять управляемым доменам и лесам, хотя дополнительным приложениям может потребоваться двустороннее отношение доверия, проверка безопасности или тестирование.

Чтобы разрешить учетным записям в административном лесу входить только на соответствующие производственные узлы, используется выборочная проверка подлинности. Для поддержания контроллеров домена и делегирования прав в Active Directory обычно требуется предоставлять право "Разрешен вход в систему" для контроллеров домена назначенным учетным записям администратора уровня 0 в административном лесу. См. раздел [Настройка параметров выборочной проверки подлинности](http://technet.microsoft.com/library/cc816580.aspx) для получения дополнительной информации.

## <a name="maintain-logical-separation"></a>Обслуживание логического разделения

Чтобы среду бастиона не затронули существующие или будущие инциденты безопасности в службе Active Directory организации, следует учитывать следующие рекомендации при подготовке системы для среды бастиона.

- Серверы Windows Server не должны быть присоединены к домену, использовать программное обеспечение или распространяемые параметры существующей среды.

- Среда бастиона должна содержать собственные доменные службы Active Directory, предоставляющие среде бастиона службы Kerberos, LDAP, DNS, а также службы времени.

- MIM не должен использовать ферму базы данных SQL в существующей среде. SQL Server должен быть развернут на выделенных серверах в среде бастиона.

- Среде бастиона требуется диспетчер удостоверений (Майкрософт) (MIM) 2016; в частности, должны быть развернуты служба MIM и компоненты PAM.

- Программное обеспечение резервного копирования и носители среды бастиона должны быть отделены от соответствующих ПО и носителей в существующих лесах таким образом, чтобы администратор в существующем лесу не мог нарушить состояние резервной копии среды бастиона.

- Пользователи, управляющие серверами среды бастиона, должны входить в систему с рабочих станций, недоступных для администраторов в существующей среде, чтобы не допустить утечки учетных данных среды бастиона.

## <a name="ensure-availability-of-administration-services"></a>Обеспечение доступности служб администрирования

Поскольку администрирование приложений будет переноситься в среду бастиона, необходимо учитывать, каким образом обеспечится достаточная доступность в соответствии с требованиями этих приложений. Методы включают следующее:

- Развертывание доменных служб Active Directory на нескольких компьютерах в среде бастиона. Для обеспечения постоянной проверки подлинности необходимы по крайней мере два сервера (если один будет перезапускаться для запланированного обслуживания). Дополнительные компьютеры могут потребоваться при большой нагрузке, а также для управления ресурсами и администраторами, находящимися в различных географических регионах.

- Подготовка в существующем лесу и выделенном административном лесу аварийных учетных записей для экстренных случаев.

- Развертывание SQL Server и службы MIM на нескольких компьютерах в среде бастиона.

- Создание резервных копий AD и SQL для всех изменений пользователей и определений ролей в выделенном административном лесу.

## <a name="configure-appropriate-active-directory-permissions"></a>Настройка соответствующих разрешений Active Directory

Административный лес должен быть настроен для предоставления наименьших прав доступа в соответствии с требованиями для администрирования Active Directory.

- Учетные записи в административном лесу, используемые для администрирования рабочей среды, не должны иметь прав администратора в лесу администрирования, его доменах и на рабочих станциях в нем.

- Права администратора в самом административном лесу должны жестко контролироваться автономным процессом, чтобы уменьшить возможность для злоумышленников извне или изнутри компании стереть журналы аудита. Это также помогает убедиться, что персонал с учетными записями администратора для рабочей среды не сможет ослабить ограничения своих учетных записей и повысить риск для организации.

- Административный лес должен соответствовать конфигурациям диспетчера соответствия требованиям безопасности Майкрософт (SCM) для данного домена, включая надежные конфигурации для протоколов проверки подлинности.

При создании среды бастиона, перед установкой диспетчера Microsoft Identity Manager (MIM), определите и создайте учетные записи, которые будут использоваться для администрирования в этой среде. Сюда входят следующие учетные записи:

- **Аварийные учетные записи** должны разрешать вход только на контроллеры домена в среде бастиона.

- **Администраторы "красной карточки"** предназначены для подготовки других учетных записей и проведения внепланового обслуживания. У них не должно быть доступа к существующим лесам и системам вне среды бастиона. Учетные данные, например смарт-карты, должны быть физически защищены, а использование этих учетных записей должно регистрироваться в журнале.

- **Учетные записи служб**, необходимые диспетчеру Microsoft Identity Manager (MIM), SQL Server и другим программам.

## <a name="harden-the-hosts"></a>Усиление защиты узлов

На всех узлах, присоединенных к административному лесу (включая контроллеры домена, серверы и рабочие станции), должны быть установлены новейшие операционные системы с последними пакетами обновления. Также должно быть организовано регулярное обновление ОС.

- Приложения, необходимые для администрирования, следует заранее установить на рабочих станциях, чтобы их учетным записям не требовалось состоять в группе локальных администраторов для установки приложений. Обслуживание контроллеров домена обычно можно выполнять с помощью удаленного рабочего стола и средств удаленного администрирования сервера.

- Узлы административного леса должны автоматически получать обновления системы безопасности. Хотя это может создать риск прерывания операций обслуживания контроллера домена, риск нарушения безопасности из-за незакрытых уязвимостей будет значительно ниже.

### <a name="identify-administrative-hosts"></a>Определение узлов администрирования

Риск системы или рабочей станции оценивается по самому высокому риску выполняемых в ней действий, среди которых просмотр ресурсов Интернета, отправка и получение электронной почты, использование других приложений, обрабатывающих неизвестное или ненадежное содержимое.

Узлы администрирования включают следующие компьютеры:

- Компьютер, на котором физически вводятся учетные данные администратора.

- Административные "серверы перехода", на которых открываются административные сеансы и запускаются средства администрирования.

- Все узлы, на которых выполняются административные действия, включая те, которые используют для удаленного администрирования серверов и приложений рабочий стол обычного пользователя с клиентом RDP.

- Серверы, на которых размещены подлежащие администрированию приложения, доступ к которым производится не с помощью протокола удаленного рабочего стола или удаленного взаимодействия Windows PowerShell.

### <a name="deploy-dedicated-administrative-workstations"></a>Развертывание выделенных административных рабочих станций

Несмотря на неудобство, для пользователей с критически важными административными правами могут быть выделены отдельные рабочие станции с усиленной защитой. При этом узлу необходимо обеспечить уровень безопасности, который будет равен уровню прав таких пользователь или превышать его. Рассмотрим внедрение следующих мер для дополнительной защиты:

- **Проверка на чистоту всех установочных носителей** для снижения риска активизации вредоносных программ, которые могли быть установлены в главный образ или внедрены в файл установки во время загрузки или хранения.

- **Базовые конфигурации безопасности** , которые следует использовать в качестве начальных конфигураций. Диспетчер соответствия требованиям безопасности Майкрософт (SCM) может помочь с настройкой базовых конфигураций на узлах администрирования.

- **Безопасная загрузка** для противодействия взломщикам и вредоносным программам, пытающимся внедрить неподписанный код в процесс загрузки.

- **Ограничение ПО** , обеспечивающее выполнение на узлах администрирования только авторизованного ПО администрирования. Клиенты могут использовать для этой задачи AppLocker с белым списком разрешенных приложений, что предотвратит выполнение вредоносных программ и неподдерживаемых приложений.

- **Полное шифрование тома** для обеспечения безопасности при физической потере компьютеров, в частности используемых удаленно ноутбуков администраторов.

- **Ограничения USB** для защиты от инфицирования с физических носителей.

- **Сетевая изоляция** для защиты от сетевых атак и случайных административных операций. Брандмауэры должны блокировать все входящие подключения, кроме явно разрешенных, и все ненужные исходящие подключения к Интернету.

- **Антивирусное ПО** для защиты от известных угроз и вредоносных программ.

- **Защита от уязвимостей** для защиты от неизвестных угроз и уязвимостей, включая набор средств Enhanced Mitigation Experience Toolkit (EMET).

- **Анализ возможных направлений атак** для предотвращения появления в Windows новых направлений атак во время установки нового программного обеспечения. Такие средства, как Attack Surface Analyzer (ASA), помогут оценить параметры конфигурации на узле и определить векторы атак, возникающие в результате изменений программного обеспечения или конфигурации.

- Пользователям не следует предоставлять **права администратора** на их локальных компьютерах.

- Исходящие RDP-сеансы должны иметь **режим RestrictedAdmin**, за исключением случаев, когда иное требуется для используемой роли. См. раздел [Что нового в службах удаленных рабочих столов в Windows Server](https://technet.microsoft.com/library/dn283323.aspx) для получения дополнительной информации.

Некоторые из этих мер могут показаться чрезмерными, но события последних лет показали значительные возможности несанкционированного доступа к данным, которыми обладают опытные злоумышленники.

## <a name="prepare-existing-domains-to-be-managed-by-the-bastion-environment"></a>Подготовка существующих доменов для управления средой бастиона

Для установления доверия между существующими доменами AD и выделенным административным лесом в среде бастиона в MIM используются командлеты PowerShell. После развертывания среды бастиона и до преобразования любых пользователей или групп в JIT командлеты `New-PAMTrust` и `New-PAMDomainConfiguration` обновляют отношение доверия для домена и создают артефакты, необходимые для AD и MIM.

При изменении существующей топологии Active Directory для обновления отношения доверия можно использовать командлеты `Test-PAMTrust`, `Test-PAMDomainConfiguration`, `Remove-PAMTrust` и `Remove-PAMDomainConfiguration` .

## <a name="establish-trust-for-each-forest"></a>Установление доверия для каждого леса

Командлет `New-PAMTrust` необходимо запустить один раз для каждого существующего леса. Он вызывается на компьютере службы MIM в административном домене. Параметры этой команды — имя верхнего домена в существующем лесу и учетные данные администратора этого домена.

```
New-PAMTrust -SourceForest "contoso.local" -Credentials (get-credential)
```

После установления доверия следует настроить каждый домен так, чтобы включить управление из среды бастиона, как описано в следующем разделе.

## <a name="enable-management-of-each-domain"></a>Включение управления для каждого домена

Существует семь требований для включения управления в существующем домене.

### <a name="1-a-security-group-on-the-local-domain"></a>1. Группа безопасности в локальном домене

В существующем домене должна быть группа, имя которой представляет собой имя NetBIOS домена с тремя знаками доллара, например *CONTOSO$$$*. Область этой группы должна быть задана как *локальная группа домена*, а ее тип — как *безопасность*. Это потребуется для того, чтобы группы в выделенном административном лесу создавались с тем же идентификатором безопасности, что и группы в этом домене. Такая группа создается с помощью следующей команды PowerShell, выполняемой администратором существующего домена на рабочей станции, присоединенной к существующему домену:

```PowerShell
New-ADGroup -name 'CONTOSO$$$' -GroupCategory Security -GroupScope DomainLocal -SamAccountName 'CONTOSO$$$'
```

### <a name="2-success-and-failure-auditing"></a>2. Аудит успехов и неудач

Параметры групповой политики на контроллере домена для аудита должны включать аудит как успехов, так и неудач для аудита управления учетными записями и аудита доступа к службе каталогов. Это может сделать администратор существующего домена с помощью консоли управления групповыми политиками на рабочей станции, присоединенной к существующему домену.

3. Последовательно выберите пункты **Пуск** > **Администрирование** > **Управление групповыми политиками**.

4. Перейдите в раздел **Лес: contoso.local** > **Домены** > **contoso.local** > **Контроллеры доменов** > **Политика контроллеров доменов по умолчанию**. Появится информационное сообщение.

    ![Политика контроллеров доменов по умолчанию — снимок экрана](media/pam-group-policy-management.jpg)

5. Щелкните правой кнопкой мыши пункт **Политика контроллеров домена по умолчанию** и выберите команду **Изменить**. Откроется новое окно.

6. В окне "Редактор управления групповыми политиками" в дереве "Политика контроллеров домена по умолчанию" перейдите к пункту **Настройка компьютера** > **Политики** > **Параметры Windows** > **Параметры безопасности** > **Локальные политики** > **Политики аудита**.

    ![Редактор управления групповыми политиками — снимок экрана](media/pam-group-policy-management-editor.jpg)

5. В области сведений щелкните правой кнопкой мыши пункт **Управление учетной записью аудита** и выберите пункт **Свойства**. Установите флажок **Определить следующие параметры политики**, флажки **Выполнено** и **Сбой**, нажмите кнопку **Применить**, а затем **ОК**.

6. В области сведений щелкните правой кнопкой мыши пункт **Доступ к службе каталогов аудита** и выберите пункт **Свойства**. Установите флажок **Определить следующие параметры политики**, флажки **Выполнено** и **Сбой**, нажмите кнопку **Применить**, а затем **ОК**.

    ![Параметры успешной и неудачной политики — снимок экрана](media/pam-group-policy-management-editor2.jpg)

7. Закройте окно редактора управления групповыми политиками и окно управления групповыми политиками. Затем примените параметры аудита, открыв окно PowerShell и выполнив следующую команду:

    ```cmd
    gpupdate /force /target:computer
    ```

Через несколько минут должно появиться сообщение "Обновление политики компьютера успешно завершено".

### <a name="3-allow-connections-to-the-local-security-authority"></a>3. Разрешение подключений к локальной системе безопасности

Контроллеры домена должны разрешать RPC через соединения TCP/IP для локальной системы безопасности (LSA) из среды бастиона. В предыдущих версиях Windows Server поддержку TCP/IP в LSA следует включить в реестре.

```PowerShell
New-ItemProperty -Path HKLM:SYSTEM\\CurrentControlSet\\Control\\Lsa -Name TcpipClientSupport -PropertyType DWORD -Value 1
```

### <a name="4-create-the-pam-domain-configuration"></a>4. Создание конфигурации домена PAM

Командлет `New-PAMDomainConfiguration` необходимо запускать на компьютере службы MIM в административном домене. Параметры этой команды — имя существующего домена и учетные данные администратора этого домена.

```PowerShell
 New-PAMDomainConfiguration -SourceDomain "contoso" -Credentials (get-credential)
```

### <a name="5-give-read-permissions-to-accounts"></a>5. Предоставление учетным записям разрешений на чтение

В лесу-бастионе учетным записям, используемым для определения ролей (администраторам, использующим командлеты `New-PAMUser` и `New-PAMGroup` ), а также учетной записи, используемой службой мониторинга MIM, нужны разрешения на чтение в этом домене.

Следующие шаги включают предоставление пользователю *PRIV\Administrator* доступа на чтение домена *Contoso* в контроллере домена *CORPDC*.

1. Убедитесь, что вы вошли в CORPDC с правами администратора домена Contoso (например, Contoso\Administrator).

2. Запустите оснастку "Пользователи и компьютеры Active Directory".

3. Щелкните правой кнопкой мыши домен **contoso.local** и выберите пункт **Делегирование управления**.

4. На вкладке "Выбранные пользователи и группы" нажмите кнопку **Добавить**.

5. Во всплывающем окне Выбор пользователей, компьютеров или групп нажмите кнопку **Расположения** и измените расположение на *priv.contoso.local*. В качестве имени объекта введите *Администраторы домена* и нажмите кнопку **Проверить имена**. Когда появится всплывающее окно, введите имя пользователя *priv\administrator* и соответствующий пароль.

6. После группы "Администраторы домена" допишите *; MIMMonitor*. Когда "Администраторы домена" и MIMMonitor будут подчеркнуты, нажмите кнопку **ОК**, а затем **Далее**.

7. В списке типичных задач выберите **Чтение информации обо всех пользователях**, нажмите кнопку **Далее**, а затем **Готово**.

18. Закройте окно "Пользователи и компьютеры Active Directory".

### <a name="6-a-break-glass-account"></a>6. Аварийные учетные записи

Если целью проекта управления привилегированным доступом является уменьшение числа учетных записей с правами администратора домена, постоянно назначенных домену, в домене должна быть создана *аварийная* учетная запись на случай возможных проблем с отношениями доверия. Учетные записи аварийного доступа в производственный лес должны существовать в каждом домене и должны обеспечивать вход только в контроллеры домена. Для организаций с несколькими филиалами могут потребоваться дополнительные учетные записи для обеспечения избыточности.

### <a name="7-update-permissions-in-the-bastion-environment"></a>7. Обновление разрешений в среде бастиона

Просмотрите разрешения для объекта *AdminSDHolder* в контейнере System в этом домене. Объект *AdminSDHolder* имеет уникальный список управления доступом (ACL), используемый для управления разрешениями субъектов безопасности, которые являются членами встроенных привилегированных групп Active Directory. Примечание. Если разрешения по умолчанию были изменены, это отразится на пользователях с правами администратора в этом домене, поскольку эти разрешения не будут применяться к пользователям, чьи учетные записи находятся в среде бастиона.

## <a name="select-users-and-groups-for-inclusion"></a>Выбор пользователей и групп для включения

Следующим шагом является определение ролей PAM, сопоставляющих пользователей с группами, к которым они имеют доступ. Как правило, это будет подмножество пользователей и групп для уровня, указанного в качестве управляемого в среде бастиона. Дополнительные сведения см. в статье [Определение ролей для управления привилегированным доступом](defining-roles-for-pam.md).
