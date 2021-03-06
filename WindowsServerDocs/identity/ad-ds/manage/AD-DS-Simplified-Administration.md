---
ms.assetid: f74eec9a-2485-4ee0-a0d8-cce01250a294
title: Упрощенное администрирование доменных служб Active Directory
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: e1989630cadd7d63f8ed041174135722d568484f
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/08/2020
ms.locfileid: "80824427"
---
# <a name="ad-ds-simplified-administration"></a>Упрощенное администрирование доменных служб Active Directory

>Область применения: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

В этом разделе объясняются возможности и преимущества развертывания и администрирования контроллера домена Windows Server 2012, а также различия между предыдущими развертываниями КОНТРОЛЛЕРов операционной системы и новой реализацией Windows Server 2012.  
  
Windows Server 2012 представил следующее поколение упрощенного администрирования служб домен Active Directory Services, и это было наиболее коренным путем повторного формирования доменов с момента выпуска Windows 2000 Server. Упрощенное администрирование доменных служб Active Directory было разработано с учетом двенадцатилетнего опыта работы с Active Directory. Оно улучшает поддержку административных возможностей для архитекторов и администраторов, делает их более гибкими и интуитивно понятными. Достигнуто это было путем создания новых версий существующих технологий, а также расширения возможностей компонентов, появившихся в Windows Server 2008 R2.  
  
Упрощенное администрирование доменных служб Active Directory — это новый подход к развертыванию доменов.  
  
- Развертывание роли доменных служб Active Directory теперь является частью архитектуры диспетчера сервера и допускает удаленную установку.  
- Модуль развертывания и настройки доменных служб Active Directory теперь основан на Windows PowerShell даже при использовании нового мастера настройки доменных служб Active Directory.  
- Расширение схемы, подготовка леса и домена производятся автоматически в ходе повышения роли контроллера домена и больше не требуют выполнения отдельных задач на специальных серверах, таких как хозяин схемы.  
- При повышении роли теперь проводится проверка предварительных требований, с помощью которой подтверждается готовность леса и домена к установке нового контроллера домена, что снижает вероятность сбоев.  
- Модуль Active Directory для Windows PowerShell теперь включает командлеты для управления топологией репликации, динамического контроля доступа и других операций.  
- В режиме работы леса Windows Server 2012 новые функции не реализуются, а режим работы домена необходим только для подмножества новых функций Kerberos, что упрощает создание однородных сред контроллеров доменов для администраторов.  
- Добавлена полная поддержка виртуализированных контроллеров домена, включая автоматическое развертывание и защиту от отката.  
   - Дополнительные сведения о виртуализированных контроллерах домена см. [в статье Введение в &#40;домен Active Directory&#41; Services &#40;AD DS уровень&#41;виртуализации 100](../../ad-ds/Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md).

Кроме того, реализовано множество улучшений, касающихся администрирования и обслуживания:  

- Центр администрирования Active Directory включает в себя корзину Active Directory с графическим интерфейсом, управление детальной политикой паролей и средство просмотра журнала Windows PowerShell.
- Новый диспетчер сервера имеет специальные интерфейсы для доменных служб Active Directory, позволяющие отслеживать производительность, проводить анализ на основе рекомендаций, определять критические службы и просматривать журналы событий.  
- Групповые управляемые учетные записи служб поддерживают несколько компьютеров, использующих одни и те же субъекты безопасности.  
- Оптимизированы выдача и мониторинг относительных идентификаторов (RID) для более эффективного управления существующими доменами Active Directory.  

AD DS прибыли от других новых функций, входящих в состав Windows Server 2012, например:  

- объединение сетевых карт и мост для центра обработки данных;  
- безопасность DNS и более быстрая доступность зон, интегрированных с Active Directory, после загрузки;  
- улучшенная надежность и масштабируемость Hyper-V;  
- Сетевая разблокировка BitLocker  
- дополнительные модули администрирования компонентов Windows PowerShell.  

## <a name="adprep-integration"></a>Интеграция ADPREP

Расширение схемы леса Active Directory и подготовка домена теперь интегрированы в процесс настройки контроллера домена. При повышении роли нового контроллера домена в существующем лесу процесс определяет состояние обновления и этапы расширения схемы и подготовки домена происходят автоматически. Пользователь, устанавливающий первый контроллер домена Windows Server 2012, по-прежнему должен входить в группы "Администраторы предприятия" и "Администраторы схемы" или предоставить альтернативные действительные учетные данные.  
  
Средство Adprep.exe остается на DVD-диске для подготовки отдельных лесов и доменов. Версия средства, включенная в Windows Server 2012, имеет обратную совместимость с Windows Server 2008 x64 и Windows Server 2008 R2. Adprep.exe также поддерживает удаленные команды forestprep и domainprep, так же как средства настройки контроллера домена на основе ADDSDeployment.  
  
Информацию о средстве Adprep и подготовке леса в предыдущих операционных системах см. в разделе [Работа с программой Adprep.exe (Windows Server 2008 R2)](https://technet.microsoft.com/library/dd464018(WS.10).aspx).  

## <a name="server-manager-ad-ds-integration"></a>Интеграция диспетчера сервера и доменных служб Active Directory

![Упрощенное администрирование](media/AD-DS-Simplified-Administration/ADDS_SMI_TR_Dashboard.png)  
  
Диспетчер сервера выступает в качестве единой консоли для выполнения задач управления сервером. На его информационной панели периодически обновляются представления с установленными ролями и группами удаленных серверов. Диспетчер сервера обеспечивает централизованное управление локальными и удаленными серверами без необходимости доступа к локальной консоли.  
  
Домен Active Directory Services — одна из этих ролей концентратора; запустив диспетчер сервера на контроллере домена или средства удаленного администрирования сервера в Windows 8, вы увидите важные проблемы на контроллерах домена в лесу.  
  
Эти представления включают в себя:  
  
- доступность сервера;  
- монитор производительности с предупреждениями о высокой загрузке процессора и памяти;  
- состояние служб Windows, относящихся к доменным службам Active Directory;  
- последние предупреждения, связанные со службами каталогов, и записи ошибок в журнале событий;  
- анализ выполнения рекомендаций для контроллера домена, проводимый на основе набора правил Майкрософт.  

## <a name="active-directory-administrative-center-recycle-bin"></a>Корзина в центре администрирования Active Directory

![Упрощенное администрирование](media/AD-DS-Simplified-Administration/ADDS_SMI_TR_ADAC.png)  
  
В Windows Server 2008 R2 впервые появилась корзина Active Directory, которая позволяет восстанавливать удаленные объекты Active Directory без восстановления из резервной копии, перезапуска доменных служб Active Directory или перезагрузки контроллеров домена.  
  
В Windows Server 2012 существующие возможности восстановления на основе Windows PowerShell улучшены благодаря новому графическому интерфейсу в центре администрирования Active Directory. Это позволяет администраторам включить корзину и затем найти или восстановить удаленные объекты в контексте доменов леса, и все это без непосредственного использования командлетов Windows PowerShell. Центр администрирования Active Directory и корзина Active Directory по-прежнему используют среду Windows PowerShell, поэтому предыдущие сценарии и процедуры можно с успехом применять.  
  
Информацию о корзине Active Directory см. в [пошаговом руководстве по работе с корзиной Active Directory (Windows Server 2008 R2)](https://technet.microsoft.com/library/dd392261(WS.10).aspx).  
  
## <a name="active-directory-administrative-center-fine-grained-password-policy"></a>Детальная политика паролей в центре администрирования Active Directory

![Упрощенное администрирование](media/AD-DS-Simplified-Administration/ADDS_SMI_TR_FGPP.png)  
  
В Windows Server 2008 появилась детальная политика паролей, которая позволяет администраторам настроить несколько политик паролей и блокировки учетных записей в домене. Это решение позволило гибко управлять более или менее строгими правилами паролей на основе пользователей и групп. У него не было отдельного интерфейса управления, и администраторам приходилось настраивать его с помощью средства Ldp.exe или Adsiedit.msc. В Windows Server 2008 R2 появился модуль Active Directory для Windows PowerShell, который позволил администраторам использовать интерфейс командной строки для управления детальной политикой паролей.  
  
В Windows Server 2012 реализован графический интерфейс для настройки детальной политики паролей. Центр администрирования Active Directory теперь является отправной точкой упрощенного управления детальной политикой паролей для всех администраторов.  
  
Информацию о детальной политике паролей см. в [пошаговом руководстве по детальной настройке политик блокировки учетных записей и паролей доменных служб Active Directory (Windows Server 2008 R2)](https://technet.microsoft.com/library/cc770842(WS.10).aspx).  
  
## <a name="active-directory-administrative-center-windows-powershell-history-viewer"></a>Средство просмотра журнала Windows PowerShell в центре администрирования Active Directory

![Упрощенное администрирование](media/AD-DS-Simplified-Administration/ADDS_SMI_TR_HistoryViewer.png)  
  
В Windows Server 2008 R2 появился центр администрирования Active Directory, который заменил известную администраторам еще со времен Windows 2000 оснастку "Пользователи и компьютеры Active Directory". Центр администрирования Active Directory предоставляет графический интерфейс для модуля Active Directory для Windows PowerShell.  
  
Так как модуль Active Directory содержит более ста командлетов, в них можно легко запутаться. Сейчас среда Windows PowerShell тесно интегрирована в стратегию администрирования ОС Windows, и центр администрирования Active Directory теперь включает в себя средство просмотра, которое позволяет наблюдать за выполнением командлетов в графическом интерфейсе. Вы можете осуществлять поиск и копирование, очищать историю и добавлять заметки в простом интерфейсе. Это позволяет администратору использовать графический интерфейс для создания и изменения объектов, а затем просматривать их с помощью средства просмотра журнала, чтобы узнавать больше о возможностях сценариев PowerShell на примерах.  

## <a name="ad-replication-windows-powershell"></a>Репликация Active Directory средствами Windows PowerShell

![Упрощенное администрирование](media/AD-DS-Simplified-Administration/ADDS_PSNewADReplSite.png)  
  
В Windows Server 2012 добавлены дополнительные командлеты для репликации Active Directory в модуль Active Directory для Windows PowerShell. Они позволяют настраивать новые и существующие сайты, подсети, подключения, связи сайтов и мосты. Они также возвращают метаданные репликации Active Directory, состояние репликации, а также актуальные данные об очередях и векторе синхронизации версий. Командлеты репликации в сочетании с другими командлетами модуля Active Directory позволяют администрировать весь лес, используя только Windows PowerShell. Все это дает новые возможности администраторам, желающим предоставлять ресурсы и управлять системой Windows Server 2012 без использования графического интерфейса, что сокращает уязвимость операционной системы к атакам и требования к обслуживанию. Это приобретает особое значение, если серверы необходимо развернуть в сетях с высоким уровнем защиты, таких как сети SIPR и корпоративные сети периметра.  
  
Подробнее о топологии сайтов и репликации доменных служб Active Directory см. в разделе [Технический справочник по Windows Server](https://technet.microsoft.com/library/cc739127(WS.10).aspx).  

## <a name="rid-management-and-issuance-improvements"></a>Улучшения в области выдачи идентификаторов RID и управления ими

В системе Active Directory в Windows 2000 появился хозяин RID, который выдавал пулы относительных идентификаторов контроллерам домена, чтобы последние могли создавать идентификаторы безопасности (SID) для субъектов безопасности, таких как пользователи, группы и компьютеры.  По умолчанию глобальное пространство RID ограничено общим количеством идентификаторов безопасности (2<sup>30</sup> , или 1 073 741 823), которое можно создать в домене. Идентификаторы безопасности нельзя вернуть в пул или выдать повторно. Со временем в большом домене может возникнуть нехватка идентификаторов RID либо их пул может начать иссякать в результате различных происшествий, ведущих к удалению RID.  
  
В Windows Server 2012 решен ряд проблем, связанных с выдачей идентификаторов RID и управлением ими, которые были выявлены клиентами и службой поддержки клиентов Майкрософт с 1999 года, когда были созданы первые домены Active Directory. К ним можно отнести следующие.  

- В журнал событий периодически записываются предупреждения об использовании идентификаторов RID.  
- Когда администратор делает пул RID недействительным, в журнале создается событие.  
- Ограничение на максимальный размер блока RID теперь устанавливается принудительно в политике RID.  
- Искусственный верхний порог RID теперь применяется принудительно, а если глобальное пространство RID истощается, в журнал заносится запись, что позволяет администратору предпринять меры прежде, чем пространство будет исчерпано.
- Глобальное пространство RID теперь можно увеличить на один бит, благодаря чему его размер увеличивается вдвое — до 2<sup>31</sup> (2 147 483 648 идентификаторов безопасности).  

Подробнее об идентификаторах RID и хозяине RID см. в разделе [Принципы работы идентификаторов безопасности](https://technet.microsoft.com/library/cc778824(WS.10).aspx).  
  
## <a name="ad-ds-role-deployment-and-management-architecture"></a>Архитектура развертывания роли доменных служб Active Directory и управления ею

Функциональные возможности диспетчера сервера и модуля Windows PowerShell ADDSDeployment, связанные с развертыванием роли доменных служб Active Directory и управлением ею, обеспечиваются следующими основными сборками:  

- Microsoft.ADroles.Aspects.dll  
- Microsoft.ADroles.Instrumentation.dll  
- Microsoft.ADRoles.ServerManager.Common.dll  
- Microsoft.ADRoles.UI.Common.dll  
- Microsoft.DirectoryServices.Deployment.Types.dll  
- Microsoft.DirectoryServices.ServerManager.dll  
- Addsdeployment.psm1  
- Addsdeployment.psd1  

Оба компонента используют среду Windows PowerShell и ее механизм удаленного вызова команд для удаленной установки и настройки роли.  

![Упрощенное администрирование](media/AD-DS-Simplified-Administration/ADDS_SMI_TR_DepDLLs.png)  

В Windows Server 2012 также перестроен ряд операций повышения роли, которые ранее обеспечивались программой LSASS.EXE и входили в состав следующих компонентов:  

- служба сервера с ролью доменных служб (DsRoleSvc);  
- библиотека DSRoleSvc.dll (загружаемая службой DsRoleSvc).  

Эта служба должна быть установлена и запущена для повышения и понижения роли, а также клонирования виртуальных контроллеров домена. При установке роли доменных служб Active Directory эта служба добавляется по умолчанию и для нее устанавливается тип запуска "Вручную". Не отключайте эту службу.  

## <a name="adprep-and-prerequisite-checking-architecture"></a>Архитектура ADPrep и проверки предварительных требований

Средство Adprep больше не обязательно запускать на хозяине схемы. Его можно запускать удаленно с компьютера с 64-разрядной версией Windows Server 2008 или более поздней версии.  
  
> [!NOTE]  
> Средство Adprep использует протокол LDAP для импорта файлов Schxx.ldf и не переподключается автоматически, если во время импорта подключение к хозяину схемы прерывается. В процессе импорта хозяин схемы переводится в специальный режим, а переподключение отключается, так как при повторном подключении по протоколу LDAP режим станет иным. В этом случае схема будет обновлена неправильно.  
  
Проверка предварительных требований обеспечивает соблюдение определенных условий. Эти условия необходимы для успешной установки доменных служб Active Directory. Если некоторые обязательные условия не выполняются, вы можете устранить проблемы, а затем продолжить установку. Также проверяется готовность леса или домена к автоматическому выполнению кода развертывания Adprep.  

### <a name="adprep-executables-dlls-ldfs-files"></a>Исполняемые файлы, файлы DLL, LDF и другие файлы ADPrep

- ADprep.dll  
- Ldifde.dll  
- Csvde.dll  
- Sch14.ldf - Sch56.ldf  
- Schupgrade.cat  
- *dcpromo.csv  

Код подготовки Active Directory, который ранее помещался в файле ADprep.exe, прошел рефакторинг и теперь находится в файле adprep.dll. Это позволяет как программе ADPrep.exe, так и модулю Windows PowerShell ADDSDeployment использовать библиотеку для выполнения одних и тех же задач с помощью одинаковых возможностей. Программа Adprep.exe имеется на установочном носителе, но автоматические процессы не обращаются к ней напрямую — администратор должен запустить ее вручную. Она может выполняться в 64-разрядной версии Windows Server 2008 и более поздних операционных системах. Программы ldifde.exe и csvde.exe также имеют DLL-версии, прошедшие рефакторинг, которые загружаются процессом подготовки. Для расширения схемы по-прежнему используются заверенные подписями LDF-файлы, как в предыдущих версиях операционной системы.  
  
![Упрощенное администрирование](media/AD-DS-Simplified-Administration/ADDS_SMI_TR_AdprepDLLs.png)  
  
> [!IMPORTANT]  
> 32-разрядного средства Adprep32.exe для Windows Server 2012 не существует. Для подготовки леса и домена необходим по крайней мере один компьютер с Windows Server 2008 (64-разрядной версии), Windows Server 2008 R2 или Windows Server 2012, работающий как контроллер домена, рядовой сервер или член рабочей группы. Средство Adprep.exe нельзя запустить в 64-разрядной версии Windows Server 2003.  
  
## <a name="prerequisite-checking"></a><a name="BKMK_PrereuisiteChecking"></a>Проверка готовности к установке

Система проверки предварительных требований, встроенная в управляемый код Windows PowerShell ADDSDeployment, работает в различных режимах в зависимости от условий. В приведенных ниже таблицах описывается каждый тест, ситуации, в которых он используется, а также объект и способ проверки. Эти таблицы могут быть полезны в тех случаях, когда пройти проверку не удается, но описания ошибки недостаточно для устранения неполадки.  
  
Результаты этих тестов регистрируются через канал операционного журнала событий **DirectoryServices-Deployment** в категории задач **Основные**и всегда имеют код события **103**.  
  
### <a name="prerequisite-windows-powershell"></a>Проверка предварительных требований с помощью Windows PowerShell

В модуле Windows PowerShell ADDSDeployment есть командлеты для проверки выполнения каждого командлета развертывания контроллера домена. Их аргументы почти полностью совпадают с аргументами проверяемых командлетов.  

- Test-ADDSDomainControllerInstallation  
- Test-ADDSDomainControllerUninstallation  
- Test-ADDSDomainInstallation  
- Test-ADDSForestInstallation  
- Test-ADDSReadOnlyDomainControllerAccountCreation  

Как правило, запускать эти командлеты не требуется, так как они по умолчанию выполняются вместе с командлетами развертывания.  

#### <a name="prerequisite-tests"></a><a name="BKMK_ADDSInstallPrerequisiteTests"></a>Тесты необходимых компонентов

||||  
|-|-|-|  
|Имя теста|Протоколы<p>используется|Описание и примечания|  
|VerifyAdminTrusted<p>ForDelegationProvider|LDAP|Проверяет, есть ли у вас доступ к существующему партнерскому контроллеру домена с правом "Разрешение доверия к учетным записям компьютеров и пользователей при делегировании" (SeEnableDelegationPrivilege). Для этого требуется доступ к построенному атрибуту tokenGroups.<p>Не используется при взаимодействии с контроллерами домена Windows Server 2003. Перед повышением роли необходимо вручную подтвердить это разрешение.|  
|VerifyADPrep<p>Предварительные требования (лес)|LDAP|Обнаруживает хозяина схемы и связывается с ним с помощью атрибута rootDSE namingContexts и атрибута fsmoRoleOwner контекста именования схемы. Определяет, какие операции подготовки (forestprep, domainprep или rodcprep) требуются для установки доменных служб Active Directory. Проверяет правильность атрибута objectVersion схемы и необходимость ее дальнейшего расширения.|  
|VerifyADPrep<p>Предварительные требования (домен и контроллер домена только для чтения)|LDAP|Обнаруживает хозяина инфраструктуры и связывается с ним с помощью атрибута rootDSE namingContexts и атрибута fsmoRoleOwner контейнера инфраструктуры. В случае установки контроллера домена только для чтения этот тест обнаруживает хозяина именования доменов и проверяет, подключен ли он к сети.|  
|CheckGroup<p>Членство|LDAP,<p>RPC через SMB (LSARPC)|Проверяет, является ли пользователь членом группы "Администраторы домена" или "Администраторы предприятия" в зависимости от операции ("Администраторы домена" в случае добавления или понижения роли контроллера домена"; "Администраторы предприятия" в случае добавления или удаления домена).|  
|CheckForestPrep<p>GroupMembership|LDAP,<p>RPC через SMB (LSARPC)|Проверяет, является ли пользователь членом групп "Администраторы схемы" и "Администраторы предприятия" и имеет ли он разрешение "Управление журналами аудита и событий безопасности" (SesScurityPrivilege) для существующих контроллеров домена.|  
|CheckDomainPrep<p>GroupMembership|LDAP,<p>RPC через SMB (LSARPC)|Проверяет, является ли пользователь членом группы "Администраторы домена" и имеет ли он разрешение "Управление журналами аудита и событий безопасности" (SesScurityPrivilege) для существующих контроллеров домена.|  
|CheckRODCPrep<p>GroupMembership|LDAP,<p>RPC через SMB (LSARPC)|Проверяет, является ли пользователь членом группы "Администраторы предприятия" и имеет ли он разрешение "Управление журналами аудита и событий безопасности" (SesScurityPrivilege) для существующих контроллеров домена.|  
|VerifyInitSync<p>AfterReboot|LDAP|Проверяет, был ли хозяин схемы реплицирован хотя бы один раз после перезапуска, путем присвоения фиктивного значения атрибуту rootDSE becomeSchemaMaster.|  
|VerifySFUHotFix<p>Applied|LDAP|Проверяет, нет ли в существующей схеме леса известной проблемы с расширением SFU2 для атрибута UID с идентификатором объекта 1.2.840.113556.1.4.7000.187.102<p>([https://support.microsoft.com/kb/821732](https://support.microsoft.com/kb/821732))|  
|VerifyExchange<p>SchemaFixed|LDAP, WMI, DCOM, RPC|Проверка существующей схемы леса по-прежнему не содержит проблем с расширениями Exchange 2000 MS-дов-Assistant-Name, MS-дов-Лабеледури и MS-дов-House-identifier ([https://support.microsoft.com/kb/314649](https://support.microsoft.com/kb/314649))|  
|VerifyWin2KSchema<p>Consistency|LDAP|Проверяет, имеет ли существующая схема леса согласованные (не измененные неправильно третьей стороной) основные атрибуты и классы.|  
|DCPromo|DRSR через RPC,<p>LDAP,<p>DNS<p>RPC через SMB (SAMR)|Проверяет синтаксис командной строки, передаваемый в код повышения роли и тестового повышения роли. Проверяет, не существует ли уже создаваемый лес или домен.|  
|VerifyOutbound<p>ReplicationEnabled|LDAP, DRSR через SMB, RPC через SMB (LSARPC)|Проверяет, включена ли исходящая репликация в существующем контроллере домена, указанном в качестве партнера репликации. Для этого проверяется атрибут параметров NTDSDSA_OPT_DISABLE_OUTBOUND_REPL (0x00000004) объекта "Параметры NTDS".|  
|VerifyMachineAdmin<p>Пароль|DRSR через RPC,<p>LDAP,<p>DNS<p>RPC через SMB (SAMR)|Проверяет, соответствует ли пароль безопасного режима, установленный для режима восстановления служб каталогов, требованиям к уровню сложности для домена.|  
|VerifySafeModePassword|*Нет данных*|Проверяет, соответствует ли заданный пароль локального администратора требованиям к уровню сложности, предъявляемым политикой безопасности компьютера.|  
