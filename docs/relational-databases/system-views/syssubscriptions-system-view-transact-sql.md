---
title: syssubscriptions (Системное представление) (Transact-SQL) | Документация Майкрософт
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- syssubscriptions_TSQL
- syssubscriptions
dev_langs:
- TSQL
helpviewer_keywords:
- syssubscriptions view
ms.assetid: c9613858-9512-43a9-aa53-7ee8064f064c
author: stevestein
ms.author: sstein
ms.openlocfilehash: 517d9359085f7cb4bc4c94eb941981a09ca06eef
ms.sourcegitcommit: 43c3d8939f6f7b0ddc493d8e7a643eb7db634535
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/14/2019
ms.locfileid: "72304786"
---
# <a name="syssubscriptions-system-view-transact-sql"></a>syssubscriptions (системное представление) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Представление **syssubscriptions** предоставляет сведения о подписке. Это представление хранится в базе данных распространителя.  
  
|Имя столбца|Тип данных|Описание|  
|-----------------|---------------|-----------------|  
|**artid**|**int**|Уникальный идентификатор статьи подписки.|  
|**srvid**|**smallint**|Идентификатор сервера подписчика.|  
|**dest_db**|**sysname**|Имя базы данных подписки.|  
|**status**|**tinyint**|Состояние подписки.<br /><br /> **0** = неактивно.<br /><br /> **1** = подписка выполнена.<br /><br /> **2** = активно.|  
|**sync_type**|**tinyint**|Тип начальной синхронизации.<br /><br /> **1** = автоматический.<br /><br /> **2** = нет.|  
|**login_name**|**sysname**|Имя входа, которое используется при подключении к издателю для добавления подписки.|  
|**subscription_type**|**int**|Тип подписки.<br /><br /> **0** = Push-агент распространителя запускается на распространителе.<br /><br /> **1** = по запросу — агент распространителя запускается на подписчике.|  
|**distribution_jobid**|**двоичный (16)**|Определяет задание агента распространителя, который используется для синхронизации подписки.|  
|**тиместмап**|**timestamp**|Дата и время создания подписки.|  
|**update_mode**|**tinyint**|Режим обновления.<br /><br /> **0** = только для чтения.<br /><br /> **1** = немедленное обновление.|  
|**loopback_detection**|**bit**|Применяется к подпискам, которые являются частью двунаправленной топологии репликации транзакций. Механизм распознавания обратной связи определяет, отправляет ли агент распространителя транзакции, созданные в подписчике, обратно подписчику:<br /><br /> **0** = отправляет обратно.<br /><br /> **1** = не отправляет обратно.|  
|**queued_reinit**|**bit**|Определяет, помечена ли статья для инициализации или повторной инициализации. Значение **1** указывает, что статья, на которую оформлена подписка, помечена как для инициализации, так и для повторной инициализации.|  
|**nosync_type**|**tinyint**|Тип инициализации подписки:<br /><br /> **0** = автоматический (моментальный снимок)<br /><br /> **1** = только поддержка репликации<br /><br /> **2** = инициализировать с помощью резервного копирования<br /><br /> **3** = инициализировать из регистрационного номера транзакции в журнале (LSN)<br /><br /> Дополнительные сведения см. в описании параметра **\@sync_type** для [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md).<br /><br /> **3** = [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**срвнаме**|**sysname**|Имя подписчика.|  
  
## <a name="see-also"></a>См. также  
 [Таблицы &#40;репликации Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Представления &#40;репликации Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [syssubscriptions (Transact-SQL)](../../relational-databases/system-tables/syssubscriptions-transact-sql.md)  
  
  
