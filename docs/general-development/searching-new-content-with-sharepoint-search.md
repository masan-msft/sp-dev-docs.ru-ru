---
title: "Поиск по новому контенту с поиска SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 2a3a7d23-775a-4d95-9066-ebbd18c92ad4
ms.openlocfilehash: b8798b513c8db47c66c6754f72edb805fc724ce0
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="searching-new-content-with-sharepoint-search"></a><span data-ttu-id="4592f-102">Поиск по новому контенту с поиска SharePoint</span><span class="sxs-lookup"><span data-stu-id="4592f-102">Searching new content with SharePoint Search</span></span>
<span data-ttu-id="4592f-103">Узнайте, как сделать контент доступным для пользователям выполнять поиск с помощью SharePoint.</span><span class="sxs-lookup"><span data-stu-id="4592f-103">Learn how to make content available for users to search with SharePoint.</span></span>
## <a name="making-content-available-for-search-in-sharepoint"></a><span data-ttu-id="4592f-104">Создание контента, доступного для поиска в SharePoint</span><span class="sxs-lookup"><span data-stu-id="4592f-104">Making content available for search in SharePoint</span></span>

<span data-ttu-id="4592f-105">Поиска в SharePoint предоставляет два подхода для обработки запросов для возвращения результатов поиска — федеративного поиска и обхода контента.</span><span class="sxs-lookup"><span data-stu-id="4592f-105">Search in SharePoint provides two approaches for processing queries to return search results—federated search and content crawling.</span></span>
  
    
    
 <span data-ttu-id="4592f-p101">**Федеративном поиске** В этом подходе результаты поиска возвращаются для контента, обход которого не выполнен с сервера поиска. Запрос перенаправляется к внешнему репозиторию контента, где он обрабатывается поисковой системы, репозитория. Поисковый механизм репозитория затем возвращает результаты на поисковый сервер. Сервер поиска форматирует и отображает результаты из внешнего хранилища для отображения на странице результатов поиска. Такой подход имеет следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="4592f-p101">**Federated search** In this approach, search results are returned for content that is not crawled by your search server. The query is forwarded to an external content repository where it is processed by that repository's search engine. The repository's search engine then returns the results to the search server. The search server formats and renders the results from the external repository to display on the search results page. This approach offers the following advantages:</span></span>
  
    
    

- <span data-ttu-id="4592f-111">Нет дополнительных мощностей необходимых для индекса контента, как не выполняется обход контента для поиска в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="4592f-111">You require no additional capacity requirements for the content index, as content is not crawled by Search in SharePoint.</span></span>
    
  
- <span data-ttu-id="4592f-p102">Вы можете воспользоваться преимуществами существующих поисковый механизм репозитория. Например можно создать федерацию для поиска в Интернете для поиска в Интернете.</span><span class="sxs-lookup"><span data-stu-id="4592f-p102">You can take advantage of a repository's existing search engine. For example, you can federate to an Internet search engine to search the web.</span></span>
    
  
- <span data-ttu-id="4592f-114">Можно оптимизировать поисковую систему репозитория контента специально для хранящегося в нем набора контента, что позволит значительно повысить производительность этого набора.</span><span class="sxs-lookup"><span data-stu-id="4592f-114">You can optimize the content repository's search engine for the repository's specific set of content, which might provide better search performance on the content set.</span></span>
    
  
- <span data-ttu-id="4592f-115">Возможен доступ к репозиториям, которые защищены от обхода контента, но доступны для поисковых запросов.</span><span class="sxs-lookup"><span data-stu-id="4592f-115">You can access repositories that are secured against crawls, but which can be accessed by search queries.</span></span>
    
  
 <span data-ttu-id="4592f-p103">**Обход контента** В этот подход результаты возвращаются из индекса контента приложения службы поиска по запросу пользователя. Индекс контента содержит контент, для которого выполняется обход приложением-службой поиска и включает в себя текстовое содержимое и метаданные для каждого элемента контента. Такой подход позволяет:</span><span class="sxs-lookup"><span data-stu-id="4592f-p103">**Content crawling** In this approach, results are returned from the Search service application's content index based on the user's query. The content index contains content that is crawled by the Search service application, and includes text content and metadata for each content item. This approach enables you to:</span></span>
  
    
    

- <span data-ttu-id="4592f-119">Сортировка результатов по релевантности.</span><span class="sxs-lookup"><span data-stu-id="4592f-119">Sort results by relevance.</span></span>
    
  
- <span data-ttu-id="4592f-120">Управление частотой обновления индекса контента.</span><span class="sxs-lookup"><span data-stu-id="4592f-120">Control how frequently the content index is updated.</span></span>
    
  
- <span data-ttu-id="4592f-121">Определение метаданных для обхода.</span><span class="sxs-lookup"><span data-stu-id="4592f-121">Specify what metadata is crawled.</span></span>
    
  
- <span data-ttu-id="4592f-122">Выполнение одной операции резервного копирования для контента, для которого выполнен обход.</span><span class="sxs-lookup"><span data-stu-id="4592f-122">Perform a single backup operation for crawled content.</span></span>
    
  

## <a name="in-this-section"></a><span data-ttu-id="4592f-123">В этой статье</span><span class="sxs-lookup"><span data-stu-id="4592f-123">In this section</span></span>


-  [<span data-ttu-id="4592f-124">Инфраструктура соединителей поиска в SharePoint</span><span class="sxs-lookup"><span data-stu-id="4592f-124">Search connector framework in SharePoint</span></span>](search-connector-framework-in-sharepoint.md)
    
  -  [<span data-ttu-id="4592f-125">Улучшение файла модели BDC для поиска в SharePoint</span><span class="sxs-lookup"><span data-stu-id="4592f-125">Enhancing the BDC model file for Search in SharePoint</span></span>](enhancing-the-bdc-model-file-for-search-in-sharepoint.md)
    
  
  -  [<span data-ttu-id="4592f-126">Как: обход связанных внешних типов контента в SharePoint</span><span class="sxs-lookup"><span data-stu-id="4592f-126">How to: Crawl associated external content types in SharePoint</span></span>](how-to-crawl-associated-external-content-types-in-sharepoint.md)
    
  
  -  [<span data-ttu-id="4592f-127">Как: обхода больших двоичных объектов (BLOB) в SharePoint</span><span class="sxs-lookup"><span data-stu-id="4592f-127">How to: Crawl binary large objects (BLOBs) in SharePoint</span></span>](how-to-crawl-binary-large-objects-blobs-in-sharepoint.md)
    
  
  -  [<span data-ttu-id="4592f-128">Как: обход связанных внешних типов контента в SharePoint</span><span class="sxs-lookup"><span data-stu-id="4592f-128">How to: Crawl associated external content types in SharePoint</span></span>](how-to-crawl-associated-external-content-types-in-sharepoint.md)
    
  
  -  [<span data-ttu-id="4592f-129">Как: настройка безопасности на уровне элементов в SharePoint</span><span class="sxs-lookup"><span data-stu-id="4592f-129">How to: Configure item-level security in SharePoint</span></span>](how-to-configure-item-level-security-in-sharepoint.md)
    
  

