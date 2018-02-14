---
title: "Особенности разработки клиентских веб-частей SharePoint"
description: "Используйте компоненты Office UI Fabric React для сборки и оформления веб-частей."
ms.date: 01/24/2018
ms.prod: sharepoint
ms.openlocfilehash: d19d5593f6093ed44d993f9f61a37f56dcaa3883
ms.sourcegitcommit: 0ad5aeee2c5efc47eb57e050581e4f411c4be643
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/29/2018
---
# <a name="design-considerations-for-sharepoint-client-side-web-parts"></a><span data-ttu-id="92bb1-103">Особенности разработки клиентских веб-частей SharePoint</span><span class="sxs-lookup"><span data-stu-id="92bb1-103">Design considerations for SharePoint client-side web parts</span></span>

<span data-ttu-id="92bb1-104">Для разработки веб-частей необходимо понимание работы с [Office UI Fabric](https://developer.microsoft.com/ru-RU/fabric).</span><span class="sxs-lookup"><span data-stu-id="92bb1-104">To get started designing web parts, you need to be familiar with [Office UI Fabric](https://developer.microsoft.com/ru-RU/fabric).</span></span> <span data-ttu-id="92bb1-105">Все стили из [Fabric Core](https://github.com/OfficeDev/office-ui-fabric-core) (включая значки, оформление, использование цветов, анимацию и адаптируемую сетку) загружаются по умолчанию и доступны веб-части.</span><span class="sxs-lookup"><span data-stu-id="92bb1-105">All of the styles from [Fabric Core](https://github.com/OfficeDev/office-ui-fabric-core), including icons, typography, color usage, animation, and the responsive grid, are loaded by default and available to your web part.</span></span> 

<span data-ttu-id="92bb1-106">Не импортируйте копию Fabric для веб-части, так как может возникнуть конфликт с глобальной копией.</span><span class="sxs-lookup"><span data-stu-id="92bb1-106">Do not import a copy of Fabric for your web part because this may conflict with the global copy.</span></span> <span data-ttu-id="92bb1-107">Эти классы формируют основу стиля веб-части, от которой можно отклоняться, если требуется другое оформление, соответствующее фирменной символике компании.</span><span class="sxs-lookup"><span data-stu-id="92bb1-107">These classes provide a foundation to your web part's styling, which you can always depart from if you require different visuals to match your company's brand.</span></span>

## <a name="office-ui-fabric-react-components"></a><span data-ttu-id="92bb1-108">Компоненты Office UI Fabric React</span><span class="sxs-lookup"><span data-stu-id="92bb1-108">Office UI Fabric React Components</span></span>

<span data-ttu-id="92bb1-109">Наряду с Office UI Fabric для создания веб-частей можно использовать компоненты Office UI Fabric React.</span><span class="sxs-lookup"><span data-stu-id="92bb1-109">Along with Office UI Fabric, you can use Office UI Fabric React components to build your web parts.</span></span> <span data-ttu-id="92bb1-110">Fabric React — это адаптируемая, рассчитанная на мобильные устройства коллекция компонентов, призванных ускорить и упростить создание веб-интерфейсов с помощью языка дизайна Office.</span><span class="sxs-lookup"><span data-stu-id="92bb1-110">Along with Office UI Fabric, you can use Office UI Fabric React components to build your web parts. Fabric React is a responsive, mobile-first collection of  components designed to make it quick and simple for you to create web experiences using the Office Design Language.</span></span>

<span data-ttu-id="92bb1-111">В приведенном ниже примере со списком дел компоненты Fabric используются в области свойств, с помощью которой автор страницы может настраивать веб-часть.</span><span class="sxs-lookup"><span data-stu-id="92bb1-111">The following To Do list example uses Fabric components in the property pane that lets the page author configure a web part.</span></span>

![Пример веб-части списка дел, использующей Fabric](../../../images/design-wp-todo-example.png)

<span data-ttu-id="92bb1-113">Полный список стилей, вариантов оформления, цветов, значков и анимаций Office UI Fabric представлен на странице [Стили Office UI Fabric](https://developer.microsoft.com/ru-RU/fabric#/styles).</span><span class="sxs-lookup"><span data-stu-id="92bb1-113">You can find a complete list of the Office UI Fabric styles, typography, color, icons, and animations at [Office UI Fabric styles](https://developer.microsoft.com/ru-RU/fabric#/styles).</span></span>


## <a name="responsive-behavior"></a><span data-ttu-id="92bb1-114">Адаптируемое поведение</span><span class="sxs-lookup"><span data-stu-id="92bb1-114">Responsive behavior</span></span>

<span data-ttu-id="92bb1-115">На страницах нового интерфейса разработки SharePoint используется адаптируемая сетка Office UI Fabric, обеспечивающая приятный внешний вид каждой страницы.</span><span class="sxs-lookup"><span data-stu-id="92bb1-115">Pages in the new SharePoint authoring experience use the Office UI Fabric responsive grid to help ensure that each page will look great.</span></span> 

### <a name="maximum-width"></a><span data-ttu-id="92bb1-116">Максимальная ширина</span><span class="sxs-lookup"><span data-stu-id="92bb1-116">Maximum width</span></span>

<span data-ttu-id="92bb1-117">Рекомендуем использовать во всех веб-частях максимальную ширину 100 %, чтобы обеспечить их правильное расплавление и корректную работу на любой странице.</span><span class="sxs-lookup"><span data-stu-id="92bb1-117">We recommend that all web parts use a 100% maximum width to ensure that they re-flow and function properly on any page.</span></span> <span data-ttu-id="92bb1-118">Ширина страниц и столбцов определяется шаблоном страницы, но разработчик может менять ее.</span><span class="sxs-lookup"><span data-stu-id="92bb1-118">The page and column widths are defined by the page template but can be modified by the author.</span></span> <span data-ttu-id="92bb1-119">Если для веб-части задано максимальное количество пикселей, это может непредсказуемым образом повлиять на функции и макет страницы при ее просмотре на экранах разной ширины.</span><span class="sxs-lookup"><span data-stu-id="92bb1-119">If a maximum pixel value is set in the web part, there could be unexpected results in both functionality and layout when the page is seen at different widths.</span></span>

![Адаптируемая максимальная ширина веб-части](../../../images/design-wp-responsive-max-width.png)

### <a name="minimum-width"></a><span data-ttu-id="92bb1-121">Минимальная ширина</span><span class="sxs-lookup"><span data-stu-id="92bb1-121">Minimum width</span></span>

<span data-ttu-id="92bb1-122">Все веб-части должны поддерживать расплавление, так как ширина страниц и столбцов может уменьшаться до минимального значения в 320 пикселей.</span><span class="sxs-lookup"><span data-stu-id="92bb1-122">All web parts should be designed to reflow as the page/column width gets smaller down to a min width of 320 px.</span></span>

![Адаптируемая минимальная ширина веб-части](../../../images/design-wp-responsive-min-width.png)

<br/>

## <a name="web-part-edit-mode"></a><span data-ttu-id="92bb1-124">Режим правки веб-части</span><span class="sxs-lookup"><span data-stu-id="92bb1-124">Web part Edit mode</span></span>

<span data-ttu-id="92bb1-125">У нового интерфейса создания страниц SharePoint есть два режима:</span><span class="sxs-lookup"><span data-stu-id="92bb1-125">The new SharePoint page authoring experience has two modes:</span></span>

* <span data-ttu-id="92bb1-126">**режим публикации**, в котором группа или аудитория может просматривать содержимое и работать с веб-частями;</span><span class="sxs-lookup"><span data-stu-id="92bb1-126">**Published mode** which allows your team or audience to view content and interact with web parts.</span></span>
* <span data-ttu-id="92bb1-127">**режим правки**, в котором авторы страницы могут добавлять и настраивать веб-части, чтобы добавлять содержимое на страницу.</span><span class="sxs-lookup"><span data-stu-id="92bb1-127">**Edit mode** which allows page author(s) to add and configure web parts to add content to a page.</span></span>

<span data-ttu-id="92bb1-128">В разделах ниже описывается режим правки.</span><span class="sxs-lookup"><span data-stu-id="92bb1-128">The following sections describe Edit mode.</span></span>

### <a name="add-hint-and-toolbox"></a><span data-ttu-id="92bb1-129">Подсказка о добавлении и панель элементов</span><span class="sxs-lookup"><span data-stu-id="92bb1-129">Add hint and Toolbox</span></span>

<span data-ttu-id="92bb1-130">Подсказка о добавлении — это горизонтальная линия со значком "плюс", которая отображается при выделении веб-части или наведении указателя мыши на нее и указывает, что авторы могут добавлять веб-части на свою страницу.</span><span class="sxs-lookup"><span data-stu-id="92bb1-130">The add hint is a horizontal line with a plus icon that is visible when a web part is selected and on hover to indicate where page authors can add new web parts to their page.</span></span> <span data-ttu-id="92bb1-131">Когда пользователь нажимает значок "плюс", открывается панель элементов.</span><span class="sxs-lookup"><span data-stu-id="92bb1-131">The Toolbox opens when a user selects the plus icon.</span></span> <span data-ttu-id="92bb1-132">Панель элементов содержит все веб-части, которые можно добавить на страницу.</span><span class="sxs-lookup"><span data-stu-id="92bb1-132">The Toolbox contains all the web parts that can be added to a page.</span></span>

![Подсказка о добавлении и панель элементов веб-части](../../../images/design-wp-toolbox.png)

### <a name="toolbar"></a><span data-ttu-id="92bb1-134">Панель инструментов</span><span class="sxs-lookup"><span data-stu-id="92bb1-134">Toolbar</span></span>

<span data-ttu-id="92bb1-p106">Вертикальная панель инструментов и ограничивающий прямоугольник входят в состав платформы для каждой веб-части и предоставляются страницей. Для каждой веб-части на панели инструментов есть действия редактирования и удаления.</span><span class="sxs-lookup"><span data-stu-id="92bb1-p106">A vertical toolbar and bounding box is part of the framework for every web part and provided by the page. Each web part has an edit and delete action in the toolbar.</span></span>

![Вертикальная панель инструментов для веб-части](../../../images/design-wp-toolbar.png)

### <a name="contextual-edits"></a><span data-ttu-id="92bb1-138">Контекстная правка</span><span class="sxs-lookup"><span data-stu-id="92bb1-138">Contextual edits</span></span>

<span data-ttu-id="92bb1-139">Для веб-частей следует разработать интерфейс в режиме WYSIWYG, где можно вводить данные и добавлять содержимое, которое отображается для пользователя после публикации.</span><span class="sxs-lookup"><span data-stu-id="92bb1-139">A WYSIWYG experience should be designed for web parts to fill in information or add content that is displayed to the user when published.</span></span> <span data-ttu-id="92bb1-140">Вводить это содержимое следует на странице, чтобы пользователь понимал, как оно будет выглядеть.</span><span class="sxs-lookup"><span data-stu-id="92bb1-140">Entering this content should be done on the page so that the user understands how the viewer sees the content.</span></span> <span data-ttu-id="92bb1-141">Например, заголовки и описания следует вводить там, где будет отображаться текст, а новые задачи следует добавлять и редактировать в контексте страницы.</span><span class="sxs-lookup"><span data-stu-id="92bb1-141">For example, titles and descriptions should be filled out where the text displays; new tasks should be added and modified in the context of the page.</span></span>

![Контекстная правка веб-частей](../../../images/design-wp-contexual-edits.png)

### <a name="item-level-edits"></a><span data-ttu-id="92bb1-143">Правка на уровне элементов</span><span class="sxs-lookup"><span data-stu-id="92bb1-143">Item-level edits</span></span>

<span data-ttu-id="92bb1-144">Пользовательский интерфейс веб-части может меняться. Например, текст может превращаться в текстовое поле для ввода ссылок, а при отображении интерфейса можно менять порядок элементов и отмечать задачи в веб-части.</span><span class="sxs-lookup"><span data-stu-id="92bb1-144">UI can change within the web part; for example, turning text into a text field to fill out links or when displaying UI to reorder items or to check of tasks in a web part</span></span>

![Правка веб-части на уровне элементов](../../../images/design-wp-item-level-edits.png)

## <a name="property-panes"></a><span data-ttu-id="92bb1-146">Области свойств</span><span class="sxs-lookup"><span data-stu-id="92bb1-146">Property panes</span></span>

<span data-ttu-id="92bb1-147">Области свойств вызываются с помощью значка редактирования на панели инструментов.</span><span class="sxs-lookup"><span data-stu-id="92bb1-147">Property panes are invoked via the Edit icon on the toolbar.</span></span> <span data-ttu-id="92bb1-148">Области в первую очередь должны содержать параметры конфигурации для включения и отключения компонентов, которые либо отображаются на странице, либо вызывают службу для отображения содержимого.</span><span class="sxs-lookup"><span data-stu-id="92bb1-148">Property panes are invoked via the edit action icon on the toolbar. Panes should primarily contain configuration settings that enable/disable features that either show on page or that make a call to a service to display content.</span></span>

![Оформление области свойств веб-части](../../../images/design-wp-pp.png)

<span data-ttu-id="92bb1-150">Существует три типа областей свойств, позволяющих создавать и оформлять веб-части в соответствии с потребностями бизнеса или клиентов.</span><span class="sxs-lookup"><span data-stu-id="92bb1-150">There are three types of property panes to enable you to design and develop web parts that fit your business or customer needs.</span></span>

### <a name="single-pane"></a><span data-ttu-id="92bb1-151">Одиночная область</span><span class="sxs-lookup"><span data-stu-id="92bb1-151">Single pane</span></span>

<span data-ttu-id="92bb1-152">Одиночная область используется для простых веб-частей с небольшим количеством настраиваемых свойств.</span><span class="sxs-lookup"><span data-stu-id="92bb1-152">A single pane is used for simple web parts that only have a small number of properties to configure.</span></span>

![Оформление одиночной области свойств веб-части](../../../images/design-wp-pp-single.png)

### <a name="accordion-pane"></a><span data-ttu-id="92bb1-154">Область-гармошка</span><span class="sxs-lookup"><span data-stu-id="92bb1-154">Accordion pane</span></span>

<span data-ttu-id="92bb1-155">Область-гармошка используется для размещения групп свойств с большим количеством вариантов, образующих длинный прокручивающийся список.</span><span class="sxs-lookup"><span data-stu-id="92bb1-155">A accordion pane is used for containing a group or groups of properties with many options and where the groups would result in a long scrolling list of options. For example, you might have three groups named Properties, Appearance, and Layout, each with ten components.</span></span> <span data-ttu-id="92bb1-156">Например, у вас может быть три группы с названиями "Свойства", "Внешний вид" и "Макет", по десять компонентов в каждой.</span><span class="sxs-lookup"><span data-stu-id="92bb1-156">For example, you might have three groups named Properties, Appearance, and Layout, each with ten components.</span></span>

#### <a name="accordion---one-group-open"></a><span data-ttu-id="92bb1-157">Гармошка с одной открытой группой</span><span class="sxs-lookup"><span data-stu-id="92bb1-157">Accordion - One group open</span></span>

![Область-гармошка свойств веб-части с одной открытой группой](../../../images/design-wp-pp-accordion.png)

#### <a name="accordion---two-groups-open-and-scrolled"></a><span data-ttu-id="92bb1-159">Гармошка с двумя открытыми прокручивающимися группами</span><span class="sxs-lookup"><span data-stu-id="92bb1-159">Accordion- Two groups open and scrolled</span></span>

![Область-гармошка свойств веб-части с двумя открытыми прокручивающимися группами](../../../images/design-wp-pp-accordion-groups.png)


### <a name="property-pane-stepspages"></a><span data-ttu-id="92bb1-161">Ступенчатые и страничные области свойств</span><span class="sxs-lookup"><span data-stu-id="92bb1-161">Property pane steps/pages</span></span>

<span data-ttu-id="92bb1-162">Ступенчатая область используется для группирования свойств на нескольких шагах или страницах, если веб-часть требуется настраивать в линейном порядке или параметры, выбранные на первом шаге, влияют на то, какие параметры отображаются на втором.</span><span class="sxs-lookup"><span data-stu-id="92bb1-162">A steps pane is used for grouping properties in multiple steps or pages when you need the web part to be configured in a linear order or when choices made on the first step affect options that display on the second step.</span></span>

#### <a name="step-1-of-3"></a><span data-ttu-id="92bb1-163">Шаг 1 из 3</span><span class="sxs-lookup"><span data-stu-id="92bb1-163">Step 1 of 3</span></span>

![Область свойств с шагом 1 из 3](../../../images/design-wp-pp-pages-step1.png)

#### <a name="step-2-of-3"></a><span data-ttu-id="92bb1-165">Шаг 2 из 3</span><span class="sxs-lookup"><span data-stu-id="92bb1-165">Step 2 of 3</span></span>

![Область свойств с шагом 2 из 3](../../../images/design-wp-pp-pages-step2.png)

#### <a name="step-3-of-3"></a><span data-ttu-id="92bb1-167">Шаг 3 из 3</span><span class="sxs-lookup"><span data-stu-id="92bb1-167">Step 3 of 3</span></span>

![Область свойств с шагом 3 из 3](../../../images/design-wp-pp-pages-step3.png)


## <a name="reactive-vs-non-reactive-web-parts"></a><span data-ttu-id="92bb1-169">Сравнение реактивных и нереактивных веб-частей</span><span class="sxs-lookup"><span data-stu-id="92bb1-169">Reactive vs non-reactive web parts</span></span>

<span data-ttu-id="92bb1-170">**Реактивные веб-части** разрабатываются как полноценные клиентские веб-части, то есть каждый компонент, настроенный в области свойств, отражает изменения в веб-части на странице.</span><span class="sxs-lookup"><span data-stu-id="92bb1-170">Reactive web parts are designed to be full client-side web parts, which mean that each component that is configured in the properties pane will reflect as the change is made within the web part on the page. For the To-Do List web part, unchecking “Completed Tasks” will hide this view in the web part.</span></span> <span data-ttu-id="92bb1-171">Так, снятие флажка "Выполненные задачи" скрывает это представление в веб-части "Список дел".</span><span class="sxs-lookup"><span data-stu-id="92bb1-171">For example, for the To-Do List web part, unchecking “Completed Tasks” hides this view in the web part.</span></span>

![Оформление реактивной веб-части](../../../images/design-wp-pp-reactive.png)

<span data-ttu-id="92bb1-173">**Нереактивные веб-части** работают не только на стороне клиента. Как правило, одному или нескольким свойствам требуется совершить вызов, чтобы задать, получить или сохранить данные на сервере.</span><span class="sxs-lookup"><span data-stu-id="92bb1-173">Nonreactive web parts are not fully client-side; generally, one or more properties need to make a call to set/pull or store data on a server.</span></span> <span data-ttu-id="92bb1-174">В этом случае следует включить кнопки "Применить" и "Отмена" в нижней части области свойств.</span><span class="sxs-lookup"><span data-stu-id="92bb1-174">In this case, you should enable the Apply and Cancel buttons at the bottom of the properties pane.</span></span>

![Оформление нереактивной веб-части](../../../images/design-wp-pp-non-reactive.png)

## <a name="constructing-the-to-do-list-property-pane"></a><span data-ttu-id="92bb1-176">Создание области свойств для списка дел</span><span class="sxs-lookup"><span data-stu-id="92bb1-176">Constructing the To-Do List property pane</span></span>

<span data-ttu-id="92bb1-177">В примере со списком дел используются одиночная область и реактивная веб-часть.</span><span class="sxs-lookup"><span data-stu-id="92bb1-177">The To-Do List example uses the single pane and is a reactive web part. The following shows each Fabric React component and the resulting design.</span></span> <span data-ttu-id="92bb1-178">На схемах ниже показаны все компоненты Fabric React и соответствующее оформление.</span><span class="sxs-lookup"><span data-stu-id="92bb1-178">The following diagrams show each Fabric React component and the resulting design.</span></span>

#### <a name="adding-a-description-for-to-do-list"></a><span data-ttu-id="92bb1-179">Добавление описания для списка дел</span><span class="sxs-lookup"><span data-stu-id="92bb1-179">Adding a description for To-Do List Adding a description for To-Do List</span></span>

![Добавление описания для списка дел](../../../images/design-wp-todo-pp-description.png)

#### <a name="dropdown--to-select-tasks-from-an-existing-list"></a><span data-ttu-id="92bb1-181">Раскрывающийся список — для выбора задач из имеющегося списка</span><span class="sxs-lookup"><span data-stu-id="92bb1-181">Dropdown – to select tasks from an existing list</span></span>

![Раскрывающийся список для выбора задач из имеющегося списка](../../../images/design-wp-todo-pp-dropdown.png)

#### <a name="check-box--to-allow-authors-to-show-or-hide-different-views"></a><span data-ttu-id="92bb1-183">Флажок — с его помощью которого авторы могут показывать и скрывать различные представления</span><span class="sxs-lookup"><span data-stu-id="92bb1-183">Check box – to allow authors to show or hide different views</span></span>

![Флажок, с помощью которого авторы могут показывать и скрывать различные представления](../../../images/design-wp-todo-pp-checkbox.png)

#### <a name="slider--to-set-the-number-of-tasks-visible"></a><span data-ttu-id="92bb1-185">Ползунок — для выбора количества отображаемых задач</span><span class="sxs-lookup"><span data-stu-id="92bb1-185">Slider – to set the number of tasks visible Slider to set the number of tasks visible</span></span>

![Ползунок для выбора количества отображаемых задач](../../../images/design-wp-todo-pp-slider.png)

#### <a name="after-selecting-a-list-from-the-dropdown-the-web-part-shows-an-indicator-of-items-loading-onto-the-page"></a><span data-ttu-id="92bb1-187">После выбора элемента в раскрывающемся списке в веб-части отображается индикатор загрузки элементов на странице.</span><span class="sxs-lookup"><span data-stu-id="92bb1-187">After selecting a list from the drop down the web part shows and indicator of items loading onto the page Web part showing loading indicator to load items</span></span>

![Веб-часть с индикатором загрузки элементов](../../../images/design-wp-todo-loading-indicator.png)

#### <a name="when-the-new-tasks-are-loaded-they-fade-into-view-by-using-animation-styles-from-office-ui-fabric"></a><span data-ttu-id="92bb1-189">После загрузки новые задачи плавно появляются на экране. Для этого используются стили анимации из Office UI Fabric.</span><span class="sxs-lookup"><span data-stu-id="92bb1-189">When the new tasks are loaded, they fade into view by using animation components from Office UI Fabric.</span></span>

![Веб-часть с анимацией Fabric](../../../images/design-wp-todo-fabric-animations.png)

## <a name="see-also"></a><span data-ttu-id="92bb1-191">См. также</span><span class="sxs-lookup"><span data-stu-id="92bb1-191">See also</span></span>

- [<span data-ttu-id="92bb1-192">Разработка веб-части SharePoint</span><span class="sxs-lookup"><span data-stu-id="92bb1-192">Designing a SharePoint web part</span></span>](../../../design/design-a-web-part.md)
- [<span data-ttu-id="92bb1-193">Принципы дизайна SharePoint</span><span class="sxs-lookup"><span data-stu-id="92bb1-193">Designing great SharePoint experiences</span></span>](../../../design/design-guidance-overview.md)
