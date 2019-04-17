---
title: "Восстановление леса AD — Очистка метаданных удаленных контроллеров домена"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: e7543381-4081-407f-adad-a9de792c6616
ms.technology: identity-adfs
ms.openlocfilehash: 3027c59b58801b44d20127e6bcf62dd7319708bd
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/12/2017
---
# <a name="ad-forest-recovery---cleaning-metadata-of-removed-writable-domain-controllers"></a>Восстановление леса AD — Очистка метаданных удаленных для записи контроллеров домена 

>Область применения: Windows Server 2016, Windows Server 2012 и 2012 R2, Windows Server 2008 и 2008 R2
 
 Очистка метаданных удаляет данные Active Directory, определяющий контроллеру домена в системе репликации.  
  
 Используйте следующую процедуру для удаления объектов контроллеров домена для контроллеров домена, которые планируется добавить к сети путем повторной установки AD DS.  
  
 Если вы используете версию Active Directory-пользователи и компьютеры Active Directory — сайты и службы, которые включены средства удаленного администрирования сервера (RSAT), автоматически выполняется очистка метаданных, при удалении объекта контроллера домена.  
  

## <a name="deleting-a-domain-controller-using-active-directory-users-and-computers"></a>Удаление контроллера домена, с помощью Active Directory-пользователи и компьютеры  
 При использовании версии Active Directory-пользователи и компьютеры или Центр администрирования Active Directory в средств администрирования удаленного сервера (RSAT), Очистка метаданных выполняется автоматически при удалении объекта контроллера домена. Объект-сервер и объект-компьютер также будут автоматически удалены.  
  
 В качестве альтернативы Вы можно также использовать Active Directory — сайты и службы в средства удаленного администрирования сервера для удаления объекта контроллера домена. Если вы используете Active Directory — сайты и службы, необходимо удалить связанного сервера объекта и объект параметров NTDS перед удалением объект контроллера домена.  
  
 Чтобы загрузить RSAT:  

-   [Средства удаленного администрирования сервера для Windows 10](https://www.microsoft.com/download/details.aspx?id=45520)
  
-   [Средства удаленного администрирования сервера для Windows 8](https://www.microsoft.com/download/details.aspx?id=28972)  

-   [Средства удаленного администрирования сервера для Windows 7 с пакетом обновления 1 (SP1)](https://www.microsoft.com/download/details.aspx?id=7887)  
  
-   [Средства удаленного администрирования сервера для Windows Vista](https://www.microsoft.com/download/details.aspx?id=21090)  
  
 Следующая процедура является одинаковым для контроллеров домена под управлением либо Windows Server 2016, 2012, 2008 R2 или 2008. Целевой контроллер домена операции очистки метаданных можно запустить в любой версии Windows Server.  
  
### <a name="to-delete-a-domain-controller-object-using-active-directory-users-and-computers-in-rsat"></a>Чтобы удалить объект контроллера домена, с помощью Active Directory-пользователи и компьютеры в средства удаленного администрирования сервера  
  
1.  Нажмите кнопку **запустить**, нажмите кнопку **Администрирование**, а затем нажмите кнопку **Active Directory-пользователи и компьютеры**.  
2.  В дереве консоли дважды щелкните контейнер домена, а затем дважды щелкните **контроллеры домена** подразделение (OU).  
3.  В области сведений щелкните правой кнопкой мыши контроллер домена, который вы хотите удалить, а затем щелкните **удалить**. 
![Удаление](media/AD-Forest-Recovery-Cleaning-Metadata/delete1.png) 
4.  Нажмите кнопку **Да** для подтверждения удаления. Выберите **этот контроллер домена, постоянно находятся в автономном и можно больше нельзя понизить роль с помощью Active Directory домена службы установки мастер (DCPROMO)** флажок и нажмите кнопку **удалить**.  
5.  Если контроллер домена является сервером глобального каталога, щелкните **Да** убедитесь, что удаление.  
  
## <a name="next-steps"></a>Дальнейшие действия

- [Руководство по восстановлению леса AD](AD-Forest-Recovery-Guide.md)
- [Восстановление леса AD — процедуры](AD-Forest-Recovery-Procedures.md)
  