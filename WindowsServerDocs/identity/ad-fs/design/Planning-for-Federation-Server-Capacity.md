---
ms.assetid: 7013fc21-9ced-4f9d-9588-cb04d6d60924
title: "Планирование емкости сервера федерации"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 618dc9419be965dedaaf7dc946da436a5001f121
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/03/2017
---
# <a name="planning-for-federation-server-capacity"></a>Планирование емкости сервера федерации

>Область применения: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Планирование емкости для серверов федерации поможет вам оценить.  
  
-   Какие факторы увеличения размера базы данных конфигурации AD FS.  
  
-   Соответствующим требованиям к оборудованию для каждого сервера федерации.  
  
-   Число серверов федерации, чтобы поместить в каждой организации.  
  
Серверы федерации выдачи маркеров безопасности для пользователей. Эти маркеры предоставляются проверяющую сторону для потребления. Серверы федерации токенов безопасности после проверки подлинности пользователя, или после получения маркера безопасности, который ранее был выдан службой федерации партнера. Маркер безопасности запрашивается из службы федерации после первоначального входа к федеративным приложениям или срок действия их маркеры безопасности, пока они получают доступ к федеративным приложениям.  
  
Серверы федерации предназначены для размещения сервера фермы сценарии высокой доступности, использующих технологию балансировки сетевой нагрузки Майкрософт \(NLB\). Серверы федерации в ферме конфигурации может обслуживать запросы независимо, без доступа к все общие компоненты фермы для каждого запроса. Таким образом не налагает излишних нагрузок, участвующие в масштабирование развертывания серверов федерации.  
  
**Рекомендации:**  
  
-   Для критически важных mission\ или развертываний сценарии высокой доступности, рекомендуется создать ферму серверов федерации небольшой в каждой партнерской организации с помощью по крайней мере два сервера федерации на каждой ферме, чтобы обеспечить отказоустойчивость.  
  
-   Необходимость в высокой доступности и простота масштабирования серверов федерации масштабирование — это рекомендуемый метод для обработки большого числа запросов в секунду для конкретной службы федерации. Масштабирование за базовую конфигурацию в данном руководстве вряд ли создают значительные емкости обработки прибыли.  
  
## <a name="ad-fs-configuration-database-size-and-growth"></a>Размер базы данных конфигурации AD FS и рост  
Размер базы данных конфигурации Служб федерации Active Directory обычно считается должен быть небольшим, и размер базы данных не оказываются основных следует учитывать при развертывании Служб федерации Active Directory.  Точный размер базы данных конфигурации AD FS можно основном зависят от количества отношений доверия и связанные метаданные, связанные с trust\ — например утверждений, правила утверждений и мониторинг параметров, настроенных для каждой доверия. Растет число записей доверия в базе данных конфигурации, то же самое происходит потребность больше места на диске.  
  
Дополнительные сведения о развертывании базы данных конфигурации AD FS, см. [некоторые аспекты топологии развертывания AD FS](AD-FS-Deployment-Topology-Considerations.md).  
  
## <a name="memory-cpu-and-disk-space-requirements"></a>Требования к пространству памяти, Процессора и диска  
К счастью требования к памяти, Процессора и диска пространства для серверов федерации скромных, и они не может быть движущие коэффициент решения об оборудовании. Дополнительные сведения о требованиях к оборудованию см. в разделе [приложение а. Общие сведения об AD FS требования](Appendix-A--Reviewing-AD-FS-Requirements.md).  
  
> [!NOTE]  
> В тестах, проведенных командой разработчиков AD FS, используя ферму серверов федерации с выделенным сервером SQL для хранения базы данных конфигурации Служб федерации Active Directory Общая нагрузка на сервере SQL Server обычно представляло собой низкой. В один тест с использованием фермы four\-federation\-server, который был настроен на использование одного SQL Server ЦП не превысили 10%, несмотря на результаты тестов, принесших цели использования серверов федерации.  
  
## <a name="bk_estimatefs"></a>Рассчитайте необходимое количество серверов федерации для вашей организации  
С целью упрощения процесса для серверов федерации планирования оборудования группы разработчиков AD FS разработала AD FS масштабов электронной таблице планирования емкости. Этой электронной таблицы Excel включает функции calculator\ типа, которое займет ожидаемого использования, предоставленные вами данные о пользователях в вашей организации и возвращать рекомендуемые оптимальное число серверов федерации для рабочей среды Служб федерации Active Directory.  
  
> [!NOTE]  
> Число серверов федерации, порекомендует этой электронной таблицей основана на спецификации аппаратной и сетевой группы разработчиков AD FS, используемые во время тестирования. Таким образом необходимо понимать число серверов федерации, порекомендует электронной таблицы в этом контексте.  Дополнительные сведения о спецификации, используемые во время тестирования см. в разделе под названием [Планирование емкости сервера AD FS](Planning-for-AD-FS-Server-Capacity.md).  
  
### <a name="using-the-ad-fs-capacity-planning-sizing-spreadsheet"></a>С помощью электронную таблицу масштабов для планирования емкости AD FS  
При использовании этой электронной таблицы, необходимо выбрать значение \ (либо **40%**, **60%**, или **80%**\), наилучшим образом представляет процент от общего числа пользователей, предполагается, что будет отправлять запросы на проверку подлинности на серверы федерации во время периодов пикового использования.  
  
Затем необходимо выбрать значение \ (либо **1 минута**, **15 минут**, или **1 час**\), наилучшим образом представляет время, предполагается, что период использования (пик) до последнего. Например вы оценить 40%, как значение общего числа пользователей, будет войти в систему в течение периода, равного 15 минутам, или 60% от пользователей будет войти в систему в течение периода 1 час. В совокупности эти значения определяют профиль пиковой нагрузки, с помощью которого будет вычисляться вашу рекомендацию изменения размера.  
  
Затем необходимо указать общее число пользователей, которым требуется единого входа на доступ к целевому приложению поддержкой claims\, зависимости от того, являются ли пользователи:  
  
-   Ведение журнала в Active Directory с локального компьютера, который физически подключен к корпоративной сети \ (с помощью встроенной authentication\ Windows)  
  
-   Ведение журнала в Active Directory удаленно с компьютера, который не подключен к корпоративной сети физически \ (через Windows встроенная проверка подлинности или имя пользователя и password\)  
  
-   Из другой организации, а также являются попытки доступа к в целевое приложение с поддержкой claims\ из ее доверенным партнером  
  
-   С помощью поставщика удостоверений SAML 2.0 и могут попытаться получить доступ к в целевое приложение с поддержкой claims\  
  
#### <a name="how-to-use-this-spreadsheet"></a>Использование этой электронной таблицы  
Можно использовать следующие действия для каждого экземпляра фермы серверов федерации, необходимо выполнить развертывание, чтобы определить Рекомендованное количество серверов федерации.  
  
1.  Загрузите и откройте [электронную таблицу масштабов AD FS с емкости планирование для Windows Server 2012 R2](https://adfsdocs.blob.core.windows.net/adfs/ADFSCapacityPlanning.xlsx) или [электронную таблицу масштабов AD FS с емкости планирование для Windows Server 2016](https://adfsdocs.blob.core.windows.net/adfs/ADFSCapacity2016.xlsx).
  
2.  В ячейке справа от **в течение периода пиковой загрузки системы использования ожидается, что этот процент Мои пользователям проходить проверку подлинности** сотовой связи, щелкните ячейку и затем выбрать свой уровень использования системные, либо с помощью стрелок раскрывающиеся **40%**, **60%** или **80%** для развертывания.  
  
3.  В ячейке справа от **в следующий период времени** сотовой связи, щелкните ячейку и затем выберите либо с помощью стрелок раскрывающиеся **1 минута**, **15 минут**, или **1 час** выберите длительность пиковой нагрузки.  
  
4.  В ячейке справа от **ввод предполагаемое количество внутренних приложений \ (например SharePoint \(2007 or 2010\) или утверждений учитывать web applications\)** сотовой связи, введите количество внутренних приложений, которые будут использоваться в вашей организации.  
  
5.  В ячейке справа от **ввод предполагаемое количество веб-приложений \ (например, Office 365 Exchange Online, SharePoint Online или Lync Online\)** сотовой связи, введите номер веб-приложений или услуг, вам нужно будет использовать в вашей организации.  
  
6.  В разделе под названием ячейки **число пользователей**, введите номер на каждую строку, которая применяется к пример сценария приложения пользователям будет необходимо единого входа на доступ к. В этом столбце должно содержать количество определенных пользователей, не максимальной нагрузки пользователей в секунду. Если попытки доступа к приложению должен пройти страница обнаружения домашней области, введите **Y**. Если вы не уверены, этот вариант, введите **Y**.  
  
7.  Примите во внимание следующие рекомендуемые значения, предоставляемые:  
  
    1.  Общее число серверов федерации рекомендуемые см. в нижней правой ячейку, выделены серым цветом.  
  
    2.  Количество серверов, рекомендуется для каждого сценария пример приложения см. ячейку в строке, выделены серым цветом.  
  
> [!NOTE]  
> Значение, которое будет автоматически вычисляется в ячейке справа от ячейки под названием **общее число серверов федерации рекомендуется** в нижней части электронной таблицы содержит формулу, который будет добавлять дополнительные буфера 20% в общую сумму всех значений в каждом из отдельных строк, перед ним. Формула, добавлены **общее число серверов федерации рекомендуется** ячейки сборки в этот буфер для вашей всего рекомендуемое число серверов федерации развернутой, чтобы сделать его очень маловероятно, что общая нагрузка на ферме никогда не будет достигнуть точкой насыщенности.  
  
## <a name="see-also"></a>См. также:
[Руководство по разработке служб AD FS в Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)