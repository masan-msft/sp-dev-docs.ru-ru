---
title: "Синхронизация элементов SharePoint с помощью службы REST"
description: "Узнайте, как синхронизировать элементы между SharePoint и надстройками или службами с помощью ресурса GetListItemChangesSinceToken, входящего в состав службы REST в SharePoint."
ms.date: 12/14/2017
ms.prod: sharepoint
ms.openlocfilehash: 18386524bca492930001b457f065bac39dce7699
ms.sourcegitcommit: 4e65e89f3ad8ef1d953e2fdd04d7ab5c0e7df174
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/27/2018
---
# <a name="synchronize-sharepoint-items-using-the-rest-service"></a><span data-ttu-id="4e3fd-103">Синхронизация элементов SharePoint с помощью службы REST</span><span class="sxs-lookup"><span data-stu-id="4e3fd-103">Synchronize SharePoint items using the REST service</span></span>

<span data-ttu-id="4e3fd-104">Синхронизировать элементы между SharePoint и надстройками или службами можно с помощью ресурса **GetListItemChangesSinceToken**.</span><span class="sxs-lookup"><span data-stu-id="4e3fd-104">If you want to synchronize items between SharePoint and your add-ins or services, you can use the  **GetListItemChangesSinceToken** resource to do so. The GetListItemChangesSinceToken, part of the SharePoint REST service, corresponds to the  Lists.GetListItemChangesSinceToken web service call.</span></span> <span data-ttu-id="4e3fd-105">**GetListItemChangesSinceToken** — это элемент службы SharePoint REST, соответствующий вызову веб-службы **Lists.GetListItemChangesSinceToken**.</span><span class="sxs-lookup"><span data-stu-id="4e3fd-105">If you want to synchronize items between SharePoint and your add-ins or services, you can use the  **GetListItemChangesSinceToken** resource to do so. The GetListItemChangesSinceToken, part of the SharePoint REST service, corresponds to the  **Lists.GetListItemChangesSinceToken** web service call.</span></span>

<span data-ttu-id="4e3fd-106">Выполните запрос **POST**, тело которого содержит объект [Свойства объекта SP.ChangeLogItemQuery](#bk_props).</span><span class="sxs-lookup"><span data-stu-id="4e3fd-106">Perform a  **POST** request that includes a [SP.ChangeLogItemQuery object properties](#bk_props) object in the request body.</span></span>

<span data-ttu-id="4e3fd-107">Запрос вернет XML-файл с **набором строк** объектов ADO, которые соответствуют любым изменениям элементов списка, соответствующим указанному запросу.</span><span class="sxs-lookup"><span data-stu-id="4e3fd-107">The request returns ADO  **rowset** XML which includes rows corresponding to any list item change matching the specified query. For more information on these properties, including property data structures, CAML element descriptions, and return values, see Lists.GetListItemChangesSinceToken.</span></span> <span data-ttu-id="4e3fd-108">Дополнительные сведения об этих свойствах, в том числе сведения о возвращаемых значениях, структурах данных свойств и описание элементов CAML, см. в статье [Lists.GetListItemChangesSinceToken](https://msdn.microsoft.com/ru-RU/library/office/jj247029.aspx).</span><span class="sxs-lookup"><span data-stu-id="4e3fd-108">The request returns ADO  rowset XML which includes rows corresponding to any list item change matching the specified query. For more information on these properties, including property data structures, CAML element descriptions, and return values, see [Lists.GetListItemChangesSinceToken](https://msdn.microsoft.com/ru-RU/library/office/jj247029.aspx).</span></span>

### <a name="example"></a><span data-ttu-id="4e3fd-109">Пример</span><span class="sxs-lookup"><span data-stu-id="4e3fd-109">Example</span></span>

<span data-ttu-id="4e3fd-110">**Пример запроса**</span><span class="sxs-lookup"><span data-stu-id="4e3fd-110">**Example request**</span></span>

`POST http://server/site/_api/web/Lists/GetByTitle('Announcements')/GetListItemChangesSinceToken`

<span data-ttu-id="4e3fd-111">**Пример тела запроса POST**</span><span class="sxs-lookup"><span data-stu-id="4e3fd-111">**Example POST Body**</span></span>

```XML
{ 'd' : { 
  'query': { 
    '__metadata': { 'type': 'SP.ChangeLogItemQuery'}, 
    'ViewName': '', 
    'Query': '
      <Query>
      <Where>
      <Contains>
         <FieldRef Name="Title" />
         <Value Type='Text'>Te</Value>
      </Contains></Where>'</Query>,
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

<br/>

<span data-ttu-id="4e3fd-112"><a name="bk_props"> </a></span><span class="sxs-lookup"><span data-stu-id="4e3fd-112"></span></span>

## <a name="spchangelogitemquery-object-properties"></a><span data-ttu-id="4e3fd-113">Свойства объекта SP.ChangeLogItemQuery</span><span class="sxs-lookup"><span data-stu-id="4e3fd-113">SP.ChangeLogItemQuery object properties</span></span>

|<span data-ttu-id="4e3fd-114">**Свойство**</span><span class="sxs-lookup"><span data-stu-id="4e3fd-114">**Property**</span></span>|<span data-ttu-id="4e3fd-115">**Описание**</span><span class="sxs-lookup"><span data-stu-id="4e3fd-115">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="4e3fd-116">**ListName**</span><span class="sxs-lookup"><span data-stu-id="4e3fd-116">**ListName**</span></span>|<span data-ttu-id="4e3fd-p103">Строка, которая содержит название или GUID для списка. При запросе таблицы UserInfo строка содержит UserInfo. Использование GUID приводит к повышению производительности.</span><span class="sxs-lookup"><span data-stu-id="4e3fd-p103">A string that contains either the title or the GUID for the list. When querying the UserInfo table, the string contains UserInfo. Using the GUID results in better performance.</span></span>|
|<span data-ttu-id="4e3fd-120">**ViewName**</span><span class="sxs-lookup"><span data-stu-id="4e3fd-120">**ViewName**</span></span>|<span data-ttu-id="4e3fd-p104">Строка, содержащая GUID представления, которое необходимо использовать для атрибутов по умолчанию, представленных параметрами _query_, _viewFields_ и _rowLimit_. Если этот аргумент не указан, используется представление по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="4e3fd-p104">A string that contains the GUID for the view, which determines the view to use for the default view attributes represented by the  _query_,  _viewFields_, and  _rowLimit_ parameters. If this argument is not supplied, the default view is assumed. If it is supplied, the value of the query,  viewFields, or  rowLimit parameter overrides the equivalent setting within the view. For example, if the view specified by the viewFields parameter has a row limit of 100 rows but the rowLimit parameter contains a value of 1000, then 1,000 rows are returned in the response.</span></span><br/><br/><span data-ttu-id="4e3fd-123">Если же он указан, значение параметра _query_, _viewFields_ или _rowLimit_ переопределяет соответствующее значение в представлении.</span><span class="sxs-lookup"><span data-stu-id="4e3fd-123">If it is supplied, the value of the _query_,  _viewFields_, or _rowLimit_ parameter overrides the equivalent setting within the view.</span></span><br/><br/><span data-ttu-id="4e3fd-124">Например, если в представлении, заданном с помощью параметра _viewFields_, установлено ограничение на количество строк 100, но параметр _rowLimit_ содержит значение 1000, то в ответе будет 1000 строк.</span><span class="sxs-lookup"><span data-stu-id="4e3fd-124">For example, if the view specified by the _viewFields_ parameter has a row limit of 100 rows, but the _rowLimit_ parameter contains a value of 1000, then 1,000 rows are returned in the response.</span></span>|
|<span data-ttu-id="4e3fd-125">**Query**</span><span class="sxs-lookup"><span data-stu-id="4e3fd-125">**Query**</span></span>|<span data-ttu-id="4e3fd-126">Элемент [Query](http://msdn.microsoft.com/ru-RU/library/ms471093.aspx), содержащий запрос, который определяет, какие записи возвращаются и в каком порядке.</span><span class="sxs-lookup"><span data-stu-id="4e3fd-126">A  [Query](http://msdn.microsoft.com/ru-RU/library/ms471093.aspx) element containing the query that determines which records are returned and in what order.</span></span>|
|<span data-ttu-id="4e3fd-127">**QueryOptions**</span><span class="sxs-lookup"><span data-stu-id="4e3fd-127">**QueryOptions**</span></span>|<span data-ttu-id="4e3fd-128">Фрагмент XML следующей формы, содержащий отдельные узлы для различных свойств объекта **SPQuery**:</span><span class="sxs-lookup"><span data-stu-id="4e3fd-128">An XML fragment in the following form that contains separate nodes for the various properties of the  **SPQuery** object.</span></span>|
|<span data-ttu-id="4e3fd-129">**ChangeToken**</span><span class="sxs-lookup"><span data-stu-id="4e3fd-129">**ChangeToken**</span></span>|<span data-ttu-id="4e3fd-130">Строка, содержащая токен изменений для запроса.</span><span class="sxs-lookup"><span data-stu-id="4e3fd-130">A string that contains the change token for the request.</span></span><br/><br/><span data-ttu-id="4e3fd-131">Описание формата этой строки см. в статье [Обзор журнала изменений](http://msdn.microsoft.com/ru-RU/library/bb417456.aspx).</span><span class="sxs-lookup"><span data-stu-id="4e3fd-131">A string that contains the change token for the request. For a description of the format that is used in this string, see  [Overview of the Change Log](http://msdn.microsoft.com/ru-RU/library/bb417456.aspx). If null is passed, all items in the list are returned.</span></span> <span data-ttu-id="4e3fd-132">Если передается значение NULL, то возвращаются все элементы списка.</span><span class="sxs-lookup"><span data-stu-id="4e3fd-132">If null is passed, all items in the list are returned.</span></span>|
|<span data-ttu-id="4e3fd-133">**Contains**</span><span class="sxs-lookup"><span data-stu-id="4e3fd-133">**Contains**</span></span>|<span data-ttu-id="4e3fd-134">Элемент [Contains](http://msdn.microsoft.com/ru-RU/library/ms196501.aspx), который определяет настройки фильтрации для запроса.</span><span class="sxs-lookup"><span data-stu-id="4e3fd-134">A  [Contains](http://msdn.microsoft.com/ru-RU/library/ms196501.aspx) element that defines custom filtering for the query.</span></span>|

## <a name="see-also"></a><span data-ttu-id="4e3fd-135">См. также</span><span class="sxs-lookup"><span data-stu-id="4e3fd-135">See also</span></span>
<span data-ttu-id="4e3fd-136"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="4e3fd-136"><a name="bk_addresources"> </a></span></span>

- [<span data-ttu-id="4e3fd-137">Знакомство со службой REST в SharePoint</span><span class="sxs-lookup"><span data-stu-id="4e3fd-137">Get to know the SharePoint REST service</span></span>](get-to-know-the-sharepoint-rest-service.md)
- [<span data-ttu-id="4e3fd-138">Получение версий списков документов с помощью значений ETag в службе REST</span><span class="sxs-lookup"><span data-stu-id="4e3fd-138">Use ETag values through the REST service to get document list item versioning</span></span>](working-with-lists-and-list-items-with-rest.md#using-etag-values-to-determine-document-and-list-item-versioning)
- [<span data-ttu-id="4e3fd-139">Справочные материалы по REST API и примеры</span><span class="sxs-lookup"><span data-stu-id="4e3fd-139">REST API reference and samples</span></span>](https://msdn.microsoft.com/library)
- [<span data-ttu-id="4e3fd-140">Материалы по OData</span><span class="sxs-lookup"><span data-stu-id="4e3fd-140">OData resources</span></span>](get-to-know-the-sharepoint-rest-service.md#odata-resources)
- [<span data-ttu-id="4e3fd-141">Разработка надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="4e3fd-141">Develop SharePoint Add-ins</span></span>](develop-sharepoint-add-ins.md)

    
 

 

 

