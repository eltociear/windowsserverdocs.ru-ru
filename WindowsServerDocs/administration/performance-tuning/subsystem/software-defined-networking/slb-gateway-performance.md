---
title: Настройка в программном обеспечении производительности шлюза SLB определенные сетей
description: Шлюз SLB рекомендации по настройке производительности в сетях SDN
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: grcusanz; AnPaul
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: fede7d404ddbb4f465eff435cc340db1907ce9d2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2019
ms.locfileid: "59829935"
---
# <a name="slb-gateway-performance-tuning-in-software-defined-networks"></a>Настройка в программном обеспечении производительности шлюза SLB определенные сетей

Балансировка нагрузки программного обеспечения предоставляется с помощью сочетания диспетчера подсистемы балансировки нагрузки в виртуальные машины сетевого контроллера, виртуальный коммутатор Hyper-V и набором виртуальных машин Multixplexor подсистемы балансировки нагрузки (Mux).

Нет дополнительных настройках производительности необходим для настройки сетевого контроллера или узел Hyper-V для балансировки дальше описан в [программно-Конфигурируемую сеть](index.md) раздел, если только вы будете использовать SR-IOV для Мультиплексорами, как описано ниже.

## <a name="slb-mux-vm-configuration"></a>Конфигурация виртуальной Машины мультиплексора SLB

В конфигурации активный-активный развернуты виртуальные машины SLB/Mux.  Это означает, что каждая виртуальная машина мультиплексора, развертывания и добавляемый сетевой контроллер может обрабатывать входящие запросы.  Таким образом общее суммарная пропускная способность всех подключений ограничивается только число виртуальных машин мультиплексора, что было развернуто.  

Отдельного подключения к виртуальному IP-адрес (VIP) всегда отправляются же мультиплексора, при условии, что количество мультиплексорами остается постоянным, и поэтому ее пропускная способность будет ограничена пропускная способность одной виртуальной машины мультиплексора.  Мультиплексорами только обработки входящего трафика, предназначенного для VIP-адрес.  Пакетов ответа перейдите непосредственно из виртуальной Машины, который отправляет ответ на физическом коммутаторе, а затем перенаправляются клиенту.

В некоторых случаях когда источник запроса от узлом SDN, который добавляется к одному контроллеру сети, который управляет виртуального IP-адреса, дальнейшая оптимизация входящего пути для запроса также выполняется позволяющий большинство пакеты передаются непосредственно из клиент к серверу, полностью обход виртуальной Машины мультиплексора.  Никаких дополнительных настроек не требуется для этой оптимизации вступили в силу.

Каждой виртуальной Машины мультиплексора SLB, должен иметь размер в соответствии с рекомендациями из SDN разделу инфраструктуры в виртуальную машину роли требования [планирование инфраструктуры программно-определяемой сети](../../../../networking/sdn/plan/Plan-a-Software-Defined-Network-Infrastructure.md) раздела.

## <a name="single-root-io-virtualization-sr-iov"></a>Единый корневой виртуализация ввода-ВЫВОДА (SR-IOV)

При использовании 40 Гбит Ethernet, возможность для виртуального коммутатора, который процесс пакетов для виртуальной Машины мультиплексора становится ограничивающим фактором для пропускной способности виртуальной Машины мультиплексора.  По этой причине рекомендуется включить SR-IOV на сетевом адаптере виртуальной Машины SLB виртуальной Машины, чтобы убедиться, что виртуальный коммутатор не является узким местом.

Чтобы включить SR-IOV, необходимо включить его на виртуальном коммутаторе, при создании виртуального коммутатора.  В этом примере мы создаем виртуальный коммутатор с switch embedded teaming (SET) и SR-IOV:
``` syntax
    new-vmswitch -Name SDNSwitch -EnableEmbeddedTeaming $true -NetAdapterName @("NIC1", "NIC2") -EnableIOV $true
```
Затем его необходимо включить на виртуальных сетевых адаптеров виртуальной машины мультиплексора SLB, которое обрабатывает трафик данных.  В этом примере SR-IOV включается для всех адаптеров:
``` syntax
    get-vmnetworkadapter -VMName SLBMUX1 | set-vmnetworkadapter -IovWeight 50
```