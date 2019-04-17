---
title: Мост (DCB) центра обработки данных
description: Вводная информация о мост для центра обработки данных в Windows Server 2016, можно использовать в этом разделе.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: da58f312-bd3b-4bb6-98ca-6177869dd6ad
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 3d465e855adc387d7136919ac11fbab56c792c34
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/28/2018
---
# <a name="data-center-bridging-dcb"></a>Мост \(DCB\) центра обработки данных

>Область применения: Windows Server (канал точками годовой), Windows Server 2016

Вводная информация о \(DCB\) мост для центра обработки данных можно использовать в этом разделе.

DCB — это набор стандартов институтом инженеров по электротехнике и электронике \(IEEE\) включающих Конвергентные структуры в центре обработки данных, где хранения, данных по сети, \(IPC\) Inter\ процесс взаимодействия кластера и трафик управления совместно используют ту же сетевую инфраструктуру Ethernet.

>[!NOTE]
>Дополнение к данному разделу доступна следующая документация DCB
>
>- [Установить мост центра обработки данных в Windows Server 2016 или Windows 10](dcb-install.md)
>- [Управление центром обработки данных (DCB) мост](dcb-manage.md)

Мост центра обработки данных обеспечивает распределение пропускной способности на основе hardware\ для конкретного типа сетевого трафика и повышает надежность передачи Ethernet с помощью управления потоками на основе priority\.

Распределение пропускной способности на основе Hardware\ важно в том случае, если трафик обходит операционную систему и разгружается в конвергентном сетевом адаптере, который может поддерживать интерфейс Internet \(iSCSI\), \(RDMA\) удаленного прямого доступа к памяти через Ethernet или оптоволоконный канал через Ethernet \(FCoE\).

Контроль потока на основе Priority\ важен в том случае, если протокол верхнего уровня, такой как Fiber Channel, предполагает базовую транспортировку без потерь.

## <a name="dcb-protocols-and-management-options"></a>Протоколы мост центра обработки данных и параметров управления

Мост центра обработки данных состоит из следующих набор протоколов. 

- Расширенные службы передачи \(ETS\) — IEEE 802.1Qaz, которая основана на 802.1 P и 802.1Q стандартов
- Приоритет потока управления \(PFS\) IEEE 802.1Qbb 
- Протокол Exchange DCB \(DCBX\) IEEE 802.1AB, как расширенной в стандартных 802.1Qaz.

Протокол DCBX позволяет настроить DCB на коммутаторе, который можно автоматически настроить циклом устройства, например компьютер под управлением Windows Server 2016.

Если вы хотите управлять DCB от коммутатора, не необходимо установить DCB как компонент в Windows Server 2016, однако такой подход включает некоторые ограничения.

Поскольку DCBX только может сообщить сетевого адаптера узла ETS класса размеров и включения PFC, однако узлов Windows Server обычно требуют установку DCB, чтобы трафик сопоставляется ETS классы.

Обычно приложения для Windows не предназначены для участвовать в обмене DCBX. По этой причине узел должен быть настроен отдельно от сетевых коммутаторов, но с идентичными параметрами.

При выборе для управления DCB от коммутатора можно по-прежнему просматривать конфигураций в Windows Server 2016 с помощью команд Windows PowerShell.

##  <a name="important-dcb-functionality"></a>Важные функции DCB

Ниже приведен список функций, предоставленных DCB.

1. Обеспечение взаимодействия между функцией DCB\ сетевые адаптеры и коммутаторы с поддержкой DCB\.

2. Предоставляет имеющего потерь транспорта Ethernet между компьютером под управлением Windows Server 2016 и его соседним коммутатором с помощью включения управления потоками на основе priority\ на сетевой адаптер.

3. Предоставляет возможность выделить пропускной способности \(TC\) управление трафиком в процентном соотношении, где управление ТРАФИКОМ может состоять из одного или нескольких классов трафика, отличающихся согласно индикаторы \(priority\) класс трафика 802.1p.

4. Позволяет администраторам сервера или сетевым администраторам возможности относить приложение к определенному классу трафика или на основе приоритета известным протоколам, известный порт TCP/UDP или NetworkDirect порта, используемым этим приложением.

5. Обеспечение управления БЛОКОМ управления через инструментарий Windows Server 2016 Windows управления \(WMI\) и Windows PowerShell. Дополнительные сведения см. раздел [команд Windows PowerShell для блока управления Каталогами](#bkmk_wps) далее в этом разделе, а также следующие разделы.
    - [Компоненты для предоставленных системой DCB](https://msdn.microsoft.com/windows/hardware/drivers/network/system-provided-dcb-components)
    - [Требования к QoS NDIS для моста для центра обработки данных](https://msdn.microsoft.com/windows/hardware/drivers/network/ndis-qos-requirements-for-data-center-bridging)

6. Обеспечение управления БЛОКОМ управления через групповую политику Windows Server 2016.

7. Поддерживает совместное существование Windows Server 2016 \(QoS\) решений обслуживания.

>[!NOTE]
>Прежде чем использовать любой RDMA по Конвергентной сети Ethernet \(RoCE\) версии RDMA, необходимо включить DCB. Хотя это не обязательно для протокола RDMA ширину области \(iWARP\) сетей, тестирование определила, улучшения работы всех технологий на основе Ethernet\ RDMA в DCB. По этой причине следует использовать DCB для iWARP RDMA развертываний. Дополнительные сведения см. в разделе [удаленный прямой доступ к памяти (RDMA) и коммутатора объединение ВНЕДРЕННЫХ](../../../virtualization/hyper-v-virtual-switch/RDMA-and-Switch-Embedded-Teaming.md).

##  <a name="practical-applications-of-dcb"></a>Практическое применение DCB

Многие организации имеют большое Fiber Channel \(FC\) хранилища области сети \(SAN\) установок для службы хранилища. Оптоволоконной сети хранения данных требуются специальные сетевые адаптеры на серверах и Оптоволоконных коммутаторах в сети. В таких организациях обычно также использовать сетевые адаптеры Ethernet и коммутаторы.

В большинстве случаев Оптоволоконного оборудования намного дороже, чем оборудование Ethernet, что приводит к повышению капитальных затрат развертывание. Кроме того требования для отдельных Ethernet и Оптоволоконной сети хранения данных сетевой адаптер и аппаратный коммутатор требует дополнительного пространства, энергии и охлаждения в центре обработки данных, что приводит к дополнительной постоянным эксплуатационным затратам.

С точки зрения стоимости для многих организаций объединить Оптоволоконные технологии с аппаратным Ethernet\ решением для хранения и службы сетевой обработки данных.

### <a name="using-dcb-for-an-ethernet-based-converged-fabric-for-storage-and-data-networking"></a>С помощью DCB для основе Ethernet\ конвергентную структуру для хранения данных и данных по сети

Для организаций, которые уже есть большой Оптоволоконной сети хранения данных, но желающих избежать дополнительных инвестиций в Оптоволоконную технологию, мост центра обработки данных позволяет создавать на основе Ethernet схождение выполнено структуры для хранения данных и данных по сети. DCB схождение выполнено структуры может снизить совокупную стоимость владения в будущем \(TCO\) и для упрощения управления.

Для поставщиков услуг размещения, которые уже приняли или планируют внедрить iSCSI в качестве решения хранилища, DCB может предоставить резервирование пропускной способности на основе hardware\ для трафика iSCSI, чтобы обеспечить изоляцию производительности. И, в отличие от других коммерческих решений мост центра обработки данных на основе standards\ - и таким образом, сравнительно легко развернуть и управлять им в разнородной сети.

Windows Server на основе 2016\ реализация DCB устраняет множество проблем, возникающих при гиперконвергентном что структуры решения предоставляются несколько \(OEMs\) изготовителями оборудования.

Реализации разных коммерческих решений, предоставляемых несколько изготовители оборудования не могут взаимодействовать друг с другом, может быть сложно управлять и они обычно используют разные графики программного обеспечения обслуживания. 

Напротив Windows Server 2016 мост центра обработки данных основан на standards\, и вы можете развернуть и управлять DCB в разнородной сети.

## <a name="bkmk_wps"></a>Команды Windows PowerShell для DCB

Существует команды DCB Windows PowerShell для Windows Server 2016 и Windows Server 2012 R2. Все команды можно использовать для Windows Server 2012 R2 в Windows Server 2016.

### <a name="windows-server-2016-windows-powershell-commands-for-dcb"></a>Команды Windows PowerShell Windows Server 2016 для DCB

Windows Server 2016 в следующем разделе приводится описание командлетов Windows PowerShell и синтаксис всех \(DCB\) мост для центра обработки данных качества обслуживания \ командлеты \-specific (QoS\). Он командлеты перечисляются в алфавитном порядке по команде в начале имени командлета.

- [Модуль DcbQoS](https://technet.microsoft.com/itpro/powershell/windows/dcbqos/dcbqos)

### <a name="windows-server-2012-r2-windows-powershell-commands-for-dcb"></a>Команды Windows Server 2012 R2 Windows PowerShell для DCB

Windows Server 2012 R2 в следующем разделе приводится описание командлетов Windows PowerShell и синтаксис всех \(DCB\) мост для центра обработки данных качества обслуживания \ командлеты \-specific (QoS\). Он командлеты перечисляются в алфавитном порядке по команде в начале имени командлета.

- [Качество обслуживания (QoS) командлетов в Windows PowerShell (DCB) мост центра обработки данных](https://technet.microsoft.com/library/hh967440.aspx)