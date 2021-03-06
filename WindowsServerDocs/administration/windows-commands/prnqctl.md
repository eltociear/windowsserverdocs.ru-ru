---
title: prnqctl
description: Печать тестовой страницы, приостановка или возобновление печати принтера.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 8df9dfa7-984c-4276-bb7d-e7675e7c399e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: 3e18a9c0321197887b1f708854a130f41b41e7a7
ms.sourcegitcommit: 29bc8740e5a8b1ba8f73b10ba4d08afdf07438b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/30/2020
ms.locfileid: "84222034"
---
# <a name="prnqctl"></a>prnqctl

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Печать тестовой страницы, приостановка или возобновление печати принтера и очистка очереди печати.

## <a name="syntax"></a>Синтаксис
```
cscript Prnqctl {-z | -m | -e | -x | -?} [-s <ServerName>]
[-p <printerName>] [-u <UserName>] [-w <Password>]
```
### <a name="parameters"></a>Параметры

|Параметр|Описание|
|-------|--------|
|-Z|приостанавливает печать на принтере, указанном параметром **-p** .|
|-M|Возобновляет печать на принтере, указанном параметром **-p** .|
|-E|выводит тестовую страницу на принтере, указанном параметром **-p** .|
|-X|Отменяет все задания печати на принтере, указанном параметром **-p** .|
|-s\<ServerName>|Указывает имя удаленного компьютера, на котором размещен принтер, которым требуется управлять. Если компьютер не указан, используется локальный компьютер.|
|-p\<printerName>|Указывает имя принтера, которым требуется управлять. Обязательный.|
|-u \<UserName> -w\<Password>|Указывает учетную запись с разрешениями на подключение к компьютеру, на котором размещен принтер, которым требуется управлять. Все члены локальной группы администраторов целевого компьютера имеют эти разрешения, но разрешения также могут быть предоставлены другим пользователям. Если учетная запись не указана, необходимо войти в систему с учетной записью с этими разрешениями, чтобы команда работала.|
|/?|Отображение справки в командной строке.|

## <a name="remarks"></a>Комментарии
- Команда **прнкктл** является сценарием Visual Basic, расположенным в каталоге%WINDIR%\system32\ printing_Admin_Scripts \\ <language> . Чтобы использовать эту команду, в командной строке введите **cscript** , а затем полный путь к файлу прнкктл или измените каталоги на соответствующую папку. Пример:
  ```
  cscript %WINdir%\System32\printing_Admin_Scripts\en-US\prnqctl
  ```
- Если предоставленные сведения содержат пробелы, заключите текст в кавычки (например, `"computer Name"` ).

## <a name="examples"></a><a name="BKMK_examples"></a>Примеры
Чтобы напечатать тестовую страницу на принтере Laserprinter1, совместно используемом \\ компьютером \Server1, введите:
```
cscript Prnqctl -e -s Server1 -p Laserprinter1
```
Чтобы приостановить печать на принтере Laserprinter1 на локальном компьютере, введите:
```
cscript Prnqctl -z -p Laserprinter1
```
Чтобы отменить все задания печати на принтере Laserprinter1 на локальном компьютере, введите:
```
cscript Prnqctl -x -p Laserprinter1
```

## <a name="additional-references"></a>Дополнительные ссылки
- Ключ синтаксиса [командной строки](command-line-syntax-key.md) 
 [Справочник по командам печати](print-command-reference.md)
