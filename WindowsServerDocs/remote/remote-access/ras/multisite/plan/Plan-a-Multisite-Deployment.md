---
title: Планирование многосайтового развертывания
description: Этот раздел является частью руководства развертывание несколькими серверами удаленного доступа в многосайтового развертывания в Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8387eabe-7363-4367-b5b1-03c67baa2933
ms.author: pashort
author: shortpatti
ms.openlocfilehash: ba813fc5da53e9635e9ef1363f1a559a29419312
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/20/2019
ms.locfileid: "67282604"
---
# <a name="plan-a-multisite-deployment"></a>Планирование многосайтового развертывания

>Область применения. Windows Server (полугодовой канал), Windows Server 2016

 Windows Server 2016, Windows Server 2012 объединить в единую роль удаленного доступа DirectAccess и маршрутизации и удаленного доступа (RRAS) VPN. Данный обзор представляет введение в этапы планирования, необходимые для развертывания Windows Server 2016 или Windows Server 2012 удаленного доступа в конфигурации с несколькими узлами.  
  
1.  [Развертывание одиночного сервера DirectAccess с расширенными параметрами](https://technet.microsoft.com/library/hh831436(v=ws.11).aspx). Этот этап включает планирование инфраструктуры, необходимой для развертывания одного сервера. Он включает в себя Планирование сети и параметры сервера, требования к сертификатам, параметры DNS, развертывание сервера сетевых расположений, серверы управления DirectAccess, параметры Active Directory и объектов групповой политики (GPO).  
  
2.  [Шаг 2 Планирование многосайтового инфраструктуры](Step-2-Plan-the-Multisite-Infrastructure.md). Этот этап включает Active Directory и планирование объектов групповой Политики и конфигурации DNS.  
  
3.  [Шаг 3 Планирование многосайтового развертывания](Step-3-Plan-the-Multisite-Deployment.md). Этот этап включает планирование параметров сертификата, сетевого расположения сервера конфигурации, параметры точки входа клиента, параметры префикс IPv6 и при необходимости глобальных параметров балансировки нагрузки.  
  
> [!NOTE]  
> Запишите принятые при планировании решения для расширенного развертывания удаленного доступа. Эти данные можно использовать как задание для всех лиц, участвующих в развертывании.  
  
После завершения описанных этапов планирования, см. в разделе [настройке многосайтового развертывания](../configure/Configure-a-Multisite-Deployment.md).  
  

