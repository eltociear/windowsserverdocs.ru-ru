---
title: Не устанавливайте виртуальных машин, настроенных с виртуальными адаптерами Fibre Channel, чтобы разрешить динамической миграции, при наличии меньшего числа путей к Fibre Channel логические устройства (LUN) на сервере назначения, чем в источнике
description: Интернет-версию текст для этого правила анализатора соответствия рекомендациям.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 6ff69d5cb09133a806c2a2df3446713264a4e892
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2019
ms.locfileid: "59849555"
---
# <a name="avoid-enabling-virtual-machines-configured-with-virtual-fibre-channel-adapters-to-allow-live-migrations-when-there-are-fewer-paths-to-fibre-channel-logical-units-luns-on-the-destination-than-on-the-source"></a>Не устанавливайте виртуальных машин, настроенных с виртуальными адаптерами Fibre Channel, чтобы разрешить динамической миграции, при наличии меньшего числа путей к Fibre Channel логические устройства (LUN) на сервере назначения, чем в источнике

>Область применения. Windows Server 2016

Дополнительные сведения о рекомендациях и проверках см. в разделе [запуска наиболее проверок анализатором соответствия рекомендациям и Управление результатами проверок](https://go.microsoft.com/fwlink/p/?LinkID=223177).  
  
|Свойство|Подробности|  
|-|-|  
|**Операционная система**|Windows Server 2016|  
|**Продукта или компонента**|Hyper-V|  
|**Уровень серьезности**|Предупреждение|  
|**Категория**|Конфигурация|

В следующих разделах курсив указывает текст пользовательского Интерфейса, который отображается в анализатор соответствия рекомендациям для этой проблемы.
  
## <a name="issue"></a>**Проблема**  
*Один или несколько виртуальных машин быть задано свойство AllowReducedFcRedunancy в поставщике WMI виртуализации.*  
  
## <a name="impact"></a>**Влияние**  
*Динамический перенос следующих виртуальных машин может привести к потере данных или прерывания ввода-вывода в хранилище:*  
  
\<Список виртуальных машин >  
  
## <a name="resolution"></a>**Решение**  
*Рассмотрите возможность Очистка свойства AllowReducedFcRedundancy WMI на затронутые виртуальные машины. Если это свойство установлен, можно выполнить динамическую миграцию на виртуальные машины, настроенные с помощью виртуальных адаптеров Fibre Channel, только в том случае, если число путей к Fibre Channel в месте назначения же или больше, чем число путей в источнике. Это позволяет предотвратить потерю данных или прерывания ввода-вывода в хранилище.* 