---
title: Установка компонента BranchCache
description: Этот раздел является частью BranchCache развертывания руководство для Windows Server 2016, который показывает, как развернуть BranchCache в режимах распределенный и размещенный кэш, чтобы оптимизировать использование пропускной способности глобальной сети в филиалах
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 4f31dc61-2dbe-4c7e-b3f9-85ae49a45049
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 8b4aecd9e9355a6c2d5ac485ac77c76428fe295f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2019
ms.locfileid: "59872195"
---
# <a name="install-the-branchcache-feature"></a>Установка компонента BranchCache

>Относится к: Windows Server (полугодовой канал), Windows Server 2016

Эту процедуру можно использовать для установки компонента BranchCache и запустите службу BranchCache на компьютере под управлением Windows Server&reg; 2016, Windows Server 2012 R2 или Windows Server 2012.  
  
Членство в группе **Администраторы** либо эквивалентной, является минимальным требованием для выполнения этой процедуры.  
  
Перед выполнением этой процедуры рекомендуется установить и настроить приложение на основе BITS или веб-сервера.  
  
> [!NOTE]  
> Для выполнения этой процедуры с помощью Windows PowerShell, запустите Windows PowerShell от имени администратора, введите следующие команды в командной строке Windows PowerShell и нажмите клавишу ВВОД.  
>   
> `Install-WindowsFeature BranchCache`  
>   
> `Restart-Computer`  
  
### <a name="to-install-and-enable-the-branchcache-feature"></a>Чтобы установить и включить функцию BranchCache  
  
1.  Откройте диспетчер серверов, щелкните **Управление**, а затем нажмите кнопку **Добавить роли и компоненты**. Откроется мастер добавления ролей и компонентов. Нажмите кнопку **Далее**.  
  
2.  В **Выбор типа установки**, убедитесь, что **Установка ролей или компонентов** выбран, а затем нажмите кнопку **Далее**.  
  
3.  В **Выбор целевого сервера**, убедитесь, что выбран правильный сервер и нажмите кнопку **Далее**.  
  
4.  На странице **Выбор ролей сервера**нажмите кнопку **Далее**.  
  
5.  В **Выбор компонентов**, нажмите кнопку **BranchCache**, а затем нажмите кнопку **Далее**.  
  
6.  На странице **Подтверждение выбранных элементов для установки** нажмите кнопку **Установить**. В **ход выполнения установки**, выполняется установка компонента BranchCache. По завершении установки нажмите кнопку **закрыть**.  
  
После установки компонента BranchCache, службе BranchCache, также называемый PeerDistSvc -, и тип запуска имеется автоматически.  
  

