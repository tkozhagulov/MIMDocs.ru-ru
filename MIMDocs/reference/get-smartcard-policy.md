---
title: "Получение политики смарт-карты | Документация Майкрософт"
description: 
keywords: 
author: msmbaldwin
ms.author: mbaldwin
manager: mbaldwin
ms.date: 10/17/2016
ms.topic: article
ms.prod: microsoft-identity-manager
ms.service: microsoft-identity-manager
ms.technology: security
ms.assetid: c015ffc7-5c94-427e-a3b3-870ec8ab92b6
audience: developer
ms.reviewer: mwahl
ms.suite: ems
ms.openlocfilehash: 1164795e81ff0ef2f93086144b721e760f8dd028
ms.sourcegitcommit: 02fb1274ae0dc11288f8bd9cd4799af144b8feae
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/13/2017
---
# <a name="get-smartcard-policy"></a>Получение политики смарт-карты

Получает политику шаблона профиля для указанного рабочего процесса. Эти данные используются при создании запроса. Политика рабочих процессов указывает, какие данные необходимы клиенту для создания запроса. Эти данные могут включать: различные элементы коллекции данных, примечания к запросам и политику одноразового пароля.

**Примечание**. URL-адреса, приведенные в этом разделе, относятся к имени узла, выбранному во время развертывания API. Например: `https://api.contoso.com`.
##<a name="request"></a>Запрос


Метод  |URL-адрес запроса  
---------|---------
GET     |/CertificateManagement/api/v1.0/profiletemplates/{id}/policy/workflow/{type}

###<a name="url-parameters"></a>Параметры URL-адресов
Параметр| Описание
--------|-------------
id| Обязательный параметр. Идентификатор GUID, соответствующий шаблону профиля, из которого извлекается политика.
type| Обязательный параметр. Тип запрашиваемой политики. Возможны следующие значения: *Enroll*, *Duplicate*, *OfflineUnblock*, *OnlineUpdate*, *Renew*, *Recover*, *RecoverOnBehalf*, *Reinstate*, *Retire*, *Revoke*, *TemporaryEnroll*, *Unblock*.

###<a name="request-headers"></a>Заголовки запроса
Распространенные заголовки запросов см. в таблице c [заголовками HTTP-запросов и ответов](certificate-management-rest-api-service-details.md#http-request-and-response-headers) в статье *CM REST API Service Details* (Сведения о REST API управления сертификатами).
###<a name="request-body"></a>Текст запроса
отсутствуют

##<a name="response"></a>Ответ
###<a name="response-codes"></a>Коды ответа
код  |Описание  
---------|---------
200     | ОК
403 | Запрещено
204 | Нет содержимого
500 | Внутренняя ошибка

###<a name="response-headers"></a>Заголовки ответа
Распространенные заголовки ответов см. в таблице с [заголовками HTTP-запросов и ответов](certificate-management-rest-api-service-details.md#http-request-and-response-headers) в статье *CM REST API Service Details* (Сведения о REST API управления сертификатами).
###<a name="response-body"></a>Текст ответа
В случае успешного выполнения возвращается объект политики на основе объекта [ProfileTemplatePolicy](https://msdn.microsoft.com/library/windows/desktop/microsoft.clm.shared.profiletemplates.profiletemplatepolicy.aspx). Как минимум, объект политики будет содержать представленные в следующей таблице свойства, но также может включать дополнительные свойства, в зависимости от запрашиваемой политики. Например, запрос политики регистрации вернет объект [EnrollPolicy](https://msdn.microsoft.com/library/windows/desktop/microsoft.clm.shared.profiletemplates.enrollpolicy). Дополнительные сведения см. в документации по объекту политики, связанному с параметром {type} в запросе. Сведения о различных типах объектов политики можно найти в документации по [пространству имен Microsoft.Clm.Shared.ProfileTemplates](https://msdn.microsoft.com/library/windows/desktop/microsoft.clm.shared.profiletemplates).

Свойство | Описание
---------|------------
ApprovalsNeeded | Число подтверждений, необходимое для запросов политики FIM CM.
AuthorizedApprover | Дескриптор безопасности для пользователей, имеющих право на утверждение запросов политики FIM CM.
AuthorizedEnrollmentAgent | Дескриптор безопасности для пользователей, которые могут выступать в качестве агентов регистрации для политики.
AuthorizedInitiator | Дескриптор безопасности для пользователей, которые могут отправлять запросы FIM CM для политики.
CollectComments | Логическое значение, указывающее, включен ли сбор комментариев для запросов политики FIM CM.
CollectЗапросPriority | Логическое значение, указывающее, включен ли сбор приоритетов запросов для запросов политики FIM CM.
DefaultЗапросPriority | Приоритет по умолчанию для запросов FIM CM на политику.
Documents | Документы, настроенные для политики.
Включен | Логическое значение, указывающее, включена ли политика.
EnrollAgentRequired | Логическое значение, указывающее, требуются ли агенты регистрации для запросов политики FIM CM.
OneTimePasswordPolicy | Получает способ распространения запросов политики FIM CM.
Personalization | Параметры персонализации смарт-карт для политики.
PolicyDataCollection | Элементы сбора данных, связанные с политикой.
SelfServiceВключен | Логическое значение, указывающее, включена ли для политики самостоятельная отправка запросов FIM CM.

##<a name="example"></a>Пример

###<a name="request-1"></a>Запрос 1
```
GET /CertificateManagement/api/v1.0/profiletemplates/97CD65FA-AF4B-4587-9309-0DD6BFD8B4E1/policies/enroll HTTP/1.1
```
###<a name="response-1"></a>Ответ 1
```
HTTP/1.1 200 OK

... body coming soon
```       
###<a name="request-2"></a>Запрос 2
```
GET /CertificateManagement/api/v1.0/profiletemplates/97CD65FA-AF4B-4587-9309-0DD6BFD8B4E1/policies/renew HTTP/1.1
```
###<a name="response-2"></a>Ответ 2
```
HTTP/1.1 200 OK

... body coming soon
```       
##<a name="see-also"></a>См. также

- [Класс Microsoft.Clm.Shared.ProfileTemplates.ProfileTemplatePolicy](https://msdn.microsoft.com/library/windows/desktop/microsoft.clm.shared.profiletemplates.profiletemplatepolicy.aspx)
- [Пространство имен Microsoft.Clm.Shared.ProfileTemplates](https://msdn.microsoft.com/library/windows/desktop/microsoft.clm.shared.profiletemplates.aspx)
