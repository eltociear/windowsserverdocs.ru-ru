---
title: ping
description: Команду ping для проверки сетевых подключений.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 49272671-2eec-4fa5-881f-65c24cfbef52
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: 1ac02a148061cd6eb8480c67f15e934f5fd57768
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2019
ms.locfileid: "59816755"
---
# <a name="ping"></a>ping

>Область применения. Windows Server (полугодовой канал), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

**Ping** команда проверяет возможность подключения на уровне IP-адрес к другому компьютеру TCP/IP путем отправки сообщения запроса проверки связи Internet Control Message Protocol (ICMP). Получение соответствующего echo ответного сообщения, а также время кругового пути. ping — это основной TCP/IP-команда, используемая для устранения неполадок подключения, достижимость и разрешение имен. При использовании без параметров, **ping** отображает справку.

## <a name="syntax"></a>Синтаксис

```
ping [/t] [/a] [/n <Count>] [/l <Size>] [/f] [/I <TTL>] [/v <TOS>] [/r <Count>] [/s <Count>] [{/j <Hostlist> | /k <Hostlist>}] [/w <timeout>] [/R] [/S <Srcaddr>] [/4] [/6] <TargetName>
```

### <a name="parameters"></a>Параметры

|Параметр|Описание|
|-------|--------|
|/t|Задает для команды ping отправки сообщения запроса проверки связи в место назначения до прерывания. Для прерываний и отображения статистики, нажмите клавиши CTRL + break. Для прерывания и выйти из программы **ping**, нажмите клавиши CTRL + C.|
|/a|Указывает, что обратное разрешение имен выполняется на IP-адрес назначения. Если это удалось, выводится имя соответствующего узла.|
|/n \<Count\>|Указывает количество echo отправляются сообщения запросов. Значение по умолчанию — 4.|
|/l \<размер\>|Задает длину в байтах, поля данных в echo запрос сообщения, отправленные. Значение по умолчанию — 32. Максимальный размер — 65527.|
|/f|Указывает, которые повторяют сообщения запроса отправляются с Do не фрагментировать флаг в значение 1 (доступно только в IPv4) IP-заголовке. Echo сообщение запроса невозможность фрагментировать маршрутизаторами в пути к назначению. Этот параметр полезен для устранения неполадок, связанных с Максимальная Единица передачи данных (PMTU) путь.|
|/I \<TTL\>|Задает значение поля TTL в заголовке IP-адрес для проверки связи сообщений, отправленных запросов. Значение по умолчанию является значение срока ЖИЗНИ по умолчанию для узла. Максимально *TTL* составляет 255.|
|/v \<и инструкции\>|Указывает значение типа поля Service (TOS) в IP-заголовке для echo запрос сообщения, отправленные (доступно только в IPv4). Значение по умолчанию — 0. *TOS* указывается как десятичное значение от 0 до 255.|
|/r \<Count\>|Указывает, что параметр записи маршрута в заголовке IP-адрес используется для записи путь, по на экран сообщение запроса и соответствующего сообщения ответа (доступно только в IPv4), проверки в связи. Каждый переход в пути использует параметр записи маршрута. По возможности указывайте *число* , равным или больше, чем количество прыжков между источником и назначением. *Число* должно быть значение от 1 до 9.|
|/s \<Count\>|Указывает, что параметр "timestamp" Internet "в заголовке IP-адрес используется для записи времени прибытия сообщения запроса проверки связи и соответствующего сообщения ответа для каждого прыжка, проверки связи. *Число* должно быть от 1 до максимум 4. Это необходимо для локальных адресов.|
|/j \<Hostlist\>|Указывает, что в IP-заголовке с набором промежуточных мест назначения, указанный в диалоговом окне echo использование сообщений запроса свободной маршрутизации *Hostlist* (доступно только в IPv4). При свободной маршрутизации последовательные промежуточные места назначения могут быть разделены одним или несколькими маршрутизаторами. Максимальное число адресов или имен в списке узлов равно 9. Список узлов — это последовательность IP-адресов (в точечно-десятичной нотации), разделенных пробелами.|
|/k \<Hostlist\>|Указывает, что в IP-заголовке с набором промежуточных мест назначения, указанный в диалоговом окне echo использование сообщений запроса строгой маршрутизации *Hostlist* (доступно только в IPv4). При строгой маршрутизации, далее промежуточного назначения можно получить напрямую (должен быть соседней в интерфейсе маршрутизатора). Максимальное число адресов или имен в списке узлов равно 9. Список узлов — это последовательность IP-адресов (в точечно-десятичной нотации), разделенных пробелами.|
|/w \<время ожидания\>|Указывает количество времени, в миллисекундах для ожидания echo ответное сообщение, соответствующее заданной echo сообщение запроса должно быть получено. Если echo ответное сообщение не получено в течение времени ожидания, отображается сообщение об ошибке» запроса «истекло время ожидания. Время ожидания по умолчанию — 4000 (4 секунды).|
|/R|Указывает, что пути, это событие регистрируется (доступно только в IPv6).|
|/S \<Srcaddr\>|Указывает адрес источника (доступно только в IPv6).|
|/4|Указывает, что IPv4 используется для проверки связи. Этот параметр не требуется для идентификации целевого узла с адресом IPv4. Она необходима только для идентификации конечного узла по имени.|
|/6|Указывает, что IPv6 используется для проверки связи. Этот параметр не требуется для идентификации конечного узла с адресом IPv6. Она необходима только для идентификации конечного узла по имени.|
|\<TargetName\>|Указывает имя узла или IP-адрес назначения.|
|/?|Отображение справки в командной строке.|

## <a name="remarks"></a>Примечания

-   Можно использовать **ping** проверяемое имя компьютера и IP-адрес компьютера. Если проверка связи IP-адрес успешно, но не проверка имени, возможно, проблема с разрешением имени. В этом случае убедитесь, что имя компьютера, который вы указываете было разрешено в локальный файл Hosts, с помощью запросов доменных имен (DNS), или посредством NetBIOS методов разрешения имен.
-   Эта команда доступна только в том случае, если протокол Интернета (TCP/IP) устанавливается как компонент в свойствах сетевого адаптера в сетевых подключений.

## <a name="BKMK_Examples"></a>Примеры

В следующем примере показан **ping** выходные данные команды:

```
C:\>ping example.microsoft.com       
         pinging example.microsoft.com [192.168.239.132] with 32 bytes of data:       
         Reply from 192.168.239.132: bytes=32 time=101ms TTL=124       
         Reply from 192.168.239.132: bytes=32 time=100ms TTL=124       
         Reply from 192.168.239.132: bytes=32 time=120ms TTL=124       
         Reply from 192.168.239.132: bytes=32 time=120ms TTL=124
```

Для назначения 10.0.99.221 и разрешения 10.0.99.221 для имени узла, введите следующую команду:

```
ping /a 10.0.99.221
```

Для назначения 10.0.99.221 с 10 эхо-сообщения запроса, каждый из которых имеет поле данных из 1000 байт, введите следующую команду:

```
ping /n 10 /l 1000 10.0.99.221
```

Для назначения 10.0.99.221 и записи маршрута для 4 переходов, введите следующую команду:

```
ping /r 4 10.0.99.221
```

Чтобы указать свободной маршрутизации для точек назначения 10.12.0.1-10.29.3.1-10.1.44.1 назначения 10.0.99.221, введите следующую команду:

```
ping /j 10.12.0.1 10.29.3.1 10.1.44.1 10.0.99.221
```

## <a name="additional-references"></a>Дополнительные ссылки
-   [Ключ синтаксиса командной строки](command-line-syntax-key.md)