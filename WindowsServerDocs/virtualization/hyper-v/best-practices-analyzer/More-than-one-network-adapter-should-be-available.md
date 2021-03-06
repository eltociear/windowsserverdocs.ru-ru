---
title: Должна быть доступна более одного сетевого адаптера
description: Интернет-версия текста для этого правила анализатор соответствия рекомендациям.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 59940e56-e06a-490f-90ea-cf30d9f80b09
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 56cb747ac44d48b115dbf105ea96e4623d458b28
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/08/2020
ms.locfileid: "80861897"
---
# <a name="more-than-one-network-adapter-should-be-available"></a>Должна быть доступна более одного сетевого адаптера

>Область применения: Windows Server 2016

Дополнительные сведения о рекомендациях и сканировании см. в разделе [Анализатор соответствия рекомендациям](https://go.microsoft.com/fwlink/?LinkId=122786).  
  
|Свойство|Подробности|  
|-|-|  
|**Операционная система**|Windows Server 2016|  
|**Продукт или функция**|Hyper-V|  
|**Серьезности**|Ошибка|  
|**Категория**|Конфигурация|  

В следующих разделах курсив указывает текст пользовательского Интерфейса, который отображается в анализатор соответствия рекомендациям для этой проблемы.

## <a name="issue"></a>Проблема  
  
*На этом сервере настроен один сетевой адаптер, который должен быть общим для операционной системы управления, а также для всех виртуальных машин, которым требуется доступ к физической сети.*  
  
## <a name="impact"></a>Влияние  
  
*Производительность сети может снижаться в операционной системе управления.*  
  
## <a name="resolution"></a>Разрешение  
  
*Добавьте сетевые адаптеры на этот компьютер. Чтобы зарезервировать один сетевой адаптер для монопольного использования операционной системой управления, не настраивайте его для использования с внешней виртуальной сетью.*  
  
Сведения о добавлении сетевого адаптера на компьютер см. в документации к компьютеру или сетевому адаптеру. Затем, чтобы зарезервировать его исключительно для операционной системы управления, не подключайте его к виртуальному коммутатору.   
  


