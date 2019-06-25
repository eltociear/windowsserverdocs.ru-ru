---
title: Добавление записи ресурса DNS
description: Этот раздел является частью в руководстве по управления IP Address Management (IPAM) в Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-ipam
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5379373f-a3d9-4f51-b6fc-bf0f6df1d244
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 36773525187229e498b9addf4b1e6532fd413701
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/20/2019
ms.locfileid: "67282313"
---
# <a name="add-a-dns-resource-record"></a>Добавление записи ресурса DNS

>Относится к: Windows Server (полугодовой канал), Windows Server 2016

В этом разделе можно использовать для добавления одной или нескольких новых записей ресурсов DNS с помощью консоли ipam-клиента.  
  
Для выполнения этой процедуры необходимо быть членом группы **Администраторы** или пользователем с аналогичными правами.  
  
### <a name="to-add-a-dns-resource-record"></a>Чтобы добавить запись ресурса DNS  
  
1.  В диспетчере серверов щелкните **IPAM**. Откроется консоль ipam-клиента.  
  
2.  В области навигации в **НАБЛЮДЕНИЕ и УПРАВЛЕНИЕ**, нажмите кнопку **зон DNS**.  На панели навигации делит на верхней панели навигации и нижней панели навигации.  
  
3.  В нижней области навигации щелкните **прямого просмотра**. Все управляемые IPAM DNS зоны прямого просмотра отображаются в результатах поиска панели отображения. Щелкните правой кнопкой мыши зону, в которой необходимо добавить запись ресурса, а затем нажмите кнопку **добавить DNS-записи ресурса**.  
  
    ![Добавление записи ресурса DNS](../../media/Add-a-DNS-Resource-Record/ipam_DNSrr_01.jpg)
  
4.  **Добавление записей ресурсов DNS** откроется диалоговое окно. В **свойства записей ресурсов**, нажмите кнопку **DNS-сервер** и выберите DNS-сервер, где вы хотите добавить новые записи ресурсов. В **записей ресурсов DNS, настройте**, нажмите кнопку **New**.  
  
    ![Настроить записи ресурсов DNS](../../media/Add-a-DNS-Resource-Record/ipam_DNSrr_02.jpg)  
  
5.  Чтобы отобразить диалоговое окно раскроется **новую запись ресурса**. Нажмите кнопку **тип записи ресурса**.  
  
    ![Тип записи ресурса](../../media/Add-a-DNS-Resource-Record/ipam_DNSrr_03.jpg)  
  
6.  Отображается список типов записей ресурсов. Выберите тип записи ресурса, который вы хотите добавить.  
  
    ![Выберите тип записи для добавления](../../media/Add-a-DNS-Resource-Record/ipam_DNSrr_04.jpg)  
  
7.  В **новую запись ресурса,** в **имя**, введите имя записи ресурса. В **IP-адрес**, введите IP-адрес и выберите свойства записи ресурса, которые подходят для развертывания. Нажмите кнопку **Добавление записи ресурса**.  
  
    ![Добавление записи ресурса](../../media/Add-a-DNS-Resource-Record/ipam_DNSrr_06.jpg)  
  
8.  Если вы не хотите создать новые записи ресурсов, нажмите кнопку **ОК**. Если вы хотите создать новые записи ресурсов, нажмите кнопку **New**.  
  
    ![Нажмите кнопку ОК или новые](../../media/Add-a-DNS-Resource-Record/ipam_DNSrr_r2_01.jpg)
  
9. Чтобы отобразить диалоговое окно раскроется **новую запись ресурса**. Нажмите кнопку **тип записи ресурса**. Отображается список типов записей ресурсов. Выберите тип записи ресурса, который вы хотите добавить.  
  
10. В **новую запись ресурса,** в **имя**, введите имя записи ресурса. В **IP-адрес**, введите IP-адрес и выберите свойства записи ресурса, которые подходят для развертывания. Нажмите кнопку **Добавление записи ресурса**.  
  
    ![Добавление записи ресурса](../../media/Add-a-DNS-Resource-Record/ipam_DNSrr_r2_02.jpg)  
  
11. Если вы хотите добавить дополнительные записи ресурсов, повторите процедуру для создания записей. Когда вы закончите создание новых записях ресурсов, нажмите кнопку **применить**.  
  
    ![Создание записи полный ресурс](../../media/Add-a-DNS-Resource-Record/ipam_DNSrr_r2_03.jpg)  
  
12. **Добавление записи ресурса** диалоговое окно отображает сводку записей ресурсов, хотя IPAM создаются записи о ресурсах на DNS-сервере, который вы указали. После успешного создания записи **состояние** записи — **успех**.  
  
    ![Состояние записи сложения](../../media/Add-a-DNS-Resource-Record/ipam_DNSrr_r2_04.jpg)  
  
13. Нажмите кнопку **ОК**.  
  
## <a name="see-also"></a>См. также  
[Управление записями ресурсов DNS](DNS-Resource-Record-Management.md)  
[Управление IPAM](Manage-IPAM.md)  
  

