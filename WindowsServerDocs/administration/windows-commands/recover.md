---
title: recover
description: Справочный раздел по * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: cf9be2e3-90c8-4773-a201-dc503b91948e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b316ed26f008a62f88aaeb4a7a7f3030d08f1588
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/01/2020
ms.locfileid: "82722617"
---
# <a name="recover"></a>recover



Восстанавливает данные, доступные для чтения, с поврежденного или дефектного диска.



## <a name="syntax"></a>Синтаксис

```
recover [<Drive>:][<Path>]<FileName>
```

### <a name="parameters"></a>Параметры

|           Параметр           |                                          Описание                                          |
|-------------------------------|-----------------------------------------------------------------------------------------------|
| [\<Диск>:] [<Path>]<FileName> | Указывает расположение и имя файла, который требуется восстановить. Требуется *имя файла* . |
|              /?               |                             Отображение справки в командной строке.                              |

## <a name="remarks"></a>Примечания

-   Команда **восстановления** считывает файл, сектор на сектор и восстанавливает данные из хороших секторов. Данные в поврежденных секторах теряются.
-   Если диск был подготовлен к работе, поврежденные секторы, о которых сообщила **программа chkdsk** , были помечены как ошибочные. Они не представляют опасности, и **Восстановление** не влияет на них.
-   Так как все данные в поврежденных секторах теряются при восстановлении файла, следует восстановить только один файл за раз.
-   Нельзя использовать подстановочные знаки (**&#42;** и **?**) с командой **recover** . Необходимо указать файл (и расположение файла, если он не находится в текущем каталоге).

## <a name="examples"></a>Примеры

Чтобы восстановить файл истории. txt в каталоге \Фиктион на диске D, введите:
```
recover d:\fiction\story.txt 
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)