---
title: "Получение ответа на проверку подлинности смарт-карты | Документация Майкрософт"
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
ms.assetid: e05ec898-06cd-4c17-a4f4-8f3545af0f14
audience: developer
ms.reviewer: mwahl
ms.suite: ems
ms.openlocfilehash: 1c7a6f5e7ebd1e6e4cfc0992607adb91743f343e
ms.sourcegitcommit: 02fb1274ae0dc11288f8bd9cd4799af144b8feae
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/13/2017
---
# <a name="get-smartcard-authentication-response"></a>Получение ответа на проверку подлинности смарт-карты
Операция возвращает ответ на запрос проверки подлинности базового поставщика служб шифрования.

**Примечание**. URL-адреса, приведенные в этом разделе, относятся к имени узла, выбранному во время развертывания API. Например: `https://api.contoso.com`.
##<a name="request"></a>Запрос


Метод  |URL-адрес запроса  
---------|---------
GET     |/CertificateManagement/api/v1.0/requests/{reqid}/smartcards/{scid}/authenticationresponse

###<a name="url-parameters"></a>Параметры URL-адресов
Параметр | Описание
---------|------------
reqid | Обязательный параметр. Идентификатор запроса (для MIM CM).
scid | Обязательный параметр. Идентификатор смарт-карты (для MIM CM). Получается из объекта [Microsoft.Clm.Shared.Smartcards.Smartcard](http://msdn.microsoft.com/library/microsoft.clm.shared.smartcards.smartcard.aspx).
###<a name="query-parameters"></a>Параметры запроса
Параметр | Описание
---------|------------
atr | Опциональный параметр. Строка ATR (Answer-to-reset) смарт-карты.
cardid | Обязательный параметр. Код карты.
challenge | Обязательный параметр. Строка, представляющая запрос, выданный смарт-картой, в кодировке Base 64.
diversified | Обязательный параметр. Логический флаг, обозначающий диверсификацию ключа администратора смарт-карты.


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
В случае успешного выполнения возвращает байтовый BLOB-объект, представляющий ответ на запрос.

##<a name="example"></a>Пример

###<a name="request"></a>Запрос
```
GET /certificatemanagement/api/v1.0/requests/a9b4b42c-cc50-4c9b-89d1-bbc0bcd5a099/smartcards/17cf063d-e337-4aa9-a822-346554ddd3c9/authenticationresponse?cardid=bc88f13f-83ba-4037-8262-46eba1291c6e&challenge=1hFD%2Bcz%2F0so%3D&diversified=False HTTP/1.1

```
###<a name="response"></a>Ответ
```
HTTP/1.1 200 OK

"F0Zudm4wPLY="
```       
##<a name="see-also"></a>См. также

- [Метод Microsoft.Clm.Provision.ExecuteOperations.GetBaseCspResponse](https://msdn.microsoft.com/library/microsoft.clm.provision.executeoperations.getbasecspresponse.aspx)
