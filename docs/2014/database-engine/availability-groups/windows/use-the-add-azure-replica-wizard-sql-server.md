---
title: Использование мастера добавления реплики Azure (SQL Server) | Документы Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.addreplicawizard.azurereplica.f1
ms.assetid: b89cc41b-07b4-49f3-82cc-bc42b2e793ae
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 90418193ac869641a20f8b0f684fc43dd46712f8
ms.sourcegitcommit: 3b1f873f02af8f4e89facc7b25f8993f535061c9
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/30/2019
ms.locfileid: "70175996"
---
# <a name="use-the-add-azure-replica-wizard-sql-server"></a>Использование мастера добавления реплики Azure (SQL Server)
  С помощью мастера добавления реплики Azure вы сможете создать виртуальную машину Azure в гибридной ИТ-службе и настроить ее в качестве вторичной реплики для новой или существующей группы доступности AlwaysOn.  
  
-   **Перед началом:**  
  
     [Предварительные требования](#Prerequisites)  
  
     [безопасность](#Security)  
  
-   **Добавление реплики с помощью**  [Мастер добавления реплики Azure (SQL Server Management Studio)](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> Перед началом  
 Если вы еще не добавили реплику доступности в группу доступности, см. разделы "экземпляры сервера" и "группы доступности и реплики" в разделе [Предварительные требования, ограничения и рекомендации для &#40;группы доступности AlwaysOn SQL. Сервер&#41;](prereqs-restrictions-recommendations-always-on-availability.md).  
  
###  <a name="Prerequisites"></a> Предварительные требования  
  
-   Необходимо подключиться к экземпляру сервера, на котором размещена текущая первичная реплика.  
  
-   Необходимо иметь гибридную ИТ-среду, в которой локальная подсеть имеет VPN-подключение типа "сеть — сеть" с Azure. Дополнительные сведения см. в разделе [Настройка виртуальной частной сети между площадками через портал управления](https://azure.microsoft.com/documentation/articles/vpn-gateway-site-to-site-create).  
  
-   Группа доступности должна содержать реплики доступности локально.  
  
-   Клиенты для прослушивателя группы доступности должны иметь возможность подключения к Интернету, если они хотят поддерживать подключение к прослушивателю при отработки отказа группы доступности в реплику Azure.  
  
-   **Предварительные условия для использования полной начальной синхронизации данных** Необходимо указать сетевой ресурс, чтобы мастер мог создавать и получать доступ к резервным копиям. Для каждой первичной реплики учетная запись, используемая для запуска [!INCLUDE[ssDE](../../../includes/ssde-md.md)] , должна иметь разрешения в файловой системе на чтение и запись в общей сетевой папке. Для вторичных реплик учетная запись должна иметь разрешение на чтение в сетевой папке.  
  
     Если нет возможности воспользоваться мастером для выполнения полной первоначальной синхронизации данных, то базы данных-получатели нужно подготовить вручную. Это можно сделать до или после запуска мастера. Дополнительные сведения см. в разделе [Подготовка базы данных-получателя для присоединения к группе доступности вручную (SQL Server)](manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md).  
  
###  <a name="Security"></a> безопасность  
  
####  <a name="Permissions"></a> Permissions  
 См. раздел [Security](use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md#Security)  
  
##  <a name="SSMSProcedure"></a> Работа с мастером добавления реплики Azure (SQL Server Management Studio)  
 Мастер добавления реплики Azure можно запустить на странице [Выбор реплик](specify-replicas-page-new-availability-group-wizard-add-replica-wizard.md). На эту страницу можно перейти двумя способами.  
  
-   [Использование мастера групп доступности (среда SQL Server Management Studio)](use-the-availability-group-wizard-sql-server-management-studio.md)  
  
-   [Использование мастера добавления реплики в группу доступности (среда SQL Server Management Studio)](use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md)  
  
 После того как был запущен мастер добавления реплики Azure, выполните следующие шаги.  
  
1.  Сначала скачайте сертификат управления для подписки Azure. Нажмите кнопку **Загрузить** , чтобы открыть страницу входа.  
  
2.  На странице входа войдите в свою подписку Azure. После входа мастер выполняет установку сертификата управления на ваш локальный компьютер. Этот сертификат управления автоматически загружается при последующем использовании этого мастера. Если было загружено несколько сертификатов управления, можно нажать кнопку **...** , чтобы выбрать нужный сертификат для использования.  
  
3.  Затем подключитесь к подписке, нажав кнопку **Подключиться**. После подключения раскрывающиеся списки заполняются параметрами Azure, такими как **Виртуальная сеть** и **подсеть виртуальной сети**.  
  
4.  Укажите параметры для виртуальной машины Azure, на которой будет размещена новая вторичная реплика:  
  
     Image  
     Имя образа SQL Server, используемого для виртуальной машины Azure  
  
     Размер виртуальной машины  
     Размер виртуальной машины Azure  
  
     Имя виртуальной машины  
     DNS-имя виртуальной машины Azure  
  
     Имя пользователя виртуальной машины  
     Имя пользователя администратора по умолчанию для виртуальной машины Azure  
  
     Пароль администратора виртуальной машины (и подтверждение пароля)  
     Пароль для администратора по умолчанию для виртуальной машины Azure  
  
     Виртуальная сеть  
     Виртуальная сеть, в которой будет размещена виртуальная машина Azure.  
  
     Подсеть виртуальной сети  
     Подсеть виртуальной сети, в которой будет размещена виртуальная машина Azure.  
  
     Домен  
     Домен Active Directory (AD) для приподключения к виртуальной машине Azure  
  
     Имя пользователя домена  
     Имя пользователя AD, используемое для приподключения виртуальной машины Azure к домену.  
  
     Пароль  
     Пароль, используемый для приподключения виртуальной машины Azure к домену.  
  
5.  Нажмите кнопку **ОК** , чтобы зафиксировать ваши параметры, и выйдите из мастера добавления реплики Azure.  
  
6.  Продолжайте выполнять остальные шаги конфигурации на странице [Выбор реплик](specify-replicas-page-new-availability-group-wizard-add-replica-wizard.md) так же, как и для любых новых реплик.  
  
     Завершив работу с мастером групп доступности или мастером добавления реплики в группу доступности, процесс настройки выполняет все операции в Azure, чтобы создать новую виртуальную машину, присоедините ее к домену AD, добавьте в кластер Windows, включив AlwaysOn High. Доступность и добавление новой реплики в группу доступности.  
  
##  <a name="RelatedTasks"></a> Связанные задачи  
  
-   [Добавление вторичной реплики к группе доступности (SQL Server)](add-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
## <a name="see-also"></a>См. также  
 [Общие сведения о &#40;группы доступности AlwaysOn SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Предварительные требования, ограничения и рекомендации для &#40;группы доступности AlwaysOn SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md)   
 [Добавление вторичной реплики к группе доступности (SQL Server)](add-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
  
