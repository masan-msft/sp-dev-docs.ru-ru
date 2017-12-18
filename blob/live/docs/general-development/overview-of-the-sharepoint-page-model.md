---
title: "Обзор модели страниц в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 808b1af3-89ab-4f02-89cc-ea86cb1f9a6e
ms.openlocfilehash: c4b92c40cf047d33b7617fc5cba214ce1832cbb6
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="overview-of-the-sharepoint-page-model"></a><span data-ttu-id="a09d6-102">Обзор модели страниц в SharePoint</span><span class="sxs-lookup"><span data-stu-id="a09d6-102">Overview of the SharePoint page model</span></span>
<span data-ttu-id="a09d6-103">Информация о пересмотренной модели страницы (включая эталонные страницы и макеты страниц), модернизированной для SharePoint.</span><span class="sxs-lookup"><span data-stu-id="a09d6-103">Learn about the revised page model—including master pages and page layouts—redesigned for SharePoint.</span></span>
## <a name="introduction-to-the-page-model"></a><span data-ttu-id="a09d6-104">Общие сведения о модели страницы</span><span class="sxs-lookup"><span data-stu-id="a09d6-104">Introduction to the page model</span></span>
<span data-ttu-id="a09d6-105"><a name="bk_Introduction"> </a></span><span class="sxs-lookup"><span data-stu-id="a09d6-105"><a name="bk_Introduction"> </a></span></span>

<span data-ttu-id="a09d6-p101">Прежде чем приступить к разработке или созданию фирменной символики сайта SharePoint, необходимо иметь базовое представление о частях сайта SharePoint и компоновке страниц SharePoint. В этой статье представлены наглядные схемы этих фрагментов, чтобы учитывать их при планировании оформления веб-сайта. Данная статья применима главным образом к веб-сайтам публикации в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="a09d6-p101">Before you design or brand a SharePoint site, you need a basic understanding of the parts of a SharePoint site and how a SharePoint page is put together. This article gives you a visual overview of the pieces to think about as you plan how to brand your site. This article applies specifically to publishing sites in SharePoint.</span></span>
  
    
    

## <a name="master-pages-page-layouts-and-pages"></a><span data-ttu-id="a09d6-109">Эталонные страницы, макеты страниц и страницы</span><span class="sxs-lookup"><span data-stu-id="a09d6-109">Master pages, page layouts, and pages</span></span>
<span data-ttu-id="a09d6-110"><a name="bk_MasterPages"> </a></span><span class="sxs-lookup"><span data-stu-id="a09d6-110"><a name="bk_MasterPages"> </a></span></span>

<span data-ttu-id="a09d6-p102">SharePoint использует макеты, чтобы определить и отрисовать страницы, которые отображаются на веб-сайте. Структура страницы SharePoint включает три основных элемента:</span><span class="sxs-lookup"><span data-stu-id="a09d6-p102">SharePoint uses templates to define and render the pages that a site displays. The structure of a SharePoint page includes three main elements:</span></span>
  
    
    

- <span data-ttu-id="a09d6-113">Эталонная страница определяет общие элементы фрейма (хром) для всех страниц на вашем сайте.</span><span class="sxs-lookup"><span data-stu-id="a09d6-113">Master pages define the shared framing elements—the chrome—for all pages in your site.</span></span>
    
  
- <span data-ttu-id="a09d6-114">Макеты страниц определяют макет для определенного класса страниц.</span><span class="sxs-lookup"><span data-stu-id="a09d6-114">Page layouts define the layout for a specific class of pages.</span></span>
    
  
- <span data-ttu-id="a09d6-115">Страницы создаются на основе макета страницы авторами, добавляющими содержимое в поля страницы.</span><span class="sxs-lookup"><span data-stu-id="a09d6-115">Pages are created from a page layout by authors who add content to page fields.</span></span>
    
  

<span data-ttu-id="a09d6-116">**Рис. 1. Эталонная страница, макет страницы и страница**</span><span class="sxs-lookup"><span data-stu-id="a09d6-116">**Figure 1. Master page, page layout, and page**</span></span>

  
    
    

  
    
    
![Главная страница, макет страницы и страница](../images/101_page_model_overview.gif)
  
    
    

### <a name="master-pages"></a><span data-ttu-id="a09d6-118">Главные страницы</span><span class="sxs-lookup"><span data-stu-id="a09d6-118">Master pages</span></span>

<span data-ttu-id="a09d6-p103">Эталонная страница определяет хром (общие элементы фрейма) вашего сайта. Эти элементы могут включать верхний и нижний колонтитулы, верхнюю панель навигации, "хлебные крошки", поле поиска, эмблему сайта и другие элементы фирменной символики. При перемещении посетителей по сайту эталонная страница остается неизменной.</span><span class="sxs-lookup"><span data-stu-id="a09d6-p103">A master page defines the chrome (the shared framing elements) of your site. These elements may include the header and footer, top navigation, breadcrumbs, search box, site logo, and other branding elements. The master page remains consistent as visitors navigate through your site.</span></span>
  
    
    

<span data-ttu-id="a09d6-122">**Рисунок 2. Эталонная страница**</span><span class="sxs-lookup"><span data-stu-id="a09d6-122">**Figure 2. Master page**</span></span>

  
    
    

  
    
    
![Главная страница](../images/102_master_page.gif)
  
    
    
<span data-ttu-id="a09d6-p104">Кроме того, эталонная страница определяет области, называемые заполнителями контента, которые наполняются контентом из соответствующих областей на макетах страниц. Чаще всего основная часть эталонной страницы содержит единственный заполнитель (который называется **PlaceHolderMain** и создается автоматически), и весь контент из макета страницы появляется внутри него (заполнитель контента **PlaceHolderMain** выделен красным цветом на рис. 3).</span><span class="sxs-lookup"><span data-stu-id="a09d6-p104">A master page also defines regions called content placeholders that are filled in by content from matching regions on page layouts. Most commonly, the body of a master page contains just a single content placeholder (named **PlaceHolderMain**, which is created automatically), and all of the content from a page layout appears inside this one content placeholder (the **PlaceHolderMain** content placeholder is outlined in red in Figure 3).</span></span>
  
    
    

<span data-ttu-id="a09d6-126">**Рисунок 3. Эталонная страница с выделенным макетом страницы**</span><span class="sxs-lookup"><span data-stu-id="a09d6-126">**Figure 3. Master page with page layout outlined**</span></span>

  
    
    

  
    
    
![Главная страница с выделенным макетом страницы](../images/103_master_page_with_page_layout_outlined.gif)
  
    
    
<span data-ttu-id="a09d6-p105">При просмотре эталонной страницы в Дизайнере вы увидите представленное ниже сообщение. Этот тег **<div>** находится внутри заполнителя основного содержимого. Проще говоря, эталонная страница определяет хром страницы, а макет страницы определяет текст, содержащийся в заполнителе основного содержимого.</span><span class="sxs-lookup"><span data-stu-id="a09d6-p105">When you preview a master page in Design Manager, you see the following message. This **<div>** resides inside the main content placeholder. Put simply, the master page defines the chrome of a page, and the page layout defines the body contained in the main content placeholder.</span></span>
  
    
    

<span data-ttu-id="a09d6-131">**Рисунок 4. Сообщение при предварительном просмотре эталонной страницы**</span><span class="sxs-lookup"><span data-stu-id="a09d6-131">**Figure 4. Master page preview message**</span></span>

  
    
    

  
    
    
![Сообщение предварительного просмотра главной страницы](../images/104_master_page_preview_message.gif)
  
    
    

  
    
    

  
    
    

### <a name="page-layouts"></a><span data-ttu-id="a09d6-133">Макеты страниц</span><span class="sxs-lookup"><span data-stu-id="a09d6-133">Page layouts</span></span>

<span data-ttu-id="a09d6-p106">Макет страницы  это шаблон для определенного типа страницы на вашем сайте, например страницы статьи или страницы сведений о продукте. Как следует из названия, можно представить макет страницы как определение макета или структуры для основной части страницы.</span><span class="sxs-lookup"><span data-stu-id="a09d6-p106">A page layout is a template for a specific type of page in your site, such as an article page or a product details page. Just like its name implies, you can think of a page layout as defining the layout or structure for the body of a page.</span></span>
  
    
    

<span data-ttu-id="a09d6-136">**Рисунок 5. Макет страницы**</span><span class="sxs-lookup"><span data-stu-id="a09d6-136">**Figure 5. Page layout**</span></span>

  
    
    

  
    
    
![Макет страницы](../images/105_page_layout.gif)
  
    
    
<span data-ttu-id="a09d6-p107">Макеты страниц определяют области или области содержимого, которые сопоставляются заполнителям контента на эталонной странице (выделены красным цветом на рис. 6). И снова наиболее распространенный сценарий  это когда макет страницы определяет единственную область содержимого, которая сопоставлена единственному заполнителю контента, автоматически созданному на эталонной странице.</span><span class="sxs-lookup"><span data-stu-id="a09d6-p107">Page layouts define regions or content areas that map to content placeholders on the master page (outlined in red in Figure 6). Again, the most common scenario is that a page layout defines a single content region that maps to the single content placeholder that is created automatically on a master page.</span></span>
  
    
    

<span data-ttu-id="a09d6-140">**Рисунок 6. Область содержимого и заполнитель контента**</span><span class="sxs-lookup"><span data-stu-id="a09d6-140">**Figure 6. Content region and content placeholder**</span></span>

  
    
    

  
    
    
![Область содержимого и заполнитель содержимого](../images/106_content_region_and_content_placeholder.gif)
  
    
    

  
    
    

  
    
    

### <a name="page-field-controls"></a><span data-ttu-id="a09d6-142">Элементы управления полями страницы</span><span class="sxs-lookup"><span data-stu-id="a09d6-142">Page field controls</span></span>

<span data-ttu-id="a09d6-p108">Основное назначение макета страницы  упорядочить поля страницы. При создании макета страницы вы вставляете, определяете положение и стиль элементов, называемых элементы управления полями страницы. В конечном итоге, когда автор создаст страницы на основе данного макета страницы, в этих элементах управления будет содержаться контент. В дополнение к полям страницы макеты страниц могут содержать зоны веб-частей, в которые авторы контента могут добавлять веб-части. (Эталонные страницы не могут содержать зоны веб-частей.)</span><span class="sxs-lookup"><span data-stu-id="a09d6-p108">The primary purpose of a page layout is to arrange page fields. When you design a page layout, you insert, position, and style elements called page field controls. These controls will eventually contain content when an author creates a page based on that page layout. In addition to page fields, page layouts can also contain Web Part zones, to which content authors can add Web Parts. (Master pages can't contain Web Part zones.)</span></span>
  
    
    
<span data-ttu-id="a09d6-p109">С помощью элемента управления полями страницы вы можете определить стили контента. Авторы могут добавлять контент на страницу, однако отображение контента целиком определяет проектировщик с помощью таблицы CSS, которая применяется к этим элементам управления.</span><span class="sxs-lookup"><span data-stu-id="a09d6-p109">With a page field control, you can define the styles used by the content. Authors can add content to a page, but the designer has ultimate control over how that content is rendered through CSS applied to those controls.</span></span>
  
    
    

<span data-ttu-id="a09d6-150">**Рисунок 7. Макет страницы с элементами управления полями страницы**</span><span class="sxs-lookup"><span data-stu-id="a09d6-150">**Figure 7. Page layout with page field controls**</span></span>

  
    
    

  
    
    
![Макет страницы с элементами управления полей страницы](../images/107_page_layout_with_page_fields.gif)
  
    
    
<span data-ttu-id="a09d6-p110">Каждый макет страницы связан с типом контента в библиотеке страниц сайта. Тип контента  это схема столбцов и типов данных. Для любого макета страницы поля страницы, доступные для данного макета, напрямую соответствуют столбцам, определенным для типа контента этого макета страницы.</span><span class="sxs-lookup"><span data-stu-id="a09d6-p110">Every page layout is associated with a content type in the Pages library of a site. A content type is a schema of columns and data types. For any page layout, the page fields that are available for that layout correspond directly to the columns defined for that page layout's content type.</span></span>
  
    
    

### <a name="relationship-of-master-pages-and-page-layouts"></a><span data-ttu-id="a09d6-155">Отношение эталонных страниц и макетов страниц</span><span class="sxs-lookup"><span data-stu-id="a09d6-155">Relationship of master pages and page layouts</span></span>

<span data-ttu-id="a09d6-156">Эталонная страница и макет страницы вместе создают страницу содержимого.</span><span class="sxs-lookup"><span data-stu-id="a09d6-156">Together, a master page and a page layout create a content page.</span></span>
  
    
    

<span data-ttu-id="a09d6-157">**Рисунок 8. Эталонная страница с макетом страницы**</span><span class="sxs-lookup"><span data-stu-id="a09d6-157">**Figure 8. Master page with page layout**</span></span>

  
    
    

  
    
    
![Главная страница с макетом страницы](../images/108_master_page_with_page_layout.gif)
  
    
    
<span data-ttu-id="a09d6-159">Эталонная страница определяет хром для всех страниц на сайте, поскольку в большинстве случаев многие макеты страниц (и поэтому многие страницы создаются из этих макетов страницы) связаны с одной эталонной страницей.</span><span class="sxs-lookup"><span data-stu-id="a09d6-159">The master page defines the chrome for all pages in the site so, often many page layouts (and therefore many pages created from those page layouts) are associated with one master page.</span></span>
  
    
    

<span data-ttu-id="a09d6-160">**Рисунок 9. Одна эталонная страницы связана с тремя макетами страниц**</span><span class="sxs-lookup"><span data-stu-id="a09d6-160">**Figure 9. One master page tied to three page layouts**</span></span>

  
    
    

  
    
    
![Одна главная страница, привязанная к трем макетам страниц](../images/109_one_master_many_layouts.gif)
  
    
    
<span data-ttu-id="a09d6-p111">Однако ваш сайт, скорее всего, использует несколько эталонных страниц. Например, кроме эталонной страницы по умолчанию, у вас могут быть одна или несколько эталонных страниц, которые предназначены для определенных устройств, например смартфонов или планшетов. В этом случае один макет страницы используется несколькими эталонными страницами (более подробную информацию можно узнать в разделе о каналах устройств).</span><span class="sxs-lookup"><span data-stu-id="a09d6-p111">But, your site will likely use multiple master pages. For example, in addition to the default master page, you may have one or more master pages that target specific devices such as smart phones or tablets. In this case, one page layout is used by many master pages (see the section about device channels).</span></span>
  
    
    
<span data-ttu-id="a09d6-165">Вы можете использовать одну эталонную страницу на каждый канал по каждому сайту SharePoint.</span><span class="sxs-lookup"><span data-stu-id="a09d6-165">You can use one master page per channel per SharePoint site.</span></span>
  
    
    

### <a name="pages"></a><span data-ttu-id="a09d6-166">Страницы</span><span class="sxs-lookup"><span data-stu-id="a09d6-166">Pages</span></span>

<span data-ttu-id="a09d6-p112">Авторы могут создавать страницы, добавлять содержимое на поля страниц и добавлять веб-части в любую зону веб-частей или редакторы форматированного текста. Структура страниц выполнена таким образом, что авторы страниц не смогут внести изменения за пределы полей страницы.</span><span class="sxs-lookup"><span data-stu-id="a09d6-p112">Authors can create pages and add content to the page fields, and they can add Web Parts to any Web Part zones or Rich Text Editors. Pages are structured so that content authors cannot make changes outside of page fields.</span></span>
  
    
    

<span data-ttu-id="a09d6-169">**Рисунок 10. Страница с авторским содержимым**</span><span class="sxs-lookup"><span data-stu-id="a09d6-169">**Figure 10. Page with authored content**</span></span>

  
    
    

  
    
    
![Страница с созданным содержимым](../images/110_page_with_authored_content.gif)
  
    
    
<span data-ttu-id="a09d6-p113">Отображаемая страница  это то, что посетители видят на сайте. Когда браузер запрашивает страницу, эталонная страница объединяется с макетом, чтобы создать страницу содержимого, и содержимое для данной страницы объединяется с полями из данной страницы в библиотеке страниц.</span><span class="sxs-lookup"><span data-stu-id="a09d6-p113">The rendered page is what site visitors see. When a page is requested by the browser, the master page is merged with a page layout to create a content page, and the content for that page is merged into the page fields from that page in the Pages library.</span></span>
  
    
    

<span data-ttu-id="a09d6-173">**Рисунок 11. Отображаемая страница в браузере**</span><span class="sxs-lookup"><span data-stu-id="a09d6-173">**Figure 11. Rendered page in browser**</span></span>

  
    
    

  
    
    
![Страница, отображенная в браузере](../images/111_rendered_page.gif)
  
    
    

<span data-ttu-id="a09d6-175">**Рисунок 12. Эталонная страница, макет страницы и страница**</span><span class="sxs-lookup"><span data-stu-id="a09d6-175">**Figure 12. Master page, page layout, and page**</span></span>

  
    
    

  
    
    
![Главная страница, макет страницы и страница](../images/112_master_plus_layout_plus_page.gif)
  
    
    

  
    
    

  
    
    

## <a name="search-driven-web-parts-and-display-templates"></a><span data-ttu-id="a09d6-177">Веб-части на основе поиска и шаблоны для отображения</span><span class="sxs-lookup"><span data-stu-id="a09d6-177">Search-driven Web Parts and display templates</span></span>
<span data-ttu-id="a09d6-178"><a name="bk_SearchDriven"> </a></span><span class="sxs-lookup"><span data-stu-id="a09d6-178"><a name="bk_SearchDriven"> </a></span></span>

<span data-ttu-id="a09d6-p114">В предыдущем разделе была рассмотрена модель страниц SharePoint с точки зрения эталонных страниц, макетов страниц (с полями страниц) и страниц. Эти элементы наиболее распространены на сайте публикации, на котором авторы регулярно создают и публикуют новый контент. Когда дело доходит до отображения этого контента на вашем сайте, в игру вступают еще пара элементов. Хотите вы подключиться к внешнему каталогу или просто отобразить определенный набор результатов поиска, для выполнения этих действий вам понадобятся веб-части на основе поиска.</span><span class="sxs-lookup"><span data-stu-id="a09d6-p114">The previous section explains the SharePoint page model in terms of master pages, page layouts (with page fields), and pages. These elements are the most common in a publishing site in which authors regularly create and publish new content. When it comes to surfacing that content on your site, though, a couple more elements come into play. Whether you have connected to an external catalog or simply want to show a particular set of search results, search-driven Web Parts can help you achieve your goal.</span></span>
  
    
    
<span data-ttu-id="a09d6-183">В сценарии со страницами на основе поиска страница SharePoint содержит три основных элемента:</span><span class="sxs-lookup"><span data-stu-id="a09d6-183">In the search-driven pages scenario, a SharePoint page contains these main elements:</span></span>
  
    
    

- <span data-ttu-id="a09d6-184">Главные страницы</span><span class="sxs-lookup"><span data-stu-id="a09d6-184">Master pages</span></span>
    
  
- <span data-ttu-id="a09d6-185">Макеты страниц:</span><span class="sxs-lookup"><span data-stu-id="a09d6-185">Page layouts:</span></span>
    
  - <span data-ttu-id="a09d6-186">обычные макеты страниц, которые создаются вами для определенных типов контента, как это описано в данной статье выше;</span><span class="sxs-lookup"><span data-stu-id="a09d6-186">Regular page layouts that you created for specific content types, as described previously in this article</span></span>
    
  
  - <span data-ttu-id="a09d6-187">макеты страниц со сведениями о категории или элементе, которые создаются с помощью публикации каталога на нескольких сайтах.</span><span class="sxs-lookup"><span data-stu-id="a09d6-187">Category and item details page layouts that are created through cross-site publishing of a catalog</span></span>
    
  
- <span data-ttu-id="a09d6-188">Страницы</span><span class="sxs-lookup"><span data-stu-id="a09d6-188">Pages</span></span>
    
  
- <span data-ttu-id="a09d6-189">Веб-части на основе поиска, например веб-часть поиска контента.</span><span class="sxs-lookup"><span data-stu-id="a09d6-189">Search-driven Web Parts, such as the Content Search Web Part</span></span>
    
  
- <span data-ttu-id="a09d6-190">Шаблоны для отображения, чтобы контролировать появление управляемых свойств в результатах поиска веб-части поиска контента и управлять стилем и поведением данных результатов поиска:</span><span class="sxs-lookup"><span data-stu-id="a09d6-190">Display templates to control which managed properties appear in the search results of a search-driven Web Part, and control the styling and behavior of those search results:</span></span>
    
  - <span data-ttu-id="a09d6-191">шаблоны отображения элементов управления, которые управляют макетом результатов поиска и любыми элементами, общими для всех результатов, например разбиение по страницам, сортировка и другие ссылки;</span><span class="sxs-lookup"><span data-stu-id="a09d6-191">Control display templates, which control the layout of search results and any elements common to all results such as paging, sorting, and other links</span></span>
    
  
  - <span data-ttu-id="a09d6-192">шаблоны отображения элемента, которые управляют отображением и повторением каждого результата поиска.</span><span class="sxs-lookup"><span data-stu-id="a09d6-192">Item display templates, which control how each search result is displayed and repeated for each result</span></span>
    
  

<span data-ttu-id="a09d6-193">**Рисунок 13. Эталонная страница, макет страницы и страница с веб-частью**</span><span class="sxs-lookup"><span data-stu-id="a09d6-193">**Figure 13. Master page, page layout, and page with Web Part**</span></span>

  
    
    

  
    
    
![Главная страница, макет страницы и страница с веб-частью](../images/113_114_master_and_layout_and_page_and_web_part_closeup.gif)
  
    
    

### <a name="search-driven-web-parts"></a><span data-ttu-id="a09d6-195">Веб-части на основе поиска</span><span class="sxs-lookup"><span data-stu-id="a09d6-195">Search-driven Web Parts</span></span>

<span data-ttu-id="a09d6-p115">С помощью веб-частей на основе поиска вы можете динамически представлять хранимую в индексе поиска информацию. Представление данных в веб-части поиска контента управляется с помощью шаблонов для отображения, которые находятся в коллекции эталонных страниц вместе с эталонными страницами и макетами страниц.</span><span class="sxs-lookup"><span data-stu-id="a09d6-p115">With search-driven Web Parts, you can dynamically present information stored in the search index. The presentation of data in the Content Search Web Part is controlled by display templates, which reside in the Master Page Gallery alongside master pages and page layouts.</span></span>
  
    
    
<span data-ttu-id="a09d6-198">В SharePoint есть несколько готовых шаблонов отображения, например списки и слайд-шоу для веб-частей поиска контента.</span><span class="sxs-lookup"><span data-stu-id="a09d6-198">SharePoint includes several ready-to-use display templates such as lists and slideshows for your Content Search Web Parts.</span></span> <span data-ttu-id="a09d6-199">Шаблоны отображения можно выбрать во время настройки веб-части поиска контента в браузере.</span><span class="sxs-lookup"><span data-stu-id="a09d6-199">When you configure a Content Search Web Part in the browser, you choose which display templates to use.</span></span>
  
    
    

<span data-ttu-id="a09d6-200">**Рис. 14. Область инструментов веб-части поиска контента**</span><span class="sxs-lookup"><span data-stu-id="a09d6-200">**Figure 14. Tool pane of Content Search Web Part**</span></span>

  
    
    

  
    
    
![Область инструментов веб-части поиска в содержимом](../images/115_content_search_web_part_tool_pane.gif)
  
    
    
<span data-ttu-id="a09d6-p117">Веб-части поиска контента используют два типа шаблонов для отображения  шаблон отображения элемента управления и шаблон отображения элемента. В рамках разработки или создания фирменной символики своего сайта вы можете создать пользовательский шаблон для отображения, который использует определенные вами макеты, стили и поведение.</span><span class="sxs-lookup"><span data-stu-id="a09d6-p117">Content Search Web Parts use two types of display templates, control and item. As part of the design or branding of your site, you can create custom display templates that use layouts, styles, and behaviors that you define.</span></span>
  
    
    

<span data-ttu-id="a09d6-204">**Рисунок 15. Две схемы веб-частей поиска контента**</span><span class="sxs-lookup"><span data-stu-id="a09d6-204">**Figure 15. Two diagrams of Content Search Web Parts**</span></span>

  
    
    

  
    
    
![Две схемы веб-частей поиска в содержимом](../images/116_117_control_templates_1_and_2.gif)
  
    
    

  
    
    

  
    
    

### <a name="control-display-template"></a><span data-ttu-id="a09d6-206">Шаблон отображения элемента управления</span><span class="sxs-lookup"><span data-stu-id="a09d6-206">Control display template</span></span>

<span data-ttu-id="a09d6-p118">Шаблон элемента управления определяет всю структуру и макет представления результатов поиска, например список с разбиением по страницам или слайд-шоу. Каждая веб-часть поиска контента использует один шаблон элемента управления.</span><span class="sxs-lookup"><span data-stu-id="a09d6-p118">The control template determines the overall structure and layout of how you want to present the search results, such as a list with paging or a slideshow. Each Content Search Web Part uses one control template.</span></span>
  
    
    
<span data-ttu-id="a09d6-209">Кроме того, этот шаблон включает функциональные возможности, общие для всех результатов поиска, включая разбиение по страницам, сортировку, параметры просмотра и разделители.</span><span class="sxs-lookup"><span data-stu-id="a09d6-209">The control template also includes functionality common to all the search results, including paging, sorting, view options, and separators.</span></span>
  
    
    

<span data-ttu-id="a09d6-210">**Рисунок 16. Шаблон элемента управления, выделенный в веб-части и на веб-странице**</span><span class="sxs-lookup"><span data-stu-id="a09d6-210">**Figure 16. Control template outlined on Web Part and webpage**</span></span>

  
    
    

  
    
    
![Шаблон элемента управления, выделенный в веб-части и на веб-странице](../images/118_119_control_template_outlined_on_web_part_and_page.gif)
  
    
    

  
    
    

  
    
    

### <a name="item-display-template"></a><span data-ttu-id="a09d6-212">Шаблон отображения элемента</span><span class="sxs-lookup"><span data-stu-id="a09d6-212">Item display template</span></span>

<span data-ttu-id="a09d6-p119">Шаблон элемента определяет способ отображения каждого результата в наборе; этот шаблон повторяется для каждого результата. Шаблон элемента может отображать изображение, изображение с текстом, видео и другой контент.</span><span class="sxs-lookup"><span data-stu-id="a09d6-p119">The item template determines how each result in the set is displayed, and the template is repeated for each result. An item template can display an image, an image with text, a video, and other content.</span></span>
  
    
    
<span data-ttu-id="a09d6-p120">Кроме того, он определяет, какие управляемые свойства и значения отображаются за счет веб-части поиска контента. В данном примере шаблон элемента отображает три управляемых свойства: небольшое изображение, название продукта в виде гиперссылки и краткое текстовое описание.</span><span class="sxs-lookup"><span data-stu-id="a09d6-p120">The item display template also determines which managed properties and values are displayed by the Content Search Web Part. In this example, the item template displays three managed properties: a small-sized image, a product name as a hyperlink, and a brief text description.</span></span>
  
    
    

<span data-ttu-id="a09d6-217">**Рисунок 17. Шаблоны элементов, выделенные в веб-части и на веб-странице**</span><span class="sxs-lookup"><span data-stu-id="a09d6-217">**Figure 17. Item templates outlined on Web Part and webpage**</span></span>

  
    
    

  
    
    
![Шаблоны элементов, выделенные в веб-части и на веб-странице](../images/120_121_item_templates_outlined_on_web_part_and_page.gif)
  
    
    

  
    
    

  
    
    

## <a name="device-channels-and-device-channel-panels"></a><span data-ttu-id="a09d6-219">Каналы устройств и панели канала устройств</span><span class="sxs-lookup"><span data-stu-id="a09d6-219">Device channels and device channel panels</span></span>
<span data-ttu-id="a09d6-220"><a name="bk_DeviceChannels"> </a></span><span class="sxs-lookup"><span data-stu-id="a09d6-220"><a name="bk_DeviceChannels"> </a></span></span>

<span data-ttu-id="a09d6-p121">В SharePoint вы можете использовать каналы устройств, чтобы отображать один веб-сайт несколькими способами с использованием различных макетов, предназначенных для различных устройств. Вы создаете один сайт и авторский контент только один раз. Затем этот сайт и контент можно сопоставить, чтобы использовать различные эталонные страницы и таблицы стилей, предназначенные определенным устройствам или группам устройств.</span><span class="sxs-lookup"><span data-stu-id="a09d6-p121">In SharePoint, you can use device channels to render a single publishing site in multiple ways by using different designs that target different devices. You create a single site and author the content in it a single time. Then, that site and content can be mapped to use different master pages and style sheets to target a specific device or group of devices.</span></span>
  
    
    
<span data-ttu-id="a09d6-224">При разработке сайта для более одного устройства учтите следующие элементы:</span><span class="sxs-lookup"><span data-stu-id="a09d6-224">When you design for more than one device, consider these elements:</span></span>
  
    
    

- <span data-ttu-id="a09d6-225">Каналы устройств:</span><span class="sxs-lookup"><span data-stu-id="a09d6-225">Device channels:</span></span>
    
  - <span data-ttu-id="a09d6-226">Используя различные эталонные страницы и таблицы CSS для каждого канала, одинаковое содержимое страницы для определенных устройств (например, Windows Phone) или групп устройств (все смартфоны) можно представить различными способами.</span><span class="sxs-lookup"><span data-stu-id="a09d6-226">By using different master pages and CSS per channel, identical page content can be presented in different ways for specific devices (for example, Windows Phone) or groups of devices (all smart phones).</span></span>
    
  
- <span data-ttu-id="a09d6-227">Макеты страниц:</span><span class="sxs-lookup"><span data-stu-id="a09d6-227">Page layouts:</span></span>
    
  - <span data-ttu-id="a09d6-228">Если контент не меняется, вы можете использовать для всех каналов устройств одинаковые макеты страниц несмотря на то, что они могут иметь разные стили, основанные на CSS другой эталонной страницы, для каждого канала.</span><span class="sxs-lookup"><span data-stu-id="a09d6-228">If the content does not change, you use the same page layouts for all device channels, though they can be styled differently based on the CSS of the different master page for each channel.</span></span>
    
  
  - <span data-ttu-id="a09d6-229">Если вы хотите включить контент только для определенных устройств, используйте панели канала устройств.</span><span class="sxs-lookup"><span data-stu-id="a09d6-229">If you want to include content only for specific devices, use device channel panels.</span></span>
    
  
- <span data-ttu-id="a09d6-230">Страницы</span><span class="sxs-lookup"><span data-stu-id="a09d6-230">Pages</span></span>
    
  

### <a name="device-channels"></a><span data-ttu-id="a09d6-231">Каналы устройств</span><span class="sxs-lookup"><span data-stu-id="a09d6-231">Device channels</span></span>

<span data-ttu-id="a09d6-p122">Когда вы создаете канал устройства, вы указываете подстроки агента пользователя для целевых устройств канала. Это позволяет хорошо управлять устройством (или браузером), которое было захвачено через канал. Затем вы назначаете этому каналу эталонную страницу; каждая эталонная страница в свою очередь ссылается на собственную таблицу стилей, в которой макет и стили оптимизированы для данного типа устройства.</span><span class="sxs-lookup"><span data-stu-id="a09d6-p122">When you create a device channel, you specify the user agent substrings for the devices that you want the channel to target. This gives you fine-tuned control over what devices (or browsers) are captured by each channel. Then you assign a master page to that channel; in turn, each master page links to its own style sheet where the layout and styles are optimized for that type of device.</span></span>
  
    
    

<span data-ttu-id="a09d6-235">**Рисунок 18. Два канала устройства с отдельными эталонными страницами**</span><span class="sxs-lookup"><span data-stu-id="a09d6-235">**Figure 18. Two device channels with separate master pages**</span></span>

  
    
    

  
    
    
![Два канала устройств с отдельными главными страницами](../images/122_123_two_channels_two_master_pages.gif)
  
    
    
<span data-ttu-id="a09d6-p123">Вы можете многое реализовать, используя только CSS. Это возможно для эталонных страниц для двух различных каналов (например, компьютер и телефон), которые идентичны за исключением ссылки на разные таблицы стилей. Файлы CSS просто используют различные стили для одних и тех же элементов страницы.</span><span class="sxs-lookup"><span data-stu-id="a09d6-p123">You can accomplish a great deal using only CSS. It is possible for the master pages for two different channels (for example, desktop and phone) to be identical except that they link to different style sheets. The CSS files simply use different styles for the same page elements.</span></span>
  
    
    

### <a name="relationship-of-master-pages-and-page-layouts"></a><span data-ttu-id="a09d6-240">Отношение эталонных страниц и макетов страниц</span><span class="sxs-lookup"><span data-stu-id="a09d6-240">Relationship of master pages and page layouts</span></span>

<span data-ttu-id="a09d6-p124">В отличие от эталонных страниц вы не указываете различным каналам устройств различные макеты страниц. Все макеты работают со всеми созданными вами каналами. Соответственно, один макет страницы применяется ко многим каналам устройств и эталонным страницам.</span><span class="sxs-lookup"><span data-stu-id="a09d6-p124">Unlike master pages, you do not specify different page layouts for different device channels. All page layouts work with all channels that you create. Thus, one page layout applies to many device channels and master pages.</span></span>
  
    
    
<span data-ttu-id="a09d6-p125">Это основное преимущество каналов устройств  изменяется структура (эталонной страницы или файла CSS), а контент остается тем же (макеты страниц и страницы). Однако вы можете изменять отображаемый по различным каналам контент из макета страницы с помощью панелей канала устройств (см. следующий раздел).</span><span class="sxs-lookup"><span data-stu-id="a09d6-p125">This is one of the primary benefits of device channels: the design changes (the master page and CSS), but the content stays the same (page layouts and pages). But, you can vary what content from a page layout is displayed across different channels by using device channel panels (see the next section).</span></span>
  
    
    

<span data-ttu-id="a09d6-246">**Рисунок 19. Один макет страницы, работающий с двумя макетами страниц**</span><span class="sxs-lookup"><span data-stu-id="a09d6-246">**Figure 19. One page layout working with two master pages**</span></span>

  
    
    

  
    
    
![Макет одной страницы работает с двумя главными страницами](../images/124_one_layout_many_masters.gif)
  
    
    

  
    
    

  
    
    

### <a name="device-channel-panels"></a><span data-ttu-id="a09d6-248">Панели каналов устройств</span><span class="sxs-lookup"><span data-stu-id="a09d6-248">Device channel panels</span></span>

<span data-ttu-id="a09d6-p126">Панель канала устройства  это элемент управления, который можно добавить на эталонную страницу, макет страницы или шаблон для отображения, чтобы управлять отображаемым на каждом канале контентом. Панель каналов, по сути, является контейнером, который определяет один или несколько каналов; если один или более этих каналов активны при отображении страницы, то отображается также и контент панели каналов. Панель каналов может включать любой тип контента, включая ссылку на CSS- или JS-файл, и это простой способ включить определенный контент для определенных каналов.</span><span class="sxs-lookup"><span data-stu-id="a09d6-p126">A device channel panel is a control that you can add to a master page, page layout, or display template to control what content is rendered in each channel. A channel panel is basically a container that specifies one or more channels; if one or more of those channels are active when the page is rendered, all of the contents of the channel panel are also rendered. A channel panel can include any type of content, including a link to a CSS file or a .js file, and is an easy way to include specific content for specific channels.</span></span>
  
    
    
<span data-ttu-id="a09d6-p127">Пожалуй, наиболее распространенным сценарием использования панелей каналов является выборочное включение частей макета страницы для определенных каналов. Например, у вас есть макет страницы с отдельными текстовыми полями для длинного и короткого приветствий. Поместив поля страницы внутри панелей каналов, вы можете отображать только короткое приветствие для телефонов и только длинное  для компьютеров. Контент панели каналов устройств не отображается для каналов, в которые он не включен, и контент внутри этой панели каналов устройств не отображается вообще, что запрещает передачу данных по кабельной сети.</span><span class="sxs-lookup"><span data-stu-id="a09d6-p127">Perhaps the most common scenario for using channel panels is to selectively include parts of a page layout for specific channels. For example, you may have a page layout with separate text fields for a long greeting and a short greeting. By placing the page fields inside channel panels, you can display the short greeting only to phones and the long greeting only to desktops. The content of a device channel panel is not displayed to channels that it doesn't include—and the content inside that device channel panel is not rendered at all, which prevents bytes from going across the wire.</span></span>
  
    
    

<span data-ttu-id="a09d6-256">**Рисунок 20. Макет страницы с панелями каналов**</span><span class="sxs-lookup"><span data-stu-id="a09d6-256">**Figure 20. Page layout with channel panels**</span></span>

  
    
    

  
    
    
![Макет страницы с панелями канала](../images/125_126_page_layout_with_channel_panels.gif)
  
    
    
<span data-ttu-id="a09d6-p128">Кроме того, вы можете использовать панели каналов на эталонных страницах. Например, если у вас есть эталонная страница, которую можно приспособить для двух различных устройств (или двух различных браузеров) с минимальными изменениями, вы можете использовать панели каналов, чтобы хранить контент на эталонной странице, которая уникальна для каждого из этих устройств.</span><span class="sxs-lookup"><span data-stu-id="a09d6-p128">You can also use channel panels on master pages. For example, if you have a master page that can accommodate two different devices (or two different browsers) with only minimal changes, you can use channel panels to hold the content on the master page that is specific to each of those devices.</span></span>
  
    
    
<span data-ttu-id="a09d6-260">Или вы можете использовать панель каналов внутри шаблона отображения элемента для веб-части поиска контента, чтобы отображать дополнительные управляемые свойства для этого элемента только из каталога для компьютеров, но не для телефонов.</span><span class="sxs-lookup"><span data-stu-id="a09d6-260">Or, you can use a channel panel inside the item display template of a Content Search Web Part, to display additional managed properties for that item from the catalog only for desktops and not for phones.</span></span>
  
    
    

<span data-ttu-id="a09d6-261">**Рисунок 21. Макет страницы и шаблоны элементов с панелями каналов**</span><span class="sxs-lookup"><span data-stu-id="a09d6-261">**Figure 21. Page layout and item templates with channel panels**</span></span>

  
    
    

  
    
    
![Макет страницы и шаблоны элементов с панелями канала](../images/127_128_item_display_templates_with_channel_panel.gif)
  
    
    

  
    
    

  
    
    

## <a name="see-also"></a><span data-ttu-id="a09d6-263">См. также</span><span class="sxs-lookup"><span data-stu-id="a09d6-263">See also</span></span>
<span data-ttu-id="a09d6-264"><a name="bk_AdditionalResources"> </a></span><span class="sxs-lookup"><span data-stu-id="a09d6-264"><a name="bk_AdditionalResources"> </a></span></span>


-  [<span data-ttu-id="a09d6-265">Обзор Дизайнера в SharePoint</span><span class="sxs-lookup"><span data-stu-id="a09d6-265">Overview of Design Manager in SharePoint</span></span>](overview-of-design-manager-in-sharepoint.md)
    
  
-  [<span data-ttu-id="a09d6-266">Создание сайтов для SharePoint</span><span class="sxs-lookup"><span data-stu-id="a09d6-266">Build sites for SharePoint</span></span>](build-sites-for-sharepoint.md)
    
  
-  [<span data-ttu-id="a09d6-267">Шаблоны отображения Дизайнера SharePoint</span><span class="sxs-lookup"><span data-stu-id="a09d6-267">SharePoint Design Manager display templates</span></span>](sharepoint-design-manager-display-templates.md)
    
  
-  [<span data-ttu-id="a09d6-268">Каналы устройств в компоненте "Дизайнер" SharePoint</span><span class="sxs-lookup"><span data-stu-id="a09d6-268">SharePoint Design Manager device channels</span></span>](sharepoint-design-manager-device-channels.md)
    
  

