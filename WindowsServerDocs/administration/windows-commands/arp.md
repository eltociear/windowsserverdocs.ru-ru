---
title: arp
description: Справочный раздел по команде ARP, которая отображает и изменяет записи в кэше ARP, который используется для хранения IP-адресов и их разрешенных физических адресов.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 827e96eb-1945-483f-980f-714703456f7c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: fdbb9fe636bb30be90164d9a2163c495a9c2e704
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/24/2020
ms.locfileid: "83819654"
---
# <a name="arp"></a>arp

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Отображает и изменяет записи в кэше протокола ARP. Кэш ARP содержит одну или несколько таблиц, которые используются для хранения IP-адресов и разрешенных физических адресов Ethernet или Token Ring. Для каждого сетевого адаптера Ethernet или Token Ring, установленного на компьютере, существует отдельная таблица. При использовании без параметров в **ARP** отображаются справочные сведения.

## <a name="syntax"></a>Синтаксис

```
arp [/a [<inetaddr>] [/n <ifaceaddr>]] [/g [<inetaddr>] [-n <ifaceaddr>]] [/d <inetaddr> [<ifaceaddr>]] [/s <inetaddr> <etheraddr> [<ifaceaddr>]]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| `[/a [<inetaddr>] [/n <ifaceaddr>]` | Отображает текущие таблицы кэша ARP для всех интерфейсов. Параметр **/n** учитывает регистр. Чтобы отобразить запись кэша ARP для определенного IP-адреса, используйте **ARP/a** с параметром **инетаддр** , где **инетаддр** — это IP-адрес. Если **инетаддр** не указан, используется первый подходящий интерфейс. Чтобы отобразить таблицу кэша ARP для определенного интерфейса, используйте параметр **/n ифацеаддр** в сочетании с параметром **/a** , где **инетаддр** — это IP-адрес, назначенный интерфейсу. |
| `[/g [<inetaddr>] [/n <ifaceaddr>]` | Идентично **/a**. |
| `[/d <inetaddr> [<ifaceaddr>]` | Удаляет запись с указанным IP-адресом, где **инетаддр** — это IP-адрес. Чтобы удалить запись в таблице для определенного интерфейса, используйте параметр **ифацеаддр** , где **ифацеаддр** — это IP-адрес, назначенный интерфейсу. Чтобы удалить все записи, используйте подстановочный знак звездочки (*) вместо **инетаддр**. |
| `[/s <inetaddr> <etheraddr> [<ifaceaddr>]` | Добавляет статическую запись в кэш ARP, которая разрешает IP-адрес **инетаддр** с физическим адресом **есераддр**. Чтобы добавить статическую запись кэша ARP в таблицу для определенного интерфейса, используйте параметр **ифацеаддр** , где **ифацеаддр** — это IP-адрес, назначенный интерфейсу. |
| /? | Отображение справки в командной строке. |

### <a name="remarks"></a>Замечания

- IP-адреса для **инетаддр** и **ифацеаддр** выражаются в десятичной нотации.

- Физический адрес для **есераддр** состоит из шести байт, выраженных в шестнадцатеричной нотации и разделенных дефисами (например, 00-AA-00-4F-2A-9C).

- Записи, добавленные с параметром **/s** , являются статическими и не выходят за пределы времени ожидания кэша ARP. Записи удаляются, если протокол TCP/IP остановлен и запущен. Чтобы создать постоянные статические записи кэша ARP, поместите соответствующие команды **ARP** в пакетный файл и используйте запланированные задания для запуска пакетного файла при запуске.

## <a name="examples"></a>Примеры

Чтобы отобразить таблицы кэша ARP для всех интерфейсов, введите:

```
arp /a
```

Чтобы отобразить таблицу кэша ARP для интерфейса, которому назначен IP-адрес *10.0.0.99*, введите:

```
arp /a /n 10.0.0.99
```

Чтобы добавить статическую запись кэша ARP, которая разрешает IP-адрес *10.0.0.80* к физическому адресу *00-AA-00-4F-2A-9C*, введите:

```
arp /s 10.0.0.80 00-AA-00-4F-2A-9C
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
