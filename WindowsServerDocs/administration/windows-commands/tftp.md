---
title: tftp
description: Перенос файлов и с удаленного компьютера.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 772f19a8-dafe-45cd-878a-f5691f6568ef vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ad195409076840fda0e8d6bf5cd0c295a62cdede
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2019
ms.locfileid: "59845905"
---
# <a name="tftp"></a>tftp

>Область применения. Windows Server (полугодовой канал), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Обычно обмен файлами с удаленного компьютера, на компьютере под управлением UNIX, на котором выполняется служба упрощенный протокол передачи файлов (tftp) или управляющей программы. TFTP обычно используется встроенными устройствами или системами, которые получают встроенного по, сведения о конфигурации или образ системы во время процесса загрузки с tftp-сервера.   

## <a name="syntax"></a>Синтаксис  
```  
tftp [-i] [<Host>] [{get | put}] <Source> [<Destination>]  
```  

### <a name="parameters"></a>Параметры  
|Параметр|Описание|  
|-------|--------|  
|-i|Задает режим передачи двоичных (также называется режимом октета). В двоичном режиме файл передается в байту. Используйте этот режим, при передаче двоичных файлов. Если **-i** — этот параметр опущен, файл передается в режиме ASCII. Это режим передачи по умолчанию. В этом режиме преобразует символы окончания строки (EOL) в соответствующий формат для указанного компьютера. Используйте этот режим, при передаче текстовых файлов. Если передача файла прошла успешно, отображается скорость передачи данных.|  
|\<Узел\>|Указывает локальный или удаленный компьютер.|  
|PUT|Передает файл *источника* на локальном компьютере в файл *назначения* на удаленном компьютере. Поскольку протокол tftp не поддерживает проверку подлинности пользователя, пользователь должен войти на удаленный компьютер и файлы должны быть доступны для записи на удаленном компьютере.|  
|get|Передает файл *назначения* на удаленном компьютере в файл *источника* на локальном компьютере.|  
|\<Source\>|Задает файл для передачи.|  
|\<Назначение\>|Указывает, где для передачи файла.|  

## <a name="remarks"></a>Примечания  
-   Можно установить клиент tftp, с помощью функции мастера добавления.  
-   Протокол tftp не поддерживает любой механизм проверки подлинности или шифрования, а также таким образом привести угрозу безопасности, если он присутствует. Установка tftp-клиента не рекомендуется для систем, подключенном к Интернету.  
-   Клиент tftp — это необязательное программное обеспечение и помечено как устаревшее в Windows Vista и более поздних версиях операционной системы Windows. Службу сервера tftp больше не предоставляются корпорацией Майкрософт, по соображениям безопасности.  

## <a name="BKMK_Examples"></a>Примеры  
Скопируйте файл **boot.img** с удаленного компьютера **Host1**.  
```  
tftp  -i Host1 get boot.img  
```  

## <a name="additional-references"></a>Дополнительная справка  
-   [Ключ синтаксиса командной строки](command-line-syntax-key.md)  