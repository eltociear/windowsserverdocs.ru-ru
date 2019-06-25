---
title: Обзор сценария лаборатории тестирования
description: Этот раздел входит руководство по лаборатории тестирования — продемонстрировать DirectAccess многосайтового развертывания для Windows Server 2016
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9afeced4-1a9b-4cb3-9fc4-d7e44c675755
ms.author: pashort
author: shortpatti
ms.openlocfilehash: b067d5f247f5dc13ea294d83a76f267c5a57ffe7
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/20/2019
ms.locfileid: "67283300"
---
# <a name="overview-of-the-test-lab-scenario"></a>Обзор сценария лаборатории тестирования

>Область применения. Windows Server (полугодовой канал), Windows Server 2016

В этом сценарии лаборатории тестирования DirectAccess развертывается с помощью:  
  
-   **DC1**- сервере, настроенном в качестве контроллера домена, DNS-сервер и DHCP-сервер для домена corp.contoso.com.  
  
-   **2-DC1**- сервере, настроенном в качестве контроллера домена и DNS-сервер для домена corp2.corp.contoso.com.  
  
-   **EDGE1 и 2 EDGE1**— два сервера во внутренней сети, настроенных как серверы удаленного доступа. Каждый сервер имеет два сетевых адаптера; один из которых подключен к внутренней сети, а второй к внешней сети.  
  
-   **App1 и 2-APP1**— два сервера во внутренней сети, настроенные в качестве файла и веб-серверов.  
  
-   **APP2**— компьютер во внутренней сети, настроенный в качестве IPv4 только веб- и файловым сервером. Этот компьютер используется для описания возможностей NAT64/DNS64.  
  
-   **ROUTER1**- сервер настроен для маршрутизации между двумя сетями корпоративной внутренней.  
  
-   **INET1**- сервере, настроенном в качестве Internet DNS и DHCP-сервера.  
  
-   **NAT1**- клиентский компьютер, настроенный в качестве сетевого адреса translator (NAT) устройства с помощью подключения к Интернету.  
  
-   **CLIENT1 и CLIENT2**-двух клиентских компьютеров, настроенных как клиенты DirectAccess, которые будут использоваться для проверки подключения DirectAccess при перемещении между внутренней сети, смоделированной сети Интернет и домашней сети. **CLIENT2** является в Windows 7&reg; клиента.  
  
Лаборатория тестирования включает четыре подсети, которые имитируют следующее:  
  
-   Домашняя сеть с именем Homenet (192.168.137.0/24) подключен к Интернету, NAT.  
  
-   Внешние сети, представленного подсети Интернет (131.107.0.0/24).  
  
-   Внутренняя сеть с именем Corpnet (10.0.0.0/24; 2001:db8:1:: / 64) разделенные сервера удаленного доступа EDGE1 из Интернета.  
  
-   Внутренняя сеть с именем 2 Corpnet1 (10.2.0.0/24; 2001:db8:2:: / 64) разделенные 2 EDGE1 сервера удаленного доступа из Интернета.  
  
Компьютеры в каждой подсети подключаются, с помощью физических или виртуальных концентратора или коммутатора, как показано на рисунке ниже.  
  
![Обзор лаборатории тестирования](../../../media/Overview-of-the-Test-Lab-Scenario_4/TLG_DA_Multisite.png)  
  

