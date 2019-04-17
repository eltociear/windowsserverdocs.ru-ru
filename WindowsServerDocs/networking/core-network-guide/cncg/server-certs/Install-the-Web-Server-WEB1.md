---
title: Установка веб-сервера WEB1
description: Этот раздел входит руководство развертывание сервера сертификатов для развертывания беспроводных и проводных сетей 802.1 X
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: f51c9e38-98bb-49c1-9d39-427d07021499
ms.author: pashort
author: shortpatti
ms.openlocfilehash: e818eac49719b394a2c73cc125a2e7ba9ea80c82
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/28/2018
---
# <a name="install-the-web-server-web1"></a>Установка веб-сервера WEB1

>Область применения: Windows Server (канал точками годовой), Windows Server 2016

Роль веб-сервер (IIS) в Windows Server 2016 предоставляет безопасную, простую в управлении, модульную и расширяемую платформу для надежного размещения веб-сайтов, служб и приложений. Со службами IIS общий доступ к информации пользователям в Интернете, интрасети или экстрасети. IIS является унифицированной веб-платформой, которая интегрирует IIS, ASP.NET, службы FTP, PHP и Windows Communication Foundation (WCF).  

При развертывании сертификаты сервера веб-сервер предоставляет расположение, где можно опубликовать список отзыва сертификатов (CRL) для центра сертификации (ЦС). После публикации он доступен для всех компьютеров в сети, чтобы они использовали этот список во время процесса проверки подлинности, чтобы убедиться, что сертификаты, предоставленному другие компьютеры не отозван.   

Если список отзыва Сертификатов как отозван сертификат, усилия проверки подлинности завершается сбоем, и компьютер будет защищен доверия сущность, которая содержит сертификат, который больше не действительна.  

Прежде чем установить роль веб-сервера (IIS), убедитесь, что настроено имя сервера и IP-адрес и присоединения компьютера к домену.  

## <a name="to-install-the-web-server-iis-server-role"></a>Установка роли сервера веб-сервер (IIS)  
Для выполнения этой процедуры необходимо быть членом **Администраторы** группы.  

>[!NOTE]  
>Чтобы выполнить эту процедуру с помощью Windows PowerShell, откройте PowerShell, введите следующую команду и нажмите клавишу ВВОД.  
`Install-WindowsFeature Web-Server -IncludeManagementTools`  

1.  В диспетчере серверов щелкните **управление**, а затем нажмите кнопку **Добавить роли и компоненты**. Откроется мастер добавления ролей и компонентов.  
2.  В **перед началом**, нажмите кнопку **Далее**.  

**Примечание**   
**Перед началом** страница мастера компонентов и добавить роли не отображается, если ранее выполнения добавления ролей и компонентов мастер, и вы выбрали **пропустить эту страницу по умолчанию** в данный момент.  

3.  На **типа установки** щелкните **Далее**.  
4.  На **Выбор сервера** щелкните **Далее**.  
5.  На **ролей сервера** выберите **веб-сервер (IIS)**, а затем нажмите кнопку **Далее**.  
6.  Нажмите кнопку **Далее** пока вы приняли все значения по умолчанию параметры веб-сервера и нажмите кнопку **установить**.  
7.  Убедитесь в успешном завершении установки всех компонентов, а затем нажмите кнопку **закрыть**.