---
ms.assetid: 8be8c48d-790c-4199-b9d3-9f4a07d5ced2
title: Сбор сведений о сети
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/08/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 6792d565e08a188e1957c67ce419676d4a044d82
ms.sourcegitcommit: 11421f4005f9f3a3f6c0db95b1836d0f765a9fa3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2020
ms.locfileid: "81624392"
---
# <a name="collecting-network-information"></a>Сбор сведений о сети

> Область применения. Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Первый шаг в проектировании эффективной топологии сайтов в домен Active Directory Services (AD DS) заключается в том, чтобы обратиться в сетевую группу Организации для получения информации и регулярно взаимодействовать с ними о топологии физической сети.

## <a name="creating-a-location-map"></a>Создание схемы расположения

Создайте карту расположения, которая представляет физическую сетевую инфраструктуру вашей организации. На карте расположения Найдите географические расположения, содержащие группы компьютеров с внутренним подключением по 10 мегабит в секунду (Мбит/с) или выше (локальная сеть) или более поздней версии.

## <a name="listing-communication-links-and-available-bandwidth"></a>Перечисление каналов связи и доступная пропускная способность

После создания схемы расположения Задокументируйте тип канала связи, скорость связи и доступную полосу пропускания между каждым расположением. Получение топологии глобальной сети (WAN) из сетевой группы. Список распространенных типов каналов WAN и их пропускной способности см. в разделе "определение затрат" статьи [Создание структуры связи сайтов](../../ad-ds/plan/Creating-a-Site-Link-Design.md). Эти сведения понадобятся вам для создания связей сайтов позже в процессе разработки топологии сайта.

Пропускная способность относится к объему данных, которые можно передавать по каналу связи за определенный промежуток времени. Доступная пропускная способность — это объем пропускной способности, фактически доступный для использования AD DS. Вы можете получить доступ к сведениям о пропускной способности из сетевой группы или проанализировать трафик по каждому каналу с помощью анализатора протокола, например сетевой монитор. Сведения об установке сетевой монитор см. в статье [мониторинг сетевого трафика](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc783075(v=ws.10)).

Документировать каждое расположение и другие связанные с ним расположения. Кроме того, запишите тип канала связи и доступную пропускную способность. Лист, помогающий в составлении списка каналов связи и доступной пропускной способности, см. в разделе [вспомогательные материалы для Windows Server 2003 Deployment Kit](https://microsoft.com/download/details.aspx?id=9608), скачайте Job_Aids_Designing_and_Deploying_Directory_and_Security_Services. zip и откройте "географические расположения и каналы связи" (DSSTOPO_1. doc).

## <a name="listing-ip-subnets-within-each-location"></a>Вывод списка IP-подсетей в каждом расположении

После документирования каналов связи и доступной пропускной способности между ними запишите IP-подсети в каждом расположении. Если вы еще не знакомы с маской подсети и IP-адресом в каждом расположении, обратитесь к сетевой группе.

AD DS связывает рабочую станцию с сайтом, сравнивая IP-адрес рабочей станции с подсетями, связанными с каждым сайтом. При добавлении контроллеров домена в домен AD DS также проверяет их IP-адреса и помещает их на самый подходящий сайт.

Сведения о том, как получить список IP-подсетей в каждом расположении, см. в статье [вспомогательные программы для Windows Server 2003 Deployment Kit](https://microsoft.com/download/details.aspx?id=9608), скачайте Job_Aids_Designing_and_Deploying_Directory_and_Security_Services. zip и откройте папку "расположения и подсети" (DSSTOPO_2. doc).

> [!NOTE]
> Кроме адресов IP версии 4 (IPv4), Windows Server также поддерживает префиксы подсети IP версии 6 (IPv6). Сведения о том, как получить список префиксов подсети IPv6, см. в [приложении а. расположение и префиксы подсети](../../ad-ds/plan/Appendix-A--Locations-and-Subnet-Prefixes.md).

## <a name="listing-domains-and-number-of-users-for-each-location"></a>Вывод списка доменов и числа пользователей для каждого расположения

Число пользователей для каждого регионального домена, представленное в расположении, является одним из факторов, определяющих размещение региональных контроллеров домена и серверов глобального каталога, что является следующим шагом в процессе разработки топологии сайта. Например, запланируйте размещение регионального контроллера домена в расположении, содержащем более 100 пользователей регионального домена, чтобы они могли войти в домен в случае сбоя подключения к глобальной сети.

Запишите расположения, домены, представленные в каждом расположении, и число пользователей для каждого домена, представленного в каждом расположении. Сведения о том, как получить список доменов и число пользователей, представленных в каждом расположении, см. в разделе [вспомогательные программы для Windows Server 2003 Deployment Kit](https://microsoft.com/download/details.aspx?id=9608), скачайте Job_Aids_Designing_and_Deploying_Directory_and_Security_Services. zip и откройте "домены и пользователи в каждом расположении" (DSSTOPO_3. doc).
