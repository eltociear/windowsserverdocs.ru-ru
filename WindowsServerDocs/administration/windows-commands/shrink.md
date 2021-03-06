---
title: shrink
description: Справочный раздел по сжатию файла DiskPart, который уменьшает размер выбранного тома на указанный вами объем.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ec87cc7c-9846-465e-a10d-4ee10db4f4e6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 357a2320bf8b26130c9aa148d513edff6f1e85db
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/01/2020
ms.locfileid: "82721803"
---
# <a name="shrink"></a>shrink

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Команда DiskPart Shrink уменьшает размер выбранного тома на указанный вами объем. Эта команда освобождает свободное место на диске, доступное по неиспользуемому пространству в конце тома.

## <a name="syntax"></a>Синтаксис
```
shrink [desired=<n>] [minimum=<n>] [nowait] [noerr]
shrink querymax [noerr]
```
### <a name="parameters"></a>Параметры

|  Параметр  |                                                                                             Описание                                                                                              |
|-------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| требуется =<n> |                                                     Указывает требуемый объем пространства в мегабайтах (МБ) для уменьшения размера тома.                                                     |
| минимум =<n> |                                                           Указывает минимальный объем пространства в МБ, по истечение которого уменьшается размер тома.                                                           |
|  querymax   |                       Возвращает максимальный объем пространства в МБ, на который может быть уменьшен размер тома. Это значение может измениться, если приложения в данный момент обращаются к тому.                        |
|   nowait    |                                                       принудительно Возвращает команду, пока процесс сжатия все еще выполняется.                                                        |
|    Noerr    | только для сценариев. При возникновении ошибки DiskPart продолжит обрабатывать команды, как если бы ошибка не возникала. Без этого параметра ошибка приводит к выходу из программы DiskPart с кодом ошибки. |

## <a name="remarks"></a>Примечания
- Размер тома можно уменьшить только в том случае, если он отформатирован с помощью файловой системы NTFS или если у него нет файловой системы.
- Эта команда работает с базовыми томами, а также с простыми или составными динамическими томами.
- Если требуемая величина не указана, объем тома будет уменьшен на минимальный (если он указан).
- Если минимальная сумма не указана, объем тома будет уменьшен на требуемый объем (если он указан).
- Если не указать ни минимальную сумму, ни требуемую величину, том будет сокращен с учетом того, насколько это возможно.
- Если минимальная сумма указана, но недостаточно свободного места, команда завершится ошибкой.
- Для выполнения этой операции необходимо выбрать том. Используйте команду **выбрать том** , чтобы выбрать том и переместить фокус на него.
- Эта команда не работает с разделами изготовителя оборудования (OEM), системными разделами расширяемого микропрограммного обеспечения (EFI) или разделами восстановления.
  ## <a name="examples"></a>Примеры
  Чтобы уменьшить размер выбранного тома на максимально возможное число от 250 до 500 МБ, введите:
  ```
  shrink desired=500 minimum=250
  ```
  Чтобы отобразить максимальное количество МБ, которое может быть сокращено для тома, введите:
  ```
  shrink querymax
  ```

[Resize-Partition](https://technet.microsoft.com/library/hh848680.aspx)
