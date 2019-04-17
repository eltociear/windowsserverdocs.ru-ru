---
title: Шаблоны NPS
description: В этом разделе представлен обзор шаблонов сервера политики сети в Windows Server 2016.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: fdfc0df1-21c7-492c-9fad-38fe9c7d935a
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 2835959b8c076ef7b6aeb1fca31a62717ef95037
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/28/2018
---
# <a name="nps-templates"></a>Шаблоны NPS

>Область применения: Windows Server (канал точками годовой), Windows Server 2016

Шаблоны \(NPS\) сервера политики сети позволяет создавать элементы конфигурации, такие как клиенты \(RADIUS\) удаленной службы проверки подлинности удаленного пользователя или общие секретные данные, которые вы можете повторно использовать на локальный сервер политики сети и экспорта для использования на других серверах политики сети.

Шаблоны NPS предназначены для сокращения времени и затрат, необходимое для настройки сервера политики сети на один или несколько серверов. Для конфигурации в Управление шаблонами доступны следующие типы шаблонов сервера политики сети.

- Общие секреты
- RADIUS-клиентов
- Удаленных RADIUS-серверов
- IP-фильтры
- Группы серверов обновлений

Настройка шаблона отличается от непосредственно Настройка сервера политики сети. Создание шаблона не влияет на функциональные возможности сервера политики сети. Это только при выборе шаблона в консоли сервера политики сети, что шаблон влияет на функциональные возможности сервера политики сети в нужном месте. 

Например при настройке RADIUS-клиента в консоли сервера политики сети в разделе клиенты и серверы RADIUS изменениям конфигурации сервера NPS и выполняется настройка сервера политики сети для обмена данными с одним из \(NAS's\) серверы доступа к сети. \ (Следующим шагом будет Настройка NAS для взаимодействия с NPS. \) тем не менее, если настроить новый шаблон RADIUS-клиентов в консоли сервера политики сети в разделе **Управление шаблонами** вместо создания нового RADIUS-клиента в разделе **клиенты и серверы RADIUS**, созданный шаблон, но не будут изменены функциональные возможности сервера политики сети еще. Для изменения функциональности сервера политики сети, в правильное расположение в консоли сервера политики сети необходимо выбрать шаблон.

## <a name="creating-templates"></a>Создание шаблонов

Создание шаблона, откройте консоль NPS щелкните правой кнопкой мыши тип шаблона, например **IP-фильтров**, а затем нажмите кнопку **New**. Новое диалоговое окно свойств шаблона откроется, вы можете настроить шаблон.

## <a name="using-templates-locally"></a>С помощью шаблонов локально

Можно использовать шаблон, который вы создали в **Управление шаблонами**, перейдите в расположение в консоли сервера политики сети, где может применяться шаблон. Например, если вы создаете новый шаблон общие секреты, необходимо применить к конфигурации RADIUS-клиента, в **клиенты и серверы RADIUS** и **RADIUS-клиенты**, откройте свойства RADIUS-клиента. В **выбрать существующий шаблон общие секреты**, выберите шаблон, созданную ранее, в списке доступных шаблонов.

Дополнительные сведения о сервере политики сети см. в разделе [сервера политики сети (NPS)](nps-top.md).