---
title: "Руководство по синтаксису языка запросов по ключевым словам (KQL)"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: d8489f59-522f-433c-b9c1-69e597be51c7
ms.openlocfilehash: ae8691e371220e8c796267bba2f940a45219004d
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="keyword-query-language-kql-syntax-reference"></a><span data-ttu-id="9c68e-102">Руководство по синтаксису языка запросов по ключевым словам (KQL)</span><span class="sxs-lookup"><span data-stu-id="9c68e-102">Keyword Query Language (KQL) syntax reference</span></span>
<span data-ttu-id="9c68e-p101">Узнайте, как создавать KQL-запросы для Поиск в SharePoint. Этот справочник по синтаксису описывает элементы KQL-запросов, а также порядок использования ограничений свойств и операторов в таких запросах.</span><span class="sxs-lookup"><span data-stu-id="9c68e-p101">Learn to construct KQL queries for Search in SharePoint. This syntax reference describes KQL query elements and how to use property restrictions and operators in KQL queries.</span></span>
## <a name="elements-of-a-kql-query"></a><span data-ttu-id="9c68e-105">Элементы KQL-запроса</span><span class="sxs-lookup"><span data-stu-id="9c68e-105">Elements of a KQL query</span></span>
<span data-ttu-id="9c68e-106"><a name="SP15KQL_elements"> </a></span><span class="sxs-lookup"><span data-stu-id="9c68e-106"></span></span>

<span data-ttu-id="9c68e-107">KQL-запрос состоит из одного или нескольких элементов, перечисленных далее.</span><span class="sxs-lookup"><span data-stu-id="9c68e-107">A KQL query consists of one or more of the following elements:</span></span> 
  
    
    

- <span data-ttu-id="9c68e-108">Ключевые слова с произвольным текстом (слова или фразы)</span><span class="sxs-lookup"><span data-stu-id="9c68e-108">Free text-keywords—words or phrases</span></span> 
    
  
- <span data-ttu-id="9c68e-109">Ограничения свойств</span><span class="sxs-lookup"><span data-stu-id="9c68e-109">Property restrictions</span></span> 
    
  
<span data-ttu-id="9c68e-110">Элементы KQL-запросов можно комбинировать с одним или несколькими доступными операторами.</span><span class="sxs-lookup"><span data-stu-id="9c68e-110">You can combine KQL query elements with one or more of the available operators.</span></span>
  
    
    
<span data-ttu-id="9c68e-p102">KQL-запросы, которые содержат только операторы, а также пустые KQL-запросы являются недопустимыми. KQL-запросы не учитывают регистр, однако операторы указываются с учетом регистра (прописными буквами).</span><span class="sxs-lookup"><span data-stu-id="9c68e-p102">If the KQL query contains only operators or is empty, it isn't valid. KQL queries are case-insensitive but the operators are case-sensitive (uppercase).</span></span>
  
    
    

> <span data-ttu-id="9c68e-113">**Примечание.** Ограничение длины KQL-запроса зависит от способа его создания.</span><span class="sxs-lookup"><span data-stu-id="9c68e-113">**Note:** The length limit of a KQL query varies depending on how you create it.</span></span> <span data-ttu-id="9c68e-114">Если KQL-запрос создан при помощи внешнего интерфейса поиска SharePoint, доступного по умолчанию, максимальная длина составляет 2048 символов.</span><span class="sxs-lookup"><span data-stu-id="9c68e-114">If you create the KQL query by using the default SharePoint search front end, the length limit is 2,048 characters.</span></span> <span data-ttu-id="9c68e-115">Если же вы создаете KQL-запрос программным путем с помощью объектной модели запроса, ограничение длины по умолчанию составляет 4096 знаков.</span><span class="sxs-lookup"><span data-stu-id="9c68e-115">However, KQL queries you create programmatically by using the Query object model have a default length limit of 4,096 characters.</span></span> <span data-ttu-id="9c68e-116">Вы можете изменить это ограничение, увеличив количество знаков до 20 480, с помощью свойства [MaxKeywordQueryTextLength](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.SearchServiceApplication.MaxKeywordQueryTextLength.aspx) или [DiscoveryMaxKeywordQueryTextLength](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.SearchServiceApplication.DiscoveryMaxKeywordQueryTextLength.aspx) (для обнаружения электронных данных).</span><span class="sxs-lookup"><span data-stu-id="9c68e-116">You can increase this limit up to 20,480 characters by using the  [MaxKeywordQueryTextLength](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.SearchServiceApplication.MaxKeywordQueryTextLength.aspx) property or the [DiscoveryMaxKeywordQueryTextLength](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.SearchServiceApplication.DiscoveryMaxKeywordQueryTextLength.aspx) property (for eDiscovery).</span></span>
  
    
    


## <a name="constructing-free-text-queries-using-kql"></a><span data-ttu-id="9c68e-117">Создание запросов с произвольным текстом при помощи KQL</span><span class="sxs-lookup"><span data-stu-id="9c68e-117">Constructing free-text queries using KQL</span></span>
<span data-ttu-id="9c68e-118"><a name="SP15KQL_constructing_freetext_queries"> </a></span><span class="sxs-lookup"><span data-stu-id="9c68e-118"></span></span>

<span data-ttu-id="9c68e-p104">При создании KQL-запроса с использованием произвольных выражений Поиск в SharePoint подбирает результаты с совпадениями для выбранных вами терминов, основываясь на терминах, хранящихся в полнотекстовом индексе. Сюда входят значения управляемых свойств, в которых параметр  [FullTextQueriable](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedProperty.FullTextQueriable.aspx) имеет значение **true**.</span><span class="sxs-lookup"><span data-stu-id="9c68e-p104">When you construct your KQL query by using free-text expressions, Search in SharePoint matches results for the terms you chose for the query based on terms stored in the full-text index. This includes managed property values where  [FullTextQueriable](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedProperty.FullTextQueriable.aspx) is set to **true**.</span></span>
  
    
    
<span data-ttu-id="9c68e-p105">KQL-запросы с произвольным текстом не чувствительны к регистру, однако операторы должны быть записаны заглавными буквами. Вы можете строить KQL-запросы с помощью одного или нескольких произвольных выражений:</span><span class="sxs-lookup"><span data-stu-id="9c68e-p105">Free text KQL queries are case-insensitive but the operators must be in uppercase. You can construct KQL queries by using one or more of the following as free-text expressions:</span></span>
  
    
    

- <span data-ttu-id="9c68e-123">**word** (содержит один или несколько символов без пробелов и знаков препинания);</span><span class="sxs-lookup"><span data-stu-id="9c68e-123">A **word** (includes one or more characters without spaces or punctuation)</span></span>
    
  
- <span data-ttu-id="9c68e-124">**phrase** (содержит два и более слов, разделенных пробелами и обязательно заключенных в двойные кавычки).</span><span class="sxs-lookup"><span data-stu-id="9c68e-124">A **phrase** (includes two or more words together, separated by spaces; however, the words must be enclosed in double quotation marks)</span></span>
    
  
<span data-ttu-id="9c68e-p106">Чтобы создать сложные запросы, вы можете комбинировать несколько произвольных выражений с помощью операторов KQL-запросов. Если операторы между выражениями отсутствуют, запрос будет выполняться так же, как при использовании оператора **AND**.</span><span class="sxs-lookup"><span data-stu-id="9c68e-p106">To construct complex queries, you can combine multiple free-text expressions with KQL query operators. If there are multiple free-text expressions without any operators in between them, the query behavior is the same as using the **AND** operator.</span></span>
  
    
    

### <a name="using-words-in-the-free-text-kql-query"></a><span data-ttu-id="9c68e-127">Использование слов в KQL-запросе с произвольным текстом</span><span class="sxs-lookup"><span data-stu-id="9c68e-127">Using words in the free-text KQL query</span></span>

<span data-ttu-id="9c68e-p107">Если вы используете слова в KQL-запросе с произвольным текстом, служба Поиск в SharePoint возвращает результаты с точным совпадением этих слов с терминами, хранящимися в полнотекстовом индексе. Можно указывать только начальную часть слова, применяя оператор подстановочного знака (*) для включения сопоставления префиксов. При таком сопоставлении служба Поиск в SharePoint подбирает совпадения с терминами, содержащими искомое слово, за которым могут следовать другие символы.</span><span class="sxs-lookup"><span data-stu-id="9c68e-p107">When you use words in a free-text KQL query, Search in SharePoint returns results based on exact matches of your words with the terms stored in the full-text index. You can use just a part of a word, from the beginning of the word, by using the wildcard operator (*) to enable prefix matching. In prefix matching, Search in SharePoint matches results with terms that contain the word followed by zero or more characters.</span></span>
  
    
    
<span data-ttu-id="9c68e-131">Например, следующие KQL­-запросы вернут элементы, содержащие термины "federated" и "search":</span><span class="sxs-lookup"><span data-stu-id="9c68e-131">For example, the following KQL queries return content items that contain the terms "federated" and "search":</span></span> 
  
    
    
 `federated search`
  
    
    
 `federat* search`
  
    
    
 `search fed*`
  
    
    
<span data-ttu-id="9c68e-132">KQL­-запросы не поддерживают сопоставление суффиксов.</span><span class="sxs-lookup"><span data-stu-id="9c68e-132">KQL queries don't support suffix matching.</span></span>
  
    
    

### <a name="using-phrases-in-the-free-text-kql-query"></a><span data-ttu-id="9c68e-133">Использование фраз в KQL-запросе с произвольным текстом</span><span class="sxs-lookup"><span data-stu-id="9c68e-133">Using phrases in the free-text KQL query</span></span>

<span data-ttu-id="9c68e-p108">Если вы используете фразы в KQL-запросе с произвольным текстом, служба Поиск в SharePoint возвращает только элементы, в которых есть слова из вашей фразы, следующие друг за другом. Чтобы задать фразу в KQL-запросе, необходимо использовать двойные кавычки.</span><span class="sxs-lookup"><span data-stu-id="9c68e-p108">When you use phrases in a free-text KQL query, Search in SharePoint returns only the items in which the words in your phrase are located next to each other. To specify a phrase in a KQL query, you must use double quotation marks.</span></span> 
  
    
    
<span data-ttu-id="9c68e-p109">KQL-запросы не поддерживают сопоставление суффиксов, поэтому в запросах с произвольным текстом нельзя использовать оператор подстановочного знака перед фразой. Однако вы можете использовать оператор подстановочного знака после фразы.</span><span class="sxs-lookup"><span data-stu-id="9c68e-p109">KQL queries don't support suffix matching, so you can't use the wildcard operator before a phrase in free-text queries. However, you can use the wildcard operator after a phrase.</span></span>
  
    
    

## <a name="property-restriction-queries-in-kql"></a><span data-ttu-id="9c68e-138">Запросы с ограничениями свойств в KQL</span><span class="sxs-lookup"><span data-stu-id="9c68e-138">Property restriction queries in KQL</span></span>
<span data-ttu-id="9c68e-139"><a name="kql_property_restriction_queries"> </a></span><span class="sxs-lookup"><span data-stu-id="9c68e-139"></span></span>

<span data-ttu-id="9c68e-140">С помощью KQL вы можете строить запросы, использующие ограничения свойств, чтобы получать результаты запроса только по заданному условию.</span><span class="sxs-lookup"><span data-stu-id="9c68e-140">Using KQL, you can construct queries that use property restrictions to narrow the focus of the query to match only results based on a specified condition.</span></span>
  
    
    

### <a name="specifying-property-restrictions"></a><span data-ttu-id="9c68e-141">Задание ограничений свойств</span><span class="sxs-lookup"><span data-stu-id="9c68e-141">Specifying property restrictions</span></span>

<span data-ttu-id="9c68e-142">Базовое ограничение свойств состоит из перечисленных ниже элементов.</span><span class="sxs-lookup"><span data-stu-id="9c68e-142">A basic property restriction consists of the following:</span></span>
  
    
    
 `<Property Name><Property Operator><Property Value>`
  
    
    
<span data-ttu-id="9c68e-143">В таблице 1 приведены некоторые примеры допустимого синтаксиса ограничений свойств в KQL-запросах.</span><span class="sxs-lookup"><span data-stu-id="9c68e-143">Table 1 lists some examples of valid property restrictions syntax in KQL queries.</span></span>
  
    
    

<span data-ttu-id="9c68e-144">**Таблица 1. Допустимый синтаксис ограничений свойств**</span><span class="sxs-lookup"><span data-stu-id="9c68e-144">**Table 1. Valid property restriction syntax**</span></span>


|<span data-ttu-id="9c68e-145">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="9c68e-145">**Syntax**</span></span>|<span data-ttu-id="9c68e-146">**Возвращаемое значение**</span><span class="sxs-lookup"><span data-stu-id="9c68e-146">**Returns**</span></span>|
|:-----|:-----|
| `author:"John Smith"` <br/> |<span data-ttu-id="9c68e-147">Возвращает элементы контента, автором которого является John Smith.</span><span class="sxs-lookup"><span data-stu-id="9c68e-147">Returns content items authored by John Smith.</span></span>  <br/> |
| `filetype:docx` <br/> |<span data-ttu-id="9c68e-148">Возвращает документы Microsoft Word.</span><span class="sxs-lookup"><span data-stu-id="9c68e-148">Returns Microsoft Word documents.</span></span>  <br/> |
| `filename:budget.xlsx` <br/> |<span data-ttu-id="9c68e-149">Возвращает элементы, содержащие имя файла  `budget.xlsx`.</span><span class="sxs-lookup"><span data-stu-id="9c68e-149">Returns content items with the file name  `budget.xlsx`.</span></span>  <br/> |
   
<span data-ttu-id="9c68e-p110">Ограничение свойства не должно содержать пробелы между именем, оператором и значением этого свойства. Иначе это ограничение будет обрабатываться как запрос с произвольным текстом. Максимальная длина ограничения свойства составляет 2048 символов.</span><span class="sxs-lookup"><span data-stu-id="9c68e-p110">The property restriction must not include white space between the property name, property operator, and the property value, or the property restriction is treated as a free-text query. The length of a property restriction is limited to 2,048 characters.</span></span> 
  
    
    
<span data-ttu-id="9c68e-152">В следующих примерах наличие пробела приводит к тому, что запрос возвращает элементы, содержащие термины "author" и "John Smith", вместо элементов контента, автором которого является John Smith:</span><span class="sxs-lookup"><span data-stu-id="9c68e-152">In the following examples, the white space causes the query to return content items containing the terms "author" and "John Smith", instead of content items authored by John Smith:</span></span>
  
    
    
 `author: "John Smith"`
  
    
    
 `author :"John Smith"`
  
    
    
 `author : "John Smith"`
  
    
    
<span data-ttu-id="9c68e-153">Другими словами, описанные выше ограничения свойств эквивалентны следующему запросу:</span><span class="sxs-lookup"><span data-stu-id="9c68e-153">In other words, the previous property restrictions are equivalent to the following:</span></span>
  
    
    
 `author "John Smith"`
  
    
    

### <a name="specifying-property-names-for-property-restrictions"></a><span data-ttu-id="9c68e-154">Указание имен свойств для ограничений свойств</span><span class="sxs-lookup"><span data-stu-id="9c68e-154">Specifying property names for property restrictions</span></span>

<span data-ttu-id="9c68e-p111">Необходимо указать допустимое имя управляемого свойства для ограничения свойства. По умолчанию в Поиск в SharePoint входит несколько управляемых свойств для документов.</span><span class="sxs-lookup"><span data-stu-id="9c68e-p111">You must specify a valid managed property name for the property restriction. By default, Search in SharePoint includes several managed properties for documents.</span></span>
  
    
    
<span data-ttu-id="9c68e-p112">Чтобы задать ограничение для значения свойства, извлеченного при обходе контента, сначала необходимо сопоставить это свойство с управляемым свойством. См. раздел **Управляемые свойства и свойства для обхода** статьи [Планирование методов поиска для конечных пользователей (Office SharePoint Server)](http://technet.microsoft.com/ru-RU/library/cc263089.aspx).</span><span class="sxs-lookup"><span data-stu-id="9c68e-p112">To specify a property restriction for a crawled property value, you must first map the crawled property to a managed property. See **Managed and crawled properties** in [Plan the end-user search experience](http://technet.microsoft.com/ru-RU/library/cc263089.aspx).</span></span> 
  
    
    
<span data-ttu-id="9c68e-p113">Управляемое свойство должно относиться к типу  [Queryable](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedProperty.Queryable.aspx) , чтобы вы могли искать это управляемое свойство в документе. Кроме того, управляемое свойство может относиться к типу [Retrievable](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedProperty.Retrievable.aspx) , чтобы можно было его извлечь. Однако управляемое свойство не обязательно должно относиться к типу [Retrievable](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedProperty.Retrievable.aspx) , чтобы можно было найти свойство.</span><span class="sxs-lookup"><span data-stu-id="9c68e-p113">The managed property must be  [Queryable](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedProperty.Queryable.aspx) so that you can search for that managed property in a document. In addition, the managed property may be [Retrievable](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedProperty.Retrievable.aspx) for the managed property to be retrieved. However, the managed property doesn't have to be [Retrievable](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedProperty.Retrievable.aspx) to carry out property searches.</span></span>
  
    
    

### <a name="property-operators-that-are-supported-in-property-restrictions"></a><span data-ttu-id="9c68e-162">Операторы свойств, поддерживаемые в ограничениях свойств</span><span class="sxs-lookup"><span data-stu-id="9c68e-162">Property operators that are supported in property restrictions</span></span>

<span data-ttu-id="9c68e-163">Служба Поиск в SharePoint поддерживает несколько операторов свойств для ограничений свойств, приведенных в таблице 2.</span><span class="sxs-lookup"><span data-stu-id="9c68e-163">Search in SharePoint supports several property operators for property restrictions, as shown in Table 2.</span></span> 
  
    
    

<span data-ttu-id="9c68e-164">**Таблица 2. Допустимые операторы свойств для ограничений свойств**</span><span class="sxs-lookup"><span data-stu-id="9c68e-164">**Table 2. Valid property operators for property restrictions**</span></span>


|<span data-ttu-id="9c68e-165">**Оператор**</span><span class="sxs-lookup"><span data-stu-id="9c68e-165">**Operator**</span></span>|<span data-ttu-id="9c68e-166">**Описание**</span><span class="sxs-lookup"><span data-stu-id="9c68e-166">**Description**</span></span>|<span data-ttu-id="9c68e-167">**Поддерживаемый тип управляемого свойства**</span><span class="sxs-lookup"><span data-stu-id="9c68e-167">**Supported managed property type**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="9c68e-168">.</span><span class="sxs-lookup"><span data-stu-id="9c68e-168"></span></span>  <br/> |<span data-ttu-id="9c68e-169">Возвращает результаты, в которых указанное в ограничении свойства значение равно значению свойства, хранящегося в базе данных хранилища свойств, или совпадает с отдельными терминами в значении свойства, хранящегося в полнотекстовом индексе.</span><span class="sxs-lookup"><span data-stu-id="9c68e-169">Returns results where the value specified in the property restriction is equal to the property value that is stored in the Property Store database, or matches individual terms in the property value that is stored in the full-text index.</span></span>  <br/> | [<span data-ttu-id="9c68e-170">Text</span><span class="sxs-lookup"><span data-stu-id="9c68e-170">Text</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Text.aspx) <br/>  [<span data-ttu-id="9c68e-171">DateTime</span><span class="sxs-lookup"><span data-stu-id="9c68e-171">DateTime</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.DateTime.aspx) <br/>  [<span data-ttu-id="9c68e-172">Integer</span><span class="sxs-lookup"><span data-stu-id="9c68e-172">Integer</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Integer.aspx) <br/>  [<span data-ttu-id="9c68e-173">Decimal</span><span class="sxs-lookup"><span data-stu-id="9c68e-173">Decimal</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Decimal.aspx) <br/>  [<span data-ttu-id="9c68e-174">Double</span><span class="sxs-lookup"><span data-stu-id="9c68e-174">Double</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Double.aspx) <br/>  [<span data-ttu-id="9c68e-175">YesNo</span><span class="sxs-lookup"><span data-stu-id="9c68e-175">Yes/No</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.YesNo.aspx) <br/> |
|=  <br/> |<span data-ttu-id="9c68e-176">Возвращает результаты поиска со значениями свойств, равными значению, определенному при ограничении свойств.</span><span class="sxs-lookup"><span data-stu-id="9c68e-176">Returns search results where the property value is equal to the value specified in the property restriction.</span></span>  <br/> <span data-ttu-id="9c68e-177">**Примечание.** Не рекомендуем сочетать оператор **=** со знаком звездочки (**\***), если нужно найти точное совпадение.</span><span class="sxs-lookup"><span data-stu-id="9c68e-177">We do not recommend combining the **=** operator together with asterisk ( *****) when you do exact matching.</span></span>           | [<span data-ttu-id="9c68e-178">Text</span><span class="sxs-lookup"><span data-stu-id="9c68e-178">Text</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Text.aspx) <br/>  [<span data-ttu-id="9c68e-179">DateTime</span><span class="sxs-lookup"><span data-stu-id="9c68e-179">DateTime</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.DateTime.aspx) <br/>  [<span data-ttu-id="9c68e-180">Integer</span><span class="sxs-lookup"><span data-stu-id="9c68e-180">Integer</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Integer.aspx) <br/>  [<span data-ttu-id="9c68e-181">Decimal</span><span class="sxs-lookup"><span data-stu-id="9c68e-181">Decimal</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Decimal.aspx) <br/>  [<span data-ttu-id="9c68e-182">Double</span><span class="sxs-lookup"><span data-stu-id="9c68e-182">Double</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Double.aspx) <br/>  [<span data-ttu-id="9c68e-183">YesNo</span><span class="sxs-lookup"><span data-stu-id="9c68e-183">Yes/No</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.YesNo.aspx) <br/> |
|<  <br/> |<span data-ttu-id="9c68e-184">Возвращает результаты, в которых значение свойства меньше значения, указанного в ограничении свойства.</span><span class="sxs-lookup"><span data-stu-id="9c68e-184">Returns results where the property value is less than the value specified in the property restriction.</span></span>  <br/> | [<span data-ttu-id="9c68e-185">DateTime</span><span class="sxs-lookup"><span data-stu-id="9c68e-185">DateTime</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.DateTime.aspx) <br/>  [<span data-ttu-id="9c68e-186">Integer</span><span class="sxs-lookup"><span data-stu-id="9c68e-186">Integer</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Integer.aspx) <br/>  [<span data-ttu-id="9c68e-187">Decimal</span><span class="sxs-lookup"><span data-stu-id="9c68e-187">Decimal</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Decimal.aspx) <br/>  [<span data-ttu-id="9c68e-188">Double</span><span class="sxs-lookup"><span data-stu-id="9c68e-188">Double</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Double.aspx) <br/> |
|>  <br/> |<span data-ttu-id="9c68e-189">Возвращает результаты, в которых значение свойства больше значения, указанного в ограничении свойства.</span><span class="sxs-lookup"><span data-stu-id="9c68e-189">Returns search results where the property value is greater than the value specified in the property restriction.</span></span>  <br/> | [<span data-ttu-id="9c68e-190">DateTime</span><span class="sxs-lookup"><span data-stu-id="9c68e-190">DateTime</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.DateTime.aspx) <br/>  [<span data-ttu-id="9c68e-191">Integer</span><span class="sxs-lookup"><span data-stu-id="9c68e-191">Integer</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Integer.aspx) <br/>  [<span data-ttu-id="9c68e-192">Decimal</span><span class="sxs-lookup"><span data-stu-id="9c68e-192">Decimal</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Decimal.aspx) <br/>  [<span data-ttu-id="9c68e-193">Double</span><span class="sxs-lookup"><span data-stu-id="9c68e-193">Double</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Double.aspx) <br/> |
|<=  <br/> |<span data-ttu-id="9c68e-194">Возвращает результаты со значением свойства, меньшим или равным значению, указанному в ограничении свойства.</span><span class="sxs-lookup"><span data-stu-id="9c68e-194">Returns search results where the property value is less than or equal to the value specified in the property restriction.</span></span>  <br/> | [<span data-ttu-id="9c68e-195">DateTime</span><span class="sxs-lookup"><span data-stu-id="9c68e-195">DateTime</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.DateTime.aspx) <br/>  [<span data-ttu-id="9c68e-196">Integer</span><span class="sxs-lookup"><span data-stu-id="9c68e-196">Integer</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Integer.aspx) <br/>  [<span data-ttu-id="9c68e-197">Decimal</span><span class="sxs-lookup"><span data-stu-id="9c68e-197">Decimal</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Decimal.aspx) <br/>  [<span data-ttu-id="9c68e-198">Double</span><span class="sxs-lookup"><span data-stu-id="9c68e-198">Double</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Double.aspx) <br/> |
|>=  <br/> |<span data-ttu-id="9c68e-199">Возвращает результаты со значением свойства, большим или равным значению, указанному в ограничении свойства.</span><span class="sxs-lookup"><span data-stu-id="9c68e-199">Returns search results where the property value is greater than or equal to the value specified in the property restriction.</span></span>  <br/> | [<span data-ttu-id="9c68e-200">DateTime</span><span class="sxs-lookup"><span data-stu-id="9c68e-200">DateTime</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.DateTime.aspx) <br/>  [<span data-ttu-id="9c68e-201">Integer</span><span class="sxs-lookup"><span data-stu-id="9c68e-201">Integer</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Integer.aspx) <br/>  [<span data-ttu-id="9c68e-202">Decimal</span><span class="sxs-lookup"><span data-stu-id="9c68e-202">Decimal</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Decimal.aspx) <br/>  [<span data-ttu-id="9c68e-203">Double</span><span class="sxs-lookup"><span data-stu-id="9c68e-203">Double</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Double.aspx) <br/> |
|\<\>  <br/> |<span data-ttu-id="9c68e-204">Возвращает результаты со значением свойства, не равным значению, указанному в ограничении свойства.</span><span class="sxs-lookup"><span data-stu-id="9c68e-204">Returns search results where the property value does not equal the value specified in the property restriction.</span></span>  <br/> | [<span data-ttu-id="9c68e-205">DateTime</span><span class="sxs-lookup"><span data-stu-id="9c68e-205">DateTime</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.DateTime.aspx) <br/>  [<span data-ttu-id="9c68e-206">Integer</span><span class="sxs-lookup"><span data-stu-id="9c68e-206">Integer</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Integer.aspx) <br/>  [<span data-ttu-id="9c68e-207">Decimal</span><span class="sxs-lookup"><span data-stu-id="9c68e-207">Decimal</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Decimal.aspx) <br/>  [<span data-ttu-id="9c68e-208">Text</span><span class="sxs-lookup"><span data-stu-id="9c68e-208">Text</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Text.aspx) <br/>  [<span data-ttu-id="9c68e-209">Double</span><span class="sxs-lookup"><span data-stu-id="9c68e-209">Double</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Double.aspx) <br/>  [<span data-ttu-id="9c68e-210">YesNo</span><span class="sxs-lookup"><span data-stu-id="9c68e-210">Yes/No</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.YesNo.aspx) <br/> |
|<span data-ttu-id="9c68e-211">..</span><span class="sxs-lookup"><span data-stu-id="9c68e-211"></span></span>  <br/> |<span data-ttu-id="9c68e-212">Возвращает результаты, в которых значение свойства включено в диапазон, указанный в ограничении свойства.</span><span class="sxs-lookup"><span data-stu-id="9c68e-212">Returns search results where the property value falls within the range specified in the property restriction.</span></span>  <br/> <span data-ttu-id="9c68e-p114">Например, диапазон A..B представляет собой набор значений от A до B со значениями A и B включительно. Для диапазонов дат такая запись означает диапазон от начала дня A до конца дня B.</span><span class="sxs-lookup"><span data-stu-id="9c68e-p114">For example, the range A..B represents a set of values from A to B where both A and B are inclusive. For date ranges this means from the beginning of day A to the end of day B.</span></span>  <br/> | [<span data-ttu-id="9c68e-215">DateTime</span><span class="sxs-lookup"><span data-stu-id="9c68e-215">DateTime</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.DateTime.aspx) <br/>  [<span data-ttu-id="9c68e-216">Integer</span><span class="sxs-lookup"><span data-stu-id="9c68e-216">Integer</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Integer.aspx) <br/>  [<span data-ttu-id="9c68e-217">Decimal</span><span class="sxs-lookup"><span data-stu-id="9c68e-217">Decimal</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Decimal.aspx) <br/>  [<span data-ttu-id="9c68e-218">Double</span><span class="sxs-lookup"><span data-stu-id="9c68e-218">Double</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Double.aspx) <br/> |
   

### <a name="specifying-property-values"></a><span data-ttu-id="9c68e-219">Указание значений свойств</span><span class="sxs-lookup"><span data-stu-id="9c68e-219">Specifying property values</span></span>

<span data-ttu-id="9c68e-p115">Укажите значение свойства, имеющего допустимый тип данных для типа управляемого свойства. В таблице 3 приведен перечень сопоставлений типов.</span><span class="sxs-lookup"><span data-stu-id="9c68e-p115">You must specify a property value that is a valid data type for the managed property's type. Table 3 lists these type mappings.</span></span>
  
    
    

<span data-ttu-id="9c68e-222">**Таблица 3. Соответствие допустимых типов данных типам управляемых свойств**</span><span class="sxs-lookup"><span data-stu-id="9c68e-222">**Table 3. Valid data type mappings for managed property types**</span></span>


|<span data-ttu-id="9c68e-223">**Тип управляемых свойств**</span><span class="sxs-lookup"><span data-stu-id="9c68e-223">**Managed type**</span></span>|<span data-ttu-id="9c68e-224">**Тип данных**</span><span class="sxs-lookup"><span data-stu-id="9c68e-224">**Data type**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="9c68e-225">Text</span><span class="sxs-lookup"><span data-stu-id="9c68e-225">Text</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Text.aspx) <br/> | [<span data-ttu-id="9c68e-226">String</span><span class="sxs-lookup"><span data-stu-id="9c68e-226">String</span></span>](https://msdn.microsoft.com/library/System.String.aspx) <br/> |
| [<span data-ttu-id="9c68e-227">Integer</span><span class="sxs-lookup"><span data-stu-id="9c68e-227">Integer</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Integer.aspx) <br/> | [<span data-ttu-id="9c68e-228">Int64</span><span class="sxs-lookup"><span data-stu-id="9c68e-228">Int64</span></span>](https://msdn.microsoft.com/library/System.Int64.aspx) <br/> |
| [<span data-ttu-id="9c68e-229">Double</span><span class="sxs-lookup"><span data-stu-id="9c68e-229">Double</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Double.aspx) <br/> | [<span data-ttu-id="9c68e-230">System.Double</span><span class="sxs-lookup"><span data-stu-id="9c68e-230">System.Double</span></span>](https://msdn.microsoft.com/library/System.Double.aspx) <br/> |
| [<span data-ttu-id="9c68e-231">Decimal</span><span class="sxs-lookup"><span data-stu-id="9c68e-231">Decimal</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.Decimal.aspx) <br/> | [<span data-ttu-id="9c68e-232">Decimal</span><span class="sxs-lookup"><span data-stu-id="9c68e-232">Decimal</span></span>](https://msdn.microsoft.com/library/System.Decimal.aspx) <br/> |
| [<span data-ttu-id="9c68e-233">DateTime()</span><span class="sxs-lookup"><span data-stu-id="9c68e-233">DateTime</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.DateTime.aspx) <br/> | [<span data-ttu-id="9c68e-234">DateTime</span><span class="sxs-lookup"><span data-stu-id="9c68e-234">DateTime</span></span>](https://msdn.microsoft.com/library/System.DateTime.aspx) <br/> |
| [<span data-ttu-id="9c68e-235">YesNo</span><span class="sxs-lookup"><span data-stu-id="9c68e-235">Yes/No</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedDataType.YesNo.aspx) <br/> | [<span data-ttu-id="9c68e-236">Boolean</span><span class="sxs-lookup"><span data-stu-id="9c68e-236">Boolean</span></span>](https://msdn.microsoft.com/library/System.Boolean.aspx) <br/> |
   

#### <a name="text-property-values"></a><span data-ttu-id="9c68e-237">Значения текстовых свойств</span><span class="sxs-lookup"><span data-stu-id="9c68e-237">Text property values</span></span>

<span data-ttu-id="9c68e-238">В случае значений текстовых свойств ход сопоставления зависит от того, хранится ли свойство в полнотекстовом индексе или в индексе поиска.</span><span class="sxs-lookup"><span data-stu-id="9c68e-238">For text property values, the matching behavior depends on whether the property is stored in the full-text index or in the search index.</span></span> 
  
    
    

#### <a name="property-values-in-the-full-text-index"></a><span data-ttu-id="9c68e-239">Значения свойств в полнотекстовом индексе</span><span class="sxs-lookup"><span data-stu-id="9c68e-239">Property values in the full-text index</span></span>

<span data-ttu-id="9c68e-p116">Значения свойств хранятся в полнотекстовом индексе, когда свойству **FullTextQueriable** присвоено значение **true** для управляемого свойства. Эту настройку можно использовать только для строковых свойств. Значения свойств, указанные в запросе, сопоставляются с отдельными терминами, которые хранятся в полнотекстовом индексе. Используйте свойство [NoWordBreaker](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedProperty.NoWordBreaker.aspx) , чтобы указать, должен ли проводиться поиск совпадений с полным значением свойства.</span><span class="sxs-lookup"><span data-stu-id="9c68e-p116">Property values are stored in the full-text index when the **FullTextQueriable** property is set to **true** for a managed property. You can configure this only for string properties. Property values that are specified in the query are matched against individual terms that are stored in the full-text index. Use the [NoWordBreaker](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.ManagedProperty.NoWordBreaker.aspx) property to specify whether to match with the whole property value.</span></span>
  
    
    
<span data-ttu-id="9c68e-244">Например, если вы ищете элемент контента, созданный пользователем Paul Shakespear, такой KQL-запрос возвращает результаты с совпадениями:</span><span class="sxs-lookup"><span data-stu-id="9c68e-244">For example, if you're searching for a content item authored by Paul Shakespear, the following KQL query returns matching results:</span></span>
  
    
    
 `author:Shakespear`
  
    
    
 `author:Paul`
  
    
    
<span data-ttu-id="9c68e-p117">Кроме того, поддерживается сопоставление префиксов. Вы можете использовать оператор подстановочного знака (*), однако он не требуется при указании отдельных слов. Перейдем к следующему примеру. Этот KQL-запрос тоже возвращает элементы контента, созданные пользователем Paul Shakespear:</span><span class="sxs-lookup"><span data-stu-id="9c68e-p117">Prefix matching is also supported. You can use the wildcard operator (*), but isn't required when you specify individual words. Continuing with the previous example, the following KQL query returns content items authored by Paul Shakespear as matches:</span></span> 
  
    
    
 `author:Shakesp*`
  
    
    
<span data-ttu-id="9c68e-p118">Когда вы указываете фразу для значения свойства, результаты с совпадениями должны содержать указанную фразу в значении свойства, хранящегося в полнотекстовом индексе. Такой запрос возвращает элементы контента с текстом "Advanced Search" в названии, например "Advanced Search XML" и "Learning About the Advanced Search Web Part":</span><span class="sxs-lookup"><span data-stu-id="9c68e-p118">When you specify a phrase for the property value, matched results must contain the specified phrase within the property value that is stored in the full-text index. The following query example returns content items with the text "Advanced Search" in the title, such as "Advanced Search XML", "Learning About the Advanced Search Web Part", and so on:</span></span>
  
    
    
 `title:"Advanced Search"`
  
    
    
<span data-ttu-id="9c68e-250">Сопоставление префиксов также поддерживается для фраз, указанных в значениях свойств. Но в этом случае в запросе следует использовать оператор подстановочного знака (*), который допустим только в конце фразы, например:</span><span class="sxs-lookup"><span data-stu-id="9c68e-250">Prefix matching is also supported with phrases specified in property values, but you must use the wildcard operator (*) in the query, and it is supported only at the end of the phrase, as follows:</span></span>
  
    
    
 `title:"Advanced Sear*"`
  
    
    
<span data-ttu-id="9c68e-251">Следующие запросы не возвращают ожидаемые результаты:</span><span class="sxs-lookup"><span data-stu-id="9c68e-251">The following queries do not return the expected results:</span></span>
  
    
    
 `title:"Advan* Search"`
  
    
    
 `title:"Advanced Sear"`
  
    
    

#### <a name="numerical-values-for-properties"></a><span data-ttu-id="9c68e-252">Числовые значения свойств</span><span class="sxs-lookup"><span data-stu-id="9c68e-252">Numerical values for properties</span></span>

<span data-ttu-id="9c68e-253">В случае числовых значений свойств, к которым относятся управляемые типы **Integer**, **Double** и **Decimal**, ограничение свойства сопоставляется с полным значением свойства.</span><span class="sxs-lookup"><span data-stu-id="9c68e-253">For numerical property values, which include the **Integer**, **Double**, and **Decimal** managed types, the property restriction is matched against the entire value of the property.</span></span>
  
    
    

### <a name="date-or-time-values-for-properties"></a><span data-ttu-id="9c68e-254">Значения даты и времени для свойств</span><span class="sxs-lookup"><span data-stu-id="9c68e-254">Date or time values for properties</span></span>

<span data-ttu-id="9c68e-255">В языке KQL для даты и времени предназначен тип данных **datetime**. В запросах поддерживаются следующие форматы даты и времени, совместимые с ISO 8601:</span><span class="sxs-lookup"><span data-stu-id="9c68e-255">KQL provides the **datetime** data type for date and time.The following ISO 8601-compatible datetime formats are supported in queries:</span></span>
  
    
    

- <span data-ttu-id="9c68e-256">ГГГГ-ММ-ДД</span><span class="sxs-lookup"><span data-stu-id="9c68e-256">YYYY-MM-DD</span></span>
    
  
- <span data-ttu-id="9c68e-257">ГГГГ-ММ-ДДTчч:мм:сс</span><span class="sxs-lookup"><span data-stu-id="9c68e-257">YYYY-MM-DDThh:mm:ss</span></span>
    
  
- <span data-ttu-id="9c68e-258">ГГГГ-ММ-ДДTчч:мм:ссZ</span><span class="sxs-lookup"><span data-stu-id="9c68e-258">YYYY-MM-DDThh:mm:ssZ</span></span>
    
  
- <span data-ttu-id="9c68e-259">ГГГГ-ММ-ДДTчч:мм:ссfrZ</span><span class="sxs-lookup"><span data-stu-id="9c68e-259">YYYY-MM-DDThh:mm:ssfrZ</span></span>
    
  
<span data-ttu-id="9c68e-260">В этих форматах **datetime**:</span><span class="sxs-lookup"><span data-stu-id="9c68e-260">In these **datetime** formats:</span></span>
  
    
    

-  <span data-ttu-id="9c68e-261">_ГГГГ_ задает год из четырех цифр.</span><span class="sxs-lookup"><span data-stu-id="9c68e-261">_YYYY_ specifies a four-digit year.</span></span>
    
    > <span data-ttu-id="9c68e-262">**Примечание.** Поддерживается только формат года из четырех цифр.</span><span class="sxs-lookup"><span data-stu-id="9c68e-262">**Note** Only four-digit years are supported.</span></span> 
-  <span data-ttu-id="9c68e-p119">_ММ_ задает месяц в формате двух цифр. Например, 01 — это январь.</span><span class="sxs-lookup"><span data-stu-id="9c68e-p119">_MM_ specifies a two-digit month. For example, 01 = January.</span></span>
    
  
-  <span data-ttu-id="9c68e-265">Параметр  _ДД_ задает двузначное значение дня месяца (от 01 до 31).</span><span class="sxs-lookup"><span data-stu-id="9c68e-265">_DD_ specifies a two-digit day of the month (01 through 31).</span></span>
    
  
-  <span data-ttu-id="9c68e-266">Параметр  _T_ обозначает букву "T".</span><span class="sxs-lookup"><span data-stu-id="9c68e-266">_T_ specifies the letter "T".</span></span>
    
  
-  <span data-ttu-id="9c68e-p120">Параметр  _чч_ обозначает часы в формате двух цифр (от 00 до 23). Обозначения a.m. и p.m. не допускаются.</span><span class="sxs-lookup"><span data-stu-id="9c68e-p120">_hh_ specifies a two-digits hour (00 through 23); A.M./P.M. indication is not allowed.</span></span>
    
  
-  <span data-ttu-id="9c68e-269">Параметр  _мм_ обозначает минуты в формате двух цифр (от 00 до 59).</span><span class="sxs-lookup"><span data-stu-id="9c68e-269">_mm_ specifies a two-digit minute (00 through 59).</span></span>
    
  
-  <span data-ttu-id="9c68e-270">Параметр  _сс_ обозначает секунды в формате двух цифр (от 00 до 59).</span><span class="sxs-lookup"><span data-stu-id="9c68e-270">_ss_ specifies a two-digit second (00 through 59).</span></span>
    
  
-  <span data-ttu-id="9c68e-p121">Параметр  _fr_ задает доли секунды (необязательно). В этом случае используется от 1 до 7 цифр после разделителя (" **.**"), отделяющего доли секунды от секунд. Например, 2012-09-27T11:57:34.1234567.</span><span class="sxs-lookup"><span data-stu-id="9c68e-p121">_fr_ specifies an optional fraction of seconds, ss; between 1 to 7 digits that follows the **.** after the seconds. For example, 2012-09-27T11:57:34.1234567.</span></span>
    
  
<span data-ttu-id="9c68e-p122">Все значения даты и времени необходимо указывать в часовом поясе UTC (другое название  GMT). Идентификатор часового пояса UTC (символ "Z" в конце) указывать необязательно.</span><span class="sxs-lookup"><span data-stu-id="9c68e-p122">All date/time values must be specified according to the UTC (Coordinated Universal Time), also known as GMT (Greenwich Mean Time) time zone. The UTC time zone identifier (a trailing "Z" character) is optional.</span></span>
  
    
    

#### <a name="relevant-date-intervals-supported-by-kql"></a><span data-ttu-id="9c68e-276">Соответствующие интервалы дат, поддерживаемые KQL</span><span class="sxs-lookup"><span data-stu-id="9c68e-276">Relevant date intervals supported by KQL</span></span>

<span data-ttu-id="9c68e-p123">Язык KQL поддерживает реляционные запросы в диапазоне day, для которых зарезервированы ключевые слова, как показано в таблице 4. Используйте двойные кавычки ("") для интервалов дат, между их названиями ставьте пробел.</span><span class="sxs-lookup"><span data-stu-id="9c68e-p123">KQL enables you to build search queries that support relative "day" range query, with reserved keywords as shown in Table 4. Use double quotation marks ("") for date intervals with a space between their names.</span></span>
  
    
    


|<span data-ttu-id="9c68e-279">**Имя интервала дат**</span><span class="sxs-lookup"><span data-stu-id="9c68e-279">**Name of date interval**</span></span>|<span data-ttu-id="9c68e-280">**Описание**</span><span class="sxs-lookup"><span data-stu-id="9c68e-280">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="9c68e-281">today</span><span class="sxs-lookup"><span data-stu-id="9c68e-281">today</span></span>  <br/> |<span data-ttu-id="9c68e-282">Представляет период времени с начала текущего дня до его окончания.</span><span class="sxs-lookup"><span data-stu-id="9c68e-282">Represents the time from the beginning of the current day until the end of the current day.</span></span>  <br/> |
|<span data-ttu-id="9c68e-283">yesterday</span><span class="sxs-lookup"><span data-stu-id="9c68e-283">yesterday</span></span>  <br/> |<span data-ttu-id="9c68e-284">Представляет период времени с начала предшествующего дня до его окончания.</span><span class="sxs-lookup"><span data-stu-id="9c68e-284">Represents the time from the beginning of the day until the end of the day that precedes the current day.</span></span>  <br/> |
|<span data-ttu-id="9c68e-285">this week</span><span class="sxs-lookup"><span data-stu-id="9c68e-285">this week</span></span>  <br/> |<span data-ttu-id="9c68e-p124">Представляет период времени от начала текущей недели до ее окончания. При определении первого дня недели учитываются традиции региона, в котором формируется текст запроса.</span><span class="sxs-lookup"><span data-stu-id="9c68e-p124">Represents the time from the beginning of the current week until the end of the current week. The culture in which the query text was formulated is taken into account to determine the first day of the week.</span></span>  <br/> |
|<span data-ttu-id="9c68e-288">this month</span><span class="sxs-lookup"><span data-stu-id="9c68e-288">this month</span></span>  <br/> |<span data-ttu-id="9c68e-289">Представляет период времени с начала текущего месяца до его окончания.</span><span class="sxs-lookup"><span data-stu-id="9c68e-289">Represents the time from the beginning of the current month until the end of the current month.</span></span>  <br/> |
|<span data-ttu-id="9c68e-290">last month</span><span class="sxs-lookup"><span data-stu-id="9c68e-290">last month</span></span>  <br/> |<span data-ttu-id="9c68e-291">Представляет период времени от начала предыдущего месяца до его окончания.</span><span class="sxs-lookup"><span data-stu-id="9c68e-291">Represents the entire month that precedes the current month.</span></span>  <br/> |
|<span data-ttu-id="9c68e-292">this year</span><span class="sxs-lookup"><span data-stu-id="9c68e-292">this year</span></span>  <br/> |<span data-ttu-id="9c68e-293">Представляет период времени от начала текущего года до его окончания.</span><span class="sxs-lookup"><span data-stu-id="9c68e-293">Represents the time from the beginning of the current year until the end of the current year.</span></span>  <br/> |
|<span data-ttu-id="9c68e-294">last year</span><span class="sxs-lookup"><span data-stu-id="9c68e-294">last year</span></span>  <br/> |<span data-ttu-id="9c68e-295">Представляет весь год, предшествующий текущему.</span><span class="sxs-lookup"><span data-stu-id="9c68e-295">Represents the entire year that precedes the current year.</span></span>  <br/> |
   

### <a name="using-multiple-property-restrictions-within-a-kql-query"></a><span data-ttu-id="9c68e-296">Использование нескольких ограничений свойств в KQL-запросе</span><span class="sxs-lookup"><span data-stu-id="9c68e-296">Using multiple property restrictions within a KQL query</span></span>

<span data-ttu-id="9c68e-p125">Служба Поиск в SharePoint поддерживает использование нескольких ограничений свойств в одном KQL-запросе. Можно использовать либо одно свойство для нескольких ограничений свойств, либо разные свойства для каждого ограничения свойств.</span><span class="sxs-lookup"><span data-stu-id="9c68e-p125">Search in SharePoint supports the use of multiple property restrictions within the same KQL query. You can use either the same property for more than one property restriction, or a different property for each property restriction.</span></span> 
  
    
    
<span data-ttu-id="9c68e-p126">Если вы используете несколько экземпляров ограничений свойств, поиск совпадений основан на объединении ограничений свойств в KQL-запросе. В этом примере совпадения включают элементы контента, автором которого является John Smith или Jane Smith:</span><span class="sxs-lookup"><span data-stu-id="9c68e-p126">When you use multiple instances of the same property restriction, matches are based on the union of the property restrictions in the KQL query. Matches would include content items authored by John Smith or Jane Smith, as follows:</span></span>
  
    
    
 `author:"John Smith" author:"Jane Smith"`
  
    
    
<span data-ttu-id="9c68e-301">Результат будет таким же, как и при использовании логического оператора **OR** в запросе, например:</span><span class="sxs-lookup"><span data-stu-id="9c68e-301">This functionally is the same as using the **OR** Boolean operator, as follows:</span></span>
  
    
    
 `author:"John Smith" OR author:"Jane Smith"`
  
    
    
<span data-ttu-id="9c68e-302">Если вы используете различные ограничения свойств, поиск совпадений основан на пересечении ограничений свойств в KQL-запросе, например:</span><span class="sxs-lookup"><span data-stu-id="9c68e-302">When you use different property restrictions, matches are based on an intersection of the property restrictions in the KQL query, as follows:</span></span>
  
    
    
 `author:"John Smith" filetype:docx`
  
    
    
<span data-ttu-id="9c68e-p127">Совпадения будут содержать документы Microsoft Word, созданные пользователем John Smith. Такой же результат будет при использовании логического оператора **AND**, как показано в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="9c68e-p127">Matches would include Microsoft Word documents authored by John Smith. This is the same as using the **AND** Boolean operator, as follows:</span></span>
  
    
    
 `author:"John Smith" AND filetype:docx`
  
    
    

## <a name="kql-operators-for-complex-queries"></a><span data-ttu-id="9c68e-305">Операторы KQL для сложных запросов</span><span class="sxs-lookup"><span data-stu-id="9c68e-305">KQL operators for complex queries</span></span>
<span data-ttu-id="9c68e-306"><a name="kql_operators"> </a></span><span class="sxs-lookup"><span data-stu-id="9c68e-306"></span></span>

<span data-ttu-id="9c68e-307">Синтаксис языка KQL включает несколько операторов, которые можно использовать для создания сложных запросов.</span><span class="sxs-lookup"><span data-stu-id="9c68e-307">KQL syntax includes several operators that you can use to construct complex queries.</span></span> 
  
    
    

### <a name="boolean-operators"></a><span data-ttu-id="9c68e-308">Логические операторы</span><span class="sxs-lookup"><span data-stu-id="9c68e-308">Boolean operators</span></span>

<span data-ttu-id="9c68e-p128">Используйте логические операторы, чтобы расширить или сузить область поиска. Логические операторы в KQL-запросах можно использовать с произвольными выражениями и ограничениями свойств. В таблице 5 перечислены поддерживаемые логические операторы.</span><span class="sxs-lookup"><span data-stu-id="9c68e-p128">You use Boolean operators to broaden or narrow your search. You can use Boolean operators with free text expressions and property restrictions in KQL queries. Table 5 lists the supported Boolean operators.</span></span>
  
    
    

<span data-ttu-id="9c68e-312">**Таблица 5. Логические операторы, поддерживаемые в KQL**</span><span class="sxs-lookup"><span data-stu-id="9c68e-312">**Table 5. Boolean operators supported in KQL**</span></span>


|<span data-ttu-id="9c68e-313">**Оператор**</span><span class="sxs-lookup"><span data-stu-id="9c68e-313">**Operator**</span></span>|<span data-ttu-id="9c68e-314">**Описание**</span><span class="sxs-lookup"><span data-stu-id="9c68e-314">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="9c68e-315">**AND**</span><span class="sxs-lookup"><span data-stu-id="9c68e-315">**AND**</span></span> <br/> |<span data-ttu-id="9c68e-p129">Возвращает результаты поиска, содержащие все произвольные выражения или ограничения свойств, заданные оператором **AND**. Укажите допустимое произвольное текстовое выражение и (или) допустимое ограничение свойств перед оператором **AND** и после него. Представьте, что используете знак "+". </span><span class="sxs-lookup"><span data-stu-id="9c68e-p129">Returns search results that include all of the free text expressions, or property restrictions specified with the **AND** operator. You must specify a valid free text expression and/or a valid property restriction both preceding and following the **AND** operator. This is the same as using the plus ("+") character. </span></span><br/> |
|<span data-ttu-id="9c68e-319">**NOT**</span><span class="sxs-lookup"><span data-stu-id="9c68e-319">**NOT**</span></span> <br/> |<span data-ttu-id="9c68e-p130">Возвращает результаты поиска, не содержащие заданных произвольных выражений или ограничений свойств. Укажите допустимое произвольное текстовое выражение и (или) допустимое ограничение свойств после оператора **NOT**. Представьте, что используете знак "-".</span><span class="sxs-lookup"><span data-stu-id="9c68e-p130">Returns search results that don't include the specified free text expressions or property restrictions. You must specify a valid free text expression and/or a valid property restriction following the **NOT** operator. This is the same as using the minus ("-") character. </span></span><br/> |
|<span data-ttu-id="9c68e-323">**ИЛИ**</span><span class="sxs-lookup"><span data-stu-id="9c68e-323">**OR**</span></span> <br/> |<span data-ttu-id="9c68e-p131">Возвращает результаты поиска, содержащие одно или несколько заданных произвольных выражений или ограничений свойств. Укажите допустимое произвольное текстовое выражение и (или) допустимое ограничение свойств перед оператором **OR** и после него.</span><span class="sxs-lookup"><span data-stu-id="9c68e-p131">Returns search results that include one or more of the specified free text expressions or property restrictions. You must specify a valid free text expression and/or a valid property restriction both preceding and following the **OR** operator. </span></span><br/> |
   

  
    
    

### <a name="proximity-operators"></a><span data-ttu-id="9c68e-326">Операторы поиска с учетом расположения</span><span class="sxs-lookup"><span data-stu-id="9c68e-326">Proximity operators</span></span>

<span data-ttu-id="9c68e-p132">Используйте операторы поиска с учетом расположения, чтобы получить результаты, в которых заданные термины находятся в непосредственной близости друг от друга. Такие операторы вы можете использовать только с произвольными текстовыми выражениями: они не предназначены для использования с ограничениями свойств в KQL-запросах. Существует два оператора операторы поиска с учетом расположения: **NEAR** и **ONEAR**.</span><span class="sxs-lookup"><span data-stu-id="9c68e-p132">You use proximity operators to match the results where the specified search terms are within close proximity to each other. Proximity operators can be used with free-text expressions only; they are not supported with property restrictions in KQL queries. There are two proximity operators: **NEAR** and **ONEAR**.</span></span>
  
    
    

#### <a name="near-operator"></a><span data-ttu-id="9c68e-330">Оператор NEAR</span><span class="sxs-lookup"><span data-stu-id="9c68e-330">NEAR operator</span></span>

<span data-ttu-id="9c68e-p133">Оператор **NEAR** возвращает совпадения, в которых заданные термины поиска находятся в непосредственной близости друг от друга (при этом не учитывается порядок следования терминов). Синтаксис оператора **NEAR**:</span><span class="sxs-lookup"><span data-stu-id="9c68e-p133">The **NEAR** operator matches the results where the specified search terms are within close proximity to each other, without preserving the order of the terms. The syntax for **NEAR** is as follows:</span></span>
  
    
    
 `<expression> NEAR(n=4) <expression>`
  
    
    
<span data-ttu-id="9c68e-p134">_n_  необязательный параметр, указывающий максимальное расстояние между терминами. Параметр _n_ может принимать целые значения >= 0, значение по умолчанию: **8**.</span><span class="sxs-lookup"><span data-stu-id="9c68e-p134">Where  _n_ is an optional parameter that indicates maximum distance between the terms. The value of _n_ is an integer >= 0 with a default of **8**.</span></span>
  
    
    
<span data-ttu-id="9c68e-335">Параметр  _n_ может быть задан как `n=v`, где  _v_  это значение. Можно указать и сокращенную форму: _v_. Например, в выражении  `NEAR(4)` параметр _v_ равен 4.</span><span class="sxs-lookup"><span data-stu-id="9c68e-335">The parameter  _n_ can be specified as `n=v` where _v_ represents the value, or shortened to only _v_; such as  `NEAR(4)` where _v_ is 4.</span></span>
  
    
    
<span data-ttu-id="9c68e-336">Пример:</span><span class="sxs-lookup"><span data-stu-id="9c68e-336">For example:</span></span>
  
    
    
 `"acquisition" NEAR "debt"`
  
    
    
<span data-ttu-id="9c68e-p135">Результатом запроса будут элементы, в которых термины "acquisition" и "debt" появляются в одном элементе, в котором за термином "acquisition" следует до восьми других терминов, а за ними  "debt" (или наоборот). Порядок терминов при поиске совпадений не учитывается.</span><span class="sxs-lookup"><span data-stu-id="9c68e-p135">This query matches items where the terms "acquisition" and "debt" appear within the same item, where an instance of "acquisition" is followed by up to eight other terms, and then an instance of the term "debt"; or vice versa. The order of the terms is not significant for the match.</span></span>
  
    
    
<span data-ttu-id="9c68e-p136">Если вам нужно меньшее расстояние между терминами, укажите его. Результатом следующего запроса будут элементы, в которых термины "acquisition" и "debt" появляются в одном элементе, при этом между ними не более трех терминов. Порядок следования терминов также не учитывается.</span><span class="sxs-lookup"><span data-stu-id="9c68e-p136">If you need a smaller distance between the terms, you can specify it. The following query matches items where the terms "acquisition" and "debt" appear within the same item, where a maximum distance of 3 between the terms. Once again the order of the terms does not affect the match.</span></span>
  
    
    
 `"acquisition" NEAR(n=3) "debt"`
  
    
    

> <span data-ttu-id="9c68e-342">**Примечание.** В SharePoint оператор **NEAR** больше не сохраняет порядок токенов.</span><span class="sxs-lookup"><span data-stu-id="9c68e-342">**Note:** In SharePoint the **NEAR** operator no longer preserves the ordering of tokens.</span></span> <span data-ttu-id="9c68e-343">Кроме того, оператор **NEAR** теперь принимает необязательный параметр, который указывает на расстояние до токена.</span><span class="sxs-lookup"><span data-stu-id="9c68e-343">In addition, the **NEAR** operator now receives an optional parameter that indicates maximum token distance.</span></span> <span data-ttu-id="9c68e-344">Однако значение по умолчанию все еще равно **8**.</span><span class="sxs-lookup"><span data-stu-id="9c68e-344">However, the default value is still **8**.</span></span> <span data-ttu-id="9c68e-345">Если нужно реализовать предыдущее поведение, используйте оператор **ONEAR**.</span><span class="sxs-lookup"><span data-stu-id="9c68e-345">If you must use the previous behavior, use **ONEAR** instead.</span></span>
  
    
    


#### <a name="onear-operator"></a><span data-ttu-id="9c68e-346">Оператор ONEAR</span><span class="sxs-lookup"><span data-stu-id="9c68e-346">ONEAR operator</span></span>

<span data-ttu-id="9c68e-p138">Оператор **ONEAR** возвращает совпадения, в которых заданные термины поиска находятся в непосредственной близости друг от друга, при этом сохраняется порядок их следования. Ниже приведен синтаксис оператора **ONEAR**, где  _n_  необязательный параметр, указывающий максимальное расстояние между терминами. Параметр _n_ может принимать целые значения >= 0. Значение по умолчанию: **8**.</span><span class="sxs-lookup"><span data-stu-id="9c68e-p138">The **ONEAR** operator matches the results where the specified search terms are within close proximity to each other, while preserving the order of the terms. The syntax for **ONEAR** is as follows, where _n_ is an optional parameter that indicates maximum distance between the terms. The value of _n_ is an integer >= 0 with a default of **8**.</span></span>
  
    
    
 `<expression> ONEAR(n=4) <expression>`
  
    
    
<span data-ttu-id="9c68e-350">Параметр  _n_ может быть задан как `n=v`, где  _v_  это значение. Можно указать и сокращенную форму: _v_. Например, в выражении  `ONEAR(4)` параметр _v_ равен 4.</span><span class="sxs-lookup"><span data-stu-id="9c68e-350">The parameter  _n_ can be specified as `n=v` where _v_ represents the value, or shortened to only _v_; such as  `ONEAR(4)` where _v_ is 4.</span></span>
  
    
    
<span data-ttu-id="9c68e-p139">Например, результатом следующего запроса будут элементы, в которых термины "acquisition" и "debt" появляются в одном элементе, при этом за термином "acquisition" следует до восьми других терминов, а за ними  "debt". Порядок следования терминов **должен** совпадать с их порядком в возвращаемом элементе:</span><span class="sxs-lookup"><span data-stu-id="9c68e-p139">For example, the following query matches items where the terms "acquisition" and "debt" appear within the same item, where an instance of "acquisition" is followed by up to eight other terms, and then an instance of the term "debt". The order of the terms **must** match for an item to be returned:</span></span>
  
    
    
 `"acquisition" ONEAR "debt"`
  
    
    
<span data-ttu-id="9c68e-p140">Если требуется меньшее расстояние между терминами, укажите его, как показано в примере ниже. Результатом следующего запроса будут элементы, в которых термины "acquisition" и "debt" появляются в одном элементе, при этом между ними не более 3 терминов. Порядок следования терминов **должен** совпадать с их порядком в возвращаемом элементе:</span><span class="sxs-lookup"><span data-stu-id="9c68e-p140">If you require a smaller distance between the terms, you can specify it as follows. This query matches items where the terms "acquisition" and "debt" appear within the same item, where a maximum distance of 3 between the terms. The order of the terms **must** match for an item to be returned:</span></span>
  
    
    
 `"acquisition" ONEAR(n=3) "debt"`
  
    
    

### <a name="synonym-operators"></a><span data-ttu-id="9c68e-356">Операторы поиска синонимов</span><span class="sxs-lookup"><span data-stu-id="9c68e-356">Synonym operators</span></span>

<span data-ttu-id="9c68e-p141">Используйте оператор **WORDS**, чтобы указать, что термины в запросе синонимичны, и возвращаемые результаты должны совпадать с любым из заданных терминов. Оператор **WORDS** вы можете использовать только с произвольными текстовыми выражениями. Его использование с ограничениями свойств в KQL-запросах не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="9c68e-p141">You use the **WORDS** operator to specify that the terms in the query are synonyms, and that results returned should match either of the specified terms. You can use the **WORDS** operator with free text expressions only; it is not supported with property restrictions in KQL queries.</span></span>
  
    
    
<span data-ttu-id="9c68e-p142">Указанный ниже пример запроса выдает результаты, содержащие термин "TV" или "television". Под ним приведен еще один запрос, его результаты аналогичны предыдущим.</span><span class="sxs-lookup"><span data-stu-id="9c68e-p142">The following query example matches results that contain either the term "TV" or the term "television". This matching behavior is the same as if you had used the following query:</span></span>
  
    
    
 `WORDS(TV, Television)`
  
    
    
 `TV OR Television`
  
    
    
<span data-ttu-id="9c68e-p143">Эти запросы отличаются ранжированием результатов. При использовании оператора **WORDS** термины "TV" и "television" рассматриваются как синонимы, а не как отдельные термины. Поэтому оба эти термина ранжируются, как если бы они были одним термином. Например, элемент контента, содержащий один термин "television" и пять терминов "TV", ранжируется так же, как элемент контента с шестью терминами "TV".</span><span class="sxs-lookup"><span data-stu-id="9c68e-p143">These queries differ in how the results are ranked. When you use the **WORDS** operator, the terms "TV" and "television" are treated as synonyms instead of separate terms. Therefore, instances of either term are ranked as if they were the same term. For example, a content item that contained one instance of the term "television" and five instances of the term "TV" would be ranked the same as a content item with six instances of the term "TV".</span></span>
  
    
    

### <a name="wildcard-operator"></a><span data-ttu-id="9c68e-365">Оператор подстановочного знака</span><span class="sxs-lookup"><span data-stu-id="9c68e-365">Wildcard operator</span></span>

<span data-ttu-id="9c68e-366">Используйте оператор подстановочного знака (символ звездочки, "**\***"), чтобы включить сопоставление префиксов.</span><span class="sxs-lookup"><span data-stu-id="9c68e-366">You use the wildcard operator—the asterisk character (" **\*** ")—to enable prefix matching.</span></span> <span data-ttu-id="9c68e-367">Вы можете указать в запросе начальную часть слова, поставив далее оператор подстановочного знака, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="9c68e-367">You can specify part of a word, from the beginning of the word, followed by the wildcard operator, in your query, as follows.</span></span> <span data-ttu-id="9c68e-368">Результат следующего запроса — термины, начинающиеся на "serv" (при этом далее могут следовать другие знаки), например "serve", "server", "service":</span><span class="sxs-lookup"><span data-stu-id="9c68e-368">You use the wildcard operator—the asterisk character ("*")—to enable prefix matching. You can specify part of a word, from the beginning of the word, followed by the wildcard operator, in your query, as follows. This query would match results that include terms beginning with "serv", followed by zero or more characters, such as serve, server, service, and so on:</span></span>
  
    
    
 `serv*`
  
    
    

### <a name="inclusion-and-exclusion-operators"></a><span data-ttu-id="9c68e-369">Операторы включения и исключения</span><span class="sxs-lookup"><span data-stu-id="9c68e-369">Inclusion and exclusion operators</span></span>

<span data-ttu-id="9c68e-370">С помощью операторов включения и исключения, описанных в таблице 6, вы можете указать, будут ли возвращаемые результаты включать или исключать контент, совпадающий со значением, указанным в произвольном текстовом выражении или ограничении свойств.</span><span class="sxs-lookup"><span data-stu-id="9c68e-370">You can specify whether the results that are returned should include or exclude content that matches the value specified in the free text expression or the property restriction by using the inclusion and exclusion operators, described in Table 6.</span></span>
  
    
    

<span data-ttu-id="9c68e-371">**Таблица 6. Операторы для включения и исключения контента в результатах**</span><span class="sxs-lookup"><span data-stu-id="9c68e-371">**Table 6. Operators for including and excluding content in results**</span></span>


|<span data-ttu-id="9c68e-372">**Имя**</span><span class="sxs-lookup"><span data-stu-id="9c68e-372">**Name**</span></span>|<span data-ttu-id="9c68e-373">**Оператор**</span><span class="sxs-lookup"><span data-stu-id="9c68e-373">**Operator**</span></span>|<span data-ttu-id="9c68e-374">**Поведение**</span><span class="sxs-lookup"><span data-stu-id="9c68e-374">**Behavior**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="9c68e-375">Включение</span><span class="sxs-lookup"><span data-stu-id="9c68e-375">Inclusion</span></span>  <br/> |<span data-ttu-id="9c68e-376">" **+** "</span><span class="sxs-lookup"><span data-stu-id="9c68e-376"></span></span> <br/> |<span data-ttu-id="9c68e-377">Включает в результаты контент со значениями, совпадающими с теми, которые нужно включить.</span><span class="sxs-lookup"><span data-stu-id="9c68e-377">Includes content with values that match the inclusion.</span></span>  <br/> <span data-ttu-id="9c68e-p145">Это поведение по умолчанию, если символы не указаны. Аналогичный результат будет при использовании оператора **AND**.</span><span class="sxs-lookup"><span data-stu-id="9c68e-p145">This is the default behavior if no character is specified. This is the same as using the **AND** operator. </span></span><br/> |
|<span data-ttu-id="9c68e-380">Исключения</span><span class="sxs-lookup"><span data-stu-id="9c68e-380">Exclusion</span></span>  <br/> |<span data-ttu-id="9c68e-381">" **-** "</span><span class="sxs-lookup"><span data-stu-id="9c68e-381"></span></span> <br/> |<span data-ttu-id="9c68e-p146">Исключает контент со значениями, совпадающими с теми, которые нужно исключить. Аналогичный результат будет при использовании оператора **NOT**.</span><span class="sxs-lookup"><span data-stu-id="9c68e-p146">Excludes content with values that match the exclusion. This is the same as using the **NOT** operator. </span></span><br/> |
   

### <a name="dynamic-ranking-operator"></a><span data-ttu-id="9c68e-384">Оператор динамического ранжирования</span><span class="sxs-lookup"><span data-stu-id="9c68e-384">Dynamic ranking operator</span></span>

<span data-ttu-id="9c68e-p147">Применяйте оператор **XRANK**, чтобы повысить динамический рейтинг элементов в зависимости от повторений определенных терминов в  _match expression_, не меняя состав элементов, удовлетворяющих критериям запроса. Выражение **XRANK** содержит один компонент, совпадение с которым обязательно ( _match expression_), и один или несколько компонентов, которые влияют только на динамическое ранжирование ( _rank expression_). Должен быть задан хотя бы **один** параметр (за исключением _n_), чтобы выражение **XRANK** было допустимым.</span><span class="sxs-lookup"><span data-stu-id="9c68e-p147">You use the **XRANK** operator to boost the dynamic rank of items based on certain term occurrences within the _match expression_, without changing which items match the query. An **XRANK** expression contains one component that must be matched, the _match expression_, and one or more components that contribute only to dynamic ranking, the  _rank expression_. At least **one** of the parameters, excluding _n_, must be specified for an **XRANK** expression to be valid.</span></span>
  
    
    
 <span data-ttu-id="9c68e-p148">Параметр  _Match expressions_ может быть любым допустимым выражением KQL, включая вложенные выражения **XRANK**. Параметр  _Rank expressions_ может быть любым допустимым выражением в языке KQL, кроме выражений **XRANK**. Если KQL-запросы содержат несколько операторов **XRANK**, итоговое значение динамического рейтинга рассчитывается как сумма увеличений по всем операторам **XRANK**.</span><span class="sxs-lookup"><span data-stu-id="9c68e-p148">_Match expressions_ may be any valid KQL expression, including nested **XRANK** expressions. _Rank expressions_ may be any valid KQL expression without **XRANK** expressions. If your KQL queries have multiple **XRANK** operators, the final dynamic rank value is calculated as a sum of boosts across all **XRANK** operators.</span></span>
  
    
    

> <span data-ttu-id="9c68e-391">**Примечание.** Используйте скобки, чтобы явно указать порядок вычисления для KQL-запросов, содержащих более одного оператора **XRANK** на одном уровне.</span><span class="sxs-lookup"><span data-stu-id="9c68e-391">**Note** Use parenthesis to explicitly indicate the order of computation for KQL queries that have more than one **XRANK** operator at the same level.</span></span>
  
    
    

<span data-ttu-id="9c68e-392">Можно использовать следующий синтаксис оператора **XRANK**:</span><span class="sxs-lookup"><span data-stu-id="9c68e-392">You can use the **XRANK** operator in the following syntax:</span></span>
  
    
    
 `<match expression> XRANK(cb=100, rb=0.4, pb=0.4, avgb=0.4, stdb=0.4, nb=0.4, n=200) <rank expression>`
  
    
    
<span data-ttu-id="9c68e-393">Динамического рейтинг с использованием оператора **XRANK** вычисляется по формуле:</span><span class="sxs-lookup"><span data-stu-id="9c68e-393">The **XRANK** operator's dynamic ranking calculation is based on this formula:</span></span>
  
    
    

  
    
    
![Формула для оператора XRANK](../images/XRANKFormula.gif)
  
    
    
<span data-ttu-id="9c68e-395">В таблице 7 перечислены основные параметры, доступные для оператора **XRANK**.</span><span class="sxs-lookup"><span data-stu-id="9c68e-395">Table 7 lists the basic parameters available for the **XRANK** operator.</span></span>
  
    
    

<span data-ttu-id="9c68e-396">**Таблица 7. Параметры оператора XRANK**</span><span class="sxs-lookup"><span data-stu-id="9c68e-396">**Table 7. XRANK operator parameters**</span></span>


|<span data-ttu-id="9c68e-397">**Параметр**</span><span class="sxs-lookup"><span data-stu-id="9c68e-397">**Parameter**</span></span>|<span data-ttu-id="9c68e-398">**Значение**</span><span class="sxs-lookup"><span data-stu-id="9c68e-398">**Value**</span></span>|<span data-ttu-id="9c68e-399">**Описание**</span><span class="sxs-lookup"><span data-stu-id="9c68e-399">**Description**</span></span>|
|:-----|:-----|:-----|
| _n_ <br/> | <span data-ttu-id="9c68e-400">_<integer_value>_</span><span class="sxs-lookup"><span data-stu-id="9c68e-400">_<integer_value>_</span></span> <br/> |<span data-ttu-id="9c68e-401">Указывает количество результатов для вычисления статистики.</span><span class="sxs-lookup"><span data-stu-id="9c68e-401">Specifies the number of results to compute statistics from.</span></span>  <br/> <span data-ttu-id="9c68e-402">Этот параметр не влияет на количество результатов, на которые влияет динамический рейтинг. С его помощью из вычисления статистики просто исключаются ненужные элементы.</span><span class="sxs-lookup"><span data-stu-id="9c68e-402">This parameter does not affect the number of results that the dynamic rank contributes to; it is just a means to exclude irrelevant items from the statistics calculations.</span></span>  <br/> <span data-ttu-id="9c68e-p149"> По умолчанию: **0**. Нулевое значение означает *все документы*  . </span><span class="sxs-lookup"><span data-stu-id="9c68e-p149">Default: **0**. A zero value carries the semantic of *all documents*  . </span></span><br/> |
| <span data-ttu-id="9c68e-405">_nb_</span><span class="sxs-lookup"><span data-stu-id="9c68e-405">_nb_</span></span> <br/> | <span data-ttu-id="9c68e-406">_<float_value>_</span><span class="sxs-lookup"><span data-stu-id="9c68e-406">_<float_value>_</span></span> <br/> |<span data-ttu-id="9c68e-p150">Параметр  _nb_ относится к нормированному увеличению. Этот параметр определяет коэффициент, на который умножается произведение дисперсии и среднего арифметического значений рейтингов в наборе результатов.</span><span class="sxs-lookup"><span data-stu-id="9c68e-p150">The  _nb_ parameter refers to normalized boost. This parameter specifies the factor that is multiplied with the product of the variance and average score of the rank values of the results set. </span></span><br/>  <span data-ttu-id="9c68e-409">Параметр  _f_ в формуле XRANK.</span><span class="sxs-lookup"><span data-stu-id="9c68e-409">_f_ in the XRANK formula.</span></span> <br/> |
   
<span data-ttu-id="9c68e-p151">Обычно нормированное увеличение ( _nb_)  единственный изменяемый параметр. Этого параметра достаточно, чтобы понижать или повышать рейтинг отдельного элемента, не учитывая стандартное отклонение.</span><span class="sxs-lookup"><span data-stu-id="9c68e-p151">Typically, normalized boost,  _nb_, is the only parameter that is modified. This parameter provides the necessary control to promote or demote a particular item, without taking standard deviation into account.</span></span> 
  
    
    
<span data-ttu-id="9c68e-p152">Доступны также дополнительные параметры, указанные ниже. Но обычно они не используются.</span><span class="sxs-lookup"><span data-stu-id="9c68e-p152">The following advanced parameters are also available. However, typically they're not used.</span></span>
  
    
    

<span data-ttu-id="9c68e-414">**Таблица 8. Дополнительные параметры оператора XRANK**</span><span class="sxs-lookup"><span data-stu-id="9c68e-414">**Table 8. Advanced parameters for XRANK**</span></span>


|<span data-ttu-id="9c68e-415">**Параметр**</span><span class="sxs-lookup"><span data-stu-id="9c68e-415">**Parameter**</span></span>|<span data-ttu-id="9c68e-416">**Значение**</span><span class="sxs-lookup"><span data-stu-id="9c68e-416">**Value**</span></span>|<span data-ttu-id="9c68e-417">**Описание**</span><span class="sxs-lookup"><span data-stu-id="9c68e-417">**Description**</span></span>|
|:-----|:-----|:-----|
| <span data-ttu-id="9c68e-418">_cb_</span><span class="sxs-lookup"><span data-stu-id="9c68e-418">_cb_</span></span> <br/> | <span data-ttu-id="9c68e-419">_<float_value>_</span><span class="sxs-lookup"><span data-stu-id="9c68e-419">_<float_value>_</span></span> <br/> |<span data-ttu-id="9c68e-420">Параметр  _cb_ увеличивает рейтинг на постоянную величину.</span><span class="sxs-lookup"><span data-stu-id="9c68e-420">The  _cb_ parameter refers to constant boost.</span></span> <br/> <span data-ttu-id="9c68e-421">Значение по умолчанию: **0**.</span><span class="sxs-lookup"><span data-stu-id="9c68e-421">Default: **0**.</span></span> <br/>  <span data-ttu-id="9c68e-422">Параметр  _a_ в формуле XRANK.</span><span class="sxs-lookup"><span data-stu-id="9c68e-422">_a_ in the XRANK formula.</span></span> <br/> |
| <span data-ttu-id="9c68e-423">_stdb_</span><span class="sxs-lookup"><span data-stu-id="9c68e-423">_stdb_</span></span> <br/> | <span data-ttu-id="9c68e-424">_<float_value>_</span><span class="sxs-lookup"><span data-stu-id="9c68e-424">_<float_value>_</span></span> <br/> |<span data-ttu-id="9c68e-425">Параметр  _stdb_ увеличивает рейтинг на величину стандартного отклонения.</span><span class="sxs-lookup"><span data-stu-id="9c68e-425">The  _stdb_ parameter refers to standard deviation boost.</span></span> <br/> <span data-ttu-id="9c68e-426">Значение по умолчанию: **0**.</span><span class="sxs-lookup"><span data-stu-id="9c68e-426">Default: **0**.</span></span> <br/>  <span data-ttu-id="9c68e-427">Параметр  _e_ в формуле XRANK.</span><span class="sxs-lookup"><span data-stu-id="9c68e-427">_e_ in the XRANK formula.</span></span> <br/> |
| <span data-ttu-id="9c68e-428">_avgb_</span><span class="sxs-lookup"><span data-stu-id="9c68e-428">_avgb_</span></span> <br/> | <span data-ttu-id="9c68e-429">_<float_value>_</span><span class="sxs-lookup"><span data-stu-id="9c68e-429">_<float_value>_</span></span> <br/> |<span data-ttu-id="9c68e-430">Параметр  _avgb_ увеличивает рейтинг на среднее значение.</span><span class="sxs-lookup"><span data-stu-id="9c68e-430">The  _avgb_ parameter refers to average boost.</span></span> <br/> <span data-ttu-id="9c68e-431">По умолчанию: **0**.</span><span class="sxs-lookup"><span data-stu-id="9c68e-431">Default: **0**.</span></span> <br/>  <span data-ttu-id="9c68e-432">Параметр  _d_ в формуле XRANK.</span><span class="sxs-lookup"><span data-stu-id="9c68e-432">_d_ in the XRANK formula.</span></span> <br/> |
| <span data-ttu-id="9c68e-433">_rb_</span><span class="sxs-lookup"><span data-stu-id="9c68e-433">_rb_</span></span> <br/> | <span data-ttu-id="9c68e-434">_<float_value>_</span><span class="sxs-lookup"><span data-stu-id="9c68e-434">_<float_value>_</span></span> <br/> |<span data-ttu-id="9c68e-p153">Параметр  _rb_ увеличивает рейтинг в диапазоне. Этот коэффициент умножается на диапазон значений рейтингов в наборе результатов.</span><span class="sxs-lookup"><span data-stu-id="9c68e-p153">The  _rb_ parameter refers to range boost. This factor is multiplied with the range of rank values in the results set. </span></span><br/> <span data-ttu-id="9c68e-437">Значение по умолчанию: **0**.</span><span class="sxs-lookup"><span data-stu-id="9c68e-437">Default: **0**.</span></span> <br/>  <span data-ttu-id="9c68e-438">Параметр  _b_ в формуле XRANK.</span><span class="sxs-lookup"><span data-stu-id="9c68e-438">_b_ in the XRANK formula.</span></span> <br/> |
| <span data-ttu-id="9c68e-439">_pb_</span><span class="sxs-lookup"><span data-stu-id="9c68e-439">_pb_</span></span> <br/> | <span data-ttu-id="9c68e-440">_<float_value>_</span><span class="sxs-lookup"><span data-stu-id="9c68e-440">_<float_value>_</span></span> <br/> |<span data-ttu-id="9c68e-p154">Параметр  _pb_ задает увеличение в процентах. Этот коэффициент умножается на собственный рейтинг элемента в сравнении с минимальным значением в наборе.</span><span class="sxs-lookup"><span data-stu-id="9c68e-p154">The  _pb_ parameter refers to percentage boost. This factor is multiplied with the item's own rank compared to the minimum value in the corpus. </span></span><br/> <span data-ttu-id="9c68e-443">Значение по умолчанию: **0**.</span><span class="sxs-lookup"><span data-stu-id="9c68e-443">Default: **0**.</span></span> <br/>  <span data-ttu-id="9c68e-444">Параметр  _c_ в формуле XRANK.</span><span class="sxs-lookup"><span data-stu-id="9c68e-444">_c_ in the XRANK formula.</span></span> <br/> |
   

#### <a name="examples"></a><span data-ttu-id="9c68e-445">Примеры</span><span class="sxs-lookup"><span data-stu-id="9c68e-445">Examples</span></span>

 <span data-ttu-id="9c68e-p155">**Пример 1.** Следующее выражение сопоставляет элементы, для которых полнотекстовый индекс по умолчанию содержит "cat" или "dog". Выражение увеличивает на постоянную величину 100 динамический рейтинг элементов, содержащих также термин "thoroughbred".</span><span class="sxs-lookup"><span data-stu-id="9c68e-p155">**Example 1.** The following expression matches items for which the default full-text index contains either "cat" or "dog". The expression increases dynamic rank of those items with a constant boost of 100 for items that also contain "thoroughbred".</span></span>
  
    
    
 `(cat OR dog) XRANK(cb=100) thoroughbred`
  
    
    
 <span data-ttu-id="9c68e-p156">**Пример 2.** Следующее выражение сопоставляет элементы, для которых полнотекстовый индекс по умолчанию содержит термины "cat" или "dog". Выражение увеличивает динамический рейтинг элементов на нормированную величину 1,5 для элементов, содержащих также термин "thoroughbred".</span><span class="sxs-lookup"><span data-stu-id="9c68e-p156">**Example 2.** The following expression matches items for which the default full-text index contains either "cat" or "dog". The expression increases dynamic rank of those items with a normalized boost of 1.5 for items that also contain "thoroughbred".</span></span>
  
    
    
 `(cat OR dog) XRANK(nb=1.5) thoroughbred`
  
    
    
 <span data-ttu-id="9c68e-p157">**Пример 3.** Следующее выражение сопоставляет элементы, для которых полнотекстовый индекс по умолчанию содержит термины "cat" или "dog". Выражение увеличивает динамический рейтинг элементов на постоянную величину 100 и нормированную величину 1,5 для элементов, содержащих также термин "thoroughbred".</span><span class="sxs-lookup"><span data-stu-id="9c68e-p157">**Example 3.** The following expression matches items for which the default full-text index contains either "cat" or "dog". The expression increases dynamic rank of those items with a constant boost of 100 and a normalized boost of 1.5, for items that also contain "thoroughbred".</span></span>
  
    
    
 `(cat OR dog) XRANK(cb=100, nb=1.5) thoroughbred`
  
    
    
 <span data-ttu-id="9c68e-p158">**Пример 4.** Следующее выражение сопоставляет все элементы, содержащие термин "animals", и увеличивает динамический рейтинг следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9c68e-p158">**Example 4.** The following expression matches all items containing the term "animals", and boosts dynamic rank as follows:</span></span>
  
    
    

- <span data-ttu-id="9c68e-457">динамический рейтинг элементов, содержащих термин "dogs", увеличивается на 100 баллов;</span><span class="sxs-lookup"><span data-stu-id="9c68e-457">Dynamic rank of items that contain the term "dogs" is boosted by 100 points.</span></span>
    
  
- <span data-ttu-id="9c68e-458">динамический рейтинг элементов, содержащих термин "cats", увеличивается на 200 баллов;</span><span class="sxs-lookup"><span data-stu-id="9c68e-458">Dynamic rank of items that contain the term "cats" is boosted by 200 points.</span></span>
    
  
- <span data-ttu-id="9c68e-459">динамический рейтинг элементов, содержащих и термин "dogs", и термин "cats", увеличивается на 300 баллов.</span><span class="sxs-lookup"><span data-stu-id="9c68e-459">Dynamic rank of items that contain both the terms "dogs" and "cats" is boosted by 300 points.</span></span>
    
  
 `(animals XRANK(cb=100) dogs) XRANK(cb=200) cats`
  
    
    

### <a name="parenthesis"></a><span data-ttu-id="9c68e-460">Круглые скобки</span><span class="sxs-lookup"><span data-stu-id="9c68e-460">Parenthesis</span></span>

<span data-ttu-id="9c68e-p159">Можно объединять разные части запросов по ключевым словам с помощью открывающей скобки " **(** " и закрывающей скобки " **)** ". Каждой открывающей скобке " **(** " должна соответствовать закрывающая скобка " **)** ". Пробел до или после скобки не влияет на запрос.</span><span class="sxs-lookup"><span data-stu-id="9c68e-p159">You can combine different parts of a keyword query by using the opening parenthesis character " **(** " and closing parenthesis character " **)** ". Each opening parenthesis " **(** " must have a matching closing parenthesis " **)** ". A white space before or after a parenthesis does not affect the query.</span></span>
  
    
    

## <a name="additional-resources"></a><span data-ttu-id="9c68e-464">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="9c68e-464">Additional resources</span></span>
<span data-ttu-id="9c68e-465"><a name="SP15KQL_addlresources"> </a></span><span class="sxs-lookup"><span data-stu-id="9c68e-465"></span></span>


-  [<span data-ttu-id="9c68e-466">Построение запросов поиска в SharePoint</span><span class="sxs-lookup"><span data-stu-id="9c68e-466">Building search queries in SharePoint</span></span>](building-search-queries-in-sharepoint.md)
    
  
