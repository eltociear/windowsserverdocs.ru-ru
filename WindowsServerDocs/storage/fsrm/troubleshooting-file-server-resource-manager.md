---
title: "Устранение неполадок в диспетчере ресурсов файлового сервера"
description: "В этой статье описывается, как устранять распространенные проблемы при использовании диспетчера ресурсов файлового сервера"
ms.date: 7/7/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 923710fac426f63d2c38d9b9a68c92427783abb1
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/17/2017
---
# <a name="troubleshooting-file-server-resource-manager"></a>Устранение неполадок в диспетчере ресурсов файлового сервера

> Область применения: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

В данном разделе перечислены распространенные проблемы, которые могут возникнуть при использовании диспетчера ресурсов файлового сервера.

> [!Note]
> Хорошим способом устранения неполадок является использование журналов событий, которые были созданы диспетчером ресурсов файлового сервера. Все записи журнала событий для диспетчера ресурсов файлового сервера можно найти в журнале событий **Приложения** источника **SRMSVC**

## <a name="i-am-not-receiving-e-mail-notifications"></a>Не приходят уведомления по электронной почте.

-   **Причина**: параметры электронной почты не были настроены или были настроены неправильно.

-   **Решение**: на вкладке **Уведомления по электронной почте** в диалоговом окне **Параметры диспетчера ресурсов файлового сервера** проверьте, что SMTP-сервер и получатели электронной почты по умолчанию были указаны и являются допустимыми. Отправьте проверочное сообщение электронной почты, чтобы удостовериться в правильности сведений и проверить корректность работы SMTP-сервера, который используется для отправки уведомлений. Дополнительные сведения см. в разделе [Настройка уведомлений, отправляемых по электронной почте](configure-email-notifications.md).


## <a name="i-am-only-receiving-one-e-mail-notification-even-though-the-event-that-triggered-that-notification-happened-several-times-in-a-row"></a>Приходит только одно уведомление по электронной почте, даже если событие, вызвавшее оповещение, произошло несколько раз подряд.

-   **Причина**: когда пользователь пытается несколько раз сохранить заблокированный файл или файл, который превышает пороговое значение квоты, и для фильтра блокировки файлов или события квоты настроено уведомление по электронной почте, по умолчанию администратору отправляется только одно сообщение электронной почты в течение 60 минут. Это помогает предотвратить переполнение учетной записи электронной почты администратора сообщениями.

-   **Решение**: на вкладке **Пределы уведомлений** в диалоговом окне **Параметры диспетчера ресурсов файлового сервера** можно задать ограничение по времени для каждого типа уведомлений: электронная почта, журнал событий, команды и отчеты. Каждое ограничение определяет период времени, который должен пройти, прежде чем для одной и той же проблемы будет сформировано еще одно уведомление того же типа. Дополнительные сведения см. в разделе [Настройка пределов уведомлений](configure-notification-limits.md).


## <a name="my-storage-reports-keep-failing-and-little-or-no-information-is-available-in-the-event-log-regarding-the-source-of-the-failure"></a>Отчеты хранилища формируются со сбоем и в журнале событий содержится мало информации (или она отсутствует) относительно причины сбоя.

-   **Причина**: том, где сохраняются отчеты, может быть поврежден.
-   **Решение**: запустите **chkdsk** на этом томе и попробуйте повторно создать отчеты.

## <a name="my-file-screening-audit-reports-do-not-contain-any-information"></a>В отчетах аудита фильтра блокировки файлов отсутствуют данные.

-   **Причина**: может быть одна или несколько следующих причин.
    -   База данных аудита не настроена для записи действий фильтра блокировки файлов.
    -   База данных аудита пуста (то есть отсутствуют действия фильтра блокировки файлов, которые можно записать).
    -   Параметры отчета аудита фильтра блокировки файлов не выбирают данные из базы данных аудита.
    
-   **Решение**: на вкладке **Аудит фильтра блокировки файлов** в диалоговом окне **Параметры диспетчера ресурсов файлового сервера** проверьте, что установлен флажок **Записывать действия фильтра блокировки файлов в базе данных аудита**.
    -   Дополнительные сведения о записи действий фильтра блокировки файлов см. в разделе [Настройка аудита фильтра блокировки файлов](configure-file-screen-audit.md).
    -   Чтобы настроить параметры по умолчанию для отчета аудита фильтра блокировки файлов, см. раздел [Настройка отчетов хранилища](configure-storage-reports.md).
    -   Чтобы изменить параметры отчета для запланированных задач отчета или отчетов по требованию, см. раздел [Управление отчетами хранилища](storage-reports-management.md).

## <a name="the-used-and-available-values-for-some-of-the-quotas-i-have-created-do-not-correspond-to-the-actual-limit-setting"></a>Значения "Используется" и "Доступно" для некоторых созданных квот не соответствуют фактическому значению параметра "Предел".

-   **Причина**: имеется вложенная квота; в этом случае квота вложенной папки является производным более строгого ограничения квоты родительской папки. Например, предельная квота, составляющая 100 мегабайт (МБ), может применяться к родительской папке, а квота в 200 МБ— применяться отдельно к каждой из ее вложенных папок. Если в родительской папке хранится 50 МБ данных (сумма данных, хранящихся в ее вложенных папках), для каждой вложенной папки будет доступно только 50 МБ свободного пространства.

-   **Решение**: в разделе **Управление квотами** нажмите кнопку **Квоты**. На панели **Результаты** выберите запись квоты, для которой выполняется устранение неполадки. На панели **Действия** щелкните **Просмотреть квоты, влияющие на папку**и найдите квоты, которые применяются к родительским папкам. Это позволит определить, предел хранилища каких квот родительских папок ниже значения выбранной квоты.
