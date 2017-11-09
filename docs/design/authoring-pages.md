---
title: "Разработка страниц на сайте SharePoint"
ms.date: 9/25/2017
ms.openlocfilehash: 349de6ef579d2313ddaa27a178cab9c31654e223
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="authoring-pages-in-a-sharepoint-site"></a><span data-ttu-id="3b93d-102">Разработка страниц на сайте SharePoint</span><span class="sxs-lookup"><span data-stu-id="3b93d-102">Authoring pages in a SharePoint site</span></span>

<span data-ttu-id="3b93d-103">Разработка страниц в SharePoint — это простой процесс, тем не менее требующий знакомства со средой SharePoint, а также понимания того, для каких целей и для какой аудитории создается страница.</span><span class="sxs-lookup"><span data-stu-id="3b93d-103">Authoring pages in SharePoint is a simple process, but it does require some familiarity with the SharePoint environment, as well as an understanding of what and who you are designing the page for.</span></span> <span data-ttu-id="3b93d-104">Приступая к разработке, полезно следовать нескольким базовым принципам, например "начинайте с простого" и "развивайте то, что работает".</span><span class="sxs-lookup"><span data-stu-id="3b93d-104">A few basic principles – like remembering to "Start simple" and "Build on what's working" - are valuable things to consider as you start authoring.</span></span> <span data-ttu-id="3b93d-105">Кроме того, полезно регулярно напоминать себе о своей аудитории и целях, которых вы пытаетесь помочь ей достичь.</span><span class="sxs-lookup"><span data-stu-id="3b93d-105">It's also a good idea to consistently remind yourself of your audience, and the goals that you are trying to help them achieve.</span></span>

<!-- Do we have content about the design principles that we can link to here? -->

<span data-ttu-id="3b93d-106">У интерфейса создания страниц SharePoint есть два режима.</span><span class="sxs-lookup"><span data-stu-id="3b93d-106">The new SharePoint page authoring experience has two modes:</span></span> 

- <span data-ttu-id="3b93d-107">В режиме правки авторы страниц могут добавлять и настраивать веб-части, чтобы добавлять содержимое на страницу.</span><span class="sxs-lookup"><span data-stu-id="3b93d-107">Edit mode which allows page author(s) to add and configure web parts to add content to a page.</span></span>
- <span data-ttu-id="3b93d-108">В режиме публикации группа или аудитория может просматривать содержимое и работать с веб-частями.</span><span class="sxs-lookup"><span data-stu-id="3b93d-108">Published mode which allows your team or audience to view content and interact with web parts.</span></span> 

## <a name="edit-mode"></a><span data-ttu-id="3b93d-109">Режим правки</span><span class="sxs-lookup"><span data-stu-id="3b93d-109">Edit mode</span></span>

<span data-ttu-id="3b93d-110">При создании страницы пользователям доступен пользовательский интерфейс разработки для добавления и настройки содержимого страницы.</span><span class="sxs-lookup"><span data-stu-id="3b93d-110">When creating a new page, users have access to the authoring UI to add content to and customize the page content.</span></span> 


![Элемент управления "Поле ввода"](../images/design-authoring-edit-01.png)

![Элемент управления "Поле ввода" с указателем, наведенным на выделенный элемент](../images/design-authoring-edit-02.png)


### <a name="add-hint-and-toolbox"></a><span data-ttu-id="3b93d-113">Подсказка о добавлении и панель элементов</span><span class="sxs-lookup"><span data-stu-id="3b93d-113">Add hint and Toolbox</span></span>

<span data-ttu-id="3b93d-114">Подсказка о добавлении — это горизонтальная линия со значком "плюс", которая отображается при выделении веб-части или наведении указателя мыши на нее и указывает на то, что авторы могут добавлять веб-части на свою страницу.</span><span class="sxs-lookup"><span data-stu-id="3b93d-114">The add hint is a horizontal line with a plus icon that is visible when a web part is selected and on hover to indicate where page authors can add new web parts to their page. The toolbox opens when a user clicks/taps the plus icon. The toolbox contains all the web parts that can be added to a page.</span></span> <span data-ttu-id="3b93d-115">Когда пользователь нажимает значок "плюс", открывается панель элементов.</span><span class="sxs-lookup"><span data-stu-id="3b93d-115">The Toolbox opens when a user chooses the plus icon.</span></span> <span data-ttu-id="3b93d-116">Панель элементов содержит все веб-части, которые можно добавить на страницу.</span><span class="sxs-lookup"><span data-stu-id="3b93d-116">The Toolbox contains all the web parts that can be added to a page.</span></span>

![Подсказка и панель элементов с инструментами](../images/design-authoring-add-hint.png)


### <a name="toolbar"></a><span data-ttu-id="3b93d-118">Панель инструментов</span><span class="sxs-lookup"><span data-stu-id="3b93d-118">Toolbar</span></span>

<span data-ttu-id="3b93d-119">Вертикальная панель инструментов и ограничивающий прямоугольник входят в состав платформы для каждой веб-части и предоставляются страницей.</span><span class="sxs-lookup"><span data-stu-id="3b93d-119">A vertical toolbar and bounding box is part of the framework for every web part and provided by the page. Each web part has an edit and delete action in the toolbar.</span></span> <span data-ttu-id="3b93d-120">Для каждой веб-части на панели инструментов есть действия редактирования и удаления.</span><span class="sxs-lookup"><span data-stu-id="3b93d-120">Each web part has an edit and delete action in the toolbar.</span></span> 

![Развернутая панель инструментов](../images/design-authoring-toolbar.png)


### <a name="active-and-hover-states"></a><span data-ttu-id="3b93d-122">Активное и плавающее состояния</span><span class="sxs-lookup"><span data-stu-id="3b93d-122">Active and hover states</span></span>

<span data-ttu-id="3b93d-123">В активном и плавающем состояниях обычно отображаются линии подсказок синего цвета или основного цвета темы сайта.</span><span class="sxs-lookup"><span data-stu-id="3b93d-123">On hover/active, the hint bars are primary blue or the primary theme color for the site.</span></span>

![Плавающее и активное состояние](../images/design-authoring-active-hover-01.png)

<span data-ttu-id="3b93d-125">По умолчанию веб-часть окружена серым ограничивающим прямоугольником, но при наведении указателя или выборе веб-части его цвет меняется на синий или основной цвет темы сайта.</span><span class="sxs-lookup"><span data-stu-id="3b93d-125">The bounding box for a web part is gray by default, but picks up the primary blue or primary theme color for the site on hover or when the web part is selected.</span></span>

![Ограничивающий прямоугольник в активном и неактивном состояниях](../images/design-authoring-active-hover-02.png)


### <a name="contextual-edits"></a><span data-ttu-id="3b93d-127">Контекстная правка</span><span class="sxs-lookup"><span data-stu-id="3b93d-127">Contextual edits</span></span>

<span data-ttu-id="3b93d-128">Создавайте для веб-частей интерфейс в режиме WYSIWYG, чтобы пользователи могли указывать сведения и добавлять содержимое, которое будет отображаться при публикации.</span><span class="sxs-lookup"><span data-stu-id="3b93d-128">Design a WYSIWYG experience for web parts so that users can fill in information or add content that will be displayed when published.</span></span> <span data-ttu-id="3b93d-129">Это содержимое следует добавлять на странице, чтобы пользователь понимал, как оно будет отображаться.</span><span class="sxs-lookup"><span data-stu-id="3b93d-129">This content should be entered on the page so the user understands how the it will render in the viewer.</span></span> <span data-ttu-id="3b93d-130">Например, заголовки и описания следует вводить там, где будет отображаться текст, а новые задачи следует добавлять и редактировать в контексте страницы.</span><span class="sxs-lookup"><span data-stu-id="3b93d-130">For example, titles and descriptions should be filled out where the text displays; new tasks should be added and modified in the context of the page.</span></span>

![Элемент формы для контекстной правки](../images/design-authoring-contextual-edits.png)


### <a name="item-level-edits"></a><span data-ttu-id="3b93d-132">Правка на уровне элементов</span><span class="sxs-lookup"><span data-stu-id="3b93d-132">Item-level edits</span></span>

<span data-ttu-id="3b93d-133">Пользовательский интерфейс веб-части может меняться. Например, текст может превращаться в текстовое поле, а при отображении интерфейса можно менять порядок элементов и отмечать задачи в веб-части.</span><span class="sxs-lookup"><span data-stu-id="3b93d-133">UI can change within the web part; for example, turning text into a text field to fill out links or when displaying UI to reorder items or to check of tasks in a web part</span></span> <span data-ttu-id="3b93d-134">Вы можете включить интерактивные функции веб-частей в режиме правки, режиме чтения или в обоих режимах в зависимости от целей разработки.</span><span class="sxs-lookup"><span data-stu-id="3b93d-134">You can enable interactive functionality for web parts in edit mode, in read mode, or in both, depending on your design intent.</span></span>

![Правка на уровне элемента с выбранным состоянием](../images/design-authoring-item-level.png)


### <a name="property-panes"></a><span data-ttu-id="3b93d-136">Области свойств</span><span class="sxs-lookup"><span data-stu-id="3b93d-136">Property panes</span></span>

<span data-ttu-id="3b93d-137">Области свойств вызываются с помощью значка **Правка** на панели инструментов.</span><span class="sxs-lookup"><span data-stu-id="3b93d-137">Property panes are invoked via the **Edit** icon on the toolbar.</span></span> <span data-ttu-id="3b93d-138">Области свойств в первую очередь должны содержать параметры конфигурации для включения и отключения компонентов, которые либо отображаются на странице, либо вызывают службу для отображения содержимого.</span><span class="sxs-lookup"><span data-stu-id="3b93d-138">Property panes are invoked via the edit action icon on the toolbar. Panes should primarily contain configuration settings that enable/disable features that either show on page or that make a call to a service to display content.</span></span> 

![Развернутая панель](../images/design-authoring-panes.png)


## <a name="published-mode"></a><span data-ttu-id="3b93d-140">Режим публикации</span><span class="sxs-lookup"><span data-stu-id="3b93d-140">Published mode</span></span>

<span data-ttu-id="3b93d-141">После публикации страницы пользовательский интерфейс редактирования отключается для посетителей страницы.</span><span class="sxs-lookup"><span data-stu-id="3b93d-141">After the page is published, all edit UI is disabled and for the viewer or reader of the page.</span></span> <span data-ttu-id="3b93d-142">Чтобы продолжить ее редактировать, пользователь может нажать кнопку **Изменить** в правом верхнем углу панели команд.</span><span class="sxs-lookup"><span data-stu-id="3b93d-142">To continue editing the page, the user selects the **Edit** button on the top right corner of the command bar.</span></span>

![Выделенная кнопка "Опубликовать"](../images/design-authoring-published.png)


## <a name="mobile-view"></a><span data-ttu-id="3b93d-144">Мобильное представление</span><span class="sxs-lookup"><span data-stu-id="3b93d-144">Mobile view</span></span>

<span data-ttu-id="3b93d-145">Все страницы SharePoint являются [адаптивными](grid-and-responsive-design.md), то есть их содержимое можно просматривать на мобильных устройствах.</span><span class="sxs-lookup"><span data-stu-id="3b93d-145">All SharePoint pages are [responsive](grid-and-responsive-design.md) to allow the content of the page to be viewed on mobile devices.</span></span> <span data-ttu-id="3b93d-146">При разработке веб-части важно понимать, как новые страницы сайтов SharePoint отображаются на разных устройствах.</span><span class="sxs-lookup"><span data-stu-id="3b93d-146">While designing a web part, it is important to understand how the new SharePoint site pages render across different devices.</span></span>



![Мобильное представление сайта](../images/design-authoring-mobile.png)