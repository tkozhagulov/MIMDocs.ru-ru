---
title: "Пошаговое руководство по регистрации с примером | Документация Майкрософт"
description: 
keywords: 
author: msmbaldwin
ms.author: mbaldwin
manager: mbaldwin
ms.date: 10/17/2016
ms.topic: article
ms.prod: identity-manager-2015
ms.service: microsoft-identity-manager
ms.technology: security
ms.assetid: 92b97803-9475-4b90-9a6c-430f107a167d
audience: developer
ms.reviewer: mwahl
ms.suite: ems
ms.openlocfilehash: 574a4d6fc2d5d4a51483a371cf96c2d48c582a8b
ms.sourcegitcommit: 02fb1274ae0dc11288f8bd9cd4799af144b8feae
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/13/2017
---
# <a name="sample-enrollment-walkthrough"></a>Пошаговое руководство по примеру регистрации
В этой статье дана инструкция для самостоятельной регистрации виртуальной смарт-карты. Здесь показан самозаверяющий запрос с PIN-кодом, который задает пользователь.
1.  Клиент выполняет проверку подлинности пользователя, а затем запрашивает список шаблонов профилей, который может зарегистрировать пользователь, прошедший проверку подлинности:

    ```
    GET /CertificateManagement/api/v1.0/profiletemplates.
    ```
    <br/>
2.  Клиент показывает полученный список пользователю. Пользователь выбирает шаблон профиля "vSC (виртуальная смарт-карта)" с именем "VPN виртуальной смарт-карты" и идентификатором UUID *97CD65FA-AF4B-4587-9309-0DD6BFD8B4E1*.

3.  Клиент получает политику регистрации выбранного шаблона профиля с помощью идентификатора UUID, возвращенного на предыдущем этапе:

    ```
    GET /CertificateManagement/api/v1.0/profiletemplates/97CD65FA-AF4B-4587-9309-0DD6BFD8B4E1/policies/enroll
    ```
 <br/>   
4.  Клиент анализирует поле DataCollection полученной политики, обращая внимание на один элемент коллекции данных под названием "Причина запроса". Клиент также замечает, что флаг collectComments имеет значение *false*, поэтому пользователю не предлагается оставить комментарий.

5.  Когда пользователь укажет причину запроса сертификатов, клиент создает запрос:

    ```
    POST /CertificateManagement/api/v1.0/requests

    {
        "datacollection":"[{“Request Reason”:”Need VPN Certs”}]",
        "type":"Enroll",
        "profiletemplateuuid":"97CD65FA-AF4B-4587-9309-0DD6BFD8B4E1",
        "comment":""
    }
    ```
<br/>
6.  Сервер успешно создает запрос и возвращает URI запроса клиенту: /CertificateManagement/api/v1.0/requests/C6BAD97C-F97F-4920-8947-BE980C98C6B5.

7.  Клиент получает объект запроса, вызывая полученный URI:

    ```
    GET /CertificateManagement/api/v1.0/requests/C6BAD97C-F97F-4920-8947-BE980C98C6B5
    ```
<br/>
8.  Клиент проверяет, задано ли для свойства state в запросе значение approved. Может начаться выполнение запроса.

9.  Клиент изучает запрос, чтобы проверить, связана ли с запросом смарт-карта, по значению параметра newsmartcarduuid.

10. Так как он содержит только пустой идентификатор GUID, клиент должен либо использовать имеющуюся карту, еще не используемую службой MIM CM, либо создать ее, если шаблон профиля настроен для виртуальных смарт-карт.

11. Поскольку последний указан клиенту с помощью исходного запроса для регистрируемых шаблонов профиля (этап 1), теперь клиент должен создать устройство для виртуальной смарт-карты.

12. Клиент получает политику смарт-карты из шаблона профиля (по идентификатору UUID шаблона, выбранному на этапе 3):

    ```
    GET /CertificateManagement/api/v1.0/profiletemplates/97CD65FA-AF4B-4587-9309-0DD6BFD8B4E1/configuration/smartcards
    ```
13. Политика смарт-карты хранит ключ администратора по умолчанию в свойстве DefaultAdminKeyHex. При создании смарт-карты клиент должен указать в этом ключе исходный ключ администратора.  

14. После создания устройства смарт-карты клиент должен назначить его запросу:

    ```
    POST /CertificateManagement/api/v1.0/smartcards

    {
        "requestid":" C6BAD97C-F97F-4920-8947-BE980C98C6B5",
        "cardid":"23CADD5F-020D-4C3B-A5CA-307B7A06F9C9",
    }
    ```
<br/>
15. В ответ сервер отправит клиенту URI нового объекта смарт-карты: api/v1.0/smartcards/D700D97C-F91F-4930-8947-BE980C98A644.

16. Клиент получает объект смарт-карты:

    ```
    GET /CertificateManagement/api/v1.0/smartcards/ D700D97C-F91F-4930-8947-BE980C98A644
    ```
<br/>
17. Проверив значение флага diversifyadminkey в политике смарт-карты, полученной на этапе 12, клиент узнает, что необходимо изменить ключ администратора.

18. Клиент получает предложенный ключ администратора:

    ```
    GET /CertificateManagement/api/v1.0/requests/C6BAD97C-F97F-4920-8947-BE980C98C6B5/smartcards/D700D97C-F91F-4930-8947-BE980C98A644/diversifiedkey?cardid=23CADD5F-020D-4C3B-A5CA-307B7A06F9C9
    ```
<br/>
19. Клиент должен пройти проверку подлинности для карточки от имени администратора, чтобы задать ключ администратора. Для этого клиент запрашивает задание проверки подлинности у смарт-карты и отправляет его на сервер:

    ```
    GET /CertificateManagement/api/v1.0/requests/C6BAD97C-F97F-4920-8947-BE980C98C6B5/smartcards/D700D97C-F91F-4930-8947-BE980C98A644/authenticationresponse?cardid=23CADD5F-020D-4C3B-A5CA-307B7A06F9C9&challenge=CFAA62118BBD25&diversified=false
    ```

    Сервер отправляет ответ на запрос в тексте ответа HTTP. Найдите шестнадцатеричную строку запроса, преобразуйте ее в base64 и передайте ее в качестве параметра в URL-адрес. Этот URL-адрес вернет другой ответ, который необходимо преобразовать обратно в шестнадцатеричный формат.
<br/>
20. Сервер отправляет ответ на запрос в тексте ответа HTTP, а клиент использует его для изменения ключа администратора.

21. По значению поля UserPinOption в политике смарт-карты клиент определяет, что пользователь должен предоставить необходимый PIN-код.

22. Когда пользователь укажет необходимый PIN-код в диалоговом окне, клиент выполняет проверку подлинности по заданию и ответу, как описано на этапе 19, с тем отличием, что для измененного флага должно быть задано значение true:

    ```
    GET /CertificateManagement/api/v1.0/ requests/C6BAD97C-F97F-4920-8947-BE980C98C6B5/smartcards/D700D97C-F91F-4930-8947-BE980C98A644/authenticationresponse?cardid=23CADD5F-020D-4C3B-A5CA-307B7A06F9C9&challenge=CFAA62118BBD25&diversified=true
    ```
<br/>
23. Клиент использует ответ, полученный с сервера, чтобы задать PIN-код пользователя.

24. Теперь клиент готов к созданию запросов на сертификаты. Он запрашивает параметры создания сертификатов шаблонов профиля, чтобы определить, как должны создаваться ключи и запросы.

    ```
    GET /CertificateManagement/api/v1.0/requests/C6BAD97C-F97F-4920-8947-BE980C98C6B5/certificaterequestgenerationoptions.
    ```
<br/>
25. В ответ сервер пришлет один объект CertificateRequestGenerationOptions с перечислением JSON, содержащий сведения о возможности экспорта ключа, понятном имени сертификата, а также об алгоритме хэширования, алгоритме ключа, размере ключа и т. д. Клиент использует эти параметры для создания запроса сертификата.

26. На сервер отправляется один запрос сертификата. Клиент может также указать пароль PFX, который необходим для расшифровки больших двоичных объектов PFX, если шаблон сертификата задает архивирование сертификатов в центре сертификации, т. е. центр сертификации создает пару ключей и отправляет ее клиенту. Клиент также может добавить примечания.

    ```
    POST /CertificateManagement/api/v1.0/requests/C6BAD97C-F97F-4920-8947-BE980C98C6B5/certificatedata

    {
       "pfxpassword":"",
       "certificaterequests":[
           "MIIDZDC…”
        ]
    }   
    ```
<br/>
27. Через несколько секунд сервер отправляет в ответ один объект Microsoft.Clm.Shared.Certificate с перечислением JSON. По значению флага isPkcs7 клиент узнает, что этот ответ не является большим двоичным объектом PFX. Клиент извлекает большой двоичный объект, расшифровывая строку pkcs7 по кодировке base64, и устанавливает его.

28. Клиент отмечает запрос как выполненный.

    ```
    PUT /CertificateManagement/api/v1.0/requests/C6BAD97C-F97F-4920-8947-BE980C98C6B5

    {
        "status":"Completed"
    }
    ```
