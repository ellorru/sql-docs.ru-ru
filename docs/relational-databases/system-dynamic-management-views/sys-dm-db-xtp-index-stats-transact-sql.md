---
title: "sys.dm_db_xtp_index_stats (Transact-SQL) | Документы Microsoft"
ms.custom: 
ms.date: 08/29/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_db_xtp_index_stats
- dm_db_xtp_index_stats
- sys.dm_db_xtp_index_stats_TSQL
- dm_db_xtp_index_stats_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.dm_db_xtp_index_stats dynamic management view
ms.assetid: 8d0a50b8-2015-4576-930f-e3307dfc888e
caps.latest.revision: "25"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8803e51eab52a10e67e90dc6ddb06cfc7d737434
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmdbxtpindexstats-transact-sql"></a>sys.dm_db_xtp_index_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  Содержит статистические данные, собранные со времени последнего перезапуска базы данных.  
  
 Дополнительные сведения см. в разделе [In-Memory OLTP &#40; оптимизация в памяти &#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md) и [правила с помощью индексов в таблицах, оптимизированных для памяти](http://msdn.microsoft.com/library/16ef63a4-367a-46ac-917d-9eebc81ab29b).  

  
|Имя столбца|Тип данных|Description|  
|-----------------|---------------|-----------------|  
|object_id|**bigint**|Идентификатор объекта, которому принадлежит данный индекс.|  
|xtp_object_id|**bigint**|Внутренний идентификатор, соответствующий текущей версии объекта.<br /><br /> Примечание: Применяется к [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)].|  
|index_id|**bigint**|Идентификатор индекса. Значение index_id уникально только в пределах объекта.|  
|scans_started|**bigint**|Количество выполненных сканирований индексов In-Memory OLTP. Каждая инструкция SELECT, INSERT, UPDATE и DELETE требует сканирования индекса.|  
|scans_retries|**bigint**|Количество сканирований индекса, необходимое для повторной попытки.|  
|rows_returned|**bigint**|Общее количество возвращенных строк с момента создания таблицы или запуска [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|rows_touched|**bigint**|Общее количество строк, к которым был осуществлен доступ, с момента создания таблицы или запуска [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|rows_expiring|**bigint**|Только для внутреннего применения.|  
|rows_expired|**bigint**|Только для внутреннего применения.|  
|rows_expired_removed|**bigint**|Только для внутреннего применения.|  
|phantom_scans_started|**bigint**|Только для внутреннего применения.|  
|phatom_scans_retries|**bigint**|Только для внутреннего применения.|  
|phantom_rows_touched|**bigint**|Только для внутреннего применения.|  
|phantom_expiring_rows_encountered|**bigint**|Только для внутреннего применения.|  
|phantom_expired_rows_encountered|**bigint**|Только для внутреннего применения.|  
|phantom_expired_removed_rows_encountered|**bigint**|Только для внутреннего применения.|  
|phantom_expired_rows_removed|**bigint**|Только для внутреннего применения.|  
|object_address|**varbinary(8)**|Только для внутреннего применения.|  
  
## <a name="permissions"></a>Permissions  
 Необходимо разрешение VIEW DATABASE STATE на текущую базу данных.  
  
## <a name="see-also"></a>См. также:  
 [Динамические административные представления таблиц, оптимизированных для памяти &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  