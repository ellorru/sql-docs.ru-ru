---
title: Обновление PowerPivot для SharePoint | Документация Майкрософт
ms.custom: ''
ms.date: 03/25/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: 80ba9e43-f3f0-4730-9fb1-2afd2dd3e6fc
author: Minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 78112ef90eab7b6b6dd881474d04a350f6ea6ca0
ms.sourcegitcommit: a165052c789a327a3a7202872669ce039bd9e495
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/22/2019
ms.locfileid: "72783168"
---
# <a name="upgrade-powerpivot-for-sharepoint"></a>Обновление PowerPivot для SharePoint
  В этом разделе описаны шаги, необходимые для обновления развертывания [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] до [!INCLUDE[ssGeminiLong](../../includes/ssgeminilong-md.md)]. Конкретная последовательность действий зависит от версии SharePoint вашей среды и включает надстройку PowerPivot для SharePoint (**spPowerPivot.msi**).  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]**  SharePoint 2010 | SharePoint 2013  
  
 Сведения о выпуске см. в разделе [Заметки о выпуске SQL Server 2014](https://go.microsoft.com/fwlink/?LinkID=296445).  
  

  
## <a name="background"></a>Историческая справка  
  
-   При обновлении многосерверной фермы SharePoint 2010 с двумя или более экземпляров [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] необходимо полностью обновить каждый сервер, **прежде** чем переходить к следующему серверу. Полное обновление включает запуск программы установки SQL Server для обновления программных файлов [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] , вслед за чем выполняются действия по обновлению SharePoint, которые состоят в настройке обновленных служб. Доступность сервера будет ограниченна, пока не выполнены действия по обновлению в подходящем средстве настройки PowerPivot или Windows PowerShell.  
  
-   Все экземпляры служб PowerPivot System Service и Analysis Services в ферме SharePoint 2010 должны иметь одинаковые версии. Сведения о том, как проверить версию, см. в разделе [Проверка версий компонентов и служб PowerPivot](#bkmk_verify_versions) в этой статье.  
  
-   Средства настройки PowerPivot — это одни из общих компонентов SQL Server. Все общие компоненты обновляются одновременно. Если во время обновления будут выбраны другие экземпляры SQL Server или функции, для которых требуется обновление общих компонентов, то средство настройки PowerPivot также будет обновлено. Если средство настройки PowerPivot было обновлено, а экземпляр PowerPivot не был, могут возникнуть проблемы. Дополнительные сведения о SQL Server общих компонентах см. в статье [обновление до SQL Server 2014 с помощью &#40;мастера&#41;установки](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md).  
  
-   Надстройка PowerPivot для SharePoint (**spPowerPivot.msi**) устанавливается параллельно с предыдущими версиями. Например, надстройка [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] устанавливается в папку `c:\Program Files\Microsoft SQL Server\120\Tools\PowerPivotTools`.  
  

  
##  <a name="bkmk_prereq"></a> предварительные требования  
 **Permissions**  
  
-   Чтобы обновить PowerPivot для SharePoint, пользователь должен быть администратором фермы. Для запуска программы установки SQL Server необходимо быть локальным администратором.  
  
-   Необходимо иметь разрешения **db_owner** в базе данных конфигураций фермы.  
  
 **SQL Server:**  
  
-   Если существующая установка PowerPivot имеет версию [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], то для обновления до [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]  [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)].  
  
-   Если существующая установка PowerPivot имеет версию [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], то для обновления до [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)].  
  
 **SharePoint 2010.**  
  
-   Если существующая установка выполняет SharePoint 2010, установите пакет обновления 2 (SP2) для SharePoint 2010 перед обновлением до [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]. Дополнительные сведения см. в разделе [Пакет обновления 2 (SP2) для Microsoft SharePoint 2010](https://www.microsoft.com/download/details.aspx?id=39672). Используйте команду PowerShell `(Get-SPfarm).BuildVersion.ToString()` , чтобы проверить версию. Для получения информации о дате выпуска по версии сборки см. раздел [Номера сборок в SharePoint 2010](http://www.toddklindt.com/blog/Lists/Posts/Post.aspx?ID=224).  
  
 
  
##  <a name="bkmk_uprgade_sharepoint2013"></a> Обновление существующей фермы SharePoint 2013  
 Для обновления [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] , развернутых в SharePoint 2013, выполните следующие действия.  
  
 ![Обновление PowerPivot для SharePoint 2013](../../../2014/sql-server/install/media/as-powepivot-upgrade-flow-sharepoint2013.png "Обновление PowerPivot для SharePoint 2013")  
  
1.  Запустите программу установки [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] на внутренних серверах, выполняющих [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] в режиме интеграции с SharePoint. Если сервер содержит несколько экземпляров [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], обновите по крайней мере экземпляр **POWERPIVOT** . В следующем списке приведена сводка шагов мастера установки, относящихся к обновлению [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] :  
  
    1.  В мастере установки [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] нажмите кнопку **Установка**.  
  
    2.  Выберите **Обновление с SQL Server...** .  
  
    3.  На странице **Выбор экземпляра** выберите экземпляр с именем **POWERPIVOT** и нажмите кнопку **Далее**.  
  
    4.  Дополнительные сведения см. в статье [обновление до SQL Server 2014 с помощью мастера &#40;&#41; установки](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md) .  
  
2.  Перезапустите сервер.  
  
3.  Запустите надстройку [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] для SharePoint (**spPowerPivot.msi**) на каждом сервере в ферме SharePoint 2013, чтобы установить поставщики данных. Исключением будут серверы, где вы запустили мастер установки SQL Server, который также обновляет поставщики данных. Дополнительные сведения см. [в разделе Установка или удаление надстройки &#40;PowerPivot для SharePoint SharePoint 2013&#41;](https://docs.microsoft.com/analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013).  
  
4.  **Запустите средство настройки PowerPivot для SharePoint 2013** на одном из серверов приложений SharePoint для настройки фермы SharePoint на работу с обновленными файлами решения, которые установила надстройка. На этом шаге нельзя использовать центр администрирования SharePoint. Дополнительные сведения см. в следующих разделах:  
  
    1.  На начальной странице в Windows введите **PowerPivot** и в результатах поиска щелкните **Настройка PowerPivot для SharePoint 2013**. Обратите внимание, что в результатах поиска могут быть возвращены обе версии средства настройки.  
  
         ![два средства PowerPivot два](https://docs.microsoft.com/analysis-services/analysis-services/media/as-powerpivot-configtools-bothicons.gif "два средства PowerPivot два")  
  
         либо  
  
         В меню **Пуск** последовательно выберите пункты **Все программы**, [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], **Средства настройки**, **Средство настройки PowerPivot для SharePoint 2013**. Обратите внимание, что это средство присутствует в списке вариантов, только если на локальном сервере установлен компонент [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)].  
  
    2.  Во время запуска средство настройки проверяет состояние обновления решения фермы и решений веб-приложений PowerPivot. Если обнаружены более старые версии этих решений, вы увидите сообщение "**обнаружены более новые версии файлов решения PowerPivot. Выберите вариант обновления для обновления фермы**". Нажмите кнопку **ОК** , чтобы закрыть сообщение проверки системы.  
  
    3.  Выберите **Удаление компонентов, служб, приложений и решений**и нажмите кнопку **ОК**.  
  
    4.  Просмотрите действия в списке задач левой панели и исключите те, которые не хотите применять. По умолчанию в список включены все действия. Чтобы удалить действие, выберите его в левом списке задач и снимите флажок напротив параметра **Включить это действие в список задач** на странице **Параметры** .  
  
    5.  При необходимости просмотрите подробную информацию на вкладке **Скрипт** или **Вывод** .  
  
         Вкладка «Вывод» содержит краткое описание действий, которые будут выполнены средством. Эти сведения сохраняются в файлах журналов, расположенных в папке `C:\Program Files\Microsoft SQL Server\120\Tools\PowerPivotTools\SPAddinConfiguration\Log`.  
  
         Вкладка «Скрипт» содержит командлеты PowerShell или ссылки на файлы скриптов PowerShell, которые будут выполнены средством.  
  
    6.  Нажмите кнопку **Проверка** , чтобы убедиться, что каждое действие является допустимым. Если кнопка **Проверка** недоступна, значит, все действия являются допустимыми. Если кнопка **Проверка** доступна, возможно, вы изменили входное значение (например, имя приложения службы Excel), либо средство определило, что определенное действие выполнить невозможно. Если действие не может быть выполнено, следует исключить его или исправить базовые условия, из-за которых действие было отмечено как недопустимое.  
  
        > [!IMPORTANT]  
        >  Первое действие, **Обновление решения фермы**, должно всегда обрабатываться в первую очередь. Это действие регистрирует командлеты PowerShell, которые используются для настройки сервера. При получении ошибки, связанной с этим действием, не продолжайте операцию. Вместо этого используйте сведения из сообщения об ошибке для диагностики и разрешения проблемы, прежде чем обрабатывать другие действия в списке задач.  
  
    7.  Нажмите кнопку **Запуск** , чтобы выполнить все действия, которые являются допустимыми для данной задачи. Кнопка**Запуск** становится доступной только после прохождения проверки. При нажатии кнопки **выполнить**появится следующее предупреждение, в котором будет показано, что действия обрабатываются в пакетном режиме: "**все параметры конфигурации, помеченные как допустимые в средстве, будут применены к ферме SharePoint. Вы хотите продолжить?** ".  
  
    8.  Чтобы продолжить, нажмите кнопку **Да** .  
  
    9. Обновление решений и компонентов в ферме может занять несколько минут. В течение этого времени запросы на подключение к данным PowerPivot **будут завершаться** с ошибками, похожими на "**не удается обновить данные**" или "при**попытке выполнить запрошенное действие произошла ошибка. Повторите попытку**". После завершения обновления сервер станет доступным, и эти ошибки больше не будут возникать.  
  
     Дополнительные сведения см. в следующих разделах:  
  
    -   [Средства настройки PowerPivot](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/power-pivot-configuration-tools)  
  
    -   [Настройка или восстановление PowerPivot для SharePoint 2013 &#40;средства настройки PowerPivot&#41;](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/configure-or-repair-power-pivot-for-sharepoint-2013)  
  
    -   [Настройка PowerPivot с помощью Windows PowerShell](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/power-pivot-configuration-using-windows-powershell)  
  
    -   [Справочник по PowerShell для PowerPivot для SharePoint](/sql/analysis-services/powershell/powershell-reference-for-power-pivot-for-sharepoint)  
  
5.  Убедитесь, что обновление выполнено успешно, выполнив шаги после завершения обновления и проверив версию серверов PowerPivot в ферме. Подробные сведения см. в разделе [Post-upgrade verification tasks](#verify) и следующем разделе.  
  
 
  
##  <a name="bkmk_uprgade_sharepoint2010"></a> Обновление существующей фермы SharePoint 2010  
 Для обновления [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] , развернутых в SharePoint 2010, выполните следующие действия.  
  
 ![Обновление PowerPivot для SharePoint 2010](../../../2014/sql-server/install/media/as-powepivot-upgrade-flow-sharepoint2010.png "Обновление PowerPivot для SharePoint 2010")  
  
1.  Загрузите [Пакет обновления 2 (SP2) для Microsoft SharePoint 2010](https://www.microsoft.com/download/details.aspx?id=39672) и примените его на всех серверах в ферме. Проверьте успешность установки SharePoint с пакетом обновления 2 (SP2). В центре администрирования на странице «Обновление и миграция» откройте страницу состояния «Проверка установки продукта и обновлений», чтобы просмотреть сообщения о состоянии, относящиеся к пакету обновления 2 (SP2).  
  
2.  Убедитесь, что служба администрирования Windows SharePoint 2010 запущена.  
  
    ```powershell
    Get-Service | Where {$_.displayname -like "*SharePoint*"}  
    ```  
  
3.  Убедитесь, что службы **SharePoint** **SQL Server Analysis Services** и **SQL Server PowerPivot System Service** запущены в центре администрирования SharePoint, или выполните следующую команду PowerShell:  
  
    ```powershell
    Get-SPServiceInstance | where {$_.typename -like "*sql*"}  
    ```  
  
4.  Убедитесь, что службы **Windows** **Службы SQL Server Analysis Services (PowerPivot)** запущены.  
  
    ```powershell
    Get-Service | where {$_.displayname -like "*powerpivot*"}  
    ```  
  
5.  **Запустите программу установки [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Установку** на первом сервере приложений SharePoint, где запущена служба Windows **Службы SQL Server Analysis Services (PowerPivot)** , чтобы обновить экземпляр POWERPIVOT. На странице «Установка» мастера установки SQL Server выберите вариант обновления. Дополнительные сведения см. в статье [Upgrade to SQL Server 2014 с помощью мастера &#40;&#41;установки](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md).  
  
6.  **Перезапустите сервер** перед запуском средства настройки. В этом случае любые обновления или необходимые компоненты, установленные программой установки SQL Server, будут полностью настроены в системе.  
  
7.  **Запустите средство настройки PowerPivot** на первом сервере приложений SharePoint, на котором запущена служба SQL Server Analysis Services (PowerPivot), чтобы обновить решения и веб-службы в SharePoint. На этом шаге нельзя использовать центр администрирования.  
  
    1.  В меню **Пуск** последовательно укажите пункты **Все программы**, щелкните [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], щелкните **Средства настройки**и выберите пункт **Средство настройки PowerPivot**. Обратите внимание, что это средство присутствует в списке вариантов, только если на локальном сервере установлен компонент [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)].  
  
    2.  Во время запуска средство настройки проверяет состояние обновления решения фермы и решений веб-приложений PowerPivot. Если обнаружены более старые версии этих решений, вы увидите сообщение "обнаружены более новые версии файлов решения PowerPivot. Выберите параметр обновления для обновления фермы". Нажмите кнопку **OК** , чтобы закрыть окно сообщения.  
  
    3.  Для продолжения выберите **Обновление компонентов, служб, приложений и решений**и нажмите кнопку **ОК** .  
  
    4.  Появится следующее предупреждение: "книги на панели управления PowerPivot будут обновлены до последней версии. Все настройки, внесенные в существующие книги, будут утеряны. Продолжить?".  
  
         Это предупреждение относится к книгам на панели управления PowerPivot, связанным с обновлением данных. Если эти книги были настроены, изменения, внесенные в книги, будут утеряны при замене существующих файлов файлами новой версии.  
  
         Нажмите кнопку **Да** для перезаписи книг книгами более новой версии. В противном случае нажмите кнопку **Нет** , чтобы вернуться на главную страницу. Сохраните книги в другой папке, чтобы иметь их копии, и затем вернитесь к этому шагу для продолжения.  
  
         Дополнительные сведения о настройке книг, используемых на панели управления, см. в разделе [Настройка панели управления PowerPivot](https://go.microsoft.com/fwlink/?linkID=229639).  
  
    5.  Просмотрите действия в списке задач и исключите те, которые средство настройки не должно выполнять. По умолчанию в список включены все действия. Чтобы удалить действие, выберите его в списке задач и снимите флажок напротив параметра **Включить это действие в список задач** на странице «Параметры».  
  
    6.  При необходимости просмотрите подробную информацию на вкладке **Вывод** или **Скрипт** .  
  
         Вкладка «Вывод» содержит краткое описание действий, которые будут выполнены средством. Эти сведения сохраняются в файлах журналов, расположенных в папке `c:\Program Files\Microsoft SQL Server\120\Tools\PowerPivotTools\ConfigurationTool\Log`.  
  
         Вкладка «Скрипт» содержит командлеты PowerShell или ссылки на файлы скриптов PowerShell, которые будут выполнены средством.  
  
    7.  Нажмите кнопку **Проверка** , чтобы убедиться, что каждое действие является допустимым. Если кнопка **Проверка** недоступна, значит, все действия являются допустимыми. Если кнопка **Проверка** доступна, возможно, вы изменили входное значение (например, имя приложения службы Excel), либо средство определило, что определенное действие выполнить невозможно. Если действие не может быть выполнено, следует исключить его или исправить базовые условия, из-за которых действие было отмечено как недопустимое.  
  
        > [!IMPORTANT]  
        >  Первое действие, **Обновление решения фермы**, должно всегда обрабатываться в первую очередь. Это действие регистрирует командлеты PowerShell, которые используются для настройки сервера. При получении ошибки, связанной с этим действием, не продолжайте операцию. Вместо этого используйте сведения из сообщения об ошибке для диагностики и разрешения проблемы, прежде чем обрабатывать другие действия в списке задач.  
  
    8.  Нажмите кнопку **Запуск** , чтобы выполнить все действия, которые являются допустимыми для данной задачи. Кнопка**Запуск** становится доступной только после прохождения проверки. При нажатии кнопки **Запуск** появится предупреждение о том, что действия обрабатываются в пакетном режиме: "Все параметры конфигурации, помеченные средством как действительные, будут применены к ферме SharePoint. Продолжить?".  
  
    9. Чтобы продолжить, нажмите кнопку **Да** .  
  
    10. Обновление решений и компонентов в ферме может занять несколько минут. В течение этого времени запросы на соединение с данными PowerPivot завершатся ошибкой, например "не удалось обновить данные" или "произошла ошибка при попытке выполнить запрошенное действие. Повторите попытку". После завершения обновления сервер станет доступным, и эти ошибки больше не будут возникать.  
  
8.  **Повторите эту процедуру** для каждой службы SQL Server Analysis Services (PowerPivot) в ферме: 1) запустите SQL Server Setup 2) запустите средство настройки PowerPivot.  
  
9. Убедитесь, что обновление выполнено успешно, выполнив шаги после завершения обновления и проверив версию серверов PowerPivot в ферме. Подробные сведения см. в разделе [Post-upgrade verification tasks](#verify) и следующем разделе.  
  
10. **Устранение ошибок**  
  
     На панели «Параметры» для каждого действия можно просмотреть сведения об ошибке.  
  
     Для решения проблем, связанных с развертыванием или откатом решения, убедитесь, что служба администрирования SharePoint 2010 запущена. Эта служба запускает задания таймера, которые вызывают изменения конфигурации фермы. Если служба не запущена, развертывание или откат решения будет невозможен. Повторяющиеся ошибки указывают на то, что существующее задание развертывания или отката уже поставлено в очередь и происходит блокирование дальнейших действий средства настройки.  
  
    1.  Запустите консоль управления SharePoint 2010 с учетной записью администратора и выполните следующую команду для просмотра заданий, поставленных в очередь:  
  
        ```cmd
        stsadm -o enumdeployments  
        ```  
  
    2.  Просмотрите существующие развертывания для уточнения следующих сведений: **Тип** — откат или развертывание, **Файл** — powerpivotwebapp.wsp или powerpivotfarm.wsp.  
  
    3.  Для развертываний или реотзывов, связанных с решениями PowerPivot, скопируйте значение GUID для **JOBID** и вставьте его в следующую команду (используйте команды "отметить", "Копировать" и "вставить" в меню "Правка" оболочки, чтобы скопировать GUID):  
  
        ```cmd
        stsadm -o canceldeployment -id "<GUID>"  
        ```  
  
    4.  Повторите задачу в средстве настройки, нажав кнопку **Проверка** , а затем кнопку **Запуск**.  
  
     Сведения о других ошибках см. в журналах ULS. Дополнительные сведения см. в разделе [Настройка и просмотр файлов журнала SharePoint и журнала &#40;диагностики&#41;PowerPivot для SharePoint](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/configure-and-view-sharepoint-and-diagnostic-logging).  
  

  
##  <a name="bkmk_workbooks"></a> книги  
 При обновлении сервера книги PowerPivot, расположенные на сервере, не обязательно обновляются, но старые книги, созданные в предыдущей версии PowerPivot для Excel, будут работать как и прежде, используя функции, доступные в старом выпуске. Работоспособность книг сохраняется, поскольку обновленный сервер имеет версию поставщика OLE DB служб Analysis Services, который был частью предыдущей установки.  
  
  
  
##  <a name="bkmk_datarefresh"></a> Обновление данных  
 Обновление повлияет на операции обновления данных. Плановое обновление данных на сервере доступно только для книг, соответствующих версии сервера. Если имеются книги предыдущей версии, то обновление данных для этих книг может перестать работать. Чтобы снова обеспечить возможность обновления данных, необходимо выполнить обновление этих книг. Каждую книгу можно обновить вручную в PowerPivot для Excel или включить автоматическое обновление для компонента обновления данных в SharePoint 2010. Автоматическое обновление обновит книгу до текущей версии перед тем, как выполнять обновление данных, что позволяет выполнять операции обновления данных по расписанию.  
  

  
##  <a name="bkmk_verify_versions"></a>Проверка версий компонентов и служб PowerPivot  
 Все экземпляры служб [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] PowerPivot System Service и Analysis Services должны иметь одну и ту же версию. Чтобы убедиться, что все компоненты сервера имеют одну и ту же версию, проверьте сведения о версии следующих объектов.  
  
### <a name="verify-the-version-of-powerpivot-solutions-and-the-powerpivot-system-service"></a>Проверьте версии решений PowerPivot и службы PowerPivot System Service  
 Выполните следующую команду PowerShell:  
  
```powershell
Get-PowerPivotSystemService  
```  
  
 Проверьте **CurrentSolutionVersion**. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] имеет версию 12,0.\<основной > сборки.\<дополнительный > сборки  
  
### <a name="verify-the-version-of-the-analysis-services-windows-service"></a>Проверьте версию службы Windows Analysis Services  
 Если обновлены лишь некоторые серверы [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] в ферме SharePoint 2010, экземпляр [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] на необновленных серверах будет более старым, чем версия, ожидаемая в ферме. Чтобы использовать все серверы, потребуется обновить их до одной и той же версии. Чтобы проверить версию службы Windows SQL Server Analysis Services (PowerPivot) на каждом компьютере, используйте один из следующих методов.  
  
 **Обозреватель файлов Windows**:  
  
1.  Перейдите к папке **Bin** для экземпляра [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Например, `C:\Program Files\Microsoft SQL Server\MSAS12.POWERPIVOT\OLAP\bin`.  
  
2.  Щелкните `msmdsrv.exe`правой кнопкой мыши и выберите **Свойства**.  
  
3.  Щелкните **Сведения**.  
  
4.  Версия файла [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] должна быть 12,00.\<основной > сборки.\<дополнительный > сборки.  
  
5.  Проверьте, что этот номер такой же, как у версии решения PowerPivot и версии системной службы.  
  
 **Сведения о запуске службы.**  
  
 При запуске службы PowerPivot она записывает сведения о версии в журнал событий Windows.  
  
1.  Запустите Windows `eventvwr`  
  
2.  Создайте фильтр для источника `MSOLAP$POWERPIVOT`.  
  
3.  Найдите информационное событие следующего вида:  
  
     Служба   запущена. Microsoft SQL Server Analysis Services 64 Bit Evaluation (x64) RTM **12.0.2000.8**.  
  
 **Использование PowerShell для проверки версии файла.**  
  
 Для проверки версии продукта можно использовать PowerShell. Использование PowerShell будет хорошим вариантом, если вы хотите запрограммировать в скрипте или автоматизировать проверку версии.  
  
```powershell
(Get-ChildItem "C:\Program Files\Microsoft SQL Server\MSAS12.POWERPIVOT2000\OLAP\bin\msmdsrv.exe").VersionInfo  
```  
  
 Вышеуказанная команда PowerShell возвращает информацию, аналогичную следующей.  
  
 ProductVersion   FileVersion           FileName  
  
 **12.0.2000.8** 2014.0120.200    C:\Program Files\Microsoft SQL Server\MSAS12.POWERPIVOT2000\OLAP\bin\msmdsrv.exe  
  
### <a name="verify-the-msolap-data-provider-version-on-sharepoint"></a>Проверка версии поставщика данных MSOLAP в SharePoint  
 Чтобы проверить, какие версии поставщиков OLE DB служб Analysis Services являются надежными для служб Excel, используйте следующие инструкции. Проверить настройки надежного поставщика данных служб Excel может только администратор фермы или приложения службы.  
  
1.  В разделе «Управление приложениями» центра администрирования выберите пункт **Управление приложениями служб**.  
  
2.  Щелкните имя приложения служб Excel, например **ExcelServiceApp1**.  
  
3.  Щелкните **Надежные поставщики данных**. Должна отобразиться MSOLAP.5 (поставщик Microsoft OLE DB для служб OLAP 11.0). Если вы обновили установку [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] , также будет показано MSOLAP.4 из предыдущей версии.  
  
4.  Дополнительные сведения см. в разделе [Добавление MSOLAP.5 в качестве надежного поставщика данных в службах Excel Services](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/add-msolap-5-as-a-trusted-data-provider-in-excel-services).  
  
 MSOLAP.4 описывается как поставщик OLE DB (Майкрософт) для служб OLAP 10.0. Эта версия может являться версией по умолчанию для [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] , которая устанавливается со службами Excel, или это может быть версия [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] . Версия по умолчанию, устанавливаемая SharePoint, не поддерживает доступ к данным PowerPivot. Чтобы подключиться к книгам PowerPivot на сервере SharePoint, требуется версия [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] или более поздняя. Чтобы убедиться в наличии версии [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] , используйте инструкции в предыдущем разделе, в котором описывается проверка версий путем просмотра свойств файлов.  
  
### <a name="verify-the-adomdnet-data-provider-version"></a>Проверка версии поставщика данных ADOMD.NET  
 Для определения установленной версии ADOMD.NET действуйте следующим образом. Проверить настройки надежного поставщика данных служб Excel может только администратор фермы или приложения службы.  
  
1.  На сервере приложений SharePoint перейдите к `c:\Windows\Assembly`.  
  
2.  Отсортируйте результаты по имени сборки и найдите **Microsoft.Analysis Services.Adomd.Client**.  
  
3.  Убедитесь, что у вас установлена версия 12,0. > номер сборки\<.  
  

##  <a name="geminifarm"></a>Обновление нескольких серверов PowerPivot для SharePoint в ферме SharePoint  
 В многосерверной топологии, включающей более одного сервера [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] , все экземпляры серверов и компонентов должны иметь одинаковую версию. Сервер, на котором работает более высокая версия ПО, задает уровень поддержки для всех серверов фермы. Если обновить лишь некоторые из серверов, то все оставшиеся, на которых работают предыдущие версии ПО, станут недоступными до тех пор, пока тоже не будут обновлены.  
  
 После обновления первого сервера дополнительные серверы, которые еще не обновлены, **станут недоступными**. Доступность восстанавливается после того, как все серверы начнут работать на одном и том же уровне.  
  
 Программа установки SQL Server обновляет файлы решения PowerPivot на месте на физическом компьютере, но для обновления решений, которые используются в ферме, необходимо воспользоваться средством настройки PowerPivot, описанном в предыдущем подразделе.  

##  <a name="qfe"></a>Применение QFE к экземпляру PowerPivot в ферме  
 При обновлении сервера PowerPivot для SharePoint существующие программные файлы будут обновлены до новых версий, включая исправления некоторых проблем. При применении QFE к многосерверной топологии отсутствует основной сервер, с которого нужно начинать. Поэтому обновление можно начать с любого сервера, при условии, что к остальным серверам PowerPivot в ферме будет применяться тот же QFE.  
  
 При применении QFE также необходимо выполнить шаг настройки, в котором информация о версии сервера обновляется в базе данных конфигурации фермы. Версия обновленного сервера становится новой ожидаемой версией фермы. До применения и настройки QFE на всех компьютерах экземпляры PowerPivot для SharePoint, к которым не применен QFE, будут недоступны для обработки запросов данных PowerPivot.  
  
 Следуйте данным инструкциям, чтобы обеспечить применения и правильную настройку QFE.  
  
1.  Установите обновление, следуя инструкциям, прилагаемым к QFE.  
  
2.  Запустите средство настройки PowerPivot.  
  
3.  Выберите **Удаление компонентов, служб, приложений и решений**и нажмите кнопку **ОК**.  
  
4.  Ознакомьтесь с действиями, которые включены в обновления задач и затем щелкните **Проверить**.  
  
5.  Нажмите кнопку **Выполнить** для предварительного просмотра отчета.  
  
6.  Повторите для дополнительных экземпляров PowerPivot для SharePoint в ферме.  
  
    > [!IMPORTANT]  
    >  В многосерверной среде развертывания убедитесь, что обновление применено и настроено на каждом экземпляре. Затем переходите к следующему компьютеру. Перед тем как перейти к следующему экземпляру, необходимо выполнить с помощью средства настройки PowerPivot обновление для текущего экземпляра.  
  
 Проверить сведения о версии для служб в ферме можно на странице **Проверка состояния установки продукта и обновлений** в разделе «Управление обновлением и исправлениями» центра администрирования.  
  
##  <a name="verify"></a> Задачи проверки после обновления  
 После завершения обновления выполните следующие действия, чтобы проверить работоспособность сервера.  
  
|Задача|Ссылка|  
|----------|----------|  
|Проверьте, запущена ли служба на всех компьютерах, где работает PowerPivot для SharePoint.|[Запуск и остановка PowerPivot для сервера SharePoint](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/start-or-stop-a-power-pivot-for-sharepoint-server)|  
|Проверьте активацию компонентов на уровне семейства веб-сайтов.|[Активация интеграции функций PowerPivot для семейств веб-сайтов в центре администрирования](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/activate-power-pivot-integration-for-site-collections-in-ca)|  
|Проверьте, правильно ли загружаются книги PowerPivot, открыв книгу и выбрав фильтры и срезы, чтобы выполнить запрос.|Проверьте наличие кэшированных файлов на жестком диске. Если файл присутствует в кэше, значит этот файл данных загрузился на данном физическом сервере. Ищите кэшированные файлы в папке c:\Program Files\Microsoft SQL Server\MSAS12.POWERPIVOT\OLAP\Backup.|  
|Проверьте функцию обновления данных в выбранных книгах, настроенных для поддержки обновления данных.|Самый простой способ проверки обновления данных заключается в изменении расписания обновления данных с помощью установки флажка **Обновлять при первой возможности** , чтобы операции обновления данных выполнялись немедленно. При помощи этого шага удастся определить успешность обновления данных для текущей книги. Повторите эти шаги для других часто используемых книг, чтобы убедиться, что обновление данных работает. Дополнительные сведения о планировании обновления данных см. [в разделе планирование PowerPivot для SharePoint &#40;&#41;обновления данных](../../../2014/analysis-services/schedule-a-data-refresh-powerpivot-for-sharepoint.md).|  
|Следите за отчетами об обновлении данных на панели мониторинга PowerPivot, чтобы убедиться в отсутствии ошибок.|[Панель мониторинга управления PowerPivot и данные об использовании](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/power-pivot-management-dashboard-and-usage-data)|  
  
 Дополнительные сведения о настройке параметров и компонентов PowerPivot см. [в разделе Администрирование сервера PowerPivot и настройка в центре администрирования](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration).  
  
 Пошаговые инструкции по выполнению всех задач настройки после установки см. в разделе [Начальная настройка &#40;&#41;PowerPivot для SharePoint](../../../2014/sql-server/install/initial-configuration-powerpivot-for-sharepoint.md).  

## <a name="see-also"></a>См. также статью  
 [Функции, поддерживаемые различными Выпусками SQL Server 2014](../../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)   
 [Установка PowerPivot для SharePoint 2010](../../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md)  
