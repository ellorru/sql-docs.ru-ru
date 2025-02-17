---
title: Импорт модуля SQLPS | Документация Майкрософт
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: a972c56e-b2af-4fe6-abbd-817406e2c93a
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 34859c0c516c61a73e31dbf752ab274188c6343a
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/23/2019
ms.locfileid: "72797869"
---
# <a name="import-the-sqlps-module"></a>Импорт модуля SQLPS
  Для управления [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] из PowerShell рекомендуется импортировать модуль `sqlps` в среду Windows PowerShell 2.0. Модуль загружает и регистрирует оснастки [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] и сборки управляемости.  
  
1.  **Перед началом работы:**  [Безопасность](#Security)  
  
2.  **Чтобы загрузить модуль:**  [Загрузка модуля sqlps](#LoadSqlps)  
  
## <a name="before-you-begin"></a>Перед началом  
 После импорта модуля `sqlps` в среду Windows PowerShell можно:  
  
-   Вводить команды Windows PowerShell в интерактивном режиме.  
  
-   Запускать файлы скриптов Windows PowerShell.  
  
-   Запускать командлеты служб [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
-   Использовать пути поставщика служб [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] для передвижения по иерархии объектов среды служб [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
-   Для управления объектами [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] используйте объектные модели управляемости [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (такие как Microsoft.SqlServer.Management.Smo).  
  
> [!NOTE]  
>  Команды, используемые в именах двух командлетов SQL Server (`Encode-Sqlname` и `Decode-Sqlname`), не соответствуют утвержденным командам для Windows PowerShell 2.0. Это не влияет на их работу, однако среда Windows PowerShell выдает предупреждение при импорте модуля `sqlps` в сеанс.  
  
###  <a name="Security"></a> безопасность  
 По умолчанию в Windows PowerShell политика выполнения скриптов работает в **ограниченном**режиме, блокируя все скрипты Windows PowerShell. Для загрузки модуля `sqlps` можно использовать командлет `Set-ExecutionPolicy`, чтобы включить запуск как подписанных, так и любых других скриптов. Следует выполнять только скрипты, полученные из доверенных источников, а также защищать все входные и выходные файлы, установив необходимые разрешения NTFS. Дополнительные сведения о включении скриптов Windows PowerShell см. в разделе [Выполнение скриптов Windows PowerShell](https://docs.microsoft.com/powershell/scripting/setup/starting-windows-powershell?view=powershell-6#how-to-enable-windows-powershell-ise-on-earlier-releases-of-windows).  
  
##  <a name="LoadSqlps"></a> Загрузка модуля sqlps  

### <a name="to-load-the-sqlps-module-in-windows-powershell"></a>Загрузка модуля sqlps в среду Windows PowerShell
  
1.  Чтобы установить соответствующую политику выполнения скриптов, используйте командлет `Set-ExecutionPolicy`.  
  
2.  Для импорта модуля sqlps используйте командлет `Import-Module`. Если требуется отключить предупреждение о `DisableNameChecking` и `Encode-Sqlname`, задайте параметр `Decode-Sqlname`.  
  
### <a name="example-powershell"></a>Пример (PowerShell)  
 В этом примере показана загрузка модуля `sqlps` с отключенной проверкой имен.  
  
```powershell
## Import the SQL Server Module.  
  
Import-Module "sqlps" -DisableNameChecking  
```  

## <a name="see-also"></a>См. также статью  
 [SQL Server PowerShell](../powershell/sql-server-powershell.md)   
 [SQL Server PowerShell, поставщик](../powershell/sql-server-powershell-provider.md)   
 [Использование командлетов ядра СУБД](../../2014/database-engine/use-the-database-engine-cmdlets.md)  
