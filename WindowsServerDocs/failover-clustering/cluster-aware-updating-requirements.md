---
ms.assetid: 75cc1d24-fa2f-45bd-8f3b-1bbd4a1aead0
title: "Кластерное обновление требования и рекомендации"
ms.prod: windows-server-threshold
ms.topic: article
ms.manager: dongill
author: JasonGerend
ms.author: jgerend
ms.technology: storage-failover-clustering
ms.date: 4/28/2017
description: "Требования для использования кластерного обновления для установки обновлений в кластерах с ОС Windows Server."
ms.openlocfilehash: 8517466d58345077af446c1b2c1e2aeb3b17aaa1
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/17/2017
---
# <a name="cluster-aware-updating-requirements-and-best-practices"></a>Кластерное обновление требования и рекомендации

>Применяется к: Windows Server (канал точками годовой), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

В этом разделе описываются требования и зависимости, которые необходимы для использования [кластерное обновление](cluster-aware-updating.md) (CAU) для применения обновлений в отказоустойчивый кластер под управлением Windows Server.
  
> [!NOTE]  
> Может потребоваться самостоятельно проверить готовность кластерной среды к применению обновлений, если вы используете модулей в, отличным от **Microsoft.WindowsUpdatePlugin**. Если вы используете отличных корпорации Майкрософт в модулей, обратитесь к издателю Дополнительные сведения. Дополнительные сведения о модулях модулей см. в разделе [модулей Общие сведения о модулях](cluster-aware-updating-plug-ins.md).   
  
## <a name="BKMK_REQ_CLUS"></a>Установка компонента отказоустойчивости кластеров и средств отказоустойчивости кластеров  
CAU необходимо установить компонент отказоустойчивой кластеризации и средств отказоустойчивости кластеров. Средства отказоустойчивости кластеров включают \(clusterawareupdating.dll\) средства CAU, командлеты отказоустойчивой кластеризации и другие компоненты, необходимые для операций CAU. Инструкции по установке компонента отказоустойчивости кластеров см. в разделе [Установка средства отказоустойчивости кластеров и инструментов](http://go.microsoft.com/fwlink/p/?LinkId=253342).  
  
Требования установки для средства отказоустойчивости кластеров зависят от того, координирует ли компонент CAU обновления как кластерная роль в отказоустойчивом кластере \ (с помощью mode\ многоразовый обновления) или с удаленного компьютера. Режим многоразовый обновления CAU необходимо дополнительно установить кластерную роль CAU в отказоустойчивом кластере с помощью средств CAU.    
  
В следующей таблице представлены требования к установке компонента кластерного обновления для двух режимов обновления CAU.  
  
|Установленный компонент|Режим многоразовый обновления|Режим Remote\ обновления|  
|-----------------------|-----------------------|-------------------------|  
|Средство отказоустойчивости кластеров|Требуется во всех узлах кластера|Требуется во всех узлах кластера|  
|Средства отказоустойчивости кластеров|Требуется во всех узлах кластера|-Требуемые обновления remote\ компьютера<br />-Требуется во всех узлах кластера для выполнения [Save-CauDebugTrace](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/save-caudebugtrace) командлета|  
|Кластерная роль CAU|Обязательно|Не требуется|  
  
## <a name="obtain-an-administrator-account"></a>Получить учетную запись администратора  
Для использования компонентов CAU требуются следующим требованиям к администратору.  
  
-   Для просмотра или применения обновлений с помощью пользовательского интерфейса CAU \(UI\) или командлетов кластерного обновления, необходимо использовать учетную запись домена с правами и разрешениями локального администратора на всех узлах кластера. Если учетная запись не имеет достаточных полномочий на каждом узле, предлагается в окне кластерное обновление предоставить необходимые учетные данные при выполнении этих действий. Чтобы использовать [кластерное обновление](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating) командлетов, можно предоставить необходимые учетные данные в виде параметра командлета.  
  
-   При использовании CAU в режим обновления remote\ вы выполнили вход, используя учетную запись, которая не имеет прав и разрешений локального администратора на узлах кластера, вам необходимо запустить средства CAU от имени администратора, с помощью учетной записи локального администратора на компьютере координатора обновлений или с помощью учетной записи с **имитация клиента после проверки подлинности** право пользователя. 
  
-   Для запуска анализатора соответствия рекомендациям для кластерного обновления, необходимо использовать учетную запись с правами администратора на узлах кластера и правами локального администратора на компьютере, который использовался для запуска [Test-CauSetup](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/test-causetup) командлета или анализа с помощью окна кластерное обновление готовности к обновлению кластера. Дополнительные сведения см. в разделе [готовности к обновлению кластера теста](#BKMK_BPA).  
  
## <a name="verify-the-cluster-configuration"></a>Проверка конфигурации кластера  
Ниже приведены общие требования для отказоустойчивого кластера для поддержки обновлений с помощью CAU. Дополнительные требования к конфигурации для удаленного управления на узлах, перечислены в [Настройка узлов для удаленного управления](#BKMK_NODE_CONFIG) далее в этом разделе.  
  
-   Достаточное число узлов кластера должно быть доступно, поэтому, в кластере был кворум.  
  
-   Все узлы кластера должны быть в том же домене Active Directory.  
  
-   Имя кластера должно разрешаться в сети, с помощью DNS.  
  
-   Если кластерное обновление используется в режим обновления remote\, компьютер координатора обновлений должен иметь сетевое подключение для узлов отказоустойчивого кластера, и он должен находиться в домене Active Directory в отказоустойчивом кластере.  
  
-   Служба кластеров должна работать на всех узлах кластера. По умолчанию эта служба устанавливается на всех узлах кластера и настроена на автоматический запуск.  
  
-   Чтобы использовать предварительно обновления или обновления post\ сценариев PowerShell во время прогона обновления CAU, убедитесь, что они установлены на всех узлах кластера или что они доступны для всех узлов, например, в общей папке высокой доступности сети. Если сценарии сохранены в общей сетевой папке, настройте для разрешение на чтение для этой группы.  
  
## <a name="BKMK_NODE_CONFIG"></a>Настройка узлов для удаленного управления  
Чтобы использовать кластерное обновление, все узлы кластера необходимо настроить для удаленного управления. По умолчанию, единственной задачей необходимо выполнить для настройки узлов для удаленного управления, является [Включение правила брандмауэра для обеспечения автоматического перезапуска](#BKMK_FW). 

В следующей таблице перечислены требования к завершения удаленного управления, в случае среды отличается от значения по умолчанию.

Эти требования дополняют требования для установки [установки компонента отказоустойчивой кластеризации и средств отказоустойчивости кластеров](#BKMK_REQ_CLUS) и общие кластеризации требований, описанных в предыдущих подразделах этого раздела.  
  
|Требования|Состояние по умолчанию|Режим многоразовый обновления|Режим Remote\ обновления|  
|---------------|---|-----------------------|-------------------------|  
|[Включение правила брандмауэра для обеспечения автоматического перезапуска](#BKMK_FW)|Отключено|Требуется во всех узлах кластера, если используется брандмауэр|Требуется во всех узлах кластера, если используется брандмауэр|  
|[Включение инструментария управления Windows](#BKMK_WMI)|Включен|Требуется во всех узлах кластера|Требуется во всех узлах кластера|  
|[Включение Windows PowerShell 3.0 или 4.0 и удаленного взаимодействия Windows PowerShell](#BKMK_PS)|Включен|Требуется во всех узлах кластера|Требуется во всех узлах кластера выполните следующую команду:<br /><br />- [Save-CauDebugTrace](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/save-caudebugtrace) командлета<br />-Сценариев PowerShell, предварительно обновления и обновления post\ во время прогона обновления<br />-Тестов с помощью окна кластерное обновление готовности к обновлению кластера или [Test\ CauSetup](http://go.microsoft.com/fwlink/p/?LinkId=242384) командлета Windows PowerShell|  
|[Установка .NET Framework 4.6 или 4,5](#BKMK_NET)|Включен|Требуется во всех узлах кластера|Требуется во всех узлах кластера выполните следующую команду:<br /><br />- [Save-CauDebugTrace](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/save-caudebugtrace) командлета<br />-Сценариев PowerShell, предварительно обновления и обновления post\ во время прогона обновления<br />-Тестов с помощью окна кластерное обновление готовности к обновлению кластера или [Test\ CauSetup](http://go.microsoft.com/fwlink/p/?LinkId=242384) командлета Windows PowerShell|  

### <a name="BKMK_FW"></a>Включение правила брандмауэра для обеспечения автоматического перезапуска  
Для обеспечения автоматического перезапуска после применения обновлений \ (если установки обновления требуется restart\), если в узлах кластера используется брандмауэр Windows или брандмауэр отличных Майкрософт, правило брандмауэра должно быть включено на каждом узле, разрешающее следующий трафик:  
  
-   Протокол: TCP  
  
-   Направление: входящий  
  
-   Программа: wininit.exe  
  
-   Порты: Динамические порты RPC  
  
-   Профиль: домен  
  
Если на узлах кластера используется брандмауэр Windows, это можно сделать, включив **удаленное завершение работы** группу правил брандмауэра Windows на каждом узле кластера. Когда вы используете окно кластерного обновления для применения обновлений и настройки параметров обновления многоразовый, **удаленное завершение работы** группу правил брандмауэра Windows включается автоматически на каждом узле кластера.  
  
> [!NOTE]  
> **Удаленное завершение работы** группу правил брандмауэра Windows нельзя включить, если она вступит в конфликт с параметрами групповой политики, настроенными для брандмауэра Windows.    
  
**Удаленное завершение работы** группу правил брандмауэра, также можно включить путем указания **– EnableFirewallRules** параметра при выполнении следующих командлетов: [Add-CauClusterRole](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/add-cauclusterrole), [Invoke-CauRun](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/invoke-causcan), и [SetCauClusterRole](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/set-cauclusterrole).  
  
В следующем примере PowerShell дополнительный способ включения автоматического перезапуска в узле кластера.  
  
```PowerShell  
Set-NetFirewallRule -Group "@firewallapi.dll,-36751" -Profile Domain -Enabled true  
```  

### <a name="BKMK_WMI"></a>Включение инструментария управления Windows (WMI) 
Все узлы кластера необходимо настроить удаленное управление с помощью \(WMI\) инструментария управления Windows. Этот параметр включен по умолчанию.  
  
Чтобы включить удаленное управление вручную, выполните следующие действия.  
  
1.  В консоли службы, запустите **удаленного управления Windows** обслуживания и задайте для нее тип запуска **автоматического**.  
  
2.  Запустите [Set-WSManQuickConfig](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.wsman.management/set-wsmanquickconfig) или следующую команду из с повышенными привилегиями командной строки:  
  
    ```PowerShell  
    winrm quickconfig -q  
    ```  
  
Для поддержки удаленного взаимодействия WMI, если в узлах кластера используется брандмауэр Windows, правило брандмауэра для **\(HTTP\-In\) удаленного управления Windows** должна быть включена на каждом узле.  Это правило включено по умолчанию.  
  
### <a name="BKMK_PS"></a>Включение Windows PowerShell и удаленное взаимодействие Windows PowerShell  
Чтобы включить режим обновления многоразовый и некоторых функций CAU в режим обновления remote\, PowerShell необходимо установить и включить выполнение удаленных команд на всех узлах кластера. По умолчанию устанавливается и включается удаленное взаимодействие PowerShell.  
  
Чтобы включить удаленное взаимодействие PowerShell, используйте один из следующих методов:  
  
-   Запустите [Enable-PSRemoting](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/enable-psremoting) командлета.  
  
-   Настройка параметра групповой политики уровня domain\ для \(WinRM\) удаленного управления Windows.  
  
Дополнительные сведения о включении удаленного взаимодействия PowerShell см. в разделе [about\_Remote\_Requirements](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/about/about_remote_requirements).  
  
### <a name="BKMK_NET"></a>Установка .NET Framework 4.6 или 4,5  
Чтобы включить режим обновления многоразовый и некоторых функций CAU в режим обновления remote\ .NET Framework 4.6 и .NET Framework 4.5 (в Windows Server 2012 R2) необходимо установить на всех узлах кластера. По умолчанию устанавливается .NET Framework.  

Чтобы установить .NET Framework 4.6 (или 4.5) с помощью PowerShell, если она еще не установлена, используйте следующую команду:

```PowerShell
Install-WindowsFeature -Name NET-Framework-45-Core
```

## <a name="BKMK_BEST_PRAC"></a>Рекомендации по использованию кластерного обновления 
  
### <a name="BKMK_BP_WUA"></a>Рекомендации по применению обновлений Майкрософт

Рекомендуется перед началом использования CAU для применения обновлений по умолчанию **Microsoft.WindowsUpdatePlugin** модулей в кластере, остановить с помощью других методов установки обновлений программного обеспечения от корпорации Майкрософт на узлах кластера.  
  
> [!CAUTION]  
> Одновременное использование CAU и методов, автоматическое обновление отдельных узлов \ (на schedule\ заданное время) может привести к непредсказуемым результатам — вплоть до прерывания обслуживания и незапланированных простоев.  
  
Мы рекомендуем выполнить следующие указания:  
  
-   Для получения оптимальных результатов рекомендуется отключить параметры на узлах кластера для автоматического обновления, например, параметры автоматического обновления на панели управления или параметры, настроенные с помощью групповой политики.  
  
    > [!CAUTION]  
    > Автоматическая установка обновлений на узлах кластера может помешать установке обновлений с помощью кластерного обновления и может привести к сбоям CAU.  
  
    При необходимости, следующие параметры автоматического обновления совместимы с CAU, так как администратор может управлять временем установки обновлений:  
  
    -   Параметры для уведомления перед загрузкой обновлений и уведомлять перед установкой  
  
    -   Параметры обновления загружаются автоматически и уведомлять перед установкой  
  
    Тем не менее если служба автоматического обновления загружает обновления одновременно прогона обновления CAU, выполнение обновления может занять больше времени.  
  
-   Не настраивайте систему обновления, такие как Windows Server Update Services \(WSUS\) для применения обновления автоматически \ (на schedule\ заданное время) на узлах кластера.  
  
-   На всех узлах кластера должно быть настроено использовать тот же источник обновления, например, WSUS сервера, Центр обновления Windows или Центра обновления Майкрософт.  
  
-   При использовании системы управления конфигурацией для обновления программного обеспечения на компьютерах в сети отмените все обязательные и автоматические обновления узлов кластера. Примеры систем управления конфигурацией включают Microsoft System Center Configuration Manager 2007 и Microsoft System Center Virtual Machine Manager 2008.  
  
-   Если серверы распространения программного обеспечения внутренней \ (например, servers\ WSUS), используются для содержат и развертывать обновления, убедитесь, что эти серверы правильно определяют утвержденные обновления для узлов кластера.  
  
#### <a name="BKMK_PROXY"></a>Применение обновлений Майкрософт в филиалах  
Для загрузки обновлений Майкрософт из центра обновления Майкрософт или Центра обновления Windows на узлы кластера в некоторых филиалах, может потребоваться настроить параметры прокси-сервера для учетной записи Local System в каждом узле. Например необходимо сделать это, если кластеры в филиалах получают доступ к центра обновления Майкрософт или Центра обновления Windows для загрузки обновлений с помощью локальный прокси-сервер.  
  
При необходимости настройте параметры прокси-сервера WinHTTP на каждом узле, чтобы указать локальный прокси-сервер и исключения локальных адресов \ (то есть список локальных addresses\). Чтобы сделать это, выполните следующую команду на каждом узле кластера из командной строки с повышенными привилегиями:  
  
```  
netsh winhttp set proxy <ProxyServerFQDN >:<port> "<local>"  
```  
  
где <*ProxyServerFQDN*> — это полное доменное имя для прокси-сервера и <*порт*> — это порт, через который для обмена данными (обычно это порт 443).  
  
Например, чтобы настроить параметры прокси-сервера WinHTTP для учетной записи Local System, указав прокси-сервер *MyProxy.CONTOSO.com*, с портом 443 и исключения локальных адресов, введите следующую команду:  
  
```  
netsh winhttp set proxy MyProxy.CONTOSO.com:443 "<local>"  
```  
  
### <a name="BKMK_BP_HF"></a>Рекомендации по использованию подключаемого модуля Microsoft.HotfixPlugin  
  
-   Мы рекомендуем настроить разрешения в корневой папке исправлений и файла конфигурации исправлений, чтобы ограничить доступ для записи только локальным администраторам компьютеров, которые используются для хранения этих файлов. Это поможет предотвратить несанкционированный доступ к этим файлам, который может нарушить функционирование отказоустойчивого кластера, при применении исправлений.  
  
-   Чтобы обеспечить целостность данных для сообщений блок \(SMB\) подключения, используемые для доступа к корневой папке исправлений, следует настроить шифрование SMB в общей папке SMB, если это возможно. **Microsoft.HotfixPlugin** требует настройки подписания SMB или шифрования SMB для обеспечения целостности данных для подключения SMB. 
  
    Дополнительные сведения см. в разделе [ограничить доступ к корневой папке исправлений и файлу конфигурации исправлений](cluster-aware-updating-plug-ins.md#BKMK_ACL).
  
### <a name="additional-recommendations"></a>Дополнительные рекомендации  
  
-   Чтобы не помешать выполнению пробега обновления CAU, может быть запланирован на то же время, не планируйте изменение паролей для объектов имен кластеров и виртуальных объектов-компьютеров периоды запланированного обслуживания.  
  
-   Следует задать соответствующие разрешения на предварительно обновления и обновления post\ сценариев, которые сохранены в сетевых общих папках, чтобы предотвратить возможный несанкционированный доступ к этим файлам неавторизованных пользователей.  
  
-   Чтобы настроить CAU в режиме обновления многоразовый, виртуальный объект-компьютер \(VCO\) для кластерной роли CAU необходимо создать в Active Directory. Кластерное обновление можно создать этот объект автоматически при добавлении кластерной роли CAU, если отказоустойчивого кластера достаточно разрешений. Однако из-за политик безопасности в некоторых организациях, он может быть необходимо предварительно подготовить объект в Active Directory. Процедуры для этого см. в разделе [действия по предварительной настройке учетной записи для кластерной роли](http://go.microsoft.com/fwlink/p/?LinkId=237624).  
  
-   Чтобы сохранять и повторно использовать параметры прогона обновления для отказоустойчивых кластеров с аналогичными обновление потребностей в ИТ-организации, можно создать профили прогона обновления. Кроме того в зависимости от режима обновления можно сохранить и управлять профили прогона обновления на файловом ресурсе, доступном всем удаленным компьютерам координатора обновлений или отказоустойчивым кластерам. Дополнительные сведения см. в разделе [Дополнительные параметры и обновление профилей выполнения кластерного обновления](cluster-aware-updating-options.md).  
  
## <a name="BKMK_BPA"></a>Тест готовности к обновлению кластера  
Можно запустить модель \(BPA\) CAU анализатор соответствия рекомендациям для проверки отказоустойчивого кластера и сетевая среда многим из требований для применения обновлений по CAU. Многие из тестов проверяют среду на готовность к применению обновлений Майкрософт с помощью по умолчанию модулей в **Microsoft.WindowsUpdatePlugin**.  
  
> [!NOTE]  
> Может потребоваться самостоятельно проверить готовность кластерной среды готовность к применению обновлений программного обеспечения с помощью модулей в, отличным от **Microsoft.WindowsUpdatePlugin**. Если вы используете Microsoft отличных модулей в, например, изготовителя оборудования, обратитесь к издателю Дополнительные сведения.  
  
Анализатор соответствия Рекомендациям можно запустить двумя способами:  
  
1.  Выберите **проанализировать готовность кластера к обновлению** в консоли CAU. После анализатора соответствия Рекомендациям выполнит тесты готовности, отображается отчет о тестировании. Если проблемы обнаружено на узлах кластера, выявленных неполадках и узлы, на которой отображаются проблемы так что можно предпримите следующие корректирующие действия. Выполнение тестов может занять несколько минут.  
  
2.  Запустите [Test-CauSetup](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/test-causetup) командлета. Его можно выполнить на локальном или удаленном компьютере, на котором установлен модуль для Windows PowerShell для отказоустойчивой кластеризации (часть средства отказоустойчивой кластеризации). Также можно запустить командлет на узле отказоустойчивого кластера.  
  
> [!NOTE]  
> -   Необходимо использовать учетную запись с правами администратора на узлах кластера и правами локального администратора на компьютере, который использовался для запуска **Test\ CauSetup** командлета или анализа с помощью окна кластерное обновление готовности к обновлению кластера. Для выполнения тестов с помощью окна кластерное обновление, необходимо войти в компьютер с необходимые учетные данные.  
> -   При проведении тестов предполагается, что средства CAU, используемые для просмотра и применения обновлений программного обеспечения, запускаются с того же компьютера и с теми же учетными, используются для проверки готовности к обновлению кластера.  
  
> [!IMPORTANT]  
> Мы настоятельно рекомендуем проверить кластер на готовность к обновлению в следующих ситуациях:  
>   
> -   Прежде чем использовать кластерное обновление в первый раз для обновления программного обеспечения.  
> -   После добавления узла в кластер или внесения других изменений в оборудование кластера, требующих запуска мастера кластера проверки.  
> -   После изменения источника обновлений, или изменения параметров или конфигураций обновления \(other than CAU\), может повлиять на применение обновлений к узлам.  
  
### <a name="tests-for-cluster-updating-readiness"></a>Тесты готовности к обновлению кластера  
В следующей таблице перечислены обновлению кластера тесты готовности, некоторые распространенные проблемы и действия по их устранению.  
  
|Тест|Возможные проблемы и их последствия|Действия по разрешению|  
|--------|-------------------------------|--------------------|  
|Должен быть доступен отказоустойчивый кластер|Не удается разрешить имя отказоустойчивого кластера или одного или нескольких узлах кластера невозможен. Анализатор соответствия Рекомендациям не может выполнить тесты готовности кластера.|— Проверьте написание имени кластера, указанное во время запуска анализатора соответствия Рекомендациям.<br />-Убедитесь, что все узлы кластера подключены к сети и выполнения.<br />— Проверьте, что проверки мастера настройки можно успешно запустить в отказоустойчивом кластере.|  
|Узлы отказоустойчивого кластера необходимо включить удаленное управление через WMI|Одного или нескольких узлах отказоустойчивого кластера не включено удаленное управление с помощью \(WMI\) инструментария управления Windows. Кластерное обновление не может обновить узлы кластера, если узлы не настроены для удаленного управления.|Убедитесь в том, что все узлы отказоустойчивого кластера включено удаленное управление через WMI. Дополнительные сведения см. в разделе [Настройка узлов для удаленного управления](#BKMK_NODE_CONFIG) в этом разделе.|  
|На каждом узле отказоустойчивого кластера следует включить удаленное взаимодействие PowerShell|PowerShell не установлена или не включена для удаленного взаимодействия на одном или нескольких узлах отказоустойчивого кластера. Кластерное обновление не может быть настроен для режим обновления многоразовый или использования некоторых функций в режим обновления remote\.|Убедитесь, что PowerShell установлены на всех узлах кластера и настроена для удаленного взаимодействия.<br /><br />Дополнительные сведения см. в разделе [Настройка узлов для удаленного управления](#BKMK_NODE_CONFIG) в этом разделе.|  
|Версия отказоустойчивого кластера|Один или несколько узлов в отказоустойчивом кластере не выполняются в Windows Server 2016, Windows Server 2012 R2 или Windows Server 2012. Кластерное обновление не может обновить отказоустойчивый кластер.|Убедитесь, что запущен отказоустойчивый кластер, указанные во время запуска анализатора соответствия Рекомендациям Windows Server 2016, Windows Server 2012 R2 или Windows Server 2012.<br /><br />Дополнительные сведения см. в разделе [Проверка конфигурации кластера](#BKMK_REQ_CLUS) в этом разделе.|  
|Требуемые версии .NET Framework и Windows PowerShell должен быть установлен на всех узлах отказоустойчивого кластера|.NET framework 4.6, 4.5 или Windows PowerShell не установлена на одном или нескольких узлах кластера. Некоторые функции CAU могут не работать.|Убедитесь, что .NET Framework 4.6 или 4.5 и Windows PowerShell установлены на всех узлах кластера, если они необходимы.<br /><br />Дополнительные сведения см. в разделе [Настройка узлов для удаленного управления](#BKMK_NODE_CONFIG) в этом разделе.|  
|Служба кластеров должна работать на всех узлах кластера|Служба кластеров не запущена на одном или нескольких узлах. Кластерное обновление не может обновить отказоустойчивый кластер.|-Убедитесь, что \(clussvc\) служба кластеров запущена на всех узлах в кластере, и она настроена на автоматический запуск.<br />— Проверьте, что проверки мастера настройки можно успешно запустить в отказоустойчивом кластере.<br /><br />Дополнительные сведения см. в разделе [Проверка конфигурации кластера](#BKMK_REQ_CLUS) в этом разделе.|  
|Автоматическое обновление не должен быть настроен на автоматическую установку обновлений на узлы отказоустойчивого кластера|В по крайней мере одного узла отказоустойчивого кластера автоматического обновления настроена на автоматическую установку обновлений корпорации Майкрософт на этом узле. Использование CAU в сочетании с другими способами обновления может привести к незапланированным простоям или непредвиденным результатам.|Если функции обновления Windows настроен для автоматического обновления на одном или нескольких узлах кластера, убедитесь, что автоматическое обновление не настроен на автоматическую установку обновлений.<br /><br />Дополнительные сведения см. в разделе [рекомендации по применению обновлений Майкрософт](#BKMK_BP_WUA).|  
|Узлы отказоустойчивого кластера должны использовать тот же источник обновления|Одного или нескольких узлах отказоустойчивого кластера, настроены на использование источника обновлений Майкрософт, отличается от остальных узлов. Обновления могут не применяться единообразно на узлах кластера с помощью CAU.|Убедитесь, что каждый узел кластера, настроен для использования того же источника обновлений, например, сервер WSUS, центра обновления Windows или Центра обновления Майкрософт.<br /><br />Дополнительные сведения см. в разделе [рекомендации по применению обновлений Майкрософт](#BKMK_BP_WUA).|  
|Правило брандмауэра, разрешающее удаленное завершение работы должен быть включен на каждом узле отказоустойчивого кластера|Одного или нескольких узлах отказоустойчивого кластера не включено правило брандмауэра, разрешающее удаленное завершение работы или параметр групповой политики этого правила запрещено его включение. Прогон обновления, который применяет обновления, требующие автоматической перезагрузки узлов могут быть применены неверно.|Если в узлах кластера используется брандмауэр Windows или брандмауэр отличных Майкрософт, настройте правило брандмауэра, разрешающее удаленное завершение работы.<br /><br />Дополнительные сведения см. в разделе [Включение правила брандмауэра для обеспечения автоматического перезапуска](#BKMK_FW) в этом разделе.|  
|Прокси-сервера сервера на каждом узле отказоустойчивого кластера должен быть задан локальный прокси-сервер|Одного или нескольких узлах отказоустойчивого кластера имеют конфигурацию неверный прокси-сервера.<br /><br />Если используется локальный прокси-сервер, параметр прокси-сервера на каждом узле должен быть настроен правильно для кластера, для доступа к центра обновления Майкрософт или Центра обновления Windows.|Убедитесь, что параметры прокси-сервера WinHTTP на каждом узле кластера заданы локальный прокси-сервер при необходимости. Если прокси-сервер не используется в вашей среде, это предупреждение можно игнорировать.<br /><br />Дополнительные сведения см. в разделе [применение обновлений в филиалах](#BKMK_PROXY) в этом разделе.|  
|Кластерная роль CAU должен устанавливаться на отказоустойчивом кластере, чтобы включить режим многоразовый обновления|Кластерная роль CAU не установлена на этом отказоустойчивом кластере. Эта роль необходима для многоразовый обновлению кластера.|Чтобы использовать CAU в режим обновления многоразовый, добавьте кластерную роль CAU на отказоустойчивом кластере одним из следующих способов:<br /><br />-Запустите [Add-CauClusterRole](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/add-cauclusterrole) командлета PowerShell.<br />— Выберите **настроить параметры обновления многоразовый кластера** действие в окне кластерного обновления.|  
|В отказоустойчивом кластере для включения режим обновления многоразовый должна включена кластерная роль CAU|Кластерная роль CAU отключена. Например, кластерная роль CAU не установлена или отключена с помощью [Disable\-CauClusterRole](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/disable-cauclusterrole) командлета PowerShell. Эта роль необходима для многоразовый обновлению кластера.|Чтобы использовать CAU в режим обновления многоразовый, включите кластерную роль CAU в отказоустойчивом кластере одним из следующих способов:<br /><br />-Запустите [Enable-CauClusterRole](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/enable-cauclusterrole) командлета PowerShell.<br />— Выберите **настроить параметры обновления многоразовый кластера** действие в окне кластерного обновления.|  
|Настроенный CAU модулей в для режим обновления многоразовый должен быть зарегистрирован на всех узлах отказоустойчивого кластера|Кластерная роль CAU на одном или нескольких узлах этого отказоустойчивого кластера не может получить доступ к модулю модулей в CAU, настроенном в параметрах многоразовый обновления. Многоразовый обновление запуска может завершиться ошибкой.|-Убедитесь, что настроенный CAU модулей в устанавливается на всех узлах кластера, выполнив процедуру установки для продукта, который содержит CAU модулей в.<br />-Запустите [Register\ CauPlugin](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/register-cauplugin) командлет PowerShell для регистрации модулей в на требуемых узлах кластера.|  
|Все узлы отказоустойчивого кластера должны иметь один и тот же набор зарегистрированных модулей модулей CAU|Многоразовый обновление запуска может завершиться сбоем модулей в, настроенный для использования в прогона обновления изменяется на тот, который доступен не на всех узлах кластера.|-Убедитесь, что настроенный CAU модулей в устанавливается на всех узлах кластера, выполнив процедуру установки для продукта, который содержит CAU модулей в.<br />-Запустите [Register\ CauPlugin](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/register-cauplugin) командлет PowerShell для регистрации модулей в на требуемых узлах кластера.|  
|Обновления должны быть настроены допустимые параметры|Обновление многоразовый расписания и параметров прогона обновления, настроенные для этого отказоустойчивого кластера являются неполными или недопустимыми. Многоразовый обновление запуска может завершиться ошибкой.|Настройте допустимое расписание обновления многоразовый и набор параметров прогона обновления. Например, можно использовать [Set\-CauClusterRole](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/set-cauclusterrole) командлет PowerShell для настройки CAU кластерной роли.|  
|По крайней мере два узла отказоустойчивого кластера должны быть владельцами кластерной роли CAU|Прогон обновления, запущенный в режиме обновления многоразовый произойдет сбой, так как нет узла-владельца, чтобы переместить кластерную роль CAU.|Чтобы убедиться, что все узлы кластера настраиваются как CAU возможные владельцы кластерной роли, используйте средства отказоустойчивой кластеризации. Это конфигурация по умолчанию.||  
|Все узлы отказоустойчивого кластера должны иметь доступ к сценариям Windows PowerShell|Не все возможные узлы-владельцы кластерной роли CAU можно получить доступ к настроенным сценариям Windows PowerShell предварительно обновления и обновления post\. Многоразовый обновление выполнить не удастся.|Убедитесь, что все возможные узлы-владельцы кластерной роли CAU есть разрешения на доступ к настроенным сценариям предварительно обновления и обновления post\ PowerShell.|  
|Все узлы отказоустойчивого кластера должны использоваться идентичные сценарии Windows PowerShell|Не все возможные узлы-владельцы кластерной роли CAU используется та же копия указанных сценариев Windows PowerShell предварительно обновления и обновления post\. Прогон обновления многоразовый может сбоем или выполняться непредвиденным образом.|Убедитесь, что все возможные узлы-владельцы кластерной роли CAU используют же предварительно обновления и обновления post\ сценариев PowerShell.|  
|Параметра WarnAfter, заданное для прогона обновления должно быть меньше значения параметра StopAfter|Указанные значения времени ожидания прогона обновления CAU делают время ожидания предупреждения недействительным. Выполнение обновления может быть отменен до регистрации предупреждения в журнале событий могут быть созданы.|В параметрах прогона обновления можно настроить **WarnAfter** параметра значение меньше, чем **StopAfter** значение параметра.|  
  
## <a name="see-also"></a>См. также:  
  
-   [Обзор кластерного обновления](cluster-aware-updating.md)
  