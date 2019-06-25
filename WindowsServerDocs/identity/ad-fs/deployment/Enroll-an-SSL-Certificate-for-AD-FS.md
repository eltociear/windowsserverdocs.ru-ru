---
ms.assetid: 3095e6a7-b562-4c6a-bf29-13b32c133cac
title: Регистрация SSL-сертификата для AD FS
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: e80927f2670614d2949f4e67cc158319f05c5fa0
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/24/2019
ms.locfileid: "66192150"
---
# <a name="enroll-an-ssl-certificate-for-ad-fs"></a>Регистрация SSL-сертификата для AD FS

Службы федерации Active Directory \(AD FS\) наличие сертификата Secure Socket Layer \(SSL\) проверки подлинности сервера на каждом сервере федерации в ферме серверов федерации. Тот же сертификат можно использовать на каждом сервере федерации в ферме. Сертификат и его закрытый ключ должны быть доступны. Например, если сертификат и его закрытый ключ находятся в PFX-файле, то можно импортировать этот файл непосредственно в мастер настройки служб федерации Active Directory. Этот SSL-сертификат должен содержать указанные ниже данные.  
  
1.  Имя субъекта и альтернативное имя субъекта должно содержать имя службы федерации, например fs.contoso.com.  
  
2.  Альтернативное имя субъекта должно содержать значение **enterpriseregistration** , а затем по имени участника-пользователя \(имени участника-пользователя\) суффикс вашей организации, например,  **enterpriseregistration.corp.contoso.com**.  
  
    > [!WARNING]  
    > Укажите альтернативное имя субъекта, если вы планируете включить службу регистрации устройств \(DRS\) для присоединения к рабочему месту.  
  
> [!IMPORTANT]  
> Если ваша организация использует несколько суффиксов имени участника-пользователя, и вы планируете включить службы DRS, SSL-сертификат должен содержать запись альтернативного имени субъекта для каждого суффикса.  
  
## <a name="see-also"></a>См. также
[Развертывание AD FS](../../ad-fs/AD-FS-Deployment.md)  

[Руководство по развертыванию Windows Server 2012 R2 AD FS](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)  
 
[Развертывание фермы серверов федерации](../../ad-fs/deployment/Deploying-a-Federation-Server-Farm.md)  
  
  
