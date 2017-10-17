---
title: "Новые возможности рабочих процессов для SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 1d51421b-61ac-46b6-a865-52f968ddc5b3
ms.openlocfilehash: d17537f93cd1636e8399d0713801c975f3e7f042
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="whats-new-in-workflows-for-sharepoint"></a><span data-ttu-id="7f68d-102">Новые возможности рабочих процессов для SharePoint</span><span class="sxs-lookup"><span data-stu-id="7f68d-102">What's new in workflows for SharePoint</span></span>
<span data-ttu-id="7f68d-p101">Узнайте о новых возможностях и функциях рабочих процессов в SharePoint. В SharePoint существенно изменилась инфраструктура рабочих процессов. В разделах ниже кратко описаны наиболее важные обновления и улучшения в инфраструктуре рабочих процессов.</span><span class="sxs-lookup"><span data-stu-id="7f68d-p101">Learn about the capabilities and features that are new to workflows in SharePoint. The workflow framework in SharePoint is significantly changed from previous versions. The following sections provide brief summaries of the most significant updates and enhancements to the workflow infrastructure.</span></span>
  
    
    


## <a name="completely-redesigned-workflow-infrastructure"></a><span data-ttu-id="7f68d-106">Полностью обновленная инфраструктура рабочих процессов</span><span class="sxs-lookup"><span data-stu-id="7f68d-106">Completely redesigned workflow infrastructure</span></span>
<span data-ttu-id="7f68d-107"><a name="SP15Whatsnewinworflow_infrastructure"> </a></span><span class="sxs-lookup"><span data-stu-id="7f68d-107"></span></span>

<span data-ttu-id="7f68d-p102">Рабочие процессы SharePoint основаны на платформе Windows Workflow Foundation 4 (WF), которая значительно отличается от предыдущих версий. Платформа Windows Workflow Foundation, в свою очередь, основана на функциональности обмена сообщениями  [Windows Communication Foundation (WCF)](http://msdn.microsoft.com/en-us/netframework/aa663324).</span><span class="sxs-lookup"><span data-stu-id="7f68d-p102">SharePoint workflows are powered by Windows Workflow Foundation 4 (WF), which was substantially redesigned from previous versions. Windows Workflow Foundation, in turn, is built on the messaging functionality that is provided by  [Windows Communication Foundation (WCF)](http://msdn.microsoft.com/en-us/netframework/aa663324).</span></span>
  
    
    
<span data-ttu-id="7f68d-p103">Пожалуй, наиболее характерной особенностью новой инфраструктуры рабочих процессов стало внедрение Microsoft Azure в качестве нового узла выполнения рабочих процессов. Рабочие процессы теперь выполняются за пределами сервера SharePoint  в Microsoft Azure. На рис. 1 представлена обобщенная высокоуровневая схема новой инфраструктуры рабочих процессов. Более подробное описание понятий, представленных на рис. 1, см. в статье  [Основные сведения о рабочих процессах в SharePoint](sharepoint-workflow-fundamentals.md).</span><span class="sxs-lookup"><span data-stu-id="7f68d-p103">Perhaps the most prominent feature of the new workflow infrastructure is the introduction of Microsoft Azure as the new workflow execution host. The workflow execution engine now lives outside of SharePoint, in Microsoft Azure. Figure 1 provides a generalized, high-level view of the new workflow infrastructure. For a more thorough discussion of the concepts presented in Figure 1, see  [SharePoint workflow fundamentals](sharepoint-workflow-fundamentals.md).</span></span>
  
    
    

<span data-ttu-id="7f68d-114">**Рис. 1. Высокоуровневая архитектура инфраструктуры рабочих процессов**</span><span class="sxs-lookup"><span data-stu-id="7f68d-114">**Figure 1. High-level architecture of the workflow infrastructure**</span></span>

  
    
    

  
    
    
![Высокоуровневая архитектура рабочего процесса](../images/wfArchitecture1.png)
  
    
    

  
    
    

  
    
    

## <a name="fully-declarative-no-code-authoring-environment"></a><span data-ttu-id="7f68d-116">Полностью декларативная среда разработки без программного кода</span><span class="sxs-lookup"><span data-stu-id="7f68d-116">Fully declarative, no-code authoring environment</span></span>
<span data-ttu-id="7f68d-117"><a name="SP15Whatsnewinworflow_environment"> </a></span><span class="sxs-lookup"><span data-stu-id="7f68d-117"></span></span>

<span data-ttu-id="7f68d-p104">Другое важное изменение состоит в том, что рабочие процессы на платформе WF 4 являются полностью декларативными. Рабочие процессы больше не компилируются в управляемые сборки и не развертываются в кэш сборок. Вместо этого рабочие процессы и ход их выполнения определяют XAML-файлы.</span><span class="sxs-lookup"><span data-stu-id="7f68d-p104">Another of the prominent changes is that workflows on the WF 4 platform are fully declarative. That is, workflows are no longer compiled into managed assemblies and deployed to an assembly cache. Instead, XAML files define your workflows and frame their execution.</span></span>
  
    
    

## <a name="enhanced-sharepoint-designer-2013-authoring-support"></a><span data-ttu-id="7f68d-121">Улучшены возможности разработки в SharePoint Designer 2013</span><span class="sxs-lookup"><span data-stu-id="7f68d-121">Enhanced SharePoint Designer 2013 authoring support</span></span>
<span data-ttu-id="7f68d-122"><a name="SP15Whatsnewinworflow_SPDauthoring"> </a></span><span class="sxs-lookup"><span data-stu-id="7f68d-122"></span></span>

<span data-ttu-id="7f68d-p105">Мы попытались сделать SharePoint Designer 2013 наилучшей средой для разработки рабочих процессов SharePoint. В SharePoint Designer 2013 представлены рабочая область конструирования и текстовая среда разработки рабочих процессов. Вы можете создавать дополнительные действия рабочих процессов в Visual Studio 2012, а затем импортировать их в SharePoint Designer 2013, где они будут доступны из Конструктор рабочих процессов.</span><span class="sxs-lookup"><span data-stu-id="7f68d-p105">SharePoint Designer 2013 has been updated with the goal of making it the authoring environment of choice for authoring SharePoint workflows. SharePoint Designer 2013 provides workflow authors with both a designer surface and a text-based workflow authoring environment. Additionally, you can develop workflow custom actions in Visual Studio 2012 and then import them into SharePoint Designer 2013, where they can then be accessed from the Workflow Designer.</span></span>
  
    
    
<span data-ttu-id="7f68d-126">Таким образом, в средах разработки рабочих процессов SharePoint учтены потребности как разработчика, так и информационного работника ("опытного пользователя").</span><span class="sxs-lookup"><span data-stu-id="7f68d-126">In short, the needs of both the information worker (the "power user") and the developer have been harnessed in SharePoint workflow authoring and development environments.</span></span>
  
    
    

## <a name="visual-studio-2012-workflow-project-type-support"></a><span data-ttu-id="7f68d-127">Поддержка типов проектов рабочих процессов Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="7f68d-127">Visual Studio 2012 workflow project type support</span></span>
<span data-ttu-id="7f68d-128"><a name="SP15Whatsnewinworflow_VSworkflow"> </a></span><span class="sxs-lookup"><span data-stu-id="7f68d-128"></span></span>

<span data-ttu-id="7f68d-p106">Чтобы упростить взаимодействие информационного работника и разработчика программного обеспечения, в Visual Studio 2012 представлены типы проектов рабочих процессов SharePoint и тип дополнительных действий рабочего процесса. Дополнительные сведения о разработке рабочих процессов с помощью Visual Studio 2012 и различиях между SharePoint Designer 2013 и Visual Studio 2012 см. в статье  [Разработка рабочих процессов в SharePoint с помощью Visual Studio](develop-sharepoint-workflows-using-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="7f68d-p106">To make collaboration easier between information worker and software developer, Visual Studio 2012 provides SharePoint workflow project types and a workflow custom action-item type. For more information about developing workflows by using Visual Studio 2012, and for information about differentiating between SharePoint Designer 2013 and Visual Studio 2012 in workflow development, see  [Develop SharePoint workflows using Visual Studio](develop-sharepoint-workflows-using-visual-studio.md).</span></span>
  
    
    

## <a name="support-for-creating-custom-actions"></a><span data-ttu-id="7f68d-131">Поддержка создания дополнительных действий</span><span class="sxs-lookup"><span data-stu-id="7f68d-131">Support for creating custom actions</span></span>
<span data-ttu-id="7f68d-132"><a name="SP15Whatsnewinworflow_customactions"> </a></span><span class="sxs-lookup"><span data-stu-id="7f68d-132"></span></span>

<span data-ttu-id="7f68d-p107">В SharePoint Designer 2013 и Visual Studio 2012 представлены шаблоны, действия и операции, которые могут понадобиться авторам рабочих процессов. Однако невозможно предугадать, что может понадобиться каждому конкретному пользователю. Поэтому в Visual Studio 2012 доступен настраиваемый тип, который позволяет разработчикам создавать дополнительные действия. Чтобы узнать больше о дополнительных действиях рабочих процессов, см. статью  [Как: построение и развертывание настраиваемого действия рабочего процесса](how-to-build-and-deploy-workflow-custom-actions.md).</span><span class="sxs-lookup"><span data-stu-id="7f68d-p107">A lot of effort has gone into anticipating the business requirements of workflow authors in the providing of workflow templates, actions, and activities in SharePoint Designer 2013 and in Visual Studio 2012. However, we also know that we cannot anticipate each person's specific needs. For this reason, Visual Studio 2012 provides a workflow custom action-item type that lets developers create custom actions. For more information about workflow custom actions, see  [How to: Build and deploy workflow custom actions](how-to-build-and-deploy-workflow-custom-actions.md).</span></span>
  
    
    

## <a name="tools-support-for-sharepoint-workflows"></a><span data-ttu-id="7f68d-137">Поддержка средств для рабочих процессов SharePoint</span><span class="sxs-lookup"><span data-stu-id="7f68d-137">Tools support for SharePoint workflows</span></span>
<span data-ttu-id="7f68d-138"><a name="SP15Whatsnewinworflow_Tools"> </a></span><span class="sxs-lookup"><span data-stu-id="7f68d-138"></span></span>

<span data-ttu-id="7f68d-p108">В Visual Studio 2012 представлены шаблоны и возможность создания рабочих процессов на базе инфраструктуры SharePoint. Рабочие процессы SharePoint похожи на рабочие процессы предыдущих версий за исключением того, что они выполняются в Microsoft Azure на основе платформы WF 4. Кроме того, они являются полностью декларативными (XAML) и предназначены для взаимодействия с облаком и работы с Надстройки SharePoint. Одно из их основных преимуществ состоит в том, что они позволяют удаленно размещать и выполнять рабочие процессы за пределами SharePoint Server.</span><span class="sxs-lookup"><span data-stu-id="7f68d-p108">Visual Studio 2012 provides templates and support for creating workflows on the SharePoint workflow framework. SharePoint workflows are similar to previous versions of workflows except that they are powered by WF 4 and run in Microsoft Azure. They are also declarative-only (XAML) and designed to interact with the cloud and work with SharePoint Add-ins. One of their primary benefits is that they enable you to remotely host and run workflows outside SharePoint Server.</span></span>
  
    
    

## <a name="new-workflow-actions"></a><span data-ttu-id="7f68d-142">Новые действия рабочих процессов</span><span class="sxs-lookup"><span data-stu-id="7f68d-142">New workflow actions</span></span>
<span data-ttu-id="7f68d-143"><a name="SP15Whatsnewinworflow_Newwfactions"> </a></span><span class="sxs-lookup"><span data-stu-id="7f68d-143"></span></span>

<span data-ttu-id="7f68d-p109">Ниже перечислены новые действия рабочих процессов, доступные в SharePoint. Полное описание новых и устаревших действий см. в статье  [Справочник по действий рабочих процессов для SharePoint](workflow-actions-and-activities-reference-for-sharepoint.md). В SharePoint впервые внедрен набор действий рабочих процессов, которые обеспечивают интеграцию с Project 2013 и позволяют создавать рабочие процессы на основе проектов.</span><span class="sxs-lookup"><span data-stu-id="7f68d-p109">Following are new workflow actions that are provided in SharePoint. For a full detailing of both new and deprecated actions, see  [Workflow actions and activities reference for SharePoint](workflow-actions-and-activities-reference-for-sharepoint.md). New to workflows in SharePoint are a set of workflow actions that allow you to integrate with Project 2013 and let you create Project-based workflows.</span></span>
  
    
    

<span data-ttu-id="7f68d-147">**Таблица 1. Новые действия рабочих процессов в SharePoint**</span><span class="sxs-lookup"><span data-stu-id="7f68d-147">**Table 1. New workflow actions in SharePoint**</span></span>


|<span data-ttu-id="7f68d-148">**Действие**</span><span class="sxs-lookup"><span data-stu-id="7f68d-148">**Action**</span></span>|<span data-ttu-id="7f68d-149">**Описание**</span><span class="sxs-lookup"><span data-stu-id="7f68d-149">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="7f68d-150">Назначить задачу</span><span class="sxs-lookup"><span data-stu-id="7f68d-150">Assign a Task</span></span>  <br/> |<span data-ttu-id="7f68d-151">Назначает одну задачу рабочего процесса пользователю или группе.</span><span class="sxs-lookup"><span data-stu-id="7f68d-151">Assigns a single workflow task to a user or group.</span></span>  <br/> |
|<span data-ttu-id="7f68d-152">Начать рабочий процесс</span><span class="sxs-lookup"><span data-stu-id="7f68d-152">Start a Task Process</span></span>  <br/> |<span data-ttu-id="7f68d-153">Инициирует выполнение процесса задачи.</span><span class="sxs-lookup"><span data-stu-id="7f68d-153">Initiates execution of a task process.</span></span>  <br/> |
|<span data-ttu-id="7f68d-154">Перейти к этой стадии</span><span class="sxs-lookup"><span data-stu-id="7f68d-154">Go to This Stage</span></span>  <br/> |<span data-ttu-id="7f68d-155">Определяет следующую стадию рабочего процесса, которой необходимо передать управление потоком.</span><span class="sxs-lookup"><span data-stu-id="7f68d-155">Specifies the next stage in a workflow to which flow control should be handed.</span></span>  <br/> |
|<span data-ttu-id="7f68d-156">Вызов веб-службы HTTP</span><span class="sxs-lookup"><span data-stu-id="7f68d-156">Call HTTP Web Service</span></span>  <br/> |<span data-ttu-id="7f68d-157">Используется для вызова конечной точки REST.</span><span class="sxs-lookup"><span data-stu-id="7f68d-157">Functions as a method call to a Representational State Transfer (REST) endpoint.</span></span>  <br/> |
|<span data-ttu-id="7f68d-158">Начать рабочий процесс списка</span><span class="sxs-lookup"><span data-stu-id="7f68d-158">Start a List Workflow</span></span>  <br/> |<span data-ttu-id="7f68d-159">Запускает рабочий процесс списка.</span><span class="sxs-lookup"><span data-stu-id="7f68d-159">Starts a list-scoped workflow.</span></span>  <br/> |
|<span data-ttu-id="7f68d-160">Начать рабочий процесс сайта</span><span class="sxs-lookup"><span data-stu-id="7f68d-160">Start a Site Workflow</span></span>  <br/> |<span data-ttu-id="7f68d-161">Запускает рабочий процесс сайта.</span><span class="sxs-lookup"><span data-stu-id="7f68d-161">Starts a site-scoped workflow.</span></span>  <br/> |
|<span data-ttu-id="7f68d-162">Построить DynamicValue</span><span class="sxs-lookup"><span data-stu-id="7f68d-162">Build DynamicValue</span></span>  <br/> |<span data-ttu-id="7f68d-163">Создает новую переменную типа **DynamicValue**.</span><span class="sxs-lookup"><span data-stu-id="7f68d-163">Creates a new variable of type **DynamicValue**.</span></span>  <br/> |
|<span data-ttu-id="7f68d-164">Получить свойство из DynamicValue</span><span class="sxs-lookup"><span data-stu-id="7f68d-164">Get Property from DynamicValue</span></span>  <br/> |<span data-ttu-id="7f68d-165">Получает значение свойства из указанной переменной типа **DynamicValue**.</span><span class="sxs-lookup"><span data-stu-id="7f68d-165">Retrieves a property value from a specified variable of type **DynamicValue**.</span></span>  <br/> |
|<span data-ttu-id="7f68d-166">Количество элементов в DynamicValue</span><span class="sxs-lookup"><span data-stu-id="7f68d-166">Count Items in DynamicValue</span></span>  <br/> |<span data-ttu-id="7f68d-167">Возвращает количество строк в переменной типа **DynamicValue**.</span><span class="sxs-lookup"><span data-stu-id="7f68d-167">Returns the number of rows in a variable of type **DynamicValue**.</span></span>  <br/> |
|<span data-ttu-id="7f68d-168">Обрезать строку</span><span class="sxs-lookup"><span data-stu-id="7f68d-168">Trim String</span></span>  <br/> |<span data-ttu-id="7f68d-169">Удаляет все начальные и конечные пробелы из текущей строки.</span><span class="sxs-lookup"><span data-stu-id="7f68d-169">Removes all leading and trailing white-space characters from the current string.</span></span>  <br/> |
|<span data-ttu-id="7f68d-170">Найти подстроку в строке</span><span class="sxs-lookup"><span data-stu-id="7f68d-170">Find Substring in String</span></span>  <br/> |<span data-ttu-id="7f68d-171">Возвращает индекс (отсчет ведется от 1) первого вхождения одного либо нескольких символов или первого вхождения строки (в пределах строки).</span><span class="sxs-lookup"><span data-stu-id="7f68d-171">Returns 1-based index of the first occurrence of one or more characters, or the first occurrence of a string, within a string.</span></span>  <br/> |
|<span data-ttu-id="7f68d-172">Заменить подстроку в строке</span><span class="sxs-lookup"><span data-stu-id="7f68d-172">Replace Substring in String</span></span>  <br/> |<span data-ttu-id="7f68d-173">Возвращает новую строку, в которой все экземпляры указанного символа или строки заменены на другой указанный символ или строку.</span><span class="sxs-lookup"><span data-stu-id="7f68d-173">Returns a new string in which all occurrences of a specified character or string are replaced with another specified character or string.</span></span>  <br/> |
|<span data-ttu-id="7f68d-174">Перевести документ</span><span class="sxs-lookup"><span data-stu-id="7f68d-174">Translate Document</span></span>  <br/> |<span data-ttu-id="7f68d-p110">Используется в качестве оболочки действия HTTP, которое вызывает API синхронного перевода. Необходимо настроить приложение-службу машинного перевода для сайта SharePoint, на котором выполняется рабочий процесс.</span><span class="sxs-lookup"><span data-stu-id="7f68d-p110">Functions as a wrapper around the HTTP activity that calls the synchronous translation API. You must configure a Machine Translation Service Application for the SharePoint site on which you run the workflow.</span></span>  <br/> |
|<span data-ttu-id="7f68d-177">Изменить состояние рабочего процесса</span><span class="sxs-lookup"><span data-stu-id="7f68d-177">Set Workflow Status</span></span>  <br/> |<span data-ttu-id="7f68d-178">Обновляет состояние рабочего процесса, как указано в строке сообщения.</span><span class="sxs-lookup"><span data-stu-id="7f68d-178">Updates workflow status as specified in message string.</span></span>  <br/> |
|<span data-ttu-id="7f68d-179">Создать проект из текущего элемента [Microsoft Project]</span><span class="sxs-lookup"><span data-stu-id="7f68d-179">Create a Project from Current Item [Microsoft Project]</span></span>  <br/> |<span data-ttu-id="7f68d-180">Создает проект Project Server на основе текущего элемента.</span><span class="sxs-lookup"><span data-stu-id="7f68d-180">Creates a Project Server project based on the current item.</span></span>  <br/> |
|<span data-ttu-id="7f68d-181">Задать это значение текущего состояния стадии проекта [Microsoft Project]</span><span class="sxs-lookup"><span data-stu-id="7f68d-181">Set the current project stage status to this value [Microsoft Project]</span></span>  <br/> |<span data-ttu-id="7f68d-182">Задает два поля состояния на текущей стадии проекта.</span><span class="sxs-lookup"><span data-stu-id="7f68d-182">Sets the two status fields within the current stage of the project.</span></span>  <br/> |
|<span data-ttu-id="7f68d-183">Изменить состояние объекта из списка идей на это значение [Microsoft Project]</span><span class="sxs-lookup"><span data-stu-id="7f68d-183">Set the status field in the idea list item to this value [Microsoft Project]</span></span>  <br/> |<span data-ttu-id="7f68d-184">Обновляет поле состояния исходного элемента списка SharePoint.</span><span class="sxs-lookup"><span data-stu-id="7f68d-184">Updates the status field of the original SharePoint list item.</span></span>  <br/> |
|<span data-ttu-id="7f68d-185">Дождаться события проекта [Microsoft Project]</span><span class="sxs-lookup"><span data-stu-id="7f68d-185">Wait for Project Event [Microsoft Project]</span></span>  <br/> |<span data-ttu-id="7f68d-186">Приостанавливает текущий экземпляр рабочего процесса до наступления указанного события проекта: возвращение, выделение, отправление.</span><span class="sxs-lookup"><span data-stu-id="7f68d-186">Pauses the current instance of the workflow to await a specified Project event: Project checked in, Project committed, Project submitted.</span></span>  <br/> |
|<span data-ttu-id="7f68d-187">Присвоить это значение этому полю в проекте [Microsoft Project]</span><span class="sxs-lookup"><span data-stu-id="7f68d-187">Set this field in the project to this value [Microsoft Project]</span></span>  <br/> |<span data-ttu-id="7f68d-188">Задает значение корпоративного настраиваемого поля для указанного проекта.</span><span class="sxs-lookup"><span data-stu-id="7f68d-188">Sets the value for the enterprise custom field for a specified project.</span></span>  <br/> |
   

## <a name="additional-resources"></a><span data-ttu-id="7f68d-189">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="7f68d-189">Additional resources</span></span>
<span data-ttu-id="7f68d-190"><a name="SP15Whatsnewinworflow_Addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="7f68d-190"></span></span>


-  [<span data-ttu-id="7f68d-191">Общие сведения о рабочих процессах в SharePoint</span><span class="sxs-lookup"><span data-stu-id="7f68d-191">Get started with workflows in SharePoint</span></span>](get-started-with-workflows-in-sharepoint.md)
    
  
-  [<span data-ttu-id="7f68d-192">Новые возможности для разработчиков в SharePoint</span><span class="sxs-lookup"><span data-stu-id="7f68d-192">What's new for developers in SharePoint</span></span>](what-s-new-for-developers-in-sharepoint.md)
    
  
-  [<span data-ttu-id="7f68d-193">Справочник по действий рабочих процессов для SharePoint</span><span class="sxs-lookup"><span data-stu-id="7f68d-193">Workflow actions and activities reference for SharePoint</span></span>](workflow-actions-and-activities-reference-for-sharepoint.md)
    
  
-  [<span data-ttu-id="7f68d-194">Краткий справочник по действиям рабочего процесса (платформа рабочих процессов в SharePoint)</span><span class="sxs-lookup"><span data-stu-id="7f68d-194">Workflow actions quick reference (SharePoint Workflow platform)</span></span>](workflow-actions-quick-reference-sharepoint-workflow-platform.md)
    
  

