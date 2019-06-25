---
title: Выполнение задач после миграции для Windows Server Essentials migration1
description: Описывает способ использования Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f2d236a4-0d62-4961-9d1f-332054e06f6d
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 93d07938435ab1ce7686b1960974696582a2924c
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/31/2019
ms.locfileid: "66432660"
---
# <a name="perform-post-migration-tasks-for-windows-server-essentials-migration1"></a>Выполнение задач после миграции для Windows Server Essentials migration1

>Область применения. Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Следующие задачи помогут вам завершить настройку конечного сервера с теми же параметрами, которые были на исходном сервере. Возможно, вы отключили некоторые из этих параметров на исходном сервере во время процесса миграции, поэтому они не были перенесены на конечный сервер. Либо они относятся к необязательным операциям, которые требуется выполнить.  
  

-   [Удаление DNS-записей исходного сервера](Perform-post-migration-tasks-for-Windows-Server-Essentials-migration.md#BKMK_DeleteDNSEntries)  
  
-   [Совместное использование бизнес- и другим папкам данных приложения](Perform-post-migration-tasks-for-Windows-Server-Essentials-migration.md#BKMK_ShareLineOfBusinessAndOtherApplications)  
  
-   [Исправление проблем с компьютером клиента после переноса](Perform-post-migration-tasks-for-Windows-Server-Essentials-migration.md#BKMK_FixClientComputerIssuesAfterMigrating)  
  
-   [Предоставить право на вход в качестве пакетного задания встроенной группе администраторов](Perform-post-migration-tasks-for-Windows-Server-Essentials-migration.md#BKMK_AdminGroup)  

-   [Удаление DNS-записей исходного сервера](../migrate/Perform-post-migration-tasks-for-Windows-Server-Essentials-migration.md#BKMK_DeleteDNSEntries)  
  
-   [Совместное использование бизнес- и другим папкам данных приложения](../migrate/Perform-post-migration-tasks-for-Windows-Server-Essentials-migration.md#BKMK_ShareLineOfBusinessAndOtherApplications)  
  
-   [Исправление проблем с компьютером клиента после переноса](../migrate/Perform-post-migration-tasks-for-Windows-Server-Essentials-migration.md#BKMK_FixClientComputerIssuesAfterMigrating)  
  
-   [Предоставить право на вход в качестве пакетного задания встроенной группе администраторов](../migrate/Perform-post-migration-tasks-for-Windows-Server-Essentials-migration.md#BKMK_AdminGroup)  

  
##  <a name="BKMK_DeleteDNSEntries"></a> Удаление DNS-записей исходного сервера  
 После списания исходного сервера, сервера сервер службы доменных имен (DNS) может все еще содержать элементы, указывающие на этот исходный сервер. Удалите эти записи DNS.  
  
#### <a name="to-delete-dns-entries-that-point-to-the-source-server"></a>Чтобы удалить DNS-записи, которые ссылаются на исходный сервер  
  
1.  Откройте **Диспетчер DNS**на конечном сервере .  
  
2.  В диспетчере DNS щелкните правой кнопкой мыши имя сервера, щелкните **Свойства**, а затем перейдите на вкладку **Серверы пересылки** .  
  
3.  Определите, имеется ли в списке пересылок запись, указывающая на исходный сервер. Если такая запись есть, нажмите кнопку **Изменить** и удалите эту запись в окне **Редактировать серверы пересылки**.  
  
4.  В окне **Диспетчер DNS** разверните имя сервера и затем разверните пункт **Зоны прямого просмотра**.  
  
5.  Для каждой зоны прямого просмотра щелкните правой кнопкой мыши зону, выберите пункт **Свойства**, а затем откройте вкладку **Серверы имен**.  
  
6.  Щелкните запись в поле **Серверы имен**, которая указывает на исходный сервер, нажмите **Удалить**, а затем нажмите **ОК**.  
  
7.  Повторите шаги 5 и 6, пока не будут удалены все указатели на исходный сервер.  
  
8.  Нажмите кнопку **ОК**, чтобы закрыть окно **Свойства**.  
  
9. В консоли**Диспетчер DNS** разверните **Зоны обратного просмотра**.  
  
10. Повторите шаги 6–9, чтобы удалить все зоны обратного просмотра, которые указывают на исходный сервер.  
  
##  <a name="BKMK_ShareLineOfBusinessAndOtherApplications"></a> Совместное использование бизнес- и другим папкам данных приложения  
 Для скопированных на конечный сервер папок с данными бизнес-приложений и прочих приложений необходимо задать разрешения для общей папки и разрешения NTFS. После настройки разрешений общие папки отображаются в панели мониторинга Windows Server Essentials в **хранения** раздел.  
  
 Если для сопоставления дисков с общими папками вы используете сценарий входа, для сопоставления с дисками на конечном сервере сценарий необходимо обновить.  
  
##  <a name="BKMK_FixClientComputerIssuesAfterMigrating"></a> Исправление проблем с компьютером клиента после переноса  
 При миграции на Windows Server Essentials из Windows Small Business Server 2003 Premium Edition с Microsoft Internet Security и Acceleration (ISA) Server установлена, клиентские компьютеры в сети по-прежнему имеют клиент брандмауэра Microsoft и Интернета Обозреватель настроен на использование прокси-сервер.  
  
 Это приводит к проблемам со связью на клиентских компьютерах, так как прокси-сервер больше не существует. Если имеется другой прокси-сервером, на клиентских компьютерах продолжать использовать сервер под управлением Windows SBS 2003 для прокси-сервера. Для устранения этой проблемы необходимо перенастроить Internet Explorer, чтобы он не использовал прокси-сервер или использовал новый прокси-сервер.  
  
#### <a name="to-reconfigure-internet-explorer"></a>Перенастройка Internet Explorer  
  
1.  В Internet Explorer щелкните **Сервис**и выберите **Свойства обозревателя**.  
  
2.  Перейдите на вкладку **Подключения**, затем **Параметры сети** и выполните одно из следующих действий:  
  
    -   Если вы не используете прокси-сервер в своей сети, снимите все флажки в диалоговом окне **Параметры локальной сети (LAN)** .  
  
    -   Если вы хотите использовать новый прокси-сервер в своей сети:  
  
        1.  В диалоговом окне **Параметры локальной сети (LAN)** снимите флажки в разделе **Автоматическая настройка**.  
  
        2.  В разделе **Прокси-сервер** убедитесь, что установлены оба флажка.  
  
        3.  В поле **Адрес** введите полное доменное имя (FQDN) прокси-сервера.  
  
        4.  В поле **Порт** введите **80**.  
  
3.  Щелкните дважды **ОК** .  
  
4.  Перейдите на веб-сайт и убедитесь в правильности параметров подключения.  
  
##  <a name="BKMK_AdminGroup"></a> Предоставить право на вход в качестве пакетного задания встроенной группе администраторов  
 После миграции существующего домена Windows Small Business Server 2003 на Windows Server Essentials, встроенной группе администраторов следует предоставить право на вход в качестве пакетного задания. Убедитесь, что встроенная группа администраторов по-прежнему имеет право на вход в качестве пакетного задания на целевой сервер. Администраторам требуется это разрешение для запуска оповещения на целевом сервере без входа в систему.  
  
#### <a name="to-give-the-built-in-administrators-group-the-right-to-log-on-as-a-batch-job"></a>Предоставление права на вход в качестве пакетного задания встроенной группе администраторов  
  
1. На конечном сервере откройте средство администрирования **Управление групповой политикой**.  
  
2. В **Управление групповой политикой** дереве консоли, разверните узел **леса:** *< ServerName\>* , разверните домены, а затем разверните свой сервер.  
  
3. Разверните **Контроллеры домена**, щелкните правой кнопкой мыши **Политика контроллеров домена по умолчанию**, а затем нажмите **Изменить**.  
  
4. В **редактор управления групповыми политиками**, нажмите кнопку **политика контроллеров домена по умолчанию**<em>< ServerName\></em>**политики**, а затем разверните **Конфигурация компьютера**.  
  
5. Разверните **Политики**, разверните **Параметры Windows**, а затем разверните **Параметры безопасности**.  
  
6. В дереве **Параметры безопасности** разверните **Локальные политики**, а затем щелкните **Назначение прав пользователя**.  
  
7. На панели результатов щелкните правой кнопкой мыши **Вход в качестве пакетного задания**, а затем нажмите кнопку Свойства.  
  
8. На странице **Вход в качестве пакетного задания свойства** щелкните **Добавить пользователя или группу**.  
  
9. В диалоговом окне **Добавить пользователя или группу** щелкните **Обзор**.  
  
10. В диалоговом окне **Выбор: пользователи, компьютеры или группы** введите **Administrators**.  
  
11. Щелкните **Проверить имена**, чтобы убедиться, что появляется встроенная группа администраторов, и нажмите три раза кнопку **ОК** для сохранения параметра.  
  
## <a name="see-also"></a>См. также  
  

-   [Миграция с Windows SBS 2003](Migrate-Windows-Small-Business-Server-2003-to-Windows-Server-Essentials.md)  
  
-   [Перенос данных сервера в Windows Server Essentials](Migrate-Server-Data-to-Windows-Server-Essentials.md)

-   [Миграция с Windows SBS 2003](../migrate/Migrate-Windows-Small-Business-Server-2003-to-Windows-Server-Essentials.md)  
  
-   [Перенос данных сервера в Windows Server Essentials](../migrate/Migrate-Server-Data-to-Windows-Server-Essentials.md)
