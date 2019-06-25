---
title: Подготовка к миграции прокси-сервера федерации AD FS 2.0
description: Сведения о подготовке к миграции прокси-сервера AD FS в Windows Server 2012.
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/28/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 2b2275af0934413fa2de02de720d609feda7392c
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/31/2019
ms.locfileid: "66444450"
---
# <a name="prepare-to-migrate-the-ad-fs-20-federation-server-proxy"></a>Подготовка к миграции прокси-сервера федерации AD FS 2.0

Чтобы подготовиться к миграции прокси AD FS 2.0 federation server до Windows Server 2012, необходимо экспортировать и резервное копирование данных конфигурации AD FS с этого прокси-сервера.  Действия, описанные в этом разделе, относятся к сценарию с одним или несколькими прокси-серверами федерации.  
  
 Чтобы экспортировать данные конфигурации AD FS, выполните следующие действия.  
  
-   [Шаг 1. Экспорт параметров службы прокси-сервера](#step-1-export-proxy-service-settings)  
  
-   [Шаг 2. Резервное копирование пользовательских настроек веб-страницы](#step-2-back-up-webpage-customizations)  
  
##  <a name="step-1-export-proxy-service-settings"></a>Шаг 1. Экспорт параметров службы прокси-сервера  
 Чтобы экспортировать параметры службы прокси-сервера федерации, выполните следующие действия.  
  
### <a name="to-export-proxy-service-settings"></a>Экспорт параметров службы прокси-сервера  
  
1.  Экспортируйте SSL-сертификат и его закрытый ключ в PFX-файл. Дополнительные сведения см. в разделе [Экспорт части закрытого ключа сертификата проверки подлинности сервера](export-the-private-key-portion-of-a-server-authentication-certificate.md).  
  
> [!NOTE]
>  Этот шаг не является обязательным, потому что этот сертификат сохраняется во время обновления операционной системы.  
  
2. Экспортируйте свойства прокси-сервера федерации AD FS 2.0 в файл. Это можно сделать с помощью Windows PowerShell.  
  
Откройте Windows PowerShell и выполните следующую команду, чтобы добавить командлеты AD FS в сеанс Windows PowerShell: `PSH:>add-pssnapin “Microsoft.adfs.powershell”`. Затем выполните следующую команду для экспорта свойств прокси-сервера федерации в файл: `PSH:> Get-ADFSProxyProperties | out-file “.\proxyproperties.txt”`.  
  
3. Убедитесь, что вам известны данные учетной записи администратора сервера федерации AD FS или учетной записи службы, от имени которой выполняется служба федерации AD FS.  Эти сведения необходимы для настройки доверия прокси-сервера.  
  
   При выполнении этого шага осуществляется сбор следующих сведений, необходимых для настройки прокси-сервера федерации AD FS:  
  
-   имя службы федерации AD FS;  
  
-   имя учетной записи домена, которая необходима для настройки доверия прокси-сервера;  
  
-   адрес и порт прокси-сервера HTTP (если между прокси-сервером федерации AD FS и серверами федерации AD FS есть прокси-сервер HTTP).  
  
##  <a name="step-2-back-up-webpage-customizations"></a>Шаг 2. Резервное копирование пользовательских настроек веб-страницы  
 Чтобы выполнить резервное копирование пользовательских настроек веб-страницы, скопируйте веб-страницы прокси-сервера AD FS и файл **web.config** из каталога, сопоставленного виртуальному пути **“/adfs/ls”** , в IIS.  По умолчанию он находится в каталоге **%systemdrive%\inetpub\adfs\ls**.  
  
## <a name="next-steps"></a>Следующие шаги
 [Подготовка к миграции сервера AD FS 2.0 Federation](prepare-to-migrate-ad-fs-fed-server.md)   
 [Подготовка к миграции прокси-сервера AD FS 2.0 Federation](prepare-to-migrate-ad-fs-fed-proxy.md)   
 [Перенос сервера AD FS 2.0 Federation](migrate-the-ad-fs-fed-server.md)   
 [Перенос прокси-сервера AD FS 2.0 Federation](migrate-the-ad-fs-2-fed-server-proxy.md)   
 [Перенос веб-агентов AD FS 1.1](migrate-the-ad-fs-web-agent.md)