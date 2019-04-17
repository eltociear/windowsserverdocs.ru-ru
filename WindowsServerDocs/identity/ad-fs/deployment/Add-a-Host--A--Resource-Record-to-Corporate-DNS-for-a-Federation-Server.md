---
ms.assetid: 026747c7-4c34-41c7-b7ea-27f9a7f64a35
title: "Добавление записи ресурса узла (A) в корпоративной DNS для сервера федерации"
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 425cfe794095f1515eb3fae2f1a5e5db90ba3d00
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/12/2017
---
# <a name="add-a-host-a-resource-record-to-corporate-dns-for-a-federation-server"></a>Добавление записи ресурса узла (A) в корпоративной DNS для сервера федерации

>Область применения: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012


Для клиентов в корпоративной сети успешно доступ сервера федерации с использованием встроенной проверки подлинности Windows в корпоративной системе доменных имен \(DNS\), разрешает имя узла сервера федерации учетных записей предварительно необходимо создать запись ресурса узла \(A\) \ (например, fs.fabrikam.com\) в IP-адрес сервера федерации или кластера сервера федерации. Можно использовать следующую процедуру для добавления записи ресурса \(A\) узла в корпоративную систему DNS для сервера федерации.  
  
Членство в группе **Администраторы**, или в эквивалентной минимальным требованием для выполнения этой процедуры.  Подробные сведения об использовании соответствующих учетных записей и членстве в группах в [локальные и доменные группы по умолчанию ](https://go.microsoft.com/fwlink/?LinkId=83477).   
  
### <a name="to-add-a-host-a-resource-record-to-corporate-dns-for-a-federation-server"></a>Добавление записи ресурса узла \(A\) корпоративной DNS для сервера федерации  
  
1.  На DNS-сервере корпоративной сети откройте DNS оснастка.  
  
2.  В консоли дерева, щелкните правой кнопкой мыши зону прямого просмотра, а затем щелкните **новый узел \(A or AAAA\)**.  
  
3.  В **имя**, введите только имя компьютера сервера федерации или кластера серверов федерации; Например, для полное доменное имя \(FQDN\) fs.fabrikam.com тип **fs**.  
  
4.  В **IP-адрес**, введите IP-адрес для сервера федерации или кластера сервера федерации, например, 192.168.1.4.  
  
5.  Нажмите кнопку **добавления узла**.  
  
## <a name="additional-references"></a>Дополнительные ссылки  
[Контрольный список: Настройка сервера федерации](Checklist--Setting-Up-a-Federation-Server.md)  
  
[Требования к разрешению имен для серверов федерации](https://technet.microsoft.com/library/dd807055.aspx)  
  
