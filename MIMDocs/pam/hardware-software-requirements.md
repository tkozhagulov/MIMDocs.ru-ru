---
title: "Требования к программному обеспечению PAM | Документация Майкрософт"
description: "Требования к оборудованию и программному обеспечению для успешного развертывания Privileged Access Management"
keywords: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 03/15/2017
ms.topic: article
ms.service: microsoft-identity-manager
ms.technology: active-directory-domain-services
ms.assetid: 82a9085c-9667-4b3b-8079-657eab1d1e58
ms.reviewer: mwahl
ms.suite: ems
ms.openlocfilehash: 2985215821db843d2f90d8a34250a8ca6a84b592
ms.sourcegitcommit: 02fb1274ae0dc11288f8bd9cd4799af144b8feae
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/13/2017
---
# Требования к оборудованию и программному обеспечению
<a id="hardware-and-software-requirements" class="xliff"></a>

Privileged Access Management не имеет требований к оборудованию, выходящих за рамки требований к базовой платформе программного обеспечения. Просто убедитесь, что имеется достаточно памяти или места на диске и сетевое подключение.

В этой статье описываются минимальные требования к базовому развертыванию. Она не рассчитана на то, чтобы демонстрировать высокую производительность, масштабируемость или высокий уровень доступности. Кроме того, она не является топологией развертывания, обязательной для больших предприятий или рабочих сред.

## Установка с помощью комплектов программного обеспечения
<a id="installing-from-software-packages" class="xliff"></a>

Следующее программное обеспечение можно загрузить из центра оценки TechNet или из MSDN:  
- Microsoft Identity Manager 2016
  - Служба и портал: содержит установщик для службы и портала MIM, а также для сценария PAM
  - Надстройки и расширения: содержит установщик для командлетов PowerShell запросившей стороны

Из GitHub можно загрузить следующее программное обеспечение:  
- PAMSamplePortal: содержит образец веб-приложения для API REST

## Требуемое программное обеспечение
<a id="required-software" class="xliff"></a>

- Windows Server 2012 R2  
- Windows 8.1 Корпоративная или Windows 10 Корпоративная  
- SQL Server 2012 с пакетом обновления 1 (SP1) или SQL Server 2014  

## Ознакомительная версия программного обеспечения
<a id="evaluation-software" class="xliff"></a>

Если у вас нет лицензий для Windows, SQL Server или Windows Server, загрузите ознакомительные версии программного обеспечения.

### Центр оценки TechNet
<a id="technet-evaluation-center" class="xliff"></a>

- [Windows Server 2012 R2](https://www.microsoft.com/evalcenter/evaluate-windows-server-2012-r2)  
- [Windows 8.1 Enterprise](https://www.microsoft.com/evalcenter/evaluate-windows-8-1-enterprise)  
- [Windows 10 Корпоративная](https://www.microsoft.com/evalcenter/evaluate-windows-10-enterprise)  

### Центре загрузки Майкрософт
<a id="microsoft-download-center" class="xliff"></a>

- [SQL Server](https://www.microsoft.com/download/details.aspx?id=29066)  
- [SharePoint Foundation 2013 с пакетом обновления 1 (SP1) и его обязательные компоненты](https://www.microsoft.com/download/details.aspx?id=42039)

## Требования к оборудованию
<a id="hardware-requirements" class="xliff"></a>

Проверьте системные требования каждого компонента управления привилегированным доступом.

Для CORPDC:  
- [Windows Server 2012 R2](https://technet.microsoft.com/library/dn303418.aspx) или более ранняя версия

Для CORPWKSTN:  
- [Windows 8.1](http://windows.microsoft.com/windows-8/system-requirements)

Для PRIVDC:  
- [Windows Server 2012 R2](https://technet.microsoft.com/library/dn303418.aspx)

Для PAMSRV:
- [Windows Server 2012 R2](https://technet.microsoft.com/library/dn303418.aspx)  
- [SQL Server 2012](https://msdn.microsoft.com/library/ms143506(sql.110).aspx) или [SQL Server 2014](https://msdn.microsoft.com/en-us/library/ms143506(v=sql.120).aspx)
