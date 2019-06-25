---
title: создать зеркальный том
description: 'Раздел Windows команды для ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 48776917-783a-47ff-8da4-1cab77cea34b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 72d80fdf6eca1262a858cbe2a98ed8c9c421bff6
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/31/2019
ms.locfileid: "66434080"
---
# <a name="create-volume-mirror"></a>создать зеркальный том

>Область применения. Windows Server (полугодовой канал), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Создание зеркального тома с помощью двух указанных динамических дисков.  
  
> [!NOTE]  
> Эта команда доступна только в Windows 7 и Windows Server 2008 R2.  
  
  
  
## <a name="syntax"></a>Синтаксис  
  
```  
create volume mirror [size=<n>] disk=<n>,<n>[,<n>,...] [align=<n>] [noerr] [noerr]  
```  
  
## <a name="parameters"></a>Параметры  
  
|         Параметр         |                                                                                                                                     Описание                                                                                                                                     |
|---------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|         Размер\=<n>         |                 Указывает объем места на диске в мегабайтах \(МБ\), том будет занимать на каждом диске. Если размер не задан, новый том занимает самый маленький диск и равное количество места на каждом последующем диске свободное место.                 |
| диск\=<n>,<n>\[,<n>,...\] |                       Указывает динамические диски, по которым создается зеркальный том. Требуется два диски для создания зеркального тома. Объем пространства, который равен размер, указанный с помощью **размер** параметра выделяется на каждом диске.                        |
|        Выравнивание\=<n>         | Выравнивает все области тома до ближайшей границы выравнивания. Этот параметр обычно используется с оборудованием номер логического устройства RAID \(LUN\) массивы для повышения производительности. *n* число килобайт \(КБ\) с самого начала диска до ближайшей границы выравнивания. |
|           успешного           |                                        Используется только для сценариев. При обнаружении ошибки, DiskPart продолжает обрабатывать команды, как если бы ошибки не было. Без этого параметра по ошибке будет возобновлено DiskPart завершить работу с ошибкой.                                         |
  
## <a name="remarks"></a>Примечания  
  
-   После создания тома фокус автоматически переносится на новый том.  
  
## <a name="BKMK_examples"></a>Примеры  
Чтобы создать зеркальный том 1000 МБ размер на дисках, 1 и 2, введите:  
  
```  
create volume mirror size=1000 disk=1,2  
```  
  
#### <a name="additional-references"></a>Дополнительные ссылки  
[Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)  
  

  
