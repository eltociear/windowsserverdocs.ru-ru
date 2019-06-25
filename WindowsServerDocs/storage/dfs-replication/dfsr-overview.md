---
Title: Общие сведения о репликации DFS
ms.date: 03/08/2019
ms.prod: windows-server-threshold
ms.technology: storage
author: JasonGerend
manager: elizapo
ms.author: jgerend
ms.openlocfilehash: dd381c04b02889a7f2e7b8992ff6050d1b0f078a
ms.sourcegitcommit: 48bb3e5c179dc520fa879b16c9afe09e07c87629
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/31/2019
ms.locfileid: "66453062"
---
# <a name="dfs-replication-overview"></a>Общие сведения о репликации DFS

> Относится к: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008, Windows Server (Semi-Annual Channel)

Репликация DFS — это служба роли в Windows Server, который предоставляет возможность эффективно реплицировать папки (включая те, обращение по пути пространства имен DFS) между множеством серверов и сайтов. Репликация DFS — это эффективный и нескольких основных репликации обработчик, который можно использовать для синхронизации папок между серверами внутри сетевых подключений ограниченной пропускной способностью. Заменяет как механизм репликации службы репликации файлов (FRS) для пространств имен DFS, а также для репликации папки SYSVOL доменных служб Active Directory (AD DS) в доменах, использующих Windows Server 2008 или более поздней режим работы домена.

Репликация DFS использует алгоритм сжатия, называемый удаленным разностным сжатием (remote differential compression — RDC). RDC выявляет изменения данных в файле и активируется репликация DFS для репликации только измененных блоков файла вместо всего файла.

Дополнительные сведения о репликации SYSVOL с помощью репликации DFS см. в разделе [миграции репликации SYSVOL с репликацией DFS](migrate-sysvol-to-dfsr.md).

Для использования репликации DFS, необходимо создать группы репликации и добавление реплицированных папок в группы. На следующем рисунке показаны группы репликации, реплицированных папок и элементов.

![Группа репликации, содержащий соединение между двумя членами, каждая из которых имеет несколько реплицированных папок](media/dfsr-overview.gif)

На этом рисунке показано, что группу репликации — это набор серверов, известный как члены, который участвует в репликации один или несколько реплицируемых папок. Реплицируемой папки — это папка, которая остается синхронизированным на каждом члене. На рисунке имеется две реплицированной папки: Проекты и предложений. По мере изменения данных в каждой реплицированной папки изменения реплицируются по подключениям между членами группы репликации. Подключения между всеми членами формирования топологии репликации.
Создание нескольких реплицируемых папок в одну группу репликации упрощает процесс развертывания реплицированных папок, так как топология, расписания и полосы пропускания для группы репликации применяются к каждой реплицированной папки. Для развертывания дополнительных реплицированных папок, можно использовать Dfsradmin.exe или следуйте инструкциям в мастере задать локальный путь и разрешения для новой реплицируемой папки.

Каждой реплицированной папки имеет уникальные параметры, такие как файлы и вложенные фильтры, чтобы отфильтровать различные файлы и вложенные папки для каждой реплицированной папки.

Реплицированных папок, хранящихся на каждом члене может находиться на разных томах в члене и реплицированных папок не обязательно должны быть общих папок или частью пространства имен. Тем не менее оснастка "Управление DFS" упрощает совместное использование реплицированных папок и при необходимости публиковать их в существующее пространство имен.

Для администрирования репликации DFS с помощью управления DFS, DfsrAdmin и Dfsrdiag команд или сценариев, вызывающих WMI.

## <a name="requirements"></a>Требования

До начала развертывания репликации распределенной файловой системы (DFS) необходимо настроить серверы следующим образом.

- Обновите схему доменных служб Active Directory (AD DS), Windows Server 2003 R2 или более поздней версии дополнений схемы. Реплицированные папки только для чтения нельзя использовать с Windows Server 2003 R2 или более старых дополнений схемы.
- Убедитесь, что все серверы в группе репликации находятся в одном и том же лесу. Репликация на серверах, находящихся в разных лесах, недоступна.
- Установите репликацию DFS на все серверы, которые будут членами группы репликации.
- Чтобы проверить совместимость антивирусного программного обеспечения с репликацией распределенной файловой системы (DFS), свяжитесь с поставщиком антивирусного программного обеспечения.
- Найдите все папки, которые требуется реплицировать, на томах, форматированных в файловой системе NTFS. Репликация DFS не поддерживает файловые системы ReFS (Resilient File System) и FAT. Также репликация DFS не поддерживает репликацию содержимого общих томов кластера.

## <a name="interoperability-with-azure-virtual-machines"></a>Взаимодействие с виртуальными машинами Azure

С помощью репликации DFS на виртуальной машине в Azure была протестирована с Windows Server; Однако существуют некоторые ограничения и требования, которые необходимо выполнить.

- Использование снимков или сохраненных состояний для восстановления сервера, выполняющего репликацию DFS с целью реплицирования любых данных, кроме папки SYSVOL, приводит к отказу репликации DFS, что требует особых действий по восстановлению базы данных. Нельзя экспортировать, клонировать или копировать виртуальные машины. Дополнительные сведения см. в статье [2517913](http://support.microsoft.com/kb/2517913) базы знаний Майкрософт и в разделе [Безопасная виртуализация DFSR](https://blogs.technet.microsoft.com/filecab/2013/04/05/safely-virtualizing-dfsr/).
- При резервном копировании данных в реплицированной папке, размещенной на виртуальной машине, необходимо использовать программы резервного копирования из гостевой виртуальной машины.
- Служба репликации DFS требуется доступ к контроллерам домена физической и виртуальной — он не может взаимодействовать непосредственно с Azure AD.
- Репликации DFS требуется VPN-подключение между локальными членами группы репликации и другими элементами, размещенными на виртуальных машинах Azure. Необходимо также настроить локальный маршрутизатор (например, Microsoft Forefront Threat Management Gateway) для разрешения сопоставителя конечных точек RPC (порт 135) и назначения случайным образом порта между 49152 и 65535 для передачи через VPN-подключение. Для указания статического порта вместо случайного можно использовать командлет Set-DfsrMachineConfiguration или средство командной строки Dfsrdiag. Дополнительные сведения о способах указания статического порта для репликации DFS см. в разделе [Set-DfsrMachineConfiguration](https://docs.microsoft.com/powershell/module/dfsr/set-dfsrserviceconfiguration). Сведения о связанных портах, используемых для управления Windows Server, см. в статье [832017](http://support.microsoft.com/kb/832017) в базе знаний Майкрософт.

Дополнительные сведения о начале работы с виртуальными машинами Azure см. на [веб-сайте Microsoft Azure](https://docs.microsoft.com/azure/virtual-machines/).

## <a name="installing-dfs-replication"></a>Установка репликации DFS

Репликация DFS входит в роль файловых служб и служб хранилища. Средства управления для DFS (DFS-управление, модуль репликации DFS для Windows PowerShell и средства командной строки) устанавливаются отдельно, как часть средств удаленного администрирования сервера.

Установите репликацию DFS с помощью [Windows Admin Center](../../manage/windows-admin-center/understand/windows-admin-center.md), диспетчер серверов или PowerShell, как описано в следующих разделах.

### <a name="to-install-dfs-by-using-server-manager"></a>Чтобы установить DFS с помощью диспетчера серверов

1. Откройте диспетчер серверов, щелкните **Управление**, а затем нажмите кнопку **Добавить роли и компоненты**. Откроется мастер добавления ролей и компонентов.

2. На странице **Выбор сервера** выберите сервер или виртуальный жесткий диск автономной виртуальной машины, на который требуется установить DFS.

3. Выберите службы ролей и компоненты, которые следует установить.

    - Чтобы установить службу репликации DFS на **ролей сервера** выберите **репликации DFS**.

    - Чтобы установить только средства управления DFS, на странице **Компоненты** разверните узлы **Средства администрирования удаленного сервера**, **Средства администрирования ролей**, **Средства файловых служб**, а затем выберите **Средства управления DFS**.

         **Средства управления DFS** устанавливает "Управление DFS" оснастки, репликация DFS и модулей пространства имен DFS для Windows PowerShell и средства командной строки, но не устанавливает никаких служб DFS на сервере.

### <a name="to-install-dfs-replication-by-using-windows-powershell"></a>Установка репликации DFS с помощью Windows PowerShell

Откройте сеанс Windows PowerShell с повышенными правами и введите следующую команду, где < имя\> — это служба роли или компонент, который вы хотите установить (см. ниже таблицу со списком соответствующих имен служб ролей или компонентов):

```PowerShell
Install-WindowsFeature <name>
```

|Служба роли или компонент|Имя|
|---|---|
|Репликация DFS|`FS-DFS-Replication`|
|Средства управления DFS|`RSAT-DFS-Mgmt-Con`|

Например, для установки средств распределенной файловой системы, включенных в компонент средств удаленного администрирования сервера, введите:

```PowerShell
Install-WindowsFeature "RSAT-DFS-Mgmt-Con"
```

Чтобы установить репликации DFS и части средств распределенной файловой системы, компонента средств удаленного администрирования сервера, введите следующую команду:

```PowerShell
Install-WindowsFeature "FS-DFS-Replication", "RSAT-DFS-Mgmt-Con"
```

## <a name="see-also"></a>См. также

- [Обзор пространств имен DFS и репликации DFS](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj127250(v%3dws.11))
- [Контрольный список. Репликация DFS развернута](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc772201(v%3dws.11))
- [Контрольный список. Управление репликацией DFS](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc755035(v%3dws.11))
- [Развертывание репликации DFS](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc770925(v%3dws.11))
- [Управление репликацией DFS](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc770925(v%3dws.11))
- [Устранение неполадок репликации DFS](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc732802(v%3dws.11))