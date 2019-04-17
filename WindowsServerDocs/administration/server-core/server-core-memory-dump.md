---
title: Настройка дампа памяти для установки основных серверных компонентов
description: Сведения о настройке дампа памяти для установки основных серверных компонентов Windows Server
ms.prod: windows-server-threshold
ms.mktglfcycl: manage
ms.sitesec: library
author: lizap
ms.localizationpriority: medium
ms.date: 10/17/2017
ms.openlocfilehash: bd22378ec7ce5a1ff4e39546246e6e85ca859c45
ms.sourcegitcommit: 1533d994a6ddea54ac189ceb316b7d3c074307db
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/01/2018
ms.locfileid: "1448184"
---
# <a name="configure-memory-dump-files-for-server-core-installation"></a>Настройка дампа памяти для установки основных серверных компонентов

>Область применения: Windows Server (Semi-Annual Channel) и Windows Server 2016

Используйте следующие действия для настройки дамп памяти для установки основных серверных компонентов. 

## <a name="step-1-disable-the-automatic-system-page-file-management"></a>Шаг 1: Отключите Управление файловым страницы автоматическая системы

Первый шаг — это вручную настроить параметры восстановления системы. Это необходимо для выполнения оставшихся действий.

Выполните следующую команду. 

```
wmic computersystem set AutomaticManagedPagefile=False
```
 
## <a name="step-2-configure-the-destination-path-for-a-memory-dump"></a>Шаг 2: Настройте конечный путь для дампа памяти

Не требуется иметь файл страницы в разделе, где установлена операционная система. Чтобы поместить файл страницы в другом разделе, необходимо создать новый раздел реестра с именем **DedicatedDumpFile**. Размер файла подкачки можно определить с помощью записей реестра **DumpFileSize** . Создание записей реестра DedicatedDumpFile и DumpFileSize, выполните следующие действия. 

1. В командной строке выполните команду **regedit** , чтобы открыть редактор реестра.
2. Найдите и выберите следующий подраздел реестра: HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\CrashControl
3. Нажмите кнопку **Правка > Создать > строковое значение**.
4. Назовите новое значение **DedicatedDumpFile**и нажмите клавишу ВВОД.
5. Щелкните правой кнопкой мыши **DedicatedDumpFile**и выберите команду **Изменить**.
6. В типе **данных значение** **\ < Drive\ >: \\\ < Dedicateddumpfile.sys\ >**, а затем нажмите **кнопку ОК**.

   >[!NOTE] 
   > Замените \ < Drive\ > с диска, содержащего достаточно дискового пространства для файла подкачки и замените \ < Dedicateddumpfile.dmp\ > полный путь к файлу выделенного.
 
7. Нажмите кнопку **Правка > Создать > значение DWORD**.
8. Введите **DumpFileSize**и нажмите клавишу ВВОД.
9. Щелкните правой кнопкой мыши **DumpFileSize**и выберите команду **Изменить**.
10. В поле **Изменение параметра DWORD** **базы**щелкните **Decimal**.
11. **Данные значения**введите соответствующее значение и нажмите кнопку **ОК**.
   >[!NOTE]
   > Размер файла дампа — в мегабайтах (МБ).
12. Закройте редактор реестра.

После определения местоположения раздела дампа памяти настройте конечный путь для файла страницы. Чтобы просмотреть текущий конечный путь для файла подкачки, выполните следующую команду:

```
wmic RECOVEROS get DebugFilePath
```

Назначения по умолчанию для **DebugFilePath** — % systemroot%\memory.dmp. Чтобы изменить текущий каталог, выполните следующую команду:

```
wmic RECOVEROS set DebugFilePath = <FilePath>
```

Задайте \ < FilePath\ > в конечную папку. Например следующую команду задает путь назначения дамп памяти C:\WINDOWS\MEMORY. DMP: 

```
wmic RECOVEROS set DebugFilePath = C:\WINDOWS\MEMORY.DMP
```
 
## <a name="step-3-set-the-type-of-memory-dump"></a>Шаг 3: Задайте тип дампа памяти

Определите тип дампа памяти для настройки сервера. Чтобы просмотреть текущий тип дампа памяти, выполните следующую команду:

```
wmic RECOVEROS get DebugInfoType
```

Чтобы изменить текущий тип дампа памяти, выполните следующую команду: 

```
wmic RECOVEROS set DebugInfoType = <Value>
```

\ < Value\ > может быть 0, 1, 2 или 3, как указано ниже.

- 0: отключение удаления дамп памяти.
- 1: полный дамп памяти. Записывает все содержимое системной памяти при непредвиденной остановке компьютера. Полный дамп памяти может содержать данные из процессов, которые были запущены дамп памяти.
- 2: дамп памяти ядра (по умолчанию). Записывает только память ядра. Это ускоряет процесс записи данных в файл журнала, когда зависания компьютера.
- 3: малый дамп памяти. Записывается минимальный набор полезной информации, которая может помочь определить причину компьютеру неожиданного сбоя.

## <a name="step-4-configure-the-server-to-restart-automatically-after-generating-a-memory-dump"></a>Шаг 4: Настройте сервер автоматический перезапуск после создания дампа памяти

По умолчанию сервер автоматически перезапускается после создания дампа памяти. Чтобы просмотреть текущую конфигурацию, выполните следующую команду:

```
wmic RECOVEROS get AutoReboot
```

Если значение для **AutoReboot** имеет значение TRUE, сервер перезапустится автоматически после создания дампа памяти. Настройка не требуется, и можно перейти к следующему шагу.

Если значение для **AutoReboot** имеет значение FALSE, сервер не перезапустится автоматически. Выполните следующую команду, чтобы изменить значение:

```
wmic RECOVEROS set AutoReboot = true
```
 
## <a name="step-5-configure-the-server-to-overwrite-the-existing-memory-dump-file"></a>Шаг 5: Настройте сервер на перезапись существующего файла дампа памяти

По умолчанию сервер перезаписывает существующий файл дампа памяти при создании нового, он будет создан. Чтобы определить, если существующие файлы дампа памяти уже настроены, требуется перезаписать, выполните следующую команду:

```
wmic RECOVEROS get OverwriteExistingDebugFile
```

Если значение равно 1, сервер будет перезапись существующего файла дампа памяти. Настройка не требуется, и можно перейти к следующему шагу.

Если значение равно 0, сервер не перезаписать существующий файл дампа памяти. Выполните следующую команду, чтобы изменить значение: 

```
wmic RECOVEROS set OverwriteExistingDebugFile = 1
```
 
## <a name="step-6-set-an-administrative-alert"></a>Шаг 6: Установка административные оповещения

Определить, подходит ли оповещение и назначьте **SendAdminAlert** соответствующим образом. Чтобы просмотреть текущее значение для SendAdminAlert, выполните следующую команду:

```
wmic RECOVEROS get SendAdminAlert
```

Возможные значения для SendAdminAlert: TRUE или FALSE. Чтобы изменить существующее значение SendAdminAlert имеет значение true, выполните следующую команду: 

```
wmic RECOVEROS set SendAdminAlert = true
```
 
## <a name="step-7-set-the-memory-dumps-page-file-size"></a>Шаг 7: Задайте размер файла подкачки дамп памяти

Чтобы проверить текущие настройки файла страницы, выполните одно из следующих команд:

   ```
   wmic.exe pagefile
   ```

   или

   ```
   wmic.exe pagefile list /format:list
   ```

Например выполните следующую команду, чтобы настроить исходный и максимальный размеры файла страницы:

```
wmic pagefileset where name="c:\\pagefile.sys" set InitialSize=1000,MaximumSize=5000
```

## <a name="step-8-configure-the-server-to-generate-a-manual-memory-dump"></a>Шаг 8: Настройка сервера для создания дампа памяти вручную

Можно вручную создать дамп памяти с помощью клавиатуры PS/2. По умолчанию эта функция отключена и недоступен для клавиатуры универсальной последовательной шины (USB).

Чтобы включить памяти вручную выводит с помощью клавиатуры PS/2, выполните следующую команду:

```
reg add HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\i8042prt\Parameters /v CrashOnCtrlScroll /t REG_DWORD /d 1 /f
```

Чтобы определить, если была включена функция должным образом, выполните следующую команду:

```
Reg query HKEY_LOCAL_MACHINE \ SYSTEM \ CurrentControlSet \ Services \ i8042prt \ Parameters / v CrashOnCtrlScroll
```

Необходимо перезапустить сервер, чтобы изменения вступили в силу. Можно перезапустить сервер, выполнив следующую команду:

```
Shutdown / r / t 0
```

Можно создать дамп памяти вручную с помощью клавиатуры PS/2, который подключен к серверу, удерживая клавишу CTRL СПРАВА клавиши SCROLL LOCK. Это делает компьютер ошибок проверки с кодом ошибки 0xE2. После перезапуска сервера новый файл дампа появится в окне конечный путь, установленной на шаге 2.

## <a name="step-9-verify-that-memory-dump-files-are-being-created-correctly"></a>Шаг 9: Проверьте, правильно создаются файлы дампа памяти

Чтобы убедиться, что правильно создаются файлы дампа памяти можно использовать утилиту dumpchk.exe. Служебная программа dumpchk.exe не установлен с параметром установки Server Core, необходимо будет запустить его с сервера с рабочего стола или из Windows 10. Кроме того необходимо установить средства отладки для продуктов системы Windows.  

Служебная программа dumpchk.exe позволяет передавать файл дампа памяти из установки основных серверных компонентов Windows Server 2008 на другой компьютер с помощью носитель.

> [!WARNING]
> Файлы страниц может быть очень большим тщательно рассмотрите возможность переключения метод и ресурсы, которые требуется метод.
 

Дополнительные справочные материалы

Общие сведения об использовании дампа памяти просмотрите [Общие сведения о параметрах файла дампа памяти для Windows](https://support.microsoft.com/help/254649/overview-of-memory-dump-file-options-for-windows).

Дополнительные сведения о файлах выделенного дамп Узнайте, [как использовать значение реестра DedicatedDeumpFile в целях преодоления ограничения места на системном диске во время записи дампа памяти системы](https://blogs.msdn.microsoft.com/ntdebugging/2010/04/02/how-to-use-the-dedicateddumpfile-registry-value-to-overcome-space-limitations-on-the-system-drive-when-capturing-a-system-memory-dump/).


