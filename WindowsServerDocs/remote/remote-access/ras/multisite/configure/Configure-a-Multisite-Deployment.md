---
title: Настройка многосайтового развертывания
description: Этот раздел является частью руководства развертывание несколькими серверами удаленного доступа в многосайтового развертывания в Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cb84920e-7cf5-4266-b071-d09e3d5e1f10
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 28fcb2506e59ff2afb501a2c8bc74da2d6f0cd15
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/20/2019
ms.locfileid: "67280990"
---
# <a name="configure-a-multisite-deployment"></a>Настройка многосайтового развертывания

>Область применения. Windows Server (полугодовой канал), Windows Server 2016

 Windows Server 2016 объединяет DirectAccess и удаленного доступа (RAS) VPN в единую роль удаленного доступа. Данный обзор представляет введение в шаги настройки, необходимые для развертывания одного Windows Server 2016 или удаленного доступа Windows Server 2012 многосайтового развертывания.  
  
-   Шаг 1. [Развертывание одиночного сервера DirectAccess с расширенными параметрами](https://technet.microsoft.com/windows-server-docs/networking/remote-access/directaccess/single-server-advanced/deploy-a-single-directaccess-server-with-advanced-settings). Установите и настройте сервер удаленного доступа. Многосайтовое развертывание необходимо установить один сервер перед настройкой многосайтового развертывания.  
  
-   [Шаг 2. Настройка инфраструктуры многосайтового](Step-2-Configure-the-Multisite-Infrastructure.md). Для многосайтового развертывания необходимо настроить дополнительные сайты Active Directory и контроллеры домена. Дополнительными группами безопасности и объекты групповой политики (GPO) также необходимы, если вы не используете автоматически настраиваемые объекты групповой политики.  
  
-   [Шаг 3. Настройка многосайтового развертывания](Step-3-Configure-the-Multisite-Deployment.md)— Установка роли удаленного доступа на дополнительных серверах удаленного доступа, включение многосайтового развертывания и дополнительные серверы в качестве точки входа для развертывания.  
  
-   [Шаг 4. Проверка многосайтового развертывания](Step-4-Verify-the-Multisite-Deployment.md) 
  

