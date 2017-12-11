---
title: "Изменения в схеме модели подключения к бизнес-данным для SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 882ea867-9acb-4313-99c9-865a523b72fd
ms.openlocfilehash: c95208da93af349ae768df7069c425eb088b8b30
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="changes-in-the-bdc-model-schema-for-sharepoint"></a>Изменения в схеме модели подключения к бизнес-данным для SharePoint
Узнайте, что изменилось в SharePoint для схемы модели BDC.
Количество изменений в схеме (BDCMetadata.xsd) для создания моделей BDC в SharePoint относительно невелико. Однако эти изменения оказывают значительное влияние на функцию Настройка Business Connectivity Services (BCS) и услуги.
  
    
    

Дополнительные сведения о схеме BDCMetadata можно [Справочник по схеме модели BDC для SharePoint](bdc-model-schema-reference-for-sharepoint.md).
## <a name="changes-to-complex-type-elements-in-bdcmetadataxsd"></a>Изменения в сложный тип элементов в BDCMetadata.xsd
<a name="bkmk_ChangesToElements"> </a>

В следующей таблице показаны какие изменения были внесены в элементах верхнего уровня в схеме BDCMetadata.
  
    
    

**В таблице 1. Новые сложных типов**


|**Элемент**|**Описание**|
|:-----|:-----|
|IndividuallySecurableMetadataObject  <br/> |Используется для назначения, что указанный **MetadataObject** возможность явным образом защищены, а не на связь по его родителя. <br/> |
|Метаданных (MetadataObject)  <br/> |Используется для хранения дополнительных метаданных о подключении к внешнему источнику данных.  <br/> |
   

## <a name="changes-to-simple-type-elements-in-bdcmetadataxsd"></a>Изменения в простом типе элементов в BDCMetadata.xsd
<a name="bkmk_ChangesToSimpleTypes"> </a>

В следующей таблице перечислены изменения, внесенные в атрибуты каждого элемента.
  
    
    

**В таблице 2. Изменения в простые типы**


|**Элемент**|**Описание**|
|:-----|:-----|
|Нет изменений  <br/> ||
   

## <a name="changes-to-attributes-in-bdcmetadataxsd"></a>Изменения в атрибутах в BDCMetadata.xsd
<a name="bkmk_ChangesToAttributes"> </a>

В следующей таблице перечислены изменения в атрибуты каждого элемента.
  
    
    

**В таблице 3. Изменения в атрибутах**


|**Атрибут**|**Родительский раздел**|**Описание**|
|:-----|:-----|:-----|
|Нет изменений  <br/> |||
   

## <a name="see-also"></a>См. также
<a name="bkmk_AdditionalResources"> </a>


-  [Business Connectivity Services в SharePoint](business-connectivity-services-in-sharepoint.md)
    
  
-  [Новые возможности служб Business Connectivity Services в SharePoint](what-s-new-in-business-connectivity-services-in-sharepoint.md)
    
  
-  [Начало работы со службами Business Connectivity Services в SharePoint](get-started-with-business-connectivity-services-in-sharepoint.md)
    
  
-  [Справочник по программистов Business Connectivity Services для SharePoint](business-connectivity-services-programmers-reference-for-sharepoint.md)
    
  
-  [Справочник по схеме модели BDC для SharePoint](bdc-model-schema-reference-for-sharepoint.md)
    
  

