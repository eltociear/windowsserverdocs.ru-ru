---
ms.assetid: a33bd54c-e6db-4b58-8264-c0f34bd8ba39
title: Пошаговое руководство. Workplace Join на устройство Android
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: a52c5b6e808094e1ef31c800e8a724dd0a37f3d3
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/08/2020
ms.locfileid: "80816087"
---
# <a name="walkthrough-workplace-join-to-an-android-device"></a>Пошаговое руководство. Workplace Join на устройство Android



## <a name="join-your-device-with-workplace-join"></a>Присоединение устройства с использованием функции присоединения к рабочему месту

> [!NOTE]
> Присоединение к рабочей области Android требует Регистрация устройств Azure Active Directory службы. Чтобы применить условные политики устройств локально, необходимо развернуть средство синхронизации каталогов (DirSync) с включенным параметром обратной записи объектов устройств. В настоящее время обратная запись устройства в Active Directory из Azure Active Directory может занять до 3 часов. Таким образом, пользователи должны подождать 3 часа, чтобы получить доступ к локальным веб-приложениям, после создания рабочей учетной записи. Дополнительные сведения о развертывании службы Регистрация устройств Azure Active Directory см. в разделе [Обзор службы регистрация устройств Azure Active Directory](https://msdn.microsoft.com/library/azure/dn788908.aspx) .

#### <a name="create-a-work-account-that-joins-your-device-with-workplace-join"></a>Создание рабочей учетной записи, которая присоединяет устройство к рабочей области

1.  Необходимо установить приложение Azure Authenticator на устройстве, чтобы создать рабочую учетную запись, которая присоединяет устройство к рабочей области. Следующий URL-адрес содержит инструкции по установке приложения Azure Authenticator на устройстве Android и добавлению рабочей учетной записи. Рабочая учетная запись превращает устройство Android в доверенное устройство и обеспечивает единый вход (SSO) для приложений на устройстве. Вы можете использовать доверенное устройство для доступа к веб-приложениям и современным бизнес-приложениям, как это рекомендовано ИТ-администратором. Дополнительные сведения см. в статье [Azure Authenticator для Android](https://docs.microsoft.com/azure/multi-factor-authentication/end-user/microsoft-authenticator-app-how-to).

## <a name="see-also"></a>См. также
[Присоединение к рабочему месту с любого устройства для единого входа и однофакторной проверки подлинности в приложениях компании](Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md)
[настройке локального условного доступа с помощью службы регистрация устройств Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-device-registration-on-premises-setup)


