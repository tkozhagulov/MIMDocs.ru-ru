---
title: "Сценарии развертывания PAM в MIM2016 SP1"
description: "Эта страница входит в серию статей о настройке диспетчера привилегированных удостоверений с помощью скриптов. Она включает список допущений относительно среды."
keywords: 
author: barclayn
ms.author: barclayn
manager: MBaldwin
ms.date: 01/10/2017
ms.topic: article
ms.service: microsoft-identity-manager
ms.technology: active-directory-domain-services
ms.assetid: 4b524ae7-6610-40a0-8127-de5a08988a8a
ms.reviewer: 
ms.suite: ems
ms.translationtype: Human Translation
ms.sourcegitcommit: 3797f5789bb4e48836eb21776dafd5a2e0e11613
ms.openlocfilehash: 12c60e12dc5662ff0313e21bb9180b3709969af6
ms.contentlocale: ru-ru
ms.lasthandoff: 05/09/2017


---

# <a name="mim2016-sp1-pam-deployment-scripts"></a>Сценарии развертывания PAM в MIM2016 SP1

В этом пакете обновления мы представляем набор сценариев развертывания для упрощения развертывания PAM. Эти сценарии доступны в центре загрузки. Прежде чем пытаться использовать сценарии, важно убедиться, что перечисленные ниже предположения применяются в вашей среде.

Важные предположения
1. На всех компьютерах установлена операционная система Windows Server 2012 R2 или более поздней версии. Если вы используете ознакомительную версию Windows Server 2016 Technical Preview 5, необходимо установить контроллер домена PRIV сборки TP5.
2. DNS необходимо настроить таким образом, чтобы разрешение имен между контроллерами домена и серверами компонентов выполнялось автоматически.
3. Двоичные файлы установки должны быть доступны локально на назначенных серверах для установки SQL, SharePoint и MIM.
4. В среде есть три выделенных (физических или виртуальных) машины, на которых независимо выполняются CORPDC, PRIVDC и PAMSERVER.
5. В целях проверки для выполнения этого шага предполагается наличие выделенного клиентского компьютера.

>[!NOTE]
>Если возникнут какие-либо проблемы с выполнением сценариев, необходимо просмотреть журналы. Все журналы сценариев сохраняются в расположении %AppData%\MIMPAMInstall. Выполните сжатие папки и полученный ZIP-файл отправьте по адресу электронной почты mim2016@microsoft.com вместе со сведениями об операции и ошибке.

Готовы начать работу со сценариями развертывания PAM? Начните с [настройки PAM с помощью сценариев](./pam/sp1-pam-configure-using-scripts.md).
