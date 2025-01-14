---
title: sp_replqueuemonitor (Transact-SQL) | Документация Майкрософт
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replqueuemonitor
- sp_replqueuemonitor_TSQL
helpviewer_keywords:
- sp_replqueuemonitor
ms.assetid: 6909a3f1-43a2-4df5-a6a5-9e6f347ac841
author: stevestein
ms.author: sstein
ms.openlocfilehash: d3c84d15087c3cb6bb63380bc6cf0c75e773b883
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/13/2019
ms.locfileid: "74055216"
---
# <a name="sp_replqueuemonitor-transact-sql"></a>sp_replqueuemonitor (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Список сообщений очереди из [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] очереди или [!INCLUDE[msCoName](../../includes/msconame-md.md)] очереди сообщений для подписок, обновляемых посредством очередей, в указанную публикацию. Если используются очереди [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], эта хранимая процедура выполняется в базе данных подписки на подписчике. Если используется Message Queuing, эта хранимая процедура выполняется в базе данных распространителя на распространителе.  
  
 ![Значок ссылки на раздел](../../database-engine/configure-windows/media/topic-link.gif "Значок ссылки на раздел") [Синтаксические обозначения в Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
sp_replqueuemonitor [ @publisher = ] 'publisher'  
    [ , [ @publisherdb = ] 'publisher_db' ]  
    [ , [ @publication = ] 'publication' ]  
    [ , [ @tranid = ] 'tranid' ]  
    [ , [ @queuetype = ] 'queuetype' ]  
```  
  
## <a name="arguments"></a>Аргументы  
`[ @publisher = ] 'publisher'` — это имя издателя. Аргумент *Publisher* имеет тип **sysname**и значение по умолчанию NULL. На этом сервере должна быть настроена публикация. Значение NULL означает для всех издателей.  
  
`[ @publisherdb = ] 'publisher_db' ]` — имя базы данных публикации. Аргумент *publisher_db* имеет тип **sysname**и значение по умолчанию NULL. Значение NULL означает для всех баз данных публикаций.  
  
`[ @publication = ] 'publication' ]` — имя публикации. Аргумент *publication*имеет тип **sysname**и значение по умолчанию NULL. Значение NULL означает для всех публикаций.  
  
`[ @tranid = ] 'tranid' ]` — это идентификатор транзакции. *транид*имеет тип **sysname**и значение по умолчанию NULL. Значение NULL означает для всех транзакций.  
  
`[ @queuetype = ] 'queuetype' ]` — это тип очереди, в которой хранятся транзакции. *значение queuetype* имеет тип **tinyint** со значением по умолчанию **0**и может принимать одно из следующих значений.  
  
|Значение|Описание|  
|-----------|-----------------|  
|**0**|Все типы очередей|  
|**1**|служба очередей сообщений|  
|**2**|Очередь [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
  
## <a name="return-code-values"></a>Значения кода возврата  
 **0** (успешное завершение) или **1** (сбой)  
  
## <a name="remarks"></a>Remarks  
 **sp_replqueuemonitor** используется в репликации моментальных снимков или репликации транзакций с подписками, обновляемыми посредством очередей. Сообщения очереди, не содержащие команд SQL или являющиеся частью команды SQL, не отображаются.  
  
## <a name="permissions"></a>Разрешения  
 Только члены предопределенной роли сервера **sysadmin** или предопределенной роли базы данных **db_owner** могут выполнять **sp_replqueuemonitor**.  
  
## <a name="see-also"></a>См. также статью  
 [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)   
 [Системные хранимые процедуры (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
