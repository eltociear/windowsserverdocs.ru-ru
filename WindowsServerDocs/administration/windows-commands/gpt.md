---
title: GPT
description: 'Раздел Windows команды для ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1d6f9029-807f-4420-a336-36669b5361bc
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: cba9839f98dfd5a72289838273a057dd0e09a7e5
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/31/2019
ms.locfileid: "66438179"
---
# <a name="gpt"></a>GPT

>Область применения. Windows Server (полугодовой канал), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

На базовых дисках (gpt) таблицы разделов GUID назначает атрибуты таблицы разделов GUID раздела, имеющего фокус.  атрибуты раздела GPT предоставляют дополнительные сведения об использовании секции. Некоторые атрибуты относятся только к секции типа GUID.

> [!CAUTION]
> Изменение атрибутов gpt может привести к базовых томов данных переход на другой могут быть назначены буквы дисков, или для предотвращения подключения файловой системы. Атрибуты gpt следует изменять только поставщикам вычислительной техники (ПВТ) и ИТ-специалист, опыт работы с диски gpt.
> ## <a name="syntax"></a>Синтаксис
> ```
> gpt attributes=<n>
> ```
> ## <a name="parameters"></a>Параметры
> 
> |   Параметр    |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               Описание                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
> |----------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
> | атрибуты =<n> | Задает значение атрибута, которое вы хотите применить к разделу с фокусом. Поле атрибута gpt является 64-битовое поле, которое содержит два дополнительных поля. Верхнее поле интерпретируется только в контексте идентификатора секции, а нижнее поле является общим для всех секций с идентификаторами. Допустимые значения:<br /><br />-   **0x0000000000000001**. Указывает, что секции компьютер необходим для правильной.<br />-   **0x8000000000000000**. Указывает, что раздел не получает букву диска по умолчанию, при перемещении диска на другой компьютер, или когда диск будет доступно в первый раз компьютер.<br />-   **0x4000000000000000**. Скрывает тома секции. То есть секции не будут определяться с помощью диспетчера подключений.<br />-   **0x2000000000000000**. Указывает, что секции создается теневая копия другой секции.<br />-   **0x1000000000000000**. Указывает, что раздел является только для чтения. Этот атрибут запрещает, записываемый тома.<br /><b />Дополнительные сведения об этих атрибутах см. раздел «атрибуты» [create_PARTITION_PARAMETERS структуры](https://go.microsoft.com/fwlink/?LinkId=203812) (<https://go.microsoft.com/fwlink/?LinkId=203812>). |
> 
> ## <a name="remarks"></a>Примечания
> - Системный раздел EFI содержит только файлы, необходимые для запуска операционной системы. Это упрощает для двоичных файлов OEM или определенным двоичных файлов операционной системы должно быть помещено в других секциях.
> - В раздел basic gpt необходимо выбрать для выполнения данной операции. Используйте **выберите секцию** команду, чтобы выбрать раздел gpt основные и перетянуть внимание к нему.
>   ## <a name="BKMK_examples"></a>Примеры
>   Если при перемещении gpt-диск на новом компьютере и хотите запретить автоматическое назначение буквы диска для раздела, имеющего фокус, тип компьютера:
>   ```
>   gpt attributes=0x8000000000000000
>   ```
