---
ms.assetid: 350aa5a3-5938-4921-93dc-289660f26bad
title: Новые возможности отказоустойчивой кластеризации в Windows Server
ms.prod: windows-server
ms.technology: storage-failover-clustering
ms.topic: get-started-article
manager: lizross
author: JasonGerend
ms.author: jgerend
ms.date: 10/18/2018
ms.openlocfilehash: 926c9c862d77c9fe082274a44af57e3b8339a655
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/01/2020
ms.locfileid: "82720496"
---
# <a name="whats-new-in-failover-clustering"></a>Что нового в отказоустойчивой кластеризации?

> Применяется к: Windows Server 2019, Windows Server 2016

В этом разделе объясняются новые и измененные функциональные возможности отказоустойчивой кластеризации для Windows Server 2019 и Windows Server 2016.

## <a name="whats-new-in-windows-server-2019"></a>Новые возможности Windows Server 2019

- **Наборы кластеров**

    Наборы кластеров позволяют увеличить количество серверов в одном решении (SDDC), определяемом программным обеспечением, за пределами текущих ограничений кластера. Это достигается путем группировки нескольких кластеров в набор кластеров — слабо связанное Группирование нескольких отказоустойчивых кластеров: вычислений, хранения и Hyper-схождения.
    С помощью наборов кластеров можно перемещать виртуальные машины (в режиме динамической миграции) между кластерами в наборе кластеров.

    Дополнительные сведения см. в разделе [кластерные наборы](../storage/storage-spaces/cluster-sets.md).

- **Кластеры с поддержкой Azure**
  
    Отказоустойчивые кластеры теперь автоматически обнаруживают, когда они работают в виртуальных машинах Azure IaaS, и оптимизируют конфигурацию, чтобы обеспечить профилактическую отработку отказа и ведение журнала событий запланированного обслуживания Azure для достижения наивысшего уровня доступности. Развертывание также упрощается за счет устранения необходимости в настройке подсистемы балансировки нагрузки с динамическим сетевым именем для имени кластера.

- **Миграция кластеров между доменами**

    Отказоустойчивые кластеры теперь могут динамически переноситься из одного домена Active Directory в другой, что упрощает консолидацию доменов и позволяет создавать кластеры с помощью партнеров по оборудованию и присоединять их к домену клиента позже.

- **Свидетель USB**

    Теперь можно использовать простой USB-накопитель, подключенный к сетевому коммутатору, в качестве следящего сервера при определении кворума для кластера. Это расширяет файловый ресурс-свидетель для поддержки любого устройства, совместимого с SMB2.

- **Улучшения инфраструктуры кластера**

    Кэш CSV теперь включен по умолчанию для повышения производительности виртуальной машины. MSDTC теперь поддерживает общие тома кластера, чтобы можно было проводить развертывание рабочих нагрузок MSDTC в локальных дисковых пространствах, например в SQL Server. Улучшенный алгоритм определения разделенных узлов с механизмом автоматического устранения неполадок с целью их обратного присоединения к кластеру. Улучшенное определение маршрута кластерной сети и автоматическое устранение неполадок.

- **Кластерное обновление поддерживает локальные дисковые пространства**

    В этом выпуске интегрирована функция кластерного обновления (CAU), которая учитывает локальные дисковые пространства, проверяя данные и обеспечивая завершение их повторной синхронизации на каждом угле. Обновление с поддержкой кластера проверяет обновления для интеллектуального перезапуска только при необходимости. Это позволяет управлять перезапусками всех серверов в кластере для планового обслуживания.

- **Улучшения файлового ресурса-свидетеля**

    Мы включили использование файлового ресурса-свидетеля в следующих сценариях:
  - Отсутствие или очень плохое подключение к Интернету из-за удаленного расположения, предотвращая использование облака-свидетеля.
  - Отсутствие общих дисков для диска-свидетеля. Это может быть Локальные дисковые пространства конфигурация гиперконвергентном, SQL Server Always On группы доступности (AG) или группа доступности * базы данных Exchange (DAG), ни один из которых не использует общие диски.
  - Отсутствие подключения к контроллеру домена из-за того, что кластер находится за демилитаризованной зоной.
  - В Рабочей группе или кластере между доменами, для которых отсутствует Active Directory объект имени кластера (CNO). Дополнительные сведения об этих усовершенствованиях см. в следующих публикациях в блогах по управлению сервером &: файловый ресурс отказоустойчивого кластера и DFS.

    Теперь можно явно заблокировать использование пространств имен DFS в качестве расположения. Добавление файлового ресурса-свидетеля в общую папку DFS может привести к проблемам с стабильностью кластера, и эта конфигурация никогда не поддерживалась. Мы добавили логику для определения того, использует ли общая папка пространства имен DFS, и если обнаружены пространства имен DFS, диспетчер отказоустойчивости кластеров блокирует создание следящего сервера и выводит сообщение об ошибке "не поддерживается".

- **Усиление защиты кластера**

    При обмене данными внутри кластера по протоколу Server Message Block (SMB) для общих томов кластера и локальных дисковых пространств теперь используются сертификаты с целью обеспечения высокого уровня безопасности платформы. Это позволяет отказоустойчивым кластерам работать без зависимостей от NTLM и использовать базовые параметры безопасности.

- **Отказоустойчивый кластер больше не использует аутентификацию NTLM**

    Отказоустойчивые кластеры больше не используют проверку подлинности NTLM. Вместо этого Kerberos и проверка подлинности на основе сертификата используются исключительно. Для использования этого улучшения безопасности не требуются изменения, необходимые пользователю или средствам развертывания. Это также позволяет развертывать отказоустойчивые кластеры в средах, где отключена NTLM.

## <a name="whats-new-in-windows-server-2016"></a>Новые возможности Windows Server 2016

### <a name="cluster-operating-system-rolling-upgrade"></a><a name="BKMK_RollingUpgrade"></a>Последовательное обновление ОС кластера

Последовательное обновление операционной системы кластера позволяет администратору обновить операционную систему узлов кластера с Windows Server 2012 R2 до более новой версии без остановки Hyper-V или масштабируемый файловый сервер рабочих нагрузок. Благодаря этой функции можно избежать штрафов за простои, которые полагаются согласно соглашениям об уровне обслуживания.

**Какой эффект дает это изменение?**  

Обновление кластера Hyper-V или масштабируемый файловый сервер с Windows Server 2012 R2 до Windows Server 2016 больше не требует простоя. Кластер продолжит работать на уровне Windows Server 2012 R2 до тех пор, пока все узлы в кластере не будут работать под Windows Server 2016. Функциональный уровень кластера обновляется до Windows Server 2016 с помощью командлет `Update-ClusterFunctionalLevel`Windows PowerShell.

> [!WARNING]  
> - После обновления функционального уровня кластера вы не сможете вернуться к функциональному уровню кластера Windows Server 2012 R2.
>
> - До запуска `Update-ClusterFunctionalLevel` командлета процесс будет отменен, и можно будет добавить узлы windows Server 2012 R2 и удалить узлы windows Server 2016.

**Что работает иначе?**  

Теперь можно легко обновить отказоустойчивый кластер Hyper-V или масштабируемый файловый сервер без простоя или создать новый кластер с узлами, работающими под управлением операционной системы Windows Server 2016. Миграция кластеров на Windows Server 2012 R2 включала в себя отключение существующего кластера и переустановка новой операционной системы для каждого узла, а затем подключение кластера к сети. Старый процесс был громоздким и требовал простоя. Однако в Windows Server 2016 кластеру не нужно переходить в автономный режим в любой момент.

Для каждого узла в кластере используются следующие операционные системы кластера:  
-   Узел приостановлен и остановлен на всех виртуальных машинах, на которых запущены службы. 
-   Виртуальные машины (или другие рабочие нагрузки кластера) переносятся на другой узел в кластере. 
-   Существующая операционная система удаляется, и выполняется чистая установка операционной системы Windows Server 2016 на узле. 
-   Узел, на котором запущена операционная система Windows Server 2016, добавляется обратно в кластер. 
-   На этом этапе кластер называется запуском в смешанном режиме, так как узлы кластера работают под управлением Windows Server 2012 R2 или Windows Server 2016. 
-   Функциональный уровень кластера остается в Windows Server 2012 R2. На этом функциональном уровне новые функции Windows Server 2016, которые влияют на совместимость с предыдущими версиями операционной системы, будут недоступны. 
-   Со временем все узлы обновляются до Windows Server 2016. 
-   После этого функциональный уровень кластера изменится на Windows Server 2016 с помощью командлета `Update-ClusterFunctionalLevel`Windows PowerShell. На этом этапе можно воспользоваться преимуществами функций Windows Server 2016. 

Дополнительные сведения см. в статье [последовательное обновление операционной системы кластера](cluster-operating-system-rolling-upgrade.md). 

### <a name="storage-replica"></a><a name="BKMK_SR"></a>Реплика хранилища  
Реплика хранилища — это новая функция, которая обеспечивает независимую от хранилища, синхронную репликацию между серверами или кластерами для аварийного восстановления, а также растяжение отказоустойчивого кластера между сайтами. Синхронная репликация позволяет зеркально отображать данные в физических расположениях с отказоустойчивыми томами, что полностью предотвращает потерю данных на уровне файловой системы. Асинхронная репликация позволяет использовать физические расположения за пределами города, но при этом вероятна потеря данных. 

**Какой эффект дает это изменение?**  

Реплика хранилища позволяет выполнять следующие действия.  

-   Предоставление решения по аварийному восстановлению данных от одного поставщика при запланированных и незапланированных сбоях критически важных приложений. 

-   Использование транспортного протокола SMB3 с доказанной надежностью, масштабируемостью и производительностью. 

-   Расширение отказоустойчивых кластеров Windows до городской сети. 

-   Используйте сквозное использование программного обеспечения Майкрософт для хранения и кластеризации, такие как Hyper-V, Реплика хранилища, дисковые пространства, кластер, масштабируемый файловый сервер, SMB3, дедупликация данных и ReFS/NTFS. 

-   Сокращение затрат и уменьшение сложности следующим образом:  

    -   Хранилище не зависит от оборудования, отсутствуют строгие требования к конфигурации хранилища (DAS или SAN). 

    -   Разрешается использовать стандартные технологии хранения и сетевых подключений. 

    -   Управление отдельными узлами и кластерами осуществляется в удобной графической среде с помощью диспетчера отказоустойчивости кластеров. 

    -   Функция включает в себя возможность создания комплексных крупномасштабных скриптов с помощью Windows PowerShell. 

-   Способствует сокращению времени простоев и повышению свойственной Windows надежности и производительности. 

-   Обеспечивает поддержку, диагностику и определение метрик производительности. 

Дополнительные сведения см. в статье [Storage Replica Overview](../storage/storage-replica/storage-replica-overview.md) (Обзор функций репликации хранилища). 

### <a name="cloud-witness"></a><a name="BKMK_CloudWitness"></a>Облако-свидетель

Облако-свидетель — это новый тип свидетеля кворума отказоустойчивого кластера в Windows Server 2016, который использует Microsoft Azure в качестве точки арбитража. Облако-свидетель, как любой другой свидетель кворума, получает голос и может участвовать в подсчете кворума. Вы можете настроить облако-свидетель в качестве свидетеля кворума с помощью мастера настройки кворума кластера. 

**Какой эффект дает это изменение?**  

Использование облака-свидетеля в качестве следящего сервера кворума отказоустойчивого кластера обеспечивает следующие преимущества.  

-   Использует Microsoft Azure и устраняет необходимость в третьем отдельном центре обработки данных. 

-   Использует стандартное общедоступное Microsoft Azureное хранилище BLOB-объектов, которое устраняет дополнительные затраты на обслуживание виртуальных машин, размещенных в общедоступном облаке. 

-   Ту же учетную запись служба хранилища Microsoft Azure можно использовать для нескольких кластеров (один файл большого двоичного объекта на кластер; уникальный идентификатор кластера используется как имя файла большого двоичного объекта). 

-   Обеспечивает очень низкие затраты на учетную запись хранения (очень малые данные, записываемые на файл большого двоичного объекта, файл большого двоичного объекта обновляется только один раз при изменении состояния узлов кластера). 

Дополнительные сведения см. [в статье Развертывание облака-свидетеля для отказоустойчивого кластера](deploy-cloud-witness.md). 

**Что работает иначе?**  

Это новая функция в Windows Server 2016. 

### <a name="virtual-machine-resiliency"></a><a name="BKMK_VMs"></a>Устойчивость виртуальной машины

**Устойчивость вычислений** Windows Server 2016 включает повышенную устойчивость вычислений виртуальных машин для уменьшения проблем связи между кластерами в кластере вычислений следующим образом. 

-   **Параметры устойчивости, доступные для виртуальных машин:**  Теперь можно настроить параметры устойчивости виртуальной машины, определяющие поведение виртуальных машин во время временных сбоев.  

    -   **Уровень устойчивости:** Помогает определить способ обработки временных сбоев. 

    -   **Период устойчивости:**  Помогает определить, как долго все виртуальные машины могут выполняться в изолированном виде. 

-   **Карантин неработоспособных узлов:** Неработоспособные узлы помещаются в карантин и больше не могут быть присоединены к кластеру. Это предотвращает негативное воздействие узлов неустойчивый на другие узлы и общий кластер. 

Дополнительные сведения о рабочем процессе и параметрах карантина для вычислений виртуальной машины, управляющих размещением узла в изоляции или помещении в карантин, см. [в разделе устойчивость вычислений виртуальной машины в Windows Server 2016](https://blogs.msdn.com/b/clustering/archive/2015/06/03/10619308.aspx). 

**Устойчивость хранилища** В Windows Server 2016 виртуальные машины более устойчивы к сбоям временного хранилища. Улучшенная устойчивость виртуальной машины помогает сохранить состояние сеанса виртуальной машины клиента в случае нарушения работы хранилища. Это достигается благодаря интеллектуальной и быстрой отклику виртуальной машины на проблемы инфраструктуры хранилища. 

Когда виртуальная машина отключается от базового хранилища, она приостанавливается и ожидает восстановления хранилища. При приостановке виртуальная машина продолжает работу в контексте приложений, запущенных в ней. При восстановлении подключения виртуальной машины к ее хранилищу виртуальная машина возвращается в состояние выполнения. В результате состояние сеанса компьютера клиента сохраняется при восстановлении. 

В Windows Server 2016 устойчивость хранилища виртуальной машины учитывается и оптимизирована для гостевых кластеров. 

### <a name="diagnostic-improvements-in-failover-clustering"></a><a name="BKMK_Diagnostics"></a>Улучшения диагностики в отказоустойчивой кластеризации

Для диагностики проблем с отказоустойчивыми кластерами Windows Server 2016 включает в себя следующее:  

- Некоторые улучшения в файлах журналов кластера (например, сведения о часовом поясе и журнале Диагностиквербосе) упрощают устранение неполадок отказоустойчивой кластеризации. Дополнительные сведения см. в [статье улучшения в устранении неполадок отказоустойчивого кластера Windows Server 2016 — журнал кластера](https://blogs.msdn.com/b/clustering/archive/2015/05/15/10614930.aspx). 

- Новый тип дампа **активного дампа памяти**, который фильтрует большинство страниц памяти, выделенных виртуальным машинам, и, таким образом, делает память. dmp намного меньше и проще в сохранении или копировании. Дополнительные сведения см. в [статье усовершенствования устранения неполадок отказоустойчивого кластера Windows Server 2016 — активный дамп](https://blogs.msdn.com/b/clustering/archive/2015/05/18/10615526.aspx). 

### <a name="site-aware-failover-clusters"></a><a name="BKMK_SiteAware"></a>Отказоустойчивые кластеры с поддержкой физического расположения

Windows Server 2016 включает отказоустойчивые кластеры, поддерживающие сайты, которые позволяют узлам группы в растянутых кластерах на основе их физического расположения (сайта). Служба поддержки сайта кластера расширяет операции с ключами в течение жизненного цикла кластера, например поведение при отработке отказа, политики размещения, пульс между узлами и поведение кворума. Дополнительные сведения см. [в статье отказоустойчивые кластеры, поддерживающие сайты в Windows Server 2016](https://blogs.msdn.com/b/clustering/archive/2015/08/19/10636304.aspx). 

### <a name="workgroup-and-multi-domain-clusters"></a><a name="BKMK_multidomainclusters"></a>Кластеры рабочей группы и кластеры с несколькими доменами

В Windows Server 2012 R2 и более ранних версиях кластер может быть создан только между узлами-членами, присоединенными к тому же домену. В Windows Server 2016 это ограничение снято, а также добавлена возможность создавать отказоустойчивый кластер без зависимостей от Active Directory. Теперь можно создавать отказоустойчивые кластеры в следующих конфигурациях:  

-   **Кластеры с одним доменом.** Кластеры со всеми узлами, присоединенными к одному и тому же домену. 

-   **Кластеры с несколькими доменами.** Кластеры с узлами, которые являются членами разных доменов. 

-   **Кластеры рабочих групп.** Кластеры с узлами, которые являются рядовыми серверами или рабочими группами (не присоединены к домену). 

Дополнительные сведения см. в статье о [кластерах Рабочей группы и нескольких доменов в Windows Server 2016](https://blogs.msdn.com/b/clustering/archive/2015/08/17/10635825.aspx) .

### <a name="virtual-machine-load-balancing"></a><a name="BKMK_VMLoadBalancing"></a>Балансировка нагрузки виртуальной машины  

Балансировка нагрузки виртуальной машины — это новая функция отказоустойчивой кластеризации, которая упрощает балансировку нагрузки виртуальных машин на узлах в кластере. Чрезмерно зафиксированные узлы идентифицируются на основе памяти виртуальной машины и загрузки ЦП на узле. Затем виртуальные машины перемещаются (динамически перенесены) с чрезмерно зафиксированного узла на узлы с доступной пропускной способностью (если применимо). Интенсивность балансировки может быть настроена для обеспечения оптимальной производительности и эффективности работы кластера. Балансировка нагрузки по умолчанию включена в предварительной технической версии Windows Server 2016. Однако балансировка нагрузки отключается при включении динамической оптимизации SCVMM. 

### <a name="virtual-machine-start-order"></a><a name="BKMK_VMStartOrder"></a>Порядок запуска виртуальных машин

Порядок запуска виртуальных машин — это новая функция отказоустойчивой кластеризации, которая вводит порядок запуска для виртуальных машин (и всех групп) в кластере. Теперь виртуальные машины можно группировать по уровням, а зависимости заказов можно создавать между разными уровнями. Это гарантирует, что наиболее важные виртуальные машины (например, контроллеры домена или виртуальные машины служебной программы) будут запущены первыми. Виртуальные машины не запускаются, пока не будут запущены виртуальные машины, на которых они имеют зависимость. 

### <a name="simplified-smb-multichannel-and-multi-nic-cluster-networks"></a><a name="BKMK_SMBMultiChannel"></a>Упрощенные сети с многоканальными и многосетевыми кластерами SMB

Сети отказоустойчивого кластера больше не ограничены одним сетевым интерфейсом на подсеть/сеть. Благодаря упрощенным сетям с многоканальным и многосетевым кластерам SMB конфигурация сети будет автоматически и каждый сетевой адаптер в подсети может использоваться для трафика кластера и рабочей нагрузки. Это улучшение позволяет клиентам максимально увеличить пропускную способность сети для Hyper-V, SQL Server экземпляра отказоустойчивого кластера и других рабочих нагрузок SMB. 

Дополнительные сведения см. в разделе [упрощенные сети с многоканальными и МНОГОсетевыми кластерами SMB](smb-multichannel.md).

## <a name="see-also"></a>См. также

* [Хранилище](../storage/storage.md)  
* [Новые возможности хранилища в Windows Server 2016](../storage/whats-new-in-storage.md)  
