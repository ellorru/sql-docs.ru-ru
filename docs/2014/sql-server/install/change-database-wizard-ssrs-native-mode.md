---
title: Мастер изменения базы данных (собственный режим служб SSRS) | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- SQL12.rsconfigtool.changedatabase.F1
helpviewer_keywords:
- Change Database Wizard
- report server database, create
ms.assetid: 1a2e8d18-5997-482f-a9c1-87d99f7407b8
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: cd81004765b1ba5d15c5929dc661ce1dea04b371
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952665"
---
# <a name="change-database-wizard-ssrs-native-mode"></a>Мастер изменения базы данных (службы Reporting Services в собственном режиме)
  В состав диспетчера конфигурации служб [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] входит мастер изменения базы данных, который позволяет создать новую или выбрать существующую базу данных сервера отчетов для использования в сочетании с текущим экземпляром сервера отчетов.  
  
 Если выбрана база данных предыдущей версии, то будет произведено ее обновление до версии экземпляра сервера отчетов, к которому она подключается. После запуска службы происходит проверка версии базы данных и автоматическое обновление ее схемы до текущей версии.  
  
 Чтобы запустить мастер, щелкните **Изменить базу данных** на странице базы данных в диспетчере конфигурации служб [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Инструкции по запуску Configuration Manager [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] см. в разделе [ &#40;Диспетчер конфигурации служб Reporting Services в собственном режиме&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md).  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] в собственном режиме.  
  
## <a name="options"></a>Параметры  
 **Действие**  
 Выберите задачу, которую необходимо выполнить. Новая база данных может быть создана в собственном режиме или в режиме интеграции с SharePoint. Можно также выбрать для использования с текущим экземпляром сервера отчетов существующую базу данных.  
  
 **Сервер базы данных**  
 Задает имя экземпляра компонента [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] , на котором размещается база данных сервера отчетов. Можно использовать экземпляр по умолчанию или именованный экземпляр на локальном или удаленном компьютере. При подключении к именованному экземпляру введите имя сервера в следующем формате: \<*server*> @ no__t-3 @ no__t-4*instance*>.  
  
 При подключении к экземпляру компонента [!INCLUDE[ssDE](../../includes/ssde-md.md)] следует пользоваться учетными данными, имеющими разрешение на вход на сервер и обновление данных в базе данных. Диспетчер конфигурации служб [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] пользуется учетными данными текущего пользователя Windows, однако если пользователь не имеет имени входа или разрешений для доступа к базе данных, то необходимо указать имя входа в базу данных [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Другие учетные данные Windows указать нельзя. Если подключение необходимо производить от лица другого пользователя Windows, то следует войти от этого пользователя, а затем запустить диспетчер конфигурации служб [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 Для подключения к удаленному экземпляру прежде всего необходимо включить для него удаленные соединения. В некоторых версиях и выпусках [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] удаленные соединения по умолчанию отключены. Чтобы проверить, включены ли удаленные соединения, запустите диспетчер конфигурации [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] и убедитесь, что протокол TCP/IP и протокол именованных каналов включены. Если удаленный экземпляр является именованным, убедитесь в том, что на целевом сервере включена и запущена служба браузера [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Браузер [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] возвращает диспетчеру конфигурации служб [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] номер порта, который используется именованным экземпляром.  
  
 **База данных**  
 Позволяет указать имя базы данных сервера отчетов, в которой хранятся серверные данные. Можно указать существующую базу данных или создать новую.  
  
 После выбора **Создать новую базу данных** на странице «Действия» мастер отображает свойства, которые необходимы для ее создания. Диспетчер конфигураций [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] создает две базы данных, связанные по именам: базу данных для статических данных и временную базу данных для хранения данных сеанса и рабочих данных. Дополнительные сведения см. в разделе Электронная документация по [базам &#40;данных&#41; сервера отчетов в собственном режиме](../../reporting-services/report-server/report-server-database-ssrs-native-mode.md) в [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] электронной документации по.  
  
 Кроме того, можно выбрать существующую базу данных сервера отчетов. Диспетчер конфигурации служб [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] не отфильтровывает недопустимые базы данных. Допустимыми считаются базы данных, схема которых совместима со схемой сервера отчетов (базы данных, в которых отсутствуют необходимые таблицы, представления или хранимые процедуры, будут недоступны для выбора). Если выбрана база данных, которая была создана для предыдущей версии служб [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], то производится ее обновление до текущего формата.  
  
 **Язык**  
 Это значение задается только при создании новой базы данных сервера отчетов.  
  
 Это значение позволяет задать язык, на котором создаются описания и определения ролей. В службах [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] реализована модель проверки авторизации на основе ролей, включающая ряд стандартных ролей. Эти роли создаются единожды на указанном пользователем языке. Имена и описания ролей не отображаются на других языках, даже если подключиться к серверу отчетов с помощью браузера, в котором определены параметры культуры или языка, поддерживаемые сервером. Указанный язык определяет также язык, который используется при создании папки «Мои отчеты» и папок пользователей для работы с этой функцией.  
  
 **Режим сервера**  
 База данных сервера отчетов может работать либо в собственном режиме, либо в режиме интеграции с SharePoint. Эти режимы являются взаимоисключающими.  
  
 Режим должен быть указан при создании новой базы данных сервера отчетов. Он определяет структуру базы данных сервера отчетов и задает значение, которое имеет системное свойство `SharePointIntegrated` (`true` или `false`).  
  
 При выборе для сервера отчетов другой базы данных всегда отображается режим, в котором она находится.  
  
 **Учетные данные**  
 Задает учетную запись, используемую сервером отчетов для подключения к базе данных сервера отчетов. В качестве этого значения допускается указывать учетную запись веб-службы сервера отчетов, имя входа базы данных [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , определенное в экземпляре компонента [!INCLUDE[ssDE](../../includes/ssde-md.md)] , на котором размещен сервер отчетов, или учетную запись Windows. Если используется учетная запись Windows, можно указать локальную учетную запись ( *\<computername > \\ < username @ no__t-3*), если сервер отчетов и база данных находятся на одном компьютере или учетная запись пользователя домена ( *\<domain > \\ < username @ no__t-7*), если они находятся на разных компьютерах в одном домене.  
  
 Сервер отчетов создаст имя входа базы данных и присвоит для указанной учетной записи разрешения базы данных.  
  
 Сервер отчетов не создает саму учетную запись. Указанная учетная запись уже должна быть создана и доступна для текущей конфигурации развертывания. В частности, если при использовании учетной записи Windows база данных находится на удаленном компьютере, следует указывать учетную запись, имеющую разрешения для этого компьютера.  
  
 Если компьютер находится в другом домене или в недоверенном домене, то лучше пользоваться именем входа базы данных [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Дополнительные сведения о выборе учетной записи см. [в разделе Настройка подключения к &#40;базе данных сервера&#41;отчетов SSRS Configuration Manager](../../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md).  
  
 **Сводка**  
 Проверьте параметры перед настройкой соединения программой установки.  
  
 **Ход выполнения и завершение**  
 Проследите за ходом выполнения каждой из задач.  
  
## <a name="see-also"></a>См. также  
 [Основной &#40;режим&#41;базы данных SSRS](../../../2014/sql-server/install/database-ssrs-native-mode.md)   
 [Мастер &#40;изменения учетных данных служб&#41;SSRS в собственном режиме](../../../2014/sql-server/install/change-credentials-wizard-ssrs-native-mode.md)   
 [Создание базы данных сервера отчетов, работающего в собственном режиме (диспетчер конфигурации служб SSRS)](../../reporting-services/install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md)   
 [Диспетчер конфигурации служб Reporting Services разделы &#40;справки F1 службы SSRS в&#41;основном режиме](../../../2014/sql-server/install/reporting-services-configuration-manager-f1-help-topics-ssrs-native-mode.md)   
 [Настройка подключения к базе данных сервера отчетов (диспетчер конфигураций служб Reporting Services)](../../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)  
  
  
