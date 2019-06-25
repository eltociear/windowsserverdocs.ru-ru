---
title: Безопасно виртуализация доменных служб Active Directory (AD DS)
description: Откат USN и безопасная виртуализация Active Directory
ms.topic: article
ms.prod: windows-server-threshold
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 03/22/2019
ms.technology: identity-adds
ms.assetid: 7a3114c8-bda8-49bb-83a8-4e04340ab221
ms.openlocfilehash: aa84e09e8a958193fee82c7b9c03cd1dca910c55
ms.sourcegitcommit: 2977c707a299929c6ab0d1e0adab2e1c644b8306
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/24/2019
ms.locfileid: "63684192"
---
# <a name="safely-virtualizing-active-directory-domain-services-ad-ds"></a>Безопасно виртуализация доменных служб Active Directory (AD DS)

>Область применения. Windows Server

Начиная с Windows Server 2012, AD DS предоставляют лучшую поддержку виртуализации контроллеров доменов благодаря возможностям безопасной виртуализации. В этой статье объясняется роль номера USN и InvocationIDs в репликации контроллера домена и рассматриваются некоторые возможные проблемы, которые могут возникнуть.

## <a name="update-sequence-number-and-invocationid"></a>Номер последовательного обновления и InvocationID

Виртуальные среды представляют особую трудность для распределенных рабочих потоков, зависящих от логической схемы репликации по времени. Например, репликация AD DS использует равномерно увеличивающееся значение (которое называется USN, или номер последовательного обновления), назначенное транзакциям в каждом контроллере домена. Экземпляр базы данных на каждом контроллере домена присваивается удостоверение, под названием InvocationID. InvocationID контроллера домена и его номер последовательного обновления вместе служат уникальным идентификатором, который связан с каждой транзакцией записи, выполняемой на каждом контроллере домена, и должны быть уникальны в пределах леса.

Репликация AD DS использует InvocationID и номер последовательного обновления на каждом контроллере домена, чтобы определить, какие изменения необходимо повторить на других контроллерах домена. Если контроллер домена является временем откат за пределами информированности контроллера домена, повторном использовании USN для абсолютно другой транзакции репликация не будет осуществляться, так как другие контроллеры домена будут считать, что они уже получили обновления связанный с повторно использованным номером последовательного обновления в контексте данного InvocationID.

Например, следующая иллюстрация показывает последовательность событий, происходящих в ОС Windows Server 2008 R2 и более ранних версиях, когда обнаруживается откат номера последовательного обновления на VDC2 — целевом контроллере домена, работающем на виртуальной машине. На этом рисунке обнаружение откат USN происходит на контроллере VDC2, когда партнер репликации обнаруживает, что VDC2 отправил значение номера последовательного обновления векторе синхронизации, которая ранее использовалась партнер по репликации, который указывает, что VDC2 элемента отката базы данных времени неправильно.

![Последовательность событий при обнаружении отката номера последовательного обновления](../media/Introduction-to-Active-Directory-Domain-Services--AD-DS--Virtualization--Level-100-/ADDS_Exampleofhowreplicationcanbecomeinconsistent.png)

Виртуальной машины (VM) облегчает администраторам гипервизора откат домена USN контроллера (его логических часов), например, применение моментального снимка за пределами информированности контроллера домена. Дополнительные сведения о номере последовательного обновления и его откате, включая другую иллюстрацию, демонстрирующую невыявленные экземпляры отката номера последовательного обновления, см. в разделе [Номер последовательного обновления и его откат](https://technet.microsoft.com/library/virtual_active_directory_domain_controller_virtualization_hyperv(WS.10).aspx#usn_and_usn_rollback).

Начиная с Windows Server 2012, контроллеры виртуального домена AD DS, размещенные на платформах гипервизоров, которые предоставляют идентификатор ИД создания виртуальной Машины могут определять и применять необходимые меры безопасности для защиты среды AD DS, если откат виртуальной машины назад во времени путем применения снимка виртуальной Машины. Структура ИД создания виртуальной машины использует независимый механизм поставщика гипервизора для предоставления этого идентификатора в пространстве адресов гостевой виртуальной машины, поэтому безопасная виртуализация обеспечивается любым гипервизором, который поддерживает ИД создания виртуальной машины. С помощью этого идентификатора службы и приложения, работающие на виртуальной машине, могут определить, выполнялся ли откат виртуальной машины.

## <a name="effects-of-usn-rollback"></a>Эффекты отката номера последовательного обновления

При возникновении откатов USN, изменения в объекты и атрибуты реплицируются не входящие конечные контроллеры домена, которые уже имеете представление USN.

Так как конечные контроллеры домена считаются обновленными, в актуальном состоянии, ошибки репликации не выводятся в журналах событий службы каталогов или с помощью средств диагностики и мониторинга.

Откат USN может затронуть репликацию любого объекта или атрибута в любом разделе. Наиболее часто наблюдаемая побочным эффектом является то, что учетные записи пользователей и учетные записи компьютеров, созданные на контроллере домена отката не существуют на один или несколько партнеров репликации. Или, что обновления паролей, изначально созданные на контроллере домена отката не существуют на партнеров репликации.

Откат USN может препятствовать репликации любого типа объекта в любом разделе Active Directory. Ниже приведены типы объектов:

* Топологии репликации Active Directory и расписание
* Существование контроллеров домена в лесу и ролей, которые содержат эти контроллеры домена
* Существование разделы домена и приложения в лесу
* Существование группы безопасности и их текущего членства в группах
* Регистрации записи DNS в зонах DNS, интегрированный с Active Directory

Размер отверстия USN может представлять сотен, тысяч или даже десятков тысяч изменений для пользователей, компьютеров, отношения доверия, паролей и групп безопасности. USN отверстия определяется разницу между наибольший номер последовательного обновления номер после изменений восстановленную резервную копию, а также количество исходящих изменений, созданные на контроллере домена откат, прежде чем она переводится в автономный режим.

## <a name="detecting-a-usn-rollback"></a>Обнаружение отката номера последовательного обновления

Поскольку трудно обнаружить откат USN, контроллер домена регистрирует событие 2095, когда исходный контроллер домена отправляет ранее подтвержденного номер USN для конечного контроллера домена без соответствующих изменений в ИД вызова.

Во избежание уникальный источника обновлений в Active Directory создаются на неправильно восстановленного контроллера домена, служба сетевого входа в систему будет приостановлено. Когда служба сетевого входа в систему приостановлена, учетные записи пользователей и компьютеров запрещено изменять пароль на контроллере домена, будет не исходящего трафика репликации таких изменений. Точно так же средств администрирования Active Directory будет гораздо удобнее работоспособный контроллер домена, когда они проводятся обновления в объектах в Active Directory.

На контроллере домена записываются сообщения о событиях, которые выглядеть следующим образом, если выполняются следующие условия:

* Исходный контроллер домена отправляет ранее подтвержденного номер USN для конечного контроллера домена.
* Нет соответствующих изменений в ИД вызова.

Эти события могут записываться в журнал событий службы каталогов. Тем не менее они могут быть перезаписаны, прежде чем они обнаруживаются администратором.

Если есть подозрение отката номера последовательного обновления возникла ошибка, но отсутствует соответствующее событие в случае проверьте журналы, для записи DSA не для записи в реестре. Эта запись содержит поддержки средства защиты судебных доказательств, что произошло отката номера последовательного обновления.

```
HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\NTDS\Parameters
Registry entry: Dsa Not Writable
Value: 0x4
```

> [!WARNING]
> Удаление или вручную изменить Dsa не для записи значение записи реестра помещает контроллер домена отката в состоянии без возможности восстановления не поддерживается. Таким образом такие изменения не поддерживаются. В частности изменив значение удаляет поведение карантина, добавленные код обнаружения отката номера последовательного обновления. Секции Active Directory на контроллере домена, откат будет окончательно согласована с партнерами репликации прямом и транзитивном в одном лесу Active Directory.

Дополнительные сведения об этом реестре ключ и инструкции по устранению можно найти в статье службы поддержки [Active Directory репликации ошибка 8456 или 8457: «Источник | конечный сервер в настоящий момент отвергает запросы на репликацию»](https://support.microsoft.com/help/2023007/active-directory-replication-error-8456-or-8457-the-source-destination).

## <a name="virtualization-based-safeguards"></a>Меры безопасности на основе виртуализации

Во время установки контроллера домена AD DS изначально сохраняют идентификатор ИД создания виртуальной Машины как часть атрибута msDS-GenerationID объекта-компьютера контроллера домена в своей базе данных (часто называют информационным деревом каталога, или DIT). ИД создания виртуальной машины независимо отслеживается драйвером Windows на виртуальной машине.

Когда администратор восстанавливает машину из предыдущего снимка, текущее значение ИД создания виртуальной машины от драйвера виртуальной машины сравнивается со значением в DIT.

Если значения отличаются, InvocationID сбрасывается, а пул относительного идентификатора отклоняется, чтобы предотвратить повторное использование номера последовательного обновления. Если значения совпадают, транзакция проводится в обычном режиме.

Службы AD DS также сравнивают текущее значение ИД создания виртуальной машины от виртуальной машины со значением в DIT при каждой перезагрузке контроллера домена. Если значения отличаются, службы сбрасывают InvocationID, отклоняют пул относительного идентификатора и записывают в DIT новое значение. Кроме того, службы синхронизируют папку SYSVOL недоверенным методом, чтобы завершить безопасное восстановление. Это позволяет мерам безопасности расширить применение снимков на отключенных виртуальных машинах. Эти меры безопасности, появившиеся в Windows Server 2012 Разрешить администраторам AD DS пользоваться уникальными преимуществами развертывания и управления контроллерами доменов в виртуализованной среде.

Ниже показано, как применяются меры безопасности виртуализации при обнаружении отката того же номера последовательного обновления на виртуализованном контроллере домена под управлением Windows Server 2012 на гипервизоре, поддерживающем ИД создания виртуальной Машины.

![Меры безопасности при обнаружении отката того же номера последовательного обновления](../media/Introduction-to-Active-Directory-Domain-Services--AD-DS--Virtualization--Level-100-/ADDS_VDC_Exampleofhowsafeguardswork.gif)

В этом случае, когда гипервизор обнаруживает изменение ИД создания виртуальной машины, срабатывают средства безопасности виртуализации, включая сброс кода обращения виртуализованного контроллера домена (с A на B в предыдущем примере) и обновление ИД создания виртуальной машины, сохраненного на виртуальной машине, для обеспечения соответствия новому значению (G2), которое хранит гипервизор. Меры безопасности обеспечивают выполнение репликации на обоих контроллерах доменов.

С Windows Server 2012 AD DS применяют меры безопасности на контроллерах домена, размещенных на виртуальной Машине гипервизорах и гарантирует, что случайном применении снимков или других гипервизором механизмов, которые удалось откат виртуальной состояние компьютера не нарушит среды AD DS (путем предотвращения проблем репликации, таких как номера последовательного обновления или замедление объектов).

Восстановление контроллера домена путем применения моментального снимка виртуальной машины в качестве альтернативного механизма архивации контроллера домена не рекомендуется. Мы рекомендуем и дальше использовать систему архивации данных Windows Server или другие решения для архивации на базе устройств записи VSS.

> [!CAUTION]
> Если контроллер домена в рабочей среде был случайно восстановлен до моментального снимка, рекомендуется проконсультироваться с поставщиками для приложений и служб, размещенных на этой виртуальной машине, рекомендации по проверке состояния этих программ после восстановление моментального снимка.

Дополнительные сведения см. в разделе [Virtualized domain controller safe restore architecture](../ad-ds/get-started/virtual-dc/Virtualized-Domain-Controller-Architecture.md#BKMK_SafeRestoreArch).

## <a name="recovering-from-a-usn-rollback"></a>Восстановление после отката номера последовательного обновления

Существует два подхода к восстановлению после отката номера последовательного обновления:

* Удалить контроллер домена из домена
* Восстановление состояния системы из действительной резервной копии

### <a name="remove-the-domain-controller-from-the-domain"></a>Удалить контроллер домена из домена

1. Удалите Active Directory с контроллера домена, принудительно автономным сервером.
2. Завершите работу сервера с пониженной ролью.
3. На работоспособном контроллере домена очистите метаданные контроллера домена с пониженной ролью.
4. Если неверно восстановленном домена контроллера размещены роли хозяина операций, переместите эти роли на работоспособный контроллер домена.
5. Перезапустите сервер с пониженной ролью.
6. Если необходимо, установите Active Directory на изолированном сервере еще раз.
7. Если контроллер домена раньше был глобальным каталогом, настройте контроллер домена как глобальный каталог.
8. Если в контроллере домена раньше размещались роли хозяина операций, переместите их обратно к контроллеру домена.

### <a name="restore-the-system-state-of-a-good-backup"></a>Восстановление состояния системы из действительной резервной копии

Оцените наличие резервных копий состояния системы, допустимый для данного контроллера домена. Если резервной копии состояния системы допустимым была создана до неправильного восстановления контроллера домена откат, и резервная копия содержит последние изменения, внесенные на контроллере домена, восстановите состояние системы из последней резервной копии.

Моментальный снимок также можно использовать как источник из резервной копии. Или можно задать базе данных выдачу нового идентификатора вызова с помощью процедуры в разделе [восстановление виртуального контроллера домена, если соответствующие данные резервном копировании состояния не доступна](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd363553%28v%3dws.10%29#restoring-a-virtual-domain-controller-when-an-appropriate-system-state-data-backup-is-not-available)

## <a name="next-steps"></a>Следующие шаги

* Дополнительные сведения о диагностике виртуализованных контроллеров доменов см. в разделе [Диагностика виртуализованных контроллеров доменов](../ad-ds/manage/virtual-dc/Virtualized-Domain-Controller-Troubleshooting.md).
* [Подробные сведения о служба времени Windows (W32Time)](../../networking/windows-time-service/windows-time-service-top.md)