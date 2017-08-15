---
title: "Перенос данных профиля | Документация Майкрософт"
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
ms.assetid: 3eba062b-7adf-4766-9b94-cba1c7be2fd3
audience: developer
ms.reviewer: mwahl
ms.suite: ems
ms.openlocfilehash: 068497509b07b879fcadde6b60a9530d3d8db093
ms.sourcegitcommit: 02fb1274ae0dc11288f8bd9cd4799af144b8feae
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/13/2017
---
# <a name="get-profile-data"></a>Получение данных профиля
Возвращает список профилей сертификатов программного обеспечения пользователя со списком возможных операций, которые могут быть выполнены текущим пользователем. Запрос можно инициировать для любой из указанных операций.

**Примечание**. Сервер задаст ПИН-код, только если политика шаблона профиля указывает, что это необходимо. В противном случае его должен указать пользователь.

**Примечание**. URL-адреса, приведенные в этом разделе, относятся к имени узла, выбранному во время развертывания API. Например: `https://api.contoso.com`.
##<a name="request"></a>Запрос


Метод  |URL-адрес запроса  
---------|---------
GET     |/CertificateManagement/api/v1.0/profiles<br/>/CertificateManagement/api/v1.0/profiles/{id} <br/>/CertificateManagement/api/v1.0/requests/{requestid}/profiles

###<a name="url-parameters"></a>Параметры URL-адресов
Параметр | Описание
---------|------------
id | Идентификатор (GUID) возвращаемого профиля.
requestId | Идентификатор запроса, для которого возвращаются профили.

###<a name="query-parameters"></a>Параметры запроса
Параметр | Описание
---------|------------
состояние | Необязательный параметр. Указывает состояние профилей, для которых извлекаются данные. Возможные типы состояния: "Активно", "Утверждено", "Отменено", "Завершено", "Запрещено", "Выполняется", "Сбой", "Отсутствуют" и "Ожидание". <br/>Если состояние не указано, возвращаются все профили, независимо от состояния.
###<a name="request-headers"></a>Заголовки запроса
Распространенные заголовки запросов см. в таблице c [заголовками HTTP-запросов и ответов](certificate-management-rest-api-service-details.md#http-request-and-response-headers) в статье *CM REST API Service Details* (Сведения о REST API управления сертификатами).
###<a name="request-body"></a>Текст запроса
отсутствуют

##<a name="response"></a>Ответ
###<a name="response-codes"></a>Коды ответа
код  |Описание  
---------|---------
200 | ОК
204 | Нет содержимого
403 | Запрещено
500 | Внутренняя ошибка

###<a name="response-headers"></a>Заголовки ответа
Распространенные заголовки ответов см. в таблице с [заголовками HTTP-запросов и ответов](certificate-management-rest-api-service-details.md#http-request-and-response-headers) в статье *CM REST API Service Details* (Сведения о REST API управления сертификатами).
###<a name="response-body"></a>Текст ответа
В случае успешного выполнения возвращает список JSON-сериализованных объектов [Microsoft.Clm.Shared.Profiles.Profile](https://msdn.microsoft.com/library/microsoft.clm.shared.profiles.profile.aspx) со следующими свойствами:

Свойство | Описание
---------|------------
AssignedUserUuid | Идентификатор пользователя, которому назначен профиль.
Комментарий | Комментарий, описывающий профиль.
Флажки | Флажки, описывающие профиль.
ParentProfileUuid | Идентификатор старого профиля, который заменил этот профиль.
PrimaryProfileUuid | Идентификатор основного профиля.
ProfileOperations | Список возможных операций, которые может выполнять текущий пользователь в этом профиле.
ProfileTemplateUuid | Идентификатор шаблона профиля, который содержит политики и параметры, управляющие профилем.
ProfileTemplateVersion | Версия шаблона профиля во время создания профиля.
состояние; | Состояние профиля.
Uuid | Идентификатор профиля.


##<a name="example"></a>Пример

###<a name="request"></a>Запрос
```
GET /certificatemanagement/api/v1.0/profiles?status=Active HTTP/1.1
```
###<a name="response"></a>Ответ
```
HTTP/1.1 200 OK

[
    {
        "Uuid":"c0dd5c7d-ec35-4346-baca-3ad711e9722f",
        "Status":2,
        "Flags":1,
        "ParentProfileUuid":"1c9e2606-fea2-4048-a6ac-b014e54c22df",
        "PrimaryProfileUuid":"00000000-0000-0000-0000-000000000000",
        "AssignedUserUuid":"0378a33b-8650-4713-a727-efd233903643",
        "ProfileTemplateUuid":"8f31803f-8afc-49bb-911d-402ec264b589",
        "ProfileTemplateVersion":8,
        "Comment":"",
        "ProfileOperations":[
            "renew",
            "disable",
            "recover"
        ]
    },
    {
        "Uuid":"5ad77b40-aa42-4533-9396-c9c59fd021a8",
        "Status":2,
        "Flags":1,
        "ParentProfileUuid":"00000000-0000-0000-0000-000000000000",
        "PrimaryProfileUuid":"00000000-0000-0000-0000-000000000000",
        "AssignedUserUuid":"0378a33b-8650-4713-a727-efd233903643",
        "ProfileTemplateUuid":"8f31803f-8afc-49bb-911d-402ec264b589",
        "ProfileTemplateVersion":8,
        "Comment":"",
        "ProfileOperations":[
            "renew",
            "disable",
            "recover"
        ]
    },
    {
        "Uuid":"ff342953-c444-4dc7-b144-f5515d6460c6",
        "Status":2,
        "Flags":1,
        "ParentProfileUuid":"00000000-0000-0000-0000-000000000000",
        "PrimaryProfileUuid":"00000000-0000-0000-0000-000000000000",
        "AssignedUserUuid":"0378a33b-8650-4713-a727-efd233903643",
        "ProfileTemplateUuid":"1e3a31fe-699b-4a6b-945c-18b83c985bc1",
        "ProfileTemplateVersion":9,
        "Comment":"",
        "ProfileOperations":[
            "renew",
            "disable"
        ]
    }
]
```       
##<a name="see-also"></a>См. также

- [Класс Microsoft.Clm.Shared.Profiles.Profile](https://msdn.microsoft.com/library/microsoft.clm.shared.profiles.profile.aspx)
