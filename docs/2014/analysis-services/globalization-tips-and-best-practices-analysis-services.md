---
title: Советы и рекомендации по глобализации (Analysis Services) | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- translations [Analysis Services], client applications
- date comparisons
- day-of-week comparisons [Analysis Services]
- time [Analysis Services]
- month comparisons [Analysis Services]
ms.assetid: 71a8c438-1370-4c69-961e-d067ee4e47c2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d8d98d2a45ff50c60a37ee04e576567db7f96e26
ms.sourcegitcommit: f76b4e96c03ce78d94520e898faa9170463fdf4f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2019
ms.locfileid: "70874412"
---
# <a name="globalization-tips-and-best-practices-analysis-services"></a>Советы и рекомендации по глобализации (службы Analysis Services)
  **[!INCLUDE[applies](../includes/applies-md.md)]**  Только многомерные  
  
 Эти советы и рекомендации помогут улучшить переносимость решений для бизнес-аналитики и избежать ошибок, которые непосредственно связаны с языковыми параметрами и параметрами сортировки.  
  
-   [Использование одинаковых параметров сортировки во всем стеке](#bkmk_sameColl)  
  
-   [Общие рекомендации для параметров сортировки](#bkmk_recos)  
  
-   [Чувствительность к регистру идентификаторов объекта](#bkmk_objid)  
  
-   [Тестирование языкового стандарта с помощью Excel и SQL Server Profiler](#bkmk_test)  
  
-   [Написание MDX-запросов в решении, содержащем переводы](#bkmk_mdx)  
  
-   [Написание MDX-запросов, содержащих значения даты и времени](#bkmk_datetime)  
  
##  <a name="bkmk_sameColl"></a> Использование одинаковых параметров сортировки во всем стеке  
 Если это возможно, попробуйте использовать те же параметры сортировки в [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , которые применяются для компонента Database Engine, чтобы добиться соответствия чувствительности к ширине, регистру и диакритическим знакам.  
  
 Каждая служба имеет свои собственные параметры сортировки. По умолчанию для ядра СУБД используется SQL_Latin1_General_CP1_CI_AS, а для Analysis Services — Latin1_General_AS. Значения по умолчанию совместимы с точки зрения чувствительности к регистру, ширине и диакритическим знакам. Помните, что, если изменить какие-либо параметры сортировки, могут возникнуть проблемы, если свойства параметров сортировки существенно отличаются.  
  
 Даже если параметры сортировки функционально эквивалентны, может возникнуть особый случай, где пустое место в любом месте строки интерпретируется каждой службой по-разному.  
  
 Символ пробела — это особый случай, так как он может быть представлен однобайтовым (SBCS) или двухбайтовым (DBCS) набором символов в кодировке Юникод. В реляционном механизме две составные строки, разделенные пробелом (одна из которых использует SBCS, а другая —DBCS), считаются идентичными. Во время обработки в службах Analysis Services те же составные строки не совпадают, а второй экземпляр будет отмечен как дубликат.  
  
 Дополнительные сведения и рекомендуемые пути устранения проблем см. в разделе [Пробелы в строке Юникода обрабатываются по-разному в зависимости от параметров сортировки](https://social.technet.microsoft.com/wiki/contents/articles/23979.ssas-processing-error-blanks-in-a-unicode-string-have-different-processing-outcomes-based-on-collation-and-character-set.aspx).  
  
##  <a name="bkmk_recos"></a> Общие рекомендации для параметров сортировки  
 В Analysis Services всегда представлен полный список всех доступных языков и параметров сортировки; список параметров сортировки не отфильтровывается в зависимости от выбранного языка. Обязательно выберите пригодное для работы сочетание.  
  
 Некоторые из наиболее часто используемых параметров сортировки перечислены в следующем списке.  
  
 Этот список следует считать основой для дальнейшей работы, но не окончательной рекомендацией, исключающей другие варианты. Может оказаться, что для ваших данных лучше всего подходят параметры сортировки, не рекомендованные явным образом. Тщательное тестирование является единственным способом проверить правильность сортировки и сравнения данных. При тестировании параметров сортировки всегда запускайте нагрузку по обработке и по запросам.  
  
-   Latin1_General_100_AS часто используется для приложений, использующих 26 букв [основного латинского алфавита ISO](http://en.wikipedia.org/wiki/ISO_basic_Latin_alphabet).  
  
-   В языках стран Северной Европы, где встречаются скандинавские буквы (например, ø), можно использовать Finnish_Swedish_100.  
  
-   В языках Восточной Европы, например в русском, часто используется Cyrillic_General_100.  
  
-   Китайский язык и параметры сортировки различаются в зависимости от региона, но чаще всего это либо китайский (упрощенное письмо), либо китайский (традиционное письмо).  
  
     В КНР и Сингапуре служба поддержки Майкрософт обычно применяет китайский (упрощенное письмо) и порядок сортировки пиньинь. Рекомендуемые параметры сортировки: Chinese_PRC (для SQL Server 2000), Chinese_PRC_90 (для SQL Server 2005) или Chinese_Simplified_Pinyin_100 (SQL Server 2008 и более поздних версий).  
  
     В Тайваньском стандарте рекомендуется использовать традиционный китайский, а рекомендуемый порядок сортировки основан на количестве штрихов: Chinese_Taiwan_Stroke (для SQL Server 2000), Chinese_Taiwan_Stroke_90 (для SQL Server 2005) или Chinese_Traditional_Stroke_Count_100 (для SQL Server 2008 и более поздних версий).  
  
     Другие регионы (например, Гонконг и Макао) также используют традиционный китайский. Для сортировке в Гонконге часто используется Chinese_Hong_Kong_Stroke_90 (в SQL Server 2005). В Макао Chinese_Traditional_Stroke_Count_100 (в SQL Server 2008 и более поздних версиях) используется довольно часто.  
  
-   Для японского языка наиболее часто используется Japanese_CI_AS. Japanese_XJIS_100 применяется в установках, поддерживающих [JIS2004](http://en.wikipedia.org/wiki/JIS_X_0213). Japanese_BIN2 обычно применяется в проектах миграции данных, где исходные данные получены с платформ, отличных от Windows, или из источников данных, отличных от реляционной СУБД SQL Server.  
  
     Japanese_Bushu_Kakusu_100 редко встречается на серверах с Analysis Services.  
  
-   Для корейского языка рекомендуется использовать Korean_100. В списке есть и Korean_Wansung_Unicode, но эта сортировка считается устаревшей.  
  
##  <a name="bkmk_objid"></a> Чувствительность к регистру идентификаторов объекта  
 Начиная с SQL Server 2012 SP2 учет регистра идентификаторов объектов применяется независимо от параметров сортировки, но поведение зависит от языка.  
  
|Набор знаков|Учет регистра букв|  
|---------------------|----------------------|  
|**Основной латинский алфавит**|Идентификаторы объектов, выраженные латинским алфавитом (любой из 26 английских символов верхнего или нижнего регистра), обрабатываются без учета регистра независимо от параметров сортировки. Например, следующие идентификаторы объектов считаются идентичными: 54321**abcdef**, 54321**abcdef**, 54321**abcdef**. Службы Analysis Services обрабатывают символы в строке так, будто все они прописные, а затем выполняют простое побайтное сравнение, которое не зависит от языка.<br /><br /> Обратите внимание, что затрагиваются только 26 символов. У западноевропейских языков со скандинавскими символами дополнительные символы не будут в верхнем регистре.|  
|**Кириллица, греческий, коптский, армянский**|В идентификаторах объектов на языках с письмом, отличным от латинского, где строчные и заглавные буквы различаются, всегда учитывается регистр. Например, "Измерение" и "измерение" считаются различными значениями, хотя единственная разница — первая буква.|  
  
 **Влияния учета регистра в идентификаторах объектов**  
  
 Только к идентификаторам, а не именам объектов применяются типы поведения, описанные в таблице. Если вы заметите изменения в работе решения (после установки SQL Server 2012 SP2 или более поздней версии), то это изменение, по всей видимости, будет связано с обработкой. Идентификаторы объектов не влияют на запросы. Для обоих языков запросов (DAX и MDX) механизм обработки формул использует имя объекта (а не идентификатор).  
  
> [!NOTE]  
>  Изменения кода, связанные с учета регистра, были критическими изменениями для некоторых приложений. Дополнительные сведения см. [в разделе критические изменения Analysis Services функций в SQL Server 2014](breaking-changes-to-analysis-services-features-in-sql-server-2014.md) .  
  
##  <a name="bkmk_test"></a> Тестирования языков с помощью Excel, SQL Server Profiler и SQL Server Management Studio  
 При тестировании переводов соединение должно указывать код языка перевода. Как указано в разделе [Получение другого языка из служб SSAS в Excel](http://extremeexperts.com/sql/Tips/ExcelDiffLocale.aspx), для тестирования переводов можно использовать Excel.  
  
 Это можно сделать вручную, добавив в ODC-файл свойство строки подключения кода языка. Попробуйте этот подход с примером многомерной базы данных Adventure Works.  
  
-   Найдите существующие ODC-файлы. Затем найдите файл для многомерной базы данных Adventure Works и щелкните правой кнопкой мыши файл, чтобы открыть его в программе "Блокнот".  
  
-   Добавьте `Locale Identifier=1036` в строку подключения. Сохраните и закройте файл.  
  
-   Откройте Excel | Выберите **Данные** | **Существующие подключения**. Отфильтруйте список, чтобы показать только файлы подключений на этом компьютере. Найдите подключение для Adventure Works (внимательно посмотрите на имя, их может быть несколько). Откройте соединение.  
  
     Вы увидите переводы на французский из образца базы данных Adventure Works.  
  
     ![Сводная таблица Excel с переводом на французский](media/ssas-localetest-excel.png "Сводная таблица Excel с переводом на французский")  
  
 Затем можно использовать приложение SQL Server Profiler для подтверждения кода языка. Щелкните событие `Session Initialize` , а затем найдите `<localeidentifier>1036</localeidentifier>`в текстовом поле под списком свойств.  
  
 В среде Management Studio можно указать код языка для соединения с сервером.  
  
-   В обозревателе объектов последовательно выберите **Подключения** | **Службы Analysis Services** | **Параметры**и откройте вкладку **Дополнительные параметры соединения** .  
  
-   Введите `Local Identifier=1036` и нажмите кнопку **Подключение**.  
  
-   Выполните MDX-запрос к базе данных Adventure Works. Результатами запроса должны быть переводы на французский.  
  
     ![Запрос многомерных выражений с переводом на французский в SSMS](media/ssas-localetest-ssms.png "Запрос многомерных выражений с переводом на французский в SSMS")  
  
##  <a name="bkmk_mdx"></a> Написание MDX-запросов в решении, содержащем переводы  
 Переводы предоставляют отображаемые сведения об именах объектов служб [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , однако идентификаторы тех же самых объектов не переводятся. По возможности для объектов служб [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] необходимо использовать идентификаторы и ключи, а не переведенные заголовки и имена. Например, для обеспечения мобильности в нескольких языках необходимо использовать ключи элементов, а не имена элементов для инструкций многомерных выражений и скриптов.  
  
> [!NOTE]  
>  Помните, что в именах табличных объектов регистр никогда не учитывается, независимо от параметров сортировки. В именах многомерных объектов, напротив, регистр учитывается таким же образом, как в параметрах сортировки. Поскольку регистр учитывается только в именах многомерных объектов, убедитесь, что все запросы MDX, ссылающиеся на многомерные объекты, имеют правильный регистр.  
  
##  <a name="bkmk_datetime"></a> Написание MDX-запросов, содержащих значения даты и времени  
 Следующие рекомендации помогут удобнее переносить запросы MDX на основе даты и времени на разные языки:  
  
1.  **Использование числовых частей для сравнения и операций**  
  
     При выполнении операций и сравнений месяцев и дней недели используйте числовые части даты и времени, а не строковые эквиваленты (например, используйте MonthNumberofYear вместо MonthName). Числовые значения в меньше степени затрагиваются различиями в переводах.  
  
2.  **Использование строковых эквивалентов в результирующем наборе**  
  
     При построении результирующих наборов, видимых конечным пользователям, используйте строки (например, MonthName), чтобы многоязычная аудитория могла пользоваться предоставленными переводами.  
  
3.  **Использование форматов даты ISO для получения универсальных сведений о дате и времени**  
  
     У одного [эксперта Analysis Services](http://geekswithblogs.net/darrengosbell/Default.aspx) есть следующие рекомендации: "Я всегда использую формат даты ISO гггг-мм-дд для любых строк даты, передаваемых в запросы в SQL или многомерных выражениях, так как это неоднозначное и будет работать независимо от региональных параметров клиента или сервера. Я соглашусь с тем, что сервер должен игнорировать свои региональные настройки при синтаксическом анализе неоднозначного формата даты, но я также думаю, если у вас есть вариант, интерпретируемый одинаково, лучше остановиться на нем".  
  
4.  `Use the Format function to enforce a specific format, regardless of regional language settings`  
  
     В следующем запросе MDX, взятом из публикации на форуме, показано использование параметра Format для возврата данных в определенном формате вне зависимости от базовых региональных параметров.  
  
     Исходное сообщение см. в записи на форуме [SSAS 2012 создает недопустимые даты (Network Steve)](http://www.networksteve.com/forum/topic.php/SSAS_2012_generates_invalid_dates/?TopicId=40504&Posts=2) .  
  
    ```  
    WITH MEMBER [LinkTimeAdd11Date_Manual] as Format(dateadd("d",15,"2014-12-11"), "mm/dd/yyyy")  
    member [LinkTimeAdd15Date_Manual] as Format(dateadd("d",11,"2014-12-13"), "mm/dd/yyyy")  
    SELECT  
    { [LinkTimeAdd11Date_Manual]  
    ,[LinkTimeAdd15Date_Manual]  
    }  
    ON COLUMNS   
    FROM [Adventure Works]  
  
    ```  
  
## <a name="see-also"></a>См. также  
 [Сценарии глобализации для Analysis Services многомерных](globalization-scenarios-for-analysis-services-multiidimensional.md)   
 [Написание инструкций Transact-SQL, адаптированных к международному использованию](../relational-databases/collations/write-international-transact-sql-statements.md)  
  
  
