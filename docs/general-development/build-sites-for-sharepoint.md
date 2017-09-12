---
title: "Создание сайтов для SharePoint"
ms.prod: SHAREPOINT
ms.assetid: 3b372a63-7cdf-462a-abb4-750e611e967d
ms.openlocfilehash: d03f7748c42fd12cf07d1d18c6d125dcd8138119
ms.sourcegitcommit: d9e955bf9d5afd9ad8ae8304a3ddb85ac27b3406
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/06/2017
---
# <a name="build-sites-for-sharepoint"></a><span data-ttu-id="b1e03-102">Создание сайтов для SharePoint</span><span class="sxs-lookup"><span data-stu-id="b1e03-102">Build sites for SharePoint</span></span>
<span data-ttu-id="b1e03-103">В этой статье описываются новая модель создания и публикации веб-сайтов в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="b1e03-103">Learn about the new site authoring and publishing model for websites in SharePoint.</span></span>
## <a name="introduction-to-site-publishing-for-designers-and-developers-in-sharepoint"></a><span data-ttu-id="b1e03-104">Общие сведения о публикации сайтов в SharePoint для конструкторов и разработчиков</span><span class="sxs-lookup"><span data-stu-id="b1e03-104">Introduction to site publishing for designers and developers in SharePoint</span></span>
<span data-ttu-id="b1e03-105"><a name="SP15_BuildSitesForSP2013_IntroToSitePublishing"> </a></span><span class="sxs-lookup"><span data-stu-id="b1e03-105"></span></span>

<span data-ttu-id="b1e03-p101">В SharePoint представлена модель создания и публикации сайтов публикации. Эти сайты можно использовать для публикации контента на сайтах интрасети и Интернета. Сайты публикации отличаются от других типов сайтов SharePoint, например сайтов группы, в основном, из-за их предназначения - многие пользователи читают контент сайта публикации, но только некоторые из них добавляют, обновляют и удаляют контент из одного или нескольких семейств веб-сайтов. На сайтах группы же многие пользователи могут обрабатывать контент.</span><span class="sxs-lookup"><span data-stu-id="b1e03-p101">SharePoint introduces a site authoring and publishing model to create publishing sites. You can use publishing sites to publish content on intranet or Internet sites. Publishing sites differ from other types of SharePoint sites, such as team sites, mainly due to their purpose—many users read publishing site content, but only a few contribute by adding, updating, and deleting content from one or more site collections. Contrast these sites with team sites, where many people may collaborate and contribute to the content.</span></span> 
  
    
    
<span data-ttu-id="b1e03-p102">Возможности сайтов публикации SharePoint можно использовать для создания, настройки и поддержки сайтов публикации в соответствии с бизнес-потребностями. И профессиональные дизайнеры, знакомые с HTML, CSS и JavaScript, и разработчики, которые создают приложения для SharePoint и применяют пользовательский код .NET для создания сайтов и решений ферм, могут использовать возможности сайта в SharePoint для управления всеми этапами жизненного цикла контента, в том числе следующие:</span><span class="sxs-lookup"><span data-stu-id="b1e03-p102">You can use the SharePoint site publishing capabilities to build, customize, and maintain publishing sites that meet specific business needs. Whether you are a professional designer with HTML, CSS, and JavaScript skills or a developer who writes SharePoint apps and uses custom .NET code to build sites and farm solutions, you can use site features in SharePoint to manage all phases of the content life cycle, including:</span></span>
  
    
    

- <span data-ttu-id="b1e03-112">**Authoring** и повторное использование контента;</span><span class="sxs-lookup"><span data-stu-id="b1e03-112">**Authoring** and reusing site content.</span></span>
    
  
- <span data-ttu-id="b1e03-113">**Branding** и разработка внешнего вида сайта;</span><span class="sxs-lookup"><span data-stu-id="b1e03-113">**Branding** and designing your site's look, feel, and behavior.</span></span>
    
  
- <span data-ttu-id="b1e03-114">**Managing metadata** - вы можете создать систему навигации сайта на основе таксономии;</span><span class="sxs-lookup"><span data-stu-id="b1e03-114">**Managing metadata**—you can build a taxonomy-driven site navigation system.</span></span>
    
  
- <span data-ttu-id="b1e03-115">**Publishing** контента в текущем семействе веб-сайтов или публикация контента в разных семействах веб-сайтов, в том числе на сайтах интрасети и Интернета.</span><span class="sxs-lookup"><span data-stu-id="b1e03-115">**Publishing** content smoothly to the current site collection, or publishing content across site collections—even spanning the intranet and Internet site boundary.</span></span>
    
  
- <span data-ttu-id="b1e03-116">**Accessibility** - вы можете повышать доступность опубликованных сайтов.</span><span class="sxs-lookup"><span data-stu-id="b1e03-116">**Accessibility**—you can use to improve the accessibility of your published sites.</span></span>
    
  
<span data-ttu-id="b1e03-117">Сводку новых возможностей для разработчиков веб-сайтов публикации SharePoint см. в статье  [Новые возможности разработки сайтов в SharePoint](what-s-new-with-sharepoint-site-development).</span><span class="sxs-lookup"><span data-stu-id="b1e03-117">If you want to see a summary of what's new for designers and developers of publishing websites in SharePoint, see  [What's new with SharePoint site development](what-s-new-with-sharepoint-site-development).</span></span> 
  
    
    

## <a name="authoring-design-and-branding-in-sharepoint"></a><span data-ttu-id="b1e03-118">Разработка, оформление и фирменная символика в SharePoint</span><span class="sxs-lookup"><span data-stu-id="b1e03-118">Authoring, design, and branding in SharePoint</span></span>
<span data-ttu-id="b1e03-119"><a name="SP15_BuildSitesForSP2013_AuthoringDesignBranding"> </a></span><span class="sxs-lookup"><span data-stu-id="b1e03-119"></span></span>

<span data-ttu-id="b1e03-p103">SharePoint предоставляет новый подход к проектированию веб-сайтов. Рабочий процесс создания контент был изменен, и теперь вы можете использовать любой инструмент и создавать привлекательный контент. Для оформления сайта без написания кода .NET используйте  [Дизайнер](overview-of-design-manager-in-sharepoint) для импорта элементов дизайна. С помощью Дизайнера также можно создать главную страницу на основе HTML, чтобы определить элементы управления, общие для всех страниц сайта (хром), и создать макеты страниц для проектирования шаблонов страниц. Если вы решили написать пользовательский код, можно использовать серверную и клиентскую (CSOM) объектную модель .NET, Silverlight и библиотеки JavaScript.</span><span class="sxs-lookup"><span data-stu-id="b1e03-p103">SharePoint provides a new approach for designing websites. The content-creation workflow is revised so that you can create content using any —and author great content. To brand your site without having to write custom .NET code, use the  [Design Manager](overview-of-design-manager-in-sharepoint) to import design elements. With Design Manager, you can also create an HTML-based master page to define the chrome shared by all of your site's pages and create page layouts to design templates for pages. If you choose to write custom code, you can use .NET server, .NET client (CSOM), Silverlight, and JavaScript libraries.</span></span>
  
    
    
<span data-ttu-id="b1e03-p104">SharePoint предоставляет новый подход к созданию и обработке контента. Рабочий процесс создания контент был изменен, и теперь вы можете применять любой инструмент и создавать привлекательный контент. Для оформления сайта без написания кода .NET используйте Дизайнер. Вы можете импортировать элементы дизайна и создать главную страницу на основе HTML, чтобы определить элементы управления, общие для всех страниц сайта и макетов страниц (хром). Если вы решили написать пользовательский код, вы можете использовать библиотеки публикации и таксономии.</span><span class="sxs-lookup"><span data-stu-id="b1e03-p104">SharePoint also provides a new approach to content and authoring. The content-creation workflow is revised so that you can create content using any authoring and branding tool and author great content. To brand your site without having to write custom ASP.NET code, use the Design Manager. You can import design elements and create an HTML-based master page to define the shared framing elements—the chrome—that all of your site's pages and page layouts share. If you choose to write custom code when branding your site, you can use the publishing and taxonomy libraries.</span></span>
  
    
    

## <a name="publishing-sites-client-object-model-programming-and-the-new-sharepoint-app-model"></a><span data-ttu-id="b1e03-130">Публикация сайтов, программирование с использованием клиентской объектной модели и новая модель приложений SharePoint</span><span class="sxs-lookup"><span data-stu-id="b1e03-130">Publishing sites, client object model programming, and the new SharePoint app model</span></span>
<span data-ttu-id="b1e03-131"><a name="SP15_BuildSitesForSP2013_PublishingSites"> </a></span><span class="sxs-lookup"><span data-stu-id="b1e03-131"></span></span>

<span data-ttu-id="b1e03-p105">С помощью новой клиентской объектной модели (CSOM) .NET можно разрабатывать приложения для SharePoint, применяя Модель для надстроек SharePoint. Вы можете использовать множество API-интерфейсов, также доступных для программирования сервера .NET. Они поддерживают клиентскую объектную модель .NET, Silverlight, JavaScript и, в некоторых случаях, Windows Phone. Вот некоторые идеи для приложений веб-сайтов: опросы, управление учетными записями приложений, поддержка электронной коммерции, интеграция социальных компонентов и внешних данных в сайты публикации, добавление внешнего контента и мобильные приложения-компаньоны.</span><span class="sxs-lookup"><span data-stu-id="b1e03-p105">You can use the new .NET client object model (CSOM) to develop SharePoint apps with the model for SharePoint Add-ins. You can use many of the APIs that are also available for .NET server programming in the .NET client object models, which support .NET client, Silverlight, JavaScript—and in some cases Windows Phone—development. Some ideas for developing apps for websites include surveys, account management apps, eCommerce support, integrating social features and external data into publishing websites, outsourced content additions, and mobile companion apps.</span></span> 
  
    
    

## <a name="page-model-for-publishing-websites"></a><span data-ttu-id="b1e03-135">Модель страниц для веб-сайтов публикации</span><span class="sxs-lookup"><span data-stu-id="b1e03-135">Page model for publishing websites</span></span>
<span data-ttu-id="b1e03-136"><a name="SP15_BuildSitesForSP2013_PageModel"> </a></span><span class="sxs-lookup"><span data-stu-id="b1e03-136"></span></span>

<span data-ttu-id="b1e03-p106">SharePoint использует модель страницы для веб-сайтов публикации. В нее входят главные страницы, макеты страниц и другие компоненты, которые отображают структуру сайта и контент, определяют его внешний вид и поведение. Дополнительные сведения см. в статье  [Обзор модели страниц в SharePoint](overview-of-the-sharepoint-page-model).</span><span class="sxs-lookup"><span data-stu-id="b1e03-p106">SharePoint includes a page model for publishing websites. The page model includes master pages, page layouts, and other components that render your site structure, content, look and feel, and behavior. To learn more, see  [Overview of the SharePoint page model](overview-of-the-sharepoint-page-model).</span></span>
  
    
    

## <a name="master-pages-and-page-layouts"></a><span data-ttu-id="b1e03-140">Главные страницы и макеты страниц</span><span class="sxs-lookup"><span data-stu-id="b1e03-140">Master pages and page layouts</span></span>
<span data-ttu-id="b1e03-141"><a name="SP15_BuildSitesForSP2013_MasterAndLayout"> </a></span><span class="sxs-lookup"><span data-stu-id="b1e03-141"></span></span>

<span data-ttu-id="b1e03-p107">Главная страница — это основной шаблон, который определяет общие структурные элемента сайта — хром. Все страницы на сайте используют эти элементы, которые определяют области страницы, в которых отображается контент макета страницы.</span><span class="sxs-lookup"><span data-stu-id="b1e03-p107">A master page is the main template that defines the shared structural elements of your site—the chrome. All of the pages on the site share these elements, which define the regions of the page that display page layout content.</span></span>
  
    
    
<span data-ttu-id="b1e03-p108">Макеты страниц используются отдельными страницами определенного типа. Они заполнены полями страницы. Эти страницы определяют отдельные элементы на странице. Отдельные страницы основаны на макетах страниц и создаются в браузере с помощью пользовательского кода или другого способа, позволяющего пользователям заполнять поля страниц. Дополнительные сведения о модели страниц SharePoint см. в статье  [Обзор модели страниц в SharePoint](overview-of-the-sharepoint-page-model).</span><span class="sxs-lookup"><span data-stu-id="b1e03-p108">Page layouts are used by individual pages of a certain type. They are populated with arrangements of page fields. These pages define individual elements on the page. Individual pages are based on page layouts and are created in your web browser either by custom code or by how the site's users fill out the page's fields. To learn more about the page model in SharePoint, see  [Overview of the SharePoint page model](overview-of-the-sharepoint-page-model).</span></span> 
  
    
    

## <a name="client-side-rendering-controls"></a><span data-ttu-id="b1e03-149">Клиентские элементы управления отображением</span><span class="sxs-lookup"><span data-stu-id="b1e03-149">Client-side rendering controls</span></span>
<span data-ttu-id="b1e03-150"><a name="SP15_BuildSitesForSP2013_ClientSideRendering"> </a></span><span class="sxs-lookup"><span data-stu-id="b1e03-150"></span></span>

<span data-ttu-id="b1e03-p109">Все новые элементы управления в SharePoint отображаются. Данные записываются в элементы управления массиве JSON на стороне клиента, а контент можно отобразить с помощью JavaScript, CSS и шаблонов. Дизайнер или разработчик может управлять визуализацией контента на странице, можно используя различные методы разработки, чтобы добиться нужного внешнего вида публикуемых страниц с помощью таких компонентов, как  [Веб-часть поиска контента в SharePoint](content-search-web-part-in-sharepoint) и шаблоны отображения.</span><span class="sxs-lookup"><span data-stu-id="b1e03-p109">All new controls in SharePoint are rendered. Data is written to the controls in a client-side JSON array, and you can display content using JavaScript, CSS, and templates. As a designer or developer, you have control over how content is rendered on the page, and you can use various design techniques to get the look and behaviors you want on your published pages by using features like the  [Content Search Web Part in SharePoint](content-search-web-part-in-sharepoint) and display templates.</span></span>
  
    
    

## <a name="sites-and-mobile-devices"></a><span data-ttu-id="b1e03-154">Сайты и мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="b1e03-154">Sites and mobile devices</span></span>
<span data-ttu-id="b1e03-155"><a name="SP15_BuildSitesForSP2013_SitesAndMobile"> </a></span><span class="sxs-lookup"><span data-stu-id="b1e03-155"></span></span>

<span data-ttu-id="b1e03-p110">Веб-сайты публикации в SharePoint оптимизированы для мобильных приложений. Вы можете определить каналы для одного или нескольких устройств (каналы устройств) и назначить альтернативную главную страницу каждому каналу, задав для него уникальные структурные элементы или хром. Вы можете включить или исключить любую часть макета страницы из канала и просмотреть, как будет выглядеть страница канала во время разработки.</span><span class="sxs-lookup"><span data-stu-id="b1e03-p110">Publishing websites in SharePoint are optimized for mobile development. You can define channels for one or more devices (device channels) and assign an alternate master page for each channel, giving it unique structural elements, or chrome. You can choose to include or exclude portions of any page layout in a channel, and preview how mobile channel design is progressing while it's being developed.</span></span> 
  
    
    

## <a name="metadata-and-navigation-in-sharepoint"></a><span data-ttu-id="b1e03-159">Метаданные и навигация в SharePoint</span><span class="sxs-lookup"><span data-stu-id="b1e03-159">Metadata and navigation in SharePoint</span></span>
<span data-ttu-id="b1e03-160"><a name="SP15_BuildSitesForSP2013_MetadataNav"> </a></span><span class="sxs-lookup"><span data-stu-id="b1e03-160"></span></span>

<span data-ttu-id="b1e03-p111">Возможности управляемых метаданных, представленные в Microsoft SharePoint Server 2010, в SharePoint были улучшены и расширены, чтобы повысить производительность, упростить доступ с помощью пользовательского интерфейса и навигации на основе таксономии (управляемой навигации). Вы можете использовать управляемую навигацию или навигацию на основе структуры веб-сайта SharePoint (структурной навигации) для создания навигации сайта. Дополнительные сведения об управляемой навигации см. в статьях  [Управляемые метаданные и навигация в SharePoint](managed-metadata-and-navigation-in-sharepoint) и [Управляемая навигация в SharePoint](managed-navigation-in-sharepoint).</span><span class="sxs-lookup"><span data-stu-id="b1e03-p111">Managed metadata capabilities introduced in Microsoft SharePoint Server 2010 are improved and extended in SharePoint for better performance, easier access through the user interface, and taxonomy-driven navigation—called managed navigation. You can use managed navigation or navigation based on the SharePoint website structure—called structured navigation—to build your site navigation. To learn more about managed navigation, see  [Managed metadata and navigation in SharePoint](managed-metadata-and-navigation-in-sharepoint) and [Managed navigation in SharePoint](managed-navigation-in-sharepoint).</span></span>
  
    
    

## <a name="publishing-content-in-sharepoint"></a><span data-ttu-id="b1e03-164">Публикация контента в SharePoint</span><span class="sxs-lookup"><span data-stu-id="b1e03-164">Publishing content in SharePoint</span></span>
<span data-ttu-id="b1e03-165"><a name="SP15_BuildSitesForSP2013_PublishingContent"> </a></span><span class="sxs-lookup"><span data-stu-id="b1e03-165"></span></span>

<span data-ttu-id="b1e03-166">SharePoint предоставляет следующие новые возможности публикации контента, позволяющие создавать сайты публикации, которые поддерживают более гибкие, доступные и сложные топологии и сценарии.</span><span class="sxs-lookup"><span data-stu-id="b1e03-166">SharePoint offers the following new content publishing features that enable you to develop publishing sites that support more flexible, more accessible, and more complex topologies and scenarios.</span></span> 
  
    
    

### <a name="catalogs"></a><span data-ttu-id="b1e03-167">Каталоги</span><span class="sxs-lookup"><span data-stu-id="b1e03-167">Catalogs</span></span>

<span data-ttu-id="b1e03-p112">В SharePoint представлены каталоги, который можно использовать для публикации контента в семействах веб-сайтов. Возможности публикации на нескольких сайтах основаны на каталогах. С их помощью можно повторно использовать контент на сайтах интрасети и Интернета. Для предварительно определенных запросов поиска каталоги отмечаются в результатах поиска. Вы можете предоставить доступ к контенту в каталогах различным семействам веб-сайтов с помощью  [Веб-часть поиска контента в SharePoint](content-search-web-part-in-sharepoint).</span><span class="sxs-lookup"><span data-stu-id="b1e03-p112">SharePoint introduces catalogs, which you can use to publish content across site collections. Cross-site publishing features depend on catalogs. You can use them to reuse content across your sites and across the boundary between your intranet sites and Internet sites. For predefined search queries, catalogs are flagged in search. You can surface content stored in catalogs across site collections by using the  [Content Search Web Part in SharePoint](content-search-web-part-in-sharepoint).</span></span>
  
    
    

### <a name="cross-site-publishing"></a><span data-ttu-id="b1e03-173">Публикация на нескольких сайтах</span><span class="sxs-lookup"><span data-stu-id="b1e03-173">Cross-site publishing</span></span>

<span data-ttu-id="b1e03-p113">В SharePoint представлена возможность публикации на нескольких сайтах, позволяющая повторно использовать один контент в разных семействах веб-сайтов. Для этого применяются встроенные функции поиски, реализующие полезные сценарии и архитектуры публикации. Впервые вы сможете создавать сайты, охватывающие несколько ферм SharePoint и даже выходящие за пределы сайтов интрасети и Интернет-сайтов. Вы можете использовать CSWP для отображения данных поиска, опубликованных на разных сайтах и семействах веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="b1e03-p113">SharePoint introduces a cross-site publishing feature to reuse content across multiple site collections. It uses built-in search capabilities to enable publishing scenarios and architectures. For the first time, you can design sites that cross SharePoint farms—enabling your sites to span the boundary between intranets and the Internet. You can use the CSWP to display search data published from across sites and site collections.</span></span>
  
    
    

### <a name="variations-and-multilingual-sites"></a><span data-ttu-id="b1e03-178">Варианты и многоязычные сайты</span><span class="sxs-lookup"><span data-stu-id="b1e03-178">Variations and multilingual sites</span></span>

<span data-ttu-id="b1e03-p114">В SharePoint вы можете использовать функцию вариантов, чтобы создавать многоязычные сайты или другие сайты, где необходимо изменить представление содержимого. Функция вариантов ограничивается одним семейством веб-сайтов. То есть вы можете создать целевые языковые или региональные "варианты" исходного языка или региона текущего сайта в рамках того же семейства веб-сайтов SharePoint. Варианты поддерживают понятные URL-адреса и возможность экспорта или импорта содержимого в  [формате XLIFF-файла](the-xliff-interchange-file-format-in-sharepoint), чтобы третья сторона могла выполнить перевод. Вы можете включать в свои пакеты экспорта метки, страницы для трансляции и репликации, вариант списка элементов (например, библиотеки документов) и навигацию.</span><span class="sxs-lookup"><span data-stu-id="b1e03-p114">You can use the variations feature in SharePoint to create multilingual sites or other sites where you want to vary the presentation of your content. The variations feature is constrained to one site collection. That is, you can create target language/locale "variants" of a source language/locale as current websites within the same SharePoint site collection. Variations supports friendly URLs and the ability to export or import content for translation by a third party in  [XLIFF file format](the-xliff-interchange-file-format-in-sharepoint). You can include labels, a page for translation and replication, a variety of list items (for example, document libraries), and navigation in your export packages.</span></span> 
  
    
    

### <a name="accessible-sites"></a><span data-ttu-id="b1e03-184">Доступные сайты</span><span class="sxs-lookup"><span data-stu-id="b1e03-184">Accessible sites</span></span>

<span data-ttu-id="b1e03-p115">С помощью функции вариантов в SharePoint вы можете создавать доступные сайты или другие сайты, где вы хотите приспособить внешний вид контента к различным потребностям пользователей. В SharePoint предусмотрены специальные возможности, которые можно активировать, открыв веб-страницу SharePoint и нажимая клавишу TAB, пока не появится ссылка "Включить специальные возможности". Эта функция повторно создает веб-страницу в стандартном формате HTML, повышая удобство чтения с экрана. Гарантируя, что пользователи смогут перевести фокус на эту ссылку с помощью клавиши TAB, вы сможете создать более доступную версию своей страницы SharePoint. В частности, раскрывающиеся меню на основе JavaScript преобразуются в списки гиперссылок, а объекты - в более простой код HTML, поддерживающий чтение с экрана.</span><span class="sxs-lookup"><span data-stu-id="b1e03-p115">You can use the variations feature in SharePoint to create accessible sites or other sites where you want to adapt the presentation of your content for users who have a variety of accessability needs. SharePointprovides a "More Accessible Mode", which can be activated by opening a SharePoint webpage, and pressing the TAB key until you find the "Turn on More Accessible Mode" link. This feature recreates the webpage in standard HTML, making it friendlier for screen-readers. By ensuring that users are able to press the TAB key to focus on this link, you are able to create a more accessible version of your SharePoint webpage. This includes JavaScript-based drop-down menus being converted to hyperlink lists and objects are converted to simpler HTML to allow screen-readers to understand the content.</span></span> 
  
    
    

## <a name="additional-resources"></a><span data-ttu-id="b1e03-190">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="b1e03-190">Additional resources</span></span>
<span data-ttu-id="b1e03-191"><a name="SP15_BuildSitesForSP2013_AdditionalResources"> </a></span><span class="sxs-lookup"><span data-stu-id="b1e03-191"></span></span>


-  [<span data-ttu-id="b1e03-192">Оптимизация специальные возможности сайта SharePoint</span><span class="sxs-lookup"><span data-stu-id="b1e03-192">Optimize SharePoint site accessibility</span></span>](optimize-sharepoint-site-accessibility)
    
  
-  [<span data-ttu-id="b1e03-193">Настройка общей среды разработки для SharePoint</span><span class="sxs-lookup"><span data-stu-id="b1e03-193">Set up a general development environment for SharePoint</span></span>](set-up-a-general-development-environment-for-sharepoint)
    
  
-  [<span data-ttu-id="b1e03-194">Новые возможности разработки сайтов в SharePoint</span><span class="sxs-lookup"><span data-stu-id="b1e03-194">What's new with SharePoint site development</span></span>](what-s-new-with-sharepoint-site-development)
    
  
-  [<span data-ttu-id="b1e03-195">Общие сведения о минимальной загрузки стратегия</span><span class="sxs-lookup"><span data-stu-id="b1e03-195">Minimal Download Strategy overview</span></span>](minimal-download-strategy-overview)
    
  
-  [<span data-ttu-id="b1e03-196">Изменение компонентов SharePoint для MDS</span><span class="sxs-lookup"><span data-stu-id="b1e03-196">Modify SharePoint components for MDS</span></span>](modify-sharepoint-components-for-mds)
    
  
-  [<span data-ttu-id="b1e03-197">Библиотека классов сервера сайтов и контента SharePoint</span><span class="sxs-lookup"><span data-stu-id="b1e03-197">SharePoint Sites and Content server class library</span></span>](http://msdn.microsoft.com/library/8a93e838-234c-41d8-b990-7ac1a415dd5e%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="b1e03-198">Библиотека клиентских классов для сайта и контента</span><span class="sxs-lookup"><span data-stu-id="b1e03-198">Sites and Content client class library</span></span>](http://msdn.microsoft.com/library/e6542022-a459-4c3b-aee0-e350c6397139%28Office.15%29.aspx)
    
  

