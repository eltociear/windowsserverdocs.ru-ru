---
title: Управление сертификатами, используемыми с сервером политики сети
description: Этот раздел содержит сведения об использовании сертификатов сервера с сервера политики сети в Windows Server 2016.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 204a4ef4-9d78-4a62-9940-43cc0e1c39d0
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 73f3d6a1e9dc6ae1520b1d685b6b05b5f3aed601
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2019
ms.locfileid: "59864235"
---
# <a name="manage-certificates-used-with-nps"></a>Управление сертификатами, используемыми с сервером политики сети

>Относится к: Windows Server (полугодовой канал), Windows Server 2016

Если вы развертываете метод проверки подлинности на основе сертификата, например протокол расширенной проверки подлинности\-Transport Layer Security \(EAP\-TLS\), защищенный наращиваемый протокол аутентификации\-Transport Layer Security \(PEAP\-TLS\)и PEAP\-Майкрософт протокола CHAP версии 2 \(MS\-CHAP v2\), необходимо зарегистрировать сертификат сервера на все ваши NPSs. Сертификат сервера должен:

- Соответствует минимальным требованиям, как описано в разделе [Настройка шаблонов сертификатов для протоколов PEAP и EAP требования](nps-manage-cert-requirements.md)

- Выданный центром сертификации \(ЦС\) , доверенным для клиентских компьютеров. ЦС является доверенным, когда существует свой сертификат в хранилище сертификатов доверенных корневых центров сертификации для текущего пользователя и локального компьютера.

Приведенные ниже инструкции помогают в управлении сертификатами сервера политики сети в развертываниях, где доверенный корневой ЦС является сторонним центром сертификации, таким как Verisign, или является ЦС, который вы развернули инфраструктуру открытых ключей \(PKI\) с помощью активный Службы сертификатов Directory \(AD CS\).

## <a name="change-the-cached-tls-handle-expiry"></a>Изменение срока действия маркера кэшированных TLS

Во время процессов начальную проверку подлинности для EAP\-TLS, PEAP\-TLS и PEAP\-MS\-CHAP версии 2, сервер политики сети кэширует часть свойства подключения TLS подключающегося клиента. Клиент также кэширует часть свойства подключения TLS NPS.

Каждой отдельной коллекции из этих свойств подключения TLS называется дескриптор TLS.

Клиентские компьютеры можно кэшировать маркеры TLS для нескольких структур проверки подлинности, хотя NPSs может кэшировать маркеры TLS многих клиентских компьютерах.

Кэшированные маркеры TLS на клиенте и сервере разрешить повторную проверку подлинности процесса происходят быстрее. Например при присоединяют компьютер выполняемой с сервер политики сети, сервер политики сети можно изучить дескриптор TLS для беспроводного клиентского и может быстро определить, что клиент использует выполняется попытка повторного подключения. Сервер политики сети разрешает подключение без выполнения полной проверки подлинности.

Соответственно клиент проверяет дескриптор TLS для сервера политики сети, определяет, что он выполняется попытка повторного подключения и не нужно выполнять проверку подлинности сервера.

На компьютерах под управлением Windows 10 и Windows Server 2016 срок действия маркера TLS по умолчанию — 10 часов.

В некоторых случаях может потребоваться увеличить или уменьшить время окончания срока действия маркера TLS.

Например можно уменьшить время окончания срока действия маркера TLS в случаях, где пользователя сертификат отзывается администратором, а действия сертификата истек. В этом случае пользователь может подключаться к сети, если сервер политики сети имеет кэшированный дескриптор TLS, который не истек. Уменьшение TLS истечения срока действия маркера может помочь предотвратить повторное подключение таких пользователей с помощью отозванных сертификатов.

>[!NOTE]
>В этом случае лучше для отключения учетной записи пользователя в Active Directory, или удалить учетную запись пользователя из группы Active Directory, который предоставляется разрешение на подключение к сети в политике сети. Распространение этих изменений на все контроллеры домена также может быть отложена, однако из-за задержки репликации. 

## <a name="configure-the-tls-handle-expiry-time-on-client-computers"></a>Настроить срок действия маркера TLS на клиентских компьютерах

Эта процедура позволяет изменить количество времени, что клиентские компьютеры кэшировать дескриптор TLS сервер политики сети. После успешной проверки подлинности сервер политики сети, клиентские компьютеры кэшировать свойства TLS-подключения сервера политики сети как дескриптор TLS. Дескриптор TLS имеет длительность по умолчанию 10 часов \(36,000,000 миллисекунд\). Можно увеличить или уменьшить время окончания срока действия маркера TLS, используя описанную ниже процедуру.

Членство в группе **Администраторы**, или эквивалентной является минимальным требованием для выполнения этой процедуры.

>[!IMPORTANT]
>Эта процедура должна быть выполнена на сервер политики сети, а не на клиентском компьютере.

### <a name="to-configure-the-tls-handle-expiry-time-on-client-computers"></a>Чтобы настроить протокол TLS обработки время окончания срока действия на клиентских компьютерах

1. На сервер политики сети откройте редактор реестра.

2. Перейдите к разделу реестра **HKEY\_ЛОКАЛЬНОГО\_MACHINE\System\CurrentControlSet\Control\SecurityProviders\SCHANNEL**

3. На **изменить** меню, щелкните **New**, а затем нажмите кнопку **ключ**.

4. Тип **ClientCacheTime**, и нажмите клавишу ВВОД.

5. Щелкните правой кнопкой мыши **ClientCacheTime**, нажмите кнопку **New**, а затем нажмите кнопку **DWORD (32-разрядное) значение**.

6. Введите количество времени, в миллисекундах, возникает необходимость клиентским компьютерам кэшировать дескриптор TLS сервер политики сети, после первой успешной аутентификации попытки с сервером политики сети.

## <a name="configure-the-tls-handle-expiry-time-on-npss"></a>Настроить срок действия маркера TLS на NPSs

Эта процедура используется для изменения количества времени, что NPSs кэширование дескрипторов TLS клиентских компьютеров. После успешной проверки подлинности клиентов доступа, NPSs кэшировать свойства TLS-подключения клиентского компьютера как дескриптор TLS. Дескриптор TLS имеет длительность по умолчанию 10 часов \(36,000,000 миллисекунд\). Можно увеличить или уменьшить время окончания срока действия маркера TLS, используя описанную ниже процедуру.

Членство в группе **Администраторы**, или эквивалентной является минимальным требованием для выполнения этой процедуры.

>[!IMPORTANT]
>Эта процедура должна быть выполнена на сервер политики сети, а не на клиентском компьютере.

### <a name="to-configure-the-tls-handle-expiry-time-on-npss"></a>Чтобы настроить протокол TLS обработки время окончания срока действия на NPSs

1. На сервер политики сети откройте редактор реестра.

2. Перейдите к разделу реестра **HKEY\_ЛОКАЛЬНОГО\_MACHINE\System\CurrentControlSet\Control\SecurityProviders\SCHANNEL**

3. На **изменить** меню, щелкните **New**, а затем нажмите кнопку **ключ**.

4. Тип **ServerCacheTime**, и нажмите клавишу ВВОД.

5. Щелкните правой кнопкой мыши **ServerCacheTime**, нажмите кнопку **New**, а затем нажмите кнопку **DWORD (32-разрядное) значение**.

6. Введите количество времени, в миллисекундах, возникает необходимость NPSs на кэширование дескрипторов TLS клиентского компьютера, после первой успешной аутентификации попытки клиентом.

## <a name="obtain-the-sha-1-hash-of-a-trusted-root-ca-certificate"></a>Получение хэша SHA-1 сертификата доверенного корневого ЦС

Эта процедура используется для получения хэша доверенного корневого центра сертификации (ЦС) защиты хэш-алгоритм (SHA-1) на основе сертификата, установленного на локальном компьютере. В некоторых случаях например, при развертывании групповой политики, это необходимо назначить сертификат с помощью хэша SHA-1 сертификата.

При использовании групповой политики, можно назначить один или несколько сертификатов доверенных корневых ЦС, которые клиенты должны использовать для проверки подлинности сервером политики сети в процессе взаимной проверки подлинности EAP или PEAP. Чтобы назначить сертификат доверенного корневого ЦС, который клиенты должны использовать для проверки сертификата сервера, можно ввести хэш SHA-1 сертификата.

Ниже описана процедура получить хэш-код доверенного корневого сертификата ЦС SHA-1, используя оснастку сертификатов консоли управления (MMC). 

Для выполнения этой процедуры необходимо быть членом **пользователей** группе на локальном компьютере.

### <a name="to-obtain-the-sha-1-hash-of-a-trusted-root-ca-certificate"></a>Для получения хэша сертификата доверенного корневого ЦС на SHA-1

1. В диалоговом окне "Выполнить" или Windows PowerShell, введите **mmc**, и нажмите клавишу ВВОД. Консоль управления \(MMC\) открывает. В консоли MMC щелкните **файл**, затем нажмите кнопку **Snap\in добавить или удалить**. **Добавление или удаление оснасток** откроется диалоговое окно.

2. В **Добавление или удаление оснасток**в **Доступные оснастки**, дважды щелкните **сертификаты**. Откроется мастер оснастки сертификатов. Нажмите кнопку **учетная запись компьютера**, а затем нажмите кнопку **Далее**.

3. В **Выбор компьютера**, убедитесь, что **локальном компьютере (компьютер, на которой запущена эта консоль)** является, щелкните **Готово**, а затем нажмите кнопку **ОК**.

4. В левой области дважды щелкните **сертификаты (локальный компьютер)**, а затем дважды щелкните **доверенные корневые центры сертификации** папки.

5. **Сертификаты** папка является вложенной **доверенные корневые центры сертификации** папки. Нажмите кнопку **сертификаты** папки.

6. В области сведений найдите сертификат для вашего доверенного корневого центра сертификации. Дважды щелкните сертификат. **Сертификат** откроется диалоговое окно.

7. В **сертификат** диалоговом окне щелкните **сведения** вкладки.

8. В списке полей, прокрутите список и выберите **отпечаток**.

9. В нижней области отображается шестнадцатеричную строку, которая является хэш SHA-1 сертификата. Выберите хэш SHA-1 и нажмите сочетание клавиш Windows для команды Copy \(CTRL\+C\) копируемые хэш-код в буфер обмена Windows.

10. Откройте расположение, к которому вы хотите вставить хэш SHA-1, правильно обнаружить курсор и нажмите сочетание клавиш Windows для команды Paste \(CTRL\+V\). 

Дополнительные сведения о сертификатах и NPS см. в разделе [Настройка шаблонов сертификатов для протоколов PEAP и EAP требования](nps-manage-cert-requirements.md).

Дополнительные сведения о сервере политики сети, см. в разделе [сервера политики сети (NPS)](nps-top.md).