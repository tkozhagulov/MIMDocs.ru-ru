---
title: Установка службы синхронизации Microsoft Identity Manager | Документация Майкрософт
description: Начните работу с компонентами MIM 2016, установив и настроив службу синхронизации.
keywords: ''
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 05/01/2018
ms.topic: get-started-article
ms.prod: microsoft-identity-manager
ms.assetid: 2585e9c5-ce34-46c7-bdcf-8c08773901dc
ms.reviewer: mwahl
ms.suite: ems
ms.openlocfilehash: cec04cf430ba38ec40b61e4aad68fd8447d13c99
ms.sourcegitcommit: 4f0b2883922bcb8fbef6b4284c35c6ca62c11565
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/27/2019
ms.locfileid: "56952185"
---
# <a name="install-mim-2016-mim-synchronization-service"></a>Установка MIM 2016: Служба синхронизации MIM

> [!div class="step-by-step"]
> [« Exchange Server](prepare-server-exchange.md)
> [Служба и портал MIM »](install-mim-service-portal.md)
> 
> [!NOTE]
> В этом пошаговом руководстве используются примеры имен и значений для компании Contoso. Замените их своими значениями. Пример.
> - Имя контроллера домена — **corpdc**
> - Имя домена — **contoso**.
> - Имя сервера службы MIM — **corpservice**
> - Имя сервера синхронизации MIM — **corpsync**
> - Имя SQL Server — **corpsql**
> - Пароль — <strong>Pass@word1</strong>

Прежде чем устанавливать компоненты Microsoft Identity Manager 2016, необходимо установить пакет установки.

1. Выполните вход с использованием *contoso\miminstall* на сервер, используемый для синхронизации управления идентификацией **corpsync**.

2. Распакуйте пакет установки MIM или подключите образ DVD-диска MIM.  Если у вас нет этого DVD-диска, см. сведения о [лицензировании и скачивании Microsoft Identity Manager](microsoft-identity-manager-licensing.md).

## <a name="install-mim-2016-sp1-synchronization-service"></a>Установка MIM 2016 с пакетом обновления 1 (SP1): служба синхронизации

1. Перейдите в папку установки MIM и откройте папку **Synchronization Service** .

2. Запустите **программу установки службы синхронизации MIM**. Следуйте инструкциям и завершите установку.

3. Нажмите кнопку **Далее**на экране приветствия.

    ![Изображение экрана приветствия для мастера установки MIM](media/install-mim-sync/MIM_Install1.png)

4. Изучите условия лицензионного соглашения и нажмите кнопку **Далее**, чтобы принять их.

5. На экране **Выборочная установка** нажмите кнопку **Далее**.

    ![Изображение для выборочной установки](media/install-mim-sync/MIM_Install2.png)

6. На экране настройки базы данных службы синхронизации выберите следующее.

   1.  SQL Server находится на: **Удаленный компьютер** с именем **corpsql.contoso.com**.

   2.  Экземпляр SQL Server: **Экземпляр по умолчанию**

   ![Изображение для подключения к базе данных](media/install-mim-sync/MIM_Install3.png)

7. Сделайте учетную запись, созданную ранее, учетной записью службы синхронизации.

   1. Учетная запись службы: *MIMSync*

   2. Пароль: <em>Pass@word1</em>

   3. Домен учетной записи службы или имя локального компьютера: *contoso*

   ![Изображение для учетной записи службы](media/install-mim-sync/MIM_Install4.png)

8. Укажите в установщике службы синхронизации MIM нужные группы безопасности.

   1. Администратор = *contoso\MIMSyncAdmins*

   2. Оператор = *contoso\MIMSyncOperators*

   3. Соединитель = *contoso\MIMSyncJoiners*

   4. Обзор соединителя = *contoso\MIMSyncBrowse*

   5. Управление паролями WMI = *contoso\MIMSyncPasswordReset*

   ![Изображение для групп безопасности](media/install-mim-sync/MIM_Install5.png)

9. На экране параметров безопасности установите флажок **Enable firewall rules for inbound RPC communications** (Включить правила брандмауэра для входящих подключений RPC) и нажмите кнопку **Далее**.

10. Нажмите кнопку **Установить**, чтобы начать установку службы синхронизации MIM.

    1. Может появиться предупреждение об учетной записи службы синхронизации MIM, в этом случае нажмите **ОК**.

    2. Служба синхронизации MIM будет установлена.

    3. Появляется уведомление о создании архива ключа шифрования. Нажмите кнопку **OК**, а затем выберите папку для сохранения архива.

        ![Изображение для уведомления об архивации ключа шифрования в службе синхронизации MIM](media/MIM-Install7.png)

    4. После успешного завершения установки нажмите кнопку **Готово**.

    5. Необходимо выйти из системы и снова войти в нее, чтобы изменения членства в группе вступили в силу. Нажмите **Да** для выхода.

> [!div class="step-by-step"]  
> [« Exchange Server](prepare-server-exchange.md)
> [Служба и портал MIM »](install-mim-service-portal.md)
