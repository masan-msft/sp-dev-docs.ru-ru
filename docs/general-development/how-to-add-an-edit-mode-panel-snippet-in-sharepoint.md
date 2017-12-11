---
title: "Добавление фрагмента панель режима изменения в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 39fa1e32-9129-407d-914f-96f4c6e66dc8
ms.openlocfilehash: c5b971b72d8910ac511b27d96a441400afce5323
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="add-an-edit-mode-panel-snippet-in-sharepoint"></a><span data-ttu-id="9ccac-102">Добавление фрагмента панель режима изменения в SharePoint</span><span class="sxs-lookup"><span data-stu-id="9ccac-102">Add an Edit Mode Panel snippet in SharePoint</span></span>

<span data-ttu-id="9ccac-p101">Панель режима изменения  это фрагмент, который можно создать для отображения инструкции или другого содержимого для авторов контента, которые видят содержимое этой панели только во время изменения страницы. С другой стороны, этот фрагмент также можно настроить для отображения этого содержимого только в обычном режиме (режиме просмотра), а не режиме изменения.</span><span class="sxs-lookup"><span data-stu-id="9ccac-p101">An Edit Mode Panel is a snippet that you can use to display instructions or other content to content authors, who see the contents of that panel only when they edit a page. Conversely, this snippet can also be configured to display its contents only in regular (view) mode instead of in edit mode.</span></span>

## <a name="introduction-to-the-edit-mode-panel"></a><span data-ttu-id="9ccac-105">Общие сведения о панели режим редактирования</span><span class="sxs-lookup"><span data-stu-id="9ccac-105">Introduction to the Edit Mode Panel</span></span>
<span data-ttu-id="9ccac-106"><a name="Introduction"> </a></span><span class="sxs-lookup"><span data-stu-id="9ccac-106"></span></span>

<span data-ttu-id="9ccac-p102">При публикации сайта авторы контента с необходимыми разрешениями можно создавать или изменять страницы, которые находятся в библиотеке страниц. Как правило автор решает создать или изменить страницу и затем добавляет содержимое поля страницы.</span><span class="sxs-lookup"><span data-stu-id="9ccac-p102">In a publishing site, content authors with the necessary permissions can create or edit pages that reside in the Pages library. Typically, an author chooses to create or edit a page, and then adds content to the various page fields.</span></span>
  
    
    
<span data-ttu-id="9ccac-p103">Разработчик может добавить панель изменение режима на главной странице или макету страницы и содержимое фрагмента будет отображаться для авторы контента только в том случае, когда они выбрать для изменения страницы в зависимости от макета страницы или страницы, связанные с этой главной страницы. Например можно использовать панель изменение режима будет отображаться следующее содержимое только к авторы контента, если страница находится в режиме редактирования:</span><span class="sxs-lookup"><span data-stu-id="9ccac-p103">As a designer, you can add an Edit Mode Panel to a master page or page layout, and the contents of that snippet will be visible to content authors only when they choose to edit a page based on that page layout or a page associated with that master page. For example, you can use an Edit Mode Panel to display the following content only to content authors when the page is in edit mode:</span></span>
  
    
    

- <span data-ttu-id="9ccac-111">Поля страницы, такие как **Schedule Publishing Date**, важна автор контента, но не посетители просматриваете страницу на действующего сайта.</span><span class="sxs-lookup"><span data-stu-id="9ccac-111">A page field, such as **Schedule Publishing Date**, that's important to the content author but not to visitors viewing the page on the live site.</span></span>
    
  
- <span data-ttu-id="9ccac-112">Описание типа контента, следует ввести в поле страницы.</span><span class="sxs-lookup"><span data-stu-id="9ccac-112">A description of what kind of content should be entered in a page field.</span></span>
    
  
- <span data-ttu-id="9ccac-113">Примечание для авторов контента, их следует учесть, как будет выглядеть страница для разных каналах устройств.</span><span class="sxs-lookup"><span data-stu-id="9ccac-113">A note to content authors that they should consider how the page looks for different device channels.</span></span>
    
  
<span data-ttu-id="9ccac-114">Также можно поместить ссылки для различных стилей панели изменить режим таким образом, можно обеспечить различных стилей для изменить режим и режим просмотра.</span><span class="sxs-lookup"><span data-stu-id="9ccac-114">You can also put links to different style sheets in an Edit Mode Panel so that you can provide different styling for edit mode vs. view mode.</span></span>
  
    
    
<span data-ttu-id="9ccac-p104">Панель изменение режима следует добавить в макет страниц при заметки о авторы контента зависят от типа контента, на котором основан этот макет страницы. Также можно добавить в этом фрагменте на главную страницу, когда заметки о авторы могут быть применены на всех страницах, которые должны быть связаны с этой главной страницей  например, если панель будет содержать инструкции по предоставляющий контент для канала определенное устройство, которая использует Главная.</span><span class="sxs-lookup"><span data-stu-id="9ccac-p104">You should add the Edit Mode Panel to a page layout when the notes for content authors are specific to the content type on which that page layout is based. You can also add this snippet to a master page when the notes for authors are applicable to all pages that will be associated with that master page—for example, if the panel will contain instructions for supplying content for a specific device channel that uses that master page.</span></span>
  
    
    
<span data-ttu-id="9ccac-117">Изменение панели режим для отображения содержимого только в обычном режиме, а не в режиме редактирования, можно также задать при наличии сценария, где это полезно или полезны для отображения содержимого только посетителям сайта (но не авторы содержимого) Если требуется изменить страницу.</span><span class="sxs-lookup"><span data-stu-id="9ccac-117">You can also set an Edit Mode Panel to display its contents only in regular mode, instead of edit mode, if you have a scenario where it's useful or helpful to display content only to site visitors (but not content authors) when they're editing a page.</span></span>
  
    
    

### <a name="insert-an-edit-mode-panel"></a><span data-ttu-id="9ccac-118">Вставка панели режим редактирования</span><span class="sxs-lookup"><span data-stu-id="9ccac-118">Insert an Edit Mode Panel</span></span>
<span data-ttu-id="9ccac-119"><a name="InsertSnippet"> </a></span><span class="sxs-lookup"><span data-stu-id="9ccac-119"></span></span>

<span data-ttu-id="9ccac-p105">Как и все фрагменты кода добавляются в этом фрагменте коллекция фрагментов кода. Чтобы перейти к коллекция фрагментов кода, сначала нужно выбрать главную страницу или макет страницы для редактирования.</span><span class="sxs-lookup"><span data-stu-id="9ccac-p105">Like all snippets, you add this snippet from the Snippet Gallery. To navigate to the Snippet Gallery, you must first select a master page or page layout to edit.</span></span>
  
    
    

### <a name="to-insert-an-edit-mode-panel"></a><span data-ttu-id="9ccac-122">Чтобы вставить панель режиме редактирования</span><span class="sxs-lookup"><span data-stu-id="9ccac-122">To insert an Edit Mode panel</span></span>


1. <span data-ttu-id="9ccac-123">Откройте свой сайт публикации.</span><span class="sxs-lookup"><span data-stu-id="9ccac-123">Browse to your publishing site.</span></span>
    
  
2. <span data-ttu-id="9ccac-124">Нажмите значок шестеренки "Параметры" в правом верхнем углу страницы, а затем выберите **Дизайнер**.</span><span class="sxs-lookup"><span data-stu-id="9ccac-124">In the upper-right corner of the page, choose the Settings gear, and then choose **Design Manager**.</span></span>
    
  
3. <span data-ttu-id="9ccac-125">В диспетчере оформления на левой панели навигации слева выберите **Изменить главную страницу** или **Изменение макетов страниц**, в зависимости от того, какой тип файла требуется изменить.</span><span class="sxs-lookup"><span data-stu-id="9ccac-125">In Design Manager, in the left navigation pane, choose **Edit Master Pages** or **Edit Page Layouts**, depending on what type of file you're editing.</span></span>
    
  
4. <span data-ttu-id="9ccac-126">Выберите имя главной страницы или макет страницы, который вы хотите добавить фрагмент для.</span><span class="sxs-lookup"><span data-stu-id="9ccac-126">Select the name of the master page or page layout that you want to add the snippet to.</span></span>
    
  
5. <span data-ttu-id="9ccac-127">Чтобы открыть коллекцию фрагментов, выберите **Фрагменты** в правом верхнем углу страницы предварительного просмотра на стороне сервера.</span><span class="sxs-lookup"><span data-stu-id="9ccac-127">To open the Snippet Gallery, choose **Snippets** in the upper-right corner of the server-side preview.</span></span>
    
  
6. <span data-ttu-id="9ccac-128">На ленте перейдите на вкладку **Конструктор** нажмите кнопку **Изменить режим панели** и выберите требуемый фрагмент кода для отображения в режим.</span><span class="sxs-lookup"><span data-stu-id="9ccac-128">On the ribbon, on the **Design** tab, choose **Edit Mode Panel**, and then choose the mode that you want your snippet to be displayed in.</span></span>
    
  
7. <span data-ttu-id="9ccac-129">В разделе **Об этом компоненте** в правой части коллекции фрагментов щелкните или выберите заголовок раздела, чтобы развернуть или свернуть группу свойств, а затем настройте все нужные настраиваемые параметры.</span><span class="sxs-lookup"><span data-stu-id="9ccac-129">On the right side of the Snippet Gallery, under **About this Component**, click or select section headers to expand or collapse groups of properties, and then configure any custom settings that you want.</span></span>
    
    <span data-ttu-id="9ccac-p106">Раздел, с именем важные содержит свойства, которые наиболее важные для работы этого конкретного фрагмента. Для изменения режима панели **PageDisplayMode** свойство будет иметь значение **Edit** или **Display**, в зависимости от режима, выбранного на ленте.</span><span class="sxs-lookup"><span data-stu-id="9ccac-p106">The section named Important contains the properties that are most important to how this particular snippet works. For an Edit Mode Panel, the **PageDisplayMode** property will be set to either **Edit** or **Display**, depending on the mode that you selected on the ribbon.</span></span>
    
  
8. <span data-ttu-id="9ccac-p107">Настроив свойства, нажмите **Обновить**. При этом обновляется фрагмент HTML в левой части страницы, чтобы разметка отражала настраиваемые параметры. Вы всегда можете нажать кнопку **Сбросить**, чтобы восстановить исходные значения всех свойств.</span><span class="sxs-lookup"><span data-stu-id="9ccac-p107">After you configure any properties, choose **Update**. This updates the HTML snippet on the left side of the page, so that the markup reflects your custom settings. You can always choose **Reset** to return all properties to their default settings.</span></span>
    
  
9. <span data-ttu-id="9ccac-135">В разделе **Фрагмент HTML** в левой части коллекции фрагментов выберите команду **Копировать в буфер обмена**.</span><span class="sxs-lookup"><span data-stu-id="9ccac-135">On the left side of the Snippet Gallery, under **HTML Snippet**, choose **Copy to Clipboard**.</span></span>
    
  
10. <span data-ttu-id="9ccac-136">В редакторе HTML откройте сопоставленный сетевой диск на своем компьютере, а затем откройте HTML-файл для эталонной страницы или макета, к которым добавляется фрагмент.</span><span class="sxs-lookup"><span data-stu-id="9ccac-136">In your HTML editor, open the mapped network drive on your computer, and then open the HTML file for the master page or page layout that you're adding the snippet to.</span></span> <span data-ttu-id="9ccac-137">Дополнительные сведения см. в статье  [Как: сопоставление сетевого диска коллекции главных страниц SharePoint](how-to-map-a-network-drive-to-the-sharepoint-master-page-gallery.md).</span><span class="sxs-lookup"><span data-stu-id="9ccac-137">For more information, see  [How to: Map a network drive to the SharePoint Master Page Gallery](how-to-map-a-network-drive-to-the-sharepoint-master-page-gallery.md).</span></span>
    
  
11. <span data-ttu-id="9ccac-138">Вставьте фрагмент в том месте HTML-файла, где должна отображаться разметка.</span><span class="sxs-lookup"><span data-stu-id="9ccac-138">In the HTML file, paste the snippet where you want the markup to appear.</span></span>
    
    <span data-ttu-id="9ccac-p109">При добавлении панель режима изменения в макет страниц, убедитесь в том вставить фрагмент внутри **PlaceHolderMain**, чтобы панели будет отображаться авторы контента в режиме редактирования. Можно вставить фрагмент непосредственно перед полем определенные страницы или можно размещать одно или несколько полей страницы внутри панели режима редактирования.</span><span class="sxs-lookup"><span data-stu-id="9ccac-p109">If you're adding the Edit Mode Panel to a page layout, make sure to paste the snippet inside **PlaceHolderMain** so that the panel is visible to content authors in edit mode. You can paste the snippet immediately before a specific page field, or you can put one or more page fields inside the Edit Mode Panel.</span></span>
    
  
12. <span data-ttu-id="9ccac-141">Замените **<div>** где `class="DefaultContentBlock"` с конкретного содержимого  например, с помощью заметки или инструкциям, чтобы авторы контента или поля определенных параметров страницы, предназначенные для авторов, но не посетители сайта.</span><span class="sxs-lookup"><span data-stu-id="9ccac-141">Replace the **<div>** where `class="DefaultContentBlock"` with your own specific content—for example, with notes or instructions to content authors, or specific page fields that are useful for authors but not site visitors.</span></span>
    
  
13. <span data-ttu-id="9ccac-142">Сохраните страницу и обновите на сервере предварительного просмотра в диспетчере оформления для убедитесь, что отображается панель изменение режима.</span><span class="sxs-lookup"><span data-stu-id="9ccac-142">Save the page, and then refresh the server-side preview in Design Manager to make sure the Edit Mode Panel appears as expected.</span></span>
    
  

## <a name="understand-the-snippet-markup"></a><span data-ttu-id="9ccac-143">Понять фрагмент разметки</span><span class="sxs-lookup"><span data-stu-id="9ccac-143">Understand the snippet markup</span></span>
<span data-ttu-id="9ccac-144"><a name="UnderstandMarkup"> </a></span><span class="sxs-lookup"><span data-stu-id="9ccac-144"></span></span>

<span data-ttu-id="9ccac-p110">Два наиболее важные части фрагмента панели изменить режим, свойство **PageDisplayMode** и **<div>** где `class="DefaultContentBlock"`. Свойство **PageDisplayMode** определяет, отображаются ли содержимое панели только в режиме редактирования или в режиме обычный и отображения (то есть каждый раз, когда страница не находится в режиме редактирования).</span><span class="sxs-lookup"><span data-stu-id="9ccac-p110">The two most important parts of an Edit Mode Panel snippet are the **PageDisplayMode** property and the **<div>** where `class="DefaultContentBlock"`. The **PageDisplayMode** property determines whether the contents of the panel are displayed only in edit mode or in regular/display mode (meaning whenever the page is not in edit mode).</span></span>
  
> [!NOTE]
> <span data-ttu-id="9ccac-p111">[!Примечание] Это свойство не отображается в разметке, если не измените значение на **Display**. Если свойство не отображается в разметке, режим по умолчанию для фрагмента  режим редактирования.</span><span class="sxs-lookup"><span data-stu-id="9ccac-p111">This property doesn't appear in the markup unless you change the value to **Display**. When the property does not appear in the markup, the default mode for the snippet is Edit mode.</span></span> 
  
    
    

<span data-ttu-id="9ccac-149">**<div>**, где `class="DefaultContentBlock"`  заменить на собственный текст, который может содержать другие фрагменты кода и элементов управления.</span><span class="sxs-lookup"><span data-stu-id="9ccac-149">The **<div>** where `class="DefaultContentBlock"` is what you replace with your own content, which can include other snippets and controls.</span></span>
  
    
    



```HTML

<div data-name="EditModePanelShowInEdit">
    <!--CS: Start Edit Mode Panel Snippet-->
    <!--SPM:<%@Register Tagprefix="Publishing" Namespace="Microsoft.SharePoint.Publishing.WebControls" Assembly="Microsoft.SharePoint.Publishing, Version=15.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"%>-->
    <!--MS:<Publishing:EditModePanel runat="server" PageDisplayMode="Display" CssClass="edit-mode-panel">-->
        <!--PS: Start of READ-ONLY PREVIEW (do not modify)--><!--PE: End of READ-ONLY PREVIEW-->
        <div class="DefaultContentBlock" style="border:medium black solid; background:yellow; color:black; margin:20px; padding:10px;">
        You should replace this div with content that renders based on your Edit Mode Panel Properties.
        </div>
        <!--PS: Start of READ-ONLY PREVIEW (do not modify)--><!--PE: End of READ-ONLY PREVIEW-->
    <!--ME:</Publishing:EditModePanel>-->
    <!--CE: End Edit Mode Panel Snippet-->
</div>
```


## <a name="see-also"></a><span data-ttu-id="9ccac-150">См. также</span><span class="sxs-lookup"><span data-stu-id="9ccac-150">See also</span></span>
<span data-ttu-id="9ccac-151"><a name="AdditionalResources"> </a></span><span class="sxs-lookup"><span data-stu-id="9ccac-151"></span></span>


-  [<span data-ttu-id="9ccac-152">Фрагменты кода дизайнер SharePoint</span><span class="sxs-lookup"><span data-stu-id="9ccac-152">SharePoint Design Manager snippets</span></span>](sharepoint-design-manager-snippets.md)
    
  
-  [<span data-ttu-id="9ccac-153">Как: добавить фрагмент Trim безопасности в SharePoint</span><span class="sxs-lookup"><span data-stu-id="9ccac-153">How to: Add a Security Trim snippet in SharePoint</span></span>](how-to-add-a-security-trim-snippet-in-sharepoint.md)
    
  
-  [<span data-ttu-id="9ccac-154">Создание сайтов для SharePoint</span><span class="sxs-lookup"><span data-stu-id="9ccac-154">Build sites for SharePoint</span></span>](build-sites-for-sharepoint.md)
    
  
-  [<span data-ttu-id="9ccac-155">Разработка макета сайта в SharePoint</span><span class="sxs-lookup"><span data-stu-id="9ccac-155">Develop the site design in SharePoint</span></span>](develop-the-site-design-in-sharepoint.md)
    
  

