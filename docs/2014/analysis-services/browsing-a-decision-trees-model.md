---
title: Просмотр решения модели дерева | Документация Майкрософт
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- mining models, browsing
- mining models, viewing
- tree viewer
- mining model, decision tree
- decision tree [data mining]
- dependency network
ms.assetid: 6b3dd1ae-caff-41c3-817b-802dc020ff88
caps.latest.revision: 15
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 077a392ff2374c89c5056e71c24fc6969b742a18
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/02/2018
ms.locfileid: "37255096"
---
# <a name="browsing-a-decision-trees-model"></a>Просмотр модели дерева принятия решений
  При открытии модели классификации с помощью **Обзор**, модель отображается в интерактивных средство просмотра дерева решений, аналогичную [!INCLUDE[msCoName](../includes/msconame-md.md)] средство просмотра дерева принятия решений в [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. В средстве просмотра отображаются результаты классификации в виде диаграммы, разработанной для выделения условий, которые отличают одну группу данных от другой. Также можно выполнить детализацию до отдельных подмножеств дерева и получить базовые данные.  
  
##  <a name="bkmk_Top"></a> Просмотр модели  
 Модели на основе алгоритма деревьев решений содержат много полезных сведений, которые рекомендуется изучить. **Обзор** окно содержит следующие вкладки и области, которые помогут вам изучить шаблоны и спрогнозировать результаты с помощью диаграммы:  
  
-   [Дерево принятия решений](#BKMK_DecisionTree)  
  
-   [Сеть зависимостей](#BKMK_DNetwork)  
  
 Для экспериментов с моделью дерева решений можно использовать образцы данных на вкладке «Обучающие данные» (или «Исходные данные») книги с образцами данных и построить модель дерева решений, использовав «Покупатель велосипеда» в качестве прогнозируемого атрибута.  
  
###  <a name="BKMK_DecisionTree"></a> Дерево принятия решений  
 Это представление может помочь в понимании и исследовании факторов, которые привели к получению результата.  
  
 Диаграмму дерева решений можно читать слева направо следующим образом.  
  
-   Прямоугольники, которые называются *узлы*, содержат подмножества данных. Метка на узле указывает определяющие характеристики этого подмножества.  
  
-   Крайний левый узел с меткой **все**, представляет полный набор данных. Все последующие узлы представляют подмножества данных.  
  
-   Дерево принятия решений содержит множество *разделяет*, или местах, где данные разбиваются на несколько наборов на основе атрибутов.  
  
     Например, в образце первое разбиение модели разделяет набор данных на три группы по возрасту.  
  
-   Разбиение сразу после **все** узел является наиболее важным, так как оно отображает Основное условие, которое делит этого набора данных.  
  
     Дополнительные разбиения расположены справа. Таким образом, путем анализа различных фрагментов дерева можно определить атрибуты, оказывающие наибольшее влияние на оценку возможности приобретения.  
  
 ![Диаграмма сети зависимостей для модели взаимосвязей](media/dm13-dec-tree-split-definition.gif "диаграммы сети зависимостей для модели взаимосвязей")  
  
 Используя эти сведения, можно сосредоточить маркетинговую кампанию на клиентах, которым просто необходимо поощрение для совершения покупки.  
  
##### <a name="explore-the-decision-tree"></a>Просмотр дерева решений  
  
1.  Нажмите кнопку **все** узел и посмотрите **обозначения интеллектуального анализа данных**.  
  
     Они указывают точное число вариантов в наборе данных для обучения, а также распределение выходных данных.  
  
     Эти сведения можно просмотреть в подсказке при наведении указателя мыши на узел.  
  
2.  Щелкните знак «плюс» и «минус» рядом с каждым узлом, чтобы развернуть или свернуть дерево.  
  
     Можно также использовать **Показать уровень** ползунок, чтобы развернуть или свернуть дерево.  
  
3.  Обратите внимание на то, что некоторые узлы темнее, чем другие.  
  
     По умолчанию **заполнение** используется как переменная заливки, это означает, что насыщенность цвета показано, какие узлы имеют наибольшую поддержку.  
  
     Поэтому крайний левый узел является наиболее темным, поскольку он содержит весь набор данных.  
  
4.  Измените значение **фона** из **всех случаях** для **Да**.  
  
     ![Изменение диаграммы дерева принятия решений для выделения покупателей](media/dm13-dectreeshadedbuyer.gif "изменение диаграммы дерева принятия решений для выделения покупателей")  
  
5.  Теперь насыщенность цвета показывает, сколько клиентов в каждом узле купили велосипед, т.е. интересующий нас показатель.  
  
     Обратите внимание на цветные линии в каждом узле. Это гистограмма, показывающая распределение выходных данных в этом подмножество данных. Например, в дереве решений образец «Покупатель велосипеда» цветная полоса указывает долю клиентов, купивших велосипеды (значения «Да») от тех, которые не (нет значения). Чтобы получить точные значения, можно щелкнуть узел, чтобы просмотреть **обозначения интеллектуального анализа данных**.  
  
6.  Проанализировав диаграмму, можно определить, как каждое подмножество данных разделено на более мелкие группы и какие атрибуты наиболее полезны при прогнозировании результата.  
  
     Интенсивность заливки позволяет сосредоточиться на нескольких наиболее важных группах и получить более подробные данные о них для выполнения сравнения. Например, эти группы имеют очень высокую вероятность покупки велосипедов:  
  
    -   Возраст > = 32 и \< 53 и годовой доход > = 26000 и детей = 0  
  
         Всего вариантов: 1150  
  
         Покупатель вероятность покупки велосипеда: 18%  
  
    -   Возраст > = 32 и \< 53 и годовой доход > = 26000 и детей не = 0 и семейное положение = «Холост»  
  
         Всего вариантов: 402  
  
         Покупатель вероятность покупки велосипеда: 16%  
  
7.  Измените значение **фона** из **Да** для **нет** и увидеть, как диаграмма изменится.  
  
     ![Диаграмма сети зависимостей для модели взаимосвязей](media/dm13-dec-tree-background-no.gif "диаграммы сети зависимостей для модели взаимосвязей")  
  
 **Советы**  
  
-   Если данные можно разделить на несколько рядов, другая модель создается для каждого набора данных, подлежащего моделированию.  
  
-   В образце модели данных существует только один прогнозируемый результат — «Покупатель велосипеда»; но предположим, что имеются сведения о совершении клиентом покупки плана обслуживания, и этот результат также необходимо спрогнозировать. В таком случае эти данные будут указаны в отдельном столбце и в модель будут включены два прогнозируемых атрибута.  
  
     Нажмите кнопку **гистограммы** параметр в верхнем левом углу панели дерева решений, чтобы изменить максимальное число состояний, которые могут присутствовать в гистограммах дерева. Это полезно, когда у прогнозируемого атрибута много состояний. Состояния появляются на гистограмме упорядоченными по степени распространенности, слева направо.  
  
-   Можно также использовать параметры на **дерево принятия решений** вкладку для изменения способа отображения дерева, увеличение и уменьшение или изменения размера диаграммы по размеру окна.  
  
-   Используйте ползунок **Расширение по умолчанию** для установки количества уровней по умолчанию, которые отображаются для всех деревьев в модели.  
  
-   Выберите **Показывать длинное имя** для отображения полное имя атрибута, включая источник данных. Короткие и длинные имена одинаковы, если только атрибуты не получены из различных источников данных.  
  
 [К началу страницы](#bkmk_Top)  
  
###  <a name="BKMK_DNetwork"></a> Сеть зависимостей  
 **Сеть зависимостей** представление отображает связи между входными атрибутами и прогнозируемыми атрибутами модели.  
  
1.  Перетащите ползунок в левой части средства просмотра  
  
     В верхней части отображаются все связи. Если переместить ползунок ниже, будут видны только наиболее прочные из них.  
  
2.  Теперь выберите узел «Покупатель велосипеда».  
  
     ![Представление сети зависимостей для деревьев принятия решений](media/dm13-dectree-depnet.gif "представление сети зависимостей для деревьев принятия решений")  
  
     После выбора узла в средстве просмотра выделяются зависимости, относящиеся к узлу. В этом случае в средстве просмотра выделяется каждый узел, позволяющий прогнозировать результат.  
  
3.  Средство просмотра содержит много узлов, вы можете найти нужные с помощью **найти узел** кнопки. После нажатия кнопки **Найти узел** откроется диалоговое окно **Поиск узла** , где можно использовать фильтр для поиска и выбора нужных узлов.  
  
4.  Условные обозначения в нижней части средства просмотра связывают цветовые коды с типом зависимости на графе. Например, при выборе прогнозируемого узла он выделяется бирюзовым цветом, а узлы, которые прогнозируют выбранный узел, — оранжевым цветом.  
  
 [К началу страницы](#bkmk_Top)  
  
### <a name="drill-through-to-underlying-data"></a>Углубленная детализация до базовых данных  
 Несколько типов моделей поддерживают возможность *детализацию* из модели к основополагающим данным варианта. Это может быть полезно, если нужно связаться с клиентами в определенном сегменте или извлечь данные для дальнейшего анализа.  
  
##### <a name="get-case-data"></a>Извлечение данных вариантов  
  
1.  Щелкните правой кнопкой мыши узел дерева, содержащий нужные данные, и выберите один из следующих вариантов.  
  
    -   **Детализация по модели**. Этот аргумент возвращает варианты, принадлежащие выбранному узлу, и сохраняет их в таблице в Excel. Возвращаются только столбцы данных, которые действительно использовались для построения модели.  
  
    -   **Детализировать столбцы структуры**. Этот аргумент возвращает варианты, принадлежащие выбранному узлу, и сохраняет их в таблице в Excel. Будут получены все сведения, которые были доступны в базовых данных при построении, даже данные столбца, который не был использован в модели. Например, адрес клиента и почтовый индекс могли быть исключены, поскольку эти поля не требуются для анализа, но они остались в структуре.  
  
     Вернитесь в Excel, чтобы просмотреть данные. Средство просмотра «Обзор» выполняет запрос, сохраняет данные в таблице на новом листе и присваивает метки результатам.  
  
     ![результаты детализации сохраняются в таблице Excel](media/dm13-dectree-drillthroughresults.gif "результаты детализации сохраняются в таблице Excel")  
  
## <a name="see-also"></a>См. также  
 [Просмотр моделей в Excel &#40;надстройки интеллектуального анализа данных SQL Server&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md)  
  
  