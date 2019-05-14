---
title: Лицензирование и скачивание Microsoft Identity Manager | Документация Майкрософт
description: В этой статье описано, как лицензировать Microsoft Identity Manager (MIM) 2016 и скачать программное обеспечение.
keywords: ''
author: markwahl-msft
ms.author: markwahl-msft
manager: femila
ms.date: 02/25/2019
ms.topic: article
ms.service: microsoft-identity-manager
ms.technology: security
ms.assetid: ''
ms.reviewer: billmath
ms.suite: ems
ms.openlocfilehash: 7c5ab987801c63dca2457025442a35560dca3b86
ms.sourcegitcommit: 225fca802d6b59bdc98d50020b297eb6393f70eb
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2019
ms.locfileid: "64518749"
---
# <a name="microsoft-identity-manager-2016-licensing-and-downloads"></a>Лицензирование и скачивание Microsoft Identity Manager

В этой статье описано, как лицензировать Microsoft Identity Manager (MIM) 2016 и скачать программное обеспечение.

## <a name="licensing-mim-for-your-organization"></a>Лицензирование MIM для организации

Microsoft Identity Manager 2016 лицензируется отдельно для каждого пользователя.  Подробные сведения о лицензировании содержатся в условиях использования продуктов и связанной документации. Все эти материалы можно скачать на странице с [условиями лицензирования](https://www.microsoft.com/en-us/licensing/product-licensing/products.aspx).

### <a name="licensing-for-azure-ad-premium-customers"></a>Лицензирование для клиентов Azure AD Premium

Решение Microsoft Identity Manager 2016 доступно в рамках предложения Azure Active Directory Premium (P1 и P2), которое является частью решения Enterprise Mobility + Security.

Azure AD Premium предоставляется в рамках [Соглашения Enterprise](https://www.microsoft.com/en-us/licensing/licensing-programs/enterprise.aspx), [программы Microsoft Open License](https://www.microsoft.com/en-us/licensing/licensing-programs/open-license.aspx) и программы [поставщиков облачных решений](https://go.microsoft.com/fwlink/?LinkId=614968&clcid=0x409). Подписчики Azure и Office 365 могут приобрести Active Directory Premium через Интернет.  Дополнительные сведения см. на странице [цен на Azure Active Directory](https://azure.microsoft.com/en-us/pricing/details/active-directory/).

### <a name="mim-cals"></a>Клиентские лицензии на MIM

Если у ваших пользователей нет подписок на Azure Active Directory Premium, а вы используете дополнительные возможности MIM без синхронизации, значит каждому пользователю, удостоверением которого управляет MIM, требуется [клиентская лицензия](https://www.microsoft.com/en-us/licensing/product-licensing/client-access-license.aspx). Если требуется обеспечить доступ к MIM сторонним пользователям — деловым партнерам, подрядчикам или клиентам — вы можете приобрести для них пользовательские лицензии или лицензии External Connector. Клиентские лицензии на Microsoft Identity Manager 2016 не требуются пользователям, удостоверения которых используются только в службе синхронизации Microsoft Identity Manager и не управляются другими компонентами MIM.

### <a name="licenses-for-platform-components"></a>Лицензии для компонентов платформы

Чтобы использовать серверное программное обеспечение Microsoft Identity Manager 2016 в качестве дополнительного компонента Windows Server, требуется лицензия на Windows Server. Для развертывания MIM также необходимо установить SQL Server.  Лицензии на Windows Server и SQL Server не предоставляются вместе с MIM.

## <a name="obtaining-mim-software"></a>Получение программного обеспечения MIM

Перед первоначальной установкой или обновлением MIM убедитесь, что у вас есть последняя версия программы.

При первоначальной установке MIM необходимо скачать файлы установки для каждого компонента MIM, который требуется для вашего сценария. Затем в Центре загрузки нужно скачать обновления для этих файлов и дополнительные компоненты.


| Сценарий | Компонент | Соответствие сценарию | Имя папки с ISO-файлом DVD-диска | Комментарии |
|----------|-----------|---------------------   |-------------------|----------|--------------|
|Синхронизация| Служба синхронизации (с соединителем для AD) | Да | `Synchronization Service` | |
| Синхронизация | PCNS | Нет | `Password Change Notification Service` |  Необходимо установить на контроллеры домена |
| Синхронизация | Соединители для LDAP, SQL, веб-служб, PowerShell, Graph | Нет | Н/Д | Доступны в Центре загрузки |
| Privileged Access Management (Защита Windows и Microsoft Azure Active Directory с помощью управления привилегированным доступом) | Служба MIM | Да | `Service and Portal` | |
| Самообслуживание | Служба MIM, портал MIM | Да | `Service and Portal` | |
| Самообслуживание | Надстройки и расширения | Нет | `Add-ins and extensions` | Необходимо установить на компьютеры пользователей |
| Самообслуживание | Отчеты SCSM | Нет | `Data Warehouse Support Scripts` | |
| Самообслуживание | Агент гибридной отчетности | Нет | Н/Д | Доступно в Центре загрузки |
| Самообслуживание | Языковые пакеты | Нет | `LANGUAGE Packs` | |
| Управление сертификатами | CM | Да | `Certificate Management` | |
| Управление сертификатами | Пакетный клиент CM | Нет | `CM Bulk Client` | |
| Управление сертификатами | Клиент CM | Нет | `CM Client`  | |
| Управление сертификатами | Приложение CM для Windows | Нет | `FIMCMModernApp*` | | |

### <a name="obtaining-windows-installer-packages"></a>Получение пакетов установщика Windows

При первоначальной установке большинство организаций скачивают соответствующие пакеты MIM в [Центре поддержки корпоративных лицензий (VLSC)](https://www.microsoft.com/licensing/servicecenter/default.aspx). 


В ISO-файле DVD-диска каждый компонент MIM помещен в отдельную папку. Это служба синхронизации, служба MIM, портал MIM и т. д. Если вы собираетесь установить программное обеспечение не на том компьютере, на который его скачали, полностью скопируйте ISO-файл или папку с компонентом, а не один только MSI-файл из папки без остальных файлов и вложенных папок.

При отсутствии доступа к Центру поддержки корпоративных лицензий клиенты с соответствующей подпиской разработчика могут скачать ISO-файл MIM 2016 SP1 в [разделе загрузок на портале Visual Studio](https://my.visualstudio.com/Downloads?q=Microsoft%20Identity%20Manager%202016%20with%20Service%20Pack%201&pgroup=).  На портале найдите Microsoft Identity Manager 2016 with Service Pack 1.  

Если у вас нет доступа к Центру поддержки корпоративных лицензий и вы просто хотите опробовать программное обеспечение MIM в течение ограниченного периода времени, можно скачать [ознакомительную версию MIM 2016](https://www.microsoft.com/en-us/download/details.aspx?id=48244). Эта версия не предназначена для использования в рабочей среде. Срок ее действия заканчивается через 180 дней после установки без возможности обновления. Для установки ознакомительной версии требуется Windows Server 2008 R2, Windows Server 2012 или Windows Server 2012 R2.  Если вы не знакомы с MIM и только изучаете эту технологию, имейте в виду, что для всех сценариев MIM требуется домен Active Directory и установленные экземпляры Windows Server и SQL Server. Если у вас не установлены экземпляры Windows Server или SQL Server, вы можете [подготовить виртуальную машину с SQL Server 2016 и Windows Server 2016](https://azure.microsoft.com/en-us/blog/azure-images-sql-server-2016-on-windows-server-2016/).

### <a name="obtaining-updates"></a>Получение обновлений

После установки MIM из MSI-файла нужно установить необходимые исправления.

В [журнале выпуска версий Identity Manager](./reference/version-history.md) узнайте номер выпуска последнего обновления, который содержит ссылку на скачивание файлов исправлений.

Определить необходимые файлы обновления можно с помощью следующей таблицы, в которой перечислены компоненты и имена соответствующих файлов (MSP) в обновлении.

| Сценарий | Компонент | Имя папки с ISO-файлом DVD-диска | Имя файла исправления |
|----------|-----------|-   |-------------------|----------|--------------|
|Синхронизация| Служба синхронизации MIM | `Synchronization Service` | `FIMSyncService_x64*.msp` |
| Самообслуживание | Служба MIM, портал MIM | `Service and Portal` | `FIMService_x64*msp` |
| Самообслуживание | Надстройки и расширения | `Add-ins and extensions` | `FIMAddinsExtensions*msp` |
| Самообслуживание | Языковые пакеты | `LANGUAGE Packs` | `LANGUAGE Packs.zip` |
| Управление доступом (BHOLD) | BHOLD | `BHOLD` | `AccessManagementConnector.msi`, `BHOLD*.msi` |
| Управление сертификатами | CM |  `Certificate Management` | `FIMCM*.msp` |
| Управление сертификатами | Пакетный клиент CM |  `CM Bulk Client` |`FIMCMBulkClient*msp` |
| Управление сертификатами | Клиент CM | Клиент CM |`FIMCMClient*msp` |

Перед установкой MSP-файла ознакомьтесь с заметками о выпуске соответствующего обновления.

Обновления для [BHOLD](https://www.microsoft.com/en-us/download/details.aspx?id=55950) недоступны в виде файлов MSP, а выполняются только с помощью установщиков MSI.

### <a name="additional-downloads"></a>Дополнительные файлы для скачивания

Вам также могут понадобиться следующие файлы:

- [Агент для составления гибридной отчетности о MIM](https://www.microsoft.com/download/details.aspx?id=55112).

- [Универсальный соединитель LDAP, универсальный соединитель SQL, соединитель Graph, соединитель Lotus Domino, соединитель PowerShell, соединитель веб-служб](http://go.microsoft.com/fwlink/?LinkId=717495).

- [Соединитель для хранилища профилей пользователей в SharePoint](https://www.microsoft.com/en-us/download/details.aspx?id=41164).

- Если у вас нет домена Active Directory и вы настраиваете сценарий PAM в экспериментальных целях, ознакомьтесь со статьей [Сценарии развертывания PAM в MIM 2016 SP1](sp1-deployment-scripts.md).

## <a name="next-steps"></a>Дальнейшие шаги

- Дополнительные сведения о сценариях, добавленных в MIM 2016, см. в статье [Microsoft Identity Manager 2016: новости и обновления](microsoft-identity-manager-2016.md).
- [Руководство по планированию ресурсов](capacity-planning-guide.md).
- [Развертывание Microsoft Identity Manager 2016 с пакетом обновления 1 (SP1)](microsoft-identity-manager-deploy.md), [Управление привилегированным доступом для доменных служб Active Directory](./pam/privileged-identity-management-for-active-directory-domain-services.md).

