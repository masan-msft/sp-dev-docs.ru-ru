---
title: "Общие сведения об API службы поиска REST для SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: d0684be67a04f79cea059564390918be084d9eaf
ms.sourcegitcommit: d68d6cf927d69696a3561f7d8ffe9a3ed9dbd03c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/18/2017
---
# <a name="sharepoint-search-rest-api-overview"></a><span data-ttu-id="c4c0c-102">Общие сведения об API REST для службы поиска SharePoint</span><span class="sxs-lookup"><span data-stu-id="c4c0c-102">SharePoint Search REST API overview</span></span>
<span data-ttu-id="c4c0c-103">Добавление функций поиска в клиентские и мобильные приложения с помощью службы поиска REST в SharePoint и любой технологии, поддерживающей веб-запросы REST.</span><span class="sxs-lookup"><span data-stu-id="c4c0c-103">Add search functionality to client and mobile applications using the Search REST service in SharePoint Server 2013 and any technology that supports REST web requests.</span></span>
## <a name="querying-with-the-search-rest-service"></a><span data-ttu-id="c4c0c-104">Отправка запросов с помощью службы поиска REST</span><span class="sxs-lookup"><span data-stu-id="c4c0c-104">Querying with the Search REST service</span></span>
<span data-ttu-id="c4c0c-105"><a name="bk_queryrest"> </a></span><span class="sxs-lookup"><span data-stu-id="c4c0c-105"></span></span>

<span data-ttu-id="c4c0c-p101">Поиск в SharePoint включает службу поиска REST, которую вы можете использовать для добавления функции поиска в свои клиентские или мобильные приложения с помощью любой технологии, поддерживающей веб-запросы REST. Вы можете использовать службу поиска REST для отправки запросов на языке запросов по ключевым словам (KQL) или на языке FAST-запросов (FQL) в своих Надстройки SharePoint, удаленных клиентских приложениях, мобильных и других приложениях.</span><span class="sxs-lookup"><span data-stu-id="c4c0c-p101">Search in SharePoint includes a Search REST service you can use to add search functionality to your client and mobile applications by using any technology that supports REST web requests. You can use the Search REST service to submit Keyword Query Language (KQL) or FAST Query Language (FQL) queries in your SharePoint Add-ins, remote client applications, mobile applications, and other applications.</span></span>
  
    
    
<span data-ttu-id="c4c0c-108">Служба поиска REST поддерживает HTTP-запросы **POST** и **GET**.</span><span class="sxs-lookup"><span data-stu-id="c4c0c-108">The Search REST service supports both HTTP **POST** and HTTP **GET** requests.</span></span>
  
    
    

### <a name="get-requests"></a><span data-ttu-id="c4c0c-109">Запросы GET</span><span class="sxs-lookup"><span data-stu-id="c4c0c-109">GET requests</span></span>

<span data-ttu-id="c4c0c-110">Создайте URI, чтобы отправлять службе поиска REST запросы **GET**:</span><span class="sxs-lookup"><span data-stu-id="c4c0c-110">Construct the URI for query **GET** requests to the Search REST service as follows:</span></span>
  
    
    
 `/_api/search/query`
  
    
    
<span data-ttu-id="c4c0c-p102">Укажите параметры запроса для запросов **GET** в URL-адресе. Вы можете создать URL-адрес запроса **GET** двумя способами:</span><span class="sxs-lookup"><span data-stu-id="c4c0c-p102">For **GET** requests, you specify the query parameters in the URL. You can construct the **GET** request URL in two ways:</span></span>
  
    
    


  
    
    
>  `http://server/_api/search/query?query_parameter=value&amp;query_parameter=value`
    
  

  
    
    
>  `http://server/_api/search/query(query_parameter=value&amp;query_parameter=<value>)`
    
  

### <a name="post-requests"></a><span data-ttu-id="c4c0c-113">Запросы POST</span><span class="sxs-lookup"><span data-stu-id="c4c0c-113">POST requests</span></span>

<span data-ttu-id="c4c0c-114">Создайте URI, чтобы отправлять службе поиска REST запросы **POST**:</span><span class="sxs-lookup"><span data-stu-id="c4c0c-114">You construct the URI for query **POST** requests to the Search REST service as follows:</span></span>
  
    
    
 `/_api/search/postquery`
  
    
    
<span data-ttu-id="c4c0c-115">Для запросов **POST** передайте параметры запроса в запросе в формате Нотация объектов JavaScript (JSON).</span><span class="sxs-lookup"><span data-stu-id="c4c0c-115">For **POST** requests, you pass the query parameters in the request in JavaScript Object Notation (JSON) format.</span></span>
  
    
    
<span data-ttu-id="c4c0c-p103">HTTP-версия **POST** службы поиска REST поддерживает все параметры, поддерживаемые версией **GET**. Однако некоторые параметры имеют различные типы данных, как это описано в таблице 1.</span><span class="sxs-lookup"><span data-stu-id="c4c0c-p103">The HTTP **POST** version of the Search REST service supports all parameters supported by the HTTP **GET** version. However, some of the parameters have different data types, as described in Table 1.</span></span>
  
    
    

<span data-ttu-id="c4c0c-118">**Таблица 1. Параметры запроса с различными типами данных для запросов POST**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-118">**Table 1. Query parameters with different data types for POST requests**</span></span>


|<span data-ttu-id="c4c0c-119">**Параметр**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-119">**Parameter**</span></span>|<span data-ttu-id="c4c0c-120">**Тип данных**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-120">**Data type**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="c4c0c-121">SelectProperties</span><span class="sxs-lookup"><span data-stu-id="c4c0c-121">SelectProperties</span></span>](#bk_SelectProperties) <br/> |<span data-ttu-id="c4c0c-122">строка[]</span><span class="sxs-lookup"><span data-stu-id="c4c0c-122">string[]</span></span>  <br/> |
| [<span data-ttu-id="c4c0c-123">RefinementFilters</span><span class="sxs-lookup"><span data-stu-id="c4c0c-123">RefinementFilters</span></span>](#bk_RefinementFilters) <br/> |<span data-ttu-id="c4c0c-124">строка[]</span><span class="sxs-lookup"><span data-stu-id="c4c0c-124">string[]</span></span>  <br/> |
| [<span data-ttu-id="c4c0c-125">SortList</span><span class="sxs-lookup"><span data-stu-id="c4c0c-125">SortList</span></span>](#bk_SortList) <br/> | [<span data-ttu-id="c4c0c-126">Sort</span><span class="sxs-lookup"><span data-stu-id="c4c0c-126">Sort</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Search.Query.Sort.aspx) <br/> |
| [<span data-ttu-id="c4c0c-127">HithighlightedProperties</span><span class="sxs-lookup"><span data-stu-id="c4c0c-127">HithighlightedProperties</span></span>](#bk_HithighlightedProperties) <br/> |<span data-ttu-id="c4c0c-128">строка[]</span><span class="sxs-lookup"><span data-stu-id="c4c0c-128">string[]</span></span>  <br/> |
| [<span data-ttu-id="c4c0c-129">Properties</span><span class="sxs-lookup"><span data-stu-id="c4c0c-129">Properties</span></span>](#bk_Properties) <br/> | [<span data-ttu-id="c4c0c-130">Microsoft.SharePoint.Client.Search.Query.KeywordQueryProperties</span><span class="sxs-lookup"><span data-stu-id="c4c0c-130">Microsoft.SharePoint.Client.Search.Query.KeywordQueryProperties</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Search.Query.KeywordQueryProperties.aspx) <br/> |
   
<span data-ttu-id="c4c0c-131">Используйте запросы **POST** в следующих случаях:</span><span class="sxs-lookup"><span data-stu-id="c4c0c-131">Use **POST** requests in the following scenarios:</span></span>
  
    
    

- <span data-ttu-id="c4c0c-132">Если вы превысите ограничение длины URL-адреса с помощью запроса **GET**.</span><span class="sxs-lookup"><span data-stu-id="c4c0c-132">When you'll exceed the URL length restriction with a **GET** request.</span></span>
    
  
- <span data-ttu-id="c4c0c-p104">Если вы не можете указать параметры запроса в простом URL-адресе. Например, если вам нужно передать значения параметров, которые содержат массив сложных типов или строки с разделителем-запятой, запрос **POST** предоставит вам более широкие возможности.</span><span class="sxs-lookup"><span data-stu-id="c4c0c-p104">When you can't specify the query parameters in a simple URL. For example, if you have to pass parameter values that contain a complex type array, or comma-separated strings, you have more flexibility when constructing the **POST** request.</span></span>
    
  
- <span data-ttu-id="c4c0c-135">Если вы используете параметр  [ReorderingRules](#bk_ReorderingRules), так как он поддерживается только с помощью запросов **POST**.</span><span class="sxs-lookup"><span data-stu-id="c4c0c-135">When you use the  [ReorderingRules](#bk_ReorderingRules) parameter because it is supported only with **POST** requests.</span></span>
    
  

## <a name="using-query-parameters-with-the-search-rest-service"></a><span data-ttu-id="c4c0c-136">Использование параметров запроса с помощью службы поиска REST</span><span class="sxs-lookup"><span data-stu-id="c4c0c-136">Using query parameters with the Search REST service</span></span>
<span data-ttu-id="c4c0c-137"><a name="bk_UsingQueryParams"> </a></span><span class="sxs-lookup"><span data-stu-id="c4c0c-137"></span></span>

<span data-ttu-id="c4c0c-p105">При вызове службы поиска REST вы указываете параметры запроса вместе с самим запросом. Поиск в SharePoint использует эти параметры для создания запроса поиска. Для запроса **GET** укажите параметры запроса в URL-адресе, для запросов **POST** передайте их в теле в формате Нотация объектов JavaScript (JSON).</span><span class="sxs-lookup"><span data-stu-id="c4c0c-p105">When you make a call to the Search REST service, you specify query parameters with the request. Search in SharePoint uses these query parameters to construct the search query. With a **GET** request, you specify the query parameters in the URL. For **POST** requests, you pass the query parameters in the body in JavaScript Object Notation (JSON) format.</span></span>
  
    
    
<span data-ttu-id="c4c0c-142">В следующих разделах описаны параметры запроса, которые можно использовать для отправки запросов поиска с помощью службы поиска REST.</span><span class="sxs-lookup"><span data-stu-id="c4c0c-142">The following sections describe the query parameters you can use to submit search queries with the Search REST service.</span></span>
  
    
    

### <a name="querytext-parameter"></a><span data-ttu-id="c4c0c-143">Параметр QueryText</span><span class="sxs-lookup"><span data-stu-id="c4c0c-143">QueryText parameter</span></span>

<span data-ttu-id="c4c0c-144">Строка, содержащая текст для запроса поиска.</span><span class="sxs-lookup"><span data-stu-id="c4c0c-144">A string that contains the text for the search query.</span></span>
  
    
    
 <span data-ttu-id="c4c0c-145">**Пример запроса GET**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-145">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="c4c0c-146">http:// _server_/_api/search/query?querytext='sharepoint'</span><span class="sxs-lookup"><span data-stu-id="c4c0c-146">http:// _server_/_api/search/query?querytext='sharepoint'</span></span>
  
    
    
 <span data-ttu-id="c4c0c-147">**Пример запроса POST**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-147">**Sample POST request**</span></span>

```JSON
{
    'request': {
         'Querytext': 'sharepoint',
         'RowLimit':20, 
         'ClientType':'ContentSearchRegular'
         }
}
```


### <a name="querytemplate"></a><span data-ttu-id="c4c0c-148">QueryTemplate</span><span class="sxs-lookup"><span data-stu-id="c4c0c-148">QueryTemplate</span></span>
<span data-ttu-id="c4c0c-149"><a name="bk_QueryTemplate"> </a></span><span class="sxs-lookup"><span data-stu-id="c4c0c-149"></span></span>

<span data-ttu-id="c4c0c-150">Строка, содержащая текст, который замещает текст запроса в ходе преобразования запроса.</span><span class="sxs-lookup"><span data-stu-id="c4c0c-150">A string that contains the text that replaces the query text, as part of a query transform.</span></span>
  
    
    
 <span data-ttu-id="c4c0c-151">**Пример запроса GET**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-151">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="c4c0c-152">http://server/_api/search/query?querytext='sharepoint'&amp;querytemplate='{searchterms} author:johndoe'</span><span class="sxs-lookup"><span data-stu-id="c4c0c-152">http://server/_api/search/query?querytext='sharepoint'&amp;querytemplate='{searchterms} author:johndoe'</span></span>
  
    
    
 <span data-ttu-id="c4c0c-153">**Пример запроса POST**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-153">**Sample POST request**</span></span>
  
    
    



```

{
'__metadata' : {'type' : 'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
'Querytemplate' : '{searchterms} Author:johndoe'
}
```


### <a name="enableinterleaving"></a><span data-ttu-id="c4c0c-154">EnableInterleaving</span><span class="sxs-lookup"><span data-stu-id="c4c0c-154">EnableInterleaving</span></span>
<span data-ttu-id="c4c0c-155"><a name="bk_EnableInterleaving"> </a></span><span class="sxs-lookup"><span data-stu-id="c4c0c-155"></span></span>

<span data-ttu-id="c4c0c-156">Логическое значение, которое указывает смешаны ли таблицы результатов, возвращенных для блока результатов, с таблицами результатов, возвращенных для исходного запроса.</span><span class="sxs-lookup"><span data-stu-id="c4c0c-156">A Boolean value that specifies whether the result tables that are returned for the result block are mixed with the result tables that are returned for the original query.</span></span> 
  
    
    
 <span data-ttu-id="c4c0c-p106">Значение **true**, чтобы связать ResultTables; иначе  **false**. Значение по умолчанию  **true**.</span><span class="sxs-lookup"><span data-stu-id="c4c0c-p106">**true** to mix the ResultTables; otherwise, **false**. The default value is **true**.</span></span> 
  
    
    
<span data-ttu-id="c4c0c-159">Изменяйте это значение только в том случае, если вы хотите предоставить собственное чередующееся выполнение.</span><span class="sxs-lookup"><span data-stu-id="c4c0c-159">Change this value only if you want to provide your own interleaving implementation.</span></span>
  
    
    
 <span data-ttu-id="c4c0c-160">**Пример запроса GET**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-160">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="c4c0c-161">http:// _server_/_api/search/query?querytext='sharepoint'&amp;enableinterleaving=true</span><span class="sxs-lookup"><span data-stu-id="c4c0c-161">http:// _server_/_api/search/query?querytext='sharepoint'&amp;enableinterleaving=true</span></span>
  
    
    
 <span data-ttu-id="c4c0c-162">**Пример запроса POST**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-162">**Sample POST request**</span></span>
  
    
    



```

{
'__metadata' : {'type' : 'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
'EnableInterleaving' : 'True'
}
```


### <a name="sourceid"></a><span data-ttu-id="c4c0c-163">SourceId</span><span class="sxs-lookup"><span data-stu-id="c4c0c-163">SourceId</span></span>
<span data-ttu-id="c4c0c-164"><a name="bk_SourceId"> </a></span><span class="sxs-lookup"><span data-stu-id="c4c0c-164"></span></span>

<span data-ttu-id="c4c0c-165">Идентификатор источника результатов, использующийся для выполнения запроса поиска.</span><span class="sxs-lookup"><span data-stu-id="c4c0c-165">The result source ID to use for executing the search query.</span></span>
  
    
    
 <span data-ttu-id="c4c0c-166">**Пример запроса GET**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-166">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="c4c0c-167">http:// _server_/_api/search/query?querytext='sharepoint'&amp;sourceid='8413cd39-2156-4e00-b54d-11efd9abdb89'</span><span class="sxs-lookup"><span data-stu-id="c4c0c-167">http:// _server_/_api/search/query?querytext='sharepoint'&amp;sourceid='8413cd39-2156-4e00-b54d-11efd9abdb89'</span></span>
  
    
    
 <span data-ttu-id="c4c0c-168">**Пример запроса POST**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-168">**Sample POST request**</span></span>
  
    
    



```

{
'__metadata' : {'type' : 'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
'SourceId' : '8413cd39-2156-4e00-b54d-11efd9abdb89'
}
```


### <a name="rankingmodelid"></a><span data-ttu-id="c4c0c-169">RankingModelId</span><span class="sxs-lookup"><span data-stu-id="c4c0c-169">RankingModelId</span></span>
<span data-ttu-id="c4c0c-170"><a name="bk_RankingModelId"> </a></span><span class="sxs-lookup"><span data-stu-id="c4c0c-170"></span></span>

<span data-ttu-id="c4c0c-171">Идентификатор модели ранжирования для запроса.</span><span class="sxs-lookup"><span data-stu-id="c4c0c-171">The ID of the ranking model to use for the query.</span></span>
  
    
    
 <span data-ttu-id="c4c0c-172">**Пример запроса GET**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-172">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="c4c0c-173">http:// _server_/_api/search/query?querytext='sharepoint'&amp;rankingmodelid= _CustomRankingModelID_</span><span class="sxs-lookup"><span data-stu-id="c4c0c-173">http:// _server_/_api/search/query?querytext='sharepoint'&amp;rankingmodelid= _CustomRankingModelID_</span></span>
  
    
    
 <span data-ttu-id="c4c0c-174">**Пример запроса POST**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-174">**Sample POST request**</span></span>
  
    
    



```

{
'__metadata' : {'type' : 'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
'RankingModelId' : 'CustomRankingModelID '
}
```


### <a name="startrow"></a><span data-ttu-id="c4c0c-175">StartRow</span><span class="sxs-lookup"><span data-stu-id="c4c0c-175">StartRow</span></span>
<span data-ttu-id="c4c0c-176"><a name="bk_StartRow"> </a></span><span class="sxs-lookup"><span data-stu-id="c4c0c-176"></span></span>

<span data-ttu-id="c4c0c-p107">Первая строка, включаемая в возвращаемые результаты поиска. Используйте этот параметр, чтобы разбить результаты поиска по страницам.</span><span class="sxs-lookup"><span data-stu-id="c4c0c-p107">The first row that is included in the search results that are returned. You use this parameter when you want to implement paging for search results.</span></span>
  
    
    
 <span data-ttu-id="c4c0c-179">**Пример запроса GET**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-179">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="c4c0c-180">http:// _server_/_api/search/query?querytext='sharepoint'&amp;startrow=10</span><span class="sxs-lookup"><span data-stu-id="c4c0c-180">http:// _server_/_api/search/query?querytext='sharepoint'&amp;startrow=10</span></span>
  
    
    
 <span data-ttu-id="c4c0c-181">**Пример запроса POST**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-181">**Sample POST request**</span></span>
  
    
    



```

{
'__metadata' : {'type' : 'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
'StartRow' : '10'
}
```


### <a name="rowlimit"></a><span data-ttu-id="c4c0c-182">RowLimit</span><span class="sxs-lookup"><span data-stu-id="c4c0c-182">RowLimit</span></span>
<span data-ttu-id="c4c0c-183"><a name="bk_RowLimit"> </a></span><span class="sxs-lookup"><span data-stu-id="c4c0c-183"></span></span>

<span data-ttu-id="c4c0c-p108">Общее максимальное количество строк, которые возвращаются в результатах поиска. По сравнению с  _RowsPerPage_,  _RowLimit_  это максимальное количество возвращаемых строк в целом.</span><span class="sxs-lookup"><span data-stu-id="c4c0c-p108">The maximum number of rows overall that are returned in the search results. Compared to  _RowsPerPage_,  _RowLimit_ is the maximum number of rows returned overall.</span></span>
  
    
    
 <span data-ttu-id="c4c0c-186">**Пример запроса GET**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-186">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="c4c0c-187">http:// _server_/_api/search/query?querytext='sharepoint'&amp;rowlimit=30</span><span class="sxs-lookup"><span data-stu-id="c4c0c-187">http:// _server_/_api/search/query?querytext='sharepoint'&amp;rowlimit=30</span></span>
  
    
    
 <span data-ttu-id="c4c0c-188">**Пример запроса POST**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-188">**Sample POST request**</span></span>
  
    
    



```

{
'__metadata' : {'type' : 'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
'RowLimit' : '30'
}
```


### <a name="rowsperpage"></a><span data-ttu-id="c4c0c-189">RowsPerPage</span><span class="sxs-lookup"><span data-stu-id="c4c0c-189">RowsPerPage</span></span>
<span data-ttu-id="c4c0c-190"><a name="bk_RowsPerPage"> </a></span><span class="sxs-lookup"><span data-stu-id="c4c0c-190"></span></span>

<span data-ttu-id="c4c0c-p109">Максимальное количество строк, возвращаемых на каждую страницу. По сравнению с  _RowLimit_,  _RowsPerPage_ ссылается на максимальное количество строк, возвращаемых на страницу, и обычно используется в случаях, когда необходимо разбить результаты поиска по страницам.</span><span class="sxs-lookup"><span data-stu-id="c4c0c-p109">The maximum number of rows to return per page. Compared to  _RowLimit_,  _RowsPerPage_ refers to the maximum number of rows to return per page, and is used primarily when you want to implement paging for search results.</span></span>
  
    
    
 <span data-ttu-id="c4c0c-193">**Пример запроса GET**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-193">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="c4c0c-194">http:// _server_/_api/search/query?querytext='sharepoint'&amp;rowsperpage=10</span><span class="sxs-lookup"><span data-stu-id="c4c0c-194">http:// _server_/_api/search/query?querytext='sharepoint'&amp;rowsperpage=10</span></span>
  
    
    
 <span data-ttu-id="c4c0c-195">**Пример запроса POST**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-195">**Sample POST request**</span></span>
  
    
    



```

{
'__metadata' : {'type' : 'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
'RowsPerPage' : '10'
}
```


### <a name="selectproperties"></a><span data-ttu-id="c4c0c-196">SelectProperties</span><span class="sxs-lookup"><span data-stu-id="c4c0c-196">SelectProperties</span></span>
<span data-ttu-id="c4c0c-197"><a name="bk_SelectProperties"> </a></span><span class="sxs-lookup"><span data-stu-id="c4c0c-197"></span></span>

<span data-ttu-id="c4c0c-p110">Управляемые свойства, возвращаемые в результатах поиска. Чтобы вернуть управляемое свойство, установите флаг извлечения свойства в схеме поиска в значение **true**.</span><span class="sxs-lookup"><span data-stu-id="c4c0c-p110">The managed properties to return in the search results. To return a managed property, set the property's retrievable flag to **true** in the search schema.</span></span>
  
    
    
<span data-ttu-id="c4c0c-p111">Для запросов **GET** укажите в строке, содержащей список свойств, разделенных запятыми, параметр _SelectProperties_. Для запросов **POST** укажите параметр _SelectProperties_ в виде массива строк.</span><span class="sxs-lookup"><span data-stu-id="c4c0c-p111">For **GET** requests, you specify the _SelectProperties_ parameter in a string containing a comma-separated list of properties. For **POST** requests, you specify the _SelectProperties_ parameter as a string array.</span></span>
  
    
    
 <span data-ttu-id="c4c0c-202">**Пример запроса GET**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-202">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="c4c0c-203">http:// _server_/_api/search/query?querytext='sharepoint'&amp;selectproperties='Title,Author'</span><span class="sxs-lookup"><span data-stu-id="c4c0c-203">http:// _server_/_api/search/query?querytext='sharepoint'&amp;selectproperties='Title,Author'</span></span>
  
    
    
 <span data-ttu-id="c4c0c-204">**Пример запроса POST**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-204">**Sample POST request**</span></span>
  
    
    



```

{
'__metadata' : {'type' : 'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
'SelectProperties' : {
    'results' : [
          'Title,
          Author'
          ]
}
}
```


### <a name="culture"></a><span data-ttu-id="c4c0c-205">Culture</span><span class="sxs-lookup"><span data-stu-id="c4c0c-205">Culture</span></span>
<span data-ttu-id="c4c0c-206"><a name="bk_Culture"> </a></span><span class="sxs-lookup"><span data-stu-id="c4c0c-206"></span></span>

<span data-ttu-id="c4c0c-207">Код языка (LCID) для запроса (см. статью  [Коды языков, присвоенные Майкрософт](http://msdn.microsoft.com/en-us/goglobal/bb964664.aspx)).</span><span class="sxs-lookup"><span data-stu-id="c4c0c-207">The locale ID (LCID) for the query (see  [Locale IDs Assigned by Microsoft](http://msdn.microsoft.com/en-us/goglobal/bb964664.aspx)).</span></span>
  
    
    
 <span data-ttu-id="c4c0c-208">**Пример запроса GET**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-208">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="c4c0c-209">http:// _server_/_api/search/query?querytext='sharepoint'&amp;culture=1044</span><span class="sxs-lookup"><span data-stu-id="c4c0c-209">http:// _server_/_api/search/query?querytext='sharepoint'&amp;culture=1044</span></span>
  
    
    
 <span data-ttu-id="c4c0c-210">**Пример запроса POST**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-210">**Sample POST request**</span></span>
  
    
    



```

{
'__metadata' : {'type' : 'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
'Culture' : '1044'
}
```


### <a name="refinementfilters"></a><span data-ttu-id="c4c0c-211">RefinementFilters</span><span class="sxs-lookup"><span data-stu-id="c4c0c-211">RefinementFilters</span></span>
<span data-ttu-id="c4c0c-212"><a name="bk_RefinementFilters"> </a></span><span class="sxs-lookup"><span data-stu-id="c4c0c-212"></span></span>

<span data-ttu-id="c4c0c-p112">Набор фильтров уточнения, используемых при получении запроса уточнения. Для запросов **GET** параметр _RefinementFilters_ указывается в виде FQL-фильтра. Для запросов **POST** параметр _RefinementFilters_ указывается в виде массива FQL-фильтров.</span><span class="sxs-lookup"><span data-stu-id="c4c0c-p112">The set of refinement filters used when issuing a refinement query. For **GET** requests, the _RefinementFilters_ parameter is specified as an FQL filter. For **POST** requests, the _RefinementFilters_ parameter is specified as an array of FQL filters.</span></span>
  
    
    
 <span data-ttu-id="c4c0c-216">**Пример запроса GET**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-216">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="c4c0c-217">http:// _server_/_api/search/query?querytext='sharepoint'&amp;refinementfilters='fileExtension:equals("docx")'</span><span class="sxs-lookup"><span data-stu-id="c4c0c-217">http:// _server_/_api/search/query?querytext='sharepoint'&amp;refinementfilters='fileExtension:equals("docx")'</span></span>
  
    
    
 <span data-ttu-id="c4c0c-218">**Пример запроса POST**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-218">**Sample POST request**</span></span>
  
    
    



```

{
'__metadata' : {'type' : 'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
'RefinementFilters' : {
'results' : ['fileExtension:equals("docx")']
}
}
```


### <a name="refiners"></a><span data-ttu-id="c4c0c-219">Уточнения</span><span class="sxs-lookup"><span data-stu-id="c4c0c-219">Refiners</span></span>
<span data-ttu-id="c4c0c-220"><a name="bk_Refiners"> </a></span><span class="sxs-lookup"><span data-stu-id="c4c0c-220"></span></span>

<span data-ttu-id="c4c0c-221">Набор уточнений, возвращаемых в результатах поиска.</span><span class="sxs-lookup"><span data-stu-id="c4c0c-221">The set of refiners to return in a search result.</span></span>
  
    
    
 <span data-ttu-id="c4c0c-222">**Пример запроса GET**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-222">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="c4c0c-223">http:// _server_/_api/search/query?querytext='sharepoint'&amp;refiners='author,size'</span><span class="sxs-lookup"><span data-stu-id="c4c0c-223">http:// _server_/_api/search/query?querytext='sharepoint'&amp;refiners='author,size'</span></span>
  
    
    
 <span data-ttu-id="c4c0c-224">**Пример запроса POST**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-224">**Sample POST request**</span></span>
  
    
    



```

{
'__metadata':{'type':'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext':'sharepoint',
'Refiners': {
'results' : ['author,size']
}
}
```


### <a name="hiddenconstraints"></a><span data-ttu-id="c4c0c-225">HiddenConstraints</span><span class="sxs-lookup"><span data-stu-id="c4c0c-225">HiddenConstraints</span></span>
<span data-ttu-id="c4c0c-226"><a name="bk_HiddenConstraints"> </a></span><span class="sxs-lookup"><span data-stu-id="c4c0c-226"></span></span>

<span data-ttu-id="c4c0c-227">Дополнительные термины, присоединяемые к запросу.</span><span class="sxs-lookup"><span data-stu-id="c4c0c-227">The additional query terms to append to the query.</span></span>
  
    
    
 <span data-ttu-id="c4c0c-228">**Пример запроса GET**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-228">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="c4c0c-229">http:// _server_/_api/search/query?querytext='sharepoint'&amp;hiddenconstraints='developer'</span><span class="sxs-lookup"><span data-stu-id="c4c0c-229">http:// _server_/_api/search/query?querytext='sharepoint'&amp;hiddenconstraints='developer'</span></span>
  
    
    
 <span data-ttu-id="c4c0c-230">**Пример запроса POST**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-230">**Sample POST request**</span></span>
  
    
    



```

{
'__metadata':{'type':'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext':'sharepoint',
'HiddenConstraints':'developer'
}
```


### <a name="sortlist"></a><span data-ttu-id="c4c0c-231">SortList</span><span class="sxs-lookup"><span data-stu-id="c4c0c-231">SortList</span></span>
<span data-ttu-id="c4c0c-232"><a name="bk_SortList"> </a></span><span class="sxs-lookup"><span data-stu-id="c4c0c-232"></span></span>

<span data-ttu-id="c4c0c-233">Список свойств, по которым упорядочиваются результаты поиска.</span><span class="sxs-lookup"><span data-stu-id="c4c0c-233">The list of properties by which the search results are ordered.</span></span>
  
    
    
 <span data-ttu-id="c4c0c-234">**Пример запроса GET**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-234">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="c4c0c-235">http:// _server_/_api/search/query?querytext='sharepoint'&amp;sortlist='rank:descending,modifiedby:ascending'</span><span class="sxs-lookup"><span data-stu-id="c4c0c-235">http:// _server_/_api/search/query?querytext='sharepoint'&amp;sortlist='rank:descending,modifiedby:ascending'</span></span>
  
    
    
 <span data-ttu-id="c4c0c-236">**Пример запроса POST**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-236">**Sample POST request**</span></span>
  
    
    



```

{
'__metadata' : {'type':'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
'SortList' : 
{
    'results' : [
        {
                'Property':'Created',
                'Direction': '0'
        },
        {
                'Property':'FileExtension',
                'Direction': '1'
        }
    ]
}
}
```


### <a name="enablestemming"></a><span data-ttu-id="c4c0c-237">EnableStemming</span><span class="sxs-lookup"><span data-stu-id="c4c0c-237">EnableStemming</span></span>
<span data-ttu-id="c4c0c-238"><a name="bk_EnableStemming"> </a></span><span class="sxs-lookup"><span data-stu-id="c4c0c-238"></span></span>

<span data-ttu-id="c4c0c-239">Логическое значение, указывающее, включено ли выделение корней.</span><span class="sxs-lookup"><span data-stu-id="c4c0c-239">A Boolean value that specifies whether stemming is enabled.</span></span> 
  
    
    
 <span data-ttu-id="c4c0c-p113">Значение **true**, если выделение корней включено, иначе  **false**. Значение по умолчанию  **true**.</span><span class="sxs-lookup"><span data-stu-id="c4c0c-p113">**true** if the stemming is enabled; otherwise, **false**. The default value is **true**.</span></span>
  
    
    
 <span data-ttu-id="c4c0c-242">**Пример запроса GET**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-242">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="c4c0c-243">http:// _server_/_api/search/query?querytext='sharepoint'&amp;enablestemming=false</span><span class="sxs-lookup"><span data-stu-id="c4c0c-243">http:// _server_/_api/search/query?querytext='sharepoint'&amp;enablestemming=false</span></span>
  
    
    
 <span data-ttu-id="c4c0c-244">**Пример запроса POST**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-244">**Sample POST request**</span></span>
  
    
    



```

{
'__metadata' : {'type':'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
'EnableStemming : 'False'
}
```


### <a name="trimduplicates"></a><span data-ttu-id="c4c0c-245">TrimDuplicates</span><span class="sxs-lookup"><span data-stu-id="c4c0c-245">TrimDuplicates</span></span>
<span data-ttu-id="c4c0c-246"><a name="bk_TrimDuplicates"> </a></span><span class="sxs-lookup"><span data-stu-id="c4c0c-246"></span></span>

<span data-ttu-id="c4c0c-247">Логическое значение, указывающее, удалены ли из результатов повторяющиеся элементы.</span><span class="sxs-lookup"><span data-stu-id="c4c0c-247">A Boolean value that specifies whether duplicate items are removed from the results.</span></span> 
  
    
    
 <span data-ttu-id="c4c0c-p114">Значение **true**, чтобы удалить повторяющиеся элементы, иначе  **false**. Значение по умолчанию  **true**.</span><span class="sxs-lookup"><span data-stu-id="c4c0c-p114">**true** to remove the duplicate items; otherwise, **false**. The default value is **true**.</span></span>
  
    
    
 <span data-ttu-id="c4c0c-250">**Пример запроса GET**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-250">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="c4c0c-251">http:// _server_/_api/search/query?querytext='sharepoint'&amp;trimduplicates=false</span><span class="sxs-lookup"><span data-stu-id="c4c0c-251">http:// _server_/_api/search/query?querytext='sharepoint'&amp;trimduplicates=false</span></span>
  
    
    
 <span data-ttu-id="c4c0c-252">**Пример запроса POST**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-252">**Sample POST request**</span></span>
  
    
    



```

{
'__metadata':{'type':'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext':'sharepoint',
'TrimDuplicates':'False'
}
```


### <a name="timeout"></a><span data-ttu-id="c4c0c-253">Timeout</span><span class="sxs-lookup"><span data-stu-id="c4c0c-253">Timeout</span></span>
<span data-ttu-id="c4c0c-254"><a name="bk_Timeout"> </a></span><span class="sxs-lookup"><span data-stu-id="c4c0c-254"></span></span>

<span data-ttu-id="c4c0c-255">Время до истечения времени запроса в миллисекундах. Значение по умолчанию: 30 000.</span><span class="sxs-lookup"><span data-stu-id="c4c0c-255">The amount of time in milliseconds before the query request times out. The default value is 30000.</span></span>
  
    
    
 <span data-ttu-id="c4c0c-256">**Пример запроса GET**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-256">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="c4c0c-257">http:// _server_/_api/search/query?querytext='sharepoint'&amp;timeout=60000</span><span class="sxs-lookup"><span data-stu-id="c4c0c-257">http:// _server_/_api/search/query?querytext='sharepoint'&amp;timeout=60000</span></span>
  
    
    
 <span data-ttu-id="c4c0c-258">**Пример запроса POST**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-258">**Sample POST request**</span></span>
  
    
    



```

{
'__metadata':{'type':'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext':'sharepoint',
'Timeout':'60000'
}
```


### <a name="enablenicknames"></a><span data-ttu-id="c4c0c-259">EnableNicknames</span><span class="sxs-lookup"><span data-stu-id="c4c0c-259">EnableNicknames</span></span>
<span data-ttu-id="c4c0c-260"><a name="bk_EnableNicknames"> </a></span><span class="sxs-lookup"><span data-stu-id="c4c0c-260"></span></span>

<span data-ttu-id="c4c0c-261">Логическое значение, указывающее, используются для поиска совпадений только точные термины или еще и псевдонимы.</span><span class="sxs-lookup"><span data-stu-id="c4c0c-261">A Boolean value that specifies whether the exact terms in the search query are used to find matches, or if nicknames are used also.</span></span> 
  
    
    
 <span data-ttu-id="c4c0c-p115">Значение **true**, если используются псевдонимы; иначе  **false**. Значение по умолчанию  **false**.</span><span class="sxs-lookup"><span data-stu-id="c4c0c-p115">**true** if nicknames are used; otherwise, **false**. The default value is **false**.</span></span>
  
    
    
 <span data-ttu-id="c4c0c-264">**Пример запроса GET**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-264">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="c4c0c-265">http:// _server_/_api/search/query?querytext='sharepoint'&amp;enablenicknames=true</span><span class="sxs-lookup"><span data-stu-id="c4c0c-265">http:// _server_/_api/search/query?querytext='sharepoint'&amp;enablenicknames=true</span></span>
  
    
    
 <span data-ttu-id="c4c0c-266">**Пример запроса POST**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-266">**Sample POST request**</span></span>
  
    
    



```

{
'__metadata':{'type':'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext':'sharepoint',
'EnableNicknames':'True'
}
```


### <a name="enablephonetic"></a><span data-ttu-id="c4c0c-267">EnablePhonetic</span><span class="sxs-lookup"><span data-stu-id="c4c0c-267">EnablePhonetic</span></span>
<span data-ttu-id="c4c0c-268"><a name="bk_EnablePhonetic"> </a></span><span class="sxs-lookup"><span data-stu-id="c4c0c-268"></span></span>

<span data-ttu-id="c4c0c-269">Логическое значение, которое указывает, используется ли для поиска соответствий фонетические формы терминов запроса.</span><span class="sxs-lookup"><span data-stu-id="c4c0c-269">A Boolean value that specifies whether the phonetic forms of the query terms are used to find matches.</span></span> 
  
    
    
 <span data-ttu-id="c4c0c-p116">Значение **true**, если используются фонетические формы, иначе  **false**. Значение по умолчанию  **false**.</span><span class="sxs-lookup"><span data-stu-id="c4c0c-p116">**true** if phonetic forms are used; otherwise, **false**. The default value is **false**.</span></span>
  
    
    
 <span data-ttu-id="c4c0c-272">**Пример запроса GET**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-272">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="c4c0c-273">http:// _server_/_api/search/query?querytext='sharepoint'&amp;enablephonetic=true</span><span class="sxs-lookup"><span data-stu-id="c4c0c-273">http:// _server_/_api/search/query?querytext='sharepoint'&amp;enablephonetic=true</span></span>
  
    
    
 <span data-ttu-id="c4c0c-274">**Пример запроса POST**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-274">**Sample POST request**</span></span>
  
    
    



```

{
'__metadata':{'type':'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext':'sharepoint',
'EnablePhonetic':'True'
}
```


### <a name="enablefql"></a><span data-ttu-id="c4c0c-275">EnableFql</span><span class="sxs-lookup"><span data-stu-id="c4c0c-275">EnableFql</span></span>
<span data-ttu-id="c4c0c-276"><a name="bk_EnableFql"> </a></span><span class="sxs-lookup"><span data-stu-id="c4c0c-276"></span></span>

<span data-ttu-id="c4c0c-277">Логическое значение, указывающее, использует ли запрос язык FAST-запросов (FQL).</span><span class="sxs-lookup"><span data-stu-id="c4c0c-277">A Boolean value that specifies whether the query uses the FAST Query Language (FQL).</span></span> 
  
    
    
 <span data-ttu-id="c4c0c-p117">Значение **true**, если запрос является FQL-запросом, иначе  **false**. Значение по умолчанию  **false**.</span><span class="sxs-lookup"><span data-stu-id="c4c0c-p117">**true** if the query is an FQL query; otherwise, **false**. The default value is **false**.</span></span>
  
    
    
 <span data-ttu-id="c4c0c-280">**Пример запроса GET**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-280">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="c4c0c-281">http:// _server_/_api/search/query?querytext='sharepoint'&amp;enablefql=true</span><span class="sxs-lookup"><span data-stu-id="c4c0c-281">http:// _server_/_api/search/query?querytext='sharepoint'&amp;enablefql=true</span></span>
  
    
    
 <span data-ttu-id="c4c0c-282">**Пример запроса POST**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-282">**Sample POST request**</span></span>
  
    
    



```

{
'__metadata':{'type':'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext':'sharepoint',
'EnableFQL':'True'
}
```


### <a name="hithighlightedproperties"></a><span data-ttu-id="c4c0c-283">HithighlightedProperties</span><span class="sxs-lookup"><span data-stu-id="c4c0c-283">HithighlightedProperties</span></span>
<span data-ttu-id="c4c0c-284"><a name="bk_HithighlightedProperties"> </a></span><span class="sxs-lookup"><span data-stu-id="c4c0c-284"></span></span>

<span data-ttu-id="c4c0c-p118">Свойства, которые выделяются в сводке результатов поиска, если значение свойства соответствует терминам поиска, которые указал пользователь. Для запросов **GET** укажите в виде строки, содержащую список свойств, разделенных запятыми; для запросов **POST**  в виде массива строк.</span><span class="sxs-lookup"><span data-stu-id="c4c0c-p118">The properties to highlight in the search result summary when the property value matches the search terms entered by the user. For **GET** requests, Specify in a string containing a comma-separated list of properties. For **POST** requests, specify as an array of strings.</span></span>
  
    
    
 <span data-ttu-id="c4c0c-288">**Пример запроса GET**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-288">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="c4c0c-289">http:// _server_/_api/search/query?querytext='sharepoint'&amp;hithighlightedproperties='Title'</span><span class="sxs-lookup"><span data-stu-id="c4c0c-289">http:// _server_/_api/search/query?querytext='sharepoint'&amp;hithighlightedproperties='Title'</span></span>
  
    
    
 <span data-ttu-id="c4c0c-290">**Пример запроса POST**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-290">**Sample POST request**</span></span>
  
    
    



```

{
'__metadata' : {'type':'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
'HitHighlightedProperties' :  {
    'results' : [
         'Title'   
    ]
}
}
```


### <a name="bypassresulttypes"></a><span data-ttu-id="c4c0c-291">BypassResultTypes</span><span class="sxs-lookup"><span data-stu-id="c4c0c-291">BypassResultTypes</span></span>
<span data-ttu-id="c4c0c-292"><a name="bk_BypassResultTypes"> </a></span><span class="sxs-lookup"><span data-stu-id="c4c0c-292"></span></span>

<span data-ttu-id="c4c0c-293">Логическое значение, указывающее, следует ли выполнять обработку типа результата для запроса.</span><span class="sxs-lookup"><span data-stu-id="c4c0c-293">A Boolean value that specifies whether to perform result type processing for the query.</span></span> 
  
    
    
 <span data-ttu-id="c4c0c-p119">Значение **true**, чтобы выполнить обработку типа результата, иначе  **false**. Значение по умолчанию  **false**.</span><span class="sxs-lookup"><span data-stu-id="c4c0c-p119">**true** to perform result type processing; otherwise, **false**. The default value is **false**.</span></span>
  
    
    
 <span data-ttu-id="c4c0c-296">**Пример запроса GET**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-296">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="c4c0c-297">http:// _server_/_api/search/query?querytext='sharepoint'&amp;bypassresulttypes=true</span><span class="sxs-lookup"><span data-stu-id="c4c0c-297">http:// _server_/_api/search/query?querytext='sharepoint'&amp;bypassresulttypes=true</span></span>
  
    
    
 <span data-ttu-id="c4c0c-298">**Пример запроса POST**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-298">**Sample POST request**</span></span>
  
    
    



```

{
'__metadata' : {'type' : 'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
'BypassResultTypes' : 'true'
}
```


### <a name="processbestbets"></a><span data-ttu-id="c4c0c-299">ProcessBestBets</span><span class="sxs-lookup"><span data-stu-id="c4c0c-299">ProcessBestBets</span></span>
<span data-ttu-id="c4c0c-300"><a name="bk_ProcessBestBets"> </a></span><span class="sxs-lookup"><span data-stu-id="c4c0c-300"></span></span>

<span data-ttu-id="c4c0c-301">Логическое значение, указывающее, следует ли возвращать наиболее подходящие элементы результатов для запроса.</span><span class="sxs-lookup"><span data-stu-id="c4c0c-301">A Boolean value that specifies whether to return best bet results for the query.</span></span> 
  
    
    
 <span data-ttu-id="c4c0c-p120">Значение **true**, чтобы вернуть наиболее подходящие элементы, иначе  **false**. Этот параметр используется только когда **EnableQueryRules** установлен в значение **true**, в противном случае он игнорируется. Значение по умолчанию  **false**.</span><span class="sxs-lookup"><span data-stu-id="c4c0c-p120">**true** to return best bets; otherwise, **false**. This parameter is used only when **EnableQueryRules** is set to **true**, otherwise it is ignored. The default value is **false**.</span></span>
  
    
    
 <span data-ttu-id="c4c0c-305">**Пример запроса GET**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-305">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="c4c0c-306">http:// _server_/_api/search/query?querytext='sharepoint'&amp;processbestbets=true&amp;enablequeryrules=true</span><span class="sxs-lookup"><span data-stu-id="c4c0c-306">http:// _server_/_api/search/query?querytext='sharepoint'&amp;processbestbets=true&amp;enablequeryrules=true</span></span>
  
    
    
 <span data-ttu-id="c4c0c-307">**Пример запроса POST**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-307">**Sample POST request**</span></span>
  
    
    



```

{
'__metadata' : {'type' : 'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
'ProcessBestBets' : 'true',
'EnableQueryRules' : 'true'
}
```


### <a name="clienttype"></a><span data-ttu-id="c4c0c-308">ClientType</span><span class="sxs-lookup"><span data-stu-id="c4c0c-308">ClientType</span></span>
<span data-ttu-id="c4c0c-309"><a name="bk_ClientType"> </a></span><span class="sxs-lookup"><span data-stu-id="c4c0c-309"></span></span>

<span data-ttu-id="c4c0c-310">Тип клиента, выдавшего запрос.</span><span class="sxs-lookup"><span data-stu-id="c4c0c-310">The type of the client that issued the query.</span></span>
  
    
    
 <span data-ttu-id="c4c0c-311">**Пример запроса GET**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-311">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="c4c0c-312">http:// _server_/_api/search/query?querytext='sharepoint'&amp;clienttype='custom'</span><span class="sxs-lookup"><span data-stu-id="c4c0c-312">http:// _server_/_api/search/query?querytext='sharepoint'&amp;clienttype='custom'</span></span>
  
    
    
 <span data-ttu-id="c4c0c-313">**Пример запроса POST**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-313">**Sample POST request**</span></span>
  
    
    



```

{
'__metadata':{'type':'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext':'sharepoint',
'ClientType':'custom'
}
```


### <a name="personalizationdata"></a><span data-ttu-id="c4c0c-314">PersonalizationData</span><span class="sxs-lookup"><span data-stu-id="c4c0c-314">PersonalizationData</span></span>
<span data-ttu-id="c4c0c-315"><a name="bk_PersonalizationData"> </a></span><span class="sxs-lookup"><span data-stu-id="c4c0c-315"></span></span>

<span data-ttu-id="c4c0c-316">GUID пользователя, отправившего запрос поиска.</span><span class="sxs-lookup"><span data-stu-id="c4c0c-316">The GUID for the user who submitted the search query.</span></span>
  
    
    
 <span data-ttu-id="c4c0c-317">**Пример запроса GET**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-317">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="c4c0c-318">http:// _\<server\>_/_api/search/query?querytext='sharepoint'&amp;personalizationdata=' _\<GUID\>_'</span><span class="sxs-lookup"><span data-stu-id="c4c0c-318">http:// _\<server\>_/_api/search/query?querytext='sharepoint'&amp;personalizationdata=' _\<GUID\>_'</span></span>
  
    
    
 <span data-ttu-id="c4c0c-319">**Пример запроса POST**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-319">**Sample POST request**</span></span>
  
    
    



```

{
'__metadata' : {'type' : 'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
'PersonalizationData' : ' <GUID> '
}
```


### <a name="resultsurl"></a><span data-ttu-id="c4c0c-320">ResultsURL</span><span class="sxs-lookup"><span data-stu-id="c4c0c-320">ResultsURL</span></span>
<span data-ttu-id="c4c0c-321"><a name="bk_ResultsURL"> </a></span><span class="sxs-lookup"><span data-stu-id="c4c0c-321"></span></span>

<span data-ttu-id="c4c0c-322">URL-адрес для страницы результатов поиска.</span><span class="sxs-lookup"><span data-stu-id="c4c0c-322">The URL for the search results page.</span></span>
  
    
    
 <span data-ttu-id="c4c0c-323">**Пример запроса GET**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-323">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="c4c0c-324">http:// _server_/_api/search/query?querytext='sharepoint'&amp;resultsurl='http://server/site/resultspage.aspx'</span><span class="sxs-lookup"><span data-stu-id="c4c0c-324">http:// _server_/_api/search/query?querytext='sharepoint'&amp;resultsurl='http://server/site/resultspage.aspx'</span></span>
  
    
    
 <span data-ttu-id="c4c0c-325">**Пример запроса POST**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-325">**Sample POST request**</span></span>
  
    
    



```

{
'__metadata' : {'type' : 'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint'
'ResultURL' : 'http://server/site/resultspage.aspx'
}
```


### <a name="querytag"></a><span data-ttu-id="c4c0c-326">QueryTag</span><span class="sxs-lookup"><span data-stu-id="c4c0c-326">QueryTag</span></span>
<span data-ttu-id="c4c0c-327"><a name="bk_QueryTag"> </a></span><span class="sxs-lookup"><span data-stu-id="c4c0c-327"></span></span>

<span data-ttu-id="c4c0c-p121">Пользовательские теги, идентифицирующие запрос. Вы можете указать несколько тегов запроса, разделенных точкой с запятой.</span><span class="sxs-lookup"><span data-stu-id="c4c0c-p121">Custom tags that identify the query. You can specify multiple query tags, separated by semicolons.</span></span>
  
    
    
 <span data-ttu-id="c4c0c-330">**Пример запроса GET**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-330">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="c4c0c-331">http:// _server_/_api/search/query?querytext='sharepoint'</span><span class="sxs-lookup"><span data-stu-id="c4c0c-331">http:// _server_/_api/search/query?querytext='sharepoint'</span></span>
  
    
    
 <span data-ttu-id="c4c0c-332">**Пример запроса POST**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-332">**Sample POST request**</span></span>
  
    
    



```

{
'__metadata':{'type':'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext':'sharepoint'
}
```


### <a name="properties"></a><span data-ttu-id="c4c0c-333">Свойства</span><span class="sxs-lookup"><span data-stu-id="c4c0c-333">Properties</span></span>
<span data-ttu-id="c4c0c-334"><a name="bk_Properties"> </a></span><span class="sxs-lookup"><span data-stu-id="c4c0c-334"></span></span>

<span data-ttu-id="c4c0c-p122">Дополнительные свойства для запроса. Запросы **GET** поддерживают только строковое значение. Запросы **POST** поддерживают значения любого типа.</span><span class="sxs-lookup"><span data-stu-id="c4c0c-p122">Additional properties for the query. **GET** requests support only string values. **POST** requests support values of any type.</span></span>
  
    
    
 <span data-ttu-id="c4c0c-338">**Пример запроса GET**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-338">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="c4c0c-339">http:// _server_/_api/search/query?querytext='sharepoint'&amp;properties='termid:guid'</span><span class="sxs-lookup"><span data-stu-id="c4c0c-339">http:// _server_/_api/search/query?querytext='sharepoint'&amp;properties='termid:guid'</span></span>
  
    
    
 <span data-ttu-id="c4c0c-340">**Пример запроса POST**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-340">**Sample POST request**</span></span>
  
    
    



```

{
'__metadata':{'type':'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext':'sharepoint',
'Properties' : {
     'results' : [
          {
               'Name' : 'sampleBooleanProperty',
               'Value' :
               {
                    'BoolVal' : 'True',
                    'QueryPropertyValueTypeIndex' : 3
               }
          },
          {
               'Name' : 'sampleIntProperty',
               'Value' : 
               {
                    'IntVal' : '1234',
                    'QueryPropertyValueTypeIndex' : 2
               }
          }
     ]
}
}
```


> <span data-ttu-id="c4c0c-341">**Примечание.** [QueryPropertyValueType](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.QueryPropertyValueType.aspx) указывает тип свойства. Каждому типу соответствует определенное значение индекса.</span><span class="sxs-lookup"><span data-stu-id="c4c0c-341">Note  QueryPropertyValueType specifies the type for the property; each type has a specific index value.</span></span>
  
    
    


### <a name="enablequeryrules"></a><span data-ttu-id="c4c0c-342">EnableQueryRules</span><span class="sxs-lookup"><span data-stu-id="c4c0c-342">EnableQueryRules</span></span>
<span data-ttu-id="c4c0c-343"><a name="bk_EnableQueryRules"> </a></span><span class="sxs-lookup"><span data-stu-id="c4c0c-343"></span></span>

<span data-ttu-id="c4c0c-344">Логическое значение, указывающее, включены ли правила запросов для запроса.</span><span class="sxs-lookup"><span data-stu-id="c4c0c-344">A Boolean value that specifies whether to enable query rules for the query.</span></span> 
  
    
    
 <span data-ttu-id="c4c0c-p123">Значение **true**, чтобы включить правила запросов, иначе  **false**. Значение по умолчанию  **true**.</span><span class="sxs-lookup"><span data-stu-id="c4c0c-p123">**true** to enable query rules; otherwise, **false**. The default value is **true**.</span></span>
  
    
    
 <span data-ttu-id="c4c0c-347">**Пример запроса GET**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-347">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="c4c0c-348">http:// _server_/_api/search/query?querytext='sharepoint'&amp;enablequeryrules=false</span><span class="sxs-lookup"><span data-stu-id="c4c0c-348">http:// _server_/_api/search/query?querytext='sharepoint'&amp;enablequeryrules=false</span></span>
  
    
    
 <span data-ttu-id="c4c0c-349">**Пример запроса POST**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-349">**Sample POST request**</span></span>
  
    
    



```

{
'__metadata' : {'type' : 'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
'EnableQueryRules' : 'false' 
}
```


### <a name="reorderingrules"></a><span data-ttu-id="c4c0c-350">ReorderingRules</span><span class="sxs-lookup"><span data-stu-id="c4c0c-350">ReorderingRules</span></span>
<span data-ttu-id="c4c0c-351"><a name="bk_ReorderingRules"> </a></span><span class="sxs-lookup"><span data-stu-id="c4c0c-351"></span></span>

<span data-ttu-id="c4c0c-p124">Специальные правила для изменения порядка результатов поиска. Эти правила могут указывать, что документы, соответствующие определенным условиям, имеют более высокий или более низкий рейтинг в результатах. Это свойство применяется только тогда, когда результаты поиска отсортированы на основе рейтинга. Используйте для этого свойства запрос **POST**, оно не работает с запросом **GET**.</span><span class="sxs-lookup"><span data-stu-id="c4c0c-p124">Special rules for reordering search results. These rules can specify that documents matching certain conditions are ranked higher or lower in the results. This property applies only when search results are sorted based on rank. You must use a **POST** request for this property; it does not work in a **GET** request.</span></span>
  
    
    
<span data-ttu-id="c4c0c-p125">В следующем примере  _MatchType_ относится к [ReorderingRuleMatchType](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ReorderingRuleMatchType.aspx) . В следующем примере `'MatchType' : '0'` определяет [ResultContainsKeyword](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ReorderingRuleMatchType.ResultContainsKeyword.aspx) .</span><span class="sxs-lookup"><span data-stu-id="c4c0c-p125">In the following example,  _MatchType_ refers to [ReorderingRuleMatchType](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ReorderingRuleMatchType.aspx) . In the following example, `'MatchType' : '0'` specifies [ResultContainsKeyword](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ReorderingRuleMatchType.ResultContainsKeyword.aspx) .</span></span>
  
    
    
 <span data-ttu-id="c4c0c-358">**Пример запроса POST**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-358">**Sample POST request**</span></span>
  
    
    



```

{
'__metadata' : {'type' : 'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
'ReorderingRules' :  {
    'results' : [
         {
             'MatchValue' : '<someValue>',
             'Boost' : '10',
             'MatchType' : '0'
         }
    ]
}
}
```


### <a name="processpersonalfavorites"></a><span data-ttu-id="c4c0c-359">ProcessPersonalFavorites</span><span class="sxs-lookup"><span data-stu-id="c4c0c-359">ProcessPersonalFavorites</span></span>
<span data-ttu-id="c4c0c-360"><a name="bk_ProcessPersonalFavorites"> </a></span><span class="sxs-lookup"><span data-stu-id="c4c0c-360"></span></span>

<span data-ttu-id="c4c0c-361">Логическое значение, указывающее, возвращать ли личное избранное с результатами поиска.</span><span class="sxs-lookup"><span data-stu-id="c4c0c-361">A Boolean value that specifies whether to return personal favorites with the search results.</span></span> 
  
    
    
 <span data-ttu-id="c4c0c-362">Значение **true**, чтобы вернуть личное избранное, иначе  **false**.</span><span class="sxs-lookup"><span data-stu-id="c4c0c-362">**true** to return personal favorites; otherwise **false**.</span></span> 
  
    
    
 <span data-ttu-id="c4c0c-363">**Пример запроса GET**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-363">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="c4c0c-364">http:// _server_/_api/search/query?querytext='sharepoint'&amp;processpersonalfavorites=true</span><span class="sxs-lookup"><span data-stu-id="c4c0c-364">http:// _server_/_api/search/query?querytext='sharepoint'&amp;processpersonalfavorites=true</span></span>
  
    
    
 <span data-ttu-id="c4c0c-365">**Пример запроса POST**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-365">**Sample POST request**</span></span>
  
    
    



```

{
'__metadata':{'type':'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
'ProcessPersonalFavorites' : 'false'
}
```


### <a name="querytemplatepropertiesurl"></a><span data-ttu-id="c4c0c-366">QueryTemplatePropertiesUrl</span><span class="sxs-lookup"><span data-stu-id="c4c0c-366">QueryTemplatePropertiesUrl</span></span>
<span data-ttu-id="c4c0c-367"><a name="bk_ProcessPersonalFavorites"> </a></span><span class="sxs-lookup"><span data-stu-id="c4c0c-367"></span></span>

<span data-ttu-id="c4c0c-p126">Расположение файла queryparametertemplate.xml. Этот файл используется для того, чтобы разрешить анонимным пользователям создавать запросы поиска REST.</span><span class="sxs-lookup"><span data-stu-id="c4c0c-p126">The location of the queryparametertemplate.xml file. This file is used to enable anonymous users to make Search REST queries.</span></span>
  
    
    
 <span data-ttu-id="c4c0c-370">**Пример запроса GET**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-370">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="c4c0c-371">http:// _server_/_api/search/query?querytext='sharepoint'&amp;querytemplatepropertiesurl='spfile://webroot/queryparametertemplate.xml'</span><span class="sxs-lookup"><span data-stu-id="c4c0c-371">http:// _server_/_api/search/query?querytext='sharepoint'&amp;querytemplatepropertiesurl='spfile://webroot/queryparametertemplate.xml'</span></span>
  
    
    
 <span data-ttu-id="c4c0c-372">**Пример запроса POST**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-372">**Sample POST request**</span></span>
  
    
    



```

{
'__metadata':{'type':'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
QueryTemplatePropertiesUrl : 'spfile://webroot/queryparametertemplate.xml'
}
```


### <a name="hithighlightedmultivaluepropertylimit"></a><span data-ttu-id="c4c0c-373">HitHighlightedMultivaluePropertyLimit</span><span class="sxs-lookup"><span data-stu-id="c4c0c-373">HitHighlightedMultivaluePropertyLimit</span></span>
<span data-ttu-id="c4c0c-374"><a name="bk_ProcessPersonalFavorites"> </a></span><span class="sxs-lookup"><span data-stu-id="c4c0c-374"></span></span>

<span data-ttu-id="c4c0c-375">Количество свойств, которые отображаются как подсвеченные совпадения в результатах поиска.</span><span class="sxs-lookup"><span data-stu-id="c4c0c-375">The number of properties to show hit highlighting for in the search results.</span></span>
  
    
    
 <span data-ttu-id="c4c0c-376">**Пример запроса GET**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-376">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="c4c0c-377">http:// _server_/_api/search/query?querytext='sharepoint'&amp;hithighlightedmultivaluepropertylimit=2</span><span class="sxs-lookup"><span data-stu-id="c4c0c-377">http:// _server_/_api/search/query?querytext='sharepoint'&amp;hithighlightedmultivaluepropertylimit=2</span></span>
  
    
    
 <span data-ttu-id="c4c0c-378">**Пример запроса POST**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-378">**Sample POST request**</span></span>
  
    
    



```

{
'__metadata':{'type':'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
'HitHighlihtedMultivaluePropertyLimit' : '2'
}
```


### <a name="enableorderinghithighlightedproperty"></a><span data-ttu-id="c4c0c-379">EnableOrderingHitHighlightedProperty</span><span class="sxs-lookup"><span data-stu-id="c4c0c-379">EnableOrderingHitHighlightedProperty</span></span>
<span data-ttu-id="c4c0c-380"><a name="bk_ProcessPersonalFavorites"> </a></span><span class="sxs-lookup"><span data-stu-id="c4c0c-380"></span></span>

<span data-ttu-id="c4c0c-381">Логическое значение, указывающее, упорядочивать ли свойства подсвеченных совпадений.</span><span class="sxs-lookup"><span data-stu-id="c4c0c-381">A Boolean value that specifies whether the hit highlighted properties can be ordered.</span></span> 
  
    
    
 <span data-ttu-id="c4c0c-382">Значение **true**, чтобы включить правила упорядочивания, иначе  **false**.</span><span class="sxs-lookup"><span data-stu-id="c4c0c-382">**true** to enable ordering rules; otherwise **false**.</span></span>
  
    
    
 <span data-ttu-id="c4c0c-383">**Пример запроса GET**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-383">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="c4c0c-384">http:// _server_/_api/search/query?querytext='sharepoint'&amp;enableorderinghithighlightedproperty=false</span><span class="sxs-lookup"><span data-stu-id="c4c0c-384">http:// _server_/_api/search/query?querytext='sharepoint'&amp;enableorderinghithighlightedproperty=false</span></span>
  
    
    
 <span data-ttu-id="c4c0c-385">**Пример запроса POST**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-385">**Sample POST request**</span></span>
  
    
    



```

{
'__metadata':{'type':'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
'EnableOrderingHitHighlightedProperty' : 'false'
}
```


### <a name="collapsespecification"></a><span data-ttu-id="c4c0c-386">CollapseSpecification</span><span class="sxs-lookup"><span data-stu-id="c4c0c-386">CollapseSpecification</span></span>
<span data-ttu-id="c4c0c-387"><a name="bk_ProcessPersonalFavorites"> </a></span><span class="sxs-lookup"><span data-stu-id="c4c0c-387"></span></span>

<span data-ttu-id="c4c0c-p127">Управляемые свойства, которые используются для определения способа свертывания отдельных результатов поиска. Результаты сворачиваются в один результат или указанное число результатов, если они соответствуют любым отдельным спецификациям свертывания. В рамках одной спецификации результаты сворачиваются, если их свойства соответствуют всем отдельным свойствам в спецификации.</span><span class="sxs-lookup"><span data-stu-id="c4c0c-p127">The managed properties that are used to determine how to collapse individual search results. Results are collapsed into one or a specified number of results if they match any of the individual collapse specifications. Within a single collapse specification, results are collapsed if their properties match all individual properties in the collapse specification.</span></span>
  
    
    
 <span data-ttu-id="c4c0c-391">**Пример запроса GET**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-391">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="c4c0c-392">http:// _server_/_api/search/query?querytext='sharepoint'&amp;collapsespecification='Author:1 ContentType:2'</span><span class="sxs-lookup"><span data-stu-id="c4c0c-392">http:// _server_/_api/search/query?querytext='sharepoint'&amp;collapsespecification='Author:1 ContentType:2'</span></span>
  
    
    
 <span data-ttu-id="c4c0c-393">**Пример запроса POST**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-393">**Sample POST request**</span></span>
  
    
    



```

{
'__metadata':{'type':'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
'CollapseSpecification' : 'Author:1 ContentType:2'
}
```


### <a name="enablesorting"></a><span data-ttu-id="c4c0c-394">EnableSorting</span><span class="sxs-lookup"><span data-stu-id="c4c0c-394">EnableSorting</span></span>
<span data-ttu-id="c4c0c-395"><a name="bk_ProcessPersonalFavorites"> </a></span><span class="sxs-lookup"><span data-stu-id="c4c0c-395"></span></span>

<span data-ttu-id="c4c0c-396">Логическое значение, указывающее, требуется ли сортировка результатов поиска.</span><span class="sxs-lookup"><span data-stu-id="c4c0c-396">A Boolean value that specifies whether to sort search results.</span></span> 
  
    
    
<span data-ttu-id="c4c0c-p128">Значение **true**, чтобы отсортировать результаты поиска с использованием параметра  _SortList_, или по рейтингу, если  _SortList_  пустое. Значение **false**, чтобы оставить результаты неотсортированными.</span><span class="sxs-lookup"><span data-stu-id="c4c0c-p128">I **true** to sort search results using _SortList_, or by rank if  _SortList_ is empty. **false** to leave results unsorted.</span></span>
  
    
    
 <span data-ttu-id="c4c0c-399">**Пример запроса GET**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-399">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="c4c0c-400">http:// _server_/_api/search/query?querytext='sharepoint'&amp;enablesorting=false</span><span class="sxs-lookup"><span data-stu-id="c4c0c-400">http:// _server_/_api/search/query?querytext='sharepoint'&amp;enablesorting=false</span></span>
  
    
    
 <span data-ttu-id="c4c0c-401">**Пример запроса POST**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-401">**Sample POST request**</span></span>
  
    
    



```

{
'__metadata':{'type':'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
'EnableSorting' : 'false'
}
```


### <a name="generateblockranklog"></a><span data-ttu-id="c4c0c-402">GenerateBlockRankLog</span><span class="sxs-lookup"><span data-stu-id="c4c0c-402">GenerateBlockRankLog</span></span>
<span data-ttu-id="c4c0c-403"><a name="bk_ProcessPersonalFavorites"> </a></span><span class="sxs-lookup"><span data-stu-id="c4c0c-403"></span></span>

<span data-ttu-id="c4c0c-p129">Логическое значение, указывающее, следует ли возвращать сведения о журнале для рейтинга блоков в свойстве **BlockRankLog** таблицы чередующихся результатов. Журнал рейтинга блоков содержит текстовые сведения по рейтингу блоков и удаленным повторяющимся документам.</span><span class="sxs-lookup"><span data-stu-id="c4c0c-p129">A Boolean value that specifies whether to return block rank log information in the **BlockRankLog** property of the interleaved result table. A block rank log contains the textual information on the block score and the documents that were de-duplicated.</span></span>
  
    
    
 <span data-ttu-id="c4c0c-406">Значение **true**, чтобы вернуть сведения о журнале рейтинга блоков, иначе  **false**.</span><span class="sxs-lookup"><span data-stu-id="c4c0c-406">**true** to return block rank log information; otherwise, **false**.</span></span>
  
    
    
 <span data-ttu-id="c4c0c-407">**Пример запроса GET**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-407">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="c4c0c-408">http:// _server_/_api/search/query?querytext='sharepoint'&amp;generateblockranklog=true</span><span class="sxs-lookup"><span data-stu-id="c4c0c-408">http:// _server_/_api/search/query?querytext='sharepoint'&amp;generateblockranklog=true</span></span>
  
    
    
 <span data-ttu-id="c4c0c-409">**Пример запроса POST**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-409">**Sample POST request**</span></span>
  
    
    



```

{
'__metadata':{'type':'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
'GenerateBlockRankLog' : 'true'
}
```


### <a name="uilanguage"></a><span data-ttu-id="c4c0c-410">UIlanguage</span><span class="sxs-lookup"><span data-stu-id="c4c0c-410">UIlanguage</span></span>
<span data-ttu-id="c4c0c-411"><a name="bk_ProcessPersonalFavorites"> </a></span><span class="sxs-lookup"><span data-stu-id="c4c0c-411"></span></span>

<span data-ttu-id="c4c0c-412">Код языка (LCID) интерфейса пользователя (см. статью  [Коды языков, присвоенные Майкрософт](http://msdn.microsoft.com/en-us/goglobal/bb964664)).</span><span class="sxs-lookup"><span data-stu-id="c4c0c-412">The locale identifier (LCID) of the user interface (see  [Locale IDs Assigned by Microsoft](http://msdn.microsoft.com/en-us/goglobal/bb964664)).</span></span>
  
    
    
 <span data-ttu-id="c4c0c-413">**Пример запроса GET**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-413">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="c4c0c-414">http:// _server_/_api/search/query?querytext='sharepoint'&amp;uilanguage=1044</span><span class="sxs-lookup"><span data-stu-id="c4c0c-414">http:// _server_/_api/search/query?querytext='sharepoint'&amp;uilanguage=1044</span></span>
  
    
    
 <span data-ttu-id="c4c0c-415">**Пример запроса POST**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-415">**Sample POST request**</span></span>
  
    
    



```

{
'__metadata':{'type':'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
'UILanguage' : '1044'
}
```


### <a name="desiredsnippetlength"></a><span data-ttu-id="c4c0c-416">DesiredSnippetLength</span><span class="sxs-lookup"><span data-stu-id="c4c0c-416">DesiredSnippetLength</span></span>
<span data-ttu-id="c4c0c-417"><a name="bk_ProcessPersonalFavorites"> </a></span><span class="sxs-lookup"><span data-stu-id="c4c0c-417"></span></span>

<span data-ttu-id="c4c0c-418">Предпочтительное количество символов для отображения в сводке подсвеченных совпадений, которая создана для результатов поиска.</span><span class="sxs-lookup"><span data-stu-id="c4c0c-418">The preferred number of characters to display in the hit-highlighted summary generated for a search result.</span></span>
  
    
    
 <span data-ttu-id="c4c0c-419">**Пример запроса GET**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-419">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="c4c0c-420">http:// _server_/_api/search/query?querytext='sharepoint'&amp;desiredsnippetlength=80</span><span class="sxs-lookup"><span data-stu-id="c4c0c-420">http:// _server_/_api/search/query?querytext='sharepoint'&amp;desiredsnippetlength=80</span></span>
  
    
    
 <span data-ttu-id="c4c0c-421">**Пример запроса POST**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-421">**Sample POST request**</span></span>
  
    
    



```

{
'__metadata':{'type':'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
'DesiredSnippetLength' : '80'
}
```


### <a name="maxsnippetlength"></a><span data-ttu-id="c4c0c-422">MaxSnippetLength</span><span class="sxs-lookup"><span data-stu-id="c4c0c-422">MaxSnippetLength</span></span>
<span data-ttu-id="c4c0c-423"><a name="bk_ProcessPersonalFavorites"> </a></span><span class="sxs-lookup"><span data-stu-id="c4c0c-423"></span></span>

<span data-ttu-id="c4c0c-424">Максимальное количество символов, которые отображаются в сводке подсвеченных совпадений, созданной для результатов поиска.</span><span class="sxs-lookup"><span data-stu-id="c4c0c-424">The maximum number of characters to display in the hit-highlighted summary generated for a search result.</span></span>
  
    
    
 <span data-ttu-id="c4c0c-425">**Пример запроса GET**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-425">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="c4c0c-426">http:// _server_/_api/search/query?querytext='sharepoint'&amp;maxsnippetlength=100</span><span class="sxs-lookup"><span data-stu-id="c4c0c-426">http:// _server_/_api/search/query?querytext='sharepoint'&amp;maxsnippetlength=100</span></span>
  
    
    
 <span data-ttu-id="c4c0c-427">**Пример запроса POST**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-427">**Sample POST request**</span></span>
  
    
    



```

{
'__metadata':{'type':'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
'MaxSnippetLength' : '100' 
}
```


### <a name="summarylength"></a><span data-ttu-id="c4c0c-428">SummaryLength</span><span class="sxs-lookup"><span data-stu-id="c4c0c-428">SummaryLength</span></span>
<span data-ttu-id="c4c0c-429"><a name="bk_ProcessPersonalFavorites"> </a></span><span class="sxs-lookup"><span data-stu-id="c4c0c-429"></span></span>

<span data-ttu-id="c4c0c-430">Количество символов, которые отображаются в сводке результатов для результатов поиска.</span><span class="sxs-lookup"><span data-stu-id="c4c0c-430">The number of characters to display in the result summary for a search result.</span></span>
  
    
    
 <span data-ttu-id="c4c0c-431">**Пример запроса GET**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-431">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="c4c0c-432">http:// _server_/_api/search/query?querytext='sharepoint'&amp;summarylength=150</span><span class="sxs-lookup"><span data-stu-id="c4c0c-432">http:// _server_/_api/search/query?querytext='sharepoint'&amp;summarylength=150</span></span>
  
    
    
 <span data-ttu-id="c4c0c-433">**Пример запроса POST**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-433">**Sample POST request**</span></span>
  
    
    



```

{
'__metadata':{'type':'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'sharepoint',
'Summarylength' : '150'
}
```


## <a name="enabling-anonymous-search-rest-queries"></a><span data-ttu-id="c4c0c-434">Включение анонимных запросов поиска REST</span><span class="sxs-lookup"><span data-stu-id="c4c0c-434">Enabling anonymous Search REST queries</span></span>
<span data-ttu-id="c4c0c-435"><a name="bk_AnonymousREST"> </a></span><span class="sxs-lookup"><span data-stu-id="c4c0c-435"></span></span>

<span data-ttu-id="c4c0c-p130">Вы можете настроить поиск, который поддерживает запросы поиска REST от анонимных пользователей. Администраторы сайта могут определить с помощью файла queryparametertemplate.xml, какие параметры запросов предоставить анонимным пользователям. В этом разделе описано, как настроить свой сайт, чтобы включить анонимный доступ, и создать файл queryparametertemplate.xml.</span><span class="sxs-lookup"><span data-stu-id="c4c0c-p130">You can configure search to support Search REST queries from anonymous users. Site administrators can decide what query parameters to expose to anonymous users by using the queryparametertemplate.xml file. This section describes how to configure your site to enable anonymous access, and create the queryparametertemplate.xml file.</span></span>
  
    
    

### <a name="to-enable-anonymous-search-rest-queries"></a><span data-ttu-id="c4c0c-439">Чтобы включить анонимные запросы поиска REST:</span><span class="sxs-lookup"><span data-stu-id="c4c0c-439">To enable anonymous Search REST queries</span></span>


1. <span data-ttu-id="c4c0c-p131">Включите анонимный доступ в веб-приложении и на сайте публикации. Более подробную информацию о том, как это сделать, можно узнать в статьях  [Управление политиками разрешений для веб-приложения в SharePoint](http://technet.microsoft.com/en-us/library/ff608071.aspx) и [Планирование методов проверки подлинности пользователя в SharePoint](http://technet.microsoft.com/en-us/library/cc262350.aspx) на сайте [TechNet](http://technet.microsoft.com/en-US/).</span><span class="sxs-lookup"><span data-stu-id="c4c0c-p131">Enable anonymous access on the web application and publishing site. For more information about how to do this, see  [Manage permission policies for a web application in SharePoint](http://technet.microsoft.com/en-us/library/ff608071.aspx) and [Plan for user authentication methods in SharePoint](http://technet.microsoft.com/en-us/library/cc262350.aspx) on [TechNet](http://technet.microsoft.com/en-US/).</span></span>
    
  
2. <span data-ttu-id="c4c0c-442">Добавьте на сайт публикации новую библиотеку документов с именем QueryPropertiesTemplate.</span><span class="sxs-lookup"><span data-stu-id="c4c0c-442">Add a new document library named QueryPropertiesTemplate to the publishing site.</span></span>
    
  
3. <span data-ttu-id="c4c0c-443">Создайте XML-файл с именем queryparametertemplate.xml и скопируйте в него следующий XML-код:</span><span class="sxs-lookup"><span data-stu-id="c4c0c-443">Create an XML file named queryparametertemplate.xml, and copy the following XML to the file.</span></span>
    
```XML
  
<QueryPropertiesTemplate xmlns="http://www.microsoft.com/sharepoint/search/KnownTypes/2008/08" xmlns:i="http://www.w3.org/2001/XMLSchema-instance">
    <QueryProperties i:type="KeywordQueryProperties">
        <EnableStemming>true</EnableStemming>
        <FarmId>FarmID</FarmId>
        <IgnoreAllNoiseQuery>true</IgnoreAllNoiseQuery>
        <KeywordInclusion>AllKeywords</KeywordInclusion>
        <SiteId>SiteID</SiteId>
        <SummaryLength>180</SummaryLength>
        <TrimDuplicates>true</TrimDuplicates>
        <WcfTimeout>120000</WcfTimeout>
        <WebId>WebID</WebId>
        <Properties xmlns:a="http://schemas.microsoft.com/2003/10/Serialization/Arrays">
            <a:KeyValueOfstringanyType>
                <a:Key>_IsEntSearchLicensed</a:Key>
                <a:Value i:type="b:boolean" xmlns:b="http://www.w3.org/2001/XMLSchema">true</a:Value>
            </a:KeyValueOfstringanyType>
            <a:KeyValueOfstringanyType>
                <a:Key>EnableSorting</a:Key>
                <a:Value i:type="b:boolean" xmlns:b="http://www.w3.org/2001/XMLSchema">true</a:Value>
            </a:KeyValueOfstringanyType>
            <a:KeyValueOfstringanyType>
                <a:Key>MaxKeywordQueryTextLength</a:Key>
                <a:Value i:type="b:int" xmlns:b="http://www.w3.org/2001/XMLSchema">4096</a:Value>
            </a:KeyValueOfstringanyType>
            <a:KeyValueOfstringanyType>
                <a:Key>TryCache</a:Key>
                <a:Value i:type="b:boolean" xmlns:b="http://www.w3.org/2001/XMLSchema">true</a:Value>
            </a:KeyValueOfstringanyType>
        </Properties>
        <PropertiesContractVersion>15.0.0.0</PropertiesContractVersion>
        <EnableFQL>false</EnableFQL>
        <EnableSpellcheck>Suggest</EnableSpellcheck>
        <EnableUrlSmashing>true</EnableUrlSmashing>
        <IsCachable>false</IsCachable>
        <MaxShallowRefinementHits>100</MaxShallowRefinementHits>
        <MaxSummaryLength>185</MaxSummaryLength>
        <MaxUrlLength>2048</MaxUrlLength>
        <SimilarType>None</SimilarType>
        <SortSimilar>true</SortSimilar>
        <TrimDuplicatesIncludeId>0</TrimDuplicatesIncludeId>
        <TrimDuplicatesKeepCount>1</TrimDuplicatesKeepCount>
    </QueryProperties>
    <WhiteList xmlns:a="http://schemas.microsoft.com/2003/10/Serialization/Arrays">
        <a:string>RowLimit</a:string>
        <a:string>SortList</a:string>
        <a:string>StartRow</a:string>
        <a:string>RefinementFilters</a:string>
        <a:string>Culture</a:string>
        <a:string>RankingModelId</a:string>
        <a:string>TrimDuplicatesIncludeId</a:string>
        <a:string>ReorderingRules</a:string>
        <a:string>EnableQueryRules</a:string>
        <a:string>HiddenConstraints</a:string>
        <a:string>QueryText</a:string>
        <a:string>QueryTemplate</a:string>
    </WhiteList>
</QueryPropertiesTemplate>
```

4. <span data-ttu-id="c4c0c-444">Обновите элементы  _SiteId_,  _FarmId_ и _WebId_ со значениями для вашей фермы, веб-сайта и семейства сайтов публикации.</span><span class="sxs-lookup"><span data-stu-id="c4c0c-444">Update the  _SiteId_,  _FarmId_, and  _WebId_ elements with the values for your farm, website and publishing site collection.</span></span>
    
  
5. <span data-ttu-id="c4c0c-445">Сохраните queryparametertemplate.xml в библиотеку документов QueryPropertiesTemplate.</span><span class="sxs-lookup"><span data-stu-id="c4c0c-445">Save queryparametertemplate.xml to the QueryPropertiesTemplate document library.</span></span>
    
  
6. <span data-ttu-id="c4c0c-446">Добавьте параметр  _QueryTemplatePropertiesUrl_ в свой вызов поиска REST, указав в качестве значенияspfile://webroot/queryparametertemplate.xml.</span><span class="sxs-lookup"><span data-stu-id="c4c0c-446">Add the  _QueryTemplatePropertiesUrl_ parameter to your Search REST call, specifyingspfile://webroot/queryparametertemplate.xml as the value.</span></span>
    
  

### <a name="queryparametertemplatexml-file"></a><span data-ttu-id="c4c0c-447">queryparametertemplate.xml file</span><span class="sxs-lookup"><span data-stu-id="c4c0c-447">queryparametertemplate.xml file</span></span>

<span data-ttu-id="c4c0c-448">Основными элементами в файле queryparametertemplate.xml являются:</span><span class="sxs-lookup"><span data-stu-id="c4c0c-448">The primary elements in the queryparametertemplate.xml file are:</span></span>
  
    
    

- <span data-ttu-id="c4c0c-449">Элемент **QueryProperties**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-449">**QueryProperties** element</span></span>
  
    
    
<span data-ttu-id="c4c0c-450">Содержит сериализованный объект  [QueryProperties](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.QueryProperties.aspx) .</span><span class="sxs-lookup"><span data-stu-id="c4c0c-450">Contains a serialized  [QueryProperties](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.QueryProperties.aspx) object.</span></span>
    
  
- <span data-ttu-id="c4c0c-451">Элемент **WhiteList**</span><span class="sxs-lookup"><span data-stu-id="c4c0c-451">**WhiteList** element</span></span>
  
    
    
<span data-ttu-id="c4c0c-452">Содержит список свойств запроса, которые разрешено устанавливать анонимным пользователям.</span><span class="sxs-lookup"><span data-stu-id="c4c0c-452">Contains the list of query properties that the anonymous user is allowed to set.</span></span>
    
  
<span data-ttu-id="c4c0c-p132">При отправке анонимного запроса поиска REST создается объект запроса с использованием значения, указанного в элементе **QueryProperties**. Затем все свойства, перечисленные в whitelist, копируются из входящего запроса в только что созданный объект запроса.</span><span class="sxs-lookup"><span data-stu-id="c4c0c-p132">When an anonymous Search REST query is submitted, the query object is constructed using what's specified in the **QueryProperties** element. Then, all the properties that are listed in the whitelist are copied from the incoming query to the newly constructed query object.</span></span>
  
    
    

## <a name="in-this-section"></a><span data-ttu-id="c4c0c-455">В этом разделе:</span><span class="sxs-lookup"><span data-stu-id="c4c0c-455">In this section</span></span>
<span data-ttu-id="c4c0c-456"><a name="bk_AnonymousREST"> </a></span><span class="sxs-lookup"><span data-stu-id="c4c0c-456"></span></span>

-  [<span data-ttu-id="c4c0c-457">Получение предложений запроса, с помощью службы Search REST</span><span class="sxs-lookup"><span data-stu-id="c4c0c-457">Retrieving query suggestions using the Search REST service</span></span>](retrieving-query-suggestions-using-the-search-rest-service.md)
    
  

## <a name="additional-resources"></a><span data-ttu-id="c4c0c-458">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="c4c0c-458">Additional resources</span></span>
<span data-ttu-id="c4c0c-459"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="c4c0c-459"></span></span>


-  [<span data-ttu-id="c4c0c-460">Поиск в SharePoint</span><span class="sxs-lookup"><span data-stu-id="c4c0c-460">Search in SharePoint</span></span>](search-in-sharepoint.md)
    
  
-  [<span data-ttu-id="c4c0c-461">SharePoint: использование службы поиска REST в приложении для SharePoint</span><span class="sxs-lookup"><span data-stu-id="c4c0c-461">SharePoint: Using the search REST service from an app for SharePoint</span></span>](http://code.msdn.microsoft.com/sharepoint/SharePoint-Perform-a-1bf3e87d)
    
  
-  [<span data-ttu-id="c4c0c-462">Новые возможности поиска в SharePoint для разработчиков (en)</span><span class="sxs-lookup"><span data-stu-id="c4c0c-462">What's new in SharePoint search for developers</span></span>](what-s-new-in-sharepoint-search-for-developers.md)
    
  
-  [<span data-ttu-id="c4c0c-463">Программирование с использованием службы SharePoint REST</span><span class="sxs-lookup"><span data-stu-id="c4c0c-463">Use OData query operations in SharePoint REST requests</span></span>](http://msdn.microsoft.com/library/d4b5c277-ed50-420c-8a9b-860342284b72%28Office.15%29.aspx)
    
  

  
    
    

