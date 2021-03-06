---
title: Программно-конфигурируемая сеть (SDN)
description: Программно-определяемая сеть (SDN) позволяет централизованно настраивать и контролировать физические и виртуальные сетевые устройства, например маршрутизаторы, коммутаторы и шлюзы в центре обработки данных. В этом разделе содержатся сведения о технологиях программно-определяемой сети (SDN), предоставляемых в Windows Server, System Center и Microsoft Azure.
manager: grcusanz
ms.prod: windows-server
ms.technology: networking-sdn
ms.topic: article
ms.assetid: 9a1ea73c-20cd-42c5-95ad-b003b9cc6d64
ms.author: anpaul
author: AnirbanPaul
ms.date: 08/09/2018
ms.openlocfilehash: 355375b17132a46f070d5ef34cd6ea02a36868e0
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/08/2020
ms.locfileid: "80854337"
---
# <a name="sdn-in-windows-server-overview"></a>Обзор SDN в Windows Server

>Область применения: Windows Server (Semi-Annual Channel), Windows Server 2016


Программно-определяемая сеть (SDN) позволяет централизованно настраивать и контролировать физические и виртуальные сетевые устройства, например маршрутизаторы, коммутаторы и шлюзы в центре обработки данных. Вы можете использовать существующие устройства, совместимые с SDN, чтобы обеспечить более глубокую интеграцию между виртуальной сетью и физической сетью. Такие элементы виртуальной сети, как виртуальный коммутатор Hyper-V, виртуализация сети Hyper-V и шлюз RAS, являются неотъемлемой частью инфраструктуры SDN. 

>[!Note]
>На узлах Hyper-V и виртуальных машинах под управлением серверов инфраструктуры SDN, таких как узлы сетевого контроллера и программной балансировки нагрузки, должен быть установлен Windows Server 2016 Datacenter Edition. 
>
>Узлы Hyper-V, содержащие только виртуальные машины рабочей нагрузки клиента, подключенные к сетям, управляемым SDN, могут использовать Windows Server 2016 Standard Edition.

Это возможно, поскольку сетевые плоскости больше не привязаны к сетевым устройствам. Однако другие сущности, такие как программное обеспечение для управления центром обработки данных, например System Center 2016, используют сетевые плоскости. SDN позволяет динамически управлять сетью центра обработки данных, предоставляя автоматизированный, централизованный способ удовлетворения требований приложений и рабочих нагрузок. 

SDN можно использовать для:

- Динамически создавайте, Обеспечивайте безопасность и подключайте сеть для удовлетворения растущих потребностей ваших приложений.
- Ускоренное развертывание рабочих нагрузок без нарушения работы
- Защита от распространения уязвимостей по сети
- Определение и управление политиками, контролирующими как физические, так и виртуальные сети 
- Единообразная реализация сетевых политик в масштабе

SDN позволяет выполнять все эти операции, одновременно уменьшая общие затраты на инфраструктуру.



## <a name="contact-the-datacenter-and-cloud-networking-product-team"></a>Обращение к группе разработчиков центра обработки данных и облачных сетей

Если вы заинтересованы в обсуждении технологий SDN с корпорацией Майкрософт или другими клиентами SDN, существует множество методов для связи.

Дополнительные сведения см. [в разделе Обращение к команде "центр обработки данных" и "облачная сеть"](contact-sdn-team.md).
