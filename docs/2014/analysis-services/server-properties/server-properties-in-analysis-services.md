---
title: Настройка свойств сервера в службах Analysis Services | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SSAS, configuration properties
- Analysis Services, configuration properties
- SQL Server Analysis Services, configuration properties
- configuration options [Analysis Services]
- server properties [Analysis Services]
- properties [Analysis Services], configuration
- properties [Analysis Services]
ms.assetid: 274b89cd-14ed-4666-bc13-eedf1de51e18
caps.latest.revision: 19
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 19f6f04dfe165cb5f3af5bd5587232d65c8c4582
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/02/2018
ms.locfileid: "37247354"
---
# <a name="configure-server-properties-in-analysis-services"></a>Настройка свойств сервера в службах Analysis Services
  Администратор служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] может изменить по умолчанию свойства конфигурации сервера для экземпляра служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. У всех экземпляров имеются собственные свойства конфигурации, которые можно задать независимо от других экземпляров на этом же сервере.  
  
 Для задания свойств сервера используйте среду SQL Server Management Studio или измените файл msmdsrv.ini соответствующего экземпляра.  
  
 Этот раздел состоит из следующих подразделов.  
  
 [Настройка свойств сервера (экземпляр)](#bkmk_config)  
  
 [Справочник по свойствам сервера](#bkmk_ref)  
  
##  <a name="bkmk_config"></a> Настройка свойств сервера (экземпляр)  
 Страницы свойств в среде SQL Server Management Studio содержат подмножество доступных свойств, при этом отображаются только те из свойств, которые с наибольшей вероятностью могут быть изменены. Полный набор свойств содержится в файле msmdsrv.ini.  
  
> [!NOTE]  
>  В этом разделе не описываются свойства конфигурации развертывания в среде [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Дополнительные сведения о конфигурации развертывания, см. в разделе [Указание настроек конфигурации для развертывания решения](../multidimensional-models/deployment-script-files-solution-deployment-config-settings.md).  
  
#### <a name="view-or-set-configuration-properties-in-management-studio"></a>Просмотр и настройка свойств конфигурации в среде Management Studio  
  
1.  В среде [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]подключитесь к экземпляру служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
     В обозревателе объектов щелкните правой кнопкой мыши экземпляр служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] и выберите пункт **Свойства**. Отображается страница «Общие», содержащая основные свойства.  
  
2.  Для просмотра дополнительных свойств установите флажок **Показать дополнительные (все) свойства** в нижней части страницы.  
  
     Изменение свойств сервера поддерживается только для серверов в табличном и многомерном режимах. Если установлен [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)], всегда используйте значения по умолчанию, если только инженер службы технической поддержки Майкрософт не даст другие указания.  
  
     Указания по решению проблем, связанных с функционированием или производительностью, путем изменения свойств сервера см. в [Руководстве по использованию служб SQL Server 2008 R2 Analysis Services](http://go.microsoft.com/fwlink/?LinkID=225539).  
  
     Кроме того, дополнительные сведения о свойствах сервера (многие из которых не изменялись в последних нескольких выпусках) можно получить в техническом документе Майкрософт [Свойства сервера служб SQL Server 2005 Analysis Services (SSAS)](http://go.microsoft.com/fwlink/?LinkID=199102).  
  
    > [!NOTE]  
    >  Определенные свойства можно задать только в файле msmdrsrv.ini. Если свойство, которое необходимо задать, не отображается даже после включения дополнительных свойств, может потребоваться внести изменения непосредственно в файл msmdsrv.ini.  
  
#### <a name="view-or-edit-configuration-properties-in-the-msmdsrvini-file"></a>Просмотр и изменение свойств конфигурации в файле msmdsrv.ini  
  
1.  Перед началом работы проверьте свойство **DataDir** на странице свойств «Общие» в среде Management Studio, чтобы проверить, где находятся программные файлы служб Analysis Services, в том числе файл msmdsrv.ini. Это позволит гарантировать, что изменения вносятся в правильный файл.  
  
    > [!NOTE]  
    >  В установке по умолчанию файл находится в папке \Program Files\Microsoft SQL Server\MSAS12.MSSQLSERVER\OLAP\Config  
  
2.  Создайте резервную копию файла на случай необходимости использования исходного файла.  
  
3.  Используйте текстовый редактор для просмотра и изменения файла msmdsrv.ini.  
  
4.  После сохранения файла необходимо перезапустить службу.  
  
##  <a name="bkmk_ref"></a> Справочник по свойствам сервера  
 Свойства конфигурации служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] применяются для тонкой настройки системы. Например, чтобы настроить поведение журнала запросов в соответствии со своими требованиями, нужно установить соответствующие свойства.  
  
 В следующих разделах описаны различные [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] свойства конфигурации:  
  
|Раздел|Описание|  
|-----------|-----------------|  
|[Общие свойства](general-properties.md)|К общим свойствам относятся основные и расширенные свойства, а так же свойства, которые определяют каталог данных, каталог резервного копирования и другие характеристики сервера.|  
|[Свойства интеллектуального анализа данных](data-mining-properties.md)|Свойства интеллектуального анализа данных позволяют включать или отключать различные алгоритмы интеллектуального анализа. По умолчанию все алгоритмы включены.|  
|объекты DSO|Объекты DSO теперь не поддерживаются. Свойства DSO не обрабатываются.|  
|[Свойства функций](feature-properties.md)|Свойства функций служат для настройки возможностей продуктов, большинство из которых являются расширенными, включая свойства, управляющие связями между экземплярами сервера.|  
|[Свойства хранилища файлов](filestore-properties.md)|Свойства файлового хранилища предназначены только для расширенного использования. К этим свойствам относятся расширенные параметры управления памятью.|  
|[Свойства диспетчера блокировок](lock-manager-properties.md)|Свойства диспетчера блокировок управляют блокировками и временем ожидания сервера. Большинство из них предназначены только для расширенного использования.|  
|[Свойства журнала](log-properties.md)|Свойства журналов управляют регистрацией событий на сервере, если она используется. Они позволяют настроить регистрацию ошибок и исключений, «черный ящик», регистрацию запросов и трассировку.|  
|[Свойства памяти](memory-properties.md)|Свойства памяти управляют использованием памяти сервером. Они предназначены, главным образом, для расширенного использования.|  
|[Свойства сети](network-properties.md)|Сетевые свойства контролируют работу сервера в сети, к ним относятся свойства, управляющие сжатием и двоичными файлами XML. Большинство из них предназначены только для расширенного использования.|  
|[Свойства OLAP](olap-properties.md)|Свойства OLAP управляют обработкой кубов и измерений, отложенной обработкой, кэшированием данных и поведением запросов. К ним относятся и основные, и расширенные свойства.|  
|[Свойства безопасности](security-properties.md)|Раздел безопасности содержит основные и расширенные свойства, определяющие разрешения доступа. К ним относятся параметры, управляющие действиями администраторов и пользователей.|  
|[Свойства пула потоков](thread-pool-properties.md)|Свойства пула потоков управляют количеством потоков, которые создает сервер. Они предназначены, главным образом, для расширенного использования.|  
  
## <a name="see-also"></a>См. также  
 [Управление экземплярами служб Analysis Services](../instances/analysis-services-instance-management.md)   
 [Указание настроек конфигурации для развертывания решения](../multidimensional-models/deployment-script-files-solution-deployment-config-settings.md)  
  
  