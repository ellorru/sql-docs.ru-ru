---
title: "Выборка строк | Документы Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db-rowsets
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- fetching rows
- OLE DB rowsets, fetching
- rowsets [OLE DB], fetching
- IRowset interface
- SQL Server Native Client OLE DB provider, fetching
ms.assetid: 5e6dbe36-b682-464d-adfa-8e886f9bd452
caps.latest.revision: "30"
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9aa63737e286f8890a9ee454983428ef90e61a31
ms.sourcegitcommit: a0aa5e611a0e6ebb74ac1e2f613e8916dc7a7617
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/24/2018
---
# <a name="fetching-rows"></a>Выборка строк
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  **IRowset** интерфейс — базовый интерфейс набора строк. **IRowset** интерфейс предоставляет методы для последовательной выборки строк, получение данных из этих строк и управления строками. Потребители используют методы **IRowset** для всех строк базовых операций. Сюда входят выборка и освобождение строк, а также получение значений столбцов.  
  
 Когда потребитель получает указатель интерфейса на набор строк, обычно является первым шагом для определения возможностей для набора строк с помощью **IRowsetInfo::GetProperties** метод. Этот метод возвращает сведения об интерфейсах, предоставляемых набором строк, а также о свойствах набора строк, не отображаемых в качестве отдельных интерфейсов, таких как максимальное количество активных строк и количество строк, операции обновления которых одновременно ожидают в очереди.  
  
 Следующим шагом потребителя является определение характеристик или метаданных столбцов в наборе строк. Для этого можно воспользоваться **IColumnsInfo** простой столбец сведения или **IColumnsRowset** метод для расширенных сведений о столбце. **GetColumnInfo** метод возвращает следующие данные:  
  
-   Количество столбцов в результирующем наборе.  
  
-   Массив структур DBCOLUMNINFO, по одной на столбец.  
  
     Порядок структур соответствует порядку столбцов в наборе строк. Каждая структура DBCOLUMNINFO включает метаданные столбца, такие как имя столбца, порядковый номер столбца, максимально возможная длина значения в столбце, тип данных в столбце, точность и длина.  
  
-   Указатель хранилища для всех строковых значений в одном блоке распределения.  
  
 Потребитель определяет, какие столбцы ему требуются, либо на основе метаданных, либо на основе текста команды, создавшей набор строк. Он определяет порядковые номера необходимых столбцов на основе Упорядочение столбцов информацию, возвращаемую **IColumnsInfo** или из порядковых номеров в наборе строк метаданных столбцов, возвращенных **IColumnsRowset**.  
  
 **IColumnsInfo** и **IColumnsRowset** интерфейсы используются для получения сведений о столбцах в наборе строк. **IColumnsInfo** интерфейс возвращает ограниченный набор данных, тогда как **IColumnsRowset** предоставляет все метаданные.  
  
> [!NOTE]  
>  В [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] версии 7.0 и более ранних версий, возвращенных необязательный столбец метаданных DBCOLUMN_COMPUTEMODE **IColumnsInfo::GetColumnsInfo** содержит значение DBSTATUS_S_ISNULL (а не значения, является ли столбец вычисляемый), так как невозможно определить, является ли вычисляемым Базовый столбец.  
  
 Порядковые номера используются для указания привязок к столбцу. Привязка — это структура, связывающая элемент пользовательской структуры со столбцом. Привязываться может значение данных, длина или значение состояния столбца.  
  
 Набор привязок объединяется в метод доступа. Он будет создан с помощью **IAccessor::CreateAccessor** метод. Метод доступа может содержать несколько привязок, чтобы данные из нескольких столбцов можно было получать или задавать одним вызовом. Потребитель может создать несколько методов доступа для различных способов использования в различных частях приложения. Можно создавать и освобождать методы доступа, пока существует набор строк.  
  
 Для выборки строк из базы данных, потребитель вызывает метод, такие как **IRowset::GetNextRows** или **IRowsetLocate::GetRowsAt**. Эти операции выборки помещают данные строк с сервера в буфер строк поставщика. Потребитель не имеет прямого доступа к буферу строк поставщика. Потребитель вызывает **IRowset::GetData** для копирования данных из буфера поставщика в буфер потребителя и **IRowsetChange::SetData** для копирования изменений из буфера потребителя в буфер поставщика.  
  
 Потребитель вызывает метод **GetData** метод и передает дескриптор строке, дескриптор методу доступа и указатель буферу потребителя. **GetData** преобразует данные и возвращает столбцы, как указано в привязках, использовавшихся для создания метода доступа. Потребитель может вызвать **GetData** более чем один раз для одной строки с помощью различных методов доступа и буферы, поэтому потребитель может получить несколько копий тех же данных.  
  
 Данные из столбцов с переменной длиной могут обрабатываться различными способами. Прежде всего, такие столбцы могут быть привязаны к конечному разделу структуры потребителя. Это вызывает усечение, если длина данных превышает размер буфера. Потребитель может определить, что произошло усечение, проверив состояние DBSTATUS_S_TRUNCATED. Возвращаемая длина — это всегда действительная длина в байтах, соответственно, потребитель может также определить, сколько данных было усечено.  
  
 Когда потребитель завершает выборку или обновление строк, он освобождает их с **ReleaseRows** метод. Это позволяет высвободить ресурсы, затраченные на хранение копии строк в наборе, и создает свободное пространство для новых строк. Потребитель затем может повторить цикл выборки или создания строк и доступа к данным в них.  
  
 После завершения работы с помощью набора строк потребителя, он вызывает **IAccessor::ReleaseAccessor** метод для освобождения любого метода доступа. Он вызывает **IUnknown::Release** метод для всех интерфейсов, предоставляемых набором строк, для освобождения набора строк. После освобождения набора строк принудительно освобождаются все оставшиеся строки или методы доступа, которые могут удерживаться потребителем.  
  
## <a name="in-this-section"></a>В этом разделе  
  
-   [Следующая позиция выборки](../../relational-databases/native-client-ole-db-rowsets/fetching-rows-next-fetch-position.md)  
  
## <a name="see-also"></a>См. также  
 [Наборы строк](../../relational-databases/native-client-ole-db-rowsets/rowsets.md)  
  
  