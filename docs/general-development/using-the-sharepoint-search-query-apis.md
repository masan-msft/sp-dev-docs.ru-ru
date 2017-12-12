---
title: "Использование API поисковых запросов SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: ae9d73ed-1140-430b-9287-01dbbe8ae7d1
ms.openlocfilehash: 4e706bbc5c685ba637f6b02d4eb748de8889d6fb
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="using-the-sharepoint-search-query-apis"></a>Использование API поисковых запросов SharePoint
Узнайте, какие API-интерфейсов запросов в SharePoint позволяют добавлять возможности поиска в пользовательские решения и приложения. 
## <a name="sharepoint-query-apis"></a>API-интерфейсы запросов SharePoint
<a name="bk_QueryAPIs"> </a>

Поиск в SharePoint предусматривает несколько интерфейсов API запроса, которые предоставляют множество способов доступа к результатам поиска, чтобы вы могли вернуть различные типы пользовательских решений.
  
    
    
Помимо серверной объектной модели, доступной в предыдущих версиях SharePoint, Поиск в SharePoint также предоставляет:
  
    
    

- клиентскую объектную модель (CSOM);
    
  
- объектную модель JavaScript (JSOM);
    
  
- службу передачи репрезентативного состояния (REST).
    
  
В таблице 1 приведены API-интерфейсы, которые можно использовать для программируемых запросов, а также путь к исходному файлу на сервере.
  
    
    

**Таблица 1. Поисковые интерфейсы API**


|**Имя API**|**Библиотека или схема классов и путь**|
|:-----|:-----|
|.NET CSOM  <br/> |Microsoft.SharePoint.Client.Search.dll <br/>%ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\ISAPI  <br/> |
|Silverlight CSOM  <br/> |Microsoft.SharePoint.Client.Search.Silverlight.dll <br/>%ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\TEMPLATE\\LAYOUTS\\ClientBin  <br/> |
|JavaScript CSOM  <br/> |SP.search.js <br/>%ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\TEMPLATE\\LAYOUTS  <br/> |
|Конечные точки службы REST  <br/> |http://server/_api/search/query <br/>http://server/_api/search/suggest  <br/> |
|Объектная модель сервера  <br/> |Microsoft.Office.Server.Search.dll <br/>%ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\ISAPI  <br/> |
   
Согласно передовой практике в разработке SharePoint используйте клиентские интерфейсы API, когда это возможно. Клиентские интерфейсы API включают клиентские объектные модели .NET, Silverlight, Phone и JavaScript и службу REST. Более подробную информацию об интерфейсах API в SharePoint и их использовании можно узнать в статье  [Выбор правильного набора API в SharePoint](choose-the-right-api-set-in-sharepoint.md).
  
    
    

### <a name="query-using-the-net-client-object-model"></a>Запросы с использованием клиентской объектной модели .NET
<a name="bk_QueryNETcsom"> </a>

В Поиск в SharePoint реализована клиентская объектная модель, предоставляющая доступ к результатам поиска для разработки веб-приложений, локальных и мобильных приложений. CSOM Поиск в SharePoint основана на CSOM SharePoint. Поэтому клиентскому коду сначала нужно получить доступ к CSOM SharePoint, а затем  к CSOM Поиск в SharePoint. Дополнительные сведения о клиентской объектной модели SharePoint см. в статье  [Управляемая клиентская объектная модель](http://msdn.microsoft.com/library/8c086b11-2b8b-41ec-82ae-cd4fef0aeac6%28Office.15%29.aspx). Дополнительные сведения о классе  [ClientContext](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.ClientContext.aspx) , который служит точкой входа в CSOM, см. в статье [Контекст клиента как центральный объект](http://msdn.microsoft.com/library/6299f0df-ab4c-40e6-b709-ec80271c99b3%28Office.15%29.aspx).
  
    
    
При использовании управляемой CSOM .NET получите экземпляр **ClientContext** (расположен в пространстве имен [Microsoft.SharePoint.Client](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.aspx) в библиотеке Microsoft.SharePoint.Client.dll). Затем используйте объектную модель в пространстве имен **Microsoft.SharePoint.Search.Client.Query** из библиотеки Microsoft.SharePoint.Search.Client.dll.
  
    
    
Вот простой пример.
  
    
    



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

Чтобы скачать пример, изучите следующий пример кода, опубликованный  [Кори Ротом](http://mvp.microsoft.com/ru-RU/mvp/Corey%20Roth-4029260), специалистом MVP по SharePoint:  [SharePoint: поисковый с помощью управляемой клиентской объектной модели](http://code.msdn.microsoft.com/Query-Search-with-the-649f1bc1).
  
    
    

### <a name="query-using-the-javascript-client-object-model"></a>Запросы с использованием клиентской объектной модели JavaScript
<a name="bk_QueryJSOM"> </a>

Для клиентской объектной модели JavaScript получите экземпляр  [ClientContext](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.ClientContext.aspx) , а затем используйте объектную модель в файле SP.Search.js.
  
    
    
Вот простой пример.
  
    
    



```

var clientContext = new SP.ClientContext("<serverRelativeUrl>");
var contextSite = clientContext.get_site();
var keywordQuery = new Microsoft.SharePoint.Client.Search.Query.KeywordQuery(clientContext); 
keywordQuery.set_queryText("SharePoint"); 
var searchExecutor = new Microsoft.SharePoint.Client.Search.Query.SearchExecutor(clientContext);  
var results = searchExecutor.executeQuery(keywordQuery); 
context.executeQueryAsync(onQuerySuccess, onQueryError);
```

Чтобы скачать пример, изучите следующий пример кода, опубликованный  [Кори Ротом](http://mvp.microsoft.com/ru-RU/mvp/Corey%20Roth-4029260), специалистом MVP по SharePoint:  [SharePoint: поисковый запрос с помощью клиентской объектной модели JavaScript](http://code.msdn.microsoft.com/SharePoint-Querying-a629b53b).
  
    
    

### <a name="query-using-the-rest-service"></a>Запросы с использованием службы REST
<a name="bk_QueryREST"> </a>

SharePoint предоставляет службу REST, которая позволяет удаленно выполнять запросы к службе поиска SharePoint из клиентских приложений, используя любые технологии, поддерживающие веб-запросы REST. Служба REST поиска предоставляет две конечных точки, **query** и **suggest**, и поддерживает операции **GET** и **POST**. Результаты возвращаются в формате XML или Нотация объектов JavaScript (JSON).
  
    
    
Далее показана точка доступа для службы:  `http://server/_api/search/`. Вы также можете указать сайт в URL-адресе следующим образом:  `http://server/site/_api/search/`. Служба поиска возвращает результаты из всего семейства веб-сайтов, поэтому для обоих методов доступа к службе возвращаются одинаковые результаты.
  
    
    
Подробнее см. в статьях  [Общие сведения об API службы поиска REST для SharePoint](sharepoint-search-rest-api-overview.md) и [Получение предложений запроса, с помощью службы Search REST](retrieving-query-suggestions-using-the-search-rest-service.md).
  
    
    

### <a name="query-using-the-net-server-object-model"></a>Запросы с использованием серверной объектной модели .NET
<a name="bk_QuerySOM"> </a>

Приложения, использующие серверную объектную модель, должны выполняться непосредственно на сервере, где запущен SharePoint. Серверная объектная модель поисковых запросов размещена в пространстве имен  [Microsoft.Office.Server.Search.Query](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.aspx) в библиотеке Microsoft.Office.Server.Search.dll.
  
    
    
Как и в SharePoint Server 2010, вы используете класс  **KeywordQuery** , чтобы определить запрос, а затем вызываете метод [Execute()](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.Query.Execute.aspx) , чтобы отправить запрос. В SharePoint метод **Execute** по-прежнему работает, но считается устаревшим, поэтому следует использовать класс [SearchExecutor](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.SearchExecutor.aspx) . Чтобы отправить запрос, вызовите метод [ExecuteQuery()](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.SearchExecutor.ExecuteQuery.aspx) , передав экземпляр класса **KeywordQuery** в вызове.
  
    
    
Вот простой пример.
  
    
    



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

Чтобы скачать пример, изучите следующий пример кода, опубликованный  [Кори Ротом](http://mvp.microsoft.com/ru-RU/mvp/Corey%20Roth-4029260), специалистом MVP по SharePoint:  [SharePoint: поисковый запрос с помощью класса KeywordQuery](http://code.msdn.microsoft.com/Query-Search-with-the-372139b5).
  
    
    

## <a name="see-also"></a>См. также
<a name="bk_addresources"> </a>


-  [Построение запросов поиска в SharePoint](building-search-queries-in-sharepoint.md)
    
  
-  [Общие сведения об API службы поиска REST для SharePoint](sharepoint-search-rest-api-overview.md)
    
  
-  [SharePoint: использование службы поиска REST в приложении для SharePoint](http://code.msdn.microsoft.com/sharepoint/SharePoint-Perform-a-1bf3e87d)
    
  

  
    
    
