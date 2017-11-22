---
title: "Разработка веб-части SharePoint"
ms.date: 9/25/2017
ms.openlocfilehash: fdee0792f486ebb792d5aaf8d8c7993cdd273324
ms.sourcegitcommit: 1b295a186814ca6ab13dda1a17e34dc69a61d81e
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="designing-a-sharepoint-web-part"></a><span data-ttu-id="6599a-102">Разработка веб-части SharePoint</span><span class="sxs-lookup"><span data-stu-id="6599a-102">Designing a SharePoint web part</span></span>

<span data-ttu-id="6599a-103">Перед разработкой веб-части SharePoint следует знать, как [создавать страницы на сайте SharePoint](authoring-pages.md).</span><span class="sxs-lookup"><span data-stu-id="6599a-103">Before you design a SharePoint web part, you should understand how to [author pages in a SharePoint site](authoring-pages.md).</span></span> <span data-ttu-id="6599a-104">Если вы еще не сделали этого, создайте страницу и добавьте на нее веб-части нескольких типов.</span><span class="sxs-lookup"><span data-stu-id="6599a-104">If you haven't already, take some time to create a page and add multiple types of web parts.</span></span> <span data-ttu-id="6599a-105">Важно понимать, как упростить и ускорить подготовку новой веб-части к работе с помощью компонентов и стилей Office Fabric.</span><span class="sxs-lookup"><span data-stu-id="6599a-105">It is important know how to leverage Office Fabric components and styles to make it easier and quicker to get your new web part up and running.</span></span>

<span data-ttu-id="6599a-106">При разработке веб-частей важно владеть понятиями, описанными в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="6599a-106">When you design web parts, it's important to be familiar with the following concepts:</span></span>

- <span data-ttu-id="6599a-107">[Типы областей свойств и их применение](#property-pane-types);</span><span class="sxs-lookup"><span data-stu-id="6599a-107">[Property pane types and when to use each type](#property-pane-types)</span></span>
- <span data-ttu-id="6599a-108">[Реактивные и нереактивные веб-части](reactive-and-nonreactive-web-parts.md);</span><span class="sxs-lookup"><span data-stu-id="6599a-108">[Reactive and nonreactive web parts](reactive-and-nonreactive-web-parts.md)</span></span>
- <span data-ttu-id="6599a-109">[Названия и описания](web-part-titles-and-descriptions.md);</span><span class="sxs-lookup"><span data-stu-id="6599a-109">[Titles and descriptions](web-part-titles-and-descriptions.md)</span></span>
- <span data-ttu-id="6599a-110">[Резервные варианты и заполнители](placeholders-and-fallbacks.md).</span><span class="sxs-lookup"><span data-stu-id="6599a-110">[Fallbacks and placeholders](placeholders-and-fallbacks.md)</span></span>


## <a name="property-pane-types"></a><span data-ttu-id="6599a-111">Типы областей свойств</span><span class="sxs-lookup"><span data-stu-id="6599a-111">Property pane types</span></span>

<span data-ttu-id="6599a-112">Вы можете использовать области свойств трех типов для оформления и разработки веб-частей, соответствующих потребностям вашего бизнеса и клиентов.</span><span class="sxs-lookup"><span data-stu-id="6599a-112">There are three types of property panes to enable you to design and develop web parts that fit your business or customer needs.</span></span>

<span data-ttu-id="6599a-113">Чтобы открыть область для настройки параметров веб-части, нажмите **Изменить**.</span><span class="sxs-lookup"><span data-stu-id="6599a-113">To open a pane to configure settings for a web part, choose **Edit**.</span></span> <span data-ttu-id="6599a-114">С помощью этой области можно включать и отключать функции, выбирать источник и макет, а также задавать параметры.</span><span class="sxs-lookup"><span data-stu-id="6599a-114">Use the pane to enable and disable features, select a source, choose a layout, and set options.</span></span> <span data-ttu-id="6599a-115">Редактируйте содержимое веб-части в самой веб-части, а не в области свойств.</span><span class="sxs-lookup"><span data-stu-id="6599a-115">Edit web part content within the web part rather than in the property pane.</span></span>

<span data-ttu-id="6599a-116">Ширина области свойств составляет 320 пикселей. При ее открытии выполняется автоматическое расплавление страницы.</span><span class="sxs-lookup"><span data-stu-id="6599a-116">The property pane is 320px and when opened, the page will responsively reflow.</span></span>

### <a name="single-pane"></a><span data-ttu-id="6599a-117">Одиночная область</span><span class="sxs-lookup"><span data-stu-id="6599a-117">Single pane</span></span>
<span data-ttu-id="6599a-118">Одиночная область используется для простых веб-частей с небольшим количеством настраиваемых свойств.</span><span class="sxs-lookup"><span data-stu-id="6599a-118">A single pane is used for simple web parts that only have a small number of properties to configure.</span></span>


![Одиночная область](../images/design-web-part-single.png)


### <a name="accordion-pane"></a><span data-ttu-id="6599a-120">Область с элементом "аккордеон"</span><span class="sxs-lookup"><span data-stu-id="6599a-120">Accordion pane</span></span>
<span data-ttu-id="6599a-121">Область-гармошка используется для размещения групп свойств с большим количеством вариантов, образующих длинный прокручивающийся список.</span><span class="sxs-lookup"><span data-stu-id="6599a-121">Use an accordion pane to contain a group or groups of properties with many options, and where the groups result in a long scrolling list of options.</span></span> <span data-ttu-id="6599a-122">Например, у вас может быть три группы с названиями "Свойства", "Внешний вид" и "Макет", по десять компонентов в каждой.</span><span class="sxs-lookup"><span data-stu-id="6599a-122">For example, you might have three groups named Properties, Appearance, and Layout, each with ten components.</span></span>

<span data-ttu-id="6599a-123">Используйте области с элементами "аккордеон", если требуется добавить классификацию в сложную веб-часть.</span><span class="sxs-lookup"><span data-stu-id="6599a-123">Use accordion panes when you need to apply categorization for a complex web part.</span></span>

![Область с элементом "аккордеон"](../images/design-web-part-accordion-group.png)


<span data-ttu-id="6599a-125">**Пример групп элементов "аккордеон", где открыта последняя область**</span><span class="sxs-lookup"><span data-stu-id="6599a-125">**Accordian groups example with last pane open**</span></span>


![Область с элементом "аккордеон", открыта последняя область](../images/design-web-part-accordion-last-open.png)


<span data-ttu-id="6599a-127">**Пример групп элементов "аккордеон", где открыты две группы**</span><span class="sxs-lookup"><span data-stu-id="6599a-127">**Accordion groups example with two groups open**</span></span>

![Область с элементом "аккордеон", где открыты две группы](../images/design-web-part-accordion-two-open.png)



### <a name="steps-pane"></a><span data-ttu-id="6599a-129">Область с пошаговым представлением</span><span class="sxs-lookup"><span data-stu-id="6599a-129">Steps pane</span></span>

<span data-ttu-id="6599a-130">Область с пошаговым представлением используется для группирования свойств на нескольких этапах или страницах, если веб-часть требуется настраивать в линейном порядке, а также если параметры, выбранные на первом этапе, влияют на то, какие параметры отображаются на втором или третьем.</span><span class="sxs-lookup"><span data-stu-id="6599a-130">A steps pane is used for grouping properties in multiple steps or pages when you need the web part to be configured in a linear order or when choices made on the first step affect options that display on the second step.</span></span> 

<span data-ttu-id="6599a-131">**Этап 1 в области с пошаговым представлением**</span><span class="sxs-lookup"><span data-stu-id="6599a-131">**Step 1 of the steps pane**</span></span>

<span data-ttu-id="6599a-132">На этапе 1 кнопка "Назад" отключена, а кнопка "Далее" включена.</span><span class="sxs-lookup"><span data-stu-id="6599a-132">In step 1, the back button is disabled and the next button is enabled.</span></span>

![Область с пошаговым представлением, где включена кнопка "Далее"](../images/design-web-part-step-pane-01.png)


<span data-ttu-id="6599a-134">**Этап 2 в области с пошаговым представлением**</span><span class="sxs-lookup"><span data-stu-id="6599a-134">**Step 2 of the steps pane**</span></span> 

<span data-ttu-id="6599a-135">На этапе 2 кнопки "Назад" и "Далее" включены.</span><span class="sxs-lookup"><span data-stu-id="6599a-135">In step 2, the back and next buttons are enabled.</span></span>

![Область с пошаговым представлением, где включены кнопки "Назад" и "Далее"](../images/design-web-part-step-pane-02.png)


<span data-ttu-id="6599a-137">**Этап 3 в области с пошаговым представлением**</span><span class="sxs-lookup"><span data-stu-id="6599a-137">**Step 3 of the steps pane**</span></span> 

<span data-ttu-id="6599a-138">На этапе 3 кнопка "Далее" отключена, а кнопка "Назад" включена.</span><span class="sxs-lookup"><span data-stu-id="6599a-138">In step 3, the next button is disabled and the back button is enabled.</span></span>

![Область с пошаговым представлением, где включена кнопка "Назад"](../images/design-web-part-step-pane-03.png)
