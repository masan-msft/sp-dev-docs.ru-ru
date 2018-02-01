---
title: "Разработка веб-части SharePoint"
description: "Проектируйте и разрабатывайте веб-части, соответствующие потребностям компании или клиентов, используя области свойств трех типов."
ms.date: 01/23/2018
ms.openlocfilehash: 0e6afe3323407fda99d76bd72c7006527c30c5f5
ms.sourcegitcommit: 0ad5aeee2c5efc47eb57e050581e4f411c4be643
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/29/2018
---
# <a name="designing-a-sharepoint-web-part"></a><span data-ttu-id="272af-103">Разработка веб-части SharePoint</span><span class="sxs-lookup"><span data-stu-id="272af-103">Designing a SharePoint web part</span></span>

<span data-ttu-id="272af-104">Перед разработкой веб-части SharePoint следует знать, как [создавать страницы на сайте SharePoint](authoring-pages.md).</span><span class="sxs-lookup"><span data-stu-id="272af-104">Before you design a SharePoint web part, you should understand how to [author pages in a SharePoint site](authoring-pages.md).</span></span> <span data-ttu-id="272af-105">Если вы еще не сделали этого, создайте страницу и добавьте на нее веб-части нескольких типов.</span><span class="sxs-lookup"><span data-stu-id="272af-105">If you haven't already, take some time to create a page and add multiple types of web parts.</span></span> <span data-ttu-id="272af-106">Важно понимать, как упростить и ускорить настройку новой веб-части с помощью компонентов и стилей Office Fabric.</span><span class="sxs-lookup"><span data-stu-id="272af-106">It is important know how to leverage Office Fabric components and styles to make it easier and quicker to get your new web part up and running.</span></span>

<span data-ttu-id="272af-107">При разработке веб-частей важно владеть понятиями, описанными в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="272af-107">When you design web parts, it's important to be familiar with the following concepts:</span></span>

- <span data-ttu-id="272af-108">[Типы областей свойств и их применение](#property-pane-types);</span><span class="sxs-lookup"><span data-stu-id="272af-108">[Property pane types and when to use each type](#property-pane-types)</span></span>
- <span data-ttu-id="272af-109">[Реактивные и нереактивные веб-части](reactive-and-nonreactive-web-parts.md);</span><span class="sxs-lookup"><span data-stu-id="272af-109">[Reactive and nonreactive web parts](reactive-and-nonreactive-web-parts.md)</span></span>
- [<span data-ttu-id="272af-110">Названия и описания</span><span class="sxs-lookup"><span data-stu-id="272af-110">Titles and descriptions</span></span>](web-part-titles-and-descriptions.md)
- [<span data-ttu-id="272af-111">Заполнители и резервные элементы</span><span class="sxs-lookup"><span data-stu-id="272af-111">Placeholders and fallbacks</span></span>](placeholders-and-fallbacks.md)


## <a name="property-pane-types"></a><span data-ttu-id="272af-112">Типы областей свойств</span><span class="sxs-lookup"><span data-stu-id="272af-112">Property pane types</span></span>

<span data-ttu-id="272af-113">Вы можете использовать области свойств трех типов для оформления и разработки веб-частей, соответствующих потребностям вашего бизнеса и клиентов.</span><span class="sxs-lookup"><span data-stu-id="272af-113">You can use three types of property panes to design and develop web parts that fit your business or customer needs.</span></span>

<span data-ttu-id="272af-114">Чтобы открыть область для настройки параметров веб-части, нажмите **Изменить**.</span><span class="sxs-lookup"><span data-stu-id="272af-114">To open a pane to configure settings for a web part, select **Edit**.</span></span> <span data-ttu-id="272af-115">С помощью этой области можно включать и отключать функции, выбирать источник и макет, а также задавать параметры.</span><span class="sxs-lookup"><span data-stu-id="272af-115">Use the pane to enable and disable features, select a source, choose a layout, and set options.</span></span> <span data-ttu-id="272af-116">Редактируйте содержимое веб-части в самой веб-части, а не в области свойств.</span><span class="sxs-lookup"><span data-stu-id="272af-116">Edit web part content within the web part rather than in the property pane.</span></span>

<span data-ttu-id="272af-117">Ширина области свойств — 320 пикселей. При открытии страница оперативно перестраивается.</span><span class="sxs-lookup"><span data-stu-id="272af-117">The property pane is 320px and when opened, the page will responsively reflow.</span></span>

### <a name="single-pane"></a><span data-ttu-id="272af-118">Одиночная область</span><span class="sxs-lookup"><span data-stu-id="272af-118">Single pane</span></span>

<span data-ttu-id="272af-119">Одиночная область используется для простых веб-частей с небольшим количеством настраиваемых свойств.</span><span class="sxs-lookup"><span data-stu-id="272af-119">Use a single pane for simple web parts that have only a small number of properties to configure.</span></span>

![Одиночная область](../images/design-web-part-single.png)

<br/>

### <a name="accordion-pane"></a><span data-ttu-id="272af-121">Область с элементом "аккордеон"</span><span class="sxs-lookup"><span data-stu-id="272af-121">Accordion pane</span></span>

<span data-ttu-id="272af-122">Область-гармошка используется для размещения групп свойств с большим количеством вариантов, образующих длинный прокручивающийся список.</span><span class="sxs-lookup"><span data-stu-id="272af-122">Use an accordion pane to contain a group or groups of properties with many options, and where the groups result in a long scrolling list of options.</span></span> <span data-ttu-id="272af-123">Например, у вас может быть три группы с названиями "Свойства", "Внешний вид" и "Макет", по десять компонентов в каждой.</span><span class="sxs-lookup"><span data-stu-id="272af-123">For example, you might have three groups named Properties, Appearance, and Layout, each with ten components.</span></span>

<span data-ttu-id="272af-124">Используйте области с элементами "аккордеон", если требуется добавить классификацию в сложную веб-часть.</span><span class="sxs-lookup"><span data-stu-id="272af-124">Use accordion panes when you need to apply categorization for a complex web part.</span></span>

![Область с элементом "аккордеон"](../images/design-web-part-accordion-group.png)

<br/>

<span data-ttu-id="272af-126">**Пример групп элементов "аккордеон", где открыта последняя область**</span><span class="sxs-lookup"><span data-stu-id="272af-126">**Accordian groups example with last pane open**</span></span>

![Область с элементом "аккордеон", открыта последняя область](../images/design-web-part-accordion-last-open.png)

<br/>

<span data-ttu-id="272af-128">**Пример групп элементов "аккордеон", где открыты две группы**</span><span class="sxs-lookup"><span data-stu-id="272af-128">**Accordion groups example with two groups open**</span></span>

![Область с элементом "аккордеон", где открыты две группы](../images/design-web-part-accordion-two-open.png)

<br/>

### <a name="steps-pane"></a><span data-ttu-id="272af-130">Область с пошаговым представлением</span><span class="sxs-lookup"><span data-stu-id="272af-130">Steps pane</span></span>

<span data-ttu-id="272af-131">Область с пошаговым представлением используется для группирования свойств на нескольких этапах или страницах, если веб-часть требуется настраивать в линейном порядке, а также если параметры, выбранные на первом этапе, влияют на то, какие параметры отображаются на втором или третьем.</span><span class="sxs-lookup"><span data-stu-id="272af-131">Use a steps pane to group properties in multiple steps or pages when you need the web part to be configured in a linear order, or when choices in the first step affect the options that display in the second or third step.</span></span> 

<span data-ttu-id="272af-132">**Этап 1 в области с пошаговым представлением**</span><span class="sxs-lookup"><span data-stu-id="272af-132">**Step 1 of the steps pane**</span></span>

<span data-ttu-id="272af-133">На этапе 1 кнопка "Назад" отключена, а кнопка "Далее" включена.</span><span class="sxs-lookup"><span data-stu-id="272af-133">In step 1, the back button is disabled and the next button is enabled.</span></span>

![Область с пошаговым представлением, где включена кнопка "Далее"](../images/design-web-part-steps-pane-01.png)

<br/>

<span data-ttu-id="272af-135">**Этап 2 в области с пошаговым представлением**</span><span class="sxs-lookup"><span data-stu-id="272af-135">**Step 2 of the steps pane**</span></span> 

<span data-ttu-id="272af-136">На этапе 2 кнопки "Назад" и "Далее" включены.</span><span class="sxs-lookup"><span data-stu-id="272af-136">In step 2, the back and next buttons are enabled.</span></span>

![Область с пошаговым представлением, где включены кнопки "Назад" и "Далее"](../images/design-web-part-steps-pane-02.png)

<br/>

<span data-ttu-id="272af-138">**Этап 3 в области с пошаговым представлением**</span><span class="sxs-lookup"><span data-stu-id="272af-138">**Step 3 of the steps pane**</span></span> 

<span data-ttu-id="272af-139">На этапе 3 кнопка "Далее" отключена, а кнопка "Назад" включена.</span><span class="sxs-lookup"><span data-stu-id="272af-139">In step 3, the next button is disabled and the back button is enabled.</span></span>

![Область с пошаговым представлением, где включена кнопка "Назад"](../images/design-web-part-steps-pane-03.png)


## <a name="see-also"></a><span data-ttu-id="272af-141">См. также</span><span class="sxs-lookup"><span data-stu-id="272af-141">See also</span></span>

- [<span data-ttu-id="272af-142">Разработка прекрасных решений для SharePoint</span><span class="sxs-lookup"><span data-stu-id="272af-142">Designing great SharePoint experiences</span></span>](design-guidance-overview.md)


