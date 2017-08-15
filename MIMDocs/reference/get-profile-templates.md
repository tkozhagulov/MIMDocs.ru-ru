---
title: "Получение шаблонов профилей | Документация Майкрософт"
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
ms.assetid: b7d8ed76-168b-4cb8-b87c-cdb0976c179a
audience: developer
ms.reviewer: mwahl
ms.suite: ems
ms.openlocfilehash: 8736b328926445f6434bd037a1ecf2e5de9ee466
ms.sourcegitcommit: 02fb1274ae0dc11288f8bd9cd4799af144b8feae
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/13/2017
---
# <a name="get-profile-templates"></a>Получение шаблонов профилей
Получает список шаблонов профилей, которые может зарегистрировать пользователь. Этот метод возвращает ограниченное представление шаблона профиля. Возвращаемых данных о шаблонах профилей должно быть достаточно, чтобы запрашивающий пользователь мог решить, какие шаблоны профилей нужно зарегистрировать. Если не указаны рабочий процесс и разрешения, будут возвращены все шаблоны профилей, видимые пользователю.

**Примечание**. URL-адреса, приведенные в этом разделе, относятся к имени узла, выбранному во время развертывания API. Например: `https://api.contoso.com`.
##<a name="request"></a>Запрос


Метод  |URL-адрес запроса  
---------|---------
GET     |/ CertificateManagement/api/v1.0/profiletemplates? \[targetuser\] 

###<a name="url-parameters"></a>Параметры URL-адресов
Параметр| Описание
--------|-------------
targetuser| Необязательный параметр. Задает целевого пользователю, для которого нужно вернуть шаблон профиля. Если он не указан, будет использоваться удостоверение текущего пользователя. <br/>**Примечание**. В настоящее время поддерживается только текущий пользователь.

###<a name="request-headers"></a>Заголовки запроса
Распространенные заголовки запросов см. в статье о службе.
###<a name="request-body"></a>Текст запроса
отсутствуют

##<a name="response"></a>Ответ
###<a name="response-codes"></a>Коды ответа
код  |Описание  
---------|---------
200     | ОК
204 | Нет содержимого
500 | Внутренняя ошибка

###<a name="response-headers"></a>Заголовки ответа
Распространенные заголовки ответов см. в статье о службе.
###<a name="response-body"></a>Текст ответа
В случае успешного выполнения возвращается список объектов ProfileTemplateLimitedView со следующими свойствами.

Свойство| Type| Описание
--------|-----|--------
Название| строка| Отображаемое имя шаблона профиля.
Описание| строка| Описание шаблона профиля.
Uuid| GUID| Идентификатор шаблона профиля.
IsSmartcardProfileTemplate| bool| Указывает, является ли шаблон шаблоном профиля смарт-карты.
IsVirtualSmartcardProfileTemplate| bool| Указывает, требует ли шаблон профиля наличия виртуальной смарт-карты.

##<a name="example"></a>Пример

###<a name="request"></a>Запрос
```
GET /certificatemanagement/api/v1.0/profiletemplates HTTP/1.1
```
###<a name="response"></a>Ответ
```
HTTP/1.1 200 OK

[
    {
        "Name":"FIM CM Sample Profile Template",
        "Description":"Description of the template goes here",
        "Uuid":"12bd5120-86a2-4ee1-8d05-131066871578",
        "IsSmartcardProfileTemplate":false,
        "IsVirtualSmartcardProfileTemplate":false
    },
    {
        "Name":"FIM CM Sample Smart Card Logon Profile Template",
        "Description":"Description of the template goes here",
        "Uuid":"2b7044cf-aa96-4911-b886-177947e9271b",
        "IsSmartcardProfileTemplate":true,
        "IsVirtualSmartcardProfileTemplate":false
    }
]

```       
