---
title: Диагностика проблем с проверкой подлинности
description: Этот раздел является частью руководства развертывание удаленного доступа с проверкой подлинности OTP в Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 71307757-f8f4-4f82-b8b3-ffd4fd8c5d6d
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 08dd6822cc30135506d82041cfbeab0bc1a058ab
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/20/2019
ms.locfileid: "67282358"
---
# <a name="troubleshooting-authentication-issues"></a>Диагностика проблем с проверкой подлинности

>Область применения. Windows Server (полугодовой канал), Windows Server 2016

В этом разделе содержатся сведения об устранении проблемы, связанные с неполадками, пользователи могут возникнуть при попытке подключения к DirectAccess с помощью проверки подлинности OTP. DirectAccerss OTP связанные события регистрируются на клиентском компьютере в средстве просмотра событий в **приложений и журналы служб/Microsoft/Windows/OtpCredentialProvider**. Убедитесь, что этот журнал включен, при устранении неполадок с помощью OTP для DirectAccess.  
  
## <a name="failed-to-access-the-ca-that-issues-otp-certificates"></a>Не удалось получить доступ к центру сертификации, который выдает сертификаты OTP  
**Сценарий**. Пользователю не удается выполнить аутентификацию с помощью OTP с ошибкой: «Проверка подлинности не пройдена из-за внутренней ошибки»  
  
**Сообщение об ошибке** (журнал событий клиента). Регистрация сертификата OTP для пользователя <username> сбой на сервере ЦС < CA_name >, запрос не удалось выполнить, возможные причины сбоя: Не удается разрешить имя сервера, сервера ЦС не может осуществляться через первый туннель DirectAccess или не удается установить соединение с сервером ЦС.  
  
**Причина**  
  
Предоставляемое пользователем допустимый одноразовый пароль и сервер DirectAccess автоматический запрос на сертификат; Тем не менее клиентский компьютер не удается связаться с ЦС, выдающего сертификаты OTP, чтобы завершить процесс регистрации.  
  
**Решение**  
  
На сервере DirectAccess выполните следующие команды Windows PowerShell:  
  
1.  Получить список настроенных OTP, выдающие ЦС и проверьте значение параметра «CAServer»: `Get-DAOtpAuthentication`  
  
2.  Убедитесь, что сервер клиентского доступа настроены как серверы управления. `Get-DAMgmtServer -Type All`  
  
3.  Убедитесь, что клиентский компьютер устанавливает туннель инфраструктуры: В брандмауэр Windows в режиме повышенной безопасности консоли, разверните **сопоставления мониторинг/безопасности**, нажмите кнопку **основного режима**и убедитесь, что сопоставления безопасности IPsec отображаются правильные удаленное адреса для настройки DirectAccess.  
  
## <a name="directaccess-server-connectivity-issues"></a>Проблемы с подключением сервера DirectAccess  
**Сценарий**. Пользователю не удается выполнить аутентификацию с помощью OTP с ошибкой: «Проверка подлинности не пройдена из-за внутренней ошибки»  
  
**Сообщение об ошибке** (журнал событий клиента)  
  
Один из следующих ошибок:  
  
-   Не удалось установить подключение к серверу удаленного доступа < DirectAccess_server_hostname >, используя базовый путь < OTP_authentication_path > и < OTP_authentication_port > порт. Код ошибки: < internal_error_code >.  
  
-   Невозможно отправить учетные данные пользователя для сервера удаленного доступа < DirectAccess_server_hostname >, используя базовый путь < OTP_authentication_path > и < OTP_authentication_port > порт. Код ошибки: < internal_error_code >.  
  
-   Ответ не был получен с сервера удаленного доступа < DirectAccess_server_hostname >, используя базовый путь < OTP_authentication_path > и < OTP_authentication_port > порт. Код ошибки: < internal_error_code >.  
  
**Причина**  
  
Клиентский компьютер не может получить доступ к серверу DirectAccess через Интернет, из-за либо проблемы с сетью или неправильной настройкой сервера IIS на сервере DirectAccess.  
  
**Решение**  
  
Убедитесь, что работает подключение к Интернету на клиентском компьютере и убедитесь, что служба DirectAccess находится запущен и доступен через Интернет.  
  
## <a name="failed-to-enroll-for-the-directaccess-otp-logon-certificate"></a>Не удалось зарегистрировать сертификата для входа методом OTP для DirectAccess  
**Сценарий**. Пользователю не удается выполнить аутентификацию с помощью OTP с ошибкой: «Проверка подлинности не пройдена из-за внутренней ошибки»  
  
**Сообщение об ошибке** (журнал событий клиента). Сбой при регистрации сертификата из ЦС < CA_name >. Запрос не был подписан с помощью сертификата подписи OTP должным образом, или пользователь не имеет разрешения на регистрацию.  
  
**Причина**  
  
Одноразовый пароль, предоставленный пользователем была выполнена без ошибок, но отклонено выдающего центра сертификации (ЦС) для выдачи сертификата OTP входа в систему. Запрос на сертификат может не быть подписан должным образом правильный расширенного использования ключа (политики приложения центра регистрации OTP), или пользователь не имеет разрешения «Регистрация» в шаблоне DA OTP.  
  
**Решение**  
  
Убедитесь, что методом OTP для DirectAccess пользователи имеют разрешение на регистрацию сертификата для входа методом OTP для DirectAccess и включение правильный «политика приложения» в связи с центром регистрации DA OTP шаблон подписи. Кроме того, убедитесь, что сертификата центра регистрации DirectAccess на сервере удаленного доступа является допустимым. См. в разделе шаблона сертификата OTP планирование 3.2 и 3.3 запланируйте сертификата центра регистрации.  
  
## <a name="missing-or-invalid-computer-account-certificate"></a>Отсутствующий или недопустимый сертификат учетной записи компьютера  
**Сценарий**. Пользователю не удается выполнить аутентификацию с помощью OTP с ошибкой: «Проверка подлинности не пройдена из-за внутренней ошибки»  
  
**Сообщение об ошибке** (журнал событий клиента).  Проверки подлинности OTP не удается завершить, поскольку не удалось найти сертификат компьютера, который требуется для OTP в хранилище сертификатов локального компьютера.  
  
**Причина**  
  
Проверка подлинности методом OTP для DirectAccess требуется сертификат клиента компьютера для установки SSL-соединения с сервером DirectAccess; Тем не менее сертификата клиентского компьютера не найден или является недопустимым, например, если срок действия сертификата истек.  
  
**Решение**  
  
Убедитесь, что сертификат компьютера существует и является допустимым:  
  
1.  На клиентском компьютере, в консоли сертификатов MMC, учетной записи локального компьютера, откройте **личные/сертификаты**.  
  
2.  Убедитесь, что сертификат выдан, соответствующий имени компьютера и дважды щелкните сертификат.  
  
3.  На **сертификат** диалоговом окне **путь к сертификату** в списке **статус сертификата**, убедитесь, что отображается надпись «этого сертификата — ОК».  
  
Если действительный сертификат не найден, удалите недопустимый сертификат (если он существует) и выполните повторную регистрацию для сертификата компьютера, либо запустив `gpupdate /Force` из строки с повышенными привилегиями команду или перезагрузка компьютера-клиента.  
  
## <a name="missing-ca-that-issues-otp-certificates"></a>Отсутствует ЦС, выдающий сертификаты OTP  
**Сценарий**. Пользователю не удается выполнить аутентификацию с помощью OTP с ошибкой: «Проверка подлинности не пройдена из-за внутренней ошибки»  
  
**Сообщение об ошибке** (журнал событий клиента). Невозможно выполнить проверки подлинности OTP, поскольку DA сервер не возвратил адреса выдающий ЦС.  
  
**Причина**  
  
Нет ЦС, выдавать сертификаты OTP настроены либо все настроенные ЦС, выдающими сертификаты OTP, отвечать на запросы.  
  
**Решение**  
  
1.  Используйте следующую команду, чтобы получить список ЦС, выдающими сертификаты OTP (имя ЦС отображается в CAServer): `Get-DAOtpAuthentication`.  
  
2.  Если ЦС не настроены:  
  
    1.  Используйте либо команду `Set-DAOtpAuthentication` или консоли управления удаленным доступом, чтобы настроить ЦС, выдающими DirectAccess OTP сертификата для входа.  
  
    2.  Применить новую конфигурацию и заставить клиентов, чтобы обновить параметры объектов групповой Политики DirectAccess, выполнив `gpupdate /Force` из строки с повышенными привилегиями команду или перезагрузив компьютер клиента.  
  
3.  Если настроить ЦС, убедитесь, что они online и отвечает на запросы на регистрацию.  
  
## <a name="misconfigured-directaccess-server-address"></a>Неправильно настроенные адрес сервера DirectAccess  
**Сценарий**. Пользователю не удается выполнить аутентификацию с помощью OTP с ошибкой: «Проверка подлинности не пройдена из-за внутренней ошибки»  
  
**Сообщение об ошибке** (журнал событий клиента). Проверка подлинности OTP не удается правильно завершить. Не удается определить имя или адрес сервера удаленного доступа.  Код ошибки: < error_code >. Параметры DirectAccess должны проверяться администратором сервера.  
  
**Причина**  
  
Неправильно настроен адрес сервера DirectAccess.  
  
**Решение**  
  
Проверка настроенных DirectAccess серверу адрес с помощью `Get-DirectAccess` и исправьте адрес, если он настроен неправильно.  
  
Убедитесь, что последние параметры развертываются на клиентском компьютере, выполнив `gpupdate /force` из командной строки с повышенными или перезагрузите компьютер клиента.  
  
## <a name="failed-to-generate-the-otp-logon-certificate-request"></a>Не удалось создать запрос на сертификат входа OTP  
**Сценарий**. Пользователю не удается выполнить аутентификацию с помощью OTP с ошибкой: «Проверка подлинности не пройдена из-за внутренней ошибки»  
  
**Сообщение об ошибке** (журнал событий клиента). Не удается инициализировать запрос на сертификат для проверки подлинности OTP. Невозможно создать закрытый ключ, или пользователь <username> не может получить доступ к < OTP_template_name > шаблон сертификата на контроллере домена.  
  
**Причина**  
  
Существуют две возможные причины этой ошибки:  
  
-   У пользователя нет разрешения на чтение шаблона входа OTP.  
  
-   На компьютере нет доступа к контроллеру домена из-за проблемы с сетью.  
  
**Решение**  
  
-   Просмотрите разрешения на шаблон входа OTP и убедитесь, что все пользователи, подготовленные для DirectAccess OTP «разрешение на чтение».  
  
-   Убедитесь, что контроллер домена настроен как сервер управления и что клиентском компьютере можно получить доступ к контроллеру домена через туннель инфраструктуры. См. в разделе 3.2 плана шаблона сертификата OTP.  
  
## <a name="no-connection-to-the-domain-controller"></a>Нет подключения к контроллеру домена  
**Сценарий**. Пользователю не удается выполнить аутентификацию с помощью OTP с ошибкой: «Проверка подлинности не пройдена из-за внутренней ошибки»  
  
**Сообщение об ошибке** (журнал событий клиента). Не удалось установить соединение с контроллером домена для проверки подлинности OTP. Код ошибки: < error_code >.  
  
**Причина**  
  
Существуют две возможные причины этой ошибки:  
  
-   На компьютере имеет отсутствует сетевое подключение.  
  
-   Контроллер домена недоступен через туннель инфраструктуры.  
  
**Решение**  
  
-   Убедитесь, что контроллер домена, настроен как сервер управления, выполнив следующую команду в командной строке PowerShell: `Get-DAMgmtServer -Type All`.  
  
-   Убедитесь, что компьютер клиента имеет доступ к контроллеру домена через туннель инфраструктуры.  
  
## <a name="otp-provider-requires-challengeresponse"></a>Поставщик OTP требует запрос/ответ  
**Сценарий**. Пользователю не удается выполнить аутентификацию с помощью OTP с ошибкой: «Проверка подлинности не пройдена из-за внутренней ошибки»  
  
**Сообщение об ошибке** (журнал событий клиента). Проверка подлинности OTP с сервера удаленного доступа (< DirectAccess_server_name >) для пользователя (<username>) требуется пройти от пользователя.  
  
**Причина**  
  
Поставщик OTP, используемый требует от пользователя ввести дополнительные учетные данные в виде обмена запрос/ответ RADIUS, который не поддерживается в Windows Server 2012 DirectAccess OTP.  
  
**Решение**  
  
Настройка OTP поставщика не требуется вызов ответ в любом сценарии.  
  
## <a name="incorrect-otp-logon-template-used"></a>Неправильный шаблон входа OTP, используемый  
**Сценарий**. Пользователю не удается выполнить аутентификацию с помощью OTP с ошибкой: «Проверка подлинности не пройдена из-за внутренней ошибки»  
  
**Сообщение об ошибке** (журнал событий клиента). Шаблон ЦС, из которых пользователь <username> запрошенный сертификат не настроен для выдачи сертификатов для OTP.  
  
**Причина**  
  
Был заменен шаблон входа методом OTP для DirectAccess и клиентский компьютер пытается выполнить аутентификацию с помощью старом шаблоне.  
  
**Решение**  
  
Убедитесь, что клиентский компьютер использует последнюю конфигурацию OTP, выполнив одну из следующих:  
  
-   Принудительное обновление групповой политики, выполнив следующую команду из командной строки с повышенными правами: `gpupdate /Force`.  
  
-   Перезапустите клиентский компьютер.  
  
## <a name="missing-otp-signing-certificate"></a>Отсутствует сертификат для подписи OTP  
**Сценарий**. Пользователю не удается выполнить аутентификацию с помощью OTP с ошибкой: «Проверка подлинности не пройдена из-за внутренней ошибки»  
  
**Сообщение об ошибке** (журнал событий клиента). Не удалось найти сертификат подписи OTP. Не удалось подписать запрос на регистрацию сертификата OTP.  
  
**Причина**  
  
Не удается найти сертификат для подписи методом OTP для DirectAccess на сервере удаленного доступа; Таким образом запрос на сертификат пользователя не может быть подписан сервера удаленного доступа. Отсутствует сертификат подписи, или сертификат для подписи истек и не была обновлена.  
  
**Решение**  
  
Выполните эти действия на сервере удаленного доступа.  
  
1.  Проверьте настроенные OTP подписи имя шаблона сертификата, выполнив командлет PowerShell `Get-DAOtpAuthentication` и проверьте значение `SigningCertificateTemplateName`.  
  
2.  Используйте оснастку MMC для сертификатов, чтобы убедиться в том, что на компьютере имеется действительный сертификат, зарегистрированных на основе этого шаблона.  
  
3.  Если сертификат не существует, удалите просроченного сертификата (если он существует) и зарегистрировать новый сертификат на основе этого шаблона.  
  
Для создания OTP подписывания сертификата см. в разделе 3.3 плана сертификата центра регистрации.  
  
## <a name="missing-or-incorrect-upndn-for-the-user"></a>Отсутствует или неверен имени участника-пользователя, доменное имя для пользователя  
**Сценарий**. Пользователю не удается выполнить аутентификацию с помощью OTP с ошибкой: «Проверка подлинности не пройдена из-за внутренней ошибки»  
  
**Сообщение об ошибке** (журнал событий клиента)  
  
Один из следующих ошибок:  
  
-   Пользователь <username> не может выполнять аутентификацию с помощью OTP. Убедитесь, что имя участника-пользователя определен для имени пользователя в Active Directory. Код ошибки: < error_code >.  
  
-   Пользователь <username> не может выполнять аутентификацию с помощью OTP. Убедитесь, что DN определен для имени пользователя в Active Directory. Код ошибки: < error_code >.  
  
**Сообщение об ошибке** (журнал событий сервера)  
  
Имя пользователя <username> для проверки подлинности OTP не существует.  
  
**Причина**  
  
Пользователь не имеет имя участника-пользователя (UPN) или различающееся имя (DN) правильно установлены в учетной записи пользователя, эти свойства необходимы для правильной работы OTP для DirectAccess.  
  
**Решение**  
  
Используйте консоль Active Directory — пользователи и компьютеры на контроллере домена, чтобы убедиться, что оба эти атрибута заданы правильно для проверки подлинности пользователя.  
  
## <a name="otp-certificate-is-not-trusted-for-login"></a>OTP сертификат не является доверенным для имени входа  
**Сценарий**. Пользователю не удается выполнить аутентификацию с помощью OTP с ошибкой: «Проверка подлинности не пройдена из-за внутренней ошибки»  
  
**Причина**  
  
ЦС, выдающего сертификаты OTP не находится в хранилище NTAuth предприятия; Таким образом зарегистрированных сертификатов не может использоваться для входа в систему. Это может произойти в нескольких домена и в нескольких лесах средах, где междоменного доверия ЦС не будет установлено.  
  
**Решение**  
  
Убедитесь, что сертификат корень иерархии ЦС, выдающего сертификаты OTP установлен на предприятии, в хранилище NTAuth сертификатов домена, к которому пользователь пытается выполнить проверку подлинности.  
  
## <a name="windows-could-not-verify-user-credentials"></a>Windows не удалось проверить учетные данные пользователя  
**Сценарий**. Пользователю не удается выполнить аутентификацию с помощью OTP с ошибкой: «Проверка подлинности не пройдена из-за внутренней ошибки»  
  
**Сообщение об ошибке** (клиентского компьютера). Произошла ошибка Windows проверка учетных данных. Повторите попытку или обратиться за помощью к администратору.  
  
**Причина**  
  
Протокол проверки подлинности Kerberos работает не в том случае, если сертификат входа DirectAccess OTP не поддерживает список отзыва Сертификатов. Сертификат входа DirectAccess OTP не поддерживает список отзыва Сертификатов, так как либо:  
  
-   Шаблон входа методом OTP для DirectAccess был настроен с параметром **не включают сведения об отзыве в выданных сертификатов**.  
  
-   В ЦС настроен не для публикации списков отзыва сертификатов.  
  
**Решение**  
  
1.  Чтобы подтвердить причину этой ошибки, в консоли управления удаленным доступом в **шаг 2 сервер удаленного доступа**, нажмите кнопку **изменить**, а затем в **установки сервера удаленного доступа** мастер, нажмите кнопку **шаблонов сертификатов для OTP**. Запомните или запишите шаблона сертификата, используемого для подачи заявок на сертификаты, выданные для проверки подлинности OTP. Откройте консоль центра сертификации в области слева щелкните **шаблонов сертификатов**, дважды щелкните сертификат OTP входа в систему для просмотра свойств шаблона сертификата.  
  
    Чтобы решить эту проблему, настройте сертификат для сертификата для входа OTP и не устанавливайте **не включают сведения об отзыве в выданных сертификатов** флажок на **Server** вкладке шаблона диалоговое окно свойств.  
  
2.  На сервере ЦС, откройте консоль Управления центра сертификации, выдающий ЦС щелкните правой кнопкой мыши и нажмите кнопку **свойства**. На **расширения** вкладке убедитесь, что правильно настроена публикация списков отзыва Сертификатов.  
  

