---
title: Настройка отчетов хранилища
description: В этой статье описывается процесс настройки параметров по умолчанию для отчетов хранилища
ms.date: 7/7/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: f62109a8d3ea3e4e6386956789d276f9aa911e80
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2019
ms.locfileid: "59885235"
---
# <a name="configure-storage-reports"></a>Настройка отчетов хранилища

> Относится к: Windows Server (полугодовой канал), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

Для отчетов хранилища можно настраивать параметры по умолчанию. Эти параметры по умолчанию используются отчетами об инцидентах, которые создаются при возникновении события квоты или события фильтра блокировки файлов. Они также используются для отчетов по расписанию и по требованию, и при определении конкретных свойств этих отчетов параметры по умолчанию можно переопределить.

> [!Important]
> При изменении параметров по умолчанию для типа отчета изменения распространяются на все отчеты об инцидентах и любые существующие запланированные задачи отчетов, использующие эти параметры по умолчанию.

## <a name="to-configure-the-default-parameters-for-storage-reports"></a>Настройка параметров по умолчанию для отчетов хранилища

1. В древе консоли выберите **Диспетчер ресурсов файлового сервера** и выберите команду **Настроить параметры**. Откроется диалоговое окно **Параметры диспетчера ресурсов файлового сервера** .

2. На вкладке **Отчеты хранилища** в разделе **Настройка параметры по умолчанию** выберите тип отчета, который требуется изменить.

3. Щелкните **Изменить параметры**.

4. В зависимости от выбранного типа отчета для редактирования будут доступны разные параметры отчета. Выполните все необходимые изменения и нажмите кнопку **ОК**, чтобы сохранить их в качестве параметров по умолчанию для выбранного типа отчета.

5.  Для всех редактируемых типов отчетов повторите шаги со 2 по 4.

6. Чтобы просмотреть список параметров по умолчанию для всех отчетов, нажмите **Просмотреть отчеты**. Затем нажмите кнопку **Закрыть**.

7.  Нажмите кнопку **ОК**.

## <a name="see-also"></a>См. также

-   [Параметры диспетчера ресурсов файлового сервера в параметр](setting-file-server-resource-manager-options.md)
-   [Управление ресурсами хранилища](storage-reports-management.md)