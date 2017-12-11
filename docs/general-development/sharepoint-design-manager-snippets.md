---
title: "Фрагменты кода дизайнер SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 68caef4c-5941-4a88-b34b-f88122801cef
ms.openlocfilehash: 2c670d8fb7cd6ec3f293a3e5da9b75380005f598
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="sharepoint-design-manager-snippets"></a><span data-ttu-id="08618-102">Фрагменты кода дизайнер SharePoint</span><span class="sxs-lookup"><span data-stu-id="08618-102">SharePoint Design Manager snippets</span></span>
<span data-ttu-id="08618-p101">Фрагмент является представлением HTML компонентов SharePoint или элемента управления, например панели навигации или веб-части. С помощью коллекция фрагментов кода в диспетчере оформления, можно быстро добавить функциональные возможности SharePoint для главной страницы HTML или макет страницы.</span><span class="sxs-lookup"><span data-stu-id="08618-p101">A snippet is an HTML representation of a SharePoint component or control such as a navigation bar or a Web Part. By using the Snippet Gallery in Design Manager, you can quickly add SharePoint functionality to your HTML master page or page layout.</span></span>
## <a name="introduction-to-snippets-and-the-snippet-gallery"></a><span data-ttu-id="08618-105">Общие сведения о фрагменты кода и коллекция фрагментов кода</span><span class="sxs-lookup"><span data-stu-id="08618-105">Introduction to snippets and the Snippet Gallery</span></span>
<span data-ttu-id="08618-106"><a name="Introduction"> </a></span><span class="sxs-lookup"><span data-stu-id="08618-106"></span></span>

<span data-ttu-id="08618-p102">После преобразования главную страницу или создание макета страницы, у вас есть HTML-версии этой страницы. С помощью коллекция фрагментов кода можно быстро добавить определенных функций SharePoint, например поиска или навигации или каналов устройств для HTML-файла, связанного с главной странице или макету страницы. Коллекция фрагментов кода представляет собой страницу в диспетчере оформления которых можно:</span><span class="sxs-lookup"><span data-stu-id="08618-p102">After you convert a master page or create a page layout, you have an HTML version of that page. With the Snippet Gallery, you can quickly add specific SharePoint functionality, such as search or navigation or device channel panels, to the HTML file associated with your master page or page layout. The Snippet Gallery is a page in Design Manager where you can:</span></span>
  
    
    

- <span data-ttu-id="08618-110">Выберите компонент SharePoint от тех, которые доступны на ленте.</span><span class="sxs-lookup"><span data-stu-id="08618-110">Choose a SharePoint component from those available on the ribbon.</span></span>
    
  
- <span data-ttu-id="08618-111">Настройка свойств для этого компонента.</span><span class="sxs-lookup"><span data-stu-id="08618-111">Configure the properties for that component.</span></span>
    
  
- <span data-ttu-id="08618-112">Предварительный просмотр внешнего вида в браузере.</span><span class="sxs-lookup"><span data-stu-id="08618-112">Preview its appearance in the browser.</span></span>
    
  
- <span data-ttu-id="08618-113">Скопируйте фрагмент кода HTML в буфер обмена, чтобы можно было вставить фрагмент в расположении в HTML-файл.</span><span class="sxs-lookup"><span data-stu-id="08618-113">Copy the HTML code snippet to the Clipboard so that you can paste the snippet at the location you want in the HTML file.</span></span>
    
  
<span data-ttu-id="08618-p103">Коллекция фрагментов кода отображает различные параметры на ленте, в зависимости от того, редактировании главной странице или макету страницы  например, элементы управления навигацией, отображаются только для главных страниц и зоны веб-частей и элементов управления полей страницы, отображаются только для макетов страниц. Кроме того при изменении макета страницы полей страниц, доступных зависят от типа контента макета страницы, который требуется изменить.</span><span class="sxs-lookup"><span data-stu-id="08618-p103">The Snippet Gallery displays different options on the ribbon, depending on whether you're editing a master page or page layout—for example, navigation controls are displayed only for master pages, and Web Part zones and page field controls are displayed only for page layouts. Also, when you are editing a page layout, the page fields that are available depend on the content type of the page layout that you're editing.</span></span>
  
    
    
<span data-ttu-id="08618-p104">После вставки фрагмента кода в HTML-файл, вы получаете разработки preview из HTML, представленные в примере. Также можно использовать preview на сервере в диспетчере оформления чтобы увидеть, как будет выглядеть элемент управления действующего сайта. Предварительный просмотр разработки может включать статические демонстрационных данных, но preview на сервере с помощью динамических данных, если он доступен. Например элемент управления навигации, которая отображает ссылки для перехода из набора терминов динамически отображать эти термины в предварительной версии на сервере, но предварительного просмотра во время разработки будет статический условия во время создания фрагмента. Динамических данных недоступен в предварительной версии на сервере для некоторых фрагменты кода, тем не менее, включая количество веб-частей. В этом случае preview на сервере может сказать **Предварительной версии недоступно**.</span><span class="sxs-lookup"><span data-stu-id="08618-p104">After you paste a snippet into your HTML file, you get a design-time preview from the HTML provided in the snippet. You can also use the server-side preview in Design Manager to see how the control will appear on the live site. The design-time preview may include static sample data, but the server-side preview uses live data, if available. For example, a navigation control that draws navigation links from a term set will display those terms dynamically in the server-side preview, but the design-time preview will have a static snapshot of the terms at the time you created the snippet. Live data is not available in the server-side preview for some snippets, however, including many Web Parts. In this case, the server-side preview may say **Preview Not Available**.</span></span>
  
> [!NOTE]
> <span data-ttu-id="08618-p105">[!Примечание] Содержит фрагмент HTML-разметку, можно просмотреть во время разработки в редакторе HTML, но HTML-разметку содержатся в «запуск предварительного просмотра» и «предварительный просмотр плана» комментарии нельзя изменять так, как оно затрагивает только предварительного просмотра во время разработки, не как SharePoint воспроизводится в конечном счете фрагмента. Вместо этого стиля фрагмент кода, обычно необходимо определить и переопределения стилей SharePoint по умолчанию, которые применяются к фрагмента.</span><span class="sxs-lookup"><span data-stu-id="08618-p105">A snippet contains HTML markup that gives you a design-time preview in your HTML editor, but the HTML markup contained in "start preview" and "end preview" comments should not be edited because it affects only the design-time preview, not how SharePoint ultimately renders that snippet. Instead, to style your snippet, you typically have to identify and override the default SharePoint styles that are applied to the snippet.</span></span> 
  
    
    


  
    
    

## <a name="insert-a-snippet-from-the-snippet-gallery"></a><span data-ttu-id="08618-124">Вставить фрагмент кода из коллекции фрагмента</span><span class="sxs-lookup"><span data-stu-id="08618-124">Insert a snippet from the Snippet Gallery</span></span>
<span data-ttu-id="08618-125"><a name="InsertSnippet"> </a></span><span class="sxs-lookup"><span data-stu-id="08618-125"></span></span>

<span data-ttu-id="08618-p106">Коллекция фрагментов кода отображает различные параметры в зависимости от файла, который требуется изменить. Например другой страницы макетов иметь различные наборы поля страниц, доступных для них. По этой причине для перехода к коллекция фрагментов кода, сначала нужно выбрать главную страницу или макет страницы для редактирования.</span><span class="sxs-lookup"><span data-stu-id="08618-p106">The Snippet Gallery displays different options depending on the file that you're editing. For example, different page layouts have different sets of page fields available to them. For this reason, to navigate to the Snippet Gallery, you must first select a master page or page layout to edit.</span></span>
  
    
    

### <a name="to-insert-a-snippet"></a><span data-ttu-id="08618-129">Чтобы вставить фрагмент</span><span class="sxs-lookup"><span data-stu-id="08618-129">To insert a snippet</span></span>


1. <span data-ttu-id="08618-130">Откройте свой сайт публикации.</span><span class="sxs-lookup"><span data-stu-id="08618-130">Browse to your publishing site.</span></span>
    
  
2. <span data-ttu-id="08618-131">Нажмите значок шестеренки "Параметры" в правом верхнем углу страницы, а затем выберите **Дизайнер**.</span><span class="sxs-lookup"><span data-stu-id="08618-131">In the upper-right corner of the page, choose the Settings gear, and then choose **Design Manager**.</span></span>
    
  
3. <span data-ttu-id="08618-132">В диспетчере оформления на левой панели навигации слева выберите **Изменить главную страницу** или **Изменение макетов страниц**, в зависимости от того, какой тип файла требуется изменить.</span><span class="sxs-lookup"><span data-stu-id="08618-132">In Design Manager, in the left navigation pane, choose **Edit Master Pages** or **Edit Page Layouts**, depending on what type of file you're editing.</span></span>
    
  
4. <span data-ttu-id="08618-133">Выберите имя главной страницы или макет страницы, который вы хотите добавить фрагменты кода для.</span><span class="sxs-lookup"><span data-stu-id="08618-133">Select the name of the master page or page layout that you want to add snippets to.</span></span>
    
  
5. <span data-ttu-id="08618-134">Чтобы открыть коллекцию фрагментов, выберите **Фрагменты** в правом верхнем углу страницы предварительного просмотра на стороне сервера.</span><span class="sxs-lookup"><span data-stu-id="08618-134">To open the Snippet Gallery, choose **Snippets** in the upper-right corner of the server-side preview.</span></span>
    
  
6. <span data-ttu-id="08618-135">На ленте перейдите на вкладку **Конструктор** выберите фрагмент, который нужно добавить на страницу.</span><span class="sxs-lookup"><span data-stu-id="08618-135">On the ribbon, on the **Design** tab, choose the snippet that you want to add to your page.</span></span>
    
    <span data-ttu-id="08618-136">При выборе фрагмент коллекция фрагментов кода обновляются, чтобы на странице отображается предварительный просмотр фрагмента свойства, доступные для фрагмента и фрагмент кода HTML, который можно скопировать в главной страницы HTML или макет страницы.</span><span class="sxs-lookup"><span data-stu-id="08618-136">When you select a snippet, the Snippet Gallery refreshes so that the page shows you a preview of that snippet, the properties available for that snippet, and the HTML code snippet that you can copy into your HTML master page or page layout.</span></span>
    
  
7. <span data-ttu-id="08618-137">В разделе **Об этом компоненте** в правой части коллекции фрагментов щелкните или выберите заголовок раздела, чтобы развернуть или свернуть группу свойств, а затем настройте все нужные настраиваемые параметры.</span><span class="sxs-lookup"><span data-stu-id="08618-137">On the right side of the Snippet Gallery, under **About this Component**, click or select section headers to expand or collapse groups of properties, and then configure any custom settings that you want.</span></span>
    
    <span data-ttu-id="08618-p107">В верхнем разделе с именем важные отображаются свойства, которые являются наиболее важные для основных целей фрагмента. Далее представлены ключевые свойства, которые необходимо изучить при использовании фрагмент.</span><span class="sxs-lookup"><span data-stu-id="08618-p107">The properties that are most important for the core purpose of the snippet appear in the top section named Important. These are the key properties that you have to understand when using a snippet.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="08618-140">[!Примечание] Если сетка свойств заголовка, который заканчивается на AjaxDelta, так как они применяются к элементам управления, связанные с минимальной загрузки стратегической, которое отключено главные страницы и макеты страниц, созданные через дизайнер следует игнорировать этих свойств.</span><span class="sxs-lookup"><span data-stu-id="08618-140">If the property grid has a header that ends with AjaxDelta, you should ignore those properties because they apply to the controls related to the Minimal Download Strategy, which is disabled for master pages and page layouts created through Design Manager.</span></span> 

8. <span data-ttu-id="08618-p108">После настройки всех свойств выберите **обновление**. Обновляет Предварительный просмотр и фрагмент HTML в левой части страницы, чтобы разметка отражает пользовательских параметров. Всегда можно **сбросить** для возврата всех свойств к значениям по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="08618-p108">After you configure any properties, choose **Update**. This updates both the preview and the HTML snippet on the left side of the page, so that the markup reflects your custom settings. You can always choose **Reset** to return all properties to their default settings.</span></span>
    
  
9. <span data-ttu-id="08618-144">В разделе **Фрагмент HTML** в левой части коллекции фрагментов выберите команду **Копировать в буфер обмена**.</span><span class="sxs-lookup"><span data-stu-id="08618-144">On the left side of the Snippet Gallery, under **HTML Snippet**, choose **Copy to Clipboard**.</span></span>
    
  
10. <span data-ttu-id="08618-145">В редакторе HTML откройте сопоставленный сетевой диск на своем компьютере, а затем откройте HTML-файл для эталонной страницы или макета, к которым добавляется фрагмент.</span><span class="sxs-lookup"><span data-stu-id="08618-145">In your HTML editor, open the mapped network drive on your computer, and then open the HTML file for the master page or page layout that you're adding the snippet to.</span></span>
    
  
11. <span data-ttu-id="08618-146">Вставьте фрагмент в том месте HTML-файла, где должна отображаться разметка.</span><span class="sxs-lookup"><span data-stu-id="08618-146">In the HTML file, paste the snippet where you want the markup to appear.</span></span>
    
    <span data-ttu-id="08618-p109">Каждый фрагмент содержит HTML-код, который предоставляет visual предварительной версии компонента и образец данных. Не следует изменять этот HTML-код для предварительного просмотра только для чтения внутри тегов **<!--PS>** и **<!--PE>**, поскольку эта разметка влияет на только во время разработки preview фрагмента, не фрагмента отображения действующего сайта.</span><span class="sxs-lookup"><span data-stu-id="08618-p109">Each snippet contains HTML that provides a visual preview of the component and sample data. You shouldn't modify this HTML for the read-only preview inside the **<!--PS>** and **<!--PE>** tags because this markup affects only the design-time preview of the snippet, not how the snippet will appear on the live site.</span></span>
    
  
12. <span data-ttu-id="08618-149">Для просмотра на сервере фрагмент, сохраните файл HTML-код для синхронизации изменений в файле связанного ASP.NET и обновите на сервере предварительного просмотра в диспетчере оформления.</span><span class="sxs-lookup"><span data-stu-id="08618-149">To see the server-side preview of the snippet, save the HTML file to sync the changes to the associated ASP.NET file, and then refresh the server-side preview in Design Manager.</span></span>
    
    <span data-ttu-id="08618-150">В отличие от предварительного просмотра во время разработки предварительного просмотра на сервере показан элемент управления, как отобразить с помощью SharePoint.</span><span class="sxs-lookup"><span data-stu-id="08618-150">Unlike the design-time preview, the server-side preview shows the control as rendered by SharePoint.</span></span>
    
  

## <a name="understand-the-markup-in-an-html-snippet"></a><span data-ttu-id="08618-151">Понимание разметки в фрагмента кода HTML</span><span class="sxs-lookup"><span data-stu-id="08618-151">Understand the markup in an HTML snippet</span></span>
<span data-ttu-id="08618-152"><a name="UnderstandMarkup"> </a></span><span class="sxs-lookup"><span data-stu-id="08618-152"></span></span>

<span data-ttu-id="08618-153">Он содержит четыре основных раздела:</span><span class="sxs-lookup"><span data-stu-id="08618-153">A snippet contains four basic sections:</span></span>
  
    
    

- <span data-ttu-id="08618-154">**Заголовок** с начала теги **<div>** и **<!--CS>** (за исключением пользовательских ASP.NET фрагменты кода, которые не помещаются в тег **<div>** )</span><span class="sxs-lookup"><span data-stu-id="08618-154">**Header** with starting **<div>** and **<!--CS>** tags (except custom ASP.NET snippets, which are not wrapped in a **<div>** tag)</span></span>
    
  
- <span data-ttu-id="08618-155">**Разметка SharePoint**, где фрагменты заключены в **<!--MS>** начала и **<!--ME>** закрывающие теги</span><span class="sxs-lookup"><span data-stu-id="08618-155">**SharePoint markup** where snippets are enclosed in **<!--MS>** start and **<!--ME>** end tags</span></span>
    
  
- <span data-ttu-id="08618-156">**Предварительный просмотр HTML-код** внутри **<!--PS>** start и **<!--PE>** закрывающие теги</span><span class="sxs-lookup"><span data-stu-id="08618-156">**HTML preview** enclosed in **<!--PS>** start and **<!--PE>** end tags</span></span>
    
  
- <span data-ttu-id="08618-157">**Нижний колонтитул** с закрывающие теги **<!--CE>** и **</div>**</span><span class="sxs-lookup"><span data-stu-id="08618-157">**Footer** with closing **<!--CE>** and **</div>** tags</span></span>
    
  
<span data-ttu-id="08618-p110">Все разделы фрагмент, за исключением предварительного просмотра HTML, заключаются в HTML-код комментариев во избежание взаимодействия с помощью модели объектов документа (DOM) и существующего стилей. Фрагмент начинается с именем компонента и затем включает фактический разметки ASP.NET, предварительный просмотр HTML-код для отрисовки во время разработки и затем к концу тегов. Закомментированы разметка ASP.NET, но SharePoint Удаляет теги комментариев и используется эта разметка при HTML-файл синхронизируется с .master или .aspx файла. Если вы знаете ASP.NET, можно настроить этот разметки в фрагменте.</span><span class="sxs-lookup"><span data-stu-id="08618-p110">All sections of a snippet, except the HTML preview, are enclosed in HTML comments to avoid interactions with the Document Object Model (DOM) and existing styling. A snippet starts with the name of a component, and then includes its actual ASP.NET markup, an HTML preview for design-time rendering, and then ending tags. The ASP.NET markup is commented out, but SharePoint strips out the comment tags and uses this markup when the HTML file is synced to the .master or .aspx file. If you know ASP.NET, you can customize this markup in the snippet.</span></span>
  
    
    
<span data-ttu-id="08618-162">Пример: Вот разметка по умолчанию для изменения режима панели, просто контейнер, в котором условно отображаются другие содержимое и элементы управления.</span><span class="sxs-lookup"><span data-stu-id="08618-162">As an example, the following is the default markup for an Edit Mode Panel, which is simply a container that conditionally displays other content and controls.</span></span>
  
    
    

### <a name="header"></a><span data-ttu-id="08618-163">Верхний колонтитул</span><span class="sxs-lookup"><span data-stu-id="08618-163">Header</span></span>


```HTML

<div data-name="EditModePanelShowInEdit">
    <!--CS: Start Edit Mode Panel Snippet-->
```


### <a name="sharepoint-markup"></a><span data-ttu-id="08618-164">Разметка SharePoint</span><span class="sxs-lookup"><span data-stu-id="08618-164">SharePoint markup</span></span>


```HTML

<!--SPM:<%@Register Tagprefix="Publishing" Namespace="Microsoft.SharePoint.Publishing.WebControls" Assembly="Microsoft.SharePoint.Publishing, Version=15.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"%>-->
    <!--MS:<Publishing:EditModePanel runat="server" CssClass="edit-mode-panel">-->
```


### <a name="html-preview"></a><span data-ttu-id="08618-165">Предварительный просмотр HTML-код</span><span class="sxs-lookup"><span data-stu-id="08618-165">HTML preview</span></span>


```HTML

<!--PS: Start of READ-ONLY PREVIEW (do not modify)--><!--PE: End of READ-ONLY PREVIEW-->
        <div class="DefaultContentBlock" style="border:medium black solid; background:yellow; color:black; margin:20px; padding:10px;">
        You should replace this div with content that renders based on your Edit Mode Panel Properties.
    
        </div>
        <!--PS: Start of READ-ONLY PREVIEW (do not modify)--><!--PE: End of READ-ONLY PREVIEW-->
```


### <a name="footer"></a><span data-ttu-id="08618-166">Нижний колонтитул</span><span class="sxs-lookup"><span data-stu-id="08618-166">Footer</span></span>


```HTML

<!--ME:</Publishing:EditModePanel>-->
    <!--CE: End Edit Mode Panel Snippet-->
</div>
```

<span data-ttu-id="08618-167">Ниже представлена разметка по умолчанию для навигации в начало фрагмента, которого является более сложным, поскольку в этом фрагменте содержит несколько различных элементов управления, с некоторыми вложенных в друг с другом, включая источник данных для терминов навигации, замещаемого элемента управления и заполнитель контента.</span><span class="sxs-lookup"><span data-stu-id="08618-167">The following is the default markup for a Top Navigation snippet, which is more complex because this snippet contains several different controls, with some nested inside each other, including a data source for the navigation terms, a delegate control, and a content placeholder.</span></span>
  
> [!NOTE]
> <span data-ttu-id="08618-168">[!Примечание] Некоторые элементы управления, такие как заполнитель контента, содержат пустые теги предварительном HTML, так как этот элемент не требует визуальное представление на странице.</span><span class="sxs-lookup"><span data-stu-id="08618-168">Some of the controls, such as the content placeholder, contain empty tags for an HTML preview because that element does not require a visual representation on the page.</span></span> 
  
    
    


### <a name="header"></a><span data-ttu-id="08618-169">Верхний колонтитул</span><span class="sxs-lookup"><span data-stu-id="08618-169">Header</span></span>


```HTML

<div data-name="TopNavigationNoFlyoutWithStartNode">
<!--CS: Start Top Navigation Snippet-->    <!--SPM:<%@Register Tagprefix="Publishing" Namespace="Microsoft.SharePoint.Publishing.WebControls" Assembly="Microsoft.SharePoint.Publishing, Version=15.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"%>-->
    <!--MS:<Publishing:EditModePanel runat="server" CssClass="edit-mode-panel">-->
```


### <a name="sharepoint-markup"></a><span data-ttu-id="08618-170">Разметка SharePoint</span><span class="sxs-lookup"><span data-stu-id="08618-170">SharePoint markup</span></span>


```HTML

<!--SPM:<%@Register Tagprefix="SharePoint" Namespace="Microsoft.SharePoint.WebControls" Assembly="Microsoft.SharePoint, Version=15.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"%>-->
<!--MS:<SharePoint:AjaxDelta ID="DeltaTopNavigation" BlockElement="true" CssClass="ms-displayInline ms-core-navigation ms-dialogHidden" runat="server">-->
```


### <a name="html-preview"></a><span data-ttu-id="08618-171">Предварительный просмотр HTML-код</span><span class="sxs-lookup"><span data-stu-id="08618-171">HTML preview</span></span>


```HTML

<!--PS: Start of READ-ONLY PREVIEW (do not modify)-->
<!--PE: End of READ-ONLY PREVIEW-->
```


### <a name="sharepoint-markup"></a><span data-ttu-id="08618-172">Разметка SharePoint</span><span class="sxs-lookup"><span data-stu-id="08618-172">SharePoint markup</span></span>


```HTML

<!--MS:<SharePoint:DelegateControl runat="server" ControlId="TopNavigationDataSource" Id="topNavigationDelegate">-->
```


### <a name="html-preview"></a><span data-ttu-id="08618-173">Предварительный просмотр HTML-код</span><span class="sxs-lookup"><span data-stu-id="08618-173">HTML preview</span></span>


```HTML
<!--PS: Start of READ-ONLY PREVIEW (do not modify)-->
<span style="display:none">
<table cellpadding="4" cellspacing="0" style="font:messagebox;color:buttontext;background-color:buttonface;border: solid 1px;border-top-color:buttonhighlight;border-left-color:buttonhighlight;border-bottom-color:buttonshadow;border-right-color:buttonshadow">
<tr><td nowrap="nowrap">
<span style="font-weight:bold">PortalSiteMapDataSource</span> - topSiteMap</td></tr><tr><td></td></tr></table></span>
<!--PE: End of READ-ONLY PREVIEW-->
```


### <a name="sharepoint-markup"></a><span data-ttu-id="08618-174">Разметка SharePoint</span><span class="sxs-lookup"><span data-stu-id="08618-174">SharePoint markup</span></span>


```HTML

<!--MS:<Template_Controls>-->
<!--MS:<asp:SiteMapDataSource ShowStartingNode="True" SiteMapProvider="SPNavigationProvider" ID="topSiteMap" runat="server" StartingNodeUrl="sid:1002">-->
```


### <a name="sharepoint-markup"></a><span data-ttu-id="08618-175">Разметка SharePoint</span><span class="sxs-lookup"><span data-stu-id="08618-175">SharePoint markup</span></span>


```HTML

<!--ME:</asp:SiteMapDataSource>-->
<!--ME:</Template_Controls>-->
<!--ME:</SharePoint:DelegateControl>--><a name="startNavigation"></a>
```


### <a name="sharepoint-markup"></a><span data-ttu-id="08618-176">Разметка SharePoint</span><span class="sxs-lookup"><span data-stu-id="08618-176">SharePoint markup</span></span>


```HTML

<!--MS:<asp:ContentPlaceHolder ID="PlaceHolderTopNavBar" runat="server">-->
<!--MS:<SharePoint:AspMenu ID="TopNavigationMenu" runat="server" EnableViewState="false" DataSourceID="topSiteMap" AccessKey="&amp;#60;%$Resources:wss,navigation_accesskey%&amp;#62;" UseSimpleRendering="true" UseSeparateCss="false" Orientation="Horizontal" StaticDisplayLevels="2" AdjustForShowStartingNode="false" MaximumDynamicDisplayLevels="0" SkipLinkText="">-->
```


### <a name="html-preview"></a><span data-ttu-id="08618-177">Предварительный просмотр HTML-код</span><span class="sxs-lookup"><span data-stu-id="08618-177">HTML preview</span></span>


```HTML

<!--PS: Start of READ-ONLY PREVIEW (do not modify)-->
<link rel="stylesheet" type="text/css" href="/_layouts/15/1033/styles/menu-21.css" />
<div id="zz7_TopNavigationMenu" class=" noindex ms-core-listMenu-horizontalBox">
<ul id="zz9_RootAspMenu" class="root ms-core-listMenu-root static">
<li class="static">
<a class="static menu-item ms-core-listMenu-item ms-displayInline ms-navedit-linkNode" tabindex="0" title="Default Publishing Site" href="/sites/PubSite/Pages/default.aspx" accesskey="1">
<span class="additional-background ms-navedit-flyoutArrow">
<span class="menu-item-text">Default Publishing Site</span></span></a></li></ul></div>
<!--PE: End of READ-ONLY PREVIEW-->
```


### <a name="sharepoint-markup"></a><span data-ttu-id="08618-178">Разметка SharePoint</span><span class="sxs-lookup"><span data-stu-id="08618-178">SharePoint markup</span></span>


```HTML

<!--ME:</SharePoint:AspMenu>-->
<!--ME:</asp:ContentPlaceHolder>-->
```


### <a name="html-preview"></a><span data-ttu-id="08618-179">Предварительный просмотр HTML-код</span><span class="sxs-lookup"><span data-stu-id="08618-179">HTML preview</span></span>


```HTML

<!--PS: Start of READ-ONLY PREVIEW (do not modify)-->
<!--PE: End of READ-ONLY PREVIEW-->
```


### <a name="sharepoint-markup"></a><span data-ttu-id="08618-180">Разметка SharePoint</span><span class="sxs-lookup"><span data-stu-id="08618-180">SharePoint markup</span></span>


```HTML

<!--ME:</SharePoint:AjaxDelta>-->
```


### <a name="footer"></a><span data-ttu-id="08618-181">Нижний колонтитул</span><span class="sxs-lookup"><span data-stu-id="08618-181">Footer</span></span>


```HTML
<!--CE: End Top Navigation Snippet-->
</div>
```


### <a name="types-of-markup"></a><span data-ttu-id="08618-182">Типы разметки</span><span class="sxs-lookup"><span data-stu-id="08618-182">Types of markup</span></span>

<span data-ttu-id="08618-183">Вот разбивкой типами разметки, включенные в фрагмент.</span><span class="sxs-lookup"><span data-stu-id="08618-183">Here is a breakdown of the types of markup that are included in a snippet.</span></span>
  
    
    
 <span data-ttu-id="08618-184">**Регистрация имен SharePoint** SPM ("SharePoint разметки") указывает строку регистрации пространства имен SharePoint.</span><span class="sxs-lookup"><span data-stu-id="08618-184">**SharePoint namespace registration** SPM ("SharePoint markup") indicates a line registering a SharePoint namespace.</span></span>
  
    
    



```HTML

<!--SPM:<%@Register Tagprefix="SharePoint" Namespace="Microsoft.SharePoint.WebControls" Assembly="Microsoft.SharePoint, Version=15.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"%>-->
```

 <span data-ttu-id="08618-185">**Комментарии** CS и CE («Комментарий начала» и «комментарий окончания») помогают синтаксический анализ строки разметки.</span><span class="sxs-lookup"><span data-stu-id="08618-185">**Comments** CS and CE ("Comment start" and "comment end") help you parse the lines of markup.</span></span>
  
    
    



```HTML
<!--CS: Start Top Navigation Snippet-->
…
<!--CE: End Top Navigation Snippet-->

```

 <span data-ttu-id="08618-p111">**Фрагменты кода** MS и ME («разметки начала» и «разметка окончания») обозначения начала и окончания управления SharePoint или фрагмент. Некоторые фрагменты кода, такой как ленты или выше, элемент управления навигации в начало содержать несколько элементов управления, включенная в один фрагмент.</span><span class="sxs-lookup"><span data-stu-id="08618-p111">**Snippets** MS and ME ("markup start" and "markup end") denote the beginning and end of a SharePoint control or a snippet. Some snippets, like the ribbon or the Top Navigation control above, contain several controls nested within a single snippet.</span></span>
  
    
    



```HTML

<!--MS:<SharePoint:DelegateControl runat="server" ControlId="TopNavigationDataSource" Id="topNavigationDelegate">-->
…
<!--ME:</SharePoint:DelegateControl>--><a name="startNavigation"></a>

<!--MS:<Template_Controls>-->
…
<!--ME:</Template_Controls>-->

<!--MS:<asp:SiteMapDataSource ShowStartingNode="True" SiteMapProvider="SPNavigationProvider" ID="topSiteMap" runat="server" StartingNodeUrl="sid:1002">-->
…
<!--ME:</asp:SiteMapDataSource>-->

```

 <span data-ttu-id="08618-p112">**Предварительная версия блоки** PS и заключите раздел HTML-код, который не следует изменять среда Предустановки («Начало просмотра» и «предварительный просмотр плана»). В этих разделах предварительной версии являются моментальный снимок времени элемента управления SharePoint Вставка фрагмента. Предварительный просмотр позволяет работать более осмысленно на HTML-файл в редакторе HTML со стороны клиента. Однако изменения содержимого или применения стилей в рамках этой предварительной версии не влияет устойчивые на master-файл, который является то, что SharePoint будет в конечном счете с помощью. Применять стиль фрагмент, необходимо определить и переопределения стилей SharePoint с помощью собственных настраиваемых CSS.</span><span class="sxs-lookup"><span data-stu-id="08618-p112">**Preview blocks** PS and PE ("Preview start" and "preview end") surround a section of HTML code that you should not edit. These preview sections are a snapshot in time of the SharePoint control that snippet is inserting. A preview makes it possible for you to work more meaningfully on the HTML file in a client-side HTML editor. But, changing the content or styling within that preview has no lasting effect on the .master file, which is what SharePoint is ultimately using. To style a snippet, you have to identify and override the SharePoint styles with your own custom CSS.</span></span>
  
    
    



```HTML

<!--PS: Start of READ-ONLY PREVIEW (do not modify)--><span style="display:none"><table cellpadding="4" cellspacing="0" style="font:messagebox;color:buttontext;background-color:buttonface;border: solid 1px;border-top-color:buttonhighlight;border-left-color:buttonhighlight;border-bottom-color:buttonshadow;border-right-color:buttonshadow"><tr><td nowrap="nowrap"><span style="font-weight:bold">PortalSiteMapDataSource</span> - topSiteMap</td></tr><tr><td></td></tr></table></span><!--PE: End of READ-ONLY PREVIEW-->

<!--PS: Start of READ-ONLY PREVIEW (do not modify)--><link rel="stylesheet" type="text/css" href="/_layouts/15/1033/styles/menu-21.css" /><div id="zz7_TopNavigationMenu" class=" noindex ms-core-listMenu-horizontalBox"><ul id="zz9_RootAspMenu" class="root ms-core-listMenu-root static"><li class="static"><a class="static menu-item ms-core-listMenu-item ms-displayInline ms-navedit-linkNode" tabindex="0" title="Default Publishing Site" href="/sites/PubSite/Pages/default.aspx" accesskey="1"><span class="additional-background ms-navedit-flyoutArrow"><span class="menu-item-text">Default Publishing Site</span></span></a></li></ul></div><!--PE: End of READ-ONLY PREVIEW-->
```


## <a name="see-also"></a><span data-ttu-id="08618-193">См. также</span><span class="sxs-lookup"><span data-stu-id="08618-193">See also</span></span>
<span data-ttu-id="08618-194"><a name="Resources"> </a></span><span class="sxs-lookup"><span data-stu-id="08618-194"></span></span>


-  [<span data-ttu-id="08618-195">Инструкции. Преобразование HTML-файла в эталонную страницу SharePoint</span><span class="sxs-lookup"><span data-stu-id="08618-195">How to: Convert an HTML file into a master page in SharePoint</span></span>](how-to-convert-an-html-file-into-a-master-page-in-sharepoint.md)
    
  
-  [<span data-ttu-id="08618-196">Инструкции. Создание макета страницы в SharePoint</span><span class="sxs-lookup"><span data-stu-id="08618-196">How to: Create a page layout in SharePoint</span></span>](how-to-create-a-page-layout-in-sharepoint.md)
    
  
-  [<span data-ttu-id="08618-197">Как: Добавление фрагмента панель режима изменения в SharePoint</span><span class="sxs-lookup"><span data-stu-id="08618-197">How to: Add an Edit Mode Panel snippet in SharePoint</span></span>](how-to-add-an-edit-mode-panel-snippet-in-sharepoint.md)
    
  
-  [<span data-ttu-id="08618-198">Как: добавить фрагмент Trim безопасности в SharePoint</span><span class="sxs-lookup"><span data-stu-id="08618-198">How to: Add a Security Trim snippet in SharePoint</span></span>](how-to-add-a-security-trim-snippet-in-sharepoint.md)
    
  

