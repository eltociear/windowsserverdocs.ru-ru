---
ms.assetid: 204f5fe9-3611-4da0-b057-a386004b4598
title: Основные сведения о федерации ключей Active Directory основные понятия служб
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: ac666539170bb7aabf0b7f58a7ef003ebe87c2a8
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/24/2019
ms.locfileid: "66188391"
---
# <a name="understanding-key-ad-fs-concepts"></a>Общие сведения о ключевых понятиях AD FS
Рекомендуется, чтобы узнать о важных концепциях для служб федерации Active Directory и ознакомиться с набором функций.  
  
> [!TIP]  
> Ссылки на дополнительные материалы по AD FS 2.0 см. на странице [карты содержимого разделов](https://social.technet.microsoft.com/wiki/contents/articles/2735.aspx) на вики-сайте Microsoft TechNet. Эту страницу ведут участники сообщества AD FS и регулярно проверяют сотрудники группы разработки AD FS.  
  
## <a name="ad-fs-terminology-used-in-this-guide"></a>Термины AD FS, употребляемые в этом руководстве  
  
|Термин AD FS|Определение|  
|--------------|--------------|  
|Партнерская организация по учетным записям|Партнерская организация по федерации, представляемая в службе федерации отношениями доверия поставщика утверждений. Организации партнера по учетным записям содержит пользователей, которые будет доступ к веб-\-приложениям в организации партнера по ресурсам.|  
|Сервер федерации учетных записей.|Сервер федерации в партнерской организации по учетным записям. Сервер федерации по учетным записям издает маркеры безопасности пользователям на основе аутентификации пользователей. Сервер проверяет подлинность пользователя, извлекает соответствующие атрибуты и сведения о членстве в группах из хранилища атрибутов, упаковывает эту информацию в утверждения и создает и подписывает маркер безопасности \(которого содержит утверждения\)для возврата пользователю, либо для использования в его собственной организации или отправки в партнерскую организацию.|  
|База данных конфигурации AD FS|База данных, используемая для хранения всех данных конфигурации, которые представляют отдельный экземпляр AD FS или службу федерации. Эти данные конфигурации, которые могут храниться в любой базе данных SQL Server или с помощью функции внутренней базы данных Windows в состав Windows Server 2016, Windows Server 2012 и 2012 R2 и Windows Server 2008 и 2008 R2. </br></br>Можно создать базу данных конфигурации AD FS для SQL Server, с помощью команды Fsconfig.exe\-линия и для Windows с помощью мастера настройки сервера AD FS федерации внутренней базы данных.|  
|Поставщик утверждений|Организация, поставляющая утверждения своим пользователям. См. партнерскую организацию по учетным записям.|  
|Отношения доверия с поставщиком утверждений|В консоли управления AD FS\-, утверждения, отношения доверия с поставщиком доверия объекты обычно создаются в партнерских организациях по ресурсам для представления организации во взаимоотношениях доверия, учетные записи которых будут осуществлять доступ к ресурсам в ресурсе партнерской организации. Объект доверия поставщика утверждений состоит из разных идентификаторов, имен и правил, идентифицирующих этого партнера в локальной службе федерации.|  
|Отношения доверия с локальным поставщиком утверждений|Объект доверия, представляющий AD LDS или третьим\-лицам LDAP\-на основе каталогов в ферму AD FS. Доверия локального поставщика утверждений состоит из разных идентификаторов, имен и правил, идентифицирующих этого LDAP\-каталоге в локальную службу федерации на основе.|  
|Метаданные федерации|Формат данных для передачи сведений о конфигурации между поставщиком утверждений и проверяющей стороной с целью правильной настройки отношений доверия поставщика утверждений и отношений доверия проверяющих сторон. Формат данных определяется в Security Assertion Markup Language \(SAML\) 2.0 и расширяется в WS\-федерации.|  
|Сервер федерации|Windows Server, который был настроен с помощью мастера конфигурации сервера AD FS федерации для работы в роли сервера федерации. Сервер федерации издает маркеры и функционирует как часть службы федерации|  
|Прокси-сервер федерации|Windows Server, который был настроен с помощью AD FS прокси-сервера мастер настройки сервера федерации в качестве промежуточной прокси-класса службы между Интернет-клиентом и службой федерации, расположенной за пределами брандмауэра в корпоративной сети.|  
|Основной сервер федерации|Windows Server, настроенный в роли сервера федерации, с помощью мастера конфигурации сервера AD FS федерации и имеет чтения\/записи копию базы данных конфигурации AD FS. </br></br> Основной сервер федерации создается при использовании мастера конфигурации федерации сервера AD FS и выберите параметр для создания новой службы федерации и сделать этот компьютер первого сервера федерации в ферме. Все остальные серверы федерации на этой ферме должны реплицировать изменения, внесенные на основном сервере федерации для чтения\-копию базы данных конфигурации AD FS, которая хранится локально. Термин "основной сервер федерации" неприменим, если база данных конфигурации AD FS хранится в базе данных SQL, поскольку все серверы федерации могут в равной степени считывать и осуществлять запись в базу данных конфигурации, хранимой на SQL Server.|  
|Проверяющая сторона|Организация, получающая и обрабатывающая утверждения. См. партнерскую организацию по ресурсам.|  
|Отношения доверия с проверяющей стороной|В консоли управления AD FS\-, доверия с проверяющей стороной, объекты доверия, которые обычно создаются:<br /><br />-Учетная запись партнерских организаций для представления организации во взаимоотношениях доверия, учетные записи которых будут осуществлять доступ к ресурсам в партнерской организации по ресурсам.<br />-Партнерских организациях по ресурсам для представления отношения доверия между службой федерации и один веб-узел\-приложения на основе.<br /><br />Объект доверия проверяющей стороны состоит из разных идентификаторов, имен и правил, идентифицирующих этого партнера или веб-\-приложения к локальной службе федерации.|  
|Сервер федерации ресурсов|Сервер федерации в партнерской организации по ресурсам. Сервер федерации ресурсов, как правило, издает маркеры безопасности пользователям на основании маркера безопасности, изданного сервером федерации учетных записей. Сервер получает маркер безопасности, проверяет подпись, применяет логику правил утверждений в работе утверждения для создания нужные исходящие утверждения, создает новый маркер безопасности \(с исходящими утверждениями\) на основе информации во входящем маркере безопасности и подписывает новый маркер для возвращения пользователю и в конечном счете веб-приложению.|  
|Партнерская организация по ресурсам|Партнер по федерации, представляемый в службе федерации отношениями доверия с проверяющей стороной. Партнер по ресурсам издает утверждений\-на основе маркеров безопасности, которые содержит опубликованные веб-\-приложений, доступных пользователям в организации партнера по учетной записи.|  
  
## <a name="overview-of-ad-fs"></a>Обзор AD FS  
AD FS представляет это решение доступа удостоверение, обеспечивающее для клиентских компьютеров \(внутренним или внешним по отношению к вашей сети\) простого единого входа для доступа к защищенные Internet\-для Интернета, приложениям или службам, даже если учетные записи пользователей и приложения находятся в совершенно разных сетях или организациях.  
  
Если приложение или служба находятся в одной сети, а учетная запись пользователя — в другой, пользователю, как правило, приходится вводить дополнительные учетные данные при попытке доступа к приложению или службе. Эти дополнительные учетные данные представляют удостоверение пользователя в области нахождения приложения или службы. Их ввода обычно требует веб-сервер, на котором размещено приложение или служба, для принятия наиболее взвешенного решения об авторизации.  
  
С AD FS, организации могут обходить запросы ввода дополнительных учетных данных путем создания отношений доверия \(отношения доверия федерации\) , эти организации можно использовать для проекта пользователя цифровыми удостоверениями и доступом правами надежным партнеры. В федерированной среде каждая организация управляет своими собственными удостоверениями. При этом каждая может безопасно проецировать и принимать удостоверения от других организаций.  
  
-   [Роль хранилищ атрибутов](The-Role-of-Attribute-Stores.md)  
  
-   [Роль базы данных конфигурации AD FS](The-Role-of-the-AD-FS-Configuration-Database.md).  
  
-   [Роль утверждений](The-Role-of-Claims.md)  
  
-   [Роль правил утверждений](The-Role-of-Claim-Rules.md)  
  
-   [Роль механизма утверждений](The-Role-of-the-Claims-Engine.md)  
  
-   [Роль канала утверждений](The-Role-of-the-Claims-Pipeline.md)  
  
-   [Роль языка правил утверждений](The-Role-of-the-Claim-Rule-Language.md)  
  
-   [Определения типа шаблона правил утверждений](Determine-the-Type-of-Claim-Rule-Template-to-Use.md)  
  
-   [Использование универсальных кодов ресурсов (URI) в AD FS](How-URIs-Are-Used-in-AD-FS.md)  
  
