---
title: "Новые возможности поиска SharePoint для разработчиков (en)"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: b8d69685-3612-421e-b011-50b4d580d461
ms.openlocfilehash: aa3e8633312ee6fa814a7e9bb0152d131e30b799
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="whats-new-in-sharepoint-search-for-developers"></a><span data-ttu-id="93c75-102">Новые возможности поиска SharePoint для разработчиков (en)</span><span class="sxs-lookup"><span data-stu-id="93c75-102">What's new in SharePoint search for developers</span></span>
<span data-ttu-id="93c75-103">Узнайте о новых возможностях для разработчиков в системе поиска в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="93c75-103">Learn about the new features available for developers in Search in SharePoint.</span></span>
## <a name="search-client-object-model-for-access-to-query-object-model-functionality-for-online-on-premises-and-mobile-development"></a><span data-ttu-id="93c75-104">Поиск клиентской объектной модели для доступа к Интернет-версия функциональные возможности модели объектов для запроса, в локальной и разработке для мобильных устройств</span><span class="sxs-lookup"><span data-stu-id="93c75-104">Search client object model for access to Query object model functionality for online, on-premises, and mobile development</span></span>
<span data-ttu-id="93c75-105"><a name="SPSearchnew_clientOM"> </a></span><span class="sxs-lookup"><span data-stu-id="93c75-105"></span></span>

<span data-ttu-id="93c75-106">Поиск SharePoint включает клиентская объектная модель (CSOM), которая обеспечивает доступ к большую часть функциональных возможностей объектной модели запросов для Интернет-версия, локальной и разработки для мобильных устройств.</span><span class="sxs-lookup"><span data-stu-id="93c75-106">SharePoint Search includes a client object model (CSOM) that enables access to most of the Query object model functionality for online, on-premises, and mobile development.</span></span> <span data-ttu-id="93c75-107">CSOM поиска можно использовать для создания клиентских приложений, работающих на компьютере, который не имеет SharePoint, установленные для возврата результатов поиска SharePoint.</span><span class="sxs-lookup"><span data-stu-id="93c75-107">You can use the Search CSOM to create client applications that run on a machine that does not have SharePoint installed to return SharePoint search results.</span></span>
  
    
    
<span data-ttu-id="93c75-108">CSOM поиска включает Microsoft .NET Framework управляемой клиентской объектной модели и объектной модели JavaScript, а построен на SharePoint.</span><span class="sxs-lookup"><span data-stu-id="93c75-108">The Search CSOM includes a Microsoft .NET Framework managed client object model and JavaScript object model, and it is built on SharePoint.</span></span> <span data-ttu-id="93c75-109">Во-первых клиентский код получает доступ к SharePoint CSOM.</span><span class="sxs-lookup"><span data-stu-id="93c75-109">First, client code accesses the SharePoint CSOM.</span></span> <span data-ttu-id="93c75-110">Затем код клиент обращается к CSOM поиска.</span><span class="sxs-lookup"><span data-stu-id="93c75-110">Then, client code accesses the Search CSOM.</span></span> 
  
    
    
<span data-ttu-id="93c75-p103">Чтобы использовать поиск .NET Framework управляемая клиентская объектная модель, необходимо получить экземпляр  [ClientContext](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.ClientContext.aspx) (находится в пространстве имен [Microsoft.SharePoint.Client](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.aspx) в библиотеке Microsoft.SharePoint.Client.dll). Затем можно используйте объектную модель в пространстве имен [Microsoft.SharePoint.Client.Search.Query](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Search.Query.aspx) в Microsoft.Office.Server.Search.Client.dll. Дополнительные сведения о SharePoint CSOM можно [Управляемая клиентская объектная модель](http://msdn.microsoft.com/library/8c086b11-2b8b-41ec-82ae-cd4fef0aeac6%28Office.15%29.aspx). Дополнительные сведения об объекте **ClientContext**, которая точка входа в CSOM, можно [Контекст клиента как центральный объект](http://msdn.microsoft.com/library/6299f0df-ab4c-40e6-b709-ec80271c99b3%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="93c75-p103">To use the Search .NET Framework managed CSOM, you must get a  [ClientContext](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.ClientContext.aspx) instance (located in the [Microsoft.SharePoint.Client](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.aspx) namespace in the Microsoft.SharePoint.Client.dll). Then, use the object model in the [Microsoft.SharePoint.Client.Search.Query](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Search.Query.aspx) namespace in the Microsoft.Office.Server.Search.Client.dll. For more information about the SharePoint CSOM, see [SharePoint 2010 Client Object Model](http://msdn.microsoft.com/library/8c086b11-2b8b-41ec-82ae-cd4fef0aeac6%28Office.15%29.aspx). For more information about the **ClientContext** object, which is the entry point to the CSOM, see [Client Context as Central Object](http://msdn.microsoft.com/library/6299f0df-ab4c-40e6-b709-ec80271c99b3%28Office.15%29.aspx).</span></span>
  
    
    
<span data-ttu-id="93c75-p104">CSOM поиска возвращает результаты поиска с сервера в JavaScript Object Notation (JSON). JSON для данных результатов поиска содержит коллекцию  [ResultTableCollection](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Search.Query.ResultTableCollection.aspx) состоять [ResultTable](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Search.Query.ResultTable.aspx) объектов, представляющих различных наборов записей.</span><span class="sxs-lookup"><span data-stu-id="93c75-p104">The Search CSOM returns the search results data from the server in JavaScript Object Notation (JSON). The JSON for the search results data contains a  [ResultTableCollection](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Search.Query.ResultTableCollection.aspx) collection composed of [ResultTable](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Search.Query.ResultTable.aspx) objects that represent different result sets.</span></span>
  
    
    

## <a name="sql-syntax-support-removed"></a><span data-ttu-id="93c75-117">Удалена поддержка синтаксис SQL</span><span class="sxs-lookup"><span data-stu-id="93c75-117">SQL Syntax Support Removed</span></span>
<span data-ttu-id="93c75-118"><a name="SP15Searchnew_support"> </a></span><span class="sxs-lookup"><span data-stu-id="93c75-118"></span></span>

<span data-ttu-id="93c75-119">Настраиваемые поисковые решения в SharePoint не поддерживают [синтаксис SQL](http://msdn.microsoft.com/ru-ru/library/ee558869).</span><span class="sxs-lookup"><span data-stu-id="93c75-119">Custom search solutions in SharePoint do not support  [SQL syntax](http://msdn.microsoft.com/ru-ru/library/ee558869).</span></span> <span data-ttu-id="93c75-120">Поиск в SharePoint поддерживает синтаксис FQL и KQL настраиваемые поисковые решения.</span><span class="sxs-lookup"><span data-stu-id="93c75-120">Search in SharePoint supports FQL syntax and KQL syntax for custom search solutions.</span></span> <span data-ttu-id="93c75-121">Синтаксис SQL нельзя использовать настраиваемые поисковые решения с помощью любой технологии, включая server объектной модели запросов, клиентской объектной модели и службы поиска REST.</span><span class="sxs-lookup"><span data-stu-id="93c75-121">You cannot use SQL syntax in custom search solutions using any technologies, including the Query server object model, the client object model, and the Search REST service.</span></span> <span data-ttu-id="93c75-122">Решения поиска, использующие синтаксис SQL server объектной модели запросов и веб-службы запросов, которые были созданы в более ранних версиях SharePoint Server не будет работать при обновлении в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="93c75-122">Custom search solutions that use SQL syntax with the Query server object model and the Query web service that were created in earlier versions of SharePoint Server will not work when you upgrade them to SharePoint.</span></span> <span data-ttu-id="93c75-123">Возвращает ошибку, запросов, отправленных с помощью этих приложений.</span><span class="sxs-lookup"><span data-stu-id="93c75-123">Queries submitted via these applications will return an error.</span></span> <span data-ttu-id="93c75-124">Дополнительные сведения об использовании синтаксиса FQL и KQL видеть [ссылку синтаксис ключевых слов Query Language (KQL)](keyword-query-language-kql-syntax-reference.md) и [синтаксис FAST Query Language (FQL.md)](fast-query-language-fql-syntax-reference.md).</span><span class="sxs-lookup"><span data-stu-id="93c75-124">For more information about using FQL syntax and KQL syntax, see  [Keyword Query Language (KQL) syntax reference](keyword-query-language-kql-syntax-reference.md) and [FAST Query Language (FQL.md) syntax reference](fast-query-language-fql-syntax-reference.md).</span></span>
  
    
    

## <a name="search-rest-service-for-remote-execution-of-queries-from-client-applications"></a><span data-ttu-id="93c75-125">Службы поиска REST для удаленное выполнение запросов из клиентских приложений</span><span class="sxs-lookup"><span data-stu-id="93c75-125">Search REST service for remote execution of queries from client applications</span></span>
<span data-ttu-id="93c75-126"><a name="SP15Searchnew_support"> </a></span><span class="sxs-lookup"><span data-stu-id="93c75-126"></span></span>

<span data-ttu-id="93c75-127">SharePoint включает в себя представлений состояния (REST) служба, которая позволяет удаленно выполнять запросы, направленные службы поиска SharePoint из клиентских приложений с помощью любой технологии, поддерживающей веб-запросы REST.</span><span class="sxs-lookup"><span data-stu-id="93c75-127">SharePoint includes a Representational State Transfer (REST) service that enables you to remotely execute queries against the SharePoint Search service from client applications by using any technology that supports REST web requests.</span></span> <span data-ttu-id="93c75-128">Службы поиска REST предоставляет две конечные точки, **запросов** и **Предложить**и обеспечения операции **GET** и **POST** .</span><span class="sxs-lookup"><span data-stu-id="93c75-128">The Search REST service exposes two endpoints, **query** and **suggest**, and will support both **GET** and **POST** operations.</span></span> <span data-ttu-id="93c75-129">Результаты возвращаются в формате XML или JSON.</span><span class="sxs-lookup"><span data-stu-id="93c75-129">Results are returned in either XML or JSON format.</span></span>
  
    
    
<span data-ttu-id="93c75-p107">Далее показана точка доступа для службы:  `http://server/_api/search/`. Вы также можете указать сайт в URL-адресе следующим образом:  `http://server/site/_api/search/`. Служба поиска возвращает результаты из всего семейства веб-сайтов, поэтому для обоих методов доступа к службе возвращаются одинаковые результаты.</span><span class="sxs-lookup"><span data-stu-id="93c75-p107">The following is the access point for the service:  `http://server/_api/search/`. You can also specify the site in the URL, as follows:  `http://server/site/_api/search/`. The search service returns results from the entire site collection, so the same results are returned for both ways to access the service.</span></span>
  
    
    
<span data-ttu-id="93c75-p108">Вы также можете использовать URL-адрес, который ссылается client.svc для доступа к службе следующим образом:  `http://server/_vti_bin/client.svc/search/`. Тем не менее с помощью  `_api` является предпочтительным соглашением.</span><span class="sxs-lookup"><span data-stu-id="93c75-p108">You can also use the URL that references client.svc to access the service, as follows:  `http://server/_vti_bin/client.svc/search/`. However, using  `_api` is the preferred convention.</span></span>
  
    
    
<span data-ttu-id="93c75-135">Используйте следующие точка доступа для доступа к метаданных службы:</span><span class="sxs-lookup"><span data-stu-id="93c75-135">Use the following access point to access the service metadata:</span></span> 
  
    
    
 `http://server/_api/$metadata`
  
    
    
<span data-ttu-id="93c75-136">Общие сведения о службе REST в SharePoint видеть [операции запросов OData используется в запросах SharePoint REST](http://msdn.microsoft.com/library/d4b5c277-ed50-420c-8a9b-860342284b72%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="93c75-136">For general information about the REST service in SharePoint, see  [Use OData query operations in SharePoint REST requests](http://msdn.microsoft.com/library/d4b5c277-ed50-420c-8a9b-860342284b72%28Office.15%29.aspx).</span></span>
  
    
    

## <a name="sharepoint-search-query-web-service-is-deprecated"></a><span data-ttu-id="93c75-137">Устаревшие веб-службы запросов поиска SharePoint</span><span class="sxs-lookup"><span data-stu-id="93c75-137">SharePoint Search Query web service is deprecated</span></span>
<span data-ttu-id="93c75-138"><a name="SP15Searchnew_support"> </a></span><span class="sxs-lookup"><span data-stu-id="93c75-138"></span></span>

<span data-ttu-id="93c75-139">Веб-службы запросов (находится в поле путь `http://server/site/_vti_bin/search.asmx`) — это не поддерживаются в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="93c75-139">The Query web service (located in the path  `http://server/site/_vti_bin/search.asmx`) is deprecated in SharePoint.</span></span> <span data-ttu-id="93c75-140">При создании новых приложений, не используйте этот компонент не рекомендуемые для использования и вместо этого использовать новую службу запросов REST или запроса CSOM.</span><span class="sxs-lookup"><span data-stu-id="93c75-140">If you write new applications, avoid using this deprecated feature and instead use the new Query CSOM or Query REST service.</span></span> <span data-ttu-id="93c75-141">Если изменить существующие приложения, мы настоятельно рекомендуем вам удалить любые зависимости на этот компонент.</span><span class="sxs-lookup"><span data-stu-id="93c75-141">If you modify existing applications, we strongly encourage you to remove any dependency on this feature.</span></span>
  
    
    

## <a name="sharepoint-search-query-object-model-enhancements"></a><span data-ttu-id="93c75-142">Расширения объектной модели SharePoint поискового запроса</span><span class="sxs-lookup"><span data-stu-id="93c75-142">SharePoint Search Query object model enhancements</span></span>
<span data-ttu-id="93c75-143"><a name="SP15Searchnew_support"> </a></span><span class="sxs-lookup"><span data-stu-id="93c75-143"></span></span>

<span data-ttu-id="93c75-144">Запрос свойства содержат сведения о запросе поиска.</span><span class="sxs-lookup"><span data-stu-id="93c75-144">Query properties provide information about a search query.</span></span> <span data-ttu-id="93c75-145">Поиска SharePoint, в контейнере свойств был добавлен в классы запросов и результатов для включения пользовательских запросов свойств.</span><span class="sxs-lookup"><span data-stu-id="93c75-145">In SharePoint Search, a property bag was added to the query and result classes to enable user-defined query properties.</span></span> <span data-ttu-id="93c75-146">Работайте со существующие свойства запроса с помощью свойства одного из классов запросов следующим образом:</span><span class="sxs-lookup"><span data-stu-id="93c75-146">You can access existing query properties via the property on one of the query classes, as follows:</span></span> 
  
    
    
 `KeywordQuery.EnableStemming`
  
    
    
<span data-ttu-id="93c75-147">Или контейнера свойств можно использовать следующим образом:</span><span class="sxs-lookup"><span data-stu-id="93c75-147">Or you can use the property bag, as follows:</span></span> 
  
    
    
 `KeywordQuery.Properties["EnableStemming"]`
  
    
    
<span data-ttu-id="93c75-148">Пользовательские свойства доступны только с помощью контейнера свойств, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="93c75-148">You can access user-defined properties only by using the property bag, as follows:</span></span> 
  
    
    
 `KeywordQuery.Properties["UserDefinedProperty"]`
  
    
    
<span data-ttu-id="93c75-149">Поиск SharePoint включает в себя свойства запроса в контейнере свойств, например, включая новые свойства запроса:</span><span class="sxs-lookup"><span data-stu-id="93c75-149">SharePoint Search includes query properties in the property bag, including new query properties such as:</span></span>
  
    
    

- <span data-ttu-id="93c75-p111">**BypassResultTypes** Указывает, возвращается ли тип элемента результата поиска в окне результатов запроса. Укажите **true** для возвращения не тип результата; в противном случае  **false**.</span><span class="sxs-lookup"><span data-stu-id="93c75-p111">**BypassResultTypes** Specifies whether the search result item type is returned for the query results. Specify **true** to return no result type; otherwise, **false**.</span></span>
    
  
- <span data-ttu-id="93c75-p112">**EnableInterleaving** Указывает, будет ли наборы результатов, созданы при выполнении действия правила запроса для добавления блока результатов смешиваются с результирующий набор для исходного запроса. Укажите **true** смешивать созданный результирующий набор с исходной результирующий набор; в противном случае  **false**.</span><span class="sxs-lookup"><span data-stu-id="93c75-p112">**EnableInterleaving** Specifies whether the result sets generated by executing query rule actions to add a result block are mixed with the result set for the original query. Specify **true** to mix the generated result set with the original result set; otherwise, **false**.</span></span>
    
  
- <span data-ttu-id="93c75-p113">**EnableQueryRules** Указывает, включены ли правила запросов для этого запроса. Укажите **true** для включения правил запросов для запросов; в противном случае  **false**.</span><span class="sxs-lookup"><span data-stu-id="93c75-p113">**EnableQueryRules** Specifies whether query rules are turned on for this query. Specify **true** to enable query rules for the query; otherwise, **false**.</span></span>
    
  
<span data-ttu-id="93c75-p114">Можно указать любое свойство в контейнере свойств, включая пользовательские свойства, как условия правила запроса. Использование правил запроса настраивать параметры поиска для типов запросов, которые важны для пользователей. При запросе соответствует условиям, указанным в правиле запроса, правило задает действия для повышения релевантности результатов поиска связанных.</span><span class="sxs-lookup"><span data-stu-id="93c75-p114">You can specify any property in the property bag, including user-defined properties, as query rule conditions. You use query rules to customize the search experience for the kinds of queries that are important to your users. When a query meets conditions specified in a query rule, the rule specifies actions to improve the relevance of the associated search results.</span></span> 
  
    
    

## <a name="keyword-query-language-enhancements"></a><span data-ttu-id="93c75-159">Расширения языка запросов ключевых слов</span><span class="sxs-lookup"><span data-stu-id="93c75-159">Keyword query language enhancements</span></span>
<span data-ttu-id="93c75-160"><a name="SP15Searchnew_support"> </a></span><span class="sxs-lookup"><span data-stu-id="93c75-160"></span></span>

<span data-ttu-id="93c75-161">SharePoint включает в себя улучшения языка запросов ключевых слов, описанных в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="93c75-161">SharePoint includes improvements to the Keyword query language, which are described in this section.</span></span> 
  
    
    

### <a name="improved-near-operator"></a><span data-ttu-id="93c75-162">Улучшенная РЯДОМ с оператор</span><span class="sxs-lookup"><span data-stu-id="93c75-162">Improved NEAR operator</span></span>

<span data-ttu-id="93c75-163">В SharePoint Server 2010 оператор **NEAR** подразумеваемых максимальное расстояние маркеров **8** и сохраняется порядок использования ввода маркеры.</span><span class="sxs-lookup"><span data-stu-id="93c75-163">In SharePoint Server 2010, the **NEAR** operator implied a maximum token distance of **8** and preserved the ordering of the input tokens.</span></span> <span data-ttu-id="93c75-164">В SharePoint оператор **NEAR** больше не сохраняет порядок использования маркеры.</span><span class="sxs-lookup"><span data-stu-id="93c75-164">In SharePoint, the **NEAR** operator no longer preserves the ordering of tokens.</span></span> <span data-ttu-id="93c75-165">Кроме того оператор **NEAR** теперь получает дополнительный параметр, который указывает максимальное расстояние маркеров.</span><span class="sxs-lookup"><span data-stu-id="93c75-165">In addition, the **NEAR** operator now receives an optional parameter that indicates maximum token distance.</span></span> <span data-ttu-id="93c75-166">Тем не менее значение по умолчанию равно **8**.</span><span class="sxs-lookup"><span data-stu-id="93c75-166">However, the default value is still **8**.</span></span> <span data-ttu-id="93c75-167">Если необходимо использовать предыдущий режим, используйте **ONEAR** .</span><span class="sxs-lookup"><span data-stu-id="93c75-167">If you must use the previous behavior, use **ONEAR** instead.</span></span>
  
    
    
<span data-ttu-id="93c75-168">Оператор **NEAR** можно использовать в выражениях ограничений свойств, как показано в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="93c75-168">The **NEAR** operator can be used in property restriction expressions, as shown in the following example:</span></span>
  
    
    
 `"acquisition" NEAR "debt"`
  
    
    
<span data-ttu-id="93c75-p116">Этот запрос соответствует элементов, где маркеры «приобретение» и «долг» отображаются в пределах одного документа с помощью маркеров максимальное расстояние **8** (если значение не указано, используется значение по умолчанию _n_ ). Порядок маркеры не имеет значения для сопоставления.</span><span class="sxs-lookup"><span data-stu-id="93c75-p116">This query matches items where the tokens "acquisition" and "debt" appear within the same document, with a maximum token distance of **8** (which is the default value of _n_ if no value is provided). The order of the tokens is not significant for the match.</span></span>
  
    
    
<span data-ttu-id="93c75-171">Если требуется меньше расстояние маркеров, можно указать следующим образом:</span><span class="sxs-lookup"><span data-stu-id="93c75-171">If you require a smaller token distance, you can specify it as follows:</span></span>
  
    
    
 `"acquisition" NEAR(n=3) "debt"`
  
    
    
<span data-ttu-id="93c75-p117">Этот запрос соответствует элементов, где два маркеры «приобретения» и «долг» отображаются в пределах одного документа с максимальное расстояние маркеров **3**. Порядок маркеры не имеет значения для сопоставления.</span><span class="sxs-lookup"><span data-stu-id="93c75-p117">This query matches items where the two tokens "acquisition" and "debt" appear within the same document, with a maximum token distance of **3**. The order of the tokens is not significant for the match.</span></span>
  
    
    

### <a name="new-onear-operator"></a><span data-ttu-id="93c75-174">Новый оператор ONEAR</span><span class="sxs-lookup"><span data-stu-id="93c75-174">New ONEAR operator</span></span>

<span data-ttu-id="93c75-p118">Оператор **ONEAR** предоставляет упорядоченный рядом с функциональные возможности. Получает дополнительный параметр, который указывает максимальное расстояние маркеров; значение по умолчанию: **8**.</span><span class="sxs-lookup"><span data-stu-id="93c75-p118">The **ONEAR** operator provides ordered near functionality. It receives an optional parameter that indicates maximum token distance; the default value is **8**.</span></span>
  
    
    
<span data-ttu-id="93c75-p119">Оператор **ONEAR** сохраняет порядок ввода выражения. Для неупорядоченные близости используйте **NEAR**.</span><span class="sxs-lookup"><span data-stu-id="93c75-p119">The **ONEAR** operator preserves the order of the input expressions. For unordered proximity, use **NEAR**.</span></span>
  
    
    
<span data-ttu-id="93c75-179">Оператор **ONEAR** можно использовать в выражениях ограничений свойств, как показано в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="93c75-179">You can use the **ONEAR** operator in property restriction expressions, as shown in the following example:</span></span>
  
    
    
 `"acquisition" ONEAR "debt"`
  
    
    
<span data-ttu-id="93c75-p120">Этот запрос соответствует элементов, где два маркеры «приобретение» и «долг» отображаются в пределах одного документа с помощью маркеров максимальное расстояние **8** (если значение не указано, используется значение по умолчанию _n_ ). Порядок маркеры должен соответствовать для элемента должно быть возвращено.</span><span class="sxs-lookup"><span data-stu-id="93c75-p120">This query matches items where the two tokens "acquisition" and "debt" appear within the same document, with a maximum token distance of **8** (which is the default value of _n_ if no value is provided). The order of the tokens must match for an item to be returned.</span></span>
  
    
    
<span data-ttu-id="93c75-182">Если требуется меньше расстояние маркеров, можно указать следующим образом:</span><span class="sxs-lookup"><span data-stu-id="93c75-182">If you require a smaller token distance, you can specify it as follows:</span></span>
  
    
    
 `"acquisition" ONEAR(n=3) "debt"`
  
    
    
<span data-ttu-id="93c75-p121">Этот запрос соответствует элементов, где два маркеры «приобретения» и «долг» отображаются в пределах одного документа с максимальное расстояние маркеров **3**. Порядок маркеры должен соответствовать для элемента должно быть возвращено.</span><span class="sxs-lookup"><span data-stu-id="93c75-p121">This query matches items where the two tokens "acquisition" and "debt" appear within the same document, with a maximum token distance of **3**. The order of the tokens must match for an item to be returned.</span></span>
  
    
    

### <a name="new-xrank-operator"></a><span data-ttu-id="93c75-185">Новый оператор XRANK</span><span class="sxs-lookup"><span data-stu-id="93c75-185">New XRANK operator</span></span>

<span data-ttu-id="93c75-186">В SharePoint Server 2010 оператор **XRANK** был доступен только с помощью языка запросов FAST (FQL).</span><span class="sxs-lookup"><span data-stu-id="93c75-186">In SharePoint Server 2010, the **XRANK** operator was available only with FAST Query language (FQL).</span></span> <span data-ttu-id="93c75-187">SharePoint представлены новые и мощные оператор **XRANK** .</span><span class="sxs-lookup"><span data-stu-id="93c75-187">SharePoint introduces a new and powerful **XRANK** operator.</span></span>
  
    
    
<span data-ttu-id="93c75-p123">Оператор **XRANK** предоставляет элемент управления динамического ранжирования. Этот оператор повышает динамического ранга элементы в зависимости от появления некоторых терминов, не изменяя элементы, соответствующие запроса.</span><span class="sxs-lookup"><span data-stu-id="93c75-p123">The **XRANK** operator provides dynamic control of ranking. This operator boosts the dynamic rank of items based on the occurrence of certain terms without changing items that match the query.</span></span>
  
    
    

## <a name="rich-results-framework-for-customizing-search-results-ui"></a><span data-ttu-id="93c75-190">Структура полнофункциональные результатов по настройке пользовательском Интерфейсе результатов поиска</span><span class="sxs-lookup"><span data-stu-id="93c75-190">Rich results framework for customizing search results UI</span></span>
<span data-ttu-id="93c75-191"><a name="SP15Searchnew_support"> </a></span><span class="sxs-lookup"><span data-stu-id="93c75-191"></span></span>

<span data-ttu-id="93c75-192">Поиск SharePoint включает в себя новой рамки результатов, который позволяет легко настроить внешний вид (внешний вид и функции) пользовательского интерфейса (UI) результаты поиска.</span><span class="sxs-lookup"><span data-stu-id="93c75-192">SharePoint Search includes a new results framework that makes it easy to customize the appearance (look and feel) of the search results user interface (UI).</span></span> <span data-ttu-id="93c75-193">Теперь вместо написания настраиваемое преобразование XSLT, чтобы изменить способ отображения результатов поиска, можно настроить внешний вид важные типы результатов с помощью типов результатов и шаблонов отображения.</span><span class="sxs-lookup"><span data-stu-id="93c75-193">Now, instead of writing a custom XSLT to change how search results are displayed, you can customize the appearance of important types of results by using display templates and result types.</span></span>
  
    
    

### <a name="display-templates"></a><span data-ttu-id="93c75-194">Шаблоны для отображения</span><span class="sxs-lookup"><span data-stu-id="93c75-194">Display templates</span></span>

<span data-ttu-id="93c75-p125">Шаблоны для отображения определяют макет и поведение типа результата с помощью HTML, CSS и JavaScript. Можно настроить существующие шаблоны отображения или создать шаблоны для отображения с использованием HTML-редактора и загрузите их в коллекцию шаблонов отображения.</span><span class="sxs-lookup"><span data-stu-id="93c75-p125">Display templates define the visual layout and behavior of a result type by using HTML, CSS, and JavaScript. You can customize the existing display templates or create display templates by using an HTML editor and upload them to the display templates gallery.</span></span>
  
    
    

### <a name="result-types"></a><span data-ttu-id="93c75-197">Типы результатов</span><span class="sxs-lookup"><span data-stu-id="93c75-197">Result types</span></span>

<span data-ttu-id="93c75-198">Типы результатов определяют, как для отображения набора результатов поиска в семействе сайтов из следующих:</span><span class="sxs-lookup"><span data-stu-id="93c75-198">Result types define how to display a set of search results based on a collection of the following:</span></span>
  
    
    

- <span data-ttu-id="93c75-p126">**Правила** Определите, когда следует применять тип результата, на основании заданных условий. Условия правила может быть присоединен с помощью равенства, сравнения и логические операторы.</span><span class="sxs-lookup"><span data-stu-id="93c75-p126">**Rules** Determine when to apply a result type, based on the specified conditions. Rule conditions can be joined by using equality, comparison, and logical operators.</span></span>
    
  
- <span data-ttu-id="93c75-p127">**Свойства** Определение списка управляемых свойств для результата. Управляемые свойства необходимо добавить в список перед Сопоставление управляемого свойства для шаблона для отображения.</span><span class="sxs-lookup"><span data-stu-id="93c75-p127">**Properties** Determine the list of managed properties for the result. You must add managed properties to the list before you map the managed property to a display template.</span></span>
    
  
- <span data-ttu-id="93c75-203">**Шаблоны отображения** Определение расположения тип результата.</span><span class="sxs-lookup"><span data-stu-id="93c75-203">**Display templates** Define the visual layout of the result type.</span></span>
    
  
<span data-ttu-id="93c75-204">Администраторы могут создавать и управлять типы результатов на уровне сайта или уровне приложения службы. нет пользовательского кода не требуется.</span><span class="sxs-lookup"><span data-stu-id="93c75-204">Administrators can create and manage result types at the site level or service application level; no custom coding is required.</span></span>
  
    
    

## <a name="connector-framework-enhancements"></a><span data-ttu-id="93c75-205">Улучшения Connector framework</span><span class="sxs-lookup"><span data-stu-id="93c75-205">Connector framework enhancements</span></span>
<span data-ttu-id="93c75-206"><a name="SP15Searchnew_support"> </a></span><span class="sxs-lookup"><span data-stu-id="93c75-206"></span></span>

<span data-ttu-id="93c75-207">Поиск SharePoint позволяет получить сведения об утверждениях для контента, хранящиеся в пользовательских внешних источников данных, которые выполняет обход контента с помощью платформы соединителя.</span><span class="sxs-lookup"><span data-stu-id="93c75-207">SharePoint Search enables you to retrieve claims information for content stored in custom external data sources that are crawled by using the connector framework.</span></span>
  
    
    
<span data-ttu-id="93c75-208">Connector framework также предоставляет улучшенные исключений записи и сбор данных об устранении ошибки, обнаруженные во время обхода источников контента, с помощью настраиваемых соединителей, основанные на основе инфраструктуры соединителей.</span><span class="sxs-lookup"><span data-stu-id="93c75-208">The connector framework also provides improved exception capturing and logging to help you troubleshoot errors encountered when crawling content sources using custom connectors that are built on top of the connector framework.</span></span> <span data-ttu-id="93c75-209">Сведения о connector framework содержатся [инфраструктурой соединителя поиска в SharePoint](search-connector-framework-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="93c75-209">For information about the connector framework, see  [Search connector framework in SharePoint](search-connector-framework-in-sharepoint.md).</span></span>
  
    
    

## <a name="additional-resources"></a><span data-ttu-id="93c75-210">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="93c75-210">Additional resources</span></span>
<span data-ttu-id="93c75-211"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="93c75-211"></span></span>


-  [<span data-ttu-id="93c75-212">Поиск по новому контенту с поиска SharePoint</span><span class="sxs-lookup"><span data-stu-id="93c75-212">Searching new content with SharePoint Search</span></span>](searching-new-content-with-sharepoint-search.md)
    
  
-  [<span data-ttu-id="93c75-213">Настройка службы поиска в SharePoint</span><span class="sxs-lookup"><span data-stu-id="93c75-213">Configure search in SharePoint</span></span>](configure-search-in-sharepoint.md)
    
  
-  [<span data-ttu-id="93c75-214">Построение запросов поиска в SharePoint</span><span class="sxs-lookup"><span data-stu-id="93c75-214">Building search queries in SharePoint</span></span>](building-search-queries-in-sharepoint.md)
    
  
-  [<span data-ttu-id="93c75-215">Способ: использование пользовательского триммера безопасности для результатов поиска SharePoint Server</span><span class="sxs-lookup"><span data-stu-id="93c75-215">How to: Use a custom security trimmer for SharePoint Server search results</span></span>](how-to-use-a-custom-security-trimmer-for-sharepoint-server-search-results.md)
    
  

