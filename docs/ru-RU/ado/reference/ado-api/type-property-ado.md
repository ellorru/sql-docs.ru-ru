---
title: Type-свойство (ADO) | Документы Microsoft
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Parameter::Type
- Field20::Type
helpviewer_keywords:
- Type property [ADO]
ms.assetid: 8a4c079f-9f4f-4545-801d-85983b8db71e
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 91e4e4e3b7a4c1c16b16cb5ffc61c5337b761260
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/03/2018
---
# <a name="type-property-ado"></a>Свойство Type (ADO)
Тип рабочей тип или данные [параметр](../../../ado/reference/ado-api/parameter-object.md), [поле](../../../ado/reference/ado-api/field-object.md), или [свойство](../../../ado/reference/ado-api/property-object-ado.md) объекта.  
  
## <a name="settings-and-return-values"></a>Параметры и возвращаемые значения  
 Возвращает или задает [DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md) значение.  
  
## <a name="remarks"></a>Замечания  
 Для **параметр** объектов, **тип** свойство доступно для чтения/записи. Для новых **поле** объектов, добавленных в [поля](../../../ado/reference/ado-api/fields-collection-ado.md) коллекцию [запись](../../../ado/reference/ado-api/record-object-ado.md), **тип** доступен для чтения и записи только после [ Значение](../../../ado/reference/ado-api/value-property-ado.md) свойство **поле** был указан и поставщик данных успешно добавлен новый **поле** путем вызова [обновить](../../../ado/reference/ado-api/update-method.md)метод **поля** коллекции.  
  
 Для всех остальных объектов **тип** свойство доступно только для чтения.  
  
## <a name="applies-to"></a>Объект применения  
  
||||  
|-|-|-|  
|[Объект Field](../../../ado/reference/ado-api/field-object.md)|[Объект Parameter](../../../ado/reference/ado-api/parameter-object.md)|[Объект Property (ADO)](../../../ado/reference/ado-api/property-object-ado.md)|  
  
## <a name="see-also"></a>См. также  
 [Пример свойства типа (поле) (Visual Basic)](../../../ado/reference/ado-api/type-property-example-field-vb.md)   
 [Пример типа свойства (свойство) (VC ++)](../../../ado/reference/ado-api/type-property-example-property-vc.md)   
 [Свойство RecordType (ADO)](../../../ado/reference/ado-api/recordtype-property-ado.md)   
 [Свойство Type (объект Stream ADO)](../../../ado/reference/ado-api/type-property-ado-stream.md)