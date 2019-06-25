---
ms.assetid: e1f2ce2d-b24f-4ccd-8add-9e69419fc6c1
title: Импорт сертификата аутентификации сервера на веб-сайт по умолчанию
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: da91a3e8c34c86f7fd03ca875b3800fdb6001750
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/24/2019
ms.locfileid: "66192119"
---
# <a name="import-a-server-authentication-certificate-to-the-default-web-site"></a>Импорт сертификата аутентификации сервера на веб-сайт по умолчанию

После получения сервера проверки подлинности сертификата из центра сертификации \(ЦС\), необходимо вручную установить этот сертификат на по умолчанию веб-сайте для каждого сервера федерации или прокси-сервера федерации в ферме серверов.  
  
Для веб-серверов необходимо вручную установить сертификат аутентификации сервера на соответствующем веб-сайте или виртуальном каталоге, где хранится федеративное приложение.  
  
При настройке фермы не забудьте выполнить эту процедуру аналогичным образом, используя одинаковые параметры на каждом сервере фермы.  
  
> [!NOTE]  
> Оснастка управления AD FS\-в расценивает сертификаты проверки подлинности серверов для серверов федерации как сертификаты взаимодействия служб.  
  
Для выполнения этой процедуры минимальным требованием является членство в группе **Администраторы** или эквивалентные права на локальном компьютере.  Просмотрите сведения об использовании соответствующих учетных записей и членства в группах в [локальные и доменные группы по умолчанию](https://go.microsoft.com/fwlink/?LinkId=83477).   
  
### <a name="to-import-a-server-authentication-certificate-to-the-default-web-site"></a>Импорт сертификата аутентификации сервера на веб-сайт по умолчанию  
  
1.  На **запустить** введите**Internet Information Services \(IIS\) Manager**, и нажмите клавишу ВВОД.  
  
2.  В дереве консоли щелкните **Имя_компьютера**.  
  
3.  В центральной области дважды\-щелкните **сертификаты сервера**.  
  
4.  В области **Действия** щелкните **Импорт**.  
  
5.  В области **Импорт сертификатов** нажмите кнопку **…** .  
  
6.  Найдите местоположение PFX-файла сертификата, выделите его и щелкните **Открыть**.  
  
7.  Введите пароль для сертификата, а затем нажмите кнопку **ОК**.  
  
## <a name="additional-references"></a>Дополнительная справка  
[Контрольный список. Настройка сервера федерации](Checklist--Setting-Up-a-Federation-Server.md)  
  
[Контрольный список. Настройка прокси-сервера федерации](Checklist--Setting-Up-a-Federation-Server-Proxy.md)  
  
[Требования к сертификатам для серверов федерации](https://technet.microsoft.com/library/dd807040.aspx)  
  
[Требования к сертификатам для прокси-серверов федерации](https://technet.microsoft.com/library/dd807054.aspx)  
   
  
