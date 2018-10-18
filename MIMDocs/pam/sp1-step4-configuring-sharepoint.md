---
title: Шаг 4. Настройка SharePoint
description: В этой статье описывается шаг 4 настройки PAM с помощью скриптов. На этом шаге настраивается среда SharePoint, которая будет использоваться в рамках развертывания PAM.
keywords: ''
author: barclayn
ms.author: barclayn
manager: MBaldwin
ms.date: 08/18/2017
ms.topic: article
ms.prod: microsoft-identity-manager
ms.technology: active-directory-domain-services
ms.assetid: 4b524ae7-6610-40a0-8127-de5a08988a8a
ms.reviewer: ''
ms.suite: ems
ms.openlocfilehash: af91fc1283e8576b38dcfef3deda2d2da6eed24e
ms.sourcegitcommit: ace4d997c599215e46566386a1a3d335e991d821
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/15/2018
ms.locfileid: "49333213"
---
# <a name="step-4-configuring-sharepoint"></a>Шаг 4. Настройка SharePoint

> [!div class="step-by-step"]
> [« Шаг 3](sp1-step3-installing-configuring-sql.md)
> [Шаг 5 »](sp1-step5-configuring-pam.md)

Версия SharePoint должна быть не ниже SharePoint Foundation 2013 с пакетом обновления 1 (SP1).

Имя для входа на присоединенные к домену серверы — MIMAdmin.

1. Запустите PowerShell от имени администратора.
2.  .\PAMDeployment.ps1.
3.  Выберите пункт 4 меню (Установка SharePoint).


Для серверов рабочих групп

1. Запустите PowerShell от имени администратора.
2.  cd $env:SYSTEMDRIVE\PAM.
3.  .\PAMDeployment.ps1.
4. Выберите пункт 4 меню (Установка SharePoint).

В процессе установки SharePoint компьютер будет перезагружаться несколько раз. Каждый раз необходимо повторно запускать программу установки SharePoint, выполнив вход от имени учетной записи MIMAdmin.
Если компьютер, на который выполняется установка SharePoint, не имеет подключения к Интернету для загрузки необходимых компонентов, их можно скачать отдельно и поместить в локальную папку. **Путь к этой локальной папке необходимо обновить в файле PAMConfiguration.xml в расположении <PrerequisitesBinaryLocation/>.** В Приложении 5 содержатся ссылки для скачивания файлов.
После установки откроется графический интерфейс конфигурации SharePoint, и нужно будет выполнить пошаговые инструкции для завершения установки SharePoint. Выберите тип "Полный сервер" и последовательно пройдите остальную часть пользовательского интерфейса. После установки вам будет предложено запустить мастер настройки. Выполните указанные ниже действия.

1. На вкладке **Подключение к ферме серверов** выберите пункт **Создать ферму серверов**.
2. Укажите **SQLServer** как сервер баз данных для базы данных конфигурации, а **SharePoint ServiceAccount** — как учетную запись доступа к базе данных для SharePoint.
3. В качестве пароля введите парольную фразу фермы **(он не будет применяться далее).**
4. Примите остальные значения, заданные по умолчанию для параметров мастера настройки SharePoint, чтобы создать ферму из одного сервера.

Подробные сведения можно найти в разделе **Настройка SharePoint** статьи [Шаг 3. Подготовка сервера PAM](/microsoft-identity-manager/pam/step-3-prepare-pam-server). По завершении запустите повторно сценарий \PAMDeployment.ps1 и выберите вариант 4 (Установка SharePoint) для выполнения этого этапа.

> [!div class="step-by-step"]
> [« Шаг 3](sp1-step3-installing-configuring-sql.md)
> [Шаг 5 »](sp1-step5-configuring-pam.md)
