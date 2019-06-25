---
title: Evntcmd
description: 'Раздел Windows команды для ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c1aabb74-76e7-4304-95a6-50ad87e92fd9
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e2a4a7f9e6bdf6f200b86e028617cae924571455
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/31/2019
ms.locfileid: "66439451"
---
# <a name="evntcmd"></a>Evntcmd

>Область применения. Windows Server (полугодовой канал), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Настройка преобразования событий в ловушки, ловушки или на основе сведений в файле конфигурации.   
## <a name="syntax"></a>Синтаксис  
```  
evntcmd [/s <computerName>] [/v <verbosityLevel>] [/n] <FileName>  
```  
### <a name="parameters"></a>Параметры  

|      Параметр      |                                                                                                                                                            Описание                                                                                                                                                             |
|---------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  /s <computerName>  |                                                         Указывает имя компьютера, на котором вы хотите настроить перевод события для ловушки и ловушки. Если компьютер не указан, конфигурации происходит на локальном компьютере.                                                          |
| /v <verbosityLevel> | Указывает, какие типы состояний сообщения отображаются в виде ловушки и адреса назначения ловушек настроены. Этот параметр должен быть целым числом от 0 до 10. Если указать 10, отображаются все типы сообщений, включая отслеживание сообщений и предупреждения о ли ловушки Настройка успешно завершена. Если указать значение 0, сообщения не отображаются. |
|         /n          |                                                                                                           Указывает, не перезапустить службу SNMP, если этот компьютер получает изменения настройки ловушки.                                                                                                            |
|     <FileName>      |                                                                                     Задает имя файла конфигурации, содержащий сведения о преобразовании событий ловушек и ловушки, что вы хотите настроить.                                                                                     |
|         /?          |                                                                                                                                                Отображение справки в командной строке.                                                                                                                                                |

## <a name="remarks"></a>Примечания  
- Если вы хотите настроить ловушки, но не адреса назначения ловушки, можно создать допустимый файл конфигурации с помощью событий в ловушки, который — это графическая программа. Если у вас установлена служба SNMP, можно запустить событие для ловушки, введя **evntwin** в командной строке. После определения ловушек, требуется, нажмите кнопку экспорта для создания файла можно использовать с **evntcmd**. Можно использовать события для ловушки легко создать файл конфигурации, а затем использовать файл конфигурации, содержащий **evntcmd** в командной строке, чтобы быстро настроить ловушки на нескольких компьютерах.  
- Синтаксис для настройки ловушки выглядит следующим образом:  
  **Добавление #pragma** <em> <EventLogFile> <EventSource> <EventID> [<Count> [<Period>]]</em>  
  -   Текст **#pragma** должны располагаться в начале каждой записи в файл.  
  -   Параметр **добавить** указывает, что вы хотите добавить событие в настройку ловушки.  
  -   Параметры *ФайлЖурналаСобытий*, *EventSource*, и *EventID* являются обязательными. Параметр *ФайлЖурналаСобытий* указывает файл, в который записывается событие. Параметр *EventSource* задает приложение, которое создает событие. *EventID* параметр указывает уникальный номер, определяющий каждое событие. Чтобы узнать, какие значения соответствуют конкретному событию, запустите событие для ловушки, введя **evntwin** в командной строке. Нажмите кнопку **Custom**, а затем нажмите кнопку **изменить**. В разделе **источники событий**, просматривать папки, пока не найдете нужный события, необходимо настроить, щелкните его и нажмите кнопку **добавить**. Сведения об источнике событий, файла журнала событий и идентификатор события отображаются в разделе **источника, журналов**, и **специальный идентификатор ловушки**, соответственно.  
  -   *Число* параметр является необязательным и указывает сколько раз событие должно произойти, прежде чем отправляется сообщение ловушки. Если вы не используете *число* параметра, отправляется сообщение ловушки после это событие возникает один раз.  
  -   *Период* параметр является необязательным, но он требует использовать *число* параметра. *Период* параметр задает интервал времени (в секундах), во время которого событие должно произойти количество времени, указанного в параметре счетчик перед отправкой сообщения ловушки. Если вы не используете *период* параметра, отправляется сообщение ловушки после возникновения события число раз, указанное в *число* параметр, независимо от того, сколько времени прошло между событиями.  
- Синтаксис для удаления ловушки выглядит следующим образом:  
  **#pragma delete**<em><EventLogFile> <EventSource> <EventID></em>  
  -   Текст **#pragma** должны располагаться в начале каждой записи в файл.  
  -   Параметр *удалить* указывает, что действительно необходимо удалить событие настройки ловушки.  
  -   Параметры *ФайлЖурналаСобытий*, *EventSource*, и *EventID* являются обязательными. Параметр *ФайлЖурналаСобытий* задает журнал, в который записывается событие. Параметр *EventSource* задает приложение, которое создает событие. *EventID* параметр указывает уникальный номер, определяющий каждое событие.  
- Настройка назначения ловушки синтаксис выглядит следующим образом:  
  **#pragma add_TRAP_DEST**<em><CommunityName> <HostID></em>  
  -   Текст **#pragma** должны располагаться в начале каждой записи в файл.  
  -   Параметр **add_TRAP_DEST** указывает, следует ли ловушки сообщения должны отправляться на конкретный узел внутри сообщества.  
  -   Параметр *ИмяСообщества* задает имя, сообщество, в какие ловушки отправляются сообщения.  
  -   Параметр *HostID* указывает, что по имени или IP-адрес узла, на который необходимо отправлять сообщения ловушки.  
- Удаление назначения ловушки синтаксис выглядит следующим образом:  
  **#pragma delete_TRAP_DEST**<em><CommunityName> <HostID></em>  
  - Текст **#pragma** должны располагаться в начале каждой записи в файл.  
  - Параметр *delete_TRAP_DEST* указывает, что нежелательно ловушки сообщения должны отправляться на конкретный узел внутри сообщества.  
  - Параметр *ИмяСообщества* задает имя, сообщество, в какие ловушки отправляются сообщения.  
  - Параметр *HostID* указывает, что по имени или IP-адрес узла, к которому требуется отправлять сообщения ловушки.  
    ## <a name="BKMK_Examples"></a>Примеры  
    В следующих примерах показаны записи в файле конфигурации для **evntcmd** команды. Они не предназначены для вводиться в командной строке.  
    Чтобы отправить сообщение ловушки при перезапуске службы журнала событий, введите:  
    ```  
    #pragma add System "Eventlog" 2147489653  
    ```  
    Чтобы отправить сообщение ловушки при перезапуске службы журнала событий, два раза в три минуты, введите:  
    ```  
    #pragma add System "Eventlog" 2147489653 2 180  
    ```  
    Чтобы остановить отправку сообщения ловушки, при каждом перезапуске службы журнала событий, введите:  
    ```  
    #pragma delete System "Eventlog" 2147489653  
    ```  
    Чтобы отправить сообщения ловушки в сообщество с названием Public для узла с IP-адресом 192.168.100.100, введите:  
    ```  
    #pragma add_TRAP_DEST public 192.168.100.100  
    ```  
    Чтобы отправить сообщения ловушки в сообществе, с именем "Private" на узел с именем Host1, введите:  
    ```  
    #pragma add_TRAP_DEST private Host1  
    ```  
    Чтобы остановить отправку ловушки в сообществе, с именем "Private" на том же компьютере, на котором вы настраиваете ловушки, введите:  
    ```  
    #pragma delete_TRAP_DEST private localhost  
    ```  
    ## <a name="additional-references"></a>Дополнительные ссылки  
- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)  