---
title: Инициализация с использованием режима клавиши в лесу-бастионе кластера HGS
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: e785ee17bf68c07d965816480baa0d59062fc434
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/31/2019
ms.locfileid: "66447420"
---
# <a name="initialize-the-hgs-cluster-using-key-mode-in-an-existing-bastion-forest"></a>Инициализировать HGS кластера с помощью режима клавиши в существующем лесу бастиона

> Относится к: Windows Server 2019
> 
> [!div class="step-by-step"]
> [«Установка HGS в новом лесу](guarded-fabric-install-hgs-in-a-bastion-forest.md)
> [создать ключ узла»](guarded-fabric-create-host-key.md)

Доменные службы Active Directory устанавливается на компьютере, но должны оставаться ненастроенный.

[!INCLUDE [Obtain certificates for HGS](../../../includes/guarded-fabric-initialize-hgs-default-step-two.md)] 

Прежде чем продолжить, убедитесь, что предварительно подготовленного кластера объектов для службы защиты узла и вошедшего пользователя предоставлены **полный контроль** над объектами VCO и CNO в Active Directory.
Имя объекта виртуального компьютера необходимо передать для `-HgsServiceName` параметра и имя кластера, чтобы `-ClusterName` параметра.

> [!TIP]
> Внимательно проверьте контроллеров домена AD, чтобы обеспечить объектов кластера были реплицированы на контроллеры домена перед продолжением.

Если вы используете сертификаты на основе PFX-ФАЙЛ, выполните следующие команды на сервер HGS:

```powershell
$signingCertPass = Read-Host -AsSecureString -Prompt "Signing certificate password"
$encryptionCertPass = Read-Host -AsSecureString -Prompt "Encryption certificate password"

Install-ADServiceAccount -Identity 'HGSgMSA'

Initialize-HgsServer -UseExistingDomain -ServiceAccount 'HGSgMSA' -JeaReviewersGroup 'HgsJeaReviewers' -JeaAdministratorsGroup 'HgsJeaAdmins' -HgsServiceName 'HgsService' -ClusterName 'HgsCluster' -SigningCertificatePath '.\signCert.pfx' -SigningCertificatePassword $signPass -EncryptionCertificatePath '.\encCert.pfx' -EncryptionCertificatePassword $encryptionCertPass -TrustHostKey
```

Если вы используете сертификатов, установленных на локальном компьютере (например, поддержкой HSM и не экспортируются сертификаты), используйте `-SigningCertificateThumbprint` и `-EncryptionCertificateThumbprint` параметров вместо этого.
