---
ms.assetid: 27e1e299-0beb-4e86-8143-1ba031dc3502
title: Добавление сертификата расшифровки токенов
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 5714a41950b9c2f818ddc154a9af7a55fdb362d8
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/08/2020
ms.locfileid: "80814968"
---
# <a name="add-a-token-decrypting-certificate"></a>Добавление сертификата расшифровки токенов

Серверы федерации используют токен\-сертификата расшифровки, когда сервер федерации проверяющей стороны должен расшифровывать маркеры, выпущенные с помощью старого сертификата, после того, как в качестве основного сертификата расшифровки был задан новый сертификат. Службы федерации Active Directory (AD FS) \(AD FS\) использует SSL \(сертификат SSL\) для службы IIS \(IIS\) в качестве сертификата расшифровки по умолчанию.  
  
> [!CAUTION]  
> Сертификаты, используемые для дешифрования\-маркеров, крайне важны для стабильности служба федерации. Поскольку потери или незапланированные удаления любых сертификатов, настроенных для этой цели, могут нарушить работу службы, следует создать резервную копию всех сертификатов, настроенных для этой цели.  
  
Для добавления маркера\-расшифровки сертификата в оснастку управления AD FS\-в из экспортированного файла можно использовать следующую процедуру.  
  
Для выполнения этой процедуры требуется членство в группе **Администраторы** или в эквивалентной группе на локальном компьютере.  Просмотрите сведения об использовании соответствующих учетных записей и членства в группах в [локальной среде и группах домена по умолчанию](https://go.microsoft.com/fwlink/?LinkId=83477) \(http:\/\/go.Microsoft.com\/fwlink\/? LinkId\=83477\).   
  
### <a name="to-add-a-token-decrypting-certificate"></a>Добавление маркера\-расшифровки сертификата  
  
1.  На **начальном** экране введите**AD FS управление**и нажмите клавишу ВВОД.  
  
2.  В дереве консоли дважды\-кнопку **Служба**, а затем выберите пункт **Сертификаты**.  
  
3.  На панели **действия** щелкните ссылку **Добавить токен\-расшифровку сертификата** .  
  
4.  В диалоговом окне **Выбор файла сертификата** перейдите к файлу сертификата, который необходимо добавить, выберите файл сертификата и нажмите кнопку **Открыть**.  
  
## <a name="additional-references"></a>Дополнительная справка  
[Контрольный список: Настройка сервера федерации](Checklist--Setting-Up-a-Federation-Server.md)  
  
[Требования к сертификатам для серверов федерации](https://technet.microsoft.com/library/dd807040.aspx)  
  

