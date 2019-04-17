---
redirect_url: /windows-server/windows-server
ms.openlocfilehash: aa1bc1d94f91a2b9584f72398385575d22db33a9
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/17/2017
---
# <a name="windows-server-2016"></a>Windows Server 2016

Эта библиотека содержит информацию, необходимую ИТ-специалистам для оценки, планирования, развертывания, защиты и администрирования Windows Server 2016.

> [!Note] 
> В следующую версию Windows Server будут внесены изменения! Информацию о планируемых изменениях см. в [обзоре Semi-Annual Channel для Windows Server](./get-started/semi-annual-channel-overview.md). 

[![WВидеообзор Windows Server 2016(media/front-page-video.png)](https://www.youtube.com/embed/V8oF0JpDzaM)

<table border="0" width="100%" align='center'>
  <tr style="text-align:center;">
    <td align='center' style="width:25%; border:0;">
      <a href="/windows-server/get-started/what-s-new-in-windows-server-2016">
        <img height=145 src="media/whats-new-highlight.png" alt="What's new icon" title="Новые возможности Windows Server16"/></a>
        <br/>Новые возможности
    </td>
    <td align='center' style="width:25%; border:0;">
      <a href="/windows-server/get-started/server-basics">
        <img height=145 src="media/1-getstarted.png" alt="get started icon" title="Начало работы с Windows Server16" /></a>
      <br/>Начало работы </td>
    <td align='center' style="width:25%; border:0;">
      <a href="/windows-server/administration/index">
        <img height=145 src="media/8-management.png" alt="administer icon" title="Администрирование Windows Server" /></a>
      <br/>Администрирование </td>
    <td align='center' style="width:25%; border:0;">
      <a href="/windows-server/failover-clustering/failover-clustering-overview">
        <img height=145 src="media/3-failover.png" alt="Failover clustering icon" title="Отказоустойчивая кластеризация Windows Server" /></a>
      <br/>Отказоустойчивая кластеризация </td>
  </tr>
  <tr style="text-align:center;">
    <td align='center' style="width:25%; border:0;"><br/>
      <a href="/windows-server/identity/identity-and-access">
        <img height=145 src="media/4-identity.png" alt="Identity and access icon" title="Удостоверения и доступ Windows Server" /></a>
      <br>Удостоверения и доступ </td>
    <td align='center' style="width:25%; border:0;"><br/>
      <a href="/windows-server/networking/networking">
        <img height=145 src="media/6-networking.png" alt="Networking icon" title="Сетевое взаимодействие в Windows Server" />
        </a>
      <br/>Сетевое взаимодействие </td>
    <td align='center' style="width:25%; border:0;"><br/>
      <a href="/windows-server/remote/index">
        <img height=145 src="media/remote.png" alt="remote icon" title="Удаленный доступ и управление серверами" />
        </a>
      <br/>Удаленный доступ </td>
    <td align='center' style="width:25%; border:0;"><br/>
      <a href="/windows-server/security/security-and-assurance">
        <img height=145 src="media/5-security.png" alt="Security icon" title="Безопасность и контроль в Windows Server" />
      </a>
      <br/>Безопасность и контроль </td>
  </tr>
  <tr style="text-align:center;">
    <td align='center' style="width:25%; border:0;">&nbsp;</td>
    <td align='center' style="width:25%; border:0;"><br>
      <a href="/windows-server/storage/storage">
        <img height=145 src="media/7-storage.png" alt="Storage icon" title="Хранение данных в Windows Server" />
      </a>
      <br/>Хранение </td>
   <td align='center' style="width:25%; border:0;"><br/>
      <a href="/windows-server/virtualization/virtualization">
        <img height=145 src="media/virtualization.png" alt="virtualization icon" title="Виртуализация Windows Server" /></a>
      <br/>Виртуализация </td>
    <td align='center' style="width:25%; border:0;">&nbsp; </td>
  </tr>
</table>

<br/>

> [!Note] 
> Чтобы лично оценить новые функции и возможности в Windows Server 2016, можно скачать ознакомительную версию, посетив страницу [Оценки Windows Server](https://www.microsoft.com/evalcenter/evaluate-windows-server-2016). 


## <a name="windows-server-2016-editions"></a>Выпуски Windows Server2016

Для Windows Server2016 доступны выпуски Standard, Datacenter и Essentials. Windows Server2016 Datacenter включает неограниченные права на виртуализацию, а также новые возможности для создания программно-определяемого центра обработки данных. Windows Server2016 Standard предлагает возможности корпоративного класса с ограниченными правами на виртуализацию. Windows Server Essentials— оптимальный вариант для первого сервера, подключенного к облаку. Он снабжен собственной [подробной документацией](http://go.microsoft.com/fwlink/?LinkID=827171), поэтому в данных материалах основное внимание уделяется выпускам Standard и Datacenter. В следующей таблице кратко перечислены основные различия между выпусками Standard и Datacenter:

|Функция|Datacenter|Standard|  
|-------------------|----------|-----------------------|  
|Основные функциональные возможности Windows Server| да| да|
|Контейнеры Hyper-V/ОС|без ограничений|   2|
|Контейнеры Windows Server|без ограничений|   без ограничений|
|Служба защиты узла| да| да|
|Вариант установки Nano Server| да| да|
|Компоненты хранилища, включая локальные дисковые пространства и реплики хранилища| да| нет|
|Экранированные виртуальные машины| да| нет|
|Инфраструктура программно-конфигурируемой сети (сетевой контроллер, балансировка нагрузки программного обеспечения и мультитенантный шлюз)| да| нет|

Дополнительные сведения см. в статьях [Цены и условия лицензирования для Windows Server2016](https://www.microsoft.com/en-us/cloud-platform/windows-server-pricing) и [Сравнение функций в разных версиях Windows Server](https://www.microsoft.com/en-us/cloud-platform/windows-server-comparison).

## <a name="installation-options"></a>Параметры установки

Выпуски Standard и Datacenter поддерживают три варианта установки:

- **Основные серверные компоненты**: сокращает требования к свободному пространству на диске, уменьшает поле для потенциальных атак и, самое главное, снижает требования к обслуживанию. Это **рекомендуемый** вариант, если только у вас нет особой необходимости в дополнительных элементах пользовательского интерфейса и графических средствах управления.
- **Сервер с рабочим столом**: устанавливает стандартный пользовательский интерфейс и все инструменты, в том числе компоненты взаимодействия с пользователем, для которых в выпуске в Windows Server2012 R2 требовалась отдельная установка. Роли и компоненты сервера устанавливаются при помощи диспетчера серверов или других методов.
- **Nano Server**: это удаленно управляемая серверная ОС, оптимизированная для частных облаков и центров обработки данных. Этот вариант аналогичен Windows Server в режиме основных серверных компонентов, однако значительно меньше по размеру, не имеет функций локального входа и поддерживает только 64-разрядные приложения, средства и агенты. В сравнении с другими вариантами он занимает гораздо меньше места на диске, намного быстрее запускается и требует на порядок меньше обновлений и перезапусков.

>[!Note]
> В отличие от предыдущих выпусков Windows Server, после установки преобразовать основные серверные компоненты в сервер с возможностями рабочего стола (и наоборот) невозможно. Например, если вы установили основные серверные компоненты, а затем решили использовать сервер с возможностями рабочего стола, необходимо выполнить установку заново (и наоборот).


Теперь, когда вы знаете, какой выпуск и вариант установки подходит именно вам, щелкните ниже для начала работы с Windows Server 2016.
<br/>
<br/>

<table border="0" width="100%" align='center'>
  <tr style="text-align:center;">
    <td align='center' style="width:33%; border:0;">
      <a  href="/windows-server/get-started/getting-started-with-nano-server"> <img width="175" src="media/nano.png" alt="Icon representing Nano server" title="Сервер Nano Server— самое простое решение" /><br/>Сервер Nano Server — <br/>самое простое решение</a>
    </td>
    <td align='center' style="width:33%; border:0;"><a href="/windows-server/get-started/getting-started-with-server-core"> <img width="175" src="media/servercore.png" alt="Icon representing the Server Core installation" title="Основные серверные компоненты— рекомендуется" /><br/>Основные серверные компоненты — <br/>рекомендуется</a></td>
   <td align='center' style="width:33%; border:0;"><a href="/windows-server/get-started/getting-started-with-server-with-desktop-experience"><img width="175" src="media/desktop.png" alt="Icon representing the full desktop experience installation option for Windows Server" title="Возможности рабочего стола— все возможности" /><br/>Возможности рабочего стола — <br/>полный интерфейс</a></td>
  </tr>
</table>

## <a name="windows-server-software-defined-datacenter-sddc"></a>Программный ЦОД Windows Server

Технологии виртуализированного хранилища, сети, системы безопасности и средств управления являются основой программного ЦОД Windows Server.
<br/>
<br/>

<table border="0" width="100%" align='center'>
  <tr style="text-align:center;">
    <td align='center' style="width:10%; border:0;"></td>
    <td align='center' style="width:50%; border:0;"><a href="/windows-server/sddc"><img width="400" src="media/sddc/WS16-heading.png" alt="Icon representing SDDC" title="Программный ЦОД Windows Server" /><br/>Программный ЦОД Windows Server</a></td>
    <td align='center' style="width:10%; border:0;"></td>
  </tr>
</table>

Не нашли нужную информацию? Пользователи Windows 10 могут рассказать о том, что им необходимо, в [Центре отзывов](feedback-hub://?referrer=techDocsUcPage&tabid=2&contextid=898&newFeedback=true&topic=Windows-Server-2016.md). 