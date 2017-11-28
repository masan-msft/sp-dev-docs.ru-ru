---
title: "Настройки поиска для SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: c8afb3e0589e65e100ca3512926e931e966e510a
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
# <a name="search-customizations-for-sharepoint"></a><span data-ttu-id="06b94-102">Настройки поиска для SharePoint</span><span class="sxs-lookup"><span data-stu-id="06b94-102">Search customizations for SharePoint</span></span>

<span data-ttu-id="06b94-103">Создание настраиваемого SharePoint 2013 и SharePoint Online сценарии поиска с помощью каталога сайтов на основе поиска, персонализированные поиска или поиска конфигурации мобильности.</span><span class="sxs-lookup"><span data-stu-id="06b94-103">Create customized SharePoint 2013 and SharePoint Online search scenarios by using a search-based site directory, personalized search, or search configuration portability.</span></span> 

<span data-ttu-id="06b94-104">_**Применимо к:** Office 365 | SharePoint 2013 | Надстройки SharePoint | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="06b94-104">_**Applies to:** Office 365 | SharePoint 2013 | SharePoint Add-ins | SharePoint Online_</span></span>

## <a name="search-based-site-directory"></a><span data-ttu-id="06b94-105">Каталог сайтов на основе поиска</span><span class="sxs-lookup"><span data-stu-id="06b94-105">Search-based site directory</span></span>

<span data-ttu-id="06b94-106">Поиск SharePoint позволяет создавать каталог сайтов на основе поиска без какого-либо пользовательского кода.</span><span class="sxs-lookup"><span data-stu-id="06b94-106">SharePoint search enables you to create a search-based site directory without writing any custom code.</span></span> 

<span data-ttu-id="06b94-107">Создание каталога сайтов:</span><span class="sxs-lookup"><span data-stu-id="06b94-107">To create a site directory:</span></span>

1. <span data-ttu-id="06b94-108">Создайте сайт каталога шаблонов отображения.</span><span class="sxs-lookup"><span data-stu-id="06b94-108">Create the site directory display templates.</span></span>
    
2. <span data-ttu-id="06b94-109">Определите тип результата каталога сайтов.</span><span class="sxs-lookup"><span data-stu-id="06b94-109">Define the site directory result type.</span></span>
    
3. <span data-ttu-id="06b94-110">Создание страницы результатов.</span><span class="sxs-lookup"><span data-stu-id="06b94-110">Create the results page.</span></span>
    
4. <span data-ttu-id="06b94-111">Изменение свойств веб-части результатов.</span><span class="sxs-lookup"><span data-stu-id="06b94-111">Edit the Results Web Part properties.</span></span>
    
<span data-ttu-id="06b94-112">Чтобы создать сайт каталога шаблонов отображения:</span><span class="sxs-lookup"><span data-stu-id="06b94-112">To create the site directory display templates:</span></span>

<span data-ttu-id="06b94-113">**Примечание:**  В этой процедуре используются шаблоны отображения, связанные с сайта без изменений.</span><span class="sxs-lookup"><span data-stu-id="06b94-113">**Note:**  This procedure uses the site-related display templates without modification.</span></span> <span data-ttu-id="06b94-114">Если вы хотите изменить способ отображения результатов каталог сайтов, изменять шаблоны отображения, созданные вами.</span><span class="sxs-lookup"><span data-stu-id="06b94-114">If you want to change how site directory results are displayed, modify the display templates that you create.</span></span>

1. <span data-ttu-id="06b94-115">Откройте сопоставление сетевого диска **Коллекции главных страниц**.</span><span class="sxs-lookup"><span data-stu-id="06b94-115">Open the mapped network drive to the  **Master Page Gallery**.</span></span> <span data-ttu-id="06b94-116">Дополнительные сведения можно [как: сопоставление сетевого диска коллекции главных страниц SharePoint 2013](http://msdn.microsoft.com/en-us/library/office/jj733519%28v=office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="06b94-116">For more information, see [How to: Map a network drive to the SharePoint 2013 Master Page Gallery](http://msdn.microsoft.com/en-us/library/office/jj733519%28v=office.15%29.aspx).</span></span>
    
2. <span data-ttu-id="06b94-117">Сделайте копии шаблона отображения HTML-файлы, которые лучше сопоставить вы пытаетесь выполнить.</span><span class="sxs-lookup"><span data-stu-id="06b94-117">Make copies of the display template HTML files that best map what you're trying to do.</span></span> <span data-ttu-id="06b94-118">Для сценария, каталог сайтов это будет Item_Site.html и Item_Site_HoverPanel.html.</span><span class="sxs-lookup"><span data-stu-id="06b94-118">For the site directory scenario, this will be Item_Site.html and Item_Site_HoverPanel.html.</span></span> <span data-ttu-id="06b94-119">Оба файла располагаются в `\Display Templates\Search` папки в сопоставление сетевого диска.</span><span class="sxs-lookup"><span data-stu-id="06b94-119">Both files are located in the  `\Display Templates\Search` folder in the mapped network drive.</span></span>
    
3. <span data-ttu-id="06b94-120">Переименование копии, которые вы внесли файлов Item_SiteDirectory.html и Item_SiteDirectory_HoverPanel.html, как показано.</span><span class="sxs-lookup"><span data-stu-id="06b94-120">Rename the copies that you made of the Item_SiteDirectory.html and Item_SiteDirectory_HoverPanel.html files as shown.</span></span>
    
    <span data-ttu-id="06b94-121">**На рисунке 1. Шаблоны отображения каталога сайтов**</span><span class="sxs-lookup"><span data-stu-id="06b94-121">**Figure 1. Site directory display templates**</span></span>

    ![Шаблоны отображения каталога сайтов](media/search-customizations-for-sharepoint/4c084d31-bad4-45f0-950b-ba214f9487f7.png)

4. <span data-ttu-id="06b94-123">Откройте файл Item_SiteDirectory.html и внесите следующие изменения:</span><span class="sxs-lookup"><span data-stu-id="06b94-123">Open the Item_SiteDirectory.html file and make the following changes:</span></span>
    
    - <span data-ttu-id="06b94-124">Изменение `<title>` значение из «Узла элемента», «Каталог узлов» тега.</span><span class="sxs-lookup"><span data-stu-id="06b94-124">Change the  `<title>` tag value from "Site Item" to "Site Directory".</span></span>
    
    - <span data-ttu-id="06b94-125">Изменение первого `<div>` тег после открывающего `<body>` тега из `<div id="Item_Site">` для `<div id="Item_SiteDirectory">`.</span><span class="sxs-lookup"><span data-stu-id="06b94-125">Change the first  `<div>` tag after the opening `<body>` tag from `<div id="Item_Site">` to `<div id="Item_SiteDirectory">`.</span></span>
    
    - <span data-ttu-id="06b94-126">Изменение меняющейся панели JavaScript имя файла шаблона отображения из: `var hoverUrl = "~sitecollection/_catalogs/masterpage/Display Templates/Search/Item_Site_HoverPanel.js";`для:`var hoverUrl = "~sitecollection/_catalogs/masterpage/Display Templates/Search/Item_SiteDirectory_HoverPanel.js";`</span><span class="sxs-lookup"><span data-stu-id="06b94-126">Change the hover panel display template JavaScript file name from: `var hoverUrl = "~sitecollection/_catalogs/masterpage/Display Templates/Search/Item_Site_HoverPanel.js";`to: `var hoverUrl = "~sitecollection/_catalogs/masterpage/Display Templates/Search/Item_SiteDirectory_HoverPanel.js";`</span></span>
    
5. <span data-ttu-id="06b94-127">Откройте файл Item_SiteDirectory_HoverPanel.html и внесите следующие изменения:</span><span class="sxs-lookup"><span data-stu-id="06b94-127">Open the Item_SiteDirectory_HoverPanel.html file and make the following changes:</span></span>
    
    - <span data-ttu-id="06b94-128">Изменение `<div>` следующий открывающий тег `<body>` тега из: `<title>Site Hover Panel Test</title>`для:`<title>Site Directory Hover Panel</title>`</span><span class="sxs-lookup"><span data-stu-id="06b94-128">Change the  `<div>` tag following the opening `<body>` tag from: `<title>Site Hover Panel Test</title>`to: `<title>Site Directory Hover Panel</title>`</span></span>
    
    - <span data-ttu-id="06b94-129">Изменение `<title>` тега из: `<div id="Item_Site_HoverPanel">`для:`<div id="Item_SiteDirectory_HoverPanel">`</span><span class="sxs-lookup"><span data-stu-id="06b94-129">Change the  `<title>` tag from: `<div id="Item_Site_HoverPanel">`to: `<div id="Item_SiteDirectory_HoverPanel">`</span></span>
    
<span data-ttu-id="06b94-130">Чтобы определить тип результатов каталога сайта:</span><span class="sxs-lookup"><span data-stu-id="06b94-130">To define the site directory result type:</span></span>

1. <span data-ttu-id="06b94-131">Последовательно выберите пункты **Параметры сайта** > **поиска** > **Типы результатов**, а затем выберите **Новый тип результата**.</span><span class="sxs-lookup"><span data-stu-id="06b94-131">Go to  **Site Settings** > **Search** > **Result Types**, and then choose  **New Result Type**.</span></span>
    
2. <span data-ttu-id="06b94-132">Имя нового типа результата «Основные каталог сайтов».</span><span class="sxs-lookup"><span data-stu-id="06b94-132">Name your new result type "Basic Site Directory".</span></span>
    
3. <span data-ttu-id="06b94-133">В **как должны выглядеть эти результаты?** выберите **Каталога сайтов**.</span><span class="sxs-lookup"><span data-stu-id="06b94-133">In the  **What should these results look like?** box, select **Site Directory**.</span></span>
    
    <span data-ttu-id="06b94-134">**На рисунке 2. Конфигурация сайта результатов**</span><span class="sxs-lookup"><span data-stu-id="06b94-134">**Figure 2. Site result configuration**</span></span>

    ![Пример конфигурации сайта результатов](media/search-customizations-for-sharepoint/4f42a7c4-326b-4508-b9a7-e030ef34cd33.png)

4. <span data-ttu-id="06b94-136">Выберите команду **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="06b94-136">Choose  **Save**.</span></span>
    
<span data-ttu-id="06b94-137">Создание страницы результатов:</span><span class="sxs-lookup"><span data-stu-id="06b94-137">To create the results page:</span></span>

1. <span data-ttu-id="06b94-138">В меню **Параметры сайта** выберите **контент сайта**.</span><span class="sxs-lookup"><span data-stu-id="06b94-138">On the  **Site Settings** menu, select **Site contents**.</span></span>
    
2. <span data-ttu-id="06b94-139">Выберите **страницы**.</span><span class="sxs-lookup"><span data-stu-id="06b94-139">Select  **Pages**.</span></span>
    
3. <span data-ttu-id="06b94-140">Выберите **файлы**в библиотеке **страниц**  > **Новый документ** > **страницы**.</span><span class="sxs-lookup"><span data-stu-id="06b94-140">In the  **Pages** library, select **Files** > **New Document** > **Page**.</span></span>
    
4. <span data-ttu-id="06b94-141">На странице " **Создание страницы** " укажите «Каталог сайтов» для **заголовка** и «каталог_сайтов» для **URL-имя**.</span><span class="sxs-lookup"><span data-stu-id="06b94-141">On the  **Create Page** page, specify "Site Directory" for **Title** and "sitedirectory" for **URL Name**.</span></span>
    
5. <span data-ttu-id="06b94-142">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="06b94-142">Choose  **Create**.</span></span>
    
<span data-ttu-id="06b94-143">Чтобы изменить свойства веб-части результатов:</span><span class="sxs-lookup"><span data-stu-id="06b94-143">To edit the Results Web Part properties:</span></span>

1. <span data-ttu-id="06b94-144">На странице **Каталога веб-сайтов** выберите **Параметры** > **Изменить страницу**.</span><span class="sxs-lookup"><span data-stu-id="06b94-144">On the  **Site Directory** page, choose **Settings** > **Edit Page**.</span></span>
    
2. <span data-ttu-id="06b94-145">В **Веб-части результатов поиска**выберите в меню **Веб-части** и выберите **Изменить веб-часть**.</span><span class="sxs-lookup"><span data-stu-id="06b94-145">In the  **Search Results Web Part**, choose the  **Web Part** menu, and then choose **Edit Web Part**.</span></span>
    
    <span data-ttu-id="06b94-146">**На рисунке 3. Меню веб-части**</span><span class="sxs-lookup"><span data-stu-id="06b94-146">**Figure 3. Web Part menu**</span></span>

    ![Рис 3](media/search-customizations-for-sharepoint/1b01ac59-3bc1-42eb-a63d-61c2ad15cee4.png)

3. <span data-ttu-id="06b94-148">В области инструментов веб-части нажмите кнопку **Изменить запрос** , чтобы открыть построитель запросов.</span><span class="sxs-lookup"><span data-stu-id="06b94-148">In the Web Part tool pane, choose  **Change query** to open the Query Builder.</span></span>
    
4. <span data-ttu-id="06b94-149">В поле **текст запроса** введите следующие значения.`ContentClass:STS_Web OR ContentClass:STS_Site path:http://<YourServer>`</span><span class="sxs-lookup"><span data-stu-id="06b94-149">In the  **Query text** field, enter the following: `ContentClass:STS_Web OR ContentClass:STS_Site path:http://<YourServer>`</span></span>
    
5. <span data-ttu-id="06b94-150">Подтвердите правильность синтаксиса выберите **Пробный запрос** .</span><span class="sxs-lookup"><span data-stu-id="06b94-150">Choose  **Test query** to confirm that the syntax is correct.</span></span> <span data-ttu-id="06b94-151">В области **Предварительного просмотра результатов поиска** должны отображать дочерних сайтов на сайте, выбранные для _пути_ в **тексте запроса**.</span><span class="sxs-lookup"><span data-stu-id="06b94-151">The **Search Results Preview** pane should display subsites within the site you specified for _path_ in the **Query text**.</span></span>
    
    <span data-ttu-id="06b94-152">**На рисунке 4. Построитель запросов веб-части результатов поиска**</span><span class="sxs-lookup"><span data-stu-id="06b94-152">**Figure 4. Search results Web Part query builder**</span></span>

    ![Построитель запросов части web результатов поиска](media/search-customizations-for-sharepoint/7b55c821-4772-4874-bbcb-c757e2723599.png)

6. <span data-ttu-id="06b94-154">Нажмите **кнопку ОК** , чтобы закрыть построитель запросов.</span><span class="sxs-lookup"><span data-stu-id="06b94-154">Choose  **OK** to close the Query Builder.</span></span>
    
7. <span data-ttu-id="06b94-155">В области **Шаблоны отображения**выберите **типы результатов используется для отображения элементов**.</span><span class="sxs-lookup"><span data-stu-id="06b94-155">In  **Display Templates**, select  **Use result types to display items**.</span></span>
    
8. <span data-ttu-id="06b94-156">Выберите в раскрывающемся списке **тип результатов для элемента** **Базового каталога сайтов** .</span><span class="sxs-lookup"><span data-stu-id="06b94-156">Select  **Basic Site Directory** in the **Result type for item** drop-down list.</span></span>
    
9. <span data-ttu-id="06b94-157">В разделе **внешний вид** изменения **заголовка** «Сайты ли включить доступ».</span><span class="sxs-lookup"><span data-stu-id="06b94-157">In the  **Appearance** section, change the **Title** to "Sites I have access to".</span></span>
    
10. <span data-ttu-id="06b94-158">Нажмите **кнопку ОК** , чтобы сохранить изменения в веб-часть закрыть панель инструментов веб-части.</span><span class="sxs-lookup"><span data-stu-id="06b94-158">Choose  **OK** to save the changes to the Web Part and to close the Web Part tool pane.</span></span> <span data-ttu-id="06b94-159">На следующем рисунке показан пример страницы каталога сайтов на основе поиска.</span><span class="sxs-lookup"><span data-stu-id="06b94-159">The following figure shows an example of a search-based site directory page.</span></span>
    
    <span data-ttu-id="06b94-160">**На рисунке 5. Пример каталога сайтов на основе поиска Contoso**</span><span class="sxs-lookup"><span data-stu-id="06b94-160">**Figure 5. Contoso search-based site directory example**</span></span>

    ![Пример каталога сайтов на основе поиска Contoso](media/search-customizations-for-sharepoint/5d1317d5-2e82-4819-b5a4-5bb515898a7b.png)

## <a name="personalized-search-results"></a><span data-ttu-id="06b94-162">Результаты поиска индивидуально настроенных</span><span class="sxs-lookup"><span data-stu-id="06b94-162">Personalized search results</span></span>

<span data-ttu-id="06b94-163">Показать результаты поиска, предназначенных для пользователя, отправившего запрос поиска при индивидуально настроенных поиска.</span><span class="sxs-lookup"><span data-stu-id="06b94-163">Personalized search is when you show search results targeted to the user submitting the search request.</span></span> <span data-ttu-id="06b94-164">В этом разделе описываются некоторые сценарии для настраиваемого поиска и как их можно реализовать.</span><span class="sxs-lookup"><span data-stu-id="06b94-164">This section describes some scenarios for personalized search and how you might implement them.</span></span>

### <a name="your-news-scenario"></a><span data-ttu-id="06b94-165">Новости сценария</span><span class="sxs-lookup"><span data-stu-id="06b94-165">Your news scenario</span></span>

<span data-ttu-id="06b94-166">В этом сценарии создания надстройки поиска, который отображает соответствующий контент, например новости и события, предназначенных для пользователя.</span><span class="sxs-lookup"><span data-stu-id="06b94-166">In this scenario, you create a search add-in that shows relevant content, such as news and events, targeted to the user.</span></span>

<span data-ttu-id="06b94-167">**На рисунке 6. Новости сценария настраиваемого поиска**</span><span class="sxs-lookup"><span data-stu-id="06b94-167">**Figure 6. Your News personalized search scenario**</span></span>

![Новости сценария настраиваемого поиска](media/search-customizations-for-sharepoint/188af4d1-b8bb-4212-bfdb-c29a13f30286.png)

<span data-ttu-id="06b94-169">Для реализации сценария новости, используйте веб-части результатов поиска SharePoint и шаблоны для отображения по умолчанию для отображения информации новости, включая заголовок, описание и отображаемое изображение.</span><span class="sxs-lookup"><span data-stu-id="06b94-169">To implement the news scenario, use the SharePoint search results Web Part and default display templates to display the news information, including title, description, and rollup image.</span></span> <span data-ttu-id="06b94-170">Отображение первых 10 элементов новостей.</span><span class="sxs-lookup"><span data-stu-id="06b94-170">Show the first 10 news items.</span></span> <span data-ttu-id="06b94-171">При выборе пользователем отображаемое изображение, заголовок или чтение более ссылки, загружается страница статьи новостей.</span><span class="sxs-lookup"><span data-stu-id="06b94-171">When the user chooses the rollup image, title, or Read More link, the news article page is loaded.</span></span>

<span data-ttu-id="06b94-172">Кроме того можно создать поиска надстройки с помощью запроса API (CSOM или REST).</span><span class="sxs-lookup"><span data-stu-id="06b94-172">Alternatively, you can create a search add-in using the query API (CSOM or REST).</span></span> <span data-ttu-id="06b94-173">Можно сделать номер новостей для отображения настраивается с помощью свойства поиска надстройки.</span><span class="sxs-lookup"><span data-stu-id="06b94-173">You can make the number of news items to be displayed configurable by using the search add-in properties.</span></span>

<span data-ttu-id="06b94-174">Другая возможность — это использовать API запросов для добавления запроса кода API, которое извлекает непосредственно для макета страницы результатов поиска.</span><span class="sxs-lookup"><span data-stu-id="06b94-174">Another option is to use the query API to add the query API code that retrieves the search results directly to the page layout.</span></span>

<span data-ttu-id="06b94-175">Чтобы отобразить новости и события сведения, относящиеся к пользователю:</span><span class="sxs-lookup"><span data-stu-id="06b94-175">To display the news and event information specific to the user:</span></span>

1. <span data-ttu-id="06b94-176">Измените запрос для фильтрации результатов новости и события на основе свойств профиля пользователя как бизнес-единицы, региона и языка.</span><span class="sxs-lookup"><span data-stu-id="06b94-176">Modify the query to filter news and event results based on user profile properties like business unit, region, and language.</span></span>
    
2. <span data-ttu-id="06b94-177">Извлечь заголовок, описание, отображаемое изображение и свойства URL-адрес для элементов, новостей и событий.</span><span class="sxs-lookup"><span data-stu-id="06b94-177">Retrieve the Title, Description, rollup image, and URL properties for the news or event items.</span></span>
    
3. <span data-ttu-id="06b94-178">Реализация логики сортировки объединенный новости и события на основе свойства **Дата последнего изменения** .</span><span class="sxs-lookup"><span data-stu-id="06b94-178">Implement sorting logic for the combined news and events based on the  **LastModifiedDate** property.</span></span>

### <a name="upcoming-events-scenario"></a><span data-ttu-id="06b94-179">Сценарий Предстоящие мероприятия</span><span class="sxs-lookup"><span data-stu-id="06b94-179">Upcoming events scenario</span></span>

<span data-ttu-id="06b94-180">В этом сценарии надстройка поиска отображает соответствующие события, нацелено на пользователя.</span><span class="sxs-lookup"><span data-stu-id="06b94-180">In this scenario, the search add-in shows relevant events targeted to the user.</span></span>

<span data-ttu-id="06b94-181">**На рисунке 7. Предстоящие события сценария настраиваемого поиска**</span><span class="sxs-lookup"><span data-stu-id="06b94-181">**Figure 7. Upcoming Events personalized search scenario**</span></span>

![Предстоящие события сценария настраиваемого поиска](media/search-customizations-for-sharepoint/35afac63-b4e9-4d94-abc1-a5fa11cc2dbf.png)

<span data-ttu-id="06b94-183">Чтобы реализовать этот сценарий, можно настроить веб-части, чтобы изменить запрос для извлечения сведений о предстоящих событиях только результаты поиска SharePoint.</span><span class="sxs-lookup"><span data-stu-id="06b94-183">To implement this scenario, you can configure the SharePoint search results Web Part to change the query to only retrieve upcoming event information.</span></span> <span data-ttu-id="06b94-184">Чтобы сделать это, укажите `ContentClass:STS_ListItem_Events` для текста запроса в веб-части.</span><span class="sxs-lookup"><span data-stu-id="06b94-184">To do this, specify  `ContentClass:STS_ListItem_Events` for the Web Part's query text.</span></span> <span data-ttu-id="06b94-185">Чтобы изменить способ отображения результатов события, создайте пользовательское отображаемое шаблоны для отображения сведений о событиях.</span><span class="sxs-lookup"><span data-stu-id="06b94-185">To change how event results are displayed, create custom display templates to render the event information.</span></span>

<span data-ttu-id="06b94-186">Можно изменить шаблон отображения элемента, чтобы при выборе пользователем изображения, заголовок или чтение более ссылки, загрузки страницы данные события.</span><span class="sxs-lookup"><span data-stu-id="06b94-186">You can modify the item display template so that when the user chooses the image, title, or Read More link, the event information page is loaded.</span></span> <span data-ttu-id="06b94-187">Можно также изменить шаблон отображения элемента управления, чтобы при выборе **Более видеть**, Далее результаты 10 событий отображаются в веб-части.</span><span class="sxs-lookup"><span data-stu-id="06b94-187">You can also modify the control display template so that when the user chooses  **See More**, the next 10 event results are displayed in the Web Part.</span></span>

<span data-ttu-id="06b94-188">Можно также создать надстройки поиска, которая используется для получения даже результаты запроса API.</span><span class="sxs-lookup"><span data-stu-id="06b94-188">You can also create a search add-in that uses the query API to retrieve even results.</span></span> <span data-ttu-id="06b94-189">Можно настроить надстройки поиска для отображения по умолчанию только 10 последних предстоящие события, этот параметр настраивается через свойства поиска надстройки.</span><span class="sxs-lookup"><span data-stu-id="06b94-189">You can configure the search add-in to show, by default, only 10 of the latest upcoming events, but make this setting configurable through the search add-in properties.</span></span> 

### <a name="featured-news-scenario"></a><span data-ttu-id="06b94-190">Основные новости сценария</span><span class="sxs-lookup"><span data-stu-id="06b94-190">Featured news scenario</span></span>

<span data-ttu-id="06b94-191">В этом сценарии в поиска показаны результаты поиска, как основные содержимое, предназначенное для пользователей в местах, такие как корпоративной интрасети и подразделений целевые страницы.</span><span class="sxs-lookup"><span data-stu-id="06b94-191">In this scenario, the search add-in shows search results as featured content targeted to your users in places such as corporate intranet and divisional landing pages.</span></span> <span data-ttu-id="06b94-192">Вы можете реализовать с частью надстройки, которая содержит подключаемый модуль jQuery с HTML, которое использует службы поиска REST или запроса CSOM для получения результатов поиска из SharePoint и отобразить результаты.</span><span class="sxs-lookup"><span data-stu-id="06b94-192">You can implement this with an add-in part that contains a jQuery plugin with HTML, that uses the search REST service or the query CSOM to get search results from SharePoint and display the results.</span></span>

### <a name="code-sample-for-personalized-search"></a><span data-ttu-id="06b94-193">Пример кода для настраиваемого поиска</span><span class="sxs-lookup"><span data-stu-id="06b94-193">Code sample for personalized search</span></span>

<span data-ttu-id="06b94-194">[SharePoint 2013: результатов поиска в личные настройки в SharePoint Add-in](http://code.msdn.microsoft.com/SharePoint-2013-Personalizi-fb6ddcf9) приведен пример базового поиска и индивидуально настроенных результатов, использующего запрос поиска CSOM.</span><span class="sxs-lookup"><span data-stu-id="06b94-194">The [SharePoint 2013: Personalizing search results in a SharePoint Add-in](http://code.msdn.microsoft.com/SharePoint-2013-Personalizi-fb6ddcf9) sample shows a basic search example and a personalized search results example that uses the search query CSOM.</span></span> <span data-ttu-id="06b94-195">Пример базового поиска позволяет пользователю предоставлять поисковый фильтр для поиска на уровне клиента.</span><span class="sxs-lookup"><span data-stu-id="06b94-195">The basic search example lets the user provide a search filter to use for a tenant-wide search.</span></span> <span data-ttu-id="06b94-196">Сайты выполняется на этот фильтр пользовательские основе.</span><span class="sxs-lookup"><span data-stu-id="06b94-196">Sites are searched based on that user-supplied filter.</span></span>

<span data-ttu-id="06b94-197">В примере сначала возвращается контекста SharePoint с помощью класса **SharePointContextProvider** .</span><span class="sxs-lookup"><span data-stu-id="06b94-197">The example first gets SharePoint context by using the  **SharePointContextProvider** class.</span></span>

```
var spContext = SharePointContextProvider.Current.GetSharePointContext(Context);
```

<span data-ttu-id="06b94-198">Затем создает запрос, основанный на ввод пользователя.</span><span class="sxs-lookup"><span data-stu-id="06b94-198">Next, it builds the query based on what the user entered.</span></span> <span data-ttu-id="06b94-199">Ограничивает запрос для семейств веб-сайтов и затем вызывает метод **ProcessQuery** , передав контекст и запроса в вызове метода.</span><span class="sxs-lookup"><span data-stu-id="06b94-199">It restricts the query to site collections, and then calls the  **ProcessQuery** method, passing the context and the query in the method call.</span></span> <span data-ttu-id="06b94-200">Он возвращает результаты **ProcessQuery** в результате таблицы, который затем анализируется с помощью метода **FormatResults** .</span><span class="sxs-lookup"><span data-stu-id="06b94-200">It then returns the **ProcessQuery** results as a result table, which is then parsed by the **FormatResults** method.</span></span>

```
using (var clientContext = spContext.CreateUserClientContextForSPHost())
{
    string query = searchtext.Text + " contentclass:\"STS_Site\"";
    ClientResult<ResultTableCollection> results = ProcessQuery(clientContext, query);
    lblStatus1.Text = FormatResults(results);
}
```

<span data-ttu-id="06b94-201">Метод **ProcessQuery** создает **KeywordQuery** объект, представляющий поисковый запрос.</span><span class="sxs-lookup"><span data-stu-id="06b94-201">The  **ProcessQuery** method builds a **KeywordQuery** object that represents the search query.</span></span>

```
KeywordQuery keywordQuery = new KeywordQuery(ctx);
keywordQuery.QueryText = keywordQueryValue;
keywordQuery.RowLimit = 500;
keywordQuery.StartRow = 0;
keywordQuery.SelectProperties.Add("Title");
keywordQuery.SelectProperties.Add("SPSiteUrl");
keywordQuery.SelectProperties.Add("Description");
keywordQuery.SelectProperties.Add("WebTemplate");
keywordQuery.SortList.Add("SPSiteUrl", Microsoft.SharePoint.Client.Search.Query.SortDirection.Ascending);
```

<span data-ttu-id="06b94-202">Затем в поисковый запрос отправляется SharePoint путем вызова метода **ExecuteQuery_Client(Query)** .</span><span class="sxs-lookup"><span data-stu-id="06b94-202">The search query is then submitted to SharePoint by calling the  **ExecuteQuery_Client(Query)** method.</span></span> <span data-ttu-id="06b94-203">Результаты передаются в **ClientResult < T&gt; ** объектов.</span><span class="sxs-lookup"><span data-stu-id="06b94-203">Results are returned to the **ClientResult<T&gt;** object.</span></span>

```
SearchExecutor searchExec = new SearchExecutor(ctx);
ClientResult<ResultTableCollection> results = searchExec.ExecuteQuery(keywordQuery);
ctx.ExecuteQuery();
```

<span data-ttu-id="06b94-204">Метод **FormatResults** выполняется итерация по результатам и создает HTML-таблицы для отображения значений результатов.</span><span class="sxs-lookup"><span data-stu-id="06b94-204">The  **FormatResults** method iterates through the results and constructs an HTML table to display the result values.</span></span>

```
string responseHtml = "<h3>Results</h3>";
responseHtml += "<table>";
responseHtml += "<tr><th>Title</th><th>Site URL</th><th>Description</th><th>Template</th></tr>";
if (results.Value[0].RowCount > 0)
{
 foreach (var row in results.Value[0].ResultRows)
 {
   responseHtml += "<tr>";
   responseHtml += string.Format("<td>{0}</td>", row["Title"] != null ? row["Title"].ToString() : "");
   responseHtml += string.Format("<td>{0}</td>", row["SPSiteUrl"] != null ? row["SPSiteUrl"].ToString() : "");
   responseHtml += string.Format("<td>{0}</td>", row["Description"] != null ? row["Description"].ToString() : "");
   responseHtml += string.Format("<td>{0}</td>", row["WebTemplate"] != null ? row["WebTemplate"].ToString() : "");
   responseHtml += "</tr>";
 }
}
responseHtml += "</table>";
```

<span data-ttu-id="06b94-205">Метод **ResolveAdditionalFilter** проверяет «Apptest».</span><span class="sxs-lookup"><span data-stu-id="06b94-205">The  **ResolveAdditionalFilter** method checks for "Apptest".</span></span> <span data-ttu-id="06b94-206">Если он найден, список шаблонов сайтов любого типа возвращается в результатах поиска.</span><span class="sxs-lookup"><span data-stu-id="06b94-206">If it is found, a list of site templates of any type is returned in the search results.</span></span> <span data-ttu-id="06b94-207">Если он не найден, только службы маркеров безопасности веб-шаблоны возвращаются в результатах поиска.</span><span class="sxs-lookup"><span data-stu-id="06b94-207">If it is not found, only STS web templates are returned in the search results.</span></span>

```
private string ResolveAdditionalFilter(string aboutMeValue)
{
    if (!aboutMeValue.Contains("AppTest"))
    {
        return "WebTemplate=STS";
    }
    return "";
}
```

<span data-ttu-id="06b94-208">Затем создает запрос и вызывает методы **ProcessQuery** и **FormatResults** для извлечения, формат и отображения результатов поиска.</span><span class="sxs-lookup"><span data-stu-id="06b94-208">The example then constructs the query and calls the  **ProcessQuery** and **FormatResults** methods to retrieve, format, and display the search results.</span></span>

```
string query = "contentclass:\"STS_Site\" " + templateFilter;
ClientResult<ResultTableCollection> results = ProcessQuery(clientContext, query);
lblStatus2.Text = FormatResults(results);
```

<span data-ttu-id="06b94-209">Вы можете увидеть пользовательского интерфейса в данном примере на следующем рисунке.</span><span class="sxs-lookup"><span data-stu-id="06b94-209">You can see the UI for this example in the following figure.</span></span>

<span data-ttu-id="06b94-210">**На рисунке 8. Пример результатов поиска индивидуально настроенных пользовательского интерфейса**</span><span class="sxs-lookup"><span data-stu-id="06b94-210">**Figure 8. Personalized search results sample UI**</span></span>

![Пример результатов поиска индивидуально настроенных пользовательского интерфейса](media/search-customizations-for-sharepoint/8e1c412b-71a7-42e2-b9f3-b7d045df3bde.png)

## <a name="search-configuration-portability"></a><span data-ttu-id="06b94-212">Переносимость конфигурации поиска</span><span class="sxs-lookup"><span data-stu-id="06b94-212">Search configuration portability</span></span>

<span data-ttu-id="06b94-213">В SharePoint 2013 и SharePoint Online можно экспортировать и импортировать параметров конфигурации настраиваемого поиска между сайтов и семейств сайтов.</span><span class="sxs-lookup"><span data-stu-id="06b94-213">In SharePoint 2013 and SharePoint Online, you can export and import customized search configuration settings between site collections and sites.</span></span> <span data-ttu-id="06b94-214">Можно экспортировать только параметров конфигурации настраиваемого поиска на уровне приложения (SSA) службы поиска и вам следует использовать API-интерфейсы поиска для этого программными средствами.</span><span class="sxs-lookup"><span data-stu-id="06b94-214">You can only export customized search configuration settings at the Search service application (SSA) level, and you have to use the search APIs to do this programmatically.</span></span> <span data-ttu-id="06b94-215">Параметр экспорта недоступен в Интерфейсе пользователя SharePoint.</span><span class="sxs-lookup"><span data-stu-id="06b94-215">The export option is not available in the SharePoint UI.</span></span>

<span data-ttu-id="06b94-216">[SharePoint 2013: Импорт и экспорт параметры поиска для SharePoint Online](http://code.msdn.microsoft.com/SharePoint-2013-Import-and-6287b5ac) пример показано, как импортировать и экспортировать параметры поиска для сайта SharePoint Online с помощью CSOM поиска в консольное приложение.</span><span class="sxs-lookup"><span data-stu-id="06b94-216">The [SharePoint 2013: Import and Export search settings for SharePoint Online](http://code.msdn.microsoft.com/SharePoint-2013-Import-and-6287b5ac) sample show how to import and export search settings for a SharePoint Online site using the search CSOM in a console application.</span></span>

### <a name="configuration-settings-that-are-portable"></a><span data-ttu-id="06b94-217">Параметры конфигурации, которые можно переносить</span><span class="sxs-lookup"><span data-stu-id="06b94-217">Configuration settings that are portable</span></span>

<span data-ttu-id="06b94-218">При экспорте параметров конфигурации настраиваемого поиска SharePoint 2013 создает файл конфигурации поиска в формате XML.</span><span class="sxs-lookup"><span data-stu-id="06b94-218">When you export customized search configuration settings, SharePoint 2013 creates a search configuration file in XML format.</span></span> <span data-ttu-id="06b94-219">Этот файл конфигурации поиска включает в себя все параметры конфигурации экспортируемый настраиваемого поиска на SSA, семейства веб-сайтов или уровне сайтов, из которой начать экспорт.</span><span class="sxs-lookup"><span data-stu-id="06b94-219">This search configuration file includes all exportable customized search configuration settings at the SSA, site collection, or site level from where you start the export.</span></span> <span data-ttu-id="06b94-220">Файл конфигурации поиска для семейства веб-сайтов не содержит параметров конфигурации поиска из отдельных сайтов в пределах семейства веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="06b94-220">A search configuration file for a site collection does not contain search configuration settings from the individual sites within the site collection.</span></span>

<span data-ttu-id="06b94-221">При импорте файла конфигурации поиска SharePoint 2013 создает и включает каждый параметр конфигурации настраиваемого поиска в семейства веб-сайтов или сайта, с которой начать импорт.</span><span class="sxs-lookup"><span data-stu-id="06b94-221">When you import a search configuration file, SharePoint 2013 creates and enables each customized search configuration setting in the site collection or site from where you start the import.</span></span>

<span data-ttu-id="06b94-222">В таблице 1 перечислены параметры, которые можно экспортировать и импортировать, а также любые зависимости от других параметров конфигурации настраиваемого поиска.</span><span class="sxs-lookup"><span data-stu-id="06b94-222">Table 1 lists the settings that you can export and import and any dependencies on other customized search configuration settings.</span></span> <span data-ttu-id="06b94-223">Параметров конфигурации настраиваемого поиска зависит от параметр конфигурации настраиваемого поиска на другом уровне, необходимо экспортировать и импортировать параметры все соответствующие уровни.</span><span class="sxs-lookup"><span data-stu-id="06b94-223">If the customized search configuration settings depend on a customized search configuration setting at a different level, you must export and import settings at all relevant levels.</span></span>

<span data-ttu-id="06b94-224">**В таблице 1. Параметры поиска, которые можно экспортировать и импортировать**</span><span class="sxs-lookup"><span data-stu-id="06b94-224">**Table 1. Search settings that you can export and import**</span></span>

|<span data-ttu-id="06b94-225">**Параметр конфигурации**</span><span class="sxs-lookup"><span data-stu-id="06b94-225">**Configuration setting**</span></span>|<span data-ttu-id="06b94-226">**Зависимости**</span><span class="sxs-lookup"><span data-stu-id="06b94-226">**Dependencies**</span></span>|
|:-----|:-----|
|<span data-ttu-id="06b94-227">Правила запросов, включая blocs результатов, результатов повышенного уровня и сегменты пользователей</span><span class="sxs-lookup"><span data-stu-id="06b94-227">Query rules, including result blocs, promoted results, and user segments</span></span>|<span data-ttu-id="06b94-228">Источники результатов, типы результатов, схема поиска, модель ранжирования</span><span class="sxs-lookup"><span data-stu-id="06b94-228">Result sources, result types, search schema, ranking model</span></span>|
|<span data-ttu-id="06b94-229">Источники результатов</span><span class="sxs-lookup"><span data-stu-id="06b94-229">Result sources</span></span>|<span data-ttu-id="06b94-230">Схема поиска</span><span class="sxs-lookup"><span data-stu-id="06b94-230">Search schema</span></span>|
|<span data-ttu-id="06b94-231">Типы результатов</span><span class="sxs-lookup"><span data-stu-id="06b94-231">Result types</span></span>|<span data-ttu-id="06b94-232">Схема поиска, источники результатов, шаблоны отображения</span><span class="sxs-lookup"><span data-stu-id="06b94-232">Search schema, result sources, display templates</span></span>|
|<span data-ttu-id="06b94-233">Схема поиска</span><span class="sxs-lookup"><span data-stu-id="06b94-233">Search schema</span></span>|<span data-ttu-id="06b94-234">Нет</span><span class="sxs-lookup"><span data-stu-id="06b94-234">None</span></span>|
|<span data-ttu-id="06b94-235">Модель ранжирования</span><span class="sxs-lookup"><span data-stu-id="06b94-235">Ranking model</span></span>|<span data-ttu-id="06b94-236">Схема поиска</span><span class="sxs-lookup"><span data-stu-id="06b94-236">Search schema</span></span>|

<span data-ttu-id="06b94-237">Можно экспорт параметров конфигурации настраиваемого поиска из SSA и импорта параметров для сайтов и семейств веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="06b94-237">You can export customized search configuration settings from an SSA and import the settings to site collections and sites.</span></span> <span data-ttu-id="06b94-238">Однако нельзя импортировать параметров конфигурации настраиваемого поиска для SSA.</span><span class="sxs-lookup"><span data-stu-id="06b94-238">But you can't import customized search configuration settings to an SSA.</span></span> <span data-ttu-id="06b94-239">Невозможно экспортировать параметры конфигурации поиска по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="06b94-239">You also can't export the default search configuration settings.</span></span>

<span data-ttu-id="06b94-240">На сайте или уровне семейства сайтов можно экспортировать или импорта параметров конфигурации поиска с помощью пользовательского интерфейса SharePoint.</span><span class="sxs-lookup"><span data-stu-id="06b94-240">At the site or site collection level, you can export or import search configuration settings by using the SharePoint UI.</span></span> <span data-ttu-id="06b94-241">Эти параметры находятся в разделе " **Поиск** " на странице **Параметры сайта** .</span><span class="sxs-lookup"><span data-stu-id="06b94-241">These settings are located in the  **Search** section of the **Site Settings** page.</span></span>

<span data-ttu-id="06b94-242">**Параметры веб - поиска**</span><span class="sxs-lookup"><span data-stu-id="06b94-242">**Site Settings - Search**</span></span>

![Параметры веб - поиска](media/search-customizations-for-sharepoint/ada14bf4-d721-4974-ad50-a1f8ce01933f.png)

<span data-ttu-id="06b94-244">Эти параметры также доступны в разделе **Администрирование семейства веб-сайтов** .</span><span class="sxs-lookup"><span data-stu-id="06b94-244">These settings are also available in the  **Site Collection Administration** section.</span></span> <span data-ttu-id="06b94-245">Кроме того можно программно импорта и экспорта эти параметры с помощью CSOM поиска SharePoint 2013.</span><span class="sxs-lookup"><span data-stu-id="06b94-245">Alternatively, you can programmatically import and export these settings by using the SharePoint 2013 search CSOM.</span></span>

### <a name="search-configuration-files"></a><span data-ttu-id="06b94-246">Файлы конфигурации поиска</span><span class="sxs-lookup"><span data-stu-id="06b94-246">Search configuration files</span></span>

<span data-ttu-id="06b94-247">В следующей таблице перечислены файлы схемы, которые поддерживают конфигурации поиска.</span><span class="sxs-lookup"><span data-stu-id="06b94-247">The following table lists schema files that support a search configuration.</span></span> <span data-ttu-id="06b94-248">Сведения о формате схемы см [общий ресурс поиска параметры мобильности схемы](http://msdn.microsoft.com/en-us/library/office/dn627953%28v=office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="06b94-248">For information about the schema format, see [Share Point search settings portability schemas](http://msdn.microsoft.com/en-us/library/office/dn627953%28v=office.15%29.aspx).</span></span>

<span data-ttu-id="06b94-249">**Примечание:**  Файлы схемы можно загрузить из [http://download.microsoft.com/download/1/2/2/12204CDE-56A6-4B2F-9719-4EA25FDA7743/SP15_search_settings_portability_schema.zip](http://download.microsoft.com/download/1/2/2/12204CDE-56A6-4B2F-9719-4EA25FDA7743/SP15_search_settings_portability_schema.zip).</span><span class="sxs-lookup"><span data-stu-id="06b94-249">**Note:**  You can download the schema files from [http://download.microsoft.com/download/1/2/2/12204CDE-56A6-4B2F-9719-4EA25FDA7743/SP15_search_settings_portability_schema.zip](http://download.microsoft.com/download/1/2/2/12204CDE-56A6-4B2F-9719-4EA25FDA7743/SP15_search_settings_portability_schema.zip).</span></span> 

<span data-ttu-id="06b94-250">**В таблице 2. Переносимость схем параметры поиска**</span><span class="sxs-lookup"><span data-stu-id="06b94-250">**Table 2. Search settings portability schemas**</span></span>

|<span data-ttu-id="06b94-251">**Схемы**</span><span class="sxs-lookup"><span data-stu-id="06b94-251">**Schema**</span></span>|<span data-ttu-id="06b94-252">**Описание**</span><span class="sxs-lookup"><span data-stu-id="06b94-252">**Description**</span></span>|
|:-----|:-----|
|[<span data-ttu-id="06b94-253">SPS15XSDSearchSet1</span><span class="sxs-lookup"><span data-stu-id="06b94-253">SPS15XSDSearchSet1</span></span>](http://msdn.microsoft.com/en-us/library/office/dn639116%28v=office.15%29.aspx)|<span data-ttu-id="06b94-254">Задает XML, представляющий источники результатов.</span><span class="sxs-lookup"><span data-stu-id="06b94-254">Specifies XML that represents result sources.</span></span>|
|[<span data-ttu-id="06b94-255">SPS15XSDSearchSet2</span><span class="sxs-lookup"><span data-stu-id="06b94-255">SPS15XSDSearchSet2</span></span>](http://msdn.microsoft.com/en-us/library/office/dn639118%28v=office.15%29.aspx)|<span data-ttu-id="06b94-256">Задает XML, представляющий административные типы и члены для управления к экземпляру поиска SSA.</span><span class="sxs-lookup"><span data-stu-id="06b94-256">Specifies XML that represents administrative types and members for managing an SSA search instance.</span></span> <span data-ttu-id="06b94-257">Включает параметры правила свойства и типы элементов результатов.</span><span class="sxs-lookup"><span data-stu-id="06b94-257">This includes result item types and property rule settings.</span></span>|
|[<span data-ttu-id="06b94-258">SPS15XSDSearchSet3</span><span class="sxs-lookup"><span data-stu-id="06b94-258">SPS15XSDSearchSet3</span></span>](http://msdn.microsoft.com/en-us/library/office/dn639120%28v=office.15%29.aspx)|<span data-ttu-id="06b94-259">Задает XML, представляющий параметры, которые включают правила запросов, источники результатов, управляемых свойств, свойств для обхода и моделей ранжирования.</span><span class="sxs-lookup"><span data-stu-id="06b94-259">Specifies XML that represents settings that include query rules, result sources, managed properties, crawled properties, and ranking models.</span></span>|
|[<span data-ttu-id="06b94-260">SPS15XSDSearchSet4</span><span class="sxs-lookup"><span data-stu-id="06b94-260">SPS15XSDSearchSet4</span></span>](http://msdn.microsoft.com/en-us/library/office/dn639117%28v=office.15%29.aspx)|<span data-ttu-id="06b94-261">Задает XML, представляющий перечисления, используемые в другие схемы.</span><span class="sxs-lookup"><span data-stu-id="06b94-261">Specifies XML that represents enumerations used in other schemas.</span></span>|
|[<span data-ttu-id="06b94-262">SPS15XSDSearchSet5</span><span class="sxs-lookup"><span data-stu-id="06b94-262">SPS15XSDSearchSet5</span></span>](http://msdn.microsoft.com/en-us/library/office/dn639119%28v=office.15%29.aspx)|<span data-ttu-id="06b94-263">Задает XML, представляющий перечисления как **ResultType** , используемые в другие схемы.</span><span class="sxs-lookup"><span data-stu-id="06b94-263">Specifies XML that represents enumerations like  **ResultType** that are used in other schemas.</span></span>|
|[<span data-ttu-id="06b94-264">SPS15XSDSearchSet6</span><span class="sxs-lookup"><span data-stu-id="06b94-264">SPS15XSDSearchSet6</span></span>](http://msdn.microsoft.com/en-us/library/office/dn639115%28v=office.15%29.aspx)|<span data-ttu-id="06b94-265">Задает XML, представляющий перечисления, используемые в схеме **Microsoft.Office.Server.Search.Administration** .</span><span class="sxs-lookup"><span data-stu-id="06b94-265">Specifies XML that represents enumerations used in the  **Microsoft.Office.Server.Search.Administration** schema.</span></span>|

### <a name="using-csom-to-port-configuration-settings"></a><span data-ttu-id="06b94-266">С помощью CSOM к параметрам конфигурации порта</span><span class="sxs-lookup"><span data-stu-id="06b94-266">Using CSOM to port configuration settings</span></span>

<span data-ttu-id="06b94-267">CSOM API, которые необходимы для импорта и экспорта параметров конфигурации поиска находятся в **SearchConfigurationPortability** классов в пространстве имен **Microsoft.SharePoint.Client.Search.Portability** .</span><span class="sxs-lookup"><span data-stu-id="06b94-267">The CSOM APIs that you need in order to import and export your search configuration settings are in the  **SearchConfigurationPortability** class in the **Microsoft.SharePoint.Client.Search.Portability** namespace.</span></span>

<span data-ttu-id="06b94-268">В следующем примере кода показано, как для экспорта параметров конфигурации поиска с сайта.</span><span class="sxs-lookup"><span data-stu-id="06b94-268">The following code example shows how to export a site's search configuration settings.</span></span>

```
private static void ExportSearchSettings(ClientContext context, string settingsFile)
{
   SearchConfigurationPortability sconfig = new SearchConfigurationPortability(context);
   SearchObjectOwner owner = new SearchObjectOwner(context, SearchObjectLevel.SPWeb);
   ClientResult<string> configresults = sconfig.ExportSearchConfiguration(owner);
   context.ExecuteQuery();
   string results = configresults.Value;
   System.IO.File.WriteAllText(settingsFile, results);
}
```

<span data-ttu-id="06b94-269">Следующий код демонстрирует Импорт параметров конфигурации поиска с сайта.</span><span class="sxs-lookup"><span data-stu-id="06b94-269">The following code shows how to import a site's search configuration settings.</span></span>

```
private static void ImportSearchSettings(ClientContext context, string settingsFile)
{
   SearchConfigurationPortability sconfig = new SearchConfigurationPortability(context);
   SearchObjectOwner owner = new SearchObjectOwner(context, SearchObjectLevel.SPWeb);
   sconfig.ImportSearchConfiguration(owner, System.IO.File.ReadAllText(settingsFile));
   context.ExecuteQuery();            
}
```

## <a name="additional-resources"></a><span data-ttu-id="06b94-270">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="06b94-270">Additional resources</span></span>
<span data-ttu-id="06b94-271"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="06b94-271"></span></span>

- [<span data-ttu-id="06b94-272">Решения для поиска в SharePoint 2013 и SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="06b94-272">Search solutions in SharePoint 2013 and SharePoint Online</span></span>](search-solutions-in-sharepoint-2013-and-sharepoint-online.md)
    
- [<span data-ttu-id="06b94-273">SharePoint 2013: Импорт и экспорт параметры поиска для SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="06b94-273">SharePoint 2013: Import and Export search settings for SharePoint Online</span></span>](http://code.msdn.microsoft.com/SharePoint-2013-Import-and-6287b5ac)
    
- [<span data-ttu-id="06b94-274">SharePoint 2013: Настройка поиска результатов в SharePoint Add-in</span><span class="sxs-lookup"><span data-stu-id="06b94-274">SharePoint 2013: Personalizing search results in a SharePoint Add-in</span></span>](http://code.msdn.microsoft.com/SharePoint-2013-Personalizi-fb6ddcf9)
