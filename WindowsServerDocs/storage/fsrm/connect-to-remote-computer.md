---
title: "Подключение к удаленному компьютеру"
description: "В этой статье описано, как подключиться к удаленному компьютеру, чтобы управлять ресурсами хранилища из диспетчера ресурсов файлового сервера"
ms.date: 7/7/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 93d2be926437b65ed8eb84a828ea0d7da6a51086
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/17/2017
---
# <a name="connect-to-a-remote-computer"></a>Подключение к удаленному компьютеру 

> Область применения: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

Чтобы управлять ресурсами хранилища на удаленном компьютере, можно подключиться к компьютеру из диспетчера ресурсов файлового сервера. При установленном подключении диспетчер ресурсов файлового сервера позволяет управлять квотами, файлами фильтра блокировки файлов, управлять категориями, планировать создание задач по управлению файлами и создавать отчеты по этим удаленным ресурсам.

> [!Note]
> Диспетчер ресурсов файлового сервера может управлять ресурсами на локальном или удаленном компьютере, однако не на обоих одновременно.

## <a name="to-connect-to-a-remote-computer-from-file-server-resource-manager"></a>Чтобы подключиться к удаленному компьютеру из диспетчера ресурсов файлового сервера, выполните следующие действия.

1.  В разделе **Администрирование** выберите **Диспетчер ресурсов файлового сервера**.

2.  В древе консоли щелкните правой кнопкой мыши **Диспетчер ресурсов файлового сервера**, а затем нажмите **Подключение к другому компьютеру**.

3.  В диалоговом окне **Подключение к другому компьютеру** нажмите кнопку **Другой компьютер**. Затем введите имя сервера, к которому необходимо подключиться (или щелкните **Обзор**, чтобы найти удаленный компьютер).

4.  Нажмите кнопку **OK**.

> [!Important]
> Команда **Подключение к другому компьютеру** доступна только при открытии диспетчера ресурсов файлового сервера в разделе **Администрирование**. При осуществлении доступа к диспетчеру ресурсов файлового сервера из диспетчера серверов эта команда недоступна.

## <a name="additional-considerations"></a>Дополнительные рекомендации

Для управления удаленными ресурсам с помощью диспетчера ресурсов файлового сервера:

-   Вы должны осуществить вход в систему локального компьютера, используя учетную запись домена, являющуюся членом группы **Администраторы** на удаленном компьютере.
-   Удаленный компьютер должен работать под управлением Windows Server, и должен быть установлен диспетчер ресурсов файлового сервера.
-   На удаленном компьютере должно быть включено исключение **Управление удаленным диспетчером ресурсов файлового сервера**. Включите это исключение, используя брандмауэр Windows на панели управления.

## <a name="see-also"></a>См. также:

-   [Управление ресурсами удаленного хранилища](managing-remote-storage-resources.md)