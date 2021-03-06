---
title: Программный ЦОД Windows Server
Description: Обзор программного ЦОД Windows Server
ms.prod: windows-server
ms.technology: SDDC
ms.topic: get-started article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 06/04/2019
ms.localizationpriority: medium
ms.openlocfilehash: 5a90ad13a51a540c6c76adacb7df0225d642573a
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2020
ms.locfileid: "80857197"
---
# <a name="windows-server-software-defined-datacenter"></a>Программно-определяемый ЦОД Windows Server

>Область применения. Windows Server 2019, Windows Server 2016

![](media/sddc/heading.png)

## <a name="what-is-windows-server-software-defined-datacenter"></a>Что такое программный ЦОД Windows Server?

Программно-определяемый центр обработки данных (ЦОД) — распространенный отраслевой термин, который, как правило, обозначает центр обработки данных с полностью виртуализированой инфраструктурой. Виртуализация играет ключевую роль. Это означает, что оборудование и программное обеспечение в центре обработки данных выходят за рамки традиционного соотношения один к одному. За счет эмуляции оборудования с помощью гипервизора операционные системы и приложения можно абстрагировать от физического оборудования и умножить для объединения процессоров, памяти, устройств ввода-вывода и сетей в эластичные пулы ресурсов.
 
Реализация программного ЦОД корпорации Майкрософт состоит из технологий Windows Server, описываемых в этой статье. В ее основе лежит низкоуровневая оболочка Hyper-V, предоставляющая платформу виртуализации, на которой формируются сеть и хранилище. Технологии безопасности, разработанные для уникальных задач виртуализированной инфраструктуры, устраняют внутренние и внешние угрозы. Благодаря встроенной в Windows Server оболочке PowerShell в сочетании с [System Center](https://docs.microsoft.com/system-center/) и/или [Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview) можно программировать и автоматизировать подготовку, развертывание, настройку и управление.

Технологии в составе Windows Server и System Center являются основными компонентами программного ЦОД Windows Server. Но несмотря на то, что это виртуализированная платформа, в ее основе должно лежать соответствующее оборудование. Партнеры Майкрософт, участвующие в программах **Программные решения Windows Server** и **Решения Azure Stack HCI** помогут помочь вашей компании приобрести необходимое оборудование и ввести его в эксплуатацию в первый же день.

![](media/sddc/video.png) **[Посмотрите видео, чтобы узнать больше о программном ЦОД Майкрософт](https://mva.microsoft.com/training-courses/whats-new-in-windows-server-2016-16457?l=YcsJR6sXC_1006218965)**

![](media/sddc/poster-ico.png) **[Скачайте PDF-файл с этой страницей в формате плаката](https://github.com/MicrosoftDocs/windowsserverdocs/blob/master/WindowsServerDocs/media/sddc/sddc_poster_0801417_ANSI-E.pdf)**

![](media/sddc/spacer1.png)<a href="https://github.com/MicrosoftDocs/windowsserverdocs/blob/master/WindowsServerDocs//media/sddc/sddc_poster_0801417_ANSI-E.pdf"><img src="media/sddc/poster.png"></a>

## <a name="azure-stack-hci-solutions"></a>Решения Azure Stack HCI

Выбор оптимальной аппаратной инфраструктуры — одно из важнейших условий успешного создания программного ЦОД Windows Server. Именно поэтому мы заключили партнерское соглашение с 15 партнерами по созданию проверенных корпорацией Майкрософт проектов программного ЦОД и рекомендаций по развертыванию.

Партнеры Майкрософт предоставляют целый ряд решений, совместимых с Windows Server 2019 через программу Azure Stack HCI и Windows Server 2016 через программно-определяемый центр обработки данных на основе Windows Server, которая доставляет высокопроизводительную гиперконвергентную инфраструктуру хранилища и сети. Гиперконвергентные решения объединяют ресурсы вычислений, хранения и сети в соответствующих отраслевым стандартам серверах и компонентах для улучшенной аналитики и контроля в ЦОД.

![](media/sddc/learn.png) **[Дополнительные сведения о решениях Azure Stack HCI](https://azure.microsoft.com/overview/azure-stack/hci)**

![](media/sddc/learn.png) **[Дополнительные сведения о решениях WSSD](https://www.microsoft.com/cloud-platform/software-defined-datacenter)**

## <a name="windows-server-virtualized-technologies"></a>Виртуализированные технологии Windows Server ##

В оставшейся части этого раздела перечислены технологии программного ЦОД Windows Server и приведены ссылки на документацию по каждой из них. Технологии указаны в следующей таблице:

![](media/sddc/table.png)

![](media/sddc/virtualize.png)

### <a name="windows-server-hyper-converged"></a>Гиперконвергентное решение Windows Server

Технологии виртуализации Windows Server включают в себя обновления для Hyper-V, виртуального коммутатора Hyper-V, а также для защищенной структуры и экранированных виртуальных машин. Эти обновления повышают безопасность, масштабируемость и надежность. Благодаря обновлениям отказоустойчивой кластеризации, сетевых компонентов и хранилища эти технологии еще удобнее развертывать и администрировать при использовании в сочетании с Hyper-V.

![](media/sddc/spacer1.png)![](media/sddc/hyper-converged.png)

![](media/sddc/learn.png) **[Дополнительные сведения о гиперконвергентном решении Windows Server](https://docs.microsoft.com/windows-server/get-started/what-s-new-in-windows-server-2016#computevirtualizationvirtualizationmd)**

### <a name="hyper-v-hypervisor"></a>Низкоуровневая оболочка Hyper-V

Hyper-V — это технология виртуализации на основе гипервизора для Windows. Гипервизор ключевым компонентом технологии виртуализации. Это процессор-зависимая платформа виртуализации, позволяющая нескольким изолированным операционным системам использовать общую аппаратную платформу.

![](media/sddc/spacer1.png)![](media/sddc/hypervisor.png)

![](media/sddc/learn.png) **[Дополнительные сведения о низкоуровневой оболочке Hyper-V](https://www.microsoft.com/cloud-platform/server-virtualization)**

### <a name="guest-clustering-with-shared-vhdx"></a>Кластеризация гостевой системы с помощью общего диска VHDX

![](media/sddc/virtualize-line.png)

Общий диск VHDX отличается гибкостью и безопасностью, а также не привязан к топологии базового хранилища, поэтому он устраняет необходимость предоставлять физическое базовое хранилище для гостевой ОС. Новый общий диск VHDX поддерживает оперативное изменение размера.

![](media/sddc/spacer1.png)![](media/sddc/cluster.png)

- Общий диск VHDX может располагаться в общем томе кластера (CSV) в блочном хранилище или в файловом хранилище SMB.
- Защищено: Общий диск VHDX поддерживает реплику Hyper-V и резервное копирование на уровне узла.

![](media/sddc/learn.png) **[Дополнительные сведения о кластеризации гостевой системы с помощью общего диска VHDX](https://technet.microsoft.com/library/dn281956(v=ws.11).aspx)**

### <a name="hyper-v-replica"></a>Реплика Hyper-V

![](media/sddc/virtualize-line.png)

Встроенная программная репликация виртуальных машин в сети с использованием сертификатов. Отсутствие привязки к серверам, сетевому оборудованию или оборудованию для хранения данных на обеих сайтах.

![](media/sddc/spacer1.png)![](media/sddc/replica.png)

Отсутствие потребности в других технологиях репликации виртуальных машин и, как следствие, снижение расходов.
- Автоматическое выполнение динамической миграции.
- Удобство настройки и управления через диспетчер Hyper-V, PowerShell или Azure Site Recovery.

![](media/sddc/learn.png) **[Дополнительные сведения о реплике Hyper-V](https://docs.microsoft.com/windows-server/virtualization/hyper-v/manage/set-up-hyper-v-replica)**

![](media/sddc/networking.png)

### <a name="network-controller"></a>Сетевой контроллер

![](media/sddc/networking-line.png)

Централизованная программируемая точка автоматизации для управления, настройки, мониторинга, а также выявления и устранения неисправностей в виртуальной и физической сетевой инфраструктуре центра данных.

![](media/sddc/spacer1.png)![](media/sddc/netcontroller.png)

Администраторы используют средство управления, взаимодействующее напрямую с сетевым контроллером. Сетевой контроллер предоставляет средству управления сведения о сетевой инфраструктуре, включая виртуальную и физическую инфраструктуру.

![](media/sddc/learn.png) **[Дополнительные сведения о сетевом контроллере](https://docs.microsoft.com/windows-server/networking/sdn/technologies/network-controller/network-controller)**

### <a name="datacenter-firewall"></a>Брандмауэр центра обработки данных

![](media/sddc/networking-line.png)

Если этот компонент развернут и предоставляется как услуга, администраторы клиента могут установить и настроить политики брандмауэра, чтобы защитить виртуальные сети от нежелательного трафика из Интернета и интрасетей.

![](media/sddc/spacer1.png)![](media/sddc/firewall.png)

Администратор поставщика услуг или клиента может управлять политиками брандмауэра центра обработки данных через сетевой контроллер.

![](media/sddc/learn.png) **[Дополнительные сведения о брандмауэре центра обработки данных](https://docs.microsoft.com/windows-server/networking/sdn/technologies/network-function-virtualization/datacenter-firewall-overview)**

### <a name="switch-embedded-teaming"></a>Объединение внедренных коммутаторов

![](media/sddc/networking-line.png)

SET является альтернативным решением для объединения сетевых карт, которое можно использовать в средах с Hyper-V и стеком [программно-конфигурируемой сети (SDN)](https://docs.microsoft.com/windows-server/networking/sdn/software-defined-networking).

![](media/sddc/spacer1.png)![](media/sddc/teaming.png)

![](media/sddc/learn.png) **[Дополнительные сведения об объединении внедренных коммутаторов](https://docs.microsoft.com/windows-server/networking/sdn/technologies/set-for-sdn)**

### <a name="software-load-balancing"></a>Балансировка нагрузки программного обеспечения

![](media/sddc/networking-line.png)

SLB позволяет размещать одну и ту же рабочую нагрузку на нескольких серверах, что обеспечивает высокий уровень доступности и масштабирования. Возможности масштабируемой балансировки нагрузки с использованием виртуальных машин SLB на тех же серверах Hyper-V, что используются для других рабочих нагрузок виртуальных машин. SLB поддерживает быстрое создание и удаление конечных точек балансировки нагрузки для операций поставщиков облачных услуг. SLB поддерживает десятки гигабайтов на кластер, предоставляет простую модель подготовки, которая удобна в масштабировании.

![](media/sddc/spacer1.png)![](media/sddc/balancer.png)

![](media/sddc/learn.png) **[Дополнительные сведения о программной балансировке нагрузки](https://docs.microsoft.com/windows-server/networking/sdn/technologies/network-function-virtualization/software-load-balancing-for-sdn)**


![](media/sddc/storage.png)

### <a name="storage-spaces-direct"></a>Дисковые пространства прямого подключения

![](media/sddc/storage-line.png)

Локальные дисковые пространства используют стандартные серверы с локально подключенными дисками для создания программно-определяемого хранилища с высоким уровнем доступности и масштабируемости, причем стоимость такого хранилища значительно ниже стоимости традиционных массивов SAN или NAS. Архитектура такого хранилища существенно упрощает подготовку ресурсов и развертывание.

![На каждом узле есть локально подключенные диски, объединенные в пулы на уровне кластера с помощью локальных дисковых пространств. В дальнейшем виртуальные машины получают к ним доступ через общие тома кластера](media/sddc/spacer1.png)![](media/sddc/ssd.png).

Локальные дисковые пространства представляют новую шину Software Storage Bus, а также в них используется множество существующих возможностей Windows Server, таких как отказоустойчивая кластеризация, общие тома кластера (CSV), протокол SMB3 и, конечно, дисковые пространства.

![](media/sddc/learn.png) **[Дополнительные сведения о локальных дисковых пространствах](storage/storage-spaces/storage-spaces-direct-overview.md)**
### <a name="storage-quality-of-service"></a>Качество обслуживания хранилища ###

![](media/sddc/storage-line.png)

Централизованные отслеживание и контроль производительности хранилища виртуальных машин с помощью ролей Hyper-V и масштабируемого файлового сервера помогают обеспечить равномерное использование ресурсов хранилища между несколькими виртуальными машинами.

![](media/sddc/spacer1.png)![](media/sddc/qos.png)

Служба качества обслуживания хранилища встроена в программно-определяемое решение Майкрософт для хранения данных, предоставляемое масштабируемым файловым сервером и Hyper-V с использованием протокола SMB3. Новый диспетчер политик обеспечивает централизованный мониторинг производительности хранилища.

![](media/sddc/learn.png) **[Дополнительные сведения о качестве обслуживания хранилища](https://docs.microsoft.com/windows-server/storage/storage-qos/storage-qos-overview)**

### <a name="storage-replica"></a>Реплика хранилища


![](media/sddc/storage-line.png)

Аварийное восстановление и готовность к аварийным ситуациям помогают полностью исключить потери данных, а также позволяют организовать синхронную защиту данных, расположенных в разных стойках, на разных этажах, в разных зданиях, филиалах, городах и странах за счет более эффективного использования нескольких центров обработки данных.

![](media/sddc/spacer1.png)
![](media/sddc/storage-replica.png)

Синхронная репликация

1. Приложение записывает данные.
2. Данные журнала записываются и реплицируются на удаленный сайт.
3. Данные журнала записываются на удаленный сайт.
4. Подтверждение от удаленного сайта.
5. Подтверждение операции записи приложения.

t и t1. Данные записываются в том, для журналов применяется сквозная запись.

![](media/sddc/learn.png) **[Дополнительные сведения о реплике хранилища](https://docs.microsoft.com/windows-server/storage/storage-replica/storage-replica-overview)**

![](media/sddc/security.png)

### <a name="guarded-fabric"></a>Защищенная структура

![](media/sddc/security-line.png)

Поставщики облачных служб и администраторы корпоративного частного облака могут использовать защищенную структуру для создания более безопасной среды для виртуальных машин. Защищенная структура состоит из одной службы защиты узла (HGS), которая обычно представлена кластером из трех узлов, одним или несколькими защищенными узлами и набором экранированных виртуальных машин.

![](media/sddc/spacer1.png)![](media/sddc/guarded-fabric.png)

![](media/sddc/learn.png) **[Дополнительные сведения о защищенной структуре](https://docs.microsoft.com/windows-server/virtualization/guarded-fabric-shielded-vm/guarded-fabric-and-shielded-vms)**

### <a name="shielded-vms"></a>Экранированные виртуальные машины

![](media/sddc/security-line.png)

Данные и состояние экранированной виртуальной машины защищены от проверки, кражи и несанкционированных изменений со стороны как вредоносных программ, так и администраторов центра обработки данных.

![](media/sddc/spacer1.png)![](media/sddc/shielded.png)

- Экранированные виртуальные машины запускаются только в структурах, назначенных владельцами виртуальных машин.
- Экранированные виртуальные машины шифруются службой BitLocker или иным способом, чтобы их могли запускать только назначенные владельцы.
- Работающие виртуальные машины можно преобразовать в экранированные.

![](media/sddc/learn.png) **[Дополнительные сведения об экранированных виртуальных машинах](https://docs.microsoft.com/windows-server/virtualization/guarded-fabric-shielded-vm/guarded-fabric-and-shielded-vms)**

### <a name="host-guardian-service"></a>Служба защиты узла

![](media/sddc/security-line.png)

Служба защиты узла содержит ключи от допустимых структур, а также от зашифрованных виртуальных машин.

![](media/sddc/spacer1.png)![](media/sddc/guardian.png)

![](media/sddc/learn.png) **[Дополнительные сведения о службе защиты узла](https://docs.microsoft.com/windows-server/virtualization/guarded-fabric-shielded-vm/guarded-fabric-manage-hgs)**

### <a name="device-health-attestation"></a>Подтверждение работоспособности устройств

![](media/sddc/security-line.png)

Аттестация помогает повысить уровень корпоративной безопасности путем отслеживания и подтверждения защиты на аппаратном уровне без существенного роста эксплуатационных расходов.


![](media/sddc/spacer1.png)![](media/sddc/attestation.png)


Показанный выше доверенный режим оборудования обеспечивает наивысший уровень достоверности благодаря доверию на основе встроенного в оборудование модуля TPM версии 2.0 и соответствию политике целостности кода для выпуска ключей.


![](media/sddc/learn.png) **[Дополнительные сведения об аттестации работоспособности устройства](https://docs.microsoft.com/windows-server/security/device-health-attestation)**

![](media/sddc/management.png)

### <a name="powershell-desired-state-configuration"></a>PowerShell Desired State Configuration

![](media/sddc/management-line.png)

Windows PowerShell Desired State Configuration — это встроенная в Windows платформа управления конфигурациями, основанная на открытых стандартах. DSC отличается достаточной гибкостью для надежной, согласованной работы на каждом этапе жизненного цикла развертывания (разработка, тестирование, подготовка, производство), а также при масштабировании.

![](media/sddc/spacer1.png)![](media/sddc/dsc.png)

DSC поддерживает непрерывные развертывания, поэтому можно многократно развертывать конфигурации, ничего не нарушая.

-  Для ускорения развертывания в конфигурациях DSC применяются лишь те параметры, которые изменились по сравнению с исходным значением.
-  DSC можно использовать в локальной, общедоступной или частной облачной среде.
-  DSC можно интегрировать с любым решением Майкрософт или стороннего поставщика, если сохраняется возможность выполнения сценариев PowerShell в целевой системе.

![](media/sddc/learn.png) **[Дополнительные сведения о DSC PowerShell](https://docs.microsoft.com/powershell/dsc/overview)**


### <a name="system-center-vmm"></a>System Center VMM

![](media/sddc/management-line.png)

Диспетчер виртуальных машин входит в пакет System Center, который используется для настройки, администрирования и преобразования традиционных ЦОД с целью централизованного управления локальными средами, поставщиками услуг и облаком Azure.

![](media/sddc/spacer1.png)![](media/sddc/vmm.png)

- Центр обработки данных: настройка и администрирование компонентов ЦОД как единой структуры в VMM. 
- Узлы виртуализации: VMM позволяет добавлять, подготавливать к работе и управлять узлами и кластерами виртуализации Hyper-V и VMware.
- Сетевое взаимодействие: VMM обеспечивает виртуализацию сети, включая поддержку создания и администрирования виртуальных сетей и сетевых шлюзов. 
- Хранилище: VMM позволяет обнаруживать, классифицировать, подготавливать к работе, выделять и назначать локальные и удаленные хранилища.

![](media/sddc/learn.png) **[Дополнительные сведения о System Center VMM](https://docs.microsoft.com/system-center/vmm/)**

### <a name="windows-admin-center"></a>Windows Admin Center

![](media/sddc/management-line.png)

Windows Admin Center — это разворачиваемый в локальной среде набор браузерных средств управления, позволяющий администрировать локальную среду систем с Windows Server независимо от Azure или облака. Windows Admin Center предоставляет ИТ-администраторам полный контроль над всеми аспектами инфраструктуры Windows Server. Это решение особенно полезно для управления частными сетями, не подключенными к Интернету.

![](media/sddc/spacer1.png)![](media/sddc/architecture.png)

Публикация веб-сервера в DNS и настройка корпоративного брандмауэра помогут получить доступ к Windows Admin Center через Интернет, что позволит вам подключаться к вашим серверам и управлять ими из любого места с помощью Microsoft Edge или Google Chrome.

![](media/sddc/learn.png) **[Дополнительные сведения о Windows Admin Center](manage/windows-admin-center/overview.md)**
