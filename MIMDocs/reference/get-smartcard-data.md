---
title: "Получение данных смарт-карты | Документация Майкрософт"
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
ms.assetid: 81f4b7cd-e4d9-4b11-b125-78cc9f183cf0
audience: developer
ms.reviewer: mwahl
ms.suite: ems
ms.openlocfilehash: 9a84982971d169b5c9e7bd758cc74d795416975b
ms.sourcegitcommit: 02fb1274ae0dc11288f8bd9cd4799af144b8feae
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/13/2017
---
# <a name="get-smartcard-data"></a>Получение данных смарт-карты
Возвращает список профилей смарт-карт пользователя со списком возможных операций, которые могут быть выполнены текущим пользователем. Запрос можно инициировать для любой из указанных операций.

**Примечание**. URL-адреса, приведенные в этом разделе, относятся к имени узла, выбранному во время развертывания API. Например: `https://api.contoso.com`.
##<a name="request"></a>Запрос


Метод  |URL-адрес запроса  
---------|---------
GET     |/CertificateManagement/api/v1.0/smartcards <br/> /CertificateManagement/api/v1.0/smartcards/{smartcarduuid}


###<a name="url-parameters"></a>Параметры URL-адресов
Свойство| Описание
---------|--------
smartcarduuid | Необязательный параметр. UUID смарт-карты, указанный MIM CM. Это поле "uuid" объекта [Microsoft.Clm.Shared.Smartcards.Smartcard](http://msdn.microsoft.com/library/microsoft.clm.shared.smartcards.smartcard.aspx).

###<a name="query-parameters"></a>Параметры запроса
Свойство| Описание
---------|--------
cardid | Необязательный параметр. UUID смарт-карты, указанный MIM CM. Это поле "uuid" объекта [Microsoft.Clm.Shared.Smartcards.Smartcard](http://msdn.microsoft.com/library/microsoft.clm.shared.smartcards.smartcard.aspx).


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
В случае успешного выполнения возвращает JSON-сериализованный объект [Microsoft.Clm.Shared.Smartcards.Smartcard](http://msdn.microsoft.com/library/microsoft.clm.shared.smartcards.smartcard.aspx) объектов со следующими свойствами:

Имя | Описание
-----|-----------
AssignedUserUuid | Идентификатор пользователя, которому назначена смарт-карта.
Atr | Строка ATR смарт-карты, которая в настоящее время инициализируется.
Примечание | Комментарий, описывающий смарт-карту.
Флажки | Флажки, описывающие смарт-карту.
ПО промежуточного слоя | ПО промежуточного слоя смарт-карты.
ParentSmartcardUuid | Идентификатор старой смарт-карты, которую заменила эта смарт-карта.
PermanentSmartcardUuid | Идентификатор постоянной смарт-карты, связанной с этой смарт-картой.
PrimarySmartcardUuid | Идентификатор основной смарт-карты.
ProfileTemplateUuid | Идентификатор шаблона профиля, который содержит политики и параметры, управляющие смарт-картой.
ProfileTemplateVersion | Версия шаблона профиля во время создания профиля смарт-карты.
SerialNumber | Серийный номер смарт-карты.
Состояние | Состояние смарт-карты.
Uuid | Идентификатор профиля смарт-карты.

##<a name="example"></a>Пример

###<a name="request-1"></a>Запрос 1
```
GET /certificatemanagement/api/v1.0/smartcards?cardid=d1ef6869-5517-42a0-8f05-16ca1a0b834d HTTP/1.1

```
###<a name="response-1"></a>Ответ 1
```
HTTP/1.1 200 OK

{
    "Uuid":"438d1b30-f3b4-4bed-85fa-285e08605ba7",
    "Status":3,
    "Flags":1,
    "ParentSmartcardUuid":"00000000-0000-0000-0000-000000000000",
    "PrimarySmartcardUuid":"00000000-0000-0000-0000-000000000000",
    "PermanentSmartcardUuid":"00000000-0000-0000-0000-000000000000",
    "AssignedUserUuid":"8f1590dc-d932-4b66-8e68-2e91c5880780",
    "ProfileTemplateUuid":"a039b4d0-5ce8-4eff-8651-181c6576fda3",
    "ProfileTemplateVersion":46,
    "Comment":"",
    "SerialNumber":"{d1ef6869-5517-42a0-8f05-16ca1a0b834d}",
    "Middleware":"MSBaseCSP",
    "Atr":"3b8d0180fba000000397425446590301c8"
}
```       
###<a name="request-2"></a>Запрос 2
```
GET /certificatemanagement/api/v1.0/smartcards/17cf063d-e337-4aa9-a822-346554ddd3c9 HTTP/1.1
```
###<a name="response-2"></a>Ответ 2
```
HTTP/1.1 200 OK

{
    "Uuid":"17cf063d-e337-4aa9-a822-346554ddd3c9",
    "Status":2,
    "Flags":1,
    "ParentSmartcardUuid":"00000000-0000-0000-0000-000000000000",
    "PrimarySmartcardUuid":"00000000-0000-0000-0000-000000000000",
    "PermanentSmartcardUuid":"00000000-0000-0000-0000-000000000000",
    "AssignedUserUuid":"8f1590dc-d932-4b66-8e68-2e91c5880780",
    "ProfileTemplateUuid":"a039b4d0-5ce8-4eff-8651-181c6576fda3",
    "ProfileTemplateVersion":46,
    "Comment":"",
    "SerialNumber":"{bc88f13f-83ba-4037-8262-46eba1291c6e}",
    "Middleware":"MSBaseCSP",
    "Atr":"3b8d0180fba000000397425446590301c8"
}
```       
##<a name="see-also"></a>См. также

-[Класс Microsoft.Clm.Shared.Smartcards.Smartcard](https://msdn.microsoft.com/library/microsoft.clm.shared.smartcards.smartcard.aspx)
