---
title: sp_query_store_force_plan (Transact-SQL) | Документация Майкрософт
ms.custom: ''
ms.date: 03/29/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- SYS.SP_QUERY_STORE_FORCE_PLAN
- SP_QUERY_STORE_FORCE_PLAN
- SYS.SP_QUERY_STORE_FORCE_PLAN_TSQL
- SP_QUERY_STORE_FORCE_PLAN_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_query_store_force_plan
- sp_query_store_force_plan
ms.assetid: 0068f258-b998-4e4e-b47b-e375157c8213
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b34cf94a2ab6cfec601d41b02bf32b00f0eb3b41
ms.sourcegitcommit: 816ff47eeab157c66e0f75f18897a63dc8033502
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/24/2019
ms.locfileid: "71207721"
---
# <a name="sp_query_store_force_plan-transact-sql"></a>sp_query_store_force_plan (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Включает принудительное применение определенного плана для конкретного запроса.  
  
 Если план принудительно используется для конкретного запроса, каждый раз [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] при возникновении запроса он пытается принудительно выполнить план в оптимизаторе запросов. Если форсирование плана завершается неудачей, запускается расширенное событие, и оптимизатор запросов подает запрос на оптимизацию обычным способом.  
  
 ![Значок ссылки на раздел](../../database-engine/configure-windows/media/topic-link.gif "Значок ссылки на раздел") [Синтаксические обозначения в Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Синтаксис  
  
```  
sp_query_store_force_plan [ @query_id = ] query_id , [ @plan_id = ] plan_id [;]  
```  
  
## <a name="arguments"></a>Аргументы  
`[ @query_id = ] query_id`Идентификатор запроса. *query_id* имеет тип **bigint**и не имеет значения по умолчанию.  
  
`[ @plan_id = ] plan_id`Идентификатор плана запроса, который необходимо принудительно применить. *plan_id* имеет тип **bigint**и не имеет значения по умолчанию.  
  
## <a name="return-code-values"></a>Значения кода возврата  
 0 (успешное завершение) или 1 (неуспешное завершение)  
  
## <a name="remarks"></a>Примечания  
  
## <a name="permissions"></a>Разрешения  
 Требуется разрешение **ALTER** на базу данных.
  
## <a name="examples"></a>Примеры  
 В следующем примере возвращаются сведения о запросах в хранилище запросов.  
  
```sql  
SELECT Txt.query_text_id, Txt.query_sql_text, Pl.plan_id, Qry.*  
FROM sys.query_store_plan AS Pl  
JOIN sys.query_store_query AS Qry  
    ON Pl.query_id = Qry.query_id  
JOIN sys.query_store_query_text AS Txt  
    ON Qry.query_text_id = Txt.query_text_id ;  
```  
  
 Определив query_id и plan_id, которые вы хотите форсировать, используйте следующий пример, чтобы принудительно использовать план в запросе.  
  
```sql  
EXEC sp_query_store_force_plan 3, 3;  
```  
  
## <a name="see-also"></a>См. также  
 [sp_query_store_remove_plan &#40;TRANSCT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-remove-plan-transct-sql.md)   
 [sp_query_store_remove_query &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-remove-query-transact-sql.md)   
 [sp_query_store_unforce_plan &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-unforce-plan-transact-sql.md)   
 [Query Store Catalog Views (Transact-SQL) ](../../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md)  (Представления каталогов хранилища запросов (Transact-SQL))  
 [Мониторинг производительности с помощью хранилища запросов](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [sp_query_store_reset_exec_stats &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-reset-exec-stats-transact-sql.md)   
 [sp_query_store_flush_db &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-flush-db-transact-sql.md)       
 [Рекомендации по хранилищу запросов](../../relational-databases/performance/best-practice-with-the-query-store.md#CheckForced)    
  
  
