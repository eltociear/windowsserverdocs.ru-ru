---
title: Сообщения служб WSUS и советы по диагностике
description: Раздел по службам Windows Server Update Service (WSUS) — устранение неполадок с помощью сообщений WSUS
ms.prod: windows-server
ms.technology: manage-wsus
ms.topic: article
ms.assetid: 9f6317f7-bfe0-42d9-87ce-d8f038c728ca
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e4fe14eeaba3fc82e125288f8c47fb445f6e00b0
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/08/2020
ms.locfileid: "80828317"
---
# <a name="wsus-messages-and-troubleshooting-tips"></a>Сообщения служб WSUS и советы по диагностике

>Область применения: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

В этом разделе содержатся сведения о следующих сообщениях WSUS:

-   Компьютер не сообщил о состоянии

-   Идентификатор сообщения 6703 — сбой синхронизации WSUS

-   Ошибка 0x80070643: Неустранимая ошибка во время установки

-   Некоторые службы не работают. Проверьте следующие службы [...]

## <a name="computer-has-not-reported-status"></a>Компьютер не сообщил о состоянии
Это сообщение создается в консоли WSUS, когда клиентский компьютер WSUS не отправляет сведения на сервер WSUS для указания его текущего состояния обновления. Эта проблема обычно вызвана клиентским компьютером WSUS, а не сервером WSUS.

Наиболее распространенные причины:

-   Компьютер потерял подключение к сети:
    -   Сетевой кабель не подключен.
    -   Неисправность промежуточного сетевого кабеля.
    -   Компьютер имеет неисправный сетевой адаптер.
    -   Сетевой порт, к которому подключается компьютер, был отключен.
    -   Адаптеру беспроводной сети не удается сопоставить и подключиться к корпоративной точке доступа к беспроводной сети.
-   Компьютер отключен. (Она была выключена или находится в спящем режиме или режим гибернации.)

## <a name="message-id-6703---wsus-synchronization-failed"></a>Идентификатор сообщения 6703 — сбой синхронизации WSUS
> Сообщение: запрос завершился ошибкой с кодом состояния HTTP 503: служба недоступна.
> 
> Источник: Microsoft. UpdateServices. Administration. Админпрокси. Креатеупдатесервер.

При попытке открыть службы обновления на сервере WSUS появляется следующее сообщение об ошибке:

> Ошибка: ошибка подключения
> 
> При попытке подключения к серверу WSUS произошла ошибка. Эта ошибка может возникать по ряду причин. Если проблема не исчезнет, обратитесь к сетевому администратору. Щелкните узел сервера сброса, чтобы снова подключиться к серверу.

В дополнение к приведенному выше, пытается получить доступ к URL-адресу сайта администрирования WSUS (т. е. `http://CM12CAS:8530`) завершается с ошибкой:

> Ошибка HTTP 503. Служба недоступна

В этом случае наиболее вероятной причиной является то, что пул приложений WsusPool в IIS находится в остановленном состоянии.

Кроме того, для пула приложений, вероятно, установлено значение по умолчанию 1843200 КБ (в КБ). При возникновении этой проблемы увеличьте предельный объем выделенной памяти до 4 ГБ (4000000 КБ) и перезапустите пул приложений. Чтобы увеличить лимит выделенной памяти, выберите пул приложений WsusPool и щелкните Дополнительные параметры в разделе Изменение пула приложений. Затем установите ограничение для закрытой памяти 4 ГБ (4000000 КБ). После перезапуска пула приложений Отслеживайте ошибки в SMS_WSUS_SYNC_MANAGER состояние компонента, WCM. log и файл wsyncmgr. log. Обратите внимание, что может потребоваться увеличить предельный объем выделенной памяти до 8 ГБ (8000000 КБ) или выше в зависимости от среды.

Дополнительные сведения см. в статье [сбой синхронизации WSUS в ConfigMgr 2012 с ошибками HTTP 503](https://blogs.technet.com/b/sus/archive/2015/03/23/configmgr-2012-support-tip-wsus-sync-fails-with-http-503-errors.aspx) .

## <a name="error-0x80070643-fatal-error-during-installation"></a>Ошибка 0x80070643: Неустранимая ошибка во время установки
Программа установки WSUS использует Microsoft SQL Server для выполнения установки. Эта проблема возникает из-за того, что пользователь, запускающий программу установки WSUS, не имеет разрешений системного администратора в SQL Server.

Чтобы устранить эту проблему, предоставьте системному администратору разрешения на учетную запись пользователя или учетную запись группы в SQL Server, а затем снова запустите программу установки служб WSUS.

## <a name="some-services-are-not-running-check-the-following-services"></a>Некоторые службы не работают. Проверьте следующие службы:

- **Selfupdate:** Дополнительные сведения об устранении неполадок службы selfupdate см. в статье [Автоматическое обновление необходимо обновить](https://technet.microsoft.com/library/cc708554(v=ws.10).aspx) .

- **Вссусервице. exe:** Эта служба упрощает синхронизацию. При возникновении проблем с синхронизацией откройте WSUSService. exe, нажав кнопку **Пуск**, выбрав пункты **Администрирование**, **службы**и найти **службу обновления Windows Server** в списке служб. Выполните следующие действия.
    
    -   Убедитесь, что служба запущена. Нажмите кнопку **запустить** , если она остановлена или **перезапущена** , чтобы обновить службу.
    
    -   Используйте Просмотр событий, чтобы проверить наличие событий, которые могут указывать на проблему, в журналах событий **приложения**, **Безопасность**y и **системных** событиях.
    
    -   Можно также проверить журнал SoftwareDistribution. log, чтобы узнать, есть ли события, которые могут указывать на проблему.

- **Веб-служба сервицесскл:** Веб-службы размещаются в службах IIS. Если они не запущены, убедитесь, что службы IIS запущены (или запущены). Можно также попробовать сбросить веб-службу, введя команду **iisreset** в командной строке.

- **Служба SQL:** Для каждой службы, кроме службы selfupdate, требуется, чтобы была запущена служба SQL. Если в любом из файлов журнала указываются проблемы с подключением к SQL, сначала проверьте службу SQL. Чтобы получить доступ к службе SQL, нажмите кнопку **Пуск**, укажите пункт **Администрирование**, выберите пункт **службы**, а затем найдите один из следующих элементов:
    
  - **MSSQLSERver** (если используется WMSDE или MSDE или используется SQL Server и в качестве имени экземпляра используется имя экземпляра по умолчанию);
    
  - **MSSQL $ WSUS** (если вы используете базу данных SQL Server и имеет имя экземпляра базы данных WSUS)
    
    Щелкните службу правой кнопкой мыши и выберите пункт **запустить** , если служба не запущена, или **перезапустите** , чтобы обновить службу, если она запущена.
