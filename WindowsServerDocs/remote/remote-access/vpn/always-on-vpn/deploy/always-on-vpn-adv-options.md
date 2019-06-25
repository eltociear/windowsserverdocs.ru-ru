---
title: Расширенные функции постоянно подключенного VPN-профиля
description: Помимо сценарий развертывания, описанный в этом развертывании можно добавить другие расширенные функции VPN для повышения безопасности и доступности VPN-подключения.
ms.assetid: 51a1ee61-3ffe-4f65-b8de-ff21903e1e74
ms.prod: windows-server-threshold
ms.technology: networking-ras
ms.topic: article
ms.date: 11/05/2018
ms.author: pashort
author: shortpatti
ms.localizationpriority: medium
ms.reviewer: deverette
ms.openlocfilehash: 5f43d64dc7642ef67da03fec989909bc4f2f14ae
ms.sourcegitcommit: a3c9a7718502de723e8c156288017de465daaf6b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/19/2019
ms.locfileid: "67263028"
---
# <a name="advanced-features-of-always-on-vpn"></a>Расширенные возможности AlwaysOn VPN

>Относится к: Windows Server (полугодовой канал), Windows Server 2016, Windows Server 2012 R2, Windows 10

- [**Предыдущих:** Дополнительные сведения о технологии AlwaysOn VPN](../always-on-vpn-technology-overview.md)
- [**Далее:** Начать планирование развертывания AlwaysOn VPN](always-on-vpn-deploy-planning.md)

После развертывания сценарии, обеспечиваемые можно добавить другие расширенные функции VPN для повышения безопасности и доступности VPN-подключения. Например такие компоненты помогает убедитесь, что подключающийся клиент работоспособен, прежде чем разрешить соединения.

## <a name="high-availability"></a>Высокая доступность

Ниже приведены дополнительные параметры для обеспечения высокой доступности.

|Параметр  |Описание  |
|---------|---------|
|Устойчивость сервера и балансировки нагрузки     |В средах, требующих высокого уровня доступности или поддержки большого количества запросов можно увеличить производительность и отказоустойчивость удаленного доступа с помощью балансировки нагрузки между несколькими серверами, которые под управлением сервера политики сети (NPS) и включение удаленного доступа Сервер доступа кластеризации.<p>Связанные документы:<ul><li>[Балансировка нагрузки сервера прокси-сервера политики сети](../../../../../networking/technologies/nps/nps-manage-proxy-lb.md)</li><li>[Развертывание удаленного доступа в кластере](https://docs.microsoft.com/windows-server/remote/remote-access/ras/cluster/deploy-remote-access-in-cluster)</li></ul>        |
|Устойчивости географических сайтов     |Для географического положения на основе IP-адресов можно использовать глобальный диспетчер трафика с помощью DNS в Windows Server 2016. Для более надежной балансировки нагрузки географических, можно использовать решения глобального сервера балансировки нагрузки, например диспетчер трафика Microsoft Azure.<p>Связанные документы:<ul><li>[Обзор диспетчера трафика](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview)</li><li>[Диспетчер трафика Microsoft Azure](https://azure.microsoft.com/services/traffic-manager)</li></ul>         |

## <a name="advanced-authentication"></a>Расширенная проверка подлинности

Ниже приведены дополнительные параметры для проверки подлинности.

|Параметр  |Описание  |
|---------|---------|
|Windows Hello для бизнеса;     |В Windows 10 служба Windows Hello для бизнеса заменяет пароли на строгую двухфакторную проверку подлинности на компьютерах и мобильных устройствах. Эта проверка подлинности состоит из нового типа учетных данных пользователя, который привязывается к устройству и использует биометрические или личный идентификационный номер (PIN).<p>Клиент Windows 10 VPN не совместимы с Windows Hello для бизнеса. После входа пользователя в систему с помощью жеста, VPN-подключение использует Windows Hello для бизнеса сертификат для проверки подлинности на основе сертификата.<p>Связанные документы:<ul><li>[Windows Hello для бизнеса](https://docs.microsoft.com/windows/access-protection/hello-for-business/hello-identity-verification)</li><li>Пример внедрения: [Включение удаленного доступа с помощью Windows Hello для бизнеса в Windows 10](https://msdn.microsoft.com/library/mt728163.aspx)</li></ul>         |
|Azure многофакторная Идентификация (MFA)     |Azure MFA имеет облачных и локальных версий, которые можно интегрировать с механизмом проверки подлинности Windows VPN.<p>Дополнительные сведения о том, как работает этот механизм, см. в разделе [интеграция аутентификации RADIUS с сервером многофакторной идентификации Azure](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-server-radius).         |

## <a name="advanced-vpn-features"></a>Функции расширенной VPN

Ниже приведены дополнительные параметры для расширенных функций.

|Параметр  |Описание  |
|---------|---------|
|Фильтрация трафика     |Если необходимо применить, какие приложения VPN клиенты имеют доступ к, вы можете включить фильтры трафика VPN.<p>Дополнительные сведения см. в разделе [функции безопасности VPN](https://docs.microsoft.com/windows/access-protection/vpn/vpn-security-features).         |
|VPN-подключение, инициированное приложением     |Можно настроить профили VPN для автоматического подключения при запуске некоторых приложений или типов приложений.<p>Дополнительные сведения об этом и других параметров активации, см. в разделе [параметры для автоматического запуска профиля VPN](https://docs.microsoft.com/windows/access-protection/vpn/vpn-auto-trigger-profile).         |
|Условный доступ через VPN   |Соответствие требованиям условного доступа и устройств может потребоваться управляемых устройств для обеспечения соответствия стандартам, прежде чем они смогут подключаться к VPN. Одно из дополнительных функций для условного доступа VPN позволяет ограничить VPN-подключений только теми, где сертификат проверки подлинности клиента содержит AAD условного доступа из "1.3.6.1.4.1.311.87 OID «».<p>Чтобы ограничить VPN-подключений, вам потребуется:<ol><li>На сервере политики сети откройте **сервера политики сети** оснастки.</li><li>Разверните **политики** > **политик сети**.</li><li>Щелкните правой кнопкой мыши **подключений виртуальной частной сети (VPN)** сетевой политики и выберите **свойства**.</li><li>Выберите **параметры** вкладки.</li><li>Выберите **конкретного поставщика** и выберите **добавить**.</li><li>Выберите **идентификатор Объекта сертификата разрешено** и затем выберите **добавить**.</li><li>Вставьте AAD условного доступа OID **1.3.6.1.4.1.311.87** как значение атрибута, а затем выберите **ОК** дважды.</li><li>Выберите **закрыть** и затем **применить**.<p>Теперь когда VPN-клиенты пытаются подключиться с помощью любой сертификат, отличный от сертификата кратковременное облачной, соединение будет разорвано.</li></ol>Дополнительные сведения об условном доступе см. в разделе [VPN и условный доступ](https://docs.microsoft.com/windows/access-protection/vpn/vpn-conditional-access).   |


---
## <a name="blocking-vpn-clients-that-use-revoked-certificates"></a>Блокировка клиентов VPN, которые используют отозванные сертификаты
  
После установки обновлений, RRAS-сервер может применить отзыва сертификатов для VPN, использующих IKEv2 и сертификаты компьютера для проверки подлинности, например устройства туннеля VPN типа "Always-on". Это означает, что для таких VPN RRAS-сервере можно запретить VPN-подключений на клиентах, использующих отозванных сертификатов.

**Доступность**

В следующей таблице перечислены дат приблизительное выпуска исправления для каждой версии Windows.

|Версия операционной системы |Дата выпуска * |
|---------|---------|
|Windows Server версии 1903  |Q2, 2019 Г.  |
|Windows Server 2019<br />Windows Server версии 1809  |ВОПРОС 3, 2019 Г.  |
|Windows Server версии 1803  |ВОПРОС 3, 2019 Г.  |
|Windows Server версии 1709  |ВОПРОС 3, 2019 Г.  |
|Windows Server 2016 версии 1607  |Q2, 2019 Г.  |
  
\* Все даты выхода, перечислены в календарных кварталов. Значения даты являются приблизительными и могут изменяться без уведомления.

**Настройка необходимых компонентов** 

1. Установите обновления для Windows, как только они становятся доступными.
1. Убедитесь, что наличие записи CDP VPN-клиента и сертификаты сервера RRAS, используемые и что соответствующие списки отзыва сертификатов можно связаться с сервера RRAS.
1. На сервере RRAS, используйте **набора VpnAuthProtocol** командлет PowerShell для настройки **RootCertificateNameToAccept** параметра.<br /><br />
   В следующем примере перечисляются команды, чтобы это сделать. В примере **CN = корневой центр сертификации Contoso** представляет различающееся имя корневого центра сертификации. 
   ``` powershell
   $cert1 = ( Get-ChildItem -Path cert:LocalMachine\root | Where-Object -FilterScript { $_.Subject -Like "*CN=Contoso Root Certification Authority,*" } )
   Set-VpnAuthProtocol -RootCertificateNameToAccept $cert1 -PassThru
   ```
**Настройка сервера RRAS для принудительного применения отзыва сертификатов для VPN-подключений на основании сертификатов компьютеров IKEv2**

1. В окне командной строки выполните следующую команду: 
   ```
   reg add HKLM\SYSTEM\CurrentControlSet\Services\RemoteAccess\Parameters\Ikev2 /f /v CertAuthFlags /t REG_DWORD /d "4"
   ```

1. Перезапустите **маршрутизации и удаленного доступа** службы.
  
Чтобы отключить отзыва сертификатов для подключений VPN, задайте **CertAuthFlags = 2** или удалите **CertAuthFlags** значение, а затем перезапустите **маршрутизации и удаленного доступа**службы. 

**Как отменить сертификат VPN-клиента для VPN-подключения, на основании сертификата компьютера IKEv2**
1. Отозвать сертификат клиента из центра сертификации.
1. Опубликуйте новый список отзыва Сертификатов центра сертификации.
1. На RRAS-сервере откройте окно командной строки администратора и выполните следующие команды:
   ```
   certutil -urlcache * delete
   certutil -setreg chain\ChainCacheResyncFiletime @now
   ```

**Работа по проверке этого отзыва сертификатов для подключений VPN на основе сертификата компьютера IKEv2**  
>[!Note]  
> Прежде чем использовать эту процедуру, убедитесь, что включен CAPI2 операционного журнала событий.
1. Выполните предыдущие шаги, чтобы отозвать сертификат клиента VPN.
1. Попробуйте подключиться к VPN с помощью клиента, имеющего отозванных сертификатов. Сервер RRAS следует запретить подключение и отображения сообщения, такие как «учетные данные проверки подлинности IKE, неприемлемо.»
1. На RRAS-сервере, откройте средство просмотра событий и перейдите к **приложений и журналы служб/Microsoft/Windows/CAPI2**. 
1. Найдите событие, которое содержит следующие сведения:
   * Имя журнала: **Microsoft-Windows-CAPI2/Operational Microsoft-Windows-CAPI2/Operational**
   * ИД события: **41** 
   * Событие содержит следующий текст: **тема =»*полное доменное имя клиента*"** (*полное доменное имя клиента* представляет полное доменное имя клиента, который имеет отозванных сертификат.) 

   **<Result>** Поле данных события должно включать **сертификат был отозван**. Например см. в разделе ниже отрывки из события:
   ```xml
   Log Name:      Microsoft-Windows-CAPI2/Operational Microsoft-Windows-CAPI2/Operational  
   Source:        Microsoft-Windows-CAPI2  
   Date:          5/20/2019 1:33:24 PM  
   Event ID:      41  
   ...  
   Event Xml:
   <Event xmlns="http://schemas.microsoft.com/win/2004/08/events/event">
    <UserData>  
     <CertVerifyRevocation>  
      <Certificate fileRef="C97AE73E9823E8179903E81107E089497C77A720.cer" subjectName="client01.corp.contoso.com" />  
      <IssuerCertificate fileRef="34B1AE2BD868FE4F8BFDCA96E47C87C12BC01E3A.cer" subjectName="Contoso Root Certification Authority" />
      ...
      <Result value="80092010">The certificate is revoked.</Result>
     </CertVerifyRevocation>
    </UserData>
   </Event>
   ```

---
## <a name="additional-protection"></a>Дополнительная защита

### <a name="trusted-platform-module-tpm-key-attestation"></a>Аттестация ключей доверенного платформенного модуля (TPM)

Сертификат пользователя с ключом аттестовать TPM предоставляет выше гарантии безопасности, резервное копирование, не возможность экспорта, противодействия подбору и изоляцию ключи, предоставляемые доверенного платформенного МОДУЛЯ.

Дополнительные сведения об аттестации ключей доверенного платформенного МОДУЛЯ в Windows 10, см. в разделе [Аттестация ключей доверенного платформенного МОДУЛЯ](https://docs.microsoft.com/windows-server/identity/ad-ds/manage/component-updates/tpm-key-attestation).

## <a name="next-step"></a>Дальнейшие действия

[Начать планирование развертывания AlwaysOn VPN](always-on-vpn-deploy-planning.md): Перед установкой роли сервера удаленного доступа на компьютере, который вы планируете использование в качестве VPN-сервера необходимо выполните следующие задачи. После правильного планирования, можно развернуть AlwaysOn VPN и при необходимости настроить условный доступ для VPN-подключения с помощью Azure AD.  

## <a name="related-topics"></a>См. также
- [Балансировка нагрузки сервера прокси-сервера NPS](../../../../../networking/technologies/nps/nps-manage-proxy-lb.md): Удаленные клиенты Authentication Dial-In User Service (RADIUS), которые являются серверы сетевого доступа, такими как серверы виртуальной частной сети (VPN) и точки беспроводного доступа, создайте запросы на соединение и отправляют их серверам RADIUS, таких как сервер политики сети. В некоторых случаях сервер политики сети может получить слишком много запросов на подключение за один раз приведет к снижению производительности или перегрузку.

- [Обзор диспетчера трафика](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview): В этом разделе представлен обзор Azure диспетчера трафика, который позволяет управлять распределением пользовательского трафика для конечных точек службы. Диспетчер трафика использует систему доменных имен (DNS) для направления клиентских запросов к наиболее подходящей конечной точке, в зависимости от метода маршрутизации трафика и работоспособности конечных точек. 

- [Windows Hello для бизнеса](https://docs.microsoft.com/windows/access-protection/hello-for-business/hello-identity-verification): В этом разделе приводятся предварительные требования, например в случае развертывания облачных и гибридных развертываний.  Кроме того, в этом разделе перечислены часто задаваемые вопросы о Windows Hello для бизнеса.

- [Пример внедрения: Включение удаленного доступа с помощью Windows Hello для бизнеса в Windows 10](https://msdn.microsoft.com/library/mt728163.aspx): В этом пример внедрения вы узнаете, как корпорация Майкрософт реализовала удаленного доступа с помощью Windows Hello для бизнеса.  Windows Hello для бизнеса — это метод проверки подлинности на основе сертификатов для организаций и потребителей, выходящих за рамки пароли и закрытого и открытого ключа. Такая форма проверки подлинности использует учетные данные пары ключей, которые могут заменить пароли и брешей в системе, хищение и фишинг. 

- [Интеграция аутентификации RADIUS с сервером многофакторной идентификации Azure](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-server-radius): В этом разделе описана процедура добавления и настройки аутентификации клиентов RADIUS с сервером многофакторной идентификации Azure. RADIUS является стандартным протоколом получения запросов проверки подлинности и обработки этих запросов. На сервере многофакторной идентификации Azure может действовать как сервер RADIUS. 

- [Функции безопасности VPN](https://docs.microsoft.com/windows/access-protection/vpn/vpn-security-features): В этом разделе содержит вы VPN рекомендации по безопасности для блокировать VPN, интеграция Windows Information Protection (WIP) с помощью VPN и фильтры трафика. 

- [Параметры для автоматического запуска профиля VPN](https://docs.microsoft.com/windows/access-protection/vpn/vpn-auto-trigger-profile): В этом разделе приведены параметры для автоматического запуска профиля VPN, например триггер приложения, на основании имени триггера и Always On.

- [VPN и условный доступ](https://docs.microsoft.com/windows/access-protection/vpn/vpn-conditional-access): Здесь представлен обзор платформы облачных условного доступа предоставляет вариант соответствия устройств для удаленных клиентов. Условный доступ — это модуль оценки на основе политик, который позволяет создавать правила доступа для любого приложения, подключенного к Azure Active Directory (Azure AD). 

- [Аттестация ключей TPM](https://docs.microsoft.com/windows-server/identity/ad-ds/manage/component-updates/tpm-key-attestation): Здесь представлен обзор доверенного платформенного модуля (TPM) и процедуру развертывания аттестации ключей доверенного платформенного МОДУЛЯ. Можно также найти сведения и решить проблемы устранения неполадок.