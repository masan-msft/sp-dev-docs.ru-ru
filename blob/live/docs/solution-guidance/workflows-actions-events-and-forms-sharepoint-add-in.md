---
title: "Рабочие процессы, действия (действия), события и форм в объектная модель SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: d20da3810fc6c6f0cc32eda185ec7cfd45d1f607
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
<a name="workflows-actions-activities-events-and-forms-in-the-sharepoint-add-in-model"></a><span data-ttu-id="2ee5e-102">Рабочие процессы, действия (действия), события и форм в объектная модель SharePoint</span><span class="sxs-lookup"><span data-stu-id="2ee5e-102">Workflows, actions (activities), events, and forms in the SharePoint add-in model</span></span>
=================================================================================

<a name="summary"></a><span data-ttu-id="2ee5e-103">Summary</span><span class="sxs-lookup"><span data-stu-id="2ee5e-103">Summary</span></span>
-------

<span data-ttu-id="2ee5e-104">Выбор подхода к реализации рабочих процессов и их связанные компоненты отличается новой модели надстройки SharePoint от был с кодом полного доверия.</span><span class="sxs-lookup"><span data-stu-id="2ee5e-104">The approach you take to implement workflows and their associated components is different in the new SharePoint Add-in model than it was with Full Trust Code.</span></span>  <span data-ttu-id="2ee5e-105">В типичных полного доверия кода (FTC) / сценарий решения фермы, рабочие процессы и их связанных компонентов, разработанных с помощью кода на стороне сервера и развернуты через решений SharePoint.</span><span class="sxs-lookup"><span data-stu-id="2ee5e-105">In a typical Full Trust Code (FTC) / Farm Solution scenario, workflows and their associated components were built with server side code and deployed via SharePoint Solutions.</span></span>  <span data-ttu-id="2ee5e-106">Рабочие процессы и их связанных компонентов выполнялись на сервере SharePoint.</span><span class="sxs-lookup"><span data-stu-id="2ee5e-106">The workflows and their associated components ran on the SharePoint server.</span></span>

<span data-ttu-id="2ee5e-107">В SharePoint надстройки модели сценарии рабочие процессы и их связанных компонентов разработанных с помощью кода, который выполняется на удаленных серверах.</span><span class="sxs-lookup"><span data-stu-id="2ee5e-107">In an SharePoint Add-in model scenario, workflows and their associated components are developed with code that runs on remote servers.</span></span>  <span data-ttu-id="2ee5e-108">Зарегистрированные рабочие процессы и их компоненты, связанные со службой рабочего процесса, но весь код выполняется на удаленных серверах.</span><span class="sxs-lookup"><span data-stu-id="2ee5e-108">Workflows and their associated components are registered with the Workflow Service, but all code executes on remote servers.</span></span>

<a name="high-level-guidelines"></a><span data-ttu-id="2ee5e-109">Рекомендации по высокого уровня</span><span class="sxs-lookup"><span data-stu-id="2ee5e-109">High Level Guidelines</span></span>
---------------------

<span data-ttu-id="2ee5e-110">Как правило эскиз мы хотели бы предоставить со следующими рекомендациями высокого уровня для создания рабочих процессов и их связанных компонентов в новой модели надстройки SharePoint.</span><span class="sxs-lookup"><span data-stu-id="2ee5e-110">As a rule of a thumb, we would like to provide the following high level guidelines for creating workflows and their associated components in the new SharePoint Add-in model.</span></span>

- <span data-ttu-id="2ee5e-111">Код рабочие процессы, недоступны в Office 365 клиенты или с помощью модели надстройки SharePoint в целом.</span><span class="sxs-lookup"><span data-stu-id="2ee5e-111">Code behind workflows are not available in Office 365 tenancies, or with the SharePoint Add-in model in general.</span></span>
- <span data-ttu-id="2ee5e-112">Фоновый код все связанные с рабочими процессами и их связанные компоненты должны быть расположены в внешние веб-службы, запущенные на удаленном сервере.</span><span class="sxs-lookup"><span data-stu-id="2ee5e-112">All code behind associated with workflows and their associated components must be placed in an external web service running on a remote server.</span></span>

<a name="options-to-create-custom-workflows-and-their-associated-components"></a><span data-ttu-id="2ee5e-113">Параметры для создания настраиваемых рабочих процессов и их связанные компоненты</span><span class="sxs-lookup"><span data-stu-id="2ee5e-113">Options to create custom workflows and their associated components</span></span>
------------------------------------------------------------------
<span data-ttu-id="2ee5e-114">У вас есть несколько вариантов для создания настраиваемых рабочих процессов и их связанных компонентов.</span><span class="sxs-lookup"><span data-stu-id="2ee5e-114">You have a few options to create custom workflows and their associated components.</span></span>

- <span data-ttu-id="2ee5e-115">Создание настраиваемых рабочих процессов</span><span class="sxs-lookup"><span data-stu-id="2ee5e-115">Create custom workflows</span></span>
- <span data-ttu-id="2ee5e-116">Создайте настраиваемые действия рабочего процесса</span><span class="sxs-lookup"><span data-stu-id="2ee5e-116">Create custom workflow activities</span></span>
- <span data-ttu-id="2ee5e-117">Создание настраиваемого рабочего процесса событий</span><span class="sxs-lookup"><span data-stu-id="2ee5e-117">Create custom workflow events</span></span>
- <span data-ttu-id="2ee5e-118">Создание форм настраиваемых рабочих процессов</span><span class="sxs-lookup"><span data-stu-id="2ee5e-118">Create custom workflow forms</span></span>

<a name="create-custom-workflows"></a><span data-ttu-id="2ee5e-119">Создание настраиваемых рабочих процессов</span><span class="sxs-lookup"><span data-stu-id="2ee5e-119">Create custom workflows</span></span>
-----------------------
<span data-ttu-id="2ee5e-120">В этот параметр, настраиваемых рабочих процессов создания, развертывания и связанных с веб узла в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="2ee5e-120">In this option custom workflows are created, deployed, and associated with the Host-web in SharePoint.</span></span>

- <span data-ttu-id="2ee5e-121">Настраиваемые рабочие процессы могут создаваться с использованием Visual Studio или SharePoint Designer.</span><span class="sxs-lookup"><span data-stu-id="2ee5e-121">Custom workflows may be created with Visual Studio or SharePoint Designer.</span></span>
    + <span data-ttu-id="2ee5e-122">В разделе [Разработка SharePoint 2013 рабочих процессов с помощью Visual Studio (статья MSDN)](https://msdn.microsoft.com/en-us/library/office/jj163199.aspx) , который приводится сводка оба параметры и рассматриваются преимущества и недостатки каждого из них.</span><span class="sxs-lookup"><span data-stu-id="2ee5e-122">See the [Develop SharePoint 2013 workflows using Visual Studio (MSDN Article)](https://msdn.microsoft.com/en-us/library/office/jj163199.aspx) that summarizes both options and discusses the advantages and disadvantages of each.</span></span>
- <span data-ttu-id="2ee5e-123">Настраиваемые рабочие процессы могут развернуть и связанных с веб узла в SharePoint несколькими способами.</span><span class="sxs-lookup"><span data-stu-id="2ee5e-123">Custom workflows may be deployed and associated with the Host-web in SharePoint in several ways.</span></span>
    - <span data-ttu-id="2ee5e-124">Рабочие процессы, созданные в Visual Studio автоматически упакованных внутри возможности развертывания.</span><span class="sxs-lookup"><span data-stu-id="2ee5e-124">Workflows created in Visual Studio are automatically packaged inside features for deployment.</span></span>
    - <span data-ttu-id="2ee5e-125">Создания рабочих процессов в SharePoint designer необходимо экспортировать и импортировать их развертывания на сервере разработки на сервер приложений.</span><span class="sxs-lookup"><span data-stu-id="2ee5e-125">Workflows created in SharePoint designer must be exported and imported to deploy them from a development server to a production server.</span></span>
    - <span data-ttu-id="2ee5e-126">Рабочие процессы могут развернуть и связанных с веб узла в SharePoint с помощью удаленного подготовки шаблон.</span><span class="sxs-lookup"><span data-stu-id="2ee5e-126">Workflows may also be deployed and associated with the Host-web in SharePoint via the remote provisioning pattern.</span></span>  <span data-ttu-id="2ee5e-127">В разделе [подготовки сайта (добавить в SharePoint набора команд)](site-provisioning-sharepoint-add-in.md) для получения дополнительных сведений о шаблоне удаленного подготовки.</span><span class="sxs-lookup"><span data-stu-id="2ee5e-127">See the [Site provisioning (SharePoint Add-in Recipe)](site-provisioning-sharepoint-add-in.md) for more details about the remote provisioning pattern.</span></span>

<span data-ttu-id="2ee5e-128">В следующем примере кода показано, как использовать CSOM для подготовки рабочего процесса и списки, поддерживающие рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="2ee5e-128">The following code sample demonstrates how to use CSOM to provision a workflow and the lists which support the workflow.</span></span>

    public void ProvisionIncidentWorkflowAndRelatedLists(string incidentWorkflowFile, string suiteLevelWebAppUrl, string dispatcherName)
    {
        //Return the list the workflow will be associated with
        var incidentsList = CSOMUtil.GetListByTitle(clientContext, "Incidents");

        //Create a new WorkflowProvisionService class instance which uses the 
        //Microsoft.SharePoint.Client.WorkflowServices.WorkflowServicesManager to
        //provision and configure workflows
        var service = new WorkflowProvisionService(clientContext);

        //Read the workflow .XAML file
        var incidentWF = System.IO.File.ReadAllText(incidentWorkflowFile);

        //Create the WorkflowDefinition and use the 
        //Microsoft.SharePoint.Client.WorkflowServices.WorkflowServicesManager
        //to save and publish it.  
        //This method is shown below for reference.
        var incidentWFDefinitionId = service.SaveDefinitionAndPublish("Incident",
            WorkflowUtil.TranslateWorkflow(incidentWF));

        //Create the workflow tasks list
        var taskListId = service.CreateTaskList("Incident Workflow Tasks");

        //Create the workflow history list
        var historyListId = service.CreateHistoryList("Incident Workflow History");

        //Use the Microsoft.SharePoint.Client.WorkflowServices.WorkflowSubscriptionService to 
        //subscibe the workflow to the list the workflow is associated with, register the
        //events it is associated with, and register the tasks and history list. 
        //This method is shown below for reference.
        service.Subscribe("Incident Workflow", incidentWFDefinitionId, incidentsList.Id,
            WorkflowSubscritpionEventType.ItemAdded, taskListId, historyListId);
    }
    
    public Guid SaveDefinitionAndPublish(string name, string translatedWorkflows)
    {
        var definition = new WorkflowDefinition(ClientContext)
        {
            DisplayName = name,
            Xaml = translatedWorkflows
        };

        var deploymentService = workflowServicesManager.GetWorkflowDeploymentService();
        var result = deploymentService.SaveDefinition(definition);
        ClientContext.ExecuteQuery();

        deploymentService.PublishDefinition(result.Value);
        ClientContext.ExecuteQuery();

        return result.Value;
    }

    public Guid Subscribe(string name, Guid definitionId, Guid targetListId, WorkflowSubscritpionEventType eventTypes, Guid taskListId, Guid historyListId)
    {
        var eventTypesList = new List<string>();
        foreach (WorkflowSubscritpionEventType type in Enum.GetValues(typeof(WorkflowSubscritpionEventType)))
        {
            if ((type & eventTypes) > 0)
                eventTypesList.Add(type.ToString());
        }

        var subscription = new WorkflowSubscription(ClientContext)
        {
            Name = name,
            Enabled = true,
            DefinitionId = definitionId,
            EventSourceId = targetListId,
            EventTypes = eventTypesList.ToArray()
        };

        subscription.SetProperty("TaskListId", taskListId.ToString());
        subscription.SetProperty("HistoryListId", historyListId.ToString());

        var subscriptionService = workflowServicesManager.GetWorkflowSubscriptionService();
        var result = subscriptionService.PublishSubscriptionForList(subscription, targetListId);

        ClientContext.ExecuteQuery();
        return result.Value;
    }

<span data-ttu-id="2ee5e-129">**Когда это подходит?**</span><span class="sxs-lookup"><span data-stu-id="2ee5e-129">**When is it a good fit?**</span></span>

<span data-ttu-id="2ee5e-130">При необходимости для создания настраиваемых рабочих процессов с ним код, этот параметр, — это хорошо подходит.</span><span class="sxs-lookup"><span data-stu-id="2ee5e-130">When you need to create custom workflows with code behind them this option is a good fit.</span></span>

<span data-ttu-id="2ee5e-131">**Приступая к работе**</span><span class="sxs-lookup"><span data-stu-id="2ee5e-131">**Getting Started**</span></span>

<span data-ttu-id="2ee5e-132">Следующие статьи приведены инструкции для создания настраиваемых рабочих процессов.</span><span class="sxs-lookup"><span data-stu-id="2ee5e-132">The following articles demonstrate how to create custom workflows.</span></span>

- [<span data-ttu-id="2ee5e-133">Создание приложения рабочего процесса SharePoint с помощью Visual Studio 2012 г. (статья MSDN)</span><span class="sxs-lookup"><span data-stu-id="2ee5e-133">Create a SharePoint workflow app using Visual Studio 2012 (MSDN Article)</span></span>](https://msdn.microsoft.com/EN-US/library/office/dn456545.aspx)
- [<span data-ttu-id="2ee5e-134">Как: создание рабочих процессов SharePoint 2013 с помощью Visual Studio (статья MSDN)</span><span class="sxs-lookup"><span data-stu-id="2ee5e-134">How to: Create SharePoint 2013 Workflows using Visual Studio (MSDN Article)</span></span>](https://msdn.microsoft.com/EN-US/library/office/dn584771.aspx)

<a name="create-custom-workflow-activities"></a><span data-ttu-id="2ee5e-135">Создайте настраиваемые действия рабочего процесса</span><span class="sxs-lookup"><span data-stu-id="2ee5e-135">Create custom workflow activities</span></span>
---------------------------------
<span data-ttu-id="2ee5e-136">В этот параметр, настраиваемые действия рабочего процесса создан и развернут в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="2ee5e-136">In this option custom workflow activities are created and deployed to SharePoint.</span></span>

- <span data-ttu-id="2ee5e-137">Настраиваемые действия рабочего процесса могут быть созданы с помощью Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2ee5e-137">Custom workflow activities may be created with Visual Studio.</span></span>
- <span data-ttu-id="2ee5e-138">Настраиваемые действия рабочего процесса может быть создан с помощью SharePoint Designer.</span><span class="sxs-lookup"><span data-stu-id="2ee5e-138">Custom workflow activities may not be created with SharePoint Designer.</span></span>
- <span data-ttu-id="2ee5e-139">Настраиваемые действия рабочего процесса могут быть использованы в SharePoint Designer, после развертывания в среде SharePoint.</span><span class="sxs-lookup"><span data-stu-id="2ee5e-139">Custom workflow activities may be used in SharePoint Designer after they are deployed to a SharePoint environment.</span></span>

<span data-ttu-id="2ee5e-140">**Когда это подходит?**</span><span class="sxs-lookup"><span data-stu-id="2ee5e-140">**When is it a good fit?**</span></span>

<span data-ttu-id="2ee5e-141">Когда следует реализовать рабочих процессов в бизнес-процессов путем ожидания введите библиотека действий рабочих процессов в SharePoint Designer не выполняются, требования к</span><span class="sxs-lookup"><span data-stu-id="2ee5e-141">When you need to implement workflows in business processes whose requirements are not met by the out-of-the-box library of workflow actions in SharePoint Designer</span></span>

<span data-ttu-id="2ee5e-142">**Приступая к работе**</span><span class="sxs-lookup"><span data-stu-id="2ee5e-142">**Getting Started**</span></span>

<span data-ttu-id="2ee5e-143">Следующей статье демонстрируется создание действий настраиваемого рабочего процесса с помощью Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2ee5e-143">The following article demonstrates how to create a custom workflow activity with Visual Studio.</span></span>

- [<span data-ttu-id="2ee5e-144">Как: построение и развертывание настраиваемого действия рабочего процесса (статья MSDN)</span><span class="sxs-lookup"><span data-stu-id="2ee5e-144">How to: Build and deploy workflow custom actions (MSDN Article)</span></span>](https://msdn.microsoft.com/en-us/library/office/jj163911.aspx)

<span data-ttu-id="2ee5e-145">[Workflow.Activities (O365 PnP образец)](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.Activities) включает в себя несколько действий настраиваемого рабочего процесса, созданных с помощью Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2ee5e-145">The [Workflow.Activities (O365 PnP Sample)](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.Activities) includes several custom workflow activities created with Visual Studio.</span></span>  <span data-ttu-id="2ee5e-146">Также показано, как использовать настраиваемые действия рабочего процесса в рабочий процесс.</span><span class="sxs-lookup"><span data-stu-id="2ee5e-146">It also demonstrates how to use the custom workflow activities in a workflow.</span></span>

<a name="create-custom-workflow-events"></a><span data-ttu-id="2ee5e-147">Создание настраиваемого рабочего процесса событий</span><span class="sxs-lookup"><span data-stu-id="2ee5e-147">Create custom workflow events</span></span>
-----------------------------
<span data-ttu-id="2ee5e-148">В этот параметр, события настраиваемого рабочего процесса создан и развернут в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="2ee5e-148">In this option custom workflow events are created and deployed to SharePoint.</span></span>

- <span data-ttu-id="2ee5e-149">События настраиваемый рабочий процесс может быть создан с помощью Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2ee5e-149">Custom workflow events may be created with Visual Studio.</span></span>
- <span data-ttu-id="2ee5e-150">События настраиваемый рабочий процесс может быть создан с помощью SharePoint Designer.</span><span class="sxs-lookup"><span data-stu-id="2ee5e-150">Custom workflow events may not be created with SharePoint Designer.</span></span>
- <span data-ttu-id="2ee5e-151">Могут быть использованы события настраиваемых рабочих процессов в SharePoint Designer, после развертывания в среде SharePoint.</span><span class="sxs-lookup"><span data-stu-id="2ee5e-151">Custom workflow events may be used in SharePoint Designer after they are deployed to a SharePoint environment.</span></span>

<span data-ttu-id="2ee5e-152">**Когда это подходит?**</span><span class="sxs-lookup"><span data-stu-id="2ee5e-152">**When is it a good fit?**</span></span>

<span data-ttu-id="2ee5e-153">Когда следует реализовать рабочих процессов в бизнес-процессы с требованиями требуют рабочих процессов следует ожидать в пользовательское событие перед тем как перейти.</span><span class="sxs-lookup"><span data-stu-id="2ee5e-153">When you need to implement workflows in business processes whose requirements require the workflows to wait for a custom event before proceeding.</span></span>

<span data-ttu-id="2ee5e-154">**Приступая к работе**</span><span class="sxs-lookup"><span data-stu-id="2ee5e-154">**Getting Started**</span></span>

<span data-ttu-id="2ee5e-155">[Workflow.CustomEvents (PnP образец O365)](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CustomEvents) демонстрируется создание рабочего процесса, который ожидает настраиваемую даже должно срабатывать, прежде чем продолжить.</span><span class="sxs-lookup"><span data-stu-id="2ee5e-155">The [Workflow.CustomEvents (O365 PnP Sample)](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CustomEvents) demonstrates how to create a workflow that waits for a custom even to fire before proceeding.</span></span>  <span data-ttu-id="2ee5e-156">Также демонстрируется использование JavaScript клиента со стороны объектной модели (JSOM) для Диспетчер служб рабочих процессов для создания настраиваемого события.</span><span class="sxs-lookup"><span data-stu-id="2ee5e-156">It also demonstrates how to use the JavaScript Client Side Object Model (JSOM) for the Workflow Services Manager to raise a custom event.</span></span>

<a name="create-custom-workflow-forms"></a><span data-ttu-id="2ee5e-157">Создание форм настраиваемых рабочих процессов</span><span class="sxs-lookup"><span data-stu-id="2ee5e-157">Create custom workflow forms</span></span>
------------------------------------------------
<span data-ttu-id="2ee5e-158">В этом параметре форм пользовательских процессов создан и развернут в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="2ee5e-158">In this option custom workflow forms are created and deployed to SharePoint.</span></span>

- <span data-ttu-id="2ee5e-159">Форм пользовательских процессов могут быть созданы с помощью Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2ee5e-159">Custom workflow forms may be created with Visual Studio.</span></span>
- <span data-ttu-id="2ee5e-160">Формы настраиваемый рабочий процесс может быть создан с помощью SharePoint Designer.</span><span class="sxs-lookup"><span data-stu-id="2ee5e-160">Custom workflow forms may not be created with SharePoint Designer.</span></span>
- <span data-ttu-id="2ee5e-161">Могут быть использованы форм настраиваемых рабочих процессов в SharePoint Designer, после развертывания в среде SharePoint.</span><span class="sxs-lookup"><span data-stu-id="2ee5e-161">Custom workflow forms may be used in SharePoint Designer after they are deployed to a SharePoint environment.</span></span>

<span data-ttu-id="2ee5e-162">**Когда это подходит?**</span><span class="sxs-lookup"><span data-stu-id="2ee5e-162">**When is it a good fit?**</span></span>

<span data-ttu-id="2ee5e-163">При необходимости для реализации рабочих процессов в бизнес-процессы с требованиями требуют настраиваемых форм.</span><span class="sxs-lookup"><span data-stu-id="2ee5e-163">When you need to implement workflows in business processes whose requirements require custom forms.</span></span>

<span data-ttu-id="2ee5e-164">**Приступая к работе**</span><span class="sxs-lookup"><span data-stu-id="2ee5e-164">**Getting Started**</span></span>

<span data-ttu-id="2ee5e-165">Следующей статье показано, как создавать формы сопоставления и запуска пользовательского рабочего процесса и использовать их в рабочий процесс.</span><span class="sxs-lookup"><span data-stu-id="2ee5e-165">The following article demonstrates how to create custom workflow association and initiation forms and use them in a workflow.</span></span>

- [<span data-ttu-id="2ee5e-166">Как: Создание настраиваемых форм рабочих процессов SharePoint Server 2013 с помощью Visual Studio 2012 г. (статья MSDN)</span><span class="sxs-lookup"><span data-stu-id="2ee5e-166">How to: Create Custom SharePoint Server 2013 Workflow Forms with Visual Studio 2012 (MSDN Article)</span></span>](https://msdn.microsoft.com/EN-US/library/office/dn518136.aspx)

<span data-ttu-id="2ee5e-167">[Workflow.CustomTasks (PnP образец O365)](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CustomTasks) показано, как создать настраиваемые формы задачи и запуска и использовать их в рабочий процесс.</span><span class="sxs-lookup"><span data-stu-id="2ee5e-167">The [Workflow.CustomTasks (O365 PnP Sample)](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CustomTasks) demonstrates how to create custom task and initiation forms and use them in a workflow.</span></span>

<a name="options-to-update-sharepoint-data-from-a-custom-workflow"></a><span data-ttu-id="2ee5e-168">Параметры для обновления данных SharePoint из настраиваемого рабочего процесса</span><span class="sxs-lookup"><span data-stu-id="2ee5e-168">Options to update SharePoint data from a custom workflow</span></span>
--------------------------------------------------------
<span data-ttu-id="2ee5e-169">У вас есть две возможности для изменения данных из настраиваемого рабочего процесса в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="2ee5e-169">You have a couple of options to update SharePoint data from a custom workflow.</span></span>

- <span data-ttu-id="2ee5e-170">Используйте маркер контекста и добавить в URL-адрес для проверки подлинности SharePoint.</span><span class="sxs-lookup"><span data-stu-id="2ee5e-170">Use the context token and Add-in web URL to authenticate to SharePoint.</span></span>
- <span data-ttu-id="2ee5e-171">URL-адрес использования надстройки и веб-прокси SharePoint для проверки подлинности SharePoint.</span><span class="sxs-lookup"><span data-stu-id="2ee5e-171">Use the Add-in web URL and the SharePoint web proxy to authenticate to SharePoint.</span></span>

<a name="use-the-context-token-and-add-in-web-url-to-authenticate-to-sharepoint"></a><span data-ttu-id="2ee5e-172">Используйте маркер контекста и добавить в URL-адрес для проверки подлинности SharePoint</span><span class="sxs-lookup"><span data-stu-id="2ee5e-172">Use the context token and Add-in web URL to authenticate to SharePoint</span></span>
----------------------------------------------------------------------

<span data-ttu-id="2ee5e-173">В этот параметр, необходимо передать маркер контекста и добавить в URL-адрес из рабочего процесса службы, рабочий процесс вызывает через заголовки http.</span><span class="sxs-lookup"><span data-stu-id="2ee5e-173">In this option you pass the context token and the Add-in web URL from the workflow to the service the workflow calls via http headers.</span></span>  <span data-ttu-id="2ee5e-174">Служба использует маркер контекста и добавить в URL-адрес для проверки подлинности в SharePoint и возвращает маркер доступа перед обновлением данных SharePoint.</span><span class="sxs-lookup"><span data-stu-id="2ee5e-174">The service uses the context token and Add-in web URL to authenticate to SharePoint and return an access token before updating SharePoint data.</span></span> 

- <span data-ttu-id="2ee5e-175">Этот подход требует передачи контента маркер из рабочего процесса для веб-службы.</span><span class="sxs-lookup"><span data-stu-id="2ee5e-175">This approach requires passing the content token from the workflow to the web service.</span></span>

<span data-ttu-id="2ee5e-176">**Когда это подходит?**</span><span class="sxs-lookup"><span data-stu-id="2ee5e-176">**When is it a good fit?**</span></span>

<span data-ttu-id="2ee5e-177">Если вам требуется передача данных в SharePoint будет выполнена на уровне клиента.</span><span class="sxs-lookup"><span data-stu-id="2ee5e-177">When you want the communication to SharePoint to occur at the client level.</span></span>

<span data-ttu-id="2ee5e-178">**Приступая к работе**</span><span class="sxs-lookup"><span data-stu-id="2ee5e-178">**Getting Started**</span></span>

<span data-ttu-id="2ee5e-179">Следующий пример показывает, как использовать маркер контекста и добавить в URL-адрес для проверки подлинности в SharePoint и изменения данных в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="2ee5e-179">The following sample demonstrates how to use the context token and the Add-in web URL to authenticate to SharePoint and update SharePoint data.</span></span>

- [<span data-ttu-id="2ee5e-180">Workflow.CallCustomService (O365 PnP образец)</span><span class="sxs-lookup"><span data-stu-id="2ee5e-180">Workflow.CallCustomService (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallCustomService)

<span data-ttu-id="2ee5e-181">Обратитесь к разделу [вызов Api веб-службы](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallCustomService#call-web-api-service) в [Workflow.CallCustomService (O365 PnP образец)](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallCustomService) README для получения дополнительных сведений о передаче маркер контекста и добавить в URL-адрес из рабочего процесса в службу.</span><span class="sxs-lookup"><span data-stu-id="2ee5e-181">See the [Call Web Api service](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallCustomService#call-web-api-service) section in the [Workflow.CallCustomService (O365 PnP Sample)](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallCustomService) README for more details about passing the context token and the Add-in web URL from the workflow to the service.</span></span>

<span data-ttu-id="2ee5e-182">Все остальные разделы [Workflow.CallCustomService (O365 PnP образец)](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallCustomService) README содержатся подробные сведения о всей рабочего процесса и удаленной службы и также пошаговыми руководствами для установки всех компонентов в Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="2ee5e-182">The other sections in the [Workflow.CallCustomService (O365 PnP Sample)](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallCustomService) README provide detailed information about the entire workflow and remote service and also walk you through setting up all of the components in Microsoft Azure.</span></span>

<a name="use-the-add-in-web-url-and-the-sharepoint-web-proxy-to-authenticate-to-sharepoint"></a><span data-ttu-id="2ee5e-183">URL-адрес использования надстройки и веб-прокси SharePoint для проверки подлинности SharePoint</span><span class="sxs-lookup"><span data-stu-id="2ee5e-183">Use the Add-in web URL and the SharePoint web proxy to authenticate to SharePoint</span></span>
---------------------------------------------------------------------------------

<span data-ttu-id="2ee5e-184">В этот параметр, когда вызывает рабочий процесс запускается, передаваемого Add-in web URL-адрес из рабочего процесса к службе рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="2ee5e-184">In this option when the workflow starts you pass the Add-in web URL from the workflow to the service the workflow calls.</span></span>  <span data-ttu-id="2ee5e-185">Служба передает Add-in web URL-адрес веб-прокси SharePoint.</span><span class="sxs-lookup"><span data-stu-id="2ee5e-185">The service passes the Add-in web URL to the SharePoint Web Proxy.</span></span>  <span data-ttu-id="2ee5e-186">Веб-прокси SharePoint использует Add-in web URL-адрес для проверки подлинности в SharePoint и возвращает маркер доступа.</span><span class="sxs-lookup"><span data-stu-id="2ee5e-186">The SharePoint Web Proxy uses the Add-in web URL to authenticate to SharePoint and return an access token.</span></span>  <span data-ttu-id="2ee5e-187">После этого веб-прокси SharePoint добавляет маркер доступа заголовки http перед вызовом для изменения данных в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="2ee5e-187">Then, the SharePoint Web Proxy appends the access token to the http headers before making the call to update SharePoint data.</span></span>

- <span data-ttu-id="2ee5e-188">Такой подход не требует передачи контента маркер из рабочего процесса для веб-службы.</span><span class="sxs-lookup"><span data-stu-id="2ee5e-188">This approach does not require passing the content token from the workflow to the web service.</span></span>

<span data-ttu-id="2ee5e-189">**Когда это подходит?**</span><span class="sxs-lookup"><span data-stu-id="2ee5e-189">**When is it a good fit?**</span></span>

<span data-ttu-id="2ee5e-190">Если вам требуется передача данных в SharePoint будет выполнена на уровне сервера.</span><span class="sxs-lookup"><span data-stu-id="2ee5e-190">When you want the communication to SharePoint to occur at the server level.</span></span>

<span data-ttu-id="2ee5e-191">**Приступая к работе**</span><span class="sxs-lookup"><span data-stu-id="2ee5e-191">**Getting Started**</span></span>

<span data-ttu-id="2ee5e-192">Следующий пример демонстрирует использование Add-in web URL-адрес и веб-прокси SharePoint для проверки подлинности в SharePoint и изменения данных в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="2ee5e-192">The following sample demonstrates how to use the Add-in web URL and the SharePoint web proxy to authenticate to SharePoint and update SharePoint data.</span></span>

- [<span data-ttu-id="2ee5e-193">Workflow.CallServiceUpdateSPViaProxy (O365 PnP образец)</span><span class="sxs-lookup"><span data-stu-id="2ee5e-193">Workflow.CallServiceUpdateSPViaProxy (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallServiceUpdateSPViaProxy)

<span data-ttu-id="2ee5e-194">Обратитесь к разделу [вызов Api веб-службы с помощью веб-прокси](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallServiceUpdateSPViaProxy#call-web-api-service-via-web-proxy) в [Workflow.CallServiceUpdateSPViaProxy (O365 PnP образец)](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallServiceUpdateSPViaProxy) README для получения дополнительных сведений о вызове SharePoint веб-прокси.</span><span class="sxs-lookup"><span data-stu-id="2ee5e-194">See the [Call Web Api service via web proxy](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallServiceUpdateSPViaProxy#call-web-api-service-via-web-proxy) section in the [Workflow.CallServiceUpdateSPViaProxy (O365 PnP Sample)](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallServiceUpdateSPViaProxy) README for more details about the SharePoint Web Proxy invocation.</span></span>

<span data-ttu-id="2ee5e-195">Все остальные разделы [Workflow.CallServiceUpdateSPViaProxy (O365 PnP образец)](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallServiceUpdateSPViaProxy) README содержатся подробные сведения о всей рабочего процесса и удаленной службы и также пошаговыми руководствами для установки всех компонентов в Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="2ee5e-195">The other sections in the [Workflow.CallServiceUpdateSPViaProxy (O365 PnP Sample)](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallServiceUpdateSPViaProxy) README provide detailed information about the entire workflow and remote service and also walk you through setting up all of the components in Microsoft Azure.</span></span>

<span data-ttu-id="2ee5e-196">В разделе [запроса удаленной службы с помощью веб-прокси в SharePoint 2013 (статья MSDN)](https://msdn.microsoft.com/en-us/library/office/fp179895.aspx) Дополнительные сведения о SharePoint веб-прокси.</span><span class="sxs-lookup"><span data-stu-id="2ee5e-196">See the [Query a remote service using the web proxy in SharePoint 2013 (MSDN Article)](https://msdn.microsoft.com/en-us/library/office/fp179895.aspx) for more information about the SharePoint Web Proxy.</span></span>

<a name="related-links"></a><span data-ttu-id="2ee5e-197">Ссылки по теме</span><span class="sxs-lookup"><span data-stu-id="2ee5e-197">Related links</span></span>
=============
- [<span data-ttu-id="2ee5e-198">Объектная модель рабочего процесса SharePoint 2013 (статья MSDN)</span><span class="sxs-lookup"><span data-stu-id="2ee5e-198">SharePoint 2013 workflow object model (MSDN Article)</span></span>](https://msdn.microsoft.com/EN-US/library/office/jj163969.aspx)
- [<span data-ttu-id="2ee5e-199">Типичные сообщения об ошибках при разработке рабочих процессов для SharePoint (статья MSDN)</span><span class="sxs-lookup"><span data-stu-id="2ee5e-199">Common error messages in SharePoint workflow development (MSDN Article)</span></span>](https://msdn.microsoft.com/EN-US/library/office/dn449112.aspx)
- [<span data-ttu-id="2ee5e-200">Использование средств взаимодействия рабочих процессов для SharePoint 2013 (статья MSDN)</span><span class="sxs-lookup"><span data-stu-id="2ee5e-200">Use workflow interop for SharePoint 2013 (MSDN Article)</span></span>](https://msdn.microsoft.com/EN-US/library/office/jj670125.aspx)
- [<span data-ttu-id="2ee5e-201">Разработка рабочих процессов SharePoint 2013 с помощью Visual Studio (статья MSDN)</span><span class="sxs-lookup"><span data-stu-id="2ee5e-201">Develop SharePoint 2013 workflows using Visual Studio (MSDN Article)</span></span>](https://msdn.microsoft.com/en-us/library/office/jj163199.aspx)
- [<span data-ttu-id="2ee5e-202">Веб-сайтов подготовки (добавить в SharePoint набора команд)</span><span class="sxs-lookup"><span data-stu-id="2ee5e-202">Site provisioning (SharePoint Add-in Recipe)</span></span>](site-provisioning-sharepoint-add-in.md)
- [<span data-ttu-id="2ee5e-203">Создание приложения рабочего процесса SharePoint с помощью Visual Studio 2012 г. (статья MSDN)</span><span class="sxs-lookup"><span data-stu-id="2ee5e-203">Create a SharePoint workflow app using Visual Studio 2012 (MSDN Article)</span></span>](https://msdn.microsoft.com/EN-US/library/office/dn456545.aspx)
- [<span data-ttu-id="2ee5e-204">Как: создание рабочих процессов SharePoint 2013 с помощью Visual Studio (статья MSDN)</span><span class="sxs-lookup"><span data-stu-id="2ee5e-204">How to: Create SharePoint 2013 Workflows using Visual Studio (MSDN Article)</span></span>](https://msdn.microsoft.com/EN-US/library/office/dn584771.aspx)
- [<span data-ttu-id="2ee5e-205">Как: построение и развертывание настраиваемого действия рабочего процесса (статья MSDN)</span><span class="sxs-lookup"><span data-stu-id="2ee5e-205">How to: Build and deploy workflow custom actions (MSDN Article)</span></span>](https://msdn.microsoft.com/en-us/library/office/jj163911.aspx)
- [<span data-ttu-id="2ee5e-206">Как: Создание настраиваемых форм рабочих процессов SharePoint Server 2013 с помощью Visual Studio 2012 г. (статья MSDN)</span><span class="sxs-lookup"><span data-stu-id="2ee5e-206">How to: Create Custom SharePoint Server 2013 Workflow Forms with Visual Studio 2012 (MSDN Article)</span></span>](https://msdn.microsoft.com/EN-US/library/office/dn518136.aspx)
- [<span data-ttu-id="2ee5e-207">Запроса удаленной службы с помощью веб-прокси в SharePoint 2013 (статья MSDN)</span><span class="sxs-lookup"><span data-stu-id="2ee5e-207">Query a remote service using the web proxy in SharePoint 2013 (MSDN Article)</span></span>](https://msdn.microsoft.com/en-us/library/office/fp179895.aspx)
- [<span data-ttu-id="2ee5e-208">Модули (надстройки SharePoint набора команд)</span><span class="sxs-lookup"><span data-stu-id="2ee5e-208">Modules (SharePoint Add-in Recipe)</span></span>](modules-sharepoint-add-in.md)
- [<span data-ttu-id="2ee5e-209">Веб-сайтов подготовки (добавить в SharePoint набора команд)</span><span class="sxs-lookup"><span data-stu-id="2ee5e-209">Site provisioning (SharePoint Add-in Recipe)</span></span>](site-provisioning-sharepoint-add-in.md)
- <span data-ttu-id="2ee5e-210">Руководств по [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Руководств")</span><span class="sxs-lookup"><span data-stu-id="2ee5e-210">Guidance articles at [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Guidance Articles")</span></span>
- <span data-ttu-id="2ee5e-211">Справочные материалы в библиотеке MSDN по [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "Справочные материалы в библиотеке MSDN")</span><span class="sxs-lookup"><span data-stu-id="2ee5e-211">References in MSDN at [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "References in MSDN")</span></span>
- <span data-ttu-id="2ee5e-212">Видеозаписи по [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "видео")</span><span class="sxs-lookup"><span data-stu-id="2ee5e-212">Videos at [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")</span></span>

<a name="related-pnp-samples"></a><span data-ttu-id="2ee5e-213">Примеры связанных с ними PnP</span><span class="sxs-lookup"><span data-stu-id="2ee5e-213">Related PnP samples</span></span>
===================
- [<span data-ttu-id="2ee5e-214">Workflow.Activities (O365 PnP образец)</span><span class="sxs-lookup"><span data-stu-id="2ee5e-214">Workflow.Activities (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.Activities)
- [<span data-ttu-id="2ee5e-215">Workflow.CustomEvents (O365 PnP образец)</span><span class="sxs-lookup"><span data-stu-id="2ee5e-215">Workflow.CustomEvents (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CustomEvents)
- [<span data-ttu-id="2ee5e-216">Workflow.CustomTasks (O365 PnP образец)</span><span class="sxs-lookup"><span data-stu-id="2ee5e-216">Workflow.CustomTasks (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CustomTasks)
- [<span data-ttu-id="2ee5e-217">Workflow.CallCustomService (O365 PnP образец)</span><span class="sxs-lookup"><span data-stu-id="2ee5e-217">Workflow.CallCustomService (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallCustomService)
- [<span data-ttu-id="2ee5e-218">Workflow.CallServiceUpdateSPViaProxy (O365 PnP образец)</span><span class="sxs-lookup"><span data-stu-id="2ee5e-218">Workflow.CallServiceUpdateSPViaProxy (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallServiceUpdateSPViaProxy)
- <span data-ttu-id="2ee5e-219">Примеры и содержимое в [http://aka.ms/OfficeDevPnP](http://aka.ms/OfficeDevPnP)</span><span class="sxs-lookup"><span data-stu-id="2ee5e-219">Samples and content at [http://aka.ms/OfficeDevPnP](http://aka.ms/OfficeDevPnP)</span></span>

<a name="applies-to"></a><span data-ttu-id="2ee5e-220">Применимо к</span><span class="sxs-lookup"><span data-stu-id="2ee5e-220">Applies to</span></span>
==========
- <span data-ttu-id="2ee5e-221">Office 365 нескольких клиентов (MT)</span><span class="sxs-lookup"><span data-stu-id="2ee5e-221">Office 365 Multi Tenant (MT)</span></span>
- <span data-ttu-id="2ee5e-222">Office 365 выделенных (D)</span><span class="sxs-lookup"><span data-stu-id="2ee5e-222">Office 365 Dedicated (D)</span></span>
- <span data-ttu-id="2ee5e-223">SharePoint 2013 в локальной</span><span class="sxs-lookup"><span data-stu-id="2ee5e-223">SharePoint 2013 on-premises</span></span>
