---
ms.assetid: 38c9bcd3-c6f8-4153-8e42-5fd31568c65a
title: Контрольный список — Настройка прокси-сервера федерации
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: c8cd5cbe2ce0c7985a56f8444edfa7c71ee17c2d
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/24/2019
ms.locfileid: "66192349"
---
# <a name="checklist-setting-up-a-federation-server-proxy"></a>Контрольный список: Настройка прокси-сервера федерации

Этот контрольный список содержит задачи развертывания для подготовки сервера под управлением Windows Server® 2012 роль прокси-сервера федерации в службах федерации Active Directory \(AD FS\).  
  
> [!NOTE]  
> Выполните по порядку задачи в контрольном списке. После выполнения всех шагов процедуры, на которую указывает ссылка, следует вернуться к этому разделу и продолжить выполнение оставшихся задач контрольного списка.  
  
![Настройка федеративной прокси-сервер](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)**контрольный список: Настройка прокси-сервера федерации**  
  
||Задача|Ссылка|  
|-|--------|-------------|  
|![Настройка федеративной прокси-сервер](media/icon_checkboxo.gif)|Перед началом развертывания прокси-сервера федерации AD FS, просмотрите типы топологии развертывания AD FS и их размещения связанного сервера и рекомендациях макета.|![Настройка федеративной прокси-сервер](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[определение топологии развертывания AD FS](https://technet.microsoft.com/library/gg982491.aspx)<br /><br />![Настройка федеративной прокси-сервер](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[планирование размещения прокси-сервера федерации](https://technet.microsoft.com/library/dd807130.aspx)<br /><br />![Настройка федеративной прокси-сервер](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Where to Place a Federation Server Proxy](https://technet.microsoft.com/library/dd807048.aspx)|  
|![Настройка федеративной прокси-сервер](media/icon_checkboxo.gif)|Просмотрите руководство по планированию AD FS ресурсов, чтобы определить нужное число прокси-серверов федерации, который следует использовать в рабочей среде.|![Настройка федеративной прокси-сервер](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Планирование емкости прокси-сервера федерации](https://technet.microsoft.com/library/gg749898.aspx)|  
|![Настройка федеративной прокси-сервер](media/icon_checkboxo.gif)|Определите, является лучшим для развертывания прокси-сервера федерации единый или ферму прокси-сервера федерации. **Примечание.** Серверы федерации также выполнять обязанности прокси сервера федерации.|![Настройка федеративной прокси-сервер](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[When to Create a Federation Server Proxy](https://technet.microsoft.com/library/dd807032.aspx)<br /><br />![Настройка федеративной прокси-сервер](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[когда следует создавать ферму прокси-сервера федерации](https://technet.microsoft.com/library/dd807082.aspx)|  
|![Настройка федеративной прокси-сервер](media/icon_checkboxo.gif)|Определите, будет ли создан этот прокси-сервера федерации в сети периметра организации партнера по учетным записям или организации партнера по ресурсам.|![Настройка федеративной прокси-сервер](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[сведения о роли прокси-сервера федерации в организации партнера по учетной записи](https://technet.microsoft.com/library/dd807109.aspx)<br /><br />![Настройка федеративной прокси-сервер](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[сведения о роли прокси-сервера федерации в организации партнера по ресурсам](https://technet.microsoft.com/library/dd807052.aspx)|  
|![Настройка федеративной прокси-сервер](media/icon_checkboxo.gif)|Перед установкой AD FS на компьютере, который должен стать прокси-сервера федерации, узнайте о важности получения сертификата проверки подлинности сервера, для ферм прокси сервера федерации — Добавление или совместного использования сертификатов на всех серверах в ферме.|![Настройка федеративной прокси-сервер](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[требования к сертификатам для прокси-серверов федерации](https://technet.microsoft.com/library/dd807054.aspx)|  
|![Настройка федеративной прокси-сервер](media/icon_checkboxo.gif)|Просмотрите сведения в AD FS Design Guide об обновлении доменных имен \(DNS\) в сети периметра, поэтому может возникнуть, успешное разрешение имен для серверов федерации и прокси-серверов федерации.|![Настройка федеративной прокси-сервер](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[требования к разрешению имен для прокси-серверов федерации](https://technet.microsoft.com/library/dd807055.aspx)|  
|![Настройка федеративной прокси-сервер](media/icon_checkboxo.gif)|Определите, является ли прокси-сервера федерации должен быть присоединен к домену. Несмотря на то, что прокси-серверов федерации, присоединенных к домену не требуется, их можно было легко управлять с помощью удаленного администрирования и возможности групповой политики, когда они присоединены к домену.|![Настройка федеративной прокси-сервер](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[присоединить компьютер к домену](Join-a-Computer-to-a-Domain.md)|  
|![Настройка федеративной прокси-сервер](media/icon_checkboxo.gif)|В зависимости от настроек инфраструктуры DNS в сети периметра выполните одно из процедуры, описанные в разделах справа до развертывания прокси-сервера федерации в вашей организации. **Примечание.** Обе процедуры выполнять не нужно. Чтение [требования к разрешению имен для прокси-серверов федерации](https://technet.microsoft.com/library/dd807055.aspx) для определения, какие процедуры наиболее подходящий требованиям вашей организации.|![Настройка федеративной прокси-сервер](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[настроить разрешение имен для прокси-сервера федерации в зону DNS, который обслуживает только сеть периметра](Configure-Name-Resolution-for-a-Federation-Server-Proxy-in-a-DNS-Zone-That-Serves-Only-the-Perimeter-Network.md)<br /><br />![Настройка федеративной прокси-сервер](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[настроить разрешение имен для прокси-сервера федерации в DNS зоны, обслуживает как сети периметра и Интернет-клиентов](Configure-Name-Resolution-for-a-Federation-Server-Proxy-in-a-DNS-Zone-That-Serves-Both-the-Perimeter-Network-and-Internet-Clients.md)|  
|![Настройка федеративной прокси-сервер](media/icon_checkboxo.gif)|После получения сертификата проверки подлинности сервера необходимо установить его в службах IIS \(IIS\) веб-сайте по умолчанию прокси-сервера федерации.|![Настройка федеративной прокси-сервер](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[Импорт сертификата аутентификации сервера на веб-сайт по умолчанию](Import-a-Server-Authentication-Certificate-to-the-Default-Web-Site.md)|  
|![Настройка федеративной прокси-сервер](media/icon_checkboxo.gif)|\(Необязательный\) в качестве альтернативы для получения сертификата проверки подлинности сервера из центра сертификации \(ЦС\), IIS можно использовать для получения примера сертификат для вашего прокси-сервера федерации.<br /><br />Так как IIS создает самостоятельно\-подписанном сертификате, которое не берутся из надежного источника, использовать его для создания самозаверяющего\-сертификат только в следующих сценариях:<br /><br />— Если необходимо создать Secure Sockets Layer \(SSL\) канал между сервером и ограниченный, известные группы пользователей<br />-При наличии для устранения неполадок в-третьих\-проблем с сертификатами сторона **осторожность:** Это не рекомендуется безопасности для развертывания прокси-сервера федерации в рабочей среде с помощью самостоятельно\-со знаком, сертификат проверки подлинности сервера.|![Настройка федеративной прокси-сервер](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[IIS: Создать самозаверяющий\-самозаверяющему сертификату сервера](https://go.microsoft.com/fwlink/?LinkID=108271)|  
|![Настройка федеративной прокси-сервер](media/icon_checkboxo.gif)|Установка службы роли прокси-сервера службы федерации на компьютере, который должен стать прокси-сервера федерации.|![Настройка федеративной прокси-сервер](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[Установка роли прокси-сервера для службы федерации](Install-the-Federation-Service-Proxy-Role-Service.md)|  
|![Настройка федеративной прокси-сервер](media/icon_checkboxo.gif)|Настройте программное обеспечение AD FS на компьютере, чтобы выступать в роли прокси-сервера федерации с помощью мастера конфигурации прокси-сервера AD FSFederation.|![Настройка федеративной прокси-сервер](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[Настройка компьютера для роли прокси-сервера федерации](Configure-a-Computer-for-the-Federation-Server-Proxy-Role.md)|  
|![Настройка федеративной прокси-сервер](media/icon_checkboxo.gif)|В средстве просмотра событий убедитесь, что служба прокси-сервера федерации была запущена.|![Настройка федеративной прокси-сервер](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[убедитесь, что Federation Server функционирования прокси-](Verify-That-a-Federation-Server-Proxy-Is-Operational.md)|  