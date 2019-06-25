---
title: Обновление Windows Server 2008 и Windows Server 2008 R2
description: Поддержка Windows Server 2008 и 2008 R2 будет прекращена. Узнайте, как выполнить обновление в локальной среде или разместить их в Azure.
ms.prod: windows-server-threshold
ms.mktglfcycl: manage
ms.sitesec: library
author: mikeblodge
ms.author: mikeblodge
ms.date: 07/12/2018
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.localizationpriority: high
ms.openlocfilehash: 9d8a8cae62a9be3384c09009dbad52e06623adb0
ms.sourcegitcommit: 8ba2c4de3bafa487a46c13c40e4a488bf95b6c33
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/25/2019
ms.locfileid: "66222912"
---
# <a name="upgrade-windows-server-2008-and-windows-server-2008-r2"></a>Обновление Windows Server 2008 и Windows Server 2008 R2

Расширенная поддержка для Windows Server 2008 и Windows Server 2008 R2 закончится 14 января 2020 г. Существует два пути модернизации: Локальное обновление или миграция путем повторного размещения в Azure. **Если повторное размещение в Azure, вы можете перенести существующие образы Server бесплатно.**

![Блок-схема с описанием путей обновления Windows Server 2008](media/WS08_upgrade_paths.png)


## <a name="on-premises-upgrade"></a>Локальное обновление
Если требуется оставить серверы в локальной среде и если вы используете Windows Server 2008 или Windows Server 2008 R2, необходимо будет выполнить [обновление до Windows Server 2012/2012 R2](installation-and-upgrade.md#upgrading-to-windows-server-2012-r2), прежде чем вы сможете выполнить [обновление до Windows Server 2016](installation-and-upgrade.md#upgrading-to-windows-server-2016). В ходе обновления у вас останется возможность выполнить перенос в Azure путем повторного размещения.

Дополнительные сведения о вариантах локального обновления см. в разделе [Обновление с Windows Server 2008 R2 или Windows Server 2008](installation-and-upgrade.md#upgrading-from-windows-server-2008-r2-or-windows-server-2008).

Если вы используете Windows Server 2003, необходимо выполнить [обновление до Windows Server 2008](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff972408(v%3dws.10)). Дополнительные сведения о вариантах локального обновления см. в разделе [Пути обновления для Windows Server 2008](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd979563(v=ws.10)).


## <a name="migrate-to-azure"></a>Перенос в Azure
Можно выполнить перенос локальных серверов Windows Server 2008 и Windows Server 2008 R2 в Azure и продолжить использовать их на виртуальных машинах. В Azure вы сохраните соответствие нормативным требованиям, повысите уровень защиты и сможете использовать в своей работе преимущества облачных технологий. Преимущества переноса в Azure.

- Обновления системы безопасности в Azure.
- В течение трех дополнительных лет вы будете получать важные обновления системы безопасности для Windows Server 2008 R2 или 2008 без дополнительной платы. 
- Бесплатные обновления в Azure.
- Внедрение дополнительных облачных служб по мере готовности.
- При переносе SQL Server в управляемые экземпляры Azure или на виртуальные машины в течение трех дополнительных лет вы будете получать важные обновления системы безопасности для Windows Server 2008 R2 или 2008 без дополнительной платы. 
- Используйте имеющиеся лицензии на SQL Server и Windows Server для экономии на облачных ресурсах только при использовании Azure.

[![Запуск миграции в Azure с помощью специализированного образа](./media/WS08-image-banner-small.png)](uploading-specialized-WS08-image-to-azure.md)

Чтобы приступить к переносу, см. раздел [Отправка специализированного образа Windows Server 2008 или 2008 R2 в Azure](uploading-specialized-WS08-image-to-azure.md).

Чтобы понять, как анализировать имеющиеся ИТ-ресурсы, оценить то, что у вас уже есть, выделить преимущества переноса конкретных служб и приложений в облако по сравнению с сохранением рабочих нагрузок в локальной среде, а также понять, какую выгоду вы получите от обновления до последней версии Windows Server, см. раздел [Руководство по переносу для Windows Server](https://go.microsoft.com/fwlink/?linkid=872689).

## <a name="upgrade-sql-server-20082008-r2-in-parallel-with-your-windows-servers"></a>Обновление SQL Server 2008 или 2008 R2 параллельно с серверами Windows Server

![Логотип SQL Server](media/sqlr2.jpg)

Если вы используете SQL Server 2008 или 2008 R2, вы можете выполнить обновление до SQL Server [2016](https://docs.microsoft.com/sql/sql-server/sql-server-technical-documentation?view=sql-server-2016) или [2017](https://docs.microsoft.com/sql/sql-server/sql-server-technical-documentation?view=sql-server-2017).


## <a name="additional-resources"></a>Дополнительные ресурсы
[Microsoft Azure](https://docs.microsoft.com/azure/#pivot=products)