---
title: "Обзор проверки подлинности Kerberos"
description: "Безопасность Windows Server"
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-kerberos
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 646c6309-e865-4be2-b415-44dd125af5c2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 9f8878fb959c34663b1e1f3858fa7e0b6e7b6105
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/12/2017
---
# <a name="kerberos-authentication-overview"></a>Обзор проверки подлинности Kerberos

>Область применения: Windows Server (канал точками годовой), Windows Server 2016

Kerberos — это протокол проверки подлинности, который используется для проверки удостоверения пользователя или узла. Этот раздел содержит сведения о проверке подлинности Kerberos в Windows Server 2012 и Windows 8.

## <a name="BKMK_OVER"></a>Описание компонентов
Операционные системы Windows Server реализуют протокол проверки подлинности Kerberos версии 5 и расширения для проверка подлинности открытого ключа, переноса данных авторизации и делегирования. Клиент проверки подлинности Kerberos реализован как поставщик поддержки безопасности \(SSP\) и он может осуществляться через интерфейс поставщика поддержки безопасности \(SSPI\). Начальная проверка подлинности пользователя интегрирована в архитектуру единого Winlogon входа в систему.

Центр распространения ключей Kerberos \(KDC\) встроен в другие службы безопасности Windows Server, работающие на контроллере домена. KDC использует базу данных домена в доменных службах Active Directory в качестве базы данных учетной записи безопасности. Доменные службы Active Directory необходима для реализаций Kerberos по умолчанию в рамках домена или леса.

## <a name="kerb_tr_Kerb_Benefits"></a>Практическое применение
Ниже перечислены преимущества, за счет использования Kerberos для проверки подлинности на основе domain\.

-   **Делегированная проверка подлинности.**

    Службы, работающие в операционных системах Windows могут олицетворять клиентский компьютер, при доступе к ресурсам от имени клиента. Во многих случаях служба может выполнить свою работу для клиента путем доступа к ресурсам на локальном компьютере. Когда клиентский компьютер проходит проверку подлинности службе, протоколы NTLM и Kerberos предоставляют сведения авторизации, что службе необходимо олицетворять клиентский компьютер локально. Однако некоторые распределенные приложения разработаны, чтобы служба front\ окончания необходимо использовать удостоверение клиентского компьютера, когда он подключается к службам back\ окончания на других компьютерах. Проверка подлинности Kerberos поддерживает механизм делегирования, позволяющий службе действовать от имени клиента при подключении к другим службам.

-   **Единый вход.**

    С помощью Kerberos проверки подлинности в домене или в лесу позволяет пользователю или службе получать доступ к ресурсам, разрешенным администраторами, без многократного ввода учетных данных. После первоначального входа в систему домена через функцию Winlogon протокол Kerberos управляет учетными данными по всему лесу при каждой попытке доступа к ресурсам.

-   **Возможности взаимодействия.**

    В реализации протокола Kerberos V5 Майкрософт основана на спецификациях отслеживания standards\, рекомендуется \(IETF\) Internet Engineering Task Force. В результате в операционных системах Windows протокол Kerberos лежит в основе взаимодействия с другими сетями, в которых используется протокол Kerberos для проверки подлинности. Кроме того Корпорация Майкрософт публикует документацию протоколы Windows для реализации протокола Kerberos. Документация содержит технические требования, ограничения, зависимости и поведение протокола конкретного ими корпорации Майкрософт о реализации протокола Kerberos.

-   **Более эффективная проверка подлинности на серверы.**

    Перед применением Kerberos проверка подлинности NTLM может использоваться, что требует сервер приложений, чтобы подключиться к контроллеру домена для проверки подлинности каждого клиентского компьютера или службы. С помощью протокола Kerberos возобновляемые билеты сеанса заменяют pass\ через проверку подлинности. Сервер не требуется переходить к контроллеру домена \ (если только требуется проверка \(PAC\)\) сертификата атрибута привилегий. Вместо этого сервер может проверить подлинность клиентского компьютера путем проверки учетных данных, предоставленных клиентом. Клиентские компьютеры могут получить учетные данные для определенного сервера однократно и затем использовать их на протяжении всего сеанса входа в систему.

-   **Взаимная проверка подлинности.**

    С помощью протокола Kerberos сторона на любом конце сетевого подключения может проверить, что сторона на противоположном конце является субъектом, за которого себя выдает. NTLM не позволяет клиентам проверять удостоверение сервера или одному серверу проверять удостоверение другого. Проверка подлинности NTLM предназначена для сетевой среды, в которой серверы считаются подлинными. Протокол Kerberos такого допущения нет.

## <a name="see-also"></a>См. также:
[Обзор проверки подлинности Windows](../windows-authentication/windows-authentication-overview.md)

