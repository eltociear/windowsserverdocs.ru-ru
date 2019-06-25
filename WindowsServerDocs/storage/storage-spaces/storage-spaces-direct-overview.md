---
title: Обзор локальных дисковых пространств
ms.prod: windows-server-threshold
ms.author: cosdar
ms.manager: dongill
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 06/07/2019
ms.assetid: 8bd0d09a-0421-40a4-b752-40ecb5350ffd
description: Обзор дисковыми пространствами, в состав Windows Server, который позволяет кластера серверов с помощью внутреннего хранилища в программно определяемого хранилища решение.
ms.localizationpriority: medium
ms.openlocfilehash: 1ff63794de25565a9ade7eb4e8b66cf1e394c14a
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/07/2019
ms.locfileid: "66812698"
---
# <a name="storage-spaces-direct-overview"></a>Обзор локальных дисковых пространств

>Относится к: Windows Server 2019, Windows Server 2016

Локальные дисковые пространства используют стандартные серверы с локально подключенными дисками для создания программно-определяемого хранилища с высоким уровнем доступности и масштабируемости, причем стоимость такого хранилища значительно ниже стоимости традиционных массивов SAN или NAS. Его Конвергентная или гиперконвергентная архитектура существенно упрощает подготовку ресурсов и развертывание при возможности, такие как кэширование, уровни хранения и помехоустойчивое кодирование, поставлять с помощью последних аппаратных инноваций, таких как сети RDMA и диски NVMe, непревзойденную эффективность и производительность.

Дисковые пространства включается в 2019 Windows Server Datacenter, Windows Server 2016 Datacenter и [Windows Server Insider Preview Builds](https://insider.windows.com/for-business-getting-started-server/). 

Для других приложений, дисковых пространств, таких как кластеры общего SAS и автономными серверами, см. в разделе [обзор дисковых пространств](overview.md). Если вы ищете информацию об использовании дискового пространства на Компьютере с Windows 10, см. в разделе [дисковых пространств в Windows 10](https://support.microsoft.com/help/12438/windows-10-storage-spaces).

|       |       |
|   -   |   -   |
| **Понять**<br><ul><li>Обзор (вы здесь)</li><li>[Общие сведения о кэше](understand-the-cache.md)</li><li>[Отказоустойчивость и эффективность хранения](storage-spaces-fault-tolerance.md)<li>[Рекомендации по симметрии диска](drive-symmetry-considerations.md)</li><li>[Принцип работы и отслеживание повторной синхронизации хранилища](understand-storage-resync.md)</li><li>[Общие сведения о кворуме кластеров и пулов](understand-quorum.md)</li><li>[Наборы кластеров](cluster-sets.md)</li> | **План**<br><ul><li>[Требования к оборудованию](storage-spaces-direct-hardware-requirements.md)</li><li>[Использование кэша чтения в памяти CSV](csv-cache.md)</li><li>[Выбор дисков](choosing-drives.md)</li><li>[Планирование томов](plan-volumes.md)</li><li>[Использование кластеров гостевых виртуальных машин](storage-spaces-direct-in-vm.md)</li><li>[Аварийное восстановление](storage-spaces-direct-disaster-recovery.md)</li> |
| **Развертывание**<br><ul><li>[Развертывание локальных дисковых пространств](deploy-storage-spaces-direct.md)</li><li>[Создание томов](create-volumes.md)</li><li>[Вложенная устойчивость](nested-resiliency.md)</li><li>[Настройка кворума](../../failover-clustering/manage-cluster-quorum.md)</li><li>[Обновление кластера Локальных дисковых пространств в Windows Server 2019](upgrade-storage-spaces-direct-to-windows-server-2019.md)</li> | **Управление**<br><ul><li>[Управление с помощью Windows Admin Center](../../manage/windows-admin-center/use/manage-hyper-converged.md)</li><li>[Добавление серверов или дисков](add-nodes.md)</li><li>[Перевод сервера в автономный режим для обслуживания](maintain-servers.md)</li><li>[Удаление серверов](remove-servers.md)</li><li>[Увеличение размеров томов](resize-volumes.md)</li><li>[Удаление томов](delete-volumes.md)</li><li>[Обновление встроенного ПО дисков](../update-firmware.md)</li><li>[Журнал производительности](performance-history.md)</li><li>[Разграничение выделения томов](delimit-volume-allocation.md)</li><li>[Используйте Azure Monitor в гиперконвергированный кластер](configure-azure-monitor.md)</li> |
| **Устранение неполадок**<br><ul><li>[Устранение неполадок работоспособности и состояния работоспособности](storage-spaces-states.md)</li><li>[Сбор диагностических данных с дисковыми пространствами](data-collection.md)</li> | **Последние сообщения в блоге**<br><ul><li>[13.7 миллиона операций ввода-ВЫВОДА, с дисковыми пространствами: новой записи отрасли для гиперконвергентной инфраструктуры](https://blogs.technet.microsoft.com/filecab/2018/10/30/windows-server-2019-and-intel-optane-dc-persistent-memory/)</li><li>[Гиперконвергентной инфраструктуры, в Windows Server 2019 — обратный отсчет начинается с момента сейчас!](https://blogs.technet.microsoft.com/filecab/2018/10/02/hci-the-countdown-clock-starts-now/)</li><li>[Пять больших объявления от Windows Server Summit](https://blogs.technet.microsoft.com/filecab/2018/06/27/windows-server-summit-recap)</li><li>[10 000 кластерами дисковых и инвентаризации...](https://blogs.technet.microsoft.com/filecab/2018/03/27/storage-spaces-direct-momentum/)</li> |

## <a name="videos"></a>Видео

**Краткий обзор видео (5 минут)**

> [!Video https://www.youtube-nocookie.com/embed/raeUiNtMk0E]

**Дисковыми пространствами на Microsoft Ignite 2018 (1 час)**

> [!Video https://www.youtube-nocookie.com/embed/5kaUiW3qo30]

**Дисковыми пространствами Microsoft Ignite 2017 (1 час)**

> [!Video https://www.youtube-nocookie.com/embed/YDr2sqNB-3c]

**Запуск события на конференции Microsoft Ignite 2016 (1 час)**

> [!Video https://www.youtube-nocookie.com/embed/LK2ViRGbWs]

## <a name="key-benefits"></a>Основные преимущества

|       |       |
|   -   |   -   |
| ![Простота](media/storage-spaces-direct-in-windows-server-2016/simplicity-icon.png)   | **Простота.** Создать кластер локальных дисковых пространств на основе стандартных серверов с ОС Windows Server 2016 можно меньше чем за 15 минут. Пользователи System Center могут выполнить развертывание, установив один флажок.       |
| ![Непревзойденная производительность](media/storage-spaces-direct-in-windows-server-2016/performance-icon.png)   | **Непревзойденная производительность.** Как при использовании только флэш-памяти, так и при использовании гибридных носителей локальные дисковые пространства позволяют обеспечить [скорость ввода-вывода более 150 000 операций в секунду в смешанном режиме и более 4000 операций в секунду в произвольном режиме на сервер](https://blogs.technet.microsoft.com/filecab/2016/07/26/storage-iops-update-with-storage-spaces-direct/) со стабильно низкой задержкой. Это достигается благодаря архитектуре со встроенной низкоуровневой оболочкой, встроенному кэшу чтения и записи и поддержке передовых дисков NVMe, подключаемых непосредственно к шине PCIe.      |
| ![Устойчивость к сбоям](media/storage-spaces-direct-in-windows-server-2016/fault-tolerance-icon.png)   | **Устойчивость к сбоям.** Встроенные средства отказоустойчивости обрабатывают сбои дисков, серверов или компонентов, обеспечивая непрерывную доступность. В более масштабных развертываниях можно также настроить [отказоустойчивость шасси и стоек](../../failover-clustering/fault-domains.md). При сбое оборудования просто отключите его: программное обеспечение восстановит работоспособность самостоятельно, без выполнения сложных действий по управлению.       |
| ![Эффективность работы с ресурсами](media/storage-spaces-direct-in-windows-server-2016/efficiency-icon.png)   | **Эффективность использования ресурсов.** Помехоустойчивое кодирование повышает экономичность хранения в 2,4 раза, а уникальные инновации, такие как локальные коды реконструкции и уровни ReFS в режиме реального времени, позволяют распространить эти преимущества на жесткие диски и смешанные (холодные и горячие) рабочие нагрузки. При этом снижается загрузка ЦП, и ресурсы высвобождаются для наиболее важной задачи — выполнения виртуальных машин.       |
| ![Управляемость](media/storage-spaces-direct-in-windows-server-2016/manageability-icon.png)   | **Управляемость**. Используйте [средства управления качеством обслуживания хранилища](../storage-qos/storage-qos-overview.md), чтобы контролировать работу наиболее загруженных виртуальных машин с помощью минимальных и максимальных значений скорости ввода-вывода на виртуальную машину. [Служба работоспособности](../../failover-clustering/health-service-overview.md) предоставляет встроенные возможности непрерывного мониторинга и оповещения, а новые интерфейсы API позволяют легко собирать расширенные метрики производительности и емкости в масштабе всего кластера.      |
| ![Масштабируемость](media/storage-spaces-direct-in-windows-server-2016/scalability-icon.png)   | **Масштабируемость**. Поддерживается масштабирование до 16 серверов и более чем 400 дисков, что позволяет получать объем хранилища в 1 петабайт (1000 терабайт) на кластер. Чтобы осуществить масштабирование, просто добавьте диски или серверы. Локальные дисковые пространства автоматически подключат новые диски и начнут использовать их. Эффективность и производительность хранилища повышают предсказуемость при масштабировании.       |

## <a name="deployment-options"></a>Варианты развертывания

Локальные дисковые пространства предусматривают два разных варианта развертывания:

### <a name="converged"></a>конвергентное;

**Хранилище и вычислительные ресурсы в отдельные кластеры.** При конвергентном развертывании, также известном как дезагрегированное, масштабируемый файловый сервер (SoFS) размещается поверх локальных дисковых пространств для предоставления подключенного к сети хранилища посредством общих папок SMB3. Это позволяет масштабировать вычислительные ресурсы и рабочие нагрузки независимо от кластера хранилища, особенно в масштабных развертываниях, например Hyper-V IaaS (инфраструктура как услуга), для поставщиков услуг и крупных предприятий.

![Дисковые пространства прямого подключения обслуживают хранилище с помощью функции масштабирования файлового сервера в виртуальные машины Hyper-V на другом сервере или кластере](media/storage-spaces-direct-in-windows-server-2016/converged-minimal.png)

### <a name="hyper-converged"></a>Гиперконвергентные

**Один кластер для вычислений и хранения.** При гиперконвергентном развертывании виртуальные машины Hyper-V или базы данных SQL Server работают непосредственно на серверах, предоставляющих хранилище, и сохраняют файлы в локальных томах. Это устраняет необходимость в настройке доступа к файловым серверам и разрешений. Кроме того, снижается стоимость оборудования при развертывании на малых и средних предприятиях, а также в удаленных офисах и филиалах. См. в разделе [развертывание локальных дисковых](deploy-storage-spaces-direct.md).

![Дисковые пространства прямого подключения обслуживают хранилище в виртуальных машинах Hyper-V на одном и том же кластере](media/storage-spaces-direct-in-windows-server-2016/hyper-converged-minimal.png)

## <a name="how-it-works"></a>Принцип работы

Локальные дисковые пространства являются развитием дисковых пространств, впервые представленных в Windows Server 2012. В них используется множество существующих возможностей Windows Server, таких как отказоустойчивая кластеризация, файловая система CSV, протокол SMB3 и, конечно, дисковые пространства. В них также были реализованы новые технологии, в первую очередь шина Software Storage Bus.

Ниже представлен обзор стека локальных дисковых пространств.

![Стек локальных дисковых пространств](media/storage-spaces-direct-in-windows-server-2016/converged-full-stack.png)

**Сетевое оборудование.** Для обмена данными между серверами локальные дисковые пространства используют протокол SMB3, включая SMB Direct и SMB Multichannel, работающий через Ethernet. Мы настоятельно рекомендуем использовать Ethernet со скоростью передачи данных более 10 Гбит/с и удаленным доступом к памяти (RDMA) — iWARP или RoCE.

**Оборудование для хранения.** От 2 до 16 серверов с локально подключенными дисками SATA, SAS или NVMe. Каждый сервер должен иметь по крайней мере 2 твердотельных накопителя и 4 дополнительных диска. Устройства SATA и SAS должны располагаться за адаптером шины (HBA) и расширителем SAS. Мы настоятельно рекомендуем использовать тщательно спроектированные и протестированные платформы от наших партнеров (ожидаются в ближайшее время).

**Отказоустойчивая кластеризация.** Встроенная функция кластеризации Windows Server используется для подключения серверов.

**Шина Software Storage Bus.** Шина Software Storage Bus — это новая технология, представленная в локальных дисковых пространствах. Она охватывает весь кластер и создает программно-определяемую структуру хранения, в которой каждый сервер имеет доступ к локальным дискам любого другого сервера. Это можно рассматривать как замену дорогостоящим и ограниченным в своих возможностях подключениям Fibre Channel или Shared SAS.

**Кэш уровня шины хранилища.** Шина Software Storage Bus динамически связывает самые быстрые диски присутствует (например, SSD) с более медленными дисками (например, жесткими дисками) для обеспечения кэширования на сервере чтения и записи, ускоряет операции ввода-ВЫВОДА и повысить пропускную способность.

**Пул носителей.** Набор дисков, которые образуют основу для дисковых пространств, называется пулом носителей. Он создается автоматически, и все подходящие диски обнаруживаются и добавляются в него также автоматически. Мы настоятельно рекомендуем использовать один пул носителей в каждом кластере с параметрами по умолчанию. Прочитайте раздел [Глубокое погружение в пул носителей](https://blogs.technet.microsoft.com/filecab/2016/11/21/deep-dive-pool-in-spaces-direct/), чтобы узнать больше.

**Дисковые пространства.** Дисковые пространства обеспечивают отказоустойчивость виртуальных накопителей с помощью [зеркалирования, помехоустойчивого кодирования или обеих этих технологий](storage-spaces-fault-tolerance.md). Их можно представить как распределенный программно-определяемый массив RAID на основе дисков в пуле. В локальных дисковых пространствах виртуальные диски обычно устойчивы к одновременному сбою двух дисков или серверов (то есть применяется трехстороннее зеркалирование, при котором каждая копия данных размещается на отдельном сервере), хотя также доступна отказоустойчивость на уровне шасси или стоек.

**Восстанавливаемая файловая система (ReFS).** ReFS — это файловая система с превосходными возможностями, предназначенная специально для виртуализации. Она позволяет существенно ускорить операции с файлами VHDX, такие как создание, расширение и объединение контрольных точек, а также имеет встроенные средства проверки контрольной суммы для обнаружения и исправления ошибок на уровне отдельных битов. В ней также реализовано переключение уровней в режиме реального времени, позволяющее переносить данные между "активными" и "пассивными" уровнями хранения в режиме реального времени в соответствии с интенсивностью использования.

**Общие тома кластера.** Файловая система CSV объединяет все тома ReFS в единое пространство имен, доступное с любого сервера, так что для каждого сервера все тома представляются как локально подключенные.

**Масштабируемый файловый сервер.** Этот последний уровень необходим только в конвергентных развертываниях. Он обеспечивает удаленный доступ к файлам со стороны клиентов, например другого кластера Hyper-V, через сеть по протоколу SMB3. Таким образом локальные дисковые пространства по сути превращаются в подключенное к сети хранилище (NAS).

## <a name="customer-stories"></a>Истории клиентов

Существуют [более 10 000 кластеров](https://blogs.technet.microsoft.com/filecab/2018/03/27/storage-spaces-direct-momentum/) по всему миру дисковых. Организаций любых размеров — от малых предприятий, развертывание только двумя узлами для крупных предприятий и государственные учреждения, развертывание сотнями узлов, зависят от дисковых пространств для своих критически важных приложений и инфраструктуры.

Посетите [Microsoft.com/HCI](https://www.microsoft.com/hci) читать их истории:

[![Сетка логотипы клиентов](media/storage-spaces-direct-in-windows-server-2016/customer-stories.png)](https://www.microsoft.com/hci)

## <a name="management-tools"></a>Средства управления

Управление и/или отслеживания дисковыми пространствами можно использовать следующие средства:

| Имя | Графическое или командной строки? | Платная или включен? |
|-----------------|----------------------------|-------------------|
| [Windows Admin Center](../../manage/windows-admin-center/overview.md)     | Графический    | Включено |
| Диспетчер серверов и Диспетчер отказоустойчивости кластеров                                 | Графический    | Включено |
| Windows PowerShell                                                        | Командная строка | Включено |
| [System Center Virtual Machine Manager (SCVMM)](https://technet.microsoft.com/system-center-docs/vmm/manage/manage-storage-spaces-direct-vmm) <br>& [Operations Manager (SCOM)](https://www.microsoft.com/download/details.aspx?id=54700) | Графический    | Платная     |

## <a name="get-started"></a>Начало работы

Попробуйте локальные дисковые пространства [в Microsoft Azure](https://blogs.technet.microsoft.com/filecab/2016/05/05/s2dazuretp5/) или скачайте [ознакомительную версию Windows Server](https://go.microsoft.com/fwlink/?linkid=842602) с лицензией на 180 дней.

## <a name="see-also"></a>См. также

- [Отказоустойчивость и эффективность хранения](storage-spaces-fault-tolerance.md)
- [Реплика хранилища](../storage-replica/storage-replica-overview.md)
- [Хранилище в блоге Майкрософт](https://blogs.technet.microsoft.com/filecab/)
- [Пропускная способность дисковых пространств прямого подключения с iWARP](https://blogs.technet.microsoft.com/filecab/2017/03/13/storage-spaces-direct-throughput-with-iwarp) (блог TechNet)
- [Новые возможности отказоустойчивой кластеризации в Windows Server](../../failover-clustering/whats-new-in-failover-clustering.md)  
- [Качество обслуживания хранилища](../storage-qos/storage-qos-overview.md)
- [Windows ИТ-специалистов поддержки](https://www.microsoft.com/itpro/windows/support)