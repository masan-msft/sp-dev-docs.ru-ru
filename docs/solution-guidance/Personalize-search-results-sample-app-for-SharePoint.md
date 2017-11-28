---
title: "Настройка поиска результаты пример надстройки для SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: f29604a72bd9346cccf548c928812b7e55703849
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
# <a name="personalize-search-results-sample-add-in-for-sharepoint"></a>Настройка поиска результаты пример надстройки для SharePoint

SharePoint можно настроить путем фильтрации информацию, которая отображается для пользователей, на основе значения свойства профиля пользователя.
    
_**Область применения:** Office 365 | SharePoint 2013 | SharePoint Online_
    
В примере кода [Search.PersonalizedResults](https://github.com/SharePoint/PnP/tree/master/Samples/Search.PersonalizedResults) показано, как можно настроить SharePoint, данные фильтрации на основе значения свойства профиля пользователя. Некоторые примеры pesonalization.

- Новости и другое содержимое, отфильтрованные по стране или расположение.
    
- Навигационные ссылки фильтруется на основе роли пользователя или организации.
    
- Рестораны или списков выхода розничной торговли, основываясь на положении предприятия.
    
В этом примере код использует размещение у поставщика в надстройке для отображения результатов поиска для пользователей, включающую все сайты или только сайты групп, которые пользователь имеет доступ к. Для этого примера:

- Проверяет значение свойства профиля пользователя **AboutMe** .
    
- Создает строку фильтра запроса поиска, связанного со значением свойства профиля пользователя **AboutMe** .
    
- Выполняется запросов поиска и отображает результаты запроса поиска.

## <a name="before-you-begin"></a>Перед началом работы
<a name="sectionSection0"> </a>

Чтобы начать работу, загрузите пример надстройки [Search.PersonalizedResults](https://github.com/SharePoint/PnP/tree/master/Samples/Search.PersonalizedResults) из проекта [разработчика Office 365 шаблоны и рекомендации](https://github.com/SharePoint/PnP/tree/dev) на репозиториев.

## <a name="using-the-searchpersonalizedresults-app"></a>С помощью приложения Search.PersonalizedResults
<a name="sectionSection1"> </a>

При запуске в этом примере отображается приложение, размещаемое у поставщика как показано на рисунке 1. 

**На рисунке 1. Начальная страница приложения Search.PersonalizedResults**

![Снимок экрана, показывающий начальной странице Search.PersonalizedResults приложения](media/d5df9bb4-fa11-4bd6-91fd-c4d339687a8a.png)

В этой статье описан сценарий **поиска индивидуально настроенных выполнение всех шаблонов сайта с помощью данных профилей** . Выбор **Выполнения персонально поиска** возвращает результаты фильтрованного поиска, которые содержат веб-сайтов групп, как показано на рисунке 2. Обратите внимание, что в столбце **шаблона** сайтов типа только для **службы маркеров безопасности** .

**На рисунке 2. Отображение веб-сайтов групп только результаты поиска**

![Снимок экрана с отображением веб-сайтов групп только результаты поиск](media/dde71d9f-a296-4bee-b48b-964f81193404.png)

Для обработки сценариев личной настройки, можно изменить запрос поиска по:

- Считывание и тестирование значение свойства профиля пользователя для этого пользователя. В этом примере проверяется свойство **Сведения обо мне** для значения **AppTest**.
    
- Сделать определенные курсов действия на основе значения свойства профиля пользователя. К примеру Если **AppTest**значение **Сведения обо мне** свойство профиля пользователя, в этом примере кода удаляет фильтр сайта группы и возвращает результаты поиска, которые содержат все сайты.

### <a name="to-enter-apptest-in-the-about-me-user-profile-property"></a>Чтобы ввести AppTest в сведения обо мне свойство профиля пользователя

1. В верхней части сайта Office 365 выберите изображение профиля и нажмите кнопку **Сведения обо мне**, как показано на рисунке 3.
    
2. На странице " **сведения обо мне** " нажмите кнопку **Изменить профиль**.
    
3. **Сведения обо мне**введите **AppTest**.
    
4. Выберите команду **Сохранить все и закрыть**.

**На рисунке 3. Переход к странице профиля пользователя, выбрав сведения обо мне**

![Снимок экрана страницы профиля пользователя с помощью сведения обо мне с выделением.](media/a7eccfcd-68f7-44b9-8f32-14a0d2f60398.png)

Вернитесь к **Search.PersonalizedResults** размещением у поставщика надстройки и еще раз нажмите **Выполнить поиск персонализации** . Надстройка изменение фильтра по запросу поиска для отображения всех сайтов веб-сайтов групп, как показано на рисунке 4. В столбце **шаблона** теперь содержит несколько типов шаблонов другой сайт.

**На рисунке 4. Отображение всех сайтов результатов поиска**

![Снимок экрана с отображением всех сайтов результатов поиска](media/3af49550-cd2d-4e7e-af1d-5227a5603730.png)

Выбор **Выполнения поиска персонально** вызывает метод **btnPersonalizedSearch_Click** в файле default.aspx.cs. **btnPersonalizedSearch_Click** выполняет следующие действия:

- Использует **PeopleManager** для получения всех свойств профиля пользователя для пользователя, выполняющего эту надстройку.
    
- Получает и проверяет значение свойства профиля пользователя **AboutMe** . Если значение свойства **AboutMe** **AppTest**, поискового запроса извлекаются все сайты, использующие строки запроса `contentclass:"STS_Site"`. Если значение свойства **AboutMe** не **AppTest**, используется в качестве фильтра сайта группы в строку запроса ( `WebTemplate=STS`), и веб-сайтов групп только получает поисковый запрос.
    
- Вызывает метод **ProcessQuery** , чтобы получать результаты поиска, в зависимости от строки предоставленного запроса. **ProcessQuery** также показано, как указать список свойств для возврата с результатами поиска.
    
- Вызывает метод **FormatResults** для форматирования результатов поиска в HTML-таблицы.
    
**Примечание**  Код, приведенный в данной статье предоставляется в качестве-без никаких гарантий, явных или подразумеваемых, включая никаких гарантий соответствие для определенной задачи, окупаемость или не нарушения прав.

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

## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="bk_addresources"> </a>

-  [Решения пользовательского профиля для SharePoint 2013 и SharePoint Online](user-profile-solutions-for-sharepoint.md)
    
-  [Search.PersonalizedResults приложения](https://github.com/SharePoint/PnP/tree/master/Samples/Search.PersonalizedResults)
    
-  [UserProfile.Manipulation.CSOM](https://github.com/SharePoint/PnP/tree/master/Samples/UserProfile.Manipulation.CSOM)
    
-  [UserProfile.Manipulation.CSOM.Console](https://github.com/SharePoint/PnP/tree/master/Samples/UserProfile.Manipulation.CSOM.Console)
    
-  [Core.ProfileProperty.Migration](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ProfileProperty.Migration)
