---
title: "Создание поисковых запросов в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: c4372fcc-4574-4c81-a345-a1bb282ca8f7
ms.openlocfilehash: d2dfcbbe782057d012f72ca05328316638db635f
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="building-search-queries-in-sharepoint"></a><span data-ttu-id="16b5f-102">Создание поисковых запросов в SharePoint</span><span class="sxs-lookup"><span data-stu-id="16b5f-102">Building search queries in SharePoint</span></span>
<span data-ttu-id="16b5f-103">Узнайте о синтаксисе поиска, который поддерживается в SharePoint для создания правил запроса и поисковых запросов.</span><span class="sxs-lookup"><span data-stu-id="16b5f-103">Learn about the search syntax supported in SharePoint for building query rules and search queries.</span></span>
## <a name="supported-search-syntax-in-sharepoint-for-building-search-queries"></a><span data-ttu-id="16b5f-104">Поддерживаемый синтаксис поиска в SharePoint для создания поисковых запросов</span><span class="sxs-lookup"><span data-stu-id="16b5f-104">Supported search syntax in SharePoint for building search queries</span></span>
<span data-ttu-id="16b5f-105"><a name="SP15Buildquery_support"> </a></span><span class="sxs-lookup"><span data-stu-id="16b5f-105"><a name="SP15Buildquery_support"> </a></span></span>

<span data-ttu-id="16b5f-106">Поиск в SharePoint поддерживает синтаксис языка запросов по ключевым словам (KQL) и языка запросов FAST (FQL).</span><span class="sxs-lookup"><span data-stu-id="16b5f-106">SharePoint search supports Keyword Query Language (KQL) and FAST Query Language (FQL) search syntax for building search queries.</span></span>
  
    
    
 <span data-ttu-id="16b5f-107">**Язык запросов по ключевым словам (KQL)**</span><span class="sxs-lookup"><span data-stu-id="16b5f-107">**Keyword Query Language (KQL)**</span></span>
  
    
    
<span data-ttu-id="16b5f-p101">KQL  это язык запросов для создания поисковых запросов, использующийся по умолчанию. С его помощью можно задать условия поиска или ограничения свойств, передающиеся в службу поиска SharePoint.</span><span class="sxs-lookup"><span data-stu-id="16b5f-p101">KQL is the default query language for building search queries. Using KQL, you specify the search terms or property restrictions that are passed to the SharePoint search service.</span></span>
  
    
    
 <span data-ttu-id="16b5f-110">**Язык запросов FAST (FQL)**</span><span class="sxs-lookup"><span data-stu-id="16b5f-110">**FAST Query Language (FQL)**</span></span>
  
    
    
<span data-ttu-id="16b5f-p102">FQL  это язык SQL, поддерживающий расширенные операторы запросов. Его можно использовать для создания сложных запросов, которые необходимо программно передать в службу запросов SharePoint. FQL не предназначен для пользователей и отключен по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="16b5f-p102">FQL is a structured query language that supports advanced query operators. You can use FQL when you want to create complex queries that you want to pass programmatically to the SharePoint search service. FQL isn't intended to be exposed to end users, and is disabled by default.</span></span> 
  
    
    
<span data-ttu-id="16b5f-p103">Чтобы его включить, используйте свойство **EnableFQL**. Затем скопируйте источник результатов по умолчанию и измените строку преобразования запроса  `{?{searchTerms} -ContentClass=urn:content-class:SPSPeople}` на одном из трех уровней (в приложении службы поиска, или SSA, семействе веб-сайтов, а также на сайте), одним из этих способов:</span><span class="sxs-lookup"><span data-stu-id="16b5f-p103">To enable FQL, use the **EnableFQL** property. Then, copy the default result source and modify the Query Transformation string `{?{searchTerms} -ContentClass=urn:content-class:SPSPeople}`, at one of these levels -- Search Service Application (SSA), Site Collection, or Site -- and in one of the following ways:</span></span>
  
    
    

- <span data-ttu-id="16b5f-p104">Удалите фильтр KQL  `-ContentClass:urn:content-class:SPSPeople` в строке преобразования запроса. В результате получится следующая строка: `{?{searchTerms}}`.</span><span class="sxs-lookup"><span data-stu-id="16b5f-p104">Remove the KQL filter,  `-ContentClass:urn:content-class:SPSPeople`, from the Query Transformation. The resulting Query Transformation string will be:  `{?{searchTerms}}`</span></span>
    
  
- <span data-ttu-id="16b5f-118">Замените строку преобразования запроса на эквивалентную строку на языке FQL, например `{?andnot({searchTerms},filter(contentclass:"urn:content-class:SPSPeople*"))}`.</span><span class="sxs-lookup"><span data-stu-id="16b5f-118">Replace the Query Transformation string with an FQL equivalent, such as  `{?andnot({searchTerms},filter(contentclass:"urn:content-class:SPSPeople*"))}`.</span></span>
    
  
<span data-ttu-id="16b5f-119">Дополнительные сведения об источниках результатов и принципах их использования см. в статьях [Источники результатов](http://office.microsoft.com/ru-RU/support/sharepoint/sharepointsearch/understanding-result-sources-HA102848849.aspx) и [Настройка источников результатов для поиска в SharePoint](http://technet.microsoft.com/ru-RU/library/jj683115%28v=office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="16b5f-119">For more information about result sources and how they work, see to:  [Understanding result sources](http://office.microsoft.com/ru-RU/support/sharepoint/sharepointsearch/understanding-result-sources-HA102848849.aspx) and [Configure result sources for search in SharePoint](http://technet.microsoft.com/ru-RU/library/jj683115%28v=office.15%29.aspx).</span></span>
  
    
    

## <a name="in-this-section"></a><span data-ttu-id="16b5f-120">В этом разделе:</span><span class="sxs-lookup"><span data-stu-id="16b5f-120">In this section</span></span>
<span data-ttu-id="16b5f-121"><a name="SP15Buildquery_support"> </a></span><span class="sxs-lookup"><span data-stu-id="16b5f-121"><a name="SP15Buildquery_support"> </a></span></span>


-  [<span data-ttu-id="16b5f-122">Справочник по синтаксису языка запросов по ключевым словам (KQL)</span><span class="sxs-lookup"><span data-stu-id="16b5f-122">Keyword Query Language (KQL) syntax reference</span></span>](keyword-query-language-kql-syntax-reference.md)
    
  
-  [<span data-ttu-id="16b5f-123">справочник по синтаксису языка запросов FAST (FQL)</span><span class="sxs-lookup"><span data-stu-id="16b5f-123">FAST Query Language (FQL) syntax reference</span></span>](fast-query-language-fql-syntax-reference.md)
    
  
-  [<span data-ttu-id="16b5f-124">Использование API поисковых запросов SharePoint</span><span class="sxs-lookup"><span data-stu-id="16b5f-124">Using the SharePoint search Query APIs</span></span>](using-the-sharepoint-search-query-apis.md)
    
  

## <a name="see-also"></a><span data-ttu-id="16b5f-125">См. также</span><span class="sxs-lookup"><span data-stu-id="16b5f-125">See also</span></span>
<span data-ttu-id="16b5f-126"><a name="SP15Buildquery_addlresources"> </a></span><span class="sxs-lookup"><span data-stu-id="16b5f-126"><a name="SP15Buildquery_addlresources"> </a></span></span>


-  [<span data-ttu-id="16b5f-127">Поиск в SharePoint</span><span class="sxs-lookup"><span data-stu-id="16b5f-127">Search in SharePoint</span></span>](search-in-sharepoint.md)
    
  
-  [<span data-ttu-id="16b5f-128">Планирование преобразования запросов и упорядочивания результатов в SharePoint</span><span class="sxs-lookup"><span data-stu-id="16b5f-128">Overview of query processing in SharePoint</span></span>](http://technet.microsoft.com/ru-RU/library/jj219620%28v=office.15%29.aspx)
    
  
-  [<span data-ttu-id="16b5f-129">Переменные запроса в SharePoint</span><span class="sxs-lookup"><span data-stu-id="16b5f-129">Query variables in SharePoint</span></span>](http://technet.microsoft.com/ru-RU/library/jj683123.aspx)
    
  

