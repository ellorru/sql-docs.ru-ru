---
title: "Возвращающие табличные значения параметров (ODBC) | Документы Microsoft"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-table-valued-parameters
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC)
- ODBC, table-valued parameters
ms.assetid: ef06cd13-18e2-4c65-8ede-c3955d820e54
caps.latest.revision: "28"
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ddf538c325283ad20c0e75ee73c49799fe890404
ms.sourcegitcommit: a0aa5e611a0e6ebb74ac1e2f613e8916dc7a7617
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/24/2018
---
# <a name="table-valued-parameters-odbc"></a>Возвращающие табличное значение параметры (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Поддержка в ODBC возвращающих табличное значение параметров позволяет клиентским приложениям с большей эффективностью передавать параметризованные данные на сервер за счет передачи нескольких строк в ходе одного вызова.  
  
 Сведения о возвращающих табличные значения параметров на сервере см. в разделе [использование возвращающих табличные значения параметры &#40; компонент Database Engine &#41;](../../relational-databases/tables/use-table-valued-parameters-database-engine.md).  
  
 В ODBC существует два способа передачи на сервер возвращающих табличное значение параметров.  
  
-   Все данные возвращающего табличное значение параметра может быть в памяти во время вызова SQLExecDirect или SQLExecute. Эти данные хранятся в массивах, если в табличном значении имеется несколько строк.  
  
-   Приложение может указать данные времени выполнения для возвращающего табличное значение параметра при вызове SQLExecDirect или SQLExecute. В этом случае строки данных для табличного значения могут быть представлены в пакетах или по одному, чтобы снизить требования, предъявляемые к памяти.  
  
 В первом случае хранимые процедуры могут инкапсулировать дополнительные объемы бизнес-логики. К примеру, если элементы заказа передаются в виде возвращающего табличное значение параметра, одна хранимая процедура может инкапсулировать целую транзакцию по приему заказов. Этот параметр очень эффективен, поскольку предполагает только одно обращение к серверу. Существует и другая возможность: использовать одни процедуры для обработки заголовка заказа, а другие – для элементов заказа, но в этом случае потребуется дополнительный код и более сложный контракт между клиентом и сервером.  
  
 Второй метод представляет собой эффективный механизм для выполнения массовых операций с очень большими объемами данных. Это дает приложению возможность осуществлять потоковую передачу строк данных на сервер без предварительной буферизации их в памяти.  
  
 При создании этой табличной переменной можно формировать ограничения и первичные ключи. Ограничения дают хорошую гарантию того, что данные таблицы соответствуют определенным требованиям.  
  
## <a name="in-this-section"></a>В этом разделе  
 [Сценарии использования возвращающих табличное значение параметров ODBC](../../relational-databases/native-client-odbc-table-valued-parameters/uses-of-odbc-table-valued-parameters.md)  
 Описывает основные пользовательские сценарии для возвращающих табличное значение параметров и ODBC.  
  
 [Тип ODBC SQL для параметров, возвращающих табличное значение](../../relational-databases/native-client-odbc-table-valued-parameters/odbc-sql-type-for-table-valued-parameters.md)  
 Описывает тип SQL_SS_TABLE. Это новый тип ODBC SQL, поддерживающий возвращающие табличное значение параметры.  
  
 [Поля дескрипторов возвращающего табличное значение параметра](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameter-descriptor-fields.md)  
 Описывает поля дескриптора, которые поддерживают возвращающие табличное значение параметры.  
  
 [Поля дескриптора для столбцов, содержащих параметры, возвращающие табличные значения](../../relational-databases/native-client-odbc-table-valued-parameters/descriptor-fields-for-table-valued-parameter-constituent-columns.md)  
 Описывает поля дескриптора, имеющие смысл для возвращающих табличное значение параметров.  
  
 [Поля диагностических записей для возвращающих табличные значения параметров](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameter-diagnostic-record-fields.md)  
 Описывает два диагностических поля, добавленных к диагностическим записям для поддержки параметров, возвращающих табличное значение.  
  
 [Атрибуты инструкции, влияющие на возвращающие табличное значение параметры](../../relational-databases/native-client-odbc-table-valued-parameters/statement-attributes-that-affect-table-valued-parameters.md)  
 Описывает новое поле заголовка дескриптора, активирующее столбцы с возвращающими табличное значение параметрами, к которым будет осуществляться обращение.  
  
 [Привязка и передача данных возвращающих табличное значение параметров и значений столбцов](../../relational-databases/native-client-odbc-table-valued-parameters/binding-and-data-transfer-of-table-valued-parameters-and-column-values.md)  
 Описывает привязку параметров и разъясняет, как передавать серверу возвращающий табличное значение параметр.  
  
 [Метаданные возвращающего табличное значение параметра для подготовленных инструкций](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameter-metadata-for-prepared-statements.md)  
 Описывает, как приложение может получить метаданные для заготовленного вызова процедуры.  
  
 [Дополнительные метаданные возвращающего табличное значение параметра](../../relational-databases/native-client-odbc-table-valued-parameters/additional-table-valued-parameter-metadata.md)  
 Описывает, как использовать SQLColumns, SQLProcedureColumns и SQLTables для получения метаданных возвращающего табличное значение параметра.  
  
 [Ошибки и предупреждения преобразования данных возвращающих табличное значение параметров и другие](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameter-data-conversion-and-other-errors-and-warnings.md)  
 Описывает, как обрабатывать ошибки в значениях столбцов с возвращающими табличное значение параметрами.  
  
 [Совместимость версий](../../relational-databases/native-client-odbc-table-valued-parameters/cross-version-compatibility.md)  
 Описывает конфликты, которые могут возникать при использовании возвращающих табличное значение параметров клиентом или сервером версии более ранней, чем [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].  
  
 [Сводка по API-интерфейсам возвращающих табличное значение параметров ODBC](../../relational-databases/native-client-odbc-table-valued-parameters/odbc-table-valued-parameter-api-summary.md)  
 Приводит перечень функций ODBC, которые поддерживают возвращающие табличное значение параметры.  
  
 [Примеры программирования с использованием ODBC табличное значение параметра](http://msdn.microsoft.com/library/3f52b7a7-f2bd-4455-b79e-d015fb397726)  
 Описывает, как следует выполнять типичные задачи.  
  
## <a name="see-also"></a>См. также  
 [Собственный клиент SQL Server &#40; ODBC &#41;](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)   
 [Возвращающие табличные значения параметры &#40; Собственный клиент SQL Server &#41;](../../relational-databases/native-client/features/table-valued-parameters-sql-server-native-client.md)  
  
  