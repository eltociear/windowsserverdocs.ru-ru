---
title: Переключение между режимами
description: Сведения о переключении между режимами станции и консоли в службах MultiPoint
ms.custom: na
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5f1b2324-c1b0-4b61-ab51-39af15e7792a
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 08/04/2016
ms.openlocfilehash: a9c00d65ad1c59e91f4011ab932bf9f921957c59
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/31/2019
ms.locfileid: "66446155"
---
# <a name="switch-between-modes"></a>Переключение между режимами
MultiPoint Manager включает следующие режимы, которые помогут вам выполнять различные виды управления системой служб MultiPoint.  
  
-   *Режим станции*: По умолчанию система служб MultiPoint запускается в режиме станции. В этом режиме станции служб MultiPoint функционируют как отдельные компьютеры под управлением Windows, и несколько пользователей могут использовать систему одновременно. Вы и ваши пользователи можете предоставлять общий доступ к файлам и выполнять свою работу.  
  
-   *Режим консоли*: Когда в системе MultiPoint Services находится в режиме консоли, можно установить и обновить программное обеспечение и драйверы или выполнить другие задачи обслуживания. Если система находится в режиме консоли, *станции* недоступны другим пользователям компьютера. Такие станции не отображаются в MultiPoint Manager. Все мониторы, напрямую подключенные к серверу, учитываются как компьютерной системы.   
  
> [!NOTE]
> Вы можете принудительно запускать систему в режиме консоли, изменив значения по умолчанию в настройках сервера.  
> ## <a name="to-switch-from-station-mode-to-console-mode"></a>Переключение из режима станции в режим консоли  
  
1.  Откройте диспетчер MultiPoint в режиме станции и нажмите кнопку **Главная** вкладки.  
  
2.  В столбце **Компьютер** выберите компьютер, для которого вы хотите изменить режим.  
  
3.  В разделе *имя_компьютера* **задачи**, нажмите кнопку **переключиться в режим консоли**. Компьютер будет перезагружен, и все станции станут недоступны.  
  
## <a name="to-switch-from-console-mode-to-station-mode"></a>Переключение из режима консоли в режим станции  
  
1.  Откройте диспетчер MultiPoint в режиме консоли, а затем нажмите кнопку **Главная** вкладки.  
  
2.  В столбце **Компьютер** выберите компьютер, для которого вы хотите изменить режим.  
  
3.  В разделе *имя_компьютера* **задачи**, нажмите кнопку **переключиться в режим станции**. Компьютер будет перезагружен, и все станции станут доступны.  
  
## <a name="see-also"></a>См. также  
[Управление системными задачами с помощью диспетчера MultiPoint](Manage-System-Tasks-Using-MultiPoint-Manager.md)