---
title: Wbadmin останавливает задание
description: Справочный раздел по параметру Wbadmin остановить задание, который отменяет операцию резервного копирования или восстановления, которая выполняется в данный момент. Отмененные операции не могут быть перезапущены — необходимо повторно выполнить отмененную операцию резервного копирования или восстановления с начала.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3b83b398-39c7-4410-bf17-5c1fb1a4f46d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6e6d2be62468102060aad502d47efbb6eae4fca8
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/24/2020
ms.locfileid: "83821364"
---
# <a name="wbadmin-stop-job"></a>Wbadmin останавливает задание



Отменяет операцию резервного копирования или восстановления, которая выполняется в данный момент. Отмененные операции не могут быть перезапущены — необходимо повторно выполнить отмененную операцию резервного копирования или восстановления с начала.

Чтобы предотвратить операцию резервного копирования или восстановления с помощью этой подкоманды, необходимо быть членом группы " **Операторы архива** " или " **Администраторы** ", либо вам должны быть делегированы соответствующие полномочия. Кроме того, необходимо запустить программу **Wbadmin** из командной строки с повышенными привилегиями. (Чтобы открыть командную строку с повышенными привилегиями, щелкните правой кнопкой мыши пункт **Командная строка** и выберите команду **Запуск от имени администратора**.)

## <a name="syntax"></a>Синтаксис

```
wbadmin stop job
[-quiet]
```

### <a name="parameters"></a>Параметры

|Параметр|Описание|
|---------|-----------|
|-quiet|Выполняет подкоманду без запросов пользователю.|

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)