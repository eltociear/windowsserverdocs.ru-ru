---
ms.assetid: 01c8cece-66ce-4a83-a81e-aa6cc98e51fc
title: Дополнительные параметры дедупликации данных
ms.prod: windows-server-threshold
ms.technology: storage-deduplication
ms.topic: article
author: wmgries
manager: klaasl
ms.author: wgries
ms.date: 09/15/2016
ms.openlocfilehash: af977519b5e77eb768fdf8de1e6a34f7c8274666
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/31/2019
ms.locfileid: "66447238"
---
# <a name="advanced-data-deduplication-settings"></a>Дополнительные параметры дедупликации данных

> Область применения: Windows Server (Semi-Annual Channel), Windows Server 2016

В этом документе описывается изменение дополнительных параметров [дедупликации данных](overview.md). Параметров по умолчанию должно быть достаточно для [рекомендуемых рабочих нагрузок](install-enable.md#enable-dedup-candidate-workloads). Основная причина изменения этих параметров — это повышение эффективности дедупликации данных при выполнении других типов рабочих нагрузок.

## <a id="modifying-job-schedules"></a>Изменение расписания заданий дедупликации данных
[Расписания заданий дедупликации данных по умолчанию](understand.md#job-info) прекрасно взаимодействуют с рекомендуемыми рабочими нагрузками. Они не принудительны (за исключением задания *приоритетной оптимизации* с поддержкой типа использования [ **** ](understand.md#usage-type-backup)). Если требования рабочих нагрузок к ресурсам значительные, можно обеспечить, чтобы задания выполнялись только во время простоя, а также сократить или увеличить допустимый объем системных ресурсов, потребляемых заданием дедупликации данных.

### <a id="modifying-job-schedules-change-schedule"></a>Изменение расписания дедупликации данных
Для планирования заданий дедупликации данных используется планировщик заданий Windows. Кроме того, их можно просматривать и изменять по пути Microsoft\Windows\Дедупликация. Дедупликация данных включает несколько командлетов, упрощающих планирование.
* [`Get-DedupSchedule`](https://technet.microsoft.com/library/hh848446.aspx) показывает текущие запланированные задания.
* [`New-DedupSchedule`](https://technet.microsoft.com/library/hh848445.aspx) Создает новое запланированное задание.
* [`Set-DedupSchedule`](https://technet.microsoft.com/library/hh848447.aspx) Изменение существующего запланированного задания.
* [`Remove-DedupSchedule`](https://technet.microsoft.com/library/hh848451.aspx) Удаляет запланированное задание.

Обеспечить выполнение заданий в нерабочее время — наиболее распространенная причина для изменения при выполнении заданий дедупликации данных. В приведенном ниже пошаговом примере показано, как изменить расписание дедупликации данных для *оптимального* сценария: гиперконвергентный узел Hyper-V неактивен в выходные и после 19:00 в будние вечера. Чтобы изменить расписание, выполните следующие командлеты PowerShell с правами администратора.

1. Отключите запланированные почасовые задания [оптимизации](understand.md#job-info-optimization).  
    ```PowerShell
    Set-DedupSchedule -Name BackgroundOptimization -Enabled $false
    Set-DedupSchedule -Name PriorityOptimization -Enabled $false
    ```

2. Удалите текущие запланированные задания [сборки мусора](understand.md#job-info-gc) и [проверки целостности](understand.md#job-info-scrubbing).
    ```PowerShell
    Get-DedupSchedule -Type GarbageCollection | ForEach-Object { Remove-DedupSchedule -InputObject $_ }
    Get-DedupSchedule -Type Scrubbing | ForEach-Object { Remove-DedupSchedule -InputObject $_ }
    ```

3. Создайте ежедневное задание оптимизации с высоким приоритетом, выполняющееся в 19:00, а также предоставьте доступ ко всем ресурсам ЦП и памяти в системе.
    ```PowerShell
    New-DedupSchedule -Name "NightlyOptimization" -Type Optimization -DurationHours 11 -Memory 100 -Cores 100 -Priority High -Days @(1,2,3,4,5) -Start (Get-Date "2016-08-08 19:00:00")
    ```

    >[!NOTE]  
    > Часть с *датой* значения `System.Datetime`, указываемая в параметре `-Start`, несущественна (пока она указана в прошлом), но часть с *временем* указывает на время начала задания.
4. Создайте еженедельное задание сборки мусора с высоким приоритетом, выполняющееся по субботам начиная с 7:00, а также предоставьте доступ ко всем ресурсам ЦП и памяти в системе.
    ```PowerShell
    New-DedupSchedule -Name "WeeklyGarbageCollection" -Type GarbageCollection -DurationHours 23 -Memory 100 -Cores 100 -Priority High -Days @(6) -Start (Get-Date "2016-08-13 07:00:00")
    ```

5. Создайте еженедельное задание проверки целостности с высоким приоритетом, выполняющееся по воскресеньям начиная с 7:00, а также предоставьте доступ ко всем ресурсам ЦП и памяти в системе.
    ```PowerShell
    New-DedupSchedule -Name "WeeklyIntegrityScrubbing" -Type Scrubbing -DurationHours 23 -Memory 100 -Cores 100 -Priority High -Days @(0) -Start (Get-Date "2016-08-14 07:00:00")
    ```

### <a id="modifying-job-schedules-available-settings"></a>Доступные параметры на уровне задания
Для новых или запланированных заданий дедупликации данных можно выбрать следующие параметры:

<table>
    <thead>
        <tr>
            <th style="min-width:125px">Имя параметра</th>
            <th>Определение</th>
            <th>Допустимые значения</th>
            <th>Почему необходимо задать это значение?</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Тип</td>
            <td>Тип задания, который нужно запланировать</td>
            <td>
                <ul>
                    <li>Оптимизация</li>
                    <li>Сборка мусора</li>
                    <li>Проведение</li>
                </ul>
            </td>
            <td>Это значение является обязательным, так как это тип задания, который нужно запланировать. После планирования задачи это значение нельзя изменить.</td>
        </tr>
        <tr>
            <td>Priority</td>
            <td>Системный приоритет запланированного задания</td>
            <td>
                <ul>
                    <li>Высокий</li>
                    <li>Средний</li>
                    <li>Низкий</li>
                </ul>
            </td>
            <td>Это значение позволяет определить распределение времени ЦП в системе. Если установить значение <em>Высокий</em>, будет использоваться больше времени ЦП, а если <em>Низкий</em> — меньше.</td>
        </tr>
        <tr>
            <td>Дни</td>
            <td>Дни, на которые запланировано выполнение задания</td>
            <td>Массив целых чисел от 0 до 6, определяющих дни недели:<ul>
                <li>0 — воскресенье;</li>
                <li>1 — понедельник;</li>
                <li>2 — вторник;</li>
                <li>3 — среда;</li>
                <li>4 — четверг;</li>
                <li>5 — пятница;</li>
                <li>6 — суббота.</li>
            </ul></td>
            <td>Запланированные задачи нужно выполнять по крайней мере раз в день.</td>
        </tr>
        <tr>
            <td>Ядра</td>
            <td>Процентное выражение ядер в системе, необходимых для выполнения задания.</td>
            <td>Целые числа от 0 до 100 (указывают значение в процентах)</td>
            <td>Чтобы контролировать уровень влияния задания на вычислительные ресурсы в системе.</td>
        </tr>
        <tr>
            <td>DurationHours</td>
            <td>Максимально допустимая продолжительность выполнения задания (в часах)</td>
            <td>Положительные целые числа</td>
            <td>Чтобы предотвратить выполнение в рабочую нагрузку задания&#39;несколько часов не в режиме простоя</td>
        </tr>
        <tr>
            <td>Enabled</td>
            <td>Возможность выполнения задания.</td>
            <td>True или False</td>
            <td>Чтобы отключить задание, не удаляя его</td>
        </tr>
        <tr>
            <td>Полный</td>
            <td>Планирование задания полной сборки мусора</td>
            <td>Параметр (True или False)</td>
            <td>По умолчанию каждое четвертое задание представляет собой задание полной сборки мусора. С помощью этого параметра можно запланировать более частое выполнение полной сборки мусора.</td>
        </tr>
        <tr>
            <td>InputOutputThrottle</td>
            <td>Указывает объем регулирования входящих и исходящих данных для задания.</td>
            <td>Целые числа от 0 до 100 (указывают значение в процентах)</td>
            <td>Регулирование обеспечивает неработающие заданий&#39;t конфликтовать с другими процессами ввода-вывода.</td>
        </tr>
        <tr>
            <td>Память</td>
            <td>Процентное выражение памяти в системе, необходимой для выполнения задания.</td>
            <td>Целые числа от 0 до 100 (указывают значение в процентах)</td>
            <td>Чтобы контролировать уровень влияния задания на ресурсы памяти в системе.</td>
        </tr>
        <tr>
            <td>Имя</td>
            <td>Имя запланированного задания</td>
            <td>Строка</td>
            <td>Задание должно иметь уникальное персональное имя.</td>
        </tr>
        <tr>
            <td>ReadOnly</td>
            <td>Указывает на обработку и сообщение о найденных повреждениях в задании проверки, а не выполнение действий по восстановлению.</td>
            <td>Параметр (True или False)</td>
            <td>Необходимо вручную восстановить файлы, расположенные на поврежденных разделах диска.</td>
        </tr>
        <tr>
            <td>Начало</td>
            <td>Указывает необходимое время запуска задания</td>
            <td><code>System.DateTime</code></td>
            <td><em>Даты</em> частью <code>System.Datetime</code> для <em>запустить</em> не имеет значения (условии, что он&#39;s в прошлом), но <em>время</em> часть указывает время начала задания .</td>
        </tr>
        <tr>
            <td>StopWhenSystemBusy</td>
            <td>Указывает, должна ли прекратиться дедупликация данных в случае занятости системы</td>
            <td>Параметр (True или False)</td>
            <td>Этот параметр дает возможность управлять поведением дедупликации данных. Это особенно важно, если необходимо выполнить дедупликацию данных при выполнении рабочей нагрузки.</td>
        </tr>
    </tbody>
</table>

## <a id="modifying-volume-settings"></a>Изменение параметров дедупликации данных на уровне тома
### <a id="modifying-volume-settings-how-to-toggle"></a>Переключение параметров тома
Вы можете задать параметры по умолчанию на уровне тома для дедупликации данных через [тип использования](understand.md#usage-type), выбранный при включении дедупликации для тома. Дедупликация данных включает командлеты, упрощающие изменение параметров на уровне тома:

* [`Get-DedupVolume`](https://technet.microsoft.com/library/hh848448.aspx)
* [`Set-DedupVolume`](https://technet.microsoft.com/library/hh848438.aspx)

Основными причинами для изменения параметров тома из выбранного типа использования являются: повышение производительности чтения для конкретных файлов (например, мультимедиа или другие типы файлов, которые уже сжаты) или точная настройка дедупликации данных для повышения уровня оптимизации конкретной рабочей нагрузки. В приведенном ниже примере показано, как изменить параметры тома дедупликации данных для рабочей нагрузки, которая больше всего соответствует рабочей нагрузке файлового сервера общего назначения, но использует часто изменяющиеся большие файлы.

1. Просмотрите текущие параметры тома для общего тома кластера 1.
    ```PowerShell
    Get-DedupVolume -Volume C:\ClusterStorage\Volume1 | Select *
    ```

2. Включите OptimizePartialFiles в общем томе кластера 1 для применения политики MinimumFileAge к разделам файла, а не ко всему файлу. Таким образом большая часть файла оптимизируется, несмотря на то, что разделы файла регулярно изменяются.
    ```PowerShell
    Set-DedupVolume -Volume C:\ClusterStorage\Volume1 -OptimizePartialFiles
    ```

### <a id="modifying-volume-settings-available-settings"></a>Доступные параметры на уровне тома
<table>
    <thead>
        <tr>
            <th style="min-width:125px">Имя параметра</th>
            <th>Определение</th>
            <th>Допустимые значения</th>
            <th>Почему необходимо изменить это значение?</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>ChunkRedundancyThreshold</td>
            <td>Количество ссылок на блок до его копирования в раздел активной зоны хранилища блоков. Раздел активной зоны значение, так называемые &quot;горячей&quot; блоки, на которые часто содержат несколько путей для ускорения доступа.</td>
            <td>Положительные целые числа</td>
            <td>Основная причина изменения этого количества — это повышение скорости сохранения для томов с высокой дупликацией. Как правило, значение по умолчанию (100) — это рекомендуемый параметр и вы не может&#39;нужно изменить.</td>
        </tr>
        <tr>
            <td>ExcludeFileType</td>
            <td>Типы файлов, исключаемые из оптимизации.</td>
            <td>Массив расширений файлов</td>
            <td>Некоторые типы файлов, особенно мультимедиа или файлы, которые уже сжаты, не выигрывают от возможности оптимизации. Этот параметр позволяет настроить исключаемые типы.</td>
        </tr>
        <tr>
            <td>ExcludeFolder</td>
            <td>Указывает пути к папкам, которые не учитываются при оптимизации.</td>
            <td>Массив путей к папкам</td>
            <td>Если необходимо повысить производительность или не оптимизировать содержимое в определенных путях, эти пути на томе можно исключить из оптимизации.</td>
        </tr>
        <tr>
            <td>InputOutputScale</td>
            <td>Указывает уровень параллелизации операций ввода-вывода (очереди ввода-вывода) для дедупликации данных, используемый на томе во время задания постобработки.</td>
            <td>Положительные целые числа в диапазоне от 1 до 36</td>
            <td>Основной причиной для изменения этого значения является уменьшение влияния на производительность высокой рабочей нагрузки ввода-вывода за счет ограничения числа очередей ввода-вывода, которое разрешено использовать на томе при дедупликации данных. Обратите внимание, что изменение этого параметра по умолчанию может привести к дедупликации данных&#39;s завершающей обработки заданий, запускаемых медленно.</td>
        </tr>
        <tr>
            <td>MinimumFileAgeDays</td>
            <td>Число дней после создания файла, прежде чем он будет считаться доступным для оптимизации.</td>
            <td>Положительные целые числа (включая ноль)</td>
            <td>Чтобы повысить производительность активных или недавно созданных файлов, для типов использования <strong>Default</strong> и <strong>HyperV</strong> задается значение 3. Может потребоваться изменить это значение, если необходимо повысить активность дедупликации данных или если дополнительные задержки, связанные с дедупликацией, не важны.</td>
        </tr>
        <tr>
            <td>MinimumFileSize</td>
            <td>Минимальный размер файла, чтобы он мог считаться доступным для оптимизации.</td>
            <td>Положительные целые числа (байты) больше 32 КБ</td>
            <td>Основная причина изменения этого значения — исключение небольших файлов, преимущества оптимизации для которых ограничены (экономия времени вычислений незначительна).</td>
        </tr>
        <tr>
            <td>NoCompress</td>
            <td>Указывает, следует ли сжимать блоки перед их помещением в хранилище блоков.</td>
            <td>True или False</td>
            <td>Некоторые типы файлов, особенно файлы мультимедиа и уже сжатые типы файлов, могут не сжиматься. Этот параметр позволяет отключить сжатие для всех файлов на томе. Это идеальный сценарий при оптимизации набора данных, содержащего большое количество уже сжатых файлов.</td>
        </tr>
        <tr>
            <td>NoCompressionFileType</td>
            <td>Типы файлов, блоки которых не нужно сжимать перед их помещением в хранилище блоков.</td>
            <td>Массив расширений файлов</td>
            <td>Некоторые типы файлов, особенно файлы мультимедиа и уже сжатые типы файлов, могут не сжиматься. Этот параметр позволяет выключить сжатие для этих файлов, обеспечивая экономию ресурсов ЦП.</td>
        </tr>
        <tr>
            <td>OptimizeInUseFiles</td>
            <td>При включении этого параметра файлы, содержащие активные дескрипторы, будут считаться доступными для оптимизации.</td>
            <td>True или False</td>
            <td>Включите этот параметр, если при выполнении рабочей нагрузки файлы остаются открытыми в течение длительного времени. Если этот параметр не включен, файл никогда не будут оптимизированы, если рабочая нагрузка содержит открытый дескриптор, даже если он&#39;s лишь время от времени добавляет данные в конце.</td>
        </tr>
        <tr>
            <td>OptimizePartialFiles</td>
            <td>При включении этого параметра значение MinimumFileAge применяется к сегментам файла, а не ко всему файлу.</td>
            <td>True или False</td>
            <td>Включите этот параметр, если рабочая нагрузка работает с большими, часто измененными файлами, в которых большая часть содержимого остается без изменений. Если этот параметр не включен, эти файлы никогда не будут оптимизированы, так как они изменяются, несмотря на то, что большая часть содержимого файла готова к оптимизации.</td>
        </tr>
        <tr>
            <td>Проверить</td>
            <td>При включении этого параметра, если хэш соответствует блоку, уже имеющемуся в хранилище блоков, блоки сравниваются по байтам для обеспечения их идентичности.</td>
            <td>True или False</td>
            <td>Эта функция проверки целостности гарантирует, что алгоритм хэширования, сравнивающий блоки данных, не совершит ошибку, сравнив два разных блока данных с одинаковым хэшем. На практике такой сценарий очень маловероятен. При включении функции проверки нагрузка задания оптимизации значительно повышается.</td>
        </tr>
    </tbody>
</table>

## <a id="modifying-dedup-system-settings"></a>Изменение параметров дедупликации данных на уровне системы
Дедупликация данных имеет дополнительные параметры уровня системы, которые можно настроить с помощью [реестра](https://technet.microsoft.com/library/cc755256(v=ws.11).aspx). Эти параметры применяются ко всем заданиям и томам, выполняемым в системе. При любом изменении реестра необходимо соблюдать осторожность.

Например, может потребоваться отключить полную сборку мусора. Дополнительные сведения о возможной пользе этих параметров для вашего сценария см. в разделе [Вопросы и ответы](#faq-why-disable-full-gc). Для изменения реестра с помощью PowerShell сделайте следующее:

* Если дедупликация данных выполняется в кластере:
    ```PowerShell
    Set-ItemProperty -Path HKLM:\System\CurrentControlSet\Services\ddpsvc\Settings -Name DeepGCInterval -Type DWord -Value 0xFFFFFFFF
    Set-ItemProperty -Path HKLM:\CLUSTER\Dedup -Name DeepGCInterval -Type DWord -Value 0xFFFFFFFF
    ```

* Если дедупликация данных не выполняется в кластере:
    ```PowerShell
    Set-ItemProperty -Path HKLM:\System\CurrentControlSet\Services\ddpsvc\Settings -Name DeepGCInterval -Type DWord -Value 0xFFFFFFFF
    ```

### <a id="modifying-dedup-system-settings-available-settings"></a>Доступные параметры уровня системы
<table>
    <thead>
        <tr>
            <th style="min-width:125px">Имя параметра</th>
            <th>Определение</th>
            <th>Допустимые значения</th>
            <th>Почему это значение следует изменить?</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>WlmMemoryOverPercentThreshold</td>
            <td>Этот параметр позволяет заданиям использовать больше памяти по сравнению с доступным объемом, оцененным заданиями дедупликации данных. Например, значение 300 означает, что для отмены задания понадобится в три раза больше назначенного объема памяти.</td>
            <td>Положительные целые числа (значение 300 означает 300 % или 3 раза)</td>
            <td>При наличии другого задания, которое остановится, если дедупликация данных использует больше ресурсов памяти</td>
        </tr>
        <tr>
            <td>DeepGCInterval</td>
            <td>Этот параметр настраивает интервал, через который обычное задание сборки мусора становится <a href="advanced-settings.md#faq-full-v-regular-gc" data-raw-source="[full Garbage Collection jobs](advanced-settings.md#faq-full-v-regular-gc)">заданием полной сборки мусора</a>. Значение n означает, что каждое n<sup>-ое</sup> задание было заданием полной сборки мусора. Обратите внимание: полная сборка мусора всегда отключена (независимо от значения реестра) для томов с <a href="understand.md#usage-type-backup" data-raw-source="[Backup Usage Type](understand.md#usage-type-backup)">архивным типом использования</a>. <code>Start-DedupJob -Type GarbageCollection -Full</code> может использоваться, если требуется полная сборка мусора на томе резервного копирования.</td>
            <td>Целые числа (–1 означает "отключено")</td>
            <td>См. <a href="advanced-settings.md#faq-why-disable-full-gc" data-raw-source="[this frequently asked question](advanced-settings.md#faq-why-disable-full-gc)">этот вопрос и ответ</a>.</td>
        </tr>
    </tbody>
</table>

## <a id="faq"></a>Часто задаваемые вопросы
<a id="faq-use-responsibly"></a>**Я изменил параметр дедупликации данных и теперь задания выполняются медленно или не завершаются или производительность рабочей нагрузки, уменьшилось. Почему?**  
Эти параметры предоставляют широкие возможности для управления выполнением дедупликации данных. Используйте их ответственно и [наблюдайте за производительностью](run.md#monitoring-dedup).

<a id="faq-running-dedup-jobs-manually"></a>**Я хочу выполнить задание дедупликации данных прямо сейчас, но я не хочу создать новое расписание — это сделать?**  
Да, [все задания можно выполнять вручную](run.md#running-dedup-jobs-manually).

<a id="faq-full-v-regular-gc"></a>**Какова разница между полной и обычной сбора мусора?**  
Существует два типа [сборки мусора](understand.md#job-info-gc):

- В *обычной сборке мусора* используется статистический алгоритм для поиска больших блоков без ссылок, соответствующих определенным критериям (малое использование памяти и низкий процент операций ввода-вывода в секунду). Обычная сборка мусора сжимает контейнер хранилища блоков, только если существует минимальный процент блоков без ссылок. Этот тип сборки мусора выполняется намного быстрее и использует меньше ресурсов, чем полная сборка мусора. В соответствии с расписанием по умолчанию задания обычной сборки мусора выполняются раз в неделю.
- *Полная сборка мусора* более эффективно справляется с поиском блоков без ссылок и освобождает больше места на диске. Полная сборка мусора сжимает каждый контейнер, даже если на отдельный блок в контейнере отсутствует ссылка. Она также освобождает место на диске, которое могло использоваться при аварийном завершении или сбое питания во время выполнения задания оптимизации. Задания полной сборки мусора приведут к восстановлению 100 % доступного места на дедуплицированном томе. Но для этого требуется больше времени и системных ресурсов по сравнению с заданием обычной сборки мусора. Как правило, задание полной сборки мусора находит и освобождает до 5 % больше данных, на которые нет ссылок, в отличие от задания обычной сборки мусора. В соответствии с расписанием по умолчанию полная сборка мусора выполняется каждый четвертый раз при планировании задания полной сборки мусора.

<a id="faq-why-disable-full-gc"></a>**Зачем отключить полную сборку мусора?**  
- Сборка мусора может негативно повлиять на теневые копии времени жизни тома и на размер добавочной архивации. В результате производительность рабочих нагрузок с высокой скоростью обновления данных или интенсивными операциями ввода-вывода может снизиться при выполнении заданий полной сборки мусора.           
- Задание полной сборки мусора можно выполнить вручную из PowerShell для устранения утечки в случае аварийного завершения системы.