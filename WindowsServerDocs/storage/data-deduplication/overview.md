---
ms.assetid: 4b844404-36ba-4154-aa5d-237a3dd644be
title: "Обзор дедупликации данных"
ms.technology: storage-deduplication
ms.prod: windows-server-threshold
ms.topic: article
author: wmgries
manager: klaasl
ms.author: wgries
ms.date: 05/09/2017
ms.openlocfilehash: 4344108f96d14475c15a31bd1ab917e7fc78ef9f
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/17/2017
---
# <a name="data-deduplication-overview"></a>Обзор дедупликации данных

> Область применения: Windows Server (Semi-Annual Channel), Windows Server 2016

## <a name="what-is-dedup"></a>Что такое дедупликация данных

Дедупликацию данных для краткости часто называют Dedup. Это функция Windows Server 2016, с помощью которой можно уменьшить влияние избыточных данных на стоимость хранения. Если дедупликация данных включена, она оптимизирует свободное место в томе за счет проверки данных тома на наличие дублирующихся частей. Дублирующиеся части набора данных тома сохраняются один раз и (при необходимости) сжимаются для дополнительной экономии. Дедупликация оптимизирует избыточные данные, не нарушая достоверность или целостность данных. Дополнительные сведения о дедупликации данных см. в разделе [Как работает дедупликация данных?](understand.md#how-does-dedup-work) на странице [Общие сведения о дедупликации данных](understand.md).

> [!Important]  
> Обновление [KB4025334](https://support.microsoft.com/kb/4025334) содержит накопительный пакет исправлений, в том числе обеспечивающих надежность системы. Мы настоятельно рекомендуем установить его при использовании дедупликации данных в Windows Server 2016.

## <a name="why-is-dedup-useful"></a>Преимущества дедупликации данных

Дедупликация данных помогает администраторам хранилища снизить затраты, связанные с дублирующимися данными. Зачастую в больших наборах данных **<u>многие</u>** данные дублируются, что увеличивает затраты на их хранение. Например:

- Файловые ресурсы пользователей могут содержать множество копий одних и тех же или похожих файлов.
- Гостевые службы виртуализации могут практически не отличаться от служб на виртуальных машинах.
- Моментальные снимки резервных копий могут иметь минимальные отличия от ежедневных.

Экономия места, которую может обеспечить дедупликация данных, зависит от набора данных или рабочей нагрузки в томе. В наборах данных с высоким уровнем дупликации скорость оптимизации достигает 95%, а объем использования службы хранилища может уменьшаться в 20раз. В следующей таблице представлены типичные значения экономии за счет дедупликации для разных типов содержимого.

| Сценарий       | Содержимое                                        | Обычная экономия пространства |
|----------------|------------------------------------------------|-----------------------|
| Документы пользователя | Документы Office, фотографии, музыка, видео ит.д.  | 30-50 %                |
| Общие ресурсы развертывания | Двоичные файлы программного обеспечения, CAB-файлы, символы и т.д. | 70–80 %                |
| Библиотеки виртуализации | Образы ISO, файлы виртуальных жестких дисков и т.д.  | 80–95 %                |
| Файловый ресурс общего доступа | Все вышеперечисленное                           | 50–60 %                |

## <a id="when-can-dedup-be-used"></a>Когда можно использовать дедупликацию данных  
<table>
    <tbody>
        <tr>
            <td style="text-align:center;min-width:150px;vertical-align:center;"><img src="media/overview-clustered-gpfs.png" alt="Illustration of file servers" /></td>
            <td style="vertical-align:top">
                <b>Файловые серверы общего назначения</b><br />
Файловые серверы общего назначения представляют собой файловые серверы для общего использования, которые могут содержать общие папки любого типа из перечисленных далее: <ul>
                    <li>Общие групповые папки</li>
                    <li>домашние папки пользователей;</li>
                    <li><a href="https://technet.microsoft.com/library/dn265974.aspx">рабочие папки</a></li>
                    <li>Общие ресурсы для разработки программного обеспечения</li>
                </ul>
Файловые серверы общего назначения подходят для дедупликации данных из-за тенденции сохранения многочисленных копий или версий одного файла несколькими пользователями. От дедупликации данных выигрывают общие ресурсы для разработки программного обеспечения, так как многие двоичные файлы остаются по сути неизменными от сборки к сборке. 
            </td>
        </tr>
        <tr>
            <td style="text-align:center;min-width:150px;vertical-align:center;"><img src="media/overview-vdi.png" alt="Illustration of VDI servers" /></td>
            <td style="vertical-align:top">
                <b>Развертывания инфраструктуры виртуальных рабочих столов (VDI)</b><br />
Благодаря серверам VDI, таким как <a href="https://technet.microsoft.com/library/cc725560.aspx">службы удаленных рабочих столов</a>, организации получают упрощенный способ подготовки настольных компьютеров для пользователей. Эта технология подходит для организаций по многим причинам. <ul>
                    <li><b>Развертывание приложений</b>: вы получаете возможность быстрого развертывания приложений в среде предприятия. Это особенно полезно при наличии приложений, которые часто обновляются, редко используются или являются сложными в управлении.</li>
                    <li><b>Консолидация приложений</b>: при установке и запуске приложений из набора централизованно управляемых виртуальных машин больше нет необходимости обновлять приложения на клиентских компьютерах. Это также снижает требования к пропускной способности сети, необходимой для доступа к приложениям.</li>
                    <li><b>Удаленный доступ</b>: пользователи могут получать доступ к корпоративным приложениям с таких устройств, как домашние компьютеры, киоски и маломощное оборудование, а также из операционных систем, отличных от Windows.</li>
                    <li><b>Доступ к филиалам</b>: развертывания VDI могут обеспечить лучшую производительность приложений для работников филиала, которым требуется доступ к централизованным хранилищам данных. Ресурсоемкие приложения иногда не имеют протоколов клиентов и серверов, оптимизированных для подключений по медленной линии.</li>
                </ul>
Развертывания VDI прекрасно подходят для дедупликации данных, так как виртуальные жесткие диски, определяющие удаленные рабочие столы для пользователей, по сути идентичны. Кроме того, дедупликация данных может помочь в случае падения производительности хранилища на пиковых нагрузках (так называемый *VDI boot storm*), когда множество пользователей одновременно входит на настольные системы в начале дня.
            </td>
        </tr>
        <tr>
            <td style="text-align:center;min-width:150px;vertical-align:center;"><img src="media/overview-backup.png" alt="Illustration of backup applications" /></td>
            <td style="vertical-align:top">
                <b>Целевые объекты резервного копирования, например виртуализированные приложения резервного копирования</b><br />
Приложения резервного копирования, такие как <a href="https://technet.microsoft.com/library/hh758173.aspx">Microsoft Data Protection Manager (DPM)</a>, прекрасно подходят для дедупликации данных, так как значительная часть моментальных снимков резервных копий дублируется.
            </td>
        </tr>
        <tr>
            <td style="text-align:center;min-width:150px;vertical-align:center;"><img src="media/overview-other.png" alt="Illustration of other workloads" /></td>
            <td style="vertical-align:top">
                <b>Другие рабочие нагрузки</b><br />
                [К другим рабочим нагрузкам также можно применять дедупликацию данных](install-enable.md#enable-dedup-candidate-workloads).
            </td>
        </tr>
    </tbody>
</table>