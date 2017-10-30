---
title: "Запуск и настройка свойств рабочего процесса"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 7386bbf9-3ed6-4732-bcdb-b27baed7397e
ms.openlocfilehash: eb69b75b91289cca91edb448242b4f233c7a08f7
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="workflow-initiation-and-configuration-properties"></a><span data-ttu-id="4ed8a-102">Запуск и настройка свойств рабочего процесса</span><span class="sxs-lookup"><span data-stu-id="4ed8a-102">Workflow initiation and configuration properties</span></span>
<span data-ttu-id="4ed8a-103">Общие сведения о инициализации и сопоставлении свойств, которые задает SharePoint для рабочих процессов.</span><span class="sxs-lookup"><span data-stu-id="4ed8a-103">See an overview of the initiation and association properties that SharePoint sets on workflows.</span></span>
## 

<span data-ttu-id="4ed8a-p101">При запуске рабочего процесса SharePoint автоматически устанавливает количество сопоставления и запуска свойства, которые поддерживают рабочего процесса. Они перечислены ниже. Набор свойств, определенных отличается немного в зависимости от рабочих процессов **сайта** или рабочий процесс **списка**. Эти различия определяются в списках.</span><span class="sxs-lookup"><span data-stu-id="4ed8a-p101">When you launch a workflow, SharePoint automatically sets a number of association and initiation properties that support the workflow. These are listed below. The set of properties that are set differs slightly depending whether it is a **site** workflows or a **list** workflow. These differences are identified in the lists.</span></span>
  
    
    
<span data-ttu-id="4ed8a-108">Используйте следующие рекомендации для сопоставления и запуска рабочих процессов с помощью объектной модели рабочих процессов (инициирование):</span><span class="sxs-lookup"><span data-stu-id="4ed8a-108">Use the following guidelines to associate and launch (initiate) your workflows using the workflow object model:</span></span>
  
    
    

- <span data-ttu-id="4ed8a-109">Чтобы создать связь для рабочего процесса **списка**, используйте метод [PublishSubscriptionForList](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowSubscriptionService.PublishSubscriptionForList.aspx) .</span><span class="sxs-lookup"><span data-stu-id="4ed8a-109">To create an association for a **list** workflow, use the [PublishSubscriptionForList](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowSubscriptionService.PublishSubscriptionForList.aspx) method.</span></span>
    
  
- <span data-ttu-id="4ed8a-110">Чтобы создать связь для рабочего процесса **сайта**, используйте метод [PublishSubscription](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowSubscriptionService.PublishSubscription.aspx) .</span><span class="sxs-lookup"><span data-stu-id="4ed8a-110">To create an association for a **site** workflow, use the [PublishSubscription](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowSubscriptionService.PublishSubscription.aspx) method.</span></span>
    
  
- <span data-ttu-id="4ed8a-111">Чтобы запустить рабочий процесс **списка**, используйте метод [StartWorkflowOnListItem](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowInstanceService.StartWorkflowOnListItem.aspx) .</span><span class="sxs-lookup"><span data-stu-id="4ed8a-111">To initiate a **list** workflow, use the [StartWorkflowOnListItem](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowInstanceService.StartWorkflowOnListItem.aspx) method.</span></span>
    
  
- <span data-ttu-id="4ed8a-112">Для запуска рабочего процесса **сайта**, используйте метод [StartWorkflow](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowInstanceService.StartWorkflow.aspx) .</span><span class="sxs-lookup"><span data-stu-id="4ed8a-112">To initiate a **site** workflow, use the [StartWorkflow](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowInstanceService.StartWorkflow.aspx) method.</span></span>
    
  

> <span data-ttu-id="4ed8a-113">**Примечание:** Два метода для **связывания** рабочих процессов находятся в классе [WorkflowSubscriptionService](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowSubscriptionService.aspx) во время на класс [WorkflowInstanceService](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowInstanceService.aspx) находятся два метода для **запуска** рабочих процессов.</span><span class="sxs-lookup"><span data-stu-id="4ed8a-113">**Note:** The two methods for **associating** workflows are found on the [WorkflowSubscriptionService](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowSubscriptionService.aspx) class, while the two methods for **launching** workflows are found on the [WorkflowInstanceService](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowInstanceService.aspx) class.</span></span>
  
    
    


## <a name="association-properties"></a><span data-ttu-id="4ed8a-114">Сопоставления свойств</span><span class="sxs-lookup"><span data-stu-id="4ed8a-114">Association properties</span></span>

<span data-ttu-id="4ed8a-p102">Значения свойства ассоциации устанавливаются при вызове  [PublishSubscription](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowSubscriptionService.PublishSubscription.aspx) . Значения свойств связи являются свойства уровня привязки, что означает, что все экземпляры рабочих процессов с помощью данного сопоставления совместно использовать такое же значение свойства. Значение свойства связи в пределах рабочим процессом можно извлечь с помощью действия **GetConfigurationValue**.</span><span class="sxs-lookup"><span data-stu-id="4ed8a-p102">The values of association properties are set when you call  [PublishSubscription](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowSubscriptionService.PublishSubscription.aspx) . The association property values are association-level properties, meaning that all workflow instances with a given association share the same property value. You can retrieve an association property value within the workflow itself by using the **GetConfigurationValue** activity.</span></span>
  
    
    
<span data-ttu-id="4ed8a-118">Ниже приведен список свойств связи, установленные по умолчанию для **списка** и **сайта** рабочих процессов при вызове [PublishSubscription](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowSubscriptionService.PublishSubscription.aspx) .</span><span class="sxs-lookup"><span data-stu-id="4ed8a-118">Following is a list of association properties that are set by default for both **list** and **site** workflows when you call [PublishSubscription](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowSubscriptionService.PublishSubscription.aspx) .</span></span>
  
    
    

-  [<span data-ttu-id="4ed8a-119">AssociationTitle</span><span class="sxs-lookup"><span data-stu-id="4ed8a-119">AssociationTitle</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowConfigurationPropertyName.AssociationTitle.aspx)
    
  
-  [<span data-ttu-id="4ed8a-120">AssociatorUserId</span><span class="sxs-lookup"><span data-stu-id="4ed8a-120">AssociatorUserId</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowConfigurationPropertyName.AssociatorUserId.aspx)
    
  
-  [<span data-ttu-id="4ed8a-121">LayoutsFolder</span><span class="sxs-lookup"><span data-stu-id="4ed8a-121">LayoutsFolder</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowConfigurationPropertyName.LayoutsFolder.aspx)
    
  
-  <span data-ttu-id="4ed8a-122">ParentContentTypeId()</span><span class="sxs-lookup"><span data-stu-id="4ed8a-122">ParentContentTypeId()</span></span>
    
  
- <span data-ttu-id="4ed8a-123">**HistoryListId***</span><span class="sxs-lookup"><span data-stu-id="4ed8a-123">**HistoryListId***</span></span>
    
  
- <span data-ttu-id="4ed8a-124">**TaskListId***</span><span class="sxs-lookup"><span data-stu-id="4ed8a-124">**TaskListId***</span></span>
    
  
- <span data-ttu-id="4ed8a-125">**FormData***</span><span class="sxs-lookup"><span data-stu-id="4ed8a-125">**FormData***</span></span>
    
  
- <span data-ttu-id="4ed8a-126">**SharePointWorkflowContext.Subscription.EventSourceId***</span><span class="sxs-lookup"><span data-stu-id="4ed8a-126">**SharePointWorkflowContext.Subscription.EventSourceId***</span></span>
    
  
- <span data-ttu-id="4ed8a-127">**SharePointWorkflowContext.Subscription.EventType***</span><span class="sxs-lookup"><span data-stu-id="4ed8a-127">**SharePointWorkflowContext.Subscription.EventType***</span></span>
    
  
- <span data-ttu-id="4ed8a-128">**SharePointWorkflowContext.Subscription.DisplayName***</span><span class="sxs-lookup"><span data-stu-id="4ed8a-128">**SharePointWorkflowContext.Subscription.DisplayName***</span></span>
    
  
- <span data-ttu-id="4ed8a-129">**SharePointWorkflowContext.Subscription.Id***</span><span class="sxs-lookup"><span data-stu-id="4ed8a-129">**SharePointWorkflowContext.Subscription.Id***</span></span>
    
  
- <span data-ttu-id="4ed8a-130">**SharePointWorkflowContext.Subscription.Name***</span><span class="sxs-lookup"><span data-stu-id="4ed8a-130">**SharePointWorkflowContext.Subscription.Name***</span></span>
    
  
- <span data-ttu-id="4ed8a-131">**SharePointWorkflowContext.Subscription.CreatedDate***</span><span class="sxs-lookup"><span data-stu-id="4ed8a-131">**SharePointWorkflowContext.Subscription.CreatedDate***</span></span>
    
  

> <span data-ttu-id="4ed8a-132">**Важные:** Свойства, помеченные звездочкой (\*) не определены в API рабочего процесса, чтобы получить доступ к их просто использовать их строковые значения.</span><span class="sxs-lookup"><span data-stu-id="4ed8a-132">**Important:** Properties marked with an asterisk (\*) are not defined in the Workflow APIs, so to access them simply use their string values.</span></span> 
  
    
    

<span data-ttu-id="4ed8a-133">В случае **списка** рабочих процессов существует четыре дополнительных сопоставления свойств, определенных по умолчанию при вызове [PublishSubscriptionForList(WorkflowSubscription, Guid)](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowSubscriptionService.PublishSubscriptionForList.aspx) .</span><span class="sxs-lookup"><span data-stu-id="4ed8a-133">In the case of **list** workflows, there are four additional association properties that are set by default when you call [PublishSubscriptionForList(WorkflowSubscription, Guid)](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowSubscriptionService.PublishSubscriptionForList.aspx) .</span></span>
  
    
    

-  [<span data-ttu-id="4ed8a-134">ListId</span><span class="sxs-lookup"><span data-stu-id="4ed8a-134">ListId</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowConfigurationPropertyName.ListId.aspx)
    
  
-  [<span data-ttu-id="4ed8a-135">ListName</span><span class="sxs-lookup"><span data-stu-id="4ed8a-135">ListName</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowConfigurationPropertyName.ListName.aspx)
    
  
- <span data-ttu-id="4ed8a-136">**StatusColumnCreated***</span><span class="sxs-lookup"><span data-stu-id="4ed8a-136">**StatusColumnCreated***</span></span>
    
  
- <span data-ttu-id="4ed8a-137">**StatusFieldName***</span><span class="sxs-lookup"><span data-stu-id="4ed8a-137">**StatusFieldName***</span></span>
    
  

> <span data-ttu-id="4ed8a-138">**Важные:** Свойства, помеченные звездочкой (\*) не определены в API рабочего процесса, чтобы получить доступ к их просто использовать их строковые значения.</span><span class="sxs-lookup"><span data-stu-id="4ed8a-138">**Important:** Properties marked with an asterisk (\*) are not defined in the Workflow APIs, so to access them simply use their string values.</span></span> 
  
    
    


> <span data-ttu-id="4ed8a-139">**Примечание:** Можно добавить пользовательские сопоставления свойств с помощью формы связывания.</span><span class="sxs-lookup"><span data-stu-id="4ed8a-139">**Note:** You can add custom association properties by using an association form.</span></span> 
  
    
    


## <a name="initiation-properties"></a><span data-ttu-id="4ed8a-140">Свойства инициализации</span><span class="sxs-lookup"><span data-stu-id="4ed8a-140">Initiation properties</span></span>

<span data-ttu-id="4ed8a-p103">Свойства запуска  это внешние переменные, значения которых установлены при запуске рабочего процесса  то есть, при вызове **StartWorkflow**. Тем не менее, значения свойств могут обновляться во время выполнения из экземпляра рабочего процесса с помощью действия **ExternalVariableValue**. Значения внешних переменных можно извлечь из *за пределами*  рабочего процесса с помощью [Properties](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowInstance.Properties.aspx) .</span><span class="sxs-lookup"><span data-stu-id="4ed8a-p103">Initiation properties are external variables whose values are set when the workflow is initiated - that is, when you call **StartWorkflow**. Note, however, that the property values can be updated at runtime from within the workflow instance by using the **ExternalVariableValue** activity. You can retrieve the values of external variables from *outside*  the workflow by using [Properties](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowInstance.Properties.aspx) .</span></span>
  
    
    
<span data-ttu-id="4ed8a-144">Внешние значения переменных специфичны для каждого экземпляра рабочего процесса (в отличие от свойства связи, где все экземпляры рабочих процессов совместно использовать те же значения свойства).</span><span class="sxs-lookup"><span data-stu-id="4ed8a-144">External variable values are specific to each workflow instance (as opposed to association properties, where all workflow instances share the same property values).</span></span> 
  
    
    
<span data-ttu-id="4ed8a-145">Все экземпляры рабочих процессов (списка и сайта) иметь некоторые внешние переменные, которые устанавливаются по умолчанию при вызове **StartWorkflow**:</span><span class="sxs-lookup"><span data-stu-id="4ed8a-145">All workflow instances (both list and site) have some external variables that are set by default when you call **StartWorkflow**:</span></span>
  
    
    

-  [<span data-ttu-id="4ed8a-146">InitiatorUserId</span><span class="sxs-lookup"><span data-stu-id="4ed8a-146">InitiatorUserId</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.ExternalVariableName.InitiatorUserId.aspx)
    
  
-  [<span data-ttu-id="4ed8a-147">RetryCode</span><span class="sxs-lookup"><span data-stu-id="4ed8a-147">RetryCode</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.ExternalVariableName.RetryCode.aspx)
    
  
-  [<span data-ttu-id="4ed8a-148">RelatedItems</span><span class="sxs-lookup"><span data-stu-id="4ed8a-148">RelatedItems</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.ExternalVariableName.RelatedItems.aspx)
    
  
<span data-ttu-id="4ed8a-149">Список экземпляров рабочих процессов имеет некоторые дополнительные внешние переменные, которые устанавливаются по умолчанию при вызове  [StartWorkflowOnListItem](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowInstanceService.StartWorkflowOnListItem.aspx) :</span><span class="sxs-lookup"><span data-stu-id="4ed8a-149">List workflows instances have some additional external variables that are set by default when you call  [StartWorkflowOnListItem](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowInstanceService.StartWorkflowOnListItem.aspx) :</span></span>
  
    
    

-  [<span data-ttu-id="4ed8a-150">CurrentItemUrl</span><span class="sxs-lookup"><span data-stu-id="4ed8a-150">CurrentItemUrl</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.ExternalVariableName.CurrentItemUrl.aspx)
    
  
-  [<span data-ttu-id="4ed8a-151">ItemId</span><span class="sxs-lookup"><span data-stu-id="4ed8a-151">ItemId</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.ExternalVariableName.ItemId.aspx)
    
  
-  [<span data-ttu-id="4ed8a-152">ItemGuid</span><span class="sxs-lookup"><span data-stu-id="4ed8a-152">ItemGuid</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.ExternalVariableName.ItemGuid.aspx)
    
  
-  [<span data-ttu-id="4ed8a-153">ContextListId</span><span class="sxs-lookup"><span data-stu-id="4ed8a-153">ContextListId</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.ExternalVariableName.ContextListId.aspx)
    
  
-  [<span data-ttu-id="4ed8a-154">UniqueId</span><span class="sxs-lookup"><span data-stu-id="4ed8a-154">UniqueId</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.ExternalVariableName.UniqueId.aspx)
    
  

> <span data-ttu-id="4ed8a-155">**Примечание:** Можно добавить настраиваемые инициализации свойства с помощью форму запуска.</span><span class="sxs-lookup"><span data-stu-id="4ed8a-155">**Note:** You can add custom initiation properties by using an initiation form.</span></span> 
  
    
    


## <a name="additional-resources"></a><span data-ttu-id="4ed8a-156">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="4ed8a-156">Additional resources</span></span>
<span data-ttu-id="4ed8a-157"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="4ed8a-157"><a name="bk_addresources"> </a></span></span>


-  [<span data-ttu-id="4ed8a-158">Разработка рабочих процессов в SharePoint с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4ed8a-158">Develop SharePoint workflows using Visual Studio</span></span>](develop-sharepoint-workflows-using-visual-studio.md)
    
  
-  [<span data-ttu-id="4ed8a-159">Как: создание рабочих процессов SharePoint с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4ed8a-159">How to: Create SharePoint Workflows using Visual Studio</span></span>](how-to-create-sharepoint-workflows-using-visual-studio.md)
    
  

  
    
    

