---
title: Выполнение асинхронных операций | Документация Майкрософт
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- initialization [SQL Server Native Client]
- database connections [SQL Server Native Client]
- data access [SQL Server Native Client], asynchronous operations
- connections [SQL Server Native Client]
- asynchronous operations [SQL Server Native Client]
- rowsets [SQL Server], initializing
- SQLNCLI, asynchronous operations
- SQL Server Native Client, asynchronous operations
ms.assetid: 8fbd84b4-69cb-4708-9f0f-bbdf69029bcc
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: de08a6ca5e7f68c1a2537eafb6c837085a3ec254
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/07/2019
ms.locfileid: "73761369"
---
# <a name="performing-asynchronous-operations"></a>Выполнение асинхронных операций
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] позволяет приложениям выполнять асинхронные операции с базой данных. Асинхронная обработка позволяет выполнять возврат из методов немедленно, не блокируя вызывающий поток. Это позволяет использовать значительную часть мощности и гибкости многопотоковой обработки, и разработчику при этом не требуется явно создавать потоки или обрабатывать синхронизацию. Приложения запрашивают асинхронную обработку при инициализации подключения к базе данных или при инициализации результата выполнения команды.  
  
## <a name="opening-and-closing-a-database-connection"></a>Открытие и закрытие подключения к базе данных  
 При использовании поставщика [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] собственного клиента OLE DB приложения, предназначенные для асинхронной инициализации объекта источника данных, могут установить бит DBPROPVAL_ASYNCH_INITIALIZE в свойстве DBPROP_INIT_ASYNCH до вызова **IDBInitialize:: Initialize** . Когда это свойство задано, поставщик обеспечивает немедленный возврат из метода **Initialize** с результатом S_OK, если операция была завершена немедленно, или DB_S_ASYNCHRONOUS, если инициализация продолжается асинхронно. Приложения могут запрашивать интерфейс **IDBAsynchStatus** или [метод ISSAsynchStatus](../../../relational-databases/native-client-ole-db-interfaces/issasynchstatus-ole-db.md)в объекте источника данных, а затем вызывать **IDBAsynchStatus::** GetObject или[метод ISSAsynchStatus:: WaitForAsynchCompletion](../../../relational-databases/native-client-ole-db-interfaces/issasynchstatus-waitforasynchcompletion-ole-db.md) для получения состояния инициализации.  
  
 Кроме того, в набор свойств DBPROPSET_SQLSERVERROWSET добавлено свойство SSPROP_ISSAsynchStatus. Поставщики, поддерживающие интерфейс **ISSAsynchStatus**, должны реализовывать это свойство со значением VARIANT_TRUE.  
  
 Функции **IDBAsynchStatus::Abort** и [ISSAsynchStatus::Abort](../../../relational-databases/native-client-ole-db-interfaces/issasynchstatus-abort-ole-db.md) могут быть вызваны для отмены асинхронного вызова **Initialize**. Потребитель должен явно запросить асинхронную инициализацию источника данных. В противном случае возврат из метода **IDBInitialize::Initialize** не происходит до тех пор, пока объект источника данных не будет инициализирован полностью.  
  
> [!NOTE]  
>  Объекты источника данных, используемые для объединения соединений, не могут вызывать интерфейс **метод ISSAsynchStatus** в [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] собственного клиента OLE DB Provider. Интерфейс **ISSAsynchStatus** недоступен для объединенных в пул объектов источников данных.  
>   
>  Если приложение явно и принудительно использует ядро курсора, методы **IOpenRowset::OpenRowset** и **IMultipleResults::GetResult** не будут поддерживать асинхронную обработку.  
>   
>  Кроме того, прокси-сервер удаленного взаимодействия или библиотека DLL заглушки (в MDAC 2,8) не могут вызывать интерфейс **метод ISSAsynchStatus** в [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] собственного клиента. Интерфейс **ISSAsynchStatus** недоступен при удаленном взаимодействии.  
>   
>  Компоненты служб не поддерживают интерфейс **ISSAsynchStatus**.  
  
## <a name="execution-and-rowset-initialization"></a>Выполнение и инициализация наборов строк  
 Приложения, способные асинхронно открывать результаты выполнения команд, могут установить бит DBPROPVAL_ASYNCH_INITIALIZE в свойстве DBPROP_ROWSET_ASYNCH. Если задать этот бит перед вызовом **IDBInitialize::Initialize**, **ICommand::Execute**, **IOpenRowset::OpenRowset** или **IMultipleResults::GetResult**, значение аргумента *riid* должно быть IID_IDBAsynchStatus, IID_ISSAsynchStatus или IID_IUnknown.  
  
 Метод возвращается немедленно с результатом S_OK, если инициализация набора строк завершается немедленно, или с результатом DB_S_ASYNCHRONOUS, если инициализация набора строк продолжается асинхронно, а параметр *ppRowset* указывает запрошенный интерфейс для набора строк. Для поставщика [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] собственного клиента OLE DB этот интерфейс может быть только **IDBAsynchStatus** или **метод ISSAsynchStatus**. Пока набор строк не инициализирован полностью, этот интерфейс действует, как если бы он был приостановлен, и при вызове метода **QueryInterface** для получения интерфейсов, отличных от **IID_IDBAsynchStatus** или **IID_ISSAsynchStatus**, может быть возращена ошибка E_NOINTERFACE. Если потребитель явно не запросил асинхронную обработку, набор строк инициализируется синхронно. Все запрашиваемые интерфейсы доступны, когда метод **IDBAsynchStaus::GetStatus** или **ISSAsynchStatus::WaitForAsynchCompletion** возвращается с указанием того, что асинхронная операция завершена. Это не обязательно означает, что набор строк заполнен, но он завершен и полностью функционален.  
  
 Если выполненная команда не возвращает набор строк, она все равно возвращается немедленно с объектом, поддерживающим **IDBAsynchStatus**.  
  
 Если требуется получить несколько результатов асинхронного выполнения команды, выполните следующие действия.  
  
-   Установите бит DBPROPVAL_ASYNCH_INITIALIZE свойства DBPROP_ROWSET_ASYNCH перед выполнением команды.  
  
-   Вызовите метод **ICommand::Execute** и запросите интерфейс **IMultipleResults**.  
  
 Интерфейсы **IDBAsynchStatus** и **ISSAsynchStatus** могут быть получены путем запроса интерфейса множественных результатов с помощью метода **QueryInterface**.  
  
 После завершения выполнения команды **IMultipleResults** можно использовать как нормальную, с одним исключением из синхронного случая: DB_S_ASYNCHRONOUS может быть возвращено, в этом случае **IDBAsynchStatus** или **метод ISSAsynchStatus** можно использовать для определить, когда операция завершена.  
  
## <a name="examples"></a>Примеры  
 В следующем примере приложение вызывает неблокирующий метод, выполняет некоторую другую обработку, а затем возвращает результаты процессу. Интерфейс **ISSAsynchStatus::WaitForAsynchCompletion** ожидает объект внутреннего события, пока не будет завершена асинхронно выполняющаяся операция или пока не истечет время, указанное в параметре *dwMilisecTimeOut*.  
  
```  
// Set the DBPROPVAL_ASYNCH_INITIALIZE bit in the   
// DBPROP_ROWSET_ASYNCH property before calling Execute().  
  
DBPROPSET CmdPropset[1];  
DBPROP CmdProperties[1];  
  
CmdPropset[0].rgProperties = CmdProperties;  
CmdPropset[0].cProperties = 1;  
CmdPropset[0].guidPropertySet = DBPROPSET_ROWSET;  
  
// Set asynch mode for command.  
CmdProperties[0].dwPropertyID = DBPROP_ROWSET_ASYNCH;  
CmdProperties[0].vValue.vt = VT_I4;  
CmdProperties[0].vValue.lVal = DBPROPVAL_ASYNCH_INITIALIZE;  
CmdProperties[0].dwOptions = DBPROPOPTIONS_REQUIRED;  
  
hr = pICommandProps->SetProperties(1, CmdPropset);  
  
hr = pICommand->Execute(  
   pUnkOuter,  
   IID_ISSAsynchStatus,  
   pParams,  
   pcRowsAffected,  
   (IUnknown**)&pISSAsynchStatus);  
  
if (hr == DB_S_ASYNCHRONOUS)  
{  
   // Do some work here...  
  
   hr = pISSAsynchStatus->WaitForAsynchCompletion(dwMilisecTimeOut);  
   if ( hr == S_OK)  
   {  
      hr = pISSAsynchStatus->QueryInterface(IID_IRowset, (void**)&pRowset);  
      pISSAsynchStatus->Release();  
   }  
}  
```  
  
 Метод **ISSAsynchStatus::WaitForAsynchCompletion** ожидает объект внутреннего события, пока не будет завершена асинхронно выполняющаяся операция или пока не будет передано значение *dwMilisecTimeOut*.  
  
 В следующем примере показана асинхронная обработка с несколькими результирующими наборами.  
  
```  
DBPROP CmdProperties[1];  
  
// Set asynch mode for command.  
CmdProperties[0].dwPropertyID = DBPROP_ROWSET_ASYNCH;  
CmdProperties[0].vValue.vt = VT_I4;  
CmdProperties[0].vValue.lVal = DBPROPVAL_ASYNCH_INITIALIZE;  
  
hr = pICommand->Execute(  
   pUnkOuter,  
   IID_IMultipleResults,  
   pParams,  
   pcRowsAffected,  
   (IUnknown**)&pIMultipleResults);  
  
// Use GetResults for ISSAsynchStatus.  
hr = pIMultipleResults->GetResult(IID_ISSAsynchStatus, (void **) &pISSAsynchStatus);  
  
if (hr == DB_S_ASYNCHRONOUS)  
{  
   // Do some work here...  
  
   hr = pISSAsynchStatus->WaitForAsynchCompletion(dwMilisecTimeOut);  
   if (hr == S_OK)  
   {  
      hr = pISSAsynchStatus->QueryInterface(IID_IRowset, (void**)&pRowset);  
      pISSAsynchStatus->Release();  
   }  
}  
```  
  
 Чтобы предотвратить блокировку, клиент может проверить состояние выполняющейся асинхронной операции, как показано в следующем примере.  
  
```  
// Set the DBPROPVAL_ASYNCH_INITIALIZE bit in the   
// DBPROP_ROWSET_ASYNCH property before calling Execute().  
hr = pICommand->Execute(  
   pUnkOuter,  
   IID_ISSAsynchStatus,  
   pParams,  
   pcRowsAffected,  
   (IUnknown**)&pISSAsynchStatus);   
  
if (hr == DB_S_ASYNCHRONOUS)  
{  
   do{  
      // Do some work...  
      hr = pISSAsynchStatus->GetStatus(DB_NULL_HCHAPTER, DBASYNCHOP_OPEN, NULL, NULL, &ulAsynchPhase, NULL);  
   }while (DBASYNCHPHASE_COMPLETE != ulAsynchPhase)  
   if SUCCEEDED(hr)  
   {  
      hr = pISSAsynchStatus->QueryInterface(IID_IRowset, (void**)&pRowset);  
   }  
   pIDBAsynchStatus->Release();  
}  
```  
  
 В следующем примере показано, как можно отменить выполняющуюся в настоящее время асинхронную операцию.  
  
```  
// Set the DBPROPVAL_ASYNCH_INITIALIZE bit in the   
// DBPROP_ROWSET_ASYNCH property before calling Execute().  
hr = pICommand->Execute(  
   pUnkOuter,  
   IID_ISSAsynchStatus,  
   pParams,  
   pcRowsAffected,  
   (IUnknown**)&pISSAsynchStatus);  
  
if (hr == DB_S_ASYNCHRONOUS)  
{  
   // Do some work...  
   hr = pISSAsynchStatus->Abort(DB_NULL_HCHAPTER, DBASYNCHOP_OPEN);  
}  
```  
  
## <a name="see-also"></a>См. также раздел  
 [Компоненты собственного клиента SQL Server](../../../relational-databases/native-client/features/sql-server-native-client-features.md)   
 [Свойства и поведение наборов строк](../../../relational-databases/native-client-ole-db-rowsets/rowset-properties-and-behaviors.md)   
 [Метод ISSAsynchStatus &#40;OLE DB&#41;](../../../relational-databases/native-client-ole-db-interfaces/issasynchstatus-ole-db.md)  
  
  
