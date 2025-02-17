---
title: Использование поставщика PowerShell для расширенных событий | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xevents
ms.topic: conceptual
helpviewer_keywords:
- PowerShell [SQL Server], xevent
- extended events [SQL Server], PowerShell
- PowerShell [SQL Server], extended events
ms.assetid: 0b10016f-a479-4444-a484-46cb4677cf64
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ea4432b07007ce1bbc4ec5b944594b204a7ad808
ms.sourcegitcommit: a165052c789a327a3a7202872669ce039bd9e495
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/22/2019
ms.locfileid: "72782909"
---
# <a name="use-the-powershell-provider-for-extended-events"></a>Использование поставщика PowerShell для расширенных событий
  Управлять расширенными событиями [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] можно с помощью поставщика [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell. Вложенная папка XEvent находится на диске SQLSERVER. Получить доступ к папке можно одним из следующих способов.  
  
-   В командной строке введите команду `sqlps` и нажмите клавишу ВВОД. Введите `cd xevent` и нажмите клавишу ВВОД. В нем можно использовать команды **CD** и `dir` (или командлеты **Set-Location** и **Get-ChildItem** ), чтобы перейти к имени сервера и имени экземпляра.  
  
-   В обозревателе объектов разверните узел имени экземпляра, разверните узел **Управление**, щелкните правой кнопкой мыши **Расширенные события**и выберите команду **Запустить PowerShell**. Оболочка PowerShell будет запущена в следующем пути:  
  
     PS SQLSERVER:\XEvent\\*ServerName*\\*InstanceName*>  
  
    > [!NOTE]  
    >  Запустить PowerShell можно из любого узла в категории **Расширенные события**. Например, можно щелкнуть правой кнопкой мыши **Сеансы**, а затем выбрать команду **Запустить PowerShell**. При этом оболочка PowerShell будет запущена на один уровень ниже, в папке «Сеансы».  
  
 В дереве папки XEvent можно просматривать существующие сеансы расширенных событий и связанные с ними события, цели и предикаты. Например, если в поле PS SQLSERVER: \ XEvent\\*имя_сервера*\\*instanceName*> путь, введите `cd sessions`, нажмите клавишу ВВОД, введите `dir`и нажмите клавишу ВВОД, чтобы просмотреть список сеансов, хранящихся в этом экземпляре. Также можно проверить, выполняется ли сеанс в данный момент (и если выполняется, то в течение какого периода), а также задан ли запуск сеанса вместе с запуском экземпляра.  
  
 Для просмотра событий, их предикатов и целей, связанных с сеансом, можно изменить имена каталогов на имя сеанса и затем просматривать либо папку событий, либо папку целей. Например, чтобы просмотреть события и их предикаты, связанные с сеансом исправности системы по умолчанию, в поле PS SQLSERVER: \ XEvent\\*имя_сервера*\\*имя_экземпляра*\сессионс > путь введите `cd system_health\events,` нажмите клавишу ВВОД. `dir`и нажмите клавишу ВВОД.  
  
 Поставщик [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell предоставляет широкий набор функций для создания, изменения сеансов расширенных событий и управления ими. В следующем разделе приведены некоторые простые примеры использования скриптов PowerShell с расширенными событиями.  
  
## <a name="examples"></a>Примеры  
 В приведенных далее примерах обратите внимание на следующие моменты.  
  
-   Скрипты должны запускаться из командной строки PS SQLSERVER:\\> (для этого введите `sqlps` в командной строке).  
  
-   Скрипты используют экземпляр [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] по умолчанию.  
  
-   Скрипты должны сохраняться с расширением PS1.  
  
-   Политика выполнения PowerShell должна разрешать выполнения скриптов. Чтобы задать политику выполнения, воспользуйтесь командлетом **Set-Executionpolicy** . (Для получения дополнительных сведений введите `get-help set-executionpolicy -detailed` и нажмите клавишу ВВОД.)  
  
 Следующий скрипт создает новый сеанс с именем «TestSession».  
  
```powershell
#Script for creating a session.  
cd XEvent  
$h = hostname  
cd $h  
  
#Use the default instance.  
$store = dir | where {$_.DisplayName -ieq 'default'}  
$session = New-Object Microsoft.SqlServer.Management.XEvent.Session -ArgumentList $store, "TestSession"  
$event = $session.AddEvent("sqlserver.file_written")  
$event.AddAction("package0.callstack")  
$session.Create()  
```  
  
 Следующий скрипт добавляет цель «Кольцевой буфер» в сеанс, созданный в предыдущем примере. (В этом примере демонстрируется использование метода `Alter`. Помните, что добавлять цель можно только после создания сеанса.)  
  
```powershell
#Script to alter a session.  
cd XEvent  
$h = hostname  
cd $h  
cd DEFAULT\Sessions  
  
#Used to find the specified session.  
$session = dir | where {$_.Name -eq 'TestSession'}  
  
#Add the ring buffer target and call the Alter method.  
$session.AddTarget("package0.ring_buffer")  
$session.Alter()  
```  
  
 Следующий скрипт создает новый сеанс, в котором используется выражение предиката. В данном случае сеанс собирает сведения о времени записи в файл c:\temp.log (с помощью события sqlserver.file_written).  
  
```powershell
#Script for creating a session.  
cd XEvent  
$h = hostname  
cd $h  
  
#Use the default instance.  
$store = dir | where {$_.DisplayName -ieq 'default'}  
$session = New-Object Microsoft.SqlServer.Management.XEvent.Session -ArgumentList $store, "TestSession2"  
$event = $session.AddEvent("sqlserver.file_written")  
  
#Construct a predicate "equal_i_unicode_string(path, N'c:\temp.log')".  
$column = $store.SqlServerPackage.EventInfoSet["file_written"].DataEventColumnInfoSet["path"]  
$operand = new-object Microsoft.SqlServer.Management.XEvent.PredOperand -argumentlist $column  
$value = new-object Microsoft.SqlServer.Management.XEvent.PredValue -argumentlist "c:\temp.log"  
$compare = $store.Package0Package.PredCompareInfoSet["equal_i_unicode_string"]  
$predicate = new-object Microsoft.SqlServer.Management.XEvent.PredFunctionExpr -ArgumentList $compare, $operand, $value  
$event.SetPredicate($predicate)  
$session.Create()  
```  
  
## <a name="security"></a>безопасность  
 Чтобы создать, изменить или удалить сеанс расширенных событий, требуется разрешение ALTER ANY EVENT SESSION.  
  
## <a name="see-also"></a>См. также статью  
 [SQL Server PowerShell](../../powershell/sql-server-powershell.md)   
 [Использование сеанса system_health](use-the-ssms-xe-profiler.md)   
 [Средства расширенных событий](extended-events-tools.md)  
