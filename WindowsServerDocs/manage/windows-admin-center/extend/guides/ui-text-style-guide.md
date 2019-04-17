---
title: Руководство по стилю для текста и оформления пользовательского интерфейса Windows Admin Center
description: Пользовательского интерфейса Windows Admin Center текста и оформления SDK руководства по стилю
ms.technology: manage
ms.topic: article
author: jasongerend
ms.author: jgerend
ms.date: 10/17/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: ab5bee55975b803a77db0b6cdb179b76590e1d83
ms.sourcegitcommit: 56cccb09a35b2d3eef9056e2406c3a1762d28682
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/17/2018
ms.locfileid: "4739984"
---
# Руководство по стилю для текста и оформления пользовательского интерфейса Windows Admin Center

>Область применения: Windows Admin Center

В этом разделе описывается общий подход к созданию текста пользовательского интерфейса (UI) для Windows Admin Center, а также определенные условные обозначения и подходы, которые мы используем.

Windows Admin Center и все его расширения должны соблюдать [принципы стиля корпорации Майкрософт](https://docs.microsoft.com/style-guide/brand-voice-above-all-simple-human), чтобы обеспечить понятность и простоту использования. Это руководство по стилю основано на этих принципах стиля, а также [Руководстве по стилю письма Microsoft](https://docs.microsoft.com/style-guide/welcome/), поэтому обязательно используйте оба эти ресурса для получения информации о таких аспектах, как [специальные возможности](https://docs.microsoft.com/style-guide/accessibility/accessibility-guidelines-requirements), [сокращения](https://docs.microsoft.com/style-guide/acronyms), и [подборе словесных формулировок](https://docs.microsoft.com/style-guide/word-choice/), например [пожалуйста](https://docs.microsoft.com/style-guide/a-z-word-list-term-collections/p/please) и [к сожалению](https://docs.microsoft.com/style-guide/a-z-word-list-term-collections/s/sorry).

## Кнопки

- Кнопки должны по возможности содержать одно слово, особенно в том случае, если вы планируете локализовать свое средство. Два или три нормально, но постарайтесь не больше. Если у вас четыре слова или больше, было бы удобнее использовать элемент управления ссылку.
- Надписи на кнопках должен быть краткими, точными и понятными. Вместо универсальной кнопки «Отправить» используйте глагол, соответствующий действию пользователя, например «Создать», «Удалить», «Добавить», «Форматировать» и т. п.
- Если появляется после вопроса, ее надпись должна точно соответствовать вопросу (обычно «Да» или «Нет»).

## Прописные буквы

Мы придерживаемся стиля Microsoft в вопросах [написания прописными буквами](https://docs.microsoft.com/style-guide/capitalization), то есть используем прописные буквы, как в предложениях, практически повсеместно.

| Элемент пользовательского интерфейса              |Прописные буквы|Комментарии|
|-------------------------|--------------|--------|
|Значки (например, ПРЕДВАРИТЕЛЬНАЯ ВЕРСИЯ) |Все прописные      ||
|Все остальное          |Как в предложении|Тем не менее, существует несколько исключений, где мы получаем свойства объекта из WMI или PowerShell, и мы их не контролируем.|

## Двоеточия

Используйте двоеточия для внедрения списков. Пример.

    Choose one of the following:
    Cats
    Dogs
    Quokkas

Не используйте двоеточия в текста пользовательского интерфейса, когда метка включен другой строки из самое его метки или если существует четкое различие между меткой и самое Создание меток.

Используйте двоеточия в текста пользовательского интерфейса, когда метку в одной строке как текст статического и вам необходимо предотвратить вместе с двумя элементами.

## Сообщения о подтверждении

Диалоговые окна подтверждения полезны, когда у продолжение может быть непредсказуемым результатам, например потеря данных. Они должны содержать читаемым, полезные сведения очистить результатам, особенно для событий, которые нельзя отменить. 

- Убедитесь, что подтверждения не требуется. Если нет новые данные, чтобы предложить (например, «вы уверены?»), а затем подтверждение может не потребоваться.  
- Убедитесь, что клиент хочет перейти с действием.
- Убедитесь, что основная инструкция (заголовок) и текст (тела) не избыточными.
- В заголовке, определяете возможные результаты как вопрос или инструкции о том, что произойдет дальше. Например «удалить все данные на этом диске? или «Вы хотите стереть все данные».
- Добавление сведений в тексте. Если переменная, такие как имя элемента, который кажется вам об изменении, включайте его здесь.
- Включите простой вопрос (как в заголовке, так и в тексте), кадры Выбор между двумя кнопки действий.
- Для выбора сложных используйте Да/нет кнопок, которые побуждают внимательны чтения. Для выбора проще, используйте кнопки, которые относятся к действию, таких как удалить все или отменить.

## Первый запуск

При первом посещении страницы пользователями вы можете помочь им приступить к работе со средством. Это может быть:

- Текстовая строка на пустой странице с краткими инструкциями по началу работы, например «Выберите "Добавить", чтобы добавить приложение».
- Ссылка на элемент управления, который поможет пользователям начать работу, например «Добавьте приложение для начала работы».
- Короткий анимационный или видеоролик, демонстрирующий пользователю, как начать работу.

Вот несколько советов из нашего руководства по стилю Windows.

### 1. Приносить пользу

- Избегайте маркетингового стиля и языка.
- Когда вы что-то демонстрируете или предлагаете, конечный результат должен быть понятен. Если вы просто показываете пользователю, как что-то сделать, это не будет эффективно, если конечная цель действия не ясна.
- Не давайте советы, если они не нужны пользователю.

### 2. Показывать, а не рассказывать

Текст должен быть максимально простым (как в небольшой анимации или видеоролике).

### 3. Не перегружать

- Ограничьте использование всплывающих окон и советов четырьмя для каждого сеанса использования, включая системные сообщения и уведомления командной консоли.
- Следите за тем, чтобы всплывающие окна появлялись вовремя.
- Не мешайте пользователю.
- Всплывающие окна должно быть легко убрать.

### 4. Соответствовать контексту

- Обучающие элементы наиболее эффективны, когда отображаются в нужный момент.
- Если вы создаете учебник или слайд-шоу, информация должна быть конкретной.
- Не надо маркетинговой «воды» — сосредоточьтесь на конкретных советах и рекомендациях.
- Предоставьте пользователю возможность вернуться к учебнику позже, если это потребуется (мы часто не запоминаем информацию сразу, но инструкции по установке могут быть полезны только один раз).
- Показ сообщений на пустых страницах — это естественный подход для обучения и развлечения, и здесь важно обеспечить простоту и информативность.

### 5. Минимизировать сложность настройки

Если необходимо, чтобы пользователь выполнил еще одно действие для полноценного использования (войти в веб-сервис и т. п.), постарайтесь максимально облегчить эту задачу.

- Сообщения должны быть краткими и ясными.
- Постарайтесь удержать пользователя на месте. Если это достижимо, предоставьте возможность для подключения прямо отсюда.
- Если возможно, предложите сделать это позже, а затем напомните об этом.
- Если пользователь покидает какой-то процесс, предоставьте возможность быстро и легко переключиться обратно.

## Ссылки на файлы справки

Вот несколько советов из нашего руководства по стилю Windows.

### Когда следует предоставить ссылку справки?

Практически никогда не. Предоставить ссылку справки только тогда, когда:

- Существует очевидным и важные вопрос, клиенты, скорее всего, тогда как они в пользовательском Интерфейсе, ответ на который поможет им успешного выполнения на задачу пользовательского интерфейса. 
- Не хватает места в пользовательском Интерфейсе для обеспечения объем данных, необходимых для пользователей, чтобы добиться успеха задачу пользовательского интерфейса. 

### Где должен отображаться ссылки на справку? 

- Текст ссылки должно появиться стараться элемент пользовательского интерфейса, который справки предназначено для детей как можно скорее. 
- Если необходимо предоставить ссылку текста, которая применяется к весь экран пользовательского интерфейса, поместите его в левой нижней части экрана. 
- Если вы предоставляете ссылки с помощью кнопки справки (?), подсказка должна быть «Справка».

### Какой URL-адрес должен мы используем?

Никогда не создания прямой ссылки на веб-адрес — вместо этого использовать служба перенаправления.

Корпорация Майкрософт разработчики должны использовать FWLink за исключением когда это ссылка на справку, что пользователям может потребоваться вручную ввести, в этом случае используйте ссылку на aka.ms (поскольку целевой URL-адрес веб-сайта, который автоматически распознает языковой стандарт браузера, такие как Docs.microsoft.com)

### Рекомендации по текста 

- Используйте полные предложения.
- Не включайте завершающей пунктуации за исключением вопросительные знаки. 
- Вам не нужно использовать тот же текст в качестве заголовка задач; Используйте текст, который имеет смысл в контексте пользовательского интерфейса, но убедитесь, что существует логическое соединение между ними. Пример. 
- Ссылка на справку: опасности разрешения исключений? 
- Заголовок раздела справки: «Разрешение программе устанавливать связь через брандмауэр Windows»
- Внимательно максимально о содержимом раздела справки. 
    - Наши стиля
        - Как брандмауэр Windows помогает защитить компьютер?
        - Почему блики может улучшить изображение
    - Не наших стиля
        - Дополнительные сведения о брандмауэре Windows
        - Дополнительные сведения об управлении цветом
        - Дополнительные сведения
- Используйте целое предложение для текст ссылки, не только ключевых слов. 
    - Наши стиля 
        - [Что такое риск при создании исключений]()
    - Не наших стиля
        - Что такое [риск при создании исключений]() 

## Сообщения об ошибке

Вот некоторые советы, полученного из руководства по стилю Windows:

Создание хорошего сообщения — баланс между предоставить достаточно объяснение, но не слишком технические; между, несложных и personable, но не надоедают или оскорбительные.

### Общие рекомендации

Используйте одно сообщение в случае ошибки.

#### Заголовки

- Должно быть кратким и объясним кратко проблема либо **в идеале действия**. <br>Некоторые поверхностей интерфейса, возможно, заголовки, которые усекать вместо обтекания, когда они слишком много времени, поэтому будьте внимательны для этих.
- Используйте решение в заголовке, если это простой шаг.
- Убедитесь, что заголовок относятся непосредственно к кнопке на случай, если средство чтения игнорирует основной текст.
- Избегайте «Возникла проблема» в заголовках, если у вас нет выбором. Поддерживать более проблему.
- Избегайте использования переменных (например, имена файла, папки и приложения) в заголовках. Поместите их в тексте.

#### Body

- Если заголовок достаточно описание проблемы или решения, вам не нужны основной текст.
- Не повторяйте заголовок в сообщении в немного измененной формулировке.
- Четко и кратко что такое решение.
- Сосредоточьтесь на предоставление факты сначала.
- Не пользователей обвиняйте ошибки.
- Если код ошибки связанный с ошибкой и если вы считаете, что код ошибки в том числе может помочь клиента или службы поддержки Майкрософт для изучения проблемы, включают непосредственно под основной текст и записываете его следующим образом:

    Код ошибки: ###

    Если у клиента есть все сведения, необходимые для устранения ошибки без кода, не нужно включить его.

#### Кнопки

- Напишите текст на кнопке, чтобы он был определенных ответа на основную инструкцию. Если это невозможно, используйте «Закрыть» текста кнопки об увольнении (вместо «Пожалуйста» или «Готово»).
- Если у вас есть несколько кнопок, сделать левой кнопки действия пользователю рекомендуется выполнить. Сделать правой кнопки более консервативный действие, например «Отмена».

#### Ссылки на файлы справки

Рассмотрим только ссылки на файлы справки для сообщения об ошибках, которые не могут предоставить определенные и полезных.

## Текст состояния "null"

Вот некоторые справки из руководства по стилю Windows.

Значение NULL, состояние возникает, когда отсутствует данных клиентов или содержимое из приложения или компонента, когда результаты не возвращаются после поиска, или когда требуется данные отсутствуют формы, например сведения о транзакции выставления счетов.

### Требования

 - По возможности используйте ситуациях состояния "null" как возможность, чтобы рассказать пользователям о том, как использовать функцию (например, инструкции по добавлению музыка, где для поиска изображений и т. д.)  
- Если у вас есть заголовок в пользовательском Интерфейсе, объясняющие действие, выполняемое для «исправления» состояния "null" (например, «добавление некоторых музыка») 
- Наслаждайтесь исследованием с текстом. Это пространство можно предоставить удовольствие, так как она, скорее всего, не будут отображаться несколько раз. 
- Во избежание «Его — до сих здесь». Это sad и были чрезмерном. 
- Во избежание вопросы, например «Не подключались принтера?» Итак использовать один раз, но этот формат, как правило получить чрезмерном и вопросы включить дополнительную нагрузку/давление клиента. Можно также ощущение condescending. 
- Различные текстом состояния "null" очень хорошо. 

### Примеры:

- «Добавить пользователя в список избранного, и вы увидите их здесь».
- «Получено каких-либо достижений или игровые видеоролики, которые вы особенно достигнутым результатом? Добавьте их в вашем showcase.»
- «Никто элемента в стороны еще. Включите другой!»
- «Кто-либо добавляет как открывающий, вы увидите их здесь.»
- «При помещается как разблокировать достижения, запишите игровых клипов и добавить друзей, вы увидите его весь здесь.»
- «Друзей избранного будет отображаться здесь, чтобы вы могли видеть, когда они online и что они до.»

## Знаки препинания

- Завершающие знаки препинания (точки, вопросительные знаки) не используются в заголовках и неполных предложениях. Исключение — диалоговое окно подтверждения, где в заголовке задается вопрос
- Используйте рекомендации по стилю Microsoft в отношении [точек](https://docs.microsoft.com/style-guide/punctuation/periods) и [вопросительных знаков](https://docs.microsoft.com/style-guide/punctuation/question-marks).

## Сообщения о состоянии

Сообщения о состоянии состоят из всплывающих сообщений и уведомлений.

|Тип строки         | Примечания                               |
|------------        |-------------------------------------|
|Всплывающее уведомление               |С прописной буквы и с завершающей пунктуацией. В идеале — с переменной объекта, чтобы пользователи могли понять, к какому объекту относится сообщения, если они ушли от этого объекта|
|Заголовок уведомления|С прописной буквы без завершающей пунктуации (это заголовок). В идеале — с переменной объекта|
|Подробности уведомления|Полные предложения, в идеале — с ссылкой на раздел в пользовательском интерфейсе, где отображается объект|

Вот некоторые подробные рекомендации для сообщений с уведомлениями.

|Тип строки         | Примечания                               |
|------------        |-------------------------------------|
|Начинается             |Опускайте по возможности — обычно можно просто перейти к сообщению о ходе выполнения, чтобы как можно меньше отвлекать.|
|Выполняется         |Начните с описания выполняемого действия и закончите многоточием, чтобы показать незавершенность операции. Вот пример.<br> *Создание тома «Данные пользователя»...*|
|Выполнено             |Начните с наречия «Успешно» и закончите описанием только что завершенного действия. Вот пример.<br> *Успешно создан том «Данные пользователя».*|
|Сбой             |Начните с «Не удалось» и закончите описанием действия, которое программному обеспечению выполнить не удалось. Вот пример.<br> *Не удалось создать том «Данные пользователя».*|

## Подсказки

Хорошо подсказки кратко описываются элементы управления, без метки или предоставить некоторая дополнительная информация для элементов управления, отмеченные места, когда это полезно. Они могут также помогают навигации по пользовательскому Интерфейсу, предлагая дополнительные — Нет избыточности — сведения о меток элементов управления, значки, ссылки, и т. д.

Слишком часто или вообще не следует использовать всплывающие подсказки. Они могут быть прерывания для клиента, поэтому не включайте подсказку, просто состояний очевидным или повторяется метку. Всегда следует добавить ценные сведения.

|    Контекст                                 |    Как написать подсказки    |
|    -----------------------                 |    -------------------------    |
|Когда элемент управления или элементе пользовательского интерфейса без метки …|Используйте простую и описательное именной. Пример.<br> Выделение пера |
|Когда меткой элемента пользовательского интерфейса, но его предназначение ему уточнение …|<ul><li>Кратко опишите, что делать с этим элементом пользовательского интерфейса. </li><li>Используйте форму императивного команды. Например, «поиск текста в этот файл» (не «поиск текста в этом файле»).</li><li>Не включайте препинания только при наличии нескольких полных предложений.</li> </ul>|
|Если текстовая метка усеченная или скорее всего, усекать в некоторых языках …|<ul><li>Предоставить untruncated метки в подсказку.</li><li>Необязательно: На другую строку, описание упрощению, но только при необходимости.</li><li>Не предоставить подсказку, если untruncated информация предоставляется в другом месте на странице или в поток.</li></ul>|
|Если сочетание клавиш доступно …|<ul><li>Необязательно: Предоставляют сочетания клавиш в круглых скобках после метки или описательную фразу, например «Печать (Ctrl + P)» или «Поиск текста в этот файл (Ctrl + F)»</li><li>Это можно добавить полезные сочетания клавиш в подсказку упрощению, но не добавляйте подсказки только для отображения сочетания клавиш. </li></ul>|