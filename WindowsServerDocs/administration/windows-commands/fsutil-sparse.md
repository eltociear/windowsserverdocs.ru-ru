---
title: fsutil sparse
description: Справочный раздел, посвященный команде fsutil sparse, которая управляет разреженными файлами.
ms.prod: windows-server
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
ms.assetid: 77545920-2d13-4f35-a4d1-14dbec8340dc
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: e68ac844bb7aa7e22a9df0ddb0c982b3701231d7
ms.sourcegitcommit: bf887504703337f8ad685d778124f65fe8c3dc13
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/16/2020
ms.locfileid: "83435719"
---
# <a name="fsutil-sparse"></a>fsutil sparse

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8

Управляет разреженными файлами. Разреженный файл — это файл с одним или несколькими регионами нераспределенных данных.

Программа видит эти Нераспределенные регионы как содержащие байты с нулевым значением и не имеет места на диске, представляющего эти нули. При чтении разреженного файла выделенные данные возвращаются в виде сохраненных данных, а нераспределенные данные по умолчанию возвращаются в виде нулей в соответствии со спецификацией требования безопасности C2. Поддержка разреженных файлов позволяет освободить данные из любого места в файле.

## <a name="syntax"></a>Синтаксис

```
fsutil sparse [queryflag] <filename>
fsutil sparse [queryrange] <filename>
fsutil sparse [setflag] <filename>
fsutil sparse [setrange] <filename> <beginningoffset> <length>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| куерифлаг | Разреженные запросы. |
| куериранже | Сканирует файл и ищет диапазоны, которые могут содержать ненулевые данные. |
| setflag | Помечает указанный файл как разреженный. |
| SetRange | Заполняет указанный диапазон файла нулями. |
| `<filename>` | Указывает полный путь к файлу, включая имя файла и расширение, например *к:\документс\филенаме.ткст*. |
| `<beginningoffset>` | Задает смещение в файле для пометки как разреженного. |
| `<length>` | Указывает длину области в файле, которая будет помечена как разреженная (в байтах). |

#### <a name="remarks"></a>Комментарии

- Все осмысленные или ненулевые данные выделяются, а все незначимые данные (большие строки данных, состоящие из нулей) не выделяются.

- В разреженном файле большие диапазоны нулей могут не требовать выделения места на диске. При написании файла выделяется пространство для ненулевых данных.

- Только сжатые или разреженные файлы могут иметь нулевые диапазоны, известные операционной системе.

- Если файл Разреженный или сжатый, NTFS может отменить выделение дискового пространства в файле. Этот параметр задает для диапазона байтов нулевое значение без увеличения размера файла.

### <a name="examples"></a>Примеры

Чтобы пометить файл с именем *Sample. txt* в каталоге *c:\temp* как разреженный, введите:

```
fsutil sparse setflag c:\temp\sample.txt
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [fsutil](fsutil.md)
