---
title: "Как сделать настраиваемые CSS-файлы тем в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: b8c82c77-c836-47f9-a11e-6c9c656d436b
ms.openlocfilehash: 24d22d47c8c53b0aeb33a14bef989ab3138a06f8
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-make-custom-css-files-themable-in-sharepoint"></a><span data-ttu-id="f6d98-102">Как: сделать настраиваемые CSS-файлы тем в SharePoint</span><span class="sxs-lookup"><span data-stu-id="f6d98-102">How to: Make custom CSS files themable in SharePoint</span></span>
<span data-ttu-id="f6d98-103">Узнайте, как добавьте разметку комментарий стилей CSS-файл, чтобы его можно использовать в модуле темы SharePoint.</span><span class="sxs-lookup"><span data-stu-id="f6d98-103">Learn how to add comment-style markup to a CSS file so that it can be used in the SharePoint theming engine.</span></span>
## <a name="introduction-to-annotations"></a><span data-ttu-id="f6d98-104">Общие сведения о аннотаций</span><span class="sxs-lookup"><span data-stu-id="f6d98-104">Introduction to annotations</span></span>
<span data-ttu-id="f6d98-105"><a name="Intro"> </a></span><span class="sxs-lookup"><span data-stu-id="f6d98-105"></span></span>

<span data-ttu-id="f6d98-106">Примечания, разметку специальные стиль комментариев, сообщают engine темы SharePoint как свойства темы в CSS-файл.</span><span class="sxs-lookup"><span data-stu-id="f6d98-106">Annotations are special comment-style markup that tell the SharePoint theming engine how to theme properties in a CSS file.</span></span> <span data-ttu-id="f6d98-107">При применении темы к сайту engine темы заменяет значения свойств CSS значения соответствующие темы.</span><span class="sxs-lookup"><span data-stu-id="f6d98-107">When a theme is applied to a site, the theming engine replaces the CSS property values with the appropriate theme values.</span></span> <span data-ttu-id="f6d98-108">В SharePoint можно использовать примечания для изменения цвета, шрифта и фонового изображения.</span><span class="sxs-lookup"><span data-stu-id="f6d98-108">In SharePoint, you can use annotations to change the color, font, or background image.</span></span> <span data-ttu-id="f6d98-109">Можно также изменить цвет изображения.</span><span class="sxs-lookup"><span data-stu-id="f6d98-109">You can also recolor an image.</span></span> <span data-ttu-id="f6d98-110">При использовании настраиваемого CSS-файлы, если вы хотите использовать их с помощью механизма темы SharePoint необходимо добавить эти аннотации CSS-файлы.</span><span class="sxs-lookup"><span data-stu-id="f6d98-110">If you are using custom CSS files, you must add these annotations to the CSS files if you want to use them with the SharePoint theming engine.</span></span> <span data-ttu-id="f6d98-111">Если применить тему для сайта, использующего настраиваемые CSS-файлы, и вы не добавили аннотации, свойства CSS не изменяются.</span><span class="sxs-lookup"><span data-stu-id="f6d98-111">If you apply a theme to a site that uses custom CSS files, and you haven't added annotations, the CSS properties remain unchanged.</span></span> <span data-ttu-id="f6d98-112">Это может привести к сайтом с несоответствие разработки.</span><span class="sxs-lookup"><span data-stu-id="f6d98-112">This can result in a site that has a mismatched design.</span></span>
  
    
    
<span data-ttu-id="f6d98-113">В этой статье описываются доступные заметки и регистрация CSS-файлы.</span><span class="sxs-lookup"><span data-stu-id="f6d98-113">This article describes the available annotations and how to register CSS files.</span></span>
  
    
    
<span data-ttu-id="f6d98-114">Дополнительные сведения о пользовательских тем можно [как: развернуть пользовательской темы в SharePoint](how-to-deploy-a-custom-theme-in-sharepoint.md) и [как: создать файл предварительного просмотра главной страницы в SharePoint](how-to-create-a-master-page-preview-file-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="f6d98-114">For more information about custom themes, see  [How to: Deploy a custom theme in SharePoint](how-to-deploy-a-custom-theme-in-sharepoint.md) and [How to: Create a master page preview file in SharePoint](how-to-create-a-master-page-preview-file-in-sharepoint.md).</span></span>
  
    
    

## <a name="add-annotations-to-custom-css-files"></a><span data-ttu-id="f6d98-115">Добавлять примечания к настраиваемые CSS-файлы</span><span class="sxs-lookup"><span data-stu-id="f6d98-115">Add annotations to custom CSS files</span></span>
<span data-ttu-id="f6d98-116"><a name="annotations"> </a></span><span class="sxs-lookup"><span data-stu-id="f6d98-116"></span></span>

<span data-ttu-id="f6d98-p102">Заметки сообщить engine темы SharePoint как свойства темы в CSS-файл. В этом разделе описываются доступные заметки и как их использовать.</span><span class="sxs-lookup"><span data-stu-id="f6d98-p102">Annotations tell the SharePoint theming engine how to theme properties in a CSS file. This section describes the available annotations and how they can be used.</span></span>
  
    
    

### <a name="replacecolor-annotation"></a><span data-ttu-id="f6d98-119">ReplaceColor заметки</span><span class="sxs-lookup"><span data-stu-id="f6d98-119">ReplaceColor annotation</span></span>
<span data-ttu-id="f6d98-120"><a name="replaceColor"> </a></span><span class="sxs-lookup"><span data-stu-id="f6d98-120"></span></span>

<span data-ttu-id="f6d98-p103">Заметки **ReplaceColor** заменяет значение цвета цвет указанного темы. Его можно использовать со свойствами CSS, которые определяют значения цвета, такие как **color**, **background-color**, **border** и т. д.</span><span class="sxs-lookup"><span data-stu-id="f6d98-p103">The **ReplaceColor** annotation replaces the color value with the specified theme color. It can be used with CSS properties that define a color value, such as **color**, **background-color**, **border**, and so on.</span></span>
  
    
    
<span data-ttu-id="f6d98-123">Ниже приводится формат **ReplaceColor** заметки.</span><span class="sxs-lookup"><span data-stu-id="f6d98-123">The following shows the format for the **ReplaceColor** annotation.</span></span>
  
    
    



```

/* [ReplaceColor(themeColor:"ColorSlot"[, themeShade:"ShadeValue"][, themeTint:"TintValue"][, opacity:"OpacityValue"])] */

```

<span data-ttu-id="f6d98-124">Замените _ColorSlot_ имя заметки разъем цвет для использования.</span><span class="sxs-lookup"><span data-stu-id="f6d98-124">Replace  _ColorSlot_ with the annotation name of the color slot to use.</span></span> <span data-ttu-id="f6d98-125">Чтобы просмотреть список доступных разъемов разделу, посвященному [разъем сопоставление цветов](color-palettes-and-fonts-in-sharepoint.md#colorSlots) [палитры цветов и шрифтов в SharePoint](color-palettes-and-fonts-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="f6d98-125">To see a list of available color slots, see the [Color slot mapping](color-palettes-and-fonts-in-sharepoint.md#colorSlots) section in [Color palettes and fonts in SharePoint](color-palettes-and-fonts-in-sharepoint.md).</span></span>
  
    
    
<span data-ttu-id="f6d98-p105">Используйте параметр необязательно **themeShade**, если вы хотите затемнить цвет темы. Замените _ShadeValue_ числовое значение от 0,0 (без изменений) для версии 1.0 (самый темный).</span><span class="sxs-lookup"><span data-stu-id="f6d98-p105">Use the optional **themeShade** parameter if you want to darken the theme color. Replace _ShadeValue_ with a numeric value from 0.0 (no change) to 1.0 (darkest).</span></span>
  
    
    
<span data-ttu-id="f6d98-p106">Используйте параметр необязательно **themeTint**, если вы хотите осветлить цвет темы. Замените _TintValue_ числовое значение от 0,0 (без изменений) для версии 1.0 (очень светлый).</span><span class="sxs-lookup"><span data-stu-id="f6d98-p106">Use the optional **themeTint** parameter if you want to lighten the theme color. Replace _TintValue_ with a numeric value from 0.0 (no change) to 1.0 (lightest).</span></span>
  
    
    
<span data-ttu-id="f6d98-p107">Используйте параметр необязательно **opacity**, если вы хотите задать непрозрачность цвет темы. Замените _OpacityValue_ числовое значение, указывающее, непрозрачность. Непрозрачность параметр в диапазоне от 0.0 (полностью прозрачный) до 1.0 (полная непрозрачность).</span><span class="sxs-lookup"><span data-stu-id="f6d98-p107">Use the optional **opacity** parameter if you want to specify the opacity of the theme color. Replace _OpacityValue_ with a numeric value that specifies the opacity setting. The opacity setting ranges from 0.0 (fully transparent) to 1.0 (fully opaque).</span></span>
  
    
    
<span data-ttu-id="f6d98-133">Ниже приведены примеры **ReplaceColor** заметки, используемых в CSS-файл.</span><span class="sxs-lookup"><span data-stu-id="f6d98-133">The following shows examples of the **ReplaceColor** annotation being used in a CSS file.</span></span>
  
    
    

-  `/* [ReplaceColor(themeColor:"BodyText")] */ color:#444;`
    
  
-  `/* [ReplaceColor(themeColor:"BackgroundOverlay",opacity:"0.5")] */ background-color:#fff;`
    
  
-  `/* [ReplaceColor(themeColor:"EmphasisBackground",themeTint:"0.05")] */ background-color:#f2faff;`
    
  

### <a name="replacefont-annotation"></a><span data-ttu-id="f6d98-134">ReplaceFont заметки</span><span class="sxs-lookup"><span data-stu-id="f6d98-134">ReplaceFont annotation</span></span>
<span data-ttu-id="f6d98-135"><a name="replaceFont"> </a></span><span class="sxs-lookup"><span data-stu-id="f6d98-135"></span></span>

<span data-ttu-id="f6d98-p108">Заметки **ReplaceFont** добавляет шрифт темы указанного списка доступных шрифтов. Его можно использовать со свойствами CSS **font** и **font-family**.</span><span class="sxs-lookup"><span data-stu-id="f6d98-p108">The **ReplaceFont** annotation adds the specified theme font to the list of available fonts. It can be used with the **font** and **font-family** CSS properties.</span></span>
  
    
    
<span data-ttu-id="f6d98-138">Ниже приводится формат **ReplaceFont** заметки.</span><span class="sxs-lookup"><span data-stu-id="f6d98-138">The following shows the format for the **ReplaceFont** annotation.</span></span>
  
    
    



```

/* [ReplaceFont(themeFont:"FontSlot")] */
```

<span data-ttu-id="f6d98-139">Замените _FontSlot_ имя разъем шрифта для использования.</span><span class="sxs-lookup"><span data-stu-id="f6d98-139">Replace  _FontSlot_ with the name of the font slot to use.</span></span> <span data-ttu-id="f6d98-140">Чтобы просмотреть список доступных шрифта разъемов разделу, посвященному [слотами шрифта](color-palettes-and-fonts-in-sharepoint.md#fontSlot) [палитры цветов и шрифтов в SharePoint](color-palettes-and-fonts-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="f6d98-140">To see a list of available font slots, see the [Font slots](color-palettes-and-fonts-in-sharepoint.md#fontSlot) section in [Color palettes and fonts in SharePoint](color-palettes-and-fonts-in-sharepoint.md).</span></span>
  
    
    
<span data-ttu-id="f6d98-p110">Ниже показан пример **ReplaceFont** заметки. В этом примере Если разъем **body** шрифтов определяется как Courier в теме, Courier добавляются как первый элемент в списке доступных шрифтов в мастере **Choose the Look**.</span><span class="sxs-lookup"><span data-stu-id="f6d98-p110">The following shows an example of the **ReplaceFont** annotation. In this example, if the **body** font slot is defined as Courier in the theme, Courier will be added as the first item in the list of available fonts in the **Choose the Look** wizard.</span></span>
  
    
    

-  `/* [ReplaceFont(themeFont:"body")] */ font-family:"Segoe UI","Segoe",Tahoma,Helvetica,Arial,sans-serif;`
    
  

### <a name="replacebgimage-annotation"></a><span data-ttu-id="f6d98-143">ReplaceBGImage заметки</span><span class="sxs-lookup"><span data-stu-id="f6d98-143">ReplaceBGImage annotation</span></span>
<span data-ttu-id="f6d98-144"><a name="replaceBGimage"> </a></span><span class="sxs-lookup"><span data-stu-id="f6d98-144"></span></span>

<span data-ttu-id="f6d98-p111">Заметки **ReplaceBGImage** заменяет фонового изображения в CSS-файл фонового изображения темы. Его можно использовать со свойствами CSS **background** и **background-image**.</span><span class="sxs-lookup"><span data-stu-id="f6d98-p111">The **ReplaceBGImage** annotation replaces the background image in the CSS file with the theme background image. It can be used with the **background** and **background-image** CSS properties.</span></span>
  
    
    
<span data-ttu-id="f6d98-p112">Ниже приводится формат **ReplaceBGImage** заметки. Заметки **ReplaceBGImage** можно также использовать с фильтром **AlphaImageLoader** для поддержки более ранних версий Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="f6d98-p112">The following shows the format for the **ReplaceBGImage** annotation. The **ReplaceBGImage** annotation can also be used with the **AlphaImageLoader** filter to support earlier versions of Internet Explorer.</span></span>
  
    
    



```
/* [ReplaceBGImage] */
```


### <a name="recolorimage-annotation"></a><span data-ttu-id="f6d98-149">RecolorImage заметки</span><span class="sxs-lookup"><span data-stu-id="f6d98-149">RecolorImage annotation</span></span>
<span data-ttu-id="f6d98-150"><a name="replaceBGimage"> </a></span><span class="sxs-lookup"><span data-stu-id="f6d98-150"></span></span>

<span data-ttu-id="f6d98-151">Заметки **RecolorImage** recolors указываемое изображение.</span><span class="sxs-lookup"><span data-stu-id="f6d98-151">The **RecolorImage** annotation recolors the image specified.</span></span>
  
    
    
<span data-ttu-id="f6d98-152">Следующие описывает формат **RecolorImage** заметки.</span><span class="sxs-lookup"><span data-stu-id="f6d98-152">The following describes the format of the **RecolorImage** annotation.</span></span>
  
    
    



```
/* [RecolorImage(themeColor:"ColorSlot"[, method:["Tinting"|"Blending"|"Filling"]][, includeRectangle: {x:x-Setting,y:y-Setting,width:RegionWidth,height:RegionHeight})] */

```

<span data-ttu-id="f6d98-153">Замените _ColorSlot_ имя заметки разъем цвет.</span><span class="sxs-lookup"><span data-stu-id="f6d98-153">Replace  _ColorSlot_ with the annotation name of the color slot.</span></span> <span data-ttu-id="f6d98-154">Чтобы просмотреть список доступных разъемов разделу, посвященному [разъем сопоставление цветов](color-palettes-and-fonts-in-sharepoint.md#colorSlots) [палитры цветов и шрифтов в SharePoint](color-palettes-and-fonts-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="f6d98-154">To see a list of available color slots, see the [Color slot mapping](color-palettes-and-fonts-in-sharepoint.md#colorSlots) section in [Color palettes and fonts in SharePoint](color-palettes-and-fonts-in-sharepoint.md).</span></span>
  
    
    
<span data-ttu-id="f6d98-155">Используйте параметр необязательно **method**, если вы хотите указать метод recoloring.</span><span class="sxs-lookup"><span data-stu-id="f6d98-155">Use the optional **method** parameter if you want to specify the recoloring method.</span></span>
  
    
    
<span data-ttu-id="f6d98-p114">Используйте параметр необязательно **includeRectangle**, если вы хотите изменить цвет для отдельного региона изображения. Замените _x-Setting_,  _y-Setting_,  _RegionWidth_и  _RegionHeight_ оси x, оси y, ширину и высоту области, которую требуется изменить цвет.</span><span class="sxs-lookup"><span data-stu-id="f6d98-p114">Use the optional **includeRectangle** parameter if you want to recolor only a specific region of an image. Replace _x-Setting_,  _y-Setting_,  _RegionWidth_, and  _RegionHeight_ with the x-coordinate, y-coordinate, width, and height of the region that you want to recolor.</span></span>
  
    
    
<span data-ttu-id="f6d98-158">Ниже приведены примеры **RecolorImage** заметки, используемых в CSS-файл.</span><span class="sxs-lookup"><span data-stu-id="f6d98-158">The following shows examples of the **RecolorImage** annotation being used in a CSS file.</span></span>
  
    
    

-  `/* [RecolorImage(themeColor:"SubtleBodyText",method:"Tinting")] */ background-image:url("/_layouts/15/images/tabtitlerowbottombg.png?rev=23");`
    
  
-  `/* [RecolorImage(themeColor:"BodyText",method:"Filling",includeRectangle:{x:161,y:178,width:16;height:16})] */ background:url("/_layouts/15/images/spcommon.png?rev=23") no-repeat -161px -178px;`
    
  

## <a name="upload-the-css-file-to-the-themable-folder-in-the-style-library"></a><span data-ttu-id="f6d98-159">Отправка CSS-файл в папку Themable в библиотеку стилей</span><span class="sxs-lookup"><span data-stu-id="f6d98-159">Upload the CSS file to the Themable folder in the Style library</span></span>
<span data-ttu-id="f6d98-160"><a name="uploadCSS"> </a></span><span class="sxs-lookup"><span data-stu-id="f6d98-160"></span></span>

<span data-ttu-id="f6d98-161">Размещение настраиваемого CSS-файлы в папку Themable в библиотеку стилей (не Themable папке в коллекции главных страниц).</span><span class="sxs-lookup"><span data-stu-id="f6d98-161">Place the custom CSS files in the Themable folder in the Style library (not the Themable folder in the Master Page Gallery).</span></span> <span data-ttu-id="f6d98-162">Только CSS-файлы, которые хранятся в папке Themable в библиотеку стилей распознаются ядром темы.</span><span class="sxs-lookup"><span data-stu-id="f6d98-162">Only CSS files that are stored in the Themable folder in the Style library are recognized by the theming engine.</span></span> <span data-ttu-id="f6d98-163">Для сайтов публикации автоматически создается папка Themable.</span><span class="sxs-lookup"><span data-stu-id="f6d98-163">The Themable folder is created automatically for publishing sites.</span></span> <span data-ttu-id="f6d98-164">В противном случае можно создать папку Themable в правильном месте (http:// _SiteCollectionName_Style Library / __языка/Themable /).</span><span class="sxs-lookup"><span data-stu-id="f6d98-164">Otherwise, you can create the Themable folder in the correct location (http://  _SiteCollectionName_/Style Library/ _language_/Themable/).</span></span>
  
    
    

> <span data-ttu-id="f6d98-165">**Примечание:** Имя папки _языка_ должно быть в формате 4-значного _Яя сс_ для идентификации языка и региональных параметров, соответственно.</span><span class="sxs-lookup"><span data-stu-id="f6d98-165">**Note:** The name of the  _language_ folder must be in the 4-digit format _ll-cc_ to identify the language and culture, respectively.</span></span> <span data-ttu-id="f6d98-166">Например, en-us или ar-sa.</span><span class="sxs-lookup"><span data-stu-id="f6d98-166">For example, en-us or ar-sa.</span></span> <span data-ttu-id="f6d98-167">Для получения дополнительных сведений см [идентификаторы языков и значения идентификаторов OptionState в Office 2013](http://technet.microsoft.com/ru-ru/library/cc179219.aspx).</span><span class="sxs-lookup"><span data-stu-id="f6d98-167">For more information, see [Language identifiers and OptionState Id values in Office 2013](http://technet.microsoft.com/ru-ru/library/cc179219.aspx).</span></span> 
  
    
    

<span data-ttu-id="f6d98-p117">CSS-файлы должны вернули и опубликован. Если CSS-файлы изменяются, необходимо повторно применить темы для внесенных изменений.</span><span class="sxs-lookup"><span data-stu-id="f6d98-p117">CSS files must be checked in and published. If CSS files are changed, you must reapply the theme for the changes to be recognized.</span></span>
  
    
    

## <a name="register-the-css-file"></a><span data-ttu-id="f6d98-170">Регистрация CSS-файла</span><span class="sxs-lookup"><span data-stu-id="f6d98-170">Register the CSS file</span></span>
<span data-ttu-id="f6d98-171"><a name="registerCSS"> </a></span><span class="sxs-lookup"><span data-stu-id="f6d98-171"></span></span>

<span data-ttu-id="f6d98-p118">Необходимо зарегистрировать CSS-файла в главную страницу, прежде чем CSS-файла можно использовать ядром темы. Если применить тему к сайту, направляет главную страницу в CSS-файл. Регистрация CSS-файла, добавьте элемент **<SharePoint:CssRegistration>** в элемент **<head>** главной страницы. Ниже показан формат элемента **<SharePoint:CssRegistration>**.</span><span class="sxs-lookup"><span data-stu-id="f6d98-p118">You must register the CSS file with a master page before the CSS file can be used by the theming engine. This directs the master page to the CSS file when you apply a theme to a site. To register a CSS file, you add a **<SharePoint:CssRegistration>** element to the **<head>** element of the master page. The following shows the format of the **<SharePoint:CssRegistration>** element.</span></span>
  
    
    

```HTML

<SharePoint:CssRegistration Name="CSSFileLocation" runat="server" />
```

<span data-ttu-id="f6d98-176">Замените  _CSSFileLocation_ расположение CSS-файла.</span><span class="sxs-lookup"><span data-stu-id="f6d98-176">Replace  _CSSFileLocation_ with the location of the CSS file.</span></span>
  
    
    
<span data-ttu-id="f6d98-177">Ниже приведен пример элемента **<SharePoint:CssRegistration>**.</span><span class="sxs-lookup"><span data-stu-id="f6d98-177">The following is an example of an **<SharePoint:CssRegistration>** element.</span></span>
  
    
    



```HTML
<head>
…
<SharePoint:CssRegistration Name="<%$SPUrl:~SiteCollection/Style Library/~language/Themable/MyCustomFile.css%>" runat="server" />
</head>
```


> <span data-ttu-id="f6d98-178">**Примечание:** Маркер **%$SPUrl** не может использоваться в SharePoint Foundation 2013.</span><span class="sxs-lookup"><span data-stu-id="f6d98-178">**Note:** The **%$SPUrl** token cannot be used on SharePoint Foundation 2013.</span></span> <span data-ttu-id="f6d98-179">Необходимо использовать URL-адрес, чтобы указать расположение CSS-файла.</span><span class="sxs-lookup"><span data-stu-id="f6d98-179">You must use a URL to specify the location of the CSS file.</span></span>
  
    
    


## <a name="additional-resources"></a><span data-ttu-id="f6d98-180">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="f6d98-180">Additional resources</span></span>
<span data-ttu-id="f6d98-181"><a name="addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="f6d98-181"></span></span>


-  [<span data-ttu-id="f6d98-182">Общие сведения о темах для SharePoint</span><span class="sxs-lookup"><span data-stu-id="f6d98-182">Themes overview for SharePoint</span></span>](themes-overview-for-sharepoint.md)
    
  
-  [<span data-ttu-id="f6d98-183">Инструкции. Развертывание пользовательской темы в SharePoint</span><span class="sxs-lookup"><span data-stu-id="f6d98-183">How to: Deploy a custom theme in SharePoint</span></span>](how-to-deploy-a-custom-theme-in-sharepoint.md)
    
  
-  [<span data-ttu-id="f6d98-184">Обновление пользовательских тем и CSS для SharePoint</span><span class="sxs-lookup"><span data-stu-id="f6d98-184">Upgrade custom themes and CSS to SharePoint</span></span>](upgrade-custom-themes-and-css-to-sharepoint.md)
    
  
-  [<span data-ttu-id="f6d98-185">Инструкции. Создание файла предварительного просмотра эталонной страницы в SharePoint</span><span class="sxs-lookup"><span data-stu-id="f6d98-185">How to: Create a master page preview file in SharePoint</span></span>](how-to-create-a-master-page-preview-file-in-sharepoint.md)
    
  
-  [<span data-ttu-id="f6d98-186">Цветовые палитры и шрифты в SharePoint</span><span class="sxs-lookup"><span data-stu-id="f6d98-186">Color palettes and fonts in SharePoint</span></span>](color-palettes-and-fonts-in-sharepoint.md)
    
  
-  [<span data-ttu-id="f6d98-187">Блог команды разработчиков SharePoint. Свой собственный стиль с помощью тем SharePoint</span><span class="sxs-lookup"><span data-stu-id="f6d98-187">SharePoint Team Blog: Show off your style with SharePoint theming</span></span>](http://blogs.office.com/b/sharepoint/archive/2012/10/29/show-off-your-style-with-sharepoint-theming.aspx)
    
  
-  [<span data-ttu-id="f6d98-188">Фирменная символика и конструкция возможности дизайнер SharePoint</span><span class="sxs-lookup"><span data-stu-id="f6d98-188">SharePoint Design Manager branding and design capabilities</span></span>](sharepoint-design-manager-branding-and-design-capabilities.md)
    
  

