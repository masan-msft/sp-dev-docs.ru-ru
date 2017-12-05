---
title: "Основные сведения для упаковки и развертывания рабочих процессов в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 545b4930-ac05-4c9d-9980-5818cb800cf1
ms.openlocfilehash: c7627a78d47fc01b2b5366e0919c85434cdcad96
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="understanding-how-to-package-and-deploy-workflow-in-sharepoint"></a><span data-ttu-id="ba4b2-102">Основные сведения для упаковки и развертывания рабочих процессов в SharePoint</span><span class="sxs-lookup"><span data-stu-id="ba4b2-102">Understanding how to package and deploy workflow in SharePoint</span></span>
<span data-ttu-id="ba4b2-103">Узнайте, как для упаковки и развертывания рабочего процесса в SharePoint с помощью SharePoint Designer 2013.</span><span class="sxs-lookup"><span data-stu-id="ba4b2-103">Learn how to package and deploy a workflow in SharePoint with SharePoint Designer 2013.</span></span>
## <a name="overview-of-the-workflow-packaging-capabilities-of-sharepoint-designer-2013"></a><span data-ttu-id="ba4b2-104">Обзор возможностей Создание пакета, содержащего рабочего процесса из SharePoint Designer 2013</span><span class="sxs-lookup"><span data-stu-id="ba4b2-104">Overview of the workflow packaging capabilities of SharePoint Designer 2013</span></span>
<span data-ttu-id="ba4b2-105"><a name="section1"> </a></span><span class="sxs-lookup"><span data-stu-id="ba4b2-105"></span></span>

<span data-ttu-id="ba4b2-106">SharePoint Designer 2013 предоставляет возможность сохранения рабочего процесса в качестве шаблона.</span><span class="sxs-lookup"><span data-stu-id="ba4b2-106">SharePoint Designer 2013 provides the capability to save a workflow as a template.</span></span> <span data-ttu-id="ba4b2-107">Сохранение как шаблона рабочего процесса также известные как упаковка рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="ba4b2-107">Saving a workflow as a template is also known as packaging the workflow.</span></span> <span data-ttu-id="ba4b2-108">После сохранения рабочего процесса в качестве шаблона его можно быть импортированы в других средах SharePoint и используется без необходимости чипа рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="ba4b2-108">After the workflow is saved as a template, it can then be imported into other SharePoint environments and used without the need to redevelop the workflow.</span></span> <span data-ttu-id="ba4b2-109">Не все типы рабочих процессов можно сохранить как шаблон.</span><span class="sxs-lookup"><span data-stu-id="ba4b2-109">Not all workflow types can be saved as a template.</span></span> <span data-ttu-id="ba4b2-110">Следующие матрицы показаны типы рабочих процессов, которые могут быть сохранены как шаблон.</span><span class="sxs-lookup"><span data-stu-id="ba4b2-110">The following matrix shows the workflow types that can be saved as a template.</span></span> 
  
    
    

<span data-ttu-id="ba4b2-111">**Поддержка по платформы для сохранения рабочего процесса в виде шаблона**</span><span class="sxs-lookup"><span data-stu-id="ba4b2-111">**Support, by platform, for saving a workflow as a template**</span></span>


|<span data-ttu-id="ba4b2-112">**Тип рабочего процесса**</span><span class="sxs-lookup"><span data-stu-id="ba4b2-112">**Workflow type**</span></span>|<span data-ttu-id="ba4b2-113">**Платформа рабочих процессов SharePoint 2010**</span><span class="sxs-lookup"><span data-stu-id="ba4b2-113">**SharePoint 2010 Workflow platform**</span></span>|<span data-ttu-id="ba4b2-114">**Платформа рабочих процессов SharePoint**</span><span class="sxs-lookup"><span data-stu-id="ba4b2-114">**SharePoint Workflow platform**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="ba4b2-115">Рабочий процесс списка</span><span class="sxs-lookup"><span data-stu-id="ba4b2-115">List Workflow</span></span>  <br/> |<span data-ttu-id="ba4b2-116">Нет</span><span class="sxs-lookup"><span data-stu-id="ba4b2-116">No</span></span>  <br/> |<span data-ttu-id="ba4b2-117">Да</span><span class="sxs-lookup"><span data-stu-id="ba4b2-117">Yes</span></span>  <br/> |
|<span data-ttu-id="ba4b2-118">Рабочий процесс сайта</span><span class="sxs-lookup"><span data-stu-id="ba4b2-118">Site Workflow</span></span>  <br/> |<span data-ttu-id="ba4b2-119">Нет</span><span class="sxs-lookup"><span data-stu-id="ba4b2-119">No</span></span>  <br/> |<span data-ttu-id="ba4b2-120">Да</span><span class="sxs-lookup"><span data-stu-id="ba4b2-120">Yes</span></span>  <br/> |
|<span data-ttu-id="ba4b2-121">Рабочий процесс для повторного использования</span><span class="sxs-lookup"><span data-stu-id="ba4b2-121">Reusable Workflow</span></span>  <br/> |<span data-ttu-id="ba4b2-122">Да</span><span class="sxs-lookup"><span data-stu-id="ba4b2-122">Yes</span></span>  <br/> |<span data-ttu-id="ba4b2-123">Да</span><span class="sxs-lookup"><span data-stu-id="ba4b2-123">Yes</span></span>  <br/> |
   

  
    
    

  
    
    

> <span data-ttu-id="ba4b2-124">**Примечание:** Содержит две платформы различных рабочих процессов SharePoint: платформы рабочего процесса SharePoint 2010 и платформы рабочих процессов SharePoint.</span><span class="sxs-lookup"><span data-stu-id="ba4b2-124">**Note:** SharePoint contains two different workflow platforms: the SharePoint 2010 Workflow platform and the SharePoint Workflow platform.</span></span> <span data-ttu-id="ba4b2-125">Обе платформы доступны в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="ba4b2-125">Both platforms are available in SharePoint.</span></span> <span data-ttu-id="ba4b2-126">Дополнительные сведения о двух рабочего процесса можно [Приступая к работе с рабочего процесса SharePoint.](http://msdn.microsoft.com/library/cc73be76-a329-449f-90ab-86822b1c2ee8.aspx)</span><span class="sxs-lookup"><span data-stu-id="ba4b2-126">For more information about the two workflow, see  [Getting started with SharePoint workflow.](http://msdn.microsoft.com/library/cc73be76-a329-449f-90ab-86822b1c2ee8.aspx)</span></span>
  
    
    


## <a name="packaging-a-workflow-by-using-sharepoint-designer-2013"></a><span data-ttu-id="ba4b2-127">Упаковка рабочего процесса с помощью SharePoint Designer 2013</span><span class="sxs-lookup"><span data-stu-id="ba4b2-127">Packaging a workflow by using SharePoint Designer 2013</span></span>
<span data-ttu-id="ba4b2-128"><a name="section2"> </a></span><span class="sxs-lookup"><span data-stu-id="ba4b2-128"></span></span>

<span data-ttu-id="ba4b2-p103">Процесс создания пакетов рабочего процесса включает сохранение файла шаблона рабочего процесса с помощью SharePoint Designer 2013. Пакет рабочего процесса в виде файла Web пакета решения (WSP) и с расширением WSP-файл. Упаковка рабочего процесса выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="ba4b2-p103">The process for packaging a workflow involves saving the workflow to a template file by using SharePoint Designer 2013. A workflow package is in the form of a Web Solution Package (WSP) file and has a .wsp extension. To package a workflow follow these steps.</span></span> 
  
    
    

### <a name="package-a-workflow"></a><span data-ttu-id="ba4b2-132">Создание пакета рабочего процесса</span><span class="sxs-lookup"><span data-stu-id="ba4b2-132">Package a workflow</span></span>


1. <span data-ttu-id="ba4b2-133">Откройте существующий рабочий процесс или разработать новый рабочий процесс, в SharePoint Designer 2013.</span><span class="sxs-lookup"><span data-stu-id="ba4b2-133">Open an existing workflow, or develop a new workflow, in SharePoint Designer 2013.</span></span>
    
  
2. <span data-ttu-id="ba4b2-134">На вкладке **Параметры рабочих процессов** на ленте нажмите кнопку **Сохранить в качестве шаблона** в разделе **Управление**, как показано на рисунке.</span><span class="sxs-lookup"><span data-stu-id="ba4b2-134">On the **Workflow Settings** tab in the ribbon, click the **Save as Template** button in the **Manage** section as shown in the figure.</span></span>
    
   <span data-ttu-id="ba4b2-135">**Рисунок: Сохранение в качестве шаблона рабочего процесса**</span><span class="sxs-lookup"><span data-stu-id="ba4b2-135">**Figure: Save workflow as template**</span></span>

  

  ![Рабочий процесс упаковки в SPD 2013](../images/SPD15-PackagingWorkflow1.png)
  

  

  
3. <span data-ttu-id="ba4b2-137">Откроется диалоговое окно информационные сообщите вы знаете, что шаблон сохранен в библиотеку **Активов сайта**.</span><span class="sxs-lookup"><span data-stu-id="ba4b2-137">An informational dialog box appears to let you know the template has been saved to the **Site Assets** library.</span></span>
    
  
4. <span data-ttu-id="ba4b2-138">Выберите библиотеку активов сайта для просмотра шаблона рабочего процесса, как показано на рисунке.</span><span class="sxs-lookup"><span data-stu-id="ba4b2-138">Click the Site Assets library to view the workflow template as shown in the figure.</span></span>
    
   <span data-ttu-id="ba4b2-139">**Рисунок: Шаблона рабочего процесса в ресурсах сайта**</span><span class="sxs-lookup"><span data-stu-id="ba4b2-139">**Figure: A workflow template in Site Assets**</span></span>

  

  ![Шаблон рабочего процесса в ресурсах сайта.](../images/SPD15-PackagingWorkflow2.png)
  

  

  

  
    
    

> <span data-ttu-id="ba4b2-141">**Совет:** Шаблон рабочего процесса автоматически сохраняет библиотеки **Материалы сайта** семейства сайтов, в котором находится рабочий процесс.</span><span class="sxs-lookup"><span data-stu-id="ba4b2-141">**Tip:** A workflow template automatically saves to the **Site Assets** library of the site collection in which the workflow resides.</span></span>
  
    
    


## <a name="deploying-a-workflow-package-to-sharepoint"></a><span data-ttu-id="ba4b2-142">Развертывание пакета рабочего процесса в SharePoint</span><span class="sxs-lookup"><span data-stu-id="ba4b2-142">Deploying a workflow package to SharePoint</span></span>
<span data-ttu-id="ba4b2-143"><a name="section3"> </a></span><span class="sxs-lookup"><span data-stu-id="ba4b2-143"></span></span>

<span data-ttu-id="ba4b2-p104">Можно развернуть пакет рабочих процессов для фермы SharePoint или сайта, отличный от фермы или сайта, в котором он был разработан. В порядке для рабочего процесса должны быть выполнены развертывания быть успешно двумя элементами:</span><span class="sxs-lookup"><span data-stu-id="ba4b2-p104">You can deploy a workflow package to a SharePoint farm or site that is different from the farm or site in which it was developed. In order for a workflow deployment to be successful two items must be fulfilled:</span></span>
  
    
    

- <span data-ttu-id="ba4b2-146">Все зависимости рабочих процессов, таких как списки, библиотеки, столбцов и типов контента должны уже существовать на новый сайт.</span><span class="sxs-lookup"><span data-stu-id="ba4b2-146">All workflow dependencies such as lists, libraries, columns, and content types must already exist on the new site.</span></span>
    
  
- <span data-ttu-id="ba4b2-147">Каждой зависимости должен иметь точное имя зависимостей источника.</span><span class="sxs-lookup"><span data-stu-id="ba4b2-147">Each dependency must have the exact name of the source dependency.</span></span>
    
  
<span data-ttu-id="ba4b2-148">Если развертывание рабочего процесса и точное зависимостей не существуют результатом будет ошибка.</span><span class="sxs-lookup"><span data-stu-id="ba4b2-148">If a workflow is deployed and the exact dependencies do not exist then the result will be an error.</span></span>
  
    
    
<span data-ttu-id="ba4b2-149">Перед развертыванием рабочего процесса необходимо экспортировать шаблон рабочего процесса из исходной фермы SharePoint.</span><span class="sxs-lookup"><span data-stu-id="ba4b2-149">Before you can deploy a workflow you must first export the workflow template from the source SharePoint farm.</span></span> <span data-ttu-id="ba4b2-150">Экспорт шаблона рабочего процесса, выполните следующую процедуру.</span><span class="sxs-lookup"><span data-stu-id="ba4b2-150">To export a workflow template, follow this procedure.</span></span>
  
    
    

### <a name="export-a-workflow-template"></a><span data-ttu-id="ba4b2-151">Экспорт шаблона рабочего процесса</span><span class="sxs-lookup"><span data-stu-id="ba4b2-151">Export a workflow template</span></span>


1. <span data-ttu-id="ba4b2-152">Откройте SharePoint Designer 2013 и перейдите в библиотеку активов сайта, где находится шаблон.</span><span class="sxs-lookup"><span data-stu-id="ba4b2-152">Open SharePoint Designer 2013 and navigate to the Site Assets library where the template is located.</span></span>
    
  
2. <span data-ttu-id="ba4b2-153">Выберите шаблон рабочего процесса, который необходимо экспортировать, щелкнув его.</span><span class="sxs-lookup"><span data-stu-id="ba4b2-153">Select the workflow template you want to export by clicking it.</span></span>
    
  
3. <span data-ttu-id="ba4b2-154">Нажмите кнопку **Экспорт файла** для сохранения файла шаблона для локального компьютера или сетевой диск, как показано на рисунке.</span><span class="sxs-lookup"><span data-stu-id="ba4b2-154">Click the **Export File** button to save the template file to your local computer or a network drive, as shown in the figure.</span></span>
    
   <span data-ttu-id="ba4b2-155">**Рисунок: Экспорт шаблона рабочего процесса из SharePoint Designer 2013**</span><span class="sxs-lookup"><span data-stu-id="ba4b2-155">**Figure: Export workflow template from SharePoint Designer 2013**</span></span>

  

  ![Экспорт файла рабочего процесса из SPD.](../images/SPD15-PackagingWorkflow3.png)
  

  

  
<span data-ttu-id="ba4b2-157">Развертывание пакета процесса выполните следующую процедуру.</span><span class="sxs-lookup"><span data-stu-id="ba4b2-157">To deploy a workflow package follow this procedure.</span></span>
  
    
    

### <a name="deploy-a-workflow-solution"></a><span data-ttu-id="ba4b2-158">Развертывание решения рабочего процесса</span><span class="sxs-lookup"><span data-stu-id="ba4b2-158">Deploy a workflow solution</span></span>


1. <span data-ttu-id="ba4b2-159">Откройте Internet Explorer и перейдите к семейству сайтов SharePoint, где вы хотите развернуть рабочий процесс.</span><span class="sxs-lookup"><span data-stu-id="ba4b2-159">Open Internet Explorer and navigate to the SharePoint site collection where you want to deploy the workflow.</span></span>
    
  
2. <span data-ttu-id="ba4b2-160">Щелкните **Действия сайта** и выберите **Параметры сайта**.</span><span class="sxs-lookup"><span data-stu-id="ba4b2-160">Click **Site Actions** and select **Site Settings**.</span></span>
    
  
3. <span data-ttu-id="ba4b2-161">В разделе **Веб-разработки галерей** выберите **решения**.</span><span class="sxs-lookup"><span data-stu-id="ba4b2-161">In the **Web Design Galleries** section click **Solutions**.</span></span>
    
    > <span data-ttu-id="ba4b2-162">**Примечание:** На странице " **Параметры сайта** " для семейства веб-сайтов необходимо быть для просмотра в коллекцию **решений** .</span><span class="sxs-lookup"><span data-stu-id="ba4b2-162">**Note:** You must be on the **Site Settings** page for the site collection in order to see the **Solutions** gallery.</span></span> <span data-ttu-id="ba4b2-163">Если вы находитесь на странице **Параметры сайта** для дочерних сайтов выберите каталог **решений** не отображается.</span><span class="sxs-lookup"><span data-stu-id="ba4b2-163">If you are on the **Site Settings** page for a sub-site then the **Solutions** gallery is not visible.</span></span>
4. <span data-ttu-id="ba4b2-164">Нажмите кнопку **Отправить решение**, чтобы загрузить решение, как показано на рисунке.</span><span class="sxs-lookup"><span data-stu-id="ba4b2-164">Click the **Upload Solution** button to upload the solution as shown in the figure.</span></span>
    
   <span data-ttu-id="ba4b2-165">**Рисунок: Кнопка отправки решения**</span><span class="sxs-lookup"><span data-stu-id="ba4b2-165">**Figure: Upload Solution button**</span></span>

  

  ![Кнопка загрузки решения.](../images/SPD15-PackagingWorkflow4.png)
  

  

  
5. <span data-ttu-id="ba4b2-167">Активация решения, щелкнув кнопку " **активировать** ", как показано на рисунке.</span><span class="sxs-lookup"><span data-stu-id="ba4b2-167">Activate the solution by clicking the **Activate** button as shown in the figure.</span></span>
    
   <span data-ttu-id="ba4b2-168">**Рисунок: Активация решения диалогового окна и кнопка**</span><span class="sxs-lookup"><span data-stu-id="ba4b2-168">**Figure: Activate Solution dialog and button**</span></span>

  

  ![Активация решения после обновления.](../images/SPD15-PackagingWorkflow5.png)
  

  

  
<span data-ttu-id="ba4b2-p107">После активации решения рабочего процесса для семейства веб-сайтов может использоваться как компонент для всех дочерних сайтах. Чтобы активировать компонент рабочего процесса для дочерних сайтов, выполните следующую процедуру.</span><span class="sxs-lookup"><span data-stu-id="ba4b2-p107">After a workflow solution has been activated for a site collection, it is available as a feature for all sub-sites. To activate the workflow feature for a sub-site, follow this procedure.</span></span>
  
    
    

### <a name="activate-the-workflow-feature"></a><span data-ttu-id="ba4b2-172">Активация компонента рабочего процесса</span><span class="sxs-lookup"><span data-stu-id="ba4b2-172">Activate the workflow feature</span></span>


1. <span data-ttu-id="ba4b2-173">Откройте **Параметры сайта** на сайт, которую вы хотите активировать компонент рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="ba4b2-173">Open **Site Settings** on the site where you wish to activate the workflow feature.</span></span>
    
  
2. <span data-ttu-id="ba4b2-174">В меню " **Действия сайта** " выберите **Управление возможностями сайта**.</span><span class="sxs-lookup"><span data-stu-id="ba4b2-174">In the **Site Actions** group, click **Manage site features**.</span></span>
    
  
3. <span data-ttu-id="ba4b2-175">Выберите **Включить** рядом с компонентом рабочего процесса, как показано на рисунке.</span><span class="sxs-lookup"><span data-stu-id="ba4b2-175">Click **Activate** next to the workflow feature as shown in the figure.</span></span>
    
  

<span data-ttu-id="ba4b2-176">**Рисунок: Активируйте компонент рабочего процесса для сайта**</span><span class="sxs-lookup"><span data-stu-id="ba4b2-176">**Figure: Activate workflow feature for site**</span></span>

  
    
    

  
    
    
![Активация компонента сайта.](../images/SPD15-PackagingWorkflow6.png)
  
    
    

  
    
    

  
    
    

## <a name="additional-resources"></a><span data-ttu-id="ba4b2-178">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="ba4b2-178">Additional resources</span></span>
<span data-ttu-id="ba4b2-179"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="ba4b2-179"></span></span>


-  [<span data-ttu-id="ba4b2-180">Рабочий процесс в SharePoint </span><span class="sxs-lookup"><span data-stu-id="ba4b2-180">Workflow in SharePoint </span></span>](http://technet.microsoft.com/ru-ru/sharepoint/jj556245.aspx)
    
  
-  [<span data-ttu-id="ba4b2-181">Новые возможности рабочего процесса в SharePoint</span><span class="sxs-lookup"><span data-stu-id="ba4b2-181">What's new in workflow in SharePoint</span></span>](http://msdn.microsoft.com/library/6ab8a28b-fa2f-4530-8b55-a7f663bf15ea.aspx)
    
  
-  [<span data-ttu-id="ba4b2-182">Приступая к работе с рабочего процесса SharePoint</span><span class="sxs-lookup"><span data-stu-id="ba4b2-182">Getting started with SharePoint workflow</span></span>](http://msdn.microsoft.com/library/cc73be76-a329-449f-90ab-86822b1c2ee8.aspx)
    
  
-  [<span data-ttu-id="ba4b2-183">Разработка рабочих процессов в SharePoint Designer и Visio</span><span class="sxs-lookup"><span data-stu-id="ba4b2-183">Workflow development in SharePoint Designer and Visio</span></span>](workflow-development-in-sharepoint-designer-and-visio.md)
    
  
-  [<span data-ttu-id="ba4b2-184">Краткий справочник по действиям рабочего процесса (платформа рабочих процессов в SharePoint)</span><span class="sxs-lookup"><span data-stu-id="ba4b2-184">Workflow actions quick reference (SharePoint Workflow platform)</span></span>](workflow-actions-quick-reference-sharepoint-workflow-platform.md)
    
  
-  [<span data-ttu-id="ba4b2-185">Статья блога группы разработчиков SharePoint Designer: рабочий процесс упаковки и развертывания сценарий</span><span class="sxs-lookup"><span data-stu-id="ba4b2-185">Blog article from the SharePoint Designer team: Workflow package and deploy scenario</span></span>](http://blogs.msdn.com/b/sharepointdesigner/archive/2012/08/30/packaging-list-site-and-reusable-workflow-and-how-to-deploy-the-package.aspx)
    
  
