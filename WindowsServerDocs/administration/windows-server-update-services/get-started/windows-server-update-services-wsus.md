---
title: Начало работы со службами обновления Windows Server (WSUS)
description: Статья о службах обновления Windows Server (WSUS) с описанием роли сервера и ее применения на практике
ms.prod: windows-server
ms.technology: manage-wsus
ms.topic: get-started article
ms.assetid: 90e3464c-49d8-4861-96db-ee6f8a09ec5b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 5/22/2017
ms.openlocfilehash: 3bb365c627840d4152b0dc450e24dd83d82103ca
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2020
ms.locfileid: "80828637"
---
# <a name="windows-server-update-services-wsus"></a>Службы Windows Server Update Services (WSUS)

>Область применения. Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Службы Windows Server Update Services (WSUS) позволяют ИТ-администраторам развертывать новейшие обновления продуктов Майкрософт. Службы WSUS позволяют в полной мере управлять процессом распределения обновлений, выпущенных через Центр обновления Майкрософт, среди компьютеров в сети. В данном разделе представлен обзор этой роли сервера и дополнительные сведения о том, как развертывать и обслуживать WSUS.

## <a name="wsus-server-role-description"></a>Описание роли сервера WSUS
Сервер WSUS предоставляет возможности для управления обновлениями и их распространения через консоль управления. Сервер служб WSUS может также быть источником обновлений для других серверов WSUS в организации. Сервер WSUS, действующий как источник обновлений, называется вышестоящим сервером. В реализации служб WSUS хотя бы один сервер WSUS в сети должен иметь возможность подключаться к Центру обновления Майкрософт для получения информации о доступных обновлениях. Учитывая вопросы безопасности и конфигурации сети, администратор может самостоятельно определить количество дополнительных серверов, напрямую подключенных к Центру обновления Майкрософт.

### <a name="practical-applications"></a>Практическое применение
Управление обновлениями — это процесс управления развертыванием и обслуживанием промежуточных выпусков программного обеспечения в рабочей среде. Это помогает поддерживать производительность, преодолевать уязвимости и обеспечивать стабильность рабочей среды. Если организация не может устанавливать и поддерживать известный уровень доверия в своих операционных системах и прикладном программном обеспечении, то у нее может появиться ряд уязвимостей, что в случае взлома способно привести к потере дохода и интеллектуальной собственности. Чтобы минимизировать данную угрозу, необходимо правильно настроить системы, использовать последние версии программного обеспечения и установить рекомендуемые обновления ПО.

Основными сценариями, в которых WSUS повышает эффективность вашего бизнеса, являются:

-   Централизованное управление обновлениями

-   Автоматизация управления обновлениями

### <a name="new-and-changed-functionality"></a>Новые и измененные функции

> [!NOTE]
> Обновление с любой версии Windows Server, поддерживающей WSUS 3.2, до Windows Server 2012 R2 требует предварительного удаления WSUS 3.2.
> 
> В Windows Server 2012 обновление с любой версии Windows Server с установленными службами WSUS 3.2 блокируется в процессе установки, если будет обнаружена служба WSUS 3.2. В этом случае вам будет предложено сначала удалить службы обновления Windows Server, а затем повторно обновить сервер.
> 
> Но после изменений, внесенных в текущем выпуске Windows Server и Windows Server 2012 R2, установка не блокируется при обновлении с любой версии Windows Server и WSUS 3.2. Если перед выполнением обновления Windows Server или Windows Server 2012 R2 не будут удалены службы WSUS 3.2, то задачи WSUS после установки будут завершаться ошибкой. Известен только один метод решения такой проблемы — отформатировать жесткий диск и повторно установить Windows Server.

Службы Windows Server Update Services представляют собой встроенную роль сервера со следующими дополнительными возможностями.

-   Может быть добавлена и удалена с помощью диспетчера серверов

-   Включает командлеты Windows PowerShell для управления наиболее важными задачами администрирования в службах WSUS

-   Добавляет возможность использования хэширования SHA256 для дополнительной безопасности

-   Обеспечивает разделение клиента и сервера, благодаря чему версии агента Центра обновления Windows (WUA) могут поставляться независимо от WSUS

### <a name="using-windows-powershell-to-manage-wsus"></a>Использование Windows PowerShell для управления WSUS
Системным администраторам для автоматизации работы необходим охват с помощью автоматизации командной строки. Основной целью является облегчение администрирования WSUS, позволяя системным администраторам автоматизировать их ежедневный труд.

**Какой эффект дает это изменение?**

Пропуская основные операции WSUS через Windows PowerShell, системные администраторы могут увеличить продуктивность, уменьшить время на изучение новых инструментов, а также снизить количество ошибок из-за неоправданных ожиданий, ставших результатом отсутствия согласованности простых операций.

**Что работает иначе?**

В более ранних версиях операционной системы Windows Server отсутствовали командлеты Windows PowerShell, а автоматизация управления обновлениями была затруднительным делом. Командлеты Windows PowerShell для операций WSUS дают дополнительную гибкость и быстроту системному администратору.

## <a name="in-this-collection"></a>Содержание коллекции
В эту коллекцию включены следующие руководства по планированию, развертыванию и администрированию служб WSUS.

-   [Развертывание служб Windows Server Update Services](../deploy/deploy-windows-server-update-services.md)

-   [Управление обновлениями с помощью служб Windows Server Update Services](../manage/update-management-with-windows-server-update-services.md)


