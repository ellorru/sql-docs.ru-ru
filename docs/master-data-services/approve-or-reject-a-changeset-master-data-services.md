---
title: Утверждение или отклонение набора изменений
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 45bd01f9-ae15-4fc5-a2ba-eee565a26ef8
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 401983aa2e5094560f7bcc852c839986ffe4234d
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/07/2019
ms.locfileid: "73728770"
---
# <a name="approve-or-reject-a-changeset-master-data-services"></a>Утверждение или отклонение набора изменений (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Набор изменений — это совокупность ожидающих изменений основных данных. Если для изменений сущности требуется утверждение администратора, после отправки набора изменений на утверждение администратор может просмотреть и утвердить или отклонить его.  
  
## <a name="prerequisites"></a>Предварительные требования  
  
-   Необходимо иметь разрешение на доступ к функциональной области **Обозреватель** . Дополнительные сведения см. в разделе [Разрешения функциональной области (службы Master Data Services)](../master-data-services/functional-area-permissions-master-data-services.md).  
  
-   Необходимо обладать правами администратора сущности.  
  
-   Изменения сущности должны требовать утверждения администратором.  
  
-   Набор изменений можно просмотреть, а затем утвердить или отклонить, если он находится в состоянии ожидания.  
  
-   Пользователи не могут утверждать свои собственные изменения. Если вы администратор сущности, необходимо назначить дополнительного администратора, чтобы утвердить свой набор изменений.  
  
## <a name="to-approve-or-reject-a-changeset"></a>Утверждение или отклонение набора изменений  
  
1.  На домашней странице [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] выберите модель и версию, а затем щелкните **Обозреватель**.  
  
2.  Щелкните сущность в меню **Сущности** .  
  
3.  В области справа выберите **Наборы изменений** и дважды щелкните набор изменений, который необходимо утвердить или отклонить.  
  
4.  Чтобы применить набор изменений и просмотреть ожидающие изменения, нажмите кнопку **Применить** .  
  
5.  Чтобы отклонить набор изменений и отправить его обратно владельцу, нажмите кнопку **Отклонить** .  
  
6.  Чтобы утвердить набор изменений, нажмите кнопку **Утвердить** . Набор изменений фиксируется автоматически.  
  
## <a name="see-also"></a>См. также раздел  
 [Создание набора изменений (Master Data Services)](../master-data-services/create-a-changeset-master-data-services.md)   
 [Применение и обновление набора изменений (службы Master Data Services)](../master-data-services/apply-and-update-a-changeset-master-data-services.md)   
 [Фиксация или отправка набора изменений (Master Data Services)](../master-data-services/commit-or-submit-a-changeset-master-data-services.md)  
  
  
