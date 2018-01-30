---
title: "Преобразования из C в SQL | Документы Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-date-time
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords: conversions [ODBC], C to SQL
ms.assetid: 7ac098db-9147-4883-8da9-a58ab24a0d31
caps.latest.revision: "35"
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: de47b5b75d0823d7cae56db844a1d84bbac25f2f
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/25/2018
---
# <a name="datetime-data-type-conversions-from-c-to-sql"></a>Преобразование типов данных из C SQL DateTime
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  В этом разделе перечислены проблемы, которые следует учитывать при преобразовании типов C [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] типы даты и времени.  
  
 Преобразования, описанные в следующей таблице, относятся к преобразованиям, совершаемым на клиенте. В случаях, когда клиент задает точность в долях секунды для параметра, отличающуюся от определенной на сервере, клиентское преобразование может завершиться успешно, но сервер вернет ошибку при **SQLExecute** или  **SQLExecuteDirect** вызывается. В частности, ODBC рассматривает любое усечение долей секунды как ошибку, тогда как [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] округляет; например, округление выполняется при переходе от **datetime2(6)** для **datetime2(2)**. Значения столбцов даты-времени округляются до 1/300 секунды, а в значениях типа smalldatetime сервер устанавливает для секунд значение, равное нулю.  
  
|||||||||  
|-|-|-|-|-|-|-|-|  
||SQL_TYPE_DATE|SQL_TYPE_TIME|SQL_SS_TIME2|SQL_TYPE_TIMESTAMP|SQL_SS_TIMSTAMPOFFSET|SQL_CHAR|SQL_WCHAR|  
|SQL_C_DATE|1|-|-|1,6|1,5,6|1,13|1,13|  
|SQL_C_TIME|-|1|1|1,7|1,5,7|1,13|1,13|  
|SQL_C_SS_TIME2|-|1,3|1,10|1,7|1,5,7|1,13|1,13|  
|SQL_C_BINARY(SQL_SS_TIME2_STRUCT)|Недоступно|Недоступно|1,10,11|Недоступно|Недоступно|Недоступно|Недоступно|  
|SQL_C_TYPE_TIMESTAMP|1,2|1,3,4|1,4,10|1,10|1,5,10|1,13|1,13|  
|SQL_C_SS_TIMESTAMPOFFSET|1,2,8|1,3,4,8|1,4,8,10|1,8,10|1,10|1,13|1,13|  
|SQL_C_BINARY(SQL_SS_TIMESTAMPOFFSET_STRUCT)|Недоступно|Недоступно|Недоступно|Недоступно|1,10,11|Недоступно|Недоступно|  
|SQL_C_CHAR/SQL_WCHAR (date)|9|9|9|9,6|9,5,6|Недоступно|Недоступно|  
|SQL_C_CHAR/SQL_WCHAR (time2)|9|9,3|9,10|9,7,10|9,5,7,10|Недоступно|Недоступно|  
|SQL_C_CHAR/SQL_WCHAR (datetime)|9,2|9,3,4|9,4,10|9,10|9,5,10|Недоступно|Недоступно|  
|SQL_C_CHAR/SQL_WCHAR (datetimeoffset)|9,2,8|9,3,4,8|9,4,8,10|9,8,10|9,10|Недоступно|Недоступно|  
|SQL_C_BINARY(SQL_DATE_STRUCT)|1,11|Недоступно|Недоступно|Недоступно|Недоступно|Недоступно|Недоступно|  
|SQL_C_BINARY(SQL_TIME_STRUCT)|Недоступно|Недоступно|Недоступно|Недоступно|Недоступно|Недоступно|Недоступно|  
|SQL_C_BINARY(SQL_TIMESTAMP_STRUCT)|Недоступно|Недоступно|Недоступно|Недоступно|Недоступно|Недоступно|Недоступно|  
  
## <a name="key-to-symbols"></a>Расшифровка символов  
  
-   **-**: Преобразование не поддерживается. Создается запись диагностики с кодом SQLSTATE 07006 и сообщением «Нарушение атрибута ограниченного типа данных».  
  
-   **1**: Если данных, является недопустимым, создается диагностическая запись создается с кодом SQLSTATE 22007 и сообщением «недопустимое значение datetime формат».  
  
-   **2**: поля времени должны быть равны нулю, или создается запись диагностики с кодом SQLSTATE 22008 и сообщением «Частичное усечение».  
  
-   **3**: доли секунды должны быть равны нулю, или создается запись диагностики с кодом SQLSTATE 22008 и сообщением «Частичное усечение».  
  
-   **4**: компонент даты учитывается.  
  
-   **5**: часовой пояс устанавливается с часовым поясом клиента.  
  
-   **6**: время устанавливается равным нулю.  
  
-   **7**: дата устанавливается в текущую дату.  
  
-   **8**: время приводится от часового пояса клиента в формате UTC. Если во время этого преобразования возникла ошибка, создается запись диагностики с кодом SQLSTATE 22008 и сообщением «Переполнение поля datetime».  
  
-   **9**: строка анализируется и преобразуется в даты, datetime, datetimeoffset или значения времени, в зависимости от первого встреченного знака препинания и наличия остальных компонентов. Затем строка преобразуется в целевой тип согласно правилам, описанным в приведенной выше таблице для типа исходных данных, который выясняется в процессе анализа. Если во время синтаксического анализа обнаружена ошибка, то создается диагностическая запись с кодом SQLSTATE 22018 и сообщением «Недопустимое значение символа для спецификации преобразования». Для параметров типа datetime и smalldatetime, если значение года выходит за пределы допустимого диапазона, создается диагностическая запись с кодом SQLSTATE 22007 и сообщением «Недопустимый формат даты и времени».  
  
     Значение datetimeoffset после преобразования во времени в формате UTC должно находиться в пределах диапазона, даже если преобразование во времени в формате UTC не требуется. Причина этого заключается в том, что поток табличных данных и сервер всегда нормализуют время в значениях datetimeoffset для времени в формате UTC, поэтому клиент должен проверять, что значение времени после преобразования во времени в формате UTC находится в пределах поддерживаемого диапазона. Если переданы недопустимые для поддерживаемого диапазона времени в формате UTC данные, то создается диагностическая запись с кодом SQLSTATE 22007 и сообщением «Недопустимый формат даты и времени».  
  
-   **10**: Если происходит усечение с потерей данных, то диагностики создается запись с кодом SQLSTATE 22008 и сообщением «недопустимый формат времени». Эта ошибка также возникает в том случае, если значение выходит за пределы диапазона, который может быть представлен диапазоном времени в формате UTC, используемым сервером.  
  
-   **11**: Если байтовая длина данных равен размеру структуры, нужной для данного типа SQL, с ошибкой SQLSTATE 22003 и сообщением «Численное значение вне допустимого диапазона» создается запись диагностики.  
  
-   **12**: Если байтовая длина данных равна 4 или 8, данные отправляются на сервер в необработанном формате smalldatetime или datetime TDS. Если байтовая длина данных в точности равна размеру структуры SQL_TIMESTAMP_STRUCT, данные преобразуются в формат потока табличных данных для типа datetime2.  
  
-   **13**: Если происходит усечение с потерей данных, то диагностики создается запись с кодом SQLSTATE 22001 и сообщением «Строковые данные, усечение справа».  
  
     Число разрядов для дробной секунды (масштаб) определяется размером целевого столбца согласно следующей таблице.  
  
    ||||  
    |-|-|-|  
    |Тип|Подразумеваемый масштаб<br /><br /> 0|Подразумеваемый масштаб<br /><br /> 1..9|  
    |SQL_C_TYPE_TIMESTAMP|19|21..29|  
  
     Однако для типа SQL_C_TYPE_TIMESTAMP, если доли секунды можно представить в трех разрядах без потери данных, и размер столбца больше или равен 23, для дробной доли секунды создаются ровно три разряда. Это поведение обеспечивает обратную совместимость с приложениями, разработанными в расчете на более старые драйверы ODBC.  
  
     Для размеров столбцов, превышающих диапазон таблицы, подразумевается масштаб 9. Это преобразование должно учитывать доли секунд с точностью до девяти значащих цифр — максимум, поддерживаемый ODBC.  
  
     Если для столбца установлен размер, равный нулю, в ODBC это означает неограниченный размер для символьных типов переменной длины (9 разрядов там, где не работает правило трех разрядов для типа SQL_C_TYPE_TIMESTAMP). Задать размер столбца, равный нулю, для символьных типов фиксированной длины будет ошибкой.  
  
-   **Н/д**: существующий [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] и более ранних версий сохранен.  
  
## <a name="see-also"></a>См. также  
 [Дата и время усовершенствования &#40; ODBC &#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)  
  
  