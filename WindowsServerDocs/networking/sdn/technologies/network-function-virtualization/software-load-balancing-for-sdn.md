---
title: Программная балансировка нагрузки для SDN
description: Дополнительные сведения о балансировке нагрузки программного обеспечения для программно-Конфигурируемую сеть в Windows Server 2016 можно использовать в этом разделе.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 97abf182-4725-4026-801c-122db96964ed
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 26fb4aa21e80618c4c63bd9edbf8731bf886db62
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2019
ms.locfileid: "59853765"
---
# <a name="software-load-balancing-slb-for-sdn"></a>Программная Балансировка нагрузки \(SLB\) для SDN

>Относится к: Windows Server (полугодовой канал), Windows Server 2016

Дополнительные сведения о балансировке нагрузки программного обеспечения для программно-Конфигурируемую сеть в Windows Server 2016 можно использовать в этом разделе.  

Поставщиков облачных служб (CSP) и предприятия, развертывающие программно определяемой сети (SDN) в Windows Server 2016 можно использовать для равномерного распределения клиента клиент сетевого трафика между ресурсами виртуальной сети клиента и балансировка нагрузки программного обеспечения (SLB). Windows Server SLB позволяет размещать одну и ту же рабочую нагрузку на нескольких серверах, что обеспечивает высокий уровень доступности и масштабирование.
  
Windows Server SLB включает в себя следующие возможности.  
  
-   Службы балансировки для «Север-Юг» и «Восток-Запад» TCP/UDP трафика нагрузки уровня 4 (уровень 4).  
  
-   Открытые и внутренние трафика Балансировка сетевой нагрузки.  
  
-   Поддерживает динамические IP-адреса (DIP), виртуальные локальные сети (VLAN) и виртуальных сетей, создаваемые с помощью виртуализации сети Hyper-V.  
  
-   Поддержка проверки работоспособности.  
  
-   Готова для масштабирования в облаке, включая возможность горизонтального масштабирования и масштаб возможностей для Мультиплексоры и узлов агентов.  
  
Дополнительные сведения см. в разделе [функции балансировки нагрузки программного обеспечения](#bkmk_features) в этом разделе.  
  
> [!NOTE]  
> Мультитенантности, для виртуальных сетей не поддерживается сетевым контроллером, тем не менее можно использовать виртуальные локальные сети с помощью SLB для поставщика служб управляемых рабочих нагрузок, например инфраструктуру центров обработки данных и веб-серверов с высокой плотностью.  
  
С помощью Windows Server SLB, можно масштабировать ваши возможности балансировки нагрузки с помощью виртуальных машин SLB на тех же серверах вычислений Hyper-V, используемых для других рабочих нагрузок виртуальных Машин. По этой причине SLB поддерживает быстрое создание и удаление конечные точки балансировки нагрузки, необходимые для операций CSP. Кроме того Windows Server SLB поддерживает десятки гигабайт на кластер, представлена простая модель подготовки и легко разворачивания и сворачивания.  
  
**Как работает SLB**  
  
SLB работает путем сопоставления виртуальных IP-адресов (VIP) с динамические IP-адреса (DIP), которые являются частью набора службы облачных ресурсов в центре обработки данных.  
  
Виртуальные IP-адреса являются IP-адресам, предоставляющие общий доступ к пулу нагрузки виртуальных машин с балансировкой. Например виртуальные IP-адреса являются IP-адресов, которые доступны в Интернете, клиентов и клиентов для подключения к ресурсам клиента в облачный центр обработки данных.  
  
Частные интерфейсы являются IP-адреса виртуальных машин с балансировкой нагрузки пула за VIP-адрес элемента. Частные интерфейсы назначаются в рамках облачной инфраструктуры к ресурсам клиента.  
  
Виртуальные IP-адреса находятся в SLB мультиплексор (Мультиплексор).  Мультиплексор состоит из одного или нескольких виртуальных машин (ВМ).  Сетевой контроллер обеспечивает каждого Мультиплексора с каждого виртуального IP-адреса, а каждый Мультиплексора в свою очередь использует протокол пограничного шлюза (BGP) для объявления каждого виртуального IP-адреса для маршрутизаторов в физической сети, как это маршрута.  BGP позволяет физическими сетевыми маршрутизаторами для:  
  
-   Узнайте, что VIP-адрес доступен на каждый Мультиплексора, даже если Мультиплексорами принадлежат разным подсетям в сети уровня 3.  
  
-   Распределите нагрузку для каждого виртуального IP-адреса на всех доступных Мультиплексорами, с помощью маршрутизации многопутевых равны стоимости (ECMP).  
  
-   Автоматическое определение Мультиплексора сбой или демонтажа и прекратили отправлять трафик на сбой Мультиплексора.  
  
-   Распределите нагрузку из Мультиплексора неудачных или удаленные на работоспособное Мультиплексорами.  
  
По прибытии общего трафика из Интернета, SLB/MUX проверяет трафик, который содержит виртуальный IP-адрес, как назначение и сопоставляет и перезаписывает трафик, таким образом, чтобы он поступает на отдельных DIP. Для входящего сетевого трафика эта транзакция выполняется в два этапа, распределенный между Мультиплексора виртуальные машины (VM) и узла Hyper-V, где находится целевой DIP-адрес:  
  
-   Балансировка нагрузки — Мультиплексора использует виртуальный IP-адрес, чтобы выбрать DIP, инкапсулирует пакет и перенаправляет трафик на узел Hyper-V, где находится DIP.  
  
-   Преобразование сетевых адресов (NAT) — на узле Hyper-V удаляет инкапсуляция из пакета, преобразует VIP к DIP, повторно отображает порты и пересылает его DIP виртуальной Машины.  
  
Мультиплексор знает, как сопоставляются правильный частные интерфейсы виртуальных IP-адресов из-за политики, которые определяются с помощью сетевого контроллера балансировки нагрузки. Эти правила включают протокол, интерфейсный порт, внутренний порт и алгоритм распределения (5, 3 или 2 кортежей).  
  
При клиента, которые отвечать виртуальных машин и отправки исходящего сетевого трафика обратно к Интернету или расположения удаленного клиента, поскольку NAT осуществляется на узле Hyper-V, трафик обходит Мультиплексора и переходит непосредственно для пограничного маршрутизатора с узла Hyper-V. Этот процесс обхода Мультиплексора называется прямой ответ от сервера (DSR).  
  
И после начальной сетевой трафик, входящий трафик обходит SLB/MUX полностью.  
  
На следующем рисунке клиентский компьютер выполняет запрос DNS для IP-адреса корпоративного сайта SharePoint — в этом случае в вымышленной компании Contoso. Следующая процедура выполняется.  
  
-   DNS-сервер возвращает 107.105.47.60 виртуальный IP-адрес клиенту.  
  
-   Клиент отправляет запрос HTTP на VIP-адрес.  
  
-   Физической сети имеет несколько путей, доступных для доступа к виртуальным IP-адресом, расположенных на любой Мультиплексора.  Каждый маршрутизатор использует ECMP, чтобы выбрать следующего сегмента пути, пока запрос достигает Мультиплексора.  
  
-   Мультиплексора, который получает запрос проверяет настроенных политик и видит, что доступно, два спада 10.10.10.5 и 10.10.20.5 в виртуальной сети для обработки запроса 107.105.47.60 виртуальный IP-адрес  
  
-   Мультиплексор выбирает 10.10.10.5 DIP-адрес и инкапсулирует пакеты с помощью VXLAN, поэтому он может отправить его на узел, содержащий DIP-адрес, используя узлы физический сетевой адрес.  
  
-   Узел получает инкапсулированный пакет и проверяет его.  Она удаляет инкапсуляция и перезаписывает пакета, поэтому назначения становится DIP 10.10.10.5, а не виртуальный IP-адрес и отправляет трафик в DIP виртуальной Машины.  
  
-   Запрос достиг теперь сайта Contoso SharePoint в ферме Server 2. Сервер формирует ответ и отправляет его клиенту, используя собственный IP-адрес в качестве источника.  
  
-   Узел перехватывает исходящих пакетов в виртуальный коммутатор, который запоминает, клиента, теперь назначения, исходный запрос виртуальный IP-адрес.  Узел перезаписывает источника пакета можно виртуального IP-адреса, поэтому, чтобы клиент не видит выделенный IP-адрес.  
  
-   Узел перенаправляет пакет непосредственно на шлюз по умолчанию для физической сети, использующий стандартный таблице маршрутизации для пересылки пакетов на клиент, который в конечном итоге получает ответ.  
  
![Процесс балансировки нагрузки программного обеспечения](../../../media/Software-Load-Balancing--SLB--for-SDN/slb_process.jpg)  
  
**Балансировка нагрузки внутреннего центра обработки данных трафика**  
  
Когда балансировки нагрузки сетевого трафика внутренним для центра обработки данных, такие как между ресурсов клиентов, которые работают на разных серверах и являются членами одной виртуальной сети, виртуальный коммутатор Hyper-V, к которому подключены виртуальные машины NAT.  
  
Внутренний трафик балансировки нагрузки, первый запрос отправляется и обрабатывается Мультиплексора, который выбирает соответствующий DIP-адрес и направляет трафик на DIP. С этого момента установленного трафик обходит Мультиплексора и переходит непосредственно из виртуальной Машины к виртуальной Машине.  
  
**Пробы работоспособности.**  
  
SLB включает в себя проверку работоспособности для проверки работоспособности сетевой инфраструктуры, включая следующие.  
  
-   Проба TCP к порту  
  
-   Проверка HTTP, порт и URL-адрес  
  
В отличие от традиционных устройства для балансировки нагрузки где Проба поступает с устройства и хранении и передаче на DIP, зонд SLB происходит на узле, где расположен DIP-адрес и выполняется напрямую с SLB агент узла на DIP, дальнейшего распространения работать между узлами.  
  
## <a name="bkmk_infrastructure"></a>Инфраструктура балансировки нагрузки программного обеспечения  
Чтобы развернуть Windows Server SLB, необходимо произвести развертывание сетевого контроллера в Windows Server 2016 и один или несколько виртуальных машин SLB/MUX.  
  
Кроме того необходимо настроить узлы Hyper-V с помощью виртуального коммутатора Hyper-V с поддержкой SDN и убедитесь, что запущен агент узла SLB.  Маршрутизаторы, обслуживающим узлы должны поддерживать маршрутизацию равной цены multipath (ECMP) и протокола пограничного шлюза (BGP) и должен быть настроен на прием запросов пиринга BGP от Мультиплексорами SLB.  
  
Ниже приведен обзор инфраструктуры SLB.  

![Инфраструктура Балансировка нагрузки программного обеспечения](../../../media/Software-Load-Balancing--SLB--for-SDN/slb_overview1.png)  
  
Дополнительные сведения об этих элементах инфраструктуры SLB в следующих разделах.  
  
### <a name="scvmm"></a>SCVMM  
С помощью System Center 2016 можно настроить сетевого контроллера в Windows Server 2016, включая диспетчера SLB и монитор работоспособности. System Center также можно использовать для развертывания SLB MUXs и для установки SLB узлов агентов на компьютерах, работающих под управлением Windows Server 2016 и Hyper-V.  
  
Дополнительные сведения о System Center 2016, см. в разделе [System Center 2016](https://www.microsoft.com/server-cloud/products/system-center-2016/).  
  
> [!NOTE]  
> Если вы не хотите использовать System Center 2016, Windows PowerShell или другого управляющего приложения можно использовать для установки и настройки сетевого контроллера и другой инфраструктуры SLB. Дополнительные сведения см. в разделе [развертывание сетевого контроллера с помощью Windows PowerShell](../../../sdn/deploy/Deploy-Network-Controller-using-Windows-PowerShell.md).  
  
### <a name="network-controller"></a>Сетевой контроллер  
Сетевой контроллер размещает диспетчера SLB и выполняет следующие действия для SLB.  
  
-   Обрабатывает команды SLB, поступающих через Северный API-Интерфейс от System Center, Windows PowerShell или другого управляющего приложения с поддержкой сети.  
  
-   Вычисляет политику для распространения Мультиплексорами SLB и узлов Hyper-V.  
  
-   Предоставляет сведения о состоянии работоспособности инфраструктуры SLB.  
  
### <a name="slb-mux"></a>SLB/MUX  
SLB/MUX обрабатывает входящий сетевой трафик и сопоставляется частные интерфейсы виртуальных IP-адресов, а затем перенаправляет трафик на правильный DIP. Каждый Мультиплексора также использует BGP для публикации виртуальных IP-адресов маршруты пограничные маршрутизаторы. BGP поддерживать в активном состоянии уведомляет Мультиплексорами Мультиплексора ошибки, что позволяет active Мультиплексорами перераспределить нагрузку в случае сбоя Мультиплексора — по существу предоставляя балансировки нагрузки для подсистем балансировки нагрузки.  
  
### <a name="hosts-that-are-running-hyper-v"></a>Узлы, работающих под управлением Hyper-V  
SLB можно использовать с компьютеров, работающих под управлением Windows Server 2016 и Hyper-V. Виртуальные машины на узле Hyper-V можно запустить любой операционной системе, поддерживаемое Hyper-V.  
  
### <a name="slb-host-agent"></a>Агент узла SLB  
При развертывании SLB, необходимо использовать System Center, Windows PowerShell или другого управляющего приложения для развертывания SLB агент узла на каждом компьютере узла Hyper-V. Во всех версиях Windows Server 2016, которые обеспечивают поддержку Hyper-V, включая Nano Server можно установить агент узла SLB.  
  
Агент узла SLB ожидает передачи данных для обновления политики SLB из сетевого контроллера. Кроме того агент узла программы правила для подсистемы SLB в SDN с поддержкой Hyper-V виртуальные коммутаторы, которые настроены на локальном компьютере.  
  
### <a name="sdn-enabled-hyper-v-virtual-switch"></a>Виртуальный коммутатор Hyper-V включена SDN  
Для виртуального коммутатора совместимость с SLB необходимо использовать диспетчер виртуальных коммутаторов Hyper-V или Windows PowerShell команды для создания коммутатора и затем включить виртуальной платформы фильтрации (VFP) для виртуального коммутатора.  
  
Сведения о включении VFP на виртуальных коммутаторах см. в разделе команд Windows PowerShell [Get-VMSystemSwitchExtension](https://technet.microsoft.com/library/hh848603.aspx) и [Enable-VMSwitchExtension](https://technet.microsoft.com/library/hh848541.aspx?f=255&MSPPError=-2147217396).  
  
SDN включен виртуальный коммутатор Hyper-V выполняет следующие действия для SLB.  
  
-   Обрабатывает путь к данным для SLB.  
  
-   Получает входящий сетевой трафик от Мультиплексора.  
  
-   Обходит Мультиплексора для исходящего сетевого трафика, отправкой маршрутизатору, используя DSR.  
  
-   Запускается на экземплярах сервера Nano Server, Hyper-v.  
  
### <a name="bgp-enabled-router"></a>Маршрутизатор с поддержкой BGP  
Маршрутизатор BGP выполняет следующие действия для SLB.  
  
-   Маршруты входящий трафик с помощью ECMP Мультиплексора.  
  
-   Для исходящего сетевого трафика использует маршрут, предоставленный средой размещения.  
  
-   Принимает обновления маршрутов для виртуальных IP-адресов из SLB/MUX.  
  
-   Удаляет из ротации для SLB Мультиплексорами SLB, при сбое поддерживать в активном состоянии.  
  
## <a name="bkmk_features"></a>Функции балансировки нагрузки программного обеспечения  
Ниже приведены некоторые функции и возможности SLB.  
  
**Основные функциональные возможности**  
  
-   SLB предоставляет службы для «Север-Юг» и «Восток-Запад» TCP/UDP трафика балансировки нагрузки уровня 4  
  
-   Можно использовать подсистему балансировки Нагрузки на сеть на основе виртуализации сети Hyper-V  
  
-   SLB можно использовать с сетью на основе виртуальной ЛС для выделенного IP-адреса виртуальных машин, подключенных к SDN включен Hyper-V виртуальный коммутатор.  
  
-   Один экземпляр SLB может обрабатывать несколько клиентов  
  
-   Подсистема SLB и DIP-адрес поддержки масштабируемой и низкой задержкой обратный путь, реализованное с прямой ответ от сервера (DSR)  
  
-   Функции SLB, когда вы также используете коммутатор внедренных коммутаторов (SET) или виртуализацию ввода-вывода одного корнем (SR-IOV)  
  
-   Протокол IP версии 4 (IPv4) включает в себя SLB поддержки  
  
-   Для сценариев шлюза сайт сайт SLB предоставляет возможности NAT все подключения сеть сеть, использовать один общедоступный IP-адрес  
  
-   Можно установить SLB, включая полный агент узла и Мультиплексора, в Windows Server 2016 Core и установки Nano.  
  
**Масштаб и производительность**  
  
-   Готова для масштабирования в облаке, включая возможность горизонтального масштабирования и масштаб возможностей для Мультиплексорами и узлов агентов.  
  
-   Один активный модуль диспетчера SLB сетевого контроллера может поддерживать 8 экземпляров Мультиплексора  
  
**Высокий уровень доступности**  
  
-   Можно развернуть SLB более двух узлов активный/активный  
  
-   Мультиплексорами можно добавлять и удалять из пула Мультиплексора без влияния на службы SLB. Это позволяет сохранить доступность SLB при   
    отдельные Мультиплексорами являются вносятся исправления.  
  
-   Отдельные экземпляры Мультиплексора бесперебойная 99%  
  
-   Данные мониторинга работоспособности для управления сущностями  
  
**Выравнивание**  
  
-   Можно развернуть и настроить SLB с помощью SCVMM  
  
-   SLB предоставляет единую границу многопользовательских за счет интеграции с Microsoft устройства, такие как мультитенантный шлюз RAS, брандмауэр центра обработки данных и объектом, отражающим маршрут.  
  
