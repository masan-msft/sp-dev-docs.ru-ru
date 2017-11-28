---
title: "Использование состоит выполняет на сайты SharePoint торговая марка"
ms.date: 11/03/2017
ms.openlocfilehash: ebf4fa0e503cb8c811c6e7ac549d1b89998c1a7d
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
# <a name="use-composed-looks-to-brand-sharepoint-sites"></a><span data-ttu-id="9d0db-102">Использование состоит выполняет на сайты SharePoint торговая марка</span><span class="sxs-lookup"><span data-stu-id="9d0db-102">Use composed looks to brand SharePoint sites</span></span>

<span data-ttu-id="9d0db-103">Применение вариантов оформления, включая цвета, шрифты и фонового изображения, к сайтам SharePoint 2013 и SharePoint Online с помощью модуля темы SharePoint.</span><span class="sxs-lookup"><span data-stu-id="9d0db-103">Apply composed looks, including colors, fonts, and a background image, to your SharePoint 2013 and SharePoint Online sites by using the SharePoint theming engine.</span></span>

<span data-ttu-id="9d0db-104">_**Область применения:** Office 365 | SharePoint 2013 | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="9d0db-104">_**Applies to:** Office 365 | SharePoint 2013 | SharePoint Online_</span></span>

<span data-ttu-id="9d0db-105">Вариантов оформления можно применить к сайтам SharePoint.</span><span class="sxs-lookup"><span data-stu-id="9d0db-105">You can apply composed looks to your SharePoint sites.</span></span> <span data-ttu-id="9d0db-106">Вариантов оформления, ожидания введите тем, которые включены в SharePoint 2013 и SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="9d0db-106">Composed looks are out-of-the-box themes that are included in SharePoint 2013 and SharePoint Online.</span></span> <span data-ttu-id="9d0db-107">Чтобы применить вариант оформления на сайт SharePoint, выберите **Параметры сайта** > **внешний вид и функции** > **Изменение внешнего вида**.</span><span class="sxs-lookup"><span data-stu-id="9d0db-107">To apply a composed look to a SharePoint site, select **Site Settings** > **Look and Feel** > **Change the look**.</span></span> <span data-ttu-id="9d0db-108">Затем можно использовать изменение внешнего вида мастера настройки цвета, шрифты, главные страницы и фонового изображения вариант оформления.</span><span class="sxs-lookup"><span data-stu-id="9d0db-108">You can then use the Change the look wizard to customize the colors, fonts, master page, and background image of a composed look.</span></span> <span data-ttu-id="9d0db-109">Изменение внешнего вида мастер копирует, преобразует и сохраняет CSS в базе данных контента SharePoint.</span><span class="sxs-lookup"><span data-stu-id="9d0db-109">The Change the look wizard copies, transforms, and stores CSS in SharePoint's content database.</span></span> <span data-ttu-id="9d0db-110">Также recolors изображения и сохраняет их в базе данных контента.</span><span class="sxs-lookup"><span data-stu-id="9d0db-110">It also recolors images and stores them in the content database.</span></span> 

## <a name="sharepoint-theming-engine"></a><span data-ttu-id="9d0db-111">Модуль темы SharePoint</span><span class="sxs-lookup"><span data-stu-id="9d0db-111">SharePoint theming engine</span></span>
<span data-ttu-id="9d0db-112"><a name="sectionSection0"> </a></span><span class="sxs-lookup"><span data-stu-id="9d0db-112"></span></span>

<span data-ttu-id="9d0db-113">Модуль SharePoint 2013 темы можно использовать для применения цвета, шрифты и фонового изображения на сайт с помощью сопоставления этих элементов с главной страницы.</span><span class="sxs-lookup"><span data-stu-id="9d0db-113">You can use the SharePoint 2013 theming engine to apply colors, fonts, and a background image to a site by associating those elements with a master page.</span></span>

<span data-ttu-id="9d0db-114">В SharePoint 2013 и SharePoint Online темы — подключенных набор файлов определений XML, файл изображения и связанную главную страницу, которые можно использовать для применения настраиваемых CSS к сайту.</span><span class="sxs-lookup"><span data-stu-id="9d0db-114">In SharePoint 2013 and SharePoint Online, a theme is a connected set of XML definition files, an image file, and an associated master page that you can use to apply custom CSS to a site.</span></span> <span data-ttu-id="9d0db-115">Следующие XML-файлы определения слотами цвета и слотами шрифта, которые определяют сведения о конкретных цветовое оформление и шрифты, как они в случае применены стили:</span><span class="sxs-lookup"><span data-stu-id="9d0db-115">The following XML files define color slots and font slots that define the details of specific colors and fonts as they're applied to styles:</span></span> 

- <span data-ttu-id="9d0db-116">.spcolor</span><span class="sxs-lookup"><span data-stu-id="9d0db-116">.spcolor</span></span>
    
- <span data-ttu-id="9d0db-117">.spfont</span><span class="sxs-lookup"><span data-stu-id="9d0db-117">.spfont</span></span>
    
<span data-ttu-id="9d0db-118">Можно создать собственные файлы шрифтов и цветов в любого текстового редактора.</span><span class="sxs-lookup"><span data-stu-id="9d0db-118">You can create your own color and font files in your favorite text editor.</span></span>

<span data-ttu-id="9d0db-119">В следующей таблице перечислены элементы вариант оформления.</span><span class="sxs-lookup"><span data-stu-id="9d0db-119">The following table lists the elements of a composed look.</span></span>

|<span data-ttu-id="9d0db-120">**Элемент**</span><span class="sxs-lookup"><span data-stu-id="9d0db-120">**Element**</span></span>|<span data-ttu-id="9d0db-121">**Файл или файлы**</span><span class="sxs-lookup"><span data-stu-id="9d0db-121">**File or files**</span></span>|<span data-ttu-id="9d0db-122">**Где хранится**</span><span class="sxs-lookup"><span data-stu-id="9d0db-122">**Where it's stored**</span></span>|<span data-ttu-id="9d0db-123">**Обязательность**</span><span class="sxs-lookup"><span data-stu-id="9d0db-123">**Required?**</span></span>|
|:-----|:-----|:-----|:-----|
|<span data-ttu-id="9d0db-124">Цветовая палитра</span><span class="sxs-lookup"><span data-stu-id="9d0db-124">Color palette</span></span>|<span data-ttu-id="9d0db-125">.spcolor</span><span class="sxs-lookup"><span data-stu-id="9d0db-125">.spcolor</span></span>|<span data-ttu-id="9d0db-126">Папка Gallery\15 темы</span><span class="sxs-lookup"><span data-stu-id="9d0db-126">Theme Gallery\15 folder</span></span>|<span data-ttu-id="9d0db-127">Да</span><span class="sxs-lookup"><span data-stu-id="9d0db-127">Yes</span></span>|
|<span data-ttu-id="9d0db-128">Схемы шрифтов</span><span class="sxs-lookup"><span data-stu-id="9d0db-128">Font scheme</span></span>|<span data-ttu-id="9d0db-129">.spfont</span><span class="sxs-lookup"><span data-stu-id="9d0db-129">.spfont</span></span>|<span data-ttu-id="9d0db-130">Папка Gallery\15 темы</span><span class="sxs-lookup"><span data-stu-id="9d0db-130">Theme Gallery\15 folder</span></span>|<span data-ttu-id="9d0db-131">Нет</span><span class="sxs-lookup"><span data-stu-id="9d0db-131">No</span></span>|
|<span data-ttu-id="9d0db-132">Макет сайта</span><span class="sxs-lookup"><span data-stu-id="9d0db-132">Site layout</span></span>|<p><span data-ttu-id="9d0db-133">.master</span><span class="sxs-lookup"><span data-stu-id="9d0db-133">.master</span></span></p><p><span data-ttu-id="9d0db-134">.Preview</span><span class="sxs-lookup"><span data-stu-id="9d0db-134">.preview</span></span></p>|<span data-ttu-id="9d0db-135">Коллекция главных страниц</span><span class="sxs-lookup"><span data-stu-id="9d0db-135">Master Page Gallery</span></span>|<span data-ttu-id="9d0db-136">Да</span><span class="sxs-lookup"><span data-stu-id="9d0db-136">Yes</span></span>|
|<span data-ttu-id="9d0db-137">Фоновое изображение</span><span class="sxs-lookup"><span data-stu-id="9d0db-137">Background image</span></span>|<p><span data-ttu-id="9d0db-138">.jpg</span><span class="sxs-lookup"><span data-stu-id="9d0db-138">.jpg</span></span></p><p><span data-ttu-id="9d0db-139">.bmp</span><span class="sxs-lookup"><span data-stu-id="9d0db-139">.bmp</span></span></p><p><span data-ttu-id="9d0db-140">.PNG</span><span class="sxs-lookup"><span data-stu-id="9d0db-140">.png</span></span></p><p><span data-ttu-id="9d0db-141">.gif</span><span class="sxs-lookup"><span data-stu-id="9d0db-141">.gif</span></span></p>|<span data-ttu-id="9d0db-142">Активы сайта</span><span class="sxs-lookup"><span data-stu-id="9d0db-142">Site assets</span></span>|<span data-ttu-id="9d0db-143">Нет</span><span class="sxs-lookup"><span data-stu-id="9d0db-143">No</span></span>|
<span data-ttu-id="9d0db-144">Пользователи могут выбрать вариантов оформления с помощью изменения внешнего вида мастера (**Параметры узла** > **внешний вид и функции** > **Изменение внешнего вида**), начало работы пользовательского интерфейса, или непосредственно в меню Действия сайта.</span><span class="sxs-lookup"><span data-stu-id="9d0db-144">Users can select composed looks by using the Change the look wizard (**Site Settings** > **Look and Feel** > **Change the Look**), the Getting Started UI, or directly in the site actions menu.</span></span> <span data-ttu-id="9d0db-145">Когда пользователь выбирает вариант оформления, модуль темы применяется цвета, шрифты, фоновые рисунки, связанные главную страницу и файл .preview, связанный с главную страницу на сайте.</span><span class="sxs-lookup"><span data-stu-id="9d0db-145">When a user selects a composed look, the theming engine applies colors, fonts, background images, the associated .master page, and the .preview file associated with the .master page to the site.</span></span> 

### <a name="color-palettes"></a><span data-ttu-id="9d0db-146">Палитры цветов</span><span class="sxs-lookup"><span data-stu-id="9d0db-146">Color palettes</span></span>

<span data-ttu-id="9d0db-147">Модуль темы сохраняет цветов в цветовой палитры, определенные в файле .spcolor, как показано на рисунке 1.</span><span class="sxs-lookup"><span data-stu-id="9d0db-147">The theming engine stores colors in color palettes defined by the .spcolor file, as shown in Figure 1.</span></span> <span data-ttu-id="9d0db-148">Цветовой палитры, хранятся в коллекцию тем корневого сайта.</span><span class="sxs-lookup"><span data-stu-id="9d0db-148">Color palettes are stored in the Theme Gallery of the root site.</span></span> <span data-ttu-id="9d0db-149">Цветовой палитры является редактирования XML-файла включает в себя определения цветовой палитры и слотами цвет.</span><span class="sxs-lookup"><span data-stu-id="9d0db-149">A color palette is an editable XML file made up of color palette definitions and color slots.</span></span> <span data-ttu-id="9d0db-150">Цветовой палитры метаданных ( `<s:colorPalette>`) определяет следующее:</span><span class="sxs-lookup"><span data-stu-id="9d0db-150">Color palette metadata ( `<s:colorPalette>`) defines the following:</span></span>

- <span data-ttu-id="9d0db-151">Три Предварительный просмотр области, которые определяют цвет разъемов для использования в области просмотра вариант оформления.</span><span class="sxs-lookup"><span data-stu-id="9d0db-151">Three preview slots that define what color slots to use in composed look previews.</span></span>
    
- <span data-ttu-id="9d0db-152">Это свойство **isInverted** , которое позволяет указать, будет ли темы Обращенный конструктора палитры (темный фон на светло текст).</span><span class="sxs-lookup"><span data-stu-id="9d0db-152">An  **isInverted** property that lets the palette designer specify whether the theme is inverted (dark background with light text).</span></span>
    
- <span data-ttu-id="9d0db-153">Пространство имен XML, связанные с темой.</span><span class="sxs-lookup"><span data-stu-id="9d0db-153">The XML namespace associated with the theme.</span></span>
    
<span data-ttu-id="9d0db-154">Цвет слотами определяются два attributesâ€ «цвет имени и valueâ€», определите имя цвета и его значение RGB.</span><span class="sxs-lookup"><span data-stu-id="9d0db-154">Color slots are defined by two attributesâ€”color name and valueâ€”that define a name for the color and its RGB value.</span></span> <span data-ttu-id="9d0db-155">Цвет имеется семантических имена, например BodyText или SiteTitle, помогает идентифицировать какие слоты соответствуют область страницы SharePoint.</span><span class="sxs-lookup"><span data-stu-id="9d0db-155">Color slots have semantic names, such as BodyText or SiteTitle, that help you identify which slots correspond to a region of a SharePoint page.</span></span>

`<s:color name="BodyText" value="444444" />`

<span data-ttu-id="9d0db-156">**На рисунке 1. файл .spcolor**</span><span class="sxs-lookup"><span data-stu-id="9d0db-156">**Figure 1. .spcolor file**</span></span>

![Снимок экрана с отображением имени и значения атрибутов цвета .spcolor-файла](media/16de0716-2e21-471f-b9e5-f461a33b397b.png)

<span data-ttu-id="9d0db-158">Строка 2 .spcolor-файла определяет пространство имен XML слотами предварительного просмотра и ли Обращенный цвета (у них быстрое переднего плана на темный фон вместо темный переднего плана на светлый фон).</span><span class="sxs-lookup"><span data-stu-id="9d0db-158">Line 2 of the .spcolor file defines the XML namespace, preview slots, and whether colors are inverted (they have a light foreground on a dark background instead of a dark foreground on a light background).</span></span> 

<span data-ttu-id="9d0db-159">Файл .spcolor содержит 89 слотами цвет.</span><span class="sxs-lookup"><span data-stu-id="9d0db-159">The .spcolor file contains 89 color slots.</span></span> <span data-ttu-id="9d0db-160">Цвет слотами можно использовать для определения функционального аспектов цвет, включая непрозрачность, с помощью 8-значного шестнадцатеричные значения.</span><span class="sxs-lookup"><span data-stu-id="9d0db-160">You can use color slots to define richer aspects of color, including opacity, by using 8-digit hexadecimal values.</span></span> <span data-ttu-id="9d0db-161">Например, если зеленый будет вида RRGGBB 00FF00, соответствующее 70 процентов непрозрачный является AARRGGBB 7F00FF00.</span><span class="sxs-lookup"><span data-stu-id="9d0db-161">For example, if green is RRGGBB 00FF00, a 70 percent opaque green is AARRGGBB 7F00FF00.</span></span> <span data-ttu-id="9d0db-162">Если SharePoint использует область, которая не был определен, любой CSS, которая ссылается на него не будет изменить цвет.</span><span class="sxs-lookup"><span data-stu-id="9d0db-162">If SharePoint uses a slot that you don't define, any CSS that references it won't change color.</span></span> <span data-ttu-id="9d0db-163">Если область определен, никогда не содержит ссылку на CSS, цвет никогда не отображается в пользовательском Интерфейсе.</span><span class="sxs-lookup"><span data-stu-id="9d0db-163">If a slot is defined that is never referenced in CSS, the color is never shown in the UI.</span></span>

<span data-ttu-id="9d0db-164">Можно изменить файл .spcolor в "Блокнот".</span><span class="sxs-lookup"><span data-stu-id="9d0db-164">You can edit the .spcolor file in Notepad.</span></span> <span data-ttu-id="9d0db-165">Его нельзя изменить в Microsoft PowerPoint.</span><span class="sxs-lookup"><span data-stu-id="9d0db-165">You cannot edit it in PowerPoint.</span></span>

### <a name="color-palette-tool"></a><span data-ttu-id="9d0db-166">Средство цветовой палитры</span><span class="sxs-lookup"><span data-stu-id="9d0db-166">Color palette tool</span></span>

<span data-ttu-id="9d0db-167">Можно использовать [средство цветовой палитры](http://www.microsoft.com/en-us/download/details.aspx?id=38182) для визуализации цвета темы и как они работают вместе на странице.</span><span class="sxs-lookup"><span data-stu-id="9d0db-167">You can use the  [color palette tool](http://www.microsoft.com/en-us/download/details.aspx?id=38182) to visualize theme colors and how they work together on the page.</span></span> <span data-ttu-id="9d0db-168">Используйте его для определения цвета сведения можно использовать в слотами цвет файла .spcolor и цвета для сайта SharePoint без изменения любого CSS в ходе процесса.</span><span class="sxs-lookup"><span data-stu-id="9d0db-168">Use it to identify color information you can use in the color slots of the .spcolor file, and apply colors to a SharePoint site without changing any CSS as part of the process.</span></span>

<span data-ttu-id="9d0db-169">Появится цвета в шестнадцатеричном формате, поэтому можно легко скопируйте и вставьте значение цвета в соответствующий элемент в файле .spcolor.</span><span class="sxs-lookup"><span data-stu-id="9d0db-169">The tool displays the colors in hexadecimal format, so you can easily copy and paste the color value into the appropriate element in your .spcolor file.</span></span> <span data-ttu-id="9d0db-170">Можно также использовать средство цветовой палитры для размещения фонового изображения в макете и переключение между seattle.master и oslo.master главных страниц.</span><span class="sxs-lookup"><span data-stu-id="9d0db-170">You can also use the color palette tool to fit a background image into a mockup and toggle between the seattle.master and oslo.master master pages.</span></span> 


<span data-ttu-id="9d0db-171">**На рисунке 2. Средство цветовой палитры**</span><span class="sxs-lookup"><span data-stu-id="9d0db-171">**Figure 2. Color palette tool**</span></span>

![Снимок экрана средства палитры цветов](media/407d8095-20cd-4d9b-be53-493d95b4653c.png)

<span data-ttu-id="9d0db-173">Файл .spcolor — это единственный файл, который необходим для новой темы, но может потребоваться добавить некоторые объявления пользовательских шрифтов, в зависимости от глубины к проекту.</span><span class="sxs-lookup"><span data-stu-id="9d0db-173">The .spcolor file is the only file that is required for a new theme, but you might need to add some custom font declarations, depending on the depth of your design.</span></span> <span data-ttu-id="9d0db-174">Для этого необходимо получить доступ к файлу .spfont.</span><span class="sxs-lookup"><span data-stu-id="9d0db-174">To do that, you need to access the .spfont file.</span></span>

### <a name="font-schemes"></a><span data-ttu-id="9d0db-175">Схемы шрифтов</span><span class="sxs-lookup"><span data-stu-id="9d0db-175">Font schemes</span></span>

<span data-ttu-id="9d0db-176">Так же, как определить, что палитры цветов использование цветов в вариантов оформления схемы шрифтов определения шрифтов в вариантов оформления.</span><span class="sxs-lookup"><span data-stu-id="9d0db-176">In the same way that color palettes define how colors are used in composed looks, font schemes define the fonts in composed looks.</span></span> 

<span data-ttu-id="9d0db-177">Схемы шрифтов определены в файле .spfont, хранящиеся в коллекцию тем.</span><span class="sxs-lookup"><span data-stu-id="9d0db-177">Font schemes are defined in the .spfont file stored in the Theme Gallery.</span></span> <span data-ttu-id="9d0db-178">Файл .spfont включает в себя следующие слотами шрифта, которые определяют имя, гарнитуры и скрипт значения вариант оформления:</span><span class="sxs-lookup"><span data-stu-id="9d0db-178">The .spfont file includes the following font slots that define the name, typeface, and script values of a composed look:</span></span>

- <span data-ttu-id="9d0db-179">Заголовок</span><span class="sxs-lookup"><span data-stu-id="9d0db-179">Title</span></span>
    
- <span data-ttu-id="9d0db-180">Navigation</span><span class="sxs-lookup"><span data-stu-id="9d0db-180">Navigation</span></span>
    
- <span data-ttu-id="9d0db-181">Заголовок небольшим</span><span class="sxs-lookup"><span data-stu-id="9d0db-181">Small-heading</span></span>
    
- <span data-ttu-id="9d0db-182">Заголовок</span><span class="sxs-lookup"><span data-stu-id="9d0db-182">Heading</span></span>
    
- <span data-ttu-id="9d0db-183">Large заголовок</span><span class="sxs-lookup"><span data-stu-id="9d0db-183">Large-heading</span></span>
    
- <span data-ttu-id="9d0db-184">Body</span><span class="sxs-lookup"><span data-stu-id="9d0db-184">Body</span></span>
    
- <span data-ttu-id="9d0db-185">Large-body</span><span class="sxs-lookup"><span data-stu-id="9d0db-185">Large-body</span></span>
    
<span data-ttu-id="9d0db-186">Шрифты дальнейшей области по типу сценария (например, латиница, арабский, кириллица).</span><span class="sxs-lookup"><span data-stu-id="9d0db-186">Fonts are further scoped by script type (for example, Latin, Arabic, Cyrillic).</span></span> <span data-ttu-id="9d0db-187">Поддержка шрифты Web включен в четырех типов файлов:</span><span class="sxs-lookup"><span data-stu-id="9d0db-187">Web fonts support is included in four file types:</span></span>

- <span data-ttu-id="9d0db-188">Тип внедренного open (EOT)</span><span class="sxs-lookup"><span data-stu-id="9d0db-188">Embedded open type (EOT)</span></span>
    
- <span data-ttu-id="9d0db-189">Файл в формате open шрифта Web (WOFF)</span><span class="sxs-lookup"><span data-stu-id="9d0db-189">Web open font format file (WOFF)</span></span>
    
- <span data-ttu-id="9d0db-190">Шрифтов TrueType (TTF)</span><span class="sxs-lookup"><span data-stu-id="9d0db-190">TrueType font (TTF)</span></span>
    
- <span data-ttu-id="9d0db-191">Масштабируемой векторной графики (SVG)</span><span class="sxs-lookup"><span data-stu-id="9d0db-191">Scalable vector graphics (SVG)</span></span>
    
<span data-ttu-id="9d0db-192">Схемы шрифтов определяется изображения для предварительного просмотра и изображения для малых предварительного просмотра.</span><span class="sxs-lookup"><span data-stu-id="9d0db-192">The font scheme defines a large preview image and a small preview image.</span></span> <span data-ttu-id="9d0db-193">Они необходимы только для веб-шрифты.</span><span class="sxs-lookup"><span data-stu-id="9d0db-193">They are required only for web fonts.</span></span>

<span data-ttu-id="9d0db-194">**Примечание**  Можно изменить файл .spfont в "Блокнот".</span><span class="sxs-lookup"><span data-stu-id="9d0db-194">**Note**  You can edit the .spfont file in Notepad.</span></span> <span data-ttu-id="9d0db-195">Его нельзя изменить в Microsoft PowerPoint.</span><span class="sxs-lookup"><span data-stu-id="9d0db-195">You cannot edit it in PowerPoint.</span></span>

<span data-ttu-id="9d0db-196">Ниже приведен пример файла .spfont.</span><span class="sxs-lookup"><span data-stu-id="9d0db-196">The following is an example of an .spfont file.</span></span>

```XML
<?xml version="1.0" encoding="utf-8"?>
<s:fontScheme name="Georgia" previewSlot1="title" previewSlot2="body"
  xmlns:s=http://schemas.microsoft.com/sharepoint/>
    <s:fontSlots>
        <s:fontSlot name="title">
            <s:latin typeface="Georgia"/>
            <s:font script="Arab" typeface="Calibri" />
            <s:font script="Deva" typeface="Mangal" />
            . . . 
        </s:fontSlot>
    <s:fontSlot name="navigation">
        <s:latin typeface="Georgia"/>
        <s:font script="Arab" typeface="Calibri" />
        <s:font script="Deva" typeface="Mangal" />
        . . . 
        </s:fontSlot>
    </s:fontSlots>
</s:fontScheme>
```

### <a name="site-layout-master-pages-and-corresponding-preview-files"></a><span data-ttu-id="9d0db-197">Макет сайта: главные страницы и соответствующие файлы предварительного просмотра</span><span class="sxs-lookup"><span data-stu-id="9d0db-197">Site layout: master pages and corresponding preview files</span></span>

<span data-ttu-id="9d0db-198">Модуль темы определяет макет сайта вариант оформления на основе .master главной страницы и соответствующего файла .preview.</span><span class="sxs-lookup"><span data-stu-id="9d0db-198">The theming engine defines the site layout of a composed look based on the .master master page and its corresponding .preview file.</span></span> <span data-ttu-id="9d0db-199">Например если главная страница, определенных для вариант оформления seattle.master, Главная страница определяет макет сайта.</span><span class="sxs-lookup"><span data-stu-id="9d0db-199">For example, if the master page defined for the composed look is seattle.master, that master page defines the layout of the site.</span></span>

<span data-ttu-id="9d0db-200">Макет сайта извлечено из коллекции главных страниц главных страницах, которые имеют сопутствующие файлы .preview.</span><span class="sxs-lookup"><span data-stu-id="9d0db-200">The site layout is pulled from the Master Page Gallery of any master pages that have accompanying .preview files.</span></span> <span data-ttu-id="9d0db-201">Файл .preview является обязательным для главной страницы на отображается в качестве параметра в разделе **Изменение внешнего вида** пользовательского интерфейса (**Параметры узла** > **внешний вид и функции** > **Изменение внешнего вида**).</span><span class="sxs-lookup"><span data-stu-id="9d0db-201">A .preview file is required for a master page to appear as an option in the **Change the look** UI (**Site Settings** > **Look and Feel** > **Change the look**).</span></span>

<span data-ttu-id="9d0db-202">Создавать главную страницу, доступные в раскрывающемся меню Макет сайта, создайте файл .preview, соответствующий главную страницу.</span><span class="sxs-lookup"><span data-stu-id="9d0db-202">To make a master page available from the Site Layout drop-down menu, create a .preview file that corresponds to the .master page.</span></span> <span data-ttu-id="9d0db-203">Файл .preview отображение эскизов вариант оформления и в разделе Просмотр справа от параметры **изменения внешнего вида** страницы designbuilder.aspx.</span><span class="sxs-lookup"><span data-stu-id="9d0db-203">The .preview file displays thumbnail images for the composed look and the preview section to the right of the **Change the look** options on the designbuilder.aspx page.</span></span>

### <a name="background-image"></a><span data-ttu-id="9d0db-204">Фоновое изображение</span><span class="sxs-lookup"><span data-stu-id="9d0db-204">Background image</span></span>

<span data-ttu-id="9d0db-205">Фоновое изображение вариант оформления можно изменить, выбрав **Изменить**.</span><span class="sxs-lookup"><span data-stu-id="9d0db-205">You can change the background image of a composed look by choosing **Change**.</span></span> <span data-ttu-id="9d0db-206">Откроется диалоговое окно Отправка, которые можно использовать для передачи файла изображения.</span><span class="sxs-lookup"><span data-stu-id="9d0db-206">This opens an upload dialog box that you can use to upload an image file.</span></span> <span data-ttu-id="9d0db-207">Также можно перетащить собственное изображение на просмотр фона.</span><span class="sxs-lookup"><span data-stu-id="9d0db-207">You can also drag your own image onto the background preview.</span></span>

## <a name="create-custom-themes"></a><span data-ttu-id="9d0db-208">Создание пользовательских тем</span><span class="sxs-lookup"><span data-stu-id="9d0db-208">Create custom themes</span></span>
<span data-ttu-id="9d0db-209"><a name="sectionSection1"> </a></span><span class="sxs-lookup"><span data-stu-id="9d0db-209"></span></span>

<span data-ttu-id="9d0db-210">Для создания пользовательской темы:</span><span class="sxs-lookup"><span data-stu-id="9d0db-210">To create a custom theme:</span></span>

1. <span data-ttu-id="9d0db-211">Перейти к **параметрам сайта**и под заголовком коллекции веб-дизайнера, выберите **тем** > **15**.</span><span class="sxs-lookup"><span data-stu-id="9d0db-211">Go to **Site settings**, and under the Web Designer Galleries heading, select **Themes** > **15**.</span></span> <span data-ttu-id="9d0db-212">Появится список файлов .spcolor и .spfont, как показано на рисунке 3.</span><span class="sxs-lookup"><span data-stu-id="9d0db-212">A list of .spcolor and .spfont files appears, as shown in Figure 3.</span></span>
    
    <span data-ttu-id="9d0db-213">**На рисунке 3. Коллекция тем**</span><span class="sxs-lookup"><span data-stu-id="9d0db-213">**Figure 3. Theme Gallery**</span></span>

    ![Снимок экрана из коллекции тем, показывающий файлы fontscheme и палитры](media/76e9b4f3-5838-4cd8-9f2f-33a0c94bfddd.png)

2. <span data-ttu-id="9d0db-215">Загрузить копию один из файлов .spcolor (например, Palette001.spcolor) и откройте его в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="9d0db-215">Download a copy of one of the .spcolor files (for example, Palette001.spcolor) and open it in a text editor.</span></span> 
    
3. <span data-ttu-id="9d0db-216">Редактирование файла скопированной .spcolor в соответствии с требованиями к разработки.</span><span class="sxs-lookup"><span data-stu-id="9d0db-216">Edit the copied .spcolor file to reflect your design guidelines.</span></span> <span data-ttu-id="9d0db-217">Например, при наличии черного шрифта для основной текст, отредактируйте файл, чтобы измените строку `<s:color name="BodyText" value="444444" />` для `<s:color name="BodyText" value="000000" />`.</span><span class="sxs-lookup"><span data-stu-id="9d0db-217">For example, if you have a black font for main body text, edit the file to change the line  `<s:color name="BodyText" value="444444" />` to `<s:color name="BodyText" value="000000" />`.</span></span>
    
4. <span data-ttu-id="9d0db-218">Для каждого элемента HTML добавьте цвета.</span><span class="sxs-lookup"><span data-stu-id="9d0db-218">For each HTML element, add your color.</span></span> 
    
5. <span data-ttu-id="9d0db-219">Закончив, отправьте файл .spcolor **Параметры сайта** > **темы** > **15** папки.</span><span class="sxs-lookup"><span data-stu-id="9d0db-219">When you are done, upload the .spcolor file to the **Site settings** > **Theme** > **15** folder.</span></span>
    
    <span data-ttu-id="9d0db-220">**Примечание**  Сохраните файл под новым именем файла (например, custom_palette1.spcolor).</span><span class="sxs-lookup"><span data-stu-id="9d0db-220">**Note**  Save the file with a new file name (for example, custom_palette1.spcolor).</span></span>

   <span data-ttu-id="9d0db-221">В следующей таблице сопоставлены цветовое оформление и элементы страниц в код в файле .spcolor.</span><span class="sxs-lookup"><span data-stu-id="9d0db-221">The following table maps colors and page elements to their code in the .spcolor file.</span></span> <span data-ttu-id="9d0db-222">Он является частью сопоставления, доступные в файле .spcolor.</span><span class="sxs-lookup"><span data-stu-id="9d0db-222">It is a subset of the mappings that are available in the .spcolor file.</span></span>
    

    |<span data-ttu-id="9d0db-223">**Элемент**</span><span class="sxs-lookup"><span data-stu-id="9d0db-223">**Element**</span></span>|<span data-ttu-id="9d0db-224">**Цвет**</span><span class="sxs-lookup"><span data-stu-id="9d0db-224">**Color**</span></span>|<span data-ttu-id="9d0db-225">**Код**</span><span class="sxs-lookup"><span data-stu-id="9d0db-225">**Code**</span></span>|
    |:-----|:-----|:-----|
    |<span data-ttu-id="9d0db-226">Основной текст</span><span class="sxs-lookup"><span data-stu-id="9d0db-226">Body text</span></span>|<span data-ttu-id="9d0db-227">Черный</span><span class="sxs-lookup"><span data-stu-id="9d0db-227">Black</span></span>| `<s:color name="BodyText" value="000000" />`|
    |<span data-ttu-id="9d0db-228">Фон глобальной навигации</span><span class="sxs-lookup"><span data-stu-id="9d0db-228">Global navigation background</span></span>|<span data-ttu-id="9d0db-229">Синий</span><span class="sxs-lookup"><span data-stu-id="9d0db-229">Blue</span></span>| `<s:color name="HeaderBackground" value="018dff" />`|
    |<span data-ttu-id="9d0db-230">Текст глобальной навигации</span><span class="sxs-lookup"><span data-stu-id="9d0db-230">Global navigation text</span></span>|<span data-ttu-id="9d0db-231">Белый</span><span class="sxs-lookup"><span data-stu-id="9d0db-231">White</span></span>| `<s:color name="HeaderNavigationText" value="ffffff" />`|
    |<span data-ttu-id="9d0db-232">Текущий фон навигации</span><span class="sxs-lookup"><span data-stu-id="9d0db-232">Current navigation background</span></span>|<span data-ttu-id="9d0db-233">Красный</span><span class="sxs-lookup"><span data-stu-id="9d0db-233">Red</span></span>| `<s:color name="NavigationHoverBackground" value="e51400" />`|
    |<span data-ttu-id="9d0db-234">Текущий текст навигации</span><span class="sxs-lookup"><span data-stu-id="9d0db-234">Current navigation text</span></span>|<span data-ttu-id="9d0db-235">Белый</span><span class="sxs-lookup"><span data-stu-id="9d0db-235">White</span></span>| `<s:color name="Navigation" value="ffffff" />`|
    |<span data-ttu-id="9d0db-236">Заголовок</span><span class="sxs-lookup"><span data-stu-id="9d0db-236">Title</span></span>|<span data-ttu-id="9d0db-237">Белый</span><span class="sxs-lookup"><span data-stu-id="9d0db-237">White</span></span>| `<s:color name="SiteTitle" value="FFFFFF" />`|
    |<span data-ttu-id="9d0db-238">Нижний колонтитул фона</span><span class="sxs-lookup"><span data-stu-id="9d0db-238">Footer background</span></span>|<span data-ttu-id="9d0db-239">Черный</span><span class="sxs-lookup"><span data-stu-id="9d0db-239">Black</span></span>| `<s:color name="FooterBackground" value="000000" />`|

6. <span data-ttu-id="9d0db-240">Чтобы настроить .spfont, загрузить копию файла .spfont и откройте его в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="9d0db-240">To customize .spfont, download a copy of a .spfont file and open it in a text editor.</span></span> <span data-ttu-id="9d0db-241">Обратите внимание на то, немного иначе, чем .spcolor макета в файл .spfont, однако, что оба файла совместно использовать аналогичную структуру.</span><span class="sxs-lookup"><span data-stu-id="9d0db-241">Notice that the .spfont file is laid out a bit differently than .spcolor, but that both files share a similar structure.</span></span> 
    
    <span data-ttu-id="9d0db-242">**На рисунке 4. файл .spfont**</span><span class="sxs-lookup"><span data-stu-id="9d0db-242">**Figure 4. .spfont file**</span></span>

    ![Снимок экрана, на котором отображается содержимое файла .spfont](media/893f905a-34d9-4dbd-a012-03797084f9e6.png)

7. <span data-ttu-id="9d0db-244">Изменение каждого `<s:fontSlot />` раздела для настройки шрифта SharePoint относятся к разъем указанного шрифта на странице.</span><span class="sxs-lookup"><span data-stu-id="9d0db-244">Edit each  `<s:fontSlot />` section to customize the font SharePoint applies to the specified font slot on the page.</span></span> <span data-ttu-id="9d0db-245">Например, обратите внимание на то первой записи `<s:fontSlot name="title">`.</span><span class="sxs-lookup"><span data-stu-id="9d0db-245">For example, notice the first entry, `<s:fontSlot name="title">`.</span></span> <span data-ttu-id="9d0db-246">В этой записи описывает шрифт SharePoint с помощью стиля заголовка страницы.</span><span class="sxs-lookup"><span data-stu-id="9d0db-246">This entry describes which font SharePoint uses to style the title of the page.</span></span> <span data-ttu-id="9d0db-247">В этом разделе также определяет, какой шрифт будет использоваться для различных языков.</span><span class="sxs-lookup"><span data-stu-id="9d0db-247">This section also specifies which font will be used for different languages.</span></span>
    
    <span data-ttu-id="9d0db-248">**Примечание**  Можно загрузить пользовательских шрифтов в SharePoint и выберите пункт в каждую запись настраиваемого файла .eot, .woff, .ttf и .svg.</span><span class="sxs-lookup"><span data-stu-id="9d0db-248">**Note**  You can upload custom fonts to SharePoint and point each entry to a custom .eot, .woff, .ttf, and .svg file.</span></span> 

8. <span data-ttu-id="9d0db-249">Передача файла **параметров сайта** > **темы** > **15** папки.</span><span class="sxs-lookup"><span data-stu-id="9d0db-249">Upload the file to the **Site settings** > **Theme** > **15** folder.</span></span>
    
    <span data-ttu-id="9d0db-250">**Примечание**  Сохраните файл под новым именем файла (например, custom_font.spfont).</span><span class="sxs-lookup"><span data-stu-id="9d0db-250">**Note**  Save the file with a new file name (for example, custom_font.spfont).</span></span>

    <span data-ttu-id="9d0db-251">В следующей таблице показаны элементы страницы на шрифты, как они определены в файле .spfont.</span><span class="sxs-lookup"><span data-stu-id="9d0db-251">The following table maps page elements to fonts as they're defined in the .spfont file.</span></span>

|<span data-ttu-id="9d0db-252">**Элемент**</span><span class="sxs-lookup"><span data-stu-id="9d0db-252">**Element**</span></span>|<span data-ttu-id="9d0db-253">**Шрифт**</span><span class="sxs-lookup"><span data-stu-id="9d0db-253">**Font**</span></span>|<span data-ttu-id="9d0db-254">**Код**</span><span class="sxs-lookup"><span data-stu-id="9d0db-254">**Code**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="9d0db-255">Заголовок</span><span class="sxs-lookup"><span data-stu-id="9d0db-255">Title</span></span>|<span data-ttu-id="9d0db-256">Открыть Sans</span><span class="sxs-lookup"><span data-stu-id="9d0db-256">Open Sans</span></span>| `<s:cs typeface="Open Sans" />`|
|<span data-ttu-id="9d0db-257">Navigation</span><span class="sxs-lookup"><span data-stu-id="9d0db-257">Navigation</span></span>|<span data-ttu-id="9d0db-258">Roboto</span><span class="sxs-lookup"><span data-stu-id="9d0db-258">Roboto</span></span>| `<s:cs typeface="Roboto" />`|
|<span data-ttu-id="9d0db-259">Заголовки</span><span class="sxs-lookup"><span data-stu-id="9d0db-259">Headings</span></span>|<span data-ttu-id="9d0db-260">Trajan Pro</span><span class="sxs-lookup"><span data-stu-id="9d0db-260">Trajan Pro</span></span>| `<s:cs typeface="Trajan Pro" />`|
|<span data-ttu-id="9d0db-261">Body</span><span class="sxs-lookup"><span data-stu-id="9d0db-261">Body</span></span>|<span data-ttu-id="9d0db-262">Открыть Sans</span><span class="sxs-lookup"><span data-stu-id="9d0db-262">Open Sans</span></span>| `<s:cs typeface="Open Sans" />`|

<span data-ttu-id="9d0db-263">Возможно, чтобы убедиться, что некоторые настраиваемые шрифты доступны в браузерах пользователей.</span><span class="sxs-lookup"><span data-stu-id="9d0db-263">You might have to ensure that some custom fonts are available to users' browsers.</span></span> <span data-ttu-id="9d0db-264">Например если заголовки обращайтесь к Trajan специалистов шрифта, которая редко на компьютерах большинства пользователей, добавьте следующие объявления шрифтов в верхней части объявления < s:fontSlot >.</span><span class="sxs-lookup"><span data-stu-id="9d0db-264">For example, if the headings refer to a Trajan Pro font, which is uncommon on most users' computers, add the following font declarations at the top of the <s:fontSlot> declaration.</span></span> <span data-ttu-id="9d0db-265">Это гарантирует, что отображаются правильные шрифта.</span><span class="sxs-lookup"><span data-stu-id="9d0db-265">This will ensure that the correct font is displayed.</span></span> 

```XML
<s:latin typeface=" Trajan Pro" eotsrc="/SiteAssets/Trajan Pro.eot" woffsrc="/SiteAssets/Trajan Pro.woff" ttfsrc="/SiteAssets/Trajan Pro.ttf" svgsrc="/SiteAssets/Trajan Pro.svg"  />
```

## <a name="add-a-custom-theme-to-sharepoint"></a><span data-ttu-id="9d0db-266">Добавление пользовательской темы в SharePoint</span><span class="sxs-lookup"><span data-stu-id="9d0db-266">Add a custom theme to SharePoint</span></span>
<span data-ttu-id="9d0db-267"><a name="sectionSection2"> </a></span><span class="sxs-lookup"><span data-stu-id="9d0db-267"></span></span>

<span data-ttu-id="9d0db-268">После настройки главной страницей, .spcolor и .spfont файлы, добавьте их в каталог вариантов оформления, чтобы доступ к ним SharePoint.</span><span class="sxs-lookup"><span data-stu-id="9d0db-268">After you make your customizations to the master page, .spcolor, and .spfont files, add them to the Composed Looks directory so that SharePoint can access them.</span></span> 

1. <span data-ttu-id="9d0db-269">Перейти к **параметрам сайта**и в разделе **Коллекции веб-дизайнера**, выберите **Вариантов оформления**.</span><span class="sxs-lookup"><span data-stu-id="9d0db-269">Go to **Site settings**, and under **Web Designer Galleries**, select **Composed Looks**.</span></span> 
    
2. <span data-ttu-id="9d0db-270">Выберите ссылку **Создать элемент** в верхней левой.</span><span class="sxs-lookup"><span data-stu-id="9d0db-270">Choose the **new item** link at the top left.</span></span> <span data-ttu-id="9d0db-271">Откроется окно, как показано на рисунке 5.</span><span class="sxs-lookup"><span data-stu-id="9d0db-271">A window opens, as shown in Figure 5.</span></span>
    
    <span data-ttu-id="9d0db-272">**На рисунке 5. Вариантов оформления**</span><span class="sxs-lookup"><span data-stu-id="9d0db-272">**Figure 5. Composed looks**</span></span>

    ![Снимок экрана, которая показана страница новый вариант оформления](media/8155ba5d-9492-473d-b153-c3db566cbdec.png)

3. <span data-ttu-id="9d0db-274">Добавьте заголовок и имя для вариант оформления.</span><span class="sxs-lookup"><span data-stu-id="9d0db-274">Add a title and a name for your composed look.</span></span>
    
4. <span data-ttu-id="9d0db-275">Заполните оставшиеся поля.</span><span class="sxs-lookup"><span data-stu-id="9d0db-275">Complete the remaining field:</span></span>
    
    - <span data-ttu-id="9d0db-276">В поле **URL-адрес главной страницы** добавьте URL-адрес, предоставляемых темы, используемой главной страницы.</span><span class="sxs-lookup"><span data-stu-id="9d0db-276">In the **Master Page URL** field, add the URL of the master page you would like the theme to use.</span></span>
    
    - <span data-ttu-id="9d0db-277">В поле **URL-адрес темы** добавьте URL-адрес файла .spcolor.</span><span class="sxs-lookup"><span data-stu-id="9d0db-277">In the **Theme URL** field, add the URL of the .spcolor file.</span></span>
    
    - <span data-ttu-id="9d0db-278">В поле **URL-адрес изображения** включите URL-адрес изображения, которое вы хотите использовать в качестве фона.</span><span class="sxs-lookup"><span data-stu-id="9d0db-278">In the **Image URL** field, include the URL of an image that you want to use as a background.</span></span> <span data-ttu-id="9d0db-279">Это не требуется, если данный проект не вызываться для фонового изображения.</span><span class="sxs-lookup"><span data-stu-id="9d0db-279">This is not required if your design doesn't call for a background image.</span></span>
    
    - <span data-ttu-id="9d0db-280">В поле **URL-адрес схемы шрифтов** включите URL-адрес файла .spfont.</span><span class="sxs-lookup"><span data-stu-id="9d0db-280">In the **Font Scheme URL** field, include the URL of the .spfont file.</span></span>
    
    - <span data-ttu-id="9d0db-281">В поле **Порядок отображения** укажите порядок, в котором должен отображаться вариант оформления.</span><span class="sxs-lookup"><span data-stu-id="9d0db-281">In the **Display Order** field, indicate the order in which the composed look should be displayed.</span></span>
    
5. <span data-ttu-id="9d0db-282">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="9d0db-282">Choose **Save**.</span></span> <span data-ttu-id="9d0db-283">Запись темы теперь будет отображаться в списке **Вариантов оформления** .</span><span class="sxs-lookup"><span data-stu-id="9d0db-283">Your theme entry will now appear in the  **Composed Looks** list.</span></span>
    
<span data-ttu-id="9d0db-284">После добавления пользовательской темы в качестве вариант оформления, темы доступа пользователей и его применения к сайту, перейдя к **параметрам сайта** > **внешний вид и функции** > **Изменение внешнего вида**.</span><span class="sxs-lookup"><span data-stu-id="9d0db-284">After you add your custom theme to as a composed look, users can access the theme and apply it to a site by going to **Site settings** > **Look and Feel** > **Change the look**.</span></span> <span data-ttu-id="9d0db-285">На рисунке 6 показан пример раздела **Изменение внешнего вида** в **Настройках сайта**.</span><span class="sxs-lookup"><span data-stu-id="9d0db-285">Figure 6 shows an example of a **Change the look** section in **Site Settings**.</span></span>

<span data-ttu-id="9d0db-286">**На рисунке 6. Вариантов оформления, доступные в изменение внешнего вида**</span><span class="sxs-lookup"><span data-stu-id="9d0db-286">**Figure 6. Composed looks available in Change the look**</span></span>

![Снимок экрана, показывающий состоять выглядит доступны в настройках сайта > Изменение внешнего вида](media/11acb4ea-cff6-483c-890f-8c574e14f29d.png)

## <a name="what-does-the-theming-engine-do-when-a-user-applies-a-composed-look"></a><span data-ttu-id="9d0db-288">Что такое модуль темы? при включении вариант оформления</span><span class="sxs-lookup"><span data-stu-id="9d0db-288">What does the theming engine do when a user applies a composed look?</span></span>
<span data-ttu-id="9d0db-289"><a name="sectionSection3"> </a></span><span class="sxs-lookup"><span data-stu-id="9d0db-289"></span></span>

<span data-ttu-id="9d0db-290">Когда пользователь применяет вариант оформления, SharePoint копирует, преобразует и сохраняет CSS в базе данных контента.</span><span class="sxs-lookup"><span data-stu-id="9d0db-290">When a user applies a composed look, SharePoint copies, transforms, and stores CSS in the content database.</span></span> <span data-ttu-id="9d0db-291">Также recolors и хранятся изображения в базе данных контента.</span><span class="sxs-lookup"><span data-stu-id="9d0db-291">It also recolors and stores images in the content database.</span></span> <span data-ttu-id="9d0db-292">Как часть процесса Применение темы к сайту модуль темы извлекает шрифта и цвет значениями, полученными из указанного цветовая схема палитры и шрифта, обнаруженных в коллекцию тем корневого сайта.</span><span class="sxs-lookup"><span data-stu-id="9d0db-292">As part of the process of applying a theme to a site, the theming engine pulls color and font values from the specified color palette and font scheme found in the Theme Gallery of the root site.</span></span> <span data-ttu-id="9d0db-293">Чтобы применить главную страницу и файл .preview главной страницы (макет сайта), модуль темы извлекает главных страниц в коллекции главных страниц, которые имеют соответствующий файл .preview.</span><span class="sxs-lookup"><span data-stu-id="9d0db-293">To apply .master page and the master page .preview file (the site layout), the theming engine pulls master pages in the Master Page Gallery that have a corresponding .preview file.</span></span> 

<span data-ttu-id="9d0db-294">Когда он применяется вариант оформления, ядро сопоставляет параметры, указанные с определенным комментарии CSS, определяет модуль темы.</span><span class="sxs-lookup"><span data-stu-id="9d0db-294">When it applies a composed look, the engine maps the settings specified by specific CSS comments that the theming engine defines.</span></span> <span data-ttu-id="9d0db-295">На кухню engine темы сохраняет фонового изображения в ресурсах сайта, шкал и сжимает JPG и BMP изображений и ограничивает размер изображения GIF и PNG.</span><span class="sxs-lookup"><span data-stu-id="9d0db-295">Under the hood, the theming engine saves the background image to Site Assets, scales and compresses JPG and BMP images, and limits the size of GIF and PNG images.</span></span> 

<span data-ttu-id="9d0db-296">Когда вариант оформления применяется к сайту SharePoint, SharePoint, поиск и замена маркеры комментариев CSS путем внедрения значения, производные от вариант оформления в следующей строке в CSS-файл после маркера.</span><span class="sxs-lookup"><span data-stu-id="9d0db-296">When a composed look is applied to a SharePoint site, SharePoint finds and replaces CSS comment tokens by embedding a value derived from the composed look in the next line in the CSS file after the token.</span></span> <span data-ttu-id="9d0db-297">Это значение применяется к сайту SharePoint.</span><span class="sxs-lookup"><span data-stu-id="9d0db-297">This new value is applied to the SharePoint site.</span></span>

<span data-ttu-id="9d0db-298">В следующей таблице перечислены маркеры комментариев CSS.</span><span class="sxs-lookup"><span data-stu-id="9d0db-298">The following table lists the CSS comment tokens.</span></span>

|<span data-ttu-id="9d0db-299">**Маркер**</span><span class="sxs-lookup"><span data-stu-id="9d0db-299">**Token**</span></span>|<span data-ttu-id="9d0db-300">**Описание**</span><span class="sxs-lookup"><span data-stu-id="9d0db-300">**Description**</span></span>|<span data-ttu-id="9d0db-301">**Соответствующий параметр ApplyTheme**</span><span class="sxs-lookup"><span data-stu-id="9d0db-301">**Corresponding ApplyTheme parameter**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="9d0db-302">/ * ReplaceBGImage * /</span><span class="sxs-lookup"><span data-stu-id="9d0db-302">/* ReplaceBGImage */</span></span>|<span data-ttu-id="9d0db-303">Текущее фоновое изображение swaps с изображением в назначенный состоит внешний вид URL-адрес изображения.</span><span class="sxs-lookup"><span data-stu-id="9d0db-303">Swaps current background image with the image in the assigned composed look image URL.</span></span>|<span data-ttu-id="9d0db-304">backgroundImageUrl</span><span class="sxs-lookup"><span data-stu-id="9d0db-304">backgroundImageUrl</span></span>|
|<span data-ttu-id="9d0db-305">/ * ReplaceFont * /</span><span class="sxs-lookup"><span data-stu-id="9d0db-305">/* ReplaceFont */</span></span>|<span data-ttu-id="9d0db-306">Меняет местами текущего шрифта с одним из шрифтов в URL-адрес схемы шрифтов из назначенного вариант оформления.</span><span class="sxs-lookup"><span data-stu-id="9d0db-306">Swaps the current font with one of the fonts found in the font scheme URL of the assigned composed look.</span></span>|<span data-ttu-id="9d0db-307">fontSchemeUrl</span><span class="sxs-lookup"><span data-stu-id="9d0db-307">fontSchemeUrl</span></span>|
|<span data-ttu-id="9d0db-308">/ * ReplaceColor * /</span><span class="sxs-lookup"><span data-stu-id="9d0db-308">/* ReplaceColor */</span></span>|<span data-ttu-id="9d0db-309">Меняет местами текущего цвета с одним из цветами, указанными в ячейку цвет в цветовой палитры URL-адрес назначенный вариант оформления.</span><span class="sxs-lookup"><span data-stu-id="9d0db-309">Swaps the current color with one of the colors specified in a color slot in the color palette URL of the assigned composed look.</span></span>|<span data-ttu-id="9d0db-310">colorPaletteUrl</span><span class="sxs-lookup"><span data-stu-id="9d0db-310">colorPaletteUrl</span></span>|
|<span data-ttu-id="9d0db-311">/ * RecolorImage * /</span><span class="sxs-lookup"><span data-stu-id="9d0db-311">/* RecolorImage */</span></span>|<span data-ttu-id="9d0db-312">Recolors изображений с помощью оттенки или заполнения.</span><span class="sxs-lookup"><span data-stu-id="9d0db-312">Recolors images using tinting or filling.</span></span> ||

## <a name="additional-resources"></a><span data-ttu-id="9d0db-313">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="9d0db-313">Additional resources</span></span>
<span data-ttu-id="9d0db-314"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="9d0db-314"></span></span>

-  [<span data-ttu-id="9d0db-315">Решения для создания фирменного стиля и настройки страниц на сайтах SharePoint</span><span class="sxs-lookup"><span data-stu-id="9d0db-315">SharePoint site branding and page customization solutions</span></span>](SharePoint-site-branding-and-page-customization-solutions.md)
    
-  [<span data-ttu-id="9d0db-316">Фирменная символика и решения для SharePoint 2013 и SharePoint Online по подготовке сайта</span><span class="sxs-lookup"><span data-stu-id="9d0db-316">Branding and site provisioning solutions for SharePoint 2013 and SharePoint Online</span></span>](Branding-and-site-provisioning-solutions-for-SharePoint.md)
