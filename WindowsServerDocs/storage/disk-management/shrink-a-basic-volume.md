---
title: Сжатие базового тома
description: В этой статье описывается, как сжать базовый том
ms.date: 06/07/2019
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 9073632a656f512bdb49ebe4eeefd4cd5f4eaadf
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/07/2019
ms.locfileid: "66812529"
---
# <a name="shrink-a-basic-volume"></a>Сжатие базового тома

> **Область применения:** Windows 10, Windows 8.1, Windows Server (полугодовой канал), Windows Server 2019 г., Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Объем существующих основных разделов и логических дисков можно уменьшить, выполнив для них операцию сжатия, перемещающую файлы в соседнюю, нефрагментированную область того же диска. Например, если возникает потребность в дополнительном разделе, но дополнительных дисков нет, можно сжать существующий раздел со стороны конца тома, чтобы создать незанятое пространство, которое можно использовать для нового раздела. Операция сжатия может быть заблокирована наличием определенных типов файлов. Дополнительные сведения см. в разделе [Дополнительные замечания](#additional-considerations) 

При сжатии раздела все обычные файлы автоматически перемещаются на диск для формирования нового незанятного пространства. Для сжатия тома повторно форматировать диск не нужно.

> [!CAUTION]
> Если раздел является необработанным (то есть не отформатирован в какой-либо файловой системе) и содержит данные (например, файл базы данных), сжатие раздела может привести к уничтожению этих данных.

## <a name="shrinking-a-basic-volume"></a>Сжатие базового тома

> [!NOTE]
> Для выполнения следующих шагов необходимо как минимум состоять в группе **Операторы архива** или **Администраторы**.

#### <a name="to-shrink-a-basic-volume-using-the-windows-interface"></a>Процедура сжатия базового тома с помощью интерфейса Windows

1.  В диспетчере дисков щелкните правой кнопкой мыши том, который требуется сжать.

2.  Выберите пункт **Сжать том**.

3.  Следуйте инструкциям на экране.


> [!NOTE]
> Сжать можно только те базовые тома, у которых нет файловой системы или которые отформатированы в файловой системе NTFS.

#### <a name="to-shrink-a-basic-volume-using-a-command-line"></a>Процедура сжатия базового тома с помощью командной строки

1.  Откройте командную строку и введите: `diskpart`.

2.  В командной строке **DISKPART** введите `list volume`. Запомните номер простого тома, который требуется сжать.

3.  В командной строке **DISKPART** введите `select volume <volumenumber>`. Выбирает простой том *volumenumber*, который требуется сжать.

4.  В командной строке **DISKPART** введите `shrink [desired=<desiredsize>] [minimum=<minimumsize>]`. Сжимает выбранный том до размера *desiredsize* в мегабайтах (МБ), если возможно, или до размера *minimumsize*, если размер *desiredsize* слишком велик.

| Значение             | Описание |
| ---               | ----------- |
| **Список томов** | Отображает список базовых и динамических томов на всех дисках. |
| **Выберите том** | Выбирает указанный том, где <em>volumenumber</em> — номер тома, и переводит на него фокус. Если том не указан, команда **select** отображает текущий том с фокусом. Для указания тома можно использовать номер, букву диска или путь к точке подключения. При выборе тома на базовом диске фокус переводится на соответствующий раздел. |
| **Сжатие** | Сжимает том с фокусом для создания нераспределенного пространства. Все данные остаются в сохранности. Если раздел содержит неперемещаемые файлы (например, файл подкачки или область хранения теневых копий), том сожмется до того места, в котором расположены эти файлы. |
| **требуемый =** <em>желаемый размер</em> | Объем пространства в мегабайтах, который требуется восстановить в текущем разделе. |
| **Минимальное =** <em>minimumsize</em> | Минимальный объем пространства в мегабайтах, который требуется восстановить в текущем разделе. Если не указать желаемый или минимальный размеры, команда освободит максимально возможное пространство. |

## <a name="additional-considerations"></a>Дополнительные рекомендации

-   При сжатии раздела определенные файлы (например, файл подкачки или область хранения теневых копий) невозможно переместить автоматически, а также невозможно сократить распределенное пространство дальше того места, в котором расположены неперемещаемые файлы. Если операция сжатия завершается сбоем, проверьте журнал приложений на наличие события 259, которое определит неперемещаемый файл. Если вам известно, какие кластеры, связанные с файлом, мешают операции сжатия, можно использовать команду **fsutil** в командной строке (введите **fsutil volume querycluster /?** для использования). Если предоставить параметр **querycluster**, в выходных данных команды будет указан неперемещаемый файл, мешающий выполнить операцию сжатия.
В некоторых случаях этот файл можно переместить временно. Например, если требуется еще сильнее сжать раздел, можно использовать панель управления, чтобы переместить файл подкачки или сохраненные теневые копии на другой диск, удалить сохраненные теневые копии, сжать том, а затем переместить файл подкачки обратно на диск. Если число поврежденных кластеров, обнаруженных при динамическом сопоставлении поврежденных кластеров, слишком велико, сжать раздел не удастся. В этом случае следует переместить данные и заменить диск.

-  Не используйте копию уровня блоков для переноса данных. При этом будет также скопирована таблица поверженных секторов, и новый диск будет считать эти секторы поврежденными, хотя на самом деле они будут исправными.

-   Можно сжать основные разделы и логические диски в необработанных разделах (не отформатированных в какой-либо файловой системе) или разделах, отформатированных в файловой системе NTFS.

## <a name="see-also"></a>См. также

-   [Управление базовыми томами](manage-basic-volumes.md)