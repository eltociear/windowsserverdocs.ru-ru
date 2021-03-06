---
title: Добавление серверов в диспетчер серверов
description: Диспетчер сервера
ms.prod: windows-server
ms.technology: manage-server-manager
ms.topic: article
ms.assetid: aab895f2-fe4d-4408-b66b-cdeadbd8969e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.localizationpriority: medium
ms.date: 02/01/2018
ms.openlocfilehash: f7b5a5b358fa2df54777e0f1f88b1e86a7dafd80
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851577"
---
# <a name="add-servers-to-server-manager"></a>Добавление серверов в диспетчер серверов

>Область применения: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

В Windows Server можно управлять несколькими удаленными серверами с помощью единой консоли диспетчера серверов. Серверы, которыми вы хотите управлять с помощью диспетчера серверов, могут работать под управлением Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 или Windows Server 2008. Обратите внимание, что нельзя управлять более новыми версиями Windows Server с помощью старого выпуска диспетчера серверов.

В этом разделе описывается, как добавлять серверы в пул серверов диспетчера серверов.

> [!NOTE]
> Согласно проведенным тестам, в Windows Server 2012 и более поздних выпусках Windows Server диспетчер серверов можно использовать для управления до 100 серверами, настроенными на выполнение обычной рабочей нагрузки. Число серверов, которыми можно управлять, используя единую консоль диспетчера серверов, зависит от количества данных, запрашиваемых от управляемых серверов, а также от аппаратных и сетевых ресурсов, доступных на компьютере, на котором выполняется диспетчер серверов. По мере приближения количества отображаемых данных к пределам производственной мощности ресурсов компьютера могут наблюдаться замедление отклика от диспетчера серверов и задержка выполнения обновлений. Чтобы увеличить количество серверов, которыми можно управлять с помощью диспетчера серверов, рекомендуется ограничить количество данных событий, которые диспетчер серверов получает от управляемых серверов, задав соответствующие параметры в диалоговом окне **Настройка данных события**. Окно настройки показа событий можно открыть из меню **Задачи** в плитке **События**. Крупные организации с большим количеством серверов могут воспользоваться продуктами из пакета [Microsoft System Center](https://go.microsoft.com/fwlink/p/?LinkId=239437).
> 
> Диспетчер серверов может получать от серверов с запущенной Windows Server 2003 только состояния "В сети" и "Не в сети". Несмотря на то что диспетчер серверов используется для управления серверами с операционной системой Windows Server 2008 R2 или Windows Server 2008, невозможно добавить роли и компоненты к серверам с системами Windows Server 2008 R2, Windows Server 2008 или Windows Server 2003.
> 
> Диспетчер серверов нельзя использовать для управления более новыми выпусками операционной системы Windows Server. Диспетчер серверов под управлением Windows Server 2012 R2, Windows Server 2012, Windows 8.1 или Windows 8 нельзя использовать для управления серверами под управлением Windows Server 2016.

В этом разделе содержатся следующие подразделы:

-   [Добавление серверов для управления](#BKMK_add)

-   [Ввод учетных данных с помощью команды "Управление как"](#BKMK_creds)

## <a name="provide-credentials-with-the-manage-as-command"></a><a name=BKMK_creds></a>Ввод учетных данных с помощью команды "Управление как"
При добавлении удаленных серверов в диспетчер серверов некоторые из добавленных серверов могут требовать учетные данные другой учетной записи пользователя для доступа к ним или управления ими. Чтобы указать учетные данные для управляемого сервера, отличные от используемых для входа на компьютер, на котором работает диспетчер серверов, воспользуйтесь командой **Manage As** после добавления сервера в диспетчер серверов, которую можно вызвать, щелкнув правой кнопкой мыши запись для управляемого сервера в плитке **Серверы** домашней страницы роли или группы. Если щелкнуть команду **Manage As**, откроется диалоговое окно **Безопасность Windows**, в котором можно ввести имя пользователя, имеющего права доступа на управляемом сервере, в одном из следующих форматов.

-   *Имя пользователя*

-   *Имя пользователя*@example.domain.com

-   *Домен*\\*Имя пользователя*

Диалоговое окно **Безопасность Windows**, которое открывается командой **Manage As**, не может принимать учетные данные смарт-карты; предоставление учетных данных смарт-карты через диспетчер серверов не поддерживается. Учетные данные, предоставленные для управляемого сервера с помощью команды **Manage As**, кэшируются и сохраняются до тех пор, пока вы управляете сервером с помощью того же компьютера, на котором в текущий момент работает диспетчер серверов, или до тех пор, пока вы их не переопределите, указав пустые или другие учетные данные для этого сервера. При экспорте параметров диспетчера серверов на другие компьютеры или настройке перемещаемого профиля домена, чтобы разрешить использование параметров диспетчера серверов на других компьютерах, учетные данные **Manage As** для серверов в вашем пуле серверов не сохраняются в перемещаемом профиле. Пользователи диспетчера серверов должны добавлять их на каждом компьютере, с которого им необходимо осуществлять управление.

После добавления серверов для управления с помощью следующих процедур, приводимых в этом разделе, но перед использованием команды **Manage As** для указания альтернативных учетных данных, необходимых для управления добавленным сервером, для этого сервера могут отображаться следующие ошибки состояния управляемости:

-   Ошибка разрешения целевого компьютера Kerberos

-   Ошибка проверки подлинности Kerberos

-   В сети: отказано в доступе

> [!NOTE]
> Роли и компоненты, которые не поддерживают команду **Manage As**: службы удаленных рабочих столов (RDS) и сервер управления IP-адресами (IPAM). Если вы не можете управлять удаленным сервером RDS или IPAM с помощью учетных данных, используемых на компьютере, на котором работает диспетчер серверов, попробуйте добавить учетную запись, которая обычно используется для управления этими удаленными серверами, в группу администраторов на компьютере с диспетчером серверов. Затем войдите на компьютер, на котором работает диспетчер серверов, с учетной записью, которая используется для управления удаленным сервером, на котором работает RDS или IPAM.

## <a name="add-servers-to-manage"></a><a name=BKMK_add></a>Добавление серверов для управления
Диспетчер серверов позволяет добавлять серверы для управления в диалоговом окне **Добавление серверов** тремя способами.

-   **Доменные службы Active Directory** — добавление серверов, найденных Active Directory в том же домене, что и локальный компьютер.

-   **Запись службы доменных имен (DNS)** — поиск серверов для управления по имени или IP-адресу компьютера.

-   **Импорт нескольких серверов** — выбирается несколько серверов для импортирования в файл, в котором серверы отсортированы по имени компьютера или IP-адресу.

#### <a name="to-add-servers-to-the-server-pool"></a>Добавление серверов в пул

1.  Если диспетчер серверов уже открыт, переходите к следующему шагу. Если диспетчер серверов еще не открыт, откройте его одним из следующих способов.

    -   На рабочем столе Windows запустите диспетчер серверов, щелкнув **Диспетчер серверов** на панели задач Windows.

    -   На **начальном экране** Windows выберите плитку "Диспетчер серверов".

2.  В меню **Управление** выберите команду **Добавить серверы**.

3.  Выполните одно из указанных ниже действий.

    -   На вкладке **Active Directory** выберите серверы, находящиеся в текущем домене. Чтобы выделить несколько серверов, удерживайте нажатой клавишу **CTRL**. Нажмите кнопку со стрелкой вправо, чтобы переместить выбранные серверы в список **Выбрано**.

    -   На вкладке **DNS** введите первые несколько символов имени или IP-адреса компьютера, а затем нажмите клавишу **ВВОД** или кнопку **Поиск**. Выберите серверы, которые вы хотите добавить, и нажмите кнопку со стрелкой вправо.

    -   На вкладке **Импорт** найдите текстовый файл, содержащий DNS-имена или IP-адреса компьютеров, которые нужно добавить, в котором в каждой строке располагается одно имя или один IP-адрес.

4.  После добавления серверов нажмите кнопку **ОК**.

### <a name="add-and-manage-servers-in-workgroups"></a>Добавление серверов рабочих групп и управление ими
В некоторых случаях после добавления входящих в рабочие группы серверов в диспетчер серверов в столбце **Управляемость** плитки **Серверы** на странице роли или группы, включающей в себя сервер рабочей группы, могут отображаться ошибки **Учетные данные недействительны**, которые возникают при попытках подключиться к удаленному серверу рабочей группы или получить данные от него.

Эти или аналогичную ошибки могут возникать в следующих ситуациях.

-   Когда управляемый сервер находится в той же рабочей группе, что и компьютер с диспетчером серверов.

-   Когда управляемый сервер находится в рабочей группе, отличной от рабочей группы, в которой находится компьютер с диспетчером серверов.

-   Один из компьютеров находится в рабочей группе, а другой — в домене.

-   Компьютер, на котором работает диспетчер серверов, является членом рабочей группы, а удаленные управляемые серверы находятся в другой подсети.

-   Оба компьютера находятся в доменах, но между этими доменами отсутствуют отношения доверия.

-   Оба компьютера находятся в доменах, но между этими доменами существует только одностороннее отношение доверия.

-   Сервер, которым требуется управлять, был добавлен с использованием его IP-адреса.

##### <a name="to-add-remote-workgroup-servers-to-server-manager"></a>Добавление удаленных серверов рабочей группы в диспетчер сервера

1.  На компьютере с диспетчером серверов добавьте имя сервера рабочей группы в список **TrustedHosts**. Это требуется для проверки подлинности NTLM. Чтобы добавить имя компьютера в существующий список доверенных узлов, добавьте в команду параметр `Concatenate` . Например, чтобы добавить компьютер `Server01` к существующему списку доверенных узлов, примените следующую команду.

    ```
    Set-Item wsman:\localhost\Client\TrustedHosts Server01 -Concatenate -force
    ```

2.  Определите, находится ли сервер рабочей группы, которым требуется управлять, в той же подсети, что и компьютер с диспетчером серверов.

    Если эти два компьютера находятся в одной подсети или для сетевого профиля сервера рабочей группы задано значение **Частный** в **Центре управления сетями и общим доступом**, переходите к следующему шагу.

    Если они находятся в разных подсетях или для сетевого профиля компьютера рабочей группы не установлено значение **Частный**, то на компьютере рабочей группы измените параметр **Служба удаленного управления Windows (HTTP — входящий трафик)** брандмауэра Windows, чтобы явно разрешить подключение с удаленных компьютеров путем добавления их имен на вкладке **Компьютеры** диалогового окна **Свойства** для этого параметра.

3.  > [!IMPORTANT]
    > На этом шаге выполнение командлета переопределяет ограничения контроля учетных записей (UAC), которые запрещают запуск процессов с повышенными правами на компьютерах рабочей группы, если это делается не от имени встроенной учетной записи администратора или системной учетной записи. Данный командлет позволяет членам группы администраторов управлять сервером рабочей группы без входа в систему с встроенной учетной записью администратора. Допуск дополнительных пользователей к управлению сервером рабочей группы может повысить риск угрозы безопасности, однако это менее рискованно, чем предоставление учетных данных встроенной учетной записи администратора нескольким людям, управляющим сервером рабочей группы.

    Чтобы переопределить ограничения на выполнение процессов с повышенными правами на компьютерах рабочей группы, которые налагаются контролем учетных записей, создайте в реестре сервера рабочей группы раздел под названием **LocalAccountTokenFilterPolicy**, выполнив следующий командлет.

    ```
    New-ItemProperty -Name LocalAccountTokenFilterPolicy -path HKLM:\SOFTWARE\Microsoft\Windows\Currentversion\Policies\System -propertytype DWord -value 1
    ```

4.  На компьютере, на котором выполняется диспетчер серверов, откройте страницу **Все серверы** .

5.  Если компьютер, на котором работает диспетчер серверов, и целевой сервер рабочей группы состоят в одной рабочей группе, переходите к последнему шагу. Если эти два компьютера не принадлежат к одной рабочей группе, щелкните правой кнопкой мыши целевой сервер рабочей группы на плитке **Серверы** и выберите **Управлять как**.

6.  Войдите на сервер рабочей группы с встроенной учетной записью администратора этого сервера.

7.  Убедитесь, что диспетчер серверов может подключаться к серверу рабочей группы и получать от него данные, обновив страницу **Все серверы** и просмотрев состояние управления для этого сервера.

##### <a name="to-add-remote-servers-when-server-manager-is-running-on-a-workgroup-computer"></a>Добавление удаленных серверов, если диспетчер сервера выполняется на компьютере рабочей группы

1.  На компьютере, на котором работает диспетчер серверов, добавьте удаленные серверы в список **TrustedHosts** в рамках сеанса Windows PowerShell. Чтобы добавить имя компьютера в существующий список доверенных узлов, добавьте в команду параметр `Concatenate` . Например, чтобы добавить компьютер `Server01` к существующему списку доверенных узлов, примените следующую команду.

    ```
    Set-Item wsman:\localhost\Client\TrustedHosts Server01 -Concatenate -force
    ```

2.  Определите, находится ли сервер, которым требуется управлять, в той же подсети, что и компьютер рабочей группы с диспетчером серверов.

    Если эти два компьютера находятся в одной подсети или для сетевого профиля компьютера рабочей группы задано значение **Частный** в **Центре управления сетями и общим доступом**, переходите к следующему шагу.

    Если они находятся в разных подсетях или для сетевого профиля компьютера рабочей группы не установлено значение **Частный**, то на компьютере рабочей группы с диспетчером серверов измените параметр **Служба удаленного управления Windows (HTTP — входящий трафик)** брандмауэра Windows, чтобы явно разрешить подключение с удаленных компьютеров путем добавления их имен на вкладке **Компьютеры** диалогового окна **Свойства** для этого параметра.

3.  На компьютере, на котором выполняется диспетчер серверов, откройте страницу **Все серверы** .

4.  Убедитесь, что диспетчер серверов может подключаться к удаленному серверу и получать от него данные, обновив страницу **Все серверы** и просмотрев состояние управления для этого сервера. Если на плитке **Серверы** для удаленного сервера по-прежнему отображается сообщение об ошибке управления, перейдите к следующему шагу.

5.  Выйдите из системы на компьютере, на котором работает диспетчер серверов, а затем снова войдите в систему с использованием встроенной учетной записи администратора. Повторите предыдущий шаг, чтобы убедиться, что диспетчер серверов может подключаться к удаленному серверу и получать от него данные.

Если после выполнения описанных выше действий проблемы при управлении компьютерами рабочих групп или при управлении другими компьютерами с компьютеров рабочих групп не будут устранены, см. раздел [Сведения об удаленной диагностике](https://technet.microsoft.com/library/dd347642.aspx) на веб-сайте Майкрософт.

### <a name="add-and-manage-servers-in-clusters"></a>Добавление серверов и управление ими
Вы можете использовать диспетчер серверов для управления серверами, которые находятся в отказоустойчивых кластерах (также называемых кластерами серверов или MSCS). Серверы в отказоустойчивых кластерах (в зависимости от того, являются ли они физическими или виртуальными узлами кластера) имеют некоторые особенности поведения и ограничения управления в диспетчере серверов.

-   Как физические, так и виртуальные серверы в кластерах автоматически добавляются в диспетчер серверов, когда один сервер из этого кластера добавляется в диспетчер серверов. Аналогично, при удалении кластерного сервера из диспетчера серверов, вам будет предложено удалить остальные серверы в этом кластере.

-   Диспетчер серверов не отображает данные для кластерных виртуальных серверов, так как эти данные являются динамическими и идентичны данным для сервера, на котором размещается этот виртуальный кластерный узел. Вы можете выбрать сервер, на котором размещается виртуальный сервер, чтобы просмотреть его данные.

-   При добавлении сервера в диспетчер серверов с использованием имени виртуального кластерного объекта сервера, в диспетчере серверов отображается имя виртуального объекта вместо имени физического сервера (ожидаемого).

-   Нельзя устанавливать роли и компоненты на кластерном виртуальном сервере.

## <a name="see-also"></a>См. также
[Диспетчер серверов](server-manager.md)
[Создание и управление группами серверов](create-and-manage-server-groups.md)
