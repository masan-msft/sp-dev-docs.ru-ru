---
title: "Изменения в схеме модели BDC для SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 882ea867-9acb-4313-99c9-865a523b72fd
ms.openlocfilehash: 95048677b9ef34f394c58d4a13c3edf5ab538754
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="changes-in-the-bdc-model-schema-for-sharepoint"></a><span data-ttu-id="357b9-102">Изменения в схеме модели BDC для SharePoint</span><span class="sxs-lookup"><span data-stu-id="357b9-102">Changes in the BDC model schema for SharePoint</span></span>
<span data-ttu-id="357b9-103">Узнайте, что изменилось в SharePoint для схемы модели BDC.</span><span class="sxs-lookup"><span data-stu-id="357b9-103">Learn what has changed in SharePoint for the BDC model schema.</span></span>
<span data-ttu-id="357b9-104">Количество изменений в схеме (BDCMetadata.xsd) для создания моделей BDC в SharePoint относительно невелико.</span><span class="sxs-lookup"><span data-stu-id="357b9-104">The number of changes in the schema (BDCMetadata.xsd) for creating BDC models in SharePoint is relatively small.</span></span> <span data-ttu-id="357b9-105">Однако эти изменения оказывают значительное влияние на функцию Настройка Business Connectivity Services (BCS) и услуги.</span><span class="sxs-lookup"><span data-stu-id="357b9-105">But these changes have significant impact on the feature set offerings of Business Connectivity Services (BCS).</span></span>
  
    
    

<span data-ttu-id="357b9-106">Дополнительные сведения о схеме BDCMetadata можно [Справочник по схеме модели BDC для SharePoint](bdc-model-schema-reference-for-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="357b9-106">For more information about the BDCMetadata schema, see  [BDC model schema reference for SharePoint](bdc-model-schema-reference-for-sharepoint.md).</span></span>
## <a name="changes-to-complex-type-elements-in-bdcmetadataxsd"></a><span data-ttu-id="357b9-107">Изменения в сложный тип элементов в BDCMetadata.xsd</span><span class="sxs-lookup"><span data-stu-id="357b9-107">Changes to complex type elements in BDCMetadata.xsd</span></span>
<span data-ttu-id="357b9-108"><a name="bkmk_ChangesToElements"> </a></span><span class="sxs-lookup"><span data-stu-id="357b9-108"></span></span>

<span data-ttu-id="357b9-109">В следующей таблице показаны какие изменения были внесены в элементах верхнего уровня в схеме BDCMetadata.</span><span class="sxs-lookup"><span data-stu-id="357b9-109">The following table shows what changes have been made to the top-level elements in the BDCMetadata schema.</span></span>
  
    
    

<span data-ttu-id="357b9-110">**В таблице 1. Новые сложных типов**</span><span class="sxs-lookup"><span data-stu-id="357b9-110">**Table 1. New complex types**</span></span>


|<span data-ttu-id="357b9-111">**Элемент**</span><span class="sxs-lookup"><span data-stu-id="357b9-111">**Element**</span></span>|<span data-ttu-id="357b9-112">**Описание**</span><span class="sxs-lookup"><span data-stu-id="357b9-112">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="357b9-113">IndividuallySecurableMetadataObject</span><span class="sxs-lookup"><span data-stu-id="357b9-113">IndividuallySecurableMetadataObject</span></span>  <br/> |<span data-ttu-id="357b9-114">Используется для назначения, что указанный **MetadataObject** возможность явным образом защищены, а не на связь по его родителя.</span><span class="sxs-lookup"><span data-stu-id="357b9-114">Used to designate that the specified **MetadataObject** is able to be secured explicitly and not by association to its parent.</span></span> <br/> |
|<span data-ttu-id="357b9-115">Метаданных (MetadataObject)</span><span class="sxs-lookup"><span data-stu-id="357b9-115">MetadataObject</span></span>  <br/> |<span data-ttu-id="357b9-116">Используется для хранения дополнительных метаданных о подключении к внешнему источнику данных.</span><span class="sxs-lookup"><span data-stu-id="357b9-116">Used to store additional metadata about the connection to the external data source.</span></span>  <br/> |
   

## <a name="changes-to-simple-type-elements-in-bdcmetadataxsd"></a><span data-ttu-id="357b9-117">Изменения в простом типе элементов в BDCMetadata.xsd</span><span class="sxs-lookup"><span data-stu-id="357b9-117">Changes to simple type elements in BDCMetadata.xsd</span></span>
<span data-ttu-id="357b9-118"><a name="bkmk_ChangesToSimpleTypes"> </a></span><span class="sxs-lookup"><span data-stu-id="357b9-118"></span></span>

<span data-ttu-id="357b9-119">В следующей таблице перечислены изменения, внесенные в атрибуты каждого элемента.</span><span class="sxs-lookup"><span data-stu-id="357b9-119">The following table lists the changes that have been made to the attributes of each element.</span></span>
  
    
    

<span data-ttu-id="357b9-120">**В таблице 2. Изменения в простые типы**</span><span class="sxs-lookup"><span data-stu-id="357b9-120">**Table 2. Changes to simple types**</span></span>


|<span data-ttu-id="357b9-121">**Элемент**</span><span class="sxs-lookup"><span data-stu-id="357b9-121">**Element**</span></span>|<span data-ttu-id="357b9-122">**Описание**</span><span class="sxs-lookup"><span data-stu-id="357b9-122">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="357b9-123">Нет изменений</span><span class="sxs-lookup"><span data-stu-id="357b9-123">No changes</span></span>  <br/> ||
   

## <a name="changes-to-attributes-in-bdcmetadataxsd"></a><span data-ttu-id="357b9-124">Изменения в атрибутах в BDCMetadata.xsd</span><span class="sxs-lookup"><span data-stu-id="357b9-124">Changes to attributes in BDCMetadata.xsd</span></span>
<span data-ttu-id="357b9-125"><a name="bkmk_ChangesToAttributes"> </a></span><span class="sxs-lookup"><span data-stu-id="357b9-125"></span></span>

<span data-ttu-id="357b9-126">В следующей таблице перечислены изменения в атрибуты каждого элемента.</span><span class="sxs-lookup"><span data-stu-id="357b9-126">The following table lists the changes to the attributes of each element.</span></span>
  
    
    

<span data-ttu-id="357b9-127">**В таблице 3. Изменения в атрибутах**</span><span class="sxs-lookup"><span data-stu-id="357b9-127">**Table 3. Changes to attributes**</span></span>


|<span data-ttu-id="357b9-128">**Атрибут**</span><span class="sxs-lookup"><span data-stu-id="357b9-128">**Attribute**</span></span>|<span data-ttu-id="357b9-129">**Родительский раздел**</span><span class="sxs-lookup"><span data-stu-id="357b9-129">**Parent**</span></span>|<span data-ttu-id="357b9-130">**Описание**</span><span class="sxs-lookup"><span data-stu-id="357b9-130">**Description**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="357b9-131">Нет изменений</span><span class="sxs-lookup"><span data-stu-id="357b9-131">No changes</span></span>  <br/> |||
   

## <a name="additional-resources"></a><span data-ttu-id="357b9-132">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="357b9-132">Additional resources</span></span>
<span data-ttu-id="357b9-133"><a name="bkmk_AdditionalResources"> </a></span><span class="sxs-lookup"><span data-stu-id="357b9-133"></span></span>


-  [<span data-ttu-id="357b9-134">Business Connectivity Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="357b9-134">Business Connectivity Services in SharePoint</span></span>](business-connectivity-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="357b9-135">Новые возможности служб Business Connectivity Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="357b9-135">What's new in Business Connectivity Services in SharePoint</span></span>](what-s-new-in-business-connectivity-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="357b9-136">Начало работы со службами Business Connectivity Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="357b9-136">Get started with Business Connectivity Services in SharePoint</span></span>](get-started-with-business-connectivity-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="357b9-137">Справочник по программистов Business Connectivity Services для SharePoint</span><span class="sxs-lookup"><span data-stu-id="357b9-137">Business Connectivity Services programmers reference for SharePoint</span></span>](business-connectivity-services-programmers-reference-for-sharepoint.md)
    
  
-  [<span data-ttu-id="357b9-138">Справочник по схеме модели BDC для SharePoint</span><span class="sxs-lookup"><span data-stu-id="357b9-138">BDC model schema reference for SharePoint</span></span>](bdc-model-schema-reference-for-sharepoint.md)
    
  

