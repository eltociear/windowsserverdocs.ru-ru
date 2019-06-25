---
title: FTP-get
description: Получить разделе команд Windows, для FTP-сервера
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d70355c4-58ef-43e0-916b-c7ecf77e6ee4 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 28961ccf0ae04b52586728f9c68a9b2ca3e69b1d
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/31/2019
ms.locfileid: "66438775"
---
# <a name="ftp-get"></a>FTP: получение

>Область применения. Windows Server (полугодовой канал), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Копирует удаленный файл на локальный компьютер, используя текущий тип передачи файла.   
## <a name="syntax"></a>Синтаксис  
```  
get <remoteFile> [<LocalFile>]  
```  
### <a name="parameters"></a>Параметры  

|   Параметр   |                                                              Описание                                                               |
|---------------|----------------------------------------------------------------------------------------------------------------------------------------|
| <remoteFile>  |                                                   Задает удаленный файл для копирования.                                                   |
| [<LocalFile>] | Указывает имя файла для использования на локальном компьютере. Если *Локальный_файл* не указан, будет использовано *Удаленный_файл* имя. |

## <a name="remarks"></a>Примечания  
**Получить** команда идентична **recv** команды.  
## <a name="BKMK_Examples"></a>Примеры  
Копировать **test.txt** на локальном компьютере, с помощью текущего типа передачи файлов.  
```  
get test.txt  
```  
Копировать **test.txt** на локальном компьютере как **test1.txt** тип переноса с помощью текущего файла.  
```  
Get test.txt test1.txt  
```  
## <a name="additional-references"></a>Дополнительные ссылки  
-   [FTP: ascii](ftp-ascii.md)  
-   [FTP: двоичные](ftp-binary.md)  
-   [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)  