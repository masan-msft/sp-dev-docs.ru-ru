---
title: "Управляемая навигация в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 6dbb9da2d644b6f6f93ea4508616daee7fac321e
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="managed-navigation-in-sharepoint"></a><span data-ttu-id="878a4-102">Управляемая навигация в SharePoint</span><span class="sxs-lookup"><span data-stu-id="878a4-102">Managed navigation in SharePoint</span></span>

  
    
    
![Раздел концептуального обзора](../images/mod_icon_badge_conoverview.png)
  
    
    

  
    
    

  
    
    
<span data-ttu-id="878a4-104">Сведения о функции управляемой навигации на основе таксономии в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="878a4-104">Learn about the taxonomy-driven managed navigation feature in SharePoint.</span></span>
## <a name="introducing-managed-navigation"></a><span data-ttu-id="878a4-105">Общие сведения об управляемой навигации</span><span class="sxs-lookup"><span data-stu-id="878a4-105">Introducing managed navigation</span></span>
<span data-ttu-id="878a4-106"><a name="SP15_ManagedNav_Introducing"> </a></span><span class="sxs-lookup"><span data-stu-id="878a4-106"><a name="SP15_ManagedNav_Introducing"> </a></span></span>

<span data-ttu-id="878a4-p101">Хорошо спланированная навигация поможет пользователям узнать о вашем предприятии, продукции и службах, предоставляемых веб-сайтом. Обновив таксономию навигации, предприятия могут стимулировать и подстраиваться под перемены, не переделывая навигацию своего сайта. Функция управляемой навигации в SharePoint позволяет разработать навигацию сайта на основе управляемых метаданных и создавать оптимизированные для поисковых систем URL-адреса, основанные на структуре управляемой навигации. Управляемая навигация является альтернативой традиционной (структурированной) навигации SharePoint, основанной на структуре SharePoint. Так как управляемая навигация основана на таксономии, ее можно использовать, чтобы разработать навигацию сайта с учетом важных бизнес-концепций, не меняя структуру сайтов и их компонентов.</span><span class="sxs-lookup"><span data-stu-id="878a4-p101">A well-designed navigation tells your site's users a lot about the business, products, and services that the website offers. By updating the taxonomy behind the navigation, businesses can drive and keep up with change without having to recreate their site navigation in the process. In SharePoint, the managed navigation feature enables you to design site navigation that is driven by managed metadata and create SEO-friendly URLs that are derived from the managed navigation structure. Managed navigation provides an alternative to the traditional SharePoint navigation feature—structured navigation—that is based on the structure of SharePoint. Because managed navigation is driven by taxonomy, you can use it to design site navigation around important business concepts without changing the structure of your sites or site components.</span></span>
  
    
    

## <a name="how-managed-navigation-works"></a><span data-ttu-id="878a4-112">Принцип работы управляемой навигации</span><span class="sxs-lookup"><span data-stu-id="878a4-112">How managed navigation works</span></span>
<span data-ttu-id="878a4-113"><a name="SP15_ManagedNav_HowManagedNavWorks"> </a></span><span class="sxs-lookup"><span data-stu-id="878a4-113"><a name="SP15_ManagedNav_HowManagedNavWorks"> </a></span></span>

<span data-ttu-id="878a4-p102">Управляемая навигация предоставляет платформу для динамически создаваемых страниц и связанного URL-адреса, оптимизированного для поисковых систем. Каждая созданная страница представлена в иерархии навигации. Чтобы для каждой категории таксономии не требовалось создавать отдельные страницы, эта платформа предоставляет механизм шаблонов и наследования, который создает страницы для каждой навигационной ссылки. Вы можете использовать функцию тематических страниц, чтобы настраивать внешний вид этих страниц.</span><span class="sxs-lookup"><span data-stu-id="878a4-p102">Managed navigation provides a framework for dynamically generated pages and provides an associated SEO-friendly URL. Each generated page is represented in the navigation hierarchy. Instead of requiring separate pages to be authored for each category in the taxonomy, the framework provides a templating and inheritance mechanism that creates the landing pages for each navigation link. You can use the topic pages feature to customize the landing page experience.</span></span>
  
    
    
<span data-ttu-id="878a4-p103">Интерфейсы API управляемой навигации встроены в компоненты таксономии и публикации SharePoint. Такие компоненты управляемых метаданных, как наборы терминов и банк терминов, используются, чтобы сайт поддерживал навигацию на основе таксономии. В серверной библиотеке классов .NET пространство имен  [Microsoft.SharePoint.Publishing.Navigation](https://msdn.microsoft.com/library/Microsoft.SharePoint.Publishing.Navigation.aspx) содержит термины, наборы терминов и другие объекты классов, которые дублируют классы **Term** и **TermSet** в пространстве имен навигации [Microsoft.SharePoint.Taxonomy](https://msdn.microsoft.com/library/Microsoft.SharePoint.Taxonomy.aspx) , предоставляя методы и свойства, разработанные специально для связывания этих метаданных с элементами навигации. Другие классы, например [TaxonomySiteMapNode](https://msdn.microsoft.com/library/Microsoft.SharePoint.Publishing.Navigation.TaxonomySiteMapNode.aspx) , позволяют предоставлять метаданные с различными элементами навигации сайта, например узлами карты сайта и другими элементами навигации сайта. Другие классы позволяют использовать кэширование и контекст для управляемой навигации.</span><span class="sxs-lookup"><span data-stu-id="878a4-p103">Managed navigation APIs are built into the taxonomy and publishing libraries in SharePoint. Managed metadata components like term sets and the term store are used to enable taxonomy-driven navigation for your site. In the .NET server class library, the  [Microsoft.SharePoint.Publishing.Navigation](https://msdn.microsoft.com/library/Microsoft.SharePoint.Publishing.Navigation.aspx) namespace contains term, term set, and other class objects that mirror the **Term** class and **TermSet** class in the [Microsoft.SharePoint.Taxonomy](https://msdn.microsoft.com/library/Microsoft.SharePoint.Taxonomy.aspx) navigation namespace, providing methods and properties specifically designed to associate those metadata items with navigation elements. Other classes, like [TaxonomySiteMapNode](https://msdn.microsoft.com/library/Microsoft.SharePoint.Publishing.Navigation.TaxonomySiteMapNode.aspx) , enable you to provide metadata with various site navigation elements, such as site map nodes and other parts of your site's navigation. Other classes enable caching and context for managed navigation.</span></span>
  
    
    
<span data-ttu-id="878a4-p104">В глобальной навигации могут отображаться ссылки навигации на основе таксономии. Глобальная навигация  это уровень навигации с одним или несколькими слоями, который всегда присутствует, обычно отображается в верхней части сайта и отображает категории контента верхнего уровня. Эти ссылки также могут отображаться в текущем элементе управления навигации, который часто отображается в левой части страницы. Текущий элемент управления навигации представляет следующий уровень иерархии для категории, выбранной в глобальной навигации, или набор ссылок, принадлежащих к этой категории.</span><span class="sxs-lookup"><span data-stu-id="878a4-p104">You can display taxonomy-driven navigation links in the Global Navigation. The Global Navigation is a navigation layer with one or more layers that's always present, which often appears at the top of a site and displays the top-level content categories. You can also display these links in the current navigation control that often appears on the left side of a page. The current navigation control represents the next level of hierarchy for the category chosen in Global Navigation, or a set of links that belong to that category.</span></span>
  
    
    

## <a name="friendly-urls-and-the-managed-navigation-provider"></a><span data-ttu-id="878a4-127">Полнотекстовые URL-адреса и поставщик управляемой навигации</span><span class="sxs-lookup"><span data-stu-id="878a4-127">Friendly URLs and the managed navigation provider</span></span>
<span data-ttu-id="878a4-128"><a name="SP15_ManagedNav_FriendlyURLs"> </a></span><span class="sxs-lookup"><span data-stu-id="878a4-128"><a name="SP15_ManagedNav_FriendlyURLs"> </a></span></span>

<span data-ttu-id="878a4-p105">Посетив сайт SharePoint в первый раз, вы можете заменить, что формат URL-адресов изменился. Вместо расширения  `/Pages/default.aspx` URL-адрес заканчивается символом `/`. Управляемая навигация предоставляет схему для полнотекстовых URL-адресов, согласованную на страницах сайтов, категорий и элементов.</span><span class="sxs-lookup"><span data-stu-id="878a4-p105">When you browse to a SharePoint site for the first time, you may notice that the URL format has changed. Instead of an address with a  `/Pages/default.aspx` extension, the page URL ends with only `/`. Managed navigation provides a scheme for friendly URLs that is consistent across site, category, and item pages.</span></span>
  
    
    
<span data-ttu-id="878a4-p106">Управляемая навигация позволяет создать такую среду. При переходе на корневую страницу любого сайта, использующего поставщика управляемой навигации, загружаемой страницей и ее внешним видом в браузере управляет параметр "Начальная страница сайта", но формат отображаемого URL-адреса (также показываемого в результатах поиска) меняется на более понятный.</span><span class="sxs-lookup"><span data-stu-id="878a4-p106">The managed navigation provider enables this experience. When you navigate to the root of any site that uses the managed navigation provider, the Site Welcome Page setting controls the page that's loaded and displayed in the browser, but the URL you see (and that appears in search results) is rewritten to this friendlier format.</span></span>
  
    
    
<span data-ttu-id="878a4-p107">У любой страницы, включая начальную страницу вашего сайта, может быть полнотекстовый URL-адрес. В зависимости от конфигурации сайта большинство страниц автоматически получают полнотекстовый URL-адрес. Полнотекстовые URL-адреса невозможно локализовать.</span><span class="sxs-lookup"><span data-stu-id="878a4-p107">Any page, including your site's Welcome Page, can have a friendly URL. Depending on how you configure your site, most pages automatically get a friendly URL. Friendly URLs can be localized.</span></span>
  
    
    

## <a name="managed-navigation-apis"></a><span data-ttu-id="878a4-137">Интерфейсы API управляемой навигации</span><span class="sxs-lookup"><span data-stu-id="878a4-137">Managed Navigation APIs</span></span>
<span data-ttu-id="878a4-138"><a name="SP15_ManagedNav_ManagedNavAPIs"> </a></span><span class="sxs-lookup"><span data-stu-id="878a4-138"><a name="SP15_ManagedNav_ManagedNavAPIs"> </a></span></span>

<span data-ttu-id="878a4-p108">API таксономии предоставляет несколько новых методов и свойств в SharePoint, которые можно использовать для настройки терминов, наборов терминов и других элементов метаданных в банке терминов, используемых в сценариях навигации сайта. Эти интерфейсы API доступны в моделях программирования клиента .NET, сервера .NET, Silverlight и JavaScript.</span><span class="sxs-lookup"><span data-stu-id="878a4-p108">The taxonomy API provides several new methods and properties in SharePoint that you can use to customize terms, term sets, and other metadata elements in the term store for use in site navigation scenarios. These APIs are available in the .NET client, .NET server, Silverlight, and JavaScript programming models.</span></span>
  
    
    

## <a name="code-example-customizing-managed-navigation-with-the-net-client-object-model-csom-api"></a><span data-ttu-id="878a4-141">Пример кода. Настройка управляемой навигации с API клиентской объектной модели .NET (CSOM)</span><span class="sxs-lookup"><span data-stu-id="878a4-141">Code Example: Customizing managed navigation with the .NET client object model (CSOM) API</span></span>
<span data-ttu-id="878a4-142"><a name="SP15_ManagedNav_CustomizingManagedNavWithNETCSOM"> </a></span><span class="sxs-lookup"><span data-stu-id="878a4-142"><a name="SP15_ManagedNav_CustomizingManagedNavWithNETCSOM"> </a></span></span>

<span data-ttu-id="878a4-143">При использовании клиентской объектной модели .NET для таксономии вы можете создать новый набор терминов навигации, если для текущего семейства веб-сайтов существует банк терминов, или преобразовать имеющийся набор терминов в набор, поддерживающий управляемую навигацию.</span><span class="sxs-lookup"><span data-stu-id="878a4-143">When you use the .NET client object model for taxonomy, you can create a new navigation term set if a term store exists for the current site collection, or convert an existing term set into one that supports managed navigation.</span></span>
  
    
    

  
    
    



```cs

///Create a navigation term set.
public class NavigationTermSetTests
    {
      public void CreateNavigationTermSet()
              {
               ClientContext clientContext = new ClientContext(TestConfig.ServerUrl);
            
                 TaxonomySession taxonomySession = TaxonomySession.GetTaxonomySession(clientContext);
                 taxonomySession.UpdateCache();

                 clientContext.Load(taxonomySession, ts => ts.TermStores);
                 clientContext.ExecuteQuery();

                 if (taxonomySession.TermStores.Count == 0)
                 throw new InvalidOperationException("The Taxonomy Service is offline or missing");

                 TermStore termStore = taxonomySession.TermStores[0];
                 clientContext.Load(termStore, 
                 ts => ts.Name, 
                 ts => ts.WorkingLanguage);

                 // Does the TermSet object already exist?
                 TermSet existingTermSet;

                 // Handles an error that occurs if the return value is null.
                 ExceptionHandlingScope exceptionScope = new ExceptionHandlingScope(clientContext);
             using (exceptionScope.StartScope())
                 {
                 using (exceptionScope.StartTry())
                 {
                 existingTermSet = termStore.GetTermSet(TestConfig.NavTermSetId);
                 }
                 using (exceptionScope.StartCatch())
                {
                }
                }
                clientContext.ExecuteQuery();

                if (!existingTermSet.ServerObjectIsNull.Value)
                {
                Log("CreateNavigationTermSet(): Deleting old TermSet");
                existingTermSet.DeleteObject();
                termStore.CommitAll();
                clientContext.ExecuteQuery();
                }

                Log("CreateNavigationTermSet(): Creating new TermSet");

               // Creates a new TermSet object.
            TermGroup siteCollectionGroup = termStore.GetSiteCollectionGroup(clientContext.Site, 
                createIfMissing: true);
            TermSet termSet = siteCollectionGroup.CreateTermSet("Navigation Demo", TestConfig.NavTermSetId, 
                termStore.WorkingLanguage);

            termStore.CommitAll();
            clientContext.ExecuteQuery();

            NavigationTermSet navTermSet = NavigationTermSet.GetAsResolvedByWeb(clientContext,
                termSet, clientContext.Web, "GlobalNavigationTaxonomyProvider");

            navTermSet.IsNavigationTermSet = true;
            navTermSet.TargetUrlForChildTerms.Value = "~site/Pages/Topics/Topic.aspx";

            termStore.CommitAll();
            clientContext.ExecuteQuery();

            NavigationTerm term1 = navTermSet.CreateTerm("Term 1", NavigationLinkType.SimpleLink, Guid.NewGuid());
            term1.SimpleLinkUrl = "http://www.bing.com/";

            Guid term2Guid = new Guid("87FAA433-4E3E-4500-AA5B-E04330B12ACD");
            NavigationTerm term2 = navTermSet.CreateTerm("Term 2", NavigationLinkType.FriendlyUrl,
                term2Guid);

            NavigationTerm childTerm = term2.CreateTerm("Term 2 child", NavigationLinkType.FriendlyUrl, Guid.NewGuid());

            childTerm.GetTaxonomyTerm().TermStore.CommitAll();
            clientContext.ExecuteQuery();
}


```


## <a name="code-example-customizing-managed-navigation-with-the-net-server-object-model-api"></a><span data-ttu-id="878a4-144">Пример кода. Настройка управляемой навигации с API серверной объектной модели .NET</span><span class="sxs-lookup"><span data-stu-id="878a4-144">Code Example: Customizing managed navigation with the .NET server object model API</span></span>
<span data-ttu-id="878a4-145"><a name="SP15_ManagedNav_CustomizingManagedNavNETServerObjectModel"> </a></span><span class="sxs-lookup"><span data-stu-id="878a4-145"><a name="SP15_ManagedNav_CustomizingManagedNavNETServerObjectModel"> </a></span></span>

<span data-ttu-id="878a4-146">Вы можете использовать серверные классы и методы таксономии .NET в пространствах имен  [Microsoft.SharePoint.Taxonomy](https://msdn.microsoft.com/library/Microsoft.SharePoint.Taxonomy.aspx) и [Microsoft.SharePoint.Publishing.Navigation](https://msdn.microsoft.com/library/Microsoft.SharePoint.Publishing.Navigation.aspx) , чтобы создать новый набор терминов навигации.</span><span class="sxs-lookup"><span data-stu-id="878a4-146">You can use the .NET server taxonomy classes and methods in the  [Microsoft.SharePoint.Taxonomy](https://msdn.microsoft.com/library/Microsoft.SharePoint.Taxonomy.aspx) and [Microsoft.SharePoint.Publishing.Navigation](https://msdn.microsoft.com/library/Microsoft.SharePoint.Publishing.Navigation.aspx) namespaces to create a new navigation term set.</span></span>
  
    
    

  
    
    



```cs

///Create a navigation term set.
using (SPSite site = new SPSite(TestConfig.ServerUrl))
            {
                using (SPWeb web = site.OpenWeb())
                {
                    TaxonomySession taxonomySession = new TaxonomySession(site, updateCache: true);

                    /// Use the first TermStore object in the list.
                    if (taxonomySession.TermStores.Count == 0)
                        throw new InvalidOperationException("The Taxonomy Service is offline or missing");

                    TermStore termStore = taxonomySession.TermStores[0];

                    /// Does the TermSet object already exist?
                    TermSet existingTermSet = termStore.GetTermSet(TestConfig.NavTermSetId);
                    if (existingTermSet != null)
                    {
                        Log("CreateNavigationTermSet(): Deleting old TermSet");
                        existingTermSet.Delete();
                        termStore.CommitAll();
                    }

                    Log("CreateNavigationTermSet(): Creating new TermSet");

                    /// Create a new TermSet object.
                    Group siteCollectionGroup = termStore.GetSiteCollectionGroup(site);
                    TermSet termSet = siteCollectionGroup.CreateTermSet("Navigation Demo", TestConfig.NavTermSetId);

                    NavigationTermSet navTermSet = NavigationTermSet.GetAsResolvedByWeb(termSet, web,
                        StandardNavigationProviderNames.GlobalNavigationTaxonomyProvider);

                    navTermSet.IsNavigationTermSet = true;
                    navTermSet.TargetUrlForChildTerms.Value = "~site/Pages/Topics/Topic.aspx";

                    NavigationTerm term1 = navTermSet.CreateTerm("Term 1", NavigationLinkType.SimpleLink);
                    term1.SimpleLinkUrl = "http://www.bing.com/";

                    Guid term2Guid = new Guid("87FAA433-4E3E-4500-AA5B-E04330B12ACD");
                    NavigationTerm term2 = navTermSet.CreateTerm("Term 2", NavigationLinkType.FriendlyUrl,
                        term2Guid);

                    /// Verify that the NavigationTermSetView is being applied correctly.
                    Assert.AreEqual(web.ServerRelativeUrl + "/term-2", term2.GetResolvedDisplayUrl(null).ToString());

                    string expectedTargetUrl = web.ServerRelativeUrl 
                        + "/Pages/Topics/Topic.aspx?TermStoreId=" + termStore.Id.ToString() 
                        + "&amp;TermSetId=" + TestConfig.NavTermSetId.ToString()
                        + "&amp;TermId=" + term2Guid.ToString();
                    Assert.AreEqual(expectedTargetUrl, term2.GetResolvedTargetUrl(null, null).ToString());

                    NavigationTerm childTerm = term2.CreateTerm("Term 2 child", NavigationLinkType.FriendlyUrl);
                    Assert.AreEqual(web.ServerRelativeUrl + "/term-2/term-2-child", childTerm.GetResolvedDisplayUrl(null).ToString());

                    /// Commit changes.
                    childTerm.GetTaxonomyTerm().TermStore.CommitAll();
                }
            }
```


## <a name="additional-resources"></a><span data-ttu-id="878a4-147">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="878a4-147">Additional resources</span></span>
<span data-ttu-id="878a4-148"><a name="SP15_ManagedNav_AdditionalResources"> </a></span><span class="sxs-lookup"><span data-stu-id="878a4-148"><a name="SP15_ManagedNav_AdditionalResources"> </a></span></span>


-  [<span data-ttu-id="878a4-149">Веб-часть поиска контента в SharePoint</span><span class="sxs-lookup"><span data-stu-id="878a4-149">Content Search Web Part in SharePoint</span></span>](content-search-web-part-in-sharepoint.md)
    
  

