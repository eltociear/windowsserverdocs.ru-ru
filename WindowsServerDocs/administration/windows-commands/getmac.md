---
title: getmac
description: Справочный раздел по команде жетмак, который возвращает MAC-адрес и список сетевых протоколов, связанных с каждым, локально или по сети.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: a749a348-7cd1-4336-9f33-bb42dd0e31e1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b84218b5506770bbefd5af8c89801547cc658f88
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/24/2020
ms.locfileid: "83819094"
---
# <a name="getmac"></a>getmac

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Возвращает MAC-адрес и список сетевых протоколов, связанных с каждым адресом для всех сетевых карт на каждом компьютере (локально или по сети). Эта команда особенно полезна, если требуется ввести MAC-адрес в анализатор сети или если необходимо знать, какие протоколы используются на каждом сетевом адаптере компьютера.

## <a name="syntax"></a>Синтаксис

```
getmac[.exe][/s <computer> [/u <domain\<user> [/p <password>]]][/fo {table | list | csv}][/nh][/v]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- |------------ |
| ключ`<computer>` | Указывает имя или IP-адрес удаленного компьютера (не используйте символы обратной косой черты). По умолчанию используется локальный компьютер. |
| /u`<domain>\<user>` | Выполняет команду с разрешениями учетной записи пользователя, указанного *пользователем* или *домен \*пользователь. По умолчанию заданы разрешения текущего вошедшего в систему пользователя на компьютере, выполняющем команду. |
| /p`<password>` | Указывает пароль учетной записи пользователя, указанной в параметре **/u** . |
| /FO {таблица | list | - | Указывает формат, используемый для вывода запроса. Допустимые значения: **Table**, **List**и **CSV**. Формат выходных данных по умолчанию — **Table**. |
| использован | Подавляет вывод заголовка столбца в выходных данных. Допустим, если для параметра **/FO** задано значение **Table** или **CSV**. |
| /v | Указывает, что выходные данные отображают подробные сведения. |
| /? | Отображение справки в командной строке. |

### <a name="examples"></a>Примеры

В следующих примерах показано, как можно использовать команду **жетмак** :

```
getmac /fo table /nh /v
```

```
getmac /s srvmain
```

```
getmac /s srvmain /u maindom\hiropln
```

```
getmac /s srvmain /u maindom\hiropln /p p@ssW23
```

```
getmac /s srvmain /u maindom\hiropln /p p@ssW23 /fo list /v
```

```
getmac /s srvmain /u maindom\hiropln /p p@ssW23 /fo table /nh
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
