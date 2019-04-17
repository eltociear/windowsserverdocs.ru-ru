---
title: Получение интеллектуальных ответов DNS на основе времени дня с помощью политики DNS
description: Этот раздел является частью DNS политики сценарий руководство для Windows Server 2016
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dns
ms.topic: article
ms.assetid: 161446ff-a072-4cc4-b339-00a04857ff3a
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 46821daff4a0046bf78d7f56dc7c5deabcc437e4
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/28/2018
---
# <a name="use-dns-policy-for-intelligent-dns-responses-based-on-the-time-of-day"></a>Получение интеллектуальных ответов DNS на основе времени дня с помощью политики DNS

>Область применения: Windows Server (канал точками годовой), Windows Server 2016

В этом разделе можно использовать, чтобы узнать, как для распределения трафика приложения по географически различных экземпляров приложения с помощью политики DNS, которые основаны на время дня.  
  
Этот сценарий полезен в ситуациях, где вы хотите направлять трафик в один часовой пояс на серверы альтернативного приложений, таких как веб-серверы, которые находятся в другой часовой пояс. Это позволяет балансировки нагрузки трафика между экземплярами приложения во время пиковой период, когда серверов-источников перегружен трафика.   
  
### <a name="bkmk_example1"></a>Пример интеллектуальных ответов DNS на основе времени дня  
Ниже приведен пример того, как можно использовать политику DNS для Балансировка трафика приложения на основе времени дня.  
  
В этом примере используется один вымышленной компании Contoso оплаты службы, которая предоставляет online подарить свой решения по всему миру через веб-сайтах, contosogiftservices.com.   
  
contosogiftservices.com веб-сайт размещается в двумя центрами обработки данных, в Сиэтле (Северная Америка), а другой в Дублине (Европа). DNS-серверы, настраиваются для отправки ответов знать, с помощью политики DNS географического расположения. С последней всплеск бизнес contosogiftservices.com имеет более высокого количества посетителей каждый день, и некоторые клиенты сообщили проблемы доступности службы.  
  
Службы оплаты Contoso выполняет анализ сайта и обнаруживает, что каждый вечер между 6 PM и 9 PM местного времени, скачков трафика на веб-серверах. Веб-серверы не масштабирование для обработки увеличить пропускную способность в эти часы максимальной нагрузки приведет к отказу в обслуживании клиентам. Же перегрузку трафика час (пик) происходит в европейских и American центрах данных. В других случаях день серверы обрабатывать трафик томов, которые также ниже их максимальные возможности.  
  
Чтобы убедиться, что клиенты contosogiftservices.com получить быстрое взаимодействие с веб-сайта, службы оплаты Contoso хочет перенаправлять некоторые Dublin трафик на серверы приложений Сиэтл между 6 PM и 9 PM в Дублине; и они должны перенаправляться Сиэтл трафик на серверы приложений Dublin между 6 PM и 9 PM в Сиэтле.  
  
Этот сценарий показана на следующем рисунке.  
  
![Время пример день политики DNS](../../media/DNS-Policy-Tod1/dns_policy_tod1.jpg)  
  
### <a name="bkmk_works1"></a>Как интеллектуальных ответов DNS на основе времени дня работает  
  
Если DNS-сервер настроен с времени дня политики DNS, между 6 PM и 9 PM в каждом географическом расположении, DNS-сервер выполняет следующие функции.  
  
- Ответы первые четыре запросы, получаемые с IP-адресом веб-сервера в локальном центре обработки данных.  
- Ответы пятая запрос, который он получает IP-адрес веб-сервера в удаленном центре обработки данных.   
  
Это поведение на основе политики разгружает двадцати процентов нагрузки трафика локальный веб-сервер для удаленного веб-сервера, нагрузку на сервер локальное приложение для реалистичной анимации и повышая производительность сайта для клиентов.  
  
Во время наименьшей нагрузки DNS-серверы, осуществлять управление обычный географического расположения на основе трафика. Кроме того, DNS-клиенты, которые отправляют запросы из расположения, отличный от Северной Америке и Европе, нагрузки на сервер DNS распределяет трафик между Сиэтла и Dublin центров обработки данных.  
  
Несколько политик DNS настраиваются в DNS, они — это упорядоченный набор правил, и они обрабатываются DNS с наивысшим приоритетом для самый низкий приоритет. DNS использует первой политики, соответствующий обстоятельств, включая время дня. По этой причине более специфические политики должны иметь более высокий приоритет. Если для создания политик день и предоставить высокий приоритет в списке политик DNS обрабатывает и сначала использует эти политики, если они совпадают, параметров DNS-запрос клиента и критериев, указанных в политике. Если они не совпадают, DNS перемещение вниз в списке политик для обработки политики по умолчанию, пока не будет совпадения.  
  
Дополнительные сведения о типах политики и условия см. в разделе [Обзор политик DNS](../../dns/deploy/DNS-Policies-Overview.md).  
  
### <a name="bkmk_how1"></a>Настройка политики DNS для интеллектуальных ответов DNS на основе времени дня  
Чтобы настроить политики время дня балансировки нагрузки приложений на основе ответы на запросы DNS, необходимо выполнить следующие действия.  
  
- [Создание подсети клиента DNS](#bkmk_subnets)  
- [Создание областей зоны](#bkmk_zscopes)  
- [Добавить записи в области зоны](#bkmk_records)  
- [Создание политик DNS](#bkmk_policies)  
  
>[!NOTE]
>На DNS-сервере, который является заслуживающим доверия для зоны, которую вы хотите настроить, необходимо выполнить следующие действия. Членство в группе **DnsAdmins**, или наличие эквивалентных прав, необходимых для выполнения следующих процедур.  
  
В следующих разделах приводятся подробных инструкций по настройке.  
  
>[!IMPORTANT]
>В следующих разделах приведены примеры Windows PowerShell команд, содержащих примеры значений для многих параметров. Убедитесь, замените примеры значений в этих командах со значениями, подходящими для вашего развертывания, прежде чем выполнять эти команды.  
  
#### <a name="bkmk_subnets"></a>Создание подсети клиента DNS  
Первым шагом является для определения подсетей, или пространство IP-адресов из регионов, для которых требуется для перенаправления трафика. Например для перенаправления трафика для США и Европе, необходимо определить подсети или пространства IP-адресов из этих регионов.  
  
Эти сведения можно получить из карты географического-IP. На основании этих IP-географического распределения, необходимо создать «Подсети клиента DNS». Подсеть клиента DNS является логической группой подсети IPv4 или IPv6, из которых запросы отправляются на DNS-сервер.  
  
Создание подсети клиента DNS можно использовать следующие команды Windows PowerShell.  
  
```  
Add-DnsServerClientSubnet -Name "AmericaSubnet" -IPv4Subnet "192.0.0.0/24, 182.0.0.0/24"  
  
Add-DnsServerClientSubnet -Name "EuropeSubnet" -IPv4Subnet "141.1.0.0/24, 151.1.0.0/24"  
  
```  
Дополнительные сведения см. в разделе [добавить DnsServerClientSubnet](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverclientsubnet?view=win10-ps).  
  
#### <a name="bkmk_zscopes"></a>Создание областей зоны  
После настройки подсети клиента необходимо разделить зоны, трафик которого будет перенаправляться в две области другой зоне одну область для каждой из подсетей клиента DNS, который вы настроили.  
  
Например если требуется перенаправить трафик для DNS-имени www.contosogiftservices.com, необходимо создать две области другой зоне в зоне contosogiftservices.com: для США и Европы.  
  
Область зоны представляет уникальный экземпляр зоны. Зона DNS может иметь несколько областей зоны, с каждой областью зону, содержащую собственный набор DNS-записей. Ту же запись может быть представлен в нескольких областях, различные IP-адреса или одинаковые IP-адреса.  
  
>[!NOTE]
>По умолчанию область зоны существует для зон DNS. Эта область зоны имеет то же имя, что зона и устаревших операции DNS-сервера работают в этой области.  
  
Следующие команды Windows PowerShell можно использовать для создания областей зоны.  
  
```  
Add-DnsServerZoneScope -ZoneName "contosogiftservices.com" -Name "SeattleZoneScope"  
  
Add-DnsServerZoneScope -ZoneName "contosogiftservices.com" -Name "DublinZoneScope"  
  
```  
Дополнительные сведения см. в разделе [добавить DnsServerZoneScope](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverzonescope?view=win10-ps).  
  
#### <a name="bkmk_records"></a>Добавить записи в области зоны  
Теперь необходимо добавить записи, представляющий веб-сервера в области две зоны.  
  
Например, в **SeattleZoneScope**, запись **www.contosogiftservices.com** добавляется с IP-адресом 192.0.0.1, который находится в Сиэтле центре обработки данных. Аналогичным образом, в **DublinZoneScope**, запись **www.contosogiftservices.com** добавляется с IP-адресом 141.1.0.3 в центре обработки данных Dublin  
  
Можно использовать следующие команды Windows PowerShell для добавления записей в зоне области.  
  
```  
Add-DnsServerResourceRecord -ZoneName "contosogiftservices.com" -A -Name "www" -IPv4Address "192.0.0.1" -ZoneScope "SeattleZoneScope  
  
Add-DnsServerResourceRecord -ZoneName "contosogiftservices.com" -A -Name "www" -IPv4Address "141.1.0.3" -ZoneScope "DublinZoneScope"  
  
```  
Параметр зонаобласть не включена, при добавлении записи в области по умолчанию. Это то же самое, что при добавлении записей стандартной зоны DNS.  
  
Дополнительные сведения см. в разделе [добавить DnsServerResourceRecord](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverresourcerecord?view=win10-ps).  
  
#### <a name="bkmk_policies"></a>Создание политик DNS  
После создания подсетей разделов (области зоны) и вы добавили записей, необходимо создать политики, которые связывают подсети и разделы, чтобы при запросе поступает из источника в одной подсети клиента DNS, ответ на запрос возвращается из области действия зоны. Политики не требуются для сопоставления зоны области по умолчанию.  
  
После настройки этих политик DNS работе DNS-сервера выглядит следующим образом:  
  
1. Европейской DNS-клиенты получают IP-адрес веб-сервера в центре обработки данных Dublin в их ответ на запрос DNS.  
2. Американский DNS-клиенты получают IP-адрес веб-сервера в центре обработки данных Сиэтл в их ответ на запрос DNS.  
3. Между 6 PM и 9 PM в Дублине 20% запросов от клиентов европейской получать IP-адрес веб-сервера в центре обработки данных Сиэтл в их ответ на запрос DNS.  
4. Между 6 PM и 9 PM в Сиэтле 20% запросов от клиентов American получать IP-адрес веб-сервера в центре обработки данных Dublin в их ответ на запрос DNS.  
5. Часть запросы от остального мира получать IP-адрес в центре обработки данных в Сиэтле и другая половина получать IP-адрес Dublin центра обработки данных.  
  
  
Следующие команды Windows PowerShell можно использовать для создания политики DNS со ссылкой подсети клиента DNS-сервера и области зоны.  
  
>[!NOTE]
>В этом примере DNS-сервер находится в зоне времени по Гринвичу, поэтому час пиковые периоды времени должна быть выражена в эквивалентное время по Гринвичу.  
  
```  
Add-DnsServerQueryResolutionPolicy -Name "America6To9Policy" -Action ALLOW -ClientSubnet "eq,AmericaSubnet" -ZoneScope "SeattleZoneScope,4;DublinZoneScope,1" -TimeOfDay "EQ,01:00-04:00" -ZoneName "contosogiftservices.com" -ProcessingOrder 1  
  
Add-DnsServerQueryResolutionPolicy -Name "Europe6To9Policy" -Action ALLOW -ClientSubnet "eq,EuropeSubnet" -ZoneScope "SeattleZoneScope,1;DublinZoneScope,4" -TimeOfDay "EQ,17:00-20:00" -ZoneName "contosogiftservices.com" -ProcessingOrder 2  
  
Add-DnsServerQueryResolutionPolicy -Name "AmericaPolicy" -Action ALLOW -ClientSubnet "eq,AmericaSubnet" -ZoneScope "SeattleZoneScope,1" -ZoneName "contosogiftservices.com" -ProcessingOrder 3  
  
Add-DnsServerQueryResolutionPolicy -Name "EuropePolicy" -Action ALLOW -ClientSubnet "eq,EuropeSubnet" -ZoneScope "DublinZoneScope,1" -ZoneName "contosogiftservices.com" -ProcessingOrder 4  
  
Add-DnsServerQueryResolutionPolicy -Name "RestOfWorldPolicy" -Action ALLOW --ZoneScope "DublinZoneScope,1;SeattleZoneScope,1" -ZoneName "contosogiftservices.com" -ProcessingOrder 5  
  
```  
Дополнительные сведения см. в разделе [добавить DnsServerQueryResolutionPolicy](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverqueryresolutionpolicy?view=win10-ps).  
  
Теперь DNS-сервер настроен с необходимые политики DNS для перенаправления трафика в зависимости от географического расположения и время суток.  
  
Когда DNS-сервер получает запросы разрешения имен, DNS-сервер оценивает поля на DNS-запрос от настроенных политик DNS. Если исходный IP-адрес в запросе на разрешение имени соответствует какой-либо политики, область связанные зоны используется реагировать на запрос, и пользователь направляется на ресурс, который географически ближайшего к ним.  
  
Можно создать тысячи политик DNS в соответствии с трафик требования к управлению, и все новые политики применяются динамически — без перезагрузки DNS-сервер — на входящие запросы.

