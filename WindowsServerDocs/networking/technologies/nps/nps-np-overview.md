---
title: Политики сети
description: В этом разделе представлен обзор политик сети для сервера политики сети в Windows Server 2016 и содержит ссылки на дополнительные руководства по NPS.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: e4a9b134-6d1d-40d7-a49c-5f46d5fdb419
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 60ab80bb6cf26578430b76806405a65a0f596ef2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2019
ms.locfileid: "59848955"
---
# <a name="network-policies"></a>Политики сети

>Относится к: Windows Server (полугодовой канал), Windows Server 2016

Обзор политик сети на сервере политики сети можно использовать в этом разделе.

>[!NOTE]
>Дополнение к данному разделу доступна следующая документация по политики сети.
> - [Разрешение на доступ](nps-np-access.md)
> - [Настройка политик сети](nps-np-configure.md)

Сетевые политики — это набор условий, ограничений и параметров, которые можно указать, кто имеет права для подключения к сети и обстоятельства, при которых они могут или не удается подключиться.

При обработке запросов на подключение, как сервер службы проверки подлинности удаленного пользователя (RADIUS), сервер политики сети выполняет проверку подлинности и авторизации для запроса на подключение. В процессе проверки подлинности NPS проверяет подлинность пользователя или компьютера, подключающегося к сети. В процессе авторизации NPS определяет, разрешено ли пользователю или компьютеру доступ к сети.

Чтобы сделать эти решения, сервер политики сети использует сетевые политики, которые настраиваются в консоли сервера политики сети. NPS также проверяет свойства удаленного доступа в учетной записи пользователя в Active Directory&reg; доменных служб \(AD DS\) для выполнения авторизации.

## <a name="network-policies---an-ordered-set-of-rules"></a>Сетевые политики — упорядоченный набор правил

Политики сети можно рассматривать как правила. Каждое правило имеет набор условий и параметров. Сервер политики сети сравнивает условия правила в свойства запросов на подключение. При наличии совпадения правила и запрос на подключение, параметрам, заданным в правиле применяются к соединению.

Если несколько политик сети настроены на сервере политики сети, они упорядоченный набор правил. NPS проверяет каждый запрос на подключение с первым правилом в списке, а затем второго и т. д., пока не будет найдено совпадение.

Каждая политика сети имеет **состояние политики** параметр, который позволяет включить или отключить политику. При отключении политики сети, сервер политики сети не оценивает политику при авторизации запросов на подключение.

>[!NOTE]
>Если требуется, чтобы сервер политики сети для определения политики сети, при выполнении авторизации запросов на подключение, необходимо настроить **состояние политики** "флажок" включить параметр, выбрав политику.

## <a name="network-policy-properties"></a>Свойства политики сети

Существует четыре категории свойств для каждой политики сети.

### <a name="overview"></a>Обзор

 Эти свойства позволяют пользователю указать ли политика включена, ли политика предоставляет или запрещает доступ и является ли метод определенного сетевого соединения или тип сервера доступа к сети (NAS), необходимые для запросов на подключение. Общие сведения о свойствах также позволяют пользователю указать, игнорируются ли свойств удаленного доступа учетных записей пользователей в AD DS. Если этот флажок установлен, только в параметрах политики сети используются сервером политики сети для определения, разрешен ли соединение.


### <a name="conditions"></a>Условия

 Эти свойства позволяют указать условия, которые должны иметь запрос на подключение для соответствия политике сети; Если запрос на подключение соответствуют условиям, настроенные в политике, NPS применяет параметры, назначенные в политике сети для подключения. Например если указать NAS IPv4-адрес в качестве условия политики сети и сервера политики сети получает запрос на подключение из NAS, который имеет указанный IP-адрес, условие в политике соответствует запрос на подключение. 


### <a name="constraints"></a>Ограничения

 Ограничения — Дополнительные параметры сетевой политики, которые необходимы для проверки этого запроса подключения. Если запрос на подключение не соответствует ограничению, сервер политики сети автоматически отклоняет запрос. В отличие от NPS несоответствия запроса условиям в политике сети если не соответствует ограничению, сервер политики сети отклоняет запрос на подключение без оценки дополнительных сетевых политик.

### <a name="settings"></a>Параметры

 Эти свойства позволяют указать параметры, сервер политики сети применяется к запрос на подключение, если все условия политики сети для политики совпадают.

При добавлении новой сетевой политики с помощью консоли сервера политики сети, необходимо использовать мастер создания политики сети. После создания политики сети с помощью мастера, можно настроить политику, дважды щелкнув политику в консоли сервера политики сети, чтобы получить свойства политики.

Примеры синтаксиса, поиска совпадения с шаблоном, чтобы указать сетевой атрибуты политики, см. в разделе [использовать регулярные выражения в NPS](nps-crp-reg-expressions.md).

Дополнительные сведения о сервере политики сети, см. в разделе [сервера политики сети (NPS)](nps-top.md).