---
ms.assetid: 208928eb-bb17-4984-a312-23fff43133e3
title: Усовершенствования аудита в AD FS под управлением Windows Server 2016
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 10/25/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 2f6e4abb4255281be85b7fa928566f681bcf2de2
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/24/2019
ms.locfileid: "66188359"
---
# <a name="auditing-enhancements-to-ad-fs-in-windows-server-2016"></a>Усовершенствования аудита в AD FS под управлением Windows Server 2016


В настоящее время в AD FS для Windows Server 2012 R2 существует являются многочисленные события аудита, созданные для одного запроса и соответствующие сведения о входа или выдачи маркера действия либо отсутствуют (в некоторых версиях AD FS) или распределяться на несколько событий аудита. По умолчанию AD FS события аудита будут отключены из-за своей природе verbose.  
    С появлением AD FS в Windows Server 2016 аудит стала более простой и менее многословный.  
  
## <a name="auditing-levels-in-ad-fs-for-windows-server-2016"></a>Аудит уровня в AD FS для Windows Server 2016  
По умолчанию AD FS в Windows Server 2016 имеет базовый аудит включен.  С помощью основные возможности аудита, администраторы будут см. в разделе не более пяти события для отдельного запроса.  Это обозначает значительное уменьшается число событий, которые администраторы имеют просмотра, чтобы увидеть одного запроса.   Уровень аудита можно быть увеличивается или уменьшается, используя командлет PowerShell:  SET-AdfsProperties - AuditLevel.  В таблице ниже приведены доступные уровни аудита.  
  
||||  
|-|-|-|  
|Уровень аудита|Синтаксис PowerShell|Описание|  
|Нет|SET-AdfsProperties - AuditLevel None|Аудит отключен и события не регистрируются.|  
|Basic (по умолчанию)|SET-AdfsProperties - AuditLevel Basic|Не более 5 события будут регистрироваться для отдельного запроса|  
|Verbose|Set-AdfsProperties - AuditLevel Verbose|Регистрируются все события.  Это позволит входить значительный объем сведения каждого запроса.|  
  
Чтобы просмотреть текущий уровень аудита, можно использовать командлет PowerShell:  Get-AdfsProperties.  
  
![улучшения аудита](media/Auditing-Enhancements-to-AD-FS-in-Windows-Server-2016/ADFS_Audit_1.PNG)  
  
Уровень аудита можно быть увеличивается или уменьшается, используя командлет PowerShell:  SET-AdfsProperties - AuditLevel.  
  
![улучшения аудита](media/Auditing-Enhancements-to-AD-FS-in-Windows-Server-2016/ADFS_Audit_2.png)  
  
## <a name="types-of-audit-events"></a>Типы событий аудита  
События аудита AD FS может относиться к разным типам, исходя из различных типов запросов, обработанных службами AD FS. Каждый тип событий аудита имеет данных, связанных с ним.  Тип событий аудита могут отличаться от запросов на вход (т. е. запросы маркеров) и запросы системы (вызовы сервера, включая получение сведений о конфигурации).    
  В следующей таблице описываются основные типы событий аудита.  
  
||||  
|-|-|-|  
|Тип событий аудита|Идентификатор события|Описание|  
|Успех проверки новых учетных данных|1202|Запрос, где новые учетные данные проверяются успешно службой федерации. Это включает в себя WS-Trust, WS-Federation, SAML-P (первый этап для создания единого входа) и конечных точек авторизации OAuth.|  
|Ошибка проверки новой учетных данных|1203|Запрос, где сбой проверки новых учетных данных в службе федерации. Это включает в себя WS-Trust, WS-Fed, SAML-P (первый этап для создания единого входа) и конечных точек авторизации OAuth.|  
|Приложение успешно маркеров|1200|Запрос, где успешно выданный маркер безопасности службой федерации. Для WS-Federation, SAML-P, это действие регистрируется, когда запрос обрабатывается с артефактом единого входа. (например, файл cookie единого входа).|  
|Сбой маркера приложения|1201|Запрос, где сбой выдачи маркеров безопасности в службе федерации. Для WS-Federation, SAML-P, это действие регистрируется при обработке запроса с артефактом единого входа. (например, файл cookie единого входа).|  
|Запрос на изменение пароля успешно|1204|Транзакции, где запрос на смену пароля успешно обработан службой федерации.|  
|Ошибка запроса изменения пароля|1205|Не удалось обработать службой федерации транзакций, где запрос на смену пароля.| 
|Выйдите из системы успешно|1206|Описывает успешный запрос выхода.|  
|Выйдите из системы сбоя|1207|Описывает Невыполненный запрос выхода.|  

  

