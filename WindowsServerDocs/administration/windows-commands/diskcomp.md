---
title: diskcomp
description: Справочный раздел по команде diskcomp, который сравнивает содержимое двух дискет.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4f56f534-a356-4daa-8b4f-38e089341e42
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: fcb810f4cd18d51f8151b27a6f447c86130624fd
ms.sourcegitcommit: fad2ba64bbc13763772e21ed3eabd010f6a5da34
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/09/2020
ms.locfileid: "82992522"
---
# <a name="diskcomp"></a>diskcomp

Сравнение содержимого двух гибких дисков. Если используется без параметров, **команда diskcomp** использует текущий диск для сравнения обоих дисков.

## <a name="syntax"></a>Синтаксис

```
diskcomp [<drive1>: [<drive2>:]]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| `<drive1>` | Указывает диск, содержащий один из гибких дисков. |
| /? | Отображение справки в командной строке. |

#### <a name="remarks"></a>Remarks

- Команда **diskcomp** работает только с гибкими дисками. Нельзя использовать **diskcomp** с жестким диском. Если для *диск1* или *диск2*указан жесткий диск, **команда diskcomp** выводит следующее сообщение об ошибке:

  ```
  Invalid drive specification
  Specified drive does not exist
  or is nonremovable
  ```

- Если все дорожки на двух сравниваемых дисках одинаковы (он игнорирует номер тома диска), **команда diskcomp** выводит следующее сообщение:

  ```
  Compare OK
  ```

  Если дорожки не совпадают, **команда diskcomp** выведет примерно следующее сообщение:

  ```
  Compare error on
  side 1, track 2
  ```

  Когда **команда diskcomp** завершает сравнение, отображается следующее сообщение:

  ```
  Compare another diskette (Y/N)?
  ```

  Если нажать клавишу **Y**, программа **diskcomp** предложит вставить диск для следующего сравнения. При нажатии **N**клавиши N **команда diskcomp** прекращает сравнение.

- Если опустить параметр *диск2* , **команда diskcomp** будет использовать текущий диск для *диск2*. Если вы не пропускаете оба параметра диска, **команда diskcomp** использует текущий диск для обоих параметров. Если текущий диск совпадает с параметром *диск1*, программа **diskcomp** предлагает при необходимости поменять диски.

- Если для *диск1* и *диск2*указан один и тот же гибкий диск, программа **diskcomp** сравнивает их с использованием одного диска и предлагает вставить диски по мере необходимости. Возможно, потребуется переключить диски несколько раз в зависимости от емкости дисков и объема доступной памяти.

- **Diskcomp** не может сравнить односторонний диск с двойным диском и диск высокой плотности с диском двойной плотности. Если диск в параметре *диск1* отличается от типа диска в *диск2*, **команда diskcomp** выводит следующее сообщение:

  ```
  Drive types or diskette types not compatible
  ```

- Команда **diskcomp** не работает на сетевом диске или на диске, созданном с помощью команды **subst** . При попытке использовать команду **diskcomp** с диском любого из этих типов **команда diskcomp** выводит следующее сообщение об ошибке:

  ```
  Invalid drive specification
  ```

- Если вы используете команду **diskcomp** с диском, созданным с помощью команды **Copy**, **команда diskcomp** может вывести примерно следующее сообщение:

  ```
  Compare error on
  side 0, track 0
  ```

  Этот тип ошибки может возникать, даже если файлы на дисках идентичны. Несмотря на то, что данные **копирования** дублируются, они не обязательно будут размещаться в том же расположении на целевом диске.

- коды завершения команды **diskcomp** :

  | Код выхода | Описание |
  | --------- | ----------- |
  | 0 | Диски одинаковы |
  | 1 | Обнаружены различия |
  | 3 | Произошла твердая ошибка |
  | 4 | Произошла ошибка инициализации |

  Для обработки кодов завершения, возвращаемых командой **diskcomp**, можно использовать переменную среды *ERRORLEVEL* в командной строке **If** в пакетной программе.

## <a name="examples"></a>Примеры

Если на компьютере имеется только один дисковод гибких дисков (например, диск A) и требуется сравнить два диска, введите:

```
diskcomp a: a:
```

При необходимости программа **diskcomp** предлагает вставить каждый диск.

Описание процесса обработки **кода выхода из** командной строки в пакетной программе, использующей переменную среды *ERRORLEVEL* в командную строку **If** :

```
rem Checkout.bat compares the disks in drive A and B
echo off
diskcomp a: b:
if errorlevel 4 goto ini_error
if errorlevel 3 goto hard_error
if errorlevel 1 goto no_compare
if errorlevel 0 goto compare_ok
:ini_error
echo ERROR: Insufficient memory or command invalid
goto exit
:hard_error
echo ERROR: An irrecoverable error occurred
goto exit
:break
echo You just pressed CTRL+C to stop the comparison
goto exit
:no_compare
echo Disks are not the same
goto exit
:compare_ok
echo The comparison was successful; the disks are the same
goto exit
:exit
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
