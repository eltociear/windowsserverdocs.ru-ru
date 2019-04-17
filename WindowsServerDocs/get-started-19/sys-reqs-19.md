---
title: Требования к системе Windows Server 2019 г.
description: Минимальные требования к хранилищу, ЦП, сети, памяти и ОЗУ при чистой установке Windows Server 2019.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: server-general
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4a8b42d7-9fe5-4efe-9ea1-ace2131f860e
author: coreyp-at-msft
ms.author: coreyp
manager: jasgroce
ms.localizationpriority: medium
ms.openlocfilehash: 82a42cd219e41330fe4215124c21e799a41e412c
ms.sourcegitcommit: fcc26ec5a2cc73b59c5752377b39c070d288655e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/19/2018
ms.locfileid: "8976660"
---
# Системные требования

>Область применения: Windows Server 2019 

В этом разделе описаны минимальные системные требования для запуска Windows Server&reg; 2019 г.

## Обзор требований к системе  
Ниже указаны примерные системные требования Windows Server 2019. Если компьютер не удовлетворяет минимальным требованиям, то правильно установить продукт будет невозможно. Фактические требования зависят от конфигурации системы и устанавливаемых приложений и компонентов.

Если не указано иное, эти минимальные системные требования применяются ко всем вариантам установки (основные серверные компоненты, сервер с рабочим столом и сервер Nano Server), а также к выпускам Standard и Datacenter.  

> [!IMPORTANT]  
> Возможные варианты развертывания столь разнообразны, что невозможно дать универсальные рекомендации по требованиям к системе. Чтобы подробнее узнать о ресурсах, необходимых для каждой развертываемой роли сервера, обратитесь к документации по этой роли. Выполните тестовое развертывание, чтобы определить подходящие требования к системе в конкретном сценарии. Это позволит добиться оптимального результата.  


## Процессор  
Производительность процессора зависит не только от тактовой частоты, но также от количества его ядер и размера кэша. Ниже указаны требования к процессору для данного продукта.  

**Минимальные требования**  
- 64-разрядный процессор с тактовой частотой 1,4 ГГц  
- Совместимый с набором инструкций для архитектуры х64  
- Поддержка технологий NX и DEP  
- Поддержка CMPXCHG16b, LAHF/SAHF и PrefetchW  
- Поддержка преобразования адресов второго уровня (EPT или NPT)  

[Coreinfo](https://technet.microsoft.com/sysinternals/cc835722.aspx) — это средство позволяет проверить, какие из этих возможностей обладает ваш ЦП.

## ОЗУ  
Ниже указаны примерные требования к ОЗУ для данного продукта.  

**Минимальные требования**  
- 512МБ (2ГБ для варианта установки "Сервер с рабочим столом")
- Тип ECC (код исправления ошибок) или аналогичная технология, для развертываний физического узла

> [!IMPORTANT]  
> Если вы создадите виртуальную машину с минимальными поддерживаемыми параметрами оборудования (1 ядро процессора и ОЗУ объемом 512 МБ) и затем попытаетесь установить этот выпуск на виртуальной машине, установка завершится ошибкой.  
>   
> Чтобы этого не случилось, выполните одно из указанных ниже действий.  
>   
> -   Выделите виртуальной машине, на которой планируется установить данный выпуск, более 800 МБ ОЗУ. По завершении установки можно уменьшить этот объем до 512 МБ в зависимости от реальной конфигурации сервера.  
> -   Прервите процесс загрузки данного выпуска на виртуальной машине, нажав клавиши SHIFT+F10. Используйте программу Diskpart.exe в открывшейся командной строке, чтобы создать и отформатировать раздел для установки. Запустите **Wpeutil createpagefile /path=C:\pf.sys** (предполагается, что созданный вами раздел для установки — C:). Закройте окно командной строки и продолжите установку.  

## Требования к контроллеру запоминающего устройства и пространству на диске  
Компьютеры под управлением Windows Server 2019 необходимо включить адаптер хранения, соответствующий спецификации архитектуры PCI Express. Устройства постоянного хранения на серверах, классифицируемые как жесткие диски, не должны быть устройствами PATA. Windows Server 2019 не позволяет ATA/PATA/IDE и EIDE для загрузки, страницы или дисков с данными.  

Ниже указаны примерные **минимальные** требования к свободному месту на диске для системного раздела.  

**Минимальные требования**: 32 ГБ  

   > [!NOTE]  
    > Обратите ванимание, что 32ГБ— это *абсолютный минимум* для успешной установки. Этот минимум должен позволять установить Windows Server 2019 в режиме Server Core с ролью сервера веб-служб (IIS). Сервер в режиме установки основных серверных компонентов примерно на 4 ГБ меньше, чем тот же сервер с графическим пользовательским интерфейсом. 
    >   
    > В любом из следующих случаев потребуется дополнительное место для системного раздела.  
    >   
    > -   Система устанавливается по сети.  
    > -   Для компьютеров с объемом ОЗУ более 16 ГБ потребуется больше места на диске для файлов подкачки, гибернации и дампа.  

## Требования к сетевому адаптеру  

Сетевые адаптеры, используемые в этом выпуске, должны включать следующие компоненты.  

**Минимальные требования**  
- Адаптер Ethernet с пропускной способностью не менее 1ГБ.  
- Совместимость со спецификацией архитектуры PCI Express.  

Сетевой адаптер с поддержкой сетевой отладки (KDNet) может пригодиться, но не входит в минимальные требования.   

Сетевой адаптер, что поддерживает функциональность будет полезна предзагрузочной среды выполнения (PXE), но не в минимальные требования.



## Другие требования  
Компьютеры под управлением этого выпуска также должны содержать следующие компоненты.  

-   Дисковод DVD-дисков (если операционная система будет устанавливаться с DVD-диска)  

Следующие элементы не являются безусловно обязательными, но необходимы для некоторых компонентов.  

- Система UEFI на основании версии 2.3.1c и встроенное ПО с поддержкой безопасной загрузки.  
- Доверенный платформенный модуль  

-   Графическое устройство и монитор Super VGA (1024 x 768) или с более высоким разрешением.  

-   Клавиатура и мышь Microsoft&reg; (или другое совместимое указывающее устройство).  

-   Доступ к Интернету (может потребоваться дополнительная оплата)  

>[!NOTE]  
> Микросхема доверенного платформенного модуля (TPM) не является обязательным требованием для установки данного выпуска, однако она необходима для использования определенных функций, таких как шифрование диска BitLocker. Если компьютер использует доверенный платформенный модуль, он должен соответствовать следующим требованиям.  
>  
>- Аппаратный доверенный платформенный модуль должен иметь спецификации доверенного платформенного модуля версии 2.0.  
>- Доверенные платформенные модули, реализующие версию 2.0, должны иметь сертификат EK, который должен быть либо предварительно подготовлен для доверенного платформенного модуля поставщиком оборудования, либо поддерживать получение устройством во время первой загрузки.  
>- Доверенные платформенные модули, которые реализуют версию 2.0, должны поставляться с банками PCR SHA-256 и реализовывать PCR от 0 до 23 для SHA-256. Допускается поставка доверенных платформенных модулей с одним переключаемым банком PCR, который может использоваться для измерений как SHA-1, так и SHA-256.  
>- Параметр UEFI, запрашивающий выключение доверенного платформенного модуля, не является обязательным требованием.  