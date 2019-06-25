---
title: Контрольный список настройки пространства имен DFS
description: В этой статье рассматривается оптимизация того, как пространство имен DFS обрабатывает ссылки и опрашивает AD DS на предмет актуальных данных пространства имен.
ms.date: 6/5/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 5e2d43f75a64a6a7950539c14386c6a037bc3c45
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2019
ms.locfileid: "59872645"
---
# <a name="checklist-tune-a-dfs-namespace"></a>Контрольный список: Настройка пространства имен DFS

> Относится к: Windows Server 2019, Windows Server (полугодовой канал), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

После создания пространства имен и добавления папок и целевых объектов, используйте следующий контрольный список для настройки или оптимизировать способ пространств имен DFS обрабатывает ссылки и опрашивает доменных служб Active Directory (AD DS) для обновленных данных пространства имен.

-   Запретите пользователям просматривать папки в пространстве имен, на доступ к которым у них нет разрешения. [Включить перечисление на основе доступа в пространстве имен](enable-access-based-enumeration-on-a-namespace.md) 
-   Разрешите или запретите пользователям перенаправление на пространство имен или конечный объект папки при обращении к папке в пространстве имен. [Включение и отключение ссылок и восстановление размещения клиента](enable-or-disable-referrals-and-client-failback.md) 
-   Настройте продолжительность кэширования клиентами ссылки перед запросом новой. [Изменить количество времени, которого клиенты кэшируют ссылки](change-the-amount-of-time-that-clients-cache-referrals.md)
-   Оптимизируйте опрос AD DS серверами пространства имен для получения самых свежих данных пространства имен. [Оптимизация опроса пространства имен](optimize-namespace-polling.md)
-   Используйте унаследованные разрешения, чтобы управлять тем, кто из пользователей может просматривать папки в пространстве имен, для которого включено перечисление на основе доступа. [Использование наследуемых разрешений с перечислением на основе доступа](using-inherited-permissions-with-access-based-enumeration.md)

Кроме того с помощью пространств имен DFS, известную как приоритет, можно указать приоритет серверов, чтобы определенный сервер всегда помещается первыми или последними в списке серверов (известный как ссылку), клиент получает, когда она осуществляет доступ к папке с целевыми объектами в пространстве имен.

-   Укажите, в каком порядке пользователи будут перенаправляться на конечные объекты папок. [Выбор метода упорядочения конечных объектов в ссылках](set-the-ordering-method-for-targets-in-referrals.md)
-   Переопределение порядка в ссылках для конкретного сервера пространства имен или конечного объекта папки. [Установка приоритета переопределить сортировку ссылок](set-target-priority-to-override-referral-ordering.md)

## <a name="see-also"></a>См. также

-   [Пространства имен](https://technet.microsoft.com/library/cc771914(v=ws.11).aspx)
-   [Контрольный список: Развертывание пространств имен DFS](checklist-deploy-dfs-namespaces.md)
-   [Настройка пространств имен DFS](tuning-dfs-namespaces.md)

