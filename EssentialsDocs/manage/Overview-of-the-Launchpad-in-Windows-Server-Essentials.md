---
title: Обзор Launchpad в Windows Server Essentials
description: Описывает способ использования Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 198d16cb-3d07-4706-be89-ad14a5f7dc47
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 4dd32d57f6f36bdbf94c763fe0cbd1f37ff990b8
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/31/2019
ms.locfileid: "66433109"
---
# <a name="overview-of-the-launchpad-in-windows-server-essentials"></a>Обзор Launchpad в Windows Server Essentials

>Область применения. Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Панель запуска Windows Server Essentials представляет собой небольшое приложение, устанавливаемое на компьютере при первом подключении компьютера к серверу. Панель запуска предоставляет прошедшим проверку пользователям доступ к основным возможности Windows Server Essentials, включая архивацию компьютеров, общие файлы и мультимедиа, а также сайт удаленного веб-доступа. Пользователи могут получить доступ к этим возможностям с компьютеров, как присоединенных, так и не присоединенных к домену. Кроме того, панель запуска предоставляет в реальном времени информацию и уведомления о работоспособности компьютера. Администраторы могут использовать панель запуска для доступа к панели мониторинга сервера, даже если компьютер не подключен к сети.  
  
 Изготовители оборудования и независимые поставщики программного обеспечения, занимающиеся разработкой надстроек для Windows Server Essentials, могут использовать панель запуска для распространения функциональности надстроек на компьютеры в сети.  
  
 Использование панели запуска Windows Server Essentials поддерживают следующие операционные системы Windows:  
  
- **Windows 8**: все выпуски.  
  
- **Windows 7**: все выпуски.  
- **Windows 10**: все выпуски. 
  
  Следующие операционные системы Windows не поддерживают использование панели запуска Windows Server Essentials:  
  
- **Дополнительные серверы**: панель запуска Windows Server Essentials нельзя использовать на других компьютерах под управлением операционной системы Windows Server.  
  
  Содержание раздела:  
  
- [Использовать панель запуска](Overview-of-the-Launchpad-in-Windows-Server-Essentials.md#BKMK_Launchpad)  
  
- [Использование панели запуска на компьютере Mac](Overview-of-the-Launchpad-in-Windows-Server-Essentials.md#BKMK_Mac)  
  
##  <a name="BKMK_Launchpad"></a> Использовать панель запуска  
 В панели запуска Windows Server Essentials доступны следующие сведения и ссылки.  
  
### <a name="backup"></a>Резервное копирование  
 Щелкните элемент **Архивация** , чтобы открыть **Свойства архивации** для данного компьютера. На странице **Свойства архивации** можно выполнить следующие действия:  
  
- Запуск и остановка архивации.  
  
- Просмотр состояния и сведений о последней архивации.  
  
- Указание способа управления питанием компьютера при выполнении архивации.  
  
  Сведения об использовании панели запуска для архивации данных компьютера, см. в разделе [Управление архивацией клиента](Manage-Client-Computer-Backup-in-Windows-Server-Essentials.md).  
  
### <a name="remote-web-access"></a>Удаленный веб-доступ  
 Щелкните элемент **Удаленный веб-доступ**, чтобы открыть сайт удаленного веб-доступа в веб-браузере. Сайт удаленного веб-доступа позволяет подключиться к другим компьютерам и получить доступ к некоторым сетевым ресурсам из офиса или из любого удаленного расположения с компьютера, подключенного к сети Интернет. Дополнительные сведения об удаленном веб-доступе см. в разделе [Manage Remote Web Access](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md).  
  
### <a name="shared-folders"></a>Общие папки  
 Щелкните элемент **Общие папки**, чтобы открыть расположение общих папок на сервере в проводнике. Сведения об общем доступе к файлам и папкам см. в разделе [Управление серверными папками](Manage-Server-Folders-in-Windows-Server-Essentials.md).  
  
### <a name="dashboard"></a>Информационная панель  
 Щелкните элемент  **Панель мониторинга** , чтобы открыть страницу **входа** для доступа к панели мониторинга Windows Server Essentials. После входа открывается подключение к удаленному рабочему столу для панели мониторинга сервера. Дополнительные сведения о панели мониторинга, см. в разделе [Обзор панели мониторинга](Overview-of-the-Dashboard-in-Windows-Server-Essentials.md).  
  
> [!NOTE]
>  Чтобы использовать эту возможность, необходимы права доступа или разрешения для входа на сервер.  
  
### <a name="microsoft-office-365"></a>Microsoft Office 365  
 Ссылка **Microsoft Office 365** отображается на панели доступа только при наличии у пользователя учетной записи Office 365. Щелкните элемент  **Microsoft Office 365** , чтобы получить доступ к дополнительным ссылкам на ресурсы Office 365. Дополнительные сведения см. в разделе [краткое руководство по использованию Microsoft Office 365](../use/Quick-Start-Guide-to-Using-Microsoft-Office-365-with-Windows-Server-Essentials.md).  
  
### <a name="computer-health-alerts"></a>Оповещения о работоспособности компьютера  
 Оповещения, отображаемые на панели запуска, содержат краткую информацию о текущем состоянии работоспособности компьютера. Чтобы просмотреть информацию оповещения о работоспособности, щелкните индикатор оповещения для открытия средства просмотра оповещений. Оповещения о работоспособности отображаются в средстве просмотра в зависимости от уровня серьезности. Наиболее серьезные предупреждения находятся в начале списка, а наименее серьезные — в конце. Дополнительные сведения об оповещениях о работоспособности компьютера см. в разделе [Manage System Health](Manage-System-Health-in-Windows-Server-Essentials.md).  
  
##  <a name="BKMK_Mac"></a> Использование панели запуска на компьютере Mac  
 Можно подключить компьютер Mac® под управлением Mac OS X® x® 10.5 или более поздней версии, Windows Server Essentials, Windows Server Essentials или Windows Server 2012 R2, либо путем скачивания и установки программного обеспечения connector. После завершения установки программного обеспечения соединителя можно автоматически запускать панель запуска во время запуска системы.  
  
 Панель запуска представляет собой небольшое приложение, которое предоставляет прошедшим проверку пользователям доступ к основные возможностям сервера, включая общие файлы и мультимедиа, надстройки и удаленный веб-доступ. Кроме того, панель запуска предоставляет в реальном времени информацию и уведомления о работоспособности компьютера.  
  
> [!NOTE]
>  Администраторы сервера не могут использовать панель запуска или удаленный веб-доступ на компьютере Mac для открытия панели мониторинга сервера и управления этим сервером.  
  
### <a name="backup"></a>Резервное копирование  
 Щелкните элемент **Архивация**, чтобы настроить Time Machine на архивацию компьютера и изменить параметры Time Machine. Дополнительные сведения о Time Machine см. в документации, предоставляемой изготовителем компьютера.  
  
### <a name="remote-web-access"></a>Удаленный веб-доступ  
 Нажмите кнопку **удаленного веб-доступа** для открытия веб-браузер на сайт удаленного веб-доступа. Удаленный веб-доступ обеспечивает доступ к общим файлам и папкам на сервере из любого удаленного расположения с компьютера, подключенного к Интернету. Можно отправлять файлы, воспроизводить музыку и видео в веб-службе Media Play, а также просматривать изображения и слайд-шоу. Дополнительные сведения см. в разделе [Use Remote Web Access](../use/Use-Remote-Web-Access-in-Windows-Server-Essentials.md).  
  
### <a name="shared-folders"></a>Общие папки  
 Щелкните элемент **Общие папки**, чтобы открыть расположение общих папок на сервере в средстве поиска. Сведения об общем доступе к файлам и папкам см. в разделе [использование общих папок](../use/Use-Shared-Folders-in-Windows-Server-Essentials.md).  
  
### <a name="computer-health-alerts"></a>Оповещения о работоспособности компьютера  
 Оповещения, отображаемые на панели запуска, содержат краткую информацию о текущем состоянии работоспособности компьютера. Чтобы просмотреть информацию оповещения о работоспособности, щелкните индикатор оповещения для открытия средства просмотра оповещений. Оповещения о работоспособности отображаются в средстве просмотра в зависимости от уровня серьезности. Наиболее серьезные предупреждения находятся в начале списка, а наименее серьезные — в конце.  
  
## <a name="see-also"></a>См. также  
  
-   [Установка подключения](../use/Get-Connected-in-Windows-Server-Essentials.md)  
  
-   [Использование Windows Server Essentials](../use/Use-Windows-Server-Essentials.md)  
  
-   [Управление Windows Server Essentials](Manage-Windows-Server-Essentials.md)