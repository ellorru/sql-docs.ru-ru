---
title: Изменение скомпилированных в собственном коде модулей T-SQL | Документация Майкрософт
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 010318a0-6807-47c3-8ecc-bb7cb60513f0
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 03f7e4fd87068e31674e74dc81dd33dadba323cd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/15/2019
ms.locfileid: "67951268"
---
# <a name="altering-natively-compiled-t-sql-modules"></a>Изменение скомпилированных в собственном коде модулей T-SQL
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

В [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] — [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]) и [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] можно выполнять операции `ALTER` применительно к скомпилированным в собственном коде хранимым процедурам и другим скомпилированным в собственном коде модулям [!INCLUDE[tsql](../../includes/tsql-md.md)], например определяемым пользователем скалярным функциям и триггерам, с помощью инструкции `ALTER`.  
  
При выполнении инструкции `ALTER` скомпилированный в собственном коде модуль [!INCLUDE[tsql](../../includes/tsql-md.md)] перекомпилируется с использованием нового определения. Во время перекомпиляции старую версию модуля все еще можно выполнить. После завершения компиляции выполнение модуля постепенно завершается, и устанавливается новая версия модуля. При изменении скомпилированного в собственном коде модуля [!INCLUDE[tsql](../../includes/tsql-md.md)] можно изменить перечисленные ниже параметры.  
  
-   Параметры  
-   EXECUTE AS  
-   TRANSACTION ISOLATION LEVEL  
-   LANGUAGE  
-   DATEFIRST  
-   DATEFORMAT  
-   DELAYED_DURABILITY  
  
> [!NOTE]  
> Невозможно преобразовать скомпилированные в собственном коде модули [!INCLUDE[tsql](../../includes/tsql-md.md)] в модули, не скомпилированные в собственном коде. Невозможно преобразовать модули T-SQL, не скомпилированные в собственном коде, в модули, скомпилированные в собственном коде.  
  
Дополнительные сведения о функции `ALTER PROCEDURE` и ее синтаксисе см. в разделе [ALTER PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-procedure-transact-sql.md).  
  
Вы можете выполнить [sp_recompile](../../relational-databases/system-stored-procedures/sp-recompile-transact-sql.md) для скомпилированного в собственном коде модуля [!INCLUDE[tsql](../../includes/tsql-md.md)], что приведет к повторной компиляции при следующем выполнении.  
  
## <a name="example"></a>Пример  
В следующем примере создается оптимизированная для памяти таблица (T1) и скомпилированная в собственном коде хранимая процедура (usp_1), которая выбирает все столбцы таблицы T1. Затем процедура usp_1 изменяется: из нее удаляется предложение `EXECUTE AS`, изменяется параметр `LANGUAGE`, а из таблицы T1 выбирается только один столбец (T1).  
  
```sql  
CREATE TABLE [dbo].[T1] (  
  [c1] [int] NOT NULL,  
  [c2] [float] NOT NULL,  
  CONSTRAINT [PK_T1] PRIMARY KEY NONCLUSTERED ([c1])  
  ) WITH ( MEMORY_OPTIMIZED = ON , DURABILITY = SCHEMA_AND_DATA )  
GO  
  
CREATE PROCEDURE [dbo].[usp_1]  
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS BEGIN ATOMIC WITH  
(  
 TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english'  
)  
   SELECT c1, c2 FROM dbo.T1  
END  
GO  
  
ALTER PROCEDURE [dbo].[usp_1]  
WITH NATIVE_COMPILATION, SCHEMABINDING  
AS BEGIN ATOMIC WITH  
(  
 TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'Dutch'  
)  
   SELECT c1 FROM dbo.T1  
END  
GO    
```   
  
## <a name="see-also"></a>См. также:  
 [Скомпилированные в собственном коде хранимые процедуры](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)    
