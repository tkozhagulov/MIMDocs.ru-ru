---
title: "Установка модуля BHOLD Model Generator | Документация Майкрософт"
description: "Модуль BHOLD Model Generator позволяет структурировать данные из различных источников"
keywords: 
author: barclayn
ms.author: barclayn
manager: mbaldwin
ms.date: 09/07/2017
ms.topic: article
ms.service: microsoft-identity-manager
ms.technology: security
ms.assetid: 
ms.openlocfilehash: 96363fb3b0067ff5c8f8c2f32e9a855464038653
ms.sourcegitcommit: 0d8b19c5d4bfd39d9c202a3d2f990144402ca79c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/14/2017
---
# <a name="bhold-model-generator-installation"></a>Установка модуля BHOLD Model Generator

С помощью модуля BHOLD Model Generator можно структурировать данные из полномочных источников, содержащих сведения пользователей и организации, включая списки управления доступом (ACL), в модель, которая может использоваться в администрировании BHOLD.

## <a name="bhold-model-generator-installation-requirements"></a>Требования к установке модуля Model Generator 

Перед установкой модуля BHOLD Model Generator необходимо установить следующие компоненты.

1. Модуль BHOLD Core на сервере, на котором планируется установить модуль BHOLD Model Generator. Сведения об установке модуля BHOLD Core см. в статье [BHOLD Core Installation](https://technet.microsoft.com/en-us/library/jj134095(v=ws.10).aspx) (Установка модуля BHOLD Core).

2. Должен быть установлен поставщик Microsoft OLE DB для Microsoft Jet. Дополнительные сведения см. в [этой статье](http://support.microsoft.com/kb/271908).

>[!WARNING]
Не устанавливайте модуль BHOLD Model Generator в рабочей сети. Модуль BHOLD Model Generator предназначен для автономного использования в промежуточной среде в целях создания нормализованной модели ролей, которую можно импортировать в корпоративную модель ролей. Запуск модуля BHOLD Model Generator в рабочей сети может привести к потере существующей модели ролей.

## <a name="before-you-begin"></a>Подготовка к работе

Перед установкой модуля BHOLD Model Generator необходимо подготовить сведения, которые потребуются мастеру установки модуля BHOLD Model Generator для завершения установки. Сведения в следующей таблице помогут пройти все шаги мастера. Скачайте

распространяемый пакет Microsoft Access Database Engine 2010

 

*со страницы \<*<http://daipvstf:8080/tfs/ActiveDirectory/IAM/_workitems>*\>*

 

<https://www.microsoft.com/en-us/download/confirmation.aspx?id=13255>

**Параметры учетной записи**

| **Элемент**                                    | **Описание**                                                                                                                                                                                                           | **Значение**                                                                                                                                                                                                                                                                                                            |
|---------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Использовать поставщик безопасности в домене или на компьютере** | Выбранный параметр указывает, что система безопасности доменных служб Active Directory управляет доступом к модулю BHOLD Core.                                                                                                                | Установите требуемый флажок. **Важно**. Если этот флажок не установлен, установка завершится ошибкой.                                                                                                                                                                                                                   |
| **Домен**                                  | Указывает домен, содержащий учетную запись службы, созданную при установке модуля BHOLD Core. Дополнительные сведения см. в статье [BHOLD Core Installation](https://technet.microsoft.com/en-us/library/jj134095(v=ws.10).aspx) (Установка модуля BHOLD Core). | Мастер автоматически задает имя домена. Если имя указано неверно, измените его. **Важно**. Укажите имя домена, используя краткое имя NetBIOS, а не полное доменное имя (FQDN). Например, если полное доменное имя — fabrikam.com, укажите имя домена как FABRIKAM. |
| **User**                                    | Указывает имя входа для учетной записи службы BHOLD Core.                                                                                                                                                          | Запишите имя учетной записи пользователя:                                                                                                                                                                                                                                                                                    |
| **Пароль**                                | Задает пароль для учетной записи пользователя службы.                                                                                                                                                                       | Запишите пароль: **Важно**. Пароль необходимо хранить в безопасном и надежном месте.                                                                                                                                                                                                                  |

**Параметры резервной базы данных**

| Элемент                                        | Описание                                                                                                                                                                                                                                                                                                                                                                                                                  | Значение                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
|---------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Использовать встроенную безопасность**                 | Указывает, что для доступа к базе данных используется проверка подлинности Windows.                                                                                                                                                                                                                                                                                                                                                        | Установите флажок, если для подключения к SQL Server используется проверка подлинности Windows. Снимите флажок, если используется проверка подлинности SQL Server. Если используется проверка подлинности SQL Server, база данных должна быть создана до запуска программы установки BHOLD Core. **Примечание**. Если используется проверка подлинности Windows, необходимо войти в систему с помощью учетной записи с ролью сервера sysadmin на сервере базы данных. **Важно**. Проверку подлинности SQL Server следует использовать только в тестовой среде. Корпорация Майкрософт настоятельно рекомендует использовать проверку подлинности Windows в производственной среде. |
| **Пользователь базы данных** и **Пароль баз данных** | Указывает имя пользователя и пароль пользователя с ролью сервера sysadmin на сервере базы данных. Эти значения указываются только в том случае, если используется проверка подлинности SQL Server.                                                                                                                                                                                                                                                  | Запишите имя пользователя SQL Server: Запишите пароль пользователя SQL Server: </br></br> **Важно**. Пароль необходимо хранить в безопасном и надежном месте.                                                                                                                                                                                                                                                                                                                                                                                                           |
| **Сервер базы данных** и **Имя базы данных**   | Указывает NetBIOS-имя сервера базы данных и имя резервной базы данных, которая будет создана программой установки BHOLD Model Generator. Если вы не использует экземпляр сервера базы данных по умолчанию, укажите экземпляр сервера базы данных в формате *\<сервер\>*\\*\<экземпляр\>*.  Корпорация Майкрософт рекомендует задать имя резервной базы данных с использованием имени BHOLD Core, за которым следует \_BACKUP, например B1_BACKUP. | Запишите имя сервера (или сервер и экземпляр): </br> Запишите имя базы данных:

## <a name="bhold-model-generator-setup"></a>Установка модуля BHOLD Model Generator

Чтобы установить модуль BHOLD Model Generator, войдите в систему как член группы "Администраторы домена", скачайте следующий файл и запустите его от имени администратора на сервере, где вы собираетесь установить модуль BHOLD Core:

- BholdModelGenerator *\<версия\>*\_Release.msi

Замените *\<версия\>* на номер версии устанавливаемого выпуска BHOLD Model Generator.

Чтобы запустить файл программы от имени администратора, щелкните его правой кнопкой мыши и выберите пункт **Запуск от имени администратора**.

## <a name="next-steps"></a>Дальнейшие действия

- Сведения о создании входных файлов см. в [техническом справочнике Microsoft BHOLD Suite](https://technet.microsoft.com/en-us/library/jj134935(v=ws.10).aspx).
- [Руководство по установке BHOLD](bhold-installation-guide.md)
- [Справочник разработчика BHOLD](../reference/mim2016-bhold-developer-reference.md)
- [Журнал версий BHOLD](../reference/version-bhold-history.md)