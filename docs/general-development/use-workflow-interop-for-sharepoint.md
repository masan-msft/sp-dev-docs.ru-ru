---
title: "Использование средств взаимодействия рабочих процессов для SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 3da21b5ba12d0e2b463a3e1a8b5807cd8a597862
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="use-workflow-interop-for-sharepoint"></a><span data-ttu-id="48752-102">Использование средств взаимодействия рабочих процессов для SharePoint</span><span class="sxs-lookup"><span data-stu-id="48752-102">Use workflow interop for SharePoint</span></span>
<span data-ttu-id="48752-103">Предоставляет сведения об использовании средств взаимодействия рабочих процессов SharePoint в конструкторе рабочих процессов Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="48752-103">Provides a discussion of using SharePoint workflow Interop in the Visual Studio 2012 workflow designer.</span></span> <span data-ttu-id="48752-104">Рабочий процесс взаимодействия позволяет выполнять рабочего процесса SharePoint 2010 из рабочего процесса SharePoint.</span><span class="sxs-lookup"><span data-stu-id="48752-104">Workflow interop allows you to invoke a SharePoint 2010 workflow from within a SharePoint workflow.</span></span> <span data-ttu-id="48752-105">Это является важной функцией, которая позволяет повторно использовать существующие компоненты рабочих процессов и вызвать для действий рабочего процесса, не встроенные в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="48752-105">This is an important feature that allows you to reuse existing workflow features, and to call on workflow activities that are not integrated into SharePoint.</span></span>

  
    
    


> <span data-ttu-id="48752-106">**Важные:** Чтобы узнать, как использовать функции взаимодействия SharePoint рабочего процесса в SharePoint Designer 2013, просмотрите [действия по координации общее представление о в SharePoint Designer 2013](understanding-coordination-actions-in-sharepoint-designer.md).</span><span class="sxs-lookup"><span data-stu-id="48752-106">**Important:** To learn about using SharePoint workflow interop functionality in SharePoint Designer 2013, see  [Understanding Coordination actions in SharePoint Designer 2013](understanding-coordination-actions-in-sharepoint-designer.md).</span></span> 
  
    
    


## <a name="sharepoint-workflow-interop"></a><span data-ttu-id="48752-107">Взаимодействие рабочих процессов SharePoint</span><span class="sxs-lookup"><span data-stu-id="48752-107">SharePoint workflow interop</span></span>
<span data-ttu-id="48752-108"><a name="bkm_interop"> </a></span><span class="sxs-lookup"><span data-stu-id="48752-108"></span></span>

<span data-ttu-id="48752-109">Вот проблемы.</span><span class="sxs-lookup"><span data-stu-id="48752-109">Here's the problem.</span></span> <span data-ttu-id="48752-110">У вас есть устаревших рабочих процессов SharePoint 2010, которые необходимо повторно использовать платформы SharePoint.</span><span class="sxs-lookup"><span data-stu-id="48752-110">You have legacy SharePoint 2010 workflows that you wish to reuse on your SharePoint platform.</span></span> <span data-ttu-id="48752-111">Или, того, вы создаете новые рабочие процессы SharePoint и необходимые для вызова действия, которые доступны только в платформе SharePoint 2010.</span><span class="sxs-lookup"><span data-stu-id="48752-111">Or, worse, you are creating new SharePoint workflows and you need to invoke activities that are only available in the SharePoint 2010 platform.</span></span> <span data-ttu-id="48752-112">И вы не знаете, что делать.</span><span class="sxs-lookup"><span data-stu-id="48752-112">And you don't know what to do.</span></span> <span data-ttu-id="48752-113">На самом деле, простое решение: использование рабочего процесса SharePoint взаимодействия.</span><span class="sxs-lookup"><span data-stu-id="48752-113">Actually, the solution is simple: use SharePoint workflow Interop.</span></span>
  
    
    
<span data-ttu-id="48752-114">Для нормальной работы с модуля рабочего процесса SharePoint, который основан на Windows Workflow Foundation 4 взаимодействия рабочих процессов SharePoint позволяет рабочих процессов SharePoint 2010 (основан на Windows Workflow Foundation 3).</span><span class="sxs-lookup"><span data-stu-id="48752-114">SharePoint workflow interop enables SharePoint 2010 workflows (built on Windows Workflow Foundation 3) to work smoothly with the SharePoint workflow engine, which is based on Windows Workflow Foundation 4.</span></span> <span data-ttu-id="48752-115">Хотя новый модуль выполнения Windows Workflow Foundation 4 размещается в диспетчер рабочих процессов, который используется в качестве внешней службы SharePoint по-прежнему содержит прежних версий узла рабочего процесса SharePoint, который используется для обработки рабочих процессов SharePoint 2010.</span><span class="sxs-lookup"><span data-stu-id="48752-115">While the new Windows Workflow Foundation 4 execution engine is hosted in Workflow Manager, which runs as an external service, SharePoint still contains the legacy SharePoint workflow host which it uses to process SharePoint 2010 workflows.</span></span> <span data-ttu-id="48752-116">Взаимодействие рабочих процессов SharePoint согласует среды выполнения двух, как показано на рисунке 1.</span><span class="sxs-lookup"><span data-stu-id="48752-116">SharePoint workflow interop negotiates the two execution environments, as depicted in Figure 1.</span></span>
  
    
    

<span data-ttu-id="48752-117">**На рисунке 1. Взаимодействие рабочих процессов SharePoint в действии**</span><span class="sxs-lookup"><span data-stu-id="48752-117">**Figure 1. SharePoint workflow interop in action**</span></span>

  
    
    

  
    
    
![Мост межпрограммного взаимодействия с рабочим процессом](../images/wfInteropBridge.png)
  
    
    
<span data-ttu-id="48752-p104">Рассмотрим процесс показано на рисунке 1. Используйте буквы в поиске точек особое внимание на рисунке:</span><span class="sxs-lookup"><span data-stu-id="48752-p104">Let's walk through the process depicted in Figure 1. Use the letters to reference points of emphasis in the illustration:</span></span>
  
    
    


  
    
    
> <span data-ttu-id="48752-121">Запускает ( **A** ) экземпляр рабочего процесса SharePoint для запуска диспетчера рабочих процессов нажмите на основе Windows Workflow Foundation 4.</span><span class="sxs-lookup"><span data-stu-id="48752-121">( **A** ) An instance of a SharePoint workflow starts to run in then Windows Workflow Foundation 4-based Workflow Manager.</span></span> <span data-ttu-id="48752-122">Обратите внимание на то, что диспетчер рабочих процессов не входит в SharePoint, но вместо этого используется в качестве внешней службы.</span><span class="sxs-lookup"><span data-stu-id="48752-122">Note that the Workflow Manager is not in SharePoint, but instead runs as an external service.</span></span>
    
  

  
    
    
> <span data-ttu-id="48752-123">( **Б** ) достижении точки в рабочий процесс SharePoint — номер этапа 3 в диспетчер рабочих процессов - которой вы хотите вызвать рабочего процесса SharePoint 2010.</span><span class="sxs-lookup"><span data-stu-id="48752-123">( **B** ) You reach a point in the SharePoint workflow - step number 3 in the Workflow Manager - where you wish to invoke a SharePoint 2010 workflow.</span></span> <span data-ttu-id="48752-124">В конструкторе рабочих процессов Visual Studio 2012 это делается при помощи действия **WF 2010 Пуск** , как показано на рисунке 2.</span><span class="sxs-lookup"><span data-stu-id="48752-124">In the Visual Studio 2012 workflow designer, you do this by implementing the **Start 2010 WF** activity, as shown in Figure 2.</span></span>
    
   <span data-ttu-id="48752-125">**На рисунке 2. Плитка "Стадия" для запуска рабочего процесса SharePoint 2010.**</span><span class="sxs-lookup"><span data-stu-id="48752-125">**Figure 2. Stage tile for starting a SharePoint 2010 workflow.**</span></span>

  

  ![Запуск рабочего процесса 2010](../images/wfInterop_Stage1.png)
  

    
    
    From the perspective of the SharePoint object model, this is accomplished using the  [StartWorkflow](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowInteropService.StartWorkflow.aspx) method on the [WorkflowInteropService](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowInteropService.aspx) class.
    
  

  
    
    
> <span data-ttu-id="48752-p107">( **C** ) на этом этапе рабочего процесса SharePoint 2010 начинает выполнение в узле Windows Workflow Foundation 3,5 рабочего процесса в SharePoint. Однако включается особое внимание. В некоторых случаях вы можете 2013 рабочего процесса, чтобы ожидать в рабочий процесс 2010 для завершения работы (и может быть возвращены некоторые данные) перед тем как продолжить выполнение рабочего процесса 2013. В других сценариях это может быть не требуется и оба рабочие процессы могут выполняться независимо, параллельно.</span><span class="sxs-lookup"><span data-stu-id="48752-p107">( **C** ) At this point, the SharePoint 2010 workflow begins executing in the Windows Workflow Foundation 3.5 workflow host inside of SharePoint. But an important consideration comes up. In some scenarios you may want the 2013 workflow to wait for the 2010 workflow to complete running (and perhaps return some data) before continuing to execute the 2013 workflow. In other scenarios, this may not be necessary and both workflows may run independently, in parallel.</span></span>
    
    To control this behavior, the  [WorkflowInterop](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.Activities.WorkflowInterop.aspx) class, which controls executing workflows in the Windows Workflow Foundation 3.5 workflow host, provides a [Wait](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.Activities.WorkflowInterop.Wait.aspx) property. Setting this Boolean property to " **Yes**" (in the designer dialog box) or to **true** in the on the **Wait** property, causes the 2013 workflow to pause until the 2010 finished executing and returns a **completed** message.
    
    
    

   <span data-ttu-id="48752-131">**На рисунке 3. Запустите диалоговое окно свойств рабочего процесса.**</span><span class="sxs-lookup"><span data-stu-id="48752-131">**Figure 3. Start a Workflow properties dialog box.**</span></span>

  

  ![Установка свойств для действия "Запустить рабочий процесс"](../images/wfInterop_.png)
  

  

  

  
    
    
> <span data-ttu-id="48752-p108">Здесь приведен ( **D** ) приводит к практическим результатам по выбору **true** или **false** на **Wait** свойство (или **Да** или **Нет** в диалоговом окне Свойства). Если **Wait** **true**, затем рабочий процесс 2010 передает событие  [WorkflowCompleted](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowInteropEventReceiver.WorkflowCompleted.aspx) (и, при необходимости, возвращает данные в качестве свойства [DynamicValue](http://msdn.microsoft.com/library/2af7983b-8357-4e0f-9ba9-dfdeed05a8a7.aspx) ). Дополнительные сведения о динамических значения можно [Understanding Dynamic Value](http://msdn.microsoft.com/library/c5702628-9625-4d19-95c5-13923e91fea1.aspx).</span><span class="sxs-lookup"><span data-stu-id="48752-p108">( **D** ) The practical effect of selecting **true** or **false** on the **Wait** property (or **Yes** or **No** in the properties dialog box) is depicted here. If **Wait** is **true**, then the 2010 workflow passes a  [WorkflowCompleted](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowInteropEventReceiver.WorkflowCompleted.aspx) event (and, optionally, returns data as a [DynamicValue](http://msdn.microsoft.com/library/2af7983b-8357-4e0f-9ba9-dfdeed05a8a7.aspx) property). For more information about dynamic values, see [Understanding Dynamic Value](http://msdn.microsoft.com/library/c5702628-9625-4d19-95c5-13923e91fea1.aspx).</span></span>
    
    Of course, if **Wait** is set to **false**, then your 2010 workflow executes, then terminates normally.
    
  

  
    
    
> <span data-ttu-id="48752-p109">( **E** ) этот шаг применяется только в том случае, если ваше вызова рабочего процесса 2010 указан **Wait=true**. В этом случае 2013 workflow получил событие **WorkflowCompleted** и перезапускает выполнение 2013 рабочего процесса на то, что оно было остановлено.</span><span class="sxs-lookup"><span data-stu-id="48752-p109">( **E** ) This step is only relevant if your invocation of the 2010 workflow specified **Wait=true**. In that case, your 2013 workflow received the **WorkflowCompleted** event and restarts the workflow 2013 execution at the point it left off.</span></span>
    
  

  
    
    
> <span data-ttu-id="48752-p110">Затем ( **F** ) 2013 workflow завершает выполнение и завершается. Если **Wait=false**, затем рабочий процесс 2013 выполняет и завершает независимо от рабочего процесса 2010.</span><span class="sxs-lookup"><span data-stu-id="48752-p110">( **F** ) Your 2013 workflow then completes execution and terminates normally. If **Wait=false**, then your 2013 workflow executes and terminates independently of the 2010 workflow.</span></span> 
    
  

## <a name="workflow-interop-design"></a><span data-ttu-id="48752-140">Взаимодействия разработки рабочего процесса</span><span class="sxs-lookup"><span data-stu-id="48752-140">Workflow interop design</span></span>
<span data-ttu-id="48752-141"><a name="bkm_interopDesign"> </a></span><span class="sxs-lookup"><span data-stu-id="48752-141"></span></span>

<span data-ttu-id="48752-p111">Взаимодействия рабочих процессов SharePoint  это платформа обмена сообщениями, которое поддерживает один к одному экземпляру сопоставление действий рабочих процессов WF 3 и WF 4. WF 3 и WF 4 взаимодействовать через обмена сообщениями, реализуемые пространством набора действий WF 4 на  [WorkflowInteropService](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowInteropService.aspx) .</span><span class="sxs-lookup"><span data-stu-id="48752-p111">SharePoint workflow interop is a messaging framework that supports a one-to-one instance mapping between WF 3 and WF 4 workflow activities. WF 3 and WF 4 interoperate through message exchanges that are wrapped by a set of WF 4 activities on  [WorkflowInteropService](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowInteropService.aspx) .</span></span>
  
    
    
<span data-ttu-id="48752-p112">Для поддержки взаимодействия рабочих процессов, конструирования рабочего процесса в SharePoint Designer предоставляет доступ к нового действия рабочих процессов **WF 2010 Пуск**, который является оболочкой для метода  [StartWorkflow](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowInteropService.StartWorkflow.aspx) . Это действие позволяет запустить рабочий процесс списка или рабочий процесс сайта.</span><span class="sxs-lookup"><span data-stu-id="48752-p112">To support workflow interop, the workflow design surface in SharePoint Designer provides access to a new workflow activity, **Start 2010 WF**, which is a wrapper on the  [StartWorkflow](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowInteropService.StartWorkflow.aspx) method. This activity allows you to start either a list workflow or a site workflow.</span></span>
  
    
    
<span data-ttu-id="48752-146">Действия на самом деле — это последовательность сообщений, которые происходят между диспетчера рабочих процессов и узел рабочего процесса SharePoint 2010, на котором работает внутри SharePoint.</span><span class="sxs-lookup"><span data-stu-id="48752-146">The activity is in fact a sequence of messages that take place between the Workflow Manager and the SharePoint 2010 Workflow Host that is running inside SharePoint.</span></span> <span data-ttu-id="48752-147">Эти два являются посредством уровень обмена сообщениями, как показано на рисунке 4.</span><span class="sxs-lookup"><span data-stu-id="48752-147">These two are mediated by a messaging layer, as shown in Figure 4.</span></span> <span data-ttu-id="48752-148">Последовательность начинается в диспетчер рабочих процессов SharePoint с помощью вызова метода **StartWorkflow** .</span><span class="sxs-lookup"><span data-stu-id="48752-148">The sequence begins in the SharePoint workflow manager with an invocation of the **StartWorkflow** method.</span></span> <span data-ttu-id="48752-149">Сообщение «Пуск» переходит в службе рабочих процессов в SharePoint, где в свою очередь запускает рабочий процесс внутри узла рабочего процесса SharePoint 2010.</span><span class="sxs-lookup"><span data-stu-id="48752-149">The "start" message goes to the workflow service inside of SharePoint, where in turn it launches the workflow inside the SharePoint 2010 workflow host.</span></span> <span data-ttu-id="48752-150">По завершении выполнения рабочего процесса 2010 происходит событие, которое отправляет сообщение «завершенная» с помощью publisher события диспетчера рабочих процессов 2013.</span><span class="sxs-lookup"><span data-stu-id="48752-150">When execution of the 2010 workflow is complete, an event is fired that sends a "completed" message through the event publisher back to the 2013 workflow manager.</span></span>
  
    
    

<span data-ttu-id="48752-151">**На рисунке 4. Протокол взаимодействия обмена сообщениями рабочего процесса SharePoint**</span><span class="sxs-lookup"><span data-stu-id="48752-151">**Figure 4. SharePoint workflow interop messaging protocol**</span></span>

  
    
    

  
    
    
![Обмен сообщениями межпрограммного взаимодействия с рабочим процессом](../images/wfInteropMessaging.png)
  
    
    

  
    
    

  
    
    

## <a name="additional-resources"></a><span data-ttu-id="48752-153">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="48752-153">Additional resources</span></span>
<span data-ttu-id="48752-154"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="48752-154"></span></span>


-  [<span data-ttu-id="48752-155">Общие сведения о рабочих процессах в SharePoint</span><span class="sxs-lookup"><span data-stu-id="48752-155">Get started with workflows in SharePoint</span></span>](get-started-with-workflows-in-sharepoint.md)
    
  
-  [<span data-ttu-id="48752-156">Основные сведения о рабочих процессах в SharePoint</span><span class="sxs-lookup"><span data-stu-id="48752-156">SharePoint workflow fundamentals</span></span>](sharepoint-workflow-fundamentals.md)
    
  
-  [<span data-ttu-id="48752-157">Общие сведения о действия по координации в SharePoint Designer 2013</span><span class="sxs-lookup"><span data-stu-id="48752-157">Understanding Coordination actions in SharePoint Designer 2013</span></span>](understanding-coordination-actions-in-sharepoint-designer.md)
    
  
-  [<span data-ttu-id="48752-158">WorkflowInteropService</span><span class="sxs-lookup"><span data-stu-id="48752-158">WorkflowInteropService</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowInteropService.aspx)
    
  
-  [<span data-ttu-id="48752-159">WorkflowInteropEventReceiver</span><span class="sxs-lookup"><span data-stu-id="48752-159">WorkflowInteropEventReceiver</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowInteropEventReceiver.aspx)
    
  

  
    
    

