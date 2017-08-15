---
title: "Создание запроса PAM | Документация Майкрософт"
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
ms.assetid: fe8b3374-9d32-4cc3-9328-f1eafeadfe8e
audience: developer
ms.reviewer: mwahl
ms.suite: ems
ms.openlocfilehash: de28af5c49eb98c5a1ccfbd8ed9353cf202e9e66
ms.sourcegitcommit: 02fb1274ae0dc11288f8bd9cd4799af144b8feae
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/13/2017
---
# <a name="create-pam-request"></a>Создание запроса PAM
Используется привилегированной учетной записью для повышения роли PAM.

**Примечание**. URL-адреса, приведенные в этом разделе, относятся к имени узла, выбранному во время развертывания API. Например: `http://api.contoso.com`.
##<a name="request"></a>Запрос


Метод  |URL-адрес запроса  
---------|---------
POST     |/api/pamresources/pamrequests

###<a name="query-parameters"></a>Параметры запроса
Параметр | Описание
--------|-------------
Justification | Необязательный параметр. Указанная пользователем причина запроса на повышение прав.
RoleId| Обязательный параметр. Уникальный идентификатор (GUID) роли PAM, до которой необходимо выполнить повышение.
RequestedTTL| Обязательный параметр. Запрошенный срок действия, в секундах.
ЗапросedTime | Необязательный параметр. Время повышения прав.  
v | Необязательный параметр. Версия API. Если этот параметр не указан, будет использоваться текущая (последняя) версия API. Дополнительные сведения см. в [разделе об управлении версиями в статье "PAM REST API Service Details"](privileged-access-management-rest-api-service-details.md#versioning) (Сведения о REST API службы PAM)

**Примечание**. Параметры *Justification*, *RoleId*, *RequestedTTL*и *RequestedTime* можно указать как свойства в тексте запроса, а не как параметры запроса. Параметр *v* можно указать только как параметр запроса.

###<a name="request-headers"></a>Заголовки запроса
Распространенные заголовки запросов см. в таблице с [заголовками HTTP-запросов и ответов](privileged-access-management-rest-api-service-details.md#http-request-and-response-headers) в статье *PAM REST API Service Details* (Сведения о REST API службы PAM).
###<a name="request-body"></a>Текст запроса
Необязательный параметр. Как отмечалось выше, параметры *Justification*, *RoleId*, *RequestedTTL*и *RequestedTime* можно указать как свойства в тексте запроса, а не в строке запроса URL-адреса.

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
Успешный ответ содержит объект запроса PAM со следующими свойствами.

Свойство | Описание
--------|-------------
ЗапросID | Уникальный идентификатор (GUID) запроса PAM.
CreatorID | Уникальный идентификатор (GUID) учетной записи, создавшей запрос, в службе MIM.
Justification | Причина повышения прав.
CreationTime | Время создания запроса.
CreationМетод | Метод, используемый для создания запроса.
ExpirationTime | Срок действия запроса.
RoleID| Уникальный идентификатор (GUID) роли PAM.
ЗапросedTTL | Запрошенное время ожидания в секундах.
RequestedTime | Запрошенное время повышения прав.
Состояние RequestStatus | Состояние запроса. Возможны следующие значения: "Идет обработка", "Активный", "Закрыто", "Закрытие", "Срок истек", "Ожидает утверждения", "Ожидает многофакторной проверки подлинности" и "Отклонено".

##<a name="example"></a>Пример

###<a name="request-1"></a>Запрос 1
```
POST /api/pamresources/pamrequests?Justification=Sample+Reason&RoleId=c28eab4a-95cf-4c08-a153-d5e8a9e660cd&RequestedTTL=7200&RequestedTime=2015%2F07%2F11+23%3A40 HTTP/1.1
```
###<a name="response-1"></a>Ответ 1
```
HTTP/1.1 201 Created

{  
    "odata.metadata":"http://localhost:8086/api/pamresources/%24metadata#pamrequests/@Element",
    "RequestId":"c0112f13-b16b-40ad-b547-07f23a7fba52",
    "CreatorID":"73257e5e-00b3-4309-a330-f1e607ff113a",
    "Justification":"Sample Reason",
    "CreationTime":"2015-07-11T23:38:09.036164-07:00",
    "CreationMethod":"PAM Web API",
    "ExpirationTime":"0001-01-01T00:00:00",
    "RoleId":"c28eab4a-95cf-4c08-a153-d5e8a9e660cd",
    "RequestedTTL":"7200",
    "RequestedTime":"2015-07-12T06:40:00Z",
    "RequestStatus":"PendingApproval"
}
```       

###<a name="request-2"></a>Запрос 2
```
POST /api/pamresources/pamrequests?Justification=&RoleId=c28eab4a-95cf-4c08-a153-d5e8a9e660cd&RequestedTTL=3600&RequestedTime= HTTP/1.1
```
###<a name="response-2"></a>Ответ 2
```
HTTP/1.1 201 Created

{
    "odata.metadata":"http://localhost:8086/api/pamresources/%24metadata#pamrequests/@Element",
    "RequestId":"504f9c49-00db-42bd-a157-ee5664617189",
    "CreatorID":"73257e5e-00b3-4309-a330-f1e607ff113a",
    "Justification":null,
    "CreationTime":"2015-07-11T23:07:30.2200123-07:00",
    "CreationMethod":"PAM Web API",
    "ExpirationTime":"0001-01-01T00:00:00",
    "RoleId":"c28eab4a-95cf-4c08-a153-d5e8a9e660cd",
    "RequestedTTL":"3600",
    "RequestedTime":"2015-07-12T06:07:27.7229894Z",
    "RequestStatus":"PendingApproval"
}
```       
