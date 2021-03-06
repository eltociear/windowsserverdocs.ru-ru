---
title: ksetup аддкпассвд
description: Справочный раздел по команде ksetup аддкпассвд, который добавляет адрес сервера пароля Kerberos (кпассвд) для области.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: d3196995-1b38-48ff-ba08-911cfab77317
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e0cff2f3d74e6d862bbdd000602a1d03312373d2
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/24/2020
ms.locfileid: "83818074"
---
# <a name="ksetup-addkpasswd"></a>ksetup аддкпассвд

Добавляет адрес сервера пароля Kerberos (кпассвд) для области.

## <a name="syntax"></a>Синтаксис

```
ksetup /addkpasswd <realmname> [<kpasswdname>]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| `<realmname>` | Указывает DNS-имя в верхнем регистре, например CORP. CONTOSO.COM и указывается в качестве области по умолчанию или **области =** при запуске **ksetup** . |
| `<kpasswdname>` | Указывает сервер паролей Kerberos. Оно называется без учета регистра, полное доменное имя, например mitkdc.contoso.com. Если имя KDC пропущено, для размещения Кдкс может использоваться DNS. |

#### <a name="remarks"></a>Замечания

- Если область Kerberos, в которой выполняется проверка подлинности на рабочей станции, поддерживает протокол Kerberos для изменения пароля, можно настроить клиентский компьютер под управлением операционной системы Windows для использования сервера паролей Kerberos.

- Можно добавить дополнительные имена KDC по одному.

### <a name="examples"></a>Примеры

Для настройки корпоративной сети. Чтобы использовать в качестве сервера паролей CONTOSO.COM-сервер, отличный от Windows KDC, введите:

```
ksetup /addkpasswd CORP.CONTOSO.COM mitkdc.contoso.com
```

Чтобы убедиться, что имя KDC задано, введите `ksetup` и просмотрите выходные данные, выполняя поиск текста **кпассвд =**. Если текст не отображается, это означает, что сопоставление не было настроено.

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда ksetup](ksetup.md)

- [ksetup делкпассвд, команда](ksetup-delkpasswd.md)
