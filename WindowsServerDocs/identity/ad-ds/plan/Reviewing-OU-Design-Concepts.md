---
ms.assetid: 41b56704-c6f9-4d29-af97-62123e300565
title: "Просмотр понятиях проекта Подразделения"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 0e832d068a4d03316853d8b59e3f2ac4a6ebc816
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/03/2017
---
# <a name="reviewing-ou-design-concepts"></a>Просмотр понятиях проекта Подразделения

>Область применения: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Структура подразделения (OU) для домена включает в себя следующее:  
  
-   Схема иерархии Подразделений  
  
-   Список подразделений  
  
-   Для каждого Подразделения:  
  
    -   Назначение для Подразделения  
  
    -   Список пользователей или групп, которые могут контролировать, Подразделения или объекты в Подразделении  
  
    -   Тип элемента управления, пользователи и группы имеют над объектами в Подразделении  
  
Иерархия Подразделений не требуется отразить иерархии подразделений организации или группы. Приложение групповой политики или чтобы ограничить видимость объектов подразделений создаются для определенной цели, например делегированию прав администрирования.  
  
Вы можете создать структуру Подразделений и делегировать администрирование для отдельных пользователей или групп в организации, которым требуется автономность для управления собственные данные и ресурсы. Подразделения представляют административные границы и позволяет вам контролировать объем полномочий администраторов данных.  
  
Например можно создать Подразделение под названием ResourceOU и используйте его для хранения всех учетных записей компьютеров, принадлежащих к файлу и управляется группу серверов печати. Затем можно настроить безопасности в подразделении, так что только администраторы данных в группе имеют доступ к Подразделению. Это предотвращает незаконное изменение файла и учетных записей сервера печати администраторы данных в другие группы.  
  
Можно дополнительно уточнить структуру Подразделений, создав поддеревья подразделений для определенных целей, такие как приложение групповой политики или ограничить видимость защищенных объектов, чтобы только определенные пользователи могут их видеть. Например если необходимо применить групповую политику для выбранной группы пользователей или ресурсов, можно добавить этих пользователей или ресурсов к Подразделению и затем применить групповую политику к Подразделению. Также можно использовать иерархии Подразделений для дальнейшей делегирования административный контроль.  
  
Хотя технические ограничения на число уровней структуры Подразделений, которые не существуют, управляемость мы рекомендуем ограничить структуру Подразделений и не более 10 уровней. Технические ограничения количества подразделений на каждом уровне не существует. Обратите внимание что служб Active Directory домена (AD DS) — приложения с поддержкой может иметь ограничения на число символов, используемых в указанное различающееся имя (то есть полный облегченного доступа к каталогам LDAP Directory Access Protocol () путь в объект в каталоге) или на глубины Подразделения в иерархии.  
  
Структуры Подразделений в Доменных службах Active Directory не является видимым для конечных пользователей. Структуры Подразделений является средством администрирования для администраторов служб и для администраторов данных и легко изменить. По-прежнему для пересмотра и обновления проектирования структуры Подразделений в соответствии с изменениями структуры администратора и поддерживает администрирование на основе политики.  
  

