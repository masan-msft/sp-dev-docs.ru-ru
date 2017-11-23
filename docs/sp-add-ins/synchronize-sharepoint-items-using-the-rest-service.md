---
title: "Синхронизация элементов SharePoint с помощью службы REST"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: cfb67d048bc2b79aa724a6a3d2861327fd51fed3
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="synchronize-sharepoint-items-using-the-rest-service"></a><span data-ttu-id="bc52a-102">Синхронизация элементов SharePoint с помощью службы REST</span><span class="sxs-lookup"><span data-stu-id="bc52a-102">Synchronize SharePoint items using the REST service</span></span>
<span data-ttu-id="bc52a-103">Узнайте, как синхронизировать элементы между SharePoint и надстройками или службами с помощью ресурса **GetListItemChangesSinceToken**, входящего в состав службы REST в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="bc52a-103">Learn how to synchronize items between SharePoint and your add-ins or services by using the  **GetListItemChangesSinceToken** resource, part of the SharePoint REST service.</span></span>
 

 <span data-ttu-id="bc52a-p101">**Примечание.** В настоящее время идет процесс замены названия "приложения для SharePoint" названием "надстройки SharePoint". Во время этого процесса в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio может по-прежнему использоваться термин "приложения для SharePoint". Дополнительные сведения см. в статье [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="bc52a-p101">**Note**  The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see  [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span></span>
 


## <a name="synchronizing-sharepoint-items-using-the-getlistitemchangessincetoken-resource"></a><span data-ttu-id="bc52a-107">Синхронизация элементов SharePoint с помощью ресурса GetListItemChangesSinceToken</span><span class="sxs-lookup"><span data-stu-id="bc52a-107">Synchronizing SharePoint items using the GetListItemChangesSinceToken resource</span></span>

<span data-ttu-id="bc52a-p102">Синхронизировать элементы между SharePoint и надстройками или службами можно с помощью ресурса **GetListItemChangesSinceToken**. **GetListItemChangesSinceToken** — это элемент службы SharePoint REST, соответствующий вызову веб-службы **Lists.GetListItemChangesSinceToken**.</span><span class="sxs-lookup"><span data-stu-id="bc52a-p102">If you want to synchronize items between SharePoint and your add-ins or services, you can use the  **GetListItemChangesSinceToken** resource to do so. The **GetListItemChangesSinceToken**, part of the SharePoint REST service, corresponds to the  **Lists.GetListItemChangesSinceToken** web service call.</span></span>
 

 
<span data-ttu-id="bc52a-110">Выполните запрос **POST**, который содержит в тексте объект [Свойства объекта SP.ChangeLogItemQuery](#bk_props).</span><span class="sxs-lookup"><span data-stu-id="bc52a-110">Perform a  **POST** request that includes a [SP.ChangeLogItemQuery object properties](#bk_props) object in the request body.</span></span>
 

 
<span data-ttu-id="bc52a-p103">Запрос вернет XML-файл с **набором строк** ADO, которые соответствуют любым изменениям элементов списка, соответствующим указанному запросу. Дополнительные сведения об этих свойствах, в том числе структуры данных свойств, описание элементов CAML и возвращаемые значения, см. в разделе **Lists.GetListItemChangesSinceToken**.</span><span class="sxs-lookup"><span data-stu-id="bc52a-p103">The request returns ADO  **rowset** XML which includes rows corresponding to any list item change matching the specified query. For more information on these properties, including property data structures, CAML element descriptions, and return values, see **Lists.GetListItemChangesSinceToken**.</span></span>
 

 

||
|:-----|
|<span data-ttu-id="bc52a-113">**Пример запроса**</span><span class="sxs-lookup"><span data-stu-id="bc52a-113">**Example request**</span></span>|
| `POST http://server/site/_api/web/Lists/GetByTitle('Announcements')/GetListItemChangesSinceToken`|
|<span data-ttu-id="bc52a-114">**Пример текста запроса POST**</span><span class="sxs-lookup"><span data-stu-id="bc52a-114">**Example POST Body**</span></span>|
|
```XML
{ 'd' : { 
  'query': { 
    '__metadata': { 'type': 'SP.ChangeLogItemQuery'}, 
    'ViewName': '', 
    'Query': '<Where>
      <Contains>
         <FieldRef Name="Title" />
         <Value Type='Text'>Te</Value>
      </Contains></Where>',
    'QueryOptions': '<QueryOptions>
      <IncludeMandatoryColumns>FALSE</IncludeMandatoryColumns>
      <DateInUtc>False</DateInUtc>
      <IncludePermissions>TRUE</IncludePermissions>
      <IncludeAttachmentUrls>FALSE</IncludeAttachmentUrls>
      <Folder>Shared Documents/Test1</Folder></QueryOptions>', 
    'ChangeToken':'1;3;eee4c6d5-f88a-42c4-8ce1-685122984870;634397182229400000;3710', 
    'Contains':'<Contains>
      <FieldRef Name="Title"/>
      <Value Type="Text">Testing</Value></Contains>' } 
  } 
}

```

|

## <a name="spchangelogitemquery-object-properties"></a><span data-ttu-id="bc52a-115">Свойства объекта SP.ChangeLogItemQuery</span><span class="sxs-lookup"><span data-stu-id="bc52a-115">SP.ChangeLogItemQuery object properties</span></span>
<span data-ttu-id="bc52a-116"><a name="bk_props"> </a></span><span class="sxs-lookup"><span data-stu-id="bc52a-116"></span></span>


****


|<span data-ttu-id="bc52a-117">**Свойство**</span><span class="sxs-lookup"><span data-stu-id="bc52a-117">**Property**</span></span>|<span data-ttu-id="bc52a-118">**Описание**</span><span class="sxs-lookup"><span data-stu-id="bc52a-118">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="bc52a-119">**ListName**</span><span class="sxs-lookup"><span data-stu-id="bc52a-119">**ListName**</span></span>|<span data-ttu-id="bc52a-p104">Строка, которая содержит название или GUID для списка. При запросе таблицы UserInfo строка содержит UserInfo. Использование GUID приводит к повышению производительности.</span><span class="sxs-lookup"><span data-stu-id="bc52a-p104">A string that contains either the title or the GUID for the list. When querying the UserInfo table, the string contains UserInfo. Using the GUID results in better performance.</span></span>|
|<span data-ttu-id="bc52a-123">**ViewName**</span><span class="sxs-lookup"><span data-stu-id="bc52a-123">**ViewName**</span></span>|<span data-ttu-id="bc52a-p105">Строка, содержащая GUID представления, которое необходимо использовать для атрибутов по умолчанию, представленных параметрами _Query_, _viewFields_ и _rowLimit_. Если этот аргумент не указан, используется представление по умолчанию. Если указано, значение параметра _Query_, _viewFields_ или _rowLimit_ переопределяет соответствующее значение в представлении. Например, если в представлении, заданном с помощью параметра _viewFields_, установлено ограничение на количество строк 100, но параметр _rowLimit_ содержит значение 1000, то в ответе будет 1000 строк.</span><span class="sxs-lookup"><span data-stu-id="bc52a-p105">A string that contains the GUID for the view, which determines the view to use for the default view attributes represented by the  _query_,  _viewFields_, and  _rowLimit_ parameters. If this argument is not supplied, the default view is assumed. If it is supplied, the value of the _query_,  _viewFields_, or  _rowLimit_ parameter overrides the equivalent setting within the view. For example, if the view specified by the _viewFields_ parameter has a row limit of 100 rows but the _rowLimit_ parameter contains a value of 1000, then 1,000 rows are returned in the response.</span></span>|
|<span data-ttu-id="bc52a-128">**Query**</span><span class="sxs-lookup"><span data-stu-id="bc52a-128">**Query**</span></span>|<span data-ttu-id="bc52a-129">Элемент [Query](http://msdn.microsoft.com/ru-ru/library/ms471093.aspx), содержащий запрос, который определяет, какие записи возвращаются и в каком порядке.</span><span class="sxs-lookup"><span data-stu-id="bc52a-129">A  [Query](http://msdn.microsoft.com/ru-ru/library/ms471093.aspx) element containing the query that determines which records are returned and in what order.</span></span>|
|<span data-ttu-id="bc52a-130">**QueryOptions**</span><span class="sxs-lookup"><span data-stu-id="bc52a-130">**QueryOptions**</span></span>|<span data-ttu-id="bc52a-131">Фрагмент XML следующей формы, содержащий отдельные узлы для различных свойств объекта **SPQuery**.</span><span class="sxs-lookup"><span data-stu-id="bc52a-131">An XML fragment in the following form that contains separate nodes for the various properties of the  **SPQuery** object.</span></span>|
|<span data-ttu-id="bc52a-132">**ChangeToken**</span><span class="sxs-lookup"><span data-stu-id="bc52a-132">**ChangeToken**</span></span>|<span data-ttu-id="bc52a-p106">Строка, содержащая токен изменений для запроса. Описание формата этой строки см. в статье [Обзор журнала изменений](http://msdn.microsoft.com/ru-ru/library/bb417456.aspx). Если передается значение null, то возвращаются все элементы списка.</span><span class="sxs-lookup"><span data-stu-id="bc52a-p106">A string that contains the change token for the request. For a description of the format that is used in this string, see  [Overview of the Change Log](http://msdn.microsoft.com/ru-ru/library/bb417456.aspx). If null is passed, all items in the list are returned.</span></span>|
|<span data-ttu-id="bc52a-136">**Contains**</span><span class="sxs-lookup"><span data-stu-id="bc52a-136">**Contains**</span></span>|<span data-ttu-id="bc52a-137">Элемент [Contains](http://msdn.microsoft.com/ru-ru/library/ms196501.aspx), который определяет настройки фильтрации для запроса.</span><span class="sxs-lookup"><span data-stu-id="bc52a-137">A  [Contains](http://msdn.microsoft.com/ru-ru/library/ms196501.aspx) element that defines custom filtering for the query.</span></span>|

## <a name="additional-resources"></a><span data-ttu-id="bc52a-138">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="bc52a-138">Additional resources</span></span>
<span data-ttu-id="bc52a-139"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="bc52a-139"></span></span>


-  [<span data-ttu-id="bc52a-140">Знакомство со службой REST в SharePoint</span><span class="sxs-lookup"><span data-stu-id="bc52a-140">Get to know the SharePoint REST service</span></span>](get-to-know-the-sharepoint-rest-service.md)
    
 
-  [<span data-ttu-id="bc52a-141">Выполнение базовых операций с использованием конечных точек SharePoint REST</span><span class="sxs-lookup"><span data-stu-id="bc52a-141">Complete basic operations using SharePoint REST endpoints</span></span>](complete-basic-operations-using-sharepoint-rest-endpoints.md)
    
 
-  [<span data-ttu-id="bc52a-142">Работа со списками и элементами списков в интерфейсе REST</span><span class="sxs-lookup"><span data-stu-id="bc52a-142">Working with lists and list items with REST</span></span>](working-with-lists-and-list-items-with-rest.md)
    
 
-  [<span data-ttu-id="bc52a-143">Работа с папками и файлами в службе REST</span><span class="sxs-lookup"><span data-stu-id="bc52a-143">Working with folders and files with REST</span></span>](working-with-folders-and-files-with-rest.md)
    
 
-  [<span data-ttu-id="bc52a-144">Навигация по структуре данных SharePoint, представленной в службе REST</span><span class="sxs-lookup"><span data-stu-id="bc52a-144">Navigate the SharePoint data structure represented in the REST service</span></span>](navigate-the-sharepoint-data-structure-represented-in-the-rest-service.md)
    
 
-  [<span data-ttu-id="bc52a-145">Определение универсальных кодов ресурсов (URI) конечных точек службы SharePoint REST</span><span class="sxs-lookup"><span data-stu-id="bc52a-145">Determine SharePoint REST service endpoint URIs</span></span>](determine-sharepoint-rest-service-endpoint-uris.md)
    
 
-  [<span data-ttu-id="bc52a-146">Использование операций запросов OData в запросах REST SharePoint</span><span class="sxs-lookup"><span data-stu-id="bc52a-146">Use OData query operations in SharePoint REST requests</span></span>](use-odata-query-operations-in-sharepoint-rest-requests.md)
    
 
-  [<span data-ttu-id="bc52a-147">Справочные материалы по интерфейсу API службы REST и примеры</span><span class="sxs-lookup"><span data-stu-id="bc52a-147">REST API reference and samples</span></span>](http://msdn.microsoft.com/library/rest-api-reference-and-samples%28Office.15%29.aspx)
    
 
-  [<span data-ttu-id="bc52a-148">Получение версий списков документов с помощью значений ETag в службе REST</span><span class="sxs-lookup"><span data-stu-id="bc52a-148">Use ETag values through the REST service to get document list item versioning</span></span>](http://msdn.microsoft.com/library/5f7e0579-46b7-44ab-b3b4-cdbc622dcd98%28Office.15%29.aspx)
    
 

 

 

