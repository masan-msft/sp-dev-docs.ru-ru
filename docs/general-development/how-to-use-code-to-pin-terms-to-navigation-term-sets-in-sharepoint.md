---
title: "Закрепление терминов в наборах терминов навигации в SharePoint с помощью кода"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 4a2811dc-25fd-4eb2-b0ab-1edded64c556
ms.openlocfilehash: 477311aeba990eebf85157f04ae2380f135f297b
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="use-code-to-pin-terms-to-navigation-term-sets-in-sharepoint"></a><span data-ttu-id="85416-102">Закрепление терминов в наборах терминов навигации в SharePoint с помощью кода</span><span class="sxs-lookup"><span data-stu-id="85416-102">Use code to pin terms to navigation term sets in SharePoint</span></span>

<span data-ttu-id="85416-103">Узнайте, как использовать код, чтобы закрепить термины в наборах терминов навигации.</span><span class="sxs-lookup"><span data-stu-id="85416-103">Learn how to use code to pin terms to navigation term sets.</span></span>

<span data-ttu-id="85416-104">В разделе Создание таксономии фиксации — это возможность подключать терминов в целевой.</span><span class="sxs-lookup"><span data-stu-id="85416-104">In taxonomy creation, pinning is the ability to attach a term to a target.</span></span> <span data-ttu-id="85416-105">SharePoint представляется фиксации терминов.</span><span class="sxs-lookup"><span data-stu-id="85416-105">SharePoint introduces term pinning.</span></span> <span data-ttu-id="85416-106">Закрепленные терминов — так же, как условие, которое используется повторно, за исключением того, как он доступен только для чтения и не может изменяться в расположение, где используется термин.</span><span class="sxs-lookup"><span data-stu-id="85416-106">A pinned term is just like a term that is reused, except it is read-only and cannot be changed in the location where the term is used.</span></span>

<span data-ttu-id="85416-107">В области навигации управляемых API позволяет ПИН-код нового или существующего условия [NavigationTermSet](https://msdn.microsoft.com/library/Microsoft.SharePoint.Publishing.Navigation.NavigationTermSet.aspx) объект.</span><span class="sxs-lookup"><span data-stu-id="85416-107">In SharePoint managed navigation, the API enables you to pin new or existing terms to a  [NavigationTermSet](https://msdn.microsoft.com/library/Microsoft.SharePoint.Publishing.Navigation.NavigationTermSet.aspx) object.</span></span> <span data-ttu-id="85416-108">В Microsoft SharePoint Server 2010 пользователи могли бы повторно использовать условия (и всех вложенных в повторно используемую условия) в другие расположения в иерархии терминов.</span><span class="sxs-lookup"><span data-stu-id="85416-108">In Microsoft SharePoint Server 2010, users could reuse terms (and all terms nested under the reused terms) in other locations in the term hierarchy.</span></span> <span data-ttu-id="85416-109">После того как эти термины, которые использовались повторно, может быть изменено в любом месте и изменения будут видны везде термины, которые использовались повторно.</span><span class="sxs-lookup"><span data-stu-id="85416-109">After these terms were reused, they could be modified in any location and changes would be seen everywhere the terms were reused.</span></span>

## <a name="term-pinning-essentials"></a><span data-ttu-id="85416-110">Закрепленным essentials терминов</span><span class="sxs-lookup"><span data-stu-id="85416-110">Term pinning essentials</span></span>
<span data-ttu-id="85416-111"><a name="SP15_H2UseCodeToPinTerms_TermPinningEssentials"> </a></span><span class="sxs-lookup"><span data-stu-id="85416-111"></span></span>

<span data-ttu-id="85416-112">Чтобы понять, фиксации в SharePoint, может потребоваться сведения об управляемых метаданных, терминов, наборов терминов, управляемых навигации, банк терминов и другие связанные понятия и API-интерфейсы.</span><span class="sxs-lookup"><span data-stu-id="85416-112">To understand pinning in SharePoint, you may want to learn about managed metadata, terms, term sets, managed navigation, the term store, and other related concepts and APIs.</span></span> <span data-ttu-id="85416-113">В таблице 1 описаны статьи, в которых представлены дополнительные сведения о фиксации.</span><span class="sxs-lookup"><span data-stu-id="85416-113">Table 1 describes articles that give more information about pinning.</span></span> 
  
    
    

<span data-ttu-id="85416-114">**В таблице 1. Основные понятия, которые для фиксации**</span><span class="sxs-lookup"><span data-stu-id="85416-114">**Table 1. Core concepts for pinning**</span></span>


|<span data-ttu-id="85416-115">**Название статьи**</span><span class="sxs-lookup"><span data-stu-id="85416-115">**Article title**</span></span>|<span data-ttu-id="85416-116">**Описание**</span><span class="sxs-lookup"><span data-stu-id="85416-116">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="85416-117">Краткое введение в компоненты Enterprise Metadata Management для разработчиков Microsoft SharePoint Server 2010</span><span class="sxs-lookup"><span data-stu-id="85416-117">A Brief Introduction to Enterprise Metadata Management for Microsoft SharePoint Server 2010 Developers</span></span>](http://msdn.microsoft.com/library/113a5d75-ac4d-498b-8436-725e04fb685d%28Office.15%29.aspx) <br/> |<span data-ttu-id="85416-118">Написана для SharePoint Server 2010 в этой статье приводятся общие сведения о корпоративных управляемых метаданных, программирование модели, а также основными понятиями, такие как терминов и наборов терминов.</span><span class="sxs-lookup"><span data-stu-id="85416-118">Written for SharePoint Server 2010, this article provides a basic overview of the enterprise managed metadata programming model and core concepts, such as terms and term sets.</span></span>  <br/> |
| [<span data-ttu-id="85416-119">Управляемой навигации в SharePoint</span><span class="sxs-lookup"><span data-stu-id="85416-119">Managed navigation in SharePoint</span></span>](managed-navigation-in-sharepoint.md) <br/> |<span data-ttu-id="85416-120">Общие сведения о функции на основе таксономии управляемой навигации в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="85416-120">An introduction to the taxonomy-driven managed navigation feature in SharePoint.</span></span>  <br/> |
   

## <a name="use-code-to-complete-pinning-tasks"></a><span data-ttu-id="85416-121">Использовать код для выполнения задач, закрепленным</span><span class="sxs-lookup"><span data-stu-id="85416-121">Use code to complete pinning tasks</span></span>
<span data-ttu-id="85416-122"><a name="SP15_H2UseCodeToPinTerms_UseCodeToCompletePinning"> </a></span><span class="sxs-lookup"><span data-stu-id="85416-122"></span></span>

<span data-ttu-id="85416-p104">Можно использовать пользовательский код из .NET server, .NET клиента (CSOM), Silverlight или JavaScript моделей программирования для выполнения операций закрепленным на терминов и наборов терминов. В следующих примерах кода .NET server включить проверку закрепленным терминов для наборов терминов навигации и метод, который можно использовать для проверки, является ли указанный **TermSet** объект закреплен объект **Term**. Затем тест создает объекты **Term** и один из них объект указанного **NavigationTermSet** ПИН-код.</span><span class="sxs-lookup"><span data-stu-id="85416-p104">You can use custom code from the .NET server, .NET client (CSOM), Silverlight, or JavaScript programming models to complete pinning operations on terms and term sets. The following .NET server code examples include a test for pinning terms to navigation term sets, and a method that you can use to test whether a **Term** object is pinned to a specified **TermSet** object. Then, the test creates **Term** objects, and pins one of them to the specified **NavigationTermSet** object.</span></span>
  
    
    

### <a name="to-pin-terms-to-navigation-term-sets"></a><span data-ttu-id="85416-126">Закрепление терминов для навигации по наборам терминов</span><span class="sxs-lookup"><span data-stu-id="85416-126">To pin terms to navigation term sets</span></span>


- <span data-ttu-id="85416-p105">Следующий пример проверяет закрепленным терминов в наборах терминов навигации. Он использует объект  [NavigationTermSet](https://msdn.microsoft.com/library/Microsoft.SharePoint.SharePoint.NavigationTermSet.aspx) , который содержит методы и свойства, которые удобны в сценарии управляемой навигации, такие как создание сайт на основе таксономии меню навигации.</span><span class="sxs-lookup"><span data-stu-id="85416-p105">The following sample tests pinning terms to navigation term sets. It uses the  [NavigationTermSet](https://msdn.microsoft.com/library/Microsoft.SharePoint.SharePoint.NavigationTermSet.aspx) object, which contains methods and properties that are handy in managed navigation scenarios, such as creating taxonomy-driven site navigation menus.</span></span>
    
    <span data-ttu-id="85416-p106">Пример сначала проверяет, существует ли объект **NavigationTermSet**. Если он не существует, код создает **NavigationTermSet**. (Если он уже существует, код удаляет старый перед созданием новой). Затем после код создает некоторые объекты **Term**, чтобы выбрать нужное, его создает файл публикации страницы (ASPX) в целях демонстрации, устанавливает в качестве настраиваемого конечной страницы для закрепленных соглашения и затем ПИН-код некоторые свойства навигации на страницу.</span><span class="sxs-lookup"><span data-stu-id="85416-p106">The sample first checks whether a **NavigationTermSet** object exists. If one doesn't exist, then the code creates a **NavigationTermSet**. (If one already exists, the code deletes the old one before it creates a new one). Then, after the code creates some **Term** objects to pick from, it creates a publishing page (.aspx) file for demonstration purposes, sets it as the custom target page for pinned terms, and then pins some navigation properties to the page.</span></span>
    


```cs
  
public void TermPinningTest()
        {
using (SPSite site = new SPSite(TestConfig.ServerUrl))
            {
                using (SPWeb web = site.OpenWeb())
                {
                    TaxonomySession taxonomySession = new TaxonomySession(site, updateCache: true);

                    // Create the navigation term set.
                    NavigationTermSet menuNavTermSet = DemoUtilities.SetUpSampleNavTermSet(
                        this.TestContext, taxonomySession, web);
                    TermSet menuTaxTermSet = menuNavTermSet.GetTaxonomyTermSet();

                    TermStore termStore = menuTaxTermSet.TermStore;
                    Group group = menuTaxTermSet.Group;

                    // Does the tagging Taxonomy term set already exist?
                    TermSet taggingTaxTermSet = group.TermSets.FirstOrDefault(
                        ts => ts.Id == TestConfig.TaggingTermSetId);

                    if (taggingTaxTermSet != null)
                    {
                        Log("Deleting old tagging term set");

                        // If the tagging Taxonomy term set already exists, delete the old one.
                        taggingTaxTermSet.Delete();
                        termStore.CommitAll();
                    }

                    Log("Creating the tagging term set");

                    taggingTaxTermSet = group.CreateTermSet("Demo Tagging TermSet", TestConfig.TaggingTermSetId);

                    int lcid = termStore.WorkingLanguage;

                    // Create some terms.
                    Term taggingProductsTaxTerm = taggingTaxTermSet.CreateTerm("Products", lcid);
                    taggingProductsTaxTerm.CreateTerm("Electronics", lcid);
                    taggingProductsTaxTerm.CreateTerm("Footwear", lcid);
                    taggingProductsTaxTerm.CreateTerm("Sports", lcid);

                    termStore.CommitAll();

                    /// Pinning the products subtree. Pins the "Products" Term object to the NavigationTermSet object.
                    Term menuProductsTaxTerm = menuTaxTermSet.ReuseTermWithPinning(taggingProductsTaxTerm);
                    termStore.CommitAll();

                    /// Creating the publishing page template DemoTargetPage.aspx");
                    PublishingWeb publishingWeb = PublishingWeb.GetPublishingWeb(web);

                    SPListItem pageListItem = null;
                    PublishingPage publishingPage;
                    try
                    {
                        pageListItem = web.GetListItem(web.Url + "/Pages/DemoTargetPage.aspx");
                        publishingPage = PublishingPage.GetPublishingPage(pageListItem);
   
                    }
                    catch (FileNotFoundException)
                    {
                        Log("Creating new target page");
                        publishingPage = publishingWeb.AddPublishingPage("DemoTargetPage.aspx", publishingWeb.DefaultPageLayout);
                        Log("Checking in target page draft");
                        publishingPage.CheckIn("TermPinningTest");
                    }

                    // Set a custom target page for the pinned terms and then set some navigation properties.

                    // Normally the navigation objects are obtained by way of an optimized function such as
                    // TaxonomyNavigation.GetTermSetForWeb() or TaxonomyNavigationContext.Current.NavigationTerm.
                    // The function guarantees that URLs will be resolved using a valid NavigationTerm.View.
                    // But because we are populating totally new data, the cache will probably not be updated
                    // yet, so instead we manually construct a view using GetAsResolvedByWeb().
                    NavigationTerm menuProductsNavTerm = NavigationTerm.GetAsResolvedByWeb(menuProductsTaxTerm,
                        web, StandardNavigationProviderNames.GlobalNavigationTaxonomyProvider);

                    menuProductsNavTerm.TargetUrl.Value = publishingPage.Uri.AbsolutePath;
                    menuProductsNavTerm.TargetUrlForChildTerms.Value = publishingPage.Uri.AbsolutePath;

                    termStore.CommitAll();

                    Log("TermPinningTest completed successfully");
                }
            }

}
```


## <a name="see-also"></a><span data-ttu-id="85416-133">См. также</span><span class="sxs-lookup"><span data-stu-id="85416-133">See also</span></span>
<span data-ttu-id="85416-134"><a name="SP15_H2UseCodeToPinTerms_AdditionalResources"> </a></span><span class="sxs-lookup"><span data-stu-id="85416-134"></span></span>


-  [<span data-ttu-id="85416-135">Управляемые метаданные и навигация в SharePoint</span><span class="sxs-lookup"><span data-stu-id="85416-135">Managed metadata and navigation in SharePoint</span></span>](managed-metadata-and-navigation-in-sharepoint.md)
    
  
-  [<span data-ttu-id="85416-136">Microsoft.SharePoint.Publishing.Navigation</span><span class="sxs-lookup"><span data-stu-id="85416-136">Microsoft.SharePoint.Publishing.Navigation</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.Publishing.Navigation.aspx)
    
  

