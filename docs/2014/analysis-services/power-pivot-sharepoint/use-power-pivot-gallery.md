---
title: Использование галереи PowerPivot | Документация Майкрософт
ms.custom: ''
ms.date: 09/01/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: c9ff92d1-787a-4f34-990f-6676b61875d7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3e4dd52a33fbfb84f65658db6c645a5317b39c44
ms.sourcegitcommit: f76b4e96c03ce78d94520e898faa9170463fdf4f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2019
ms.locfileid: "70874483"
---
# <a name="use-powerpivot-gallery"></a>использовать галерею PowerPivot
  Галерея [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] — это специальная библиотека документов SharePoint. Она предлагает широкие возможности просмотра документов и управления ими для опубликованных книг Excel и отчетов служб Reporting Services, содержащих данные PowerPivot.  
  
> [!NOTE]  
>  В зависимости от конфигурации сервера в области предварительного просмотра для некоторых документов могут появляться предупреждения или сообщения об ошибках. Сообщения могут появляться, если для книги Excel задано автоматическое обновление данных при открытии. Сообщения с предупреждениями об обновлении данных отображаются в изображении предварительного просмотра, если в службе Excel настроена выдача таких предупреждений. Администратор фермы или службы может изменить параметры конфигурации, включив показ фактических листов при предварительном просмотре. Дополнительные сведения см. в разделе [Создание надежного расположения для сайтов PowerPivot в центре администрирования](create-a-trusted-location-for-power-pivot-sites-in-central-administration.md).  
  
##  <a name="bkmk_top"></a> В этом разделе  
  
-   [Значки в галерее PowerPivot](#icons)  
  
-   [Сохранение книги Excel в галерее PowerPivot](#add)  
  
-   [Создание новых отчетов или книг на основе опубликованной книги PowerPivot](#newdocs)  
  
-   [Открыть книгу или отчет в полностраничном режиме](#view)  
  
-   [Планирование обновления данных для книг PowerPivot в галерее PowerPivot](#newdr)  
  
-   [Удаление книги или отчета в галерее PowerPivot](#delete)  
  
-   [Обновление эскиза](#image)  
  
-   [Известные проблемы](#bkmk_known_issues)  
  
 [Предварительные требования](#prereq)  
  
##  <a name="prereq"></a> Предварительные требования  
  
> [!NOTE]  
>  Для коллекции Power Pivot требуется Microsoft Silverlight.  Браузер Microsoft Edge не поддерживает Silverlight.   
> Чтобы просмотреть содержимое библиотеки в Microsoft ребр, перейдите на вкладку **Библиотека** в коллекции Power PIVOT, а затем измените представление библиотеки документов на **все документы**.    
> Чтобы изменить представление по умолчанию, щелкните вкладку **Библиотека** и щелкните "Изменить представление". Щелкните "Сделать представлением по умолчанию", а затем "ОК", чтобы сохранить представление по умолчанию.  
>  Дополнительные сведения о поддержке Microsoft ребр см. в блоге Windows, [перерыве в прошлом, часть 2. Не говорите о ActiveX, VBScript...](http://blogs.windows.com/msedgedev/2015/05/06/a-break-from-the-past-part-2-saying-goodbye-to-activex-vbscript-attachevent/)  
  
 Полный список необходимых компонентов см. в разделе [Создание и настройка галереи PowerPivot](create-and-customize-power-pivot-gallery.md).  
  
##  <a name="icons"></a>Значки в галерее PowerPivot  
 Значки являются визуальным индикатором наличия контекста и состояния.  
  
|Значок|Описание|  
|----------|-----------------|  
|![GMNI_PowerPivotGalleryIcon_Hourglass](../media/gmni-powerpivotgalleryicon-hourglass.gif "GMNI_PowerPivotGalleryIcon_Hourglass")|Значок песочных часов появляется во время формирования эскиза каждой страницы документа. Обновите страницу, чтобы отобразить обновленное изображение.|  
|![GMNI_PowerPivotGalleryIcon_Truncated](../media/gmni-powerpivotgalleryicon-truncated.gif "GMNI_PowerPivotGalleryIcon_Truncated")|Значок страниц появляется в тот момент, когда число страниц книги или отчета превышает максимальное число страниц, которое может быть отображено в галерее PowerPivot. Для просмотра всех страниц необходимо пользоваться клиентским приложением.|  
|![GMNI_PowerPivotGalleryIcon_Error](../media/gmni-powerpivotgalleryicon-error.gif "GMNI_PowerPivotGalleryIcon_Error")|Значок ошибки появляется в том случае, если не удалось отобразить эскиз документа. Документ публикуется в библиотеке, однако его не удается подготовить для просмотра в пользовательских представлениях галереи PowerPivot. При этом его открытие будет возможно в таких клиентских приложениях, как надстройка PowerPivot для Excel.|  
|![GMNI_PowerPivotGalleryIcon_badtype](../media/gmni-powerpivotgalleryicon-badtype.gif "GMNI_PowerPivotGalleryIcon_badtype")|Значок недоступного содержимого открывается, когда загруженный документ невозможно отобразить в галерее PowerPivot. Поддерживаются следующие типы документов: книги PowerPivot и отчеты, созданные в построителе отчетов служб SQL Server 2008 R2 Reporting Services.<br /><br /> Этот значок также появляется при восстановлении документа из корзины.<br /><br /> Если этот значок появляется для документа, который раньше представлял собой допустимое изображение предварительного просмотра, изображение можно обновить, изменив свойство документа и сохранив изменения.|  
|![GMNI_PowerPivotGalleryIcon_Locked](../media/gmni-powerpivotgalleryicon-locked.gif "GMNI_PowerPivotGalleryIcon_Locked")|Значок заблокированного содержимого появляется в тот момент, когда отображение эскизов для этого документа преднамеренно отключено. Галерея PowerPivot не создает эскизы для книг Excel, которые не содержат данных PowerPivot, а также для книг PowerPivot и отчетов Reporting Services, которые не соответствуют требованиям к формированию моментальных снимков. Дополнительные сведения см. в подразделе «Предварительные условия» в этом разделе.|  
  
##  <a name="add"></a>Сохранение книги Excel в галерее PowerPivot  
 Книги [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] можно опубликовать в библиотеке с помощью любых методов совместного доступа, имеющихся в Excel 2010. Например, в Excel 2010 при выполнении команды «Сохранить как» путь SharePoint к библиотеке можно указать полностью или частично.  
  
1.  Сохраните файл.  
  
2.  1.  **Excel 2010:** В меню Файл выберите команду **сохранить & отправить**.  
  
    2.  Выберите операцию **Сохранить в SharePoint**.  
  
    3.  Если для выбора отдельных публикуемых листов или параметров требуется использовать параметры служб Excel, выберите **Параметры публикации** . Например, вкладка «Параметры» в параметрах служб Excel позволяет выбрать, какие срезы будут выводиться в опубликованной книге.  
  
    1.  **Excel 2013:**  В меню Файл выберите команду **сохранить**.  
  
    2.  Для выбора отдельных публикуемых листов или параметров требуется использовать параметры служб Excel, выберите **Параметры представления браузера** . Например, вкладка «Параметры» в параметрах служб Excel позволяет выбрать, какие срезы будут выводиться в опубликованной книге.  
  
3.  В поле имени файла диалогового окна «Сохранить как» введите полный или частичный URL-адрес коллекции [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Если введена часть URL-адреса, например имя сервера, можно просмотреть сайт, чтобы найти галерею [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Для этого нажмите **Сохранить** , чтобы установить соединение с указанным сервером.  
  
     ![GMNI_ExcelSaveAs](../media/gmni-excelsaveas.gif "GMNI_ExcelSaveAs")  
  
1.  В диалоговом окне «Сохранить как» выберите галерею [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] на вашем сайте.  
  
2.  Нажмите кнопку **Открыть** , чтобы открыть библиотеку.  
  
3.  Нажмите кнопку **Сохранить** , чтобы опубликовать книгу в библиотеке.  
  
 В окне браузера убедитесь, что документ выводится в галерее [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Новые опубликованные документы появятся в списке. Параметры библиотеки определяют место размещения документов (например, они будут отсортированы в порядке возрастания по дате или в алфавитном порядке по имени). Возможно, понадобится обновить окно браузера, чтобы отобразить самые последние добавления.  
  
#### <a name="upload-a-workbook-into-powerpivot-gallery"></a>Передача книги в библиотеку PowerPivot Gallery  
 Можно также передать книгу, если вы хотите начать с SharePoint и выбрать на компьютере файл для публикации.  
  
1.  На сайте SharePoint откройте коллекцию [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
2.  На ленте библиотеки выберите **Документы**.  
  
3.  В меню **Передача документа**выберите параметр передачи и укажите имя и расположение файла, который необходимо передать. Параметры библиотеки определяют, где появляется документ. Возможно, понадобится обновить окно браузера для просмотра самых последних добавлений.  
  
##  <a name="newdocs"></a>Создание новых отчетов или книг на основе опубликованной книги PowerPivot  
 Для книг [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , которые публикуются в Галерее [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , можно создавать дополнительные книги или отчеты служб Reporting Services, использующие опубликованную книгу в качестве подключенного источника данных.  
  
|||  
|-|-|  
|![GMNI_btn_NewDocReportGallery](../media/gmni-btn-newdocreportgallery.gif "GMNI_btn_NewDocReportGallery")|Нажмите часть кнопки «Создать отчет» со стрелкой вниз, чтобы запустить построитель отчетов или Excel 2010. Чтобы кнопка «Создать отчет» стала доступной, в коллекции PowerPivot необходимо использовать один из стандартных режимов просмотра («Театр», «Коллекция» или «Карусель»).|  
  
#### <a name="create-report-builder-report"></a>Создание отчета построителя отчетов  
 Для создания нового отчета, основанного на существующей книге PowerPivot в библиотеке, требуется, чтобы службы Reporting Services были настроены для интеграции с SharePoint для сайтов, которые содержат Галерею PowerPivot. При выборе варианта «Создать отчет построителя отчетов» с сервера отчетов загружается построитель отчетов, который устанавливается на локальной рабочей станции при первом использовании. Для нового отчета создается файл-заполнитель отчета, который сохраняется в Галерее PowerPivot. Сведения о соединении с книгой PowerPivot создаются как новый источник данных в отчете. На следующем шаге в рабочей области конструктора можно создать наборы данных и макет отчета. При использовании построителя отчетов для сборки отчета изменения и окончательные результаты можно сохранить в документе отчета в галерее. Чтобы в будущем не допустить разрыва связей между данными, необходимо хранить файлы отчета и книги в одной библиотеке.  
  
#### <a name="open-new-excel-workbook"></a>Открыть новую книгу Excel  
 Чтобы создать новую книгу Excel из существующей, на локальном компьютере должны быть установлены Excel и клиент [!INCLUDE[ssGeminiClient](../../includes/ssgeminiclient-md.md)] . При выборе команды «Открыть новую книгу Excel» запускается Excel, открывается пустой файл книги (XLSX) и в качестве подключенного источника данных в фоновом режиме загружаются данные [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . В новой книге используются только данные из окна PowerPivot в исходной книге. Сводные таблицы или сводные диаграммы из исходной книги исключаются. Новая книга ссылается на данные исходной книги. Данные не копируются в саму новую книгу.  
  
##  <a name="view"></a> Открыть книгу или отчет в полностраничном режиме  
 Щелкните любой видимый эскиз просматриваемого документа, чтобы открыть его в полностраничном режиме отдельно от предварительного просмотра галереи [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] открываются в браузере. Отчеты Reporting Services откроются в веб-части ReportViewer, являющейся частью развернутой службы Reporting Services на сервере SharePoint.  
  
 Вместо просмотра книги в браузере можно открыть книгу в Excel на клиентской рабочей станции. Для просмотра файла необходимы Excel 2013 или Excel 2010 и надстройка [!INCLUDE[ssGeminiClient](../../includes/ssgeminiclient-md.md)] . В Excel 2007 можно открыть файл, но нельзя использовать Excel 2007 для сведения данных. Поэтому для просмотра и создания данных PowerPivot рекомендуется использовать Excel 2013 или Excel 2010. Если у вас нет нужных приложений, необходимо использовать браузер для просмотра книги из SharePoint.  
  
##  <a name="newdr"></a>Планирование обновления данных для книг PowerPivot в галерее PowerPivot  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] в опубликованной книге Excel можно обновлять через запланированные интервалы.  
  
|||  
|-|-|  
|![GMNI_btn_NewDataRefreshReportGallery](../media/gmni-btn-newdatarefreshreportgallery.gif "GMNI_btn_NewDataRefreshReportGallery")|Нажмите кнопку «Управление обновлением данных», чтобы создать или просмотреть расписание получения обновленных данных из подключенных источников данных. Инструкции по созданию расписания см. в разделе [планирование &#40;&#41;PowerPivot для SharePoint обновления данных](../schedule-a-data-refresh-powerpivot-for-sharepoint.md).|  
  
##  <a name="delete"></a>Удаление книги или отчета в галерее PowerPivot  
 Чтобы удалить документ из библиотеки, сначала нужно переключиться на представление «Все документы».  
  
1.  На сайте SharePoint откройте коллекцию [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
2.  На ленте нажмите кнопку **Библиотека**.  
  
3.  В области «Управление представлениями» в списке текущих представлений нажмите стрелку вниз и выберите «Все документы».  
  
4.  Выберите книгу или отчет, которые хотите удалить.  
  
5.  В области "Документы (файлы)" в разделе "Управление" нажмите кнопку **Удалить документ** .  
  
##  <a name="image"></a> Обновление эскиза  
 Для повторного создания эскиза документа в Галерее PowerPivot выполните следующие действия.  
  
1.  Переключите коллекцию PowerPivot в представление «Все документы». Для этого выберите пункт **Библиотека** на ленте и измените **Текущее представление** на **Все документы**.  
  
2.  Выберите книгу или отчет, для которого нужно обновить эскиз.  
  
3.  Нажмите стрелку вниз справа и выберите **Изменить свойства**.  
  
4.  Нажмите кнопку **Сохранить**. При сохранении документа служба моментальных снимков выполняет повторное создание эскиза.  
  
##  <a name="bkmk_known_issues"></a> Известные проблемы  
  
### <a name="document-type-is-not-supported"></a>Тип документа не поддерживается  
 Тип содержимого **Документ галереи PowerPivot** не поддерживается. Если включить тип содержимого **Документ галереи PowerPivot** для библиотеки документов и попытаться создать новый документ этого типа, появится сообщение об ошибке, похожее на следующее:  
  
-   Для "нового документа" требуется приложение, совместимое с Microsoft SharePoint Foundation, и веб-браузер. Чтобы добавить документ в эту библиотеку документов, нажмите кнопку "отправить документ".  
  
-   "Адрес Интернета" http://[имя сервера]/TestSite/PowerPivot Gallery Gallery/ReportGallery/Forms/Template. xlsx "является недопустимым." " Microsoft Excel не удается получить доступ к файлу "http://[имя сервера]/TestSite/PowerPivot Gallery Gallery/ReportGallery/Forms/Template. xlsx". Существует несколько возможных причин.  
  
 Тип содержимого **Документ галереи PowerPivot** не добавляется автоматически в библиотеки документов. Вы не столкнетесь с этой проблемой, если вручную не включите неподдерживаемый тип содержимого.  
  
## <a name="see-also"></a>См. также  
 [Создание надежного расположения для сайтов PowerPivot в центре администрирования](create-a-trusted-location-for-power-pivot-sites-in-central-administration.md)   
 [Удалить галерею PowerPivot](delete-power-pivot-gallery.md)   
 [Создание и настройка галереи PowerPivot](create-and-customize-power-pivot-gallery.md)   
 [Планирование обновления &#40;данных PowerPivot для SharePoint&#41;](../schedule-a-data-refresh-powerpivot-for-sharepoint.md)  
  
  
