---
title: sys. dm_exec_query_profiles (Transact-SQL) | Документация Майкрософт
ms.custom: ''
ms.date: 10/25/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_exec_query_profiles_TSQL
- sys.dm_exec_query_profiles_TSQL
- dm_exec_query_profiles
- sys.dm_exec_query_profiles
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_query_profiles dynamic management view
ms.assetid: 54efc6cb-eea8-4f6d-a4d0-aa05eeb54081
author: stevestein
ms.author: sstein
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: cd30a6c07bccde04bb38189fab00f688dd763356
ms.sourcegitcommit: f018eb3caedabfcde553f9a5fc9c3e381c563f1a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/18/2019
ms.locfileid: "74165506"
---
# <a name="sysdm_exec_query_profiles-transact-sql"></a>sys.dm_exec_query_profiles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

Контролирует ход выполнения запросов в реальном времени. Например, используйте данное динамическое административное представление для определения, какая часть запроса выполняется медленно. Это динамическое административное представление можно объединять с другими за счет столбцов, определенных в поле описания. Или объедините данное динамическое административное представление с другими счетчиками производительности (такими как Системный Монитор, xperf), используя столбцы меток времени.  
  
## <a name="table-returned"></a>Возвращаемая таблица  
Возвращаемые счетчики есть на каждом операторе и каждом потоке. Результаты являются динамическими и не соответствуют результатам существующих параметров, таких как `SET STATISTICS XML ON`, которые создают выходные данные только по завершении запроса.  
  
|Имя столбца|Data type|Описание|  
|-----------------|---------------|-----------------|  
|session_id|**smallint**|Определяет сеанс, в котором выполняется этот запрос. Ссылка на dm_exec_sessions.session_id.|  
|request_id|**int**|Идентифицирует целевой запрос. Ссылка на dm_exec_sessions.request_id.|  
|sql_handle|**varbinary (64)**|Токен, однозначно определяющий пакет или хранимую процедуру, частью которой является запрос. Ссылка на dm_exec_query_stats.sql_handle.|  
|plan_handle|**varbinary (64)**|Токен, однозначно определяющий план выполнения запроса для пакета, который был выполнен, а его план находится в кэше планов или в данный момент выполняется. Ссылается на dm_exec_query_stats. plan_handle.|  
|physical_operator_name|**nvarchar(256)**|Имя физического оператора.|  
|node_id|**int**|Определяет узел оператора в дереве запросов.|  
|thread_id|**int**|Используется для различения потоков (для параллельного запроса), принадлежащих одному узлу оператора запроса.|  
|task_address|**varbinary (8)**|Определяет задачу SQLOS, используемую этим потоком. Ссылка на dm_os_tasks.task_address.|  
|row_count|**bigint**|Число строк, возвращенных оператором к настоящему моменту.|  
|rewind_count|**bigint**|Число сбросов к текущему моменту.|  
|rebind_count|**bigint**|Число повторных привязок к текущему моменту.|  
|end_of_scan_count|**bigint**|Количество окончаний просмотров к текущему моменту.|  
|estimate_row_count|**bigint**|Предполагаемое количество строк Может быть полезным сравнение estimated_row_count с фактическим row_count.|  
|first_active_time|**bigint**|Время, в миллисекундах, когда оператор был вызван первым.|  
|last_active_time|**bigint**|Время, в миллисекундах, когда оператор был вызван последним.|  
|open_time|**bigint**|Метка времени открытия (в миллисекундах).|  
|first_row_time|**bigint**|Метка времени открытия первой строки (в миллисекундах.)|  
|last_row_time|**bigint**|Метка времени открытия последней строки (в миллисекундах.)|  
|close_time|**bigint**|Метка времени закрытия (в миллисекундах).|  
|elapsed_time_ms|**bigint**|Общее затраченное время (в миллисекундах), используемое операциями целевого узла до сих пор.|  
|cpu_time_ms|**bigint**|Общее время ЦП (в миллисекундах), используемое операциями целевого узла до сих пор.|  
|database_id|**smallint**|Идентификатор базы данных, которая содержит объект, на котором выполняются операции чтения и записи.|  
|object_id|**int**|Идентификатор объекта, на котором выполняются операции чтения и записи. Ссылки на sys.objects.object_id.|  
|index_id|**int**|Индекс (если есть), для которого открыт набор строк.|  
|scan_count|**bigint**|Количество просмотров таблиц и индексов к текущему моменту.|  
|logical_read_count|**bigint**|Количество операций логического считывания к текущему времени.|  
|physical_read_count|**bigint**|Количество операций физического считывания к текущему времени.|  
|read_ahead_count|**bigint**|Количество операций упреждающего чтения к текущему времени.|  
|write_page_count|**bigint**|Число операций записи страниц, вызванных сбросами, к текущему времени.|  
|lob_logical_read_count|**bigint**|Количество операций логического считывания LOB к текущему времени.|  
|lob_physical_read_count|**bigint**|Количество операций физического считывания LOB к текущему времени.|  
|lob_read_ahead_count|**bigint**|Количество операций упреждающего чтения LOB к текущему времени.|  
|segment_read_count|**int**|Количество операций упреждающего чтения сегментов к текущему времени.|  
|segment_skip_count|**int**|Количество сегментов, пропущенных к текущему времени.| 
|actual_read_row_count|**bigint**|Число строк, считанных оператором перед применением остаточного предиката.| 
|estimated_read_row_count|**bigint**|**Применимо к:** Начиная с [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] с пакетом обновления 1 (SP1). <br/>Количество строк, которое должно быть считано оператором перед применением остаточного предиката.|  
  
## <a name="general-remarks"></a>Общие замечания  
 Если у узла плана запроса нет операций ввода-вывода, то для всех счетчиков, связанных с вводом-выводом, устанавливается значение NULL.  
  
 Счетчики, связанные с вводом-выводом, о которых сообщает это динамическое административное представление, более детализированы по сравнению с `SET STATISTICS IO` в следующих двух случаях:  
  
-   `SET STATISTICS IO` группирует счетчики для всех операций ввода-вывода в указанную таблицу. Это динамическое административное представление получит отдельные счетчики для каждого узла в плане запроса, который выполняет операции ввода-вывода в таблице.  
  
-   Если есть параллельное сканирование, данное динамическое административное представление выдает счетчики для каждого из параллельных потоков, выполняющих сканирование.
 
Начиная с [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] с пакетом обновления 1 (SP1), *инфраструктура профилирования статистики выполнения стандартного запроса* существует параллельно с *инфраструктурой профилирования статистики выполнения упрощенных запросов*. `SET STATISTICS XML ON` и `SET STATISTICS PROFILE ON` всегда используют *стандартную инфраструктуру профилирования статистики выполнения запросов*. Для заполнения `sys.dm_exec_query_profiles` необходимо включить одну из инфраструктур профилирования запросов. Дополнительные сведения см. в разделе [Инфраструктура профилирования запросов](../../relational-databases/performance/query-profiling-infrastructure.md).    

>[!NOTE]
> Запрос в процессе расследования должен начаться **после** включения инфраструктуры профилирования запросов, после того как запрос не будет давать результаты `sys.dm_exec_query_profiles`. Дополнительные сведения о том, как включить инфраструктуру профилирования запросов, см. в разделе [инфраструктура профилирования запросов](../../relational-databases/performance/query-profiling-infrastructure.md).

## <a name="permissions"></a>Разрешения  
Для [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] и [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] управляемого экземпляра требуется `VIEW DATABASE STATE` разрешения и членство в роли базы данных `db_owner`.   
На уровнях [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] Premium требуется разрешение `VIEW DATABASE STATE` в базе данных. На уровнях [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] Standard и Basic требуется **Администратор сервера** или учетная запись **администратора Azure Active Directory** .   
   
## <a name="examples"></a>Примеры  
 Шаг 1. Войдите в сеанс, в котором планируется выполнить запрос, который будет проанализирован с помощью `sys.dm_exec_query_profiles`. Чтобы настроить запрос на использование профилирования `SET STATISTICS PROFILE ON`. Выполните ваш запрос в данном сеансе.  
  
```sql  
--Configure query for profiling with sys.dm_exec_query_profiles  
SET STATISTICS PROFILE ON;  
GO  

--Or enable query profiling globally under SQL Server 2016 SP1 or above (not needed in SQL Server 2019)  
DBCC TRACEON (7412, -1);  
GO 
  
--Next, run your query in this session, or in any other session if query profiling has been enabled globally 
```  
  
 Шаг 2. Войдите во второй сеанс, отличный от сеанса, в котором выполняется запрос.  
  
 Следующее выражение суммирует состояние, достигнутое текущим запросом в сеансе 54. Для этого оно рассчитывает общее число выходных строк со всех потоков для каждого узла, и сравнивает его с ожидаемым числом выходных строк для этого узла.  
  
```sql  
--Run this in a different session than the session in which your query is running. 
--Note that you may need to change session id 54 below with the session id you want to monitor.
SELECT node_id,physical_operator_name, SUM(row_count) row_count, 
  SUM(estimate_row_count) AS estimate_row_count, 
  CAST(SUM(row_count)*100 AS float)/SUM(estimate_row_count)  
FROM sys.dm_exec_query_profiles   
WHERE session_id=54
GROUP BY node_id,physical_operator_name  
ORDER BY node_id;  
```  
  
## <a name="see-also"></a>См. также статью  
 [Динамические административные представления и функции (Transact-SQL)](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Динамические административные представления и функции, связанные с выполнением (Transact-SQL)](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)  
 
