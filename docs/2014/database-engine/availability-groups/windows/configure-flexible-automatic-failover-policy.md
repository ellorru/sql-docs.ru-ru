---
title: Настройка гибкой политики отработки отказа для управления условиями автоматической отработки отказа (Always On групп доступности) | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], flexible failover policy
- Availability Groups [SQL Server], failover
- failover [SQL Server], AlwaysOn Availability Groups
ms.assetid: 1ed564b4-9835-4245-ae35-9ba67419a4ce
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 452d3ac4dae2164fa0fa172528ae398ea91fed31
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/23/2019
ms.locfileid: "72797751"
---
# <a name="configure-the-flexible-failover-policy-to-control-conditions-for-automatic-failover-always-on-availability-groups"></a>Настройка гибкой политики отработки отказа для обеспечения контроля над автоматическим переходом на другой ресурс (группы доступности AlwaysOn)
  В данном разделе описывается настройка гибкой политики отработки отказа в группе доступности AlwaysOn при помощи [!INCLUDE[tsql](../../../includes/tsql-md.md)] или PowerShell в [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. Гибкая политика отработки отказа предоставляет гранулярное управление условиями, которые могут вызвать автоматический переход на другой ресурс для группы доступности. Изменяя условия отказа, которые инициируют автоматический переход на другой ресурс, и частоту проверки исправности, вы можете увеличить или уменьшить вероятность автоматического перехода на другой ресурс и добиться высокого уровня доступности соглашения об уровне обслуживания.  
  
  
  
    > [!NOTE]  
    >  The flexible failover policy of an availability group cannot be configured by using [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)].  
  
##  <a name="BeforeYouBegin"></a> Перед началом  
  
###  <a name="Limitations"></a> Ограничения автоматического перехода на другой ресурс  
  
-   Для автоматического перехода на другой ресурс текущая первичная реплика и одна вторичная реплика должны быть настроены в режиме доступности синхронной фиксации с автоматическим переходом на другой ресурс, а вторичная реплика должна быть синхронизирована с первичной.  
  
-   Если в группе доступности превышен порог сбоя WSFC, то кластер WSFC не выполняет автоматический переход на другой ресурс для этой группы доступности. Более того, группа ресурсов WSFC для группы доступности остается в состоянии сбоя, пока администратор кластера вручную не переведет сбойную группу ресурсов в режим «в сети» или пока администратор базы данных вручную не выполнит переход группы доступности на другой ресурс. *Порог сбоя WSFC* определяется как максимальное число сбоев, которые могут произойти в группе доступности за заданный период времени. По умолчанию используется период в шесть часов, а максимальное число сбоев за этот период по умолчанию равно *n*-1, где *n* — число узлов WSFC. Чтобы изменить пороговые значения сбоя для заданной группы доступности, используйте консоль диспетчера отработки отказа WSFC.  
  
###  <a name="Prerequisites"></a> предварительные требования  
  
-   Необходимо подключиться к экземпляру сервера, на котором размещена первичная реплика.  
  
###  <a name="Security"></a> безопасность  
  
####  <a name="Permissions"></a> Разрешения  
  
|Задача|Permissions|  
|----------|-----------------|  
|Настройка гибкой политики отработки отказа для новой группы доступности|Требуется членство в фиксированной роли сервера **sysadmin** и одно из разрешений: CREATE AVAILABILITY GROUP, ALTER ANY AVAILABILITY GROUP или CONTROL SERVER.|  
|Изменение политики существующей группы доступности|Необходимо разрешение ALTER AVAILABILITY GROUP для группы доступности, разрешение CONTROL AVAILABILITY GROUP, разрешение ALTER ANY AVAILABILITY GROUP или разрешение CONTROL SERVER.|  
  
##  <a name="TsqlProcedure"></a> Использование Transact-SQL  
 **Настройка гибкой политики отработки отказа**  
  
1.  Подключитесь к экземпляру сервера, на котором находится первичная реплика.  
  
2.  Для новой группы доступности используйте инструкцию [CREATE AVAILABILITY GROUP](/sql/t-sql/statements/create-availability-group-transact-sql)[!INCLUDE[tsql](../../../includes/tsql-md.md)] . При добавлении или изменении существующей группы доступности воспользуйтесь инструкцией [ALTER AVAILABILITY GROUP](/sql/t-sql/statements/alter-availability-group-transact-sql)[!INCLUDE[tsql](../../../includes/tsql-md.md)] .  
  
    -   Чтобы установить уровень условий перехода на другой ресурс, используйте параметр FAILURE_CONDITION_LEVEL = *n* , где *n* — это целое число от 1 до 5.  
  
         Например, следующая инструкция [!INCLUDE[tsql](../../../includes/tsql-md.md)] изменяет уровень условия сбоя для существующей группы доступности `AG1`до уровня 1:  
  
        ```sql
        ALTER AVAILABILITY GROUP AG1 SET (FAILURE_CONDITION_LEVEL = 1);  
        ```  
  
         Эти целочисленные значения следующим образом соответствуют уровням условий сбоя.  
  
        |[!INCLUDE[tsql](../../../includes/tsql-md.md)] Значение|level|Автоматическая отработка отказа запускается при...|  
        |------------------------------|-----------|-------------------------------------------|  
        |1|Один|При остановке работы сервера. Служба SQL Server останавливается из-за отработки отказа или перезапуска.|  
        |2|Два|При отсутствии ответа от сервера. Удовлетворяется любое условие более низкого значения, служба SQL Server подключена к кластеру, а пороговое значение ожидания проверки работоспособности превышено, либо текущая первичная реплика находится в неисправном состоянии.|  
        |3|Три|В случае критической ошибки сервера. Удовлетворяется любое условие более низкого значения, или возникает внутренняя критическая ошибка сервера.<br /><br /> Это уровень, заданный по умолчанию.|  
        |4|Четыре|В случае ошибки сервера средней значимости. Удовлетворяется любое условие более низкого значения, или возникает ошибка сервера средней значимости.|  
        |5|Пять|При любых подходящих условиях сбоя. Удовлетворяется любое условие более низкого значения, или возникает подходящее условие сбоя.|  
  
         Дополнительные сведения об уровнях условий перехода на другой ресурс см. в статье [Гибкая политика отработки отказа для автоматического перехода на другой ресурс группы доступности (SQL Server)](flexible-automatic-failover-policy-availability-group.md).  
  
    -   Чтобы настроить пороговое значение ожидания проверки работоспособности, используйте параметр HEALTH_CHECK_TIMEOUT = *n*, где *n* является целым числом от 15000 миллисекунд (15 секунд) до 4294967295 миллисекунд. Значение по умолчанию — 30 000 миллисекунд (30 секунд)  
  
         Например, следующая инструкция [!INCLUDE[tsql](../../../includes/tsql-md.md)] изменяет пороговое значение времени ожидания проверки работоспособности существующей группы доступности `AG1`на значение 60 000 миллисекунд (одна минута).  
  
        ```sql
        ALTER AVAILABILITY GROUP AG1 SET (HEALTH_CHECK_TIMEOUT = 60000);  
        ```  
  
##  <a name="PowerShellProcedure"></a> Использование PowerShell  

### <a name="to-configure-the-flexible-failover-policy"></a>Настройка гибкой политики отработки отказа * *  
  
1.  Установите значение по умолчанию (`cd`) равным серверу экземпляра, на котором размещена первичная реплика.  
  
2.  При добавлении реплики доступности в группу доступности воспользуйтесь командлетом `New-SqlAvailabilityGroup`. При изменении существующей реплики доступности воспользуйтесь командлетом `Set-SqlAvailabilityGroup`.  
  
    -   Чтобы задать уровень условия отработки отказа, используйте параметр *уровня* `FailureConditionLevel`, где, *Level* имеет одно из следующих значений:  
  
        |Value|level|Автоматическая отработка отказа запускается при...|  
        |-----------|-----------|-------------------------------------------|  
        |`OnServerDown`|Один|При остановке работы сервера. Служба SQL Server останавливается из-за отработки отказа или перезапуска.|  
        |`OnServerUnresponsive`|Два|При отсутствии ответа от сервера. Удовлетворяется любое условие более низкого значения, служба SQL Server подключена к кластеру, а пороговое значение ожидания проверки работоспособности превышено, либо текущая первичная реплика находится в неисправном состоянии.|  
        |`OnCriticalServerError`|Три|В случае критической ошибки сервера. Удовлетворяется любое условие более низкого значения, или возникает внутренняя критическая ошибка сервера.<br /><br /> Это уровень, заданный по умолчанию.|  
        |`OnModerateServerError`|Четыре|В случае ошибки сервера средней значимости. Удовлетворяется любое условие более низкого значения, или возникает ошибка сервера средней значимости.|  
        |`OnAnyQualifiedFailureConditions`|Пять|При любых подходящих условиях сбоя. Удовлетворяется любое условие более низкого значения, или возникает подходящее условие сбоя.|  
  
         Дополнительные сведения об уровнях условий перехода на другой ресурс см. в статье [Гибкая политика отработки отказа для автоматического перехода на другой ресурс группы доступности (SQL Server)](flexible-automatic-failover-policy-availability-group.md).  
  
         Например, следующая команда изменяет уровень условия сбоя для существующей группы доступности `AG1`до уровня 1.  
  
        ```powershell
        Set-SqlAvailabilityGroup `
         -Path SQLSERVER:\Sql\PrimaryServer\InstanceName\AvailabilityGroups\MyAg `
         -FailureConditionLevel OnServerDown  
        ```  
  
    -   Чтобы установить пороговое значение времени ожидания проверки работоспособности, используйте параметр `HealthCheckTimeout`*n* , где *n* — это целое число от 15000 миллисекунд (15 секунд) до 4294967295 миллисекунд. Значение по умолчанию — 30 000 миллисекунд (30 секунд).  
  
         Например, следующая команда изменяет пороговое значение времени ожидания проверки работоспособности существующей группы доступности `AG1`на значение 120 000 миллисекунд (две минуты).  
  
        ```powershell
        Set-SqlAvailabilityGroup `
         -Path SQLSERVER:\Sql\PrimaryServer\InstanceName\AvailabilityGroups\MyAG `
         -HealthCheckTimeout 120000  
        ```  
  
> [!NOTE]  
>  Чтобы просмотреть синтаксис командлета, воспользуйтесь командлетом `Get-Help` в среде [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell. Дополнительные сведения см. в разделе [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md).  
  
 **Настройка и использование поставщика SQL Server PowerShell**  
  
-   [Поставщик SQL Server PowerShell](../../../powershell/sql-server-powershell-provider.md)  
  
-   [Получение справок по SQL Server PowerShell](../../../powershell/sql-server-powershell.md)  
  
## <a name="see-also"></a>См. также статью  
 [Общие сведения о &#40;группы доступности AlwaysOn&#41; SQL Server](overview-of-always-on-availability-groups-sql-server.md)    
 [Режимы доступности (группы доступности AlwaysOn)](availability-modes-always-on-availability-groups.md)    
 [Отказоустойчивость и режимы &#40;отработки отказа группы доступности AlwaysOn&#41; ](failover-and-failover-modes-always-on-availability-groups.md)    
 [Отказоустойчивая кластеризация Windows Server (WSFC) с SQL Server](../../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md)   
 [Политика отработки отказа для экземпляров откзоустойчивого кластера](../../../sql-server/failover-clusters/windows/failover-policy-for-failover-cluster-instances.md)   
 [sp_server_diagnostics (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql)  
