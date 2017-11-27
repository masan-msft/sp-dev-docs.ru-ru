---
title: "Задает использовать код с условиями ПИН-кода для терминов навигации в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 4a2811dc-25fd-4eb2-b0ab-1edded64c556
ms.openlocfilehash: c04261b5106e2c66a308b0f96afd09b2065e41d4
ms.sourcegitcommit: f6ea922341c38e700d0697961f8df9a454a03cba
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/15/2017
---
# <a name="use-code-to-pin-terms-to-navigation-term-sets-in-sharepoint"></a>Задает использовать код с условиями ПИН-кода для терминов навигации в SharePoint

Узнайте, как использовать код, чтобы закрепить термины в наборах терминов навигации.

В разделе Создание таксономии фиксации — это возможность подключать терминов в целевой. SharePoint представляется фиксации терминов. Закрепленные терминов — так же, как условие, которое используется повторно, за исключением того, как он доступен только для чтения и не может изменяться в расположение, где используется термин.

В области навигации управляемых API позволяет ПИН-код нового или существующего условия [NavigationTermSet](https://msdn.microsoft.com/library/Microsoft.SharePoint.Publishing.Navigation.NavigationTermSet.aspx) объект. В Microsoft SharePoint Server 2010 пользователи могли бы повторно использовать условия (и всех вложенных в повторно используемую условия) в другие расположения в иерархии терминов. После того как эти термины, которые использовались повторно, может быть изменено в любом месте и изменения будут видны везде термины, которые использовались повторно.

## <a name="term-pinning-essentials"></a>Закрепленным essentials терминов
<a name="SP15_H2UseCodeToPinTerms_TermPinningEssentials"> </a>

Чтобы понять, фиксации в SharePoint, может потребоваться сведения об управляемых метаданных, терминов, наборов терминов, управляемых навигации, банк терминов и другие связанные понятия и API-интерфейсы. В таблице 1 описаны статьи, в которых представлены дополнительные сведения о фиксации. 
  
    
    

**В таблице 1. Основные понятия, которые для фиксации**


|**Название статьи**|**Описание**|
|:-----|:-----|
| [Краткое введение в компоненты Enterprise Metadata Management для разработчиков Microsoft SharePoint Server 2010](http://msdn.microsoft.com/library/113a5d75-ac4d-498b-8436-725e04fb685d%28Office.15%29.aspx) <br/> |Написана для SharePoint Server 2010 в этой статье приводятся общие сведения о корпоративных управляемых метаданных, программирование модели, а также основными понятиями, такие как терминов и наборов терминов.  <br/> |
| [Управляемой навигации в SharePoint](managed-navigation-in-sharepoint.md) <br/> |Общие сведения о функции на основе таксономии управляемой навигации в SharePoint.  <br/> |
   

## <a name="use-code-to-complete-pinning-tasks"></a>Использовать код для выполнения задач, закрепленным
<a name="SP15_H2UseCodeToPinTerms_UseCodeToCompletePinning"> </a>

Можно использовать пользовательский код из .NET server, .NET клиента (CSOM), Silverlight или JavaScript моделей программирования для выполнения операций закрепленным на терминов и наборов терминов. В следующих примерах кода .NET server включить проверку закрепленным терминов для наборов терминов навигации и метод, который можно использовать для проверки, является ли указанный **TermSet** объект закреплен объект **Term**. Затем тест создает объекты **Term** и один из них объект указанного **NavigationTermSet** ПИН-код.
  
    
    

### <a name="to-pin-terms-to-navigation-term-sets"></a>Закрепление терминов для навигации по наборам терминов


- Следующий пример проверяет закрепленным терминов в наборах терминов навигации. Он использует объект  [NavigationTermSet](https://msdn.microsoft.com/library/Microsoft.SharePoint.SharePoint.NavigationTermSet.aspx) , который содержит методы и свойства, которые удобны в сценарии управляемой навигации, такие как создание сайт на основе таксономии меню навигации.
    
    Пример сначала проверяет, существует ли объект **NavigationTermSet**. Если он не существует, код создает **NavigationTermSet**. (Если он уже существует, код удаляет старый перед созданием новой). Затем после код создает некоторые объекты **Term**, чтобы выбрать нужное, его создает файл публикации страницы (ASPX) в целях демонстрации, устанавливает в качестве настраиваемого конечной страницы для закрепленных соглашения и затем ПИН-код некоторые свойства навигации на страницу.
    


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


## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="SP15_H2UseCodeToPinTerms_AdditionalResources"> </a>


-  [Управляемые метаданные и навигация в SharePoint](managed-metadata-and-navigation-in-sharepoint.md)
    
  
-  [Microsoft.SharePoint.Publishing.Navigation](https://msdn.microsoft.com/library/Microsoft.SharePoint.Publishing.Navigation.aspx)
    
  

