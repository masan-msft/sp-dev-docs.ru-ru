---
title: "Проблемы проверки в Visio (платформа рабочих процессов SharePoint 2010)"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 416c8269-3c4e-40f4-bc20-a625f07a4dac
ms.openlocfilehash: 4a700ee4a3061096db6e63f78fde2b0badac7f7c
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="validation-issues-in-visio-sharepoint-2010-workflow-platform"></a><span data-ttu-id="ad5e3-102">Проблемы проверки в Visio (платформа рабочих процессов SharePoint 2010)</span><span class="sxs-lookup"><span data-stu-id="ad5e3-102">Validation issues in Visio (SharePoint 2010 Workflow platform)</span></span>
<span data-ttu-id="ad5e3-p101">Используйте эту ссылку для устранения проблемы при проверке при экспорте рабочего процесса SharePoint в Visio Professional 2013 SharePoint Designer 2013. В этой статье описываются проблемы, которые могут возникнуть при использовании платформы рабочего процесса SharePoint 2010 в SharePoint Designer 2013 при проверке.</span><span class="sxs-lookup"><span data-stu-id="ad5e3-p101">Use this reference to help resolve validation issues when you export a SharePoint workflow from Visio Professional 2013 to SharePoint Designer 2013. This article describes validation issues that might arise when you use the SharePoint 2010 Workflow platform in SharePoint Designer 2013.</span></span>
  
    
    


## <a name="introduction"></a><span data-ttu-id="ad5e3-105">Введение</span><span class="sxs-lookup"><span data-stu-id="ad5e3-105">Introduction</span></span>
<span data-ttu-id="ad5e3-106"><a name="section1"> </a></span><span class="sxs-lookup"><span data-stu-id="ad5e3-106"><a name="section1"> </a></span></span>

<span data-ttu-id="ad5e3-p102">При экспорте рабочего процесса SharePoint из Microsoft Visio профессиональный 2013 Microsoft SharePoint Designer 2013, необходимо сначала проверить схему. Если схема рабочего процесса не является допустимым, откроется окно " **ошибки** ", которая содержит список проблем, которые необходимо исправить, прежде чем рабочий процесс может быть экспортирован...</span><span class="sxs-lookup"><span data-stu-id="ad5e3-p102">When you export a SharePoint workflow from Microsoft Visio Professional 2013 to Microsoft SharePoint Designer 2013, the diagram must first be validated. If the workflow diagram is not valid, an **Issues** window appears that includes a list of issues that must be repaired before the workflow can be exported..</span></span>
  
    
    
<span data-ttu-id="ad5e3-p103">Данная статья содержит описание, пример и рекомендуемые действия для каждого из проблемы проверки рабочих процессов, которые можно получить в Visio Professional 2013. Если во время проверки получают уведомление о проблеме, найдите имя проблемы в списке ниже, используйте пример, чтобы определить, где проблема в том и следуйте предложенные действия для ее решения.</span><span class="sxs-lookup"><span data-stu-id="ad5e3-p103">This article includes a description, example, and suggested action for each of the workflow validation issues that you can receive in Visio Professional 2013. If you receive notice of an issue during validation, find the issue name in the list below, use the example to help identify where the problem is, and then follow the suggested action to resolve it.</span></span>
  
    
    

## <a name="a-custom-action-cannot-be-added-to-a-workflow-diagram"></a><span data-ttu-id="ad5e3-111">Настраиваемое действие нельзя добавить на схему рабочего процесса</span><span class="sxs-lookup"><span data-stu-id="ad5e3-111">A custom action cannot be added to a workflow diagram</span></span>
<span data-ttu-id="ad5e3-112"><a name="section2"> </a></span><span class="sxs-lookup"><span data-stu-id="ad5e3-112"><a name="section2"> </a></span></span>

<span data-ttu-id="ad5e3-113">Сообщение</span><span class="sxs-lookup"><span data-stu-id="ad5e3-113">Message:</span></span>
  
    
    
<span data-ttu-id="ad5e3-p104">Настраиваемое действие нельзя добавить на схему рабочего процесса. Настраиваемое действие возможно только при импорте рабочего процесса из SharePoint Designer.</span><span class="sxs-lookup"><span data-stu-id="ad5e3-p104">A Custom action cannot be added to a workflow diagram. The Custom action can only be generated when importing workflow from SharePoint Designer.</span></span>
  
    
    
<span data-ttu-id="ad5e3-116">Пример:</span><span class="sxs-lookup"><span data-stu-id="ad5e3-116">Example:</span></span>
  
    
    

  
    
    
![Невозможно добавить настраиваемое действие.](../images/spd15-wf-error1.JPG)
  
    
    
<span data-ttu-id="ad5e3-118">Предполагаемое действие:</span><span class="sxs-lookup"><span data-stu-id="ad5e3-118">Suggested action:</span></span>
  
    
    
<span data-ttu-id="ad5e3-p105">Если требуется добавить действие в рабочий процесс и основной фигуры не существует для его в наборе элементов, не создавать свои собственные фигуры и импортировать сертификат из другой набор элементов. Вместо этого используйте существующей фигуры и затем использовать функцию **Добавьте комментарий** фигуры для указания режима целям.</span><span class="sxs-lookup"><span data-stu-id="ad5e3-p105">If you want to add an action to your workflow and a master shape does not exist for it in the stencil, do not create your own shape or import one from a different stencil. Instead, use an existing shape, and then use the **Add Comment** feature of the shape to specify the intended behavior.</span></span>
  
    
    

## <a name="a-custom-condition-cannot-be-added-to-a-workflow-diagram"></a><span data-ttu-id="ad5e3-121">Настраиваемые условие нельзя добавить на схему рабочего процесса</span><span class="sxs-lookup"><span data-stu-id="ad5e3-121">A Custom condition cannot be added to a workflow diagram</span></span>
<span data-ttu-id="ad5e3-122"><a name="section3"> </a></span><span class="sxs-lookup"><span data-stu-id="ad5e3-122"><a name="section3"> </a></span></span>

<span data-ttu-id="ad5e3-123">Сообщение</span><span class="sxs-lookup"><span data-stu-id="ad5e3-123">Message:</span></span>
  
    
    
<span data-ttu-id="ad5e3-p106">Настраиваемые условие нельзя добавить на схему рабочего процесса. Настраиваемое условие возможно только при импорте рабочего процесса из SharePoint Designer.</span><span class="sxs-lookup"><span data-stu-id="ad5e3-p106">A Custom condition cannot be added to a workflow diagram. The custom condition can only be generated when importing workflow from SharePoint Designer.</span></span>
  
    
    
<span data-ttu-id="ad5e3-126">Пример:</span><span class="sxs-lookup"><span data-stu-id="ad5e3-126">Example:</span></span>
  
    
    

  
    
    
![Невозможно добавить настраиваемое условие](../images/spd15-wf-error2.JPG)
  
    
    
<span data-ttu-id="ad5e3-128">Предполагаемое действие:</span><span class="sxs-lookup"><span data-stu-id="ad5e3-128">Suggested action:</span></span>
  
    
    
<span data-ttu-id="ad5e3-p107">Если требуется добавить условие в рабочий процесс и основной фигуры не существует для его в наборе элементов, не создавать свои собственные фигуры и импортировать сертификат из другой набор элементов. Вместо этого используйте существующей фигуры и затем использовать функцию **Добавьте комментарий** фигуры для указания режима целям.</span><span class="sxs-lookup"><span data-stu-id="ad5e3-p107">If you want to add a condition to your workflow and a master shape does not exist for it in the stencil, do not create your own shape or import one from a different stencil. Instead, use an existing shape, and then use the **Add Comment** feature of the shape to specify the intended behavior.</span></span>
  
    
    

## <a name="a-compound-condition-cannot-be-manually-added-to-a-workflow-diagram"></a><span data-ttu-id="ad5e3-131">Составное условие нельзя добавить на схему рабочего процесса вручную</span><span class="sxs-lookup"><span data-stu-id="ad5e3-131">A Compound condition cannot be manually added to a workflow diagram</span></span>
<span data-ttu-id="ad5e3-132"><a name="section4"> </a></span><span class="sxs-lookup"><span data-stu-id="ad5e3-132"><a name="section4"> </a></span></span>

<span data-ttu-id="ad5e3-133">Сообщение</span><span class="sxs-lookup"><span data-stu-id="ad5e3-133">Message:</span></span>
  
    
    
<span data-ttu-id="ad5e3-p108">Составное условие нельзя добавить на схему рабочего процесса вручную. Составное условие возможно только при импорте рабочего процесса из SharePoint Designer.</span><span class="sxs-lookup"><span data-stu-id="ad5e3-p108">A Compound condition cannot be manually added to a workflow diagram. The compound condition can only be generated when importing workflow from SharePoint Designer.</span></span>
  
    
    
<span data-ttu-id="ad5e3-136">Пример:</span><span class="sxs-lookup"><span data-stu-id="ad5e3-136">Example:</span></span>
  
    
    

  
    
    
![Невозможно вручную добавить составное условие](../images/spd15-wf-error3.JPG)
  
    
    
<span data-ttu-id="ad5e3-138">Предполагаемое действие:</span><span class="sxs-lookup"><span data-stu-id="ad5e3-138">Suggested action:</span></span>
  
    
    
<span data-ttu-id="ad5e3-p109">Если требуется добавить условие в рабочий процесс и основной фигуры не существует для его в наборе элементов, не создавать свои собственные фигуры и импортировать сертификат из другой набор элементов. Вместо этого используйте существующей фигуры и затем использовать функцию **Добавить комментарий** фигуры для указания режима целям.</span><span class="sxs-lookup"><span data-stu-id="ad5e3-p109">If you want to add a condition to your workflow and a master shape does not exist for it in the stencil, do not create your own shape or import one from a different stencil. Instead, use an existing shape, and then use the **Add a Comment** feature of the shape to specify the intended behavior.</span></span>
  
    
    

## <a name="duplicate-connections-exist-between-workflow-shapes"></a><span data-ttu-id="ad5e3-141">Существуют дубликаты соединений между фигурами рабочего процесса</span><span class="sxs-lookup"><span data-stu-id="ad5e3-141">Duplicate connections exist between workflow shapes</span></span>
<span data-ttu-id="ad5e3-142"><a name="section5"> </a></span><span class="sxs-lookup"><span data-stu-id="ad5e3-142"><a name="section5"> </a></span></span>

<span data-ttu-id="ad5e3-143">Сообщение</span><span class="sxs-lookup"><span data-stu-id="ad5e3-143">Message:</span></span>
  
    
    
<span data-ttu-id="ad5e3-144">Существуют дубликаты соединений между фигурами рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="ad5e3-144">Duplicate connections exist between workflow shapes.</span></span>
  
    
    
<span data-ttu-id="ad5e3-145">Пример:</span><span class="sxs-lookup"><span data-stu-id="ad5e3-145">Example:</span></span>
  
    
    

  
    
    
![Между фигурами существуют дубликаты соединений](../images/spd15-wf-error4.JPG)
  
    
    
<span data-ttu-id="ad5e3-147">Предполагаемое действие:</span><span class="sxs-lookup"><span data-stu-id="ad5e3-147">Suggested action:</span></span>
  
    
    
<span data-ttu-id="ad5e3-148">Удаление избыточных соединителя, выбрав и его удаление.</span><span class="sxs-lookup"><span data-stu-id="ad5e3-148">Remove the redundant connector by selecting and deleting it.</span></span>
  
    
    

## <a name="loop-back-to-parent-shape-is-not-allowed"></a><span data-ttu-id="ad5e3-149">Замыкание на родительскую фигуру запрещено</span><span class="sxs-lookup"><span data-stu-id="ad5e3-149">Loop back to parent shape is not allowed</span></span>
<span data-ttu-id="ad5e3-150"><a name="section6"> </a></span><span class="sxs-lookup"><span data-stu-id="ad5e3-150"><a name="section6"> </a></span></span>

<span data-ttu-id="ad5e3-151">Сообщение</span><span class="sxs-lookup"><span data-stu-id="ad5e3-151">Message:</span></span>
  
    
    
<span data-ttu-id="ad5e3-152">Замыкание на родительскую фигуру запрещено</span><span class="sxs-lookup"><span data-stu-id="ad5e3-152">Loop back to parent shape is not allowed.</span></span>
  
    
    
<span data-ttu-id="ad5e3-153">Пример:</span><span class="sxs-lookup"><span data-stu-id="ad5e3-153">Example:</span></span>
  
    
    

  
    
    
![Замыкание на родительскую фигуру запрещено](../images/spd15-wf-error5.JPG)
  
    
    
<span data-ttu-id="ad5e3-155">Предполагаемое действие:</span><span class="sxs-lookup"><span data-stu-id="ad5e3-155">Suggested action:</span></span>
  
    
    
<span data-ttu-id="ad5e3-p110">Ни Visio Professional 2013, ни SharePoint Designer 2013 не поддерживают рабочих процессов с помощью циклов. Проверка рабочего процесса для циклов и удалить цикла подключения. Если вы хотите создать рабочий процесс SharePoint, который включает набор повтора действия, необходимо создать рабочий процесс в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ad5e3-p110">Neither Visio Professional 2013 nor SharePoint Designer 2013 supports workflows with loops. Check your workflow for loops, and delete the looping connections. If you want to create a SharePoint workflow that includes a set of looping steps, you must create the workflow in Visual Studio.</span></span>
  
    
    

## <a name="parallel-activities-that-are-also-sequential-are-not-allowed"></a><span data-ttu-id="ad5e3-159">Параллельные действия, также являющиеся последовательными не разрешены</span><span class="sxs-lookup"><span data-stu-id="ad5e3-159">Parallel activities that are also sequential are not allowed</span></span>
<span data-ttu-id="ad5e3-160"><a name="section7"> </a></span><span class="sxs-lookup"><span data-stu-id="ad5e3-160"><a name="section7"> </a></span></span>

<span data-ttu-id="ad5e3-161">Сообщение</span><span class="sxs-lookup"><span data-stu-id="ad5e3-161">Message:</span></span>
  
    
    
<span data-ttu-id="ad5e3-162">Параллельные действия, также являющиеся последовательными не разрешены.</span><span class="sxs-lookup"><span data-stu-id="ad5e3-162">Parallel activities that are also sequential are not allowed.</span></span>
  
    
    
<span data-ttu-id="ad5e3-163">Пример:</span><span class="sxs-lookup"><span data-stu-id="ad5e3-163">Example:</span></span>
  
    
    

  
    
    
![Параллельные действия, которые также являются последовательными](../images/spd15-wf-error6.JPG)
  
    
    
<span data-ttu-id="ad5e3-165">Предполагаемое действие:</span><span class="sxs-lookup"><span data-stu-id="ad5e3-165">Suggested action:</span></span>
  
    
    
<span data-ttu-id="ad5e3-p111">Действия может быть либо параллельный, либо последовательные, но не оба одновременно. Параллельные действия удалите последовательного соединители. Для последовательного мероприятий удалите параллельный соединители. В некоторых случаях одновременно параллельных и последовательных действий может быть трудно определить. В приведенных ниже примерах Показать другие распространенные экземпляры параллельных и последовательных сообщений по беседам и предлагают альтернативные arrangements.</span><span class="sxs-lookup"><span data-stu-id="ad5e3-p111">Activities can be either parallel or sequential, but not both simultaneously. For parallel activities, remove the sequential connectors. For sequential activities, remove the parallel connectors. Sometimes, simultaneously parallel and sequential activities can be difficult to identify. The following examples show other common instances of parallel and sequential arrangement and offer alternative arrangements.</span></span>
  
    
    
<span data-ttu-id="ad5e3-171">Пример:</span><span class="sxs-lookup"><span data-stu-id="ad5e3-171">Example:</span></span>
  
    
    

  
    
    
![Избегайте ссылки на действие из нескольких путей](../images/spd15-wf-error7.JPG)
  
    
    
<span data-ttu-id="ad5e3-173">Предполагаемое действие:</span><span class="sxs-lookup"><span data-stu-id="ad5e3-173">Suggested action:</span></span>
  
    
    
<span data-ttu-id="ad5e3-174">Чтобы избежать необходимости соединители пункты же действие из нескольких путей, попробуйте дублирования для действия:</span><span class="sxs-lookup"><span data-stu-id="ad5e3-174">To avoid having connectors point to the same activity from multiple paths, try duplicating the activity:</span></span>
  
    
    

  
    
    
![Параллельные действия, которые также являются последовательными](../images/spd15-wf-error8.JPG)
  
    
    
<span data-ttu-id="ad5e3-176">Пример:</span><span class="sxs-lookup"><span data-stu-id="ad5e3-176">Example:</span></span>
  
    
    

  
    
    
![Параллельные действия, которые также являются последовательными](../images/spd15-wf-error9.JPG)
  
    
    
<span data-ttu-id="ad5e3-178">Предполагаемое действие:</span><span class="sxs-lookup"><span data-stu-id="ad5e3-178">Suggested action:</span></span>
  
    
    
<span data-ttu-id="ad5e3-179">При работе с параллельные блоки в последовательные этапы (обычно находится в рабочих процессах, созданный с помощью SharePoint Designer), попробуйте использовать фигуры «Добавьте комментарий» между двумя параллельные блоки, чтобы разделить действия.</span><span class="sxs-lookup"><span data-stu-id="ad5e3-179">If dealing with parallel blocks in sequential steps (usually found in workflows constructed by using SharePoint Designer), try using the "Add a Comment" shape between the two parallel blocks so that the steps are separated cleanly.</span></span>
  
    
    

  
    
    
![Параллельные действия, которые также являются последовательными](../images/spd15-wf.JPG)
  
    
    

  
    
    

  
    
    

## <a name="the-condition-shape-does-not-have-connections-labeled-with-yes-or-no"></a><span data-ttu-id="ad5e3-181">Фигура условия не имеет соединений с Да или нет</span><span class="sxs-lookup"><span data-stu-id="ad5e3-181">The condition shape does not have connections labeled with Yes or No</span></span>
<span data-ttu-id="ad5e3-182"><a name="section8"> </a></span><span class="sxs-lookup"><span data-stu-id="ad5e3-182"><a name="section8"> </a></span></span>

<span data-ttu-id="ad5e3-183">Сообщение</span><span class="sxs-lookup"><span data-stu-id="ad5e3-183">Message:</span></span>
  
    
    
<span data-ttu-id="ad5e3-184">Фигура условия не имеет соединений с Да или нет.</span><span class="sxs-lookup"><span data-stu-id="ad5e3-184">The condition shape does not have connections labeled with Yes or No.</span></span>
  
    
    
<span data-ttu-id="ad5e3-185">Пример:</span><span class="sxs-lookup"><span data-stu-id="ad5e3-185">Example:</span></span>
  
    
    

  
    
    
![Фигура условия не имеет соединений "Да" и "Нет"](../images/spd15-wf-error11.JPG)
  
    
    
<span data-ttu-id="ad5e3-187">Предполагаемое действие:</span><span class="sxs-lookup"><span data-stu-id="ad5e3-187">Suggested action:</span></span>
  
    
    
<span data-ttu-id="ad5e3-188">Щелкните правой кнопкой мыши соединитель для назначения значение «Да» или «Нет» метки.</span><span class="sxs-lookup"><span data-stu-id="ad5e3-188">Right-click the connector to assign a "Yes" or "No" label.</span></span>
  
    
    

## <a name="the-condition-shape-must-have-at-least-one-outgoing-connection-with-label-yes-or-no"></a><span data-ttu-id="ad5e3-189">Фигура условия должна иметь по крайней мере одно исходящее соединение с меткой Да или нет</span><span class="sxs-lookup"><span data-stu-id="ad5e3-189">The condition shape must have at least one outgoing connection with label Yes or No</span></span>
<span data-ttu-id="ad5e3-190"><a name="section9"> </a></span><span class="sxs-lookup"><span data-stu-id="ad5e3-190"><a name="section9"> </a></span></span>

<span data-ttu-id="ad5e3-191">Сообщение</span><span class="sxs-lookup"><span data-stu-id="ad5e3-191">Message:</span></span>
  
    
    
<span data-ttu-id="ad5e3-192">Фигура условия должна иметь по крайней мере одно исходящее соединение с меткой Да или нет.</span><span class="sxs-lookup"><span data-stu-id="ad5e3-192">The condition shape must have at least one outgoing connection with label Yes or No.</span></span>
  
    
    
<span data-ttu-id="ad5e3-193">Пример:</span><span class="sxs-lookup"><span data-stu-id="ad5e3-193">Example:</span></span>
  
    
    

  
    
    
![Фигура соединения должна иметь исходящее соединение](../images/spd15-wf-error12.JPG)
  
    
    
<span data-ttu-id="ad5e3-195">Предполагаемое действие:</span><span class="sxs-lookup"><span data-stu-id="ad5e3-195">Suggested action:</span></span>
  
    
    
<span data-ttu-id="ad5e3-196">Убедитесь, что фигура условия по крайней мере одного исходящего соединителя, подключенного к другой фигурой рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="ad5e3-196">Ensure that the condition shape has at least one outgoing connector attached to another workflow shape.</span></span>
  
    
    

## <a name="the-connector-is-not-a-sharepoint-workflow-connector"></a><span data-ttu-id="ad5e3-197">Соединитель не является соединителем рабочего процесса SharePoint</span><span class="sxs-lookup"><span data-stu-id="ad5e3-197">The connector is not a SharePoint Workflow connector</span></span>
<span data-ttu-id="ad5e3-198"><a name="section10"> </a></span><span class="sxs-lookup"><span data-stu-id="ad5e3-198"><a name="section10"> </a></span></span>

<span data-ttu-id="ad5e3-199">Сообщение</span><span class="sxs-lookup"><span data-stu-id="ad5e3-199">Message:</span></span>
  
    
    
<span data-ttu-id="ad5e3-p112">Соединитель не является соединителем рабочего процесса SharePoint. Убедитесь, что используется правильный соединитель с использованием соединительной или Автосоединение.</span><span class="sxs-lookup"><span data-stu-id="ad5e3-p112">The connector is not a SharePoint Workflow connector. Ensure the correct connector is used by using the connector tool or AutoConnect.</span></span>
  
    
    
<span data-ttu-id="ad5e3-202">Пример:</span><span class="sxs-lookup"><span data-stu-id="ad5e3-202">Example:</span></span>
  
    
    

  
    
    
![Убедитесь, что используется правильный соединитель](../images/spd15-wf-error13.JPG)
  
    
    
<span data-ttu-id="ad5e3-204">Предполагаемое действие:</span><span class="sxs-lookup"><span data-stu-id="ad5e3-204">Suggested action:</span></span>
  
    
    
<span data-ttu-id="ad5e3-p113">Избегайте повторное использование соединителей из других схем, так как они не являются обязательно предназначен для использования с рабочими процессами SharePoint. Удаление выбранного соединителя и замените нового соединителя с помощью средства соединитель или Автосоединение.</span><span class="sxs-lookup"><span data-stu-id="ad5e3-p113">Avoid reusing connectors from other diagrams, because they are not necessarily designed to be used with SharePoint workflows. Delete the selected connector, and use the connector tool or AutoConnect to replace it with a new connector.</span></span>
  
    
    

## <a name="the-connector-must-be-connected-to-two-workflow-shapes"></a><span data-ttu-id="ad5e3-207">Соединитель должна быть соединена с двумя фигурами рабочего процесса</span><span class="sxs-lookup"><span data-stu-id="ad5e3-207">The connector must be connected to two workflow shapes</span></span>
<span data-ttu-id="ad5e3-208"><a name="section11"> </a></span><span class="sxs-lookup"><span data-stu-id="ad5e3-208"><a name="section11"> </a></span></span>

<span data-ttu-id="ad5e3-209">Сообщение</span><span class="sxs-lookup"><span data-stu-id="ad5e3-209">Message:</span></span>
  
    
    
<span data-ttu-id="ad5e3-210">Соединитель должен быть подключен к двум фигурам рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="ad5e3-210">The connector must be connected to two workflow shapes.</span></span>
  
    
    
<span data-ttu-id="ad5e3-211">Пример:</span><span class="sxs-lookup"><span data-stu-id="ad5e3-211">Example:</span></span>
  
    
    

  
    
    
![Соединитель должен быть подключен к двум фигурам рабочего процесса](../images/spd15-wf-error14.JPG)
  
    
    
<span data-ttu-id="ad5e3-213">Предполагаемое действие:</span><span class="sxs-lookup"><span data-stu-id="ad5e3-213">Suggested action:</span></span>
  
    
    
<span data-ttu-id="ad5e3-214">Удалите dead-end соединители или подключите их второй фигуры.</span><span class="sxs-lookup"><span data-stu-id="ad5e3-214">Remove dead-end connectors or attach them to a second shape.</span></span>
  
    
    

## <a name="the-diagram-must-only-have-one-workflow-and-one-start-shape"></a><span data-ttu-id="ad5e3-215">Схема должна иметь только один рабочий процесс и одно фигуру начала</span><span class="sxs-lookup"><span data-stu-id="ad5e3-215">The diagram must only have one workflow and one Start shape</span></span>
<span data-ttu-id="ad5e3-216"><a name="section12"> </a></span><span class="sxs-lookup"><span data-stu-id="ad5e3-216"><a name="section12"> </a></span></span>

<span data-ttu-id="ad5e3-217">Сообщение</span><span class="sxs-lookup"><span data-stu-id="ad5e3-217">Message:</span></span>
  
    
    
<span data-ttu-id="ad5e3-218">Схема должна иметь только один рабочий процесс и одно фигуру начала.</span><span class="sxs-lookup"><span data-stu-id="ad5e3-218">The diagram must only have one workflow and one Start shape.</span></span>
  
    
    
<span data-ttu-id="ad5e3-219">Пример:</span><span class="sxs-lookup"><span data-stu-id="ad5e3-219">Example:</span></span>
  
    
    

  
    
    
![Схема должна иметь только один рабочий процесс и одно начало](../images/spd15-wf-error15.JPG)
  
    
    
<span data-ttu-id="ad5e3-221">Предполагаемое действие:</span><span class="sxs-lookup"><span data-stu-id="ad5e3-221">Suggested action:</span></span>
  
    
    
<span data-ttu-id="ad5e3-p114">Все пути должны берутся из **той же фигурой**. Удалить лишние **Начать** с фигурами и упорядочить соединители, чтобы путь начинается в одном месте.</span><span class="sxs-lookup"><span data-stu-id="ad5e3-p114">All paths must originate from the same **Start** shape. Remove extra **Start** shapes, and arrange the connectors so that the path starts in one place.</span></span>
  
    
    

## <a name="the-shape-is-not-a-sharepoint-workflow-shape-only-sharepoint-workflow-shapes-can-be-connected-in-a-workflow"></a><span data-ttu-id="ad5e3-p115">Фигура не является фигурой рабочего процесса SharePoint. Только фигуры рабочего процесса SharePoint могут быть подключены в рабочем процессе</span><span class="sxs-lookup"><span data-stu-id="ad5e3-p115">The shape is not a SharePoint workflow shape. Only SharePoint workflow shapes can be connected in a workflow</span></span>
<span data-ttu-id="ad5e3-226"><a name="section13"> </a></span><span class="sxs-lookup"><span data-stu-id="ad5e3-226"><a name="section13"> </a></span></span>

<span data-ttu-id="ad5e3-227">Сообщение</span><span class="sxs-lookup"><span data-stu-id="ad5e3-227">Message:</span></span>
  
    
    
<span data-ttu-id="ad5e3-p116">Фигура не является фигурой рабочего процесса SharePoint. Только фигуры рабочего процесса SharePoint могут быть подключены в рабочем процессе.</span><span class="sxs-lookup"><span data-stu-id="ad5e3-p116">The shape is not a SharePoint workflow shape. Only SharePoint workflow shapes can be connected in a workflow.</span></span>
  
    
    
<span data-ttu-id="ad5e3-230">Пример:</span><span class="sxs-lookup"><span data-stu-id="ad5e3-230">Example:</span></span>
  
    
    

  
    
    
![Фигура не является фигурой рабочего процесса SharePoint](../images/spd15-wf-error16.JPG)
  
    
    
<span data-ttu-id="ad5e3-232">Предполагаемое действие:</span><span class="sxs-lookup"><span data-stu-id="ad5e3-232">Suggested action:</span></span>
  
    
    
<span data-ttu-id="ad5e3-p117">Можно использовать только фигуры рабочего процесса из шаблонов рабочих процессов SharePoint в шаблоне рабочего процесса Microsoft SharePoint. Другие фигуры блок-схемы, не распознаются, и они запретить экспорт на SharePoint Designer 2013 рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="ad5e3-p117">Only workflow shapes from the SharePoint workflow stencils can be used in the Microsoft SharePoint Workflow template. Other flowchart shapes are not recognized, and they prevent the workflow from being exported to SharePoint Designer 2013.</span></span>
  
    
    

## <a name="the-start-shape-must-not-have-incoming-connections"></a><span data-ttu-id="ad5e3-235">Фигура начала не должна иметь входящих соединений</span><span class="sxs-lookup"><span data-stu-id="ad5e3-235">The Start shape must not have incoming connections</span></span>
<span data-ttu-id="ad5e3-236"><a name="section14"> </a></span><span class="sxs-lookup"><span data-stu-id="ad5e3-236"><a name="section14"> </a></span></span>

<span data-ttu-id="ad5e3-237">Сообщение</span><span class="sxs-lookup"><span data-stu-id="ad5e3-237">Message:</span></span>
  
    
    
<span data-ttu-id="ad5e3-238">Фигура начала не должна иметь входящих соединений</span><span class="sxs-lookup"><span data-stu-id="ad5e3-238">The Start shape must not have incoming connections.</span></span>
  
    
    
<span data-ttu-id="ad5e3-239">Пример:</span><span class="sxs-lookup"><span data-stu-id="ad5e3-239">Example:</span></span>
  
    
    

  
    
    
![Фигура начала не должна иметь входящих соединений](../images/spd15-wf-error17.JPG)
  
    
    
<span data-ttu-id="ad5e3-241">Предполагаемое действие:</span><span class="sxs-lookup"><span data-stu-id="ad5e3-241">Suggested action:</span></span>
  
    
    
<span data-ttu-id="ad5e3-242">Удаление входящего соединителя для формы **запуска**.</span><span class="sxs-lookup"><span data-stu-id="ad5e3-242">Remove the incoming connector to the **Start** shape.</span></span>
  
    
    

## <a name="the-terminate-shape-must-not-have-outgoing-connections"></a><span data-ttu-id="ad5e3-243">Фигура окончания не должна иметь исходящих соединений</span><span class="sxs-lookup"><span data-stu-id="ad5e3-243">The Terminate shape must not have outgoing connections</span></span>
<span data-ttu-id="ad5e3-244"><a name="section15"> </a></span><span class="sxs-lookup"><span data-stu-id="ad5e3-244"><a name="section15"> </a></span></span>

<span data-ttu-id="ad5e3-245">Сообщение</span><span class="sxs-lookup"><span data-stu-id="ad5e3-245">Message:</span></span>
  
    
    
<span data-ttu-id="ad5e3-246">Фигура окончания не должна иметь исходящих соединений.</span><span class="sxs-lookup"><span data-stu-id="ad5e3-246">The Terminate shape must not have outgoing connections.</span></span>
  
    
    
<span data-ttu-id="ad5e3-247">Пример:</span><span class="sxs-lookup"><span data-stu-id="ad5e3-247">Example:</span></span>
  
    
    

  
    
    
![Фигура окончания не должна иметь исходящих соединений](../images/spd15-wf-error18.JPG)
  
    
    
<span data-ttu-id="ad5e3-249">Предполагаемое действие:</span><span class="sxs-lookup"><span data-stu-id="ad5e3-249">Suggested action:</span></span>
  
    
    
<span data-ttu-id="ad5e3-250">Удаление исходящего соединителя из фигура **окончания**.</span><span class="sxs-lookup"><span data-stu-id="ad5e3-250">Remove the outgoing connector from the **Terminate** shape.</span></span>
  
    
    

## <a name="the-workflow-must-have-a-start-shape"></a><span data-ttu-id="ad5e3-251">Рабочий процесс должен иметь фигуру начала</span><span class="sxs-lookup"><span data-stu-id="ad5e3-251">The workflow must have a Start shape</span></span>
<span data-ttu-id="ad5e3-252"><a name="section16"> </a></span><span class="sxs-lookup"><span data-stu-id="ad5e3-252"><a name="section16"> </a></span></span>

<span data-ttu-id="ad5e3-253">Сообщение</span><span class="sxs-lookup"><span data-stu-id="ad5e3-253">Message:</span></span>
  
    
    
<span data-ttu-id="ad5e3-254">Рабочий процесс должен иметь фигуру начала</span><span class="sxs-lookup"><span data-stu-id="ad5e3-254">The workflow must have a Start shape.</span></span>
  
    
    
<span data-ttu-id="ad5e3-255">Пример:</span><span class="sxs-lookup"><span data-stu-id="ad5e3-255">Example:</span></span>
  
    
    

  
    
    
![Рабочий процесс должен иметь фигуру начала](../images/spd15-wf-error19.JPG)
  
    
    
<span data-ttu-id="ad5e3-257">Предполагаемое действие:</span><span class="sxs-lookup"><span data-stu-id="ad5e3-257">Suggested action:</span></span>
  
    
    
<span data-ttu-id="ad5e3-258">Добавьте **запустите** фигуры в начало рабочего процесса и подключиться к первого действия.</span><span class="sxs-lookup"><span data-stu-id="ad5e3-258">Add a **Start** shape to the beginning of the workflow, and connect it to the first activity.</span></span>
  
    
    

## <a name="the-workflow-shape-is-not-connected-to-a-terminate-shape"></a><span data-ttu-id="ad5e3-259">Фигура рабочего процесса не соединена Фигура окончания</span><span class="sxs-lookup"><span data-stu-id="ad5e3-259">The workflow shape is not connected to a Terminate shape</span></span>
<span data-ttu-id="ad5e3-260"><a name="section17"> </a></span><span class="sxs-lookup"><span data-stu-id="ad5e3-260"><a name="section17"> </a></span></span>

<span data-ttu-id="ad5e3-261">Сообщение</span><span class="sxs-lookup"><span data-stu-id="ad5e3-261">Message:</span></span>
  
    
    
<span data-ttu-id="ad5e3-262">Фигура рабочего процесса не соединена Фигура окончания.</span><span class="sxs-lookup"><span data-stu-id="ad5e3-262">The workflow shape is not connected to a Terminate shape.</span></span>
  
    
    
<span data-ttu-id="ad5e3-263">Пример:</span><span class="sxs-lookup"><span data-stu-id="ad5e3-263">Example:</span></span>
  
    
    

  
    
    
![Фигура рабочего процесса не соединена с фигурой окончания](../images/spd15-wf-error20.JPG)
  
    
    
<span data-ttu-id="ad5e3-265">Предполагаемое действие:</span><span class="sxs-lookup"><span data-stu-id="ad5e3-265">Suggested action:</span></span>
  
    
    
<span data-ttu-id="ad5e3-p118">Если рабочий процесс не имеет фигура **окончания**, добавьте один и подключитесь к концу рабочего процесса. Если фигура рабочего процесса не находит соединения с другой фигурой рабочего процесса (см), можно удалить его или подключиться к другой фигурой рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="ad5e3-p118">If the workflow does not have a **Terminate** shape, add one and connect it to the end of the workflow. If a workflow shape is missing a connection to another workflow shape (see example), you can remove it or connect it to another workflow shape.</span></span>
  
    
    

## <a name="the-workflow-shape-is-not-connected-to-the-workflow"></a><span data-ttu-id="ad5e3-268">Фигура рабочего процесса не соединена с рабочим процессом</span><span class="sxs-lookup"><span data-stu-id="ad5e3-268">The workflow shape is not connected to the workflow</span></span>
<span data-ttu-id="ad5e3-269"><a name="section18"> </a></span><span class="sxs-lookup"><span data-stu-id="ad5e3-269"><a name="section18"> </a></span></span>

<span data-ttu-id="ad5e3-270">Сообщение</span><span class="sxs-lookup"><span data-stu-id="ad5e3-270">Message:</span></span>
  
    
    
<span data-ttu-id="ad5e3-271">Фигура рабочего процесса не соединена с рабочим процессом.</span><span class="sxs-lookup"><span data-stu-id="ad5e3-271">The workflow shape is not connected to the workflow.</span></span>
  
    
    
<span data-ttu-id="ad5e3-272">Пример</span><span class="sxs-lookup"><span data-stu-id="ad5e3-272">Example:</span></span>
  
    
    

  
    
    
![Фигура рабочего процесса не соединена с рабочим процессом](../images/spd15-wf-error21.JPG)
  
    
    
<span data-ttu-id="ad5e3-274">Предполагаемое действие:</span><span class="sxs-lookup"><span data-stu-id="ad5e3-274">Suggested action:</span></span>
  
    
    
<span data-ttu-id="ad5e3-p119">При необходимости в форме рабочего процесса добавьте соединителей для присоединения к пути рабочего процесса. В противном случае удалите форму.</span><span class="sxs-lookup"><span data-stu-id="ad5e3-p119">If the workflow shape is necessary, add connectors to attach it to the workflow path. Otherwise, delete the shape.</span></span>
  
    
    

## <a name="workflow-nesting-levels-must-not-exceed-a-maximum-of-10"></a><span data-ttu-id="ad5e3-277">Число уровней вложения рабочего процесса не должен превышать не более 10</span><span class="sxs-lookup"><span data-stu-id="ad5e3-277">Workflow nesting levels must not exceed a maximum of 10</span></span>
<span data-ttu-id="ad5e3-278"><a name="section19"> </a></span><span class="sxs-lookup"><span data-stu-id="ad5e3-278"><a name="section19"> </a></span></span>

<span data-ttu-id="ad5e3-279">Сообщение</span><span class="sxs-lookup"><span data-stu-id="ad5e3-279">Message:</span></span>
  
    
    
<span data-ttu-id="ad5e3-280">Число уровней вложения рабочего процесса не должен превышать не более 10.</span><span class="sxs-lookup"><span data-stu-id="ad5e3-280">Workflow nesting levels must not exceed a maximum of 10.</span></span>
  
    
    
<span data-ttu-id="ad5e3-281">Предполагаемое действие:</span><span class="sxs-lookup"><span data-stu-id="ad5e3-281">Suggested action:</span></span>
  
    
    
<span data-ttu-id="ad5e3-p120">Visio профессиональный 2013 может распознать не более 10 уровней вложенных действий. Изменение порядка рабочего процесса, чтобы сократить сложность, не тратя действия или разделения пути рабочего процесса на более одного филиала.</span><span class="sxs-lookup"><span data-stu-id="ad5e3-p120">Visio Professional 2013 can recognize a maximum of 10 levels of nested workflow activities. Rearrange the workflow to reduce complexity by eliminating activities or dividing the workflow path into more than one branch.</span></span>
  
    
    

## <a name="see-also"></a><span data-ttu-id="ad5e3-284">См. также</span><span class="sxs-lookup"><span data-stu-id="ad5e3-284">See also</span></span>
<span data-ttu-id="ad5e3-285"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="ad5e3-285"><a name="bk_addresources"> </a></span></span>


-  [<span data-ttu-id="ad5e3-286">Что нового в рабочих процессах для SharePoint</span><span class="sxs-lookup"><span data-stu-id="ad5e3-286">What's new in workflows for SharePoint</span></span>](what-s-new-in-workflows-for-sharepoint.md)
    
  
-  [<span data-ttu-id="ad5e3-287">Общие сведения о рабочих процессах в SharePoint</span><span class="sxs-lookup"><span data-stu-id="ad5e3-287">Get started with workflows in SharePoint</span></span>](get-started-with-workflows-in-sharepoint.md)
    
  
-  [<span data-ttu-id="ad5e3-288">Разработка рабочих процессов в SharePoint Designer и Visio</span><span class="sxs-lookup"><span data-stu-id="ad5e3-288">Workflow development in SharePoint Designer and Visio</span></span>](workflow-development-in-sharepoint-designer-and-visio.md)
    
  

  
    
    

