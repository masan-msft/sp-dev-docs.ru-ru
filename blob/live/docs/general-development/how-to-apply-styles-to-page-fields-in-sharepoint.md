---
title: "Применение стилей к полям страницы в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: e227613d-0e4d-4312-924d-bb55e1fe4293
ms.openlocfilehash: 9804ef7fe338f668dd843f3c79c6a77d92310f17
ms.sourcegitcommit: f6ea922341c38e700d0697961f8df9a454a03cba
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/15/2017
---
# <a name="apply-styles-to-page-fields-in-sharepoint"></a><span data-ttu-id="703cf-102">Применение стилей к полям страницы в SharePoint</span><span class="sxs-lookup"><span data-stu-id="703cf-102">How to: Apply styles to page fields in SharePoint</span></span>
<span data-ttu-id="703cf-p101">В макете страницы можно применить стили для поля страницы, и эти стили, применяются к любое содержимое, добавленные в окончательную авторы контента при создании страницы из макета страницы. Кроме того вы имеют параметры для управления стилями содержимого в поле страницы RichHtmlField.</span><span class="sxs-lookup"><span data-stu-id="703cf-p101">In a page layout, you can apply styles to a page field, and those styles are applied to any content added by content authors when they create a page from that page layout. Also, you have further options to control how content in a RichHtmlField page field is styled.</span></span>
## <a name="introduction-to-applying-styles-to-page-fields"></a><span data-ttu-id="703cf-105">Общие сведения о применение стилей поля страниц</span><span class="sxs-lookup"><span data-stu-id="703cf-105">Introduction to applying styles to page fields</span></span>
<span data-ttu-id="703cf-106"><a name="Introduction"> </a></span><span class="sxs-lookup"><span data-stu-id="703cf-106"><a name="Introduction"> </a></span></span>

<span data-ttu-id="703cf-p102">Разработчик у вас есть полный контроль над расположения и стиля поля страниц на макет страницы и всех страниц, созданных в этом макете страницы. При авторы контента создавать страницы из браузера, нельзя перемещать поля страницы на странице или переопределяют стили, которые можно указать. Это гарантирует, что ваше фирменной символики читаемых через все страницы на сайте.</span><span class="sxs-lookup"><span data-stu-id="703cf-p102">As a designer, you have ultimate control over the positioning and styling of page fields on a page layout and on any pages created from that page layout. When content authors create pages from a browser, they can't move page fields on the page or override the styles that you specify. This helps to ensure that your branding remains consistent through all pages in the site.</span></span>
  
    
    
<span data-ttu-id="703cf-110">Существует две основные категории типов полей, которые следует учитывать применить стили для поля страницы.</span><span class="sxs-lookup"><span data-stu-id="703cf-110">When you apply styles to page fields, there are two basic categories of field types to consider:</span></span>
  
    
    

- <span data-ttu-id="703cf-p103">**Типы полей, отличные от RichHtmlField** Поля страниц, которые будут включены в макете страницы соответствует тип контента для макета страницы. В поле страницы может быть множество типов, таких как однострочного текста (текстовое поле) или многострочный текст (NoteField). Разработчик будут применяться стили для всех этих полей страницы таким же образом, с помощью стилей в поле страницы непосредственно в макет страницы.</span><span class="sxs-lookup"><span data-stu-id="703cf-p103">**Field types other than RichHtmlField** The page fields that make up a page layout conform to the content type for that page layout. A page field can be of many types, such as a Single Line of Text (TextField) or Multiple Lines of Text (NoteField). As a designer, you can apply styles to all of these page fields in the same way, by applying styles to the page field directly on the page layout.</span></span>
    
  
- <span data-ttu-id="703cf-p104">**RichHtmlField** Управления поля форматированного HTML (HTML публикации поле)  наиболее эффективные и часто используемых элементов управления в макеты страниц. По умолчанию в поле с расширенными возможностями HTML авторы контента используют ленты для форматирования и применения стилей к содержимому, а для вставки таблицы, мультимедиа, такие как изображения и видео- и веб-частей. Этот тип поля полезен, когда нужно предоставить возможность добавлять и стиля содержимого, которые можно управлять параметрами авторы контента. Можно управлять RichHtmlField двумя способами:</span><span class="sxs-lookup"><span data-stu-id="703cf-p104">**RichHtmlField** The rich HTML field control (also known as a Publishing HTML field) is one of the most powerful and frequently used controls in page layouts. By default, in a rich HTML field, content authors use the ribbon to format and apply styles to content, and to insert tables, media such as images and video, and Web Parts. This field type is useful when you want to give content authors the freedom to add and style content within parameters that you can control. You can control a RichHtmlField in two ways:</span></span>
    
  - <span data-ttu-id="703cf-p105">**Создание пользовательской таблицы стилей** По умолчанию стили, доступные на ленте RichHtmlField поступают из таблицы стилей с именем HtmlEditorStyles.css. Свойство **PrefixStyleSheet** в этом фрагменте можно настроить для отображения на ленте авторам использовать настраиваемые стили.</span><span class="sxs-lookup"><span data-stu-id="703cf-p105">**Create a custom style sheet** By default, the styles available on the ribbon of a RichHtmlField come from a style sheet named HtmlEditorStyles.css. You can configure the **PrefixStyleSheet** property for this snippet so that your own custom styles appear on the ribbon for content authors to use.</span></span>
    
  
  - <span data-ttu-id="703cf-p106">**Настройка свойств разрешить** Фрагмент кода для RichHtmlField имеет 28 доступные свойства, которые начинаются с **Allow**и сделать определенные команды или группы команд на ленте, становится недоступной для авторы содержимого можно использовать эти свойства. Например если значение свойства **AllowFontsMenu** **False**, авторы нельзя использовать меню «Шрифт» на ленте для изменения какие шрифта применяется к тексту; Вместо этого они могут использовать стили CSS, которые можно указать.</span><span class="sxs-lookup"><span data-stu-id="703cf-p106">**Configure the Allow properties** A snippet for a RichHtmlField has 28 available properties that start with **Allow**, and you can use these properties to make specific commands or groups of commands on the ribbon unavailable to content authors. For example, if you set the **AllowFontsMenu** property to **False**, authors cannot use the Font menu on the ribbon to change what font is applied to text; instead, they can use only the CSS styles that you specify.</span></span>
    
  
<span data-ttu-id="703cf-p107">Для всех типов полей страницы, включая RichHtmlField конструкторе определяет, как содержимое со стилями. RichHtmlField можно использовать для предоставления авторы контента свободу действий для вставки Форматированный контент и применения стилей; по-прежнему имеет полный контроль над можно добавлять содержимое и стили, что может применяться.</span><span class="sxs-lookup"><span data-stu-id="703cf-p107">For all types of page fields, including the RichHtmlField, the designer determines how the content is styled. You can use the RichHtmlField to give content authors the freedom to insert rich content and apply styles; you still have ultimate control over what content can be added and what styles can be applied.</span></span>
  
    
    

## <a name="applying-styles-to-page-fields-other-than-richhtmlfield"></a><span data-ttu-id="703cf-124">Применение стилей к поля страниц, отличный от RichHtmlField</span><span class="sxs-lookup"><span data-stu-id="703cf-124">Applying styles to page fields other than RichHtmlField</span></span>
<span data-ttu-id="703cf-125"><a name="Applying"> </a></span><span class="sxs-lookup"><span data-stu-id="703cf-125"><a name="Applying"> </a></span></span>

<span data-ttu-id="703cf-p108">С помощью элемента управления поля страницы можно определить стили, используемые контента. Авторы могут добавить содержимое на страницу, но конструктора элементов управления, как этот контент визуализируется с помощью CSS применяется для этих элементов управления.</span><span class="sxs-lookup"><span data-stu-id="703cf-p108">With a page field control, you can define the styles used by the content. Authors can add content to a page, but the designer controls how that content is rendered through CSS applied to those controls.</span></span>
  
    
    
<span data-ttu-id="703cf-128">В разметке страницы HTML каждое поле страницы заключено в тег **\<div\>**.</span><span class="sxs-lookup"><span data-stu-id="703cf-128">In the HTML page layout, each page field is wrapped in a **\<div\>** tag.</span></span> <span data-ttu-id="703cf-129">Чтобы применить стиль к полю страницы, вы можете просто добавить стиль к тегу **\<div\>**, например `<div style="font-weight:bold"`.</span><span class="sxs-lookup"><span data-stu-id="703cf-129">To apply a style to a page field, you can simply add a style to the **\<div\>**—for example,  `<div style="font-weight:bold"`.</span></span> <span data-ttu-id="703cf-130">Однако более распространенный и удобный способ — добавление атрибута **id** в тег **\<div\>** для каждого поля страницы в разметке с последующим использованием атрибута **id** для выбора стилей во внешней таблице стилей.</span><span class="sxs-lookup"><span data-stu-id="703cf-130">But the more common and useful scenario is that you add an **id** attribute to the **\<div\>** for each page field in the page layout, and then use the **id** as a selector for styles that reside in an external style sheet.</span></span> <span data-ttu-id="703cf-131">Таким образом, если у вас есть несколько каналов устройств, а у каждого канала есть своя таблица стилей, вы можете применить разные стили к каждому полю страницы для каждого канала.</span><span class="sxs-lookup"><span data-stu-id="703cf-131">This way, if you have multiple device channels, and each channel has its own style sheet, you can apply different styles to each page field for each channel.</span></span> <span data-ttu-id="703cf-132">Например, приведенное ниже поле страницы типа TextField (другое название — "Многострочный текст") может содержать только атрибут **id** в теге **\<div\>**.</span><span class="sxs-lookup"><span data-stu-id="703cf-132">For example, the following page field of the type TextField (also called Multiple Lines of Text) might have only an **id** attribute on the **\<div\>** tag.</span></span>
  
    
    



```HTML

<div id="ShortSummaryPageField">
<!--CS: Start Page Field: ShortSummary Snippet-->
<!--SPM:<%@Register Tagprefix="PageFieldNoteField" Namespace="Microsoft.SharePoint.WebControls" Assembly="Microsoft.SharePoint, Version=15.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"%>-->
<!--MS:<PageFieldNoteField:NoteField FieldName="a5249942-2dc5-4917-85e2-661d019ad548" runat="server">-->
<!--PS: Start of READ-ONLY PREVIEW (do not modify)--><div align="left" class="ms-formfieldcontainer"><div class="ms-formfieldlabelcontainer" nowrap="nowrap"><span class="ms-formfieldlabel" nowrap="nowrap">ShortSummary</span></div><div class="ms-formfieldvaluecontainer"><div class="ms-rtestate-field">ShortSummary field value.</div></div></div><!--PE: End of READ-ONLY PREVIEW-->
<!--ME:</PageFieldNoteField:NoteField>-->
<!--CE: End Page Field: ShortSummary Snippet-->
</div>
```

<span data-ttu-id="703cf-133">Дополнительные сведения о котором должен приходить стили и ссылки на стиль для макета страницы содержатся в разделе  [Инструкции. Создание макета страницы в SharePoint](how-to-create-a-page-layout-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="703cf-133">For more information about where styles and style references for a page layout should go, see  [How to: Create a page layout in SharePoint](how-to-create-a-page-layout-in-sharepoint.md).</span></span>
  
    
    

## <a name="disabling-options-on-the-ribbon-of-a-richhtmlfield"></a><span data-ttu-id="703cf-134">Отключение параметров на ленте RichHtmlField</span><span class="sxs-lookup"><span data-stu-id="703cf-134">Disabling options on the ribbon of a RichHtmlField</span></span>
<span data-ttu-id="703cf-135"><a name="Disabling"> </a></span><span class="sxs-lookup"><span data-stu-id="703cf-135"><a name="Disabling"> </a></span></span>

<span data-ttu-id="703cf-136">Когда авторы контента создать или изменить страницу и добавлять содержимое RichHtmlField, с помощью браузера, их можно использовать команды на ленте для этого поля для форматирования стиля, или вставки Форматированный контент и мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="703cf-136">When content authors create or edit a page and then add content to a RichHtmlField using a browser, they can use commands on the ribbon for that field to format, style, or insert rich content and media.</span></span> 
  
    
    
<span data-ttu-id="703cf-p110">В коллекция фрагментов кода можно настроить свойства поля страницы типа RichHtmlField, таким образом, чтобы определенные команды или группы команд на ленте, становятся недоступными для авторов. К примеру задав свойство **AllowFontSizesMenu** **False**, можно отключить **Font Size** меню ленты. Свойства **AllowFonts** значение **False**, можно отключить всей группы **шрифта** на ленте.</span><span class="sxs-lookup"><span data-stu-id="703cf-p110">In the Snippet Gallery, you can configure the properties of a page field of the type RichHtmlField, so that specific commands or groups of commands on the ribbon are made unavailable to authors. For example, by setting the **AllowFontSizesMenu** property to **False**, you can disable the **Font Size** menu on the ribbon. By setting the **AllowFonts** property to **False**, you can disable the entire **Font** group on the ribbon.</span></span>
  
    
    
<span data-ttu-id="703cf-140">После настройки этих свойств в коллекция фрагментов кода и затем обновить фрагмента в разметке фрагмент внутри комментария  `<!--MS:>` отображаются свойства.</span><span class="sxs-lookup"><span data-stu-id="703cf-140">After you configure these properties in the Snippet Gallery and then update the snippet, the properties appear in the snippet markup inside the  `<!--MS:>` comment.</span></span>
  
    
    



```HTML

<div data-name="Page Field: ArticleBody">
<!--CS: Start Page Field: ArticleBody Snippet-->
<!--SPM:<%@Register Tagprefix="PageFieldRichHtmlField" Namespace="Microsoft.SharePoint.Publishing.WebControls" Assembly="Microsoft.SharePoint.Publishing, Version=15.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"%>-->
<!--MS:<PageFieldRichHtmlField:RichHtmlField runat="server" AllowFonts="False" FieldName="db3168db-8778-4fb6-a48f-57f598497388">-->
<!--PS: Start of READ-ONLY PREVIEW (do not modify)--><div id="ctl02_label" style="display:none">ArticleBody</div><div id="ctl02__ControlWrapper_RichHtmlField" class="ms-rtestate-field" style="display:inline" aria-labelledby="ctl02_label"><div align="left" class="ms-formfieldcontainer"><div class="ms-formfieldlabelcontainer" nowrap="nowrap"><span class="ms-formfieldlabel" nowrap="nowrap">ArticleBody</span></div><div class="ms-formfieldvaluecontainer"><div class="ms-rtestate-field">ArticleBody field value. Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.</div></div></div></div>
<!--PE: End of READ-ONLY PREVIEW-->
<!--ME:</PageFieldRichHtmlField:RichHtmlField>-->
<!--CE: End Page Field: ArticleBody Snippet-->
</div>
```


> <span data-ttu-id="703cf-141">**Примечание.** Если задать для атрибута **AllowFonts** значение **False**, создатели контента по-прежнему смогут использовать такие сочетания клавиш, как CTRL+B (жирный шрифт), для форматирования текста.</span><span class="sxs-lookup"><span data-stu-id="703cf-141">**Note:** If you set **AllowFonts** to **False**, content authors can still use keyboard shortcuts such as CTRL+B (strong) to format text.</span></span> <span data-ttu-id="703cf-142">Чтобы авторы не могли добавлять к тексту стили, вы можете задать для атрибута **AllowTextMarkup** значение **False**.</span><span class="sxs-lookup"><span data-stu-id="703cf-142">To prevent authors from adding any styles to text, you can set **AllowTextMarkup** to **False**.</span></span> <span data-ttu-id="703cf-143">В этом случае, когда автор пытается сохранить контент, где к тексту применены стили, редактор HTML в браузере возвращает ошибку и предлагает автору удалить недопустимую разметку.</span><span class="sxs-lookup"><span data-stu-id="703cf-143">With this setting, when content authors attempt to save content that contains styles applied to text, the HTML editor in the browser returns an error and prompts the author to remove the markup that is not valid.</span></span> 
  
    
    

<span data-ttu-id="703cf-p112">В поле страницы RichHtmlField содержит 28 различных **Allow** свойства. Дополнительные сведения о какой элемент управления определенных свойств [Свойства RichHtmlField](http://msdn.microsoft.com/ru-RU/library/microsoft.sharepoint.publishing.webcontrols.richhtmlfield_properties) более подробные сведения добавлении и настройке фрагменты кода, посмотрите [Фрагменты кода дизайнер SharePoint](sharepoint-design-manager-snippets.md).</span><span class="sxs-lookup"><span data-stu-id="703cf-p112">A RichHtmlField page field contains 28 different **Allow** properties. For more information about what specific properties control, see [RichHtmlField properties](http://msdn.microsoft.com/ru-RU/library/microsoft.sharepoint.publishing.webcontrols.richhtmlfield_properties) For more information about adding and configuring snippets, see [SharePoint Design Manager snippets](sharepoint-design-manager-snippets.md).</span></span>
  
    
    

## <a name="controlling-the-styles-available-in-a-richhtmlfield"></a><span data-ttu-id="703cf-146">Управление стили, доступные в RichHtmlField</span><span class="sxs-lookup"><span data-stu-id="703cf-146">Controlling the styles available in a RichHtmlField</span></span>
<span data-ttu-id="703cf-147"><a name="Controlling"> </a></span><span class="sxs-lookup"><span data-stu-id="703cf-147"><a name="Controlling"> </a></span></span>

<span data-ttu-id="703cf-p113">В RichHtmlField авторы контента можно использовать параметры на ленте на форматирование содержимого. Эти параметры форматирования реализуются с помощью CSS и эти стили, определяются в таблицы стилей SharePoint, с именем HtmlEditorStyles.css, который находится на сервере в одном из следующих расположений:</span><span class="sxs-lookup"><span data-stu-id="703cf-p113">In a RichHtmlField, content authors can use options on the ribbon to format content. These formatting options are implemented by using CSS, and these styles are defined in a SharePoint style sheet named HtmlEditorStyles.css that resides on the server at one of the following locations:</span></span>
  
    
    

- <span data-ttu-id="703cf-150">C:\\Program Files\\Common Files\\Microsoft Shared\\Web Server Extensions\\15\\TEMPLATE\\LAYOUTS\\1033\\STYLES</span><span class="sxs-lookup"><span data-stu-id="703cf-150">C:\\Program Files\\Common Files\\Microsoft Shared\\Web Server Extensions\\15\\TEMPLATE\\LAYOUTS\\1033\\STYLES</span></span> 
    
  
- <span data-ttu-id="703cf-151">C:\\Program Files\\Common Files\\Microsoft Shared\\Web Server Extensions\\15\\TEMPLATE\\FEATURES\\PublishingLayouts\\en-"мне нравится"</span><span class="sxs-lookup"><span data-stu-id="703cf-151">C:\\Program Files\\Common Files\\Microsoft Shared\\Web Server Extensions\\15\\TEMPLATE\\FEATURES\\PublishingLayouts\\en-us</span></span>
    
  
<span data-ttu-id="703cf-p114">Так как RichHtmlField в браузере используется для реализации его стили CSS, можно создать собственные стили, которые совместимы с использованием фирменной символики сайта и затем вы можете предоставить эти стили на ленте для авторы контента для использования. Чтобы внесены незначительные изменения стилей по умолчанию, можно скопировать существующий стиль из HtmlEditorStyles.css таблицы стилей, на который ссылается макет страницы и измените стиля с помощью изменения свойства CSS и значения (но не "Выбор"). Также можно скрыть стили по умолчанию из ленты, скопировав вашей таблицы стилей, а затем параметр  `display:none`.</span><span class="sxs-lookup"><span data-stu-id="703cf-p114">Because the RichHtmlField in the browser uses CSS to implement its styles, you can create your own styles that are consistent with the branding of your site, and then you can make those styles available on the ribbon for content authors to use. To make minor changes to the default styles, you can copy an existing style from HtmlEditorStyles.css to your style sheet that is referenced by the page layout, and then modify that style by changing the CSS properties and values (but not the selector). You can also hide default styles from the ribbon by copying them to your style sheet and then setting  `display:none`.</span></span>
  
    
    
<span data-ttu-id="703cf-p115">Чтобы реализовать настраиваемые стили, вы также создавать таблицы стилей с нуля путем изменения свойства **PrefixStyleSheet** для фрагмента RichHtmlField. По умолчанию это свойство имеет значение **ms-rte**и стилей в таблицу стилей по умолчанию HtmlEditorStyles.css каждого начинаются с данного префикса  например:</span><span class="sxs-lookup"><span data-stu-id="703cf-p115">To implement custom styles, you can also build a style sheet from scratch by changing the **PrefixStyleSheet** property for the RichHtmlField snippet. By default, this property is set to **ms-rte**, and the styles in the default style sheet HtmlEditorStyles.css each begin with this prefix—for example:</span></span>
  
    
    



```HTML

H1. ms-rteElement-H1
{
-ms-name:"Heading 1";
-ms-element:"true";
}
```

<span data-ttu-id="703cf-p116">При изменении значения свойства **PrefixStyleSheet** существующих стилей **ms-rte** нет в полнофункциональный редактор HTML и авторы контента доступны только стили, которые вы создаете, использующие новый префикс. Это означает, что если вы хотите использовать часть стилей по умолчанию, их необходимо скопировать в таблице стилей и изменения, чтобы они использовали новый префикс.</span><span class="sxs-lookup"><span data-stu-id="703cf-p116">When you change the value of the **PrefixStyleSheet** property, none of the existing **ms-rte** styles are available in the rich HTML editor, and only styles that you create that use the new prefix are available to content authors. This means if you want to use some of the default styles, they must be copied to your style sheet and modified so that they use the new prefix.</span></span>
  
    
    

> <span data-ttu-id="703cf-159">**Примечание.** Свойство **PrefixStyleSheet** определяется для каждого поля страницы RichHtmlField, но в нескольких полях страницы для этого свойства может быть задано одно и то же значение.</span><span class="sxs-lookup"><span data-stu-id="703cf-159">**Note:** The **PrefixStyleSheet** property is defined per each RichHtmlField page field, but multiple page fields can use the same value for this property.</span></span> <span data-ttu-id="703cf-160">Таким образом, если несколько макетов страниц ссылаются на одну и ту же таблицу стилей, то несколько полей RichHtmlField в этих макетах могут содержать один и тот же префикс стиля и ссылаться на одни и те же стили.</span><span class="sxs-lookup"><span data-stu-id="703cf-160">So, if multiple page layouts reference the same style sheet, it's possible for multiple RichHtmlFields on those page layouts to have the same style prefix and reference the same styles.</span></span>
  
    
    


### <a name="to-define-a-new-list-of-styles-for-a-richhtmlfield"></a><span data-ttu-id="703cf-161">Определение нового списка стилей для объекта RichHtmlField</span><span class="sxs-lookup"><span data-stu-id="703cf-161">To define a new list of styles for a RichHtmlField</span></span>


1. <span data-ttu-id="703cf-162">Перейдите на сайт публикации.</span><span class="sxs-lookup"><span data-stu-id="703cf-162">Browse to your publishing site.</span></span>
    
  
2. <span data-ttu-id="703cf-163">В правом верхнем углу страницы выберите пункт **Параметры**, а затем выберите **Дизайнер**.</span><span class="sxs-lookup"><span data-stu-id="703cf-163">In the upper-right corner of the page, choose **Settings**, and then choose **Design Manager**.</span></span>
    
  
3. <span data-ttu-id="703cf-164">В Дизайнере в левой области панели навигации выберите команду **Изменить макеты страниц**.</span><span class="sxs-lookup"><span data-stu-id="703cf-164">In Design Manager, in the left navigation pane, choose **Edit Page Layouts**.</span></span>
    
  
4. <span data-ttu-id="703cf-165">Выберите макет страницы, на котором будет находиться в поле страницы RichHtmlField.</span><span class="sxs-lookup"><span data-stu-id="703cf-165">Choose the page layout on which the RichHtmlField page field will reside.</span></span>
    
  
5. <span data-ttu-id="703cf-166">В правом верхнем углу preview на сервере выберите **Коллекция фрагментов кода**.</span><span class="sxs-lookup"><span data-stu-id="703cf-166">In the upper-right corner of the server-side preview, choose **Snippet Gallery**.</span></span>
    
  
6. <span data-ttu-id="703cf-167">На ленте выберите **Поля страниц** и выберите поле страницы типа **RichHtmlField**.</span><span class="sxs-lookup"><span data-stu-id="703cf-167">On the ribbon, choose **Page Fields**, and then choose a page field of the type **RichHtmlField**.</span></span>
    
  
7. <span data-ttu-id="703cf-168">В сетке свойств разверните раздел **Разное** и затем измените свойство **PrefixStyleSheet** значение, отличное от **ms-rte** например, измените значение, которое должно **customstyle**.</span><span class="sxs-lookup"><span data-stu-id="703cf-168">In the property grid, expand the **Misc** section, and then change the **PrefixStyleSheet** property to a value other than **ms-rte**—for example, change the value to be **customstyle**.</span></span>
    
    > <span data-ttu-id="703cf-169">**Важно!** Значение этого свойства должно быть целиком представлено в нижнем регистре.</span><span class="sxs-lookup"><span data-stu-id="703cf-169">**Important:** This property value must be all lowercase.</span></span> 
8. <span data-ttu-id="703cf-170">Нажмите **Обновить**.</span><span class="sxs-lookup"><span data-stu-id="703cf-170">Choose **Update**.</span></span>
    
  
9. <span data-ttu-id="703cf-171">В левой части коллекция фрагментов кода выберите команду **Копировать в буфер обмена**.</span><span class="sxs-lookup"><span data-stu-id="703cf-171">On the left side of the Snippet Gallery, choose **Copy to Clipboard**.</span></span>
    
  
10. <span data-ttu-id="703cf-172">На сопоставленном сетевом диске на компьютере откройте макет HTML-страницы в редакторе HTML.</span><span class="sxs-lookup"><span data-stu-id="703cf-172">In the mapped network drive on your computer, open the HTML page layout in your HTML editor.</span></span>
    
    > <span data-ttu-id="703cf-173">**Примечание.** Дополнительные сведения см. в статье [Инструкции. Сопоставление сетевого диска с коллекцией эталонных страниц SharePoint](how-to-map-a-network-drive-to-the-sharepoint-master-page-gallery.md).</span><span class="sxs-lookup"><span data-stu-id="703cf-173">**Note:** For more information, see  [How to: Map a network drive to the SharePoint Master Page Gallery](how-to-map-a-network-drive-to-the-sharepoint-master-page-gallery.md).</span></span> 
11. <span data-ttu-id="703cf-174">В макете HTML-страницы вставьте фрагмент кода HTML в разделе **PlaceHolderMain**.</span><span class="sxs-lookup"><span data-stu-id="703cf-174">In the HTML page layout, paste the HTML snippet inside **PlaceHolderMain**.</span></span>
    
  
12. <span data-ttu-id="703cf-p118">Сохраните макет страницы HTML. Макет страницы связанного .aspx синхронизации изменений в HTML-файл.</span><span class="sxs-lookup"><span data-stu-id="703cf-p118">Save the HTML page layout. The changes to the HTML file are synced to the associated .aspx page layout.</span></span>
    
    <span data-ttu-id="703cf-177">На этом этапе Если автор создает или изменяет страница, основанная на этот макет страницы, без стилей доступны на ленте в редакторе HTML, так как это поле определенных параметров страницы используется только стили, начинающихся с новой префикс **customstyle**, но эти стили еще не определен.</span><span class="sxs-lookup"><span data-stu-id="703cf-177">At this point, if a content author creates or edits a page based on this page layout, no styles are available on the ribbon of the HTML editor because this specific page field uses only styles that begin with the new prefix **customstyle**, but those styles have not yet been defined.</span></span>
    
  
13. <span data-ttu-id="703cf-178">На сервере перейдите к следующей папке и откройте HtmlEditorStyles.css:</span><span class="sxs-lookup"><span data-stu-id="703cf-178">On the server, browse to the following location and open HtmlEditorStyles.css:</span></span>
    
    <span data-ttu-id="703cf-179">C:\\Program Files\\Common Files\\Microsoft Shared\\Web Server Extensions\\15\\TEMPLATE\\LAYOUTS\\1033\\STYLES</span><span class="sxs-lookup"><span data-stu-id="703cf-179">C:\\Program Files\\Common Files\\Microsoft Shared\\Web Server Extensions\\15\\TEMPLATE\\LAYOUTS\\1033\\STYLES</span></span>
    
    <span data-ttu-id="703cf-p119">Полезно для просмотра стилей по умолчанию, понимать, как они записываются в случае и возможно повторно использовать некоторые из них копировать их в таблице стилей и их изменение. После этого замените префикс по умолчанию **ms-rte** свои собственные префикса.</span><span class="sxs-lookup"><span data-stu-id="703cf-p119">It's useful to view the default styles, understand how they're written, and possibly reuse some of them by copying them to your style sheet and then modifying them. If you do this, replace the default **ms-rte** prefix with your own prefix.</span></span>
    
    > <span data-ttu-id="703cf-182">**Важно!** Не меняйте используемую по умолчанию таблицу стилей HtmlEditorStyles.css.</span><span class="sxs-lookup"><span data-stu-id="703cf-182">**Important:** Do not modify the default style sheet, HtmlEditorStyles.css.</span></span> <span data-ttu-id="703cf-183">Она предоставляет стили для каждого объекта RichHtmlField в ферме.</span><span class="sxs-lookup"><span data-stu-id="703cf-183">This style sheet provides styles for every RichHtmlField in the farm.</span></span> <span data-ttu-id="703cf-184">Кроме того, при обновлении служб или установке новой версии этот файл может быть перезаписан, что приведет к потере всех изменений.</span><span class="sxs-lookup"><span data-stu-id="703cf-184">Also, service updates or an upgrade may overwrite this file, causing you to lose any changes.</span></span> 
14. <span data-ttu-id="703cf-185">Создайте в таблице стилей список новых стилей с новым префиксом.</span><span class="sxs-lookup"><span data-stu-id="703cf-185">In your style sheet, create a list of new styles that start with the new prefix.</span></span>
    
    <span data-ttu-id="703cf-186">Например если **customstyle** новый префикс, таблицы стилей может содержать следующий стиль.</span><span class="sxs-lookup"><span data-stu-id="703cf-186">For example, if **customstyle** is the new prefix, your style sheet might contain the following style.</span></span>
    


```HTML
  
H2.customstyleElement-H2
{
-ms-name:"Heading 2";
-ms-element:"true";
}
customstyleElement-H2
{
font-weight: bold;
font-family: Cambria;
font-size: 16pt;
} 

```


    For clarity, the class name and the name of the style as it appears on the ribbon are defined separately from the style properties. In this example, **H2** is the element selector for the style, and **customstyleElement-H2** is the class name of the style. The class name has two parts: **customstyle** is the prefix that you specified for this page field, and **Element** specifies that this style will appear in the **Page Elements** section of the **Styles** gallery on the ribbon of the HTML editor. The **-ms-name** property sets the display name that appears to content authors in the Styles gallery.
    
    SharePoint maps a style to a menu or command on the ribbon by parsing the class name immediately after the prefix and looking for one of these strings:
    
  - <span data-ttu-id="703cf-187">**Element**: раздел элементы страниц из коллекции стилей</span><span class="sxs-lookup"><span data-stu-id="703cf-187">**Element**: The Page Elements section of the Styles gallery</span></span>
    
  
  - <span data-ttu-id="703cf-188">**Style**: раздел стили текста из коллекции стилей</span><span class="sxs-lookup"><span data-stu-id="703cf-188">**Style**: The Text Styles section of the Styles gallery</span></span>
    
  
  - <span data-ttu-id="703cf-189">**FontSize**: размер шрифта меню</span><span class="sxs-lookup"><span data-stu-id="703cf-189">**FontSize**: The Font Size menu</span></span>
    
  
  - <span data-ttu-id="703cf-190">**ThemeFontFace**: меню "Шрифт"</span><span class="sxs-lookup"><span data-stu-id="703cf-190">**ThemeFontFace**: The Font menu</span></span>
    
  
  - <span data-ttu-id="703cf-191">**ForeColor**: меню Цвет шрифта</span><span class="sxs-lookup"><span data-stu-id="703cf-191">**ForeColor**: The Font Color menu</span></span>
    
  
  - <span data-ttu-id="703cf-192">**BackColor**: выделение цветом меню</span><span class="sxs-lookup"><span data-stu-id="703cf-192">**BackColor**: The Highlight Color menu</span></span>
    
  
  - <span data-ttu-id="703cf-193">**Image**: меню "изображение"</span><span class="sxs-lookup"><span data-stu-id="703cf-193">**Image**: The Image menu</span></span>
    
  
  - <span data-ttu-id="703cf-194">**Table**: меню таблицы</span><span class="sxs-lookup"><span data-stu-id="703cf-194">**Table**: The Table menu</span></span>
    
  
  - <span data-ttu-id="703cf-195">**Position**: выравнивание кнопок в группе абзаца</span><span class="sxs-lookup"><span data-stu-id="703cf-195">**Position**: The Align buttons in the Paragraph group</span></span>
    
  

    <span data-ttu-id="703cf-196">Дополнительные сведения о котором должно находиться стили для макета страницы содержатся в разделе  [Инструкции. Создание макета страницы в SharePoint](how-to-create-a-page-layout-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="703cf-196">For more information about where styles for a page layout should reside, see  [How to: Create a page layout in SharePoint](how-to-create-a-page-layout-in-sharepoint.md).</span></span>
    
  

## <a name="additional-resources"></a><span data-ttu-id="703cf-197">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="703cf-197">Additional resources</span></span>
<span data-ttu-id="703cf-198"><a name="Additional"> </a></span><span class="sxs-lookup"><span data-stu-id="703cf-198"><a name="Additional"> </a></span></span>


-  [<span data-ttu-id="703cf-199">Обзор Дизайнера в SharePoint</span><span class="sxs-lookup"><span data-stu-id="703cf-199">Overview of Design Manager in SharePoint</span></span>](overview-of-design-manager-in-sharepoint.md)
    
  
-  [<span data-ttu-id="703cf-200">Инструкции. Создание макета страницы в SharePoint</span><span class="sxs-lookup"><span data-stu-id="703cf-200">How to: Create a page layout in SharePoint</span></span>](how-to-create-a-page-layout-in-sharepoint.md)
    
  
-  [<span data-ttu-id="703cf-201">Фрагменты кода дизайнер SharePoint</span><span class="sxs-lookup"><span data-stu-id="703cf-201">SharePoint Design Manager snippets</span></span>](sharepoint-design-manager-snippets.md)
    
  

