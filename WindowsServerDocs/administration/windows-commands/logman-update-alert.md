---
title: оповещение об обновлении Logman
description: Справочный раздел по команде Logman Update Alert, который обновляет свойства существующего сборщика данных оповещений.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ede94a76-931c-40ed-9fda-6766bed8ff72
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 49d07744df911b054c9c9235b297090e8c39019b
ms.sourcegitcommit: 29bc8740e5a8b1ba8f73b10ba4d08afdf07438b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/30/2020
ms.locfileid: "84222798"
---
# <a name="logman-update-alert"></a>оповещение об обновлении Logman

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Обновляет свойства существующего сборщика данных предупреждений.

## <a name="syntax"></a>Синтаксис

```
logman update alert <[-n] <name>> [options]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| -s`<computer name>` | Выполните команду на указанном удаленном компьютере. |
| -config`<value>` | Указывает файл параметров, содержащий параметры команды. |
| [-n]`<name>` | Имя целевого объекта. |
| -[-] u`<user [password]>` | Указывает пользователя для запуска от имени. При вводе `*` для пароля выводится запрос на ввод пароля. Пароль не отображается при вводе. |
| -m`<[start] [stop] [[start] [stop] [...]]>` | Изменения в начале или в ручном режиме вместо запланированного начала или окончания. |
| -RF`<[[hh:]mm:]ss>` | Запускает сборщик данных за указанный период времени. |
| -б`<M/d/yyyy h:mm:ss[AM|PM]>` | Начинает сбор данных в указанное время. |
| -e `<M/d/yyyy h:mm:ss[AM|PM]>` | Завершает сбор данных в указанное время. |
| -Si`<[[hh:]mm:]ss>` | Указывает интервал выборки для собираются данных счетчиков производительности. |
| -o`<path|dsn!log>` | Указывает выходной файл журнала или имя DSN и набора журналов в базе данных SQL. |
| -[-] r | Повторяет сборщик данных ежедневно с заданным временем начала и окончания. |
| -[-] a | Добавляет существующий файл журнала. |
| -[-] | Перезаписывает существующий файл журнала. |
| -[-] v`<nnnnnn|mmddhhmm>` | Присоединяет сведения о управлении версиями файлов к концу имени файла журнала. |
| -[-] RC`<task>` | Выполняет команду, указанную при каждом закрытии журнала. |
| -[-] максимум`<value>` | Максимальный размер файла журнала (в МБ или в максимальном количестве записей для журналов SQL). |
| -[-] cnf`<[[hh:]mm:]ss>` | Если указано время, создает новый файл по истечении указанного времени. Если параметр time не указан, создает новый файл при превышении максимального размера. |
| -y | Отвечает Да на все вопросы без запроса. |
| -CF`<filename>` | Указывает файл со списком счетчиков производительности для накопления. Файл должен содержать по одному имени счетчика производительности в строке. |
| -[-] El | Включает или отключает отчеты журнала событий. |
| -й`<threshold [threshold [...]]>` | Укажите счетчики и их пороговые значения для предупреждения. |
| -[-] RDC`<name>` | Указывает группу сборщиков данных, запускаемую при срабатывании предупреждения. |
| -[-] тн`<task>` | Указывает задачу, выполняемую при срабатывании оповещения. |
| -[-] коне`<argument>` | Указывает аргументы задачи, которые будут использоваться с задачей, заданной с помощью-тн. |
| /? | Отображает контекстную справку. |

#### <a name="remarks"></a>Комментарии

- Где [-] присутствует, Добавление дополнительного дефиса (-) инвертирует параметр.

### <a name="examples"></a>Примеры

Чтобы обновить существующее оповещение, именуемое *new_alert*, установите пороговое значение счетчика "% загруженности процессора" в группе счетчиков процессоров (_Total) в 40%, тип:

```
logman update alert new_alert -th \Processor(_Total)\% Processor time>40
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [команда logman Create Alert](logman-create-alert.md)

- [команда logman](logman.md)
