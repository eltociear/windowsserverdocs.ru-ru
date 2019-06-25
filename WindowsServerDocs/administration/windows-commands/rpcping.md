---
title: rpcping
description: 'Раздел Windows команды для ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7382aa0d-90fc-47c0-84b3-15f52dd656d0
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a32f9c16c8c077942459599f2099a2d7e85a1397
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/31/2019
ms.locfileid: "66441691"
---
# <a name="rpcping"></a>rpcping

>Область применения. Windows Server (полугодовой канал), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Подтверждает возможность подключения RPC между компьютером с Microsoft Exchange Server и любой из поддерживаемых Microsoft Exchange клиентских рабочих станциях в сети. Эта служебная программа используется для проверки служб Microsoft Exchange Server, отвечают ли на запросы RPC из клиентских рабочих станциях в сети. 

## <a name="syntax"></a>Синтаксис
```
rpcping [/t <protseq>] [/s <server_addr>] [/e <endpoint>
        |/f <interface UUID>[,Majorver]] [/O <Interface Object UUID]
        [/i <#_iterations>] [/u <security_package_id>] [/a <authn_level>]
        [/N <server_princ_name>] [/I <auth_identity>] [/C <capabilities>]
        [/T <identity_tracking>] [/M <impersonation_type>]
        [/S <server_sid>] [/P <proxy_auth_identity>] [/F <RPCHTTP_flags>]
        [/H <RPC/HTTP_authn_schemes>] [/o <binding_options>]
        [/B <server_certificate_subject>] [/b] [/E] [/q] [/c]
        [/A <http_proxy_auth_identity>] [/U <HTTP_proxy_authn_schemes>]
        [/r <report_results_interval>] [/v <verbose_level>] [/d]
```

### <a name="parameters"></a>Параметры

|            Параметр             |                                                                                                                                                                                                                                                                                                                                               Описание                                                                                                                                                                                                                                                                                                                                               |
|----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|          /t \<protseq>           |                                                                                                                                                                                                                                                  Указывает используемый протокол последовательностью. Может принимать одно из стандартных последовательности протокола RPC, например: ncacn_ip_tcp ncacn_np, или переднего плана.<br /><br />Если не указан, значение по умолчанию — ncacn_ip_tcp.                                                                                                                                                                                                                                                   |
|        /s \<server_addr>         |                                                                                                                                                                                                                                                                                                            Указывает адрес сервера. Если не указан, будет отвечвают локального компьютера.                                                                                                                                                                                                                                                                                                            |
|          /e \<endpoint>          |                                                                                                                                                                                                                                                    Указывает конечную точку для проверки связи. Если ничего не указано, будет отвечвают конечных точек на конечном компьютере.<br /><br />Этот параметр является взаимоисключающим с интерфейсом ( **/f**) параметр.                                                                                                                                                                                                                                                     |
|      /o \<binding_options >       |                                                                                                                                                                                                                                                                                                                             Задает параметры привязки RPC ping.                                                                                                                                                                                                                                                                                                                             |
| /f \<интерфейс UUID > [, основная версия]  |                                                                                                            Задает интерфейс для проверки связи. Этот параметр является взаимоисключающим с параметром конечной точки. Интерфейс указываются в виде UUID.<br /><br />Если *Majorver* не указан, будет использоваться интерфейс версии 1.<br /><br />При указании интерфейс **rpcping** будет запрашивать конечных точек на конечном компьютере для получения конечной точки для указанного интерфейса. Сопоставитель конечных точек будет выполнять запросы параметров, заданных в командной строке.                                                                                                             |
|        /O \<UUID объекта >         |                                                                                                                                                                                                                                                                                                                       Указывает объект UUID, если интерфейс зарегистрирован одним.                                                                                                                                                                                                                                                                                                                        |
|        /i \<#_iterations>        |                                                                                                                                                                                                                                                                          Указывает количество вызовов, чтобы сделать. Значение по умолчанию — 1. Этот параметр полезен для измерения задержки подключения, если указаны несколько итераций.                                                                                                                                                                                                                                                                          |
|    /u \<security_package_id>     | Указывает пакет безопасности (security поставщик) RPC будет использоваться для вызова. Пакет безопасности определяется как число или имя. Если используется номер, это тот же номер, как и в API RpcBindingSetAuthInfoEx завершился сбоем. В следующем списке перечислены имена и номера. Имена не чувствительны к регистру:<br /><br />— Negotiate / 9, или один из nego snego или negotiate<br />-NTLM / 10 или NTLM<br />-SChannel / 14 или SChannel<br />-Kerberos / 16 или Kerberos<br />-Kernel / 20 или ядра<br />    При использовании этого параметра необходимо указать уровень проверки подлинности, отличный от none. По умолчанию для этого параметра отсутствует. Если он не указан, RPC не будет использоваться защита для проверки связи. |
|        /a \<authn_level>         |                                                                                                                                                               Указывает уровень проверки подлинности для использования. Возможные значения:<br /><br />-подключение<br />-вызов<br />-pkt<br />— целостность<br />-конфиденциальности<br /><br />Если этот параметр указан, идентификатор безопасности пакета (/ u) также должен быть указан. По умолчанию для этого параметра отсутствует.<br /><br />Если этот параметр не указан, RPC не будет использоваться защита для проверки связи.                                                                                                                                                               |
|     /N \<server_princ_name >      |                                                                                                                                                                                                                                                                                 Указывает имя сервера-участника.<br /><br />Это поле может использоваться только когда выбраны пакет проверки подлинности уровня и безопасности.                                                                                                                                                                                                                                                                                  |
|       /I \<auth_identity>        |                                                         Можно указать другое удостоверение для подключения к серверу. Удостоверение находится в форме пользователя, домен, пароль. Если имя пользователя, домена или пароль имеют специальные символы, которые могут обрабатываться оболочкой, заключите идентификатор в двойные кавычки. Можно указать **\\** \* вместо пароля и RPC предложит ввести пароль без отправки его на экране. Если это поле не указано, будет использоваться удостоверение пользователя, вошедшего в систему.<br /><br />Это поле может использоваться только когда выбраны пакет проверки подлинности уровня и безопасности.                                                         |
|        /C \<возможности >        |                                                                                                                                                                                                                                                                                   Задает шестнадцатеричное битовую маску, флагов. Это поле может использоваться только когда выбраны пакет проверки подлинности уровня и безопасности.                                                                                                                                                                                                                                                                                    |
|     /T \<identity_tracking>      |                                                                                                                                                                                                                                                               Указывает статический или динамический. Если не задано, динамическое значение по умолчанию.<br /><br />Это поле может использоваться только когда выбраны пакет проверки подлинности уровня и безопасности.                                                                                                                                                                                                                                                                |
|     /M \<impersonation_type>     |                                                                                                                                                                                                                                                           Задает анонимный доступ, идентификации, олицетворения или делегирования. По умолчанию олицетворение.<br /><br />Это поле может использоваться только когда выбраны пакет проверки подлинности уровня и безопасности.                                                                                                                                                                                                                                                           |
|         /S \<server_sid>         |                                                                                                                                                                                                                                                                              Указывает ожидаемый идентификатор SID сервера.<br /><br />Это поле может использоваться только когда выбраны пакет проверки подлинности уровня и безопасности.                                                                                                                                                                                                                                                                              |
|    /P \<proxy_auth_identity>     |                                                                                                                                                                                                                              Задает удостоверение для проверки подлинности на прокси-сервер RPC/HTTP. Имеет тот же формат, что и для параметра/i. Необходимо указать пакет безопасности (/ u), уровень проверки подлинности (/) и схемы проверки подлинности (/ H) для использования этого варианта.                                                                                                                                                                                                                               |
|       /F \<RPCHTTP_flags>        |                                                                                                                                                                Задает флаги для передачи для проверки подлинности внешнего интерфейса RPC/HTTP. Флаги могут быть указаны как числа или имена, которые являются распознанный флаги:<br /><br />— Используйте SSL / 1 или ssl или use_ssl<br />-Используется первая схема проверки подлинности / 2 или первым, или use_first<br /><br />Необходимо указать пакет безопасности (/ u) и уровень проверки подлинности (/) для использования этого варианта.                                                                                                                                                                 |
|   /H \<RPC/HTTP_authn_schemes>   |                                                                                                                           Указывает схемы проверки подлинности для проверки подлинности внешнего интерфейса RPC/HTTP. Этот параметр является список числовых значений или имен, разделенных запятыми. Пример. Basic, NTLM. Допустимые значения: (именах не учитывается регистр):<br /><br />— Базовый / 1 "или" базовый<br />-NTLM / 2 или NTLM<br />— Сертификат / 65536 или Cert<br /><br />Необходимо указать пакет безопасности (/ u) и уровень проверки подлинности (/) для использования этого варианта.                                                                                                                            |
| /B \<server_certificate_subject> |                                                                                                                                                                                                                                                    Указывает субъект сертификата сервера. Для работы, необходимо использовать SSL для этого параметра.<br /><br />Необходимо указать пакет безопасности (/ u) и уровень проверки подлинности (/) для использования этого варианта.                                                                                                                                                                                                                                                     |
|                /b                |                                                                                                                                                                                      Получает субъект сертификата сервера из сертификат, отправленный сервером и его вывод экрана или файл журнала. Является допустимым, только в том случае, если прокси-сервер echo только параметр (/ E) и указываются параметры использования SSL.<br /><br />Необходимо указать пакет безопасности (/ u) и уровень проверки подлинности (/) для использования этого варианта.                                                                                                                                                                                      |
|                /R                |                                                                                                                                                               Задает HTTP-прокси. Если *none*, используется прокси-сервер RPC. Значение *по умолчанию* означает использование параметров IE в клиентском компьютере. Любое другое значение будет рассматриваться как HTTP-прокси явным. Если этот флаг не указан, предполагается значение по умолчанию, то есть проверяются настройках IE. Этот флаг доступен, только если **/E** установлен флаг (только для проверки связи).                                                                                                                                                                |
|                /E                |                                                                                                                                                     Ограничивает запрос проверки связи только прокси RPC/HTTP. Проверка связи не достигает сервера. Это удобно при попытке установления, доступен ли прокси-сервер RPC/HTTP. Чтобы указать прокси-сервер HTTP, используйте флаг /R. Если прокси-сервер HTTP задан в флаг/o, этот параметр будет игнорироваться.<br /><br />Необходимо указать пакет безопасности (/ u) и уровень проверки подлинности (/) для использования этого варианта.                                                                                                                                                      |
|                /q                |                                                                                                                                                                                                                                                                                 Задает тихий режим. Не выдает никаких запросов, за исключением паролей. Предполагается, что *Y* ответ на все запросы. Этот параметр следует используйте с осторожностью.                                                                                                                                                                                                                                                                                  |
|                /c                |                                                                                                                                                                                                                                                                                                               Используйте сертификат смарт-карты. RPCPing предложит пользователю выбирать смарт-карты.                                                                                                                                                                                                                                                                                                                |
|                /A                |                                                                                                                                                                                                                        Задает удостоверение, с которым для проверки подлинности на прокси-сервер HTTP. Имеет тот же формат, что и для параметра/i.<br /><br />Необходимо указать схемы проверки подлинности (/ U), пакет безопасности (/ u) и уровень проверки подлинности (/) для использования этого варианта.                                                                                                                                                                                                                         |
|                /U                |                                                                                                                                                  Указывает схемы проверки подлинности для проверки подлинности прокси-сервера HTTP. Этот параметр является список числовых значений или имен, разделенных запятыми. Пример. Basic, NTLM. Допустимые значения: (именах не учитывается регистр):<br /><br />— Базовый / 1 "или" базовый<br />-NTLM / 2 или NTLM<br /><br />Необходимо указать пакет безопасности (/ u) и уровень проверки подлинности (/) для использования этого варианта.                                                                                                                                                  |
|                /r                |                                                                                                                                                                                                                                             Если указаны несколько итераций, этот параметр сделает **rpcping** отображения текущая статистика выполнения периодически вместо этого после последнего вызова. Интервал отчета задается в секундах. Значение по умолчанию — 15.                                                                                                                                                                                                                                              |
|                /v                |                                                                                                                                                                                                                                                                                           Сообщает **rpcping** как verbose, чтобы выходные данные. Значение по умолчанию — 1. 2 и 3 полученным дополнительные **rpcping**.                                                                                                                                                                                                                                                                                           |
|                /d                |                                                                                                                                                                                                                                                                                                                                   Запуск RPC сетевой диагностики пользовательского интерфейса.                                                                                                                                                                                                                                                                                                                                   |
|                /p                |                                                                                                                                                                                                                                                                                                                      Задает для запроса учетных данных при сбое проверки подлинности.                                                                                                                                                                                                                                                                                                                       |
|                /?                |                                                                                                                                                                                                                                                                                                                                  Отображение справки в командной строке.                                                                                                                                                                                                                                                                                                                                   |

## <a name="BKMK_Examples"></a>Примеры
Чтобы определить, доступен ли сервер Exchange, подключаться через RPC/HTTP, введите следующую команду:
```
rpcping /t ncacn_http /s exchange_server /o RpcProxy=front_end_proxy /P "username,domain,*" /H Basic /u NTLM /a connect /F 3
```

## <a name="additional-references"></a>Дополнительная справка
-   [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)