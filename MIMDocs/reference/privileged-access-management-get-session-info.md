---
title: "Получение сведений о сеансе PAM | Документация Майкрософт"
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
ms.assetid: bc30e455-9a9c-413a-b8ca-9669286299cf
audience: developer
ms.reviewer: mwahl
ms.suite: ems
ms.openlocfilehash: 150bc7e863fc679e785526935155611fb75cd69b
ms.sourcegitcommit: 02fb1274ae0dc11288f8bd9cd4799af144b8feae
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/13/2017
---
# <a name="get-pam-session-info"></a>Получение сведений о сеансе PAM
Используется привилегированной учетной записью для получения имени учетной записи, совершившей вход в сеанс.

**Примечание**. URL-адреса, приведенные в этом разделе, относятся к имени узла, выбранному во время развертывания API. Например: `http://api.contoso.com`.
##<a name="request"></a>Запрос


Метод  |URL-адрес запроса  
---------|---------
GET     |/api/session/sessionв статьеfo

###<a name="query-parameters"></a>Параметры запроса
Параметр | Описание
----------|--------------
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
Успешный ответ содержит объект сеанса PAM со следующими свойствами.

Свойство| Описание
--------|-------------
Имя пользователя| Имя учетной записи, которая вошла в сеанс.

##<a name="example"></a>Пример

###<a name="request"></a>Запрос
```
GET /api/session/sessioninfo/ HTTP/1.1
```
###<a name="response"></a>Ответ
```
HTTP/1.1 200 OK

{
    "odata.metadata":"http://localhost:8086/api/pamresources/%24metadata#sessioninfo",
    "value":[
        {
            "Username":"FIMCITONEBOXAD\\Jen"
        }
    ]
}
```       
