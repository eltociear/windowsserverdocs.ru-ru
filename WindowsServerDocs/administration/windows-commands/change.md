---
title: изменить
description: 'Раздел Windows команды для ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 90012116-0fb3-4f34-a819-cf4d4b4f8981
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f0a02302c4b99ead3701a966ba2d3fc65f6b078d
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/31/2019
ms.locfileid: "66434404"
---
# <a name="change"></a>изменить

>Область применения. Windows Server (полугодовой канал), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Изменяет параметры сервера узла сеансов удаленных рабочих столов (rd узла сеансов) для входа в систему, сопоставления COM-портов и режим установки.
> [!NOTE]
> В Windows Server 2008 R2 службы терминалов были переименованы на службы удаленных рабочих столов. Чтобы найти новые возможности в последней версии, см. в разделе [какие возможности служб удаленных рабочих столов в Windows Server 2012](https://technet.microsoft.com/library/hh831527) в технической библиотеке Windows Server.
> ## <a name="syntax"></a>Синтаксис
> ```
> change logon
> change port
> change user
> ```
> ## <a name="parameters"></a>Параметры
> 
> |            Параметр            |                                                   Описание                                                   |
> |---------------------------------|-----------------------------------------------------------------------------------------------------------------|
> | [change logon](change-logon.md) | Включает или отключает вход сеансов на сервере узла сеансов удаленных рабочих столов или отображает текущее состояние входа в систему. |
> |  [change port](change-port.md)  |                Отображает и изменяет сопоставления COM-портов для совместимости с приложениями MS-DOS.                |
> |  [change user](change-user.md)  |                            изменяет режим установки для сервера узла сеансов удаленных рабочих столов.                             |
> 
> #### <a name="additional-references"></a>Дополнительные ссылки
> [Синтаксис командной строки Key](command-line-syntax-key.md)
> [служб удаленных рабочих столов &#40;служб терминалов&#41; описанием команды](remote-desktop-services-terminal-services-command-reference.md)