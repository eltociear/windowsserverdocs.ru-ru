---
ms.assetid: 22347a94-aeea-44b4-85fb-af2c968f432a
title: Развертывание аудита безопасности при помощи централизованной политики аудита (поэтапная демонстрация)
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 9ad3f069eaea6917d29f56a00c6ecde035ecb01d
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/08/2020
ms.locfileid: "80861197"
---
# <a name="deploy-security-auditing-with-central-audit-policies-demonstration-steps"></a>Развертывание аудита безопасности при помощи централизованной политики аудита (поэтапная демонстрация)

>Область применения: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

В этом сценарии вы будете выполнять аудит доступа к файлам в папке «финансы» с помощью политики финансов, созданной в [статье &#40;&#41;развертывание централизованной политики доступа](Deploy-a-Central-Access-Policy--Demonstration-Steps-.md). При попытке неавторизованного пользователя получить доступ к упомянутой папке такая активность записывается в просмотре событий.   
 Для проверки данного сценария требуется выполнение следующих действий.  
  
|Задача|Описание|  
|--------|---------------|  
|[Настройка доступа к глобальным объектам](Deploy-Security-Auditing-with-Central-Audit-Policies--Demonstration-Steps-.md#BKMK_1)|На данном этапе выполняется настройка политики доступа к глобальным объектам на контроллере домена.|  
|[Обновление параметров групповая политика](Deploy-Security-Auditing-with-Central-Audit-Policies--Demonstration-Steps-.md#BKMK_2)|Войдите в файловый сервер и примените обновление групповой политики.|  
|[Проверка применения политики доступа к глобальным объектам](Deploy-Security-Auditing-with-Central-Audit-Policies--Demonstration-Steps-.md#BKMK_3)|Просмотрите соответствующие события в просмотре событий. События должны включать метаданные по стране и типу документа.|  
  
## <a name="configure-global-object-access-policy"></a><a name="BKMK_1"></a>Настройка политики доступа к глобальным объектам  
На данном этапе выполняется настройка политики доступа к глобальным объектам в контроллере домена.  
  
#### <a name="to-configure-a-global-object-access-policy"></a>Выполнение настройки политики доступа к глобальным объектам  
  
1. Войдите на контроллер домена DC1 как CONTOSO\Administrator с паролем <strong>pass@word1</strong>.  
  
2. В диспетчере серверов выберите **Средства**, затем нажмите **Управление групповой политикой**.  
  
3. В дереве консоли дважды щелкните **Домены**, дважды щелкните **contoso.com**, нажмите **Contoso**, а затем дважды щелкните **Файловые серверы**.  
  
4. Правой кнопкой мыши щелкните элемент **FlexibleAccessGPO**, затем нажмите **Изменить**.  
  
5. Дважды щелкните пункт **Конфигурация компьютера**, дважды щелкните пункт **Политики**, а затем дважды щелкните **Параметры Windows**.  
  
6. Дважды щелкните пункт **Параметры безопасности**, дважды щелкните пункт **Конфигурация расширенной политики аудита**, а затем дважды щелкните **Политики аудита**.  
  
7. Дважды щелкните пункты **Доступ к объектам**и **Аудит файловой системы**.  
  
8. Установите флажок **Настроить следующие события**, установите флажки **Успех** и **Отказ**, а затем нажмите кнопку **ОК**.  
  
9. В области навигации дважды щелкните **Аудит доступа к глобальным объектам**, затем дважды щелкните **Файловая система**.  
  
10. Установите флажок **Определить этот параметр политики** и нажмите кнопку **Настроить**.  
  
11. В поле **Дополнительные параметры безопасности глобального системного списка управления доступом к файлам** нажмите **Добавить**, затем нажмите **Выбрать субъект**, введите **Все**, а затем нажмите **ОК**.  
  
12. В поле **Запись аудита глобального системного списка управления доступом к файлам** выберите **Полный доступ** в поле **Разрешения**.  
  
13. В разделе **Добавить условие** нажмите **Добавить условие** и в раскрывающихся списках выберите   
    [**Ресурс**] [**Отдел**] [**Любой из**] [**Значение**] [**Финансы**].  
  
14. Трижды нажмите кнопку **ОК** для завершения конфигурации параметров политики аудита доступа к глобальным объектам.  
  
15. В области навигации щелкните **Доступ к объектам**, а в области результатов дважды щелкните **Аудит работы с дескрипторами**. Нажмите **Настроить следующие события аудита**, **Успех**и **Отказ**, нажмите кнопку **ОК**, затем закройте объект групповой политики гибкого доступа.  
  
## <a name="update-group-policy-settings"></a><a name="BKMK_2"></a>Обновление параметров групповая политика  
На данном этапе выполняется обновление параметров групповой политики после создания политики аудита.  
  
#### <a name="to-update-group-policy-settings"></a>Обновление параметров групповой политики  
  
1. Войдите на файловый сервер, FILE1 как contoso\Administrator, с паролем <strong>pass@word1</strong>.  
  
2. Нажмите клавишу Windows+R, затем введите **cmd** для открытия окна командной строки.  
  
   > [!NOTE]  
   > Если появится диалог **Контроль учетных записей**, подтвердите, что действие, которое оно отображает то, что нужно, затем щелкните **Да**.  
  
3. Введите **gpupdate /force** и нажмите клавишу ВВОД.  
  
## <a name="verify-that-the-global-object-access-policy-has-been-applied"></a><a name="BKMK_3"></a>Проверка применения политики доступа к глобальным объектам  
После того как параметры групповой политики будут применены, можно проверить, правильно ли были применены параметры политики аудита.  
  
#### <a name="to-verify-that-the-global-object-access-policy-has-been-applied"></a>Проверка применения политики доступа к глобальным объектам  
  
1.  Войдите в клиентский компьютер CLIENT1 с учетной записью Contoso\MReid. Перейдите к ГИПЕРССЫЛКе на папку "file:///\\\\\\\ ID_AD_FILE1\\\Финанце" \\\ FILE1\Finance Documents и измените Word Document 2.  
  
2.  Войдите в файловый сервер FILE1 с учетной записью contoso\administrator. Откройте просмотр событий, перейдите в раздел **Журналы Windows**, выберите **Безопасность** и подтвердите, что ваши действия привели к событиям аудита **4656** и **4663** (даже несмотря на то, что вы не задавали конкретных системных списков управления доступом для аудита файлов или папок, созданных, измененных или удаленных вами).  
  
> [!IMPORTANT]  
> Новое событие входа создается на том компьютере, где размещается ресурс, от лица того пользователя, для которого производится проверка действующих прав доступа. При анализе журналов аудита безопасности на предмет выявления активности пользователя по входу в систему включается информация уровня олицетворения с целью различения событий входа, созданных ввиду действующих прав доступа, и событий входа, созданных вследствие входа текущего пользователя сети. В случае создания события входа ввиду действующих прав доступа уровень олицетворения будет "Удостоверение". Вход текущего пользователя сети обычно приводит к созданию события входа с уровнем олицетворения "Олицетворение" или "Делегирование".  
  
## <a name="see-also"></a><a name="BKMK_Links"></a> См. также  
  
-   [Сценарий: аудит доступа к файлам](Scenario--File-Access-Auditing.md)  
  
-   [Планирование для аудита доступа к файлам](Plan-for-File-Access-Auditing.md)  
  
-   [Динамический контроль доступа: обзор сценария](Dynamic-Access-Control--Scenario-Overview.md)  
  

