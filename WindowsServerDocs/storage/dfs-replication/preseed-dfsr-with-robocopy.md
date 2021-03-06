---
title: Предварительное заполнение файлов для репликации DFS с помощью Robocopy
description: Как выполнять предварительное заполнение файлов для репликации DFS с помощью программы Robocopy.exe.
ms.prod: windows-server
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 05/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: 8ff800fc2a0885cec39ca104607d7207f0bd8ce0
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2020
ms.locfileid: "80815607"
---
# <a name="use-robocopy-to-pre-seed-files-for-dfs-replication"></a>Предварительное заполнение файлов для репликации DFS с помощью Robocopy

>Применяется к: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

В этой статье объясняется, как с помощью программы командной строки **Robocopy.exe** выполнять предварительное заполнение файлов при настройке репликации распределенной файловой системы (DFS) (DFSR или DFS-R) в Windows Server. Предварительное заполнение файлов перед настройкой репликации DFS, репликация нового партнера или замена сервера ускоряют начальную синхронизацию и позволяют включить клонирование базы данных репликации DFS в Windows Server 2012 R2. Robocopy — это один из нескольких инструментов для предварительного заполнения (см. сведения о [предварительном заполнении файлов для репликации DFS](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn495046(v%3dws.11)>)).

Программа командной строки Robocopy (Robust File Copy) входит в состав Windows Server. Программа предоставляет широкие возможности, в том числе копирование протоколов безопасности, поддержку API резервного копирования, преимущества повторных попыток и ведение журнала. Более поздние версии включают в себя поддержку многопоточности, а также операций ввода-вывода без буферизации.

>[!IMPORTANT]
>Программа Robocopy не копирует монопольно заблокированные файлы. Если пользователи предпочитают блокировать множество файлов на файловых серверах на длительное время, попробуйте использовать другой метод предварительного заполнения. Предварительное заполнение не требует идеального соответствия между списками файлов на исходном и целевом серверах. Но чем меньше файлов существует при начальной синхронизации для репликации DFS, тем более эффективным будет предварительное заполнение. Чтобы избежать конфликтов блокировок, старайтесь использовать Robocopy в своей организации в нерабочее время. Чтобы узнать, какие файлы пропущены из-за монопольных блокировок, обязательно просматривайте журналы Robocopy после предварительного заполнения.

Для предварительного заполнения файлов для репликации DFS с помощью Robocopy выполните следующие действия:

1. [Скачайте и установите последнюю версию программы Robocopy](#step-1-download-and-install-the-latest-version-of-robocopy).
2. [Стабилизируйте файлы, которые будут реплицированы](#step-2-stabilize-files-that-will-be-replicated).
3. [Скопируйте реплицированные файлы на целевой сервер](#step-3-copy-the-replicated-files-to-the-destination-server).

## <a name="prerequisites"></a>Предварительные условия

Предварительное заполнение не подразумевает прямой репликации DFS. Поэтому важно выполнить требования к копированию файлов с помощью программы Robocopy.

- Вам потребуется учетная запись участника локальной группы администраторов на исходном и целевом серверах.

- Установите последнюю версию программы Robocopy на сервере, который будет использоваться для копирования файлов — или на исходном, или на целевом сервере. Необходимо также установить самую последнюю версию операционной системы. См. инструкции в разделе [Шаг 2. Стабилизация файлов, которые будут реплицированы](#step-2-stabilize-files-that-will-be-replicated). Если вы выполняете предварительное заполнение файлов с сервера не под управлением Windows Server 2003 R2, программу Robocopy можно запустить на исходном или целевом сервере. На целевом сервере, на котором обычно установлена последняя версия операционной системы, предоставляется доступ к самой последней версии программы Robocopy.

- Убедитесь, что на целевом диске достаточно места для хранения. Не создавайте папку с путем, по которому планируется копировать файлы. Программа Robocopy должна создать корневую папку.
    
    >[!NOTE]
    >Выбирая объем пространства, которое нужно выделить для предварительно заполненных файлов, следует учитывать ожидаемое увеличение объема данных с течением времени и требования к хранилищу для репликации DFS. Дополнительные сведения см. в статьях [Edit the Quota Size of the Staging Folder and Conflict and Deleted Folde](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754229(v=ws.11)) (Изменение размера квоты промежуточной папки и папки конфликтов и удаленных объектов) и [Managing DFS Replication](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754771(v=ws.11)>) (Управление репликацией DFS).

- На исходном сервере при необходимости установите монитор процессов или обозреватель процессов, чтобы использовать его для проверки приложений, блокирующих файлы. Сведения о скачивании см. в статье [Process Monitor v3.53](https://docs.microsoft.com/sysinternals/downloads/procmon) (Монитор процессов версии 3.53) и [Process Explorer v16.31](https://docs.microsoft.com/sysinternals/downloads/process-explorer) (Обозреватель процессов версии 16.31).

## <a name="step-1-download-and-install-the-latest-version-of-robocopy"></a>Шаг 1. Скачивание и установка последней версии программы Robocopy

Прежде чем выполнять предварительное заполнение файлов с помощью программы Robocopy, скачайте и установите последнюю версию файла **Robocopy.exe**. Таким образом репликация DFS не пропустит файлы из-за проблем в коммерческих версиях программы Robocopy.

Источник последней совместимой версии программы Robocopy зависит от версии Windows Server, которая работает на сервере. Сведения о скачивании исправления с последней версией программы Robocopy для Windows Server 2008 R2 или Windows Server 2008 см. в статье [List of currently available hotfixes for Distributed File System (DFS) technologies in Windows Server 2008 and in Windows Server 2008 R2](https://support.microsoft.com/help/968429/list-of-currently-available-hotfixes-for-distributed-file-system-dfs-t) (Список доступных исправлений для технологий распределенной файловой системы (DFS) в Windows Server 2008 и Windows Server 2008 R2).

Кроме того, выбрать и установить последнее исправление для операционной системы можно, выполнив следующие действия.

### <a name="locate-and-install-the-latest-version-of-robocopy-for-a-specific-version-of-windows-server"></a>Поиск и установка последней версии программы Robocopy для конкретной версии Windows Server

1. Откройте [https://support.microsoft.com](https://support.microsoft.com/) в браузере.

2. В поле **Поиск справки** введите следующую строку, заменив `<operating system version>` соответствующей операционной системой, а затем нажмите клавишу ВВОД:
    
    ```robocopy.exe kbqfe "<operating system version>"```
    
    Например, введите **robocopy.exe kbqfe "Windows Server 2008 R2"** .

3. Найдите и скачайте исправление с наибольшим номером идентификатора (то есть последнюю версию).

4. Установите исправление на сервере.

## <a name="step-2-stabilize-files-that-will-be-replicated"></a>Шаг 2. Стабилизация файлов, которые будут реплицированы

После установки на сервере последней версии программы Robocopy не следует предотвращать копирование заблокированных файлов с помощью методов, описанных в таблице ниже. Большинство приложений не выполняют монопольную блокировку файлов. Но при нормальной работе на файловых серверах может быть заблокирован небольшой процент файлов.

|Источник блокировки|Объяснение|Решение|
|---|---|---|
|Пользователи удаленно открывают файлы в общих папках.|Сотрудники могут подключаться к стандартному файловому серверу и редактировать документы, мультимедийное содержимое или другие файлы. Иногда это называется традиционными рабочими нагрузками домашней папки или общих данных.|Выполнять операции Robocopy следует только в часы наименьшей нагрузки в нерабочее время. Это позволяет сократить количество файлов, которые программа Robocopy должна пропустить во время предварительного заполнения.<br><br>Попробуйте временно установить доступ только для чтения к общим папкам, которые будут реплицироваться с помощью командлетов Windows PowerShell **Grant-SmbShareAccess** и **Close-SmbSession**. Если вы настроили разрешения на чтение для общей группы, например для всех пользователей или прошедших проверку подлинности, менее вероятно, что обычные пользователи будут открывать файлы и создавать монопольные блокировки (если их приложения обнаружат доступ только для чтения при открытии файлов).<br><br>Также можно установить временное правило брандмауэра для входящего SMB-порта 445 сервера, чтобы блокировать доступ к файлам, или использовать командлет **Block-SmbShareAccess**. Но оба эти метода существенно усложняют работу пользователей.|
|Приложения открывают файлы в локальной среде.|Рабочие нагрузки приложений, выполняющиеся на файловом сервере, иногда блокируют файлы.|Временно отключите или удалите приложения, блокирующие файлы. Для определения приложений, блокирующих файлы, можно использовать монитор процессов или обозреватель процессов. Чтобы скачать их, перейдите на страницы [Process Monitor v3.53](https://docs.microsoft.com/sysinternals/downloads/procmon) (Монитор процессов версии 3.53) и [Process Explorer v16.31](https://docs.microsoft.com/sysinternals/downloads/process-explorer) (Обозреватель процессов версии 16.31).|

## <a name="step-3-copy-the-replicated-files-to-the-destination-server"></a>Шаг 3. Копирование реплицированных файлов на целевой сервер

Сократив количество блокировок реплицируемых файлов, можно выполнить начальное заполнение файлов с исходного сервера на целевой.

>[!NOTE]
>Программу Robocopy можно запустить на исходном или целевом компьютере. Следующая процедура описывает запуск программы Robocopy на целевом сервере, который обычно работает под управлением операционной системы последней версии, что позволяет воспользоваться всеми самыми новыми возможностями Robocopy, доступными с такой ОС.

### <a name="pre-seed-the-replicated-files-onto-the-destination-server-with-robocopy"></a>Предварительное заполнение реплицированных файлов на целевой сервер с помощью программы Robocopy

1. Войдите на целевой сервер, используя учетную запись участника локальной группы администраторов на исходном и целевом серверах.

2. Откройте командную строку с повышенными привилегиями.

3. Чтобы реализовать предварительное заполнение файлов с исходного на целевой сервер, выполните следующую команду, подставив собственные пути к источнику, назначению и файлам журналов вместо значений в квадратных скобках:
    
    ```PowerShell
    robocopy "<source replicated folder path>" "<destination replicated folder path>" /e /b /copyall /r:6 /w:5 /MT:64 /xd DfsrPrivate /tee /log:<log file path> /v
    ```
    
    Эта команда копирует все содержимое исходной папки в целевую со следующими параметрами:
    
    |Параметр|Описание|
    |---|---|
    |\<путь к исходной реплицируемой папке\>|Указывает исходную папку для предварительного заполнения на целевой сервер.|
    |\<путь к целевой папке реплицируемой папки\>|Указывает путь к папке, в которой будут храниться файлы для предварительного заполнения.<br><br>Целевая папка не должна создаваться на целевом сервере. Чтобы получить соответствующие хэши файлов, программа Robocopy должна создать корневую папку при предварительном заполнении файлов.|
    |/e|Копирует подкаталоги и их файлы, а также пустые подкаталоги.|
    |/b|Копирует файлы в режиме резервного копирования.|
    |/copyall|Копирует все сведения о файле, в том числе данные, атрибуты, метки времени, список управления доступом NTFS, сведения о владельце и сведения об аудите.|
    |/r:6|Повторяет операцию шесть раз при возникновении ошибки.|
    |/w:5|Обеспечивает ожидание 5 секунд между повторными попытками.|
    |MT:64|Одновременно копирует 64 файла.|
    |/xd DfsrPrivate|Исключает папку DfsrPrivate.|
    |/tee|Записывает выходные данные состояния в окно консоли, а также в файл журнала.|
    |/log \<путь к файлу>|Указывает файл журнала для записи. Перезаписывает существующее содержимое файла. (Чтобы добавить записи в существующий файл журнала, используйте `/log+ <log file path>`.)|
    |/v|Создает подробные выходные данные, в том числе пропущенных файлов.|
    
    Например, следующая команда реплицирует файлы из исходной реплицированной папки, E:\\RF01, на диск данных D на целевом сервере:
    
    ```PowerShell
    robocopy.exe "\\srv01\e$\rf01" "d:\rf01" /e /b /copyall /r:6 /w:5 /MT:64 /xd DfsrPrivate /tee /log:c:\temp\pre-seedsrv02.log
    ```
    
    >[!NOTE]
    >При предварительном заполнении файлов для репликации DFS с помощью программы Robocopy мы рекомендуем использовать параметры, описанные выше. Некоторые из значений можно изменить или можно добавить дополнительные параметры. Например, в ходе тестирования может оказаться, что вы можете установить более высокое значение (количество потоков) для параметра */MT*. Кроме того, если вы в основном реплицируете файлы большего размера, можно увеличить производительность копирования, добавив параметр **/j** для операций ввода-вывода без буферизации. Дополнительные сведения о средстве Robocopy см. на странице справочника по командной строке [Robocopy](https://docs.microsoft.com/windows-server/administration/windows-commands/robocopy).

    >[!WARNING]
    >Чтобы избежать возможной потери данных предварительном заполнении файлов для репликации DFS с помощью программы Robocopy, не вносите в рекомендуемые параметры следующие изменения:
    >- Не используйте параметр */mir* (который производит зеркальное отражение дерева каталогов) или параметр */mov* (который перемещает файлы, а затем удаляет их из источника).
    >-  Не удаляйте параметры **/e**, **/b** и **/copyall**.

4. После завершения копирования проверьте журнал на наличие ошибок или пропущенных файлов. Используйте программу Robocopy, чтобы скопировать пропущенные файлы по отдельности вместо копирования всего набора файлов. Если файлы пропущены из-за монопольных блокировок, попробуйте скопировать отдельные файлы с помощью программы Robocopy позже или учтите, что эти файлы потребуется реплицировать по проводной сети с помощью репликации DFS во время начальной синхронизации.

## <a name="next-step"></a>Далее

После начального копирования и последующего решения проблем с максимально возможным количеством пропущенных файлов с помощью программы Robocopy используйте командлет **Get-DfsrFileHash** в Windows PowerShell или команду **Dfsrdiag**. Это позволит проверить предварительно заполненные файлы путем сравнения хэшей файлов на исходном и целевом серверах. Подробные инструкции см. в статье [Step 2: Шаг 2. Проверка предварительно заполненных файлов для репликации DFS](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn495042(v%3dws.11)>).
