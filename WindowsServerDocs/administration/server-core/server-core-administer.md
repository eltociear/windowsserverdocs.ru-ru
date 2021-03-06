---
title: Администрирование Server Core
description: Сведения об администрировании установки основных серверных компонентов Windows Server
ms.prod: windows-server
ms.mktglfcycl: manage
ms.sitesec: library
author: lizap
ms.author: elizapo
ms.localizationpriority: medium
ms.date: 12/18/2018
ms.openlocfilehash: 577014f6fd7e3a3eb58567b1a644d44360f9e498
ms.sourcegitcommit: 51e0b575ef43cd16b2dab2db31c1d416e66eebe8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/17/2020
ms.locfileid: "76259056"
---
# <a name="administer-a-server-core-server"></a>Администрирование сервера Server Core

>Область применения: Windows Server 2019, Windows Server 2016 и Windows Server (половина ежегодного канала)

Поскольку серверное ядро не имеет пользовательского интерфейса, для выполнения основных задач администрирования необходимо использовать командлеты Windows PowerShell, средства командной строки или средства удаленного управления. В следующих разделах описаны командлеты и команды PowerShell, используемые для основных задач. Для администрирования установки можно также использовать [центр администрирования Windows](../../manage/windows-admin-center/overview.md)— единый портал управления, находящиеся в общедоступной предварительной версии. 

## <a name="administrative-tasks-using-powershell-cmdlets"></a>Задачи администрирования с помощью командлетов PowerShell
Используйте следующие сведения для выполнения основных задач администрирования с помощью командлетов Windows PowerShell.

### <a name="set-a-static-ip-address"></a>Настройка статического IP-адреса
При установке сервера Server Core по умолчанию он имеет адрес DHCP. Если вам нужен статический IP-адрес, его можно задать, выполнив следующие действия.

Чтобы просмотреть текущую конфигурацию сети, используйте **Get-нетипконфигуратион**.

Чтобы просмотреть IP-адреса, которые вы уже используете, используйте **Get-нетипаддресс**.

Чтобы задать статический IP-адрес, выполните следующие действия. 

1. Выполните команду **Get-нетипинтерфаце**. 
2. Обратите внимание на число в столбце **ifindex** для IP-интерфейса или строки **интерфацедескриптион** . При наличии нескольких сетевых адаптеров Обратите внимание на число или строку, соответствующие интерфейсу, для которого нужно задать статический IP-адрес.
3. Выполните следующий командлет, чтобы задать статический IP-адрес:

   ```powershell
   New-NetIPaddress -InterfaceIndex 12 -IPAddress 192.0.2.2 -PrefixLength 24 -DefaultGateway 192.0.2.1
   ```

   Где:
   - **InterfaceIndex** — это значение **ifindex** из шага 2. (В нашем примере — 12)
   - **IPAddress** — это статический IP-адрес, который вы хотите задать. (В нашем примере это 191.0.2.2)
   - **PrefixLength** — это длина префикса (другая форма маски подсети) для НАСТРОЕННОГО IP-адреса. (Для нашего примера — 24)
   - **DefaultGateway** — это IP-адрес шлюза по умолчанию. (В нашем примере это 192.0.2.1)
4. Выполните следующий командлет, чтобы задать адрес сервера клиента DNS: 

   ```powershell
   Set-DNSClientServerAddress –InterfaceIndex 12 -ServerAddresses 192.0.2.4
   ```
   
   Где:
   - **InterfaceIndex** — это значение ifindex из шага 2.
   - **Сервераддрессес** — это IP-адрес DNS-сервера.
5. Чтобы добавить несколько DNS-серверов, выполните следующий командлет: 

   ```powershell
   Set-DNSClientServerAddress –InterfaceIndex 12 -ServerAddresses 192.0.2.4,192.0.2.5
   ```

   в этом примере **192.0.2.4** и **192.0.2.5** являются IP-адресами DNS-серверов.

Если необходимо переключиться на использование DHCP, выполните команду **Set-днсклиентсервераддресс – InterfaceIndex 12 – ресетсервераддрессес**.

### <a name="join-a-domain"></a>Присоединение к домену
Используйте следующие командлеты для приподключения компьютера к домену.

1. Запустите **Add-Computer**. Вам будет предложено ввести оба учетных данных для приподключения к домену и доменному имени.
2. Если необходимо добавить учетную запись пользователя домена в группу локальных администраторов, выполните следующую команду в командной строке (не в окне PowerShell):

   ```
   net localgroup administrators /add <DomainName>\<UserName>
   ```
3. Перезагрузите компьютер. Это можно сделать, запустив **Restart-Computer**.

### <a name="rename-the-server"></a>Изменение имени сервера
Чтобы переименовать сервер, выполните следующие действия.

1. Определите текущее имя сервера с помощью команды " **HostName** " или " **ipconfig** ".
2. Выполните команду **Rename-Computer-ComputerName \<new_name\>** .
3. Перезагрузите компьютер.

### <a name="activate-the-server"></a>Активация сервера

Выполните команду **slmgr. vbs – ипк\<productkey\>** . Затем запустите **slmgr. vbs – ATO**. Если активация прошла удачно, сообщение не будет получено.

> [!NOTE]
> Вы также можете активировать сервер по телефону, используя [сервер службы управления ключами (KMS)](../../get-started/server-2016-activation.md)или удаленно. Для удаленной активации выполните следующий командлет с удаленного компьютера: 
> 
> ```
> cscript windows\system32\slmgr.vbs <ServerName> <UserName> <password>:-ato
> ```
 
### <a name="configure-windows-firewall"></a>Настройка брандмауэра Windows

Брандмауэр Windows на компьютере с основными серверными компонентами можно настроить локально, используя командлеты и сценарии Windows PowerShell. Командлеты, которые можно использовать для настройки брандмауэра Windows, см. в разделе [NetSecurity](/powershell/module/netsecurity/?view=win10-ps) .

### <a name="enable-windows-powershell-remoting"></a>разрешение удаленного взаимодействия с Windows PowerShell;

Можно разрешить удаленное взаимодействие с Windows PowerShell, при котором команды Windows PowerShell, введенные на одном компьютере, выполняются на другом компьютере. Включите удаленное взаимодействие Windows PowerShell с помощью **Enable-PSRemoting**.

Дополнительные сведения см. в статье [об удаленном решении вопросов и ответов](/powershell/module/microsoft.powershell.core/about/about_remote_faq?view=powershell-5.1).

## <a name="administrative-tasks-from-the-command-line"></a>Задачи администрирования из командной строки
Используйте следующие справочные сведения для выполнения административных задач из командной строки.

### <a name="configuration-and-installation"></a>Настройка и установка

|                             Задача                              |                                                                                                                                                                                                                 Команда                                                                                                                                                                                                                 |
|---------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|             Установка локального пароля администратора             |                                                                                                                                                                                                      \* **администратора пользователей сети**                                                                                                                                                                                                      |
|                  Присоединение компьютера к домену                  |                                                                                                                                                       **netdom join% ComputerName%** **/Domain:\<домен\>/усерд:\<домен\\имя_пользователя\>/пассвордд:** \* <br> Перезагрузите компьютер.                                                                                                                                                        |
|              Подтверждение изменения домена              |                                                                                                                                                                                                                 **set**                                                                                                                                                                                                                 |
|                Удаление компьютера из домена                |                                                                                                                                                                                                   **Netdom Remove \<ComputerName\>**                                                                                                                                                                                                    |
|         Добавление пользователя в локальную группу администраторов          |                                                                                                                                                                                       **net localgroup Administrators/Add \<домен\\имя_пользователя\>**                                                                                                                                                                                       |
|       Удаление пользователя из локальной группы администраторов       |                                                                                                                                                                                     **net localgroup Administrators/Delete \<домен\\имя_пользователя\>**                                                                                                                                                                                      |
|               Добавление пользователя на локальный компьютер                |                                                                                                                                                                                                **NET User \<домен \ имя_пользователя\> \*/Add**                                                                                                                                                                                                 |
|               Добавление группы на локальный компьютер               |                                                                                                                                                                                                 **имя группы \<net localgroup\>/Add**                                                                                                                                                                                                  |
|          Изменение имени компьютера в домене          |                                                                                                                                                           **netdom ренамекомпутер% имя_компьютера%/newname.:\<новое имя компьютера\>/усерд:\<домен\\имя_пользователя\>/пассвордд:** \*                                                                                                                                                            |
|                 Подтверждение нового имени компьютера                 |                                                                                                                                                                                                                 **set**                                                                                                                                                                                                                 |
|         Изменение имени компьютера в рабочей группе         |                                                                                                                                                                **Netdom ренамекомпутер \<курренткомпутернаме\>/newname.:\<невкомпутернаме\>** <br>Перезагрузите компьютер.                                                                                                                                                                 |
|                Запрет управления файлом подкачки                 |                                                                                                                                                                        **WMIC ComputerSystem, где name = "\<ComputerName\>" Set Аутоматикманажедпажефиле = false**                                                                                                                                                                         |
|                   Конфигурация файла подкачки                   |                                                            **WMIC пажефилесет WHERE Name = "\<путь/имя файла\>" Set Инитиалсизе =\<инитиалсизе\>, MaximumSize =\<MAXSIZE\>** <br>Где *путь/имя* файла — это путь к файлу подкачки и его имя, *инитиалсизе* — это начальный размер файла подкачки в байтах, а параметр *MAXSIZE* — максимальный размер страничного файла в байтах.                                                             |
|                 Изменение статического IP-адреса                 | **ipconfig/all** <br>Запишите соответствующие сведения или перенаправьте их в текстовый файл (**ipconfig/all > ipconfig. txt**).<br>**Интерфейс Netsh интерфейса IPv4 показывать интерфейсы**<br>Убедитесь в наличии списка интерфейсов.<br>**netsh interface IPv4 Set адрес \<имя идентификатор из списка интерфейс\> Source = статический адрес =\<предпочитаемый IP-адрес\> шлюз =\<адрес шлюза\>**<br>Выполните **команду ipconfig/all** , чтобы убедиться, что параметр DHCP включен в значение **нет**. |
|                   Задайте статический DNS-адрес.                   |   <strong>netsh interface IPv4 Add dnsserver Name =\<имя или идентификатор сетевой карты\> адрес =\<IP-адрес основного DNS-сервера\> индекс = 1 <br></strong>netsh interface IPv4 Add dnsserver Name =\<имя дополнительного DNS-сервера\> адрес =\<IP-адрес дополнительного DNS-сервера\> индекс = 2\*\* <br> Повторите эти действия, чтобы добавить дополнительные серверы.<br>Выполните **команду ipconfig/all** , чтобы убедиться в правильности адресов.   |
| Изменение статического IP-адреса на IP-адрес, получаемый по протоколу DHCP |                                                                                                                                      **netsh interface IPv4 Set адрес Name =\<IP-адрес локальной системы\> Source = DHCP** <br>Выполните **команду ipconfig/all** , чтобы убедиться, что для параметра DCHP Enabled задано значение **Да**.                                                                                                                                      |
|                      Ввод ключа продукта                      |                                                                                                                                                                                                   **slmgr. vbs – ИПК \<ключ продукта\>**                                                                                                                                                                                                    |
|                  Локальная активация сервера                  |                                                                                                                                                                                                           **slmgr. vbs-ATO**                                                                                                                                                                                                            |
|                 Удаленная активация сервера                  |                                            **cscript slmgr. vbs – ИПК \<ключ продукта\>\<имя сервера\>\<имя_пользователя\>\<Password\>** <br>**cscript slmgr. vbs-ATO \<ServerName\> \<имя_пользователя\> \<Password\>** <br>Получите идентификатор GUID компьютера, выполнив **cscript slmgr. vbs.** <br> Запустите **cscript slmgr. vbs-dli \<GUID\>** <br>Убедитесь, что для состояния лицензии задано значение **лицензировано (активировано)** .                                             |

### <a name="networking-and-firewall"></a>Сеть и брандмауэр

|Задача|Команда| 
|----|-------|
|Настройка сервера для использования прокси-сервера|**Netsh WinHTTP Set proxy \<ServerName\>:\<номер порта\>** <br>**Примечание.** Установка основных серверных компонентов не может получить доступ к Интернету через прокси-сервер, для которого требуется пароль, чтобы разрешить подключения.|
|Настройка сервера для обхода прокси-сервера для адресов Интернета|**Netsh WinHTTP Set proxy \<ServerName\>:\<номер порта\> обход-List = "\<Local\>"**| 
|Отображение или изменение конфигурации IPSEC|**Netsh IPSec**| 
|Отображение или изменение конфигурации защиты доступа к сети|**Netsh NAP**| 
|Отображение или изменение преобразования IP-адресов в физический адрес|**arp**| 
|Отображение или Настройка локальной таблицы маршрутизации|**route**| 
|Просмотр или Настройка параметров DNS-сервера|**nslookup**| 
|Отображение статистики протокола и текущих TCP/IP-подключений|**netstat**| 
|Отображение статистики протокола и текущих подключений TCP/IP с помощью NetBIOS через TCP/IP (NBT)|**nbtstat**| 
|Отображение прыжков для сетевых подключений|**pathping**| 
|Трассировка прыжков для сетевых подключений|**tracert**| 
|Отображение конфигурации маршрутизатора с поддержкой многоадресной рассылки|**mrinfo**| 
|Включение удаленного администрирования брандмауэра|**netsh advfirewall firewall set Rule Group = "удаленное управление брандмауэром защитника Windows" новое включить = да**| 
 

### <a name="updates-error-reporting-and-feedback"></a>Обновления, отчеты об ошибках и отзывы

|                               Задача                                |                                                                                                                               Команда                                                                                                                                |
|-------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                         Установка обновления                         |                                                                                                                    **WUSA \<обновление\>. msu/quiet**                                                                                                                    |
|                      Вывод списка установленных обновлений                       |                                                                                                                            **systeminfo**                                                                                                                            |
|                         Удаление обновления                          |                                 **Разверните раздел/f:\* \<Update\>. msu c:\test** <br>Перейдите к к:\тест\ и откройте \<обновление\>. XML в текстовом редакторе.<br>Замените **Install** на **Remove** и сохраните файл.<br>**pkgmgr/n:\<Update\>. XML**                                 |
|                    Настройка автоматических обновлений                    |          Чтобы проверить текущее значение параметра: **cscript%systemroot%\SYSTEM32\SCREGEDIT.WSF/ау/v \*\*<br>включить автоматическое обновление: \*\*cscript скрежедит. WSF/ау 4** <br>Отключение автоматического обновления: **cscript%systemroot%\SYSTEM32\SCREGEDIT.WSF/ау 1**          |
|                      Включение отчетов об ошибках                       | Проверка текущего параметра: **сервервероптин/Query** <br>Автоматическая отправка подробных отчетов: **сервервероптин/детаилед** <br>Автоматическая отправка сводных отчетов: **сервервероптин/Summary** <br>Отключение отчетов об ошибках: **сервервероптин/Disable** |
| Участие в Программе улучшения качества программного обеспечения (CEIP) |                                                     Проверка текущего параметра: **серверцеипоптин/Query** <br>Включение программы улучшения качества программного обеспечения: **серверцеипоптин/Enable** <br>Отключение программы улучшения качества программного обеспечения: **серверцеипоптин/Disable**                                                      |

### <a name="services-processes-and-performance"></a>Службы, процессы и производительность

|                               Задача                               |                                                                                                                                                                                                             Команда                                                                                                                                                                                                              |
|------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                    Список выполняющихся служб                     |                                                                                                                                                                                                  **SC Query** или **net start**                                                                                                                                                                                                   |
|                         Запуск службы                          |                                                                                                                                                                                 **SC start \<Service name\>** или **net start \<имя службы\>**                                                                                                                                                                                  |
|                          Остановка службы                          |                                                                                                                                                                                  **SC останавливает \<Service name\>** или **net останавливают \<имя службы\>**                                                                                                                                                                                   |
| Получение списка запущенных приложений и связанных процессов |                                                                                                                                                                                                           **tasklist**                                                                                                                                                                                                           |
|                        Запуск диспетчера задач                        |                                                                                                                                                                                                           **панели Диспетчер задач**                                                                                                                                                                                                            |
|    Создание и управление сеансами трассировки событий и журналами производительности    | Создание счетчика, трассировки, сбора данных конфигурации или API-интерфейса: **Logman цеате** <br>Запрос свойств сборщика данных: **Logman Query** <br>Чтобы запустить или отключить сбор данных, выполните следующие действия: **Logman start\|остановкой** <br>Удаление сборщика: **Logman Delete** <br> Обновление свойств сборщика: **Logman Update** <br>Импорт набора сборщиков данных из XML-файла или его экспорт в XML-файл: **Программа Logman import\|Export** |

### <a name="event-logs"></a>Журналы событий

|Задача|Команда| 
|----|-------|
|Вывод списка журналов событий|**wevtutil El**| 
|Запрос событий в указанном журнале|**wevtutil QE/f: Text \<имя журнала\>**| 
|Экспорт журнала событий|**wevtutil EPL \<имя журнала\>**| 
|Очистка журнала событий|**wevtutil CL \<имя журнала\>**| 


### <a name="disk-and-file-system"></a>Диск и файловая система

|                   Задача                   |                        Команда                        |
|------------------------------------------|-------------------------------------------------------|
|          Управление разделами диска          | Чтобы получить полный список команд, выполните команду **DiskPart/?**  |
|           Управление программным RAID           | Полный список команд запускается с помощью команды **DiskRAID/?**  |
|        Управление точками подключения томов        | Чтобы получить полный список команд, выполните команду **mountvol/?**  |
|           Дефрагментация тома            |  Полный список команд: Run **Defrag/?**   |
| Преобразование тома в файловую систему NTFS |        **преобразовать \<букву тома\>/FS: NTFS**         |
|              Сжатие файла              |  Полный список команд приведен в разделе Выполнение команды **Compact/?**  |
|          Управление открытыми файлами           | Чтобы получить полный список команд, выполните команду **openfiles/?** |
|          Управление папками VSS          | Чтобы получить полный список команд, выполните команду **vssadmin/?**  |
|        Управление файловой системой        |  Чтобы получить полный список команд, выполните команду **fsutil/?**   |
|    Смена владельца файла или папки    |  Чтобы получить полный список команд, выполните команду **icacls/?**   |
 
### <a name="hardware"></a>Оборудование

|Задача|Команда| 
|----|-------|
|Добавление драйвера нового устройства|Скопируйте драйвер в папку в папке% хомедриве%\\\<драйвере\>. Выполните команду **PnPUtil-i-a% хомедриве%\\\<драйвер\>\\\<драйвер\>. INF**|
|Удаление драйвера устройства|Чтобы получить список загруженных драйверов, выполните команду **SC Query Type = драйвер**. Затем выполните команду **SC delete \<service_name\>**|
