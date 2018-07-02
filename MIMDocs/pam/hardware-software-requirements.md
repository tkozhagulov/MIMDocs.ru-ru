---
title: Требования к программному обеспечению PAM | Документация Майкрософт
description: Требования к оборудованию и программному обеспечению для успешного развертывания Privileged Access Management
keywords: ''
author: barclayn
ms.author: barclayn
manager: mbaldwin
ms.date: 09/06/2017
ms.topic: article
ms.service: microsoft-identity-manager
ms.technology: active-directory-domain-services
ms.assetid: 82a9085c-9667-4b3b-8079-657eab1d1e58
ms.reviewer: mwahl
ms.suite: ems
ms.openlocfilehash: c53d8cc815f792d1a1246a7434350f1cfb087844
ms.sourcegitcommit: 35f2989dc007336422c58a6a94e304fa84d1bcb6
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/20/2018
ms.locfileid: "36288968"
---
# <a name="hardware-and-software-requirements"></a>Требования к оборудованию и программному обеспечению

Privileged Access Management не имеет требований к оборудованию, выходящих за рамки требований к базовой платформе программного обеспечения. Просто убедитесь, что имеется достаточно памяти или места на диске и сетевое подключение.

> [!IMPORTANT]
> В этой статье описываются минимальные требования к базовому развертыванию. В ее цели не входит демонстрация высокой производительности, масштабируемости или высокой доступности. Она не представляет рекомендуемую топологию развертывания для крупных предприятий или рабочих сред.

## <a name="installing-from-software-packages"></a>Установка с помощью комплектов программного обеспечения

Следующее программное обеспечение можно загрузить из центра оценки TechNet или из MSDN:

- Microsoft Identity Manager 2016
  - Служба и портал: содержит установщик для службы и портала MIM, а также для сценария PAM
  - Надстройки и расширения: содержит установщик для командлетов PowerShell запросившей стороны

Из GitHub можно загрузить следующее программное обеспечение:

- [PAMSamplePortal](https://github.com/Azure/identity-management-samples): содержит пример веб-приложения для REST API.

## <a name="required-software"></a>Требуемое программное обеспечение

- Windows Server 2012 R2
- Windows 10 Корпоративная
- SQL Server 2012 с пакетом обновления 1 (SP1) или SQL Server 2014

## <a name="evaluation-software"></a>Ознакомительная версия программного обеспечения

Если у вас нет лицензий для Windows, SQL Server или Windows Server, загрузите ознакомительные версии программного обеспечения.

### <a name="technet-evaluation-center"></a>Центр оценки TechNet

- [Windows Server 2012 R2](https://www.microsoft.com/evalcenter/evaluate-windows-server-2012-r2)
- [Windows 10 Корпоративная](https://www.microsoft.com/evalcenter/evaluate-windows-10-enterprise)

### <a name="microsoft-download-center"></a>Центре загрузки Майкрософт

- [SQL Server](https://www.microsoft.com/download/details.aspx?id=29066)  
- [SharePoint Foundation 2013 с пакетом обновления 1 (SP1) и его обязательные компоненты](https://www.microsoft.com/download/details.aspx?id=42039)

## <a name="hardware-requirements"></a>Требования к оборудованию

Проверьте системные требования каждого компонента управления привилегированным доступом.

Для CORPDC:

- [Windows Server 2012 R2](https://technet.microsoft.com/library/dn303418.aspx) или более ранняя версия

Для CORPWKSTN:

- [Windows 10](https://technet.microsoft.com/windows/dn798752.aspx)

Для PRIVDC:

- [Windows Server 2012 R2](https://technet.microsoft.com/library/dn303418.aspx)

Для PAMSRV:

- [Windows Server 2012 R2](https://technet.microsoft.com/library/dn303418.aspx)
- [SQL Server 2012](https://msdn.microsoft.com/library/ms143506(sql.110).aspx) или [SQL Server 2014](https://msdn.microsoft.com/library/ms143506(v=sql.120).aspx)
