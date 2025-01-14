---
title: sp_addtype (Transact-SQL) | Документация Майкрософт
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_addtype
- sp_addtype_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addtype
ms.assetid: ed72cd8e-5ff7-4084-8458-2d8ed279d817
author: stevestein
ms.author: sstein
ms.openlocfilehash: ab825ce5eb1310f3ff502965e409731b8741932e
ms.sourcegitcommit: 43c3d8939f6f7b0ddc493d8e7a643eb7db634535
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/14/2019
ms.locfileid: "72305137"
---
# <a name="sp_addtype-transact-sql"></a>sp_addtype (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Создает псевдоним типа данных.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] используйте вместо этого [CREATE TYPE](../../t-sql/statements/create-type-transact-sql.md) .  
  
 ![Значок ссылки на раздел](../../database-engine/configure-windows/media/topic-link.gif "Значок ссылки на раздел") [Синтаксические обозначения в Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
sp_addtype [ @typename = ] type,   
    [ @phystype = ] system_data_type   
    [ , [ @nulltype = ] 'null_type' ] ;  
```  
  
## <a name="arguments"></a>Аргументы  
`[ @typename = ] type` — имя псевдонима типа данных. Имена типов данных псевдонима должны соответствовать правилам для [идентификаторов](../../relational-databases/databases/database-identifiers.md) и должны быть уникальными в каждой базе данных. Аргумент *Type имеет тип* **sysname**и не имеет значения по умолчанию.  
  
`[ @phystype = ] system_data_type` — это физический или [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] тип данных, на котором основан псевдоним типа данных. *system_data_type* имеет тип **sysname**, не имеет значения по умолчанию и может принимать одно из следующих значений:  
  
||||  
|-|-|-|  
|**bigint**|**binary(n)**|**bit**|  
|**char(n)**|**datetime**|**decimal**|  
|**float**|**image**|**int**|  
|**money**|**nchar(n)**|**ntext**|  
|**numeric**|**nvarchar(n)**|**real**|  
|**smalldatetime**|**smallint**|**smallmoney**|  
|**sql_variant**|**text**|**tinyint**|  
|**uniqueidentifier**|**varbinary(n)**|**varchar(n)**|  
  
 Кавычки необходимы для всех параметров, в которых содержатся начальные пробелы или знаки пунктуации. Дополнительные сведения о доступных типах данных см. в разделе [типы &#40;данных Transact-&#41;SQL](../../t-sql/data-types/data-types-transact-sql.md).  
  
 *n*  
 Неотрицательное целое число, которое показывает длину выбранного типа данных.  
  
 *Ш*  
 Неотрицательное целое число, показывающее максимальное количество десятичных разрядов числа (как слева, так и справа от десятичного разделителя). Дополнительные сведения см. в разделе [decimal и numeric (Transact-SQL)](../../t-sql/data-types/decimal-and-numeric-transact-sql.md).  
  
 *s*  
 Неотрицательное целое число, показывающее максимальное количество десятичных разрядов числа (справа от десятичного разделителя), которое не должно превышать точность. Дополнительные сведения см. в разделе [decimal и numeric (Transact-SQL)](../../t-sql/data-types/decimal-and-numeric-transact-sql.md).  
  
`[ @nulltype = ] 'null_type'` указывает, как псевдоним типа данных обрабатывает значения NULL. *null_type* имеет тип **varchar (** 8 **)** , значение по умолчанию NULL и должен быть заключен в одинарные кавычки ("null", "NOT NULL" или "null"). Если *null_type* не определен явным образом с помощью процедуры **sp_addtype**, ему присваивается текущая допустимость значений NULL по умолчанию. Для определения текущего значения параметра возможности по умолчанию иметь значения NULL используйте системную функцию NULLGETANSINULL. Его можно настраивать с помощью инструкции SET или ALTER DATABASE. Возможность иметь значения NULL необходимо задавать в явной форме. Если параметр **\@phystype** имеет значение **bit**, а **\@nulltype** не задан, по умолчанию используется значение NOT NULL.  
  
> [!NOTE]  
>  Параметр *null_type* определяет допустимость значений NULL по умолчанию для этого типа данных. Если возможность иметь значения NULL явно указывается для типа данных псевдонима при создании таблицы, эта настройка имеет приоритет над возможностью по умолчанию иметь значения NULL. Дополнительные сведения см. в разделе [ALTER &#40;TABLE Transact-&#41; SQL](../../t-sql/statements/alter-table-transact-sql.md) и [Create Table &#40;Transact-&#41;SQL](../../t-sql/statements/create-table-transact-sql.md).  
  
## <a name="return-code-values"></a>Значения кода возврата  
 0 (успешное завершение) или 1 (неуспешное завершение)  
  
## <a name="result-sets"></a>Результирующие наборы  
 None  
  
## <a name="remarks"></a>Примечания  
 Имя типа данных псевдонима должно быть уникальным в базе данных, но типы данных псевдонима с различными именами могут иметь одно определение.  
  
 При запуске процедуры **sp_addtype** создается псевдоним типа данных, который отображается в представлении каталога **sys. types** для конкретной базы данных. Если псевдоним типа данных должен быть доступен во всех новых пользовательских базах данных, добавьте его в **модель**. После создания типа данных псевдонима его можно использовать в инструкциях CREATE TABLE и ALTER TABLE, а также привязывать значения по умолчанию и правила к нему. Все типы данных скалярного псевдонима, созданные с помощью процедуры **sp_addtype** , содержатся в схеме **dbo** .  
  
 Типы данных псевдонима наследуют параметры сортировки базы данных по умолчанию. Параметры сортировки столбцов и переменных типов псевдонимов определяются в инструкциях [!INCLUDE[tsql](../../includes/tsql-md.md)] CREATE TABLE, ALTER TABLE и DECLARE @*local_variable* . Изменение параметров сортировки по умолчанию базы данных применяется только к новым столбцам и переменным типа и не изменяет параметры сортировки существующих столбцов и переменных.  
  
> [!IMPORTANT]  
>  В целях обратной совместимости роли **общей** базы данных автоматически предоставляется разрешение REFERENCES на псевдонимы типов данных, создаваемые с помощью процедуры **sp_addtype**. Примечание. при создании псевдонимов типов данных с помощью инструкции CREATE TYPE вместо процедуры **sp_addtype**автоматическое предоставление не выполняется.  
  
 Типы данных псевдонима не могут быть определены с помощью типов данных [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **timestamp**, **Table**, **XML**, **varchar (max)** , **nvarchar (max)** или **varbinary (max)** .  
  
## <a name="permissions"></a>Разрешения  
 Требуется членство в предопределенной роли базы данных **db_owner** или **db_ddladmin** .  
  
## <a name="examples"></a>Примеры  
  
### <a name="a-creating-an-alias-data-type-that-does-not-allow-for-null-values"></a>A. Создание псевдонима типа данных, не поддерживающего значения NULL  
 В следующем примере создается псевдоним типа данных с именем `ssn` (номер социального страхования), основанный на @no__t типе данных **varchar** , переданном -1. Тип данных `ssn` используется для столбцов, хранящих номера карточек социального страхования, состоящих из 11 разрядов (999-99-9999). Эти столбцы не могут иметь значение NULL.  
  
 Обратите внимание на то, что тип `varchar(11)` заключен в одинарные кавычки, поскольку содержит знак пунктуации (скобки).  
  
```  
USE master;  
GO  
EXEC sp_addtype ssn, 'varchar(11)', 'NOT NULL';  
GO  
```  
  
### <a name="b-creating-an-alias-data-type-that-allows-for-null-values"></a>Б. Создание псевдонима типа данных, поддерживающего значения NULL  
 В следующем примере создается тип данных псевдонима (на основе `datetime`) с именем `birthday`, который поддерживает значения NULL.  
  
```  
USE master;  
GO  
EXEC sp_addtype birthday, datetime, 'NULL';  
```  
  
### <a name="c-creating-additional-alias-data-types"></a>В. Создание дополнительных псевдонимов типов данных  
 В следующем примере создается два дополнительных типа данных псевдонима, `telephone` и `fax`, служащих для внутренних и международных номеров телефонов и факсов.  
  
```  
USE master;  
GO  
EXEC sp_addtype telephone, 'varchar(24)', 'NOT NULL';  
GO  
EXEC sp_addtype fax, 'varchar(24)', 'NULL';  
GO  
```  
  
## <a name="see-also"></a>См. также  
 [Ядро СУБД хранимых &#40;процедур Transact-&#41;SQL](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [CREATE TYPE (Transact-SQL)](../../t-sql/statements/create-type-transact-sql.md)   
 [CREATE DEFAULT (Transact-SQL)](../../t-sql/statements/create-default-transact-sql.md)   
 [CREATE RULE (Transact-SQL)](../../t-sql/statements/create-rule-transact-sql.md)   
 [sp_bindefault (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-bindefault-transact-sql.md)   
 [sp_bindrule (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-bindrule-transact-sql.md)   
 [sp_droptype &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droptype-transact-sql.md)   
 [sp_rename (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md)   
 [sp_unbindefault &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-unbindefault-transact-sql.md)   
 [sp_unbindrule (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-unbindrule-transact-sql.md)   
 [Системные хранимые процедуры (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
