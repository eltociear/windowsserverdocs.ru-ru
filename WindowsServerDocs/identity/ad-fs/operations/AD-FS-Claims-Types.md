---
ms.assetid: 
title: "Типы в AD FS утверждений клиентского доступа"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 1e37aded450555d293806d1ed8903a51e3df9424
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/12/2017
---
#<a name="client-access-policy-claim-types-in-ad-fs"></a>Типы в AD FS утверждений клиентской политики доступа

Чтобы предоставить сведения о контексте дополнительный запрос, политик доступа клиентов используйте следующие типы утверждений, которые AD FS создает из данные заголовка запроса, для обработки.  Дополнительные сведения см. [роль механизма утверждений](../technical-reference/the-role-of-the-claims-engine.md).

##<a name="x-ms-forwarded-client-ip"></a>X-MS-пересылаются--IP-адрес клиента

Тип утверждения: `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip`

Это утверждение AD FS представляет это «лучший попытка «Проверка IP-адрес пользователя (например, клиент Outlook) процесс создания запроса. Это утверждение может содержать несколько IP-адресов, включая адрес каждого прокси-сервер, на который перенаправляется запрос.  Это утверждение заполняется из заголовка HTTP, в настоящее время настроить только с Exchange Online, который заполняет заголовок при передаче запрос на проверку подлинности в AD FS. Значение утверждения может быть одно из следующих значений:


- Один IP-адрес — IP-адрес клиента, который был подключен непосредственно к Exchange Online

    >! [Примечание.] IP-адрес клиента в корпоративной сети будет отображаться как IP-адрес внешнего интерфейса организации исходящих прокси-сервера или шлюза.

- Один или несколько IP-адресов
    - Если Exchange Online не удается определить IP-адрес подключение клиента, он будет значение на основе значения заголовка x пересылаются для нестандартных заголовок, который может быть включена в HTTP на основе запросов и поддерживается многие клиенты подсистемы балансировки нагрузки и прокси-серверов на рынке.
    - Несколько IP-адресов, IP-адрес клиента и адрес каждого прокси-сервера, передавшего запрос будет содержать запятую.

    >! [Примечание.] IP-адресов, связанных с Exchange Online инфраструктуры не будет присутствовать в списке.


>! [Предупреждение] Exchange Online в настоящее время поддерживает только IPV4-адресов; он не поддерживает IPV6-адресов. 


## <a name="x-ms-client-application"></a>X-MS-клиентского приложения

Тип утверждения: `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application`

Это утверждение AD FS представляет протокол, используемый клиентом end, который соответствует слабо используемого приложения.  Это утверждение заполняется из заголовка HTTP, в настоящее время настроить только с Exchange Online, который заполняет заголовок при передаче запрос на проверку подлинности в AD FS. В зависимости от приложения значение это утверждение будет иметь одно из следующих:



- В случае устройств, использующих Exchange Active Sync значение равно Microsoft.Exchange.ActiveSync. 
- Использование клиентом Microsoft Outlook может привести к любым из следующих значений:
    - Microsoft.Exchange.Autodiscover
    - Microsoft.Exchange.OfflineAddressBook
    - Microsoft.Exchange.RPC
    - Microsoft.Exchange.WebServices
    - Microsoft.Exchange.Mapi
- Другие возможные значения для этого заголовка включают следующие:
    - Microsoft.Exchange.Powershell
    - Microsoft.Exchange.SMTP
    - Microsoft.Exchange.PopImap
    - Microsoft.Exchange.Pop
    - Microsoft.Exchange.Imap

## <a name="x-ms-client-user-agent"></a>X-MS-клиент — агент пользователя

Тип утверждения: `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-user-agent`

Это утверждение AD FS предоставляет строку для представления тип устройства, используемый клиентом для доступа к службе. Может использоваться, когда пользователям требуется запретить доступ для определенных устройств (например, определенные типы смартфонов).  Это утверждение заполняется из заголовка HTTP, в настоящее время настроить только с Exchange Online, который заполняет заголовок при передаче запрос на проверку подлинности в AD FS. Примеры значений для это утверждение включают (но не ограничиваются) ниже значения.
>! [Примечание.] Ниже приведены примеры значение x-ms агента пользователя могут содержать для клиента, которого x-ms клиентского приложения — «Microsoft.Exchange.ActiveSync»

- Vortex/1.0
- Apple iPad1C1 812.1 или
- Apple iPhone3C1 811.2 или
- Apple iPhone 704.11 или
- Moto-DROID2/4.5.1
- SAMSUNGSPHD700 ИЛИ 100.202
- Android и 0,3

>! [Примечание.] Это также возможно, это значение является пустым.


## <a name="x-ms-proxy"></a>X-MS-прокси

Тип утверждения: `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-proxy`

Это утверждение AD FS означает, что запрос прошло через прокси-сервера федерации.  Это утверждение заполняется прокси-сервера федерации, который заполняет заголовок при передаче запрос на проверку подлинности в серверной части службы федерации. AD FS затем преобразует его утверждения. 

Значение утверждения является DNS-имя прокси-сервера федерации, передавшего запрос.

## <a name="x-ms-endpoint-absolute-path-active-vs-passive"></a>X-MS--абсолютное-путь к конечной точке (пассивный Active vs)

Тип утверждения: `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path`

Этот тип утверждения можно использовать для определения запросов, исходящих от клиентов с «активным» (расширенными возможностями) и «пассивных» клиентов (веб-на основе браузера). Это позволяет внешних запросов из приложений на основе браузера, например Outlook Web Access, SharePoint Online или на портал Office 365 разрешаются во время запросов, исходящих от форматированного клиентов, таких как Microsoft Outlook, блокируются.

Значение утверждения — имя службы AD FS, которая получила запрос.