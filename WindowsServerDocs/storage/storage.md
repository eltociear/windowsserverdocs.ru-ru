---
title: Хранилище
description: ''
author: JasonGerend
manager: elizapo
layout: LandingPage
ms.prod: windows-server-threshold
ms.technology: storage
ms.assetid: 6b74bc7c-a58d-4915-af8e-2cc27f2c4726
ms.topic: landing-page
ms.author: jgerend
ms.localizationpriority: medium
ms.date: 03/08/2019
ms.openlocfilehash: d83d51ebf56d38f93c176d403ea5c6c14f625ee2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2019
ms.locfileid: "59833805"
---
# <a name="storage"></a>Хранилище

>Относится к: Windows Server 2019 г., Windows Server 2016, Windows Server (Semi-Annual Channel)

>[!TIP]
> Ищете дополнительные сведения о старых версиях Windows Server? Ознакомьтесь с нашими другими [библиотеками Windows Server](/previous-versions/windows/) на docs.microsoft.com. Кроме того, вы можете найти нужную информацию [на этом сайте](https://docs.microsoft.com/search/index?search=Windows+Server&dataSource=previousVersions).

<hr />
Хранилище в Windows Server предоставляет новые и улучшенные возможности для клиентов программно-определяемых центров обработки данных, использующих виртуализированные рабочие нагрузки. Windows Server также обеспечивает расширенную поддержку для корпоративных клиентов, использующих файловые серверы с существующими рабочими нагрузками.

<hr />
<ul class="cardsF panelContent">
<li>
 <a href="whats-new-in-storage.md">
                            <div class="cardSize">
                                <div class="cardPadding">
                                    <div class="card">
                                        <div class="cardImageOuter">
                                            <div class="cardImage">
                                                <img src="../media/i-whats-new.svg" alt="" />
                                            </div>
                                        </div>
                                        <div class="cardText">
                                            <h2>Что нового?</h2>
                                            <p>Новые возможности в Windows Server Storage</p>
                                        </div>
                                    </div>
                                </div>
                            </div>
                          </a>
                        </li>
</ul>
<hr />
<ul class="cardsF panelContent">
<li>
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../media/i-store.svg" alt="" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Программно-определяемое хранилище для виртуализированных рабочих нагрузок</h3>
<HR />
                        <p><h3><a href="storage-spaces/storage-spaces-direct-overview.md">Дисковые пространства</a></h3> Непосредственно подключаемые Локальные накопители, включая устройства SATA и NVME, чтобы оптимизировать использование дисков после добавления новых физических дисков и быстрее виртуального диска восстановить раз. Также см. раздел <a href="storage-spaces/overview.md">Дисковые пространства</a>, чтобы найти информацию об общих SAS и изолированных дисковых пространствах.</p>
<HR />
                        <p><h3><a href="storage-replica/storage-replica-overview.md">Реплика хранилища</a></h3> Независимую от хранилища, блочные синхронную репликацию между кластерами или серверами для аварийного ситуациям и восстановления, а также растягивать отказоустойчивый кластер на узлах для обеспечения высокой доступности. Синхронная репликация позволяет зеркально отображать данные на физических сайтах с отказоустойчивыми томами, что полностью предотвращает потерю данных на уровне файловой системы.</p>
<HR />
                        <p><h3><a href="storage-qos/storage-qos-overview.md">Качество обслуживания (QoS) хранилища</a></h3> Централизованно отслеживать и контролировать производительность хранилища виртуальных машин с помощью Hyper-V и роли масштабируемого файлового сервера автоматически improveing равномерное использование ресурсов хранилища между несколькими виртуальными машинами, используя один кластер файловых серверов.</p>
<HR />
                        <p><h3><a href="data-deduplication/overview.md">Дедупликация данных</a></h3> Она оптимизирует свободное место на томе, путем проверки данных на томе для дублирования. По завершении проверки дублирующиеся части набора данных тома сохраняются один раз и (при необходимости) сжимаются для дополнительной экономии. Дедупликация оптимизирует избыточные данные, не нарушая достоверность или целостность данных.</p>
                    </div>
                </div>
            </div>
        </div>
    </li>
<li>
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../media/i-store.svg" alt="" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Файловые серверы общего назначения</h3>
<HR />
                        <p><h3><a href="storage-migration-service/overview.md">Служба миграции хранилища</a></h3>Перенос серверов до более новой версии Windows Server, используя графическое средство, которое проводит инвентаризацию данные на серверах, передает данные и конфигурацию на более новых серверах и при необходимости перемещает удостоверения старых серверов на новые серверы таким образом, приложений и пользователей не нужно ничего менять.</p>
<HR />
                        <p><h3><a href="work-folders/work-folders-overview.md">Рабочие папки</a></h3> Store и доступ к рабочим файлам на персональных компьютерах и устройствах, часто называют перевести-принеси свое устройство (BYOD), помимо корпоративных ПК. Пользователи получают удобное место для хранения рабочих файлов и доступа к ним из любого места. Организации контролируют корпоративные данные, храня файлы на централизованно управляемых файловых серверах и при необходимости задавая политики устройств пользователей (такие как шифрование и пароли блокировки экрана).</p>
<HR />
                        <p><h3><a href="folder-redirection/folder-redirection-rup-overview.md">Автономные файлы и перенаправление папок</a></h3> Перенаправлять путь к локальным папкам (например, папка «документы») в сети во время кэширования содержимого локально для увеличения скорости и доступности.</p>
<HR />
                        <p><h3><a href="folder-redirection/deploy-roaming-user-profiles.md">Перемещаемые профили пользователей</a></h3> Перенаправлять профиль пользователя в сетевую папку.</p>
<HR />
                        <p><h3><a href="dfs-namespaces/dfs-overview.md">Пространства имен DFS</a></h3> Объединения общих папок, находящихся на разных серверах, в один или несколько логически структурированных пространств имен. Каждое пространство имен представляется пользователям как одна общая папка с серией вложенных папок. Однако базовая структура пространства имен может состоять из многих файловых ресурсов общего доступа, расположенных на различных серверах и нескольких сайтах.</p>
<HR />
                        <p><h3><a href="dfs-replication/dfsr-overview.md">Служба репликации DFS</a></h3> Реплицировать папки (включая те, обращение по пути пространства имен DFS) между множеством серверов и сайтов. Репликация DFS использует алгоритм сжатия, называемый удаленным разностным сжатием (remote differential compression — RDC). Алгоритмом удаленного разностного сжатия определяются изменения данных в файле и активируется репликация DFS для репликации только измененных блоков файла вместо всего файла.</p>
<HR />
                        <p><h3><a href="fsrm/fsrm-overview.md">Диспетчер ресурсов файлового сервера</a></h3> Управление и классификации данных, сохраненных на файловых серверах.<p>
<HR />
                        <p><h3><a href="iscsi/iscsi-target-server.md">Сервер цели iSCSI</a></h3> Предоставляет блочные хранилища другим серверам и приложениям с помощью стандарта Internet SCSI (iSCSI).</p>
<HR />
                       <p><h3><a href="iscsi/iscsi-boot-overview.md">Сервер цели iSCSI</a></h3> Может загружать сотни компьютеров из одного образа операционной системы, хранящийся в центральном расположении. Это улучшает эффективность, управляемость, доступность и безопасность.</p>
                    </div>
                </div>
            </div>
        </div>
    </li>
<li>
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../media/i-store.svg" alt="" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Файловые системы, протоколы и т. д.</h3>
<HR />
                        <p><h3><a href="refs/refs-overview.md">ReFS</a></h3> Восстанавливаемая файловая система, которая повышает доступность данных, обеспечивает эффективное масштабирование для очень больших наборов данных различных вариантов нагрузки и обеспечивает целостность данных благодаря устойчивости к повреждениям (вне зависимости от сбоев оборудования или программного обеспечения).<p>
<HR />
                        <p><h3><a href="file-server/file-server-smb-overview.md">Протокол Server Message Block (SMB)</a></h3> Файл сетевой протокол, который позволяет приложениям на компьютере для чтения и записи в файлы, а также для запроса службы серверных программ в компьютерной сети общего доступа. Протокол SMB может использоваться поверх протокола TCP/IP или других сетевых протоколов. С помощью протокола SMB приложение (или использующий его пользователь) может получать доступ к файлам и другим ресурсам удаленного сервера. Это позволяет приложениям читать, создавать и обновлять файлы на удаленном сервере. Этот протокол может также обмениваться данными с любой серверной программой, которая настроена на получение клиентских запросов SMB.<p>
<HR />
                        <p><h3><a href="storage-spaces/Storage-class-memory-health.md">Память класса хранилища</a></h3> Обеспечивает производительность, как объем памяти компьютера (очень высокую), но с сохранением данных обычных дисках. Система Windows работает с памятью класса хранилища так же, как обычными дисками (только более быстрыми), но есть ряд отличий в управлении работоспособностью устройств.<p>
<HR />
                        <p><h3><a href="https://technet.microsoft.com/library/cc766295(v=ws.10).aspx">Шифрование диска BitLocker</a></h3> Сохраняет данные на томах в зашифрованном виде, даже если незаконно компьютера или операционной системы не запущена. Это позволяет обеспечить защиту от атак по сети, атак, совершаемых путем отключения или обхода установленной операционной системы, а также путем извлечения жесткого диска для получения прямого доступа к данным.<p>
<HR />
                        <p><h3><a href="https://technet.microsoft.com/library/dn466522(v=ws.11).aspx">NTFS</a></h3> Основная файловая система в последних версиях Windows и Windows Server — предоставляет полный набор функций, включая дескрипторы безопасности, шифрование, дисковые квоты и расширенные метаданные и может использоваться для предоставления непрерывно с Общие тома кластера (CSV) доступные тома, которые могут осуществлять одновременно из нескольких узлов отказоустойчивого кластера.<p>
<HR />
                        <p><h3><a href="https://technet.microsoft.com/library/jj592688(v=ws.11).aspx">Сетевой файловой системы (NFS)</a></h3> Предоставляет общего решения для предприятий с разнородными средами, которые состоят из Windows и компьютеров, отличных от Windows.<p>
                    </div>
                </div>
            </div>
        </div>
    </li>
</ul>

---


## <a name="in-azure"></a>В Azure

* [Служба хранилища Azure](https://azure.microsoft.com/documentation/services/storage/)
* [Azure StorSimple](https://www.microsoft.com/en-us/cloud-platform/azure-storsimple)