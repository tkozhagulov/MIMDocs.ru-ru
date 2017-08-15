---
title: "Утверждение или отклонение ожидающего запроса PAM | Документация Майкрософт"
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
ms.assetid: 0632656f-ecf4-4090-85a8-216d5638140a
audience: developer
ms.reviewer: mwahl
ms.suite: ems
ms.openlocfilehash: 3e5506f96a22d1918cff7d0c9b822babb0f6cfa9
ms.sourcegitcommit: 02fb1274ae0dc11288f8bd9cd4799af144b8feae
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/13/2017
---
# <a name="approve-or-reject-a-pending-pam-request"></a>Утверждение или отклонение ожидающего запроса PAM
Используется привилегированной учетной записью для утверждения, закрытия или отклонения запроса на повышение роли PAM.

**Примечание**. URL-адреса, приведенные в этом разделе, относятся к имени узла, выбранному во время развертывания API. Например: `http://api.contoso.com`.
##<a name="request"></a>Запрос


Метод  |URL-адрес запроса  
---------|---------
POST     |/api/pamresources/pamrequeststoapprove({approvalId)/Approve <br/>/api/pamresources/pamrequeststoapprove({approvalId)/Reject

###<a name="url-parameters"></a>Параметры URL-адресов
Параметр | Описание
----------|-----------
approvalId | Идентификатор GUID объекта утверждения в PAM, заданный в следующем формате: `guid'xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx'`

###<a name="query-parameters"></a>Параметры запроса
Параметр | Описание
----------|--------------
v | Необязательный параметр. Версия API. Если этот параметр не указан, будет использоваться текущая (последняя) версия API. Дополнительные сведения см. в [разделе об управлении версиями в статье "PAM REST API Service Details"](privileged-access-management-rest-api-service-details.md#versioning) (Сведения о REST API службы PAM)


###<a name="request-headers"></a>Заголовки запроса
Распространенные заголовки запросов см. в таблице с [заголовками HTTP-запросов и ответов](privileged-access-management-rest-api-service-details.md#http-request-and-response-headers) в статье *PAM REST API Service Details* (Сведения о REST API службы PAM).
###<a name="request-body"></a>Текст запроса
Отсутствуют.

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
отсутствуют
##<a name="example"></a>Пример

###<a name="request"></a>Запрос
```
POST /api/pamresources/pamrequeststoapprove(guid'5dbd9d0c-0a9d-4f75-8cbd-ff6ffdc00143')/Approve HTTP/1.1


```
###<a name="response"></a>Ответ
```
HTTP/1.1 200 OK

```       
