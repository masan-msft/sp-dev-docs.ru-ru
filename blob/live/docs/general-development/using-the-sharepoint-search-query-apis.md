---
title: "Использование API поисковых запросов SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: ae9d73ed-1140-430b-9287-01dbbe8ae7d1
ms.openlocfilehash: 1a68b192b9b27040b68f8f4a5b95e3711ba57ba5
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="using-the-sharepoint-search-query-apis"></a><span data-ttu-id="84ca5-102">Использование API поисковых запросов SharePoint</span><span class="sxs-lookup"><span data-stu-id="84ca5-102">Using the SharePoint search Query APIs</span></span>
<span data-ttu-id="84ca5-103">Узнайте, какие API-интерфейсов запросов в SharePoint позволяют добавлять возможности поиска в пользовательские решения и приложения.</span><span class="sxs-lookup"><span data-stu-id="84ca5-103">Learn about the query APIs available in SharePoint that enable you to add search functionality to custom solutions and applications.</span></span> 
## <a name="sharepoint-query-apis"></a><span data-ttu-id="84ca5-104">API-интерфейсы запросов SharePoint</span><span class="sxs-lookup"><span data-stu-id="84ca5-104">SharePoint Query APIs</span></span>
<span data-ttu-id="84ca5-105"><a name="bk_QueryAPIs"> </a></span><span class="sxs-lookup"><span data-stu-id="84ca5-105"></span></span>

<span data-ttu-id="84ca5-106">Поиск в SharePoint предусматривает несколько интерфейсов API запроса, которые предоставляют множество способов доступа к результатам поиска, чтобы вы могли вернуть различные типы пользовательских решений.</span><span class="sxs-lookup"><span data-stu-id="84ca5-106">Search in SharePoint provides several query APIs, giving you lots of ways to access search results, so that you can return search results in a variety of custom solution types.</span></span>
  
    
    
<span data-ttu-id="84ca5-107">Помимо серверной объектной модели, доступной в предыдущих версиях SharePoint, Поиск в SharePoint также предоставляет:</span><span class="sxs-lookup"><span data-stu-id="84ca5-107">In addition to the server object model that was available in previous versions of SharePoint, Search in SharePoint also provides the following:</span></span>
  
    
    

- <span data-ttu-id="84ca5-108">клиентскую объектную модель (CSOM);</span><span class="sxs-lookup"><span data-stu-id="84ca5-108">Client object model (CSOM)</span></span>
    
  
- <span data-ttu-id="84ca5-109">объектную модель JavaScript (JSOM);</span><span class="sxs-lookup"><span data-stu-id="84ca5-109">JavaScript object model (JSOM)</span></span>
    
  
- <span data-ttu-id="84ca5-110">службу передачи репрезентативного состояния (REST).</span><span class="sxs-lookup"><span data-stu-id="84ca5-110">Representational State Transfer (REST) service</span></span>
    
  
<span data-ttu-id="84ca5-111">В таблице 1 приведены API-интерфейсы, которые можно использовать для программируемых запросов, а также путь к исходному файлу на сервере.</span><span class="sxs-lookup"><span data-stu-id="84ca5-111">Table 1 shows the APIs that you can use to program search queries and the path to the source file on the server.</span></span>
  
    
    

<span data-ttu-id="84ca5-112">**Таблица 1. Поисковые интерфейсы API**</span><span class="sxs-lookup"><span data-stu-id="84ca5-112">**Table 1. Search APIs**</span></span>


|<span data-ttu-id="84ca5-113">**Имя API**</span><span class="sxs-lookup"><span data-stu-id="84ca5-113">**API name**</span></span>|<span data-ttu-id="84ca5-114">**Библиотека или схема классов и путь**</span><span class="sxs-lookup"><span data-stu-id="84ca5-114">**Class library or schema and path**</span></span>|
|:-----|:-----|
|<span data-ttu-id="84ca5-115">.NET CSOM</span><span class="sxs-lookup"><span data-stu-id="84ca5-115">.NET CSOM</span></span>  <br/> |<span data-ttu-id="84ca5-116">Microsoft.SharePoint.Client.Search.dll</span><span class="sxs-lookup"><span data-stu-id="84ca5-116">Microsoft.SharePoint.Client.Search.dll          %ProgramFiles%Common FilesMicrosoft Sharedweb server extensions15ISAPI</span></span> <br/><span data-ttu-id="84ca5-117">%ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\ISAPI</span><span class="sxs-lookup"><span data-stu-id="84ca5-117">Microsoft.SharePoint.Client.Search.dll          %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\ISAPI</span></span>  <br/> |
|<span data-ttu-id="84ca5-118">Silverlight CSOM</span><span class="sxs-lookup"><span data-stu-id="84ca5-118">Silverlight CSOM</span></span>  <br/> |<span data-ttu-id="84ca5-119">Microsoft.SharePoint.Client.Search.Silverlight.dll</span><span class="sxs-lookup"><span data-stu-id="84ca5-119">Microsoft.SharePoint.Client.Search.Silverlight.dll          %ProgramFiles%Common FilesMicrosoft Sharedweb server extensions15TEMPLATELAYOUTSClientBin</span></span> <br/><span data-ttu-id="84ca5-120">%ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\TEMPLATE\\LAYOUTS\\ClientBin</span><span class="sxs-lookup"><span data-stu-id="84ca5-120">Microsoft.SharePoint.Client.Search.Silverlight.dll          %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\TEMPLATE\\LAYOUTS\\ClientBin</span></span>  <br/> |
|<span data-ttu-id="84ca5-121">JavaScript CSOM</span><span class="sxs-lookup"><span data-stu-id="84ca5-121">JavaScript CSOM</span></span>  <br/> |<span data-ttu-id="84ca5-122">SP.search.js</span><span class="sxs-lookup"><span data-stu-id="84ca5-122">SP.search.js</span></span> <br/><span data-ttu-id="84ca5-123">%ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\TEMPLATE\\LAYOUTS</span><span class="sxs-lookup"><span data-stu-id="84ca5-123">SP.search.js          %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\TEMPLATE\\LAYOUTS</span></span>  <br/> |
|<span data-ttu-id="84ca5-124">Конечные точки службы REST</span><span class="sxs-lookup"><span data-stu-id="84ca5-124">REST service endpoints</span></span>  <br/> |<span data-ttu-id="84ca5-125">http://server/_api/search/query</span><span class="sxs-lookup"><span data-stu-id="84ca5-125">http://server/_api/search/query</span></span> <br/><span data-ttu-id="84ca5-126">http://server/_api/search/suggest</span><span class="sxs-lookup"><span data-stu-id="84ca5-126">http://server/_api/search/queryhttp://server/_api/search/suggest</span></span>  <br/> |
|<span data-ttu-id="84ca5-127">Объектная модель сервера</span><span class="sxs-lookup"><span data-stu-id="84ca5-127">Server object model</span></span>  <br/> |<span data-ttu-id="84ca5-128">Microsoft.Office.Server.Search.dll</span><span class="sxs-lookup"><span data-stu-id="84ca5-128">Microsoft.Office.Server.Search.dll</span></span> <br/><span data-ttu-id="84ca5-129">%ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\ISAPI</span><span class="sxs-lookup"><span data-stu-id="84ca5-129">Microsoft.Office.Server.Search.dll          %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\ISAPI</span></span>  <br/> |
   
<span data-ttu-id="84ca5-p101">Согласно передовой практике в разработке SharePoint используйте клиентские интерфейсы API, когда это возможно. Клиентские интерфейсы API включают клиентские объектные модели .NET, Silverlight, Phone и JavaScript и службу REST. Более подробную информацию об интерфейсах API в SharePoint и их использовании можно узнать в статье  [Выбор правильного набора API в SharePoint](choose-the-right-api-set-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="84ca5-p101">As a best practice in SharePoint development, use client APIs when you can. Client APIs include the .NET, Silverlight, Phone, and JavaScript client object models, and the REST service. For more information about the APIs in SharePoint and when to use them, see  [Choose the right API set in SharePoint](choose-the-right-api-set-in-sharepoint.md).</span></span>
  
    
    

### <a name="query-using-the-net-client-object-model"></a><span data-ttu-id="84ca5-133">Запросы с использованием клиентской объектной модели .NET</span><span class="sxs-lookup"><span data-stu-id="84ca5-133">Query using the .NET client object model</span></span>
<span data-ttu-id="84ca5-134"><a name="bk_QueryNETcsom"> </a></span><span class="sxs-lookup"><span data-stu-id="84ca5-134"></span></span>

<span data-ttu-id="84ca5-p102">В Поиск в SharePoint реализована клиентская объектная модель, предоставляющая доступ к результатам поиска для разработки веб-приложений, локальных и мобильных приложений. CSOM Поиск в SharePoint основана на CSOM SharePoint. Поэтому клиентскому коду сначала нужно получить доступ к CSOM SharePoint, а затем  к CSOM Поиск в SharePoint. Дополнительные сведения о клиентской объектной модели SharePoint см. в статье  [Управляемая клиентская объектная модель](http://msdn.microsoft.com/library/8c086b11-2b8b-41ec-82ae-cd4fef0aeac6%28Office.15%29.aspx). Дополнительные сведения о классе  [ClientContext](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.ClientContext.aspx) , который служит точкой входа в CSOM, см. в статье [Контекст клиента как центральный объект](http://msdn.microsoft.com/library/6299f0df-ab4c-40e6-b709-ec80271c99b3%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="84ca5-p102">Search in SharePoint includes a client object model that enables access to search results for online, on-premises, and mobile development. The Search in SharePoint CSOM is built on the SharePoint CSOM. Therefore, your client code first needs to access the SharePoint CSOM and then access the Search in SharePoint CSOM. For more information about the SharePoint CSOM, see  [SharePoint 2010 Client Object Model](http://msdn.microsoft.com/library/8c086b11-2b8b-41ec-82ae-cd4fef0aeac6%28Office.15%29.aspx). For more information about the  [ClientContext](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.ClientContext.aspx) class, which is the entry point to the CSOM, see [Client Context as Central Object](http://msdn.microsoft.com/library/6299f0df-ab4c-40e6-b709-ec80271c99b3%28Office.15%29.aspx).</span></span>
  
    
    
<span data-ttu-id="84ca5-p103">При использовании управляемой CSOM .NET получите экземпляр **ClientContext** (расположен в пространстве имен [Microsoft.SharePoint.Client](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.aspx) в библиотеке Microsoft.SharePoint.Client.dll). Затем используйте объектную модель в пространстве имен **Microsoft.SharePoint.Search.Client.Query** из библиотеки Microsoft.SharePoint.Search.Client.dll.</span><span class="sxs-lookup"><span data-stu-id="84ca5-p103">For the .NET managed CSOM, get a **ClientContext** instance (located in the [Microsoft.SharePoint.Client](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.aspx) namespace in the Microsoft.SharePoint.Client.dll). Then use the object model in the **Microsoft.SharePoint.Search.Client.Query** namespace in the Microsoft.SharePoint.Search.Client.dll.</span></span>
  
    
    
<span data-ttu-id="84ca5-142">Вот простой пример.</span><span class="sxs-lookup"><span data-stu-id="84ca5-142">Here's a basic example.</span></span>
  
    
    



```cs

using (ClientContext clientContext = new ClientContext("http://<serverName>/sites/<siteCollectionPath>"))
{
    KeywordQuery keywordQuery = new KeywordQuery(clientContext);
    keywordQuery.QueryText = "SharePoint";
    SearchExecutor searchExecutor = new SearchExecutor(clientContext);
    ClientResult<ResultTableCollection> results = searchExecutor.ExecuteQuery(keywordQuery);
    clientContext.ExecuteQuery();
}
```

<span data-ttu-id="84ca5-143">Чтобы скачать пример, изучите следующий пример кода, опубликованный  [Кори Ротом](http://mvp.microsoft.com/en-us/mvp/Corey%20Roth-4029260), специалистом MVP по SharePoint:  [SharePoint: поисковый с помощью управляемой клиентской объектной модели](http://code.msdn.microsoft.com/Query-Search-with-the-649f1bc1).</span><span class="sxs-lookup"><span data-stu-id="84ca5-143">To download an example, see the following code sample posted by SharePoint MVP  [Corey Roth](http://mvp.microsoft.com/en-us/mvp/Corey%20Roth-4029260):  [SharePoint: Query Search with the Managed Client Object Model](http://code.msdn.microsoft.com/Query-Search-with-the-649f1bc1).</span></span>
  
    
    

### <a name="query-using-the-javascript-client-object-model"></a><span data-ttu-id="84ca5-144">Запросы с использованием клиентской объектной модели JavaScript</span><span class="sxs-lookup"><span data-stu-id="84ca5-144">Query using the JavaScript client object model</span></span>
<span data-ttu-id="84ca5-145"><a name="bk_QueryJSOM"> </a></span><span class="sxs-lookup"><span data-stu-id="84ca5-145"></span></span>

<span data-ttu-id="84ca5-146">Для клиентской объектной модели JavaScript получите экземпляр  [ClientContext](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.ClientContext.aspx) , а затем используйте объектную модель в файле SP.Search.js.</span><span class="sxs-lookup"><span data-stu-id="84ca5-146">For the JavaScript CSOM, get a  [ClientContext](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.ClientContext.aspx) instance, and then use the object model in the SP.Search.js file.</span></span>
  
    
    
<span data-ttu-id="84ca5-147">Вот простой пример.</span><span class="sxs-lookup"><span data-stu-id="84ca5-147">Here's a basic example.</span></span>
  
    
    



```

var clientContext = new SP.ClientContext("<serverRelativeUrl>");
var contextSite = clientContext.get_site();
var keywordQuery = new Microsoft.SharePoint.Client.Search.Query.KeywordQuery(clientContext); 
keywordQuery.set_queryText("SharePoint"); 
var searchExecutor = new Microsoft.SharePoint.Client.Search.Query.SearchExecutor(clientContext);  
var results = searchExecutor.executeQuery(keywordQuery); 
context.executeQueryAsync(onQuerySuccess, onQueryError);
```

<span data-ttu-id="84ca5-148">Чтобы скачать пример, изучите следующий пример кода, опубликованный  [Кори Ротом](http://mvp.microsoft.com/en-us/mvp/Corey%20Roth-4029260), специалистом MVP по SharePoint:  [SharePoint: поисковый запрос с помощью клиентской объектной модели JavaScript](http://code.msdn.microsoft.com/SharePoint-Querying-a629b53b).</span><span class="sxs-lookup"><span data-stu-id="84ca5-148">To download an example, see the following code sample posted by SharePoint MVP  [Corey Roth](http://mvp.microsoft.com/en-us/mvp/Corey%20Roth-4029260):  [SharePoint: Querying Search with the JavaScript Client Object Model](http://code.msdn.microsoft.com/SharePoint-Querying-a629b53b).</span></span>
  
    
    

### <a name="query-using-the-rest-service"></a><span data-ttu-id="84ca5-149">Запросы с использованием службы REST</span><span class="sxs-lookup"><span data-stu-id="84ca5-149">Query using the REST service</span></span>
<span data-ttu-id="84ca5-150"><a name="bk_QueryREST"> </a></span><span class="sxs-lookup"><span data-stu-id="84ca5-150"></span></span>

<span data-ttu-id="84ca5-p104">SharePoint предоставляет службу REST, которая позволяет удаленно выполнять запросы к службе поиска SharePoint из клиентских приложений, используя любые технологии, поддерживающие веб-запросы REST. Служба REST поиска предоставляет две конечных точки, **query** и **suggest**, и поддерживает операции **GET** и **POST**. Результаты возвращаются в формате XML или Нотация объектов JavaScript (JSON).</span><span class="sxs-lookup"><span data-stu-id="84ca5-p104">SharePoint includes a REST service that enables you to remotely execute queries against the SharePoint Search service from client applications by using any technology that supports REST web requests. The Search REST service exposes two endpoints, **query** and **suggest**, and will support both **GET** and **POST** operations. Results are returned in either XML or JavaScript Object Notation (JSON) format.</span></span>
  
    
    
<span data-ttu-id="84ca5-p105">Далее показана точка доступа для службы:  `http://server/_api/search/`. Вы также можете указать сайт в URL-адресе следующим образом:  `http://server/site/_api/search/`. Служба поиска возвращает результаты из всего семейства веб-сайтов, поэтому для обоих методов доступа к службе возвращаются одинаковые результаты.</span><span class="sxs-lookup"><span data-stu-id="84ca5-p105">The following is the access point for the service:  `http://server/_api/search/`. You can also specify the site in the URL, as follows:  `http://server/site/_api/search/`. The search service returns results from the entire site collection, so the same results are returned for both ways to access the service.</span></span>
  
    
    
<span data-ttu-id="84ca5-157">Подробнее см. в статьях  [Общие сведения об API службы поиска REST для SharePoint](sharepoint-search-rest-api-overview.md) и [Получение предложений запроса, с помощью службы Search REST](retrieving-query-suggestions-using-the-search-rest-service.md).</span><span class="sxs-lookup"><span data-stu-id="84ca5-157">See  [SharePoint Search REST API overview](sharepoint-search-rest-api-overview.md) and [Retrieving query suggestions using the Search REST service](retrieving-query-suggestions-using-the-search-rest-service.md) for more information.</span></span>
  
    
    

### <a name="query-using-the-net-server-object-model"></a><span data-ttu-id="84ca5-158">Запросы с использованием серверной объектной модели .NET</span><span class="sxs-lookup"><span data-stu-id="84ca5-158">Query using the .NET server object model</span></span>
<span data-ttu-id="84ca5-159"><a name="bk_QuerySOM"> </a></span><span class="sxs-lookup"><span data-stu-id="84ca5-159"></span></span>

<span data-ttu-id="84ca5-p106">Приложения, использующие серверную объектную модель, должны выполняться непосредственно на сервере, где запущен SharePoint. Серверная объектная модель поисковых запросов размещена в пространстве имен  [Microsoft.Office.Server.Search.Query](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.aspx) в библиотеке Microsoft.Office.Server.Search.dll.</span><span class="sxs-lookup"><span data-stu-id="84ca5-p106">Applications that use the server object model must run directly on a server that is running SharePoint. The search Query server object model resides in the  [Microsoft.Office.Server.Search.Query](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.aspx) namespace, which is located in Microsoft.Office.Server.Search.dll.</span></span>
  
    
    
<span data-ttu-id="84ca5-p107">Как и в SharePoint Server 2010, вы используете класс  **KeywordQuery** , чтобы определить запрос, а затем вызываете метод [Execute()](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.Query.Execute.aspx) , чтобы отправить запрос. В SharePoint метод **Execute** по-прежнему работает, но считается устаревшим, поэтому следует использовать класс [SearchExecutor](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.SearchExecutor.aspx) . Чтобы отправить запрос, вызовите метод [ExecuteQuery()](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.SearchExecutor.ExecuteQuery.aspx) , передав экземпляр класса **KeywordQuery** в вызове.</span><span class="sxs-lookup"><span data-stu-id="84ca5-p107">As in SharePoint Server 2010, you use the  **KeywordQuery** class to define the query, and then called the [Execute()](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.Query.Execute.aspx) method to submit the query. In SharePoint, the **Execute** method is obsolete, and while it will still work, you should use the [SearchExecutor](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.SearchExecutor.aspx) class instead. To submit the query, call the [ExecuteQuery()](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.SearchExecutor.ExecuteQuery.aspx) method, passing the instance of the **KeywordQuery** class in the call.</span></span>
  
    
    
<span data-ttu-id="84ca5-165">Вот простой пример.</span><span class="sxs-lookup"><span data-stu-id="84ca5-165">Here's a basic example.</span></span>
  
    
    



```cs

using (SPSite siteCollection = new SPSite("<serverRelativeUrl>"))
{
    KeywordQuery keywordQuery = new KeywordQuery(siteCollection);
    keywordQuery.QueryText = "SharePoint";
    SearchExecutor searchExecutor = new SearchExecutor(); 
    ResultTableCollection resultTableCollection = searchExecutor.ExecuteQuery(keywordQuery); 
    resultTableCollection = resultTableCollection.Filter("TableType", KnownTableTypes.RelevantResults); 
    ResultTable resultTable = resultTableCollection.FirstOrDefault(); 
    DataTable dataTable = resultTable.Table; 
}
```

<span data-ttu-id="84ca5-166">Чтобы скачать пример, изучите следующий пример кода, опубликованный  [Кори Ротом](http://mvp.microsoft.com/en-us/mvp/Corey%20Roth-4029260), специалистом MVP по SharePoint:  [SharePoint: поисковый запрос с помощью класса KeywordQuery](http://code.msdn.microsoft.com/Query-Search-with-the-372139b5).</span><span class="sxs-lookup"><span data-stu-id="84ca5-166">To download an example, see the following code sample posted by SharePoint MVP  [Corey Roth](http://mvp.microsoft.com/en-us/mvp/Corey%20Roth-4029260):  [SharePoint: Query Search with the KeywordQuery Class](http://code.msdn.microsoft.com/Query-Search-with-the-372139b5).</span></span>
  
    
    

## <a name="additional-resources"></a><span data-ttu-id="84ca5-167">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="84ca5-167">Additional resources</span></span>
<span data-ttu-id="84ca5-168"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="84ca5-168"></span></span>


-  [<span data-ttu-id="84ca5-169">Построение запросов поиска в SharePoint</span><span class="sxs-lookup"><span data-stu-id="84ca5-169">Building search queries in SharePoint</span></span>](building-search-queries-in-sharepoint.md)
    
  
-  [<span data-ttu-id="84ca5-170">Общие сведения об API службы поиска REST для SharePoint</span><span class="sxs-lookup"><span data-stu-id="84ca5-170">SharePoint Search REST API overview</span></span>](sharepoint-search-rest-api-overview.md)
    
  
-  [<span data-ttu-id="84ca5-171">SharePoint: использование службы поиска REST в приложении для SharePoint</span><span class="sxs-lookup"><span data-stu-id="84ca5-171">SharePoint: Using the search REST service from an app for SharePoint</span></span>](http://code.msdn.microsoft.com/sharepoint/SharePoint-Perform-a-1bf3e87d)
    
  

  
    
    
