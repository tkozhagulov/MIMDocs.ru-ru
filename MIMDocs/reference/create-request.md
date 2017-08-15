---
title: "Создание запроса | Документация Майкрософт"
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
ms.assetid: 80fe0656-6fb2-400c-9ef8-5f62b61b2a1b
audience: developer
ms.reviewer: mwahl
ms.suite: ems
ms.openlocfilehash: d5af8767583cb6999de399de58b321147846291a
ms.sourcegitcommit: 02fb1274ae0dc11288f8bd9cd4799af144b8feae
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/13/2017
---
# <a name="create-request"></a>Создание запроса
Создайте запрос MIM CM.

**Примечание**. URL-адреса, приведенные в этом разделе, относятся к имени узла, выбранному во время развертывания API. Например: `https://api.contoso.com`.
##<a name="request"></a>Запрос


Метод  |URL-адрес запроса  
---------|---------
POST     |/CertificateManagement/api/v1.0/requests

###<a name="url-parameters"></a>Параметры URL-адресов
отсутствуют

###<a name="request-headers"></a>Заголовки запроса
Распространенные заголовки запросов см. в таблице c [заголовками HTTP-запросов и ответов](certificate-management-rest-api-service-details.md#http-request-and-response-headers) в статье *CM REST API Service Details* (Сведения о REST API управления сертификатами).
###<a name="request-body"></a>Текст запроса
Текст запроса содержит следующие свойства.

Свойство | Описание
---------|-----------
profiletemplateuuid | Обязательный параметр. Идентификатор GUID шаблона профиля, для которого пользователь создает запрос.
datacollection | Обязательный параметр. Коллекция пар "имя-значение", представляющая данные, которые предоставляются регистрирующимся пользователем. Коллекцию необходимых данных можно извлечь из политики рабочего процесса шаблона профиля. Можно указать и пустую коллекцию.
target | Опциональный параметр. Идентификатор GUID целевого пользователя, для которого создается запрос. Если параметр не указан, применяется GUID текущего пользователя.
type | Обязательный параметр. Тип создаваемого запроса. Доступные типы запросов: "Enroll", "Duplicate", "OfflineUnblock", "OnlineUpdate", "Renew", "Recover", "RecoverOnBehalf", "Reinstate", "Retire", "Revoke", "TemporaryCards" и "Unblock".<br/>**Примечание**. Не все типы запросов поддерживаются для всех шаблонов профиля. Например, невозможно указать операцию разблокировки для шаблона профиля программного обеспечения.
комментарий | Обязательный параметр. Любые комментарии, которые может ввести пользователь. Политика рабочего процесса определяет, необходимо ли это. Можно указать пустую строку.
priority | Необязательный параметр. Приоритет запроса. Если параметр не указан, используется приоритет запроса по умолчанию, определяемый параметрами шаблона профиля.


##<a name="response"></a>Ответ
###<a name="response-codes"></a>Коды ответа
код  |Описание  
---------|---------
201     | Создано
403 | Запрещено
500 | Внутренняя ошибка

###<a name="response-headers"></a>Заголовки ответа
Распространенные заголовки ответов см. в таблице с [заголовками HTTP-запросов и ответов](certificate-management-rest-api-service-details.md#http-request-and-response-headers) в статье *CM REST API Service Details* (Сведения о REST API управления сертификатами).
###<a name="response-body"></a>Текст ответа
В случае успешного выполнения возвращается URI созданного запроса.
##<a name="example"></a>Пример

###<a name="request-1"></a>Запрос 1
```
POST /CertificateManagement/api/v1.0/requests HTTP/1.1

{
    "datacollection":"[]",
    "type":"Enroll",
    "profiletemplateuuid":"a039b4d0-5ce8-4eff-8651-181c6576fda3",
    "comment":""
}
```
###<a name="response-1"></a>Ответ 1
```
HTTP/1.1 201 Created

"api/v1.0/requests/a9b4b42c-cc50-4c9b-89d1-bbc0bcd5a099"
```
###<a name="request-2"></a>Запрос 2
```
POST /CertificateManagement/api/v1.0/requests HTTP/1.1

{  
    "datacollection":"[]",
    "type":"Unblock",
    "smartcard":"17cf063d-e337-4aa9-a822-346554ddd3c9",
    "comment":""
}
```
###<a name="response-2"></a>Ответ 2
```
HTTP/1.1 201 Created

"api/v1.0/requests/0c96d73f-967b-420e-854a-43ad2a1504bc"
```       

###<a name="request-3"></a>Запрос 3
```
POST /CertificateManagement/api/v1.0/requests HTTP/1.1

{
    "profiletemplateuuid" : "97CD65FA-AF4B-4587-9309-0DD6BFD8B4E1",
    "datacollection":
    [
        {"name" : "pavle"},
        {"city" : "seattle"}
    ],
    "target" : "97CC3493-F556-4C9B-9D8B-982434201527",
    "type" : "Enroll",
    "comment" : "LALALALA",
    "priority" :  "4"
}
```
##<a name="see-also"></a>См. также

- [Метод Microsoft.Clm.Provision.RequestOperations.InitiateEnroll](https://msdn.microsoft.com/library/windows/desktop/microsoft.clm.provision.requestoperations.initiateenroll.aspx)
- [Метод Microsoft.Clm.Provision.RequestOperations.InitiateOfflineUnblock](https://msdn.microsoft.com/library/windows/desktop/microsoft.clm.provision.requestoperations.initiateofflineunblock.aspx)
- [Метод Microsoft.Clm.Provision.RequestOperations.InitiateRecover](https://msdn.microsoft.com/library/windows/desktop/microsoft.clm.provision.requestoperations.initiaterecover.aspx)
- [Метод Microsoft.Clm.Provision.RequestOperations.InitiateRetire](https://msdn.microsoft.com/library/windows/desktop/microsoft.clm.provision.requestoperations.initiateretire.aspx)
- [Метод Microsoft.Clm.Provision.RequestOperations.InitiateUnblock](https://msdn.microsoft.com/library/windows/desktop/microsoft.clm.provision.requestoperations.initiateunblock.aspx)
