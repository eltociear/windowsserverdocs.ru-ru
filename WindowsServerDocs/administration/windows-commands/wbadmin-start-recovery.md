---
title: Wbadmin start Recovery
description: Справочный раздел по главному восстановлению, в котором выполняется операция восстановления на основе указанных параметров.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 52381316-a0fa-459f-b6a6-01e31fb21612
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ec116bb69dd70cb58f6cb71ccf9ccfa04dea2e54
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725884"
---
# <a name="wbadmin-start-recovery"></a>Wbadmin start Recovery

Выполняет операцию восстановления на основе указанных параметров.

Чтобы выполнить восстановление с помощью этой подкоманды, необходимо быть членом группы " **Операторы архива** " или " **Администраторы** ", либо вам должны быть делегированы соответствующие разрешения. Кроме того, необходимо запустить программу **Wbadmin** из командной строки с повышенными привилегиями. (Чтобы открыть командную строку с повышенными привилегиями, нажмите кнопку **Пуск**, щелкните правой кнопкой мыши пункт **Командная строка**и выберите команду **Запуск от имени администратора**.)

## <a name="syntax"></a>Синтаксис

```
wbadmin start recovery
-version:<VersionIdentifier>
-items:{<VolumesToRecover> | <AppsToRecover> | <FilesOrFoldersToRecover>}
-itemtype:{Volume | App | File}
[-backupTarget:{<VolumeHostingBackup> | <NetworkShareHostingBackup>}]
[-machine:<BackupMachineName>]
[-recoveryTarget:{<TargetVolumeForRecovery> | <TargetPathForRecovery>}]
[-recursive]
[-overwrite:{Overwrite | CreateCopy | Skip}]
[-notRestoreAcl]
[-skipBadClusterCheck]
[-noRollForward]
[-quiet]
```

### <a name="parameters"></a>Параметры

|Параметр|Описание|
|---------|-----------|
|-version|Указывает идентификатор версии восстанавливаемой резервной копии в формате мм/дд/гггг-чч: мм. Если вы не знакомы с идентификатором версии, введите **Wbadmin get versions**.|
|— элементы|Задает разделенный запятыми список томов, приложений, файлов или папок для восстановления.</br>Если параметр **-ItemType** имеет значение **Volume**, можно указать только один том, указав букву диска тома, точку подключения тома или имя тома на основе GUID.</br>Если параметр **-ItemType** имеет значение **app**, можно указать только одно приложение. Для восстановления приложение должно быть зарегистрировано в cистема архивации данных Windows Server. Можно также использовать значение **адифм** для восстановления установки Active Directory. Дополнительные сведения см. в разделе Примечания в.</br>Если параметр **-ItemType** имеет значение **File**, можно указать файлы или папки, но они должны быть частью одного тома, и они должны находиться в одной родительской папке.|
|-ItemType|Указывает тип восстанавливаемых элементов. Это должен быть **том**, **приложение**или **файл**.|
|-backupTarget|Указывает место хранения резервной копии, которую необходимо восстановить. Этот параметр полезен, если расположение отличается от того, где обычно хранятся резервные копии этого компьютера.|
|-Machine|Указывает имя компьютера, для которого требуется восстановить резервную копию. Этот параметр полезен при резервном копировании нескольких компьютеров в одно расположение. Его следует использовать, если указан параметр **-backupTarget** .|
|-Рековеритаржет|Задает расположение для восстановления. Этот параметр полезен, если это расположение отличается от расположения, резервное копирование которого было выполнено ранее. Его также можно использовать для восстановления томов, файлов или приложений. При восстановлении тома можно указать букву диска тома для дополнительного тома. При восстановлении файла или приложения можно указать альтернативное расположение для восстановления.|
|— рекурсивно|Действует только при восстановлении файлов. Восстанавливает файлы в папках и все файлы, подчиненные указанным папкам. По умолчанию восстанавливаются только файлы, находящиеся непосредственно в указанных папках.|
|-overwrite|Действует только при восстановлении файлов. Указывает действие, выполняемое, когда восстанавливаемый файл уже существует в том же расположении.</br>-   **Skip** вызывает Cистема архивации данных Windows Server пропустить существующий файл и продолжит восстановление следующего файла.</br>-   **CreateCopy** приводит к тому, что Cистема архивации данных Windows Server создать копию существующего файла, чтобы существующий файл не был изменен.</br>-   **Перезапись** приводит к тому, что Cистема архивации данных Windows Server перезаписывает существующий файл файлом из резервной копии.|
|-Нотрестореакл|Действует только при восстановлении файлов. Указывает, что не следует восстанавливать списки управления доступом (ACL) файлов, восстанавливаемых из резервной копии. По умолчанию списки ACL безопасности восстанавливаются (значение по умолчанию — **true)**. Если используется этот параметр, списки ACL для восстановленных файлов будут унаследованы от расположения, в которое восстанавливаются файлы.|
|-Скипбадклустерчекк|Действует только при восстановлении томов. Пропускает проверку дисков, на которые выполняется восстановление, для получения сведений о поврежденном кластере. При восстановлении на другом сервере или оборудовании рекомендуется не использовать этот параметр. Вы можете в любое время вручную выполнить команду **chkdsk/b** на этих дисках, чтобы проверить их на наличие поврежденных кластеров, а затем обновить сведения о файловой системе соответствующим образом.</br>Важно. до запуска **chkdsk** в соответствии с описанием поврежденные кластеры, переданные в восстановленной системе, могут быть неточными.|
|-Нороллфорвард|Действует только при восстановлении приложений. Разрешает предыдущее восстановление приложения на момент времени, если выбрана последняя версия из резервных копий. Для других версий приложения, которые не являются последними, предыдущее восстановление на момент времени выполняется по умолчанию.|
|-quiet|Выполняет подкоманду без запросов пользователю.|

## <a name="remarks"></a>Примечания

-   Чтобы просмотреть список элементов, доступных для восстановления из определенной версии резервной копии, используйте **Wbadmin get Items**. Если во время резервного копирования том не имел точки подключения или буквы диска, эта подкоманда вернет имя тома на основе GUID, которое будет использоваться для восстановления тома.
-   Если для параметра **-ItemType** задано значение **адифм** **, то для**выполнения операции установки с носителя можно воспользоваться значением параметра- **Item** , чтобы восстановить все связанные данные, необходимые для служб домен Active Directory. **Адифм** создает копию базы данных Active Directory, реестра и состояния SYSVOL, а затем сохраняет эти сведения в расположении, указанном параметром **-рековеритаржет**. Используйте этот параметр только при указании параметра **-рековеритаржет** .

>     [!NOTE]
>     Before using **wbadmin** to perform an install from media operation, you should consider using the **ntdsutil** command because **ntdsutil** only copies the minimum amount of data needed, and it uses a more secure data transport method.

## <a name="examples"></a>Примеры

Чтобы выполнить восстановление резервной копии с 31 марта 2013, созданной в 9:00 утра, тома d:, введите:
```
wbadmin start recovery -version:03/31/2013-09:00 -itemType:Volume -items:d:
```
Чтобы выполнить восстановление на диск d из резервной копии с 31 марта 2013 г. в реестре с 9:00 утра, введите:
```
wbadmin start recovery -version:03/31/2013-09:00 -itemType:App -items:Registry -recoverytarget:d:\
```
Чтобы выполнить восстановление резервной копии с 31 марта 2013, созданной в 9:00 утра, д:\фолдер и папок, подчиненных д:\фолдер, введите:
```
wbadmin start recovery -version:03/31/2013-09:00 -itemType:File -items:d:\folder -recursive
```
Чтобы выполнить восстановление резервной копии с 31 марта 2013, созданного в 9:00 утра, для тома \\ \\? \Volume{cc566d14-44a0-11d9-9d93-806e6f6e6963}\, введите:
```
wbadmin start recovery -version:03/31/2013-09:00 -itemType:Volume 
-items:\\?\Volume{cc566d14-44a0-11d9-9d93-806e6f6e6963}\
```
Чтобы выполнить восстановление резервной копии с 30 апреля 2013, которая заняла 9:00 утра общей папки \\ \\сервернаме\шаре из Server01, введите:
```
wbadmin start recovery -version:04/30/2013-09:00 -backupTarget:\\servername\share -machine:server01
```

## <a name="additional-references"></a>Дополнительные ссылки

-   [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)
-   Командлет [Start-вбфилерековери](https://technet.microsoft.com/library/jj902457.aspx)
-   Командлет [Start-вбхиперврековери](https://technet.microsoft.com/library/jj902463.aspx)
-   Командлет [Start-вбсистемстатерековери](https://technet.microsoft.com/library/jj902449.aspx)
-   Командлет [Start-вбволумерековери](https://technet.microsoft.com/library/jj902470.aspx)