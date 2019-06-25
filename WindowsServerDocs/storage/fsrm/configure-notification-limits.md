---
title: Настройка пределов уведомлений
description: В этой статье описывается процесс добавления ограничений по времени в различные типы уведомлений
ms.date: 7/7/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: dba5b3b3c8b651935ec3c69695583d04087b7f2d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2019
ms.locfileid: "59826315"
---
# <a name="configure-notification-limits"></a>Настройка пределов уведомлений

> Относится к: Windows Server (полугодовой канал), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

Чтобы уменьшить количество уведомлений, которые накапливаются при постоянном превышении порога квоты или при попытке сохранить запрещенный файл, диспетчер ресурсов файлового сервера применяет ограничения по времени к следующим типам уведомлений.

-   электронная почта
-   Журнал событий
-   Command
-   Отчет

Каждое ограничение определяет период времени, который должен пройти, прежде чем для одной и той же проблемы будет сформировано еще одно уведомление того же типа.

Для каждого типа уведомления установлено ограничение по умолчанию, составляющее 60 минут, однако вы можете изменить его. Ограничение применяется ко всем уведомлениям данного типа независимо от способа их создания: по пороговым значениям квоты или по событиям фильтра блокировки файлов.

## <a name="to-specify-a-standard-notification-limit-for-each-notification-type"></a>Чтобы указать стандартное ограничение для каждого типа уведомления, выполните следующие действия.

1.  В древе консоли выберите **Диспетчер ресурсов файлового сервера** и выберите команду **Настроить параметры**. Откроется диалоговое окно **Параметры диспетчера ресурсов файлового сервера** .

2.  На вкладке **Пределы уведомлений** введите значение в минутах для каждого отображающегося типа уведомлений.

3.  Нажмите кнопку **ОК**.

> [!Note]
> Чтобы настроить ограничения по времени, связанные с уведомлениями для конкретной квоты или фильтра блокировки файлов, можно использовать средства командной строки диспетчера ресурсов файлового сервера **Dirquota.exe** и **Filescrn.exe** или использовать командлеты [диспетчера ресурсов файлового сервера](https://technet.microsoft.com/itpro/powershell/windows/fileserverresourcemanager/fileserverresourcemanager).

## <a name="see-also"></a>См. также

-   [Параметры диспетчера ресурсов файлового сервера в параметр](setting-file-server-resource-manager-options.md)
-   [Программы командной строки](command-line-tools.md)