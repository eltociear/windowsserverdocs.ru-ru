---
title: Экранированные виртуальные машины для клиентов — развертывание экранированной виртуальной машины с помощью Windows Azure Pack
ms.prod: windows-server
ms.topic: article
ms.assetid: 095315e4-c4a7-4b80-91d8-528119b62c4c
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: ce3aac47ea6c44abd1811efc1e23b901f53333bb
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/08/2020
ms.locfileid: "80856467"
---
# <a name="shielded-vms--for-tenants---deploying-a-shielded-vm-by-using-windows-azure-pack"></a>Экранированные виртуальные машины для клиентов — развертывание экранированной виртуальной машины с помощью Windows Azure Pack

>Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016

Если поставщик услуг размещения поддерживает его, можно использовать Windows Azure Pack для развертывания экранированной виртуальной машины.

Выполните следующие действия.

1. Подпишитесь на один или несколько планов, предлагаемых в Windows Azure Pack.

2. Создайте экранированную виртуальную машину с помощью Windows Azure Pack.

    [Используйте экранированные виртуальные машины](https://technet.microsoft.com/library/mt720674.aspx), которые описаны в следующих разделах:

   - [Создайте данные экранирования](https://technet.microsoft.com/library/mt720672.aspx) (и отправьте файл данных экранирования, как описано во второй процедуре в разделе).
    
     > [!NOTE]
     > В процессе создания данных экранирования будет скачан файл ключа защитника, который будет XML-файлом в формате UTF-8. Не изменяйте файл на UTF-16.
    
   - [Создание экранированной виртуальной машины](https://technet.microsoft.com/library/mt720673.aspx) с **быстрым созданием**через экранированный шаблон или обычным шаблоном.
    
       > [!WARNING]
       > Если вы [создаете экранированную виртуальную машину с помощью обычного шаблона](https://technet.microsoft.com/library/mt720673.aspx#Anchor_2), важно отметить, что виртуальная машина подготовлена в *неэкранированном*виде. Это означает, что диск шаблона не проверяется по списку доверенных дисков в файле данных экранирования и не является секретами в файле данных экранирования, используемом для подготовки виртуальной машины. Если экранированный шаблон доступен, предпочтительнее развернуть экранированную виртуальную машину с экранированным шаблоном, чтобы обеспечить сквозную защиту секретов.
    
   - [Преобразование виртуальной машины версии 2 в экранированную виртуальную машину](https://technet.microsoft.com/library/mt720670.aspx)
    
       > [!NOTE]
       > При преобразовании виртуальной машины в экранированную виртуальную машину существующие контрольные точки и резервные копии не шифруются. Старые контрольные точки следует удалять по возможности, чтобы предотвратить доступ к старым, расшифрованным данным.

## <a name="see-also"></a>См. также:

- [Этапы настройки поставщика услуг размещения для защищенных узлов и экранированных виртуальных машин](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md)
- [Защищенная структура и экранированные виртуальные машины](guarded-fabric-and-shielded-vms-top-node.md)
