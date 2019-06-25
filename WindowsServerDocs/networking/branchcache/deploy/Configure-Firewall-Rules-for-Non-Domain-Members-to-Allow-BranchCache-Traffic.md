---
title: Настройка правил брандмауэра для элементов, не входящих в домен, для разрешения трафика BranchCache
description: Этот раздел является частью BranchCache развертывания руководство для Windows Server 2016, который показывает, как развернуть BranchCache в режимах распределенный и размещенный кэш, чтобы оптимизировать использование пропускной способности глобальной сети в филиалах
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: da956be0-c92d-46ea-99eb-85e2bd67bf07
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 288865f0237969e0bed7e105f8d539759984275e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2019
ms.locfileid: "59834775"
---
# <a name="configure-firewall-rules-for-non-domain-members-to-allow-branchcache-traffic"></a>Настройка правил брандмауэра для элементов, не входящих в домен, для разрешения трафика BranchCache

>Относится к: Windows Server (полугодовой канал), Windows Server 2016

Сведения этого раздела можно использовать для настройки брандмауэра продукты сторонних производителей и вручную настроить клиентский компьютер с помощью правил брандмауэра, разрешающих BranchCache в режиме распределенного кэша.  
  
> [!NOTE]  
> -   Если вы настроили клиентских компьютеров BranchCache, с помощью групповой политики, параметры групповой политики переопределяют любые ручные настройки клиентских компьютеров, к которым применены политики.  
> -   Если вы развернули BranchCache с помощью DirectAccess, можно использовать параметры в этом разделе для настройки правила IPsec, чтобы разрешить трафик BranchCache.  
  
Членство в группе **Администраторы**, или эквивалентной является минимальным требованием для внесения изменений в конфигурацию.  
  
## <a name="ms-pccrd-peer-content-caching-and-retrieval-discovery-protocol"></a>[MS-PCCRD]: Кэширование содержимого для однорангового узла и протокол обнаружения извлечения  
Распределенного кэша клиенты необходимо разрешить входящий и исходящий трафик MS-PCCRD, включенный в протоколе динамического обнаружения веб-служб (WS-Discovery).  
  
Параметры брандмауэра необходимо разрешить трафик многоадресной рассылки в дополнение к входящего и исходящего трафика. Можно использовать следующие параметры для настройки исключений брандмауэра для режима распределенного кэша.  
  
IPv4 многоадресной рассылки: 239.255.255.250  
  
Многоадресной рассылки IPv6: FF02::C  
  
Входящий трафик: Локальный порт: 3702, удаленный порт: временные  
  
Исходящий трафик: Локальный порт: временные, удаленный порт: 3702  
  
Программа: %systemroot%\system32\svchost.exe (Служба BranchCache [PeerDistSvc])  
  
## <a name="ms-pccrr-peer-content-caching-and-retrieval-retrieval-protocol"></a>[MS-PCCRR]: Кэширование содержимого для однорангового узла и извлечения: Протокол извлечения  
Клиенты распределенного кэша необходимо разрешить входящий и исходящий трафик MS PCCRR, который переносится в протоколе HTTP 1.1, как описано в документах (RFC) 2616.  
  
Параметры брандмауэра необходимо разрешить входящий и исходящий трафик. Можно использовать следующие параметры для настройки исключений брандмауэра для режима распределенного кэша.  
  
Входящий трафик: Локальный порт: 80, удаленный порт: временные  
  
Исходящий трафик: Локальный порт: временные, удаленный порт: 80  
  

