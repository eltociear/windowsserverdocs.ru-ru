---
title: What's New in Kerberos Authentication
ms.prod: windows-server
ms.topic: article
ms.assetid: 7bd17803-6e42-4a3b-803f-e47c74725813
manager: alanth
author: justinha
ms.technology: security-authentication
ms.date: 11/09/2016
ms.openlocfilehash: 35eff73e97c8fdbb6df2c1412779b033a9ca3fa5
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/08/2020
ms.locfileid: "80858817"
---
# <a name="whats-new-in-kerberos-authentication"></a>What's New in Kerberos Authentication

>Область применения: Windows Server 2016 и Windows 10

## <a name="kdc-support-for-public-key-trust-based-client-authentication"></a>Поддержка KDC для проверки подлинности клиента на основе открытого ключа

Начиная с Windows Server 2016, Кдкс поддерживает способ сопоставления открытого ключа. Если для учетной записи подготавливается открытый ключ, KDC поддерживает протокол Kerberos PKInit явным образом с помощью этого ключа. Поскольку проверка сертификата не выполняется, поддерживаются самозаверяющие сертификаты, и механизм проверки подлинности не поддерживается.

Ключ доверия рекомендуется использовать при настройке учетной записи независимо от значения параметра Усесубжекталтнаме.

## <a name="kerberos-client-and-kdc-support-for-rfc-8070-pkinit-freshness-extension"></a>Поддержка клиента Kerberos и KDC для расширения свежести RFC 8070 PKInit

Начиная с Windows 10, версии 1607 и Windows Server 2016, клиенты Kerberos пытаются попытаться установить [свежее расширение RFC 8070 PKInit](https://datatracker.ietf.org/doc/draft-ietf-kitten-pkinit-freshness/) для входа на основе открытых ключей. 

Начиная с Windows Server 2016, Кдкс может поддерживать свежее расширение PKInit. По умолчанию Кдкс не предлагают расширение обновления PKInit. Чтобы включить его, используйте новую поддержку KDC для расширения обновления безопасности с помощью административного шаблона KDC для всех контроллеров домена в домене. При настройке поддерживаются следующие параметры, если домен является режимом работы домена Windows Server 2016 (ДФЛ):

- **Отключено**. KDC никогда не предлагает расширение актуальности PKInit и принимает допустимые запросы проверки подлинности без проверки на актуальность. Пользователи никогда не получат новый идентификатор безопасности удостоверения открытого ключа.
- **Поддерживается**: расширение обновления PKInit поддерживается по запросу. Клиенты Kerberos, успешно прошедшие проверку подлинности с помощью расширения PKInit, получают новый идентификатор безопасности удостоверения открытого ключа.
- **Обязательно**. для успешной проверки подлинности требуется расширение обновления PKInit. Клиенты Kerberos, которые не поддерживают расширение PKInit, всегда будут завершаться ошибкой при использовании учетных данных открытого ключа.

## <a name="domain-joined-device-support-for-authentication-using-public-key"></a>Поддержка устройства, присоединенного к домену, для проверки подлинности с помощью открытого ключа

Начиная с Windows 10 версии 1507 и Windows Server 2016, если устройство, присоединенное к домену, может зарегистрировать свой открытый ключ в контроллере домена Windows Server 2016, устройство может пройти проверку подлинности с помощью открытого ключа, используя проверку подлинности Kerberos на контроллере домена Windows Server 2016. Дополнительные сведения см. в статье [Аутентификация с помощью открытого ключа устройства, присоединенного к домену](Domain-joined-Device-Public-Key-Authentication.md) .

## <a name="kerberos-clients-allow-ipv4-and-ipv6-address-hostnames-in-service-principal-names-spns"></a>Клиенты Kerberos разрешают адреса узлов IPv4 и IPv6 в именах субъектов-служб (SPN).

Начиная с Windows 10 версии 1507 и Windows Server 2016, клиенты Kerberos можно настроить для поддержки имен узлов IPv4 и IPv6 в именах участников-служб. 

Путь в реестре:

хклм\софтваре\микрософт\виндовс\куррентверсион\полиЦиес\систем\керберос\параметерс

Чтобы настроить поддержку имен узлов в именах участников-служб, создайте запись Трипспн. Эта запись не существует в реестре по умолчанию. После создания записи измените значение DWORD на 1. Если значение не настроено, имена узлов IP-адресов не будут пытаться.

Если имя субъекта-службы зарегистрировано в Active Directory, проверка подлинности выполняется с помощью протокола Kerberos. 

Дополнительные сведения см. в документе [Настройка Kerberos для IP-адресов](configuring-kerberos-over-ip.md).

## <a name="kdc-support-for-key-trust-account-mapping"></a>Поддержка KDC для сопоставления учетных записей доверия ключей

Начиная с Windows Server 2016, контроллеры домена поддерживают сопоставление учетных записей доверия ключей, а также откат к существующим AltSecID и имени участника-пользователя (UPN) в работе сети SAN. Если Усесубжекталтнаме имеет значение:

- 0: требуется явное сопоставление. В этом случае должно быть одно из следующих:
    - Доверительные отношения ключей (новое в Windows Server 2016)
    - експлиЦиталтсеЦид
- 1: неявное сопоставление разрешено (по умолчанию):
    1. Если для учетной записи настроено доверие ключа, то оно используется для сопоставления (новое в Windows Server 2016).
    2. Если в сети SAN нет имени участника-пользователя, AltSecID пытается выполнить сопоставление.
    3. Если в сети SAN есть имя участника-пользователя, предпринимается предпринятая подстановка имени участника-пользователя.

## <a name="see-also"></a>См. также

- [Обзор проверки подлинности Kerberos](kerberos-authentication-overview.md)
