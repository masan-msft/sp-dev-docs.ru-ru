---
title: "Инструкции. Настройка макетов страниц для сайта на основе каталога в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 21d8db99-73b3-4429-b6cb-04e375af9f55
ms.openlocfilehash: 33c3859956e80ceae0c3171906b0784fb6726146
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-customize-page-layouts-for-a-catalog-based-site-in-sharepoint"></a><span data-ttu-id="12611-102">Инструкции. Настройка макетов страниц для сайта на основе каталогов в SharePoint</span><span class="sxs-lookup"><span data-stu-id="12611-102">How to: Customize page layouts for a catalog-based site in SharePoint</span></span>
<span data-ttu-id="12611-103">Узнайте, как создавать и настраивать макеты страниц категорий и страниц элементов каталога для сайта SharePoint с публикацией на нескольких сайтах.</span><span class="sxs-lookup"><span data-stu-id="12611-103">Learn how to create and customize category page and catalog-item page layouts for a SharePoint Server 2013 cross-site publishing site.</span></span>
## <a name="prerequisites-for-creating-and-customizing-page-layouts-for-a-catalog-based-site"></a><span data-ttu-id="12611-104">Необходимые компоненты для создания и настройки макетов страниц сайта на основе каталогов</span><span class="sxs-lookup"><span data-stu-id="12611-104">Prerequisites for creating and customizing page layouts for a catalog-based site</span></span>
<span data-ttu-id="12611-105"><a name="bk_prereqs"> </a></span><span class="sxs-lookup"><span data-stu-id="12611-105"></span></span>

<span data-ttu-id="12611-106">Для выполнения действий, описанных в этом примере, вам необходимо следующее:</span><span class="sxs-lookup"><span data-stu-id="12611-106">To follow the steps in this example, you must have the following:</span></span>
  
    
    

- <span data-ttu-id="12611-107">редактор HTML;</span><span class="sxs-lookup"><span data-stu-id="12611-107">An HTML editor</span></span>
    
  
- <span data-ttu-id="12611-108">среда SharePoint для публикации на нескольких сайтах.</span><span class="sxs-lookup"><span data-stu-id="12611-108">A SharePoint Server 2013 cross-site publishing environment</span></span>
    
  
<span data-ttu-id="12611-109">Сведения о настройке среды SharePoint для публикации на нескольких сайтах см. в статье [Настройка публикации на нескольких сайтах в SharePoint](http://technet.microsoft.com/en-us/library/jj656774.aspx).</span><span class="sxs-lookup"><span data-stu-id="12611-109">For information about how to set up a SharePoint cross-site publishing environment, see  [Configure cross-site publishing in SharePoint Server 2013](http://technet.microsoft.com/en-us/library/jj656774.aspx).</span></span>
  
    
    

### <a name="core-concepts-to-know-for-creating-and-customizing-page-layouts-for-a-catalog-based-site"></a><span data-ttu-id="12611-110">Основные понятия, используемые при создании и настройке макетов страниц сайта на основе каталогов</span><span class="sxs-lookup"><span data-stu-id="12611-110">Core concepts to know for creating and customizing page layouts for a catalog-based site</span></span>

<span data-ttu-id="12611-111">В таблице 1 приведены полезные статьи, которые помогут изучить основные понятия и действия, используемые для создания и настройки макетов страниц сайта на основе каталога.</span><span class="sxs-lookup"><span data-stu-id="12611-111">Table 1 lists useful articles that can help you understand the concepts and steps that are involved in creating and customizing page layouts for a catalog-based site.</span></span>
  
    
    

<span data-ttu-id="12611-112">**Таблица 1. Основные понятия, используемые при создании и настройке макетов страниц сайта на основе каталога**</span><span class="sxs-lookup"><span data-stu-id="12611-112">**Table 1. Core concepts for creating and customizing page layouts for a catalog-based site**</span></span>


|<span data-ttu-id="12611-113">**Название статьи**</span><span class="sxs-lookup"><span data-stu-id="12611-113">**Article title**</span></span>|<span data-ttu-id="12611-114">**Описание**</span><span class="sxs-lookup"><span data-stu-id="12611-114">**Description**</span></span>|
|:-----|:-----|
| <span data-ttu-id="12611-115">
  [Обзор публикации на нескольких сайтах в SharePoint](http://technet.microsoft.com/en-us/library/jj635883.aspx)</span><span class="sxs-lookup"><span data-stu-id="12611-115">[Overview of cross-site publishing in SharePoint Server 2013](http://technet.microsoft.com/en-us/library/jj635883.aspx)</span></span> <br/> |<span data-ttu-id="12611-116">Узнайте, как использовать веб-части поиска и публикацию на нескольких сайтах для создания адаптивных сайтов Интернета, интрасети и экстрасети SharePoint.</span><span class="sxs-lookup"><span data-stu-id="12611-116">Learn about how to use cross-site publishing and Search Web Parts to create adaptive SharePoint Internet, intranet, and extranet sites.</span></span>  <br/> |
| [<span data-ttu-id="12611-117">Инструкции. Создание макета страницы в SharePoint</span><span class="sxs-lookup"><span data-stu-id="12611-117">How to: Create a page layout in SharePoint</span></span>](how-to-create-a-page-layout-in-sharepoint.md) <br/> |<span data-ttu-id="12611-118">Узнайте, как создавать макеты страниц в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="12611-118">Learn about how to create page layouts in SharePoint Server 2013.</span></span>  <br/> |
| [<span data-ttu-id="12611-119">Инструкции. Устранение ошибок и предупреждений при предварительном просмотре страницы в SharePoint</span><span class="sxs-lookup"><span data-stu-id="12611-119">How to: Resolve errors and warnings when previewing a page in SharePoint</span></span>](how-to-resolve-errors-and-warnings-when-previewing-a-page-in-sharepoint.md) <br/> |<span data-ttu-id="12611-120">Узнайте о способах устранения проблем, которые препятствуют отрисовке страницы при предварительном просмотре со стороны сервера.</span><span class="sxs-lookup"><span data-stu-id="12611-120">Learn about how to resolve any issues that prevent the server-side preview from rendering your page.</span></span>  <br/> |
| [<span data-ttu-id="12611-121">Фрагменты кода дизайнер SharePoint</span><span class="sxs-lookup"><span data-stu-id="12611-121">SharePoint Design Manager snippets</span></span>](sharepoint-design-manager-snippets.md) <br/> |<span data-ttu-id="12611-122">Узнайте о способах использования фрагментов для добавления функций SharePoint на главную страницу HTML или макет страницы.</span><span class="sxs-lookup"><span data-stu-id="12611-122">Learn about how to use snippets to add SharePoint functionality to your HTML master page or page layout.</span></span>  <br/> |
   

## <a name="introduction-to-category-page-layouts-and-catalog-item-page-layouts"></a><span data-ttu-id="12611-123">Общие сведения о макетах страниц категорий и страниц элементов каталога</span><span class="sxs-lookup"><span data-stu-id="12611-123">Introduction to category page layouts and catalog item page layouts</span></span>
<span data-ttu-id="12611-124"><a name="bk_introduction"> </a></span><span class="sxs-lookup"><span data-stu-id="12611-124"></span></span>

<span data-ttu-id="12611-125">Страницы категорий и страницы элементов каталога — это макеты страниц, которые можно использовать для согласованного отображения структурированного содержимого каталога на сайте.</span><span class="sxs-lookup"><span data-stu-id="12611-125">Category pages and catalog item pages are page layouts that you can use to show structured catalog content consistently across a site. SharePoint 2013 enables you to create and customize page layouts for SharePoint Server 2013 and above. For more information, see  Customize page layouts for a catalog-based site in SharePoint 2013.</span></span> <span data-ttu-id="12611-126">По умолчанию SharePoint может автоматически создать один макет страницы категорий и один макет страницы элементов каталога для подключения к каталогу.</span><span class="sxs-lookup"><span data-stu-id="12611-126">By default, SharePoint can automatically create one category page layout and one catalog item page layout per catalog connection.</span></span> <span data-ttu-id="12611-127">Страницы, основанные на этих макетах, создаются в библиотеке страниц сайта публикации при подключении сайта к каталогу.</span><span class="sxs-lookup"><span data-stu-id="12611-127">Pages based on these layouts are created in the Pages library of a publishing site when you connect the site to a catalog.</span></span> <span data-ttu-id="12611-128">Дополнительные сведения о макетах страниц см. в статье [Инструкции. Создание макета страницы в SharePoint](how-to-create-a-page-layout-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="12611-128">For more information, see  [How to: Create a page layout in SharePoint](how-to-create-a-page-layout-in-sharepoint.md).</span></span> <span data-ttu-id="12611-129">Дополнительные сведения о функциях, связанных с макетами страниц категорий и макетами страниц элементов каталога, см. в статье [Обзор публикации на нескольких сайтах в SharePoint](http://technet.microsoft.com/en-us/library/jj635883.aspx).</span><span class="sxs-lookup"><span data-stu-id="12611-129">For more information about features that are specific to category page layouts and catalog item page layouts, see  [Overview of cross-site publishing in SharePoint](http://technet.microsoft.com/en-us/library/jj635883.aspx).</span></span>
  
    
    
<span data-ttu-id="12611-p102">По умолчанию макеты страниц категорий и страниц элементов каталога создаются автоматически при подключении сайта публикации к каталогу. Вы также можете использовать Дизайнер для создания макетов страниц категорий и страниц элементов каталога, которые можно выбрать при подключении сайта публикации к каталогу или при настройке банка терминов навигации на сайте публикации.</span><span class="sxs-lookup"><span data-stu-id="12611-p102">By default, category page layouts and catalog item page layouts are created automatically when you connect a publishing site to a catalog. You can also use Design Manager to create category page layouts and catalog item page layouts that you can select when you connect a publishing site to a catalog, or when you configure the navigation term set on a publishing site.</span></span>
  
    
    

## <a name="create-a-category-page-layout"></a><span data-ttu-id="12611-132">Создание макета страницы категорий</span><span class="sxs-lookup"><span data-stu-id="12611-132">Create a category page layout</span></span>
<span data-ttu-id="12611-133"><a name="bk_createCategoryPage"> </a></span><span class="sxs-lookup"><span data-stu-id="12611-133"></span></span>

<span data-ttu-id="12611-p103">Перед созданием или настройкой макета страницы категорий мы рекомендуем создать сопоставленный сетевой диск, который указывает на **коллекцию главных страниц**. Дополнительные сведения см. в разделе  [Как: сопоставление сетевого диска коллекции главных страниц SharePoint](how-to-map-a-network-drive-to-the-sharepoint-master-page-gallery.md).</span><span class="sxs-lookup"><span data-stu-id="12611-p103">Before you can create or customize a category page layout, we recommend that you create a mapped network drive that points to the **Master Page Gallery**. For more information, see  [How to: Map a network drive to the SharePoint Master Page Gallery](how-to-map-a-network-drive-to-the-sharepoint-master-page-gallery.md).</span></span>
  
    
    
<span data-ttu-id="12611-p104">Самый простой способ создать макет страницы категорий — позволить SharePoint автоматически сделать это при подключении сайта публикации к каталогу, а затем изменить разметку существующего макета. Кроме того, можно создать макет страницы категорий с нуля с помощью Дизайнера.</span><span class="sxs-lookup"><span data-stu-id="12611-p104">The simplest way to create a category page layout is to let SharePoint create the page layout automatically when you connect the publishing site to a catalog, and then customize the existing category page layout to change the markup as required by the page design. Alternatively, you can create a new category page layout from scratch by using Design Manager.</span></span>
  
    
    

### <a name="to-customize-an-existing-category-page-layout-that-was-created-automatically-by-sharepoint"></a><span data-ttu-id="12611-138">Настройка макета страницы категорий, созданного SharePoint автоматически</span><span class="sxs-lookup"><span data-stu-id="12611-138">To customize an existing category page layout that was created automatically by SharePoint</span></span>


1. <span data-ttu-id="12611-139">С помощью проводника Windows откройте сетевой диск, сопоставленный с коллекцией главных страниц.</span><span class="sxs-lookup"><span data-stu-id="12611-139">Using Windows Explorer, open the mapped network drive to the Master Page Gallery.</span></span>
    
  
2. <span data-ttu-id="12611-p105">Чтобы настроить макет страницы категорий, измените HTML-файл, который находится непосредственно на сервере. Для этого откройте и измените HTML-файл на сопоставленном диске с помощью HTML-редактора. Каждый раз при сохранении HTML-файл все изменения синхронизируются со связанным ASPX-файлом.</span><span class="sxs-lookup"><span data-stu-id="12611-p105">To customize a category page layout, edit the HTML file that resides directly on the server by using an HTML editor to open and edit the HTML file in the mapped drive. Each time that you save the HTML file, any changes are synched to the associated .aspx file.</span></span>
    
  
3. <span data-ttu-id="12611-142">Замените часть кода в заполнителе контента с элементом **id="PlaceHolderMain"** тем кодом, который требуется использовать в макете страницы.</span><span class="sxs-lookup"><span data-stu-id="12611-142">Replace the markup inside the content placeholder that has **id="PlaceHolderMain"** with the markup that you want to use in the page layout.</span></span>
    
    > <span data-ttu-id="12611-143">**Важно!** Сохраните фрагмент кода для поиска контента, чтобы на странице категорий можно было отображать результаты поиска.</span><span class="sxs-lookup"><span data-stu-id="12611-143">**Important** You must keep the Content Search Snippet markup so that the category page can display search results.</span></span> 
4. <span data-ttu-id="12611-144">Чтобы изменить и скопировать HTML-код для всех фрагментов, которые необходимо добавить на страницу, выполните шаги с 1 по 11 из раздела "Вставка фрагмента из коллекции фрагментов" статьи  [Фрагменты кода дизайнер SharePoint](sharepoint-design-manager-snippets.md).</span><span class="sxs-lookup"><span data-stu-id="12611-144">To configure and copy the HTML for any snippets you want to add to the page, follow step 1 through step 11 in the "Insert a snippet from the Snippet Gallery" section of  [SharePoint Design Manager snippets](sharepoint-design-manager-snippets.md).</span></span>
    
  
5. <span data-ttu-id="12611-145">Внесите необходимые изменения в разметку и сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="12611-145">Make any other required changes to the markup, and then save the file.</span></span>
    
  
6. <span data-ttu-id="12611-146">Выполните шаги с 9 по 11 из раздела "Создание макета страницы" статьи  [Инструкции. Создание макета страницы в SharePoint](how-to-create-a-page-layout-in-sharepoint.md), чтобы проверить состояние файла, просмотреть макет страницы и устранить все ошибки.</span><span class="sxs-lookup"><span data-stu-id="12611-146">Follow step 9 through step 11 in the "Create a page layout" section of  [How to: Create a page layout in SharePoint](how-to-create-a-page-layout-in-sharepoint.md) to check the status of the file, preview the page layout, and fix any errors.</span></span>
    
  

### <a name="to-create-a-category-page-layout-by-using-design-manager"></a><span data-ttu-id="12611-147">Создание макета страницы категорий с помощью Дизайнера</span><span class="sxs-lookup"><span data-stu-id="12611-147">To create a category page layout by using Design Manager</span></span>


1. <span data-ttu-id="12611-148">Выполните шаги 1-6 из раздела "Создание макета страницы" статьи  [Инструкции. Создание макета страницы в SharePoint](how-to-create-a-page-layout-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="12611-148">Follow step 1 through step 6 in the "Create a page layout" section of  [How to: Create a page layout in SharePoint](how-to-create-a-page-layout-in-sharepoint.md).</span></span>
    
  
2. <span data-ttu-id="12611-149">На шаге 7 выберите тип контента **Страница статьи**.</span><span class="sxs-lookup"><span data-stu-id="12611-149">In step 7, choose the **Article Page** content type.</span></span>
    
  
3. <span data-ttu-id="12611-150">Нажмите кнопку **OK**.</span><span class="sxs-lookup"><span data-stu-id="12611-150">Choose **OK**.</span></span>
    
    <span data-ttu-id="12611-151">На этом этапе SharePoint создает HTML-файл и ASPX-файл с таким же именем.</span><span class="sxs-lookup"><span data-stu-id="12611-151">At this point, SharePoint creates an HTML file and an .aspx file that has the same name.</span></span>
    
    <span data-ttu-id="12611-152">В Дизайнере HTML-файл теперь отображается со столбцом **Состояние**, в котором отображается одно из двух состояний:</span><span class="sxs-lookup"><span data-stu-id="12611-152">In Design Manager, your HTML file now appears with a **Status** column that shows one of two statuses:</span></span>
    
  - <span data-ttu-id="12611-153">Ошибки</span><span class="sxs-lookup"><span data-stu-id="12611-153">**Warnings and Errors**</span></span>
    
  
  - <span data-ttu-id="12611-154">**Преобразование выполнено успешно**.</span><span class="sxs-lookup"><span data-stu-id="12611-154">**Conversion successful**</span></span>
    
  
4. <span data-ttu-id="12611-155">С помощью проводника Windows откройте сетевой диск, сопоставленный с коллекцией главных страниц.</span><span class="sxs-lookup"><span data-stu-id="12611-155">Using Windows Explorer, open the mapped network drive to the Master Page Gallery.</span></span>
    
  
5. <span data-ttu-id="12611-p106">Чтобы настроить макет страницы категорий, измените HTML-файл, который находится непосредственно на сервере. Для этого откройте и измените HTML-файл на сопоставленном диске с помощью HTML-редактора. Каждый раз при сохранении HTML-файл все изменения синхронизируются со связанным ASPX-файлом.</span><span class="sxs-lookup"><span data-stu-id="12611-p106">To customize the category page layout, edit the HTML file that resides directly on the server by using an HTML editor to open and edit the HTML file in the mapped drive. Each time that you save the HTML file, any changes are synched to the associated .aspx file.</span></span>
    
  
6. <span data-ttu-id="12611-158">В теге **\<head\>** замените заполнитель контента с элементом **id="PlaceHolderPageTitle"** следующим:</span><span class="sxs-lookup"><span data-stu-id="12611-158">In the <head> tag, replace the content placeholder that has id="PlaceHolderPageTitle" with:</span></span>
    
```HTML
  
<!--MS:<asp:ContentPlaceHolder id="PlaceHolderPageTitle" runat="server">-->
<!--CS: Start Taxonomy TermProperty Snippet-->
<!--SPM:<%@Register Tagprefix="Taxonomy"  Namespace="Microsoft.SharePoint.Taxonomy" Assembly="Microsoft.SharePoint.Taxonomy, Version=15.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" %>-->
<!--MS:<Taxonomy:TermProperty Property="Name" runat="server">-->
<!--ME:</Taxonomy:TermProperty>-->
<!--ME:</asp:ContentPlaceHolder>-->
```

7. <span data-ttu-id="12611-159">Найдите заполнитель контента с элементом **id="PlaceHolderPageTitleInTitleArea"** и замените следующим:</span><span class="sxs-lookup"><span data-stu-id="12611-159">Find the content placeholder that has the **id="PlaceHolderPageTitleInTitleArea"** and replace it with:</span></span>
    
```HTML
  
<!--MS:<asp:ContentPlaceHolder id="PlaceHolderPageTitleInTitleArea" runat="server">-->
<!--SPM:<asp:SiteMapPath runat="server" ParentLevelsDisplayed="1" SiteMapProvider="CurrentNavigationSwitchableProvider"/>-->
<!--ME:</asp:ContentPlaceHolder>-->
```

8. <span data-ttu-id="12611-160">Замените разметку в заполнителе контента, содержащего элемент **id="PlaceHolderMain"** с разметкой, которую требуется использовать в макете страницы.</span><span class="sxs-lookup"><span data-stu-id="12611-160">Replace the markup inside the content placeholder that has **id="PlaceHolderMain"** with the markup that you want to use in the page layout.</span></span>
    
  
9. <span data-ttu-id="12611-161">Чтобы изменить и скопировать HTML-код для фрагмента поиска контента и других фрагментов, которые необходимо добавить на страницу, выполните шаги с 1 по 11 из раздела "Вставка фрагмента из коллекции фрагментов" статьи  [Фрагменты кода дизайнер SharePoint](sharepoint-design-manager-snippets.md).</span><span class="sxs-lookup"><span data-stu-id="12611-161">To configure and copy the HTML for the Content Search Snippet and any other snippets you want to add to the page, follow step 1 through step 11 in the "Insert a snippet from the Snippet Gallery" section of  [SharePoint Design Manager snippets](sharepoint-design-manager-snippets.md).</span></span>
    
    > <span data-ttu-id="12611-162">**Примечание.** При добавлении фрагмента кода для поиска контента в макет страницы обязательно измените запрос так, чтобы использовать источник результатов, созданный при подключении сайта публикации к каталогу.</span><span class="sxs-lookup"><span data-stu-id="12611-162">**Note** When you add the Content Search Snippet to the page layout, be sure to change the query to use the result source that was created when you connected the publishing site to a catalog. For more information, see  Configure result sources for web content management in SharePoint Server 2013.</span></span> <span data-ttu-id="12611-163">Дополнительные сведения см. в статье [Настройка источников результатов для управления веб-контентом в SharePoint](http://technet.microsoft.com/en-us/library/jj715262.aspx).</span><span class="sxs-lookup"><span data-stu-id="12611-163">For more information, see  [Configure result sources for web content management in SharePoint](http://technet.microsoft.com/en-us/library/jj715262.aspx).</span></span> 
10. <span data-ttu-id="12611-164">Внесите другие необходимые изменения в код и сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="12611-164">Make any other required changes to the markup, and then save the file.</span></span>
    
  
11. <span data-ttu-id="12611-165">Выполните шаги с 9 по 11 из раздела "Создание макета страницы" статьи  [Инструкции. Создание макета страницы в SharePoint](how-to-create-a-page-layout-in-sharepoint.md), чтобы проверить состояние файла, просмотреть макет страницы и устранить все ошибки.</span><span class="sxs-lookup"><span data-stu-id="12611-165">Follow step 9 through step 11 in the "Create a page layout" section of  [How to: Create a page layout in SharePoint](how-to-create-a-page-layout-in-sharepoint.md) to check the status of the file, preview the page layout, and fix any errors.</span></span>
    
  

## <a name="understanding-the-markup-in-the-html-category-page-layout"></a><span data-ttu-id="12611-166">Общие сведения о разметке в макете страницы категорий HTML</span><span class="sxs-lookup"><span data-stu-id="12611-166">Understanding the markup in the HTML category page layout</span></span>
<span data-ttu-id="12611-167"><a name="bk_CategoryPageMarkup"> </a></span><span class="sxs-lookup"><span data-stu-id="12611-167"></span></span>

<span data-ttu-id="12611-p108">При создании макета страницы создается ASPX-файл, используемый SharePoint, а определенная HTML-разметка добавляется в HTML-версию макета страницы. Макеты страниц категорий содержат компоненты разметки, добавляемые в зависимости от функции публикации в нескольких семействах сайтов и которые уникальны для макетов страниц категорий. Если вы хотите изменить макет страницы категорий HTML в редакторе HTML, вам будет полезно ознакомиться с этой разметкой.</span><span class="sxs-lookup"><span data-stu-id="12611-p108">When you create a page layout, an .aspx file is created that SharePoint uses, and some HTML markup is added to the HTML version of the page layout. Category page layouts have markup components that are added to the page layout based on the Cross-Site Collection Publishing feature, and that are unique to category page layouts. When you edit the HTML category page layout in your HTML editor, it might be helpful to understand some of this markup.</span></span>
  
    
    

### <a name="browser-window-page-title"></a><span data-ttu-id="12611-171">Заголовок страницы в окне браузера</span><span class="sxs-lookup"><span data-stu-id="12611-171">Browser window page title</span></span>

<span data-ttu-id="12611-p109">Компонент, который отображается в заполнителе контента с **id="PlaceHolderPageTitle"**, содержит разметку, которая сообщает SharePoint о необходимости использования свойства термина в качестве заголовка страницы в окне браузера вместо стандартного значения поля страницы. В следующем коде показана разметка для заголовка страницы в окне браузера.</span><span class="sxs-lookup"><span data-stu-id="12611-p109">The component that appears inside the content placeholder with **id="PlaceHolderPageTitle"** contains markup that tells SharePoint to use a term property as the page title in the browser window, instead of using the standard page field value. The following code shows the markup for the browser window page title.</span></span>
  
    
    

```HTML

<!--CS: Start Taxonomy TermProperty Snippet-->
<!--SPM:<%@Register Tagprefix="Taxonomy"  Namespace="Microsoft.SharePoint.Taxonomy" Assembly="Microsoft.SharePoint.Taxonomy, Version=15.0.0.0, Culture=neutral, 
PublicKeyToken=71e9bce111e9429c" %>-->
<!--MS:<Taxonomy:TermProperty Property="Name" runat="server">-->
<!--ME:</Taxonomy:TermProperty>-->
```


### <a name="page-title"></a><span data-ttu-id="12611-174">Заголовок страницы</span><span class="sxs-lookup"><span data-stu-id="12611-174">Page title</span></span>

<span data-ttu-id="12611-p110">Компонент, который отображается в заполнителе контента с **id="PlaceHolderPageTitleInTitleArea"**, содержит разметку, которая сообщает SharePoint о необходимости использования свойства термина в качестве заголовка страницы вместо фрагмента **SPTitleBreadcrumb** и стандартного значения поля заголовка страницы. В следующем коде показана разметка для заголовка страницы.</span><span class="sxs-lookup"><span data-stu-id="12611-p110">The component that appears inside the content placeholder with **id="PlaceHolderPageTitleInTitleArea"** contains markup that tells SharePoint to use a term property as the page title on the page, instead of using the **SPTitleBreadcrumb** snippet and the standard page title field value. The following code shows the markup for the page title.</span></span>
  
    
    

```HTML

<!--SPM:<asp:SiteMapPath runat="server" ParentLevelsDisplayed="1" SiteMapProvider="CurrentNavigationSwitchableProvider"/>-->"
```


### <a name="content-search-snippet"></a><span data-ttu-id="12611-177">Фрагмент поиска контента</span><span class="sxs-lookup"><span data-stu-id="12611-177">Content Search Snippet</span></span>

<span data-ttu-id="12611-p111">Компоненты, которые отображаются после фрагмента контента страницы, в заполнителе контента с **id="PlaceHolderMain"**, содержат разметку для фрагмента зоны веб-части, которая содержит четыре зоны веб-частей. Первая зона включает в себя фрагмент поиска контента, который отображает веб-часть поиска контента на странице. Этот фрагмент также содержит сведения, которые помогают веб-части поиска контента запросить источник результатов и показать результаты на странице. Последние три зоны веб-частей будут пустыми. Если вы решили создать макет страницы категорий, необходимо добавить разметку для фрагмента поиска контента в HTML-файл разметки страницы. В следующем коде показана разметка для фрагмента поиска контента. Замените  _ResultSourceID_ на GUID источника результатов, а вместо _CatalogURL_ укажите URL-адрес каталога.</span><span class="sxs-lookup"><span data-stu-id="12611-p111">The components that appear after the page content snippet, inside the content placeholder with **id="PlaceHolderMain"**, contain markup for a Web Part Zone Snippet that contains four Web Part zones. The first Web Part zone contains a Content Search Snippet that displays a Content Search Web Part on the page. This snippet also contains information that helps the Content Search Web Part query a result source and show the results on the page. The last three Web Part zones are empty. If you choose to create your own category page layout, you must include the markup for the Content Search Snippet in the HTML file for your page layout. The following code shows the markup for the Content Search snippet. Replace  _ResultSourceID_ with the GUID of the result source, and replace _CatalogURL_ with the URL of the catalog.</span></span>
  
    
    

> <span data-ttu-id="12611-185">**Примечание.** Идентификаторы GUID для **ID** и **\_\_WebPartId** случайным образом создаются SharePoint при добавлении фрагментов кода в макет страницы.</span><span class="sxs-lookup"><span data-stu-id="12611-185">Note The GUIDs for ID and __WebPartId are randomly generated by SharePoint when the snippets are added to the page layout.</span></span>
  
    
    


```HTML
<!--
CS: Start Content Search Snippet-->
<!--SPM:<%@Register Tagprefix="a781102493" Namespace="Microsoft.Office.Server.Search.WebControls" Assembly="Microsoft.Office.Server.Search, Version=15.0.0.0, Culture=neutral, 
PublicKeyToken=71e9bce111e9429c"%>-->
<!--MS:<a781102493:ContentBySearchWebPart runat="server" DataProviderJSON="{&amp;#34;QueryTemplate&amp;#34;:&amp;#34;&amp;#34;,&amp;#34;SourceID&amp;#34;
:&amp;#34;ResultSourceID&amp;#34;,&amp;#34;PropertiesJson&amp;#34;:&amp;#34;
{'Tag':'{Term.IDWithChildren}','Scope':'CatalogURL'}&amp;#34;}" ResultsPerPage="3" RenderTemplateId="~sitecollection/_catalogs/masterpage/Display Templates/Content Web Parts/Control_ListWithPaging.js" 
ItemTemplateId="~sitecollection/_catalogs/masterpage/Display Templates/Content Web Parts/Item_PictureOnTop.js" SelectedPropertiesJson="[&amp;#34;WorkId&amp;#34;,&amp;#34;Rank&amp;#34;,&amp;#34;Title&amp;#34;,&amp;#34;Author&amp;#34;,&amp;#34;
Size&amp;#34;,&amp;#34;Path&amp;#34;,&amp;#34;Description&amp;#34;,&amp;#34;Write&amp;#34;,&amp;#34;CollapsingStatus&amp;#34;,&amp;#34;
HitHighlightedSummary&amp;#34;,&amp;#34;HitHighlightedProperties&amp;#34;,&amp;#34;ContentClass&amp;#34;,&amp;#34;
PictureThumbnailURL&amp;#34;,&amp;#34;ServerRedirectedURL&amp;#34;,&amp;#34;ServerRedirectedEmbedURL&amp;#34;,&amp;#34;
ServerRedirectedPreviewURL&amp;#34;,&amp;#34;FileExtension&amp;#34;,&amp;#34;ContentTypeId&amp;#34;,&amp;#34;ParentLink&amp;#34;,&amp;#34;
ViewsLifeTime&amp;#34;,&amp;#34;ViewsRecent&amp;#34;,&amp;#34;SectionNames&amp;#34;,&amp;#34;SectionIndexes&amp;#34;,&amp;#34;
SiteLogo&amp;#34;,&amp;#34;SiteDescription&amp;#34;,&amp;#34;deeplinks&amp;#34;,&amp;#34;importance&amp;#34;]" ShouldHideControlWhenEmpty="True" FrameType="None" SuppressWebPartChrome="False" Description="$Resources:Microsoft.Office.Server.Search,CBS_Description;" IsIncluded="True" 
ZoneID="" PartOrder="0" FrameState="Normal" AllowRemove="True" AllowZoneChange="True" 
AllowMinimize="True" AllowConnect="True" AllowEdit="True" AllowHide="True" IsVisible="True" 
DetailLink="" HelpLink="" HelpMode="Modeless" Dir="Default" PartImageSmall="" IsIncludedFilter="" ExportControlledProperties="True" ConnectionID="00000000-0000-0000-0000-000000000000" ID="g_54e35103_6f29_4dd9_b93b_8d4c863834af" ChromeType="None" ExportMode="All" __MarkupType="vsattributemarkup" __WebPartId="54e35103-6f29-4dd9-b93b-8d4c863834af" 
WebPart="true" Height="" Width="" Title="$Resources:cms,WebPartZoneTitle_Dynamic;">-->
<!--ME:</a781102493:ContentBySearchWebPart>-->
<!--CE: End Content Search Snippet-->

```


## <a name="create-a-catalog-item-page-layout"></a><span data-ttu-id="12611-186">Создание макета страницы элементов каталога</span><span class="sxs-lookup"><span data-stu-id="12611-186">Create a catalog item page layout</span></span>
<span data-ttu-id="12611-187"><a name="bk_createCatItemPage"> </a></span><span class="sxs-lookup"><span data-stu-id="12611-187"></span></span>

<span data-ttu-id="12611-p112">Перед созданием или настройкой макета страницы элементов каталога мы рекомендуем создать сопоставленный сетевой диск, который указывает на коллекцию главных страниц. Дополнительные сведения см. в разделе  [Как: сопоставление сетевого диска коллекции главных страниц SharePoint](how-to-map-a-network-drive-to-the-sharepoint-master-page-gallery.md).</span><span class="sxs-lookup"><span data-stu-id="12611-p112">Before you can create or customize a catalog item page layout, we recommend that you create a mapped network drive that points to the Master Page Gallery. For more information, see  [How to: Map a network drive to the SharePoint Master Page Gallery](how-to-map-a-network-drive-to-the-sharepoint-master-page-gallery.md).</span></span>
  
    
    
<span data-ttu-id="12611-p113">Как и для макета страницы категорий, самый простой способ создать макет страницы элементов каталога — позволить SharePoint сделать это автоматически при подключении сайта публикации к каталогу и добавить в существующий макет дополнительную разметку. Кроме того, можно создать макет страницы элементов каталога с нуля с помощью Дизайнера.</span><span class="sxs-lookup"><span data-stu-id="12611-p113">As with the category page layout, the simplest way to create a catalog item page layout is to let SharePoint create the page layout automatically when you connect the publishing site to a catalog, and then customize the existing catalog item page layout to add any additional markup required by the page design. Alternatively, you can create a catalog item page layout from scratch by using Design Manager.</span></span>
  
    
    

### <a name="to-customize-an-existing-catalog-item-page-layout-that-was-created-automatically-by-sharepoint"></a><span data-ttu-id="12611-192">Настройка макета страницы элементов каталога, созданного SharePoint автоматически</span><span class="sxs-lookup"><span data-stu-id="12611-192">To customize an existing catalog item page layout that was created automatically by SharePoint</span></span>


1. <span data-ttu-id="12611-193">С помощью проводника Windows откройте сетевой диск, сопоставленный с коллекцией главных страниц.</span><span class="sxs-lookup"><span data-stu-id="12611-193">Using Windows Explorer, open the mapped network drive to the Master Page Gallery.</span></span>
    
  
2. <span data-ttu-id="12611-p114">Чтобы настроить макет страницы элементов каталога, измените HTML-файл, который находится непосредственно на сервере. Для этого откройте и измените HTML-файл на сопоставленном диске с помощью HTML-редактора. Каждый раз при сохранении HTML-файл все изменения синхронизируются со связанным ASPX-файлом.</span><span class="sxs-lookup"><span data-stu-id="12611-p114">To customize a catalog item page layout, edit the HTML file that resides directly on the server by using an HTML editor to open and edit the HTML file in the mapped drive. Each time that you save the HTML file, any changes are synched to the associated .aspx file.</span></span>
    
  
3. <span data-ttu-id="12611-196">Добавьте в заполнитель контента, содержащего элемент **id="PlaceHolderMain"**, разметку, которую требуется использовать в макете страницы.</span><span class="sxs-lookup"><span data-stu-id="12611-196">Inside the content placeholder that has **id="PlaceHolderMain"**, add the markup that you want to use in the page layout.</span></span>
    
  
4. <span data-ttu-id="12611-197">Удалите все фрагменты, которые не требуются, из макета страницы и переместите оставшиеся фрагменты туда, где необходимо показывать значения свойств.</span><span class="sxs-lookup"><span data-stu-id="12611-197">Delete any snippets that you do not want to use in the page layout, and move the remaining snippets to places in the markup where you want the property values to appear.</span></span>
    
    > <span data-ttu-id="12611-198">**Внимание!** По умолчанию фрагмент кода для зоны веб-частей, который содержит фрагмент кода для повторного использования элементов каталога, добавляется в макет страницы.</span><span class="sxs-lookup"><span data-stu-id="12611-198">**Caution:** By default, a Web Part Zone Snippet that contains a Catalog-Item Reuse Snippet is added to the page layout.</span></span> <span data-ttu-id="12611-199">Этот фрагмент кода включает в себя поставщик данных, возвращающий результаты запроса, которые используются всеми другими фрагментами кода на странице.</span><span class="sxs-lookup"><span data-stu-id="12611-199">This snippet contains the data provider that returns query results that are used by all other snippets on the page.</span></span> <span data-ttu-id="12611-200">Мы рекомендуем оставить этот фрагмент кода для повторного использования элементов каталога в данном фрагменте кода для зоны веб-частей по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="12611-200">We recommend that you keep the Catalog-Item Reuse Snippet in this default Web Part Zone Snippet.</span></span> <span data-ttu-id="12611-201">Можно переместить фрагмент кода для повторного использования элементов каталога за пределы зоны веб-частей, также можно изменить свойство, которое он показывает.</span><span class="sxs-lookup"><span data-stu-id="12611-201">(You can move the Catalog-Item Reuse Snippet outside the Web Part Zone, and you can change the property that it displays.</span></span> <span data-ttu-id="12611-202">Однако необходимо сохранить фрагмент кода для повторного использования элементов каталога в макете страницы. Дополнительные сведения см. разделе [Поля страницы](how-to-customize-page-layouts-for-a-catalog-based-site-in-sharepoint.md#bk_pagefields) далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="12611-202">But, you must keep the Catalog-Item Reuse Snippet in the page layout.) For more information, see  [Page fields](how-to-customize-page-layouts-for-a-catalog-based-site-in-sharepoint.md#bk_pagefields), later in this article.</span></span> 
5. <span data-ttu-id="12611-203">Чтобы изменить и скопировать HTML-код для всех фрагментов, которые необходимо использовать на странице, выполните шаги с 1 по 11 из раздела "Вставка фрагмента из коллекции фрагментов" статьи  [Фрагменты кода дизайнер SharePoint](sharepoint-design-manager-snippets.md).</span><span class="sxs-lookup"><span data-stu-id="12611-203">To configure and copy the HTML snippet for any snippets you want to use in the page, follow step 1 through step 11 in the "Insert a snippet from the Snippet Gallery" section of  [SharePoint Design Manager snippets](sharepoint-design-manager-snippets.md).</span></span>
    
  
6. <span data-ttu-id="12611-204">Внесите необходимые изменения в разметку и сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="12611-204">Make any other required changes to the markup, and then save the file.</span></span>
    
  
7. <span data-ttu-id="12611-205">Выполните шаги с 9 по 11 из раздела "Создание макета страницы" статьи  [Инструкции. Создание макета страницы в SharePoint](how-to-create-a-page-layout-in-sharepoint.md), чтобы проверить состояние файла, просмотреть макет страницы и устранить все ошибки.</span><span class="sxs-lookup"><span data-stu-id="12611-205">Follow step 9 through step 11 in the "Create a page layout" section of  [How to: Create a page layout in SharePoint](how-to-create-a-page-layout-in-sharepoint.md) to check the status of the file, preview the page layout, and fix any errors.</span></span>
    
  

### <a name="to-create-a-catalog-item-page-layout-by-using-design-manager"></a><span data-ttu-id="12611-206">Создание макета страницы элементов каталога с помощью Дизайнера</span><span class="sxs-lookup"><span data-stu-id="12611-206">To create a catalog item page layout by using Design Manager</span></span>


1. <span data-ttu-id="12611-207">Выполните шаги 1-6 из раздела "Создание макета страницы" статьи  [Инструкции. Создание макета страницы в SharePoint](how-to-create-a-page-layout-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="12611-207">Follow step 1 through step 6 in the "Create a page layout" section of  [How to: Create a page layout in SharePoint](how-to-create-a-page-layout-in-sharepoint.md).</span></span>
    
  
2. <span data-ttu-id="12611-208">На шаге 7 выберите **Удаленный каталог**, а затем выберите каталог, который содержит данные, которые будут отображаться на странице.</span><span class="sxs-lookup"><span data-stu-id="12611-208">In step 7, choose **Remote Catalog**, and then choose the catalog that contains the data to appear on the page.</span></span>
    
  
3. <span data-ttu-id="12611-209">Нажмите кнопку **OK**.</span><span class="sxs-lookup"><span data-stu-id="12611-209">Choose **OK**.</span></span>
    
    <span data-ttu-id="12611-210">На этом этапе SharePoint создает HTML-файл и ASPX-файл с таким же именем.</span><span class="sxs-lookup"><span data-stu-id="12611-210">At this point, SharePoint creates an HTML file and an .aspx file that has the same name.</span></span>
    
    <span data-ttu-id="12611-211">В Дизайнере HTML-файл теперь отображается со столбцом **Состояние**, в котором отображается одно из двух состояний:</span><span class="sxs-lookup"><span data-stu-id="12611-211">In Design Manager, your HTML file now appears with a **Status** column that shows one of two statuses:</span></span>
    
  - <span data-ttu-id="12611-212">Ошибки</span><span class="sxs-lookup"><span data-stu-id="12611-212">**Warnings and Errors**</span></span>
    
  
  - <span data-ttu-id="12611-213">**Преобразование выполнено успешно**.</span><span class="sxs-lookup"><span data-stu-id="12611-213">**Conversion successful**</span></span>
    
  
4. <span data-ttu-id="12611-214">С помощью проводника Windows откройте сетевой диск, сопоставленный с коллекцией главных страниц.</span><span class="sxs-lookup"><span data-stu-id="12611-214">Using Windows Explorer, open the mapped network drive to the Master Page Gallery.</span></span>
    
  
5. <span data-ttu-id="12611-p116">Чтобы настроить макет страницы элементов каталога, измените HTML-файл, который находится непосредственно на сервере. Для этого откройте и измените HTML-файл на сопоставленном диске с помощью HTML-редактора. Каждый раз при сохранении HTML-файл все изменения синхронизируются со связанным ASPX-файлом.</span><span class="sxs-lookup"><span data-stu-id="12611-p116">To customize the catalog item page layout, edit the HTML file that resides directly on the server by using an HTML editor to open and edit the HTML file in the mapped drive. Each time that you save the HTML file, any changes are synched to the associated .aspx file.</span></span>
    
  
6. <span data-ttu-id="12611-217">Добавьте в заполнитель контента, содержащего элемент **id="PlaceHolderMain"**, разметку, которую требуется использовать в макете страницы.</span><span class="sxs-lookup"><span data-stu-id="12611-217">Inside the content placeholder that has **id="PlaceHolderMain"**, add the markup that you want to use in the page layout.</span></span>
    
  
7. <span data-ttu-id="12611-218">Удалите все фрагменты, которые не требуются, из макета страницы и переместите оставшиеся фрагменты туда, где необходимо показывать значения свойств.</span><span class="sxs-lookup"><span data-stu-id="12611-218">Delete any snippets that you do not want to use in the page layout, and move the remaining snippets to places in the markup where you want the property values to appear.</span></span>
    
    > <span data-ttu-id="12611-219">**Внимание!** По умолчанию фрагмент кода для зоны веб-частей, который содержит фрагмент кода для повторного использования элементов каталога, добавляется в макет страницы.</span><span class="sxs-lookup"><span data-stu-id="12611-219">**Caution:** By default, a Web Part Zone Snippet that contains a Catalog-Item Reuse Snippet is added to the page layout.</span></span> <span data-ttu-id="12611-220">Этот фрагмент кода включает в себя поставщик данных, возвращающий результаты запроса, которые используются всеми другими фрагментами кода на странице.</span><span class="sxs-lookup"><span data-stu-id="12611-220">This snippet contains the data provider that returns query results that are used by all other snippets on the page.</span></span> <span data-ttu-id="12611-221">Мы рекомендуем оставить этот фрагмент кода для повторного использования элементов каталога в данном фрагменте кода для зоны веб-частей по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="12611-221">We recommend that you keep the Catalog-Item Reuse Snippet in this default Web Part Zone Snippet.</span></span> <span data-ttu-id="12611-222">Можно переместить фрагмент кода для повторного использования элементов каталога за пределы зоны веб-частей, также можно изменить свойство, которое он показывает.</span><span class="sxs-lookup"><span data-stu-id="12611-222">(You can move the Catalog-Item Reuse Snippet outside the Web Part Zone, and you can change the property that it displays.</span></span> <span data-ttu-id="12611-223">Однако необходимо сохранить фрагмент кода для повторного использования элементов каталога в макете страницы. Дополнительные сведения см. разделе [Поля страницы](how-to-customize-page-layouts-for-a-catalog-based-site-in-sharepoint.md#bk_pagefields) далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="12611-223">But, you must keep the Catalog-Item Reuse Snippet in the page layout.) For more information, see  [Page fields](how-to-customize-page-layouts-for-a-catalog-based-site-in-sharepoint.md#bk_pagefields), later in this article.</span></span> 
8. <span data-ttu-id="12611-224">Чтобы изменить и скопировать HTML-код для всех фрагментов, которые необходимо использовать на странице, выполните шаги с 1 по 11 из раздела "Вставка фрагмента из коллекции фрагментов" статьи  [Фрагменты кода дизайнер SharePoint](sharepoint-design-manager-snippets.md).</span><span class="sxs-lookup"><span data-stu-id="12611-224">To configure and copy the HTML snippet for any snippets you want to use in the page, follow step 1 through step 11 in the "Insert a snippet from the Snippet Gallery" section of  [SharePoint Design Manager snippets](sharepoint-design-manager-snippets.md).</span></span>
    
  
9. <span data-ttu-id="12611-225">Внесите необходимые изменения в разметку и сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="12611-225">Make any other required changes to the markup, and then save the file.</span></span>
    
  
10. <span data-ttu-id="12611-226">Выполните шаги с 9 по 11 из раздела "Создание макета страницы" статьи  [Инструкции. Создание макета страницы в SharePoint](how-to-create-a-page-layout-in-sharepoint.md), чтобы проверить состояние файла, просмотреть макет страницы и устранить все ошибки.</span><span class="sxs-lookup"><span data-stu-id="12611-226">Follow step 9 through step 11 in the "Create a page layout" section of  [How to: Create a page layout in SharePoint](how-to-create-a-page-layout-in-sharepoint.md) to check the status of the file, preview the page layout, and fix any errors.</span></span>
    
  

## <a name="understanding-the-markup-in-the-html-catalog-item-page-layout"></a><span data-ttu-id="12611-227">Общие сведения о разметке в макете страницы элементов каталога HTML</span><span class="sxs-lookup"><span data-stu-id="12611-227">Understanding the markup in the HTML catalog item page layout</span></span>
<span data-ttu-id="12611-228"><a name="bk_CatItemMarkup"> </a></span><span class="sxs-lookup"><span data-stu-id="12611-228"></span></span>

<span data-ttu-id="12611-p118">При создании макета страницы создается ASPX-файл, используемый SharePoint, а определенная HTML-разметка добавляется в HTML-версию макета страницы. Макеты страниц элементов каталога содержат компоненты разметки, добавляемые в зависимости от функции публикации в нескольких семействах сайтов и которые уникальны для макетов страниц элементов каталога. Если вы хотите изменить макет страницы элементов каталога HTML в редакторе HTML, вам будет полезно ознакомиться с этой разметкой.</span><span class="sxs-lookup"><span data-stu-id="12611-p118">When you create a page layout, an .aspx file is created that SharePoint uses, and some HTML markup is added to the HTML version of the page layout. Catalog item page layouts have markup components that are added to the page layout based on the Cross-Site Collection Publishing feature, and that are unique to catalog item page layouts. When you edit the HTML catalog item page layout in your HTML editor, it might be helpful to understand some of this markup.</span></span>
  
    
    

### <a name="browser-window-page-title"></a><span data-ttu-id="12611-232">Заголовок страницы в окне браузера</span><span class="sxs-lookup"><span data-stu-id="12611-232">Browser window page title</span></span>

<span data-ttu-id="12611-p119">Компонент, который отображается в заполнителе контента с **id="PlaceHolderPageTitle"**, содержит фрагмент повторного использования элементов каталога, который сообщает SharePoint о необходимости использовать элемент каталога в качестве заголовка страницы в окне браузера вместо стандартного значения поля заголовка страницы. В следующем коде показана разметка для заголовка страницы в окне браузера.</span><span class="sxs-lookup"><span data-stu-id="12611-p119">The component that appears inside the content placeholder with **id="PlaceHolderPageTitle"** contains a Catalog-Item Reuse Snippet that tells SharePoint to use the name of the catalog item as the page title in the browser window, instead of using the standard page title field value. The following code shows the markup for the browser window page title.</span></span>
  
    
    

> <span data-ttu-id="12611-235">**Примечание.** Идентификаторы GUID для **ID** и **__WebPartId** случайным образом создаются SharePoint при добавлении фрагментов кода в макет страницы.</span><span class="sxs-lookup"><span data-stu-id="12611-235">**Note** The GUIDs for **ID** and **__WebPartId** are randomly generated by SharePoint when the snippets are added to the page layout.</span></span>
  
    
    


```HTML

<!--CS: [Title] Start Catalog-Item Reuse Snippet-->
<!--SPM:<cc1:CatalogItemReuseWebPart runat="server" UseServerSideRenderFormat="True" ResultType="" NumberOfItems="1" UseSharedDataProvider="True" OverwriteResultPath="False" ResultsPerPage="1"  SelectedPropertiesJson="[&amp;#34;Title&amp;#34;]" 
Title="$Resources:Microsoft.Office.Server.Search,CBSItem_Title;" Description="$Resources:Microsoft.Office.Server.Search,CBSItem_Description;" 
MissingAssembly="Cannot import this Web Part." ID="g_863912c1_c849_46dc_8781_2920ee2bc83f" __WebPartId="{863912c1-c849-46dc-8781-2920ee2bc83f}">-->
<!--SPM:<RenderFormat>-->
<!--DC:Renders value from search without any additional formatting.-->
<!--SPM:</RenderFormat>-->
<!--SPM:</cc1:CatalogItemReuseWebPart>-->
<!--CE:End Catalog-Item Reuse Snippet-->

```


### <a name="page-fields"></a><span data-ttu-id="12611-236">Поля страницы</span><span class="sxs-lookup"><span data-stu-id="12611-236">Page fields</span></span>
<span data-ttu-id="12611-237"><a name="bk_pagefields"> </a></span><span class="sxs-lookup"><span data-stu-id="12611-237"></span></span>

<span data-ttu-id="12611-p120">Компоненты, которые отображаются в заполнителе контента с **id="PlaceHolderMain"**, содержат фрагменты для полей **Title**, **Page Content** и **Catalog-Item URL**. Вы можете удалить любой из них. В следующем примере кода показана разметки для этих полей страницы.</span><span class="sxs-lookup"><span data-stu-id="12611-p120">The components that appear inside the content placeholder with **id="PlaceHolderMain"** contain snippets for the **Title**, **Page Content**, and **Catalog-Item URL** fields. You may delete any of these snippets from the page layout. The following code shows the markup for these page fields.</span></span>
  
    
    

```HTML

<div>
    <!--CS: Start Page Field: Title Snippet-->
    <!--SPM:<%@Register Tagprefix="PageFieldTextField" Namespace="Microsoft.SharePoint.WebControls" Assembly="Microsoft.SharePoint, 
Version=15.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"%>-->
    <!--SPM:<%@Register Tagprefix="Publishing" Namespace="Microsoft.SharePoint.Publishing.WebControls" Assembly="Microsoft.SharePoint.Publishing, Version=15.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"%>-->
    <!--MS:<Publishing:EditModePanel runat="server" CssClass="edit-mode-panel">-->
        <!--MS:<PageFieldTextField:TextField FieldName="fa564e0f-0c70-4ab9-b863-0177e6ddd247" 
runat="server">-->
        <!--ME:</PageFieldTextField:TextField>-->
    <!--ME:</Publishing:EditModePanel>-->
    <!--CE: End Page Field: Title Snippet-->
</div>
<div>
    <!--CS: Start Page Field: Page Content Snippet-->
    <!--SPM:<%@Register Tagprefix="PageFieldRichHtmlField" Namespace="Microsoft.SharePoint.Publishing.WebControls" Assembly="Microsoft.SharePoint.Publishing, Version=15.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"%>-->
    <!--MS:<PageFieldRichHtmlField:RichHtmlField FieldName="f55c4d88-1f2e-4ad9-aaa8-819af4ee7ee8" runat="server">-->
        <!--PS: Start of READ-ONLY PREVIEW (do not modify)-->
            <div id="ctl02_label" style="display:none">Page Content</div>
            <div id="ctl02__ControlWrapper_RichHtmlField" class="ms-rtestate-field" style="display:inline" aria-labelledby="ctl02_label">
                <div align="left" class="ms-formfieldcontainer">
                    <div class="ms-formfieldlabelcontainer" nowrap="nowrap">
                        <span class="ms-formfieldlabel" nowrap="nowrap">Page Content</span>
                    </div>
                    <div class="ms-formfieldvaluecontainer">
                        <div class="ms-rtestate-field">Page Content field value. Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.</div>
                    </div>
                </div>
            </div>
        <!--PE: End of READ-ONLY PREVIEW-->
    <!--ME:</PageFieldRichHtmlField:RichHtmlField>-->
    <!--CE: End Page Field: Page Content Snippet-->
</div>
<div>
    <!--CS: Start Page Field: Catalog-Item URL Snippet-->
    <!--SPM:<%@Register Tagprefix="PageFieldCatalogSourceFieldControl" Namespace="Microsoft.SharePoint.Publishing.WebControls" Assembly="Microsoft.SharePoint.Publishing, Version=15.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"%>-->
    <!--MS:<PageFieldCatalogSourceFieldControl:CatalogSourceFieldControl FieldName="75772bbf-0c25-4710-b52c-7b78344ad136" runat="server">-->
    <!--PS: Start of READ-ONLY PREVIEW (do not modify)-->
        <div align="left" class="ms-formfieldcontainer">
            <div class="ms-formfieldlabelcontainer" nowrap="nowrap">
                <span class="ms-formfieldlabel" nowrap="nowrap">Catalog-Item URL</span>
            </div>
            <div class="ms-formfieldvaluecontainer">
                <a href="http://www.example.com">Link to sample web site.</a>
            </div>
        </div>
    <!--PE: End of READ-ONLY PREVIEW-->
    <!--ME:</PageFieldCatalogSourceFieldControl:CatalogSourceFieldControl>-->
    <!--CE: End Page Field: Catalog-Item URL Snippet-->
</div>

```

<span data-ttu-id="12611-p121">Если макет страницы элементов каталога был создан автоматически при подключении сайта публикации к каталогу или после выбора удаленного каталога во время создания макета страницы, то в макете также будет содержаться фрагмент зоны веб-части, в который входит фрагмент повторного использования элементов каталога. Он регистрирует поставщик данных для страницы. Фрагмент повторного использования элементов каталога содержит свойство **UseSharedDataProvider** со значением **False**. Фрагмент зоны веб-части можно удалить из макета страницы. Но фрагмент повторного использования элементов каталога должен храниться в разметке макета страницы, чтобы на элементы каталога могли отображаться на странице. При создании страницы, которая использует этот макет, можно настроить веб-часть так, чтобы она была скрыта, когда пользователь просматривает страницу.</span><span class="sxs-lookup"><span data-stu-id="12611-p121">If the catalog item page layout was created automatically when the publishing site was connected to a catalog, or was created by selecting a remote catalog during page layout creation, the page layout also contains a Web Part Zone Snippet that contains a Catalog-Item Reuse Snippet that registers a data provider for the page. The Catalog-Item Reuse Snippet contains a **UseSharedDataProvider** property, which is set to **False**. The Web Part Zone Snippet can be deleted from the page layout. But, the Catalog-Item Reuse Snippet must be kept in the page layout markup for the page to display catalog items. When you create a page that uses this page layout, you can configure the Web Part so that it is hidden when a user views the page.</span></span>
  
    
    

> <span data-ttu-id="12611-246">**Важно!** Если при создании макета страницы элементов каталога выбирается тип контента вместо удаленного каталога, необходимо добавить фрагмент кода для повторного использования элементов каталога в макет страницы.</span><span class="sxs-lookup"><span data-stu-id="12611-246">**Important:** If you create a new catalog item page layout, and you choose a content type instead of a remote catalog, you must include a Catalog-Item Reuse Snippet in the page layout.</span></span> <span data-ttu-id="12611-247">Ниже показан фрагмент кода для повторного использования элементов каталога, который размещен во фрагменте кода зоны веб-частей.</span><span class="sxs-lookup"><span data-stu-id="12611-247">The following code shows the markup for the Catalog-Item Reuse Snippet as it appears inside the Web Part Zone Snippet.</span></span> <span data-ttu-id="12611-248">Замените _ManagedPropertyName_ именем управляемого свойства, которое нужно показать, _ResultSourceID_ — идентификатором GUID источника результатов, а _CatalogURL_ — URL-адресом каталога.</span><span class="sxs-lookup"><span data-stu-id="12611-248">Replace  _ManagedPropertyName_ with the name of the managed property to display, replace _ResultSourceID_ with the GUID of the result source, and replace _CatalogURL_ with the URL of the catalog.</span></span>
  
    
    




```HTML

<div>
    <!--CS: Start Web Part Zone Snippet-->
    <!--SPM:<%@Register Tagprefix="WebPartPages" Namespace="Microsoft.SharePoint.WebPartPages" Assembly="Microsoft.SharePoint, 
Version=15.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"%>-->
    <!--SPM:<%@Register Tagprefix="cc1"  Namespace="Microsoft.Office.Server.Search.WebControls" Assembly="Microsoft.Office.Server.Search, Version=15.0.0.0, Culture=neutral, 
PublicKeyToken=71e9bce111e9429c" %>-->
    <!--MS:<WebPartPages:WebPartZone runat="server" Title="&amp;#60;%$Resources:cms,WebPartZoneTitle_Body%&amp;#62;" AllowPersonalization="False" FrameType="TitleBarOnly" ID="Body" Orientation="Vertical">-->
        <!--MS:<ZoneTemplate>-->
            <!--CS: [ManagedPropertyName] Start Catalog-Item Reuse Snippet-->
            <!--DC:To render the search property using a rendering template, change the "UseServerSideRenderFormat" property to "False".-->
            <!--SPM:<cc1:CatalogItemReuseWebPart runat="server" UseServerSideRenderFormat="True" 
ResultType="" NumberOfItems="1" AddSEOPropertiesFromSearch="True" LogAnalyticsViewEvent="True" UseSharedDataProvider="False" OverwriteResultPath="False" DataProviderJSON="{&amp;#34;QueryTemplate&amp;#34;:&amp;#34;ListItemID:{URLTOKEN.1}&amp;#34;,&amp;#34;SourceID&amp;#34;:&amp;#34; ResultSourceID&amp;#34;,&amp;#34;PropertiesJson&amp;#34;:&amp;#34;{&amp;#39;Scope&amp;#39;:&amp;#39;  CatalogURL&amp;#39;,&amp;#39;Tag&amp;#39;:&amp;#39;{Term}&amp;#39;}&amp;#34;}" ResultsPerPage="1"  SelectedPropertiesJson="[&amp;#34;ManagedPropertyName&amp;#34;]" Title="$Resources:Microsoft.Office.Server.Search,CBSItem_Title;" Description="$Resources:Microsoft.Office.Server.Search,CBSItem_Description;" MissingAssembly="Cannot import this Web Part." ID="g_d63eebe7_207f_4e8c_9566_7381acc80cc7" __WebPartId="{d63eebe7-207f-4e8c-9566-7381acc80cc7}">-->
            <!--SPM:<RenderFormat>-->
            <!--DC:Renders value from search without any additional formatting.-->
            <!--SPM:</RenderFormat>-->
            <!--SPM:</cc1:CatalogItemReuseWebPart>-->
        <!--ME:</ZoneTemplate>-->
    <!--ME:</WebPartPages:WebPartZone>-->
    <!--CE:End Catalog-Item Reuse Snippet-->
</div>

```

<span data-ttu-id="12611-p123">Если макет страницы элементов каталога был создан автоматически при подключении сайта публикации к каталогу или после выбора удаленного каталога во время создания макета страницы, остальная часть страницы содержит фрагменты повторного использования элементов каталога, соответствующие управляемым свойствам из каталога на сайте разработки. Эти управляемые свойства показывают сведения об определенном элементе каталога, который отображается с помощью макета страницы элементов каталога. Фрагменты повторного использования элементов каталога находятся за пределами зоны веб-частей и отображаются непосредственно на странице при выборе элемента на странице категорий. В таблице 2 перечислены управляемые свойства, которые автоматически добавляются в макет страницы элементов каталога.</span><span class="sxs-lookup"><span data-stu-id="12611-p123">If the catalog item page layout was created automatically when the publishing site was connected to a catalog, or was created by selecting a remote catalog during page layout creation, the rest of the page contains Catalog-Item Reuse Snippets that correspond to managed properties from the catalog on the authoring site. These managed properties display the details for the specific catalog item that is displayed by using the catalog item page layout. These Catalog-Item Reuse Snippets appear outside the Web Part zone, and are rendered directly on the page when an item is chosen on a category page. Table 2 lists the managed properties that are automatically included in the catalog item page layout.</span></span>
  
    
    

> <span data-ttu-id="12611-253">**Примечание.** Некоторые управляемые свойства добавляются, только если каталог находится в библиотеке страниц.</span><span class="sxs-lookup"><span data-stu-id="12611-253">**Note:** Some managed properties are included only if the catalog is a Pages library.</span></span> <span data-ttu-id="12611-254">В столбце **Используется** таблицы 2 показано, какие управляемые свойства используются и для библиотеки страниц, и для списка, а какие — только для библиотеки страниц.</span><span class="sxs-lookup"><span data-stu-id="12611-254">Some managed properties are included only if the catalog is a Pages library. The **Used by** column in Table 2 indicates which managed properties are used by both a Pages library and a list, and which from a Pages library only.</span></span>
  
    
    


<span data-ttu-id="12611-255">**Таблица 2. Управляемые свойства фрагментов кода для повторного использования элементов каталога по умолчанию**</span><span class="sxs-lookup"><span data-stu-id="12611-255">**Table 2. Default managed properties Catalog-Item Reuse Snippets**</span></span>


|<span data-ttu-id="12611-256">**Управляемое свойство**</span><span class="sxs-lookup"><span data-stu-id="12611-256">**Managed property**</span></span>|<span data-ttu-id="12611-257">**Описание**</span><span class="sxs-lookup"><span data-stu-id="12611-257">**Description**</span></span>|<span data-ttu-id="12611-258">**Используется**</span><span class="sxs-lookup"><span data-stu-id="12611-258">**Used by**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="12611-259">**AuthorOWSUSER**</span><span class="sxs-lookup"><span data-stu-id="12611-259">**AuthorOWSUSER**</span></span> <br/> |<span data-ttu-id="12611-260">Имя пользователя, создавшего страницу.</span><span class="sxs-lookup"><span data-stu-id="12611-260">The name of the user who created the page.</span></span>  <br/> |<span data-ttu-id="12611-261">Только библиотекой страниц</span><span class="sxs-lookup"><span data-stu-id="12611-261">Pages library only</span></span>  <br/> |
|<span data-ttu-id="12611-262">**CreatedOWSDATE**</span><span class="sxs-lookup"><span data-stu-id="12611-262">**CreatedOWSDATE**</span></span> <br/> |<span data-ttu-id="12611-263">Дата создания страницы или элемента списка.</span><span class="sxs-lookup"><span data-stu-id="12611-263">The date the page or list item was created.</span></span>  <br/> |<span data-ttu-id="12611-264">Библиотекой страниц и списком</span><span class="sxs-lookup"><span data-stu-id="12611-264">Pages library and list</span></span>  <br/> |
|<span data-ttu-id="12611-265">**EditorOWSUSER**</span><span class="sxs-lookup"><span data-stu-id="12611-265">**EditorOWSUSER**</span></span> <br/> |<span data-ttu-id="12611-266">Имя пользователя, который последним изменил страницу или элемент списка.</span><span class="sxs-lookup"><span data-stu-id="12611-266">The name of the user who last changed the page or list item.</span></span>  <br/> |<span data-ttu-id="12611-267">Библиотекой страниц и списком</span><span class="sxs-lookup"><span data-stu-id="12611-267">Pages library and list</span></span>  <br/> |
|<span data-ttu-id="12611-268">**ListItemID**</span><span class="sxs-lookup"><span data-stu-id="12611-268">**listItemId**</span></span> <br/> |<span data-ttu-id="12611-269">Идентификатор страницы или элемента списка.</span><span class="sxs-lookup"><span data-stu-id="12611-269">The ID for the page or list item.</span></span>  <br/> |<span data-ttu-id="12611-270">Библиотекой страниц и списком</span><span class="sxs-lookup"><span data-stu-id="12611-270">Pages library and list</span></span>  <br/> |
|<span data-ttu-id="12611-271">**ModifiedOWSDATE**</span><span class="sxs-lookup"><span data-stu-id="12611-271">**ModifiedOWSDATE**</span></span> <br/> |<span data-ttu-id="12611-272">Дата последнего изменения страницы или элемента списка.</span><span class="sxs-lookup"><span data-stu-id="12611-272">The date the page or list item was last changed.</span></span>  <br/> |<span data-ttu-id="12611-273">Библиотекой страниц и списком</span><span class="sxs-lookup"><span data-stu-id="12611-273">Pages library and list</span></span>  <br/> |
|<span data-ttu-id="12611-274">**PublishingContactOWSUSER**</span><span class="sxs-lookup"><span data-stu-id="12611-274">**PublishingContactOWSUSER**</span></span> <br/> |<span data-ttu-id="12611-p125">Контакт — это столбец сайта, создаваемый функцией публикации. Он используется в типе контента страницы как пользователь или группа, представляющая контактное лицо для страницы.</span><span class="sxs-lookup"><span data-stu-id="12611-p125">Contact is a site column created by the Publishing feature. It is used on the Page Content Type as the person or group who is the contact person for the page.</span></span>  <br/> |<span data-ttu-id="12611-277">Только библиотекой страниц</span><span class="sxs-lookup"><span data-stu-id="12611-277">Pages library only</span></span>  <br/> |
|<span data-ttu-id="12611-278">**PublishingIsFurlPageOWSBOOL**</span><span class="sxs-lookup"><span data-stu-id="12611-278">**PublishingIsFurlPageOWSBOOL**</span></span> <br/> |<span data-ttu-id="12611-279">Логическое значение, указывающее, связана ли страница с понятным URL-адресом.</span><span class="sxs-lookup"><span data-stu-id="12611-279">A Boolean value that indicates whether the page is associated with a friendly URL.</span></span>  <br/> |<span data-ttu-id="12611-280">Только библиотекой страниц</span><span class="sxs-lookup"><span data-stu-id="12611-280">Pages library only</span></span>  <br/> |
|<span data-ttu-id="12611-281">**PublishingPageContentOWSHTML**</span><span class="sxs-lookup"><span data-stu-id="12611-281">**PublishingPageContentOWSHTML**</span></span> <br/> |<span data-ttu-id="12611-282">HTML-контент страницы.</span><span class="sxs-lookup"><span data-stu-id="12611-282">The HTML content of the page.</span></span>  <br/> |<span data-ttu-id="12611-283">Только библиотекой страниц</span><span class="sxs-lookup"><span data-stu-id="12611-283">Pages library only</span></span>  <br/> |
|<span data-ttu-id="12611-284">**PublishingPageLayoutOWSURLH**</span><span class="sxs-lookup"><span data-stu-id="12611-284">**PublishingPageLayoutOWSURLH**</span></span> <br/> |<span data-ttu-id="12611-285">URL-адрес макета страницы, который использовался для создания страницы.</span><span class="sxs-lookup"><span data-stu-id="12611-285">The URL to the page layout that was used to create the page.</span></span>  <br/> |<span data-ttu-id="12611-286">Только библиотекой страниц</span><span class="sxs-lookup"><span data-stu-id="12611-286">Pages library only</span></span>  <br/> |
|<span data-ttu-id="12611-287">**Title**</span><span class="sxs-lookup"><span data-stu-id="12611-287">**Title**</span></span> <br/> |<span data-ttu-id="12611-288">Заголовок страницы или элемента списка.</span><span class="sxs-lookup"><span data-stu-id="12611-288">The title of the page or list item.</span></span>  <br/> |<span data-ttu-id="12611-289">Библиотека страниц и список</span><span class="sxs-lookup"><span data-stu-id="12611-289">Pages library and list</span></span>  <br/> |
   
<span data-ttu-id="12611-290">Управляемые свойства для пользовательских столбцов, добавляемых в библиотеку страниц или список, также включаются во фрагменты кода для повторного использования элементов каталога.</span><span class="sxs-lookup"><span data-stu-id="12611-290">The managed properties for custom columns that you add to the Pages library or list are also included in Catalog-Item Reuse Snippets.</span></span> <span data-ttu-id="12611-291">Имя управляемого свойства зависит от типа столбца сайта, который используется при создании столбца сайта.</span><span class="sxs-lookup"><span data-stu-id="12611-291">The managed property name will vary, based on the site column type that you use when you create the site column.</span></span> <span data-ttu-id="12611-292">Дополнительные сведения см. в статьях [Автоматически созданные управляемые свойства в SharePoint](http://technet.microsoft.com/en-us/library/jj613136.aspx) и [Обзор схемы поиска в SharePoint](http://technet.microsoft.com/en-us/library/jj219669.aspx).</span><span class="sxs-lookup"><span data-stu-id="12611-292">For more information, see  [Automatically created managed properties in SharePoint](http://technet.microsoft.com/en-us/library/jj613136.aspx), and  [Overview of the search schema in SharePoint](http://technet.microsoft.com/en-us/library/jj219669.aspx).</span></span>
  
    
    

> <span data-ttu-id="12611-293">**Важно!** Столбец сайта **Page Image** в библиотеке страниц сопоставляется с управляемым свойством **PublishingImage**.</span><span class="sxs-lookup"><span data-stu-id="12611-293">**Important:** The **Page Image** site column in a Pages library is mapped to the **PublishingImage** managed property.</span></span> <span data-ttu-id="12611-294">Но управляемое свойство **PublishingImage** не добавляется автоматически в макет страницы элементов категорий.</span><span class="sxs-lookup"><span data-stu-id="12611-294">But, the **PublishingImage** managed property is not automatically included in the category-item page layout.</span></span> <span data-ttu-id="12611-295">Чтобы добавить изображение в макет страницы, необходимо включить фрагмент кода для повторного использования элементов каталога для управляемого свойства **PublishingImage**.</span><span class="sxs-lookup"><span data-stu-id="12611-295">To include the image in your page layout, you must add a Catalog-Item Reuse Snippet for the **PublishingImage** managed property.</span></span> <span data-ttu-id="12611-296">Указанный ниже HTML-код позволит добавить фрагмент кода для повторного использования элементов каталога, чтобы обеспечить отображение значения управляемого свойства **PublishingImage** в макете страницы.</span><span class="sxs-lookup"><span data-stu-id="12611-296">Use the following HTML to add a Catalog-Item Reuse Snippet to display the value of the **PublishingImage** managed property in your page layout.</span></span> <span data-ttu-id="12611-297">Замените _UniqueID_ идентификатором GUID, который является уникальным для каждого экземпляра фрагмента кода.</span><span class="sxs-lookup"><span data-stu-id="12611-297">Replace _UniqueID_ with a GUID that is unique to each instance of the snippet.</span></span>
  
    
    




```HTML

<div>
<!--CS: [PublishingImage] Start Catalog-Item Reuse Snippet-->
<!--SPM:<cc1:CatalogItemReuseWebPart runat="server" UseServerSideRenderFormat="True" 
ResultType="" NumberOfItems="1" UseSharedDataProvider="True" OverwriteResultPath="False" 
ResultsPerPage="1"  SelectedPropertiesJson="[&amp;#34;PublishingImage&amp;#34;]" 
Title="$Resources:Microsoft.Office.Server.Search,CBSItem_Title;" 
Description="$Resources:Microsoft.Office.Server.Search,CBSItem_Description;" 
MissingAssembly="Cannot import this Web Part." ID="g_UniqueID" __WebPartId="{UniqueID}">-->
<!--SPM:<RenderFormat>-->
<!--SPM:<Format Type="HTML"> -->
<!--SPM:<Picture>-->True<!--SPM:</Picture>-->
<!--SPM:</Format> -->
<!--SPM:</RenderFormat>-->
<!--SPM:</cc1:CatalogItemReuseWebPart>-->
<!--CE:End Catalog-Item Reuse Snippet-->
</div>

```

<span data-ttu-id="12611-p128">Если вы создаете макет страницы элементов каталога с помощью Дизайнера и выбираете тип контента вместо удаленного каталога, вы можете добавить фрагменты повторного использования элементов каталога на страницу с помощью коллекции фрагментов. В следующем коде показана разметка фрагментов повторного использования для управляемых свойств **Title**, **PublishingPageContentOWSHTML**, **CreatedOWSDATE** и **owstaxIdPageCategory**.</span><span class="sxs-lookup"><span data-stu-id="12611-p128">If you create a new catalog item page layout by using Design Manager, and you choose a content type instead of a remote catalog, you can add Catalog-Item Reuse Snippets to the page by using the Snippet Gallery. The following code shows the markup for the Catalog-Item Reuse Snippets for the **Title**, **PublishingPageContentOWSHTML**, **CreatedOWSDATE**, and **owstaxIdPageCategory** managed properties.</span></span>
  
    
    

> <span data-ttu-id="12611-300">**Примечание.** Идентификаторы GUID для **ID** и **__WebPartId** случайным образом создаются SharePoint при добавлении фрагментов кода в макет страницы.</span><span class="sxs-lookup"><span data-stu-id="12611-300">**Note** The GUIDs for **ID** and **__WebPartId** are randomly generated by SharePoint when the snippets are added to the page layout.</span></span>
  
    
    




```HTML

<div>
    <!--CS: [Title] Start Catalog-Item Reuse Snippet-->
    <!--SPM:<cc1:CatalogItemReuseWebPart runat="server" UseServerSideRenderFormat="True" 
ResultType="" NumberOfItems="1" UseSharedDataProvider="True" OverwriteResultPath="False" 
ResultsPerPage="1"  SelectedPropertiesJson="[&amp;#34;Title&amp;#34;]" 
Title="$Resources:Microsoft.Office.Server.Search,CBSItem_Title;" 
Description="$Resources:Microsoft.Office.Server.Search,CBSItem_Description;" 
MissingAssembly="Cannot import this Web Part." ID="g_0dc23bb8_8d34_4f9f_8085_5a6ac286cb9e" 
__WebPartId="{0dc23bb8-8d34-4f9f-8085-5a6ac286cb9e}">-->
    <!--SPM:<RenderFormat>-->
    <!--DC:Renders value from search without any additional formatting.-->
    <!--SPM:</RenderFormat>-->
    <!--SPM:</cc1:CatalogItemReuseWebPart>-->
    <!--CE:End Catalog-Item Reuse Snippet-->
</div>
<div>
    <!--CS: [PublishingPageContentOWSHTML] Start Catalog-Item Reuse Snippet-->
    <!--SPM:<cc1:CatalogItemReuseWebPart runat="server" UseServerSideRenderFormat="True" 
ResultType="" NumberOfItems="1" UseSharedDataProvider="True" OverwriteResultPath="False" 
ResultsPerPage="1"  SelectedPropertiesJson="[&amp;#34;PublishingPageContentOWSHTML&amp;#34;]" 
Title="$Resources:Microsoft.Office.Server.Search,CBSItem_Title;" 
Description="$Resources:Microsoft.Office.Server.Search,CBSItem_Description;" 
MissingAssembly="Cannot import this Web Part." ID="g_25253a49_a9a6_4277_bf9d_416961024cee" 
__WebPartId="{25253a49-a9a6-4277-bf9d-416961024cee}">-->
    <!--SPM:<RenderFormat>-->
    <!--DC:Renders value from search without any additional formatting.-->
    <!--SPM:</RenderFormat>-->
    <!--SPM:</cc1:CatalogItemReuseWebPart>-->
    <!--CE:End Catalog-Item Reuse Snippet-->
</div>
<div>
    <!--CS: [CreatedOWSDATE] Start Catalog-Item Reuse Snippet-->
    <!--SPM:<cc1:CatalogItemReuseWebPart runat="server" UseServerSideRenderFormat="True" 
ResultType="" NumberOfItems="1" UseSharedDataProvider="True" OverwriteResultPath="False" 
ResultsPerPage="1"  SelectedPropertiesJson="[&amp;#34;CreatedOWSDATE&amp;#34;]" 
Title="$Resources:Microsoft.Office.Server.Search,CBSItem_Title;" 
Description="$Resources:Microsoft.Office.Server.Search,CBSItem_Description;" 
MissingAssembly="Cannot import this Web Part." 
ID="g_4e1f180b_12f8_4e50_84d7_c72b0ee3793f" 
__WebPartId="{4e1f180b-12f8-4e50-84d7-c72b0ee3793f}">-->
    <!--SPM:<RenderFormat>-->
    <!--SPM:<Format Type="DateTime"> -->
    <!--DC:To render Date and Time, change this value to False.-->
    <!--SPM:<DateOnly>-->True<!--SPM:</DateOnly>-->
    <!--SPM:</Format> -->
    <!--SPM:</RenderFormat>-->
    <!--SPM:</cc1:CatalogItemReuseWebPart>-->
    <!--CE:End Catalog-Item Reuse Snippet-->
</div>
<div>
    <!--CS: [owstaxIdPageCategory] Start Catalog-Item Reuse Snippet-->
    <!--SPM:<cc1:CatalogItemReuseWebPart runat="server" UseServerSideRenderFormat="True" 
ResultType="" NumberOfItems="1" UseSharedDataProvider="True" OverwriteResultPath="False" 
ResultsPerPage="1"  SelectedPropertiesJson="[&amp;#34;owstaxIdPageCategory&amp;#34;]" 
Title="$Resources:Microsoft.Office.Server.Search,CBSItem_Title;" 
Description="$Resources:Microsoft.Office.Server.Search,CBSItem_Description;" 
MissingAssembly="Cannot import this Web Part." ID="g_22e39e9d_1b25_42c7_bf2a_7ebca37616d4" 
__WebPartId="{22e39e9d-1b25-42c7-bf2a-7ebca37616d4}">-->
    <!--SPM:<RenderFormat>-->
    <!--DC:Renders value from search without any additional formatting.-->
    <!--SPM:</RenderFormat>-->
    <!--SPM:</cc1:CatalogItemReuseWebPart>-->
    <!--CE:End Catalog-Item Reuse Snippet-->
</div>

```


## <a name="additional-resources"></a><span data-ttu-id="12611-301">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="12611-301">Additional resources</span></span>
<span data-ttu-id="12611-302"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="12611-302"></span></span>


-  [<span data-ttu-id="12611-303">Разработка макета сайта в SharePoint</span><span class="sxs-lookup"><span data-stu-id="12611-303">Develop the site design in SharePoint</span></span>](develop-the-site-design-in-sharepoint.md)
    
  
-  [<span data-ttu-id="12611-304">Обзор Дизайнера в SharePoint</span><span class="sxs-lookup"><span data-stu-id="12611-304">Overview of Design Manager in SharePoint</span></span>](overview-of-design-manager-in-sharepoint.md)
    
  
-  [<span data-ttu-id="12611-305">Обзор модели страниц в SharePoint</span><span class="sxs-lookup"><span data-stu-id="12611-305">Overview of the SharePoint page model</span></span>](overview-of-the-sharepoint-page-model.md)
    
  
-  [<span data-ttu-id="12611-306">Инструкции. Создание макета страницы в SharePoint</span><span class="sxs-lookup"><span data-stu-id="12611-306">How to: Create a page layout in SharePoint</span></span>](how-to-create-a-page-layout-in-sharepoint.md)
    
  
-  [<span data-ttu-id="12611-307">Шаблоны отображения Дизайнера SharePoint</span><span class="sxs-lookup"><span data-stu-id="12611-307">SharePoint Design Manager display templates</span></span>](sharepoint-design-manager-display-templates.md)
    
  

