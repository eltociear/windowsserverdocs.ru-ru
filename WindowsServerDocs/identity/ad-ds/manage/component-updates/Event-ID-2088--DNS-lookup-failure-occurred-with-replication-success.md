---
ms.assetid: 0fd7b6aa-3e50-45a3-a3a6-56982844363e
title: ИД события 2088 — Ошибка уточняющего запроса DNS при репликации
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: f84fd7be45995e9e0b318b42c8b4152af244a9da
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/08/2020
ms.locfileid: "80823057"
---
# <a name="event-id-2088-dns-lookup-failure-occurred-with-replication-success"></a>Событие c идентификатором 2088: сбой поиска в DNS при успешной репликации

>Область применения: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

    
    <developerConceptualDocument xmlns="https://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:xlink="https://www.w3.org/1999/xlink" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="https://ddue.schemas.microsoft.com/authoring/2003/5 http://clixdevr3.blob.core.windows.net/ddueschema/developer.xsd">
      <introduction>
    <para>When a destination domain controller running Windows Server 2003 with Service Pack 1 (SP1) receives Event ID 2088 in the Directory Service event log, attempts to resolve the globally unique identifier (GUID) in the alias (CNAME) resource record to an IP address for the source domain controller failed. However, the destination domain controller tried other means to resolve the name and succeeded by using either the fully qualified domain name (FQDN) or the NetBIOS name of the source domain controller. Although replication was successful, the Domain Name System (DNS) problem should be diagnosed and resolved. </para>
    <para>The following is an example of the event text: </para>
    <code>Log Name: Directory Service

    Source: Microsoft-Windows-ActiveDirectory_DomainService
    Date: 3/15/2008  9:20:11 AM
    Event ID: 2088
    Task Category: DS RPC Client 
    Level: Warning
    Keywords: Classic
    User: ANONYMOUS LOGON
    Computer: DC3.contoso.com
    Description:
    Active Directory could not use DNS to resolve the IP address of the 
    source domain controller listed below. To maintain the consistency 
    of Security groups, group policy, users and computers and their passwords, 
    Active Directory Domain Services successfully replicated using the NetBIOS 
    or fully qualified computer name of the source domain controller. 

Недействительная конфигурация DNS может влиять на другие базовые операции на компьютерах-членах, контроллерах домена или серверах приложений в этом лесу домен Active Directory Services, включая проверку подлинности входа или доступ к сетевым ресурсам. 

Следует немедленно устранить эту ошибку конфигурации DNS, чтобы этот контроллер домена мог разрешить IP-адрес исходного контроллера домена с помощью DNS. 

Альтернативное имя сервера: DC1 не удалось выполнить DNS-имя узла: 4a8717eb-8e58-456c-995a-c92e4add7e8e. _msdcs. contoso. com 

Примечание. по умолчанию для любого 12-часового периода отображается не более 10 ошибок DNS, даже если происходит более 10 сбоев.  Чтобы регистрировать все индивидуальные события сбоя, задайте для следующего параметра реестра диагностики значение 1: 

Путь реестра: клиент RPC HKLM\System\CurrentControlSet\Services\NTDS\Diagnostics\22 DS 

Действие пользователя: 

1) Если исходный контроллер домена больше не работает или его операционная система переустановлена с другим именем компьютера или GUID объекта НТДСДСА, удалите метаданные исходного контроллера домена с помощью Ntdsutil. exe, выполнив действия, описанные в статье МСКБ 216498. 

2) Убедитесь, что исходный контроллер домена работает Active Directory и доступен в сети, введя команду "net view \\&lt;Source DC Name&gt;" или "ping &lt;Source DC Name&gt;". 

3) Убедитесь, что исходный контроллер домена использует допустимый DNS-сервер для служб DNS и что запись узла и запись CNAME исходного контроллера домена зарегистрированы правильно, используя улучшенную версию службы DNS DCDIAG. EXE, доступный на <https://www.microsoft.com/dns> 

Dcdiag/test: DNS 

4) Убедитесь, что этот конечный контроллер домена использует допустимый DNS-сервер для служб DNS, запустив улучшенную версию службы DNS для программы DCDIAG. EXE в консоли конечного контроллера домена следующим образом: 

Dcdiag/test: DNS 

5) Дальнейший анализ ошибок DNS см. в статье KB 824449: <https://support.microsoft.com/?kbid=824449> 

Дополнительное значение ошибки данных: 11004 запрошенное имя допустимо, но данные запрошенного типа не найдены</code> </introduction>
  <section>
    <title>Диагностика</title>
    <content>
      <para>Сбой разрешения имени исходного контроллера домена с помощью записи ресурса псевдонима (CNAME) в DNS может быть вызвана невозможностью настройки DNS или задержками при распространении данных DNS.</para>
    </content>
  </section>
  <section>
      
    <content>
    <title>разрешения</title><para>Выполните тестирование DNS, как описано в &quot;<link xlink:href="85b1d179-f53e-4f95-b0b8-5b1c096a8076">событие с идентификатором 2087: сбой уточняющего запроса DNS привел к сбою репликации</link>.&quot;</para>
    </content>
  </section>
  <relatedTopics />
</developerConceptualDocument>


