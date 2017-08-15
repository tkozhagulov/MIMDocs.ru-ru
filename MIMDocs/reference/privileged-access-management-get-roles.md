---
title: "Получение ролей PAM | Документация Майкрософт"
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
ms.assetid: d3c4f528-c3c8-41c1-905e-7eb84f074ce4
audience: developer
ms.reviewer: mwahl
ms.suite: ems
ms.openlocfilehash: 4cb4bbc6c7696f354e5759a677ece88a4e606544
ms.sourcegitcommit: 02fb1274ae0dc11288f8bd9cd4799af144b8feae
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/13/2017
---
# <a name="get-pam-roles"></a>Получение ролей PAM
Используется привилегированной учетной записью для получения списка ролей PAM, кандидатом на которые является учетная запись.

**Примечание**. URL-адреса, приведенные в этом разделе, относятся к имени узла, выбранному во время развертывания API. Например: `http://api.contoso.com`.
##<a name="request"></a>Запрос


Метод  |URL-адрес запроса  
---------|---------
GET     |/api/pamresources/pamroles

###<a name="query-parameters"></a>Параметры запроса
Параметр | Описание
----------|--------------
$filter | Необязательный параметр. Укажите любые свойства роли PAM в выражении фильтра, чтобы получить отфильтрованный список ответов. Подробнее о поддерживаемых операторах см. в [разделе о фильтрации в статье "PAM REST API Service Details"](privileged-access-management-rest-api-service-details.md#filtering) (Сведения о REST API службы PAM).
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
Успешный ответ содержит коллекцию из одной или нескольких ролей PAM, каждая из которых имеет следующие свойства.

Свойство | Описание
--------|-------------
RoleID | Уникальный идентификатор (GUID) роли PAM.
DisplayName | Отображаемое имя роли PAM в службе MIM.
Описание | Описание роли PAM в службе MIM.
TTL | Максимальное время ожидания прав доступа к роли в секундах.
AvailableFrom | Самое раннее время дня, в которое можно активировать запрос.
AvailableTo | Самое позднее время дня, в которое можно активировать запрос.
MFAEnabled | Логическое значение, указывающее, требуют ли запросы на активацию для этой роли запрос многофакторной проверки подлинности.
ApprovalEnabled | Логическое значение, указывающее, требуют ли запросы на активацию для этой роли утверждения владельцем роли.
AvailibitlyWв статьеdowEnabled | Логическое значение, указывающее, можно ли активировать роль только в определенный временной интервал.

##<a name="example"></a>Пример

###<a name="request"></a>Запрос
```
GET /api/pamresources/pamroles HTTP/1.1
```
###<a name="response"></a>Ответ
```
HTTP/1.1 200 OK

{
    "odata.metadata":"http://localhost:8086/api/pamresources/%24metadata#pamroles",
    "value":[
        {
            "RoleId":"8f5cec1a-ecba-42ec-b76d-e6e0e4bf4c62",
            "DisplayName":"Allow AD Access ",
            "Description":null,
            "TTL":"3600",
            "AvailableFrom":"0001-01-01T00:00:00",
            "AvailableTo":"0001-01-01T00:00:00",
            "MFAEnabled":false,
            "ApprovalEnabled":false,
            "AvailabilityWindowEnabled":false
        },
        {
            "RoleId":"c28eab4a-95cf-4c08-a153-d5e8a9e660cd",
            "DisplayName":"ApprovalRole",
            "Description":null,
            "TTL":"3600",
            "AvailableFrom":"0001-01-01T00:00:00",
            "AvailableTo":"0001-01-01T00:00:00",
            "MFAEnabled":false,
            "ApprovalEnabled":true,
            "AvailabilityWindowEnabled":false
        }
    ]
}
```       
