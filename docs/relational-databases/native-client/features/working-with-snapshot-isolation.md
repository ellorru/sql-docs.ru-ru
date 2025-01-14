---
title: Работа с изоляцией моментальных снимков | Документация Майкрософт
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- data access [SQL Server Native Client], snapshot isolation
- SQLNCLI, snapshot isolation
- isolation levels [SQL Server], snapshot
- DBPROPSET_SESSION property set
- DBDROPSET_DATASOURCEINFO property set
- snapshot isolation [SQL Server Native Client]
- SQL Server Native Client OLE DB provider, snapshot isolation
- SQL Server Native Client ODBC driver, snapshot isolation
- SQL Server Native Client, snapshot isolation
- SQLGetInfo function
- concurrency [SQL Server Native Client]
- SQLSetConnectAttr function
ms.assetid: 39e87eb1-677e-45dd-bc61-83a4025a7756
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 502c36c0d4793a28cb3f9db631d9544ab8467bcf
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/07/2019
ms.locfileid: "73761274"
---
# <a name="working-with-snapshot-isolation"></a>Работа с изоляцией моментального снимка
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  В [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] появился новый уровень изоляции «моментального снимка», предназначенный для повышения параллелизма приложений оперативной обработки транзакций (OLTP). В предыдущих версиях [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] параллелизм был основан исключительно на блокировках, что могло вызвать проблемы с блокировками и взаимоблокировками для некоторых приложений. Изоляция моментального снимка зависит от расширений управления версиями строк и предназначена для улучшения производительности путем исключения сценариев блокировки модулей чтения или записи.  
  
 Транзакции, запускаемые в режиме изоляции моментальных снимков, читают моментальный снимок базы данных на момент запуска транзакции. Один из результатов состоит в том, что поведение набора ключей, динамических и статических серверных курсоров, открываемых в контексте транзакции моментальных снимков, более походит на статические курсоры, открытые в сериализуемых транзакциях. Однако, когда курсоры открыты на уровне изоляции моментальных снимков, блокировки не применяются, что может снизить блокирование на сервере.  
  
## <a name="sql-server-native-client-ole-db-provider"></a>Поставщик OLE DB для собственного клиента SQL Server  
 Поставщик [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB обладает улучшениями, которые используют преимущества изоляции моментального снимка, представленной в [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]. Среди этих улучшений изменения наборов свойств DBPROPSET_DATASOURCEINFO и DBPROPSET_SESSION.  
  
### <a name="dbpropset_datasourceinfo"></a>DBPROPSET_DATASOURCEINFO  
 Набор свойств DBPROPSET_DATASOURCEINFO изменен и указывает на поддержку уровня изоляции моментальных снимков благодаря добавлению значения DBPROPVAL_TI_SNAPSHOT, используемого в свойстве DBPROP_SUPPORTEDTXNISOLEVELS. Это новое значение указывает, что уровень изоляции моментального снимка поддерживается независимо от того, включено ли в базе данных управление версиями. Ниже приведен список значений DBPROP_SUPPORTEDTXNISOLEVELS.  
  
|Идентификатор свойства|Описание|  
|-----------------|-----------------|  
|DBPROP_SUPPORTEDTXNISOLEVELS|Тип: VT_I4<br /><br /> R/W: только для чтения<br /><br /> Описание: битовая маска, указывающая поддерживаемые уровни изоляции транзакции. Сочетание может включать нуль или несколько следующих значений:<br /><br /> DBPROPVAL_TI_CHAOS<br /><br /> DBPROPVAL_TI_READUNCOMMITTED<br /><br /> DBPROPVAL_TI_BROWSE<br /><br /> DBPROPVAL_TI_CURSORSTABILITY<br /><br /> DBPROPVAL_TI_READCOMMITTED<br /><br /> DBPROPVAL_TI_REPEATABLEREAD<br /><br /> DBPROPVAL_TI_SERIALIZABLE<br /><br /> DBPROPVAL_TI_ISOLATED<br /><br /> DBPROPVAL_TI_SNAPSHOT|  
  
### <a name="dbpropset_session"></a>Набор свойств DBPROPSET_SESSION  
 Набор свойств DBPROPSET_SESSION изменен и указывает на поддержку уровня изоляции моментальных снимков благодаря добавлению значения DBPROPVAL_TI_SNAPSHOT, используемого в свойстве DBPROP_SESS_AUTOCOMMITISOLEVELS. Это новое значение указывает, что уровень изоляции моментального снимка поддерживается независимо от того, включено ли в базе данных управление версиями. Ниже приведен список значений DBPROP_SESS_AUTOCOMMITISOLEVELS.  
  
|Идентификатор свойства|Описание|  
|-----------------|-----------------|  
|DBPROP_SESS_AUTOCOMMITISOLEVELS|Тип: VT_I4<br /><br /> R/W: только для чтения<br /><br /> Описание: задает битовую маску, которая указывает уровень изоляции транзакции в режиме автоматической фиксации. Значения, которые можно установить в этой битовой маске, такие же, как устанавливаемые для DBPROP_SUPPORTEDTXNISOLEVELS.|  
  
> [!NOTE]  
>  Ошибки DB_S_ERRORSOCCURRED или DB_E_ERRORSOCCURRED происходят, если значение DBPROPVAL_TI_SNAPSHOT установлено при использовании версий [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], предшествующих [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].  
  
 Сведения о поддержке изоляции моментальных снимков в транзакциях см. в разделе [Поддержка локальных транзакций](../../../relational-databases/native-client-ole-db-transactions/supporting-local-transactions.md).  
  
## <a name="sql-server-native-client-odbc-driver"></a>Драйвер ODBC для собственного клиента SQL Server  
 Драйвер ODBC для собственного клиента [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] поддерживает изоляцию моментальных снимков, а также усовершенствования функций [SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) и [SQLGetInfo](../../../relational-databases/native-client-odbc-api/sqlgetinfo.md) .  
  
### <a name="sqlsetconnectattr"></a>SQLSetConnectAttr  
 Функция **SQLSetConnectAttr** теперь поддерживает использование атрибута SQL_COPT_SS_TXN_ISOLATION. Задание SQL_COPT_SS_TXN_ISOLATION значения SQL_TXN_SS_SNAPSHOT указывает, что транзакция произойдет на уровне изоляции моментального снимка.  
  
### <a name="sqlgetinfo"></a>SQLGetInfo  
 Функция [SQLGetInfo](../../../relational-databases/native-client-odbc-api/sqlgetinfo.md) теперь поддерживает SQL_TXN_SS_SNAPSHOT значение, добавленное в тип сведений SQL_TXN_ISOLATION_OPTION.  
  
 Сведения о поддержке изоляции моментальных снимков в транзакциях см. в разделе [уровень изоляции транзакций курсора](../../../relational-databases/native-client-odbc-cursors/properties/cursor-transaction-isolation-level.md).  
  
## <a name="see-also"></a>См. также раздел  
 [Компоненты собственного клиента SQL Server](../../../relational-databases/native-client/features/sql-server-native-client-features.md)   
 [Свойства и поведение наборов строк](../../../relational-databases/native-client-ole-db-rowsets/rowset-properties-and-behaviors.md)  
  
  
