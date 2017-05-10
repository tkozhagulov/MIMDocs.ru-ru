---
title: "Руководство по топологии для развертывания | Документация Майкрософт"
description: "вы можете ознакомиться с общими сведениями о компонентах MIM 2016, а также рекомендациями по их развертыванию в вашей среде."
keywords: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 03/21/2017
ms.topic: article
ms.service: microsoft-identity-manager
ms.technology: security
ms.assetid: 735dc357-dfba-4f68-a5b3-d66d6c018803
ms.reviewer: mwahl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: bfc73723bdd3a49529522f78ac056939bb8025a3
ms.openlocfilehash: f7e4dc737444df70de3a8a78eb518e9e6f26aadc
ms.lasthandoff: 05/02/2017


---


# <a name="topology-considerations"></a>Вопросы по топологии
Компоненты Microsoft Identity Manager (MIM) можно развернуть на том же сервере или на нескольких серверах с разными конфигурациями. Выбранная вами топология влияет на потенциальную производительность MIM. Эта статья описывает несколько топологий развертывания, которые можно реализовать.

## <a name="mim-components"></a>Компоненты MIM
При проектировании топологии развертывания важно знать назначение всех компонентов и механизмы их взаимодействия.

- <a name="mim-portal---an-interface-for-password-resets-group-management-and-administrative-operations"></a>**Портал MIM** — это интерфейс для сброса пароля, управления группами и выполнения административных операций.
    -
- **Служба MIM** — это веб-служба, реализующая функциональность управления удостоверениями MIM 2016.
- **Служба синхронизации MIM** — синхронизирует данные с другими системами идентификации.
- **Microsoft SQL Server** — служба MIM и служба синхронизации MIM хранят свои данные в Базах данных SQL.

В следующей таблице приведены варианты размещения отдельных компонентов MIM. Они могут размещаться на одном компьютере или распределяться по нескольким серверам и кластерам.

| | Портал MIM | Служба MIM | Служба синхронизации MIM | SQL Server |
| --- | --- | --- | --- | --- |
| Один компьютер | да | Да | Да | да |
| Отдельный сервер | да | Да | Да | да |
| Кластер балансировки сетевой нагрузки | да | да | | |
| Кластер SQL Server | | | | да |


## <a name="multitier-topology"></a>Многоуровневая топология
Многоуровневая топология используется чаще всего. Она обеспечивает наибольшую гибкость. Портал MIM, служба MIM и базы данных разделены на уровни и развернуты на нескольких компьютерах. Эта топология повышает гибкость масштабирования для различных компонентов MIM. Например, можно осуществить горизонтальное масштабирование портала MIM, добавив новые серверы в кластер балансировки сетевой нагрузки (NLB). Аналогичным образом можно масштабировать службу MIM, используя кластер балансировки сетевой нагрузки и при необходимости увеличивая число компьютеров (узлов) в нем.

В многоуровневой топологии выделяется отдельный компьютер для размещения каждой Базы данных SQL (одна для службы MIM и другая для службы синхронизации MIM). Масштабируемость производительности компьютеров, где размещены Базы данных SQL, можно увеличить, добавив или модернизировав оборудование, например обновив ЦП, добавив дополнительные ЦП, увеличив объем ОЗУ или обновив модули памяти, а также обновив конфигурации жесткого диска для ускорения чтения и записи и снижения задержки.

![Схема многоуровневой топологии MIM](media/MIM-topo-multitier.png)

При такой конфигурации служба синхронизации MIM и ее базы данных размещаются на одном компьютере. Однако можно добиться сопоставимого уровня производительности при наличии гигабитного выделенного сетевого подключения между службой синхронизации MIM и ее базой данных, размещенных на разных компьютерах.


## <a name="multitier-topology-with-multiple-mim-services"></a>Многоуровневая топология с несколькими службами FIM
Синхронизация данных с внешними системами может занять много времени. Кроме того, эта процедура может увеличить нагрузку на систему. Если настройка синхронизации приводит к запуску политик с рабочими процессами, эти политики конкурируют за ресурсы с рабочими процессами конечных пользователей. Такие проблемы могут быть особенно заметны для рабочих процессов проверки подлинности, таких как сброс пароля, которые выполняются в режиме реального времени, пока пользователь ожидает их завершения. Предоставив один экземпляр службы MIM для операций конечного пользователя и отдельный портал для синхронизации административных данных, вы можете повысить скорость реагирования для операций конечных пользователей.

![Схема нескольких многоуровневых топологий MIM](media/MIM-topo-multitier-multiservice.png)

Как в случае со стандартной многоуровневой топологией, производительность портала MIM можно увеличить, используя кластер балансировки сетевой нагрузки и при необходимости увеличивая число узлов в нем.

Компьютеры SQL Server, где размещается служба синхронизации MIM и база данных службы MIM, сильно влияют на общую производительность развертывания MIM. Следуйте рекомендациям по оптимизации производительности базы данных, приведенным в документации для SQL Server. Дополнительные сведения см. в следующих документах:

## <a name="see-also"></a>См. также
- Скачиваемое [руководство по планированию ресурсов для Forefront Identity Manager (FIM) 2010](http://go.microsoft.com/fwlink/?LinkId=200180) содержит более подробные сведения о тестовой сборке и результатах тестирования производительности.
