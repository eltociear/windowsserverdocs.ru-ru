---
title: Обзор панели мониторинга в Windows Server Essentials
description: Описание использования Windows Server Essentials
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: f70a79de-9c56-4496-89b5-20a1bff2293e
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: ad59d4c23efdb0094d0cac780815f3f3238db3da
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/08/2020
ms.locfileid: "80852677"
---
# <a name="overview-of-the-dashboard-in-windows-server-essentials"></a>Обзор панели мониторинга в Windows Server Essentials

>Область применения: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials
 
 Windows Server Essentials и Windows Server 2012 R2 Standard с включенной ролью "режим Windows Server Essentials" предоставляют панель администрирования, которая упрощает задачи по управлению сетью и сервером Windows Server Essentials. C помощью панели мониторинга Windows Server Essentials можно решать следующие задачи.  
  
- Завершение настройки сервера  
  
- Выполнение стандартных задач администрирования и доступ к ним  
  
- Просмотр предупреждений сервера и принятие соответствующих мер  
  
- Настройка и изменение параметров сервера  
  
- Поиск разделов справки в Интернете и доступ к ним  
  
- Доступ к ресурсам сообщества в Интернете  
  
- Управление учетными записями пользователей  
  
- Управление устройствами и резервным копированием  
  
- Управление доступом и параметрами для серверных папок и жестких дисков  
  
- Просмотр приложений-надстроек и управление ими  
  
- Интеграция с веб-службами Microsoft  
  
  Этот раздел включает:  
  
- [Основные возможности панели мониторинга](#BKMK_Design)  
  
- [Возможности домашней страницы панели мониторинга](#BKMK_Home)  
  
- [Разделы администрирования панели мониторинга](#BKMK_Features)  
  
- [Доступ к панели мониторинга Windows Server Essentials](#BKMK_AccessDb)  
  
- [Использование безопасного режима](#BKMK_UseSafeMode)  
  
##  <a name="basic-features-of-the-dashboard"></a><a name="BKMK_Design"></a>Основные возможности панели мониторинга  
 Панель мониторинга Windows Server Essentials помогает быстро осуществлять доступ к ключевым сведениям и функциям управления на сервере. Панель мониторинга содержит несколько разделов. В следующей таблице перечислены разделы.  
  
 
  
|Элемент|Функция на панели мониторинга|Описание|  
|----------|-----------------------|-----------------|  
|1|Панель навигации|Щелкните раздел на панели навигации, чтобы получить доступ к сведениям и задачам, связанным с этим разделом. Всякий раз при открытии панели мониторинга по умолчанию отображается страница **Главная**.|  
|2|Вкладки подразделов|Вкладки подразделов позволяют осуществлять доступ к административным задачам Windows Server Essentials второго уровня.|  
|3|Область списков|В представлении списка отображаются управляемые объекты и общие сведения о каждом из них.|  
|4|панель «Подробности»|В области сведений отображается дополнительная информация об объекте, выбранном в представлении списка.|  
|5|Область "Задачи"|Область задач содержит ссылки на инструменты и сведения, облегчающие управление свойствами конкретного объекта (например, учетной записи пользователя или компьютера) или глобальными параметрами категории объекта. Область "Задачи" разделена на следующие два раздела.<br /><br /> **Задачи объекта** : содержат ссылки на средства и сведения, помогающие управлять свойствами объекта, выбранного в представлении списка (например, учетной записи пользователя или компьютера).<br /><br /> **Глобальные задачи** : содержат ссылки на средства и сведения, помогающие управлять глобальными задачами для функциональной области. К глобальным задачам относятся следующие: добавление новых объектов, настройка политики и т. д.|  
|6|Сведения и параметры|Из этого раздела осуществляется прямой доступ к параметрам сервера, здесь же можно найти ссылку на разделы справки, содержащие сведения о просматриваемой странице панели мониторинга.|  
|7|Статус предупреждений|Статус предупреждений позволяет быстро получить визуальное представление о состоянии сервера. Щелкните изображение предупреждения для просмотра критических и важных предупреждений.<br /><br /> **Примечание.** В Windows Server Essentials и Windows Server 2012 R2 Standard с установленной ролью Windows Server Essentials Experience состояние оповещения доступно на вкладке **сведения и параметры** .|  
|8|Строка состояния|В строке состояния отображается число объектов в представлении списка. В приложениях-надстройках также может отображаться другой статус.|  
  
##  <a name="features-of-the-dashboard-home-page"></a><a name="BKMK_Home"></a>Возможности домашней страницы панели мониторинга  
 При открытии панели мониторинга по умолчанию отображается страница **Главная** с категорией **НАСТРОЙКА**. Страница **Главная** панели мониторинга Windows Server Essentials обеспечивает быстрый доступ к задачам и сведениям, упрощающим пользовательскую настройку сервера и конфигурацию основных функций. Страница "Главная" состоит из четырех функциональных областей, где отображаются сведения и задачи конфигурации по выбранным параметрам. В следующей таблице перечислены функции.  
  
|Элемент|Функция|Описание|  
|----------|-------------|-----------------|  
|1|Панель навигации|Щелкните раздел на панели навигации, чтобы получить доступ к сведениям и задачам, связанным с этим разделом. Всякий раз при открытии панели мониторинга по умолчанию отображается страница **Главная**.|  
|2|Область "Категория"|В этой области отображаются основные функциональные области, обеспечивающие быстрый доступ к сведениям и средствам конфигурации для настройки (включая пользовательскую настройку) сервера. Щелкните категорию, чтобы отобразить задачи и ресурсы, связанные с этой категорией.|  
|3|Область "Задачи"|В этой области отображаются ссылки на задачи и сведения, применяемые к выбранной категории. Щелкните задачу или ресурс, чтобы отобразить дополнительные сведения.|  
|4|Область действий|Эта область содержит краткое описание функции или задачи, а также ссылки для открытия мастеров конфигурации и страниц со сведениями. Щелкните ссылку, чтобы предпринять дальнейшие действия|  
  
##  <a name="administrative-sections-of-the-dashboard"></a><a name="BKMK_Features"></a>Разделы администрирования панели мониторинга  
 На панели мониторинга Windows Server Essentials сетевая информация и административные задачи упорядочены по функциональным областям. Страница управления каждой функциональной области содержит сведения об объектах, связанных с этой областью, например **Пользователи** или **Устройства**. На странице управления также отображаются задачи, с помощью которых можно просматривать или изменять параметры, а также запускать программы, автоматизирующие выполнение многошаговых задач.  
  
 В следующей таблице описаны административные разделы панели мониторинга, которые после установки доступны по умолчанию. В этой таблице также перечислены задачи, доступные в каждом разделе.  
  
|Раздел|Описание|  
|-------------|-----------------|  
|Главная|Страница **Главная** отображается по умолчанию всякий раз при открытии панели мониторинга. Здесь отображаются задачи и сведения для следующих категорий.<br /><br /> **Программа установки** : выполнить задачи в этой категории, чтобы настроить сервер в первый раз. Дополнительные сведения об этих задачах см. в разделе [Установка и настройка Windows Server Essentials](../install/Install-and-Configure-Windows-Server-Essentials.md).<br /><br /> **Электронная почта** : выберите параметр в этой категории для интеграции службы электронной почты с сервером.<br /><br /> **Примечание.** Эта категория доступна только в Windows Server Essentials.<br /><br /> **Службы** : выберите задачу в этой категории, чтобы интегрировать Microsoft веб-службы с сервером.<br /><br /> **Примечание.** Эта категория доступна только в Windows Server Essentials и Windows Server 2012 R2 Standard с включенной ролью Windows Server Essentials Experience.<br /><br /> **Надстройки** : щелкните эту категорию, чтобы установить ценные надстройки для вашего бизнеса.<br /><br /> В **кратком состоянии** : отображается состояние сервера высокого уровня. Щелкните статус, чтобы просмотреть сведения об этой функции и возможности ее конфигурации. Если выполнены все задачи в категории "НАСТРОЙКА", эта категория отображается вверху области "Категория".<br /><br /> **Справка** :. Используйте поле поиска для поиска справки в Интернете. Щелкните ссылку, чтобы посетить веб-сайт выбранного варианта поддержки.|  
|Users|Для того чтобы пользователи могли осуществлять доступ к предоставляемым Windows Server Essentials ресурсам, необходимо создать учетные записи пользователей, воспользовавшись панелью мониторинга Windows Server Essentials. После создания учетных записей пользователя можно осуществлять управление учетными записями с помощью доступных на странице **Пользователи** панели мониторинга задач. На этой странице доступны следующие задачи.<br /><br /> — Просмотр списка учетных записей пользователей.<br /><br /> — Просмотр свойств учетной записи пользователя и управление ими.<br /><br /> — Активация или деактивация учетных записей пользователей.<br /><br /> — Добавление или удаление учетных записей пользователей.<br /><br /> — Назначьте учетные записи локальной сети учетным записям Майкрософт веб-службы, если сервер интегрирован с Office 365.<br /><br /> — Изменение паролей учетных записей пользователей и управление политикой паролей.<br /><br /> Сведения об управлении учетными записями пользователей см. в разделе [Управление учетными записями пользователей](Manage-User-Accounts-in-Windows-Server-Essentials.md).|  
|Группы пользователей|**Примечание.** Эта функция доступна только в Windows Server Essentials и Windows Server 2012 R2 Standard с включенной ролью Windows Server Essentials Experience.<br /><br /> На этой странице доступны следующие задачи.<br /><br /> — Просмотр списка групп пользователей.<br /><br /> — Просмотр групп пользователей и управление ими.<br /><br /> — Добавление или удаление групп пользователей.|  
|группы распространения.|**Примечание.** Эта функция доступна только в Windows Server Essentials и Windows Server 2012 R2 Standard с включенной ролью Windows Server Essentials Experience. Эта вкладка отображается только при условии интеграции Windows Server Essentials с Office 365.<br /><br /> На этой странице доступны следующие задачи.<br /><br /> — Просмотр списка групп рассылки.<br /><br /> — Добавление или удаление групп рассылки.|  
|Устройства|После подключения компьютеров к сети Windows Server Essentials управлять компьютерами можно со страницы **Устройства** панели мониторинга. На этой странице доступны следующие задачи.<br /><br /> — Просмотр списка компьютеров, присоединенных к сети.<br /><br /> — Управление мобильными устройствами с помощью возможности управления мобильными устройствами Office 365.<br /><br /> **Примечание.** Эта функция доступна только в Windows Server Essentials и Windows Server 2012 R2 Standard с включенной ролью Windows Server Essentials Experience.<br /><br /> — Просмотр свойств компьютера и оповещений о работоспособности для каждого компьютера.<br /><br /> Настройка и управление резервными копиями компьютеров.<br /><br /> — Восстановление файлов и папок на компьютерах.<br /><br /> — Установка удаленный рабочий стол подключения к компьютеру<br /><br /> -Настройка параметров резервного копирования и журнала файлов компьютера<br /><br /> Сведения об управлении компьютерами и резервными копиями см. в разделе [Manage Devices](Manage-Devices-in-Windows-Server-Essentials.md).|  
|Хранилище|В зависимости от используемой версии Windows Server Essentials раздел **Хранение** панели мониторинга по умолчанию содержит следующие разделы.<br /><br /> — Подраздел **Server Folders** содержит задачи, помогающие просматривать свойства папок сервера и управлять ими. На этой странице также доступны задачи по открытию и добавлению серверных папок.<br /><br /> — Страница **Жесткие диски** содержит задачи, помогающие просматривать и проверять работоспособность дисков, подключенных к серверу.<br /><br /> — В Windows Server Essentials и Windows Server 2012 R2 Standard с включенной ролью Windows Server Essentials на странице **библиотеки SharePoint** содержатся задачи, помогающие управлять библиотеками SharePoint в службе Office 365.<br /><br /> Сведения об управлении папками сервера см. в разделе [Manage Server Folders](Manage-Server-Folders-in-Windows-Server-Essentials.md).<br /><br /> Сведения об управлении жесткими дисками см. в разделе [Управление хранилищем сервера](Manage-Server-Storage-in-Windows-Server-Essentials.md).|  
|Приложения|— Раздел **приложений** на панели мониторинга Windows Server Essentials содержит два подраздела по умолчанию.<br /><br /> Сведения об управлении приложениями надстроек см. в разделе [Manage Applications](Manage-Applications-in-Windows-Server-Essentials.md).<br /><br /> — В подразделе **надстройки** отображается список установленных надстроек и приводятся задачи, позволяющие удалить надстройку и получить доступ к дополнительным сведениям о выбранной надстройке.<br /><br /> — Подраздел **Microsoft Pinpoint** содержит список приложений, доступных в Microsoft Pinpoint.|  
|Office 365|Вкладка **Office 365** отображается, только если Windows Server Essentials интегрирован с Microsoft Office 365. В этом разделе содержится информация о подписке Office 365 и учетной записи администратора.|  
  
> [!NOTE]
>  Если устанавливается надстройка для панели мониторинга Windows Server Essentials, могут быть созданы дополнительные административные разделы. Эти разделы могут отображаться в главной строке навигации или на вкладке подразделов.  
  
##  <a name="access-the-windows-server-essentials-dashboard"></a><a name="BKMK_AccessDb"></a>Доступ к панели мониторинга Windows Server Essentials  
 Доступ к панели мониторинга осуществляется одним из следующих методов. Выбор метода зависит от того, осуществляется ли доступ с сервера, компьютера, подключенного к сети Windows Server Essentials, или удаленного компьютера.  
  
 В целях сохранения безопасности сети только пользователи с разрешениями администратора могут осуществлять доступ к панели мониторинга Windows Server Essentials. Кроме того, невозможно использовать встроенную учетную запись администратора для входа на панель мониторинга Windows Server Essentials с панели запуска.  
  
###  <a name="access-the-dashboard-from-the-server"></a><a name="BKMK_Server"></a>Доступ к панели мониторинга с сервера  
 При установке Windows Server Essentials в ходе процедуры настройки создается ярлык на панель мониторинга на экране **Пуск** и на рабочем столе. Если в указанных расположениях отсутствует ярлык, можно воспользоваться областью **Поиск** для поиска и запуска программы "Панель мониторинга".  
  
##### <a name="to-access-the-dashboard-from-the-server"></a>Доступ к панели мониторинга с сервера  
  
-   Выполните вход на сервер с правами администратора, а затем выполните любое из следующих действий.  
  
    -   На экране **Пуск** щелкните **Панель мониторинга**.  
  
    -   На рабочем столе дважды щелкните **Панель мониторинга**.  
  
    -   В поле **Поиск** введите **dashboard**, а затем щелкните **Панель мониторинга** в результатах поиска.  
  
###  <a name="access-the-dashboard-from-a-computer-that-is-connected-to-the-network"></a><a name="BKMK_Network"></a>Доступ к панели мониторинга с компьютера, подключенного к сети  
 После подключения компьютера к сети администраторы в Windows Server Essentials могут осуществлять доступ к панели мониторинга сервера с этого компьютера, используя панель запуска.  
  
> [!WARNING]
>  Чтобы подключиться к панели мониторинга с клиентского компьютера в Windows Server Essentials, щелкните правой кнопкой мыши значок области, а затем откройте панель мониторинга из контекстного меню.  
  
##### <a name="to-access-the-dashboard-by-using-the-launchpad"></a>Доступ к панели мониторинга с помощью панели запуска  
  
1.  На подключенном к сети компьютере откройте **Панель запуска**.  
  
2.  В меню панели запуска щелкните **Панель мониторинга**.  
  
3.  На странице **Вход** панели мониторинга введите учетные данные сетевого администратора, а затем нажмите клавишу ВВОД.  
  
     Откроется удаленное подключение к панели мониторинга Windows Server Essentials.  
  
###  <a name="access-the-dashboard-from-a-remote-computer"></a><a name="BKMK_Remote"></a>Доступ к панели мониторинга с удаленного компьютера  
 При работе с удаленного компьютера вы можете получить доступ к панели мониторинга Windows Server Essentials с помощью удаленного Веб-доступ сайта.  
  
##### <a name="to-access-the-dashboard-by-using-remote-web-access"></a>Доступ к панели мониторинга с использованием удаленного веб-доступа  
  
1.  На удаленном компьютере откройте веб-браузер, например Internet Explorer.  
  
2.  В адресной строке Интернет-браузера введите следующее:**https://< имя_домена\>/ремоте**, где *имя_домена* — это внешнее доменное имя организации (например, contoso.com).  
  
3.  Введите имя пользователя и пароль для входа на удаленный Веб-доступ сайт.  
  
4.  В разделе " **Компьютеры** "**домашней** страницы удаленного веб-доступ; Выберите сервер и нажмите кнопку **подключить**.  
  
     Откроется удаленное подключение к панели мониторинга.  
  
    > [!NOTE]
    >  Если сервер не отображается в разделе **Компьютеры** на странице "Главная", щелкните **Подключиться к другим компьютерам**, найдите сервер в списке и щелкните его, чтобы установить подключение.  
    >   
    >  Чтобы предоставить пользователю разрешение на доступ к панели мониторинга с удаленного Веб-доступ, откройте страницу свойств учетной записи пользователя, а затем выберите параметр **панель мониторинга сервера** на вкладке **доступ с любого места** .  
  
##  <a name="use-the-safe-mode"></a><a name="BKMK_UseSafeMode"></a>Использование безопасного режима  
 Функция безопасного режима в Windows Server Essentials осуществляет мониторинг надстроек, установленных на сервере. Если панель мониторинга становится нестабильной или не отвечает, безопасный режим обнаруживает и изолирует надстройки, которые, возможно, являются причиной проблемы, и отображает их на странице **Параметры безопасного режима** при следующем открытии панели мониторинга. На странице **Параметры безопасного режима** можно по одной отключать и включать надстройки, чтобы определить, какая из них является причиной проблемы. Затем можно оставить надстройку отключенной для дальнейших запусков или удалить ее.  
  
 Можно просмотреть список всех надстроек, установленных на сервере в то или иное время. Вы также можете открыть панель мониторинга в защищенном режиме, которая автоматически отключает все надстройки сторонних разработчиков. Windows Server Essentials также позволяет получить доступ к панели мониторинга в защищенном режиме с другого компьютера в сети.  
  
#### <a name="to-view-a-list-of-installed-add-ins"></a>Просмотр списка установленных надстроек  
  
-   На панели мониторинга щелкните **Справка**, а затем щелкните **Параметры безопасного режима**.  
  
#### <a name="to-open-the-dashboard-in-safe-mode"></a>Открытие панели мониторинга в безопасном режиме  
  
-   В области **Поиск** введите **safe**, а затем в результатах поиска щелкните **Панель мониторинга (безопасный режим)** .  
  
#### <a name="to-open-the-dashboard-in-safe-mode-from-another-computer-on-the-network"></a>Открытие панели мониторинга в безопасном режиме с другого компьютера сети  
  
1.  На компьютере, подключенном к сети, откройте панель запуска Windows Server Essentials и щелкните **Панель мониторинга**.  
  
2.  На странице входа на панель мониторинга введите имя пользователя и пароль учетной записи, обладающей разрешением на вход на сервер, установите флажок **Разрешить мне выбрать надстройки для загрузки** и щелкните стрелку, чтобы войти.  
  
## <a name="see-also"></a>См. также:  
  
-   [Управление приложениями](Manage-Applications-in-Windows-Server-Essentials.md)  
  
-   [Управление Windows Server Essentials](Manage-Windows-Server-Essentials.md)
