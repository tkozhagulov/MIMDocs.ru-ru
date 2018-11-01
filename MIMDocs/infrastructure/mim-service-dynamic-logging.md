---
title: Динамическое ведение журнала службы MIM | Документация Майкрософт
description: Включение динамического ведения журнала службы MIM без перезапуска службы управления
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 10/29/2018
ms.topic: article
ms.openlocfilehash: e5d8bcc640ad77b71a515b13bcb3bcf6985654f5
ms.sourcegitcommit: 44a2293ff17c50381a59053303311d7db8b25249
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/31/2018
ms.locfileid: "50380091"
---
# <a name="mim-sp1-4414360--service-dynamic-logging"></a>Динамическое ведение журнала службы MIM с пакетом обновления 1 (SP1) (4.4.1436.0)

В версии 4.4.1436.0 мы представили новую возможность ведения журнала. Она позволит администратору и инженерам службы поддержки включать ведение журнала без перезапуска службы управления.

После установки вы увидите следующую новую строку в вызванном Microsoft.ResourceManagement.Service.exe.config

*   Строка 6: ``<section name="dynamicLogging" type="Microsoft.ResourceManagement.Utilities.DynamicLoggingSection, Microsoft.ResourceManagement.Service" />``
*   Строка 8: ``<dynamicLogging mode="true" loggingLevel="Verbose" />``
*   Строка 266: ``</system.diagnostics> ``

![В выделенных разделах показаны новые записи динамического ведения журнала.](media/mim-service-dynamic-logging/screen01.png)

Уровни ведения журнала можно найти [здесь](https://msdn.microsoft.com/library/ms733025(v=vs.110).aspx#Anchor_3).

- Критические — служба уровня по умолчанию будет записывать только критические события
- Введите в строке 8 (dynamicLogging mode="true" loggingLevel="Critical") предпочтительное значение для ведения журнала.

Конфигурация динамического ведения журнала, расположенная в строке 266: Microsoft.ResourceManagement.Service.exe.config

![В выделенных разделах показаны строки с разными областями ведения журнала.](media/mim-service-dynamic-logging/screen02.png)

По умолчанию расположение для ведения журнала — папка **C:\Program Files\Microsoft Forefront Identity Manager\2010\Service. Учетной записи службы FIM потребуется разрешение на запись, чтобы создать в этом расположении динамический журнал.

![Расположение папки журналов](media/mim-service-dynamic-logging/screen03.png)

> [!NOTE]
>  В случае непредвиденных ошибок (синтаксических или других ошибок в файле конфигурации Microsoft.ResourceManagement.Service.exe.config) соответствующее сообщение об ошибке будет записано в файл Microsoft.ResourceManagement.Service.exe_Emergency.log с путем %TMP%, %TEMP% или %USERPROFILE% (любой из существующих).  
> 1. "%TMP%\Microsoft.ResourceManagement.Service.exe_Emergency.log"
> 2. "%TEMP%\Microsoft.ResourceManagement.Service.exe_Emergency.log"
> 3. "% USERPROFILE %\Microsoft.ResourceManagement.Service.exe_Emergency.log"

Чтобы просмотреть трассировку, используйте [средство просмотра трассировки службы](https://msdn.microsoft.com//library/aa751795(v=vs.110).aspx).

 ![Снимок экрана средства просмотра трассировки службы](media/mim-service-dynamic-logging/screen04.png)

# <a name="updates-build-45xx-or-greater"></a>Обновления: сборка 4.5.x.x или более поздней версии

В сборке 4.5.x.x мы доработали функцию ведения журнала и теперь по умолчанию используется уровень журнала **Предупреждение**. Служба записывает сообщения в два файла (у которых перед расширением добавляются индексы 00 и 01). Эти файлы размещаются в папке C:\Program Files\Microsoft Forefront Identity Manager\2010\Service. Когда размер файла превышает максимально допустимый, служба начинает запись в другой файл. Если тот файл уже существует, он будет перезаписан. По умолчанию максимальный размер файла составляет 1 ГБ. Чтобы изменить максимальный размер по умолчанию, добавьте для прослушивателя параметр **maxOutputFileSizeKB** со значением максимального размера файла в КБ (см. пример ниже) и перезапустите службу MIM. При запуске служба добавляет журналы в новый файл (а если его размер превышает максимальный, то перезаписывает более старый файл). 

> [!NOTE] 
> Так как служба проверяет размер файла только до записи очередного сообщения, фактический размер файла может оказаться больше, чем максимально допустимый, на размер одного сообщения. По умолчанию размер всех журналов может достигать около 6 ГБ (три прослушивателя, каждый из которых создает два файла размером 1 ГБ).

> [!NOTE] 
> Учетная запись службы должна иметь разрешения на запись в каталог C:\Program Files\Microsoft Forefront Identity Manager\2010\Service. Если учетная запись службы не имеет таких прав, файлы не будут созданы.

Пример настройки максимального размера файлов в 200 МБ (200 * 1024 КБ) для файлов SVCLOG и 100 МБ (100 * 1024 КБ) для файлов TXT.

`<add initializeData="Microsoft.ResourceManagement.Service_tracelog.svclog" type="Microsoft.IdentityManagement.CircularTraceListener.CircularXmlTraceListener, Microsoft.IdentityManagement.CircularTraceListener, PublicKeyToken=31bf3856ad364e35" name="ServiceModelTraceListener" traceOutputOptions="LogicalOperationStack, DateTime, Timestamp, ProcessId, ThreadId, Callstack" maxOutputFileSizeKB="204800">`
