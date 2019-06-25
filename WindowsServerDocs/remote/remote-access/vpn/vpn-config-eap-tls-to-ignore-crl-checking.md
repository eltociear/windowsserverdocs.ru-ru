---
title: Настройка игнорирования проверки списка отзыва сертификатов (CRL) в EAP-TLS
description: Клиент EAP-TLS не удается подключиться, если сервер политики сети завершает проверку отзыва цепочки сертификатов (включая корневой сертификат), клиент и проверяет, что сертификаты были отозваны.
services: active-directory
ms.prod: windows-server-threshold
ms.technology: networking-ras
documentationcenter: ''
ms.assetid: ''
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2018
ms.author: pashort
author: shortpatti
ms.localizationpriority: medium
ms.reviewer: deverette
ms.openlocfilehash: 781239f45b9b260b7d374c2a6972cdb8faad2879
ms.sourcegitcommit: 0948a1abff1c1be506216eeb51ffc6f752a9fe7e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/06/2019
ms.locfileid: "66749594"
---
# <a name="step-71-configure-eap-tls-to-ignore-certificate-revocation-list-crl-checking"></a>Шаг 7.1. Настройка игнорирования проверки списка отзыва сертификатов (CRL) в EAP-TLS

>Относится к: Windows Server (полугодовой канал), Windows Server 2016, Windows Server 2012 R2, Windows 10

- [**Предыдущих:** Шаг 7. (Необязательно) Условный доступ для VPN-подключения с помощью Azure AD](ad-ca-vpn-connectivity-windows10.md)
- [**Далее:** Шаг 7.2. Создание корневых сертификатов для проверки подлинности VPN с помощью Azure AD](vpn-create-root-cert-for-vpn-auth-azure-ad.md)

>[!IMPORTANT]
>Для реализации этого изменения в реестр вызывает подключения IKEv2, использование сертификатов облака с помощью PEAP переход на другой, но подключения IKEv2 с использованием сертификатов проверки подлинности клиента, выданный ЦС на предприятии продолжает работать.

На этом этапе можно добавить **IgnoreNoRevocationCheck** и настройте его для разрешения проверки подлинности клиентов в том случае, если сертификат не содержит точки распространения списков отзыва Сертификатов. По умолчанию IgnoreNoRevocationCheck имеет значение 0 (отключен).

>[!NOTE]
>Если Windows маршрутизации и удаленного доступа (RRAS) использует сервер политики сети на прокси-сервер RADIUS вызывает на второй сервер политики сети, то необходимо задать **IgnoreNoRevocationCheck = 1** на обоих серверах.

Клиент EAP-TLS не удается подключиться, если сервер политики сети завершается проверка цепочки сертификатов (включая корневой сертификат). Cloud сертификаты, выданные Azure AD для пользователя нет список отзыва Сертификатов, поскольку они являются короткоживущими сертификаты со сроком жизни один час. EAP на сервере политики сети должен быть настроен для игнорирования отсутствие списка отзыва Сертификатов. По умолчанию IgnoreNoRevocationCheck имеет значение 0 (отключен). Добавьте IgnoreNoRevocationCheck и присвойте ей значение 1 для разрешения проверки подлинности клиентов в том случае, если сертификат не содержит точки распространения списков отзыва Сертификатов. 

Так как метод проверки подлинности EAP-TLS, это значение реестра требуется только в разделе EAP\13. Если используются другие методы проверки подлинности EAP, затем значение реестра необходимо добавить в те также. 

**Процедура**

1. Откройте **regedit.exe** на NPS-сервере.

2. Перейдите к **HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\RasMan\PPP\EAP\13**.

3. Выберите **изменить > New** и выберите **DWORD (32-разрядное) значение** и введите **IgnoreNoRevocationCheck**.

4. Дважды щелкните **IgnoreNoRevocationCheck** и задать для него значение **1**.

5. Выберите **ОК** и перезагрузите сервер. Перезапуск службы RRAS и NPS не достаточно.

Дополнительные сведения см. в разделе [как включить или отключить проверка отзыва сертификатов (CRL) на клиентах](https://technet.microsoft.com/library/bb680540.aspx).


|Путь реестра  |Расширение EAP  |
|---------|---------|
|HKLM\SYSTEM\CurrentControlSet\Services\RasMan\PPP\EAP\13     |Протокол EAP-TLS         |
|HKLM\SYSTEM\CurrentControlSet\Services\RasMan\PPP\EAP\25     |PEAP         |
|HKLM\SYSTEM\CurrentControlSet\Services\RasMan\PPP\EAP\26     |EAP-MSCHAP v2         |

## <a name="next-steps"></a>Следующие шаги

[Шаг 7.2. Создать корневые сертификаты для проверки подлинности VPN с Azure AD](vpn-create-root-cert-for-vpn-auth-azure-ad.md): На этом шаге настраивается условного доступа корневые сертификаты для проверки подлинности VPN с Azure AD, который автоматически создает VPN-сервер облачного приложения в клиенте.