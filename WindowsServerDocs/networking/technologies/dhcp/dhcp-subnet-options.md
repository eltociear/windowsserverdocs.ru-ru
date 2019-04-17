---
title: Выбор параметров DHCP подсети
description: Этот раздел содержит сведения о параметрах выделение подсети DHCP для DHCP Dynamic Host Configuration Protocol () в Windows Server 2016.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dhcp
ms.topic: get-started-article
ms.assetid: ca19e7d1-e445-48fc-8cf5-e4c45f561607
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 43bc3d165f895767ded921b41118ecaccf9734e8
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/28/2018
---
# <a name="dhcp-subnet-selection-options"></a>Выбор параметров DHCP подсети

>Область применения: Windows Server (канал точками годовой), Windows Server 2016

В этом разделе можно использовать для получения сведений о новых вариантах выбора подсети DHCP.

Протокол DHCP теперь поддерживает параметры 118 и 82 \(sub-option 5\). Эти параметры можно использовать для прокси-сервера DHCP-клиентов и агенты ретрансляции для запроса IP-адрес для конкретной подсети, а также из определенного диапазона IP-адресов и область.

Если вы используете DHCP-клиента прокси-сервера, который настроен с параметром DHCP 118, например сервер виртуальной частной сети (VPN), на котором работает Windows Server 2016 и роль сервера удаленного доступа, VPN-сервер может запросить аренды IP-адресов для VPN-клиентов из определенного диапазона IP-адресов.

Если используется агент DHCP-ретрансляции, который настроен с параметром DHCP 82 подкатегории вариант 5, агент ретрансляции может запросить аренду IP-адреса для DHCP-клиентов из определенного диапазона IP-адресов.

Ниже приведены ссылки на запрос комментарии разделы для этих параметров.

- **Параметр 118**: [возможность выбора подсети IPv4 3011 RFC для DHCP](http://www.rfc-base.org/rfc-3011.html)
- **Параметр 82 Sub вариант 5**: [RFC 3527 ссылку выбора вложенные параметр параметр информация агента ретрансляции DHCPv4](https://tools.ietf.org/html/rfc3527)


## <a name="dhcp-option-118-client-subnet-and-relay-agent-link-selection"></a>DHCP-параметра 118: Подсеть клиента и ссылку Выбор агента ретрансляции

Выбор параметра подсети DHCP предоставляет механизм для прокси-серверы DHCP указать IP-подсеть, из которой DHCP-сервера следует назначать IP-адреса и параметры.

### <a name="use-case-scenario"></a>Вариант сценария использования

В этом сценарии сервер виртуальной частной сети \(VPN\) выделяет IP-адресов VPN-клиентам. 

В этом случае VPN-сервер подключен как интрасети, где установлен DHCP-сервера и к Интернету, чтобы VPN-клиенты могли подключаться к VPN-серверу из удаленных расположений.

Перед VPN-сервер может предоставлять аренды IP-адресов VPN-клиентам, сервер связывается с сервером DHCP на использование внутренней подсети и оставляет за собой блок IP-адресов. Затем VPN-сервер управляет IP-адресов, который он получен от DHCP-сервера. Если VPN-сервер предоставляет все зарезервированные IP-адреса в аренду клиентам VPN, VPN-сервер получает дополнительные IP-адреса с DHCP-сервера.

При настройке VPN-сервера с DHCP-параметра 118, можно указать диапазон IP-адресов и область, которая будет использоваться для VPN-клиентов. После настройки параметра 118 VPN-сервер запрашивает IP-адресов из определенного диапазона IP-адресов и область с DHCP-сервера.

### <a name="the-dhcp-subnet-selection-option-field"></a>Поле параметра выделение подсети DHCP

Поле DHCP подсети выбора параметра содержит один IPv4, адрес, используемый для обозначения исходный адрес подсети, для запроса аренды DHCP.  DHCP-сервера, которые настроены на реагирование на этот параметр выделяет адреса либо из:

1. Подсети, указанный в параметре выделение подсети.
2. Подсети, в том же сегменте сети, как подсети, которая указана в параметре выделение подсети.

## <a name="option-82-sub-option-5-link-selection-sub-option"></a>Параметр 82 Sub вариант 5: Функция Sub выделение ссылок

Выбор ссылки агента ретрансляции вложенные позволяет агента ретрансляции DHCP указать IP-подсеть, из которой DHCP-сервера следует назначать IP-адреса и параметры.

Как правило агенты ретрансляции DHCP полагаться на поле \(GIADDR\) IP-адрес шлюза, чтобы взаимодействовать с DHCP-серверами. Тем не менее GIADDR ограничено двумя функциями рабочей:

1. Для DHCP-сервера информирования о подсети, на котором находится DHCP-клиента, запрашивающего аренды IP-адресов.
2. Чтобы сообщить IP-адреса, используемый для взаимодействия с помощью агента ретрансляции DHCP-сервера.

В некоторых случаях IP-адрес агента ретрансляции использует для связи с DHCP-сервера может отличаться от диапазона IP-адресов, с которого необходимо выделить IP-адрес клиента DHCP. 

Агенты ретрансляции DHCP не удается создать использование параметр 118, как ограничен их работу и можно только запись для поля GIADDR или \(option 82\) параметр информация агента ретрансляции. 

Возможность выбора Sub ссылку параметр 82 полезно в этой ситуации, позволяя агента ретрансляции в явной форме указать, что подсети, из которого он хочет IP-адрес в виде параметра v4 DHCP 82 sub вариант 5.

### <a name="use-case-scenario"></a>Вариант сценария использования

В этом сценарии сети организации включает в себя как DHCP-сервера, так и к беспроводной точке доступа \(AP\) для гостевых пользователей. IP-адресов клиентов Гости назначаются из DHCP-сервер организации — Однако из-за ограничений политики брандмауэра, DHCP-сервера не удается получить доступ к беспроводной сети на виртуальной машине или беспроводных клиентов с broadcase сообщения.

Чтобы устранить данное ограничение, точки доступа настроены 5 ссылку Sub выбора параметр, чтобы указать подсеть, из которого он хочет IP-адрес, выделенного для клиентов виртуальной машине, во время GIADDR, также указывать IP-адрес внутреннего интерфейса, который приводит к корпоративной сети.