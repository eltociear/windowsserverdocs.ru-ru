---
ms.assetid: 350aa5a3-5938-4921-93dc-289660f26bad
title: Новые возможности отказоустойчивой кластеризации в Windows Server
ms.prod: windows-server-threshold
ms.technology: storage-failover-clustering
ms.topic: get-started-article
manager: dongill
author: JasonGerend
ms.author: jgerend
ms.date: 10/18/2018
ms.openlocfilehash: 330f65721fca1908ac54ddfd194f96ffe540f1b5
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/31/2019
ms.locfileid: "66442359"
---
# <a name="whats-new-in-failover-clustering"></a>Что нового в отказоустойчивой кластеризации?

> Относится к: Windows Server 2019, Windows Server 2016

В этом разделе приводятся сведения о новых и измененных функциях отказоустойчивого кластера для Windows Server 2019 г. и Windows Server 2016.

## <a name="whats-new-in-windows-server-2019"></a>Новые возможности в Windows Server 2019

- **Наборы кластеров**

    Наборы кластера позволяют увеличить количество серверов в решении одного программно определяемого центра обработки данных (SDDC) превышает ограничение по текущего кластера. Это достигается путем группирования нескольких кластеров в набор кластера — это слабо связанная группа несколькими отказоустойчивыми кластерами: вычисления, хранение и гиперконвергентную.
    При использовании наборов кластера можно перемещать виртуальные машины в Интернете (Динамическая миграция) между кластерами в кластере необходимо установить.

    Дополнительные сведения см. в разделе [кластера наборы](../storage/storage-spaces/cluster-sets.md).

- **Azure с поддержкой кластеров**

    Отказоустойчивые кластеры теперь автоматически определять, когда они используются в виртуальных машинах Azure IaaS и оптимизации конфигурации для обеспечения упреждающую отработку отказа и ведение журнала событий плановое обслуживание Azure для достижения высочайшего уровня доступности. Кроме того упрощена процедура развертывания, избавляя от необходимости настроить подсистему балансировки нагрузки с помощью динамического сетевое имя для имени кластера.

- **Миграция кластера между доменами**

    Отказоустойчивые кластеры можно теперь динамически перемещать из одного домена Active Directory в другой, упрощение объединения доменов и позволяя кластеры, чтобы быть сведены в домен клиента, созданные партнерами оборудования.
- **Следящий сервер USB**

    Теперь можно использовать простой USB-устройства, подключенные к сетевому коммутатору следящего в определении кворума для кластера. При этом расширяется файлового ресурса-свидетеля для поддержки любого SMB2-совместимые устройства.

- **Усовершенствования инфраструктуры кластера**

    Кэш CSV теперь включена по умолчанию для повышения производительности виртуальной машины. MSDTC теперь поддерживает общие тома кластера, чтобы можно было проводить развертывание рабочих нагрузок MSDTC в локальных дисковых пространствах, например в SQL Server. Улучшенный алгоритм определения разделенных узлов с механизмом автоматического устранения неполадок с целью их обратного присоединения к кластеру. Улучшенное определение маршрута кластерной сети и автоматическое устранение неполадок.

- **Кластерного обновления поддерживает дисковыми пространствами**

    В этом выпуске интегрирована функция кластерного обновления (CAU), которая учитывает локальные дисковые пространства, проверяя данные и обеспечивая завершение их повторной синхронизации на каждом угле. Кластерного обновления проверяет обновления интеллектуально перезапустить только при необходимости. Это позволяет процессами перезагрузки всех серверов в кластере для выполнения планового обслуживания.

- **Файл усовершенствования следящий сервер общий ресурс** мы включили использование файлового ресурса-свидетеля в следующих сценариях: 
  - Отсутствует или очень низкой доступ к Интернету из-за удаленного расположения, отказ от использования облака-свидетеля. 
  - Отсутствие общих дисков для диска-свидетеля. Это может быть дисковых конфигурации гиперконвергентного, всегда на доступности группы (групп Доступности SQL Server), или * Exchange базы данных группы доступности (DAG), ни один из которых использовать общие диски. 
  - Отсутствие подключения к контроллеру домена из-за кластера выполняется за сети Периметра. 
  - Рабочей группе или между доменами кластер для которого существует — нет Active Directory объект имени кластера (CNO). Дополнительные сведения об этих улучшениях в следующей записи в блоги по управлению & сервера: Отказоустойчивый кластер файлового ресурса-свидетеля и DFS.
    
    Мы также явно блокировать использование пространств имен DFS общего файлового ресурса в качестве расположения. Добавление файлового ресурса-свидетеля для DFS общего ресурса может вызвать проблемы с надежностью для кластера, а эта конфигурация не поддерживается. Мы добавили логику обнаружения, если папка использует пространства имен DFS и пространств имен DFS в случае обнаружения Диспетчер отказоустойчивости кластеров блокирует создание следящего сервера и отображает сообщение об ошибке о не поддерживается.
- **Усиление безопасности кластера**

    При обмене данными внутри кластера по протоколу Server Message Block (SMB) для общих томов кластера и локальных дисковых пространств теперь используются сертификаты с целью обеспечения высокого уровня безопасности платформы. Это позволяет отказоустойчивым кластерам работать без зависимостей от NTLM и использовать базовые параметры безопасности.
- **Отказоустойчивый кластер больше не использует проверку подлинности NTLM**

    Отказоустойчивые кластеры больше не использовать проверку подлинности NTLM. Вместо этого Kerberos и проверки подлинности на основе сертификата используется исключительно. Нет изменений требуется пользователем, или средства развертывания, чтобы воспользоваться преимуществами этого улучшения безопасности. Он также позволяет отказоустойчивые кластеры для развертывания в средах, где был отключен NTLM. 


## <a name="whats-new-in-windows-server-2016"></a>Новые возможности в Windows Server 2016

### <a name="BKMK_RollingUpgrade"></a>Последовательное обновление ОС кластера

Последовательное обновление кластера операционной системы позволяет администратору обновлять ОС узлов кластера с Windows Server 2012 R2 до более новой версии не останавливая рабочие нагрузки Scale-Out File Server или Hyper-V. Благодаря этой функции можно избежать штрафов за простои, которые полагаются согласно соглашениям об уровне обслуживания. 

**Какой эффект дает это изменение?**  

Обновление Hyper-V или масштабируемого файлового сервера кластера Windows Server 2012 R2 до Windows Server 2016 больше не приводит к простою. Кластер будет продолжать работать на уровне Windows Server 2012 R2, пока все узлы в кластере работают под управлением Windows Server 2016. Функциональный уровень кластера обновляется до Windows Server 2016 с помощью Windows PowerShell командлет `Update-ClusterFunctionalLevel`. 

> [!WARNING]  
> -   После обновления режима работы кластера, вы не сможете перейти обратно функциональный уровень кластера Windows Server 2012 R2. 
> -   Пока `Update-ClusterFunctionalLevel` выполнения командлета, процесс является обратным и можно добавлять узлы Windows Server 2012 R2 и узлы Windows Server 2016 могут быть удалены. 

**Что работает иначе?**  

Отказоустойчивый кластер Hyper-V или масштабируемого файлового сервера можно теперь легко обновить без простоев, или нужно создать новый кластер с узлами, работающих под управлением операционной системы Windows Server 2016. Перенос кластеров Windows Server 2012 R2 участвует перевода существующего кластера в автономный режим и повторной установки новой операционной системы для каждого из узлов, а затем перерыва в работе кластера обратно в оперативный режим. Старый процесс была громоздкой и требуется время простоя. Тем не менее в Windows Server 2016, кластер не нужно перейти в автономный режим, в любой момент. 

Ниже приведены операционных систем кластера к обновлению на этапах для каждого узла в кластере.  
-   Узел приостановлен и всех виртуальных машин, которые запущены на нем останавливаются. 
-   Виртуальные машины (или другой рабочей нагрузки кластера), переносятся на другой узел в кластере. 
-   Существующая операционная система будет удален, и выполнить чистую установку операционной системы Windows Server 2016 на узле. 
-   Под управлением операционной системы Windows Server 2016 узел добавляется обратно в кластер. 
-   На этом этапе кластер называется работать в смешанном режиме, так как узлов под управлением Windows Server 2012 R2 или Windows Server 2016. 
-   Функциональный уровень кластера остается в Windows Server 2012 R2. В этот режим работы невозможна новые возможности в Windows Server 2016, влияющие на совместимость с предыдущими версиями операционной системы. 
-   В конечном счете все узлы будут обновлены до Windows Server 2016. 
-   Функциональный уровень кластера, то изменить на Windows Server 2016 с помощью командлета Windows PowerShell `Update-ClusterFunctionalLevel`. На этом этапе можно воспользоваться преимуществами функций Windows Server 2016. 

Дополнительные сведения см. в разделе [последовательного обновления кластерной ОС](cluster-operating-system-rolling-upgrade.md). 

### <a name="BKMK_SR"></a>Реплика хранилища  
Реплика хранилища — это новая функция, которая позволяет независимую от хранилища, блочные синхронную репликацию между серверами или кластерами для аварийного восстановления, а также растягивать отказоустойчивый кластер, между сайтами. Синхронная репликация позволяет зеркально отображать данные в физических расположениях с отказоустойчивыми томами, что полностью предотвращает потерю данных на уровне файловой системы. Асинхронная репликация позволяет использовать физические расположения за пределами города, но при этом вероятна потеря данных. 

**Какой эффект дает это изменение?**  

Реплика хранилища позволяет выполнять следующее:  

-   Предоставление решения по аварийному восстановлению данных от одного поставщика при запланированных и незапланированных сбоях критически важных приложений. 

-   Использование транспортного протокола SMB3 с доказанной надежностью, масштабируемостью и производительностью. 

-   Расширение отказоустойчивых кластеров Windows до городской сети. 

-   Использование программного обеспечения Microsoft сквозного для хранения и кластеризации, таких как Hyper-V, реплики хранилища, дисковых пространств, кластера, масштабируемого файлового сервера, SMB3, дедупликации и ReFS/NTFS. 

-   Сокращение затрат и уменьшение сложности следующим образом:  

    -   Хранилище не зависит от оборудования, отсутствуют строгие требования к конфигурации хранилища (DAS или SAN). 

    -   Разрешается использовать стандартные технологии хранения и сетевых подключений. 

    -   Управление отдельными узлами и кластерами осуществляется в удобной графической среде с помощью диспетчера отказоустойчивости кластеров. 

    -   Функция включает в себя возможность создания комплексных крупномасштабных скриптов с помощью Windows PowerShell. 

-   Способствует сокращению времени простоев и повышению свойственной Windows надежности и производительности. 

-   Обеспечивает поддержку, диагностику и определение метрик производительности. 

Дополнительные сведения см. в разделе [Реплика хранилища в Windows Server 2016](../storage/storage-replica/storage-replica-overview.md). 


### <a name="BKMK_CloudWitness"></a>Облако-свидетель  
Облако-свидетель — это новый тип свидетеля кворума отказоустойчивого кластера в Windows Server 2016, который использует Microsoft Azure в качестве точки арбитража. Облако-свидетель, как любой другой свидетель кворума, получает голос и может участвовать в подсчете кворума. Вы можете настроить облако-свидетель в качестве свидетеля кворума с помощью мастера настройки кворума кластера. 

**Какой эффект дает это изменение?**  

С помощью облака-свидетеля в качестве отказоустойчивого кластера свидетеля кворума обеспечивает следующие преимущества:  

-   Использует Microsoft Azure и устраняет необходимость в третьем отдельном центре данных. 

-   Использует стандартные общедоступные Microsoft Azure Blob Storage тем самым устраняет лишние дополнительной нагрузки от виртуальных машин, размещенных в общедоступном облаке. 

-   Одной учетной записи хранения Microsoft Azure можно использовать для нескольких кластеров (файл одного большого двоичного объекта для каждого кластера; уникальный идентификатор кластера используется в качестве имени файла BLOB-объектов). 

-   Предоставляет очень низкой стоимости выполняющуюся в учетную запись хранения (очень мало данные, записанные на файл большого двоичного объекта обновлен файл большого двоичного объекта только в том случае, когда при изменении состояния узлов кластера). 

Дополнительные сведения см. в разделе [развертывание облачных следящего сервера для отказоустойчивого кластера](deploy-cloud-witness.md). 

**Что работает иначе?**  

Это новая функция в Windows Server 2016. 

### <a name="BKMK_VMs"></a>Устойчивость виртуальных машин  
**COMPUTE Resiliency** Windows Server 2016 включает устойчивости вычислительных Повышенная виртуальных машин с целью сокращения проблемы связи, происходящим внутри вычислительных кластеров следующим образом: 

-   **Параметры устойчивости, доступные для виртуальных машин:**  Теперь можно настроить параметры устойчивости виртуальных машин, которые определяют поведение виртуальных машин во время временных сбоев.  

    -   **Уровень устойчивости:** Помогает определить способ обработки временных сбоев. 

    -   **Устойчивость период:**  Помогает определить, как долго все виртуальные машины могут запускать изолированной. 

-   **Подвергнуть карантину неработоспособных узлов:** Неработоспособные узлы помещаются на карантин и больше не разрешены для присоединения к кластеру. Это предотвращает хлопания узлы отрицательно влияющие на другие узлы и кластера в целом. 

Дополнительные сведения о виртуальной машины вычислений устойчивости рабочего процесса и узел карантина параметры, определяющие как ваш узел размещается в изоляции или помещение в карантин, см. в разделе [устойчивость вычислительных виртуальных машин в Windows Server 2016](http://blogs.msdn.com/b/clustering/archive/2015/06/03/10619308.aspx). 

**Устойчивость хранения** в Windows Server 2016, виртуальные машины являются более устойчивым к сбоям временного хранилища. Улучшенная устойчивость виртуальных машин помогает сохранить состояние сеанса клиента виртуальных машин в случае прерывания работы хранилища. Это достигается путем виртуальной машины интеллектуальные и быстрый ответ на проблемы с инфраструктурой хранения. 

Когда виртуальная машина отключается от его базового хранилища, он приостанавливается и ожидает хранения для восстановления. Пока выполнение приостановлено, виртуальная машина сохраняет в контексте приложений, работающих под управлением в нем. Когда восстанавливается подключение к виртуальной машине в хранилище, виртуальную машину возвращает состояние выполнения. В результате на восстановления сохраняется состояние сеанса на компьютере клиента. 

В Windows Server 2016 устойчивость виртуальных машин хранилища слишком зависимых и оптимизированный для гостевых кластеров. 

### <a name="BKMK_Diagnostics"></a>Усовершенствования диагностики в отказоустойчивой кластеризации  
Для диагностики проблем с отказоустойчивыми кластерами, Windows Server 2016 включает в себя следующее:  

-   Ряд дополнительных возможностей для файлов журнала кластера (например, сведения о часовом поясе и DiagnosticVerbose журнала), которые делает проще устранять неполадки кластеризации отработки отказа. Дополнительные сведения см. в разделе [Windows Server 2016 отказоустойчивого кластера улучшенное Устранение неполадок — журнал кластера](http://blogs.msdn.com/b/clustering/archive/2015/05/15/10614930.aspx). 

-   Новый дамп тип **дампа активной памяти**, который отфильтровывает большинства страниц памяти, выделенных для виртуальных машин и таким образом делает memory.dmp гораздо меньше и удобнее для сохранения или копирования. Дополнительные сведения см. в разделе [Windows Server 2016 отказоустойчивого кластера улучшенное Устранение неполадок — Active дампа](http://blogs.msdn.com/b/clustering/archive/2015/05/18/10615526.aspx). 

### <a name="BKMK_SiteAware"></a>Сайт с поддержкой отказоустойчивых кластеров  
Windows Server 2016 включает виду отказоустойчивыми кластерами на сайте -, включить группу узлов в растянутых кластерах, в зависимости от их физического расположения (сайт). Поддержку веб-сайт кластера оптимизирует ключевые операции во время жизненного цикла, включая способ отработки отказа, политики размещения, периодических сигналов между узлами и поведение кворума. Дополнительные сведения см. в разделе [учетом сайта отказоустойчивых кластеров в Windows Server 2016](http://blogs.msdn.com/b/clustering/archive/2015/08/19/10636304.aspx). 

### <a name="BKMK_multidomainclusters"></a>Кластеры рабочей группы и нескольких доменов  
В Windows Server 2012 R2 и предыдущих версиях кластер может создаваться только между узлами члена, присоединен к тому же домену. В Windows Server 2016 это ограничение снято, а также добавлена возможность создавать отказоустойчивый кластер без зависимостей от Active Directory. Теперь можно создать отказоустойчивые кластеры в следующих конфигурациях:  

-   **Кластеры с одним доменом.** Кластеры с узлами, присоединен к тому же домену. 

-   **Кластеры с несколькими доменами.** Кластеры с узлами, которые входят в разных доменах. 

-   **Кластеры рабочей группы.** Кластеры с узлами, которые являются членами / рабочей группы (не к домену). 

Дополнительные сведения см. в разделе [кластеры рабочей группы и нескольких доменов в Windows Server 2016](http://blogs.msdn.com/b/clustering/archive/2015/08/17/10635825.aspx)  
### <a name="BKMK_VMLoadBalancing"></a>Балансировка нагрузки виртуальной машины  
Балансировка нагрузки виртуальной машины — это новая функция в отказоустойчивой кластеризации, облегчающий эффективная Балансировка нагрузки для виртуальных машин между узлами в кластере. Перегруженное узлы определяются на основе виртуальной машины памяти и ЦП на узле. Виртуальные машины перемещаются (динамическую миграцию) из перегруженное узла на узлы с доступной пропускной способности (если применимо). Интенсивность балансировки, можно оптимизировать для обеспечения кластера для оптимальной производительности и использования. Балансировки нагрузки включена по умолчанию в Windows Server 2016 Technical Preview. Тем не менее Балансировка нагрузки отключена при включении динамической оптимизации SCVMM. 

### <a name="BKMK_VMStartOrder"></a>Порядок запуска виртуальных машин  
Порядок запуска виртуальных машин — это новая функция в отказоустойчивой кластеризации, который вводит оркестрации порядок запуска виртуальных машин (и всех групп) в кластере. Виртуальные машины можно группировать на уровни и зависимости для порядка запуска могут создаваться между различными уровнями. Это гарантирует, что первого запуска наиболее важных виртуальных машин (например, контроллеры домена или служебную программу виртуальных машин). Виртуальные машины не запущены, пока виртуальные машины, которые они имеют зависимость от также запускаются. 

### <a name="BKMK_SMBMultiChannel"></a> Упрощенное сети SMB Multichannel и Multi-NIC кластера  
Сетях отказоустойчивом кластере больше не ограничены одним сетевым Адаптером каждой подсети или сети. Упрощенное SMB Multichannel и Multi-NIC сетей кластера конфигурация сети выполняется автоматически, и каждому сетевому Адаптеру в подсети может использоваться для трафика кластера и рабочей нагрузки. Это улучшение позволяет увеличить пропускную способность сети для Hyper-V, экземпляра отказоустойчивого кластера SQL Server и других рабочих нагрузок SMB. 

Дополнительные сведения см. в разделе [упрощенное SMB Multichannel и Multi-NIC сетей кластера](smb-multichannel.md).

## <a name="see-also"></a>См. также  
* [Хранилище](../storage/storage.md)  
* [Новые возможности хранилища в Windows Server 2016](../storage/whats-new-in-storage.md)  