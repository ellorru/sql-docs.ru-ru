---
title: Основные понятия программирования интеграции со средой CLR | Документация Майкрософт
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- CLR [SQL Server] See common language runtime [SQL Server]
- Database Engine [SQL Server], .NET Framework
- .NET Framework [SQL Server], Database Engine programming
- common language runtime [SQL Server]
- .NET Framework [SQL Server]
ms.assetid: 951bf851-3e6e-4361-ae6a-2bcd5b837ebd
author: rothja
ms.author: jroth
ms.openlocfilehash: b172399d5e7a04365cf8005b5dc52ebc9795c13a
ms.sourcegitcommit: 734529a6f108e6ee6bfce939d8be562d405e1832
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/02/2019
ms.locfileid: "70212391"
---
# <a name="common-language-runtime-clr-integration-programming-concepts"></a>Основные понятия о программировании интеграции со средой CLR
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  Начиная с версии [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] обеспечивает интеграцию с компонентами CLR платформы .NET Framework для [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows. Это означает, что хранимые процедуры, триггеры, определяемые пользователем типы, определяемые пользователем функции, определяемые пользователем статистические функции и возвращающие табличные значение потоковые функции теперь могут разрабатываться с использованием любого языка .NET Framework, включая [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic .NET и [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C#.  
  
 Пространство имен Microsoft.SqlServer.Server содержит основные возможности программирования CLR для [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Однако пространство имен Microsoft.SqlServer.Server документировано в пакете .NET Framework SDK. Эта документация не включена в электронную документацию по [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
>  По умолчанию платформа .NET Framework устанавливается вместе с [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], но пакет .NET Framework SDK в эту установку не включен. Если пакет SDK установлен на рабочем компьютере и не добавлен к коллекции электронной документации, то ссылки на содержимое пакета SDK, имеющиеся в этом разделе, работать не будут. Установите пакет .NET Framework SDK. После установки добавьте пакет SDK в коллекцию электронной документации и оглавление, следуя инструкциям в разделе [Установка пакета SDK для .NET Framework](https://technet.microsoft.com/library/bb686823\(v=SQL.105\).aspx).  
  
> [!NOTE]  
>  Функции CLR, такие как пользовательские функции CLR, *не* поддерживаются для базы данных SQL Azure.  
  
 В следующей таблице приводится список подразделов данного раздела.  
  
 [Общие сведения об &#40;интеграции&#41; CLR](../../relational-databases/clr-integration/common-language-runtime-integration-overview.md)  
 Содержит общие сведения о среде CLR и описывает способы и преимущества использования технологии в [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Описывает преимущества использования среды CLR для создания объектов базы данных.  
  
 [Сборки (компонент Database Engine)](../../relational-databases/clr-integration/assemblies-database-engine.md)  
 Описывает использование в [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] сборок для развертывания функций, хранимых процедур, триггеров, пользовательских статистических функций и определяемых пользователем типов данных, написанных на одном из языков управляемого кода, поддерживаемых средой CLR [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework, а не на языке [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 [Создание объектов базы данных с &#40;&#41; интегрированной средой CLR](../../relational-databases/clr-integration/database-objects/building-database-objects-with-common-language-runtime-clr-integration.md)  
 Описывает виды объектов, которые можно строить с использованием среды CLR, и рассматривает требования к построению объектов баз данных CLR.  
  
 [Доступ к данным из объектов среды CLR для работы с базами данных](../../relational-databases/clr-integration/data-access/data-access-from-clr-database-objects.md)  
 Описывает, как подпрограмма CLR может обращаться к данным, хранящимся в экземпляре [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [Безопасность интеграции со средой CLR](../../relational-databases/clr-integration/security/clr-integration-security.md)  
 Описывает модель безопасности для средств интеграции со средой CLR.  
  
 [Отладка объектов базы данных среды CLR](../../relational-databases/clr-integration/debugging-clr-database-objects.md)  
 Описывает ограничения и требования для отладки объектов базы данных CLR.  
  
 [Развертывание объектов базы данных CLR](../../relational-databases/clr-integration/deploying-clr-database-objects.md)  
 Описывает развертывание сборок на рабочих серверах.  
  
 [Управление сборками интеграции со средой CLR](../../relational-databases/clr-integration/assemblies/managing-clr-integration-assemblies.md)  
 Описывает способы создания и удаления сборок интеграции со средой CLR.  
  
 [Мониторинг и устранение неполадок управляемых объектов базы данных](../../relational-databases/clr-integration/monitoring-and-troubleshooting-managed-database-objects.md)  
 Данный раздел содержит информацию о средствах, которые можно использовать для наблюдения и диагностики управляемых объектов базы данных и сборок, работающих в [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [Сценарии использования и примеры интеграции со средой CLR](https://msdn.microsoft.com/library/33aac25f-abb4-4f29-af88-4a0dacd80ae7)  
 Описывает сценарии использования и образцы кода, использующие объекты CLR.  
  
## <a name="see-also"></a>См. также  
 [Сборки &#40;ядро СУБД&#41;](../../relational-databases/clr-integration/assemblies-database-engine.md)   
 [Установка пакета SDK для .NET Framework](https://technet.microsoft.com/library/bb686823\(v=SQL.105\).aspx)  
  
  
