---
title: "Демонстрация оформления веб-части SharePoint: создание области свойств со списком дел"
description: "Создайте реактивную веб-часть \"Список дел\" с одной областью."
ms.date: 01/23/2018
ms.openlocfilehash: a3df418a3143fb638210dfde4e5b39841b71444b
ms.sourcegitcommit: 0ad5aeee2c5efc47eb57e050581e4f411c4be643
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/29/2018
---
# <a name="sharepoint-web-part-design-showcase-create-a-to-do-list-property-pane"></a><span data-ttu-id="9d960-103">Демонстрация дизайна веб-части SharePoint: создание области свойств со списком дел</span><span class="sxs-lookup"><span data-stu-id="9d960-103">SharePoint web part design showcase: Create a To-Do list property pane</span></span>

<span data-ttu-id="9d960-104">В этой статье описано создание веб-части со списком дел.</span><span class="sxs-lookup"><span data-stu-id="9d960-104">This article describes how to create a To-Do list web part.</span></span> <span data-ttu-id="9d960-105">В этом примере используется [одиночная область свойств](design-a-web-part.md). Это [реактивная](reactive-and-nonreactive-web-parts.md) веб-часть, основанная на адаптивной сетке [Office UI Fabric](https://developer.microsoft.com/ru-RU/fabric).</span><span class="sxs-lookup"><span data-stu-id="9d960-105">This example uses the single pane [property pane type](design-a-web-part.md) and is [reactive](reactive-and-nonreactive-web-parts.md) and based on the [Office UI Fabric](https://developer.microsoft.com/ru-RU/fabric) responsive grid.</span></span>


## <a name="create-a-to-do-list-web-part"></a><span data-ttu-id="9d960-106">Создание веб-части "Список дел"</span><span class="sxs-lookup"><span data-stu-id="9d960-106">Create a To-Do list web part</span></span>

1. <span data-ttu-id="9d960-107">Добавьте описание, чтобы пользователи могли узнать больше о веб-части и ее свойствах.</span><span class="sxs-lookup"><span data-stu-id="9d960-107">Add a description to help users understand more about the web part and its properties.</span></span>

    <span data-ttu-id="9d960-108">В этом примере задано описание "Выберите источник своих дел и настройте отображение списка задач".</span><span class="sxs-lookup"><span data-stu-id="9d960-108">In this example, the description is "Select a source for your to-dos and customize the display for the list of tasks."</span></span>
    
    ![Добавление описания](../images/design-showcase-01.png)

    <br/>

2. <span data-ttu-id="9d960-110">Добавьте [компонент раскрывающегося списка](https://developer.microsoft.com/ru-RU/fabric#/components/dropdown) Fabric, подключенный к списку.</span><span class="sxs-lookup"><span data-stu-id="9d960-110">Add a Fabric [drop-down component](https://developer.microsoft.com/ru-RU/fabric#/components/dropdown) connected to a list.</span></span>

    ![Добавление раскрывающегося списка Fabric](../images/design-showcase-02.png)

    <br/>

3. <span data-ttu-id="9d960-112">Добавьте [компонент флажка](https://developer.microsoft.com/ru-RU/fabric#/components/checkbox) Fabric для отображения выполненных задач.</span><span class="sxs-lookup"><span data-stu-id="9d960-112">Add a Fabric [checkbox component](https://developer.microsoft.com/ru-RU/fabric#/components/checkbox) to display completed tasks.</span></span>

    ![Добавление флажка Fabric](../images/design-showcase-03.png)

    <br/>

4. <span data-ttu-id="9d960-114">Добавьте еще два флажка для управления параметрами отображения.</span><span class="sxs-lookup"><span data-stu-id="9d960-114">Add two more checkboxes to control display options.</span></span>

    ![Добавление еще двух флажков Fabric](../images/design-showcase-04.png)

    <br/>

5. <span data-ttu-id="9d960-116">Добавьте [ползунок](https://developer.microsoft.com/ru-RU/fabric#/components/slider) Fabric для отображения максимального количества элементов.</span><span class="sxs-lookup"><span data-stu-id="9d960-116">Add a Fabric [slider](https://developer.microsoft.com/ru-RU/fabric#/components/slider) for the maximum number of items to display.</span></span>

    ![Добавление ползунка Fabric](../images/design-showcase-05.png)

    <br/>

6. <span data-ttu-id="9d960-118">После этого автор страницы выбирает список или вручную добавляет задачи для предварительного заполнения веб-части "Список дел".</span><span class="sxs-lookup"><span data-stu-id="9d960-118">Next, the author of the page selects a list or manually adds tasks to prepopulate the To-Do list web part.</span></span>

    ![Область "Выберите список"](../images/design-showcase-06.png)

    <br/>

    ![Развернутая область "Выберите список"](../images/design-showcase-07.png)

    <br/>

    ![Добавление задач в список вручную](../images/design-showcase-08.png)

    <br/>

7. <span data-ttu-id="9d960-122">Веб-часть показывает индикатор загрузки элементов на страницу.</span><span class="sxs-lookup"><span data-stu-id="9d960-122">The web part shows an indicator of items loading onto the page.</span></span>

    ![Индикатор элементов](../images/design-showcase-09.png)

    <br/>

8. <span data-ttu-id="9d960-124">Загружаются элементы из списка.</span><span class="sxs-lookup"><span data-stu-id="9d960-124">Items from the list load.</span></span>

    ![Загрузка элементов списка](../images/design-showcase-10.png)

    <br/>

    <span data-ttu-id="9d960-126">После загрузки новые задачи плавно появляются на экране. Для этого используются компоненты анимации из Office UI Fabric.</span><span class="sxs-lookup"><span data-stu-id="9d960-126">When the new tasks are loaded, they fade into view using animation components from Office UI Fabric.</span></span>

    ![Новые задачи загружены](../images/design-showcase-11.png)

    <br/>

9. <span data-ttu-id="9d960-128">Область свойств управляет пользовательским интерфейсом.</span><span class="sxs-lookup"><span data-stu-id="9d960-128">The property pane controls the UI.</span></span> <span data-ttu-id="9d960-129">Задачи с включенными сводками отображаются с помощью флажков отображения в области свойств.</span><span class="sxs-lookup"><span data-stu-id="9d960-129">Tasks with pivots enabled are displayed via the Display checkboxes in the property pane.</span></span> 

    ![Область свойств, контролирующая элементы веб-части](../images/design-showcase-12.png)

    <br/>

## <a name="responsive-views"></a><span data-ttu-id="9d960-131">Адаптивные представления</span><span class="sxs-lookup"><span data-stu-id="9d960-131">Responsive views</span></span>

<span data-ttu-id="9d960-132">В приведенном ниже примере показано представление с 2 из 3 столбцов в веб-части.</span><span class="sxs-lookup"><span data-stu-id="9d960-132">The following example shows the 2/3 column view of the web part.</span></span>

![Представление столбцов, занимающее две трети области](../images/design-showcase-13.png)

<br/>

<span data-ttu-id="9d960-134">В приведенном ниже примере показано представление с 1 из 3 столбцов в веб-части.</span><span class="sxs-lookup"><span data-stu-id="9d960-134">The following example shows the 1/3 column view of the web part.</span></span>

![Представление столбцов, занимающее одну треть области](../images/design-showcase-14.png)

<br/>

<span data-ttu-id="9d960-136">В приведенном ниже примере показано мобильное (доступное только для чтения) представление веб-части.</span><span class="sxs-lookup"><span data-stu-id="9d960-136">The following example shows the mobile (read-only) view of the web part.</span></span>

![Мобильное представление веб-части со списком дел](../images/design-showcase-15.png)

<br/>

## <a name="see-also"></a><span data-ttu-id="9d960-138">См. также</span><span class="sxs-lookup"><span data-stu-id="9d960-138">See also</span></span>

- [<span data-ttu-id="9d960-139">Разработка прекрасных решений для SharePoint</span><span class="sxs-lookup"><span data-stu-id="9d960-139">Designing great SharePoint experiences</span></span>](design-guidance-overview.md)