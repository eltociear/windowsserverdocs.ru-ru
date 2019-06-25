---
title: Обновление групповой политики
description: Этот раздел является частью руководства развертывание сервера сертификатов для развертывания беспроводных и проводных сетей 802.1 X
manager: brianlic
ms.topic: article
ms.assetid: 65b36794-bb09-4c1b-a2e7-8fc780893d97
ms.prod: windows-server-threshold
ms.technology: networking
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 83dd48297535aafe30e48fe37010d81b279f4c91
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2019
ms.locfileid: "59863455"
---
# <a name="refresh-group-policy"></a>Обновление групповой политики

>Относится к: Windows Server (полугодовой канал), Windows Server 2016

Эту процедуру можно использовать для обновления групповой политики вручную на локальном компьютере. При обновлении групповой политики, если автоматической регистрации сертификатов настроена и работает правильно, локальный компьютер является автоматически подающие сертификата центром сертификации (ЦС).  
  
> [!NOTE]  
> Групповая политика обновляется автоматически при перезагрузке компьютера-члена домена, или при входе пользователя в домен компьютер. Кроме того Групповая политика обновляется периодически. По умолчанию это периодическое обновление выполняется каждые 90 минут со смещением случайную до 30 минут.  
  
Членство в группе **Администраторы**, или эквивалентной является минимальным требованием для выполнения этой процедуры.  
  
### <a name="to-refresh-group-policy-on-the-local-computer"></a>Обновление групповой политики на локальном компьютере  
  
1.  На компьютере, где установлен сервер политики сети, откройте Windows PowerShell&reg; с помощью значка на панели задач.  
  
2.  В командной строке Windows PowerShell, введите **gpupdate**, и нажмите клавишу ВВОД.  
  

