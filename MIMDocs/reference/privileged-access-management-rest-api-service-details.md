---
title: "Сведения о службе REST API PAM | Документация Майкрософт"
description: 
keywords: 
author: msmbaldwin
ms.author: mbaldwin
manager: mbaldwin
ms.date: 10/17/2016
ms.topic: article
ms.prod: identity-manager-2015
ms.service: microsoft-identity-manager
ms.technology: security
ms.assetid: 54c78bbd-8da1-42ff-9edc-47d913011941
audience: developer
ms.reviewer: mwahl
ms.suite: ems
ms.openlocfilehash: 6e248ba4a65e75b1e914c61de70072c7e094123a
ms.sourcegitcommit: 02fb1274ae0dc11288f8bd9cd4799af144b8feae
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/13/2017
---
# <a name="pam-rest-api-service-details"></a>Сведения о службе API REST PAM
Ниже описывается интерфейс API REST управления привилегированным доступом (PAM) диспетчера удостоверений Майкрософт (MIM).

## <a name="http-request-and-response-headers"></a>Заголовки HTTP-запросов и ответов

HTTP-запросы, адресованные API, должны содержать следующие заголовки (это неисчерпывающий список):

Заголовок | Описание
-------|------------
Авторизация | Обязательный параметр. Содержимое будет зависеть от метода проверки подлинности, который можно настроить и который может быть основан на WIA (встроенная проверка подлинности Windows) или службах федерации Active Directory.
Content-Type | Требуется, если в запросе есть текст. Должно быть задано как "application/json".
Content-Length | Требуется, если в запросе есть текст. 
Файл cookie | Файл cookie данного сеанса. Может потребоваться в зависимости от метода проверки подлинности.
<br/>
HTTP-ответы содержат следующие заголовки (это неисчерпывающий список):

Header | Описание
-------|------------
Content-Type | API всегда возвращает значение "application/json".
Content-Length | Длина текста запроса, если он имеется, в байтах.

## <a name="versioning"></a>Управление версиями 
Текущая версия интерфейса API — 1. Версию API можно указать с помощью параметра запроса в URL-адресе запроса, как показано в следующем примере: `http://localhost:8086/api/pamresources/pamrequests?v=1` Если в запросе версия не указана, запрос выполняется для последней выпущенной версии API-интерфейса. 

## <a name="security"></a>Безопасность 
Для доступа к API требуется встроенная проверка подлинности Windows (IWA). Эти параметры необходимо настроить вручную в службах IIS перед установкой диспетчера удостоверений Майкрософт (MIM).

Протокол HTTPS (TLS) поддерживается, но его нужно настроить в службах IIS вручную. Подробнее: **Implement Secure Sockets Layer (SSL) for the FIM Portal** (Реализация протокола SSL для портала FIM) в разделе [Step 9: Perform FIM 2010 R2 Post-Installation Tasks] (Шаг 9. Выполнение задач после установки FIM 2010 R2)(https://technet.microsoft.com/library/hh322875(v=ws.10%29.aspx) руководства по лаборатории тестирования "Installing FIM 2010 R2" (Установка FIM 2010 R2). 

Вы можете создать новый сертификат SSL-сервера, выполнив следующую команду в командной строке Visual Studio:
```
Makecert -r -pe -n CN="test.cwap.com" -b 05/10/2014 -e 12/22/2048 -eku 1.3.6.1.5.5.7.3.1 -ss my -sr localmachine -sky exchange -sp "Microsoft RSA SChannel Cryptographic Provider" -sy 12
```
 
Эта команда создает самозаверяющий сертификат, с помощью которого можно проверить веб-приложение, использующее протокол SSL на веб-сервере с URL-адресом test.cwap.com. OID, заданный в параметре -eku, определяет сертификат как сертификат SSL-сервера. Сертификат размещается в личном хранилище и доступен на уровне компьютера, поэтому его можно экспортировать из оснастки "Сертификаты" в mmc.exe

## <a name="cross-domain-access-cors"></a>Междоменный доступ (CORS) 
CORS поддерживается, но его нужно настроить в службах IIS вручную. Добавьте следующие элементы в развернутый файл web.config интерфейса API, чтобы разрешить междоменные вызовы: 

```
<system.webServer>       
    <httpProtocol> 
        <customHeaders> 
            <add name="Access-Control-Allow-Credentials" value="true"  /> 
            <add name="Access-Control-Allow-Headers" value="content-type" /> 
            <add name="Access-Control-Allow-Origin" value="http://<hostname>:8090" /> 
        </customHeaders> 
    </httpProtocol> 
</system.webServer> 
```
<br/>

## <a name="error-handling"></a>Обработка ошибок 
Интерфейс API возвращает сообщения об ошибках HTTP для описания ошибок. Ошибки совместимы с OData. В следующей таблице показаны коды ошибок, которые могут быть возвращены клиенту.

Код состояния HTTP | Описание
-----------------|------------
401 | Недостаточно прав 
403 | Запрещено 
408 | Время ожидания запроса   
500 | Внутренняя ошибка сервера 
503 | Служба недоступна 
<br/>

## <a name="filtering"></a>Фильтрация 
Запросы API-интерфейса REST PAM могут содержать фильтры для указания свойств, которые необходимо включить в ответ. Синтаксис фильтра основан на выражениях OData.

Фильтры могут определять любые из свойств запросов, ролей или ожидающих запросов PAM. Например: *ExpirationTime*, *DisplayName*или любое допустимое свойство запроса, роли или ожидающего запроса PAM.

API-интерфейс поддерживает следующие операторы в выражениях фильтра: *And*, *Equal*, *NotEqual*, *GreaterThan*, *LessThan*, *GreaterThenOrEqueal*и *LessThanOrEqual*. 

Следующий пример запросов содержит фильтры:

- Этот запрос возвращает все запросы PAM в заданном диапазоне дат: `http://localhost:8086/api/pamresources/pamrequests?$filter=ExpirationTime gt datetime"2015-01-09T08:26:49.721Z" and ExpirationTime lt datetime"2015-02-10T08:26:49.722Z" `
 
- Этот запрос возвращает роль PAM с отображаемым именем "Доступ к файлам SQL": `http://localhost:8086/api/pamresources/pamroles?$filter=DisplayName eq "SQL File Access" `
