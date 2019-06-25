---
title: Устранение неполадок инвентаризации программного обеспечения
description: Сведения об устранении распространенных проблем развертывания для ведения журнала инвентаризации программного обеспечения.
ms.custom: na
ms.prod: windows-server-threshold
ms.technology: manage-software-inventory-logging
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
author: brentfor
ms.author: coreyp
manager: lizapo
ms.date: 10/16/2017
ms.openlocfilehash: 8a1fe22a1f721c0ac94096fe22c559c9bb092293
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/31/2019
ms.locfileid: "66435313"
---
# <a name="troubleshoot-software-inventory-logging"></a>Устранение неполадок инвентаризации программного обеспечения 

>Область применения. Windows Server (полугодовой канал), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

## <a name="understanding-sil"></a>Основные сведения о инвентаризации программного обеспечения

Прежде чем приступить к устранению неполадок инвентаризации программного обеспечения, необходимо хорошо понимать ее компоненты и как это работает. Следующие видео предоставляют обзор инвентаризации программного обеспечения и средство инвентаризации программного обеспечения и способы их использования для пересылки и данные инвентаризации отчета:

1. [Введение в инвентаризации программного обеспечения (SIL) (10:57)](https://channel9.msdn.com/Blogs/Regular-IT-Guy/An-Introduction-to-Software-Inventory-Logging-SIL)

2. [Программное обеспечение ведения журнала инвентаризации: Настройка инвентаризации программного обеспечения (14:34)](https://channel9.msdn.com/Blogs/windowsserver/Software-Inventory-Logging-Setting-up-SIL-Aggregator)

3. [Программное обеспечение ведения журнала инвентаризации: Включение переадресации инвентаризации программного обеспечения (7:20)](https://channel9.msdn.com/Blogs/windowsserver/Software-Inventory-Logging-Enabling-SIL-Forwarding)

## <a name="how-sil-data-flow-works"></a>Как передавать works в данные инвентаризации программного обеспечения

Платформы SIL имеет два основных компонента и два канала связи. Поток данных через оба каналы, а также между обоих компонентов, необходимых для успешного развертывания инвентаризации программного обеспечения (предполагается среде виртуализованный или в облаке, — исключительно физических сред необходима только один из каналов связи). Необходимо понять компоненты и поток данных об инвентаризации программного обеспечения правильного развертывания. После просмотра в обзорных видеоматериалах выше, будет видно схеме архитектуры, показаны соответствующие компоненты и поток данных на обоих каналов. Оранжевый цвет стрелки обозначают удаленные запросы через WinRM, зеленый пунктирные стрелки обозначают, что HTTPS отправляет средство инвентаризации программного обеспечения из инвентаризации программного обеспечения в каждый конечный узел WS:

![](../media/software-inventory-logging/image1.png)

Если возникли проблемы с инвентаризацией программного обеспечения, он скорее всего связана с перебои в поток данных по каналам, а также между компонентами. Ниже приведены наиболее распространенные проблемы, связанные с потоком данных, а затем в следующем разделе действия по устранению неполадок, чтобы устранить все проблемы, три.

-   **Причина 1 поток данных** — **нет данных в отчете при использовании командлета Publish-SilReport** (или обычно отсутствующих данных).

-   **Причина 2 потока данных** — **слишком много серверов в разделе неизвестный узел** в отчете.

-   **Проблема 3 потока данных** — **слишком много виртуальных машин в группе физические узлы, указанные как Неизвестная ОС** в отчет, и/или ошибку, полученных при использовании **Publish-SilData** на серверах Windows, под управлением инвентаризации программного обеспечения.

## <a name="troubleshooting-data-flow-issues"></a>Устранение неполадок потока данных

Прежде чем начать, необходимо знать, как давно средства инвентаризации программного обеспечения к работе с **Start-SilAggregator** командлета.

>[!IMPORTANT]
>Будет нет данных в отчете до обработки куба данных SQL во время локальной системы 3: 00. Не выполняйте действия по устранению неполадок пока куб обработан данных.

При устранении неполадок данных в отчет (или в отчете отсутствуют), более свежие, чем время последней обработки куба или прежде, чем когда-либо куб обработан (для новой установки), выполните следующие действия для обработки куба данных SQL в режиме реального времени :

1. Войдите в качестве администратора SQL Server и выполните **SSMS** в командной строке.
2. Подключитесь к ядру СУБД.
3. Разверните **агента SQL Server** и раскройте **заданий**.
4. Щелкните правой кнопкой мыши **SILStagingRefresh** , а затем выберите **запустить задание на шаге**.
5. Нажмите кнопку **запустить** и подождите, пока индикатор хода выполнения обновления для завершения.
6. Откройте PowerShell от имени администратора и выполните **публикации silreport - ОткрытьОтчет** командлета.

Если по-прежнему нет данных в отчете, продолжить устранение проблем три данных потока.

### <a name="data-flow-issue-1"></a>Проблемы потока данных 1 

#### <a name="no-data-in-the-report-when-using-the-publish-silreport-cmdlet-or-data-is-generally-missing"></a>Нет данных в отчете при использовании командлета Publish-SilReport (или данных обычно отсутствует)

Если данные отсутствуют, вполне вероятно, из-за необходимости еще не обработаны куб данных SQL. Если вы считаете, что данные, отсутствующие должны попасть в средство инвентаризации программного обеспечения перед обработкой куба обработана недавно, путь прохождения данных в обратном порядке. Выберите уникальный узла и виртуальной Машины уникальным для устранения неполадок. Путь к данным в обратном порядке будет **отчет в виде загружаемого МОДУЛЯ** &lt; **базы данных в виде загружаемого МОДУЛЯ** &lt; **локальный каталог в виде загружаемого МОДУЛЯ** &lt;  **удаленного физического узла** или **WS виртуальной Машины под управлением агента/задача инвентаризации программного обеспечения**.

#### <a name="check-to-see-if-data-is-in-the-database"></a>Проверьте, находится ли данные в базе данных

Для поиска данных двумя способами: **PowerShell** или **SSMS**.

>[!Important]
>Если куб обработан по крайней мере один раз, так как данные вставлены в виде загружаемого МОДУЛЯ в базе данных, эти данные должно быть отражено в отчете. Если нет данных в базе данных затем либо опроса физических узлов произошел сбой или ничего не поступают по протоколу HTTPS, или оба.

 #### <a name="powershell"></a>PowerShell

1. Откройте PowerShell от имени администратора и выполните **get-silvmhost** командлета, а затем запустите **get-silaggregator**.

    >[!NOTE]
    >Выходные данные **get-silaggregator** всегда будет имитировать **вкладка сведений о Windows Server** отчета Excel. Не ожидайте, что результат будет другим.

2. Запустите **get-silvmhost**
   - Если затем нет узлов в списке, добавьте узлы, использующие **-silvmhost** командлета.
   - Если узлы указаны как **Неизвестный**, а затем перейдите к проблема 2. 
   d - Если узлы перечислены в списке, но не **datetime** под **последние опроса** столбец, а затем перейдите в раздел **проблема 2** ниже.

**Другие связанные команды**

**Get-SilAggregator - Computername &lt;полное доменное имя известных сервера, принудительная отправка данных&gt;** : Даже перед куб обработан, создаст сведений из базы данных о компьютере (VM). Таким образом этот командлет можно использовать для проверки на основе данных в базе данных Windows Server, отправить данные Инвентаризации по протоколу HTTPS, до или без обработки куба в 03: 00 (или если еще не обновляются в кубе, в режиме реального времени, как описано в начале этого раздела).

**Get-SilAggregator - VmHostName &lt;полное доменное имя опроса физического узла там, где имеется значение в столбце последние опроса, при использовании командлета Get-SilVmHost&gt;** : Это создаст сведения из базы данных о физическом узле, даже в том случае, до обработки куба.

#### <a name="ssms"></a>SSMS

n**поиска данных с узлов выполняется опрос:**
 
1. Откройте **SSMS** и подключитесь к **СУБД**.
2. Разверните **баз данных**, разверните **SoftwareInventoryLogging** базы данных, разверните **таблиц**, щелкните правой кнопкой мыши **HostInfo** таблицу и затем Выберите первые 1000 строк. 

    Если данные для одного или нескольких узлов в таблице, то опрос, / those узлами успешного выполнения хотя бы один раз.

   **Проверьте данные из виртуальных машин или автономных серверах, которые отправленных данных по протоколу HTTPS:** 

3. Откройте **SSMS** и подключитесь к **СУБД**.
   a2. Разверните **баз данных**, разверните **SoftwareInventoryLogging** базы данных, разверните **таблиц**, щелкните правой кнопкой мыши **VMInfo** таблицу и затем Выделите 1000 верхних строк. 

    >[!NOTE] 
    >Представляет один обработки каждой строки для виртуальной Машины уникальным **bmil** файл успешно отправлено по протоколу HTTPS и обрабатывается средство инвентаризации программного обеспечения. Файлы Bmil конфиденциальные файлы, используемые SIL, она будет создана каждого наших каждым экземпляром SIL Обратите внимание, что это требуется только при инвентаризации программного обеспечения и в виде загружаемого МОДУЛЯ используются в виртуальных средах. В противном случае только HTTPS-трафик или ожидаемой необходимости).

   Все данные в базе данных должно быть отражено в отчетах инвентаризации программного обеспечения, после обработки куба.

### <a name="data-flow-issue-2"></a>Поток данных, выпуск 2
#### <a name="too-many-servers-under-unknown-host"></a>Слишком много серверов в разделе неизвестный узел

Это может произойти в виртуальных средах при инвентаризации программного обеспечения успешно не опрашивает физические узлы, на которых размещаются виртуальные машины.

1. Откройте **PowerShell** с правами администратора и выполнения **get-silvmhost** командлета.

    -   Если узлы указаны как **Неизвестный**, **-silvmhost** командлет не работает — обычно из-за плохой добавленных учетных данных для доступа к этим узлам (таким образом, неизвестно). Но если проверки учетных данных, это может означать автоматическое обнаружение **hosttype** и **hypervisortype** в **-silvmhost** командлету не удалось распознать Платформа. Существуют расширенные для таких ситуациях действия по устранению неполадок, но здесь не описаны (проверьте каналы EventViewer средства инвентаризации программного обеспечения).

    -   Если в списке узлов, и **hosttype** и **hypervisortype** отображаются со значениями, которые не являются **Неизвестный**, т. е. Windows и Hyper-v, или Ubuntu и Xen, и т.д., но не **datetime** под **последние опроса** столбец, затем опрос еще не произошло успешно.

        -   Необходимо подождать час после добавления узла для опроса возникает (при условии, что этот интервал по умолчанию — можно проверить с помощью **get-silaggregator** командлет).

        -   Если он был часа с момента добавления узла, убедитесь, что задача опроса: В **планировщик задач**выберите **Software Inventory Logging Aggregator** под **Microsoft** &gt; **Windows** и установите флажок журнал задания.

    -   Если указан узел, но не имеет смысла для **RecentPoll**, **HostType**, или **HypervisorType**, это может быть значительной степени не учитываются. Это происходит только в средах Hyper-v. Эти данные действительно поступают из виртуальной Машины Windows Server, определяющий физического узла, на котором он выполняется по протоколу HTTPS. Это могут быть полезны при выявлении в определенную виртуальную Машину, которая сообщает, но требует интеллектуального анализа данных в базе данных с помощью **Get SilAggregatorData** командлета.

После правильно опрашиваемых узлов, можно просматривать данные для этих физических узлов, в базе данных в виде загружаемого МОДУЛЯ где **datetime** под **последние опроса**. Проблема 1 раздела выше шаги для получения этих данных.

### <a name="data-flow-issue-3"></a>Проблемы потока данных 3
#### <a name="too-many-physical-hosts-with-vms-listed-as-unknown-os"></a>Слишком много физических узлов с виртуальными машинами, указанные как Неизвестная ОС

1. Выберите один Windows Server конечным узлом (VM), которые хранятся на одном из этих узлов, войдите в систему как администратор.
2. Откройте PowerShell с правами администратора.
3. Проверьте **SilLogging** выполняется с помощью **Get-SilLogging** командлета.
   - Если запущена, попробуйте вручную отправить данные инвентаризации программного обеспечения с помощью **Publish-SilData**.

   - Если возникает ошибка:
     - Убедитесь, **targeturi** имеет **https://** в записи.
     - Убедитесь, что все предварительные требования 
     - Обеспечить установку всех необходимых обновлений для Windows Server (см. предварительные условия для инвентаризации программного обеспечения). Быстрый способ проверить (на WS 2012 R2. только) — поиск обновлений с помощью следующего командлета: **Get-SilWindowsUpdate \*3060, \*3000**
     - Убедитесь, сертификату, используемому для проверки подлинности в средстве инвентаризации программного обеспечения установлен в правильном хранилище на локальном сервере должны быть подвергнуты инвентаризации с **SilLogging**.
     - В средстве инвентаризации, убедитесь, что отпечаток сертификата, используемого для проверки подлинности с помощью средства инвентаризации программного обеспечения добавляется в список с помощью **командлета Set-SilAggregator** **-AddCertificateThumbprint** командлет.
     - При использовании корпоративных сертификатов убедитесь, что сервер с включенной инвентаризацией программного обеспечения входит в домен, для которого сертификат был создан, либо его можно проверить другим способом в корневом центре. Если сертификат не является доверенным на локальном компьютере, который пытается отправить данные средству инвентаризации программного обеспечения, действие завершится ошибкой.

     Если все вышеперечисленное установлен и проверены, но проблема повторяется:

     - Убедитесь, что сертификат, используемый для установки средства инвентаризации программного обеспечения находится в работоспособном состоянии и совпадает с именем самого сервера средства инвентаризации программного обеспечения. Кроме того, если для установки средства инвентаризации программного обеспечения используются корпоративные сертификаты, может потребоваться присоединение средства к домену, в котором был создан сертификат (эти шаги необязательны, если другие компьютеры успешно пересылают данные на то же средство инвентаризации программного обеспечения).

     -  Наконец, можно проверить наличие кэшированных файлов инвентаризации программного обеспечения на сервере при попытке отправить, в следующей папке **\Windows\System32\Logfiles\SIL**. Если **SilLogging** запущен и работает более часа, или **Publish-SilData** недавно выполнена и нет файлов в этом каталоге, чем это было по инвентаризации успешно выполнена.

Если нет ошибок и не выводятся на консоль, затем данные Push-уведомлений/публикации с конечным узлом Windows Server средства инвентаризации программного обеспечения по протоколу HTTPS прошла успешно. К траектории входа вперед, данные инвентаризации программного обеспечения с правами администратора и проверьте файлы данных, которые уже доступны. Перейдите к **Program Files (x86)** &gt; **средства инвентаризации программного обеспечения Microsoft** &gt; каталог в виде загружаемого МОДУЛЯ. Вы можете просмотреть файлы данных, поступающих в реальном времени.

>[!NOTE] 
>Более одного файла данных были перенесены с **Publish-SilData** командлета. Инвентаризацию программного обеспечения на конечным узлом будет кэшировать неудачных Push-уведомления в течение 30 дней. На следующей успешной отправке все файлы данных изменится на средство инвентаризации программного обеспечения для обработки. Таким образом вновь установить средство инвентаризации программного обеспечения удалось показать данные из узла конечного задолго до собственную программу установки.

>[!NOTE] 
>Существуют правила, которым в виде загружаемого МОДУЛЯ при обработке данных файлов в каталоге в виде загружаемого МОДУЛЯ, которые имеют значение только в низком объеме трафика. Высокий трафик всегда будет активировать обработку в режиме реального времени. Поведение по умолчанию является то, что обработка вступает в силу либо после получения 100 файлов в каталоге или в течение 15 минут. При устранении неполадок end-to-end, в небольших средах, часто бывает необходимо подождать 15 минут.

После обработки этих файлов, вы увидите данные в базе данных.