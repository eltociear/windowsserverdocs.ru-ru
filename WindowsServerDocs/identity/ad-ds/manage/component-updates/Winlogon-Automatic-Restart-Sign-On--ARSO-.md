---
ms.assetid: cb834273-828a-4141-9387-37dd8270e932
title: Автоматический вход при перезапуске с помощью Winlogon (ARSO)
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 4024a00c6c186aa929e88cb2aa86b0ec04a731b3
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2019
ms.locfileid: "59883625"
---
# <a name="winlogon-automatic-restart-sign-on-arso"></a>Автоматический вход при перезапуске с помощью Winlogon (ARSO)

>Область применения. Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

**Автор**: Джастин Тернер, старший инженер по улучшению поддержки с группой Windows

> [!NOTE]
> Этот материал создан инженером службы поддержки клиентов Майкрософт и предназначен для опытных администраторов и архитекторов систем, которым нужны более глубокие технические сведения о функциях и решениях в Windows Server 2012 R2, а не обычная информация, доступная в статьях на сайте TechNet. Однако он не был отредактирован согласно требованиям сайта, поэтому некоторые формулировки могут быть не такими выверенными, как на станицах TechNet.

## <a name="overview"></a>Обзор
Windows 8 появился приложений экрана блокировки.  Это приложения, которые выполняются и отображать уведомления при заблокированном сеанс пользователя (календарь, встреч, электронной почты и сообщения, и т.д.).  Не отображать эти уведомления на экране блокировки после перезапуска устройства, которые будут запущены вновь из-за процесс обновления Windows.  Некоторые пользователи зависят от этих приложений экрана блокировки.

## <a name="whats-changed"></a>Что изменилось?
При входе пользователя на устройстве Windows 8.1, LSA сохранить только процессом lsass.exe учетные данные пользователя в зашифрованных объем доступной памяти. Когда обновление Windows инициирует автоматическое обновление без присутствия пользователя, эти учетные данные будет использоваться для настройки автоматического входа для пользователя. Обновление Windows, под управлением системы с привилегиями TCB инициирует вызов RPC для этого.

На перезагрузку, пользователь будет автоматически в системе с помощью механизма автоматического входа в систему и Кроме того заблокирован для защиты сеанс пользователя. Блокировка будет запущена с помощью Winlogon, тогда как управление учетными данными выполняется путем LSA.  Автоматическое подписывание и блокировке пользователя на консоли приложений экрана блокировки пользователя будет перезапуск и доступность.

> [!NOTE]
> После обновления Windows, вызываемых перезагрузки, автоматически последнего интерактивный пользователь вошел и сеанс блокируется таким образом можно запустить приложения экран блокировки пользователя.

![Winlogon](media/Winlogon-Automatic-Restart-Sign-On--ARSO-/GTR_ADDS_LockScreenApp.gif)

![Winlogon](media/Winlogon-Automatic-Restart-Sign-On--ARSO-/GTR_ADDS_LockScreen.gif)

**Краткий обзор**

-   Обновления Windows требуется перезагрузка

-   Является возможность перезапуска компьютером (*нет приложений, которые будут потеряны данные*)?

    -   Перезапуск для вас

    -   Повторить вход

    -   Блокировка компьютера

-   Включить или отключить с помощью групповой политики

    -   Отключено по умолчанию в SKU серверов

-   Почему?

    -   Некоторые обновления не может завершиться, пока пользователь не выйдет в.

    -   Более эффективное взаимодействие с пользователем: не нужно ждать 15 минут для завершения установки обновлений

-   Как? AutoLogon

    -   сохраняет пароль, использует эти учетные данные для входа

    -   Сохранение учетных данных как секрет LSA в выгружаемой памяти

    -   Можно включить только при включении BitLocker

## <a name="group-policy-sign-in-last-interactive-user-automatically-after-a-system-initiated-restart"></a>Групповая политика: Вход последний интерактивный пользователь автоматически после перезапуска, инициированные системой
В Windows 8.1 / Windows Server 2012 R2, автоматический вход в систему пользователя экран блокировки после перезапуска Windows Update согласиться для номеров SKU для сервера и отказаться от для клиентских SKU.

**Размещение политики:** Конфигурация компьютера > политики > Административные шаблоны > компоненты Windows > параметр входа в систему Windows

**Имя политики:** Вход последний интерактивный пользователь автоматически после перезапуска, инициированные системой

**Поддерживается в:** Не ниже Windows Server 2012 R2, Windows 8.1 или Windows RT 8.1

**Описание: Справка:**

Этот параметр политики определяет, является ли устройство будет автоматически войти последнего интерактивного пользователя после обновления Windows перезапускает компьютер.

Если вы включаете или не настраивать этот параметр политики, устройство безопасно сохраняет учетные данные пользователя (включая имя пользователя, домена и зашифрованный пароль) для настройки автоматического входа в систему, после перезапуска обновления Windows. После перезагрузки Windows Update он автоматически вошедшего в систему, и сеанс блокируется автоматически с помощью всех приложений экрана блокировки, настроенных для этого пользователя.

Если этот параметр политики отключен, устройство не хранит учетные данные пользователя для автоматического входа в систему после перезагрузки компьютера обновления Windows. После перезапуска системы, приложений экрана блокировки пользователей не перезапускаются.

**Редактор реестра**

|Имя значения|Тип|Данные|
|--------------|--------|--------|
|DisableAutomaticRestartSignOn|DWORD|0<br /><br />**Пример:**<br /><br />0 (включено)<br /><br />1 (выключена)|

**Расположение реестра политики:** HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System

**Тип:** DWORD

**Имя реестра:** DisableAutomaticRestartSignOn

Значение: 0 или 1

0 = Enabled

1 = отключено

![Winlogon](media/Winlogon-Automatic-Restart-Sign-On--ARSO-/GTR_ADDS_SignInPolicy.gif)

## <a name="troubleshooting"></a>Устранение неполадок
При автоматической блокировки WinLogon трассировки WinLogon его состояние будет храниться в журнале событий WinLogon.

Регистрируется состояние конфигурации попытка автоматического входа

-   При успешном выполнении

    -   записи, таким образом

-   В случае сбоя:

    -   Записывает, что произошел сбой

-   При изменении состояния BitLocker:

    -   удаление учетных данных будет регистрироваться

        -   Они будут храниться в LSA операционного журнала.

### <a name="reasons-why-autologon-might-fail"></a>Причин возможного сбоя автоматического входа
Существует несколько случаев, в которых нельзя достичь Автоматическое имя входа пользователя.  Этот раздел предназначен для захвата известных сценариев, в которых это может произойти.

### <a name="user-must-change-password-at-next-login"></a>Пользователь должен сменить пароль при следующем входе в систему
Имя входа пользователя можно ввести блокированном состоянии, при необходимости изменения пароля при следующем входе в систему.  Это может быть обнаружены до перезапуска, в большинстве случаев, но не все (например, можно получить истечение срока действия пароля между выключением и следующим следующего входа в систему.

### <a name="user-account-disabled"></a>Учетная запись пользователя отключена
Можно поддерживать существующего сеанса пользователя, даже если он отключен.  Перезапуск для учетной записи, которая отключена можно обнаружить локально в большинстве случаев заранее, в зависимости от групповой политики, не может быть для учетных записей домена (некоторые домена с кэшированием рабочих сценариев входа в систему даже если учетная запись отключена на контроллере домена).

### <a name="logon-hours-and-parental-controls"></a>Время входа и родительский контроль
Время входа и родительского контроля можно запретить создается новый пользовательский сеанс.  В случае перезапуска этого периода, пользователю будет запрещен для входа в систему.  Нет дополнительных политику, которая включает блокировку или выход из системы, как действие для обеспечения соответствия.  Это может вызвать проблемы во многих случаях дочерних, где блокировки учетной записи возможно возникновение испытательной времени и пробуждения, особенно в том случае, если период обслуживания — обычно в течение этого времени.

## <a name="additional-resources"></a>Дополнительные ресурсы
**Таблицы SEQ таблицы \\ \* ARABIC 3: Глоссарий ARSO**

|Термин|Определение|
|--------|--------------|
|Автоматический вход в систему|Автоматический вход — это функция, которая присутствует в Windows на протяжении нескольких версий.  Это документированной функцией Windows, даже есть средства, такие как Autologon для Windows версии 3.01  *[http:/technet.microsoft.com/sysinternals/bb963905.aspx](https://technet.microsoft.com/sysinternals/bb963905.aspx)*<br /><br />Он позволяет одного пользователя устройства для автоматического входа без ввода учетных данных. Настроить учетные данные, хранящиеся в реестре как зашифрованный секрет LSA.|

