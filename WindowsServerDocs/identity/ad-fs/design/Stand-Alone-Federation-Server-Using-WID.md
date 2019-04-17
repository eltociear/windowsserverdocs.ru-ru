---
ms.assetid: 33b80a3f-67f3-4da7-ac4a-7fd2232fbd5d
title: "Изолированный сервер федерации с использованием WID"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 9ec4150a7d3adfaac786219d253e1d0898c18204
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/03/2017
---
# <a name="stand-alone-federation-server-using-wid"></a>Изолированный сервер федерации с использованием WID

>Область применения: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Сервер федерации отдельной в \(AD FS\) служб федерации Active Directory состоит из одного сервера, который узлов службы федерации настроены для использования \(WID\) внутренней базы данных Windows. В этой топологии Служб федерации Active Directory предназначен для лаборатории тестирования. Не рекомендуется для производственных сред, так как он ограничен только одним сервером федерации и не может использоваться для масштабирование для нескольких серверов.  
  
Если вы хотите добавить дополнительные серверы федерации в лаборатории тестирования, необходимо перестроить службы федерации с нуля, развернув любой из топологий, которая описывается ниже в этом разделе. Поэтому рекомендуется применять эту топологию для тестовой лаборатории или proof\ of\ концепции среды в тестовой сети в котором одного сервера федерации подходит, как показано на следующем рисунке.  
  
![сервер с использованием WID](media/FedServerWID.gif)  
  
## <a name="test-lab-considerations"></a>Рекомендации по лаборатории тестирования  
В этом разделе приведены основные аспекты, которые об целевая аудитория, преимущества и ограничения, связанные с этой топологии для тестовых лабораторных сред.  
  
### <a name="who-should-use-this-topology"></a>Кому следует использовать эту топологию?  
  
-   \(IT\) специалистов по информационным технологиям или ИТ-архитекторы, которые хотят оценить или разработка эксперимента для этой технологии  
  
### <a name="what-are-the-benefits-of-using-this-topology"></a>В чем заключаются преимущества использования этой топологии?  
  
-   Легко настроить в среде лаборатории тестирования  
  
### <a name="what-are-the-limitations-of-using-this-topology"></a>Что такое ограничений использования этой топологии  
  
-   Только один сервер федерации каждой службы федерации \ (не возможность масштабирование для farm\)  
  
-   Нет избыточности \ (только один экземпляр exists\ базы данных конфигурации AD FS)  
  

## <a name="see-also"></a>См. также:
[Руководство по разработке служб AD FS в Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)