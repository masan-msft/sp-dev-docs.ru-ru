---
title: "Особенности разработки клиентских веб-частей SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 98a0662e893ea5f5729e6f77d01a51dcc5f57fb0
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="design-considerations-for-sharepoint-client-side-web-parts"></a><span data-ttu-id="3f036-102">Особенности разработки клиентских веб-частей SharePoint</span><span class="sxs-lookup"><span data-stu-id="3f036-102">Design considerations for SharePoint client-side web parts</span></span>

<span data-ttu-id="3f036-p101">Для разработки веб-частей необходимо понимание [Office UI Fabric](http://dev.office.com/fabric). Все стили из [Fabric Core](https://github.com/OfficeDev/office-ui-fabric-core) (включая значки, оформление, использование цветов, анимация и адаптируемая сетка) загружаются по умолчанию и доступны веб-части. Не импортируйте копию Fabric для веб-части, так как может возникнуть конфликт с глобальной копией. Эти классы формируют основу стиля веб-части, от которой можно отклоняться, если требуется другое оформление, соответствующее фирменной символике компании.</span><span class="sxs-lookup"><span data-stu-id="3f036-p101">To get started designing web parts, you will want to be familiar with [Office UI Fabric](http://dev.office.com/fabric). All of the styles from [Fabric Core](https://github.com/OfficeDev/office-ui-fabric-core) – including icons, typography, color usage, animation, and the responsive grid – are loaded by default and available to your web part. Do not import a copy of Fabric for your web part, as this may conflict with the global copy. These classes provide a foundation to your web part's styling, which you can always depart from if you require different visuals to match your company's brand.</span></span>

## <a name="office-ui-fabric-react-components"></a><span data-ttu-id="3f036-107">Компоненты Office UI Fabric React</span><span class="sxs-lookup"><span data-stu-id="3f036-107">Office UI Fabric React Components</span></span>

<span data-ttu-id="3f036-p102">Наряду с Office UI Fabric для создания веб-частей можно использовать компоненты Office UI Fabric React. Fabric React — это адаптируемая, рассчитанная на мобильные устройства коллекция компонентов, призванных ускорить и упростить создание веб-интерфейсов с помощью языка разработки Office.</span><span class="sxs-lookup"><span data-stu-id="3f036-p102">Along with Office UI Fabric, you can use Office UI Fabric React components to build your web parts. Fabric React is a responsive, mobile-first collection of  components designed to make it quick and simple for you to create web experiences using the Office Design Language.</span></span>

<span data-ttu-id="3f036-110">В приведенном ниже примере со списком дел компоненты Fabric используются в области свойств, с помощью которой автор страницы может настраивать веб-часть.</span><span class="sxs-lookup"><span data-stu-id="3f036-110">The following To Do list example uses Fabric components in the property pane that lets the page author configure a web part.</span></span>

![Пример веб-части списка дел, использующей Fabric](../../../images/design-wp-todo-example.png)

<span data-ttu-id="3f036-112">Полный список стилей, вариантов оформления, цветов, значков и анимаций Office UI Fabric представлен на странице [Стили Office UI Fabric](http://dev.office.com/fabric/styles).</span><span class="sxs-lookup"><span data-stu-id="3f036-112">You can find a complete list of the Office UI Fabric styles, typography, color, icons, and animations at [Office UI Fabric styles](http://dev.office.com/fabric/styles).</span></span>


## <a name="responsive-behavior"></a><span data-ttu-id="3f036-113">Адаптируемое поведение</span><span class="sxs-lookup"><span data-stu-id="3f036-113">Responsive behavior</span></span>

<span data-ttu-id="3f036-114">На страницах нового интерфейса разработки SharePoint используется адаптируемая сетка Office UI Fabric, обеспечивающая приятный внешний вид каждой страницы.</span><span class="sxs-lookup"><span data-stu-id="3f036-114">Pages in the new SharePoint authoring experience use the Office UI Fabric responsive grid to help ensure that each page will look great.</span></span> 

### <a name="max-width"></a><span data-ttu-id="3f036-115">Максимальная ширина</span><span class="sxs-lookup"><span data-stu-id="3f036-115">Max width</span></span>

<span data-ttu-id="3f036-p103">Рекомендуем использовать во всех веб-частях максимальную ширину 100 %, чтобы обеспечить их правильное расплавление и корректную работу на любой странице. Ширина страниц и столбцов определяется шаблоном страницы, но разработчик может менять ее. Если для веб-части задано максимальное количество пикселей, это может непредсказуемым образом повлиять на функции и макет страницы при ее просмотре на экранах разной ширины.</span><span class="sxs-lookup"><span data-stu-id="3f036-p103">We recommend that all web parts use a 100% maximum width to ensure that they will re-flow and function properly on any page. The page and column widths are defined by the page template but can be modified by the author. If a max pixel value is set in the web part, there could be unexpected results in both functionality and layout when the page is seen at different widths.</span></span>

![Адаптируемая максимальная ширина веб-части](../../../images/design-wp-responsive-max-width.png)

### <a name="min-width"></a><span data-ttu-id="3f036-120">Минимальная ширина</span><span class="sxs-lookup"><span data-stu-id="3f036-120">Min width</span></span>

<span data-ttu-id="3f036-121">Все веб-части должны поддерживать расплавление, так как ширина страниц и столбцов может уменьшаться до 320 пикселей.</span><span class="sxs-lookup"><span data-stu-id="3f036-121">All web parts should be designed to reflow as the page/column width gets smaller down to a min width of 320 px.</span></span>

![Адаптируемая минимальная ширина веб-части](../../../images/design-wp-responsive-min-width.png)

## <a name="web-part-published-mode-vs-edit-mode"></a><span data-ttu-id="3f036-123">Сравнение режимов публикации и правки веб-частей</span><span class="sxs-lookup"><span data-stu-id="3f036-123">Web part published mode vs edit mode</span></span>

<span data-ttu-id="3f036-124">У нового интерфейса создания страниц SharePoint есть два режима:</span><span class="sxs-lookup"><span data-stu-id="3f036-124">The new SharePoint page authoring experience has two modes:</span></span>

* <span data-ttu-id="3f036-125">**Режим публикации**, в котором группа или аудитория может просматривать содержимое и работать с веб-частями.</span><span class="sxs-lookup"><span data-stu-id="3f036-125">**Published mode** which allows your team or audience to view content and interact with web parts.</span></span>
* <span data-ttu-id="3f036-126">**Режим правки**, в котором авторы страницы могут добавлять и настраивать веб-части, чтобы добавлять содержимое на страницу.</span><span class="sxs-lookup"><span data-stu-id="3f036-126">**Edit mode** which allows page author(s) to add and configure web parts to add content to a page.</span></span>

### <a name="edit-mode"></a><span data-ttu-id="3f036-127">Режим правки</span><span class="sxs-lookup"><span data-stu-id="3f036-127">Edit mode</span></span>

#### <a name="add-hint-and-toolbox"></a><span data-ttu-id="3f036-128">Подсказка о добавлении и панель элементов</span><span class="sxs-lookup"><span data-stu-id="3f036-128">Add hint and Toolbox</span></span>

<span data-ttu-id="3f036-p104">Подсказка о добавлении — это горизонтальная линия со значком "плюс", которая отображается при выделении веб-части или наведении указателя мыши на нее и указывает, что авторы могут добавлять веб-части на свою страницу. Когда пользователь нажимает значок "плюс", открывается панель элементов. Панель элементов содержит все веб-части, которые можно добавить на страницу.</span><span class="sxs-lookup"><span data-stu-id="3f036-p104">The add hint is a horizontal line with a plus icon that is visible when a web part is selected and on hover to indicate where page authors can add new web parts to their page. The toolbox opens when a user clicks/taps the plus icon. The toolbox contains all the web parts that can be added to a page.</span></span>

![Подсказка о добавлении и панель элементов веб-части](../../../images/design-wp-toolbox.png)

#### <a name="toolbar"></a><span data-ttu-id="3f036-133">Панель инструментов</span><span class="sxs-lookup"><span data-stu-id="3f036-133">Toolbar</span></span>

<span data-ttu-id="3f036-p105">Вертикальная панель инструментов и ограничивающий прямоугольник входят в состав платформы для каждой веб-части и предоставляются страницей. Для каждой веб-части на панели инструментов есть действия редактирования и удаления.</span><span class="sxs-lookup"><span data-stu-id="3f036-p105">A vertical toolbar and bounding box is part of the framework for every web part and provided by the page. Each web part has an edit and delete action in the toolbar.</span></span>

![Вертикальная панель инструментов для веб-части](../../../images/design-wp-toolbar.png)

#### <a name="contextual-edits"></a><span data-ttu-id="3f036-137">Контекстная правка</span><span class="sxs-lookup"><span data-stu-id="3f036-137">Contextual edits</span></span>

<span data-ttu-id="3f036-p106">Для веб-частей следует разработать интерфейс в режиме WYSIWYG, где можно вводить данные и добавлять содержимое, которое увидит пользователь после публикации. Добавлять содержимое следует на странице, чтобы пользователь понимал, как оно будет выглядеть. Например, заголовки и описания следует вводить там, где будет отображаться текст, а новые задачи следует добавлять и редактировать в контексте страницы.</span><span class="sxs-lookup"><span data-stu-id="3f036-p106">A WYSIWYG experience should be designed for web parts to fill in information or add content that will be displayed to the user when published. Entering this content should be done in page so the user understands how the viewer will see the content. For example, titles and descriptions should be filled out where the text displays or new tasks should be added and modified in context of the page.</span></span>

![Контекстная правка веб-частей](../../../images/design-wp-contexual-edits.png)

#### <a name="item-level-edits"></a><span data-ttu-id="3f036-142">Правка на уровне элементов</span><span class="sxs-lookup"><span data-stu-id="3f036-142">Item-level edits</span></span>

<span data-ttu-id="3f036-143">Пользовательский интерфейс веб-части может меняться. Например, текст может превращаться в текстовое поле для ввода ссылок, а при отображении интерфейса можно менять порядок элементов и отмечать задачи в веб-части.</span><span class="sxs-lookup"><span data-stu-id="3f036-143">UI can change within the web part; for example, turning text into a text field to fill out links or when displaying UI to reorder items or to check of tasks in a web part</span></span>

![Правка веб-части на уровне элементов](../../../images/design-wp-item-level-edits.png)

## <a name="property-panes"></a><span data-ttu-id="3f036-145">Области свойств</span><span class="sxs-lookup"><span data-stu-id="3f036-145">Property panes</span></span>

<span data-ttu-id="3f036-p107">Области свойств вызываются с помощью значка редактирования на панели инструментов. Области в первую очередь должны содержать параметры конфигурации для включения и отключения компонентов, которые либо отображаются на странице, либо вызывают службу для отображения содержимого.</span><span class="sxs-lookup"><span data-stu-id="3f036-p107">Property panes are invoked via the edit action icon on the toolbar. Panes should primarily contain configuration settings that enable/disable features that either show on page or that make a call to a service to display content.</span></span>

![Оформление области свойств веб-части](../../../images/design-wp-pp.png)

<span data-ttu-id="3f036-149">Существует три типа областей свойств, позволяющих создавать и оформлять веб-части в соответствии с потребностями бизнеса или клиентов.</span><span class="sxs-lookup"><span data-stu-id="3f036-149">There are three types of property panes to enable you to design and develop web parts that fit your business or customer needs.</span></span>

### <a name="single-pane"></a><span data-ttu-id="3f036-150">Одиночная область</span><span class="sxs-lookup"><span data-stu-id="3f036-150">Single pane</span></span>

<span data-ttu-id="3f036-151">Одиночная область используется для простых веб-частей с небольшим количеством настраиваемых свойств.</span><span class="sxs-lookup"><span data-stu-id="3f036-151">A single pane is used for simple web parts that only have a small number of properties to configure.</span></span>

![Оформление одиночной области свойств веб-части](../../../images/design-wp-pp-single.png)

### <a name="accordion-pane"></a><span data-ttu-id="3f036-153">Область-гармошка</span><span class="sxs-lookup"><span data-stu-id="3f036-153">Accordion pane</span></span>

<span data-ttu-id="3f036-p108">Область-гармошка используется для размещения групп свойств с большим количеством вариантов, образующих длинный прокручивающийся список. Например, у вас может быть три группы с названиями "Свойства", "Внешний вид" и "Макет", по десять компонентов в каждой.</span><span class="sxs-lookup"><span data-stu-id="3f036-p108">A accordion pane is used for containing a group or groups of properties with many options and where the groups would result in a long scrolling list of options. For example, you might have three groups named Properties, Appearance, and Layout, each with ten components.</span></span>

#### <a name="accordion---one-group-open"></a><span data-ttu-id="3f036-156">Гармошка с одной открытой группой</span><span class="sxs-lookup"><span data-stu-id="3f036-156">Accordion - One group open</span></span>

![Область-гармошка свойств веб-части с одной открытой группой](../../../images/design-wp-pp-accordion.png)

#### <a name="accordion--two-groups-open-and-scrolled"></a><span data-ttu-id="3f036-158">Гармошка с двумя открытыми прокручивающимися группами</span><span class="sxs-lookup"><span data-stu-id="3f036-158">Accordion- Two groups open and scrolled</span></span>

![Область-гармошка свойств веб-части с двумя открытыми прокручивающимися группами](../../../images/design-wp-pp-accordion-groups.png)


### <a name="property-pane-stepspages"></a><span data-ttu-id="3f036-160">Ступенчатые и страничные области свойств</span><span class="sxs-lookup"><span data-stu-id="3f036-160">Property pane steps/pages</span></span>

<span data-ttu-id="3f036-161">Ступенчатая область используется для группирования свойств на нескольких шагах или страницах, если веб-часть требуется настраивать в линейном порядке или параметры, выбранные на первом шаге, влияют на то, какие параметры отображаются на втором.</span><span class="sxs-lookup"><span data-stu-id="3f036-161">A steps pane is used for grouping properties in multiple steps or pages when you need the web part to be configured in a linear order or when choices made on the first step affect options that display on the second step.</span></span>

<span data-ttu-id="3f036-162">**Шаг 1 из 3**![Область свойств с шагом 1 из 3](../../../images/design-wp-pp-pages-step1.png)</span><span class="sxs-lookup"><span data-stu-id="3f036-162">**Step 1 of 3**
![Property pane with steps design 1 of 3](../../../images/design-wp-pp-pages-step1.png)</span></span>

<span data-ttu-id="3f036-163">**Шаг 2 из 3**![Область свойств с шагом 2 из 3](../../../images/design-wp-pp-pages-step2.png)</span><span class="sxs-lookup"><span data-stu-id="3f036-163">**Step 2 of 3**
![Property pane with steps design 2 of 3](../../../images/design-wp-pp-pages-step2.png)</span></span>

<span data-ttu-id="3f036-164">**Шаг 3 из 3**![Область свойств с шагом 3 из 3](../../../images/design-wp-pp-pages-step3.png)</span><span class="sxs-lookup"><span data-stu-id="3f036-164">**Step 3 of 3**
![Property pane with steps design 3 of 3](../../../images/design-wp-pp-pages-step3.png)</span></span>


## <a name="reactive-vs-non-reactive-web-parts"></a><span data-ttu-id="3f036-165">Сравнение реактивных и нереактивных веб-частей</span><span class="sxs-lookup"><span data-stu-id="3f036-165">Reactive vs non-reactive web parts</span></span>

<span data-ttu-id="3f036-p109">Реактивные веб-части разрабатываются как полноценные клиентские веб-части, то есть каждый компонент, настроенный в свойствах, отражает изменения в веб-части на странице. В веб-части "Список дел" при снятии флажка "Выполненные задачи" скрывается соответствующее представление в веб-части.</span><span class="sxs-lookup"><span data-stu-id="3f036-p109">Reactive web parts are designed to be full client-side web parts, which mean that each component that is configured in the properties pane will reflect as the change is made within the web part on the page. For the To-Do List web part, unchecking “Completed Tasks” will hide this view in the web part.</span></span>

![Оформление реактивной веб-части](../../../images/design-wp-pp-reactive.png)

<span data-ttu-id="3f036-p110">Нереактивные веб-части работают не только на стороне клиента. Как правило, одному или нескольким свойствам требуется совершить вызов, чтобы задать, получить или сохранить данные на сервере. В этом случае следует включить кнопки "Применить" и "Отмена" в нижней части области свойств.</span><span class="sxs-lookup"><span data-stu-id="3f036-p110">Non-reactive web parts are not fully client side and generally one or more properties need to make a call to set/pull or store data on a server. In this case, you should enable the Apply and Cancel buttons at the bottom of the properties pane.</span></span>

![Оформление нереактивной веб-части](../../../images/design-wp-pp-non-reactive.png)

## <a name="constructing-the-to-do-list-property-pane"></a><span data-ttu-id="3f036-172">Создание области свойств для списка дел</span><span class="sxs-lookup"><span data-stu-id="3f036-172">Constructing the To-Do List property pane</span></span>

<span data-ttu-id="3f036-p111">В примере со списком дел используются одиночная область и реактивная веб-часть. Ниже показаны все компоненты Fabric React и соответствующее оформление.</span><span class="sxs-lookup"><span data-stu-id="3f036-p111">The To-Do List example uses the single pane and is a reactive web part. The following shows each Fabric React component and the resulting design.</span></span>

<span data-ttu-id="3f036-175">Добавление описания списка дел ![Добавление описания списка дел](../../../images/design-wp-todo-pp-description.png)</span><span class="sxs-lookup"><span data-stu-id="3f036-175">Adding a description for To-Do List ![Adding a description for To-Do List](../../../images/design-wp-todo-pp-description.png)</span></span>

<span data-ttu-id="3f036-176">Раскрывающийся список для выбора задач из имеющегося списка ![Раскрывающийся список для выбора задач из имеющегося списка](../../../images/design-wp-todo-pp-dropdown.png)</span><span class="sxs-lookup"><span data-stu-id="3f036-176">Drop down – to select tasks from an existing list ![Drop down to select tasks from an existing list](../../../images/design-wp-todo-pp-dropdown.png)</span></span>

<span data-ttu-id="3f036-177">Флажок, с помощью которого авторы могут показывать и скрывать различные представления ![Флажок, с помощью которого авторы могут показывать и скрывать различные представления](../../../images/design-wp-todo-pp-checkbox.png)</span><span class="sxs-lookup"><span data-stu-id="3f036-177">Checkbox– to allow authors to show or hide different views ![Checkbox to allow authors to show or hide different views](../../../images/design-wp-todo-pp-checkbox.png)</span></span>

<span data-ttu-id="3f036-178">Ползунок для выбора количества отображаемых задач ![Ползунок для выбора количества отображаемых задач](../../../images/design-wp-todo-pp-slider.png)</span><span class="sxs-lookup"><span data-stu-id="3f036-178">Slider – to set the number of tasks visible ![Slider to set the number of tasks visible](../../../images/design-wp-todo-pp-slider.png)</span></span>

<span data-ttu-id="3f036-179">После выбора элемента в раскрывающемся списке в веб-части отображается индикатор загрузки элементов на странице ![Веб-часть с индикатором загрузки элементов](../../../images/design-wp-todo-loading-indicator.png)</span><span class="sxs-lookup"><span data-stu-id="3f036-179">After selecting a list from the drop down the web part shows and indicator of items loading onto the page ![Web part showing loading indicator to load items](../../../images/design-wp-todo-loading-indicator.png)</span></span>

<span data-ttu-id="3f036-180">После загрузки новые задачи плавно появляются с использованием стилей анимации из Office UI Fabric ![Веб-часть с анимацией Fabric](../../../images/design-wp-todo-fabric-animations.png)</span><span class="sxs-lookup"><span data-stu-id="3f036-180">When the new tasks are loaded the fade into view using animation styles from Office UI Fabric ![Web part with fabric animations](../../../images/design-wp-todo-fabric-animations.png)</span></span>
