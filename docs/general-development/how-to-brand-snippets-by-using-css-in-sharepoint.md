---
title: "Фрагменты кода марки с помощью CSS в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: d18d07b6-1a6b-4589-a65c-932b67cef595
ms.openlocfilehash: 4ed891c06956c4d2ff79cd681b81a3869a03cc3c
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="brand-snippets-by-using-css-in-sharepoint"></a><span data-ttu-id="c80e8-102">Фрагменты кода марки с помощью CSS в SharePoint</span><span class="sxs-lookup"><span data-stu-id="c80e8-102">Brand snippets by using CSS in SharePoint</span></span>

<span data-ttu-id="c80e8-p101">Применять стиль фрагмент, переопределить стилей по умолчанию с помощью настраиваемого CSS. Идентификаторы CSS и значения выбора элементов можно использовать для переопределения стилей по умолчанию, применяемые к элементам, или можно использовать редактор HTML или средства, такие как средства разработчика F12 в Internet Explorer для идентификации и переопределения стили установленный по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="c80e8-p101">To style a snippet, you override the default styles with custom CSS. You can use CSS IDs and element selectors to override all the default styles applied to elements, or you can use an HTML editor or a tool such as the F12 developer tools in Internet Explorer to identify and override specific default styles.</span></span>

## <a name="introduction-to-styling-snippets-with-css"></a><span data-ttu-id="c80e8-105">Общие сведения о фрагменты стилей с помощью CSS</span><span class="sxs-lookup"><span data-stu-id="c80e8-105">Introduction to styling snippets with CSS</span></span>
<span data-ttu-id="c80e8-106"><a name="Introduction"> </a></span><span class="sxs-lookup"><span data-stu-id="c80e8-106"></span></span>

<span data-ttu-id="c80e8-p102">Преобразование HTML-главной страницы или создать макет страницы HTML, можно выполнить предварительный просмотр страницы в режиме предварительного просмотра дизайнер на сервере. На странице просмотра можно перейдите к коллекция фрагментов кода и затем скопируйте фрагментов кода HTML-файл. Фрагмент  это представление HTML управления SharePoint, такие как элемент управления навигации верхнего уровня или поле поиска.</span><span class="sxs-lookup"><span data-stu-id="c80e8-p102">After you convert an HTML master page or create an HTML page layout, you can preview that page in the Design Manager server-side preview. From the preview page, you can navigate to the Snippet Gallery and then copy snippets to your HTML file. A snippet is an HTML representation of a SharePoint control such as a top navigation control or a search box.</span></span>
  
    
    
<span data-ttu-id="c80e8-p103">После скопируйте фрагмент в HTML-файл в подключенный диск и затем сохранить изменения, можно обновить Предварительный просмотр HTML-файл, чтобы увидеть, как элемент управления отображается на сервере. Фрагменты кода содержат разметка, которая предоставляет предварительного просмотра во время разработки в редакторе HTML выбора, но не следует изменить Эта разметка, так как он доступен только для чтения и не влияет на порядок отображения элемента управления на сервере. В то же время, предварительного просмотра на сервере показывает preview надежностью с помощью динамических данных, если доступен  например, элемент управления навигации будет показывать текущей структуры навигации веб-узла с помощью динамических данных из источника данных, таких как банк терминов SharePoint для управляемой навигации.</span><span class="sxs-lookup"><span data-stu-id="c80e8-p103">After you copy a snippet into the HTML file in your mapped drive and then save the changes, you can refresh the server-side preview of the HTML file to see how the control is rendered. Snippets contain markup that provides a design-time preview in your HTML editor of choice, but you shouldn't edit this markup because it's read-only and doesn't affect how the control is rendered on the server. By contrast, the server-side preview shows a full-fidelity preview with live data, if available—for example, a navigation control will show the site's current navigation structure with live data from your data source, such as a SharePoint term store for managed navigation.</span></span>
  
> [!NOTE]
> <span data-ttu-id="c80e8-113">Дополнительные сведения о сопоставлении сетевого диска можно [как: сопоставление сетевого диска коллекции SharePoint главных страниц](how-to-map-a-network-drive-to-the-sharepoint-master-page-gallery.md).</span><span class="sxs-lookup"><span data-stu-id="c80e8-113">For more information about mapping a network drive, see  [How to: Map a network drive to the SharePoint Master Page Gallery](how-to-map-a-network-drive-to-the-sharepoint-master-page-gallery.md).</span></span> 
  
    
    

<span data-ttu-id="c80e8-114">По умолчанию фрагменты наследуют свои стили из таблицы стилей SharePoint, такие как corev15.css.</span><span class="sxs-lookup"><span data-stu-id="c80e8-114">By default, snippets inherit their styles from SharePoint style sheets such as corev15.css.</span></span> <span data-ttu-id="c80e8-115">Чтобы стиль фрагмент, необходимо переопределить эти стили по умолчанию с помощью настраиваемого CSS.</span><span class="sxs-lookup"><span data-stu-id="c80e8-115">To style a snippet, you have to override these default styles with your custom CSS.</span></span> <span data-ttu-id="c80e8-116">Для этого можно выполнить следующие действия.</span><span class="sxs-lookup"><span data-stu-id="c80e8-116">To do this, you can:</span></span>
  
    
    

- <span data-ttu-id="c80e8-117">Использование CSS идентификаторы и значения выбора элементов полностью переопределить стили по умолчанию, применяемые к выбранные элементы.</span><span class="sxs-lookup"><span data-stu-id="c80e8-117">Use CSS IDs and element selectors to completely override the default styles applied to the chosen elements.</span></span>
    
  
- <span data-ttu-id="c80e8-118">Воспользуйтесь средством браузере, например средства разработчика F12 в Internet Explorer для проверки стилей по умолчанию в режиме предварительного просмотра в диспетчере оформления на сервере и затем определите определенные стили для переопределения.</span><span class="sxs-lookup"><span data-stu-id="c80e8-118">Use a browser-based tool such as the F12 developer tools in Internet Explorer to inspect the default styles in the server-side preview in Design Manager, and then identify specific styles to override.</span></span>
    
  
- <span data-ttu-id="c80e8-119">Используйте возможности редактора HTML для проверки стилей по умолчанию в режиме предварительного просмотра только для чтения фрагмент и определите определенные стили для переопределения.</span><span class="sxs-lookup"><span data-stu-id="c80e8-119">Use the features of your HTML editor to inspect the default styles in the read-only preview of a snippet, and then identify specific styles to override.</span></span> 
    
  
<span data-ttu-id="c80e8-p105">Для определения стилей по умолчанию с помощью средств разработки в браузере Internet Explorer, следует использовать preview на сервере в диспетчере оформления для просмотра главной страницы HTML или макет страницы, нажмите клавишу **F12** для запуска средства разработчика, выберите меню « **Поиск** », а затем нажмите **выбрать элемент, нажмите кнопку**. Это позволяет щелкните элементы на странице и посмотрите, какой точно стили, чтобы переопределить, добавив CSS для пользовательской таблицы стилей, HTML главной страницы или страницы макета ссылки на.</span><span class="sxs-lookup"><span data-stu-id="c80e8-p105">To identify the default styles by using the developer tools in Internet Explorer, you should use the server-side preview in Design Manager to view your HTML master page or page layout, press **F12** to start the developer tools, choose the **Find** menu, and then choose **Select element by click**. This enables you to click elements on the page and see exactly what styles to override by adding CSS to the custom style sheet that your HTML master page or page layout links to.</span></span>
  
    
    
<span data-ttu-id="c80e8-122">Таблицы стилей SharePoint по умолчанию содержат множество стили, которые можно сделать его сложного для идентификации определенных стилей.</span><span class="sxs-lookup"><span data-stu-id="c80e8-122">The default SharePoint style sheets contain many styles, which can make it challenging to identify specific styles.</span></span> <span data-ttu-id="c80e8-123">В качестве альтернативы для средства на основе браузера и в зависимости от редактора HTML можно проще копирование фрагмента коллекция фрагментов кода в HTML-файл и затем использовать редактор HTML для определения стилей.</span><span class="sxs-lookup"><span data-stu-id="c80e8-123">As an alternative to browser-based tools, and depending on your HTML editor, you may find it easier to copy the snippet from the Snippet Gallery into your HTML file, and then use the HTML editor to identify the styles.</span></span> <span data-ttu-id="c80e8-124">В коллекции фрагмент при выборе **обновления** и нажмите кнопку **Копировать в буфер обмена**, фрагмент содержит HTML-код для фрагмента.</span><span class="sxs-lookup"><span data-stu-id="c80e8-124">In the Snippet Gallery, when you choose **Update** and then choose **Copy to Clipboard**, the snippet contains an HTML preview of that snippet.</span></span> <span data-ttu-id="c80e8-125">После копирования фрагмента в HTML-файл, можно проверить стилей, используемых в предварительной версии только для чтения, содержащихся в фрагменте.</span><span class="sxs-lookup"><span data-stu-id="c80e8-125">After you copy the snippet into your HTML file, you can inspect the styles used in the read-only preview contained in the snippet.</span></span> <span data-ttu-id="c80e8-126">Таким образом, синтаксический анализ небольшому стилей по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="c80e8-126">This way, you are parsing a smaller subset of the default styles.</span></span>
  
    
    
<span data-ttu-id="c80e8-p107">В зависимости от фрагмента и степень настройки можно полностью переопределить все стили по умолчанию, вместо выбор стилей установленный по умолчанию для переопределения с помощью CSS идентификаторы и значения выбора элементов. Следующий пример демонстрирует этот метод используется для применение пользовательских стилей к фрагменту верхней панели навигации.</span><span class="sxs-lookup"><span data-stu-id="c80e8-p107">Depending on the snippet and the extent of your customization, you may want to use CSS IDs and element selectors to completely override all of the default styles, instead of choosing specific default styles to override. The following example demonstrates how to use this method to apply custom styles to the top navigation snippet.</span></span>
  
    
    

## <a name="example-style-the-top-navigation-snippet"></a><span data-ttu-id="c80e8-129">Пример: Стиль фрагмент верхней панели навигации</span><span class="sxs-lookup"><span data-stu-id="c80e8-129">Example: Style the top navigation snippet</span></span>
<span data-ttu-id="c80e8-130"><a name="Example"> </a></span><span class="sxs-lookup"><span data-stu-id="c80e8-130"></span></span>

<span data-ttu-id="c80e8-131">В верхней панели навигации фрагменте — это один из наиболее часто используемые фрагменты кода, поэтому он также является одним из наиболее часто фирменной символики фрагменты кода.</span><span class="sxs-lookup"><span data-stu-id="c80e8-131">The top navigation snippet is one of the most commonly used snippets, so it's also one of the most commonly branded snippets.</span></span> <span data-ttu-id="c80e8-132">На сайте SharePoint можно выбрать параметр для использования управляемой навигации, чтобы банка терминов, становится источник данных для фрагмента верхней панели навигации.</span><span class="sxs-lookup"><span data-stu-id="c80e8-132">In a SharePoint site, you can select an option to use managed navigation, so that a term store becomes the data source for the top navigation snippet.</span></span> <span data-ttu-id="c80e8-133">Таким образом, можно использовать средство управления терминами хранилища в **Настройках сайта** для добавления или удаления терминам навигации и управления таксономии навигации, которая отображается по навигации в начало фрагмента.</span><span class="sxs-lookup"><span data-stu-id="c80e8-133">This way, you can use the Term Store Management tool in **Site Settings** to add or delete navigation terms and to manage the navigation taxonomy that is displayed by the Top Navigation snippet.</span></span>
  
    
    
<span data-ttu-id="c80e8-p109">В этом примере на сайте используется управляемая навигация, элемент управления навигации верхнего уровня извлекает его записи из банка терминов. Существует один уровень всплывающие окна, отображаются при наведении указателя на термин навигации верхнего уровня, например, **компьютеры**. В этом разделе показано, как эти настраиваемые стили переопределить стилей SharePoint по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="c80e8-p109">In this example, the site uses managed navigation, so the top navigation control pulls its entries from a term store. There is one level of flyouts that appear when you hover over a top-level navigation term, such as **Computers**. This section demonstrates how these custom styles override the default SharePoint styles.</span></span>
  
    
    

### <a name="sample-1-navigation-div-from-the-html-mockup-file"></a><span data-ttu-id="c80e8-137">Пример 1: Навигации \<div\> из HTML-файл макета</span><span class="sxs-lookup"><span data-stu-id="c80e8-137">Sample 1: Navigation \<div\> from the HTML mockup file</span></span>

<span data-ttu-id="c80e8-138">Прежде чем использовать Дизайнер, при разработке макета HTML для главной страницы, скорее всего используется HTML и CSS для разработки элемент функциональным верхней панели навигации.</span><span class="sxs-lookup"><span data-stu-id="c80e8-138">Before you use Design Manager, when you design the HTML mockup for your master page, you'll likely use HTML and CSS to design a functional top navigation element.</span></span> <span data-ttu-id="c80e8-139">В этом примере HTML используется базовая структура для верхней панели навигации: ** \<div\> ** идентификатор и имя класса, в список для записи навигации верхнего уровня и вложенных списков для каждого подменю всплывающего в элемент.</span><span class="sxs-lookup"><span data-stu-id="c80e8-139">This HTML sample uses a basic structure for the top navigation: a **\<div\>** element with an ID and class name, a list for the top-level navigation entries, and a nested list for each flyout submenu.</span></span>
  
    
    

```HTML

<div id="navigation" class="msax-Navigation">
   <ul>
      <li><a href="#">Cameras</a>
         <ul>
            <li><a href="#">Camcorders</a></li>
            <li><a href="#">Digital cameras</a></li>
            <li><a href="#">Disposable cameras</a></li>
            <li><a href="#">Film cameras</a></li>
         </ul>
      </li>
      <li><a href="#">Computers</a>
         <ul>
            <li><a href="#">Desktops</a></li>
            <li><a href="#">Laptops</a></li>
            <li><a href="#">Netbooks</a></li>
            <li><a href="#">Tablets</a></li>
         </ul>
      </li>
      <li><a href="#">Media</a>
         <ul>
            <li><a href="#">Movies</a></li>
            <li><a href="#">Music</a></li>
            <li><a href="#">TV shows </a></li>
            <li><a href="#">Video games </a></li>
         </ul>
      </li>
      <li></li>
   </ul>
</div>

```


### <a name="sample-2-navigation-div-styled-with-custom-css"></a><span data-ttu-id="c80e8-140">Пример 2: Навигации \<div\> со стилем с помощью настраиваемого CSS</span><span class="sxs-lookup"><span data-stu-id="c80e8-140">Sample 2: Navigation \<div\> styled with custom CSS</span></span>

<span data-ttu-id="c80e8-141">Чтобы переопределить значение по умолчанию стилей SharePoint в макете HTML-файле включают стандартной связи в CSS-файл `(<link rel="stylesheet" type="text/css" href="URLtoYourCustomCSSFile"/>`) непосредственно перед закрывающим тегом ** \</head\> ** тег.</span><span class="sxs-lookup"><span data-stu-id="c80e8-141">To override the default SharePoint styles, in the mockup HTML file, include a standard link to your CSS file  `(<link rel="stylesheet" type="text/css" href="URLtoYourCustomCSSFile"/>`) just before the closing **\</head\>** tag.</span></span>
  
    
    
<span data-ttu-id="c80e8-142">В этих примерах HTML и CSS Обратите внимание на следующее:</span><span class="sxs-lookup"><span data-stu-id="c80e8-142">In these HTML and CSS samples, note the following:</span></span>
  
    
    

- <span data-ttu-id="c80e8-143">Записи навигации со стилями, используя формат `.msax-Navigation ul li` не напрямую, чтобы применять классы ** \<ul\> ** или ** \<li\> ** тегов.</span><span class="sxs-lookup"><span data-stu-id="c80e8-143">Navigation entries are styled by using the format  `.msax-Navigation ul li` instead of applying classes directly to the **\<ul\>** or **\<li\>** tags.</span></span>
    
  
- <span data-ttu-id="c80e8-144">Стили используется синтаксис `.msax-Navigation ul li` вместо `.msax-Navigation ul>li` так как фрагмент разметки может содержать промежуточных ** \<div\> ** между выбранные элементы.</span><span class="sxs-lookup"><span data-stu-id="c80e8-144">Styles use the syntax  `.msax-Navigation ul li` instead of `.msax-Navigation ul>li` because the snippet markup may contain intervening **\<div\>** tags between the selected elements.</span></span>
    
  
- <span data-ttu-id="c80e8-145">Макете HTML-код содержит пустой ** \<li\>\</li\> ** элемента в качестве последней записи верхнего уровня ** \<ul\>**.</span><span class="sxs-lookup"><span data-stu-id="c80e8-145">The HTML mockup contains an empty **\<li\>\</li\>** element as the last entry of the top-level **\<ul\>**.</span></span> <span data-ttu-id="c80e8-146">Это, поскольку с включенным управляемой навигации, SharePoint добавляет команду **Изменить связи** как последний элемент навигации верхнего уровня и окончательный сайта обычно не требуется отображать этот параметр.</span><span class="sxs-lookup"><span data-stu-id="c80e8-146">This is because, with managed navigation turned on, SharePoint adds an **Edit Links** command as the final entry to the top-level navigation, and the final site typically does not need to display this option.</span></span> <span data-ttu-id="c80e8-147">CSS примере используются `.msax-Navigation ul li:last-child` выберите эту запись и задайте отображаемое значение `none`.</span><span class="sxs-lookup"><span data-stu-id="c80e8-147">The CSS sample uses `.msax-Navigation ul li:last-child` to select this entry and set the display value to `none`.</span></span> <span data-ttu-id="c80e8-148">Пустой ** \<li\>\</li\> ** элемент в HTML-файл является временной заменой запись **Изменить связи** по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="c80e8-148">The empty **\<li\>\</li\>** element in the HTML file is a temporary substitute for the default **Edit Links** entry.</span></span> <span data-ttu-id="c80e8-149">Необходимо учитывать этом последнем ** \<li\> ** элемент при использовании сайтом управляемой навигации и таблицы стилей CSS используются какие-либо `li:last-child` селекторы.</span><span class="sxs-lookup"><span data-stu-id="c80e8-149">Be aware of this final **\<li\>** element if your site uses managed navigation and your CSS uses any `li:last-child` selectors.</span></span>
    
  



```HTML

.msax-Navigation {
margin: 10px 0px; top: 0px; position: relative;
z-index:200;
}
.msax-Navigation a {
margin: 0px; padding: 0px; border: 0px currentColor;
}
.msax-Navigation ul {
list-style: none; margin: 0px; padding: 0px; font-size: 16px; z-index:200;
}
.msax-Navigation ul li {
padding: 10px; display: inline-block; position: relative; z-index:200;
}
.msax-Navigation ul li:first-child {
margin: 0px;
}
.msax-Navigation ul li:last-child {
margin: 0px; padding: 0px; display: none;
}
.msax-Navigation ul li a.selected, .msax-Navigation ul li.selected {
background-color: rgb(58,60,62) !important;
color:rgb(255,255,255) !important;
}
.msax-Navigation ul li a {
width: 100%; color: rgb(58,60,62); font-size: 16px;
}
.msax-Navigation ul li:hover {
background-color: rgb(58,60,62);
color:rgb(255,255,255) !important;
}
.msax-Navigation ul li a:hover {
text-decoration: none;
color:rgb(255,255,255) !important;
}
.msax-Navigation li ul {
left: 0px; top: 35px; display: none; position: absolute; min-width: 100px; box-shadow: 5px 5px 10px 0px rgb(0,0,0); background-color: rgb(58,60,62);
}
.msax-Navigation li:hover ul {
display: block; z-index: 150;
}
.msax-Navigation li li {
margin: 0px; padding: 5px 10px 5px 0px; border-top-width: 0px; display: block; min-width: 100px;
}
.msax-Navigation li li:last-child {
margin: 0px; padding: 5px 10px 5px 0px; border-top-width: 0px; display: block; min-width: 100px;
}
.msax-Navigation li li a {
width: 100%; padding-left: 10px; display: block; color:rgb(255,255,255) !important;
}
.msax-Navigation li li:hover {
background-color: rgb(120, 120, 120);
}

```


### <a name="sample-3-read-only-preview-of-the-top-navigation-snippet"></a><span data-ttu-id="c80e8-150">Пример 3: Предварительный просмотр только для чтения фрагмента верхней панели навигации</span><span class="sxs-lookup"><span data-stu-id="c80e8-150">Sample 3: Read-only preview of the top navigation snippet</span></span>

<span data-ttu-id="c80e8-151">После того как настраиваемые стили реализованы в вашей макете HTML и у вас есть элемент функциональным верхней панели навигации, выполните обычные действия.</span><span class="sxs-lookup"><span data-stu-id="c80e8-151">After your custom styles are implemented in your HTML mockup and you have a functional top navigation element, follow the usual steps:</span></span>
  
    
    

1. <span data-ttu-id="c80e8-152">Сопоставление сетевого диска.</span><span class="sxs-lookup"><span data-stu-id="c80e8-152">Map a network drive.</span></span>
    
  
2. <span data-ttu-id="c80e8-153">Отправьте файлы проекта.</span><span class="sxs-lookup"><span data-stu-id="c80e8-153">Upload your design files.</span></span>
    
  
3. <span data-ttu-id="c80e8-154">Преобразование HTML-файла в эталонную страницу</span><span class="sxs-lookup"><span data-stu-id="c80e8-154">Convert the HTML file into a master page.</span></span>
    
  
4. <span data-ttu-id="c80e8-155">Предварительный просмотр и устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="c80e8-155">Preview and fix any issues.</span></span>
    
  
5. <span data-ttu-id="c80e8-156">Добавьте фрагмент верхней панели навигации на главную страницу HTML с помощью коллекция фрагментов кода.</span><span class="sxs-lookup"><span data-stu-id="c80e8-156">Add the top navigation snippet to the HTML master page by using the Snippet Gallery.</span></span>
    
  
<span data-ttu-id="c80e8-157">Коллекция фрагментов кода при настройке свойства фрагмента верхней панели навигации, обратите внимание на следующее:</span><span class="sxs-lookup"><span data-stu-id="c80e8-157">In the Snippet Gallery, when you configure the properties of the top navigation snippet, note the following:</span></span>
  
    
    

- <span data-ttu-id="c80e8-158">В разделе **важные** вверху не изменяйте свойством **CssClass**.</span><span class="sxs-lookup"><span data-stu-id="c80e8-158">In the **Important** section at the top, do not make any changes to the **CssClass** property.</span></span>
    
  
- <span data-ttu-id="c80e8-p112">Не вносите никаких изменений в свойства под заголовком **AjaxDelta**, так как эти свойства связаны с MDS свойства, которые SharePoint использует для преобразования фрагмент HTML в соответствующем фрагменте ASP.NET. Это относится к любой фрагмент не только фрагмент верхней панели навигации.</span><span class="sxs-lookup"><span data-stu-id="c80e8-p112">Do not make any changes to properties under the **AjaxDelta** heading because these properties are related to the MDS properties that SharePoint uses to convert the HTML snippet into the corresponding ASP.NET snippet. This applies to any snippet, not just the top navigation snippet.</span></span>
    
  
- <span data-ttu-id="c80e8-p113">Если вы планируете переопределить стилей SharePoint по умолчанию, в коллекция фрагментов кода, в разделе **Behavior** **AspMenu** (может быть более одного раздела **Behavior** Если фрагмент содержит более одного элемента управления, такие как замещаемого элемента управления), присвойте **ClientIDMode** **Static**. Если оставить значение по умолчанию **ClientIDMode** установки, **Inherit**, применяемые CSS фрагмент классы будет изменяться в зависимости от порядок использования фрагменты на странице. Дополнительные сведения о **ClientIDMode** [Control.ClientIDMode свойство](http://msdn.microsoft.com/en-us/library/system.web.ui.control.clientidmode.aspx)см.</span><span class="sxs-lookup"><span data-stu-id="c80e8-p113">If you're planning to override the default SharePoint styles, in the Snippet Gallery, in the **Behavior** section under **AspMenu** (there may be more than one **Behavior** section if the snippet contains more than one control, such as a delegate control), set **ClientIDMode** to **Static**. If you leave **ClientIDMode** set to the default setting, **Inherit**, the snippet's applied CSS classes will change based on the ordering of snippets on the page. For more information about **ClientIDMode**, see  [Control.ClientIDMode property](http://msdn.microsoft.com/en-us/library/system.web.ui.control.clientidmode.aspx).</span></span>
    
    <span data-ttu-id="c80e8-p114">Например по умолчанию, элемент управления верхней панели навигации использует атрибуты идентификатор SharePoint по умолчанию, такие как **zz5_TopNavigationMenu** и **zz6_RootAspMenu**. Изменяя **ClientIDMode** **Static**, можно сделать возможным для использования этих кодов по умолчанию в качестве селекторы в свои собственные CSS для переопределения стилей SharePoint по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="c80e8-p114">For example, by default, the top navigation control uses default SharePoint ID attributes such as **zz5_TopNavigationMenu** and **zz6_RootAspMenu**. By changing **ClientIDMode** to **Static**, you make it possible to use these default IDs as selectors in your own CSS to override the default SharePoint styles.</span></span>
    
  
- <span data-ttu-id="c80e8-p115">Некоторые свойства уже настроена для сделать фирменной символики в верхней панели навигации фрагменте удобства, устраняя поведение динамических CSS и JavaScript по умолчанию  например, по умолчанию **UseSimpleRendering** задано значение **True**, **MaximumDynamicDisplayLevels** задано значение **0**. Дополнительные сведения о конкретных свойствах фрагмент верхней панели навигации можно  [AspMenu свойства](http://msdn.microsoft.com/en-us/library/ms412476.aspx) и [Свойства меню](http://msdn.microsoft.com/en-us/library/282668a1.aspx).</span><span class="sxs-lookup"><span data-stu-id="c80e8-p115">Some properties are already configured to make branding the top navigation snippet easier by eliminating the default dynamic CSS and JavaScript behaviors—for example, by default **UseSimpleRendering** is set to **True** and **MaximumDynamicDisplayLevels** is set to **0**. For more information about specific properties of the top navigation snippet, see  [AspMenu properties](http://msdn.microsoft.com/en-us/library/ms412476.aspx) and [Menu properties](http://msdn.microsoft.com/en-us/library/282668a1.aspx).</span></span>
    
  
<span data-ttu-id="c80e8-168">После настройки фрагмента верхней панели навигации в коллекция фрагментов кода выберите **обновления**и нажмите кнопку **Копировать в буфер обмена**.</span><span class="sxs-lookup"><span data-stu-id="c80e8-168">After you configure the top navigation snippet in the Snippet Gallery, choose **Update**, and then choose **Copy to Clipboard**.</span></span> <span data-ttu-id="c80e8-169">На главной странице HTML, удалите содержимое панели навигации `<div id="navigation" class="msax-Navigation">` , который содержит элемент управления макета (удалить только содержимое ** \<div\> ** тега, не ** \<div\> ** тега самого) и затем скопируйте фрагмент в панели навигации ** \<div\>**.</span><span class="sxs-lookup"><span data-stu-id="c80e8-169">In the HTML master page, delete the contents of the navigation  `<div id="navigation" class="msax-Navigation">` that contains your mockup control (delete just the contents of the **\<div\>** tag, not the **\<div\>** tag itself), and then copy the snippet into the navigation **\<div\>**.</span></span> <span data-ttu-id="c80e8-170">При необходимости изменить положение панели навигации ** \<div\>**, обычно непосредственно после начала `<div id="s4-bodyContainer">` тега, но перед ** \<div\> ** содержащий `PlaceHolderMain`.</span><span class="sxs-lookup"><span data-stu-id="c80e8-170">If necessary, reposition the navigation **\<div\>**, typically just after the start of the  `<div id="s4-bodyContainer">` tag but before the **\<div\>** containing `PlaceHolderMain`.</span></span>
  
    
    
<span data-ttu-id="c80e8-171">Для удобного сравнения с HTML-код навигации ** \<div\> ** выше, следующий пример содержит структуру переходов ** \<div\> ** часть фрагмента верхней панели навигации.</span><span class="sxs-lookup"><span data-stu-id="c80e8-171">For easy comparison with the HTML of the navigation **\<div\>** above, the following sample contains the navigation **\<div\>** portion of the top navigation snippet.</span></span> <span data-ttu-id="c80e8-172">Обратите внимание на то, что это не всей фрагмента.</span><span class="sxs-lookup"><span data-stu-id="c80e8-172">Note that this is not the entire snippet.</span></span>
  
    
    



```HTML

<div id="zz7_TopNavigationMenu" class=" noindex ms-core-listMenu-horizontalBox">
     <ul id="zz9_RootAspMenu" class="root ms-core-listMenu-root static">
          <li class="static">
          <a accesskey="1" class="static menu-item ms-core-listMenu-item ms-displayInline ms-navedit-linkNode" href="/sites/PubSite/cameras" tabindex="0">
          <span class="additional-background ms-navedit-flyoutArrow">
          <span class="menu-item-text">Cameras</span></span></a><ul class="static">
               <li class="static">
               <a class="static menu-item ms-core-listMenu-item ms-displayInline ms-navedit-linkNode" href="/sites/PubSite/cameras/camcorders" tabindex="0">
               <span class="additional-background ms-navedit-flyoutArrow">
               <span class="menu-item-text">Camcorders</span></span></a></li>
               <li class="static">
               <a class="static menu-item ms-core-listMenu-item ms-displayInline ms-navedit-linkNode" href="/sites/PubSite/cameras/digital-cameras" tabindex="0">
               <span class="additional-background ms-navedit-flyoutArrow">
               <span class="menu-item-text">Digital cameras</span></span></a></li>
               <li class="static">
               <a class="static menu-item ms-core-listMenu-item ms-displayInline ms-navedit-linkNode" href="/sites/PubSite/cameras/disposable-cameras" tabindex="0">
               <span class="additional-background ms-navedit-flyoutArrow">
               <span class="menu-item-text">Disposable cameras</span></span></a></li>
               <li class="static">
               <a class="static menu-item ms-core-listMenu-item ms-displayInline ms-navedit-linkNode" href="/sites/PubSite/cameras/film-cameras" tabindex="0">
               <span class="additional-background ms-navedit-flyoutArrow">
               <span class="menu-item-text">Film cameras</span></span></a></li>
          </ul>
          </li>
          <li class="static">
          <a class="static menu-item ms-core-listMenu-item ms-displayInline ms-navedit-linkNode" href="/sites/PubSite/computers" tabindex="0">
          <span class="additional-background ms-navedit-flyoutArrow">
          <span class="menu-item-text">Computers</span></span></a><ul class="static">
               <li class="static">
               <a class="static menu-item ms-core-listMenu-item ms-displayInline ms-navedit-linkNode" href="/sites/PubSite/computers/desktops" tabindex="0">
               <span class="additional-background ms-navedit-flyoutArrow">
               <span class="menu-item-text">Desktops</span></span></a></li>
               <li class="static">
               <a class="static menu-item ms-core-listMenu-item ms-displayInline ms-navedit-linkNode" href="/sites/PubSite/computers/laptops" tabindex="0">
               <span class="additional-background ms-navedit-flyoutArrow">
               <span class="menu-item-text">Laptops</span></span></a></li>
               <li class="static">
               <a class="static menu-item ms-core-listMenu-item ms-displayInline ms-navedit-linkNode" href="/sites/PubSite/computers/netbooks" tabindex="0">
               <span class="additional-background ms-navedit-flyoutArrow">
               <span class="menu-item-text">Netbooks</span></span></a></li>
               <li class="static">
               <a class="static menu-item ms-core-listMenu-item ms-displayInline ms-navedit-linkNode" href="/sites/PubSite/computers/tablets" tabindex="0">
               <span class="additional-background ms-navedit-flyoutArrow">
               <span class="menu-item-text">Tablets</span></span></a></li>
          </ul>
          </li>
          <li class="static">
          <a class="static menu-item ms-core-listMenu-item ms-displayInline ms-navedit-linkNode" href="/sites/PubSite/media" tabindex="0">
          <span class="additional-background ms-navedit-flyoutArrow">
          <span class="menu-item-text">Media</span></span></a><ul class="static">
               <li class="static">
               <a class="static menu-item ms-core-listMenu-item ms-displayInline ms-navedit-linkNode" href="/sites/PubSite/media/movies" tabindex="0">
               <span class="additional-background ms-navedit-flyoutArrow">
               <span class="menu-item-text">Movies</span></span></a></li>
               <li class="static">
               <a class="static menu-item ms-core-listMenu-item ms-displayInline ms-navedit-linkNode" href="/sites/PubSite/media/music" tabindex="0">
               <span class="additional-background ms-navedit-flyoutArrow">
               <span class="menu-item-text">Music</span></span></a></li>
               <li class="static">
               <a class="static menu-item ms-core-listMenu-item ms-displayInline ms-navedit-linkNode" href="/sites/PubSite/media/tv-shows" tabindex="0">
               <span class="additional-background ms-navedit-flyoutArrow">
               <span class="menu-item-text">TV shows</span></span></a></li>
               <li class="static">
               <a class="static menu-item ms-core-listMenu-item ms-displayInline ms-navedit-linkNode" href="/sites/PubSite/media/video-games" tabindex="0">
               <span class="additional-background ms-navedit-flyoutArrow">
               <span class="menu-item-text">Video games</span></span></a></li>
          </ul>
          </li>
          <li class="static ms-verticalAlignTop ms-listMenu-editLink ms-navedit-editArea">
          <span id="zz7_TopNavigationMenu_NavMenu_Edit" class="ms-navedit-editSpan">
          <a id="zz7_TopNavigationMenu_NavMenu_EditLinks" class="ms-navedit-editLinksText" href="#" onclick="g_QuickLaunchMenu = null; EnsureScriptParams('quicklaunch.js', 'QuickLaunchInitEditMode', 'zz7_TopNavigationMenu', 2, 0, 0, ''); cancelDefault(event); return false;">
          <span class="ms-displayInlineBlock">
          <span class="ms-navedit-editLinksIconWrapper ms-verticalAlignMiddle">
          <img class="ms-navedit-editLinksIcon" src="/_layouts/15/images/spcommon.png?rev=23" /></span><span class="ms-metadata ms-verticalAlignMiddle">Edit Links</span></span></a><span id="zz7_TopNavigationMenu_NavMenu_Loading" class="ms-navedit-menuLoading ms-hide"><a id="zz7_TopNavigationMenu_NavMenu_GearsLink" href="#" onclick="HideGears(); return false;" title="This animation indicates the operation is in progress. Click to remove this animated image."><img id="zz7_TopNavigationMenu_NavMenu_GearsImage" src="/_layouts/15/images/loadingcirclests16.gif?rev=23" /></a></span><div id="zz7_TopNavigationMenu_NavMenu_ErrorMsg" class="ms-navedit-errorMsg">
          </div>
          </span></li>
     </ul>
</div>

```

<span data-ttu-id="c80e8-p118">Вместо использования только настраиваемые стили, в некоторых случаях сценарий, где необходимо переопределить только определенный стиль. Например чтобы скрыть узел **Изменение ссылки**, можно создать настраиваемый стиль, который используется по умолчанию идентификатор **zz7_TopNavigationMenu_NavMenu_Edit**, чтобы задать параметры отображения `none`.</span><span class="sxs-lookup"><span data-stu-id="c80e8-p118">Instead of using only custom styles, you may have a scenario where you want to override just a specific style. For example, to hide the **Edit Links** node, you can create a custom style that uses the default id **zz7_TopNavigationMenu_NavMenu_Edit** to set the display setting to `none`.</span></span>
  
    
    

## <a name="see-also"></a><span data-ttu-id="c80e8-175">См. также</span><span class="sxs-lookup"><span data-stu-id="c80e8-175">See also</span></span>
<span data-ttu-id="c80e8-176"><a name="Additional"> </a></span><span class="sxs-lookup"><span data-stu-id="c80e8-176"></span></span>


-  [<span data-ttu-id="c80e8-177">Фрагменты кода дизайнер SharePoint</span><span class="sxs-lookup"><span data-stu-id="c80e8-177">SharePoint Design Manager snippets</span></span>](sharepoint-design-manager-snippets.md)
    
  
-  [<span data-ttu-id="c80e8-178">Обзор Дизайнера в SharePoint</span><span class="sxs-lookup"><span data-stu-id="c80e8-178">Overview of Design Manager in SharePoint</span></span>](overview-of-design-manager-in-sharepoint.md)
    
  
-  [<span data-ttu-id="c80e8-179">Инструкции. Преобразование HTML-файла в эталонную страницу SharePoint</span><span class="sxs-lookup"><span data-stu-id="c80e8-179">How to: Convert an HTML file into a master page in SharePoint</span></span>](how-to-convert-an-html-file-into-a-master-page-in-sharepoint.md)
    
  
-  [<span data-ttu-id="c80e8-180">Инструкции. Создание макета страницы в SharePoint</span><span class="sxs-lookup"><span data-stu-id="c80e8-180">How to: Create a page layout in SharePoint</span></span>](how-to-create-a-page-layout-in-sharepoint.md)
    
  
-  [<span data-ttu-id="c80e8-181">Разработка макета сайта в SharePoint</span><span class="sxs-lookup"><span data-stu-id="c80e8-181">Develop the site design in SharePoint</span></span>](develop-the-site-design-in-sharepoint.md)
    
  

