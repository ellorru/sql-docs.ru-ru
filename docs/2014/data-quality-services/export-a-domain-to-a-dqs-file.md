---
title: Экспорт домена в файл DQS | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: eba10d3d-b5c4-447b-8a30-fa07996cb28e
caps.latest.revision: 17
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: c1257e0ff051e56974c7c187ec214e8cbe357dba
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/02/2018
ms.locfileid: "37232044"
---
# <a name="export-a-domain-to-a-dqs-file"></a>Экспорт домена в файл .dqs
  В этом разделе описывается экспорт домена в файл .dqs в службах [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS). Экспортировать в файл данных можно домен или всю базу знаний. Сведения об экспорте базы знаний см. в разделе [Экспорт базы знаний в файл DQS](../../2014/data-quality-services/export-a-knowledge-base-to-a-dqs-file.md).  
  
 Экспорт домена из одной базы знаний в файл данных DQS и последующий импорт в другую базу знаний упрощает процесс создания знаний и экономит время. Благодаря этому можно использовать домен и его набор знаний совместно с другими пользователями.  
  
 Можно экспортировать один одиночный домен или один составной домен. Файл DQS содержащий один домен, включает все сведения о домене, включая свойства домена, значения и сведения о правилах, кроме сведений о добавленных ссылочных данных. Файл DQS, содержащий составной домен, содержит все данные составного домена, в том числе все данные для доменов, которые входят в составной домен, а также свойства, связи и правила составного домена, кроме сведений о ссылочных данных. После импорта файла DQS следует повторно добавить домен или составной домен в соответствующие службы ссылочных данных. Экспортируются как опубликованные, так и неопубликованные данные.  
  
 Файл данных DQS, созданный в процессе экспорта, зашифровывается, его просмотр становится невозможным.  
  
##  <a name="BeforeYouBegin"></a> Перед началом  
  
###  <a name="Prerequisites"></a> Предварительные требования  
 Чтобы экспортировать домен в файл данных .dqs, необходимо предварительно создать и выбрать одиночный домен или составной домен, содержащий несколько одиночных доменов. Файл DQS не требуется, он будет создан в процессе экспорта.  
  
###  <a name="Security"></a> безопасность  
  
####  <a name="Permissions"></a> Permissions  
 Для экспорта домена в файл данных .dqs необходимы роли dqs_kb_editor или dqs_administrator в базе данных DQS_MAIN.  
  
##  <a name="Export"></a> Export a domain to a .dqs file  
 Можно выполнить экспорт с любой страницы «Управление доменами». Команда экспорта доступна как в виде элемента управления в пользовательском интерфейсе, так и в виде команды контекстного меню на панели «Список доменов».  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Запуск клиентского приложения Data Quality Client](../../2014/data-quality-services/run-the-data-quality-client-application.md).  
  
2.  На главном экране клиента [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] откройте базу знаний в разделе управления доменами.  
  
3.  На странице **Управление доменами** (с любой выбранной вкладкой) выберите одиночный или составной домен в списке **Домен** .  
  
4.  Щелкните значок **Экспортировать данные базы знаний** над списком доменов, затем щелкните **Экспортировать домен**. Также можно щелкнуть правой кнопкой мыши домен в списке **Домен** , указать пункт **Экспорт**, а затем выбрать команду **Экспортировать домен**.  
  
5.  В диалоговом окне **Экспорт в файл данных** перейдите в папку, где нужно сохранить файл, присвойте файлу имя или оставьте имя по умолчанию, оставьте **Файлы данных DQS (\*.dqs)** в качестве **Типа файла** и нажмите кнопку **Сохранить**.  
  
6.  В диалоговом окне **Экспортировать домен** убедитесь, что в строке состояния диалогового окна отобразилось сообщение о завершении экспорта. Нажмите кнопку **ОК**.  
  
##  <a name="FollowUp"></a> Дальнейшие действия. После экспорта домена в файл DQS  
 После экспорта домена в файл DQS можно импортировать домен в другую базу знаний.  
  
  