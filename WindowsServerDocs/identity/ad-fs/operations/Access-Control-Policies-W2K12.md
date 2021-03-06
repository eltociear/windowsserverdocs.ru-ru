---
ms.assetid: 5728847d-dcef-4694-9080-d63bfb1fe24b
title: Политики управления доступом в AD FS
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/05/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 7355ff9ed49a5e4ee8bca3a3d266a0ec1ecc0780
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/08/2020
ms.locfileid: "80814897"
---
# <a name="access-control-policies-in-windows-server-2012-r2-and-windows-server-2012-ad-fs"></a>Политики управления доступом в Windows Server 2012 R2 и Windows Server 2012 AD FS


Политики, описанные в этой статье, используют два типа утверждений.  

1.  Утверждения AD FS создаются на основе информации, которую AD FS и прокси веб-приложения могут проверять и проверять, например IP-адрес клиента, подключающегося напрямую к AD FS или WAP.  

2.  Утверждения AD FS создаются на основе сведений, пересылаемых клиентом в AD FS в виде HTTP-заголовков.  

>**Важно**. Политики, описанные ниже, блокируют сценарии приподключения к домену Windows 10 и сценариев входа, которым требуется доступ к следующим дополнительным конечным точкам.

AD FS конечных точек, необходимых для приподключения к домену Windows 10 и входа в систему
- [имя службы федерации]/ADFS/Services/Trust/2005/windowstransport
- [имя службы федерации]/ADFS/Services/Trust/13/windowstransport
- [имя службы федерации]/ADFS/Services/Trust/2005/usernamemixed
- [имя службы федерации]/ADFS/Services/Trust/13/usernamemixed 
- [имя службы федерации]/ADFS/Services/Trust/2005/certificatemixed
- [имя службы федерации]/ADFS/Services/Trust/13/certificatemixed

>**Важно**. конечные точки/ADFS/Services/Trust/2005/windowstransport и/ADFS/Services/Trust/13/windowstransport должны быть включены только для доступа к интрасети, так как они предназначены для конечных точек в интрасети, использующих привязку WIA на HTTPS. Предоставление доступа к экстрасети может позволить запросам к этим конечным точкам обходить защиту блокировок. Эти конечные точки должны быть отключены на прокси-сервере (т. е. отключены из экстрасети) для защиты блокировки учетных записей AD. 

Чтобы устранить эту проблему, обновите политики, которые запрещаются на основе утверждения конечной точки, чтобы разрешить исключения для указанных выше конечных точек.

Например, следующее правило:

`c1:[Type == "http://custom/ipoutsiderange", Value == "true"] && c2:[Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path", Value != "/adfs/ls/"] => issue(Type = "https://schemas.microsoft.com/authorization/claims/deny", Value = " DenyUsersWithClaim");`  

будет обновлен до:

`c1:[Type == "http://custom/ipoutsiderange", Value == "true"] && c2:[Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path", Value != "(/adfs/ls/)|(/adfs/services/trust/2005/windowstransport)|(/adfs/services/trust/13/windowstransport)|(/adfs/services/trust/2005/usernamemixed)|(/adfs/services/trust/13/usernamemixed)|(/adfs/services/trust/2005/certificatemixed)|(/adfs/services/trust/13/certificatemixed)"] => issue(Type = "https://schemas.microsoft.com/authorization/claims/deny", Value = " DenyUsersWithClaim");`



> [!NOTE]
>  Утверждения из этой категории следует использовать только для реализации бизнес-политик, а не в качестве политик безопасности для защиты доступа к сети.  Неавторизованные клиенты могут отправить заголовки с ложными сведениями как способ получения доступа.  

Политики, описанные в этой статье, всегда следует использовать с другим методом проверки подлинности, например с именем пользователя и паролем или многофакторной проверкой подлинности.  

## <a name="client-access-policies-scenarios"></a>Сценарии политик клиентского доступа  

|**Сценарий**|**Описание**| 
| --- | --- | 
|Сценарий 1. Блокировать весь внешний доступ к Office 365|Доступ к Office 365 разрешен со всех клиентов во внутренней корпоративной сети, но запросы от внешних клиентов отклоняются на основе IP-адреса внешнего клиента.|  
|Сценарий 2. Блокировать весь внешний доступ к Office 365, кроме Exchange ActiveSync|Доступ к Office 365 разрешен со всех клиентов во внутренней корпоративной сети, а также с любых внешних клиентских устройств, таких как смарт-телефоны, которые используют Exchange ActiveSync. Все другие внешние клиенты, такие как, использующие Outlook, блокируются.|  
|Сценарий 3. Блокировать весь внешний доступ к Office 365, за исключением браузерных приложений|Блокирует внешний доступ к Office 365, за исключением пассивных (основанных на браузерах) приложений, таких как Outlook Веб-доступ или SharePoint Online.|  
|Сценарий 4. Блокировать весь внешний доступ к Office 365, кроме назначенных групп Active Directory|Этот сценарий используется для тестирования и проверки развертывания политики клиентского доступа. Он блокирует внешний доступ к Office 365 только для членов одной или нескольких групп Active Directory. Он также может использоваться для предоставления внешнего доступа только членам группы.|  

## <a name="enabling-client-access-policy"></a>Включение политики клиентского доступа  
 Чтобы включить политику клиентского доступа в AD FS в Windows Server 2012 R2, необходимо обновить отношение доверия с проверяющей стороной платформы удостоверений Microsoft Office 365. Выберите один из приведенных ниже примеров сценариев, чтобы настроить правила утверждений для отношения доверия с проверяющей стороной **платформы Microsoft Office 365** , которое наилучшим образом соответствует потребностям вашей организации.  

###  <a name="scenario-1-block-all-external-access-to-office-365"></a><a name="scenario1"></a>Сценарий 1. Блокировать весь внешний доступ к Office 365  
 Этот сценарий политики клиентского доступа разрешает доступ со всех внутренних клиентов и блокирует все внешние клиенты на основе IP-адреса внешнего клиента. Следующие процедуры используются для добавления правильных правил авторизации выдачи в отношение доверия с проверяющей стороной Office 365 для выбранного сценария.  

##### <a name="to-create-rules-to-block-all-external-access-to-office-365"></a>Создание правил для блокировки внешнего доступа к Office 365  

1.  В **Диспетчер сервера**выберите **Сервис**, а затем — **Управление AD FS**.  

2.  В дереве консоли в разделе **отношения AD фс\труст**щелкните отношения **доверия с проверяющей стороной**, щелкните правой кнопкой мыши **Microsoft Office 365 удостоверение платформы удостоверения** и выберите пункт **изменить правила утверждений**.  

3.  В диалоговом окне **изменение правил утверждений** перейдите на вкладку **правила авторизации выдачи** и нажмите кнопку **Добавить правило** , чтобы запустить мастер правил для утверждений.  

4.  На странице **Выбор шаблона правила** в разделе **шаблон правила утверждения**выберите **Отправить утверждения с помощью настраиваемого правила**, а затем нажмите кнопку **Далее**.  

5.  На странице **Настройка правила** в разделе **имя правила утверждения**введите отображаемое имя для этого правила, например "Если имеется утверждение IP-адресов за пределами нужного диапазона," запретить ". В разделе **настраиваемое правило**введите или вставьте следующий синтаксис языка правил обработки заявок (замените значение выше для x-MS-forwardd-Client-IP на допустимое выражение IP):  
`c1:[Type == "https://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "false"] && c2:[Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip", Value =~ "^(?!192\.168\.1\.77|10\.83\.118\.23)"] => issue(Type = "https://schemas.microsoft.com/authorization/claims/deny", Value = " DenyUsersWithClaim");` </br>
6.  Нажмите кнопку **Готово**. Убедитесь, что новое правило отображается в списке правила авторизации выдачи, прежде чем перейти к правилу **Разрешить доступ для всех пользователей** по умолчанию (правило запрета будет иметь приоритет, даже если оно присутствует в списке ранее).  Если у вас нет правила разрешения доступа по умолчанию, вы можете добавить его в конце списка, используя язык правил утверждений, следующим образом:  </br>

    `c:[] => issue(Type = "https://schemas.microsoft.com/authorization/claims/permit", Value = "true"); ` 

7.  Чтобы сохранить новые правила, в диалоговом окне **изменение правил утверждений** нажмите кнопку **ОК**. Полученный список должен выглядеть следующим образом.  

     ![Правила проверки подлинности выдачи](media/Access-Control-Policies-W2K12/clientaccess1.png "ADFS_Client_Access_1")  

###  <a name="scenario-2-block-all-external-access-to-office-365-except-exchange-activesync"></a><a name="scenario2"></a>Сценарий 2. Блокировать весь внешний доступ к Office 365, кроме Exchange ActiveSync  
 В следующем примере предоставляется доступ ко всем приложениям Office 365, включая Exchange Online, от внутренних клиентов, включая Outlook. Он блокирует доступ клиентов, находящихся за пределами корпоративной сети, как указано IP-адресом клиента, за исключением клиентов Exchange ActiveSync, таких как Интеллектуальные телефоны.  

##### <a name="to-create-rules-to-block-all-external-access-to-office-365-except-exchange-activesync"></a>Создание правил для блокировки внешнего доступа к Office 365, кроме Exchange ActiveSync  

1.  В **Диспетчер сервера**выберите **Сервис**, а затем — **Управление AD FS**.  

2.  В дереве консоли в разделе **отношения AD фс\труст**щелкните отношения **доверия с проверяющей стороной**, щелкните правой кнопкой мыши **Microsoft Office 365 удостоверение платформы удостоверения** и выберите пункт **изменить правила утверждений**.  

3.  В диалоговом окне **изменение правил утверждений** перейдите на вкладку **правила авторизации выдачи** и нажмите кнопку **Добавить правило** , чтобы запустить мастер правил для утверждений.  

4.  На странице **Выбор шаблона правила** в разделе **шаблон правила утверждения**выберите **Отправить утверждения с помощью настраиваемого правила**, а затем нажмите кнопку **Далее**.  

5.  На странице **Настройка правила** в разделе **имя правила утверждения**введите отображаемое имя для этого правила, например "Если имеется утверждение IP-адресов за пределами нужного диапазона, выдайте ипаутсидеранже утверждение". В разделе **настраиваемое правило**введите или вставьте следующий синтаксис языка правил обработки заявок (замените значение выше для x-MS-forwardd-Client-IP на допустимое выражение IP):  

    `c1:[Type == "https://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "false"] && c2:[Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip", Value =~ "^(?!192\.168\.1\.77|10\.83\.118\.23)"] => issue(Type = "http://custom/ipoutsiderange", Value = "true");`  

6.  Нажмите кнопку **Готово**. Убедитесь, что новое правило отображается в списке **правила авторизации выдачи** .  

7.  Затем в диалоговом окне **изменение правил утверждений** на вкладке **правила авторизации выдачи** нажмите кнопку **Добавить правило** , чтобы снова запустить мастер правил утверждений.  

8.  На странице **Выбор шаблона правила** в разделе **шаблон правила утверждения**выберите **Отправить утверждения с помощью настраиваемого правила**, а затем нажмите кнопку **Далее**.  

9. На странице **Настройка правила** в разделе **имя правила утверждения**введите отображаемое имя для этого правила, например "Если имеется IP-адрес за пределами нужного диапазона, а также не-EAS x-MS-Client-Application утверждений, Deny". В разделе **настраиваемое правило**введите или вставьте следующий синтаксис языка правил для утверждений:  


~~~
`c1:[Type == "http://custom/ipoutsiderange", Value == "true"] && c2:[Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application", Value != "Microsoft.Exchange.ActiveSync"] => issue(Type = "https://schemas.microsoft.com/authorization/claims/deny", Value = "DenyUsersWithClaim");`  
~~~

10. Нажмите кнопку **Готово**. Убедитесь, что новое правило отображается в списке **правила авторизации выдачи** .  

11. Затем в диалоговом окне **изменение правил утверждений** на вкладке **правила авторизации выдачи** нажмите кнопку **Добавить правило** , чтобы снова запустить мастер правил утверждений.  

12. На странице **Выбор шаблона правила** в разделе **шаблон правила утверждения** выберите **Отправить утверждения с помощью настраиваемого правила**, а затем нажмите кнопку **Далее**.  

13. На странице **Настройка правила** в разделе **имя правила утверждения**введите отображаемое имя для этого правила, например "проверить, существует ли утверждение приложения". В разделе **настраиваемое правило**введите или вставьте следующий синтаксис языка правил для утверждений:  

   ```  
   NOT EXISTS([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application"]) => add(Type = "http://custom/xmsapplication", Value = "fail");  
   ```  

14. Нажмите кнопку **Готово**. Убедитесь, что новое правило отображается в списке **правила авторизации выдачи** .  

15. Затем в диалоговом окне **изменение правил утверждений** на вкладке **правила авторизации выдачи** нажмите кнопку **Добавить правило** , чтобы снова запустить мастер правил утверждений.  

16. На странице **Выбор шаблона правила** в разделе **шаблон правила утверждения** выберите **Отправить утверждения с помощью настраиваемого правила**, а затем нажмите кнопку **Далее**.  

17. На странице **Настройка правила** в разделе **имя правила утверждения**введите отображаемое имя для этого правила, например "запретить пользователям с ипаутсидеранже true и сбой приложения". В разделе **настраиваемое правило**введите или вставьте следующий синтаксис языка правил для утверждений:  

`c1:[Type == "http://custom/ipoutsiderange", Value == "true"] && c2:[Type == "http://custom/xmsapplication", Value == "fail"] => issue(Type = "https://schemas.microsoft.com/authorization/claims/deny", Value = "DenyUsersWithClaim");`</br>  
18. Нажмите кнопку **Готово**. Убедитесь, что новое правило отображается непосредственно под предыдущим правилом, и до значения правила разрешения доступа ко всем пользователям по умолчанию в списке правила авторизации выдачи (правило запрета будет иметь приоритет, даже если оно отображается ранее в списке).  </br>Если у вас нет правила разрешения доступа по умолчанию, вы можете добавить его в конце списка, используя язык правил утверждений, следующим образом:</br></br>      `c:[] => issue(Type = "https://schemas.microsoft.com/authorization/claims/permit", Value = "true");`</br></br>
19. Чтобы сохранить новые правила, в диалоговом окне **изменение правил утверждений** нажмите кнопку ОК. Полученный список должен выглядеть следующим образом.  

    ![Правила авторизации выдачи](media/Access-Control-Policies-W2K12/clientaccess2.png )  

###  <a name="scenario-3-block-all-external-access-to-office-365-except-browser-based-applications"></a><a name="scenario3"></a>Сценарий 3. Блокировать весь внешний доступ к Office 365, за исключением браузерных приложений  

##### <a name="to-create-rules-to-block-all-external-access-to-office-365-except-browser-based-applications"></a>Создание правил для блокирования всех внешних доступов к Office 365 за исключением браузерных приложений  

1.  В **Диспетчер сервера**выберите **Сервис**, а затем — **Управление AD FS**.  

2.  В дереве консоли в разделе **отношения AD фс\труст**щелкните отношения **доверия с проверяющей стороной**, щелкните правой кнопкой мыши **Microsoft Office 365 удостоверение платформы удостоверения** и выберите пункт **изменить правила утверждений**.  

3.  В диалоговом окне **изменение правил утверждений** перейдите на вкладку **правила авторизации выдачи** и нажмите кнопку **Добавить правило** , чтобы запустить мастер правил для утверждений.  

4.  На странице **Выбор шаблона правила** в разделе **шаблон правила утверждения**выберите **Отправить утверждения с помощью настраиваемого правила**, а затем нажмите кнопку **Далее**.  

5.  На странице **Настройка правила** в разделе **имя правила утверждения**введите отображаемое имя для этого правила, например "Если имеется утверждение IP-адресов за пределами нужного диапазона, выдайте ипаутсидеранже утверждение". В разделе **настраиваемое правило**введите или вставьте следующий синтаксис языка правил обработки заявок (замените значение выше для x-MS-forwardd-Client-IP на допустимое выражение IP):  </br>
`c1:[Type == "https://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "false"] && c2:[Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip", Value =~ "^(?!192\.168\.1\.77|10\.83\.118\.23)"] => issue(Type = "http://custom/ipoutsiderange", Value = "true");`   
6.  Нажмите кнопку **Готово**. Убедитесь, что новое правило отображается в списке **правила авторизации выдачи** .  

7.  Затем в диалоговом окне **изменение правил утверждений** на вкладке **правила авторизации выдачи** нажмите кнопку **Добавить правило** , чтобы снова запустить мастер правил утверждений.  

8.  На странице **Выбор шаблона правила** в разделе **шаблон правила утверждения** выберите **Отправить утверждения с помощью настраиваемого правила**, а затем нажмите кнопку **Далее**.  

9. На странице **Настройка правила** в разделе **имя правила утверждения**введите отображаемое имя для этого правила, например "Если имеется IP-адрес за пределами нужного диапазона, а конечная точка не/адфс/ЛС, запретите". В разделе **настраиваемое правило**введите или вставьте следующий синтаксис языка правил для утверждений:  


~~~
`c1:[Type == "http://custom/ipoutsiderange", Value == "true"] && c2:[Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path", Value != "/adfs/ls/"] => issue(Type = "https://schemas.microsoft.com/authorization/claims/deny", Value = " DenyUsersWithClaim");`  
~~~

10. Нажмите кнопку **Готово**. Убедитесь, что новое правило отображается в списке правила авторизации выдачи, прежде чем перейти к правилу **Разрешить доступ для всех пользователей** по умолчанию (правило запрета будет иметь приоритет, даже если оно присутствует в списке ранее).  </br></br> Если у вас нет правила разрешения доступа по умолчанию, вы можете добавить его в конце списка, используя язык правил утверждений, следующим образом:  

   `c:[] => issue(Type = "https://schemas.microsoft.com/authorization/claims/permit", Value = "true");`

11. Чтобы сохранить новые правила, в диалоговом окне **изменение правил утверждений** нажмите кнопку **ОК**. Полученный список должен выглядеть следующим образом.  

    ![Выдача](media/Access-Control-Policies-W2K12/clientaccess3.png)  

###  <a name="scenario-4-block-all-external-access-to-office-365-except-for-designated-active-directory-groups"></a><a name="scenario4"></a>Сценарий 4. Блокировать весь внешний доступ к Office 365, кроме назначенных групп Active Directory  
 В следующем примере предоставляется доступ с внутренних клиентов на основе IP-адреса. Он блокирует доступ клиентов, находящихся за пределами корпоративной сети, имеющей внешний IP-адрес клиента, за исключением тех, которые входят в указанную группу Active Directory. чтобы добавить правильные правила авторизации выдачи в отношение доверия с проверяющей стороной **платформы удостоверений Microsoft Office 365** с помощью мастера правил утверждений, выполните следующие действия.  

##### <a name="to-create-rules-to-block-all-external-access-to-office-365-except-for-designated-active-directory-groups"></a>Создание правил для блокировки внешнего доступа к Office 365 за исключением назначенных групп Active Directory  

1.  В **Диспетчер сервера**выберите **Сервис**, а затем — **Управление AD FS**.  

2.  В дереве консоли в разделе **отношения AD фс\труст**щелкните отношения **доверия с проверяющей стороной**, щелкните правой кнопкой мыши **Microsoft Office 365 удостоверение платформы удостоверения** и выберите пункт **изменить правила утверждений**.  

3.  В диалоговом окне **изменение правил утверждений** перейдите на вкладку **правила авторизации выдачи** и нажмите кнопку **Добавить правило** , чтобы запустить мастер правил для утверждений.  

4.  На странице **Выбор шаблона правила** в разделе **шаблон правила утверждения**выберите **Отправить утверждения с помощью настраиваемого правила**, а затем нажмите кнопку **Далее**.  

5.  На странице **Настройка правила** в разделе **имя правила утверждения**введите отображаемое имя для этого правила, например "Если имеется утверждение IP-адресов за пределами нужного диапазона, выдайте заявку ипаутсидеранже". В разделе **настраиваемое правило**введите или вставьте следующий синтаксис языка правил обработки заявок (замените значение выше для x-MS-forwardd-Client-IP на допустимое выражение IP):  


~~~
`c1:[Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip", Value =~ "^(?!192\.168\.1\.77|10\.83\.118\.23)"] && c2:[Type == "https://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "false"] => issue(Type = "http://custom/ipoutsiderange", Value = "true");`  
~~~

6. Нажмите кнопку **Готово**. Убедитесь, что новое правило отображается в списке **правила авторизации выдачи** .  

7. Затем в диалоговом окне **изменение правил утверждений** на вкладке **правила авторизации выдачи** нажмите кнопку **Добавить правило** , чтобы снова запустить мастер правил утверждений.  

8. На странице **Выбор шаблона правила** в разделе **шаблон правила утверждения** выберите **Отправить утверждения с помощью настраиваемого правила**, а затем нажмите кнопку **Далее**.  

9. На странице **Настройка правила** в разделе **имя правила утверждения**введите отображаемое имя для этого правила, например "проверить идентификатор безопасности группы". В разделе **настраиваемое правило**введите или вставьте следующий синтаксис языка правила для утверждений (замените "граупсид" фактическим идентификатором безопасности используемой группы Active Directory):  

    `NOT EXISTS([Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", Value == "S-1-5-32-100"]) => add(Type = "http://custom/groupsid", Value = "fail");`  

10. Нажмите кнопку **Готово**. Убедитесь, что новое правило отображается в списке **правила авторизации выдачи** .  

11. Затем в диалоговом окне **изменение правил утверждений** на вкладке **правила авторизации выдачи** нажмите кнопку **Добавить правило** , чтобы снова запустить мастер правил утверждений.  

12. На странице **Выбор шаблона правила** в разделе **шаблон правила утверждения** выберите **Отправить утверждения с помощью настраиваемого правила**, а затем нажмите кнопку **Далее**.  

13. На странице **Настройка правила** в разделе **имя правила утверждения**введите отображаемое имя для этого правила, например "запретить пользователям с ипаутсидеранже true и граупсид Fail". В разделе **настраиваемое правило**введите или вставьте следующий синтаксис языка правил для утверждений:  

   `c1:[Type == "http://custom/ipoutsiderange", Value == "true"] && c2:[Type == "http://custom/groupsid", Value == "fail"] => issue(Type = "https://schemas.microsoft.com/authorization/claims/deny", Value = "DenyUsersWithClaim");`  

14. Нажмите кнопку **Готово**. Убедитесь, что новое правило отображается непосредственно под предыдущим правилом, и до значения правила разрешения доступа ко всем пользователям по умолчанию в списке правила авторизации выдачи (правило запрета будет иметь приоритет, даже если оно отображается ранее в списке).  </br></br>Если у вас нет правила разрешения доступа по умолчанию, вы можете добавить его в конце списка, используя язык правил утверждений, следующим образом:  

   `c:[] => issue(Type = "https://schemas.microsoft.com/authorization/claims/permit", Value = "true");`  

15. Чтобы сохранить новые правила, в диалоговом окне **изменение правил утверждений** нажмите кнопку ОК. Полученный список должен выглядеть следующим образом.  

     ![Выдача](media/Access-Control-Policies-W2K12/clientaccess4.png)  

##  <a name="building-the-ip-address-range-expression"></a><a name="buildingip"></a>Создание выражения диапазона IP-адресов  
 Утверждение x-MS-Forwarded-Client-IP заносится из заголовка HTTP, который в настоящее время задается только Exchange Online, который заполняет заголовок при передаче запроса на проверку подлинности в AD FS. Значение утверждения может быть одним из следующих:  

> [!NOTE]
>  В настоящее время Exchange Online поддерживает только IPV4 и не IPV6-адреса.  

-   Один IP-адрес: IP-адрес клиента, подключенного непосредственно к Exchange Online  

> [!NOTE]
> - IP-адрес клиента в корпоративной сети будет отображаться как IP-адрес внешнего интерфейса исходящего прокси-сервера или шлюза Организации.  
>   -   Клиенты, подключенные к корпоративной сети с помощью VPN или Microsoft DirectAccess (DA), могут отображаться как внутренние корпоративные клиенты или как внешние клиенты в зависимости от конфигурации VPN или DA.  

-   Один или несколько IP-адресов: Если Exchange Online не может определить IP-адрес подключающегося клиента, он установит значение на основе значения заголовка x-forwardd-for, нестандартного заголовка, который может быть включен в HTTP-запросы и поддерживается многими клиентами, подсистемами балансировки нагрузки и прокси на рынке.  

> [!NOTE]
> 1. Несколько IP-адресов, указывающих IP-адрес клиента и адрес каждого прокси-сервера, который продавал запрос, будут разделены запятыми.  
>    2. IP-адреса, связанные с инфраструктурой Exchange Online, не будут включены в список.  

### <a name="regular-expressions"></a>Использование регулярных выражений  
 Если необходимо сопоставить диапазон IP-адресов, необходимо создать регулярное выражение для выполнения сравнения. В следующих шагах мы предложим примеры того, как создать такое выражение, которое будет соответствовать следующим диапазонам адресов (Обратите внимание, что эти примеры потребуется изменить в соответствии с диапазоном общедоступных IP-адресов):  

- 192.168.1.1 — 192.168.1.25  

- 10.0.0.1 – 10.0.0.14  

  Сначала базовый шаблон, который будет соответствовать одному IP-адресу, выглядит следующим образом: \b # # #\\. # # #\\. # #\\. # # # \b  

  В этом случае мы можем сопоставить два разных IP-адреса с выражением или следующим образом: \b # # #\\. # # #\\. # # #\\. # # #&#124;\b \b # # #\\. # # #\\. # #\\. # # # \b  

  Таким образом, пример для сопоставления только двух адресов (например, 192.168.1.1 или 10.0.0.1) будет выглядеть следующим образом: \b192\\. 168\\0,1\\1&#124;– b \b10\\0\\. 0\\. 1 \ b  

  Это дает возможность ввести любое количество адресов. Если необходимо разрешить диапазон адресов, например 192.168.1.1 – 192.168.1.25, сопоставление должно выполняться по символу: \b192\\. 168\\. 1\\. ([1-9]&#124;1 [0-9]&#124;2 [0-5]) \b  

  Имейте в виду следующее:  

- IP-адрес рассматривается как строка, а не число.  

- Правило разбивается следующим образом: \b192\\. 168\\. 1\\.  

- Это соответствует любому значению, начиная с 192.168.1.  

- Следующие сведения соответствуют диапазонам, необходимым для части адреса после завершающей десятичной запятой:  

  -   ([1-9] совпадает с адресами, завершающимися в 1-9  

  -   &#124;1 [0-9] соответствует адресам, завершающимся в 10-19  

  -   &#124;2 [0-5]) соответствует адресам, завершающимся в 20-25  

- Обратите внимание, что круглые скобки должны быть правильно размещены, чтобы не начинать сопоставление других частей IP-адресов.  

- При совпадении с блоком 192 можно написать аналогичное выражение для 10 блока: \b10\\0\\. 0\\. ([1-9]&#124;1 [0-4]) \b  

- И поместив их вместе, следующее выражение должно соответствовать всем адресам для "192.168.1.1 ~ 25" и "10.0.0.1 ~ 14": \b192\\. 168\\. 1\\. ([1-9]&#124;1 [0-9]&#124;2 [0-5]) \b&#124;\b10\\0\\. 0\\. ([1-9]&#124;1 [0-4]) \b  

### <a name="testing-the-expression"></a>Тестирование выражения  
 Выражения Regex могут стать довольно сложными, поэтому мы настоятельно рекомендуем использовать средство проверки регулярного выражения. Если вы выполняете поиск в Интернете по запросу "Построитель регулярных выражений в Интернете", вы найдете несколько хороших интерактивных служебных программ, которые позволят опробовать выражения в демонстрационных данных.  

 При тестировании выражения важно понимать, что должно быть найдено. Система Exchange Online может отправить несколько IP-адресов, разделенных запятыми. Приведенные выше выражения будут работать. Однако важно подумать об этом при тестировании выражений регулярного выражения. Например, можно использовать следующий пример входных данных для проверки приведенных выше примеров.  

 192.168.1.1, 192.168.1.2, 192.169.1.1. 192.168.12.1, 192.168.1.10, 192.168.1.25, 192.168.1.26, 192.168.1.30, 1192.168.1.20  

 10.0.0.1, 10.0.0.5, 10.0.0.10, 10.0.1.0, 10.0.1.1, 110.0.0.1, 10.0.0.14, 10.0.0.15, 10.0.0.10, 10, 0.0.1  

## <a name="claim-types"></a>Типы утверждений  
 AD FS в Windows Server 2012 R2 предоставляет сведения о контексте запроса, используя следующие типы утверждений:  

### <a name="x-ms-forwarded-client-ip"></a>X-MS-Forwarded-Client-IP  
 Тип утверждения: `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip`  

 Это утверждение AD FS представляет собой "лучшую попытку" при поиске IP-адреса пользователя (например, клиента Outlook), выполняющего запрос. Это утверждение может содержать несколько IP-адресов, включая адрес каждого прокси-сервера, который перенаправлял запрос.  Это утверждение заполняется по протоколу HTTP. Значение утверждения может быть одним из следующих:  

-   Один IP-адрес — IP-адрес клиента, подключенного непосредственно к Exchange Online.  

> [!NOTE]
>  IP-адрес клиента в корпоративной сети будет отображаться как IP-адрес внешнего интерфейса исходящего прокси-сервера или шлюза Организации.  

-   Один или несколько IP-адресов  

    -   Если Exchange Online не может определить IP-адрес подключающегося клиента, он установит значение на основе значения заголовка x-forwardd-for, нестандартного заголовка, который может быть включен в запросы на основе HTTP и поддерживается многими клиентами, подсистемами балансировки нагрузки и учетные записи-посредники на рынке.  

    -   Если IP-адрес клиента и адрес каждого прокси-сервера, который продавал запрос, будут разделяться запятыми, будет использоваться несколько IP-адресов.  

> [!NOTE]
>  IP-адреса, связанные с инфраструктурой Exchange Online, отсутствуют в списке.  

> [!WARNING]
>  В настоящее время Exchange Online поддерживает только IPV4-адреса; Он не поддерживает IPV6-адреса.  

### <a name="x-ms-client-application"></a>X-MS-Client-Application  
 Тип утверждения: `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application`  

 Это утверждение AD FS представляет протокол, используемый конечным клиентом, который неплотно соответствует используемому приложению.  Это утверждение заполняется из заголовка HTTP, который в настоящее время задается Exchange Online, который заполняет заголовок при передаче запроса на проверку подлинности в AD FS. В зависимости от приложения значение этого утверждения будет одним из следующих:  

-   В случае с устройствами, использующими Exchange Active Sync, значением будет Microsoft. Exchange. ActiveSync.  

-   Использование клиента Microsoft Outlook может привести к любому из следующих значений:  

    -   Microsoft. Exchange. автообнаружения  

    -   Microsoft. Exchange. Оффлинеаддрессбук  

    -   Microsoft. Exchange. Рпкмикрософт. Exchange. WebService  

    -   Microsoft. Exchange. Рпкмикрософт. Exchange. WebService  

-   К другим возможным значениям этого заголовка относятся следующие.  

    -   Microsoft. Exchange. PowerShell  

    -   Microsoft. Exchange. SMTP  

    -   Microsoft. Exchange. POP  

    -   Microsoft. Exchange. IMAP  

### <a name="x-ms-client-user-agent"></a>X-MS-Client-User-Agent  
 Тип утверждения: `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-user-agent`  

 Это утверждение AD FS предоставляет строку для представления типа устройства, который используется клиентом для доступа к службе. Это можно использовать, когда клиенты хотели бы запретить доступ к определенным устройствам (например, к определенным типам смартфонов).  Примеры значений для этого утверждения: (но не ограничиваются ими) значениями ниже.  

 Ниже приведены примеры того, что может содержать значение x-MS-User-Agent для клиента, x-MS-Client-Application — Microsoft. Exchange. ActiveSync.  

- Вортекс/1.0  

- Apple-iPad1C1/812.1  

- Apple-iPhone3C1/811.2  

- Apple-iPhone/704.11  

- Мото-DROID2/4.5.1  

- SAMSUNGSPHD700/100.202  

- Android/0,3  

  Также возможно, что это значение пустое.  

### <a name="x-ms-proxy"></a>X-MS-Proxy  
 Тип утверждения: `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-proxy`  

 Это утверждение AD FS указывает, что запрос прошел через прокси веб-приложения.  Это утверждение заполняется прокси-службой, которая заполняет заголовок при передаче запроса на проверку подлинности в служба федерации серверной части. AD FS преобразует его в утверждение.  

 Значение утверждения — это DNS-имя прокси-сервера, который передал запрос.  

### <a name="insidecorporatenetwork"></a>инсидекорпоратенетворк  
 Тип утверждения: `https://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork`  

 Аналогично приведенному выше типу утверждения x-MS-Proxy этот тип утверждения указывает, прошел ли запрос через прокси веб-приложения. В отличие от x-MS-Proxy, инсидекорпоратенетворк — это логическое значение со значением true, которое указывает на запрос непосредственно к службе Федерации в корпоративной сети.  

### <a name="x-ms-endpoint-absolute-path-active-vs-passive"></a>X-MS-Endpoint-абсолютный путь (Активный vs passive)  
 Тип утверждения: `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path`  

 Этот тип утверждения можно использовать для определения запросов, исходящих от "активных" (насыщенных) клиентов, а также от "пассивных" (на основе веб-браузеров). Это позволяет выполнять внешние запросы из приложений на основе браузера, таких как Outlook Веб-доступ, SharePoint Online или портал Office 365, в то время как запросы, поступающие от многофункциональных клиентов, таких как Microsoft Outlook, блокируются.  

 Значение утверждения — это имя службы AD FS, которая получила запрос.  

## <a name="see-also"></a>См. также  
 [Операции AD FS](../../ad-fs/AD-FS-2016-Operations.md)
