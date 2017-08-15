---
title: "Возвращение параметров для создания запроса на сертификат | Документация Майкрософт"
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
ms.assetid: 36bd1fc9-3443-4028-90e7-a24fef0ec0ae
audience: developer
ms.reviewer: mwahl
ms.suite: ems
ms.openlocfilehash: 5822da1b9cf8558becccff815fd0208923fcaaa0
ms.sourcegitcommit: 02fb1274ae0dc11288f8bd9cd4799af144b8feae
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/13/2017
---
# <a name="get-certificate-request-generation-options"></a>Получение параметров создания запроса сертификата

Возвращает параметры для создания запроса сертификата на стороне клиента.

**Примечание**. URL-адреса, приведенные в этом разделе, относятся к имени узла, выбранному во время развертывания API. Например: `https://api.contoso.com`.
##<a name="request"></a>Запрос


Метод  |URL-адрес запроса  
---------|---------
GET     |/CertificateManagement/api/v1.0/requests/{RequestID}/certificaterequestgenerationoptions

###<a name="url-parameters"></a>Параметры URL-адресов
Параметр | Описание
--------|--------------
RequestID| Обязательный параметр. Идентификатор GUID запроса MIM CM, для которого необходимо получить параметры создания запроса сертификата.

###<a name="request-headers"></a>Заголовки запроса
Распространенные заголовки запросов см. в таблице c [заголовками HTTP-запросов и ответов](certificate-management-rest-api-service-details.md#http-request-and-response-headers) в статье *CM REST API Service Details* (Сведения о REST API управления сертификатами).
###<a name="request-body"></a>Текст запроса
Отсутствуют.


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
В случае успешного выполнения возвращается список объектов CertificateRequestGenerationOptions. Каждый объект CertificateRequestGenerationOptions соответствует одному запросу сертификата, который клиент должен создать, и предоставляет следующие свойства:

Свойство| Описание
--------|-----------
Exportable | Значение, указывающее, можно ли экспортировать закрытый ключ, созданный для запроса.
FriendlyName | Отображаемое имя зарегистрированного сертификата.
HashAlgorithmName | Хэш-алгоритм, используемый при создании подписи запроса сертификата.
KeyAlgorithmName | Алгоритм открытого ключа.
KeyProtectionLevel | Уровень надежной защиты ключа.
KeySize | Размер создаваемого закрытого ключа в битах.
KeyStorageProviderNames | Список допустимых поставщиков хранилища ключей (KSP), которые можно использовать для создания закрытого ключа. Если первый KSP не может использоваться для создания запроса сертификата, может применяться любой из указанных KSP до достижения успеха.
KeyUsages | Операция, которую может выполнить закрытый ключ, созданный для этого запроса сертификата. Значение по умолчанию — Signing.
Субъект | Имя субъекта.

**Примечание**. Подробные сведения об этих свойствах см. в описании [класса Windows.Security.Cryptography.Certificates.CertificateRequestProperties](https://msdn.microsoft.com/library/windows/apps/br212079.aspx), но имейте в виду, что нет однозначного соответствия между этим классом и объектом CertificateRequestGenerationOptions.

##<a name="example"></a>Пример

###<a name="request"></a>Запрос
```
GET /certificatemanagement/api/v1.0/requests/a9b4b42c-cc50-4c9b-89d1-bbc0bcd5a099/certificaterequestgenerationoptions HTTP/1.1

```
###<a name="response"></a>Ответ
```
HTTP/1.1 200 OK

[
    {
        "Subject":"",
        "KeyAlgorithmName":"RSA",
        "KeySize":2048,
        "FriendlyName":"",
        "HashAlgorithmName":"SHA1",
        "KeyStorageProviderNames":[
            "Contoso Smart Card Key Storage Provider"
        ],
        "Exportable":0,
        "KeyProtectionLevel":0,
        "KeyUsages":3
    }
]
```       
