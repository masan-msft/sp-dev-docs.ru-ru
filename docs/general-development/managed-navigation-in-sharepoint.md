
# <a name="managed-navigation-in-sharepoint"></a>Управляемая навигация в SharePoint

  
    
    
![Раздел концептуального обзора](../../images/mod_icon_badge_conoverview.png)
  
    
    

  
    
    

  
    
    
Сведения о функции управляемой навигации на основе таксономии в SharePoint.
## <a name="introducing-managed-navigation"></a>Общие сведения об управляемой навигации
<a name="SP15_ManagedNav_Introducing"> </a>

Хорошо спланированная навигация поможет пользователям узнать о вашем предприятии, продукции и службах, предоставляемых веб-сайтом. Обновив таксономию навигации, предприятия могут стимулировать и подстраиваться под перемены, не переделывая навигацию своего сайта. Функция управляемой навигации в SharePoint позволяет разработать навигацию сайта на основе управляемых метаданных и создавать оптимизированные для поисковых систем URL-адреса, основанные на структуре управляемой навигации. Управляемая навигация является альтернативой традиционной (структурированной) навигации SharePoint, основанной на структуре SharePoint. Так как управляемая навигация основана на таксономии, ее можно использовать, чтобы разработать навигацию сайта с учетом важных бизнес-концепций, не меняя структуру сайтов и их компонентов.
  
    
    

## <a name="how-managed-navigation-works"></a>Принцип работы управляемой навигации
<a name="SP15_ManagedNav_HowManagedNavWorks"> </a>

Управляемая навигация предоставляет платформу для динамически создаваемых страниц и связанного URL-адреса, оптимизированного для поисковых систем. Каждая созданная страница представлена в иерархии навигации. Чтобы для каждой категории таксономии не требовалось создавать отдельные страницы, эта платформа предоставляет механизм шаблонов и наследования, который создает страницы для каждой навигационной ссылки. Вы можете использовать функцию тематических страниц, чтобы настраивать внешний вид этих страниц.
  
    
    
Интерфейсы API управляемой навигации встроены в компоненты таксономии и публикации SharePoint. Такие компоненты управляемых метаданных, как наборы терминов и банк терминов, используются, чтобы сайт поддерживал навигацию на основе таксономии. В серверной библиотеке классов .NET пространство имен  [Microsoft.SharePoint.Publishing.Navigation](https://msdn.microsoft.com/library/Microsoft.SharePoint.Publishing.Navigation.aspx) содержит термины, наборы терминов и другие объекты классов, которые дублируют классы **Term** и **TermSet** в пространстве имен навигации [Microsoft.SharePoint.Taxonomy](https://msdn.microsoft.com/library/Microsoft.SharePoint.Taxonomy.aspx) , предоставляя методы и свойства, разработанные специально для связывания этих метаданных с элементами навигации. Другие классы, например [TaxonomySiteMapNode](https://msdn.microsoft.com/library/Microsoft.SharePoint.Publishing.Navigation.TaxonomySiteMapNode.aspx) , позволяют предоставлять метаданные с различными элементами навигации сайта, например узлами карты сайта и другими элементами навигации сайта. Другие классы позволяют использовать кэширование и контекст для управляемой навигации.
  
    
    
В глобальной навигации могут отображаться ссылки навигации на основе таксономии. Глобальная навигация  это уровень навигации с одним или несколькими слоями, который всегда присутствует, обычно отображается в верхней части сайта и отображает категории контента верхнего уровня. Эти ссылки также могут отображаться в текущем элементе управления навигации, который часто отображается в левой части страницы. Текущий элемент управления навигации представляет следующий уровень иерархии для категории, выбранной в глобальной навигации, или набор ссылок, принадлежащих к этой категории.
  
    
    

## <a name="friendly-urls-and-the-managed-navigation-provider"></a>Полнотекстовые URL-адреса и поставщик управляемой навигации
<a name="SP15_ManagedNav_FriendlyURLs"> </a>

Посетив сайт SharePoint в первый раз, вы можете заменить, что формат URL-адресов изменился. Вместо расширения  `/Pages/default.aspx` URL-адрес заканчивается символом `/`. Управляемая навигация предоставляет схему для полнотекстовых URL-адресов, согласованную на страницах сайтов, категорий и элементов.
  
    
    
Управляемая навигация позволяет создать такую среду. При переходе на корневую страницу любого сайта, использующего поставщика управляемой навигации, загружаемой страницей и ее внешним видом в браузере управляет параметр "Начальная страница сайта", но формат отображаемого URL-адреса (также показываемого в результатах поиска) меняется на более понятный.
  
    
    
У любой страницы, включая начальную страницу вашего сайта, может быть полнотекстовый URL-адрес. В зависимости от конфигурации сайта большинство страниц автоматически получают полнотекстовый URL-адрес. Полнотекстовые URL-адреса невозможно локализовать.
  
    
    

## <a name="managed-navigation-apis"></a>Интерфейсы API управляемой навигации
<a name="SP15_ManagedNav_ManagedNavAPIs"> </a>

API таксономии предоставляет несколько новых методов и свойств в SharePoint, которые можно использовать для настройки терминов, наборов терминов и других элементов метаданных в банке терминов, используемых в сценариях навигации сайта. Эти интерфейсы API доступны в моделях программирования клиента .NET, сервера .NET, Silverlight и JavaScript.
  
    
    

## <a name="code-example-customizing-managed-navigation-with-the-net-client-object-model-csom-api"></a>Пример кода. Настройка управляемой навигации с API клиентской объектной модели .NET (CSOM)
<a name="SP15_ManagedNav_CustomizingManagedNavWithNETCSOM"> </a>

При использовании клиентской объектной модели .NET для таксономии вы можете создать новый набор терминов навигации, если для текущего семейства веб-сайтов существует банк терминов, или преобразовать имеющийся набор терминов в набор, поддерживающий управляемую навигацию.
  
    
    

  
    
    



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


## <a name="code-example-customizing-managed-navigation-with-the-net-server-object-model-api"></a>Пример кода. Настройка управляемой навигации с API серверной объектной модели .NET
<a name="SP15_ManagedNav_CustomizingManagedNavNETServerObjectModel"> </a>

Вы можете использовать серверные классы и методы таксономии .NET в пространствах имен  [Microsoft.SharePoint.Taxonomy](https://msdn.microsoft.com/library/Microsoft.SharePoint.Taxonomy.aspx) и [Microsoft.SharePoint.Publishing.Navigation](https://msdn.microsoft.com/library/Microsoft.SharePoint.Publishing.Navigation.aspx) , чтобы создать новый набор терминов навигации.
  
    
    

  
    
    



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


## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="SP15_ManagedNav_AdditionalResources"> </a>


-  [Веб-часть поиска контента в SharePoint](content-search-web-part-in-sharepoint)
    
  

