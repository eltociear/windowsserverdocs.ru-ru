---
title: Удаленный доступ к памяти (RDMA) и объединение внедренных коммутаторов
description: В этом разделе содержит сведения о настройке интерфейсов удаленный доступ к памяти (RDMA) с Hyper-V в Windows Server 2016, а также сведения о коммутатора внедренных коммутаторов (SET).
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-hv-switch
ms.topic: get-started-article
ms.assetid: 68c35b64-4d24-42be-90c9-184f2b5f19be
ms.author: pashort
author: shortpatti
ms.openlocfilehash: c945144194ac86623bfa8ce60a306f0202df0874
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2019
ms.locfileid: "59881665"
---
# <a name="remote-direct-memory-access-rdma-and-switch-embedded-teaming-set"></a>Удаленный прямой доступ к памяти \(RDMA\) и объединение внедренных коммутаторов \(значение\)

>Область применения. Windows Server (полугодовой канал), Windows Server 2016

В этом разделе содержатся сведения о настройке удаленного прямого доступа к памяти \(RDMA\) взаимодействует с Hyper-V в Windows Server 2016, в дополнение к сведениям о Switch Embedded Teaming \(ЗАДАТЬ\).  

> [!NOTE]
> Помимо этого раздела доступно следующее содержимое Switch Embedded Teaming. 
> - Загрузка коллекции TechNet. [Windows Server 2016, сетевой Адаптер и Switch Embedded Teaming руководство](https://gallery.technet.microsoft.com/Windows-Server-2016-839cb607?redir=0)

## <a name="bkmk_rdma"></a>Настройка интерфейсов RDMA с Hyper-V  

В Windows Server 2012 R2 с помощью RDMA и Hyper-V на компьютере сетевых адаптеров, предоставляющие службы RDMA не могут быть привязаны к виртуальному коммутатору Hyper-V. Это увеличивает число физических сетевых адаптеров, которые требуются для установки на узле Hyper-V.

>[!TIP]
>В выпусках Windows Server до Windows Server 2016 не можно настроить RDMA на сетевых адаптерах, связанные в группу Сетевых карт или к виртуальному коммутатору Hyper-V. В Windows Server 2016 вы можете включить RDMA для сетевых адаптеров, привязанных к виртуальному коммутатору Hyper-V с или без НАБОРА.

В Windows Server 2016 при использовании RDMA с или без НАБОРА можно использовать меньшее количество сетевых адаптеров.

На следующем рисунке показаны изменения архитектуры программного обеспечения между Windows Server 2012 R2 и Windows Server 2016.

![Изменения в архитектуре](../media/RDMA-and-SET/rdma_over.jpg)

В следующих разделах приведены инструкции о том, как использовать команды Windows PowerShell для включения Data Center Bridging (DCB), создайте виртуальный коммутатор Hyper-V с помощью виртуального сетевого Адаптера RDMA \(виртуального сетевого адаптера\)и создайте виртуальный коммутатор Hyper-V с помощью НАБОРА и виртуальных сетевых адаптеров RDMA.

### <a name="enable-data-center-bridging-dcb"></a>Мост для центра обработки данных enable \(мост центра обработки данных\)

Прежде чем использовать любой RDMA over Converged Ethernet \(RoCE\) версии из RDMA, включите DCB.  Хотя не требуется для протокола RDMA ширину области \(iWARP\) сетей, тестирования определила, что все технологии RDMA на основе Ethernet улучшают работу DCB. По этой причине следует использовать DCB, даже для iWARP RDMA развертываний.

Следующие примеры команд Windows PowerShell показано, как включить и настроить DCB для SMB Direct.

Включить мост центра обработки данных

    Install-WindowsFeature Data-Center-Bridging

Установка политики для SMB Direct:

    New-NetQosPolicy "SMB" -NetDirectPortMatchCondition 445 -PriorityValue8021Action 3

Включение управления потоком для SMB:

    Enable-NetQosFlowControl  -Priority 3

Убедитесь, что отключено управление потоком для другого трафика:

    Disable-NetQosFlowControl  -Priority 0,1,2,4,5,6,7

Применить политику к целевым адаптерам:

    Enable-NetAdapterQos  -Name "SLOT 2"

Выделите для SMB Direct 30% минимум полосы пропускания:

`New-NetQosTrafficClass "SMB"  -Priority 3  -BandwidthPercentage 30  -Algorithm ETS`  

При наличии в системе установлен отладчик ядра, необходимо настроить отладчик, чтобы разрешить качества обслуживания для установки, выполнив следующую команду.

Переопределить отладчика — по умолчанию отладчик блокирует NetQos:
 
    Set-ItemProperty HKLM:"\SYSTEM\CurrentControlSet\Services\NDIS\Parameters" AllowFlowControlUnderDebugger -type DWORD -Value 1 -Force

### <a name="create-a-hyper-v-virtual-switch-with-an-rdma-vnic"></a>Создание виртуального коммутатора Hyper-V с помощью виртуального сетевого адаптера RDMA

Если НАБОР не является обязательным для развертывания, можно использовать следующие команды Windows PowerShell, чтобы создать виртуальный коммутатор Hyper-V с помощью виртуального сетевого адаптера RDMA.

> [!NOTE]
> С помощью НАБОРА команд с поддержкой RDMA физических сетевых адаптеров предоставляет дополнительные ресурсы RDMA для виртуальных сетевых адаптеров для использования.

    New-VMSwitch -Name RDMAswitch -NetAdapterName "SLOT 2"

Добавьте виртуальные сетевые карты узла и сделать их RDMA поддерживает:

    Add-VMNetworkAdapter -SwitchName RDMAswitch -Name SMB_1
    Enable-NetAdapterRDMA "vEthernet (SMB_1)" "SLOT 2"

Проверьте характеристики RDMA:

    Get-NetAdapterRdma

###  <a name="bkmk_set-rdma"></a>Создание виртуального коммутатора Hyper-V с помощью SET и RDMA

Чтобы использовать RDMA capabilies в Hyper-V размещение виртуальных сетевых адаптеров \(виртуальных сетевых адаптеров\) в виртуальном коммутаторе Hyper-V, поддерживает объединение RDMA, можно использовать эти примеры команд Windows PowerShell.

    New-VMSwitch -Name SETswitch -NetAdapterName "SLOT 2","SLOT 3" -EnableEmbeddedTeaming $true

Добавьте виртуальные сетевые карты узла:

    Add-VMNetworkAdapter -SwitchName SETswitch -Name SMB_1 -managementOS
    Add-VMNetworkAdapter -SwitchName SETswitch -Name SMB_2 -managementOS

Количество переключений не передать сведения о классе трафика непомеченный трафик виртуальной локальной сети, поэтому убедитесь, что адаптеры для RDMA, виртуальных локальных сетей. Этот пример назначает два SMB_ * виртуальные адаптеры узла 42 виртуальной локальной сети.
    
    Set-VMNetworkAdapterIsolation -ManagementOS -VMNetworkAdapterName SMB_1  -IsolationMode VLAN -DefaultIsolationID 42
    Set-VMNetworkAdapterIsolation -ManagementOS -VMNetworkAdapterName SMB_2  -IsolationMode VLAN -DefaultIsolationID 42
    

Включите RDMA на виртуальных сетевых адаптеров узла:

    Enable-NetAdapterRDMA "vEthernet (SMB_1)","vEthernet (SMB_2)" "SLOT 2", "SLOT 3"

Проверьте характеристики RDMA; Убедитесь, что возможности не равны нулю.

    Get-NetAdapterRdma | fl *


## <a name="bkmk_sswitchembedded"></a>Переключение внедренных объединения (SET)  

В этом разделе представлен обзор из коммутатора внедренных коммутаторов (SET) в Windows Server 2016 и содержит следующие разделы.

- [Общие сведения о НАБОРЕ](#bkmk_over)

- [НАБОР доступности](#bkmk_avail)

- [Поддерживаемые и неподдерживаемые сетевых адаптеров для НАБОРА](#bkmk_nics)

- [ЗАДАЙТЕ совместимость с сетевых технологий Windows Server](#bkmk_compat)

- [Режимы НАБОРА и параметры](#bkmk_modes)

- [НАБОР и очереди виртуальной машины (Vmq)](#bkmk_vmq)

- [НАБОР и виртуализации сети Hyper-V (HNV)](#bkmk_hnv)

- [УСТАНОВИТЕ и динамической миграции](#bkmk_live)

- [Использование MAC-адресов для передачи пакетов](#bkmk_mac)

- [Управляет командой SET](#bkmk_manage)

## <a name="bkmk_over"></a>Общие сведения о НАБОРЕ

НАБОР представляют собой альтернативное решение объединение Сетевых карт, который можно использовать в средах Hyper-V и программно-Конфигурируемую сеть \(SDN\) стек в Windows Server 2016. НАБОР объединяет некоторые функции объединения Сетевых карт в виртуальный коммутатор Hyper-V.

НАБОР позволяет группировать между одной и восемь физические сетевые адаптеры Ethernet в один или несколько программных виртуальных сетевых адаптеров. Эти виртуальные сетевые адаптеры обеспечивают высокую производительность и отказоустойчивость в случае сбоя сетевого адаптера.

НАБОР элементов сетевых адаптеров необходимо установить на одном физическом узле Hyper-V должно быть помещено в группу.

> [!NOTE]
> Использование НАБОРА поддерживается только в виртуальный коммутатор Hyper-V в Windows Server 2016. Невозможно развернуть SET в Windows Server 2012 R2.

Ваш объединенные сетевые адаптеры можно подключиться к одному физическому коммутатору или к разным физическим коммутаторам. Если сетевых адаптеров подключаться к разным коммутаторам, оба параметра должны находиться в той же подсети.

На следующем рисунке показана архитектура.

![Архитектура](../media/RDMA-and-SET/set_architecture.jpg)

Так как НАБОР интегрирована в виртуальный коммутатор Hyper-V, нельзя использовать SET внутри виртуальной машины (VM). Однако можно использовать объединение Сетевых карт в виртуальных машинах.

Дополнительные сведения см. в разделе [объединение Сетевых карт в виртуальных машинах (ВМ)](https://docs.microsoft.com/windows-server/networking/technologies/nic-teaming/nict-vms).

Кроме того архитектура не предоставляет интерфейсы team. Вместо этого необходимо настроить порты виртуального коммутатора Hyper-V.

## <a name="bkmk_avail"></a>НАБОР доступности

НАБОР доступен во всех версиях Windows Server 2016, включающие Hyper-V и стек SDN. Кроме того можно использовать команды Windows PowerShell и подключения удаленного рабочего стола для управления НАБОРОМ с удаленных компьютеров, работающих под управлением клиентской операционной системы, на котором поддерживаются средства.

## <a name="bkmk_nics"></a>Поддерживаемые сетевые адаптеры для НАБОРА

Можно использовать любую сетевую КАРТУ Ethernet, прошедшей квалификации оборудования Windows и логотип \(WHQL\) тестирование в команде SET в Windows Server 2016. НАБОР требует, что все сетевые адаптеры, которые являются членами команды SET должны совпадать \(т. е. же производителя, одной модели, же встроенного по и драйвера\). НАБОР поддерживает между одной и восемь сетевых адаптеров в группе.
  
## <a name="bkmk_compat"></a>ЗАДАЙТЕ совместимость с сетевых технологий Windows Server

НАБОР совместим со следующими сетевыми технологиями в Windows Server 2016.

- Мост для центра обработки данных \(мост центра обработки данных\)
  
- Виртуализация сетей Hyper-V — NV GRE и VxLAN поддерживаются в Windows Server 2016.  
- Разгрузка контрольной суммы на стороне приема \(IPv4, IPv6, TCP\) -они поддерживаются, если любой из членов команды SET поддерживает их.

- Удаленный прямой доступ к памяти \(RDMA\)

- Виртуализация SR-iov \(SR-IOV\)

- Разгрузка контрольной суммы передачи со стороны \(IPv4, IPv6, TCP\) -они поддерживаются, если все члены команды SET поддерживают их.

- Очереди виртуальной машины \(VMQ\)

- Виртуальный масштабирование на стороне приема \(RSS\)

НАБОР не совместим с следующие сетевые технологии в Windows Server 2016.

- Проверка подлинности 802.1 X. 802. 1 протокол расширенной проверки подлинности x \(EAP\) пакетов, автоматически удаляется инструкцией Hyper\-V виртуального коммутатора в сценарии НАБОРОВ.
 
- Разгрузка задач IPsec \(IPsecTO\). Это устаревшая технология, которая не поддерживается в большинстве сетевых адаптеров, и где он существует, она отключена по умолчанию.

- Использование службы качества обслуживания \(pacer.exe\) в узел или операционной системы в машинном коде. Эти сценарии QoS не Hyper\-V сценариев, поэтому эти технологии не пересекаются. Кроме того QoS — доступны, но не включены по умолчанию — намеренно, необходимо настроить службу качества обслуживания.

- Объединение полученных стороне \(RSC\). Технология RSC отключена по Hyper\-V виртуального коммутатора.

- Масштабирование на стороне приема \(RSS\). Так как Hyper-V использует очереди для VMQ и VMMQ, RSS всегда отключена при создании виртуального коммутатора.

- Разгрузка TCP Chimney. Эта технология отключена по умолчанию.

- Качество обслуживания виртуальной машины \(качества обслуживания виртуальной Машины\). QoS виртуальных Машин — доступны, но по умолчанию отключено. Если вы настраиваете качества обслуживания виртуальной Машины в среде SET, параметры качества обслуживания будет привести к непредсказуемым результатам.

## <a name="bkmk_modes"></a>Режимы НАБОРА и параметры

При создании команды SET, в отличие от объединение Сетевых карт, нельзя настроить имя команды. Кроме того используется резервный адаптер поддерживается в объединении Сетевых карт, но не поддерживается в НАБОРЕ. При развертывании НАБОРА все сетевые адаптеры активны, и ни одна не в режиме ожидания.

Еще одно важное отличие между объединение Сетевых карт и НАБОРОМ том, что объединение Сетевых карт предоставляет выбор из трех вариантов объединения, а НАБОР поддерживает только **не зависит от коммутатора** режим. С не зависит от коммутатора режима коммутатор или переключателей, к которым подключены ЗАДАТЬ участники не знают о наличие НАБОРА team и не определяют способ распределения сетевого трафика, чтобы ЗАДАТЬ члены команды - вместо этого команда SET распределяет входящего сетевого трафика трафик между участниками команды SET.

При создании новой команды SET, необходимо настроить следующие свойства команды.

- Адаптеры членов

- Режим балансировки нагрузки

### <a name="member-adapters"></a>Адаптеры членов

При создании команды SET, необходимо указать до восьми одинаковые сетевые адаптеры, которые привязаны к виртуальному коммутатору Hyper-V как адаптеры членов команды SET.

### <a name="load-balancing-mode"></a>Режим балансировки нагрузки

Группы параметров для НАБОРА балансировки нагрузки, режим распределения **порта Hyper-V** и **динамическое**.

**Порт Hyper-V**

Виртуальные машины будут подключены к порту на виртуальном коммутаторе Hyper-V. При использовании режима порта Hyper-V для НАБОРА команд, портом виртуального коммутатора Hyper-V и связанных MAC-адреса используются для разделения сетевого трафика между членами группы НАБОРА.

> [!NOTE]
> При использовании НАБОРА в сочетании с Packet Direct, на режим поддержки групп **не зависит от коммутатора** и режим балансировки нагрузки **порта Hyper-V** являются обязательными.

Поскольку соседний коммутатор всегда видит определенный MAC-адрес на определенный порт, коммутатор распределяет нагрузку входящего трафика (трафик от коммутатора к узлу) к порту, где находится MAC-адрес. Это особенно полезно при использовании очереди виртуальной машины (Vmq), так как очередь можно разместить на конкретную сетевую КАРТУ, где трафик должен поступать.

Тем не менее если узел имеет несколько виртуальных машин, этот режим может оказаться достаточно детализирован и может получить хорошее распределение. Этот режим также всегда будет ограничивать отдельную виртуальную Машину (т. е. трафик с порта один коммутатор) пропускной способности, которая доступна на одном интерфейсе.

**динамические**

Этот режим балансировки нагрузки обеспечивает следующие преимущества.

- Исходящие загружает распределяются по хэшу TCP-порты и IP-адресов.  Динамический режим также повторно распределяет загружается в режиме реального времени, заданного исходящего потока можно перемещаться вперед и назад между участниками команды SET.

- Входящий загружает распространяются в так же, как режим порта Hyper-V.

Динамически распределяются на основе использует концепцию flowlets исходящих загружает в этом режиме. Так же, как телефонных разговоров имеет естественным разрывов в конце слов и предложений, потоки обычного протокола TCP (потоки связи TCP) также разрывами естественным образом встречающиеся. Часть поток TCP между два разрыва называется flowlet.

При динамическом режиме алгоритм обнаруживает, что было обнаружено границе flowlet - например когда разрыв достаточной длины произошла в потоке TCP - алгоритм автоматически перераспределит потока другому члену команды, при необходимости.  В некоторых редких обстоятельствах алгоритм может также периодически перераспределять потоки, которые не содержат все flowlets. По этой причине сходство между член потока и команда TCP можно изменить в любое время, как работает динамический алгоритм балансировки для распределения рабочей нагрузки из участников команды.

## <a name="bkmk_vmq"></a>НАБОР и очереди виртуальной машины (Vmq)

VMQ и ЗАДАТЬ эффективной совместной работы, и следует включить очередь виртуальных МАШИН, каждый раз, когда вы используете Hyper-V и УСТАНОВИТЬ.

> [!NOTE]
> ЗНАЧЕНИЕ всегда представляет общее количество очередей, которые доступны через НАБОР все члены команды. В объединении Сетевых карт это называется режимом суммы из очереди.

Большинство сетевые адаптеры имеют очередей, которые могут использоваться для либо масштабирование на стороне приема \(RSS\) или VMQ, но не оба одновременно.
  
Некоторые параметры VMQ могут быть параметры для очередей RSS, но действительно приведены параметры на универсальный очереди, RSS и VMQ в зависимости от того, какая функция используется в настоящее время используется. Каждый сетевой Адаптер имеет в его расширенные свойства, значения для `*RssBaseProcNumber` и `*MaxRssProcessors`.

Ниже приведены некоторые параметры VMQ, которые повышают производительность системы.

- В идеале каждый сетевой Адаптер должен иметь `*RssBaseProcNumber` присвоено четным числом больше или равно двум (2). Это обусловлено первый физический процессор Core 0 \(логических процессоров 0 и 1\), обычно выполняет большую часть обработки системы, поэтому нужно управлять сетевой обработки от этого физического процессора. 

>[!NOTE]
>Некоторые архитектуры машины не имеют два логических процессора одного физического процессора, поэтому для таких машин базового процессора должен быть больше или равно 1. Если вы сомневаетесь, предположим, что ваш сайт использует 2 логических процессоров на основе архитектуры физического процессора.

- Должен быть участников группы процессоров, при условии, что практические, перекрываться. Например, в основном приложении 4-ядерный \(8 логических процессоров\) вместе с командой двумя сетевыми адаптерами 10 Гбит/с, можно задать первый из них использовать базовый обработчик 2 и использовать 4 ядра; второй будет иметь значение использовать базовый обработчик 6 и использовать 2 ядра.

## <a name="bkmk_hnv"></a>НАБОР и Hyper-V виртуализация сети \(HNV\)

НАБОР полностью совместима с виртуализацией сети Hyper-V в Windows Server 2016. Система управления HNV сведения для НАБОРА драйвер, который позволяет НАБОРА для распределения сетевого трафика, меняя таким образом, оптимизирован для трафика HNV.
  
## <a name="bkmk_live"></a>УСТАНОВИТЕ и динамической миграции

Динамическая миграция поддерживается в Windows Server 2016.

## <a name="bkmk_mac"></a>Использование MAC-адресов для передачи пакетов

При настройке команды SET с распределением динамической нагрузке, пакеты из одного источника \(например одной виртуальной Машины\) одновременно распределяются между несколькими участниками группы. 

Предотвратить получение путать переключатели и чтобы предотвратить MAC хлопания сигналы, ЗАДАЙТЕ заменяет исходный MAC-адрес другой MAC-адрес на кадры, которые передаются на члены команды, отличный от участника непотоковой команды. По этой причине каждый член команды использует другой MAC-адрес, и конфликты MAC-адресов блокируются до тех пор, пока не происходит сбой.

При обнаружении ошибки в основной сетевой КАРТЫ, НАБОР, программное обеспечение для объединения начинается с помощью MAC-адрес виртуальной Машины на участника команды, который выбирается в качестве участника команды временный непотоковой \(т. е. того, который отобразится в коммутатор как виртуальной Машины интерфейс\).

Это изменение применяется только к трафику, который происходит отправляемых участниками MAC-адресом Виртуальной машины собственные непотоковой виртуальной Машины в качестве источника MAC-адрес. Другой трафик продолжает отправлять с любой исходный MAC-адрес, могла бы использовать до сбоя.

Ниже приведены списки, которые описывают НАБОР карт поведение замены адрес MAC, в зависимости от того, как настроена группа:

- В режиме, не зависит от коммутатора с распределением порта Hyper-V

    - Каждый порт vmSwitch приводится в соответствие члену команды
  
    - Каждый пакет отправляется на член команды, к которому приводится в соответствие порт  
  
    - Источник замены MAC не выполняется  
  
- В режиме, не зависит от коммутатора с помощью динамического распределения
  
    - Каждый порт vmSwitch приводится в соответствие члену команды  
  
    - Все пакеты ARP/NS отправляются на член команды, к которому приводится в соответствие порт  
  
    - Пакеты, отправляемые на участника команды, который является членом группы сходных иметь источник не выполнена замена адрес MAC  
  
    - Пакеты, отправляемые на элемент группы, кроме непотоковой team будет иметь адрес источника MAC замены с Готово  
  
## <a name="bkmk_manage"></a>Управляет командой SET

Рекомендуется использовать System Center Virtual Machine Manager \(VMM\) для управления НАБОРОМ командами, однако можно также использовать Windows PowerShell для управления НАБОРОМ. Следующие разделы содержат команд Windows PowerShell можно использовать для управления НАБОРОМ.

Сведения о том, как создать НАБОР команды с помощью VMM, см. в разделе «Настройка логического коммутатора» в статье библиотеки System Center VMM [Создание логических коммутаторов](https://docs.microsoft.com/system-center/vmm/network-switch).
  
### <a name="create-a-set-team"></a>Создать команду SET

Необходимо создать в то же время, создать виртуальный коммутатор Hyper-V с помощью команды SET **New-VMSwitch** команду Windows PowerShell.

При создании виртуального коммутатора Hyper-V, необходимо включить в него новые **EnableEmbeddedTeaming** параметр в синтаксис команды. В следующем примере с именем коммутатора Hyper-V **TeamedvSwitch** с embedded teaming и два первоначальном командном создается членов.
  
```  
New-VMSwitch -Name TeamedvSwitch -NetAdapterName "NIC 1","NIC 2" -EnableEmbeddedTeaming $true  
```  
  
**EnableEmbeddedTeaming** параметра подразумевается по Windows PowerShell при аргументе **NetAdapterName** представляет собой массив сетевых адаптеров, а не один сетевой интерфейс. В результате выполнения предыдущей команды мог пересмотреть следующим образом.

```  
New-VMSwitch -Name TeamedvSwitch -NetAdapterName "NIC 1","NIC 2"  
```  

Если вы хотите создать НАБОР с поддержкой переключитесь с один таким образом, чтобы член команды можно добавить позже, то необходимо использовать параметр EnableEmbeddedTeaming.

```  
New-VMSwitch -Name TeamedvSwitch -NetAdapterName "NIC 1" -EnableEmbeddedTeaming $true  
```  

### <a name="adding-or-removing-a-set-team-member"></a>Добавление или удаление член команды SET

**Набора VMSwitchTeam** команда включает в себя **NetAdapterName** параметр. Для изменения членам команды в команде SET, введите нужный список членов группы после **NetAdapterName** параметр. Если **TeamedvSwitch** был изначально создан с сетевого Адаптера 1 и 2 сетевой Адаптер, то следующая команда удаляет член команды SET «NIC 2» и добавляет новый член команды SET «сетевой Адаптер 3".
  
```  
Set-VMSwitchTeam -Name TeamedvSwitch -NetAdapterName "NIC 1","NIC 3"  
```  

### <a name="removing-a-set-team"></a>Удаление группой НАБОРА

Команда SET можно удалить только путем удаления виртуальный коммутатор Hyper-V, содержащий команды SET.  Используйте раздел [Remove-VMSwitch](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/remove-vmswitch) сведения о том, как удалить виртуальный коммутатор Hyper-V. В следующем примере удаляется виртуальный коммутатор с именем **SETvSwitch**.

```  
Remove-VMSwitch "SETvSwitch"  
```  

### <a name="changing-the-load-distribution-algorithm-for-a-set-team"></a>Изменение в основе алгоритма распределения нагрузки для команды SET

**Набора VMSwitchTeam** командлет имеет **LoadBalancingAlgorithm** параметр. Этот параметр принимает одно из двух возможных значений: **HyperVPort** или **динамическое**. Чтобы задать или изменить в основе алгоритма распределения нагрузки для команды switch embedded, используйте этот параметр. 

В следующем примере с именем VMSwitchTeam **TeamedvSwitch** использует **динамическое** алгоритм балансировки нагрузки.  
```  
Set-VMSwitchTeam -Name TeamedvSwitch -LoadBalancingAlgorithm Dynamic  
```  
### <a name="affinitizing-virtual-interfaces-to-physical-team-members"></a>Установка соответствия виртуальных интерфейсов физических участникам

НАБОР позволяет создание сопоставления между виртуальным интерфейсом \(т. е. порт виртуального коммутатора Hyper-V\) и один из физических сетевых адаптеров в группе. 

Например, при создании двух размещения виртуальных сетевых адаптеров для SMB\-напрямую, как описано в разделе [Создание виртуального коммутатора Hyper-V с помощью SET и RDMA](#bkmk_set-rdma), убедитесь, что два виртуальных сетевых адаптеров использовать разные члены команды. 

Добавление в сценарий в этом разделе, можно использовать следующие команды Windows PowerShell.

    Set-VMNetworkAdapterTeamMapping -VMNetworkAdapterName SMB_1 –ManagementOS –PhysicalNetAdapterName “SLOT 2”
    Set-VMNetworkAdapterTeamMapping -VMNetworkAdapterName SMB_2 –ManagementOS –PhysicalNetAdapterName “SLOT 3”

Эта тема рассматривается более подробно в разделе 4.2.5 [Windows Server 2016, сетевой Адаптер и Switch Embedded Teaming руководство пользователя по](https://gallery.technet.microsoft.com/Windows-Server-2016-839cb607?redir=0).