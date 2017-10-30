---
title: "Выполнение обхода связанных внешних типов контента в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 187ec42e-f749-4e22-abef-1df604143063
ms.openlocfilehash: 492c481703b7bb16a4c709d65f1698a06e024ded
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-crawl-associated-external-content-types-in-sharepoint"></a><span data-ttu-id="24268-102">Как: обход связанных внешних типов контента в SharePoint</span><span class="sxs-lookup"><span data-stu-id="24268-102">How to: Crawl associated external content types in SharePoint</span></span>
<span data-ttu-id="24268-103">В этой статье описывается использование свойств, имеющих отношение к поиску, в модели метаданных Служба подключения к бизнес-данным (BDC) для обхода связей, а также различные взаимодействия с пользователем, которые можно задействовать.</span><span class="sxs-lookup"><span data-stu-id="24268-103">Learn how to use the search specific properties in the Business Data Connectivity (BDC) service metadata model for crawling associations, and the different user experiences that you can enable.</span></span>
## <a name="crawling-the-associated-external-content-type"></a><span data-ttu-id="24268-104">Обход связанного внешнего типа контента</span><span class="sxs-lookup"><span data-stu-id="24268-104">Crawling the associated external content type</span></span>
<span data-ttu-id="24268-105"><a name="HowToCrawlAssociations_CrawlingAssociatedExternalTypes"> </a></span><span class="sxs-lookup"><span data-stu-id="24268-105"></span></span>

<span data-ttu-id="24268-p101">Службы Microsoft Business Connectivity Services (BCS) позволяет связать два связанных внешних типов контента, который затем позволяет извлечь связанные внешнего контента. Например внешнее содержимое можно извлечь из двух SQL Server базы данных на основе таблицы внешних типов контента, основанных на внешних ключей. Эта концепция компоновки два связанных внешних типов контента, называется  *связь*  . Дополнительные сведения о сопоставлениях [Добавление связей между внешними типами контента](http://msdn.microsoft.com/library/791e95ab-9b3c-413b-be12-bd0e59962c93%28Office.15%29.aspx)см.</span><span class="sxs-lookup"><span data-stu-id="24268-p101">Microsoft Business Connectivity Services (BCS) enables you to link two related external content types, which then enables you to fetch related external content. For example, you can fetch external content from two SQL Server database table-based external content types that are based on foreign keys. This concept of linking two related external content types is known as an  *association*  . For more information about associations, see [Adding Associations Between External Content Types](http://msdn.microsoft.com/library/791e95ab-9b3c-413b-be12-bd0e59962c93%28Office.15%29.aspx).</span></span> 
  
    
    
<span data-ttu-id="24268-p102">В контексте инфраструктурой соединителя Поиск внешнего типа контента источника ассоциации называется родительский тип внешнего контента. Программа-обходчик Поиск может выполнять обход внешних типов контента, связанные с родительской двумя способами: как вложения или дочерние элементы. Эти связей между типами внешнего контента повлиять на следующее:</span><span class="sxs-lookup"><span data-stu-id="24268-p102">In the context of the Search connector framework, the source external content type of an association is referred to as the parent external content type. The Search crawler can crawl external content types that are associated with the parent in two ways: as attachments or as children. These external content type associations affect the following:</span></span>
  
    
    

- <span data-ttu-id="24268-113">Взаимодействие с пользователем</span><span class="sxs-lookup"><span data-stu-id="24268-113">User experience</span></span>
    
  
- <span data-ttu-id="24268-114">Добавочные обходы контента</span><span class="sxs-lookup"><span data-stu-id="24268-114">Incremental crawls</span></span>
    
  
- <span data-ttu-id="24268-115">Обработка удалений обхода контента</span><span class="sxs-lookup"><span data-stu-id="24268-115">Processing crawl deletions</span></span>
    
  

### <a name="user-experience-effects-from-external-content-type-associations"></a><span data-ttu-id="24268-116">Влияние связей внешнего типа контента на взаимодействие с пользователем</span><span class="sxs-lookup"><span data-stu-id="24268-116">User experience effects from external content type associations</span></span>

<span data-ttu-id="24268-p103">Дочерний внешний тип контента имеет собственный URL-адрес страницы результатов поиска и страницу профиля (если она создана). URL-адрес страницы результатов поиска  это URL-адрес, который отображается, если пользователь выполняет поиск термина в данных дочернего внешнего типа контента.</span><span class="sxs-lookup"><span data-stu-id="24268-p103">A child external content type has its own search result URL and profile page, if the profile page has been created. The search result URL is the URL that is displayed if the user searches for a term in the child external content type data.</span></span> 
  
    
    
<span data-ttu-id="24268-p104">Внешний тип контента для вложения не имеет собственного URL-адреса страницы результатов поиска. Поэтому, если пользователь выполняет поиск термина во внешнем элементе вложения, отображается URL-адрес родительского внешнего типа контента. Этот URL-адрес можно задать для URL-адреса страницы профиля родительского типа. Страница профиля родительского внешнего типа контента будет отображать все поля из внешнего типа контента вложения, предоставленные навигатором связей.</span><span class="sxs-lookup"><span data-stu-id="24268-p104">The external content type for an attachment does not have its own search result URL. So if the user searches for a term in the attachment external item, the URL for the parent external content type is displayed instead. You can set this URL to the profile page URL of the parent. The profile page for the parent external content type will display all the fields from the attachment external content type that are exposed by the association navigator.</span></span>
  
    
    

### <a name="incremental-crawl-effects-from-external-content-type-associations"></a><span data-ttu-id="24268-123">Влияние связей внешнего типа контента на добавочный обход контента</span><span class="sxs-lookup"><span data-stu-id="24268-123">Incremental crawl effects from external content type associations</span></span>

<span data-ttu-id="24268-124">Дочерних внешних элементов повторный обход и обновляются на основе временных меток добавочных обходов, при изменении отметки времени родительского внешнего элемента.</span><span class="sxs-lookup"><span data-stu-id="24268-124">Child external items are re-crawled and updated for timestamp-based incremental crawls if the timestamp of the child external item changes.</span></span> 
  
    
    
<span data-ttu-id="24268-p105">Для внешних типов контента вложения отметка времени родительского внешнего элемента интерпретируется как отметка времени внешнего элемента вложения. Это значит, что изменения во внешнем элементе вложения собираются добавочным обходом контента только при изменении отметки времени родительского внешнего элемента.</span><span class="sxs-lookup"><span data-stu-id="24268-p105">For attachment external content types, the timestamp of the parent external item is interpreted as the timestamp of the attachment external item. This means that any changes in the attachment external item are picked up by an incremental crawl only when the timestamp of the parent external item changes.</span></span>
  
    
    

### <a name="processing-crawl-deletions-effects-from-external-content-type-associations"></a><span data-ttu-id="24268-127">Влияние связей внешнего типа контента на обработку удалений обхода контента</span><span class="sxs-lookup"><span data-stu-id="24268-127">Processing crawl deletions effects from external content type associations</span></span>

<span data-ttu-id="24268-128">При обработке удалений обхода контента, если родительский тип внешнего контента удаляется из индекса, программа-обходчик Поиск удаляет вложения связанных внешних типов контента и дочерние внешние типы контента из индекса.</span><span class="sxs-lookup"><span data-stu-id="24268-128">When processing crawl deletions, if the parent external content type is deleted from the index, the Search crawler deletes the associated attachment external content types and child external content types from the index.</span></span>
  
    
    

## <a name="crawling-associated-external-content-type-attachments"></a><span data-ttu-id="24268-129">Обход вложений связанного внешнего типа контента</span><span class="sxs-lookup"><span data-stu-id="24268-129">Crawling associated external content type attachments</span></span>
<span data-ttu-id="24268-130"><a name="HowToCrawlAssociations_CrawlingAttachments"> </a></span><span class="sxs-lookup"><span data-stu-id="24268-130"></span></span>

<span data-ttu-id="24268-131">Чтобы отметить связь для обхода в качестве вложения, добавьте свойство **AttachmentAccessor** в экземпляр метода **Association**, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="24268-131">To mark an association so that it is crawled as an attachment, add the **AttachmentAccessor** property to the **Association** method instance, as follows.</span></span>
  
    
    

```XML

<Association Name="AttachmentsNavigate Association" Type="AssociationNavigator" ...>
    <Properties>
        <Property Name="ForeignFieldMappings" Type="System.String">....... </Property>
        <Property Name="AttachmentAccessor" Type="System.String">x</Property>
    </Properties>
    <SourceEntity Namespace="ParentExternalContentType" Name="Parent" />
    <DestinationEntity Namespace="AttachmentExternalContentType" Name="Attachment External Content Type" />
</Association>
```


> <span data-ttu-id="24268-132">**Примечание:** Можно задать любое значение для свойства **AttachmentAccessor** ; Поиск не проверяет это значение.</span><span class="sxs-lookup"><span data-stu-id="24268-132">**Note:** You can specify any value for the **AttachmentAccessor** property; Search does not examine this value.</span></span>
  
    
    


## <a name="crawling-associated-external-content-types-as-child-external-content-types"></a><span data-ttu-id="24268-133">Обход связанных внешних типов контента в качестве дочерних внешних типов контента</span><span class="sxs-lookup"><span data-stu-id="24268-133">Crawling associated external content types as child external content types</span></span>
<span data-ttu-id="24268-134"><a name="HowToCrawlAssociations_CrawlingChildExternalTypes"> </a></span><span class="sxs-lookup"><span data-stu-id="24268-134"></span></span>

<span data-ttu-id="24268-135">Чтобы отметить связь для обхода в качестве дочернего внешнего типа контента, добавьте свойство **DirectoryLink** в экземпляр метода **Association**, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="24268-135">To mark an association so that it is crawled as a child external content type, add the **DirectoryLink** property to the **Association** method instance, as follows.</span></span>
  
    
    

```XML

<Association Name="ChildrenNavigator Association" Type="AssociationNavigator" ...>
    <Properties>
        <Property Name="DirectoryLink" Type="System.String">x</Property>
    </Properties>
    <SourceEntity Namespace="ParentExternalContentType" Name="Parent" />
    <DestinationEntity Namespace="ChildExternalContentType" Name="Child External Content Type" />
</Association>
```


> <span data-ttu-id="24268-136">**Примечание:** Можно задать любое значение для свойства **DirectoryLink** .</span><span class="sxs-lookup"><span data-stu-id="24268-136">**Note:** You can specify any value for the **DirectoryLink** property.</span></span> <span data-ttu-id="24268-137">Поиск не проверяет это значение.</span><span class="sxs-lookup"><span data-stu-id="24268-137">Search does not examine this value.</span></span>
  
    
    


## <a name="additional-resources"></a><span data-ttu-id="24268-138">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="24268-138">Additional resources</span></span>
<span data-ttu-id="24268-139"><a name="SP15crawlects_addlresources"> </a></span><span class="sxs-lookup"><span data-stu-id="24268-139"></span></span>


-  [<span data-ttu-id="24268-140">Инфраструктура соединителей поиска в SharePoint</span><span class="sxs-lookup"><span data-stu-id="24268-140">Search connector framework in SharePoint</span></span>](search-connector-framework-in-sharepoint.md)
    
  
-  [<span data-ttu-id="24268-141">Добавление связей между внешними типами контента</span><span class="sxs-lookup"><span data-stu-id="24268-141">Adding Associations Between External Content Types</span></span>](http://msdn.microsoft.com/library/791e95ab-9b3c-413b-be12-bd0e59962c93%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="24268-142">Элемент Association в элементе MethodInstances (схемы BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="24268-142">Association Element in MethodInstances (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/9659a1f5-1b12-03ef-f9e3-5c9904cc5dd0%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="24268-143">Step 4 (Optional): Define Associations</span><span class="sxs-lookup"><span data-stu-id="24268-143">Step 4 (Optional): Define Associations</span></span>](http://msdn.microsoft.com/library/6bc55f46-459a-4986-8744-8c6c5f45097b%28Office.15%29.aspx)
    
  

