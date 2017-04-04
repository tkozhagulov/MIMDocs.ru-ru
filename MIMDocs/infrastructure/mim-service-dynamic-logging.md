---
title: "Динамическое ведение журнала службы MIM | Документация Майкрософт"
description: "Включение динамического ведения журнала службы MIM без перезапуска службы управления"
keywords: 
author: barclayn
ms.author: barclayn
manager: mbaldwin
ms.date: 03/24/2017
ms.topic: article
ms.service: microsoft-identity-manager
ms.technology: active-directory-domain-services
ms.assetid: 
translationtype: Human Translation
ms.sourcegitcommit: 90a0f144b7674bbfaf13138dfd926dbfc3c74f28
ms.openlocfilehash: ddd707210d5cd6b618709a477d40e7771d73cfa1
ms.lasthandoff: 03/27/2017



---
# <a name="mim-sp1-4414360--service-dynamic-logging"></a>Динамическое ведение журнала службы MIM с пакетом обновления 1 (SP1) (4.4.1436.0)
В версии 4.4.1436.0 мы представили новую возможность ведения журнала. Она позволит администратору и инженерам службы поддержки включать ведение журнала без перезапуска службы управления.

После установки вы увидите следующую новую строку в вызванном Microsoft.ResourceManagement.Service.exe.config

*    Строка 6: ``<section name="dynamicLogging" type="Microsoft.ResourceManagement.Utilities.DynamicLoggingSection, Microsoft.ResourceManagement.Service" />``
*    Строка 8: ``<dynamicLogging mode="true" loggingLevel="Verbose" />``
*    Строка 266: ``</system.diagnostics> ``

![В выделенных разделах показаны новые записи динамического ведения журнала.](/media/mim-service-dynamic-logging/screen01.png)

Уровни ведения журнала можно найти [здесь](https://msdn.microsoft.com/library/ms733025(v=vs.110).aspx#Anchor_3).

- Критические — служба уровня по умолчанию будет записывать только критические события
- Введите в строке 8 (dynamicLogging mode="true" loggingLevel="Critical") предпочтительное значение для ведения журнала.

Конфигурация динамического ведения журнала, расположенная в строке 266: Microsoft.ResourceManagement.Service.exe.config

![В выделенных разделах показаны строки с разными областями ведения журнала.](/media/mim-service-dynamic-logging/screen02.png)

По умолчанию расположение для ведения журнала — папка **C:\Program Files\Microsoft Forefront Identity Manager\2010\Service**. Учетной записи службы FIM потребуется разрешение на запись, чтобы создать в этом расположении динамический журнал.

![Расположение папки журналов](/media/mim-service-dynamic-logging/screen03.png)

 >[!NOTE]
 В случае непредвиденных ошибок (синтаксических или других ошибок в файле конфигурации Microsoft.ResourceManagement.Service.exe.config) соответствующее сообщение об ошибке будет записано в файл Microsoft.ResourceManagement.Service.exe_Emergency.log с путем %TMP%, %TEMP% или %USERPROFILE% (любой из существующих).  
1. "%TMP%\Microsoft.ResourceManagement.Service.exe_Emergency.log"
2. "%TEMP%\Microsoft.ResourceManagement.Service.exe_Emergency.log"
3. "% USERPROFILE %\Microsoft.ResourceManagement.Service.exe_Emergency.log"

Чтобы просмотреть трассировку, используйте [средство просмотра трассировки службы](https://msdn.microsoft.com//library/aa751795(v=vs.110).aspx).

 ![Снимок экрана средства просмотра трассировки службы](/media/mim-service-dynamic-logging/screen04.png)

