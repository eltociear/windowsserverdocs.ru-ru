---
ms.assetid: 475e34f9-9399-43f4-a840-9dd77258e11a
title: "Создание правила для отправки членства в группе как утверждения"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: d4fb03de9de2dcca36b18ce089db11ed599de820
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/12/2017
---
# <a name="create-a-rule-to-send-group-membership-as-a-claim"></a>Создание правила для отправки членства в группе как утверждения

>Область применения: Windows Server 2016, Windows Server 2012 R2

Используя отправлять членство в группе в качестве шаблона правил утверждений в \(AD FS\) служб федерации Active Directory, можно создать правило, которое позволит для выбора группы безопасности Active Directory для отправки в виде утверждений. Из этого правила на основе выбранной группы выбранного будут выдаваться только одно утверждение. Например можно использовать этот шаблон правила, чтобы создать правило, которое будет отправлять утверждение группы со значением Admin, если пользователь является членом группы безопасности "Администраторы домена". Это правило можно использовать только для пользователей в локальном домене Active Directory.  
  
Можно использовать следующую процедуру для создания правила утверждения с управления AD FS оснастка.  
  
Членство в группе **Администраторы**, или эквивалентной группе на локальном компьютере минимальным требованием для выполнения этой процедуры.  Подробные сведения об использовании соответствующих учетных записей и членстве в группах в [локальные и доменные группы по умолчанию ](https://go.microsoft.com/fwlink/?LinkId=83477).   

## <a name="to-create-a-rule-to-send-group-membership-as-a-claim-on-a-relying-party-trust-in-windows-server-2016"></a>Создание правила для отправки членства в группах как утверждения на доверия с проверяющей стороной в Windows Server 2016 

1.  В диспетчере серверов щелкните **средства**, а затем выберите **управления AD FS **.  
  
2.  В дереве консоли в разделе **AD FS**, нажмите кнопку **доверия с проверяющей стороной **. 
![Создание правила](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule9.PNG)  
  
3.  Щелкните правой кнопкой мыши выбранные доверия, а затем нажмите кнопку **изменение политики выдачи утверждений **.
![Создание правила](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule10.PNG)   
  
4.  В **изменение политики выдачи утверждений** диалогового окна **правила преобразования выдачи** щелкните **добавить правило** для запуска мастера создания правила. 
![Создание правила](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule11.PNG)    

5.  На **Выбор шаблона правила** в разделе **шаблон правила утверждения**выберите **отправлять членство в группе как утверждение** из списка и нажмите кнопку **Далее**.  
![Создание правила](media/Create-a-Rule-to-Send-Group-Membership-as-a-Claim/group3.PNG)      

6.   На **Настройка правила** в разделе **имя правила утверждений** введите отображаемое имя для этого правила в **группы пользователя** щелкните **Обзор** и выберите группу, в разделе **исходящие утверждения и тип** выберите тип требуемой утверждения и затем в разделе **тип исходящего утверждения** введите значение.
![Создание правила](media/Create-a-Rule-to-Send-Group-Membership-as-a-Claim/group4.PNG)   

7.  Нажмите кнопку **Готово** кнопки.  
  
8.  В **изменение правил для утверждений** диалоговом нажмите кнопку **ОК** чтобы сохранить правило.
  
## <a name="to-create-a-rule-to-to-send-group-membership-as-a-claim-on-a-claims-provider-trust-in-windows-server-2016"></a>Создание правила для отправки членства в группах как утверждения на доверия с поставщиком утверждений в Windows Server 2016 
  
1.  В диспетчере серверов щелкните **средства**, а затем выберите **управления AD FS **.  
  
2.  В дереве консоли в разделе **AD FS**, нажмите кнопку **отношения доверия поставщиков утверждений **. 
![Создание правила](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule1.PNG)  
  
3.  Щелкните правой кнопкой мыши выбранные доверия, а затем нажмите кнопку **изменение правил для утверждений **.
![Создание правила](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule2.PNG)   
  
4.  В **изменение правил для утверждений** диалогового окна **правила преобразования принятия** щелкните **добавить правило** для запуска мастера создания правила.
![Создание правила](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule3.PNG)    

5.  На **Выбор шаблона правила** в разделе **шаблон правила утверждения**выберите **отправлять членство в группе как утверждение** из списка и нажмите кнопку **Далее**.  
![Создание правила](media/Create-a-Rule-to-Send-Group-Membership-as-a-Claim/group3.PNG)     

6.   На **Настройка правила** в разделе **имя правила утверждений** введите отображаемое имя для этого правила в **группы пользователя** щелкните **Обзор** и выберите группу, в разделе **исходящие утверждения и тип** выберите тип требуемой утверждения и затем в разделе **тип исходящего утверждения** введите значение. 
![Создание правила](media/Create-a-Rule-to-Send-Group-Membership-as-a-Claim/group4.PNG)      

7.  Нажмите кнопку **Готово** кнопки.  
  
8.  В **изменение правил для утверждений** диалоговом нажмите кнопку **ОК** чтобы сохранить правило.  




  
## <a name="to-create-a-rule-to-send-group-membership-as-a-claim-in-windows-server-2012-r2"></a>Создание правила для отправки членства в группах как утверждения в Windows Server 2012 R2 
  
1.  В диспетчере серверов щелкните **средства**, а затем выберите **управления AD FS **.  
  
2.  В дереве консоли в разделе **отношения FS\\Trust AD**, выбрать пункт **отношения доверия поставщиков утверждений** или **доверия с проверяющей стороной**и нажмите кнопку определенных отношений доверия в списке, где вы хотите создать это правило.  
  
3.  Щелкните правой кнопкой мыши выбранные доверия, а затем нажмите кнопку **изменение правил для утверждений **.
![Создание правила](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule6.PNG)  
  
4.  В **изменение правил для утверждений** диалоговое окно "", выберите один следующих вкладок, в зависимости от доверия, что вы изменяете и правила, которые вы хотите создать это правило в и нажмите кнопку **добавить правило** для запуска мастера правил, который связан с этого набора правил:  
  
    -   **Правила преобразования принятия**  
  
    -   **Правила преобразования выдачи**  
  
    -   **Правила авторизации выдачи**  
  
    -   **Правила авторизации делегирования**  
![Создание правила](media/Create-a-Rule-to-Permit-All-Users/permitall5.PNG)
    
5.  На **Выбор шаблона правила** в разделе **шаблон правила утверждения**выберите **отправлять членство в группе как утверждение** из списка и нажмите кнопку **Далее**.  
![Создание правила](media/Create-a-Rule-to-Send-Group-Membership-as-a-Claim/group1.PNG)

6.  На **Настройка правила** в разделе **имя правила утверждений** введите отображаемое имя для этого правила в **группы пользователя** щелкните **Обзор** и выберите группу, в разделе **исходящие утверждения и тип** выберите тип требуемой утверждения и затем в разделе **тип исходящего утверждения** введите значение.  
![Создание правила](media/Create-a-Rule-to-Send-Group-Membership-as-a-Claim/group2.PNG)  

7.  Нажмите кнопку **Готово **.  
  
8.  В **изменение правил для утверждений** диалоговом нажмите кнопку **ОК** чтобы сохранить правило.  



## <a name="additional-references"></a>Дополнительные ссылки 
[Настройка правил для утверждения](Configure-Claim-Rules.md)  
 
[Контрольный список: Создание правил утверждений для отношений доверия с проверяющей стороной](https://technet.microsoft.com/library/ee913578.aspx)  

[Контрольный список: Создание правил утверждений для поставщика утверждений доверия](https://technet.microsoft.com/library/ee913564.aspx)  
  
[Когда следует использовать правило авторизации утверждений](../../ad-fs/technical-reference/When-to-Use-an-Authorization-Claim-Rule.md)  

[Роль утверждений](../../ad-fs/technical-reference/The-Role-of-Claims.md)  
  
[Роль правил утверждений](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md) 