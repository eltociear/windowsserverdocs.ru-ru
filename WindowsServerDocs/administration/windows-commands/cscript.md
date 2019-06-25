---
title: cscript
description: 'Раздел Windows команды для ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fba3cbca-594e-4663-bb22-4ee0f63a1ac6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ef98a98088e345f267aa852318cee6e237604aa4
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/31/2019
ms.locfileid: "66433991"
---
# <a name="cscript"></a>cscript

>Область применения. Windows Server (полугодовой канал), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

запускает сценарий для запуска его в среде командной строки.
## <a name="syntax"></a>Синтаксис
```
cscript <Scriptname.extension> [/B] [/D] [/E:<Engine>] [{/H:cscript|/H:wscript}] [/I] [/Job:<Identifier>] [{/Logo|/NoLogo}] [/S] [/T:<Seconds>] [/X] [/U] [/?] [<ScriptArguments>]
```
### <a name="parameters"></a>Параметры

|      Параметр       |                                                                      Описание                                                                       |
|----------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| Scriptname.Extension |                                 Указывает путь и имя файла скрипта с необязательным расширением.                                 |
|          /B          |                                Указывает режим пакетной службы, в котором не отображаются предупреждения, сообщения об ошибках и запросов на входные данные.                                |
|          /D          |                                                                  Запускает отладчик.                                                                  |
|     / E:<Engine>      |                                                  Задает обработчик, который используется для запуска скрипта.                                                  |
|      / H      |                                         Регистрирует cscript.exe в качестве сервера сценариев по умолчанию для выполнения скриптов.                                          |
|      /H:Wscript      |                               Регистрация wscript.exe в качестве сервера сценариев по умолчанию для выполнения скриптов. Это значение используется по умолчанию.                               |
|          /I          |        Указывает интерактивный режим, в котором отображаются предупреждения, сообщения об ошибках и запросов на входные данные. Это значение по умолчанию и противоположностью **/B**.         |
|  / Задание:<Identifier>   |                                             Запускает задание, определяемое *идентификатор* в файле скрипта .wsf.                                             |
|        И логотип         | Указывает, что Windows Script Host баннер отображается в консоли, перед выполнением сценария. Это значение по умолчанию и противоположностью **/nologo**. |
|       / Nologo        |                                 Указывает, что Windows Script Host баннер не отображается, перед выполнением сценария.                                 |
|          /S          |                                             Сохраняет текущие параметры командной строки для текущего пользователя.                                             |
|     /T:<Seconds>     |            Указывает максимальное время выполнения сценария (в секундах). Можно указать до 32 767 секунд. По умолчанию используется без временных ограничений.             |
|          /U          |                                      Указание формата Юникод для ввода и вывода, который перенаправляется из консоли.                                       |
|          /X          |                                                           Запускает сценарий в отладчике.                                                           |
|          /?          |  Отображает доступные параметры и предоставляет справку по их использованию. Это то же самое, как ввести **cscript.exe** без параметров и не сценарий.  |
|   Аргументы_сценария    |                        Задает аргументы, переданные в сценарий. Каждый аргумент скрипт должен предшествовать косая черта ( **/** ).                         |

### <a name="remarks"></a>Примечания
-   Для выполнения этой задачи не требуются права, соответствующие учетным данным администратора. Таким образом, по соображениям безопасности ее рекомендуется выполнять от имени пользователя, не обладающего правами на администрирование системы.
-   Чтобы открыть командную строку, на **запустить** введите **cmd**и нажмите кнопку **командной**.
-   Все параметры являются необязательными; Тем не менее нельзя указать аргументы скрипта, не указывая сценарий. Если вы не укажете сценарий или любые аргументы скрипта, cscript.exe отображает синтаксис cscript.exe и ключи.
-   **/T** параметр предотвращает чрезмерное выполнение сценариев с помощью таймера. Если время выполнения превышает указанное значение, cscript прерывает работу обработчика сценариев и завершает процесс.
-   Файлы скриптов Windows обычно имеют один из следующих расширений имени файла: .wsf, .vbs, .js.
-   Можно задать свойства для отдельных сценариев. Дополнительные сведения см.
-   Файлы скриптов .wsf можно использовать сервер сценариев Windows. Каждый файл .wsf можно иметь несколько обработчиков и выполнять несколько заданий.
-   Если дважды щелкнуть файл сценария с расширением, не связан ни, **открыть с помощью** откроется диалоговое окно. Выберите wscript или cscript, а затем выберите **всегда используйте программу для открытия данного типа файлов**. Это регистрирует wscript.exe или cscript в качестве сервера сценариев по умолчанию для файлов этого типа.
-   Можно задать свойства для отдельных сценариев. См. в разделе [Дополнительные ссылки](#BKMK_references) Дополнительные сведения.
-   Файлы скриптов .wsf можно использовать сервер сценариев Windows. Каждый файл .wsf можно иметь несколько обработчиков и выполнять несколько заданий.

#### <a name="BKMK_references"></a>Дополнительные ссылки

[Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)