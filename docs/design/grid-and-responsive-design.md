---
title: "Сетка SharePoint и адаптивный дизайн"
description: "Базовая сетка страницы и пограничные значения, или ключевые размеры экрана, при которых будет меняться разметка страниц."
ms.date: 01/23/2018
ms.openlocfilehash: b94980b57682e519091272bcf3801fcffcf854ff
ms.sourcegitcommit: 0ad5aeee2c5efc47eb57e050581e4f411c4be643
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/29/2018
---
# <a name="sharepoint-grid-and-responsive-design"></a><span data-ttu-id="3c187-103">Сетка SharePoint и адаптивный дизайн</span><span class="sxs-lookup"><span data-stu-id="3c187-103">SharePoint grid and responsive design</span></span>
 
<span data-ttu-id="3c187-104">Адаптивные интерфейсы легко масштабируются на различных устройствах, чтобы содержимое лучше отображалась на экранах разных размеров.</span><span class="sxs-lookup"><span data-stu-id="3c187-104">Responsive experiences seamlessly scale across devices, to better display your content on a range of different screen sizes.</span></span> <span data-ttu-id="3c187-105">Адаптивный дизайн также избавляет от необходимости создавать несколько версий страниц сайта для поддержки различных устройств.</span><span class="sxs-lookup"><span data-stu-id="3c187-105">Responsive design also eliminates the need to build multiple versions of your site pages to support different devices.</span></span>  

<span data-ttu-id="3c187-106">В рекомендациях по проектированию адаптивных страниц в среде разработки SharePoint используется система адаптивной сетки, основанная на [Office UI Fabric](https://developer.microsoft.com/ru-RU/fabric).</span><span class="sxs-lookup"><span data-stu-id="3c187-106">The design guidance for responsive pages in the SharePoint authoring environment incorporates a responsive grid system that is based on [Office UI Fabric](https://developer.microsoft.com/ru-RU/fabric).</span></span> <span data-ttu-id="3c187-107">В этой статье описаны базовая система сетки страниц и пограничные значения, или ключевые размеры экрана, при использовании которых будет меняться разметка страниц.</span><span class="sxs-lookup"><span data-stu-id="3c187-107">This article describes the underlying page grid system and the breakpoints, or key screen sizes where the layout of the pages will change.</span></span> 


![Страница SharePoint на нескольких устройствах](../images/design-grid-responsive-overview.png)



## <a name="page-type-grids"></a><span data-ttu-id="3c187-109">Сетки типов страниц</span><span class="sxs-lookup"><span data-stu-id="3c187-109">Page type grids</span></span> 

<span data-ttu-id="3c187-110">Для каждой страницы в среде разработки SharePoint могут действовать собственные правила касательно применения адаптивной сетки Fabric.</span><span class="sxs-lookup"><span data-stu-id="3c187-110">Each page type in the SharePoint authoring experience can have its own rules for how it applies the Fabric responsive grid.</span></span> <span data-ttu-id="3c187-111">Благодаря этому каждая страница будет хорошо выглядеть независимо от того, для какого устройства она разработана, а интерфейс будет оптимизирован для соответствующей среды.</span><span class="sxs-lookup"><span data-stu-id="3c187-111">This is to ensure that each page looks great, regardless of what device it's designed for, and that the experience is optimized for that environment.</span></span> <span data-ttu-id="3c187-112">Базовая сетка в классических средах SharePoint представляет собой структуру из 12 столбцов.</span><span class="sxs-lookup"><span data-stu-id="3c187-112">The basic grid in the SharePoint desktop experiences is a 12 column structure.</span></span> <span data-ttu-id="3c187-113">Количество столбцов и интервал между ними регулируются в соответствии с шириной экрана.</span><span class="sxs-lookup"><span data-stu-id="3c187-113">The number of columns and gutter width will adjust based on the screen width.</span></span> 

<span data-ttu-id="3c187-114">В приведенных ниже разделах представлена базовая структура сетки, применяемая на страницах SharePoint разных типов, чтобы помочь вам лучше понять, как сетка регулируется в соответствии с потребностями интерфейса и устройства.</span><span class="sxs-lookup"><span data-stu-id="3c187-114">The following sections show the basic grid structure applied across different types of SharePoint pages, to help you better understand how the grid adjusts to support the experience and device needs.</span></span>


![Схема сетки с двенадцатью столбцами](../images/design-grid_diagram.png)

<br/>

### <a name="team-sites"></a><span data-ttu-id="3c187-116">Сайты групп</span><span class="sxs-lookup"><span data-stu-id="3c187-116">Team sites</span></span>

<span data-ttu-id="3c187-117">Область контента для сайта группы закреплена в левой части экрана.</span><span class="sxs-lookup"><span data-stu-id="3c187-117">The content area for a team site is locked to the left.</span></span> <span data-ttu-id="3c187-118">На сайтах групп область навигации расположена слева, поэтому при добавлении веб-частей на сетку и перестраивании страницы она не перекрывается.</span><span class="sxs-lookup"><span data-stu-id="3c187-118">Team sites have a left navigation, therefore the space web parts occupy on the gird and the reflow behavior respects the space given to the navigation.</span></span> <span data-ttu-id="3c187-119">Максимальная ширина области контента на сайте группы — 1204 пикселя, а минимальный размер — 320 пикселей для поддержки мобильных устройств.</span><span class="sxs-lookup"><span data-stu-id="3c187-119">The max width of the content area of a Team site is 1204px and the minimum size is 320px for mobile support.</span></span>

![Сайт группы](../images/design-grid-team-site.png)

<br/>

<span data-ttu-id="3c187-121">В приведенных ниже примерах показано, как сетка регулируется с учетом основных пограничных значений на сайте группы.</span><span class="sxs-lookup"><span data-stu-id="3c187-121">The following examples show how the grid adjusts between key breakpoints on a team site.</span></span>

#### <a name="small-320-x-568"></a><span data-ttu-id="3c187-122">Маленькая (320 x 568)</span><span class="sxs-lookup"><span data-stu-id="3c187-122">Small 320 x 568</span></span>
<span data-ttu-id="3c187-123">Маленькая сетка содержит один столбец по центру с полями по 20 пикселей слева и справа.</span><span class="sxs-lookup"><span data-stu-id="3c187-123">The small size has a single centered column area, with 20px margins left and right.</span></span>

![Маленькая сетка на сайте группы](../images/design-grid-Team-site-S-Canvas-no-column.png)

<br/>

#### <a name="medium-480-x-854"></a><span data-ttu-id="3c187-125">Средняя (480 x 854)</span><span class="sxs-lookup"><span data-stu-id="3c187-125">Medium 480 x 854</span></span>
<span data-ttu-id="3c187-126">Средняя сетка содержит 12 столбцов с интервалами по 16 пикселей.</span><span class="sxs-lookup"><span data-stu-id="3c187-126">The medium size has 12 columns, with 16px gutters.</span></span>

![Средняя сетка на сайте группы](../images/design-grid-Team-site-M-Canvas-16px-gutters.png)

<br/>

#### <a name="large-640-x-1024"></a><span data-ttu-id="3c187-128">Крупная (640 x 1024)</span><span class="sxs-lookup"><span data-stu-id="3c187-128">Large 640 x 1024</span></span>
<span data-ttu-id="3c187-129">Крупная сетка содержит 12 столбцов с интервалами по 24 пикселя.</span><span class="sxs-lookup"><span data-stu-id="3c187-129">The large size has 12 columns, with 24px gutters.</span></span>

![Крупная сетка на сайте группы](../images/design-grid-Team-site-L-Canvas-24px-gutters.png)

<br/>

#### <a name="xl-1024-x-768"></a><span data-ttu-id="3c187-131">XL (1024 x 768)</span><span class="sxs-lookup"><span data-stu-id="3c187-131">XL 1024 x 768</span></span>
<span data-ttu-id="3c187-132">Сетка размера XL содержит 12 столбцов с интервалами по 24 пикселя.</span><span class="sxs-lookup"><span data-stu-id="3c187-132">The XL size has 12 columns, with 24px gutters.</span></span>

![Сетка размера XL на сайте группы](../images/design-grid-Team-site-XL-Canvas-24px-gutters.png)

<br/>

#### <a name="xxl-1366-x-768"></a><span data-ttu-id="3c187-134">XXL (1366 x 768)</span><span class="sxs-lookup"><span data-stu-id="3c187-134">XXL 1366 x 768</span></span>
<span data-ttu-id="3c187-135">Сетка размера XXL содержит 12 столбцов с интервалами по 32 пикселя.</span><span class="sxs-lookup"><span data-stu-id="3c187-135">The XXL size has 12 columns, with 32px gutters.</span></span>

![Сетка размера XXL на сайте группы](../images/design-grid-Team-site-XXL-Canvas-32px-gutters.png)

<br/>

#### <a name="xxxl-1920-x-1080"></a><span data-ttu-id="3c187-137">XXXL (1920 x 1080)</span><span class="sxs-lookup"><span data-stu-id="3c187-137">XXXL 1920 x 1080</span></span>
<span data-ttu-id="3c187-138">Сетка размера XXXL содержит 12 столбцов с интервалами по 32 пикселя.</span><span class="sxs-lookup"><span data-stu-id="3c187-138">The XXXL size has 12 columns, with 32px gutters.</span></span>

![Сетка размера XXXL на сайте группы](../images/design-grid-Team-site-XXXL-Canvas-32px-gutters-maxwidth-1204.png)

<br/>

#### <a name="team-site-multicolumn-pages-and-web-parts"></a><span data-ttu-id="3c187-140">Страницы с несколькими столбцами и веб-части на сайтах групп</span><span class="sxs-lookup"><span data-stu-id="3c187-140">Team site multicolumn pages and web parts</span></span>
<span data-ttu-id="3c187-141">Веб-части масштабируются по горизонтали в зависимости от разметки страницы.</span><span class="sxs-lookup"><span data-stu-id="3c187-141">Web parts will scale horizontally depending on the page layout.</span></span> <span data-ttu-id="3c187-142">Ниже показано, как размер веб-части корректируется, чтобы поместилась область навигации слева.</span><span class="sxs-lookup"><span data-stu-id="3c187-142">The following example shows how the size of a web part adjusts to accommodate the left navigation.</span></span>

![Страница с несколькими столбцами и веб-частями на сайте группы](../images/design-grid-Team-site-web-parts.png)


### <a name="communication-sites"></a><span data-ttu-id="3c187-144">Сайты для общения</span><span class="sxs-lookup"><span data-stu-id="3c187-144">Communication sites</span></span>

<span data-ttu-id="3c187-145">На сайтах для общения область навигации расположена вверху, а область контента — по центру.</span><span class="sxs-lookup"><span data-stu-id="3c187-145">Communication sites have a top navigation and a centered content area.</span></span> <span data-ttu-id="3c187-146">Максимальная ширина области контента на сайте для общения — 1204 пикселей, а минимальный размер — 320 пикселей для поддержки мобильных устройств.</span><span class="sxs-lookup"><span data-stu-id="3c187-146">The maximum width of the content area of a communication site is 1204px and the minimum size is 320px for mobile support.</span></span>

![Сайт для общения](../images/design-grid-communication_site.png)

<br/>

<span data-ttu-id="3c187-148">В приведенных ниже примерах показано, как сетка регулируется с учетом основных пограничных значений на сайте для общения.</span><span class="sxs-lookup"><span data-stu-id="3c187-148">The following examples show how the grid adjusts between key breakpoints on a communication site.</span></span>

#### <a name="small-320-x-568"></a><span data-ttu-id="3c187-149">Маленькая (320 x 568)</span><span class="sxs-lookup"><span data-stu-id="3c187-149">Small 320 x 568</span></span>
<span data-ttu-id="3c187-150">Маленькая сетка содержит один столбец по центру с полями по 20 пикселей слева и справа.</span><span class="sxs-lookup"><span data-stu-id="3c187-150">The small size has a single centered column area, with 20px margins left and right.</span></span>

![Маленькая сетка на сайте для общения](../images/design-grid-Communication-site-S-Canvas-no-column.png)

<br/>

#### <a name="medium-480-x-854"></a><span data-ttu-id="3c187-152">Средняя (480 x 854)</span><span class="sxs-lookup"><span data-stu-id="3c187-152">Medium 480 x 854</span></span>
<span data-ttu-id="3c187-153">Средняя сетка содержит 12 столбцов с интервалами по 16 пикселей.</span><span class="sxs-lookup"><span data-stu-id="3c187-153">The medium size has 12 columns, with 16px gutters.</span></span>

![Средняя сетка на сайте для общения](../images/design-grid-Communication-site-M-Canvas-16px-gutters.png)

<br/>

#### <a name="large-640-x-1024"></a><span data-ttu-id="3c187-155">Крупная (640 x 1024)</span><span class="sxs-lookup"><span data-stu-id="3c187-155">Large 640 x 1024</span></span>
<span data-ttu-id="3c187-156">Крупная сетка содержит 12 столбцов с интервалами по 24 пикселя.</span><span class="sxs-lookup"><span data-stu-id="3c187-156">The large size has 12 columns, with 24px gutters.</span></span>

![Крупная сетка на сайте для общения](../images/design-grid-Communication-site-L-Canvas-24px-gutters.png)

<br/>

#### <a name="xl-1024-x-768"></a><span data-ttu-id="3c187-158">XL (1024 x 768)</span><span class="sxs-lookup"><span data-stu-id="3c187-158">XL 1024 x 768</span></span>
<span data-ttu-id="3c187-159">Сетка размера XL содержит 12 столбцов с интервалами по 24 пикселя.</span><span class="sxs-lookup"><span data-stu-id="3c187-159">The XL size has 12 columns, with 24px gutters.</span></span>

![Сетка размера XL на сайте для общения](../images/design-grid-Communication-site-XL-Canvas-24px-gutters.png)

<br/>

#### <a name="xxl-1366-x-768"></a><span data-ttu-id="3c187-161">XXL (1366 x 768)</span><span class="sxs-lookup"><span data-stu-id="3c187-161">XXL 1366 x 768</span></span>
<span data-ttu-id="3c187-162">Сетка размера XXL содержит 12 столбцов с интервалами по 32 пикселя.</span><span class="sxs-lookup"><span data-stu-id="3c187-162">The XXL size has 12 columns, with 32px gutters.</span></span>

![Сетка размера XXL на сайте для общения](../images/design-grid-Communication-site-XXL-Canvas-32px-gutters-maxwidth-1204.png)

<br/>

#### <a name="xxxl-1920-x-1080"></a><span data-ttu-id="3c187-164">XXXL (1920 x 1080)</span><span class="sxs-lookup"><span data-stu-id="3c187-164">XXXL 1920 x 1080</span></span>
<span data-ttu-id="3c187-165">Сетка размера XXXL содержит 12 столбцов с интервалами по 32 пикселя.</span><span class="sxs-lookup"><span data-stu-id="3c187-165">The XXXL size has 12 columns, with 32px gutters.</span></span>

![Сетка размера XXXL на сайте для общения](../images/design-grid-Communication-site-XXXL-Canvas-32px-gutters-maxwidth-1204.png)

<br/>

#### <a name="communication-site-multicolumn-pages-and-web-parts"></a><span data-ttu-id="3c187-167">Страницы с несколькими столбцами и веб-части на сайтах для общения</span><span class="sxs-lookup"><span data-stu-id="3c187-167">Communication site multicolumn pages and web parts</span></span>
<span data-ttu-id="3c187-168">Веб-части масштабируются по горизонтали в зависимости от разметки страницы.</span><span class="sxs-lookup"><span data-stu-id="3c187-168">Web parts will scale horizontally depending on the page layout.</span></span> <span data-ttu-id="3c187-169">Ниже показаны сайт для общения и веб-части для макетов с 1–3 столбцами.</span><span class="sxs-lookup"><span data-stu-id="3c187-169">This example shows a communcation site and web parts for single to three column layouts.</span></span>

![Страница с несколькими столбцами и веб-частями на сайте для общения](../images/design-grid-Communciation-site-web-parts.png)



## <a name="breakpoints"></a><span data-ttu-id="3c187-171">Пограничные значения</span><span class="sxs-lookup"><span data-stu-id="3c187-171">Breakpoints</span></span> 

<span data-ttu-id="3c187-172">Чтобы страница правильно перестраивалась на экранах всех размеров, пользовательский интерфейс SharePoint должен адаптировать разметку с учетом следующих пограничных значений ширины:</span><span class="sxs-lookup"><span data-stu-id="3c187-172">To create a smooth flowing experience between screen sizes, the SharePoint UI should adapt layouts for the following breakpoint widths:</span></span> 

- <span data-ttu-id="3c187-173">320 пкс</span><span class="sxs-lookup"><span data-stu-id="3c187-173">320 px</span></span>
- <span data-ttu-id="3c187-174">1024 пкс</span><span class="sxs-lookup"><span data-stu-id="3c187-174">1024 px</span></span>
- <span data-ttu-id="3c187-175">1366 пкс</span><span class="sxs-lookup"><span data-stu-id="3c187-175">1366 px</span></span>
- <span data-ttu-id="3c187-176">1920 пкс</span><span class="sxs-lookup"><span data-stu-id="3c187-176">1920 px</span></span>
 
<span data-ttu-id="3c187-177">При использовании этих пограничных значений следует учитывать, как сместится контент после оптимизации окна просмотра в соответствии с ближайшим пограничным значением.</span><span class="sxs-lookup"><span data-stu-id="3c187-177">Within these breakpoints, you should take into consideration how your content will shift when the viewport size becomes optimized for the nearest breakpoint.</span></span> <span data-ttu-id="3c187-178">Обратите внимание, что эта схема представлена в иллюстративных целях и не является точной.</span><span class="sxs-lookup"><span data-stu-id="3c187-178">Note that this diagram is for illustration only and is not pixel accurate.</span></span>


![Схема SharePoint с пограничными значениями](../images/design-grid-breakpoints.png)

<br/>

<span data-ttu-id="3c187-180">Адаптивная сетка на сайтах групп и сайтах для общения регулируется при переходе от больших пограничных значений к значениям для мобильных приложений.</span><span class="sxs-lookup"><span data-stu-id="3c187-180">The responsive grid for both team sites and communication sites adjusts when going from large breakpoints to mobile breakpoints.</span></span> <span data-ttu-id="3c187-181">Так сайт корректируется для устройства и размера его экрана.</span><span class="sxs-lookup"><span data-stu-id="3c187-181">This optimizes the site for the device and screen size.</span></span> <span data-ttu-id="3c187-182">В приведенной ниже таблице описаны размеры сетки при различных пограничных значениях для размеров экранов популярных устройств.</span><span class="sxs-lookup"><span data-stu-id="3c187-182">The following table describes the grid sizes at various breakpoints based on popular device sizes.</span></span>



| <span data-ttu-id="3c187-183">Ширина окна</span><span class="sxs-lookup"><span data-stu-id="3c187-183">Window width</span></span> | <span data-ttu-id="3c187-184">Устройство</span><span class="sxs-lookup"><span data-stu-id="3c187-184">Device</span></span>                  | <span data-ttu-id="3c187-185">Пограничное значение</span><span class="sxs-lookup"><span data-stu-id="3c187-185">Breakpoint</span></span> | <span data-ttu-id="3c187-186">Столбцы</span><span class="sxs-lookup"><span data-stu-id="3c187-186">Columns</span></span> | <span data-ttu-id="3c187-187">Интервал</span><span class="sxs-lookup"><span data-stu-id="3c187-187">Gutter</span></span> | <span data-ttu-id="3c187-188">Максимальное количество столбцов для раздела</span><span class="sxs-lookup"><span data-stu-id="3c187-188">Max columns per section</span></span> |
|:-------------|:------------------------|:-----------|:-------:|:------:|:-----------------------:|
| <span data-ttu-id="3c187-189">320</span><span class="sxs-lookup"><span data-stu-id="3c187-189">320</span></span>          | <span data-ttu-id="3c187-190">iPhone 5/SE, 320 x 568</span><span class="sxs-lookup"><span data-stu-id="3c187-190">iPhone 5/SE,320x568</span></span>     | <span data-ttu-id="3c187-191">Малый</span><span class="sxs-lookup"><span data-stu-id="3c187-191">Small</span></span>      | <span data-ttu-id="3c187-192">1</span><span class="sxs-lookup"><span data-stu-id="3c187-192">1</span></span>       | <span data-ttu-id="3c187-193">Н/д</span><span class="sxs-lookup"><span data-stu-id="3c187-193">N/A</span></span>    | <span data-ttu-id="3c187-194">1</span><span class="sxs-lookup"><span data-stu-id="3c187-194">1</span></span>                       |
| <span data-ttu-id="3c187-195">480</span><span class="sxs-lookup"><span data-stu-id="3c187-195">480</span></span>          | <span data-ttu-id="3c187-196">Устройство с 6-дюймовым экраном</span><span class="sxs-lookup"><span data-stu-id="3c187-196">6" device</span></span>               | <span data-ttu-id="3c187-197">Средний</span><span class="sxs-lookup"><span data-stu-id="3c187-197">Medium</span></span>     | <span data-ttu-id="3c187-198">1</span><span class="sxs-lookup"><span data-stu-id="3c187-198">1</span></span>       | <span data-ttu-id="3c187-199">Н/д</span><span class="sxs-lookup"><span data-stu-id="3c187-199">N/A</span></span>    | <span data-ttu-id="3c187-200">1</span><span class="sxs-lookup"><span data-stu-id="3c187-200">1</span></span>                       |
| <span data-ttu-id="3c187-201">640</span><span class="sxs-lookup"><span data-stu-id="3c187-201">640</span></span>          | <span data-ttu-id="3c187-202">Устройство с 8-дюймовым экраном</span><span class="sxs-lookup"><span data-stu-id="3c187-202">8" device</span></span>               | <span data-ttu-id="3c187-203">Крупный</span><span class="sxs-lookup"><span data-stu-id="3c187-203">Large</span></span>      | <span data-ttu-id="3c187-204">12</span><span class="sxs-lookup"><span data-stu-id="3c187-204">1.2</span></span>      | <span data-ttu-id="3c187-205">16</span><span class="sxs-lookup"><span data-stu-id="3c187-205">1.6</span></span>     | <span data-ttu-id="3c187-206">2</span><span class="sxs-lookup"><span data-stu-id="3c187-206">2</span></span>                       |
| <span data-ttu-id="3c187-207">768</span><span class="sxs-lookup"><span data-stu-id="3c187-207">768</span></span>          | <span data-ttu-id="3c187-208">iPad с книжной ориентацией, 768 x 1024</span><span class="sxs-lookup"><span data-stu-id="3c187-208">iPad portrait 768x1024</span></span>  | <span data-ttu-id="3c187-209">Крупный</span><span class="sxs-lookup"><span data-stu-id="3c187-209">Large</span></span>      | <span data-ttu-id="3c187-210">12</span><span class="sxs-lookup"><span data-stu-id="3c187-210">1.2</span></span>      | <span data-ttu-id="3c187-211">24</span><span class="sxs-lookup"><span data-stu-id="3c187-211">2.4</span></span>     | <span data-ttu-id="3c187-212">2</span><span class="sxs-lookup"><span data-stu-id="3c187-212">2</span></span>                       |
| <span data-ttu-id="3c187-213">1024</span><span class="sxs-lookup"><span data-stu-id="3c187-213">Default: 1024</span></span>         | <span data-ttu-id="3c187-214">iPad с альбомной ориентацией, 1024 x 768</span><span class="sxs-lookup"><span data-stu-id="3c187-214">iPad landscape 1024x768</span></span> | <span data-ttu-id="3c187-215">Размер XL</span><span class="sxs-lookup"><span data-stu-id="3c187-215">X-Large</span></span>    | <span data-ttu-id="3c187-216">12</span><span class="sxs-lookup"><span data-stu-id="3c187-216">1.2</span></span>      | <span data-ttu-id="3c187-217">24</span><span class="sxs-lookup"><span data-stu-id="3c187-217">2.4</span></span>     | <span data-ttu-id="3c187-218">3</span><span class="sxs-lookup"><span data-stu-id="3c187-218">3</span></span>                       |
| <span data-ttu-id="3c187-219">1368</span><span class="sxs-lookup"><span data-stu-id="3c187-219">1368</span></span>         | <span data-ttu-id="3c187-220">Surface Pro 3, 1368 x 912</span><span class="sxs-lookup"><span data-stu-id="3c187-220">Surface Pro 3 1368x912</span></span>  | <span data-ttu-id="3c187-221">Размер XXL</span><span class="sxs-lookup"><span data-stu-id="3c187-221">XX-Large</span></span>   | <span data-ttu-id="3c187-222">12</span><span class="sxs-lookup"><span data-stu-id="3c187-222">1.2</span></span>      | <span data-ttu-id="3c187-223">32</span><span class="sxs-lookup"><span data-stu-id="3c187-223">3.2</span></span>     | <span data-ttu-id="3c187-224">3</span><span class="sxs-lookup"><span data-stu-id="3c187-224">3</span></span>                       |
| <span data-ttu-id="3c187-225">1440</span><span class="sxs-lookup"><span data-stu-id="3c187-225">1440</span></span>         | <span data-ttu-id="3c187-226">Surface Pro 4, 1440 x 960</span><span class="sxs-lookup"><span data-stu-id="3c187-226">Surface Pro 4 1440x960</span></span>  | <span data-ttu-id="3c187-227">Размер XXL</span><span class="sxs-lookup"><span data-stu-id="3c187-227">XX-Large</span></span>   | <span data-ttu-id="3c187-228">12</span><span class="sxs-lookup"><span data-stu-id="3c187-228">1.2</span></span>      | <span data-ttu-id="3c187-229">32</span><span class="sxs-lookup"><span data-stu-id="3c187-229">3.2</span></span>     | <span data-ttu-id="3c187-230">3</span><span class="sxs-lookup"><span data-stu-id="3c187-230">3</span></span>                       |
| <span data-ttu-id="3c187-231">1600</span><span class="sxs-lookup"><span data-stu-id="3c187-231">1600</span></span>         | <span data-ttu-id="3c187-232">Веб-браузер, 1600 x 900</span><span class="sxs-lookup"><span data-stu-id="3c187-232">Web 1600x900</span></span>            | <span data-ttu-id="3c187-233">Размер XXL</span><span class="sxs-lookup"><span data-stu-id="3c187-233">XX-Large</span></span>   | <span data-ttu-id="3c187-234">12</span><span class="sxs-lookup"><span data-stu-id="3c187-234">1.2</span></span>      | <span data-ttu-id="3c187-235">32</span><span class="sxs-lookup"><span data-stu-id="3c187-235">3.2</span></span>     | <span data-ttu-id="3c187-236">3</span><span class="sxs-lookup"><span data-stu-id="3c187-236">3</span></span>                       |
| <span data-ttu-id="3c187-237">1920</span><span class="sxs-lookup"><span data-stu-id="3c187-237">1920</span></span>         | <span data-ttu-id="3c187-238">Веб-браузер, 1920 x 1080</span><span class="sxs-lookup"><span data-stu-id="3c187-238">Web 1920x1080</span></span>           | <span data-ttu-id="3c187-239">Размер XXXL</span><span class="sxs-lookup"><span data-stu-id="3c187-239">XXX-Large</span></span>  | <span data-ttu-id="3c187-240">12</span><span class="sxs-lookup"><span data-stu-id="3c187-240">1.2</span></span>      | <span data-ttu-id="3c187-241">32</span><span class="sxs-lookup"><span data-stu-id="3c187-241">3.2</span></span>     | <span data-ttu-id="3c187-242">3</span><span class="sxs-lookup"><span data-stu-id="3c187-242">3</span></span>                       |

<br/>

## <a name="see-also"></a><span data-ttu-id="3c187-243">См. также</span><span class="sxs-lookup"><span data-stu-id="3c187-243">See also</span></span>

- [<span data-ttu-id="3c187-244">Набор инструментов и ресурсы для дизайна</span><span class="sxs-lookup"><span data-stu-id="3c187-244">Design toolkit and assets</span></span>](https://developer.microsoft.com/ru-RU/fabric#/resources)
- [<span data-ttu-id="3c187-245">Принципы дизайна SharePoint</span><span class="sxs-lookup"><span data-stu-id="3c187-245">Designing great SharePoint experiences</span></span>](design-guidance-overview.md)


