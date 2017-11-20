---
title: "Разработка рабочих процессов в SharePoint Designer и Visio"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 496780d5-47d6-4a43-bf14-70aefb8d820c
ms.openlocfilehash: 7a6e5e4d3cff0289930a34da749fd8fa7ce10585
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="workflow-development-in-sharepoint-designer-and-visio"></a><span data-ttu-id="ef25a-102">Разработка рабочих процессов в SharePoint Designer и Visio</span><span class="sxs-lookup"><span data-stu-id="ef25a-102">Workflow development in SharePoint Designer and Visio</span></span>
<span data-ttu-id="ef25a-103">Узнайте, как использовать Visio 2013 и SharePoint Designer 2013, чтобы создавать и публиковать рабочие процессы для сайта SharePoint без какого-либо кода.</span><span class="sxs-lookup"><span data-stu-id="ef25a-103">Learn to use Visio 2013 and SharePoint Designer 2013 to create and publish workflows to a SharePoint site without needing any code.</span></span>
## <a name="introduction"></a><span data-ttu-id="ef25a-104">Введение</span><span class="sxs-lookup"><span data-stu-id="ef25a-104">Introduction</span></span>
<span data-ttu-id="ef25a-105"><a name="VSSPD_Intro"> </a></span><span class="sxs-lookup"><span data-stu-id="ef25a-105"></span></span>

<span data-ttu-id="ef25a-p101">Visio 2013 и SharePoint Designer 2013 упрощают совместную работу и создание рабочих процессов для бизнес-аналитиков, консультантов и ИТ-специалистов. И Visio профессиональный 2013, и визуальный конструктор в SharePoint Designer 2013 используют расширенное представление рабочих процессов в формате, понятном программистов и далеким от программирования пользователям.</span><span class="sxs-lookup"><span data-stu-id="ef25a-p101">Visio 2013 and SharePoint Designer 2013 make it easy for business analysts, process consultants, and IT professionals to collaborate and build workflows. Both Visio Professional 2013 and the Visual Designer in SharePoint Designer 2013 provide a rich representation of workflows in a format that is understandable to programmers and non-programmers alike.</span></span>
  
    
    

> <span data-ttu-id="ef25a-108">**Примечание.** Инструкции по установке и настройке SharePoint и сервера Workflow Manager см. в статье [Настройка рабочих процессов в SharePoint](http://technet.microsoft.com/ru-RU/library/jj658586.aspx).</span><span class="sxs-lookup"><span data-stu-id="ef25a-108">**Note** For guidance on setting up and configuring SharePoint Server 2013 and the Workflow Manager server, see  [Configure workflow in SharePoint Server 2013](http://technet.microsoft.com/ru-RU/library/jj658586.aspx).</span></span> 
  
    
    

<span data-ttu-id="ef25a-p102">С помощью Visio 2013 можно визуально создать рабочий процесс SharePoint, экспортировать его в SharePoint Designer 2013, а затем опубликовать на сайте SharePoint. После создания рабочего процесса в Visio 2013 его необходимо экспортировать в SharePoint Designer 2013. Затем владелец сайта SharePoint или ИТ-специалист добавляет параметры рабочего процесса, используя текстовый редактор и новый визуальный конструктор рабочих процессов, который представляет собой элемент управления ActiveX Visio 2013, размещенный в SharePoint Designer 2013. После завершения рабочего процесса он может быть опубликованы на сайте SharePoint.</span><span class="sxs-lookup"><span data-stu-id="ef25a-p102">By using Visio 2013, you can visually create a SharePoint workflow, export the workflow to SharePoint Designer 2013, and then publish that workflow to a SharePoint site. After a workflow has been created in Visio 2013, it must be exported to SharePoint Designer 2013. Then, a SharePoint site owner or IT professional adds parameters to the workflow by using either the workflow text editor or the new Visual Workflow Designer, which is a Visio 2013 ActiveX control that is hosted in SharePoint Designer 2013. After the workflow has been completed, it can be published to the SharePoint site.</span></span>
  
    
    
<span data-ttu-id="ef25a-p103">Эти возможности идеально подходят для бизнес-аналитиков и консультантов по процессам, которые уже знакомы с блок-схемами в Visio, поскольку они позволяют создавать рабочие процессы, представляющие бизнес-логику. Пользователь, проектирующий рабочий процесс, может сосредоточиться исключительно на бизнес-аналитике, при этом не надо быть экспертом по декларативным рабочим процессам.</span><span class="sxs-lookup"><span data-stu-id="ef25a-p103">This is ideal for business analysts and process consultants who are already familiar with flowcharts in Visio, because it allows them to design a workflow that represents business logic. The person who designs the workflow can focus solely on the business intelligence (BI) needs of the workflow without needing to be an expert in declarative workflows.</span></span>
  
    
    

## <a name="about-creating-sharepoint-workflows-in-visio-2013-and-sharepoint-designer-2013"></a><span data-ttu-id="ef25a-115">Сведения о создании рабочих процессов SharePoint в Visio 2013 и SharePoint Designer 2013</span><span class="sxs-lookup"><span data-stu-id="ef25a-115">About creating SharePoint Workflows in Visio 2013 and SharePoint Designer 2013</span></span>
<span data-ttu-id="ef25a-116"><a name="VSSPD_About"> </a></span><span class="sxs-lookup"><span data-stu-id="ef25a-116"></span></span>

<span data-ttu-id="ef25a-p104">В Visio 2013 представлен шаблон рабочего процесса SharePoint, который можно использовать для создания рабочих процессов SharePoint. Шаблон рабочего процесса SharePoint связан с тремя наборами элементов: действиями рабочего процесса SharePoint, условиями рабочего процесса SharePoint и фигурами завершения рабочего процесса SharePoint. Фигуры в этих наборах элементов соответствуют определенным действиям и условиям, которые можно использовать в рабочем процессе SharePoint. Чтобы создать рабочий процесс, необходимо просто перетащить фигуры на полотно в Visio 2013 для моделирования бизнес-логики рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="ef25a-p104">Visio 2013 includes a SharePoint Workflow template that can be used to build SharePoint workflows. The SharePoint Workflow template is associated with three stencils: SharePoint Workflow Actions, SharePoint Workflow Conditions, and SharePoint Workflow Terminators. The shapes in these stencils correspond to specific actions and conditions that can be used within a SharePoint workflow. To build a workflow, you need only to drag shapes onto the drawing canvas in Visio 2013 to model the business logic behind the workflow.</span></span>
  
    
    

### <a name="stages-loops-and-steps"></a><span data-ttu-id="ef25a-121">Стадии, циклы и этапы</span><span class="sxs-lookup"><span data-stu-id="ef25a-121">Stages, loops, and steps</span></span>

<span data-ttu-id="ef25a-p105">Рабочие процессы в SharePoint Designer 2013 теперь используют понятия стадий, циклов иэтапов. Создатели рабочих процессов могут сгруппировать несколько отдельных действий и условий в единый блок, чтобы более четко определить процесс. Например, может существовать стадия или этап утверждения или запроса. Эта стадия или этап будут содержать все действия, необходимые для процесса. Сама стадия или этап могут быть узлом более крупного рабочего процесса, при этом пользователи будут видеть состояние стадии или этапа как единого целого, а не набора отдельных действий.</span><span class="sxs-lookup"><span data-stu-id="ef25a-p105">Workflows in SharePoint Designer 2013 now include the notions of stages, loops, and steps. Workflow authors can group a number of individual actions and conditions as a single unit to more clearly define the process. For example, there could be an Approval or Request Feedback stage or step. Within that stage or step would be all of the actions that are necessary for that process. The stage or step itself might be one node of a longer workflow and would allow a viewer to see the status of that stage as a whole, rather than a set of individual actions.</span></span>
  
    
    
<span data-ttu-id="ef25a-127">Шаблон рабочего процесса SharePoint, который входит в Visio 2013, также использует стадии, циклы и этапы как логические блоки для создания рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="ef25a-127">The SharePoint Workflow template that is included in Visio 2013 also uses stages, loops, and steps as logical building blocks for creating a workflow.</span></span> 
  
    
    

> <span data-ttu-id="ef25a-128">**Внимание!** Из-за существенных различий шаблонов рабочего процесса Microsoft SharePoint 2010 и SharePoint вы не можете использовать фигуры из одного шаблона в схеме, созданной в другом шаблоне.</span><span class="sxs-lookup"><span data-stu-id="ef25a-128">**Important** Because of the underlying differences between the Microsoft SharePoint 2010 Workflow template and the SharePoint Workflow template, you cannot use shapes from one template within a diagram created by the other. Only shapes from the SharePoint Workflow Actions, SharePoint Workflow Conditions, and SharePoint Workflow Terminators stencils can be used to build a SharePoint workflow.</span></span> <span data-ttu-id="ef25a-129">Только фигуры из наборов элементов "Действия рабочего процесса SharePoint", "Условия рабочего процесса SharePoint" и "Фигуры завершения рабочего процесса в SharePoint" можно использовать для создания рабочего процесса SharePoint.</span><span class="sxs-lookup"><span data-stu-id="ef25a-129">Important Because of the underlying differences between the Microsoft SharePoint 2010 Workflow template and the SharePoint Workflow template, you cannot use shapes from one template within a diagram created by the other. Only shapes from the SharePoint Workflow Actions, SharePoint Workflow Conditions, and SharePoint Workflow Terminators stencils can be used to build a SharePoint workflow.</span></span> 
  
    
    


### <a name="stage-shapes"></a><span data-ttu-id="ef25a-130">Фигуры стадий</span><span class="sxs-lookup"><span data-stu-id="ef25a-130">Stage shapes</span></span>

<span data-ttu-id="ef25a-p107">Стадия может содержать любое число фигур, а также ветвления. Однако в стадии может быть только один вход в стадию (и этап) и один выход. Все действия в рабочем процессе должны входить в рабочую область. Фигуры стадии отображаются с помощью фигур контейнера. Для получения фигуры стадии необходимо добавить фигуру входа и выхода к краям контейнера, чтобы определить вход и выход из стадии. Visio 2013 и визуальный конструктор в SharePoint Designer 2013 добавляют фигуры входа и выхода автоматически после перетаскивания контейнера.</span><span class="sxs-lookup"><span data-stu-id="ef25a-p107">A stage can contain any number of shapes and may include branching. However, there can be only one path into a stage (and a step) and one path out. All actions in the workflow must be contained by a stage. Stage shapes are visualized by using container shapes. A Stage shape requires that an Enter and an Exit shape be added to the edges of the container to define the paths in and out of the stage. Visio 2013 and the Visual Designer in SharePoint Designer 2013 add the Enter and Exit shapes for you when you first drop the container.</span></span>
  
    
    
<span data-ttu-id="ef25a-136">К стадиям также применяются следующие правила:</span><span class="sxs-lookup"><span data-stu-id="ef25a-136">Stages also have the following rules:</span></span>
  
    
    

- <span data-ttu-id="ef25a-p108">По крайней мере одна стадия должна входить в каждую схему. Стадия с фигурами входа и выхода составляют шаблон рабочего процесса SharePoint по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="ef25a-p108">All diagrams must have at least one stage. A stage, complete with Enter, Exit, and Start shapes are present as part of the default SharePoint Workflow template.</span></span>
    
  
- <span data-ttu-id="ef25a-139">Если добавить новую стадию на полотно, Visio 2013 добавит соединители начала и окончания после перетаскивания стадии.</span><span class="sxs-lookup"><span data-stu-id="ef25a-139">When you add a new stage to the drawing canvas, Visio 2013 will add Start and End connectors when the stage is dropped.</span></span>
    
  
- <span data-ttu-id="ef25a-140">У стадий могут быть только соединители, выходящие из фигур входа и выхода.</span><span class="sxs-lookup"><span data-stu-id="ef25a-140">Stages cannot have any connectors coming in or going out other than through the Enter and Exit shapes.</span></span>
    
  
- <span data-ttu-id="ef25a-p109">Контейнеры стадий не могут быть вложенными. Если вам требуется вложить подпроцесс в стадию, используйте этап.</span><span class="sxs-lookup"><span data-stu-id="ef25a-p109">Stage containers cannot be nested. If you want to nest another sub-process within a stage, use a step.</span></span>
    
  
- <span data-ttu-id="ef25a-143">В стадии можно разместить фигуры остановки рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="ef25a-143">Stop Workflow shapes may exist within a stage.</span></span>
    
  
- <span data-ttu-id="ef25a-p110">Явная фигура начала должна быть расположена вне стадии для всей схеме. Явная фигура завершения вне стадии необязательна.</span><span class="sxs-lookup"><span data-stu-id="ef25a-p110">An explicit Start shape is required outside of the stage for the entire diagram. An explicit Terminate shape outside of the stage is not required.</span></span>
    
  
- <span data-ttu-id="ef25a-p111">На верхнем уровне рабочий процесс может содержать только стадии, условные фигуры, а также оконечные фигуры начала и завершения. Все другие фигуры должны входить в стадию.</span><span class="sxs-lookup"><span data-stu-id="ef25a-p111">At the top level, the workflow can contain only stages, conditional shapes, and Start and Terminate terminators. All other shapes must be contained within a stage.</span></span>
    
  

### <a name="loop-shapes"></a><span data-ttu-id="ef25a-148">Фигуры циклов</span><span class="sxs-lookup"><span data-stu-id="ef25a-148">Loop shapes</span></span>

<span data-ttu-id="ef25a-149">Циклы  это ряд соединенных фигур, которые будут выполняться как цикл, возвращаясь из последней фигуры в первую, пока условие выполняется.</span><span class="sxs-lookup"><span data-stu-id="ef25a-149">Loops are a series of connected shapes that will execute as a loop, returning from the last shape in the series to the first, until a condition is satisfied.</span></span> 
  
    
    
<span data-ttu-id="ef25a-p112">Как и стадии, циклы представлены в виде фигуры контейнера, которая содержит фигуры входа и выхода (они добавляются при перетаскивании фигуры на полотно). Для фигуры цикла также требуется добавить фигуры входа и выхода к краям контейнера для определения входа и выходы из цикла.</span><span class="sxs-lookup"><span data-stu-id="ef25a-p112">Like stages, loops are represented by a container shape that includes an Enter and Exit shape (added when the shape is dropped on the drawing canvas). A Loop shape also requires that an Enter and Exit shape be added to the edges of the container to define the paths in and out of the loop.</span></span>
  
    
    
<span data-ttu-id="ef25a-152">Visio 2013 и SharePoint Designer 2013 поддерживают два типа циклов: цикл  *n*  раз и цикл, пока *значение1*  равно *значение2*  .</span><span class="sxs-lookup"><span data-stu-id="ef25a-152">Visio 2013 and SharePoint Designer 2013 support two types of loops: loop  *n*  times and loop until *value1*  equals *value2*  .</span></span>
  
    
    
<span data-ttu-id="ef25a-153">Циклы также должны соответствовать следующим требованиям:</span><span class="sxs-lookup"><span data-stu-id="ef25a-153">Loops must also conform to the following rules:</span></span>
  
    
    

- <span data-ttu-id="ef25a-154">циклы должны находиться в стадии, стадии не могут входить в цикл;</span><span class="sxs-lookup"><span data-stu-id="ef25a-154">Loops must be within a stage, and stages cannot be within a loop.</span></span>
    
  
- <span data-ttu-id="ef25a-155">этапы могут входить в цикл;</span><span class="sxs-lookup"><span data-stu-id="ef25a-155">Steps may be within a loop.</span></span>
    
  
- <span data-ttu-id="ef25a-156">у цикла может быть только одна точка входа и одна точка выхода.</span><span class="sxs-lookup"><span data-stu-id="ef25a-156">Loops may have only one entry and one exit point.</span></span>
    
  

### <a name="step-shapes"></a><span data-ttu-id="ef25a-157">Фигуры этапов</span><span class="sxs-lookup"><span data-stu-id="ef25a-157">Step shapes</span></span>

<span data-ttu-id="ef25a-p113">Этапы представляют ряд сгруппированных последовательных действий. Этапы содержаться в стадии. У фигуры стадии также должны быть фигуры входа и выхода, определяющие пути входа и выхода. Обе фигуры добавляются по умолчанию при перетаскивании фигуры на полотно.</span><span class="sxs-lookup"><span data-stu-id="ef25a-p113">Steps represent a grouped series of sequential actions. Steps must be contained by a stage. A step shape must also have an Enter and Exit shape to define the paths in and out of the shape. Both shapes are added by default when the shape is dropped onto the canvas.</span></span>
  
    
    

## <a name="creating-a-workflow-in-visio-2013"></a><span data-ttu-id="ef25a-162">Создание рабочего процесса в Visio 2013</span><span class="sxs-lookup"><span data-stu-id="ef25a-162">Creating a workflow in Visio 2013</span></span>
<span data-ttu-id="ef25a-163"><a name="VSSPD_Creating"> </a></span><span class="sxs-lookup"><span data-stu-id="ef25a-163"></span></span>

<span data-ttu-id="ef25a-p114">Все образцы фигур в наборе элементов SharePoint соответствуют действиям, условиям и другим логическим конструкциям в рабочем процессе SharePoint. Для создания рабочего процесса можно перетащить фигуры на полотно так же, как и для любой другой блок-схемы в Visio. После завершения создания рабочего процесса в Visio 2013 сохраните свою работу, чтобы его можно было открыть в SharePoint Designer 2013.</span><span class="sxs-lookup"><span data-stu-id="ef25a-p114">All of the master shapes in the SharePoint Workflow stencils correspond to actions, conditions, and other logical constructs within a SharePoint workflow. To build a workflow, you can drag shapes onto the drawing canvas, just like any other flowchart in Visio. After you have finished building the workflow in Visio 2013, save the workflow before SharePoint Designer 2013 can open it.</span></span>
  
    
    
<span data-ttu-id="ef25a-167">Чтобы открыть шаблон рабочего процесса SharePoint в Visio 2013, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="ef25a-167">To open the SharePoint Workflow template in Visio 2013, do the following:</span></span>
  
    
    

### <a name="to-open-the-sharepoint-workflow-template-in-visio-2013"></a><span data-ttu-id="ef25a-168">Открытие шаблона рабочего процесса SharePoint в Visio 2013</span><span class="sxs-lookup"><span data-stu-id="ef25a-168">To open the SharePoint Workflow template in Visio 2013</span></span>


1. <span data-ttu-id="ef25a-169">Откройте Visio 2013.</span><span class="sxs-lookup"><span data-stu-id="ef25a-169">Open Visio 2013.</span></span>
    
  
2. <span data-ttu-id="ef25a-170">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="ef25a-170">Choose **New**.</span></span>
    
  
3. <span data-ttu-id="ef25a-171">В разделе **Категории шаблонов** выберите **Блок-схема**.</span><span class="sxs-lookup"><span data-stu-id="ef25a-171">Under **Template Categories**, choose **Flowchart**.</span></span>
    
  
4. <span data-ttu-id="ef25a-172">В окне **Выберите шаблон** щелкните **Рабочий процесс SharePoint** и выберите **Создать**.</span><span class="sxs-lookup"><span data-stu-id="ef25a-172">Under **Choose a Template**, choose **SharePoint Workflow** and then choose **Create**.</span></span>
    
    <span data-ttu-id="ef25a-p115">Откроется шаблон, а на полотно будут добавлены фигуры начала и стадии. Фигура стадии содержит фигуры входа и выхода, объединенные одним соединителем.</span><span class="sxs-lookup"><span data-stu-id="ef25a-p115">The template opens and the drawing canvas is prepopulated with Start, and Stage shapes. The Stage shape contains an Enter and an Exit shape, joined by a single connector.</span></span>
    
  
<span data-ttu-id="ef25a-p116">Перетащите действия, условия и другие фигуры на полотно открытого шаблона рабочего процесса SharePoint, чтобы создать рабочий процесс. Дополнительные сведения об отдельных фигурах и их значении см. в статье  [Фигуры в шаблоне рабочего процесса SharePoint Server в Visio](shapes-in-the-sharepoint-server-workflow-template-in-visio.md).</span><span class="sxs-lookup"><span data-stu-id="ef25a-p116">With the SharePoint Workflow template open, drag actions, conditions, and other shapes onto the drawing canvas to design a workflow. For more information about individual shapes and what they mean, see the article  [Shapes in the SharePoint Server workflow template in Visio](shapes-in-the-sharepoint-server-workflow-template-in-visio.md).</span></span>
  
    
    

> <span data-ttu-id="ef25a-177">**Совет.** При создании рабочего процесса учитывайте указанные ниже дополнительные факторы.</span><span class="sxs-lookup"><span data-stu-id="ef25a-177">When designing a workflow, keep the following additional considerations in mind:</span></span>
>  - <span data-ttu-id="ef25a-178">Чтобы быстро создать рабочий процесс, перетащите фигуры действий и условий на внутренний соединитель, который есть в новых фигурах стадии.</span><span class="sxs-lookup"><span data-stu-id="ef25a-178">To quickly build a workflow, drop action and condition shapes onto the internal connector that is contained by new stage shapes. vis15short automatically splits the connector into additional connectors, keeping the workflow connected from the Enter shape to the Exit shape.</span></span> <span data-ttu-id="ef25a-179">Visio 2013 автоматически делит соединитель на дополнительные соединители, сохраняя рабочий процесс соединенным с фигурами входа и выхода.</span><span class="sxs-lookup"><span data-stu-id="ef25a-179">Visio 2013 automatically splits the connector into additional connectors, keeping the workflow connected from the Enter shape to the Exit shape.</span></span>
>  - <span data-ttu-id="ef25a-180">Не используйте фигуры из наборов элементов, отличных от "Действия рабочего процесса SharePoint", "Условия рабочего процесса SharePoint" и "Фигуры завершения рабочего процесса в SharePoint".</span><span class="sxs-lookup"><span data-stu-id="ef25a-180">Do not use any shapes from a stencil other than the SharePoint Workflow Actions, SharePoint Workflow Conditions, and SharePoint Workflow Terminators stencils.</span></span> <span data-ttu-id="ef25a-181">Чтобы добавлять соединения между фигурами, используйте только средство создания соединителей, доступное в шаблоне рабочего процесса SharePoint.</span><span class="sxs-lookup"><span data-stu-id="ef25a-181">Use only the Connector tool provided by the SharePoint Workflow template to add connections between shapes.</span></span> <span data-ttu-id="ef25a-182">Все другие фигуры соединителей недопустимы для рабочего процесса SharePoint.</span><span class="sxs-lookup"><span data-stu-id="ef25a-182">All other connector shapes are not valid within a SharePoint workflow.</span></span>
>  - <span data-ttu-id="ef25a-p119">Фигуры действий, циклы и стадии должны всегда входить в фигуру стадии. Некоторые условные фигуры могут находиться вне стадии.</span><span class="sxs-lookup"><span data-stu-id="ef25a-p119">Action shapes, steps, and loops must always be contained within a Stage shape. Some conditional shapes can be outside of a stage.</span></span>
>  - <span data-ttu-id="ef25a-p120">У фигуры стадии должна быть только одна фигура входа и одна фигура выхода. Подпроцесс рабочего процесса, который содержится в стадии, должен начинаться с фигуры входа и заканчиваться фигурой выхода.</span><span class="sxs-lookup"><span data-stu-id="ef25a-p120">A Stage shape must have exactly one Enter shape and one Exit shape. The workflow sub-process that is contained within the stage must start with the Enter shape and end with the Exit shape.</span></span>
>  - <span data-ttu-id="ef25a-187">Из фигуры условия должны выходить два соединителя. Один из них должен быть помечен как "Да", другой — как "Нет".</span><span class="sxs-lookup"><span data-stu-id="ef25a-187">A condition shape must have two connectors leaving the shape, one labeled “Yes” and the other labeled “No.” You can right-click a connector to choose Yes or No.</span></span> <span data-ttu-id="ef25a-188">Щелкните соединитель правой кнопкой, чтобы выбрать **Да** или **Нет**.</span><span class="sxs-lookup"><span data-stu-id="ef25a-188">You can right-click a connector to choose **Yes** or **No**.</span></span> 
>  - <span data-ttu-id="ef25a-p122">В рабочем процессе должна быть только одна фигура начала, которая располагается вне стадии.</span><span class="sxs-lookup"><span data-stu-id="ef25a-p122">A workflow must have only one Start shape. The Start shape must be outside of a stage.</span></span>
>  - <span data-ttu-id="ef25a-191">Вы можете добавлять текст к фигурам в рабочем процессе, но он не влияет на рабочий процесс.</span><span class="sxs-lookup"><span data-stu-id="ef25a-191">You add text to shapes in the workflow, but the shape text will not affect the workflow.</span></span>
  
    
    


  
    
    
<span data-ttu-id="ef25a-p123">Проверка рабочего процесса в Visio 2013 аналогична проверке других соединенных схем: Visio проверяет схему на соответствие набору правил и возвращает список ошибок, найденных в схеме. Сведения об устранении обнаруженных проблем см. в статье  [Диагностика ошибок проверки рабочих процессов SharePoint Server в Visio](troubleshooting-sharepoint-server-workflow-validation-errors-in-visio.md).</span><span class="sxs-lookup"><span data-stu-id="ef25a-p123">Validating the workflow in Visio 2013 is like validating any other connected diagram: Visio checks the diagram against a set of rules and returns a list of errors that it found in the diagram. See the article  [Troubleshooting SharePoint Server workflow validation errors in Visio](troubleshooting-sharepoint-server-workflow-validation-errors-in-visio.md) to learn how to resolve validation issues.</span></span>
  
    
    

### <a name="to-validate-a-sharepoint-workflow-in-visio-2013"></a><span data-ttu-id="ef25a-194">Проверка рабочего процесса SharePoint в Visio 2013</span><span class="sxs-lookup"><span data-stu-id="ef25a-194">To validate a SharePoint workflow in Visio 2013</span></span>


1. <span data-ttu-id="ef25a-195">На вкладке **Процесс** в группе **Проверка схемы** нажмите кнопку **Проверить схему**.</span><span class="sxs-lookup"><span data-stu-id="ef25a-195">On the **Process** tab, in the **Diagram Validation** group, choose **Check Diagram**.</span></span>
    
  
2. <span data-ttu-id="ef25a-p124">Если в рабочем процессе найдены ошибки, под схемой откроется область **Проблемы**. Выберите каждый элемент в списке, чтобы выделить фигуру на схеме, вызвавшую ошибку.</span><span class="sxs-lookup"><span data-stu-id="ef25a-p124">If any errors are found in the workflow, the **Issues** pane opens below the diagram. Choose each item in the list to select the shape in the diagram that caused the error.</span></span>
    
  
3. <span data-ttu-id="ef25a-p125">Устраните все ошибки, указанные в списке **Проблемы**. После этого нажмите кнопку **Проверить схему** еще раз. Дополнительные сведения об устранении проблем при проверке в Visio 2013 см. в статье [Диагностика ошибок проверки рабочих процессов SharePoint Server в Visio](troubleshooting-sharepoint-server-workflow-validation-errors-in-visio.md).</span><span class="sxs-lookup"><span data-stu-id="ef25a-p125">Resolve each validation error listed in the **Issues** list. Once all of the errors have been addressed, choose **Check Diagram** again. For more information about how to resolve validation issues in Visio 2013, see the article [Troubleshooting SharePoint Server workflow validation errors in Visio](troubleshooting-sharepoint-server-workflow-validation-errors-in-visio.md).</span></span>
    
  
4. <span data-ttu-id="ef25a-201">Если ошибки в рабочем процессе не найдены, Visio отображает сообщение об успешном завершении проверки схемы.</span><span class="sxs-lookup"><span data-stu-id="ef25a-201">If no errors are found in the workflow, Visio displays a message stating that the diagram validation is complete and that no issues were found.</span></span>
    
  
<span data-ttu-id="ef25a-p126">После проверки процесса в Visio 2013 вы можете сохранить файл и импортировать его в SharePoint Designer 2013. В отличие от шаблона рабочего процесса Microsoft SharePoint 2010 можно сохранить копию схемы рабочего процесса SharePoint в формате Visio 2013 по умолчанию (VSDX), а SharePoint Designer 2013 сможет открыть файл.</span><span class="sxs-lookup"><span data-stu-id="ef25a-p126">After the workflow has been successfully validated in Visio 2013, you can save the file and import it into SharePoint Designer 2013. Unlike the Microsoft SharePoint 2010 Workflow template, you can save a copy of the SharePoint Workflow diagram as the default Visio 2013 file format (.vsdx) and SharePoint Designer 2013 can open the file.</span></span> 
  
    
    
<span data-ttu-id="ef25a-204">Используйте следующую процедуру, чтобы сохранить рабочий процесс SharePoint в Visio 2013 как VSDX-файл Visio 2013, который можно открыть в SharePoint Designer 2013:</span><span class="sxs-lookup"><span data-stu-id="ef25a-204">Use the following procedure to save a SharePoint workflow in Visio 2013 as a Visio 2013 .vsdx file that can be opened in SharePoint Designer 2013:</span></span>
  
    
    

### <a name="to-save-a-workflow-in-visio-2013"></a><span data-ttu-id="ef25a-205">Сохранение рабочего процесса в Visio 2013</span><span class="sxs-lookup"><span data-stu-id="ef25a-205">To save a workflow in Visio 2013</span></span>


1. <span data-ttu-id="ef25a-206">В меню **Файл** щелкните **Сохранить как**.</span><span class="sxs-lookup"><span data-stu-id="ef25a-206">Choose **File**, and then choose **Save As**.</span></span>
    
  
2. <span data-ttu-id="ef25a-207">В окне **Сохранить как** нажмите кнопку **Сохранить**, а затем нажмите **Обзор**.</span><span class="sxs-lookup"><span data-stu-id="ef25a-207">Under **Save As**, choose **Save**, and then choose **Browse**.</span></span>
    
  
3. <span data-ttu-id="ef25a-208">В диалоговом окне **Сохранить как** выберите папку для сохранения файла и введите имя файла ("My SP Workflow").</span><span class="sxs-lookup"><span data-stu-id="ef25a-208">In the **Save As** dialog box, select a location to save the file and type a name for the file ("My SP Workflow").</span></span>
    
  
4. <span data-ttu-id="ef25a-209">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="ef25a-209">Choose **Save**.</span></span>
    
  

## <a name="customizing-and-publishing-a-workflow-in-sharepoint-designer-2013"></a><span data-ttu-id="ef25a-210">Настройка и публикация рабочего процесса в SharePoint Designer 2013</span><span class="sxs-lookup"><span data-stu-id="ef25a-210">Customizing and publishing a workflow in SharePoint Designer 2013</span></span>
<span data-ttu-id="ef25a-211"><a name="VSSPD_Customizing"> </a></span><span class="sxs-lookup"><span data-stu-id="ef25a-211"></span></span>

<span data-ttu-id="ef25a-p127">После создания базовой бизнес-логики для рабочего процесса SharePoint в Visio 2013 и сохранения схем вы можете открыть VSDX-файл Visio в SharePoint Designer 2013 и приступить к настройке рабочего процесса для вашего сайта SharePoint. VSDX-файл содержит XML-документы, которые SharePoint Designer 2013 может преобразовать в рабочие процессы.</span><span class="sxs-lookup"><span data-stu-id="ef25a-p127">Once you have created the underlying business logic for a SharePoint workflow in Visio 2013 and saved the diagram, you can open the Visio .vsdx file in SharePoint Designer 2013 and begin tailoring the workflow to your SharePoint site. The .vsdx file package contains XML documents that SharePoint Designer 2013 can translate into workflows.</span></span>
  
    
    
<span data-ttu-id="ef25a-214">Используйте следующую процедуру, чтобы открыть сайт SharePoint в SharePoint Designer 2013:</span><span class="sxs-lookup"><span data-stu-id="ef25a-214">Use the following procedure to open a SharePoint site in SharePoint Designer 2013:</span></span>
  
    
    

### <a name="to-open-a-sharepoint-site-in-sharepoint-designer-2013"></a><span data-ttu-id="ef25a-215">Открытие сайта SharePoint в SharePoint Designer 2013</span><span class="sxs-lookup"><span data-stu-id="ef25a-215">To open a SharePoint site in SharePoint Designer 2013</span></span>


1. <span data-ttu-id="ef25a-216">Откройте SharePoint Designer 2013.</span><span class="sxs-lookup"><span data-stu-id="ef25a-216">Open SharePoint Designer 2013.</span></span>
    
  
2. <span data-ttu-id="ef25a-217">В окне **Открыть сайт SharePoint** нажмите кнопку **Открыть сайт**.</span><span class="sxs-lookup"><span data-stu-id="ef25a-217">Under **Open SharePoint Site**, choose **Open Site**.</span></span>
    
  
3. <span data-ttu-id="ef25a-218">В диалоговом окне **Открытие сайта** выберите сайт, который требуется открыть.</span><span class="sxs-lookup"><span data-stu-id="ef25a-218">In the **Open Site** dialog box, select the site that you want to open.</span></span>
    
  
4. <span data-ttu-id="ef25a-219">Нажмите кнопку **Открыть**.</span><span class="sxs-lookup"><span data-stu-id="ef25a-219">Choose **Open**.</span></span>
    
  
<span data-ttu-id="ef25a-220">После открытия сайта SharePoint вы можете открыть VSDX-схему Visio 2013 в SharePoint Designer 2013.</span><span class="sxs-lookup"><span data-stu-id="ef25a-220">Once the SharePoint site is open, you can open the Visio 2013 .vsdx diagram within SharePoint Designer 2013.</span></span>
  
    
    

### <a name="to-open-a-visio-professional-2013-workflow-in-sharepoint-designer-2013"></a><span data-ttu-id="ef25a-221">Открытие рабочего процесса Visio профессиональный 2013 в SharePoint Designer 2013</span><span class="sxs-lookup"><span data-stu-id="ef25a-221">To open a Visio Professional 2013 workflow in SharePoint Designer 2013</span></span>


1. <span data-ttu-id="ef25a-222">В меню **Файл** щелкните **Добавить элемент**.</span><span class="sxs-lookup"><span data-stu-id="ef25a-222">Choose **File**, and then choose **Add Item**.</span></span>
    
  
2. <span data-ttu-id="ef25a-223">Чтобы создать рабочий процесс списка, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="ef25a-223">To create a List Workflow, do the following:</span></span>
    
1. <span data-ttu-id="ef25a-224">В разделе **Рабочие процессы** выберите **Рабочий процесс списка**.</span><span class="sxs-lookup"><span data-stu-id="ef25a-224">Under **Workflows**, choose **List Workflow**.</span></span>
    
  
2. <span data-ttu-id="ef25a-225">В области слева в разделе **Рабочий процесс списка** введите имя рабочего процесса (Мой первый рабочий процесс SP2013) и выберите список на сайте, на котором вы хотите опубликовать рабочий процесс.</span><span class="sxs-lookup"><span data-stu-id="ef25a-225">In the left pane under **List Workflow**, type a name for your workflow (My First SP2013 Workflow) and select the list on the site that you want to publish the workflow to.</span></span>
    
  
3. <span data-ttu-id="ef25a-226">В списке **Выберите платформу рабочего процесса для нового рабочего процесса** выберите элемент **Рабочий процесс SharePoint**.</span><span class="sxs-lookup"><span data-stu-id="ef25a-226">In the **Choose the workflow platform for the new workflow** list, select **SharePoint Workflow**.</span></span>
    
  
4. <span data-ttu-id="ef25a-227">Выберите пункт **Создать**.</span><span class="sxs-lookup"><span data-stu-id="ef25a-227">Choose **Create**.</span></span>
    
  
3. <span data-ttu-id="ef25a-228">Чтобы создать рабочий процесс сайта, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="ef25a-228">To create a Site Workflow, do the following:</span></span>
    
1. <span data-ttu-id="ef25a-229">В разделе **Рабочие процессы** выберите **Рабочий процесс сайта**.</span><span class="sxs-lookup"><span data-stu-id="ef25a-229">Under **Workflows**, choose **Site Workflow**.</span></span>
    
  
2. <span data-ttu-id="ef25a-230">В области слева в разделе **Рабочий процесс сайта** введите имя рабочего процесса (Мой первый рабочий процесс SP2013).</span><span class="sxs-lookup"><span data-stu-id="ef25a-230">In the left pane, under **Site Workflow**, type a name for your workflow (My First SP2013 Workflow).</span></span>
    
  
3. <span data-ttu-id="ef25a-231">В списке **Выберите платформу рабочего процесса для нового рабочего процесса** выберите элемент **Рабочий процесс SharePoint**.</span><span class="sxs-lookup"><span data-stu-id="ef25a-231">In the **Choose the workflow platform for the new workflow** list, select **SharePoint Workflow**.</span></span>
    
  
4. <span data-ttu-id="ef25a-232">Выберите пункт **Создать**.</span><span class="sxs-lookup"><span data-stu-id="ef25a-232">Choose **Create**.</span></span>
    
  
4. <span data-ttu-id="ef25a-233">На вкладке **Рабочий процесс** в группе **Управление** щелкните **Параметры рабочих процессов**.</span><span class="sxs-lookup"><span data-stu-id="ef25a-233">On the **Workflow** tab, in the **Manage** group, choose **Workflow Settings**.</span></span>
    
  
5. <span data-ttu-id="ef25a-234">На вкладке **Параметры рабочего процесса** в группе **Управление** щелкните **Импортировать из Visio**.</span><span class="sxs-lookup"><span data-stu-id="ef25a-234">On the **Workflow Settings** tab, in the **Manage** group, choose **Import from Visio.**</span></span>
    
  
6. <span data-ttu-id="ef25a-235">В диалоговом окне **Импорт рабочего процесса из документа Visio** перейдите к папке, где находится VSDX-файл.</span><span class="sxs-lookup"><span data-stu-id="ef25a-235">In the **Import Workflow from Visio Drawing** dialog box, browse to the location where the .vsdx file is located.</span></span>
    
  
7. <span data-ttu-id="ef25a-236">Выберите файл, который нужно открыть (My SP Workflow), а затем нажмите кнопку **Открыть**.</span><span class="sxs-lookup"><span data-stu-id="ef25a-236">Select the file that you want to open (My SP Workflow), and then choose **Open**.</span></span>
    
  
<span data-ttu-id="ef25a-p128">После открытия VSDX-файла в SharePoint Designer 2013 он отображается в визуальном конструкторе, элементе управления ActiveX Visio, который размещен в SharePoint Designer. Схема Visio 2013 сохраняет все фигуры и текст фигур, который был создан в Visio.</span><span class="sxs-lookup"><span data-stu-id="ef25a-p128">When you open a .vsdx file in SharePoint Designer 2013, the file is displayed in the Visual Designer, a Visio ActiveX control that is hosted within SharePoint Designer. The Visio 2013 diagram retains all of the shapes and shape text that was created in Visio.</span></span> 
  
    
    

> <span data-ttu-id="ef25a-239">**Примечание.** Для переключения между визуальным и декларативным конструкторами в SharePoint Designer 2013 в группе **Управление** на вкладке **Рабочий процесс** щелкните **Вид**.</span><span class="sxs-lookup"><span data-stu-id="ef25a-239">**Note:** To switch between the Visual Designer and the Declarative Designer in SharePoint Designer 2013, on the **Workflow** tab, in the **Manage** group, choose **Views**.</span></span> <span data-ttu-id="ef25a-240">Этот процесс может занять несколько секунд, так как SharePoint Designer 2013 проверяет рабочий процесс, а затем преобразовывает его данные из одного формата в другой.</span><span class="sxs-lookup"><span data-stu-id="ef25a-240">This process may take a few moments, as SharePoint Designer 2013 validates the workflow and then converts the workflow information from one format to another.</span></span> <span data-ttu-id="ef25a-241">Во время этого процесса выполняется другая проверка на уровне фигур.</span><span class="sxs-lookup"><span data-stu-id="ef25a-241">During this process, another shape level validation will occur.</span></span> <span data-ttu-id="ef25a-242">Если будут обнаружены ошибки схемы, они будут отображаться в области ошибок (в нижней части полотна) точно так же, как в Visio.</span><span class="sxs-lookup"><span data-stu-id="ef25a-242">If any errors are detected with the diagram, the errors will be displayed in an error pane at the bottom of the canvas (just like in Visio).</span></span> 
  
    
    

<span data-ttu-id="ef25a-p130">Фигуры, которые отображаются в визуальном конструкторе, также имеют теги действий (они отмечены значком параметров рабочего процесса в левом нижнем углу фигуры). При выборе тега действия в раскрывающемся меню отображаются атрибуты для этого действия или условия и свойство **Свойства**. Эти свойства определяют значения параметров для этого действия: из каких списков будут извлечены элементы, какой оператор вычисления будет использоваться или на какой адрес электронной почты будет отправлено сообщение. Если выбрать свойство, которое отображается в списке, появится диалоговое окно в котором можно настроить параметры для этого свойства.</span><span class="sxs-lookup"><span data-stu-id="ef25a-p130">The shapes that are displayed in the Visual Designer also have Action Tags (shown by a workflow settings type icon on the bottom left hand side of the shape). When you choose an Action Tag, a drop-down menu displays the attributes for that action or condition in the workflow and **Properties** property. These properties will define the parameter values to be used for that action: which lists to pull items from, what calculation operator to use, or which email address to send a message to. When you choose a property that is displayed in the list, a dialog box appears in which you can customize the settings for that property.</span></span>
  
    
    
<span data-ttu-id="ef25a-p131">Например, с фигурой **Отправить сообщение электронной почты** связано два свойства: **Создать сообщение электронной почты** и **Свойства**. Если выбрать свойство **Создать сообщение электронной почты**, откроется диалоговое окно **Определение сообщения электронной почты**, в котором можно создать сообщение, отправляемое действием. Если выбрать **Свойство** откроется диалоговое окно **Свойства отправки сообщения электронной почты**, в котором отображаются все параметры действия.</span><span class="sxs-lookup"><span data-stu-id="ef25a-p131">For example, the **Send an email** shape has two properties associated with it: **Create Email** and **Properties**. When you choose **Create Email**, a **Define Email Message** dialog box appears in which you can create the message to be sent by the action. If you choose **Properties**, a **Send an Email Properties** dialog box appears that displays all of the parameters for the action.</span></span>
  
    
    

> <span data-ttu-id="ef25a-250">**Примечание.** Дополнительные сведения об отдельных действиях, фигурах и их свойствах см. в статьях [Фигуры в шаблоне рабочих процессов SharePoint Server в Visio](shapes-in-the-sharepoint-server-workflow-template-in-visio.md) и [Краткий справочник по действиям рабочих процессов (платформа рабочих процессов в SharePoint)](workflow-actions-quick-reference-sharepoint-workflow-platform.md).</span><span class="sxs-lookup"><span data-stu-id="ef25a-250">**Note** For more information about individual actions, shapes, and their properties, see the articles  [Shapes in the SharePoint Server workflow template in Visio](shapes-in-the-sharepoint-server-workflow-template-in-visio.md) and [Workflow actions quick reference (SharePoint Workflow platform)](workflow-actions-quick-reference-sharepoint-workflow-platform.md).</span></span> 
  
    
    

<span data-ttu-id="ef25a-p132">После установки свойств в рабочем процессе и перед публикацией сначала следует проверить рабочий процесс на наличие ошибок в SharePoint Designer 2013. Если выбрать команду **Опубликовать** в **визуальном конструкторе** на ленте, SharePoint Designer 2013 автоматически проверяет рабочий процесс на наличие ошибок. При необходимости проверку можно запустить вручную.</span><span class="sxs-lookup"><span data-stu-id="ef25a-p132">Once you have set the properties within the workflow and are ready to publish, you must first check the workflow for errors in SharePoint Designer 2013. When you choose **Publish** in the **Visual Designer** tab in the ribbon, SharePoint Designer 2013 automatically checks the workflow for errors. If you want, you can also manually initiate the error checking.</span></span>
  
    
    
<span data-ttu-id="ef25a-254">Используйте следующую процедуру, чтобы проверить рабочий процесс SharePoint в SharePoint Designer 2013:</span><span class="sxs-lookup"><span data-stu-id="ef25a-254">Use the following procedure to check the SharePoint workflow in SharePoint Designer 2013:</span></span>
  
    
    

### <a name="to-manually-check-a-workflow-for-errors-in-sharepoint-designer-2013"></a><span data-ttu-id="ef25a-255">Проверка рабочего процесса на наличие ошибок вручную SharePoint Designer 2013</span><span class="sxs-lookup"><span data-stu-id="ef25a-255">To manually check a workflow for errors in SharePoint Designer 2013</span></span>


1. <span data-ttu-id="ef25a-256">На вкладке **Визуальный конструктор** в группе **Сохранить** нажмите кнопку **Проверить**.</span><span class="sxs-lookup"><span data-stu-id="ef25a-256">On the **Visual Designer** tab, in the **Save** group, choose **Check for Errors**.</span></span>
    
  
2. <span data-ttu-id="ef25a-p133">Если в рабочем процессе найдены ошибки, под визуальным конструктором откроется область **Проблемы**. Выберите каждый элемент в списке, чтобы выделить действие, условие, соединитель, оконечный элемент или контейнер на схеме, вызвавший ошибку.</span><span class="sxs-lookup"><span data-stu-id="ef25a-p133">If any errors are found in the workflow, the **Issues** pane opens below the Visual Designer canvas. Choose each item in the list to select the action, condition, connector, terminator, or container in the workflow that caused the error.</span></span>
    
  
3. <span data-ttu-id="ef25a-p134">Устраните все ошибки проверки, указанные в списке **Проблемы**. После этого нажмите кнопку **Проверить** еще раз.</span><span class="sxs-lookup"><span data-stu-id="ef25a-p134">Resolve each validation error listed in the **Issues** list. Once all of the errors have been addressed, choose **Check for Errors** again.</span></span>
    
  
4. <span data-ttu-id="ef25a-261">Если ошибки в рабочем процессе не найдены, SharePoint Designer отображает сообщение об успешной проверке.</span><span class="sxs-lookup"><span data-stu-id="ef25a-261">If no errors are found in the workflow, SharePoint Designer displays a message stating that no issues were found in the workflow.</span></span>
    
  
<span data-ttu-id="ef25a-p135">Если после проверки рабочего процесса проблемы не обнаружены, вы можете опубликовать рабочий процесс в списке SharePoint. Чтобы опубликовать рабочий процесс из SharePoint Designer 2013, на вкладке **Визуальный конструктор** в группе **Сохранить** нажмите кнопку **Опубликовать**. При возникновении ошибки во время публикации SharePoint Designer 2013 возвращается в визуальный конструктор и отображает ошибки в области **Проблемы**.</span><span class="sxs-lookup"><span data-stu-id="ef25a-p135">After the workflow has been checked and no issues have been found, you can publish the workflow to the SharePoint list. To publish the workflow from SharePoint Designer 2013, on the **Visual Designer** tab, in the **Save** group, choose **Publish**. If any errors occur during the publishing process, SharePoint Designer 2013 returns to the Visual Designer and displays the errors in the **Issues** pane.</span></span>
  
    
    

## <a name="additional-resources"></a><span data-ttu-id="ef25a-265">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="ef25a-265">Additional Resources</span></span>
<span data-ttu-id="ef25a-266"><a name="VSSPD_Additional"> </a></span><span class="sxs-lookup"><span data-stu-id="ef25a-266"></span></span>

<span data-ttu-id="ef25a-267">Дополнительные сведения см. в следующих источниках:</span><span class="sxs-lookup"><span data-stu-id="ef25a-267">For more information, see the following resources:</span></span>
  
    
    

-  [<span data-ttu-id="ef25a-268">Краткий справочник по действиям рабочего процесса (платформа рабочих процессов в SharePoint)</span><span class="sxs-lookup"><span data-stu-id="ef25a-268">Workflow actions quick reference (SharePoint Workflow platform)</span></span>](workflow-actions-quick-reference-sharepoint-workflow-platform.md)
    
  
-  [<span data-ttu-id="ef25a-269">Фигуры в шаблоне рабочего процесса SharePoint Server в Visio</span><span class="sxs-lookup"><span data-stu-id="ef25a-269">Shapes in the SharePoint Server workflow template in Visio</span></span>](shapes-in-the-sharepoint-server-workflow-template-in-visio.md)
    
  
-  [<span data-ttu-id="ef25a-270">Диагностика ошибок проверки рабочих процессов SharePoint Server в Visio</span><span class="sxs-lookup"><span data-stu-id="ef25a-270">Troubleshooting SharePoint Server workflow validation errors in Visio</span></span>](troubleshooting-sharepoint-server-workflow-validation-errors-in-visio.md)
    
  
-  [<span data-ttu-id="ef25a-271">Создание, импорт и экспорт рабочих процессов SharePoint в Visio 2010</span><span class="sxs-lookup"><span data-stu-id="ef25a-271">Create, import, and export SharePoint workflows in Visio 2010</span></span>](http://office.microsoft.com/ru-RU/visio-help/create-import-and-export-sharepoint-workflows-in-visio-HA101888007.aspx)
    
  
-  [<span data-ttu-id="ef25a-272">Центр по разработке для SharePoint</span><span class="sxs-lookup"><span data-stu-id="ef25a-272">SharePoint Developer Center</span></span>](http://msdn.microsoft.com/ru-RU/sharepoint/default.aspx)
    
  
-  [<span data-ttu-id="ef25a-273">Центр по разработке для Visio</span><span class="sxs-lookup"><span data-stu-id="ef25a-273">Visio Developer Center</span></span>](http://msdn.microsoft.com/ru-RU/office/aa905478)
    
  

