---
ms.assetid: 0abe0976-4b49-45d6-a7b3-81d28bdb8210
title: Рекомендации по политике аудита
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 343a9a7aedf22e9c021249f00fb628f871a2ce1f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2019
ms.locfileid: "59835755"
---
# <a name="audit-policy-recommendations"></a>Рекомендации по политике аудита

>Область применения. Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows 10, Windows 8.1, Windows 7

В этом разделе рассматриваются параметры политики аудита Windows по умолчанию, рекомендуемые базовые параметры политики аудита и интенсивнее рекомендации корпорации Майкрософт, для рабочей станции и серверными продуктами.  

Базовые рекомендации SCM, показанный здесь, а также параметры, которые мы рекомендуем для обнаружения нарушений безопасности, предназначены только для использования в структуру начальную базовых показателей для администраторов. Каждая организация должна принятия решений относительно угрозы, которые могут возникнуть, их отклонения приемлемым риском и какие категории политик аудита или подкатегорий активировать. Сведения об угрозах см [угрозы и меры противодействия](https://technet.microsoft.com/library/hh125921(v=ws.10).aspx). Администраторы без политики аудита продуманный на месте, рекомендуется начать с параметрами, рекомендуемым здесь, а затем изменить и протестировать, до их применения в своей рабочей среде.  

Рекомендации предназначены для компьютеров корпоративного класса, которые корпорация Майкрософт определяет, что компьютеры, которые имеют требования безопасности, среднее и требуют высокого уровня функциональной работоспособности. Политики аудита сущности, которым требуется более высокого уровня защиты, которые требования следует рассмотреть возможность более интенсивное.  

> [!NOTE]  
> Microsoft Windows по умолчанию, а также базовые рекомендации были взяты из [средство Microsoft Security Compliance Manager](https://technet.microsoft.com/library/cc677002.aspx).  

Рекомендуется использовать следующие параметры политики аудита базовых показателей для системы безопасности компьютеров, которые не известны как активных, успешной атаке злоумышленников или вредоносных программ.  

## <a name="recommended-audit-policies-by-operating-system"></a>Рекомендуемые политики аудита операционной системой  
Этот раздел содержит таблицы, в которых перечислены рекомендации относительно параметров аудита, которые применяются для следующих операционных систем:  

-   Windows Server 2016 

-   Windows Server 2012  

-   Windows Server 2012 R2  

-   Windows Server 2008  

-   Windows 10

-   Windows 8.1  

-   Windows 7  

Эти таблицы содержат Windows по умолчанию, Базовые рекомендации и более надежные рекомендации для этих операционных систем.  

**Условные обозначения таблицы политики аудита**  

|||  
|-|-|  
|**Нотация**|**Рекомендация**|  
|ДА|В целом сценариев|  
|НЕТ|Сделать **не** сценариев в целом|  
|IF|Включить при необходимости для конкретного сценария, или если роль или компонент, для которого аудита необходим установленный на компьютере|  
|DC|Включить на контроллерах домена|  
|[Пустые]|Нет рекомендаций|  

**Windows 10, Windows 8 и Windows 7 аудита параметры рекомендации**  

**Политика аудита**  

|Категории политики аудита, или «Подкатегория»|По умолчанию Windows<br /><br />Успех отказ|Базовые рекомендации<br /><br />Успех отказ|Более надежные рекомендации<br /><br />Успех отказ|  
|----------------------------------------|------------------------------------------|--------------------------------------------------|--------------------------------------------------|  
|**Вход в учетную запись**||||  
|Аудит проверки учетных данных|Нет-нет|Да Нет|Да-да|  
|Аудит службы проверки подлинности Kerberos|||Да-да|  
|Аудит операций с билетами службы Kerberos|||Да-да|  
|Аудит других событий входа учетных записей|||Да-да|  
|**Управление учетными записями**||||  
|Аудит управления группами приложений||||  
|Аудит управления учетными записями компьютеров||Да Нет|Да-да|  
|Аудит управления группами распространения||||  
|Аудит других событий управления учетными записями||Да Нет|Да-да|  
|Аудит управления группами безопасности||Да Нет|Да-да|  
|Аудит управления учетными записями пользователей|Да Нет|Да Нет|Да-да|  
|**Подробное отслеживание**||||  
|Аудит активности DPAPI|||Да-да|  
|Аудит создания процессов||Да Нет|Да-да|  
|Аудит завершения процессов||||  
|Аудит событий RPC||||  
|**Доступ к службе Каталогов**||||  
|Аудит подробной репликации службы каталогов||||  
|Аудит доступа к службе каталогов||||  
|Аудит изменения службы каталогов||||  
|Аудит репликации службы каталогов||||  
|**Вход в систему и выхода из системы**||||  
|Аудит блокировки учетных записей|Да Нет||Да Нет|  
|Аудит заявок пользователей или устройств на доступ||||  
|Аудит расширенного режима IPsec||||  
|Аудит основного режима IPsec|||ЕСЛИ IF|  
|Аудит быстрого режима IPsec||||  
|Аудит выхода из системы|Да Нет|Да Нет|Да Нет|  
|Аудит входа в систему <sup>1</sup>|Да-да|Да-да|Да-да|  
|Аудит сервера политики сети|Да-да|||  
|Аудит других событий входа и выхода||||  
|Аудит специального входа|Да Нет|Да Нет|Да-да|  
|**Доступ к объектам**||||  
|Аудит событий, создаваемых приложениями||||  
|Аудит служб сертификации||||  
|Аудит сведений об общем файловом ресурсе||||  
|Аудит общего файлового ресурса||||  
|Аудит файловой системы||||  
|Аудит подключения платформы фильтрации||||  
|Аудит отбрасывания пакетов платформой фильтрации||||  
|Аудит работы с дескрипторами||||  
|Аудит объектов ядра||||  
|Аудит других событий доступа к объектам||||  
|Аудит реестра||||  
|Аудит съемного носителя||||  
|Аудит диспетчера учетных записей безопасности||||  
|Аудит сверки с централизованной политикой доступа||||  
|**Изменение политики**||||  
|Аудит изменения политики аудита|Да Нет|Да-да|Да-да|  
|Аудит изменения политики проверки подлинности|Да Нет|Да Нет|Да-да|  
|Аудит изменения политики авторизации||||  
|Аудит изменения политики платформы фильтрации||||  
|Аудит изменения политики на уровне правил MPSSVC|||Да  |  
|Аудит других событий изменения политики||||  
|**Использование прав**||||  
|Аудит использования привилегий, не затрагивающих конфиденциальные данные||||  
|Аудит других событий использования привилегий||||  
|Аудит использования привилегий, затрагивающих конфиденциальные данные||||  
|**Системы**||||  
|Аудит драйвера IPsec||Да-да|Да-да|  
|Аудит других системных событий|Да-да|||  
|Аудит изменения состояния безопасности|Да Нет|Да-да|Да-да|  
|Аудит расширения системы безопасности||Да-да|Да-да|  
|Аудит целостности системы|Да-да|Да-да|Да-да|  
|**Доступа к глобальным объектам аудита**||||  
|Аудит драйвера IPsec||||  
|Аудит других системных событий||||  
|Аудит изменения состояния безопасности||||  
|Аудит расширения системы безопасности||||  
|Аудит целостности системы||||  

<sup>1</sup> начиная с Windows 10 версии 1809, аудит входа в систему включен по умолчанию Успех и отказ. В предыдущих версиях Windows только успешно включена по умолчанию.

**Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 и рекомендации по настройке Windows Server 2008 аудита**  

|Категории политики аудита, или «Подкатегория»|По умолчанию Windows<br /><br />Успех отказ|Базовые рекомендации<br /><br />Успех отказ|Более надежные рекомендации<br /><br />Успех отказ|  
|----------------------------------------|------------------------------------------|--------------------------------------------------|--------------------------------------------------|  
|**Вход в учетную запись**||||  
|Аудит проверки учетных данных|Нет-нет|Да-да|Да-да|  
|Аудит службы проверки подлинности Kerberos|||Да-да|  
|Аудит операций с билетами службы Kerberos|||Да-да|  
|Аудит других событий входа учетных записей|||Да-да|  
|**Управление учетными записями**||||  
|Аудит управления группами приложений||||  
|Аудит управления учетными записями компьютеров||Да, контроллер домена|Да-да|  
|Аудит управления группами распространения||||  
|Аудит других событий управления учетными записями||Да-да|Да-да|  
|Аудит управления группами безопасности||Да-да|Да-да|  
|Аудит управления учетными записями пользователей|Да Нет|Да-да|Да-да|  
|**Подробное отслеживание**||||  
|Аудит активности DPAPI|||Да-да|  
|Аудит создания процессов||Да Нет|Да-да|  
|Аудит завершения процессов||||  
|Аудит событий RPC||||  
|**Доступ к службе Каталогов**||||  
|Аудит подробной репликации службы каталогов||||  
|Аудит доступа к службе каталогов||КОНТРОЛЛЕР ДОМЕНА С КОНТРОЛЛЕРА ДОМЕНА|КОНТРОЛЛЕР ДОМЕНА С КОНТРОЛЛЕРА ДОМЕНА|  
|Аудит изменения службы каталогов||КОНТРОЛЛЕР ДОМЕНА С КОНТРОЛЛЕРА ДОМЕНА|КОНТРОЛЛЕР ДОМЕНА С КОНТРОЛЛЕРА ДОМЕНА|  
|Аудит репликации службы каталогов||||  
|**Вход в систему и выхода из системы**||||  
|Аудит блокировки учетных записей|Да Нет||Да Нет|  
|Аудит заявок пользователей или устройств на доступ||||  
|Аудит расширенного режима IPsec||||  
|Аудит основного режима IPsec|||ЕСЛИ IF|  
|Аудит быстрого режима IPsec||||  
|Аудит выхода из системы|Да Нет|Да Нет|Да Нет|  
|Аудит входа в систему|Да-да|Да-да|Да-да|  
|Аудит сервера политики сети|Да-да|||  
|Аудит других событий входа и выхода|||Да-да|  
|Аудит специального входа|Да Нет|Да Нет|Да-да|  
|**Доступ к объектам**||||  
|Аудит событий, создаваемых приложениями||||  
|Аудит служб сертификации||||  
|Аудит сведений об общем файловом ресурсе||||  
|Аудит общего файлового ресурса||||  
|Аудит файловой системы||||  
|Аудит подключения платформы фильтрации||||  
|Аудит отбрасывания пакетов платформой фильтрации||||  
|Аудит работы с дескрипторами||||  
|Аудит объектов ядра||||  
|Аудит других событий доступа к объектам||||  
|Аудит реестра||||  
|Аудит съемного носителя||||  
|Аудит диспетчера учетных записей безопасности||||  
|Аудит сверки с централизованной политикой доступа||||  
|**Изменение политики**||||  
|Аудит изменения политики аудита|Да Нет|Да-да|Да-да|  
|Аудит изменения политики проверки подлинности|Да Нет|Да Нет|Да-да|  
|Аудит изменения политики авторизации||||  
|Аудит изменения политики платформы фильтрации||||  
|Аудит изменения политики на уровне правил MPSSVC|||Да  |  
|Аудит других событий изменения политики||||  
|**Использование прав**||||  
|Аудит использования привилегий, не затрагивающих конфиденциальные данные||||  
|Аудит других событий использования привилегий||||  
|Аудит использования привилегий, затрагивающих конфиденциальные данные||||  
|**Системы**||||  
|Аудит драйвера IPsec||Да-да|Да-да|  
|Аудит других системных событий|Да-да|||  
|Аудит изменения состояния безопасности|Да Нет|Да-да|Да-да|  
|Аудит расширения системы безопасности||Да-да|Да-да|  
|Аудит целостности системы|Да-да|Да-да|Да-да|  
|**Доступа к глобальным объектам аудита**||||  
|Аудит драйвера IPsec||||  
|Аудит других системных событий||||  
|Аудит изменения состояния безопасности||||  
|Аудит расширения системы безопасности||||  
|Аудит целостности системы||||  

## <a name="set-audit-policy-on-workstations-and-servers"></a>Настроить политику аудита на рабочих станциях и серверах  
Все планы управления журнала событий, необходимо отслеживать рабочих станций и серверов. Распространенная ошибка — только мониторинг серверов и контроллеров домена. Вредоносные атаки изначально часто выполняется на рабочих станциях и мониторинг рабочих станций не пропускает лучшие и самой ранней источник данных.  

Администраторы должны продуманным Просмотр и тестирование любой политики аудита перед реализацией в своей рабочей среде.  

## <a name="events-to-monitor"></a>События для мониторинга  
Идеальный Событиями для создания оповещения системы безопасности должен содержать следующие атрибуты:  

-   Высока вероятность того, возникновение указывает на несанкционированные действия  

-   небольшое число ложных срабатываний;  

-   Вхождение должно привести к расследование или экспертиза  

Два типа событий необходимо оценить и оповещения:  

1.  Эти события, даже однократное возникновение которых указывает на несанкционированные действия  

2.  Накопление количества событий выше ожидаемых и допустимых базовых показателей.  

Ниже приведен пример первого события.  

Если "Администраторы домена" (DAs) запрещен вход на компьютеры, не являющихся контроллерами домена, при однократном участник DA входа на рабочую станцию для конечных пользователей следует создавать оповещение и изучить. Оповещение этого типа можно легко создать с помощью события аудит специального входа 4964 (специальные группы, назначенные учетную запись для входа). Другие примеры один экземпляр предупреждения.  

-   Если сервер A никогда не следует подключать на сервер B, предупреждение, если они подключаются друг к другу.  

-   Предупреждение, если учетная запись обычного пользователя неожиданно добавляется в группу безопасности конфиденциальные.  

-   Если сотрудники в расположение фабрики A не сможет работать по ночам, оповещения при входе пользователя в полночь.  

-   Предупреждение, если это несанкционированного служба устанавливается на контроллере домена.  

-   Проверьте, пытающийся регулярных пользователей напрямую войти в систему на SQL Server, для которой они имеют не очистить причина для этого.  

-   Если вы не имеют членов в группе DA сами кто-то добавит туда, проверьте его немедленно.  

Ниже приведен пример второго события.  

Нетипичное количество неудачных попыток входа может указывать пароль атаки. Для предприятия для обеспечения оповещение необычно большое число неудачных попыток входа они должны понимать обычный уровни неудачных попыток входа в своей среде до события защиты от вредоносных программ.  

Полный список событий, которые следует включать При мониторинге для обнаружения признаков компрометации, см. в разделе [приложение L: События для мониторинга](../../../ad-ds/plan/Appendix-L--Events-to-Monitor.md).  

## <a name="active-directory-objects-and-attributes-to-monitor"></a>Объекты Active Directory и атрибуты для монитора  
Ниже приведены учетные записи, группы и атрибуты, которые необходимо отслеживать для обнаружения компрометации установки доменных служб Active Directory.  

-   Системы для отключения или удаления антивирусные и антивредоносные программы (автоматически перезапуска защиты, если оно отключено вручную)  

-   Учетные записи администратора для несанкционированных изменений  

-   Действия, которые выполняются с использованием привилегированных учетных записей (автоматически удалить при подозрительных действий будут завершены или выделенное время срока действия учетной записи)  

-   Привилегированных и ВАЖНЫХ учетных записей в Доменных службах Active Directory. Монитор изменений, особенно изменения атрибутов, на вкладке "учетная запись" (например, cn, name, sAMAccountName, userPrincipalName или userAccountControl). Помимо отслеживания учетных записей, ограничить, кто может изменять учетные записи в качестве небольшого набора пользователей с правами администратора максимально.  

Ссылаться на [приложение м: События для мониторинга](../../../ad-ds/plan/Appendix-L--Events-to-Monitor.md) список рекомендуемых события монитора, оценку важности и Сводка событий сообщения.  

-   Группа серверов по классификации рабочих нагрузок, которая позволяет быстро определить серверы, которые должны быть наиболее близко отслеживаемых и наиболее компиляторам настроен  

-   Изменения в свойства и членство в следующие группы AD DS. Enterprise (EA), "Администраторы", "Администраторы домена" (DA), администратора (BA) и "Администраторы схемы" (SA)  

-   Отключенные привилегированных учетных записей (например, встроенные учетные записи администратора в Active Directory и в системах член) для включения учетных записей  

-   Управление учетными записями в журнал все операции записи к учетной записи  

-   Встроенный мастер настройки безопасности для настройки службы, реестра, аудита и параметры брандмауэра, чтобы уменьшить уязвимость сервера. Этот мастер используется в том случае, если вы реализуете серверы перехода как часть стратегии администратора узла.  

## <a name="additional-information-for-monitoring-active-directory-domain-services"></a>Дополнительные сведения о мониторинге доменных служб Active Directory  
Просмотрите следующие ссылки на дополнительные сведения о мониторинге AD DS:  
  
-   [Аудит доступа к глобальным объектам является Magic](http://blogs.technet.com/b/askds/archive/2011/03/10/global-object-access-auditing-is-magic.aspx) -предоставляет сведения о настройке и использовании конфигурация расширенной политики аудита, добавленный в Windows 7 и Windows Server 2008 R2.  

-   [Знакомство с аудит изменений в Windows 2008](http://blogs.technet.com/b/askds/archive/2007/10/19/introducing-auditing-changes-in-windows-2008.aspx) -вводит аудита изменений, внесенных в Windows 2008.  

-   ["Холодный" Аудит рекомендации в Vista и 2008](http://blogs.technet.com/b/askds/archive/2007/11/16/cool-auditing-tricks-in-vista-and-2008.aspx) -объясняет интересных функций аудита в Windows Vista и Windows Server 2008, который может использоваться для устранения неполадок или видеть, что происходит в вашей среде.  

-   [Единое средство для аудита в Windows Server 2008 и Windows Vista](http://blogs.technet.com/b/askds/archive/2008/03/27/one-stop-shop-for-auditing-in-windows-server-2008-and-windows-vista.aspx) -содержит компиляции аудита функции и сведения, содержащиеся в Windows Server 2008 и Windows Vista.  

-   [AD DS аудит Пошаговое руководство по использованию](https://technet.microsoft.com/library/a9c25483-89e2-4202-881c-ea8e02b4b2a5.aspx) -описывается новая функция аудита доменных служб Active Directory (AD DS) в Windows Server 2008. Он также предоставляет процедуры, реализуемые этой новой функции.  

## <a name="general-list-of-security-event-id-recommendation-criticalities"></a>Общие списка степеней рекомендация идентификатор события безопасности  
Все рекомендации ИД события могут быть загружены по важности, оценка следующим образом:  

**Высокий уровень:** Идентификаторы событий с оценкой высокой важности следует всегда и сразу же быть оповещения и изучить.  

**Средний:** Идентификатор события с оценкой средний уровень важности может указывать на вредоносное действие, но он должен сопровождаться некоторые другие неисправность (например, необычно в определенный период времени, Непредвиденная вхождений или экземпляров на компьютере, обычно не ожидается событий в.). Средний-уровень важности событий может также r, собираемых в качестве метрики и по сравнению с течением времени.  

**"Низкий".** И идентификатор события с помощью событий низкой важности не привлекают внимания или вызывают оповещения, в том случае, если связаны с событиями, средним или высоким уровнем важности.  

Эти рекомендации предназначены для предоставления базовых показателей руководства для администратора. Все рекомендации, необходимо тщательно проверить перед реализацией в рабочей среде.  

Ссылаться на [приложение м: События для мониторинга](../../../ad-ds/plan/Appendix-L--Events-to-Monitor.md) список рекомендуемых события монитора, оценку важности и сводка сообщений событий.  