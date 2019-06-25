---
ms.assetid: 45a65504-70b5-46ea-b2e0-db45263fabaa
title: Поддержка использования реплики Hyper-V для виртуализированных контроллеров домена
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 0203c6de55a4e691d7c484351a3280c49891f317
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2019
ms.locfileid: "59866285"
---
# <a name="support-for-using-hyper-v-replica-for-virtualized-domain-controllers"></a>Поддержка использования реплики Hyper-V для виртуализированных контроллеров домена

>Область применения. Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

В данном разделе поясняется поддержка использования реплики Hyper-V для репликации виртуальной машины, которая работает в качестве контроллера домена. Реплика Hyper-V — это новый компонент Hyper-V, появившийся в Windows Server 2012, который предоставляет встроенный механизм репликации на уровне виртуальных машин.  
  
Реплика Hyper-V асинхронно реплицирует выбранные виртуальные машины с основного узла Hyper-V на узел реплики Hyper-V по каналам локальной или глобальной сети. После завершения начальной репликации последующие изменения реплицируются с интервалом, заданным администратором.  
  
Отработка отказа может быть как запланированной, так и незапланированной. Запланированная отработка отказа инициируется администратором для основной виртуальной машины, а все нереплицированные изменения копируются в виртуальную машину реплики для предотвращения потери данных. Незапланированная отработка отказа инициируется в виртуальной машине реплики при реагировании на непредвиденный сбой основной виртуальной машины. Потеря данных может произойти из-за отсутствия возможности передать изменения на основной виртуальной машине, которые, возможно, еще не были реплицированы.  
  
Дополнительные сведения о Hyper-V Replica см. в разделе [Обзор Hyper-V Replica](https://technet.microsoft.com/library/jj134172.aspx) и [Развертывание Hyper-V Replica](https://technet.microsoft.com/library/jj134207.aspx).  
  
> [!NOTE]  
> Реплика Hyper-V может выполняться только в Windows Server Hyper-V, в версии Hyper-V под управлением Windows 8 этот компонент не работает.  
  
## <a name="windows-server-2012-or-newer-domain-controllers-required"></a>Windows Server 2012 или более новые требуется контроллер домена

Windows Server 2012 Hyper-V появился ИД создания виртуальной Машины (VMGenID). ИД создания виртуальной машины предоставляет низкоуровневой оболочке средство взаимодействия с гостевой ОС при внесении существенных изменений. Например, низкоуровневая оболочка может сообщить виртуализированному контроллеру домена, что было выполнено восстановление из моментального снимка (технология восстановления моментальных снимков Hyper-V, а не резервных копий). AD DS в Windows Server 2012 и более поздних версий поддерживает технологию виртуальных Машин VMGenID и используют ее для обнаружения при выполнении операций низкоуровневой оболочки, таких как восстановление моментального снимка, который позволяет лучше защитить себя.  
  
> [!NOTE]
> Только AD DS на контроллеров домена Windows Server 2012 или более поздней версии предоставляют эти меры безопасности, полученный в результате VMGenID; Контроллеры домена под управлением всех предыдущих версиях Windows Server будут возникать проблемы, например отката номера последовательного обновления, которые могут возникнуть при восстановлении виртуализированного контроллера домена с использованием неподдерживаемого механизма, таких как восстановление моментального снимка. Дополнительные сведения об этих мерах безопасности и условиях их активации см. в разделе [Архитектура виртуализированных контроллеров доменов](https://technet.microsoft.com/library/jj574118.aspx).  
  
В случае отработки отказа реплики Hyper-V (запланированная или незапланированная) виртуализованного контроллера домена обнаруживает Сброс VMGenID, активируя функции безопасности в упомянутых выше. После этого операции Active Directory продолжают выполняться в обычном режиме. Виртуальная машина реплики выполняется вместо основной виртуальной машины.  
  
> [!NOTE]  
> Учитывая наличие двух экземпляров одного удостоверения контроллера домена, существует вероятность одновременного выполнения как основного, так и реплицированного экземпляра. Хотя реплика Hyper-V снабжена управляющими механизмами, предотвращающими одновременное выполнение основной виртуальной машины и виртуальной машины реплики, такая ситуация все же возможна в случае обрыва канала связи между ними после репликации виртуальной машины. Если такая маловероятная ситуация все же возникнет, в виртуализированных контроллерах домена под управлением Windows Server 2012 предусмотрены специальные меры безопасности для защиты доменных служб Active Directory, в виртуализированных контроллерах домена, работающих под управлением предыдущих версий Windows Server, такие меры отсутствуют.  
  
При использовании Hyper-V Replica убедитесь, что выполнены рекомендации для [работающих виртуальных контроллеров доменов на Hyper-V](https://technet.microsoft.com/library/virtual_active_directory_domain_controller_virtualization_hyperv(v=WS.10).aspx). Среди прочего, в этом разделе рассматриваются рекомендации по хранению файлов Active Directory на виртуальных дисках SCSI, что позволяет гарантировать сохранность данных.  
  
## <a name="supported-and-unsupported-scenarios"></a>Поддерживаемые и неподдерживаемые сценарии

Только виртуальные машины, что запуска Windows Server 2012 или более новые поддерживаются для незапланированной и тестовой отработки отказа. Даже для плановой отработки отказа чтобы снизить риски в случае, когда администратор непреднамеренно запускает основной виртуальной Машины и реплицируемая виртуальная машина в то же время для виртуализованного контроллера домена рекомендуется Windows Server 2012 или более поздней версии.  
  
Виртуальные машины под управлением предыдущих версий Windows Server поддерживаются для запланированной отработки отказа, однако не поддерживаются для незапланированной отработки отказа в связи с риском отката номера последовательного обновления. Дополнительные сведения об откате USN см. в разделе [USN и откат USN](https://technet.microsoft.com/library/d2cae85b-41ac-497f-8cd1-5fbaa6740ffe(v=ws.10)).  
  
> [!NOTE]  
> Требования к режиму работы для домена или леса отсутствуют, имеются требования только требования к операционной системе для контроллеров домена, работающих в качестве виртуальных машин, которые реплицируются с использованием реплики Hyper-V. Виртуальные машины можно развернуть в лесу, содержащем другие физические или виртуальные контроллеры домена, которые работают под управлением предыдущих версий Windows Server и также могут как реплицироваться, так и не реплицироваться с помощью реплики Hyper-V.  
  
Данное заявление о поддержке основано на тестах, проведенных в лесе с одним доменом, однако конфигурации леса с несколькими доменами также поддерживаются. Для этих тестов виртуализированные контроллеры домена DC1 и DC2 являются партнерами репликации Active Directory на одном сайте, размещенном на сервере, где выполняется Hyper-V в Windows Server 2012. В операционной системе виртуальной машины, где выполняется DC2, включена реплика Hyper-V. Сервер-реплика размещается в другом географически удаленном центре обработки данных. Чтобы упростить восприятие приведенных ниже процедур тестового случая, для виртуальной машины, выполняемой на сервере-реплике, используется имя DC2-Rec (хотя на практике она сохраняет имя исходной виртуальной машины).  
  
### <a name="windows-server-2012"></a>Windows Server 2012

В следующей таблице поясняется поддержка виртуализированных контроллеров домена, работающих под управлением Windows Server 2012, и тестовых случаев.  
  
|||  
|-|-|  
|Запланированная отработка отказа|Незапланированная отработка отказа|  
|Поддерживается|Поддерживается|  
|Тестовый случай:<br /><br />-DC1 и DC2 работают Windows Server 2012.<br /><br />-DC2 отключен, и отработка отказа выполняется на DC2-Rec. Отработка отказа может быть запланированной или незапланированной.<br /><br />-После запуска DC2-Rec проверяет, является ли значение VMGenID в его базе данных совпадает со значением в драйвере виртуальной машины, сохранена на сервере реплики Hyper-V.<br /><br />— В результате DC2-Rec активирует меры безопасности виртуализации; Другими словами он сбрасывает свой InvocationID, отменяет свой пул относительных ИДЕНТИФИКАТОРОВ и задает требование начальной синхронизации, прежде чем делать предположение о роли хозяина операций. Дополнительные сведения о требовании начальной синхронизации см. в разделе .<br /><br />-Затем DC2-Rec сохраняет новое значение VMGenID в своей базе данных и фиксирует все последующие обновления в контексте нового InvocationID.<br /><br />— В результате использования сброса InvocationID DC1 объединит все изменения AD, вызванные DC2-Rec, даже если он был выполнен откат, времени, то есть все обновления AD выполняется на DC2-Rec после отработки отказа, выполняется безопасное схождение|Тестовый случай аналогичен плановую отработку отказа, со следующими исключениями:<br /><br />— Любое AD обновляет полученные на DC2, но еще не реплицированные AD на партнера репликации до отработки отказа, будут утеряны.<br /><br />-AD обновления, полученные на DC2 после время точки восстановления, которые были реплицированы Active Directory на DC1 будут реплицированы с DC1 обратно на DC2-Rec.|  
  
### <a name="windows-server-2008-r2-and-earlier-versions"></a>Windows Server 2008 R2 и более ранних версий

В следующей таблице поясняется поддержка виртуализированных контроллеров домена, работающих под управлением Windows Server 2008 R2 и более ранних версий.  
  
|||  
|-|-|  
|Запланированная отработка отказа|Незапланированная отработка отказа|  
|Поддерживается, но не рекомендуется, так как контроллеры домена, работающие под управлением этих версий Windows Server, не поддерживают VMGenID или использование соответствующих мер безопасности. Поэтому они подвержены риску отката номера последовательного обновления. Дополнительные сведения см. в разделе [USN и откат USN](https://technet.microsoft.com/library/d2cae85b-41ac-497f-8cd1-5fbaa6740ffe(v=ws.10)).|Не поддерживается **Примечание:** Незапланированная отработка отказа поддерживается только в тех ситуациях, где отсутствует риск отката номера последовательного обновления, например, при наличии единственного контроллера домена в лесу (использовать такую конфигурацию не рекомендуется).|  
|Тестовый случай:<br /><br />-DC1 и DC2 под управлением Windows Server 2008 R2.<br /><br />-DC2 отключен, и на DC2-Rec выполняется запланированная отработка отказа. Все данные на DC2 реплицируются на DC2-Rec до окончания процедуры завершения работы.<br /><br />-После запуска DC2-Rec возобновляет репликацию с DC1, используя то же значение invocationID в качестве DC2.|Н/Д|  