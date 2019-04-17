---
ms.assetid: 27e1e299-0beb-4e86-8143-1ba031dc3502
title: "Добавление сертификата расшифровки токенов"
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 0eba51521e7ef88542bccf93d92d2e783d800b5e
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/12/2017
---
# <a name="add-a-token-decrypting-certificate"></a>Добавление сертификата расшифровки токенов

>Область применения: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Серверы федерации используют сертификат расшифровки token\, если сервер федерации проверяющей стороной должно расшифровывать токены, выданные с более старым сертификатом после нового сертификата в качестве основного сертификата расшифровки. Active Directory службы федерации \(AD FS\) \(SSL\) Secure Sockets Layer сертификат используется для \(IIS\) Internet Information Services как сертификат расшифровки по умолчанию.  
  
> [!CAUTION]  
> Сертификаты, используемые для расшифровки token\ крайне важную роль для стабильности службы федерации. Поскольку потеря или незапланированное удаление всех сертификатов, настроенных для этой цели могут нарушить работу службы, следует создать резервную копию всех сертификатов, настроенных для этой цели.  
  
Добавление сертификата расшифровки token\ управления AD FS оснастка из файла, который вы экспортировали, можно использовать следующую процедуру.  
  
Членство в группе **Администраторы**, или эквивалентной группе на локальном компьютере минимальным требованием для выполнения этой процедуры.  Подробные сведения об использовании соответствующих учетных записей и членстве в группах в [локальные и доменные группы по умолчанию](https://go.microsoft.com/fwlink/?LinkId=83477) \ (http:///\/ go.microsoft.com\/fwlink\ /? LinkId\ = 83477\).   
  
### <a name="to-add-a-token-decrypting-certificate"></a>Добавление сертификата расшифровки token\  
  
1.  На **запустить** введите**управления AD FS**, и нажмите клавишу ВВОД.  
  
2.  В дереве консоли двойном щелчке **службы**, а затем нажмите кнопку **сертификаты**.  
  
3.  В **действия** панели, щелкните **сертификат расшифровки добавить Token\** ссылку.  
  
4.  В **поиск файла сертификата** диалоговом окне перейдите к файлу сертификата, который требуется добавить, выберите файл сертификата и нажмите кнопку **откройте**.  
  
## <a name="additional-references"></a>Дополнительные ссылки  
[Контрольный список: Настройка сервера федерации](Checklist--Setting-Up-a-Federation-Server.md)  
  
[Требования к сертификатам для серверов федерации](https://technet.microsoft.com/library/dd807040.aspx)  
  
