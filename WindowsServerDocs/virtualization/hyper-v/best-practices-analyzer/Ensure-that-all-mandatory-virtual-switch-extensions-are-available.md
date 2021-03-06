---
title: Убедитесь, что доступны все обязательные расширения виртуального коммутатора
description: Интернет-версия текста для этого правила анализатор соответствия рекомендациям.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 2f2f2698-f5ec-4cad-aa64-d6987e8142a1
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 14c9fc31521a7d4f5e0eed821c0cc49dcfe74e69
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/08/2020
ms.locfileid: "80861937"
---
# <a name="ensure-that-all-mandatory-virtual-switch-extensions-are-available"></a>Убедитесь, что доступны все обязательные расширения виртуального коммутатора

>Область применения: Windows Server 2016

Дополнительные сведения о рекомендациях и проверках см. в разделе [запуска наиболее проверок анализатором соответствия рекомендациям и Управление результатами проверок](https://go.microsoft.com/fwlink/p/?LinkID=223177).  
  
|Свойство|Подробности|  
|-|-|  
|**Операционная система**|Windows Server 2016|  
|**Продукт или функция**|Hyper-V|  
|**Серьезности**|Предупреждение|  
|**Категория**|Конфигурация|  
  
В следующих разделах курсив указывает текст пользовательского Интерфейса, который отображается в анализатор соответствия рекомендациям для этой проблемы.  
  
## <a name="issue"></a>Проблема  
*Один или несколько виртуальных сетевых адаптеров подключены к виртуальному коммутатору с обязательными расширениями, которые отключены или не установлены.*  
  
## <a name="impact"></a>Влияние  
*Сетевой трафик заблокирован на одном или нескольких виртуальных сетевых адаптерах на следующих виртуальных машинах:*  
  
\<список виртуальных машин >  
  
## <a name="resolution"></a>Разрешение  
*Сначала убедитесь, что на узле установлено обязательное расширение, и при необходимости установите расширение. Затем, если обязательное расширение отключено, используйте диспетчер виртуальных коммутаторов или командлет Windows PowerShell Enable-Вмсвитчекстенсион, чтобы включить расширение.*  
  


