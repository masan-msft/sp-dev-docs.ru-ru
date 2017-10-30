---
title: "Перемещение рабочего процесса SharePoint Designer 2013 и Visio Professional 2013 (платформа рабочих процессов SharePoint 2010)"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: dbe6f019-b4f2-480f-a8e7-bcb8842ab924
ms.openlocfilehash: 42d3743885eeea645e2f8a5a88b8646c68379d91
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="transfer-a-workflow-between-sharepoint-designer-2013-and-visio-professional-2013-sharepoint-2010-workflow-platform"></a><span data-ttu-id="269a9-102">Перемещение рабочего процесса SharePoint Designer 2013 и Visio Professional 2013 (платформа рабочих процессов SharePoint 2010)</span><span class="sxs-lookup"><span data-stu-id="269a9-102">Transfer a workflow between SharePoint Designer 2013 and Visio Professional 2013 (SharePoint 2010 Workflow platform)</span></span>
<span data-ttu-id="269a9-103">Используйте SharePoint Designer для импорта рабочего процесса Visio или Экспорт рабочего процесса в Visio.</span><span class="sxs-lookup"><span data-stu-id="269a9-103">Use SharePoint Designer to import a workflow from Visio or export a workflow to Visio.</span></span>
## <a name="transferring-a-workflow-between-sharepoint-designer-2013-and-visio-professional-2013"></a><span data-ttu-id="269a9-104">Передача рабочего процесса между SharePoint Designer 2013 и Visio профессиональный 2013</span><span class="sxs-lookup"><span data-stu-id="269a9-104">Transferring a workflow between SharePoint Designer 2013 and Visio Professional 2013</span></span>
<span data-ttu-id="269a9-105"><a name="section1"> </a></span><span class="sxs-lookup"><span data-stu-id="269a9-105"></span></span>

<span data-ttu-id="269a9-p101">Бизнес-аналитики и аналитики процесс, уже знакомых с Создание блок-схемы в Visio можно использовать Visio для разработки рабочего процесса SharePoint. Рабочий процесс в Visio представляет бизнес-логики. По завершении бизнес-логику рабочего процесса можно экспортировать в SharePoint Designer. После включения рабочего процесса в SharePoint Designer ИТ-специалистов можно привязать его к на сайте SharePoint.</span><span class="sxs-lookup"><span data-stu-id="269a9-p101">Business analysts and process analysts who are already familiar with flowcharting in Visio can use Visio to design a SharePoint workflow. The workflow in Visio represents the business logic. After the business logic is complete, the workflow can be exported to SharePoint Designer. Once the workflow is in SharePoint Designer, an IT professional can wire it up to the SharePoint site.</span></span>
  
    
    

  
    
    
![Преобразование бизнес-логики в правила рабочего процесса](../images/spd15-wf-importFromVisio.png)
  
    
    
<span data-ttu-id="269a9-111">В Microsoft SharePoint Designer 2013 можно импортировать рабочий поток, созданный в Microsoft Visio профессиональный 2013 или Экспорт рабочего процесса в Visio для просмотра.</span><span class="sxs-lookup"><span data-stu-id="269a9-111">In Microsoft SharePoint Designer 2013, you can import a workflow created in Microsoft Visio Professional 2013 or export a workflow to Visio for viewing.</span></span> 
  
    
    
<span data-ttu-id="269a9-112">В этой статье описывается перенос рабочего процесса с помощью платформы рабочего процесса SharePoint 2010 в SharePoint Designer 2013.</span><span class="sxs-lookup"><span data-stu-id="269a9-112">This article describes transferring a workflow by using the SharePoint 2010 Workflow platform in SharePoint Designer 2013.</span></span>
  
    
    
<span data-ttu-id="269a9-113">Чтобы выбрать платформы рабочего процесса SharePoint 2010 для создания рабочего процесса:</span><span class="sxs-lookup"><span data-stu-id="269a9-113">To select the SharePoint 2010 Workflow platform when you create a workflow:</span></span>
  
    
    

  
    
    

1. <span data-ttu-id="269a9-114">В области **Навигация** щелкните **Рабочие процессы**.</span><span class="sxs-lookup"><span data-stu-id="269a9-114">In the **Navigation** pane, click **Workflows**.</span></span>
    
  
2. <span data-ttu-id="269a9-115">На вкладке **рабочие процессы** в разделе **New** щелкните **Рабочий процесс списка**, **Рабочий процесс для повторного использования** или **Рабочего процесса сайта**.</span><span class="sxs-lookup"><span data-stu-id="269a9-115">On the **Workflows** tab, in the **New** section, click **List Workflow**, **Reusable Workflow**, or **Site Workflow**.</span></span>
    
  
3. <span data-ttu-id="269a9-116">В диалоговом окне **Создать рабочий процесс** в поле **Тип платформы** выберите **Рабочий процесс SharePoint 2010**.</span><span class="sxs-lookup"><span data-stu-id="269a9-116">In the **Create Workflow** dialog box, in the **Platform Type** box, click **SharePoint 2010 Workflow**.</span></span>
    
  
<span data-ttu-id="269a9-117">Могут выполнять визуализацию рабочих процессов в SharePoint Designer двумя способами:</span><span class="sxs-lookup"><span data-stu-id="269a9-117">You can visualize workflows in SharePoint Designer in two ways:</span></span>
  
    
    

- <span data-ttu-id="269a9-118">Если установлены службы Visio на сервере, на котором работает SharePoint, можно создать визуализация рабочего процесса на странице состояния рабочего процесса, который отображается ход выполнения и назначений.</span><span class="sxs-lookup"><span data-stu-id="269a9-118">If Visio Services is installed on the server that is running SharePoint, you can create a workflow visualization on the workflow status page that displays progress and assignments.</span></span>
    
  
- <span data-ttu-id="269a9-119">Рабочий процесс можно экспортировать в Visio для создания документа рабочего процесса, который может использоваться для обратной связи и утверждения.</span><span class="sxs-lookup"><span data-stu-id="269a9-119">You can export the workflow to Visio to create a workflow drawing that can be used for feedback and approval.</span></span>
    
  

  
    
    
![Схемы рабочих процессов можно экспортировать в Visio](../images/spd15-wf-exportToVisio.png)
  
    
    

  
    
    

  
    
    

## <a name="import-a-workflow-from-visio"></a><span data-ttu-id="269a9-121">Импорт рабочего процесса из Visio</span><span class="sxs-lookup"><span data-stu-id="269a9-121">Import a workflow from Visio</span></span>
<span data-ttu-id="269a9-122"><a name="section2"> </a></span><span class="sxs-lookup"><span data-stu-id="269a9-122"></span></span>

<span data-ttu-id="269a9-123">Импорт рабочего процесса SharePoint, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="269a9-123">To import a SharePoint workflow, do the following:</span></span>
  
    
    

1. <span data-ttu-id="269a9-124">В SharePoint Designer 2013, в области **навигации** щелкните **рабочие процессы**.</span><span class="sxs-lookup"><span data-stu-id="269a9-124">In SharePoint Designer 2013, in the **Navigation** pane, click **Workflows**.</span></span>
    
  
2. <span data-ttu-id="269a9-125">На вкладке **рабочие процессы** в группе **Управление** выберите пункт **Импорт из Visio**.</span><span class="sxs-lookup"><span data-stu-id="269a9-125">On the **Workflows** tab, in the **Manage** group, click **Import from Visio**.</span></span>
    
  ![Импорт рабочего процесса](../images/spd15-ImportFromVisio.JPG)
  

  

  
3. <span data-ttu-id="269a9-127">В диалоговом окне **Импорт рабочего процесса из документа Visio** перейдите и выберите файл Visio рабочего процесса обмена (.vwi), который требуется использовать и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="269a9-127">In the **Import Workflow from Visio Drawing** dialog box, browse to and select the Visio Workflow Interchange (.vwi) file you want to use, and then click **Next**.</span></span>
    
  
4. <span data-ttu-id="269a9-p102">Введите имя для рабочего процесса и затем выберите тип рабочего процесса, он должен быть после завершения импорта. Возможны следующие значения.</span><span class="sxs-lookup"><span data-stu-id="269a9-p102">Type a name for the workflow, and then select the type of workflow you want it to be once it has been imported. Your choices are:</span></span>
    
  - <span data-ttu-id="269a9-p103">**Рабочий процесс списка** Рабочий процесс, подключенный к определенному списку. Если выбран этот параметр, необходимо выбрать список, к которому будет присоединен рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="269a9-p103">**List workflow** A workflow that is attached to a specific list. If you select this option, you must choose the list to which the workflow will be attached.</span></span>
    
  
  - <span data-ttu-id="269a9-p104">**Рабочий процесс для повторного использования** Рабочий процесс, подключенный к типу контента и поэтому portable. Его можно использовать в различных списках на сайте SharePoint. Если выбран этот параметр, необходимо выбрать тип контента, на котором будет запускаться рабочий процесс.</span><span class="sxs-lookup"><span data-stu-id="269a9-p104">**Reusable workflow** A workflow that is attached to a content type, and is therefore portable. It can be used by different lists on a SharePoint site. If you select this option, you must choose the content type on which the workflow will run.</span></span>
    
  
5. <span data-ttu-id="269a9-135">Нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="269a9-135">Click **Finish**.</span></span>
    
  
<span data-ttu-id="269a9-p105">Импортированный рабочий процесс отображается в редакторе полноэкранный режим рабочего процесса SharePoint Designer. Весь текст в собственные фигуры Visio импортируется в SharePoint Designer как действие подписи (серый текст на рисунке ниже) для уточнения рабочего процесса:</span><span class="sxs-lookup"><span data-stu-id="269a9-p105">The imported workflow appears in the SharePoint Designer full-screen workflow editor. All text in the Visio custom shapes is imported into SharePoint Designer as activity labels (the gray text in the image below) to clarify the intent of the workflow:</span></span>
  
    
    

  
    
    
![Импортированный рабочий процесс](../images/spd15-wf-PO.JPG)
  
    
    
<span data-ttu-id="269a9-139">После импорта рабочий процесс в конструкторе SharePoint можно редактировать и может быть изменено для добавления необходимых условий, действий, действия и параметры.</span><span class="sxs-lookup"><span data-stu-id="269a9-139">After the workflow is imported to SharePoint Designer, it is editable and can be revised to add the necessary conditions, actions, steps, and settings.</span></span> 
  
    
    

## <a name="export-a-workflow-to-visio"></a><span data-ttu-id="269a9-140">Экспорт рабочего процесса в Visio</span><span class="sxs-lookup"><span data-stu-id="269a9-140">Export a workflow to Visio</span></span>
<span data-ttu-id="269a9-141"><a name="section3"> </a></span><span class="sxs-lookup"><span data-stu-id="269a9-141"></span></span>

<span data-ttu-id="269a9-p106">После создания или изменения рабочего процесса в SharePoint Designer 2013 можно экспортировать рабочего процесса в приложении Visio, который можно открыть в Visio профессиональный 2013. Экспорт рабочего процесса в Visio после изменения в SharePoint Designer, также известной как «обратное преобразование»  обеспечивает более подробные совместную работу бизнес-пользователи и разработчики рабочих процессов. При итерации разработки рабочего процесса, таким образом, можно использовать Visio для определения бизнес-требований, а затем использовать обратное преобразование для координации усилий и Подтверждение изменений.</span><span class="sxs-lookup"><span data-stu-id="269a9-p106">Once you have created or edited a workflow in SharePoint Designer 2013, you can export the workflow as a Visio drawing that can be opened in Visio Professional 2013. The ability to export a workflow back to Visio after it has been edited in SharePoint Designer—also known as "round-tripping"—enables deeper collaboration between business users and workflow designers. When you iterate the workflow design in this way, you can use Visio to define the business requirements and then use round-tripping to coordinate and approve changes.</span></span>
  
    
    

> <span data-ttu-id="269a9-145">**Примечание:** Visio профессиональный 2013 не поддерживает действия.</span><span class="sxs-lookup"><span data-stu-id="269a9-145">**Note:** Visio Professional 2013 does not support steps.</span></span> <span data-ttu-id="269a9-146">Сведения о действие, которое было добавлено в SharePoint Designer может утеряны при просмотре рабочего процесса в Visio и повторно импортированы в SharePoint Designer.</span><span class="sxs-lookup"><span data-stu-id="269a9-146">Step information that has been added in SharePoint Designer may be lost when the workflow is viewed in Visio and then re-imported into SharePoint Designer.</span></span> 
  
    
    

<span data-ttu-id="269a9-147">Экспорт рабочего процесса, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="269a9-147">To export a workflow, do the following:</span></span>
  
    
    

1. <span data-ttu-id="269a9-148">В SharePoint Designer 2013 щелкните **рабочие процессы** в области **навигации**.</span><span class="sxs-lookup"><span data-stu-id="269a9-148">In SharePoint Designer 2013, click **Workflows** in the **Navigation** pane.</span></span>
    
  
2. <span data-ttu-id="269a9-149">На вкладке **рабочего процесса** в группе **Управление** нажмите кнопку **Экспорт в Visio**.</span><span class="sxs-lookup"><span data-stu-id="269a9-149">On the **Workflow** tab, in the **Manage** group, click **Export to Visio**.</span></span>
    
  
3. <span data-ttu-id="269a9-p108">В диалоговом окне **Экспорт рабочего процесса в документ Visio** имя файла, выберите расположение и нажмите кнопку **Сохранить**. Экспортированный файл сохраняется в виде VWI-файлом, который можно открывать непосредственно в Visio профессиональный 2013.</span><span class="sxs-lookup"><span data-stu-id="269a9-p108">In the **Export Workflow to Visio Drawing** dialog box, name the file, select a location, and then click **Save**. The exported file is saved as a .vwi file that can be opened directly in Visio Professional 2013.</span></span>
    
  

## <a name="additional-resources"></a><span data-ttu-id="269a9-152">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="269a9-152">Additional resources</span></span>
<span data-ttu-id="269a9-153"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="269a9-153"></span></span>


-  [<span data-ttu-id="269a9-154">Что нового в рабочих процессах для SharePoint</span><span class="sxs-lookup"><span data-stu-id="269a9-154">What's new in workflows for SharePoint</span></span>](what-s-new-in-workflows-for-sharepoint.md)
    
  
-  [<span data-ttu-id="269a9-155">Общие сведения о рабочих процессах в SharePoint</span><span class="sxs-lookup"><span data-stu-id="269a9-155">Get started with workflows in SharePoint</span></span>](get-started-with-workflows-in-sharepoint.md)
    
  
-  [<span data-ttu-id="269a9-156">Разработка рабочих процессов в SharePoint Designer и Visio</span><span class="sxs-lookup"><span data-stu-id="269a9-156">Workflow development in SharePoint Designer and Visio</span></span>](workflow-development-in-sharepoint-designer-and-visio.md)
    
  

  
    
    

