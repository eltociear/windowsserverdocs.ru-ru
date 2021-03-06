---
title: Управление локальным сервером и консолью диспетчера серверов
description: Диспетчер сервера
ms.prod: windows-server
ms.technology: manage-server-manager
ms.topic: article
ms.assetid: eeb32f65-d588-4ed5-82ba-1ca37f517139
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d64d45fec0c48f66da72dfee7ab9f1f9965205ad
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851497"
---
# <a name="manage-the-local-server-and-the-server-manager-console"></a>Управление локальным сервером и консолью диспетчера серверов

>Область применения: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

В Windows Server диспетчер сервера позволяет управлять как локальным сервером (если выполняется диспетчер сервера на Windows Server, так и не в клиентской операционной системе под управлением Windows) и удаленными серверами, работающими под управлением Windows Server 2008 и более поздних версий операционной системы Windows Server.

На странице **локальный сервер** в Диспетчер сервера отображаются свойства сервера, события, данные счетчика производительности и службы, а также результаты анализатор соответствия рекомендациям (BPA) для локального сервера. Плитки событий, служб, плитки анализатора соответствия рекомендациям (BPA) и плитки производительности работают так, как на страницах групп серверов и ролей. Дополнительные сведения о настройке данных, которые отображаются на этих плитках, см. в разделах [View и Configure Performance, Event, и Service Data](view-and-configure-performance-event-and-service-data.md) и [Run Best Practices Analyzer Scans и Manage Scan Results](run-best-practices-analyzer-scans-and-manage-scan-results.md).

Команды меню и параметры в панелях заголовков консоли диспетчер сервера применяются глобально ко всем серверам в пуле серверов и позволяют использовать диспетчер сервера для управления всем пулом серверов.

В этом разделе содержатся следующие подразделы:

-   [Завершение работы локального сервера](#BKMK_shutdown)

-   [Настройка свойств диспетчер сервера](#BKMK_props)

-   [Управление консолью диспетчер сервера](#BKMK_managesm)

-   [Настройка средств, отображаемых в меню "Сервис"](#BKMK_tools)

-   [Управление ролями на домашних страницах ролей](#BKMK_roles)

## <a name="shut-down-the-local-server"></a><a name=BKMK_shutdown></a>Завершение работы локального сервера
Меню **задачи** на плитке **свойства** локального сервера позволяет запустить сеанс Windows PowerShell на локальном сервере, открыть оснастку MMC " **Управление компьютером** " или открыть оснастки MMC для ролей или компонентов, установленных на локальном сервере. Также завершить работу локального сервера можно с помощью команды **Завершить работу локального сервера** в меню **Задачи**. Команда **Завершить работу локального сервера** также доступна для локального сервера на плитке **Серверы** на странице **Все серверы** либо на любой странице роли или группы, на которой представлен локальный сервер.

Завершение работы локального сервера с помощью этого метода, в отличие от завершения работы Windows Server 2016 на **начальном** экране, открывает диалоговое окно **Завершение работы Windows** , которое позволяет указать причины завершения работы в области " **средство регистрации событий завершения работы** ".

> [!NOTE]
> Завершить работу сервера или перезагрузить его могут только члены группы "Администраторы". Обычные пользователи не могут завершить работу сервера или перезагрузить его. В результате выполнения команды **Завершить работу локального сервера** сеансы обычных пользователей на сервере закрываются. При этом происходит то же самое, что и при выполнении команды завершения работы **Alt+F4** обычным пользователем на рабочем столе сервера.

## <a name="configure-server-manager-properties"></a><a name=BKMK_props></a>Настройка свойств диспетчер сервера
На плитке **Свойства** на странице **Локальный сервер** можно просмотреть или изменить следующие параметры. Чтобы изменить значение параметра, щелкните гипертекстовых значений параметра.

> [!NOTE]
> Обычно свойства, отображаемые на плитке **Свойства** локального сервера, можно изменить только на локальном сервере. Невозможно изменить свойства локального сервера с удаленного компьютера с помощью диспетчер сервера, так как плитка " **Свойства** " может получать только сведения о локальном компьютере, а не на удаленных компьютерах.
> 
> Так как многие свойства, отображаемые на плитке **Свойства** , управляются средствами, которые не являются частью Диспетчер сервера (например, панель управления), изменения параметров **свойств** не всегда немедленно отображаются на плитке **Свойства** . По умолчанию данные плитки **Свойства** обновляются каждые две минуты. Чтобы немедленно обновить **Свойства** данных, нажмите кнопку **Обновить** в адресной строке Диспетчер сервера.

|Параметр|Описание|
|------|--------|
|имя компьютера|Отображает понятное имя компьютера и открывает диалоговое окно **Свойства системы** , которое позволяет изменить имя сервера, членство в домене и другие системные параметры, такие как профили пользователей.|
|Домен (или "Рабочая группа", если сервер не присоединен к домену)|Отображает домен или рабочую группу, членом которой является сервер. Открывает диалоговое окно **Свойства системы** , которое позволяет изменить имя сервера, членство в домене и другие параметры системы, такие как профили пользователей.|
|брандмауэр Windows|Отображает состояние брандмауэра Windows для локального сервера. Открывает раздел **Панель управления\Система и безопасность\Брандмауэр Windows**. Дополнительные сведения о настройке брандмауэра Windows см. в разделе [Брандмауэр Windows в режиме повышенной безопасности и IPsec](https://go.microsoft.com/fwlink/?LinkId=253465).|
|удаленное управление|Отображает диспетчер сервера и состояние удаленного управления Windows PowerShell. Открывает диалоговое окно **Настройка удаленного управления** . Дополнительные сведения об удаленном управлении см. [в разделе Настройка удаленного управления в Диспетчер сервера](configure-remote-management-in-server-manager.md).|
|Удаленный рабочий стол|Показывает, могут ли пользователи подключаться к серверу удаленно с помощью сеансов удаленного рабочего стола. Открывает вкладку **Удаленный** диалогового окна **Свойства системы** .|
|объединение сетевых карт.|Показывает, участвует ли локальный сервер в объединении сетевых карт. Открывает диалоговое окно **Объединение сетевых карт** и позволяет присоединить локальный сервер к объединению сетевых карт, если это требуется. Дополнительные сведения об объединении сетевых карт см. в [техническом документе об объединении сетевых карт](https://go.microsoft.com/fwlink/?LinkID=253449).|
|Ethernet|Отображает состояние сети сервера. Открывает раздел **Панель управления\Сеть и Интернет\Сетевые подключения**.|
|Версия операционной системы|В этом доступном только для чтения поле отображается номер версии операционной системы Windows, под управлением которой работает локальный сервер.|
|Сведения об оборудовании|В этом доступном только для чтения поле отображается изготовитель, название и номер модели оборудования сервера.|
|Последние установленные обновления|Отображает день и время последней установки обновлений Windows. Открывает раздел **Панель управления\Система и безопасность\Центр обновления Windows**.|
|Windows Update|Отображает параметры Центра обновления Windows для локального сервера. Открывает раздел **Панель управления\Система и безопасность\Центр обновления Windows**.|
|Последняя проверка наличия обновлений|Отображает дату и время последней проверки наличия доступных обновлений для Windows сервером. Открывает раздел **Панель управления\Система и безопасность\Центр обновления Windows**.|
|Сообщения об ошибках Windows|Отображает состояние участия в программе отправки отчетов об ошибках Windows. Открывает диалоговое окно **Настройка отчетов об ошибках Windows**. Дополнительные сведения об отчетах об ошибках Windows, их преимуществах, заявлениях о конфиденциальности и параметрах участия в программе см. в разделе [Отчеты об ошибках Windows](https://go.microsoft.com/fwlink/?LinkID=245991).|
|Программа улучшения качества программного обеспечения|Отображает состояние участия в программе улучшения качества программного обеспечения Windows. Открывает диалоговое окно **Конфигурация программы улучшения качества программного обеспечения**. Дополнительные сведения о программе улучшения качества программного обеспечения Windows, ее преимуществах и параметрах участия см. в разделе [Программа улучшения качества программного обеспечения Windows](https://go.microsoft.com/fwlink/?LinkID=245992).|
|Конфигурация усиленной безопасности Internet Explorer (IE)|Показывает, включена или отключена конфигурация усиленной безопасности Internet Explorer (также называется усилением защиты IE или IE ESC). Открывает диалоговое окно **Конфигурация усиленной безопасности Internet Explorer**. Конфигурация усиленной безопасности Internet Explorer — это мера безопасности для серверов, которая препятствует открытию веб-страниц в Internet Explorer. Дополнительные сведения о конфигурации усиленной безопасности Internet Explorer, ее преимуществах и параметрах см. в разделе [Конфигурация усиленной безопасности Internet Explorer](https://go.microsoft.com/fwlink/?LinkId=253461).|
|Часовой пояс|Отображает часовой пояс локального сервера. Открывает диалоговое окно **Дата и время** .|
|Product ID|Отображает состояние активации Windows и номер идентификатора продукта (если Windows активирован) операционной системы Windows Server 2016. Этот номер не совпадает с ключом продукта Windows. Открывает диалоговое окно **Активация Windows**.|
|Процессоры|В этом поле только для чтения отображаются сведения о производителе, имени модели и скорости процессоров локального сервера.|
|Установленная память (ОЗУ)|В этом доступном только для чтения поле отображается значение объема доступной оперативной памяти в гигабайтах.|
|Всего на диске|В этом доступном только для чтения поле отображается значение доступного места на диске в гигабайтах.|

## <a name="manage-the-server-manager-console"></a><a name=BKMK_managesm></a>Управление консолью диспетчер сервера
Глобальные параметры, которые применяются ко всей консоли диспетчер сервера и ко всем удаленным серверам, добавленным в пул серверов диспетчер сервера, находятся в заголовках заголовков в верхней части окна консоли диспетчер сервера.

### <a name="add-servers-to-server-manager"></a>Добавление серверов в диспетчер сервера
Команда, открывающая диалоговое окно **Добавление серверов** и позволяющая добавлять удаленные физические или виртуальные серверы в пул серверов Диспетчер сервера, находится в меню **Управление** консоли Диспетчер сервера. Подробные сведения о добавлении серверов см. [в разделе Добавление серверов в Диспетчер сервера](add-servers-to-server-manager.md).

### <a name="refresh-data-that-is-displayed-in-server-manager"></a>Обновление данных, отображающихся в диспетчере серверов
Можно настроить интервал обновления для данных, отображаемых в диспетчер сервера в диалоговом окне **свойства Диспетчер сервера** , которое открывается из меню **Управление** .

##### <a name="to-configure-the-refresh-interval-in-server-manager"></a>Настройка интервала обновления в диспетчере серверов

1.  В меню **Управление** в консоли Диспетчер сервера выберите пункт **Диспетчер сервера свойства**.

2.  В диалоговом окне **свойства Диспетчер сервера** укажите период времени (в минутах), по истечении которого необходимо время между обновлениями данных, отображаемых в Диспетчер сервера. Значение по умолчанию составляет 10 минут. По завершении нажмите кнопку ОК.

#### <a name="refresh-limitations"></a>Ограничения обновления
Обновление применяется глобально к данным со всех серверов, добавленных в пул серверов диспетчер сервера. Невозможно обновить данные или настроить различные интервалы обновления для отдельных серверов, ролей или групп.

Когда серверы, наявляющиеся в кластере, добавляются в диспетчер сервера, являются ли они физическими компьютерами или виртуальными машинами, первое обновление данных может завершиться неудачей или отобразить данные только для сервера узла для кластерных объектов. При последующих обновлениях будут отображаться точные данные для физических или виртуальных серверов в кластере серверов.

Данные, отображаемые на домашней странице ролей в диспетчер сервера для службы удаленных рабочих столов, управления IP-адресами, а службы файлов и хранения не обновляются автоматически. Обновите данные, отображаемые на этих страницах вручную, нажав клавишу **F5** или нажав кнопку **Обновить** в заголовке консоли Диспетчер сервера, на этих страницах.

### <a name="add-or-remove-roles-or-features"></a>Добавление и удаление ролей или компонентов
Команды, открывающие мастер добавления ролей и компонентов и мастера удаления ролей и компонентов и позволяющие добавлять или удалять роли, службы ролей и компоненты для серверов в пуле серверов, находятся в меню **Управление** консоли Диспетчер сервера и меню **задачи** на **страницах роли или** группы. Дополнительные сведения о добавлении и удалении ролей и компонентов см. в разделе [Установка или удаление ролей, служб ролей и компонентов](install-or-uninstall-roles-role-services-or-features.md).

В диспетчер сервера данные ролей и компонентов отображаются на основном языке системы, также называемом языком графического пользовательского интерфейса по умолчанию или на языке, выбранном во время установки операционной системы.

### <a name="create-server-groups"></a>Создание групп серверов
Команда, открывающая диалоговое окно **Создание группы серверов** и позволяющая создавать пользовательские группы серверов, находится в меню **Управление** консоли Диспетчер сервера. Подробные сведения о создании групп серверов см. в разделе [Создание групп серверов и управление ими](create-and-manage-server-groups.md).

### <a name="prevent-server-manager-from-opening-automatically-at-logon"></a>Запрет автоматического открытия диспетчера серверов при входе в систему
Флажок не **начинать Диспетчер сервера автоматически при входе в систему** в диалоговом окне " **Свойства Диспетчер сервера** " определяет, будет ли диспетчер сервера автоматически открываться при входе в систему для членов группы "Администраторы" на локальном сервере. Этот параметр не влияет на диспетчер сервера поведение, если оно выполняется в Windows 10 в составе средства удаленного администрирования сервера. Дополнительные сведения о настройке этого параметра см. в разделе [Диспетчер сервера](server-manager.md).

### <a name="zoom-in-or-out"></a>Увеличение или уменьшение масштаба
Чтобы увеличить или уменьшить масштаб представления консоли диспетчер сервера, можно либо воспользоваться командами **Zoom** в меню **вид** , либо нажать клавиши **CTRL + плюс (+)** , чтобы увеличить масштаб и **CTRL + минус (-)** , чтобы уменьшить масштаб.

## <a name="customize-tools-that-are-displayed-in-the-tools-menu"></a><a name=BKMK_tools></a>Настройка средств, отображаемых в меню "Сервис"
Меню " **Сервис** " в Диспетчер сервера включает ссылки на ярлыки в папке " **Администрирование** " **панели управления, системы и безопасности**. Папка " **Администрирование** " содержит список ярлыков или файлов LNK для доступа к доступным средствам управления, таким как оснастки mmc. Диспетчер сервера заполнит меню " **Сервис** " ссылками на эти ярлыки и скопирует структуру папок папки " **средства администрирования** " в меню " **Сервис** ". По умолчанию средства в папке "Администрирование" организованы в виде неструктурированного списка, отсортированного по типу и имени. В меню "**Сервис** " Диспетчер сервера элементы сортируются только по имени, а не по типу.

Чтобы настроить меню **Сервис**, скопируйте ярлыки средств или сценариев, которые требуется использовать, в папку **Администрирование**. Также ярлыки можно разместить в папках, в результате чего будут созданы вложенные меню в меню **Сервис**. Кроме того, если вы хотите ограничить доступ к пользовательским инструментам в меню **Сервис** , вы можете задать права доступа пользователя как в пользовательских папках инструментов в окне Администрирование, так и непосредственно на исходном средстве или файлах сценариев.

Не рекомендуется перемещать системные и административные средства, а также любые средства управления, связанные с ролями и компонентами, установленными на локальном сервере. Перемещение средств управлениями ролями и компонентами может помешать успешному удалению этих средств управления, когда это будет необходимо. После удаления роли или компонента нерабочая ссылка на средство, ярлык которого был удален, может остаться в меню **Сервис**. Если переустановить роль, в меню **Сервис** создается дублирующаяся ссылка на то же самое средство, но одна из ссылок не будет работать.

Однако средства ролей и компонентов, установленные в составе средств удаленного администрирования сервера на компьютере под управлением клиента Windows, можно разместить в настраиваемых папках. Удаление родительской роли или компонента не влияет на ярлыки средств, которые доступны на удаленном компьютере под Windows 10.

В следующей процедуре описывается создание папки с именем *митулс*и перемещение ярлыков для двух сценариев Windows PowerShell в папку, доступ к которой можно получить из меню Диспетчер сервера сервис.

#### <a name="to-customize-the-tools-menu-by-adding-shortcuts-in-administrative-tools"></a>Настройка меню "Сервис" путем добавления ярлыков в папку "Администрирование"

1.  Создайте новую папку с именем *митулс* в удобном месте.

    > [!NOTE]
    > Из-за ограниченных прав доступа к папке **Администрирование** невозможно создать новую папку непосредственно в папке **Администрирование**; новую папку необходимо создать в другом расположении (например, на рабочем столе), а затем скопировать ее в папку **Администрирование**.

2.  Переместите или скопируйте *митулс* в **Панель управления/система, а также средства безопасности и администрирования**. По умолчанию вы должны быть членом группы "Администраторы" на компьютере, чтобы вносить изменения в папку **Администрирование**.

3.  Если вам не нужно ограничивать права доступа пользователя для ярлыков пользовательских инструментов, перейдите к шагу 6. В противном случае щелкните правой кнопкой мыши файл средства (или папку *MyTools*), затем щелкните **Свойства**.

4.  На вкладке **Безопасность** диалогового окна **свойства** файла нажмите кнопку **изменить**.

5.  для пользователей, для которых требуется ограничить доступ к средствам, снимите флажки для разрешений **чтение & выполнение**, **Чтение**и **запись** . Эти разрешения наследуются ярлыком средства в папке **Администрирование**.

    При изменении прав доступа для пользователя, когда пользователь использует диспетчер сервера (или когда диспетчер сервера открыт), изменения не отображаются в меню " **Сервис** " до тех пор, пока пользователь не перезапускает Диспетчер сервера.

    > [!NOTE]
    > Если ограничить доступ ко всей папке, скопированной в средства администрирования, пользователи с ограниченными правами не смогут видеть ни папку, ни ее содержимое в меню "**Сервис** " Диспетчер сервера.
    > 
    > Измените разрешения для папки в папке " **Администрирование** ". Поскольку скрытые файлы и папки в средствах администрирования всегда отображаются в меню "**Сервис** " Диспетчер сервера, не используйте параметр " **скрытый** " в диалоговом окне **свойств** файла или папки, чтобы ограничить доступ пользователей к ярлыкам пользовательских инструментов.
    > 
    > Разрешения **Отказать** всегда перезаписывают разрешения **Разрешить**.

6.  Щелкните правой кнопкой мыши исходный инструмент, сценарий или исполняемый файл, для которого необходимо добавить записи, в меню **Сервис** выберите команду **создать ярлык**.

7.  Переместите ярлык в папку *митулс* в меню "Администрирование".

8.  При необходимости обновите или перезапустите диспетчер сервера, чтобы просмотреть ярлык настраиваемого инструмента в меню **Сервис** .

## <a name="manage-roles-on-role-home-pages"></a><a name=BKMK_roles></a>Управление ролями на домашних страницах ролей
После добавления серверов в пул серверов диспетчер сервера и диспетчер сервера собирает данные инвентаризации о серверах в пуле, диспетчер сервера добавляет страницы в область навигации для ролей, обнаруженных на управляемых серверах. На плитке **Серверы** на страницах ролей перечисляются управляемые серверы, на которых выполняется данная роль. По умолчанию на плитках **События**, **Анализатор соответствия рекомендациям**, **Службы** и **Производительность** отображаются данные для всех серверов, на которых выполняется роль. При выборе конкретных серверов на плитке **Серверы** отображаются результаты событий, служб, счетчиков производительности и анализатора соответствия рекомендациям только для выбранных серверов. Средства управления, как правило, доступны в меню **средства** консоли Диспетчер сервера, после того как роль или компонент были установлены или обнаружены на управляемом сервере. Также можно щелкнуть правой кнопкой мыши записи сервера на плитке **Серверы** для роли или группы, а затем запустить средство управления, которое требуется использовать.

В Windows Server 2016 следующие роли и компонент имеют средства управления, интегрированные в диспетчер сервера консоль как страницы.

-   **Файловые службы и службы хранилища.** Страницы файловых служб и служб хранилища содержат настраиваемые плитки и команды для управления томами, общими ресурсами, виртуальными дисками iSCSI и пулами носителей. При открытии домашней страницы роли Файловые службы и служб хранилища в диспетчер сервера откроется область отзыва, на которой отображаются пользовательские страницы управления для служб файлов и хранения. Дополнительные сведения о развертывании файловых служб и служб хранилища и управлении ими см. в разделе [Файловые службы и службы хранилища](https://go.microsoft.com/fwlink/p/?LinkId=241530).

-   **Службы удаленных рабочих столов.** Страницы служб удаленных рабочих столов содержат настраиваемые плитки и команды для управления сеансами, лицензиями, шлюзами и виртуальными рабочими столами. Дополнительные сведения о развертывании и управлении службы удаленных рабочих столов см. в разделе [службы удаленных рабочих столов (rdS)](https://go.microsoft.com/fwlink/p/?LinkId=241532).

-   **Управление IP-адресами (IPAM).** Страница роли IPAM содержит настраиваемую плитку **приветствия** со ссылками на общие задачи конфигурации и управления IPAM, включая мастер для подготовки IPAM-сервера. Домашняя страница IPAM также содержит плитки для просмотра управляемой сети, сводки конфигурации и назначенных заданий.

    В диспетчер сервера есть некоторые ограничения на управление IPAM. В отличие от обычных страниц ролей и групп IPAM не имеет плиток **Серверы**, **События**, **Производительность**, **Анализатор соответствия рекомендациям** и **Службы**. Отсутствует модель анализатор соответствия рекомендациям, доступная для IPAM; Анализатор соответствия рекомендациям проверки на IPAM не поддерживаются. Чтобы получить доступ к серверам в пуле серверов, на которых выполняется IPAM, создайте настраиваемую группу серверов, на которых выполняется IPAM, и откройте список серверов на плитке **Серверы** на странице настраиваемой группы. Кроме того, доступ к серверам IPAM можно получить с помощью плитки **Серверы** на странице группы **Все серверы**.

    Также на эскизах панели мониторинга отображаются ограниченные строки для IPAM по сравнению с эскизами для других ролей и групп. Щелкнув строки эскизов IPAM, можно просмотреть события, данные производительности и оповещения о статусе управляемости для серверов, на которых выполняется IPAM. Службами, связанными с IPAM, можно управлять с помощью страниц для групп серверов, содержащих IPAM-серверы, например с помощью страницы для группы **Все серверы**.

    Дополнительные сведения о развертывании IPAM и управлении им см. в разделе [Управление IP-адресами (IPAM)](https://go.microsoft.com/fwlink/p/?LinkId=241533).

## <a name="see-also"></a>См. также
[Диспетчер сервера](server-manager.md)
[добавить серверы в Диспетчер сервера](add-servers-to-server-manager.md)
[создания групп серверов и управления ими](create-and-manage-server-groups.md)
[просмотра и настройки данных о производительности, событиях и службах](view-and-configure-performance-event-and-service-data.md)
[файлах и службах хранилища](https://go.microsoft.com/fwlink/p/?LinkId=241530)
[службы удаленных рабочих столов (rdS)](https://go.microsoft.com/fwlink/p/?LinkId=241532)
[управления IP-адресами (IPAM)](https://go.microsoft.com/fwlink/p/?LinkId=241533)



