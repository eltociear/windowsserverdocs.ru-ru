---
title: Начало работы с групповыми управляемыми учетными записями служб
description: Безопасность Windows Server
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-gmsa
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7130ad73-9688-4f64-aca1-46a9187a46cf
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 6da212185eb47d3f30f81ca6f1eb322bc232e229
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2019
ms.locfileid: "59881455"
---
# <a name="getting-started-with-group-managed-service-accounts"></a>Начало работы с групповыми управляемыми учетными записями служб

>Область применения. Windows Server (полугодовой канал), Windows Server 2016


Это руководство содержит пошаговые инструкции и справочные сведения об активации и использовании групповых управляемых учетных записей служб в Windows Server 2012.

**В этом документе**

-   [Предварительные требования](#BKMK_Prereqs)

-   [Введение](#BKMK_Intro)

-   [Развертывание новой фермы серверов](#BKMK_DeployNewFarm)

-   [Добавление узлов в существующую ферму серверов](#BKMK_AddMemberHosts)

-   [Обновление свойств групповой управляемой учетной записи службы](#BKMK_Update_gMSA)

-   [Списание узлов из существующей фермы серверов](#BKMK_DecommMemberHosts)


> [!NOTE]
> В этом разделе приводятся примеры командлетов Windows PowerShell, которые можно использовать для автоматизации некоторых описанных процедур. Дополнительные сведения см. в разделе [Командлеты](https://go.microsoft.com/fwlink/p/?linkid=230693).

## <a name="BKMK_Prereqs"></a>Предварительные требования
См. раздел [Требования для групповых управляемых учетных записей служб](#BKMK_gMSA_Req).

## <a name="BKMK_Intro"></a>Общие сведения о
Когда клиентский компьютер подключается к службе, размещенной на ферме серверов с использованием балансировки сетевой нагрузки (NLB) или какого-либо другого метода, при котором клиенту, проходящему проверку подлинности, все службы кажутся одной, протоколы проверки подлинности, поддерживающие взаимную проверку подлинности (такие как Kerberos), можно использовать, только если на всех экземплярах служб используется один и тот же субъект. Это означает, что удостоверение каждой службы должно подтверждаться одинаковым паролем или ключом.

> [!NOTE]
> Отказоустойчивые кластеры не поддерживают групповые управляемые учетные записи служб. При этом групповую или автономную учетную запись службы могут использовать службы, работающие поверх службы кластеров и представляющие собой службу Windows, пул приложений или назначенную задачу либо поддерживающие такие учетные записи изначально.

Службы могут выбирать следующие разрешенные субъекты, каждый из которых обладает определенными свойствами:

|Разрешенные субъекты|Область применения|Поддерживаемые службы|Управление паролями|
|-------|-----|-----------|------------|
|Учетная запись компьютера в системе Windows|Домен|Ограничена одним сервером в домене|Управляется компьютером|
|Учетная запись компьютера без системы Windows|Домен|Любой сервер в домене|Нет|
|Виртуальная учетная запись|Локальная|Ограничена одним сервером|Управляется компьютером|
|Автономная управляемая учетная запись Windows 7|Домен|Ограничена одним сервером в домене|Управляется компьютером|
|Учетная запись пользователя|Домен|Любой сервер в домене|Нет|
|Групповая управляемая учетная запись службы|Домен|Любой сервер присоединенных к домену Windows Server 2012|Управляется контроллером домена и извлекается узлом|

Учетные записи компьютеров Windows, автономные управляемые учетные записи Windows 7 и виртуальные учетные записи могут использоваться только в одной системе. Если вы настраиваете учетную запись, которая будет использоваться различными службами на фермах серверов, выберите учетную запись пользователя или учетную запись не в системе Windows. Такие учетные записи не имеют функции централизованного управления паролями, а значит, каждой организации придется создавать дорогое решение для обновления ключей для служб в каталоге Active Directory и их передачи во все экземпляры этих служб.

В Windows Server 2012 службам или администраторам служб не нужно синхронизировать пароли между экземплярами служб при использовании групповых управляемых учетных записей служб (gMSA). Вы создаете групповую управляемую учетную запись службы в Active Directory и настраиваете службу, поддерживающую управляемые учетные записи. Для подготовки групповой управляемой учетной записи службы можно использовать командлеты *-ADServiceAccount, входящие в модуль Active Directory. Конфигурацию удостоверения службы на узле поддерживают:

-   те же API, что и для автономных управляемых учетных записей служб, поэтому продукты, которые поддерживают автономные управляемые учетные записи служб, поддерживают и групповые;

-   службы, которые настраивают удостоверения для входа с помощью диспетчера управления службами;

-   службы, которые используют для настройки удостоверения диспетчер IIS для пулов приложений;

-   задачи, использующие планировщик заданий.

### <a name="BKMK_gMSA_Req"></a>Требования для групповых управляемых учетных записей служб
В приведенной ниже таблице указаны требования к операционной системе, которые должны выполняться для работы проверки подлинности Kerberos со службами, использующими групповые управляемые учетные записи служб. Требования  Active Directory перечислены под таблицей.

Для выполнения команд Windows PowerShell, которые используются для администрирования групповых управляемых учетных записей служб, необходима 64-разрядная архитектура.

**Требования к операционной системе**

|Элемент|Требование|Операционная система|
|------|--------|----------|
|Узел клиентского приложения|RFC-совместимый клиент Kerberos|Не ниже Windows XP|
|Контроллеры домена учетной записи пользователя|RFC-совместимый KDC|Не ниже Windows Server 2003|
|Узлы, входящие в службу общего доступа|| Windows Server 2012 |
|Контроллеры домена элемента узла|RFC-совместимый KDC|Не ниже Windows Server 2003|
|Контроллеры домена групповой управляемой учетной записи| Windows Server 2012 контроллеры доменов для извлечения пароля|Домен с Windows Server 2012, которые могут работать под управлением некоторых более ранних, чем Windows Server 2012 |
|Узел внутренней службы|RFC-совместимый сервер приложений Kerberos|Не ниже Windows Server 2003|
|Контроллеры домена учетной записи службы серверной части|RFC-совместимый KDC|Не ниже Windows Server 2003|
|Windows PowerShell для Active Directory|Windows PowerShell для Active Directory, установленный на компьютере с поддержкой 64-разрядной архитектуры или на компьютере удаленного управления (например, с помощью средств удаленного администрирования сервера).| Windows Server 2012 |

**Требования Active Directory службы домена**

-   Схема Active Directory в лесу домена таких учетных записей необходимо обновить до Windows Server 2012 для создания управляемой.

    Можно обновить схему, можно установить контроллер домена под управлением Windows Server 2012 или путем запуска соответствующую версию adprep.exe с компьютера под управлением Windows Server 2012. Значение атрибута для версии объекта CN=Schema,CN=Configuration,DC=Contoso,DC=Com должно быть равным 52.

-   Новая групповая управляемая учетная запись.

-   Новая или существующая группа безопасности, если вы даете узлу службы разрешение на использование групповой управляемой учетной записи службы группой.

-   Новая или существующая группа безопасности, если вы даете группе управление доступом к управляемой группе.

-   Если первый основной корневой ключ для Active Directory не развернут в домене или не создан, его необходимо создать. Результат создания ключа можно проверить в журнале рабочих событий KdsSvc, идентификатор события — 4004.

Инструкции как для создания ключа, см. раздел [создать корневой ключ KDS службы распространения ключей](create-the-key-distribution-services-kds-root-key.md). Корневым ключом для Active Directory является ключ службы распространения ключей (Майкрософт) — kdssvc.dll.

**Жизненный цикл**

Жизненный цикл фермы серверов с использованием функции групповых управляемых учетных записей служб включает следующие задачи:

-   Развертывание фермы серверов федерации

-   Добавление узлов в существующую ферму серверов

-   Списание узлов из существующей фермы серверов

-   Списание существующей фермы серверов

-   Удаление скомпрометированного узла из фермы серверов при необходимости

## <a name="BKMK_DeployNewFarm"></a>Развертывание новой фермы серверов
При развертывании новой фермы серверов администратору службы необходимо определить:

-   поддерживает ли служба использование групповых управляемых учетных записей служб;

-   требует ли служба проверки подлинности входящих или исходящих подключений;

-   имена учетных записей компьютеров для входящих в службу узлов с использованием групповых управляемых учетных записей служб;

-   NetBIOS-имя службы;

-   имя DNS-узла службы;

-   имена субъектов-служб (SPN) для службы;

-   периодичность смены пароля (по умолчанию 30 дней).

### <a name="BKMK_Step1"></a>Шаг 1. Создание групповых управляемых учетных записей служб
Управляемой можно создать только в том случае, если схема леса обновлена до Windows Server 2012, основной корневой ключ для Active Directory развернут и имеется по крайней мере один контроллер домена Windows Server 2012 в домене, в котором создается эта учетная запись.

Минимальным требованием для выполнения этих процедур является членство в группе **Администраторы домена** либо **Операторы учета** или наличие права на создание объектов msDS-GroupManagedServiceAccount.

#### <a name="BKMK_CreateGMSA"></a>Для создания групповой управляемой учетной записи, используя командлет New-ADServiceAccount.

1.  На контроллере домена Windows Server 2012, запустите Windows PowerShell из панели задач.

2.  Введите следующие команды в командной строке Windows PowerShell и нажмите клавишу ВВОД (модуль Active Directory загрузится автоматически):

    **Новый ADServiceAccount [-Name] <string> - DNSHostName <string> [-KerberosEncryptionType <ADKerberosEncryptionType>] [-ManagedPasswordIntervalInDays < допускает значения NULL [Int32] >] [-PrincipalsAllowedToRetrieveManagedPassword < ADPrincipal] >] - SamAccountName <string> - ServicePrincipalNames < string [] >**

    |Параметр|Строка|Пример|
    |-------|-----|------|
    |Имя|Имя учетной записи|ITFarm1|
    |DNSHostName|Имя DNS-узла службы|ITFarm1.contoso.com|
    |KerberosEncryptionType|Любые виды шифрования, поддерживаемые серверами узлов|RC4, AES128, AES256|
    |ManagedPasswordIntervalInDays|Периодичность смены пароля в днях (если не указано, используется значение по умолчанию 30)|90|
    |PrincipalsAllowedToRetrieveManagedPassword|Имена учетных записей компьютеров для входящих в службу узлов или групп безопасности, в которые входят эти узлы|ITFarmHosts|
    |SamAccountName|NetBIOS-имя службы, если не совпадает с именем|ITFarm1|
    |ServicePrincipalNames|Имена субъектов-служб (SPN) для службы|http/ITFarm1.contoso.com/contoso.com, http/ITFarm1.contoso.com/contoso, http/ITFarm1/contoso.com, http/ITFarm1/contoso|

    > [!IMPORTANT]
    > Периодичность смены пароля можно настроить только в процессе создания. Если вам нужно изменить это значение, создайте новую групповую управляемую учетную запись службы и настройте этот параметр в процессе ее создания.

    **Пример**

    Введите команды в одну строку, даже если кажется, что из-за ограничений форматирования они переносятся по словам на другую строку.

    ```
    New-ADServiceAccount ITFarm1 -DNSHostName ITFarm1.contoso.com -PrincipalsAllowedToRetrieveManagedPassword ITFarmHosts -KerberosEncryptionType RC4, AES128, AES256 -ServicePrincipalNames http/ITFarm1.contoso.com/contoso.com, http/ITFarm1.contoso.com/contoso, http/ITFarm1/contoso.com, http/ITFarm1/contoso

    ```

Минимальным требованием для выполнения этих процедур является членство в группе **Администраторы домена** либо **Операторы учета** или наличие права на создание объектов msDS-GroupManagedServiceAccount. Дополнительные сведения об использовании подходящих учетных записей и членства в группах см. в разделе [Локальные группы и группы домена по умолчанию](https://technet.microsoft.com/library/dd728026(WS.10).aspx).

##### <a name="to-create-a-gmsa-for-outbound-authentication-only-using-the-new-adserviceaccount-cmdlet"></a>Чтобы создать групповую управляемую учетную запись службы для исходящей проверки подлинности, используйте командлет New-ADServiceAccount.

1.  На контроллере домена Windows Server 2012, запустите Windows PowerShell из панели задач.

2.  Введите следующие команды в командной строке Windows PowerShell и нажмите клавишу ВВОД:

    **Новый ADServiceAccount [-Name] <string> - RestrictToOutboundAuthenticationOnly [-ManagedPasswordIntervalInDays < допускает значения NULL [Int32] >] [-PrincipalsAllowedToRetrieveManagedPassword < ADPrincipal [] >]**

    |Параметр|Строка|Пример|
    |-------|-----|------|
    |Имя|Имя учетной записи|ITFarm1|
    |ManagedPasswordIntervalInDays|Периодичность смены пароля в днях (если не указано, используется значение по умолчанию 30)|75|
    |PrincipalsAllowedToRetrieveManagedPassword|Имена учетных записей компьютеров для входящих в службу узлов или групп безопасности, в которые входят эти узлы|ITFarmHosts|

    > [!IMPORTANT]
    > Периодичность смены пароля можно настроить только в процессе создания. Если вам нужно изменить это значение, создайте новую групповую управляемую учетную запись службы и настройте этот параметр в процессе ее создания.

**Пример**

```
New-ADServiceAccount ITFarm1 -RestrictToOutboundAuthenticationOnly - PrincipalsAllowedToRetrieveManagedPassword ITFarmHosts

```

### <a name="BKMK_ConfigureServiceIdentity"></a>Шаг 2. Настройка службы для приложения удостоверения служб
Для настройки служб в Windows Server 2012, см. в разделе документации к следующим функциям:

-   Пул приложений IIS

    Дополнительные сведения см. в разделе [Указание удостоверения для пула приложений (IIS 7)](https://technet.microsoft.com/library/cc771170(WS.10).aspx).

-   Службы Windows

    Дополнительные сведения см. в разделе [Службы](https://technet.microsoft.com/library/cc772408.aspx).

-   Задачи

    Дополнительные сведения см. в статье [Обзор планировщика задач](https://technet.microsoft.com/library/cc721871.aspx).

Групповые управляемые учетные записи могут поддерживать и другие службы. Информацию о настройки таких служб см. в документации к соответствующим продуктам.

## <a name="BKMK_AddMemberHosts"></a>Добавление узлов в существующую ферму серверов
При использовании группы безопасности для управления, добавить учетную запись компьютера на новый узел члена в группу безопасности (который входящими узлы являются членами) с помощью одного из следующих методов.

Минимальным требованием для выполнения этих процедур является членство в группе **Администраторы домена**или наличие права на добавление объектов в группу безопасности.

-   Метод 1: Active Directory — пользователи и компьютеры

    Порядок использования данного метода см. в статье [Добавление учетной записи компьютера в группу](https://technet.microsoft.com/library/cc733097.aspx) с помощью интерфейса Windows и [Управление различными доменами в центре администрирования Active Directory](manage-different-domains-in-active-directory-administrative-center.md).

-   Метод 2: dsmod

    Порядок использования данного метода см. в статье [Добавление учетной записи компьютера в группу](https://technet.microsoft.com/library/cc733097.aspx) с помощью командной строки.

-   Метод 3: Командлет Add-ADPrincipalGroupMembership в Windows PowerShell Active Directory

    Порядок использования данного метода см. в статье [Add-ADPrincipalGroupMembership](https://technet.microsoft.com/library/ee617203.aspx).

Если используются учетные записи компьютеров, найдите существующие учетные записи и добавьте новую учетную запись компьютера.

Минимальным требованием для выполнения этой процедуры является членство в группе **Администраторы домена**либо **Операторы учета**или наличие права на управление объектами msDS-GroupManagedServiceAccount. Дополнительные сведения об использовании подходящих учетных записей и членства в группах см. в разделе "Локальные группы и группы домена по умолчанию".

#### <a name="to-add-member-hosts-using-the-set-adserviceaccount-cmdlet"></a>Добавление входящих в службу узлов с помощью командлета Set-ADServiceAccount

1.  На контроллере домена Windows Server 2012, запустите Windows PowerShell из панели задач.

2.  Введите следующие команды в командной строке Windows PowerShell и нажмите клавишу ВВОД:

    **Get-ADServiceAccount [-Name] <string> - PrincipalsAllowedToRetrieveManagedPassword**

3.  Введите следующие команды в командной строке Windows PowerShell и нажмите клавишу ВВОД:

    **SET-ADServiceAccount [-Name] <string> - PrincipalsAllowedToRetrieveManagedPassword < ADPrincipal [] >**

|Параметр|Строка|Пример|
|-------|-----|------|
|Имя|Имя учетной записи|ITFarm1|
|PrincipalsAllowedToRetrieveManagedPassword|Имена учетных записей компьютеров для входящих в службу узлов или групп безопасности, в которые входят эти узлы|Host1, Host2, Host3|

**Пример**

Например, чтобы добавить входящие в службу узлы, введите следующие команды и нажмите клавишу ВВОД:

```
Get-ADServiceAccount [-Name] ITFarm1 -PrincipalsAllowedToRetrieveManagedPassword

```

```
Set-ADServiceAccount [-Name] ITFarm1-PrincipalsAllowedToRetrieveManagedPassword Host1,Host2,Host3

```

## <a name="BKMK_Update_gMSA"></a>Обновление свойств групповой управляемой учетной записи службы
Минимальным требованием для выполнения этой процедуры является членство в группе **Администраторы домена**либо **Операторы учета**или наличие права на запись в объекты msDS-GroupManagedServiceAccount.

Откройте модуль Active Directory для Windows PowerShell и настройте желаемые свойства с помощью командлета Set-ADServiceAccount.

Подробную информацию об установке этих свойств см. в статье [Set-ADServiceAccount](https://technet.microsoft.com/library/ee617252.aspx) в библиотеке TechNet или введите **Get-Help Set-ADServiceAccount** в командной строке модуля Active Directory для Windows PowerShell и нажмите клавишу ВВОД.

## <a name="BKMK_DecommMemberHosts"></a>Списание узлов из существующей фермы серверов
Минимальным требованием для выполнения этих процедур является членство в группе **Администраторы домена** или наличие права на удаление объектов из группы безопасности.

### <a name="step-1-remove-member-host-from-gmsa"></a>Шаг 1. Удаление узла из групповой управляемой учетной записи службы
Если группы безопасности для управления, удалите учетную запись компьютера для списываемого узла из группы безопасности, что узлы входящими члена, члена с помощью любого из следующих методов.

-   Метод 1: Active Directory — пользователи и компьютеры

    Порядок использования данного метода см. в статье [Удаление учетной записи компьютера](https://technet.microsoft.com/library/cc754624.aspx) с помощью интерфейса Windows и [Управление различными доменами в центре администрирования Active Directory](manage-different-domains-in-active-directory-administrative-center.md).

-   Метод 2: drsm

    Порядок использования данного метода см. в статье [Удаление учетной записи компьютера](https://technet.microsoft.com/library/cc754624.aspx) с помощью командной строки.

-   Метод 3: командлет Remove-ADPrincipalGroupMembership в Windows PowerShell Active Directory

    Подробную информацию об использовании данного метода см. в статье  [Remove-ADPrincipalGroupMembership](https://technet.microsoft.com/library/ee617243.aspx) в библиотеке TechNet или введите **Get-Help Remove-ADPrincipalGroupMembership** в командной строке модуля Active Directory для Windows PowerShell и нажмите клавишу ВВОД.

Если используются учетные записи компьютеров, извлеките существующие учетные записи и добавьте все учетные записи компьютеров, кроме удаленных.

Минимальным требованием для выполнения этой процедуры является членство в группе **Администраторы домена**либо **Операторы учета**или наличие права на управление объектами msDS-GroupManagedServiceAccount. Дополнительные сведения об использовании подходящих учетных записей и членства в группах см. в разделе "Локальные группы и группы домена по умолчанию".

##### <a name="to-remove-member-hosts-using-the-set-adserviceaccount-cmdlet"></a>Удаление входящих в службу узлов с помощью командлета Set-ADServiceAccount

1.  На контроллере домена Windows Server 2012, запустите Windows PowerShell из панели задач.

2.  Введите следующие команды в командной строке Windows PowerShell и нажмите клавишу ВВОД:

    **Get-ADServiceAccount [-Name] <string> - PrincipalsAllowedToRetrieveManagedPassword**

3.  Введите следующие команды в командной строке Windows PowerShell и нажмите клавишу ВВОД:

    **SET-ADServiceAccount [-Name] <string> - PrincipalsAllowedToRetrieveManagedPassword < ADPrincipal [] >**

|Параметр|Строка|Пример|
|-------|-----|------|
|Имя|Имя учетной записи|ITFarm1|
|PrincipalsAllowedToRetrieveManagedPassword|Имена учетных записей компьютеров для входящих в службу узлов или групп безопасности, в которые входят эти узлы|Host1,  Host3|

**Пример**

Например, чтобы удалить входящие в службу узлы, введите следующую команду и нажмите клавишу ВВОД:

```
Get-ADServiceAccount [-Name] ITFarm1 -PrincipalsAllowedToRetrieveManagedPassword

```

```
Set-ADServiceAccount [-Name] ITFarm1 -PrincipalsAllowedToRetrieveManagedPassword Host1,Host3

```

### <a name="BKMK_RemoveGMSA"></a>Шаг 2. Удаление групповой управляемой учетной записи службы из системы
Удалите кэшированные учетные данные групповой управляемой учетной записи службы с входящего в службу узла с помощью API Uninstall-ADServiceAccount или NetRemoveServiceAccount API в системе соответствующего узла.

Минимальным требованием для выполнения этих процедур является членство в группе **Администраторы** или наличие эквивалентных прав.

##### <a name="to-remove-a-gmsa-using-the-uninstall-adserviceaccount-cmdlet"></a>Удаление групповой управляемой учетной записи службы с помощью командлета Uninstall-ADServiceAccount

1.  На контроллере домена Windows Server 2012, запустите Windows PowerShell из панели задач.

2.  Введите следующие команды в командной строке Windows PowerShell и нажмите клавишу ВВОД:

    **Удаление ADServiceAccount < Учетная_запись_службы_ad >**

    **Пример**

    Например, чтобы удалить кэшированные учетные данные групповой управляемой учетной записи службы ITFarm1, введите следующую команду и нажмите клавишу ВВОД:

    ```
    Uninstall-ADServiceAccount ITFarm1
    ```

Для получения дополнительных сведений о командлете Uninstall-ADServiceAccount введите в командной строке модуля Active Directory для Windows PowerShell команду **Get-Help Uninstall-ADServiceAccount**и нажмите клавишу ВВОД либо изучите статью [Uninstall-ADServiceAccount](https://technet.microsoft.com/library/ee617202.aspx)на веб-сайте TechNet.



## <a name="BKMK_Links"></a>См. также

-   [Обзор учетных записей группы управляемых служб](group-managed-service-accounts-overview.md)


