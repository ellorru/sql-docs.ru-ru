---
title: Поиск идентификаторов GUID для наборов свойств и целочисленных идентификаторов свойств для свойств поиска | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- full-text search [SQL Server], search property lists
- search property lists [SQL Server], configuring
ms.assetid: 7db79165-8bcc-4be6-8d40-12d44deda79f
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: f7a18a44a0f71254342f8fc29c38f0993fc05bfb
ms.sourcegitcommit: baa40306cada09e480b4c5ddb44ee8524307a2ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2019
ms.locfileid: "73637898"
---
# <a name="find-property-set-guids-and-property-integer-ids-for-search-properties"></a>Поиск идентификаторов GUID наборов свойств и целочисленных идентификаторов свойств для свойств поиска
  В этом разделе описывается получение значений, которые необходимы для добавления свойства в список свойств поиска и включения свойства для полнотекстового поиска. К таким значениям относится идентификатор GUID набора свойств и целочисленный идентификатор свойства документа.  
  
 Свойства документа, извлекаемые фильтрами IFilter из двоичных данных, т. е. из данных, хранящихся в `varbinary`, `varbinary(max)` (включая `FILESTREAM`) или `image` столбца типа данных — можно сделать доступным для полнотекстового поиска. Чтобы сделать извлеченное свойство доступным для поиска, его необходимо вручную добавить в список свойств поиска. Список свойств поиска необходимо также связать с одним или несколькими полнотекстовыми индексами. Дополнительные сведения см. в статье [Поиск свойств документа с использованием списков свойств поиска](search-document-properties-with-search-property-lists.md).  
  
 Перед добавлением доступных свойств к списку свойств необходимо найти 2 элемента данных о свойствах:  
  
-   Набор свойств GUID родительского объекта.  
  
-   Целочисленный идентификатор свойства модели.  
  
 (При добавлении свойства в список также можно указать имя и описание. Однако не обязательно использовать каноническое имя и описание свойства.)  
  
 В этом разделе описываются часто используемые методы для поиска сведений о доступных свойствах, особенно о свойствах, определенных Майкрософт. За сведениями о свойствах, определенных независимыми поставщиками программных продуктов, обращайтесь к документации или к поставщику.  
  
##  <a name="wellknown"></a> Поиск сведений о широко используемых и известных свойствах Майкрософт  
 Корпорация Майкрософт определяет несколько сотен свойств документа, которые используются во множестве контекстов, однако для каждого формата файла используется только малая часть доступных свойств. К часто используемым свойствам Windows относится небольшой набор универсальных свойств. Некоторые примеры известных универсальных свойств показаны в следующей таблице. В таблице приводится известное имя, каноническое имя Windows (из описания свойства, опубликованного корпорацией Майкрософт), идентификатор GUID набора свойств, целочисленный идентификатор свойства и краткое описание.  
  
|Известное имя|Каноническое имя Windows|Идентификатор GUID набора свойств|Целочисленный идентификатор|Описание|  
|----------------------|----------------------------|-----------------------|----------------|-----------------|  
|Авторы|`System.Author`|F29F85E0-4FF9-1068-AB91-08002B27B3D9|4|Автор или авторы данного элемента.|  
|Теги|`System.Keywords`|F29F85E0-4FF9-1068-AB91-08002B27B3D9|5|Набор ключевых слов (тегов), назначенных элементу.|  
|Тип|`System.PerceivedType`|28636AA6-953D-11D2-B5D6-00C04FD918D0|9|Ожидаемый тип файла на основе канонического типа.|  
|Title|`System.Title`|F29F85E0-4FF9-1068-AB91-08002B27B3D9|2|Заголовок элемента. Например, заголовок документа, тема сообщения, подпись к фотографии или название музыкальной композиции.|  
  
 Чтобы обеспечить согласованность между форматами файлов, корпорация Майкрософт выделила подмножество часто используемых свойств документа с повышенным приоритетом для нескольких категорий документов. К таким категориям относятся связь, контакты, документы, музыкальные файлы, изображения и видеоматериалы. Дополнительные сведения о главных свойствах для каждой категории см. в разделе [System-defined properties for custom file formats (на английском языке)](https://go.microsoft.com/fwlink/?LinkId=144336) из набора документации Windows Search.  
  
 В каждом формате файла могут быть реализованы свойства трех типов.  
  
-   Универсальные свойства, определенные [!INCLUDE[msCoName](../../includes/msconame-md.md)].  
  
-   Свойства определенных категорий, определенные [!INCLUDE[msCoName](../../includes/msconame-md.md)].  
  
-   Пользовательские свойства определенных приложений, определяемые поставщиком ПО.  
  
##  <a name="filtdump"></a> Поиск сведений о доступных свойствах с помощью FILTDUMP.EXE  
 Чтобы узнать, какие свойства обнаруживаются и извлекаются установленным фильтром IFilter, можно установить и запустить служебную программу **filtdump.exe** , которая входит в пакет SDK [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows.  
  
 Программа **filtdump.exe** запускается из командной строки с указанием одного аргумента. Такой аргумент является именем отдельного файла с типом, для которого установлен IFilter. Служебная программа отображает список всех свойств, обнаруженных в документе фильтрами IFilter, с идентификаторами GUID набора свойств, целочисленными идентификаторами и дополнительными сведениями.  
  
 Сведения об установке этого программного обеспечения см. на странице [Microsoft Windows SDK for Windows Server 7 and .NET Framework 4 (на английском языке)](https://www.microsoft.com/download/details.aspx?id=8279). После загрузки и установки пакета SDK перейдите к папкам, где находится служебная программа filtdump.exe.  
  
-   Сведения о 64-разрядной версии см. в каталоге `C:\Program Files\Microsoft SDKs\Windows\v7.1\Bin\x64`.  
  
-   Сведения о 32-разрядной версии см. в каталоге `C:\Program Files\Microsoft SDKs\Windows\v7.1\Bin`.  
  
##  <a name="propdesc"></a> Поиск значений для списка свойств поиска с помощью описания свойства Windows  
 Для известного свойства поиска Windows эти данные можно получить из атрибутов `formatID` и `propID` в описании свойства (`propertyDescription`).  
  
 В следующем примере показана нужная часть описания типичного свойства Майкрософт, в данном случае свойства `System.Author` . В атрибуте `formatID` задается идентификатор GUID набора свойств ( `F29F85E0-4FF9-1068-AB91-08002B27B3D9`), а в атрибуте `propID` задается целочисленный идентификатор свойства `4.` Обратите внимание, что в атрибуте `name` задается каноническое имя свойства Windows ( `System.Author`). (В этом примере пропускаются части описания свойства, неважные в данном случае.)  
  
```  
.  
propertyDescription  
name = System.Author  
...  
formatID = F29F85E0-4FF9-1068-AB91-08002B27B3D9  
propID = 4  
...  
```  
  
 Полное описание этого свойства см. в разделе [System.Author](https://go.microsoft.com/fwlink/?LinkId=144337) документации по Windows Search.  
  
 Полный список свойств Windows см. в разделе [Windows Properties (на английском языке)](https://go.microsoft.com/fwlink/?LinkId=215013)документации по Windows Search.  
  
##  <a name="examples"></a> Добавление свойства в список свойств поиска  
 В следующем примере показано, как добавить свойство в список свойств поиска. В примере инструкция [ALTER SEARCH PROPERTY LIST](/sql/t-sql/statements/alter-search-property-list-transact-sql) добавляет свойство `System.Author` в список свойств поиска с именем `PropertyList1`и предоставляет понятное имя `Author`для свойства.  
  
```  
ALTER SEARCH PROPERTY LIST PropertyList1   
  ADD 'Author'  
    WITH (  
          PROPERTY_SET_GUID = 'F29F85E0-4FF9-1068-AB91-08002B27B3D9',  
          PROPERTY_INT_ID = 4,   
          PROPERTY_DESCRIPTION = 'System.Author - the author or authors of the item'   
         )  
GO  
```  
  
 Дополнительные сведения о создании списка свойств поиска и создании связи с полнотекстовым индексом см. в статье [Поиск свойств документа с использованием списков свойств поиска](search-document-properties-with-search-property-lists.md).  
  
## <a name="see-also"></a>См. также раздел  
 [Поиск свойств документа с использованием списков свойств поиска](search-document-properties-with-search-property-lists.md)   
 [Настройка и управление фильтрами для поиска](configure-and-manage-filters-for-search.md)  
  
  
