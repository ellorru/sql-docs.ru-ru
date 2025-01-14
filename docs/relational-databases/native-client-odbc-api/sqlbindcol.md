---
title: SQLBindCol | Документация Майкрософт
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLBindCol function
ms.assetid: fbd7ba20-d917-4ca9-b018-018ac6af9f98
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4a92c95a67b6e9fd3d31917af4f5b7b19f4c613d
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/07/2019
ms.locfileid: "73787791"
---
# <a name="sqlbindcol"></a>SQLBindCol
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Как правило, следует рассмотреть последствия использования **SQLBindCol** для преобразования данных. Преобразования привязки являются клиентскими процессами, поэтому, например, получение значения с плавающей запятой, связанного с символьным столбцом, вынуждает драйвер выполнить локальное преобразование «плавающая запятая в символ» при выборке строки. Функция [!INCLUDE[tsql](../../includes/tsql-md.md)] CONVERT может использоваться для размещения затрат преобразования данных на сервере.  
  
 Экземпляр [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] может возвращать несколько результирующих наборов для одной инструкции. Каждый результирующий набор должен быть привязан отдельно. Дополнительные сведения о привязке для нескольких результирующих наборов см. в разделе [SQLMoreResults](../../relational-databases/native-client-odbc-api/sqlmoreresults.md).  
  
 Разработчик может привязать столбцы к [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ным типам данных C, используя значение *TargetType* **SQL_C_BINARY**. Столбцы, привязанные к типам, зависящим от служб [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], не могут быть перенесены. Определенные типы данных ODBC языка C, зависящие от [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], совпадают с определениями типов для DB-Library, и разработчики приложений переноса DB-Library могут воспользоваться этой возможностью.  
  
 Усечение данных отчетов — это дорогостоящий процесс для драйвера ODBC для собственного клиента [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Усечения можно избежать с помощью гарантии того, что все буферы связанных данных достаточно широки для возвращения данных. Для символьных данных ширина должна включать пространство для признака конца строки при использовании поведения драйвера по умолчанию для завершения строки. Например, привязка столбца [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **char (5)** к массиву из пяти символов приводит к усечению каждого полученного значения. Привязка одинакового столбца к массиву из шести символов позволит избежать усечения путем предоставления элемента символа для хранения признака конца NULL. [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md) можно использовать для эффективного извлечения длинных символьных и двоичных данных без усечения.  
  
 Для типов данных больших значений, если буфер, указанный пользователем, недостаточно велик для хранения всего значения столбца, возвращается **SQL_SUCCESS_WITH_INFO** и строковые данные. предупреждение о правильном усечении. Аргумент **StrLen_or_IndPtr** будет содержать число символов/байт, хранящихся в буфере.  
  
## <a name="sqlbindcol-support-for-enhanced-date-and-time-features"></a>Поддержка функцией SQLBindCol улучшенных возможностей работы с данными в формате даты-времени  
 Значения результирующих столбцов типов даты-времени преобразуются, как описано в статье [преобразования из SQL в C](../../relational-databases/native-client-odbc-date-time/datetime-data-type-conversions-from-sql-to-c.md). Обратите внимание, что для извлечения столбцов Time и DateTimeOffset в виде соответствующих структур (**SQL_SS_TIME2_STRUCT** и **SQL_SS_TIMESTAMPOFFSET_STRUCT**) необходимо указать *TargetType* как **SQL_C_DEFAULT** или **SQL_C_BINARY** .  
  
 Дополнительные сведения см. в разделе [улучшения &#40;даты и времени&#41;ODBC](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqlbindcol-support-for-large-clr-udts"></a>Поддержка функцией SQLBindCol определяемых пользователем типов больших данных CLR  
 **SQLBindCol** поддерживает большие определяемые пользователем типы данных CLR (UDT). Дополнительные сведения см. в разделе [типы больших определяемых пользователем &#40;типов&#41;данных CLR ODBC](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="see-also"></a>См. также раздел  
   [функции SQLBindCol](https://go.microsoft.com/fwlink/?LinkId=59327)  
 [Подробные сведения о реализации API-интерфейсов ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
