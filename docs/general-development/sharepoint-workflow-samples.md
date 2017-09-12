---
title: "Примеры рабочих процессов SharePoint"
ms.prod: SHAREPOINT
ms.assetid: ffaccd6b-426d-4ca0-b62f-bc7b14641a49
ms.openlocfilehash: 84af8d15d5375469d81602a120ca0068782337f4
ms.sourcegitcommit: d9e955bf9d5afd9ad8ae8304a3ddb85ac27b3406
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/06/2017
---
# <a name="sharepoint-workflow-samples"></a><span data-ttu-id="339fa-102">Примеры рабочих процессов SharePoint</span><span class="sxs-lookup"><span data-stu-id="339fa-102">SharePoint workflow samples</span></span>
<span data-ttu-id="339fa-103">Примеры рабочих процессов, иллюстрирующие создание и реализацию рабочих процессов SharePoint на новой платформе Workflow Manager Client 1.0.</span><span class="sxs-lookup"><span data-stu-id="339fa-103">Provides sample workflows to help illustrate how to create and implement SharePoint workflows in the new Workflow Manager Client 1.0 framework.</span></span>
## <a name="workflow-samples-for-sharepoint"></a><span data-ttu-id="339fa-104">Примеры рабочих процессов для SharePoint</span><span class="sxs-lookup"><span data-stu-id="339fa-104">Workflow samples for SharePoint</span></span>
<span data-ttu-id="339fa-105"><a name="bkm_wfsamples"> </a></span><span class="sxs-lookup"><span data-stu-id="339fa-105"></span></span>

<span data-ttu-id="339fa-p101">Эта серия примеров рабочих процессов была разработана для демонстрации широких возможностей рабочих процессов в SharePoint. Они разработаны с помощью Visual Studio 2012 и доступны в  [коллекции примеров MSDN](http://code.msdn.microsoft.com/). Ниже приводятся ссылки на отдельные примеры.</span><span class="sxs-lookup"><span data-stu-id="339fa-p101">This series of sample workflows was developed to demonstrate the large range of workflow capabilities in SharePoint. They were developed using Visual Studio 2012 and are available in the  [MSDN Samples Gallery](http://code.msdn.microsoft.com/). Links to the individual samples are provided.</span></span>
  
    
    

### <a name="sharepoint-workflow-call-an-external-web-service"></a><span data-ttu-id="339fa-109">Рабочий процесс SharePoint: вызов внешней веб-службы</span><span class="sxs-lookup"><span data-stu-id="339fa-109">SharePoint workflow: Call an external web service</span></span>

<span data-ttu-id="339fa-p102">В этом примере используется Visual Studio, чтобы продемонстрировать создание рабочего процесса, который вызывает внешнюю веб-службу с помощью действия **HttpGet**. При вызове веб-службы рабочий процесс также использует тип данных **DynamicValue**.</span><span class="sxs-lookup"><span data-stu-id="339fa-p102">This sample uses Visual Studio to demonstrate creating a workflow that calls an external web service using the **HttpGet** activity. In calling the web service, the workflow also uses the new **DynamicValue** data type.</span></span>
  
    
    
<span data-ttu-id="339fa-112">Пример с файлом readme доступен по ссылке:  [Рабочий процесс SharePoint: вызов внешней веб-службы](http://code.msdn.microsoft.com/SharePoint-workflow-48ea87d4).</span><span class="sxs-lookup"><span data-stu-id="339fa-112">The sample, along with a readme file, is available here:  [SharePoint workflow: Call an external web service](http://code.msdn.microsoft.com/SharePoint-workflow-48ea87d4)</span></span>
  
    
    

### <a name="sharepoint-workflow-create-a-custom-action"></a><span data-ttu-id="339fa-113">Рабочий процесс SharePoint: создание настраиваемого действия</span><span class="sxs-lookup"><span data-stu-id="339fa-113">SharePoint workflow: Create a custom action</span></span>

<span data-ttu-id="339fa-p103">В этом примере Visual Studio используется для создания рабочего процесса, который вызывает внешнюю веб-службу. При вызове веб-службы рабочий процесс также использует новый тип данных **DynamicValue**. Часть рабочего процесса, которая вызывает веб-службу и извлекает сведения из ответа, находится внутри настраиваемого действия, **GetNWCustomerDetailsWorkflow**.</span><span class="sxs-lookup"><span data-stu-id="339fa-p103">This sample uses Visual Studio to demonstrate creating a workflow that calls an external web service. In calling the web service, the workflow also uses the new **DynamicValue** data type. The part of the workflow that calls the web service and extracts the details from the response is contained within a custom activity, **GetNWCustomerDetailsWorkflow**.</span></span>
  
    
    
<span data-ttu-id="339fa-117">Пример с файлом readme доступен по ссылке:  [Рабочий процесс SharePoint: создание настраиваемого действия](http://code.msdn.microsoft.com/SharePoint-workflow-41e5c0f9).</span><span class="sxs-lookup"><span data-stu-id="339fa-117">The sample, along with a readme file, is available here:  [SharePoint workflow: Create a custom action](http://code.msdn.microsoft.com/SharePoint-workflow-41e5c0f9)</span></span>
  
    
    

### <a name="sharepoint-workflow-sales-tax-calculator"></a><span data-ttu-id="339fa-118">Рабочий процесс SharePoint: калькулятор налога на продажу</span><span class="sxs-lookup"><span data-stu-id="339fa-118">SharePoint workflow: Sales tax calculator</span></span>

<span data-ttu-id="339fa-119">В этом исчерпывающем примере рабочий процесс использует веб-службу, чтобы получить соответствующую налоговую ставку в зависимости от местоположения клиента, а затем использует базовую цену, чтобы вычислить налог на продажу и общую стоимость.</span><span class="sxs-lookup"><span data-stu-id="339fa-119">In this end-to-end sample, the workflow uses a web service to obtain the appropriate tax rate based on a purchaser's location, and then uses the base price to calculate the sales tax and total price.</span></span>
  
    
    
<span data-ttu-id="339fa-120">Пример с файлом readme доступен по ссылке:  [Рабочий процесс SharePoint: калькулятор налога на продажу](http://code.msdn.microsoft.com/SharePoint-workflow-f7a1a8ba).</span><span class="sxs-lookup"><span data-stu-id="339fa-120">The sample, along with a readme file, is available here:  [SharePoint workflow: Sales tax calculator](http://code.msdn.microsoft.com/SharePoint-workflow-f7a1a8ba)</span></span>
  
    
    

### <a name="sharepoint-workflow-use-a-task-action-in-sharepoint-designer"></a><span data-ttu-id="339fa-121">Рабочий процесс SharePoint: использование действия задачи в SharePoint Designer</span><span class="sxs-lookup"><span data-stu-id="339fa-121">SharePoint workflow: Use a task action in SharePoint Designer</span></span>

<span data-ttu-id="339fa-122">Расширенное пошаговое руководство по реализации действий задач в рабочем процессе, созданном с помощью Microsoft SharePoint Designer 2013.</span><span class="sxs-lookup"><span data-stu-id="339fa-122">An extended walkthrough of the process of implementing task actions in a workflow created using Microsoft SharePoint Designer 2013.</span></span>
  
    
    
<span data-ttu-id="339fa-123">Пример с файлом readme доступен по ссылке:  [Рабочий процесс SharePoint: использование действия задачи в SharePoint Designer](http://code.msdn.microsoft.com/SharePoint-workflow-942a5441).</span><span class="sxs-lookup"><span data-stu-id="339fa-123">The sample, along with a readme file, is available here:  [SharePoint workflow: Using a task action in SharePoint Designer](http://code.msdn.microsoft.com/SharePoint-workflow-942a5441)</span></span>
  
    
    

### <a name="sharepoint-workflow-workflow-om-in-a-sharepoint-app"></a><span data-ttu-id="339fa-124">Рабочий процесс SharePoint: объектная модель рабочих процессов в приложении для SharePoint</span><span class="sxs-lookup"><span data-stu-id="339fa-124">SharePoint workflow: Workflow OM in a SharePoint app</span></span>

<span data-ttu-id="339fa-125">Пример кода **Рабочий процесс SharePoint: объектная модель рабочих процессов в приложении для SharePoint** представляет собой размещаемое в SharePoint приложение, которое использует JSOM рабочих процессов SharePoint для развертывания определений рабочих процессов на сайт приложения и "родительский сайт" (то есть сайт SharePoint, на котором размещается приложение).</span><span class="sxs-lookup"><span data-stu-id="339fa-125">The **SharePoint workflow: Workflow OM in a SharePoint app** code sample is an example of an interactive SharePoint-hosted app that uses the SharePoint workflow JSOM to deploy workflow definitions to both an app web and to a "parent web" (that is, a SharePoint web that is hosting the app).</span></span>
  
    
    
<span data-ttu-id="339fa-126">Вы можете найти этот пример кода здесь:  [Рабочий процесс SharePoint: объектная модель рабочих процессов в приложении для SharePoint](http://code.msdn.microsoft.com/SharePoint-workflow-050f5211).</span><span class="sxs-lookup"><span data-stu-id="339fa-126">You can locate the sample code here:  [SharePoint workflow: Workflow OM in a SharePoint app](http://code.msdn.microsoft.com/SharePoint-workflow-050f5211).</span></span>
  
    
    

## <a name="additional-resources"></a><span data-ttu-id="339fa-127">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="339fa-127">Additional resources</span></span>
<span data-ttu-id="339fa-128"><a name="bkm_additional"> </a></span><span class="sxs-lookup"><span data-stu-id="339fa-128"></span></span>


-  [<span data-ttu-id="339fa-129">Общие сведения о рабочих процессах в SharePoint</span><span class="sxs-lookup"><span data-stu-id="339fa-129">Get started with workflows in SharePoint</span></span>](get-started-with-workflows-in-sharepoint)
    
  
-  [<span data-ttu-id="339fa-130">Установка и настройка диспетчера рабочих процессов SharePoint</span><span class="sxs-lookup"><span data-stu-id="339fa-130">Set up and configure SharePoint Workflow Manager</span></span>](set-up-and-configure-sharepoint-workflow-manager)
    
  
-  [<span data-ttu-id="339fa-131">Что нового в рабочих процессах для SharePoint</span><span class="sxs-lookup"><span data-stu-id="339fa-131">What's new in workflows for SharePoint</span></span>](what-s-new-in-workflows-for-sharepoint)
    
  
-  [<span data-ttu-id="339fa-132">Справочник по действий рабочих процессов для SharePoint</span><span class="sxs-lookup"><span data-stu-id="339fa-132">Workflow actions and activities reference for SharePoint</span></span>](workflow-actions-and-activities-reference-for-sharepoint)
    
  
-  [<span data-ttu-id="339fa-133">Надстройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="339fa-133">SharePoint Add-ins</span></span>](http://msdn.microsoft.com/library/cd1eda9e-8e54-4223-93a9-a6ea0d18df70%28Office.15%29.aspx)
    
  

