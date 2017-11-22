---
title: "Сетка SharePoint и адаптивный дизайн"
ms.date: 9/25/2017
ms.openlocfilehash: 1025e1863d03bad9056d74c87307a7a1e4c8f103
ms.sourcegitcommit: 1b295a186814ca6ab13dda1a17e34dc69a61d81e
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="sharepoint-grid-and-responsive-design"></a><span data-ttu-id="ecb6c-102">Сетка SharePoint и адаптивный дизайн</span><span class="sxs-lookup"><span data-stu-id="ecb6c-102">SharePoint grid and responsive design</span></span>
 
<span data-ttu-id="ecb6c-103">Адаптивные интерфейсы легко масштабируются на различных устройствах, чтобы содержимое лучше отображалась на экранах разных размеров.</span><span class="sxs-lookup"><span data-stu-id="ecb6c-103">Responsive experiences seamlessly scale across devices, to better display your content on a range of different screen sizes.</span></span> <span data-ttu-id="ecb6c-104">Адаптивный дизайн также избавляет от необходимости создавать несколько версий страниц сайта для поддержки различных устройств.</span><span class="sxs-lookup"><span data-stu-id="ecb6c-104">Responsive design also eliminates the need to build multiple versions of your site pages to support different devices.</span></span>  

<span data-ttu-id="ecb6c-105">В рекомендациях по проектированию адаптивных страниц в среде разработки SharePoint используется система адаптивной сетки, основанная на [Office UI Fabric](https://dev.office.com/fabric).</span><span class="sxs-lookup"><span data-stu-id="ecb6c-105">The design guidance for responsive pages in the SharePoint authoring environment incorporates a responsive grid system that is based on [Office UI Fabric](https://dev.office.com/fabric).</span></span> <span data-ttu-id="ecb6c-106">В этой статье описаны базовая система сетки страниц и пограничные значения, или ключевые размеры экрана, при использовании которых будет меняться разметка страниц.</span><span class="sxs-lookup"><span data-stu-id="ecb6c-106">This article describes the underlying page grid system and the breakpoints, or key screen sizes where the layout of the pages will change.</span></span> 


![Страница SharePoint на нескольких устройствах](../images/design-grid-responsive-overview.png)



## <a name="page-type-grids"></a><span data-ttu-id="ecb6c-108">Сетки типов страниц</span><span class="sxs-lookup"><span data-stu-id="ecb6c-108">Page type grids</span></span> 

<span data-ttu-id="ecb6c-109">Для каждой страницы в среде разработки SharePoint могут действовать собственные правила касательно применения адаптивной сетки Fabric.</span><span class="sxs-lookup"><span data-stu-id="ecb6c-109">Each page type in the SharePoint authoring experience can have its own rules for how it applies the Fabric responsive grid.</span></span> <span data-ttu-id="ecb6c-110">Благодаря этому каждая страница будет хорошо выглядеть независимо от того, для какого устройства она разработана, а интерфейс будет оптимизирован для соответствующей среды.</span><span class="sxs-lookup"><span data-stu-id="ecb6c-110">This is to ensure that each page looks great, regardless of what device it's designed for, and that the experience is optimized for that environment.</span></span> <span data-ttu-id="ecb6c-111">Базовая сетка в классических средах SharePoint представляет собой структуру из 12 столбцов.</span><span class="sxs-lookup"><span data-stu-id="ecb6c-111">The basic grid in the SharePoint desktop experiences is a 12 column structure.</span></span> <span data-ttu-id="ecb6c-112">Количество столбцов и интервал между ними регулируются в соответствии с шириной экрана.</span><span class="sxs-lookup"><span data-stu-id="ecb6c-112">The number of columns and gutter width will adjust based on the screen width.</span></span> 

<span data-ttu-id="ecb6c-113">В приведенных ниже разделах представлена базовая структура сетки, применяемая на страницах SharePoint разных типов, чтобы помочь вам лучше понять, как сетка регулируется в соответствии с потребностями интерфейса и устройства.</span><span class="sxs-lookup"><span data-stu-id="ecb6c-113">The following sections show the basic grid structure applied across different types of SharePoint pages, to help you better understand how the grid adjusts to support the experience and device needs.</span></span>


![Схема сетки с двенадцатью столбцами](../images/design-grid_diagram.png)



### <a name="team-sites"></a><span data-ttu-id="ecb6c-115">Сайты групп</span><span class="sxs-lookup"><span data-stu-id="ecb6c-115">Team sites</span></span>

<span data-ttu-id="ecb6c-116">Область контента для сайта группы закреплена в левой части экрана.</span><span class="sxs-lookup"><span data-stu-id="ecb6c-116">The content area for a team site is locked to the left.</span></span> <span data-ttu-id="ecb6c-117">На сайтах групп есть область навигации в левой части страницы, поэтому веб-части на сетке и функции расплавления не занимают пространство, выделенное для области навигации.</span><span class="sxs-lookup"><span data-stu-id="ecb6c-117">Team sites have a left navigation, therefore the space web parts occupy on the gird and the reflow behavior respects the space given to the navigation.</span></span> <span data-ttu-id="ecb6c-118">Максимальная ширина области контента на сайте группы составляет 1204 пикселя, а минимальный размер — 320 пикселей для поддержки мобильных устройств.</span><span class="sxs-lookup"><span data-stu-id="ecb6c-118">The max width of the content area of a Team site is 1204px and the minimum size is 320px for mobile support.</span></span>

![Сайт группы](../images/design-grid-team-site.png)

<span data-ttu-id="ecb6c-120">В приведенных ниже примерах показано, как сетка регулируется с учетом основных пограничных значений на сайте группы.</span><span class="sxs-lookup"><span data-stu-id="ecb6c-120">The following examples show how the grid adjusts between key breakpoints on a team site.</span></span>

#### <a name="small-320-x-568"></a><span data-ttu-id="ecb6c-121">Малый размер (320 x 568)</span><span class="sxs-lookup"><span data-stu-id="ecb6c-121">Small 320 x 568</span></span>
<span data-ttu-id="ecb6c-122">Страница малого размера содержит одну центрированную область столбцов с полями по 20 пикселей слева и справа.</span><span class="sxs-lookup"><span data-stu-id="ecb6c-122">The small size has a single centered column area, with 20px margins left and right.</span></span>

![Малая сетка сайта группы](../images/design-grid-Team-site-S-Canvas-no-column.png)

#### <a name="medium-480-x-854"></a><span data-ttu-id="ecb6c-124">Средний размер (480 x 854)</span><span class="sxs-lookup"><span data-stu-id="ecb6c-124">Medium 480 x 854</span></span>
<span data-ttu-id="ecb6c-125">Страница среднего размера содержит 12 столбцов с интервалами по 16 пикселей.</span><span class="sxs-lookup"><span data-stu-id="ecb6c-125">The medium size has 12 columns, with 16px gutters.</span></span>

![Средняя сетка сайта группы](../images/design-grid-Team-site-M-Canvas-16px-gutters.png)

#### <a name="large-640-x-1024"></a><span data-ttu-id="ecb6c-127">Крупный размер (640 x 1024)</span><span class="sxs-lookup"><span data-stu-id="ecb6c-127">Large 640 x 1024</span></span>
<span data-ttu-id="ecb6c-128">Страница большого размера содержит 12 столбцов с интервалами по 24 пикселя.</span><span class="sxs-lookup"><span data-stu-id="ecb6c-128">The large size has 12 columns, with 24px gutters.</span></span>

![Крупная сетка на сайте группы](../images/design-grid-Team-site-L-Canvas-24px-gutters.png)

#### <a name="xl-1024-x-768"></a><span data-ttu-id="ecb6c-130">XL (1024 x 768)</span><span class="sxs-lookup"><span data-stu-id="ecb6c-130">XL 1024 x 768</span></span>
<span data-ttu-id="ecb6c-131">Страница размера XL содержит двенадцать столбцов с интервалами по 24 пикселя.</span><span class="sxs-lookup"><span data-stu-id="ecb6c-131">The XL size has a twelve columns, with 24px gutters.</span></span>

![Сетка размера XL на сайте группы](../images/design-grid-Team-site-XL-Canvas-24px-gutters.png)

#### <a name="xxl-1366-x-768"></a><span data-ttu-id="ecb6c-133">XXL (1366 x 768)</span><span class="sxs-lookup"><span data-stu-id="ecb6c-133">XXL 1366 x 768</span></span>
<span data-ttu-id="ecb6c-134">Страница размера XXL содержит двенадцать столбцов с интервалами по 32 пикселя.</span><span class="sxs-lookup"><span data-stu-id="ecb6c-134">The XXL size has a twelve columns, with 32px gutters.</span></span>

![Сетка размера XXL на сайте группы](../images/design-grid-Team-site–XXL-Canvas-32px-gutters.png)

#### <a name="xxxl-1920-x-1080"></a><span data-ttu-id="ecb6c-136">XXXL (1920 x 1080)</span><span class="sxs-lookup"><span data-stu-id="ecb6c-136">XXXL 1920 x 1080</span></span>
<span data-ttu-id="ecb6c-137">Страница размера XXXL содержит двенадцать столбцов с интервалами по 32 пикселя.</span><span class="sxs-lookup"><span data-stu-id="ecb6c-137">The XXXL size has a twelve columns, with 32px gutters.</span></span>

![Сетка размера XXXL на сайте группы](../images/design-grid-Team-site-XXXL-Canvas-32px-gutters-maxwidth-1204.png)

#### <a name="team-site-multicolumn-pages-and-web-parts"></a><span data-ttu-id="ecb6c-139">Страницы с несколькими столбцами и веб-части на сайтах групп</span><span class="sxs-lookup"><span data-stu-id="ecb6c-139">Team site multicolumn pages and web parts</span></span>
<span data-ttu-id="ecb6c-140">Веб-части горизонтально масштабируются в соответствии с разметкой страницы.</span><span class="sxs-lookup"><span data-stu-id="ecb6c-140">Web parts will scale horizontally depending on the page layout.</span></span> <span data-ttu-id="ecb6c-141">В приведенном ниже примере показано, как размер веб-части регулируется, чтобы оставить место для области навигации слева.</span><span class="sxs-lookup"><span data-stu-id="ecb6c-141">The following example shows how the size of a web part adjusts to accommodate the left navigation.</span></span>

![Страница с несколькими столбцами и веб-частями на сайте группы](../images/design-grid-Team-site-web-parts.png)


### <a name="communication-sites"></a><span data-ttu-id="ecb6c-143">Сайты для общения</span><span class="sxs-lookup"><span data-stu-id="ecb6c-143">Communication sites</span></span>

<span data-ttu-id="ecb6c-144">Сайты для общения содержат верхнюю область навигации и центрированную область контента.</span><span class="sxs-lookup"><span data-stu-id="ecb6c-144">Communication sites have a top navigation and a centered content area.</span></span> <span data-ttu-id="ecb6c-145">Максимальная ширина области контента на сайте для общения составляет 1204 пикселей, а минимальный размер — 320 пикселей для поддержки мобильных устройств.</span><span class="sxs-lookup"><span data-stu-id="ecb6c-145">The maximum width of the content area of a communication site is 1204px and the minimum size is 320px for mobile support.</span></span>

![Сайт для общения](../images/design-grid-communication_site.png)

<span data-ttu-id="ecb6c-147">В приведенных ниже примерах показано, как сетка регулируется с учетом основных пограничных значений на сайте для общения.</span><span class="sxs-lookup"><span data-stu-id="ecb6c-147">The following examples show how the grid adjusts between key breakpoints on a communication site.</span></span>

#### <a name="small-320-x-568"></a><span data-ttu-id="ecb6c-148">Малый размер (320 x 568)</span><span class="sxs-lookup"><span data-stu-id="ecb6c-148">Small 320 x 568</span></span>
<span data-ttu-id="ecb6c-149">Страница малого размера содержит одну центрированную область столбцов с полями по 20 пикселей слева и справа.</span><span class="sxs-lookup"><span data-stu-id="ecb6c-149">The small size has a single centered column area, with 20px margins left and right.</span></span>

![Сетка малого размера на сайте для общения](../images/design-grid-Communication-site-S-Canvas-no-column.png)

#### <a name="medium-480-x-854"></a><span data-ttu-id="ecb6c-151">Средний размер (480 x 854)</span><span class="sxs-lookup"><span data-stu-id="ecb6c-151">Medium 480 x 854</span></span>
<span data-ttu-id="ecb6c-152">Страница среднего размера содержит 12 столбцов с интервалами по 16 пикселей.</span><span class="sxs-lookup"><span data-stu-id="ecb6c-152">The medium size has 12 columns, with 16px gutters.</span></span>

![Сетка среднего размера на сайте для общения](../images/design-grid-Communication-site-M-Canvas-16px-gutters.png)

#### <a name="large-640-x-1024"></a><span data-ttu-id="ecb6c-154">Крупный размер (640 x 1024)</span><span class="sxs-lookup"><span data-stu-id="ecb6c-154">Large 640 x 1024</span></span>
<span data-ttu-id="ecb6c-155">Страница большого размера содержит 12 столбцов с интервалами по 24 пикселя.</span><span class="sxs-lookup"><span data-stu-id="ecb6c-155">The large size has 12 columns, with 24px gutters.</span></span>

![Крупная сетка на сайте для общения](../images/design-grid-Communication-site-L-Canvas-24px-gutters.png)

#### <a name="xl-1024-x-768"></a><span data-ttu-id="ecb6c-157">XL (1024 x 768)</span><span class="sxs-lookup"><span data-stu-id="ecb6c-157">XL 1024 x 768</span></span>
<span data-ttu-id="ecb6c-158">Страница размера XL содержит двенадцать столбцов с интервалами по 24 пикселя.</span><span class="sxs-lookup"><span data-stu-id="ecb6c-158">The XL size has a twelve columns, with 24px gutters.</span></span>

![Сетка размера XL на сайте для общения](../images/design-grid-Communication-site-XL-Canvas-24px-gutters.png)


#### <a name="xxl-1366-x-768"></a><span data-ttu-id="ecb6c-160">XXL (1366 x 768)</span><span class="sxs-lookup"><span data-stu-id="ecb6c-160">XXL 1366 x 768</span></span>
<span data-ttu-id="ecb6c-161">Страница размера XXL содержит двенадцать столбцов с интервалами по 32 пикселя.</span><span class="sxs-lookup"><span data-stu-id="ecb6c-161">The XXL size has a twelve columns, with 32px gutters.</span></span>

![Сетка размера XXL на сайте для общения](../images/design-grid-Communication-site-XXL-Canvas-32px-gutters-maxwidth-1204.png)


#### <a name="xxxl-1920-x-1080"></a><span data-ttu-id="ecb6c-163">XXXL (1920 x 1080)</span><span class="sxs-lookup"><span data-stu-id="ecb6c-163">XXXL 1920 x 1080</span></span>
<span data-ttu-id="ecb6c-164">Страница размера XXXL содержит двенадцать столбцов с интервалами по 32 пикселя.</span><span class="sxs-lookup"><span data-stu-id="ecb6c-164">The XXXL size has a twelve columns, with 32px gutters.</span></span>

![Сетка размера XXXL на сайте для общения](../images/design-grid-Communication-site-XXXL-Canvas-32px-gutters-maxwidth-1204.png)

#### <a name="communication-site-multicolumn-pages-and-web-parts"></a><span data-ttu-id="ecb6c-166">Страницы с несколькими столбцами и веб-части на сайтах для общения</span><span class="sxs-lookup"><span data-stu-id="ecb6c-166">Communication site multicolumn pages and web parts</span></span>
<span data-ttu-id="ecb6c-167">Веб-части горизонтально масштабируются в соответствии с разметкой страницы.</span><span class="sxs-lookup"><span data-stu-id="ecb6c-167">Web parts will scale horizontally depending on the page layout.</span></span> <span data-ttu-id="ecb6c-168">В этом примере показаны сайт для общения и веб-части для макетов с 1–3 столбцами.</span><span class="sxs-lookup"><span data-stu-id="ecb6c-168">This example shows a communcation site and web parts for single to three column layouts.</span></span>

![Страница с несколькими столбцами и веб-частями на сайте для общения](../images/design-grid-Communciation-site-web-parts.png)



## <a name="breakpoints"></a><span data-ttu-id="ecb6c-170">Пограничные значения</span><span class="sxs-lookup"><span data-stu-id="ecb6c-170">Breakpoints</span></span> 

<span data-ttu-id="ecb6c-171">Для оптимального подстраивания под размеры экранов пользовательский интерфейс SharePoint должен корректировать разметку с учетом следующих пограничных значений ширины:</span><span class="sxs-lookup"><span data-stu-id="ecb6c-171">To create a smooth flowing experience between screen sizes, the SharePoint UI should adapt layouts for the following breakpoint widths:</span></span> 

- <span data-ttu-id="ecb6c-172">320;</span><span class="sxs-lookup"><span data-stu-id="ecb6c-172">320</span></span>
- <span data-ttu-id="ecb6c-173">1024;</span><span class="sxs-lookup"><span data-stu-id="ecb6c-173">Default: 1024</span></span>
- <span data-ttu-id="ecb6c-174">1366;</span><span class="sxs-lookup"><span data-stu-id="ecb6c-174">1366</span></span>
- <span data-ttu-id="ecb6c-175">1920.</span><span class="sxs-lookup"><span data-stu-id="ecb6c-175">1920</span></span>
 
<span data-ttu-id="ecb6c-176">При использовании этих пограничных значений следует учитывать, как сместится контент после корректировки окна просмотра в соответствии с ближайшим пограничным значением.</span><span class="sxs-lookup"><span data-stu-id="ecb6c-176">Within these breakpoints, you should take into consideration how your content will shift when the viewport size becomes optimized for the nearest breakpoint.</span></span> <span data-ttu-id="ecb6c-177">Обратите внимание на то, что эта схема представлена исключительно в качестве иллюстрации и не является точной.</span><span class="sxs-lookup"><span data-stu-id="ecb6c-177">Note that this diagram is for illustration only and is not pixel accurate.</span></span>


![Схема SharePoint с пограничными значениями](../images/design-grid-breakpoints.png)


<span data-ttu-id="ecb6c-179">Адаптивная сетка на сайтах групп и сайтах для общения регулируется при переходе от больших пограничных значений к значениям для мобильных приложений.</span><span class="sxs-lookup"><span data-stu-id="ecb6c-179">The responsive grid for both team sites and communication sites adjusts when going from large breakpoints to mobile breakpoints.</span></span> <span data-ttu-id="ecb6c-180">Так сайт корректируется для устройства и размера его экрана.</span><span class="sxs-lookup"><span data-stu-id="ecb6c-180">This optimizes the site for the device and screen size.</span></span> <span data-ttu-id="ecb6c-181">В приведенной ниже таблице описаны размеры сетки при различных пограничных значениях для размеров экранов популярных устройств.</span><span class="sxs-lookup"><span data-stu-id="ecb6c-181">The following table describes the grid sizes at various breakpoints based on popular device sizes.</span></span>



| <span data-ttu-id="ecb6c-182">Ширина окна</span><span class="sxs-lookup"><span data-stu-id="ecb6c-182">Window width</span></span> | <span data-ttu-id="ecb6c-183">Устройство</span><span class="sxs-lookup"><span data-stu-id="ecb6c-183">Device</span></span>                  | <span data-ttu-id="ecb6c-184">Пограничное значение</span><span class="sxs-lookup"><span data-stu-id="ecb6c-184">Breakpoint</span></span> | <span data-ttu-id="ecb6c-185">Столбцы</span><span class="sxs-lookup"><span data-stu-id="ecb6c-185">Columns</span></span> | <span data-ttu-id="ecb6c-186">Интервал</span><span class="sxs-lookup"><span data-stu-id="ecb6c-186">Gutter Property</span></span> | <span data-ttu-id="ecb6c-187">Максимальное количество столбцов для раздела</span><span class="sxs-lookup"><span data-stu-id="ecb6c-187">Max columns per section</span></span> |
|--------------|-------------------------|------------|---------|--------|-------------------------|
| <span data-ttu-id="ecb6c-188">320</span><span class="sxs-lookup"><span data-stu-id="ecb6c-188">320</span></span>          | <span data-ttu-id="ecb6c-189">iPhone 5/SE, 320 x 568</span><span class="sxs-lookup"><span data-stu-id="ecb6c-189">iPhone 5/SE,320x568</span></span>     | <span data-ttu-id="ecb6c-190">Малый</span><span class="sxs-lookup"><span data-stu-id="ecb6c-190">Small</span></span>      | <span data-ttu-id="ecb6c-191">1</span><span class="sxs-lookup"><span data-stu-id="ecb6c-191">1</span></span>       | <span data-ttu-id="ecb6c-192">Н/д</span><span class="sxs-lookup"><span data-stu-id="ecb6c-192">N/A</span></span>    | <span data-ttu-id="ecb6c-193">1</span><span class="sxs-lookup"><span data-stu-id="ecb6c-193">1</span></span>                       |
| <span data-ttu-id="ecb6c-194">480</span><span class="sxs-lookup"><span data-stu-id="ecb6c-194">480</span></span>          | <span data-ttu-id="ecb6c-195">Устройство с 6-дюймовым экраном</span><span class="sxs-lookup"><span data-stu-id="ecb6c-195">6" device</span></span>               | <span data-ttu-id="ecb6c-196">Средний</span><span class="sxs-lookup"><span data-stu-id="ecb6c-196">Medium</span></span>     | <span data-ttu-id="ecb6c-197">1</span><span class="sxs-lookup"><span data-stu-id="ecb6c-197">1</span></span>       | <span data-ttu-id="ecb6c-198">Н/д</span><span class="sxs-lookup"><span data-stu-id="ecb6c-198">N/A</span></span>    | <span data-ttu-id="ecb6c-199">1</span><span class="sxs-lookup"><span data-stu-id="ecb6c-199">1</span></span>                       |
| <span data-ttu-id="ecb6c-200">640</span><span class="sxs-lookup"><span data-stu-id="ecb6c-200">640</span></span>          | <span data-ttu-id="ecb6c-201">Устройство с 8-дюймовым экраном</span><span class="sxs-lookup"><span data-stu-id="ecb6c-201">8" device</span></span>               | <span data-ttu-id="ecb6c-202">Крупный</span><span class="sxs-lookup"><span data-stu-id="ecb6c-202">Large</span></span>      | <span data-ttu-id="ecb6c-203">12</span><span class="sxs-lookup"><span data-stu-id="ecb6c-203">1.2</span></span>      | <span data-ttu-id="ecb6c-204">16</span><span class="sxs-lookup"><span data-stu-id="ecb6c-204">1.6</span></span>     | <span data-ttu-id="ecb6c-205">2</span><span class="sxs-lookup"><span data-stu-id="ecb6c-205">2</span></span>                       |
| <span data-ttu-id="ecb6c-206">768</span><span class="sxs-lookup"><span data-stu-id="ecb6c-206">768</span></span>          | <span data-ttu-id="ecb6c-207">iPad с книжной ориентацией, 768 x 1024</span><span class="sxs-lookup"><span data-stu-id="ecb6c-207">iPad portrait 768x1024</span></span>  | <span data-ttu-id="ecb6c-208">Крупный</span><span class="sxs-lookup"><span data-stu-id="ecb6c-208">Large</span></span>      | <span data-ttu-id="ecb6c-209">12</span><span class="sxs-lookup"><span data-stu-id="ecb6c-209">1.2</span></span>      | <span data-ttu-id="ecb6c-210">24</span><span class="sxs-lookup"><span data-stu-id="ecb6c-210">2.4</span></span>     | <span data-ttu-id="ecb6c-211">2</span><span class="sxs-lookup"><span data-stu-id="ecb6c-211">2</span></span>                       |
| <span data-ttu-id="ecb6c-212">1024</span><span class="sxs-lookup"><span data-stu-id="ecb6c-212">Default: 1024</span></span>         | <span data-ttu-id="ecb6c-213">iPad с альбомной ориентацией, 1024 x 768</span><span class="sxs-lookup"><span data-stu-id="ecb6c-213">iPad landscape 1024x768</span></span> | <span data-ttu-id="ecb6c-214">Размер XL</span><span class="sxs-lookup"><span data-stu-id="ecb6c-214">X-Large</span></span>    | <span data-ttu-id="ecb6c-215">12</span><span class="sxs-lookup"><span data-stu-id="ecb6c-215">1.2</span></span>      | <span data-ttu-id="ecb6c-216">24</span><span class="sxs-lookup"><span data-stu-id="ecb6c-216">2.4</span></span>     | <span data-ttu-id="ecb6c-217">3</span><span class="sxs-lookup"><span data-stu-id="ecb6c-217">3</span></span>                       |
| <span data-ttu-id="ecb6c-218">1368</span><span class="sxs-lookup"><span data-stu-id="ecb6c-218">1368</span></span>         | <span data-ttu-id="ecb6c-219">Surface Pro 3, 1368 x 912</span><span class="sxs-lookup"><span data-stu-id="ecb6c-219">Surface Pro 3 1368x912</span></span>  | <span data-ttu-id="ecb6c-220">Размер XXL</span><span class="sxs-lookup"><span data-stu-id="ecb6c-220">XX-Large</span></span>   | <span data-ttu-id="ecb6c-221">12</span><span class="sxs-lookup"><span data-stu-id="ecb6c-221">1.2</span></span>      | <span data-ttu-id="ecb6c-222">32</span><span class="sxs-lookup"><span data-stu-id="ecb6c-222">3.2</span></span>     | <span data-ttu-id="ecb6c-223">3</span><span class="sxs-lookup"><span data-stu-id="ecb6c-223">3</span></span>                       |
| <span data-ttu-id="ecb6c-224">1440</span><span class="sxs-lookup"><span data-stu-id="ecb6c-224">1440</span></span>         | <span data-ttu-id="ecb6c-225">Surface Pro 4, 1440 x 960</span><span class="sxs-lookup"><span data-stu-id="ecb6c-225">Surface Pro 4 1440x960</span></span>  | <span data-ttu-id="ecb6c-226">Размер XXL</span><span class="sxs-lookup"><span data-stu-id="ecb6c-226">XX-Large</span></span>   | <span data-ttu-id="ecb6c-227">12</span><span class="sxs-lookup"><span data-stu-id="ecb6c-227">1.2</span></span>      | <span data-ttu-id="ecb6c-228">32</span><span class="sxs-lookup"><span data-stu-id="ecb6c-228">3.2</span></span>     | <span data-ttu-id="ecb6c-229">3</span><span class="sxs-lookup"><span data-stu-id="ecb6c-229">3</span></span>                       |
| <span data-ttu-id="ecb6c-230">1600</span><span class="sxs-lookup"><span data-stu-id="ecb6c-230">1600</span></span>         | <span data-ttu-id="ecb6c-231">Веб-браузер, 1600 x 900</span><span class="sxs-lookup"><span data-stu-id="ecb6c-231">Web 1600x900</span></span>            | <span data-ttu-id="ecb6c-232">Размер XXL</span><span class="sxs-lookup"><span data-stu-id="ecb6c-232">XX-Large</span></span>   | <span data-ttu-id="ecb6c-233">12</span><span class="sxs-lookup"><span data-stu-id="ecb6c-233">1.2</span></span>      | <span data-ttu-id="ecb6c-234">32</span><span class="sxs-lookup"><span data-stu-id="ecb6c-234">3.2</span></span>     | <span data-ttu-id="ecb6c-235">3</span><span class="sxs-lookup"><span data-stu-id="ecb6c-235">3</span></span>                       |
| <span data-ttu-id="ecb6c-236">1920</span><span class="sxs-lookup"><span data-stu-id="ecb6c-236">1920</span></span>         | <span data-ttu-id="ecb6c-237">Веб-браузер, 1920 x 1080</span><span class="sxs-lookup"><span data-stu-id="ecb6c-237">Web 1920x1080</span></span>           | <span data-ttu-id="ecb6c-238">Размер XXXL</span><span class="sxs-lookup"><span data-stu-id="ecb6c-238">XXX-Large</span></span>  | <span data-ttu-id="ecb6c-239">12</span><span class="sxs-lookup"><span data-stu-id="ecb6c-239">1.2</span></span>      | <span data-ttu-id="ecb6c-240">32</span><span class="sxs-lookup"><span data-stu-id="ecb6c-240">3.2</span></span>     | <span data-ttu-id="ecb6c-241">3</span><span class="sxs-lookup"><span data-stu-id="ecb6c-241">3</span></span>                       |

## <a name="see-also"></a><span data-ttu-id="ecb6c-242">См. также</span><span class="sxs-lookup"><span data-stu-id="ecb6c-242">See also</span></span>

- [<span data-ttu-id="ecb6c-243">Набор инструментов и ресурсы для дизайна</span><span class="sxs-lookup"><span data-stu-id="ecb6c-243">Design toolkit and assets</span></span>](https://developer.microsoft.com/ru-RU/fabric#/resources)


