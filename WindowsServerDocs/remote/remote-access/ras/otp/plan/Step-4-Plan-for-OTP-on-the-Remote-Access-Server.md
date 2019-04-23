---
title: Шаг 4 Планирование OTP на сервере удаленного доступа
description: Этот раздел является частью руководства развертывание удаленного доступа с проверкой подлинности OTP в Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4b97b2fd-767a-45c1-a64e-5b3edd0c8a47
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 470eebc82177a21985afb8d0bf143427a33d65fb
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2019
ms.locfileid: "59825445"
---
# <a name="step-4-plan-for-otp-on-the-remote-access-server"></a>Шаг 4 Планирование OTP на сервере удаленного доступа

>Область применения. Windows Server (полугодовой канал), Windows Server 2016

После планирования для одноразового пароля (OTP) RADIUS-сервера и параметры сертификата, последним шагом в планировании развертывания удаленного доступа OTP является планирование для параметров клиента OTP на сервере удаленного доступа.  
  
|Задача|Описание|  
|----|--------|  
|[4.1 Планирование исключений OTP клиента](#bkmk_4_1_Exemptions)|План для исключения для пользователей, которые не требуется для проверки подлинности с помощью OTP.|  
|[4.2 планирование для клиентов Windows 7](#bkmk_4_2_Win7)|Спланируйте развертывание DirectAccess Connectivity Assistant (DCA) 2.0 для клиентских компьютеров Windows 7.|  
|[4.3 план для смарт-карт](#BKMK_smartcard)|Спланируйте использование смарт-карт для дополнительной авторизации.|  
  
## <a name="bkmk_4_1_Exemptions"></a>4.1 Планирование исключений OTP клиента  
Если включена проверка подлинности OTP, по умолчанию все пользователи должны проходить проверку подлинности с помощью сочетания имени пользователя и пароль, а учетные данные OTP. Тем не менее можно разрешить выбранным пользователям проходить проверку подлинности с помощью имени пользователя и пароль, только без OTP. Чтобы сделать это, создайте группу безопасности и добавления пользователей, которые должны будут исключены из проверки подлинности OTP.  
  
> [!NOTE]  
> Потому, что можно исключить только клиентским компьютерам из одного леса, только одну группу безопасности может быть выбран для исключения клиента.  
  
## <a name="bkmk_4_2_Win7"></a>4.2 планирование для клиентов Windows 7  
По умолчанию клиентские компьютеры Windows 7 не может проверять подлинность с помощью OTP.  Клиентские компьютеры Windows 7 требуется DCA 2.0 для проверки подлинности с помощью OTP в развертывании удаленного доступа Windows Server 2012. Дополнительные сведения о DCA 2.0, см. в разделе [DirectAccess Connectivity Assistant 2.0](https://go.microsoft.com/fwlink/?LinkId=253699) в центре загрузки Майкрософт.  
  
## <a name="BKMK_smartcard"></a>4.3 план для смарт-карт  
Если включена проверка подлинности OTP, доступен параметр, чтобы включить использование смарт-карт для дополнительной авторизации. Создайте группу безопасности, чтобы разрешить временный доступ, в случае недоступности пользователя смарт-карты не работает.  
  
## <a name="BKMK_Links"></a>См. также  
  
-   [Настройка DirectAccess с проверкой подлинности OTP](https://technet.microsoft.com/windows-server-docs/networking/remote-access/ras/otp/deploy-ra-otp)  
  

