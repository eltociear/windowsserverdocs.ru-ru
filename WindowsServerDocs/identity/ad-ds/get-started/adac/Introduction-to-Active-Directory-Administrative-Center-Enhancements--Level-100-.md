---
ms.assetid: 074e63e9-976c-49da-8cba-9ae0b3325e34
title: "Введение в дополнительные возможности центра администрирования Active Directory (уровень 100)"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 7f52b22ec74ba12c383952e68b412f871a56474c
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/12/2017
---
# <a name="introduction-to-active-directory-administrative-center-enhancements-level-100"></a>Введение в дополнительные возможности центра администрирования Active Directory (уровень 100)

>Область применения: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Центр администрирования Active Directory в Windows Server 2012 включает следующие средства управления:

-   [Корзина Active Directory](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#ad_recycle_bin_mgmt)

-   [Детально настроенной политики паролей](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#fine_grained_pswd_policy_mgmt)

-   [Средство просмотра журнала PowerShell Windows](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#windows_powershell_history_viewer)

## <a name="ad_recycle_bin_mgmt"></a>Корзина Active Directory
Случайное удаление объектов Active Directory — это обычное дело при работе доменных служб Active Directory (AD DS) и служб Active Directory облегченного доступа к каталогам (AD LDS). В прошлых версиях Windows Server до Windows Server 2008 R2 можно было восстановить случайно удаленные объекты в Active Directory, но эти решения имели свои недостатки.

В Windows Server 2008, можно использовать функцию архивации данных Windows Server и **ntdsutil** команду принудительного восстановления, чтобы пометить объекты как заслуживающие доверия и обеспечить репликацию восстановленных данных по всему домену. Недостаток при использовании принудительного восстановления заключался в том, что его приходилось выполнять в режиме восстановления служб каталогов (DSRM). В этом режиме, восстанавливаемого контроллера домена было переводить в автономный режим. Таким образом он не мог обрабатывать клиентские запросы.

В Windows Server 2003 Active Directory и Windows Server 2008, AD DS можно было восстановить удаленные объекты Active Directory при помощи восстановления полностью удаленных объектов. Тем не менее ссылочные атрибуты восстановленных объектов нессылочные атрибуты (например, членство в группах учетных записей пользователей), удаленные физически, и не были восстановлены не ссылочные атрибуты, которые были очищены. Таким образом администраторы не могли полагаться на восстановление полностью удаленных объектов как на гарантированное решение случайном удалении объектов. Дополнительные сведения о восстановлении полностью удаленных объектов см. в разделе [восстановление полностью удаленных объектов Active Directory](https://go.microsoft.com/fwlink/?LinkID=125452).

Корзина Active Directory, начиная с Windows Server 2008 R2 основана на существующей инфраструктуре восстановления полностью удаленных объектов и расширяет возможности сохранения и восстановления случайно удаленных объектов Active Directory.

При включении корзины Active Directory, все ссылочные и сохраняются не нессылочные атрибуты удаленных объектов Active Directory и объекты восстанавливаются в том же логически согласованном состоянии, они находились непосредственно перед удалением их полностью. Например восстановленные учетные записи пользователей автоматически восстанавливают все членства в группах и соответствующие права доступа, которыми они обладали непосредственно перед удалением внутри и вне доменов. Корзина Active Directory работает для сред AD DS и AD LDS. Подробное описание корзины Active Directory см. в разделе [новые в Доменных службах Active Directory: Корзина Active Directory](https://technet.microsoft.com/library/dd391916(WS.10).aspx).

**Новые возможности?** В Windows Server 2012 компонент Корзина Active Directory была дополнена новым графическим интерфейсом пользователя для пользователям восстанавливать удаленные объекты и управлять ими. Пользователи теперь визуально найдите список удаленных объектов и восстановить их в исходное или желаемое местоположение.

Если вы планируете включить корзину Active Directory в Windows Server 2012, учитывайте следующее:

-   По умолчанию Корзина Active Directory отключена. Чтобы включить ее, нужно сначала повысить режим работы леса среды AD DS или AD LDS на Windows Server 2008 R2 или более поздней версии. Это в свою очередь требует, чтобы все контроллеры домена в лесу или все серверы, на которых размещены экземпляры наборов конфигурации AD LDS под управлением Windows Server 2008 R2 или более поздней версии.

-   Процесс включения корзины Active Directory необратим. После включения корзины Active Directory в вашей среде, отключить нельзя.

-   Для управления корзиной через пользовательский интерфейс, необходимо установить версию центра администрирования Active Directory в Windows Server 2012.

    > [!NOTE]
    > Можно использовать **диспетчера сервера** для установки средств удаленного администрирования сервера (RSAT) на компьютерах Windows Server 2012, чтобы использовать правильную версию центра администрирования Active Directory для управления корзиной через пользовательский интерфейс.
    > 
    > Можно использовать [RSAT](https://go.microsoft.com/fwlink/?LinkID=238560) в Windows&reg; 8 компьютерам использовать правильную версию центра администрирования Active Directory для управления корзиной через пользовательский интерфейс.

### <a name="active-directory-recycle-bin-step-by-step"></a>Корзина Active Directory Пошаговое руководство
В следующей пошаговой процедуре вы используете Центр администрирования Active Directory для выполнения следующих задач Корзина Active Directory в Windows Server 2012:

-   [Шаг 1: Повышение режима работы леса](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_raise_ffl)

-   [Шаг 2: Включить корзину](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_enable_recycle_bin)

-   [Шаг 3: Создание тестовых пользователей, группы и подразделения](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_create_test_env)

-   [Шаг 4: Восстановление удаленных объектов](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_restore_del_obj)

> [!NOTE]
> Для выполнения следующих шагов требуется членство в группе администраторов предприятия или эквивалентные разрешения.

### <a name="bkmk_raise_ffl"></a>Шаг 1: Повышение режима работы леса
На этом шаге Вы повысите режим работы леса. Нужно сначала повысить режим работы целевого леса хотя бы Windows Server 2008 R2, прежде чем включить корзину Active Directory.

##### <a name="to-raise-the-functional-level-on-the-target-forest"></a>Чтобы повысить режим работы целевого леса:

1.  Щелкните правой кнопкой мыши значок Windows PowerShell, щелкните **Запуск от имени администратора** и тип **dsac.exe** открыть центр администрирования Active Directory.

2.  Нажмите кнопку **управление**, нажмите кнопку **добавить узлы перехода** и выберите соответствующий целевой домен в **добавить узлы перехода** диалоговое окно, а затем нажмите кнопку **ОК**.

3.  Щелкните целевой домен в левой области навигации и в **задачи** панели, щелкните **Повышение режима работы леса**. Выберите режим работы леса не ниже Windows Server 2008 R2 или более поздней версии и нажмите кнопку **ОК**.

![Введение в центре администрирования AD](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)Windows PowerShell эквивалентные команды ***

Следующий командлет Windows PowerShell или командлеты выполняют ту же функцию, что и предыдущая процедура. Введите каждый командлет в отдельной строке, несмотря на то, что они могут отображаться по здесь несколько строк словам из-за ограничений форматирования.

```
Set-ADForestMode -Identity contoso.com -ForestMode Windows2008R2Forest -Confirm:$false
```

Для **-удостоверения** аргумент, укажите полное DNS-имя.

### <a name="bkmk_enable_recycle_bin"></a>Шаг 2: Включить корзину
На этом шаге вы включите корзину для восстановления удаленных объектов в AD DS.

##### <a name="to-enable-active-directory-recycle-bin-in-adac-on-the-target-domain"></a>Чтобы включить корзину Active Directory в центре администрирования Active Directory в целевом домене:

1.  Щелкните правой кнопкой мыши значок Windows PowerShell, щелкните **Запуск от имени администратора** и тип **dsac.exe** открыть центр администрирования Active Directory.

2.  Нажмите кнопку **управление**, нажмите кнопку **добавить узлы перехода** и выберите соответствующий целевой домен в **добавить узлы перехода** диалоговое окно, а затем нажмите кнопку **ОК**.

3.  В **задачи** панели, щелкните **включить корзину... **в **задачи** панели, щелкните **ОК** в предупреждающем сообщении, а затем нажмите кнопку **ОК** для обновления сообщения центра администрирования Active Directory.

4.  Нажмите клавишу F5, чтобы обновить Центр администрирования Active Directory.

![Введение в центре администрирования AD](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)Windows PowerShell эквивалентные команды ***

Следующий командлет Windows PowerShell или командлеты выполняют ту же функцию, что и предыдущая процедура. Введите каждый командлет в отдельной строке, несмотря на то, что они могут отображаться по здесь несколько строк словам из-за ограничений форматирования.

```
Enable-ADOptionalFeature -Identity 'CN=Recycle Bin Feature,CN=Optional Features,CN=Directory Service,CN=Windows NT,CN=Services,CN=Configuration,DC=contoso,DC=com' -Scope ForestOrConfigurationSet -Target 'contoso.com'
```

### <a name="bkmk_create_test_env"></a>Шаг 3: Создание тестовых пользователей, группы и подразделения
В следующих процедурах вы создадите двух тестовых пользователей. Затем будет создать тестовую группу и добавить тестовых пользователей в группу. Кроме того вы создадите Подразделение.

##### <a name="to-create-test-users"></a>Чтобы создать тестовых пользователей

1.  Щелкните правой кнопкой мыши значок Windows PowerShell, щелкните **Запуск от имени администратора** и тип **dsac.exe** открыть центр администрирования Active Directory.

2.  Нажмите кнопку **управление**, нажмите кнопку **добавить узлы перехода** и выберите соответствующий целевой домен в **добавить узлы перехода** диалоговое окно, а затем нажмите кнопку **ОК**.

3.  В **задачи** панели, щелкните **New** и нажмите кнопку **пользователя**.

    ![Введение в центре администрирования AD](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/ADDS_ADACNewUser.gif)

4.  Введите следующие сведения в разделе **учетной записи** и нажмите кнопку ОК:

    -   Полное имя: test1

    -   Вход пользователя SamAccountName: test1

    -   Пароль:p@ssword1

    -   Подтверждение пароля:p@ssword1

5.  Повторите предыдущие шаги, чтобы создать второго пользователя, test2.

##### <a name="to-create-a-test-group-and-add-users-to-the-group"></a>Чтобы создать тестовую группу и добавить пользователей в группу

1.  Щелкните правой кнопкой мыши значок Windows PowerShell, щелкните **Запуск от имени администратора** и тип **dsac.exe** открыть центр администрирования Active Directory.

2.  Нажмите кнопку **управление**, нажмите кнопку **добавить узлы перехода** и выберите соответствующий целевой домен в **добавить узлы перехода** диалоговое окно, а затем нажмите кнопку **ОК**.

3.  В **задачи** панели, щелкните **New** и нажмите кнопку **группы**.

4.  Введите следующие сведения в разделе **группы** и нажмите кнопку **ОК**:

    -   **Имя группы: group1**

5.  Нажмите кнопку **group1**, а затем в разделе **задачи** панели, щелкните **свойства**.

6.  Нажмите кнопку **члены**, нажмите кнопку **добавить**, тип **test1; test2**, а затем нажмите кнопку **ОК**.

![Введение в центре администрирования AD](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)Windows PowerShell эквивалентные команды ***

Следующий командлет Windows PowerShell или командлеты выполняют ту же функцию, что и предыдущая процедура. Введите каждый командлет в отдельной строке, несмотря на то, что они могут отображаться по здесь несколько строк словам из-за ограничений форматирования.

```
Add-ADGroupMember -Identity group1 -Member test1
```

##### <a name="to-create-an-organizational-unit"></a>Создание подразделения

1.  Щелкните правой кнопкой мыши значок Windows PowerShell, щелкните **Запуск от имени администратора** и тип **dsac.exe** открыть центр администрирования Active Directory.

2.  Нажмите кнопку **управление**, нажмите кнопку **добавить узлы перехода** и выберите соответствующий целевой домен в **добавить узлы перехода** диалоговое окно, а затем нажмите кнопку **ОК**.

3.  В **задачи** панели, щелкните **New** и нажмите кнопку **подразделение**.

4.  Введите следующие сведения в разделе **подразделение** и нажмите кнопку **ОК**:

    -   **NameOU1**

![Введение в центре администрирования AD](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)Windows PowerShell эквивалентные команды ***

Следующий командлет Windows PowerShell или командлеты выполняют ту же функцию, что и предыдущая процедура. Введите каждый командлет в отдельной строке, несмотря на то, что они могут отображаться по здесь несколько строк словам из-за ограничений форматирования.

```
1..2 | ForEach-Object {New-ADUser -SamAccountName test$_ -Name "test$_" -Path "DC=fabrikam,DC=com" -AccountPassword (ConvertTo-SecureString -AsPlainText "p@ssword1" -Force) -Enabled $true}
New-ADGroup -Name "group1" -SamAccountName group1 -GroupCategory Security -GroupScope Global -DisplayName "group1"
New-ADOrganizationalUnit -Name OU1 -Path "DC=fabrikam,DC=com"

```

### <a name="bkmk_restore_del_obj"></a>Шаг 4: Восстановление удаленных объектов
В следующих процедурах вы восстановите удаленные объекты из **удаленные объекты** контейнера в их исходное расположение и в другое расположение.

##### <a name="to-restore-deleted-objects-to-their-original-location"></a>Чтобы восстановить удаленные объекты в их исходное расположение

1.  Щелкните правой кнопкой мыши значок Windows PowerShell, щелкните **Запуск от имени администратора** и тип **dsac.exe** открыть центр администрирования Active Directory.

2.  Нажмите кнопку **управление**, нажмите кнопку **добавить узлы перехода** и выберите соответствующий целевой домен в **добавить узлы перехода** диалоговое окно, а затем нажмите кнопку **ОК**.

3.  Выберите пользователей **test1** и **test2**, нажмите кнопку **удалить** в **задачи** панели, а затем нажмите кнопку **Да** для подтверждения удаления.

    ![Введение в центре администрирования AD](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)Windows PowerShell эквивалентные команды ***

    Следующий командлет Windows PowerShell или командлеты выполняют ту же функцию, что и предыдущая процедура. Введите каждый командлет в отдельной строке, несмотря на то, что они могут отображаться по здесь несколько строк словам из-за ограничений форматирования.

    ```
    Get-ADUser -Filter 'Name -Like "*test*"'|Remove-ADUser -Confirm:$false
    ```

4.  Перейдите к **удаленные объекты** контейнер, выберите **test2** и **test1** и нажмите кнопку **восстановить** в **задачи** области.

5.  Чтобы убедиться, что объекты были восстановлены в их исходное расположение, перейдите в целевой домен и убедитесь, что учетные записи пользователей указаны.

    > [!NOTE]
    > Если вы перейдете к **свойства** учетных записей пользователей **test1** и **test2** и нажмите кнопку **входит в состав**, вы увидите, что их членство в группах также было восстановлено.

Следующий командлет Windows PowerShell или командлеты выполняют ту же функцию, что и предыдущая процедура. Введите каждый командлет в отдельной строке, несмотря на то, что они могут отображаться по здесь несколько строк словам из-за ограничений форматирования.

![Введение в центре администрирования AD](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)Windows PowerShell эквивалентные команды ***

```
Get-ADObject -Filter 'Name -Like "*test*"' -IncludeDeletedObjects | Restore-ADObject
```

##### <a name="to-restore-deleted-objects-to-a-different-location"></a>Чтобы восстановить удаленные объекты в другое расположение

1.  Щелкните правой кнопкой мыши значок Windows PowerShell, щелкните **Запуск от имени администратора** и тип **dsac.exe** открыть центр администрирования Active Directory.

2.  Нажмите кнопку **управление**, нажмите кнопку **добавить узлы перехода** и выберите соответствующий целевой домен в **добавить узлы перехода** диалоговое окно, а затем нажмите кнопку **ОК**.

3.  Выберите пользователей **test1** и **test2**, нажмите кнопку **удалить** в **задачи** панели, а затем нажмите кнопку **Да** для подтверждения удаления.

4.  Перейдите к **удаленные объекты** контейнер, выберите **test2** и **test1** и нажмите кнопку **восстановить в** в **задачи** области.

5.  Выберите **OU1** и нажмите кнопку **ОК**.

6.  Чтобы убедиться, что объекты были восстановлены в **OU1**, перейдите в целевой домен, дважды щелкните **OU1** и проверьте, указаны учетные записи пользователей.

![Введение в центре администрирования AD](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)Windows PowerShell эквивалентные команды ***

Следующий командлет Windows PowerShell или командлеты выполняют ту же функцию, что и предыдущая процедура. Введите каждый командлет в отдельной строке, несмотря на то, что они могут отображаться по здесь несколько строк словам из-за ограничений форматирования.

```
Get-ADObject -Filter 'Name -Like "*test*"' -IncludeDeletedObjects | Restore-ADObject -TargetPath "OU=OU1,DC=contoso,DC=com"
```

## <a name="fine_grained_pswd_policy_mgmt"></a>Детально настроенной политики паролей
Операционная система Windows Server 2008 предоставляет организациям возможность определить разные пароли и политики блокирования учетных записей для разных групп пользователей в домене. В доменах Active Directory до Windows Server 2008 только одна политика паролей и политики блокировки учетных записей можно применить ко всем пользователям в домене. Эти политики устанавливались в политике домена по умолчанию для данного домена. В результате организации, которые хотели установить разные параметры паролей и учетной записи блокировки для разных групп пользователей приходилось создавать фильтр паролей, либо развертывать несколько доменов. Оба варианта требуют высоких затрат.

Чтобы указать несколько политик паролей в одном домене и применять различные ограничения для паролей и политики блокирования учетных для разных групп пользователей в домене, можно использовать детально настроенные политики паролей. Например можно применить более строгие параметры для привилегированных учетных записей и меньше strict учетным записям других пользователей. В других случаях можно применять особую политику паролей для учетных записей, пароли которых синхронизируются с другими источниками данных. Подробное описание детально настроенной политики паролей см. в разделе [Доменных службах Active Directory: детально настроенные политики паролей](https://technet.microsoft.com/library/cc770394(WS.10).aspx)

**Новые возможности?** В Windows Server 2012 управления политики сложных паролей стало более простым и наглядным благодаря пользовательскому интерфейсу, администраторам AD DS управлять этими политиками в центре администрирования Active Directory. Администраторы могут теперь просматривать результирующую политику для конкретного пользователя, просматривать и сортировать все политики паролей в данном домене и визуально управлять отдельными политиками паролей.

Если вы планируете использовать детально настроенные политики паролей в Windows Server 2012, учитывайте следующее:

-   Детальные политики паролей применяются только глобальные группы безопасности и пользовательских объектов (или к объектам inetOrgPerson, если они используются вместо пользовательских объектов). По умолчанию только члены группы администраторов домена можно задать детально настроенные политики паролей. Тем не менее можно делегировать возможность устанавливать эти политики для других пользователей. Режим работы домена должен быть Windows Server 2008 или более поздней версии.

-   Чтобы администрировать детально настроенные политики паролей через графический интерфейс пользователя, необходимо использовать версию Windows Server 2012 Центр администрирования Active Directory.

    > [!NOTE]
    > Можно использовать **диспетчера сервера** для установки средств удаленного администрирования сервера (RSAT) на компьютерах Windows Server 2012, чтобы использовать правильную версию центра администрирования Active Directory для управления корзиной через пользовательский интерфейс.
    > 
    > Можно использовать [RSAT](https://go.microsoft.com/fwlink/?LinkID=238560) в Windows&reg; 8 компьютерам использовать правильную версию центра администрирования Active Directory для управления корзиной через пользовательский интерфейс.

### <a name="fine-grained-password-policy-step-by-step"></a>Пошаговые детально настроенной политики паролей
В следующей пошаговой процедуре вы используете Центр администрирования Active Directory для выполнения следующих задач политики сложных паролей:

-   [Шаг 1: Повышение режима работы домена](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_raise_dfl)

-   [Шаг 2: Создание тестовых пользователей, группы и подразделения](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk2_test_fgpp)

-   [Шаг 3: Создание новой детально настроенной политики паролей](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_create_fgpp)

-   [Шаг 4: Просмотр результирующего набора политик для пользователя](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_view_resultant_fgpp)

-   [Шаг 5: Изменение детально настроенной политики паролей](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_edit_fgpp)

-   [Шаг 6: Удаление детально настроенной политики паролей](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_delete_fgpp)

> [!NOTE]
> Для выполнения следующих шагов требуется членство в группе администраторов домена или эквивалентные разрешения.

#### <a name="bkmk_raise_dfl"></a>Шаг 1: Повышение режима работы домена
В следующей процедуре Вы повысите режим работы домена целевого домена до Windows Server 2008 или более поздней версии. Чтобы включить детально настроенные политики паролей требуется режим работы домена Windows Server 2008 или более поздней версии.

###### <a name="to-raise-the-domain-functional-level"></a>Чтобы повысить режим работы домена

1.  Щелкните правой кнопкой мыши значок Windows PowerShell, щелкните **Запуск от имени администратора** и тип **dsac.exe** открыть центр администрирования Active Directory.

2.  Нажмите кнопку **управление**, нажмите кнопку **добавить узлы перехода** и выберите соответствующий целевой домен в **добавить узлы перехода** диалоговое окно, а затем нажмите кнопку **ОК**.

3.  Щелкните целевой домен в левой области навигации и в **задачи** панели, щелкните **Повышение режима работы домена**. Выберите режим работы леса не ниже Windows Server 2008 или более поздней версии, а затем нажмите кнопку **ОК**.

![Введение в центре администрирования AD](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)Windows PowerShell эквивалентные команды ***

Следующий командлет Windows PowerShell или командлеты выполняют ту же функцию, что и предыдущая процедура. Введите каждый командлет в отдельной строке, несмотря на то, что они могут отображаться по здесь несколько строк словам из-за ограничений форматирования.

```
Set-ADDomainMode -Identity contoso.com -DomainMode 3
```

#### <a name="bkmk2_test_fgpp"></a>Шаг 2: Создание тестовых пользователей, группы и подразделения
Чтобы создать тестовых пользователей и группу для данного этапа, выполните процедуры, описанные здесь: [шаг 3: Создание тестовых пользователей, группы и подразделения](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_create_test_env) (не необходимо для демонстрации детально настроенной политики паролей создавать Подразделение).

#### <a name="bkmk_create_fgpp"></a>Шаг 3: Создание новой детально настроенной политики паролей
В следующей процедуре вы создадите новый детальную политику паролей с помощью пользовательского интерфейса в центре администрирования Active Directory.

###### <a name="to-create-a-new-fine-grained-password-policy"></a>Чтобы создать новую детально настроенную политику паролей

1.  Щелкните правой кнопкой мыши значок Windows PowerShell, щелкните **Запуск от имени администратора** и тип **dsac.exe** открыть центр администрирования Active Directory.

2.  Нажмите кнопку **управление**, нажмите кнопку **добавить узлы перехода** и выберите соответствующий целевой домен в **добавить узлы перехода** диалоговое окно, а затем нажмите кнопку **ОК**.

3.  В области навигации центра администрирования Active Directory откройте **системы** контейнера, а затем нажмите кнопку **контейнер параметров пароля**.

4.  В **задачи** области, нажмите кнопку **New**, а затем нажмите кнопку **параметры пароля**.

    Заполните или измените содержимое полей на странице свойств для создания нового **параметры пароля** объекта. **Имя** и **приоритет** поля являются обязательными.

    ![Введение в центре администрирования AD](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/ADDS_ADACNewFGPP.gif)

5.  В разделе **применяется напрямую к**, нажмите кнопку **добавить**, тип **group1**, а затем нажмите кнопку **ОК**.

    Объект политики паролей будет связан с членами глобальной группы, которую вы создали для тестовой среды.

6.  Нажмите кнопку **ОК** чтобы подтвердить создание.

![Введение в центре администрирования AD](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)Windows PowerShell эквивалентные команды ***

Следующий командлет Windows PowerShell или командлеты выполняют ту же функцию, что и предыдущая процедура. Введите каждый командлет в отдельной строке, несмотря на то, что они могут отображаться по здесь несколько строк словам из-за ограничений форматирования.

```
New-ADFineGrainedPasswordPolicy TestPswd -ComplexityEnabled:$true -LockoutDuration:"00:30:00" -LockoutObservationWindow:"00:30:00" -LockoutThreshold:"0" -MaxPasswordAge:"42.00:00:00" -MinPasswordAge:"1.00:00:00" -MinPasswordLength:"7" -PasswordHistoryCount:"24" -Precedence:"1" -ReversibleEncryptionEnabled:$false -ProtectedFromAccidentalDeletion:$true
Add-ADFineGrainedPasswordPolicySubject TestPswd -Subjects group1
```

#### <a name="bkmk_view_resultant_fgpp"></a>Шаг 4: Просмотр результирующего набора политик для пользователя
В следующей процедуре вы просмотрите параметры результирующего пароля для пользователя, который является членом группы, для которой вы установили детально настроенную политику паролей в [шаг 3: Создание новой детально настроенной политики паролей](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_create_fgpp).

###### <a name="to-view-a-resultant-set-of-policies-for-a-user"></a>Просмотр результирующего набора политик для пользователя

1.  Щелкните правой кнопкой мыши значок Windows PowerShell, щелкните **Запуск от имени администратора** и тип **dsac.exe** открыть центр администрирования Active Directory.

2.  Нажмите кнопку **управление**, нажмите кнопку **добавить узлы перехода** и выберите соответствующий целевой домен в **добавить узлы перехода** диалоговое окно, а затем нажмите кнопку **ОК**.

3.  Выберите пользователя, **test1**, относящийся к группе, **group1** которой вы связали детально настроенной политики паролей в [шаг 3: Создание новой детально настроенной политики паролей](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_create_fgpp).

4.  Нажмите кнопку **просмотреть итоговые параметры пароля** в **задачи** области.

5.  Изучите политику параметров паролей и нажмите кнопку **отменить**.

![Введение в центре администрирования AD](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)Windows PowerShell эквивалентные команды ***

Следующий командлет Windows PowerShell или командлеты выполняют ту же функцию, что и предыдущая процедура. Введите каждый командлет в отдельной строке, несмотря на то, что они могут отображаться по здесь несколько строк словам из-за ограничений форматирования.

```
Get-ADUserResultantPasswordPolicy test1
```

#### <a name="bkmk_edit_fgpp"></a>Шаг 5: Изменение детально настроенной политики паролей
В следующей процедуре вы измените детально настроенную политику паролей был создан в [шаг 3: Создание новой детально настроенной политики паролей](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_create_fgpp)

###### <a name="to-edit-a-fine-grained-password-policy"></a>Чтобы изменить детально настроенной политики паролей

1.  Щелкните правой кнопкой мыши значок Windows PowerShell, щелкните **Запуск от имени администратора** и тип **dsac.exe** открыть центр администрирования Active Directory.

2.  Нажмите кнопку **управление**, нажмите кнопку **добавить узлы перехода** и выберите соответствующий целевой домен в **добавить узлы перехода** диалоговое окно, а затем нажмите кнопку **ОК**.

3.  В центре Администрирования **панели навигации**, разверните **системы** и нажмите кнопку **контейнер параметров пароля**.

4.  Выберите детально настроенную политику паролей был создан в [шаг 3: Создание новой детально настроенной политики паролей](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_create_fgpp) и нажмите кнопку **свойства** в **задачи** области.

5.  В разделе **вести журнал паролей**, измените значение параметра **количество запоминаемых паролей** для **30**.

6.  Нажмите кнопку **ОК**.

![Введение в центре администрирования AD](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)Windows PowerShell эквивалентные команды ***

Следующий командлет Windows PowerShell или командлеты выполняют ту же функцию, что и предыдущая процедура. Введите каждый командлет в отдельной строке, несмотря на то, что они могут отображаться по здесь несколько строк словам из-за ограничений форматирования.

```
Set-ADFineGrainedPasswordPolicy TestPswd -PasswordHistoryCount:"30"
```

#### <a name="bkmk_delete_fgpp"></a>Шаг 6: Удаление детально настроенной политики паролей

###### <a name="to-delete-a-fine-grained-password-policy"></a>Удаление детально настроенной политики паролей

1.  Щелкните правой кнопкой мыши значок Windows PowerShell, щелкните **Запуск от имени администратора** и тип **dsac.exe** открыть центр администрирования Active Directory.

2.  Нажмите кнопку **управление**, нажмите кнопку **добавить узлы перехода** и выберите соответствующий целевой домен в **добавить узлы перехода** диалоговое окно, а затем нажмите кнопку **ОК**.

3.  В области навигации центра администрирования Active Directory, разверните **системы** и нажмите кнопку **контейнер параметров пароля**.

4.  Выберите детально настроенную политику паролей был создан в [шаг 3: Создание новой детально настроенной политики паролей](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_create_fgpp) и в **задачи** щелкните **свойства**.

5.  Очистить **защитить от случайного удаления** флажок и нажмите кнопку **ОК**.

6.  Выберите детально настроенную политику паролей и в **задачи** щелкните **удалить**.

7.  Нажмите кнопку **ОК** в диалоговом окне подтверждения.

![Введение в центре администрирования AD](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)Windows PowerShell эквивалентные команды ***

Следующий командлет Windows PowerShell или командлеты выполняют ту же функцию, что и предыдущая процедура. Введите каждый командлет в отдельной строке, несмотря на то, что они могут отображаться по здесь несколько строк словам из-за ограничений форматирования.

```
Set-ADFineGrainedPasswordPolicy -Identity TestPswd -ProtectedFromAccidentalDeletion $False
Remove-ADFineGrainedPasswordPolicy TestPswd -Confirm
```

## <a name="windows_powershell_history_viewer"></a>Средство просмотра журнала PowerShell Windows
Центр администрирования Active Directory является надстраивается над Windows PowerShell средство пользовательского интерфейса.  В Windows Server 2012 ИТ-администраторы могут использовать Центр администрирования Active Directory для изучения Windows PowerShell для Active Directory командлеты с помощью средства просмотра журнала Windows PowerShell. При выполнении действий в пользовательском интерфейсе, для пользователя в средстве просмотра журнала Windows PowerShell видит эквивалентную команду Windows PowerShell. Это позволяет администраторам создавать автоматические сценарии и сокращать повторяющиеся задачи, тем самым повышая производительность ИТ-ресурсов.  Кроме того эта функция позволяет сократить время, необходимое для изучения Windows PowerShell для Active Directory и повышает уверенность пользователей в правильности их сценариев автоматизации.

При использовании средства просмотра журнала Windows PowerShell в Windows Server 2012 учитывайте следующее:

-   Чтобы использовать средство просмотра сценариев Windows PowerShell, необходимо использовать версию Windows Server 2012 Центр администрирования Active Directory

    > [!NOTE]
    > Можно использовать **диспетчера сервера** для установки средств удаленного администрирования сервера (RSAT) на компьютерах Windows Server 2012, чтобы использовать правильную версию центра администрирования Active Directory для управления корзиной через пользовательский интерфейс.
    > 
    > Можно использовать [RSAT](https://go.microsoft.com/fwlink/?LinkID=238560) в Windows&reg; 8 компьютерам использовать правильную версию центра администрирования Active Directory для управления корзиной через пользовательский интерфейс.

-   Требуются базовые знания Windows PowerShell. Например вам нужно знать принципы конвейерной передачи в Windows PowerShell. Дополнительные сведения о конвейерной передаче в Windows PowerShell см. в разделе [конвейерная передача и конвейер в Windows PowerShell](https://technet.microsoft.com/library/ee176927.aspx).

### <a name="windows-powershell-history-viewer-step-by-step"></a>Просмотра журнала Windows PowerShell Пошаговое руководство
В следующей процедуре используется средство просмотра журнала Windows PowerShell в центре администрирования Active Directory для создания сценария Windows PowerShell.  Прежде чем приступать к процедуре, удалите пользователя **test1** из группы, **group1**.

##### <a name="to-construct-a-script-using-powershell-history-viewer"></a>Чтобы создать сценарий с помощью средства просмотра журнала PowerShell

1.  Щелкните правой кнопкой мыши значок Windows PowerShell, щелкните **Запуск от имени администратора** и тип **dsac.exe** открыть центр администрирования Active Directory.

2.  Нажмите кнопку **управление**, нажмите кнопку **добавить узлы перехода** и выберите соответствующий целевой домен в **добавить узлы перехода** диалоговое окно, а затем нажмите кнопку **ОК**.

3.  Разверните **журнал Windows PowerShell** панели в нижней части экрана Центр администрирования Active Directory.

4.  Выберите пользователя **test1**.

5.  Нажмите кнопку **добавить группу... **в **задачи** области.

6.  Перейдите к **group1** и нажмите кнопку **ОК** в диалоговом окне.

7.  Перейдите к **журнал Windows PowerShell** панель и найдите только что созданную команду.

8.  Скопируйте эту команду и вставьте его в предпочтительный редактор для создания сценария.

    Например, можно изменить команду, чтобы добавить другого пользователя для **group1**, или добавить **test1** в другую группу.

## <a name="see-also"></a>См. также:
[Управления Дополнительно AD DS, используя Центр администрирования Active Directory & #40; Уровень 200 & #41;](Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-.md)

