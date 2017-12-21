---
title: "Новые возможности разработки сайтов в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: ac1e9891-5ce9-4707-84e5-6e2fc02fda6b
ms.openlocfilehash: 541fb06089538563b54e48f0a6c0741fa73fa811
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="whats-new-with-sharepoint-site-development"></a><span data-ttu-id="915f9-102">Новые возможности разработки сайтов в SharePoint</span><span class="sxs-lookup"><span data-stu-id="915f9-102">What's new with SharePoint site development</span></span>
<span data-ttu-id="915f9-103">Информация о новой модели разработки и публикации сайтов в SharePoint, которая позволяет создавать сайты публикации.</span><span class="sxs-lookup"><span data-stu-id="915f9-103">Learn about the new site authoring and publishing model in SharePoint that enables you to create publishing sites.</span></span>
## <a name="introduction-to-site-publishing-for-designers-and-developers-in-sharepoint"></a><span data-ttu-id="915f9-104">Общие сведения о публикации сайтов в SharePoint для конструкторов и разработчиков</span><span class="sxs-lookup"><span data-stu-id="915f9-104">Introduction to site publishing for designers and developers in SharePoint</span></span>
<span data-ttu-id="915f9-105"><a name="SP15_WhatsNewSiteDevelopment_IntroductionToSitePublishing"> </a></span><span class="sxs-lookup"><span data-stu-id="915f9-105"><a name="SP15_WhatsNewSiteDevelopment_IntroductionToSitePublishing"> </a></span></span>

<span data-ttu-id="915f9-106">Ниже перечислены новые возможности в SharePoint и поддержке рабочего процесса по созданию сайта управления корпоративным информационным содержимым (ECM) для сайтов публикации.</span><span class="sxs-lookup"><span data-stu-id="915f9-106">The following features are new in SharePoint and support the enterprise content management (ECM) site creation workflow for publishing sites.</span></span>
  
    
    

### <a name="client-programming-models-for-publishing-site-development"></a><span data-ttu-id="915f9-107">Клиентская модель программирования для разработки сайтов публикации</span><span class="sxs-lookup"><span data-stu-id="915f9-107">Client programming models for publishing site development</span></span>

<span data-ttu-id="915f9-p101">Для разработки настраиваемых сайтов, компонентов сайта, элементов фирменной символики и поведения в SharePoint можно использовать клиентскую объектную модель .NET (CSOM), Silverlight и модель программирования JavaScript. Большинство интерфейсов API, доступных для программирования сервера .NET, доступны в соответствующих клиентах .NET (CSOM), Silverlight и сборках JavaScript. Кроме того, в некоторых случаях соответствующие интерфейсы API доступны в библиотеках Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="915f9-p101">In SharePoint, you can use the .NET client object model (CSOM), Silverlight, and JavaScript programming models to develop custom sites, site components, branding elements, and behavior. Most APIs available for .NET server programming are available in corresponding .NET client (CSOM), Silverlight, and JavaScript assemblies. In some cases, corresponding APIs are also available in Windows Phone libraries.</span></span>
  
    
    
<span data-ttu-id="915f9-p102">Более подробную информацию можно просмотреть на справочных домашних страницах для сайтов и содержимого для  [сервера .NET](http://msdn.microsoft.com/library/8a93e838-234c-41d8-b990-7ac1a415dd5e%28Office.15%29.aspx),  [клиента .NET](http://msdn.microsoft.com/library/e6542022-a459-4c3b-aee0-e350c6397139%28Office.15%29.aspx) и [JavaScript](http://msdn.microsoft.com/library/1ead2f8d-a541-4a50-89fa-f195f2ba14e5%28Office.15%29.aspx). Либо ознакомьтесь со  [справочной домашней страницей](http://msdn.microsoft.com/library/7940ba4e-f6f0-4bc0-b995-ceb2d358ca0d%28Office.15%29.aspx), чтобы начать с самого начала и затем просмотреть содержимое каждой модели программирования.</span><span class="sxs-lookup"><span data-stu-id="915f9-p102">To learn more, see the reference home pages for sites and content for  [.NET server](http://msdn.microsoft.com/library/8a93e838-234c-41d8-b990-7ac1a415dd5e%28Office.15%29.aspx),  [.NET client](http://msdn.microsoft.com/library/e6542022-a459-4c3b-aee0-e350c6397139%28Office.15%29.aspx), and  [JavaScript](http://msdn.microsoft.com/library/1ead2f8d-a541-4a50-89fa-f195f2ba14e5%28Office.15%29.aspx). Or, start with the  [reference home page](http://msdn.microsoft.com/library/7940ba4e-f6f0-4bc0-b995-ceb2d358ca0d%28Office.15%29.aspx) if you want to start at the top and then explore the contents of each programming model.</span></span>
  
    
    

### <a name="using-publishing-and-taxonomy-apis-with-the-new-sharepoint-app-model"></a><span data-ttu-id="915f9-113">Использование интерфейсов API для публикации и таксономии с новой моделью приложений SharePoint</span><span class="sxs-lookup"><span data-stu-id="915f9-113">Using publishing and taxonomy APIs with the new SharePoint app model</span></span>

<span data-ttu-id="915f9-114">Вы можете создать в Надстройки SharePoint пользовательский код клиента и сервера, который расширит функциональные возможности публикации и таксономии SharePoint, которые доступны пользователям через пользовательский интерфейс.</span><span class="sxs-lookup"><span data-stu-id="915f9-114">You can write custom client and server code in SharePoint Add-ins that extend the SharePoint publishing and taxonomy functionality that's available to users through the user interface (UI).</span></span> 
  
    
    
<span data-ttu-id="915f9-115">Некоторые идеи по разработке приложений, улучшающих публикацию сайтов, включают опросы, приложения для управления учетными записями, поддержку электронной коммерции, приложения, которые интегрируют на сайты публикации функции социальных сетей и внешние данные, добавление содержимого на ваши сайты внешними подрядчиками и дополнительные мобильные приложения.</span><span class="sxs-lookup"><span data-stu-id="915f9-115">Some ideas for developing apps that enhance site publishing include surveys, account management apps, eCommerce support, apps that integrate social features and external data into publishing sites, outsourced content additions to your sites, and mobile companion apps.</span></span>
  
    
    

## <a name="authoring-design-and-branding-features"></a><span data-ttu-id="915f9-116">Возможности для разработки, проектирования и создания фирменной символики</span><span class="sxs-lookup"><span data-stu-id="915f9-116">Authoring, design, and branding features</span></span>
<span data-ttu-id="915f9-117"><a name="SP15_WhatsNewSiteDevelopment_AuthoringAndBranding"> </a></span><span class="sxs-lookup"><span data-stu-id="915f9-117"><a name="SP15_WhatsNewSiteDevelopment_AuthoringAndBranding"> </a></span></span>

<span data-ttu-id="915f9-118">SharePoint содержит функции и интерфейсы API, которые можно использовать для разработки, проектирования, создания фирменной символики, а также для расширения вашего сайта, элементов дизайна и символики, поведения.</span><span class="sxs-lookup"><span data-stu-id="915f9-118">SharePoint includes features and APIs that you can use to author, design, brand, and extend your site, site design and branding elements, and behaviors.</span></span> 
  
    
    

### <a name="design-manager"></a><span data-ttu-id="915f9-119">Дизайнер</span><span class="sxs-lookup"><span data-stu-id="915f9-119">Design Manager</span></span>

<span data-ttu-id="915f9-p103">В предыдущих версиях SharePoint создание фирменной символики сайта требовало специальных технических знаний о том, какие заполнители контента требуются для эталонной страницы или как эталонная страница реализует некоторые классы стиля. SharePoint представляет  [Дизайнера](overview-of-design-manager-in-sharepoint.md)  новый интерфейс и ядро для управления всеми аспектами оформления вашего сайта SharePoint. Дизайнер находится на сайте верхнего уровня для вашего семейства веб-сайтов. Он является частью шаблона семейства веб-сайтов портала публикации в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="915f9-p103">In previous versions of SharePoint, branding a site required specific technical expertise about things like what content placeholders are required on a master page, or how a master page implements certain classes of styles. SharePoint introduces  [Design Manager](overview-of-design-manager-in-sharepoint.md)—a new interface and central hub for managing all aspects of branding your SharePoint site. You can find the Design Manager in the top-level site for your site collection. It is a part of the Publishing Portal site collection template in SharePoint.</span></span>
  
    
    
<span data-ttu-id="915f9-124">Компонент "Дизайнер" позволяет пошагово создавать проектные ресурсы, которые можно использовать для фирменного оформления сайтов.</span><span class="sxs-lookup"><span data-stu-id="915f9-124">Design Manager enables a step-by-step approach for creating design assets that you can use to brand sites.</span></span> <span data-ttu-id="915f9-125">Отправляйте проектные ресурсы — изображения, HTML, CSS и т. д. — и создавайте эталонные страницы и макеты страниц.</span><span class="sxs-lookup"><span data-stu-id="915f9-125">Upload design assets—images, HTML, CSS, and so on—and then create your master pages and page layouts.</span></span> <span data-ttu-id="915f9-126">Во время разработки вы можете увидеть, как будет выглядеть оформление, в клиентском редакторе кода или на сервере.</span><span class="sxs-lookup"><span data-stu-id="915f9-126">You can preview how your design looks either in a client-side code editor or on the server as you are designing it.</span></span> <span data-ttu-id="915f9-127">Вы можете добавлять настраиваемые компоненты SharePoint и элементы ленты с помощью пользовательского интерфейса компонента "Дизайнер".</span><span class="sxs-lookup"><span data-stu-id="915f9-127">You can add custom SharePoint components and ribbon elements by using the Design Manager UI.</span></span> <span data-ttu-id="915f9-128">"Дизайнер" создает [фрагменты](sharepoint-design-manager-snippets.md) HTML-кода, которые может использовать любое средство веб-разработки. Он просто отрисовывает HTML и игнорирует разметку ASP.NET и SharePoint (SharePoint отрисовывает только разметку ASP.NET и SharePoint и игнорирует HTML).</span><span class="sxs-lookup"><span data-stu-id="915f9-128">The Design Manager generates HTML  [snippets](sharepoint-design-manager-snippets.md) that can be used by any web design tool—it renders HTML and ignores ASP.NET and SharePoint markup (while SharePoint renders only ASP.NET and SharePoint markup and ignores HTML.md).</span></span>
  
    
    
<span data-ttu-id="915f9-129">Вы можете воспользоваться своим опытом программирования на HTML, CSS и JavaScript при разработке эталонных страниц HTML и макетов страниц HTML в любом редакторе HTML.</span><span class="sxs-lookup"><span data-stu-id="915f9-129">You can use your expertise in HTML, CSS, and JavaScript to design master pages in HTML, and design HTML page layouts in the HTML editor of your choice.</span></span> <span data-ttu-id="915f9-130">Чтобы подключить ваш любимый инструмент для разработки и оформления к сайту SharePoint, [сопоставьте сетевой диск](how-to-map-a-network-drive-to-the-sharepoint-master-page-gallery.md), а затем редактируйте файл SharePoint, как будто это локальный файл.</span><span class="sxs-lookup"><span data-stu-id="915f9-130">To connect your favorite authoring and design tool to your SharePoint site,  [map a network drive](how-to-map-a-network-drive-to-the-sharepoint-master-page-gallery.md) and then edit the SharePoint file as if it were a local file.</span></span> <span data-ttu-id="915f9-131">Когда оформление вашего сайта будет готово, отправьте HTML-файл и вспомогательные файлы, а затем [преобразуйте HTML-файл в эталонную страницу ASP.NET (MASTER-файл)](how-to-convert-an-html-file-into-a-master-page-in-sharepoint.md) с помощью компонента "Дизайнер".</span><span class="sxs-lookup"><span data-stu-id="915f9-131">When your site design is ready, upload the HTML and supporting files and use Design Manager to [convert the HTML file into an ASP.NET master page (.master.md) file](how-to-convert-an-html-file-into-a-master-page-in-sharepoint.md).</span></span> <span data-ttu-id="915f9-132">Теперь [примените эталонную страницу](how-to-apply-a-master-page-to-a-site-in-sharepoint.md) к сайту SharePoint.</span><span class="sxs-lookup"><span data-stu-id="915f9-132">Now,  [apply the master page](how-to-apply-a-master-page-to-a-site-in-sharepoint.md) to your SharePoint site.</span></span> <span data-ttu-id="915f9-133">С помощью компонента "Дизайнер" [создайте макет страницы](how-to-create-a-page-layout-in-sharepoint.md). Его версия в формате HTML будет автоматически связана с соответствующей страницей ASP.NET (ASPX-файлом), которую интерпретирует SharePoint.</span><span class="sxs-lookup"><span data-stu-id="915f9-133">Use Design Manager to [create a new page layout](how-to-create-a-page-layout-in-sharepoint.md), and the HTML version of it is automatically associated with the corresponding ASP.NET page (.aspx file.md) that SharePoint interprets.</span></span> 
  
    
    
<span data-ttu-id="915f9-p106">После преобразования своих HTML-файлов вы можете использовать HTML-редактор, чтобы продолжить улучшать свой макет, выполнять предварительный просмотр файлов и сохранять их. Каждый раз при сохранении HTML-версий файлов эталонных страниц или макетов страниц SharePoint автоматически обновляет связанные эталонные страницы и макеты страниц SharePoint для отражения внесенных вами изменений.</span><span class="sxs-lookup"><span data-stu-id="915f9-p106">After you convert your HTML files, you can use your HTML editor to continue to refine your design, preview your files, and save them. Every time you save the HTML versions of the master page or page layout files, SharePoint automatically updates the associated SharePoint master page and page layouts to reflect your changes.</span></span> 
  
    
    
<span data-ttu-id="915f9-136">С помощью Дизайнера можно только изменять HTML-файлы. Тогда как вы можете и дальше создавать пользовательские эталонные страницы и макеты страниц благодаря навыкам разработки в ASP.NET и SharePoint, Дизайнер позволяет создавать прекрасные сайты, не имея знаний разработчика SharePoint.</span><span class="sxs-lookup"><span data-stu-id="915f9-136">With Design Manager, you only have to edit the HTML files—while you can continue to write custom master pages and page layouts using your ASP.NET and SharePoint development skills, Design Manager enables you to design great sites without SharePoint developer expertise.</span></span>
  
    
    
<span data-ttu-id="915f9-p107">SharePoint также включает HTML-версии нескольких эталонных страниц и макетов страниц, поэтому при желании вы можете использовать эти базовые шаблоны. Если вы хотите начать работу с этих файлов, создайте копию HTML-файла (связанный файл ASP.NET вам придется создавать самостоятельно), а затем измените HTML-файл как обычно. Вы также можете запустить базовый шаблон с помощью параметра **эталонная страница из минимального шаблона**, который автоматически создает связанный MASTER-файл.</span><span class="sxs-lookup"><span data-stu-id="915f9-p107">If you prefer, SharePoint also includes HTML versions of several master pages and page layouts that you can use as starter templates. If you want to start from these files, create a copy of the HTML file (the associated ASP.NET file will be taken care of for you), and then edit the HTML file as you normally would. You can also start from just a basic template by using the **master page from minimal template** option, which automatically creates the associated .master file.</span></span>
  
    
    

### <a name="snippet-gallery"></a><span data-ttu-id="915f9-140">Коллекция фрагментов кода</span><span class="sxs-lookup"><span data-stu-id="915f9-140">Snippet Gallery</span></span>

<span data-ttu-id="915f9-p108">SharePoint содержит большое количество готовых к использованию компонентов (например, веб-части и элементы управления), которые можно добавить на страницы своего сайта. Например, вставив в эталонную страницу такой компонент SharePoint, как поле поиска или элемент управления навигацией, вы можете легко и быстро создать большое количество функций на своих страницах.</span><span class="sxs-lookup"><span data-stu-id="915f9-p108">SharePoint contains many ready-to-use components—like Web Parts and controls—that you can add to your site's pages. For example, by inserting a SharePoint component such as a search box or navigation control into your HTML master page, you can quickly and easily build a lot of functionality into your pages.</span></span>
  
    
    
<span data-ttu-id="915f9-143">На ленте, в группе **Коллекция фрагментов**, вы можете выбрать компонент, настроить его свойства и обновить фрагмент, скопировать созданный фрагмент кода HTML и вставить его в HTML-файл.</span><span class="sxs-lookup"><span data-stu-id="915f9-143">On the ribbon, in the **Snippet Gallery** group, you can select a component, configure its properties and update the snippet, copy the HTML snippet that's generated, and paste that HTML snippet into your HTML file.</span></span> <span data-ttu-id="915f9-144">С помощью фрагмента кода HTML можно заранее увидеть компонент в высоком качестве как на стороне сервера, так и в любом редакторе HTML.</span><span class="sxs-lookup"><span data-stu-id="915f9-144">The HTML snippet gives you a high-fidelity preview of that component, both in the server-side preview and in your HTML editor of choice.</span></span> <span data-ttu-id="915f9-145">Добавив компоненты SharePoint в HTML-файлы, вы можете оформить их в своем фирменном стиле с помощью CSS.</span><span class="sxs-lookup"><span data-stu-id="915f9-145">After you add SharePoint components to your HTML files, you can use CSS to fully brand them.</span></span> <span data-ttu-id="915f9-146">Как и при любом другом изменении HTML-файла, после добавления компонентов SharePoint и придания им фирменного облика изменения автоматически синхронизируются с соответствующей эталонной страницей или макетом страницы.</span><span class="sxs-lookup"><span data-stu-id="915f9-146">And just like any update to the HTML file, after you add SharePoint components and brand them, the changes are automatically synchronized to the associated master page or page layout.</span></span> <span data-ttu-id="915f9-147">Фрагменты кода HTML автоматически преобразуются в компоненты SharePoint.</span><span class="sxs-lookup"><span data-stu-id="915f9-147">The HTML snippets are automatically converted into SharePoint components.</span></span>
  
    
    
 <span data-ttu-id="915f9-p110">Является ваш HTML-файл эталонной страницей или макетом страницы, коллекция фрагментов кода покажет вам необходимые компоненты. Если вы не видите нужный вам фрагмент, вы можете создать фрагмент HTML-кода разметки ASP.NET и добавить его на свою эталонную страницу или в макет страницы.</span><span class="sxs-lookup"><span data-stu-id="915f9-p110">Whether your HTML file is a master page or a page layout, the Snippet Gallery shows you the components that you need. If you don't see the snippet you want, you can create an HTML snippet of ASP.NET markup and add that to your HTML master page or page layout.</span></span>
  
    
    
<span data-ttu-id="915f9-p111">Дизайнер создает фрагменты HTML-кода, которые можно использовать любым средством веб-разработки; он просто отрисовывает HTML и игнорирует ASP.NET и разметку SharePoint. SharePoint отрисовывает только ASP.NET и разметку SharePoint и игнорирует HTML.</span><span class="sxs-lookup"><span data-stu-id="915f9-p111">Design Manager generates HTML snippets that can be used by any web design tool—it just renders HTML and ignores ASP.NET and SharePoint markup. SharePoint renders only ASP.NET and SharePoint markup and ignores HTML.</span></span>
  
    
    

### <a name="device-channels"></a><span data-ttu-id="915f9-152">Каналы устройств</span><span class="sxs-lookup"><span data-stu-id="915f9-152">Device channels</span></span>

<span data-ttu-id="915f9-p112">В Дизайнере вы можете создавать  [каналы устройств](sharepoint-design-manager-device-channels.md), а затем сопоставлять их с мобильными устройствами или браузерами с помощью подстрок строки агента пользователя для каждого входящего устройства. Устройство может принадлежать нескольким каналам, поэтому каналы можно ранжировать. Например, если вы создаете канал устройства для смартфонов и Windows Phone 8, вы можете ранжировать каналы таким образом, чтобы устройства под управлением Windows Phone 8 получали канал, предназначенный специально для них, тогда как другие смартфоны получали содержимое, связанное с каналом для смартфонов.</span><span class="sxs-lookup"><span data-stu-id="915f9-p112">In Design Manager, you create  [device channels](sharepoint-design-manager-device-channels.md), and then you map them to mobile devices or browsers by using substrings of each incoming device's user agent string. A device can belong to multiple channels, so channels can be ranked. For example, if you create device channels for "smart phones" and "Windows Phone 8", you can rank the channels so that devices running Windows Phone 8 get the channel specifically assigned to them, while all other smart phones get content associated with the "smart phones" channel.</span></span>
  
    
    
<span data-ttu-id="915f9-p113">После определения каналов сопоставьте каждому из них эталонную страницу. Эта эталонная страница может ссылаться на CSS-файл, отличный от CSS, используемого эталонной страницей для канала по умолчанию. Все созданные макеты страниц будут работать со всеми созданными вами каналами. Чтобы дифференцировать структуру макетов страницы между каналами, используйте элемент управления **Панель канала устройства**.</span><span class="sxs-lookup"><span data-stu-id="915f9-p113">After you define channels, map a master page to each one. This master page can reference a different CSS file than the master page for the default channel. All page layouts that you create will work with all of the channels that you create; to differentiate page layout designs between channels, use the **Device Channel Panel** control.</span></span>
  
    
    
<span data-ttu-id="915f9-p114">Сайты публикации в SharePoint оптимизированы для мобильной разработки. Чтобы определить каналы для одного или нескольких устройств, можно использовать функцию каналов устройств, которая предоставляет тонкое управление опытом взаимодействия пользователей мобильных устройств с вашим веб-сайтом. Вы можете назначить альтернативные эталонные страницы для каждого канала, задав им уникальный хром. Можно включать в канал или исключать из него части любого макета страницы и просматривать изменение структуры мобильного канала по мере его разработки. Каналы устройств разработаны с учетом оптимизации для поисковых систем (SEO). Вы можете использовать их, чтобы преобразовать внешний вид существующих страниц для поддержки мобильных сценариев.</span><span class="sxs-lookup"><span data-stu-id="915f9-p114">Publishing sites in SharePoint are optimized for mobile development. You can use the device channels feature to define channels for one or more devices—giving you finely-tuned control over how mobile users experience your site. You can assign an alternate master page to each channel, giving it a unique chrome. You can choose to include or exclude portions of any page layout in a channel and preview how mobile channel design is progressing while it is being developed. Device channels are designed with search engine optimization (SEO) in mind. You can use them to transform the look and feel of existing pages to support mobile scenarios.</span></span>
  
    
    
<span data-ttu-id="915f9-p115">Каналы можно использовать для принудительного отображения определенных отрисовок на указанных устройствах. Такие каналы называются принудительными. Они полезны в мобильных сценариях, где вы определяете отрисовки, оптимальные для указанных мобильных устройств.</span><span class="sxs-lookup"><span data-stu-id="915f9-p115">You can use channels to force specific renderings to appear on specific devices—this is called forcing channels. This is useful in mobile scenarios where you have defined a rendering that is optimal for a specific mobile device.</span></span>
  
    
    

### <a name="device-channel-panel-control"></a><span data-ttu-id="915f9-167">Элемент управления панелями каналов устройств</span><span class="sxs-lookup"><span data-stu-id="915f9-167">Device Channel Panel control</span></span>

<span data-ttu-id="915f9-p116">Панель каналов устройств  это новый элемент управления, который можно включить в макет страницы, чтобы управлять содержимым, отображаемым на этом канале. Панель каналов устройств является контейнером, который сопоставлен одному или нескольким каналам. Если при отрисовке страницы активны один или несколько этих каналов, отрисовывается все содержимое панели каналов устройств. Эта панель помогает определять, когда включать в состав указанное содержимое для указанных каналов.</span><span class="sxs-lookup"><span data-stu-id="915f9-p116">The Device Channel Panel is a new control that you can include in a page layout to control what content is rendered in which channel. The Device Channel Panel is a container that is mapped to one or more channels: If one or more of those channels are active when the page is rendered, all of the contents of the Device Channel Panel are rendered. The Device Channel Panel helps you determine when to include specific content for specific channels.</span></span>
  
    
    

### <a name="display-templates"></a><span data-ttu-id="915f9-171">Шаблоны отображения</span><span class="sxs-lookup"><span data-stu-id="915f9-171">Display templates</span></span>
<span data-ttu-id="915f9-172"><a name="SP15_BuildSitesForSP2013_DisplayTemplates"> </a></span><span class="sxs-lookup"><span data-stu-id="915f9-172"><a name="SP15_BuildSitesForSP2013_DisplayTemplates"> </a></span></span>

<span data-ttu-id="915f9-p117">Для вашего веб-сайта может понадобиться управление форматом и представлением результатов поиска. Сделать это можно с помощью шаблонов для отображения, которые расширяют параметры настройки результатов поиска через пользовательский интерфейс за пределами сопоставления предопределенных полей.</span><span class="sxs-lookup"><span data-stu-id="915f9-p117">You may want to control the format and presentation of search results on your website. You can do that using display templates, which extend the options available for customizing search results through the user interface beyond mapping the predefined fields that you want to display.</span></span>
  
    
    
<span data-ttu-id="915f9-p118">Существует три случая, когда вы можете использовать шаблоны для отображения результатов поиска: для сопоставления способа представления всей структуры результатов поиска, для отображения группы результатов и для показа способ отображения каждого результата или элемента в наборе результатов. Они называются шаблон отображения элемента управления, шаблон отображения группы и шаблон отображения элемента, соответственно.</span><span class="sxs-lookup"><span data-stu-id="915f9-p118">There are three contexts when you may want to use display templates with search results—when you want to map how the overall structure of search results are presented, when you want to show groups of results, and when you want to show how each result, or item, in the result set is displayed. These are called Control, Group, and Item templates, respectively.</span></span>
  
    
    
<span data-ttu-id="915f9-177">Дополнительную информацию о шаблонах для отображения можно узнать в статье  [Шаблоны отображения Дизайнера SharePoint](sharepoint-design-manager-display-templates.md).</span><span class="sxs-lookup"><span data-stu-id="915f9-177">To learn more about display templates, see  [SharePoint Design Manager display templates](sharepoint-design-manager-display-templates.md).</span></span>
  
    
    

### <a name="image-renditions"></a><span data-ttu-id="915f9-178">Отрисовка изображений</span><span class="sxs-lookup"><span data-stu-id="915f9-178">Image renditions</span></span>
<span data-ttu-id="915f9-179"><a name="SP15_BuildSitesForSP2013_DisplayTemplates"> </a></span><span class="sxs-lookup"><span data-stu-id="915f9-179"><a name="SP15_BuildSitesForSP2013_DisplayTemplates"> </a></span></span>

<span data-ttu-id="915f9-p119">Вы можете использовать  [представления изображений](sharepoint-design-manager-image-renditions.md), чтобы отображать прикрепленные изображения предопределенного размера, ширины и кадрирования. Можно создать несколько отображений исходного файла изображения, что означает, что вы можете один раз установить набор характеристик отображения и применять их к любому количеству изображений. Например, отображение с именем **Article_image** показывает в статье полноразмерное изображение, в то время как отображение **Thumbnail_small**  уменьшенную версию этого изображения в указанных вами случаях.</span><span class="sxs-lookup"><span data-stu-id="915f9-p119">You can use  [image renditions](sharepoint-design-manager-image-renditions.md) to display uploaded images in predefined sizes, widths, and crops. You can create more than one rendition of a source image file, which means that you can set the display characteristics once and apply them to any number of images. For example, a rendition named **Article_image** displays a full-sized image in an article, while the rendition named **Thumbnail_small** displays a smaller version of the image in a context that you define.</span></span>
  
    
    
<span data-ttu-id="915f9-p120">Перед использованием отображений изображения убедитесь, что на сервере включен кэш больших двоичных объектов. Это можно сделать в средствах администрирования в службах IIS. Найдите там файл **web.config** и включите кэш больших двоичных объектов. Обновите страницу, и отображения изображения станут доступны.</span><span class="sxs-lookup"><span data-stu-id="915f9-p120">Before you can use image renditions, ensure that the BLOB cache is enabled on the server, which you can do in the Administration tools in Internet Information Services (IIS). Find your **web.config** file there and enable the BLOB cache. Refresh the page, and image renditions will be available.</span></span>
  
    
    

## <a name="managed-metadata-and-navigation-in-sharepoint"></a><span data-ttu-id="915f9-186">Управляемые метаданные и навигация в SharePoint</span><span class="sxs-lookup"><span data-stu-id="915f9-186">Managed metadata and navigation in SharePoint</span></span>
<span data-ttu-id="915f9-187"><a name="SP15_WhatsNewSiteDevelopment_MetadataAndNavigation"> </a></span><span class="sxs-lookup"><span data-stu-id="915f9-187"><a name="SP15_WhatsNewSiteDevelopment_MetadataAndNavigation"> </a></span></span>

<span data-ttu-id="915f9-188">Возможности корпоративных управляемых метаданных (EMM), представленные в , улучшены и расширены в SharePoint, чтобы повысить производительность, упростить доступ через пользовательский интерфейс и навигацию на основе таксономии, называемую управляемой навигацией.</span><span class="sxs-lookup"><span data-stu-id="915f9-188">Enterprise managed metadata (EMM) capabilities introduced in are improved and extended in SharePoint for better performance, easier access through the UI, and taxonomy-driven navigation—called managed navigation.</span></span>
  
    
    

### <a name="managed-navigation"></a><span data-ttu-id="915f9-189">Управляемая навигация</span><span class="sxs-lookup"><span data-stu-id="915f9-189">Managed navigation</span></span>

<span data-ttu-id="915f9-p121">Управляемая навигация  это основанная на таксономии альтернатива традиционной функции навигации SharePoint, называемой структурной навигацией и основанной на структуре SharePoint. Функция [управляемой навигации](managed-navigation-in-sharepoint.md) позволяет разрабатывать навигацию сайтов, которая работает за счет управляемых метаданных. Управляемая навигация создает URL-адреса, которые поддерживают SEO и извлекаются из структуры управляемой навигации. Так как управляемая навигация работает за счет таксономии, вы можете использовать их для разработки навигации сайта около важных бизнес-концепций без изменений структуры или компонентов сайта.</span><span class="sxs-lookup"><span data-stu-id="915f9-p121">Managed navigation is the taxonomy-based alternative to the traditional SharePoint navigation feature—called structured navigation—that is based on the structure of SharePoint. The  [managed navigation](managed-navigation-in-sharepoint.md) feature enables you to design a site navigation that is driven by managed metadata. Managed navigation creates SEO-friendly URLs that are derived from the managed navigation structure. Because managed navigation is driven by taxonomy, you can use it to design site navigation around important business concepts without changing the structure of your sites or site components.</span></span>
  
    
    

### <a name="content-search-web-part"></a><span data-ttu-id="915f9-194">веб-часть поиска контента;</span><span class="sxs-lookup"><span data-stu-id="915f9-194">Content Search Web Part</span></span>
<span data-ttu-id="915f9-195"><a name="SP15_BuildSitesForSP2013_ContentSearchWebPart"> </a></span><span class="sxs-lookup"><span data-stu-id="915f9-195"><a name="SP15_BuildSitesForSP2013_ContentSearchWebPart"> </a></span></span>

<span data-ttu-id="915f9-p122">Для отображения данных поиска на веб-страницах можно использовать  [веб-часть поиска контента (CSWP)](content-search-web-part-in-sharepoint.md). Она выполняет функцию, похожую на функцию веб-части запроса контента, но служит для других целей разработки сайта. Стили CSWP настраиваются проще, чем стили веб-части запроса контента. CSWP возвращает результаты на стороне клиента в формате JSON. На сервере вы можете настроить результаты с помощью шаблонов для отображения.</span><span class="sxs-lookup"><span data-stu-id="915f9-p122">You can use the  [Content Search Web Part (CSWP)](content-search-web-part-in-sharepoint.md) to display search data on your pages. It serves a function similar to that of the Content Query Web Part, but it serves different site design goals. CSWP styles are easier to customize than Content Query Web Part styles. CSWP returns client-side results in JSON format. On the server, you can customize results by using display templates.</span></span>
  
    
    

### <a name="other-managed-metadata-improvements-for-sites"></a><span data-ttu-id="915f9-201">Другие усовершенствования управляемых метаданных для сайта</span><span class="sxs-lookup"><span data-stu-id="915f9-201">Other managed metadata improvements for sites</span></span>
<span data-ttu-id="915f9-202"><a name="SP15_BuildSitesForSP2013_ContentSearchWebPart"> </a></span><span class="sxs-lookup"><span data-stu-id="915f9-202"><a name="SP15_BuildSitesForSP2013_ContentSearchWebPart"> </a></span></span>

<span data-ttu-id="915f9-p123">SharePoint представляет несколько усовершенствований для пользовательского интерфейса и функциональности управляемых метаданных. Подробнее можно узнать в статье  [Управляемые метаданные и навигация в SharePoint](managed-metadata-and-navigation-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="915f9-p123">SharePoint introduces several improvements to the managed metadata UI and functionality. To learn more, see  [Managed metadata and navigation in SharePoint](managed-metadata-and-navigation-in-sharepoint.md).</span></span>
  
    
    

## <a name="publishing-content-in-sharepoint"></a><span data-ttu-id="915f9-205">Публикация контента в SharePoint</span><span class="sxs-lookup"><span data-stu-id="915f9-205">Publishing content in SharePoint</span></span>
<span data-ttu-id="915f9-206"><a name="SP15_WhatsNewSiteDevelopment_Publishing"> </a></span><span class="sxs-lookup"><span data-stu-id="915f9-206"><a name="SP15_WhatsNewSiteDevelopment_Publishing"> </a></span></span>

<span data-ttu-id="915f9-207">SharePoint предлагает новые функции для публикации содержимого, которые позволяют вам разрабатывать сайты публикации, поддерживающие новые, более гибкие и более сложные топологии и сценарии.</span><span class="sxs-lookup"><span data-stu-id="915f9-207">SharePoint offers new content publishing features that enable you to develop publishing sites that support new, more flexible, and more complex topologies and scenarios.</span></span> 
  
    
    

### <a name="design-packages"></a><span data-ttu-id="915f9-208">Пакеты элементов дизайна</span><span class="sxs-lookup"><span data-stu-id="915f9-208">Design packages</span></span>

<span data-ttu-id="915f9-p124">Если вы  профессиональный веб-дизайнер, вам может потребоваться создать и проверить макет в собственной среде или семействе веб-сайтов перед тем, как передать его для установки на других семействах сайтов. Если для обмена содержимым по всем семействам веб-сайтов вы используете межсайтовую публикацию, вам может понадобиться упаковать и установить один и тот же макет на каждом сайте.</span><span class="sxs-lookup"><span data-stu-id="915f9-p124">If you're a professional web designer, you may want to create and test a design in your own environment or site collection before handing it off to install in other site collections. If you're using cross-site publishing to share content across site collections, you may want to package and install the same design on each site.</span></span>
  
    
    
<span data-ttu-id="915f9-p125">В предыдущих версиях SharePoint для повторного использования макета приходилось использовать Visual Studio, чтобы создать пакет решения SharePoint (WSP-файл). Затем необходимо было отправить этот пакет в каталог решений на сайт назначения и выполнить его. Теперь в SharePoint после завершения разработки своего сайта вы можете выбрать в Дизайнере команду **Экспорт пакета**, чтобы экспортировать один WSP-файл, называемый  [пакет конструктора](sharepoint-design-manager-design-packages.md). При экспорте пакета конструктора SharePoint автоматически упаковывает в него содержимое, добавленное или измененное в коллекции эталонных страниц, коллекции стилей, библиотеке тем, списке каналов устройств и типах контента страниц.</span><span class="sxs-lookup"><span data-stu-id="915f9-p125">In previous versions of SharePoint, if you wanted to reuse a design, you had to use Visual Studio to create a SharePoint Solution Package (.wsp file). Then, in the destination site, you would upload the package to the Solutions Gallery and execute it. Now, in SharePoint, after you finish designing your site, you can choose **Export Package** in Design Manager to export a single .wsp file called a [design package](sharepoint-design-manager-design-packages.md). When you export a design package, SharePoint automatically packages all of the contents that you have added or changed in the Master Page Gallery, Style Library, Theme Gallery, the Device Channels list, and Page content types into a design package.</span></span> 
  
> [!NOTE] 
> <span data-ttu-id="915f9-215">Пакет конструктора не включает страницы, параметры навигации и банк терминов.</span><span class="sxs-lookup"><span data-stu-id="915f9-215">A design package does not include pages, navigation settings, or the term store.</span></span> 
  
    
    

<span data-ttu-id="915f9-p126">Пакеты конструктора не перезаписывают существующие файлы для общедоступных веб-сайтов Office 365. При установке пакетов конструктора создаются новые папки в коллекции эталонных страниц, коллекции стилей и коллекции тем, где проектные ресурсы изолированы.</span><span class="sxs-lookup"><span data-stu-id="915f9-p126">For Office 365 public websites, design packages do not overwrite existing files. Installing a design package creates a new folder in the Master Page Gallery, Style Gallery, and Theme Gallery where design assets are isolated.</span></span> 
  
    
    
<span data-ttu-id="915f9-p127">При импорте пакета конструктора проектные ресурсы в пакете перезаписывают любые существующие файлы и применяются в качестве текущего оформления сайта. Эталонная страница по умолчанию для сайта и эталонная страница системы, тема и альтернативная таблица CSS устанавливаются из файлов пакета конструктора. Благодаря пакетам конструктора оформление, созданное в одной среде, можно с легкостью применить к другой изолированной среде.</span><span class="sxs-lookup"><span data-stu-id="915f9-p127">When you import a design package, the design assets in the package overwrite any existing files and are applied as the current design of the site. The site's default and system master page, theme, and alternate CSS are all set from the files in the design package. With design packages, a design built in one environment can easily be applied to another, separate environment.</span></span>
  
    
    

### <a name="catalogs"></a><span data-ttu-id="915f9-221">Каталоги</span><span class="sxs-lookup"><span data-stu-id="915f9-221">Catalogs</span></span>

<span data-ttu-id="915f9-p128">Сайт публикации SharePoint вводит каталоги, которые позволяют включать списки в сайты публикации. Каталоги позволяют публиковать содержимое по всем семействам веб-сайтов, функции межсайтовой публикации зависят от каталогов. Вы можете использовать каталоги для реального повторного использования содержимого по всем сайтам и по всей границе между веб-сайтами интрасети, Интернета и экстрасети. Для предопределенных запросов каталоги отмечаются в поиске. Вы можете показать содержимое, хранимое в каталогах на всех семействах сайтов, с помощью  [веб-части поиска контента (CSWP)](content-search-web-part-in-sharepoint.md). Вы можете создать пользовательский код, чтобы наполнять каталоги, подключать каталоги продуктов к сайту и отбирать отдельные страницы с настраиваемыми макетами страниц, веб-частями и HTML-содержимым, которое отображается только в определенных случаях.</span><span class="sxs-lookup"><span data-stu-id="915f9-p128">SharePoint site publishing introduces catalogs, which enable you to incorporate lists into your publishing sites. Catalogs enable content to be published across site collections—the cross-site publishing features depend on catalogs. You can use catalogs to truly reuse content across your sites and across the boundary between your intranet sites, Internet sites, and extranet sites. For predefined search queries, catalogs are flagged in search. You can surface content stored in catalogs across site collections by using the  [Content Search Web Part (CSWP)](content-search-web-part-in-sharepoint.md). You can write custom code to populate catalogs, connect a product catalog to a site, and curate individual pages with custom page layouts, Web Parts, and HTML content that appears only in the defined context.</span></span>
  
    
    

### <a name="client-side-rendering-controls"></a><span data-ttu-id="915f9-228">Клиентские элементы управления отображением</span><span class="sxs-lookup"><span data-stu-id="915f9-228">Client-side rendering controls</span></span>

<span data-ttu-id="915f9-p129">Все новые элементы управления в SharePoint отрисовываются на стороне клиента. Вы как конструктор или разработчик управляете отрисовкой содержимого на странице и можете использовать различные технологии разработки, включая веб-часть поиска контента и шаблоны отображения, чтобы публикуемая страница выглядела и вела себя должным образом. Данные записываются в элементы управления в массиве JSON на стороне клиента, и вы можете отобразить содержимое с помощью JavaScript, CSS и шаблонов.</span><span class="sxs-lookup"><span data-stu-id="915f9-p129">All new controls in SharePoint are rendered client-side. As a designer or a developer, you have control over how content is rendered on the page, and you can use various design techniques to get the look and behaviors you want on your published pages by using features including the Content Search Web Part and display templates. Data is written to the controls in a client-side JSON array, and you can display content using JavaScript, CSS, and templates.</span></span> 
  
    
    

### <a name="cross-site-publishing"></a><span data-ttu-id="915f9-232">Публикация на нескольких сайтах</span><span class="sxs-lookup"><span data-stu-id="915f9-232">Cross-site publishing</span></span>

<span data-ttu-id="915f9-p130">Microsoft SharePoint представляет функцию межсайтовой публикации, которая позволяет повторно использовать содержимое на нескольких семействах веб-сайтов. Он использует встроенные возможности, чтобы включить сценарии и архитектуры публикаций. В первый раз вы можете разработать сайты, пересекающие фермы SharePoint. Это позволит вашим сайтам охватить границы между интрасетями и Интернетом.</span><span class="sxs-lookup"><span data-stu-id="915f9-p130">Microsoft SharePoint introduces a cross-site publishing feature that enables you to reuse content across multiple site collections. It uses built-in search capabilities to enable publishing scenarios and architectures. For the first time, you can design sites that cross SharePoint farms—enabling your sites to span the boundary between intranets and the Internet.</span></span> 
  
    
    
<span data-ttu-id="915f9-p131">Используйте функцию тематических страниц, чтобы настроить взаимодействие целевых страниц для содержимого, опубликованного по всем сайтам. Используйте URL-адреса, поддерживающие SEO, чтобы управлять и с легкостью сохранять и поддерживать структуру сайта по широкому диапазону сценариев, включая сложные топологии многоязыковых сайтов.</span><span class="sxs-lookup"><span data-stu-id="915f9-p131">Use the topic pages feature to customize the landing page experience for content that is published across sites. Use SEO-friendly URLs to manage and more easily persist and maintain site structure across a broad range of scenarios—including complex multilingual site topologies.</span></span>
  
    
    
<span data-ttu-id="915f9-238">Дополнительные сведения о публикации на нескольких сайтах см. в статье [Сценарий: создание сайтов SharePoint с помощью публикации на нескольких сайтах в SharePoint](http://technet.microsoft.com/ru-RU/sharepoint/jj872721).</span><span class="sxs-lookup"><span data-stu-id="915f9-238">To learn more about cross-site publishing, see  [Scenario: Create SharePoint sites by using cross-site publishing in SharePoint](http://technet.microsoft.com/ru-RU/sharepoint/jj872721).</span></span> <span data-ttu-id="915f9-239">Дополнительные сведения о вариантах разработки для публикации на нескольких сайтах см. в статье [Публикация на нескольких сайтах в SharePoint](cross-site-publishing-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="915f9-239">To learn more about development options for cross-site publishing, see  [Cross-site publishing in SharePoint](cross-site-publishing-in-sharepoint.md).</span></span>
  
    
    

### <a name="seo-enhancements"></a><span data-ttu-id="915f9-240">Улучшения SEO</span><span class="sxs-lookup"><span data-stu-id="915f9-240">SEO enhancements</span></span>

<span data-ttu-id="915f9-p133">Многие пользователи бизнес-сайтов переходят на них в сети Интернет из крупных поисковых систем таких, как Bing и его мировых конкурентов. SharePoint включает в себя функции, например понятные URL-адреса, перенаправления домашних страниц, XML карты сайта, настраиваемые свойства SEO, которые позволяют гибко задавать заголовок браузера, описание тега **<Meta>** и ключевые слова и настраивать понятные URL-адреса для вариантов многоязыкового сайта.</span><span class="sxs-lookup"><span data-stu-id="915f9-p133">Many business site users are referred to Internet business sites from large search engines like Bing and its global competitors. SharePoint includes features like friendly URLs, home page redirects, XML sitemaps, custom SEO properties that enable you to flexibly define the browser title and **<Meta>** tag descriptions and keywords, and easier-to-understand URLs for multilingual site variations.</span></span>
  
    
    
<span data-ttu-id="915f9-p134">В Office 365 инфраструктура сайта создает для вас обновленную XML карту сайта в течение 24 часов со времени изменения сайта. Благодаря локальной установке вы можете настроить актуальность вашей карты сайта и указать, с какими системами поиска необходимо проверять связь в случаях обновления карты сайта.</span><span class="sxs-lookup"><span data-stu-id="915f9-p134">In Office 365, the site infrastructure generates an updated XML sitemap for you within 24 hours of a site change. With an on-premises installation, you can tune the freshness of your sitemaps and specify which search engines you want Microsoft to ping when we update the sitemap.</span></span>
  
    
    
<span data-ttu-id="915f9-p135">То что нравится вашим друзьям на Facebook влияет на результаты поиска, возвращаемые Bing и другими крупными поисковыми системами. Вы можете использовать интерфейсы API в моделях программирования SharePoint, чтобы настроить способ оптимизации поиска для своего сайта.</span><span class="sxs-lookup"><span data-stu-id="915f9-p135">What your friends like on Facebook affects what you see in the search results returned by Bing and other large search engines. You can use APIs in SharePoint programming models to customize how search is optimized for your site.</span></span>
  
    
    

### <a name="analytics-and-recommendations"></a><span data-ttu-id="915f9-247">Аналитика и рекомендации</span><span class="sxs-lookup"><span data-stu-id="915f9-247">Analytics and recommendations</span></span>

<span data-ttu-id="915f9-p136">Вы можете отслеживать использование сайтов публикации и их компонентов с помощью функции анализа SharePoint, которая тесно интегрирована с поисковой системой. Аналитика управляет возможностями рекомендации содержимого и вводит расчеты в индекс поиска в виде управляемых свойств. Рекомендации, предоставляемые службой аналитики поиска, которая включает просмотры страниц и уникальных элементов в день, может влиять на релевантность результатов поиска.</span><span class="sxs-lookup"><span data-stu-id="915f9-p136">You can track how people use publishing sites and their components using the SharePoint analytics feature, which is deeply integrated with the search engine. Analytics drives recommendations capabilities on content, and injects calculations into the search index as managed properties. The recommendations provided by search analytics, which include page views and unique items per day, can influence the relevance of search results.</span></span>
  
    
    
<span data-ttu-id="915f9-p137">Служба аналитики создает анонимные данные и сворачивает их каждые 15 дней. Она очищает события каждые 15 дней, а по истечении 3 лет  каждый месяц. Представления времени жизни сохраняются всегда. Содержимое кратковременных посещений обрезается перед отправкой сводных данных в базу данных отчетов. Вы можете использовать пользовательский код, чтобы экспортировать данные из базы данных отчетов в Excel, настроить вес события **View** и создать настраиваемые события, включая события, отправленные с помощью JavaScript.</span><span class="sxs-lookup"><span data-stu-id="915f9-p137">Analytics makes data anonymous and rolls it up every 15 days. Analytics purges events every 15 days and then monthly after 3 years. Lifetime views are always retained. The least-visited content is trimmed before analytics pushes aggregate data to a reporting database. You can use custom code to export data to Excel from the reporting database, customize the weight of the **View** event, and create custom events—including those submitted by JavaScript.</span></span>
  
    
    

### <a name="variations-and-multilingual-sites"></a><span data-ttu-id="915f9-256">Варианты и многоязычные сайты</span><span class="sxs-lookup"><span data-stu-id="915f9-256">Variations and multilingual sites</span></span>

<span data-ttu-id="915f9-257">С помощью функции вариантов в SharePoint вы можете создавать многоязычные сайты или другие сайты, на которых требуется менять способ представления содержимого.</span><span class="sxs-lookup"><span data-stu-id="915f9-257">You can use the variations feature in SharePoint to create multilingual sites or other sites where you want to vary the presentation of your content.</span></span> <span data-ttu-id="915f9-258">Функция вариантов распространяется только на одно семейство веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="915f9-258">The variations feature is constrained to one site collection.</span></span> <span data-ttu-id="915f9-259">То есть вы можете создавать варианты с целевым языком или языковым стандартом на основе исходного языка или языкового стандарта в качестве текущих веб-сайтов в той же коллекции веб-сайтов SharePoint.</span><span class="sxs-lookup"><span data-stu-id="915f9-259">That is, you can create target language/locale "variants" of a source language/locale as current websites within the same SharePoint site collection.</span></span> <span data-ttu-id="915f9-260">Варианты поддерживают понятные URL-адреса и возможность экспорта или импорта содержимого в [файл формата XLIFF](the-xliff-interchange-file-format-in-sharepoint.md) для перевода третьей стороной.</span><span class="sxs-lookup"><span data-stu-id="915f9-260">Variations supports friendly URLs and the ability to export or import content for translation by a third party in  [XLIFF file format](the-xliff-interchange-file-format-in-sharepoint.md).</span></span> <span data-ttu-id="915f9-261">В пакеты экспорта можно включать метки, страницу для перевода и репликации, различные элементы списков (например, библиотеки документов) и элементы навигации.</span><span class="sxs-lookup"><span data-stu-id="915f9-261">You can include labels, a page for translation and replication, a variety of list items (for example, document libraries.md), and navigation in your export packages.</span></span> 
  
    
    

## <a name="see-also"></a><span data-ttu-id="915f9-262">См. также</span><span class="sxs-lookup"><span data-stu-id="915f9-262">See also</span></span>
<span data-ttu-id="915f9-263"><a name="SP15_WhatsNewSiteDevelopment_AdditionalResources"> </a></span><span class="sxs-lookup"><span data-stu-id="915f9-263"><a name="SP15_WhatsNewSiteDevelopment_AdditionalResources"> </a></span></span>


-  [<span data-ttu-id="915f9-264">Выполнение базовых операций с использованием кода библиотеки клиента в SharePoint</span><span class="sxs-lookup"><span data-stu-id="915f9-264">Complete basic operations using SharePoint client library code</span></span>](http://msdn.microsoft.com/library/5a69c9e3-73bf-4ed5-bc19-182056bdb394%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="915f9-265">Выполнение базовых операций с использованием кода библиотеки JavaScript в SharePoint</span><span class="sxs-lookup"><span data-stu-id="915f9-265">Complete basic operations using JavaScript library code in SharePoint</span></span>](http://msdn.microsoft.com/library/29089af8-dbc0-49b7-a1a0-9e311f49c826%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="915f9-266">Инструкции. Настройка макетов страниц для сайта на основе каталога в SharePoint</span><span class="sxs-lookup"><span data-stu-id="915f9-266">How to: Customize page layouts for a catalog-based site in SharePoint</span></span>](how-to-customize-page-layouts-for-a-catalog-based-site-in-sharepoint.md)
    
  
-  [<span data-ttu-id="915f9-267">Способ: изменение страницы предварительного просмотра в диспетчере оформления SharePoint</span><span class="sxs-lookup"><span data-stu-id="915f9-267">How to: Change the preview page in SharePoint Design Manager</span></span>](how-to-change-the-preview-page-in-sharepoint-design-manager.md)
    
  
-  [<span data-ttu-id="915f9-268">Как: Устранение ошибок и предупреждения при предварительном просмотре страницы в SharePoint</span><span class="sxs-lookup"><span data-stu-id="915f9-268">How to: Resolve errors and warnings when previewing a page in SharePoint</span></span>](how-to-resolve-errors-and-warnings-when-previewing-a-page-in-sharepoint.md)
    
  
-  [<span data-ttu-id="915f9-269">Общие сведения о темах для SharePoint</span><span class="sxs-lookup"><span data-stu-id="915f9-269">Themes overview for SharePoint</span></span>](themes-overview-for-sharepoint.md)
    
  
-  [<span data-ttu-id="915f9-270">Управляемые метаданные и навигация в SharePoint</span><span class="sxs-lookup"><span data-stu-id="915f9-270">Managed metadata and navigation in SharePoint</span></span>](managed-metadata-and-navigation-in-sharepoint.md)
    
  
-  [<span data-ttu-id="915f9-271">Новые возможности поиска в SharePoint для разработчиков (en)</span><span class="sxs-lookup"><span data-stu-id="915f9-271">What's new in SharePoint search for developers</span></span>](what-s-new-in-sharepoint-search-for-developers.md)
    
  

