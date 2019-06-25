---
ms.assetid: 16a344a9-f9a6-4ae2-9bea-c79a0075fd04
title: Аттестация ключей доверенного платформенного модуля (TPM Key) Attestation
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 3cfc047fe1a66617abbda1de5f2c5842dcbdeb12
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2019
ms.locfileid: "59862885"
---
# <a name="tpm-key-attestation"></a>Аттестация ключей доверенного платформенного модуля (TPM Key) Attestation

>Область применения. Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

**Автор**: Джастин Тернер, старший инженер по улучшению поддержки с группой Windows  
  
> [!NOTE]  
> Этот материал создан инженером службы поддержки клиентов Майкрософт и предназначен для опытных администраторов и архитекторов систем, которым нужны более глубокие технические сведения о функциях и решениях в Windows Server 2012 R2, а не обычная информация, доступная в статьях на сайте TechNet. Однако он не был отредактирован согласно требованиям сайта, поэтому некоторые формулировки могут быть не такими выверенными, как на станицах TechNet.  
  
## <a name="overview"></a>Обзор  
При поддержке для ключей, защищенных доверенным платформенным Модулем, существовавший начиная с Windows 8, было не механизмы для ЦС криптографическое, что закрытый ключ защищен с доверенного платформенного модуля (TPM). Это обновление позволяет ЦС для выполнения этого аттестации и с учетом этого аттестации в выданный сертификат.  
  
> [!NOTE]  
> В этой статье предполагается, что читатель обладает знакомы с концепцией шаблона сертификата (справочные материалы по [шаблонов сертификатов](https://technet.microsoft.com/library/cc730705.aspx)). Также предполагается, что читатель хорошо знаком с тем, как настроить ЦС предприятия для выдачи сертификатов, основанных на шаблонах сертификатов (справочные материалы по [контрольный список: Настройка центров сертификации для выпуска сертификатов и управление ими](https://technet.microsoft.com/library/cc771533.aspx)).  
  
### <a name="terminology"></a>Терминология  
  
|Термин|Определение|  
|--------|--------------|  
|EK|Ключ подтверждения. Это представляет собой асимметричный ключ, содержащийся внутри TPM (внедрен во время производства). EK уникален для каждого TPM и можно идентифицировать его. EK нельзя изменить или удалить.|  
|EKpub|Ссылается на открытый ключ EK.|  
|EKPriv|Относится к закрытому ключу EK.|  
|EKCert|Сертификат EK. Доверенный платформенный модуль производителя выданный сертификат для EKPub. Не все доверенные платформенные модули располагают EKCert.|  
|Доверенный платформенный модуль|Доверенный платформенный модуль. Доверенный платформенный модуль предназначен для предоставления аппаратных функций безопасности. Микросхема TPM — это надежный криптографический процессор, спроектированный для выполнения операций шифрования. Эта микросхема содержит несколько механизмов физической защиты для предотвращения взлома, и вредоносные программы не могут обойти функции безопасности TPM.|  
  
### <a name="background"></a>Фон  
Начиная с Windows 8, доверенного платформенного модуля (TPM) можно использовать для защиты закрытого ключа сертификата. Microsoft платформы Crypto Provider поставщик хранилища ключей (KSP) включает эту функцию. Обнаружены две проблемы с реализацией:  

-   Не было никакой гарантии, что ключ является фактически защиты доверенного платформенного МОДУЛЯ (кто-то может легко подделать KSP программного обеспечения как в KSP доверенного платформенного МОДУЛЯ с учетными данными локального администратора).

-   Не удалось ограничить список доверенных платформенных модулей, которые позволяют защитить корпоративные сертификаты, выданные (в случае, если администратору PKI для управления типами устройств, которые могут использоваться для получения сертификатов в среде).  

### <a name="tpm-key-attestation"></a>Аттестация ключей доверенного платформенного модуля (TPM)  
Аттестация ключей доверенного платформенного МОДУЛЯ является возможность сущности, запрашивающей сертификат доказать с помощью шифрования в ЦС, ключ RSA в запросе на сертификат защищен либо «» или «» доверенным платформенным Модулем, доверенным модулем ЦС. Доверительная модель доверенного платформенного МОДУЛЯ более рассматривается в [Общие сведения о развертывании](../../../ad-ds/manage/component-updates/TPM-Key-Attestation.md#BKMK_DeploymentOverview) подразделе данного раздела.  
  
### <a name="why-is-tpm-key-attestation-important"></a>Почему важна аттестации ключей доверенного платформенного МОДУЛЯ?  
Сертификат пользователя с ключом аттестовать TPM предоставляет выше гарантии безопасности, резервное копирование, не возможность экспорта, противодействия подбору и изоляцию ключи, предоставляемые доверенного платформенного МОДУЛЯ.  
  
В аттестации ключей доверенного платформенного МОДУЛЯ новая парадигма управления реализована возможность: Администратор может определить набор устройств, которые пользователи могут использовать для доступа к корпоративным ресурсам (для, например VPN или беспроводной точке доступа) и иметь **строгого** гарантирует, что другие устройства не может использоваться для доступа к ним. — Это новая парадигма элемента управления доступ **строгого** , так как он привязан к *привязкой к оборудованию* удостоверение пользователя, которое строже, чем учетных данных на основе программного обеспечения.
  
### <a name="how-does-tpm-key-attestation-work"></a>Как работает аттестации ключей доверенного платформенного МОДУЛЯ?  
Как правило Аттестация ключей TPM основана на следующие основные принципы:  
  
1.  Каждого TPM поставляется с уникальным асимметричный ключ, вызывается *ключ подтверждения* (EK), записать производителем. Мы называем этот ключ как открытую часть *EKPub* и связанный закрытый ключ как *EKPriv*. Некоторые микросхемы доверенного платформенного МОДУЛЯ также иметь сертификат EK, выпускается производителем EKPub. Мы называем этот сертификат как *EKCert*.  
  
2.  ЦС устанавливает доверительные отношения с помощью EKPub или EKCert доверенного платформенного МОДУЛЯ.  
  
3.  Пользователь подтверждает для ЦС, что ключ RSA, для которого запрашивается сертификат криптографически связана с EKPub и что пользователь является владельцем EKpriv.  
  
4.  ЦС выдает сертификат с политикой специальные выдачи OID для обозначения того, что ключ теперь аттестовать Защищаемая доверенного платформенного МОДУЛЯ.  
  
## <a name="BKMK_DeploymentOverview"></a>Общие сведения о развертывании  
В этом развертывании предполагается настроить ЦС предприятия Windows Server 2012 R2. Кроме того шаблоны сертификатов клиентов, чтобы установить сертификат для этого ЦС предприятия с помощью настраиваются (Windows 8.1). 

Существует три шага для развертывания аттестации ключей доверенного платформенного МОДУЛЯ.  
  
1.  **Планирование доверительная модель доверенного платформенного МОДУЛЯ:** Первым шагом является решить, какую модель доверия доверенный платформенный модуль для использования. Существует 3 способа, поддерживаемых для этого:  
  
    -   **Доверие, основанное на учетные данные пользователя:** ЦС предприятия доверяет EKPub предоставляемый пользователем как часть запроса сертификата и проверка не выполняется отличные от учетных данных пользователя домена.  
  
    -   **Доверие, основанное на EKCert:** ЦС предприятия использует для проверки цепочки сертификатов, который предоставляется как часть запроса на сертификат по списку управляемые администратором *допустимые цепочки сертификат EK*. Допустимые цепочек, определенного производителя и выражаются через два хранилища пользовательского сертификата в ЦС (один магазин промежуточных) и один для корневых сертификатов. Этот режим доверия означает, что **все** доверенный платформенный модуль производителем данного являются доверенными. Обратите внимание, что в этом режиме доверенных платформенных модулей, используемых в среде должен содержать EKCerts.
  
    -   **Доверие, основанное на EKPub:** ЦС предприятия выполняет проверку допустимости EKPubs EKPub, предоставляемые как часть запроса на сертификат отображается в списке управляемые администратором. Этот список выражается в виде каталога с файлами, где имя каждого файла в этот каталог является хэш SHA-2 разрешенных EKPub. Этот параметр обеспечивает самый высокий уровень надежности, но требуются дополнительные усилия по администрированию, так как каждое устройство отдельно идентифицировать. В этой модели доверия только те устройства, которые имели EKPub доверенный платформенный модуль, добавляемый в список разрешенных EKPubs разрешены для подачи заявки на сертификат аттестовать доверенного платформенного МОДУЛЯ.  
  
    В зависимости от того, какой метод используется ЦС применит политику выдачи различных OID для выдаваемый сертификат. Дополнительные сведения о политике выдачи идентификаторов объектов см. в таблице OID политик выдачи в [Настройка шаблона сертификата](../../../ad-ds/manage/component-updates/TPM-Key-Attestation.md#BKMK_ConfigCertTemplate) этой статьи.  
  
    Обратите внимание, что можно выбрать сочетание моделей доверия доверенного платформенного МОДУЛЯ. В этом случае ЦС будет принимать любые методы аттестации и политика выдачи OID будут отражать все методы аттестации, которые завершились успешно.  
  
2.  **Настройка шаблона сертификата:** Настройка шаблона сертификата описана в [сведения о развертывании](../../../ad-ds/manage/component-updates/TPM-Key-Attestation.md#BKMK_DeploymentDetails) этой статьи. В этой статье не рассматриваются способ назначения этого шаблона сертификата в ЦС предприятия или регистрация доступ предоставляется группе пользователей. Дополнительные сведения см. в разделе [контрольный список: Настройка центров сертификации для выпуска сертификатов и управление ими](https://technet.microsoft.com/library/cc771533.aspx).  
  
3.  **Настройка центра сертификации для доверительная модель доверенного платформенного МОДУЛЯ**  
  
    1.  **Доверие, основанное на учетные данные пользователя:** Никаких особых настроек является обязательным.  
  
    2.  **Доверие, основанное на EKCert:** Администратору необходимо получить цепочки сертификатов EKCert производителей доверенный платформенный модуль и импортировать их в двух новых хранилищ сертификатов, созданные администратором, в центре сертификации, которые выполняют аттестации ключей доверенного платформенного МОДУЛЯ. Дополнительные сведения см. в разделе [конфигурации ЦС](../../../ad-ds/manage/component-updates/TPM-Key-Attestation.md#BKMK_CAConfig) этой статьи.  
  
    3.  **Доверие, основанное на EKPub:** Администратор должен получить EKPub для каждого устройства, которое будет сертификаты аттестовать доверенного платформенного МОДУЛЯ и добавьте их в список разрешенных EKPubs. Дополнительные сведения см. в разделе [конфигурации ЦС](../../../ad-ds/manage/component-updates/TPM-Key-Attestation.md#BKMK_CAConfig) этой статьи.  
  
    > [!NOTE]  
    > -   Этой функции требуется Windows 8.1 и Windows Server 2012 R2.  
    > -   Аттестация ключей TPM для смарт-карты сторонние поставщики KSP с помощью не поддерживается. Необходимо использовать KSP поставщика шифрования платформы Майкрософт.  
    > -   Аттестация ключей TPM работает только для ключей RSA.  
    > -   Аттестация ключей доверенного платформенного МОДУЛЯ не поддерживается для автономного ЦС.  
    > -   Аттестация ключей доверенного платформенного МОДУЛЯ не поддерживает [обработки временных сертификатов](https://technet.microsoft.com/library/ff934598).  
  
## <a name="BKMK_DeploymentDetails"></a>Сведения о развертывании  
  
### <a name="BKMK_ConfigCertTemplate"></a>Настройка шаблона сертификата  
Чтобы настроить шаблон сертификата для аттестации ключей доверенного платформенного МОДУЛЯ, выполните следующие действия по настройке:  
  
1.  **Совместимость** вкладку  
  
    В **параметры совместимости** раздел:  
  
    -   Убедитесь, **Windows Server 2012 R2** выбран для **сертификации**.  
  
    -   Убедитесь, **Windows 8.1 или Windows Server 2012 R2** выбран для **получатель сертификата**.  
  
    ![Аттестация ключей доверенного платформенного модуля (TPM)](media/TPM-Key-Attestation/GTR_ADDS_CompatibilityTab.gif)  
  
2.  **Криптография** вкладку  
  
    Убедитесь, **поставщик хранилища ключей** выбран для **категория поставщика** и **RSA** выбран для **имя алгоритма**. Убедитесь, **запросы должны использовать один из следующих поставщиков** выбран и **поставщик службы шифрования платформы Майкрософт** выбран пункт **поставщики**.  
  
    ![Аттестация ключей доверенного платформенного модуля (TPM)](media/TPM-Key-Attestation/GTR_ADDS_CryptoTab.gif)  
  
3.  **Аттестация ключей** вкладку  
  
    Это новую вкладку для Windows Server 2012 R2:  
  
    ![Аттестация ключей доверенного платформенного модуля (TPM)](media/TPM-Key-Attestation/GTR_ADDS_ConfigCertTemplate.gif)  
  
    Выбор режима аттестации из трех возможных вариантов.  
  
    ![Аттестация ключей доверенного платформенного модуля (TPM)](media/TPM-Key-Attestation/GTR_ADDS_KeyModes.gif)  
  
    -   **NONE:** Означает, что нельзя использовать аттестацию ключей  
  
    -   **Требуется, если клиент может:** Позволяет пользователям на устройстве, которое не поддерживает аттестацию ключей доверенного платформенного МОДУЛЯ, чтобы продолжить регистрацию для этого сертификата. Пользователи, которые можно выполнять аттестацию будет отличить с политикой специальные выдачи OID. Некоторые устройства не может иметь возможность выполнить аттестацию из-за старый доверенного платформенного МОДУЛЯ, который не поддерживает аттестацию ключей или устройстве вообще не с доверенным платформенным Модулем.
  
    -   **Обязательно:** Клиент *необходимо* выполнять аттестацию ключей доверенного платформенного МОДУЛЯ, иначе произойдет сбой запроса на сертификат.  
  
    Затем выберите доверительная модель доверенного платформенного МОДУЛЯ. Снова можно тремя способами:  
  
    ![Аттестация ключей доверенного платформенного модуля (TPM)](media/TPM-Key-Attestation/GTR_ADDS_KeyTypeToEnforce.gif)  
  
    -   **Учетные данные пользователя:** Разрешить проверку подлинности пользователя, подтверждающий для допустимых доверенного платформенного МОДУЛЯ, указав свои учетные данные домена.  
  
    -   **Сертификат подтверждения:** EKCert устройства необходимо проверить через управляемые администратором доверенного платформенного МОДУЛЯ промежуточных сертификатов ЦС управляемые администратором корневого ЦС сертификата. Если выбран этот параметр, необходимо настроить EKCA и EKRoot хранилища в выдающем ЦС сертификатов, как описано в разделе [конфигурации ЦС](../../../ad-ds/manage/component-updates/TPM-Key-Attestation.md#BKMK_CAConfig) этой статьи.  
  
    -   **Ключ подтверждения:** EKPub устройства должно отображаться в списке управляемые администратором PKI. Этот параметр обеспечивает самый высокий уровень надежности, но требуются дополнительные усилия по администрированию. Если выбран этот параметр, необходимо настроить список EKPub в выдающем ЦС как описано в разделе [конфигурации ЦС](../../../ad-ds/manage/component-updates/TPM-Key-Attestation.md#BKMK_CAConfig) этой статьи.  
  
    Наконец решите, какая политика выдачи для отображения в выданный сертификат. По умолчанию каждый тип применения имеет идентификатор связанного объекта (OID), который будет вставлен в сертификат, если он проходит проверку типа принудительного применения, как описано в следующей таблице. Обратите внимание, что можно выбрать сочетание методов принудительного применения. В этом случае ЦС будет принимать любой из методов аттестации, и политика выдачи OID будут отражены все методы аттестации, успешно установленных.  
  
    **OID политики выдачи**  
  
    |OID|Аттестация ключей типа|Описание|Уровень надежности|  
    |-------|------------------------|---------------|-------------------|  
    |1.3.6.1.4.1.311.21.30|EK|«EK проверен»:   Управляемые администратором список EK|Высокий|  
    |1.3.6.1.4.1.311.21.31|Сертификат подтверждения|«EK сертификат проверен:» При проверке цепочки сертификатов EK|Средний|  
    |1.3.6.1.4.1.311.21.32|Учетные данные пользователя|«При использовании доверенных EK:» Для пользователя аттестовать EK|Низкий|  
  
    Идентификаторы объектов будет вставлен в выданный сертификат, если **включают политики выдачи** — выбрано (конфигурация по умолчанию).  
  
    ![Аттестация ключей доверенного платформенного модуля (TPM)](media/TPM-Key-Attestation/GTR_ADDS_IssuancePolicies.gif)  
  
    > [!TIP]  
    > Потенциальные необходимости OID, имеющимися в сертификате применяется для ограничения доступа к VPN или беспроводной сети на определенных устройствах. Например то политика доступа может позволить подключение (или доступ к разные виртуальные локальные сети), если OID 1.3.6.1.4.1.311.21.30 присутствует в сертификате. Это позволяет ограничить доступ к устройствам, которого EK доверенного платформенного МОДУЛЯ присутствует в списке EKPUB.  
  
### <a name="BKMK_CAConfig"></a>Настройки ЦС  
  
1.  **Настройка EKCA и EKROOT хранилищ сертификатов в выдающий ЦС**  
  
    Если вы выбрали **сертификат подтверждения** для параметров шаблона, выполните следующие действия по настройке:  
  
    1.  Создайте два новых хранилищ сертификатов на сервер центра сертификации (ЦС), будет выполнять аттестацию ключей доверенного платформенного МОДУЛЯ с помощью Windows PowerShell.  
  
    2.  Получить промежуточные и корневые сертификаты ЦС из производитель, который вы хотите разрешить в корпоративной среде. Эти сертификаты должны импортироваться в хранилище сертификатов, созданных ранее (EKCA и EKROOT) соответствующим образом.  
  
    Следующий сценарий Windows PowerShell выполняет оба этих действия. В следующем примере производителя доверенного платформенного МОДУЛЯ Fabrikam предоставил сертификат корневого *FabrikamRoot.cer* и сертификат ЦС *Fabrikamca.cer*.  
  
    ```powershell  
    PS C:>\cd cert:  
    PS Cert:\>cd .\\LocalMachine  
    PS Cert:\LocalMachine> new-item EKROOT  
    PS Cert:\ LocalMachine> new-item EKCA  
    PS Cert:\EKCA\copy FabrikamCa.cer .\EKCA  
    PS Cert:\EKROOT\copy FabrikamRoot.cer .\EKROOT  
    ```  
  
2.  **EKPUB список настроек, если с помощью типа аттестации EK**  
  
    Если вы выбрали **ключ подтверждения** в параметрах шаблона конфигурации вам для создания и настройки папки в выдающем ЦС, содержащего файлы размером 0 байт, каждая с именем для разрешенных EK хэш SHA-2. Эта папка служит в качестве «список разрешений» устройств, которые могут получить сертификаты аттестовать ключ доверенного платформенного МОДУЛЯ. Так как необходимо вручную добавить EKPUB для каждого устройства, которое требуется сертификат attested, он предоставляет предприятия, гарантирующего устройства, которые авторизованы для получения ключа аттестовать сертификаты доверенного платформенного МОДУЛЯ. Настройка ЦС для этого режима в два этапа:  
  
    1.  **Создайте запись реестра EndorsementKeyListDirectories:** Используйте средство командной строки Certutil для настройки расположения папок, где определены доверенных EKpubs, как описано в следующей таблице.  
  
        |Операция|Синтаксис команды|  
        |-------------|------------------|  
        |Добавить расположения папок|certutil.exe -setreg CA\EndorsementKeyListDirectories +"<folder>"|  
        |Удаление папки|certutil.exe -setreg CA\EndorsementKeyListDirectories -"<folder>"|  
  
        EndorsementKeyListDirectories в команды certutil – это параметр реестра, как описано в следующей таблице.  
  
        |Значение|Тип|Данные|  
        |--------------|--------|--------|  
        |EndorsementKeyListDirectories|REG_MULTI_SZ|< ЛОКАЛЬНЫЙ или UNC-путь к EKPUB разрешить списки ><br /><br />Пример.<br /><br />*\\\blueCA.contoso.com\ekpub*<br /><br />*\\\bluecluster1.contoso.com\ekpub*<br /><br />D:\ekpub|  
  
        HKLM\SYSTEM\CurrentControlSet\Services\CertSvc\Configuration\\<CA Sanitized Name>  
  
        *EndorsementKeyListDirectories* будет содержать список UNC-путь или пути локальной файловой системы, каждая из которых указывает папки, доступ на чтение к ЦС. Каждая папка может содержать ноль или больше разрешить записи списка, где каждая запись — это файл с именем, которое является SHA-2 хэш доверенных EKpub, без расширения файла. 
        Создание или изменение этой конфигурации ключа реестра требуется перезагрузка центра сертификации, так же, как существующие параметры конфигурации реестра ЦС. Однако изменения параметра конфигурации вступят в силу немедленно и не потребует ЦС должен быть перезапущен.  
  
        > [!IMPORTANT]  
        > Обеспечение защиты папок в списке от несанкционированного доступа и несанкционированного доступа путем настройки разрешений, чтобы только авторизованные администраторы доступ чтения и записи. Учетная запись компьютера ЦС требуется доступ только для чтения.  
  
    2.  **Заполните список EKPUB:** Используйте следующий командлет Windows PowerShell для получения хэш открытого ключа EK доверенного платформенного МОДУЛЯ с помощью Windows PowerShell на каждом устройстве, а затем отправить этот хэш открытого ключа ЦС и сохранить его в папке EKPubList.  
  
        ```powershell  
        PS C:>\$a=Get-TpmEndorsementKeyInfo -hashalgorithm sha256  
        PS C:>$b=new-item $a.PublicKeyHash -ItemType file  
        ```  
  
## <a name="troubleshooting"></a>Устранение неполадок  
  
### <a name="key-attestation-fields-are-unavailable-on-a-certificate-template"></a>Аттестация ключей будут недоступны для шаблона сертификата  
Аттестация ключей поля доступны не в том случае, если параметр шаблона не соответствует требованиям для аттестации. Ниже приведены распространенные причины.  
  
1.  Параметры совместимости не настроены правильно. Убедитесь, что они настроены следующим образом:  
  
    1.  **Центр сертификации**: **Windows Server 2012 R2**  
  
    2.  **Сертификат получателя**: **Windows 8.1 и Windows Server 2012 R2**  
  
2.  Параметры шифрования не настроены правильно. Убедитесь, что они настроены следующим образом:  
  
    1.  **Категория поставщика**: **Поставщик хранилища ключей**  
  
    2.  **Имя алгоритма**: **RSA**  
  
    3.  **Поставщики**: **Поставщик криптографии для платформы Microsoft**  
  
3.  Параметры обработки запроса не настроены правильно. Убедитесь, что они настроены следующим образом:  
  
    1.  **Разрешить экспортировать закрытый ключ** не должен быть выбран вариант.  
  
    2.  **Архивировать закрытый ключ субъекта** не должен быть выбран вариант.  
  
### <a name="verification-of-tpm-device-for-attestation"></a>Проверка устройства TPM для аттестации  
Используйте командлет Windows PowerShell, **CAEndorsementKeyInfo Подтверждение**, чтобы убедиться, что конкретного устройства доверенного платформенного МОДУЛЯ является доверенным для аттестации, центрами сертификации. Существует два варианта: один для проверки EKCert, а другой — для проверки EKPub. Командлет является выполнять локально в ЦС, или на удаленном сайте центра администрирования с помощью удаленного взаимодействия Windows PowerShell.  
  
1.  Для проверки доверия на EKPub, выполните следующие действия:  
  
    1.  **Извлеките EKPub с клиентского компьютера:** EKPub можно извлечь из клиентского компьютера через **Get-TpmEndorsementKeyInfo**. Из командной строки с повышенными правами используйте следующую команду:  
  
        ```  
        PS C:>\$a=Get-TpmEndorsementKeyInfo -hashalgorithm sha256  
        ```  
  
    2.  **Проверка доверия на EKCert на компьютере ЦС:** Скопируйте извлеченную строку (хэш SHA-2 EKPub) на сервер (например, по электронной почте) и передайте его в командлет Confirm-CAEndorsementKeyInfo. Обратите внимание на то, что этот параметр должен иметь 64 символов.  
  
        ```  
        Confirm-CAEndorsementKeyInfo [-PublicKeyHash] <string>  
        ```  
  
2.  Для проверки доверия на EKCert, выполните следующие действия:  
  
    1.  **Извлеките EKCert с клиентского компьютера:** EKCert можно извлечь из клиентского компьютера через **Get-TpmEndorsementKeyInfo**. Из командной строки с повышенными правами используйте следующую команду:  
  
        ```  
        PS C:>\$a=Get-TpmEndorsementKeyInfo
        PS C:>\$a.manufacturerCertificates|Export-Certificate -filepath c:\myEkcert.cer
        ```  
  
    2.  **Проверка доверия на EKCert на компьютере ЦС:** Скопируйте извлеченные EKCert (EkCert.cer) в центр сертификации (например, по электронной почте или xcopy). Например если вы копируете файл сертификата в папку «c:\diagnose» на сервере ЦС, выполните следующую команду, чтобы завершить проверку подлинности:  
  
        ```  
        PS C:>new-object System.Security.Cryptography.X509Certificates.X509Certificate2 "c:\diagnose\myEKcert.cer" | Confirm-CAEndorsementKeyInfo  
        ```  
  
## <a name="see-also"></a>См. также  
[Обзор технологии доверенного платформенного модуля](https://technet.microsoft.com/library/jj131725.aspx)  
[Внешний ресурс: Доверенный платформенный модуль](http://www.cs.unh.edu/~it666/reading_list/Hardware/tpm_fundamentals.pdf)  