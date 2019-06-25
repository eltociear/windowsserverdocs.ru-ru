---
title: Параметры реестра Layer Security (TLS) транспорта
description: Безопасность Windows Server
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-tls-ssl
ms.tgt_pltfrm: na
ms.topic: article
author: justinha
ms.author: justinha
manager: brianlic-msft
ms.date: 02/28/2019
ms.openlocfilehash: 32068319aae7545675e126eed6e1ab4c914bcbcf
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/07/2019
ms.locfileid: "66812637"
---
# <a name="transport-layer-security-tls-registry-settings"></a>Параметры реестра Layer Security (TLS) транспорта

>Относится к: Windows Server (полугодовой канал), Windows Server 2019 г., Windows Server 2016, Windows 10

В этом справочном разделе для ИТ-специалистов содержит сведения о параметрах реестра, поддерживаемых для реализации Windows протокол безопасности транспортного уровня (TLS) и протокол Secure Sockets Layer (SSL), благодаря поддержке безопасности Schannel Provider (SSP). Разделы и подразделы реестра в разделе справки можно администрировать и устранять неполадки Schannel SSP, а именно протоколов TLS и SSL. 

> [!CAUTION]
> Эти сведения предоставляются в виде справочника для использования при устранении неполадок или проверки правильности применения нужных параметров.
> Рекомендуется не изменять реестр напрямую, если есть другие возможности.
> Изменения в реестре не проверяются редактором реестра или операционной системой Windows перед их применением.
> В результате могут сохраниться неверные значения, что приведет к неустранимым ошибкам в системе.
> По возможности вместо редактирования реестра напрямую используйте групповую политику или другие средства Windows, например консоль управления (MMC) для выполнения задач.
> Если отредактировать реестр все же необходимо, соблюдайте крайнюю осторожность.

## <a name="certificatemappingmethods"></a>CertificateMappingMethods 

Эта запись не существует в реестре по умолчанию. Значение по умолчанию — что поддерживаются все четыре метода сопоставления сертификатов, перечисленные ниже.

Если серверное приложение требует проверки подлинности клиента, Schannel автоматически пытается сопоставить сертификат, предоставленный клиентским компьютером, с учетной записью пользователя. Вы можете проверять подлинность пользователей, выполняющих вход с сертификатом клиента, создавая сопоставления, связывающие данные сведения с учетной записью пользователя Windows. После создания и включения сопоставления сертификатов каждый раз, когда клиент предоставляет сертификат клиента, серверное приложение автоматически сопоставляет этого пользователя с соответствующей учетной записью Windows.

В большинстве случаев сертификат сопоставляется с учетной записью пользователя одним из двух следующих способов. 

- Один сертификат сопоставляется с одной учетной записью пользователя (сопоставление "один к одному").
- Несколько сертификатов сопоставляются с одной учетной записью пользователя (сопоставление "многие к одному").

По умолчанию поставщик Schannel будет использовать следующие четыре метода сопоставления сертификатов, перечисленные в порядке приоритета.

1. Сопоставление сертификатов "служба для пользователя" (S4U) Kerberos.
2. Сопоставление имени участника-пользователя.
3. Сопоставление "один к одному" (также называемое сопоставлением "субъект/поставщик").
4. Сопоставление "многие к одному".

Применимые версии: указаны в списке **Область применения** в начале этой статьи.

Путь реестра: HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL

## <a name="ciphers"></a>Ciphers

Шифры TLS/SSL необходимо контролировать, настроив порядок комплектов шифров. Дополнительные сведения см. в разделе [Настройка порядок комплектов шифров TLS](manage-tls.md#configuring-tls-cipher-suite-order).

Сведения о порядок наборов шифров по умолчанию, которые используются Schannel SSP, см. в разделе [шифров TLS/SSL (Schannel SSP)](https://msdn.microsoft.com/library/windows/desktop/aa374757.aspx). 

## <a name="ciphersuites"></a>CipherSuites

Настройка шифров TLS/SSL должно выполняться с помощью групповой политики, MDM или PowerShell, см. в разделе [Настройка порядок комплектов шифров TLS](manage-tls.md#configuring-tls-cipher-suite-order) подробные сведения.

Сведения о порядок наборов шифров по умолчанию, которые используются Schannel SSP, см. в разделе [шифров TLS/SSL (Schannel SSP)](https://msdn.microsoft.com/library/windows/desktop/aa374757.aspx). 


## <a name="clientcachetime"></a>ClientCacheTime

Эта запись определяет время в миллисекундах, через которое в операционной системе истекает срок действия записей кэша на стороне клиента. Значение 0 отключает кэширование безопасного подключения. Эта запись не существует в реестре по умолчанию. 

При первом подключении клиента к серверу через Schannel SSP выполняется полное подтверждение TLS/SSL. После завершения главная копия секрета, комплект шифров и сертификаты хранятся в кэше сеанса на соответствующем клиенте и сервере.

Начиная с Windows Server 2008 и Windows Vista, время кэша клиента по умолчанию — 10 часов.

Путь реестра: HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL

Время кэша клиента по умолчанию

## <a name="enableocspstaplingforsni"></a>EnableOcspStaplingForSni

Online сшивание протокола состояния сертификатов (OCSP) позволяет веб-сервер, таких как Internet Information Services (IIS), для предоставления текущее состояние отзыва сертификата сервера при отправке сертификата сервера на клиент во время подтверждения TLS. Эта функция сокращает нагрузку на серверы OCSP, так как веб-сервер может кэшировать текущее состояние OCSP сертификата сервера и отправить его для нескольких веб-клиентов. Без этой функции каждого веб-клиент попытается получить текущее состояние OCSP сертификат сервера с сервера OCSP. Это вызовет с высокой нагрузкой на этом сервере OCSP. 

Помимо служб IIS веб-служб через http.sys можно также использовать этот параметр, в том числе служб федерации Active Directory (AD FS) и прокси-сервера приложений Web (WAP). 

По умолчанию для веб-сайтов IIS, который имеет простой безопасной привязки (SSL/TLS) включена поддержка OCSP. Однако эта поддержка не включена по умолчанию, если веб-сайт IIS использует одно или оба из следующих типов безопасных привязок (SSL/TLS):
- Требовать Указание имени сервера
- Использовать централизованное хранилище сертификатов

В этом случае ответ hello сервера во время подтверждения TLS не войдут в состоянии OCSP прошит по умолчанию. Это повышает производительность: Реализация сшивания Windows OCSP может масштабироваться до сотен сертификатов сервера. Так как SNI, так и CCS включить IIS для масштабирования до тысяч веб-сайты, потенциально имеете дело с тысячами сертификатов сервера, настройка это поведение включено по умолчанию может вызвать проблемы с производительностью.

Применимые версии: Все версии, начиная с Windows Server 2012 и Windows 8. 

Путь реестра: [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL]

Добавьте следующий раздел:

"EnableOcspStaplingForSni"=dword:00000001

Чтобы отключить, задайте значение DWORD на 0:

"EnableOcspStaplingForSni"=dword:00000000

> [!NOTE] 
> Включение этого раздела реестра имеет потенциальное влияние на производительность.

## <a name="fipsalgorithmpolicy"></a>FIPSAlgorithmPolicy

Эта запись определяет соответствие требованиям Федерального стандарта обработки информации (FIPS). Значение по умолчанию — 0.

Применимые версии: Все версии, начиная с Windows Server 2012 и Windows 8. 

Путь реестра: HKLM SYSTEM\CurrentControlSet\Control\LSA

Комплекты шифров Windows Server FIPS: См. в разделе [поддерживаемые комплекты шифров и протоколы в поставщике Schannel SSP](https://technet.microsoft.com/library/dn786419.aspx).

## <a name="hashes"></a>Hashes

Алгоритмы хеширования TLS/SSL необходимо контролировать, настроив порядок комплектов шифров. См. в разделе [Настройка порядок комплектов шифров TLS](manage-tls.md#configuring-tls-cipher-suite-order) подробные сведения.

## <a name="issuercachesize"></a>IssuerCacheSize

Эта запись определяет размер кэша издателя и используется при сопоставлении издателя. Schannel SSP пытается сопоставить всех издателей в цепочке сертификатов клиента, а не только прямого издателя сертификата клиента. Когда издатели не сопоставляются с учетной записью, что является типичным случаем, сервер может пытаться повторно сопоставлять то же имя издателя, сотни раз в секунду. 

Чтобы избежать этого, сервер имеет негативный кэш, и если имя издателя не соответствует учетной записи, оно добавляется в кэш, и Schannel SSP не будет пытаться снова сопоставить это имя издателя, пока не истечет срок действия записи кэша. Эта запись реестра указывает размер кэша. Эта запись не существует в реестре по умолчанию. Значение по умолчанию — 100. 

Применимые версии: Все версии, начиная с Windows Server 2008 и Windows Vista.

Путь реестра: HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL

## <a name="issuercachetime"></a>IssuerCacheTime

Эта запись определяет продолжительность интервала времени ожидания кэша в миллисекундах. Schannel SSP пытается сопоставить всех издателей в цепочке сертификатов клиента, а не только прямого издателя сертификата клиента. В случае, когда издатели не соответствуют учетной записи, что довольно типично, сервер может пытаться повторно сопоставлять то же имя издателя, сотни раз в секунду.

Чтобы избежать этого, сервер имеет негативный кэш, и если имя издателя не соответствует учетной записи, оно добавляется в кэш, и Schannel SSP не будет пытаться снова сопоставить это имя издателя, пока не истечет срок действия записи кэша. Этот кэш сохраняется для повышения производительности, чтобы система не продолжала попытки сопоставить тех же издателей. Эта запись не существует в реестре по умолчанию. Значение по умолчанию — 10 минут.

Применимые версии: Все версии, начиная с Windows Server 2008 и Windows Vista.

Путь реестра: HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL

## <a name="keyexchangealgorithm---client-rsa-key-sizes"></a>KeyExchangeAlgorithm - клиента RSA основные размеры

Эта запись определяет размеры ключа RSA клиента. 

Необходимо контролировать использование алгоритмов обмена ключами, настроив порядок комплектов шифров.

Добавлена в Windows 10 версии 1507 и Windows Server 2016.

Путь реестра: HKLM\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\KeyExchangeAlgorithms\PKCS

Чтобы задать минимальный поддерживаемый диапазон RSA длиной бит для ключа клиента TLS, создайте **ClientMinKeyBitLength** запись. Эта запись не существует в реестре по умолчанию. После создания этой записи измените значение DWORD на нужный длина. Если не настроена, 1024 бит будет минимальным. 

Чтобы задать максимальный поддерживаемый диапазон RSA длиной бит для ключа клиента TLS, создайте **ClientMaxKeyBitLength** запись. Эта запись не существует в реестре по умолчанию. После создания этой записи измените значение DWORD на нужный длина. Если не настроена, более не применяются.

## <a name="keyexchangealgorithm---diffie-hellman-key-sizes"></a>KeyExchangeAlgorithm - размеры ключей Диффи-Хелмана

Эта запись определяет размеры ключа алгоритма Диффи-Хеллмана. 

Необходимо контролировать использование алгоритмов обмена ключами, настроив порядок комплектов шифров.

Добавлена в Windows 10 версии 1507 и Windows Server 2016.

Путь реестра: HKLM\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\KeyExchangeAlgorithms\Diffie-Hellman

Для определения длины минимальный поддерживаемый диапазон из Диффи-Helman бит для ключа клиента TLS, создание **ClientMinKeyBitLength** запись. Эта запись не существует в реестре по умолчанию. После создания этой записи измените значение DWORD на нужный длина. Если не настроена, 1024 бит будет минимальным. 
 
Для определения длины максимальный поддерживаемый диапазон из Диффи-Helman бит для ключа клиента TLS, создание **ClientMaxKeyBitLength** запись. Эта запись не существует в реестре по умолчанию. После создания этой записи измените значение DWORD на нужный длина. Если не настроена, более не применяются. 
 
Чтобы указать Helman Диффи битного ключа для TLS по умолчанию для сервера, создайте **ServerMinKeyBitLength** запись. Эта запись не существует в реестре по умолчанию. После создания этой записи измените значение DWORD на нужный длина. Если не настроена, 2048 бит будет использоваться по умолчанию. 

## <a name="maximumcachesize"></a>MaximumCacheSize

Эта запись определяет максимальное число элементов кэша. Установка для MaximumCacheSize значения 0 отключает кэш сеанса на стороне сервера и запрещает переподключение. Если для MaximumCacheSize задать значение больше установленного по умолчанию, Lsass.exe будет потреблять дополнительный объем памяти. Каждый элемент кэша сеанса обычно требует от 2 до 4 КБ памяти. Эта запись не существует в реестре по умолчанию. Значение по умолчанию — 20000. 

Применимые версии: Все версии, начиная с Windows Server 2008 и Windows Vista.

Путь реестра: HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL

## <a name="messaging--fragment-parsing"></a>Обмен сообщениями — фрагмент синтаксического анализа

________________________________________
Эта запись определяет максимальный размер фрагментированных сообщений подтверждения TLS, которые будут приняты. Сообщения, размер которых превышает разрешенный размер не будет принят и подтверждение TLS завершится ошибкой. Эти записи не существуют в реестре по умолчанию. 

Если присвоено значение 0x0, фрагментированного сообщения, не обрабатываются и приведет к сбою подтверждения TLS. В результате TLS клиентов или серверов на текущем компьютере несовместимые с RFC TLS. 

Максимально допустимый размер можно увеличить до 2 ^ 24-1 байт. Разрешение для чтения и хранить большие объемы непроверенных данных из сети клиент или сервер не является хорошей идеей и будет потреблять дополнительный объем памяти для каждого контекста безопасности. 

Добавленные в Windows 7 и Windows Server 2008 R2.
Доступно обновление, позволяющий Internet Explorer в Windows XP, Windows Vista или Windows Server 2008 для синтаксического анализа фрагментированных сообщений подтверждения TLS/SSL.

Путь реестра: HKLM\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Messaging

Чтобы задать максимальный размер фрагментированных сообщений подтверждения TLS, TLS клиент будет принимать, создайте **MessageLimitClient** запись. После создания этой записи измените значение DWORD на нужный длина. Если не задан, значение по умолчанию будет 0x8000 байт. 

Чтобы задать максимальный размер фрагментированных сообщений подтверждения TLS, на которые будет принимать сервер TLS при отсутствии без проверки подлинности клиента, создайте **MessageLimitServer** запись. После создания этой записи измените значение DWORD на нужный длина. Если не задан, значение по умолчанию будет 0x4000 байт. 

Чтобы задать максимальный размер фрагментированных сообщений подтверждения TLS, на которые будет принимать сервер TLS при отсутствии проверки подлинности клиента, создайте **MessageLimitServerClientAuth** запись. После создания этой записи измените значение DWORD на нужный длина. Если не задан, значение по умолчанию будет 0x8000 байт. 

## <a name="sendtrustedissuerlist"></a>SendTrustedIssuerList

Эта запись управляет флагом, который используется при отправке списка доверенных издателей. В случае серверов, которые доверяют сотням центров сертификации для проверки подлинности клиента, существует слишком много издателей, чтобы сервер мог отправлять их все на клиентский компьютер при запросе проверки подлинности клиента. В этом случае можно задать этот раздел реестра, и вместо отправки неполного списка Schannel SSP не будет отправлять клиенту никакой список.

Если список доверенных издателей не отправляется, это может повлиять на то, что клиент посылает в ответ на запрос сертификата клиента. Например, получив запрос на проверку подлинности клиента, Internet Explorer отображает только сертификаты клиента, по цепочке связанные с одним из центров сертификации, отправленных сервером. Если сервер не передает список, Internet Explorer отображает все сертификаты клиента, установленные на клиенте. 

Это поведение может быть нежелательно. Например, когда среда PKI включает перекрестные сертификаты, сертификаты клиента и сервера не будут иметь один и тот же корневой ЦС; таким образом Internet Explorer не может выбрать сертификат, который связан с одним из ЦС сервера. Если сервер настроен не отправлять список доверенных издателей, Internet Explorer будет отправлять все сертификаты.

Эта запись не существует в реестре по умолчанию.

Поведение отправки списка доверенных издателей по умолчанию

| Версия Windows | Time |
|-----------------|------|
| Windows Server 2012 и Windows 8 и более поздние версии | FALSE |
| Windows Server 2008 R2 и Windows 7 и более ранних версий | TRUE |

Применимые версии: Все версии, начиная с Windows Server 2008 и Windows Vista.

Путь реестра: HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL

## <a name="servercachetime"></a>ServerCacheTime

Эта запись определяет время в миллисекундах, через которое в операционной системе истекает срок действия записей кэша на стороне сервера. Значение 0 отключает кэш сеанса на стороне сервера и запрещает переподключение. Если для ServerCacheTime задать значение больше установленного по умолчанию, Lsass.exe будет потреблять дополнительный объем памяти. Каждый элемент кэша сеанса обычно требует от 2 до 4 КБ памяти. Эта запись не существует в реестре по умолчанию. 

Применимые версии: Все версии, начиная с Windows Server 2008 и Windows Vista.

Путь реестра: HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL

Время кэша сервера по умолчанию: 10 часов

## <a name="ssl-20"></a>SSL 2.0

Этот подраздел управляет использованием SSL 2.0.

Начиная с Windows 10, версия 1607 и Windows Server 2016, SSL 2.0 был удален и больше не поддерживается.
Параметры по умолчанию SSL 2.0, см. в разделе [протоколы TLS/SSL (Schannel SSP)](https://msdn.microsoft.com/library/windows/desktop/mt808159.aspx). 

Путь реестра: HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols

Чтобы включить протокол SSL 2.0, создайте **включено** запись в подразделе клиента или сервера, как описано в следующей таблице. Эта запись не существует в реестре по умолчанию. После создания этой записи измените значение DWORD на 1. 

Таблица подразделов SSL 2.0

| Подраздел | Описание |
|--------|-------------|
| клиент | Управляет использованием SSL 2.0 на стороне клиента SSL. |
| Server (Сервер) | Управляет использованием SSL 2.0 на сервере SSL. |

Чтобы отключить SSL 2.0 для клиента или сервера, измените значение DWORD на 0. Если приложение SSPI запрашивает использование SSL 2.0, будут отклонены. 

Чтобы отключить SSL 2.0 по умолчанию, создайте **DisabledByDefault** запись и изменение параметра DWORD значение 1. Если явным вызовом приложения SSPI запрашивает использование SSL 2.0, может быть согласованы. 

В следующем примере показано SSL 2.0 отключен в реестре:

![SSL 2.0 отключен](images/ssl-2-registry-setting.png)


## <a name="ssl-30"></a>SSL 3.0

Этот подраздел управляет использованием SSL 3.0.

Начиная с Windows 10, версия 1607 и Windows Server 2016, SSL 3.0 был отключен по умолчанию. Параметры по умолчанию SSL 3.0, см. в разделе [протоколы TLS/SSL (Schannel SSP)](https://msdn.microsoft.com/library/windows/desktop/mt808159.aspx). 

Путь реестра: HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols

Чтобы включить протокол SSL 3.0, создайте **включено** запись в подразделе клиента или сервера, как описано в следующей таблице.  
Эта запись не существует в реестре по умолчанию. После создания этой записи измените значение DWORD на 1. 

Таблица подразделов SSL 3.0

| Подраздел | Описание |
|--------|-------------|
| клиент | Управляет использованием SSL 3.0 на стороне клиента SSL. |
| Server (Сервер) | Управляет использованием SSL 3.0 на сервере SSL. |

Чтобы отключить SSL 3.0 для клиента или сервера, измените значение DWORD на 0.
Если приложение SSPI запрашивает использование SSL 3.0, будут отклонены. 

Чтобы отключить SSL 3.0 по умолчанию, создайте **DisabledByDefault** запись и изменение параметра DWORD значение 1. Если приложение SSPI явно запрашивает использование SSL 3.0, могут быть согласованы. 

В следующем примере показано SSL 3.0 отключен в реестре:

![SSL 3.0 отключен](images/ssl-3-registry-setting.png)

## <a name="tls-10"></a>TLS 1.0

Этот подраздел управляет использованием TLS 1.0.

Параметры по умолчанию протокол TLS 1.0, см. в разделе [протоколы TLS/SSL (Schannel SSP)](https://msdn.microsoft.com/library/windows/desktop/mt808159.aspx).

Путь реестра: HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols

Чтобы включить протокол TLS 1.0, создайте **включено** запись в раздел клиента или сервера, как описано в следующей таблице. Эта запись не существует в реестре по умолчанию. После создания этой записи измените значение DWORD на 1. 

Таблица подразделов TLS 1.0

| Подраздел | Описание |
|--------|-------------|
| клиент | Управляет использованием TLS 1.0 на TLS клиент. |
| Server (Сервер) | Управляет использованием TLS 1.0 на сервере TLS. |

Чтобы отключить TLS 1.0 для клиента или сервера, измените значение DWORD на 0.
Если SSPI приложение отправляет запрос на использование TLS 1.0, он будет запрещен. 

Чтобы отключить TLS 1.0 по умолчанию, создайте **DisabledByDefault** запись и изменение параметра DWORD значение 1. Если приложение SSPI явно запрашивает использовать TLS 1.0, могут быть согласованы. 

В следующем примере показано TLS 1.0 отключен в реестре:

![Протокол TLS 1.0 отключен](images/tls-registry-setting.png)

## <a name="tls-11"></a>TLS 1.1

Этот подраздел управляет использованием TLS 1.1.

Параметры по умолчанию TLS 1.1, см. в разделе [протоколы TLS/SSL (Schannel SSP)](https://msdn.microsoft.com/library/windows/desktop/mt808159.aspx).

Путь реестра: HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols

Чтобы включить протокол TLS 1.1, создайте **включено** запись в раздел клиента или сервера, как описано в следующей таблице. Эта запись не существует в реестре по умолчанию. После создания этой записи измените значение DWORD на 1. 

Таблица подразделов TLS 1.1

| Подраздел | Описание |
|--------|-------------|
| клиент | Управляет использованием TLS 1.1 на клиенте TLS. |
| Server (Сервер) | Управляет использованием TLS 1.1 на сервере TLS. |

Чтобы отключить TLS 1.1 для клиента или сервера, измените значение DWORD на 0.
Если приложение SSPI запросы на использование TLS 1.1, будут отклонены. 

Чтобы отключить TLS 1.1 по умолчанию, создайте **DisabledByDefault** запись и изменение параметра DWORD значение 1. Если приложение SSPI явно запрашивает на использование TLS 1.1, может быть согласованы. 

В следующем примере показано TLS 1.1 отключены в реестре:

![TLS 1.1 отключены](images/tls-11-registry-setting.png)

## <a name="tls-12"></a>TLS 1.2

Этот подраздел управляет использованием TLS 1.2.

Параметры по умолчанию протокол TLS 1.2, см. в разделе [протоколы TLS/SSL (Schannel SSP)](https://msdn.microsoft.com/library/windows/desktop/mt808159.aspx).

Путь реестра: HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols

Чтобы включить протокол TLS 1.2, создайте **включено** запись в раздел клиента или сервера, как описано в следующей таблице. Эта запись не существует в реестре по умолчанию. После создания этой записи измените значение DWORD на 1. 

Таблица подразделов TLS 1.2

| Подраздел | Описание |
|--------|-------------|
| клиент | Управляет использованием TLS 1.2 на клиенте TLS. |
| Server (Сервер) | Управляет использованием TLS 1.2 на сервере TLS. |

Чтобы отключить TLS 1.2 для клиента или сервера, измените значение DWORD на 0.
Если приложение SSPI запрашивает использование TLS 1.2, будут отклонены. 

Чтобы отключить TLS 1.2 по умолчанию, создайте **DisabledByDefault** запись и изменение параметра DWORD значение 1. Если приложение SSPI явно запрашивает использование TLS 1.2, может быть согласованы. 

В следующем примере показано TLS 1.2, отключены в реестре:

![Отключить протокол TLS 1.2](images/tls-12-registry-setting.png)

## <a name="dtls-10"></a>DTLS 1.0

Этот подраздел управляет использованием DTLS 1.0.

Параметры по умолчанию протокол DTLS 1.0, см. в разделе [протоколы TLS/SSL (Schannel SSP)](https://msdn.microsoft.com/library/windows/desktop/mt808159.aspx).

Путь реестра: HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols

Чтобы включить протокол DTLS 1.0, создайте **включено** запись в раздел клиента или сервера, как описано в следующей таблице. Эта запись не существует в реестре по умолчанию. После создания этой записи измените значение DWORD на 1. 

Таблица подразделов DTLS 1.0

| Подраздел | Описание |
|--------|-------------|
| клиент | Управляет использованием DTLS 1.0 на клиенте DTLS. |
| Server (Сервер) | Управляет использованием DTLS 1.0 на сервере DTLS. |

Чтобы отключить протокол DTLS 1.0 для клиента или сервера, измените значение DWORD на 0.
Если приложение SSPI запросы на использовать протокол DTLS версии 1.0, будут отклонены. 

Чтобы отключить протокол DTLS 1.0 по умолчанию, создайте **DisabledByDefault** запись и изменение параметра DWORD значение 1. Если приложение SSPI явно запрашивает использовать протокол DTLS версии 1.0, могут быть согласованы. 

В следующем примере показано DTLS 1.0 отключен в реестре:

![Протокол DTLS 1.0 отключен](images/dtls-10-registry-setting.png)

## <a name="dtls-12"></a>ПРОТОКОЛ DTLS ВЕРСИИ 1.2

Этот подраздел управляет использованием DTLS 1.2.

Параметры по умолчанию протокол DTLS версии 1.2, см. в разделе [протоколы TLS/SSL (Schannel SSP)](https://msdn.microsoft.com/library/windows/desktop/mt808159.aspx).

Путь реестра: HKLM SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols

Чтобы включить протокол DTLS версии 1.2, создайте **включено** запись в раздел клиента или сервера, как описано в следующей таблице. Эта запись не существует в реестре по умолчанию. После создания этой записи измените значение DWORD на 1. 

Таблица подразделов DTLS 1.2

| Подраздел | Описание |
|--------|-------------|
| клиент | Управляет использованием DTLS 1.2 на клиенте DTLS. |
| Server (Сервер) | Управляет использованием DTLS 1.2 на сервере DTLS. |


Чтобы отключить протокол DTLS 1.2 для клиента или сервера, измените значение DWORD на 0.
Если приложение SSPI запросы на использовать протокол DTLS версии 1.0, будут отклонены. 

Чтобы отключить протокол DTLS 1.2 по умолчанию, создайте **DisabledByDefault** запись и изменение параметра DWORD значение 1. Если приложение SSPI явно запрашивает использование DTLS 1.2, может быть согласованы. 

В следующем примере показано DTLS 1.1 отключены в реестре:

![Протокол DTLS 1.1 отключены](images/dtls-11-registry-setting.png)

