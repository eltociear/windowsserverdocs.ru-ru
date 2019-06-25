---
ms.assetid: f0d4cecc-5a03-448c-bef9-86c4730b4eb0
title: Обзор балансировки нагрузки виртуальной машины
ms.prod: windows-server-threshold
ms.technology: storage-failover-clustering
ms.topic: article
author: bhattacharyaz
manager: eldenc
ms.author: subhatt
ms.date: 09/19/2016
ms.openlocfilehash: 125dd7421cc1876c07983016498a9689d8a507ac
ms.sourcegitcommit: a3c9a7718502de723e8c156288017de465daaf6b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/19/2019
ms.locfileid: "65475990"
---
# <a name="virtual-machine-load-balancing-overview"></a>Обзор балансировки нагрузки виртуальной машины

> Относится к: Windows Server 2019, Windows Server 2016

Ключевыми требованиями для развертывания частного облака является (капитальных затрат<abbr title="капитальных затрат">Капитальных затрат</abbr>) требуется переходить в рабочую среду. Очень часто, добавление избыточности развертываниям частных облаков, чтобы избежать заниженных емкость во время пикового трафика в рабочей среде, но это увеличивает <abbr title="капитальных затрат">Капитальных затрат</abbr>. Потребность в избыточности определяется несбалансированное частных облаков, где некоторые узлы при размещении нескольких виртуальных машин (<abbr title="виртуальные машины">Виртуальные машины</abbr>) и другие используются недостаточно интенсивно (например, заново после перезагрузки сервера).

<strong>Краткий Видеообзор:</strong><br>(6 минут)<br>
> [!VIDEO https://channel9.msdn.com/Blogs/windowsserver/Virtual-Machine-Load-Balancing-in-Windows-Server-2016/player]

## <a id="what-is-vm-load-balancing"></a>Что такое Балансировка нагрузки виртуальной машины?
<abbr title="Виртуальная машина">Виртуальная машина</abbr> Балансировка нагрузки — это компонент в поле в Windows Server 2019 и Windows Server 2016, которая позволяет оптимизировать использование узлов в отказоустойчивом кластере. Он определяет перегруженное узлы и повторно распространяет <abbr title="виртуальные машины">Виртуальные машины</abbr> из этих узлов для узлов под committed. Некоторые ключевые аспекты этой функции, следующим образом:

* *Это решение без простоя*: <abbr title="Виртуальные машины">Виртуальные машины</abbr> — live перенесены в узлов в неактивном состоянии.
* *Удобная интеграция с существующей среды кластера*: Сбой политики, например удаление сходства, домены сбоя и возможные владельцы соблюдаются.
* *Эвристический подход для балансировки*: <abbr title="Виртуальная машина">Виртуальная машина</abbr> Нехватка памяти и ЦП узла.
* *Детальный контроль*: Включено по умолчанию. Может быть активирован по запросу или с периодическим интервалом.
* *Пороговые значения интенсивности*: Три пороговые значения доступны на основе характеристик развертывания.

## <a id="feature-in-action"></a>Функцию в действии
### <a id="new-node-added"></a>Добавляется новый узел в отказоустойчивом кластере
![График ключевого новый узел, добавляемый в отказоустойчивом кластере](media/vm-load-balancing/overview-VM-load-balancing-1.png)

При добавлении новой емкости в отказоустойчивом кластере, <abbr title="Виртуальной машины">Виртуальная машина</abbr> Функция балансировки нагрузки автоматически распределяет емкости с существующих узлов, на вновь добавленный узел, в следующем порядке:

1. Давление оценивается на существующие узлы в отказоустойчивом кластере.
2. Определены все узлы, превышение порогового значения.
3. Узлы с наибольшим давление определяются для определения приоритета балансировки.
4. <abbr title="Виртуальные машины">Виртуальные машины</abbr> будут перенесены Live (без прерывания работы) из узла, превышающие пороговое значение, чтобы вновь добавленный узел в отказоустойчивом кластере.

### <a id="recurring-load-balancing"></a>Повторяющиеся балансировки нагрузки
![График повторяющихся виртуальной машины Балансировка нагрузки](media/vm-load-balancing/overview-VM-load-balancing-2.png)

При настройке для периодического балансировки, давление на узлах кластера вычисляется для балансировки каждые 30 минут. Кроме того давление может быть вычисляются по требованию. Ниже приведена последовательность шагов:

1. Давление оценивается на всех узлах в частном облаке.
2. Определены все узлы, превышающие пороговое значение и расположенных ниже порогового значения.
3. Узлы с наибольшим давление определяются для определения приоритета балансировки.
4. <abbr title="Виртуальные машины">Виртуальные машины</abbr> — Динамическая миграция (без задержки) от узла, превышает пороговое значение для заданного порогового значения в узле.

## <a name="see-also"></a>См. также
* [Подробное описание балансировки нагрузки виртуальной машины](vm-load-balancing-deep-dive.md)
* [Отказоустойчивая кластеризация](failover-clustering-overview.md)
* [Обзор Hyper-V](../virtualization/hyper-v/Hyper-V-on-Windows-Server.md)