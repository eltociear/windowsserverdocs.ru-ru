---
ms.assetid: 3d770385-9834-4ebe-b66c-b684e0245971
title: Создание правила для разрешения или запрета пользователям на основании входящего утверждения
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 7d6be5b9194060bb16673e01e0fee8b36b081769
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/08/2020
ms.locfileid: "80816817"
---
# <a name="create-a-rule-to-permit-or-deny-users-based-on-an-incoming-claim"></a>Создание правила для разрешения или запрета пользователям на основании входящего утверждения 


В Windows Server 2016 можно использовать **политику управления доступом** для создания правила, которое позволяет или запрещать пользователям на основе входящего утверждения.  В Windows Server 2012 R2 с использованием шаблона " **Разрешить или запретить пользователей", основанного на входящем** шаблоне правила утверждений в службы федерации Active Directory (AD FS) \(AD FS\), можно создать правило авторизации, которое будет предоставлять или запрещать доступ пользователя к проверяющей стороне на основе типа и значения входящего утверждения. 

Например, с помощью этого правила можно создать правило, которое позволит получить доступ к проверяющей стороне только пользователям с утверждением группы со значением "Администраторы домена". Если вы хотите предоставить всем пользователям доступ к проверяющей стороне, используйте политику разрешения доступа ко **всем** пользователям или шаблон правило **разрешения всех пользователей** в зависимости от используемой версии Windows Server. Пользователи, которым разрешен доступ к проверяющей стороне из службы федерации, все еще могут получить отказ в обслуживании проверяющей стороной.  
  
Следующую процедуру можно использовать для создания правила утверждения с\-оснастки управления AD FS в.  
  
Для выполнения этой процедуры требуется членство в группе **Администраторы** или в эквивалентной группе на локальном компьютере.  Просмотрите сведения об использовании соответствующих учетных записей и членстве в группах в [локальной среде и группах домена по умолчанию](https://go.microsoft.com/fwlink/?LinkId=83477).  

## <a name="to-create-a-rule-to-permit-users-based-on-an-incoming-claim-on-windows-server-2016"></a>Создание правила, разрешив пользователям на основе входящего утверждения в Windows Server 2016
 
1.  В диспетчер сервера щелкните **Сервис**, а затем выберите **AD FS управление**.  
  
2.  В дереве консоли в разделе **AD FS**щелкните **политики управления доступом**. 
](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny3.PNG) ![создания правила

3. Щелкните правой кнопкой мыши и выберите **Добавить политику управления доступом**.
](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny4.PNG) ![создания правила

4. В поле Имя введите имя политики, описание и нажмите кнопку **Добавить**.
](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny5.PNG) ![создания правила

5. В **редакторе правил**в разделе Пользователи Поместите флажок **с конкретными утверждениями в запросе** и щелкните подчеркнутый **в нижней** части.
](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny6.PNG) ![создания правила

6. На экране **Выбор утверждений** щелкните переключатель **утверждения** , выберите **тип утверждения**, **оператор**и **значение утверждения** , а затем нажмите кнопку **ОК**.
](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny7.PNG) ![создания правила

7.  В **редакторе правил** нажмите кнопку **ОК**.  На экране **Добавить политику управления доступом** нажмите кнопку **ОК**.

8. В дереве консоли **управления AD FS** в разделе **AD FS**щелкните **отношения доверия с проверяющей стороной**. 
](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule9.PNG) ![создания правила

9.  Щелкните правой кнопкой мыши **отношение доверия с проверяющей стороной** , к которому требуется предоставить доступ, и выберите пункт **изменить политику управления доступом**.  
](media/Create-a-Rule-to-Permit-All-Users/permitall2.PNG) ![создания правила

10. В политике управления доступом выберите политику, а затем нажмите кнопку **Применить** и **ОК**.
](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny8.PNG) ![создания правила

## <a name="to-create-a-rule-to-deny-users-based-on-an-incoming-claim-on-windows-server-2016"></a>Создание правила для запрета доступа пользователей на основе входящего утверждения в Windows Server 2016
 
1.  В диспетчер сервера щелкните **Сервис**, а затем выберите **AD FS управление**.  
  
2.  В дереве консоли в разделе **AD FS**щелкните **политики управления доступом**. 
](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny3.PNG) ![создания правила

3. Щелкните правой кнопкой мыши и выберите **Добавить политику управления доступом**.
](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny4.PNG) ![создания правила

4. В поле Имя введите имя политики, описание и нажмите кнопку **Добавить**.
](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny9.PNG) ![создания правила

5. В **редакторе правил**убедитесь, что выбран параметр все все, а в разделе **за исключением** установите флажок **с конкретными утверждениями в запросе** и щелкните подчеркнутое **в нижней** части.
](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny10.PNG) ![создания правила

6. На экране **Выбор утверждений** щелкните переключатель **утверждения** , выберите **тип утверждения**, **оператор**и **значение утверждения** , а затем нажмите кнопку **ОК**.
](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny11.PNG) ![создания правила

7.  В **редакторе правил** нажмите кнопку **ОК**.  На экране **Добавить политику управления доступом** нажмите кнопку **ОК**.

8. В дереве консоли **управления AD FS** в разделе **AD FS**щелкните **отношения доверия с проверяющей стороной**. 
](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule9.PNG) ![создания правила

9.  Щелкните правой кнопкой мыши **отношение доверия с проверяющей стороной** , к которому требуется предоставить доступ, и выберите пункт **изменить политику управления доступом**.  
](media/Create-a-Rule-to-Permit-All-Users/permitall2.PNG) ![создания правила

10. В политике управления доступом выберите политику, а затем нажмите кнопку **Применить** и **ОК**.
](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny12.PNG) ![создания правила

  
## <a name="to-create-a-rule-to-permit-or-deny-users-based-on-an-incoming-claim-on-windows-server-2012-r2"></a>Создание правила разрешения или запрета доступа пользователей на основе входящего утверждения в Windows Server 2012 R2
  
1.  В диспетчер сервера щелкните **Сервис**, а затем выберите **AD FS управление**.    
  
2.  В дереве консоли в разделе **AD FS\\отношения доверия\\отношения доверия с проверяющей стороной**щелкните определенное отношение доверия в списке, в котором вы хотите создать это правило.  
  
3.  Справа\-щелкните выбранное отношение доверия, а затем щелкните **изменить правила утверждений**.  
](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule6.PNG) ![создания правила   

4.  В диалоговом окне **изменение правил утверждений** перейдите на вкладку **правила авторизации выдачи** или на вкладку **правила авторизации делегирования** \(в зависимости от типа правила авторизации, которое требуется\), а затем нажмите кнопку **Добавить правило** , чтобы запустить **Мастер добавления правила для утверждения авторизации**.  
](media/Create-a-Rule-to-Permit-All-Users/permitall5.PNG) ![создания правила

5.  На странице **Выбор шаблона правила** в разделе **шаблон правила утверждения**выберите **Разрешить или запретить пользователям на основе входящего утверждения** из списка, а затем нажмите кнопку **Далее**.  
](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny1.PNG) ![создания правила

6.  На странице **Настройка правила** в разделе **имя правила утверждения** введите отображаемое имя для этого правила в поле **тип входящего утверждения** выберите тип утверждения в списке, в разделе **значение входящего утверждения** введите значение или нажмите кнопку Обзор \(если оно доступно\) и выберите значение, а затем выберите один из следующих вариантов в зависимости от потребностей Организации.  
  
    -   **Разрешение доступа пользователям с этим входящим утверждением**  
  
    -   **Запретить доступ пользователям с этим входящим утверждением**  
](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny2.PNG) ![создания правила  
7.  Нажмите кнопку **Готово**.  
  
8.  В диалоговом окне **изменение правил утверждений** нажмите кнопку **ОК** , чтобы сохранить правило.  

## <a name="additional-references"></a>Дополнительная справка 
[Настройка правил для утверждения](Configure-Claim-Rules.md)  
 
[Контрольный список: создание правил утверждений для отношения доверия с проверяющей стороной](https://technet.microsoft.com/library/ee913578.aspx)  
  
[Когда следует использовать правило утверждения авторизации](../../ad-fs/technical-reference/When-to-Use-an-Authorization-Claim-Rule.md)  

[Роль утверждений](../../ad-fs/technical-reference/The-Role-of-Claims.md)  
  
[Роль правил утверждений](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md)  
