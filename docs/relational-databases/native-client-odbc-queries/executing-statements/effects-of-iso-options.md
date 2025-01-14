---
title: Влияние параметров ISO | Документация Майкрософт
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ISO options (ODBC)
- ODBC applications, ISO options
- ODBC applications, statements
- SQL Server Native Client ODBC driver, ISO options
- statements [ODBC], ISO options
ms.assetid: 813f1397-fa0b-45ec-a718-e13fe2fb88ac
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 43347e4fcf517dc52c8791dc81220a8990e1655d
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/07/2019
ms.locfileid: "73779867"
---
# <a name="effects-of-iso-options"></a>Действие параметров ISO
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Стандарт ODBC близок к стандарту ISO, а приложения ODBC ожидают стандартного поведения от драйвера ODBC. Чтобы обеспечить более тесное соответствие поведения, определенного в стандарте ODBC, драйвер ODBC для собственного клиента [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] всегда использует любые параметры ISO, доступные в версии SQL Server, с которой он подключается.  
  
 Когда драйвер ODBC для собственного клиента [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] подключается к экземпляру [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], сервер обнаруживает, что клиент использует драйвер ODBC [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, и устанавливает несколько параметров в.  
  
 Драйвер сам формирует эти инструкции; ODBC-приложение не посылает для этого никаких запросов. Установка этих параметров позволяет ODBC-приложениям, использующим драйвер, иметь лучшую переносимость, поскольку в этом случае поведение сервера более соответствует стандарту ISO.  
  
 Приложения на основе DB-Library обычно не вызывают включение этих параметров. Сайты, отслеживающие различные режимы работы клиентов ODBC или DB-Library при выполнении одной и той же инструкции SQL, не предполагают, что это указывает на проблему с драйвером ODBC для собственного клиента [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Они должны сначала перезапустить инструкцию в среде DB-Library с теми же параметрами SET, которые будут использоваться драйвером ODBC для собственного клиента [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 Поскольку пользователи и приложения могут в любое время включать и выключать параметры из набора SET, разработчики хранимых процедур и триггеров должны проводить тестирование своих процедур и триггеров как со включенными, так и с отключенными параметрами из этого набора. Это гарантирует, что триггеры и процедуры будут правильно работать независимо от того, какие параметры конкретное соединение установит при вызове триггера или процедуры. Если для работы триггера или хранимой процедуры требуется конкретное значение одного из этих параметров, инструкцию SET следует выполнить в начале триггера или хранимой процедуры. Она сохраняет силу только до завершения триггера или хранимой процедуры; после этого восстанавливается первоначальное значение параметра.  
  
 При подключении к экземпляру [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] устанавливается также четвертый параметр SET, CONCAT_NULL_YIELDS_NULL. Драйвер ODBC для собственного клиента [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] не устанавливает эти параметры в случае, если Ансинпв = NO указано в источнике данных или в [SQLDriverConnect](../../../relational-databases/native-client-odbc-api/sqldriverconnect.md) или [SQLBrowseConnect](../../../relational-databases/native-client-odbc-api/sqlbrowseconnect.md).  
  
 Как и параметры ISO, указанные ранее, драйвер ODBC для собственного клиента [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] не включает параметр QUOTED_IDENTIFIER в случае, если Куотедид = NO указано в источнике данных или в **SQLDriverConnect** или **SQLBrowseConnect**.  
  
 Чтобы драйвер мог узнавать текущие значения параметров SET, ODBC-приложения не должны задавать эти параметры с помощью инструкции языка [!INCLUDE[tsql](../../../includes/tsql-md.md)] SET. Они могут задавать их только через параметры источника данных или соединения. Если приложение запускает инструкции SET, то инструкции SQL, создаваемые драйвером, могут быть неверными.  
  
## <a name="see-also"></a>См. также раздел  
 [Выполняются инструкции &#40;ODBC&#41; ](../../../relational-databases/native-client-odbc-queries/executing-statements/executing-statements-odbc.md)   
 [SQLDriverConnect](../../../relational-databases/native-client-odbc-api/sqldriverconnect.md)   
 [SQLBrowseConnect](../../../relational-databases/native-client-odbc-api/sqlbrowseconnect.md)  
  
  
