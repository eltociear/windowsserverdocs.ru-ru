---
title: Проверка подлинности открытого ключа устройства, присоединенного к домену
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: 7bd17803-6e42-4a3b-803f-e47c74725813
manager: alanth
author: michikos
ms.technology: security-authentication
ms.date: 08/18/2017
ms.openlocfilehash: 80906e7cfe3740200938704a4b4eaf0759af303a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2019
ms.locfileid: "59885035"
---
# <a name="domain-joined-device-public-key-authentication"></a>Проверка подлинности открытого ключа устройства, присоединенного к домену

>Относится к: Windows Server 2016, Windows 10

Kerberos добавлена поддержка для устройств, присоединенных к домену, для входа в систему с использованием в сертификат, начиная с Windows Server 2012 и Windows 8. Это изменение позволяет сторонние поставщики для создания решений для подготовки и инициализации сертификаты для устройств, присоединенных к домену, использовать для проверки подлинности домена. 

## <a name="automatic-public-key-provisioning"></a>Автоматическое открытый подготовки ключей

Начиная с Windows 10 версии 1507 и Windows Server 2016, присоединенных к домену устройств Автоматическая подготовка привязанного открытый ключ к контроллеру домена Windows Server 2016 (DC). После подготовки ключа Windows можно использовать аутентификацию с открытым ключом к домену.

### <a name="public-key-generation"></a>Создание открытого ключа
Если устройство работает под управлением Credential Guard, открытый ключ создается защищать с помощью Credential Guard. 

Если не поддерживается Credential Guard и доверенного платформенного МОДУЛЯ, открытый ключ создается защищенных доверенным платформенным модулем. 

Если ни один, ключ не создается, и устройство можно только проверять подлинность с помощью пароля.

### <a name="provisioning-computer-account-public-key"></a>Подготовка открытый ключ для учетной записи компьютера
При запуске Windows, он проверяет, если открытый ключ будет предоставлен для учетной записи компьютера. Если нет, затем создает связанный открытый ключ и выполняется его настройка для собственной учетной записи AD, используя Windows Server 2016 или более поздней версии контроллера домена. Если все контроллеры домена низкого уровня, ключ не подготавливается.

### <a name="configuring-device-to-only-use-public-key"></a>Настройка устройства на использование только открытый ключ
Если параметр групповой политики **поддержки для проверки подлинности устройства с помощью сертификата** имеет значение **Force**, а затем на устройстве должно для поиска контроллера домена под управлением Windows Server 2016 или более поздней версии для проверки подлинности. Параметр находится в разделе Административные шаблоны > Система > Kerberos.

### <a name="configuring-device-to-only-use-password"></a>Чтобы настроить устройство только использовать пароль
Если параметр групповой политики **поддержки для проверки подлинности устройства с помощью сертификата** отключена, то всегда используется пароль. Параметр находится в разделе Административные шаблоны > Система > Kerberos.

## <a name="domain-joined-device-authentication-using-public-key"></a>Проверка подлинности устройства, присоединенного к домену, с помощью открытого ключа
Когда Windows имеет сертификат для устройства, присоединенного к домену, Kerberos сначала выполняет проверку подлинности с помощью сертификата и о повторных сбоев с паролем. Это позволяет устройству для проверки подлинности на контроллеры домена низкого уровня.

Поскольку автоматически подготовленные открытые ключи самозаверяющий сертификат, сертификат не пройдет проверку на контроллерах домена, которые не поддерживают сопоставление доверие на основе ключей учетной записи. По умолчанию Windows повторяет проверку подлинности с использованием пароля домена устройства.

