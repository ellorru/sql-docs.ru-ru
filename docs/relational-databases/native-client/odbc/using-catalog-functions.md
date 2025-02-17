---
title: Использование функций каталога | Документация Майкрософт
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC, functions
- SQLLinkedCatalogs function
- SQL Server Native Client ODBC driver, catalog functions
- SQLLinkedServers function
- catalog functions [ODBC]
- functions [ODBC]
ms.assetid: 7773fb2e-06b5-4c4b-88e9-0ad9132ad273
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5dbbab122d5789f26d9fd5a6c853be4f5a354a96
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/07/2019
ms.locfileid: "73760333"
---
# <a name="using-catalog-functions"></a>Использование функций каталога
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Все базы данных имеют структуру, содержащую данные, хранящиеся в базе данных. Определение этой структуры вместе с другими сведениями, например разрешениями, хранится в каталоге (реализованном как набор системных таблиц), который называют словарем данных.  
  
 Драйвер ODBC для собственного клиента [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] позволяет приложению определить структуру базы данных с помощью вызовов функций каталога ODBC. Функции каталога возвращают сведения в результирующих наборах и реализуются с помощью запросов хранимых процедур каталога к системным таблицам этого каталога. Например, приложение может запросить результирующий набор, содержащий сведения о всех таблицах в системе или всех столбцах в определенной таблице. Стандартные функции каталога ODBC используются для получения сведений о каталоге из [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], к которому подключено приложение.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] поддерживает распределенные запросы, в которых доступ к нескольким разнородным источникам данных OLE DB осуществляется одним запросом. Одним из методов доступа к удаленному источнику данных OLE DB является определение источника данных как связанного сервера. Это можно сделать с помощью [sp_addlinkedserver](../../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md). После определения связанного сервера на объекты этого сервера могут ссылаться инструкции Transact-SQL, используя четырехкомпонентное имя:  
  
 *linked_server_name. catalog. Schema. object_name*.  
  
 Драйвер ODBC для собственного клиента [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] поддерживает две зависящие от драйвера функции, помогающие получить сведения о каталоге от связанных серверов.  
  
-   **Функция SQLLinkedServers**  
  
     Возвращает список связанных серверов, определенных на локальном сервере.  
  
-   **Функция SQLLinkedCatalogs**  
  
     Возвращает список каталогов, содержащихся на связанном сервере.  
  
 После создания имени связанного сервера и каталога драйвер ODBC для собственного клиента [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] поддерживает получение сведений из каталога, используя имя из двух частей _linked_server_name_ **.** _Каталог_ для *CatalogName* для следующих функций каталога ODBC:  
  
-   **SQLColumnPrivileges**  
  
-   **SQLColumns**  
  
-   **SQLPrimaryKeys**  
  
-   **SQLStatistics**  
  
-   **SQLTablePrivileges**  
  
-   **SQLTables**  
  
 Linked_server_name из двух частей **.** _Каталог_ также поддерживается для *фккаталогнаме* и *пккаталогнаме* на [SQLForeignKeys](../../../relational-databases/native-client-odbc-api/sqlforeignkeys.md).  
  
 Использование SQLLinkedServers и SQLLinkedCatalogs требует следующих файлов.  
  
-   sqlncli.h  
  
     Включает прототипы функций и определения констант для функций каталога связанного сервера. Файл sqlncli.h необходимо включить в приложение ODBC; при компиляции приложения он должен находиться в пути поиска включаемых файлов.  
  
-   sqlncli11.lib  
  
     Должна находиться в пути к библиотекам компоновщика и определена как файл для связывания. Файл sqlncli11.lib поставляется вместе с драйвером ODBC [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.  
  
-   sqlncli11.dll  
  
     Необходима во время выполнения. Файл sqlncli11.dll поставляется вместе с драйвером ODBC [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.  
  
## <a name="see-also"></a>См. также раздел  
 [SQL Server Native Client &#40; &#41; ODBC](../../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
 [SQLColumnPrivileges](../../../relational-databases/native-client-odbc-api/sqlcolumnprivileges.md)   
 [SQLColumns](../../../relational-databases/native-client-odbc-api/sqlcolumns.md)   
 [SQLPrimaryKeys](../../../relational-databases/native-client-odbc-api/sqlprimarykeys.md)   
 [SQLTablePrivileges](../../../relational-databases/native-client-odbc-api/sqltableprivileges.md)   
 [SQLTables](../../../relational-databases/native-client-odbc-api/sqltables.md)   
 [SQLStatistics](../../../relational-databases/native-client-odbc-api/sqlstatistics.md)  
  
  
