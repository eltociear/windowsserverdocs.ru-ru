---
title: Управление записями ресурсов DNS
description: Этот раздел входит руководство по управлению управления IP-адресами (IPAM) в Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-ipam
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7b66c09d-e401-4f70-9a2a-6047dd629bfa
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 5ed781ef37243b80ea9da8aad27a29046b8dc8c9
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/28/2018
---
# <a name="dns-resource-record-management"></a>Управление записями ресурсов DNS

>Область применения: Windows Server (канал точками годовой), Windows Server 2016

В этом разделе представлены сведения об управлении DNS-записи ресурсов с помощью IPAM.  
  
> [!NOTE]  
> Помимо этого раздела в следующих разделах Управление записями ресурсов DNS, доступные в этом разделе.  
>   
> -   [Добавление записи ресурса DNS](../../technologies/ipam/Add-a-DNS-Resource-Record.md)  
> -   [Удаление записей ресурсов DNS](../../technologies/ipam/Delete-DNS-Resource-Records.md)  
> -   [Фильтрация представления записей ресурсов DNS](../../technologies/ipam/Filter-the-View-of-DNS-Resource-Records.md)  
> -   [Просмотр записей ресурсов DNS для определенного IP-адреса](../../technologies/ipam/View-DNS-Resource-Records-for-a-Specific-IP-Address.md)  
  
## <a name="resource-record-management-overview"></a>Обзор управление записями ресурсов  
При развертывании IPAM в Windows Server 2016, можно выполнить обнаружение серверов для добавления серверов DHCP и DNS в консоли управления сервером IPAM. IPAM-сервер затем динамически собирает данные DNS каждые шесть часов от DNS-серверы, настроенные для управления. IPAM поддерживает локальной базы данных, где хранятся данные DNS. IPAM предоставляет уведомления о день и время, сбор данных с сервера, а также о том, на следующий день и время, когда выполняется сбор данных от DNS-серверов.  
  
Панель желтое состояние на рисунке ниже показано расположение интерфейса пользователя уведомления IPAM.  
  
![Уведомления IPAM](../../media/DNS-Resource-Record-Management/ipam_DataCollection_01.jpg)  
  
Собираемые данные DNS включает зоны и ресурсов данные в записи DNS. Вы можете настроить IPAM производить сбор информации о зоне предпочитаемый DNS-сервера.  IPAM собирает на основе файлов и Active Directory зоны.  
  
> [!NOTE]  
> IPAM собирает данные только с присоединенных к домену DNS-серверах Майкрософт. DNS-серверы сторонних производителей и серверов к домену не входящих в домен с помощью IPAM не поддерживаются.  
  
Ниже приведен список типов записей ресурсов DNS, которые собираются с помощью IPAM.  
  
-   AFS базы данных  
  
-   Адресов ATM  
  
-   ЗАПИСЬ CNAME  
  
-   DHCID  
  
-   DNAME  
  
-   Узла A или AAAA  
  
-   Сведения об узле  
  
-   ISDN  
  
-   MX  
  
-   Серверы имен  
  
-   Указателя (PTR)  
  
-   Ответственное лицо  
  
-   Маршрут  
  
-   Расположение службы  
  
-   SOA  
  
-   SRV  
  
-   Текст  
  
-   Хорошо известная служб  
  
-   WINS  
  
-   WINS-R  
  
-   X.25  
  
В Windows Server 2016 IPAM обеспечивает интеграцию перечень IP-адресов, зоны DNS-сервера и DNS-записи ресурсов:  
  
-   IPAM можно использовать для автоматического создания перечень IP-адресов из записей ресурсов DNS.  
  
-   Можно вручную создать перечень IP-адресов в DNS A и AAAA записей ресурсов.  
  
-   Просмотр записей ресурсов DNS для конкретной зоны DNS и фильтра записи на основании типа IP адрес, данные записи ресурсов и другие параметры фильтрации.  
  
-   IPAM автоматически создается сопоставление диапазоны IP-адресов и DNS-зоны обратного просмотра.  
  
-   IPAM создает IP-адреса для PTR-записей, представленные в зоны обратного просмотра и включенных в этот диапазон IP-адресов. Вы можете изменить это сопоставление также вручную при необходимости.  
  
IPAM позволяет выполнять следующие операции для записей ресурсов с помощью консоли IPAM.  
  
-   Создание записей ресурсов DNS  
  
-   Изменение записей ресурсов DNS  
  
-   Удаление записей ресурсов DNS  
  
-   Создание соответствующих записей ресурсов  
  
IPAM автоматически регистрирует все изменения конфигурации DNS-сервера, можно сделать с помощью консоли IPAM.  
  
## <a name="see-also"></a>См. также:  
[Управление IPAM](Manage-IPAM.md)  
  

