---
title: Очистка метаданных сервера AD DS
description: Используйте встроенные средства для очистки метаданных из удаленных контроллеров домена
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 11/14/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: fbb6e720c9289c608d71d3c36695ba623a9df5f6
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2019
ms.locfileid: "59818085"
---
# <a name="clean-up-active-directory-domain-controller-server-metadata"></a>Очистка метаданных сервера контроллера домена Active Directory

Область применения. Windows Server

Очистка метаданных не является процедурой требуется после принудительного удаления доменных служб Active Directory (AD DS). Выполнить очистку метаданных на контроллере домена в домене контроллер домена, принудительно удалены. Очистка метаданных удаляет данные из AD DS, определяющий контроллер домена в системе репликации. Очистка метаданных также удаляет подключений службы репликации файлов (FRS) и репликации распределенной файловой системы (DFS) и пытается переноса или изменения размера любого (известные также как гибкие операции с единым хозяином или FSMO) роли, удалено домену контроллер содержит.

Существует три варианта Очистка метаданных сервера:

- Очистка метаданных сервера с помощью средства графического интерфейса пользователя
- Очистка метаданных сервера, с помощью командной строки
- Очистка метаданных сервера с помощью скрипта

> [!NOTE]
> Если появляется ошибка «Доступ запрещен» при использовании любого из этих методов для выполнить очистку метаданных, убедитесь, что объект-компьютер и объекте параметров NTDS для контроллера домена не защищены от случайного удаления. Чтобы проверить этот щелкните правой кнопкой мыши объект-компьютер или объект параметров NTDS, щелкните **свойства**, нажмите кнопку **объект**и снимите **защитить объект от случайного удаления** флажок. В Active Directory — пользователи и компьютеры **объект** появится вкладка объекта, если щелкнуть **представление** и нажмите кнопку **дополнительные функции**.

## <a name="clean-up-server-metadata-using-gui-tools"></a>Очистка метаданных сервера, с помощью средства графического интерфейса пользователя

При использовании средств удаленного администрирования сервера (RSAT) или Active Directory — пользователи и компьютеры консоли (Dsa.msc), который входит в состав Windows Server для удаления учетной записи компьютера контроллера домена из подразделения (OU), контроллеры домена Очистка метаданных сервера выполняется автоматически. До Windows Server 2008 нужно было выполнять процедуру очистки отдельные метаданные.

Можно также использовать Active Directory — сайты и службы консоли (Dssite.msc), чтобы удалить учетную запись компьютера контроллера домена, которая также автоматически выполняет очистку метаданных. Тем не менее Active Directory — сайты и службы удаляет метаданные автоматически только в том случае, если сначала удалить объект параметров NTDS ниже учетной записи компьютера в Dssite.msc.

До тех пор, пока вы используете Windows Server 2008 или более новые версии RSAT Dsa.msc или Dssite.msc, можно выполнить очистку метаданных, автоматически для контроллеров домена под управлением более ранних версиях операционных систем Windows.

Членство в группе **"Администраторы домена"**, или эквивалентной является минимальным требованием для выполнения этих процедур.

## <a name="clean-up-server-metadata-using-activedirectory-users-and-computers"></a>Очистка метаданных сервера, с помощью Active Directory — пользователи и компьютеры

1. Откройте оснастку **Пользователи и компьютеры Active Directory**.
2. Если вы определили партнеров репликации в процессе подготовки для выполнения этой процедуры и если вы не подключены к партнеру репликации контроллера домена, удаленные, метаданные которого тонких, щелкните правой кнопкой мыши **Active Directory — пользователи и Компьютеры** узел, а затем щелкните **Сменить контроллер домена**. Щелкните имя контроллера домена, из которого вы хотите удалить метаданные, а затем нажмите кнопку **ОК**.
3. Разверните узлы домена контроллера домена, принудительно был удален и нажмите кнопку **контроллеры домена**.
4. В области сведений щелкните правой кнопкой мыши объекта-компьютера контроллера домена, метаданные которого требуется очистить и нажмите кнопку **удалить**.
5. В **доменных служб Active Directory** диалоговом окне отображается имя контроллера домена, которую требуется удалить и нажмите кнопку **Да** для подтверждения удаления объекта компьютера.
6. В **удаление контроллера домена** выберите **этот контроллер домена без возможности восстановления вне сети и больше не может быть понижена с помощью Active Directory домена службы установки мастер (DCPROMO)**, а затем нажмите кнопку **удалить**.
7. Если контроллер домена является сервером глобального каталога в **удалить контроллер домена** диалоговом окне щелкните **Да** чтобы продолжить удаление.
8. Если контроллер домена в настоящее время содержит одну или несколько операций главной роли, щелкните **ОК** для перемещения к контроллеру домена, который отображается роль или роли. Нельзя изменить этот контроллер домена. Если вы хотите переместить роль на другой контроллер домена, необходимо переместить роль после завершения процедуры очистки метаданных сервера.

## <a name="clean-up-server-metadata-using-activedirectory-sites-and-services"></a>Очистка метаданных сервера, с помощью Active Directory — сайты и службы

1. Откройте компонент "Active Directory — сайты и службы".
2. Если вы определили партнеров репликации в процессе подготовки для выполнения этой процедуры и если вы не подключены к партнеру репликации контроллера домена, удаленные, метаданные которого тонких, щелкните правой кнопкой мыши **Active Directory — сайты и службы** , а затем нажмите кнопку **Сменить контроллер домена**. Щелкните имя контроллера домена, из которого вы хотите удалить метаданные, а затем нажмите кнопку **ОК**.
3. Разверните узел сайта контроллера домена, принудительно была удалена, затем **серверы**, разверните узел имени контроллера домена, щелкните правой кнопкой мыши объект параметров NTDS и нажмите кнопку **удалить**.
4. В **Active Directory — сайты и службы** диалоговом окне щелкните **Да** для подтверждения удаления параметров NTDS.
5. В **удаление контроллера домена** выберите **этот контроллер домена без возможности восстановления вне сети и больше не может быть понижена с помощью Active Directory домена службы установки мастер (DCPROMO)**, а затем нажмите кнопку **удалить**.
6. Если контроллер домена является сервером глобального каталога в **удалить контроллер домена** диалоговом окне щелкните **Да** чтобы продолжить удаление.
7. Если контроллер домена в настоящее время содержит одну или несколько операций главной роли, щелкните **ОК** для перемещения к контроллеру домена, который отображается роль или роли.
8. Щелкните правой кнопкой мыши контроллер домена, принудительно был удален и щелкните Удалить.
9. В **доменных служб Active Directory** диалоговом окне щелкните **Да** для подтверждения удаления контроллера домена.

## <a name="clean-up-server-metadata-using-the-command-line"></a>Очистка метаданных сервера, с помощью командной строки

Кроме того можно очистить метаданные с помощью Ntdsutil.exe, средство командной строки, который автоматически устанавливается на всех контроллерах домена и серверов, которые развернуты службы Active Directory Lightweight Directory (AD LDS) установлен. Ntdsutil.exe также доступна на компьютерах с Установленными средствами.

## <a name="to-clean-up-server-metadata-by-using-ntdsutil"></a>Очистка метаданных сервера с помощью программы Ntdsutil

1. Откройте командную строку с правами администратора: На **запустить** меню, щелкните правой кнопкой мыши **командной**, а затем нажмите кнопку **Запуск от имени администратора**. Если **контроль учетных записей пользователей** открывшемся диалоговом окне укажите учетные данные администратора организации при необходимости и нажмите кнопку **Продолжить**.
2. В командной строке введите следующую команду и нажмите клавишу ВВОД:

   `ntdsutil`

3. В командной строке `ntdsutil:` введите следующую ниже команду, а затем нажмите клавишу ВВОД.

   `metadata cleanup`

4. В командной строке `metadata cleanup:` введите следующую ниже команду, а затем нажмите клавишу ВВОД.

   `remove selected server <ServerName>`

5. В **диалоговое окно настройки удаления сервера**, просмотрите сведения и предупреждение и нажмите кнопку **Да** удаляемый объект сервера и метаданных.

   На этом этапе Ntdsutil подтверждает, что контроллер домена был успешно удален. Если появится сообщение об ошибке, указывающее, что объект не найден, контроллер домена был удален ранее.

6. В `metadata cleanup:` и `ntdsutil:` диалоги, тип `quit`, и нажмите клавишу ВВОД.

7. Чтобы подтвердить удаление контроллера домена:

   Откройте Active Directory-пользователи и компьютеры. В домене контроллера домена, удаленные, нажмите кнопку **контроллеры домена**. В области сведений щелкните объект для контроллера домена, который вы удалили не должны отображаться.

   Откройте Active Directory — сайты и службы. Перейдите к **серверы** контейнера и убедитесь, что объект сервера для контроллера домена, который вы удалили не содержит объект параметров NTDS. Если отсутствуют дочерние объекты отображаются под объект сервера, можно удалить объект сервера. Если дочерний объект, не удаляйте объект сервера, так как объект используется другим приложением.

## <a name="see-also"></a>См. также

* [Понижение уровня контроллеров домена](Demoting-Domain-Controllers-and-Domains--Level-200-.md)
* [Справочник по командам Ntdsutil](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc753343(v=ws.10))