---
title: Репозиторий программного обеспечения Linux для продуктов Майкрософт
description: В этом документе описывается, как использовать и устанавливать программные пакеты Linux для продуктов Майкрософт.
ms.prod: windows-server
manager: szark
ms.technology: compute
ms.topic: article
ms.assetid: b5387444-595f-4f38-abb7-163a70ea1895
author: szarkos
ms.author: szark
ms.date: 10/16/2017
ms.openlocfilehash: b57a1e7243f989a4529a666880572a9ceaa57644
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/08/2020
ms.locfileid: "80852067"
---
# <a name="linux-software-repository-for-microsoft-products"></a>Репозиторий программного обеспечения Linux для продуктов Майкрософт

## <a name="overview"></a>Обзор
Корпорация Майкрософт создает и поддерживает различные программные продукты для систем Linux и делает их доступными через стандартные репозитории пакетов APT и YUM. В этом документе описывается, как настроить репозиторий в системе Linux, чтобы можно было установить или обновить программное обеспечение Microsoft Linux с помощью стандартных средств управления пакетами для дистрибутива.

Репозиторий программного обеспечения Microsoft Linux состоит из нескольких дочерних репозиториев:

 - произ. рабочий репозиторий рабочей области предназначен для пакетов, предназначенных для использования в рабочей среде. Эти пакеты коммерчески поддерживаются корпорацией Майкрософт в соответствии с условиями действующего соглашения о поддержке или программы, имеющейся в корпорации Майкрософт.

 - MSSQL-Server — эти репозитории содержат пакеты для Microsoft SQL Server на Linux — см. также [SQL Server на Linux](https://www.microsoft.com/sql-server/sql-server-vnext-including-Linux).

> [!Note]
> Пакеты в репозиториях программного обеспечения Linux подчиняются условиям лицензии, расположенным в пакетах. Ознакомьтесь с условиями лицензионного соглашения перед использованием пакета. Установка и использование пакета составляют принятие этих условий. Если вы не согласны с условиями лицензии, не используйте пакет.


## <a name="configuring-the-repositories"></a>Настройка репозиториев
Репозитории можно настроить автоматически, установив пакет Linux, который относится к дистрибутиву и версии Linux. Пакет установит конфигурацию репозитория вместе с открытым ключом GPG, который используется такими инструментами, как APT/Yum/zypper, для проверки подписанных пакетов и метаданных репозитория.

### <a name="enterprise-linux-rhel-and-variants"></a>Enterprise Linux (RHEL и варианты)

 - Enterprise Linux 6 (EL6)

        sudo rpm -Uvh https://packages.microsoft.com/config/rhel/6/packages-microsoft-prod.rpm

 - Enterprise Linux 7 (EL7)

        sudo rpm -Uvh https://packages.microsoft.com/config/rhel/7/packages-microsoft-prod.rpm


### <a name="ubuntu"></a>Ubuntu

 - Ubuntu 14,04 (Trusted)

        curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
        sudo apt-add-repository https://packages.microsoft.com/ubuntu/14.04/prod
        sudo apt-get update

 - Ubuntu 16,04 (Xenial)

        curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
        sudo apt-add-repository https://packages.microsoft.com/ubuntu/16.04/prod
        sudo apt-get update

 - Ubuntu 18,04 (Бионик)

         curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
        sudo apt-add-repository https://packages.microsoft.com/ubuntu/18.04/prod
        sudo apt-get update

 - Ubuntu 18,10 (космическими)

         curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
        sudo apt-add-repository https://packages.microsoft.com/ubuntu/18.10/prod
        sudo apt-get update

 - Ubuntu 19,04 (Disco)

         curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
        sudo apt-add-repository https://packages.microsoft.com/ubuntu/19.04/prod
        sudo apt-get update

### <a name="suse-linux-enterprise-12"></a>SUSE Linux Enterprise 12

        sudo rpm -Uvh https://packages.microsoft.com/config/sles/12/packages-microsoft-prod.rpm


## <a name="manual-configuration"></a>Настроить вручную
Файлы конфигурации репозитория доступны в [Packages.Microsoft.com/config](https://packages.microsoft.com/config/). Имя и расположение этих файлов можно найти с помощью следующего соглашения об именовании URI:

        https://packages.microsoft.com/config/<Distribution>/<Version>/prod.(repo|list)

**Ключ подписывания пакета и репозитория**

 - Открытый ключ Microsoft GPG можно скачать здесь: [https://packages.microsoft.com/keys/microsoft.asc](https://packages.microsoft.com/keys/microsoft.asc)
 - Идентификатор открытого ключа: Майкрософт (подписывание выпуска) <gpgsecurity@microsoft.com>
 - Отпечаток открытого ключа: `BC52 8686 B50D 79E3 39D3 721C EB3E 94AD BE12 29CF`

### <a name="examples"></a>Примеры

 - RHEL/CentOS 7

        # Install repository configuration
        curl https://packages.microsoft.com/config/rhel/7/prod.repo > ./microsoft-prod.repo
        sudo cp ./microsoft-prod.repo /etc/yum.repos.d/

        # Install Microsoft's GPG public key
        curl https://packages.microsoft.com/keys/microsoft.asc > ./microsoft.asc
        sudo rpm --import ./microsoft.asc

 - Ubuntu 16.04

        # Install repository configuration
        curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list > ./microsoft-prod.list
        sudo cp ./microsoft-prod.list /etc/apt/sources.list.d/

        # Install Microsoft GPG public key
        curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
        sudo cp ./microsoft.gpg /etc/apt/trusted.gpg.d/



