---
title: Get-Аллсерверс
description: Справочный раздел по Get-Аллсерверс, который извлекает сведения обо всех серверах служб развертывания Windows.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: fe2e3c69-8f2e-457d-af55-d249ebf70f53
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b623b5e95e2a57147b7d9d191d42556191dd8e4d
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/01/2020
ms.locfileid: "82719981"
---
# <a name="get-allservers"></a>Get-Аллсерверс

Извлекает сведения обо всех серверах служб развертывания Windows.

> [!NOTE]
> Выполнение этой команды может занять продолжительное время, если в среде имеется много серверов служб развертывания Windows или если сетевое подключение к серверу работает слишком долго.

## <a name="syntax"></a>Синтаксис

```
WDSUTIL [Options] /Get-AllServers /Show:{Config | Images | All} [/Detailed] [/Forest:{Yes | No}]
```

### <a name="parameters"></a>Параметры

|   Параметр   |                                                                                                                 Описание                                                                                                                  |
|---------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| /Show: {config |                                                                                                                    Образы                                                                                                                    |
|  [/Детаилед]  | При использовании в сочетании с параметром **/Show: Images** или **/Show: ALL**возвращает все метаданные образа из каждого изображения. Если параметр **/детаилед** не указан, по умолчанию возвращается имя образа, описание и имя файла. |
| [/Forest: {Да |                                                                                                                     Нет}]                                                                                                                     |

## <a name="examples"></a>Примеры

Чтобы просмотреть сведения обо всех серверах, введите:
```
WDSUTIL /Get-AllServers /Show:Config
```
Чтобы просмотреть подробные сведения обо всех серверах, введите:
```
WDSUTIL /Verbose /Get-AllServers /Show:All /Detailed /Forest:Yes
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)