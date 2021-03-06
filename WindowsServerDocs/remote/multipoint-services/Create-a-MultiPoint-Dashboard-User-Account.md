---
title: Создание учетной записи пользователя панели мониторинга MultiPoint
description: Создание учетной записи для использования с панелью мониторинга
ms.prod: windows-server
ms.technology: multipoint-services
ms.topic: article
ms.assetid: eb9d7da1-eb5e-42c0-8d59-bb6d7b007ea9
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 08/04/2016
ms.openlocfilehash: b94c02fe514b4f7a694b908600127eda7c664c09
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/08/2020
ms.locfileid: "80859797"
---
# <a name="create-a-multipoint-dashboard-user-account"></a>Создание учетной записи пользователя панели мониторинга MultiPoint
Учетные записи пользователей панелей мониторинга MultiPoint создаются для тех пользователей, которым необходим регулярный доступ к станциям без возможности управления системой служб MultiPoint. Пользователи с учетными записями пользователей панели мониторинга MultiPoint могут запускать большинство приложений и сохранять файлы, но не могут запускать диспетчер MultiPoint. Чтобы узнать, кто имеет доступ к панели мониторинга MultiPoint, в диспетчере MultiPoint перейдите на вкладку **Пользователи** . учетные записи панели мониторинга MultiPoint отображаются в столбце **тип учетной записи** как **пользователь панели мониторинга MultiPoint**.  
  
Если предполагается, что ваши пользователи MultiPoint Services будут хранить частные документы в Windows, каждый из них должен входить в систему MultiPoint Services, используя уникальное имя пользователя и пароль.  
  
> [!NOTE]  
> Дополнительные сведения о том, что нужно учитывать *пользователю с правами администратора* при создании и администрировании учетных записей, см. в статье [Соображения по поводу учетных записей пользователей](User-Account-Considerations.md).  
  
#### <a name="to-create-a-multipoint-dashboard-user-account"></a>Создание учетной записи MultiPoint Dashboard  
  
1.  В диспетчере MultiPoint перейдите на вкладку **Пользователи** .  
  
2.  В разделе **Задачи пользователей** нажмите **Добавить учетную запись пользователя**. Откроется мастер **Добавление учетной записи пользователя**.  
  
3.  В поле **Учетная запись пользователя** введите имя входа для пользователя.  
  
4.  В поле **Полное имя** введите имя пользователя в любом формате. Это может быть имя, фамилия или псевдоним.  
  
5.  В поле **Создайте пароль** введите пароль для пользователя. Этот пароль должен быть известен только вам и пользователю. Храните эти данные в безопасном месте. Изменять пароль может только пользователь с правами администратора.  
  
6.  В поле **Подтвердите пароль** введите пароль еще раз и нажмите кнопку **Далее**.  
  
7.  На уровне страницы доступа выберите пункт **Пользователь MultiPoint Dashboard** и нажмите кнопку **Далее**.  
  
8.  Нажмите кнопку **Готово**.  
  
## <a name="see-also"></a>См. также  
[Соображения по поводу учетных записей пользователей](User-Account-Considerations.md)