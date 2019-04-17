---
title: Планирование развертывания постоянно подключенного VPN-профиля
description: В этом разделе приведены планирования инструкции по развертыванию VPN в Windows Server 2016.
ms.prod: windows-server-threshold
ms.technology: networking-ras
ms.topic: article
ms.assetid: 3c9de3ec-4bbd-4db0-b47a-03507a315383
ms.localizationpriority: medium
ms.author: pashort
author: shortpatti
ms.date: 11/05/2018
ms.openlocfilehash: d629f04abda0ce22deb75e487f5b485f50a60a53
ms.sourcegitcommit: 4893d79345cea85db427224bb106fc1bf88ffdbc
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/05/2018
ms.locfileid: "6067486"
---
# Шаг 1. Планирование развертывания VPN

>Область применения: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows 10


& #171;  [ **Предыдущая:** сведения о рабочего процесса развертывания VPN](always-on-vpn-deploy-deployment.md)<br>
& #187;  [ **Далее:** шаг 2. Настройка инфраструктуры сервера](vpn-deploy-server-infrastructure.md)

На этом этапе вы начать планирования и Подготовка к развертыванию вашего VPN. Перед установкой роли сервера удаленного доступа на компьютере, который вы планируете на использование в качестве VPN-сервера необходимо выполните следующие задачи. После правильного планирования можно развертывать VPN и при необходимости настройте условного доступа для подключения к VPN с помощью Azure AD. 

[!INCLUDE [always-on-vpn-standard-config-considerations-include](../../../includes/always-on-vpn-standard-config-considerations-include.md)]


## Подготовка сервера удаленного доступа

Необходимо выполнить следующие действия на компьютере, используемом в качестве VPN-сервера: 

- **Убедитесь, что программное обеспечение сервера VPN и имеет правильную конфигурацию оборудования**. Установите Windows Server 2016 на компьютере, на котором вы планируете использовать в качестве сервера удаленного доступа VPN. Этот сервер должен иметь два физические сетевые адаптеры, один — для подключения к внешним периметра сети и один для подключения к внутренней локальной сети.

- **Определение, какой сетевой адаптер подключается к Интернету и какому сетевому адаптеру подключается к частной сети**. Настройка лицом к Интернету с помощью общего IP-адреса сетевого адаптера, при этом адаптер лицом к интрасети можно использовать IP-адрес из локальной сети.

    >[!TIP]
    >Если вы предпочитаете не следует использовать общий IP-адрес в сети периметра, можно настроить брандмауэр Edge с помощью общего IP-адреса и затем настройте брандмауэр для перенаправления запросов на подключение VPN к серверу VPN.

- **Подключение к сети VPN-сервер**. Установка сервера VPN в сети периметра, между периметра брандмауэр и брандмауэре.

## Планирование методов проверки подлинности

IKEv2 является VPN, описанные в [Internet Engineering Task Force запроса для Comments7296](https://datatracker.ietf.org/doc/rfc7296/)протокол туннелирования. Основным преимуществом IKEv2 является, что он допускает перерывов в основное сетевое подключение. Например, если временный потери соединения или если пользователь перемещает клиентского компьютера одной сети на другой, когда возобновление сетевого подключения IKEv2 восстановления VPN-подключение автоматически, без вмешательства пользователя.

>[!TIP]
>Можно настроить сервер VPN удаленного доступа для поддержки подключений IKEv2 при этом также отключение неиспользуемые протоколов, что сокращает объем памяти системы безопасности сервера. 

## Планирование IP-адресов для удаленных клиентов

Можно настроить VPN-сервер для назначения адресов VPN-клиентам из пула статическим адресом, который вы настроите или IP-адресов от DHCP-сервера. 

## Подготовка среды

- **Убедитесь, что у вас есть разрешения, чтобы настроить внешний брандмауэр и у вас есть действительный общий IP-адрес**. Открытые порты брандмауэра для поддержки VPN-подключений IKEv2. Вам также понадобится общий IP-адрес, чтобы принимать подключения от внешних клиентов.

- **Выбор диапазона статических IP-адресов для VPN-клиентов**. Определите максимальное количество одновременных клиентами VPN, которые вы хотите поддерживать. Кроме того план диапазон статических IP-адресов внутренней локальной сети для соблюдения этого требования, а именно *статический пул адресов*. Если вы используете DHCP для IP-адресов на внутренний промежуточной Подсети, также может потребоваться создать исключение для этих статических IP-адресов в DHCP.

- **Убедитесь, что можно редактировать вашего открытого зоны DNS**. Добавьте записи DNS открытых домена DNS для поддержки инфраструктуры VPN. 

- **Убедитесь, что все пользователи VPN учетные записи пользователей в Active Directory — пользователи \(AD DS\)**. Прежде чем пользователи могут подключаться к сети VPN-подключений, они должны иметь учетные записи пользователей в ДОБАВЛЯЕТ.

## Подготовка маршрутизации и брандмауэра 

Установка сервера VPN в сети периметра, который разделов локальной сети в сети периметра внутренних и внешних. В зависимости от сетевой среды необходимо внести несколько изменений, маршрутизации.

- **Перенаправления портов настроить \(Optional\).** Edge брандмауэра необходимо открыть порты и протоколы кодов, связанных с помощью IKEv2 VPN и перенаправлять их на VPN-сервер. В большинстве сред это требует настраивать перенаправления портов. Перенаправление портов универсальной датаграмм UDP (Protocol) 500 и 4500 VPN-сервер.

- **Настройка маршрутизации, DNS-серверы и серверы VPN могут получить доступ к Интернету**. Это развертывание использует IKEv2 и преобразования сетевых адресов \(NAT\). Убедитесь, что все необходимые внутренних сетей и сетевых ресурсов может связаться с VPN-сервер. Любой сети или ресурсов, недостижимы из VPN-сервер недоступен также VPN-подключений из удаленных расположений.

В большинстве сред для достижения нового внутреннего периметра сети, настройте статические маршруты от края брандмауэра и VPN-сервер. В средах с более сложной тем не менее, вам может потребоваться добавить статические маршруты внутреннего маршрутизаторы или настроить правила внутреннего брандмауэра для VPN-сервера и блок IP-адресов, связанных с клиентами VPN.

## Дальнейшие действия
[Шаг 2. Настройка инфраструктуры сервера](vpn-deploy-server-infrastructure.md): на этом этапе Установка и настройка серверные компоненты, необходимые для поддержки VPN-Подключение. Серверные компоненты включают Настройка инфраструктуры открытых КЛЮЧЕЙ для распространения сертификатов, используемых пользователей, VPN-сервера и сервера политики сети. 

---