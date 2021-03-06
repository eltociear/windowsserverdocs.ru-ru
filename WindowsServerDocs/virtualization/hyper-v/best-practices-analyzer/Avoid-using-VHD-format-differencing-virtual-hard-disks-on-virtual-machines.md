---
title: Избегайте использования разностных виртуальных жестких дисков в формате VHD на виртуальных машинах, на которых выполняются рабочие нагрузки сервера, в рабочей среде.
description: Интернет-версия текста для этого правила анализатор соответствия рекомендациям.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 272de33d-2708-4679-8564-ee28848a2839
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: a11959266db4c9f3da73123c41a211198f27b9a5
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857727"
---
# <a name="avoid-using-vhd-format-differencing-virtual-hard-disks-on-virtual-machines-that-run-server-workloads-in-a-production-environment"></a>Избегайте использования разностных виртуальных жестких дисков в формате VHD на виртуальных машинах, на которых выполняются рабочие нагрузки сервера, в рабочей среде.

>Область применения: Windows Server 2016

Дополнительные сведения о рекомендациях и проверках см. в разделе [запуска наиболее проверок анализатором соответствия рекомендациям и Управление результатами проверок](https://go.microsoft.com/fwlink/p/?LinkID=223177).  
  
|Свойство|Подробности|  
|-|-|  
|**Операционная система**|Windows Server 2016|  
|**Продукт или функция**|Hyper-V|  
|**Серьезности**|Предупреждение|  
|**Категория**|Конфигурация|  
  
В следующих разделах курсив указывает текст пользовательского Интерфейса, который отображается в анализатор соответствия рекомендациям для этой проблемы.  
  
## <a name="issue"></a>**Проблема**  
*Одна или несколько виртуальных машин используют разностные виртуальные жесткие диски в формате VHD.*  
  
## <a name="impact"></a>**Благоприятн**  
*Разностные виртуальные жесткие диски в формате VHD могут столкнуться с проблемами согласованности в случае сбоя питания. Проблемы согласованности могут возникать, если физический диск выполняет неполное или неправильное обновление сектора в VHD-файле, который изменяется при сбое питания. Это влияет на следующие виртуальные машины:*  
  
\<список виртуальных машин >  
  
## <a name="resolution"></a>**Решение**  
*Завершите работу виртуальной машины и преобразуйте цепочки разностных виртуальных жестких дисков в формате VHD в формат VHDX или объедините цепочку с фиксированным виртуальным жестким диском. (Формат VHDX имеет механизмы надежности, которые помогают защитить диск от повреждений из-за сбоев питания.) Однако не преобразуйте виртуальный жесткий диск, если он, вероятно, будет подключен к более ранней версии Windows в некоторый момент. Версии Windows, предшествующие Windows Server 2012, не поддерживают формат VHDX.*  
  


