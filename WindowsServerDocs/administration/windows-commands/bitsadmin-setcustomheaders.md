---
title: bitsadmin setcustomheaders
description: Раздел Windows команды для **bitsadmin setcustomheaders** -добавить пользовательский заголовок HTTP для запроса GET.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ed926410-80d0-46ed-9a90-f752c164bb9a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6d90ac2d23b852ae0c2114e7cd5a9c9e6382ce8c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2019
ms.locfileid: "59853855"
---
# <a name="bitsadmin-setcustomheaders"></a>bitsadmin setcustomheaders



Добавьте пользовательский заголовок HTTP для запроса GET.

## <a name="syntax"></a>Синтаксис

```
bitsadmin /SetCustomHeaders <Job> <Header1> <Header2> <. . .>
```

## <a name="parameters"></a>Параметры

|Параметр|Описание|
|---------|-----------|
|Job|Отображаемое имя или идентификатор GUID задания|
|Верхний колонтитул2 верхний колонтитул1. . .|Пользовательские заголовки для задания|

## <a name="remarks"></a>Примечания

-   Этот параметр используется для добавления пользовательского заголовка HTTP на запрос GET отправляется HTTP-сервера.

## <a name="BKMK_examples"></a>Примеры

В следующем примере добавляется пользовательский заголовок HTTP для задания с именем *myDownloadJob*.
```
C:\>bitsadmin / SetCustomHeaders myDownloadJob "Accept-encoding:deflate/gzip"
```

#### <a name="additional-references"></a>Дополнительная справка

[Ключ синтаксиса командной строки](command-line-syntax-key.md)