---
title: Запуск сборщика журналов в Windows Server Essentials
description: Описание использования Windows Server Essentials
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: 0d340223-fa24-4c75-ba8e-b654feb120ab
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 6aac2ed382321349d39874c7db7617f6da845919
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/08/2020
ms.locfileid: "80852277"
---
# <a name="run-the-windows-server-essentials-log-collector"></a>Запуск сборщика журналов в Windows Server Essentials
Сборщик журналов Windows Server Essentials можно запустить с сервера или компьютера в сети. При запуске сборщика журналов на сервере можно будет собирать журналы только с сервера. При запуске сборщика журналов на сетевом компьютере можно собирать журналы с сервера, а также журналов с этого компьютера.  
  
 Для запуска сборщика журналов необходимо иметь соответствующие права администратора. При сборе файлов журнала для сервера необходимо быть администратором сервера. При сборе файлов журнала на компьютере необходимо быть администратором клиентов для этого компьютера.  
  
#### <a name="to-run-the-log-collector-on-the-server-by-using-the-wizard"></a>Запуск сборщика журналов на сервере с помощью мастера  
  
1. На **начальной** странице сервера щелкните **сборщик журналов Windows Server Essentials**.  
  
   > [!NOTE]
   > - Если программа сборщика данных журнала не отображается на **начальной** странице, перейдите к **%систем%\програм Files (x86) \Windows Server Essentials log сборщика**, а затем дважды щелкните **LogCollector**.  
   >   -   Если вы вошли на сервер без прав администратора, сборщик журналов предложит ввести учетные данные.  
  
2. При появлении запроса на сохранение собранных файлов журнала можно выбрать расположение по умолчанию, **\\\\< ServerName\>\Logs**или указать другое расположение. Чтобы принять расположение по умолчанию, щелкните **Далее**. Чтобы изменить расположение, нажмите кнопку **Обзор**, перейдите в папку, в которую необходимо сохранить файлы журнала, а затем нажмите кнопку **Сохранить**.  
  
   > [!NOTE]
   >  Для файлов журнала имена файлов указывать не надо. Сборщик журнала присваивает имя коллекции ZIP-файлов путем сцепления имени компьютера и метки времени файла.  
  
3. Во время сбора журналов отображается индикатор хода выполнения.  
  
4. Для просмотра содержимого файла коллекции журналов установите флажок **Открыть расположение файла, где сохранены журналы** и щелкните **Закрыть**, чтобы закрыть мастер и открыть файл коллекции журналов.  
  
#### <a name="to-run-the-log-collector-on-a-network-computer-by-using-the-wizard"></a>Запуск сборщика журналов на сетевом компьютере с помощью мастера  
  
1.  Перейдите к **%систем%\програм Files (x86) \Windows Server Essentials log**, а затем дважды щелкните файл **LogCollector. exe**.  
  
    > [!NOTE]
    >  Если вы вошли на компьютер сети без прав администратора, введите имя пользователя и пароль при появлении соответствующего запроса, а затем нажмите кнопку **Далее**.  
  
2.  Выберите журналы, которые необходимо собрать, следующим образом:  
  
    1.  Установите флажок **Файлы журнала сервера**, чтобы собрать файлы журнала на сервере.  
  
    2.  Флажок **Файлы журнала клиентского компьютера (этот компьютер)** устанавливается по умолчанию, указывая на то, что сборщик журналов будет собирать журналы из сетевого компьютера, на котором он выполняется. Если требуется собирать журналы сервера, снимите флажок **Файлы журнала клиентского компьютера (этот компьютер)** .  
  
    3.  Нажмите кнопку **Далее**.  
  
3.  При появлении соответствующего запроса введите имя пользователя и пароль для администратора сервера, а затем нажмите кнопку **Далее**.  
  
4.  Введите или выберите путь к расположению, где вы хотите сохранить файлы журнала, и нажмите кнопку **Далее**.  
  
    > [!NOTE]
    >  Для файлов журнала имена файлов указывать не надо. Сборщик журнала присваивает имя коллекции ZIP-файлов путем сцепления имени компьютера и метки времени файла.  
  
5.  Во время сбора журналов отображается индикатор хода выполнения.  
  
6.  Для просмотра содержимого файла коллекции журналов установите флажок **Открыть расположение файла, где сохранены журналы** и щелкните **Закрыть**, чтобы закрыть мастер и открыть файл коллекции журналов.  
  
### <a name="running-the-log-collector-manually"></a>Запуск сборщика журналов вручную  
 После установки сборщика журналов создается запланированное задание, позволяющее запускать данный инструмент. Впоследствии при возникновении проблем с запуском мастера для запуска сборщика журналов можно будет использовать **Диспетчер запланированных задач** (без применения мастера).  
  
##### <a name="to-manually-run-the-log-collector-on-the-server"></a>Запуск сборщика журналов на сервере вручную  
  
1.  Войдите на сервер напрямую или удаленно.  
  
2.  Откройте **Планировщик задач**.  
  
3.  В корне **Библиотеки планировщика задач** найдите запланированную задачу с именем **LogCollector**.  
  
4.  Щелкните правой кнопкой мыши **LogCollector**, а затем нажмите кнопку **Выполнить**. Сборщик журналов помещает журналы в папку по умолчанию на сервере **\\\\< ServerName\>\Logs**. Если у вас нет разрешения на запись в папку или папка не существует, журналы помещаются в подкаталог **< temp\>** .  
  
##### <a name="to-manually-run-the-log-collector-on-a-network-computer"></a>Запуск сборщика журналов на сетевом компьютере вручную  
  
1.  Войдите на сетевой компьютер напрямую или удаленно.  
  
2.  Откройте **Планировщик задач**.  
  
3.  В корне **Библиотеки планировщика задач** найдите запланированную задачу с именем **LogCollector**.  
  
4.  Щелкните правой кнопкой мыши **LogCollector**, а затем нажмите кнопку **Выполнить**. Сборщик данных журнала помещает журналы в папку **< temp\>** на сетевом компьютере.
