---
title: "Установка соединителя управления доступом BHOLD | Документация Майкрософт"
description: "Модуль соединителя BHOLD поддерживает первоначальную и постоянную синхронизацию данных."
keywords: 
author: barclayn
ms.author: barclayn
manager: mbaldwin
ms.date: 09/07/2017
ms.topic: article
ms.service: microsoft-identity-manager
ms.technology: security
ms.assetid: 
ms.openlocfilehash: 6d7f19f470d0c0f82a68652115ab9265a13b3508
ms.sourcegitcommit: ed8dd5563e77ef4a3345b2a52a1426859c95576a
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/15/2017
---
# <a name="access-management-connector-installation"></a>Установка соединителя управления

Модуль соединителя управления доступом BHOLD Suite поддерживает первоначальную и текущую синхронизацию данных с BHOLD. Соединитель управления доступом работает со службой синхронизации Microsoft Identity Manager (MIM), перемещая данные между базой данных BHOLD Core, метавселенной FIM 2010 и целевыми приложениями и хранилищами удостоверений. После установки модуля соединителя управления доступом вы сможете создавать агенты управления FIM, которые контролируют поток данных между BHOLD и MIM.

## <a name="access-management-connector-software-requirements"></a>Требования к программному обеспечению соединителя управления доступом

Перед установкой модуля соединителя управления доступом необходимо установить Microsoft .NET Framework 4. Дополнительные сведения о .NET Framework 4 и инструкции по установке см. на [домашней странице Microsoft .NET](http://www.microsoft.com/net).
Соединитель управления доступом необходимо установить на компьютере под управлением службы синхронизации FIM MIM.

## <a name="access-management-connector-setup"></a>Установка соединителя управления доступом

Чтобы установить модуль соединителя управления доступом, войдите в систему как член группы "Администраторы домена", скачайте следующий файл и запустите его от имени администратора на сервере, где вы собираетесь установить модуль BHOLD FIM Integration.

- AccessManagementConnector.msi

Чтобы запустить файл программы от имени администратора, щелкните его правой кнопкой мыши и выберите пункт **Запуск от имени администратора**.

## <a name="next-steps"></a>Дальнейшие действия

- [Установка модуля BHOLD FIM Integration](https://technet.microsoft.com/library/jj134093(v=ws.10).aspx). Чтобы включить самостоятельную работу пользователей с ролями, можно установить модуль BHOLD FIM Integration.
- [Руководство по установке BHOLD](bhold-installation-guide.md)
- [Справочник разработчика BHOLD](../reference/mim2016-bhold-developer-reference.md)
- [Журнал версий BHOLD](../reference/version-bhold-history.md)