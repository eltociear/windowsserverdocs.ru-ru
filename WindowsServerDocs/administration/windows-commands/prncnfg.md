---
title: prncnfg
description: Узнайте, как настроить принтер с помощью команды прнкфг.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 38a4e8fa-3122-495b-a125-35b926bc6415
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: 49d079c8c659fc1f8abc821935c401ae00bc8ba4
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/01/2020
ms.locfileid: "82722854"
---
# <a name="prncnfg"></a>prncnfg

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Настраивает или отображает сведения о конфигурации принтера.

## <a name="syntax"></a>Синтаксис
```
cscript Prncnfg {-g | -t | -x | -?} [-S <ServerName>] [-P <printerName>] [-z <NewprinterName>] [-u <UserName>] [-w <Password>] [-r <PortName>] [-l <Location>] [-h <Sharename>] [-m <Comment>] [-f <SeparatorFileName>] [-y <Datatype>] [-st <starttime>] [-ut <Untiltime>] [-i <DefaultPriority>] [-o <Priority>] [<+|->shared] [<+|->direct] [<+|->hidden] [<+|->published] [<+|->rawonly] [<+|->queued] [<+|->enablebidi] [<+|->keepprintedjobs] [<+|->workoffline] [<+|->enabledevq] [<+|->docompletefirst]
```

### <a name="parameters"></a>Параметры
|Параметр|Описание|
|-------|--------|
|-g|Отображает сведения о конфигурации принтера.|
|-T|Настраивает принтер.|
|-X|Переименовывает принтер.|
|-S \<имя_сервера\>|Указывает имя удаленного компьютера, на котором размещен принтер, которым требуется управлять. Если компьютер не указан, используется локальный компьютер.|
|-P \<принтернаме\>|Указывает имя принтера, которым требуется управлять. Обязательный.|
|-z \<невпринтернаме\>|Указывает новое имя принтера. Требуются параметры **-x** и **-P** .|
|-u \<имя_пользователя\> -w \<пароль\>|Указывает учетную запись с разрешениями на подключение к компьютеру, на котором размещен принтер, которым требуется управлять. Все члены локальной группы администраторов целевого компьютера имеют эти разрешения, но разрешения также могут быть предоставлены другим пользователям. Если учетная запись не указана, необходимо войти в систему с учетной записью с этими разрешениями, чтобы команда работала.|
|-r \<портнаме\>|Указывает порт, к которому подключен принтер. Если это параллельный или последовательный порт, используйте идентификатор порта (например, LPT1 или COM1). Если это порт TCP/IP, используйте имя порта, указанное при добавлении порта.|
|-l \<расположение\>|Указывает расположение принтера, например "Копировать комнату".|
|-h \<имя_общего_ресурса\>|Указывает имя общего ресурса принтера.|
|-m \<комментарий\>|Указывает строку комментария принтера.|
|-f \<сепараторфиленаме\>|Задает файл, содержащий текст, отображаемый на странице-разделителе.|
|-y \<тип данных\>|Указывает типы данных, которые может принимать принтер.|
|-ST \<StartTime\>|Настраивает принтер для ограниченной доступности. Указывает время суток, когда принтер доступен. При отправке документа на принтер, если он недоступен, документ сохраняется (в очереди), пока принтер не станет доступным. Необходимо указать время в виде 24-часового времени. Например, чтобы указать 11:00 P.M., введите **2300**.|
|-UT \<EndTime\>|Настраивает принтер для ограниченной доступности. Указывает время суток, когда принтер перестает быть доступным. При отправке документа на принтер, если он недоступен, документ сохраняется (в очереди), пока принтер не станет доступным. Необходимо указать время в виде 24-часового времени. Например, чтобы указать 11:00 P.M., введите **2300**.|
|-o \<приоритет\>|Указывает приоритет, используемый диспетчером очереди для направления заданий печати в очередь печати. Очередь печати с более высоким приоритетом получает все свои задания перед любой очередью с более низким приоритетом.|
|-i \<дефаултприорити\>|Указывает приоритет по умолчанию, назначаемый каждому заданию печати.|
|Общий доступ {+&#124;-}|Указывает, является ли этот принтер общим для сети.|
|Непосредственный {+&#124;-}|Указывает, должен ли документ отправляться непосредственно на принтер без помещения в очередь.|
|{+&#124;-} Опубликовано|Указывает, следует ли публиковать этот принтер в Active Directory. При публикации принтера другие пользователи могут искать его в зависимости от его расположения и возможностей (например, цветовой печати и сшивания).|
|{+&#124;-} скрыто|Зарезервированная функция.|
|{+&#124;-} равонли|Указывает, могут ли в этой очереди только задания печати с необработанными данными помещаться в очередь.|
|{+ &#124;-} поставлено в очередь|Указывает, что принтер не должен начинать печать до тех пор, пока не будет поставлена в очередь Последняя страница документа. Программа печати недоступна до завершения печати документа. Однако использование этого параметра гарантирует доступность всего документа для принтера.|
|{+ &#124;-} киппринтеджобс|Указывает, должен ли диспетчер очереди хранить документы после печати. Включение этого параметра позволяет пользователю повторно отправить документ на принтер из очереди печати, а не из программы печати.|
|{+ &#124;-} воркоффлине|Указывает, может ли пользователь отправить задания печати в очередь печати, если компьютер не подключен к сети.|
|{+ &#124;-} енабледевк|Указывает, должны ли задания печати, не соответствующие настройке принтера (например, файлы PostScript, помещенные в очередь на принтерах, отличных от PostScript), храниться в очереди, а не печататься.|
|{+ &#124;-} докомплетефирст|Указывает, должен ли диспетчер очереди отправлять задания печати с более низким приоритетом, которые завершили работу с очередью, прежде чем отправлять задания печати с более высоким приоритетом, который не завершил работу с очередью. Если этот параметр включен и документы не были завершены, то диспетчер очереди сообщений будет передавать большие документы перед меньшими. Этот параметр следует включать, если требуется максимально повысить эффективность работы принтера за счет приоритета задания. Если этот параметр отключен, диспетчер очереди печати всегда сначала отправляет задания с более высоким приоритетом в соответствующие очереди.|
|{+ &#124;-} енаблебиди|Указывает, отправляет ли принтер сведения о состоянии в Диспетчер очереди печати.|
|/?|Отображение справки в командной строке.|

## <a name="remarks"></a>Примечания
-   Команда **прнкнфг** является сценарием Visual Basic, расположенным в каталоге%WINDIR%\system32\\\ <language> printing_Admin_Scripts. Чтобы использовать эту команду, в командной строке введите **cscript** , а затем полный путь к файлу прнкнфг или измените каталоги на соответствующую папку. Пример:
    ```
    cscript %WINdir%\System32\printing_Admin_Scripts\en-US\prncnfg
    ```
-   Если предоставленные сведения содержат пробелы, заключите текст в кавычки (например, `"computer Name"`).

## <a name="examples"></a><a name="BKMK_examples"></a>Примеры
Чтобы отобразить сведения о конфигурации для принтера с именем colorprinter_2 с очередью печати, размещенной на удаленном компьютере с именем Хрсервер, введите:
```
cscript prncnfg -g -S HRServer -P colorprinter_2 
```

Чтобы настроить принтер с именем colorprinter_2 таким образом, чтобы диспетчер очереди на удаленном компьютере с именем Хрсервер сохранит задания печати после их вывода, введите:
```
cscript prncnfg -t -S HRServer -P colorprinter_2 +keepprintedjobs 
```

Чтобы изменить имя принтера на удаленном компьютере с именем Хрсервер с colorprinter_2 на колорпринтер 3, введите:
```
cscript prncnfg -x -S HRServer -P colorprinter_2 -z "colorprinter 3" 
```

## <a name="additional-references"></a>Дополнительные ссылки
- [Справочник по синтаксису](command-line-syntax-key.md)
[командной](print-command-reference.md) строки для команды Print
