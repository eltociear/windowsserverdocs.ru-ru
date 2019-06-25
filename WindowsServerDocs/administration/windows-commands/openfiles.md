---
title: openfiles
description: 'Раздел Windows команды для ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c3be561d-a11f-4bf1-9835-8e4e96fe98ec
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0bec8cf64a3c7f261c792a07da603cba4366e1a7
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/31/2019
ms.locfileid: "66436436"
---
# <a name="openfiles"></a>openfiles



Позволяет администратору запрос, отобразить или отключить файлы и каталоги, которые были открыты в системе. Также включает или отключает системы глобального флага Построение списка объектов.

Этот раздел содержит сведения о следующих команд:
-   [Openfiles / disconnect](#BKMK_disconnect)
-   [Openfiles/Query](#BKMK_query)
-   [/ Local Openfiles](#BKMK_local)

## <a name="BKMK_disconnect"></a>Openfiles / disconnect

Позволяет администратору отключить файлы и папки, которые были открыты удаленно через общую папку.

### <a name="syntax"></a>Синтаксис

```
openfiles /disconnect [/s <System> [/u [<Domain>\]<UserName> [/p [<Password>]]]] {[/id <OpenFileID>] | [/a <AccessedBy>] | [/o {read | write | read/write}]} [/op <OpenFile>]
```

### <a name="parameters"></a>Параметры

|            Параметр             |                                                                                                                                 Описание                                                                                                                                  |
|----------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|           /s \<system >           | Указывает удаленный систему для подключения к (по имени или IP-адрес). Не используйте символы обратной косой черты. Если вы не используете **/s** параметр, команда по умолчанию будет выполняться на локальном компьютере. Этот параметр применяется ко всем файлам и папкам, которые указаны в команде. |
|    /u [\<домена >\]<UserName>     |                                                          Выполняет команду с разрешениями указанной учетной записи. Если вы не используете **/u** параметр системные разрешения используются по умолчанию.                                                           |
|         /p [\<пароль >]         |                                               Указывает пароль для учетной записи пользователя, который указан в **/u** параметр. Если вы не используете **/p** параметр, при выполнении команды появится запрос на ввод пароля.                                                |
|        /id \<OpenFileID>         |                                       Отключение открытых файлов с помощью идентификатора указанного файла. Подстановочный знак ( **&#42;** ) может использоваться с этим параметром.</br>Примечание. Можно использовать **/Query openfiles** команду, чтобы найти идентификатор файла.                                       |
|         /a \<пользователем >         |                                                Отключает все открытые файлы, связанные с именем пользователя, который указан в *пользователем* параметра. Подстановочный знак ( **&#42;** ) может использоваться с этим параметром.                                                 |
| /o {чтение \| записи \| чтение и запись} |                                               Отключает все открытые файлы со значением указанного открытый режим. Допустимые значения: чтения, записи или чтения и записи. Подстановочный знак ( **&#42;** ) может использоваться с этим параметром.                                                |
|         / OP \<OpenFile >          |                                                           Отключение всех подключений к открытым файлам, которые создаются по имени конкретного открытого файла. Подстановочный знак ( **&#42;** ) может использоваться с этим параметром.                                                           |
|                /?                |                                                                                                                     Отображение справки в командной строке.                                                                                                                     |

### <a name="examples"></a>Примеры

Чтобы отключить все открытые файлы с файлом ID 26843578, введите:
```
openfiles /disconnect /id 26843578
```
Чтобы отключить все открытые файлы и каталоги, осуществляется доступ пользователя «hiropln», введите:
```
openfiles /disconnect /a hiropln
```
Чтобы отключить все открытые файлы и каталоги в режиме чтения и записи, введите:
```
openfiles /disconnect /o read/write
```
Для отключения каталоге откройте файл с именем «C:\TestShare\", независимо от того, кто имеет доступ к нему, тип:
```
openfiles /disconnect /a * /op "c:\testshare\"
```
Чтобы отключить все открытые файлы на удаленном компьютере «srvmain», доступные для пользователя «hiropln», независимо от того, Идентификатору, введите:
```
openfiles /disconnect /s srvmain /u maindom\hiropln /id *
```

## <a name="BKMK_query"></a>Openfiles/Query

Запрос и отображение всех открытых файлов.

### <a name="syntax"></a>Синтаксис

```
openfiles /query [/s <System> [/u [<Domain>\]<UserName> [/p [<Password>]]]] [/fo {TABLE | LIST | CSV}] [/nh] [/v]
```

### <a name="parameters"></a>Параметры

|          Параметр           |                                                                                                                                 Описание                                                                                                                                  |
|------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|         /s \<system >         | Указывает удаленный систему для подключения к (по имени или IP-адрес). Не используйте символы обратной косой черты. Если вы не используете **/s** параметр, команда по умолчанию будет выполняться на локальном компьютере. Этот параметр применяется ко всем файлам и папкам, которые указаны в команде. |
|  /u [\<домена >\]<UserName>   |                                                          Выполняет команду с разрешениями указанной учетной записи. Если вы не используете **/u** параметр системные разрешения используются по умолчанию.                                                           |
|       /p [\<пароль >]       |                                               Указывает пароль для учетной записи пользователя, который указан в **/u** параметр. Если вы не используете **/p** параметр, при выполнении команды появится запрос на ввод пароля.                                                |
| [/fo {таблицы \| СПИСКА \| CSV}] |                             Отображает выходные данные в указанном формате. Допустимые значения для *формат* являются:</br>ТАБЛИЦА:  Отображение выходных данных в таблицу.</br>СПИСОК: Выходные данные отображаются в списке.</br>CSV: Отображает выходные данные в формате значений, разделенных запятыми.                              |
|             /NH              |                                                                                Подавляет вывод заголовка столбца. Допустим, только если **/fo** параметр имеет значение **таблицы** или **CSV**.                                                                                 |
|              /v              |                                                                                                       Указывает, что отображаться подробные сведения в выходных данных.                                                                                                        |
|              /?              |                                                                                                                     Отображение справки в командной строке.                                                                                                                     |

### <a name="examples"></a>Примеры

Для запроса и отображения всех открытых файлов, введите следующую команду:
```
openfiles /query
```
Для запроса и отображения всех открытых файлов в формате таблицы без заголовков, введите следующую команду:
```
openfiles /query /fo table /nh
```
Для запроса и отображения всех открытых файлов в формате списка с подробными сведениями, введите следующую команду:
```
openfiles /query /fo list /v
```
Чтобы запросить и отобразить все открытые файлы в удаленной системе «srvmain», используя учетные данные для пользователя «hiropln» на домене «Maindom», введите:
```
openfiles /query /s srvmain /u maindom\hiropln /p p@ssW23
```

> [!NOTE]
> В этом примере пароль введен в командной строке. Чтобы предотвратить отображение пароля, пропустите **/p** параметр. Вам будет предложено ввести пароль, который не будет перенесен на экран.

## <a name="BKMK_local"></a>/ Local Openfiles

Включает или отключает системы глобального флага Построение списка объектов. При использовании без параметров, **/Local openfiles** отображает текущее состояние глобального флага Построение списка объектов.

### <a name="syntax"></a>Синтаксис

```
openfiles /local [on | off]
```

### <a name="parameters"></a>Параметры

|Параметр|Описание|
|---------|-----------|
|[на \| off]|Включает или отключает глобальный флаг построение списка объектов, который отслеживает обработчики локальной файловой системе.|
|/?|Отображение справки в командной строке.|

### <a name="remarks"></a>Примечания

-   Включение глобального флага Построение списка объектов может замедлить работу системы.
-   Изменения, внесенные с помощью **на** или **off** параметр не вступают в силу после перезапуска системы.

### <a name="examples"></a>Примеры

Чтобы проверить текущее состояние глобального флага Построение списка объектов, введите следующую команду:
```
openfiles /local
```
По умолчанию глобального флага Построение списка объектов отключена, и выводятся следующие данные:
```
INFO: The system global flag 'maintain objects list' is currently disabled.
```
Чтобы включить глобальный флаг построение списка объектов, введите следующую команду:
```
openfiles /local on
```
При включении глобального флага, отображается следующее сообщение:
```
SUCCESS: The system global flag 'maintain objects list' is enabled.
         This will take effect after the system is restarted.
```
Чтобы отключить глобальный флаг построение списка объектов, введите следующую команду:
```
openfiles /local off
```

#### <a name="additional-references"></a>Дополнительная справка

[Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)