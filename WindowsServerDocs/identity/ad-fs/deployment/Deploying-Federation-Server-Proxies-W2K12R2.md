---
ms.assetid: 222e9f93-7c41-4527-8a98-8f7fbc7a58af
title: Развертывание прокси-серверов федерации
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 330214e83b6da5bf711c36995306f8f1a098fa24
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/24/2019
ms.locfileid: "66192215"
---
# <a name="deploying-federation-server-proxies"></a>Развертывание прокси-серверов федерации

В службах федерации Active Directory \(AD FS\) в Windows Server 2012 R2 роль прокси-сервера федерации выполняет, новая служба роли удаленного доступа, которая называется прокси веб-приложения. Чтобы разрешить доступ к AD FS доступ из-за пределами корпоративной сети, что является целью развертывания прокси-сервера федерации в прежних версиях AD FS, например AD FS 2.0 и AD FS в Windows Server 2012, можно развернуть один или несколько прокси веб-приложений для A D FS в Windows Server 2012 R2.  
  
В контексте AD FS прокси веб-приложения выступает в качестве прокси-сервера федерации AD FS. Кроме того, прокси-сервер веб-приложения предоставляет функции обратного прокси-сервера для веб-приложений в корпоративной сети, что делает их доступными для пользователей с любых устройств из-за пределов корпоративной сети. Дополнительные сведения о службе роли прокси веб-приложения см. в разделе "Обзор прокси-сервера веб-приложения".  
  
При планировании развертывания прокси-сервера веб-приложения можно использовать сведения из следующих разделов.  
  
-   [Планирование инфраструктуры прокси-сервера веб-приложений (WAP)](https://technet.microsoft.com/library/dn383648.aspx)  
  
-   [Планирование сервера прокси-сервера веб-приложений](https://technet.microsoft.com/library/dn383647.aspx)  
  
При развертывании прокси-сервера веб-приложения можно следовать процедурам в следующих разделах.  
  
-   [Настройка инфраструктуры прокси-сервера веб-приложений](https://technet.microsoft.com/library/dn383644.aspx)  
  
-   [Установка и настройка сервера прокси-сервера веб-приложений](https://technet.microsoft.com/library/dn383662.aspx)  
  
 
## <a name="see-also"></a>См. также 

[Развертывание AD FS](../../ad-fs/AD-FS-Deployment.md)  

[Руководство по развертыванию Windows Server 2012 R2 AD FS](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)  
 
[Развертывание фермы серверов федерации](../../ad-fs/deployment/Deploying-a-Federation-Server-Farm.md)  
  
