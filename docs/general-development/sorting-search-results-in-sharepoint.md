---
title: "Сортировка результатов поиска в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 5bad3656838a7175e285ee31d9ec8ef9a3756dec
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="sorting-search-results-in-sharepoint"></a><span data-ttu-id="e27d2-102">Сортировка результатов поиска в SharePoint</span><span class="sxs-lookup"><span data-stu-id="e27d2-102">Sorting search results in SharePoint</span></span>

  
    
    
![Раздел концептуального обзора](../images/mod_icon_badge_conoverview.png)
  
    
    

  
    
    

  
    
    
<span data-ttu-id="e27d2-104">Программная результатов поиска в сортировки — по рангу по значению управляемого свойства, по формуле или в случайном порядке — с помощью объектной модели запросов в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="e27d2-104">Sort search results programmatically—by rank, by managed property value, by a formula expression, or in random order—by using the Query object model in SharePoint.</span></span> <span data-ttu-id="e27d2-105">Можно сортировать результаты поиска для SharePoint, одним из четырех способов:</span><span class="sxs-lookup"><span data-stu-id="e27d2-105">You can sort the search results for SharePoint in four ways:</span></span>
  
    
    


-  <span data-ttu-id="e27d2-106">[Сортировка результатов поиска по рангу](#SP15_Sort_search_resuilts_by_rank): позволяет сортировать результаты поиска по степени релевантности.</span><span class="sxs-lookup"><span data-stu-id="e27d2-106">[Sort search results by rank](#SP15_Sort_search_resuilts_by_rank): Enables you to sort the search result by relevance rank.</span></span>
    
  
-  <span data-ttu-id="e27d2-107">[Сортировка результатов поиска по значению управляемого свойства](#SP15_Sort_search_results_by_managed_property_value): позволяет сортировать результаты поиска, на основе значения одного или нескольких управляемых свойств.</span><span class="sxs-lookup"><span data-stu-id="e27d2-107">[Sort search results by managed property value](#SP15_Sort_search_results_by_managed_property_value): Enables you to sort the search result based on the value of one or more managed properties.</span></span>
    
  
-  <span data-ttu-id="e27d2-108">[Сортировка результатов поиска по формуле](#SP15_Sort_search_results_by_formula): позволяет сортировать результаты поиска по формуле, указанной в запросе.</span><span class="sxs-lookup"><span data-stu-id="e27d2-108">[Sort search results by a formula expression](#SP15_Sort_search_results_by_formula): Enables you to sort the search result by a formula specified in the query request.</span></span>
    
  
-  <span data-ttu-id="e27d2-109">[Сортировка результатов поиска в случайном порядке](#SP15_Sort_search_results_in_random_order): позволяет сортировать результаты запроса в случайном порядке или добавлять случайный компонент порядок сортировки.</span><span class="sxs-lookup"><span data-stu-id="e27d2-109">[Sort search results in random order](#SP15_Sort_search_results_in_random_order): Enables you to sort the query result in random order, or add a random component to the sort order.</span></span>
    
  

<span data-ttu-id="e27d2-110">В этой статье основное внимание уделяется программная сортировка результатов поиска.</span><span class="sxs-lookup"><span data-stu-id="e27d2-110">This article focuses on sorting search results programmatically.</span></span> <span data-ttu-id="e27d2-111">Чтобы узнать, как для сортировки результатов поиска с помощью правил запроса SharePoint, обратитесь к следующим статьям:</span><span class="sxs-lookup"><span data-stu-id="e27d2-111">To learn how to sort search results using SharePoint query rules, see the following articles:</span></span>
  
    
    


-  [<span data-ttu-id="e27d2-112">Изменение ранжирования результатов поиска в Управление правилами запросов</span><span class="sxs-lookup"><span data-stu-id="e27d2-112">Change ranked search results in Manage query rules</span></span>](http://technet.microsoft.com/en-us/library/jj871676.aspx#BKMK_ChangeRankedSearchResults)
    
  
-  [<span data-ttu-id="e27d2-113">Изменение ранжирования результатов поиска в создание правил запросов для управления веб-контентом</span><span class="sxs-lookup"><span data-stu-id="e27d2-113">Change ranked search results in Create query rules for web content management</span></span>](http://technet.microsoft.com/en-us/library/jj871014.aspx#BKMK_ChangeRankedSearchResults)
    
  

## <a name="how-to-specify-sorting-in-a-query-request"></a><span data-ttu-id="e27d2-114">Задание сортировки в запросе</span><span class="sxs-lookup"><span data-stu-id="e27d2-114">How to specify sorting in a query request</span></span>
<span data-ttu-id="e27d2-115"><a name="SP15_Specify_sorting_in_query_request"> </a></span><span class="sxs-lookup"><span data-stu-id="e27d2-115"></span></span>

<span data-ttu-id="e27d2-p103">При использовании объектной модели запросов можно выбрать условия сортировки с указанием спецификации через свойство  [SortList](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.KeywordQuery.SortList.aspx) класса [KeywordQuery](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.KeywordQuery.aspx) . Свойство [SortList](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.KeywordQuery.SortList.aspx) имеет тип [SortCollection](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.SortCollection.aspx) , который представляет коллекцию объектов [Sort](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.Sort.aspx) .</span><span class="sxs-lookup"><span data-stu-id="e27d2-p103">When you use the Query object model, you can choose the sort criteria by providing a sort specification through the  [SortList](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.KeywordQuery.SortList.aspx) property of the [KeywordQuery](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.KeywordQuery.aspx) class. The [SortList](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.KeywordQuery.SortList.aspx) property is of type [SortCollection](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.SortCollection.aspx) , which represents a collection of [Sort](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.Sort.aspx) objects.</span></span>
  
    
    
<span data-ttu-id="e27d2-p104">Объект  [Sort](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.Sort.aspx) определяет способ сортировки результатов поиска; он состоит из значения, чтобы заказа на результаты поиска на ( [Property](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.Sort.Property.aspx) ) и направление, в котором требуется упорядочивания результатов ( [Direction](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.Sort.Direction.aspx) ). Направление имеет тип [SortDirection()](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.SortDirection.aspx) и может по возрастанию или по убыванию.</span><span class="sxs-lookup"><span data-stu-id="e27d2-p104">A  [Sort](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.Sort.aspx) object defines a way to sort search results; it consists of a value you want to order search results on ( [Property](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.Sort.Property.aspx) ) and a direction in which you want to order the results ( [Direction](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.Sort.Direction.aspx) ). The direction is of type [SortDirection()](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.SortDirection.aspx) and can be ascending or descending.</span></span>
  
    
    
<span data-ttu-id="e27d2-p105">При наличии нескольких значений в  [SortList](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.KeywordQuery.SortList.aspx) сортировка выполняется на основе той последовательности, в котором отображаются значения. Это означает, что каждый объект **Sort** представляет уровень порядок сортировки. Любой последующий уровень не изменяет порядок результатов, которые были различаются по предыдущих, но оно может повлиять на внутренний порядок результатов, которые имеют одинаковые значения сортировки для предыдущих уровней.</span><span class="sxs-lookup"><span data-stu-id="e27d2-p105">If you have multiple values in  [SortList](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.KeywordQuery.SortList.aspx) , the sorting is performed based on the sequence in which the values appear. This means that every **Sort** object represents a sort order level. Any succeeding level does not change the ordering of results that were differentiated by previous ones, but it may affect the internal ordering of results that have the same sort values for the previous levels.</span></span>
  
    
    
<span data-ttu-id="e27d2-123">За исключением объектной модели запросов SharePoint также предоставляет службы поиска REST, которые можно использовать, чтобы отправлять запросы к индексу поиска с помощью клиента или приложения для мобильных устройств.</span><span class="sxs-lookup"><span data-stu-id="e27d2-123">Apart from the Query object model, SharePoint also provides a Search REST service that you can use to query the search index with your client or mobile applications.</span></span> <span data-ttu-id="e27d2-124">Службы поиска REST поддерживает запросов HTTP POST и HTTP GET.</span><span class="sxs-lookup"><span data-stu-id="e27d2-124">The Search REST service supports both HTTP POST and HTTP GET requests.</span></span> <span data-ttu-id="e27d2-125">Дополнительные сведения о создании коды URI для этих запросов [службы поиска REST](sharepoint-search-rest-api-overview.md#bk_queryrest)см.</span><span class="sxs-lookup"><span data-stu-id="e27d2-125">For more information on how to construct URIs for these requests, see  [Querying with the Search REST service](sharepoint-search-rest-api-overview.md#bk_queryrest).</span></span>
  
    
    

## <a name="sort-search-results-by-rank"></a><span data-ttu-id="e27d2-126">Сортировка результатов поиска по рангу</span><span class="sxs-lookup"><span data-stu-id="e27d2-126">Sort search results by rank</span></span>
<span data-ttu-id="e27d2-127"><a name="SP15_Sort_search_resuilts_by_rank"> </a></span><span class="sxs-lookup"><span data-stu-id="e27d2-127"></span></span>

<span data-ttu-id="e27d2-128">По умолчанию результаты сортируются по степени релевантности.</span><span class="sxs-lookup"><span data-stu-id="e27d2-128">By default, search results are sorted by relevance rank.</span></span> <span data-ttu-id="e27d2-129">Это означает, что SharePoint помещает наиболее подходящих результатов в верхней части окна, в наборе результатов поиска.</span><span class="sxs-lookup"><span data-stu-id="e27d2-129">This means that SharePoint places the most relevant results on top in the search result set.</span></span> <span data-ttu-id="e27d2-130">При сортировке по рангу результаты всегда сортируются в порядке убывания.</span><span class="sxs-lookup"><span data-stu-id="e27d2-130">If you sort by rank, the results are always sorted in descending order.</span></span> <span data-ttu-id="e27d2-131">Однако можно изменить порядок сортировки по возрастанию с помощью [SortDirection()](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.SortDirection.aspx) .</span><span class="sxs-lookup"><span data-stu-id="e27d2-131">But you can change the sort order to ascending by using  [SortDirection()](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.SortDirection.aspx) .</span></span>
  
    
    
<span data-ttu-id="e27d2-132">Также вы можете влиять ранга вычислений в строке запроса в одном из двух способов:</span><span class="sxs-lookup"><span data-stu-id="e27d2-132">You can also influence the rank calculation in the query string, in one of two ways:</span></span>
  
    
    

- <span data-ttu-id="e27d2-p108">С помощью оператора **XRANK**, доступные в [Справочник по синтаксису языка запросов по ключевым словам (KQL)](keyword-query-language-kql-syntax-reference.md) и [справочник по синтаксису языка запросов FAST (FQL)](fast-query-language-fql-syntax-reference.md). Применение условного ранга повышение с учетом Если условия запроса можно использовать **XRANK**.</span><span class="sxs-lookup"><span data-stu-id="e27d2-p108">By using the **XRANK** operator available in [Keyword Query Language (KQL) syntax reference](keyword-query-language-kql-syntax-reference.md) and [FAST Query Language (FQL) syntax reference](fast-query-language-fql-syntax-reference.md). You can use **XRANK** to apply a conditional rank boosting if a specific query condition is met.</span></span>
    
  
- <span data-ttu-id="e27d2-p109">Выбрав вес релевантности для динамического ранжирования. При использовании FQL, можно указать вес отдельных релевантности для каждого оператора **STRING**.</span><span class="sxs-lookup"><span data-stu-id="e27d2-p109">By choosing a relevance weight for dynamic ranking. When using FQL, you can specify an individual relevance weight for each **STRING** operator.</span></span>
    
  

## <a name="sort-search-results-by-managed-property-value"></a><span data-ttu-id="e27d2-137">Сортировка результатов поиска по значению управляемого свойства</span><span class="sxs-lookup"><span data-stu-id="e27d2-137">Sort search results by managed property value</span></span>
<span data-ttu-id="e27d2-138"><a name="SP15_Sort_search_results_by_managed_property_value"> </a></span><span class="sxs-lookup"><span data-stu-id="e27d2-138"></span></span>

<span data-ttu-id="e27d2-139">Можно задать сортировку результатов поиска на основе значения одного или нескольких управляемых свойств.</span><span class="sxs-lookup"><span data-stu-id="e27d2-139">You can specify search result sorting based on the value of one or more managed properties.</span></span> <span data-ttu-id="e27d2-140">Это означает, что SharePoint выполняет сортировку на основе всех результатов, соответствующих запросу.</span><span class="sxs-lookup"><span data-stu-id="e27d2-140">This means that SharePoint performs the sorting based on all results that match the query.</span></span>
  
    
    
<span data-ttu-id="e27d2-p111">Можно сортировать на основе текста и числовых свойств. Для свойства: текстовое порядок сортировки основано на стандартный текст сортировки. С другой стороны для числовых свойств (включая управляемых свойств типа  [DateTime](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.DateTime.aspx) ), сортировку на основе числового значения.</span><span class="sxs-lookup"><span data-stu-id="e27d2-p111">You can sort based on text and numeric properties. For text properties, the sorting is based on standard text string sorting. In contrast, for numeric properties (including managed properties of type  [DateTime](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.DateTime.aspx) ), the sorting is based on numeric value.</span></span>
  
    
    

### <a name="example"></a><span data-ttu-id="e27d2-144">Пример</span><span class="sxs-lookup"><span data-stu-id="e27d2-144">Example</span></span>

<span data-ttu-id="e27d2-145">Следующем примере показано, как для сортировки результатов поиска с помощью **Size** управляемого свойства.</span><span class="sxs-lookup"><span data-stu-id="e27d2-145">The following example shows how to sort search results by using the **Size** managed property.</span></span>
  
    
    

```cs

using (var context = new ClientContext("http://localhost"))
{
    var query = new KeywordQuery(context)
    {
        QueryText = "home"
    };
    query.SortList.Add("Size", SortDirection.Descending);

    var executor = new SearchExecutor(context);
    var results = executor.ExecuteQuery(query);

    context.ExecuteQuery();

    foreach (var result in results.Value[0].ResultRows)
    { 
        Console.WriteLine(result["Title"] + " Size:" + result["Size"]);
    }
}
```

<span data-ttu-id="e27d2-146">Кроме того можно использовать для сортировки результатов поиска с помощью свойства **Size** с при следующем вызове Search REST API.</span><span class="sxs-lookup"><span data-stu-id="e27d2-146">Alternatively, you could use the Search REST API to sort search results by using the **Size** property with the following call.</span></span>
  
    
    



```HTML

http://localhost/_api/search/query?querytext='home'&amp;sortlist='size:descending'
```


## <a name="sort-search-results-by-a-formula-expression"></a><span data-ttu-id="e27d2-147">Сортировка результатов поиска по формуле</span><span class="sxs-lookup"><span data-stu-id="e27d2-147">Sort search results by a formula expression</span></span>
<span data-ttu-id="e27d2-148"><a name="SP15_Sort_search_results_by_formula"> </a></span><span class="sxs-lookup"><span data-stu-id="e27d2-148"></span></span>

<span data-ttu-id="e27d2-149">Можно задать сортировку результатов поиска на основании спецификации, в которой значения для сортировки создаются с помощью математической формулы.</span><span class="sxs-lookup"><span data-stu-id="e27d2-149">You can specify search result sorting based on a sort specification that uses a mathematical formula to create the sorting value.</span></span>
  
    
    
<span data-ttu-id="e27d2-p112">Сортировка по формуле компонента  это расширение одноуровневая и многоуровневой сортировка функциональные возможности для результатов поиска. Позволяет задать формулу управляемого свойства в качестве критерия сортировки.</span><span class="sxs-lookup"><span data-stu-id="e27d2-p112">The sort by formula feature is an extension of the single-level and multilevel sorting functionality for search results. The feature enables you to specify a formula instead of a managed property as sorting criteria.</span></span> 
  
    
    
<span data-ttu-id="e27d2-152">При сортировке по формуле можно применять математические операции к значению одного или нескольких управляемых свойств для каждого элемента в результатах запроса.</span><span class="sxs-lookup"><span data-stu-id="e27d2-152">By using the sort by formula feature, you can apply mathematical operations on the value of one or more managed properties for each item in the query result.</span></span>
  
    
    
<span data-ttu-id="e27d2-153">Ниже приведены примеры, которые можно реализовать с помощью формулы задание сортировки результатов поиска.</span><span class="sxs-lookup"><span data-stu-id="e27d2-153">The following are examples that can be implemented by using a formula to specify search result sorting:</span></span>
  
    
    

- <span data-ttu-id="e27d2-154">Алгоритм K ближайших соседей для классификации документов.</span><span class="sxs-lookup"><span data-stu-id="e27d2-154">K-nearest neighbor algorithm to classify documents.</span></span>
    
  
- <span data-ttu-id="e27d2-155">Евклидово или манхэттенское расстояние для расчета географических расстояний.</span><span class="sxs-lookup"><span data-stu-id="e27d2-155">Euclidean distance or Manhattan distance to calculate geographical distances.</span></span>
    
  
- <span data-ttu-id="e27d2-156">Предпочитаемое значение. Например, для сортировки документов на основании того, насколько сильно отличается значение данного управляемого свойства от предпочитаемого значения.</span><span class="sxs-lookup"><span data-stu-id="e27d2-156">Preferred value, for example, to sort documents based on how far a given managed property value is from a preferred value.</span></span>
    
  
<span data-ttu-id="e27d2-157">Сортировка по формуле компонента не включает контроля статистических динамических параметров ранга, таких как частота употребления или степень сходства.</span><span class="sxs-lookup"><span data-stu-id="e27d2-157">The sort by formula feature does not include control of statistical dynamic rank parameters, such as term frequency and proximity.</span></span>
  
    
    
<span data-ttu-id="e27d2-p113">Формула вычисляется слева направо, в ней используется стандартная очередность математических операторов: сначала вычисляются функции и выражения в скобках, затем  операции умножения и деления, и наконец  операции сложения и вычитания.</span><span class="sxs-lookup"><span data-stu-id="e27d2-p113">The formula is evaluated left to right and uses standard mathematical-operator precedence. That is, functions and parenthetical groups are evaluated first, multiplication and division operations are performed next, and addition and subtraction operations are performed last.</span></span>
  
    
    

> <span data-ttu-id="e27d2-160">**Важные:** Конечный результат формулы должен быть в диапазоне от 32-разрядное целое число со знаком.</span><span class="sxs-lookup"><span data-stu-id="e27d2-160">**Important:** The final result of a formula must be in the value range of a 32-bit signed integer.</span></span> <span data-ttu-id="e27d2-161">В противном случае порядок сортировки неверно.</span><span class="sxs-lookup"><span data-stu-id="e27d2-161">Otherwise, the sorting may be incorrect.</span></span> 
  
    
    


### <a name="specifying-the-sort-formula-in-a-query"></a><span data-ttu-id="e27d2-162">Настройка формулы сортировки в запросе</span><span class="sxs-lookup"><span data-stu-id="e27d2-162">Specifying the sort formula in a query</span></span>

<span data-ttu-id="e27d2-163">В спецификации сортировки запроса указывается формула сортировки вместо управляемого свойства.</span><span class="sxs-lookup"><span data-stu-id="e27d2-163">You specify a sort formula instead of a managed property in the sort specification of the query request.</span></span>
  
    
    
<span data-ttu-id="e27d2-164">Спецификация сортировки имеет следующий формат:  `[formula:<sort-formula>]`</span><span class="sxs-lookup"><span data-stu-id="e27d2-164">The sort specification has the following format:  `[formula:<sort-formula>]`</span></span>
  
    
    
<span data-ttu-id="e27d2-165">В этом формате  _<sort-formula>_  это выражение формулы сортировки.</span><span class="sxs-lookup"><span data-stu-id="e27d2-165">In the format,  _<sort-formula>_ is the sort formula expression.</span></span>
  
> [!NOTE]
> <span data-ttu-id="e27d2-166">[!Примечание] Квадратные скобки являются частью синтаксиса спецификации сортировки.</span><span class="sxs-lookup"><span data-stu-id="e27d2-166">The square brackets are part of the sort specification syntax.</span></span> 
  
    
    

<span data-ttu-id="e27d2-p115">Направление сортировки по умолчанию  по убыванию. Можно также использовать формулу, которая сортирует в порядке возрастания значения, например, если формула указывает географических расстояний.</span><span class="sxs-lookup"><span data-stu-id="e27d2-p115">The default sort direction is descending. You may also use a formula that sorts by ascending value, for example, if the formula specifies a geographical distance.</span></span>
  
    
    
<span data-ttu-id="e27d2-169">В следующем примере кода показано, как задать сортировки по формуле в порядке возрастания с помощью объектной модели запросов.</span><span class="sxs-lookup"><span data-stu-id="e27d2-169">The following code example shows how to specify sort by formula with ascending sort order by using the Query object model.</span></span>
  
    
    



```cs
using (var context = new ClientContext("http://localhost"))
{
    var query = new KeywordQuery(context)
    {
        QueryText = "home"
    };
    query.SortList.Add("[formula:abs(2000-size)]", SortDirection.Ascending);

    var executor = new SearchExecutor(context);
    var results = executor.ExecuteQuery(query);

    context.ExecuteQuery();

    foreach (var result in results.Value[0].ResultRows)
    { 
        Console.WriteLine(result["Title"]);
    }
}
```

<span data-ttu-id="e27d2-170">Кроме того можно использовать для сортировки результатов поиска с помощью свойства **Size** с при следующем вызове Search REST API.</span><span class="sxs-lookup"><span data-stu-id="e27d2-170">Alternatively, you could use the Search REST API to sort search results by using the **Size** property with the following call.</span></span>
  
    
    



```HTML

http://localhost/_api/search/query?querytext='home'&amp;sortlist='[formula:abs(2000-size)]:ascending'

```


### <a name="using-managed-properties-in-the-sort-formula"></a><span data-ttu-id="e27d2-171">Использование управляемых свойств в формулы сортировки</span><span class="sxs-lookup"><span data-stu-id="e27d2-171">Using managed properties in the sort formula</span></span>

<span data-ttu-id="e27d2-p116">Формула сортировки можно применять на значение управляемых свойств типа  [Integer](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Integer.aspx) , [Decimal](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Decimal.aspx) и [Datetime()](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Datetime.aspx) . Необходимо включить сортировку для указанного управляемого свойства в схеме поиска.</span><span class="sxs-lookup"><span data-stu-id="e27d2-p116">You can apply a sort formula on the value of managed properties of type  [Integer](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Integer.aspx) , [Decimal](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Decimal.aspx) , and [Datetime()](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Datetime.aspx) . You must enable sorting for the specified managed property in the search schema.</span></span>
  
    
    
<span data-ttu-id="e27d2-174">Для получения дополнительных управляемых свойств из типа  [Decimal](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Decimal.aspx) , значение умножается на 10 ^(decimal digits) перед использованием в вычислении формулы.</span><span class="sxs-lookup"><span data-stu-id="e27d2-174">For more managed properties of type  [Decimal](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Decimal.aspx) , the value is multiplied by 10^(decimal digits) before being used in the formula evaluation.</span></span>
  
    
    
<span data-ttu-id="e27d2-p117">Для управляемых свойств типа  [Datetime()](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Datetime.aspx) значение преобразуется в номер 100 наносекунд начиная с 1 января 29000 штрих-КОДЫ перед использованием в вычислении формулы. Существует 366 дней в году.</span><span class="sxs-lookup"><span data-stu-id="e27d2-p117">For managed properties of type  [Datetime()](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Datetime.aspx) , the value is converted to the number of 100 nanoseconds since January 1 29000 BC before being used in the formula evaluation. There are 366 days in the year.</span></span>
  
    
    

### <a name="sort-formula-expressions"></a><span data-ttu-id="e27d2-177">Выражения формулы сортировки</span><span class="sxs-lookup"><span data-stu-id="e27d2-177">Sort formula expressions</span></span>

<span data-ttu-id="e27d2-p118">В таблице 1 перечислены функции, которые можно использовать в выражение формулы сортировки. Выражение не должно содержать пробелов.</span><span class="sxs-lookup"><span data-stu-id="e27d2-p118">Table 1 lists the functions you can use in the sort formula expression. The expression must not contain spaces.</span></span>
  
    
    

<span data-ttu-id="e27d2-180">**Таблица 1. Функции для выражений формул сортировки**</span><span class="sxs-lookup"><span data-stu-id="e27d2-180">**Table 1. Functions for sort formula expressions**</span></span>


|<span data-ttu-id="e27d2-181">**Функция**</span><span class="sxs-lookup"><span data-stu-id="e27d2-181">**Function**</span></span>|<span data-ttu-id="e27d2-182">**Описание**</span><span class="sxs-lookup"><span data-stu-id="e27d2-182">**Description**</span></span>|
|:-----|:-----|
|**+** <br/> |<span data-ttu-id="e27d2-183">Задает операцию сложения.</span><span class="sxs-lookup"><span data-stu-id="e27d2-183">Specifies addition.</span></span>  <br/> |
|**-** <br/> |<span data-ttu-id="e27d2-184">Задает операцию вычитания.</span><span class="sxs-lookup"><span data-stu-id="e27d2-184">Specifies subtraction.</span></span>  <br/> |
|* <br/> |<span data-ttu-id="e27d2-185">Задает операцию умножения.</span><span class="sxs-lookup"><span data-stu-id="e27d2-185">Specifies multiplication.</span></span>  <br/> |
|**/** <br/> |<span data-ttu-id="e27d2-186">Определяет операцию деления.</span><span class="sxs-lookup"><span data-stu-id="e27d2-186">Specifies division.</span></span>  <br/> <span data-ttu-id="e27d2-187">**Примечание**: по умолчанию, деление на ноль вызывает исключение, а запрос возвращает сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="e27d2-187">**Note**: By default, a division by zero results in an exception, and the query returns with an error.</span></span> <span data-ttu-id="e27d2-188">С помощью оператора **errtolast** , можно избежать ошибок, запросов и вместо этого размещение элементов со сбоями в конце набора результатов.</span><span class="sxs-lookup"><span data-stu-id="e27d2-188">By using the **errtolast** operator, you can avoid the query error and instead place the failing items at the end of the result set.</span></span>          |
|<span data-ttu-id="e27d2-189">**rank**</span><span class="sxs-lookup"><span data-stu-id="e27d2-189">**rank**</span></span> <br/> |<span data-ttu-id="e27d2-190">Специальное ключевое слово, представляющее динамический ранг элемента.</span><span class="sxs-lookup"><span data-stu-id="e27d2-190">A special keyword that represents the dynamic rank of an item.</span></span>  <br/> <span data-ttu-id="e27d2-191">Пример: формула  `abs(rank-100)` в качестве критерия сортировки задает величину отличия от ранга 100.</span><span class="sxs-lookup"><span data-stu-id="e27d2-191">Example:  `abs(rank-100)` will use the distance from rank value 100 as the sorting criteria.</span></span> <br/> |
|<span data-ttu-id="e27d2-192">**[0-9]. +**</span><span class="sxs-lookup"><span data-stu-id="e27d2-192">**[0-9.]+**</span></span> <br/> |<span data-ttu-id="e27d2-193">Указывает, что числа можно задавать в формате целых значений или значений двойной точности.</span><span class="sxs-lookup"><span data-stu-id="e27d2-193">Specifies that numbers can be given as integer or double values.</span></span>  <br/> <span data-ttu-id="e27d2-194">Примеры: 503, 3.14, 5.4352262</span><span class="sxs-lookup"><span data-stu-id="e27d2-194">Examples: 503, 3.14, 5.4352262</span></span>  <br/> |
|<span data-ttu-id="e27d2-195">**[a-z0-9]+]**</span><span class="sxs-lookup"><span data-stu-id="e27d2-195">**[a-z0-9]+]**</span></span> <br/> |<span data-ttu-id="e27d2-p120">Указывает, что любые последовательность знаков, не распознается как имя функции обрабатывается как имя управляемого свойства. Необходимо включить сортировку для указанного управляемого свойства в схеме поиска.</span><span class="sxs-lookup"><span data-stu-id="e27d2-p120">Specifies that any character sequence not recognized as a function name is treated as a managed property name. You must enable sorting for the specified managed property in the search schema.  </span></span><br/> <span data-ttu-id="e27d2-p121">Пример: Определение управляемого свойства с именем **height** с включена сортировка. Это позволяет использовать «высота» в качестве выражения в формуле. Формула, будут использовать значение **height** управляемого свойства. </span><span class="sxs-lookup"><span data-stu-id="e27d2-p121">Example: You can define a managed property named **height** with sorting enabled. This enables you to use "height" as an expression in the formula. The formula will use the value of the **height** managed property. </span></span><br/> |
|<span data-ttu-id="e27d2-201">**( and )**</span><span class="sxs-lookup"><span data-stu-id="e27d2-201">**( and )**</span></span> <br/> |<span data-ttu-id="e27d2-202">Используется для группирования с целью обеспечения точного порядка вычислений.</span><span class="sxs-lookup"><span data-stu-id="e27d2-202">Used to group calculations ensuring correct precedence.</span></span>  <br/> <span data-ttu-id="e27d2-203">Пример: 4*(3+2)</span><span class="sxs-lookup"><span data-stu-id="e27d2-203">Example: 4*(3+2)</span></span>  <br/> |
|<span data-ttu-id="e27d2-204">**sqrt(n)**</span><span class="sxs-lookup"><span data-stu-id="e27d2-204">**sqrt(n)**</span></span> <br/> |<span data-ttu-id="e27d2-205">Квадратный корень из  _n_.</span><span class="sxs-lookup"><span data-stu-id="e27d2-205">The square root of  _n_.</span></span>  <br/> |
|<span data-ttu-id="e27d2-206">**exp(n)**</span><span class="sxs-lookup"><span data-stu-id="e27d2-206">**exp(n)**</span></span> <br/> |<span data-ttu-id="e27d2-207">Экспоненциальная функция, эквивалентная  *pow(2,71828182846,n)*  .</span><span class="sxs-lookup"><span data-stu-id="e27d2-207">The exponential function that is equivalent to  *pow(2.71828182846,n)*</span></span>  <br/> |
|<span data-ttu-id="e27d2-208">**log(n)**</span><span class="sxs-lookup"><span data-stu-id="e27d2-208">**log(n)**</span></span> <br/> |<span data-ttu-id="e27d2-209">Натуральный логарифм от  _n_.</span><span class="sxs-lookup"><span data-stu-id="e27d2-209">The natural logarithm of  _n_.</span></span>  <br/> |
|<span data-ttu-id="e27d2-210">**abs(n)**</span><span class="sxs-lookup"><span data-stu-id="e27d2-210">**abs(n)**</span></span> <br/> |<span data-ttu-id="e27d2-211">Модуль  _n_.</span><span class="sxs-lookup"><span data-stu-id="e27d2-211">The absolute value of  _n_.</span></span>  <br/> |
|<span data-ttu-id="e27d2-212">**ceil(n)**</span><span class="sxs-lookup"><span data-stu-id="e27d2-212">**ceil(n)**</span></span> <br/> |<span data-ttu-id="e27d2-p122">Округление  _n_ вверх. Если _n_  не целое число, оно округляется вверх до следующего целого. Если _n_  целое число, то используется значение _n_. </span><span class="sxs-lookup"><span data-stu-id="e27d2-p122">The ceiling of  _n_. That is, if  _n_ is not a whole number, round up to the next whole number. If _n_ is a whole number, use _n_.  </span></span><br/> |
|<span data-ttu-id="e27d2-216">**floor(n)**</span><span class="sxs-lookup"><span data-stu-id="e27d2-216">**floor(n)**</span></span> <br/> |<span data-ttu-id="e27d2-p123">Округление  _n_ вниз. Если _n_  не целое число, оно округляется вниз до следующего целого. Если _n_  целое число, то используется значение _n_. </span><span class="sxs-lookup"><span data-stu-id="e27d2-p123">The floor of  _n_. That is, if  _n_ is not a whole number, round down to the next whole number. If _n_ is a whole number, use _n_.  </span></span><br/> |
|<span data-ttu-id="e27d2-220">**round(n)**</span><span class="sxs-lookup"><span data-stu-id="e27d2-220">**round(n)**</span></span> <br/> |<span data-ttu-id="e27d2-p124">Округление  _n_ до ближайшего даже целые числа. Также известные как «Банкиров округления» или «Round наполовину равное». </span><span class="sxs-lookup"><span data-stu-id="e27d2-p124">The rounding of  _n_ to the nearest even whole number. Also known as "Bankers rounding" or "Round half to even". </span></span><br/> |
|<span data-ttu-id="e27d2-223">**sin(n)**</span><span class="sxs-lookup"><span data-stu-id="e27d2-223">**sin(n)**</span></span> <br/> |<span data-ttu-id="e27d2-224">Синус значения  _n_ в радианах.</span><span class="sxs-lookup"><span data-stu-id="e27d2-224">The sine of  _n_ radians.</span></span> <br/> |
|<span data-ttu-id="e27d2-225">**cos(n)**</span><span class="sxs-lookup"><span data-stu-id="e27d2-225">**cos(n)**</span></span> <br/> |<span data-ttu-id="e27d2-226">Косинус значения  _n_ в радианах.</span><span class="sxs-lookup"><span data-stu-id="e27d2-226">The cosine of  _n_ radians.</span></span> <br/> |
|<span data-ttu-id="e27d2-227">**tan(n)**</span><span class="sxs-lookup"><span data-stu-id="e27d2-227">**tan(n)**</span></span> <br/> |<span data-ttu-id="e27d2-228">Тангенс значения  _n_ в радианах.</span><span class="sxs-lookup"><span data-stu-id="e27d2-228">The tangent of  _n_ radians.</span></span> <br/> |
|<span data-ttu-id="e27d2-229">**asin(n)**</span><span class="sxs-lookup"><span data-stu-id="e27d2-229">**asin(n)**</span></span> <br/> |<span data-ttu-id="e27d2-230">Арксинус значения  _n_ в радианах.</span><span class="sxs-lookup"><span data-stu-id="e27d2-230">The arcsine, in radians, of  _n_.</span></span>  <br/> |
|<span data-ttu-id="e27d2-231">**acos(n)**</span><span class="sxs-lookup"><span data-stu-id="e27d2-231">**acos(n)**</span></span> <br/> |<span data-ttu-id="e27d2-232">Арккосинус значения  _n_ в радианах.</span><span class="sxs-lookup"><span data-stu-id="e27d2-232">The arccosine, in radians, of  _n_.</span></span>  <br/> |
|<span data-ttu-id="e27d2-233">**atan(n)**</span><span class="sxs-lookup"><span data-stu-id="e27d2-233">**atan(n)**</span></span> <br/> |<span data-ttu-id="e27d2-234">Арктангенс значения  _n_ в радианах.</span><span class="sxs-lookup"><span data-stu-id="e27d2-234">The arctangent, in radians, of  _n_.</span></span>  <br/> |
|<span data-ttu-id="e27d2-235">**pow(x,y)**</span><span class="sxs-lookup"><span data-stu-id="e27d2-235">**pow(x,y)**</span></span> <br/> |<span data-ttu-id="e27d2-236">Значение  _x_ в степени _y_.</span><span class="sxs-lookup"><span data-stu-id="e27d2-236">The value of  _x_ raised to the power of _y_.</span></span>  <br/> <span data-ttu-id="e27d2-237">**Примечание**: значение _y_ должно быть действительное число.</span><span class="sxs-lookup"><span data-stu-id="e27d2-237">**Note**: The value of  _y_ must be a real number.</span></span>          |
|<span data-ttu-id="e27d2-238">**atan2(y,x)**</span><span class="sxs-lookup"><span data-stu-id="e27d2-238">**atan2(y,x)**</span></span> <br/> |<span data-ttu-id="e27d2-239">Арктангенс по двум аргументам от угла в радианах между положительным направлением оси x и указанной декартовой координатой (x,y).</span><span class="sxs-lookup"><span data-stu-id="e27d2-239">A two-argument arctangent of the angle in radians between the positive x axis and the specified Cartesian coordinate (x,y).</span></span>  <br/> |
|<span data-ttu-id="e27d2-240">**bucket(b,n1,n2,…)**</span><span class="sxs-lookup"><span data-stu-id="e27d2-240">**bucket(b,n1,n2,…)**</span></span> <br/> |<span data-ttu-id="e27d2-241">Оператор, который можно использовать для получения отдельных значений в указанных диапазонах распределения значений для выражения.</span><span class="sxs-lookup"><span data-stu-id="e27d2-241">An operator that can be used to provide discrete values for given value distribution ranges for an expression.</span></span>  <br/> <span data-ttu-id="e27d2-p125">Выражение  _b_ может быть управляемое свойство или других выражение формулы. Аргументы _n1, n2, …_ представляют собой числовые пороговые значения. Можно указать произвольное число выполненных пороговые значения интервалов. </span><span class="sxs-lookup"><span data-stu-id="e27d2-p125">The expression  _b_ can be a managed property or any other formula expression. The arguments _n1, n2, …_ represent numeric thresholds. You can specify an arbitrary number of bucket thresholds. </span></span><br/> <span data-ttu-id="e27d2-246">**Примечание**: необходимо расположить аргументы _n1, n2, n3..._</span><span class="sxs-lookup"><span data-stu-id="e27d2-246">**Note**: You must arrange the arguments  _n1, n2, n3, …_</span></span> <span data-ttu-id="e27d2-247">в следующем порядке: `n1 < n2 < n3 < ...` с `n1 >= 0`.</span><span class="sxs-lookup"><span data-stu-id="e27d2-247">in the following order: `n1 < n2 < n3 < ...` with `n1 >= 0`.</span></span>           <span data-ttu-id="e27d2-248">Значение, заданное для ввода выражения _b_ округляется вниз до ближайших порогового значения числовой присвоенное.</span><span class="sxs-lookup"><span data-stu-id="e27d2-248">A given value for the input expression  _b_ is rounded down to the closest numeric threshold given.</span></span> <span data-ttu-id="e27d2-249">Если меньше, чем наименьшее пороговое значение присвоенное, полученное значение равно нулю.</span><span class="sxs-lookup"><span data-stu-id="e27d2-249">If lower than the lowest threshold given, the resulting value is zero.</span></span> <br/> |
|<span data-ttu-id="e27d2-250">**errtolast(x)**</span><span class="sxs-lookup"><span data-stu-id="e27d2-250">**errtolast(x)**</span></span> <br/> |<span data-ttu-id="e27d2-p127">Оператор, который можно использовать для управления обработкой выражений формулы;  _x_ может быть любым выражением формулы. Если вычисление этого выражения формулы ведет к математическому исключению для элемента в наборе результатов, например, к делению на ноль, эти элементы помещаются в конец списка сортировки, независимо от указанного направления сортировки.</span><span class="sxs-lookup"><span data-stu-id="e27d2-p127">An operator that can be used to control how to handle formula exceptions;  _x_ can be any formula expression. If the calculation of this formula expression leads to a mathematical exception for an item in the result set, such as division by zero, these items appear at the end of the sort list, regardless of specified sort direction. </span></span><br/> |
   

### <a name="performance-characteristics-for-sort-by-formula"></a><span data-ttu-id="e27d2-253">Характеристики производительности для сортировки по формуле</span><span class="sxs-lookup"><span data-stu-id="e27d2-253">Performance characteristics for sort by formula</span></span>

<span data-ttu-id="e27d2-p128">Использование формулы подразумевает, что вычисления формулы применяются ко всем соответствующим элементам в наборе результатов. Это значит, что производительность запроса зависит от числа соответствующих элементов.</span><span class="sxs-lookup"><span data-stu-id="e27d2-p128">Using a sort formula implies that the formula calculations are applied to all matching items in the result set. This means that the query performance impact depends on the number of items that match the query.</span></span>
  
    
    
<span data-ttu-id="e27d2-256">Длинные формулы со многими операторами требуют больше времени на обработку, чем короткие формулы.</span><span class="sxs-lookup"><span data-stu-id="e27d2-256">Long formulas with many operators require more processing time than short formulas.</span></span>
  
    
    

### <a name="using-sort-by-formula-for-geographical-distance"></a><span data-ttu-id="e27d2-257">Использование сортировки по формуле для географических расстояний</span><span class="sxs-lookup"><span data-stu-id="e27d2-257">Using sort by formula for geographical distance</span></span>

<span data-ttu-id="e27d2-p129">Сортировку по формуле можно использовать для ранжирования на основании расстояний. Для этого требуется включить управляемые свойства, представляющие широту и долготу каждого элемента.</span><span class="sxs-lookup"><span data-stu-id="e27d2-p129">You can use sort by formula to apply a ranking based on distance. This requires that you include managed properties that represent the latitude and longitude of each item.</span></span>
  
    
    
<span data-ttu-id="e27d2-260">Например, можно использовать одну из следующих стандартных формул.</span><span class="sxs-lookup"><span data-stu-id="e27d2-260">For example, you can use one of the following standard formulas:</span></span>
  
    
    

- <span data-ttu-id="e27d2-261">Манхэттенское расстояние.</span><span class="sxs-lookup"><span data-stu-id="e27d2-261">Manhattan distance</span></span>
    
  
- <span data-ttu-id="e27d2-262">Евклидово расстояние См. пример 2.</span><span class="sxs-lookup"><span data-stu-id="e27d2-262">Euclidian distance (see example 2)</span></span>
    
  
- <span data-ttu-id="e27d2-263">Формула haversine.</span><span class="sxs-lookup"><span data-stu-id="e27d2-263">Haversine formula</span></span>
    
  

> <span data-ttu-id="e27d2-264">**Важные:** Использование управляемых свойств типа **Decimal** или **Float** для представления значений широта и долгота.</span><span class="sxs-lookup"><span data-stu-id="e27d2-264">**Important:** Use managed properties of type **Decimal** or **Float** to represent the latitude and longitude values.</span></span>
  
    
    


### <a name="examples"></a><span data-ttu-id="e27d2-265">Примеры</span><span class="sxs-lookup"><span data-stu-id="e27d2-265">Examples</span></span>

<span data-ttu-id="e27d2-266">В приведенных ниже примерах показано, как задать формулу сортировки, с помощью объектной модели запросов.</span><span class="sxs-lookup"><span data-stu-id="e27d2-266">The following examples show how to specify the sort formula using the Query object model.</span></span>
  
    
    
 <span data-ttu-id="e27d2-p130">**Пример 1.** Размещение элементов, значение управляемого свойства **height** которых ближе всего к 20, в начале набора результатов.</span><span class="sxs-lookup"><span data-stu-id="e27d2-p130">**Example 1.** Place the items that have the **height** managed property closest to 20 on top of the result list.</span></span>
  
    
    



```cs

using (var context = new ClientContext("http://localhost"))
{
    var query = new KeywordQuery(context)
    {
        QueryText = "home"
    };
    query.SortList.Add("[formula:abs(20-height)]", SortDirection.Ascending);

    var executor = new SearchExecutor(context);
    var results = executor.ExecuteQuery(query);

    context.ExecuteQuery();

    foreach (var result in results.Value[0].ResultRows)
    { 
        Console.WriteLine(result["Title"]);
    }
}
```

<span data-ttu-id="e27d2-269">Кроме того можно использовать Search REST API для размещения элементов, которые имеют **height** управляемых свойств, наиболее близкого к 20 вверху списка результатов на следующий вызов.</span><span class="sxs-lookup"><span data-stu-id="e27d2-269">Alternatively, you could use the Search REST API to place the items that have the **height** managed property closest to 20 on top of the result list, with the following call.</span></span>
  
    
    



```HTML

http://localhost/_api/search/query?querytext='home'&amp;sortlist='[formula:abs(20-height)]:ascending
```

 <span data-ttu-id="e27d2-p131">**В примере 2.** Сортировка по true объемных евклидово из заданной позиции (например, положение пользователя) на основе сведений позицию, которая предоставляется в управляемых свойств **latitude**, **longitude** и **height**. Следующая формула позволяет трехмерной евклидово предположить, что базового положения представляет 50/100/200 (Широта и долгота и высота).</span><span class="sxs-lookup"><span data-stu-id="e27d2-p131">**Example 2.** Sort by true 3-D Euclidean distance from a given position (for example, user's position) based on position information that is provided in the managed properties **latitude**, **longitude** and **height**. The following formula provides the 3-D Euclidean distance, given that the base position is 50/100/200 (latitude/longitude/height).</span></span>
  
    
    
 `sqrt(pow(50-latitude,2)+pow(100-longitude,2)+pow(200-height,2))`
  
    
    
<span data-ttu-id="e27d2-273">Если вы хотите применить на основе расстояние сортировки (не объединения расстояние с другими параметрами в формуле), можно удалить компонент  `sqrt()` как не изменяет последовательность сортировки; но улучшает производительность запросов.</span><span class="sxs-lookup"><span data-stu-id="e27d2-273">If you want to apply a distance-based sorting (not combining the distance with other parameters in a formula), you can remove the  `sqrt()` component, as it does not change the sorting sequence; but it improves the query performance.</span></span>
  
    
    



```cs
using (var context = new ClientContext("http://localhost"))
{
    var query = new KeywordQuery(context)
    {
        QueryText = "home"
    };
    query.SortList.Add("[formula:pow(50-latitude,2)+pow(100-longitude,2)+pow(200-height,2)]", SortDirection.Ascending);

    var executor = new SearchExecutor(context);
    var results = executor.ExecuteQuery(query);

    context.ExecuteQuery();

    foreach (var result in results.Value[0].ResultRows)
    { 
        Console.WriteLine(result["Title"]);
    }
}
```

 <span data-ttu-id="e27d2-p132">**В примере 3.** Round значения размера в сегменты, округления значения вниз до одно из следующих значений: 0, 5, 15, 50, 100; сортировать сначала наибольшего значения.</span><span class="sxs-lookup"><span data-stu-id="e27d2-p132">**Example 3.** Round the values of size into buckets, rounding values down to one of the following: 0, 5, 15, 50, 100; sort with largest values first.</span></span>
  
    
    



```

using (var context = new ClientContext("http://localhost"))
{
    var query = new KeywordQuery(context)
    {
        QueryText = "home"
    };
    query.SortList.Add("[formula:bucket(size,5,15,50,100)]", SortDirection.Ascending);

    var executor = new SearchExecutor(context);
    var results = executor.ExecuteQuery(query);

    context.ExecuteQuery();

    foreach (var result in results.Value[0].ResultRows)
    { 
        Console.WriteLine(result["Title"]);
    }
}
```


## <a name="sort-search-results-in-random-order"></a><span data-ttu-id="e27d2-276">Сортировка результатов поиска в случайном порядке</span><span class="sxs-lookup"><span data-stu-id="e27d2-276">Sort search results in random order</span></span>
<span data-ttu-id="e27d2-277"><a name="SP15_Sort_search_results_in_random_order"> </a></span><span class="sxs-lookup"><span data-stu-id="e27d2-277"></span></span>

<span data-ttu-id="e27d2-278">Существует и возможность сортировать результаты поиска в случайном порядке или добавлять случайный компонент в результаты сортировки.</span><span class="sxs-lookup"><span data-stu-id="e27d2-278">You may apply random sorting of the query result, or add a random component to the result sorting.</span></span>
  
    
    
<span data-ttu-id="e27d2-279">Спецификация сортировки в случайном порядке имеет следующий формат:  `[random:seed=<seed>:hashfield=<managed property>]`</span><span class="sxs-lookup"><span data-stu-id="e27d2-279">The random sort specification has the following format:  `[random:seed=<seed>:hashfield=<managed property>]`</span></span>
  
> [!NOTE]
> <span data-ttu-id="e27d2-280">[!Примечание] Квадратные скобки являются частью синтаксиса спецификации сортировки.</span><span class="sxs-lookup"><span data-stu-id="e27d2-280">The square brackets are part of the sort specification syntax.</span></span> 
  
    
    

<span data-ttu-id="e27d2-281">В таблице 2 объясняются параметры спецификации сортировки в случайном порядке.</span><span class="sxs-lookup"><span data-stu-id="e27d2-281">Table 2 explains the parameters to the random sort specification.</span></span>
  
    
    

<span data-ttu-id="e27d2-282">**Таблица 2. Параметры спецификации сортировки в случайном порядке**</span><span class="sxs-lookup"><span data-stu-id="e27d2-282">**Table 2. Parameters for the random sort specification**</span></span>


|<span data-ttu-id="e27d2-283">**Параметр**</span><span class="sxs-lookup"><span data-stu-id="e27d2-283">**Parameter**</span></span>|<span data-ttu-id="e27d2-284">**Описание**</span><span class="sxs-lookup"><span data-stu-id="e27d2-284">**Description**</span></span>|<span data-ttu-id="e27d2-285">**Обязательный**</span><span class="sxs-lookup"><span data-stu-id="e27d2-285">**Required**</span></span>|
|:-----|:-----|:-----|
| <span data-ttu-id="e27d2-286">_Seed_</span><span class="sxs-lookup"><span data-stu-id="e27d2-286">_Seed_</span></span> <br/> |<span data-ttu-id="e27d2-287">Начальное значение для создания случайного значения.</span><span class="sxs-lookup"><span data-stu-id="e27d2-287">The seed for the random value generation.</span></span>  <br/> <span data-ttu-id="e27d2-p133">Входные данные начальное значение  это функция, которая создает случайное число. В этом случайное число используется в последнем сортировка. С помощью параметра  _seed_ можно получить случайным образом отсортированный результата запроса. После обновления индекса может изменить порядок сортировки для того же запроса (при использовании того же начального значения).</span><span class="sxs-lookup"><span data-stu-id="e27d2-p133">The seed value is input to a function that generates a random number. This random number is used in the final sorting.Using only the  _seed_ option will give you a randomly sorted query result set. The sorting order for the same query (when using the same seed) may change after an index update. </span></span><br/> |<span data-ttu-id="e27d2-291">Да</span><span class="sxs-lookup"><span data-stu-id="e27d2-291">Yes</span></span>  <br/> |
| <span data-ttu-id="e27d2-292">_Hashfield_</span><span class="sxs-lookup"><span data-stu-id="e27d2-292">_Hashfield_</span></span> <br/> |<span data-ttu-id="e27d2-p134">Управляемое свойство, которое используется в качестве значения хэш-функции для создания случайного значения. Этот параметр можно использовать, чтобы убедиться, что порядок сортировки для того же запроса (при использовании того же начального значения) не изменялся после обновления индекса.</span><span class="sxs-lookup"><span data-stu-id="e27d2-p134">A managed property that is used as the hash value for the random generation. You can use this parameter to ensure that the sorting order for the same query (when using the same seed) does not change after an index update.  </span></span><br/> <span data-ttu-id="e27d2-p135">Управляемое свойство, которое должно иметь тип  [Integer](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Integer.aspx) и должен быть [Sortable()](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.Sortable.aspx) . Это управляемое свойство можно указать случайные или уникальные значения (например порядковый номер, заполненный на этапе обработки элемента). </span><span class="sxs-lookup"><span data-stu-id="e27d2-p135">The managed property must be of type  [Integer](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Integer.aspx) and must be [Sortable()](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.Sortable.aspx) . You may fill this managed property with random or unique values (for example a sequence number populated by an item processing stage). </span></span><br/> |<span data-ttu-id="e27d2-297">Нет</span><span class="sxs-lookup"><span data-stu-id="e27d2-297">No</span></span>  <br/> |
   
<span data-ttu-id="e27d2-p136">Если предоставляется одно и то же начальное значение для равнозначных запросов, то элементы будут упорядочиваться в одном и том же порядке. Это позволяет сохранять одинаковый порядок случайной сортировки при переходе по страницам результатов поиска. Чтобы сохранить один и тот же случайный порядок сортировки в случае, когда обновление индекса происходит неожиданно между запросами, используйте параметр  _hashfield_.</span><span class="sxs-lookup"><span data-stu-id="e27d2-p136">By providing the same seed for equal queries, items will be presented in the same order. This enables you to preserve the same random order when paging through search results. Use the  _hashfield_ parameter if you want to preserve the same random order when an index update accidentally occurs between the queries.</span></span>
  
    
    

### <a name="examples"></a><span data-ttu-id="e27d2-301">Примеры</span><span class="sxs-lookup"><span data-stu-id="e27d2-301">Examples</span></span>

<span data-ttu-id="e27d2-302">В приведенных ниже примерах показано, как задать сортировку в случайном порядке с помощью объектной модели запросов.</span><span class="sxs-lookup"><span data-stu-id="e27d2-302">The following examples show how to specify random sorting by using the Query object model.</span></span>
  
    
    
 <span data-ttu-id="e27d2-p137">**В примере 1.** Сортировка весь результирующий набор в случайном порядке.</span><span class="sxs-lookup"><span data-stu-id="e27d2-p137">**Example 1.** Sort the entire result set in random order.</span></span>
  
    
    



```

using (var context = new ClientContext("http://localhost"))
{
    var query = new KeywordQuery(context)
    {
        QueryText = "home"
    };
    query.SortList.Add("[random:seed=5432]", SortDirection.Ascending);

    var executor = new SearchExecutor(context);
    var results = executor.ExecuteQuery(query);

    context.ExecuteQuery();

    foreach (var result in results.Value[0].ResultRows)
    { 
        Console.WriteLine(result["Title"]);
    }
}
```

<span data-ttu-id="e27d2-305">Кроме того можно использовать API-Интерфейс REST поиска всей результаты сортируются в случайном порядке, с помощью следующих звонок.</span><span class="sxs-lookup"><span data-stu-id="e27d2-305">Alternatively, you could use the Search REST API to sort the entire result set in random order, with the following call.</span></span>
  
    
    



```HTML

http://localhost/_api/search/query?querytext='home'&amp;sortlist='[random:seed=5432]:ascending
```

 <span data-ttu-id="e27d2-p138">**В примере 2.** Сортировка весь результирующий набор в случайном порядке. Сохранение одной и той же в случайном порядке последовательности того же запроса с того же начального значения даже в том случае, если возникает коммутатору индекса. Настраиваемые управляемого свойства с именем **hashvalue** должен быть доступен в схеме поиска и заполнен случайного или последовательного числовых значений для всех индексированных элементов.</span><span class="sxs-lookup"><span data-stu-id="e27d2-p138">**Example 2.** Sort the entire result set in random order. Preserve the same random sequence for the same query with the same seed, even if an index switch occurs. A custom managed property named **hashvalue** must be available in the search schema, and populated with random or sequential numeric values for all indexed items.</span></span>
  
    
    



```cs
using (var context = new ClientContext("http://localhost"))
{
    var query = new KeywordQuery(context)
    {
        QueryText = "home"
    };
    query.SortList.Add("[random:seed=6543:hashfield=hashvalue]", SortDirection.Ascending);

    var executor = new SearchExecutor(context);
    var results = executor.ExecuteQuery(query);

    context.ExecuteQuery();

    foreach (var result in results.Value[0].ResultRows)
    { 
        Console.WriteLine(result["Title"]);
    }
}
```


## <a name="see-also"></a><span data-ttu-id="e27d2-310">См. также</span><span class="sxs-lookup"><span data-stu-id="e27d2-310">See also</span></span>
<span data-ttu-id="e27d2-311"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="e27d2-311"></span></span>


-  [<span data-ttu-id="e27d2-312">Поиск в SharePoint</span><span class="sxs-lookup"><span data-stu-id="e27d2-312">Search in SharePoint</span></span>](search-in-sharepoint.md)
    
  
-  [<span data-ttu-id="e27d2-313">Справочник по синтаксису языка запросов по ключевым словам (KQL)</span><span class="sxs-lookup"><span data-stu-id="e27d2-313">Keyword Query Language (KQL) syntax reference</span></span>](keyword-query-language-kql-syntax-reference.md)
    
  
-  [<span data-ttu-id="e27d2-314">справочник по синтаксису языка запросов FAST (FQL)</span><span class="sxs-lookup"><span data-stu-id="e27d2-314">FAST Query Language (FQL) syntax reference</span></span>](fast-query-language-fql-syntax-reference.md)
    
  
-  [<span data-ttu-id="e27d2-315">Общие сведения об API службы поиска REST для SharePoint</span><span class="sxs-lookup"><span data-stu-id="e27d2-315">SharePoint Search REST API overview</span></span>](sharepoint-search-rest-api-overview.md)
    
  
-  [<span data-ttu-id="e27d2-316">Обзор свойств для обхода и управляемых свойств в SharePoint</span><span class="sxs-lookup"><span data-stu-id="e27d2-316">Overview of crawled and managed properties in SharePoint</span></span>](http://technet.microsoft.com/en-us/library/jj219630%28office.15%29.aspx)
    
  

  
    
    
