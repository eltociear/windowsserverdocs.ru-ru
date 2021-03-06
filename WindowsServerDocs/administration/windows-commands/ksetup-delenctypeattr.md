---
title: ksetup деленктипеаттр
description: Справочный раздел по ksetup деленктипеаттр, который удаляет атрибут типа шифрования для домена.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4fc25ef3-e271-4229-a712-72c507df55aa
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b3076a25b619615402a599bd8aaa6ce9d10d4fe0
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/24/2020
ms.locfileid: "83817944"
---
# <a name="ksetup-delenctypeattr"></a>ksetup деленктипеаттр

Удаляет атрибут типа шифрования для домена. Сообщение о состоянии отображается при успешном или неудачном завершении.

Вы можете просмотреть тип шифрования для билета предоставления билета Kerberos (TGT) и ключ сеанса, выполнив команду **klist** и просмотрев выходные данные. Вы можете задать домен для подключения и использования, выполнив `ksetup /domain <domainname>` команду.

## <a name="syntax"></a>Синтаксис

```
ksetup /delenctypeattr <domainname>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| ----------| ----------- |
| `<domainname>` | Имя домена, для которого требуется установить соединение. Можно использовать либо полное доменное имя, либо простую форму имени, например corp.contoso.com или contoso. |

### <a name="examples"></a>Примеры

Чтобы определить текущие типы шифрования, установленные на этом компьютере, введите:

```
klist
```

Чтобы задать для домена значение mit.contoso.com, введите:

```
ksetup /domain mit.contoso.com
```

Чтобы проверить, какой тип шифрования имеет атрибут для домена, введите:

```
ksetup /getenctypeattr mit.contoso.com
```

Чтобы удалить атрибут SET ENCRYPTION Type для домена mit.contoso.com, введите:

```
ksetup /delenctypeattr mit.contoso.com
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда klist](klist.md)

- [Команда ksetup](ksetup.md)

- [Команда домена ksetup](ksetup-domain.md)

- [ksetup адденктипеаттр, команда](ksetup-addenctypeattr.md)

- [ksetup сетенктипеаттр, команда](ksetup-setenctypeattr.md)
