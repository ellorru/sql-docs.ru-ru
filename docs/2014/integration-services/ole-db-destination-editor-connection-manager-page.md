---
title: Редактор назначения OLE DB (страница «Диспетчер соединений») | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.oledbdestadapter.connection.f1
helpviewer_keywords:
- OLE DB Destination Editor
ms.assetid: ae2200c6-8ba0-49b7-b01a-53425b84d2ed
caps.latest.revision: 81
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 1e6aaff0e415aeaab5e42395a3acd7c0b96a0f00
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/02/2018
ms.locfileid: "37328074"
---
# <a name="ole-db-destination-editor-connection-manager-page"></a>Редактор назначения OLE DB (страница «Диспетчер соединений»)
  Страница **Диспетчер соединений** диалогового окна **Редактор назначения «OLE DB»** используется для выбора подключения OLE DB для назначения. На этой странице также можно выбрать таблицу или представление базы данных.  
  
> [!NOTE]  
>  `CommandTimeout` Свойство назначения «OLE DB» недоступно в **Редактор назначения OLE DB**, однако его можно установить с помощью **расширенный редактор**. Кроме того, некоторые параметры быстрой загрузки доступны только в **Расширенном редакторе**. Дополнительные сведения об этих свойствах см. в подразделе «Назначение "OLE DB"» раздела [OLE DB Custom Properties](data-flow/ole-db-custom-properties.md).  
  
 Дополнительные сведения о назначении «OLE DB» см. в разделе [OLE DB Destination](data-flow/ole-db-destination.md).  
  
## <a name="static-options"></a>Статические параметры  
 **Диспетчер соединений OLE DB**  
 Выберите из списка существующий диспетчер соединений или создайте новое соединение, нажав кнопку **Создать**.  
  
 **Создать**  
 Создайте новый диспетчер соединений с помощью диалогового окна **Настройка диспетчера соединений OLE DB** .  
  
 **Режим доступа к данным**  
 Укажите метод загрузки данных в назначение. Загрузка данных с двухбайтовой кодировкой (DBCS) требует одного из режимов быстрой загрузки. Дополнительные сведения о режимах доступа для быстрой загрузки данных, оптимизированных для массовой вставки, см. в разделе [OLE DB Destination](data-flow/ole-db-destination.md).  
  
|Параметр|Описание|  
|------------|-----------------|  
|Таблица или представление|Загрузка данных в таблицу или представление назначения «OLE DB».|  
|Быстрая загрузка таблицы или представления|Загрузка данных в таблицу или представление назначения «OLE DB» и использование параметра быстрой загрузки. Дополнительные сведения о режимах доступа для быстрой загрузки данных, оптимизированных для массовой вставки, см. в разделе [OLE DB Destination](data-flow/ole-db-destination.md).|  
|Переменная, содержащая имя таблицы или представления|Задайте переменную, содержащую имя таблицы или представления.<br /><br /> **См. также**: [Использование переменных в пакетах](../../2014/integration-services/use-variables-in-packages.md)|  
|Быстрая загрузка переменной имени представления или имени таблицы|Укажите переменную, содержащую имя таблицы или представления, и используйте для загрузки данных параметр быстрой загрузки. Дополнительные сведения о режимах доступа для быстрой загрузки данных, оптимизированных для массовой вставки, см. в разделе [OLE DB Destination](data-flow/ole-db-destination.md).|  
|Команда SQL|Загрузка данных в назначение «OLE DB» при помощи SQL-запроса.|  
  
 **Предварительный просмотр**  
 Просмотрите предварительные результаты, используя диалоговое окно **Предварительный просмотр результатов запроса** . В окне «Предварительный просмотр» может отображаться до 200 строк.  
  
## <a name="data-access-mode-dynamic-options"></a>Динамические параметры режима доступа к данным  
 Каждая настройка в **Режиме доступа к данным** содержит динамический набор параметров, уникальный для каждой настройки. В следующих разделах описываются все динамические параметры, доступные для каждой настройки **Режима доступа к данным** .  
  
### <a name="data-access-mode--table-or-view"></a>Режим доступа к данным = Таблица или представление  
 **Имя таблицы или представления**  
 Выберите имя таблицы или представления из списка доступных в источнике данных.  
  
 **Создать**  
 Создайте новую таблицу с помощью диалогового окна **Создание таблицы** .  
  
> [!NOTE]  
>  При нажатии кнопки **Создать**службы [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] по умолчанию формируют инструкцию CREATE TABLE на основе подключенного источника данных. Эта инструкция CREATE TABLE не включает атрибут FILESTREAM, даже если исходная таблица содержит столбец, для которого объявлен атрибут FILESTREAM. Чтобы запустить компонент служб [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] с атрибутом FILESTREAM, сначала следует создать хранилище FILESTREAM в целевой базе данных. Затем добавьте атрибут FILESTREAM к инструкции CREATE TABLE в диалоговом окне **Создание таблицы** . Дополнительные сведения см. в разделе [Данные большого двоичного объекта (SQL Server)](../relational-databases/blob/binary-large-object-blob-data-sql-server.md).  
  
### <a name="data-access-mode--table-or-view--fast-load"></a>Режим доступа к данным = Таблица или представление — быстрая загрузка  
 **Имя таблицы или представления**  
 Выберите из этого списка таблицу или представление базы данных или создайте новую таблицу, нажав кнопку **Создать**.  
  
 **Создать**  
 Создайте новую таблицу с помощью диалогового окна **Создание таблицы** .  
  
> [!NOTE]  
>  При нажатии кнопки **Создать**службы [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] по умолчанию формируют инструкцию CREATE TABLE на основе подключенного источника данных. Эта инструкция CREATE TABLE не включает атрибут FILESTREAM, даже если исходная таблица содержит столбец, для которого объявлен атрибут FILESTREAM. Чтобы запустить компонент служб [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] с атрибутом FILESTREAM, сначала следует создать хранилище FILESTREAM в целевой базе данных. Затем добавьте атрибут FILESTREAM к инструкции CREATE TABLE в диалоговом окне **Создание таблицы** . Дополнительные сведения см. в разделе [Данные большого двоичного объекта (SQL Server)](../relational-databases/blob/binary-large-object-blob-data-sql-server.md).  
  
 **Сохранять ИД**  
 Укажите, следует ли при загрузке данных копировать значения идентификаторов. Это свойство доступно только с параметром быстрой загрузки. Значение по умолчанию этого свойства — `false`.  
  
 **Сохранять значения NULL**  
 Укажите, следует ли при загрузке данных копировать значения NULL. Это свойство доступно только с параметром быстрой загрузки. Значение по умолчанию этого свойства — `false`.  
  
 **Блокировка таблицы**  
 Укажите, должна ли таблица блокироваться при загрузке. Значение по умолчанию этого свойства — `true`.  
  
 **Проверочные ограничения**  
 Определите, будет ли назначение проверять ограничения во время загрузки данных. Значение по умолчанию этого свойства — `true`.  
  
 **Строк на пакет**  
 Задает количество строк в одном пакете. Это свойство по умолчанию имеет значение **-1**, которое указывает на то, что никакое значение не присваивалось.  
  
> [!NOTE]  
>  Чтобы показать, что этому свойству не нужно присваивать пользовательское значение, очистите текстовое поле в окне **Редактор назначения "OLE DB"** .  
  
 **Макс. фиксируемый размер вставок**  
 Задайте размер пакетов, который назначение «OLE DB» пытается зафиксировать во время операций быстрой загрузки. Значение **0** указывает, что фиксация всех данных производится в одном пакете после обработки всех строк.  
  
> [!NOTE]  
>  Если назначение «OLE DB» и другой компонент потока данных обновляют одну и ту же исходную таблицу, то значение **0** может привести к тому, что выполняемый пакет перестанет отвечать на запросы. Чтобы решить эту проблему, задайте для параметра **Макс. фиксируемый размер вставок** значение **2147483647**.  
  
 При задании значения этого свойства назначение фиксирует строки в пакетах, которые меньше (а) значения **Макс. фиксируемый размер вставок**или (б) количества оставшихся строк в буфере, обрабатываемом в текущий момент.  
  
> [!NOTE]  
>  Любое нарушение ограничения в назначении вызывает сбой обработки всего пакета строк, определенного параметром **Макс. фиксируемый размер вставок** .  
  
### <a name="data-access-mode--table-name-or-view-name-variable"></a>Режим доступа к данным — переменная, содержащая имя таблицы или представления  
 **Имя переменной**  
 Выберите переменную, содержащую имя таблицы или представления.  
  
### <a name="data-access-mode--table-name-or-view-name-variable--fast-load"></a>Режим доступа к данным = переменная, содержащая имя таблицы или представления (быстрая загрузка)  
 **Имя переменной**  
 Выберите переменную, содержащую имя таблицы или представления.  
  
 **Создать**  
 Создайте новую таблицу с помощью диалогового окна **Создание таблицы** .  
  
> [!NOTE]  
>  При нажатии кнопки **Создать**службы [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] по умолчанию формируют инструкцию CREATE TABLE на основе подключенного источника данных. Эта инструкция CREATE TABLE не включает атрибут FILESTREAM, даже если исходная таблица содержит столбец, для которого объявлен атрибут FILESTREAM. Чтобы запустить компонент служб [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] с атрибутом FILESTREAM, сначала следует создать хранилище FILESTREAM в целевой базе данных. Затем добавьте атрибут FILESTREAM к инструкции CREATE TABLE в диалоговом окне **Создание таблицы** . Дополнительные сведения см. в разделе [Данные большого двоичного объекта (SQL Server)](../relational-databases/blob/binary-large-object-blob-data-sql-server.md).  
  
 **Сохранять ИД**  
 Укажите, следует ли при загрузке данных копировать значения идентификаторов. Это свойство доступно только с параметром быстрой загрузки. Значение по умолчанию этого свойства — `false`.  
  
 **Сохранять значения NULL**  
 Укажите, следует ли при загрузке данных копировать значения NULL. Это свойство доступно только с параметром быстрой загрузки. Значение по умолчанию этого свойства — `false`.  
  
 **Блокировка таблицы**  
 Укажите, должна ли таблица блокироваться при загрузке. Значение по умолчанию этого свойства — `false`.  
  
 **Проверочные ограничения**  
 Укажите, действуют ли на задачу проверочные ограничения. Значение по умолчанию этого свойства — `false`.  
  
 **Строк на пакет**  
 Задает количество строк в одном пакете. Это свойство по умолчанию имеет значение **-1**, которое указывает на то, что никакое значение не присваивалось.  
  
> [!NOTE]  
>  Чтобы показать, что этому свойству не нужно присваивать пользовательское значение, очистите текстовое поле в окне **Редактор назначения "OLE DB"** .  
  
 **Макс. фиксируемый размер вставок**  
 Задайте размер пакетов, который назначение «OLE DB» пытается зафиксировать во время операций быстрой загрузки. Значение по умолчанию **2147483647** указывает на то, что фиксация всех данных производится одним пакетом после обработки всех строк.  
  
> [!NOTE]  
>  Если назначение «OLE DB» и другой компонент потока данных обновляют одну и ту же исходную таблицу, то значение **0** может привести к тому, что выполняемый пакет перестанет отвечать на запросы. Чтобы решить эту проблему, задайте для параметра **Макс. фиксируемый размер вставок** значение **2147483647**.  
  
### <a name="data-access-mode--sql-command"></a>Режим доступа к данным — команда SQL  
 **Текст команды SQL**  
 Введите текст SQL-запроса, постройте запрос, нажав кнопку **Создать запрос**, или выберите файл, содержащий текст запроса, нажав кнопку **Обзор**.  
  
> [!NOTE]  
>  Назначение «OLE DB» не поддерживает параметры. Если необходимо выполнить параметризованную инструкцию INSERT, лучше воспользоваться преобразованием «Команда OLE DB». Дополнительные сведения см. в разделе [OLE DB Command Transformation](data-flow/transformations/ole-db-command-transformation.md).  
  
 **Создать запрос**  
 Воспользуйтесь диалоговым окном **Построитель запросов** для визуального конструирования SQL-запроса.  
  
 **Обзор**  
 Воспользуйтесь диалоговым окном **Открыть** для выбора файла, содержащего текст SQL-запроса.  
  
 **Анализ запроса**  
 Проверить синтаксис текста запроса.  
  
## <a name="see-also"></a>См. также  
 [Integration Services Error and Message Reference](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Редактор назначения OLE DB &#40;страница «сопоставления»&#41;](../../2014/integration-services/ole-db-destination-editor-mappings-page.md)   
 [Редактор назначения OLE DB &#40;странице вывода ошибок&#41;](../../2014/integration-services/ole-db-destination-editor-error-output-page.md)   
 [Загрузка данных с помощью назначения «OLE DB»](data-flow/load-data-by-using-the-ole-db-destination.md)  
  
  