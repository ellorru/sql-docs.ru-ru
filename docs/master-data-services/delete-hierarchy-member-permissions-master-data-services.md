---
title: Удаление разрешений элемента иерархии
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- deleting member permissions [Master Data Services]
- members [Master Data Services], deleting permissions
- permissions [Master Data Services], deleting member permissions
ms.assetid: 7f22d5e2-70c1-422c-99c2-e995a47d812a
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: c441545bc88ef28031815cecb2c0f441fa1ea6a4
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/07/2019
ms.locfileid: "73729354"
---
# <a name="delete-hierarchy-member-permissions-master-data-services"></a>Удаление разрешений элемента иерархии (службы Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  В среде [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]удалите разрешения на объект модели для отмены любых существующих назначений.  
  
## <a name="prerequisites"></a>Предварительные требования  
 Чтобы выполнить эту процедуру:  
  
-   необходимо иметь разрешение на доступ к функциональной области **Разрешения пользователей и групп** ;  
  
-   необходимо быть администратором модели. Дополнительные сведения см. в статье [Администраторы (службы Master Data Services)](../master-data-services/administrators-master-data-services.md).  
  
### <a name="to-delete-hierarchy-member-permissions"></a>Удаление разрешения элемента иерархии  
  
1.  В среде [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]щелкните **Разрешения пользователей и групп**.  
  
2.  На странице **Пользователи** или **Группы** выберите строку пользователя или группы, которые необходимо изменить.  
  
3.  Нажмите **Изменить выделенного пользователя**.  
  
4.  Перейдите на вкладку **Элементы иерархии** .  
  
5.  Выберите модель из списка **Модель** .  
  
6.  Выберите версию из списка **Версия** .  
  
7.  Нажмите кнопку **Изменить**.  
  
8.  Найдите узел дерева с разрешением в области **Разрешения элементов иерархии** .  
  
9. Щелкните узел дерева и выберите пункт **Нет** в контекстном меню.  
  
    > [!NOTE]  
    >  Нельзя удалить разрешение у пользователя, если разрешение унаследовано от группы. В этом случае нужно отозвать разрешение у группы.  
  
10. Нажмите кнопку **Сохранить**.  
  
## <a name="see-also"></a>См. также раздел  
 [Разрешения на элементы иерархии (службы Master Data Services)](../master-data-services/hierarchy-member-permissions-master-data-services.md)   
 [Назначение разрешений для элемента иерархии (службы Master Data Services)](../master-data-services/assign-hierarchy-member-permissions-master-data-services.md)  
  
  
