---
title: "Требования к оборудованию и программному обеспечению | Диспетчер удостоверений (Майкрософт)"
description: 
keywords: 
author: kgremban
manager: femila
ms.date: 06/17/2016
ms.topic: article
ms.prod: identity-manager-2015
ms.service: microsoft-identity-manager
ms.technology: active-directory-domain-services
ms.assetid: 82a9085c-9667-4b3b-8079-657eab1d1e58
ms.reviewer: mwahl
ms.suite: ems
ms.sourcegitcommit: a6bdf1b947ee3ebc4c9e89e74b2912697ebf1f60
ms.openlocfilehash: 77e7174e94ea8032c4e57155db489f493ce18177


---

Требования к оборудованию не выходят за рамки базовых требований к платформам операционных систем, достаточному объему памяти, свободному месту на жестком диске и сетевому соединению. В этой статье описываются минимальные требования к базовому развертыванию. Она не рассчитана на то, чтобы демонстрировать высокую производительность, масштабируемость или высокий уровень доступности. Кроме того, она не является топологией развертывания, обязательной для больших предприятий или рабочих сред.

## Установка с помощью комплектов программного обеспечения

Следующее программное обеспечение можно загрузить из центра оценки TechNet или из MSDN:  
- Microsoft Identity Manager 2016
  - Служба и портал: содержит установщик для службы и портала MIM, а также для сценария PAM
  - Надстройки и расширения: содержит установщик для командлетов PowerShell запросившей стороны

Из GitHub можно загрузить следующее программное обеспечение:  
- PAMSamplePortal: содержит образец веб-приложения для API REST

## Требуемое программное обеспечение

- Windows Server 2012 R2  
- Windows 8.1 Корпоративная или Windows 10 Корпоративная  
- SQL Server 2012 с пакетом обновления 1 (SP1) или SQL Server 2014  

## Ознакомительная версия программного обеспечения

Если у вас нет лицензий для Windows, SQL Server или Windows Server, загрузите ознакомительные версии программного обеспечения.

### Центр оценки TechNet

- [Windows Server 2012 R2](https://www.microsoft.com/evalcenter/evaluate-windows-server-2012-r2)  
- [Windows 8,1 Корпоративная](https://www.microsoft.com/evalcenter/evaluate-windows-8-1-enterprise)  
- [Windows 10 Корпоративная](https://www.microsoft.com/evalcenter/evaluate-windows-10-enterprise)  

### Центре загрузки Майкрософт

- [SQL Server](https://www.microsoft.com/download/details.aspx?id=29066)  
- [SharePoint Foundation 2013 с пакетом обновления 1 (SP1) и его обязательные компоненты](https://www.microsoft.com/download/details.aspx?id=42039)

## Требования к оборудованию

Проверьте системные требования каждого компонента управления привилегированным доступом.

Для CORPDC:  
- [Windows Server 2012 R2](https://technet.microsoft.com/library/dn303418.aspx) или более ранняя версия

Для CORPWKSTN:  
- [Windows 8.1](http://windows.microsoft.com/windows-8/system-requirements)

Для PRIVDC:  
- [Windows Server 2012 R2](https://technet.microsoft.com/library/dn303418.aspx)

Для PAMSRV:
- [Windows Server 2012 R2](https://technet.microsoft.com/library/dn303418.aspx)  
- [SQL Server 2012](https://msdn.microsoft.com/library/ms143506(sql.110).aspx) или [SQL Server 2014](https://msdn.microsoft.com/en-us/library/ms143506(v=sql.120).aspx)



<!--HONumber=Jun16_HO3-->


