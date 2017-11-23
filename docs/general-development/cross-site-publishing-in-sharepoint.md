---
title: "Публикация в SharePoint на нескольких сайтах"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 33f49e69-c1d3-4a6e-8887-5df683cba022
ms.openlocfilehash: cbb1a0eec5d60b8453e3d6c66179142fa1e07630
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="cross-site-publishing-in-sharepoint"></a><span data-ttu-id="6c432-102">Публикация в SharePoint на нескольких сайтах</span><span class="sxs-lookup"><span data-stu-id="6c432-102">Cross-site publishing in SharePoint</span></span>

<span data-ttu-id="6c432-103">SharePoint представляется межсайтовой публикации функциональная возможность, которая позволяет повторно использовать содержимое в нескольких семействах сайтов.</span><span class="sxs-lookup"><span data-stu-id="6c432-103">SharePoint introduces a cross-site publishing feature that enables you to reuse content across multiple site collections.</span></span> <span data-ttu-id="6c432-104">Встроенные возможности поиска используется для включения сценариев и архитектуры для публикации.</span><span class="sxs-lookup"><span data-stu-id="6c432-104">It uses built-in search capabilities to enable publishing scenarios and architectures.</span></span> <span data-ttu-id="6c432-105">В первый раз, вы можете разработать сайты, которые кросс-фермах SharePoint — Включение сайтов охватывать границу между интрасети и Интернет.</span><span class="sxs-lookup"><span data-stu-id="6c432-105">For the first time, you can design sites that cross SharePoint farms—enabling your sites to span the boundary between intranets and the Internet.</span></span>
  
    
    

<span data-ttu-id="6c432-p102">Рассмотрите возможность сайта с одной среды разработки семейства веб-сайтов, каналов несколько семейств сайтов публикации, с помощью различных доменах все для обхода общедоступных поисковыми и оптимизирован для оптимизации поисковых систем (SEO). Этот сценарий и других, как его, позволяет публикации на нескольких сайтах без необходимости развертывания контента. Публикация на нескольких сайтах был разработан с некоторые общие сценарии в виду, включая:</span><span class="sxs-lookup"><span data-stu-id="6c432-p102">Consider a site with one authoring site collection that feeds multiple publishing site collections, with different domains, all crawled by public search engines and optimized for search engine optimization (SEO). Cross-site publishing enables this scenario and others like it, without requiring you to use content deployment. Cross-site publishing was designed with some common scenarios in mind, including:</span></span>
  
    
    


- <span data-ttu-id="6c432-109">Совместное использование списка или библиотеки страниц как к каталогу публикации</span><span class="sxs-lookup"><span data-stu-id="6c432-109">Share an item list or a page library as a publishing catalog</span></span>
    
  
- <span data-ttu-id="6c432-110">Использование каталога из поиска</span><span class="sxs-lookup"><span data-stu-id="6c432-110">Consume a catalog from search</span></span>
    
  
- <span data-ttu-id="6c432-111">Объединение публикации на нескольких сайтах с варианты для включения многоязычных сайтов из распространенных семействе сайтов разработки среды разработки</span><span class="sxs-lookup"><span data-stu-id="6c432-111">Combine cross-site publishing with the variations feature to enable authoring multilingual sites from a common authoring site collection</span></span>
    
  

## <a name="catalogs"></a><span data-ttu-id="6c432-112">Каталоги</span><span class="sxs-lookup"><span data-stu-id="6c432-112">Catalogs</span></span>
<span data-ttu-id="6c432-113"><a name="SP15_CrossSitePublising_Catalog"> </a></span><span class="sxs-lookup"><span data-stu-id="6c432-113"></span></span>

<span data-ttu-id="6c432-114">Каталоги, введенные в SharePoint, относятся к списку или библиотеке, который открыт для поиска для использования на веб-сайтах публикации.</span><span class="sxs-lookup"><span data-stu-id="6c432-114">Catalogs, introduced in SharePoint, include a list or library that is shared out to search for consumption on publishing sites.</span></span> <span data-ttu-id="6c432-115">Каталоги включить содержимое для публикации в семействах сайтов — компоненты публикации cross-site зависят от каталоги.</span><span class="sxs-lookup"><span data-stu-id="6c432-115">Catalogs enable content to be published across site collections—the cross-site publishing features depend on catalogs.</span></span> <span data-ttu-id="6c432-116">Каталоги можно использовать для повторного использования содержимого действительно между сайтами и через границу между сайты интрасети, экстрасети и веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="6c432-116">You can use catalogs to really reuse content across your sites and across the boundary between your intranet sites, extranet sites, and Internet sites.</span></span> <span data-ttu-id="6c432-117">Для предварительно заданных поисковых запросов каталоги помечаются возможности поиска.</span><span class="sxs-lookup"><span data-stu-id="6c432-117">For predefined search queries, catalogs are flagged in search.</span></span> <span data-ttu-id="6c432-118">Может стать содержимое, хранящееся в каталогах семейства веб-сайтов с помощью [Веб-части поиска контента в SharePoint](content-search-web-part-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="6c432-118">You can surface content stored in catalogs across site collections by using the  [Content Search Web Part in SharePoint](content-search-web-part-in-sharepoint.md).</span></span>
  
    
    

## <a name="when-should-i-use-cross-site-publishing"></a><span data-ttu-id="6c432-119">Когда следует использовать публикации на нескольких сайтах</span><span class="sxs-lookup"><span data-stu-id="6c432-119">When should I use cross-site publishing?</span></span>
<span data-ttu-id="6c432-120"><a name="SP15_CrossSitePublising_WhenShouldIUseCrossSitePublishing"> </a></span><span class="sxs-lookup"><span data-stu-id="6c432-120"></span></span>

<span data-ttu-id="6c432-p104">Существует ряд случаев, когда публикации на нескольких сайтах не эффективным или соответствующие. Ли у вас есть внешних источников данных и способ подключения к их вариантов, сайта, типа реализации базы данных поиска и использующие каталога продуктов, все факторы, которые должны повлиять на решение. В таблице 1 представлены дополнительные сведения о эти рекомендации по проектированию.</span><span class="sxs-lookup"><span data-stu-id="6c432-p104">There are some cases where cross-site publishing is not efficient or appropriate. Whether you have external data sources and how you connect to them, variations, site type, search database implementation, and use of the product catalog are all factors that should influence your decision. Table 1 provides more information about these design considerations.</span></span>
  
    
    

<span data-ttu-id="6c432-124">**В таблице 1. Вопросы разработки для публикации на нескольких сайтах**</span><span class="sxs-lookup"><span data-stu-id="6c432-124">**Table 1. Design considerations for cross-site publishing**</span></span>


|<span data-ttu-id="6c432-125">**Вопрос проектирования**</span><span class="sxs-lookup"><span data-stu-id="6c432-125">**Design Consideration**</span></span>|<span data-ttu-id="6c432-126">**Описание**</span><span class="sxs-lookup"><span data-stu-id="6c432-126">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="6c432-127">**Время задержки**</span><span class="sxs-lookup"><span data-stu-id="6c432-127">**Lag time**</span></span> <br/> |<span data-ttu-id="6c432-128">Если задержки между временем автор публикует страницы и когда он отображается на сайте слишком много времени для тех, кто зависит от его, может потребоваться рекомендуется использовать развертывания контента.</span><span class="sxs-lookup"><span data-stu-id="6c432-128">If the delay between the time an author publishes a page and when it shows up on the site is too long for someone who depends on it, you may want to consider using content deployment instead.</span></span>  <br/> |
|<span data-ttu-id="6c432-129">**Реализация базы данных поиска**</span><span class="sxs-lookup"><span data-stu-id="6c432-129">**Search database implementation**</span></span> <br/> |<span data-ttu-id="6c432-p105">Если подключение базы данных поиска к внешнему источнику данных и использование соединителя external (не SharePoint), нельзя использовать публикации на нескольких сайтах. Если вы используете подключения к бизнес-служб (BCS), можно использовать публикации на нескольких сайтах.</span><span class="sxs-lookup"><span data-stu-id="6c432-p105">If you connect your search database to an external data source and you use an external (non-SharePoint) connector, you can't use cross-site publishing. If you use business connection services (BCS), you can use cross-site publishing.</span></span>  <br/> <span data-ttu-id="6c432-p106">Использование публикации на нескольких сайтах с базы данных поиска имеет смысл в некоторых случаях, но не для других пользователей. Не следует использовать публикации на нескольких сайтах публикации с исходного сайта непосредственно к Интернету, чтобы не включает базу данных поиска в реализации планирования или пользовательского кода.</span><span class="sxs-lookup"><span data-stu-id="6c432-p106">Using cross-site publishing with the search database makes sense in some cases but not others. You should not use cross-site publishing to publish from a source site directly to the Internet in a way that does not include your search database in the planning or custom code implementation.</span></span>  <br/> |
|<span data-ttu-id="6c432-134">**Варианты реализации**</span><span class="sxs-lookup"><span data-stu-id="6c432-134">**Variations implementation**</span></span> <br/> |<span data-ttu-id="6c432-p107">Если вы реализуете основных вариантов сайта, с помощью библиотеки страниц, библиотеки документов и общие перечислены доступные на нескольких языках, смысл, публикации на нескольких сайтах. Это значение true, если вы решаете реализовать управляемую навигацию или структурированная навигация на сайте вариантов.</span><span class="sxs-lookup"><span data-stu-id="6c432-p107">If you are implementing a basic variations site that makes a pages library, document library, and general lists available in a few languages, cross-site publishing makes sense. The same is true if you choose to implement managed navigation or structured navigation on a variations site.  </span></span><br/> <span data-ttu-id="6c432-p108">Для некоторых архитектуры, но не другие работает публикации на нескольких сайтах. Например можно использовать публикации на нескольких сайтах для публикации содержимого из вариантов **SPSite** к сайту публикации с некоторыми вариациями включен, если источник **SPSite** не является получение данных из другого вариантов сайта или семейства сайтов. </span><span class="sxs-lookup"><span data-stu-id="6c432-p108">Cross-site publishing works for some architectures but not others. For example, you can use cross-site publishing to publish content from a variations **SPSite** to a publishing site with variations enabled if the source **SPSite** is not consuming data from another variations site or site collection. </span></span><br/> |
|<span data-ttu-id="6c432-139">**Реализация каталога**</span><span class="sxs-lookup"><span data-stu-id="6c432-139">**Catalog implementation**</span></span> <br/> |<span data-ttu-id="6c432-p109">Ли реализовать каталог продуктов в архитектуру сайта, и как реализовать может повлиять на, является ли выбор наиболее эффективного или соответствующий публикации на нескольких сайтах. Если используется каталог продуктов для поддержки конфигурации сайта вариантов многоязыкового и публикации для Интернет-сайт, вы можете реализовать публикации на нескольких сайтах.</span><span class="sxs-lookup"><span data-stu-id="6c432-p109">Whether you implement the product catalog into your site architecture and how you implement it may affect whether cross-site publishing is the most effective or appropriate choice. If you are using the product catalog to support a multilingual variations site configuration and are publishing to an Internet site, you can implement cross-site publishing.</span></span>  <br/> |
|<span data-ttu-id="6c432-142">**Управляемая Навигация**</span><span class="sxs-lookup"><span data-stu-id="6c432-142">**Managed navigation**</span></span> <br/> |<span data-ttu-id="6c432-p110">Публикация на нескольких сайтах для работы с большинством реализаций управляемой навигации и банка терминов. В некоторых приложениях Передача метаданных навигации могут работать неправильно. Например когда одного сайта вариантов зависит от метаданных с другого сайта вариантов диск навигацию по сайту и использовании публикации на нескольких сайтах для публикации содержимого на целевом сайте, передачи метаданных навигации может работает должным образом.</span><span class="sxs-lookup"><span data-stu-id="6c432-p110">Cross-site publishing works with most implementations of managed navigation and the term store. In some implementations, navigation metadata transfer may not work as expected. For example, when one variations site depends on metadata from another variations site to drive site navigation, and you use cross-site publishing to publish content to the target site, navigation metadata transfer may not work as expected.</span></span>  <br/> |
   

## <a name="how-can-i-set-up-a-catalog"></a><span data-ttu-id="6c432-146">Как можно настроить каталога?</span><span class="sxs-lookup"><span data-stu-id="6c432-146">How can I set up a catalog?</span></span>
<span data-ttu-id="6c432-147"><a name="SP15_CrossSitePublising_WhenShouldIUseCrossSitePublishing"> </a></span><span class="sxs-lookup"><span data-stu-id="6c432-147"></span></span>

<span data-ttu-id="6c432-148">Страницы категорий и страницы элементов каталогов, макеты страниц, которые можно использовать для отображения содержимого каталогов структурированных постоянно на сайте.</span><span class="sxs-lookup"><span data-stu-id="6c432-148">Category pages and catalog item pages are page layouts that you can use to show structured catalog content consistently across a site.</span></span> <span data-ttu-id="6c432-149">SharePoint позволяет создавать и настраивать макетов страниц для SharePoint и выше.</span><span class="sxs-lookup"><span data-stu-id="6c432-149">SharePoint enables you to create and customize page layouts for SharePoint and above.</span></span> <span data-ttu-id="6c432-150">Дополнительные сведения содержатся в разделе [Настройка макетов страниц для сайтов на основе каталога в SharePoint](https://msdn.microsoft.com/ru-ru/library/office/dn144674.aspx 
).</span><span class="sxs-lookup"><span data-stu-id="6c432-150">For more information, see  [Customize page layouts for a catalog-based site in SharePoint](https://msdn.microsoft.com/ru-ru/library/office/dn144674.aspx 
).</span></span>
  
    
    

## <a name="cross-site-publishing-apis"></a><span data-ttu-id="6c432-151">Интерфейсы API межсайтовой публикации</span><span class="sxs-lookup"><span data-stu-id="6c432-151">Cross-site publishing APIs</span></span>
<span data-ttu-id="6c432-152"><a name="SP15_CrossSitePublising_CrossSitePublishingAPIs"> </a></span><span class="sxs-lookup"><span data-stu-id="6c432-152"></span></span>

<span data-ttu-id="6c432-153">SharePoint представлены классы, которые можно использовать для поддержки нескольких сайтах публикации реализации в вашем коде.</span><span class="sxs-lookup"><span data-stu-id="6c432-153">SharePoint introduces classes that you can use to support cross-site publishing implementation in your code.</span></span> <span data-ttu-id="6c432-154">Эти API-интерфейсы доступны в библиотеке публикации сервера .NET.</span><span class="sxs-lookup"><span data-stu-id="6c432-154">These APIs are available in the .NET server publishing library.</span></span> <span data-ttu-id="6c432-155">Используйте их для настройки как делится списки как каталоги для повторного использования содержимого; или использует каталога из поиска SharePoint.</span><span class="sxs-lookup"><span data-stu-id="6c432-155">Use them to customize how SharePoint shares lists as catalogs for content reuse or consumes a catalog from search.</span></span> <span data-ttu-id="6c432-156">Для поддержки нескольких сайтах публикации задачи можно использовать члены следующих классов в пользовательском коде:</span><span class="sxs-lookup"><span data-stu-id="6c432-156">You can use the members of the following classes in custom code to support cross-site publishing tasks:</span></span>
  
    
    

- <span data-ttu-id="6c432-157">Класс **PublishingCatalogUtility** используется для получения списка доступных каталогов, получение сведений о каталоги и их состояние, получение сведений о списков и библиотек, которые могут быть подключены к каталогам и запуск или остановка общего доступа к каталогам.</span><span class="sxs-lookup"><span data-stu-id="6c432-157">Use the **PublishingCatalogUtility** class to retrieve a list of available catalogs, get information about catalogs and their statuses, get information about lists and libraries that can be connected to catalogs, and start or stop sharing catalogs.</span></span>
    
    
    


```cs
  
/// Retrieve available catalogs.
public static List<CatalogConnectionSettings> GetPublishingCatalogs(SPSite site, int startRow, int numberOfRows, string filterText, out int totalNumberOfCatalogs)
```


    
    


```cs
  
///Get catalog information that is saved for a list.
public static bool GetCatalogConfiguration(SPList list, out CatalogShareSettings catalogSettings, out string selectedTaxonomyField)
```


    
    


```cs
  
///Stop sharing a list or library as a publishing catalog for cross-publishing content reuse.
public static void UnPublishCatalog(SPList list)
```

- <span data-ttu-id="6c432-p113">Класс **CatalogCollectionManager** используется для работы со каталоги из поиска. Сведения о подключении, имеющей каталога для поиска и получать сведения о ней. Добавить или удалить каталог из внутренней коллекции каталоги и очереди операции в очередь, который настраивается на перезапись URL-адресов при вызове метода **Update** подключение.</span><span class="sxs-lookup"><span data-stu-id="6c432-p113">Use the **CatalogCollectionManager** class to consume catalogs from search. Learn about the connection that a catalog has to search, and get information about it. Add or remove a catalog from the internal collection of catalogs, and queue an operation to queue up a connection that is configured to rewrite URLs when the **Update** method is called.</span></span>
    
    
    


```cs
  
/// Add catalog or site source into the internal CatalogInfo collection, but the source is not persisted into the property bag.
public void AddCatalogConnection(CatalogConnectionSettings catalogInfo)
```


    
    


```cs
  
/// Queues an Add operation to add a connection configured to rewrite URLs. The connection is added to the store when the Update method is called.
public void AddCatalogConnection(CatalogConnectionSettings catalogInfo, 
string[] orderedPropertiesForUrlRewrite,
string webUrl, 
string catalogTaxonomyManagedProperty,
bool isManualRule)
```


    
    


```cs
  
/// Update existing catalog/site source in the internal CatalogInfo collection. Edits are not committed until the Update method is called.
public void UpdateCatalogConnection(CatalogConnectionSettings catalogInfo)
```


    
    


```cs
  
/// Remove a catalog or site source. Deletion is not committed until the Update method is called.
public void DeleteCatalogConnection(string catalogPath)
```


    
    


```cs
  
/// Determine whether a connection exists to this source from the site.
public bool Contains(string catalogPath)
```


    
    


```cs
  
/// Get the settings for a catalog connected to this site.
public CatalogConnectionSettings GetCatalogConnectionSettings(string catalogPath)
```


## <a name="additional-resources"></a><span data-ttu-id="6c432-161">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="6c432-161">Additional resources</span></span>
<span data-ttu-id="6c432-162"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="6c432-162"></span></span>


-  [<span data-ttu-id="6c432-163">Публикация сайтов SharePoint</span><span class="sxs-lookup"><span data-stu-id="6c432-163">Publish SharePoint sites</span></span>](publish-sharepoint-sites.md)
    
  

