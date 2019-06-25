---
title: typeperf
description: 'Раздел Windows команды для ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0c7ca89a-03b3-4626-afcf-ef8565e90043
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: cfcbac82b88c0c8d8bcc706ebfd807f96e359de7
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/31/2019
ms.locfileid: "66440787"
---
# <a name="typeperf"></a>typeperf



**Команды typeperf** команда записывает данные о производительности в окне командной строки или в файл журнала. Чтобы остановить **команды typeperf**, нажмите клавиши CTRL + C.

Примеры использования **команды typeperf**, см. в разделе [примеры](#BKMK_EXAMPLES).

## <a name="syntax"></a>Синтаксис

```
typeperf <counter [counter ...]> [options]
typeperf -cf <filename> [options]
typeperf -q [object] [options]
typeperf -qx [object] [options]
```

## <a name="parameters"></a>Параметры

|Параметр|Описание|
|---------|-----------|
|\<Счетчик [счетчика [...]] >|Задает счетчики производительности для мониторинга.|

> [!NOTE]
> **\<Счетчик >** — полное имя счетчика производительности в  *\\ \\\Counter Computer\Object (экземпляр)* форматирования, такие как  **\\ \\Server1\ Processor(0)\% в пользовательском режиме**.

## <a name="options"></a>Параметры

|                   Параметр                   |                                                         Описание                                                          |
|--------------------------------------------|------------------------------------------------------------------------------------------------------------------------------|
|                     -?                     |                                               Отображение контекстной справки.                                               |
| -f \<CSV&verbar;TSV&verbar;BIN&verbar;SQL> |                                    Задает формат выходного файла. Значение по умолчанию — CSV.                                     |
|              -cf \<имя файла >               |              Указывает файл, содержащий список счетчиков производительности для мониторинга, в один счетчик в строке.               |
|             -si < [[чч:] мм:] сс >             |                                  Указывает интервал выборки. Значение по умолчанию составляет одну секунду.                                   |
|               -o \<имя файла >               |     Указывает путь для выходного файла или базы данных SQL. По умолчанию используется STDOUT (написанного в командном окне).      |
|                -q [object]                 | Отображение списка установленных счетчиков (нет экземпляров). Чтобы вывести список счетчиков объекта, укажите его имя. \*\*\*ПРИМЕР |
|                -qx [object]                |        Отобразить список установленных счетчики с экземплярами. Чтобы вывести список счетчиков объекта, укажите его имя.        |
|               -sc \<samples>               |             Указывает количество выборок для сбора. По умолчанию используется для сбора данных до нажатия CTRL + C.              |
|            -config \<имя файла >             |                                    Указывает файл параметров, содержащий параметры команды.                                     |
|            -s \<имя_компьютера >             |                   Указывает на удаленный компьютер для мониторинга, если не указан в пути счетчика.                    |
|                     -y                     |                                        Да, ответьте на все вопросы без запроса подтверждения.                                        |

## <a name="BKMK_EXAMPLES"></a>Примеры

- Следующий пример записывает значения для счетчика производительности на локальном компьютере  **\\ \\процессор(_всего)\% загруженности** в командном окне с интервалом по умолчанию образец 1 секунда до нажатия CTRL + C.  
  ```
  typeperf "\Processor(_Total)\% Processor Time"
  ```  
- Следующий пример записывает значения в списке счетчиков в файле **counters.txt** в файл с разделителями-знаками табуляции **domain2.tsv** с интервалом выборки 5 секунд, пока не будут собраны примеры 50.  
  ```
  typeperf -cf counters.txt -si 5 -sc 50 -f TSV -o domain2.tsv
  ```  
- В следующем примере запрос установлены счетчики с экземплярами для объекта счетчика **PhysicalDisk** и записывает полученный список в файле **counters.txt**.  
  ```
  typeperf -qx PhysicalDisk -o counters.txt
  ```