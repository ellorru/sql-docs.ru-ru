---
title: sys. DM _exec_compute_node_status (Transact-SQL) | Документация Майкрософт
ms.custom: ''
ms.date: 11/04/2019
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- DM_EXEC_COMPUTE_NODE_STATUS_TSQL
- DM_EXEC_COMPUTE_NODE_STATUS
dev_langs:
- TSQL
helpviewer_keywords:
- PolyBase,views
- PolyBase
- dm_exec_compute_node_status
- sys.dm_exec_compute_node_status management view
ms.assetid: b606f91f-3a08-4a4f-bb57-32ae155b3738
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 11883f7744aad3f8d483e808922a7170c8fe5391
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/04/2019
ms.locfileid: "73532746"
---
# <a name="sysdm_exec_compute_node_status-transact-sql"></a>sys. DM _exec_compute_node_status (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  Содержит дополнительные сведения о производительности и состоянии всех узлов Polybase. Содержит по одной строке на каждый узел.  
  
|Имя столбца|Тип данных|Описание|Диапазон|  
|-----------------|---------------|-----------------|-----------|  
|compute_node_id|`int`|Уникальный числовой идентификатор, связанный с узлом.|Уникален в масштабном кластере независимо от типа.|  
|process_id|`int`|||  
|process_name|`nvarchar(255)`|Логическое имя узла.|Любая строка соответствующей длины.|  
|allocated_memory|`bigint`|Общая выделенная память на этом узле.||  
|available_memory|`bigint`|Общая объем доступной памяти на этом узле.||  
|process_cpu_usage|`bigint`|Общее использование ЦП процесса в тактах.||  
|total_cpu_usage|`bigint`|Общее использование ЦП в тактах.||  
|thread_count|`bigint`|Общее число потоков, используемых на этом узле.||  
|handle_count|`bigint`|Общее число используемых дескрипторов на этом узле.||  
|total_elapsed_time|`bigint`|Общее время, прошедшее с момента запуска или перезапуска системы.|Общее время, прошедшее с момента запуска или перезапуска системы. Если total_elapsed_time превышает максимальное значение для целого числа (24,8 дней в миллисекундах), это приведет к сбою материализации из-за переполнения. Максимальное значение в миллисекундах эквивалентно 24,8 дням.|  
|is_available|`bit`|Флаг, указывающий, доступен ли этот узел.||  
|sent_time|`datetime`|Время последней отправки сетевого пакета этим||  
|received_time|`datetime`|Время последней отправки сетевого пакета этим узлом.||  
|error_id|`nvarchar(36)`|Уникальный идентификатор последней ошибки, произошедшей на этом узле.||
|compute_pool_id|`int`|Уникальный идентификатор пула.|

## <a name="see-also"></a>См. также раздел  
 [Устранение неполадок в polybase с помощью динамических административных представлений](https://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [Динамические административные представления и функции (Transact-SQL)](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Динамические административные представления &#40;, связанные с базами данных TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
