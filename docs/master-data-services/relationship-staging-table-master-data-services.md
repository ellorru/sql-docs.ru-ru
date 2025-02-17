---
title: Промежуточная таблица связей
ms.custom: ''
ms.date: 04/01/2016
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- relationships staging table [Master Data Services]
- database [Master Data Services], relationships table
ms.assetid: e19b6002-67bd-4e7d-9f19-ecb455522b1a
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: dff1ab73713aed3bfb635c0399028f0c9a1a8c86
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727907"
---
# <a name="relationship-staging-table-master-data-services"></a>Промежуточная таблица связей (службы Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Используйте промежуточную таблицу связей (stg.name_Relationship) в базе данных [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] для изменения расположения элементов в явной иерархии на основе связей между элементами.  
  
##  <a name="TableColumns"></a> Столбцы таблицы  
 В приведенной таблице объясняется, для чего используется каждое поле в промежуточной таблице связей.  
  
|Имя столбца|Описание|Значение|  
|-----------------|-----------------|-----------|  
|**Идентификатор**|Автоматически назначенный идентификатор.|Не вводите значение в этом поле. Если пакет не обработан, это поле пустое.|  
|**RelationshipType**|Обязательное<br /><br /> Задаваемый тип связи.|Возможны следующие значения:<br /><br /> **1**: Родительский элемент<br /><br /> **2**: одноуровневый элемент|  
|**ImportStatus_ID**|Обязательное<br /><br /> Состояние процесса импорта.|Возможны следующие значения:<br /><br /> **0**задается для указания готовности записи к промежуточному хранению;<br /><br /> **1**задается автоматически и указывает на успешное завершение промежуточного процесса записи;<br /><br /> **2**задается автоматически и указывает на ошибку промежуточного процесса записи.|  
|**Batch_ID**|Требуется только для веб-службы<br /><br /> Автоматически назначаемый идентификатор, группирующий записи для промежуточного хранения.<br /><br /> Если пакет не обработан, это поле пустое.|Всем элементам в пакете назначен этот идентификатор, который отображается в пользовательском интерфейсе [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] в столбце **ID** .|  
|**BatchTag**|Требуется, за исключением веб-службы<br /><br /> Уникальное имя для данного пакета, до 50 символов.||  
|**HierarchyName**|Обязательное<br /><br /> Имя явной иерархии. Каждый объединенный элемент может принадлежать только одной явной иерархии.||  
|**ParentCode**|Обязательное<br /><br /> Для связи родительский-дочерний элемент код объединенного элемента, который должен стать родительским для дочернего или объединенного элемента.<br /><br /> Для одноуровневых отношений код одного из одноуровневых элементов.||  
|**ChildCode**|Обязательное<br /><br /> Для связи родительский-дочерний элемент код объединенного или конечного элемента, который должен стать дочерним элементом.<br /><br /> Для одноуровневых отношений код одного из одноуровневых элементов.||  
|**Порядок сортировки**|Необязательно<br /><br /> Целое число, указывающее порядковый номер элемента относительно других элементов на уровнях ниже родителя. У всех дочерних элементов должен быть уникальный идентификатор.||  
|**ErrorCode**|Отображает код ошибки. Для всех записей со значением **ImportStatus_ID** , равным **2**, см. раздел [Ошибки промежуточного процесса (службы Master Data Services)](../master-data-services/staging-process-errors-master-data-services.md).||  
  
## <a name="see-also"></a>См. также раздел  
 [Обзор: импорт данных из таблиц (службы Master Data Services)](../master-data-services/overview-importing-data-from-tables-master-data-services.md)   
 [Просмотр ошибок, возникающих во время помещения на промежуточное хранение (службы Master Data Services)](../master-data-services/view-errors-that-occur-during-staging-master-data-services.md)   
 [Ошибки промежуточного процесса (службы Master Data Services)](../master-data-services/staging-process-errors-master-data-services.md)  
  
  
