---
title: Администрирование DQS | Microsoft Docs
ms.custom: ''
ms.date: 10/01/2012
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
helpviewer_keywords:
- dqs administration
- administration
- dqs,adminstration
ms.assetid: 9940ef5d-f6f6-4dec-9414-1077a4d7f12b
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: b801dd3792755c93006c1c6a48cfa9dc5af9cc37
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2019
ms.locfileid: "70152463"
---
# <a name="dqs-administration"></a>администрирование DQS

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Службы[!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) позволяют администрировать различные операции DQS, которые выполняются на сервере [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)], и управлять ими, настраивать свойства уровня сервера, связанные с операциями DQS, настраивать параметры службы эталонных данных и задавать параметры журнала DQS. Эти задачи выполняются в компоненте **Администрирование** клиента [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]. В зависимости от уровня доступа (роли) в DQS вам предоставляется или запрещается доступ к определенным функциям в этой области.  
  
 Помимо административных операций, в этом разделе даны сведения о резервном копировании и восстановлении баз данных DQS. Эти задачи не выполняются в клиенте [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)].  
  
 Компонент администрирования в клиенте [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] дает следующие преимущества.  
  
-   Позволяет диспетчерам данных мониторить различные операции DQS на сервере [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] с клиента [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)].  
  
-   Позволяет администраторам DQS мониторить операции DQS на сервере [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] с клиента [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]и в случае необходимости *завершать* выполняющуюся операцию или *останавливать* выполняющийся процесс в рамках операции.  
  
-   Настройка параметров службы эталонных данных, таких как Настройка подключения к Azure Marketplace и Управление прямыми поставщиками сторонних служб ссылочных данных.  
  
-   Настраивает пороговые значения для операций очистки и сопоставления.  
  
-   Включает и отключает уведомления в [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)].  
  
-   Настраивает ведение журнала в зависимости от степени серьезности событий.  
  
##  <a name="AdminUsingClent"></a> Административные действия в клиенте DQS  
 Эти действия выполняются в компоненте **Администрирование** клиента [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)].  
  
### <a name="activity-monitoring"></a>Мониторинг активности  
 Экран **Мониторинг активности** в клиенте [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] показывает подробные сведения о каждой операции, выполняемой на сервере [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]. Этот экран рассчитан в основном на диспетчеров данных и предназначен для высокоуровневого мониторинга всех действий, выполняемых на сервере [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] , к которому подключено приложение [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] . Он не предоставляет средств мониторинга на системном уровне. Кроме того, этот экран позволяет администраторам DQS управлять операцией или входящим в нее процессом, завершая выполняющуюся операцию или останавливая выполняющийся процесс в случае необходимости. Отображаются данные для обнаружения знаний, управления доменами, политики сопоставления, очистки, сопоставления и очистки на основе служб SQL Server Integration Services (SSIS).  
  
### <a name="configuration"></a>Конфигурация  
 Экран **Конфигурация** в клиенте [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] позволяет администратору DQS выполнять следующие действия.  
  
-   **Ссылочные данные**. Настройка поставщиков служб ссылочных данных: Azure Marketplace или прямые поставщики служб ссылочных данных. После настройки поставщиков служб ссылочных данных вы можете сопоставить домен или составной домен с эталонными данными в рамках операции управления доменами в базе знаний, а затем использовать эту же базу знаний для операции очистки в проекте качества данных. Он также позволяет указать параметры прокси-сервера для подключения к Интернету для использования Azure Marketplace.  
  
-   **Общие параметры**. Задайте пороговые значения для очистки данных и сопоставления данных, а также укажите, следует ли включить уведомления для [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]профилирования в. Эти пороговые значения используются DQS в ходе автоматических операций очистки и сопоставления в проекте качества данных.  
  
-   **Параметры журнала**. Файлы журналов в DQS записывают действия, выполненные в DQS, и полезны для отслеживания проблем в работе при обслуживании и устранении неполадок. Вы можете отфильтровать сообщения, которые нужно регистрировать для различных функций DQS (управление доменами, обнаружение знаний, очистка, сопоставление и службы эталонных данных) и модулей DQS в зависимости от степени серьезности событий.  
  
> [!NOTE]  
>  Экран **Конфигурация** доступен только пользователям, входящим в роль dqs_administrator в базе данных DQS_MAIN.  
  
##  <a name="AdminOutsideClient"></a> Административные действия вне клиента DQS  
 Эти действия выполняются за пределами клиента DQS:  
  
-   **Резервное копирование и восстановление баз данных DQS**. Резервное копирование и восстановление баз данных DQS выполняется так же, как резервное копирование и восстановление базы данных SQL Server с некоторыми соображениями, специфичными для DQS.  
  
-   **Присоединение и отсоединение баз данных DQS**. Действия по отсоединению и присоединению баз данных DQS аналогичны отсоединению и присоединению любой базы данных SQL Server с некоторыми соображениями, характерными для DQS.  
  
 Дополнительные сведения см. в статье [Manage DQS Databases](../data-quality-services/manage-dqs-databases.md).  
  
## <a name="related-tasks"></a>Связанные задачи  
  
|Описание задачи|Раздел|  
|----------------------|-----------|  
|Описывает мониторинг операций в DQS.|[Мониторинг операций DQS](../data-quality-services/monitor-dqs-activities.md)|  
|Описывает настройку параметров эталонных данных в DQS.|[Настройка служб DQS для использования ссылочных данных](../data-quality-services/configure-dqs-to-use-reference-data.md)|  
|Описывает настройку пороговых значений для операций очистки и сопоставления.|[Configure Threshold Values for Cleansing and Matching](../data-quality-services/configure-threshold-values-for-cleansing-and-matching.md)|  
|Описывает включение и отключение уведомлений в DQS.|[Включение или отключение уведомлений по профилированию в DQS](../data-quality-services/enable-or-disable-profiling-notifications-in-dqs.md)|  
|Описывает настройку ведения журнала DQS в зависимости от степени серьезности событий.|[Настройка степеней серьезности для файлов журнала DQS](../data-quality-services/configure-severity-levels-for-dqs-log-files.md)|  
|Описывает настройку дополнительных параметров для ведения журнала DQS.|[Настройка дополнительных параметров для файлов журнала DQS](../data-quality-services/configure-advanced-settings-for-dqs-log-files.md)|  
|Описывает создание резервной копии и восстановление баз данных DQS.|[Резервное копирование и восстановление баз данных DQS](../data-quality-services/backing-up-and-restoring-dqs-databases.md)|  
|Описывает, как отсоединять и присоединять базы данных DQS.|[Присоединение и отсоединение баз данных DQS](../data-quality-services/detaching-and-attaching-dqs-databases.md)|  
  
## <a name="see-also"></a>См. также  
 [Службы эталонных данных в DQS](../data-quality-services/reference-data-services-in-dqs.md)   
 [Управление файлами журнала DQS](../data-quality-services/manage-dqs-log-files.md)   
 [Управление базами данных DQS](../data-quality-services/manage-dqs-databases.md)  
  
  
