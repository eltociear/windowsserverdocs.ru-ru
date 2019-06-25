---
title: Параметры выбора подсети DHCP
description: В этом разделе сведения о вариантах выбора подсети DHCP для конфигурации протокола DHCP (Dynamic Host) в Windows Server 2016.
manager: dougkim
ms.prod: windows-server-threshold
ms.technology: networking-dhcp
ms.topic: get-started-article
ms.assetid: ca19e7d1-e445-48fc-8cf5-e4c45f561607
ms.author: pashort
author: shortpatti
ms.date: 08/17/2018
ms.openlocfilehash: 034ca48ef13a6bdac63ca99ac753fc9826460922
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2019
ms.locfileid: "59870815"
---
# <a name="dhcp-subnet-selection-options"></a>Параметры выбора подсети DHCP

>Относится к: Windows Server (полугодовой канал), Windows Server 2016

Сведения о новых параметров выбора подсети DHCP можно использовать в этом разделе.

DHCP, теперь поддерживает параметр 82 \(подзапроса параметр 5\). Эти параметры можно использовать прокси-сервер DHCP-клиентов и агентов ретрансляции для запроса IP-адрес для конкретной подсети, а также из определенного диапазона IP-адресов и область.  Дополнительные сведения см. в разделе **параметр 82 Sub параметр 5**: [Выбор ссылки 3527 RFC подпараметров для параметра информация агента ретрансляции для DHCPv4](https://tools.ietf.org/html/rfc3527).

Если вы используете агент ретрансляции DHCP, настроенной с DHCP-параметра 82, подзапроса вариант 5, агент ретрансляции может запросить аренду IP-адреса для DHCP-клиентов из определенного диапазона IP-адресов.


## <a name="option-82-sub-option-5-link-selection-sub-option"></a>Параметр 82 подпараметры 5: LINK-параметр выбора Sub

Выбор ссылки агента ретрансляции подпараметров позволяет агента DHCP-ретрансляции для указания IP-подсеть, с помощью которой DHCP-сервер должен назначить IP-адреса и параметры.

Как правило, агенты ретрансляции DHCP зависит от IP-адрес шлюза \(GIADDR\) поля для связи с DHCP-серверами. Тем не менее GIADDR ограничивается его двумя операционными функциями:

1. Определите для подсети, на которой находится DHCP-клиент, запрашивающий аренды IP-адресов DHCP-сервера.
2. Чтобы сообщить о DHCP-сервера IP-адреса для использования при взаимодействии с агентом ретрансляции.

В некоторых случаях IP-адрес, агент ретрансляции для взаимодействия с DHCP-сервера может отличаться от диапазона IP-адресов, из которого нужно разместить IP-адрес клиента DHCP. 

Параметр ссылки выбора Sub параметра 82 удобен в этой ситуации, позволяя агент ретрансляции, чтобы явным образом определить подсети, из которого собирается IP-адрес, выделенной в виде параметра DHCP v4 82 подпараметры 5.

> [!NOTE]
>
> Все ретрансляции агента IP-адреса (GIADDR) должны быть частью активных DHCP область диапазон IP-адресов. Любой GIADDR за пределами диапазонов адресов области DHCP считается ретранслятора незаконных и DHCP-сервера Windows не признает ее запросы клиентов DHCP из этих агентов ретрансляции.
>
> Специальные области могут создаваться для агентов ретрансляции «авторизовать». Создание области с GIADDR (или несколько последовательных IP-адресов в случае GIADDR), исключите адреса GIADDR распространения и затем активировать область. Это приведет к авторизации агенты ретрансляции распоряжаться адреса GIADDR назначение.


### <a name="use-case-scenario"></a>Сценарии использования

В этом случае в сети организации включает в себя как DHCP-сервера, так и к беспроводной точке доступа \(AP\) для гостевых пользователей. Гости клиентские IP-адреса назначаются от DHCP-сервера организации — Однако из-за ограничений политики брандмауэра, DHCP-сервер не может получить доступ к гостевой беспроводной сети или беспроводные клиенты с сообщениями broadcase.

Чтобы устранить это ограничение, ТД настроено 5 ссылку Sub выбора параметр, чтобы указать подсети, из которого собирается выделен для гостевой клиентов, в процессе GIADDR, указания IP-адрес внутреннего интерфейса, которое приводит к IP-адрес Корпоративная сеть.