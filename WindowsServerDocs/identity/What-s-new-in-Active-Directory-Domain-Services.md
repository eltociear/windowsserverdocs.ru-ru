---
ms.assetid: 9a06cd41-426f-4cb9-89cf-f5be730e0b79
title: Что&#39;возможности доменных служб Active Directory
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.service: ''
ms.suite: na
ms.technology: active-directory-domain-services
ms.tgt_pltfrm: na
ms.topic: article
author: Femila
ms.author: billmath
ms.date: 05/31/2017
ms.openlocfilehash: ffa8bcb43b17ae8779c70d499bff27a8f77cce75
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2019
ms.locfileid: "59841335"
---
# <a name="what39s-new-in-active-directory-domain-services"></a>Что&#39;возможности доменных служб Active Directory 

>Область применения. Windows Server 2016

Следующие новые функции в доменных службах Active Directory (AD DS) улучшить возможность для организаций для защиты сред Active Directory и помочь им перейти облачных развертываниях и гибридных развертываний, где находятся некоторых приложений и служб размещенные в облаке и другие размещены в локальной среде. В усовершенствования входит:  
  
-   [Управление привилегированным доступом](https://technet.microsoft.com/library/mt150258.aspx   
)  
  
- [Использование возможностей облачных служб на устройствах Windows 10 с помощью присоединения Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-azureadjoin-overview/)   
  
- [Подключение присоединенных к домену устройств к Azure AD для Windows 10 возникает](https://azure.microsoft.com/documentation/articles/active-directory-azureadjoin-devices-group-policy/)   
  
- [Включение Microsoft Passport for Work в организации](https://azure.microsoft.com/documentation/articles/active-directory-azureadjoin-passport-deployment/)    
  
-  [Устаревание функциональные уровни службы репликации файлов (FRS) и Windows Server 2003](ad-ds/active-directory-functional-levels.md)  
  
  
## <a name="BKMK_PAM"></a>Управление привилегированным доступом  
Управление привилегированным доступом (PAM) помогает снизить безопасность проблемы для сред Active Directory, вызванные учетных данных способов кражи таких pass--hash, относятся и аналогичных типах атак. Он предоставляет новое решение административного доступа, настроенного с помощью Microsoft Identity Manager (MIM). PAM предоставляет:  
  
-   Новый бастиона леса Active Directory, которая подготавливается с MIM. Лесу-бастионе имеет специальные доверия PAM с существующим лесом. Он предоставляет новой среды Active Directory, который известен свободную от любого вредоносных действий и его изоляцией от существующего леса для использования привилегированных учетных записей.  
  
-   Новые процессы в MIM, чтобы запросить права администратора, а также на утверждение запросов на основе новых рабочих процессов.  
  
-   Новые теневые субъекты безопасности (группы), которые были подготовлены в лесу-бастионе диспетчером MIM в ответ на запросы с правами администратора. Субъекты безопасности тени иметь атрибут, который ссылается на идентификатор безопасности административной группы в существующем лесу. Это позволяет теневую группу для доступа к ресурсам в существующем лесу без изменения все списки управления доступом (ACL).  
  
-   Истечение срока действия связывает функцию, которая позволяет привязкой по времени членство в группе тени. Время, которое требуется выполнить административную задачу можно добавить пользователя в группу. Членство привязанный ко времени выражается значение времени жизни (TTL), передается жизни билета Kerberos.  
  
    > [!NOTE]  
    > Срок действия которых истекает ссылки доступны на всех связанных атрибутов. Однако связанный атрибут члена/memberOf отношение между группой и пользователя — это только пример где законченное решение, например PAM настраивается заранее, чтобы использовать функцию с истекающим сроком действия ссылки.  
  
-   Усовершенствования KDC встроены в контроллеры домена Active Directory, чтобы ограничить срок действия билета Kerberos наименьшее возможное время жизни (TTL) значение в случаях, когда пользователь состоит в нескольких группах привязанный ко времени в административных группах. Например если он будет добавлен в привязанный ко времени группы A, то при входе в систему, время существования билета предоставления билета (TGT) Kerberos будет равно времени у вас есть оставшихся в группе A. Если вы также являетесь членом другой группы привязанный ко времени B, который имеет меньшее значение TTL, чем группы A, то время жизни TGT равно времени, который остался в группе B.  
  
-   Новые возможности мониторинга, к чему вы можете легко определить, кто запросили доступ, какой доступ к предоставлен и какие действия были выполнены.  
  
**Требования к**  
  
-   Диспетчер удостоверений (Майкрософт)  
  
-   Active Directory режим работы леса Windows Server 2012 R2 или более поздней версии.  
  
## <a name="BKMK_AzureADJoin"></a>Присоединение к Azure AD  
Active Directory присоединение к Azure расширяет возможности идентификации, внося для предприятия, бизнеса и для образовательных Учреждений клиентов - улучшенные возможности для корпоративных и персональных устройств.  
  
Преимущества:  
  
-   **Доступности, современный параметров** на устройства, принадлежащие corp Windows. Кислорода службы больше не требуют личную учетную запись Майкрософт: они теперь выходящих за пределы существующие рабочие учетные записи пользователей для обеспечения соответствия. Кислорода службы будут работать на ПК, присоединенных к домену Windows на локальном, и ПК и устройств, которые «присоединены» для вашего клиента Azure AD («облачный домен»). К ним относятся:  
  
    -   Перемещение или персонализации, параметры специальных возможностей и учетные данные  
  
    -   Резервное копирование и восстановление  
  
    -   Доступ к Microsoft Store с помощью рабочей учетной записи  
  
    -   Живые плитки и уведомления  
  
-   **Доступ к ресурсам организации** на мобильных устройствах (телефонах, планшетофоны), которые невозможно присоединить к домену Windows, являются ли они корпоративные или BYOD  
  
-   **Единый вход** для Office 365 и другим корпоративным приложениям, веб-сайтов и ресурсов.  
  
-   **На устройствах BYOD**, добавить рабочую учетную запись (из локального домена или Azure AD) на устройстве личных и используется единый вход для работы ресурсам, с помощью приложений, так и в Интернете, образом, чтобы обеспечить соответствие с новыми возможностями, например условного учетной записи Элемент управления и работоспособность устройств аттестации.  
  
-   **Интеграция MDM** позволяет автоматически регистрировать устройства для управления Мобильными (Intune или стороннего)  
  
-   **Настройка режима «Киоск» и общие устройства** для нескольких пользователей в вашей организации  
  
-   **Опыт разработки** позволяет создавать приложения, предназначенных для корпоративных и личных контекстах с общего программирования стека.  
  
-   **Imaging** можно выбрать между работы с образами и дает возможность пользователям для настройки устройств, принадлежащих corp непосредственно во время первого запуска.  
  
Дополнительные сведения см. [Windows 10 для предприятия: Использование устройств для работы](https://azure.microsoft.com/documentation/articles/active-directory-azureadjoin-windows10-devices-overview/?rnd=1).  
  
## <a name="BKMK_IDLocker"></a>Microsoft Passport  
Microsoft Passport — это новый сеанс аутентификации на основе ключей подход организаций и потребителей, которые выходит за рамки пароли. Такая форма проверки подлинности зависит от нарушения, кражи и устойчивость ловят учетные данные.  
  
Входе в систему на устройстве с журналом биометрические или ПИН-код на информацию, связанную с сертификатом или асимметричной парой ключей. Поставщики удостоверений (IDP) проверки пользователя путем сопоставления открытого ключа пользователя с IDLocker, а также журнала по информации через один одноразового пароля (OTP), Phonefactor или иного механизма уведомления.  
  
Дополнительные сведения см. [проверка подлинности удостоверений без использования паролей с помощью службы Microsoft Passport](https://azure.microsoft.com/documentation/articles/active-directory-azureadjoin-passport/)  
  
## <a name="BKMK_FRSDeprecation"></a>Устаревание функциональные уровни службы репликации файлов (FRS) и Windows Server 2003  
Несмотря на то, что служба репликации файлов (FRS) и режимы работы Windows Server 2003 устарели в предыдущих версиях Windows Server, это стоит повторить особо операционной системы Windows Server 2003 больше не поддерживается. Таким образом любой контроллер домена под управлением Windows Server 2003 должны удаляться из домена. Режим работы домена и леса должен быть повышен до по крайней мере Windows Server 2008, чтобы контроллер домена, под управлением более ранней версии Windows Server будут добавляться в среду.  
  
В Windows Server 2008 и более поздней версии режимы работы домена репликации распределенной файловой службы (DFS) используется для репликации содержимого папки SYSVOL между контроллерами домена. При создании нового домена в режиме работы домена Windows Server 2008 или более поздней версии, служба репликации DFS автоматически используется для репликации SYSVOL. Если вы создали домен на более низком функциональном уровне, необходимо будет переход от средств FRS на DFS для SYSVOL. Этапы миграции, вы можете либо выполните [процедуры на сайте TechNet](https://technet.microsoft.com/library/dd640019(v=WS.10).aspx) или можно ссылаться на [упрощенная схема набор шагов в блоге CAB-файла группы хранения](http://blogs.technet.com/b/filecab/archive/2014/06/25/streamlined-migration-of-frs-to-dfsr-sysvol.aspx).  
  
Windows Server 2003 леса функциональные уровни домена и по-прежнему поддерживаются, но организации должны повысить режим работы на Windows Server 2008 (или более поздней версии, если это возможно) для обеспечения совместимости репликации SYSVOL и поддерживать в будущем. Кроме того доступны многие другие преимущества и возможности на более функциональной более поздней версии. Дополнительную информацию можно найти в следующих ресурсах:  
  
-   [Основные сведения о домене Active Directory Services (AD DS) режимы работы](ad-ds/active-directory-functional-levels.md)  
  
-   [Повышение режима работы домена](https://technet.microsoft.com/library/cc753104.aspx)  
  
-   [Повышение режима работы леса](https://technet.microsoft.com/library/cc730985.aspx)  
  