---
title: Настройка шаблона сертификата сервера
description: Этот раздел является частью руководства развертывание сервера сертификатов для развертывания беспроводных и проводных сетей 802.1 X
manager: brianlic
ms.topic: article
ms.assetid: 8ff610e2-43ca-407f-a828-06d9366e02f0
ms.prod: windows-server-threshold
ms.technology: networking
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 238579c945821d19e45dad7e623450d598830596
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2019
ms.locfileid: "59886125"
---
# <a name="configure-the-server-certificate-template"></a>Настройка шаблона сертификата сервера

>Относится к: Windows Server (полугодовой канал), Windows Server 2016

Можно использовать эту процедуру для настройки шаблона сертификата Active Directory&reg; использует сертификат службы (AD CS) в качестве основы для сертификатов сервера, которые зарегистрированы для серверов в сети.  
  
При настройке этого шаблона, можно указать серверы группе Active Directory, должно автоматически получать сертификат сервера из AD CS.   
  
Описанная ниже процедура включает в себя инструкции по настройке шаблона для выдачи сертификатов, чтобы все следующие типы серверов:  
  
- Серверы, работающие со службой удаленного доступа, включая серверы шлюза RAS, которые являются членами **серверы RAS и IAS** группы.  
- Серверы, работающих под управлением службы сервера политики сети (NPS), которые являются членами **серверы RAS и IAS** группы.  
  
Членство в обоих **"Администраторы предприятия"** и корневого домена **"Администраторы домена"** группе является минимальным требованием для выполнения этой процедуры.  
  
### <a name="to-configure-the-certificate-template"></a>Чтобы настроить шаблон сертификата  
  
1.  На CA1, в диспетчере серверов щелкните **средства**, а затем нажмите кнопку **сертификации**. Открывает сертификации центра консоли управления (MMC).  
  
2.  Щелкните правой кнопкой мыши в консоли MMC, дважды щелкните имя ЦС **шаблонов сертификатов**, а затем нажмите кнопку **управление**.  
  
3.  Откроется консоль шаблонов сертификатов. В области сведений отображаются все шаблоны сертификатов.  
  
4.  В области сведений щелкните **RAS и IAS-сервер** шаблона.  
  
5.  Нажмите кнопку **действие** меню, а затем щелкните **скопировать шаблон**. Шаблон **свойства** откроется диалоговое окно.  
  
6.  Откройте вкладку **Безопасность**.   
  
7.  На **безопасности** на вкладке **имена групп или пользователей**, нажмите кнопку **серверы RAS и IAS**.  
  
8.  В **разрешения для серверов RAS и IAS**в разделе **Разрешить**, убедитесь, что **регистрация** , а затем кнопку **автоматическая подача заявок** проверки поле. Нажмите кнопку **ОК**и закройте консоль MMC шаблоны сертификатов.  
  
9.  В консоли Управления центра сертификации щелкните **шаблонов сертификатов**. На **действие** последовательно выберите пункты **New**, а затем нажмите кнопку **Выдаваемый шаблон сертификата**. **Включение шаблонов сертификатов** откроется диалоговое окно.  
  
10. В **Включение шаблонов сертификатов**, щелкните имя шаблона сертификата, который вы только что настроен и нажмите кнопку **ОК**. Например, если вы не изменяли имя шаблона сертификата по умолчанию, щелкните **копия RAS и IAS-сервер**, а затем нажмите кнопку **ОК**.  
  

