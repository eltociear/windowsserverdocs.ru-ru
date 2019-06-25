---
title: Создание отчетов по использованию на основе зарегистрированных ранее данных для удаленных клиентов
description: Этот раздел является частью руководства для удаленного мониторинга доступа и учета в Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0305467b-ce39-4532-a05a-2cc5ff946f55
ms.author: pashort
author: shortpatti
ms.openlocfilehash: cfbac18f64123f97c54b29c1aeef7364af55e49a
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/20/2019
ms.locfileid: "67281131"
---
# <a name="generate-a-usage-report-for-remote-clients-using-historical-data"></a>Создание отчетов по использованию на основе зарегистрированных ранее данных для удаленных клиентов

>Область применения. Windows Server (полугодовой канал), Windows Server 2016

**Примечание.** Windows Server 2012 объединяет DirectAccess и службы маршрутизации и удаленного доступа (RRAS) в единую роль удаленного доступа.  
  
Консоль управления на сервере удаленного доступа можно использовать для создания отчета об использовании для удаленных клиентов, которые обращаются к серверу. Чтобы создать отчет об использовании для удаленных клиентов, сначала включить учета на сервере удаленного доступа. После создания отчета, можно использовать панель мониторинга, которая доступна в консоли управления на сервере удаленного доступа для просмотра статистики нагрузки на сервере.  
  
> [!NOTE]  
> Вы должны быть подписаны качестве члена группы "Администраторы домена" или быть членом группы администраторов на каждом компьютере для выполнения задач, описанных в этом разделе. Если не удается завершить задачу, пока вы выполняете вход с использованием учетной записи, которая является членом группы "Администраторы", попробуйте, выполняя задачи, когда вы выполняете вход с использованием учетной записи, которая является членом группы "Администраторы домена".  
  
#### <a name="to-enable-accounting-on-the-remote-access-server"></a>Включение учета на сервере удаленного доступа  
  
1.  В **диспетчере серверов** щелкните **Средства** и выберите пункт **Управление удаленным доступом**.  
  
2.  Нажмите кнопку **ОТЧЕТОВ** для перехода к **удаленного доступа Reporting** в **консоли управления удаленным доступом**.  
  
3.  Нажмите кнопку **Настройка учета** в **удаленного доступа Reporting** области задач.  
  
4.  Выберите **использовать учет** флажок для включения учета на сервере удаленного доступа.  
  
5.  Нажмите кнопку **применить** включить конфигурацию учета на сервере, а затем нажмите кнопку **закрыть** сервера после установки конфигурации успешно.  
  
#### <a name="to-generate-the-usage-report"></a>Чтобы создать отчет об использовании  
  
1.  В **диспетчере серверов** щелкните **Средства** и выберите пункт **Управление удаленным доступом**.  
  
2.  Нажмите кнопку **ОТЧЕТОВ** для перехода к **удаленного доступа Reporting** в **консоли управления удаленным доступом**.  
  
3.  В средней области выберите даты календаря для выбора периода времени **Дата начала:** и **Дата окончания:** , а затем нажмите кнопку **Создание отчета**.  
  
4.  Вы увидите список пользователей, подключенных к серверу удаленного доступа в выбранный период времени и подробную статистику о них. Щелкните первую строку в списке. При выборе строки активности удаленных пользователей отображается в области предварительного просмотра. Теперь выберите **статистику загрузки сервера** вкладки в области просмотра, чтобы увидеть значительной загрузки на сервере.  
  
    Нажмите кнопку **статистику загрузки сервера** вкладки в области просмотра, чтобы увидеть значительной загрузки на сервере.  
  
> [!NOTE]  
> **Основные сведения о сеансах**  
>   
> Учет удаленного доступа основана на концепции **сеансы**. В отличие от к **подключения**, **сеанса** однозначно идентифицируется с помощью сочетания имени пользователя и адреса IP-адрес удаленного клиента. Например если машинный туннель формируется из удаленного клиента, с именем Client1, сеанс будет создан и хранящиеся в базе данных учета. Когда передает пользователя именованный пользователь User1 подключается из этого клиента через некоторое время (но машинном туннеле по-прежнему активна), сеанс регистрируется как отдельный сеанс. Различие сеансов является сохранение различие между машинный туннель и туннель пользователя.  
  
![Windows PowerShell](../../../media/Generate-a-usage-report-for-remote-clients-using-historical-data/PowerShellLogoSmall.gif)***<em>эквивалентные команды Windows PowerShell</em>***  
  
Следующие командлеты Windows PowerShell выполняют ту же функцию, что и предыдущая процедура. Вводите каждый командлет в одной строке, несмотря на то, что здесь они могут отображаться разбитыми на несколько строк из-за ограничений форматирования.  
  
В следующем сценарии, изменить диапазон дат, для которого необходимо создать отчет в **- StartDateTime** и **- EndDateTime** параметров.  
  
```  
PS> Get-RemoteAccessConnectionStatisticsSummary -StartDateTime "1 October 2010 00:00:00" -EndDateTime "14 October 2010 00:00:00"  
Shows server load statistics.  
PS> Get-RemoteAccessUserActivity -HostIPAddress 10.0.0.1 -StartDateTime "1 October 2010 00:00:00" -EndDateTime "14 October 2010 00:00:00"  
```  
  

