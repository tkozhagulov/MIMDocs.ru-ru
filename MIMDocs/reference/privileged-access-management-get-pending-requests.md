---
title: "Получение ожидающих запросов PAM | Документация Майкрософт"
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
ms.assetid: 005dc8fd-d73e-4557-b485-5566f16537eb
audience: developer
ms.reviewer: mwahl
ms.suite: ems
ms.openlocfilehash: aa1e8cd48b1bcca6e856bd553b6b92a062a08ff4
ms.sourcegitcommit: 02fb1274ae0dc11288f8bd9cd4799af144b8feae
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/13/2017
---
# <a name="get-pending-pam-requests"></a>Получение ожидающего запроса PAM
Используется привилегированной учетной записью для получения списка ожидающих запросов, требующих утверждения.

**Примечание**. URL-адреса, приведенные в этом разделе, относятся к имени узла, выбранному во время развертывания API. Например: `http://api.contoso.com`.
##<a name="request"></a>Запрос

Метод  |URL-адрес запроса  
---------|---------
GET     |/api/pamresources/pamrequeststoapprove

###<a name="query-parameters"></a>Параметры запроса
Параметр | Описание
----------|--------------
$filter | Необязательный параметр. Укажите любые свойства ожидающего запроса PAM в выражении фильтра, чтобы получить отфильтрованный список ответов. Подробнее о поддерживаемых операторах см. в [разделе о фильтрации в статье "PAM REST API Service Details"](privileged-access-management-rest-api-service-details.md#filtering) (Сведения о REST API службы PAM).
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
Успешный ответ содержит список объектов утверждения запроса PAM со следующими свойствами.

Свойство | Описание
---------|-------------
RoleName | Отображаемое имя роли, для которого требуется утверждение.
Запросor | Имя пользователя, инициирующего запрос, который требуется утвердить.
Justification | Обоснование, предоставленное пользователем.
RequestedTTL | Запрошенный срок действия в секундах.
ЗапросedTime | Запрошенное время повышения прав.
CreationTime | Время создания запроса.
FIMЗапросID | Содержит один элемент, "Value", с уникальным идентификатором (GUID) запроса PAM.
ЗапросorID | Содержит один элемент, "Value", с уникальным идентификатором (GUID) учетной записи Active Directory, создавшей запрос PAM.
ApprovalObjectID | Содержит один элемент, "Value", с уникальным идентификатором (GUID) для объекта утверждения.

##<a name="example"></a>Пример

###<a name="request"></a>Запрос
```
GET /api/pamresources/pamrequeststoapprove HTTP/1.1
```
###<a name="response"></a>Ответ
```
HTTP/1.1 200 OK

{
    "odata.metadata":"http://localhost:8086/api/pamresources/%24metadata#pamrequeststoapprove",
    "value":[
        {
            "RoleName":"ApprovalRole",
            "Requestor":"PRIV.Jen",
            "Justification":"Justification Reason",
            "RequestedTTL":"3600",
            "RequestedTime":"2015-07-11T22:25:00Z",
            "CreationTime":"2015-07-11T22:24:52.51Z",
            "FIMRequestID":{
                "Value":"9802d7b7-b4e9-4fe4-8f5c-649cda127e49"
            },
            "RequestorID":{
                "Value":"73257e5e-00b3-4309-a330-f1e607ff113a"
            },
            "ApprovalObjectID":{
                "Value":"5dbd9d0c-0a9d-4f75-8cbd-ff6ffdc00143"
            }
        }
    ]
}
```       
