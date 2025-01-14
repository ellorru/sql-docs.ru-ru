---
title: Вставка данных в параметры, возвращающие табличное значение | Документация Майкрософт
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters, inserting data into
ms.assetid: 9c1a3234-4675-40d3-b473-8df06208f880
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 61c811b25ffa94f7d635f63375dcc304339872cd
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/07/2019
ms.locfileid: "73788691"
---
# <a name="inserting-data-into-table-valued-parameters"></a>Вставка данных в параметры, возвращающие табличные значения
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Поставщик [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB поддерживает две модели для указания данных для строк параметров, возвращающих табличное значение: модель push-уведомлений и модель извлечения. Образец, в котором демонстрируется применение модели по запросу, см. в разделе [Образцы программирования служб SQL Server](https://msftdpprodsamples.codeplex.com/).  
  
> [!NOTE]  
>  Столбец возвращающего табличное значение параметра должен содержать во всех строках либо значения по умолчанию, либо значения, отличные от значений по умолчанию. Нельзя, чтобы в одних строках были значения по умолчанию, а в других — значения, отличные от них. Следовательно, в привязках табличных параметров единственными значениями состояния, разрешенными для столбца набора строк возвращающего табличное значение параметра, являются DBSTATUS_S_ISNULL и DBSTATUS_S_OK. Значение DBSTATUS_S_DEFAULT приведет к сбою, и значению состояния привязки будет присвоено значение DBSTATUS_E_BADSTATUS.  
  
## <a name="push-model-loads-all-table-valued-paremeter-data-in-memory"></a>Принудительная модель (загружает все данные табличного параметра в память)  
 Принудительная модель напоминает использование наборов параметров (то есть параметра DBPARAMS в методе ICommand::Execute). Принудительная модель используется только в том случае, если объекты набора строк возвращающего табличное значение параметра применяются без пользовательской реализации интерфейсов IRowset. Принудительная модель рекомендуется в том случае, если набор строк возвращающего табличное значение параметра содержит небольшое число строк и не потребует от приложения большого объема памяти. Эта модель проще, поскольку она не нуждается в больших возможностях приложения потребителя, довольствуясь стандартными возможностями приложений OLE DB.  
  
 Ожидается, что перед выполнением команды потребитель предоставит поставщику все данные для возвращающего табличное значение параметра. Для этого он заполняет объект набора строк табличного параметра для каждого возвращающего табличное значение параметра. Объект набора строк возвращающего табличное значение параметра реализует для набора строк операции Insert, Set и Delete, которые потребитель будет использовать для обработки данных возвращающего табличное значение параметра. Поставщик получает данные из объекта набора строк возвращающего табличное значение параметра во время выполнения.  
  
 Как только набор строк возвращающего табличное значение параметра предоставляется потребителю, он может начать работу с ним как с набором строк. Потребитель может получить сведения о типе каждого столбца (тип, максимальная длина, точность и масштаб) с помощью метода интерфейса IColumnsInfo:: GetColumnInfo или IColumnsRowset:: Жетколумнсровсет. После этого потребитель создает метод доступа для определения привязок для данных. Следующий шаг — вставка строк данных в набор строк возвращающего табличное значение параметра. Это можно сделать с помощью IRowsetChange:: InsertRow. IRowsetChange:: SetData или IRowsetChange::D Елетеровс также можно использовать в объекте набора строк возвращающего табличное значение параметра, если требуется манипулировать данными. Для объекта набора строк возвращающего табличное значение параметра имеется счетчик ссылок, как и у объектов потока.  
  
 Если используется IColumnsRowset:: Жетколумнсровсет, будут выполняться последующие вызовы методов IRowset:: GetNextRows, IRowset:: GetData и IRowset:: ReleaseRows для объекта набора строк результирующего столбца.  
  
 После того, как поставщик OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client начинает выполнять команду, значения возвращающего табличное значение параметра будут получены из объекта набора строк возвращающего табличное значений параметра и отправлены на сервер.  
  
 Принудительная модель требует минимальных затрат от потребителя, но использует больше памяти, чем модель по запросу, поскольку все данные возвращающего табличное значение параметра во время выполнения приходится хранить в памяти.  
  
## <a name="pull-model-obtaining-table-valued-parameter-data-on-demand-from-the-consumer"></a>Модель «по запросу» (получает данные возвращающего табличное значение параметра по запросу потребителя)  
 Применение модели по запросу выгодно в следующих двух случаях.  
  
-   Для создания потока строк.  
  
-   Если в качестве значения возвращающего табличное значение параметра используется набор строк от другого поставщика.  
  
 В модели получения по запросу заказчик предоставляет данные поставщику по запросу. Этот подход следует использовать в том случае, если приложение реализует множество операций вставки и хранение набора строк возвращающего табличное значение параметра потребовало бы большого объема памяти. Если используются несколько поставщиков OLE DB, то модель по запросу позволяет потребителю предоставлять любые объекты наборов строк в качестве значения возвращающего табличное значение параметра.  
  
 Для применения модели по запросу потребитель должен предоставить собственную реализацию объекта набора строк. При использовании модели извлечения с наборами строк возвращающего табличное значение параметра (CLSID_ROWSET_TVP) потребитель должен выполнить статистическую обработку объекта набора строк возвращающего табличное значение параметра, который поставщик предоставляет через Итабледефинитионвисконстраинтс:: Метод Креатетаблевисконстраинтс или метод IOpenRowset:: OpenRowset. Ожидается, что объект потребителя переопределяет только реализацию интерфейса IRowset. Должны быть переопределены следующие функции.  
  
-   IRowset::GetNextRows  
  
-   IRowset:: Аддрефровс  
  
-   IRowset:: GetData  
  
-   IRowset:: ReleaseRows  
  
-   IRowset:: свойство RestartPosition  
  
 Поставщик OLE DB для собственного клиента [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] считывает одновременно одну или несколько строк из объекта набора строк потребителя для поддержки потокового поведения возвращающих табличное значение параметров. Например, пользователь может иметь данные набора строк возвращающего табличное значение параметра на диске (а не в памяти) и реализовать считывание данных с диска, если это требуется поставщиком OLE DB для собственного клиента [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Потребитель будет передавать свой формат данных [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] поставщику OLE DB собственного клиента с помощью IAccessor:: CreateAccessor в объекте набора строк возвращающего табличное значение параметра. При считывании данных из буфера потребителя поставщик удостоверяется, что все изменяемые столбцы со значениями, отличающимися от значений по умолчанию, доступны хотя бы через один дескриптор метода доступа и использует соответствующие дескрипторы для считывания данных столбца. Чтобы избежать неоднозначности, между столбцом набора строк возвращающего табличное значение параметра и привязкой должно быть однозначное соответствие. Повторяющиеся привязки к одному и тому же столбцу приведут к ошибке. Кроме того, каждый метод доступа должен иметь *иординал* элемент дббиндингс в последовательности. Метод IRowset::GetData будет вызываться ровно столько раз, сколько существует методов доступа для одной строки, а порядок вызовов определяется порядком возрастания значений *iOrdinal*.  
  
 Ожидается, что поставщик реализует большую часть интерфейсов, предоставляемых объектом набора строк возвращающего табличное значение параметра. Потребитель реализует объект набора строк с минимальным количеством интерфейсов (IRowset). Благодаря передаче интерфейсов вслепую оставшиеся интерфейсы объекта набора строк реализуются объектом набора строк возвращающего табличное значение параметра.  
  
 Для всех остальных объектов набора строк (например, получаемых для поставщиков OLE DB), предоставленный потребителем набор строк должен реализовать все обязательные интерфейсы объектов набора строк, как указано в спецификации OLE DB.  
  
 Во время выполнения поставщик OLE DB для собственного клиента [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] выполняет обратный вызов объекта набора строк для выборки строк и считывания данных столбца.  
  
## <a name="see-also"></a>См. также раздел  
 [Возвращающие табличные значения параметры &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)   
 [Использование возвращающих табличные значения параметров &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
