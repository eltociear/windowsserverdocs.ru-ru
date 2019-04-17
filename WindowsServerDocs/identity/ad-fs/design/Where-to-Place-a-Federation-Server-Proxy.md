---
ms.assetid: ec26705c-4446-4226-b9b4-b775b642f0f4
title: "Место размещения прокси-сервера федерации"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 4bde30f694c6490962edaa0c3fe1543e74ba7fd7
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/12/2017
---
# <a name="where-to-place-a-federation-server-proxy"></a>Место размещения прокси-сервера федерации

>Область применения: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Прокси-серверов федерации \(AD FS\) служб федерации Active Directory можно разместить в сети периметра, чтобы обеспечить уровень защиты от атак злоумышленников, которые могут появиться из Интернета. Прокси-серверы федерации идеально подходят для среды сети периметра, так как они не имеют доступа к закрытым ключам, которые используются для создания маркеров. Тем не менее прокси-серверы федерации могут эффективно направлять входящие запросы на серверы федерации, авторизованные для создания этих токенов.  
  
Нет необходимости размещать прокси-сервера федерации в корпоративной сети для партнера по учетным записям или партнера по ресурсам, так как клиентские компьютеры, подключенные к корпоративной сети могут взаимодействовать напрямую с сервера федерации. В этом сценарии сервер федерации предоставляет функции прокси-сервера сервера федерации для клиентских компьютеров, которые поступают от корпоративной сети.  
  
Как это обычно бывает в сетях периметра, брандмауэр выходом intranet\ устанавливается между сетью периметра и корпоративной сети и модулю брандмауэру часто устанавливается между сетью периметра и Интернетом. В этом сценарии прокси-сервера федерации располагается между этими брандмауэрами в сети периметра.  
  
## <a name="configuring-your-firewall-servers-for-a-federation-server-proxy"></a>Настройка серверов брандмауэра для прокси-сервера федерации  
Для федерации прокси перенаправления процесс сервера можно добиться успеха все серверы брандмауэра должны быть настроены для разрешения трафика \(HTTPS\) безопасной протокол HTTP. Использование протокола HTTPS не требуются, поскольку серверы брандмауэра необходимо опубликовать прокси-сервера федерации, использовать порт 443, прокси-сервера федерации в сети периметра был доступ к сервера федерации в корпоративной сети.  
  
> [!NOTE]  
> Любой обмен данными с клиентских компьютеров также выполняется по протоколу HTTPS.  
  
Кроме того, модулю выходом брандмауэра сервера, например компьютер под управлением Microsoft Internet Security and Acceleration \(ISA\) сервера, использует процесс, известный как публикация сервера для распределения запросов клиентов Интернета соответствующим серверам периметра и корпоративной сети, таких как прокси-серверов федерации или серверы федерации.  
  
Правила публикации сервера определяют, как работает публикация сервера — по существу это фильтрация всех входящих и исходящих запросы через компьютер ISA Server. Правила публикации сервера назначают входящие клиентские запросы соответствующим серверам за компьютером ISA Server. Сведения о настройке ISA Server для публикации сервера см. в разделе [Создание безопасного правила веб-публикаций](https://go.microsoft.com/fwlink/?LinkId=75182).  
  
В федеративной среде AD FS эти клиентские запросы обычно адресованы определенному URL-АДРЕСУ, например, федерации идентификатор URL-адрес сервера например http://fs.fabrikam.com. Поскольку эти клиентские запросы приходят из Интернета, сервер брандмауэра, взаимодействующий с модулю должна быть настроена на опубликовать URL-адрес идентификатор сервера федерации для каждого прокси-сервера федерации, развернутого в сети периметра.  
  
### <a name="configuring-isa-server-to-allow-ssl"></a>Настройка ISA Server для протокола SSL  
Для упрощения безопасного обмена данными Служб федерации Active Directory, должны настроить ISA Server для обмена данными \(SSL\) Secure Sockets Layer между следующее:  
  
-   **Серверы федерации и прокси-серверов федерации.** Канал SSL обязателен для всех подключений между серверами федерации и прокси-серверов федерации. Таким образом необходимо настроить ISA Server для протокола SSL-соединение между корпоративной сетью и сетью периметра.  
  
-   **Клиентские компьютеры, серверы федерации и прокси-серверов федерации.** Чтобы могло происходить взаимодействие между клиентскими компьютерами и серверами федерации или между клиентскими компьютерами и прокси-серверов федерации, можно поместить компьютер под управлением ISA Server перед сервера федерации или прокси-сервера федерации.  
  
    Если ваша организация выполняет проверку подлинности клиента SSL на сервере федерации или прокси-сервера федерации, при размещении компьютера с ISA Server перед сервера федерации или прокси-сервера федерации, на сервере должен быть настроен для pass\ сквозная соединения SSL, так как соединение SSL должно завершаться в сервера федерации или прокси-сервера федерации.  
  
    Если ваша организация не выполняет проверку подлинности клиента SSL на сервере федерации или прокси-сервера федерации, дополнительный вариант состоит в том, чтобы разрывать соединение SSL на компьютере с ISA Server, а затем повторно-установить SSL-подключение к серверу федерации или прокси-сервера федерации.  
  
> [!NOTE]  
> Сервера федерации или прокси-сервера федерации требует, чтобы соединение было защищено SSL для защиты содержимого токена безопасности.  
  
## <a name="see-also"></a>См. также:
[Руководство по разработке служб AD FS в Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)