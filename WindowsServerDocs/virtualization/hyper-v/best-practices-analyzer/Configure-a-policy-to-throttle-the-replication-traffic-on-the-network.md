---
title: Настроить политику, чтобы регулировать трафик репликации в сети
description: Интернет-версию текст для этого правила анализатора соответствия рекомендациям.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 82cb1aef-cdc3-4d0a-88d4-ef497ab79606
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 2c1f1865fa1d611c0b5baaf981140f9807b51458
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2019
ms.locfileid: "59818695"
---
# <a name="configure-a-policy-to-throttle-the-replication-traffic-on-the-network"></a>Настроить политику, чтобы регулировать трафик репликации в сети

>Область применения. Windows Server 2016

Дополнительные сведения о рекомендациях и проверках см. в разделе [запуска наиболее проверок анализатором соответствия рекомендациям и Управление результатами проверок](https://go.microsoft.com/fwlink/p/?LinkID=223177).  
  
|Свойство|Подробности|  
|-|-|  
|**Операционная система**|Windows Server 2016|  
|**Продукта или компонента**|Hyper-V|  
|**Уровень серьезности**|Предупреждение|  
|**Категория**|Конфигурация|  
  
В следующих разделах курсив указывает текст пользовательского Интерфейса, который отображается в анализатор соответствия рекомендациям для этой проблемы.  
  
## <a name="issue"></a>Проблемы  
*Не может существовать ограничение на объем пропускной способности сети репликации может получать.*  
  
## <a name="impact"></a>Влияние  
*Пропускная способность сети может стать в первую очередь трафик репликации, влияя на другие важные сетевой активности. Это влияет на следующие порты:*  
  
\<Список виртуальных машин >  
  
## <a name="resolution"></a>Разрешение  
*Если используется другой метод для регулирования сетевого трафика, его можно игнорировать. В противном случае используйте редактор групповых политик, чтобы настроить политику, которая будет регулироваться сетевой трафик к нужному порту сервера-реплики.*  
  
  

