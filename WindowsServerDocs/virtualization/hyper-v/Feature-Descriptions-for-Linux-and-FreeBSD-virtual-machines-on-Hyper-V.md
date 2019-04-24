---
title: Описаниями для виртуальных машин Linux и FreeBSD на Hyper-V
description: Описание возможностей, которые влияют на основные компоненты, такие как сети, хранилища, объема памяти при использовании Linux и FreeBSD на виртуальной машине
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a9ee931d-91fc-40cf-9a15-ed6fa6965cb6
author: shirgall
ms.author: kathydav
ms.date: 10/03/2016
ms.openlocfilehash: 944f8e9d902953ab4d6da0750603a2c40fa9e96d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2019
ms.locfileid: "59844895"
---
# <a name="feature-descriptions-for-linux-and-freebsd-virtual-machines-on-hyper-v"></a>Описаниями для виртуальных машин Linux и FreeBSD на Hyper-V

>Область применения. Windows Server 2016, Hyper-V Server 2016, Windows Server 2012 R2, Hyper-V Server 2012 R2, Windows Server 2012, Hyper-V Server 2012, Windows Server 2008 R2, Windows 10, Windows 8.1, Windows 8, Windows 7.1, Windows 7

В этой статье описываются функции, доступные в компоненты, такие как основные, сети, хранилища и памяти, при использовании Linux и FreeBSD на виртуальной машине.

## <a name="BKMK_core"></a>Core

|**Возможность**|**Описание**|
|-|-|
|Завершение работы интегрированной|С помощью этой функции администратор может завершить работу виртуальных машин в диспетчере Hyper-V. Дополнительные сведения см. в разделе [завершение работы операционной системы](https://technet.microsoft.com/library/dn798297(WS.11).aspx#BKMK_Shutdown).|
|Синхронизация времени|Эта функция гарантирует, что, поддерживаемый время на виртуальной машине, синхронизируется с поддерживаться на время на узле. Дополнительные сведения см. в разделе [синхронизация времени](https://technet.microsoft.com/library/dn798297(WS.11).aspx#BKMK_time).|
|Точное время Windows Server 2016|Эта функция позволяет гостевой использовать возможности Windows Server 2016 точное время, что увеличивает время синхронизации с узла 1 мс точности. Дополнительные сведения см. в разделе [точное время Windows Server 2016](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-2016-accurate-time)|
|Поддержка многопроцессорной обработки|С помощью этой функции виртуальной машины можно использовать несколько процессоров на узле путем настройки нескольких виртуальных ЦП.|
|Периодический сигнал|За счет этого узла, чтобы отслеживать состояние виртуальной машины. Дополнительные сведения см. в разделе [пульса](https://technet.microsoft.com/library/dn798297(WS.11).aspx#BKMK_heartbeat).|
|Встроенной поддержки|С помощью этой функции можно использовать мышь на рабочем столе виртуальной машины и для виртуальной машины с помощью мыши без проблем между настольных систем Windows Server и на консоли Hyper-V.|
|Hyper-V конкретного устройства хранения|Эта функция предоставляет высокопроизводительные доступ к запоминающие устройства, присоединенные к виртуальной машине.|
|Hyper-V определенного сетевого устройства|Эта функция предоставляет доступ высокой производительности сетевых адаптеров, подключенных к виртуальной машине.|

## <a name="BKMK_Networking"></a>Сетевые подключения

|**Возможность**|**Описание**|
|-|-|
|Кадры крупного размера|С помощью этой функции администратор может увеличить размер сетевых пакетов за пределами 1500 байтов, что приводит к значительному увеличению производительности сети.|
|Теги виртуальной локальной сети и коммутации|Эта функция позволяет настроить трафика виртуальной локальной сети (VLAN) для виртуальных машин.|
|Динамическая миграция|С помощью этой функции можно перенести виртуальную машину с одного узла на другой узел. Дополнительные сведения см. в разделе [Обзор динамической миграции виртуальных машин](https://technet.microsoft.com/library/hh831435.aspx).|
|Статический IP-адрес внедрения|С помощью этой функции можно реплицировать статический IP-адрес виртуальной машины после ее отработки отказа его реплику на другой узел. Такие IP-репликация гарантирует рабочих нагрузок сети для эффективной работы после отработки отказа.|
|vRSS (виртуального масштабирования на стороне приема)|Распределяет нагрузку из виртуального сетевого адаптера между несколькими виртуальными процессорами на виртуальной машине. Дополнительные сведения см. в разделе [Virtual Receive-side Scaling, в Windows Server 2012 R2](https://technet.microsoft.com/library/dn383582.aspx).|
|Сегментация TCP и разгрузка контрольной суммы|Передача сегментации и контрольная сумма работать с гостевой Процессор виртуального коммутатора или сетевой адаптер во время передачи данных в сети.|
|Большой получать разгрузки (LRO)|Увеличивается пропускная способность входящих подключений с высокой пропускной способностью путем объединения нескольких пакетов в буфер большего размера, уменьшая нагрузку на ЦП.|
|SR-IOV;|Единый корневой операции ввода-вывода устройства используют DDA чтобы разрешить им доступ к частям конкретных Сетевых плат, позволяя для сокращенной задержки и увеличения пропускной способности. SR-IOV требует драйверы в актуальном состоянии физической функции (PF) на узле и виртуальных функций (VF) на гостевом компьютере.|

## <a name="BKMK_Storage"></a>Хранилища

|**Возможность**|**Описание**|
|-|-|
|Изменения размера VHDX|С помощью этой функции администратора можно изменить размер фиксированного размера vhdx-файле, подключенного к виртуальной машине. Дополнительные сведения см. в разделе [Online Virtual Hard Disk изменение размера Overview](https://technet.microsoft.com/library/dn282286.aspx).|
|виртуальный адаптер Fibre Channel;|С помощью этой функции виртуальные машины можно распознать устройство fiber channel и монтировать в скомпилированных в собственном коде. Дополнительные сведения см. в статье [Обзор виртуального адаптера Fibre Channel для Hyper-V](https://technet.microsoft.com/library/hh831413.aspx).|
|Резервное копирование виртуальной машины|Эта функция облегчает нуля работу времени резервной копии динамической виртуальных машин.<br /><br />Обратите внимание, что операция резервного копирования не работает, если у виртуальной машины, виртуальные жесткие диски (VHD), которые размещаются в удаленном хранилище, например в общей папке Server Message Block (SMB) или iSCSI-тома. Кроме того убедитесь, что целевого объекта архивации не находится на одном томе с тома, резервную копию.|
|ОБРЕЗАТЬ поддержки|TRIM подсказки уведомления на диск, который определенных секторов, которые ранее были выделены приложением больше не требуются и могут быть удалены. Этот процесс обычно используется, когда приложение делает выделение больших пространства посредством файла, а затем самостоятельно управляет выделений в файл, например, для файлов виртуальных жестких дисков.|
|WWN-ИМЕН SCSI|Драйверов storvsc извлекает сведения о World широкий-имя порта и узла устройств, подключенных к виртуальной машине, а также создает соответствующий sysfs файлы. |

## <a name="BKMK_Memory"></a>Память

|**Возможность**|**Описание**|
|-|-|
|Поддержка PAE ядра|Физический расширение адресов (PAE) технология позволяет 32-разрядных ядра для доступа к физической адресное пространство, которое больше, чем 4 ГБ. Более старые дистрибутивы Linux, такого как RHEL 5.x, используемый для отправки отдельных ядра, которое было включено расширение физических адресов. Новых установок например RHEL 6.x предварительно создали PAE поддержки.|
|Конфигурация MMIO разрыв|С помощью этой функции производителей устройства можно настроить расположение разрыв памяти сопоставлены ввода-вывода (MMIO). Разрыв MMIO обычно используется для разделения доступной физической памяти между устройство просто достаточно операционных систем (JeOS) и инфраструктуры фактическое программного обеспечения, обеспечивающий работу устройства.|
|Динамическая память — «горячей» заменой|Узел можно динамически увеличить или уменьшить объем памяти для виртуальной машины, находящимся в операции. Перед подготовкой, администратор включает динамическую память на панели параметров виртуальной машины и укажите память при запуске, минимальный объем памяти и максимальный объем памяти для виртуальной машины. Когда виртуальная машина находится в операцию, которую не удается отключить динамическую память и только минимальным и максимальным параметры можно изменить. (Это лучший способ указать эти размеры памяти, кратные 128 МБ).<br /><br />При первом запуске доступных виртуальной машине памяти равен **память при запуске**. По мере увеличения объема памяти из-за рабочих нагрузок приложений Hyper-V может динамически выделять больше памяти на виртуальную машину с помощью механизма горячей, если поддерживается этой версией ядра. Максимальный объем памяти, выделенной ограничивается значение **максимальный объем памяти** параметра.<br /><br />Вкладка "память" диспетчера Hyper-V будут отображаться объем памяти, назначенной виртуальной машине, но Статистика использования памяти виртуальной машины отобразится наибольший объем выделенной памяти.<br /><br />Дополнительные сведения см. в разделе [Hyper-V Dynamic Memory Overview](https://technet.microsoft.com/library/hh831766.aspx).<br /><br />|
|Динамическая память — воздушного шага|Узел можно динамически увеличить или уменьшить объем памяти для виртуальной машины, находящимся в операции. Перед подготовкой, администратор включает динамическую память на панели параметров виртуальной машины и укажите память при запуске, минимальный объем памяти и максимальный объем памяти для виртуальной машины. Когда виртуальная машина находится в операцию, которую не удается отключить динамическую память и только минимальным и максимальным параметры можно изменить. (Это лучший способ указать эти размеры памяти, кратные 128 МБ).<br /><br />При первом запуске доступных виртуальной машине памяти равен **память при запуске**. По мере увеличения объема памяти из-за рабочих нагрузок приложений Hyper-V может динамически выделять больше памяти на виртуальную машину с помощью механизма горячей (см. выше). Уменьшении потребностей памяти Hyper-V автоматически отменить подготовку памяти из виртуальной машины с помощью механизма выноски. Hyper-V не отменит подготовку памяти ниже **минимальный объем памяти** параметра.<br /><br />Вкладка "память" диспетчера Hyper-V будут отображаться объем памяти, назначенной виртуальной машине, но Статистика использования памяти виртуальной машины отобразится наибольший объем выделенной памяти.<br /><br />Дополнительные сведения см. в разделе [Hyper-V Dynamic Memory Overview](https://technet.microsoft.com/library/hh831766.aspx).<br /><br />|
|Изменение размера памяти среды выполнения|Администратора можно задать объем доступной памяти на виртуальную машину во время операции, его («"Горячий" Удалить») уменьшения или увеличения объема памяти («горячей»). Память возвращается Hyper-V через драйвер всплывающей (см. в разделе «Динамической памяти – воздушного шага»). Выноска драйвер поддерживает минимальный объем свободной памяти после воздушным шаром, называется «floor», поэтому назначения памяти не может быть уменьшен ниже текущего спроса, а также этот объем floor. Вкладка "память" диспетчера Hyper-V будут отображаться объем памяти, назначенной виртуальной машине, но Статистика использования памяти виртуальной машины отобразится наибольший объем выделенной памяти. (Это лучший способ указать памяти значения, кратные 128 МБ).|

## <a name="BKMK_Video"></a>Видео

|**Возможность**|**Описание**|
|-|-|
|Hyper v, появляющихся видеоустройства|Эта функция предоставляет высокопроизводительной графики и разрешения руководителя для виртуальных машин. Это устройство не поддерживает режим расширенного сеанса или Microsoft RemoteFX возможности.|

## <a name="BKMK_Misc"></a>Прочие

|**Возможность**|**Описание**|
|-|-|
|Exchange KVP (пара «ключ-значение»)|Этот компонент предоставляет пару ключ значение службы exchange (KVP) для виртуальных машин. Обычно администраторы используют механизм KVP для операций чтения и записи пользовательских данных операции на виртуальной машине. Дополнительные сведения см. в разделе [обмена данными: С помощью пары "ключ значение" для обмена информацией между узлом и гостевой в Hyper-V](https://technet.microsoft.com/library/dn798287.aspx).|
|Немаскируемое прерывание|С помощью этой функции администратор может выдавать немаскируемых прерываний (NMI) к виртуальной машине. NMIs полезны при получении аварийные дампы операционных систем, которые перестали отвечать из-за ошибок приложения. После перезагрузки, можно диагностировать эти аварийных дампов.|
|Копирование файлов с носителя на гостевой|Эта функция позволяет файлы для копирования на физический компьютер для гостевых виртуальных машин без использования сетевого адаптера. Дополнительные сведения см. в разделе [гостевые службы](https://technet.microsoft.com/library/dn798297(WS.11).aspx#BKMK_guest).|
|Команда lsvmbus|Эта команда возвращает сведения об устройствах на основе шины виртуальной машины Hyper-V (VMBus), аналогичную команды lspci сведения.|
|Сокеты Hyper-V|Это канал дополнительное взаимодействие между узлом и гостевой операционной системы. Чтобы загрузить и использовать модуль ядра сокеты Hyper-V, см. в разделе [ваши собственные службы интеграции](https://msdn.microsoft.com/virtualization/hyperv_on_windows/develop/make_mgmt_service).|
|Сквозной режим PCI/DDA|С Windows Server 2016 администраторы могут проходить через устройства PCI Express с помощью механизма дискретных назначение устройств. Общие устройства, сетевых карт, графические платы и специальные запоминающих устройств. Для виртуальной машины требуется соответствующий драйвер для использования предоставляемых оборудования. Оборудование должны назначаться виртуальной машины для его можно использовать.<br /><br />Дополнительные сведения см. в разделе [дискретных назначение устройств - описание и фона](https://blogs.technet.microsoft.com/virtualization/2015/11/19/discrete-device-assignment-description-and-background/).<br /><br />DDA является необходимым условием для работы в сети SR-IOV. Виртуальные порты нужно будет назначаться виртуальной машине и виртуальной машины необходимо использовать правильные драйверы виртуальной функции (VF) мультиплексирование устройства.|

## <a name="BKMK_gen2"></a>Виртуальные машины поколения 2

|**Возможность**|**Описание**|
|-|-|
|Загрузки, с помощью UEFI|Эта функция позволяет виртуальным машинам для загрузки с использованием Unified Extensible Firmware Interface (UEFI).<br /><br />Дополнительные сведения см. в статье, посвященной [общим сведениям о виртуальных машинах поколения 2](https://technet.microsoft.com/library/dn282285.aspx).|
|Безопасная загрузка|Эта функция позволяет виртуальным машинам в режиме безопасной загрузки на основе UEFI. При загрузке виртуальной машины в безопасном режиме различные компоненты операционной системы проверяются с использованием подписей, имеющиеся в хранилище данных UEFI.<br /><br />Дополнительные сведения см. в статье [Безопасная загрузка](https://technet.microsoft.com/library/dn486875.aspx).|

## <a name="see-also"></a>См. также

* [Поддерживается CentOS и Red Hat Enterprise Linux виртуальных машин в Hyper-V](Supported-CentOS-and-Red-Hat-Enterprise-Linux-virtual-machines-on-Hyper-V.md)

* [Поддерживаемые виртуальные машины Debian на узле Hyper-V](Supported-Debian-virtual-machines-on-Hyper-V.md)

* [Поддерживаемые виртуальные машины Oracle Linux в Hyper-V](Supported-Oracle-Linux-virtual-machines-on-Hyper-V.md)

* [Поддерживаемые виртуальные машины SUSE в Hyper-V](Supported-SUSE-virtual-machines-on-Hyper-V.md)

* [Поддерживаемые виртуальные машины Ubuntu на базе Hyper-V](Supported-Ubuntu-virtual-machines-on-Hyper-V.md)

* [Поддерживаемые виртуальные машины FreeBSD в Hyper-V](Supported-FreeBSD-virtual-machines-on-Hyper-V.md)

* [Рекомендации по использованию Linux на Hyper-V](Best-Practices-for-running-Linux-on-Hyper-V.md)

* [Рекомендации по использованию FreeBSD на Hyper-V](Best-practices-for-running-FreeBSD-on-Hyper-V.md)