---
title: "Архитектура интерфейса поставщика поддержки безопасности"
description: "Безопасность Windows Server"
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-windows-auth
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: de09e099-5711-48f8-adbd-e7b8093a0336
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 8b0a74089c5d8a88a380f8a56e3b9e03b84081c1
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/12/2017
---
# <a name="security-support-provider-interface-architecture"></a>Архитектура интерфейса поставщика поддержки безопасности

>Область применения: Windows Server (канал точками годовой), Windows Server 2016

В этом справочном разделе для ИТ-специалистов описываются протоколы проверки подлинности Windows, которые используются в архитектуре интерфейс поставщика поддержки безопасности (SSPI).

Microsoft поддержка интерфейс поставщика безопасности (SSPI) является основой для проверки подлинности Windows. Приложения и службы инфраструктуры, требующие проверки подлинности, используют SSPI для ее предоставления.

SSPI — это реализация от универсального API службы безопасности (GSSAPI) в операционных системах Windows Server. Дополнительные сведения о GSSAPI см. в разделе RFC 2743 и 2744 RFC в базе данных RFC IETF.

По умолчанию поставщиков поддержки безопасности (SSP), задействующих конкретных протоколов проверки подлинности в Windows включены в SSPI как библиотеки DLL. В следующих разделах описываются эти SSP по умолчанию. Дополнительные SSP могут быть включены, если они могут работать с SSPI.

Как показано на следующем изображении SSPI в Windows предоставляет механизм, используемый маркеры проверки подлинности через существующий канал связи между клиентским компьютером и сервером. Когда два компьютеров или устройств должны пройти проверку подлинности для безопасного взаимодействия, запросы проверки подлинности направляются в SSPI, который выполняет процесс проверки подлинности независимо от сетевого протокола, используемых в настоящее время. Интерфейс SSPI возвращает прозрачный больших двоичных объектов. Они передаются между приложениями, в какой момент их можно передать на уровень SSPI. Таким образом SSPI позволяет приложению использовать различные модели безопасности на компьютере или в сети без изменения в интерфейсе в системе безопасности.

![Схема, показывающая архитектура интерфейса поставщика поддержки безопасности](../media/security-support-provider-interface-architecture/AuthN_SecuritySupportProviderInterfaceArchitecture.jpg)

В следующих разделах описываются SSP по умолчанию, которые взаимодействуют с SSPI. SSP используются различными способами, в операционных системах Windows для обеспечения безопасного обмена данными в незащищенного сетевой среде.

-   [Поставщик поддержки безопасности Kerberos](#BKMK_KerbSSP)

-   [Поставщик поддержки безопасности NTLM](#BKMK_NTLMSSP)

-   [Дайджест поставщика поддержки безопасности](#BKMK_DigestSSP)

-   [Поставщик поддержки безопасности Schannel](#BKMK_SchannelSSP)

-   [Согласование поставщика поддержки безопасности](#BKMK_NegoSSP)

-   [Поставщик поддержки безопасности учетных данных](#BKMK_CredSSP)

-   [Согласование расширения поставщика поддержки безопасности](#BKMK_NegoExtsSSP)

-   [Поставщик поддержки безопасности PKU2U](#BKMK_PKU2USSP)

Также включены в этом разделе:

[Выбор поставщика поддержки безопасности](security-support-provider-interface-architecture.md#BKMK_SecuritySupportProviderSelection)

### <a name="BKMK_KerbSSP"></a>Поставщик поддержки безопасности Kerberos
Портал Самообслуживания использует только протокол Kerberos версии 5, реализованное корпорацией Майкрософт. Этот протокол основана на черновик версии и RFC 4120 сети работа группы. Это стандартный протокол, который используется с помощью пароля или смарт-карты для интерактивного входа в систему. Он также является предпочтительным методом аутентификации для служб в Windows.

Поскольку протокол проверки подлинности по умолчанию протокол Kerberos не начиная с Windows 2000, все доменные службы поддержки поставщика общих служб Kerberos. В число этих служб входят:

-   Active Directory запросов, которые используют протокол доступа Directory облегченного доступа к каталогам (LDAP)

-   Удаленный сервер или рабочую станцию управления, использующий службу удаленного вызова процедур

-   Службы печати

-   Клиент сервер проверки подлинности

-   Удаленный доступ к файлам, использующем протокол Server Message Block (SMB) (также известный как общих файловая система Интернета или CIFS)

-   Управление распределенной файловой системой и ссылок

-   Проверки подлинности интрасети в Internet Information Services (IIS)

-   Проверка подлинности центра безопасности для безопасность протокола IP (IPsec)

-   Службы сертификатов Active Directory для пользователей и компьютеров домена запросов на сертификаты

Расположение: %windir%\Windows\System32\kerberos.dll

Этот поставщик включен по умолчанию в версиях, указанных в **относится к** в начале этого раздела, а также Windows Server 2003 и Windows XP.

**Дополнительные ресурсы для протокола Kerberos и поставщика общих СЛУЖБ Kerberos**

-   [Kerberos Майкрософт (Windows)](https://msdn.microsoft.com/library/aa378747(VS.85).aspx)

-   [\[MS-KILE\]: расширения протокола Kerberos](https://msdn.microsoft.com/library/cc233855(PROT.10).aspx)

-   [\[MS-SFU\]: расширения протокола Kerberos: S4u и спецификация протокола ограниченного делегирования](https://msdn.microsoft.com/library/cc246071(PROT.13).aspx)

-   [Kerberos SSP/AP (Windows)](https://msdn.microsoft.com/library/aa377942(VS.85).aspx)

-   [Дополнительные возможности Kerberos](https://technet.microsoft.com/library/cc749438(v=ws.10).aspx) для Windows Vista

-   [Изменения в проверке подлинности Kerberos](https://technet.microsoft.com/library/dd560670(v=ws.10).aspx) для Windows 7 

-   [Технический справочник по проверке подлинности Kerberos](https://technet.microsoft.com/library/cc739058(v=ws.10).aspx)

### <a name="BKMK_NTLMSSP"></a>Поставщик поддержки безопасности NTLM
Поставщик поддержки безопасности NTLM (NTLM SSP) является двоичный файл, использовать, интерфейс поставщика поддержки безопасности (SSPI), чтобы разрешить проверку подлинности NTLM запроса и ответа, а также для согласования параметров целостности и конфиденциальности протокол передачи сообщений. Везде, где используется проверка подлинности SSPI, в том числе для Server Message Block или CIFS проверки подлинности, согласовывать HTTP) проверки подлинности (например, Internet Web и служба удаленного вызова процедур, используется протокол NTLM. NTLM SSP включает NTLM и NTLM версии 2 (NTLMv2) протоколы проверки подлинности.

Поддерживаемые операционные системы Windows можно использовать NTLM SSP следующее:

-   Проверка подлинности клиента или сервера

-   Службы печати

-   Доступ к файлам с помощью CIFS (SMB)

-   Безопасная служба удаленного вызова процедур или служба DCOM

Расположение: %windir%\Windows\System32\msv1_0.dll

Этот поставщик включен по умолчанию в версиях, указанных в **относится к** в начале этого раздела, а также Windows Server 2003 и Windows XP.

**Дополнительные ресурсы для протокола NTLM и NTLM SSP**

-   [Пакет проверки подлинности Msv1_0 (Windows)](https://msdn.microsoft.com/library/aa378753(VS.85).aspx)

-   [Изменения в проверке подлинности NTLM](https://technet.microsoft.com/library/dd566199(v=ws.10).aspx) в Windows 7 

-   [NTLM Майкрософт (Windows)](https://msdn.microsoft.com/library/aa378749(VS.85).aspx)

-   [Аудиту и ограничению руководство по использованию NTLM](https://technet.microsoft.com/library/jj865674(v=ws.10).aspx)

### <a name="BKMK_DigestSSP"></a>Дайджест поставщика поддержки безопасности
Дайджест-проверка подлинности является отраслевым стандартом, используемый для протокола доступа Directory облегченного доступа к каталогам (LDAP) и проверки подлинности в Интернете. Дайджест-проверка подлинности передает учетные данные в сети как подпись хэша или сообщений MD5.

Дайджест поставщика общих СЛУЖБ (Wdigest.dll) используется в следующих целях:

-   Доступ к Internet Explorer и Internet Information Services (IIS)

-   LDAP-запросы

Расположение: %windir%\Windows\System32\Digest.dll

Этот поставщик включен по умолчанию в версиях, указанных в **относится к** в начале этого раздела, а также Windows Server 2003 и Windows XP.

**Дополнительные ресурсы для протокола дайджест и дайджест поставщика общих СЛУЖБ**

-   [Microsoft дайджест-проверки подлинности (Windows)](https://msdn.microsoft.com/library/aa378745(VS.85).aspx)

-   [\[MS-DPSP\]: дайджест-расширения протокола](https://msdn.microsoft.com/library/cc227906(PROT.13).aspx)

### <a name="BKMK_SchannelSSP"></a>Поставщик поддержки безопасности Schannel
Безопасного канала (Schannel) используется для проверки подлинности веб-сервера, например когда пользователь пытается получить доступ к безопасному веб-серверу.

Протокол TLS, протокол SSL, протокол технологии конфиденциальной связи (PCT) и протокол датаграмм транспортного уровня (DTLS) основаны на шифровании с открытым ключом. Все эти протоколы предоставляются Schannel. Все протоколы Schannel используют модель клиент сервер. Schannel SSP использует сертификаты открытого ключа для проверки подлинности сторон. При проверке подлинности сторон, Schannel SSP выбирает протокол в следующем порядке приоритета:

-   Транспорта Layer Security (TLS) версии 1.0

-   Транспорта Layer Security (TLS) версии 1.1

-   Транспорта Layer Security (TLS) версии 1.2

-   Secure Socket Layer (SSL) версии 2.0

-   Secure Socket Layer (SSL) версии 3.0.

-   Технологии связи частного (PCT)

    **Примечание** PCT отключен по умолчанию.

Протокол, который выбран — идеальный протокол проверки подлинности, клиент и сервер может поддерживать. Например если сервер поддерживает все протоколы Schannel, а клиент поддерживает только SSL 3.0 и SSL 2.0, процесс проверки подлинности использует протокол SSL 3.0.

Протокол DTLS используется при вызове явным образом в приложении. Дополнительные сведения о DTLS и другие протоколы, используемые поставщиком Schannel см. в разделе [технические поставщика поддержки безопасности Schannel](../tls/schannel-security-support-provider-technical-reference.md).

Расположение: %windir%\Windows\System32\Schannel.dll

Этот поставщик включен по умолчанию в версиях, указанных в **относится к** в начале этого раздела, а также Windows Server 2003 и Windows XP.

> [!NOTE]
> TLS 1.2 впервые появился в этот поставщик в Windows Server 2008 R2 и Windows 7. Протокол DTLS впервые появился в этот поставщик в Windows Server 2012 и Windows 8.

**Дополнительные ресурсы для протоколов TLS и SSL и Schannel SSP**

-   [Безопасный канал (Windows)](https://msdn.microsoft.com/library/aa380123(VS.85).aspx)

-   [Технический справочник протоколов TLS и SSL](https://technet.microsoft.com/library/cc784149(v=ws.10).aspx)

-   [\[MS-TLSP\]: транспорта профиль Layer Security (TLS)](https://msdn.microsoft.com/library/dd207968(PROT.13).aspx)

### <a name="BKMK_NegoSSP"></a>Согласование поставщика поддержки безопасности
Простая и защищенные GSS-API согласования механизм (SPNEGO) формирует основу для поставщика общих СЛУЖБ согласование whichcan использоваться для согласования протокола проверки подлинности. Когда приложение вызывает SSPI для входа в сеть, его можно указать поставщика общих СЛУЖБ для обработки запроса. Если приложение указывает SSP согласования, он анализирует запрос и выбирает соответствующий поставщика для обработки запроса на основе политик безопасности настроенного клиента.

SPNEGO определено в документе RFC 2478.

В поддерживаемых версиях операционных систем Windows безопасности Negotiate поддерживают выбирает поставщика между протокол Kerberos и NTLM. Выбирает согласование протокола Kerberos по умолчанию, если этот протокол не может использоваться с одной из систем, участвующие в проверке подлинности или вызывающего приложения, не принес достаточных сведений, чтобы использовать протокол Kerberos.

Расположение: %windir%\Windows\System32\lsasrv.dll

Этот поставщик включен по умолчанию в версиях, указанных в **относится к** в начале этого раздела, а также Windows Server 2003 и Windows XP.

**Дополнительные ресурсы для согласования поставщика общих СЛУЖБ**

-   [Microsoft Negotiate (Windows)](https://msdn.microsoft.com/library/aa378748(VS.85).aspx)

-   [\[MS-SPNG\]: простые и защищенные GSS-API согласования механизм (SPNEGO) расширения](https://msdn.microsoft.com/library/cc247021(PROT.13).aspx)

-   [\[MS-N2HT\]: согласования и спецификация протокола проверки подлинности HTTP Nego2](https://msdn.microsoft.com/library/dd303576(PROT.13).aspx)

### <a name="BKMK_CredSSP"></a>Поставщик поддержки безопасности учетных данных
Поставщика службы безопасности учетных данных (CredSSP) предоставляет единого входа (SSO) взаимодействие с пользователем при запуске новых сеансов служб терминалов и служб удаленных рабочих столов. CredSSP дает приложениям возможность делегировать учетные данные пользователей с клиентского компьютера (с помощью клиентского SSP) на целевой сервер (с помощью серверных SSP) на основе политик клиента. CredSSP политик с помощью групповой политики и делегирование учетных данных по умолчанию отключена.

Расположение: %windir%\Windows\System32\credssp.dll

Этот поставщик включен по умолчанию в версиях, указанных в **относится к** в начале этой статьи.

**Дополнительные ресурсы для учетных данных поставщика общих СЛУЖБ**

-   [\[MS-CSSP\]: спецификация протокола (CredSSP) поставщика поддержки безопасности учетных данных](https://msdn.microsoft.com/library/cc226764(PROT.13).aspx)

-   [Учетных данных поставщика службы безопасности и единый вход для терминала службы входа в систему](https://technet.microsoft.com/library/cc749211(v=ws.10).aspx)

### <a name="BKMK_NegoExtsSSP"></a>Согласование расширения поставщика поддержки безопасности
Согласование расширения (NegoExts) — пакет проверки подлинности, который согласовывает использование поставщиков общих служб, отличных от NTLM или протокол Kerberos для приложений и сценариев, реализованных корпорацией Майкрософт и других программ компаний.

Это расширение пакет Negotiate разрешает следующие сценарии:

-   **Доступность полнофункционального клиента федеративной системы.** Документы, доступные на сайты SharePoint и их можно изменить с помощью полнофункционального приложения Microsoft Office.

-   **Полнофункциональный клиент поддержки для служб Microsoft Office.** Пользователи могут входа в службы Microsoft Office и использовать полнофункционального приложения Microsoft Office.

-   **Размещенного сервера Microsoft Exchange и Outlook.** Не установлены отношения доверия домена, установить, так как Exchange Server размещен в Интернете. Outlook использует службу Windows Live, для проверки подлинности пользователей.

-   **Доступность полнофункционального клиента между клиентскими компьютерами и серверами.** Компоненты операционной системы сети и проверки подлинности используются.

Пакет Windows согласования рассматривает NegoExts SSP так же, как Kerberos и NTLM. NegoExts.dll загружается в локальной системе (LSA) во время запуска. При получении запрос проверки подлинности на основе источника запроса NegoExts согласовывает между поддерживаемых поставщиков общих служб. Он собирает учетные данные и политик, шифрует их и отправляет эти сведения для соответствующего поставщика общих СЛУЖБ, где создается маркер безопасности.

Поставщиков общих служб, поддерживаемых NegoExts не автономного поставщиков общих служб, таких как Kerberos и NTLM. Таким образом в составе NegoExts SSP неудачной по любой причине, метод проверки подлинности сообщение сбой проверки подлинности будет отображаться или войти в систему. Возможны без повторного согласования или резервной методов проверки подлинности.

Расположение: %windir%\Windows\System32\negoexts.dll

Этот поставщик включен по умолчанию в версиях, указанных в **относится к** в начале этой статьи, за исключением Windows Server 2008 и Windows Vista.

### <a name="BKMK_PKU2USSP"></a>Поставщик поддержки безопасности PKU2U
Протокол PKU2U была введена и реализована как поставщика общих СЛУЖБ в Windows 7 и Windows Server 2008 R2. Портал Самообслуживания позволяет-одноранговой проверки подлинности, особенно через мультимедиа и общий доступ к файлам домашней группы, которая была введена в Windows 7 функцией. Позволяет обмена данными между компьютерами, которые не являются членами домена.

Расположение: %windir%\Windows\System32\pku2u.dll

Этот поставщик включен по умолчанию в версиях, указанных в **относится к** в начале этой статьи, за исключением Windows Server 2008 и Windows Vista.

**Дополнительные ресурсы для протокол PKU2U и PKU2U SSP**

-   [Знакомство с сетевым удостоверением интеграции](https://technet.microsoft.com/library/dd560662(v=ws.10).aspx)

## <a name="BKMK_SecuritySupportProviderSelection"></a>Выбор поставщика поддержки безопасности
Windows SSPI можно использовать один из протоколов, которые поддерживаются с помощью установленных поставщиков поддержки безопасности. Тем не менее так как не все операционные системы поддерживают те же пакеты поставщика общих СЛУЖБ, как каждый компьютер под управлением Windows Server, клиенты и серверы необходимо согласовать использование протокола, которые они поддерживают. Windows Server предпочитаемое клиентские компьютеры и приложения для использования протокола Kerberos, надежный протокол на основе стандартов, когда это возможно, но операционная система продолжает для клиентских компьютеров и клиентских приложений, которые не поддерживают протокол Kerberos для проверки подлинности.

До проверки подлинности связи месте двух компьютеров необходимо согласовать протокол что они поддерживают. Для любого протокола мог быть использован через интерфейс SSPI каждый компьютер должен иметь соответствующий поставщика общих служб. Например для клиентского компьютера и сервера для использования проверки подлинности Kerberos, они должны поддерживать протокол Kerberos v5. Windows Server использует функцию **EnumerateSecurityPackages** для определения, какие SSP поддерживаются на компьютере и что включают в себя из этих поставщиков общих служб.

Выбор протокола проверки подлинности может быть обработано в одном из следующих двух способов:

1.  [Протокол проверки подлинности одного](#BKMK_SingleAuth)

2.  [Согласование параметр](#BKMK_Negotiate)

### <a name="BKMK_SingleAuth"></a>Протокол проверки подлинности одного
При указании допустимого один протокол на сервере клиентский компьютер должен поддерживать протокол, заданный или сбоя связи. При указании допустимого один протокол проверки подлинности exchange происходит следующим образом:

1.  Клиентский компьютер запрашивает доступ к службе.

2.  Сервер отвечает на запрос, а также определяет протокол, который будет использоваться.

3.  Клиентский компьютер проверяет содержимое ответ и проверки, чтобы определить, поддерживает ли указанного протокола. Если клиентский компьютер поддерживает указанного протокола, проверка подлинности продолжается. Если клиентский компьютер не поддерживает протокол, проверка подлинности завершается неудачно, независимо от того, является ли клиентского компьютера права доступа к ресурсу.

### <a name="BKMK_Negotiate"></a>Согласование параметр
Чтобы разрешить клиента и сервера, чтобы попытаться найти допустимого протокола можно использовать параметр согласования. Это основана на простая и защищенные GSS-API согласования механизм (SPNEGO). Когда проверка подлинности начинается с параметром для согласования протокола проверки подлинности, SPNEGO exchange происходит следующим образом:

1.  Клиентский компьютер запрашивает доступ к службе.

2.  Ответы сервера со списком протоколов проверки подлинности, он может поддерживать и запрос проверки подлинности или ответ на основе протокола, которая является ее первый вариант. Например сервер может списка протокол Kerberos и NTLM и отправить ответ проверки подлинности Kerberos.

3.  Клиентский компьютер проверяет содержимое ответ и проверки, чтобы определить, поддерживает ли оно любого из указанных протоколов.

    -   Если клиентский компьютер поддерживает протокол, проверка подлинности продолжается.

    -   Если клиентский компьютер не поддерживает протокол, но поддерживает один из протоколов, перечисленных сервером, клиентский компьютер позволяет серверу определить, какие протокол проверки подлинности, поддерживаемых и проверка подлинности продолжается.

    -   Если клиентский компьютер не поддерживает перечисленные протоколы, проверка подлинности exchange завершается ошибкой.

## <a name="see-also"></a>См. также:
[Архитектура проверки подлинности Windows](https://technet.microsoft.com/library/dn169024(v=ws.10).aspx)

