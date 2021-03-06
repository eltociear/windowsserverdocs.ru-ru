---
title: Сетевая оболочка (Netsh)
description: В этой статье приводится обзор служебной программы командной строки "Сетевая оболочка" (netsh) в Windows Server 2016.
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: aedef092-8445-4e53-b9d4-525ecd98b02d
manager: dougkim
ms.author: lizross
author: eross-msft
ms.date: 09/13/2018
ms.openlocfilehash: d9103585d1868f586f169f01096c4d37961e7033
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2020
ms.locfileid: "80316679"
---
# <a name="network-shell-netsh"></a>Сетевая оболочка \(Netsh\)

>Применяется к: Windows Server (Semi-Annual Channel), Windows Server 2016

Сетевая оболочка (netsh) является служебной программой командной строки, которая позволяет настраивать и отображать состояние различных сетевых ролей коммуникационных серверов и компонентов после их установки на компьютер под управлением Windows Server 2016.

Некоторые клиентские технологии, например \(DHCP-клиент\) и BranchCache, также предоставляют команды netsh для настройки клиентских компьютеров под управлением Windows 10.

В большинстве случаев команды netsh предоставляют те же функциональные возможности, которые доступны в оснастке консоли управления Майкрософт \(MMC\) для каждой роли сетевого сервера или сетевого компонента. Например, вы можете настроить сервер политики сети \(NPS\) через оснастку консоли управления (NPS) или командами netsh в контексте **netsh nps**.

Кроме того, существуют команды netsh для сетевых поддержки технологий, таких как IPv6, сетевой мост и удаленный вызов процедур \(RPC\), которые недоступны в формате оснастки MMC для Windows Server.

>[!IMPORTANT]
>Мы рекомендуем для управления сетевыми технологиями в [Windows Server 2016 и Windows 10](https://technet.microsoft.com/library/mt156917.aspx) использовать Windows PowerShell, а не сетевую оболочку. Но сетевая оболочка включена и поддерживается для обеспечения совместимости с существующими скриптами.

## <a name="network-shell-netsh-technical-reference"></a>Технический справочник по сетевой оболочке (Netsh)

Технический справочник по сетевой оболочке содержит полный список команд netsh с описанием синтаксиса, параметров и примерами использования. Технический справочник по Netsh можно использовать для создания скриптов и пакетных файлов, которые выполняют команды netsh для локального или удаленного управления сетевыми технологиями на компьютерах под управлением Windows Server 2016 и Windows 10.  
  
### <a name="content-availability"></a>Доступность содержимого  
  
Технический справочник по сетевой оболочке доступен для загрузки в формате справки Windows \(*. chm\) из коллекции TechNet: [Технический справочник по Netsh](https://gallery.technet.microsoft.com/Netsh-Technical-Reference-c46523dc).  
  
---
