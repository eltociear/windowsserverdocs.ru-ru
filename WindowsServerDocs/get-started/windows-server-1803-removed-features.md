---
title: Windows Server, версия 1803 — функции, которые были удалены
description: Сведения о компонентах, которые будут удалены или не будут поддерживаться в Windows Server версии 1803 и будущих версиях
ms.prod: windows-server-threshold
ms.mktglfcycl: plan
ms.localizationpriority: medium
ms.sitesec: library
author: lizap
ms.author: elizapo
ms.date: 05/10/2018
ms.openlocfilehash: c80738fe7ceda43a1a73adb0a8b1061bbb24319f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2019
ms.locfileid: "59886205"
---
# <a name="features-removed-or-planned-for-replacement-starting-with-windows-server-version-1803"></a>Удаленные или подлежащие замене компоненты в Windows Server версии 1803

> Относится к: Windows Server версии 1803

В каждом выпуске Windows Server добавляются новые возможности и функции. Иногда мы также удаляем компоненты и функциональные возможности; как правило, это происходит, когда мы добавляем улучшенную функцию. Ниже приведены подробные сведения о функциях и возможностях, которые были удалены в Windows Server версии 1803.   

> [!TIP]
> - Ранний доступ к сборкам Windows Server можно получить, вступив в [Программу предварительной оценки Windows](https://insider.windows.com), — это отличный способ для проверки изменений в функциональных возможностях.
> - У вас есть вопросы о других выпусках? Посмотрите сведения для [Windows Server 2016](deprecated-features.md)и [Windows Server версии 1709](removed-features-1709.md).

**Список может быть изменена и могут не включать каждый затрагиваемый компонент или функциональные возможности.** 

## <a name="features-we-removed-in-this-release"></a>Компоненты, которые были удалены в этой версии

Мы удалили следующие компоненты и функциональных возможностей из установленного образа продукта в Windows Server версии 1803. Приложения или код, которые зависят от этих функций, не будут работать в этом выпуске, если вы не используете какой-либо альтернативный метод.   

|Компонент    |Вместо этого можно использовать...|
|-----------|--------------------|
|[Служба репликации файлов](https://support.microsoft.com/en-us/help/4025991/windows-server-version-1709-no-longer-supports-frs)|Службы репликации файлов, представленные в Windows Server 2003 R2, замещаются функцией репликации DFS. Вам потребуется [перевести все контроллеры доменов, использующие FRS, на репликацию DFS с помощью SYSVOL](https://blogs.technet.microsoft.com/filecab/2014/06/25/streamlined-migration-of-frs-to-dfsr-sysvol/).|
|Виртуализация сети Hyper-V (HNV)|[Виртуализация сети](../networking/sdn/technologies/hyper-v-network-virtualization/whats-new-hyperv-network-virtualization-windows-server.md) теперь включена в Windows Server как часть решения [Программно-определяемая сеть](../networking/sdn/software-defined-networking.md) (SDN), которое также включает в себя контроллер сети, балансировку нагрузки программного обеспечения, определяемую пользователем маршрутизацию и списки управления доступом.|

## <a name="features-were-no-longer-developing"></a>Компоненты, которые мы больше не развиваем

Мы прекращаем активную разработку этих функций и, возможно, удалим их из будущих обновлений. Некоторые возможности заменены другими компонентами или функциями, а другие теперь доступны в иных источниках. 

>[!NOTE]
> Обратите внимание, что некоторые компоненты и роли, приведенные ниже, не включены в вариант установки Server Core, доступный в Windows Server версии 1803. Они *представлены* в варианте установки Server с возможностями рабочего стола, который мы последний раз выпустили для Windows Server 2016 и снова выпустим для Windows Server 2019.

Если у вас есть соображения о предлагаемой замене любой из этих функций, рекомендуем использовать [приложение Центра отзывов](https://support.microsoft.com/help/4021566/windows-10-send-feedback-to-microsoft-with-feedback-hub-app). 

|Компонент или роль    |Вместо этого можно использовать...|
|-----------|---------------------|
|Бизнес-сканирование, также известно как распределенное управление сканированием (DSM)|[Функция управления сканированием](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd759124\(v%3dws.11\)) была введена в Windows Server 2008 R2 и обеспечивала безопасное сканирование и управление сканированием в организации. Мы больше не будем вкладывать усилия в этот компонент, и сейчас не существует устройств, которые бы его поддерживали.|
|Технологии туннелирования IPv4/6 (6to4, ISATAP и прямое туннелирование)|Функция 6to4 отключена по умолчанию начиная с Windows 10 версии 1607 (юбилейное обновление), ISATAP отключена по умолчанию начиная с Windows 10 версии 1703 (Creators Update), а прямое туннелирование всегда было отключено по умолчанию. Вместо этого используйте встроенную поддержку IPv6.|
|[MultiPoint Services](../remote/multipoint-services/multipoint-services.md)|Мы больше не разрабатываем роль служб MultiPoint в составе Windows Server. Службы соединителя MultiPoint доступны в функции [Компонент по требованию](https://docs.microsoft.com/windows-hardware/manufacture/desktop/features-on-demand-v2--capabilities) для Windows Server и Windows 10. Можно использовать [Службы удаленных рабочих столов](../remote/remote-desktop-services/welcome-to-rds.md), в частности, Узел сеансов служб удаленных рабочих столов для обеспечения связи RDP. |
|[Автономные пакеты символов](https://docs.microsoft.com/windows-hardware/drivers/debugger/debugger-download-symbols) (MSI-файлы символов для отладки)|Мы больше не предлагаем пакеты символов в виде загружаемых MSI-файлов. Вместо этого [сервер символов (Майкрософт) станет хранилищем символов на основе Azure](https://blogs.msdn.microsoft.com/windbg/2017/10/18/update-on-microsofts-symbol-server/). Если вам требуются символы Windows, подключитесь к серверу символов (Майкрософт), чтобы закэшировать символы в локальном режиме, или используйте файл манифеста с SymChk.exe на компьютере с доступом в Интернет.|
|[Брокер подключений к удаленному рабочему столу и узел виртуализации удаленных рабочих столов](../remote/remote-desktop-services/desktop-hosting-service.md) в установке Server Core|В большинстве развертываний служб удаленных рабочих столов эти роли совместно размещаются с узлом сеансов удаленных рабочих столов (RDSH), что требует наличия Server с возможностями рабочего стола; для обеспечения единообразия в RDSH мы изменяем эти роли, и они также будут требовать Server с возможностями рабочего стола. Мы больше не разрабатываем эти роли RDS для использования в [установке Server Core](../administration/server-core/what-is-server-core.md). Если вам необходимо [развернуть эти роли как часть инфраструктуры удаленного рабочего стола](../remote/remote-desktop-services/rds-deploy-infrastructure.md), можно [установить их в Windows Server 2016 с возможностями рабочего стола](getting-started-with-server-with-desktop-experience.md). <br/><br/>Эти роли также включаются в вариант установки с возможностями рабочего стола в Windows Server 2019. Их можно проверить в [сборке программы предварительной оценки Windows для Windows Server 2019](https://docs.microsoft.com/windows-insider/at-work/), просто не забудьте выбрать образ LTSC. |
|[RemoteFX vGPU](../remote/remote-desktop-services/rds-remotefx-vgpu.md)|Мы разрабатываем новые параметры ускорения графики для виртуализованных сред. В качестве альтернативы также можно использовать [Дискретное назначение устройств (DDA)](../virtualization/hyper-v/plan/plan-for-deploying-devices-using-discrete-device-assignment.md).|
|[Политика программных ограничений](../identity/software-restriction-policies/software-restriction-policies.md) в групповой политике|Вместо использования политики программных ограничений в групповой политике можно использовать [AppLocker](https://docs.microsoft.com/windows/security/threat-protection/applocker/applocker-overview) или [управление приложениями в Защитнике Windows](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control) для управления тем, к каким приложениям пользователи могут получить доступ и какой код может выполняться в ядре.|
|Дисковые пространства в общей конфигурации с использованием структуры SAS|Вместо этого разворачивайте [локальные дисковые пространства](../storage/storage-spaces/storage-spaces-direct-overview.md). Локальные дисковые пространства поддерживают использование сертифицированных HLK корпусов SAS, но в конфигурации без общего доступа, как описано в [требованиях к оборудованию локальных дисковых пространств](../storage/storage-spaces/storage-spaces-direct-hardware-requirements.md).|
|Режим Windows Server Essentials|Мы больше не разрабатываем роль режима Essentials для Windows Server Standard и SKU Windows Server Datacenter. Если вам требуется простое серверное решение для предприятий малого и среднего бизнеса, проверьте наше новое решение [Microsoft 365 для бизнеса](https://www.microsoft.com/microsoft-365/business) или используйте [Windows Server 2016 Essentials](https://docs.microsoft.com/windows-server-essentials/get-started/get-started).|
