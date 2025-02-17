---
title: Архивация базы данных, страница "Параметры носителя" | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- swb.backupdatabase.mediaoptions.f1
- sql12.swb.backupdatabase.mediaoptions.f1
ms.assetid: eff36228-710c-4ed5-9af5-95859575dc0f
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: d1995ca52507a3027438cac21677517059d3d219
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2019
ms.locfileid: "70154831"
---
# <a name="back-up-database-media-options-page"></a>Резервное копирование базы данных (страница «Параметры носителя»)
  На странице  **Параметры носителя** диалогового окна **Резервное копирование базы данных** можно просмотреть или изменить параметры носителя базы данных.  
  
 **Создание резервной копии с помощью среды SQL Server Management Studio**  
  
-   [Создание полной резервной копии базы данных (SQL Server)](create-a-full-database-backup-sql-server.md)  
  
-   [Создание разностной резервной копии базы данных (SQL Server)](create-a-differential-database-backup-sql-server.md)  
  
> [!IMPORTANT]  
>  Для создания резервных копий базы данных можно составить план обслуживания базы данных. Дополнительные сведения см. в статьях [Планы обслуживания](../maintenance-plans/maintenance-plans.md) и [Использование мастера планов обслуживания](../maintenance-plans/use-the-maintenance-plan-wizard.md).  
  
> [!NOTE]  
>  Если задача резервного копирования определяется с помощью среды [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], можно создать соответствующий скрипт [!INCLUDE[tsql](../../includes/tsql-md.md)][BACKUP](/sql/t-sql/statements/backup-transact-sql) , нажав кнопку **Скрипт** и выбрав место назначения для этого скрипта.  
  
## <a name="options"></a>Параметры  
  
### <a name="overwrite-media"></a>Перезаписать носитель  
 Параметры панели **Перезаписать носитель** управляют записью резервной копии на носитель. Если в качестве места назначения резервного копирования на странице Общие диалогового окна Резервное копирование базы данных выбрано значение URL-адрес (служба хранилища Azure), то параметры в разделе Перезаписать носитель будут отключены. Можно перезаписать резервную копию с помощью инструкции Transact-SQL `BACKUP TO URL.. WITH FORMAT`. Дополнительные сведения см. в разделе [SQL Server Backup to URL](sql-server-backup-to-url.md).  
  
 Параметр **Создать резервную копию на новом носителе и удалить существующие резервные наборы данных** поддерживается только с применением параметров шифрования. Если выбрать параметры в разделе **Создать резервную копию на существующем носителе** , параметры шифрования на странице **Параметры резервного копирования** будут отключены.  
  
> [!NOTE]  
>  Сведения о наборах носителей см. в разделе [Наборы носителей, семейства носителей и резервные наборы данных (SQL Server)](media-sets-media-families-and-backup-sets-sql-server.md), подключен ленточный накопитель.  
  
 **Создать резервную копию в существующем наборе носителей**  
 Создание резервной копии базы данных на существующем наборе носителей. Если выбран этот параметр, становятся доступны еще три параметра.  
  
 Выберите один из следующих параметров.  
  
 **Добавить в существующий резервный набор данных**  
 Добавление резервного набора данных к существующему набору носителей с сохранением всех предыдущих резервных копий.  
  
 **Перезаписать все существующие резервные наборы данных**  
 Замена всех предыдущих резервных копий на существующем наборе носителей текущей резервной копией.  
  
 **Проверить имя набора носителей и срок действия резервного набора данных**  
 Этот необязательный параметр указывает, что при резервном копировании на существующий набор носителей должны проверяться имя и дата окончания срока хранения резервных наборов данных.  
  
 **Имя набора носителей**  
 Если выбран параметр **Проверить имя набора носителей и срок действия резервного набора данных** , можно указать имя набора носителей, который будет использоваться для операции резервного копирования.  
  
 **Создать резервную копию в новом наборе носителей и удалить все существующие резервные наборы данных**  
 Использование нового набора носителей и удаление существующих резервных наборов данных.  
  
 Если выбран этот параметр, становятся доступны следующие параметры.  
  
 **Имя нового набора носителей**  
 Введите имя нового набора носителей (необязательно).  
  
 **Описание нового набора носителей**  
 Введите значимое описание нового набора носителей (необязательно). Описание должно быть достаточно точным, чтобы правильно передавать содержание.  
  
### <a name="reliability"></a>Надежность  
 Параметры панели **Журнал транзакций** управляют обработкой ошибок во время операции резервного копирования.  
  
 **Проверить резервную копию после завершения операции**  
 Проверка полноты резервного набора данных и читаемости всех томов.  
  
 **Рассчитать контрольную сумму перед записью на носитель**  
 Проверка контрольных сумм перед записью на резервный носитель. Выбор этого параметра эквивалентен использованию параметра CHECKSUM в инструкции BACKUP языка [!INCLUDE[tsql](../../includes/tsql-md.md)]. Выбор этого параметра может привести к увеличению рабочей нагрузки и замедлению операции резервного копирования. Дополнительные сведения о резервных контрольных суммах см. в разделе [Возможные ошибки носителей во время резервного копирования и восстановления (SQL Server)](possible-media-errors-during-backup-and-restore-sql-server.md).  
  
 **Продолжить при возникновении ошибки**  
 Операция резервного копирования будет продолжаться даже в случае возникновения одной или нескольких ошибок.  
  
### <a name="transaction-log"></a>Журнал транзакций  
 Параметры панели **Журнал транзакций** управляют поведением резервной копии журнала транзакций. Эти параметры важны только в случае использования модели полного восстановления и модели восстановления с неполным протоколированием. Они активируются, только если в поле **Тип резервной копии** на странице **Общие** диалогового окна [Резервное копирование базы данных](../../integration-services/general-page-of-integration-services-designers-options.md) выбран **Журнал транзакций** .  
  
> [!NOTE]  
>  Сведения о том, как создавать резервные копии журналов, см. в разделе [Резервные копии журналов транзакций (SQL Server)](transaction-log-backups-sql-server.md).  
  
 **Усечь журнал транзакций**  
 Выполняется резервное копирование журнала транзакций, после чего он усекается для освобождения пространства. База данных остается в режиме в сети. Это параметр по умолчанию.  
  
 **Создать резервную копию заключительного фрагмента журнала и оставить базу данных в состоянии восстановления**  
 Создание резервной копии заключительного фрагмента журнала, при этом база данных остается в состоянии восстановления из копии. Если выбран этот параметр, создается *резервная копия заключительного фрагмента журнала*и выполняется резервное копирование журналов, которые еще не были скопированы (активный журнал). Как правило, это происходит при подготовке к восстановлению базы данных из копии. База данных будет недоступна для пользователей до полного восстановления.  
  
 Выбор этого параметра равнозначен использованию параметра WITH NO_TRUNCATE, NORECOVERY в инструкции [BACKUP](/sql/t-sql/statements/backup-transact-sql) (язык [!INCLUDE[tsql](../../includes/tsql-md.md)]). Дополнительные сведения см. в статье [Резервные копии заключительного фрагмента журнала (SQL Server)](tail-log-backups-sql-server.md).  
  
### <a name="tape-drive"></a>Ленточный накопитель  
 Параметры панели **Накопитель на магнитной ленте** управляют магнитной лентой во время операции резервного копирования. Эти параметры активируются, только если на панели **Назначение** на странице **Общие** диалогового окна [Резервное копирование базы данных](../../integration-services/general-page-of-integration-services-designers-options.md) выбран накопитель **Лента** .  
  
> [!NOTE]  
>  Дополнительные сведения об использовании ленточных устройств см. в статье [Устройства резервного копирования (SQL Server)](backup-devices-sql-server.md).  
  
 **Выгрузить ленту после резервного копирования**  
 Выгрузка ленты по окончании резервного копирования.  
  
 **Перемотать ленту перед выгрузкой**  
 Освобождение и перемотка ленты перед выгрузкой. Этот параметр доступен, только если задан параметр **Выгрузить ленту после резервного копирования** .  
  
## <a name="see-also"></a>См. также  
 [BACKUP (Transact-SQL)](/sql/t-sql/statements/backup-transact-sql)   
 [Создание резервной копии журнала транзакций (SQL Server)](back-up-a-transaction-log-sql-server.md)   
 [Создание резервных копий файлов и файловых групп (SQL Server)](back-up-files-and-filegroups-sql-server.md)   
 [Создание резервной копии журнала транзакций при повреждении базы данных (SQL Server)](back-up-the-transaction-log-when-the-database-is-damaged-sql-server.md)  
  
  
