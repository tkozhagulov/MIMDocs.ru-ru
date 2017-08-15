---
title: "Получение предложенного ПИН-кода смарт-карты | Документация Майкрософт"
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
ms.assetid: ced93932-9912-4b32-9586-ada69b38a796
audience: developer
ms.reviewer: mwahl
ms.suite: ems
ms.openlocfilehash: 08d28819402dd56f996d39aa03b8ac829bef0838
ms.sourcegitcommit: 02fb1274ae0dc11288f8bd9cd4799af144b8feae
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/13/2017
---
# <a name="get-smartcard-proposed-pin"></a>Получение предложенного ПИН-кода смарт-карты
Получает созданный сервером PIN-код пользователя.

**Примечание**. Сервер задаст ПИН-код, только если политика шаблона профиля указывает, что это необходимо. В противном случае его должен указать пользователь.

**Примечание**. URL-адреса, приведенные в этом разделе, относятся к имени узла, выбранному во время развертывания API. Например: `https://api.contoso.com`.
##<a name="request"></a>Запрос


Метод  |URL-адрес запроса  
---------|---------
GET     |/CertificateManagement/api/v1.0/smartcards/{id}/serverproposedpв статье

###<a name="url-parameters"></a>Параметры URL-адресов
Параметр | Описание
---------|------------
id | Идентификатор смарт-карты (для MIM CM). Получается из объекта Microsft.Clm.Shared.Smartcard.
###<a name="query-parameters"></a>Параметры запроса
Параметр | Описание
---------|------------
atr | ATR карты.
cardid | Код карты.
challenge | Строка, представляющая запрос, выданный смарт-картой, в кодировке Base 64.

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
В случае успешного выполнения возвращается строка, представляющая собой PIN-код, предложенный сервером.

##<a name="example"></a>Пример

###<a name="request"></a>Запрос
```
GET GET /CertificateManagement/api/v1.0/smartcards/C6BAD97C-F97F-4920-8947-BE980C98C6B5/serverproposedpin HTTP/1.1
```
###<a name="response"></a>Ответ
```
HTTP/1.1 200 OK

... body coming soon
```       
