---
title: Управление
description: Из этой статьи вы узнаете о средствах, рекомендациях, а также инструкциях по управлению Windows Server
ms.prod: windows-server
layout: LandingPage
ms.technology: manage
ms.topic: landing-page
author: lizap
ms.author: elizapo
ms.localizationpriority: high
ms.openlocfilehash: 4166d4e8d2819946cdc859ef643cf53315e7290a
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2020
ms.locfileid: "71370418"
---
# <a name="management"></a>Управление


>[!TIP]
> Ищете дополнительные сведения о предыдущих версиях Windows Server? Ознакомьтесь с другими нашими [библиотеками Windows Server](/previous-versions/windows/) на сайте docs.microsoft.com. Кроме того, вы можете найти нужную информацию [на этом сайте](https://docs.microsoft.com/search/index?search=Windows+Server&dataSource=previousVersions).

<hr />

После развертывания Windows Server в вашей среде, в том числе ролей для необходимых компонентов и функций, вам нужно обеспечить управление этими серверами. Windows Server предоставляет несколько средств, которые помогут вам ознакомиться со средой Windows Server, методами управления определенными серверами, точной настройки производительности и автоматизации многих задач управления. 

Инструменты, используемые для управления экземплярами Windows Server, во многом зависят от типов развернутых систем (Windows Server с возможностями рабочего стола или основные серверные компоненты), типа компьютеров (физические или виртуальные) и расположения серверов. Воспользуйтесь следующими сведениями о выполнении базовых задач управления Windows Server.

Используйте следующую таблицу, чтобы определить, какие средства применять.

| Я   | Установка и запуск Windows Admin Center | Запуск диспетчера серверов в Windows Server | Запуск диспетчера серверов в RSAT в Windows 10 |
|--------|----------------------|--------------------------------------|------------------------------------------|
| использую ПК с Windows 10 | X  |                                      | X                                        |
| использую систему Windows Server с возможностями рабочего стола | X | X | X |
| использую систему Windows Server с основными серверными компонентами |X (установка в Windows 10, используется для управления основными серверными компонентами) | | X |
| нахожусь далеко от системы Windows Server |X | | X |
| нахожусь далеко от системы Windows Server, но мне доступны возможности рабочего стола |X | Используйте RDS для удаленного доступа к серверу, а затем используйте диспетчер серверов | X |

В дополнение к средствам, описанным ниже, вы также можете использовать [службы удаленных рабочих столов](../remote/remote-desktop-services/welcome-to-rds.md) для доступа к локальным, удаленным и виртуальным серверам. Более того, вы можете использовать диспетчер серверов для выполнения задач управления.

<HR />

<ul class="cardsI panelContent">
<li>
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../media/i-manage.svg" alt="" />
                        </div>
                    </div>
                    <div class="cardText">
                    <h3>Управление системами и средами Windows Server</h3>
<HR />
                        <p><h3><a href="../manage/windows-admin-center/overview.md">Управление локальными системами, удаленными системами и системами без пользовательского интерфейса с помощью Windows Admin Center</a></h3>Windows Admin Center — это браузерное приложение для управления системами с Windows Server независимо от Azure или облака в локальной среде. Windows Admin Center (предыдущее название — Project Honolulu) предоставляет полный контроль над всеми аспектами серверной инфраструктуры и особенно полезен для администрирования в частных сетях, которые не подключены к Интернету. Windows Admin Center можно установить в Windows 10, на сервере шлюза или непосредственно в системе Windows Server, которой вы управляете.</p>
<HR />
                        <p><h3><a href="server-manager/server-manager.md">Управление локальными системами с помощью диспетчера серверов</a></h3>Консоль управления включена в полную установку Windows Server. (Она недоступна для установок, которые не имеют пользовательского интерфейса — основные компоненты сервера не включают диспетчер серверов.) С помощью диспетчера серверов вы можете устанавливать и удалять роли серверов, добавлять и отключать удаленные серверы, запускать и останавливать службы, а также просматривать собранные данные о среде.</p>
<HR />
                        <p><h3><a href="../remote/remote-server-administration-tools.md">Управление удаленными системами и системами без пользовательского интерфейса с помощью средств удаленного администрирования сервера (RSAT)</a></h3>Если в среде есть установки основных серверных компонентов или удаленные серверы (локальные или виртуальные машины), для управления этими системами можно использовать средства удаленного администрирования сервера (RSAT). В RSAT включен диспетчер серверов, поэтому вы сможете использовать его для управления всеми серверами. Обратите внимание, что средства удаленного администрирования сервера работают в Windows 10. Средства RSAT нельзя установить в основных серверных компонентах Windows. Вы также можете управлять установками основных серверных компонентов из командной строки. Подробнее см. в статье <a href="server-core/server-core-administer.md">Administer a Server Core server</a>
 (Администрирование сервера с основными серверными компонентами).<HR />
                        <p><h3><a href="windows-server-update-services/get-started/windows-server-update-services-wsus.md">Управление системами Windows Server</a></h3>Используйте службы Windows Server Update Services (WSUS) для развертывания обновлений в системах в среде Windows Server и управления ими.</p>
                    </div>
                </div>
            </div>
        </div>
    </li>
<li>
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../media/i-manage.svg" alt="" />
                        </div>
                    </div>
                    <div class="cardText">
                    <h3>Сбор сведений о среде</h3>
<HR />
                        <p><h3><a href="get-started-with-setup-and-boot-event-collection.md">Сбор событий установки и загрузки</a></h3>Функция сбора событий установки и загрузки позволяет назначить "компьютер-сборщик", который может собирать различные важные события, возникающие на других компьютерах в ходе загрузке или установки. Затем вы можете проанализировать собранные события с помощью компонента "Просмотр событий", анализатора сообщений, Wevtutil или командлетов Windows PowerShell. </p>
<HR />
                        <p><h3><a href="software-inventory-logging/get-started-with-software-inventory-logging.md">Инвентаризация программного обеспечения (SIL)</a></h3>Журнал инвентаризации программного обеспечения в Windows Server — это компонент с простым набором командлетов PowerShell, который помогает администраторам получить список программ Майкрософт, установленных на их серверах. Он также предоставляет возможность периодически собирать и перенаправлять эти данные по сети с помощью протокола HTTPS для статистической обработки. Управление этим компонентом, главным образом для ежечасного сбора и перенаправления, также выполняется с помощью команд PowerShell.</p>
<HR />
                        <p><h3><a href="user-access-logging/get-started-with-user-access-logging.md">Ведение журнала доступа пользователей</a></h3>Компонент ведения журнала доступа пользователей объединяет уникальные события клиентских устройств и запросов пользователей, которые регистрируются на компьютере с Windows Server 2016, Windows Server 2012 R2 или Windows Server 2012 в локальной базе данных. Доступ к этим записям (с помощью запроса администратора сервера) позволяет получать сведения о количестве и экземплярах по роли сервера, пользователю, устройству, локальному серверу и дате. Кроме того, служба UAL предоставляет сторонним разработчикам программного обеспечения возможности реализовать в коде события UAL, которые должны собираться. </a>
                    </div>
                </div>
            </div>
        </div>
    </li>
<li>
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../media/i-manage.svg" alt="" />
                        </div>
                    </div>
                    <div class="cardText">
                    <h3>Настройка среды Windows Server для обеспечения высокой производительности</h3>
<HR />
                        <p><h3><a href="performance-tuning/index.md">Руководство по обеспечению высокой производительности</a></h3>Изучите набор рекомендаций, которые можно использовать для настройки параметров сервера в Windows Server и повышения производительности или экономии электроэнергии, особенно в случаях с изменением характера рабочих нагрузки со временем.</p>
<HR />
                        <p><h3><a href="server-performance-advisor/microsoft-server-performance-advisor.md">Microsoft Server Performance Advisor</a></h3>С помощью Microsoft Server Performance Advisor (SPA) вы можете в фоновом режиме собирать показатели для диагностики проблем с производительностью на серверах Windows без добавления программных агентов или перенастройки производственных серверов. SPA создает подробные отчеты о производительности и ретроспективные диаграммы с рекомендациями.</p>
                    </div>
                </div>
            </div>
        </div>
    </li>
<li>
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../media/i-manage.svg" alt="" />
                        </div>
                    </div>
                    <div class="cardText">
                    <h3>Автоматизация управления Windows Server</h3>
<HR />
                        <p><h3><a href="https://docs.microsoft.com/powershell/scripting/powershell-scripting?view=powershell-5.1">Windows PowerShell</a></h3>Windows PowerShell — это оболочка командной строки и язык сценариев, созданный для быстрой автоматизации задач администрирования. </p>
<HR />
                        <p><h3><a href="windows-commands/windows-commands.md">Команды Windows</a></h3>Средства командной строки Windows используются для выполнения административных задач в Windows. Вы можете воспользоваться справочником по командам, чтобы ознакомиться со средствами командной строки, командной оболочкой и методами автоматизации задач командной строки с помощью пакетных файлов или средств написания сценариев.</p>
                    </div>
                </div>
            </div>
        </div>
    </li>
<li>
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../media/i-manage.svg" alt="" />
                        </div>
                    </div>
                    <div class="cardText">
                    <h3>Автоматизация управления Windows Server</h3>
<HR />
                        <p><h3><a href="..\manage\system-insights\overview.md">Системная аналитика</h3></a>Встроенные средства прогнозной аналитики локально анализируют системные данные Windows Server, например счетчики производительности или события трассировки событий Windows, помогая ИТ-администраторам упреждающим образом выявлять и устранять проблемы в развертываниях.</p>
                    </div>
                </div>
            </div>
        </div>
    </li>
</ul>