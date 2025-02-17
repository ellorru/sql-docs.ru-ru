---
title: sp_update_proxy (Transact-SQL) | Документация Майкрософт
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_update_proxy
- sp_update_proxy_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER PROXY statement
- sp_update_proxy
ms.assetid: 864fd0e6-9d61-4f07-92ef-145318d2f881
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: ec6c40abd080c86722565762fab3b4f9d30bd0c0
ms.sourcegitcommit: 43c3d8939f6f7b0ddc493d8e7a643eb7db634535
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/14/2019
ms.locfileid: "72305305"
---
# <a name="sp_update_proxy-transact-sql"></a>sp_update_proxy (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Изменяет свойства существующей учетной записи-посредника.  
  
 ![Значок ссылки на раздел](../../database-engine/configure-windows/media/topic-link.gif "Значок ссылки на раздел") [Синтаксические обозначения в Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
sp_update_proxy   
    [ @proxy_id = ] id,  
    [ @proxy_name = ] 'proxy_name',  
    [ @credential_name = ] 'credential_name' ,  
    [ @credential_id = ] credential_id ,  
    [ @new_name = ] 'new_name' ,  
    [ @enabled = ] is_enabled ,  
    [ @description = ] 'description'  
```  
  
## <a name="arguments"></a>Аргументы  
`[ @proxy_id = ] id` — идентификационный номер прокси-сервера, который необходимо изменить. *Proxy_id* имеет **тип int**и значение по умолчанию NULL.  
  
`[ @proxy_name = ] 'proxy_name'` имя изменяемого прокси-сервера. Аргумент *proxy_name* имеет тип **sysname**и значение по умолчанию NULL.  
  
`[ @credential_name = ] 'credential_name'` — имя нового учетного данных для учетной записи-посредника. Аргумент *credential_name* имеет тип **sysname**и значение по умолчанию NULL. Можно указать либо *credential_name* , либо *credential_id* .  
  
`[ @credential_id = ] credential_id` — идентификационный номер новых учетных данных для учетной записи-посредника. *Credential_id* имеет **тип int**и значение по умолчанию NULL. Можно указать либо *credential_name* , либо *credential_id* .  
  
`[ @new_name = ] 'new_name'` новое имя учетной записи-посредника. Аргумент *new_name* имеет тип **sysname**и значение по умолчанию NULL. При указании процедура изменяет имя прокси-сервера на *new_name*. Если этот аргумент равен NULL, имя учетной записи-посредника остается неизменным.  
  
`[ @enabled = ] is_enabled` указывает, включен ли прокси-сервер. Флаг *is_enabled* имеет тип **tinyint**и значение по умолчанию NULL. Если *is_enabled* имеет значение **0**, то прокси-сервер не включен и не может использоваться шагом задания. Если этот аргумент равен NULL, состояние учетной записи-посредника остается неизменным.  
  
`[ @description = ] 'description'` новое описание учетной записи-посредника. *Описание* имеет тип **nvarchar (512)** и значение по умолчанию NULL. Если этот аргумент равен NULL, описание учетной записи-посредника остается неизменным.  
  
## <a name="return-code-values"></a>Значения кода возврата  
 **0** (успешное завершение) или **1** (сбой)  
  
## <a name="remarks"></a>Примечания  
 Необходимо указать либо **\@proxy_name** , либо **\@proxy_id** . Если указаны оба аргумента, они должны ссылаться на одну и ту же учетную запись-посредник, в противном случае хранимая процедура завершается ошибкой.  
  
 Для изменения учетных данных прокси-сервера необходимо указать либо **\@credential_name** , либо **\@credential_id** . Если указаны оба аргумента, они должны ссылаться на одни и те же учетные данные, в противном случае хранимая процедура завершается ошибкой.  
  
 Эта процедура вносит изменения в учетную запись-посредник, но не меняет порядок доступа к нему. Чтобы изменить доступ к учетной записи-посреднику, используйте **sp_grant_login_to_proxy** и **sp_revoke_login_from_proxy**.  
  
## <a name="permissions"></a>Разрешения  
 Эту процедуру могут выполнять только члены предопределенной роли безопасности **sysadmin** .  
  
## <a name="examples"></a>Примеры  
 В следующем примере значение «enabled» для учетной записи-посредника `Catalog application proxy` устанавливается в `0`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_update_proxy  
    @proxy_name = 'Catalog application proxy',  
    @enabled = 0;  
GO  
```  
  
## <a name="see-also"></a>См. также  
 [Агент SQL Server хранимых &#40;процедур Transact-&#41;SQL](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [Реализация агент SQL Server безопасности](../../ssms/agent/implement-sql-server-agent-security.md)   
 [sp_add_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-proxy-transact-sql.md)   
 [sp_delete_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-proxy-transact-sql.md)   
 [sp_grant_login_to_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grant-login-to-proxy-transact-sql.md)   
 [sp_revoke_login_from_proxy &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revoke-login-from-proxy-transact-sql.md)  
  
  
