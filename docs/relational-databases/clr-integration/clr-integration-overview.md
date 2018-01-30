---
title: "Общие сведения об интеграции со средой CLR | Документы Microsoft"
ms.custom: 
ms.date: 04/19/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: clr
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- common language runtime [SQL Server], about CLR integration
- extended stored procedures [SQL Server], vs. managed code
- objects [CLR integration]
- Transact-SQL vs. managed code
- managed code [SQL Server], vs. Transact-SQL
- managed code [SQL Server], vs. extended stored procedures
- execution at client vs. execution at server [CLR integration]
ms.assetid: 5aa176da-3652-4afa-a742-4c40c77ce5c3
caps.latest.revision: "50"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: f506da16cb9a5a98b2a270116ca7948f75c26ce8
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/08/2018
---
# <a name="clr-integration---overview"></a>Интеграция со средой CLR - Обзор
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]Общеязыковая среда выполнения (CLR) является сердцем платформы Microsoft .NET Framework и предоставляет среду выполнения для всего кода .NET Framework. Код, выполняемый в среде CLR, называется управляемым кодом. Среда CLR предоставляет различные функции и услуги, требуемые для выполнения программы, включая JIT-компиляцию, распределение и управление памятью, соблюдение безопасности типов, обработку исключений, управление потоками и безопасность.  Дополнительные сведения см. в пакете .NET Framework SDK.  
  
 Если среда CLR размещается в Microsoft SQL Server (что принято называть интеграцией со средой CLR), то появляется возможность разрабатывать в управляемом коде хранимые процедуры, триггеры, определяемые пользователем функции, определяемые пользователем типы и определяемые пользователем статистические функции. Из-за того, что управляемый код перед выполнением производит компиляцию в машинный код, можно достичь значительного увеличения производительности в некоторых сценариях.  
  
 В управляемом коде используется управление доступом для кода (CAS) для предотвращения выполнения сборками определенных операций. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] использует CAS для обеспечения безопасности управляемого кода и для предотвращения нарушений безопасности операционной системы или сервера баз данных.  
  
## <a name="advantages-of-clr-integration"></a>Преимущества интеграции со средой CLR  
 Язык [!INCLUDE[tsql](../../includes/tsql-md.md)] специально разработан для обеспечения прямого доступа к данным и управления данными в базе данных. Поскольку [!INCLUDE[tsql](../../includes/tsql-md.md)] предназначен в первую очередь для обеспечения доступа к данным и управления ими, он не является полноценным языком программирования. Например, [!INCLUDE[tsql](../../includes/tsql-md.md)] не поддерживает массивы, коллекции, циклы for-each, сдвиг битов и классы. Безусловно, некоторые из этих конструкций можно моделировать в [!INCLUDE[tsql](../../includes/tsql-md.md)], но в управляемом коде обеспечивается их встроенная поддержка. В зависимости от сценария эти средства могут стать убедительной причиной для внедрения в управляемый код определенных функциональных возможностей поддержки базы данных.  
  
 Microsoft Visual Basic .NET и Microsoft Visual C# предлагают объектно-ориентированные возможности, например инкапсуляцию, наследование и полиморфизм. Связанный код теперь можно легко организовать в классы и пространства имен. При работе с большими объемами серверного кода это позволяет упростить организацию и сохранение кода.  
  
 Управляемый код подходит для реализации вычислений и сложной логики выполнения больше, чем [!INCLUDE[tsql](../../includes/tsql-md.md)], и обеспечивает расширенную поддержку многих сложных задач, включая обработку строк и регулярных выражений. С помощью функциональных возможностей, содержащихся в библиотеке .NET Framework, обеспечивается доступ к тысячам предварительно построенных классов и подпрограмм. К ним можно легко получить доступ из любой хранимой процедуры, триггера или определяемой пользователем функции. Базовая библиотека классов (BCL) включает классы, обеспечивающие функциональные возможности управления строками, выполнения сложных математических операций, доступа к файлам, шифрования и т. д.  
  
> [!NOTE]  
>  Хотя многие из этих классов могут быть использованы из кода CLR в SQL Server, те из них, которые не подходят для использования на сервере (например, классы для работы с окнами), недоступны. Дополнительные сведения см. в разделе [поддерживаемые библиотеки платформы .NET Framework](../../relational-databases/clr-integration/database-objects/supported-net-framework-libraries.md).  
  
 Одним из преимуществ управляемого кода является безопасность типов, или гарантия того, что код обращается к типам только точно определенным, разрешенным способом. Перед выполнением управляемого кода среда CLR проверяет код на безопасность. Например, код проверяется для обеспечения того, что из памяти не будут считываться данные, если они не были предварительно записаны в нее. Среда CLR также гарантирует, что код не использует неуправляемую память.  
  
 Интеграция со средой CLR позволяет улучшить производительность. Сведения см. в разделе [производительность интеграции со средой CLR](../../relational-databases/clr-integration/clr-integration-architecture-performance.md).  
 
>  [!WARNING]
>  Среда CLR использует управление доступом для кода (CAS) в .NET Framework, которое больше не поддерживается в качестве границы безопасности. Сборки среды CLR, созданные с помощью `PERMISSION_SET = SAFE`, могут получать доступ к внешним системным ресурсам, вызывать неуправляемый код и получать права системного администратора. Начиная с [!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)], появился параметр `sp_configure`, называемый `clr strict security`, для повышения безопасности сборок среды CLR. `clr strict security` включен по умолчанию и рассматривает сборки `SAFE` и `EXTERNAL_ACCESS`, как если бы они были помечены `UNSAFE`. Параметр `clr strict security` можно отключить для обеспечения обратной совместимости, но это делать не рекомендуется. Корпорация Майкрософт рекомендует подписывать все сборки с помощью сертификата или асимметричного ключа с соответствующим именем входа, которому предоставлено разрешение `UNSAFE ASSEMBLY` в базе данных master. Дополнительные сведения см. в статье о параметре [clr strict security](../../database-engine/configure-windows/clr-strict-security.md). 
  
## <a name="choosing-between-transact-sql-and-managed-code"></a>Выбор между Transact-SQL и управляемым кодом  
 При записи хранимых процедур, триггеров и определяемых пользователем функций следует принять решение, использовать традиционный язык [!INCLUDE[tsql](../../includes/tsql-md.md)] или язык платформы .NET Framework, например Visual Basic .NET или Visual C#. Используйте [!INCLUDE[tsql](../../includes/tsql-md.md)] в тех случаях, когда код в основном выполняет доступ к данным с минимумом или совсем без процедурной логики. Управляемый код следует использовать для функций и процедур, интенсивно использующих ЦП, содержащих сложную логику, или при необходимости использования библиотеки BCL платформы .NET Framework.  
  
### <a name="choosing-between-execution-in-the-server-and-execution-in-the-client"></a>Выбор между выполнением на сервере и выполнением на клиенте  
 Другим фактором при принятии решения о выборе между [!INCLUDE[tsql](../../includes/tsql-md.md)] или управляемым кодом является требуемое расположение кода на серверном или на клиентском компьютере. Код [!INCLUDE[tsql](../../includes/tsql-md.md)], как и управляемый код, можно выполнять на сервере. Это позволяет упростить доступ к данным из кода и воспользоваться ресурсами обработки, имеющимися на сервере. С другой стороны, иногда приходится отказываться от размещения на сервере базы данных таких задач, которые интенсивно используют процессор. Современные клиентские компьютеры чаще всего являются очень мощными, поэтому может возникнуть необходимость воспользоваться их ресурсами обработки, разместив на клиенте максимально возможный объем кода. Управляемый код может выполняться на клиентском компьютере, а [!INCLUDE[tsql](../../includes/tsql-md.md)] — нет.  
  
## <a name="choosing-between-extended-stored-procedures-and-managed-code"></a>Выбор между расширенными хранимыми процедурами и управляемым кодом  
 Расширенные хранимые процедуры позволяют реализовать возможности, недоступные в хранимых процедурах [!INCLUDE[tsql](../../includes/tsql-md.md)]. Однако расширенные хранимые процедуры могут нарушить целостность процесса [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], а управляемый код, проверенный на строгую типизацию, — нет. Далее, управление памятью, планирование потоков и волокон, а также службы Synchronization Services более тесно интегрированы между управляемым кодом среды CLR и [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Интеграция со средой CLR обеспечивает более защищенный по сравнению с расширенными хранимыми процедурами способ создания хранимых процедур при необходимости выполнения задач, недоступных для [!INCLUDE[tsql](../../includes/tsql-md.md)]. Дополнительные сведения об интеграции со средой CLR и расширенных хранимых процедур см. в разделе [производительность интеграции со средой CLR](../../relational-databases/clr-integration/clr-integration-architecture-performance.md).  
  
## <a name="see-also"></a>См. также:  
 [Установка .NET Framework](http://technet.microsoft.com/library/ms166014\(v=SQL.105\).aspx)   
 [Архитектура интеграции со средой CLR](http://msdn.microsoft.com/library/05e4b872-3d21-46de-b4d5-739b5f2a0cf9)   
 [Доступ к данным из объектов базы данных CLR](../../relational-databases/clr-integration/data-access/data-access-from-clr-database-objects.md)   
 [Приступая к работе с интеграцией со средой CLR](../../relational-databases/clr-integration/database-objects/getting-started-with-clr-integration.md)  
  
  