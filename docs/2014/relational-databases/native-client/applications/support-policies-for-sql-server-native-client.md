---
title: Политики поддержки для собственного клиента SQL Server | Документация Майкрософт
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client  - "database-engine" - "docset-sql-devref"
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 09c80cf4-23e6-4027-a24f-cdb9c87af811
caps.latest.revision: 24
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 14b75dc088ea1542038151377d6c8339b72870e9
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/03/2018
ms.locfileid: "37426295"
---
# <a name="support-policies-for-sql-server-native-client"></a>Политики поддержки собственного клиента SQL Server
  В этом разделе рассматриваются способы использования различных компонентов доступа к данным с собственным клиентом Native Client [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="server-support"></a>Поддержка сервера  
 Клиент [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 11.0 поддерживает соединение с [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] и [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)].  
  
## <a name="supported-operating-system-versions"></a>Поддерживаемые версии операционных систем  
 В следующей таблице приведен список операционных систем, поддерживающих Native Client [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
|Версия собственного клиента SQL Server|Поддерживаемые операционные системы|  
|--------------------------------------|---------------------------------|  
|Собственный клиент SQL Server (SQL Server 2005)|-Microsoft Windows 2000 с пакетом обновления 4 или более поздней версии<br />-Microsoft Windows Server 2003 или более поздней версии<br />-Пакет обновления 1 для Microsoft Windows XP или более поздней версии<br />-Microsoft Windows Vista (требуется [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] пакет обновления 2 или более поздней версии)<br />-Microsoft Windows Server 2008 (требуется [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] пакет обновления 2 или более поздней версии)|  
|SQL Server Native Client 10.0 ([!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)])|— Microsoft Windows Server 2003 Service Pack 2, или более поздней версии<br />— Microsoft Windows XP Service Pack 2 или более поздней версии<br />-Microsoft Windows Vista<br />-Microsoft Windows Server 2008|  
|Собственный клиент SQL Server 10.5 ([!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)])|— Microsoft Windows Server 2003 Service Pack 2, или более поздней версии<br />— Microsoft Windows XP с пакетом обновления 2 или более поздней версии<br />-Microsoft Windows Vista<br />-Microsoft Windows Server 2008<br />-Microsoft Windows 7|  
|Клиент SQL Server Native Client 11.0 ([!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] и [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)])|-Microsoft Windows Vista<br />-Microsoft Windows Server 2008<br />-Microsoft Windows 7<br />-Microsoft Windows 8<br />-Microsoft Windows Server 2012|  
  
## <a name="ado-support-policies"></a>Политика поддержки ADO  
 Приложение ADO может пользоваться поставщиком OLE DB SQLOLEDB, который входит в состав Windows, если ему не требуются функции [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] или более поздней версии.  
  
 Приложения ADO могут использовать версию [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] собственный клиент включен в [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]. Приложения ADO могут также пользоваться собственным клиентом [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 11.0 (в составе [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)]), но в этом случае необходимо указать `DataTypeCompatibility=80` в строке соединения. Только функции [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] будут доступны, если в строке соединения указано значение `DataTypeCompatibility=80`.  
  
## <a name="bcp-support-policies"></a>Политика поддержки BCP  
 Начиная с [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)], программа bcp.exe поддерживает файлы данных, которые не более чем на три версии [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] старше версии [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], с которой поставляется экземпляр bcp.exe.  
  
## <a name="odbc-support-policies"></a>Политика поддержки ODBC  
 Приложения должны пользоваться драйвером ODBC [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], включенным в операционную систему Windows. Если приложение сертифицировано для работы с определенной версией собственного клиента [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], то можно пользоваться драйвером ODBC собственного клиента [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="ole-db-support-policies"></a>Политики поддержки OLE DB  
 Приложения должны пользоваться поставщиком OLE DB [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], включенным в операционную систему Windows. Если приложение сертифицировано для работы с определенной версией собственного клиента [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], то можно пользоваться поставщиком собственного клиента OLE DB [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 Приложение OLE DB, которое не было сертифицированы для использования с собственным клиентом [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], может пользоваться собственным клиентом [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], если в его строке соединения указано `DataTypeCompatibility=80`.  
  
 Приложение OLE DB, которое пользуется компонентом службы OLE DB, может пользоваться собственным клиентом [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], если в строке соединения указано `DataTypeCompatibility=80`. Тем не менее, функции, добавленные после [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] будут доступны в этом случае.  
  
## <a name="see-also"></a>См. также  
 [Построение приложений с использованием SQL Server Native Client](building-applications-with-sql-server-native-client.md)  
  
  