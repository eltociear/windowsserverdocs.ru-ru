---
title: add
description: Справочный раздел по команде Add, который добавляет тома в набор томов, предназначенных для теневого копирования, или добавляет псевдонимы в среду псевдонима.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 47efce7a-86d2-4872-ae31-baa108757afd
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9b621a3061c4e3366085c5cc44f91f26dd33d4e3
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/01/2020
ms.locfileid: "82719005"
---
# <a name="add"></a>add

Добавляет тома в набор томов, которые должны быть теневыми копиями, или добавляет псевдонимы в среду псевдонима. Если используется без подкоманд, **добавьте** список текущих томов и псевдонимов.

> [!NOTE]
> Псевдонимы не добавляются в среду псевдонима до тех пор, пока не будет создана теневая копия. Псевдонимы, которые необходимо выполнить немедленно, следует добавлять с помощью команды **Добавить псевдоним**.

## <a name="syntax"></a>Синтаксис

```
add
add volume <volume> [provider <providerid>]
add alias <aliasname> <aliasvalue>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| ---------- | ----------- |
| том | Добавляет том в набор теневых копий, который представляет собой набор томов, предназначенных для теневого копирования. См. раздел [Добавление тома](add-volume.md) для синтаксиса и параметров. |
| alias | Добавляет заданное имя и значение в среду псевдонима. Синтаксис и параметры см. в разделе [Добавление псевдонима](add-alias.md) . |
| /? | Отображает справку в командной строке. |

## <a name="examples"></a>Примеры

Чтобы отобразить добавленные тома и псевдонимы, которые в настоящее время находятся в среде, введите:

```
add
```

Следующие выходные данные показывают, что диск C добавлен в набор теневых копий:

```
Volume c: alias System1    GUID \\?\Volume{XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX}\
1 volume in Shadow Copy Set.
No Diskshadow aliases in the environment.
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)