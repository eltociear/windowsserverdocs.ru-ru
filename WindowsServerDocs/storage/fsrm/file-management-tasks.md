---
title: Задачи управления файлами
description: В этой статье описывается процесс автоматизации задач управления файлами
ms.date: 7/7/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: d8d798611a00e29337a5d45979947a51f03bcdee
ms.sourcegitcommit: ed27ddbe316d543b7865bc10590b238290a2a1ad
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/09/2019
ms.locfileid: "65475875"
---
# <a name="file-management-tasks"></a>Задачи управления файлами

> Относится к: Windows Server 2019, Windows Server 2016, Windows Server (полугодовой канал), Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

Задачи управления файлами автоматизируют процессы поиска наборов файлов на сервере и применения простых команд. Можно запланировать периодическое выполнение этих задач с целью сокращения повторяющихся расходов. Файлы, которые будут обрабатываться задачей управления файлами, можно определять с помощью любого из следующих свойств:

-   Location
-   Classification properties (свойства классификации)
-   Creation time (время создания)
-   Modification time (время изменения)
-   Last accessed time (время последнего доступа)

Задачи управления файлами также можно настраивать на оповещение владельцев файлов о любых будущих политиках, которые будут применены к их файлам.

> [!Note]
> Отдельные задачи управления файлами выполняются в соответствии с независимыми расписаниями.

<br />
Этот раздел содержит следующие темы:

-   [Создание задачи срока окончания действия файла](create-file-expiration-task.md)
-   [Создание задачи управления пользовательскими файлами](create-custom-file-management-task.md)

> [!Note]
> Чтобы настроить уведомления по электронной почте и определенные возможности создания отчетов, необходимо сначала настроить общие параметры диспетчера ресурсов файлового сервера.

## <a name="see-also"></a>См. также

-   [Настройка параметров диспетчера ресурсов файлового сервера](setting-file-server-resource-manager-options.md)

