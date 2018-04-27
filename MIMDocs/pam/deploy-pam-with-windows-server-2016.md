---
title: Развертывание Privileged Access Management для диспетчера удостоверений (Майкрософт) с помощью Windows Server 2016 | Документация Майкрософт
description: Сведения о развертывании Privileged Access Management с помощью Windows Server 2016
keywords: ''
author: barclayn
ms.author: barclayn
manager: mbaldwin
ms.date: 08/18/2017
ms.topic: article
ms.service: microsoft-identity-manager
ms.technology: active-directory-domain-services
ms.assetid: ''
ms.openlocfilehash: 6088afccec45d1353233a32828353149bcf24740
ms.sourcegitcommit: 48f89d555c0ac7caa97d149ee42e0b9ef6ccc5f5
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2018
---
# <a name="deploy-mim-pam-with-windows-server-2016"></a>Развертывание PAM диспетчера удостоверений (Майкрософт) (MIM) с помощью Windows Server 2016


В этом сценарии диспетчер удостоверений (Майкрософт) 2016 SP1 может использовать функции Windows Server 2016 в качестве контроллера домена для леса PRIV.  После настройки этого сценария билет Kerberos пользователя будет действителен, пока будет активна его роль. 

>[!Note]
Ознакомительные технические версии Windows Server 2016 до версии 5 нельзя использовать с этим диспетчером удостоверений (Майкрософт).

## <a name="preparation"></a>Подготовка

Для лабораторной среды требуются как минимум две виртуальные машины:

-   виртуальная машина под управлением Windows Server 2016, на которой размещен контроллер PRIV;

-   виртуальная машина под управлением Windows Server 2016 (рекомендуется) или Windows Server 2012 R2, на которой размещена служба MIM.

>[!NOTE]
Если в вашей лабораторной среде еще нет домена CORP, вам необходим дополнительный контроллер домена для этого домена. Контроллер домена CORP может работать под управлением Windows Server 2016 или Windows Server 2012 R2.


Выполните установку, как описано в [руководстве по началу работы](privileged-identity-management-for-active-directory-domain-services.md),  **за исключением настроек, описанных ниже**.

-   Если вы создаете новый домен CORP, во время выполнения инструкций из раздела [Шаг 1. Подготовка узла и домена CORP](step-1-prepare-corp-domain.md) вы можете при необходимости настроить домен CORP для режима работы Windows Server 2016. **Если вы выбрали этот вариант, внесите следующие изменения**.

    -   Если вы используете носитель Windows Server 2016, вариант установки будет называться Windows Server 2016 (сервер с возможностями рабочего стола).

    -   Вы можете указать режим работы Windows Server 2016 для леса и домена CORP, указав 7 как версию домена и леса в аргументе команды Install-ADDSForest, как показано ниже:
     ```
        Install-ADDSForest –DomainMode 7 –ForestMode 7 –DomainName contoso.local –DomainNetbiosName contoso –Force –NoDnsOnNetwork
        ```
    -   При создании новых пользователей и групп последняя команда (New-ADGroup -name 'CONTOSO\$\$\$' …) **не обязательна, если оба контроллера домена (CORP и PRIV) находятся в режиме работы домена Windows Server 2016**.

    -   Изменения, описанные в разделах "Настройка аудита" (пункт 8) и "Настройка параметров реестра" (пункт 10), **рекомендуются, но не являются обязательными**, если оба контроллера домена (CORP и PRIV) находятся в режиме работы домена Windows Server 2016.

-   Если вы решили использовать Windows Server 2012 R2 в качестве операционной системы для контроллера домена CORP, установите исправления 2919442, 2919355 [и обновите 3155495](http://support.microsoft.com/kb/3156418) на контроллере домена CORP.

-   Следуйте инструкциям в разделе [Шаг 2. Подготовка первого контроллера домена PRIV](step-2-prepare-priv-domain-controller.md), за исключением следующих поправок.

    -   Выполните установку с носителя Windows Server 2016. Вариант установки будет называться Windows Server 2016 (сервер с возможностями рабочего стола).

    -   В инструкциях по добавлению роли (пункт 4) **необходимо указать номера версии домена и леса в четвертой строке команд PowerShell, то есть 7**, чтобы разрешить работу описанных ниже функций Windows Server AD.

        ```
        Install-ADDSForest -DomainMode 7 -ForestMode 7 -DomainName priv.contoso.local  -DomainNetbiosName priv -Force -CreateDNSDelegation -DNSDelegationCredential $ca
        ```  

    -   При настройке прав аудита и входа в систему обратите внимание, что программа управления групповой политикой будет находиться в папке средств администрирования Windows.

    -   Настройка параметров реестра, необходимая для миграции журнала ИД безопасности (пункт 8) **не требуется, если домен PRIV находится в режиме работы Windows Server 2016**.

    -   После настройки делегирования и перед перезапуском сервера включите функции Privileged Access Management в Active Directory Windows Server 2016. Для этого откройте окно PowerShell от имени администратора и введите следующие команды.

    ```
    $of = get-ADOptionalFeature -filter "name -eq 'privileged access management feature'"
    Enable-ADOptionalFeature $of -scope ForestOrConfigurationSet -target "priv.contoso.local"
    ```

  -   После настройки делегирования и перед перезапуском сервера разрешите администраторам MIM и учетной записи службы MIM создавать и обновлять теневые субъекты.

     a. Откройте окно PowerShell и введите ADSIEdit.

     b. В меню "Действия" выберите команду "Подключиться к". В настройках точки подключения измените контекст именования с "Default naming context" на "Configuration" и нажмите кнопку "ОК".

     c. После подключения в левой части окна под заголовком "Редактирование ADSI" разверните узел "Конфигурация". Вы увидите конфигурации "CN=Configuration,DC=priv,...." Разверните "CN=Configuration", а затем разверните "CN=Services".

     d. Щелкните правой кнопкой мыши "CN=Shadow Principal Configuration" и выберите команду "Свойства". Когда откроется диалоговое окно свойств, перейдите на вкладку "Безопасность".

     д. Нажмите кнопку "Добавить". Укажите учетные записи MIMService, а также других администраторов MIM, которые позднее будут выполнять команду New-PAMGroup для создания дополнительных групп PAM. В списке разрешений для каждого пользователя добавьте разрешения "Запись", "Создание всех дочерних объектов" и "Удаление всех дочерних объектов". Добавьте разрешения.

     е. Перейдите к дополнительным параметрам безопасности. В строке, которая разрешает доступ MIMService, нажмите кнопку "Изменить". Укажите для параметра "Относится к" значение "Этот объект и все дочерние объекты". Обновите этот параметр разрешения и закройте диалоговое окно настроек безопасности.

     ж. Закройте редактор ADSI.

 -   После настройки делегирования и перед перезапуском сервера разрешите администраторам MIM создавать и обновлять политику проверки подлинности.

     a.  Откройте **командную строку** с повышенными привилегиями и введите следующие команды, подставив имя своей учетной записи администратора MIM вместо "mimadmin" в каждой из четырех строк:
    ```
       dsacls "CN=AuthN Policies,CN=AuthN Policy
       Configuration,CN=Services,CN=configuration,DC=priv,DC=contoso,DC=local" /g
       mimadmin:RPWPRCWD;;msDS-AuthNPolicy /i:s

       dsacls "CN=AuthN Policies,CN=AuthN Policy
       Configuration,CN=Services,CN=configuration,DC=priv,DC=contoso,DC=local" /g
       mimadmin:CCDC;msDS-AuthNPolicy

       dsacls "CN=AuthN Silos,CN=AuthN Policy
       Configuration,CN=Services,CN=configuration,DC=priv,DC=contoso,DC=local" /g
       mimadmin:RPWPRCWD;;msDS-AuthNPolicySilo /i:s

       dsacls "CN=AuthN Silos,CN=AuthN Policy
       Configuration,CN=Services,CN=configuration,DC=priv,DC=contoso,DC=local" /g
       mimadmin:CCDC;msDS-AuthNPolicySilo
    ```


-   Следуйте инструкциям в разделе [Шаг 3. Подготовка сервера PAM](step-3-prepare-pam-server.md), учитывая следующие поправки.

    -   При установке в Windows Server 2016 обратите внимание, что роль ApplicationServer недоступна.

    -   При установке MIM в Windows Server 2016 вы **не сможете установить SharePoint 2013**.

-   Следуйте инструкциям в разделе [Шаг 4. Установка компонентов MIM на сервере и рабочей станции PAM](step-4-install-mim-components-on-pam-server.md), учитывая следующие поправки.

    -   Для пользователя, который устанавливает компоненты PAM и службы MIM, **в AD должно быть настроено право записи в домен PRIV**, так как установка MIM создает новое подразделение AD "Объекты PAM".

    -   Если платформа SharePoint не установлена, не устанавливайте портал MIM.

-   Следуйте инструкциям в разделе [Шаг 5. Установка отношений доверия между лесами PRIV и CORP](step-5-establish-trust-between-priv-corp-forests.md), учитывая следующие поправки.

    -   При установке односторонних отношений доверия выполняйте только первые две команды PowerShell (get-credential and New-PAMTrust). **Не выполняйте команду New-PAMDomainConfiguration**.

    -   Когда отношения доверия будут установлены, войдите в контроллер домена PRIV как PRIV\\Administrator, запустите PowerShell и введите следующие команды:
  ```
    netdom trust contoso.local /domain:priv.contoso.local /enablesidhistory:yes
     /usero:contoso\administrator /passwordo:Pass@word1

     netdom trust contoso.local /domain:priv.contoso.local /quarantine:no
     /usero:contoso\administrator /passwordo:Pass@word1  

     netdom trust contoso.local /domain:priv.contoso.local /enablepimtrust:yes
     /usero:contoso\administrator /passwordo:Pass@word1
  ```

-   Пункт 5 (проверка доверия) **не обязателен, если оба контроллера домена (CORP и PRIV) находятся в режиме работы домена Windows Server 2016**.

## <a name="more-information"></a>Дополнительные сведения

- [Управление привилегированным доступом для доменных служб Active Directory](privileged-identity-management-for-active-directory-domain-services.md)
- [Настройка среды MIM для Privileged Access Management](configuring-mim-environment-for-pam.md)
- [Настройка управления привилегированным доступом (PAM) с помощью сценариев](sp1-pam-configure-using-scripts.md)
