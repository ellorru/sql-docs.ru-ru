---
title: "SQLGetTypeInfo | Документы Microsoft"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-api
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apitype: DLLExport
helpviewer_keywords: SQLGetTypeInfo function
ms.assetid: 13b982c3-ae03-4155-bc0d-e225050703ce
caps.latest.revision: "47"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c950f577efe8f0a056b86579a8b21c43763b4972
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/17/2017
---
# <a name="sqlgettypeinfo"></a>SQLGetTypeInfo
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Дополнительный столбец USERTYPE в результирующий набор отчетов драйвер ODBC для собственного клиента **SQLGetTypeInfo**. USERTYPE возвращает определение типа данных DB-Library. Этот столбец полезен разработчикам, которые переносят существующие приложения DB-Library в ODBC.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] рассматривает идентификатор как атрибут, а в ODBC он считается типом данных. Чтобы устранить это несоответствие **SQLGetTypeInfo** возвращает типы данных: **intidentity**, **smallintidentity**, **tinyintidentity**, **decimalidentity**, и **numericidentity**. **SQLGetTypeInfo** столбец результирующего набора AUTO_UNIQUE_VALUE сообщает значение TRUE для типов данных.  
  
 Для **varchar**, **nvarchar** и **varbinary**, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] продолжает отчета 8000, 4000 и 8000 соответственно для COLUMN_SIZE драйвер ODBC собственного клиента значение, несмотря на то, что фактически неограничен. Это делается в целях обратной совместимости.  
  
 Для **xml** тип данных [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] драйвер ODBC собственного клиента возвращает значение SQL_SS_LENGTH_UNLIMITED для COLUMN_SIZE для указания неограниченного размера.  
  
## <a name="sqlgettypeinfo-and-table-valued-parameters"></a>SQLGetTypeInfo и параметры, возвращающие табличные значения  
 Табличный тип для возвращающих табличные значения параметров фактически является метатипом, то есть типом, используемым для определения других типов. Таким образом он не имеет через SQLGetTypeInfo. Приложения должны использовать SQLTables, а не SQLGetTypeInfo, для получения метаданных для табличных типов при использовании возвращающих табличные значения параметров.  
  
 Дополнительные сведения о получении метаданных для возвращающих табличное значение параметров в разделе [инструкции атрибуты параметров, Affect Table-Valued](../../relational-databases/native-client-odbc-table-valued-parameters/statement-attributes-that-affect-table-valued-parameters.md).  
  
 Дополнительные сведения о возвращающих табличные значения параметров см. в разделе [табличное значение параметры &#40; ODBC &#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="sqlgettypeinfo-support-for-enhanced-date-and-time-features"></a>Поддержка SQLGetTypeInfo для улучшенных функций даты-времени  
 Значения, возвращаемые для типов даты и времени, в разделе [метаданные каталога](../../relational-databases/native-client-odbc-date-time/metadata-catalog.md).  
  
 Дополнительные общие сведения см. в разделе [даты и времени усовершенствования &#40; ODBC &#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqlgettypeinfo-support-for-large-clr-udts"></a>Поддержка SQLGetTypeInfo для больших определяемых пользователем типов данных среды CLR  
 **SQLGetTypeInfo** поддерживает большие определяемые пользователем типы (UDT). Дополнительные сведения см. в разделе [Large CLR User-Defined типы &#40; ODBC &#41;](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="see-also"></a>См. также:  
 [Функция SQLGetTypeInfo](http://go.microsoft.com/fwlink/?LinkId=59356)   
 [Подробные сведения о реализации API-интерфейсов ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  