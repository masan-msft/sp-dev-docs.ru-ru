---
title: "Использование API поиска в объектная модель SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: c4ad4850f8e76ddf2933981ce550a141bf75d792
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
<a name="search-api-usage-in-the-sharepoint-add-in-model"></a>Использование API поиска в объектная модель SharePoint
===============================================

<a name="summary"></a>Summary
-------

Подхода, можно выполнить поиск с помощью службы поиска SharePoint будет разным в новой модели надстройки SharePoint не был с кодом полного доверия.  В типичных полного доверия кода (FTC) сценарий решения фермы, на сервере объектной модели SharePoint (с запроса веб-части содержимого переопределений) или веб-службы поиска были, используемой для выполнения операций поиска с помощью службы поиска SharePoint.

В модели сценарий надстройки SharePoint выполнение операций поиска с помощью службы поиска SharePoint с помощью CSOM или API-интерфейсы REST.

<a name="high-level-guidelines"></a>Рекомендации по высокого уровня
---------------------

Как правило эскиз мы предлагаем для обеспечения высокого уровня следующее Создание и настройка семейств веб-сайтов и sub сайтам затем развертывание артефактов, конфигураций и фирменной настройки ресурсов.

- С помощью AppOnly проверки подлинности не поддерживается для любых операций службы поиска.
    + Это из-за того, что служба поиска обращается к службе профилей пользователей (UPS) для поиска сведений профиля пользователя и ИБП не поддерживает проверку подлинности AppOnly.
    + Таким образом так как их профилей атрибуты AppOnly, шаблон проверки подлинности не будет работать и релевантности поиска и другие аспекты поиска в зависимости от определенного пользователя.

<a name="options-to-execute-searches-with-the-sharepoint-search-service"></a>Параметры, чтобы выполнить поиск с помощью службы поиска SharePoint
--------------------------------------------------------------

У вас есть coupe из параметров, чтобы выполнить поиск с помощью службы поиска SharePoint.

- API-Интерфейс .net CSOM
- API CSOM JavaScript (JSOM)
- API-ИНТЕРФЕЙС REST  

<a name="net-csom-api"></a>API-Интерфейс .net CSOM
-------------
В этом параметре используется API-Интерфейс .net CSOM для выполнения операций поиска с помощью службы поиска SharePoint.
    
- Этот интерфейс API доступна только в управляемом коде .net.


**Когда это подходит?**

- Этот интерфейс API является отлично подходит для Add-ins, размещаемые у поставщика, длительной операции или других сценариях на сервере, на которых выполняется на платформе .net.
- Некоторые примеры этих сценариев, ASP.NET MVC веб-сайтов, ASP.NET Web API services, консоли .net или приложений Windows и задания Web Azure.

**Приступая к работе**

Следующий пример демонстрирует выполнение операций поиска с помощью службы поиска SharePoint с помощью API-Интерфейс .net CSOM.  В этом примере также показано, как получить доступ к профиля пользователя для индивидуальной настройки результатов поиска.

- [Search.PersonalizedResults (O365 PnP образец)](https://github.com/SharePoint/PnP/tree/master/Samples/Search.PersonalizedResults)

![Страница API поиска и личных настроек. Текст в изображение: выполнение поиска API поиска. Предоставление фильтр поиска для клиента широкого поискового запроса: текстовое поле содержит слово Test. Кнопка текста: выполнение простого поиска. Выполнение настраиваемого поиска все шаблоны сайта, с помощью данных профилей. Если сведения обо мне не содержит текст AppTest мы поиск только тех сайтов, которые являются сайты рабочих групп (WebTemplate = STS). При наличии AppTest выполняется поиск всех сайтов. Сценарий: Показать сайтов или объединенные данные из определенного расположения на основе профиля пользователя. Пример будет статистические новости страниц, которые только помеченных идентификатор, соответствующий текущее расположение пользователя или города. Кнопка текста: поиск персонализации.](media/Recipes/SearchAPI/Search.PersonalizedResults.png)

[Порядок выполнения индивидуально настроенных поисковых запросов с помощью CSOM (O365 PnP видео)](https://channel9.msdn.com/blogs/OfficeDevPnP/How-to-perform-personalized-search-queries-with-CSOM) — описание [Search.PersonalizedResults (образец O365 PnP)](https://github.com/SharePoint/PnP/tree/master/Samples/Search.PersonalizedResults).

Метод **btnPerformSearch_Click** в [файле Default.aspx.cs класс](https://github.com/SharePoint/PnP/blob/master/Samples/Search.PersonalizedResults/PersonalizedSearchResultsWeb/Pages/Default.aspx.cs) выполняет поиск текстовое значение пользователь вводит в поле «Поиск» и поиск ко всему контенту, которая хранится в семействе сайтов.  Contentclass: параметр «STS_Site» ограничивает область поиска для семейств веб-сайтов.

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

Метод **btnPersonalizedSearch_Click** в [файле Default.aspx.cs класс](https://github.com/SharePoint/PnP/blob/master/Samples/Search.PersonalizedResults/PersonalizedSearchResultsWeb/Pages/Default.aspx.cs) выполняет поиск же, как метод btnPerformSearch_Click делает и также добавляет дополнительный параметр на основе профиля текущего пользователя.  Класс PeopleManager используется для доступа к свойствам профиля текущего пользователя.

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

Метод **ResolveAdditionalFilter** в [файле Default.aspx.cs класс](https://github.com/SharePoint/PnP/blob/master/Samples/Search.PersonalizedResults/PersonalizedSearchResultsWeb/Pages/Default.aspx.cs) оценивает свойств профиля текущего пользователя и возвращает параметр поиска. В этом примере, если свойство профиля пользователя aboutMeValue содержит AppTest параметр поиска WebTemplate = STS, возвращается.  Этот параметр ограничивает область поиска для сайтов, созданных с помощью шаблона службы маркеров безопасности (сайт группы).
 
    private string ResolveAdditionalFilter(string aboutMeValue)
    {
        if (!aboutMeValue.Contains("AppTest"))
        {
            return "WebTemplate=STS";
        }
        
        return "";
    }

В обоих случаях **ProcessQuery** метода в [класс Default.aspx.cs](https://github.com/SharePoint/PnP/blob/master/Samples/Search.PersonalizedResults/PersonalizedSearchResultsWeb/Pages/Default.aspx.cs) используется класс SearchExecutor для выполнения запросов поиска и возвращать результаты. 

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

<a name="javascript-csom-jsom-api"></a>API CSOM JavaScript (JSOM)
--------------------------
В этом параметре используется JavaScript CSOM (JSOM) API для выполнения операций поиска с помощью службы поиска SharePoint.
    
- Этот интерфейс API доступен только в код JavaScript на стороне клиента.

**Когда это подходит?**

- Этот интерфейс API является отлично подходит для размещенных в SharePoint надстройки и размещение у поставщика надстройки на любой веб-платформы.
- Некоторые примеры этих сценариев, ASP.NET MVC веб-сайтов, веб-сайтов PHP, Python веб-сайтов, и т.д.

**Приступая к работе**

В следующем примере кода показано, как выполнить поиск с помощью службы поиска SharePoint с помощью JavaScript CSOM (JSOM) API.  В этом примере выполняется поиск всех элементов, содержащих слово «Blizzard».

    var context = SP.ClientContext.get_current();
    
    var keywordQuery = 
    new Microsoft.SharePoint.Client.Search.Query.KeywordQuery(context);
    
    keywordQuery.set_queryText("Blizzard");
    
    var searchExecutor = 
    new Microsoft.SharePoint.Client.Search.Query.SearchExecutor(context);
    
    results = searchExecutor.executeQuery(keywordQuery);
    
    context.executeQueryAsync(onGetEventsSuccess, onGetEventsFail);

<a name="rest-api"></a>API-ИНТЕРФЕЙС REST
--------
В этом параметре используется API-Интерфейс REST для выполнения операций поиска с помощью службы поиска SharePoint.
    
- Этот интерфейс API является наиболее гибкий, так как она доступна в коде на сервере и клиентских.
- Конечная точка корневой API-Интерфейс REST службы поиска SharePoint — это:
    + https://<tenant>/site/_api/search/query
- Вот некоторые примеры:
    + Поиск по ключевым словам
    
        ```
        https://tenant/site/_api/search/query?querytext='{Apples}'
        ```
    + Выбор свойств
    
        ```
        https://tenant/site/_api/search/query?querytext='test'&selectproperties='Rank, Title'
        ```
    + сортировке;
    
        ```
        https://tenant/site/_api/search/query?querytext='Oranges'&sortlist='LastModifiedTime:ascending'
        ```

**Когда это подходит?**

Этот интерфейс API является отлично подходит для размещенных в SharePoint надстройки и размещение у поставщика надстройки на любой веб-платформы.
- Некоторые примеры этих сценариев — ASP.NET MVC веб-сайтов, PHP веб-сайтов, Python веб-сайтов, ASP.NET Web API services, консоли .net или приложений Windows Azure Web задания, и т.д.

**Приступая к работе**

**Параметр на сервере**

Следующий пример демонстрирует выполнение операций поиска с помощью службы поиска SharePoint с использованием интерфейса API REST из управляемого кода .net.

- [EmployeeDirectory (разработчик офисных решений учебные материалы)](https://github.com/SharePoint/TrainingContent/tree/master/O3656/O3656-6%20Deep%20Dive%20into%20Search%20Scenarios%20in%20Office%20365/Demos/EmployeeDirectory)

С помощью метода **индекса** в [класс HomeController.cs](https://github.com/SharePoint/TrainingContent/blob/master/O3656/O3656-6%20Deep%20Dive%20into%20Search%20Scenarios%20in%20Office%20365/Demos/EmployeeDirectory/EmployeeDirectoryWeb/Controllers/HomeController.cs) выполняет поиск для всех пользователей, чьи фамилии начинаются со значений пользователь нажимает кнопку.

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

[Создание надстройки SharePoint, использующих возможности поиска (O365 PnP видео)](https://channel9.msdn.com/blogs/OfficeDevPnP/How-to-build-SharePoint-add-ins-that-leverage-search) — описание [EmployeeDirectory (разработчик офисных решений обучение контента)](https://github.com/SharePoint/TrainingContent/tree/master/O3656/O3656-6%20Deep%20Dive%20into%20Search%20Scenarios%20in%20Office%20365/Demos/EmployeeDirectory).

**Параметр со стороны клиента**

В следующем примере кода показано, как выполнить поиск с помощью службы поиска SharePoint с использованием интерфейса API REST из JavaScript.  В этом примере выполняется поиск всех элементов, содержащих слово «Lacrosse».
    
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

<a name="related-links"></a>Ссылки по теме
=============
- [Порядок выполнения индивидуально настроенных поисковых запросов с помощью CSOM (O365 PnP видео)](https://channel9.msdn.com/blogs/OfficeDevPnP/How-to-perform-personalized-search-queries-with-CSOM)
- [EmployeeDirectory (разработчик офисных решений учебные материалы)](https://github.com/SharePoint/TrainingContent/tree/master/O3656/O3656-6%20Deep%20Dive%20into%20Search%20Scenarios%20in%20Office%20365/Demos/EmployeeDirectory)
- [Создание надстройки SharePoint, что использование поиск (O365 PnP видео)](https://channel9.msdn.com/blogs/OfficeDevPnP/How-to-build-SharePoint-add-ins-that-leverage-search)
- Руководств по [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Руководств")
- Справочные материалы в библиотеке MSDN по [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "Справочные материалы в библиотеке MSDN")
- Видеозаписи по [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "видео")

<a name="related-pnp-samples"></a>Примеры связанных с ними PnP
===================
- [Search.PersonalizedResults (O365 PnP образец)](https://github.com/SharePoint/PnP/tree/master/Samples/Search.PersonalizedResults)
- Примеры и содержимое в [http://aka.ms/OfficeDevPnP](http://aka.ms/OfficeDevPnP)

<a name="applies-to"></a>Применимо к
==========
- Office 365 нескольких клиентов (MT)
- Office 365 выделенных (D)
- SharePoint 2013 в локальной
