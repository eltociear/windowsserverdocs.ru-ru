---
title: Защищенной структуры и экранированной виртуальной Машины, руководство для поставщиков услуг размещения
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: 392af37f-a02d-4d40-a25d-384211cbbfdd
manager: dongill
author: nirb-ms
ms.technology: security-guarded-fabric
ms.openlocfilehash: 0a43cedf8ce0138e89624ff3df5bc7088f583252
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2019
ms.locfileid: "59875305"
---
# <a name="guarded-fabric-and-shielded-vm-planning-guide-for-tenants"></a>Защищенной структуры и экранированной виртуальной Машины, руководство для клиентов

>Относится к: Windows Server 2019 г., Windows Server (полугодовой канал), Windows Server 2016

Этот раздел посвящен Владельцы виртуальных Машин, которые хотят защитить свои виртуальные машины (ВМ) для соответствия и безопасности. Независимо от ли виртуальные машины на поставщика услуг размещения защищенной структуры или частного защищенной структуре Владельцы виртуальных Машин нужно управлять уровнем безопасности их экранированные виртуальные машины, включая обслуживание сможет расшифровывать их при необходимости.

Существует три области, которые следует учитывать при с помощью экранированных виртуальных машин:

- Уровень безопасности для виртуальных машин
- Криптографические ключи, используемые для их защиты
- Данные экранирования — конфиденциальные сведения, используемые для создания экранированных виртуальных машин 

## <a name="security-level-for-the-vms"></a>Уровень безопасности для виртуальных машин

Если развертывание экранированных виртуальных машин, должен быть выбран один из двух уровней безопасности:

- Экранированный 
- С поддержкой шифрования

Оба экранированных и виртуальные машины с поддержкой шифрования имеют виртуальный доверенный платформенный модуль, подключенные к их и их защиту выполнения Windows с помощью BitLocker. Основное различие —, экранированных виртуальных машин блок доступа администраторов fabric пока виртуальные машины с поддержкой шифрования Разрешить администраторам структуры тот же уровень доступа как им нужно регулярных виртуальной Машины. Дополнительные сведения об этих различиях см. в разделе [защищенных структуры и экранированных виртуальных машин Обзор](guarded-fabric-and-shielded-vms.md). 

Выберите **экранированных виртуальных машин** Если вам нужно защитить виртуальную Машину от скомпрометированной структуры (включая скомпрометированных администраторов). Они должны использоваться в средах, где администраторы структуры и структуры, сам не доверенный. Выберите **шифрование виртуальных машин, поддерживаемых** Если вам нужны в соответствии с полосу соответствия, которые могут потребовать шифрование данных при хранении и шифрование виртуальной машины по сети (например, во время динамической миграции).

Виртуальные машины с поддержкой шифрования подходят в средах, где администраторы пользуются полным доверием, но шифрования актуально.

Сочетание обычными виртуальными машинами, экранированные виртуальные машины и виртуальные машины с поддержкой шифрования можно запустить на защищенной структуры и даже на том же узле Hyper-V. 

Экранированный или поддержкой шифрования виртуальной Машины определяется данные экранирования, который выбирается при создании виртуальной Машины. Владельцы виртуальных Машин Настройка уровня безопасности во время создания данных экранирования (см. в разделе [данные экранирования](#shielding-data) раздел).
Обратите внимание на то, что как только этот выбор будет сделан, его нельзя изменить пока виртуальная машина находится в структуре виртуализации.

## <a name="cryptographic-keys-used-for-shielded-vms"></a>Криптографические ключи, используемые для экранированных виртуальных машин

Экранированные виртуальные машины защищены от виртуализации fabric атак с помощью зашифрованных дисков и различных других зашифрованных элементов которых могут быть расшифрованы только субъектом:

- Ключ "Владелец" — это криптографический ключ, который обслуживается владелец виртуальной Машины, который обычно используется для восстановления последнего resort или устранения неполадок. Владельцы виртуальных Машин отвечают за обеспечение владельца ключей в безопасном месте.
- Один или несколько Guardians (Защитника узлов ключей) — каждый Guardian представляет структуру виртуализации, на котором владельца авторизует экранированных виртуальных машин для запуска. Предприятиям часто имеют первичный ключ и структуры виртуализации аварийного восстановления (DR) и обычно будет авторизовать их экранированные виртуальные машины для запуска на обоих. В некоторых случаях поставщик общедоступных облачных может размещаться структуре вторичной (DR). Закрытые ключи для любой защищенной структуры поддерживаются только в структуре виртуализации, хотя его открытых ключей, можно загрузить и содержатся в его защиты. 

**Как создать ключ владельца?** Ключ владельца представлены два сертификата. Сертификат для шифрования и сертификат для подписи. Можно создать этих двух сертификатов с помощью вашей собственной инфраструктуры PKI или получить SSL-сертификаты из общедоступного сертификации (ЦС). Для целей тестирования можно также создать самозаверяющий сертификат на любой компьютер, начиная с Windows 10 или Windows Server 2016.

**Сколько владельца ключей должны иметь?** Можно использовать один владелец ключ или ключи многократной владельца. Рекомендуется один владелец ключа для группы виртуальных машин, которые совместно используют же безопасность, уровень доверия или риска, а также для административного управления. Вы можете совместно использовать один владелец ключа для всех присоединенных к домену экранированных виртуальных машин и передать этот ключ владельца, чтобы управлять Администраторы домена.

**Можно ли использовать собственные ключи для Защитника узлов?** Да, вы можете «Перевести Your Own» ключ для размещения поставщика и использовать этот ключ для ваши экранированные виртуальные машины. Это дает возможность использовать определенные ключи (и, используя ключ поставщика услуг размещения) и может использоваться при наличии безопасности или правила, которые необходимо соблюдать. В целях ключа Гигиена ключи Защитника узлов должны отличаться от его владельца.

## <a name="shielding-data"></a>Данные экранирования

Данные экранирования содержит секретные данные, необходимые для развертывания экранированной или поддержкой шифрования виртуальных машин. Он также используется при преобразовании, обычными виртуальными машинами для экранированных виртуальных машин.

Данные экранирования создается с помощью мастера файл данных экранирования и хранится в файлах PDK, которые Отправка Владельцы виртуальных Машин в защищенной структуры.

Экранированные виртуальные машины защиты от атак из структуры скомпрометированных виртуализации, поэтому нам нужен безопасный механизм для передачи инициализации конфиденциальные данные, такие как пароль администратора, учетные данные присоединения к домену или сертификаты протокола удаленного рабочего СТОЛА, не отображая их в структуры виртуализации, самого или его администраторам. Кроме того данные экранирования содержит следующие элементы:

1. Безопасность уровня — экранирования или поддержкой шифрования
2. Владелец, а также список доверенных узлов Guardians, где можно запустить виртуальную Машину
3. Данные инициализации виртуальной машины (unattend.xml, сертификат RDP)
4. Список доверенных подписанных дисков шаблона для создания виртуальной Машины в среде виртуализации 

При создании виртуальной Машины экранирована "или" поддерживается шифрование или преобразование существующей виртуальной Машины, будет предложено выбрать данные экранирования, а не возникает необходимости запроса конфиденциальных сведений.

**Сколько файлов данных экранирования мне?** Один файл данных экранирования может использоваться для создания каждого экранированной виртуальной Машины. Если, однако определенной экранированной виртуальной Машины требует, что любой из четырех элементов отличаться, дополнительный файл данных экранирования не требуется. Например возможно, один файл данных экранирования для ИТ-отдела и другой файл данных экранирования для отдела Кадров, так как их пароль начальной администратора и сертификаты протокола удаленного рабочего СТОЛА различаются.

Хотя с помощью отдельных файлов данных экранирования для каждого экранированной виртуальной Машины существует, он не обязательно является оптимальным выбором и должно выполняться по нужным причинам. Например, если каждый экранированной виртуальной Машины должен иметь пароль отличается от администратора, рекомендуется вместо использования управления паролями, служба или средство например [корпорации Майкрософт локального администратора Password Solution (LAPS)](https://www.microsoft.com/en-us/download/details.aspx?id=46899).

## <a name="creating-a-shielded-vm-on-a-virtualization-fabric"></a>Создание экранированной виртуальной Машины в структуре виртуализации

Существует несколько параметров для создания экранированной виртуальной Машины в структуре виртуализации (ниже актуальны для виртуальных машин как экранированные, так и шифрование поддерживается).

1. Создание экранированной виртуальной Машины в вашей среде и передать его в структуре виртуализации
2. Создание новой экранированной виртуальной Машины из шаблона со знаком в структуре виртуализации
3. Щит существующей виртуальной Машины (существующие виртуальные Машины должны относиться к поколению 2 и должен быть запущен Windows Server 2012 или более поздней версии)

Создание новых виртуальных машин из шаблона является обычной практикой. Тем не менее поскольку диск шаблона, который используется для создания новой экранированной виртуальной Машины находится в структуре виртуализации, дополнительные меры необходимо, чтобы гарантировать, что он имеет не были изменены, администратор структуры вредоносных или вредоносных программ, работающим в структуре. Эта проблема решается с помощью подписанных дисков шаблона — диски подписанных шаблонов и их подписи диска, создаваемые в доверенный администратор или владелец виртуальной Машины. При создании экранированной виртуальной Машины диск шаблона подпись сравнивается с сигнатур, содержащихся в указанном файле данных экранирования. Если любой из подписи файла данных экранирования соответствующие сигнатуре диск шаблона, продолжается ли процесс развертывания. Если совпадения нет можно найти, процесс развертывания прерывается, гарантируя, что секреты виртуальной Машины не будут скомпрометированы из-за диском ненадежным шаблона.

При использовании диски подписанных шаблонов для создания экранированных виртуальных машин, доступны два варианта:

1. Используйте существующий диск подписанного шаблона, предоставляемый поставщиком виртуализации. В этом случае поставщик виртуализации поддерживает диски подписанных шаблонов.
2. Отправьте диск подписанного шаблона в структуре виртуализации. Владелец виртуальной Машины отвечает за ведение диски подписанных шаблонов. 

