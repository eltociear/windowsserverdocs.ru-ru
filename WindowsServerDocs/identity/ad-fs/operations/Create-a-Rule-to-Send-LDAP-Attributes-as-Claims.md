---
ms.assetid: 66664b80-2590-46c0-bfca-82402088e42c
title: Создание правила для отправки атрибутов LDAP как утверждений
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 00ea4f9f868b9c82c2a0859be971db26394251a3
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/24/2019
ms.locfileid: "66189348"
---
# <a name="create-a-rule-to-send-ldap-attributes-as-claims"></a>Создание правила для отправки атрибутов LDAP как утверждений


С помощью отправлять атрибуты LDAP как шаблон правила утверждения в службах федерации Active Directory \(AD FS\), можно создать правило, которое будет выбрать атрибуты из Lightweight Directory Access Protocol \(LDAP\)хранилища атрибутов, например Active Directory, для отправки как утверждений проверяющей стороне. Например, можно использовать этот шаблон правила для создания отправлять атрибуты LDAP как утверждений правил, который извлекает значения атрибутов для прошедших проверку пользователей из **displayName** и **telephoneNumber** Active Каталог, атрибуты и затем отправить эти значения как два разных исходящих утверждения.  
  
Это правило также может использоваться для отправки сведений о членстве пользователя во всех группах. Если вы хотите отправить только членство в отдельных группах, используйте правило "Отправлять членство в группах как утверждения". Можно использовать следующую процедуру для создания правила утверждения с помощью оснастки управления AD FS\-в.  
  
Для выполнения этой процедуры минимальным требованием является членство в группе **Администраторы** или эквивалентные права на локальном компьютере.  Просмотрите сведения об использовании соответствующих учетных записей и членства в группах в [локальные и доменные группы по умолчанию](https://go.microsoft.com/fwlink/?LinkId=83477).  

## <a name="to-create-a-rule-to-send-ldap-attributes-as-claims-for-a-relying-party-trust-in-windows-server-2016"></a>Чтобы создать правило для отправки атрибутов LDAP как утверждений для проверяющей стороны в Windows Server 2016 

1.  В диспетчере серверов щелкните **средства**, а затем выберите **управления AD FS**.  
  
2.  В дереве консоли в разделе **AD FS**, нажмите кнопку **доверия проверяющей стороны**. 
![Создание правила](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule9.PNG)  
  
3.  Справа\-выберите выбранного отношения доверия и нажмите кнопку **изменить политику выдачи утверждений**.
![Создание правила](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule10.PNG)   
  
4.  В **изменить политику выдачи утверждений** диалогового **правила преобразования выдачи** щелкните **добавить правило** для запуска мастера создания правила. 
![Создание правила](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule11.PNG)    

5.  На **Выбор шаблона правила** раздела **шаблон правила утверждения**выберите **отправлять атрибуты LDAP как утверждений** в списке и нажмите кнопку **Далее**.  
![Создание правила](media/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims/ldap1.PNG)    

6.  На **Настройка правила** странице в разделе **имя правила утверждения** введите отображаемое имя для этого правила, выберите **Store атрибут**, а затем выберите атрибут LDAP и сопоставить их Тип исходящего утверждения. 
![Создание правила](media/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims/ldap2.PNG)    

7.  Нажмите кнопку **Готово** кнопки.  
  
8.  В **изменение правил для утверждений** диалоговом окне щелкните **ОК** сохранить правило.
  
## <a name="to-create-a-rule-to-send-ldap-attributes-as-claims-for-a-claims-provider-trust-in-windows-server-2016"></a>Чтобы создать правило для отправки атрибутов LDAP как утверждений для доверия поставщика утверждений в Windows Server 2016 
  
1.  В диспетчере серверов щелкните **средства**, а затем выберите **управления AD FS**.  
  
2.  В дереве консоли в разделе **AD FS**, нажмите кнопку **отношения доверия поставщиков утверждений**. 
![Создание правила](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule1.PNG)  
  
3.  Справа\-выберите выбранного отношения доверия и нажмите кнопку **изменение правил для утверждений**.
![Создание правила](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule2.PNG)   
  
4.  В **изменение правил для утверждений** диалогового **правила преобразования принятия** щелкните **добавить правило** для запуска мастера создания правила.
![Создание правила](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule3.PNG)    

5.  На **Выбор шаблона правила** раздела **шаблон правила утверждения**выберите **отправлять атрибуты LDAP как утверждений** в списке и нажмите кнопку **Далее**.  
![Создание правила](media/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims/ldap1.PNG)       

6.  На **Настройка правила** странице в разделе **имя правила утверждения** введите отображаемое имя для этого правила, выберите **Store атрибут**, а затем выберите атрибут LDAP и сопоставить их Тип исходящего утверждения. 
![Создание правила](media/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims/ldap2.PNG)      

7.  Нажмите кнопку **Готово** кнопки.  
  
8.  В **изменение правил для утверждений** диалоговом окне щелкните **ОК** сохранить правило.  

 
  
## <a name="to-create-a-rule-to-send-ldap-attributes-as-claims-for-windows-server-2012-r2"></a>Чтобы создать правило для отправки атрибутов LDAP как утверждений для Windows Server 2012 R2  
  
1.  В диспетчере серверов щелкните **средства**, а затем выберите **управления AD FS**.  
  
2.  В дереве консоли в разделе **AD FSAD FS\\отношения доверия**, нажать **отношения доверия поставщиков утверждений** или **доверия проверяющей стороны**, а затем нажмите кнопку определенные доверия в списке, где вы хотите создать это правило.  
  
3.  Справа\-выберите выбранного отношения доверия и нажмите кнопку **изменение правил для утверждений**.
![Создание правила](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule6.PNG)  
  
4.  В **изменение правил для утверждений** диалоговом окне выберите один следующие вкладки, в зависимости от отношения доверия, что вы изменяете и какие правила вы хотите создать это правило в и нажмите кнопку **добавить правило** для запуска правила Задайте мастер, который связан с этим правилом.  
  
    -   **Правила преобразования принятия**  
  
    -   **Правила преобразования выдачи**  
  
    -   **Правила авторизации выдачи**  
  
    -   **Правила авторизации делегирования**  
![Создание правила](media/Create-a-Rule-to-Permit-All-Users/permitall5.PNG) 
  
5.  На **Выбор шаблона правила** раздела **шаблон правила утверждения**выберите **отправлять атрибуты LDAP как утверждений** в списке и нажмите кнопку **Далее**.  
![Создание правила](media/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims/ldap3.PNG)  
  
6.  На **Настройка правила** странице в разделе **имя правила утверждения** введите отображаемое имя для этого правила в разделе **хранилище атрибутов** выберите **Active Directory**и в разделе **типы утверждений сопоставление атрибутов LDAP исходящее** выберите нужный **атрибут LDAP** и соответствующие **тип исходящего утверждения** типы в раскрывающемся\-списки.  
  
    Необходимо выбрать новый атрибут LDAP и исходящих парой тип утверждения в отдельной строке для каждого атрибута Active Directory, которую требуется одно утверждение выдается для как часть этого правила.  
![Создание правила](media/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims/ldap4.PNG)    
7.  Нажмите кнопку **Готово** кнопки.  
  
8.  В **изменение правил для утверждений** диалоговом окне щелкните **ОК** сохранить правило.  

## <a name="additional-references"></a>Дополнительная справка 
[Настройка правил для утверждения](Configure-Claim-Rules.md)  
 
[Контрольный список. Создание правил утверждений для отношений доверия с проверяющей стороной](https://technet.microsoft.com/library/ee913578.aspx)  

[Контрольный список. Создание правил утверждений для отношений доверия с поставщиком утверждений](https://technet.microsoft.com/library/ee913564.aspx)  
  
[Когда следует использовать Authorization Claim Rule](../../ad-fs/technical-reference/When-to-Use-an-Authorization-Claim-Rule.md)  

[Роль утверждений](../../ad-fs/technical-reference/The-Role-of-Claims.md)  
  
[Роль правил утверждений](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md)  