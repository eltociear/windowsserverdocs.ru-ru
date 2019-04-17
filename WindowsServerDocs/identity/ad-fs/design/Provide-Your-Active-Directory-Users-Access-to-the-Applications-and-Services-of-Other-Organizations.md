---
ms.assetid: 2d62386c-b466-4a54-b6fa-5d16cda120d8
title: "Предоставление Active Directory доступа пользователей к приложениям и службам других организаций"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: d50d26c5c654e5c91b82f6f209e21f257221c12d
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/03/2017
---
# <a name="provide-your-active-directory-users-access-to-the-applications-and-services-of-other-organizations"></a>Предоставление Active Directory доступа пользователей к приложениям и службам других организаций

>Область применения: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Эта цель развертывания \(AD FS\) служб федерации Active Directory основывается на цели в [предоставляют Your Active Directory Users Access to Your Claims-Aware Applications and Services](Provide-Your-Active-Directory-Users-Access-to-Your-Claims-Aware-Applications-and-Services.md).  
  
Если вы являетесь администратором в организации партнера по учетным записям и вам была поставлена задача развертывания предоставить сотрудникам федеративный доступ размещенным ресурсам в другой организации:  
  
-   Сотрудники, вошедшие в домен Active Directory в корпоративной сети можно использовать имя входа на функции \(SSO\) для доступа к нескольким веб-приложений или служб, которые защищены с помощью AD FS, когда приложения или службы расположены в другой организации. Дополнительные сведения см. в разделе [Federated Web SSO Design](Federated-Web-SSO-Design.md).  
  
    Например Fabrikam может потребоваться корпоративной сети федеративный доступ к веб-службам, размещенным в Contoso.  
  
-   Удаленные сотрудники, вошедшие в домен Active Directory можно получить токены AD FS от сервера федерации в вашей организации для получения федеративного доступа к защищенным службами AD FS — веб-приложениям или службам, размещенным в другой организации.  
  
    Например компании Fabrikam может потребоваться предоставить удаленным сотрудникам федеративный доступ к AD FS защищаемому службам, размещенным в Contoso, без обязательного сотрудников Fabrikam в корпоративную сеть Fabrikam.  
  
Помимо основных компонентов, которые описаны в [предоставляют Your Active Directory Users Access to Your Claims-Aware Applications and Services](Provide-Your-Active-Directory-Users-Access-to-Your-Claims-Aware-Applications-and-Services.md) и затенены на следующем рисунке, для этой цели развертывания потребуются следующие компоненты:  
  
-   **Учетная запись прокси-сервера федерации партнера:** сотрудники, осуществляющие доступ к федеративной службе или приложению из Интернета можно использовать этот компонент службы федерации Active Directory для выполнения проверки подлинности. По умолчанию этот компонент выполняет проверку подлинности форм, но его также можно выполнить обычную проверку подлинности. Можно также настроить этот компонент для выполнения проверки подлинности клиента \(SSL\) протокола SSL, если сотрудники в вашей организации располагают соответствующими сертификатами. Дополнительные сведения см. в разделе [Where to Place a Federation Server Proxy](Where-to-Place-a-Federation-Server-Proxy.md).  
  
-   **Службу DNS периметра:** Эта реализация \(DNS\) доменных имен содержит имена узлов для сети периметра. Дополнительные сведения о настройке DNS периметра для прокси-сервера федерации см. в разделе [требования к разрешению имен для прокси-серверов федерации](Name-Resolution-Requirements-for-Federation-Server-Proxies.md).  
  
-   **Удаленный сотрудник:** удаленный сотрудник получает доступ к веб-приложение \ (через поддерживаемый веб browser\) или веб-службе \ (с помощью включать), используя действительные учетные данные из корпоративной сети, когда пользователь работает удаленно через Интернет. Клиентский компьютер сотрудника в удаленном расположении взаимодействует непосредственно с прокси-сервера федерации, для создания токена и проверки подлинности для приложения или службы.  
  
После просмотра сведений в соответствующих разделах можно начать развертывание, выполняя следующие действия, описанные в [контрольный список: реализация проекта Единого федеративного Web](../../ad-fs/deployment/Checklist--Implementing-a-Federated-Web-SSO-Design.md).  
  
На следующем рисунке показано все необходимые компоненты для этой цели развертывания Служб федерации Active Directory.  
  
![доступ к приложениям](media/50af4837-31e0-451f-a942-e705c2300065.gif)  
  
## <a name="see-also"></a>См. также:
[Руководство по разработке служб AD FS в Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)