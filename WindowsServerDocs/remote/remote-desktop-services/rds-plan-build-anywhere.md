---
title: Службы удаленных рабочих столов. Сборка в любом расположении
description: Информация о планировании, которая поможет вам определить, где разместить ваше развертывание служб удаленных рабочих столов.
ms.prod: windows-server
ms.technology: remote-desktop-services
ms.topic: article
ms.assetid: c803a383-0eea-4e11-bca5-d204ab758048
author: lizap
ms.author: elizapo
ms.date: 09/07/2016
manager: dongill
ms.openlocfilehash: 9b56614e347b36fb86e6e4680f1b179accaef058
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2020
ms.locfileid: "80857377"
---
# <a name="remote-desktop-services---build-anywhere"></a>Службы удаленных рабочих столов. Сборка в любом расположении

>Применяется к: Windows Server (Semi-Annual Channel), Windows Server 2019, Windows Server 2016

Разверните локально, в облаке или смешано. Измените развертывание, при изменении потребностей вашего бизнеса.

Независимо от местонахождения, базовая [архитектура](desktop-hosting-logical-architecture.md) служб удаленных рабочих столов в среде остается неизменной.
- Для использования служб "Веб-доступ к удаленным рабочим столам" и "Шлюз удаленных рабочих столов" для внешних пользователей у вас по-прежнему должен быть сервер, подключенный к Интернету.
- Для размещения свойств пользователя и удаленного рабочего стола.вы по-прежнему должны иметь домен Active Directory и базу данных SQL для высокодоступных сред.
- Чтобы иметь возможность подключать конечных пользователей к своим рабочим столам или приложениям, у вас по-прежнему должен быть коммуникационный доступ между ролями инфраструктуры RD (Посредник подключений к удаленному столу, шлюз удаленных рабочих столов, лицензирование удаленных рабочих столов, и веб-доступ к удаленным рабочим столам).

Эта гибкость позволяет вам получить лучшее из обоих миров:
- простоту и методы оплаты по мере использования, связанные с облаком и Интернетом;
- и знакомый и простой способ использовать тяжелые ресурсы, которые уже существуют локально.

Дополнительные сведения см. в статье [Построение и развертывание сред служб удаленных рабочих столов](rds-build-and-deploy.md).