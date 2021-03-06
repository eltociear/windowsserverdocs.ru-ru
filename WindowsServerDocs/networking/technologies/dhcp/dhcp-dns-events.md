---
title: События ведения журнала DHCP для регистрации записей DNS
description: В этом разделе содержатся сведения о событиях ведения журнала DHCP-сервера в Windows Server 2016.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-dhcp
ms.topic: get-started-article
ms.assetid: beb8c188-6fcf-4520-8825-d17f8ee9fb04
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 5d167666e632aa1a8d92de71feafc9014b66e7ce
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/26/2020
ms.locfileid: "80312607"
---
# <a name="dhcp-logging-events-for-dns-registrations"></a>События ведения журнала DHCP для регистрации DNS

>Область применения: Windows Server (Semi-Annual Channel), Windows Server 2016

Журналы событий DHCP-сервера теперь содержат подробные сведения о сбоях регистрации DNS.

>[!NOTE]
>Во многих случаях причиной сбоев регистрации записей DNS серверами DHCP является то, что зона поиска в обратном\-DNS либо настроена неправильно, либо не настроена вообще.

Следующие новые события DHCP помогают легко определить, когда происходит сбой регистрации DNS из-за неправильно настроенной или отсутствующей зоны обратного\-поиска DNS.

|ИДЕНТИФИКАТОР|Событие|Значение|
|-----|--------------------|--------------------------------------------------------|
|20317|DHCPv4. Форвардрекордднсфаилуре|Сбой регистрации пересылки записей для IPv4-адреса %1 и FQDN %2 с ошибкой %3. Скорее всего, это связано с тем, что зона прямого просмотра для этой записи не существует на DNS-сервере.|
|20318|DHCPv4. Форвардрекордднстимеаут|Сбой регистрации пересылки записей для IPv4-адреса %1 и FQDN %2 с ошибкой %3.|
|20319|DHCPv4. Птррекордднсфаилуре|Регистрация записи типа PTR для IPv4-адреса %1 и FQDN %2 завершилась ошибкой %3. Скорее всего, это связано с тем, что зона обратного просмотра для этой записи не существует на DNS-сервере.|
|20320|DHCPv4. Птррекордднстимеаут|Регистрация записи типа PTR для IPv4-адреса %1 и FQDN %2 завершилась ошибкой %3.|
|20321|DHCPv6. Форвардрекордднсфаилуре|Регистрация пересылки записей для IPv6-адреса %1 и FQDN %2 завершилась ошибкой %3. Скорее всего, это связано с тем, что зона прямого просмотра для этой записи не существует на DNS-сервере.|
|20322|DHCPv6. Форвардрекордднстимеаут|Регистрация пересылки записей для IPv6-адреса %1 и FQDN %2 завершилась ошибкой %3.|
|20323|DHCPv6. Птррекордднсфаилуре|Регистрация записи типа PTR для IPv6-адреса %1 и FQDN %2 завершилась ошибкой %3. Скорее всего, это связано с тем, что зона обратного просмотра для этой записи не существует на DNS-сервере.|
|20324|DHCPv6. Птррекордднстимеаут|Регистрация записи типа PTR для IPv6-адреса %1 и FQDN %2 завершилась ошибкой %3.|
|20325|DHCPv4. Форвардрекордднсеррор|Регистрация записи PTR для IPv4-адреса %1 и FQDN %2 завершилась ошибкой %3 \(%4\).|
|20326|DHCPv6. Форвардрекордднсеррор|Регистрация пересылки записей для IPv6-адреса %1 и FQDN %2 завершилась ошибкой %3 \(%4\)|
|20327|DHCPv6. Птррекордднсеррор|Регистрация записи PTR для IPv6-адреса %1 и FQDN %2 завершилась ошибкой %3 \(%4\).|

