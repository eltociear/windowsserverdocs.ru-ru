---
ms.assetid: d04dd17e-a843-46fd-8711-0039918f92d9
title: Реализация плана проектирования AD FS
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 6150b52030734c57b345aea731302650bcbddbfd
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/24/2019
ms.locfileid: "66192127"
---
# <a name="implementing-your-ad-fs-design-plan"></a>Реализация плана проектирования AD FS

Следующие условия окружающей среды и требований являются важными факторами в реализации служб федерации Active Directory \(AD FS\) разработку плана:  
  
-   **Поддерживаемые партнерами:** Обычно вы используете AD FS для работы с партнерских организаций. Чтобы установить федерацию удостоверений, определите организаций, которые следует использовать для формирования партнерства. После развертывания базового шаблона AD FS находится в месте, работе с партнерами включает в себя добавление партнеров, удаление партнеров и обновление информации для партнеров. Изменения в партнерские отношения может возникнуть по ряду причин. Например развертывание AD FS могут потребоваться обновления партнерство Если партнеру значительного изменения своего бизнеса, организации становится частью более крупной организации или федерации организации или вашей организации предоставляется другим компании. В любом сценарии, в котором федерацию удостоверений из нескольких доменов, необходимо знать домены \(партнеров\) , которые сейчас поддерживают и все дополнительные домены, которые представляют потенциальными партнерами.  
  
-   **Поддерживаемые типы приложений и служб:** Некоторые приложения и службы требуется доступ к ресурсам операционной системы, а другие — «утверждения в маркере безопасности.» Важно понимать типы приложений и служб, которые поддерживает AD FS, поэтому можно формулировать требований по администрированию.  
  
-   **Логический и физический архитектурных схем или топология развертывания:** Следует знать:  
  
    -   Ли серверы федерации будет функционировать в наборе фермами серверов или на одном сервере.  
  
    -   Где сети развертывает брандмауэры и прокси-серверы.  
  
    -   Расположение ресурсов и ли пользователи обращаются к ресурсам из вашей организации за пределами организации, или оба.  
  
## <a name="how-to-implement-your-ad-fs-design-using-this-guide"></a>Как реализовать дизайна служб AD FS, с помощью этого руководства  
Следующий шаг в реализации проекта является определение того, в каком порядке должны выполняться каждой задачи развертывания. Контрольные списки из этого руководства помогут вам выполнить необходимые задачи по развертыванию серверов и приложений в рамках реализации составленного плана. Родительские и дочерние контрольные списки, используются при необходимости для представления порядка, в какие задачи для конкретных AD FS должны быть обработаны конструктора.  
  
Используйте следующие контрольные списки родительской в этом разделе руководства к освоения задачи развертывания для реализации вашей организации предпочтительной AD FS:  
  
-   [Контрольный список. Реализация механизма единого входа через Интернет](Checklist--Implementing-a-Web-SSO-Design.md)  
  
-   [Контрольный список. Реализация федеративного механизма единого входа через Интернет [ADFS2]](Checklist--Implementing-a-Federated-Web-SSO-Design.md)  