---
title: irftp
description: Справочный раздел по команде ирфтп, который отправляет файлы по инфракрасной связи.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e15c60a7-546d-4e9f-9871-43aaa1b569d6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0d19e4f0c325baf46c0a92bf04e39bc63863fe90
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/24/2020
ms.locfileid: "83818314"
---
# <a name="irftp"></a>irftp

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Отправляет файлы по инфракрасной связи.

> [!IMPORTANT]
> Убедитесь, что устройства, предназначенные для связи по инфракрасной связи, имеют включенные функции инфракрасной связи и работают правильно. Кроме того, убедитесь, что между устройствами установлена связь по инфракрасной связи.

## <a name="syntax"></a>Синтаксис

```
irftp [<drive>:\] [[<path>] <filename>] [/h][/s]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| `<drive>:\` | Указывает диск, содержащий файлы, которые необходимо отправить через инфракрасную связь. |
| `[path]<filename>` | Указывает расположение и имя файла или набора файлов, которые требуется отправить через инфракрасную связь. Если указать набор файлов, необходимо указать полный путь для каждого файла. |
| /h | Указывает скрытый режим. Если используется скрытый режим, файлы отправляются без отображения диалогового окна беспроводная связь. |
| /s | Открывает диалоговое окно **беспроводная связь** , позволяющее выбрать файл или набор файлов, которые требуется отправить, без использования командной строки для указания диска, пути и имен файлов. Диалоговое окно **беспроводная связь** также открывается при использовании этой команды без параметров. |

### <a name="examples"></a>Примеры

Чтобы отправить *к:\ексампле.ткст* через инфракрасную связь, введите:

```
irftp c:\example.txt
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
