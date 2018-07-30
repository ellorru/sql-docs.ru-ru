---
title: Прямоугольники и линии (построитель отчетов и службы SSRS) | Документы Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: d6226b0c-0398-4185-8565-96099876fc21
caps.latest.revision: 9
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: ec70c7151ffe02978117c46e06abd3fa20ad4da6
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/02/2018
ms.locfileid: "37306964"
---
# <a name="rectangles-and-lines-report-builder-and-ssrs"></a>Прямоугольники и линии (построитель отчетов и службы SSRS)
  Для создания визуальных эффектов в отчете можно использовать прямоугольники и линии. Свойства отображения этих элементов отчета можно задать в разделе «Граница» вкладки «Главная», а другие свойства — с помощью панели «Свойства». Для прямоугольника можно добавлять такие характеристики, как цвет фона, изображение, подсказка или закладка.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="RectanglesLinesReportParts"></a> Использование прямоугольников и линий в качестве элементов отчета  
 Прямоугольники вместе с их содержимым можно опубликовать отдельно от отчета как элементы отчета. [!INCLUDE[ssRBrptparts](../../includes/ssrbrptparts-md.md)]  
  
 При этом нельзя публиковать как части отчета элементы отчета, содержащиеся в прямоугольнике. При добавлении пользователями прямоугольников к отчету выполняется добавление и прямоугольника, и содержащихся в нем элементов.  
  

  
##  <a name="RectangleAsContainer"></a> Использование прямоугольника в качестве контейнера  
 Прямоугольник можно использовать в качестве контейнера для других элементов. При перемещении прямоугольника элементы внутри него перемещаются вместе с ним. Элемент внутри прямоугольника отображает его имя в свойстве **Parent** . Дополнительные сведения об использовании прямоугольника как контейнера см. в разделах [Добавление прямоугольника или контейнера (построитель отчетов и службы SSRS)](add-a-rectangle-or-container-report-builder-and-ssrs.md) и [Отображение одних и тех же данных в матрице и на диаграмме (построитель отчетов)](display-the-same-data-on-a-matrix-and-a-chart-report-builder.md).  
  
> [!NOTE]  
>  Прямоугольник является всего лишь контейнером для элементов, которые создаются в прямоугольнике или перетаскиваются в него. Если нарисовать прямоугольник вокруг элемента, уже существующего в области конструктора, прямоугольник не будет функционировать как его контейнер. Прямоугольник будет отсутствовать в свойстве Parent этого элемента.  
  
 При помещении элементов отчета в прямоугольники необходимо учесть, какие изменения повлияют на эти элементы при подготовке отчета. Элементы отчета, которые содержат повторяющиеся строки данных (например, таблицы) развернутся таким образом, чтобы разместить все возвращенные запросом данные, и это повлияет на расположение других элементов в прямоугольнике. Таблица передвинет вниз элементы, расположенные ниже области данных. Чтобы привязать элемент к месту, можно расположить элемент отчета внутри прямоугольника, верхний край которого находится выше нижнего края таблицы. Дополнительные сведения см. в разделе [Поведение при подготовке к просмотру (построитель отчетов и службы SSRS)](rendering-behaviors-report-builder-and-ssrs.md).  
  

  
##  <a name="ReportBorder"></a> Добавление границы отчета  
 Можно добавить границу к отчету путем добавления границ к самим верхним колонтитулам, нижним колонтитулам и тексту отчета, не добавляя линии или прямоугольники. Дополнительные сведения см. в разделе [Add a Border to a Report &#40;Report Builder and SSRS&#41;](add-a-border-to-a-report-report-builder-and-ssrs.md).  
  

  
##  <a name="HowTo"></a> Инструкции  
 [Добавить границу к отчету &#40;построитель отчетов и службы SSRS&#41;](add-a-border-to-a-report-report-builder-and-ssrs.md)  
  
 [Добавление прямоугольника или контейнера &#40;построитель отчетов и службы SSRS&#41;](add-a-rectangle-or-container-report-builder-and-ssrs.md)  
  
 [Добавление и изменение линии &#40;построитель отчетов и службы SSRS&#41;](add-and-modify-a-line-report-builder-and-ssrs.md)  
  
## <a name="see-also"></a>См. также  
 [Добавление прямоугольника или контейнера &#40;построитель отчетов и службы SSRS&#41;](add-a-rectangle-or-container-report-builder-and-ssrs.md)  
  
  