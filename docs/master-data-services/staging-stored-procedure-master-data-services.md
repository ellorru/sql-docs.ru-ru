---
title: Промежуточная хранимая процедура
ms.custom: ''
ms.date: 04/01/2016
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 6a613106-9f87-4caf-a23a-a726fc6561c5
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 103c43f012f6cf7025139fd29656a42d00fc233f
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727892"
---
# <a name="staging-stored-procedure-master-data-services"></a>Промежуточная хранимая процедура (службы Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  При запуске промежуточного процесса из [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]используется одна из трех хранимых процедур.  
  
-   stg.udp_\<имя>_Leaf  
  
-   stg.udp_\<имя>_Consolidated  
  
-   stg.udp_\<имя>_Relationship  
  
 Где имя — это имя промежуточной таблицы, определенной при создании сущности.  
  
## <a name="staging-process-stored-procedure-parameters"></a>Параметры хранимой процедуры промежуточного процесса  
 В следующей таблице приведены параметры этих хранимых процедур.  
  
|Параметр|Описание|  
|---------------|-----------------|  
|**VersionName**<br /><br /> Обязательное|Имя версии. С учетом или без учета регистра, в зависимости от параметров сортировки [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .|  
|**LogFlag**<br /><br /> Обязательное|Определяет, будут ли регистрироваться транзакции в ходе промежуточного процесса. Возможны следующие значения:<br /><br /> **0**: не регистрировать транзакции.<br /><br /> **1**: регистрировать транзакции.<br /><br /> <br /><br /> Дополнительные сведения о транзакциях см. в разделе [Транзакции (службы Master Data Services)](../master-data-services/transactions-master-data-services.md).|  
|**BatchTag**<br /><br /> Требуется, за исключением веб-службы|Значение **BatchTag** , как указано в промежуточной таблице.|  
|**Batch_ID**<br /><br /> Требуется только для веб-службы|Значение **Batch_ID** , как указано в промежуточной таблице.|  
|**Имя пользователя**|Необязательный параметр|  
|**Идентификатор пользователя**|Необязательный параметр|  
  
### <a name="staging-process-stored-procedure-example"></a>Пример хранимой процедуры промежуточного процесса  
 В следующем примере показан запуск промежуточного процесса с помощью хранимой процедуры.  
  
```  
USE [DATABASE_NAME]  
GO  
  
EXEC[stg].[udp_name_Leaf]  
      @VersionName = N'VERSION_1',  
@LogFlag = 1,  
@BatchTag = N'batch1'  
      @UserName=N'domain\user'  
  
GO  
  
```  
  
## <a name="see-also"></a>См. также раздел  
 [Проверка хранимых процедур (службы Master Data Services)](../master-data-services/validation-stored-procedure-master-data-services.md)   
 [Просмотр ошибок, возникающих во время помещения на промежуточное хранение (службы Master Data Services)](../master-data-services/view-errors-that-occur-during-staging-master-data-services.md)  
  
  
