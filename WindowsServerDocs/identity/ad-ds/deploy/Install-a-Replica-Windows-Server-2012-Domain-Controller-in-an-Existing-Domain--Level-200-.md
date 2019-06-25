---
ms.assetid: e6da5984-d99d-4c34-9c11-4a18cd413f06
title: Установка реплики контроллера домена Windows Server 2012 в существующем домене (уровень 200)
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: cb4432084386cb3296163f24c801be1c74b379df
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2019
ms.locfileid: "59883045"
---
# <a name="install-a-replica-windows-server-2012-domain-controller-in-an-existing-domain-level-200"></a>Установка реплики контроллера домена Windows Server 2012 в существующем домене (уровень 200)

>Область применения. Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

В этом разделе рассматриваются действия, необходимые для обновления существующего леса или домена до Windows Server 2012 с помощью диспетчера сервера или Windows PowerShell. В нем описывается, как добавить контроллеры домена с ОС Windows Server 2012 в существующий домен.  
  
-   [Обновление и рабочий процесс репликации](../../ad-ds/deploy/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-.md#BKMK_Workflow)  
  
-   [Обновление и реплики Windows PowerShell](../../ad-ds/deploy/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-.md#BKMK_PS)  
  
-   [Развертывание](../../ad-ds/deploy/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-.md#BKMK_Dep)  
  
## <a name="BKMK_Workflow"></a>Обновление и рабочий процесс репликации  
На схеме ниже показан процесс настройки доменных служб Active Directory. Предполагается, что вы ранее установили роль доменных служб Active Directory и запустили мастер настройки доменных служб Active Directory с помощью диспетчера сервера, чтобы создать контроллер домена в существующем домене.  
  
![Установка реплики](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/adds_forestupgrade.png)  
  
## <a name="BKMK_PS"></a>Обновление и реплики Windows PowerShell  
  
|||  
|-|-|  
|**Командлет ADDSDeployment**|Аргументы (аргументы, выделенные**жирным шрифтом** , являются обязательными. Аргументы, выделенные*курсивом* , можно указать с помощью Windows PowerShell или мастера настройки доменных служб Active Directory).|  
|Install-AddsDomainController|-SkipPreChecks<br /><br />***-DomainName***<br /><br />*-SafeModeAdministratorPassword*<br /><br />*-SiteName*<br /><br />*-ADPrepCredential*<br /><br />-ApplicationPartitionsToReplicate<br /><br />*-AllowDomainControllerReinstall*<br /><br />-Confirm<br /><br />*-CreateDNSDelegation*<br /><br />***-Credential***<br /><br />-CriticalReplicationOnly<br /><br />*-DatabasePath*<br /><br />*-DNSDelegationCredential*<br /><br />-Force<br /><br />*-InstallationMediaPath*<br /><br />*-InstallDNS*<br /><br />*-LogPath*<br /><br />-MoveInfrastructureOperationMasterRoleIfNecessary<br /><br />-NoDnsOnNetwork<br /><br />*-NoGlobalCatalog*<br /><br />-Norebootoncompletion<br /><br />*-ReplicationSourceDC*<br /><br />-SkipAutoConfigureDNS<br /><br />-SiteName<br /><br />*-SystemKey*<br /><br />*-SYSVOLPath*<br /><br />*-UseExistingAccount*<br /><br />*-Whatif*|  
  
> [!NOTE]  
> Аргумент **-credential** требуется только в том случае, если вы еще не вошли как член групп "Администраторы предприятия" и "Администраторы схемы" (при обновлении леса) или группы "Администраторы домена" (при добавлении нового контроллера домена в существующий домен).  
  
## <a name="BKMK_Dep"></a>Развертывание  
  
### <a name="deployment-configuration"></a>Deployment Configuration  
![Установка реплики](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradeDeployConfig.png)  
  
Повышение роли каждого контроллера домена начинается в диспетчере сервера на странице **Конфигурация развертывания** . Оставшиеся параметры и обязательные поля меняются на этой и последующих страницах в зависимости от того, какая операция развертывания выбрана.  
  
Чтобы обновить существующий лес или добавить доступный для записи контроллер домена в существующий домен, установите переключатель в положение **Добавить контроллер домена в существующий домен** и нажмите кнопку **Выбрать** в разделе **Укажите сведения о домене для этой операции**. При необходимости диспетчер серверов запрашивает действующие учетные данные.  
  
Для обновления леса в Windows Server 2012 требуются учетные данные, включающие членство в группах "Администраторы предприятия" и "Администраторы схемы". Мастер настройки доменных служб Active Directory позднее выдает предупреждение, если у текущих учетных данных нет соответствующих разрешений или если они не включены в группы.  
  
Автоматическое выполнение процесса Adprep — это единственное различие между добавлением контроллера домена в существующий домен Windows Server 2012 и домен, в котором контроллеры домена работают под управлением более ранней версии Windows Server.  
  
Командлет и аргументы модуля Windows PowerShell ADDSDeployment:  
  
```  
Install-AddsDomainController  
-domainname <string>  
-credential <pscredential>  
```  
  
![Установка реплики](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradeCreds.png)  
  
![Установка реплики](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradeSelectDomain.png)  
  
На каждой странице выполняются определенные тесты, некоторые из которых проводятся повторно позднее как отдельные проверки предварительных требований. Например, если выбранный домен не отвечают требованию к минимальному режиму работы, вам не придется проходить всю процедуру повышения роли вплоть до проверки предварительных требований, чтобы получить в итоге следующее сообщение:  
  
![Установка реплики](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradeFFLError.png)  
  
### <a name="domain-controller-options"></a>Параметры контроллера домена  
![Установка реплики](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradeDCOptions.png)  
  
На странице **Параметры контроллера домена** показаны возможности настройки нового контроллера домена. Они включают в себя **DNS-сервер**, **Глобальный каталог** и **Контроллер домена только для чтения**. Корпорация Майкрософт рекомендует, чтобы все контроллеры домена предоставляли службы DNS и глобального каталога для обеспечения высокой доступности в распределенных средах. Глобальный каталог всегда выбран по умолчанию, а DNS-сервер выбран по умолчанию в том случае, если в текущем домене уже размещены службы DNS в контроллерах домена на основе запроса начальной записи зоны. Страница **Параметры контроллера домена** также позволяет выбрать из конфигурации леса соответствующее логичное **имя сайта** Active Directory. По умолчанию выбирается сайт с наиболее подходящей подсетью. Если существует только один сайт, он выбирается автоматически.  
  
> [!NOTE]  
> Если сервер не входит в подсеть Active Directory и имеется несколько сайтов Active Directory, выбор не производится и кнопка **Далее** останется неактивной до тех пор, пока не будет выбран сайт из списка.  
  
Указанный **пароль для режима восстановления служб каталогов** должен соответствовать политике паролей, действующей для сервера. Необходимо всегда выбирать надежный и сложный пароль, предпочтительно парольную фразу.  
  
Аргументы ADDSDeployment, эквивалентные параметрам на странице **Параметры контроллера домена** :  
  
```  
-InstallDNS <{$false | $true}>  
-NoGlobalCatalog <{$false | $true}>  
-sitename <string>  
-SafeModeAdministratorPassword <secure string>  
```  
  
> [!IMPORTANT]  
> Имя сайта уже должно существовать на момент ввода в качестве аргумента для **-sitename**. Командлет **install-AddsDomainController** не создает сайты. Для создания сайтов можно использовать командлет **new-adreplicationsite**.  
  
Аргумент **SafeModeAdministratorPassword** действует особым образом.  
  
-   Если этот аргумент *не указан* , командлет предлагает ввести и подтвердить скрытый пароль. Это предпочтительный вариант использования при интерактивном выполнении командлета.  
  
    Например, чтобы создать дополнительный контроллер домена в домене treyresearch.net с выводом запроса на ввод и подтверждение скрытого пароля, выполните следующую команду:  
  
    ```  
    Install-ADDSDomainController "DomainName treyresearch.net "credential (get-credential)  
    ```  
  
-   Если аргумент указан *со значением*, это значение должно быть защищенной строкой. Это не является предпочтительным вариантом использования при интерактивном выполнении командлета.  
  
Например, можно вручную ввести запрос пароля с помощью командлета **Read-Host**, чтобы запрашивать у пользователя ввод защищенной строки.  
  
```  
-safemodeadministratorpassword (read-host -prompt "Password:" -assecurestring)  
```  
  
> [!WARNING]  
> Поскольку в предыдущем варианте пароль не подтверждается, соблюдайте повышенную осторожность: пароль невидим.  
  
Можно также ввести защищенную строку в качестве переменной с преобразованным открытым текстом, хотя использовать такой вариант настоятельно не рекомендуется.  
  
```  
-safemodeadministratorpassword (convertto-securestring "Password1" -asplaintext -force)  
  
```  
  
Наконец, можно сохранить скрытый пароль в файле, а затем использовать его повторно, никогда не отображая пароль в виде открытого текста. Пример:  
  
```  
$file = "c:\pw.txt"  
$pw = read-host -prompt "Password:" -assecurestring  
$pw | ConvertFrom-SecureString | Set-Content $file  
  
-safemodeadministratorpassword (Get-Content $File | ConvertTo-SecureString)  
  
```  
  
> [!WARNING]  
> Ввод или хранение пароля в виде открытого или скрытого текста не рекомендуется. Любой пользователь, выполняющий эту команду в скрипты или заглядывающий через ваше плечо, сможет узнать пароль DSRM этого доменного контроллера.  Любой пользователь, имеющий доступ к файлу, сможет восстановить скрытый пароль. Зная пароль, он сможет войти в контроллер домена, запущенный в режиме восстановления служб каталогов, и персонифицировать сам контроллер домена, повысив уровень собственных привилегий в лесу Active Directory до максимального уровня. Рекомендуется выполнить дополнительные действия для шифрования данных текстового файла с помощью **System.Security.Cryptography**, однако их рассмотрение выходит за рамки этой статьи. Лучше всего полностью отказаться от хранения паролей.  
  
Командлет ADDSDeployment предлагает дополнительную возможность пропустить автоматическую настройку параметров DNS-клиента, серверов пересылки и корневых ссылок. При использовании диспетчера сервера пропустить эту настройку нельзя. Этот аргумент имеет значение только в том случае, если роль DNS-сервера была установлена до настройки контроллера домена:  
  
```  
-SkipAutoConfigureDNS  
```  
  
На странице **Параметры контроллера домена** выводится предупреждение о том, что нельзя создать контроллеры домена только для чтения, если существующие контроллеры домена работают под управлением Windows Server 2003. Это ожидаемое предупреждение, и его можно пропустить.  
  
![Установка реплики](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradeDCOptionsError.png)  
  
### <a name="dns-options-and-dns-delegation-credentials"></a>Параметры DNS и учетные данные для делегирования DNS  
![Установка реплики](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradeDNSOptions.png)  
  
На странице **Параметры DNS** можно настроить делегирование DNS, если вы выбрали параметр **DNS-сервер** на странице *Параметры контроллера домена* и указана зона, в которой разрешено делегирование DNS. Может потребоваться предоставить другие учетные данные, принадлежащие пользователю, который является членом группы **Администраторы DNS** .  
  
Аргументы командлета ADDSDeployment, эквивалентные параметрам на странице **Параметры DNS** :  
  
```  
-creatednsdelegation   
-dnsdelegationcredential <pscredential>  
```  
  
![Установка реплики](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradeCreds.png)  
  
Подробнее о необходимости создания DNS-делегирования см. в статье [Общее представление о делегировании зоны](https://technet.microsoft.com/library/cc771640.aspx).  
  
### <a name="additional-options"></a>Дополнительные параметры  
![Установка реплики](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradeAdditionalOptions.png)  
  
На странице **Дополнительные параметры** приводится параметр конфигурации, позволяющий указать имя контроллера домена, используемого в качестве источника репликации.  
  
Также можно установить контроллер домена с помощью архивированных носителей, использовав параметр установки с носителя (IFM). При установке флажка **Установка с носителя** появляется возможность выбора носителя. Чтобы убедиться в том, что указанный путь является действительным путем к носителю, необходимо нажать кнопку **Проверить** . Носители, используемые параметром IFM, создаются с помощью системы архивации данных Windows Server или Ntdsutil.exe только из другого существующего компьютера с Windows Server 2012. Windows Server 2008 R2 или операционные системы более ранних версий не подходят для создания носителей для контроллера домена с Windows Server 2012. Подробнее об изменениях в IFM см. в разделе [Приложение: упрощенное администрирование](../../ad-ds/deploy/Simplified-Administration-Appendix.md). Если носители защищены SYSKEY, диспетчер сервера запрашивает пароль образа во время проверки.  
  
![Установка реплики](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_NtdsutilIFM.png)  
  
Ниже перечислены аргументы командлета ADDSDeployment, эквивалентные параметрам на странице **Дополнительные параметры** .  
  
```  
-replicationsourcedc <string>  
-installationmediapath <string>  
-syskey <secure string>  
```  
  
### <a name="paths"></a>Paths  
![Установка реплики](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradePaths.png)  
  
Страница **Пути** позволяет переопределить расположение папок по умолчанию для базы данных AD DS, журналов транзакций базы данных и общего доступа к SYSVOL. Расположение по умолчанию всегда в подкаталогах %systemroot%.  
  
Аргументы командлета ADDSDeployment, эквивалентные параметрам на странице "Пути":  
  
```  
-databasepath <string>  
-logpath <string>  
-sysvolpath <string>  
```  
  
### <a name="preparation-options"></a>Параметры подготовки  
![Установка реплики](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradePrepOptions.png)  
  
На странице **Параметры подготовки** выводится оповещение о том, что настройка доменных служб Active Directory включает в себя расширение схемы (forestprep) и обновление домена (domainprep).  Эта страница появляется только в том случае, если лес и домен не были подготовлены в ходе предыдущей установки контроллера домена Windows Server 2012 или путем запуска средства Adprep.exe вручную. Например, мастер настройки доменных служб Active Directory подавляет эту страницу, если вы добавляете новый контроллер домена в существующий корневой домен леса Windows Server 2012.  
  
Расширение схемы и обновление домена не производятся после нажатия кнопки **Далее**. Эти операции выполняются только во время этапа установки. На этой странице просто сообщается о событиях, которые будут происходить позднее в ходе установки.  
  
На этой странице также проверяется, является ли текущий пользователь членом групп "Администраторы схемы" и "Администраторы предприятия". Членство в этих группах необходимо для расширения схемы и подготовки домена. Если на странице указано, что текущие учетные данные не дают необходимых разрешений, нажмите кнопку **Изменить**, чтобы предоставить соответствующие учетные данные пользователя.  
  
![Установка реплики](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradePrepOptionsCreds.png)  
  
Аргумент командлета ADDSDeployment, эквивалентный параметрам на странице "Дополнительные параметры":  
  
```  
-adprepcredential <pscredential>  
```  
  
> [!IMPORTANT]  
> Так же как и в предыдущих версиях Windows Server, при автоматической подготовке домена для контроллеров домена с Windows Server 2012 средство GPPREP не запускается. Выполните команду **adprep.exe /gpprep** вручную для всех доменов, которые не были ранее подготовлены для Windows Server 2003, Windows Server 2008 или Windows Server 2008 R2. Средство GPPrep следует запустить только один раз за историю домена, а не при каждом обновлении. Средство Adprep.exe не выполняет команду /gpprep автоматически, так как это может привести к повторной репликации всех файлов и папок из тома SYSVOL во всех контроллерах домена.  
>   
> Средство RODCPrep запускается автоматически при повышении роли первого контроллера RODC без предварительной подготовки в домене. Этого не происходит при повышении роли первого доступного для записи контроллера домена Windows Server 2012. Если планируется развертывать контроллеры домена только для чтения, команду **adprep.exe /rodcprep** также можно выполнить вручную.  
  
### <a name="review-options-and-view-script"></a>"Просмотреть параметры" и "Просмотреть скрипт"  
![Установка реплики](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradeReviewOptions.png)  
  
Страница **Просмотреть параметры** позволяет проверить параметры перед установкой и убедиться, что они отвечают требованиям. Позднее установку также можно будет остановить с помощью диспетчера сервера. Эта страница позволяет просмотреть и подтвердить параметры перед продолжением конфигурации.  
  
На странице **Просмотреть параметры** диспетчера сервера расположена дополнительная кнопка **Просмотреть скрипт** , предназначенная для создания текстового файла в кодировке Юникод, содержащего текущую конфигурацию развертывания ADDSDeployment в виде единого скрипта Windows PowerShell. Это позволяет использовать графический интерфейс диспетчера сервера в качестве студии развертывания Windows PowerShell. С помощью мастера настройки доменных служб Active Directory необходимо настроить параметры, экспортировать конфигурацию и затем отменить мастер.  Во время этого процесса создается допустимый и синтаксически верный образец для дальнейшего изменения или прямого использования.  
  
Пример:  
  
```  
#  
# Windows PowerShell Script for AD DS Deployment  
#  
Import-Module ADDSDeployment  
Install-ADDSDomainController `  
-CreateDNSDelegation `  
-Credential (Get-Credential) `  
-CriticalReplicationOnly:$false `  
-DatabasePath "C:\Windows\NTDS" `  
-DomainName "root.fabrikam.com" `  
-InstallDNS:$true `  
-LogPath "C:\Windows\NTDS" `  
-SiteName "Default-First-Site-Name" `  
-SYSVOLPath "C:\Windows\SYSVOL"  
-Force:$true  
  
```  
  
> [!NOTE]  
> Диспетчер сервера обычно задает значения для всех аргументов при повышении роли, не полагаясь на значения по умолчанию (так как они могут изменяться в будущих версиях Windows или пакетах обновления). Единственным исключением является аргумент **-safemodeadministratorpassword** . Для принудительного вывода запроса на подтверждение не указывайте значение при интерактивном выполнении командлета.  
>   
> Для просмотра сведений о конфигурации воспользуйтесь необязательным аргументом **Whatif** с командлетом **Install-ADDSDomainController**. Это позволит просмотреть явные и неявные значения аргументов командлета.  
  
![Установка реплики](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_PSWhatIf.png)  
  
### <a name="prerequisites-check"></a>Проверка готовности к установке  
![Установка реплики](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradePrereqCheck.png)  
  
**Проверка предварительных требований** — это новая функция настройки доменных служб Active Directory. На этом новом этапе проверяется возможность поддержки нового контроллера домена Windows Server 2012 доменом и лесом.  
  
При установке нового контроллера домена мастер настройки доменных служб Active Directory в диспетчере сервера последовательно выполняет серию модульных тестов. При этом предлагаются рекомендуемые способы восстановления. Тесты можно выполнять необходимое число раз. Установка контроллера домена не может продолжаться, пока все проверки предварительных требований не будут пройдены.  
  
На странице **Проверка предварительных требований** также приводится важная информация, например сведения об изменениях в системе безопасности, затрагивающих предыдущие операционные системы.  
  
Подробнее о проверках предварительных требований см. в разделе [Prerequisite Checking](../../ad-ds/manage/AD-DS-Simplified-Administration.md#BKMK_PrereuisiteChecking).  
  
При использовании диспетчера сервера пропустить **проверку предварительных требований** нельзя, однако это можно сделать при использовании командлета развертывания доменных служб Active Directory с помощью следующего аргумента:  
  
```  
-skipprechecks  
  
```  
  
> [!WARNING]  
> Корпорация Майкрософт не рекомендует пропускать проверку предварительных требований, так как это может привести к частичному повышению роли контроллера домена или повреждению леса Active Directory.  
  
Чтобы начать повышение роли контроллера домена, нажмите кнопку **Установить** . Это последняя возможность отменить установку. После того как процесс повышения роли начнется, отменить его будет невозможно. По завершении повышения роли компьютер автоматически перезагрузится вне зависимости от результата процесса. На странице **Проверка предварительных требований** выводится информация обо всех неполадках, выявленных в ходе проверки, и рекомендации по их устранению.  
  
### <a name="installation"></a>Установка  
![Установка реплики](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradeInstallProgress.png)  
  
Когда появляется страница **Установка** , это означает, что настройка контроллера домена началась и ее нельзя остановить или отменить. Подробная информация об операциях выводится на этой странице и записывается в следующие журналы:  
  
-   %systemroot%\debug\dcpromo.log  
  
-   %systemroot%\debug\dcpromoui.log  
  
-   %systemroot%\debug\adprep\logs  
  
-   %systemroot%\debug\netsetup.log (если сервер входит в рабочую группу)  
  
Чтобы установить новый лес Active Directory с помощью модуля ADDSDeployment, используйте следующий командлет:  
  
```  
Install-addsdomaincontroller  
```  
  
Список обязательных и необязательных аргументов см. в разделе [Обновление и добавление реплики с помощью Windows PowerShell](../../ad-ds/deploy/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-.md#BKMK_PS).  
  
Выполнение командлета **Install-AddsDomainController** включает только два этапа (проверка предварительных требований и установка). На двух иллюстрациях ниже показан этап установки с минимальным необходимым набором аргументов: **-domainname** и **-credential**. Обратите внимание на то, что операция Adprep выполняется автоматически в рамках добавления первого контроллера домена Windows Server 2012 в существующий лес Windows Server 2003:  
  
![Установка реплики](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_PSGetCred.png)  
  
Обратите внимание на то, что командлет **Install-ADDSDomainController** , как и диспетчер сервера, напоминает об автоматической перезагрузке сервера после повышения роли. Чтобы автоматически закрывать напоминание о перезагрузке, используйте аргументы **-force** или **-confirm:$false** с любым командлетом Windows PowerShell ADDSDeployment. Чтобы предотвратить автоматическую перезагрузку сервера по завершении повышения роли, используйте аргумент **-norebootoncompletion** .  
  
> [!WARNING]  
> Отключать перезагрузку не рекомендуется. Для правильной работы контроллер домена должен перезагрузиться.  
  
![Установка реплики](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_PSUpgradeConfirm.gif)  
  
![Установка реплики](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_PSUpgradeProgress.png)  
  
Чтобы удаленно настроить контроллер домена с помощью Windows PowerShell, заключите командлет **install-adddomaincontroller***в* командлет **invoke-command**. Для этого необходимо использовать фигурные скобки.  
  
```  
invoke-command {install-addsdomaincontroller "domainname <domain> -credential (get-credential)} -computername <dc name>  
```  
  
Пример:  
  
![Установка реплики](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_PSUpgradeExample.gif)  
  
> [!NOTE]  
> Дополнительные сведения о том, как выполняется установка и процесс Adprep, см. в разделе [Troubleshooting Domain Controller Deployment](../../ad-ds/deploy/Troubleshooting-Domain-Controller-Deployment.md).  
  
### <a name="results"></a>Результаты  
![Установка реплики](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_ForestSignOff.png)  
  
На странице **Результаты** показано, успешно ли было выполнено повышение роли, а также приводится важная для администраторов информация. В случае успешного выполнения контроллер домена автоматически перезагрузится через 10 секунд.  
  
Так же как и в предыдущих версиях Windows Server, при автоматической подготовке домена для контроллеров домена с Windows Server 2012 средство GPPREP не запускается. Выполните команду **adprep.exe /gpprep** вручную для всех доменов, которые не были ранее подготовлены для Windows Server 2003, Windows Server 2008 или Windows Server 2008 R2. Средство GPPrep следует запустить только один раз за историю домена, а не при каждом обновлении. Средство Adprep.exe не выполняет команду /gpprep автоматически, так как это может привести к повторной репликации всех файлов и папок из тома SYSVOL во всех контроллерах домена.  
  
