---
title: "Получение запроса PAM | Документация Майкрософт"
description: 
keywords: 
author: msmbaldwin
ms.author: mbaldwin
manager: mbaldwin
ms.date: 10/17/2016
ms.topic: reference
ms.prod: identity-manager-2015
ms.service: microsoft-identity-manager
ms.technology: security
ms.assetid: 620eebd6-e4c3-473b-b824-ee6cfe83e509
audience: developer
ms.reviewer: mwahl
ms.suite: ems
ms.openlocfilehash: 00467b6443d3e6e0511ee1817a945ffe569b99b0
ms.sourcegitcommit: 02fb1274ae0dc11288f8bd9cd4799af144b8feae
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/13/2017
---
# <a name="get-pam-requests"></a>Получение запроса PAM
Используется привилегированной учетной записью для получения журнал ранее отправленных запросов PAM.

**Примечание**. URL-адреса, приведенные в этом разделе, относятся к имени узла, выбранному во время развертывания API. Например: `http://api.contoso.com`.
##<a name="request"></a>Запрос


Метод  |URL-адрес запроса  
---------|---------
GET     |/api/pamresources/pamrequests

###<a name="query-parameters"></a>Параметры запроса
Параметр | Описание
----------|--------------
$filter | Необязательный параметр. Укажите любые свойства запроса PAM в выражении фильтра, чтобы получить отфильтрованный список ответов. Подробнее о поддерживаемых операторах см. в [разделе о фильтрации в статье "PAM REST API Service Details"](privileged-access-management-rest-api-service-details.md#filtering) (Сведения о REST API службы PAM).
v | Необязательный параметр. Версия API. Если этот параметр не указан, будет использоваться текущая (последняя) версия API. Дополнительные сведения см. в [разделе об управлении версиями в статье "PAM REST API Service Details"](privileged-access-management-rest-api-service-details.md#versioning) (Сведения о REST API службы PAM)

###<a name="request-headers"></a>Заголовки запроса
Распространенные заголовки запросов см. в таблице с [заголовками HTTP-запросов и ответов](privileged-access-management-rest-api-service-details.md#http-request-and-response-headers) в статье *PAM REST API Service Details* (Сведения о REST API службы PAM).
###<a name="request-body"></a>Текст запроса
отсутствуют

##<a name="response"></a>Ответ
###<a name="response-codes"></a>Коды ответа
код  |Описание  
---------|---------
200 | ОК
401 | Недостаточно прав
403 | Запрещено
408 | Время ожидания запроса   
500 | Внутренняя ошибка сервера
503 | Служба недоступна

###<a name="response-headers"></a>Заголовки ответа
Распространенные заголовки ответов см. в таблице с [заголовками HTTP-запросов и ответов](privileged-access-management-rest-api-service-details.md#http-request-and-response-headers) в статье *PAM REST API Service Details* (Сведения о REST API службы PAM).
###<a name="response-body"></a>Текст ответа
Успешный ответ содержит список объектов запроса PAM со следующими свойствами.

Свойство | Описание
--------|-------------
ЗапросID | Уникальный идентификатор (GUID) запроса PAM.
CreatorID | Уникальный идентификатор (GUID) учетной записи Active Directory, создавшей запрос PAM.
Justification | Причина повышения прав.
DisplayName | Отображаемое имя запроса PAM в MIM.
CreationTime | Время создания запроса.
CreationМетод | Метод, используемый для создания запроса.
ExpirationTime | Срок действия запроса.
RoleID| Уникальный идентификатор (GUID) роли PAM.
ЗапросedTTL | Запрошенное время ожидания в секундах.
RequestedTime | Запрошенное время повышения прав.
ЗапросedStatus | Состояние запроса. Возможны следующие значения: "Активный", "Закрыто", "Закрытие", "Срок истек", "Ожидает утверждения" и "Отклонено".

##<a name="example"></a>Пример

###<a name="request"></a>Запрос
```
GET /api/pamresources/pamrequests?$filter=CreationTime%20gt%20datetime'2015-06-12T04:49:32.431Z'%20and%20CreationTime%20lt%20datetime'2015-07-13T04:49:32.432Z' HTTP/1.1
```

###<a name="response"></a>Ответ
```
HTTP/1.1 200 OK

{
    "odata.metadata":"http://localhost:8086/api/pamresources/%24metadata#pamrequests",
    "value":[
        {
            "RequestId":"b22e1343-9a2b-4e33-a70a-1bb7b2d405b9",
            "CreatorID":"73257e5e-00b3-4309-a330-f1e607ff113a",
            "Justification":null,
            "CreationTime":"2015-06-23T11:34:38.58Z",
            "CreationMethod":"PAM Web API",
            "ExpirationTime":"2015-06-23T12:34:38.847Z",
            "RoleId":"8f5cec1a-ecba-42ec-b76d-e6e0e4bf4c62",
            "RequestedTTL":"3600",
            "RequestedTime":"2015-06-23T11:34:36.417Z",
            "RequestStatus":"Expired"
        },
        {
            "RequestId":"3a98d1c7-524d-4b72-9da7-bd9f907eab55",
            "CreatorID":"73257e5e-00b3-4309-a330-f1e607ff113a",
            "Justification":"Reason for Request",
            "CreationTime":"2015-07-12T04:35:14.433Z",
            "CreationMethod":"PAM Web API",
            "ExpirationTime":"2015-07-12T04:43:51.95Z",
            "RoleId":"8f5cec1a-ecba-42ec-b76d-e6e0e4bf4c62",
            "RequestedTTL":"12960000",
            "RequestedTime":"2015-07-12T04:35:00Z",
            "RequestStatus":"Closed"
        },
        {
            "RequestId":"f5e80be1-e9a3-42c4-81f8-4be5a4a429f4",
            "CreatorID":"73257e5e-00b3-4309-a330-f1e607ff113a",
            "Justification":null,
            "CreationTime":"2015-07-12T04:48:17.46Z",
            "CreationMethod":"PAM Web API",
            "ExpirationTime":"2015-07-12T05:48:17.853Z",
            "RoleId":"8f5cec1a-ecba-42ec-b76d-e6e0e4bf4c62",
            "RequestedTTL":"3600",
            "RequestedTime":"2015-07-12T04:48:14.057Z",
            "RequestStatus":"Active"
        },
        {
            "RequestId":"b0f0ddc0-c809-4770-9d39-0d706f97a2de",
            "CreatorID":"73257e5e-00b3-4309-a330-f1e607ff113a",
            "Justification":"",
            "CreationTime":"2015-06-30T07:01:13.147Z",
            "CreationMethod":"PAM Web API",
            "ExpirationTime":"0001-01-01T00:00:00",
            "RoleId":"c28eab4a-95cf-4c08-a153-d5e8a9e660cd",
            "RequestedTTL":"3600",
            "RequestedTime":"2015-06-30T07:01:13.119Z",
            "RequestStatus":"Rejected"
        },
        {
            "RequestId":"5ec10e61-cdd1-404e-a18e-740467d87dbf",
            "CreatorID":"73257e5e-00b3-4309-a330-f1e607ff113a",
            "Justification":"Example Reason",
            "CreationTime":"2015-07-12T04:49:09.963Z",
            "CreationMethod":"PAM Web API",
            "ExpirationTime":"0001-01-01T00:00:00",
            "RoleId":"c28eab4a-95cf-4c08-a153-d5e8a9e660cd",
            "RequestedTTL":"12960000",
            "RequestedTime":"2015-07-12T04:50:00Z",
            "RequestStatus":"PendingApproval"
        }
    ]
}
```       
