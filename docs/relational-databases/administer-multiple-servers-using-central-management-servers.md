---
title: Администрирование нескольких серверов с использованием центральных серверов управления | Документация Майкрософт
ms.date: 08/12/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- multiserver queries
- central management server
- multiserver administration [SQL Server]
- master servers [SQL Server], central management servers
- target configuration [SQL Server]
- server configuration [SQL Server]
ms.assetid: 427911a7-57d4-4542-8846-47c3267a5d9c
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 967f2f582b3d0bc5b5a7b6277b97f6557e19e7cc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/15/2019
ms.locfileid: "67934565"
---
# <a name="administer-multiple-servers-using-central-management-servers"></a>Администрирование нескольких серверов с использованием центральных серверов управления
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Можно администрировать сразу несколько серверов, назначив центральные серверы управления и создав группы серверов.  
  
## <a name="what-is-a-central-management-server-and-server-groups"></a>Что такое центральный сервер управления и группы серверов?  
 Экземпляр SQL Server, предназначенный для работы в качестве центрального сервера управления, обслуживает группы серверов, в которых содержатся сведения о соединении для одного или нескольких экземпляров. Инструкции [!INCLUDE[tsql](../includes/tsql-md.md)] и политики управления на основе политик можно выполнять для групп серверов одновременно. Можно также просмотреть файлы журналов на экземплярах, управляемых через центральный сервер управления. 
 
 По сути, центральный сервер управления — это центральный репозиторий, содержащий список управляемых серверов. Версии ранее [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] нельзя назначить в качестве центрального сервера управления.  
  
 [!INCLUDE[tsql](../includes/tsql-md.md)] также можно выполнить для локальных групп серверов в окне «Зарегистрированные серверы».  
  
## <a name="create-central-management-server-and-server-groups"></a>Создание центрального сервера управления и групп серверов 
 Для создания сервера централизованного управления и групп серверов воспользуйтесь окном **Зарегистрированные серверы** в среде [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. Обратите внимание, что сервер центрального управления не может быть членом группы, которую он обслуживает. 
 
 Дополнительные сведения о создании центральных серверов управления и групп серверов см. в разделе [Создание центрального сервера управления и группы серверов &#40;среда SQL Server Management Studio&#41;](../tools/sql-server-management-studio/create-a-central-management-server-and-server-group.md).  
  
## <a name="see-also"></a>См. также раздел  
 [Администрирование серверов с помощью управления на основе политик](../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)  
  
  
