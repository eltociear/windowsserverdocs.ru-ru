---
title: nslookup ls
description: 'Раздел Windows команды для ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f15f06fe-67e7-41a9-93b5-192ab14ab380
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6a11867ff2ec69b1ef938149ac485ff8827b58de
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/31/2019
ms.locfileid: "66436920"
---
# <a name="nslookup-ls"></a>nslookup ls

>Область применения. Windows Server (полугодовой канал), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Выводит сведения для домена доменных имен (DNS).
## <a name="syntax"></a>Синтаксис
```
ls [<Option>] <DNSDomain> [{[>] <FileName>|[>>] <FileName>}]
```
## <a name="parameters"></a>Параметры

|    Параметр    |                                                                                                                                                                                                                                                                                                               Описание                                                                                                                                                                                                                                                                                                                |
|-----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    <Option>     | В следующей таблице перечислены допустимые значения.<br /><br />--t: список всех записей указанного типа. Описание <querytype>, см. в разделе **setquerytype** в дополнительные ссылки.<br />--a: выводит псевдонимы компьютеров в домене DNS. Этот параметр является синонимом **- t CNAME**<br />--d: список всех записей для домена DNS. Этот параметр является синонимом **- t ANY**<br />--h: выводит сведения о DNS-домена ЦП и операционной системы. Этот параметр является синонимом **- t HINFO**<br />--s: выводит список хорошо известных служб в домене DNS. Этот параметр является синонимом **-t WKS**. |
|   <DNSDomain>   |                                                                                                                                                                                                                                                                                         Задает имя домена DNS, для которого требуется получить сведения.                                                                                                                                                                                                                                                                                         |
|   <FileName>    |                                                                                                                                                                                                                                 Задает имя файла, в котором следует сохранить выходные данные. Можно использовать больше (>) и двойные больше (>>) символы для перенаправления выходных данных обычным способом.                                                                                                                                                                                                                                  |
| {help &#124; ?} |                                                                                                                                                                                                                                                                                          Отображает краткое описание **nslookup** подкоманды.                                                                                                                                                                                                                                                                                           |

## <a name="remarks"></a>Примечания
- По умолчанию выходные данные содержат имена компьютеров и их IP-адреса. Если выходные данные направляются в файл, хэш-символы выводятся каждых 50 записей, полученных с сервера
  ## <a name="additional-references"></a>Дополнительные ссылки
  [Ключ синтаксиса команд](command-line-syntax-key.md)
  [nslookup задать querytype](nslookup-set-querytype.md)