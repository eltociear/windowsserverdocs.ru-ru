---
title: Настройка учета сервера политики сети
description: Этот раздел посвящен текстовый файл и ведения журнала для сервера политики сети в Windows Server 2016 SQL Server.
manager: dougkim
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: dfde2e21-f3d5-41e8-8492-cb3f0d028afb
ms.author: pashort
author: shortpatti
ms.date: 05/25/2018
ms.openlocfilehash: c732a9f42d942ad579468d1dd15d30324d6fea87
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2019
ms.locfileid: "59839705"
---
# <a name="configure-network-policy-server-accounting"></a>Настройка учета сервера политики сети

Существует три типа ведения журнала для сервера политики сети \(NPS\):

- **Ведение журнала событий**. Используется главным образом для аудита и устранение неполадок попытки подключения. Вы можете настроить ведение журнала путем получения свойства сервера политики сети в консоли сервера политики сети событий NPS.

- **Ведение журнала запросов учета и проверки подлинности пользователя в локальный файл**. Используется главным образом для подключения анализа и выставления счетов. Также полезен в качестве средства анализа системы безопасности, так как он предоставляет способ отслеживания действий пользователь-злоумышленник после атаки. Вы можете настроить локальный файл ведения журнала с помощью мастера настройки учета.

- **Ведение журнала пользователя и соответствующих запросов к базе данных Microsoft SQL Server совместимый с XML**. Используется, чтобы разрешить нескольким серверам под управлением NPS так, чтобы иметь один источник данных. Также предоставляет преимущества использования реляционной базы данных. Ведение журнала SQL Server можно настроить с помощью мастера настройки учета.

## <a name="use-the-accounting-configuration-wizard"></a>С помощью мастера настройки учета

С помощью мастера настройки учета, можно настроить четыре параметра учета:

- **Только ведения журнала SQL**. При использовании этого параметра, можно настроить канала передачи данных для SQL Server, который позволяет сервера политики сети для подключения к и передачу данных учета SQL server. Кроме того мастер можно настроить базу данных на сервере SQL Server, чтобы убедиться, что база данных совместима с ведения журнала сервера NPS на SQL Server.
- **Текст вход в систему**. При использовании этого параметра, можно сконфигурировать NPS журнала данных учета в текстовый файл.
- **Параллельная регистрация**. При использовании этого параметра, можно настроить связь данных SQL Server и базы данных. Можно также настроить журнал файла текста, так что NPS записывает одновременно в текстовом файле и базы данных SQL Server. 
- **Ведение журнала SQL с помощью резервной копии**. При использовании этого параметра, можно настроить связь данных SQL Server и базы данных. Кроме того можно настроить текст файла ведение журнала при сбое ведения журнала SQL Server.

Помимо этих параметров ведения текстового журнала и ведения журнала SQL Server позволяют пользователю указать ли NPS продолжает обрабатывать запросы на подключение при сбое ведения журнала. Это можно указать в **ведение журнала раздел действия сбоя** свойств ведения журнала локальный файл, в свойства ведения журнала сервера SQL, а также при запуске мастера настройки учета.

### <a name="to-run-the-accounting-configuration-wizard"></a>Для запуска мастера настройки учета

Чтобы запустить мастер настройки учета, выполните следующие действия:

1. Откройте консоль сервера политики сети или оснастку сервера политики сети консоли управления (MMC).
2. В дереве консоли щелкните **учет**.
3. В области сведений в **учет**, нажмите кнопку **Настройка учета**.

## <a name="configure-nps-log-file-properties"></a>Настройка свойств файла журнала сервера политики сети

Можно настроить сервер политики сети (NPS) для выполнения удаленного Authentication Dial-In User Service (RADIUS) учета для запросов проверки подлинности, сообщения предоставления, запрещения доступа, запросы и ответы учета и периодические обновления состояния. Эта процедура позволяет настроить файлы журналов, в которых вы хотите сохранить учетные данные.

Дополнительные сведения об интерпретации файлов журнала см. в разделе [интерпретировать NPS базы данных файлы журнала в формате](https://technet.microsoft.com/library/cc771748.aspx).

Чтобы предотвратить заполнение жестком диске файлы журналов, настоятельно рекомендуется оставить их в раздел, который отделен от системного раздела. Ниже приведены дополнительные сведения о настройке учетных данных для сервера политики сети:

- Чтобы отправить данные файла журнала для коллекции с помощью другого процесса, можно настроить таким Образом, записываемый в именованном канале. Чтобы использовать именованные каналы, задайте папку файла журнала \\. \pipe или \\ComputerName\pipe. Программа server именованного канала создает именованный канал называется \\.\pipe\iaslog.log для приема данных. В диалоговом окне локального файла свойств в создать новый файл журнала, выберите никогда не (размер файла не ограничен) при использовании именованных каналов.

- Каталог файлов журнала могут создаваться с помощью системных переменных среды (вместо переменных пользователя), например % systemdrive %, % systemroot % и % windir %. Например, следующие пути, используя переменная среды % windir %, находит файл журнала в системном каталоге во вложенной папке \System32\Logs (то есть %windir%\System32\Logs\).

- Изменение форматов файла журнала не приводит должен быть создан новый журнал. При изменении формата файла журнала, который активен во время изменения файла будет содержать оба формата (записи в начале журнала будут иметь старый формат и записи в конец журнала, будут иметь новый формат).

- Если RADIUS-учет завершается сбоем из-за заполнением жесткого диска или по другим причинам, сервер политики сети прекращает обработку запросов на подключение, позволяет пользователям получить доступ к сетевым ресурсам.

- Сервер политики сети обеспечивает возможность подключения к базе данных Microsoft® SQL Server™ в дополнение или вместо ведения журнала в локальный файл.

Членство в группе **"Администраторы домена"** группе является минимальным требованием для выполнения этой процедуры.


### <a name="to-configure-nps-log-file-properties"></a>Чтобы настроить свойства файла журнала сервера политики сети

1. Откройте консоль сервера политики сети или оснастку сервера политики сети консоли управления (MMC).
2. В дереве консоли щелкните **учет**.
3. В области сведений в **свойства файла журнала**, нажмите кнопку **изменить свойства файла журнала**. **Свойства файла журнала** откроется диалоговое окно.
4. В **свойства файла журнала**на **параметры** на вкладке **записывать следующие сведения**, убедитесь, что вы решили журнала достаточно информации, чтобы заносить. Например если журналов требуется корреляция сеансов, установите все флажки.
5. В **ведение журнала действие при ошибке**выберите **при сбое ведения журнала, отклонять запросы на подключение** освобождать для остановки обработки сообщения запроса доступа, если файлы журнала полный или недоступны по некоторым причинам. Если требуется, чтобы сервер политики сети, чтобы продолжить обработку запросов на подключение при сбое ведения журнала, не устанавливайте этот флажок.
6. В **свойства файла журнала** диалоговом окне щелкните **файл журнала** вкладки.
7. На **файл журнала** на вкладке **Directory**, введите расположение, где будут храниться файлы журналов сервера политики сети. Расположение по умолчанию является папкой systemroot\System32\LogFiles.<br>Если не указать полный путь к инструкции в **каталог файла журнала**, используется путь по умолчанию. Например, если ввести **NPSLogFile** в **каталог файла журнала**, этот файл расположен в % systemroot%\System32\NPSLogFile.
8. В **формат**, нажмите кнопку **DTS-совместимый**. При желании можно вместо этого выбрать устаревший формат файла, такие как **ODBC \(устаревших\)**  или **IAS \(устаревших\)**.<br>**ODBC** и **IAS** типы устаревших файлов содержат подмножество информации, которую NPS отправляет его базу данных SQL Server. **DTS-совместимый** тип файла XML формат идентичен формату XML, сервер политики сети использует для импорта данных в базе данных SQL Server. Таким образом **DTS-совместимый** формат файла предоставляет более эффективный и завершения передачи данных в базу данных SQL Server standard для сервера политики сети.
9. В **создать новый файл журнала**, чтобы настроить сервер политики сети, новые файлы журнала через заданные интервалы времени, выберите пункт интервала, который вы хотите использовать:
    - Если объем транзакций и ведение журнала, выберите **ежедневного**.
    - Для меньших объемах транзакций и ведение журнала, нажмите кнопку **еженедельно** или **ежемесячные**.
    - Для хранения всех транзакций в один файл журнала, нажмите кнопку **никогда \(граниченный размер файла\)**.
    - Чтобы ограничить размер каждого файла журнала, щелкните **этот размер, при достижении файлом журнала**, а затем введите размер файла, после чего создается новый журнал. Размер по умолчанию — 10 мегабайт (МБ).
10. Если требуется, чтобы сервер политики сети, удалите старые файлы журнала, чтобы создать место на диске для новых файлов журнала при жестком диске недостаточно места для, убедитесь, что **при диск заполнен, удалите старые файлы журнала** выбран. Этот параметр недоступен, тем не менее, если значение **создать новый файл журнала** — **никогда \(граниченный размер файла\)**. Кроме того Если старый файл журнала является текущий файл журнала, он не удаляется.

## <a name="configure-nps-sql-server-logging"></a>Настройка ведения журнала сервера NPS на SQL Server

Можно использовать следующую процедуру для журнала данных учета RADIUS в локальном или удаленном базу данных под управлением Microsoft SQL Server.

>[!NOTE]
>NPS форматирует данные бухгалтерской программы в виде XML-документа, который отправляется **report_event** хранимой процедуры в базе данных SQL Server, в указанную папку на сервере политики сети. Для ведения журнала для правильного функционирования SQL Server, необходимо иметь хранимую процедуру с именем **report_event** в базе данных SQL Server, можно получать и анализировать XML-документов от сервера политики сети.

Минимальным требованием для выполнения этой процедуры является членство в группе "Администраторы домена" или наличие эквивалентных прав.

### <a name="to-configure-sql-server-logging-in-nps"></a>Настройка SQL Server, ведение журнала на сервере политики сети

1. Откройте консоль сервера политики сети или оснастку сервера политики сети консоли управления (MMC).
2. В дереве консоли щелкните **учет**.
3. В области сведений в **свойства ведения журнала SQL Server**, нажмите кнопку **изменить свойства ведения журнала сервера SQL**. **Свойства ведения журнала SQL Server** откроется диалоговое окно.
4. В **записывать следующие сведения**, выберите сведения, которые будут использоваться для входа: 
    - Чтобы регистрировать все запросы учета, нажмите кнопку **запросов учета**.
    - В журнал запросов проверки подлинности, нажмите кнопку **запросы на проверку подлинности**.
    - Чтобы протоколировать состояние периодического учета, нажмите кнопку **состояние периодического учета**.
    - Чтобы записывать промежуточное состояние, например промежуточные запросы учета, нажмите кнопку **промежуточное состояние**.
5. Чтобы настроить количество одновременных сеансов между сервером политики сети и SQL Server, введите число в **максимальное число одновременных сеансов**.
6. Для настройки источника данных SQL Server, в **ведения журнала SQL Server**, нажмите кнопку **Настройка**. **Свойства канала передачи данных** откроется диалоговое окно. На **подключения** вкладке, укажите следующее: 
    - Чтобы указать имя сервера, на котором хранится база данных, введите или выберите имя в **выберите или введите имя сервера**.
    - Чтобы указать метод проверки подлинности, используемый для подключения к серверу, щелкните **встроенные средства безопасности Windows NT используйте**. Или щелкните **использовать указанные имя пользователя и пароль**, а затем введите учетные данные в **имя пользователя** и **пароль**.
    - Чтобы разрешить пустой пароль, выберите **пустой пароль**.
    - Чтобы сохранить пароль, щелкните **Разрешить сохранение пароля**.
    - Чтобы указать, какую базу данных для подключения к на компьютере под управлением SQL Server, щелкните **выберите базу данных на сервере**, а затем выберите имя базы данных из списка.
7. Чтобы проверить подключение между NPS и SQL Server, нажмите кнопку **проверить подключение**. Нажмите кнопку **ОК** закрыть **свойства канала передачи данных**.
8. В **ведение журнала действие при ошибке**выберите **Включение ведения журнала файла текста для отработки отказа** Если необходимо, чтобы сервер политики сети, чтобы продолжить работу с помощью текстового файла ведения журнала при сбое ведения журнала SQL Server. 
9. В **ведение журнала действие при ошибке**выберите **при сбое ведения журнала, отклонять запросы на подключение** освобождать для остановки обработки сообщения запроса доступа, если файлы журнала полный или недоступны по некоторым причинам. Если требуется, чтобы сервер политики сети, чтобы продолжить обработку запросов на подключение при сбое ведения журнала, не устанавливайте этот флажок.

## <a name="ping-user-name"></a>Имя пользователя ping

Некоторые прокси-серверы RADIUS и серверы доступа к сети периодически отправлять запросы проверки подлинности и учета на (известный как запросы проверки связи) и убедитесь, что сервер политики сети в сети. Эти запросы проверки связи содержатся вымышленные имена пользователей. Когда NPS обрабатывает эти запросы, журналы событий и учета заполняется записи отклонения доступа, что усложняет для отслеживания записи.

При настройке записи реестра для **ping имя_пользователя**, NPS совпадает значения записи реестра значение имени пользователя в запросы проверки связи с другими серверами. Объект **ping имя_пользователя** запись реестра указывает вымышленное имя пользователя (или шаблон имени пользователя, с переменными, который соответствует вымышленное имя пользователя), отправляемые функциями прокси-серверы RADIUS и серверы доступа к сети. Когда служба NPS получит запросы проверки связи, которые соответствуют **ping имя_пользователя** значение записи реестра, сервер политики сети отклоняет запросы проверки подлинности без обработки запроса. Сервер политики сети не будет записывать транзакций, относящихся к вымышленное имя пользователя во всех файлах журнала, что облегчает интерпретировать в журнал событий.

**Проверьте связь с имя_пользователя** не устанавливается по умолчанию. Необходимо добавить **ping имя_пользователя** в реестр. Можно добавить запись в реестр с помощью редактора реестра.

>[!CAUTION]
>Внесение в реестр неправильных изменений может привести к серьезным повреждениям системы. Перед внесением изменений следует сделать резервную копию всех ценных данных на компьютере.

### <a name="to-add-ping-user-name-to-the-registry"></a>Чтобы добавить имя пользователя ping в реестр

Имя пользователя ping могут добавляться к следующему разделу реестра как строковое значение, является членом локальной группы администраторов:

`HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\IAS\Parameters`

- **Имя**: `ping user-name`
- **Тип**: `REG_SZ`
- **Данные**:  *Имя пользователя*

>[!TIP]
>Чтобы указать более одного имени пользователя для **проверить связь с имени пользователя** значение, введите шаблон имени, например DNS-имя, включая подстановочные знаки в **данных**.