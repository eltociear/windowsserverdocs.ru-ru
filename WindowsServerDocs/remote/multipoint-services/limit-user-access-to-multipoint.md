---
title: Ограничить доступ пользователей к серверу
description: Узнайте, как предоставить или запретить доступ к службам MultiPoint для пользователей и групп
ms.custom: na
ms.date: 07/22/2016
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4cabd4f1-a764-4be6-bc6e-0a5f5566390c
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: 1466e19152847a6c7d88f77162c50ec73a5a7d27
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2019
ms.locfileid: "59830815"
---
# <a name="limit-users-access-to-the-multipoint-server"></a>Ограничить доступ пользователей к серверу Multipoint
Присоединить MultiPoint server к домену Active Directory или использовать локальные учетные записи пользователей, по умолчанию все пользователи имеют доступ к серверу MultiPoint. Перед тем как разрешить пользователю вход на станциях в вашей среде MultiPoint Services, необходимо ограничить доступ к серверу.  
  
Любой пользователь в группу пользователей удаленного рабочего стола можно вход на сервер MultiPoint. По умолчанию пользователь группу «все» является членом группы пользователей удаленного рабочего стола, и таким образом каждого локального пользователя и домен пользователя можно войти в систему на сервер MultiPoint. Чтобы ограничить доступ к серверу MultiPoint, удалите все группы из группы пользователей удаленного рабочего стола пользователя и затем добавить определенных пользователей или группы в группу Пользователи удаленного рабочего стола.  
  
## <a name="add-or-remove-users-or-groups-to-the-remote-desktop-users-group"></a>Добавить или удалить пользователей или группы в группу Пользователи удаленного рабочего стола  
  
1.  Из **запустить** экране откройте **Управление компьютером**.  
  
2.  В дереве консоли в разделе **локальные пользователи и группы**, нажмите кнопку **группы**.  
  
3.  Дважды щелкните **пользователи удаленного рабочего стола**и следуйте инструкциям, чтобы добавить или удалить пользователей.  
  
    -   Чтобы ограничить общий доступ к серверу, удалите «все».  
  
    -   Чтобы предоставить серверу MultiPoint пользователям доступ к станции, добавьте каждой локальной учетной записи или каждой учетной записи домена пользователя или группы в группу Пользователи удаленного рабочего стола.  