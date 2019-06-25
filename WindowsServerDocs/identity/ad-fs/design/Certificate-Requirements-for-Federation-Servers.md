---
ms.assetid: 9831b421-8fb7-4e15-ac27-c013cbca6d05
title: Требования к сертификатам для серверов федерации
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: ce301f6320ed3347b1ee802f57c2b2ebd4394970
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/24/2019
ms.locfileid: "66191637"
---
# <a name="certificate-requirements-for-federation-servers"></a>Требования к сертификатам для серверов федерации

В любой службы федерации Active Directory \(AD FS\) разработки, необходимо использовать различные сертификаты для защиты обмена данными и обеспечения проверки подлинности пользователей между Интернет-клиентами и серверами федерации. Каждый сервер федерации должен иметь сертификат взаимодействия служб и маркер\-сертификата для подписи до ее включения в связь службы федерации Active Directory. В следующей таблице описаны типы сертификатов, которые связаны с сервером федерации.  
  
|Тип сертификата|Описание|  
|--------------------|---------------|  
|Токен\-сертификат для подписи|Токен\-сертификат для подписи является x X509 сертификата. Серверы федерации используют связанные public\/закрытый пары ключей для цифровой подписи все издаваемые ими маркеры безопасности. Сюда относится подписывание опубликованных метаданных федерации и запросов на разрешение артефактов.<br /><br />У вас есть несколько токен\-подписи сертификаты, настроенные в консоли управления AD FS\-чтобы сделать возможной смену сертификатов, когда приближается истечение срока действия один сертификат. По умолчанию публикуются все сертификаты в списке, но только основной маркер\-сертификат для подписи используется службами AD FS для подписи токенов. Все выбранные сертификаты должны иметь соответствующий закрытый ключ.<br /><br />Дополнительные сведения см. в статьях [Token-Signing Certificates](Token-Signing-Certificates.md) и [Add a Token-Signing Certificate](../../ad-fs/deployment/Add-a-Token-Signing-Certificate.md).|  
|Сертификат взаимодействия служб|Серверы федерации используют сертификат проверки подлинности сервера, также известный как сертификат взаимодействия служб для Windows Communication Foundation \(WCF\) безопасность сообщений. По умолчанию, это тот же сертификат, который использует сервер федерации в качестве Secure Sockets Layer \(SSL\) сертификата в службах IIS \(IIS\). **Примечание.** Оснастка управления AD FS\-в расценивает сертификаты проверки подлинности серверов для серверов федерации как сертификаты взаимодействия служб.<br /><br />Дополнительные сведения см. в разделе [сертификаты взаимодействия служб](Service-Communications-Certificates.md) и [набор сертификата связи со службой](../../ad-fs/deployment/Set-a-Service-Communications-Certificate.md).<br /><br />Так как сертификат взаимодействия служб должны доверять клиентские компьютеры, мы рекомендуем использовать сертификат, подписанный доверенным центром сертификации \(ЦС\). Все выбранные сертификаты должны иметь соответствующий закрытый ключ.|  
|Secure Sockets Layer \(SSL\) сертификата|Серверы федерации используют сертификат SSL для обеспечения безопасности трафика веб-служб при обмене данными SSL с веб-клиентами и прокси-серверами федерации.<br /><br />Поскольку сертификату SSL должны доверять клиентские компьютеры, рекомендуется использовать сертификат, подписанный доверенным центром сертификации. Все выбранные сертификаты должны иметь соответствующий закрытый ключ.|  
|Токен\-сертификат расшифровки|Этот сертификат используется для расшифровки токенов, полученных этим сервером федерации.<br /><br />Можно использовать несколько сертификатов расшифровки. Это позволяет сервер федерации ресурсов не может расшифровывать токены, выданные с более старым сертификатом после настройки нового сертификата в качестве основного сертификата расшифровки. Все сертификаты, которые могут использоваться для расшифровки, однако только основной маркер\-расшифровки сертификата фактически публикуется в метаданных федерации. Все выбранные сертификаты должны иметь соответствующий закрытый ключ.<br /><br />Дополнительные сведения см. в разделе [добавить сертификат расшифровки маркера](../../ad-fs/deployment/Add-a-Token-Decrypting-Certificate.md).|  
  
Можно запросить и установить SSL-сертификат или сертификат взаимодействия служб, запрашивая сертификат взаимодействия служб через консоль управления \(MMC\) привязать\-в для служб IIS. Более общие сведения об использовании сертификатов SSL см. в разделе [IIS 7.0: Настройка SSL в IIS 7.0](https://go.microsoft.com/fwlink/?LinkID=108544) и [IIS 7.0: Настройка сертификатов сервера в IIS 7.0](https://go.microsoft.com/fwlink/?LinkID=108545) .  
  
> [!NOTE]  
> В AD FS вы можете изменить безопасного хэш-алгоритма \(SHA\) уровень, используемый для цифровых подписей для либо SHA\-1 или SHA\-256 \(безопаснее\). AD FSdoes не поддерживает использование сертификатов с другими хэш-методами, такими как MD5 \(хэш-алгоритм по умолчанию, который используется с командой Makecert.exe\-линия\). По соображениям безопасности рекомендуется использовать SHA\-256 \(которого имеет значение по умолчанию\) для всех подписей. SHA\-1 рекомендуется использовать только в сценариях, в которых требуется взаимодействие с продуктом, не поддерживает обмен данными по алгоритму SHA\-256, например непустой\-продукт Майкрософт или AD FS 1. *x*.  
  
## <a name="determining-your-ca-strategy"></a>Определение стратегии центра сертификации  
AD FS не требует издания сертификатов центром сертификации. Тем не менее SSL-сертификат \(сертификат, который также используется по умолчанию в качестве сертификата взаимодействия служб\) должны доверять клиенты AD FS. Мы рекомендуем не использовать self\-подписанные сертификаты для этих сертификатов типов.  
  
> [!IMPORTANT]  
> Использование self\-с подписью, сертификатов SSL в рабочей среде позволит злоумышленнику в партнерской организации для управления серверами федерации в партнерской организации по ресурсам. Риск безопасности существует, так как self\-подписанные сертификаты являются корневыми. Они должны быть добавлены в хранилище доверенных корневых другого сервера федерации \(к примеру, сервер федерации ресурсов\), который можно оставить этот сервер уязвимым для атак.  
  
После получения сертификата из центра сертификации необходимо убедиться, что все сертификаты импортированы в хранилище личных сертификатов на локальном компьютере. Можно импортировать сертификаты в личном хранилище с помощью оснастки MMC для сертификатов\-в.  
  
В качестве альтернативы для использования сертификатов привязать\-, можно также импортировать SSL-сертификат с помощью оснастки диспетчера IIS\-в во время, назначенное SSL сертификатов на веб-сайт по умолчанию. Дополнительные сведения см. в разделе [Импорт сертификата аутентификации сервера на веб-сайт по умолчанию](../../ad-fs/deployment/Import-a-Server-Authentication-Certificate-to-the-Default-Web-Site.md).  
  
> [!NOTE]  
> Прежде чем устанавливать программное обеспечение AD FS на компьютере, который должен стать сервером федерации, убедитесь, что оба сертификата находятся в хранилище личных сертификатов локального компьютера, а сертификат SSL назначен веб сайт по умолчанию. Дополнительные сведения о порядке задач, которые требуются для настройки сервера федерации см. в разделе [контрольный список: Настройка сервера федерации](../../ad-fs/deployment/Checklist--Setting-Up-a-Federation-Server.md).  
  
В зависимости от требований безопасности и бюджетных ограничений необходимо тщательно продумать, какие из сертификатов будут присваиваться публичным или корпоративным центром сертификации. На рисунке ниже показаны рекомендованные издатели (центры сертификации) определенных типов сертификатов. В этих рекомендациях отражен наиболее\-практике подход, безопасности и затрат.  
  
![требования к CERT](media/adfs2_fedserver_certstory_1.png)  
  
## <a name="certificate-revocation-lists"></a>Списки отзыва сертификатов  
Если у какого-либо используемого сертификата есть списки отзыва сертификатов (CRL), сервер с настроенным сертификатом должен иметь возможность связаться с сервером, распространяющим CRL.  
  
## <a name="see-also"></a>См. также
[Руководство по разработке служб федерации Active Directory в Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)