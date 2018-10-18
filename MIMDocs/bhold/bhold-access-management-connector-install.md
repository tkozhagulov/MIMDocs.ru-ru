---
title: Установка соединителя управления доступом BHOLD | Документация Майкрософт
description: Модуль соединителя BHOLD поддерживает первоначальную и постоянную синхронизацию данных.
keywords: ''
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 09/07/2017
ms.topic: article
ms.prod: microsoft-identity-manager
ms.assetid: ''
ms.openlocfilehash: 60886a84c6105e94a2cd3d42f17b86b2d69c8c0a
ms.sourcegitcommit: 7de35aaca3a21192e4696fdfd57d4dac2a7b9f90
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/16/2018
ms.locfileid: "49358607"
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

## <a name="next-steps"></a>Дальнейшие шаги

- [Установка модуля BHOLD FIM Integration](https://technet.microsoft.com/library/jj134093(v=ws.10).aspx). Чтобы включить самостоятельную работу пользователей с ролями, можно установить модуль BHOLD FIM Integration.
- [Руководство по установке BHOLD](bhold-installation-guide.md)
- [Справочник разработчика BHOLD](../reference/mim2016-bhold-developer-reference.md)
- [Журнал версий BHOLD](../reference/version-bhold-history.md)
