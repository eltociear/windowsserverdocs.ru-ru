---
title: Краткое руководство по развертыванию защищенной структуры
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: e060e052-39a0-4154-90bb-b97cc6dde68e
manager: dongill
author: justinha
ms.author: justinha
ms.technology: security-guarded-fabric
ms.date: 01/30/2019
ms.openlocfilehash: d63726e7046896c9ef7aa0c3b3d85237bc3f788d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2019
ms.locfileid: "59879065"
---
# <a name="quick-start-for-guarded-fabric-deployment"></a>Краткое руководство по развертыванию защищенной структуры

>Относится к: Windows Server (полугодовой канал), Windows Server 2016

В этом разделе объясняется, что является защищенной структуре, его требованиях и Сводка процесса развертывания. Подробное описание этапов развертывания, см. в разделе [развертывания службы защиты узла для защищенных узлов и экранированных виртуальных машин](https://technet.microsoft.com/windows-server-docs/security/guarded-fabric-shielded-vm/guarded-fabric-deploying-hgs-overview).

Предпочитаете видео? См. в разделе курса Microsoft Virtual Academy [развертывание экранированных виртуальных машин и Защищенная структура в Windows Server 2016](https://mva.microsoft.com/en-US/training-courses/deploying-shielded-vms-and-a-guarded-fabric-with-windows-server-2016-17131?l=WFLef7vUD_4604300474).

## <a name="what-is-a-guarded-fabric"></a>Что такое защищенной структуры

Объект _защищенных fabric_ способен обеспечить защиту рабочих нагрузок клиента от проверки, кражи и подмены от вредоносных программ, работающих на узле, а также от системных администраторов структуры Windows Server 2016 Hyper-V. Эти виртуализированные рабочие нагрузки клиентов — защищены на уровне rest и в рейсов — называются _экранированных виртуальных машин_. 

## <a name="what-are-the-requirements-for-a-guarded-fabric"></a>Каковы требования к защищенной структуры

Требования для защищенной структуры:

- **Место для запуска экранированных виртуальных машин, которые будут свободны от вредоносных программ.**

    Они называются _защищенных узлов_. 
    Защищенные узлы, узлы Hyper-V Windows Server 2016 Datacenter edition, которые могут запускаться экранированные виртуальные машины только в том случае, если они могут доказать, что они выполняются в известное состояние доверенного центра вызывается службы Защитника узлов (HGS). 
    HGS — новая роль сервера в Windows Server 2016 и обычно развертывается как кластер с тремя узлами. 

- **Способ проверки узел находится в работоспособном состоянии.**

    Выполняет HGS _аттестации_, где он измеряет работоспособность защищенных узлов.

- **Процесс, чтобы безопасно освободить ключи для работоспособных узлов.**

    Выполняет HGS _ключа защиты и выходом ключевых версий_, где он освобождает ключи работоспособные узлы.

- **Средства управления, позволяющие автоматизировать безопасные подготавливать и размещать экранированные виртуальные машины.**

    При необходимости можно добавить эти средства управления для защищенной структуры:

    - Virtual Machine Manager 2016 Center System (VMM). VMM является рекомендуемым, поскольку предоставляет дополнительное управление средства шире, чем у использовать только командлеты PowerShell, входящие в состав Hyper-V и рабочие нагрузки защищенной структуры).
    - System Center 2016 Service Provider Foundation (SPF). Это уровень интерфейса API между Windows Azure Pack, VMM и необходимым условием для использования Windows Azure Pack.
    - Windows Azure Pack предоставляет хороший графический веб-интерфейс для управления защищенной структуры и экранированных виртуальных машин. 

На практике, нужно принять одно решение заранее: [режим аттестации](guarded-fabric-and-shielded-vms.md#attestation-modes-in-the-guarded-fabric-solution) используемые защищенной структуры. Существует два способа — два режима взаимно исключают друг друга, по которой HGS можно измерить, узлом Hyper-V находится в работоспособном состоянии. При инициализации HGS, необходимо выбрать режим:  

- Аттестация ключей узла или режим ключа менее безопасной, но легче внедрить  
- Аттестации на основе доверенного платформенного МОДУЛЯ или в режиме доверенного платформенного МОДУЛЯ, будет более безопасным, но требует дополнительные настройки и определенного оборудования

При необходимости можно развернуть в режиме ключа, с использованием существующих узлов Hyper-V, которые были обновлены до выпуска Windows Server Datacenter 2019 г. и затем преобразовать в более безопасный режим доверенного платформенного МОДУЛЯ при доступности поддержки серверное оборудование (включая TPM 2.0). 

Теперь, когда вы знаете, что представляют собой элементы, давайте разберем пример модели развертывания.

## <a name="how-to-get-from-a-current-hyper-v-fabric-to-a-guarded-fabric"></a>Как получить из текущей структуры Hyper-V в защищенную структуру

Давайте рассмотрим следующую ситуацию — у вас есть существующие структуру Hyper-V, например Contoso.com, на следующем рисунке, и требуется выполнить сборку Windows Server 2016 защищенной структуры.

![Существующие структуру Hyper-V](../media/Guarded-Fabric-Shielded-VM/guarded-fabric-existing-hyper-v.png)

## <a name="step-1-deploy-the-hyper-v-hosts-running-windows-server-2016"></a>Шаг 1. Разверните узлы Hyper-V под управлением Windows Server 2016 

Узлы Hyper-V необходимо запустить Windows Server 2016 Datacenter edition или более поздней версии. Если вы обновляете узлов, вы можете [обновление](https://technet.microsoft.com/windowsserver/dn527667.aspx) из выпуска Standard на Datacenter edition.

![Обновление узлов Hyper-V](../../security/media/Guarded-Fabric-Shielded-VM/guarded-fabric-deployment-step-one-upgrade-hyper-v.png)

## <a name="step-2-deploy-the-host-guardian-service-hgs"></a>Шаг 2. Развертывание службы защиты узла (HGS)

Затем установите роль сервера HGS и развернуть его как кластер с тремя узлами, как показано в примере relecloud.com на следующем рисунке. Для этого требуется три командлета PowerShell:

- Чтобы добавить роль HGS, `Install-WindowsFeature` 
- Чтобы установить HGS, используйте `Install-HgsServer` 
- Чтобы инициализировать с помощью вашей выбранный режим аттестации HGS, используйте `Initialize-HgsServer` 

Если существующих серверов Hyper-V не соответствуют необходимым условиям для режима доверенного платформенного МОДУЛЯ (например, у которых нет TPM 2.0), можно инициализировать с помощью администратора аттестации на основе (режим AD), требующий доверие Active Directory с доменом fabric HGS. 

В нашем примере предположим, Contoso изначально развертывается в режиме AD, чтобы немедленно соблюдения нормативных требований и планирует преобразовать в более безопасной аттестации на основе доверенного платформенного МОДУЛЯ после подходящий серверное оборудование можно приобрести. 

![Установка HGS](../media/Guarded-Fabric-Shielded-VM/guarded-fabric-deployment-step-two-deploy-hgs.png)

## <a name="step-3-extract-identities-hardware-baselines-and-code-integrity-policies"></a>Шаг 3. Извлечение удостоверения, базовые показатели оборудования и политик целостности кода

Процесс для извлечения удостоверений из узлов Hyper-V, зависит от используемый режим аттестации.

В режиме AD идентификатор узла является учетной записью компьютера, присоединенного к домену, который должен быть членом указанной группе безопасности в домене fabric.
Членство в назначенной группе является только определяет, принадлежат ли узел находится в работоспособном состоянии или нет. 

В этом режиме администратор структуры только она несет ответственность за обеспечение работоспособности узлов Hyper-V. Поскольку HGS играет роль, нет в определении того, какова или не разрешено запускать, вредоносных программ и отладчики будет правильно работать. 

Тем не менее отладчики, которые пытаются подключиться непосредственно к процессу (WinDbg.exe) блокируются для экранированных виртуальных машин, так как рабочий процесс виртуальной Машины (VMWP.exe) является свет защищенного процесса (PPL).
Альтернативные методы отладки, например используемые LiveKd.exe, не блокируются. В отличие от экранированные виртуальные машины рабочий процесс для виртуальных машин с поддержкой шифрования не выполняет PPL, поэтому Традиционные отладчики, такие как WinDbg.exe продолжит работать нормально.

Указано иначе, строгой проверки действия, используемая для режима доверенного платформенного МОДУЛЯ не используются для режима AD любым способом.

Для режима доверенного платформенного МОДУЛЯ необходимы три элемента: 

1.  Объект _открытом ключе подтверждения_ (или _EKpub_) из TPM 2.0 на каждом узле Hyper-V. Захвачены EKpub `Get-PlatformIdentifier`. 
2.  Объект _аппаратной базы_. Если каждый из узлов Hyper-V являются идентичными, один базовый план, то все, что вам нужно. Если это не так, то она понадобится для каждого класса оборудования. Базовые показатели — в виде файла журнала группы надежных вычислений или TCGlog. TCGlog содержит все, что узел был из встроенного по UEFI, через ядро, на которой полностью загружен узел. Чтобы записать базовые показатели оборудования, установите роль Hyper-V и средство поддержку защиты узла Hyper-V и использовать `Get-HgsAttestationBaselinePolicy`. 
3.  Объект _политику целостности кода_. Если каждый из узлов Hyper-V являются идентичными, одну политику непрерывной Интеграции, то все, что вам нужно. Если это не так, то она понадобится для каждого класса оборудования. Windows Server 2016 и Windows 10 имеют новая форма принудительного применения для политики целостности кода, вызывается _принудительно низкоуровневой оболочки целостности кода (HVCI)_. HVCI обеспечивает строгое применение области и гарантирует, что узел только сможет запускать исполняемые файлы, которые доверенный администратор разрешил его запуск. Эти инструкции помещаются в политику непрерывной Интеграции, которая добавляется к HGS. HGS измеряет политика целостности кода на каждом узле, прежде чем они выполняется разрешение на запуск экранированных виртуальных машин. Чтобы записать политика целостности кода, используйте `New-CIPolicy`. Политики, затем должны быть преобразованы в его с помощью двоичной форме `ConvertFrom-CIPolicy`.

![Извлечение удостоверения, базовых показателей и политика целостности кода](../media/Guarded-Fabric-Shielded-VM/guarded-fabric-deployment-step-three-extract-identity-baseline-ci-policy.png)

Это все, построении защищенной структуры, с точки зрения инфраструктуры для его запуска.  
Теперь вы можете создать экранированного диска шаблона виртуальной Машины и поэтому экранированных файл данных экранирования можно подготовить виртуальные машины, просто и безопасно. 

## <a name="step-4-create-a-template-for-shielded-vms"></a>Шаг 4. Создание шаблона для экранированных виртуальных машин

Шаблон экранированной виртуальной Машины обеспечивает защиту дисков шаблона, создавая подпись диска известных trustworthy общую точку во времени. 
Если диск шаблона позже заражен вредоносной программой, его подпись будет отличаться исходный шаблон, который будет определяться с помощью безопасного экранированной виртуальной Машины, процесс подготовки. 
Экранированные шаблона диски создаются путем запуска **экранированных мастер создания шаблонов диска** или `Protect-TemplateDisk` от обычных шаблонов диска. 

Каждый входит в состав **средства для экранированной виртуальной Машины** компонент в [удаленного сервера администрирования средств для Windows 10](https://www.microsoft.com/download/details.aspx?id=45520).
После загрузки средства удаленного администрирования сервера, выполните следующую команду для установки **средства для экранированной виртуальной Машины** функции:

```powershell
Install-WindowsFeature RSAT-Shielded-VM-Tools -Restart
```

Trustworthy администратора, например администратор структуры или владелец виртуальной Машины, потребуется войти диск формата VHDX шаблона сертификата (часто предоставляется поставщиком услуг размещения). 

![Мастер диск экранированного шаблона](../media/Guarded-Fabric-Shielded-VM/guarded-fabric-shielded-template-wizard.png)

Подпись вычисляется раздел виртуального диска операционной системы.
При изменении любых параметров в раздел операционной системы, подпись также будут изменены.
Это позволяет пользователям строго идентифицировать какие диски, они доверяют путем указания соответствующей сигнатурой.

Просмотрите [шаблона на диске](guarded-fabric-create-a-shielded-vm-template.md) перед началом работы. 

## <a name="step-5-create-a-shielding-data-file"></a>Шаг 5. Создайте файл данных экранирования 

Файл данных экранирования, также известный как PDK-файле, сбор конфиденциальных сведений о виртуальной машине, например, пароль администратора. 

![Данные экранирования](../media/Guarded-Fabric-Shielded-VM/guarded-fabric-deployment-step-five-create-shielding-data.png)

Файл данных экранирования также включает параметр политики безопасности для экранированной виртуальной Машины. Необходимо выбрать один из двух политик безопасности, когда вы создаете файл данных экранирования:

- Экранированный
   
    Наиболее безопасный вариант, тем самым устраняет многие административные направления атак.

- С поддержкой шифрования

    Пониженного уровня защиты, по-прежнему обеспечивает преимущества соответствия не сможет зашифровать виртуальную Машину, но позволяет администраторам Hyper-V, к примеру, с помощью подключения к консоли виртуальной Машины и PowerShell Direct. 

    ![Виртуальной Машине, поддерживаемой нового шифрования](../media/Guarded-Fabric-Shielded-VM/guarded-fabric-new-shielded-vm.png)

Вы можете добавить необязательное управления инициатив, таких как VMM или Windows Azure Pack. Если вы хотите создать виртуальную Машину без установки компонентов, см. в разделе [пошагового — Создание экранированных виртуальных машин без VMM](https://blogs.technet.microsoft.com/datacentersecurity/2016/06/06/step-by-step-creating-shielded-vms-without-vmm/).

## <a name="step-6-create-a-shielded-vm"></a>Шаг 6. Создание экранированной виртуальной Машины

Создание экранированных виртуальных машин мало отличается от обычных виртуальных машин. В Windows Azure Pack интерфейс очень даже проще, чем создание регулярных виртуальной Машины, так как необходимо только указать имя, экранирования файла данных (содержащий остальные сведения специализации) и сети виртуальных Машин. 

![Новой экранированной виртуальной Машины в Windows Azure Pack](../media/Guarded-Fabric-Shielded-VM/guarded-fabric-new-vm-config.png)

## <a name="next-step"></a>Дальнейшие действия

>[!div class="nextstepaction"]
[Предварительные требования HGS](guarded-fabric-prepare-for-hgs.md)