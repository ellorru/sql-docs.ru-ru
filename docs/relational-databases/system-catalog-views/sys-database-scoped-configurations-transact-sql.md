---
title: "sys.database_scoped_configurations (Transact-SQL) | Документы Microsoft"
ms.custom: 
ms.date: 01/16/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- database_scoped_configurations
- database_scoped_configurations_TSQL
- sys.database_scoped_configurations
- sys.database_scoped_configurations_TSQL
helpviewer_keywords: sys.database_scoped_configurations catalog view
ms.assetid: 8899310a-3464-4d38-9f2f-88396c4e7dc2
caps.latest.revision: "13"
author: CarlRabeler
ms.author: carlrab
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3e9df8c18b3ca7556b10e3e2d453c41735a07e52
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/17/2018
---
# <a name="sysdatabasescopedconfigurations-transact-sql"></a>sys.database_scoped_configurations (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Содержит по одной строке для каждой конфигурации. 
  
|Имя столбца|Тип данных|Описание|  
|-----------------|---------------|-----------------|  
|**configuration_id**|**int**|Идентификатор параметра конфигурации.|  
|**name**|**nvarchar(60)**|Имя параметра конфигурации. Сведения о возможных конфигурациях см. в разделе [ALTER DATABASE SCOPED CONFIGURATION &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md).|  
|**value**|**sqlvariant**|Значение, заданное для этого параметра конфигурации для первичной реплики.|  
|**value_for_secondary**|**sqlvariant**|Значение, заданное для этого параметра конфигурации для вторичных реплик.|  
  
##  <a name="Permissions"></a> Разрешения  
 Необходимо быть членом роли **public** .  
  
## <a name="remarks"></a>Remarks  
 Если возвращается значение NULL как значение для **value_for_secondary**, это означает, что сервер-получатель является первичной.  
 
 В области базы данных конфигурации, параметры будут перенесены с базой данных. Это означает, что при заданной базы данных была восстановлена или прикреплена, существующие параметры конфигурации будет оставаться.
  
## <a name="see-also"></a>См. также  
 [ALTER DATABASE SCOPED CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)  
  
  