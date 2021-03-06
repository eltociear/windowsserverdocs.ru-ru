---
ms.assetid: e1f2ce2d-b24f-4ccd-8add-9e69419fc6c1
title: Импорт сертификата проверки подлинности сервера на веб-сайт по умолчанию
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 3f02358167b024247f934a46218028575e393ba9
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/08/2020
ms.locfileid: "80855407"
---
# <a name="import-a-server-authentication-certificate-to-the-default-web-site"></a>Импорт сертификата проверки подлинности сервера на веб-сайт по умолчанию

После получения сертификата проверки подлинности сервера из центра сертификации \(ЦС\)необходимо вручную установить этот сертификат на веб-сайте по умолчанию для каждого сервера федерации или прокси-сервера федерации в ферме серверов.  
  
Для веб-серверов необходимо вручную установить сертификат аутентификации сервера на соответствующем веб-сайте или виртуальном каталоге, где хранится федеративное приложение.  
  
При настройке фермы не забудьте выполнить эту процедуру аналогичным образом, используя одинаковые параметры на каждом сервере фермы.  
  
> [!NOTE]  
> \-оснастки управления AD FS в относится к сертификатам проверки подлинности сервера для серверов федерации в качестве сертификатов связи служб.  
  
Для выполнения этой процедуры требуется членство в группе **Администраторы** или в эквивалентной группе на локальном компьютере.  Просмотрите сведения об использовании соответствующих учетных записей и членстве в группах в [локальной среде и группах домена по умолчанию](https://go.microsoft.com/fwlink/?LinkId=83477).   
  
### <a name="to-import-a-server-authentication-certificate-to-the-default-web-site"></a>Импорт сертификата проверки подлинности сервера на веб-сайт по умолчанию  
  
1.  На **начальном** экране введите**службы IIS \(диспетчер\) IIS**, а затем нажмите клавишу ВВОД.  
  
2.  В дереве консоли щелкните **ComputerName**.  
  
3.  В центральной области дважды\-щелкните **Сертификаты сервера**.  
  
4.  На панели **Действия** щелкните **Импорт**.  
  
5.  В области **Импорт сертификатов** нажмите кнопку **…** .  
  
6.  Перейдите к месту расположения файла сертификата pfx, выделите его, а затем нажмите кнопку **Открыть**.  
  
7.  Наберите пароль для сертификата и нажмите кнопку **ОК**.  
  
## <a name="additional-references"></a>Дополнительная справка  
[Контрольный список: Настройка сервера федерации](Checklist--Setting-Up-a-Federation-Server.md)  
  
[Контрольный список: Настройка прокси-сервера федерации](Checklist--Setting-Up-a-Federation-Server-Proxy.md)  
  
[Требования к сертификатам для серверов федерации](https://technet.microsoft.com/library/dd807040.aspx)  
  
[Требования к сертификатам для прокси-серверов федерации](https://technet.microsoft.com/library/dd807054.aspx)  
   
  

