---
ms.assetid: 4ef052f0-61a9-4912-b780-5c96187c850f
title: Некоторые аспекты топологии развертывания AD FS
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: cf646dedef85add8607c7940275e3c3fae90a661
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/31/2019
ms.locfileid: "66445340"
---
# <a name="ad-fs-deployment-topology-considerations"></a>Некоторые аспекты топологии развертывания AD FS

В этом разделе рассмотрены важные вопросы, которые помогут в планировании и проектировании какие служб федерации Active Directory \(AD FS\) топологии развертывания для использования в рабочей среде. В этом разделе является отправной точкой для анализа и оценки аспектов, влияющих на какие функции и возможности будут доступны после развертывания AD FS. Например, в зависимости от того, какая база данных тип для хранения базы данных конфигурации AD FS в конечном итоге определяет возможность реализации определенных Security Assertion Markup Language \(SAML\) функций, требующих SQL Сервер.  

## <a name="determining-which-type-of-ad-fs-configuration-database-to-use"></a>Определение требуемого типа базы данных конфигурации AD FS для использования  
AD FS использует базу данных для хранения конфигурации и — в некоторых случаях — данные о транзакциях, связанных со службой федерации. Программное обеспечение AD FS можно использовать для выбора либо встроенный\-во внутренней базе данных Windows \(WID\) или Microsoft SQL Server 2005 или более поздней версии для хранения данных в службе федерации.  

Для большинства целей эти два типа баз данных относительно эквивалентны. Тем не менее существуют некоторые различия, которые следует учитывать, прежде чем начинать изучать дополнительные о различных топологиях развертывания, которые можно использовать с AD FS. В следующей таблице описаны различия в поддерживаемых функциях между Внутренней базой данных Windows и базы данных SQL Server.  

Функции AD FS  

|Компонент|Поддерживается внутренней базой данных Windows?|Поддерживается SQL Server?|Дополнительные сведения об этой функции|  
|-----------|---------------------|----------------------------|---------------------------------------|  
|Развертывание фермы серверов федерации|Да, с ограничением в 30 серверов федерации для каждой фермы|Да. Действующих ограничений на число серверов федерации, которые можно развернуть на одной ферме, не существует|[Определение топологии развертывания для служб федерации Active Directory](Determine-Your-AD-FS-Deployment-Topology.md)|  
|Разрешение артефактов SAML **Примечание:** Эта функция не требуется для сценариев Microsoft Online Services, Microsoft Office 365, Microsoft Exchange или Microsoft Office SharePoint.|Нет|Да|[Роль базы данных конфигурации AD FS](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md).<br /><br />[Рекомендации по безопасному планированию и развертыванию AD FS](Best-Practices-for-Secure-Planning-and-Deployment-of-AD-FS.md)|  
|SAML\/WS\-обнаружение воспроизведения токенов федерации|Нет|Да|[Роль базы данных конфигурации AD FS](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md).<br /><br />[Рекомендации по безопасному планированию и развертыванию AD FS](Best-Practices-for-Secure-Planning-and-Deployment-of-AD-FS.md)|  

Функции базы данных  

|Компонент|Поддерживается внутренней базой данных Windows?|Поддерживается SQL Server?|Дополнительные сведения об этой функции|  
|-----------|---------------------|----------------------------|---------------------------------------|  
|С помощью избыточность баз данных Basic репликация по запросу, где одно или дополнительные серверы, размещающие чтения\-единственная копия изменения запроса базы данных, которые выполняются на исходном сервере, на котором размещена чтения\/записи копию базы данных|Да|Нет|[Роль базы данных конфигурации AD FS](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md).|  
|Избыточность базы данных, с помощью высокой\-доступности решения, например отказоустойчивой кластеризации или зеркального отображения \(только на уровне базы данных\) **Примечание:** Все топологии развертывания AD FS поддерживают кластеризацию на уровне службы AD FS.|Нет|Да|[Роль базы данных конфигурации AD FS](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md).<br /><br />[Обзор решений высокой доступности](https://go.microsoft.com/fwlink/?LinkId=179853)|  

### <a name="sql-server-considerations"></a>Особенности SQL Server  
Следует учитывать следующие факты развертывания, при выборе SQL Server как база данных конфигурации для развертывания AD FS.  

-   **Функции SAML и их влияние на размер и рост базы данных**. Если включены функции обнаружения воспроизведения маркеров SAML или разрешение артефактов SAML, AD FS сохраняет информацию в базе данных конфигурации SQL Server для каждого токена AD FS, выданный. Увеличение размера базы данных SQL Server, в результате этого действия не рассматриваются как значительные и зависит от срока хранения настроенных воспроизведения маркеров. Каждая запись артефакта имеет размер около 30 килобайт \(КБ\).  

-   **Число необходимых для развертывания серверов**. Необходимо будет добавить по крайней мере один дополнительный сервер \(общего числа серверов, необходимых для развертывания инфраструктуры AD FS\) который будет функционировать как выделенный узел экземпляра SQL Server. Если вы планируете использовать отказоустойчивую кластеризацию или зеркальное отображение для обеспечения отказоустойчивости и масштабируемости базы данных конфигурации SQL Server, не менее двух серверов SQL Server не требуется.  

### <a name="how-the-configuration-database-type-you-select-may-impact-hardware-resources"></a>Влияние выбранного типа базы данных конфигурации на аппаратные ресурсы  
Влияние аппаратных ресурсов на сервере федерации, который развертывается на ферме, используя WID в отличие от сервера федерации, развернутый в ферме, база данных SQL Server не имеет значения. Тем не менее необходимо иметь в виду, что при использовании внутренней базы данных Windows для фермы каждый сервер федерации в ферме необходимо хранения, управлять и обслуживать изменения репликации для свою локальную копию базы данных конфигурации AD FS, при этом также сохраняя неизменный нормали операции, которые требуются службы федерации.  

В отличие от этого серверы федерации, которые развертываются в ферме, которая использует базу данных SQL Server не обязательно содержит локальный экземпляр базы данных конфигурации AD FS. Следовательно, требования к аппаратным ресурсам в этом случае несколько ниже.  

## <a name="verifying-that-your-production-environment-can-support-an-ad-fs-deployment"></a>Проверка возможности поддержки развертывания служб AD FS в рабочей среде  
Дополнение к серверам федерации, которые будут развернуты, и в зависимости от того, как настроить существующей рабочей среды для предоставления инфраструктуры, необходимой для поддержки нового развертывания AD FS могут потребоваться следующие дополнительные серверы:  

-   доменный контроллер Active Directory;  

-   Центр сертификации \(ЦС\)  

-   веб-сервер для размещения метаданных федерации;  

-   Балансировка сетевой нагрузки \(балансировки сетевой Нагрузки\)  

## <a name="see-also"></a>См. также
[Руководство по разработке служб федерации Active Directory в Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)