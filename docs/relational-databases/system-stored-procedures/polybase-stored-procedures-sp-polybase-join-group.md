---
title: sp_polybase_join_group | Документация Майкрософт
ms.custom: ''
ms.date: 05/24/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
f1_keywords:
- sp_polybase_join_group
helpviewer_keywords:
- PolyBase
ms.assetid: 48066431-fed2-4a8a-85af-ac704689e183
author: rothja
ms.author: jroth
ms.openlocfilehash: ba22ffe282e6b4248ed58bed850bc6ac08255df5
ms.sourcegitcommit: 710d60e7974e2c4c52aebe36fceb6e2bbd52727c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/11/2019
ms.locfileid: "72278111"
---
# <a name="sp_polybase_join_group-transact-sql"></a>sp_polybase_join_group (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Добавляет экземпляр SQL Server в качестве вычислительного узла в группу Polybase для вычислений с масштабным масштабированием.  
  
 На экземпляре SQL Server должен быть установлен компонент [polybase](../../relational-databases/polybase/polybase-guide.md) .  Polybase обеспечивает интеграцию источников данных, отличных от SQL Server, таких как Hadoop и хранилище BLOB-объектов Azure. См. [также &#40;SP_POLYBASE_LEAVE_GROUP Transact-&#41;SQL](../../relational-databases/system-stored-procedures/polybase-stored-procedures-sp-polybase-leave-group.md).  
  
 ![Значок ссылки на раздел](../../database-engine/configure-windows/media/topic-link.gif "Значок ссылки на раздел") [Синтаксические обозначения в Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Синтаксис  
  
```  
sp_polybase_join_group (@head_node_address = N'head_node_address',  
    @dms_control_channel_port = dms_control_channel_port,  
    @head_node_sql_server_instance_name = head_node_sql_server_instance_name)  
[ ; ]          
```  
  
## <a name="arguments"></a>Аргументы  
 *\@head_node_address* = N '*head_node_address*'  
 Имя компьютера, на котором размещен головной узел SQL Server масштабируемой группы Polybase. *\@head_node_address* имеет тип nvarchar (255).  
  
 *\@dms_control_channel_port* = dms_control_channel_port  
 Порт, на котором работает канал управления для Перемещение данных PolyBase службы головного узла. *\@dms_control_channel_port* — это неподписанный __int16. Значение по умолчанию — **16450**.  
  
 *\@head_node_sql_server_instance_name* = head_node_sql_server_instance_name  
 Имя SQL Serverного экземпляра головного узла в масштабируемой группе Polybase. *\@head_node_sql_server_instance_name* имеет тип nvarchar (16).  
  
## <a name="return-code-values"></a>Значения кода возврата  
 0 (успешное завершение) или 1 (неуспешное завершение)  
  
## <a name="permissions"></a>Разрешения  
 Необходимо разрешение CONTROL SERVER.  
  
## <a name="remarks"></a>Примечания  
 После выполнения хранимой процедуры завершите работу ядра Polybase и перезапустите службу Перемещение данных PolyBase на компьютере. Чтобы проверить, выполняется ли следующее динамическое административное представление на головном узле: **sys. DM _exec_compute_nodes**.  
  
## <a name="example"></a>Пример  
 В примере текущий компьютер присоединяется в качестве расчетного узла к группе Polybase.  Имя головного узла — **HST01** , а имя экземпляра SQL Server на головном узле — **MSSQLServer**.  
  
```  
EXEC sp_polybase_join_group N'HST01', 16450, N'MSSQLSERVER'   
```  
  
## <a name="see-also"></a>См. также  
 [Приступая к работе с PolyBase](../../relational-databases/polybase/get-started-with-polybase.md)   
 [Системные хранимые процедуры (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
