---
title: pnpunattend
description: Узнайте, как аудит драйверов устройств на компьютере, а также выполнять драйвер автоматической установки.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4fa88932-cff0-4dfc-936c-98c0e3dfbeb8 britw
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: 53b72459d497ac5d079336c2a00ba65634b2e3a6
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/31/2019
ms.locfileid: "66436333"
---
# <a name="pnpunattend"></a>pnpunattend

Проверяет компьютер, для драйверов устройств и драйвер автоматической установки или поиска без установки драйверов и, при необходимости передачи результатов в командную строку. Эта команда используется для указания установки специальные драйверы для конкретных устройств. См. "Примечания".

## <a name="syntax"></a>Синтаксис

```
PnPUnattend.exe auditSystem [/help] [/?] [/h] [/s] [/L]
```

## <a name="parameters"></a>Параметры

|Параметр|Описание|
|---------|-----------|
|auditSystem|Задает установки драйвера в сети.</br>Требуется, кроме случая, когда **pnpunattend** выполняется с помощью **/Help** или **/?** параметры.|
|/s|Необязательно. Указывает на поиск драйверов без установки.|
|/L|Необязательный. Указывает, чтобы отобразить данные журнала для этой команды в командной строке.|
|/?|Необязательно. Отображает справку для этой команды в командной строке.|

## <a name="remarks"></a>Примечания

Предварительная подготовка является обязательным. Перед использованием этой команды, необходимо выполнить следующие задачи:

1. Создайте каталог для драйверов, который вы хотите установить. Например, создайте папку в **C:\Drivers\Video** драйверы видеоадаптера.
2. Загрузите и извлеките пакет драйвера устройства. Скопируйте содержимое во вложенную папку, содержащую файл INF для вашей версии операционной системы и все вложенные папки видео созданную папку. Например скопируйте файлы видеодрайвера C:\Drivers\Video.
3. Добавьте системную переменную среды path в папку, созданную в шаге 1. Например, **C:\Drivers\Video**.
4. Создайте следующий раздел реестра, а затем для **DriverPaths** установлен ключ, вы создаете, **значение** для **1**.
5. Для Windows® 7 перейдите по пути реестра: **HKEY_LOCAL_Machine\Software\Microsoft\Windows NT\CurrentVersion\\** , а затем создать ключи: **UnattendSettings\PnPUnattend\DriverPaths\\**
6. Для Windows Vista перейдите по пути реестра: **HK_LM\Software\Microsoft\Windows NT\CurrentVersion\\** , а затем создать ключи = **\UnattendSettings\PnPUnattend\DriverPaths**.

## <a name="examples"></a>Примеры

Например, следующая команда показывает использование **PNPUnattend.exe** для аудита компьютеров для обновления драйверов, возможно, так и результаты в командную строку.

```
pnpunattend auditsystem /s /l 
```

## <a name="additional-references"></a>Дополнительная справка

[Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)