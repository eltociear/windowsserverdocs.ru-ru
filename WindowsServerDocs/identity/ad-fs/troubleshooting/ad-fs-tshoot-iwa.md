---
title: AD FS Устранение неполадок — встроенная проверка подлинности Windows
description: В этом документе описывается устранение встроенную проверку подлинности windows
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 02/21/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 9703a8652b0e0bbafe48858cbfbcc8aa9aa31ef8
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/07/2019
ms.locfileid: "66812046"
---
# <a name="ad-fs-troubleshooting---integrated-windows-authentication"></a>AD FS Устранение неполадок — встроенная проверка подлинности Windows
Встроенная проверка подлинности Windows позволяет пользователям войти, используя свои учетные данные Windows и возможности единого входа (SSO), с помощью Kerberos или NTLM.

## <a name="reason-integrated-windows-authentication-fails"></a>Не удается причина встроенную проверку подлинности windows
Существуют три основная причина, почему не удастся встроенную проверку подлинности windows. Подробные сведения.
    - Неправильной настройки Name(SPN) субъекта-службы
    - Токен привязки канала
    - Конфигурация Internet Explorer

## <a name="spn-misconfiguration"></a>Неправильной настройки имени участника-службы
Имя участника-службы (SPN) — это уникальный идентификатор экземпляра службы. Имена участников-служб используются проверкой подлинности Kerberos для связи с экземпляром службы с учетной записью входа службы. Это позволяет клиентскому приложению для запроса, что служба проверки подлинности учетной записи, даже если клиент не имеет имя учетной записи.

Пример того, как имя SPN используется с AD FS выглядит следующим образом:
1. Веб-браузер запрашивает в Active Directory, чтобы определить, какую учетную запись службы выполняется sts.contoso.com
2. Active Directory указывает обозревателю, что это учетная запись службы AD FS.
3. Браузер будет получить билет Kerberos для учетной записи службы AD FS.

Если учетная запись службы AD FS имеет неправильно настроенный или неверное имя участника-службы, это может вызвать проблемы.  Просмотрев данные трассировки сети, могут возникнуть ошибки, например ошибка KRB: KRB5KDC_ERR_S_PRINCIPAL_UNKNOWN.

Используя данные трассировки сети (например, Wireshark) можно определить, какой браузер пытается сопоставить имя участника-службы и затем с помощью командной строки средства setspn - Q <spn>, можно выполнить поиск этого имени субъекта-службы.  Он не может быть найден, или он может быть назначен другой учетной записью, отличной от учетной записи службы AD FS.

![Интегрированные](media/ad-fs-tshoot-iwa/iwa3.png)

Имя участника-службы можно проверить, просмотрев свойства учетной записи службы AD FS.

![Интегрированные](media/ad-fs-tshoot-iwa/iwa1.png)

## <a name="channel-binding-token"></a>Токен привязки канала
В настоящее время когда клиентское приложение проходит аутентификацию на сервер с помощью Kerberos, Digest или проверку NTLM с использованием HTTPS, сначала устанавливается канал безопасности транспортного уровня (TLS) и проверка подлинности выполняется по этому каналу. 

Маркер привязки канала является свойством внешнего канала с защитой TLS и используется для привязки внешнего канала к диалогу через внутренний канал, проверкой подлинности клиента.

При наличии «man-in--middle» атака происходит и они имеют de crypting и повторное шифрование трафика SSL, то ключ не будет соответствовать.  AD FS определит, что найдется что-нибудь, расположенную в середине между web Обзор r и самого себя.  Это вызовет сбой проверки подлинности Kerberos, и пользователю будет предложено 401 диалоговое окно, вместо Единого входа.

Это может быть вызвано несколькими:
 - что-либо, расположенный между браузером и AD FS
 - Fiddler
 - Обратный прокси-серверов, выполнение мост SSL

По умолчанию AD FS имеет это значение «Разрешить».  Можно изменить этот параметр, используя командлет PowerShell: `Set-ADFSProperties -ExtendProtectionTokenCheck`

Дополнительные сведения о см. в разделе [советы и рекомендации для безопасного планирования и развертывания AD FS](../../ad-fs/design/best-practices-for-secure-planning-and-deployment-of-ad-fs.md).

## <a name="internet-explorer-configuration"></a>Конфигурация Internet Explorer
По умолчанию Internet explorer будет иметь следующим образом:

1. Internet explorer будет получать ответ 401 от ADFS с в заголовке слово NEGOTIATE.
2. Это сообщает веб-браузер для получения билета Kerberos или NTLM для отправки обратно в AD FS.
3. По умолчанию IE попытается сделать (SPNEGO) без участия пользователя, если слово NEGOTIATE находится в заголовке.  Он работает только для сайтов интрасети.

Существуют 2 основным моментам, которые можно запретить это happeing.
   - Включение встроенной проверки подлинности Windows не установлен в свойствах обозревателя IE.  Это расположенный в свойства обозревателя "->" Дополнительно "->" безопасности.
   
   ![Интегрированные](media/ad-fs-tshoot-iwa/iwa4.png)
   
   - Зоны безопасности не настроены надлежащим образом
       - Полные доменные имена не находятся в зоне интрасети
       - URL-адрес для AD FS не находится в зоне интрасети.

      ![Интегрированные](media/ad-fs-tshoot-iwa/iwa5.png)
## <a name="next-steps"></a>Следующие шаги

- [Устранение неполадок в AD FS](ad-fs-tshoot-overview.md)