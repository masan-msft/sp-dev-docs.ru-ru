---
title: "Разработка страниц на сайте SharePoint"
description: "Разработка страниц в режиме правки, редактирование после публикации и просмотр с мобильного устройства."
ms.date: 1/23/2018
ms.openlocfilehash: 048105633e6c2b66e06ef3eca899c19bf19d59c0
ms.sourcegitcommit: 0ad5aeee2c5efc47eb57e050581e4f411c4be643
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/29/2018
---
# <a name="authoring-pages-in-a-sharepoint-site"></a><span data-ttu-id="cfe3b-103">Разработка страниц на сайте SharePoint</span><span class="sxs-lookup"><span data-stu-id="cfe3b-103">Authoring pages in a SharePoint site</span></span>

<span data-ttu-id="cfe3b-104">Разработка страниц в SharePoint — это простой процесс, тем не менее требующий знакомства со средой SharePoint, а также понимания того, для каких целей и для какой аудитории создается страница.</span><span class="sxs-lookup"><span data-stu-id="cfe3b-104">Authoring pages in SharePoint is a simple process, but it does require some familiarity with the SharePoint environment, as well as an understanding of what and who you are designing the page for.</span></span> <span data-ttu-id="cfe3b-105">Приступая к разработке, помните, что лучше "начинать с простого" и "развивать то, что работает".</span><span class="sxs-lookup"><span data-stu-id="cfe3b-105">A few basic principles – like remembering to "Start simple" and "Build on what's working" - are valuable things to consider as you start authoring.</span></span> <span data-ttu-id="cfe3b-106">Кроме того, полезно постоянно держать в уме свою аудиторию и назначение страницы.</span><span class="sxs-lookup"><span data-stu-id="cfe3b-106">It's also a good idea to consistently remind yourself of your audience, and the goals that you are trying to help them achieve.</span></span>

<!-- Do we have content about the design principles that we can link to here? -->

<span data-ttu-id="cfe3b-107">Разработка страниц SharePoint может выполняться в двух режимах:</span><span class="sxs-lookup"><span data-stu-id="cfe3b-107">The SharePoint page authoring experience has two modes:</span></span> 

- <span data-ttu-id="cfe3b-108">**Правка**.</span><span class="sxs-lookup"><span data-stu-id="cfe3b-108">edit</span></span> <span data-ttu-id="cfe3b-109">В этом режиме авторы страниц могут добавлять и настраивать веб-части, чтобы добавлять контент на страницу.</span><span class="sxs-lookup"><span data-stu-id="cfe3b-109">Edit - Allows page authors to add and configure web parts to add content to a page.</span></span>
- <span data-ttu-id="cfe3b-110">**Опубликовано**.</span><span class="sxs-lookup"><span data-stu-id="cfe3b-110">**published**</span></span> <span data-ttu-id="cfe3b-111">В этом режиме группа или аудитория может просматривать контент и взаимодействовать с веб-частями.</span><span class="sxs-lookup"><span data-stu-id="cfe3b-111">Published - Allows your team or audience to view content and interact with web parts.</span></span> 

## <a name="edit-mode"></a><span data-ttu-id="cfe3b-112">Режим правки</span><span class="sxs-lookup"><span data-stu-id="cfe3b-112">Edit mode</span></span>

<span data-ttu-id="cfe3b-113">При создании страницы пользователям доступен интерфейс для добавления и настройки контента.</span><span class="sxs-lookup"><span data-stu-id="cfe3b-113">When creating a new page, users have access to the authoring UI to add content to and customize the page content.</span></span> 

<img alt="Edit control" src="../images/design-authoring-edit-01.png" width="850">

<br/>

<img alt="Edit control with cursor showing highlight" src="../images/design-authoring-edit-02.png" width="850">

<br/>

### <a name="add-hint-and-toolbox"></a><span data-ttu-id="cfe3b-114">Подсказка о добавлении и панель элементов</span><span class="sxs-lookup"><span data-stu-id="cfe3b-114">Add hint and Toolbox</span></span>

<span data-ttu-id="cfe3b-115">Подсказка о добавлении — это горизонтальная линия со значком "плюс", которая отображается при выделении веб-части или наведении указателя мыши на нее и указывает, что авторы могут добавлять веб-части на свою страницу.</span><span class="sxs-lookup"><span data-stu-id="cfe3b-115">The add hint is a horizontal line with a plus icon that is visible when a web part is selected and on hover to indicate where page authors can add new web parts to their page.</span></span> <span data-ttu-id="cfe3b-116">Когда пользователь нажимает значок "плюс", открывается панель элементов.</span><span class="sxs-lookup"><span data-stu-id="cfe3b-116">The Toolbox opens when a user chooses the plus icon.</span></span> <span data-ttu-id="cfe3b-117">Панель элементов содержит все веб-части, которые можно добавить на страницу.</span><span class="sxs-lookup"><span data-stu-id="cfe3b-117">The Toolbox contains all the web parts that can be added to a page.</span></span>

<img alt="Hint and toolbox showing tools" src="../images/design-authoring-add-hint.png" width="850">

<br/>

### <a name="toolbar"></a><span data-ttu-id="cfe3b-118">Панель инструментов</span><span class="sxs-lookup"><span data-stu-id="cfe3b-118">Toolbar</span></span>

<span data-ttu-id="cfe3b-119">Вертикальная панель инструментов и ограничивающий прямоугольник входят в состав платформы для каждой веб-части и предоставляются страницей.</span><span class="sxs-lookup"><span data-stu-id="cfe3b-119">A vertical toolbar and bounding box is part of the framework for every web part and is provided by the page.</span></span> <span data-ttu-id="cfe3b-120">Для каждой веб-части на панели инструментов есть действия редактирования и удаления.</span><span class="sxs-lookup"><span data-stu-id="cfe3b-120">Each web part has an edit and delete action in the toolbar.</span></span> 

<img alt="Expanded toolbar" src="../images/design-authoring-toolbar.png" width="850">

<br/>

### <a name="active-and-hover-states"></a><span data-ttu-id="cfe3b-121">Активное и выделенное состояния</span><span class="sxs-lookup"><span data-stu-id="cfe3b-121">Active and hover states</span></span>

<span data-ttu-id="cfe3b-122">В активном и выделенном состояниях обычно отображаются панели подсказок базового синего цвета или основного цвета темы сайта.</span><span class="sxs-lookup"><span data-stu-id="cfe3b-122">On hover/active, the hint bars are primary blue or the primary theme color for the site.</span></span>

<img alt="Hover and active state" src="../images/design-authoring-active-hover-01.png" width="850">

<br/>

<span data-ttu-id="cfe3b-123">По умолчанию веб-часть окружена серым ограничивающим прямоугольником, но при наведении указателя или выборе веб-части его цвет меняется на базовый синий или основной цвет темы сайта.</span><span class="sxs-lookup"><span data-stu-id="cfe3b-123">The bounding box for a web part is gray by default, but picks up the primary blue or primary theme color for the site on hover or when the web part is selected.</span></span>

<img alt="Bounding box on and off" src="../images/design-authoring-active-hover-02.png" width="850">

<br/>

### <a name="contextual-edits"></a><span data-ttu-id="cfe3b-124">Контекстная правка</span><span class="sxs-lookup"><span data-stu-id="cfe3b-124">Contextual edits</span></span>

<span data-ttu-id="cfe3b-125">Разработайте для веб-частей среду WYSIWYG, чтобы пользователи могли указывать информацию или добавлять контент после публикации.</span><span class="sxs-lookup"><span data-stu-id="cfe3b-125">Design a WYSIWYG experience for web parts so that users can fill in information or add content that will be displayed when published.</span></span> <span data-ttu-id="cfe3b-126">Этот контент следует добавлять на странице, чтобы пользователь понимал, как он будет выглядеть.</span><span class="sxs-lookup"><span data-stu-id="cfe3b-126">This content should be entered on the page so the user understands how the it will render in the viewer.</span></span> <span data-ttu-id="cfe3b-127">Например, названия и описания следует вводить там, где будет отображаться текст, а новые задачи следует добавлять и редактировать в контексте страницы.</span><span class="sxs-lookup"><span data-stu-id="cfe3b-127">For example, titles and descriptions should be filled out where the text displays; new tasks should be added and modified in the context of the page.</span></span>

![Элемент формы для контекстной правки](../images/design-authoring-contextual-edits.png)

<br/>

### <a name="item-level-edits"></a><span data-ttu-id="cfe3b-129">Правка на уровне элементов</span><span class="sxs-lookup"><span data-stu-id="cfe3b-129">Item-level edits</span></span>

<span data-ttu-id="cfe3b-130">Пользовательский интерфейс веб-части может меняться. Например, текст может превращаться в текстовое поле, а при отображении интерфейса можно менять порядок элементов и отмечать задачи в веб-части.</span><span class="sxs-lookup"><span data-stu-id="cfe3b-130">UI can change within the web part; for example, text can become a text field, or you can display UI to reorder items or to check off tasks in a web part.</span></span> <span data-ttu-id="cfe3b-131">Вы можете включить интерактивные функции веб-частей в режиме правки, режиме чтения или в обоих режимах в зависимости от целей разработки.</span><span class="sxs-lookup"><span data-stu-id="cfe3b-131">You can enable interactive functionality for web parts in edit mode, in read mode, or in both, depending on your design intent.</span></span>

![Правка на уровне элемента с выбранным состоянием](../images/design-authoring-item-level.png)

<br/>

### <a name="property-panes"></a><span data-ttu-id="cfe3b-133">Области свойств</span><span class="sxs-lookup"><span data-stu-id="cfe3b-133">Property panes</span></span>

<span data-ttu-id="cfe3b-134">Области свойств вызываются с помощью значка **Изменить** на панели инструментов.</span><span class="sxs-lookup"><span data-stu-id="cfe3b-134">Property panes are invoked via the **Edit** icon on the toolbar.</span></span> <span data-ttu-id="cfe3b-135">Области свойств в первую очередь должны содержать параметры конфигурации для включения и отключения компонентов, которые либо отображаются на странице, либо вызывают службу для отображения контента.</span><span class="sxs-lookup"><span data-stu-id="cfe3b-135">Property panes should primarily contain configuration settings that enable or disable features that either show on page, or make a call to a service to display content.</span></span> 

![Развернутая панель](../images/design-authoring-panes.png)

<br/>

## <a name="published-mode"></a><span data-ttu-id="cfe3b-137">Режим "Опубликовано"</span><span class="sxs-lookup"><span data-stu-id="cfe3b-137">Published mode</span></span>

<span data-ttu-id="cfe3b-138">После публикации интерфейс редактирования недоступен для посетителей страницы.</span><span class="sxs-lookup"><span data-stu-id="cfe3b-138">After the page is published, all edit UI is disabled and for the viewer or reader of the page.</span></span> <span data-ttu-id="cfe3b-139">Чтобы продолжить редактирование, пользователь нажимает кнопку **Изменить** в правом верхнем углу панели команд.</span><span class="sxs-lookup"><span data-stu-id="cfe3b-139">To continue editing the page, the user selects the **Edit** button on the top right corner of the command bar.</span></span>

![Выделенная кнопка "Опубликовать"](../images/design-authoring-published.png)

<br/>

## <a name="mobile-view"></a><span data-ttu-id="cfe3b-141">Мобильное представление</span><span class="sxs-lookup"><span data-stu-id="cfe3b-141">Mobile view</span></span>

<span data-ttu-id="cfe3b-142">Все страницы SharePoint являются [адаптивными](grid-and-responsive-design.md), то есть их контент можно просматривать на мобильных устройствах.</span><span class="sxs-lookup"><span data-stu-id="cfe3b-142">All SharePoint pages are [responsive](grid-and-responsive-design.md) to allow the content of the page to be viewed on mobile devices.</span></span> <span data-ttu-id="cfe3b-143">При разработке веб-части важно понимать, как новые страницы сайтов SharePoint отображаются на разных устройствах.</span><span class="sxs-lookup"><span data-stu-id="cfe3b-143">While designing a web part, it is important to understand how the new SharePoint site pages render across different devices.</span></span>

![Мобильное представление сайта](../images/design-authoring-mobile.png)

## <a name="see-also"></a><span data-ttu-id="cfe3b-145">См. также</span><span class="sxs-lookup"><span data-stu-id="cfe3b-145">See also</span></span>

- [<span data-ttu-id="cfe3b-146">Разработка прекрасных решений для SharePoint</span><span class="sxs-lookup"><span data-stu-id="cfe3b-146">Designing great SharePoint experiences</span></span>](design-guidance-overview.md)