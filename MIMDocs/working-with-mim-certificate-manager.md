---
title: "Развертывание приложения диспетчера сертификатов MIM для Windows | Документация Microsoft"
description: "Узнайте, как развернуть приложение диспетчера сертификатов, чтобы позволить пользователям управлять своими правами доступа."
keywords: 
author: billmath
ms.author: barclayn
manager: mbaldwin
ms.date: 10/16/2017
ms.topic: article
ms.service: microsoft-identity-manager
ms.technology: security
ms.assetid: 66060045-d0be-4874-914b-5926fd924ede
ms.reviewer: mwahl
ms.suite: ems
ms.openlocfilehash: e472d7cdc07aa19464aa1f18447d8c5dc7d0f0ba
ms.sourcegitcommit: 1e0626a366a41d610e6a117cdf684241eb65ec63
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/17/2017
---
# <a name="mim-certificate-manager-windows-store-application-deployment"></a>Развертывание приложения диспетчера сертификатов MIM из магазина Windows

Убедившись, что MIM 2016 и диспетчер сертификатов запущены, вы можете развернуть приложение диспетчера сертификатов из магазина Windows. Приложение магазина Windows позволяет пользователям управлять физическими смарт-картами, виртуальными смарт-картами и сертификатами программного обеспечения. Чтобы развернуть приложение MIM CM, необходимо выполнить следующие действия:

1. создать шаблон сертификата;

2. создать шаблон профиля;

3. подготовить приложение;

4. развернуть приложение через SCCM или Intune.

## <a name="create-a-certificate-template"></a>Создание шаблона сертификата

Шаблон сертификата для приложения CM создается как и обычно, за исключением того, что необходимо убедиться, что используется шаблон сертификата версии 3 или более поздней.

1. Войдите на сервер под управлением AD CS (сервер сертификатов).

2. Откройте консоль MMC.

3. Щелкните **Файл &gt; Добавить или удалить оснастку**.

4. В списке доступных оснасток выберите **Шаблоны сертификатов**, а затем нажмите кнопку **Добавить**.

5. В консоли MMC в разделе **корень консоли** вы увидите раздел **Шаблоны сертификатов** . Дважды щелкните его, чтобы увидеть все доступные шаблоны сертификатов.

6. Щелкните правой кнопкой мыши шаблон **Вход со смарт-картой** и выберите команду **Скопировать шаблон**.

7. На вкладке "Совместимость" в поле "Центр сертификации" выберите "Windows Server 2008". В поле "Получатель сертификата" выберите "Windows 8.1/Windows Server 2012 R2". Версия шаблона устанавливается при первом создании и сохранении шаблона сертификата. Если вы не создавали шаблон сертификата таким образом, изменить эту версию на правильную невозможно.

    >[!NOTE]
    Этот шаг очень важен, так как на нем проверяется версия шаблона сертификата. Необходима версия 3 или более поздняя версия. С приложением диспетчера сертификатов работают только шаблоны версии 3.
    
8.  На вкладке **Общие** в поле **Отображаемое имя** введите имя, которое будет отображаться в пользовательском интерфейсе приложения, например **Вход с виртуальной смарт-картой**.

9. На вкладке **Обработка запроса** задайте для параметра **Цель** значение **Подпись и шифрование**, а для параметра **Выполнить следующие действия...** выберите **Запрашивать пользователя во время регистрации**.

10. На вкладке **Шифрование** в разделе **Категория поставщика**выберите **Поставщик хранилища ключей и запросы могут использовать любого поставщика, доступного на компьютере субъекта**.

    > [!NOTE]
    > Если версия шаблона — 3, вы увидите среди вариантов только поставщик хранилища ключей. Если он не отображается, возможно, вы неправильно создали шаблон сертификата с нужной версией. Начните с шага 5 выше.

11. На вкладке **Безопасность** добавьте группу безопасности, которой необходимо предоставить доступ **Заявка** . Например, если вы хотите предоставить доступ всем пользователям, выберите группу пользователей **Проверка подлинности выполнена** , а затем выберите для них разрешения **Заявка** .

12. Нажмите кнопку **ОК** , чтобы завершить изменения и создать новый шаблон. Вы увидите новый шаблон в списке шаблонов сертификатов.

13. Выберите **Файл** и нажмите кнопку **Добавить или удалить оснастку**, чтобы добавить в консоль MMC оснастку "Центр сертификации". Когда вам будет предложено выбрать компьютер, которым вы хотите управлять, выберите **Локальный компьютер**.

14. В левой области консоли MMC разверните узел **Центр сертификации (локальный)** и разверните свой центр сертификации в списке центров сертификации.

15. Правой кнопкой мыши щелкните **Шаблоны сертификатов**и выберите **Создать &gt; Выдаваемый шаблон сертификата**.

16. Выберите созданный шаблон из списка и нажмите кнопку **ОК**.

## <a name="create-a-profile-template"></a>Создание шаблона профиля

При создании шаблона профиля необходимо создать или удалить vSC и удалить коллекцию данных. Приложение CM не может обрабатывать собранные данные, поэтому требуется отключить его, как показано ниже.

1.  Войдите на портал CM от имени пользователя с правами администратора.

2.  Перейдите к профилям в разделе "Администрирование" &gt; "Управление профилем". Убедитесь, что флажок **Шаблон профиля входа с помощью смарт-карты MIM CM** установлен, а затем щелкните "Копировать выбранный шаблон профиля".

3.  Введите имя профиля шаблона и нажмите кнопку **ОК**.

4.  На следующем экране выберите **Добавить новый шаблон сертификата** и установите флажок рядом с именем ЦС.

5.  Установите флажок рядом с именем профиля шаблона **Вход** и нажмите кнопку **Добавить**.

6.  Удалите шаблон SmartCardLogon. Для этого установите рядом с ним флажок и нажмите кнопку **Удалить выбранные шаблоны сертификатов** , а затем **ОК**.

7.  Прокрутите вниз и нажмите кнопку **Изменить параметры**.

8.  Установите флажки **Create/Destroy virtual smart card** (Создать и удалить виртуальную смарт-карту) и **Diversify Admin Key** (Диверсифицировать ключ администратора).

9. В разделе **Политика ПИН-кода пользователя** выберите **Предоставляется пользователем**.

10. В левой области щелкните **Обновить политику &gt; Изменить общие параметры**. Выберите параметр **Повторно использовать карту при обновлении** и нажмите кнопку **ОК**.

11. Отключите элементы сбора данных для каждой политики, щелкнув политику в области слева. Затем установите флажок **Пример элемента данных**, щелкните **Удалить элементы сбора данных** и нажмите кнопку **ОК**.

## <a name="prepare-the-cm-app-for-deployment"></a>Подготовка к развертыванию приложения CM

1. В командной строке выполните следующую команду, чтобы распаковать приложение. Эта команда извлечет содержимое пакета в новую вложенную папку с именем appx и создаст копию, чтобы не изменять исходные файлы.

    ```cmd
    makeappx unpack /l /p <app package name>.appx /d ./appx
    ren <app package name>.appx <app package name>.appx.original
    cd appx
    ```

2. В папке appx переименуйте файл с именем CustomDataExample.xml на Custom.data

3. Откройте файл Custom.data и при необходимости измените параметры.

    |||
    |-|-|
    |URL-адрес MIM CM|Полное доменное имя портала, которое использовалось для настройки CM. Например: https://mimcmServerAddress/certificatemanagement|
    |URL-адрес ADFS|Если вы используете службы AD FS, укажите URL-адрес AD FS. Например: https://adfsServerSame/adfs </br> Если службы федерации Active Directory не используются, укажите пустую строку в качестве значения параметра.  Например: ```<ADFS URL=""/>``` |
    |PrivacyUrl|Вы можете указать URL-адрес веб-страницы, на которой описывается, что вы будете делать с данными пользователя, полученными для регистрации сертификата.|
    |SupportMail|Можно указать электронный адрес службы поддержки.|
    |LobComplianceEnable|Этому параметру можно задать значение true или false. Значение по умолчанию — true.|
    |MinimumPinLength|Значение по умолчанию — 6.|
    |NonAdmin|Этому параметру можно задать значение true или false. Значение по умолчанию — false. Это значение следует изменить, только чтобы пользователи, не являющиеся администраторами на своих компьютерах, могли регистрировать и обновлять сертификаты.|
>[!IMPORTANT]
Необходимо указать значение URL-адреса служб федерации Active Directory. Если значение не указано, современное приложение выдаст ошибку при первом использовании.
4.  Сохраните файл и закройте редактор.

5.  После подписи пакета создается файл подписи, поэтому нужно удалить исходный файл с именем AppxSignature.p7x.

6.  Файл AppxManifest.xml задает имя субъекта сертификата подписи. Откройте его для редактирования.

7.  Перед началом изучения этого раздела вам необходимо получить сертификат подписи. См. раздел "Включение обновления смарт-карты для администраторов в диспетчере сертификатов MIM 2016", шаг 1 ниже.

8.  В элементе &lt;Identity&gt; присвойте атрибуту Publisher значение, совпадающее с субъектом, указанным в сертификате подписи, например "CN=SUBJECT".

9. Сохраните файл и закройте редактор.

10. В командной строке выполните следующую команду, чтобы повторно упаковать и подписать APPX-файл.

    ```cmd
    cd ..
    makeappx pack /l /d .\appx /p <app package name>.appx
    ```
    где имя пакета приложения — это то же имя, которое использовалось при создании копии.

    ```cmd
    signtool sign /f <path\>mysign.pfx /p <pfx password> /fd "sha256" <app package name>.ap
    px
    ```
    Так будет создан новый APPX-файл. PFXf-файл предоставляет расположение для сертификата подписи и пароль для PFX-файла.

11. Для работы с проверкой подлинности AD FS:

    -  Откройте приложение Virtual Smart Card. Это упрощает поиск значений, необходимых для следующего шага.

    -  На сервере AD FS откройте Windows PowerShell и выполните команду `ConfigureMimCMClientAndRelyingParty.ps1 –redirectUri <redirectUriString> -serverFQDN <MimCmServerFQDN>`, чтобы добавить приложение в качестве клиента на сервер AD FS и настроить CM на сервере.

        Ниже приведен скрипт ConfigureMimCMClientAndRelyingParty.ps1:

       ```PowerShell
        # HELP

        <#
        .SYNOPSIS
                        Configure ADFS for CM client app and server.
        .DESCRIPTION
           What the Script does:
                                        a. Registers the MIM CM client app on the ADFS server.
                                        b. Registers the MIM CM server relying party (Tells the ADFS server that it issues tokens for the CM server).
                        For parameter information, see 'get-help -detailed'
        .PARAMETER redirectUri
                        The redirectUri for CM client app. Will be added to ADFS server.
                        It can be found as follows:
                        1. Open the settings panel. Under settings, there is a "Redirect Uri" text box (an ADFS server address must be configured in order for the text to display).
                        2. Open MIM CM client app. Navigate to 'C:\Users\<your_username>\AppData\Local\Packages\CmModernAppv.<version>\LocalState', and open 'Logs_Virtual Smart Card Certificate Manager_<version>'. Search for "Redirect URI".
        .PARAMETER serverFqdn
                        Your deployed MIM CM server’s FQDN.
        .EXAMPLE
           .\ConfigureMimCMClientAndRelyingParty.ps1 -redirectUri ms-app://s-1-15-2-0123456789-0123456789-0123456789-0123456789-0123456789-0123456789-0123456789/ -serverFqdn WIN-TRUR24L4CFS.corp.cmteam.com
        #>

        # Parameter declaration
        [CmdletBinding()]
        Param(
          [Parameter(Mandatory=$True)]
           [string]$redirectUri,

           [Parameter(Mandatory=$True)]
           [string]$serverFqdn
        )

        Write-Host "Configuring ADFS Objects for OAuth.."

        #Configure SSO to get persistent sign on cookie
        Set-ADFSProperties -SsoLifetime 2880

        #Configure Authentication Policy
        #Intranet to use Kerberos
        #Extranet to use U/P

        #Create Client Objects

        Write-Host "Creating Client Objects..."

        $existingClient = Get-ADFSClient -Name "MIM CM Modern App"

        if ($existingClient -ne $null)
        {
            Write-Host "Found existing instance of the MIM CM Modern App, removing"
            Remove-ADFSClient -TargetName "MIM CM Modern App"
            Write-Host "Client object removed"
        }

        Write-Host "Adding Client Object for MIM CM Modern App client"
        Add-ADFSClient -Name "MIM CM Modern App" -ClientId "70A8B8B1-862C-4473-80AB-4E55BAE45B4F" -RedirectUri $redirectUri
        Write-Host "Client Object for MIM CM Modern App client Created"

        #Create Relying Parties
        Write-Host "Creating Relying Party Objects"

        $existingRp = Get-ADFSRelyingPartyTrust -Name "MIM CM Service"
        if ($existingRp -ne $null)
        {
            Write-Host "Found existing instance of the MIM CM Service RP, removing"
            Remove-ADFSRelyingPartyTrust -TargetName "MIM CM Service"
            Write-Host "RP object Removed"
        }

        $authorizationRules =
        "@RuleTemplate = `"AllowAllAuthzRule`"
        => issue(Type = `"http://schemas.microsoft.com/authorization/claims/permit`", Value = `"true`");"

        $issuanceRules =
        "@RuleTemplate = `"LdapClaims`"
        @RuleName = `"Emit UPN and common name`"
        c:[Type == `"http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname`", Issuer == `"AD AUTHORITY`"]
        => issue(store = `"Active Directory`", types =
        (`"http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn`",
        `"http://schemas.xmlsoap.org/claims/CommonName`"), query =
        `";userPrincipalName,cn;{0}`", param = c.Value);

        @RuleTemplate = `"PassThroughClaims`"
        @RuleName = `"Pass through Windows Account Name`"
        c:[Type ==`"http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname`"] => issue(claim = c);"

        Write-Host "Creating RP Trust for MIM CM Service"
        Add-ADFSRelyingPartyTrust -Name "MIM CM Service" -Identifier ("https://"+$serverFqdn+"/certificatemanagement") -IssuanceAuthorizationRules $authorizationRules -IssuanceTransformRules $issuanceRules
        Write-Host "RP Trust for MIM CM Service has been created"
        ```

    - Обновите значения параметров redirectUri и serverFQDN.

    - Чтобы найти redirectUri, в приложении Virtual Smart Card откройте панель параметров приложения, нажмите кнопку **Параметры**. URI перенаправления должен быть указан в адресной строке сервера AD FS. URI отображается, только если настроен адрес сервера AD FS.

    - serverFQDN — это полное имя компьютера сервера MIMCM.

    - Чтобы получить справку по скрипту **ConfigureMIimCMClientAndRelyingParty.ps1**, выполните следующую команду. </br> 
    ```Powershell
     get-help  -detailed ConfigureMimCMClientAndRelyingParty.ps1
    ```

## <a name="deploy-the-app"></a>Развертывание приложения

При настройке приложения CM в центре загрузки скачайте файл MIMDMModernApp_&lt;версия&gt;_AnyCPU_Test.zip и извлеките его содержимое. APPX-файл — это установщик. Его можно развернуть так же, как и любое приложение Магазина Windows, используя [System Center Configuration Manager](https://technet.microsoft.com/library/dn613840.aspx)или [Intune](https://technet.microsoft.com/library/dn613839.aspx) для загрузки неопубликованного приложения, чтобы пользователи имели доступ к нему через корпоративный портал либо оно устанавливалось непосредственно на их компьютеры.

## <a name="next-steps"></a>Дальнейшие действия

- [Шаблоны профиля конфигурации](https://technet.microsoft.com/library/cc708656)
- [Управление приложениями смарт-карты](https://technet.microsoft.com/library/cc708681)