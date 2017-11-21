---
title: "Поиск в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 59220f81-0e5e-4945-8056-cf0a116446cb
ms.openlocfilehash: daf7d446efd7f20a8123b86e8325cc5f0253cd8d
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="search-in-sharepoint"></a><span data-ttu-id="d3370-102">Поиск в SharePoint</span><span class="sxs-lookup"><span data-stu-id="d3370-102">Search in SharePoint</span></span>
<span data-ttu-id="d3370-p101">Информация о расширяемости стандартных блоков в Поиск в SharePoint и об их использовании в подходящих для вас вариантах использования. Поиск в SharePoint позволяет пользователям еще легче и быстрее находить необходимую информацию и облегчает настройку возможностей поиска для администраторов поиска. Кроме того, он предоставляет несколько наборов интерфейсов API для расширенной настройки и решений.</span><span class="sxs-lookup"><span data-stu-id="d3370-p101">Understand the extensibility building blocks in Search in SharePoint and how you can use these building blocks to suit your use cases. Search in SharePoint enables users to find relevant information more quickly and easily than ever before and makes it easy for Search administrators to customize the search experience. It also provides several API sets for more advanced customizations and solutions.</span></span>
  
    
    

<span data-ttu-id="d3370-106">Перед тем как продолжить рекомендуем более детально ознакомиться с общими концепциями разработки SharePoint, которые представлены в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="d3370-106">See the following articles for a good introduction to general SharePoint development concepts; you may find it helpful to review these before proceeding:</span></span>
-  [<span data-ttu-id="d3370-107">Настройка общей среды разработки для SharePoint</span><span class="sxs-lookup"><span data-stu-id="d3370-107">Set up a general development environment for SharePoint</span></span>](set-up-a-general-development-environment-for-sharepoint.md)
    
  
-  [<span data-ttu-id="d3370-108">Выбор правильного набора API в SharePoint</span><span class="sxs-lookup"><span data-stu-id="d3370-108">Choose the right API set in SharePoint</span></span>](choose-the-right-api-set-in-sharepoint.md)
    
  
-  [<span data-ttu-id="d3370-109">Сравнение надстроек SharePoint с решениями SharePoint</span><span class="sxs-lookup"><span data-stu-id="d3370-109">SharePoint Add-ins compared with SharePoint solutions</span></span>](sharepoint-add-ins-compared-with-sharepoint-solutions.md)
    
  
-  [<span data-ttu-id="d3370-110">Выбор между надстройки SharePoint и решений SharePoint</span><span class="sxs-lookup"><span data-stu-id="d3370-110">Deciding between SharePoint Add-ins and SharePoint solutions</span></span>](deciding-between-sharepoint-add-ins-and-sharepoint-solutions.md)
    
  

## <a name="search-architecture-overview"></a><span data-ttu-id="d3370-111">Общие сведения об архитектуре поиска</span><span class="sxs-lookup"><span data-stu-id="d3370-111">Search architecture overview</span></span>

<span data-ttu-id="d3370-p102">Поиск в SharePoint включает широкий ряд усовершенствований и новых функций. В этой версии Поиск в SharePoint реорганизован в единую корпоративную поисковую платформу. Архитектура поиска включает следующие области:</span><span class="sxs-lookup"><span data-stu-id="d3370-p102">Search in SharePoint includes a wide variety of improvements and new features. With this version, Search in SharePoint is re-architected to a single enterprise search platform. The search architecture consists of the following areas:</span></span>
  
    
    

-  <span data-ttu-id="d3370-115">[Обход и обработка контента](#bk_crawl);</span><span class="sxs-lookup"><span data-stu-id="d3370-115">[Crawl and content processing](#bk_crawl)</span></span>
    
  
-  <span data-ttu-id="d3370-116">[Индекс](#bk_index);</span><span class="sxs-lookup"><span data-stu-id="d3370-116">[Index](#bk_index)</span></span>
    
  
-  <span data-ttu-id="d3370-117">[Обработка запросов](#bk_query);</span><span class="sxs-lookup"><span data-stu-id="d3370-117">[Query processing](#bk_query)</span></span>
    
  
-  <span data-ttu-id="d3370-118">[Администрирование поиска](#bk_searchadmin);</span><span class="sxs-lookup"><span data-stu-id="d3370-118">[Search administration](#bk_searchadmin)</span></span>
    
  
-  <span data-ttu-id="d3370-119">[Аналитика](#bk_analytics).</span><span class="sxs-lookup"><span data-stu-id="d3370-119">[Analytics](#bk_analytics)</span></span>
    
  
<span data-ttu-id="d3370-p103">Эти области состоят из компонентов и баз данных, которые слаженно работают, чтобы выполнить операцию поиска. На рис. 1 представлен общий вид различных областей архитектуры поиска и внутренние компоненты и базы данных, чья слаженная работа направлена на выполнение операции поиска.</span><span class="sxs-lookup"><span data-stu-id="d3370-p103">These areas consist of components and databases that work cohesively to perform the search operation. Figure 1 provides an overall view of the different areas of search architecture, and the components and databases within that work cohesively to perform the search operation.</span></span> 
  
    
    

<span data-ttu-id="d3370-122">**Рис. 1. Взаимодействие компонентов поиска**</span><span class="sxs-lookup"><span data-stu-id="d3370-122">**Figure 1. Search component interaction**</span></span>

  
    
    

  
    
    
![Взаимодействие компонентов поиска](../images/SearchComponentInteraction.jpg)
  
    
    
<span data-ttu-id="d3370-124">Более подробное представление доступно в [разделе "Поиск" на странице с техническими графиками](http://technet.microsoft.com/ru-RU/library/cc263199.aspx#search) и статье [Обзор поиска в SharePoint](http://technet.microsoft.com/ru-RU/library/jj219738.aspx).</span><span class="sxs-lookup"><span data-stu-id="d3370-124">For a more detailed view, see  [Technical Diagrams -- Search](http://technet.microsoft.com/ru-RU/library/cc263199.aspx#search) and [Overview of search in SharePoint Server 2013](http://technet.microsoft.com/ru-RU/library/jj219738.aspx).</span></span>
  
    
    

### <a name="crawl-and-content-processing"></a><span data-ttu-id="d3370-125">Обход и обработка контента</span><span class="sxs-lookup"><span data-stu-id="d3370-125">Crawl and content processing</span></span>
<span data-ttu-id="d3370-126"><a name="bk_crawl"> </a></span><span class="sxs-lookup"><span data-stu-id="d3370-126"></span></span>

<span data-ttu-id="d3370-127">Архитектура обхода и обработки контента включает представленные ниже компоненты.</span><span class="sxs-lookup"><span data-stu-id="d3370-127">The crawl and content processing architecture consists of the following:</span></span>
  
    
    
 <span data-ttu-id="d3370-128">**Компонент обхода контента**</span><span class="sxs-lookup"><span data-stu-id="d3370-128">**Crawl component**</span></span>
  
    
    
 <span data-ttu-id="d3370-129">Выполняет обход контента, собирает свойства для обхода и метаданные из обойденных элементов и отправляет их в компонент обработки контента.</span><span class="sxs-lookup"><span data-stu-id="d3370-129">Crawls content sources to collect crawled properties and metadata from crawled items and sends this information to the content processing component.</span></span>
  
    
    
 <span data-ttu-id="d3370-130">**База данных обхода**</span><span class="sxs-lookup"><span data-stu-id="d3370-130">**Crawl database**</span></span>
  
    
    
<span data-ttu-id="d3370-131">Содержит информацию об обойденных элементах, например, последнее время обхода контента, идентификатор последнего обхода и тип обновления во время последнего обхода.</span><span class="sxs-lookup"><span data-stu-id="d3370-131">Contains information about crawled items, such as last crawl time, the last crawl ID, and the type of update during the last crawl.</span></span>
  
    
    
 <span data-ttu-id="d3370-132">**Компонент обработки контента**</span><span class="sxs-lookup"><span data-stu-id="d3370-132">**Content processing component**</span></span>
  
    
    
<span data-ttu-id="d3370-133">Обходит источники контента, чтобы собрать свойства для обхода и метаданные из обойденных компонентов, и отправляет эту информацию в компонент индексирования.</span><span class="sxs-lookup"><span data-stu-id="d3370-133">Crawls content sources to collect crawled properties and metadata from crawled items and sends this information to the index component.</span></span>
  
    
    

### <a name="index"></a><span data-ttu-id="d3370-134">Указатель</span><span class="sxs-lookup"><span data-stu-id="d3370-134">Index</span></span>
<span data-ttu-id="d3370-135"><a name="bk_index"> </a></span><span class="sxs-lookup"><span data-stu-id="d3370-135"></span></span>

<span data-ttu-id="d3370-p104">Компонент индексирования получает от компонента обработки контента обработанные элементы и записывает их в индекс поиска. Кроме того, этот компонент обрабатывает входящие запросы, получает информацию от поисковых индексов и отправляет набор результатов обратно компоненту обработки контента.</span><span class="sxs-lookup"><span data-stu-id="d3370-p104">The index component receives the processed items from the content processing component and writes them to the search index. This component also handles incoming queries, retrieves information from the search index, and sends back the result set to the query processing component.</span></span>
  
    
    

### <a name="query-processing"></a><span data-ttu-id="d3370-138">Обработка запросов</span><span class="sxs-lookup"><span data-stu-id="d3370-138">Query processing</span></span>
<span data-ttu-id="d3370-139"><a name="bk_query"> </a></span><span class="sxs-lookup"><span data-stu-id="d3370-139"></span></span>

<span data-ttu-id="d3370-p105">Компонент обработки запросов анализирует и обрабатывает поисковые запросы и результаты. Затем обработанный запрос отправляется в компонент индексирования, который возвращает набор результатов поиска для данного запроса.</span><span class="sxs-lookup"><span data-stu-id="d3370-p105">The query processing component analyzes and processes search queries and results. The processed query is then submitted to the index component, which returns a set of search results for the query.</span></span>
  
    
    

### <a name="search-administration"></a><span data-ttu-id="d3370-142">Администрирование поиска</span><span class="sxs-lookup"><span data-stu-id="d3370-142">Search administration</span></span>
<span data-ttu-id="d3370-143"><a name="bk_searchadmin"> </a></span><span class="sxs-lookup"><span data-stu-id="d3370-143"></span></span>

<span data-ttu-id="d3370-144">Администрирование поиска состоит из компонента администрирования поиска и соответствующей базы данных.</span><span class="sxs-lookup"><span data-stu-id="d3370-144">Search administration is composed of the search administration component and its corresponding database.</span></span>
  
    
    
 <span data-ttu-id="d3370-145">**Компонент администрирования поиска**</span><span class="sxs-lookup"><span data-stu-id="d3370-145">**Search administration component**</span></span>
  
    
    
<span data-ttu-id="d3370-146">Запускает системные процессы поиска, а также добавляет и инициализирует новые экземпляры компонентов поиска.</span><span class="sxs-lookup"><span data-stu-id="d3370-146">Runs the system processes for search, and adds and initializes new instances of search components.</span></span>
  
    
    
 <span data-ttu-id="d3370-147">**База данных администрирования поиска**</span><span class="sxs-lookup"><span data-stu-id="d3370-147">**Search administration database**</span></span>
  
    
    
<span data-ttu-id="d3370-148">Сохраняет данные конфигурации поиска.</span><span class="sxs-lookup"><span data-stu-id="d3370-148">Stores search configuration data.</span></span>
  
    
    

### <a name="analytics"></a><span data-ttu-id="d3370-149">Аналитика</span><span class="sxs-lookup"><span data-stu-id="d3370-149">Analytics</span></span>
<span data-ttu-id="d3370-150"><a name="bk_analytics"> </a></span><span class="sxs-lookup"><span data-stu-id="d3370-150"></span></span>

<span data-ttu-id="d3370-151">Структура аналитики состоит из компонента обработки аналитики, базы данных отчетности аналитики и базу данных ссылок.</span><span class="sxs-lookup"><span data-stu-id="d3370-151">The analytics architecture consists of the analytics processing component, analytics reporting database, and link database.</span></span>
  
    
    
 <span data-ttu-id="d3370-152">**Компонент обработки аналитики**</span><span class="sxs-lookup"><span data-stu-id="d3370-152">**Analytics processing component**</span></span>
  
    
    
<span data-ttu-id="d3370-153">Выполняет анализ поиска и использования.</span><span class="sxs-lookup"><span data-stu-id="d3370-153">Performs search analytics and usage analytics.</span></span>
  
    
    
 <span data-ttu-id="d3370-154">**База данных ссылок**</span><span class="sxs-lookup"><span data-stu-id="d3370-154">**Link database**</span></span>
  
    
    
<span data-ttu-id="d3370-155">Хранит информацию, извлеченную компонентом обработки контента, и информацию по поисковым переходам.</span><span class="sxs-lookup"><span data-stu-id="d3370-155">Stores information extracted by the content processing component and search click information.</span></span>
  
    
    
 <span data-ttu-id="d3370-156">**База данных отчетности аналитики**</span><span class="sxs-lookup"><span data-stu-id="d3370-156">**Analytics reporting database**</span></span>
  
    
    
<span data-ttu-id="d3370-157">Хранит результаты использования аналитики.</span><span class="sxs-lookup"><span data-stu-id="d3370-157">Stores the results of usage analytics.</span></span>
  
    
    
 <span data-ttu-id="d3370-158">**Хранилище событий**</span><span class="sxs-lookup"><span data-stu-id="d3370-158">**Event store**</span></span>
  
    
    
<span data-ttu-id="d3370-159">Хранит события использования, которые захвачены на внешнем интерфейсе.</span><span class="sxs-lookup"><span data-stu-id="d3370-159">Stores usage events that are captured on the front-end.</span></span>
  
    
    

## <a name="search-extensibility-points"></a><span data-ttu-id="d3370-160">Точки расширения поиска</span><span class="sxs-lookup"><span data-stu-id="d3370-160">Search extensibility points</span></span>

<span data-ttu-id="d3370-p106">Архитектура Поиск в SharePoint предоставляет несколько точек расширения для поддержки сценариев настройки. В этом разделе описаны эти точки и показано, где можно найти дополнительную информацию о разработке для этих сценариев.</span><span class="sxs-lookup"><span data-stu-id="d3370-p106">The Search in SharePoint architecture provides several extensibility points to support customization scenarios. In this section, we'll describe these points and show you where you can find more information about developing for these scenarios.</span></span>
  
    
    

### <a name="connector-framework"></a><span data-ttu-id="d3370-163">Инфраструктура компонентов</span><span class="sxs-lookup"><span data-stu-id="d3370-163">Connector framework</span></span>

<span data-ttu-id="d3370-p107">Компонент обхода обходит контент, вызывая соединителей или обработчиков протоколов, которые взаимодействуют с источниками контента, чтобы получить данные. Поиск в SharePoint включает инфраструктуру компонентов, которую можно использовать для настройки и создания соединителей для обхода новых источников контента. Более подробную информацию об архитектуре инфраструктуры компонентов и способах ее расширения можно узнать в статье  [Инфраструктура соединителей поиска в SharePoint](search-connector-framework-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="d3370-p107">The crawl component crawls content by invoking connectors or protocol handlers that interact with content sources to retrieve data. Search in SharePoint includes a connector framework that you can use to customize and build connectors to crawl new content sources. For detailed information about the connector framework architecture and how to extend it, see  [Search connector framework in SharePoint](search-connector-framework-in-sharepoint.md).</span></span>
  
    
    

### <a name="custom-content-processing"></a><span data-ttu-id="d3370-167">Настройка обработки контента</span><span class="sxs-lookup"><span data-stu-id="d3370-167">Custom content processing</span></span>

<span data-ttu-id="d3370-p108">В компоненте обработки контента вы можете использовать выноски веб-службы обогащения контента, чтобы изменить управляемые свойства обходимых элементов перед тем, как они будут добавлены в индекс поиска. Эта выноска веб-службы обращается к любой созданной вами внешней веб-службе обогащения содержимого. Более подробную информацию можно узнать в статье  [Нестандартная обработка контента с использованием выноски веб-службы "Обогащение контента"](custom-content-processing-with-the-content-enrichment-web-service-callout.md). С пошаговой реализацией веб-службы обогащения контента можно ознакомиться в статье  [Как: используйте вызов повышения качества контента веб-службы для SharePoint Server](how-to-use-the-content-enrichment-web-service-callout-for-sharepoint-server.md). Также полезна будет запись блога  [Настройка поиска SharePoint с помощью веб-службы обогащения содержимого](http://blogs.msdn.com/b/sharepointdev/archive/2012/11/13/customize-the-sharepoint-search-experience-with-a-content-enrichment-web-service.aspx).</span><span class="sxs-lookup"><span data-stu-id="d3370-p108">Within the content processing component, you can use the Content Enrichment web service callout to modify the managed properties of crawled items before they are added to the search index. This web service callout calls out to any external content enrichment web service that you create. For more information, see  [Custom content processing with the Content Enrichment web service callout](custom-content-processing-with-the-content-enrichment-web-service-callout.md). For a step-by-step implementation of a content enrichment web service, see  [How to: Use the Content Enrichment web service callout for SharePoint Server](how-to-use-the-content-enrichment-web-service-callout-for-sharepoint-server.md). The blog post  [Customize the SharePoint search experience with a Content Enrichment web service](http://blogs.msdn.com/b/sharepointdev/archive/2012/11/13/customize-the-sharepoint-search-experience-with-a-content-enrichment-web-service.aspx) is also a good resource</span></span>
  
    
    

### <a name="query-apis"></a><span data-ttu-id="d3370-173">Интерфейсы API запроса</span><span class="sxs-lookup"><span data-stu-id="d3370-173">Query APIs</span></span>

<span data-ttu-id="d3370-174">Поиск в SharePoint предусматривает несколько интерфейсов API запроса, которые предоставляют множество способов доступа к результатам поиска, чтобы вы могли вернуть различные типы пользовательских решений.</span><span class="sxs-lookup"><span data-stu-id="d3370-174">Search in SharePoint provides several query APIs, giving you lots of ways to access search results, so that you can return search results in a variety of custom solution types.</span></span>
  
    
    
<span data-ttu-id="d3370-175">В таблице 1 показаны интерфейсы API, которые вы можете использовать для программирования Поиск в SharePoint, и их расположение.</span><span class="sxs-lookup"><span data-stu-id="d3370-175">Table 1 shows the APIs that you can use to program Search in SharePoint and where to find them.</span></span>
  
    
    

<span data-ttu-id="d3370-176">**Таблица 1. Поисковые интерфейсы API**</span><span class="sxs-lookup"><span data-stu-id="d3370-176">**Table 1. Search APIs**</span></span>


|<span data-ttu-id="d3370-177">**Имя API**</span><span class="sxs-lookup"><span data-stu-id="d3370-177">**API name**</span></span>|<span data-ttu-id="d3370-178">**Библиотека или схема классов и путь**</span><span class="sxs-lookup"><span data-stu-id="d3370-178">**Class library or schema and path**</span></span>|
|:-----|:-----|
|<span data-ttu-id="d3370-179">Клиентская объектная модель .NET (CSOM)</span><span class="sxs-lookup"><span data-stu-id="d3370-179">.NET client object model (CSOM)</span></span>  <br/> |<span data-ttu-id="d3370-180">Microsoft.SharePoint.Client.Search.dll</span><span class="sxs-lookup"><span data-stu-id="d3370-180">Microsoft.SharePoint.Client.Search.dll          %ProgramFiles%Common FilesMicrosoft Sharedweb server extensions15ISAPI</span></span> <br/><span data-ttu-id="d3370-181">%ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\ISAPI</span><span class="sxs-lookup"><span data-stu-id="d3370-181">Microsoft.SharePoint.Client.Search.dll          %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\ISAPI</span></span>  <br/> |
|<span data-ttu-id="d3370-182">Silverlight CSOM</span><span class="sxs-lookup"><span data-stu-id="d3370-182">Silverlight CSOM</span></span>  <br/> |<span data-ttu-id="d3370-183">Microsoft.SharePoint.Client.Search.Silverlight.dll</span><span class="sxs-lookup"><span data-stu-id="d3370-183">Microsoft.SharePoint.Client.Search.Silverlight.dll          %ProgramFiles%Common FilesMicrosoft Sharedweb server extensions15TEMPLATELAYOUTSClientBin</span></span> <br/><span data-ttu-id="d3370-184">%ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\TEMPLATE\\LAYOUTS\\ClientBin</span><span class="sxs-lookup"><span data-stu-id="d3370-184">Microsoft.SharePoint.Client.Search.Silverlight.dll          %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\TEMPLATE\\LAYOUTS\\ClientBin</span></span>  <br/> |
|<span data-ttu-id="d3370-185">JavaScript CSOM</span><span class="sxs-lookup"><span data-stu-id="d3370-185">JavaScript CSOM</span></span>  <br/> |<span data-ttu-id="d3370-186">SP.search.js</span><span class="sxs-lookup"><span data-stu-id="d3370-186">SP.search.js</span></span> <br/><span data-ttu-id="d3370-187">%ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\TEMPLATE\\LAYOUTS</span><span class="sxs-lookup"><span data-stu-id="d3370-187">SP.search.js          %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\TEMPLATE\\LAYOUTS</span></span>  <br/> |
|<span data-ttu-id="d3370-188">Конечные точки службы передачи репрезентативного состояния (REST)</span><span class="sxs-lookup"><span data-stu-id="d3370-188">Representational State Transfer (REST) service endpoints</span></span>  <br/> |<span data-ttu-id="d3370-189">http://server/_api/search/query</span><span class="sxs-lookup"><span data-stu-id="d3370-189">http://server/_api/search/query</span></span> <br/><span data-ttu-id="d3370-190">http://server/_api/search/suggest</span><span class="sxs-lookup"><span data-stu-id="d3370-190">http://server/_api/search/queryhttp://server/_api/search/suggest</span></span>  <br/> |
|<span data-ttu-id="d3370-191">Объектная модель сервера</span><span class="sxs-lookup"><span data-stu-id="d3370-191">Server object model</span></span>  <br/> |<span data-ttu-id="d3370-192">Microsoft.Office.Server.Search.dll</span><span class="sxs-lookup"><span data-stu-id="d3370-192">Microsoft.Office.Server.Search.dll</span></span> <br/><span data-ttu-id="d3370-193">%ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\ISAPI</span><span class="sxs-lookup"><span data-stu-id="d3370-193">Microsoft.Office.Server.Search.dll          %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\ISAPI</span></span>  <br/> |
   
<span data-ttu-id="d3370-194">Дополнительные сведения см. в статье [Использование API поисковых запросов в SharePoint](using-the-sharepoint-search-query-apis.md).</span><span class="sxs-lookup"><span data-stu-id="d3370-194">For more information, see  [Using the SharePoint search Query APIs](using-the-sharepoint-search-query-apis.md).</span></span>
  
    
    

### <a name="analytics"></a><span data-ttu-id="d3370-195">Аналитика</span><span class="sxs-lookup"><span data-stu-id="d3370-195">Analytics</span></span>

<span data-ttu-id="d3370-196">Для определения и обработки контента, который пользователи считают наиболее полезным и релевантным, компонент обработки аналитики анализирует как сам контент, так и способ взаимодействия с ним пользователей.</span><span class="sxs-lookup"><span data-stu-id="d3370-196">To help identify and surface the content that users consider to be the most useful and relevant, the analytics processing component analyzes both the content itself, and also the way that users interact with it.</span></span> <span data-ttu-id="d3370-197">Данный анализ выполняется согласно заданиям таймера, которые отвечают за выполнение анализа задач жизненного цикла, таких как запуск, остановка, приостановка и возобновление анализа при необходимости.</span><span class="sxs-lookup"><span data-stu-id="d3370-197">These analyses are done by timer jobs that are responsible for performing analysis lifecycle tasks such as starting, stopping, pausing, and resuming an analysis job when requested.</span></span> <span data-ttu-id="d3370-198">Этими заданиями таймера можно управлять через пространство имен [Microsoft.Office.Server.Search.Analytics](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Analytics.aspx).</span><span class="sxs-lookup"><span data-stu-id="d3370-198">You can manipulate these timer jobs through the  [Microsoft.Office.Server.Search.Analytics](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Analytics.aspx) namespace.</span></span> <span data-ttu-id="d3370-199">Подробные сведения об аналитике в SharePoint см. в статье [Обзор обработки аналитических данных в SharePoint](http://technet.microsoft.com/ru-RU/library/jj219554.aspx).</span><span class="sxs-lookup"><span data-stu-id="d3370-199">For in-depth information about analytics in SharePoint, see [Overview of analytics processing in SharePoint](http://technet.microsoft.com/ru-RU/library/jj219554.aspx).</span></span>
  
    
    

### <a name="custom-ranking-models"></a><span data-ttu-id="d3370-200">Специальные модели ранжирования</span><span class="sxs-lookup"><span data-stu-id="d3370-200">Custom ranking models</span></span>

<span data-ttu-id="d3370-201">Результаты поиска можно упорядочить разными способами, например по значению ранга.</span><span class="sxs-lookup"><span data-stu-id="d3370-201">Search results can be ordered in various ways, one of which is by rank score.</span></span> <span data-ttu-id="d3370-202">Значения ранга вычисляются поисковой системой с использованием моделей ранжирования.</span><span class="sxs-lookup"><span data-stu-id="d3370-202">Rank scores are calculated by the search engine using ranking models.</span></span> <span data-ttu-id="d3370-203">По умолчанию SharePoint предоставляет четырнадцать моделей ранжирования.</span><span class="sxs-lookup"><span data-stu-id="d3370-203">SharePoint provides fourteen ranking models by default.</span></span> <span data-ttu-id="d3370-204">Но если вас не устраивает то, как упорядочены результаты поиска, вы можете использовать специальные модели ранжирования.</span><span class="sxs-lookup"><span data-stu-id="d3370-204">However, if you are not satisfied with the way your search results are ordered, you can use a custom ranking model.</span></span> <span data-ttu-id="d3370-205">Дополнительные сведения о процессе создания специальной модели ранжирования и ее настройке см. в статье [Настройка моделей ранжирования для улучшения релевантности в SharePoint](customizing-ranking-models-to-improve-relevance-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="d3370-205">To learn more about the process of creating a custom ranking model and tuning it, see  [Customizing ranking models to improve relevance in SharePoint](customizing-ranking-models-to-improve-relevance-in-sharepoint.md).</span></span>
  
    
    

### <a name="custom-security-trimming"></a><span data-ttu-id="d3370-206">Специальная фильтрация по ролям безопасности</span><span class="sxs-lookup"><span data-stu-id="d3370-206">Custom security trimming</span></span>

<span data-ttu-id="d3370-207">При поиске в SharePoint выполняется фильтрация результатов поиска по ролям безопасности, которая основана на удостоверении пользователя, отправившего запрос, и времени запроса, при этом используются данные безопасности, полученные от компонента обхода контента.</span><span class="sxs-lookup"><span data-stu-id="d3370-207">Search in SharePoint Server 2013 performs security trimming of search results that are based on the identity of the user submitting the query, at query time, by using security information obtained from the crawl component. However, in some cases, you may need to implement custom security trimming. SharePoint Server 2013 provides two interfaces to accomplish this task:  ISecurityTrimmerPre and ISecurityTrimmerPost .</span></span> <span data-ttu-id="d3370-208">Однако в некоторых случаях вам может потребоваться реализовать специальную фильтрацию по ролям безопасности.</span><span class="sxs-lookup"><span data-stu-id="d3370-208">However, in some cases, you may need to implement custom security trimming.</span></span> <span data-ttu-id="d3370-209">Для выполнения этой задачи в SharePoint доступны два интерфейса: [ISecurityTrimmerPre](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPre.aspx) и [ISecurityTrimmerPost](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPost.aspx).</span><span class="sxs-lookup"><span data-stu-id="d3370-209">SharePoint provides two interfaces to accomplish this task:  [ISecurityTrimmerPre](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPre.aspx) and [ISecurityTrimmerPost](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPost.aspx) .</span></span>
  
    
    
<span data-ttu-id="d3370-210">Интерфейс предварительной фильтрации (**ISecurityTrimmerPre**) выполняет оценку до обработки запроса, при этом прежде чем поисковый запрос будет сопоставлен с индексом поиска, в него добавляются данные безопасности.</span><span class="sxs-lookup"><span data-stu-id="d3370-210">The **ISecurityTrimmerPre** interface carries out pre-trimming, or pre-query evaluation, where the search query is rewritten to add security information before the search query is matched to the search index. The ISecurityTrimmerPost interface carries out post-trimming, or post-query evaluation, where the search results are pruned before they are returned to the user.</span></span> <span data-ttu-id="d3370-211">Интерфейс последующей фильтрации (**ISecurityTrimmerPost**) выполняет оценку после обработки запроса, при которой некоторые результаты поиска убираются, после чего пользователю возвращаются остальные.</span><span class="sxs-lookup"><span data-stu-id="d3370-211">In contrast, the post-trimmer interface ( **ISecurityTrimmerPost**) carries out post-query evaluation, where the search results are pruned before they are returned to the user.</span></span> <span data-ttu-id="d3370-212">Дополнительные сведения об этих двух интерфейсах см. в статье [Специальная фильтрация по ролям безопасности, настраиваемая для поиска в SharePoint](custom-security-trimming-for-search-in-sharepoint-server.md).</span><span class="sxs-lookup"><span data-stu-id="d3370-212">For more information about the two interfaces, see  [Custom security trimming for Search in SharePoint](custom-security-trimming-for-search-in-sharepoint-server.md).</span></span> <span data-ttu-id="d3370-213">Пошаговые инструкции по реализации интерфейса триммера безопасности см. в статье [Применение специального триммера безопасности к результатам поиска SharePoint Server](how-to-use-a-custom-security-trimmer-for-sharepoint-server-search-results.md).</span><span class="sxs-lookup"><span data-stu-id="d3370-213">For step-by-step information on how to implement a security trimmer interface, see  [How to: Use a custom security trimmer for SharePoint Server search results](how-to-use-a-custom-security-trimmer-for-sharepoint-server-search-results.md).</span></span>
  
    
    

### <a name="content-search-web-part"></a><span data-ttu-id="d3370-214">Веб-часть "Поиск контента"</span><span class="sxs-lookup"><span data-stu-id="d3370-214">Content Search Web Part</span></span>

<span data-ttu-id="d3370-p113">Веб-часть поиска контента  это веб-часть, которая может отображать динамический контент, который ранее был обойден и добавлен в индекс поиска. Каждый экземпляр веб-части связан с индексом поиска и отображает результаты для данного конкретного запроса. Когда пользователи просматривают страницу, которая содержит веб-часть поиска контента, автоматически выдается поисковый запрос, и от индекса поиска возвращаются результаты поиска. Вы можете использовать веб-часть поиска контента когда угодно, чтобы отобразить контент, который заполняется автоматически созданными поисковыми запросами. В некоторых случаях вам может потребоваться расширить веб-часть поиска контента, которую можно изменить через пространство имен  [Microsoft.Office.Server.Search.WebControls](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.WebControls.aspx) как [ContentBySearchWebPart](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.WebControls.ContentBySearchWebPart.aspx) . Информацию о том, как расширить [ContentBySearchWebPart](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.WebControls.ContentBySearchWebPart.aspx) , чтобы веб-часть распознала пользовательские свойства, можно узнать в статье [Сегментация пользователей в SharePoint](user-segmentation-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="d3370-p113">The Content Search Web Part is a Web Part that can display dynamic content that was previously crawled and added to the search index. Each instance of the Web Part is associated with a search query and shows the results for that particular search query. When users browse to a page that contains a Content Search Web Part, a search query is automatically issued, and the corresponding search results are returned from the search index. You can use the Content Search Web Part whenever you want to display content that is populated by automatically generated search queries. In some cases, you may want to extend the Content Search Web Part, which is exposed through the  [Microsoft.Office.Server.Search.WebControls](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.WebControls.aspx) namespace as [ContentBySearchWebPart](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.WebControls.ContentBySearchWebPart.aspx) . To learn about how to extend the [ContentBySearchWebPart](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.WebControls.ContentBySearchWebPart.aspx) so that the Web Part understands custom properties, see [User segmentation in SharePoint](user-segmentation-in-sharepoint.md).</span></span>
  
    
    

### <a name="search-driven-mobile-apps-using-the-navigation-and-event-logging-rest-interfaces"></a><span data-ttu-id="d3370-221">Мобильные приложения, ориентированные на поиск, для которых используются интерфейсы REST, обеспечивающие навигацию и ведение журнала событий</span><span class="sxs-lookup"><span data-stu-id="d3370-221">Search-driven mobile apps using the Navigation and Event Logging REST interfaces</span></span>

<span data-ttu-id="d3370-222">В SharePoint доступны два новых интерфейса REST — интерфейсы навигации и ведения журнала событий.</span><span class="sxs-lookup"><span data-stu-id="d3370-222">SharePoint provides two new REST interfaces: Navigation and Event Logging.</span></span> <span data-ttu-id="d3370-223">Вы можете использовать их для создания мобильных приложений, ориентированных на поиск, для мобильных устройств, например телефонов и планшетов, работающих под управлением операционной системы, отличной от Windows.</span><span class="sxs-lookup"><span data-stu-id="d3370-223">You can use them to create search-driven mobile apps for mobile devices, such as phones and tablets, that run on operating systems other than Windows.</span></span> <span data-ttu-id="d3370-224">Эта функция позволяет отображать на мобильном устройстве каталог продукции не через мобильный канал, а другим способом.</span><span class="sxs-lookup"><span data-stu-id="d3370-224">This feature lets you display the product catalog on a mobile device in an alternate way, instead of using a mobile channel.</span></span> <span data-ttu-id="d3370-225">Подробный пример создания такого приложения описан в статье [Создание мобильных приложений, ориентированных на поиск, для которых используются интерфейсы REST, обеспечивающие навигацию и ведение журнала событий](how-to-build-search-driven-mobile-apps-with-the-navigation-and-event-logging-res.md).</span><span class="sxs-lookup"><span data-stu-id="d3370-225">See  [How to: Build search-driven mobile apps with the Navigation and Event Logging REST interfaces](how-to-build-search-driven-mobile-apps-with-the-navigation-and-event-logging-res.md) for a detailed example of how to create such an app.</span></span>
  
    
    

## <a name="in-this-section"></a><span data-ttu-id="d3370-226">В этой статье</span><span class="sxs-lookup"><span data-stu-id="d3370-226">In this section</span></span>


-  [<span data-ttu-id="d3370-227">Новые возможности поиска в SharePoint для разработчиков (en)</span><span class="sxs-lookup"><span data-stu-id="d3370-227">What's new in SharePoint search for developers</span></span>](what-s-new-in-sharepoint-search-for-developers.md)
    
  
-  [<span data-ttu-id="d3370-228">Поиск по новому контенту с поиска SharePoint</span><span class="sxs-lookup"><span data-stu-id="d3370-228">Searching new content with SharePoint Search</span></span>](searching-new-content-with-sharepoint-search.md)
    
  
-  [<span data-ttu-id="d3370-229">Настройка службы поиска в SharePoint</span><span class="sxs-lookup"><span data-stu-id="d3370-229">Configure search in SharePoint</span></span>](configure-search-in-sharepoint.md)
    
  
-  [<span data-ttu-id="d3370-230">Построение запросов поиска в SharePoint</span><span class="sxs-lookup"><span data-stu-id="d3370-230">Building search queries in SharePoint</span></span>](building-search-queries-in-sharepoint.md)
    
  
-  [<span data-ttu-id="d3370-231">Общие сведения об API службы поиска REST для SharePoint</span><span class="sxs-lookup"><span data-stu-id="d3370-231">SharePoint Search REST API overview</span></span>](sharepoint-search-rest-api-overview.md)
    
  
-  [<span data-ttu-id="d3370-232">Настройка результатов поиска в SharePoint</span><span class="sxs-lookup"><span data-stu-id="d3370-232">Customizing search results in SharePoint</span></span>](customizing-search-results-in-sharepoint.md)
    
  
-  [<span data-ttu-id="d3370-233">Сортировка результатов поиска в SharePoint</span><span class="sxs-lookup"><span data-stu-id="d3370-233">Sorting search results in SharePoint</span></span>](sorting-search-results-in-sharepoint.md)
    
  
-  [<span data-ttu-id="d3370-234">Настройка моделей ранжирования для улучшения релевантности в SharePoint</span><span class="sxs-lookup"><span data-stu-id="d3370-234">Customizing ranking models to improve relevance in SharePoint</span></span>](customizing-ranking-models-to-improve-relevance-in-sharepoint.md)
    
  
-  [<span data-ttu-id="d3370-235">Специальная фильтрация по ролям безопасности, настраиваемая для поиска в SharePoint</span><span class="sxs-lookup"><span data-stu-id="d3370-235">Custom security trimming for Search in SharePoint Server 2013</span></span>](custom-security-trimming-for-search-in-sharepoint-server.md)
    
  
-  [<span data-ttu-id="d3370-236">Экспорт и импорт параметров конфигурации поиска в SharePoint</span><span class="sxs-lookup"><span data-stu-id="d3370-236">Exporting and importing search configuration settings in SharePoint</span></span>](exporting-and-importing-search-configuration-settings-in-sharepoint.md)
    
  

## <a name="additional-resources"></a><span data-ttu-id="d3370-237">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="d3370-237">Additional resources</span></span>


-  [<span data-ttu-id="d3370-238">Отличия SharePoint 2010 от SharePoint</span><span class="sxs-lookup"><span data-stu-id="d3370-238">Changes from SharePoint 2010 to SharePoint</span></span>](http://technet.microsoft.com/ru-RU/library/ff607742.aspx)
    
  
-  [<span data-ttu-id="d3370-239">Технические графики, раздел "Поиск"</span><span class="sxs-lookup"><span data-stu-id="d3370-239">Technical Diagrams -- Search</span></span>](http://technet.microsoft.com/ru-RU/library/cc263199.aspx#search)
    
  
-  [<span data-ttu-id="d3370-240">Добавление возможностей SharePoint</span><span class="sxs-lookup"><span data-stu-id="d3370-240">Add SharePoint capabilities</span></span>](add-sharepoint-capabilities.md)
    
  
