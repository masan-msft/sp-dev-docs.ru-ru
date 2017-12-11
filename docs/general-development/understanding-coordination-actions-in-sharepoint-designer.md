---
title: "Общие сведения о действия по координации в SharePoint Designer 2013"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 33fbcf91-0a5d-47ab-85a9-9d2d556a204d
ms.openlocfilehash: 2f70d861564d5c1496d72a479e39329cfdc15a88
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="understanding-coordination-actions-in-sharepoint-designer-2013"></a><span data-ttu-id="7014d-102">Общие сведения о действия по координации в SharePoint Designer 2013</span><span class="sxs-lookup"><span data-stu-id="7014d-102">Understanding Coordination actions in SharePoint Designer 2013</span></span>
<span data-ttu-id="7014d-103">Действия по координации в SharePoint Designer 2013 позволяют запустить рабочий процесс, построенный на платформе рабочего процесса SharePoint 2010 в рабочий процесс, построенный на платформе рабочих процессов SharePoint.</span><span class="sxs-lookup"><span data-stu-id="7014d-103">Coordination Actions in SharePoint Designer 2013 are designed to start a workflow built on the SharePoint 2010 Workflow platform from within a workflow built on the SharePoint Workflow platform.</span></span>

   

## <a name="coordination-actions-in-sharepoint-designer-2013"></a><span data-ttu-id="7014d-104">Действия по координации в SharePoint Designer 2013</span><span class="sxs-lookup"><span data-stu-id="7014d-104">Coordination Actions in SharePoint Designer 2013</span></span>
<span data-ttu-id="7014d-105"><a name="section1"> </a></span><span class="sxs-lookup"><span data-stu-id="7014d-105"></span></span>

<span data-ttu-id="7014d-106">Существует два действия по координации в SharePoint Designer 2013.</span><span class="sxs-lookup"><span data-stu-id="7014d-106">There are two Coordination Actions available in SharePoint Designer 2013.</span></span> <span data-ttu-id="7014d-107">В обоих случаях доступны только для платформы рабочих процессов SharePoint.</span><span class="sxs-lookup"><span data-stu-id="7014d-107">Both actions are only available for the SharePoint Workflow platform.</span></span> <span data-ttu-id="7014d-108">Эти действия, являются:</span><span class="sxs-lookup"><span data-stu-id="7014d-108">These actions are:</span></span>
  
    
    

- <span data-ttu-id="7014d-109">Запуск рабочего процесса списка: используется для запуска рабочего процесса, разработанных для конкретного списка.</span><span class="sxs-lookup"><span data-stu-id="7014d-109">Start a List Workflow: Used to start a workflow developed for a specific list.</span></span>
    
  
- <span data-ttu-id="7014d-110">Запуск рабочего процесса сайта: используется для запуска рабочего процесса, разработанных для сайта.</span><span class="sxs-lookup"><span data-stu-id="7014d-110">Start a Site Workflow: Used to start a workflow developed for the site.</span></span>
    
  
<span data-ttu-id="7014d-111">Действия по координации отображаются в раскрывающемся меню **действий** при построении рабочего процесса на платформе рабочих процессов SharePoint, как показано на рисунке.</span><span class="sxs-lookup"><span data-stu-id="7014d-111">Coordination Actions appear in the **Actions** drop-down menu when you build a workflow based on the SharePoint Workflow platform, as shown in the figure.</span></span>
  
    
    

<span data-ttu-id="7014d-112">**Рисунок: Действия по координации в SharePoint Designer**</span><span class="sxs-lookup"><span data-stu-id="7014d-112">**Figure: Coordination Actions in SharePoint Designer**</span></span>

  
    
    

  
    
    
![Действия по координации в SharePoint Designer](../images/SPD15-CoordinationActions.png)
  
    
    
<span data-ttu-id="7014d-114">Оба действия позволяют запустить рабочий процесс, построенный на платформе рабочего процесса SharePoint 2010 из рабочего процесса, построенный на платформе рабочих процессов SharePoint.</span><span class="sxs-lookup"><span data-stu-id="7014d-114">Both actions are designed to start a workflow built on the SharePoint 2010 Workflow platform from a workflow built on the SharePoint Workflow platform.</span></span>
  
    
    

    
> <span data-ttu-id="7014d-115">**Важные:** Действия по координации поддерживают только запуска рабочего процесса на основе платформы рабочего процесса SharePoint 2010 из рабочего процесса на основании платформы рабочих процессов SharePoint.</span><span class="sxs-lookup"><span data-stu-id="7014d-115">**Important:** The coordination actions only support starting a workflow based on the SharePoint 2010 Workflow platform from a workflow based on the SharePoint Workflow platform.</span></span> <span data-ttu-id="7014d-116">Начало рабочий процесс, построенный на платформе рабочих процессов SharePoint в рабочий процесс, построенный на ту же платформу не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="7014d-116">Starting a workflow built on the SharePoint Workflow platform from within a workflow built on the same platform is not supported.</span></span> 
  
    
    


## <a name="using-coordination-actions"></a><span data-ttu-id="7014d-117">С помощью действия по согласованию</span><span class="sxs-lookup"><span data-stu-id="7014d-117">Using Coordination Actions</span></span>
<span data-ttu-id="7014d-118"><a name="section2"> </a></span><span class="sxs-lookup"><span data-stu-id="7014d-118"></span></span>

<span data-ttu-id="7014d-119">Существует несколько действий, которые были исключены из платформы рабочих процессов SharePoint.</span><span class="sxs-lookup"><span data-stu-id="7014d-119">There are a number of actions that have been deprecated in the SharePoint Workflow platform.</span></span> <span data-ttu-id="7014d-120">Для учета устаревших рабочих процессов можно использовать действия по согласованию.</span><span class="sxs-lookup"><span data-stu-id="7014d-120">To accommodate legacy workflows you can use Coordination Actions.</span></span> <span data-ttu-id="7014d-121">Действия по координации можно использовать для запуска рабочего процесса списка или рабочий процесс сайта, созданный с помощью платформы рабочего процесса SharePoint 2010.</span><span class="sxs-lookup"><span data-stu-id="7014d-121">Coordination Actions can be used to start a List workflow or a Site workflow that has been built by using the SharePoint 2010 Workflow platform.</span></span>
  
    
    
<span data-ttu-id="7014d-122">Действия по координации включает в себя три редактируемые области, как показано на рисунке.</span><span class="sxs-lookup"><span data-stu-id="7014d-122">A Coordination Action includes three editable regions, as shown in the figure.</span></span>
  
    
    

<span data-ttu-id="7014d-123">**Рисунок: Запуск действия по координации рабочего процесса списка**</span><span class="sxs-lookup"><span data-stu-id="7014d-123">**Figure: Start a List Workflow coordination action**</span></span>

  
    
    

  
    
    
![Запуск действия по координации рабочего процесса списков](../images/SPD15-CoordinationActions2.png)
  
    
    
<span data-ttu-id="7014d-125">Три редактируемые области являются:</span><span class="sxs-lookup"><span data-stu-id="7014d-125">The three editable regions are:</span></span> 
  
    
    

- <span data-ttu-id="7014d-126">**Рабочий процесс списка SharePoint 2010** Выберите запускать рабочий процесс 2010.</span><span class="sxs-lookup"><span data-stu-id="7014d-126">**SharePoint 2010 list workflow** Select the 2010 workflow to start.</span></span>
    
  
- <span data-ttu-id="7014d-127">**Параметры** Параметры для отправки в рабочий процесс 2010.</span><span class="sxs-lookup"><span data-stu-id="7014d-127">**parameters** Parameters to send to the 2010 workflow.</span></span>
    
  
- <span data-ttu-id="7014d-128">**этот элемент** Элемент, который следует запускать рабочий процесс 2010 на.</span><span class="sxs-lookup"><span data-stu-id="7014d-128">**this item** The item which the 2010 workflow should be run on.</span></span>
    
  
<span data-ttu-id="7014d-p104">Щелкните редактируемое ссылку для ввода сведений. Например выберите запускать рабочий процесс 2010, щелкните ссылку **рабочего процесса списка SharePoint 2010**. Появится диалоговое окно, которое можно использовать для выбора рабочего процесса, как показано на рисунке.</span><span class="sxs-lookup"><span data-stu-id="7014d-p104">Click an editable link to enter information. For example, to select the 2010 workflow to start, click the link **SharePoint 2010 list workflow**. A dialog box appears that can be used to select the workflow, as shown in the figure.</span></span>
  
    
    

<span data-ttu-id="7014d-132">**Рисунок: Выбор рабочего процесса на основании платформы 2010**</span><span class="sxs-lookup"><span data-stu-id="7014d-132">**Figure: Selecting a workflow based on the 2010 platform**</span></span>

  
    
    

  
    
    
![Выбор рабочего процесса на основании платформы 2010](../images/SPD15-CoordinationActions3.png)
  
    
    

  
    
    

  
    
    

  
    
    
<span data-ttu-id="7014d-134">Экземпляры рабочих процессов платформы рабочего процесса SharePoint 2010, которые являются согласованных из в рамках рабочего процесса SharePoint отображается на странице состояния рабочего процесса в разделе вспомогательные рабочие процессы, как показано на рисунке.</span><span class="sxs-lookup"><span data-stu-id="7014d-134">The SharePoint 2010 Workflow platform workflow instances that are coordinated from within a SharePoint workflow are listed on the workflow status page in the Subworkflows section, as shown in the figure.</span></span>
  
    
    

<span data-ttu-id="7014d-135">**Рисунок: Страница состояния рабочего процесса с подпроцессами**</span><span class="sxs-lookup"><span data-stu-id="7014d-135">**Figure: The workflow status page lists the subworkflows**</span></span>

  
    
    

  
    
    
![Страница состояния рабочего процесса с подпроцессами.](../images/SPD15-CorrelationActions4.png)
  
    
    

  
    
    

  
    
    

## <a name="see-also"></a><span data-ttu-id="7014d-137">См. также</span><span class="sxs-lookup"><span data-stu-id="7014d-137">See also</span></span>
<span data-ttu-id="7014d-138"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="7014d-138"></span></span>


-  [<span data-ttu-id="7014d-139">Новые возможности рабочих процессов SharePoint</span><span class="sxs-lookup"><span data-stu-id="7014d-139">What's new in workflow in SharePoint</span></span>](http://msdn.microsoft.com/library/6ab8a28b-fa2f-4530-8b55-a7f663bf15ea.aspx)
    
  
-  [<span data-ttu-id="7014d-140">Начало работы с рабочими процессами SharePoint</span><span class="sxs-lookup"><span data-stu-id="7014d-140">Getting started with SharePoint workflow</span></span>](http://msdn.microsoft.com/library/cc73be76-a329-449f-90ab-86822b1c2ee8.aspx)
    
  
-  [<span data-ttu-id="7014d-141">Общие сведения о действия словаря в SharePoint Designer 2013</span><span class="sxs-lookup"><span data-stu-id="7014d-141">Understanding Dictionary actions in SharePoint Designer 2013</span></span>](understanding-dictionary-actions-in-sharepoint-designer.md)
    
  

  
    
    

