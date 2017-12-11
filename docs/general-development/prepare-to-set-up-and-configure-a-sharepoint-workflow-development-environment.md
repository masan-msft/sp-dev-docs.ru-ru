---
title: "Подготовка к Установка и настройка среды разработки рабочего процесса SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: b6a3321f-4131-4a8e-9cb7-7a1b4ab9e26b
ms.openlocfilehash: 9d6afa7404fb31ad62e386f4204e1ae268e9acf9
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="prepare-to-set-up-and-configure-a-sharepoint-workflow-development-environment"></a><span data-ttu-id="d9487-102">Подготовка к Установка и настройка среды разработки рабочего процесса SharePoint</span><span class="sxs-lookup"><span data-stu-id="d9487-102">Prepare to set up and configure a SharePoint workflow development environment</span></span>
<span data-ttu-id="d9487-103">Узнайте, как настроить среду разработки рабочего процесса для разработки рабочих процессов SharePoint в качестве самостоятельных [приложений для SharePoint](http://msdn.microsoft.com/library/fp179930.aspx) с помощью Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="d9487-103">Learn how to set up a workflow development environment to develop SharePoint workflows as free-standing  [apps for SharePoint](http://msdn.microsoft.com/library/fp179930.aspx) by using Visual Studio 2012.</span></span>
## <a name="overview-of-workflow-development-in-sharepoint"></a><span data-ttu-id="d9487-104">Общие сведения о разработке рабочих процессов в SharePoint</span><span class="sxs-lookup"><span data-stu-id="d9487-104">Overview of workflow development in SharePoint</span></span>

<span data-ttu-id="d9487-105">Несмотря на то, что рабочие процессы были частью SharePoint начиная с более ранними версиями, рабочих процессов для SharePoint — это много расширенные и улучшенные возможности платформы.</span><span class="sxs-lookup"><span data-stu-id="d9487-105">Although workflows have been a part of SharePoint since early versions, workflows for SharePoint are a much enhanced and improved platform.</span></span> 
  
    
    

- <span data-ttu-id="d9487-106">Во-первых рабочие процессы SharePoint теперь основанные на  [Windows Workflow Foundation 4.5](http://msdn.microsoft.com/library/dd489441%28v=vs.110%29), которая является частью .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="d9487-106">First, SharePoint workflows are now built on  [Windows Workflow Foundation 4.5](http://msdn.microsoft.com/library/dd489441%28v=vs.110%29), which is part of the .NET Framework 4.5.</span></span>
    
  
- <span data-ttu-id="d9487-107">Во-вторых ядро выполнения рабочего процесса, [Диспетчер рабочих процессов](http://msdn.microsoft.com/library/windowsazure/jj193528%28v=azure.10%29.aspx), была отделена от SharePoint и выполняется независимо друг от друга.</span><span class="sxs-lookup"><span data-stu-id="d9487-107">Second, the workflow execution engine,  [Workflow Manager](http://msdn.microsoft.com/library/windowsazure/jj193528%28v=azure.10%29.aspx), has been decoupled from SharePoint and runs independently.</span></span> <span data-ttu-id="d9487-108">Это обеспечивает гибкость и масштабируемость.</span><span class="sxs-lookup"><span data-stu-id="d9487-108">This provides both flexibility and scalability.</span></span> <span data-ttu-id="d9487-109">(Внимание, что для обеспечения обратной совместимости обработчик прежних версий workflow 2010 остается частью SharePoint).</span><span class="sxs-lookup"><span data-stu-id="d9487-109">(Note that for backward compatibility, the legacy 2010 workflow engine remains a part of SharePoint.)</span></span>
    
  
- <span data-ttu-id="d9487-110">Вместо разработка рабочих процессов путем написания кода C#, создание рабочих процессов в Visual Studio с помощью конструктора рабочих процессов, поддерживающей декларативные выражения.</span><span class="sxs-lookup"><span data-stu-id="d9487-110">Instead of developing workflows by writing C# code, you now build workflows in Visual Studio using a workflow designer that uses declarative expressions.</span></span>
    
  
- <span data-ttu-id="d9487-111">Интеграция рабочих процессов SharePoint с новой модели приложений, что означает, что вы можете теперь реализовать рабочих процессов в SharePoint надстройки.</span><span class="sxs-lookup"><span data-stu-id="d9487-111">SharePoint workflows integrate with the new app model, which means you can now implement workflows in SharePoint Add-ins.</span></span>
    
  
- <span data-ttu-id="d9487-112">Вы также можете создавать рабочих процессов SharePoint с помощью SharePoint Designer 2013.</span><span class="sxs-lookup"><span data-stu-id="d9487-112">You can also develop SharePoint workflows using SharePoint Designer 2013.</span></span> <span data-ttu-id="d9487-113">Для получения дополнительных сведений см [Разработка рабочих процессов в SharePoint Designer и Visio](workflow-development-in-sharepoint-designer-and-visio.md).</span><span class="sxs-lookup"><span data-stu-id="d9487-113">For more information, see  [Workflow development in SharePoint Designer and Visio](workflow-development-in-sharepoint-designer-and-visio.md).</span></span>
    
  

### <a name="get-started"></a><span data-ttu-id="d9487-114">Начало работы</span><span class="sxs-lookup"><span data-stu-id="d9487-114">Get started</span></span>

<span data-ttu-id="d9487-115">Сначала off и познакомьтесь с новой модели приложений и концепцию Надстройки SharePoint, окунув на следующие:</span><span class="sxs-lookup"><span data-stu-id="d9487-115">First off, get acquainted with the new app model and the concepts underlying SharePoint Add-ins by dipping into the following:</span></span> 
  
    
    

|||
|:-----|:-----|
| [<span data-ttu-id="d9487-116">SharePoint для разработчиков</span><span class="sxs-lookup"><span data-stu-id="d9487-116">SharePoint for developers</span></span>](http://msdn.microsoft.com/en-us/sharepoint) <br/> |<span data-ttu-id="d9487-117">Портал для разработчиков на сайте SharePoint, где внимание уделяется приложений для SharePoint.</span><span class="sxs-lookup"><span data-stu-id="d9487-117">Portal to the SharePoint developer site, where the emphasis is on apps for SharePoint.</span></span>  <br/> |
| [<span data-ttu-id="d9487-118">Надстройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="d9487-118">SharePoint Add-ins</span></span>](http://msdn.microsoft.com/library/cd1eda9e-8e54-4223-93a9-a6ea0d18df70%28Office.15%29.aspx) <br/> |<span data-ttu-id="d9487-119">Узнайте, что такое приложений для SharePoint, зачем создавать их и базовых принципах, необходимых для их создания в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="d9487-119">Learn what apps for SharePoint are, why you should build them, and the concepts that are fundamental to building them in SharePoint.</span></span>  <br/> |
| [<span data-ttu-id="d9487-120">Новое название приложений для SharePoint</span><span class="sxs-lookup"><span data-stu-id="d9487-120">New name for apps for SharePoint</span></span>](http://msdn.microsoft.com/library/05b07b04-6c8b-4b7e-bd86-e32c589dfead%28Office.15%29.aspx) <br/> |<span data-ttu-id="d9487-121">Портал разработчиков сайт, предназначенный для создания приложений для Office и приложений для SharePoint.</span><span class="sxs-lookup"><span data-stu-id="d9487-121">Portal to a developer site devoted to building apps for Office and apps for SharePoint.</span></span>  <br/> |
| [<span data-ttu-id="d9487-122">Обзор разработки решений для SharePoint</span><span class="sxs-lookup"><span data-stu-id="d9487-122">SharePoint development overview</span></span>](sharepoint-development-overview.md) <br/> |<span data-ttu-id="d9487-123">SharePoint — это платформа разработки приложений для SharePoint и фермы решения.</span><span class="sxs-lookup"><span data-stu-id="d9487-123">SharePoint is a development platform for apps for SharePoint and farm solutions.</span></span> <span data-ttu-id="d9487-124">Познакомьтесь с возможностях и функциях SharePoint, чтобы начать разработку.</span><span class="sxs-lookup"><span data-stu-id="d9487-124">Get acquainted with the capabilities and features of SharePoint to start your development.</span></span>  <br/> |
| [<span data-ttu-id="d9487-125">Основные сведения о рабочих процессах в SharePoint</span><span class="sxs-lookup"><span data-stu-id="d9487-125">SharePoint workflow fundamentals</span></span>](sharepoint-workflow-fundamentals.md) <br/> |<span data-ttu-id="d9487-126">В этой статье представлен высокоуровневый обзор инфраструктуры рабочих процессов в SharePoint, в том числе описание архитектуры платформы и мост взаимодействия рабочих процессов.</span><span class="sxs-lookup"><span data-stu-id="d9487-126">Provides a high-level overview of the workflow infrastructure in SharePoint, including a view of the platform architecture and the workflow interop bridge.</span></span>  <br/> |
   
<span data-ttu-id="d9487-p104">Следующим шагом является убедитесь, что у вас есть установки среды разработки актуальных рабочего процесса. Не требуется для разработки на сервере SharePoint, но конечно требует установки SharePoint Server для разработки с помощью.</span><span class="sxs-lookup"><span data-stu-id="d9487-p104">Your next step is to ensure that you have an up-to-date workflow development environment installed. You don't need to develop on the SharePoint server machine, but of course you do need a SharePoint Server installation to develop against.</span></span>
  
    
    
<span data-ttu-id="d9487-p105">Ниже приведены компоненты, необходимые. Важно установить эти элементы в указанном порядке:</span><span class="sxs-lookup"><span data-stu-id="d9487-p105">Here are the components you need. It is important that you install these items in the order presented here:</span></span>
  
    
    

1. <span data-ttu-id="d9487-131">**Установка среды SharePoint**</span><span class="sxs-lookup"><span data-stu-id="d9487-131">**Install the SharePoint environment**</span></span>
    
  -  [<span data-ttu-id="d9487-132">Обновление SharePoint (KB2767999)</span><span class="sxs-lookup"><span data-stu-id="d9487-132">SharePoint update (KB2767999)</span></span>](http://support.microsoft.com/kb/2767999)
    
  
  - <span data-ttu-id="d9487-133">Кроме того можно подписаться на  [среды разработки Office 365](http://msdn.microsoft.com/library/office/apps/fp179924%28v=office.15%29)</span><span class="sxs-lookup"><span data-stu-id="d9487-133">Optionally, you can subscribe to an  [Office 365 development environment](http://msdn.microsoft.com/library/office/apps/fp179924%28v=office.15%29)</span></span>
    
  
2. <span data-ttu-id="d9487-134">**Установка среды диспетчера рабочих процессов**</span><span class="sxs-lookup"><span data-stu-id="d9487-134">**Install the Workflow Manager environment**</span></span>
    
  -  [<span data-ttu-id="d9487-135">Накопительный пакет диспетчера рабочих процессов версии 1.0 (KB2799754)</span><span class="sxs-lookup"><span data-stu-id="d9487-135">Workflow Manager 1.0 Cumulative (KB2799754)</span></span>](http://support.microsoft.com/kb/2799754/en-us)
    
  
3. <span data-ttu-id="d9487-136">**Установка среды разработки Visual Studio 2012**</span><span class="sxs-lookup"><span data-stu-id="d9487-136">**Install the Visual Studio 2012 development environment**</span></span>
    
  -  [<span data-ttu-id="d9487-137">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="d9487-137">Visual Studio 2012</span></span>](http://www.microsoft.com/visualstudio/eng/downloads#vs)
    
  
  -  [<span data-ttu-id="d9487-138">Visual Studio 2012 обновления 2 (KB2797912)</span><span class="sxs-lookup"><span data-stu-id="d9487-138">Visual Studio 2012 Update 2 (KB2797912)</span></span>](http://support.microsoft.com/kb/2797912)
    
  
  -  [<span data-ttu-id="d9487-139">Обновление .NET framework 4.5 (KB2750149)</span><span class="sxs-lookup"><span data-stu-id="d9487-139">.NET Framework 4.5 update (KB2750149)</span></span>](http://support.microsoft.com/kb/2750149/en-us)
    
  
  -  [<span data-ttu-id="d9487-140">Office Developer Tools для Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="d9487-140">Office Developer Tools for Visual Studio 2012</span></span>](http://aka.ms/OfficeDevToolsForVS2012)
    
  

### <a name="if-you-have-the-preview-version"></a><span data-ttu-id="d9487-141">Если установлена версия «Версия»</span><span class="sxs-lookup"><span data-stu-id="d9487-141">If you have the "Preview" version</span></span>

<span data-ttu-id="d9487-p106">Если предварительные (то есть, "Просмотр") версии SharePoint Server, Workflow Manager 1.0 или Инструменты разработчика Office для Visual Studio 2013 (версий до марта 2013 г.), необходимо обновить установки. Ниже приведен список соответствующих обновлений:</span><span class="sxs-lookup"><span data-stu-id="d9487-p106">If you have pre-release (that is, "Preview") versions of SharePoint Server, Workflow Manager 1.0, or Office Developer Tools for Visual Studio 2013 (versions prior to March 2013), you must update your installation. Following is a list of appropriate updates:</span></span>
  
    
    

-  [<span data-ttu-id="d9487-144">Обновление SharePoint (KB2767999)</span><span class="sxs-lookup"><span data-stu-id="d9487-144">SharePoint update (KB2767999)</span></span>](http://support.microsoft.com/kb/2767999)
    
  
-  [<span data-ttu-id="d9487-145">Microsoft Azure шины 1.0 накопительный пакет обновления (KB2799752)</span><span class="sxs-lookup"><span data-stu-id="d9487-145">Microsoft Azure Service Bus 1.0 Cumulative Update (KB2799752)</span></span>](http://support.microsoft.com/kb/2799752/en-us)
    
  
-  [<span data-ttu-id="d9487-146">Накопительный пакет диспетчера рабочих процессов версии 1.0 (KB2799754)</span><span class="sxs-lookup"><span data-stu-id="d9487-146">Workflow Manager 1.0 Cumulative (KB2799754)</span></span>](http://support.microsoft.com/kb/2799754/en-us)
    
  

### <a name="you-must-also-update-workflow-projects-created-with-the-preview-version"></a><span data-ttu-id="d9487-147">Также необходимо обновить рабочий процесс проекты, созданные с версией «Версия»</span><span class="sxs-lookup"><span data-stu-id="d9487-147">You must also update workflow projects created with the "Preview" version</span></span>

<span data-ttu-id="d9487-p107">Версии компонентов Visual Studio рабочего процесса и их соответствующие обновления внесены важные изменения, которые улучшают работу производительность, масштабируемость и надежность. К сожалению эти обновления необходимо обновить проектов рабочих процессов, созданных с помощью средства просмотра.</span><span class="sxs-lookup"><span data-stu-id="d9487-p107">The release version of the Visual Studio workflow components and their related updates introduce important changes that enhance performance, scalability, and reliability. Unfortunately, these upgrades require you to update workflow projects that you created using the Preview tools.</span></span>
  
    
    
<span data-ttu-id="d9487-150">Чтобы упростить этот процесс, мы предоставляют средство преобразования, можно получить через CodePlex.</span><span class="sxs-lookup"><span data-stu-id="d9487-150">To make this process easier, we provide a conversion tool that you can get through CodePlex.</span></span> <span data-ttu-id="d9487-151">Средство вызывается [Конвертер рабочего процесса SharePoint для Visual Studio 2012](http://wfconverter.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="d9487-151">The tool is called the  [SharePoint Workflow Converter for Visual Studio 2012](http://wfconverter.codeplex.com/).</span></span>
  
    
    
<span data-ttu-id="d9487-152">Ниже представлена сводка изменений, которые необходимо обновить проекты рабочего процесса:</span><span class="sxs-lookup"><span data-stu-id="d9487-152">Here is a summary of changes that require you to update your workflow projects:</span></span>
  
    
    

- <span data-ttu-id="d9487-153">Справочные материалы действия, которые **Item Guid** заменяются **Item Id**. Эти изменения имеют важных последствия:</span><span class="sxs-lookup"><span data-stu-id="d9487-153">Activity references to **Item Guid** are replaced by **Item Id**. This change has important consequences:</span></span>
    
  - <span data-ttu-id="d9487-154">[LookupSPListItemGuid](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.Activities.LookupSPListItemGuid.aspx) и [GetCurrentItemGuid](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.Activities.GetCurrentItemGuid.aspx) действия удаляются из инструментарий; их замены действий, **LookupSPListItemId** и **GetCurrentItemId**.</span><span class="sxs-lookup"><span data-stu-id="d9487-154">The  [LookupSPListItemGuid](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.Activities.LookupSPListItemGuid.aspx) and [GetCurrentItemGuid](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.Activities.GetCurrentItemGuid.aspx) activities are removed from the tooling; their replacement activities are **LookupSPListItemId** and **GetCurrentItemId**.</span></span>
    
  
  - <span data-ttu-id="d9487-p109">На другие задачи, использующие **Item Guid**вы найдете **Item Id** добавлена и **Item Guid** скрытым. Существующие проекты, использующие **Item Guid** будет продолжать работать (за исключением очень большие списки, содержащие более 5000 элементов, которая является одной из причин для изменения).</span><span class="sxs-lookup"><span data-stu-id="d9487-p109">For other activities that use **Item Guid**, you will find **Item Id** added and **Item Guid** hidden. Your existing projects that use **Item Guid** will continue to work (except on very large lists with more than 5000 items, which is one of the reasons for the change).</span></span>
    
  
- <span data-ttu-id="d9487-157">Существует новый формат упаковки для рабочих процессов в приложениях.</span><span class="sxs-lookup"><span data-stu-id="d9487-157">There is a new packaging format for workflows in apps.</span></span>
    
  
- <span data-ttu-id="d9487-158">Справочник по сборке действий рабочего процесса в XAML был изменен для указания на новый прокси-сервера во время разработки сборки вместо фактических действий сборки пакета обновления.</span><span class="sxs-lookup"><span data-stu-id="d9487-158">The workflow activities assembly reference in XAML has been changed to point to a new design-time proxy assembly instead of the actual SP activities assembly.</span></span>
    
  

## <a name="see-also"></a><span data-ttu-id="d9487-159">См. также</span><span class="sxs-lookup"><span data-stu-id="d9487-159">See also</span></span>
<span data-ttu-id="d9487-160"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="d9487-160"><a name="bk_addresources"> </a></span></span>


-  [<span data-ttu-id="d9487-161">Настройка локальной среды разработки надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="d9487-161">Set up an on-premises development environment for SharePoint Add-ins</span></span>](http://msdn.microsoft.com/library/b0878c12-27c9-4eea-ae3b-7e79e5a8838d%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="d9487-162">Что нового в рабочих процессах для SharePoint</span><span class="sxs-lookup"><span data-stu-id="d9487-162">What's new in workflows for SharePoint</span></span>](what-s-new-in-workflows-for-sharepoint.md)
    
  
-  [<span data-ttu-id="d9487-163">Разработка рабочих процессов в SharePoint Designer и Visio</span><span class="sxs-lookup"><span data-stu-id="d9487-163">Workflow development in SharePoint Designer and Visio</span></span>](workflow-development-in-sharepoint-designer-and-visio.md)
    
  
-  [<span data-ttu-id="d9487-164">Рабочие процессы в SharePoint</span><span class="sxs-lookup"><span data-stu-id="d9487-164">Workflows in SharePoint</span></span>](workflows-in-sharepoint.md)
    
  

