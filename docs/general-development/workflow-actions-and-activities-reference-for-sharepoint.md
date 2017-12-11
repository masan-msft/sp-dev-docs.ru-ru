---
title: "Справочник по действий рабочих процессов для SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 88e09f75-480f-4a68-87a6-b496350345cc
ms.openlocfilehash: 4f808bbc0e8d6f08d2779a1e3d6b2343f9a5dd01
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="workflow-actions-and-activities-reference-for-sharepoint"></a><span data-ttu-id="59ee0-102">Справочник по действий рабочих процессов для SharePoint</span><span class="sxs-lookup"><span data-stu-id="59ee0-102">Workflow actions and activities reference for SharePoint</span></span>
<span data-ttu-id="59ee0-103">Сведения о действия рабочего процесса, доступных для разработки рабочего процесса в SharePoint Designer 2013 и классы действий рабочего процесса, доступные для разработчиков рабочих процессов с помощью Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="59ee0-103">Learn about the workflow actions that are available for workflow authoring in SharePoint Designer 2013, and the workflow activity classes that are available to workflow developers using Visual Studio 2012.</span></span>
## <a name="workflow-activities-and-actions"></a><span data-ttu-id="59ee0-104">Действия рабочего процесса и действия</span><span class="sxs-lookup"><span data-stu-id="59ee0-104">Workflow activities and actions</span></span>
<span data-ttu-id="59ee0-105"><a name="bkm_Activities"> </a></span><span class="sxs-lookup"><span data-stu-id="59ee0-105"></span></span>

<span data-ttu-id="59ee0-p101">Рабочий процесс действия представления объектов на уровне кода, которые обрабатывают вызовы методов различным интерфейсам API, которые образуют поведение рабочего процесса. Взаимодействие с действий рабочего процесса в коде, с помощью или другой среде разработки.</span><span class="sxs-lookup"><span data-stu-id="59ee0-p101">Workflow activities represent the code-level objects that handle method calls to the various APIs that drive workflow behaviors. You interact with workflow activities in code, using or another development environment.</span></span>
  
    
    
<span data-ttu-id="59ee0-108">Чтобы получить список доступных действий видеть [классы действий рабочего процесса в SharePoint](workflow-activity-classes-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="59ee0-108">For a list of available activities, see  [Workflow activity classes in SharePoint](workflow-activity-classes-in-sharepoint.md).</span></span>
  
    
    
<span data-ttu-id="59ee0-p102">С другой стороны, бизнес-процессов действия являются программы-оболочки для объектов, которые инкапсулируют этих базовых действий и представить их в форме понятное SharePoint Designer. Взаимодействие с действия рабочего процесса в SharePoint Designer.</span><span class="sxs-lookup"><span data-stu-id="59ee0-p102">On the other hand, workflow actions are wrapper objects that encapsulate these underlying activities and present them in a user-friendly form in SharePoint Designer. You interact with workflow actions in SharePoint Designer.</span></span>
  
    
    
<span data-ttu-id="59ee0-111">Список действий рабочих процессов недоступны в разделе [действия рабочего процесса для быстрого доступа (платформа рабочих процессов SharePoint)](workflow-actions-quick-reference-sharepoint-workflow-platform.md) и [действия рабочего процесса можно получить с моста взаимодействия рабочих процессов](workflow-actions-available-using-the-workflow-interop-bridge.md).</span><span class="sxs-lookup"><span data-stu-id="59ee0-111">For a list of available workflow actions, see  [Workflow actions quick reference (SharePoint Workflow platform)](workflow-actions-quick-reference-sharepoint-workflow-platform.md) and [Workflow actions available using the workflow interop bridge](workflow-actions-available-using-the-workflow-interop-bridge.md).</span></span>
  
    
    

## <a name="windows-workflow-foundation-40-activities"></a><span data-ttu-id="59ee0-112">Действия Windows Workflow Foundation 4.0</span><span class="sxs-lookup"><span data-stu-id="59ee0-112">Windows Workflow Foundation 4.0 activities</span></span>
<span data-ttu-id="59ee0-113"><a name="bkm_WF4"> </a></span><span class="sxs-lookup"><span data-stu-id="59ee0-113"></span></span>

<span data-ttu-id="59ee0-p103">Несмотря на то, что SharePoint платформу и инфраструктуру позволяют специальный активности классы для создания настраиваемых рабочих процессов SharePoint, можно использовать одно из действий, представленными Windows Workflow Foundation (WF) 4.0. Эти классы действий WF 4.0, доступны в Microsoft .NET Framework 4 в пространстве имен  [System.Activities.Statements](http://msdn.microsoft.com/en-us/library/system.activities.statements.aspx) .</span><span class="sxs-lookup"><span data-stu-id="59ee0-p103">Although the SharePoint platform and infrastructure provide you with specially crafted activity classes for creating custom SharePoint workflows, you can also use any of the activities that are provided by Windows Workflow Foundation (WF) 4.0. These WF 4.0 activity classes are available in the Microsoft .NET Framework 4 in the  [System.Activities.Statements](http://msdn.microsoft.com/en-us/library/system.activities.statements.aspx) namespace.</span></span>
  
    
    
<span data-ttu-id="59ee0-p104">Классы действий WF 4.0 представлены некоторые полезные возможности, которые не может найти в библиотеке классов активности SharePoint. Например WF 4.0 включает в себя класс **If**, который позволяет создавать условного действия. Кроме того можно использовать действие [System.ServiceModel.Activities.Send](http://msdn.microsoft.com/en-us/library/system.servicemodel.activities.send.aspx) для подключения к веб-служб.</span><span class="sxs-lookup"><span data-stu-id="59ee0-p104">The WF 4.0 activity classes provide some useful features that you may not find in the SharePoint activity class library. For example, WF 4.0 includes the **If** class, which allows you to create conditional activities. Additionally, you can use the [System.ServiceModel.Activities.Send](http://msdn.microsoft.com/en-us/library/system.servicemodel.activities.send.aspx) activity to connect to web services.</span></span>
  
    
    

## <a name="in-this-section"></a><span data-ttu-id="59ee0-119">В этом разделе</span><span class="sxs-lookup"><span data-stu-id="59ee0-119">In this section</span></span>
<span data-ttu-id="59ee0-120"><a name="bkm_inthissection"> </a></span><span class="sxs-lookup"><span data-stu-id="59ee0-120"></span></span>


-  [<span data-ttu-id="59ee0-121">Классы действий рабочего процесса в SharePoint</span><span class="sxs-lookup"><span data-stu-id="59ee0-121">Workflow activity classes in SharePoint</span></span>](workflow-activity-classes-in-sharepoint.md)
    
  
-  [<span data-ttu-id="59ee0-122">Краткий справочник по действиям рабочего процесса (платформа рабочих процессов в SharePoint)</span><span class="sxs-lookup"><span data-stu-id="59ee0-122">Workflow actions quick reference (SharePoint Workflow platform)</span></span>](workflow-actions-quick-reference-sharepoint-workflow-platform.md)
    
  
-  [<span data-ttu-id="59ee0-123">Действия рабочего процесса можно получить с моста взаимодействия рабочих процессов</span><span class="sxs-lookup"><span data-stu-id="59ee0-123">Workflow actions available using the workflow interop bridge</span></span>](workflow-actions-available-using-the-workflow-interop-bridge.md)
    
  

## <a name="see-also"></a><span data-ttu-id="59ee0-124">См. также</span><span class="sxs-lookup"><span data-stu-id="59ee0-124">See also</span></span>
<span data-ttu-id="59ee0-125"><a name="bkm_addlres"> </a></span><span class="sxs-lookup"><span data-stu-id="59ee0-125"></span></span>


-  [<span data-ttu-id="59ee0-126">Разработка рабочих процессов в SharePoint с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="59ee0-126">Develop SharePoint workflows using Visual Studio</span></span>](develop-sharepoint-workflows-using-visual-studio.md)
    
  
-  [<span data-ttu-id="59ee0-127">Основные сведения о рабочих процессах в SharePoint</span><span class="sxs-lookup"><span data-stu-id="59ee0-127">SharePoint workflow fundamentals</span></span>](sharepoint-workflow-fundamentals.md)
    
  
-  [<span data-ttu-id="59ee0-128">Рабочие процессы в SharePoint</span><span class="sxs-lookup"><span data-stu-id="59ee0-128">Workflows in SharePoint</span></span>](workflows-in-sharepoint.md)
    
  

