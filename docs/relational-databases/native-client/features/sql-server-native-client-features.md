---
title: SQL Server Native Client компонентов | Документация Майкрософт
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- MDAC [SQL Server]
- SQL Server Native Client ODBC driver, about SQL Server Native Client ODBC driver
- SQLNCLI, about SQL Server Native Client
- data access [SQL Server Native Client], features
ms.assetid: 7bb32865-5afb-41ab-98b4-3fa545ee8953
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8821a8c0c0ef095d46682e0e1ad07e1cd74be16b
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/07/2019
ms.locfileid: "73761320"
---
# <a name="sql-server-native-client-features"></a>Компоненты собственного клиента SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Помимо возможностей компонентов доступа к данным WDAC (ранее MDAC), в собственном клиенте [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] реализовано множество других функций, позволяющих пользоваться функциональностью [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="in-this-section"></a>В этом разделе  
 [Изменение поведения драйвера ODBC при обработке преобразования символов](../../../relational-databases/native-client/features/odbc-driver-behavior-change-when-handling-character-conversions.md)  
 Описание изменения поведения, реализованного с версии Native Client [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 2012.  
  
 [Использование зеркального отображения базы данных](../../../relational-databases/native-client/features/using-database-mirroring.md)  
 Описывает, как [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client поддерживает использование зеркальных баз данных, то есть возможность сохранения копии или зеркала базы данных [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] на резервном сервере.  
  
 [Выполнение асинхронных операций](../../../relational-databases/native-client/features/performing-asynchronous-operations.md)  
 Обсуждение поддержки собственным клиентом [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] асинхронных операций, то есть способности немедленно возвращать управление, не блокируя вызывающий поток.  
  
 [Использование множественных активных результирующих наборов (MARS)](../../../relational-databases/native-client/features/using-multiple-active-result-sets-mars.md)  
 Обсуждение поддержки собственным клиентом [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] режима MARS. Режим MARS позволяет выполнять и получать несколько результирующих наборов через одно подключение к базе данных.  
  
 [Использование типов данных XML](../../../relational-databases/native-client/features/using-xml-data-types.md)  
 Обсуждение поддержки собственным клиентом [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] типа данных XML (представляющего собой тип данных на основе XML), который можно использовать как тип столбца, переменной, параметра или значения, возвращаемого функцией.  
  
 [Использование определяемых пользователем типов](../../../relational-databases/native-client/features/using-user-defined-types.md)  
 Описывает, как [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] собственный клиент поддерживает определяемые пользователем типы, которые расширяют систему типов SQL, позволяя сохранять объекты и пользовательские структуры данных в базе данных [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 [Использование типов больших значений](../../../relational-databases/native-client/features/using-large-value-types.md)  
 Обсуждение поддержки собственным клиентом [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] типов данных больших значений, то есть типов данных больших объектов (LOB).  
  
 [Смена пароля программным способом](../../../relational-databases/native-client/features/changing-passwords-programmatically.md)  
 Обсуждение поддержки собственным клиентом [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] управления истекшими паролями с возможностью сменить пароль на клиенте без вмешательства администратора.  
  
 [Работа с изоляцией моментального снимка](../../../relational-databases/native-client/features/working-with-snapshot-isolation.md)  
 Обсуждение поддержки собственным клиентом [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] расширений управления версиями строк, предназначенных для улучшения производительности путем исключения сценариев блокировки модулей чтения или записи.  
  
 [Работа с уведомлениями запросов](../../../relational-databases/native-client/features/working-with-query-notifications.md)  
 Обсуждение поддержки собственным клиентом [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] уведомления потребителя об изменении набора строк.  
  
 [Выполнение операций массового копирования](../../../relational-databases/native-client/features/performing-bulk-copy-operations.md)  
 Описывает, как [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] собственный клиент поддерживает операции с массовым копированием, которые позволяют передавать большие объемы данных в таблицу или представление [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 [Использование шифрования без проверки](../../../relational-databases/native-client/features/using-encryption-without-validation.md)  
 Обсуждение использования собственного клиента [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] для шифрования данных, передаваемых на сервер, без проверки сертификата.  
  
 [Возвращающие табличное значение параметры &#40;SQL Server Native Client&#41;](../../../relational-databases/native-client/features/table-valued-parameters-sql-server-native-client.md)  
 Обсуждение поддержки собственным клиентом [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] возвращающих табличные значения параметров.  
  
 [Большие определяемые пользователем типы данных CLR](../../../relational-databases/native-client/features/large-clr-user-defined-types.md)  
 Обсуждение поддержки определяемых пользователем типов данных среды CLR.  
  
 [Поддержка FILESTREAM](../../../relational-databases/native-client/features/filestream-support.md)  
 Описание [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] поддержки собственного клиента для расширенного компонента FILESTREAM.  
  
 [Поддержка имени субъекта-службы &#40;SPN&#41; в клиентских соединениях](../../../relational-databases/native-client/features/service-principal-name-spn-support-in-client-connections.md)  
 Обсуждение расширенной поддержки имен участника-службы (SPN) для проведения взаимной проверки подлинности по всем протоколам.  
  
 [Поддержка разреженных столбцов в SQL Server Native Client](../../../relational-databases/native-client/features/sparse-columns-support-in-sql-server-native-client.md)  
 Обсуждение поддержки собственным клиентом [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] разреженных столбцов.  
  
 [Улучшения функций даты и времени](../../../relational-databases/native-client/features/date-and-time-improvements.md)  
 Обсуждение поддержки новых типов данных даты и времени, добавленной в собственный клиент [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 [Обнаружение метаданных](../../../relational-databases/native-client/features/metadata-discovery.md)  
 Обсуждение улучшений в механизме обнаружения метаданных, внесенных в [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)].  
  
 [Поддержка UTF-16 в SQL Server Native Client 11.0](../../../relational-databases/native-client/features/utf-16-support-in-sql-server-native-client-11-0.md)  
 Рассматривает изменение поведения, появившееся в [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]. При указании буфера фиксированной длины при привязке результата или выходного параметра столбца, а также если символ **WCHAR** , записанный в буфер перед завершающим символом, является старшим замещающим кодовым точкой суррогатной пары, а следующий параметр **WCHAR** символ является младшим кодом суррогатной точки, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] собственный клиент не добавляет старшую кодовую точку в буфер.  
  
 [Поддержка высокого уровня доступности и аварийного восстановления собственного клиента SQL Server](../../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)  
 Описывается настройка приложения для использования функций высокого уровня доступности и аварийного восстановления, появившихся в [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)].  
  
 [Доступ к диагностическим сведениям в журнале расширенных событий](../../../relational-databases/native-client/features/accessing-diagnostic-information-in-the-extended-events-log.md)  
 Описывает улучшения, реализованные в клиенте [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, и функции отслеживания данных, которые дают доступ к диагностическим данным в кольцевом буфере и журналах XEvents.  
  
 [Поддержка SQL Server Native Client для LocalDB](../../../relational-databases/native-client/features/sql-server-native-client-support-for-localdb.md)  
 Обсуждение поддержки клиентом Native Client [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] улучшенной функции LocalDB.  
  
## <a name="see-also"></a>См. также раздел  
 [SQL Server Native Client  программирования](../../../relational-databases/native-client/sql-server-native-client-programming.md)  
 [Разделы руководства по ODBC](../../../relational-databases/native-client-odbc-how-to/odbc-how-to-topics.md)   
 [Инструкции по OLE DB](../../../relational-databases/native-client-ole-db-how-to/ole-db-how-to-topics.md)   
 [Установка SQL Server Native Client](../../../relational-databases/native-client/applications/installing-sql-server-native-client.md)  
  
  
