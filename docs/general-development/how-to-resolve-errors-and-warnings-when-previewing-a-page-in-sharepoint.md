---
title: "Устранение ошибок и предупреждения при предварительном просмотре страницы в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 03f72f65-b22b-4304-be92-f44ce0619372
ms.openlocfilehash: 73895457694d250f1527b69bd558335fd573263c
ms.sourcegitcommit: f6ea922341c38e700d0697961f8df9a454a03cba
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/15/2017
---
# <a name="resolve-errors-and-warnings-when-previewing-a-page-in-sharepoint"></a><span data-ttu-id="c278a-102">Устранение ошибок и предупреждения при предварительном просмотре страницы в SharePoint</span><span class="sxs-lookup"><span data-stu-id="c278a-102">Resolve errors and warnings when previewing a page in SharePoint</span></span>

<span data-ttu-id="c278a-p101">После преобразования HTML-файла в эталонную страницу SharePoint или создания макета страницы вы можете просмотреть эту страницу в браузере. Однако перед этим вам может потребоваться устранить проблемы, которые препятствуют отрисовке вашей страницы предварительного просмотра на стороне сервера.</span><span class="sxs-lookup"><span data-stu-id="c278a-p101">After you convert an HTML file into a SharePoint master page, or after you create a page layout, you can preview that page in the browser. But before you can preview a master page or page layout, you may have to resolve any issues that prevent the server-side preview from rendering your page.</span></span>

## <a name="introduction-to-resolving-preview-errors"></a><span data-ttu-id="c278a-105">Общие сведения о Устранение ошибок предварительного просмотра</span><span class="sxs-lookup"><span data-stu-id="c278a-105">Introduction to resolving preview errors</span></span>
<span data-ttu-id="c278a-106"><a name="Introduction"> </a></span><span class="sxs-lookup"><span data-stu-id="c278a-106"></span></span>

<span data-ttu-id="c278a-107">После преобразования HTML-файла в главную страницу SharePoint, или создание макета страницы, можно выполнить предварительный просмотр страницы в браузере.</span><span class="sxs-lookup"><span data-stu-id="c278a-107">After you convert an HTML file into a SharePoint master page, or after you create a page layout, you can preview that page in the browser.</span></span> <span data-ttu-id="c278a-108">Как изменить и сохранить главной страницы HTML или макет страницы, вы можете обновить Просмотр, чтобы просмотреть, как точно SharePoint отображает страницу.</span><span class="sxs-lookup"><span data-stu-id="c278a-108">As you edit and save your HTML master page or page layout, you can refresh the preview to see exactly how SharePoint renders your page.</span></span>
  
    
    
<span data-ttu-id="c278a-109">Предварительного просмотра в диспетчере оформления является интерактивный просмотр на сервере, поэтому все фрагменты или элементов управления на странице, например, элемент управления навигации или веб-части на основе механизмов поиска, использование динамических данных.</span><span class="sxs-lookup"><span data-stu-id="c278a-109">The preview in Design Manager is a live server-side preview, so any snippets or controls on your page, such as a navigation control or a search-driven Web Part, use live data.</span></span> <span data-ttu-id="c278a-110">Кроме того при предварительном просмотре главной странице или макету страницы, можно выбрать универсальный Предварительный просмотр только этот файл, или можно выбрать для предварительного просмотра способ отображения определенных страницы на сайте с этой главной страницы или макет страницы.</span><span class="sxs-lookup"><span data-stu-id="c278a-110">Also, when you preview a master page or page layout, you can choose a generic preview of just that file, or you can choose to preview how a specific page in your site renders with that master page or page layout.</span></span> <span data-ttu-id="c278a-111">Предварительная версия на сервере — очень удобен в средство, которое дополняет предварительного просмотра во время разработки в редакторе HTML.</span><span class="sxs-lookup"><span data-stu-id="c278a-111">The server-side preview is a highly useful tool that complements the design-time preview in an HTML editor.</span></span> <span data-ttu-id="c278a-112">Дополнительные сведения можно [способ: изменение страницы предварительного просмотра в диспетчере оформления SharePoint](how-to-change-the-preview-page-in-sharepoint-design-manager.md).</span><span class="sxs-lookup"><span data-stu-id="c278a-112">For more information, see  [How to: Change the preview page in SharePoint Design Manager](how-to-change-the-preview-page-in-sharepoint-design-manager.md).</span></span>
  
    
    
<span data-ttu-id="c278a-113">Однако перед можно выполнить предварительный просмотр главной странице или макету страницы, возможно, для устранения проблем, которые препятствуют предварительной версии на сервере отображения страницы.</span><span class="sxs-lookup"><span data-stu-id="c278a-113">But before you can preview a master page or page layout, you may have to resolve any issues that prevent the server-side preview from rendering your page.</span></span> <span data-ttu-id="c278a-114">Если preview на сервере не работает, это означает, что главной странице или макету страницы также не будут работать после их в случае применения к своему сайту.</span><span class="sxs-lookup"><span data-stu-id="c278a-114">If the server-side preview isn't working, this means that the master page or page layout also won't work after they're applied to your site.</span></span> <span data-ttu-id="c278a-115">В диспетчере оформления после преобразования главную страницу или создание макета страницы, можно щелкнуть состояние имя или преобразования файлов для предварительного просмотра, файл.</span><span class="sxs-lookup"><span data-stu-id="c278a-115">In Design Manager, after you convert a master page or create a page layout, you can click the file name or conversion status to preview that file.</span></span> <span data-ttu-id="c278a-116">На странице "Просмотр" в области уведомлений в верхней части страницы отображается ошибки и предупреждения.</span><span class="sxs-lookup"><span data-stu-id="c278a-116">On the preview page, the notification area at the top of the page displays any errors or warnings.</span></span>
  
    
    
<span data-ttu-id="c278a-117">Ниже приведены preview ошибки и предупреждения, которые могут возникать и справки для методы их устранения.</span><span class="sxs-lookup"><span data-stu-id="c278a-117">Here are the preview errors and warnings that you might encounter, and help for how to resolve them.</span></span>
  
    
    

## <a name="html-file-cannot-contain-form-tags"></a><span data-ttu-id="c278a-118">HTML-файл не может содержать \<формы\> тегов</span><span class="sxs-lookup"><span data-stu-id="c278a-118">HTML file cannot contain \<form\> tags</span></span>
<span data-ttu-id="c278a-119"><a name="FormTags"> </a></span><span class="sxs-lookup"><span data-stu-id="c278a-119"></span></span>


### <a name="message"></a><span data-ttu-id="c278a-120">Message</span><span class="sxs-lookup"><span data-stu-id="c278a-120">Message</span></span>

 <span data-ttu-id="c278a-121">**Главная страница содержит один или несколько HTML \<формы\> тегов. Для главной страницы для работы удалите теги (но можно оставить содержимое в них).**</span><span class="sxs-lookup"><span data-stu-id="c278a-121">**Your Master Page has one or more HTML \<FORM\> tags. For your master page to work, remove the tags (but you can leave the content in them).**</span></span>
  
    
    

### <a name="resolution"></a><span data-ttu-id="c278a-122">Решение</span><span class="sxs-lookup"><span data-stu-id="c278a-122">Resolution</span></span>

<span data-ttu-id="c278a-123">Страницы SharePoint, уже заключаться в ** \<формы\> ** тега, чтобы ASP.NET можно выполнить после завершения выполняет резервное (в частности, SharePoint.master страница содержит тег **< SharePoint:SharePointForm >** , который создает фактический ** \<формы \> ** тега при отображении связанного содержимого страницы).</span><span class="sxs-lookup"><span data-stu-id="c278a-123">SharePoint pages are already wrapped in a **\<form\>** tag so that ASP.NET can do post-backs (specifically, a SharePoint.master page contains the **<SharePoint:SharePointForm>** tag that creates an actual **\<form\>** tag when an associated content page is rendered).</span></span> <span data-ttu-id="c278a-124">В результате, включая ** \<формы\> ** тега образец страницы или страницы макета означает, что может быть вложенными ** \<формы\> ** тегов в последнем отображения на странице, которая не является допустимым в формате HTML.</span><span class="sxs-lookup"><span data-stu-id="c278a-124">So, including a **\<form\>** tag on your master page or page layout means that there would be nested **\<form\>** tags on the final rendering of the page, which is not valid in HTML.</span></span> <span data-ttu-id="c278a-125">В редакторе HTML, удалять любые ** \<формы\> ** теги сохранении страницы, а затем обновите предварительного просмотра.</span><span class="sxs-lookup"><span data-stu-id="c278a-125">In your HTML editor, delete any **\<form\>** tags, save the page, and then refresh the preview.</span></span>
  
    
    
<span data-ttu-id="c278a-126">Если вы хотите, чтобы HTML ** \<формы\> ** тег в макет страницы, следует помещать форму в заполнитель контента с Идентификатором **PlaceHolderUtilityContent** , добавив следующий код макет страницы HTML-код:</span><span class="sxs-lookup"><span data-stu-id="c278a-126">If you want an HTML **\<form\>** tag in the page layout, you should put the form within a content placeholder with the ID **PlaceHolderUtilityContent** by adding this code to your HTML page layout:</span></span>
  
    
    



```HTML

<!--CS: Start Create Snippets From Custom ASP.NET Markup Snippet-->
<!--SPM:<SharePoint:AjaxDelta id="DeltaPlaceHolderUtilityContent" runat="server">-->
<!--SPM:<asp:ContentPlaceHolder id="PlaceHolderUtilityContent" runat="server" />-->
<!--SPM:</SharePoint:AjaxDelta>-->
<!--CE: End Create Snippets From Custom ASP.NET Markup Snippet-->
```

<span data-ttu-id="c278a-127">Также можно добавить веб-часть формы HTML или веб-части форм InfoPath на страницу из коллекция фрагментов кода.</span><span class="sxs-lookup"><span data-stu-id="c278a-127">You can also add the HTML Form Web Part or the InfoPath Form Web Part to your page from the Snippet Gallery.</span></span> <span data-ttu-id="c278a-128">Дополнительные сведения см. в статье  [Фрагменты кода дизайнер SharePoint](sharepoint-design-manager-snippets.md).</span><span class="sxs-lookup"><span data-stu-id="c278a-128">For more information, see  [SharePoint Design Manager snippets](sharepoint-design-manager-snippets.md).</span></span>
  
    
    

## <a name="html-file-must-be-xml-compliant"></a><span data-ttu-id="c278a-129">HTML-файл должен быть с XML</span><span class="sxs-lookup"><span data-stu-id="c278a-129">HTML file must be XML-compliant</span></span>
<span data-ttu-id="c278a-130"><a name="XMLCompliant"> </a></span><span class="sxs-lookup"><span data-stu-id="c278a-130"></span></span>


### <a name="message"></a><span data-ttu-id="c278a-131">Message</span><span class="sxs-lookup"><span data-stu-id="c278a-131">Message</span></span>

 <span data-ttu-id="c278a-132">**SharePoint требуется HTML-файлы для соответствия стандартам XML. Файл не является XML-совместимым, скорее всего из-за свойства тега без кавычек, отсутствующие закрывающие теги и недопустимые свойства в тегах. {Тип ошибки, ошибки}. Ошибка по адресу: {время}.**</span><span class="sxs-lookup"><span data-stu-id="c278a-132">**SharePoint requires HTML files to be XML-compliant. Your file isn't XML-compliant, likely because of tag properties without quotes, missing closing tags, or invalid properties in tags. {Type of error, location of error}. Occurred at: {Time}.**</span></span>
  
    
    

### <a name="resolution"></a><span data-ttu-id="c278a-133">Решение</span><span class="sxs-lookup"><span data-stu-id="c278a-133">Resolution</span></span>

<span data-ttu-id="c278a-134">Для HTML-файла для преобразования его в файл, соответствующий ASP.NET HTML-файл должен быть спецификации XML.</span><span class="sxs-lookup"><span data-stu-id="c278a-134">For an HTML file to be converted into the corresponding ASP.NET file, the HTML file must be XML-compliant.</span></span> <span data-ttu-id="c278a-135">Эта ошибка указывает определенные разметки в HTML-файл, который не соответствует спецификации XML.</span><span class="sxs-lookup"><span data-stu-id="c278a-135">This error identifies specific markup in your HTML file that is not XML-compliant.</span></span> <span data-ttu-id="c278a-136">Работать HTML-файл с помощью средства проверки XML, устранение неполадок в редакторе HTML, сохраните файл и затем обновить предварительного просмотра.</span><span class="sxs-lookup"><span data-stu-id="c278a-136">Run the HTML file through an XML validator, fix any issues in your HTML editor, save the file, and then refresh the preview.</span></span>
  
    
    

> <span data-ttu-id="c278a-137">**Примечание:** Это требование переопределяет некоторые стандартов HTML 5.</span><span class="sxs-lookup"><span data-stu-id="c278a-137">**Note:** This requirement overrides some HTML 5 standards.</span></span> <span data-ttu-id="c278a-138">Например в HTML 5 можно указать тип документа в нижнем регистре, но в XML тип документа должно быть в верхнем регистре.</span><span class="sxs-lookup"><span data-stu-id="c278a-138">For example, in HTML 5 you can specify the doctype in lowercase, but in XML the doctype must be uppercase.</span></span> 
  
    
    


  
    
    

## <a name="html-file-contains-problematic-markup"></a><span data-ttu-id="c278a-139">HTML-файл содержит инспектором разметки</span><span class="sxs-lookup"><span data-stu-id="c278a-139">HTML file contains problematic markup</span></span>
<span data-ttu-id="c278a-140"><a name="ProblematicMarkup"> </a></span><span class="sxs-lookup"><span data-stu-id="c278a-140"></span></span>


### <a name="message"></a><span data-ttu-id="c278a-141">Message</span><span class="sxs-lookup"><span data-stu-id="c278a-141">Message</span></span>

 <span data-ttu-id="c278a-142">**SharePoint не удается обработать этот файл, скорее всего, из-за неправильно форматированные фрагмент SharePoint. Разметка в следующем расположении вызывает проблемы. Редактирование разметки вручную, чтобы устранить проблему или заменить ее новой фрагмент коллекция фрагментов кода. {Тип ошибки, ошибки}. Ошибка по адресу: {время}.**</span><span class="sxs-lookup"><span data-stu-id="c278a-142">**SharePoint can't parse this file, most likely because of an incorrectly formatted SharePoint snippet. The markup at the following location is causing problems. Edit the markup manually to fix it, or replace it with a new snippet from the Snippet Gallery. {Type of error, location of error}. Occurred at: {Time}.**</span></span>
  
    
    

### <a name="resolution"></a><span data-ttu-id="c278a-143">Решение</span><span class="sxs-lookup"><span data-stu-id="c278a-143">Resolution</span></span>

<span data-ttu-id="c278a-144">Эта ошибка появляется при наличии проблем с фрагмента SharePoint в HTML-файл.</span><span class="sxs-lookup"><span data-stu-id="c278a-144">You see this error when there is a problem with a SharePoint snippet in your HTML file.</span></span> <span data-ttu-id="c278a-145">Чтобы устранить эту ошибку, отмените все, что изменения, возникающие ошибки или замените инспектором фрагмент на новый, из коллекции фрагмент или из различных главную страницу или файл макета страницы, в котором рабочей версии фрагмента.</span><span class="sxs-lookup"><span data-stu-id="c278a-145">To fix this error, undo whatever change caused the error, or replace the problematic snippet with a new one, either from the Snippet Gallery or from a different master page or page layout file that has a working version of the snippet.</span></span> <span data-ttu-id="c278a-146">В редакторе HTML после устранить или замените фрагмента сохранить страницу и затем обновить предварительного просмотра.</span><span class="sxs-lookup"><span data-stu-id="c278a-146">In your HTML editor, after you fix or replace the snippet, save the page, and then refresh the preview.</span></span>
  
    
    

## <a name="master-page-for-a-page-layout-has-changed"></a><span data-ttu-id="c278a-147">Главная страница для макета страницы был изменен</span><span class="sxs-lookup"><span data-stu-id="c278a-147">Master page for a page layout has changed</span></span>
<span data-ttu-id="c278a-148"><a name="PageLayoutChanged"> </a></span><span class="sxs-lookup"><span data-stu-id="c278a-148"></span></span>


### <a name="message"></a><span data-ttu-id="c278a-149">Message</span><span class="sxs-lookup"><span data-stu-id="c278a-149">Message</span></span>

 <span data-ttu-id="c278a-150">**Главную страницу макета страницы, была изменена, которое может вызвать несоответствия между веб-узла. Щелкните здесь, чтобы обновить в разделах макет страницы, представляющих области главной страницы.**</span><span class="sxs-lookup"><span data-stu-id="c278a-150">**This page layout's master page has changed, which will cause inconsistencies across your site. Click here to update the sections of your page layout that represent master page regions.**</span></span>
  
    
    

### <a name="resolution"></a><span data-ttu-id="c278a-151">Решение</span><span class="sxs-lookup"><span data-stu-id="c278a-151">Resolution</span></span>

<span data-ttu-id="c278a-152">Для макета страницы для работы с заданным главной страницы два должен иметь один и тот же набор заполнителей контента.</span><span class="sxs-lookup"><span data-stu-id="c278a-152">For a page layout to work with a given master page, the two must have the same set of content placeholders.</span></span> <span data-ttu-id="c278a-153">Если создание макета страницы, на основе определенного главной страницы, а затем изменить главную страницу, HTML, вы увидите это сообщение.</span><span class="sxs-lookup"><span data-stu-id="c278a-153">If you create a page layout based on a particular master page, and then edit that HTML master page, you'll see this message.</span></span> <span data-ttu-id="c278a-154">Даже в том случае, если вы знаете, что изменения на главную страницу не добавить или удалить заполнителей контента, следует обновить области контента макета страницы, таким образом, можно выполнить предварительный просмотр изменений из главной страницы, которые могут влиять на макет страницы.</span><span class="sxs-lookup"><span data-stu-id="c278a-154">Even if you know that changes to the master page didn't add or remove content placeholders, you should update the content regions of your page layout anyway, so that you can preview any changes from the master page that might affect your page layout.</span></span>
  
    
    

## <a name="reset-the-preview"></a><span data-ttu-id="c278a-155">Сброс предварительного просмотра</span><span class="sxs-lookup"><span data-stu-id="c278a-155">Reset the preview</span></span>
<span data-ttu-id="c278a-156"><a name="ResetPreview"> </a></span><span class="sxs-lookup"><span data-stu-id="c278a-156"></span></span>


### <a name="message"></a><span data-ttu-id="c278a-157">Message</span><span class="sxs-lookup"><span data-stu-id="c278a-157">Message</span></span>

 <span data-ttu-id="c278a-158">**Главной страницы (макет страницы) не все предупреждения и ошибки. Сброс предварительного просмотра в исходное состояние.**</span><span class="sxs-lookup"><span data-stu-id="c278a-158">**Your master page (page layout) doesn't have any warnings or errors. Reset the preview to its original state.**</span></span>
  
    
    

### <a name="explanation"></a><span data-ttu-id="c278a-159">Объяснение</span><span class="sxs-lookup"><span data-stu-id="c278a-159">Explanation</span></span>

<span data-ttu-id="c278a-160">Это сообщение просто подтверждает, что процесс преобразования работает без ошибок и проблем.</span><span class="sxs-lookup"><span data-stu-id="c278a-160">This message simply confirms that the conversion process worked with no errors or issues.</span></span> <span data-ttu-id="c278a-161">Тем не менее при предварительном просмотре страницы, вы можете перейти с этой конкретной страницы или предварительного просмотра каким-либо другим образом.</span><span class="sxs-lookup"><span data-stu-id="c278a-161">However, when you preview a page, you may navigate away from that specific page or change the preview in some other way.</span></span> <span data-ttu-id="c278a-162">В этом случае вы всегда можете **Сброс предварительного просмотра** в то место сообщения.</span><span class="sxs-lookup"><span data-stu-id="c278a-162">If this happens, you can always choose **Reset the preview** in the message area.</span></span> <span data-ttu-id="c278a-163">Это так обновляет окно предварительного просмотра, чтобы он использует конкретной главной страницы или макет страницы, на котором вы работаете, что все, что вы страницы выбран для параметра **Страница изменения предварительного просмотра** в левом верхнем углу.</span><span class="sxs-lookup"><span data-stu-id="c278a-163">Doing so refreshes the preview so that it uses the specific master page or page layout that you're working on, and whatever page you've selected in the **Change Preview Page** option in the upper-left corner.</span></span>
  
    
    

## <a name="change-the-preview-page"></a><span data-ttu-id="c278a-164">Изменение страницы предварительного просмотра</span><span class="sxs-lookup"><span data-stu-id="c278a-164">Change the preview page</span></span>
<span data-ttu-id="c278a-165"><a name="ChangePreviewPage"> </a></span><span class="sxs-lookup"><span data-stu-id="c278a-165"></span></span>


### <a name="message"></a><span data-ttu-id="c278a-166">Message</span><span class="sxs-lookup"><span data-stu-id="c278a-166">Message</span></span>

 <span data-ttu-id="c278a-167">**В настоящее время для предварительного просмотра главной страницы (макет страницы) без контента. Из меню окна можно изменить страницу, которую вы находитесь в режиме просмотра.**</span><span class="sxs-lookup"><span data-stu-id="c278a-167">**You're currently previewing your master page (page layout) without any content. You can change the page you're previewing from the menu above.**</span></span>
  
    
    

### <a name="explanation"></a><span data-ttu-id="c278a-168">Объяснение</span><span class="sxs-lookup"><span data-stu-id="c278a-168">Explanation</span></span>

<span data-ttu-id="c278a-169">Это сообщение можно увидеть, если вы не используете live страницу SharePoint для предварительного просмотра главной странице или макету страницы.</span><span class="sxs-lookup"><span data-stu-id="c278a-169">You see this message when you aren't using a live SharePoint page with which to preview your master page or page layout.</span></span> <span data-ttu-id="c278a-170">Например если вы находитесь в режиме просмотра макета страницы, можно выберите **Страница изменения предварительного просмотра** в левом верхнем углу и затем выберите определенного контента страницы для предварительного просмотра с макетом страницы.</span><span class="sxs-lookup"><span data-stu-id="c278a-170">For example, if you're previewing a page layout, you can choose **Change Preview Page** in the upper-left corner, and then select a specific content page to preview with your page layout.</span></span> <span data-ttu-id="c278a-171">Таким образом, можно выполнить предварительный просмотр макет страницы с содержимым страниц в поля страницы.</span><span class="sxs-lookup"><span data-stu-id="c278a-171">This way, you can preview the page layout with actual page content in the page fields.</span></span> <span data-ttu-id="c278a-172">Если вы хотите предварительного просмотра для отображения только что положения **ContentPlaceHolderMain** или поля страницы, всегда можно использовать **Страница изменения предварительного просмотра** для возвращения универсальный предварительного просмотра.</span><span class="sxs-lookup"><span data-stu-id="c278a-172">If you want the preview to show just the positions of **ContentPlaceHolderMain** or page fields, you can always use **Change Preview Page** to switch back to a generic preview.</span></span>
  
    
    

## <a name="additional-resources"></a><span data-ttu-id="c278a-173">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="c278a-173">Additional resources</span></span>
<span data-ttu-id="c278a-174"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="c278a-174"></span></span>


-  [<span data-ttu-id="c278a-175">Разработка макета сайта в SharePoint</span><span class="sxs-lookup"><span data-stu-id="c278a-175">Develop the site design in SharePoint</span></span>](develop-the-site-design-in-sharepoint.md)
    
  
-  [<span data-ttu-id="c278a-176">Как изменить страницу предварительного просмотра в Дизайнере SharePoint</span><span class="sxs-lookup"><span data-stu-id="c278a-176">How to: Change the preview page in SharePoint Design Manager</span></span>](how-to-change-the-preview-page-in-sharepoint-design-manager.md)
    
  
-  [<span data-ttu-id="c278a-177">Фрагменты кода дизайнер SharePoint</span><span class="sxs-lookup"><span data-stu-id="c278a-177">SharePoint Design Manager snippets</span></span>](sharepoint-design-manager-snippets.md)
    
  

