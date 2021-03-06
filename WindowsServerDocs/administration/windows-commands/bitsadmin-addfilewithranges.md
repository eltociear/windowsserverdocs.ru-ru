---
title: bitsadmin addfilewithranges
description: Справочный раздел по команде битсадмин аддфилевисранжес, который добавляет файл к указанному заданию. Служба BITS загружает указанные диапазоны из удаленного файла.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: df0ce0bf-dff1-4a48-a16f-fd2f4d5f7189
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4b878b4f48441808bf971c051397d3af9bd975fe
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/01/2020
ms.locfileid: "82718470"
---
# <a name="bitsadmin-addfilewithranges"></a>bitsadmin addfilewithranges

Добавляет файл в указанное задание. Служба BITS загружает указанные диапазоны из удаленного файла. Этот параметр допустим только для заданий скачивания.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /addfilewithranges <job> <remoteURL> <localname> <rangelist>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| задание | Отображаемое имя задания или идентификатор GUID. |
| ремотеурл | URL-адрес файла на сервере. |
| localname | Имя файла на локальном компьютере. Должен содержать абсолютный путь к файлу. |
| ранжелист | Разделенный запятыми список пар "смещение: длина". Используйте двоеточие, чтобы разделить значение смещения от значения длины. Например, значение `0:100,2000:100,5000:eof` указывает, что бит передает 100 байт со смещения 0, 100 байт из смещения 2000, а остальные байт от смещения 5000 до конца файла. |

## <a name="remarks"></a>Примечания

- Токен **EOF** — это допустимое значение длины в пределах пар смещения и длины в `<rangelist>`. Он указывает службе выполнить чтение до конца указанного файла.

- `addfilewithranges` Команда завершится ошибкой с кодом ошибки 0x8020002c, если диапазон нулевой длины указан вместе с другим диапазоном с тем же смещением, например:

    `c:\bits>bitsadmin /addfilewithranges j2 http://bitsdc/dload/1k.zip c:\1k.zip 100:0,100:5`

    **Сообщение об ошибке:** Не удалось добавить файл в задание — 0x8020002c. Список диапазонов байтов содержит несколько перекрывающихся диапазонов, которые не поддерживаются.

    **Обходной путь:** Сначала не указывайте диапазон нулевой длины. Например, используйте`bitsadmin /addfilewithranges j2 http://bitsdc/dload/1k.zip c:\1k.zip 100:5,100:0`

## <a name="examples"></a>Примеры

Для перемещения 100 байт со смещения 0, 100 байт с offset 2000 и оставшихся байтов от смещения 5000 до конца файла:

```
bitsadmin /addfilewithranges http://downloadsrv/10mb.zip c:\10mb.zip 0:100,2000:100,5000:eof
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
