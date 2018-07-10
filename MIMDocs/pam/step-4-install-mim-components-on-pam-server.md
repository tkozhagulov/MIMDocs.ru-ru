---
title: Развертывание PAM. Шаг 4 — установка MIM | Документация Майкрософт
description: Установите и настройте службу и портал MIM на сервере и рабочих станциях Privileged Access Management.
keywords: ''
author: barclayn
ms.author: barclayn
manager: barclayn
ms.date: 09/13/2017
ms.topic: article
ms.service: microsoft-identity-manager
ms.technology: active-directory-domain-services
ms.assetid: ef605496-7ed7-40f4-9475-5e4db4857b4f
ROBOTS: noindex,nofollow
ms.reviewer: mwahl
ms.suite: ems
ms.openlocfilehash: 81fe10b8fbf8ada08983c4bf3c58f85215cf1d66
ms.sourcegitcommit: 35f2989dc007336422c58a6a94e304fa84d1bcb6
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/20/2018
ms.locfileid: "36290039"
---
# <a name="step-4--install-mim-components-on-pam-server-and-workstation"></a>Шаг 4. Установка компонентов MIM на сервере и рабочей станции PAM

> [!div class="step-by-step"]
> [« Шаг 3](step-3-prepare-pam-server.md)
> [Шаг 5 »](step-5-establish-trust-between-priv-corp-forests.md)

Войдите в PAMSRV от имени PRIV\Administrator, чтобы установить службу и портал MIM и пример веб-приложения портала.

  > [!NOTE]
  > Необходимо быть администратором домена; если запустить следующие команды без прав администратора домена, проверки доверия на следующем шаге пройдены не будут.

Если вы скачали MIM, распакуйте архив установки MIM в новую папку.

## <a name="run-the-service-and-portal-install-program"></a>Запустите программу установки службы и портала.

Следуйте инструкциям и завершите установку.

1. При выборе компонентов необходимо включить службу MIM (с управлением привилегированным доступом, но без службы отчетов MIM) и портал MIM.  

   ![Выборочная установка — снимок экрана](./media/PAM_GS_MIM_2015_Service_Portal.png)

2. При настройке общих служб и подключения к базе данных MIM выберите параметр **Создать новую базу данных**.

   > [!NOTE]
   > Если для обеспечения высокой доступности служба устанавливается несколько раз, установите флажок **Использовать существующую базу данных** для всех последующих установок.

3. При настройке подключения к почтовому серверу задайте в качестве почтового сервера имя узла сервера Exchange или SMTP для среды CORP (если у вас нет почтового сервера, используйте значение corpdc.contoso.local) и снимите флажки **Использовать SSL** и **Почтовый сервер — Exchange Server 2007 или Exchange Server 2010**.

4. Укажите, что необходимо создать самозаверяющий сертификат.

5. Задайте следующие учетные данные:
   - Имя учетной записи службы: *MIMService*  
   - Пароль учетной записи службы: <em>Pass@word1</em> (или пароль, созданный на шаге 2)  
   - Домен учетной записи службы: *PRIV*  
   - Учетная запись электронной почты: <em>MIMService@priv.contoso.local</em>  

6. Примите значения по умолчанию для имени узла сервера синхронизации и укажите учетную запись агента управления MIM *PRIV\MIMMA*. Появится предупреждение об отсутствии службы синхронизации MIM. Это нормально, поскольку служба синхронизации MIM не используется в этом сценарии.

7. Укажите *PAMSRV* в качестве адреса сервера службы MIM.

8. Задайте *http://pamsrv.priv.contoso.local:82* как URL-адрес коллекции сайтов SharePoint.

9. Оставьте URL-адрес портала регистрации пустым.

10. Установите флажки, чтобы открыть порты 5725 и 5726 в брандмауэре и предоставлять всем вошедшим пользователям доступ к сайту портала MIM.

11. Оставьте имя узла PAM REST API пустым и укажите *8086* в качестве номера порта.

    ![Сведения о привязке для API REST PAM — снимок экрана](./media/PAM_GS_MIM_2015_Service_Portal_configure_application_pool.png)

12. Настройка учетной записи API REST PAM MIM для использования той же учетной записи в качестве SharePoint (поскольку портал MIM также размещается на этом сервере):
    - Имя учетной записи пула приложений: *SharePoint*  
    - Пароль учетной записи пула приложений: <em>Pass@word1</em> (или пароль, созданный на шаге 2)  
    - Домен учетной записи пула приложений: *PRIV*  

    ![Учетные данные учетной записи пула приложений — снимок экрана](./media/PAM_GS_Configure_Component_Service.png)

    Может появиться предупреждение о небезопасности учетной записи службы в текущей конфигурации. Это нормально.

13. Настройте службу компонента MIM PAM:
    - Имя учетной записи службы — *MIMComponent*
    - Пароль учетной записи службы: <em>Pass@word1</em> (или пароль, созданный на шаге 2)  
    - Домен учетной записи службы: *PRIV*

    ![Учетные данные учетной записи службы компонента PAM — снимок экрана](./media/PAM_GS_Configure_MIM_PAM_component_service.png)

14. Настройте службу мониторинга PAM:
    - Имя учетной записи службы — *MIMMonitor*  
    - Пароль учетной записи службы: <em>Pass@word1</em> (или пароль, созданный на шаге 2)  
    - Домен учетной записи службы: *PRIV*  

    ![Учетные данные учетной записи службы мониторинга PAM — снимок экрана](./media/PAM_GS_Configur_PAM_Monitoring_service.png)

15. На странице "Введите данные для порталов паролей MIM" не устанавливайте никаких флажков. Нажмите кнопку **Далее**, чтобы продолжить установку.

После завершения установки сервер перезагрузится, затем убедитесь, что портал MIM активен, и разрешите пользователям просматривать собственный ресурс объекта в MIM.

## <a name="set-up-mim-portal-management-policy-rules"></a>Настройка правил политики управления для портала MIM

1. После перезагрузки PAMSRV войдите в систему от имени PRIV\Administrator.

2. Запустите Internet Explorer и перейдите на портал MIM по адресу http://pamsrv.priv.contoso.local:82/identitymanagement. Первое обнаружение этой страницы может потребовать некоторого времени.

3. При необходимости войдите в Internet Explorer от имени PRIV\Administrator.

4. В Internet Explorer откройте **Свойства обозревателя**, перейдите на вкладку **Безопасность** и добавьте узел в зону **Местная интрасеть**, если его еще там нет. Закройте диалоговое окно "Свойства обозревателя".

5. В Internet Explorer на портале MIM щелкните **Правила политики управления**.

6. Найдите правило политики управления **Управление пользователями: пользователи могут читать собственные атрибуты**.

7. Выберите это правило политики управления, снимите флажок **Политика отключена**, нажмите кнопку **ОК**, а затем **Отправить**.

## <a name="verify-the-firewall-connections"></a>Проверка подключений брандмауэра

Брандмауэр должен разрешать входящие подключения к TCP-портам 5725, 5726, 8086 и 8090.

1.  Запустите **брандмауэр Windows в режиме повышенной безопасности** (в папке "Администрирование").  
2.  Выберите **Правила для входящих подключений**.  
3.  Убедитесь, что указаны эти два правила:  
    - Forefront Identity Manager Service (STS)
    - Forefront Identity Manager Service (Webservice)  
4.  Выберите **Новое правило** > **Порт** > **TCP** и введите локальные порты *8086* и *8090*. Примите значения мастера по умолчанию, введите имя правила и нажмите кнопку **Готово**.  
5.  После завершения работы мастера закройте приложение брандмауэра Windows.

6.  Запустите **панель управления**.  
7.  Выберите **Просмотр состояния сети и задач** в разделе "Сеть и Интернет".  
8.  Убедитесь, что в списке присутствует активная сеть priv.contoso.local и доменная сеть.  
9. Закройте **панель управления**.

## <a name="set-up-the-sample-web-application"></a>Настройка примера веб-приложения

В этом разделе описывается установка и настройка примера веб-приложения для API REST PAM MIM.

1. Загрузите ZIP-файл [Примеры управления удостоверениями](https://github.com/Azure/identity-management-samples) из архива примеров веб-приложений.

2. Распакуйте содержимое папки **identity-management-samples-master\Privileged-Access-Management-Portal\src** в новую папку **C:\Program Files\Microsoft Forefront Identity Manager\2010\Privileged Access Management Portal**.

3. Создайте в IIS новый веб-сайт с именем "Пример портала MIM Privileged Access Management", физическим путем C:\Program Files\Microsoft Forefront Identity Manager\2010\Privileged Access Management Portal и портом 8090.  Это можно сделать с помощью следующей команды PowerShell:

   ```PowerShell
   New-WebSite -Name "MIM Privileged Access Management Example Portal" -Port 8090   -PhysicalPath "C:\Program Files\Microsoft Forefront Identity Manager\2010\Privileged Access Management Portal\"
   ```

4. Настройте пример веб-приложения, включив перенаправление пользователей в API REST PAM MIM. В текстовом редакторе, например в Блокноте, измените файл **C:\Program Files\Microsoft Forefront Identity Manager\2010\Privileged Access Management REST API\web.config**. В разделе **<system.webServer>** добавьте следующие строки:

   ```XML
   <httpProtocol>
   <customHeaders>
     <add name="Access-Control-Allow-Credentials" value="true"  />
     <add name="Access-Control-Allow-Headers" value="content-type" />
     <add name="Access-Control-Allow-Origin" value="http://pamsrv:8090" />  
   </customHeaders>
   </httpProtocol>
   ```

5. Настройте пример веб-приложения. В текстовом редакторе, например в Блокноте, измените файл **C:\Program Files\Microsoft Forefront Identity Manager\2010\Privileged Access Management Portal\js\utils.js**. Задайте для **pamRespApiUrl** значение *http://pamsrv.priv.contoso.local:8086/api/pamresources/*.

6. Чтобы изменения вступили в силу, перезапустите IIS, выполните следующую команду:

   ```cmd
   iisreset
   ```

7. Убедитесь, что пользователь может пройти проверку подлинности REST API (необязательно). Откройте веб-браузер с правами администратора на сервере PAMSRV.  Перейдите по URL-адресу http://pamsrv.priv.contoso.local:8086/api/pamresources/pamroles/ веб-сайта, при необходимости выполните аутентификацию и убедитесь, что скачивание происходит.

## <a name="install-the-mim-pam-requestor-cmdlets"></a>Установка командлетов запрашивающей стороны MIM PAM

Установите командлеты запрашивающей стороны MIM PAM на рабочей станции, настроенной на шаге 1.

1.  Войдите в CORPWKSTN с правами администратора.

2.  Загрузите **Надстройки и расширения** на компьютер CORPWKSTN, если их там еще нет.

3.  Распакуйте архив **Надстройки и расширения** в новую папку.

4.  Запустите установщик **setup.exe**.

5.  В окне выборочной установки выберите **клиент PAM** (**надстройку MIM для Outlook** и **расширения "Пароль MIM" и "Проверка подлинности"** выбирать не надо).

6.  В окне "Адрес сервера PAM" в качестве имени узла сервера PRIV MIM укажите *pamsrv.priv.contoso.local*.

После завершения установки перезапустите CORPWKSTN для завершения регистрации нового модуля PowerShell.

На следующем шаге описывается установка отношений доверия между лесами PRIV и CORP.

> [!div class="step-by-step"]
> [« Шаг 3](step-3-prepare-pam-server.md)
> [Шаг 5 »](step-5-establish-trust-between-priv-corp-forests.md)
