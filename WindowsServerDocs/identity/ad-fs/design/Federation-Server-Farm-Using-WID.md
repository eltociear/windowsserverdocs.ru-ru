---
ms.assetid: f775cbda-a75d-439d-9aa7-82f3bc8dc932
title: Ферма серверов федерации с использованием WID
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 926848f9d39a4e00cb30a6bbde5aecee0ef31043
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/08/2020
ms.locfileid: "80853087"
---
# <a name="federation-server-farm-using-wid"></a>Ферма серверов федерации с использованием WID

Топология по умолчанию для службы федерации Active Directory (AD FS) \(AD FS\) является фермой серверов федерации, использующей \(WID внутренней базы данных Windows.\) В этой топологии AD FS использует WID в качестве хранилища для базы данных конфигурации AD FS для всех серверов федерации, присоединенных к этой ферме. Ферма выполняет репликацию и обслуживание данных службы федерации в базе данных конфигурации на всех своих серверах. AD FS в Windows Server 2012 R2 позволяет организациям с 100 или меньшей стороной доверия проверяющей стороны настраивать фермы серверов федерации с помощью WID, а также до 30 серверов.  
  
При создании первого сервера федерации в ферме также создается новая служба федерации. При использовании WID для базы данных конфигурации AD FS первый сервер федерации, созданный в ферме, называется *основным сервером федерации*. Это означает, что на этом компьютере настроено чтение\/запись копии базы данных конфигурации AD FS.  
  
Все другие серверы федерации, настроенные для этой фермы, называются *дополнительными серверами федерации* , так как они должны реплицировать все изменения, сделанные на основном сервере федерации, на чтение\-только копии базы данных конфигурации AD FS, которые хранятся локально.  
  
> [!IMPORTANT]  
> Рекомендуется использовать по крайней мере два сервера федерации в конфигурации с балансировкой нагрузки\-.  
  
## <a name="deployment-considerations"></a>Вопросы развертывания  
В этом разделе описываются различные вопросы о предполагаемой аудитории, преимуществах и ограничениях, связанных с этой топологией развертывания.  
  
### <a name="who-should-use-this-topology"></a>Кто должен использовать эту топологию?  
  
-   Организации с 100 или меньше настроенных отношений доверия, которым необходимо предоставить внутренним пользователям \(вход на компьютеры, физически подключенные к корпоративной сети\) с единым знаком\-на \(единого входа\) доступ к федеративным приложениям или службам.  
  
-   Организации, желающие предоставить своим внутренним пользователям доступ с помощью единого входа к службам Microsoft Online Services или Microsoft Office 365  
  
-   Небольшие организации, требующие избыточных масштабируемых служб  
  
> [!NOTE]  
> Организации с большими базами данных должны использовать [ферму серверов федерации с использованием](Federation-Server-Farm-Using-SQL-Server.md) топологии развертывания SQL Server. Организации с пользователями, которые входят за пределы сети, должны использовать [ферму серверов федерации, использующую топологию WID и учетные записи-посредники](Federation-Server-Farm-Using-WID-and-Proxies.md) или [ферму серверов федерации, используя](Federation-Server-Farm-Using-SQL-Server.md) топологию SQL Server.  
  
### <a name="what-are-the-benefits-of-using-this-topology"></a>Каковы преимущества использования этой топологии?  
  
-   Предоставляет единый доступ к внутренним пользователям  
  
-   Избыточность данных и служба федерации \(каждый сервер федерации реплицирует изменения на другие серверы федерации в той же ферме\)  
  
-   WID входит в состав Windows; Следовательно, нет необходимости покупать SQL Server  
  
### <a name="what-are-the-limitations-of-using-this-topology"></a>Каковы ограничения использования этой топологии?  
  
-   Ферма WID имеет ограничение в 30 серверов федерации, если у вас 100 или меньше отношений доверия проверяющей стороны.  
  
-   Ферма WID не поддерживает определение воспроизведения маркеров или разрешение артефактов \(части язык разметки зявлений системы безопасности (SAML) \(\)протокола SAML\).  
  
Следующая таблица содержит сводку по использованию фермы WID.  Используйте его для планирования реализации.  
  
|| 1 \- 100 отношений доверия RP | Более 100 доверий RP |
| --- | --- | --- |
|1 \- 30 AD FS узлов|Поддерживается для WID|Не поддерживается при использовании WID-SQL 
|Более 30 AD FS узлов|Не поддерживается при использовании WID-SQL|Не поддерживается при использовании WID-SQL  
  
## <a name="server-placement-and-network-layout-recommendations"></a>Рекомендации по размещению и макету сети сервера  
Когда вы будете готовы начать развертывание этой топологии в сети, следует спланировать размещение всех серверов федерации в корпоративной сети за пределами балансировки сетевой нагрузки \(NLB\) узле, который можно настроить для кластера БАЛАНСИРОВКи сетевой нагрузки с выделенной системой доменных имен кластера \(DNS\) имя и IP-адрес кластера.  
  
> [!NOTE]  
> Это DNS-имя кластера должно соответствовать имени служба федерации, например fs.fabrikam.com.  
  
Узел балансировки сетевой нагрузки может использовать параметры, определенные в этом кластере балансировки сетевой нагрузки, для выделения клиентских запросов отдельным серверам федерации. На следующем рисунке показано, как вымышленная компания Fabrikam, Inc. компании настраивает первый этап развертывания с помощью двух\-фермы серверов федерации \(FS1 и FS2\) с WID и размещением DNS-сервера и одного узла балансировки сетевой нагрузки, подключенного к корпоративной сети.  
  
![ферма серверов, использующая WID](media/FarmWID.gif)  
  
> [!NOTE]  
> Если на данном узле балансировки сетевой нагрузки произошел сбой, пользователи не смогут получить доступ к федеративным приложениям или службам. Если требования бизнес-деятельности организации не допускают наличия подобных узких мест, добавьте дополнительные узлы балансировки сетевой нагрузки.  
  
Дополнительные сведения о настройке сетевой среды для использования с серверами федерации см. в разделе Требования к разрешению имен в [AD FS требованиях](AD-FS-Requirements.md).  
  
## <a name="see-also"></a>См. также  
[Планирование топологии развертывания для служб федерации Active Directory](Plan-Your-AD-FS-Deployment-Topology.md)  
[Руководство по разработке служб федерации Active Directory в Windows Server 2012 R2](AD-FS-Design-Guide-in-Windows-Server-2012-R2.md)  
  

