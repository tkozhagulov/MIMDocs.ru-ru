---
title: "Сведения о REST API службы CM | Документация Майкрософт"
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
ms.assetid: 530047f1-e43b-4a69-9542-75bc1da57bf7
audience: developer
ms.reviewer: mwahl
ms.suite: ems
ms.openlocfilehash: 3d724dea8b1536f0155f9fc287d0cd74f5f16b3c
ms.sourcegitcommit: 02fb1274ae0dc11288f8bd9cd4799af144b8feae
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/13/2017
---
# <a name="cm-rest-api-service-details"></a>Сведения о службе API REST CM
Ниже описывается интерфейс API REST управления сертификатами (CM) Microsoft Identity Manager (MIM).

## <a name="architecture"></a>Архитектура 
Вызовы REST API CM MIM обрабатываются контроллерами. В следующей таблице представлен полный список контроллеров и примеры контекста, в котором они используются.

Контроллер| Образец маршрута
----------|-------------
CertificateDataController| /api/v1.0/requests/{requestid}/certificatedata /
CertificateRequestGenerationOptionsController| /api/v1.0/requests/{requestid}/certificaterequestgenerationoptions
CertificatesController| /api/v1.0/smartcards/{smartcardid}/certificates <br/> /api/v1.0/profiles/{profileid}/certificates
OperationsController| /api/v1.0/smartcards/{smartcardid}/operations <br/> /api/v1.0/profiles/{profileid}/operations
PoliciesController| /api/v1.0/profiletemplates/{profiletemplateid}/policies/{id}
ProfilesController| /api/v1.0/profiles/{id} <br/> /api/v1.0/Profiles <br/> /api/v1.0/requests/{requestid}/profiles/{id}
ProfileTemplatesController| /api/v1.0/profiletemplates/{id} <br/> /api/v1.0/profiletemplates <br/> /api/v1.0/profiletemplates/{profiletemplateid}/policies/{id}
RequestsController| /api/v1.0/requests/{id} <br/> /api/v1.0/requests
SmartcardsController| /api/v1.0/requests/{requestid}/smartcards/{id}/diversifiedkey <br/> /api/v1.0/requests/{requestid}/smartcards/{id}/serverproposedpin <br/> /api/v1.0/requests/{requestid}/smartcards/{id}/authenticationresponse <br/> /api/v1.0/requests/{requestid}/smartcards/{id} <br/> /api/v1.0/smartcards/{id} <br/> /api/v1.0/smartcards
SmartcardsConfigurationController| /api/v1.0/profiletemplates/{profiletemplateid}/configuration/smartcards
<br/>

## <a name="http-request-and-response-headers"></a>Заголовки HTTP-запросов и ответов

HTTP-запросы, адресованные API, должны содержать следующие заголовки (это неисчерпывающий список):

Заголовок | Описание
-------|------------
Авторизация | Обязательный параметр. Содержимое будет зависеть от метода проверки подлинности, который можно настроить и который может быть основан на WIA (встроенная проверка подлинности Windows) или службах федерации Active Directory.
Content-Type | Требуется, если в запросе есть текст. Должно быть задано как "application/json".
Content-Length | Требуется, если в запросе есть текст. 
Файл cookie | Файл cookie данного сеанса. Может потребоваться в зависимости от метода проверки подлинности.
<br/>
HTTP-ответы содержат следующие заголовки (это неисчерпывающий список):

Header | Описание
-------|------------
Content-Type | API всегда возвращает значение "application/json".
Content-Length | Длина текста запроса, если он имеется, в байтах.


## <a name="api-versioning"></a>Управление версиями API 
Текущая версия интерфейса API REST CM — 1.0. Версия, указанная в сегменте непосредственно за сегментом `/api` в URI — `/api/v1.0`. В будущем этот номер версии изменится при значительных модификациях API-интерфейса.


## <a name="enabling-the-api"></a>Включение API 
В раздел `<ClmConfiguration>` файла Web.config добавлен новый ключ:

```
<add key="Clm.WebApi.Enabled" value="false" />
```
<br/>

Этот ключ определяет, доступен ли API REST CM клиентам. Если для ключа задано значение "false", сопоставление маршрута для API не выполняется при запуске приложения. Это означает, что последующие запросы к конечным точкам API вернут код ошибки HTTP 404. Ключ по умолчанию имеет значение "disabled".
После изменения этого значения "true" не забудьте запустить **iisreset** на сервере.

## <a name="enabling-tracing-and-logging"></a>Включение трассировки и ведения журнала 
API-интерфейс REST CM MIM передает данные трассировки для каждого отправленного ему HTTP-запроса. Вы можете изменить уровень детализации данных трассировки, указав следующее значение конфигурации:

```
<add name="Microsoft.Clm.Web.API" value="0" />
```
<br/>

## <a name="error-handling-and-troubleshooting"></a>Обработка ошибок и устранение неполадок 
При возникновении исключения во время обработки запроса API-интерфейс REST CM MIM возвращает код состояния HTTP веб-клиенту. Для типичных ошибок API возвращает соответствующий код состояния HTTP и код ошибки. 

Необработанные исключения преобразуются в исключение `HttpResponseException` с кодом состояния HTTP код 500 ("Внутренняя ошибка") и записываются в журнал событий и файл трассировки MIM CM. Каждое необработанное исключение записывается в журнал событий с соответствующий идентификатором корреляции. Идентификатор корреляции также отправляется получателю API в сообщении об ошибке. Чтобы устранить ошибку, администратор может найти в журнале событий соответствующий идентификатор корреляции и сведения об ошибке.

Для обеспечения безопасности трассировки стека, соответствующие ошибкам, возникшим при использовании API REST CM MIM, не возвращаются клиенту.
