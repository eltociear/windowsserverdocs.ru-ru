---
ms.assetid: e02bb152-d0db-40b0-9942-846dce75f6c7
title: Требования к развертыванию доменных служб Active Directory
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: d21491f5ce9c15ecc514e4be24a91de28b0fd0ce
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2019
ms.locfileid: "59890975"
---
# <a name="ad-ds-deployment-requirements"></a>Требования к развертыванию доменных служб Active Directory

>Область применения. Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Структура существующей среды определяет стратегии для развертывания служб Windows Server 2008 Active Directory домена (AD DS). Если вы создаете в среде AD DS, у вас нет существующей структуры домена завершить создание Доменных службах Active Directory, прежде чем начать создание среды AD DS. Затем можно развернуть новый корневой домен леса и развернуть остальную часть структуры доменов в соответствии с вашей разработки.  
  
Кроме того, как часть развертывания AD DS можно обновить и реструктурировать вашей среде. Например если ваша организация имеет существующую структуру доменов Windows 2000, может выполнить обновление на месте из некоторых доменов и реструктуризации другим пользователям. Кроме того можно снизить сложность среды путем реструктуризации доменов между лесами или реструктуризации доменов в лесу, после развертывания AD DS.  
  
## <a name="deploying-a-windows-server-2008-forest-root-domain"></a>Развертывание корневого домена леса Windows Server 2008  
Корневого домена леса предоставляет основу для вашей инфраструктуры леса AD DS. Для развертывания AD DS, необходимо сначала развернуть корневой домен леса. Чтобы сделать это, необходимо проверить разработку AD DS; Настройка службы DNS для корневого домена леса; Создание корневого домена леса, который состоит из развертывания контроллеры корневого домена леса, Настройка топологии сайта для корневого домена леса и Настройка роли хозяина операций (также известный как гибкие операции с единым хозяином или FSMO); и повысить функциональные уровни леса и домена. Ниже показан общий процесс развертывания корневого домена леса.  
  
![Требования служб AD DS](media/AD-DS-Deployment-Requirements/033aad0b-25ff-4793-8825-88a6daa01a55.gif)  
  
Дополнительные сведения см. в разделе [развертывание корневого домена леса Windows Server 2008](https://technet.microsoft.com/library/cc731174.aspx).  
  
## <a name="deploying-windows-server-2008-regional-domains"></a>Развертывание региональных доменов Windows Server 2008  
После завершения развертывания корневого домена леса, все готово для развертывания любой Windows Server 2008 региональных доменов, которые указаны в проекте. Чтобы сделать это, необходимо развернуть контроллеры домена для каждого регионального домена. На следующем рисунке процесс развертывания региональных доменов.  
  
![Требования служб AD DS](media/AD-DS-Deployment-Requirements/89a878c8-9a94-4180-ad43-ca75316a6318.gif)  
  
Дополнительные сведения см. в разделе [развертывание Windows Server 2008 региональных доменов](https://technet.microsoft.com/library/cc755118.aspx).  
  
## <a name="upgrading-active-directory-domains-to-windows-server-2008"></a>Обновление доменов Active Directory для Windows Server 2008  
Обновление доменов Windows 2000 или Windows Server 2003 до Windows Server 2008 — это эффективный и простой способ воспользоваться преимуществами дополнительных возможностей Windows Server 2008 и функций. Вы можете обновить домены для поддержания вашей текущей конфигурации сети и домена, при этом повысив безопасность, масштабируемость и управляемость сетевой инфраструктуры. Обновление с Windows 2000 или Windows Server 2003 до Windows Server 2008 требует минимальной настройки сети. Обновление также мало влияет на работу пользователей. Дополнительные сведения см. в разделе [обновления доменов Active Directory до Windows Server 2008 и Windows Server 2008 R2 доменов доменных Служб](https://technet.microsoft.com/library/cc731188.aspx).  
  
## <a name="restructuring-ad-ds-domains"></a>Реструктуризация доменов AD DS  
При реструктуризации доменов между лесами Windows Server 2008 (между лесами реструктуризации), можно сократить количество доменов в вашей среде и таким образом снизить сложность администрирования и соответствующие трудозатраты. При переносе объектов между лесами в рамках этого процесса реструктуризации, оба исходного домена и целевой доменных средах существуют одновременно. Это позволяет откатить для исходной среды во время миграции, при необходимости.  
  
При реструктуризации доменов Windows Server 2008 в рамках леса Windows Server 2008 (Реструктуризация), можно объединить структуру доменов и таким образом снизить сложность администрирования и соответствующие трудозатраты. При реструктуризации доменов в лесу, мигрированных учетных записей больше не существуют в исходном домене.  
  
Дополнительные сведения об использовании реструктуризации доменов Active Directory миграции в средство (ADMT) версии 3.1 (ADMT v3.1) см. в разделе [ADMT v3.1 руководство по миграции](https://go.microsoft.com/fwlink/?LinkId=93678).  
  

