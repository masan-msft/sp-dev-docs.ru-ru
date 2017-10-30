---
title: "Инфраструктура соединителей поиска в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 38560a3b-69c6-4a56-97ca-3625bbd5755e
ms.openlocfilehash: 74f2b263b3225e2093920eccfcbefc80759b1f0d
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="search-connector-framework-in-sharepoint"></a><span data-ttu-id="58775-102">Инфраструктура соединителей поиска в SharePoint</span><span class="sxs-lookup"><span data-stu-id="58775-102">Search connector framework in SharePoint</span></span>
<span data-ttu-id="58775-103">Сведения о SharePoint индексирования соединители, инфраструктурой соединителя и о способах создания настраиваемых BCS соединители индексации для поиска во внешних системах.</span><span class="sxs-lookup"><span data-stu-id="58775-103">Learn about the SharePoint indexing connectors, the connector framework, and how you can create custom BCS indexing connectors to search external systems.</span></span>
## <a name="making-content-available-for-search-in-sharepoint"></a><span data-ttu-id="58775-104">Создание контента, доступного для поиска в SharePoint</span><span class="sxs-lookup"><span data-stu-id="58775-104">Making content available for search in SharePoint</span></span>
<span data-ttu-id="58775-105"><a name="SP15searchconnect_make"> </a></span><span class="sxs-lookup"><span data-stu-id="58775-105"></span></span>

<span data-ttu-id="58775-106">Поиска в SharePoint предоставляет два подхода для обработки запросов для возвращения результатов поиска — федеративного поиска и обхода контента.</span><span class="sxs-lookup"><span data-stu-id="58775-106">Search in SharePoint provides two approaches for processing queries to return search results—federated search and content crawling.</span></span>
  
    
    
 <span data-ttu-id="58775-p101">**Федеративном поиске** В этом подходе результаты поиска возвращаются для контента, обход которого не выполнен с сервера поиска. Запрос перенаправляется к внешнему репозиторию контента, где он обрабатывается поисковой системы, репозитория. Поисковый механизм репозитория затем возвращает результаты на поисковый сервер. Сервер поиска форматирует и отображает результаты из внешнего хранилища для отображения на странице результатов поиска. Такой подход имеет следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="58775-p101">**Federated search** In this approach, search results are returned for content that is not crawled by your search server. The query is forwarded to an external content repository where it is processed by that repository's search engine. The repository's search engine then returns the results to the search server. The search server formats and renders the results from the external repository to display on the search results page. This approach offers the following advantages:</span></span>
  
    
    

- <span data-ttu-id="58775-112">Нет дополнительных мощностей требуется для индекса контента, поскольку не выполняется обход контента для поиска в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="58775-112">You require no additional capacity requirements for the content index, because content is not crawled by Search in SharePoint.</span></span>
    
  
- <span data-ttu-id="58775-p102">Вы можете воспользоваться преимуществами существующих поисковый механизм репозитория. Например можно создать федерацию для поиска в Интернете для поиска в Интернете.</span><span class="sxs-lookup"><span data-stu-id="58775-p102">You can take advantage of a repository's existing search engine. For example, you can federate to an Internet search engine to search the web.</span></span>
    
  
- <span data-ttu-id="58775-115">Можно оптимизировать поисковую систему репозитория контента специально для хранящегося в нем набора контента, что позволит значительно повысить производительность этого набора.</span><span class="sxs-lookup"><span data-stu-id="58775-115">You can optimize the content repository's search engine for the repository's specific set of content, which might provide better search performance on the content set.</span></span>
    
  
- <span data-ttu-id="58775-116">Можно получить доступ к репозиториям, которые защищены от обхода контента, но может осуществляться поисковых запросов.</span><span class="sxs-lookup"><span data-stu-id="58775-116">You can access repositories that are secured against crawls, but that can be accessed by search queries.</span></span>
    
  
 <span data-ttu-id="58775-p103">**Обход контента** В этот подход результаты возвращаются из индекса контента приложения службы поиска по запросу пользователя. Индекс контента содержит контент, для которого выполняется обход приложением-службой поиска и включает в себя текстовое содержимое и метаданные для каждого элемента контента. Такой подход позволяет:</span><span class="sxs-lookup"><span data-stu-id="58775-p103">**Content crawling** In this approach, results are returned from the Search service application's content index based on the user's query. The content index contains content that is crawled by the Search service application, and includes text content and metadata for each content item. This approach enables you to:</span></span>
  
    
    

- <span data-ttu-id="58775-120">Сортировка результатов по релевантности.</span><span class="sxs-lookup"><span data-stu-id="58775-120">Sort results by relevance.</span></span>
    
  
- <span data-ttu-id="58775-121">Управление частотой обновления индекса контента.</span><span class="sxs-lookup"><span data-stu-id="58775-121">Control how frequently the content index is updated.</span></span>
    
  
- <span data-ttu-id="58775-122">Определение метаданных для обхода.</span><span class="sxs-lookup"><span data-stu-id="58775-122">Specify what metadata is crawled.</span></span>
    
  
- <span data-ttu-id="58775-123">Выполнение одной операции резервного копирования для контента, для которого выполнен обход.</span><span class="sxs-lookup"><span data-stu-id="58775-123">Perform a single backup operation for crawled content.</span></span>
    
  

## <a name="crawling-content-with-indexing-connectors-in-sharepoint"></a><span data-ttu-id="58775-124">Обход контента с помощью индексации соединителей в SharePoint</span><span class="sxs-lookup"><span data-stu-id="58775-124">Crawling content with indexing connectors in SharePoint</span></span>
<span data-ttu-id="58775-125"><a name="ConnectorFramework_SPIndexingConnectors"> </a></span><span class="sxs-lookup"><span data-stu-id="58775-125"></span></span>

<span data-ttu-id="58775-p104">Программа-обходчик использует соединители индексации для доступа к контенту для обхода. Соединитель indexing connector  компонент, который знает о подключении к источнику контента, что для обхода и как его обход. В более ранних версиях SharePoint эти были известны как обработчиков протоколов и компонентов, которые основаны на выполнение неуправляемого кода C++ пользовательских интерфейсов.</span><span class="sxs-lookup"><span data-stu-id="58775-p104">The crawler uses indexing connectors to access the content to crawl. The indexing connector is the component that knows how to connect to the content source, what to crawl, and how to crawl it. In earlier versions of SharePoint, these were known as protocol handlers, components that are based on custom interfaces running unmanaged C++ code.</span></span> 
  
    
    
<span data-ttu-id="58775-129">Поиск в SharePoint включает connector framework, введенные в SharePoint Server 2010 и построен на Microsoft Business Connectivity Services (BCS), который предоставляет простой подход к разработке соединители индексации.</span><span class="sxs-lookup"><span data-stu-id="58775-129">Search in SharePoint includes a connector framework, introduced in SharePoint Server 2010 and built on Microsoft Business Connectivity Services (BCS), which provides a simpler approach to developing indexing connectors.</span></span> <span data-ttu-id="58775-130">С инфраструктурой соединителя программа-обходчик использует соединители индексации на основании BCS для обхода внешнего контента.</span><span class="sxs-lookup"><span data-stu-id="58775-130">With the connector framework, the crawler uses indexing connectors based on BCS to crawl external content.</span></span> <span data-ttu-id="58775-131">SharePoint использует соединители индексации на основе обработчик протокола и соединители индексации BCS для обхода контента.</span><span class="sxs-lookup"><span data-stu-id="58775-131">SharePoint uses both protocol handler-based indexing connectors and BCS indexing connectors to crawl content.</span></span>
  
    
    
<span data-ttu-id="58775-132">На рисунке 1 содержит общий обзор История соединителя индексации SharePoint.</span><span class="sxs-lookup"><span data-stu-id="58775-132">Figure 1 provides a high-level overview of the SharePoint indexing connector story.</span></span>
  
    
    

  
    
    
![Соединители индексации SharePoint](../images/SP15Con_CF_IndexingConnectors.jpg)
  
    
    

  
    
    

  
    
    

## <a name="bcs-overview-for-search-in-sharepoint"></a><span data-ttu-id="58775-134">Обзор службы BCS для поиска в SharePoint</span><span class="sxs-lookup"><span data-stu-id="58775-134">BCS overview for Search in SharePoint</span></span>
<span data-ttu-id="58775-135"><a name="ConnectorFramework_BCSOverview"> </a></span><span class="sxs-lookup"><span data-stu-id="58775-135"></span></span>

<span data-ttu-id="58775-p106">BCS является защиту средства и инфраструктуру, которая необходима для подключения к внешним системам с SharePoint. На рисунке 2 показано высокоуровневое представление архитектуры BCS с соответствующих областей поиска с выделением.</span><span class="sxs-lookup"><span data-stu-id="58775-p106">BCS is the umbrella of tools and infrastructure that enables you to connect to external systems from SharePoint. Figure 2 shows a high-level view of the BCS architecture, with the relevant areas for Search highlighted.</span></span>
  
    
    

  
    
    

<span data-ttu-id="58775-138">**На рисунке 2. Архитектура BCS, включая поиск**</span><span class="sxs-lookup"><span data-stu-id="58775-138">**Figure 2. BCS architecture including Search**</span></span>

  
    
    

  
    
    
![Архитектура BCS](../images/SP15Con_CF_BCS_Overview.jpg)
  
    
    

  
    
    
<span data-ttu-id="58775-p107">BCS устанавливает подключение к внешним данным, на основе определения внешнего типа контента в хранилище метаданных. Хранилище метаданных содержит следующие сведения для внешнего типа контента:</span><span class="sxs-lookup"><span data-stu-id="58775-p107">BCS makes the connection to the external data based on the external content type definition in the metadata store. The metadata store contains the following information for an external content type:</span></span>
  
    
    

- <span data-ttu-id="58775-142">**Сведения о подключении** Описывается, как подключиться к внешней системе.</span><span class="sxs-lookup"><span data-stu-id="58775-142">**Connectivity information** Describes how to connect to the external system.</span></span>
    
  
- <span data-ttu-id="58775-143">**Сведения о сущности** Описывает структуру внешних данных.</span><span class="sxs-lookup"><span data-stu-id="58775-143">**Entity information** Describes the structure of the external data.</span></span>
    
  
- <span data-ttu-id="58775-p108">**Операции** Описываются методы, используемые для доступа к внешним данным. В случае баз данных и веб-служб, это, методы, поддерживаемые внешней системы: инструкции SQL для базы данных соединители и веб-методы для веб-служб. Для .NET и настраиваемые соединители индексации BCS это методов, реализованных в сборке соединителя, компонентом библиотеки DLL, создайте для соединителя индексации.</span><span class="sxs-lookup"><span data-stu-id="58775-p108">**Operations** Describes methods used to access the external data. In the case of databases and web services, these are methods supported by the external system: SQL statements for database connectors and web methods for web services. For .NET and custom BCS indexing connectors, these are methods that are implemented in the connector assembly, which is the component DLL you create for the indexing connector.</span></span>
    
  
<span data-ttu-id="58775-p109">Эти сведения указана в файле модели BDC внешнего типа контента. Дополнительные сведения о модели BDC и их содержимое можно  [Инфраструктуры модели BDC](http://msdn.microsoft.com/library/2818ebdd-6cda-4d8f-82b2-7fde9fbf2633%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="58775-p109">This information is specified in the external content type's BDC model file. For more information about BDC models and what they contain, see  [BDC Model Infrastructure](http://msdn.microsoft.com/library/2818ebdd-6cda-4d8f-82b2-7fde9fbf2633%28Office.15%29.aspx).</span></span>
  
    
    
<span data-ttu-id="58775-149">Для получения дополнительных сведений об архитектуре BCS и функциональные возможности видеть  [Business Connectivity Services Overview](http://msdn.microsoft.com/library/91dd7b01-ead2-4f87-804b-b59ef2245c87%28Office.15%29.aspx) и [Механизм из с помощью Business Connectivity Services](http://msdn.microsoft.com/library/ff3e312b-0fbc-48ed-a752-76c50d286533%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="58775-149">For details about BCS architecture and functionality, see  [Business Connectivity Services Overview](http://msdn.microsoft.com/library/91dd7b01-ead2-4f87-804b-b59ef2245c87%28Office.15%29.aspx) and [Mechanics of Using Business Connectivity Services](http://msdn.microsoft.com/library/ff3e312b-0fbc-48ed-a752-76c50d286533%28Office.15%29.aspx).</span></span>
  
    
    

### <a name="using-the-connector-framework"></a><span data-ttu-id="58775-150">С помощью инфраструктурой соединителя</span><span class="sxs-lookup"><span data-stu-id="58775-150">Using the connector framework</span></span>

<span data-ttu-id="58775-p110">Для обхода внешних данных, необходимо добавить один из типов источников контента, которые поддерживают подключение к внешним данным. В таблице 1 перечислены этих типов источников контента.</span><span class="sxs-lookup"><span data-stu-id="58775-p110">To crawl external data, you have to add one of the content source types that support connecting to external data. Table 1 lists these content source types.</span></span>
  
    
    

<span data-ttu-id="58775-153">**В таблице 1. Типов источников контента, которые поддерживают индексирования соединители BCS**</span><span class="sxs-lookup"><span data-stu-id="58775-153">**Table 1. Content source types that support BCS indexing connectors**</span></span>


|<span data-ttu-id="58775-154">**Тип источника содержимого**</span><span class="sxs-lookup"><span data-stu-id="58775-154">**Content source type**</span></span>|<span data-ttu-id="58775-155">**Описание**</span><span class="sxs-lookup"><span data-stu-id="58775-155">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="58775-156">Бизнес-данные</span><span class="sxs-lookup"><span data-stu-id="58775-156">Line of Business Data</span></span>  <br/> |<span data-ttu-id="58775-157">Использование этого источника контента для базы данных и веб-соединители индексации службы BCS.</span><span class="sxs-lookup"><span data-stu-id="58775-157">Use this content source for database and web service BCS indexing connectors.</span></span>  <br/> |
|<span data-ttu-id="58775-158">Настраиваемый репозиторий</span><span class="sxs-lookup"><span data-stu-id="58775-158">Custom Repository</span></span>  <br/> |<span data-ttu-id="58775-159">Использование этого источника контента для .NET и настраиваемые соединители индексации BCS.</span><span class="sxs-lookup"><span data-stu-id="58775-159">Use this content source for .NET and custom BCS indexing connectors.</span></span>  <br/> |
   
<span data-ttu-id="58775-p111">Платформа соединителей позволяет создавать BCS индексирования соединителей для подключения к внешнего контента, который следует выполнить обход и включить в индекс контента. Соединитель индексации BCS используется программой-обходчиком для взаимодействия с внешнего источника данных. Во время обхода контента программа-обходчик вызывает соединителя индексации BCS для извлечения данных из внешней системы и передать его программы-обходчика. Соединитель индексации BCS также анализирует доступа поняты URL-адреса, поиска и идентификаторы, понятны BCS при их передаче между BCS и поиска во время обхода контента.</span><span class="sxs-lookup"><span data-stu-id="58775-p111">The connector framework enables you to create BCS indexing connectors to connect to external content that you want to crawl and include in the content index. The BCS indexing connector is used by the crawler to communicate with the external data source. At crawl time, the crawler calls the BCS indexing connector to fetch the data from the external system and pass it back to the crawler. The BCS indexing connector also parses the access URLs understood by Search and the identifiers understood by BCS as they are passed between BCS and Search during the crawl process.</span></span>
  
    
    
<span data-ttu-id="58775-164">Соединители индексации BCS состоят из следующих:</span><span class="sxs-lookup"><span data-stu-id="58775-164">BCS indexing connectors are composed of the following:</span></span>
  
    
    


  
    
    
> <span data-ttu-id="58775-165">**Файл модели BDC** Файл, который содержит структуру данных и, который предоставляет данные для подключения к внешней системе.</span><span class="sxs-lookup"><span data-stu-id="58775-165">**The BDC model file** The file that provides the structure of the data, and that provides connection information to the external system.</span></span>
    
  

  
    
    
> <span data-ttu-id="58775-166">**Соединитель** Компонент, содержащий код, который подключается к внешней системе и анализ доступа идентификаторы URL-адреса и BCS.</span><span class="sxs-lookup"><span data-stu-id="58775-166">**The connector** The component containing the code that connects to the external system and parses the access URLs and BCS identifiers.</span></span>
    
  
<span data-ttu-id="58775-167">Для BCS индексирования соединители на основе типов контента источника строки бизнес-данных поиска включает встроенные соединители, необходимо создать только файл модели BDC.</span><span class="sxs-lookup"><span data-stu-id="58775-167">For BCS indexing connectors based on the Line of Business Data content source types, Search includes built-in connectors, so you have to create only a BDC model file.</span></span> 
  
    
    
<span data-ttu-id="58775-168">Для соединителей индексации BCS на основе типов настраиваемый репозиторий источника контента необходимо разработать настраиваемый компонент в дополнение к файлу модели BDC для подключения к внешним данным.</span><span class="sxs-lookup"><span data-stu-id="58775-168">For BCS indexing connectors based on the Custom Repository content source types, you must develop a custom component in addition to a BDC model file to connect to the external data.</span></span>
  
    
    
<span data-ttu-id="58775-169">На рисунке 3 показана высокоуровневая архитектура структуры соединителя поиска.</span><span class="sxs-lookup"><span data-stu-id="58775-169">Figure 3 shows a high-level view of the search connector framework architecture.</span></span>
  
    
    

<span data-ttu-id="58775-170">**На рисунке 3. Базовая архитектура соединителя поиска**</span><span class="sxs-lookup"><span data-stu-id="58775-170">**Figure 3. Search connector framework architecture**</span></span>

  
    
    

  
    
    
![Архитектура структуры соединителя поиска](../images/SP15Con_CF_ConnFrwkArch.jpg)
  
    
    

  
    
    

  
    
    

### <a name="bcs-indexing-connectors"></a><span data-ttu-id="58775-172">Соединители индексации BCS</span><span class="sxs-lookup"><span data-stu-id="58775-172">BCS indexing connectors</span></span>
<span data-ttu-id="58775-173"><a name="ConnectorFramework_BCSIndexingConnectors"> </a></span><span class="sxs-lookup"><span data-stu-id="58775-173"></span></span>

<span data-ttu-id="58775-174">SharePoint поддерживает следующие типы BCS соединители индексирования:</span><span class="sxs-lookup"><span data-stu-id="58775-174">SharePoint supports the following types of BCS indexing connectors:</span></span>
  
    
    

- <span data-ttu-id="58775-175">**Подключения к базе данных** SharePoint включает в себя предварительно определенные соединитель BCS, который поддерживает подключение к базам данных, чтобы вы могли создать соединителя индексации BCS базы данных без написания кода — только что создание файла модели BDC для соединителя.</span><span class="sxs-lookup"><span data-stu-id="58775-175">**Database connector** SharePoint includes a predefined BCS connector that supports connecting to databases, so you can create a database BCS indexing connector without writing any code—just create the BDC model file for the connector.</span></span>
    
  
- <span data-ttu-id="58775-176">**Соединитель WCF (веб-служб)** SharePoint включает в себя предварительно определенные соединитель BCS, который поддерживает подключение к веб-служб, чтобы вы могли создать соединитель веб-службы BCS индексирования без написания кода — только что создание файла модели BDC для соединителя.</span><span class="sxs-lookup"><span data-stu-id="58775-176">**WCF (web services) connector** SharePoint includes a predefined BCS connector that supports connecting to web services, so you can create a web service BCS indexing connector without writing any code—just create the BDC model file for the connector.</span></span>
    
    > <span data-ttu-id="58775-177">**Примечание:** Несмотря на то, что у вас нет писать код для создания соединителя для веб-служб, веб-службы необходимо включить методы, которые предоставляют те же функциональные возможности, который предоставляет соединитель .NET BCS для передачи внешних бизнес-данных BCS.</span><span class="sxs-lookup"><span data-stu-id="58775-177">**Note:** Although you don't have to write code to create a connector for web services, the web service must include methods that provide the same functionality that the .NET BCS connector provides, to pass the external business data to BCS.</span></span> <span data-ttu-id="58775-178">Сведения о создании веб-службы можно [Создание сборки подключения .NET и веб-службы](http://msdn.microsoft.com/library/9a6c6712-868a-4a9c-9645-3aa448ad5092%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="58775-178">For information about creating a web service, see  [Creating .NET Connectivity Assemblies and Web Services](http://msdn.microsoft.com/library/9a6c6712-868a-4a9c-9645-3aa448ad5092%28Office.15%29.aspx).</span></span> <span data-ttu-id="58775-179">Примеры кода в разделе [Образец Orders ASP.NET Web Service Sample](http://msdn.microsoft.com/library/10e46860-788f-4ed0-a4d8-1e17ada58e83%28Office.15%29.aspx) и [Пример Orders WCF Service Sample](http://msdn.microsoft.com/library/535277c8-9d5c-41eb-ab23-0ae141d726c5%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="58775-179">For code examples, see  [Sample Orders ASP.NET Web Service Sample](http://msdn.microsoft.com/library/10e46860-788f-4ed0-a4d8-1e17ada58e83%28Office.15%29.aspx) and [Sample Orders WCF Service Sample](http://msdn.microsoft.com/library/535277c8-9d5c-41eb-ab23-0ae141d726c5%28Office.15%29.aspx).</span></span> 
- <span data-ttu-id="58775-180">**Соединитель .NET BCS** SharePoint не включают предварительно заданных соединителя BCS для соединителей .NET, поэтому в дополнение к созданию BDC модели файла, необходимо также создать компонент .NET для соединителя индексации BCS.</span><span class="sxs-lookup"><span data-stu-id="58775-180">**.NET BCS connector** SharePoint does not include a predefined BCS connector for .NET connectors, so in addition to creating a BDC model file, you must also create a .NET component for the BCS indexing connector.</span></span> <span data-ttu-id="58775-181">Необходимо реализовать необходимые стереотипные операции для поддержки обхода данных и реализации методов для синтаксического анализа доступа к данным и URL-адреса идентификаторы.</span><span class="sxs-lookup"><span data-stu-id="58775-181">You must implement the required stereotyped operations to support crawling the data, and implement methods for parsing the access URLs and BDC identifiers.</span></span>
    
  
- <span data-ttu-id="58775-182">**BCS настраиваемого соединителя** SharePoint не включает предопределенные соединитель BCS для настраиваемых соединителей .NET, в дополнение к Создание файла модели BDC, необходимо также создать компонент .NET для BCS, соединителе индексирования, как необходимо для соединителя .NET BCS.</span><span class="sxs-lookup"><span data-stu-id="58775-182">**Custom BCS connector** SharePoint does not include a predefined BCS connector for custom .NET connectors, so in addition to creating a BDC model file, you must also create a .NET component for the BCS indexing connector, just as you must for the .NET BCS connector.</span></span> <span data-ttu-id="58775-183">Необходимо реализовать необходимые стереотипные операции для поддержки обхода данных и реализации методов для синтаксического анализа доступа к данным и URL-адреса идентификаторы.</span><span class="sxs-lookup"><span data-stu-id="58775-183">You must implement the required stereotyped operations to support crawling the data, and implement methods for parsing the access URLs and BDC identifiers.</span></span> <span data-ttu-id="58775-184">Кроме того, необходимо реализовать интерфейс **ISystemUtility** .</span><span class="sxs-lookup"><span data-stu-id="58775-184">You must also implement the **ISystemUtility** interface.</span></span>
    
  

## <a name="building-bcs-indexing-connectors"></a><span data-ttu-id="58775-185">Построение соединители индексации BCS</span><span class="sxs-lookup"><span data-stu-id="58775-185">Building BCS indexing connectors</span></span>
<span data-ttu-id="58775-186"><a name="ConnectorFramework_BCSOverview"> </a></span><span class="sxs-lookup"><span data-stu-id="58775-186"></span></span>

<span data-ttu-id="58775-187">При разработке соединителя индексации BCS  только что создаваемым файла модели BDC для базы данных и веб-службы индексирования соединители, или создание файла модели BDC и написания кода компонент соединителя BCS для .NET и настраиваемые соединители индексации, необходимо учитывать следующее:</span><span class="sxs-lookup"><span data-stu-id="58775-187">When you develop a BCS indexing connector—whether you're just creating the BDC model file for database and web service indexing connectors, or creating the BDC model file and coding the BCS connector component for .NET and custom indexing connectors—you need to think about the following:</span></span>
  
    
    

- <span data-ttu-id="58775-p115">**Подключения к** Порядок подключения к репозиторию внешних данных, например, адрес сервера, IP-адрес или имя экземпляра базы данных. Также включает сведения о проверке подлинности, используемый для подключения к внешним данным репозитория.</span><span class="sxs-lookup"><span data-stu-id="58775-p115">**Connectivity** How to connect to the external data repository, for example, the server address, IP address, or database instance name. Also includes the authentication information used to connect to the external data repository.</span></span>
    
  
- <span data-ttu-id="58775-p116">**Структура репозитория** Для чтения данных, соединитель должен знать, как организованы репозитория.  Это иерархическая, enumerical или имеет проходить ссылки?</span><span class="sxs-lookup"><span data-stu-id="58775-p116">**Structure of repository** To read the data, the connector must know how the repository is organized. Is it hierarchical, enumerical, or does it have to traverse links?</span></span>
    
  
- <span data-ttu-id="58775-p117">**Выполняет добавочный обход** Чтобы уменьшить нагрузку на хранилище внешних данных, присвойте соединителю возможность выполнять добавочные обходы контента в дополнение к полный обход. Для этого соединителя необходимо определить, какие данные были изменены с момента последнего обхода и иметь возможность выполнять обход содержимого только эти данные. Это можно сделать с помощью добавочного обхода контента на основе метки времени или обхода на основе журнала изменений. При реализации подход зависит от API-интерфейсы, предоставляемые репозитория и актуальности контента.</span><span class="sxs-lookup"><span data-stu-id="58775-p117">**Incremental crawls** To reduce the performance load on the external data repository, give the connector the ability to do incremental crawls in addition to full crawls. For this, the connector must recognize what data has changed since the last crawl and be able to crawl only that data. This can be done by using a timestamp-based incremental crawl or a change log-based crawl. The approach you implement depends on the APIs provided by the repository and the freshness goals for the content.</span></span>
    
  
- <span data-ttu-id="58775-p118">**Обеспечение безопасности данных** В большинстве случаев не все данные доступны для всех пользователей. Важно, что это также работает с поиска, поэтому когда пользователь выполняет поиск с помощью пользовательского интерфейса поиска, пользователь может видеть только результаты он или она имеет доступ к. Это означает, что соединитель должен знать, как читать безопасности внешней системы и перенести эти сведения, связанные с безопасностью обратно во время обхода контента в индексе. Например можно реализовать во время обхода хранения Windows NT списки управления доступом (ACL).</span><span class="sxs-lookup"><span data-stu-id="58775-p118">**Securing data** In most scenarios, not all data is accessible to all users. It's important that this also works with search, so when a user searches by using the search UI, the user can see only the results he or she has access to. This means the connector must know how to read the security of the external system, and bring that security-related information back during the crawl into the index. For example, you could implement crawl-time storage of Windows NT access control lists (ACLs).</span></span>
    
  
<span data-ttu-id="58775-200">В таблице 2 описываются стереотипные операции, которые применяются при создании соединителя индексации BCS для SharePoint.</span><span class="sxs-lookup"><span data-stu-id="58775-200">Table 2 describes the stereotyped operations that apply when you create a BCS indexing connector for SharePoint.</span></span>
  
    
    

<span data-ttu-id="58775-201">**В таблице 2. BCS stereotyped операций, поддерживаемых службой поиска в SharePoint**</span><span class="sxs-lookup"><span data-stu-id="58775-201">**Table 2. BCS stereotyped operations supported by Search in SharePoint**</span></span>


|<span data-ttu-id="58775-202">**Operation**</span><span class="sxs-lookup"><span data-stu-id="58775-202">**Operation**</span></span>|<span data-ttu-id="58775-203">**Описание**</span><span class="sxs-lookup"><span data-stu-id="58775-203">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="58775-204">Служба поиска</span><span class="sxs-lookup"><span data-stu-id="58775-204">Finder</span></span>  <br/> |<span data-ttu-id="58775-p119">Основные операции, необходимые при создании соединителя BCS. Эта операция извлекает список элементов внешнего источника контента. В разделе  [Реализация Finder](http://msdn.microsoft.com/library/a0cb7cfe-8758-4057-aa85-03071536745e%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="58775-p119">Core operation required when creating a BCS connector. This operation retrieves the list of items of the external content source. See  [Implementing a Finder](http://msdn.microsoft.com/library/a0cb7cfe-8758-4057-aa85-03071536745e%28Office.15%29.aspx).  </span></span><br/> |
|<span data-ttu-id="58775-208">SpecificFinder</span><span class="sxs-lookup"><span data-stu-id="58775-208">SpecificFinder</span></span>  <br/> |<span data-ttu-id="58775-p120">Основные операции, необходимые при создании соединителя BCS. Эта операция получает отдельные элементы из внешнего источника контента. В разделе  [Реализация SpecificFinder](http://msdn.microsoft.com/library/9b6effa5-20ce-4ce7-a8dc-0fd601eb0f23%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="58775-p120">Core operation required when creating a BCS connector. This operation retrieves individual items from the external content source. See  [Implementing a SpecificFinder](http://msdn.microsoft.com/library/9b6effa5-20ce-4ce7-a8dc-0fd601eb0f23%28Office.15%29.aspx).  </span></span><br/> |
|<span data-ttu-id="58775-212">ChangedIdEnumerator</span><span class="sxs-lookup"><span data-stu-id="58775-212">ChangedIdEnumerator</span></span>  <br/> |<span data-ttu-id="58775-p121">Требуется реализовать добавочные обходы контента на основе журнала изменений. В разделе  [Реализация ChangedIdEnumerator](http://msdn.microsoft.com/library/19d3c942-f6d7-49e7-853f-4d9b61b10422%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="58775-p121">Required to implement changelog-based incremental crawls. See  [Implementing a ChangedIdEnumerator](http://msdn.microsoft.com/library/19d3c942-f6d7-49e7-853f-4d9b61b10422%28Office.15%29.aspx).  </span></span><br/> |
|<span data-ttu-id="58775-215">DeletedIdEnumerator</span><span class="sxs-lookup"><span data-stu-id="58775-215">DeletedIdEnumerator</span></span>  <br/> |<span data-ttu-id="58775-p122">Требуется реализовать добавочные обходы контента на основе журнала изменений. В разделе  [Реализация DeletedIdEnumerator](http://msdn.microsoft.com/library/aa1c521a-0c9b-4dc0-a32f-fb9e54c52bed%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="58775-p122">Required to implement changelog-based incremental crawls. See  [Implementing a DeletedIdEnumerator](http://msdn.microsoft.com/library/aa1c521a-0c9b-4dc0-a32f-fb9e54c52bed%28Office.15%29.aspx).  </span></span><br/> |
|<span data-ttu-id="58775-218">Binarysecuritydescriptoraccessor используется</span><span class="sxs-lookup"><span data-stu-id="58775-218">BinarySecurityDescriptorAccessor</span></span>  <br/> |<span data-ttu-id="58775-p123">Требуется для реализации безопасности на уровне элементов. Возвращает дескриптор безопасности для элемента из внешнего источника контента. В разделе  [Реализация binarysecuritydescriptoraccessor используется](http://msdn.microsoft.com/library/6cf70490-dd3c-49cd-bb13-ed33e938435d%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="58775-p123">Required to implement item-level security. Returns the security descriptor for an item from the external content source. See  [Implementing a BinarySecurityDescriptorAccessor](http://msdn.microsoft.com/library/6cf70490-dd3c-49cd-bb13-ed33e938435d%28Office.15%29.aspx).  </span></span><br/> |
|<span data-ttu-id="58775-222">StreamAccessor</span><span class="sxs-lookup"><span data-stu-id="58775-222">StreamAccessor</span></span>  <br/> |<span data-ttu-id="58775-p124">Требуется, чтобы включить обход вложений из внешнего источника контента. Возвращает вложения как поток данных. В разделе  [Реализация StreamAccessor](http://msdn.microsoft.com/library/e3d8053b-90c0-4207-98e3-91e42db13cf1%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="58775-p124">Required to enable crawling of attachments from the external content source. Returns the attachment as a data stream. See  [Implementing a StreamAccessor](http://msdn.microsoft.com/library/e3d8053b-90c0-4207-98e3-91e42db13cf1%28Office.15%29.aspx).  </span></span><br/> |
   

  
    
    

### <a name="tooling-support-for-developing-bcs-indexing-connectors"></a><span data-ttu-id="58775-226">Создание поддержку для разработки индексирования соединители BCS</span><span class="sxs-lookup"><span data-stu-id="58775-226">Tooling support for developing BCS indexing connectors</span></span>

<span data-ttu-id="58775-227">Службы BCS предоставляют вспомогательных средств для соединителей BCS в SharePoint Designer и Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="58775-227">BCS provides tooling support for BCS connectors in SharePoint Designer and Visual Studio.</span></span>
  
    
    

#### <a name="sharepoint-designer-tooling-support-for-bcs-connectors"></a><span data-ttu-id="58775-228">SharePoint Designer управляемых средствах для соединителей BCS</span><span class="sxs-lookup"><span data-stu-id="58775-228">SharePoint Designer tooling support for BCS connectors</span></span>

<span data-ttu-id="58775-p125">SharePoint Designer предоставляет ограниченный набор возможностей. его можно использовать для создания файлов модели для существующих типов соединителя BCS, таких как базы данных, веб-службы и соединители .NET BCS BDC. Вы также можно использовать для экспорта модели BDC файлы из одного приложения-службы BCS для другого приложения-службы BCS.</span><span class="sxs-lookup"><span data-stu-id="58775-p125">SharePoint Designer provides a limited set of capabilities; you can use it to create BDC model files for existing BCS connector types, such as database, web service, and .NET BCS connectors. You can also use it to export BDC model files from one BCS service application to another BCS service application.</span></span>
  
    
    

#### <a name="visual-studio-tooling-support-for-bcs-connectors"></a><span data-ttu-id="58775-231">Visual Studio управляемых средствах для соединителей BCS</span><span class="sxs-lookup"><span data-stu-id="58775-231">Visual Studio tooling support for BCS connectors</span></span>

<span data-ttu-id="58775-p126">Visual Studio можно использовать для создания компонентов для соединителей .NET BCS и настраиваемые соединители BCS. Для соединителей .NET BCS Visual Studio предоставляет шаблон проекта модели подключения к бизнес-данным, который включает набор конструкторов и возможности управления кода для упрощения создания, отладки и развертывания компонента .NET и связанного файла модели BDC для соединителя .NET BCS. Нет соответствующего шаблона проекта для настраиваемых соединителей BCS.</span><span class="sxs-lookup"><span data-stu-id="58775-p126">You can use Visual Studio to create the component for .NET BCS connectors and custom BCS connectors. For .NET BCS connectors, Visual Studio provides the Business Data Connectivity Model project template, which includes a set of visual designers and code management capabilities to enable you to more easily create, debug, and deploy the .NET component and the associated BDC model file for the .NET BCS connector. There is no corresponding project template for custom BCS connectors.</span></span>
  
    
    

## <a name="connector-framework-enhancements-in-sharepoint"></a><span data-ttu-id="58775-235">Улучшения Connector framework в SharePoint</span><span class="sxs-lookup"><span data-stu-id="58775-235">Connector framework enhancements in SharePoint</span></span>
<span data-ttu-id="58775-236"><a name="SP15searchconnect_enhancements"> </a></span><span class="sxs-lookup"><span data-stu-id="58775-236"></span></span>

<span data-ttu-id="58775-237">В SharePoint connector framework поддерживает BCS соединителей получения сведения об утверждениях для контента, хранящегося в репозиториях, настраиваемый компонент внешних данных.</span><span class="sxs-lookup"><span data-stu-id="58775-237">In SharePoint the connector framework supports BCS connectors retrieving claims information for content that is stored in custom external data repositories.</span></span>
  
    
    
<span data-ttu-id="58775-238">Connector framework также предоставляет улучшенные исключений записи и ведение журнала для помощи в устранении ошибки, обнаруженные во время обхода источников контента с помощью соединителей BCS.</span><span class="sxs-lookup"><span data-stu-id="58775-238">The connector framework also provides improved exception capturing and logging to help you troubleshoot errors encountered when crawling content sources by using BCS connectors.</span></span>
  
    
    

## <a name="additional-resources"></a><span data-ttu-id="58775-239">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="58775-239">Additional resources</span></span>
<span data-ttu-id="58775-240"><a name="SP15searchconnect_addlresources"> </a></span><span class="sxs-lookup"><span data-stu-id="58775-240"></span></span>


-  [<span data-ttu-id="58775-241">Улучшение файла модели BDC для поиска в SharePoint</span><span class="sxs-lookup"><span data-stu-id="58775-241">Enhancing the BDC model file for Search in SharePoint</span></span>](enhancing-the-bdc-model-file-for-search-in-sharepoint.md)
    
  
-  [<span data-ttu-id="58775-242">SharePoint 2013: пример пользовательского соединителя индексирования служб BCS MyFileConnector</span><span class="sxs-lookup"><span data-stu-id="58775-242">SharePoint 2013: MyFileConnector custom BCS indexing connector sample</span></span>](https://code.msdn.microsoft.com/sharepoint-2013-myfileconne-79d2ea26)
    
  
-  [<span data-ttu-id="58775-243">Как: обход связанных внешних типов контента в SharePoint</span><span class="sxs-lookup"><span data-stu-id="58775-243">How to: Crawl associated external content types in SharePoint</span></span>](how-to-crawl-associated-external-content-types-in-sharepoint.md)
    
  
-  [<span data-ttu-id="58775-244">Как: обхода больших двоичных объектов (BLOB) в SharePoint</span><span class="sxs-lookup"><span data-stu-id="58775-244">How to: Crawl binary large objects (BLOBs) in SharePoint</span></span>](how-to-crawl-binary-large-objects-blobs-in-sharepoint.md)
    
  
-  [<span data-ttu-id="58775-245">Как: обход связанных внешних типов контента в SharePoint</span><span class="sxs-lookup"><span data-stu-id="58775-245">How to: Crawl associated external content types in SharePoint</span></span>](how-to-crawl-associated-external-content-types-in-sharepoint.md)
    
  
-  [<span data-ttu-id="58775-246">Как: настройка безопасности на уровне элементов в SharePoint</span><span class="sxs-lookup"><span data-stu-id="58775-246">How to: Configure item-level security in SharePoint</span></span>](how-to-configure-item-level-security-in-sharepoint.md)
    
  

