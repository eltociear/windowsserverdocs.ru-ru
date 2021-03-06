---
title: bootcfg debug
description: Справочный раздел для команды bootcfg debug, которая добавляет или изменяет параметры отладки для указанной записи операционной системы.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 28afa5fb-a236-46e2-b1a4-a3c43a49c437
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c8059aaefd1b23b3e74f4c27ba96e322c44b5cb6
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/01/2020
ms.locfileid: "82709711"
---
# <a name="bootcfg-debug"></a>bootcfg debug

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Добавляет или изменяет параметры отладки для указанной записи операционной системы.

>[!NOTE]
> Если вы пытаетесь отладить порт 1394, используйте команду [bootcfg dbg1394](bootcfg-dbg1394.md) .

## <a name="syntax"></a>Синтаксис

```
bootcfg /debug {on | off | edit}[/s <computer> [/u <domain>\<user> /p <password>]] [/port {COM1 | COM2 | COM3 | COM4}] [/baud {9600 | 19200 | 38400 | 57600 | 115200}] [/id <osentrylinenum>]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| `{on | off | edit}` | Указывает значение для отладки порта, включая:<ul><li>**on.** Включает поддержку удаленной отладки путем добавления параметра/Debug в указанный `<osentrylinenum>`.</li><li>**автоном.** Отключает поддержку удаленной отладки путем удаления параметра/Debug из указанного <osentrylinenum>.</li><li>**Редактор.** Позволяет изменять параметры порта и скорости передачи, изменяя значения, связанные с параметром/Debug для указанного <osentrylinenum>.</li></ul> |
| `/s <computer>` | Указывает имя или IP-адрес удаленного компьютера (не используйте обратную косую черту). По умолчанию используется локальный компьютер. |
| `/u <domain>\<user>`  | Выполняет команду с разрешениями учетной записи пользователя, указанного `<user>` в `<domain>\<user>`параметре или. По умолчанию заданы разрешения текущего вошедшего в систему пользователя на компьютере, выполняющем команду. |
| `/p <password>` | Указывает пароль учетной записи пользователя, указанной в параметре **/u** . |
| `/port {COM1 | COM2 | COM3 | COM4}` |  Указывает COM-порт, используемый для отладки. Не используйте этот параметр, если отладка отключена. |
| `/baud {9600 | 19200 | 38400 | 57600 | 115200}` | Указывает скорость передачи, используемую для отладки. Не используйте этот параметр, если отладка отключена. |
| `/id <osentrylinenum>` | Указывает номер строки записи операционной системы в разделе [Operating Systems] файла Boot. ini, в который добавляются параметры загрузки операционной системы. Первая строка после заголовка раздела [Operating Systems] — 1. |
| /? | Отображение справки в командной строке. |

## <a name="examples"></a>Примеры

Чтобы использовать команду **bootcfg/debug** , выполните следующие действия.

```
bootcfg /debug on /port com1 /id 2
bootcfg /debug edit /port com2 /baud 19200 /id 2
bootcfg /s srvmain /u maindom\hiropln /p p@ssW23 /debug off /id 2
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда bootcfg](bootcfg.md)
