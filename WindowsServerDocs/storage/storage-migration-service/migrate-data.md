---
title: Перенос файлового сервера с помощью службы миграции хранилища
description: Краткое описание раздела по результатах поисковой системы
author: jasongerend
ms.author: jgerend
manager: elizapo
ms.date: 02/13/2019
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: storage
ms.openlocfilehash: 879a87d4383d07e37227ecf6fffa5d002a77bbc0
ms.sourcegitcommit: 214e827934e7b3e8987e9e0ab2cf00047d332c89
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/17/2019
ms.locfileid: "67153319"
---
# <a name="use-storage-migration-service-to-migrate-a-server"></a>Использование службы хранилища миграции для переноса сервера

В этом разделе рассматривается миграция сервера, включая файлы и конфигурации, на другой сервер с помощью [миграции службы хранилища](overview.md) и Windows Admin Center. Перенос состоит из трех шагов после установки службы и открыть все необходимые порты брандмауэра: инвентаризации ваших серверов, передачи данных и перехода на новые серверы.

## <a name="step-0-install-storage-migration-service-and-check-firewall-ports"></a>Шаг 0. Установите службу миграции хранилища и проверить порты брандмауэра

Прежде чем приступить к работе, установите службу миграции хранилища и убедитесь, что необходимые порты брандмауэра открыты.

1. Проверьте [требования к службе хранилища миграции](overview.md#requirements) и установить [Windows Admin Center](../../manage/windows-admin-center/understand/windows-admin-center.md) на ПК или сервер управления, если у вас еще нет.
2. В Windows Admin Center подключитесь к серверу orchestrator с ОС Windows Server 2019. <br>Это сервер, который вы установите службу миграции хранилища на и использовать для управления миграцией. Если вы переносите только один сервер, можно использовать целевой сервер до тех пор, пока она запущена Windows Server 2019. Мы рекомендуем использовать сервер отдельные оркестрации для все миграции нескольких серверов.
1. Перейдите к **диспетчера серверов** (в Windows Admin Center) > **миграции службы хранилища** и выберите **установить** для установки службы миграции хранилища и его необходимых компонентов (показано на рис. 1).
    ![Снимок экрана страницы миграции службы хранилища, показывающий кнопку "установить"](media/migrate/install.png) **рис. 1: Установка службы миграции хранилища**
1. Установите прокси-службы миграции хранилища на всех конечных серверов под управлением Windows Server 2019. Это удваивает скорость передачи, при установке на конечных серверах. <br>Для этого нужно подключиться к серверу назначения в Windows Admin Center и перейдите к **диспетчера серверов** (в Windows Admin Center) > **роли и компоненты**выберите **миграции службы хранилища Прокси-сервера**, а затем выберите **установить**.
1. На всех серверах источника и на все целевые серверы под управлением Windows Server 2012 R2 или Windows Server 2016 в Windows Admin Center, подключитесь к каждому серверу, посетите **диспетчера серверов** (в Windows Admin Center) > **брандмауэра**   >  **Входящего правила**и проверьте, что включены следующие правила:
    - Общий доступ к файлам и принтерам (входящий трафик SMB)
    - Служба Netlogon (именованные каналы — входящий трафик)
    - Инструментарий управления Windows (DCOM-In)
    - Инструментарий управления Windows (WMI-In)

   > [!NOTE]
   > Если вы используете сторонние брандмауэры, диапазонов портов для входящего трафика для открытия, TCP/445 (SMB), TCP/135 (Сопоставитель конечных точек RPC/DCOM) и TCP 1025-65535 (временные порты RPC/DCOM). Порты службы миграции хранилища, TCP/28940 (Orchestrator) и TCP/28941 (прокси).

1. Если вы используете сервер orchestrator для управления миграцией, и вы хотите загрузить события или журнала при передаче данных, к файлам и принтерам (SMB — входящий) правило проверьте, включено ли на этом сервере, а также.

## <a name="step-1-create-a-job-and-inventory-your-servers-to-figure-out-what-to-migrate"></a>Шаг 1. Создание задания и инвентаризации ваших серверов, чтобы понять, что для переноса

На этом шаге укажите какие серверы для переноса и затем проверить их, чтобы собирать сведения в свои файлы и конфигурации.

1. Выберите **новое задание**, назовите задание, а затем выберите **ОК**.
1. На **введите учетные данные** введите учетные данные администратора, которые работают на серверах, которые требуется перенести из, а затем выберите **Далее**.
1. Выберите **добавить устройство**, введите имя сервера источника и выберите **ОК**. <br>Повторите эти действия для других серверов, которые необходимо добавить в инвентаризацию.
1. Выберите **Start scan**.<br>Страницы обновляется показывает, когда сканирование будет закончено.
    ![Снимок экрана, показывающий сервере все готово для сканирования](media/migrate/inventory.png) **рис. 2: Инвентаризация серверов**
1. Выберите для просмотра общих папок, конфигурации и сетевых адаптеров, а также томов, учтенных каждого сервера. <br><br>Служба миграции хранилища не передачи файлов или папок, мы знаем, что может помешать выполнению операции Windows, поэтому в этом выпуске вы увидите предупреждения для любых общих ресурсов, расположенных в папке системы Windows. Вам придется пропустить эти общие папки на этапе передачи. Дополнительные сведения см. в разделе [какие файлы и папки исключаются из передачи](faq.md#excluded-files).
1. Выберите **Далее** для перехода к передаче данных.

## <a name="step-2-transfer-data-from-your-old-servers-to-the-destination-servers"></a>Шаг 2. Переносить данные из старых серверов на целевых серверах

На этом этапе передачи данных, после указания, куда поместить его на конечных серверах.

1. На **передачи данных** > **введите учетные данные** введите учетные данные администратора, которые работают на конечных серверах, необходимо выполнить перенос, а затем выберите **Далее**.
2. На **добавить устройства назначения и сопоставления** страница «получение», первый исходный сервер. Введите имя сервера, к которому вы хотите перенести, а затем выберите **проверять устройство на**.
3. Очистить сопоставления исходных томов для томов конечного **Include** флажок для любых общих ресурсов не требуется передавать (включая любые административные общие ресурсы, расположенные в папке системы Windows), а затем выберите **Далее** .
   ![Снимок экрана с исходного сервера и его томов и общих папок и где они будут передаваться в месте назначения](media/migrate/transfer.png) **рис. 3: Исходный сервер и где его хранилища будут передаваться**
4. Добавить конечный сервер и сопоставления для любых дополнительных серверов источника, а затем выберите **Далее**.
5. При необходимости настройте параметры передачи, а затем выберите **Далее**.
6. Выберите **Validate** , а затем выберите **Далее**.
7. Выберите **начать перенос** чтобы начать операцию передачи данных.<br>При первом переносе, мы перейдем существующие файлы в место назначения в папку резервных копий. На последующих передачи по умолчанию будет обновить назначения без создания его резервной копии первого. <br>Кроме того, службы миграции хранилища может иметь дело с перекрывающимися общие папки, мы не копирует тех же папках, дважды в одном задании.
8. После завершения передачи, ознакомьтесь с целевом сервере, чтобы убедиться, что все, что передано надлежащим образом. Выберите **только журнал ошибок** Если вы хотите скачать журнал файлов, которые не были переданы.

   > [!NOTE]
   > Если вы хотите отслеживать передачи или планируете использовать более одного передачу задания, нажмите кнопку **журнале переноса** для сохранения копии CSV. Каждый последующий передачи перезаписывает сведения о базе данных из предыдущего выполнения. 

На этом этапе у вас есть три варианта:

- **Перейдите к следующему шагу**, на переднем над таким образом, чтобы конечные серверы внедрять удостоверения исходных серверов.
- **Рассмотрите возможность миграции полный** без перевода над удостоверениями исходных серверов.
- **Повторной передачи**, копирование только те файлы, которые были обновлены с момента последней передачи.

Если ваша цель — для синхронизации файлов с помощью Azure, можно настроить конечные серверы с помощью службы синхронизации файлов Azure после передачи файлов или вырезания по на конечных серверах (см. в разделе [Планирование развертывания службы синхронизации файлов Azure](https://docs.microsoft.com/azure/storage/files/storage-sync-files-planning)).

## <a name="step-3-optionally-cut-over-to-the-new-servers"></a>Шаг 3. При необходимости перехода на новые серверы

На этом шаге вы переход с исходных серверов на конечные серверы, переход на сервере назначения IP-адреса и имена компьютеров. После завершения этого шага, приложений и пользователей получить доступ к через имена и адреса серверов, переносимого из новых серверов.

 1. Если вы перешли от задания миграции, в Windows Admin Center, перейдите к **диспетчера серверов** > **миграции службы хранилища** и выберите задание, для которого необходимо завершить. 
 1. На **перехода на новые серверы** > **введите учетные данные** выберите **Далее** использовать учетные данные, которые вы ввели ранее.
 1. На **Настройка прямой** укажите, какие сетевые адаптеры, чтобы перехватить параметры каждого исходного устройства. Это перемещает IP-адрес из источника в место назначения в процессе миграции.
 1. Укажите, какие IP-адрес для исходного сервера после прямой переход его адрес в место назначения. Можно использовать DHCP или статический адрес. Если используется статический адрес, новой подсети должен быть как старую подсеть или прямая миграция завершится ошибкой.
    ![Снимок экрана с исходного сервера и IP-адреса и имена компьютеров и что они будут заменены после миграции.](media/migrate/cutover.png)
    **рис. 4: Исходный сервер и способ его сетевая конфигурация перемещения в место назначения**
 1. Укажите, как переименование исходного сервера после целевой сервер имеет над его имя. Можно использовать случайным образом созданное имя или ввести его вручную. Затем выберите **Далее**.
 1. Выберите **Далее** на **прямой настройки** страницы.
 1. Выберите **Validate** на **проверить источник и назначение устройств** странице, а затем выберите **Далее**.
 1. Когда вы будете готовы выполнить прямую миграцию, выберите **запустить прямую миграцию**. <br>Пользователи и приложения могут возникнуть прерывания, время перемещаются адреса и имена серверов возобновлена несколько раз, каждый, но в противном случае будут затронуты процедурой миграции. Как долго перехода зависит от насколько быстро перезагрузить серверы, а также время репликации Active Directory и DNS.

## <a name="see-also"></a>См. также

- [Общие сведения о миграции службы хранилища](overview.md)
- [Часто задаваемые вопросы (FAQ) службы миграции хранилища](faq.md)
- [Планирование развертывания службы синхронизации файлов Azure](https://docs.microsoft.com/azure/storage/files/storage-sync-files-planning)