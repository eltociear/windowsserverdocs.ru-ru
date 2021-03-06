---
ms.assetid: 6b38480e-5b1c-49f0-9d46-8cf22f70f0d2
title: Настройка лабораторной среды для служб федерации Active Directory в Windows Server 2012 R2
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 44de547b0a9c8636b07886d35c451bca6ec46341
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/08/2020
ms.locfileid: "80855177"
---
# <a name="set-up-the-lab-environment-for-ad-fs-in-windows-server-2012-r2"></a>Настройка лабораторной среды для служб федерации Active Directory в Windows Server 2012 R2


В этой статье описаны шаги по настройке тестовой среды, которую можно использовать для выполнения инструкций следующих пошаговых руководств.

-   [Пошаговое руководство. Workplace Join с устройством iOS](../../ad-fs/operations/Walkthrough--Workplace-Join-with-an-iOS-Device.md)

-   [Пошаговое руководство. Workplace Join с устройством Windows](../../ad-fs/operations/Walkthrough--Workplace-Join-with-a-Windows-Device.md)


-   [Пошаговое руководство. Управление рисками с помощью контроля условного доступа](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Conditional-Access-Control.md)

-   [Пошаговое руководство. Управление рисками с помощью дополнительной многофакторной проверки подлинности для конфиденциальных приложений](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md)

> [!NOTE]
> Не рекомендуется устанавливать на одном компьютере и веб-сервер, и сервер федерации.

Для настройки данной тестовой среды выполните следующие шаги.

1.  [Шаг 1. Настройка контроллера домена (DC1)](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_1)

2.  [Шаг 2. Настройка сервера федерации (ADFS1) с помощью службы регистрации устройств](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_4)

3.  [Шаг 3. Настройка веб-сервера (WebServ1) и примера приложения на основе утверждений](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_5)

4.  [Шаг 4. Настройка клиентского компьютера (CLIENT1)](../../ad-fs/deployment/../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_10)

## <a name="step-1-configure-the-domain-controller-dc1"></a><a name="BKMK_1"></a>Шаг 1. Настройка контроллера домена (DC1)
Для целей этой тестовой среды можно вызвать корневой Active Directory домена **contoso.com** и указать <strong>pass@word1</strong> в качестве пароля администратора.

-   Установите службу роли AD DS и установите службы домен Active Directory (AD DS), чтобы сделать компьютер контроллером домена в Windows Server 2012 R2. Это действие обновляет схему AD DS в процессе создания контроллера домена. Дополнительные сведения и пошаговые инструкции см. в разделе[https://technet.microsoft.com/library/hh472162.aspx](https://technet.microsoft.com/library/hh472162.aspx).

### <a name="create-test-active-directory-accounts"></a><a name="BKMK_2"></a>Создание учетных записей Active Directory тестирования
После того как контроллер домена станет функциональным, можно создать тестовую группу и тестовые учетные записи пользователей в этом домене и добавить учетную запись пользователя в учетную запись группы. Эти учетные записи используются для выполнения пошаговых инструкций в соответствующих руководствах, которые перечислены ранее в этой статье.

Создайте следующие учетные записи.

- Пользователь: **Роберт хатлэй** со следующими учетными данными: имя пользователя: **роберс** и пароль: <strong>P@ssword</strong>

- Группа: **Finance**

Сведения о создании учетных записей пользователей и групп в Active Directory (AD) см. в разделе [https://technet.microsoft.com/library/cc783323%28v.aspx](https://technet.microsoft.com/library/cc783323%28v=ws.10%29.aspx).

Добавьте учетную запись **Robert Hatley** в группу **Finance**. Сведения о добавлении пользователя в группу в Active Directory см. в разделе [https://technet.microsoft.com/library/cc737130%28v=ws.10%29.aspx](https://technet.microsoft.com/library/cc737130%28v=ws.10%29.aspx).

### <a name="create-a-gmsa-account"></a>Создание учетной записи GMSA
Учетная запись групповой управляемой учетной записи службы (GMSA) требуется во время установки и настройки службы федерации Active Directory (AD FS) (AD FS).

##### <a name="to-create-a-gmsa-account"></a>Создание групповой управляемой учетной записи службы

1.  Откройте командное окно Windows PowerShell и введите:

    ```
    Add-KdsRootKey -EffectiveTime (Get-Date).AddHours(-10)
    New-ADServiceAccount FsGmsa -DNSHostName adfs1.contoso.com -ServicePrincipalNames http/adfs1.contoso.com

    ```

## <a name="step-2-configure-the-federation-server-adfs1-by-using-device-registration-service"></a><a name="BKMK_4"></a>Шаг 2. Настройка сервера федерации (ADFS1) с помощью службы регистрации устройств
Чтобы настроить другую виртуальную машину, установите Windows Server 2012 R2 и подключите ее к домену **contoso.com**. Настройте компьютер после его присоединения к домену, а затем перейдите к установке и настройке роли AD FS.

См. видео в статье [Серии видеороликов с практическими рекомендациями по работе со службами федерации Active Directory: установка фермы серверов AD FS Server Farm](https://technet.microsoft.com/video/dn469436).

### <a name="install-a-server-ssl-certificate"></a>Установка SSL-сертификата сервера
Необходимо установить SSL-сертификат на сервере ADFS1 в хранилище локального компьютера. Сертификат ДОЛЖЕН иметь следующие атрибуты.

-   Имя субъекта (CN): adfs1.contoso.com

-   Альтернативное имя субъекта (DNS): adfs1.contoso.com

-   Альтернативное имя субъекта (DNS): enterpriseregistration.contoso.com

Дополнительные сведения о настройке SSL-сертификатов см. в разделе [Настройка SSL и TLS на веб-сайте в домене с помощью ЦС предприятия](https://social.technet.microsoft.com/wiki/contents/articles/12485.configure-ssltls-on-a-web-site-in-the-domain-with-an-enterprise-ca.aspx).

[Серии видеороликов с практическими рекомендациями по работе со службами федерации Active Directory: обновление сертификатов](https://technet.microsoft.com/video/adfs-updating-certificates).

### <a name="install-the-ad-fs-server-role"></a>Установка роли сервера AD FS

##### <a name="to-install-the-federation-service-role-service"></a>Установка службы роли службы федерации

1. Войдите на сервер, используя учетную запись администратора домена administrator@contoso.com.

2. Запустите диспетчер сервера. Для запуска диспетчера серверов щелкните **Диспетчер серверов** на экране **Запуск** в ОС Windows или щелкните **Диспетчер серверов** на панели задач Windows рабочего стола Windows. На вкладке **Быстрый запуск** плитки **приветствия** на странице **Панель мониторинга** щелкните **Добавить роли и компоненты**. Также можно выбрать пункт **Добавить роли и компоненты** в меню **Управление**.

3. На странице **Перед началом работы** нажмите кнопку **Далее**.

4. На странице **Выбор типа установки** щелкните **Установка ролей или компонентов**, а затем нажмите кнопку **Далее**.

5. На странице **Выбор целевого сервера** щелкните **Выбрать сервер из пула серверов**, убедитесь, что выбран целевой компьютер, а затем нажмите кнопку **Далее**.

6. На странице **Выбор ролей сервера** выберите пункт **Службы федерации Active Directory** и нажмите кнопку **Далее**.

7. На странице **Выбор компонентов** нажмите кнопку **Далее**.

8. На странице **Служба федерации Active Directory** нажмите кнопку **Далее**.

9. После проверки информации на странице **Проверьте выбранные компоненты установки** установите флажок **При необходимости автоматически перезагрузить конечный сервер**, после чего нажмите кнопку **Установить**.

10. На странице **Ход установки** убедитесь, что все установлено верно, а затем нажмите кнопку **Закрыть**.

### <a name="configure-the-federation-server"></a>Настройка сервера федерации
Следующий шаг — настройка сервера федерации.

##### <a name="to-configure-the-federation-server"></a>Настройка сервера федерации

1.  На странице **Панель мониторинга** диспетчера сервера установите флажок **Уведомления**, а затем выберите **Настроить службу федерации на этом сервере**.

    Откроется **Мастер конфигурации служб федерации Active Directory**.

2.  На странице **Приветствие** щелкните **Создать первый сервер федерации на ферме серверов федерации** и нажмите кнопку **Далее**.

3.  На странице **Подключиться к AD DS** укажите учетную запись с правами администратора домена для домена Active Directory **contoso.com**, к которому подсоединен этот компьютер, а затем нажмите кнопку **Далее**.

4.  На странице **Укажите свойства службы** выполните следующее, а затем нажмите кнопку **Далее**.

    -   Импортируйте полученный ранее SSL-сертификат. Этот сертификат является необходимым сертификатом аутентификации службы. Перейдите в расположение SSL-сертификата.

    -   Чтобы предоставить имя для вашей службы федерации, введите **adfs1.contoso.com**. Это то же значение, что и предоставленное при регистрации SSL-сертификата в службах сертификатов Active Directory (AD CS).

    -   Для предоставления отображаемого имени службы федерации введите **Contoso Corporation**.

5.  На странице **Укажите учетную запись службы** выберите **Использовать существующую учетную запись пользователя домена или групповую управляемую учетную запись служб**, а затем укажите учетную запись GMSA **fsgmsa**, созданную при создании контроллера домена.

6.  На странице **Укажите базу данных конфигурации** выберите **Создать на этом сервере базу данных на основе внутренней базы данных Windows**, а затем нажмите кнопку **Далее**.

7.  На странице **Просмотр параметров** проверьте выбранные параметры конфигурации и нажмите кнопку **Далее**.

8.  На странице **Предварительные проверки** убедитесь, что все предварительные проверки успешно пройдены, и нажмите кнопку **Настроить**.

9. На странице **Результаты** проверьте результаты, убедитесь, что конфигурация успешно завершена, а затем нажмите **Для развертывания службы федерации нужно выполнить следующие действия**.

### <a name="configure-device-registration-service"></a>Настройка службы регистрации устройств
Затем необходимо настроить на сервере ADFS1 службу регистрации устройств. См. видео в статье [Серии видеороликов с практическими рекомендациями по работе со службами федерации Active Directory: включение службы регистрации устройств](https://technet.microsoft.com/video/adfs-how-to-enabling-the-device-registration-service).

##### <a name="to-configure-device-registration-service-for-windows-server-2012-rtm"></a>Настройка службы регистрации устройств для Windows Server 2012 RTM

1.  > [!IMPORTANT]
    > **Следующий шаг относится к сборке RTM Windows Server 2012 R2.**

    Откройте командное окно Windows PowerShell и введите:

    ```
    Initialize-ADDeviceRegistration
    ```

    В ответ на запрос ввода учетной записи службы введите **contoso\fsgmsa$** .

    Теперь запустите командлет Windows PowerShell.

    ```
    Enable-AdfsDeviceRegistration
    ```

2.  На сервере ADFS1 на консоли **Управление AD FS** перейдите в раздел **Политики аутентификации**. Выберите **Редактировать глобальную первичную аутентификацию**. Установите флажок в поле **Включить аутентификацию устройств** и нажмите кнопку **ОК**.

### <a name="add-host-a-and-alias-cname-resource-records-to-dns"></a>Добавление записей ресурсов узла (А) и псевдонима (CNAME) в DNS
В DC1 необходимо убедиться, что для службы регистрации устройств созданы следующие записи доменной службы имен (DNS).

|Элемент|Тип|Адрес|
|---------|--------|-----------|
|adfs1|Узел (A)|IP-адрес сервера AD FS|
|enterpriseregistration|Псевдоним (CNAME)|adfs1.contoso.com|

Можно воспользоваться следующей процедурой для добавления записи ресурса узла (А) на корпоративные серверы DNS-имен для сервера федерации и службы регистрации устройств.

Членство в группе "Администраторы" или эквивалентной ей группе является минимальным требованием для выполнения этой процедуры. Ознакомьтесь со сведениями об использовании соответствующих учетных записей и членстве<https://go.microsoft.com/fwlink/?LinkId=83477>в группах в локальной группе и группах домена по умолчанию (<https://go.microsoft.com/fwlink/p/?LinkId=83477>).

##### <a name="to-add-a-host-a-and-alias-cname-resource-records-to-dns-for-your-federation-server"></a>Добавление записей ресурсов узла (А) и псевдонима (CNAME) в DNS для сервера федерации

1.  В DC1 из диспетчера серверов в меню **Сервис** щелкните **DNS**, чтобы открыть оснастку DNS.

2.  В дереве консоли разверните DC1, затем — **Зоны прямого просмотра**, щелкните правой кнопкой мыши **contoso.com**, а затем щелкните **Новый узел (А или АААА)** .

3.  В поле **Имя** введите требуемое имя фермы AD FS. Для данного пошагового руководства введите **adfs1**.

4.  В поле **IP-адрес** введите IP-адрес сервера ADFS1. Нажмите кнопку **Добавить узел**.

5.  Щелкните правой кнопкой **contoso.com**, а затем — **Новый псевдоним (CNAME)** .

6.  В диалоговом окне **Новая запись ресурса** введите **enterpriseregistration** в поле **Имя псевдонима**.

7.  В поле полного доменного имени целевого узла введите **adfs1.contoso.com** и нажмите кнопку **ОК**.

    > [!IMPORTANT]
    > В реальном развертывании, если у компании несколько суффиксов имени участника-пользователя, необходимо создать несколько записей CNAME, по одной для каждого из этих суффиксов в DNS.

## <a name="step-3-configure-the-web-server-webserv1-and-a-sample-claims-based-application"></a><a name="BKMK_5"></a>Шаг 3. Настройка веб-сервера (WebServ1) и примера приложения на основе утверждений
Настройте виртуальную машину (WebServ1), установив операционную систему Windows Server 2012 R2 и подключая ее к домену **contoso.com**. После подключения к домену можно продолжить установку и настройку роли веб-сервера.

Для завершения пошаговых руководств, перечисленных ранее в этом разделе, необходимо иметь пример приложения, безопасность которого обеспечивается вашим сервером федерации (ADFS1).

Вы можете скачать пакет SDK для Windows Identity Foundation ([https://www.microsoft.com/download/details.aspx?id=4451](https://www.microsoft.com/download/details.aspx?id=4451), который включает пример приложения на основе утверждений.

Для настройки веб-сервера с использованием примера приложения на основе утверждений необходимо выполнить следующие действия.

> [!NOTE]
> Эти действия были протестированы на веб-сервере под управлением операционной системы Windows Server 2012 R2.

1.  [Установка роли веб-сервера и Windows Identity Foundation](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_15)

2.  [Установка пакета SDK для Windows Identity Foundation](../../ad-fs/deployment/../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_13)

3.  [Настройка простого приложения утверждений в службах IIS](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_9)

4.  [Создание отношения доверия с проверяющей стороной на сервере федерации](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_11)

### <a name="install-the-web-server-role-and-windows-identity-foundation"></a><a name="BKMK_15"></a>Установка роли веб-сервера и Windows Identity Foundation

1. > [!NOTE]
   > Необходимо иметь доступ к установочному носителю Windows Server 2012 R2.

   Войдите в WebServ1 с помощью <strong>administrator@contoso.com</strong> и пароля <strong>pass@word1</strong>.

2. В диспетчере серверов на вкладке **Быстрый запуск** плитки **Приветствие** на странице **Панель мониторинга** щелкните **Добавить роли и компоненты**. Также можно выбрать пункт **Добавить роли и компоненты** в меню **Управление**.

3. На странице **Перед началом работы** нажмите кнопку **Далее**.

4. На странице **Выбор типа установки** щелкните **Установка ролей или компонентов**, а затем нажмите кнопку **Далее**.

5. На странице **Выбор целевого сервера** щелкните **Выбрать сервер из пула серверов**, убедитесь, что выбран целевой компьютер, а затем нажмите кнопку **Далее**.

6. На странице **Выбор ролей сервера** установите флажок в поле **Веб-сервер (IIS)** , щелкните **Добавить компоненты** и нажмите кнопку **Далее**.

7. На странице **Выбор компонентов** выберите **Windows Identity Foundation 3.5** и нажмите кнопку **Далее**.

8. На странице **Роль веб-сервера (IIS)** нажмите кнопку **Далее**.

9. На странице **Выбор служб ролей** выберите и разверните узел **Разработка приложений**. Выберите **ASP.NET 3.5**, щелкните **Добавление компонентов** и нажмите кнопку **Далее**.

10. На странице **Подтверждение выбранных элементов для установки** щелкните **Указать альтернативный исходный путь**. Введите путь к каталогу SxS, который находится на установочном носителе Windows Server 2012 R2. Например, D:\Sources\Sxs. Нажмите кнопку **ОК**, а затем кнопку **Установить**.

### <a name="install-windows-identity-foundation-sdk"></a><a name="BKMK_13"></a>Установка пакета SDK для Windows Identity Foundation

1.  Запустите Виндовсидентитифаундатион-СДК-3.5. msi, чтобы установить Windows Identity Foundation SDK 3,5 (https://www.microsoft.com/download/details.aspx?id=4451). Выберите все параметры по умолчанию.

### <a name="configure-the-simple-claims-app-in-iis"></a><a name="BKMK_9"></a>Настройка простого приложения утверждений в службах IIS

1.  Установите действующий SSL-сертификат из хранилища сертификатов компьютера. Сертификат должен содержать имя веб-сервера, **webserv1.contoso.com**.

2.  Копируйте содержимое из папки C:\Program Files (x86)\Windows Identity Foundation SDK\v3.5\Samples\Quick Start\Web Application\PassiveRedirectBasedClaimsAwareWebApp в папку C:\Inetpub\Claimapp.

3.  Редактируйте файл **Default.aspx.cs**, чтобы фильтрация утверждений не осуществлялась. Этот шаг нужен для того, чтобы в примере приложения отображались все утверждения, изданные сервером федерации. Выполните следующие действия.

    1.  Откройте **Default.aspx.cs** в текстовом редакторе.

    2.  Найдите файл для второго экземпляра `ExpectedClaims`.

    3.  Закомментируйте утверждение `IF` целиком, включая круглые скобки. Укажите комментарии, вводя символы "//" (без кавычек) в начале строки.

    4.  Оператор `FOREACH` теперь должен выглядеть так же, как в примере кода.

        ```
        Foreach (claim claim in claimsIdentity.Claims)
        {
           //Before showing the claims validate that this is an expected claim
           //If it is not in the expected claims list then don't show it
           //if (ExpectedClaims.Contains( claim.ClaimType ) )
           // {
              writeClaim( claim, table );
           //}
        }

        ```

    5.  Сохраните и закройте **Default.aspx.cs**.

    6.  Откройте **web.config** в текстовом редакторе.

    7.  Полностью удалите раздел `<microsoft.identityModel>` . Удалите все, начиная с `including <microsoft.identityModel>` и до `</microsoft.identityModel>`включительно.

    8.  Сохраните и закройте **web.config**.

4.  **Настройка диспетчера IIS**

    1.  Откройте **Диспетчер Internet Information Services (IIS)** .

    2.  Перейдите в раздел **Пулы приложений**, щелкните правой кнопкой **DefaultAppPool**, чтобы выбрать **Дополнительные параметры**. Задайте для параметра **Загрузить профиль пользователя** значение **True** и нажмите кнопку **ОК**.

    3.  Щелкните правой кнопкой **DefaultAppPool**, чтобы выбрать **Основные параметры**. Измените **Версия .NET CLR** на **версия .NET CLR 2.0.50727**.

    4.  Щелкните правой кнопкой **Веб-сайт по умолчанию**, чтобы выбрать команду **Редактировать привязки**.

    5.  Добавьте привязку **HTTPS** в порт **443** с установленным SSL-сертификатом.

    6.  Щелкните правой кнопкой **Веб-сайт по умолчанию**, чтобы выбрать **Добавить приложение**.

    7.  Задайте псевдоним **claimapp** и физический путь **c:\inetpub\claimapp**.

5.  Для настройки **claimapp** для работы с сервером федерации выполните следующие действия.

    1.  Запустите FedUtil.exe, расположенный в **C:\Program Files (x86)\Windows Identity Foundation SDK\v3.5**.

    2.  Задайте для расположения конфигурации приложения значение **к:\инетпут\клаимапп\веб.конфиг** и задайте для URI приложения URL-адрес сайта **https://webserv1.contoso.com/клаимапп/** . Нажмите кнопку **Далее**.

    3.  Выберите **использовать СУЩЕСТВУЮЩУЮ STS** и перейдите к URL-адресу метаданных AD FS сервера **https://adfs1.contoso.com/federationmetadata/2007-06/federationmetadata.xml** . Нажмите кнопку **Далее**.

    4.  Выберите **Отключить проверку цепочки сертификатов**, а затем нажмите кнопку **Далее**.

    5.  Щелкните **Без шифрования** и нажмите кнопку **Далее**. На странице **Предложенные утверждения** нажмите кнопку **Далее**.

    6.  Установите флажок, чтобы **Запланировать задание для выполнения ежедневных обновлений метаданных WS-Federation**. Нажмите кнопку **Готово**.

    7.  Пример приложения настроен. Если вы тестируете URL-адрес приложения **https://webserv1.contoso.com/claimapp** , он должен перенаправить вас на сервер федерации. На сервере федерации должна отображаться страница ошибки, потому что отношения доверия с проверяющей стороной еще не настроены. Иными словами, вы не защищаете это тестовое приложение с AD FS.

Теперь вы должны защитить пример приложения, которое выполняется на веб-сервере, с AD FS. Для этого достаточно добавить отношения доверия с проверяющей стороной на сервер федерации (ADFS1). См. видео в статье [Серии видеороликов с практическими рекомендациями по работе со службами федерации Active Directory: добавление отношения доверия с проверяющей стороной](https://technet.microsoft.com/video/adfs-how-to-add-a-relying-party-trust).

### <a name="create-a-relying-party-trust-on-your-federation-server"></a><a name="BKMK_11"></a>Создание отношения доверия с проверяющей стороной на сервере федерации

1.  На сервере федерации (ADFS1) в разделе **Консоль управления AD FS** перейдите в область **Отношения доверия с проверяющей стороной**, а затем щелкните **Добавить отношения доверия с проверяющей стороной**.

2.  На странице **Выбор источника данных** выберите **Импортировать данные о проверяющей стороне, опубликованные в Интернете или локальной сети**, введите URL-адрес метаданных для **claimapp**, а затем нажмите кнопку **Далее**. Запустите созданный инструментом FedUtil.exe XML-файл метаданных. Он находится по адресу **https://webserv1.contoso.com/claimapp/federationmetadata/2007-06/federationmetadata.xml** .

3.  На странице **Укажите отображаемое имя** укажите **отображаемое имя** отношений доверия с проверяющей стороной, **claimapp**, а затем нажмите кнопку **Далее**.

4.  На странице **Настроить многофакторную аутентификацию сейчас?** выберите **Я не хочу сейчас указывать параметры многофакторной аутентификации для отношений доверия с этой проверяющей стороной** и нажмите кнопку **Далее**.

5.  На странице **Выберите правила авторизации выпуска** выберите **Разрешить всем пользователям доступ к этой проверяющей стороне**, а затем нажмите кнопку **Далее**.

6.  На странице **Готово к добавлению отношений доверия** щелкните **Далее**.

7.  В диалоговом окне **Изменение правил для утверждений** щелкните **Добавить правило**.

8.  На странице **Выберите тип правила** выберите **Отправлять утверждения с использованием пользовательского правила**, а затем нажмите кнопку **Далее**.

9. На странице **Настройка правил утверждений** в поле **Имя правила утверждений** введите **All Claims**. В поле **Пользовательское правило** введите следующее правило утверждений.

    ```
    c:[ ]
    => issue(claim = c);

    ```

10. Нажмите кнопку **Готово**, а затем — кнопку **ОК**.

## <a name="step-4-configure-the-client-computer-client1"></a><a name="BKMK_10"></a>Шаг 4. Настройка клиентского компьютера (CLIENT1)
Настройте другую виртуальную машину и установите Windows 8.1. Эта виртуальная машина должна быть в той же виртуальной сети, что и другие машины. Эта машина НЕ должна быть объединена в домен Contoso.

Клиент ДОЛЖЕН доверять SSL-сертификату, используемому для сервера федерации (ADFS1), настроенного в разделе [Step 2: Configure the federation server (ADFS1) with Device Registration Service](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_4). Система также должна быть в состоянии проверить информацию об отзыве сертификата.

Необходимо также настроить и использовать учетную запись Microsoft для входа на Клиент1.

## <a name="see-also"></a>См. также


- [Службы федерации Active Directory (AD FS) видеороликов. Установка фермы серверов AD FS](https://technet.microsoft.com/video/dn469436)
- [Службы федерации Active Directory (AD FS) серии видеороликов. обновление сертификатов](https://technet.microsoft.com/video/adfs-updating-certificates)
- [Службы федерации Active Directory (AD FS) серии видеороликов. Добавление отношения доверия с проверяющей стороной](https://technet.microsoft.com/video/adfs-how-to-add-a-relying-party-trust)
- [Службы федерации Active Directory (AD FS) серии видеороликов. Включение службы регистрации устройств](https://technet.microsoft.com/video/adfs-how-to-enabling-the-device-registration-service)
- [Службы федерации Active Directory (AD FS) серия видеороликов. Установка прокси-службы веб приложения](https://technet.microsoft.com/video/dn469438)



