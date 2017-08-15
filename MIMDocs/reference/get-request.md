---
title: "Возвращение запроса | Документация Майкрософт"
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
ms.assetid: dcacf36c-0670-44d7-9f40-388667235271
audience: developer
ms.reviewer: mwahl
ms.suite: ems
ms.openlocfilehash: 56bb25f7282879943dc624f3c24b836c7ae4a58c
ms.sourcegitcommit: 02fb1274ae0dc11288f8bd9cd4799af144b8feae
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/13/2017
---
# <a name="get-request"></a>Возвращение запроса
Возвращает один или несколько указанных запросов MIM CM

**Примечание**. URL-адреса, приведенные в этом разделе, относятся к имени узла, выбранному во время развертывания API. Например: `https://api.contoso.com`.
##<a name="request"></a>Запрос


Метод  |URL-адрес запроса  
---------|---------
GET     |/CertificateManagement/api/v1.0/requests/{id}

###<a name="url-parameters"></a>Параметры URL-адресов
Свойство| Описание
---------|--------
id| Необязательный параметр. Глобальный уникальный идентификатор (GUID) запроса, который необходимо извлечь.
###<a name="query-parameters"></a>Параметры запроса
Свойство| Описание
---------|--------
targetuser| Опциональный параметр. Целевой пользователь запроса. Если цель не указана, будут возвращены все запросы, независимо от целевого пользователя. <br/> **Примечание**. В настоящее время поддерживается только параметр "текущий".
состояние| Необязательный параметр. Указывает состояние запроса, который нужно извлечь. Возможные типы состояния: *Утверждено*, *Отменено*, *Завершено*, *Запрещено*, *Выполняется*, *Сбой*, *Отсутствуют*и *Ожидание*. <br/>Если состояние запроса не указано, будут возвращены все запросы, независимо от состояния.

###<a name="request-headers"></a>Заголовки запроса
Распространенные заголовки запросов см. в таблице c [заголовками HTTP-запросов и ответов](certificate-management-rest-api-service-details.md#http-request-and-response-headers) в статье *CM REST API Service Details* (Сведения о REST API управления сертификатами).
###<a name="request-body"></a>Текст запроса
отсутствуют

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
В случае успешного выполнения возвращается один или несколько объектов [запроса](https://msdn.microsoft.com/library/windows/desktop/microsoft.clm.shared.requests.request.aspx) со следующими свойствами:

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

###<a name="request-1"></a>Запрос 1
```
GET /certificatemanagement/api/v1.0/requests/a9b4b42c-cc50-4c9b-89d1-bbc0bcd5a099 HTTP/1.1

```
###<a name="response-1"></a>Ответ 1
```
HTTP/1.1 200 OK

{
    "Uuid":"a9b4b42c-cc50-4c9b-89d1-bbc0bcd5a099",
    "RequestType":1,
    "Status":3,
    "Flags":2,
    "DataCollection":[

    ],
    "DataCollectionFlags":32,
    "OriginatorUserUuid":"8f1590dc-d932-4b66-8e68-2e91c5880780",
    "TargetUserUuid":"8f1590dc-d932-4b66-8e68-2e91c5880780",
    "Submitted":"2015-07-07T23:36:21.93Z",
    "Completed":"0001-01-01T00:00:00",
    "NewProfileUuid":"00000000-0000-0000-0000-000000000000",
    "OldProfileUuid":"00000000-0000-0000-0000-000000000000",
    "NewSmartcardUuid":"00000000-0000-0000-0000-000000000000",
    "OldSmartcardUuid":"00000000-0000-0000-0000-000000000000",
    "Priority":0,
    "Comment":"",
    "ProfileTemplateUuid":"a039b4d0-5ce8-4eff-8651-181c6576fda3",
    "SecurityDescriptor":"O:S-1-5-21-2127521184-1604012920-1887927527-14134865D:(D;;LC;;;S-1-5-21-2127521184-1604012920-1887927527-14995557)(A;;DCSW;;;S-1-5-21-2127521184-1604012920-1887927527-5094533)(A;;DCSW;;;S-1-5-21-2127521184-1604012920-1887927527-5094534)(A;;DCSW;;;S-1-5-21-2127521184-1604012920-1887927527-5219125)(A;;SWRC;;;S-1-5-21-2127521184-1604012920-1887927527-5094533)(A;;RC;;;WD)(A;;CCDCLCSWSDRC;;;S-1-5-21-2127521184-1604012920-1887927527-14134865)(A;;DCSW;;;S-1-5-21-2127521184-1604012920-1887927527-14995557)(A;;CCDCSW;;;S-1-5-21-2127521184-1604012920-1887927527-14995557)\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000",
    "IsSmartcard":true,
    "IsEnrollmentAgent":false,
    "IsDataCollectionComplete":false
}```       
###Request 2
```
GET /certificatemanagement/api/v1.0/requests/0c96d73f-967b-420e-854a-43ad2a1504bc HTTP/1.1
```
###Response 2
```
HTTP/1.1 200 OK

{ "Uuid":"0c96d73f-967b-420e-854a-43ad2a1504bc", "RequestType":5, "Status":3, "Flags":2, "DataCollection":[ { "Name":"Sample Data Item", "Value":null } ], "DataCollectionFlags":32, "OriginatorUserUuid":"8f1590dc-d932-4b66-8e68-2e91c5880780", "TargetUserUuid":"8f1590dc-d932-4b66-8e68-2e91c5880780", "Submitted":"2015-07-07T23:40:33.133Z", "Completed":"0001-01-01T00:00:00", "NewProfileUuid":"b99ff38c-6653-471f-ae3c-325bb351a6bc", "OldProfileUuid":"b99ff38c-6653-471f-ae3c-325bb351a6bc", "NewSmartcardUuid":"17cf063d-e337-4aa9-a822-346554ddd3c9", "OldSmartcardUuid":"17cf063d-e337-4aa9-a822-346554ddd3c9", "Priority":0, "Comment":"", "ProfileTemplateUuid":"a039b4d0-5ce8-4eff-8651-181c6576fda3", "SecurityDescriptor":"O:S-1-5-21-2127521184-1604012920-1887927527-14134865D:(D;;LC;;;S-1-5-21-2127521184-1604012920-1887927527-14995557)(A;;SWRC;;;S-1-5-21-2127521184-1604012920-1887927527-5094533)(A;;RC;;;WD)(A;;CCDCLCSWSDRC;;;S-1-5-21-2127521184-1604012920-1887927527-14134865)(A;;DCSW;;;S-1-5-21-2127521184-1604012920-1887927527-14995557)(A;;CCDCSW;;;S-1-5-21-2127521184-1604012920-1887927527-14995557)\u0000\u0000\u0000\u0000\u0000\u0000", "IsSmartcard":true, "IsEnrollmentAgent":false, "IsDataCollectionComplete":false }
```       

##See Also

- [Microsoft.Clm.Provision.FindOperations.FindRequest Method](http://msdn.microsoft.com/library/windows/desktop/microsoft.clm.provision.findoperations.findrequests.aspx)
- [Microsoft.Clm.Shared.RequestPermission Enumeration](http://msdn.microsoft.com/library/windows/desktop/microsoft.clm.shared.requestpermission.aspx)
- [Microsoft.Clm.Shared.Requests.Request Class](https://msdn.microsoft.com/library/windows/desktop/microsoft.clm.shared.requests.request.aspx)
