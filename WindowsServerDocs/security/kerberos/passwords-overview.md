---
title: Общие сведения о паролях
description: Безопасность Windows Server
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-kerberos
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f608960e-2039-4c91-9c8c-9b81053c675e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 6c1b8d56b5c0da738e7dae5c0072be81040f90d8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2019
ms.locfileid: "59869605"
---
# <a name="passwords-overview"></a>Общие сведения о паролях

>Область применения. Windows Server (полугодовой канал), Windows Server 2016

В этом разделе для ИТ-специалистов описываются пароли, используемые в операционных системах Windows и ссылки на документацию и обсуждения использование паролей в стратегию управления учетными данными.

## <a name="BKMK_OVER"></a>Описание компонента
Проектирования архитектуры операционных систем и приложений в настоящее время связанных с паролями и даже при использовании смарт-карт или биометрические системы, все учетные записи по-прежнему использовать пароли, и они по-прежнему используется в некоторых случаях. Некоторые учетные записи, в частности учетные записи, используемые для запуска служб, даже не может использовать смарт-карт и биометрических маркеры и поэтому необходимо использовать пароль для проверки подлинности. Windows обеспечивает защиту с помощью криптографических хэшей паролей.

Дополнительные сведения о паролях Windows см. в разделе [Технический обзор паролей](https://technet.microsoft.com/library/hh994558(WS.10).aspx).

## <a name="BKMK_APP"></a>Практическое применение
В Windows и многих других операционных систем наиболее распространенный метод проверки подлинности удостоверения пользователя является использование секретной парольной фразы или пароля. Обеспечение безопасности среды сети требует использования надежных паролей всеми пользователями. Это позволяет избежать угрозы злоумышленников, подбирающих ненадежный пароль через методы вручную или с помощью средств, чтобы получать учетные данные учетной записи скомпрометированных. Это особенно верно для административных учетных записей. Когда регулярно менять сложный пароль, уменьшается вероятность атак пароль ущерба для этой учетной записи.

## <a name="BKMK_NEW"></a>Новые и измененные функции
В Windows Server 2012 и Windows 8 появились графических паролей. Графические пароли представляют собой сочетание к выбранному изображению пользователя, в сочетании с ряда жестов. Рисунок пароль функция отключена в домене\-компьютеров, присоединенных к. Ссылки на дополнительные сведения о графических паролей, перечислены в [см. также](#BKMK_LINKS) ниже.

Функции ввода пароля в Windows Server 2012 и Windows 8 не изменились. Новые параметры групповой политики не были добавлены. Тем не менее, улучшения были внесены в учетных данных \(и пароль\) управления, такие как с помощью графических паролей, хранилище учетных данных и повторный вход в Windows 8 с учетной записью Майкрософт, которая ранее называлась Windows Live ID .

## <a name="BKMK_DEP"></a>Нерекомендуемые функции
Никакая функциональность пароль является устаревшим в Windows Server 2012 и Windows 8.

## <a name="BKMK_SOFT"></a>Требования к программному обеспечению
В корпоративных средах пароли обычно осуществляется с помощью доменных служб Active Directory. Пароли можно также управлять на локальном компьютере, используя параметры в локальной политике паролей параметры безопасности, политики учетных записей.

## <a name="BKMK_LINKS"></a>См. также
В этой таблице перечислены дополнительные ресурсы для функций пароль, технологии и управления учетными данными.

|Тип содержимого|Ссылок|
|--------|-------|
|**Документация по сценариям**|[Защита цифрового удостоверения](http://blogs.msdn.com/b/b8/archive/2011/12/14/protecting-your-digital-identity.aspx)|
|**Операции**|[Пользователи и компьютеры Active Directory](https://technet.microsoft.com/library/cc754217.aspx)|
|**Устранение неполадок**|[Узнайте, когда истекает срок действия пароля \- блоге PowerShell Active Directory](http://blogs.msdn.com/b/adpowershell/archive/2010/08/09/9970198.aspx)|
|**безопасность**| Windows Server 2008 R2 и Windows 7 [угрозы и меры противодействия: Политики учетных записей](https://technet.microsoft.com/library/hh125920(v=ws.10).aspx)<br /><br />Рекомендации, которые [изменять и создавать надежные пароли](https://www.microsoft.com/security/online-privacy/passwords-create.aspx)|
|**Средства и параметры**|[Справочник по параметрам групповой политики для Windows и Windows Server в центре загрузки Майкрософт](https://www.microsoft.com/download/en/details.aspx?amp;displaylang=en&displaylang=en&id=25250)|
|**Ресурсы сообщества**|[Защита цифрового удостоверения](http://blogs.msdn.com/b/b8/archive/2011/12/14/protecting-your-digital-identity.aspx)<br /><br />[Вход в Windows 8 с помощью идентификатора Windows Live ID](http://blogs.msdn.com/b/b8/archive/2011/09/26/signing-in-to-windows-8-with-a-windows-live-id.aspx)<br /><br />[Вход с помощью графического пароля](http://blogs.msdn.com/b/b8/archive/2011/12/16/signing-in-with-a-picture-password.aspx)<br /><br />[Оптимизация безопасности пароль рисунка](http://blogs.msdn.com/b/b8/archive/2011/12/19/optimizing-picture-password-security.aspx)|

