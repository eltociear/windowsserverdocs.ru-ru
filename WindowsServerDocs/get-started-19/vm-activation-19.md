---
title: Автоматическая активация виртуальной машины
TOCTitle: Automatic VM Activation
description: Активация виртуальных машин в Windows Server 2019, Windows Server 2016 и Windows Server 2012 R2
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: server-general
ms.tgt_pltfrm: na
ms.topic: article
author: lizap
ms.author: elizapo
ms.localizationpriority: medium
ms.openlocfilehash: 18e20433050371dc02782fb8630a885e53ae31ad
ms.sourcegitcommit: 2977c707a299929c6ab0d1e0adab2e1c644b8306
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/24/2019
ms.locfileid: "63688707"
---
# <a name="automatic-virtual-machine-activation"></a>Автоматическая активация виртуальной машины

> Относится к: Windows Server 2019 г., Windows Server Semi-Annual Channel, Windows Server 2016, Windows Server 2012 R2

Автоматическая активация виртуальной машины (AVMA) — это механизм подтверждения законности приобретения, помогающий удостовериться, что продукты Windows используются в соответствии с правами на использование продуктов и условиями лицензионного соглашения на использование программного обеспечения корпорации Майкрософт.

AVMA позволяет устанавливать виртуальные машины на сервере с должным образом активированной ОС Windows, не настраивая ключи продукта для каждой виртуальной машины, даже в отключенных средах. Она привязывает активацию виртуальной машины к лицензированному серверу виртуализации и активирует виртуальную машину при запуске. AVMA также предоставляет отчеты по использованию в реальном времени и данные о состоянии лицензии виртуальной машины за прошлые периоды. Отчеты и данные отслеживания доступны на сервере виртуализации.

## <a name="practical-applications"></a>Практическое применение

AVMA предоставляет ряд преимуществ на серверах виртуализации, активированных с использованием корпоративного лицензирования или лицензирования OEM.

Администраторы серверов в центрах обработки данных могут использовать AVMA для выполнения следующих действий:

  - Активация виртуальных машин в удаленных расположениях

  - Активация виртуальных машин с подключением к Интернету или без него

  - Отслеживание данных об использовании и лицензиях виртуальных машин с сервера виртуализации без прав доступа к виртуализованным системам

Не требуется управлять ключами продукта и читать наклейки на серверах. Виртуальная машина активируется и продолжает работать даже при переносе в массиве серверов виртуализации.

Партнеры по лицензионному соглашению поставщика услуг (SPLA) и другие поставщики услуг размещения не обязаны предоставлять ключи продукта клиентам или активировать виртуальные машины клиентов. С помощью AVMA клиенты могут легко активировать виртуальные машины. Поставщики услуг размещения могут использовать журналы сервера для проверки соответствия лицензии и отслеживания хронологии использования клиента.

## <a name="system-requirements"></a>Системные требования

AVMA требуется, чтобы сервер виртуализации Майкрософт под управлением Windows Server 2019 Datacenter, Windows Server 2016 Datacenter или Windows Server 2012 R2. 

Ниже приведены Гости, которые могут активироваться узлы другой версии.

|Версия сервера узла|Windows Server 2019|Windows Server 2016|Windows Server 2012 R2|
|-|-|-|-|
|Windows Server 2019|X|X|X|
|Windows Server 2016| |X|X|
|Windows Server 2012 R2| ||X|

Обратите внимание на то, что они активировать все выпуски (Datacenter, Standard и Essentials).

Это средство не работает с другими технологиями виртуализации сервера.

## <a name="how-to-implement-avma"></a>Реализация AVMA

1.  На сервере виртуализации Windows Server Datacenter установите и настройте роль Microsoft Hyper-V Server. Дополнительные сведения см. в разделе [Установка Hyper-V Server](../virtualization/hyper-v/get-started/install-the-hyper-v-role-on-windows-server.md).

2.  [Создание виртуальной машины](../virtualization/hyper-v/get-started/create-a-virtual-machine-in-hyper-v.md) и установить в поддерживаемой операционной системе на нее.

3.  Установите ключ AVMA на виртуальной машине. В командной строке с повышенными привилегиями введите следующую команду:
    
    ``` 
    slmgr /ipk <AVMA_key>  
    ```

Виртуальная машина автоматически активирует лицензию в соответствии с сервером виртуализации.


> [!TIP]
> Можно также использовать ключи AVMA в любом файле установки Unattend.exe.


## <a name="avma-keys"></a>Ключи AVMA

Перечисленные ниже ключи AVMA можно использовать для Windows Server 2019.

|Выпуск|   Ключ AVMA|
|-|-|
|Datacenter|    H3RNG-8C32Q-Q8FRX-6TDXV-WMBMW|
|Standard|  TNK62-RXVTB-4P47B-2D623-4GF74|
|Essentials|    2CTP7-NHT64-BP62M-FV6GG-HFV28|
 
Перечисленные ниже ключи AVMA можно использовать для Windows Server версии 1809.

|Выпуск|   Ключ AVMA|
|-|-|
|Datacenter|    H3RNG-8C32Q-Q8FRX-6TDXV-WMBMW|
|Standard|  TNK62-RXVTB-4P47B-2D623-4GF74|

Перечисленные ниже ключи AVMA можно использовать для Windows Server версии 1803 и 1709.

|Выпуск|Ключ AVMA|
|-|-|
|Datacenter|TMJ3Y-NTRTM-FJYXT-T22BY-CWG3J|
|Standard|C3RCX-M6NRP-6CXC9-TW2F2-4RHYD|


Перечисленные ниже ключи AVMA можно использовать для Windows Server 2016.

|Выпуск|Ключ AVMA|
|-|-|
|Datacenter|TMJ3Y-NTRTM-FJYXT-T22BY-CWG3J|
|Standard|C3RCX-M6NRP-6CXC9-TW2F2-4RHYD|
|Essentials|B4YNW-62DX9-W8V6M-82649-MHBKQ|


Перечисленные ниже ключи AVMA можно использовать для Windows Server 2012 R2.

|Выпуск|Ключ AVMA|
|-|-|
|Datacenter|Y4TGP-NPTV9-HTC2H-7MGQ3-DV4TW|
|Standard|DBGBW-NPF86-BJVTX-K3WKJ-MTB6V|
|Essentials|K2XGM-NMBT3-2R6Q8-WF2FK-P36R2|

## <a name="reporting-and-tracking"></a>Отчетность и отслеживание

Реестр (KVP) на сервере виртуализации предоставляет данные по отслеживанию в реальном времени для операционных систем на виртуальной машине. Поскольку раздел реестра перемещается вместе с виртуальной машиной, можно также получить информацию о лицензии. По умолчанию KVP возвращает данные о виртуальной машине, в том числе:

  - Полное доменное имя

  - Операционную систему и установленные пакеты обновления

  - Архитектуру процессора

  - Сетевые адреса IPv4 и IPv6

  - Адреса RDP

Дополнительные сведения о том, как получить эту информацию см. в разделе [Hyper-V сценария: Просмотр KVP guestintrinsicexchangeitems](http://blogs.msdn.com/b/virtual_pc_guy/archive/2008/11/18/hyper-v-script-looking-at-kvp-guestintrinsicexchangeitems.aspx).


> [!NOTE]
> Данные KVP не защищены. Они допускают модификации и не контролируются на предмет изменений.



> [!IMPORTANT]
> Данные KVP следует удалить в случае замены ключа AVMA другим ключом продукта (розничным, OEM или ключом корпоративного лицензирования).


Данные о запросах AVMA за прошлые периоды доступны в файле журнала на сервере виртуализации (EventID 12310).

Поскольку процесс активации AVMA прозрачен, сообщения об ошибках не отображаются. Однако данные о перечисленных ниже событиях записываются в файл журнала на виртуальных машинах (EventID 12309).

|Уведомление|Описание|
|-|-|
|AVMA успешна|Виртуальная машина активирована.|
|Недопустимый узел|Сервер виртуализации не отвечает. Это может произойти, когда на сервере не установлена поддерживаемая версия Windows.|
|Недопустимые данные|Это событие обычно возникает в результате сбоя связи между сервером виртуализации и виртуальной машиной, часто из-за повреждения, шифрования или несоответствия данных.|
|Отказано в активации|Серверу виртуализации не удалось активировать операционную систему на виртуальной машине из-за несоответствия идентификатора AVMA.|
