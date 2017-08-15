---
title: "Отмена, прерывание и завершение запроса | Документация Майкрософт"
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
ms.assetid: e29e0068-7602-455e-8a3a-690da9ca8eb5
audience: developer
ms.reviewer: mwahl
ms.suite: ems
ms.openlocfilehash: 4f81c9d86006c477993b2ac8cc2e845de2c1d2f3
ms.sourcegitcommit: 02fb1274ae0dc11288f8bd9cd4799af144b8feae
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/13/2017
---
# <a name="cancel-abandon-or-complete-a-request"></a>Отмена, прерывание и завершение запроса
Как отметить запрос MIM CM как завершенный, отмененный или прерванный.

**Примечание**. URL-адреса, приведенные в этом разделе, относятся к имени узла, выбранному во время развертывания API. Например: `https://api.contoso.com`.
##<a name="request"></a>Запрос


Метод  |URL-адрес запроса  
---------|---------
PUT     |/CertificateManagement/api/v1.0/requests/{id}

###<a name="url-parameters"></a>Параметры URL-адресов
Свойство| Описание
---------|--------
id| Обязательный параметр. Идентификатор GUID запроса, который необходимо выполнить.


###<a name="request-headers"></a>Заголовки запроса
Распространенные заголовки запросов см. в таблице c [заголовками HTTP-запросов и ответов](certificate-management-rest-api-service-details.md#http-request-and-response-headers) в статье *CM REST API Service Details* (Сведения о REST API управления сертификатами).
###<a name="request-body"></a>Текст запроса
Текст запроса содержит следующие свойства.

Свойство | Описание
---------|-----------
состояние | Состояние, которое необходимо присвоить запросу. Возможны следующие значения: "Завершено", "Отменено" или "Прервано".


##<a name="response"></a>Ответ
###<a name="response-codes"></a>Коды ответа
код  |Описание  
---------|---------
200     | ОК
204 | Нет содержимого
403 | Запрещено
500 | Внутренняя ошибка

###<a name="response-headers"></a>Заголовки ответа
Распространенные заголовки ответов см. в таблице с [заголовками HTTP-запросов и ответов](certificate-management-rest-api-service-details.md#http-request-and-response-headers) в статье *CM REST API Service Details* (Сведения о REST API управления сертификатами).
###<a name="response-body"></a>Текст ответа
В случае успешного выполнения возвращает объект [Microsoft.Clm.Shared.Requests.Request](https://msdn.microsoft.com/library/microsoft.clm.shared.requests.request.aspx), который описывает запрос MIM CM, отмеченный как завершенный, со следующими свойствами:

Имя | Описание
-----|------------
Примечание | Комментарий, связанный с запросом MIM CM.
Completed | Время завершения запроса MIM CM.
DataCollection | Элементы сбора данных, связанные с запросом MIM CM.
DataCollectionФлажки | Параметры сбора данных для запроса MIM CM.
Флажки | Параметры, связанные с запросом MIM CM.
IsDataCollectionComplete | Логическое значение, указывающее, завершен ли сбор данных для запроса MIM CM.
IsEnrollmentAgent | Логическое значение, указывающее, необходим ли агент подачи заявок для выполнения запроса MIM CM.
IsSmartcard | Логическое значение, указывающее, является ли запрос MIM CM запросом смарт-карты или запросом профиля программного обеспечения.
NewProfileUuid | Идентификатор нового профиля программного обеспечения, созданный запросом MIM CM.
NewSmartcardUuid | Идентификатор новой смарт-карты, назначенный запросом MIM CM.
OldProfileUuid | Идентификатор профиля программного обеспечения, для которого создан запрос MIM CM.
OldSmartcardUuid | Идентификатор смарт-карты, для которой создан запрос MIM CM.
Origв статьеatorUserUuid | Идентификатор пользователя, отправившего запрос MIM CM
Priority | Приоритет запроса MIM CM.
ProfileTemplateUuid | Идентификатор шаблона профиля, для которого создан запрос MIM CM.
ЗапросType | Тип запроса MIM CM.
SecurityDescriptor | Дескриптор безопасности для запроса MIM CM.
Status | Состояние запроса MIM CM.
Отправлено | Время отправки запроса MIM CM.
TargetUserUuid | Идентификатор целевого пользователя для запроса MIM CM.
Uuid | Идентификатор запроса MIM CM.

##<a name="example"></a>Пример

###<a name="request"></a>Запрос
```
PUT /certificatemanagement/api/v1.0/requests/a9b4b42c-cc50-4c9b-89d1-bbc0bcd5a099 HTTP/1.1


{
    “status”:”Completed”
}
```
###<a name="response"></a>Ответ
```
HTTP/1.1 200 OK

{
    "Uuid":"a9b4b42c-cc50-4c9b-89d1-bbc0bcd5a099",
    "RequestType":1,
    "Status":8,
    "Flags":2,
    "DataCollection":[

    ],
    "DataCollectionFlags":32,
    "OriginatorUserUuid":"8f1590dc-d932-4b66-8e68-2e91c5880780",
    "TargetUserUuid":"8f1590dc-d932-4b66-8e68-2e91c5880780",
    "Submitted":"2015-07-07T23:36:21.93Z",
    "Completed":"2015-07-07T23:37:37.767Z",
    "NewProfileUuid":"b99ff38c-6653-471f-ae3c-325bb351a6bc",
    "OldProfileUuid":"00000000-0000-0000-0000-000000000000",
    "NewSmartcardUuid":"17cf063d-e337-4aa9-a822-346554ddd3c9",
    "OldSmartcardUuid":"00000000-0000-0000-0000-000000000000",
    "Priority":0,
    "Comment":"",
    "ProfileTemplateUuid":"a039b4d0-5ce8-4eff-8651-181c6576fda3",
    "SecurityDescriptor":"O:S-1-5-21-2127521184-1604012920-1887927527-14134865D:(D;;LC;;;S-1-5-21-2127521184-1604012920-1887927527-14995557)(A;;DCSW;;;S-1-5-21-2127521184-1604012920-1887927527-5094533)(A;;DCSW;;;S-1-5-21-2127521184-1604012920-1887927527-5094534)(A;;DCSW;;;S-1-5-21-2127521184-1604012920-1887927527-5219125)(A;;SWRC;;;S-1-5-21-2127521184-1604012920-1887927527-5094533)(A;;RC;;;WD)(A;;CCDCLCSWSDRC;;;S-1-5-21-2127521184-1604012920-1887927527-14134865)(A;;DCSW;;;S-1-5-21-2127521184-1604012920-1887927527-14995557)(A;;CCDCSW;;;S-1-5-21-2127521184-1604012920-1887927527-14995557)\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000",
    "IsSmartcard":true,
    "IsEnrollmentAgent":false,
    "IsDataCollectionComplete":false
}
```       
##<a name="see-also"></a>См. также

- [Метод Microsoft.Clm.Provision.ExecuteOperations.Complete](https://msdn.microsoft.com/library/microsoft.clm.provision.executeoperations.complete.aspx)
- [Объект Microsoft.Clm.Shared.Requests.Request](https://msdn.microsoft.com/library/microsoft.clm.shared.requests.request.aspx)
