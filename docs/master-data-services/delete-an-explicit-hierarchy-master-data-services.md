---
title: Удаление явной иерархии
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- explicit hierarchies, deleting
- deleting explicit hierarchies [Master Data Services]
ms.assetid: 4ce177b0-9884-47a2-9cea-212e845dd762
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 74a2b9a825b9e589cba9416eb932bcb824f00373
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/07/2019
ms.locfileid: "73728324"
---
# <a name="delete-an-explicit-hierarchy-master-data-services"></a>Удаление явной иерархии (службы Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  В службах [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]явные иерархии удаляются тогда, когда в них отпадает необходимость.  
  
> [!WARNING]  
>  При удалении явной иерархии все консолидированные элементы в этой иерархии также удаляются. Если удаляются все явные иерархии для сущности, то все коллекции для этой сущности также удаляются и сущность перестает поддерживать явные иерархии и коллекции.  
  
## <a name="prerequisites"></a>Предварительные требования  
 Чтобы выполнить эту процедуру:  
  
-   необходимо иметь разрешение на доступ к функциональной области **Администрирование системы** ;  
  
-   необходимо быть администратором модели. Дополнительные сведения см. в статье [Администраторы (службы Master Data Services)](../master-data-services/administrators-master-data-services.md).  
  
### <a name="to-delete-an-explicit-hierarchy"></a>Удаление явной иерархии  
  
1.  В [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]щелкните область **Администрирование системы**.  
  
2.  На странице **Manage Model** (Управление моделью) выберите в сетке модель и щелкните **Сущности**.  
  
3.  На странице **Manage Entity** (Управление сущностью) выберите в сетке строку сущности, для которой необходимо удалить явную иерархию.  
  
4.  Щелкните **Явные иерархии**.  
  
5.  На странице **Manage Explicit Hierarchy** (Управление явной иерархией) выберите удаляемую явную иерархию.  
  
6.  Нажмите кнопку **Изменить**.  
  
7.  В диалоговом окне подтверждения нажмите кнопку **ОК**.  
  
## <a name="see-also"></a>См. также раздел  
 [Создание явной иерархии (службы Master Data Services)](../master-data-services/create-an-explicit-hierarchy-master-data-services.md)   
 [Явные иерархии (службы Master Data Services)](../master-data-services/explicit-hierarchies-master-data-services.md)  
  
  
