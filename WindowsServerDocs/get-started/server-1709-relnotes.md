---
title: Заметки о выпуске. Важные проблемы в Windows Server версии 1709
description: Сводные данные о критических проблемах, требующих обходных действий во избежание аварийного завершения, "зависания", ошибки установки и потери данных.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.date: 04/23/2018
ms.technology: server-general
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 134aab85-664f-4d44-87ef-9e5fd389071f
author: jaimeo
ms.author: jaimeo
manager: dougkim
ms.localizationpriority: medium
ms.openlocfilehash: 4eebc498289a81c7f27fcf4b84d81ae13bc38e4f
ms.sourcegitcommit: e84e328c13a701e8039b16a4824a6e58a6e59b0b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/22/2018
ms.locfileid: "4133860"
---
# Заметки о выпуске. Важные проблемы в Windows Server версии 1709

>Область применения: Semi-Annual Channel для Windows Server

В этих заметках о выпуске приведены сводные данные о наиболее важных проблемах в операционной системе Windows Server&reg;, включая информацию о способах устранения или обхода этих проблем, если таковые известны. Информацию об изменениях структуры, новых компонентах и исправлениях в этом выпуске см. в статье [Новые возможности Windows Server версии 1709](whats-new-in-windows-server-1709.md) и в сообщениях групп разработчиков конкретных компонентов. Если не указано иное, эти заметки распространяются на все выпуски и варианты установки Windows Server 2016.  

Этот документ постоянно обновляется. По мере обнаружения критических проблем, определения обходных путей и выпуска исправлений в документ добавляются соответствующие сведения.  
  
## Локальные дисковые пространства
[comment]: # (ИД: неизвестный; Поставщик: stevenek; Состояние: утверждено)  
Локальные дисковые пространства не входят в состав Windows Serverверсии 1709. Если вызвать командлет *Enable-ClusterStorageSpacesDirect* или его псевдоним *Enable-ClusterS2D* на сервере с Windows Server версии 1709, отобразится сообщение об ошибке "Запрошенная операция не поддерживается".

Также она не поддерживается при добавлении серверов с Windows Server версии 1709 в среду локальных дисковых пространств Windows Server 2016.

Модель выпуска Windows Server предлагает новый вариант установки с целью обеспечения соответствия сходным моделям выпуска и обслуживания для [Windows 10](https://docs.microsoft.com/windows/deployment/update/waas-overview) и [Office 365 профессиональный плюс](https://support.office.com/article/Overview-of-the-upcoming-changes-to-Office-365-ProPlus-update-management-78b33779-9356-4cdf-9d2c-08350ef05cca?ui=en-US&rs=en-US&ad=US). Выпуски Semi-Annual Channel предоставляют новые возможности пользователям, которым необходимы быстрые циклы обновления, и будут выходить дважды в год— весной и осенью.

Windows Server канале Semi-Annual Channel уделено контейнеров и сценарии с приложениями ускоренные инновации приносят пользу, приведено в [блоге](https://cloudblogs.microsoft.com/windowsserver/2018/03/29/windows-server-semi-annual-channel-update) для получения дополнительной информации. Клиентов, пытавшихся найти инфраструктурные роли, такие как локальные дисковые пространства, следует использовать Long-Term Servicing Channel выпусках, таких как Windows Server 2016 (доступно, теперь) и [Windows Server 2019](https://cloudblogs.microsoft.com/windowsserver/2018/03/20/introducing-windows-server-2019-now-available-in-preview) (скоро позже в этом году). Мы стремимся построении лучшей платформой для гиперконвергентной инфраструктурой, и мы продолжаем разрабатывать новые возможности и усовершенствования уже имеющихся на основе ваших отзывов. 

Локальные дисковые пространства впервые появились в Windows Server 2016 являются основанием для нашей гиперконвергентной платформы. Мы рады тому, насколько положительно пользователи приняли гиперконвергентную платформу Майкрософт, и делаем для них все возможное.

Мы были прослушивание на ваш отзыв и являются разрабатываем [следующий набор нововведений](https://blogs.technet.microsoft.com/windowsserver/2017/09/07/sneak-peek-2-windows-server-version-1709-hyper-converged-infrastructure/) для нашей гиперконвергентной платформы. Эти возможности уже доступны в сборках [Программы предварительной оценки Windows](https://insider.windows.com/for-business/) , и нам бы хотелось, попробуйте воспользоваться ими и поделитесь своим мнением. Клиентам, которым нужно проверенное гиперконвергентное решение, мы рекомендуем программу [Windows Server Software Defined](http://microsoft.com/wssd).