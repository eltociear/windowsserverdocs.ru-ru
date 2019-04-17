---
title: Настройка параметров DNS и брандмауэра
description: Этот раздел содержит подробные инструкции по развертыванию VPN в Windows Server 2016.
ms.prod: windows-server-threshold
ms.technology: networking-ras
ms.topic: article
ms.assetid: d8cf3bae-45bf-4ffa-9205-290d555c59da
ms.localizationpriority: medium
ms.author: pashort
author: shortpatti
ms.date: 06/11/2018
ms.openlocfilehash: f57bfa005ef1af2556e4bd1cbb90ef8d3cfd22e3
ms.sourcegitcommit: 4893d79345cea85db427224bb106fc1bf88ffdbc
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/05/2018
ms.locfileid: "6067485"
---
# Шаг 5. Настройка параметров DNS и брандмауэра

>Область применения: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows 10

& #171;  [ **Предыдущих:** шаг 4. Установка и настройка сервера политики сети](vpn-deploy-nps.md)<br>
& #187;  [ **Далее:** шаг 6. Настройка клиента Windows 10 всегда на VPN-подключений](vpn-deploy-client-vpn-connections.md)

На этом этапе настройки DNS и брандмауэра параметры для подключения VPN.

## Настройка разрешения имен DNS

При подключении удаленными клиентами VPN, они используют одинаковые DNS-серверы, использующие внутренних клиентов, что позволяет им для разрешения имен так же, что и остальная часть внутренние рабочие станции. 

По этой причине необходимо убедиться, что имя компьютера, которое внешние клиенты используют для подключения к VPN-сервер соответствует альтернативное имя субъекта, определенные в сертификаты, выданные VPN-сервер.

Чтобы убедиться, что удаленные пользователи могут подключаться к VPN-серверу, можно создать запись A DNS (адреса узла) в вашем внешних зоне DNS. Запись следует использовать дополнительное имя субъекта сертификата для VPN-сервера.


### Для добавления узла \ записи ресурса (A или AAAA\) для зоны

1. На DNS-сервере, в диспетчере сервера щелкните **средства**и нажмите кнопку **DNS**. Откроется диспетчер DNS.
2. В дереве консоли диспетчера DNS выберите сервер, которым требуется управлять.
3. В области сведений в поле **имени**double\ одним нажатием **Зоны прямого просмотра** чтобы развернуть представление.
4. Сведения о **Зоны прямого просмотра** , right\ одним нажатием зоны прямого просмотра к которой необходимо добавить запись, а затем нажмите кнопку **новый узел \(A or AAAA\)**. Откроется диалоговое окно **Новый узел** .
5. В **Новый узел**, **имя**введите дополнительное имя субъекта сертификата для VPN-сервера.
6. В IP-адрес введите IP-адрес для VPN-сервера. Можно ввести адрес в IP версии 4 (IPv4) формат для добавления записи ресурса \(A\) узла или IP версии 6 \(IPv6\) формат для добавления записи ресурса \(AAAA\) узла.
7. Если вы создали зону обратного просмотра для диапазона IP-адресов, включая IP-адрес, который вы ввели, затем установите флажок **Создать соответствующую запись указателя** .  При выборе этого параметра создает запись ресурса \(PTR\) дополнительных указателя в зону обратного просмотра для данного узла, на основании информации, введенное **имя** и **IP-адрес**.
8. Нажмите кнопку **Добавить узел**.

## Настройка брандмауэра Edge

Брандмауэр Edge отделяет внешней сети периметра через Интернет. Визуальное представление такое разделение см. на рисунке в разделе [Всегда на VPN Обзор технологии](../always-on-vpn-technology-overview.md).

Edge брандмауэра необходимо разрешить и перенаправлять определенные порты для VPN-сервера. При использовании сетевых адресов \(NAT\) в брандмауэре, edge, может потребоваться включить перенаправления портов для ports500 \(UDP\) протокола датаграмм пользователя и 4500. Перешлите эти порты IP-адрес, назначенный во внешний интерфейс VPN-сервер.

Если вы маршрутизации трафика входящих и преобразование сетевых адресов выполняют или присутствуют специальные за VPN-сервер, то необходимо открыть правила вашего брандмауэра, чтобы разрешить UDP ports500 и 4500 входящих внешний IP-адрес применяется для общего интерфейса на VPN-сервер.

В любом случае если брандмауэра поддерживает тщательную проверку пакетов и у вас возникли трудности, формируя клиентские подключения следует пытаться ослабить или отключить тщательную проверку пакетов для сеансов IKE.

Сведения о том, как выполнить эти изменения конфигурации см. в разделе документации брандмауэра.

## Настройка брандмауэра внутреннего периметра сети

Внутренний сетевой брандмауэр периметра отделяет организации или в корпоративной сети из внутренней сети периметра. Визуальное представление такое разделение см. на рисунке в разделе [Всегда на VPN Обзор технологии](../always-on-vpn-technology-overview.md).

В этом развертывания удаленного доступа VPN-сервер в локальной сети настроен в качестве RADIUS-клиента.  VPN-сервер отправляет RADIUS-трафика на сервер политики сети в корпоративной сети, а также получает RADIUS-трафик от сервера политики сети.

Настройка брандмауэра для разрешения RADIUS-трафика в обоих направлениях.


>[!NOTE]
>Сервера политики сети в организации и в корпоративной сети выступает в качестве RADIUS-сервера для VPN-сервера, который является RADIUS-клиента. Дополнительные сведения о инфраструктуры RADIUS см. в разделе [Сервера политики сети (NPS)](../../../../../networking/technologies/nps/nps-top.md).

### RADIUS-трафика портов на VPN-сервера и сервера политики сети

По умолчанию сервера политики сети и VPN прослушивать RADIUS-трафика на портах 1812, 1813, 1645 и 1646 на все установленные сетевые адаптеры. При включении брандмауэра Windows в режиме повышенной безопасности, при установке сервера политики сети, исключения брандмауэра для эти порты автоматически создаются во время установки для трафика IPv4 и IPv6.

>[!IMPORTANT]
>Если сервер удаленного доступа настроены для отправки RADIUS-трафика через порты, отличные от эти значения по умолчанию, удалить исключения, созданные в брандмауэр Windows в режиме повышенной безопасности при установке сервера политики сети и создавать исключения для портов, используемые для RADIUS-трафика.

### Используйте те же порты RADIUS для конфигурация брандмауэра для внутреннего периметра сети

При использовании конфигурации порта по умолчанию RADIUS на VPN-сервера и сервера политики сети убедитесь, что при открытии следующие порты внутреннего межсетевого экрана периметра сети:

- Порты UDP1812, UDP1813, UDP1645 и UDP1646

Если вы не используете RADIUS-портов по умолчанию при развертывании сервера политики сети, необходимо настроить брандмауэр, чтобы разрешить RADIUS-трафика на портах, которые вы используете. Дополнительные сведения см. в разделе [Настройка брандмауэров для RADIUS-трафика](../../../../../networking/technologies/nps/nps-firewalls-configure.md).

## Дальнейшие действия
[Шаг 6. Настройка Windows 10 клиента всегда на VPN-подключений](vpn-deploy-client-vpn-connections.md): на этом этапе настройки клиентских компьютеров Windows 10 для связи с ИТ-инфраструктуры с VPN-подключение. Можно использовать несколько технологий для настройки клиентами VPN в Windows 10, включая Windows PowerShell, System Center Configuration Manager и Intune. Все три требуют XML-ФАЙЛ VPN-профиль, чтобы настроить соответствующие параметры VPN. 

---