---
title: "Использование Windows PowerShell в шагах агента SQL Server | Документация Майкрософт"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: powershell
ms.service: 
ms.component: powershell
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f25f7549-c9b3-4618-85f2-c9a08adbe0e3
caps.latest.revision: "10"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 0e3a5a64d8c65a722e0c235bed60daa4a9872b60
ms.sourcegitcommit: 779f3398e4e3f4c626d81ae8cedad153bee69540
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/16/2018
---
# <a name="run-windows-powershell-steps-in-sql-server-agent"></a>Использование Windows PowerShell в шагах агента SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

Агент SQL Server применяется для запуска скриптов SQL Server PowerShell в запланированное время.  
  
**Запуск PowerShell из агента SQL Server с помощью следующих средств:**  [шаг задания PowerShell](#PShellJob), [шаг задания командной строки](#CmdExecJob)  
  
> [!NOTE]
> Существует два модуля SQL Server PowerShell — **SqlServer** и **SQLPS**. Модуль **SQLPS** входит в состав установки SQL Server (для обеспечения обратной совместимости), но больше не обновляется. Самым актуальным модулем PowerShell является модуль **SqlServer**. Модуль **SqlServer** содержит обновленные версии командлетов в **SQLPS**, а также новые командлеты для поддержки последних функций SQL.  
> Предыдущие версии модуля **SqlServer** *входили* в состав среды SQL Server Management Studio (SSMS), но только с SSMS версий 16.x. Для работы PowerShell с SSMS 17.0 и более поздних версий необходимо установить модуль **SqlServer** из коллекции PowerShell.
> Сведения об установке модуля **SqlServer** см. в статье [Установка компонентов SQL Server PowerShell](download-sql-server-ps-module.md).


Существует несколько типов шагов заданий агента [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Каждый тип связан с некоторой подсистемой, в которой реализуется определенная среда, например агент репликации или среда командной строки. Можно создавать скрипты Windows PowerShell, а затем использовать агент [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , чтобы включить скрипты в задания, которые выполняются в запланированное время или в ответ на события [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Скрипты Windows PowerShell можно запускать либо с помощью шагов задания командной строки, либо с помощью шагов задания PowerShell.  
  
1.  Используйте шаги задания PowerShell для запуска подсистемой агента [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] программы **sqlps** , запускающей PowerShell и импортирующей модуль **sqlps** .  
  
2.  Используйте шаг задания командной строки для запуска PowerShell.exe и укажите скрипт, импортирующий модуль **sqlps** .  
  
###  <a name="LimitationsRestrictions"></a> ограничения  
  
> [!CAUTION]  
>  Каждый шаг задания агента [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], запускающий PowerShell с модулем **sqlps**, запускает процесс, которому требуется приблизительно 20 МБ памяти. Одновременный запуск большого числа шагов задания Windows PowerShell может иметь негативное влияние на производительность.  
  
##  <a name="PShellJob"></a> Создание шага задания PowerShell  
 **Создание шага задания PowerShell**  
  
1.  Разверните **Агент SQL Server**, создайте задание или щелкните правой кнопкой мыши существующее задание и выберите пункт **Свойства**. Дополнительные сведения о создании заданий см. в разделе [Создание заданий](http://msdn.microsoft.com/library/465fb7fc-7622-4252-a178-ea51691c935b).  
  
2.  В диалоговом окне **Свойства задания** выберите страницу **Шаги** и нажмите кнопку **Добавить**.  
  
3.  В диалоговом окне **Новый шаг задания** введите **имя шага**задания.  
  
4.  В списке **Тип** выберите **PowerShell**.  
  
5.  В списке **Выполнять как** выберите учетную запись-посредник с учетными данными, используемыми в задании.  
  
6.  В поле **Команда** введите синтаксис скрипта PowerShell, который будет выполняться в данном шаге. Или нажмите кнопку **Открыть** и выберите файл, содержащий скрипт.  
  
7.  Выберите страницу **Дополнительно** , чтобы задать следующие параметры шага задания: какие действия предпринять в случае успешного или неуспешного выполнения шага задания, сколько раз агенту [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] пытаться его выполнить и как часто повторять эти попытки.  
  
##  <a name="CmdExecJob"></a> Создание шага задания командной строки  
 **Создание шага задания CmdExec**  
  
1.  Разверните **Агент SQL Server**, создайте задание или щелкните правой кнопкой мыши существующее задание и выберите пункт **Свойства**. Дополнительные сведения о создании заданий см. в разделе [Создание заданий](http://msdn.microsoft.com/library/465fb7fc-7622-4252-a178-ea51691c935b).  
  
2.  В диалоговом окне **Свойства задания** выберите страницу **Шаги** и нажмите кнопку **Добавить**.  
  
3.  В диалоговом окне **Новый шаг задания** введите **имя шага**задания.  
  
4.  В списке **Тип** выберите **Операционная система (CmdExec)**.  
  
5.  В списке **Выполнять как** выберите учетную запись-посредник с учетными данными, используемыми в задании. По умолчанию шаги задания CmdExec выполняются под учетной записью службы агента SQL Server.  
  
6.  В поле **Код завершения процесса успешной команды** введите значение от 0 до 999999.  
  
7.  В поле **Команда** введите powershell.exe с параметрами, указывающими скрипт PowerShell для запуска.  
  
8.  Выберите вкладку **Дополнительно** , чтобы задать следующие параметры шага задания: действие, которое необходимо выполнить при успешном или неуспешном выполнении шага задания, количество попыток агента [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] выполнить шаг задания и файл, в который агент [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] может записывать результат выполнения шага задания. Только члены предопределенной роли сервера **sysadmin** могут записывать выходные данные шага задания в файл операционной системы.  
  
## <a name="see-also"></a>См. также:  
 [SQL Server PowerShell](sql-server-powershell.md)  
  
  