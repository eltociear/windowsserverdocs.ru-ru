---
ms.assetid: eafdddc3-40d7-4a75-8f4f-a45294aabfc8
title: Реализация безопасного администрирования узлов
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 4a36f27bc64e6e135451818b27dc2319f18655f4
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/08/2020
ms.locfileid: "80821187"
---
# <a name="implementing-secure-administrative-hosts"></a>Реализация безопасного администрирования узлов

>Область применения: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Безопасные административные узлы — это рабочие станции или серверы, которые были настроены специально для создания безопасных платформ, из которых привилегированные учетные записи могут выполнять административные задачи в Active Directory или на контроллерах домена, присоединенных к домену системах и приложениях, работающих в системах, присоединенных к домену. В этом случае "привилегированные учетные записи" относятся не только к учетным записям, которые являются членами наиболее привилегированных групп в Active Directory, но и к любым учетным записям, которым были делегированы права и разрешения, которые позволяют выполнять административные задачи.  
  
Эти учетные записи могут быть учетными записями службы поддержки, которые имеют возможность сбрасывать пароли для большинства пользователей в домене, учетные записи, используемые для администрирования записей и зон DNS, а также учетные записи, используемые для управления конфигурацией. Защищенные административные узлы предназначены для административных функций и не запускают программное обеспечение, например приложения электронной почты, веб-браузеры или программное обеспечение, например Microsoft Office.  
  
Несмотря на то что наиболее строго защищенные учетные записи и группы должны быть наиболее строгими, это не устраняет необходимость защищать учетные записи и группы, которым были предоставлены привилегии, превышающие учетные записи обычных пользователей.  
  
Защищенный административный узел может быть выделенной рабочей станцией, которая используется только для административных задач, рядового сервера, на котором выполняется роль сервера удаленный рабочий стол шлюза и к которому пользователи подключаются для выполнения администрирования конечных узлов, или сервера, на котором работает роль Hyper-V, и предоставляет уникальную виртуальную машину для каждого пользователя, который будет использовать для своих административных задач. Во многих средах могут быть реализованы сочетания всех трех подходов.  
  
Для реализации защищенных административных узлов требуется планирование и настройка, которые соответствуют размеру вашей организации, рекомендациям по администрированию, риску аппетит и бюджету. Рекомендации и варианты реализации защищенных административных узлов приведены здесь для использования в разработке административной стратегии, подходящей для вашей организации.  
  
## <a name="principles-for-creating-secure-administrative-hosts"></a>Принципы создания безопасных административных узлов  
Для эффективного защиты систем от атак необходимо учитывать несколько общих принципов.  
  
1.  Не следует администрировать доверенную систему (то есть безопасный сервер, такой как контроллер домена) с менее доверенного узла (т. е. рабочей станции, которая не защищена тем же уровнем, что и управляемые ими системы).  
  
2.  При выполнении привилегированных действий не следует полагаться на один фактор проверки подлинности. Это означает, что сочетания имени пользователя и пароля не следует рассматривать как приемлемую проверку подлинности, поскольку представлен только один фактор (что известно). Следует учитывать, где создаются и кэшируются учетные данные или хранятся в административных сценариях.  
  
3.  Хотя большинство атак в текущей ландшафте угроз используют вредоносные и вредоносные атаки, не следует опускать физическую безопасность при проектировании и реализации безопасных административных узлов.  
  
### <a name="account-configuration"></a>Настройка учетной записи  
Даже если ваша организация в настоящее время не использует смарт-карты, следует рассмотреть возможность их реализации для привилегированных учетных записей и безопасных административных узлов. Узлы администрирования должны быть настроены так, чтобы требовать вход с помощью смарт-карты для всех учетных записей, изменив следующий параметр в объекте групповой политики, связанном с подразделениями, содержащими административные узлы:  
  
**Компьютер \ политики \ \ локальные \ политики \ Оптионс\интерактиве вход: требовать смарт-карту**  
  
Этот параметр требует, чтобы все интерактивные входы использовали смарт-карту независимо от конфигурации отдельной учетной записи в Active Directory.  
  
Кроме того, следует настроить защищенные административные узлы, разрешив вход только в разрешенные учетные записи, которые можно настроить в:  
  
**Компьютер \ конфигурация \ локальные политики \ политики \ локальные политики \ назначение прав Policies\User**  
  
Это позволяет интерактивным (и, при необходимости, службы удаленных рабочих столов) права входа только для полномочных пользователей защищенного административного узла.  
  
### <a name="physical-security"></a>Физическая безопасность  
Чтобы узлы администрирования считались надежными, они должны быть настроены и защищены в том же степени, что и управляемые ими системы. Большинство рекомендаций по [защите контроллеров домена от атак](../../../ad-ds/plan/security-best-practices/Securing-Domain-Controllers-Against-Attack.md) также применимо к узлам, которые используются для администрирования контроллеров домена и базы данных AD DS. Одной из проблем реализации безопасных административных систем в большинстве сред является то, что физическая безопасность может быть сложнее в реализации, поскольку эти компьютеры часто находятся в областях, которые не так безопасны, как серверы, размещенные в центрах обработки данных, например, Настольные пользователи.  
  
Физическая безопасность включает управление физическим доступом к административным узлам. В небольшой организации это может означать, что вы используете выделенную административную рабочую станцию, которая остается заблокированной в офисе или стационарном ящике, когда она не используется. Или это может означать, что если вам нужно выполнить администрирование Active Directory или контроллеров домена, вы можете войти непосредственно в контроллер домена.  
  
В организациях среднего размера можно реализовать безопасные административные серверы, находящиеся в защищенном расположении в офисе и используемые при необходимости управления Active Directory или контроллерами домена. Вы также можете реализовать рабочие станции администрирования, заблокированные в безопасных расположениях, когда они не используются, с серверами переходов или без них.  
  
В больших организациях можно развертывать серверы переходов, размещенные в центре обработки данных, которые обеспечивают строго контролируемый доступ к Active Directory; контроллеры домена; файлы, принтеры и серверы приложений. Реализация архитектуры сервера переходов, скорее всего, включает в себя сочетание защищенных рабочих станций и серверов в крупных средах.  
  
Независимо от размера организации и структуры административных узлов, необходимо защитить физические компьютеры от несанкционированного доступа или кражи и использовать шифрование диска BitLocker для шифрования и защиты дисков на узлах администрирования. При реализации BitLocker на узлах администрирования даже в случае кражи узла или удаления его дисков можно гарантировать недоступность данных на диске неавторизованным пользователям.  
  
### <a name="operating-system-versions-and-configuration"></a>Версии и конфигурация операционной системы  
Все административные узлы (серверы или рабочие станции) должны запустить последнюю операционную систему, используемую в Организации, по причинам, описанным выше в этом документе. Выполняя текущие операционные системы, ваши административные сотрудники получат преимущества от новых функций безопасности, полной поддержки поставщиков и дополнительных функций, появившихся в операционной системе. Более того, при оценке новой операционной системы, предварительно развернув ее на административные узлы, необходимо ознакомиться с новыми возможностями, параметрами и механизмами управления, которые он предлагает, что впоследствии можно будет использовать при планировании более широкого развертывания операционной системы. В этом случае наиболее сложные пользователи в организации также будут пользователями, знакомыми с новой операционной системой и которые лучше подходят для ее поддержки.  
  
### <a name="microsoft-security-configuration-wizard"></a>Мастер настройки безопасности Майкрософт  
При реализации серверов переходов в рамках стратегии административного размещения следует использовать встроенный мастер настройки безопасности, чтобы настроить параметры службы, реестра, аудита и брандмауэра, чтобы уменьшить контактную зону для атак сервера. После сбора и настройки параметров конфигурации мастера настройки безопасности параметры можно преобразовать в объект групповой политики, который используется для обеспечения единообразной базовой конфигурации на всех серверах переходов. Можно дополнительно изменить объект групповой политики, чтобы реализовать параметры безопасности, относящиеся к серверам переходов, и объединить все параметры с дополнительными базовыми параметрами, извлеченными из диспетчера соответствия требованиям безопасности Майкрософт.  
  
### <a name="microsoft-security-compliance-manager"></a>Microsoft Security Compliance Manager  
[Диспетчер соответствия безопасности Microsoft](https://technet.microsoft.com/library/cc677002.aspx) — это бесплатное средство, которое интегрирует конфигурации безопасности, рекомендованные корпорацией Майкрософт, в зависимости от версии операционной системы и конфигурации ролей, а также собирает их в одном средстве и пользовательском интерфейсе, который можно использовать для создания и настройки базовых параметров безопасности для контроллеров домена. Шаблоны диспетчера соответствия безопасности (Майкрософт) можно сочетать с параметрами мастера настройки безопасности для создания комплексных базовых показателей конфигурации для серверов переходов, развернутых и принудительно применяемых объектами групповой политики, развернутыми в подразделениях, в которых расположены серверы переходов в Active Directory.  
  
> [!NOTE]  
> На момент написания этой статьи диспетчер соответствия безопасности Майкрософт не включает параметры, относящиеся к серверам переходов или другим защищенным административным узлам, но по-прежнему можно использовать диспетчер соответствия безопасности (SCM) для создания начальных базовых показателей для административных узлов. Однако для правильной защиты узлов следует применять дополнительные параметры безопасности, подходящие для высокозащищенных рабочих станций и серверов.  
  
### <a name="applocker"></a>AppLocker  
Административные узлы и виртуальные мачинесшаулд должны быть настроены с помощью сценариев, средств и добавляются приложений с помощью AppLocker или стороннего программного обеспечения для ограничения приложений. Все административные приложения или служебные программы, которые не соответствуют защищенным параметрам, должны быть обновлены или заменены инструментами, которые придерживаются к обеспечению безопасности при разработке и администрировании. Если на административном узле требуется создать новые или дополнительные средства, необходимо тщательно протестировать приложения и служебные программы, а если средства подходят для развертывания на узлах администрирования, их можно добавить в добавляются системы.  
  
### <a name="rdp-restrictions"></a>Ограничения RDP  
Хотя конкретная конфигурация зависит от архитектуры систем администрирования, следует включить ограничения на то, какие учетные записи и компьютеры можно использовать для установления подключения протокол удаленного рабочего стола (RDP) к управляемым системам, например, с помощью серверов переходов шлюза удаленный рабочий стол (шлюз удаленных рабочих столов) для контроля доступа к контроллерам домена и другим управляемым системам от полномочных пользователей и систем.  
  
Необходимо разрешить интерактивный вход с помощью полномочных пользователей, а также удалить или даже заблокировать другие типы входа, которые не требуются для доступа к серверу.  
  
### <a name="patch-and-configuration-management"></a>Управление исправлениями и конфигурациями  
В небольших организациях могут полагаться предложения, такие как Центр обновления Windows или [Windows Server Update Services](https://technet.microsoft.com/windowsserver/bb332157) (WSUS) для управления развертыванием обновлений в системах Windows, в то время как крупные организации могут реализовать программное обеспечение для управления обновлениями и конфигурацией предприятия, такое как Microsoft Endpoint Configuration Manager. Независимо от механизмов, используемых для развертывания обновлений на общем сервере и в совокупности рабочих станций, следует рассмотреть отдельные развертывания для высокозащищенных систем, таких как контроллеры домена, центры сертификации и административные узлы. Выделяя эти системы от общей инфраструктуры управления, если программное обеспечение управления или учетные записи служб скомпрометированы, компромисс не может быть легко расширен до наиболее безопасных систем в инфраструктуре.  
  
Несмотря на то, что не следует реализовывать процессы обновления вручную для защиты систем, следует настроить отдельную инфраструктуру для обновления безопасных систем. Даже в очень больших организациях эту инфраструктуру обычно можно реализовать с помощью выделенных серверов WSUS и объектов групповой политики для защищенных систем.  
  
### <a name="blocking-internet-access"></a>Блокирование доступа к Интернету  
Административные узлы не должны иметь разрешения на доступ к Интернету и не должны иметь возможность просматривать интрасеть Организации. Веб-браузеры и аналогичные приложения не должны разрешаться на узлах администрирования. Вы можете заблокировать доступ к Интернету для защищенных узлов, используя сочетание параметров брандмауэра периметра, конфигурации с ПОВЫШЕНной защитой и конфигурации прокси-сервера "Черная дыра" на защищенных узлах. Можно также использовать список разрешений приложений, чтобы предотвратить использование веб-браузеров на узлах администрирования.  
  
### <a name="virtualization"></a>Виртуализация  
Там, где это возможно, рассмотрите возможность реализации виртуальных машин в качестве административных узлов. С помощью виртуализации можно создавать централизованно хранимые и управляемые административные системы для отдельных пользователей, а также легко завершать работу, если они не используются. Это гарантирует, что учетные данные не останутся активными в административных системах. Вы также можете потребовать, чтобы виртуальные узлы администрирования были сброшены на исходный моментальный снимок после каждого использования, гарантируя, что виртуальные машины останутся поддерживалась. Дополнительные сведения о параметрах виртуализации административных узлов приведены в следующем разделе.  
  
## <a name="sample-approaches-to-implementing-secure-administrative-hosts"></a>Примеры подходов к реализации безопасных административных узлов  
Независимо от того, как вы разрабатываете и развертываете административную инфраструктуру узлов, следует помнить о рекомендациях, описанных в разделе «принципы создания защищенных административных узлов» выше в этой статье. Каждый из описанных здесь подходов содержит общие сведения о том, как можно разделить «административные» и «производительные» системы, используемые ИТ-специалистами. Системы повышения производительности — это компьютеры, которые ИТ – администраторы используют для проверки электронной почты, просмотра Интернета и использования общего программного обеспечения, например Microsoft Office. Системы администрирования — это компьютеры, которые зафиксированы и предназначены для использования при повседневном администрировании ИТ-среды.  
  
Самый простой способ реализации защищенных административных узлов — предоставить ИТ-специалистам защищенные рабочие станции, с помощью которых можно выполнять административные задачи. В реализации, предназначенной только для рабочих станций, каждая рабочая станция администрирования используется для запуска средств управления и подключений RDP для управления серверами и другой инфраструктурой. Реализации только рабочих станций могут быть эффективны в небольших организациях, хотя более крупные и более сложные инфраструктуры могут использовать распределенный дизайн для административных узлов, в которых используются выделенные административные серверы и рабочие станции, как описано в разделе "реализация безопасных административных рабочих станций и серверов перебора" Далее в этом подразделе.  
  
### <a name="implementing-separate-physical-workstations"></a>Реализация отдельных физических рабочих станций  
Одним из способов реализации административных узлов является выдача каждого пользователя с двух рабочих станций. Одна рабочая станция используется с обычной учетной записью пользователя для выполнения таких действий, как проверка электронной почты и использование приложений для повышения производительности, тогда как вторая рабочая станция выделяется исключительно административными функциями.  
  
Для рабочей станции ИТ-специалистов можно использовать обычные учетные записи пользователей вместо использования привилегированных учетных записей для входа на незащищенные компьютеры. На рабочей станции администрирования должна быть настроена жестко Управляемая конфигурация, и ИТ-специалисты должны использовать другую учетную запись для входа на рабочую станцию администратора.  
  
Если вы реализовали смарт-карты, рабочие станции администратора должны быть настроены на требование входа с помощью смарт-карт, а ИТ-персонал должен иметь отдельные учетные записи для административного использования, также настроенные для запроса интерактивного входа в систему. Административный узел следует зафиксировать, как описано выше, и только назначенные ему пользователи должны иметь право локального входа на рабочую станцию.  
  
#### <a name="pros"></a>Плюсы  
Путем реализации отдельных физических систем можно обеспечить правильную настройку каждого компьютера для своей роли и то, что пользователи не могут случайно предоставить административные системы риску.  
  
#### <a name="cons"></a>Минусы  
  
-   Реализация отдельных физических компьютеров увеличивает расходы на оборудование.  
  
-   Вход на физический компьютер с учетными данными, используемыми для администрирования удаленных систем, кэширует учетные данные в памяти.  
  
-   Если административные рабочие станции не хранятся безопасно, они могут быть уязвимы для взлома с помощью таких механизмов, как физические средства ведения журнала ключей оборудования или другие физические атаки.  
  
### <a name="implementing-a-secure-physical-workstation-with-a-virtualized-productivity-workstation"></a>Реализация безопасной физической рабочей станции с виртуализованной рабочей станцией  
При таком подходе пользователи получают защищенную административную рабочую станцию, с помощью которой можно выполнять повседневные административные функции, используя средства удаленного администрирования сервера (RSAT) или RDP-подключения к серверам в пределах их области ответственности. Когда пользователям необходимо выполнять задачи по повышению производительности, они могут подключаться через RDP к удаленной рабочей станции, работающей в качестве виртуальной машины. Для каждой рабочей станции следует использовать отдельные учетные данные, а такие элементы управления, как смарт-карты, должны быть реализованы.  
  
#### <a name="pros"></a>Плюсы  
  
-   Рабочие станции и рабочие станции с повышенной производительностью разделены.  
  
-   Сотрудники отдела ИТ, использующие защищенные рабочие станции для подключения к рабочим станциям, могут использовать отдельные учетные данные и смарт-карты, а привилегированные учетные данные — не на менее защищенном компьютере.  
  
#### <a name="cons"></a>Минусы  
  
-   Для реализации решения требуется работа с проектированием и реализацией, а также надежные варианты виртуализации.  
  
-   Если физические рабочие станции не хранятся безопасно, они могут быть уязвимы для физических атак, которые нарушают оборудование или операционную систему и делают их уязвимыми для перехвата связи.  
  
### <a name="implementing-a-single-secure-workstation-with-connections-to-separate-productivity-and-administrative-virtual-machines"></a>Реализация одной защищенной рабочей станции с подключением к отдельным виртуальным машинам "производительность" и "административная"  
При таком подходе вы можете выдать ИТ-пользователям одну физическую рабочую станцию, которая заблокирована, как описано выше, и на которой у ИТ-пользователей нет привилегированного доступа. Вы можете предоставить службы удаленных рабочих столов подключения к виртуальным машинам, размещенным на выделенных серверах, предоставив ИТ-персоналу одну виртуальную машину, на которой выполняется электронная почта и другие приложения для повышения производительности, и вторую виртуальную машину, настроенную как выделенный административный узел пользователя.  
  
Для виртуальных машин требуется смарт-карта или другое многофакторное входное подключение с использованием отдельных учетных записей, отличных от учетной записи, используемой для входа на физический компьютер. После входа пользователя на физический компьютер он может использовать смарт-карту производительности для подключения к удаленному компьютеру с высокой производительностью и отдельную учетную запись и смарт-карту для подключения к удаленному административному компьютеру.  
  
#### <a name="pros"></a>Плюсы  
  
-   Пользователи могут использовать одну физическую рабочую станцию.  
  
-   Если требуется отдельная учетная запись для виртуальных узлов и использование службы удаленных рабочих столов подключений к виртуальным машинам, учетные данные пользователей не кэшируются в памяти на локальном компьютере.  
  
-   Физический узел может быть защищен в той же степени, что и административные узлы, что снижает вероятность компрометации локального компьютера.  
  
-   В случаях, когда может быть скомпрометирована виртуальная машина ИТ-среды или ее административная виртуальная машина, можно легко сбросить виртуальную машину до "известного хорошего" состояния.  
  
-   Если физический компьютер скомпрометирован, привилегированные учетные данные не кэшируются в памяти, а использование смарт-карт может препятствовать компрометации учетных данных с помощью средств ведения журнала нажатия клавиш.  
  
#### <a name="cons"></a>Минусы  
  
-   Для реализации решения требуется работа с проектированием и реализацией, а также надежные варианты виртуализации.  
  
-   Если физические рабочие станции не хранятся безопасно, они могут быть уязвимы для физических атак, которые нарушают оборудование или операционную систему и делают их уязвимыми для перехвата связи.  
  
### <a name="implementing-secure-administrative-workstations-and-jump-servers"></a>Реализация безопасных административных рабочих станций и серверов переходов  
В качестве альтернативы безопасности рабочих станций администрирования или в сочетании с ними можно реализовать безопасные серверы переходов, а пользователи могут подключаться к серверам переходов с помощью RDP и смарт-карт для выполнения административных задач.  
  
Серверы переходов должны быть настроены для запуска роли шлюза удаленный рабочий стол, что позволяет реализовать ограничения на подключения к серверу переходов и к целевым серверам, которые будут управляться из него. Если это возможно, необходимо также установить роль Hyper-V и создать [личные виртуальные рабочие столы](https://technet.microsoft.com/library/dd759174.aspx) или другие виртуальные машины для каждого пользователя, чтобы пользователи с правами администратора могли использовать их для своих задач на серверах переходов.  
  
Предоставляя администраторам пользователей виртуальные машины для пользователей на сервере переходов, вы обеспечиваете физическую безопасность для рабочих станций администратора, а пользователи могут сбрасывать или завершать работу виртуальных машин, когда они не используются. Если вы предпочитаете не устанавливать роль Hyper-V и роль шлюза удаленный рабочий стол на одном и том же административном узле, их можно установить на разных компьютерах.  
  
Там, где это возможно, для управления серверами следует использовать средства удаленного администрирования. Функция средства удаленного администрирования сервера (RSAT) должна быть установлена на виртуальных машинах пользователей (или на сервере переходов, если для администрирования не реализованы виртуальные машины для отдельных пользователей), а административный персонал должен подключаться по протоколу RDP к виртуальным машинам для выполнения административных задач.  
  
В случаях, когда пользователь с правами администратора должен подключиться к целевому серверу по протоколу RDP для непосредственного управления, шлюз удаленных рабочих столов должен быть настроен таким образом, чтобы подключение было разрешено только в том случае, если для установления соединения с целевым сервером используется соответствующий пользователь и компьютер. Выполнение средств RSAT (или аналогичных) должно быть запрещено в системах, не являющихся назначенными системами управления, например на рабочих станциях общего пользования и рядовых серверах, которые не переходят на серверы.  
  
#### <a name="pros"></a>Плюсы  
  
-   Создание серверов переходов позволяет сопоставлять определенные серверы с зонами (наборами систем с аналогичными требованиями к конфигурации, подключению и безопасности) в сети и требовать, чтобы администрирование каждой зоны достигается административным персоналом, подключающимся с защищенных административных узлов к назначенному серверу "зона".  
  
-   Сопоставление серверов переходов с зонами позволяет реализовать детализированные элементы управления для свойств подключения и требований к конфигурации, а также легко находить попытки подключения из неавторизованных систем.  
  
-   Реализация виртуальных машин для каждого администратора на серверах переходов обеспечивает принудительное завершение работы и сброс виртуальных машин до известного чистого состояния при завершении административных задач. Принудительное завершение работы (или перезапуск) виртуальных машин при завершении административных задач не может быть назначено злоумышленниками, а атаки путем кражи учетных данных могут оказаться невозможными, так как кэшированные в памяти учетные данные не сохраняются после перезагрузки.  
  
#### <a name="cons"></a>Минусы  
  
-   Выделенные серверы необходимы для серверов переходов, физических или виртуальных.  
  
-   Реализация назначенных серверов переходов и рабочих станций администрирования требует тщательного планирования и настройки, сопоставленных с любыми зонами безопасности, настроенными в среде.  
  


