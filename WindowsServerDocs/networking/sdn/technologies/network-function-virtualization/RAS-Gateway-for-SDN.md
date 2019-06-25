---
title: Шлюз RAS-сервера для SDN
description: Дополнительные сведения о шлюз RAS, который основан на программное обеспечение, сред, маршрутизатор с поддержкой протокола пограничного шлюза (BGP) в Windows Server 2016 можно использовать в этом разделе.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a32357a5-ab1a-4a4c-848a-7a4ed65b1921
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 4f1ad0b3f0b5921a53faa8a45baae9f0b8711873
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2019
ms.locfileid: "59856275"
---
# <a name="ras-gateway-for-sdn"></a>Шлюз RAS-сервера для SDN

>Относится к: Windows Server (полугодовой канал), Windows Server 2016 ## шлюз RAS  


Шлюз RAS — на базе программного обеспечения, мультитенантную систему, маршрутизатор с поддержкой протокола пограничного шлюза (BGP) предназначен для поставщиков облачных служб (CSP) и предприятий, на которых размещены несколько виртуальных сетей клиента с помощью виртуализации сети Hyper-V. Шлюзов RAS осуществляет маршрутизацию сетевого трафика между физической сетью и ресурсами виртуальных Машин, независимо от расположения. Можно направлять сетевой трафик в том же физическом расположении или в различных местах.   

Многопользовательская архитектура платформы — это способность инфраструктуры облака обеспечивать рабочие нагрузки виртуальных машин нескольких клиентов, пока изолировать их друг от друга, хотя все рабочие нагрузки выполняются в одной инфраструктуре. Несколько рабочих нагрузок отдельного клиента могут быть связаны взаимоподключением и управляться удаленно, оставаясь отделенными от рабочих нагрузок других клиентов и не позволяя другим клиентам управлять ими.

  
> [!NOTE]  
> Помимо этой статьи доступны в следующих разделах шлюза RAS.  
>   
> -   [Новые возможности шлюза RAS](../../../sdn/technologies/network-function-virtualization/What-s-New-in-RAS-Gateway.md)  
> -   [Архитектура развертывания шлюза RAS](../../../sdn/technologies/network-function-virtualization/RAS-Gateway-Deployment-Architecture.md)  
> -   [Высокая доступность шлюза RAS](../../../sdn/technologies/network-function-virtualization/RAS-Gateway-High-Availability.md)  
> -   [Протокола пограничного шлюза &#40;BGP&#41;](../../../../remote/remote-access/bgp/Border-Gateway-Protocol-BGP.md)  
> -   [Справочник по командам PowerShell Windows BGP](../../../../remote/remote-access/bgp/BGP-Windows-PowerShell-Command-Reference.md)  
  
    
## <a name="prerequisites-for-installing-ras-gateway-for-sdn"></a>Необходимые условия для установки шлюза RAS для SDN  
Нельзя использовать интерфейс Windows для установки удаленного доступа, если вы хотите развернуть шлюз удаленного доступа в мультитенантном режиме для использования с SDN. Вместо этого необходимо использовать Windows PowerShell.  
  
Но перед установкой шлюза RAS с помощью Windows PowerShell, необходимо использовать Windows PowerShell для добавления **RemoteAccess** компонентов Windows. Чтобы сделать это, запустите следующую команду в командной строке Windows PowerShell.  
  
`Add-WindowsFeature -Name RemoteAccess -IncludeAllSubFeature -IncludeManagementTools`  
  
Эта команда добавляет **RemoteAccess** функции и команды Windows PowerShell для компонента.  
  
После добавления **RemoteAccess** на сервер удаленного доступа можно установить как шлюз удаленного доступа в мультитенантном режиме и протокола пограничного шлюза (BGP).  
  
Дополнительные сведения см. в разделе справки Windows PowerShell [Install-RemoteAccess](https://technet.microsoft.com/library/hh918408.aspx).  
  
## <a name="ras-gateway-features"></a>Функции шлюза RAS  
Ниже приведены возможности шлюза удаленного доступа в Windows Server 2016. Вы можете развернуть шлюз удаленного доступа в пулах высокий уровень доступности, использующих все эти возможности за один раз.  
  
-   **Сеть сеть VPN**. Эта функция шлюза RAS дает возможность подключения между двумя сетями в разных физических расположениях через Интернет с помощью VPN-подключение сайт сайт. Для поставщиков облачных решений, которые размещают в своем центре обработки данных множество клиентов шлюз RAS обеспечивает решение мультитенантного шлюза, который позволит вашим клиентам получить доступ к ресурсам и управлять ими через сеть сеть VPN-подключений с удаленных сайтов и позволяет потоком сетевого трафика между виртуальными ресурсами в вашем центре обработки данных и их физической сети.  
  
-   **Типа "точка сеть"**. Эта функция шлюза RAS позволяет сотрудникам организации или администраторов для подключения к корпоративной сети из удаленных расположений.  Для мультитенантных средах администраторы сети клиента можно использовать VPN-подключений точка сеть для доступа к ресурсам виртуальной сети в центре обработки данных CSP.  
  
-   **Туннелирование GRE**. Протоколом (GRE) на основе туннели обеспечивают подключение между виртуальными сетями клиентов и внешними сетями. Так как протокол GRE является упрощенным и поддерживается большинством сетевых устройств, он становится идеальным выбором для туннелирования в случаях, когда шифрование данных не требуется. Поддержка GRE в сеть — сеть (S2S) туннелях решает проблему перенаправления между виртуальными и внешними сетями клиента с помощью мультитенантного шлюза, как описано далее в этом разделе.  
  
-   **Динамическая маршрутизация с помощью протокола пограничного шлюза (BGP)**. Протокол BGP снижает потребность в ручной настройке маршрутов в маршрутизаторах, так как является протоколом динамической маршрутизации и автоматически определяет маршруты между сайтами, связанными с помощью межсайтовых подключений VPN. Если ваша организация использует несколько сайтов, подключенных с помощью маршрутизаторов с поддержкой BGP, например шлюз RAS, BGP позволяет маршрутизаторы автоматически вычислить и использовать допустимых маршрутов друг с другом в случае сбоя сети или сбоя. Дополнительные сведения см. в разделе [RFC 4271](https://tools.ietf.org/html/rfc4271).  
  

  

