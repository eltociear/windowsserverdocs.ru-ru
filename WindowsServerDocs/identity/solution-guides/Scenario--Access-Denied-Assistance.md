---
ms.assetid: aae907eb-11cf-4a87-a046-8680872ed0b1
title: Сценарий отказом в доступе
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: d6b8d8a094aa86fd5be78d2eae13bae50df3fd79
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2019
ms.locfileid: "59829095"
---
# <a name="scenario-access-denied-assistance"></a>Сценарий: помощь при отказе в доступе

>Область применения. Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Если пользователи пытаются получить доступ к общим файлам и папкам на файловом сервере, для которых у них нет разрешений, они видят сообщение об отказе в доступе. Часто у администраторов нет соответствующего контекста, что усложняет устранение проблемы.  
  
## <a name="scenario-description"></a>Описание сценария  
Отказано в доступе помощника — это новая функция в Windows Server 2012, который предоставляет следующие способы устранения неполадок, возникающих на доступ к файлам и папкам:  
  
-   **Самостоятельное решение.** Если пользователь может определить проблему и устранить ее, получив доступ к запрошенному ресурсу, степень влияния на бизнес мала и специальные исключения в централизованной политике доступа не требуются. Функция помощи при отказе в доступе отображает сообщение, которое администраторы файлового сервера могут настроить в соответствии со своими потребностями. Например, администратор может настроить сообщение так, чтобы пользователи могли запросить доступ у владельца данных без привлечения администратора файлового сервера.  
  
-   **Помощь владельца данных.** Вы можете определить список рассылки для общих папок и настроить его так, чтобы владелец папки получал уведомление по электронной почте, когда пользователю требуется доступ. Если владелец данных не знает, как помочь пользователю получить доступ, он или она могут отправить эти сведения администратору файлового сервера.  
  
-   **Помощь администратора файлового сервера.** Такой тип помощи доступен, если пользователи не могут сами устранить проблему, а владелец данных не может им помочь.  Windows Server 2012 предоставляет пользовательский интерфейс, в котором администраторы файлового сервера могут просматривать действующие разрешения пользователя для файла или папки, чтобы проще устранять проблемы с доступом.  
  
Отказом в доступе в Windows Server 2012 предоставляет администраторам необходимые сведения доступа, чтобы они могли определить проблему и средства, таким образом, чтобы они могли изменения конфигурации для удовлетворения запроса на доступ. Например, пользователь может выполнить следующую процедуру, чтобы получить доступ к файлу, к которому в текущий момент доступ отсутствует:  
  
-   Пользователь пытается прочитать файл в \\\financeshares общей папки, но сервер отображает сообщение об отказе в доступе.  
  
-    Windows Server 2012 отображает сведения отказом в доступе пользователю с возможностью запросить помощь.  
  
-   Если пользователь запрашивает доступ к ресурсу, сервер отправляет сообщение электронной почты с данными запроса доступа владельцу папки.  
  
Сведения о планировании настройки помощи при отказе в доступе см. в разделе [Plan for Access-Denied Assistance](assetId:///b169f0a4-8b97-4da8-ae4a-c8f1986d19e1).  
  
Можно найти сведения о настройке помощи при отказе в доступе в [Denied Assistance &#40;Поэтапная&#41;](Deploy-Access-Denied-Assistance--Demonstration-Steps-.md).  
  
## <a name="in-this-scenario"></a>Содержание сценария  
Этот сценарий является частью сценария динамического контроля доступа. Дополнительные сведения о динамическом контроле доступа см. в следующих разделах:  
  
-   [Динамический контроль доступа. Обзор сценария](Dynamic-Access-Control--Scenario-Overview.md)  
  
## <a name="practical-applications"></a>Практическое применение  
Помощь при отказе доступа в Windows Server 2012 участвует в реализации динамического контроля доступа, позволяя пользователям запрашивать доступ к общим файлам и папкам напрямую из сообщения об отказе в доступе.  
  
## <a name="BKMK_NEW"></a>Функции, используемые в данном сценарии  
В следующей таблице перечислены компоненты, являющиеся частью данного сценария, и описано, как они поддерживают его.  
  
|Компонент|Способ поддержки сценария|  
|-----------|---------------------------------|  
|[Обзор диспетчера ресурсов файлового сервера](https://technet.microsoft.com/library/hh831701.aspx)|Помощь при отказе в доступе можно настроить с помощью консоли диспетчера ресурсов файлового сервера.|  
|[Обзор файлов и хранилищ служб](https://technet.microsoft.com/library/hh831487.aspx)|Диспетчер ресурсов файлового сервера — это роль файловых служб и служб хранилища, состоящая из набора компонентов, которые можно использовать для администрирования файловых серверов в сети.|  
  

