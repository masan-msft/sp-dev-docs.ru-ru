---
title: "Ознакомление с визуальным конструктором для рабочих процессов в SharePoint Designer 2013"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: ff9b0314-eea1-47e4-87c7-53ed4de98c30
ms.openlocfilehash: aaf343fbfdcc984e6f63c09ea24b6b3c419e9e5d
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="getting-familiar-with-visual-designer-for-workflow-in-sharepoint-designer-2013"></a><span data-ttu-id="3a0d6-102">Ознакомление с визуальным конструктором для рабочих процессов в SharePoint Designer 2013</span><span class="sxs-lookup"><span data-stu-id="3a0d6-102">Getting familiar with Visual Designer for workflow in SharePoint Designer 2013</span></span>
<span data-ttu-id="3a0d6-103">Изучите основные возможности визуального конструктора в SharePoint Designer 2013.</span><span class="sxs-lookup"><span data-stu-id="3a0d6-103">Learn the basic features of the Visual Designer in SharePoint Designer 2013.</span></span>
## <a name="overview-of-the-visual-designer-in-sharepoint-designer-2013"></a><span data-ttu-id="3a0d6-104">Обзор визуального конструктора в SharePoint Designer 2013</span><span class="sxs-lookup"><span data-stu-id="3a0d6-104">Overview of the Visual Designer in SharePoint Designer 2013</span></span>
<span data-ttu-id="3a0d6-105"><a name="section1"> </a></span><span class="sxs-lookup"><span data-stu-id="3a0d6-105"><a name="section1"> </a></span></span>

<span data-ttu-id="3a0d6-p101">SharePoint Designer 2013 включает в себя новую поверхность разработки рабочего процесса  визуальный конструктор. С его помощью можно создавать рабочие процессы, перетаскивая фигур в область конструктора.</span><span class="sxs-lookup"><span data-stu-id="3a0d6-p101">SharePoint Designer 2013 includes a new workflow design surface called Visual Designer. You use Visual Designer to develop a workflow by dragging shapes onto the design surface.</span></span>
  
    
    

> <span data-ttu-id="3a0d6-108">**Важно!** Для работы с визуальным конструктором приложение Visio профессиональный 2013 должно быть установлено на том же компьютере, что и SharePoint Designer 2013.</span><span class="sxs-lookup"><span data-stu-id="3a0d6-108">**Important:** In order to work with the Visual Designer, you must have Visio Professional 2013 installed on the same computer as SharePoint Designer 2013.</span></span> <span data-ttu-id="3a0d6-109">Если у вас не установлено приложение Visio, возникнет ошибка, как на приведенном ниже рисунке.</span><span class="sxs-lookup"><span data-stu-id="3a0d6-109">If you do not have Visio installed you will receive an error, as shown in the figure.</span></span> 
  
    
    


<span data-ttu-id="3a0d6-110">**Рисунок. Для работы с визуальным конструктором необходимо приложение Visio 2013 профессиональный**</span><span class="sxs-lookup"><span data-stu-id="3a0d6-110">**Figure: Visio 2013 Professional is required to work with Visual Designer**</span></span>

  
    
    

  
    
    
![Visual Designer недоступен без Visio](../images/SPD15-VisualDesigner1.png)
  
    
    
<span data-ttu-id="3a0d6-p103">Область **Фигуры** в левой части содержит фигуры рабочего процесса, которые можно перетаскивать в область конструктора для создания рабочего процесса. Ниже приведены три категории фигур, доступных для создания рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="3a0d6-p103">The **Shapes** pane on the left contains workflow shapes that you can drag to the design surface in order to create the workflow. Following are the three categories of shapes available for building a workflow.</span></span>
  
    
    

- <span data-ttu-id="3a0d6-p104">**Действия:** определенные действия, которые могут выполняться рабочим процессом. В числе примеров: вызов веб-службы HTTP, добавление комментария и обновление списка.</span><span class="sxs-lookup"><span data-stu-id="3a0d6-p104">**Actions:** Specific actions that can be performed by the workflow. Some examples include calling an HTTP web service, adding a comment, and updating a list.</span></span>
    
  
- <span data-ttu-id="3a0d6-p105">**Компоненты:** общие компоненты, которые можно добавить для реализации структурированной среды для действий рабочего процесса. В числе примеров: контейнер стадии, цикл с условиями и фигура начала рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="3a0d6-p105">**Components:** General components that can be added to provide a structured environment for workflow actions. Some examples include a stage container, a loop with conditions, and a start workflow shape.</span></span>
    
  
- <span data-ttu-id="3a0d6-p106">**Условия:** фигуры условной логики, которые можно использовать для предоставления пути рабочего процесса на основе определенных критериев. В числе примеров: проверка, равно ли одно значение другому, проверка того, является ли пользователь допустимым пользователем SharePoint, и проверка того, был ли элемент создан в определенном диапазоне дат.</span><span class="sxs-lookup"><span data-stu-id="3a0d6-p106">**Conditions:** Conditional logic shapes that can be used to provide a workflow path based on specific criteria. Some examples include checking if one value equals another value, checking if a person is a valid SharePoint user, and checking if an item is created within a specific date range.</span></span>
    
  

    
> <span data-ttu-id="3a0d6-120">**Совет.** Полный список фигур, доступных в SharePoint Designer 2013, см. в статье [Фигуры в шаблонах рабочих процессов SharePoint Server в Visio](shapes-in-the-sharepoint-server-workflow-template-in-visio.md).</span><span class="sxs-lookup"><span data-stu-id="3a0d6-120">**Tip:** For a complete list of shapes available in SharePoint Designer 2013, see  [Shapes in the SharePoint Server workflow template in Visio](shapes-in-the-sharepoint-server-workflow-template-in-visio.md)</span></span>
  
    
    

<span data-ttu-id="3a0d6-121">На этом рисунке показан рабочий процесс в визуальном конструкторе.</span><span class="sxs-lookup"><span data-stu-id="3a0d6-121">The figure shows a workflow in Visual Designer.</span></span>
  
    
    

<span data-ttu-id="3a0d6-122">**Визуальный конструктор в SharePoint Designer 2013**</span><span class="sxs-lookup"><span data-stu-id="3a0d6-122">**Visual Designer in SharePoint Designer 2013**</span></span>

  
    
    

  
    
    
![Visual Designer в SharePoint Designer 2013](../images/SPD15-VisualDesigner2.png)
  
    
    

  
    
    

  
    
    

## <a name="using-the-visual-designer-in-sharepoint"></a><span data-ttu-id="3a0d6-124">Использование визуального конструктора в SharePoint</span><span class="sxs-lookup"><span data-stu-id="3a0d6-124">Using the Visual Designer in SharePoint</span></span>
<span data-ttu-id="3a0d6-125"><a name="section2"> </a></span><span class="sxs-lookup"><span data-stu-id="3a0d6-125"><a name="section2"> </a></span></span>

<span data-ttu-id="3a0d6-126">Для доступа к визуальному конструктору в SharePoint Designer 2013 используется раскрывающееся меню "Представления" на вкладке **Рабочий процесс**. Существует три различных представления, которые можно использовать для создания рабочих процессов:</span><span class="sxs-lookup"><span data-stu-id="3a0d6-126">The Visual Designer in SharePoint Designer 2013 is accessed through the Views drop-down menu of the **Workflow** tab. There are three different views that can be used for developing a workflow:</span></span>
  
    
    

- <span data-ttu-id="3a0d6-127">**Текстовый конструктор:** текстовая среда разработки рабочих процессов.</span><span class="sxs-lookup"><span data-stu-id="3a0d6-127">**Text-Based Designer:** A text-based workflow development environment.</span></span>
    
  
- <span data-ttu-id="3a0d6-p107">**Визуальный конструктор:** визуальная среда разработки рабочих процессов, где фигуры можно перетаскивать в область конструктора для создания рабочего процесса. (Требуется Visio профессиональный 2013.)</span><span class="sxs-lookup"><span data-stu-id="3a0d6-p107">**Visual Designer:** A visual workflow development environment where shapes can be dragged onto the design surface in order to develop the workflow. (Requires Visio Professional 2013)</span></span>
    
  
- <span data-ttu-id="3a0d6-p108">**Представление стадий:** высокоуровневое представление области визуального конструктора с отображением взаимодействия стадий рабочего процесса. Оно похоже на представление **визуального конструктора**, но без показа сведений на уровне фигур. (Требуется Visio профессиональный 2013.)</span><span class="sxs-lookup"><span data-stu-id="3a0d6-p108">**Stage View:** Provides a high-level view of the visual design surface by showing how stages of the workflow fit together. It is similar to the **Visual Designer** view but it does not show the shape-level detail. (Requires Visio Professional 2013)</span></span>
    
  
<span data-ttu-id="3a0d6-133">Вы можете переключаться между **представлениями** в разделе **Управление** ленты **рабочего процесса**, как показано на рисунке.</span><span class="sxs-lookup"><span data-stu-id="3a0d6-133">You can switch between **Views** in the **Manage** portion of the **Workflow** ribbon as shown in the figure.</span></span>
  
    
    

<span data-ttu-id="3a0d6-134">**Переключение между представлениями конструктора в SharePoint Designer 2013**</span><span class="sxs-lookup"><span data-stu-id="3a0d6-134">**Switching between design views in SharePoint Designer 2013**</span></span>

  
    
    

  
    
    
![Переключение между конструкторами.](../images/SPD15-VisualDesigner3.png)
  
    
    
<span data-ttu-id="3a0d6-p109">Рабочий процесс можно создать в текстовом конструкторе, визуальном конструкторе или используя оба средства. Например, если вы создаете рабочий процесс с помощью текстового конструктора, можно переключиться на представление визуального конструктора и продолжить создание того же рабочего процесса. Подобным образом можно также начать в визуальном конструкторе, а затем переключиться в текстовый конструктор и продолжить разработку. Перемещение между представлениями обеспечивает гибкость при создании рабочих процессов.</span><span class="sxs-lookup"><span data-stu-id="3a0d6-p109">A workflow can be developed in either the Text-Based Designer or the Visual Designer or both. For example, if you are developing a workflow by using the Text-Based Designer you can switch the view to the Visual Designer and continue to develop the same workflow. Likewise, you can also begin developing a workflow by using the Visual Designer and then switch the view to the Text-Based Designer and continue to develop the same workflow. Moving back and forth between views provides flexibility in workflow development.</span></span>
  
    
    

## <a name="see-also"></a><span data-ttu-id="3a0d6-140">См. также</span><span class="sxs-lookup"><span data-stu-id="3a0d6-140">See also</span></span>
<span data-ttu-id="3a0d6-141"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="3a0d6-141"><a name="bk_addresources"> </a></span></span>


-  [<span data-ttu-id="3a0d6-142">Рабочий процесс в SharePoint</span><span class="sxs-lookup"><span data-stu-id="3a0d6-142">Workflow in SharePoint </span></span>](http://technet.microsoft.com/ru-RU/sharepoint/jj556245.aspx)
    
  
-  [<span data-ttu-id="3a0d6-143">Новые возможности рабочих процессов SharePoint</span><span class="sxs-lookup"><span data-stu-id="3a0d6-143">What's new in workflow in SharePoint</span></span>](http://msdn.microsoft.com/library/6ab8a28b-fa2f-4530-8b55-a7f663bf15ea.aspx)
    
  
-  [<span data-ttu-id="3a0d6-144">Начало работы с рабочими процессами SharePoint</span><span class="sxs-lookup"><span data-stu-id="3a0d6-144">Getting started with SharePoint workflow</span></span>](http://msdn.microsoft.com/library/cc73be76-a329-449f-90ab-86822b1c2ee8.aspx)
    
  
-  [<span data-ttu-id="3a0d6-145">Разработка рабочих процессов в SharePoint Designer и Visio</span><span class="sxs-lookup"><span data-stu-id="3a0d6-145">Workflow development in SharePoint Designer and Visio</span></span>](workflow-development-in-sharepoint-designer-and-visio.md)
    
  
-  [<span data-ttu-id="3a0d6-146">Краткий справочник по действиям рабочего процесса (платформа рабочих процессов в SharePoint)</span><span class="sxs-lookup"><span data-stu-id="3a0d6-146">Workflow actions quick reference (SharePoint Workflow platform)</span></span>](workflow-actions-quick-reference-sharepoint-workflow-platform.md)
    
  

