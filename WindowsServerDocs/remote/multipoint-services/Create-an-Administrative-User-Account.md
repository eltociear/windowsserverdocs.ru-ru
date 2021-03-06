---
title: Создание учетной записи пользователя с правами администратора
description: Создание учетной записи с правами администратора в службах MultiPoint
ms.prod: windows-server
ms.technology: multipoint-services
ms.topic: article
ms.assetid: 8ce4c5a9-3dec-412f-910b-54a252f8f209
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 08/04/2016
ms.openlocfilehash: 72b7517d35d18064806d3df35f2f9ed7b636df8d
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/08/2020
ms.locfileid: "80859777"
---
# <a name="create-an-administrative-user-account"></a>Создание учетной записи пользователя с правами администратора
Создание *учетных записей пользователей с правами администратора* для пользователей, которые будут управлять системой MultiPoint Services. Чтобы узнать, кто имеет административный доступ, в диспетчере MultiPoint перейдите на вкладку **Пользователи** . учетные записи пользователей с правами администратора отображаются в столбце **тип учетной записи** с **правами администратора**. *Пользователи с правами администратора* имеют доступ ко всем задачам MultiPoint Manager, которые изменяют настольные и системные параметры, такие как:  
  
-   Создание учетных записей  
  
-   Добавление и удаление программ  
  
-   Управление *рабочими столами* и оборудованием  
  
-   Завершение *сеансов* других пользователей  
  
Пользователи с правами администратора могут выполнять задачи, затрагивающие всех остальных пользователей системы MultiPoint Services, такие как установка программного обеспечение или изменение параметров безопасности. По этой причине пользователи с правами администратора должны иметь уникальные имена и пароли, известные только им.  
  
Дополнительные сведения о том, что нужно учитывать пользователю с правами администратора при создании и администрировании учетных записей, см. в статье [Рекомендации по учетным записям пользователей](User-Account-Considerations.md).  
  
> [!NOTE]  
> Для выполнения задач в системе MultiPoint Services, не связанных с управлением этой системой, можно создать *учетную запись обычного пользователя*. В этом случае вам нужно будет входить в учетную запись пользователя с правами администратора только для выполнения задач по управлению системой.  
  
#### <a name="to-create-an-administrative-user-account"></a>Создание учетной записи пользователя с правами администратора  
  
1.  В диспетчере MultiPoint перейдите на вкладку **Пользователи** .  
  
2.  В разделе **Задачи пользователей** нажмите **Добавить учетную запись пользователя**. Откроется мастер **Добавление учетной записи пользователя**.  
  
3.  В поле **Учетная запись пользователя** введите имя входа для пользователя. Обычно в качестве имени входа используется имя и фамилия, написанные слитно, либо инициалы и фамилия, набранные без пробелов.  
  
4.  В поле **Полное имя** введите имя пользователя в любом формате. Это может быть имя, фамилия или псевдоним.  
  
5.  В поле **Пароль** введите пароль для пользователя. Этот пароль должен быть известен только вам и пользователю. Храните эти данные в безопасном месте. Изменять пароль может только пользователь с правами администратора.  
  
6.  В поле **Подтвердите пароль** введите пароль еще раз и нажмите кнопку **Далее**.  
  
7.  На уровне страницы доступа выберите пункт **Администратор** и нажмите кнопку **Далее**.  
  
8.  MultiPoint Services проверит все данные и отобразит сообщение о том, что учетная запись настроена. Когда появится текст **Учетная запись пользователя успешно создана**, нажмите кнопку **Готово**.  
