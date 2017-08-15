---
title: "Настройка портала Microsoft Identity Manager 2016 | Документация Майкрософт"
description: 
keywords: 
author: barclayn
ms.author: barclayn
manager: mbaldwin
ms.date: 08/01/2017
ms.topic: reference
ms.prod: identity-manager-2016
ms.service: microsoft-identity-manager
ms.technology: security
ms.assetid: 
ms.openlocfilehash: bebb299ece077a6ab2e0d75f3b30ad1776678303
ms.sourcegitcommit: 5ba5d916c0ca1e5aa501592af0cef714bfdc8afe
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/02/2017
---
# <a name="microsoft-identity-manager-2016-portal-customization"></a>Настройка портала Microsoft Identity Manager 2016


>[!Warning]
Перед настройкой CSS необходимо очистить кэш браузера.

В Microsoft Identity Manager 2016 (MIM) можно настроить выбранные элементы порталов для работы с паролями, включая баннер с логотипом, строковые ресурсы и каскадные таблицы стилей.

Для этого вам понадобятся несколько компонентов в зависимости от нужной конфигурации. Ниже приведен список этих компонентов, которые используются при настройке портала регистрации и сброса паролей MIM 2016.

-   Папка настроек (Customizations) — это папка, к которой MIM 2016 обращается, прежде чем использовать значения по умолчанию. С каждым настраиваемым порталом должна быть связана соответствующая папка настроек. Настройки должны применяться только в этой папке, так как программа установки не перезаписывает ее при обновлении, а также при установке в режиме изменения или восстановления.

-   Strings.resources — XML-файл, который позволяет изменять строки, отображаемые на портале. Этот файл должен находиться в папке настроек.

-   Style.CSS — это таблицы каскадных стилей, используемые порталами для настройки. Чтобы изменить логотип, эту таблицу стилей можно создать и изменить. Кроме того, ее можно полностью заменить, используя собственные настройки.

Подробные пошаговые инструкции с примером настройки порталов сброса и регистрации паролей MIM 2016 см. в соответствующем руководстве по лаборатории тестирования.

>[!ПРЕДУПРЕЖДЕНИЕ] Чтобы измененные настройки распознавались в MIM, необходимо перезапустить службы IIS, выполнив команду iisreset.


## <a name="creating-the-customizations-folder"></a>Создание папки настроек

Во время запуска MIM будет искать файл Strings.resources в папке настроек, прежде чем использовать значения по умолчанию. Необходимо создать папку настроек в каталоге для настраиваемого портала (т. е. портала регистрации паролей или портала сброса паролей). Чтобы настроить оба портала, вам нужно создать папку в каждом из этих расположений:

-   C:\\Program Files\\Microsoft Forefront Identity Manager\\2010\\Password Registration Portal

-   C:\\Program Files\\Microsoft Forefront Identity Manager\\2010\\Password Reset Portal

### <a name="to-create-the-customization-folder"></a>Создание папки настроек

1.  Перейдите к папке C:\\Program Files\\Microsoft Forefront Identity Manager\\2010\\Password Registration Portal.

2.  Создайте папку с именем "Customizations".

3.  Перейдите на уровень вверх к папке портала сброса паролей (папка "Password Reset Portal") и создайте папку настроек с именем "Customizations".

## <a name="customizing-strings"></a>Настройка строк

Многие строки в пользовательском интерфейсе портала можно настроить, создав файл Strings.resources и добавив этот файл в папку настроек. Вам нужно создать файл Strings.resources для каждого настраиваемого портала.

### <a name="to-customize-strings"></a>Настройка строк

1.  Скопируйте в Блокнот следующий код, а затем сохраните его в папке настроек как файл Strings.resources.

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <root>
     <resheader name="resmimetype">
       <value>text/microsoft-resx</value>
     </resheader>
     <resheader name="version">
       <value>2.0</value>
     </resheader>
     <resheader name="reader">
       <value>System.Resources.ResXResourceReader, System.Windows.Forms, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089</value>
    </resheader>
     <resheader name="writer">
       <value>System.Resources.ResXResourceWriter, System.Windows.Forms, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089</value>
     </resheader>

    <!-- Customizations begin here -->
     <data name=" QAGateResetTitle " xml:space="preserve">
       <value>Contoso Question and Answer Reset</value>
     </data>
     <data name="ResetPageTitle" xml:space="preserve">
       <value>Contoso Self-Service Password Reset</value>
     </data>
   </root>

   ```
2.  В разделе `<!-- Customizations begin here -->` присвойте переменным data name имя настраиваемых строк и введите значение для каждой строки между тегами <value></value>. Ниже приведен список настраиваемых строк и их значения по умолчанию.

>[!NOTE]
Файл **Strings.resources** является универсальным. Чтобы создать настраиваемые строки на определенном языке, установите соответствующий языковой пакет и сохраните файл в формате Strings.`<language>-<culture>.resources`, например Strings.en-us.resources.

Ниже приведен список настраиваемых строк портала.

<a name="portal-strings"></a>Строки портала
--------------

| Имя                                                     | Значение по умолчанию                                                                                                                                                                                                                                                                                                                                         | Примечание                                                                                                                                                                                                                                            |
|---------------------------|-------------------|--------------|
| AboutLinkText                                            | О программе         |       |
| ButtonCancel                                             | Отмена                                                                                 |     |
| ButtonFinish                                             | Готово    |    |
| ButtonNext                                               | Далее    |    |
| ButtonOk                                                 | ОК     |   |
| CancelFinishedMessage                                    | Ваш сеанс уже не активен. Вы можете закрыть окно или перезапустить сеанс, щелкнув ссылку ниже.         |      |
| CancelFinishedTitle                                      | Сеанс завершен                                                              |      |
| ErrorDescription_3000                                    | Произошла ошибка. Повторите попытку, если проблема не устранена, обратитесь в службу технической поддержки или к системному администратору. (Ошибка 3000)       |          |
| ErrorDescription_3001                                    | Убедитесь, что вы правильно ввели имя пользователя. Если по-прежнему не удается сбросить пароль,      |           |
|                                                          | свяжитесь со службой технической поддержки. (Ошибка 3001)   |                   |
| ErrorDescription_3002                                    | Сеанс завершен. Вернитесь на домашнюю страницу, чтобы повторить попытку. (Ошибка 3002)                                     |                |
| ErrorDescription_3003                                    | Текущая учетная запись пользователя не распознается программой Forefront Identity Manager. Свяжитесь со службой технической поддержки или администратором. (Ошибка 3003)           |               |
| ErrorDescription_3004                                    | Вы не имеете права на регистрацию для сброса пароля. Свяжитесь со службой технической поддержки или администратором. (Ошибка 3004)     |              |
| ErrorDescription_3005                                    | Один или несколько ответов не совпадают с ответами, предоставленными во время регистрации пароля. Чтобы сбросить пароль, ответы должны совпадать с ответами, данными при регистрации. Можно повторить попытку с главной страницы или связаться со службой технической поддержки или администратором. (Ошибка 3005) |           |
| ErrorDescription_3006                                    | Вы ввели неправильный пароль. Чтобы зарегистрироваться для сброса пароля, необходимо ввести правильный пароль. (Ошибка 3006)            |              |
| ErrorDescription_3007                                    | Сброс пароля временно запрещен. Повторите попытку позднее или свяжитесь со службой технической поддержки или администратором. (Ошибка 3007)     |         |
| ErrorDescription_3008                                    | Произошла ошибка. Повторите попытку, если проблема не устранена, обратитесь в службу технической поддержки или к системному администратору. (Ошибка 3008)        |          |
| ErrorDescription_3009                                    | Входные данные содержат текст в недопустимом формате. Повторите попытку, используя другие входные данные, либо обратитесь в службу технической поддержки или к системному администратору. (Ошибка 3009)     |             |
| ErrorDescription_3010_Registration                       | В вашем браузере отключены сценарии. Включите сценарии и вернитесь на домашнюю страницу либо обратитесь в службу технической поддержки.      |               |
| ErrorDescription_3010_Reset                              | В вашем браузере отключены сценарии. Включите сценарии и вернитесь на домашнюю страницу "Сброс пароля" либо обратитесь в службу технической поддержки.     |            |
| ErrorDescription_3011                                    | На этом сайте используются файлы cookie. Настройте браузер на прием файлов cookie и повторите попытку либо обратитесь в службу технической поддержки.          |                                           |
| ErrorDescription_3012                                    | Введенные данные не совпали с отправленным вам защитным кодом. Попробуйте сменить пароль еще раз или обратитесь за помощью в службу технической поддержки.      |                                                                                                                                                                                                                                                    |
| ErrorDescription_3013                                    | Не удалось отправить защитный код. Обратитесь за помощью в службу технической поддержки.                                                                                                                                                                                                                                                                         |                                                                                                                                                                                                                                                    |
| ErrorMessageDomainUsernameFormat                         | Введите имя пользователя в правильном формате.                                                                                                                                                                                                                                                                                                           |                                                                                                                                                                                                                                                    |
| ErrorMessageDomainUsernameRequired                       | Введите имя пользователя для продолжения.                                              |                         |
| ErrorMessagePasswordRequired                             | Введите пароль.              |                                                |
| ErrorMessagePasswordsDoNotMatch                          | Убедитесь, что оба пароля совпадают.                                |           |
| ErrorPageDefaultHeading                                  | Ошибка приложения                                            |               |
| ErrorPageServerTime                                      | Серверное время: {0:T}                     | {0} — время, когда было обнаружено исключение. "T" определяет для переданного значения времени полный формат. Это значит, что будут отображаться часы, минуты и секунды и, возможно, обозначение AM/PM (в зависимости от текущего языка и региональных параметров). |
| ErrorPageTitle                                           | Forefront Identity Management — неправильный пароль                     |   |
| ErrorTitle_3000                                          | Ошибка                                  |  |
| ErrorTitle_3001                                          | Отказано в доступе                          |  |
| ErrorTitle_3002                                          | Сеанс завершен                          |  |
| ErrorTitle_3003                                          | Неопознанный пользователь                      |  |
| ErrorTitle_3004                                          | Неавторизованный пользователь                      |  |
| ErrorTitle_3005                                          | Ответы не совпадают                    |  |
| ErrorTitle_3006                                          | Неправильный пароль                     |  |  
| ErrorTitle_3007                                          | В доступе временно отказано              |  |
| ErrorTitle_3008                                          | Ошибка связи                    |  |
| ErrorTitle_3009                                          | Запрещенные входные данные                       |  |
| ErrorTitle_3010                                          | Ошибка конфигурации браузера            |  |
| ErrorTitle_3011                                          | Ошибка конфигурации браузера            |  |
| ErrorTitle_3012                                          | Сбой проверки                    |  |
| ErrorTitle_3013                                          | Не удалось отправить код безопасности   |  |
| FinalizeRegistrationHeading1                             | Для сброса пароля выполните следующие действия:        |   |
| FinalizeRegistrationSubHeading1                          | Перейдите на портал сброса пароля   |   |
| FinalizeRegistrationSubHeading2                          | Подтвердите свое удостоверение   |   |
| FinalizeRegistrationSubHeading3                          | Выберите новый пароль    |     |
| FinishingDescription                                     | Выберите новый пароль        |    |
| FinishingTitle                                           | Сброс пароля:      |     |
| GotoPortalPrefix                                         | Перейдите на     |        |
| GotoPortalPrefix                                         | домашнюю страницу     |      |
| LabelTroubleshootingLinkText                             | Подробности           |    |
| LoadingText                                              | Загрузка...     |  |
| NoScriptTagErrorMessage                                  | В вашем браузере отключены сценарии. Включите сценарии и вернитесь на домашнюю страницу либо обратитесь в службу технической поддержки.      |   |
| PasswordResetOperationGeneralErrorMessage                | Ошибка при попытке сброса пароля.       |   |
| PasswordResetOperationPolicyViolationErrorMessage            | Пароль не соответствует корпоративным политикам паролей.             |       |
| PasswordResetOperationUserCantChangePasswordErrorMessage | Ошибка при сбросе пароля, пользователю запрещено изменять пароль.    |   |
| PrivacyStatement                                         | Заявление о конфиденциальности                                                      |    |
| RegistrationDescription                                  | Самостоятельная регистрация пароля     |    |
| RegistrationMission                                      | Если вы забудете пароль, его можно сбросить самостоятельно, не обращаясь в службу технической поддержки.   |      |
| RegistrationPageTitle                                    | Forefront Identity Management — регистрация пароля                                          |   |
| RegistrationSteps                                        | Нажмите кнопку "Далее", чтобы начать процесс регистрации.   |      |
| RegistrationSuccessDescription                           | Регистрация выполнена        |   |
| RegistrationSuccessTitle                                 | Завершено:   |    |
| RegistrationWelcomeTitle                                 | Регистрация пароля:    | |
| ResetDescription                                         | Самостоятельный сброс пароля  |    |
| ResetEnterNamePrompt                                     | Введите имя пользователя ниже     |     |
| ResetEnterPassword                                       | Введите новый пароль:                                                  |   |
| ResetExample1                                            | contoso\\mmeyers                                                                            |      |
| ResetExample2                                            | mmeyers\@contoso.com     |      |
| ResetExamples                                            | Примеры:  |    |
| ResetPageTitle                                           | Forefront Identity Management — сброс пароля       |     |
| ResetReenterPassword                                     | Повторно введите пароль:    | |
| ResetSuccessDescription                                  | Ваш пароль сброшен    |    |
| ResetSuccessTitle                                        | «Успех»                                |    |
| ResetUseNewPassword                                      | Теперь можно использовать новый пароль для входа.     |      |
| ResetUsernameTextFormat                                  | (Сброс пароля для {0})       | {0} — это имя пользователя для входа             |
| ResetWelcomeTitle                                        | Сброс пароля:     |      |
| TroubleshootingEmailSubject                              | Сведения об ошибке обработки запроса FIM     |       |
| TroubleshootingLabelAttributes                           | Атрибуты:    |    |
| TroubleshootingLabelCloseButton                          | Закрыть       |    |
| TroubleshootingLabelCopyToClipboard                      | Скопировать в буфер обмена     |     |
| TroubleshootingLabelCorrelationId                        | Идентификатор корреляции:      |          |
| TroubleshootingLabelDetails                              | Подробные сведения:                                                             |    |
| TroubleshootingLabelPostCopyClipboardMessage             | Информация скопирована в буфер обмена.           |    |
| TroubleshootingLabelRequestId                            | Идентификатор запроса:                  |    |
| TroubleshootingLabelSendEmail                            | Отправить информацию по электронной почте                            |    |
| TroubleshootingLabelSource                               | Причина:                                                                     |    |
| TroubleshootingLabelViewRequestDetails                   | Просмотр сведений о запросе        |              |                                                    
| TroubleshootingLinkText                                  | Сведения об устранении неполадок          |                  | |



Ниже приведен список настраиваемых строк шлюза аутентификации.

<a name="authentication-gate-strings"></a>Строки шлюза аутентификации
---------------------------

| Имя                                          | Значение по умолчанию                                                                                                                                                                                                                | Комментарий |
|-----------|--------------|----------|
| OTPEmailRegistraionEmailTextboxLabel          | Адрес электронной почты:             |          |
| OTPEmailRegistrationEmailRequiredErrorMessage | Поле адреса электронной почты не может быть пустым.     |          |
| OTPEmailRegistrationFooterReadOnly            | Чтобы обновить свой адрес электронной почты, следуйте процедуре, утвержденной в вашей организации, или обратитесь в службу технической поддержки.                   |          |
| OTPEmailRegistrationFooterReadWrite           | Ваша организация хранит адрес электронной почты в Forefront Identity Manager.                       |          |
| OTPEmailRegistrationGateTitle                 | Проверка адреса электронной почты   |          |
| OTPEmailRegistrationHeaderReadOnly            | Если вам когда-либо потребуется выполнить сброс пароля, на ваш адрес электронной почты будет отправлен защитный код проверки. Если ниже указан неправильный адрес электронной почты, необходимо обновить его для использования самостоятельного сброса пароля. |          |
| OTPEmailRegistrationHeaderReadWrite           | Введите адрес электронной почты в расположенном ниже поле. Если вам когда-либо потребуется выполнить сброс пароля, на ваш адрес электронной почты будет отправлен защитный код проверки.                 |          |
| OTPEmailResetGateTitle                        | Подтвердите свое удостоверение: проверка по электронной почте         |          |
| OTPEmailResetHeader                           | Введите защитный код в расположенном ниже поле. Защитный код был отправлен на адрес электронной почты, зарегистрированный для данной организации.                                                                                                             |          |
| OTPRegularExpressionErrorMessage              | Указанное значение не соответствует ожидаемому формату.                   |          |
| OTPResetOneTimePasswordRequiredErrorMessage   | Поле защитного кода не может быть пустым.        |          |
| OTPResetVerificationLabel                     | Защитный код:                    |          |
| OTPSmsRegistrationFooterReadOnly                      | Чтобы обновить свой номер мобильного телефона, следуйте процедуре, утвержденной в вашей организации, или обратитесь в службу технической поддержки.   ||
| OTPSmsRegistrationFooterReadWrite                     | Ваша организация хранит номер мобильного телефона в Forefront Identity Manager.                                                                                                                                                     |   |
| OTPSmsRegistrationGateTitle                           | Проверка мобильного телефона                      |   |
| OTPSmsRegistrationHeaderReadOnly                      | Если вам когда-либо потребуется выполнить сброс пароля, на ваш мобильный телефон будет отправлен защитный код проверки. Если ниже указан неправильный номер мобильного телефона, необходимо обновить его для использования самостоятельного сброса пароля. |   |
| OTPSmsRegistrationHeaderReadWrite                     | Введите свой номер мобильного телефона в приведенном ниже поле. Если вам когда-либо потребуется выполнить сброс пароля, на ваш мобильный телефон будет отправлен код проверки.                                                                                                     |   |
| OTPSmsRegistrationMobilePhoneRequiredErrorMessage     | Поле номера мобильного телефона не может быть пустым.      |   |
| OTPSmsRegistrationSMSTextBoxLabel                     | Мобильный телефон:                    |   |
| OTPSmsResetGateTitle                                  | Подтвердите свое удостоверение: проверка по мобильному телефону         |   |
| OTPSmsResetHeader                                     | Введите защитный код в расположенном ниже поле. Защитный код был отправлен на мобильный телефон, зарегистрированный для данной организации.                                                                                                                           |   |
| PasswordGateDescriptionText                           | Введите ниже текущий пароль и нажмите кнопку "Далее".        |   |
| PasswordGateErrorMessagePasswordRequired              | Введите текущий пароль.                  |   |
| PasswordGateGateTitle                                 | Текущий пароль               |   |
| PasswordGatePasswordLabelText                         | Пароль                 |   |
| PasswordGateUsernameTextFormat                        | `<i>`(Имя, под которым вы вошли: `<b>{0}</b>)</i>`                                                          |   |
| QAGateErrorNotEnoughQuestionsAnswered                 | Минимальное количество вопросов, на которые нужно ответить — {0}.        |   |
| QAGateIncorrectAnswer                                 | Ответы неправильные.       |   |
| QAGatePrivacyNotice                                   | Ваши ответы сохраняются вашей организацией в диспетчере Forefront Identity Manager.                                                                                                                                                  |   |
| QAGateRegistrationNumberOfQuestionsExplanation_Format | Минимальное количество вопросов, на которые нужно ответить для регистрации — {0}.     |   |
| QAGateRegistrationOneOrMoreAnswersFailedValidation    | Один или несколько ответов не соответствуют политике.      |   |
| QAGateRegistrationThisAnswerValidationFailed          | Этот ответ не соответствует политике.      |   |
| QAGateRegistrationTitle                               | Зарегистрировать ответы         |   |
| QAGateResetNumberOfQuestionsExplanation_Format        | Необходимо ответить на {0} из {1} вопросов.   |   |
| QAGateResetTitle                                      | Проверка удостоверения: отправьте ответы.                                  |   |



## <a name="customizing-the-logo-banner"></a>Настройка баннера с логотипом

Вы можете настроить стандартный баннер на страницах портала для своей организации.
Настройка баннера с логотипом

1.  Вы можете создать собственный баннер и сохранить его как PNG-файл. Файл должен отвечать следующим требованиям:

 - Размер: 490 x 50 пикселей.

 - Битовая глубина: 32.

2.  Скопируйте файл в папку \\Customizations для каждого настраиваемого портала.

3.  Создайте файл Style.css в каждой папке. Свяжите его с папкой настроек и новым логотипом. Возможно, вы захотите изменить имя логотипа (например, /Customizations/contosologo.png). Код будет выглядеть так:

   **Пример 1**

  `.title-block{background:url(../Customizations/fimlogo.png) no-repeat scroll 0 0 transparent;}`

4.  Если вы используете Internet Explorer 6.0, предоставьте альтернативный непрозрачный логотип и добавить следующий код в файл Style.css:

  `.ie6 .title-block{background-image:url(../Customizations/fimlogo-ie6.png);}`

  **Пример 2.**

  `.title-block{background:url(../Customizations/contosologo.png) no-repeat scroll 0 0 transparent;}`

Если вы используете Internet Explorer 6.0, предоставьте альтернативный непрозрачный логотип и добавить следующий код в файл Style.css:

  `.ie6 .title-block{background-image:url(../Customizations/contosologo-ie6.png);}`

## <a name="customizing-image-for-smartphones"></a>Настройка изображений для смартфонов

Вы можете настроить изображение для смартфона. Это можно сделать так:

1.  Создайте собственное изображение и сохраните его как PNG-файл. Файл должен отвечать следующим требованиям:

    - Размер: 190 x 50 пикселей.
    - Битовая глубина: 32.

2.  Скопируйте файл в папку \\Customizations для каждого настраиваемого портала.

2.  Создайте файл Style.css в каждой папке. Свяжите его с папкой настроек и новым логотипом. Возможно, вы захотите изменить имя логотипа (например, /Customizations/contosologo.png). Код будет выглядеть так:

  **Пример 1**

```css
@media only screen and (max-width: 480px)

   {

    .title-block

     {
       background: url("path_to_image/imagename.png") no-repeat scroll 0 0 transparent;
     }

   }
   ```

## <a name="customizing-style-sheets"></a>Настройка таблиц стилей

Вы можете изменить макет и стиль порталов сброса паролей с помощью настраиваемой таблицы каскадных стилей (CSS). Вот как использовать настраиваемые таблицы CSS:

1.  Создайте настроенный CSS-файл и сохраните его как Style.css.

2.  Скопируйте файл в папку \\Customizations для каждого настраиваемого портала.

Ниже приведен простой пример файла Style.css:

```css
body
{
  font: 15px Algerian;
  color: \#303030;
  background: white;
}

.pad
{
  padding: 30px;
  padding-top: 50px;
  background: white;
}

.backgroundWhite
{
  border: \#e9e9e9 2px solid;
} .
title-block
{
background:url(../Customizations/contosologo.png) no-repeat scroll 0 0 transparent;
}
```


>[!IMPORTANT]
Чтобы измененные настройки распознавались в MIM, необходимо перезапустить службы IIS, выполнив команду iisreset.                                                                                                                                                                                       

Ниже приведен более сложный пример файла Style.css: Этот файл предоставляет определенные сведения для отображения порталов на смартфонах и устройствах iРad.

```css
/****************
BASE
*****************/

body {
    font-size: 14px; /*Customizeable- Body Font Size */
    background-color: #ced5ec; /*Customizeable- Backgound Color behind the product */
}

body, button, input, select, textarea {
    font-family: Segoe UI, Arial, Verdana, Sans-Serif, Helvetica; /*Customizeable- Body Font Family */
    color: #595959; /*Customizeable- Body Font Color */
}

/****************
LINKS
*****************/

a { color: #396faf; text-decoration: none; } /*Customizeable- Link Color and Underline */
a:visited { color: #396faf; text-decoration: none; } /*Customizeable- After Link is clicked color and underline */
a:hover { color: #6486ae; text-decoration: none; } /*Customizeable- Hover mouse over Link color and underline */
a:focus { outline: thin dotted; } /*Customizeable- Keyboard event to Link and Link is in focus outline*/
a:hover, a:active { outline: 0; } /*Customizeable- Hover and Active Link outline */

/****************
Typography
*****************/

hr { border-top: 1px solid #acd9ec; } /*Customizeable- Horizontal Rule Color Above the Footer */

/****************
Layout
*****************/
#wrapper {
    background: url(../images/bg-top-slice.png) repeat-x 0 0; /*Customizeable-remove this line to remove top gradient */
}

#container {
    background: url(../images/bg-bottom-slice.png) repeat-x 100% 100% transparent;  /*Customizeable-remove this line to remove bottom gradient */
}

.title-block {
    background: url("../images/fimlogo.png") no-repeat scroll 0 0 transparent;  /*Customizeable- Logo must be 600px or less in width. Logo must be 50px or less in height. */
    border-bottom: 2px solid #acd9ec;/*Customizeable- 2px border color under logo */
}

.ie6 .title-block {
    background-image: url(../images/fimlogo-ie6.png);   /*Customizeable- Can make a non-transparent image for IE6 only */
}

h2 {
    color: #578e4c; /*Customizeable- h2 page header color */
}

h3 {
    color: #999; /*Customizeable- h3 page header color */
}

input[type=text]:focus, input[type=password]:focus {
    border: #82bd3b 2px solid; /*Customizeable- Highlight color around textbox when cursor is inside */
}

.chromeButton, .chromeButton:visited {
    background-color: #333; /*Customizeable- Color of button */
    color: #fff; /*Customizeable- Color of text on the button */
    border: 1px solid #666; /*Customizeable- Border color of button */
}

.chromeButton:hover {
    background-color: #666; /*Customizeable- Hover color of button */
    border: 1px solid #999; /*Customizeable- Hover border color of button */
}

.qcol /*Style from QAgate.css */ {
    color: #7a7a7a; /*Customizeable- Font color of Q&A container */
    background-color:#e6e7e9; /*Customizeable- Background color of Q&A container */
}

/****************
Media Queries
*****************/

/* Smartphones ----------- */
@media only screen and (max-width: 480px) {
    body {
        font-size:12px; /*Customizeable- Body Font Size for devices */
    }

    .title-block {
        background: url("../images/fim-logo-portrait.png") no-repeat scroll 0 0 transparent;  /*Customizeable- Logo must be 190px (landscape) or less in width. Logo must be 50px or less in height. */
    }
    h2, h3 {
        font-size:14px; /*Customizeable- H2 and H3 Heading Size for devices */
    }
}


/* iPads (landscape) ----------- */
@media only screen and (min-device-width : 768px) and
(max-device-width : 1024px) and
(orientation : landscape)
{
}

/* iPads (portrait) ----------- */
@media only screen and (min-device-width : 768px) and
(max-device-width : 1024px) and
(orientation : portrait)
{
}
```


## <a name="common-customization-issues"></a>Распространенные проблемы с настройкой

Ниже приведен список известных проблем, которые могут возникнуть при обновлении службы FIM и портала. Эта таблица также содержит описание решений этих проблем.

|Проблема |Разрешение                                                                    |
|------|------------------------------|
| Строки настроены, но в пользовательском интерфейсе этого не видно         | После настройки строк в файле Strings.resources нужно выполнить команду iisreset.         |
| После внесения изменений в файл Strings.resources изменения в строках не отображаются     | Формат файла Strings.resources, скорее всего, поврежден, и поэтому портал его не распознает. Проверьте журнал событий в следующем расположении: "Журналы Windows" > "Журналы приложения и служб" > "Forefront Identity Manager".                        |
| При первом добавлении файла Style.css изменения стиля на портале не отобразились            | При первом использовании файла Style.css нужно выполнить команду iisreset.     |
| В файле Style.css добавлены или изменены новые стили, но изменения не видны в браузере      | Очистите кэш браузера и обновите страницу. <br/> Проверьте синтаксис CSS.    |
| После изменения содержимого папки CSS в расположении путь_к_порталу_самостоятельного_сброса_пароля\\css\\\*.css или баннера с логотипом в расположении путь_к_порталу_самостоятельного_сброса_пароля\\images\\fimlogo.png изменения были утеряны при обновлении. | Никогда не изменяйте эти файлы. Для внесения изменений в баннер с логотипом и стили CSS в файл Style.css используйте только папку настроек (папка "Customizations"). Эта папка намеренно не перезаписывается при основных обновлениях. <br/><br/>Не пытайтесь использовать такие средства, как ILSpy и Reflector, чтобы изменить строки в сборках портала. Используйте файл Strings.resources, чтобы переопределить строки по умолчанию. Сборки будут заменены при обновлении.  |
| Баннер с логотипом отображается на порталах либо все еще отображается логотип FIM     | Имя или путь к изображению в файле Style.css являются недопустимыми или кэш браузера не был очищен.          |
| Баннер с логотипом выглядит плохо в IE6       | Вам нужно предоставить непрозрачное изображение для IE6, а также добавить специальный сопутствующий стиль в файл Style.css.        |
