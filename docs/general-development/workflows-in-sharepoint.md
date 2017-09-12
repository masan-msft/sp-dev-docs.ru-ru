---
title: "Рабочие процессы в SharePoint"
ms.prod: SHAREPOINT
ms.assetid: e0602371-ae22-44be-8a7e-9e47e9f046d6
ms.openlocfilehash: 9c92eda33073d1ee3c94e371b65938aa2e8204c4
ms.sourcegitcommit: d9e955bf9d5afd9ad8ae8304a3ddb85ac27b3406
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/06/2017
---
# <a name="workflows-in-sharepoint"></a><span data-ttu-id="0e6a9-102">Рабочие процессы в SharePoint</span><span class="sxs-lookup"><span data-stu-id="0e6a9-102">Workflows in SharePoint</span></span>
<span data-ttu-id="0e6a9-p101">Сведения о платформе разработки Workflow Manager Client 1.0 и сценариях рабочего процесса для SharePoint. Выход SharePoint отмечен появлением Workflow Manager Client 1.0 в качестве новой платформы рабочих процессов SharePoint. В рабочих процессах SharePoint, созданных на основе Windows Workflow Foundation 4, представлен ряд новых возможностей и расширений функциональности. Общие сведения о новых особенностях рабочих процессов SharePoint см. в статье  [Что нового в рабочих процессах для SharePoint](what-s-new-in-workflows-for-sharepoint).</span><span class="sxs-lookup"><span data-stu-id="0e6a9-p101">Learn about the Workflow Manager Client 1.0 authoring framework and workflow scenarios for SharePoint. SharePoint marks the introduction of Workflow Manager Client 1.0 as the new foundation for SharePoint workflows. Built on Windows Workflow Foundation 4, SharePoint workflows offer a new range of capabilities and enhancements. For an overview of the new flavor of workflows for SharePoint, see  [What's new in workflows for SharePoint](what-s-new-in-workflows-for-sharepoint).</span></span>
  
    
    

<span data-ttu-id="0e6a9-107">Дополнительные сведения о том, как настроить приложение Workflow Manager Client 1.0 и связать его с SharePoint для обеспечения правильной работы, см. в статье  [Установка и настройка диспетчера рабочих процессов SharePoint](set-up-and-configure-sharepoint-workflow-manager).</span><span class="sxs-lookup"><span data-stu-id="0e6a9-107">For information about setting up Workflow Manager Client 1.0 and pairing it to function correctly with SharePoint, see  [Set up and configure SharePoint Workflow Manager](set-up-and-configure-sharepoint-workflow-manager).</span></span>
## <a name="in-this-section"></a><span data-ttu-id="0e6a9-108">В этом разделе:</span><span class="sxs-lookup"><span data-stu-id="0e6a9-108">In this section</span></span>


-  [<span data-ttu-id="0e6a9-109">Общие сведения о рабочих процессах в SharePoint</span><span class="sxs-lookup"><span data-stu-id="0e6a9-109">Get started with workflows in SharePoint</span></span>](get-started-with-workflows-in-sharepoint)
    
  
-  [<span data-ttu-id="0e6a9-110">Что нового в рабочих процессах для SharePoint</span><span class="sxs-lookup"><span data-stu-id="0e6a9-110">What's new in workflows for SharePoint</span></span>](what-s-new-in-workflows-for-sharepoint)
    
  
-  [<span data-ttu-id="0e6a9-111">Основные сведения о рабочих процессах в SharePoint</span><span class="sxs-lookup"><span data-stu-id="0e6a9-111">SharePoint workflow fundamentals</span></span>](sharepoint-workflow-fundamentals)
    
  
-  [<span data-ttu-id="0e6a9-112">Рекомендации по разработке рабочих процессов SharePoint</span><span class="sxs-lookup"><span data-stu-id="0e6a9-112">SharePoint workflow development best practices</span></span>](sharepoint-workflow-development-best-practices)
    
  
-  [<span data-ttu-id="0e6a9-113">С помощью командлета связывания Register-SPWorkflowService</span><span class="sxs-lookup"><span data-stu-id="0e6a9-113">Using the pairing cmdlet Register-SPWorkflowService</span></span>](using-the-pairing-cmdlet-register-spworkflowservice)
    
  
-  [<span data-ttu-id="0e6a9-114">Разработка рабочих процессов в SharePoint Designer и Visio</span><span class="sxs-lookup"><span data-stu-id="0e6a9-114">Workflow development in SharePoint Designer and Visio</span></span>](workflow-development-in-sharepoint-designer-and-visio)
    
  
-  [<span data-ttu-id="0e6a9-115">Разработка рабочих процессов в SharePoint с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0e6a9-115">Develop SharePoint workflows using Visual Studio</span></span>](develop-sharepoint-workflows-using-visual-studio)
    
  
-  [<span data-ttu-id="0e6a9-116">Справочник по действий рабочих процессов для SharePoint</span><span class="sxs-lookup"><span data-stu-id="0e6a9-116">Workflow actions and activities reference for SharePoint</span></span>](workflow-actions-and-activities-reference-for-sharepoint)
    
  

## <a name="related-sections"></a><span data-ttu-id="0e6a9-117">Связанные разделы</span><span class="sxs-lookup"><span data-stu-id="0e6a9-117">Related sections</span></span>


-  [<span data-ttu-id="0e6a9-118">Обзор разработки решений с помощью SharePoint</span><span class="sxs-lookup"><span data-stu-id="0e6a9-118">SharePoint development overview</span></span>](sharepoint-development-overview)
    
  
-  [<span data-ttu-id="0e6a9-119">Добавление возможностей SharePoint</span><span class="sxs-lookup"><span data-stu-id="0e6a9-119">Add SharePoint capabilities</span></span>](add-sharepoint-capabilities)
    
  
-  [<span data-ttu-id="0e6a9-120">Установка и настройка диспетчера рабочих процессов SharePoint</span><span class="sxs-lookup"><span data-stu-id="0e6a9-120">Set up and configure SharePoint Workflow Manager</span></span>](set-up-and-configure-sharepoint-workflow-manager)
    
    <span data-ttu-id="0e6a9-121">Дополнительные сведения о рабочих процессах сайтов SharePoint см. в  [статье блога Sympraxis Consulting: циклический просмотр контента в рабочем процессе сайта SharePoint](http://sympmarc.com/2016/01/14/looping-through-content-in-a-sharepoint-site-workflow-part-1-introduction)</span><span class="sxs-lookup"><span data-stu-id="0e6a9-121">For more information about SharePoint site workflows, see  [Blog article from Sympraxis Consulting: Looping Through Content in a SharePoint Site Workflow](http://sympmarc.com/2016/01/14/looping-through-content-in-a-sharepoint-site-workflow-part-1-introduction)</span></span>
    
  

