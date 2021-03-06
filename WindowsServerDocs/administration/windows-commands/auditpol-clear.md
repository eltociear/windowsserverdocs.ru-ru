---
title: очистить Auditpol
description: Справочный раздел по команде auditpol Clear, который удаляет политику аудита для каждого пользователя для всех пользователей, сбрасывает (отключает) политику аудита системы для всех подкатегорий и устанавливает для всех параметров аудита значение отключено.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 05bfa218-2434-4ad1-b33c-e6fcfb2b4f67
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a3d4765907f1dd614f5d0a61585ea09069652ecb
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/01/2020
ms.locfileid: "82719150"
---
# <a name="auditpol-clear"></a>очистить Auditpol

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Удаляет политику аудита "на пользователя" для всех пользователей, сбрасывает (отключает) политику аудита системы для всех подкатегорий и устанавливает для всех параметров аудита значение "отключено".

Для выполнения *очистки* операций с политиками на *уровне пользователя* и *системы* необходимо иметь разрешение на **запись** или **полный** доступ для этого набора объектов в дескрипторе безопасности. Кроме того, вы можете выполнять *четкие* операции, если у вас есть права пользователя " **Управление аудитом и журналом безопасности** " (SeSecurityPrivilege). Однако это право предоставляет дополнительный доступ, ненеобходимый для выполнения общих операций *очистки* .

## <a name="syntax"></a>Синтаксис

```
auditpol /clear [/y]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| ----------- | --------------- |
| /y | Подавляет запрос на подтверждение очистки всех параметров политики аудита. |
| /? | Отображение справки в командной строке. |

## <a name="examples"></a>Примеры

Чтобы удалить политику аудита для каждого пользователя для всех пользователей, сбросьте (отключите) политику аудита системы для всех подкатегорий и установите для всех параметров политики аудита значение отключено, в окне подтверждения введите:

```
auditpol /clear
```

Чтобы удалить политику аудита для каждого пользователя для всех пользователей, сбросьте параметры политики аудита системы для всех подкатегорий и установите для всех параметров политики аудита значение отключено, без запроса подтверждения введите:

```
auditpol /clear /y
```

> [!NOTE]
> Предыдущий пример полезен при использовании скрипта для выполнения этой операции.

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [команды auditpol](auditpol.md)
