---
title: extract
description: Справочный раздел по команде Extract, который извлекает файлы из исходного расположения.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 20dab03e-f6e1-4eb8-b8a1-fd6f1d97ee83
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: dbadcc555fc9bb0b02e568b1126a317a9d59d336
ms.sourcegitcommit: bf887504703337f8ad685d778124f65fe8c3dc13
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/16/2020
ms.locfileid: "83437189"
---
# <a name="extract"></a>extract

Извлекает файлы из CAB-файла или из источника.

## <a name="syntax"></a>Синтаксис

```
extract [/y] [/a] [/d | /e] [/l dir] cabinet [filename ...]
extract [/y] source [newname]
extract [/y] /c source destination
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| файле | Используйте, если требуется извлечь два или более файлов. |
| filename | Имя файла, извлекаемого из CAB-архива. Можно использовать подстановочные знаки и несколько имен файлов (разделенные пробелами). |
| источник | Сжатый файл (CAB-файл с одним файлом). |
| newname | Новое имя файла, чтобы получить извлеченный файл. Если значение не указано, используется исходное имя. |
| /a | Обработка всех ящиков. Ниже приведена цепочка CAB-файлов, начиная с первого указанного CAB-файла. |
| /C | Копировать исходный файл в место назначения (для копирования с дисков DMF). |
| /d | Откройте каталог CAB-файлов (используйте с именем filename, чтобы избежать извлечения). |
| /e | Extract (используйте вместо *.* для извлечения всех файлов). |
| /l dir | Расположение для размещения извлеченных файлов (по умолчанию текущий каталог). |
| /y | Не выдавать запрос перед перезаписыванием существующего файла. |

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
