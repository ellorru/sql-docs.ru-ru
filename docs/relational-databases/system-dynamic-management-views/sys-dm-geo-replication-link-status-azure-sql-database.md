---
title: sys. dm_geo_replication_link_status
titleSuffix: Azure SQL Database
ms.date: 01/28/2019
ms.service: sql-database
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- dm_geo_replication_link_status
- dm_geo_replication_link_status_TSQL
- sys.dm_geo_replication_link_status
- sys.dm_geo_replication_link_status_TSQL
helpviewer_keywords:
- dm_geo_replication_link_status dynamic management view
- sys.dm_geo_replication_link_status dynamic management view
ms.assetid: d763d679-470a-4c21-86ab-dfe98d37e9fd
author: mashamsft
ms.author: mathoma
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.custom: seo-dt-2019
ms.openlocfilehash: e642fada95ddf20e81f9fcb7da8b6267469ef0c9
ms.sourcegitcommit: f688a37bb6deac2e5b7730344165bbe2c57f9b9c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/08/2019
ms.locfileid: "73843889"
---
# <a name="sysdm_geo_replication_link_status-azure-sql-database"></a>sys.dm_geo_replication_link_status (база данных SQL Azure)

[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Содержит по одной строке для каждой связи репликации между первичной и базой данных-получателем в партнерстве георепликации. Сюда входят как база данных-источник, так и сервер-получатель. Если для данной базы данных-источника существует более одного канала непрерывной репликации, то эта таблица содержит по одной строке для каждой связи. Это представление создается во всех базах данных, включая логическую реплику. Однако запрос этого представления для логической базы данных master возвращает пустой набор.  
  
|Имя столбца|Тип данных|Описание|  
|-----------------|---------------|-----------------|  
|link_guid|**uniqueidentifier**|Уникальный идентификатор канала репликации.|  
|partner_server|**sysname**|Имя сервера базы данных SQL, содержащего связанную базу данных.|  
|partner_database|**sysname**|Имя связанной базы данных на связанном сервере базы данных SQL.|  
|last_replication|**datetimeoffset**|Метка времени для подтверждения последней транзакции получателем на основе часов базы данных-источника. Это значение доступно только в базе данных-источнике.|  
|replication_lag_sec|**int**|Разница во времени в секундах между значением last_replication и меткой времени фиксации этой транзакции на основе базы данных источника, основанной на тактах.  Это значение доступно только в базе данных-источнике.|  
|replication_state|**tinyint**|Состояние георепликации для этой базы данных, одно из следующих:.<br /><br /> 1 = заполнение. Выполняется заполнение целевого объекта георепликации, но две базы данных еще не синхронизированы. Пока заполнение не завершится, вы не сможете подключиться к базе данных-получателю. Удаление базы данных-получателя с сервера-источника приведет к отмене операции заполнения.<br /><br /> 2 = перехватить. База данных-получатель находится в состоянии согласованности транзакций и постоянно синхронизируется с базой данных-источником.<br /><br /> 4 = приостановлено. Это неактивная связь непрерывного копирования. Это состояние обычно означает, что доступной для Interlink полосы пропускания недостаточно для уровня активности транзакций в базе данных-источнике. Однако связь непрерывного копирования не повреждена.|  
|replication_state_desc|**nvarchar(256)**|PENDING<br /><br /> SEEDING<br /><br /> CATCH_UP|  
|роль|**tinyint**|Роль георепликации, одна из следующих:<br /><br /> 0 = основной. Database_id ссылается на базу данных-источник в партнерстве георепликации.<br /><br /> 1 = вторичный.  Database_id ссылается на базу данных-источник в партнерстве георепликации.|  
|role_desc|**nvarchar(256)**|PRIMARY<br /><br /> SECONDARY|  
|secondary_allow_connections|**tinyint**|Вторичный тип, один из следующих:<br /><br /> 0 = прямые подключения не разрешены для базы данных-получателя, и база данных недоступна для чтения.<br /><br /> 2 = все соединения разрешены для базы данных в реплике-получателе REPL; икатион для доступа только для чтения.|  
|secondary_allow_connections_desc|**nvarchar(256)**|Нет<br /><br /> все|  
|last_commit|**datetimeoffset**|Время последней фиксации транзакции в базе данных. При получении в базе данных источника указывает время последней фиксации в базе данных источника. При получении в базе данных-получателе указывает время последней фиксации в базе данных-получателе. При получении в базе данных-получателе, когда первичная реплика канала репликации находится в недоступном виде, она указывает до того, как будет перехвачена дополнительная точка.|
  
> [!NOTE]  
>  Если отношение репликации завершается удалением базы данных-получателя (раздел 4,2), то строка для этой базы данных в представлении **sys. dm_geo_replication_link_status** исчезает.  
  
## <a name="permissions"></a>Разрешения  
 Любая учетная запись с view_database_state разрешением может выполнять запросы к **sys. dm_geo_replication_link_status**.  
  
## <a name="example"></a>Пример  
 Отображение времени отдержек репликации и последней репликации баз данных-получателей.  
  
```  
SELECT   
     link_guid  
   , partner_server  
   , last_replication  
   , replication_lag_sec   
FROM sys.dm_geo_replication_link_status;  
```  
  
## <a name="see-also"></a>См. также раздел  
   [базы &#40;данных&#41; SQL Azure ALTER DATABASE](../../t-sql/statements/alter-database-azure-sql-database.md)  
 [sys. geo_replication_links &#40;базы&#41; данных SQL Azure](../../relational-databases/system-dynamic-management-views/sys-geo-replication-links-azure-sql-database.md)   
 [sys. dm_operation_status &#40;базы данных SQL Azure&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-operation-status-azure-sql-database.md)  
  
  
