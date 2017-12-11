---
title: "Модуль записи VSS SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: e0f94ae99936f77f80b419c95d2d17acfd872345
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="sharepoint-workflow-development-best-practices"></a><span data-ttu-id="bd78b-102">Рекомендации по разработке рабочих процессов SharePoint</span><span class="sxs-lookup"><span data-stu-id="bd78b-102">SharePoint workflow development best practices</span></span>
<span data-ttu-id="bd78b-103">Содержит коллекцию советы и рекомендации для разработчиков, использующих Visual Studio для создания рабочих процессов в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="bd78b-103">Provides a collection of best practices for developers using Visual Studio to create workflows in SharePoint.</span></span>
## <a name="workflow-development-best-practices"></a><span data-ttu-id="bd78b-104">Рекомендации по разработке рабочих процессов</span><span class="sxs-lookup"><span data-stu-id="bd78b-104">Workflow development best practices</span></span>

<span data-ttu-id="bd78b-p101">Чтобы разработать без ошибок рабочих процессов для SharePoint, лучше всего, выполните некоторые общие рекомендации по работе или «практические советы». Это так ли вы используете SharePoint Designer 2013 или Visual Studio 2012 для разработки рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="bd78b-p101">To develop error-free workflows for SharePoint, it is best to follow some general guidelines, or "best practices." This is the case whether you are using SharePoint Designer 2013 or Visual Studio 2012 for workflow development.</span></span>
  
    
    

-  [<span data-ttu-id="bd78b-107">Приложения для SharePoint, которые содержат интегрированной рабочих процессов необходимо изменить тег в файле workflowmanifest.xml</span><span class="sxs-lookup"><span data-stu-id="bd78b-107">Apps for SharePoint that contain integrated workflows must edit a tag in the workflowmanifest.xml file</span></span>](sharepoint-workflow-development-best-practices.md#bkm_00)
    
  
-  [<span data-ttu-id="bd78b-108">При использовании действие журнала в список журналов, Дополнительные сведения  лучше</span><span class="sxs-lookup"><span data-stu-id="bd78b-108">When you use the Log To History List action, more information is better</span></span>](sharepoint-workflow-development-best-practices.md#bkm_01)
    
  
-  [<span data-ttu-id="bd78b-109">Записать значение каждой строки и переменную, которая выполняется построение в списке журнала</span><span class="sxs-lookup"><span data-stu-id="bd78b-109">Write the value of every string and variable that you construct to the history list</span></span>](sharepoint-workflow-development-best-practices.md#bkm_02)
    
  
-  [<span data-ttu-id="bd78b-110">Вывод журнала трассировки до и после каждого шага или важные единица работы в рабочем процессе</span><span class="sxs-lookup"><span data-stu-id="bd78b-110">Output a trace log before and after each step or important unit of work in the workflow</span></span>](sharepoint-workflow-development-best-practices.md#bkm_03)
    
  
-  [<span data-ttu-id="bd78b-111">Убедитесь, что переменные ненулевые и содержат ожидаемые значения</span><span class="sxs-lookup"><span data-stu-id="bd78b-111">Verify that variables are non-null and contain expected values</span></span>](sharepoint-workflow-development-best-practices.md#bkm_04)
    
  
-  [<span data-ttu-id="bd78b-112">Убедитесь, что строки в текстовых полях рабочего процесса не превышать 255 символов</span><span class="sxs-lookup"><span data-stu-id="bd78b-112">Ensure that strings in workflow text fields do not exceed 255 characters</span></span>](sharepoint-workflow-development-best-practices.md#bkm_05)
    
  
-  [<span data-ttu-id="bd78b-113">Используйте повышенного уровня разрешений на нейтральный учетной записи при использовании олицетворения</span><span class="sxs-lookup"><span data-stu-id="bd78b-113">Use elevated permissions on a neutral account when using impersonation</span></span>](sharepoint-workflow-development-best-practices.md#bkm_06)
    
  
-  [<span data-ttu-id="bd78b-114">В рабочих процессов для повторного использования используйте столбцов связи для обеспечения без ошибок список полей</span><span class="sxs-lookup"><span data-stu-id="bd78b-114">In reusable workflows, use Association columns to ensure error-free list fields</span></span>](sharepoint-workflow-development-best-practices.md#bkm_07)
    
  
-  [<span data-ttu-id="bd78b-115">Разработка рабочего процесса: модель бизнес-процессов в одного рабочего процесса</span><span class="sxs-lookup"><span data-stu-id="bd78b-115">Workflow design: Model a business process in a single workflow</span></span>](sharepoint-workflow-development-best-practices.md#bkm_08)
    
  
-  [<span data-ttu-id="bd78b-116">Разработка рабочего процесса: эффективное использование действия утверждения</span><span class="sxs-lookup"><span data-stu-id="bd78b-116">Workflow design: Using the Approval action effectively</span></span>](sharepoint-workflow-development-best-practices.md#bkm_09)
    
  

### <a name="apps-for-sharepoint-that-contain-integrated-workflows-must-edit-a-tag-in-the-workflowmanifestxml-file"></a><span data-ttu-id="bd78b-117">Приложения для SharePoint, которые содержат интегрированной рабочих процессов необходимо изменить тег в файле workflowmanifest.xml</span><span class="sxs-lookup"><span data-stu-id="bd78b-117">Apps for SharePoint that contain integrated workflows must edit a tag in the workflowmanifest.xml file</span></span>
<span data-ttu-id="bd78b-118"><a name="bkm_00"> </a></span><span class="sxs-lookup"><span data-stu-id="bd78b-118"><a name="bkm_00"> </a></span></span>

<span data-ttu-id="bd78b-119">Надстройки SharePoint, содержащие интегрированной рабочие процессы (которые могут быть связаны со списками на родительский сайт) отличаются от приложений обычного рабочего процесса, изменив следующий тег **true** в файле `workflowmanifest.xml` в пакет приложения:</span><span class="sxs-lookup"><span data-stu-id="bd78b-119">SharePoint Add-ins that contain integrated workflows (which can be associated with lists on the parent web) are differentiated from normal workflow apps by changing the following tag to **true** in the `workflowmanifest.xml` file in the app package:</span></span>
  
    
    

```XML

<SPIntegratedWorkflow xmlns="http://schemas.microsoft.com/sharepoint/2014/app/integratedworkflow">
    <IntegratedApp>true</IntegratedApp>
</SPIntegratedWorkflow>

```


### <a name="when-you-use-the-log-to-history-list-action-more-information-is-better"></a><span data-ttu-id="bd78b-120">При использовании действие журнала в список журналов, Дополнительные сведения  лучше</span><span class="sxs-lookup"><span data-stu-id="bd78b-120">When you use the Log To History List action, more information is better</span></span>
<span data-ttu-id="bd78b-121"><a name="bkm_01"> </a></span><span class="sxs-lookup"><span data-stu-id="bd78b-121"><a name="bkm_01"> </a></span></span>

<span data-ttu-id="bd78b-p102">Действие **Журнала в список журналов** (или класса [LogToHistoryListActivity](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowActions.LogToHistoryListActivity.aspx) при использовании Visual Studio ) позволяет регистрации сведений о рабочего процесса сделано на заданный момент жизненного цикла рабочего процесса. Это позволяет одним из наиболее важные средства устранения неполадок, которые у вас есть. Дополнительные сведения о предоставлении на важных этапах рабочего процесса, проще устранения непредвиденных событий.</span><span class="sxs-lookup"><span data-stu-id="bd78b-p102">The **Log To History List** action (or [LogToHistoryListActivity](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowActions.LogToHistoryListActivity.aspx) class if you are using Visual Studio) lets you record information about what a workflow has done at a given point in the workflow's lifecycle. This makes it one of the most important troubleshooting tools you have. The more information you provide at important points in the workflow, the easier it is to troubleshoot unexpected events.</span></span>
  
    
    
<span data-ttu-id="bd78b-125">Дополнительные сведения см. в следующих статьях.</span><span class="sxs-lookup"><span data-stu-id="bd78b-125">For more information, see the following:</span></span> 
  
    
    

-  [<span data-ttu-id="bd78b-126">Действия рабочих процессов в SharePoint Designer 2010: краткий справочник по</span><span class="sxs-lookup"><span data-stu-id="bd78b-126">Workflow actions in SharePoint Designer 2010: A quick reference guide</span></span>](https://support.office.com/en-us/article/Workflow-actions-in-SharePoint-Designer-2010-A-quick-reference-guide-5a7ad276-0ed7-49b0-b652-e56a77dd96c6?CorrelationId=9cff0340-2d05-4878-b3a0-aecb30b862ed&ui=en-US&rs=en-US&ad=US&ocmsassetID=HA010376961)
    
  
-  <span data-ttu-id="bd78b-127">Класс  [LogToHistoryListActivity](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowActions.LogToHistoryListActivity.aspx)</span><span class="sxs-lookup"><span data-stu-id="bd78b-127">[LogToHistoryListActivity](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowActions.LogToHistoryListActivity.aspx) class</span></span>
    
  
-  [<span data-ttu-id="bd78b-128">Как: журнал в списке журнала из действия рабочего процесса</span><span class="sxs-lookup"><span data-stu-id="bd78b-128">How to: Log to the History List from a Workflow Activity</span></span>](http://msdn.microsoft.com/en-us/library/ff798337.aspx)
    
  
-  [<span data-ttu-id="bd78b-129">С помощью журнала для действия SharePoint списка журнала рабочего процесса для отладки</span><span class="sxs-lookup"><span data-stu-id="bd78b-129">Using the Log to History List SharePoint workflow action for debugging</span></span>](http://www.documentmanagementworkflowinfo.com/sample-sharepoint-workflows/use-log-to-history-list-sharepoint-designer-workflow-action-debug)
    
  

### <a name="write-the-value-of-every-string-and-variable-that-you-construct-to-the-history-list"></a><span data-ttu-id="bd78b-130">Записать значение каждой строки и переменную, которая выполняется построение в списке журнала</span><span class="sxs-lookup"><span data-stu-id="bd78b-130">Write the value of every string and variable that you construct to the history list</span></span>
<span data-ttu-id="bd78b-131"><a name="bkm_02"> </a></span><span class="sxs-lookup"><span data-stu-id="bd78b-131"><a name="bkm_02"> </a></span></span>

<span data-ttu-id="bd78b-132">Отладка рабочих процессов, которые были созданы с помощью SharePoint Designer намного проще при записи строки и переменные в списке журнала с помощью действия **Log to History List**.</span><span class="sxs-lookup"><span data-stu-id="bd78b-132">Debugging workflows that were created using SharePoint Designer is much easier if you write strings and variables to the history list by using the **Log to History List** action.</span></span>
  
    
    
<span data-ttu-id="bd78b-133">Дополнительные сведения см. в следующих статьях.</span><span class="sxs-lookup"><span data-stu-id="bd78b-133">For more information, see the following:</span></span> 
  
    
    

-  [<span data-ttu-id="bd78b-134">Действия рабочих процессов в SharePoint Designer 2010: краткий справочник по</span><span class="sxs-lookup"><span data-stu-id="bd78b-134">Workflow actions in SharePoint Designer 2010: A quick reference guide</span></span>](https://support.office.com/en-us/article/Workflow-actions-in-SharePoint-Designer-2010-A-quick-reference-guide-5a7ad276-0ed7-49b0-b652-e56a77dd96c6?CorrelationId=9cff0340-2d05-4878-b3a0-aecb30b862ed&ui=en-US&rs=en-US&ad=US&ocmsassetID=HA010376961)
    
  
-  <span data-ttu-id="bd78b-135">Класс  [LogToHistoryListActivity](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowActions.LogToHistoryListActivity.aspx)</span><span class="sxs-lookup"><span data-stu-id="bd78b-135">[LogToHistoryListActivity](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowActions.LogToHistoryListActivity.aspx) class</span></span>
    
  
-  [<span data-ttu-id="bd78b-136">Как: журнал в списке журнала из действия рабочего процесса</span><span class="sxs-lookup"><span data-stu-id="bd78b-136">How to: Log to the History List from a Workflow Activity</span></span>](http://msdn.microsoft.com/en-us/library/ff798337.aspx)
    
  
-  [<span data-ttu-id="bd78b-137">С помощью журнала для действия SharePoint списка журнала рабочего процесса для отладки</span><span class="sxs-lookup"><span data-stu-id="bd78b-137">Using the Log to History List SharePoint workflow action for debugging</span></span>](http://www.documentmanagementworkflowinfo.com/sample-sharepoint-workflows/use-log-to-history-list-sharepoint-designer-workflow-action-debug)
    
  

### <a name="output-a-trace-log-before-and-after-each-step-or-important-unit-of-work-in-the-workflow"></a><span data-ttu-id="bd78b-138">Вывод журнала трассировки до и после каждого шага или важные единица работы в рабочем процессе</span><span class="sxs-lookup"><span data-stu-id="bd78b-138">Output a trace log before and after each step or important unit of work in the workflow</span></span>
<span data-ttu-id="bd78b-139"><a name="bkm_03"> </a></span><span class="sxs-lookup"><span data-stu-id="bd78b-139"><a name="bkm_03"> </a></span></span>

<span data-ttu-id="bd78b-p103">В целях отладки рабочих процессов, важно для сохранения удобной для восприятия информации до, используя следующую каждого значительные единица работы; Эти сведения должны быть зафиксированы журналов трассировки. Для получения дополнительных сведений см.:</span><span class="sxs-lookup"><span data-stu-id="bd78b-p103">To assist with debugging workflows, it is important that you capture meaningful information prior to and following each significant unit of work; this information should be committed to trace logs. For more information, see the following:</span></span>
  
    
    

-  [<span data-ttu-id="bd78b-142">Запись в журнал трассировки</span><span class="sxs-lookup"><span data-stu-id="bd78b-142">Writing to the Trace Log</span></span>](http://msdn.microsoft.com/en-us/library/aa979595.aspx)
    
  
-  [<span data-ttu-id="bd78b-143">С помощью событий и отслеживания журналы в SharePoint</span><span class="sxs-lookup"><span data-stu-id="bd78b-143">Using Event and Trace Logs in SharePoint</span></span>](http://msdn.microsoft.com/en-us/library/ff647362.aspx)
    
  

### <a name="verify-that-variables-are-non-null-and-contain-expected-values"></a><span data-ttu-id="bd78b-144">Убедитесь, что переменные ненулевые и содержат ожидаемые значения</span><span class="sxs-lookup"><span data-stu-id="bd78b-144">Verify that variables are non-null and contain expected values</span></span>
<span data-ttu-id="bd78b-145"><a name="bkm_04"> </a></span><span class="sxs-lookup"><span data-stu-id="bd78b-145"><a name="bkm_04"> </a></span></span>

<span data-ttu-id="bd78b-p104">Прежде чем использовать переменные в рабочих процессах, убедитесь, что нет значение null, переменных. Кроме того убедитесь, что переменные содержат ожидаемые значения и имеют правильный тип данных. Для получения дополнительных сведений см  [переменных и аргументов](http://msdn.microsoft.com/en-us/library/dd489456.aspx).</span><span class="sxs-lookup"><span data-stu-id="bd78b-p104">Before using variables in your workflows, ensure there are no null variables. Also, ensure that variables contain expected values and are of the correct data type. For more information, see  [Variables and Arguments](http://msdn.microsoft.com/en-us/library/dd489456.aspx).</span></span>
  
    
    

### <a name="ensure-that-strings-in-workflow-text-fields-do-not-exceed-255-characters"></a><span data-ttu-id="bd78b-149">Убедитесь, что строки в текстовых полях рабочего процесса не превышать 255 символов</span><span class="sxs-lookup"><span data-stu-id="bd78b-149">Ensure that strings in workflow text fields do not exceed 255 characters</span></span>
<span data-ttu-id="bd78b-150"><a name="bkm_05"> </a></span><span class="sxs-lookup"><span data-stu-id="bd78b-150"><a name="bkm_05"> </a></span></span>

<span data-ttu-id="bd78b-p105">Допустимый максимум для строк в текстовых полях рабочего процесса  255 знаков. Если вы настроили текстовое поле, чтобы превышать данное ограничение, его содержимое будет усечено до 255 символов.</span><span class="sxs-lookup"><span data-stu-id="bd78b-p105">The maximum allowable length for strings in workflow text fields is 255 characters. If you set your text field to exceed this limit, its content will be truncated to 255 characters.</span></span>
  
    
    

### <a name="use-elevated-permissions-on-a-neutral-account-when-using-impersonation"></a><span data-ttu-id="bd78b-153">Используйте повышенного уровня разрешений на нейтральный учетной записи при использовании олицетворения</span><span class="sxs-lookup"><span data-stu-id="bd78b-153">Use elevated permissions on a neutral account when using impersonation</span></span>
<span data-ttu-id="bd78b-154"><a name="bkm_06"> </a></span><span class="sxs-lookup"><span data-stu-id="bd78b-154"><a name="bkm_06"> </a></span></span>

<span data-ttu-id="bd78b-p106">При использовании олицетворения, описанных в рабочий процесс, следует создать рабочий процесс, с помощью учетной записи нейтральный (то есть, учетной записи, не привязанных к определенного пользователя). Это предотвратит нарушение, если учетная запись автора становится устаревшим по любой причине рабочих процессов.</span><span class="sxs-lookup"><span data-stu-id="bd78b-p106">When using impersonation steps in a workflow, you should author the workflow using a neutral account (that is, an account that is not tied to a specific user). This prevents your workflows from breaking if the author's account becomes obsolete for any reason.</span></span>
  
    
    
<span data-ttu-id="bd78b-157">Для получения дополнительных сведений см. [Создание рабочего процесса с повышенным уровнем разрешений с помощью платформы рабочих процессов SharePoint](create-a-workflow-with-elevated-permissions-by-using-the-sharepoint-workflo.md).</span><span class="sxs-lookup"><span data-stu-id="bd78b-157">For more information, see  [Create a workflow with elevated permissions by using the SharePoint Workflow platform](create-a-workflow-with-elevated-permissions-by-using-the-sharepoint-workflo.md).</span></span>
  
    
    

### <a name="in-reusable-workflows-use-association-columns-to-ensure-error-free-list-fields"></a><span data-ttu-id="bd78b-158">В рабочих процессов для повторного использования используйте столбцов связи для обеспечения без ошибок список полей</span><span class="sxs-lookup"><span data-stu-id="bd78b-158">In reusable workflows, use Association columns to ensure error-free list fields</span></span>
<span data-ttu-id="bd78b-159"><a name="bkm_07"> </a></span><span class="sxs-lookup"><span data-stu-id="bd78b-159"><a name="bkm_07"> </a></span></span>

<span data-ttu-id="bd78b-p107">При создании повторно используемого рабочего процесса, который зависит от необходимости определенного поля списка, может (1) ограничения рабочего процесса к типу контента, который имеет указанного поля или (2) сделать это поле столбца с связи. Вариант 2 рекомендуется, поскольку возможно, что тип контента будет изменить и рабочий процесс для приостановки выполнения.</span><span class="sxs-lookup"><span data-stu-id="bd78b-p107">If you create a reusable workflow that relies on its list having a specific field, you may either (1) restrict the workflow to a content type that has the specified field, or (2) make the field an association column. Option 2 is recommended because it's possible that a content type will change and cause the workflow to break.</span></span>
  
    
    

### <a name="workflow-design-model-a-business-process-in-a-single-workflow"></a><span data-ttu-id="bd78b-162">Разработка рабочего процесса: модель бизнес-процессов в одного рабочего процесса</span><span class="sxs-lookup"><span data-stu-id="bd78b-162">Workflow design: Model a business process in a single workflow</span></span>
<span data-ttu-id="bd78b-163"><a name="bkm_08"> </a></span><span class="sxs-lookup"><span data-stu-id="bd78b-163"><a name="bkm_08"> </a></span></span>

<span data-ttu-id="bd78b-164">Где это возможно, гораздо лучше для моделирования бизнес-процессов в один рабочий процесс, чтобы разделить логику рабочего процесса на несколько небольших рабочих процессов.</span><span class="sxs-lookup"><span data-stu-id="bd78b-164">Where possible, it is much better to model a business process in a single workflow than to break the workflow logic into several smaller workflows.</span></span>
  
    
    

### <a name="workflow-design-using-the-approval-action-effectively"></a><span data-ttu-id="bd78b-165">Разработка рабочего процесса: эффективное использование действия утверждения</span><span class="sxs-lookup"><span data-stu-id="bd78b-165">Workflow design: Using the Approval action effectively</span></span>
<span data-ttu-id="bd78b-166"><a name="bkm_09"> </a></span><span class="sxs-lookup"><span data-stu-id="bd78b-166"><a name="bkm_09"> </a></span></span>

<span data-ttu-id="bd78b-167">Где это возможно, вместо создания нескольких **Approval** действий, более эффективно использовать функцию **Stages** в **Approval** операции.</span><span class="sxs-lookup"><span data-stu-id="bd78b-167">Where possible, instead of creating multiple **Approval** actions, it is more effective to use the **Stages** feature within an **Approval** action.</span></span>
  
    
    

## <a name="see-also"></a><span data-ttu-id="bd78b-168">См. также</span><span class="sxs-lookup"><span data-stu-id="bd78b-168">See also</span></span>
<span data-ttu-id="bd78b-169"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="bd78b-169"><a name="bk_addresources"> </a></span></span>


-  [<span data-ttu-id="bd78b-170">Рабочие процессы в SharePoint</span><span class="sxs-lookup"><span data-stu-id="bd78b-170">Workflows in SharePoint</span></span>](workflows-in-sharepoint.md)
    
  
-  [<span data-ttu-id="bd78b-171">Основные сведения о рабочих процессах в SharePoint</span><span class="sxs-lookup"><span data-stu-id="bd78b-171">SharePoint workflow fundamentals</span></span>](sharepoint-workflow-fundamentals.md)
    
  
-  [<span data-ttu-id="bd78b-172">Разработка рабочих процессов в SharePoint с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bd78b-172">Develop SharePoint workflows using Visual Studio</span></span>](develop-sharepoint-workflows-using-visual-studio.md)
    
  

