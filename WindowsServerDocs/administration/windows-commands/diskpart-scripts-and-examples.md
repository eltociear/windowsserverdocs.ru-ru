---
title: сценарии и примеры для DiskPart
description: Справочный раздел, посвященный сценариям и примерам для автоматизации задач, связанных с диском, таких как создание томов или преобразование дисков в динамические диски.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 319c0795-11df-47c8-b203-eadb0577ee0d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f3e781e49aa978288de45da90224a3f1c2b247b1
ms.sourcegitcommit: fad2ba64bbc13763772e21ed3eabd010f6a5da34
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/09/2020
ms.locfileid: "82992491"
---
# <a name="diskpart-scripts-and-examples"></a>сценарии и примеры для DiskPart

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Используется `diskpart /s` для выполнения сценариев, автоматизирующих задачи, связанные с дисками, например для создания томов или преобразования дисков в динамические диски. Написание сценариев этих задач полезно при развертывании Windows с помощью автоматической установки или средства Sysprep, которые не поддерживают создание томов, отличных от загрузочного тома.

Чтобы создать сценарий DiskPart, создайте текстовый файл, содержащий команды DiskPart, которые необходимо выполнить, с одной командой в строке и без пустых строк. Чтобы сделать строку комментарием, `rem` можно начать с строки. Например, Вот сценарий, который очищает диск, а затем создает раздел 300 МБ для среды восстановления Windows:

    ```
    select disk 0
    clean
    convert gpt
    create partition primary size=300
    format quick fs=ntfs label=Windows RE tools
    assign letter=T
    ```

## <a name="examples"></a>Примеры

- Чтобы запустить сценарий DiskPart, в командной строке введите следующую команду, где *имя_сценария* — это имя текстового файла, содержащего скрипт:

    ```
    diskpart /s scriptname.txt
    ```

- Чтобы перенаправить выходные данные сценария DiskPart в файл, введите следующую команду, где *файл_журнала* — это имя текстового файла, в который DiskPart записывает выходные данные:

    ```
    diskpart /s scriptname.txt > logfile.txt
    ```

### <a name="remarks"></a>Remarks

- При использовании команды **DiskPart** в составе скрипта рекомендуется выполнять все операции DiskPart вместе в рамках одного сценария DiskPart. Можно выполнять последовательные скрипты DiskPart, но по крайней мере 15 секунд между каждым сценарием необходимо выполнить полное завершение работы, прежде чем запускать команду **DiskPart** в последующих сценариях. В противном случае последующие сценарии могут завершиться ошибкой. Можно добавить паузу между последовательными сценариями DiskPart, добавив `timeout /t 15` команду в пакетный файл вместе с сценариями DiskPart.

- При запуске программы DiskPart в командной строке отобразится версия и имя сервера DiskPart. По умолчанию, если при попытке выполнения задачи, выполняемой в скрипте, DiskPart обнаруживает ошибку, DiskPart прекращает обработку скрипта и выводит код ошибки (если не указан параметр **noerr** ). Однако при возникновении синтаксических ошибок программа DiskPart всегда возвращает ошибки, независимо от того, использовался ли параметр **noerr** . Параметр **noerr** позволяет выполнять такие полезные задачи, как использование одного сценария для удаления всех разделов на всех дисках, независимо от общего числа дисков.

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Пример. Настройка разделов\/жесткого\-диска на основе UEFI с помощью Windows PE и программы DiskPart](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-8.1-and-8/hh825686(v=win.10))

- [Пример. Настройка разделов\/жесткого\-диска на основе MBR BIOS с помощью Windows PE и программы DiskPart](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-8.1-and-8/hh825677(v=win.10))

- [Командлеты хранилищ в Windows PowerShell](https://docs.microsoft.com/powershell/module/storage/?view=win10-ps)
