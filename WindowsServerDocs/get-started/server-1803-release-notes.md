---
title: Примечания к выпуску — важные проблемы в Windows Server версии 1803
description: Узнайте о любых известных проблемах, ограничениях или другой информации, необходимой перед установкой Windows Server версии 1803
ms.prod: windows-server
ms.date: 05/07/2018
ms.technology: server-general
ms.topic: article
author: lizap
ms.author: elizapo
manager: dougkim
ms.localizationpriority: medium
ms.openlocfilehash: a511c9888f27fe97fdeaf65cde022e5c2aa999d4
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2020
ms.locfileid: "80826087"
---
# <a name="release-notes-important-issues-in-windows-server-version-1803"></a>Заметки о выпуске. Важные проблемы в Windows Server версии 1803

>Область применения. Windows Server, Semi-Annual Channel

В этих примечаниях к выпуску кратко изложены наиболее важные проблемы в операционной системе Windows Server, включая способы устранения или обхода известных проблем. Подробные сведения о новых возможностях этого выпуска см. в статье [Новые возможности Windows Server версии 1803](whats-new-in-windows-server-1803.md). Ознакомьтесь со статьей [О контейнерах Windows](https://docs.microsoft.com/virtualization/windowscontainers/about/), если вас интересует запуск контейнера Windows Server версии 1803. 

Если не указано иное, все эти проблемы распространяются на все выпуски и варианты установи Windows Server версии 1803.  

Мы постоянно обновляем эту статью. В случае обнаружения известных проблем, мы будем описывать их здесь. 


## <a name="software-defined-datacenter"></a>Программно-определяемый центр обработки данных

Возможности программно-определяемого центра обработки данных, такие как Локальные дисковые пространства, программно-определяемые сети и экранированные виртуальные машины, не включены в состав Windows Server версии 1803. Как описано в [обновлении Windows Server Semi-Annual Channel](https://cloudblogs.microsoft.com/windowsserver/2018/03/29/windows-server-semi-annual-channel-update/), полугодовой канал Windows Server ориентирован на контейнеры и сценарии приложений, которые выигрывают от более быстрых инноваций. 

Если вам нужны инфраструктурные роли, используйте выпуск Long-Term Servicing Channel: Windows Server 2016 (доступен сейчас) или [Windows Server 2019](https://cloudblogs.microsoft.com/windowsserver/2018/03/20/introducing-windows-server-2019-now-available-in-preview) (ожидается в этом году).

Мы стремимся создать лучшую платформу для гиперконвергентной инфраструктуры и продолжаем разрабатывать новые функции и улучшать существующие на основе ваших отзывов. Благодарим вас за помощь в получении [более 10 000 кластеров дискового пространства прямого подключения](https://blogs.technet.microsoft.com/filecab/2018/03/27/storage-spaces-direct-momentum)! Мы планируем еще один выпуск новостей позднее в этом году.