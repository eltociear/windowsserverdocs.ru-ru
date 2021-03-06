---
title: Добавить том
description: Справочный раздел по команде "добавить том", который добавляет тома в набор теневых копий, который представляет собой набор томов для теневого копирования.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: b7d4d35d-8bda-46d2-8df5-eb598cecaaba
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a8cfd3d8f7d9f008e3136d8f694dc00370b8b0f2
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/01/2020
ms.locfileid: "82719209"
---
# <a name="add-volume"></a>Добавить том

Добавляет тома в набор теневых копий, который представляет собой набор томов для теневого копирования. При создании теневой копии переменная среды связывает псевдоним с идентификатором теневого номера, поэтому псевдоним можно использовать для создания скриптов.

Тома добавляются по одному за раз. При каждом добавлении тома проверяется, поддерживает ли VSS создание теневых копий для этого тома. Эта проверка может быть недействительной при последующем использовании команды **Set context** .

Эта команда необходима для создания теневых копий. Если используется без параметров, команда **Добавить том** отображает справку в командной строке.

## <a name="syntax"></a>Синтаксис

```
add volume <volume> [provider <providerid>]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| `<volume>` | Указывает том, добавляемый в набор теневых копий. Для создания теневой копии требуется по крайней мере один том. |
| `[provider \<providerid>]` | Указывает идентификатор поставщика для зарегистрированного поставщика, который будет использоваться для создания теневой копии. Если **поставщик** не указан, используется поставщик по умолчанию. |

## <a name="examples"></a>Примеры

Чтобы просмотреть текущий список зарегистрированных поставщиков, в `diskshadow>` командной строке введите:

```
list providers
```

В следующем выводе отображается один поставщик, который будет использоваться по умолчанию:

```
* ProviderID: {b5946137-7b9f-4925-af80-51abd60b20d5}
        Type: [1] VSS_PROV_SYSTEM
        Name: Microsoft Software Shadow Copy provider 1.0
        Version: 1.0.0.7
        CLSID: {65ee1dba-8ff4-4a58-ac1c-3470ee2f376a}
1 provider registered.
```

Чтобы добавить диск C: в набор теневых копий и назначить псевдоним с именем *System1*, введите:

```
add volume c: alias System1
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [команда Set context](set-context.md)
