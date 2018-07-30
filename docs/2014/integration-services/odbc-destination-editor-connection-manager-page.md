---
title: Редактор назначения ODBC (страница «Диспетчер соединений») | Документация Майкрософт
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
- sql12.ssis.designer.odbcdest.connection.f1
ms.assetid: f6d9c6c2-e4c4-468b-9e0d-af7b9609614d
caps.latest.revision: 7
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 5994e35479f73fb4bee3c062eb76858778a72d6d
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/02/2018
ms.locfileid: "37158985"
---
# <a name="odbc-destination-editor-connection-manager-page"></a>Редактор назначения «ODBC» (страница «Диспетчер соединений»)
  Страница **Диспетчер соединений** диалогового окна **Редактор назначения ODBC** используется для выбора диспетчера соединений ODBC для назначения. На этой странице также можно выбрать таблицу или представление базы данных  
  
 Дополнительные сведения о назначении ODBC см. в разделе [ODBC Destination](data-flow/odbc-destination.md).  
  
 **Открытие страницы диспетчера соединений в редакторе назначения ODBC**  
  
## <a name="task-list"></a>Список задач  
  
-   В среде [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]откройте пакет служб [!INCLUDE[ssISCurrent](../includes/ssiscurrent-md.md)] , содержащий назначение ODBC.  
  
-   На вкладке **Поток данных** дважды щелкните назначение ODBC.  
  
-   В окне **Редактор назначения ODBC**нажмите кнопку **Диспетчер соединений**.  
  
## <a name="options"></a>Параметры  
  
### <a name="connection-manager"></a>Диспетчер соединений  
 Выберите из списка существующий диспетчер соединений ODBC или нажмите кнопку «Создать», чтобы создать новое соединение. Соединение может устанавливаться с любой базой данных, поддерживающей ODBC.  
  
### <a name="new"></a>Создать  
 Нажмите кнопку **Создать**. Откроется диалоговое окно **Настройка редактора диспетчера соединений ODBC** , где можно создать новый диспетчер соединений.  
  
### <a name="data-access-mode"></a>Режим доступа к данным  
 Выберите метод загрузки данных в назначение. Доступные параметры показаны в следующей таблице.  
  
|Параметр|Описание|  
|------------|-----------------|  
|Имя таблицы — пакетом|Выберите этот параметр, чтобы настроить назначение ODBC для работы в пакетном режиме. Если выбран этот параметр, становятся доступны следующие параметры.|  
||**Имя таблицы или представления**: выберите доступную таблицу или представление из списка.<br /><br /> Этот список содержит только первые 1000 таблиц. Если база данных содержит больше 1000 таблиц, можно ввести начальную часть имени таблицы или воспользоваться подстановочным знаком (\*), чтобы ввести любую часть имени для вывода нужных таблиц.<br /><br /> **Размер пакета**: введите размер пакета для массовой загрузки. Это количество строк, загружаемых в виде одного пакета.|  
|Имя таблицы — построчно|Выберите этот параметр, чтобы настроить назначение ODBC для вставки каждой строки в целевую таблицу по отдельности. Если выбран этот параметр, становится доступен следующий параметр.|  
||**Имя таблицы или представления**: выберите доступную таблицу или представление базы данных из списка.<br /><br /> Этот список содержит только первые 1000 таблиц. Если база данных содержит больше 1000 таблиц, можно ввести начальную часть имени таблицы или воспользоваться символом-шаблоном (*), чтобы ввести любую часть имени для вывода нужных таблиц.|  
  
### <a name="preview"></a>Предварительный просмотр  
 Нажмите кнопку **Просмотр** , чтобы просмотреть первые строки (до 200) данных для выбранной таблицы.  
  
## <a name="see-also"></a>См. также  
 [Пользовательские свойства назначений ODBC](data-flow/odbc-destination-custom-properties.md)   
 [Редактор назначения ODBC (страница "Сопоставления")](../../2014/integration-services/odbc-destination-editor-mappings-page.md)   
 [Редактор назначения ODBC &#40;странице вывода ошибок&#41;](../../2014/integration-services/odbc-destination-editor-error-output-page.md)  
  
  