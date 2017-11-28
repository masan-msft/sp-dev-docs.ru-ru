---
title: "Использование API поиска в объектная модель SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: c4ad4850f8e76ddf2933981ce550a141bf75d792
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
<a name="search-api-usage-in-the-sharepoint-add-in-model"></a><span data-ttu-id="4619c-102">Использование API поиска в объектная модель SharePoint</span><span class="sxs-lookup"><span data-stu-id="4619c-102">Search API usage in the SharePoint add-in model</span></span>
===============================================

<a name="summary"></a><span data-ttu-id="4619c-103">Summary</span><span class="sxs-lookup"><span data-stu-id="4619c-103">Summary</span></span>
-------

<span data-ttu-id="4619c-104">Подхода, можно выполнить поиск с помощью службы поиска SharePoint будет разным в новой модели надстройки SharePoint не был с кодом полного доверия.</span><span class="sxs-lookup"><span data-stu-id="4619c-104">The approach you take to execute searches with the SharePoint Search Service is different in the new SharePoint Add-in model than it was with Full Trust Code.</span></span>  <span data-ttu-id="4619c-105">В типичных полного доверия кода (FTC) сценарий решения фермы, на сервере объектной модели SharePoint (с запроса веб-части содержимого переопределений) или веб-службы поиска были, используемой для выполнения операций поиска с помощью службы поиска SharePoint.</span><span class="sxs-lookup"><span data-stu-id="4619c-105">In a typical Full Trust Code (FTC) / Farm Solution scenario, the SharePoint server-side object model (Content By Query Web Part overrides) or the Search Web Services were used to execute searches with the SharePoint Search Service.</span></span>

<span data-ttu-id="4619c-106">В модели сценарий надстройки SharePoint выполнение операций поиска с помощью службы поиска SharePoint с помощью CSOM или API-интерфейсы REST.</span><span class="sxs-lookup"><span data-stu-id="4619c-106">In a SharePoint Add-in model scenario, you execute searches with the SharePoint Search Service via the CSOM or REST APIs.</span></span>

<a name="high-level-guidelines"></a><span data-ttu-id="4619c-107">Рекомендации по высокого уровня</span><span class="sxs-lookup"><span data-stu-id="4619c-107">High Level Guidelines</span></span>
---------------------

<span data-ttu-id="4619c-108">Как правило эскиз мы предлагаем для обеспечения высокого уровня следующее Создание и настройка семейств веб-сайтов и sub сайтам затем развертывание артефактов, конфигураций и фирменной настройки ресурсов.</span><span class="sxs-lookup"><span data-stu-id="4619c-108">As a rule of a thumb, we would like to provide the following high level guidelines to create and configure site collections and sub sites then deploy artifacts, configurations, and branding assets to them.</span></span>

- <span data-ttu-id="4619c-109">С помощью AppOnly проверки подлинности не поддерживается для любых операций службы поиска.</span><span class="sxs-lookup"><span data-stu-id="4619c-109">Using AppOnly authentication is not supported for any Search Service operations.</span></span>
    + <span data-ttu-id="4619c-110">Это из-за того, что служба поиска обращается к службе профилей пользователей (UPS) для поиска сведений профиля пользователя и ИБП не поддерживает проверку подлинности AppOnly.</span><span class="sxs-lookup"><span data-stu-id="4619c-110">This is due to the fact that the Search Service accesses the User Profile Service (UPS) to search user profile information and the UPS does not support AppOnly authentication.</span></span>
    + <span data-ttu-id="4619c-111">Таким образом так как их профилей атрибуты AppOnly, шаблон проверки подлинности не будет работать и релевантности поиска и другие аспекты поиска в зависимости от определенного пользователя.</span><span class="sxs-lookup"><span data-stu-id="4619c-111">Therefore, because search relevance and other search facets depend on a given user and their profile attributes the AppOnly authentication pattern will not work.</span></span>

<a name="options-to-execute-searches-with-the-sharepoint-search-service"></a><span data-ttu-id="4619c-112">Параметры, чтобы выполнить поиск с помощью службы поиска SharePoint</span><span class="sxs-lookup"><span data-stu-id="4619c-112">Options to execute searches with the SharePoint Search Service</span></span>
--------------------------------------------------------------

<span data-ttu-id="4619c-113">У вас есть coupe из параметров, чтобы выполнить поиск с помощью службы поиска SharePoint.</span><span class="sxs-lookup"><span data-stu-id="4619c-113">You have a coupe of options to execute searches with the SharePoint Search Service.</span></span>

- <span data-ttu-id="4619c-114">API-Интерфейс .net CSOM</span><span class="sxs-lookup"><span data-stu-id="4619c-114">.Net CSOM API</span></span>
- <span data-ttu-id="4619c-115">API CSOM JavaScript (JSOM)</span><span class="sxs-lookup"><span data-stu-id="4619c-115">JavaScript CSOM (JSOM) API</span></span>
- <span data-ttu-id="4619c-116">API-ИНТЕРФЕЙС REST</span><span class="sxs-lookup"><span data-stu-id="4619c-116">REST API</span></span>  

<a name="net-csom-api"></a><span data-ttu-id="4619c-117">API-Интерфейс .net CSOM</span><span class="sxs-lookup"><span data-stu-id="4619c-117">.Net CSOM API</span></span>
-------------
<span data-ttu-id="4619c-118">В этом параметре используется API-Интерфейс .net CSOM для выполнения операций поиска с помощью службы поиска SharePoint.</span><span class="sxs-lookup"><span data-stu-id="4619c-118">In this option you use the .Net CSOM API to execute searches with the SharePoint Search Service.</span></span>
    
- <span data-ttu-id="4619c-119">Этот интерфейс API доступна только в управляемом коде .net.</span><span class="sxs-lookup"><span data-stu-id="4619c-119">This API is only available in managed .Net code.</span></span>


<span data-ttu-id="4619c-120">**Когда это подходит?**</span><span class="sxs-lookup"><span data-stu-id="4619c-120">**When is it a good fit?**</span></span>

- <span data-ttu-id="4619c-121">Этот интерфейс API является отлично подходит для Add-ins, размещаемые у поставщика, длительной операции или других сценариях на сервере, на которых выполняется на платформе .net.</span><span class="sxs-lookup"><span data-stu-id="4619c-121">This API is a great fit for Provider-hosted Add-ins, long running operations, or other server-side scenarios that run on the .Net platform.</span></span>
- <span data-ttu-id="4619c-122">Некоторые примеры этих сценариев, ASP.NET MVC веб-сайтов, ASP.NET Web API services, консоли .net или приложений Windows и задания Web Azure.</span><span class="sxs-lookup"><span data-stu-id="4619c-122">Some examples of these scenarios are ASP.NET MVC web sites, ASP.NET Web API services, .Net console or Windows applications, and Azure Web Jobs.</span></span>

<span data-ttu-id="4619c-123">**Приступая к работе**</span><span class="sxs-lookup"><span data-stu-id="4619c-123">**Getting Started**</span></span>

<span data-ttu-id="4619c-124">Следующий пример демонстрирует выполнение операций поиска с помощью службы поиска SharePoint с помощью API-Интерфейс .net CSOM.</span><span class="sxs-lookup"><span data-stu-id="4619c-124">The following sample demonstrates how to execute searches with the SharePoint Search Service with the .Net CSOM API.</span></span>  <span data-ttu-id="4619c-125">В этом примере также показано, как получить доступ к профиля пользователя для индивидуальной настройки результатов поиска.</span><span class="sxs-lookup"><span data-stu-id="4619c-125">This example also demonstrates how to access a user's profile to personalize the search results.</span></span>

- [<span data-ttu-id="4619c-126">Search.PersonalizedResults (O365 PnP образец)</span><span class="sxs-lookup"><span data-stu-id="4619c-126">Search.PersonalizedResults (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Search.PersonalizedResults)

![Страница API поиска и личных настроек.](media/Recipes/SearchAPI/Search.PersonalizedResults.png)

<span data-ttu-id="4619c-137">[Порядок выполнения индивидуально настроенных поисковых запросов с помощью CSOM (O365 PnP видео)](https://channel9.msdn.com/blogs/OfficeDevPnP/How-to-perform-personalized-search-queries-with-CSOM) — описание [Search.PersonalizedResults (образец O365 PnP)](https://github.com/SharePoint/PnP/tree/master/Samples/Search.PersonalizedResults).</span><span class="sxs-lookup"><span data-stu-id="4619c-137">The [How to perform personalized search queries with CSOM (O365 PnP Video)](https://channel9.msdn.com/blogs/OfficeDevPnP/How-to-perform-personalized-search-queries-with-CSOM) walks you through the [Search.PersonalizedResults (O365 PnP Sample)](https://github.com/SharePoint/PnP/tree/master/Samples/Search.PersonalizedResults).</span></span>

<span data-ttu-id="4619c-138">Метод **btnPerformSearch_Click** в [файле Default.aspx.cs класс](https://github.com/SharePoint/PnP/blob/master/Samples/Search.PersonalizedResults/PersonalizedSearchResultsWeb/Pages/Default.aspx.cs) выполняет поиск текстовое значение пользователь вводит в поле «Поиск» и поиск ко всему контенту, которая хранится в семействе сайтов.</span><span class="sxs-lookup"><span data-stu-id="4619c-138">The **btnPerformSearch_Click** method in the [Default.aspx.cs class](https://github.com/SharePoint/PnP/blob/master/Samples/Search.PersonalizedResults/PersonalizedSearchResultsWeb/Pages/Default.aspx.cs) executes a search for the text value the user enters into the search box and scopes the search to all content that is stored in a site collection.</span></span>  <span data-ttu-id="4619c-139">Contentclass: параметр «STS_Site» ограничивает область поиска для семейств веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="4619c-139">The contentclass:"STS_Site" parameter limits the search scope to site collections.</span></span>

    protected void btnPerformSearch_Click(object sender, EventArgs e)
    {
        var spContext = SharePointContextProvider.Current.GetSharePointContext(Context);

        using (var clientContext = spContext.CreateUserClientContextForSPHost())
        {
            // Since in this case we want only site collections, let's filter based on result type
            string query = searchtext.Text + " contentclass:\"STS_Site\"";
            ClientResult<ResultTableCollection> results = ProcessQuery(clientContext, query);
            lblStatus1.Text = FormatResults(results);
        }
    }

<span data-ttu-id="4619c-140">Метод **btnPersonalizedSearch_Click** в [файле Default.aspx.cs класс](https://github.com/SharePoint/PnP/blob/master/Samples/Search.PersonalizedResults/PersonalizedSearchResultsWeb/Pages/Default.aspx.cs) выполняет поиск же, как метод btnPerformSearch_Click делает и также добавляет дополнительный параметр на основе профиля текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="4619c-140">The **btnPersonalizedSearch_Click** method in the [Default.aspx.cs class](https://github.com/SharePoint/PnP/blob/master/Samples/Search.PersonalizedResults/PersonalizedSearchResultsWeb/Pages/Default.aspx.cs) executes the same search as the btnPerformSearch_Click method does and also adds an additional parameter based on the current user's profile.</span></span>  <span data-ttu-id="4619c-141">Класс PeopleManager используется для доступа к свойствам профиля текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="4619c-141">The PeopleManager class is used to access the current user's profile properties.</span></span>

    protected void btnPersonalizedSearch_Click(object sender, EventArgs e)
    {
        var spContext = SharePointContextProvider.Current.GetSharePointContext(Context);

        using (var clientContext = spContext.CreateUserClientContextForSPHost())
        {
            // Load user profile properties
            PeopleManager peopleManager = new PeopleManager(clientContext);
            PersonProperties personProperties = peopleManager.GetMyProperties();
            clientContext.Load(personProperties);
            clientContext.ExecuteQuery();
            // Check teh value for About Me to investigate current values
            string aboutMeValue = personProperties.UserProfileProperties["AboutMe"];
            string templateFilter = ResolveAdditionalFilter(aboutMeValue);
            // Let's build the query
            string query = "contentclass:\"STS_Site\" " + templateFilter;
            ClientResult<ResultTableCollection> results = ProcessQuery(clientContext, query);
            lblStatus2.Text = FormatResults(results);
        }
    }

<span data-ttu-id="4619c-142">Метод **ResolveAdditionalFilter** в [файле Default.aspx.cs класс](https://github.com/SharePoint/PnP/blob/master/Samples/Search.PersonalizedResults/PersonalizedSearchResultsWeb/Pages/Default.aspx.cs) оценивает свойств профиля текущего пользователя и возвращает параметр поиска.</span><span class="sxs-lookup"><span data-stu-id="4619c-142">The **ResolveAdditionalFilter** method in the [Default.aspx.cs class](https://github.com/SharePoint/PnP/blob/master/Samples/Search.PersonalizedResults/PersonalizedSearchResultsWeb/Pages/Default.aspx.cs) evaluates the current user's profile properties and returns an applicable search parameter.</span></span> <span data-ttu-id="4619c-143">В этом примере, если свойство профиля пользователя aboutMeValue содержит AppTest параметр поиска WebTemplate = STS, возвращается.</span><span class="sxs-lookup"><span data-stu-id="4619c-143">In this example, if the aboutMeValue user profile property contains AppTest then the search parameter WebTemplate=STS is returned.</span></span>  <span data-ttu-id="4619c-144">Этот параметр ограничивает область поиска для сайтов, созданных с помощью шаблона службы маркеров безопасности (сайт группы).</span><span class="sxs-lookup"><span data-stu-id="4619c-144">This parameter limits the search scope to sites built with the STS (Team Site) template.</span></span>
 
    private string ResolveAdditionalFilter(string aboutMeValue)
    {
        if (!aboutMeValue.Contains("AppTest"))
        {
            return "WebTemplate=STS";
        }
        
        return "";
    }

<span data-ttu-id="4619c-145">В обоих случаях **ProcessQuery** метода в [класс Default.aspx.cs](https://github.com/SharePoint/PnP/blob/master/Samples/Search.PersonalizedResults/PersonalizedSearchResultsWeb/Pages/Default.aspx.cs) используется класс SearchExecutor для выполнения запросов поиска и возвращать результаты.</span><span class="sxs-lookup"><span data-stu-id="4619c-145">In both cases, the **ProcessQuery** method in the [Default.aspx.cs class](https://github.com/SharePoint/PnP/blob/master/Samples/Search.PersonalizedResults/PersonalizedSearchResultsWeb/Pages/Default.aspx.cs) uses the SearchExecutor class to execute the search query and return the results.</span></span> 

    private ClientResult<ResultTableCollection> ProcessQuery(ClientContext ctx, string keywordQueryValue)
    {
        KeywordQuery keywordQuery = new KeywordQuery(ctx);
        keywordQuery.QueryText = keywordQueryValue;
        keywordQuery.RowLimit = 500;
        keywordQuery.StartRow = 0;
        keywordQuery.SelectProperties.Add("Title");
        keywordQuery.SelectProperties.Add("SPSiteUrl");
        keywordQuery.SelectProperties.Add("Description");
        keywordQuery.SelectProperties.Add("WebTemplate");
        keywordQuery.SortList.Add("SPSiteUrl", Microsoft.SharePoint.Client.Search.Query.SortDirection.Ascending);
        SearchExecutor searchExec = new SearchExecutor(ctx);
        ClientResult<ResultTableCollection> results = searchExec.ExecuteQuery(keywordQuery);
        ctx.ExecuteQuery();
        return results;
    }

<a name="javascript-csom-jsom-api"></a><span data-ttu-id="4619c-146">API CSOM JavaScript (JSOM)</span><span class="sxs-lookup"><span data-stu-id="4619c-146">JavaScript CSOM (JSOM) API</span></span>
--------------------------
<span data-ttu-id="4619c-147">В этом параметре используется JavaScript CSOM (JSOM) API для выполнения операций поиска с помощью службы поиска SharePoint.</span><span class="sxs-lookup"><span data-stu-id="4619c-147">In this option you use the JavaScript CSOM (JSOM) API to execute searches with the SharePoint Search Service.</span></span>
    
- <span data-ttu-id="4619c-148">Этот интерфейс API доступен только в код JavaScript на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="4619c-148">This API is only available in client-side JavaScript code.</span></span>

<span data-ttu-id="4619c-149">**Когда это подходит?**</span><span class="sxs-lookup"><span data-stu-id="4619c-149">**When is it a good fit?**</span></span>

- <span data-ttu-id="4619c-150">Этот интерфейс API является отлично подходит для размещенных в SharePoint надстройки и размещение у поставщика надстройки на любой веб-платформы.</span><span class="sxs-lookup"><span data-stu-id="4619c-150">This API is a great fit for SharePoint-hosted Add-ins and Provider-hosted Add-ins running on any web platform.</span></span>
- <span data-ttu-id="4619c-151">Некоторые примеры этих сценариев, ASP.NET MVC веб-сайтов, веб-сайтов PHP, Python веб-сайтов, и т.д.</span><span class="sxs-lookup"><span data-stu-id="4619c-151">Some examples of these scenarios are ASP.NET MVC web sites, PHP web sites, Python web sites, etc.</span></span>

<span data-ttu-id="4619c-152">**Приступая к работе**</span><span class="sxs-lookup"><span data-stu-id="4619c-152">**Getting Started**</span></span>

<span data-ttu-id="4619c-153">В следующем примере кода показано, как выполнить поиск с помощью службы поиска SharePoint с помощью JavaScript CSOM (JSOM) API.</span><span class="sxs-lookup"><span data-stu-id="4619c-153">The following code example demonstrates how to execute searches with the SharePoint Search Service with the JavaScript CSOM (JSOM) API.</span></span>  <span data-ttu-id="4619c-154">В этом примере выполняется поиск всех элементов, содержащих слово «Blizzard».</span><span class="sxs-lookup"><span data-stu-id="4619c-154">This example executes a search for all items that contain the term 'Blizzard'.</span></span>

    var context = SP.ClientContext.get_current();
    
    var keywordQuery = 
    new Microsoft.SharePoint.Client.Search.Query.KeywordQuery(context);
    
    keywordQuery.set_queryText("Blizzard");
    
    var searchExecutor = 
    new Microsoft.SharePoint.Client.Search.Query.SearchExecutor(context);
    
    results = searchExecutor.executeQuery(keywordQuery);
    
    context.executeQueryAsync(onGetEventsSuccess, onGetEventsFail);

<a name="rest-api"></a><span data-ttu-id="4619c-155">API-ИНТЕРФЕЙС REST</span><span class="sxs-lookup"><span data-stu-id="4619c-155">REST API</span></span>
--------
<span data-ttu-id="4619c-156">В этом параметре используется API-Интерфейс REST для выполнения операций поиска с помощью службы поиска SharePoint.</span><span class="sxs-lookup"><span data-stu-id="4619c-156">In this option you use the REST API to execute searches with the SharePoint Search Service.</span></span>
    
- <span data-ttu-id="4619c-157">Этот интерфейс API является наиболее гибкий, так как она доступна в коде на сервере и клиентских.</span><span class="sxs-lookup"><span data-stu-id="4619c-157">This API is the most flexible because it is available in both server-side and client-side code.</span></span>
- <span data-ttu-id="4619c-158">Конечная точка корневой API-Интерфейс REST службы поиска SharePoint — это:</span><span class="sxs-lookup"><span data-stu-id="4619c-158">The SharePoint Search Service REST API root endpoint is:</span></span>
    + <span data-ttu-id="4619c-159">https://<tenant>/site/_api/search/query</span><span class="sxs-lookup"><span data-stu-id="4619c-159">https://<tenant>/site/_api/search/query</span></span>
- <span data-ttu-id="4619c-160">Вот некоторые примеры:</span><span class="sxs-lookup"><span data-stu-id="4619c-160">Here are some simple examples:</span></span>
    + <span data-ttu-id="4619c-161">Поиск по ключевым словам</span><span class="sxs-lookup"><span data-stu-id="4619c-161">Keyword search</span></span>
    
        ```
        https://tenant/site/_api/search/query?querytext='{Apples}'
        ```
    + <span data-ttu-id="4619c-162">Выбор свойств</span><span class="sxs-lookup"><span data-stu-id="4619c-162">Selecting specific properties</span></span>
    
        ```
        https://tenant/site/_api/search/query?querytext='test'&selectproperties='Rank, Title'
        ```
    + <span data-ttu-id="4619c-163">сортировке;</span><span class="sxs-lookup"><span data-stu-id="4619c-163">Sorting</span></span>
    
        ```
        https://tenant/site/_api/search/query?querytext='Oranges'&sortlist='LastModifiedTime:ascending'
        ```

<span data-ttu-id="4619c-164">**Когда это подходит?**</span><span class="sxs-lookup"><span data-stu-id="4619c-164">**When is it a good fit?**</span></span>

<span data-ttu-id="4619c-165">Этот интерфейс API является отлично подходит для размещенных в SharePoint надстройки и размещение у поставщика надстройки на любой веб-платформы.</span><span class="sxs-lookup"><span data-stu-id="4619c-165">This API is a great fit for SharePoint-hosted Add-ins and Provider-hosted Add-ins running on any web platform.</span></span>
- <span data-ttu-id="4619c-166">Некоторые примеры этих сценариев — ASP.NET MVC веб-сайтов, PHP веб-сайтов, Python веб-сайтов, ASP.NET Web API services, консоли .net или приложений Windows Azure Web задания, и т.д.</span><span class="sxs-lookup"><span data-stu-id="4619c-166">Some examples of these scenarios are ASP.NET MVC web sites, PHP web sites, Python web sites, ASP.NET Web API services, .Net console or Windows applications, Azure Web Jobs, etc.</span></span>

<span data-ttu-id="4619c-167">**Приступая к работе**</span><span class="sxs-lookup"><span data-stu-id="4619c-167">**Getting Started**</span></span>

<span data-ttu-id="4619c-168">**Параметр на сервере**</span><span class="sxs-lookup"><span data-stu-id="4619c-168">**Server-side Option**</span></span>

<span data-ttu-id="4619c-169">Следующий пример демонстрирует выполнение операций поиска с помощью службы поиска SharePoint с использованием интерфейса API REST из управляемого кода .net.</span><span class="sxs-lookup"><span data-stu-id="4619c-169">The following sample demonstrates how to execute searches with the SharePoint Search Service with the REST API from managed .Net code.</span></span>

- [<span data-ttu-id="4619c-170">EmployeeDirectory (разработчик офисных решений учебные материалы)</span><span class="sxs-lookup"><span data-stu-id="4619c-170">EmployeeDirectory (OfficeDev Training Content)</span></span>](https://github.com/SharePoint/TrainingContent/tree/master/O3656/O3656-6%20Deep%20Dive%20into%20Search%20Scenarios%20in%20Office%20365/Demos/EmployeeDirectory)

<span data-ttu-id="4619c-171">С помощью метода **индекса** в [класс HomeController.cs](https://github.com/SharePoint/TrainingContent/blob/master/O3656/O3656-6%20Deep%20Dive%20into%20Search%20Scenarios%20in%20Office%20365/Demos/EmployeeDirectory/EmployeeDirectoryWeb/Controllers/HomeController.cs) выполняет поиск для всех пользователей, чьи фамилии начинаются со значений пользователь нажимает кнопку.</span><span class="sxs-lookup"><span data-stu-id="4619c-171">The **Index** method in the [HomeController.cs class](https://github.com/SharePoint/TrainingContent/blob/master/O3656/O3656-6%20Deep%20Dive%20into%20Search%20Scenarios%20in%20Office%20365/Demos/EmployeeDirectory/EmployeeDirectoryWeb/Controllers/HomeController.cs) executes a search for  all users whose last name begins with the text value the user clicks.</span></span>

    var spContext = SharePointContextProvider.Current.GetSharePointContext(HttpContext);

    string accessToken = spContext.UserAccessTokenForSPHost;

    //Build the REST API request
    StringBuilder requestUri = new StringBuilder()
    .Append(spContext.SPHostUrl)
    .Append("/_api/search/query?querytext='LastName:")
    .Append(startLetter)
    .Append("*'&selectproperties='LastName,FirstName,WorkEmail,WorkPhone'&sourceid='B09A7990-05EA-4AF9-81EF-EDFAB16C4E31'&sortlist='FirstName:ascending'");

    //Create HTTP Client
    HttpClient client = new HttpClient();
    //Add the REST API request
    HttpRequestMessage request = new HttpRequestMessage(HttpMethod.Get, requestUri.ToString());
    //Set accept header
    request.Headers.Accept.Add(new MediaTypeWithQualityHeaderValue("application/xml"));
    //Set Bearer header equal to access token
    request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", accessToken);

    //Send the REST API request
    HttpResponseMessage response = await client.SendAsync(request);
    //Set the response
    string responseString = await response.Content.ReadAsStringAsync();

<span data-ttu-id="4619c-172">[Создание надстройки SharePoint, использующих возможности поиска (O365 PnP видео)](https://channel9.msdn.com/blogs/OfficeDevPnP/How-to-build-SharePoint-add-ins-that-leverage-search) — описание [EmployeeDirectory (разработчик офисных решений обучение контента)](https://github.com/SharePoint/TrainingContent/tree/master/O3656/O3656-6%20Deep%20Dive%20into%20Search%20Scenarios%20in%20Office%20365/Demos/EmployeeDirectory).</span><span class="sxs-lookup"><span data-stu-id="4619c-172">The [How to build SharePoint add-ins that leverage search (O365 PnP Video)](https://channel9.msdn.com/blogs/OfficeDevPnP/How-to-build-SharePoint-add-ins-that-leverage-search) walks you through the [EmployeeDirectory (OfficeDev Training Content)](https://github.com/SharePoint/TrainingContent/tree/master/O3656/O3656-6%20Deep%20Dive%20into%20Search%20Scenarios%20in%20Office%20365/Demos/EmployeeDirectory).</span></span>

<span data-ttu-id="4619c-173">**Параметр со стороны клиента**</span><span class="sxs-lookup"><span data-stu-id="4619c-173">**Client-side Option**</span></span>

<span data-ttu-id="4619c-174">В следующем примере кода показано, как выполнить поиск с помощью службы поиска SharePoint с использованием интерфейса API REST из JavaScript.</span><span class="sxs-lookup"><span data-stu-id="4619c-174">The following code example demonstrates how to execute searches with the SharePoint Search Service with the REST API from JavaScript.</span></span>  <span data-ttu-id="4619c-175">В этом примере выполняется поиск всех элементов, содержащих слово «Lacrosse».</span><span class="sxs-lookup"><span data-stu-id="4619c-175">This example executes a search for all items that contain the term 'Lacrosse'.</span></span>
    
    $.ajax(
            {
                url: "http://site/_api/search/" +
                     "query?querytext='{Lacrosse}‘",
                method: "GET",
                headers: {
                    "accept": "application/json;odata=verbose",
                },
                success: onSuccess,
                error: onError
            }
        );

<a name="related-links"></a><span data-ttu-id="4619c-176">Ссылки по теме</span><span class="sxs-lookup"><span data-stu-id="4619c-176">Related links</span></span>
=============
- [<span data-ttu-id="4619c-177">Порядок выполнения индивидуально настроенных поисковых запросов с помощью CSOM (O365 PnP видео)</span><span class="sxs-lookup"><span data-stu-id="4619c-177">How to perform personalized search queries with CSOM (O365 PnP Video)</span></span>](https://channel9.msdn.com/blogs/OfficeDevPnP/How-to-perform-personalized-search-queries-with-CSOM)
- [<span data-ttu-id="4619c-178">EmployeeDirectory (разработчик офисных решений учебные материалы)</span><span class="sxs-lookup"><span data-stu-id="4619c-178">EmployeeDirectory (OfficeDev Training Content)</span></span>](https://github.com/SharePoint/TrainingContent/tree/master/O3656/O3656-6%20Deep%20Dive%20into%20Search%20Scenarios%20in%20Office%20365/Demos/EmployeeDirectory)
- [<span data-ttu-id="4619c-179">Создание надстройки SharePoint, что использование поиск (O365 PnP видео)</span><span class="sxs-lookup"><span data-stu-id="4619c-179">How to build SharePoint add-ins that leverage search (O365 PnP Video)</span></span>](https://channel9.msdn.com/blogs/OfficeDevPnP/How-to-build-SharePoint-add-ins-that-leverage-search)
- <span data-ttu-id="4619c-180">Руководств по [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Руководств")</span><span class="sxs-lookup"><span data-stu-id="4619c-180">Guidance articles at [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Guidance Articles")</span></span>
- <span data-ttu-id="4619c-181">Справочные материалы в библиотеке MSDN по [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "Справочные материалы в библиотеке MSDN")</span><span class="sxs-lookup"><span data-stu-id="4619c-181">References in MSDN at [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "References in MSDN")</span></span>
- <span data-ttu-id="4619c-182">Видеозаписи по [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "видео")</span><span class="sxs-lookup"><span data-stu-id="4619c-182">Videos at [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")</span></span>

<a name="related-pnp-samples"></a><span data-ttu-id="4619c-183">Примеры связанных с ними PnP</span><span class="sxs-lookup"><span data-stu-id="4619c-183">Related PnP samples</span></span>
===================
- [<span data-ttu-id="4619c-184">Search.PersonalizedResults (O365 PnP образец)</span><span class="sxs-lookup"><span data-stu-id="4619c-184">Search.PersonalizedResults (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Search.PersonalizedResults)
- <span data-ttu-id="4619c-185">Примеры и содержимое в [http://aka.ms/OfficeDevPnP](http://aka.ms/OfficeDevPnP)</span><span class="sxs-lookup"><span data-stu-id="4619c-185">Samples and content at [http://aka.ms/OfficeDevPnP](http://aka.ms/OfficeDevPnP)</span></span>

<a name="applies-to"></a><span data-ttu-id="4619c-186">Применимо к</span><span class="sxs-lookup"><span data-stu-id="4619c-186">Applies to</span></span>
==========
- <span data-ttu-id="4619c-187">Office 365 нескольких клиентов (MT)</span><span class="sxs-lookup"><span data-stu-id="4619c-187">Office 365 Multi Tenant (MT)</span></span>
- <span data-ttu-id="4619c-188">Office 365 выделенных (D)</span><span class="sxs-lookup"><span data-stu-id="4619c-188">Office 365 Dedicated (D)</span></span>
- <span data-ttu-id="4619c-189">SharePoint 2013 в локальной</span><span class="sxs-lookup"><span data-stu-id="4619c-189">SharePoint 2013 on-premises</span></span>
