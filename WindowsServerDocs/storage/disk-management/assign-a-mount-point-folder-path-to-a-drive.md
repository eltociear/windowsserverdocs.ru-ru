---
title: Назначение диску пути к папке точки подключения.
description: В этой статье описывается, как назначить диску путь к папке точки подключения вместо буквы.
ms.date: 06/07/2019
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: b2fda216b57fbf036ce20c40b4c8b38d44404f3c
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2020
ms.locfileid: "80815537"
---
# <a name="assign-a-mount-point-folder-path-to-a-drive"></a>Назначение диску пути к папке точки подключения

> **Относится к:** Windows 10, Windows 8.1, Windows Server (Semi-Annual Channel), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Можно использовать средство управления дисками, чтобы назначить диску путь к папке точки подключения вместо буквы. Пути к папкам точек подключения доступны только для пустых папок в базовых или динамических томах NTFS.

## <a name="assigning-a-mount-point-folder-path-to-a-drive"></a>Назначение диску пути к папке точки подключения

> [!NOTE]
> Для выполнения следующих шагов необходимо как минимум состоять в группе **Операторы архива** или **Администраторы**.

#### <a name="to-assign-a-mount-point-folder-path-to-a-drive-by-using-the-windows-interface"></a>Назначение диску пути к папке точки подключения с помощью интерфейса Windows

1.  В диспетчере дисков щелкните правой кнопкой мыши раздел или том, которому требуется назначить путь к папке точки подключения. 
2. Щелкните **Изменить букву диска или путь к диску**, а затем нажмите **Добавить**. 
3. Щелкните **Подключить к следующей пустой папке NTFS**.
4. Введите путь к пустой папке в томе NTFS или нажмите кнопку **Обзор**, чтобы найти ее.

#### <a name="to-assign-a-mount-point-folder-path-to-a-drive-using-a-command-line"></a>Назначение диску пути к папке точки подключения с помощью командной строки

1.  Откройте командную строку и введите: `diskpart`.

2.  В командной строке **DISKPART** введите `list volume` и запомните номер тома, которому требуется назначить путь.

3.  В командной строке **DISKPART** введите `select volume <volumenumber>`. 

4. Выберите простой том *volumenumber*, которому требуется назначить путь.

5.  В командной строке **DISKPART** введите `assign [mount=<path>]`.

#### <a name="to-remove-a-mount-point-folder-path-to-a-drive"></a>Удаление назначенного диску пути к папке точки подключения

-   Чтобы удалить путь к папке точки подключения, выберите его и нажмите кнопку **Удалить**.

| Применение | Описание |
| --- | --- |
| **list volume** | Отображает список базовых и динамических томов на всех дисках. |
| **select volume**        | Выбирает указанный том, где <em>volumenumber</em> — номер тома, и переводит на него фокус. Если том не указан, команда **select** отображает текущий том с фокусом. Для указания тома можно использовать номер, букву диска или путь к папке точки подключения. При выборе тома на базовом диске фокус переводится на соответствующий раздел.|
| **assign** | <ul><li> Назначает тому с фокусом букву диска или путь к папке точки подключения. Если буква диска или путь к папке точки подключения не указаны, назначается следующая доступная буква диска. Если буква диска или путь к папке точки подключения уже используется, отображается сообщение об ошибке.</li>  <li>С помощью команды **assign** можно изменить букву диска, связанную со съемным диском.</li> <li> Невозможно назначить букву диска загрузочному тому или тому с файлом подкачки. Кроме того, невозможно назначить букву диска разделу изготовителя оборудования (OEM), системному разделу EFI или любому разделу GPT, кроме базового раздела данных.</li></ul> |
| **mount=** <em>path</em> | Указывает пустую существующую папку NTFS, где будет располагаться подключенный диск.  |

## <a name="additional-considerations"></a>Дополнительные сведения

-   При администрировании локального или удаленного компьютера можно просматривать находящиеся на нем папки NTFS.
-   Пути к папкам точек подключения доступны только для пустых папок в базовых или динамических томах NTFS.
-   Для изменения пути к папке точки подключения удалите его и создайте новый путь к папке на основе нового расположения. Невозможно изменить путь к папке точки подключения напрямую.
-   При назначении диску пути к папке точки подключения используйте компонент **Просмотр событий**, чтобы проверить системный журнал на наличие ошибок или предупреждений службы кластеров, указывающих на сбои пути к папке точки подключения. Эти ошибки будут указаны как **ClusSvc** в столбце **Source** и **Physical Disk Resource** в столбце **Category**.
-   Также можно создать подключенный диск с помощью команды [mountvol](https://go.microsoft.com/fwlink/?linkid=64111).

## <a name="see-also"></a>См. также статью
-   [Представление синтаксиса команд](https://technet.microsoft.com/library/cc742449(v=ws.11).aspx)


