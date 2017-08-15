---
title: "Справочник по REST API службы Privileged Access Management | Документация Майкрософт"
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
ms.assetid: 541854b7-f285-4e8b-bbaf-3f15da69467f
audience: developer
ms.reviewer: mwahl
ms.suite: ems
ms.openlocfilehash: 02de09a7de843cb42080daa4ce43a5a0c74f2c18
ms.sourcegitcommit: 02fb1274ae0dc11288f8bd9cd4799af144b8feae
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/13/2017
---
# <a name="privileged-access-management-rest-api-reference"></a>Справочник по API REST управления привилегированным доступом (PAM)
Диспетчер удостоверений Майкрософт (MIM) 2016 добавляет новый сценарий, который называют управлением привилегированным доступом (PAM). PAM предоставляет организации более строгий контроль над правами доступа привилегированных учетных записей пользователей, таких как администратор систем или служб, к конфиденциальным ресурсам. PAM управляет доступом привилегированных учетных записей, предоставляя права доступа на ограниченное время, по требованию (JIT), когда они необходимы.

Пользователь может запросить у службы MIM привилегированных прав доступа одним из двух способов:

- с помощью API REST PAM;
- с помощью командлета New-PAMRequest PowerShell.

В этом руководстве описывается использование API-интерфейса REST PAM. Подробнее об использовании командлета PowerShell см. в следующем руководстве по лаборатории тестирования: "Демонстрация управления привилегированным доступом с помощью диспетчера удостоверений Майкрософт" (на сайте connect).

##<a name="pam-rest-api-resources-and-operations"></a>Ресурсы и операции API-интерфейса REST PAM
API-интерфейс REST PAM использует следующие ресурсы.
- **Роль PAM**. Роль PAM связывает коллекцию пользователей с набором прав доступа. Права доступа определяются с помощью ссылки на группы безопасности.  У каждой роли PAM есть список учетных записей пользователей, называемых кандидатами, которые имеют право на повышение роли PAM. Вы можете выполнять следующие действия с ролями PAM.

    - [Получение ролей PAM](privileged-access-management-get-roles.md)

- **Запрос PAM**. Пользователь, желающий повысить права доступа роли PAM, должен отправить запрос PAM и получить утверждение запроса для повышения. Объект запроса PAM отслеживает жизненный цикл этого запроса в службе MIM. Вы можете выполнять следующие операции с запросами PAM.

    - [Создание запроса PAM](privileged-access-management-create-request.md)
    - [Получение запроса PAM](privileged-access-management-get-requests.md)
    - [Закрытие запроса PAM](privileged-access-management-close-request.md)

- **Ожидающий запрос PAM**. Используется для утверждения или отклонения запросов PAM, отправленных пользователями. Вы можете выполнять следующие операции с ожидающими запросами PAM.

    - [Получение ожидающего запроса PAM](privileged-access-management-get-pending-requests.md)
    - [Утверждение или отклонение ожидающего запроса PAM](privileged-access-management-approve-reject-pending-request.md)

- **Сеанс PAM**. При использовании API-интерфейса REST PAM клиент (например, браузер) создает сеанс с конечной точкой API. В этом сеансе клиент проходит проверку подлинности на конечной точке API REST. Вы можете выполнять следующие операции с сеансами PAM.

     - [Получение сведений о сеансе PAM](privileged-access-management-get-session-info.md)

Подробные сведения об этой службе см. в статье [Сведения о службе PAM REST API](privileged-access-management-rest-api-service-details.md)

##<a name="pam-sample-portal-on-github"></a>PAM Sample Portal на веб-сайте GitHub
Один из способов узнать, как использовать API-интерфейс REST PAM — использовать PAM sample portal, веб-приложение, который использует API-интерфейс. Код для портала примеров PAM можно найти в [репозитории примеров PAM на сайте GitHub](http://go.microsoft.com/fwlink/?LinkID=618550&clcid=0x409). Развертывание примера описывается в руководстве по лаборатории тестирования PAM.
