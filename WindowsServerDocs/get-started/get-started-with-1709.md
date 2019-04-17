---
title: Знакомство с Windows Server версии 1709
description: Инструкции по получению, установке и активации
ms.prod: windows-server-threshold
ms.mktglfcycl: manage
ms.sitesec: library
author: jaimeo
ms.localizationpriority: high
ms.date: 12/5/2017
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 9cf87597-b15d-4f43-8aa1-91e60367f011
ms.openlocfilehash: a2da7b8437a9dc7f44fc83837e3ebad93b7fe3ab
ms.sourcegitcommit: e0479b0114eac7f232e8b1e45eeede96ccd72b26
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/22/2018
ms.locfileid: "1410406"
---
# <a name="introducing-windows-server-version-1709"></a>Знакомство с Windows Server версии 1709

>Область применения: Windows Server (Semi-Annual Channel)

**Windows Server версии 1709— первый выпуск в новом канале Semi-Annual Channel.** 

## <a name="what-the-semi-annual-channel-is--and-isnt"></a>Описание канала Semi-Annual Channel
Windows Server версии 1709 как первый выпуск в этом новом канале *не* является обновлением или пакетом обновлений для Windows Server 2016. Это первый из серверных выпусков, которые выходят два раза в год в **новом канале выпусков**, предназначенном для клиентов, которые переходят на «облачный жизненный цикл», например клиентов, которые используют ускоренные циклы разработки, или поставщиков услуг размещения, которые поддерживают последние инвестиции в Hyper-V. Для каждого выпуска в этом канале будет предоставляться поддержка в течение 18 месяцев, начиная с даты начального выпуска. Дополнительные сведения о канале Semi-Annual Channel, а также **советы по выбору канала** см. в разделе [Обзор канала Semi-Annual Channel](semi-annual-channel-overview.md).


**Текущий продукт в канале Long-Term Servicing Channel (LTSC)— Windows Server 2016**. LTSC лучше всего подходит вам, если вам требуется долгосрочная стабильность и предсказуемость серверной операционной системы для поддержки традиционных рабочих нагрузок и приложений. Чтобы остаться в канале LTSC, необходимо установить (или продолжить использовать) ОС Windows Server 2016, которую можно установить в режиме основных серверных компонентов или в режиме сервера с возможностями рабочего стола. Подробные сведения см. в разделе [Начало работы с Windows Server 2016](https://docs.microsoft.com/windows-server/get-started/server-basics).


## <a name="whats-different-about-1709"></a>Отличия версии 1709

Windows Server версии 1709 выполняется в режиме основных серверных компонентов. Это означает, что графического пользовательского интерфейса нет, а управление осуществляется удаленно. Тем не менее, эта особенность обеспечивает отличные преимущества, такие как более низкие требования к оборудованию, значительно уменьшенная уязвимость, а также снижение потребности в обновлениях. Если вы только начинаете работать с основными серверными компонентами, ознакомьтесь с разделом [Управление сервером в режиме основных серверных компонентов](../administration/server-core/server-core-manage.md), чтобы освоиться в этой среде. В разделе [Управление Windows Server 2016](../administration/manage-windows-server.md) представлены различные варианты удаленного управления серверами.

В разделе [Новые возможности Windows Server версии 1709](whats-new-in-windows-server-1709.md) вы узнаете о новых компонентах и возможностях, появившихся в Windows Server версии 1709.

### <a name="why-does-windows-server-version-1709-offer-only-the-server-core-installation-option"></a>Почему в Windows Server версии 1709 в качестве варианта установки доступен лишь режим основных серверных компонентов?
Одним из важнейших наших шагов при планировании каждого выпуска Windows Server является учет отзывов клиентов о том, как они используют Windows Server. Какие новые возможности окажут наибольшее влияние на среды Windows Server и, следовательно, на текущую деятельность компании? Согласно вашим отзывам, приоритетной задачей является максимально быстрое и эффективное внедрение инноваций. В то же время, клиенты, внедряющие инновации наиболее быстро, сообщили нам, что они в основном используют сценарии командной строки в PowerShell для управления центрами обработки данных, поэтому при установке Windows Server с возможностями рабочего стола им едва ли потребуется графический пользовательский интерфейс рабочего стола. Отдавая предпочтение варианту установки в режиме основных серверных компонентов, мы получаем возможность направить больше ресурсов на нововведения, сохраняя при этом присущие платформе Windows Server возможности и широкий спектр поддерживаемых приложений. Оставить отзыв, предложение или комментарий об этой или других проблемах, связанных с Windows Server или будущими выпусками, можно в [Центре отзывов](https://support.microsoft.com/help/4021566/windows-10-send-feedback-to-microsoft-with-feedback-hub-app).


### <a name="what-about-nano-server"></a>Как насчет Nano Server?
Сервер Nano Server доступен в качестве операционной системы контейнера. Подробные сведения см. в разделе [Изменения сервера Nano Server в канале Semi-Annual Channel Windows Server](nano-in-semi-annual-channel.md).

## <a name="additional-information-about-this-release"></a>Дополнительные сведения об этом выпуске
Чтобы получить полное представление об основных фактах, касающихся Windows Server версии 1709, следует также ознакомиться со следующими разделами перед установкой данной ОС:

- Какое оборудование необходимо для запуска этой ОС? См. раздел [Требования к системе](system-requirements.md). Системные требования для этого выпуска совпадают с требованиям для Windows Server 2016.
- Какие новые компоненты и возможности добавлены в этой версии? См. раздел [Новые возможности Windows Server версии 1709](whats-new-in-windows-server-1709.md)
- Какие компоненты были удалены? См. раздел [Удаленные или подлежащие замене компоненты в Windows Server (версия 1709)](Removed-Features-1709.md)
- Какие проблемы, связанные с этим выпуском, необходимо устранить? См. раздел [Заметки о выпуске. Важные проблемы в Windows Server версии 1709](server-1709-relnotes.md)


## <a name="where-to-obtain-windows-server-version-1709"></a>Получение Windows Server версии 1709

Для этого выпуска следует применять чистую установку.

- VLSC: корпоративным клиентам, участвующим в программе [Software Assurance](https://www.microsoft.com/en-us/licensing/licensing-programs/software-assurance-default.aspx), для получения этого выпуска следует перейти на веб-сайт [Volume Licensing Service Center](https://www.microsoft.com/Licensing/servicecenter/default.aspx) и нажать кнопку **Вход**. Затем необходимо щелкнуть **Загрузки и ключи** и найти этот выпуск. 

- Windows Server версии 1709 также доступна на платформе [Microsoft Azure ](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.WindowsServer?tab=Overview).

- Участники программы **Подписки на Visual Studio:** если вы уже участвуете в программе подписок на Visual Studio, то для получения Windows Server версии 1709 перейдите на [страницу скачивания для подписчиков Visual Studio](https://my.visualstudio.com/downloads?pid=2347) и скачайте расположенные на ней файлы. Если вы еще не являетесь подписчиком, перейдите на страницу [Подписки на Visual Studio](https://www.visualstudio.com/subscriptions/), зарегистрируйтесь, а затем перейдите на [страницу скачивания для подписчиков Visual Studio](https://my.visualstudio.com/downloads?pid=2347), как указано выше. Выпуски, полученные с помощью подписок Visual Studio, используются только для разработки и тестирования.




## <a name="activating-windows-server-version-1709"></a>Активация Windows Server версии 1709

- Если вы получили этот выпуск через центр Volume Licensing Service Center, для активации воспользуйтесь ключом активации Windows Server 2016.
- Если вы используете Microsoft Azure, выпуск должен активироваться автоматически.
- Если вы получили этот выпуск в рамках программы подписок на Visual Studio, он должен активироваться автоматически.