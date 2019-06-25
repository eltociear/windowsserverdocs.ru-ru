---
ms.assetid: 133474ee-316d-4b1c-acc6-ad5434a064d5
title: Общие сведения о понятиях DNS
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/08/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: d077ecc30caca9b8f3b382af624121fec729afae
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2019
ms.locfileid: "59890505"
---
# <a name="reviewing-dns-concepts"></a>Общие сведения о понятиях DNS

>Область применения. Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Система доменных имен (DNS) — это распределенная база данных, который представляет собой пространство имен. Пространство имен содержит все сведения, необходимые для любого клиента для поиска любого имени. Любой DNS-сервер может отвечать на запросы о любое имя в его пространстве имен. DNS-сервер отвечает на запросы в одном из следующих способов:  
  
- Если ответ в своем кэше, он отвечает на запрос из кэша.  
- Если ответ в зоне, размещенной на DNS-сервере, он отвечает на запрос из зоны. Зона является частью дерева DNS, хранящиеся на DNS-сервер. Когда DNS-сервер размещает зоны, он считается заслуживающим доверия, для имен в этой зоне (то есть DNS-сервер может отвечать на запросы для любое имя зоны). Например сервер, где размещены в зоне contoso.com могут отвечать на запросы по любому имени в contoso.com.  
- Если сервер не может ответить на запрос из кэша или зоны, он запрашивает другие серверы для ответа.  

Важно понимать основные функции службы DNS, например делегирования, рекурсивного разрешения имен и зон DNS, интегрированный с Active Directory, так как они имеют непосредственное влияние на разработку логической структуры Active Directory.  
  
Дополнительные сведения о DNS и доменными службами Active Directory (AD DS), см. в разделе [DNS и AD DS](../../ad-ds/plan/DNS-and-AD-DS.md).  
  
## <a name="delegation"></a>Делегирование

Для DNS-сервера для ответа на запросы о любое имя он должен быть прямой или косвенный путь к каждой зоне в пространстве имен. Эти пути создаются с помощью делегирования. Делегирование — это запись в родительской зоне, в которой перечислены сервер доменных имен, заслуживающую доверия для зоны на следующем уровне иерархии. Делегирование делают возможным для серверов в одной зоне, чтобы направлять клиентов к серверам в других зонах. Ниже показан пример делегирования.  
  
![Основные понятия DNS](../../media/Reviewing-DNS-Concepts/0c24b576-d41a-4e5d-ad3d-6be81e095835.gif)  
  
Корневой сервер DNS размещена корневая зона, представленное в виде точки (. ). Корневая зона содержит делегирование для зоны на следующем уровне иерархии, зона com. Делегирование в корневой зоне указывает, что корневой сервер DNS, чтобы найти зона com, должен связаться COM-сервера. Аналогичным образом делегирование в зоне com сообщает COM-сервера, что, чтобы найти зону contoso.com, должен связаться Contoso server.  
  
> [!NOTE]  
> Делегирование использует два типа записей. Имя записи ресурса сервера (NS) предоставляет имя полномочный сервер. Узла (A) и записи ресурсов узла (AAAA) укажите IP версии 4 (IPv4) и IP версии 6 (IPv6) адреса полномочный сервер.  
  
Эта система зон и делегирования создает иерархическое дерево, которое представляет пространство имен DNS. Каждая зона представляет уровень в иерархии, а у каждого делегирования ветви дерева.  
  
С помощью иерархии зон и делегирования, корневой сервер DNS можно найти в пространстве имен DNS любое имя. Корневая зона содержит делегирование, которые приводят к всех зон в иерархии прямо или косвенно. Любой сервер, который может выполнять запросы корневой сервер DNS можно использовать информацию в делегирования найти любое имя в пространстве имен.  
  
## <a name="recursive-name-resolution"></a>Рекурсивного разрешения имен

Рекурсивного разрешения имен — это процесс, по которому DNS-сервер использует иерархию зон и делегирования для ответа на запросы, для которых он не является полномочным.  
  
В некоторых конфигурациях DNS-серверы включают корневые ссылки (то есть список имен и IP-адреса), которые позволяют запрашивать корневые DNS-серверы. В других конфигурациях серверов перенаправлять все запросы, которые они не может ответить на другой сервер. Указания пересылки и корневых являются оба метода, которые можно использовать DNS-серверы для разрешения запросов, для которых они не заслуживающих доверия.  
  
### <a name="resolving-names-by-using-root-hints"></a>Разрешение имен с помощью корневых ссылок

Корневые ссылки включить любой DNS-сервер найти корневые DNS-серверы. После DNS-сервер обнаружения корневой сервер DNS, он может разрешать любого запроса для этого пространства имен. Ниже описывается, как служба DNS сопоставляет имя с помощью корневых ссылок.  
  
![Основные понятия DNS](../../media/Reviewing-DNS-Concepts/1c044845-b104-4262-a7af-474ba3558a85.gif)  
  
В этом примере происходят следующие события:  
  
1. Клиент отправляет рекурсивный запрос на DNS-сервер для запроса IP-адрес, соответствующий имени ftp.contoso.com. Рекурсивный запрос указывает, что клиент хочет окончательный ответ свой запрос. Ответ на рекурсивный запрос должен быть, является допустимым адресом или сообщение о том, что адрес не найден.  
2. Так как DNS-сервер не авторизован для имени и не имеет в своем кэше ответ, DNS-сервер использует корневые ссылки для поиска IP-адрес корневого сервера DNS.  
3. DNS-сервер использует итерационный запрос попросить корневой сервер DNS для разрешения имени ftp.contoso.com. Итерационный запрос указывает, что сервер принимает ссылку на другой сервер вместо окончательный ответ на запрос. Так как имя ftp.contoso.com заканчивается метка com, корневой сервер DNS возвращает ссылку на COM-сервера, на котором размещена зона com.  
4. DNS-сервер использует итерационный запрос попросить COM-сервера для разрешения имени ftp.contoso.com. Поскольку ftp.contoso.com имя заканчивается именем contoso.com, сервер Com возвращает ссылку на сервер Contoso, на котором размещается зона contoso.com.  
5. DNS-сервер использует итерационный запрос для запроса на сервере Contoso разрешение ftp.contoso.com имя. Contoso-server находит ответ в данных зоны и возвращает ответ на сервер.  
6. Затем сервер возвращает результат клиенту.  
  
### <a name="resolving-names-by-using-forwarding"></a>Разрешение имен с помощью переадресации

Пересылка позволяет маршрута разрешение имен через определенные серверы вместо использования корневых ссылок. Ниже описывается, как служба DNS сопоставляет имя с помощью переадресации.  
  
![Основные понятия DNS](../../media/Reviewing-DNS-Concepts/05bc2eb0-1033-4e53-ae30-244fa247d000.gif)  
  
В этом примере происходят следующие события:  
  
1. Клиент запрашивает DNS-сервер для ftp.contoso.com имя.  
2. DNS-сервер перенаправляет запрос на другой сервер DNS, известный как сервера пересылки.  
3. Так как сервер пересылки не является полномочным для имени и не имеет в своем кэше ответ, для поиска IP-адрес корневого DNS-сервера используется корневых ссылок.  
4. Сервер пересылки использует итерационный запрос попросить корневой сервер DNS для разрешения имени ftp.contoso.com. Так как имя ftp.contoso.com заканчивается именем com, корневой сервер DNS возвращает ссылку на COM-сервера, на котором размещена зона com.  
5. Сервер пересылки использует итерационный запрос попросить COM-сервера для разрешения имени ftp.contoso.com. Поскольку ftp.contoso.com имя заканчивается именем contoso.com, сервер Com возвращает ссылку на сервер Contoso, на котором размещается зона contoso.com.  
6. Сервер пересылки использует итерационный запрос для запроса на сервере Contoso разрешение ftp.contoso.com имя. Сервер Contoso находит ответ в файлах зоны и возвращает ответ на сервер.  
7. Затем сервер пересылки возвращает результат на исходный сервер DNS.  
8. Затем исходный сервер DNS возвращает результат клиенту.  