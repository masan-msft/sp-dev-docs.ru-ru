---
title: "Объектная модель рабочего процесса SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: be615a89-3201-4cd8-bbc7-15f3abf9f668
ms.openlocfilehash: 0b02055055f6777b6c641c1a1445194573c54de5
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="sharepoint-workflow-object-model"></a><span data-ttu-id="0e8fa-102">Объектная модель рабочего процесса SharePoint</span><span class="sxs-lookup"><span data-stu-id="0e8fa-102">SharePoint workflow object model</span></span>
<span data-ttu-id="0e8fa-103">Получите Краткое введение в объектной модели рабочих процессов в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="0e8fa-103">Get a brief introduction to the workflow object model in SharePoint.</span></span>
## <a name="sharepoint-workflow-object-model"></a><span data-ttu-id="0e8fa-104">Объектная модель рабочего процесса SharePoint</span><span class="sxs-lookup"><span data-stu-id="0e8fa-104">SharePoint workflow object model</span></span>
<span data-ttu-id="0e8fa-105"><a name="bk_SPwfom"> </a></span><span class="sxs-lookup"><span data-stu-id="0e8fa-105"></span></span>

<span data-ttu-id="0e8fa-106">Для Windows Workflow Foundation 4, но с нововведения, которые позволяют функциональности рабочих процессов в SharePoint как правило и в SharePoint надстройки в частности, объектной модели SharePoint построен на основе объектной модели .NET Framework 4.</span><span class="sxs-lookup"><span data-stu-id="0e8fa-106">The SharePoint object model is built on top of the .NET Framework 4 object model for Windows Workflow Foundation 4, but with innovations that enable workflow functionality in SharePoint generally, and in SharePoint Add-ins in particular.</span></span> <span data-ttu-id="0e8fa-107">Собственной объектной модели .NET Framework 4 для Windows Workflow Foundation 4 находится в.NET Framework [пространства имен System.Workflow](http://msdn.microsoft.com/en-us/library/gg145026.aspx).</span><span class="sxs-lookup"><span data-stu-id="0e8fa-107">The native .NET Framework 4 object model for Windows Workflow Foundation 4 is located in the .NET Framework  [System.Workflow namespaces](http://msdn.microsoft.com/en-us/library/gg145026.aspx).</span></span>
  
    
    
<span data-ttu-id="0e8fa-p102">Можно рассматривать объектной модели SharePoint, рабочий процесс  как набор служб рабочих процессов. Существует четыре службы:</span><span class="sxs-lookup"><span data-stu-id="0e8fa-p102">One way to think of the SharePoint workflow object model is as a set of workflow services. There are four services:</span></span> 
  
    
    

- <span data-ttu-id="0e8fa-110">**Экземпляра службы управления:** Управляет экземпляров рабочих процессов и их выполнения.</span><span class="sxs-lookup"><span data-stu-id="0e8fa-110">**Instance management service:** Manages workflow instances and their execution.</span></span>
    
  
- <span data-ttu-id="0e8fa-111">**Развертывания службы:** Управляет развертывания определений рабочих процессов.</span><span class="sxs-lookup"><span data-stu-id="0e8fa-111">**Deployment service:** Manages the deployment of workflow definitions.</span></span>
    
  
- <span data-ttu-id="0e8fa-112">**Взаимодействия службы:** Управляет моста взаимодействия для поддержки прежних версий рабочих процессов.</span><span class="sxs-lookup"><span data-stu-id="0e8fa-112">**Interop service:** Manages the interop bridge for supporting legacy workflows.</span></span>
    
  
- <span data-ttu-id="0e8fa-113">**Системы обмена сообщениями службы:** Управляет транспорта и сообщений.</span><span class="sxs-lookup"><span data-stu-id="0e8fa-113">**Messaging service:** Manages message queuing and transport.</span></span>
    
  

### <a name="sharepoint-workflow-namespaces"></a><span data-ttu-id="0e8fa-114">Пространства имен рабочих процессов SharePoint</span><span class="sxs-lookup"><span data-stu-id="0e8fa-114">SharePoint workflow namespaces</span></span>

<span data-ttu-id="0e8fa-115">Рабочий процесс объектной модели SharePoint, с другой стороны, содержатся в десяти пространства имен: пять из них являются зарегистрированными пространствами имен и пять другим пользователям, Microsoft Office пространства имен.</span><span class="sxs-lookup"><span data-stu-id="0e8fa-115">The SharePoint workflow object model, on the other hand, is contained in ten namespaces: five of them are SharePoint namespaces, and five others are Microsoft Office namespaces.</span></span>
  
    
    
 <span data-ttu-id="0e8fa-116">пространства имен **Microsoft.SharePoint**:</span><span class="sxs-lookup"><span data-stu-id="0e8fa-116">**Microsoft.SharePoint** namespaces:</span></span>
  
    
    

-  [<span data-ttu-id="0e8fa-117">Microsoft.SharePoint.Workflow</span><span class="sxs-lookup"><span data-stu-id="0e8fa-117">Microsoft.SharePoint.Workflow</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.Workflow.aspx)
    
  
-  [<span data-ttu-id="0e8fa-118">Microsoft.SharePoint.Workflow.Application</span><span class="sxs-lookup"><span data-stu-id="0e8fa-118">Microsoft.SharePoint.Workflow.Application</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.Workflow.Application.aspx)
    
  
-  [<span data-ttu-id="0e8fa-119">Microsoft.SharePoint.WorkflowActions</span><span class="sxs-lookup"><span data-stu-id="0e8fa-119">Microsoft.SharePoint.WorkflowActions</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowActions.aspx)
    
  
-  [<span data-ttu-id="0e8fa-120">Microsoft.SharePoint.WorkflowActions.WithKey</span><span class="sxs-lookup"><span data-stu-id="0e8fa-120">Microsoft.SharePoint.WorkflowActions.WithKey</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowActions.WithKey.aspx)
    
  
-  [<span data-ttu-id="0e8fa-121">Microsoft.SharePoint.WorkflowServices</span><span class="sxs-lookup"><span data-stu-id="0e8fa-121">Microsoft.SharePoint.WorkflowServices</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.aspx)
    
  
-  [<span data-ttu-id="0e8fa-122">Microsoft.SharePoint.WorkflowServices.Activities</span><span class="sxs-lookup"><span data-stu-id="0e8fa-122">Microsoft.SharePoint.WorkflowServices.Activities</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.Activities.aspx)
    
  
 <span data-ttu-id="0e8fa-123">пространства имен **Microsoft.Office**:</span><span class="sxs-lookup"><span data-stu-id="0e8fa-123">**Microsoft.Office** namespaces:</span></span>
  
    
    

-  [<span data-ttu-id="0e8fa-124">Microsoft.Office.Workflow</span><span class="sxs-lookup"><span data-stu-id="0e8fa-124">Microsoft.Office.Workflow</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Workflow.aspx)
    
  
-  [<span data-ttu-id="0e8fa-125">Microsoft.Office.Workflow.Actions</span><span class="sxs-lookup"><span data-stu-id="0e8fa-125">Microsoft.Office.Workflow.Actions</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Workflow.Actions.aspx)
    
  
-  [<span data-ttu-id="0e8fa-126">Microsoft.Office.Workflow.Feature</span><span class="sxs-lookup"><span data-stu-id="0e8fa-126">Microsoft.Office.Workflow.Feature</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Workflow.Feature.aspx)
    
  
-  [<span data-ttu-id="0e8fa-127">Microsoft.Office.Workflow.Routing</span><span class="sxs-lookup"><span data-stu-id="0e8fa-127">Microsoft.Office.Workflow.Routing</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Workflow.Routing.aspx)
    
  
-  [<span data-ttu-id="0e8fa-128">Microsoft.Office.Workflow.Utility</span><span class="sxs-lookup"><span data-stu-id="0e8fa-128">Microsoft.Office.Workflow.Utility</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Workflow.Utility.aspx)
    
  

### <a name="sharepoint-workflow-schemas"></a><span data-ttu-id="0e8fa-129">Схемы рабочих процессов SharePoint</span><span class="sxs-lookup"><span data-stu-id="0e8fa-129">SharePoint workflow schemas</span></span>

<span data-ttu-id="0e8fa-130">Справочник по содержимого для схем SharePoint содержащиеся в узле ссылку под названием [схемы рабочих процессов](http://msdn.microsoft.com/library/b36ded16-3ffd-4931-811e-c402c1e35b07%28Office.15%29.aspx)и содержать следующие элементы:</span><span class="sxs-lookup"><span data-stu-id="0e8fa-130">Reference content for SharePoint schemas is contained in the reference node entitled  [Workflow schemas](http://msdn.microsoft.com/library/b36ded16-3ffd-4931-811e-c402c1e35b07%28Office.15%29.aspx), and contain the following:</span></span>
  
    
    

-  [<span data-ttu-id="0e8fa-131">Справочник по схеме WorkflowActions4</span><span class="sxs-lookup"><span data-stu-id="0e8fa-131">WorkflowActions4 schema reference</span></span>](http://msdn.microsoft.com/library/1c0112de-0139-e64d-d3d6-658541695391%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="0e8fa-132">Справочник по схеме WorkflowActions3</span><span class="sxs-lookup"><span data-stu-id="0e8fa-132">WorkflowActions3 schema reference</span></span>](http://msdn.microsoft.com/library/7a03ead8-30e0-4601-9c6f-edfb04ce57f9%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="0e8fa-133">Обзор схемы конфигурации рабочего процесса</span><span class="sxs-lookup"><span data-stu-id="0e8fa-133">Workflow configuration schema reference</span></span>](http://msdn.microsoft.com/library/63824239-6eb2-4cf1-ba84-44eace4d3781%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="0e8fa-134">Справочник по схеме WorkflowInfo</span><span class="sxs-lookup"><span data-stu-id="0e8fa-134">WorkflowInfo schema reference</span></span>](http://msdn.microsoft.com/library/f3bdcc70-15a0-44b2-9b01-330f13430354%28Office.15%29.aspx)
    
  

## <a name="additional-resources"></a><span data-ttu-id="0e8fa-135">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="0e8fa-135">Additional resources</span></span>
<span data-ttu-id="0e8fa-136"><a name="bk_additionalresources"> </a></span><span class="sxs-lookup"><span data-stu-id="0e8fa-136"></span></span>


-  [<span data-ttu-id="0e8fa-137">Краткое описание Windows Workflow Foundation (WF) в .NET 4 для разработчика</span><span class="sxs-lookup"><span data-stu-id="0e8fa-137">A Developer's Introduction to Windows Workflow Foundation (WF) in .NET 4</span></span>](http://msdn.microsoft.com/en-us/library/ee342461.aspx)
    
  
-  [<span data-ttu-id="0e8fa-138">Windows Workflow Foundation 4.0: Hello, рабочий процесс!</span><span class="sxs-lookup"><span data-stu-id="0e8fa-138">Windows Workflow Foundation 4.0: Hello, workflow!</span></span>](http://weblogs.asp.net/gunnarpeipman/archive/2009/07/08/windows-workflow-foundation-4-0-hello-workflow.aspx)
    
  
-  [<span data-ttu-id="0e8fa-139">Windows Workflow Foundation (WF) (en)</span><span class="sxs-lookup"><span data-stu-id="0e8fa-139">Windows Workflow Foundation (WF) Screencasts</span></span>](http://msdn.microsoft.com/en-us/netframework/dd733248)
    
  
-  [<span data-ttu-id="0e8fa-140">Справочник по действий рабочих процессов для SharePoint</span><span class="sxs-lookup"><span data-stu-id="0e8fa-140">Workflow actions and activities reference for SharePoint</span></span>](workflow-actions-and-activities-reference-for-sharepoint.md)
    
  
-  [<span data-ttu-id="0e8fa-141">Разработка рабочих процессов в SharePoint с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0e8fa-141">Develop SharePoint workflows using Visual Studio</span></span>](develop-sharepoint-workflows-using-visual-studio.md)
    
  

  
    
    

