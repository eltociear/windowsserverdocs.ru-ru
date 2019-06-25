---
ms.assetid: bb16e39d-566d-436c-b957-394c06d556db
title: Руководство по разработке служб AD FS в Windows Server 2012
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 3f2a6df6a9c9a5cbdfa9c64bc6521e92f4982a15
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/24/2019
ms.locfileid: "66191730"
---
# <a name="ad-fs-design-guide-in-windows-server"></a>Руководство по разработке AD FS в Windows Server 


  
> [!NOTE]  
> Сведения о развертывании AD FS в Windows Server 2012 R2, см. в разделе [Windows Server 2012 R2 AD FS Deployment Guide](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md).  
  
Можно использовать службы федерации Active Directory® \(AD FS\) с Windows Server® 2012 поставщика роли, чтобы прозрачно выполнить аутентификацию пользователей к любому веб-служб операционной системы в федерации\-служб на основе или приложения, находящиеся в партнерской организации по ресурсам, без необходимости администраторы могут создавать или обслуживать внешние отношения доверия или доверия леса между сетями обеих организаций и без необходимости для пользователей выполнить вход еще раз. Процесс аутентификации в одной сети при доступе к ресурсам в другой сети — без необходимости повторного входа действий пользователей, известен как единый вход\-на \(SSO\).  
  
## <a name="about-this-guide"></a>Об этом руководстве  
В этом руководстве содержатся рекомендации по планированию нового развертывания AD FS, в соответствии с требованиями вашей организации \(также называется в данном руководстве целей развертывания\) и конкретного проекта, который вы хотите создать. Это руководство предназначено для использования специалистом по инфраструктуре или системным архитектором. Он выделяет ваши основные точки принятия решений при планировании развертывания AD FS. Перед прочтением этого руководства необходимо хорошо понимать как AD FS работает на функциональном уровне. Вы также должны хорошо понимать организационные требования, которые будут отражены в дизайна служб AD FS.  
  
В этом руководстве описывается набор целей развертывания, которые основаны на три основной схемы AD FS, и он поможет выбрать наиболее подходящий из них для своей среды. Можно использовать эти цели развертывания для формы, один из способов комплексное AD FS или пользовательской системы, соответствующей потребностям вашей среды:  
  
-   Федеративного единого входа через Интернет для поддержки бизнеса\-для\-бизнеса \(B2B\) сценарии и взаимодействие между бизнес-подразделениями и независимыми лесами  
  
-   Веб-единого входа для поддержки клиентов доступ к приложениям в бизнесе\-для\-потребителя \(B2C\) сценариев  
  
Руководство содержит инструкции по сбору необходимых данных о среде для каждой из систем. Затем эти рекомендации можно использовать для планирования и разработки развертывания AD FS. Ознакомьтесь с этим руководством и окончания сбора данных, Документирование и сопоставления требований организации, вы получите сведения, необходимые для начала развертывания AD FS, используя сведения в [Windows Server 2012 AD FS Deployment Guide](../../ad-fs/deployment/Windows-Server-2012-AD-FS-Deployment-Guide.md).  
  
## <a name="in-this-guide"></a>В данном руководстве  
  
-   [Определение целей по развертыванию служб федерации Active Directory](Identifying-Your-AD-FS-Deployment-Goals.md)  
  
-   [Сопоставление целей развертывания с разработкой служб федерации Active Directory](Mapping-Your-Deployment-Goals-to-an-AD-FS-Design.md)  
  
-   [Определение топологии развертывания для служб федерации Active Directory](Determine-Your-AD-FS-Deployment-Topology.md)  
  
-   [Планирование развертывания](Planning-Your-Deployment.md)  
  
-   [Планирование размещения серверов федерации](Planning-Federation-Server-Placement.md)  
  
-   [Планирование размещения прокси-серверов федерации](Planning-Federation-Server-Proxy-Placement.md)  
  
-   [Планирование мощности сервера AD FS](Planning-for-AD-FS-Server-Capacity.md)  
  
-   [Приложение А. Обзор требований AD FS](Appendix-A--Reviewing-AD-FS-Requirements.md)  
  
