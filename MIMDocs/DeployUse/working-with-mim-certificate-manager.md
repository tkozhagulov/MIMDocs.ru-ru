---
title: "Диспетчер сертификатов MIM | Документация Майкрософт"
description: "Узнайте, как развернуть приложение диспетчера сертификатов, чтобы позволить пользователям управлять своими правами доступа."
keywords: 
author: kgremban
ms.author: kgremban
manager: femila
ms.date: 07/21/2016
ms.topic: article
ms.service: microsoft-identity-manager
ms.technology: security
ms.assetid: 66060045-d0be-4874-914b-5926fd924ede
ms.reviewer: mwahl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 1f545bfb2da0f65c335e37fb9de9c9522bf57f25
ms.openlocfilehash: a2be6b5640dde5e2908dce36ea13d920a6643874


---

# <a name="working-with-the-mim-certificate-manager"></a>Работа с диспетчером сертификатов MIM
После того как MIM 2016 и диспетчер сертификатов запущены и работают, вы можете развернуть приложение диспетчера сертификатов MIM из Магазина Windows, чтобы пользователи могли легко управлять физическими и виртуальными смарт-картами, а также сертификатами программного обеспечения. Чтобы развернуть приложение MIM CM, необходимо выполнить следующие действия:

1.  создать шаблон сертификата;

2.  создать шаблон профиля;

3.  подготовить приложение;

4.  развернуть приложение через SCCM или Intune.

## <a name="create-a-certificate-template"></a>Создание шаблона сертификата
Шаблон сертификата для приложения CM создается как и обычно, за исключением того, что необходимо убедиться, что используется шаблон сертификата версии 3 или более поздней.

1.  Войдите на сервер под управлением AD CS (сервер сертификатов).

2.  Откройте консоль MMC.

3.  Щелкните **Файл &gt; Добавить или удалить оснастку**.

4.  В списке доступных оснасток выберите **Шаблоны сертификатов**, а затем нажмите кнопку **Добавить**.

5.  В консоли MMC в разделе **корень консоли** вы увидите раздел **Шаблоны сертификатов** . Дважды щелкните его, чтобы увидеть все доступные шаблоны сертификатов.

6.  Щелкните правой кнопкой мыши шаблон **Вход со смарт-картой** и выберите команду **Скопировать шаблон**.

7.  На вкладке "Совместимость" в разделе "Центр сертификации" выберите Windows Server 2008, а в разделе "Получатель сертификата" — Windows 8.1 или Windows Server 2012 R2.
    Этот ключевой шаг, поскольку на нем проверяется версия шаблона сертификата (необходима версия 3 или более поздняя), так как только версия 3 работает с приложением диспетчера сертификатов. Поскольку версия устанавливается при первоначальном создании и сохранении шаблона сертификата, если вам не удалось создать шаблон сертификата таким образом, невозможно изменить его версию на правильную. Поэтому следует создать новый сертификат.

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

2.  Выберите "Администрирование &gt; Управлять шаблонами профилей" и убедитесь, что установлен флажок "Шаблон профиля входа примера смарт-карты MIM CM", а затем выберите "Копировать выбранный профиль шаблона".

3.  Введите имя профиля шаблона и нажмите кнопку **ОК**.

4.  На следующем экране выберите **Добавить новый шаблон сертификата** и установите флажок рядом с именем ЦС.

5.  Установите флажок рядом с именем профиля шаблона **Вход** и нажмите кнопку **Добавить**.

6.  Удалите шаблон SmartCardLogon. Для этого установите рядом с ним флажок и нажмите кнопку **Удалить выбранные шаблоны сертификатов** , а затем **ОК**.

7.  Прокрутите вниз и нажмите кнопку **Изменить параметры**.

8.  Установите флажки **Create/Destroy virtual smart card** (Создать и удалить виртуальную смарт-карту) и **Diversify Admin Key** (Диверсифицировать ключ администратора).

9. В разделе **Политика ПИН-кода пользователя** выберите **Предоставляется пользователем**.

10. В левой области щелкните **Обновить политику &gt; Изменить общие параметры**. Выберите параметр **Повторно использовать карту при обновлении** и нажмите кнопку **ОК**.

11. Отключите сбор данных для каждой политики. Для этого выберите политику в области слева и снимите флажок **Пример элемента данных** , а затем нажмите кнопку **Удалить элементы сбора данных**. После этого щелкните **OK**.

## <a name="prepare-the-cm-app-for-deployment"></a>Подготовка к развертыванию приложения CM

1.  В командной строке выполните следующую команду, чтобы распаковать приложение и извлечь содержимое в новую вложенную папку с именем appx, а также создать копию, чтобы не изменить исходный файл.

    ```
    makeappx unpack /l /p <app package name>.appx /d ./appx
    ren <app package name>.appx <app package name>.appx.original
    cd appx
    ```

2.  В папке appx переименуйте файл с именем CustomDataExample.xml на Custom.data

3.  Откройте файл Custom.data и при необходимости измените параметры.

    |||
    |-|-|
    |URL-адрес MIM CM|Полное доменное имя портала, которое использовалось для настройки CM. Например: https://mimcmServerAddress/certificatemanagement|
    |URL-адрес ADFS|Если вы используете службы AD FS, укажите URL-адрес AD FS. Например: https://adfsServerSame/adfs|
    |PrivacyUrl|Вы можете указать URL-адрес веб-страницы, на которой описывается, что вы будете делать с данными пользователя, полученными для регистрации сертификата.|
    |SupportMail|Можно указать электронный адрес службы поддержки.|
    |LobComplianceEnable|Этому параметру можно задать значение true или false. Значение по умолчанию — true.|
    |MinimumPinLength|Значение по умолчанию — 6.|
    |NonAdmin|Этому параметру можно задать значение true или false. Значение по умолчанию — false. Это значение следует изменить, только чтобы пользователи, не являющиеся администраторами на своих компьютерах, могли регистрировать и обновлять сертификаты.|

4.  Сохраните файл и закройте редактор.

5.  После подписи пакета создается файл подписи, поэтому нужно удалить исходный файл с именем AppxSignature.p7x.

6.  Файл AppxManifest.xml задает имя субъекта сертификата подписи. Откройте его для редактирования.

7.  Перед началом изучения этого раздела вам необходимо получить сертификат подписи. См. раздел "Включение обновления смарт-карты для администраторов в диспетчере сертификатов MIM 2016", шаг 1 ниже.

8.  В элементе &lt;Identity&gt; присвойте атрибуту Publisher значение, совпадающее с субъектом, указанным в сертификате подписи, например "CN=SUBJECT".

9. Сохраните файл и закройте редактор.

10. В командной строке выполните следующую команду, чтобы повторно упаковать и подписать APPX-файл.

    ```
    cd ..
    makeappx pack /l /d .\appx /p <app package name>.appx
    ```
    где имя пакета приложения — это то же имя, которое использовалось при создании копии.

    ```
    signtool sign /f <path\>mysign.pfx /p <pfx password> /fd "sha256" <app package name>.ap
    px
    ```
    Так будет создан новый APPX-файл. PFXf-файл предоставляет расположение для сертификата подписи и пароль для PFX-файла.

11. Для работы с проверкой подлинности AD FS:

    -   Откройте приложение Virtual Smart Card. Это упрощает поиск значений, необходимых для следующего шага.

    -   На сервере AD FS откройте Windows PowerShell и выполните команду `ConfigureMimCMClientAndRelyingParty.ps1 –redirectUri <redirectUriString> -serverFQDN <MimCmServerFQDN>`, чтобы добавить приложение в качестве клиента на сервер AD FS и настроить CM на сервере.

        Ниже приведен скрипт ConfigureMimCMClientAndRelyingParty.ps1:

        ```
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

    -   Обновите значения параметров redirectUri и serverFQDN.

    -   Чтобы найти redirectUri, в приложении Virtual Smart Card откройте панель параметров приложения, нажмите кнопку **Параметры**. URI перенаправления должен быть указан в адресной строке сервера AD FS. URI отображается, только если настроен адрес сервера AD FS.

    -   serverFQDN — это полное имя компьютера сервера MIMCM.

    -   Для получения справки по скрипту **ConfigureMIimCMClientAndRelyingParty.ps1** выполните команду `get-help  -detailed ConfigureMimCMClientAndRelyingParty.ps1`.

## <a name="deploy-the-app"></a>Развертывание приложения
При настройке приложения CM в центре загрузки скачайте файл MIMDMModernApp_&lt;версия&gt;_AnyCPU_Test.zip и извлеките его содержимое. APPX-файл — это установщик. Его можно развернуть так же, как и любое приложение Магазина Windows, используя [System Center Configuration Manager](https://technet.microsoft.com/library/dn613840.aspx)или [Intune](https://technet.microsoft.com/library/dn613839.aspx) для загрузки неопубликованного приложения, чтобы пользователи имели доступ к нему через корпоративный портал либо оно устанавливалось непосредственно на их компьютеры.



<!--HONumber=Nov16_HO2-->


