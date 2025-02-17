---
title: xp_msver (Transact-SQL) | Документация Майкрософт
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- xp_msver_TSQL
- xp_msver
dev_langs:
- TSQL
helpviewer_keywords:
- xp_msver
ms.assetid: 9264cf8c-92ba-45ad-b2d6-15d26d805a16
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 85552daa2dda14c6a7516c96f0f9fe6566f31111
ms.sourcegitcommit: f688a37bb6deac2e5b7730344165bbe2c57f9b9c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/08/2019
ms.locfileid: "73843902"
---
# <a name="xp_msver-transact-sql"></a>xp_msver (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Возвращает сведения о версии [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[msCoName](../../includes/msconame-md.md)]. **xp_msver** также возвращает сведения о фактическом номере сборки сервера и сведения о среде сервера. Сведения, которые **xp_msver** возвращаемые данные, можно использовать в инструкциях [!INCLUDE[tsql](../../includes/tsql-md.md)], пакетах, хранимых процедурах и т. д., чтобы улучшить логику для кода, не зависящего от платформы.  
  
 ![Значок ссылки на раздел](../../database-engine/configure-windows/media/topic-link.gif "Значок ссылки на раздел") [Синтаксические обозначения в Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
xp_msver [ optname ]  
```  
  
## <a name="arguments"></a>Аргументы  
 *optname*  
 Имя параметра может иметь одно из следующих значений.  
  
|Имя параметра/столбца|Описание|  
|-------------------------|-----------------|  
|**ProductName**|Название продукта; Например, [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**ProductVersion**|Номер версии продукта.|  
|**Язык**|Языковая версия [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**Платформа**|Имя операционной системы, имя производителя и имя семейства чипов для компьютера, на котором работает [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**Комментарии**|Различные сведения об [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**Название**|Имя компании, производящей [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]; например [!INCLUDE[msCoName](../../includes/msconame-md.md)] Corporation.|  
|**филедескриптион**|Операционная система.|  
|**FileVersion**|Версия исполняемого файла [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**интерналнаме**|[!INCLUDE[msCoName](../../includes/msconame-md.md)] внутреннее имя для [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]; Например, SQLSERVR.|  
|**легалкопиригхт**|Сведения о законных авторских правах, требуемые для [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]; например Copyright© [!INCLUDE[msCoName](../../includes/msconame-md.md)] Corp. 1988-2005.|  
|**легалтрадемаркс**|Сведения о зарегистрированном товарном знаке, требуемые для [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Например, [!INCLUDE[msCoName](../../includes/msconame-md.md)] является охраняемым товарным знаком [!INCLUDE[msCoName](../../includes/msconame-md.md)] Corporation.|  
|**оригиналфиленаме**|Имя файла, выполняемого при запуске [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]; например Sqlservr.exe.|  
|**приватебуилд**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**спеЦиалбуилд**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**виндовсверсион**|Версия [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows, установленная на компьютере, где работает [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**ProcessorCount**|Количество процессоров в компьютере, где работает [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**процессорактивемаск**|Показывает запущенные и пригодные к использованию [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Windows процессоры, установленные в компьютере, на котором работает [!INCLUDE[msCoName](../../includes/msconame-md.md)].|  
|**ProcessorType**|Тип процессора. Аналогично **Platform**.|  
|**фисикалмемори**|Количество памяти RAM в мегабайтах (МБ), установленной на компьютере, где работает [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**Идентификатор продукта**|Идентификационный номер продукта (PID). Указывается в процессе установки. Этот номер расположен на наклейке на подлинной коробке с дисками [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
  
## <a name="return-code-values"></a>Значения кода возврата  
 1 (успешное завершение)  
  
## <a name="result-sets"></a>Результирующие наборы  
 **xp_msver**без параметров возвращает результирующий набор из четырех столбцов, в котором перечислены все значения параметров. **xp_msver**для любого параметра возвращает результирующий набор из четырех столбцов со значениями для этого параметра.  
  
## <a name="permissions"></a>Разрешения  
 Необходимо быть членом роли **public** .  
  
## <a name="see-also"></a>См. также раздел  
 [Системные функции (Transact-SQL)](../../relational-databases/system-functions/system-functions-category-transact-sql.md)   
 [Системные хранимые процедуры (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Общие расширенные хранимые &#40;процедуры Transact-&#41; SQL](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)   
 [@@VERSION &#40;Transact-SQL&#41;](../../t-sql/functions/version-transact-sql-configuration-functions.md)  
  
  
