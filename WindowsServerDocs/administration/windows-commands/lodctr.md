---
title: lodctr
description: Справочный раздел о команде lodctr, которая позволяет зарегистрировать или сохранить имя счетчика производительности и параметры реестра в файле и назначить Доверенные службы.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5a849abd-6b31-4833-bc8a-306c05eca29a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 221737d68280dabf34c270fccff02071ebf9b5a2
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/24/2020
ms.locfileid: "83820184"
---
# <a name="lodctr"></a>lodctr

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Позволяет зарегистрировать или сохранить имя счетчика производительности и параметры реестра в файле и назначить Доверенные службы.

## <a name="syntax"></a>Синтаксис

```
lodctr <filename> [/s:<filename>] [/r:<filename>] [/t:<servicename>]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| `<filename>` | Задает имя файла инициализации, который регистрирует параметры имени счетчика производительности и пояснительный текст. |
| ключ`<filename>` | Задает имя файла, в котором сохраняются параметры реестра счетчика производительности и пояснительный текст. |
| /r | Восстанавливает параметры реестра счетчиков и пояснительный текст из текущих параметров реестра и кэшированных файлов производительности, связанных с реестром. |
| /r`<filename>` | Указывает имя файла, который восстанавливает параметры реестра счетчика производительности и пояснительный текст.<p>**Предупреждение:** При использовании этой команды будут перезаписаны все параметры реестра счетчиков производительности и пояснительный текст, заменяя их конфигурациями, определенными в указанном файле. |
| /t:`<servicename>` | Указывает, что служба `<servicename>` является доверенной. |
| /? | Отображение справки в командной строке. |

#### <a name="remarks"></a>Замечания

- Если предоставленные сведения содержат пробелы, заключите его в кавычки (например, "имя файла 1").

### <a name="examples"></a>Примеры

Чтобы сохранить текущие параметры реестра производительности и пояснительный текст к файлу *perf backup1. txt*, введите:

```
lodctr /s:perf backup1.txt
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
