---
title: Практический пример пакета SDK Windows Admin Center — чисто хранилища
description: Практический пример пакета SDK Windows Admin Center — чисто хранилища
ms.technology: extend
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 1/7/2019
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 25018474fd22d05804ecc7faafbd633fbb4db269
ms.sourcegitcommit: ebeec824f802f020d0ece17524ba43b1baeba893
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/08/2019
ms.locfileid: "8995370"
---
# Расширение чисто хранилища

## Обеспечивает управление начала до конца массива для Windows Admin Center 

[Чисто хранилища](https://www.purestorage.com/) содержит корпоративных решений хранения данных только с флэш накопителями, которые предоставляют на основе данных архитектуры для ускорения вашего бизнеса для конкурентное преимущество.  Pure является партнера Майкрософт уровня Gold, сертифицированных для Microsoft Windows Server и разрабатывает техническую интеграции для ключа решений Майкрософт, например Azure, Hyper-V, SQL Server, System Center, Windows PowerShell и Windows SMB. Pure недавно объявили Предварительный просмотр Технический расширения, поддерживающий самые последние версии Windows Admin Center, который обеспечивает представление одной области в чистом FlashArray продукты.  Из этого расширения пользователи получат дополнительные из одного средства для проведения задачи наблюдения, просматривать метрик производительности в режиме реального времени и управление томов и владельцы.

На раннем этапе когда Windows Admin Center была известна как «Project Honolulu», Pure видели значение не сможет обеспечить для клиентов и партнерам позволяет управлять несколькими чисто FlashArrays хранилища в одной области стекло, предоставляющий Windows Admin Center.

При запуске Pure исследование вариант использования с «Project Honolulu» они сразу поняли, предоставляя возможности централизованного управления между Windows Admin Center и FlashArray возможной. Pure тесно работали с помощью команды разработчиков Windows Admin Center, который помог определять подробности реализации функций. Pure также была возможность оставлять отзывы на начальных этапах Windows Admin Center и материалы для разработчиков Майкрософт. 

![Расширение чисто хранилища](../../media/extend-case-study-purestorage/purestorage-1.png)

> <cite>«Мы встроили набор компонентов, которая имитирует наших FlashArray веб-интерфейс для включения прямого управления из в Windows Admin Center. Клиентам и партнерам преимущества унифицированного и необходимости работать с помощью двух разных средствами. В дополнение к одной точки управления преимущества клиенты не смогут контекстно управление серверами Windows, подключенных к FlashArray.»</cite>
>
> --Barkz, техническим директором решения корпорации Майкрософт и интеграции, чисто хранилища

Функции, которые включены в чистом расширения решения хранилища:
- Подключение к нескольким FlashArrays.
- Просмотр подробных сведений о FlashArray, в том числе операций ввода-вывода, пропускной способности, задержка, зоны данных и Управление пространством. Ниже перечислены все и те же сведения, которые вы получаете от графический Интерфейс управления FlashArray.
- Просмотрите настроенное узла группы, которые используются для включения доступа к общего тома для Windows Server узлы и кластеры Общие тома (CSV).
- Узлы представление — Все информацией о подключениях доступна в том числе имена узлов, iSCSI полное имя (IQNs) и имена (WWNs).
- Управление тома — Это включает в себя право на создание и уничтожение тома. После уничтожения тома он будет находиться в сегменте уничтожен элементов и вам потребуется Eradicate от основного графического интерфейса пользователя FlashArray управления.
- Управление владельцы — Это один из наиболее интересных возможностей предоставить контекст для отдельных серверов, будет осуществлять развертывание Windows Admin Center. Вы можете просмотреть подключенные диски (тома) отдельных серверов Windows, установите флажок, если путей IO (MPIO) установлен и настроен и создание и установка новых томов.

Для [демонстрации видео](https://youtu.be/IFAeCAd6V2g) будет создан, отображаются все сообщения о возможности, которые обеспечивает чисто расширения решения хранилища. 

Ниже снимке экрана показано просмотра, какие диски (тома) подключены к определенной узле Windows Server. Помимо просмотра сведений о подключении, мы проверяем, если настроено путей-операций ввода-ВЫВОДА.

![Расширение чисто хранилища](../../media/extend-case-study-purestorage/purestorage-2.png)

Помимо просмотра диски, создать новые тома и немедленно подключаются к узлу без необходимости использовать средство управления дисками Windows.

![Расширение чисто хранилища](../../media/extend-case-study-purestorage/purestorage-3.png)

Начиная с отпуская наших Technical Preview, отзывы пользователей, собранные в данный момент очень положительные и также предоставляет нам понять различные возможности для добавления в будущих выпусках. 

Дополнительные ресурсы:
- [Чисто хранилища расширения объявление в блоге](https://blog.purestorage.com/tech-preview-of-the-pure-storage-extension-for-windows-admin-center/)
- [PureReport](https://itunes.apple.com/us/podcast/windows-admin-center-extension-from-pure-storage/id1392639991?i=1000424316130&mt=2) подкастов