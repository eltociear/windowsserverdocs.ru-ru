---
title: Более чем один сетевой адаптер должен быть доступен
description: Интернет-версию текст для этого правила анализатора соответствия рекомендациям.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 59940e56-e06a-490f-90ea-cf30d9f80b09
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 678c0161e97b8dd022bbf0037d9add5de0281f77
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2019
ms.locfileid: "59884605"
---
# <a name="more-than-one-network-adapter-should-be-available"></a>Более чем один сетевой адаптер должен быть доступен

>Область применения. Windows Server 2016

Дополнительные сведения о рекомендациях и сканировании см. в разделе [Анализатор соответствия рекомендациям](https://go.microsoft.com/fwlink/?LinkId=122786).  
  
|Свойство|Подробности|  
|-|-|  
|**Операционная система**|Windows Server 2016|  
|**Продукта или компонента**|Hyper-V|  
|**Уровень серьезности**|Ошибка|  
|**Категория**|Конфигурация|  

В следующих разделах курсив указывает текст пользовательского Интерфейса, который отображается в анализатор соответствия рекомендациям для этой проблемы.

## <a name="issue"></a>Проблемы  
  
*Этот сервер настроен с одного сетевого адаптера, который должен быть общим для операционной системы и всех виртуальных машин, которым требуется доступ к физической сети.*  
  
## <a name="impact"></a>Влияние  
  
*Производительность сети могут быть ограничены в управляющей операционной системе.*  
  
## <a name="resolution"></a>Разрешение  
  
*Добавьте дополнительные сетевые адаптеры к этому компьютеру. Чтобы зарезервировать один сетевой адаптер для исключительного использования управляющей операционной системе, не задана для использования с внешней виртуальной сети.*  
  
Сведения о добавлении сетевого адаптера на компьютере обратитесь к документации компьютера или сетевого адаптера. Затем Чтобы зарезервировать его исключительно для операционной системы, не подключайте его к виртуальному коммутатору.   
  

