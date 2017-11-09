---
title: "Демонстрация разработки веб-части SharePoint: создание области свойств со списком дел"
ms.date: 09/25/2017
ms.openlocfilehash: e2005e1f3b02fb0d6bc89fbf0fe8e701cf52985a
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="sharepoint-web-part-design-showcase-create-a-to-do-list-property-pane"></a><span data-ttu-id="9e8c3-102">Демонстрация разработки веб-части SharePoint: создание области свойств со списком дел</span><span class="sxs-lookup"><span data-stu-id="9e8c3-102">SharePoint web part design showcase: Create a To-Do list property pane</span></span>

<span data-ttu-id="9e8c3-103">В этой статье описывается создание веб-части со списком дел.</span><span class="sxs-lookup"><span data-stu-id="9e8c3-103">This article describes how to create a To-Do list web part.</span></span> <span data-ttu-id="9e8c3-104">В этом примере используется одиночная [область свойств](design-a-web-part.md). Это [реактивная](reactive-and-nonreactive-web-parts.md) веб-часть, основанная на адаптивной сетке [Office UI Fabric](https://dev.office.com/fabric#/).</span><span class="sxs-lookup"><span data-stu-id="9e8c3-104">This example uses the single pane [property pane type](design-a-web-part.md) and is [reactive](reactive-and-nonreactive-web-parts.md) and based on the [Office UI Fabric](https://dev.office.com/fabric#/) responsive grid.</span></span>


1. <span data-ttu-id="9e8c3-105">Добавьте описание, чтобы пользователи могли узнать больше о веб-части и ее свойствах.</span><span class="sxs-lookup"><span data-stu-id="9e8c3-105">Add a description to help users understand more about the web part and its properties.</span></span>

    <span data-ttu-id="9e8c3-106">В этом примере задано описание "Выберите источник своих дел и настройте отображение списка задач".</span><span class="sxs-lookup"><span data-stu-id="9e8c3-106">In this example, the description is "Select a source for your to-dos and customize the display for the list of tasks."</span></span>
    
    ![Добавление описания](../images/design-showcase-01.png)

2. <span data-ttu-id="9e8c3-108">Добавьте [компонент раскрывающегося списка](http://dev.office.com/fabric#/components/dropdown) Fabric, подключенный к списку.</span><span class="sxs-lookup"><span data-stu-id="9e8c3-108">Add a Fabric [drop-down component](http://dev.office.com/fabric#/components/dropdown) connected to a list.</span></span>

    ![Добавление раскрывающегося списка Fabric](../images/design-showcase-02.png)

3. <span data-ttu-id="9e8c3-110">Добавьте [компонент флажка](http://dev.office.com/fabric#/components/checkbox) Fabric для отображения выполненных задач.</span><span class="sxs-lookup"><span data-stu-id="9e8c3-110">Add a Fabric [checkbox component](http://dev.office.com/fabric#/components/checkbox) to display completed tasks.</span></span>

    ![Добавление флажка Fabric](../images/design-showcase-03.png)

4. <span data-ttu-id="9e8c3-112">Добавьте еще два флажка для управления параметрами отображения.</span><span class="sxs-lookup"><span data-stu-id="9e8c3-112">Add two more checkboxes to control display options.</span></span>

    ![Добавление еще двух флажков Fabric](../images/design-showcase-04.png)

5. <span data-ttu-id="9e8c3-114">Добавьте [ползунок](http://dev.office.com/fabric#/components/slider) Fabric для отображения максимального количества элементов.</span><span class="sxs-lookup"><span data-stu-id="9e8c3-114">Add a Fabric [slider](http://dev.office.com/fabric#/components/slider) for the maximum number of items to display.</span></span>

    ![Добавление ползунка Fabric](../images/design-showcase-05.png)

6. <span data-ttu-id="9e8c3-116">Затем автор страницы выбирает список или вручную добавляет задачи для предварительного заполнения списка дел в веб-части.</span><span class="sxs-lookup"><span data-stu-id="9e8c3-116">Next, the author of the page selects a list or manually adds tasks to prepopulate the To-Do list web part.</span></span>

    <span data-ttu-id="9e8c3-117">![Выбор списка в области](../images/design-showcase-06.png) ![Выбор списка в развернутой области](../images/design-showcase-07.png) ![Добавление задач в список вручную](../images/design-showcase-08.png)</span><span class="sxs-lookup"><span data-stu-id="9e8c3-117">![Select a list in pane](../images/design-showcase-06.png) ![Select a list in pane expanded](../images/design-showcase-07.png) ![Manual addition of tasks to list](../images/design-showcase-08.png)</span></span>

7. <span data-ttu-id="9e8c3-118">В веб-части отображается индикатор загрузки элементов на страницу.</span><span class="sxs-lookup"><span data-stu-id="9e8c3-118">The web part shows an indicator of items loading onto the page.</span></span>

    ![Индикатор элементов](../images/design-showcase-09.png)

8. <span data-ttu-id="9e8c3-120">Загружаются элементы из списка.</span><span class="sxs-lookup"><span data-stu-id="9e8c3-120">Items from the list load.</span></span>

    ![Загрузка элементов списка](../images/design-showcase-10.png)

    <span data-ttu-id="9e8c3-122">После загрузки новые задачи плавно появляются с использованием компонентов анимации из Office UI Fabric.</span><span class="sxs-lookup"><span data-stu-id="9e8c3-122">When the new tasks are loaded the fade into view using animation styles from Office UI Fabric Web part with fabric animations</span></span>

    ![Новые задачи загружены](../images/design-showcase-11.png)

9. <span data-ttu-id="9e8c3-124">Область свойств управляет пользовательским интерфейсом.</span><span class="sxs-lookup"><span data-stu-id="9e8c3-124">The property pane controls the UI.</span></span> <span data-ttu-id="9e8c3-125">Задачи с включенными сводками отображаются с помощью флажков отображения в области свойств.</span><span class="sxs-lookup"><span data-stu-id="9e8c3-125">Tasks with pivots enabled are displayed via the Display checkboxes in the property pane.</span></span> 

    ![Область свойств, управляющая элементами веб-части](../images/design-showcase-12.png)

## <a name="responsive-views"></a><span data-ttu-id="9e8c3-127">Адаптивные представления</span><span class="sxs-lookup"><span data-stu-id="9e8c3-127">Responsive views</span></span>

<span data-ttu-id="9e8c3-128">В приведенном ниже примере показано представление с 2 из 3 столбцов в веб-части.</span><span class="sxs-lookup"><span data-stu-id="9e8c3-128">The following example shows the 2/3 column view of the web part.</span></span>

![Представление столбцов, занимающее две трети области](../images/design-showcase-13.png)

<span data-ttu-id="9e8c3-130">В приведенном ниже примере показано представление с 1 из 3 столбцов в веб-части.</span><span class="sxs-lookup"><span data-stu-id="9e8c3-130">The following example shows the 1/3 column view of the web part.</span></span>


![Представление столбцов, занимающее одну треть области](../images/design-showcase-14.png)

<span data-ttu-id="9e8c3-132">В приведенном ниже примере показано мобильное (доступное только для чтения) представление веб-части.</span><span class="sxs-lookup"><span data-stu-id="9e8c3-132">The following example shows the mobile (read-only) view of the web part.</span></span>

![Мобильное представление веб-части со списком дел](../images/design-showcase-15.png)