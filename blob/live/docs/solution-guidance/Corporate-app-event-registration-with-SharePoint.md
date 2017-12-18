---
title: "Корпоративный события приложения интеграция с SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: 959fea4e8fcdfe5c73a9a53e6c5da09c325d781d
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="corporate-event-app-integration-with-sharepoint"></a><span data-ttu-id="17de5-102">Корпоративный события приложения интеграция с SharePoint</span><span class="sxs-lookup"><span data-stu-id="17de5-102">Corporate event app integration with SharePoint</span></span>

<span data-ttu-id="17de5-103">Интеграция надстроек для SharePoint в бизнес-операции с помощью размещение у поставщика в надстройке, который можно реализовать несколько сложных бизнес-задач.</span><span class="sxs-lookup"><span data-stu-id="17de5-103">Integrate add-ins for SharePoint into your business operations by using a provider-hosted add-in that can implement multiple complex business tasks.</span></span>

<span data-ttu-id="17de5-104">_**Область применения:** Office 365 | SharePoint 2013 | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="17de5-104">_**Applies to:** Office 365 | SharePoint 2013 | SharePoint Online_</span></span>

<span data-ttu-id="17de5-105">Пример [BusinessApps.CorporateEventApp](https://github.com/SharePoint/PnP/tree/master/Solutions/BusinessApps.CorporateEventsApp) показано, как реализовать систему управления централизованного корпоративных событий как размещение у поставщика надстройки, которая интегрируется с существующими приложениями бизнес (LOB).</span><span class="sxs-lookup"><span data-stu-id="17de5-105">The  [BusinessApps.CorporateEventApp](https://github.com/SharePoint/PnP/tree/master/Solutions/BusinessApps.CorporateEventsApp) sample shows you how to implement a centralized corporate events management system as a provider-hosted add-in that integrates with your existing line-of-business (LOB) applications.</span></span>

<span data-ttu-id="17de5-106">В частности [BusinessApps.CorporateEventApp](https://github.com/SharePoint/PnP/tree/master/Solutions/BusinessApps.CorporateEventsApp) примере показано, как реализовать веб-приложения ASP.NET, взаимодействующий с SharePoint в качестве хранилища данных для сущностей LOB.</span><span class="sxs-lookup"><span data-stu-id="17de5-106">More specifically, the  [BusinessApps.CorporateEventApp](https://github.com/SharePoint/PnP/tree/master/Solutions/BusinessApps.CorporateEventsApp) sample shows you how to implement an ASP.NET web application that interacts with SharePoint as a data store for LOB entities.</span></span> <span data-ttu-id="17de5-107">Он также показано, как реализовать несколько действий в сложных бизнес-задачу с одной размещением у поставщика надстройки.</span><span class="sxs-lookup"><span data-stu-id="17de5-107">It also shows you how to implement multiple steps in a complex business task with a single provider-hosted add-in.</span></span>
<span data-ttu-id="17de5-108">В этом примере приложения реализует систему централизованного управления, состоящую из объектов SharePoint (списков и типов контента).</span><span class="sxs-lookup"><span data-stu-id="17de5-108">This sample app implements a centralized management system that consists of SharePoint entities (lists and content types).</span></span> <span data-ttu-id="17de5-109">Для каждого нового типа контента он создает соответствующие LOB сущности в веб-приложение ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="17de5-109">For each new content type, it creates corresponding LOB entities in an ASP.NET web application.</span></span> <span data-ttu-id="17de5-110">Компоненты веб-приложения, как удаленного выполнения размещены надстройки из частей в интерфейсе SharePoint, а также страниц, запущены на удаленного веб-узла.</span><span class="sxs-lookup"><span data-stu-id="17de5-110">Components of the web application run as remotely hosted add-in parts within the SharePoint interface and also as pages running entirely on the remote web host.</span></span> <span data-ttu-id="17de5-111">Надстройка переопределяет начальная страница по умолчанию для сайта SharePoint, чтобы его можно представить фирменной символикой пользовательского интерфейса на домашней странице сайта.</span><span class="sxs-lookup"><span data-stu-id="17de5-111">The add-in overrides the default welcome page for your SharePoint site so that it can present a custom-branded interface on the site home page.</span></span>

## <a name="using-the-businessappscorporateeventapp-sample"></a><span data-ttu-id="17de5-112">Использование примера BusinessApps.CorporateEventApp</span><span class="sxs-lookup"><span data-stu-id="17de5-112">Using the BusinessApps.CorporateEventApp sample</span></span>

<span data-ttu-id="17de5-113">При запуске примера приложения BusinessApps.CorporateEventApp на домашнюю страницу предоставляет возможность возможность настройки образца.</span><span class="sxs-lookup"><span data-stu-id="17de5-113">When you start the BusinessApps.CorporateEventApp sample app, the Home page provides an option for you to configure the sample.</span></span> <span data-ttu-id="17de5-114">Также вы указывает на количество ресурсов для получения дополнительных сведений.</span><span class="sxs-lookup"><span data-stu-id="17de5-114">It also points you to a number of resources for more information.</span></span>

<span data-ttu-id="17de5-115">При выборе **Пуск конфигурации**вы перейдите на страницу конфигурации, как показано на рисунке 1.</span><span class="sxs-lookup"><span data-stu-id="17de5-115">When you choose  **Start configuration**, you go to the Configuration page, as shown in Figure 1.</span></span> <span data-ttu-id="17de5-116">При выборе **инициализации хранилища данных** на странице Настройка примера развертывает объектов SharePoint и образцы данных, которые поддерживают примера.</span><span class="sxs-lookup"><span data-stu-id="17de5-116">When you choose  **Initialize the data store** on the Configuration page, the sample deploys the SharePoint entities and sample data that support the sample.</span></span>

<span data-ttu-id="17de5-117">**На рисунке 1. Страница настройки**</span><span class="sxs-lookup"><span data-stu-id="17de5-117">**Figure 1. Configuration page**</span></span>

![Снимок экрана, которая отображает экран данных initialize](media/ee213035-b014-45cc-94f4-d8c1c58a047e.png)

<span data-ttu-id="17de5-119">После инициализации хранилища данных, можно вернуться на сайт для просмотра новой начальной страницы (страница EventsHome.aspx), которой заполняется две веб-части, которые добавить в развертывание, как показано на рисунке 2.</span><span class="sxs-lookup"><span data-stu-id="17de5-119">After you initialize the data store, you can go back to your site to see a new welcome page (the EventsHome.aspx page), which is populated by two web parts that the add-in deployed, as shown in Figure 2.</span></span> <span data-ttu-id="17de5-120">В левом столбце вы увидите четыре новых списков, установленные приложением, с демонстрационных данных выполняется заполнение списка корпоративных событий.</span><span class="sxs-lookup"><span data-stu-id="17de5-120">In the left column, you'll see the four new lists installed by the app, The Corporate Events list is populated by sample data.</span></span>

<span data-ttu-id="17de5-121">**На рисунке 2. Начальная страница с веб-частей инициализации**</span><span class="sxs-lookup"><span data-stu-id="17de5-121">**Figure 2. Welcome page with web parts initialized**</span></span>

![Снимок экрана, показывающий начальной страницы надстройка с веб-частями развернут](media/aa4dbd35-70f0-43c2-845c-615632090c44.png)

<span data-ttu-id="17de5-123">Каждой веб-части содержит ссылки на каждый из отображения событий, где можно просмотреть сведения о событии.</span><span class="sxs-lookup"><span data-stu-id="17de5-123">Each web part contains links to each of the displayed events, where you can see the event details.</span></span> <span data-ttu-id="17de5-124">При выборе ссылки на страницу сведений события запускает отдельно на удаленном узле, как показано на рисунке 3.</span><span class="sxs-lookup"><span data-stu-id="17de5-124">When you choose a link, the event details page runs separately on the remote host, as shown in Figure 3.</span></span> <span data-ttu-id="17de5-125">Вы можете **вернуться к сайта** на странице для возврата на сайте SharePoint, а также чтобы зарегистрироваться для события.</span><span class="sxs-lookup"><span data-stu-id="17de5-125">You can choose  **Back to Site** on the page to return to the SharePoint site, and also to register yourself for the event.</span></span>

<span data-ttu-id="17de5-126">**На рисунке 3. Страница сведений о событии**</span><span class="sxs-lookup"><span data-stu-id="17de5-126">**Figure 3. Event details page**</span></span>

![Снимок экрана, которая отображает пользовательский Интерфейс надстройки с корпоративной события экран сведения о событии](media/b967e4ec-e0a6-4aae-af81-e22b92cef0d9.png)

<span data-ttu-id="17de5-128">Страница регистрации также работает отдельно на удаленном узле, а также содержит ссылку на сайт узла SharePoint (см).</span><span class="sxs-lookup"><span data-stu-id="17de5-128">The registration page also runs separately on the remote host, and also contains a link back to the SharePoint host site (see Figure 4).</span></span> <span data-ttu-id="17de5-129">После завершения регистрации для события ваше имя будет отображаться в списке только что установленного **Регистрация событий** .</span><span class="sxs-lookup"><span data-stu-id="17de5-129">When you finish registering for the event, your name will appear on the newly installed  **Event Registration** list.</span></span>

<span data-ttu-id="17de5-130">**На рисунке 4. Страница регистрации событий**</span><span class="sxs-lookup"><span data-stu-id="17de5-130">**Figure 4. Event registration page**</span></span>

![Снимок экрана, которая отображает экран регистрации событий корпоративных событий приложения](media/d2ec4156-5806-4b20-ab5b-3d25fcc33f1a.png)

<span data-ttu-id="17de5-132">Файл Models\DataInitializer.cs содержит код, который выполняется при нажатии этой кнопки.</span><span class="sxs-lookup"><span data-stu-id="17de5-132">The Models\DataInitializer.cs file contains the code that runs when you choose this button.</span></span> <span data-ttu-id="17de5-133">Код в этом файле создает и развертывает четыре новых списков SharePoint, наряду с четырьмя соответствующих типов контента:</span><span class="sxs-lookup"><span data-stu-id="17de5-133">The code in this file creates and deploys four new SharePoint lists, along with four corresponding content types:</span></span>

- <span data-ttu-id="17de5-134">Корпоративных событий</span><span class="sxs-lookup"><span data-stu-id="17de5-134">Corporate events</span></span>
    
- <span data-ttu-id="17de5-135">Регистрация событий</span><span class="sxs-lookup"><span data-stu-id="17de5-135">Event registration</span></span>
    
- <span data-ttu-id="17de5-136">Докладчики</span><span class="sxs-lookup"><span data-stu-id="17de5-136">Event speakers</span></span>
    
- <span data-ttu-id="17de5-137">Сеансы событий</span><span class="sxs-lookup"><span data-stu-id="17de5-137">Event sessions</span></span>
    
<span data-ttu-id="17de5-138">Код в этом файле использует метод, аналогичный тому, который используется в образце [Core.ModifyPages](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ModifyPages) , чтобы добавить пользовательскую страницу на сайте.</span><span class="sxs-lookup"><span data-stu-id="17de5-138">The code in this file uses a method similar to the one that is used in the  [Core.ModifyPages](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ModifyPages) sample to add a custom page to the site.</span></span>

```
            // Create default wiki page.
            web.AddWikiPage("Site Pages", "EventsHome.aspx");
AddWikiPage is an extension method from the Core.DevPnPCore project to add a new page to the site. This new page also becomes the new WelcomePage for the site. It also prepares to add the web parts to this page.
            var welcomePage = "SitePages/EventsHome.aspx";
            var serverRelativeUrl = UrlUtility.Combine(web.ServerRelativeUrl, welcomePage);

            File webPartPage = web.GetFileByServerRelativeUrl(serverRelativeUrl);

            if (webPartPage == null) {
                return;
            }

            web.Context.Load(webPartPage);
            web.Context.Load(webPartPage.ListItemAllFields);
            web.Context.Load(web.RootFolder);
            web.Context.ExecuteQuery();

            web.RootFolder.WelcomePage = welcomePage;
            web.RootFolder.Update();
            web.Context.ExecuteQuery();

```

<span data-ttu-id="17de5-139">Файл Models\DataInitializer.cs также определяет XML-код для обоих веб-частей, которые отображаются на новой странице приветствия и затем добавляет каждой из них на страницу.</span><span class="sxs-lookup"><span data-stu-id="17de5-139">The Models\DataInitializer.cs file also defines the XML for both web parts that are displayed on the new welcome page and then adds each one to the page.</span></span> <span data-ttu-id="17de5-140">В следующих примерах показано, как это работает для веб-части известных событий.</span><span class="sxs-lookup"><span data-stu-id="17de5-140">The following examples show how this works for the Featured Events web part.</span></span>

<span data-ttu-id="17de5-141">**Определение веб-части XML**</span><span class="sxs-lookup"><span data-stu-id="17de5-141">**Define web part XML**</span></span>

```XML
            var webPart1 = new WebPartEntity(){
                WebPartXml = @"<webParts>
  <webPart xmlns='http://schemas.microsoft.com/WebPart/v3'>
    <metaData>
      <type name='Microsoft.SharePoint.WebPartPages.ClientWebPart, Microsoft.SharePoint, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c' />
      <importErrorMessage>Cannot import this Web Part.</importErrorMessage>
    </metaData>
    <data>
      <properties>
        <property name='Description' type='string'>Displays featured events</property>
        <property name='FeatureId' type='System.Guid, mscorlib, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089'>3a6d7f41-2de8-4e69-b4b4-0325bd56b32c</property>
        <property name='Title' type='string'>Featured Events</property>
        <property name='ProductWebId' type='System.Guid, mscorlib, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089'>12ae648f-27db-4a97-9c63-37155d3ace1e</property>
        <property name='WebPartName' type='string'>FeaturedEvents</property>
        <property name='ProductId' type='System.Guid, mscorlib, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089'>3a6d7f41-2de8-4e69-b4b4-0325bd56b32b</property>
        <property name='ChromeState' type='chromestate'>Normal</property>
      </properties>
    </data>
  </webPart>
</webParts>",
                WebPartIndex = 0,
                WebPartTitle = "Featured Events",
                WebPartZone = "Rich Content"
            };

```

<span data-ttu-id="17de5-142">**Добавить веб-части на страницу**</span><span class="sxs-lookup"><span data-stu-id="17de5-142">**Add the web parts to the page**</span></span>

```XML
            var limitedWebPartManager = webPartPage.GetLimitedWebPartManager(Microsoft.SharePoint.Client.WebParts.PersonalizationScope.Shared);
            web.Context.Load(limitedWebPartManager.WebParts);
            web.Context.ExecuteQuery();

            for (var i = 0; i < limitedWebPartManager.WebParts.Count; i++) {
                limitedWebPartManager.WebParts[i].DeleteWebPart();
            }
            web.Context.ExecuteQuery();

            var oWebPartDefinition1 = limitedWebPartManager.ImportWebPart(webPart1.WebPartXml);
            var oWebPartDefinition2 = limitedWebPartManager.ImportWebPart(webPart2.WebPartXml);
            var wpdNew1 = limitedWebPartManager.AddWebPart(oWebPartDefinition1.WebPart, webPart1.WebPartZone, webPart1.WebPartIndex);
            var wpdNew2 = limitedWebPartManager.AddWebPart(oWebPartDefinition2.WebPart, webPart2.WebPartZone, webPart2.WebPartIndex);
            web.Context.Load(wpdNew1);
            web.Context.Load(wpdNew2);
            web.Context.ExecuteQuery();

```

<span data-ttu-id="17de5-143">В каталоге модели веб-проекта можно заметить, что это веб-приложение MVC ASP.NET содержит четыре именами классов, которые соответствуют списков и типов контента, установлено приложение:</span><span class="sxs-lookup"><span data-stu-id="17de5-143">In the Models directory of your web project, you'll notice that this MVC ASP.NET web application contains four class names that correspond to the lists and content types that the app installed:</span></span>

- <span data-ttu-id="17de5-144">Event.cs (корпоративных событий)</span><span class="sxs-lookup"><span data-stu-id="17de5-144">Event.cs (Corporate Events)</span></span>
    
- <span data-ttu-id="17de5-145">Registration.cs (Регистрация событий)</span><span class="sxs-lookup"><span data-stu-id="17de5-145">Registration.cs (Event Registration)</span></span>
    
- <span data-ttu-id="17de5-146">Session.cs (события сеансов)</span><span class="sxs-lookup"><span data-stu-id="17de5-146">Session.cs (Event Sessions)</span></span>
    
- <span data-ttu-id="17de5-147">Speaker.cs (докладчики)</span><span class="sxs-lookup"><span data-stu-id="17de5-147">Speaker.cs (Event Speakers)</span></span>
    
<span data-ttu-id="17de5-148">Эти четыре классы и их соответствующие типы содержимого SharePoint вместе составляют четыре LOB записей, использованных в этой надстройки.</span><span class="sxs-lookup"><span data-stu-id="17de5-148">These four classes and their corresponding SharePoint content types together make up the four LOB entities used in this add-in.</span></span>

<span data-ttu-id="17de5-149">Файл DataInitializer.cs добавляет демонстрационных данных для списка **Корпоративных событий** , создав образец объектов **событий** , которые соответствуют с типом контента **Корпоративных событий** и приложение добавляется в список **Корпоративных событий** .</span><span class="sxs-lookup"><span data-stu-id="17de5-149">The DataInitializer.cs file adds sample data for the  **Corporate Events** list by creating sample **Event** objects that correspond with the **Corporate Events** content type and which the app adds to the **Corporate Events** list.</span></span> <span data-ttu-id="17de5-150">При регистрации события приложение создает объект **регистрации** , соответствующий с типом контента **Регистрация событий** и приложение добавляется в список **Регистрации событий** .</span><span class="sxs-lookup"><span data-stu-id="17de5-150">When you register for an event, the app creates a **Registration** object that corresponds with the **Event Registration** content type and that the app adds to the **Event Registration** list.</span></span> <span data-ttu-id="17de5-151">Образец имеет еще не реализованы полностью объектов **сеанса** и **динамик** , поэтому приложения в настоящее время не работает с объектами.</span><span class="sxs-lookup"><span data-stu-id="17de5-151">The sample has not yet fully implemented the **Session** and **Speaker** objects, so the app currently doesn't work with those objects.</span></span>

<span data-ttu-id="17de5-152">В следующей таблице приведены свойства необходимость реализовываться классы, наследующие от абстрактного класса **BaseListItem** .</span><span class="sxs-lookup"><span data-stu-id="17de5-152">The following table lists the properties need to be implemented by the classes that inherit from the  **BaseListItem** abstract class.</span></span>

<span data-ttu-id="17de5-153">** В таблице 1.</span><span class="sxs-lookup"><span data-stu-id="17de5-153">**Table 1.</span></span> <span data-ttu-id="17de5-154">Методы для реализации в классы, унаследованные от ** BaseListItem ***</span><span class="sxs-lookup"><span data-stu-id="17de5-154">Methods to implement in classes inheriting from  **BaseListItem****</span></span>

|<span data-ttu-id="17de5-155">**Элемент  **</span><span class="sxs-lookup"><span data-stu-id="17de5-155">**Member**</span></span>|<span data-ttu-id="17de5-156">**Описание**</span><span class="sxs-lookup"><span data-stu-id="17de5-156">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="17de5-157">**Это элемент ContentTypeName**</span><span class="sxs-lookup"><span data-stu-id="17de5-157">**ContentTypeName**</span></span>|<span data-ttu-id="17de5-158">Получает тип контента, связанный с элементом.</span><span class="sxs-lookup"><span data-stu-id="17de5-158">Gets the content type that is associated with the item.</span></span> <span data-ttu-id="17de5-159">Если значение null, тип контента библиотеки по умолчанию будет назначен элемент после ее сохранения.</span><span class="sxs-lookup"><span data-stu-id="17de5-159">If null, the default library content type will be assigned to the item when you save it.</span></span>|
|<span data-ttu-id="17de5-160">**FieldInternalNames**</span><span class="sxs-lookup"><span data-stu-id="17de5-160">**FieldInternalNames**</span></span>|<span data-ttu-id="17de5-161">Список имен полей, которые могут быть кэшированы для повышения производительности при использовании для проверки данных поля до сохранения.</span><span class="sxs-lookup"><span data-stu-id="17de5-161">A list of field names that can be cached to improve performance when used for checking field data prior to save.</span></span>|
|<span data-ttu-id="17de5-162">ListTitle</span><span class="sxs-lookup"><span data-stu-id="17de5-162">ListTitle</span></span>|<span data-ttu-id="17de5-163">Получает заголовок списка (с учетом регистра).</span><span class="sxs-lookup"><span data-stu-id="17de5-163">Gets the title of the list (case sensitive).</span></span>|

<span data-ttu-id="17de5-164">В следующей таблице перечислены методы, которые должны быть реализованы классами, наследующие от абстрактного класса **BaseListItem** .</span><span class="sxs-lookup"><span data-stu-id="17de5-164">The following table lists the methods that have to be implemented by the classes that inherit from the  **BaseListItem** abstract class.</span></span> <span data-ttu-id="17de5-165">Эти методы возвращают параметры, которые необходимо задать [преобразуемых типов](https://msdn.microsoft.com/en-us/library/75dwhxf7%28v=vs.110%29.aspx) , чтобы их можно использовать на разных платформах.</span><span class="sxs-lookup"><span data-stu-id="17de5-165">These methods return parameters that should be set to [blittable types](https://msdn.microsoft.com/en-us/library/75dwhxf7%28v=vs.110%29.aspx) so that they can be used on multiple platforms.</span></span>

 <span data-ttu-id="17de5-166">**В таблице 2. Методы, возвращающие преобразуемых типов**</span><span class="sxs-lookup"><span data-stu-id="17de5-166">**Table 2. Methods that return blittable types**</span></span>

|<span data-ttu-id="17de5-167">**Метод**</span><span class="sxs-lookup"><span data-stu-id="17de5-167">**Method**</span></span>|<span data-ttu-id="17de5-168">**Описание**</span><span class="sxs-lookup"><span data-stu-id="17de5-168">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="17de5-169">**ReadProperties(ListItem)**</span><span class="sxs-lookup"><span data-stu-id="17de5-169">**ReadProperties(ListItem)**</span></span>|<span data-ttu-id="17de5-170">Считывает свойства из объекта **ListItem** , с помощью методов **BaseGet** и **BaseGetEnum** и присваивает им свойства подкласса.</span><span class="sxs-lookup"><span data-stu-id="17de5-170">Reads properties from the **ListItem** object using the **BaseGet** and **BaseGetEnum** methods and assigns them to properties of the subclass.</span></span>|
|<span data-ttu-id="17de5-171">**SetProperties(ListItem)**</span><span class="sxs-lookup"><span data-stu-id="17de5-171">**SetProperties(ListItem)**</span></span>|<span data-ttu-id="17de5-172">Задает свойства **ListItem** объекта, с помощью методов **BaseSet** и **BaseSetTaxonomyField** абстрактного класса.</span><span class="sxs-lookup"><span data-stu-id="17de5-172">Sets properties on the **ListItem** object using the **BaseSet** and **BaseSetTaxonomyField** methods of the abstract class.</span></span>|

<span data-ttu-id="17de5-173">В следующей таблице перечислены вспомогательные методы от класса **BaseListItem** , необходимо реализовать методы **ReadProperties** и **SetProperties** подклассов.</span><span class="sxs-lookup"><span data-stu-id="17de5-173">The following table lists the helper methods from the  **BaseListItem** class that the subclasses need to implement the **ReadProperties** and **SetProperties** methods.</span></span>

<span data-ttu-id="17de5-174">**В таблице 3. BaseListItem вспомогательные методы**</span><span class="sxs-lookup"><span data-stu-id="17de5-174">**Table 3. BaseListItem helper methods**</span></span>

|<span data-ttu-id="17de5-175">**Вспомогательный метод**</span><span class="sxs-lookup"><span data-stu-id="17de5-175">**Helper method**</span></span>|<span data-ttu-id="17de5-176">**Описание**</span><span class="sxs-lookup"><span data-stu-id="17de5-176">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="17de5-177">**BaseGet (элемент ListItem, внутреннееимя строка)**</span><span class="sxs-lookup"><span data-stu-id="17de5-177">**BaseGet(ListItem item, string internalName)**</span></span>|<span data-ttu-id="17de5-178">Получает свойство, определенного параметром *внутреннееимя* из **ListItem** и возвращает их универсальный тип **T**.</span><span class="sxs-lookup"><span data-stu-id="17de5-178">Gets the property defined by the *internalName* parameter from **ListItem** and returns them of generic type **T**.</span></span>|
|<span data-ttu-id="17de5-179">**BaseSet (элемент ListItem, внутреннееимя string, значение объекта)**</span><span class="sxs-lookup"><span data-stu-id="17de5-179">**BaseSet(ListItem item, string internalName, object value)**</span></span>|<span data-ttu-id="17de5-180">Задает свойства **ListItem** , определенного параметром *внутреннееимя* .</span><span class="sxs-lookup"><span data-stu-id="17de5-180">Sets the **ListItem** property defined by the *internalName* parameter.</span></span>|
|<span data-ttu-id="17de5-181">**BaseSetTaxonomyField (элемент ListItem, внутреннееимя строка, строка метки, Guid termId)**</span><span class="sxs-lookup"><span data-stu-id="17de5-181">**BaseSetTaxonomyField(ListItem item, string internalName, string label, Guid termId)**</span></span>|<span data-ttu-id="17de5-182">Задает поле таксономии **ListItem** , определенные с помощью параметров *внутреннееимя* и *termId* .</span><span class="sxs-lookup"><span data-stu-id="17de5-182">Sets the **ListItem** taxonomy field defined by the *internalName* and *termId* parameters.</span></span>|
|<span data-ttu-id="17de5-183">**BaseGetEnum (элемент ListItem, внутреннееимя string, T defaultValue)**</span><span class="sxs-lookup"><span data-stu-id="17de5-183">**BaseGetEnum(ListItem item, string internalName, T defaultValue)**</span></span>|<span data-ttu-id="17de5-184">Получает значение перечисления свойства, определенного параметром *внутреннееимя* .</span><span class="sxs-lookup"><span data-stu-id="17de5-184">Gets the value of the enum property defined by the *internalName* parameter.</span></span> <span data-ttu-id="17de5-185">Возвращает значение параметра *значение по умолчанию* , если свойство не задано.</span><span class="sxs-lookup"><span data-stu-id="17de5-185">Returns the value of the *defaultValue* parameter if the property is not set.</span></span>|

<span data-ttu-id="17de5-186">Файл Event.cs содержит следующие реализации методов **ReadProperties** и **SetProperties** .</span><span class="sxs-lookup"><span data-stu-id="17de5-186">The Event.cs file contains the following implementations of the  **ReadProperties** and **SetProperties** methods.</span></span>

<span data-ttu-id="17de5-187">**ReadProperties**</span><span class="sxs-lookup"><span data-stu-id="17de5-187">**ReadProperties**</span></span>

```C#
        protected override void ReadProperties(ListItem item) {
            RegisteredEventId = BaseGet<string>(item, FIELD_REGISTERED_EVENT_ID);
            Description = BaseGet<string>(item, FIELD_DESCRIPTION);
            Category = BaseGet<string>(item, FIELD_CATEGORY);
            EventDate = BaseGet<DateTime?>(item, FIELD_DATE);
            Location = BaseGet<string>(item, FIELD_LOCATION);
            ContactEmail = BaseGet<string>(item, FIELD_CONTACT_EMAIL);
            Status = BaseGetEnum<EventStatus>(item, FIELD_STATUS);
            var imageUrl = BaseGet<FieldUrlValue>(item, FIELD_IMAGE_URL);

            if (imageUrl != null)
                ImageUrl = imageUrl.Url;
        }
SetProperties:
        protected override void SetProperties(ListItem item) {
            BaseSet(item, FIELD_REGISTERED_EVENT_ID, RegisteredEventId);
            BaseSet(item, FIELD_DESCRIPTION, Description);
            BaseSet(item, FIELD_CATEGORY, Category);
            BaseSet(item, FIELD_DATE, EventDate);
            BaseSet(item, FIELD_LOCATION, Location);
            BaseSet(item, FIELD_CONTACT_EMAIL, ContactEmail);
            BaseSet(item, FIELD_STATUS, Status.ToEnumDescription());
            BaseSet(item, FIELD_IMAGE_URL, ImageUrl);
        }

```

<span data-ttu-id="17de5-188">В следующих примерах кода показано определение базовых методов **BaseGet** и **BaseSet** в BaseListItem.cs.</span><span class="sxs-lookup"><span data-stu-id="17de5-188">The following code examples show how the underlying  **BaseGet** and **BaseSet** methods are defined in BaseListItem.cs.</span></span>

<span data-ttu-id="17de5-189">**BaseGet**</span><span class="sxs-lookup"><span data-stu-id="17de5-189">**BaseGet**</span></span>

```
protected T BaseGet<T>(ListItem item, string internalName){
            var field = _fields[internalName.ToLowerInvariant()];
            var value = item[field.InternalName];
            return (T)value;
        }

```

<span data-ttu-id="17de5-190">**BaseSet**</span><span class="sxs-lookup"><span data-stu-id="17de5-190">**BaseSet**</span></span>

```
protected void BaseSet(ListItem item, string internalName, object value) {
            if (_fields.ContainsKey(internalName)) {
                var field = _fields[internalName.ToLowerInvariant()];

                if (field is FieldUrl &amp;&amp; value is string) {
                    var urlValue = new FieldUrlValue() {
                        Url = value.ToString()
                    };
                    value = urlValue;
                }
            }
            item[internalName] = value;
        }
```

<span data-ttu-id="17de5-191">Класс **BaseListItem** также содержит **Сохранить** метод, который используется для сохранения каждого объекта LOB, приложение создает и управляет.</span><span class="sxs-lookup"><span data-stu-id="17de5-191">The  **BaseListItem** class also contains a **Save** method that is used to save each LOB entity that the app creates and manipulates.</span></span> <span data-ttu-id="17de5-192">Этот метод загружает список и определяет, имеет ли текущий элемент идентификатор, который больше 0.</span><span class="sxs-lookup"><span data-stu-id="17de5-192">This method loads the list and determines whether the current item has an ID that is greater than 0.</span></span> <span data-ttu-id="17de5-193">Если идентификатор не больше 0, предполагается, что он не является допустимым и создает новый элемент списка.</span><span class="sxs-lookup"><span data-stu-id="17de5-193">If the ID is not greater than 0, it assumes that it's not valid and creates a new list item.</span></span> <span data-ttu-id="17de5-194">Он использует метод **SetProperties** следует задать свойства **ListItem** и затем задает свойства подкласса с помощью метода **ReadProperties** .</span><span class="sxs-lookup"><span data-stu-id="17de5-194">It uses the **SetProperties** method to set properties on the **ListItem** and then sets the properties on the subclass by using the **ReadProperties** method.</span></span>

```
public void Save(Web web) {
            var context = web.Context;
            var list = web.GetListByTitle(ListTitle);
            if (!IsNew &amp;&amp; Id > 0) {
                ListItem = list.GetItemById(Id);
            }
            else {
                var listItemCreationInfo = new ListItemCreationInformation();
                ListItem = list.AddItem(listItemCreationInfo);
            }

            // Ensure that the fields have been loaded.
            EnsureFieldsRetrieved(ListItem);

            // Set the properties on the list item.
            SetProperties(ListItem);
            BaseSet(ListItem, TITLE, Title);

            // Use if you want to override the created/modified date.
            //BaseSet(ListItem, CREATED, Created);
            //BaseSet(ListItem, MODIFIED, Modified);

            ListItem.Update();

            if (!string.IsNullOrEmpty(ContentTypeName)) {
                var contentType = list.GetContentTypeByName(ContentTypeName);
                if (contentType != null)
                    BaseSet(ListItem, "ContentTypeId", contentType.Id.StringValue);
            }

            ListItem.Update();

            // Execute the batch.
            context.ExecuteQuery();

            // Reload the properties.
            ListItem.RefreshLoad();
            UpdateBaseProperties(ListItem);
            ReadProperties(ListItem);
        }

```

## <a name="see-also"></a><span data-ttu-id="17de5-195">См. также</span><span class="sxs-lookup"><span data-stu-id="17de5-195">See also</span></span>
<span data-ttu-id="17de5-196"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="17de5-196"></span></span>

-  [<span data-ttu-id="17de5-197">Надстройки составного бизнеса для SharePoint 2013 и SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="17de5-197">Composite business add-ins for SharePoint 2013 and SharePoint Online</span></span>](Composite-buisness-apps-for-SharePoint.md)
    
-  [<span data-ttu-id="17de5-198">Пример Core.ModifyPages</span><span class="sxs-lookup"><span data-stu-id="17de5-198">Core.ModifyPages sample</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ModifyPages)
    
-  [<span data-ttu-id="17de5-199">Пример Provisioning.Pages</span><span class="sxs-lookup"><span data-stu-id="17de5-199">Provisioning.Pages sample</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.Pages)
    
-  [<span data-ttu-id="17de5-200">Пример OfficeDevPnP.Core</span><span class="sxs-lookup"><span data-stu-id="17de5-200">OfficeDevPnP.Core sample</span></span>](https://github.com/SharePoint/PnP-Sites-Core/tree/master/Core)
    
