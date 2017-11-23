---
title: "Получение предложений запроса, с помощью службы Search REST"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: a64c5bec-64a8-4752-9c72-433d1c864aed
ms.openlocfilehash: d3359be5b2c4f68ea75419babd9ceb8096fc3446
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="retrieving-query-suggestions-using-the-search-rest-service"></a><span data-ttu-id="2964d-102">Получение предложений запроса, с помощью службы Search REST</span><span class="sxs-lookup"><span data-stu-id="2964d-102">Retrieving query suggestions using the Search REST service</span></span>
<span data-ttu-id="2964d-103">Узнайте, как использовать службы поиска REST из клиентов и мобильных приложений для извлечения предложений запроса из поиска в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="2964d-103">Learn how you can use the Search REST service from your client and mobile applications to retrieve query suggestions from Search in SharePoint.</span></span>
<span data-ttu-id="2964d-104">Предложения запроса, также известной как предложения поиска, фраз, которые пользователи уже выполнен поиск и, или отобразить «предложенные» им как люди вводят свои запросы.</span><span class="sxs-lookup"><span data-stu-id="2964d-104">Query suggestions, also known as search suggestions, are phrases that users have already searched for and that are displayed or "suggested" to them as they type their queries.</span></span> <span data-ttu-id="2964d-105">Чтобы включить предложения запроса до и после запроса можно использовать поиска в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="2964d-105">You can use Search in SharePoint to turn on pre-query and post-query suggestions.</span></span> <span data-ttu-id="2964d-106">Эти варианты отображаются в списке под окном поиска, как пользователь вводит запрос.</span><span class="sxs-lookup"><span data-stu-id="2964d-106">These suggestions appear in a list below the Search box as a user types a query.</span></span> <span data-ttu-id="2964d-107">Дополнительные сведения о предложений запроса, а также для включения их можно [Управление предложениями запроса в SharePoint](http://technet.microsoft.com/ru-ru/library/jj721441.aspx).</span><span class="sxs-lookup"><span data-stu-id="2964d-107">For more information about query suggestions and how to enable them, see  [Manage query suggestions in SharePoint](http://technet.microsoft.com/ru-ru/library/jj721441.aspx).</span></span>
  
    
    


## <a name="suggest-endpoint-in-the-search-rest-service"></a><span data-ttu-id="2964d-108">Предложить конечной точки в службе REST поиска</span><span class="sxs-lookup"><span data-stu-id="2964d-108">Suggest endpoint in the Search REST service</span></span>
<span data-ttu-id="2964d-109"><a name="bk_SuggestEndpoint"> </a></span><span class="sxs-lookup"><span data-stu-id="2964d-109"><a name="bk_SuggestEndpoint"> </a></span></span>

<span data-ttu-id="2964d-110">Службы REST поиска включает в себя **Suggest** конечной точки, которые можно использовать в любой технологии, поддерживающей веб-запросы REST для получения предложений запроса, поисковая система генерирует для запросов от клиента или приложения для мобильных устройств.</span><span class="sxs-lookup"><span data-stu-id="2964d-110">The Search REST service includes a **Suggest** endpoint you can use in any technology that supports REST web requests to retrieve query suggestions that the search system generates for a query from client or mobile applications.</span></span>
  
    
    
<span data-ttu-id="2964d-111">URI для **GET** запросов к конечной точке службы поиска REST **Suggest**  это:</span><span class="sxs-lookup"><span data-stu-id="2964d-111">The URI for **GET** requests to the Search REST service's **Suggest** endpoint is:</span></span>
  
    
    
 `/_api/search/suggest`
  
    
    
<span data-ttu-id="2964d-p102">В URL-адрес заданы параметры предложения запроса. Можно создать URL-адрес запроса двумя способами:</span><span class="sxs-lookup"><span data-stu-id="2964d-p102">The query suggestion parameters are specified in the URL. You can construct the request URL in two ways:</span></span>
  
    
    


  
    
    
>  `http://server/_api/search/suggest?parameter=value&amp;parameter=value`
    
  

  
    
    
>  `http://server/_api/search/suggest(parameter=value&amp;parameter=value)`
    
  

> <span data-ttu-id="2964d-114">**Примечание:** Службы поиска REST не поддерживает анонимные запросы к конечной точке **Предложить** .</span><span class="sxs-lookup"><span data-stu-id="2964d-114">**Note:** The Search REST service doesn't support anonymous requests to the **Suggest** endpoint.</span></span>
  
    
    


## <a name="query-suggestion-parameters"></a><span data-ttu-id="2964d-115">Параметры предложений запроса</span><span class="sxs-lookup"><span data-stu-id="2964d-115">Query suggestion parameters</span></span>
<span data-ttu-id="2964d-116"><a name="bk_SuggestParameters"> </a></span><span class="sxs-lookup"><span data-stu-id="2964d-116"><a name="bk_SuggestParameters"> </a></span></span>

<span data-ttu-id="2964d-117">В следующих разделах описываются параметры, которые можно использовать для конечной точки **Suggest**.</span><span class="sxs-lookup"><span data-stu-id="2964d-117">The following sections describe the parameters you can use for the **Suggest** endpoint.</span></span>
  
    
    

### <a name="querytext"></a><span data-ttu-id="2964d-118">Текст запроса</span><span class="sxs-lookup"><span data-stu-id="2964d-118">Querytext</span></span>

<span data-ttu-id="2964d-119">Строка, содержащая текст для запроса поиска.</span><span class="sxs-lookup"><span data-stu-id="2964d-119">A string that contains the text for the search query.</span></span>
  
    
    
 <span data-ttu-id="2964d-120">**Пример запроса GET**</span><span class="sxs-lookup"><span data-stu-id="2964d-120">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="2964d-121">http:// _server_/_api/search/suggest?querytext = "sharepoint"</span><span class="sxs-lookup"><span data-stu-id="2964d-121">http:// _server_/_api/search/suggest?querytext='sharepoint'</span></span>
  
    
    

### <a name="inumberofquerysuggestions"></a><span data-ttu-id="2964d-122">iNumberOfQuerySuggestions</span><span class="sxs-lookup"><span data-stu-id="2964d-122">iNumberOfQuerySuggestions</span></span>

<span data-ttu-id="2964d-p103">Количество предложений запроса для извлечения. Должен быть больше нуля (0). Значение по умолчанию  5.</span><span class="sxs-lookup"><span data-stu-id="2964d-p103">The number of query suggestions to retrieve. Must be greater than zero (0). The default value is 5.</span></span>
  
    
    
 <span data-ttu-id="2964d-126">**Пример запроса GET**</span><span class="sxs-lookup"><span data-stu-id="2964d-126">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="2964d-127">http:// _server_/_api/search/suggest?querytext = "sharepoint" &amp; inumberofquerysuggestions = 3</span><span class="sxs-lookup"><span data-stu-id="2964d-127">http:// _server_/_api/search/suggest?querytext='sharepoint'&amp;inumberofquerysuggestions=3</span></span>
  
    
    

### <a name="inumberofresultsuggestions"></a><span data-ttu-id="2964d-128">iNumberOfResultSuggestions</span><span class="sxs-lookup"><span data-stu-id="2964d-128">iNumberOfResultSuggestions</span></span>

<span data-ttu-id="2964d-p104">Число личных результаты для извлечения. Должен быть больше нуля (0). Значение по умолчанию  5.</span><span class="sxs-lookup"><span data-stu-id="2964d-p104">The number of personal results to retrieve. Must be greater than zero (0). The default value is 5.</span></span>
  
    
    
 <span data-ttu-id="2964d-132">**Пример запроса GET**</span><span class="sxs-lookup"><span data-stu-id="2964d-132">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="2964d-133">http:// _server_/_api/search/suggest?querytext = "sharepoint" &amp; inumberofresultsuggestions = 4</span><span class="sxs-lookup"><span data-stu-id="2964d-133">http:// _server_/_api/search/suggest?querytext='sharepoint'&amp;inumberofresultsuggestions=4</span></span>
  
    
    

### <a name="fprequerysuggestions"></a><span data-ttu-id="2964d-134">fPreQuerySuggestions</span><span class="sxs-lookup"><span data-stu-id="2964d-134">fPreQuerySuggestions</span></span>

<span data-ttu-id="2964d-p105">Логическое значение, указывающее, следует ли извлекать предложения запроса до или после запроса. **true** для возврата предложения перед запроса; в противном случае  **false**. Значение по умолчанию  **false**.</span><span class="sxs-lookup"><span data-stu-id="2964d-p105">A Boolean value that specifies whether to retrieve pre-query or post-query suggestions. **true** to return pre-query suggestions; otherwise, **false**. The default value is **false**.</span></span>
  
    
    
 <span data-ttu-id="2964d-138">**Пример запроса GET**</span><span class="sxs-lookup"><span data-stu-id="2964d-138">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="2964d-139">http:// _server_/_api/search/suggest?querytext = "sharepoint" &amp; fprequerysuggestions = true</span><span class="sxs-lookup"><span data-stu-id="2964d-139">http:// _server_/_api/search/suggest?querytext='sharepoint'&amp;fprequerysuggestions=true</span></span>
  
    
    

### <a name="fhithighlighting"></a><span data-ttu-id="2964d-140">fHitHighlighting</span><span class="sxs-lookup"><span data-stu-id="2964d-140">fHitHighlighting</span></span>

<span data-ttu-id="2964d-p106">Логическое значение, которое указывает, следует ли для сбора данных для выделения и форматирования полужирным шрифтом предложений запроса. **true** форматирование полужирным шрифтом условия предложений возвращенные запроса, которые соответствуют терминов в указанного запроса; в противном случае  **false**. Значение по умолчанию  **true**.</span><span class="sxs-lookup"><span data-stu-id="2964d-p106">A Boolean value that specifies whether to hit-highlight or format in bold the query suggestions. **true** to format in bold the terms in the returned query suggestions that match terms in the specified query; otherwise, **false**. The default value is **true**.</span></span>
  
    
    
 <span data-ttu-id="2964d-144">**Пример запроса GET**</span><span class="sxs-lookup"><span data-stu-id="2964d-144">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="2964d-145">http:// _server_/_api/search/suggest?querytext = "sharepoint" &amp; fhithighlighting = false</span><span class="sxs-lookup"><span data-stu-id="2964d-145">http:// _server_/_api/search/suggest?querytext='sharepoint'&amp;fhithighlighting=false</span></span>
  
    
    

### <a name="fcapitalizefirstletters"></a><span data-ttu-id="2964d-146">fCapitalizeFirstLetters</span><span class="sxs-lookup"><span data-stu-id="2964d-146">fCapitalizeFirstLetters</span></span>

<span data-ttu-id="2964d-p107">Логическое значение, которое указывает, следует ли преобразование первой буквы в каждого термина в предложения возвращенные запроса. **true** прописной первую букву в каждом терминов; в противном случае  **false**. Значение по умолчанию  **false**.</span><span class="sxs-lookup"><span data-stu-id="2964d-p107">A Boolean value that specifies whether to capitalize the first letter in each term in the returned query suggestions. **true** to capitalize the first letter in each term; otherwise, **false**. The default value is **false**.</span></span>
  
    
    
 <span data-ttu-id="2964d-150">**Пример запроса GET**</span><span class="sxs-lookup"><span data-stu-id="2964d-150">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="2964d-151">http:// _server_/_api/search/suggest?querytext = "sharepoint" &amp; fcapitalizefirstletters = false</span><span class="sxs-lookup"><span data-stu-id="2964d-151">http:// _server_/_api/search/suggest?querytext='sharepoint'&amp;fcapitalizefirstletters=false</span></span>
  
    
    

### <a name="culture"></a><span data-ttu-id="2964d-152">Culture</span><span class="sxs-lookup"><span data-stu-id="2964d-152">Culture</span></span>

<span data-ttu-id="2964d-153">Код языка (LCID) для запроса (см. статью  [Коды языков, присвоенные Майкрософт](http://msdn.microsoft.com/en-us/goglobal/bb964664.aspx)).</span><span class="sxs-lookup"><span data-stu-id="2964d-153">The locale ID (LCID) for the query (see  [Locale IDs Assigned by Microsoft](http://msdn.microsoft.com/en-us/goglobal/bb964664.aspx)).</span></span>
  
    
    
 <span data-ttu-id="2964d-154">**Пример запроса GET**</span><span class="sxs-lookup"><span data-stu-id="2964d-154">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="2964d-155">http:// _server_/_api/search/suggest?querytext = "sharepoint" &amp; EventID = 1044</span><span class="sxs-lookup"><span data-stu-id="2964d-155">http:// _server_/_api/search/suggest?querytext='sharepoint'&amp;culture=1044</span></span>
  
    
    

### <a name="enablestemming"></a><span data-ttu-id="2964d-156">EnableStemming</span><span class="sxs-lookup"><span data-stu-id="2964d-156">EnableStemming</span></span>

<span data-ttu-id="2964d-p108">Логическое значение, указывающее, включено ли выделение корней. **true**, чтобы включить извлечение корней слов; в противном случае  **false**. Значение по умолчанию  **true**.</span><span class="sxs-lookup"><span data-stu-id="2964d-p108">A Boolean value that specifies whether stemming is enabled. **true** to enable stemming; otherwise, **false**. The default value is **true**.</span></span>
  
    
    
 <span data-ttu-id="2964d-160">**Пример запроса GET**</span><span class="sxs-lookup"><span data-stu-id="2964d-160">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="2964d-161">http:// _server_/_api/search/suggest?querytext = "sharepoint" &amp; enablestemming = false</span><span class="sxs-lookup"><span data-stu-id="2964d-161">http:// _server_/_api/search/suggest?querytext='sharepoint'&amp;enablestemming=false</span></span>
  
    
    

### <a name="showpeoplenamesuggestions"></a><span data-ttu-id="2964d-162">ShowPeopleNameSuggestions</span><span class="sxs-lookup"><span data-stu-id="2964d-162">ShowPeopleNameSuggestions</span></span>

<span data-ttu-id="2964d-p109">Логическое значение, указывающее, следует ли включать имена людей в предложения возвращенные запроса. **true** для включения имен людей в предложения возвращенные запроса; в противном случае  **false**. Значение по умолчанию  **true**.</span><span class="sxs-lookup"><span data-stu-id="2964d-p109">A Boolean value that specifies whether to include people names in the returned query suggestions. **true** to include people names in the returned query suggestions; otherwise, **false**. The default value is **true**.</span></span>
  
    
    
 <span data-ttu-id="2964d-166">**Пример запроса GET**</span><span class="sxs-lookup"><span data-stu-id="2964d-166">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="2964d-167">http:// _server_/_api/search/suggest?querytext = "sharepoint" &amp; showpeoplenamesuggestions = false</span><span class="sxs-lookup"><span data-stu-id="2964d-167">http:// _server_/_api/search/suggest?querytext='sharepoint'&amp;showpeoplenamesuggestions=false</span></span>
  
    
    

### <a name="enablequeryrules"></a><span data-ttu-id="2964d-168">EnableQueryRules</span><span class="sxs-lookup"><span data-stu-id="2964d-168">EnableQueryRules</span></span>

<span data-ttu-id="2964d-p110">Логическое значение, которое указывает, следует ли включить правила запросов для этого запроса. **true** Включение правила запросов; в противном случае  **false**. Значение по умолчанию  **true**.</span><span class="sxs-lookup"><span data-stu-id="2964d-p110">A Boolean value that specifies whether to turn on query rules for this query. **true** to turn on query rules; otherwise, **false**. The default value is **true**.</span></span>
  
    
    
 <span data-ttu-id="2964d-172">**Пример запроса GET**</span><span class="sxs-lookup"><span data-stu-id="2964d-172">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="2964d-173">http:// _server_/_api/search/suggest?querytext = "sharepoint" &amp; enablequeryrules = false</span><span class="sxs-lookup"><span data-stu-id="2964d-173">http:// _server_/_api/search/suggest?querytext='sharepoint'&amp;enablequeryrules=false</span></span>
  
    
    

### <a name="fprefixmatchallterms"></a><span data-ttu-id="2964d-174">fPrefixMatchAllTerms</span><span class="sxs-lookup"><span data-stu-id="2964d-174">fPrefixMatchAllTerms</span></span>

<span data-ttu-id="2964d-p111">Сопоставляет значение Boolean, указывающее, нужно ли возвращать предложения запроса для префикса. **true** для возврата на основе префикса предложений запроса соответствует, в противном случае **false** при предложений запроса должна соответствовать word полного запроса.</span><span class="sxs-lookup"><span data-stu-id="2964d-p111">A Boolean value that specifies whether to return query suggestions for prefix matches. **true** to return query suggestions based on prefix matches, otherwise, **false** when query suggestions should match the full query word.</span></span>
  
    
    
 <span data-ttu-id="2964d-177">**Пример запроса GET**</span><span class="sxs-lookup"><span data-stu-id="2964d-177">**Sample GET request**</span></span>
  
    
    
<span data-ttu-id="2964d-178">http:// _server_/_api/search/suggest?querytext = "sharepoint" &amp; fprefixmatchallterms = false</span><span class="sxs-lookup"><span data-stu-id="2964d-178">http:// _server_/_api/search/suggest?querytext='sharepoint'&amp;fprefixmatchallterms=false</span></span>
  
    
    

## <a name="additional-resources"></a><span data-ttu-id="2964d-179">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="2964d-179">Additional resources</span></span>
<span data-ttu-id="2964d-180"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="2964d-180"><a name="bk_addresources"> </a></span></span>


-  [<span data-ttu-id="2964d-181">Общие сведения об API службы поиска REST для SharePoint</span><span class="sxs-lookup"><span data-stu-id="2964d-181">SharePoint Search REST API overview</span></span>](sharepoint-search-rest-api-overview.md)
    
  
-  [<span data-ttu-id="2964d-182">Поиск в SharePoint</span><span class="sxs-lookup"><span data-stu-id="2964d-182">Search in SharePoint</span></span>](search-in-sharepoint.md)
    
  
-  [<span data-ttu-id="2964d-183">SharePoint: использование службы поиска REST в приложении для SharePoint</span><span class="sxs-lookup"><span data-stu-id="2964d-183">SharePoint: Using the search REST service from an app for SharePoint</span></span>](http://code.msdn.microsoft.com/sharepoint/SharePoint-Perform-a-1bf3e87d)
    
  
-  [<span data-ttu-id="2964d-184">Новые возможности поиска в SharePoint для разработчиков (en)</span><span class="sxs-lookup"><span data-stu-id="2964d-184">What's new in SharePoint search for developers</span></span>](what-s-new-in-sharepoint-search-for-developers.md)
    
  
-  [<span data-ttu-id="2964d-185">Программирование с использованием службы SharePoint 2013 REST</span><span class="sxs-lookup"><span data-stu-id="2964d-185">Use OData query operations in SharePoint REST requests</span></span>](http://msdn.microsoft.com/library/d4b5c277-ed50-420c-8a9b-860342284b72%28Office.15%29.aspx)
    
  

  
    
    

