---
title: sp_delete_jobsteplog (Transact-SQL) | Документация Майкрософт
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_delete_jobsteplog
- sp_delete_jobsteplog_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_jobsteplog
ms.assetid: e9ef4c99-abde-4038-b6a3-a25dcbaf0958
author: stevestein
ms.author: sstein
ms.openlocfilehash: 66b353c7fc79b49cb9cd3fb9fe228075f3a0d473
ms.sourcegitcommit: 43c3d8939f6f7b0ddc493d8e7a643eb7db634535
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/14/2019
ms.locfileid: "72305100"
---
# <a name="sp_delete_jobsteplog-transact-sql"></a>sp_delete_jobsteplog (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Удаляет все журналы шагов заданий для агента [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], заданные аргументами. Используйте эту хранимую процедуру для обслуживания таблицы **таблицу sysjobstepslogs** в базе данных **msdb** .  
  
  
 ![Значок ссылки на раздел](../../database-engine/configure-windows/media/topic-link.gif "Значок ссылки на раздел") [Синтаксические обозначения в Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
sp_delete_jobsteplog { [ @job_id = ] 'job_id' | [ @job_name = ] 'job_name' }  
       [ , [ @step_id = ] step_id | [ @step_name = ] 'step_name' ]  
       [ , [ @older_than = ] 'date' ]  
       [ , [ @larger_than = ] 'size_in_bytes' ]  
```  
  
## <a name="arguments"></a>Аргументы  
`[ @job_id = ] 'job_id'` — идентификационный номер задания, содержащего удаляемый журнал шагов задания. Аргумент *job_id* имеет **тип int**и значение по умолчанию NULL.  
  
`[ @job_name = ] 'job_name'` — имя задания. Аргумент *имя_задания* имеет тип **sysname**и значение по умолчанию NULL.  
  
> **ПРИМЕЧАНИЕ.** Необходимо указать *job_id* или *имя_задания* , но не указывать оба значения.  
  
`[ @step_id = ] step_id` — идентификационный номер этапа в задании, для которого удаляется журнал шагов задания. Если не указано, все журналы шагов заданий в задании удаляются, если не указаны **\@older_than** или **\@larger_than** . *step_id* имеет **тип int**и значение по умолчанию NULL.  
  
`[ @step_name = ] 'step_name'` — имя шага в задании, для которого необходимо удалить журнал шагов задания. *step_name* имеет тип **sysname**и значение по умолчанию NULL.  
  
> **ПРИМЕЧАНИЕ.** Можно указать либо *step_id* , либо *step_name* , но нельзя указывать оба значения.  
  
`[ @older_than = ] 'date'` Дата и время самого старого журнала шагов задания, который вы хотите удержать. Удаляются все журналы шагов задания старше указанной даты и времени. *Date* имеет тип **DateTime**и значение по умолчанию NULL. Можно указать как **\@older_than** , так и **\@larger_than** .  
  
`[ @larger_than = ] 'size_in_bytes'` — Размер в байтах самого крупного журнала шагов задания, который вы хотите удержать. Удаляются все журналы шагов задания, размер которых превышает указанный. Можно указать как **\@larger_than** , так и **\@older_than** .  
  
## <a name="return-code-values"></a>Значения кода возврата  
 **0** (успешное завершение) или **1** (сбой)  
  
## <a name="result-sets"></a>Результирующие наборы  
 None  
  
## <a name="remarks"></a>Примечания  
 **sp_delete_jobsteplog** находится в базе данных **msdb** .  
  
 Если не указаны аргументы, кроме **\@job_id** или **\@job_name** , удаляются все журналы шагов задания для указанного задания.  
  
## <a name="permissions"></a>Разрешения  
 По умолчанию эту хранимую процедуру могут выполнять только члены предопределенной роли сервера **sysadmin** . Другим пользователям должна быть предоставлена одна из следующих предопределенных ролей базы данных агента [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] в базе данных **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Дополнительные сведения о разрешениях этих ролей см. в разделе [Предопределенные роли базы данных агента SQL Server](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
 Только члены **роли sysadmin** могут удалять журнал шагов задания, который принадлежит другому пользователю.  
  
## <a name="examples"></a>Примеры  
  
### <a name="a-removing-all-job-step-logs-from-a-job"></a>A. Удаление всех журналов шагов определенного задания  
 В следующем примере удаляются все журналы шагов задания `Weekly Sales Data Backup`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_delete_jobsteplog  
    @job_name = N'Weekly Sales Data Backup';  
GO  
```  
  
### <a name="b-removing-the-job-step-log-for-a-particular-job-step"></a>Б. Удаление журнала определенного шага задания  
 В следующем примере удаляется журнал для шага 2 задания `Weekly Sales Data Backup`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_delete_jobsteplog  
    @job_name = N'Weekly Sales Data Backup',  
    @step_id = 2;  
GO  
```  
  
### <a name="c-removing-all-job-step-logs-based-on-age-and-size"></a>В. Удаление всех журналов шагов задания по дате создания и размеру  
 В следующем примере удаляются все журналы шагов задания `Weekly Sales Data Backup`, созданные до полудня 25 октября 2005 года, размер которых превышает 100 МБ.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_delete_jobsteplog  
    @job_name = N'Weekly Sales Data Backup',  
    @older_than = '10/25/2005 12:00:00',  
    @larger_than = 104857600;  
GO  
```  
  
## <a name="see-also"></a>См. также  
 [sp_help_jobsteplog &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-jobsteplog-transact-sql.md)   
 [Агент SQL Server хранимых &#40;процедур TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)  
  
  
