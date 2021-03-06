---
title: Подсистема балансировки сетевой нагрузки
description: В этом разделе представлен обзор балансировки сетевой нагрузки \(\) NLB в Windows Server 2016. С помощью NLB можно управлять двумя или более серверами как одним виртуальным кластером. Балансировка сетевой нагрузки повышает доступность и масштабируемость приложений Интернет-сервера, например, используемых в Интернете, FTP, брандмауэре, прокси-сервере, виртуальной частной сети \(VPN-\)и других задачах,\-важных серверах.
manager: dougkim
ms.prod: windows-server
ms.technology: networking-nlb
ms.topic: article
ms.assetid: 244a4b48-06e5-4796-8750-a50e4f88ac72
ms.author: lizross
author: eross-msft
ms.date: 09/13/2018
ms.openlocfilehash: 80dae16442041e3b46babaca6d163095c1c5e475
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/26/2020
ms.locfileid: "80309696"
---
# <a name="network-load-balancing"></a>Подсистема балансировки сетевой нагрузки

>Область применения: Windows Server (Semi-Annual Channel), Windows Server 2016

В этом разделе представлен обзор балансировки сетевой нагрузки \(\) NLB в Windows Server 2016. С помощью NLB можно управлять двумя или более серверами как одним виртуальным кластером. Балансировка сетевой нагрузки повышает доступность и масштабируемость приложений Интернет-сервера, например, используемых в Интернете, FTP, брандмауэре, прокси-сервере, виртуальной частной сети \(VPN-\)и других задачах,\-важных серверах.  

> [!NOTE]
> Windows Server 2016 включает новое программное обеспечение, основанное на Azure Load Balancer \(SLB\) в качестве компонента программно-определяемой сети \(SDN\) Infrastructure. Используйте SLB вместо балансировки сетевой нагрузки, если вы используете SDN, используют рабочие нагрузки, не относящиеся к Windows, требуется преобразование исходящего сетевого адреса \(\)NAT, или требуется уровень 3 \(\) или балансировка нагрузки на основе TCP. Вы можете продолжать использовать балансировку сетевой нагрузки с Windows Server 2016 для развертываний без SDN. Дополнительные сведения о SLB см. в разделе [Программная балансировка нагрузки (SLB) для Sdn](../sdn/technologies/network-function-virtualization/Software-Load-Balancing--SLB--for-SDN.md).

Функция балансировки сетевой нагрузки \(NLB\) распределяет трафик между несколькими серверами с помощью протокола TCP\/IP Network. Объединяя два или более компьютеров, на которых запущены приложения, в один виртуальный кластер, NLB обеспечивает надежность и производительность веб-серверов и других\-важных серверов.  
  
Серверы в NLB-кластере называются *узлами*, и на каждом узле выполняется отдельная копия серверных приложений. Балансировка сетевой нагрузки позволяет распределять входящие клиентские запросы между узлами в кластере. При этом можно настроить нагрузку для каждого узла. Если нужно обработать дополнительную нагрузку, узлы можно добавлять к кластеру динамически. Кроме того, технология балансировки сетевой нагрузки может направлять весь трафик на один предназначенный для этого узел, называемый *узлом по умолчанию*.  
  
Балансировка сетевой нагрузки позволяет обращаться ко всем компьютерам в кластере по одному и тому же набору IP-адресов и поддерживает набор уникальных IP-адресов, выделенных для каждого узла. Для приложений с балансировкой нагрузки\-при сбое или переходе узла в режим «вне сети» нагрузка автоматически перераспределяется между компьютерами, которые еще работают. Когда компьютер будет готов к работе, он может снова присоединиться к кластеру в рабочем режиме и взять на себя часть нагрузки, что позволит снизить объем данных, приходящийся на другие компьютеры кластера.  
  
## <a name="practical-applications"></a>Практическое применение  
Балансировка сетевой нагрузки полезна для обеспечения того, что приложения без отслеживания состояния, такие как веб-серверы, работающие службы IIS \(IIS\), доступны с минимальным временем простоя и что они масштабируются \(путем добавления дополнительных серверов при увеличении нагрузки\). В следующих разделах описывается применение NLB для поддержки высокой доступности, масштабируемости и управляемости кластерных серверов, выполняющих указанные приложения.  
  
### <a name="high-availability"></a>Высокая доступность  
Система высокой доступности обеспечивает обслуживание на приемлемом уровне с минимальной потерей машинного времени. Для обеспечения высокого уровня доступности NLB включает в себя встроенные\-функции, которые могут автоматически выполнять следующие действия:  
  
-   Выявление в кластере самопроизвольно прекратившего работу или отключившегося от сети узла с последующим его восстановлением.  
  
-   Балансировка нагрузки сети при добавлении и удалении узлов.  
  
-   Восстановление и перераспределение рабочей нагрузки в течение 10 секунд.  
  
### <a name="scalability"></a>Масштабируемость  
Масштабируемость показывает, насколько можно расширить возможности компьютера, службы или приложения в соответствии с повышением требований к его производительности. Применительно к кластерам NLB масштабируемость — это возможность добавления одной или нескольких систем к существующему кластеру, когда общая нагрузка кластера превышает его текущую производительность. Поддержка масштабируемости реализуется в NLB следующим образом:  
  
-   Балансировка запросов на загрузку в кластере балансировки сетевой нагрузки для отдельных служб TCP\/IP.  
  
-   Поддержка до 32 компьютеров в одном кластере.  
  
-   Распределите нагрузку на несколько запросов на загрузку сервера \(из одного клиента или с нескольких клиентов\) на нескольких узлах в кластере.  
  
-   Добавление узлов в NLB-кластер по мере увеличения нагрузки, не приводящее к сбоям в работе кластера.  
  
-   Вывод узлов из состава кластера по мере уменьшения нагрузки.  
  
-   Высокая производительность и уменьшение объема служебных данных за счет реализации полнофункционального конвейерного режима. Данный режим позволяет отправлять запросы NLB-кластеру, не ожидая ответа на предыдущий запрос.  
  
### <a name="manageability"></a>Управляемость  
Поддержка управляемости реализуется в NLB следующим образом:  
  
-   Управление и настройка нескольких кластеров балансировки сетевой нагрузки и узлов кластера с одного компьютера с помощью диспетчера NLB или [командлетов балансировки сетевой нагрузки (NLB) в Windows PowerShell](https://technet.microsoft.com/library/hh801274.aspx).
  
-   Используя правила управления портами, можно задавать режим балансировки для отдельного IP-порта или группы портов.  
  
-   Для портов каждого веб-сайта могут определяться различные правила. Если для нескольких приложений или веб-сайтов используется один и тот же набор балансировки нагрузки серверов\-, правила портов основываются на целевом виртуальном IP-адресе \(использовании виртуальных кластеров\).  

-   Направлять все клиентские запросы на один узел, используя необязательные правила одного\-узла. NLB будет направлять клиентские запросы на определенный узел, где выполняются заданные приложения.  

-   Имеется возможность блокировки доступа по сети к определенным IP-портам.  

-   Включите протокол управления группами Интернета \(поддержку IGMP\) на узлах кластера для управления переполнением портов коммутатора \(, где входящие сетевые пакеты отправляются на все порты на коммутаторе\) при работе в режиме многоадресной рассылки.  

-   Запуск, остановка и управление действиями NLB могут производиться удаленно с использованием команд или сценариев Windows PowerShell.  

-   События NLB можно просматривать в журнале событий Windows. В журнал событий записываются все действия NLB и изменения кластера.  

## <a name="important-functionality"></a>Важные функции  
 
NLB устанавливается как стандартный компонент сетевого драйвера Windows Server. Его операции прозрачны для сетевого стека TCP\/IP. На следующем рисунке показана связь между балансировкой сетевой нагрузки и другими компонентами программного обеспечения в типичной конфигурации.  
  
![Балансировка сетевой нагрузки и другие программные компоненты](../media/NLB/nlb.jpg)  
  
Ниже приведены основные возможности балансировки сетевой нагрузки.  
  
- Не требует для запуска изменений аппаратной части.  
  
- Предоставляет средства балансировки сетевой нагрузки для управления несколькими кластерами и всеми узлами кластеров, а также их настройки с одного удаленного или локального компьютера.  
  
- Позволяет клиентам получать доступ к кластеру с помощью одного логического имени Интернета и виртуального IP-адреса, который называется IP-адресом кластера \(он содержит отдельные имена для каждого компьютера\). Балансировка сетевой нагрузки поддерживает несколько виртуальных IP-адресов для многосетевых серверов.  
  
> [!NOTE]  
> При развертывании виртуальных машин в качестве виртуальных кластеров балансировка сетевой нагрузки не требует, чтобы серверы были подключены к нескольким виртуальным IP-адресам.  
  
- Средство балансировки сетевой нагрузки может быть привязано к нескольким сетевым адаптерам, что позволяет настроить несколько независимых кластеров на каждом узле. Поддержка нескольких сетевых адаптеров — это не то же самое, что виртуальные кластеры, в которых можно настраивать несколько кластеров на одном сетевом адаптере.  
  
- Не требует модификации серверных приложений, что обеспечивает их работу в любом кластере NLB.  
  
- Возможна настройка автоматического добавления узла в кластер при сбое в работе узла данного кластера с последующим возвращением с сеть. Добавленный узел может приступать к обработке новых клиентских обращений к серверу.  
  
-   Обеспечивает возможность отключения компьютеров от сети для проведения профилактического обслуживания, не затрагивая операции кластера на других узлах.  
  
## <a name="hardware-requirements"></a>Требования к оборудованию  
Ниже приведены требования к оборудованию для запуска кластера балансировки сетевой нагрузки.  
  
-   Все узлы кластера должны располагаться в одной подсети.  
  
-   Количество сетевых адаптеров на каждом узле не ограничено, при этом различные узлы могут иметь разное число адаптеров.  
  
-   Все сетевые адаптеры в одном кластере необходимо использовать либо в одноадресном, либо в многоадресном режиме. Балансировка сетевой нагрузки не поддерживает смешанную среду одноадресной и многоадресной рассылки внутри одного кластера.  
  
-   Если используется одноадресный режим, то сетевой адаптер, используемый для работы\-клиента с\-ным трафиком кластера, должен поддерживать изменение его контроля доступа к носителю \(адрес MAC\).  
  
## <a name="software-requirements"></a>Требования к программному обеспечению  
Ниже приведены требования к программному обеспечению для запуска кластера балансировки сетевой нагрузки.  
  
-   На адаптере, для которого включена балансировка сетевой нагрузки на каждом узле, можно использовать только TCP-\/IP. Не добавляйте никакие другие протоколы \(например,\) IPX к этому адаптеру.  
  
-   IP-адреса серверов в составе кластера должны быть статическими.  
  
> [!NOTE]  
> NLB не поддерживает протокол динамической конфигурации узла \(\)DHCP. NLB отключает протокол DHCP на каждом настраиваемом интерфейсе.  
  
## <a name="installation-information"></a>Сведения об установке  
Балансировку сетевой нагрузки можно установить с помощью диспетчер сервера или команд Windows PowerShell для балансировки сетевой нагрузки.

Дополнительно можно установить средства балансировки сетевой нагрузки для управления локальным или удаленным кластером NLB. К этим средствам относятся диспетчер балансировки сетевой нагрузки и команды Windows PowerShell NLB.

### <a name="installation-with-server-manager"></a>Установка с диспетчер сервера

В диспетчер сервера можно использовать мастер добавления ролей и компонентов, чтобы добавить функцию **балансировки сетевой нагрузки** . После завершения работы мастера устанавливается балансировка сетевой нагрузки и не требуется перезагружать компьютер.


### <a name="installation-with-windows-powershell"></a>Установка с помощью Windows PowerShell  

Чтобы установить NLB с помощью Windows PowerShell, выполните следующую команду в командной строке Windows PowerShell с повышенными привилегиями на компьютере, где требуется установить NLB.

    
    Install-WindowsFeature NLB -IncludeManagementTools
    
После завершения установки перезагрузка компьютера не требуется.

Дополнительные сведения см. в разделе [Install-WindowsFeature](https://docs.microsoft.com/powershell/module/servermanager/install-windowsfeature?view=win10-ps).

### <a name="network-load-balancing-manager"></a>Диспетчер балансировки сетевой нагрузки
Чтобы открыть диспетчер балансировки сетевой нагрузки в диспетчере сервера, в меню **Сервис** выберите пункт **Диспетчер балансировки сетевой нагрузки**.
  
## <a name="additional-resources"></a>Дополнительные ресурсы  
В следующей таблице приведены ссылки на дополнительные сведения о функции балансировки сетевой нагрузки.  
  
|Тип контента|Ссылки|  
|----------------|--------------|  
|Развертывание|&#124; [Рекомендации по развертыванию балансировки сетевой](https://technet.microsoft.com/library/cc754833(WS.10).aspx) нагрузки [Настройка балансировки сетевой нагрузки с помощью служб терминалов](https://technet.microsoft.com/library/cc771300(v=WS.10).aspx)|  
|Операции|&#124; [Управление кластерами балансировки сетевой нагрузки](https://technet.microsoft.com/library/cc753954(WS.10).aspx) &#124; [Настройка параметров балансировки сетевой нагрузки](https://technet.microsoft.com/library/cc731619(WS.10).aspx) [Управление узлами в кластерах балансировки сетевой нагрузки](https://technet.microsoft.com/library/cc770870(WS.10).aspx)|  
|Диагностика|[Устранение](https://technet.microsoft.com/library/cc732592(WS.10).aspx) &#124; [ошибок и событий кластера](https://technet.microsoft.com/library/cc731678(WS.10).aspx) балансировки сетевой нагрузки|
|Средства и параметры|[Балансировка сетевой нагрузки командлеты Windows PowerShell](https://go.microsoft.com/fwlink/p/?LinkId=238123)|
|Ресурсы сообщества|[Форум\) \(кластеризации высокого уровня доступности](https://go.microsoft.com/fwlink/p/?LinkId=230641)
