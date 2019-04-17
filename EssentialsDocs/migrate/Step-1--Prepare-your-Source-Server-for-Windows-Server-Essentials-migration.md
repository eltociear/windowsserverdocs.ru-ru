---
title: "Шаг 1: Подготовка к миграции исходного сервера для Windows Server Essentials"
description: "Описывается, как использовать Windows Server Essentials"
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 244c8a06-04c6-4863-8b52-974786455373
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 2efb1badde6d0ca11bc3b7526fdfb377d9f95d3f
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/12/2017
---
# <a name="step-1-prepare-your-source-server-for-windows-server-essentials-migration"></a>Шаг 1: Подготовка к миграции исходного сервера для Windows Server Essentials

>Область применения: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

В этом разделе объясняется, как резервное копирование исходного сервера, оценки работоспособности системы исходного сервера, установка последних пакетов обновления и исправления и проверка конфигурации сети.  
  
## <a name="to-prepare-for-migration"></a>Подготовка к миграции  
 Выполните следующие подготовительные действия, чтобы убедиться, что миграцию параметров и данных на исходном сервере успешно на конечный сервер.  
  
1.  [Резервное копирование исходного сервера](Step-1--Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_BackUpYourSourceServerToPrepareForMigration)  
  
2.  [Установите последние пакеты обновления](Step-1--Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_InstallTheMostRecentServicePacksToPrepareForMigration)  
  
3.  [Удаление журнала в качестве параметр учетной записи службы](Step-1--Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_DeleteSvcAcctSetting)  
  
4.  [Оценка работоспособности исходного сервера](Step-1--Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_EvaluateHealth)  
  
5.  [Создание плана для миграции бизнес приложений](Step-1--Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_MigrateLOB)  
  
###  <a name="BKMK_BackUpYourSourceServerToPrepareForMigration"></a>Резервное копирование исходного сервера  
 Создайте резервную копию исходного сервера перед началом процесса миграции. Это поможет защитить данные от случайной утраты, если происходит неустранимая ошибка во время миграции произойдут.  
  
##### <a name="to-back-up-the-source-server"></a>Резервное копирование исходного сервера  
  
1.  Используйте один из ресурсов в следующей таблице в качестве руководства при выполнении полного резервного копирования исходного сервера.  
  
2.  Убедитесь, что резервное копирование выполнено успешно. Чтобы проверить целостность резервной копии, произвольно выберите несколько файлов из резервной копии, восстановите их в альтернативное расположение и затем подтвердите, что восстанавливаемые файлы так же, как исходные файлы.  
  
   |Продукта|Ресурс|
   |---|---|
   |Windows Small Business Server 2003|[Резервное копирование и восстановление Windows Small Business Server 2003](https://msdn.microsoft.com/library/cc875809.aspx) 
   |Windows Small Business Server 2008|[Резервное копирование и восстановление данных на Windows Small Business Server 2008](https://technet.microsoft.com/library/cc527505\(WS.10\).aspx)
   |Windows Server 2008 Foundation|[Резервное копирование и восстановление](https://technet.microsoft.com/library/cc754097\(WS.10\).aspx)  
   |Windows Small Business Server 2011 Essentials|[Дополнительные сведения о настройке архивации сервера](https://technet.microsoft.com/library/server-backup-support-1.aspx)
   |Windows Small Business Server 2011 Standard|[Управление резервным копированием сервера](https://technet.microsoft.com/library/cc527488.aspx)  
   |Windows Server Essentials|[Управление архивацией и восстановлением в Windows Server Essentials](https://technet.microsoft.com/library/jj713536.aspx)

###  <a name="BKMK_InstallTheMostRecentServicePacksToPrepareForMigration"></a>Установите последние пакеты обновления  
 Необходимо установить последние обновления и пакеты обновления на исходный сервер перед миграцией.  
  
###  <a name="BKMK_DeleteSvcAcctSetting"></a>Удаление журнала в качестве параметр учетной записи службы  
 Если вы переходите с Windows Small Business Server 2003 или Windows Server 2003, удалите **вход качестве службы** из групповой политики, параметр учетной записи.  
  
##### <a name="to-delete-the-log-on-as-a-service-account-setting"></a>Удалить журнал в качестве параметр учетной записи службы  
  
1.  Чтобы открыть **Управление групповой политикой** , щелкните **запустить**, нажмите кнопку **панели управления**, нажмите кнопку **Администрирование**и нажмите кнопку **Управление групповой политикой**.  
  
2.  Щелкните правой кнопкой мыши **политика контроллеров домена по умолчанию**, а затем нажмите кнопку **изменить**.  
  
3.  Перейдите к **компьютера Конфигурация компьютера\Параметры Windows\Параметры безопасности\Локальные политики\Назначение прав назначения**.  
  
4.  В области сведений дважды щелкните **вход качестве службы**.  
  
5.  Очистить **определить следующие параметры политики** флажок.  
  
6.  Удалите \\\localhost\SYSVOL\\ < domainname\ > \scripts\SBS_LOGIN_SCRIPT.bat.  
  
###  <a name="BKMK_EvaluateHealth"></a>Оценка работоспособности исходного сервера  
 Важно оценить работоспособность исходного сервера перед началом миграции. Используйте следующие процедуры для проверки текущих, вывода отчета о работоспособности системы, а также для запуска Windows Server решения наиболее анализатора соответствия рекомендациям (BPA) обновлений.  
  
#### <a name="download-and-install-critical-and-security-updates"></a>Загрузка и установка критически важных и безопасности обновления  
 Установка критически важных обновлений и безопасности обновлений на исходном сервере помогает обеспечить успешное выполнение миграции и защитить сеть в процессе миграции.  
  
###### <a name="to-check-for-the-latest-updates"></a>Чтобы проверить наличие обновлений  
  
1.  С исходного сервера, щелкните **запустить**, нажмите кнопку **все программы**, а затем нажмите кнопку **центра обновления Windows**.  
  
2.  Нажмите кнопку **проверить наличие обновлений**.  
  
3.  Если обновления найдены, выберите **установить обновления**.  
  
#### <a name="run-the-best-practices-analyzer"></a>Запустите анализатор соответствия рекомендациям  
 Можно запустить лучший анализатора соответствия рекомендациям (BPA) чтобы убедиться в отсутствии проблем с сервером, сети и домена перед началом процесса миграции. Анализатор соответствия Рекомендациям собирает сведения о конфигурации из следующих источников:  
  
-   Active Directory инструментарий управления Windows (WMI)  
  
-   Реестр  
  
-   Internet Information Services (IIS)  
  
###### <a name="to-use-the-bpa-to-analyze-your-source-server"></a>Анализ исходного сервера с помощью анализатора соответствия Рекомендациям  
  
1.  Следующая таблица содержит ссылки на которого можно загрузить и установить наиболее анализатора соответствия рекомендациям (BPA) для исходного сервера из центра загрузки Майкрософт.  
  
   |Если исходный сервер работает под управлением|Вы можете получить средства анализатора соответствия Рекомендациям|
   |---|---|
   |Windows SBS 2003|[Веб-сайта Microsoft Windows Small Business Server 2003 анализатор соответствия рекомендациям](https://www.microsoft.com/download/details.aspx?id=5334)
   |Windows SBS 2008|[Веб-сайта Microsoft Windows Small Business Server 2008 анализатор соответствия рекомендациям](https://www.microsoft.com/download/details.aspx?id=6231)  
   |Windows SBS 2011 Essentials или Windows SBS 2011 Standard|[Веб-сайте Windows Server Solutions анализатор соответствия рекомендациям](https://www.microsoft.com/download/details.aspx?id=15556) 
   |Windows Server Essentials или Windows Server 2012|Панели мониторинга сервера  
  
2.  После завершения загрузки щелкните **запустить**, наведите курсор на **все программы**, а затем нажмите кнопку **SBS анализатор соответствия рекомендациям**.  
  
    > [!NOTE]
    >  Перед сканированием сервера проверьте наличие обновлений.  
  
3.  В области навигации щелкните **запустить проверку**.  
  
     Если исходный сервер работает под управлением Windows Server Essentials, выполните следующие действия.  
  
    1.  Войдите на конечный сервер от имени администратора и затем открыть панель мониторинга.  
  
    2.  На панели мониторинга щелкните **устройств** вкладку.  
  
    3.  В <**сервера** >**задачи** панели, щелкните **анализатор соответствия рекомендациям**.  
  
4.  В области сведений введите метку сканирования и нажмите кнопку **начала сканирования**. Эта метка содержит имя отчета о сканировании, например, **SBS BPA Scan 1 Jul 2013**.  
  
5.  После завершения сканирования щелкните **просмотреть отчет о сканировании соответствия рекомендациям**.  
  
 После анализатор соответствия Рекомендациям собирает сведения о конфигурации сервера, он проверяет правильность сведений, а также предоставляет администраторам список сведений и проблем, отсортированный по степени серьезности. Список содержит описание каждой проблемы, а также рекомендации или возможные решения. Доступны три типа отчетов.  
  
|Тип отчета|Описание
|-----------------|----------------- 
|Отчеты-списки|Отчеты, представляемые в виде обычного списка. 
|Древовидные отчеты|Отчеты, представляемые в виде иерархического списка.

Чтобы просмотреть ее описание и решения проблемы, щелкните проблему в отчете. Не все проблемы, о которых сообщает анализатор соответствия Рекомендациям, влияют на миграцию, но следует устранить все проблемы, чтобы обеспечить успешную миграцию, по возможности.  
  
####  <a name="BKMK_SynchronizeTheSourceServerTimeWithAnExternalTimeSource"></a>Синхронизация времени исходного сервера с внешним источником времени  
 Время на исходном сервере необходимо присвоить значение в течение пяти минут время на конечном сервере, и Дата и часовой пояс должны быть одинаковы на обоих серверах. Если исходный сервер работает под управлением в виртуальной машине, дата, время и часовой пояс сервера узла должны совпадать с исходного сервера и конечного сервера. Чтобы убедиться в успешной установке Windows Server Essentials, необходимо синхронизировать время исходного сервера к серверу протокола сетевого времени (NTP) в Интернете.  
  
###### <a name="to-synchronize-the-source-server-time-with-the-ntp-server"></a>Синхронизация времени исходного сервера с NTP-сервером  
  
1.  Войдите на исходный сервер с помощью учетной записи администратора домена и пароля.  
  
2.  Нажмите кнопку **запустить**, нажмите кнопку **запуска**, тип **cmd** в текстовом поле и нажмите клавишу ВВОД.  
  
3.  В командной строке введите команду w32tm/config / syncfromflags: DOMHIER / reliable: не/Update, а затем нажмите клавишу ВВОД.  
  
4.  В командной строке введите команду net stop w32time и нажмите клавишу ВВОД.  
  
5.  В командной строке введите команду net start w32time и нажмите клавишу ВВОД.  
  
> [!IMPORTANT]
>  Во время установки Windows Server Essentials у вас есть возможность проверить время на конечном сервере и изменить его при необходимости. Убедитесь, что время, в течение пяти минут времени, которые установлены на исходном сервере. После завершения установки конечный сервер синхронизируется с NTP-Сервером. Синхронизация всех компьютеров, присоединенных к домену, включая исходного сервера на конечный сервер, который предполагается, что роль основного домена эмулятор основного контроллера.  
  
###  <a name="BKMK_MigrateLOB"></a>Создание плана для миграции бизнес приложений  
 Бизнес приложения (LOB) является это компьютерные приложения, жизненно необходимые для функционирования бизнеса. Бизнес-приложения включают учета, цепочке поставок управление и планирование ресурсов приложений.  
  
 При планировании миграции бизнес-приложений необходимо проконсультироваться с поставщиком бизнес-приложения для определения подходящего метода миграции каждого приложения. Также необходимо подготовить носители, которые используются для установки бизнес-приложений на конечном сервере.  
  
> [!NOTE]
>  Если вы использовали пакет Windows Small Business Server 2011 Essentials SDK для разработки настраиваемой надстройки работоспособности системы или оповещения и вы хотите продолжать использовать такую надстройку в с Windows Server Essentials, необходимо также обновить надстройку и развернуть ее на конечном сервере.  
  
  
### <a name="create-a-plan-to-migrate-email-hosted-on-windows-sbs-2011-windows-sbs-2008-and-windows-sbs-2003"></a>Создание плана миграции электронной почты, размещенной на Windows SBS 2011, Windows SBS 2008 и Windows SBS 2003  
 В Windows SBS 2011, Windows SBS 2008 и Windows SBS 2003 электронной почты обеспечивается через Microsoft Exchange Server. Тем не менее Windows Server Essentials не предоставляет службу входящих сообщений электронной почты. Если вы используете сервер под управлением Windows SBS 2011, Windows SBS 2008 или Windows SBS 2003 для размещения электронной почты компании s, вам потребуется Миграция в альтернативное локальное или размещаемое решение.  
  
> [!NOTE]
>  После обновления и подготовки исходного сервера для миграции, рекомендуется создать резервную копию обновленного сервера перед продолжением процесса миграции.  
  
#### <a name="migrate-email-to-microsoft-office-365"></a>Миграция электронной почты в Microsoft Office 365  
 Если вы решили использовать Microsoft Office 365 в качестве решения по электронной почте для домена, следуйте рекомендациям в [Миграция всех почтовых ящиков в облако путем прямой миграции Exchange](http://help.outlook.com/140/ms.exch.ecp.emailmigrationwizardexchangelearnmore.aspx) чтобы начать миграцию электронной почты в Office 365. Мы рекомендуем выполнить миграцию электронной почты до установки Windows Server Essentials.  
  
> [!NOTE]
>  Операция удаления локального сервера Exchange на исходном сервере является обязательной, если вы собираетесь интегрировать Windows Server Essentials с Office 365. Сведения о миграции общих папок сервера Exchange в Office 365, см. в записи блога [Microsoft Exchange 2013 сценарии миграции общих папок для Office 365](http://blogs.technet.com/b/fmustafa/archive/2013/04/11/microsoft-exchange-2013-public-folders-migration-scripts-for-office-365.aspx).  
>   
>  После завершения установки необходимо включить функцию интеграции Office 365 в Windows Server Essentials, запустив **интеграция с Microsoft Office 365** задач.  
  
> [!IMPORTANT]
>  Чтобы разрешить средству миграции Office 365 для подключения к серверу Exchange Server, на котором выполняется на исходном сервере, необходимо включить RPC через HTTP на исходном сервере. Сведения о включении RPC через HTTP см. в разделе [начальное развертывание протокола RPC через HTTP в Small Business Server 2003 (Standard или Premium) впервые](https://technet.microsoft.com/library/bb123622%28EXCHG.65%29.aspx). Если после включения протокола RPC через HTTP не удается успешно запустить средство миграции Office 365, просмотрите **ValidPorts** в реестре по адресу HKEY_LOCAL_MACHINE\Software\Microsoft\Rpc\RpcProxy и убедитесь, что указано полное доменное имя (FQDN) для исходного сервера. Если полное доменное имя не указано, добавьте его вручную с помощью в следующем примере:  
>   
>  удаленный. *Contoso*.com:6001-6002; удаленных. *Contoso*.com: 6004 (Замените *contoso* с именем домена).  
  
#### <a name="migrate-email-to-another-on-premises-exchange-server"></a>Миграцию электронной почты на другой локальный сервер Exchange  
 Сведения о миграции электронной почты на другой локальный сервер Exchange см. в разделе [интеграции локального сервера Exchange с Windows Server Essentials](https://technet.microsoft.com/library/jj200172.aspx). Мы рекомендуем установить новый локальный сервер Exchange Server после установки Windows Server Essentials, а затем завершить миграцию электронной почты до понижения роли исходного сервера.  
  
> [!NOTE]
>  Windows Small Business Server POP3 Connector не включается в Exchange Server. После миграции электронной почты на другой сервер Exchange Server, вы больше не использовать возможности соединителя POP3.  
  
> [!NOTE]
>  После обновления и подготовки исходного сервера к миграции следует создать резервную копию обновленного сервера перед продолжением процесса миграции.  
  
## <a name="next-steps"></a>Дальнейшие действия  
 Исходный сервер подготовлен для миграции Windows Server Essentials.  Теперь перейдите к [шаг 2: Установка Windows Server Essentials как новую реплику контроллера домена](Step-2--Install-Windows-Server-Essentials-as-a-new-replica-domain-controller.md).  

Для просмотра всех шагов см [переход на Windows Server Essentials](Migrate-from-Previous-Versions-to-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md).
