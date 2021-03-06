---
title: Устранение неполадок инвентаризации программного обеспечения
description: Описание способов устранения распространенных проблем развертывания ведения журнала инвентаризации программного обеспечения.
ms.prod: windows-server
ms.technology: manage-software-inventory-logging
ms.topic: article
author: brentfor
ms.author: coreyp
manager: lizapo
ms.date: 10/16/2017
ms.openlocfilehash: 5a02caf63bbd02705aebb8306a7b50a32f3d6c82
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851417"
---
# <a name="troubleshoot-software-inventory-logging"></a>Устранение неполадок инвентаризации программного обеспечения 

>Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

## <a name="understanding-sil"></a>Основные сведения о SIL

Прежде чем начать устранение неполадок SIL, вы получите хорошее представление о его компонентах и принципах работы. В следующих видеороликах представлен обзор агрегатора SIL и SIL, а также способы их использования для пересылки и создания отчетов по данным инвентаризации.

1. [Общие сведения о ведении журнала инвентаризации программного обеспечения (SIL) (10:57)](https://channel9.msdn.com/Blogs/Regular-IT-Guy/An-Introduction-to-Software-Inventory-Logging-SIL)

2. [Ведение журнала инвентаризации программного обеспечения: Настройка агрегатора SIL (14:34)](https://channel9.msdn.com/Blogs/windowsserver/Software-Inventory-Logging-Setting-up-SIL-Aggregator)

3. [Ведение журнала инвентаризации программного обеспечения: Включение пересылки SIL (7:20)](https://channel9.msdn.com/Blogs/windowsserver/Software-Inventory-Logging-Enabling-SIL-Forwarding)

## <a name="how-sil-data-flow-works"></a>Как работает поток данных SIL

Платформа SIL имеет два основных компонента и два канала связи. Поток данных по обоим каналам и между ними необходим для успешного развертывания SIL (предполагается, что виртуальная или облачная среда — исключительно физические среды, для которых требуется только один канал связи). Необходимо разобраться в компонентах и потоке данных SIL, чтобы правильно развернуть его. Просмотрев обзорные видеоролики выше, вы увидите архитектурную схему, которая иллюстрирует компоненты и поток данных по обоим каналам. Оранжевые стрелки указывают на удаленные запросы по WinRM, зеленые Пунктирные стрелки обозначают записи HTTPS в агрегатор SIL из SIL в каждом узле WS.

![](../media/software-inventory-logging/image1.png)

Если возникла проблема с SIL, скорее всего, это связано с нарушением потока данных по каналам и между компонентами. Ниже приведены наиболее распространенные проблемы, связанные с потоком данных, а также действия по устранению каждой из этих трех проблем в следующем разделе.

-   **Ошибка потока данных 1** — **в отчете нет данных при использовании командлета Publish-силрепорт** (или вообще отсутствующих данных).

-   **Ошибка потока данных 2** — **слишком много серверов в неизвестном узле** отчета.

-   Ошибка **потока данных 3** — **слишком много виртуальных машин в физических узлах, указанных как неизвестная ОС** в отчете, и (или) при использовании **Publish-СИЛДАТА** на серверах Windows с SIL.

## <a name="troubleshooting-data-flow-issues"></a>Устранение неполадок потока данных

Прежде чем начать, необходимо знать, сколько времени назад SIL агрегатор запущен с помощью командлета **Start-силаггрегатор** .

>[!IMPORTANT]
>В отчете нет данных, пока куб данных SQL не будет обрабатываться в 03:00 локально системное время. Не продолжайте выполнять действия по устранению неполадок до тех пор, пока куб не обработал данные.

При диагностике данных в отчете (или отсутствующем в отчете), который более новый, чем последний раз, когда куб был обработан, или до того, как куб был обработан (для новой установки), выполните следующие действия для обработки куба данных SQL в режиме реального времени.

1. Войдите в систему от имени администратора SQL Server и запустите **SSMS** из командной строки.
2. Подключитесь к ядру СУБД.
3. Разверните **Агент SQL Server** , а затем — **задания**.
4. Щелкните правой кнопкой мыши **силстагингрефреш** и выберите пункт **запустить задание на шаге**.
5. Нажмите кнопку **запустить** и дождитесь завершения обновления индикатора выполнения.
6. Откройте PowerShell с правами администратора и выполните командлет **Publish-силрепорт-ОткрытьОтчет** .

Если в отчете по-прежнему нет данных, продолжайте устранение неполадок, связанных с тремя ошибками потока данных.

### <a name="data-flow-issue-1"></a>Ошибка потока данных 1 

#### <a name="no-data-in-the-report-when-using-the-publish-silreport-cmdlet-or-data-is-generally-missing"></a>В отчете нет данных при использовании командлета Publish-Силрепорт (или данные, как правило, отсутствуют)

Если данные отсутствуют, скорее всего, это связано с тем, что куб данных SQL еще не обработан. Если он был обработан недавно и вы считаете, что данные, которые отсутствуют, должны быть получены на агрегатор перед обработкой куба, следуйте пути к данным в обратном порядке. Выберите уникальный узел и уникальную виртуальную машину для устранения неполадок. Путь к данным в обратную **сила Report** &lt; **сила Database** &lt; **сила локальный каталог** &lt; **Удаленный физический узел** или **Виртуальная машина WS с агентом SIL/Task**.

#### <a name="check-to-see-if-data-is-in-the-database"></a>Проверьте, находятся ли данные в базе данных

Существует два способа проверки данных: **PowerShell** или **SSMS**.

>[!Important]
>Если куб обработал хотя бы один раз, так как сила вставляет данные в базу данных, эти данные должны быть отражены в отчете. Если в базе данных нет данных, то либо опрос физических узлов завершается неудачей, либо ничего не принимается по протоколу HTTPS.

 #### <a name="powershell"></a>PowerShell

1. Откройте PowerShell с правами администратора и выполните командлет **Get-силвмхост** , а затем выполните команду **Get-силаггрегатор**.

    >[!NOTE]
    >Выходные данные **Get-силаггрегатор** всегда будут имитировать вкладку « **сведения о Windows Server** » отчета Excel. Не требуется другой результат.

2. Выполните команду **Get-силвмхост** .
   - Если узлов нет в списке, добавьте узлы с помощью командлета **Add-силвмхост** .
   - Если узлы указаны как **неизвестные**, перейдите к вопросу 2. 
   d — если узлы перечислены, но в столбце " **недавние опросы** " нет **даты и времени** , перейдите к следующей **ошибке 2** .

**Другие связанные команды**

**Get-силаггрегатор-Computername &lt;полное доменное имя известного сервера&gt;** . при этом будут получены сведения из базы данных о компьютере (ВМ), даже перед обработкой куба. Таким образом, этот командлет можно использовать для проверки данных в базе данных для Windows Server, принудительной отправки SIL данных по протоколу HTTPS, до или без, процесса Куба в 03:00 (или если вы еще не обновили куб в режиме реального времени, как описано в начале этого раздела).

**Get-силаггрегатор-VmHostName &lt;полное доменное имя опроса физического узла, где имеется значение в столбце недавних опросов при использовании командлета Get-силвмхост&gt;** : это приведет к созданию сведений из базы данных о физическом узле, даже перед обработкой куба.

#### <a name="ssms"></a>SSMSE

n**Проверка данных с узлов, которые опрашиваются:**
 
1. Откройте **среду SSMS** и подключитесь к **ядро СУБД**.
2. Разверните **узел базы данных, разверните**базу данных **софтвареинвенторилоггинг** , разверните узел **таблицы**, щелкните правой кнопкой мыши таблицу **хостинфо** и выберите первые 1000 строк. 

    Если в таблице есть данные для одного или нескольких узлов, то опрос этих или узлов был выполнен по крайней мере один раз.

   **Проверьте данные с виртуальных машин или автономных серверов, которые отправили данные по протоколу HTTPS:** 

3. Откройте **среду SSMS** и подключитесь к **ядро СУБД**.
   a2. Разверните **узел базы данных, разверните**базу данных **софтвареинвенторилоггинг** , разверните узел **таблицы**, щелкните правой кнопкой мыши таблицу **вминфо** и выберите первые 1000 строк. 

    >[!NOTE] 
    >Каждая строка для уникальной виртуальной машины будет представлять один обработанный файл **бмил** , успешно отправленный по протоколу HTTPS и обработанный агрегатором SIL. Файлы бмил — это частные файлы, используемые SIL. по одному создается каждый экземпляр SIL. Обратите внимание, что это необходимо только в том случае, если в виртуальных средах используются SIL и сила. В противном случае требуется только HTTPS-трафик.

   Все данные в базе данных должны быть отражены в отчетах SIL после обработки куба.

### <a name="data-flow-issue-2"></a>Проблемы потока данных 2
#### <a name="too-many-servers-under-unknown-host"></a>Слишком много серверов в неизвестном узле

Это может произойти в виртуальных средах, когда агрегатор SIL не может успешно опрашивать физические узлы, на которых размещены виртуальные машины.

1. Откройте **PowerShell** с правами администратора и выполните командлет **Get-силвмхост** .

    -   Если узлы указаны как **неизвестные**, командлет **Add-силвмхост** работает неправильно — обычно из-за добавления неправильных учетных данных для доступа к этим узлам (то есть неизвестно). Но если учетные данные проверены, это может означать, что автоматическое обнаружение **HostType** и **хипервисортипе** в командлете **Add-силвмхост** не смогло распознать платформу. В этих ситуациях доступны дополнительные действия по устранению неполадок, но они не описаны здесь (проверьте каналы агрегатора Евентвиевер SIL).

    -   Если указаны узлы, **HostType** и **хипервисортипе** перечислены со значениями, которые не являются **неизвестными**, т. е. Windows, HyperV, Ubuntu и Xen и т. д., но в столбце " **недавние опросы** " нет **даты и времени** , опрос еще не выполнен.

        -   Необходимо подождать час после добавления узла для выполнения опроса (если для этого интервала задано значение по умолчанию — можно проверить с помощью командлета **Get-силаггрегатор** ).

        -   Если прошло час с момента добавления узла, проверьте, выполняется ли задача опроса: в **планировщик задач**выберите модуль **агрегация журнала инвентаризации программного обеспечения** в разделе **Microsoft** &gt; **Windows** и проверьте журнал задачи.

    -   Если узел указан, но нет значения для **рецентполл**, **HostType**или **хипервисортипе**, это значение можно не учитывать. Это произойдет только в средах HyperV. Фактически эти данные поступают с виртуальной машины Windows Server, определяющей физический узел, на котором он работает по протоколу HTTPS. Это может быть полезно при определении конкретной виртуальной машины, которая является отчетом, но требует интеллектуального анализа базы данных с помощью командлета **Get-силаггрегатордата** .

После того как узлы будут опрошены правильно, вы сможете увидеть данные для этих физических узлов в базе данных сила, где имеется **Дата и время** в **последнем опросе**. В разделе Проблема 1 приведена процедура получения этих данных.

### <a name="data-flow-issue-3"></a>Ошибка потока данных 3
#### <a name="too-many-physical-hosts-with-vms-listed-as-unknown-os"></a>Слишком много физических узлов с виртуальными машинами в списке "Неизвестная ОС"

1. Выберите один из конечных узлов Windows Server (ВМ), который вы узнаете на одном из этих узлов, войдите как администратор.
2. Откройте PowerShell с правами администратора.
3. Убедитесь, что **SilLogging** выполняется с помощью командлета **Get-SilLogging** .
   - При запуске попробуйте вручную отправить данные SIL с помощью **Publish-силдата**.

   - Если возникает ошибка:
     - Убедитесь, что в записи **таржетури** есть **https://** .
     - Убедитесь, что выполнены все предварительные требования 
     - Убедитесь, что установлены все необходимые обновления для Windows Server (см. Предварительные требования для SIL). Быстрый способ проверки (только для WS 2012 R2) заключается в поиске с помощью следующего командлета: **Get-силвиндовсупдате \*3060, \*3000**
     - Убедитесь, что сертификат, используемый для проверки подлинности с помощью агрегатора, установлен в правильном хранилище на локальном сервере для инвентаризации с помощью **SilLogging**.
     - В агрегаторе SIL убедитесь, что отпечаток сертификата, используемого для проверки подлинности с помощью агрегатора, добавлен в список с помощью командлета **Set-силаггрегатор** **– аддцертификатесумбпринт** .
     - При использовании корпоративных сертификатов убедитесь, что сервер с включенной инвентаризацией программного обеспечения входит в домен, для которого сертификат был создан, либо его можно проверить другим способом в корневом центре. Если сертификат не является доверенным на локальном компьютере, который пытается отправить данные средству инвентаризации программного обеспечения, действие завершится ошибкой.

     Если все вышеперечисленное проверены и проверены, но проблема сохраняется:

     - Убедитесь, что сертификат, используемый для установки агрегатора SIL, является работоспособным и соответствует имени самого сервера агрегатора SIL. Кроме того, если для установки средства инвентаризации программного обеспечения используются корпоративные сертификаты, может потребоваться присоединение средства к домену, в котором был создан сертификат (эти шаги необязательны, если другие компьютеры успешно пересылают данные на то же средство инвентаризации программного обеспечения).

     -  Наконец, можно проверить следующее расположение кэшированных файлов SIL на сервере, пытающемся переслать/отправить, **\Windows\System32\Logfiles\SIL**. Если **SilLogging** запущен и выполнялся более часа, или **Publish-силдата** был запущен недавно, и в этом каталоге нет файлов, значит, вход в агрегатор завершился успешно.

Если ошибка отсутствует и выходные данные на консоли отсутствуют, то передача данных или публикация из конечного узла Windows Server в SIL по протоколу HTTPS завершилась успешно. Чтобы проследить путь к пересылке данных, войдите в агрегатор SIL как администратор и изучите полученные файлы данных. Перейдите в раздел **Program Files (x86)** &gt; **Microsoft SIL агрегатор** &gt; сила Directory. Вы можете просматривать файлы данных, поступающие в режиме реального времени.

>[!NOTE] 
>С помощью командлета **Publish-силдата** может быть перенесено более одного файла данных. SIL на конечном узле кэширует push-уведомления с ошибками в течение 30 дней. При следующей успешной отправке все файлы данных будут переходят в агрегатор для обработки. В этом случае вновь настроенный агрегатор SIL может показывать данные с конечного узла, прежде чем выполнять собственную настройку.

>[!NOTE] 
>Существуют правила, сила при обработке файлов данных в каталоге сила, которые относятся только к ситуациям с низким трафиком. Высокий трафик всегда инициирует обработку в режиме реального времени. Поведение по умолчанию заключается в том, что обработка начнется либо после 100 файлов в каталог, либо через 15 минут. При устранении неполадок сквозной среды в небольшой среде часто бывает необходимо подождать 15 минут.

После обработки этих файлов данные будут отображаться в базе данных.
