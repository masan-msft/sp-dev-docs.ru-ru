---
title: "Настройка поиска результаты пример надстройки для SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: e2190e8d60bbca5f3353662823c921c1f59d1c27
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="personalize-search-results-sample-add-in-for-sharepoint"></a><span data-ttu-id="9096b-102">Настройка поиска результаты пример надстройки для SharePoint</span><span class="sxs-lookup"><span data-stu-id="9096b-102">Personalize search results sample add-in for SharePoint</span></span>

<span data-ttu-id="9096b-103">SharePoint можно настроить путем фильтрации информацию, которая отображается для пользователей, на основе значения свойства профиля пользователя.</span><span class="sxs-lookup"><span data-stu-id="9096b-103">You can personalize SharePoint by filtering information that is shown to the user based on the value of a user profile property.</span></span>
    
<span data-ttu-id="9096b-104">_**Область применения:** Office 365 | SharePoint 2013 | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="9096b-104">_**Applies to:** Office 365 | SharePoint 2013 | SharePoint Online_</span></span>
    
<span data-ttu-id="9096b-105">В примере кода [Search.PersonalizedResults](https://github.com/SharePoint/PnP/tree/master/Samples/Search.PersonalizedResults) показано, как можно настроить SharePoint, данные фильтрации на основе значения свойства профиля пользователя.</span><span class="sxs-lookup"><span data-stu-id="9096b-105">The [Search.PersonalizedResults](https://github.com/SharePoint/PnP/tree/master/Samples/Search.PersonalizedResults) code sample shows how you can personalize SharePoint by filtering information based on the value of a user profile property.</span></span> <span data-ttu-id="9096b-106">Некоторые примеры pesonalization.</span><span class="sxs-lookup"><span data-stu-id="9096b-106">Some examples of pesonalization include:</span></span>

- <span data-ttu-id="9096b-107">Новости и другое содержимое, отфильтрованные по стране или расположение.</span><span class="sxs-lookup"><span data-stu-id="9096b-107">News articles or other content filtered by country or location.</span></span>
    
- <span data-ttu-id="9096b-108">Навигационные ссылки фильтруется на основе роли пользователя или организации.</span><span class="sxs-lookup"><span data-stu-id="9096b-108">Navigation links filtered based on the user's role or organization.</span></span>
    
- <span data-ttu-id="9096b-109">Рестораны или списков выхода розничной торговли, основываясь на положении предприятия.</span><span class="sxs-lookup"><span data-stu-id="9096b-109">Restaurants or retail outlet listings based on the location of your place of business.</span></span>
    
<span data-ttu-id="9096b-110">В этом примере код использует размещение у поставщика в надстройке для отображения результатов поиска для пользователей, включающую все сайты или только сайты групп, которые пользователь имеет доступ к.</span><span class="sxs-lookup"><span data-stu-id="9096b-110">This code sample uses a provider-hosted add-in to display search results to the user that include either all sites or only team sites that the user has access to.</span></span> <span data-ttu-id="9096b-111">Для этого примера:</span><span class="sxs-lookup"><span data-stu-id="9096b-111">To do this, the sample:</span></span>

- <span data-ttu-id="9096b-112">Проверяет значение свойства профиля пользователя **AboutMe** .</span><span class="sxs-lookup"><span data-stu-id="9096b-112">Checks the value of the  **AboutMe** user profile property.</span></span>
    
- <span data-ttu-id="9096b-113">Создает строку фильтра запроса поиска, связанного со значением свойства профиля пользователя **AboutMe** .</span><span class="sxs-lookup"><span data-stu-id="9096b-113">Builds a search query filter string associated with the value of the  **AboutMe** user profile property.</span></span>
    
- <span data-ttu-id="9096b-114">Выполняется запросов поиска и отображает результаты запроса поиска.</span><span class="sxs-lookup"><span data-stu-id="9096b-114">Runs the search query and displays the search query results.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="9096b-115">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="9096b-115">Before you begin</span></span>
<span data-ttu-id="9096b-116"><a name="sectionSection0"> </a></span><span class="sxs-lookup"><span data-stu-id="9096b-116"></span></span>

<span data-ttu-id="9096b-117">Чтобы начать работу, загрузите пример надстройки [Search.PersonalizedResults](https://github.com/SharePoint/PnP/tree/master/Samples/Search.PersonalizedResults) из проекта [разработчика Office 365 шаблоны и рекомендации](https://github.com/SharePoint/PnP/tree/dev) на репозиториев.</span><span class="sxs-lookup"><span data-stu-id="9096b-117">To get started, download the  [Search.PersonalizedResults](https://github.com/SharePoint/PnP/tree/master/Samples/Search.PersonalizedResults) sample add-in from the [Office 365 Developer patterns and practices](https://github.com/SharePoint/PnP/tree/dev) project on GitHub.</span></span>

## <a name="using-the-searchpersonalizedresults-app"></a><span data-ttu-id="9096b-118">С помощью приложения Search.PersonalizedResults</span><span class="sxs-lookup"><span data-stu-id="9096b-118">Using the Search.PersonalizedResults app</span></span>
<span data-ttu-id="9096b-119"><a name="sectionSection1"> </a></span><span class="sxs-lookup"><span data-stu-id="9096b-119"></span></span>

<span data-ttu-id="9096b-120">При запуске в этом примере отображается приложение, размещаемое у поставщика как показано на рисунке 1.</span><span class="sxs-lookup"><span data-stu-id="9096b-120">When you run this code sample, a provider-hosted application appears, as shown in Figure 1.</span></span> 

<span data-ttu-id="9096b-121">**На рисунке 1. Начальная страница приложения Search.PersonalizedResults**</span><span class="sxs-lookup"><span data-stu-id="9096b-121">**Figure 1. Start page of the Search.PersonalizedResults app**</span></span>

![Снимок экрана, показывающий начальной странице Search.PersonalizedResults приложения](media/d5df9bb4-fa11-4bd6-91fd-c4d339687a8a.png)

<span data-ttu-id="9096b-123">В этой статье описан сценарий **поиска индивидуально настроенных выполнение всех шаблонов сайта с помощью данных профилей** .</span><span class="sxs-lookup"><span data-stu-id="9096b-123">This article describes the  **Perform personalized search of all site templates using profile data** scenario.</span></span> <span data-ttu-id="9096b-124">Выбор **Выполнения персонально поиска** возвращает результаты фильтрованного поиска, которые содержат веб-сайтов групп, как показано на рисунке 2.</span><span class="sxs-lookup"><span data-stu-id="9096b-124">Choosing **Perform Personalized Search** returns filtered search results that contain team sites only, as shown in Figure 2.</span></span> <span data-ttu-id="9096b-125">Обратите внимание, что в столбце **шаблона** сайтов типа только для **службы маркеров безопасности** .</span><span class="sxs-lookup"><span data-stu-id="9096b-125">Notice that the **Template** column contains sites of type **STS** only.</span></span>

<span data-ttu-id="9096b-126">**На рисунке 2. Отображение веб-сайтов групп только результаты поиска**</span><span class="sxs-lookup"><span data-stu-id="9096b-126">**Figure 2. Search results showing team sites only**</span></span>

![Снимок экрана с отображением веб-сайтов групп только результаты поиск](media/dde71d9f-a296-4bee-b48b-964f81193404.png)

<span data-ttu-id="9096b-128">Для обработки сценариев личной настройки, можно изменить запрос поиска по:</span><span class="sxs-lookup"><span data-stu-id="9096b-128">For handling personalization scenarios, you can change the search query by:</span></span>

- <span data-ttu-id="9096b-129">Считывание и тестирование значение свойства профиля пользователя для этого пользователя.</span><span class="sxs-lookup"><span data-stu-id="9096b-129">Reading and testing the value of a user profile property for that user.</span></span> <span data-ttu-id="9096b-130">В этом примере проверяется свойство **Сведения обо мне** для значения **AppTest**.</span><span class="sxs-lookup"><span data-stu-id="9096b-130">This code sample tests the  **About Me** property for a value of **AppTest**.</span></span>
    
- <span data-ttu-id="9096b-131">Сделать определенные курсов действия на основе значения свойства профиля пользователя.</span><span class="sxs-lookup"><span data-stu-id="9096b-131">Taking a specific course of action based on the value of the user profile property.</span></span> <span data-ttu-id="9096b-132">К примеру Если **AppTest**значение **Сведения обо мне** свойство профиля пользователя, в этом примере кода удаляет фильтр сайта группы и возвращает результаты поиска, которые содержат все сайты.</span><span class="sxs-lookup"><span data-stu-id="9096b-132">For example, if the value of the  **About Me** user profile property is **AppTest**, this code sample removes the team site filter and returns search results that contain all sites.</span></span>

### <a name="to-enter-apptest-in-the-about-me-user-profile-property"></a><span data-ttu-id="9096b-133">Чтобы ввести AppTest в сведения обо мне свойство профиля пользователя</span><span class="sxs-lookup"><span data-stu-id="9096b-133">To enter AppTest in the About Me user profile property</span></span>

1. <span data-ttu-id="9096b-134">В верхней части сайта Office 365 выберите изображение профиля и нажмите кнопку **Сведения обо мне**, как показано на рисунке 3.</span><span class="sxs-lookup"><span data-stu-id="9096b-134">At the top of your Office 365 site, choose your profile picture, then choose  **About Me**, as shown in Figure 3.</span></span>
    
2. <span data-ttu-id="9096b-135">На странице " **сведения обо мне** " нажмите кнопку **Изменить профиль**.</span><span class="sxs-lookup"><span data-stu-id="9096b-135">On the  **About me** page, choose **edit your profile**.</span></span>
    
3. <span data-ttu-id="9096b-136">**Сведения обо мне**введите **AppTest**.</span><span class="sxs-lookup"><span data-stu-id="9096b-136">In  **About me**, enter  **AppTest**.</span></span>
    
4. <span data-ttu-id="9096b-137">Выберите команду **Сохранить все и закрыть**.</span><span class="sxs-lookup"><span data-stu-id="9096b-137">Choose  **Save all and close**.</span></span>

<span data-ttu-id="9096b-138">**На рисунке 3. Переход к странице профиля пользователя, выбрав сведения обо мне**</span><span class="sxs-lookup"><span data-stu-id="9096b-138">**Figure 3. Navigating to a user's profile page by choosing About me**</span></span>

![Снимок экрана страницы профиля пользователя с помощью сведения обо мне с выделением.](media/a7eccfcd-68f7-44b9-8f32-14a0d2f60398.png)

<span data-ttu-id="9096b-140">Вернитесь к **Search.PersonalizedResults** размещением у поставщика надстройки и еще раз нажмите **Выполнить поиск персонализации** .</span><span class="sxs-lookup"><span data-stu-id="9096b-140">Return to the  **Search.PersonalizedResults** provider-hosted add-in and choose **Perform Personalized Search** again.</span></span> <span data-ttu-id="9096b-141">Надстройка изменение фильтра по запросу поиска для отображения всех сайтов веб-сайтов групп, как показано на рисунке 4.</span><span class="sxs-lookup"><span data-stu-id="9096b-141">The add-in changes the filter on the search query to show all sites instead of team sites only, as shown in Figure 4.</span></span> <span data-ttu-id="9096b-142">В столбце **шаблона** теперь содержит несколько типов шаблонов другой сайт.</span><span class="sxs-lookup"><span data-stu-id="9096b-142">The **Template** column now contains several different site template types.</span></span>

<span data-ttu-id="9096b-143">**На рисунке 4. Отображение всех сайтов результатов поиска**</span><span class="sxs-lookup"><span data-stu-id="9096b-143">**Figure 4. Search results showing all sites**</span></span>

![Снимок экрана с отображением всех сайтов результатов поиска](media/3af49550-cd2d-4e7e-af1d-5227a5603730.png)

<span data-ttu-id="9096b-145">Выбор **Выполнения поиска персонально** вызывает метод **btnPersonalizedSearch_Click** в файле default.aspx.cs.</span><span class="sxs-lookup"><span data-stu-id="9096b-145">Choosing  **Perform Personalized Search** calls the **btnPersonalizedSearch_Click** method in default.aspx.cs.</span></span> <span data-ttu-id="9096b-146">**btnPersonalizedSearch_Click** выполняет следующие действия:</span><span class="sxs-lookup"><span data-stu-id="9096b-146">**btnPersonalizedSearch_Click** performs the following actions:</span></span>

- <span data-ttu-id="9096b-147">Использует **PeopleManager** для получения всех свойств профиля пользователя для пользователя, выполняющего эту надстройку.</span><span class="sxs-lookup"><span data-stu-id="9096b-147">Uses  **PeopleManager** to get all user profile properties for the user running this add-in.</span></span>
    
- <span data-ttu-id="9096b-148">Получает и проверяет значение свойства профиля пользователя **AboutMe** .</span><span class="sxs-lookup"><span data-stu-id="9096b-148">Retrieves and checks the value of the  **AboutMe** user profile property.</span></span> <span data-ttu-id="9096b-149">Если значение свойства **AboutMe** **AppTest**, поискового запроса извлекаются все сайты, использующие строки запроса `contentclass:"STS_Site"`.</span><span class="sxs-lookup"><span data-stu-id="9096b-149">If the value of the **AboutMe** property is **AppTest**, the search query retrieves all sites using the query string  `contentclass:"STS_Site"`.</span></span> <span data-ttu-id="9096b-150">Если значение свойства **AboutMe** не **AppTest**, используется в качестве фильтра сайта группы в строку запроса ( `WebTemplate=STS`), и веб-сайтов групп только получает поисковый запрос.</span><span class="sxs-lookup"><span data-stu-id="9096b-150">If the value of the  **AboutMe** property is not **AppTest**, the team site filter is appended to the query string ( `WebTemplate=STS`), and the search query retrieves team sites only.</span></span>
    
- <span data-ttu-id="9096b-151">Вызывает метод **ProcessQuery** , чтобы получать результаты поиска, в зависимости от строки предоставленного запроса.</span><span class="sxs-lookup"><span data-stu-id="9096b-151">Calls the  **ProcessQuery** method to retrieve the search results based on the supplied query string.</span></span> <span data-ttu-id="9096b-152">**ProcessQuery** также показано, как указать список свойств для возврата с результатами поиска.</span><span class="sxs-lookup"><span data-stu-id="9096b-152">**ProcessQuery** also demonstrates how to specify a list of properties to return with the search results.</span></span>
    
- <span data-ttu-id="9096b-153">Вызывает метод **FormatResults** для форматирования результатов поиска в HTML-таблицы.</span><span class="sxs-lookup"><span data-stu-id="9096b-153">Calls the  **FormatResults** method to format the search results into an HTML table.</span></span>
    
> [!NOTE] 
> <span data-ttu-id="9096b-154">Код, приведенный в данной статье предоставляется в качестве-без никаких гарантий, явных или подразумеваемых, включая никаких гарантий соответствие для определенной задачи, окупаемость или не нарушения прав.</span><span class="sxs-lookup"><span data-stu-id="9096b-154">The code in this article is provided as-is, without warranty of any kind, either express or implied, including any implied warranties of fitness for a particular purpose, merchantability, or non-infringement.</span></span>

```
protected void btnPersonalizedSearch_Click(object sender, EventArgs e)
        {
            var spContext = SharePointContextProvider.Current.GetSharePointContext(Context);

            using (var clientContext = spContext.CreateUserClientContextForSPHost())
            {
                // Load user profile properties.
                PeopleManager peopleManager = new PeopleManager(clientContext);
                PersonProperties personProperties = peopleManager.GetMyProperties();
                clientContext.Load(personProperties);
                clientContext.ExecuteQuery();
                // Check the value of About Me. 
                string aboutMeValue = personProperties.UserProfileProperties["AboutMe"];
                string templateFilter = ResolveAdditionalFilter(aboutMeValue);
                // Build the query string.
                string query = "contentclass:\"STS_Site\" " + templateFilter;
                ClientResult<ResultTableCollection> results = ProcessQuery(clientContext, query);
                lblStatus2.Text = FormatResults(results);
            }
        }

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
```

## <a name="see-also"></a><span data-ttu-id="9096b-155">См. также</span><span class="sxs-lookup"><span data-stu-id="9096b-155">See also</span></span>
<span data-ttu-id="9096b-156"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="9096b-156"></span></span>

-  [<span data-ttu-id="9096b-157">Решения пользовательского профиля для SharePoint 2013 и SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="9096b-157">User profile solutions for SharePoint 2013 and SharePoint Online</span></span>](user-profile-solutions-for-sharepoint.md)
    
-  [<span data-ttu-id="9096b-158">Search.PersonalizedResults приложения</span><span class="sxs-lookup"><span data-stu-id="9096b-158">Search.PersonalizedResults app</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Search.PersonalizedResults)
    
-  [<span data-ttu-id="9096b-159">UserProfile.Manipulation.CSOM</span><span class="sxs-lookup"><span data-stu-id="9096b-159">UserProfile.Manipulation.CSOM</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/UserProfile.Manipulation.CSOM)
    
-  [<span data-ttu-id="9096b-160">UserProfile.Manipulation.CSOM.Console</span><span class="sxs-lookup"><span data-stu-id="9096b-160">UserProfile.Manipulation.CSOM.Console</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/UserProfile.Manipulation.CSOM.Console)
    
-  [<span data-ttu-id="9096b-161">Core.ProfileProperty.Migration</span><span class="sxs-lookup"><span data-stu-id="9096b-161">Core.ProfileProperty.Migration</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ProfileProperty.Migration)
