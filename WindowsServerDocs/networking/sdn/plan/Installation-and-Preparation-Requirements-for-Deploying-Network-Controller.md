---
title: Требования к развертыванию сетевого контроллера
description: Подготовьте центр обработки данных к развертыванию сетевого контроллера, для чего требуется один или несколько компьютеров или виртуальных машин, а также один компьютер или виртуальную машину. Прежде чем можно будет развернуть сетевой контроллер, необходимо настроить группы безопасности, расположения файлов журнала (при необходимости) и динамическую регистрацию DNS.
manager: grcusanz
ms.prod: windows-server
ms.technology: networking-sdn
ms.topic: get-started-article
ms.assetid: 7f899e62-6e5b-4fca-9a59-130d4766ee2f
ms.author: anpaul
author: AnirbanPaul
ms.date: 08/10/2018
ms.openlocfilehash: f5a7ec331c9d70214cbd0a772de6e2b2c7f4f58e
ms.sourcegitcommit: 7116460855701eed4e09d615693efa4fffc40006
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/15/2020
ms.locfileid: "83433178"
---
# <a name="requirements-for-deploying-network-controller"></a>Требования к развертыванию сетевого контроллера

>Применяется к: Windows Server (Semi-Annual Channel), Windows Server 2016

Подготовьте центр обработки данных к развертыванию сетевого контроллера, для чего требуется один или несколько компьютеров или виртуальных машин, а также один компьютер или виртуальную машину. Прежде чем можно будет развернуть сетевой контроллер, необходимо настроить группы безопасности, расположения файлов журнала (при необходимости) и динамическую регистрацию DNS.


## <a name="network-controller-requirements"></a>Требования к сетевому контроллеру

Для развертывания сетевого контроллера требуется один или несколько компьютеров или виртуальных машин, которые служат сетевым контроллером, а один компьютер или виртуальная машина — как клиент управления для сетевого контроллера. 

- Все виртуальные машины и компьютеры, запланированные как узлы сетевого контроллера, должны работать под управлением Windows Server 2016 Datacenter Edition. 
- На любом компьютере или виртуальной машине, на которой устанавливается сетевой контроллер, должен работать выпуск Datacenter операционной системы Windows Server 2016. 
- Клиентский компьютер управления или виртуальная машина для сетевого контроллера должны работать под управлением Windows 10. 


## <a name="configuration-requirements"></a>Требования настройки

Перед развертыванием сетевого контроллера необходимо настроить группы безопасности, расположения файлов журнала (при необходимости) и динамическую регистрацию DNS.

### <a name="step-1-configure-your-security-groups"></a>Шаг 1. Настройка групп безопасности

Первое, что нужно сделать, — создать две группы безопасности для проверки подлинности Kerberos. 

Вы создаете группы для пользователей, имеющих разрешение на: 

1. Настройка сетевого контроллера<p>Вы можете присвоить этому группе администраторов сетевого контроллера, например. 
2.  Настройка сети и управление ею с помощью сетевого контроллера<p>Можно присвоить имя этой группе пользователей сетевого контроллера, например. Для настройки сетевого контроллера и управления им используйте пересылку данных о состоянии (остальное).

>[!NOTE]
>Все добавляемые пользователи должны быть членами группы "Пользователи домена" в Active Directory "пользователи и компьютеры".

### <a name="step-2-configure-log-file-locations-if-needed"></a>Шаг 2. Настройка расположения файлов журналов при необходимости

Далее необходимо настроить расположения файлов для хранения журналов отладки сетевого контроллера на компьютере сетевого контроллера или виртуальной машине или на удаленном файловом ресурсе. 

>[!NOTE]
>Если журналы хранятся в удаленном файловом ресурсе, убедитесь, что общая папка доступна из сетевого контроллера.


### <a name="step-3-configure-dynamic-dns-registration-for-network-controller"></a>Шаг 3. Настройка динамической регистрации DNS для сетевого контроллера

Наконец, далее нужно развернуть узлы кластера сетевого контроллера в той же подсети или в разных подсетях. 


|         Если...         |                                                                                                                                                         То...                                                                                                                                                         |
|-----------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  В той же подсети;  |                                                                                                                                Необходимо указать IP-адрес сети сетевого контроллера.                                                                                                                                 |
| В разных подсетях | Необходимо указать DNS-имя RESTFUL сетевого контроллера, которое вы создадите в процессе развертывания. Необходимо также выполнить следующие действия.<ul><li>Настройте динамическое обновление DNS для DNS-имени сетевого контроллера на DNS-сервере.</li><li>Ограничьте динамические обновления DNS только для узлов сетевого контроллера.</li></ul> |

---

> [!NOTE]
> Членство в группах **"Администраторы домена" или "** эквивалентное" является минимальным требованием для выполнения этих процедур.

1. Разрешить динамическое обновление DNS для зоны.

   а. Откройте диспетчер DNS и в дереве консоли щелкните правой кнопкой мыши соответствующую зону и выберите пункт **Свойства**. 

   б. На вкладке **Общие** убедитесь, что зона принадлежит к типу **первичная** или **Active Directory-Integrated**.

   в. В меню **динамические обновления**убедитесь, что выбран параметр **только защита** , а затем нажмите кнопку **ОК**.

2. Настройка разрешений безопасности зоны DNS для узлов сетевого контроллера

   а.  На вкладке **Безопасность** нажмите кнопку **Дополнительно**. 

   б. В окне **Дополнительные параметры безопасности**нажмите кнопку **Добавить**. 

   в. Щелкните **Выбор участника**. 

   г. В диалоговом окне **Выбор пользователя, компьютера, учетной записи службы или группы** нажмите кнопку **типы объектов**. 

   Д. В списке **типы объектов**выберите **Компьютеры**, а затем нажмите кнопку **ОК**.

   f. В диалоговом окне **Выбор пользователя, компьютера, учетной записи службы или группы** введите NetBIOS-имя одного из узлов сетевого контроллера в развертывании, а затем нажмите кнопку **ОК**.

   ж. В **поле запись разрешения**проверьте следующие значения.

      - **Тип** = разрешить
      - **Применимо к** = этот объект и все дочерние объекты

   h. В списке **разрешения**выберите **записать все свойства** и **Удалить**, а затем нажмите кнопку **ОК**.

3. Повторите эти действия для всех компьютеров и виртуальных машин в кластере сетевого контроллера.

### <a name="step-4-configure-service-principal-name-if-using-kerberos-based-authentication"></a>Шаг 4. Настройка имени субъекта-службы при использовании проверки подлинности на основе Kerberos

Если сетевой контроллер использует проверку подлинности на основе Kerberos для взаимодействия с клиентами управления, необходимо настроить имя участника-службы (SPN) для сетевого контроллера в Active Directory. Сетевой контроллер автоматически настраивает имя субъекта-службы. Все, что нужно сделать, — предоставить разрешения на компьютеры сетевого контроллера для регистрации и изменения имени участника-службы. Дополнительные сведения см. в разделе [Настройка имен участников-служб (SPN)](https://docs.microsoft.com/windows-server/networking/sdn/security/kerberos-with-spn#configure-service-principal-names-spn).

## <a name="deployment-options"></a>Параметры развертывания

### <a name="network-controller-deployment"></a>Развертывание сетевого контроллера

Настройка обеспечивает высокую доступность с тремя узлами сетевого контроллера, настроенными на виртуальных машинах. Также показаны два клиента с виртуальной сетью клиента 2, которые разбиваются на две виртуальные подсети для имитации веб-уровня и уровня базы данных.  

![Планирование NC в SDN](../../media/Plan-a-Software-Defined-Network-Infrastructure/SDN-NC-Planning.png)

### <a name="network-controller-and-software-load-balancer-deployment"></a>Развертывание сетевого контроллера и программной подсистемы балансировки нагрузки

Для высокого доступность существует два или более узла SLB/МУЛЬТИПЛЕКСОРа.

![Планирование NC в SDN](../../media/Plan-a-Software-Defined-Network-Infrastructure/SDN-SLB-Deployment.png)

### <a name="network-controller-software-load-balancer-and-ras-gateway-deployment"></a>Сетевой контроллер, программное Load Balancer и развертывание шлюза RAS

Существует три виртуальных машины шлюза. два являются активными, а одна — избыточной.

![Планирование NC в SDN](../../media/Plan-a-Software-Defined-Network-Infrastructure/SDN-GW-Deployment.png)  

>[!IMPORTANT] 
>При развертывании с помощью VMM убедитесь, что виртуальные машины инфраструктуры (сервер VMM, AD/DNS, SQL Server и т. д.) не размещены ни на одном из четырех узлов, показанных на схемах.  


## <a name="next-steps"></a>Дальнейшие действия
[Спланируйте программно определенную сетевую инфраструктуру](https://technet.microsoft.com/windows-server-docs/networking/sdn/plan/plan-a-software-defined-network-infrastructure).

## <a name="related-topics"></a>Связанные темы
- [Сетевой контроллер](../technologies/network-controller/Network-Controller.md) 
- [Высокий уровень доступности сетевого контроллера](../technologies/network-controller/network-controller-high-availability.md) 
- [Развертывание сетевого контроллера с помощью Windows PowerShell](../deploy/Deploy-Network-Controller-using-Windows-PowerShell.md)   
- [Установка роли сервера сетевого контроллера с помощью диспетчера серверов](../technologies/network-controller/Install-the-Network-Controller-server-role-using-Server-Manager.md)   
