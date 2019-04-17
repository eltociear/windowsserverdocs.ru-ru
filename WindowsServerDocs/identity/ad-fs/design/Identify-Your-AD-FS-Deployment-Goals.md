---
ms.assetid: c81b8291-fba5-4b30-a43d-7feb2f4b66be
title: "Руководство по разработке служб AD FS в Windows Server 2012 R2"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: f618add4c4803142b3bd7278908834a412f30999
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/03/2017
---
# <a name="identify-your-ad-fs-deployment-goals"></a>Определение целей развертывания AD FS

>Область применения: Windows Server 2016, Windows Server 2012 R2

Правильное определение целей по развертыванию служб федерации Active Directory \(AD FS\) — залог успеха проекта по разработке вашей службы федерации Active Directory. Определять их приоритеты и необходимости объединяя целей развертывания, чтобы можно было разрабатывать и развертывать AD FS с помощью итераций. Можно воспользоваться существующими, задокументированы и заранее определенных целей развертывания AD FS, необходимых в AD FS проекты и разработать рабочее решение для конкретной ситуации.  
  
Предыдущие версии AD FS были наиболее часто развертывается в следующих целях:  
  
-   Предоставление сотрудникам или клиентам с веб-, единый вход для доступа к приложениям на основе claims\ на предприятии.  
  
-   Предоставление сотрудникам или клиентам с веб-службы Единого входа для доступа к ресурсам в любой партнерской организации федерации.  
  
-   Предоставление сотрудникам или клиентам с веб-, единый вход для удаленного доступа внутренне веб-сайты или службы.  
  
-   Предоставление сотрудникам или клиентам с веб-службы Единого входа для доступа к ресурсам и службам в облаке.  
  
Помимо этих AD FS в Windows Server® 2012 R2 добавляет функциональные возможности, которые могут помочь в следующих целях:  
  
-   Присоединение к рабочему месту устройства для единого входа и эффективная двухфакторной проверки подлинности. Это позволяет организациям разрешать доступ с личных устройств пользователей и управлять рисками при предоставлении доступа.  
  
-   Управление рисками с использованием несколькими управления доступом. Службы федерации Active Directory предоставляют широкий уровень авторизации, контролирующий, кто имеет доступ к каким приложениям. Это может быть основан на атрибутах пользователя \ (таких как UPN, электронная почта, членство в группе безопасности, серьезность проверки подлинности, т. д. \), атрибутах устройства \ (если устройство является joined\ рабочему месту) или атрибутах запроса \ (сети в расположение, IP-адрес или agent\ пользователя).  
  
-   Управление рисками с помощью дополнительных несколькими двухфакторной проверки подлинности для уязвимых приложений. Службы федерации Active Directory позволяет управлять политиками, чтобы при необходимости требовать несколькими двухфакторной проверки подлинности глобально или на основе каждого приложения. Кроме того службы федерации Active Directory предоставляют точки расширяемости для любого поставщика коэффициент используется в целях тесной интеграции для обеспечения беспроблемного и безопасного несколькими коэффициент взаимодействия с пользователем для конечных пользователей.  
  
-   Предоставление возможностей проверки подлинности и авторизации для доступа к веб-ресурсы из экстрасети, защищенным с помощью прокси веб-приложения.  
  
Таким образом, можно развернуть службы федерации Active Directory в Windows Server 2012 R2 для достижения следующих целей, в вашей организации:  
  
### <a name="enable-your-users-to-access-resources-on-their-personal-devices-from-anywhere"></a>Разрешить пользователям доступ к ресурсам с личных устройств из любого места  
  
-   Присоединение к рабочему месту предоставляет пользователям возможность присоединить свои личные устройства к корпоративной Active Directory и в результате получить доступ и возможность взаимодействия при обращении к корпоративным ресурсам с этих устройств.  
  
-   Предварительно-проверка подлинности ресурсов в корпоративной сети, защищенных прокси-веб-приложения и доступных из Интернета.  
  
-   Изменение пароля, чтобы пользователи могли изменять свои пароли с любого устройства, присоединенного к рабочему месту, чтобы они могли продолжать получать доступ к ресурсам срока действия пароля.  
  
### <a name="enhance-your-access-control-risk-management-tools"></a>Улучшения вашей риск средства управления доступом  
Управление рисками является важным аспектом управления и обеспечения соответствия в каждой ИТ-организации. Существует множество контроля доступа улучшений в управлении рисками в AD FS в Windows Server® 2012 R2, включая следующие:  
  
-   Гибкое управление на основе расположения сети для указания того, как пользователю проходить проверку подлинности для доступа к защищенному AD FS\ приложения.  
  
-   Гибкая политика для определения того, если требуется выполнять несколькими фактор проверки подлинности на основе данных пользователя, данных устройства и сетевого расположения пользователя.  
  
-   Контроль кусту приложения для игнорирования единого входа и принуждения пользователя ввести учетные данные каждый раз при доступе к конфиденциальному приложению.  
  
-   Политика гибкого доступа кусту приложения на основе данных пользователя, данных устройства или сетевое расположение.  
  
-   AD FS Extranet Lockout, которая позволяет администраторам защищать учетные записи Active Directory от атак методом перебора из Интернета.  
  
-   Отзыв доступа для любого устройства присоединен к рабочему месту, которое отключено или удалено в Active Directory.  
  
### <a name="use-ad-fs-to-enhance-the-sign-in-experience"></a>Использование AD FS для повышения удобства процедуры входа  
Ниже перечислены новые возможности AD FS в Windows Server® 2012 R2, позволяющие администратору настраивать и расширять возможности входа.  
  
-   Единая Настройка службы AD FS, когда изменения вносятся только один раз и затем автоматически распространяются на остальные серверы федерации AD FS в конкретной ферме.  
  
-   Обновленные одной страницы, имеющие современный внешний вид и автоматически обслуживающие различные форм-факторы.  
  
-   Поддержка автоматического возврата к проверке подлинности на основе forms\ для устройств, которые не присоединены к корпоративному домену, но по-прежнему используются для создания запросов доступа из корпоративной сети \(intranet\).  
  
-   Простые элементы управления для настройки эмблемы компании, изображения, стандартных ссылок для ИТ-поддержки, домашней страницы, конфиденциальности, и т. д.  
  
-   Настройка описательных сообщений на страницах входа.  
  
-   Настройка веб-тем.  
  
-   \(HRD\) домашней области обнаружения на основе суффикса организации пользователя для улучшенной конфиденциальности партнеров компании.  
  
-   Фильтрация HRD по кусту приложения для автоматического выбора области в зависимости от приложения.  
  
-   Нажмите кнопку One\ отчеты об ошибках для упрощения ИТ устранения неполадок.  
  
-   Настраиваемые сообщения об ошибках.  
  
-   Выбор проверки подлинности пользователя при наличии нескольких поставщиков проверки подлинности.  
  
## <a name="see-also"></a>См. также:  
[Руководство по разработке служб AD FS в Windows Server 2012 R2](../../ad-fs/design/AD-FS-Design-Guide-in-Windows-Server-2012-R2.md)  
  
