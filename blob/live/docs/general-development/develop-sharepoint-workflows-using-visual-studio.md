---
title: "Разработка рабочих процессов SharePoint с помощью Visual Studio"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 28f5d3b1-6fe8-4b1f-8c4e-b11105fe6f46
ms.openlocfilehash: de2db87007f801da6555d5f749028f4a30eda172
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="develop-sharepoint-workflows-using-visual-studio"></a><span data-ttu-id="7b471-102">Разработка рабочих процессов SharePoint с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7b471-102">Develop SharePoint workflows using Visual Studio</span></span>
<span data-ttu-id="7b471-p101">SharePointподдерживает две основных среды разработки среды рабочих процессов: SharePoint Designer и Visual Studio. В этой статье описаны обе среды, а также преимущества и недостатки каждой из них.</span><span class="sxs-lookup"><span data-stu-id="7b471-p101">SharePoint supports two primary workflow development environments for authoring workflows: SharePoint Designer and Visual Studio. This article summarizes both and discusses the advantages and disadvantages of each.</span></span>
## <a name="authoring-basics-for-sharepoint-workflows"></a><span data-ttu-id="7b471-105">Основы создания рабочих процессов SharePoint</span><span class="sxs-lookup"><span data-stu-id="7b471-105">Authoring basics for SharePoint workflows</span></span>
<span data-ttu-id="7b471-106"><a name="bkm_AuthoringBasics"> </a></span><span class="sxs-lookup"><span data-stu-id="7b471-106"></span></span>


> <span data-ttu-id="7b471-107">**Примечание.** Руководство по установке и настройке Microsoft SharePoint и сервера Workflow Manager Client 1.0 см. в статье [Установка и настройка диспетчера рабочих процессов SharePoint](set-up-and-configure-sharepoint-workflow-manager.md).</span><span class="sxs-lookup"><span data-stu-id="7b471-107">**Note** For guidance on setting up and configuring Microsoft SharePoint Server 2013 and the Workflow Manager Client 1.0 server, see  [Set up and configure SharePoint Workflow Manager](set-up-and-configure-sharepoint-workflow-manager.md).</span></span> 
  
    
    

<span data-ttu-id="7b471-p102">Как и в предыдущих версиях, Microsoft SharePoint предоставляет две основных среды разработки рабочих процессов: Microsoft SharePoint Designer и Microsoft Visual Studio. Однако отличие от предыдущих версий состоит в том, что при использовании Visual Studio больше нет стратегии разработки на основе кода. Вместо этого и SharePoint Designer, и Visual Studio реализуют полностью декларативную среду разработки без кода независимо от выбранного средства разработки.</span><span class="sxs-lookup"><span data-stu-id="7b471-p102">As with previous versions, Microsoft SharePoint provides two primary workflow development environments for authoring workflows: Microsoft SharePoint Designer and Microsoft Visual Studio. However, what differs from previous versions is that using Visual Studio no longer provides a code-based authoring strategy. Instead, both SharePoint Designer and Visual Studio provide a fully declarative, no-code authoring environment regardless of the development tool you select.</span></span>
  
    
    

> <span data-ttu-id="7b471-111">**Примечание.** Помимо разработки рабочих процессов в SharePoint Designer, вы также можете использовать Microsoft Visio 2013 для структурирования логики рабочих процессов с помощью фигур Visio 2013 и последующего импорта логики в SharePoint Designer 2013.</span><span class="sxs-lookup"><span data-stu-id="7b471-111">**Note** As a complement to authoring workflows in SharePoint Designer, you can also use Microsoft Visio 2013 to structure your workflow logic by using Visio 2013 shapes, and then import your logic into SharePoint Designer 2013. For information about using Visio 2013 to author your workflow logic, see  Workflow development in SharePoint Designer and Visio.</span></span> <span data-ttu-id="7b471-112">Сведения о разработке логики рабочих процессов с помощью Visio 2013 см. в статье [Разработка рабочих процессов в SharePoint Designer и Visio](workflow-development-in-sharepoint-designer-and-visio.md).</span><span class="sxs-lookup"><span data-stu-id="7b471-112">For information about using Visio 2013 to author your workflow logic, see  [Workflow development in SharePoint Designer and Visio](workflow-development-in-sharepoint-designer-and-visio.md).</span></span> 
  
    
    


### <a name="declarative-workflows"></a><span data-ttu-id="7b471-113">Декларативные рабочие процессы</span><span class="sxs-lookup"><span data-stu-id="7b471-113">Declarative workflows</span></span>

<span data-ttu-id="7b471-p104">Сначала поясним, что подразумевается под "декларативными" рабочими процессами. Этот термин означает, что вместо написания кода и компиляции в управляемые сборки рабочий процесс описывается (буквально) в XAML и затем интерпретируется во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="7b471-p104">Let's first be clear what is meant by "declarative" workflows. This term means that instead of being authored in code and then compiled into managed assemblies, the workflow is described (literally) in XAML and then executed interpretively at run time.</span></span>
  
    
    
<span data-ttu-id="7b471-p105">XAML формируется на основе стандартных блоков рабочего процесса, которыми вы управляете в Конструктор рабочих процессов (при использовании Visual Studio) или в области конструктора рабочих процессов SharePoint Designer (или Visio, но об этом поговорим позже). Стандартные блоки  это визуальные объекты проектирования рабочего процесса в панели инструментов конструктора: стадии, условия, этапы, события и т. д. Набор инструментов в соответствующих панелях инструментов (Visual Studio или SharePoint Designer) отличается, но концепция декларативных рабочих процессов остается неизменным.</span><span class="sxs-lookup"><span data-stu-id="7b471-p105">The XAML is derived (or inferred) from the workflow building blocks that you manipulate in the Workflow Designer (if using Visual Studio) or SharePoint Designer workflow design surface (or Visio, but more about that later). The building blocks themselves are the visual workflow design objects in the designer toolbox—stages, conditions, actions, events, and so on. The set of tools in the respective toolboxes (Visual Studio or SharePoint Designer) differs somewhat, but the concept of the declarative workflow remains the same.</span></span>
  
    
    

## <a name="decision-tree-sharepoint-designer-vs-visual-studio"></a><span data-ttu-id="7b471-119">Дерево принятия решений: SharePoint Designer и Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7b471-119">Decision tree: SharePoint Designer vs. Visual Studio</span></span>
<span data-ttu-id="7b471-120"><a name="bkm_DecisionTree"> </a></span><span class="sxs-lookup"><span data-stu-id="7b471-120"></span></span>

<span data-ttu-id="7b471-p106">Одно из основных преимуществ платформы рабочих процессов в SharePoint  это простота использования среды без кода SharePoint Designer для создания мощных рабочих процессов. Кроме того, декларативная среда разработки, такая как Visual Studio, обеспечивает высокую степень гибкости и настройки.</span><span class="sxs-lookup"><span data-stu-id="7b471-p106">Among the greatest advantages of the workflow framework in SharePoint is the ease with which information workers can use the no-code environment of SharePoint Designer to create rich and powerful workflows. Additionally, a high degree of flexibility and customization is available in a declarative authoring environment such as Visual Studio.</span></span>
  
    
    
<span data-ttu-id="7b471-p107">Обе этих среды, SharePoint Designer и Visual Studio, обладают определенными преимуществами и недостатками. В этом разделе мы расскажем, как определить, какая среда разработки больше всего подходит вам.</span><span class="sxs-lookup"><span data-stu-id="7b471-p107">Both of these workflow authoring environments—SharePoint Designer and Visual Studio—offer specific advantages and disadvantages. In this section, we explore how to determine which authoring environment best suits your workflow development needs.</span></span>
  
    
    

### <a name="using-sharepoint-designer"></a><span data-ttu-id="7b471-125">Использование SharePoint Designer</span><span class="sxs-lookup"><span data-stu-id="7b471-125">Using SharePoint Designer</span></span>


- <span data-ttu-id="7b471-126">**Целевые пользователи:** информационные работники, бизнес-аналитики, разработчики SharePoint.</span><span class="sxs-lookup"><span data-stu-id="7b471-126">**Target users:** Information workers, business analysts, SharePoint developers.</span></span>
    
  
- <span data-ttu-id="7b471-127">**Уровень сложности:** знакомство SharePoint Designer, в том числе с основными компонентами рабочего процесса, такими как стадии, шлюзы, этапы, условия и циклы.</span><span class="sxs-lookup"><span data-stu-id="7b471-127">**Difficulty level:** Familiarity with SharePoint Designer, including the core workflow components, such as stages, gates, actions, conditions, and loops.</span></span>
    
  
<span data-ttu-id="7b471-p108">В SharePoint Designer можно создать рабочий процесс, который присоединяется к списку, библиотеке или сайту, с помощью текстового конструктора без кода. Или они могут использовать новую визуальную среду разработки, в которой графические элементы размещаются на поверхности разработки и представляют логический поток бизнес-процесса. SharePoint Designer позволяет быстро создавать рабочие процессы даже нетехническим специалистам.</span><span class="sxs-lookup"><span data-stu-id="7b471-p108">With SharePoint Designer, users can create a workflow that is attached to a list, library, or site using a no-code, text-based designer. Or, they can use the new visual design environment in which graphical elements are arranged on a design surface to represent the logical flow of a business process. SharePoint Designer excels at enabling rapid workflow development by non-technical workers.</span></span>
  
    
    

### <a name="using-visual-studio"></a><span data-ttu-id="7b471-131">Использование Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7b471-131">Using Visual Studio</span></span>


- <span data-ttu-id="7b471-132">**Целевые пользователи:** разработчики программного обеспечения среднего или высокого уровня.</span><span class="sxs-lookup"><span data-stu-id="7b471-132">**Target users:** Intermediate or advanced software developers.</span></span>
    
  
- <span data-ttu-id="7b471-133">**Уровень сложности:** знакомство с Visual Studio, в том числе с концепциями разработки программного обеспечения, приемниками событий, упаковкой, развертыванием и безопасностью.</span><span class="sxs-lookup"><span data-stu-id="7b471-133">**Difficulty level:** Familiarity with Visual Studio, including software development concepts such as event receivers, packaging and deployment, and security.</span></span>
    
  
<span data-ttu-id="7b471-p109">Visual Studio позволяет гибко создавать рабочие процессы для поддержки практически любого бизнес-процесса независимо от его сложности. Разработчики также могут выполнять отладку и повторно использовать определения рабочих процессов. Возможно, наиболее важное преимущество Visual Studio состоит в том, что разработчики могут добавлять рабочие процессы SharePoint в рамках более крупного решения SharePoint или Надстройка SharePoint.</span><span class="sxs-lookup"><span data-stu-id="7b471-p109">Authoring workflows in Visual Studio provides flexibility to create workflows to support virtually any business process, regardless of its complexity, and allows debugging and reuse of workflow definitions. Perhaps most important, Visual Studio lets developers include SharePoint workflows as part of a broader SharePoint solution or SharePoint Add-in.</span></span>
  
    
    
<span data-ttu-id="7b471-p110">Visual Studioпозволяет разработчикам создавать настраиваемые действия для SharePoint Designer и предоставляет средства для выполнения настраиваемой логики. С помощью Visual Studio разработчики также могут создавать шаблоны рабочих процессов, которые можно развернуть на нескольких сайтах.</span><span class="sxs-lookup"><span data-stu-id="7b471-p110">Visual Studio enables developers to create custom actions for consumption by SharePoint Designer, and provides the means to execute custom logic. With Visual Studio, developers can also create workflow templates, which can be deployed to multiple sites.</span></span>
  
    
    

## <a name="comparing-sharepoint-designer-with-visual-studio"></a><span data-ttu-id="7b471-138">Сравнение SharePoint Designer с Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7b471-138">Comparing SharePoint Designer with Visual Studio</span></span>
<span data-ttu-id="7b471-139"><a name="bkm_Comparing"> </a></span><span class="sxs-lookup"><span data-stu-id="7b471-139"></span></span>

<span data-ttu-id="7b471-140">В таблице ниже сравниваются функции создания рабочих процессов SharePoint SharePoint Designer и Visual Studio, а также требования к их использованию.</span><span class="sxs-lookup"><span data-stu-id="7b471-140">The following table provides a side-by-side comparison of the features and requirements for using SharePoint Designer and Visual Studio to create SharePoint workflows.</span></span>
  
    
    

<span data-ttu-id="7b471-141">**Таблица 1. Сравнение инструментов создания рабочих процессов**</span><span class="sxs-lookup"><span data-stu-id="7b471-141">**Table 1. Workflow authoring tool comparison**</span></span>


|<span data-ttu-id="7b471-142">**Функции и требования**</span><span class="sxs-lookup"><span data-stu-id="7b471-142">**Feature / Requirement**</span></span>|<span data-ttu-id="7b471-143">**SharePoint Designer**</span><span class="sxs-lookup"><span data-stu-id="7b471-143">**SharePoint Designer**</span></span>|<span data-ttu-id="7b471-144">**Visual Studio**</span><span class="sxs-lookup"><span data-stu-id="7b471-144">**Visual Studio**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="7b471-145">Быстрое создание рабочих процессов</span><span class="sxs-lookup"><span data-stu-id="7b471-145">Allows rapid workflow development</span></span>  <br/> |<span data-ttu-id="7b471-146">Да</span><span class="sxs-lookup"><span data-stu-id="7b471-146">Yes</span></span>  <br/> |<span data-ttu-id="7b471-147">Да</span><span class="sxs-lookup"><span data-stu-id="7b471-147">Yes</span></span>  <br/> |
|<span data-ttu-id="7b471-148">Повторное использование рабочих процессов</span><span class="sxs-lookup"><span data-stu-id="7b471-148">Enables reuse of workflows</span></span>  <br/> |<span data-ttu-id="7b471-p111">Рабочий процесс может использоваться только списком или библиотекой, в котором он был создан. Однако SharePoint Designer предоставляет рабочие процессы, которые могут использоваться несколько раз на одном сайте.</span><span class="sxs-lookup"><span data-stu-id="7b471-p111">A workflow can be used only by the list or library on which it was developed. However, SharePoint Designer provides reusable workflows that can be used multiple times within the same site.</span></span>  <br/> |<span data-ttu-id="7b471-151">Рабочий процесс можно создать как шаблон, чтобы после развертывания его можно было повторно использовать и связывать с любым списком или библиотекой.</span><span class="sxs-lookup"><span data-stu-id="7b471-151">A workflow can be written as a template so that after it is deployed, it can be reused and associated with any list or library.</span></span>  <br/> |
|<span data-ttu-id="7b471-152">Позволяет добавить рабочий процесс в решение SharePoint или Надстройка SharePoint</span><span class="sxs-lookup"><span data-stu-id="7b471-152">Allows you to include a workflow as part of a SharePoint solution or SharePoint Add-in</span></span>  <br/> |<span data-ttu-id="7b471-153">Нет</span><span class="sxs-lookup"><span data-stu-id="7b471-153">No</span></span>  <br/> |<span data-ttu-id="7b471-154">Да</span><span class="sxs-lookup"><span data-stu-id="7b471-154">Yes</span></span>  <br/> |
|<span data-ttu-id="7b471-155">Позволяет создавать настраиваемые действия</span><span class="sxs-lookup"><span data-stu-id="7b471-155">Allows you to create custom actions</span></span>  <br/> |<span data-ttu-id="7b471-p112">Нет. Однако SharePoint Designer может использовать и реализовать настраиваемые действия, которые создаются и развертываются с помощью Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7b471-p112">No. However, SharePoint Designer can consume and implement custom actions that are created and deployed by using Visual Studio.</span></span>  <br/> |<span data-ttu-id="7b471-p113">Да. Однако помните, что в Visual Studio используются базовые действия, а не соответствующие им действия.</span><span class="sxs-lookup"><span data-stu-id="7b471-p113">Yes. However, be aware that in Visual Studio, the underlying activities, not their corresponding actions, are used.</span></span>  <br/> |
|<span data-ttu-id="7b471-160">Позволяет создавать пользовательский код</span><span class="sxs-lookup"><span data-stu-id="7b471-160">Allows you to write custom code</span></span>  <br/> |<span data-ttu-id="7b471-161">Нет</span><span class="sxs-lookup"><span data-stu-id="7b471-161">No</span></span>  <br/> |<span data-ttu-id="7b471-162">Нет</span><span class="sxs-lookup"><span data-stu-id="7b471-162">No</span></span>  <br/> <span data-ttu-id="7b471-163">**Примечание.** Эта возможность изменилась по сравнению с предыдущими версиями.</span><span class="sxs-lookup"><span data-stu-id="7b471-163">**Note:** This is changed from previous versions.</span></span> <span data-ttu-id="7b471-164">В SharePoint используются только декларативные рабочие процессы, а в Visual Studio для разработки рабочих процессов применяется рабочая область визуального конструирования.</span><span class="sxs-lookup"><span data-stu-id="7b471-164">This is changed from previous versions. In SharePoint, workflows are declarative only and Visual Studio relies on the visual design surface for workflow development.</span></span>           |
|<span data-ttu-id="7b471-165">Возможность создавать логику рабочих процессов с помощью Visio профессиональный</span><span class="sxs-lookup"><span data-stu-id="7b471-165">Can use Visio Professional to create workflow logic</span></span>  <br/> |<span data-ttu-id="7b471-166">Да</span><span class="sxs-lookup"><span data-stu-id="7b471-166">Yes</span></span>  <br/> |<span data-ttu-id="7b471-167">Нет</span><span class="sxs-lookup"><span data-stu-id="7b471-167">No</span></span>  <br/> |
|<span data-ttu-id="7b471-168">развертывание, —</span><span class="sxs-lookup"><span data-stu-id="7b471-168">Deployment</span></span>  <br/> |<span data-ttu-id="7b471-169">Автоматическое развертывание в списке, библиотеке или на сайте, на котором они созданы.</span><span class="sxs-lookup"><span data-stu-id="7b471-169">Deployed automatically to list, library, or site on which they were created.</span></span>  <br/> |<span data-ttu-id="7b471-170">Создание файла пакета (WSP-файла) решения SharePoint и развертывание пакета на сайте (SPWeb).</span><span class="sxs-lookup"><span data-stu-id="7b471-170">Create a SharePoint solution package (.wsp) file and deploy the solution package to the site (SPWeb).</span></span>  <br/> |
|<span data-ttu-id="7b471-171">Публикация рабочих процессов одним щелчком</span><span class="sxs-lookup"><span data-stu-id="7b471-171">One-click publishing available for workflows</span></span>  <br/> |<span data-ttu-id="7b471-172">Да</span><span class="sxs-lookup"><span data-stu-id="7b471-172">Yes</span></span>  <br/> |<span data-ttu-id="7b471-173">Да</span><span class="sxs-lookup"><span data-stu-id="7b471-173">Yes</span></span>  <br/> |
|<span data-ttu-id="7b471-174">Рабочие процессы можно упаковать и развернуть на удаленном сервере</span><span class="sxs-lookup"><span data-stu-id="7b471-174">Workflows can be packaged and deployed to a remote server</span></span>  <br/> |<span data-ttu-id="7b471-175">Да</span><span class="sxs-lookup"><span data-stu-id="7b471-175">Yes</span></span>  <br/> |<span data-ttu-id="7b471-176">Да</span><span class="sxs-lookup"><span data-stu-id="7b471-176">Yes</span></span>  <br/> |
|<span data-ttu-id="7b471-177">отладка</span><span class="sxs-lookup"><span data-stu-id="7b471-177">Debugging</span></span>  <br/> |<span data-ttu-id="7b471-178">Отладка не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="7b471-178">Cannot be debugged.</span></span>  <br/> |<span data-ttu-id="7b471-179">Рабочий процесс можно отлаживать с помощью Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7b471-179">Workflow can be debugged by using Visual Studio.</span></span>  <br/> |
|<span data-ttu-id="7b471-180">Можно использовать только действия, которые утверждены администратором сайта</span><span class="sxs-lookup"><span data-stu-id="7b471-180">Can use only actions that are approved by site administrator</span></span>  <br/> |<span data-ttu-id="7b471-181">Да</span><span class="sxs-lookup"><span data-stu-id="7b471-181">Yes</span></span>  <br/> |<span data-ttu-id="7b471-182">Да</span><span class="sxs-lookup"><span data-stu-id="7b471-182">Yes</span></span>  <br/> <span data-ttu-id="7b471-183">**Примечание.** Эта возможность изменилась по сравнению с предыдущими версиями.</span><span class="sxs-lookup"><span data-stu-id="7b471-183">**Note:** This is changed from previous versions.</span></span> <span data-ttu-id="7b471-184">Ранее рабочие процессы и действия, созданные с помощью Visual Studio, были основаны на коде и развертывались на уровне фермы, поэтому утверждение администратора не требовалось.</span><span class="sxs-lookup"><span data-stu-id="7b471-184">This is changed from previous versions. Previously, workflows and actions that were authored by using Visual Studio were code-based and deployed at the farm scope, so administrator approval was not required.</span></span>           |
   

## <a name="developing-workflows-using-visual-studio"></a><span data-ttu-id="7b471-185">Разработка рабочих процессов с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7b471-185">Developing workflows using Visual Studio</span></span>
<span data-ttu-id="7b471-186"><a name="bkm_Developing"> </a></span><span class="sxs-lookup"><span data-stu-id="7b471-186"></span></span>

<span data-ttu-id="7b471-p116">В отличие от более ранних версий рабочие процессы в SharePoint полностью декларативные. Visual Studio предоставляет визуальную поверхность разработки рабочих процессов на основе Windows Workflow Foundation 4, которая позволяет создавать собственные рабочие процессы, шаблоны рабочих процессов, формы и настраиваемые действия рабочих процессов исключительно в среде конструктора. Затем рабочий процесс упаковывается и развертывается как компонент SharePoint. Сведения об упаковке см. в статье  [Использование компонентов в SharePoint Foundation](http://msdn.microsoft.com/ru-RU/library/ms461324.aspx).</span><span class="sxs-lookup"><span data-stu-id="7b471-p116">Unlike earlier versions, workflows in SharePoint are entirely declarative. Built now on Windows Workflow Foundation 4, Visual Studio provides a visual workflow designer surface that lets you create custom workflows, workflow templates, forms, and custom workflow activities entirely in the designer environment. Your workflow is then packaged and deployed as a SharePoint Feature. For information about Feature packaging, see  [Using Features in SharePoint Foundation](http://msdn.microsoft.com/ru-RU/library/ms461324.aspx).</span></span>
  
    
    
<span data-ttu-id="7b471-p117">Возможно, наиболее значительное изменение для разработчиков Visual Studio состоит в том, что настраиваемые рабочие процессы больше не компилируются и не развертываются как сборки .NET Framework. Кроме того, SharePoint больше использует не формы Microsoft InfoPath, а формы Microsoft ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="7b471-p117">Perhaps the most significant change for Visual Studio developers is that custom workflows are no longer compiled and deployed as .NET Framework assemblies. Furthermore, SharePoint no longer uses Microsoft InfoPath forms; instead, forms generation relies on Microsoft ASP.NET forms.</span></span> 
  
    
    
<span data-ttu-id="7b471-p118">Наконец, изменились шаблоны проекта рабочего процесса Visual Studio. Ранее шаблоны были предоставлены для конечного автомата и последовательных рабочих процессов, эти различия больше не имеют смысла. Теперь шаблоны проектов Visual Studio доступны в сборке Visual Studio на виртуальной машине (ВМ).</span><span class="sxs-lookup"><span data-stu-id="7b471-p118">Finally, the Visual Studio workflow project templates have changed. Whereas formerly templates for state machine and sequential workflows were provided, these distinctions are no longer meaningful. Rather, Visual Studio project templates are available in the Visual Studio build provided on your virtual machine (VM).</span></span>
  
    
    

## <a name="enabling-on-premises-workflow-debugging"></a><span data-ttu-id="7b471-196">Включение локальной отладки рабочего процесса</span><span class="sxs-lookup"><span data-stu-id="7b471-196">Enabling on-premises workflow debugging</span></span>
<span data-ttu-id="7b471-197"><a name="bkm_Enabling"> </a></span><span class="sxs-lookup"><span data-stu-id="7b471-197"></span></span>

<span data-ttu-id="7b471-198">Для отладки локальных рабочих процессов в Visual Studio необходимо временно разрешить средствам диспетчера рабочих процессов доступ к системе в брандмауэре.</span><span class="sxs-lookup"><span data-stu-id="7b471-198">To debug on-premises workflows in Visual Studio, you need to temporarily allow the Workflow Manager Tools to access your system through the firewall.</span></span>
  
    
    

1. <span data-ttu-id="7b471-199">В **панели управления** выберите элемент **Система и безопасность** и щелкните **Брандмауэр Windows**.</span><span class="sxs-lookup"><span data-stu-id="7b471-199">In **Control Panel**, choose **System and Security**, **Windows Firewall**.</span></span>
    
  
2. <span data-ttu-id="7b471-200">В списке в **основном окне панели управления** щелкните ссылку **Дополнительные параметры**.</span><span class="sxs-lookup"><span data-stu-id="7b471-200">In the **Control Panel Home** list, choose the **Advanced Settings** link.</span></span>
    
  
3. <span data-ttu-id="7b471-201">В левой области брандмауэра Windows щелкните **Правила для входящих подключений**.</span><span class="sxs-lookup"><span data-stu-id="7b471-201">In the left pane of Windows Firewall, choose **Inbound Rules**.</span></span>
    
  
4. <span data-ttu-id="7b471-202">В списке **Правила для входящих подключений** выберите **Workflow Manager Tools 1.0 for Visual Studio 2012 - Test Service Host**.</span><span class="sxs-lookup"><span data-stu-id="7b471-202">In the **Inbound Rules** list, choose **Workflow Manager Tools 1.0 for Visual Studio 2012 - Test Service Host**.</span></span>
    
  
5. <span data-ttu-id="7b471-203">В списке **Действия** выберите **Включить правило**.</span><span class="sxs-lookup"><span data-stu-id="7b471-203">In the **Actions** list, choose **Enable Rule**.</span></span>
    
  
6. <span data-ttu-id="7b471-204">На странице свойств проекта SharePoint перейдите на вкладку **SharePoint**, а затем установите флажок **Включить отладку рабочего процесса**.</span><span class="sxs-lookup"><span data-stu-id="7b471-204">On the properties page of your SharePoint project, choose the **SharePoint** tab, and then select the **Enable Workflow debugging** check box.</span></span>
    
  

## <a name="debugging-sharepoint-online-workflows-using-visual-studio"></a><span data-ttu-id="7b471-205">Отладка рабочих процессов SharePoint Online с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7b471-205">Debugging SharePoint Online workflows using Visual Studio</span></span>
<span data-ttu-id="7b471-206"><a name="bkm_Debug"> </a></span><span class="sxs-lookup"><span data-stu-id="7b471-206"></span></span>

<span data-ttu-id="7b471-207">Для отладки рабочих процессов SharePoint Online в Visual Studio выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="7b471-207">To debug SharePoint Online workflows in Visual Studio, perform the following steps:</span></span>
  
    
    

1. <span data-ttu-id="7b471-208">Если ваша сеть защищена брандмауэром, может потребоваться установить прокси-клиент (например,  [Клиент Forefront Threat Management Gateway (TMG)](http://www.microsoft.com/en-us/download/details.aspx?displaylang=en&amp;id=10504)) в зависимости от топологии сети организации.</span><span class="sxs-lookup"><span data-stu-id="7b471-208">If you're behind a firewall, you may need to install a proxy client (such as the  [Forefront Threat Management Gateway (TMG) Client](http://www.microsoft.com/en-us/download/details.aspx?displaylang=en&amp;id=10504)), depending on your company's network topology.</span></span>
    
  
2. <span data-ttu-id="7b471-209">Если у вас еще нет учетной записи Microsoft Azure, зарегистрируйте ее, а затем выполните вход в эту учетную запись.</span><span class="sxs-lookup"><span data-stu-id="7b471-209">Register for a Microsoft Azure account if you haven't already, and then sign into that account.</span></span>
    
    <span data-ttu-id="7b471-210">Сведения о том, как зарегистрировать учетную запись Microsoft Azure, см. в статье  [Microsoft Azure](http://www.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="7b471-210">For information about how to register for a Microsoft Azure account, see  [Microsoft Azure](http://www.windowsazure.com).</span></span>
    
  
3. <span data-ttu-id="7b471-p119">Создайте пространство имен шины обслуживания Microsoft Azure, которое можно использовать для отладки рабочих процессов. Это можно сделать на  [портале управления Microsoft Azure](http://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="7b471-p119">Create a Microsoft Azure Service Bus namespace, which you can use to debug remote workflows. You can do this on the  [Microsoft Azure management portal](http://manage.windowsazure.com).</span></span>
    
    <span data-ttu-id="7b471-213">Дополнительные сведения о служебной шине Microsoft Azure см. в статье [Управление пространствами имен служебной шины](http://msdn.microsoft.com/ru-RU/library/windowsazure/hh690928.aspx).</span><span class="sxs-lookup"><span data-stu-id="7b471-213">For more information about the Microsoft Azure Service Bus, see  [Managing Service Bus Service Namespaces](http://msdn.microsoft.com/ru-RU/library/windowsazure/hh690928.aspx).</span></span>
    
    > <span data-ttu-id="7b471-214">**Примечание.** Для отладки рабочих процессов SharePoint Online используется компонент "Служба ретрансляции" служебной шины Microsoft Azure, поэтому за использование служебной шины будет взиматься плата.</span><span class="sxs-lookup"><span data-stu-id="7b471-214">**Note:** SharePoint Online workflow debugging uses the Relay Service component of the Microsoft Azure Service Bus, so you'll be charged for using the Service Bus.</span></span> <span data-ttu-id="7b471-215">См. статью [Часто задаваемые вопросы о служебной шине](http://msdn.microsoft.com/library/hh667438.aspx).</span><span class="sxs-lookup"><span data-stu-id="7b471-215">See  [Service Bus Pricing FAQ](http://msdn.microsoft.com/library/hh667438.aspx).</span></span> <span data-ttu-id="7b471-216">Вы бесплатно получаете доступ к Microsoft Azure в течение каждого месяца подписки на Visual Studio Professional с подпиской MSDN, Visual Studio Premium с подпиской MSDN или Visual Studio Ultimate с подпиской MSDN.</span><span class="sxs-lookup"><span data-stu-id="7b471-216">You get free access to Microsoft Azure each month that you subscribe to Visual Studio Professional with MSDN, Visual Studio Premium with MSDN, or Visual Studio Ultimate with MSDN.</span></span> <span data-ttu-id="7b471-217">При наличии такого доступа вы можете использовать ретрансляцию служебной шины в течение 1500 или 3000 часов (в зависимости от того, какова подписка на MSDN).</span><span class="sxs-lookup"><span data-stu-id="7b471-217">With this access, you can use the Service Bus relay for 1,500, 3,000, or 3,000 hours, depending on your MSDN subscription.</span></span> <span data-ttu-id="7b471-218">Узнайте больше о [доступе к службам Microsoft Azure каждый месяц без дополнительной оплаты](http://www.windowsazure.com/ru-RU/pricing/member-offers/msdn-benefits/).</span><span class="sxs-lookup"><span data-stu-id="7b471-218">See  [Get some amount of Microsoft Azure Services each month at no additional charge](http://www.windowsazure.com/ru-RU/pricing/member-offers/msdn-benefits/).</span></span> 
4. <span data-ttu-id="7b471-219">В Microsoft Azure выберите пространство имен службы, перейдите по ссылке **Ключ доступа**, а затем скопируйте текст из поля **Строка подключения**.</span><span class="sxs-lookup"><span data-stu-id="7b471-219">In Microsoft Azure, choose your service namespace, choose the **Access Key** link, and then copy the text in the **Connection String** box.</span></span>
    
  
5. <span data-ttu-id="7b471-220">На странице свойств проекта Надстройка SharePoint перейдите на вкладку **SharePoint**, а затем установите флажок **Включить отладку рабочего процесса**.</span><span class="sxs-lookup"><span data-stu-id="7b471-220">On the properties page of your SharePoint Add-in project, choose the **SharePoint** tab, and then select the **Enable Workflow debugging** check box.</span></span>
    
    <span data-ttu-id="7b471-p121">Необходимо включить эту функцию, чтобы выполнять отладку рабочих процессов событий в SharePoint Online. Это свойство применяется ко всем проектам SharePoint в Visual Studio. Visual Studio автоматически выключает отладку рабочих процессов при упаковке приложения для отправки в Магазин Office.</span><span class="sxs-lookup"><span data-stu-id="7b471-p121">You must enable this feature to debug workflows in SharePoint Online. This property applies to all of your SharePoint projects in Visual Studio. Visual Studio automatically turns off workflow debugging if you package your app for distribution on the Office store.</span></span>
    
  
6. <span data-ttu-id="7b471-p122">Установите флажок **Включить отладку через шину обслуживания Microsoft Azure**. В поле **Строка подключения шины обслуживания Microsoft Azure** вставьте ранее скопированную строку подключения.</span><span class="sxs-lookup"><span data-stu-id="7b471-p122">Select the **Enable debugging via Microsoft Azure Service Bus** check box. Then, in the **Microsoft Azure Service Bus connection string** box, paste the connection string that you copied.</span></span>
    
  
<span data-ttu-id="7b471-226">Включив отладку рабочих процессов и указав действительную строку подключения для служебной шины Microsoft Azure, вы можете приступить к отладке рабочих процессов SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="7b471-226">After you enable workflow debugging and provide a valid connection string for the Microsoft Azure Service Bus, you can debug SharePoint Online workflows.</span></span>
  
    
    

> <span data-ttu-id="7b471-227">**Примечание.** Если отладка рабочих процессов не включена и вы не хотите получать уведомления в тех случаях, когда проект содержит рабочий процесс, снимите флажок **Уведомлять меня, если отладка шины обслуживания Microsoft Azure не настроена**.</span><span class="sxs-lookup"><span data-stu-id="7b471-227">**Note** If you haven't disabled workflow debugging and don't want to receive a notification whenever your project contains a workflow, clear the **Notify me if Microsoft Azure Service Bus debugging is not configured** check box.</span></span>
  
    
    


## <a name="additional-resources"></a><span data-ttu-id="7b471-228">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="7b471-228">Additional resources</span></span>
<span data-ttu-id="7b471-229"><a name="workflowbk_addres"> </a></span><span class="sxs-lookup"><span data-stu-id="7b471-229"></span></span>

<span data-ttu-id="7b471-p123">Большая часть процесса создания рабочих процессов SharePoint в Visual Studio для разработчика осталась неизменной. Основные разделы документации для SharePoint 2010 сохраняют свою актуальность:</span><span class="sxs-lookup"><span data-stu-id="7b471-p123">A great deal of developing SharePoint workflows remains unchanged for the Visual Studio developer. The key sections of the documentation for SharePoint 2010 remain relevant:</span></span>
  
    
    

- <span data-ttu-id="7b471-232">Сведения об использовании Visual StudioКонструктор рабочих процессов см. в статье  [Обзор конструктора Visual Studio для Windows Workflow Foundation](http://msdn.microsoft.com/ru-RU/library/ms441543.aspx).</span><span class="sxs-lookup"><span data-stu-id="7b471-232">For information about using the Visual StudioWorkflow Designer, see  [Visual Studio Designer for Windows Workflow Foundation Overview](http://msdn.microsoft.com/ru-RU/library/ms441543.aspx).</span></span>
    
  
- <span data-ttu-id="7b471-233">Сведения о создании форм с помощью Microsoft ASP.NET см. в статье  [Общие сведения о формах рабочего процесса](http://msdn.microsoft.com/ru-RU/library/ms457061.aspx).</span><span class="sxs-lookup"><span data-stu-id="7b471-233">For information about creating forms by using Microsoft ASP.NET, see  [Workflow Forms Overview](http://msdn.microsoft.com/ru-RU/library/ms457061.aspx).</span></span>
    
  
- <span data-ttu-id="7b471-234">Сведения об упаковке см. в статье  [Использование компонентов в SharePoint Foundation](http://msdn.microsoft.com/ru-RU/library/ms461324.aspx).</span><span class="sxs-lookup"><span data-stu-id="7b471-234">For information about Feature packaging, see  [Using Features in SharePoint Foundation](http://msdn.microsoft.com/ru-RU/library/ms461324.aspx).</span></span>
    
  
