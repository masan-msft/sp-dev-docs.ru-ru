---
title: "Как построение и развертывание настраиваемого действия рабочего процесса"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 9d2fa681-30c2-4549-9df2-ea9ed757fda9
ms.openlocfilehash: 35ccb0313dc0a30b0308ff9ce1cc4eef988b8fae
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-build-and-deploy-workflow-custom-actions"></a><span data-ttu-id="e7137-102">Как: построение и развертывание настраиваемого действия рабочего процесса</span><span class="sxs-lookup"><span data-stu-id="e7137-102">How to: Build and deploy workflow custom actions</span></span>
<span data-ttu-id="e7137-103">Узнайте, как моделировать бизнес-процессы, требования которых не соблюдаются существующей библиотекой действий бизнес-процессов в SharePoint Designer, путем создания пользовательских бизнес-процессов в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="e7137-103">Learn how to model business processes whose requirements are not met by the existing library of workflow actions in SharePoint Designer by creating custom workflow actions in SharePoint.</span></span>
<span data-ttu-id="e7137-104">SharePoint Designer предоставляет коллекцию действий рабочих процессов, которые доступны через пользовательский интерфейс конструктора рабочих процессов (пользовательский Интерфейс).</span><span class="sxs-lookup"><span data-stu-id="e7137-104">SharePoint Designer provides a collection of workflow actions that are available through the Workflow Designer user interface (UI).</span></span> <span data-ttu-id="e7137-105">Хотя диапазон действий рабочего процесса, включенные в SharePoint Designer) — это обширный, оно тем не менее конечное.</span><span class="sxs-lookup"><span data-stu-id="e7137-105">Although the range of workflow actions that are included in SharePoint Designer) is extensive, it is nevertheless finite.</span></span> <span data-ttu-id="e7137-106">В некоторых случаях может потребоваться модель с существующей библиотеки действий рабочего процесса, доступных в SharePoint Designer не выполняются, требования к бизнес-процесса.</span><span class="sxs-lookup"><span data-stu-id="e7137-106">In some cases, you may need to model a business process whose requirements are not met by the existing library of workflow actions that are available in SharePoint Designer.</span></span>
  
    
    

<span data-ttu-id="e7137-107">Распознавание, что бизнес-процессов часто есть специализированные требования, SharePoint позволяет создавать настраиваемые действия рабочих процессов.</span><span class="sxs-lookup"><span data-stu-id="e7137-107">Recognizing that business processes often have specialized requirements, SharePoint lets you create custom workflow actions.</span></span> <span data-ttu-id="e7137-108">Можно разрабатывать этих настраиваемых действий с помощью Visual Studio и затем создание пакета и их развертывание SharePoint.</span><span class="sxs-lookup"><span data-stu-id="e7137-108">You can develop these custom actions by using Visual Studio, and then package and deploy them to SharePoint.</span></span> <span data-ttu-id="e7137-109">На этом этапе настраиваемое действие становится доступным для авторов рабочих процессов в SharePoint Designer, точно так же, как если бы между библиотека существующего действия.</span><span class="sxs-lookup"><span data-stu-id="e7137-109">At that point, the custom action becomes available to workflow authors in SharePoint Designer, exactly as if it were among the library of existing actions.</span></span> <span data-ttu-id="e7137-110">Эта возможность позволяет настраивать функциональные возможности среды разработки рабочего процесса в соответствии с любой из специализированных бизнес-процессов.</span><span class="sxs-lookup"><span data-stu-id="e7137-110">This capability lets you customize the functionality in your workflow authoring environment to match any of your specialized business processes.</span></span>
> <span data-ttu-id="e7137-111">**Примечание:** Обеспечивает пример демонстрирует создание настраиваемых действий.</span><span class="sxs-lookup"><span data-stu-id="e7137-111">**Note:** A sample is provided that illustrates creating a custom action.</span></span> <span data-ttu-id="e7137-112">Образец, а также файл readme доступен здесь: [рабочего процесса SharePoint: Создание настраиваемого действия](http://code.msdn.microsoft.com/SharePoint-workflow-41e5c0f9) (http://code.msdn.microsoft.com/SharePoint-workflow-41e5c0f9).</span><span class="sxs-lookup"><span data-stu-id="e7137-112">The sample, along with a readme file, is available here:  [SharePoint workflow: Create a custom action](http://code.msdn.microsoft.com/SharePoint-workflow-41e5c0f9) (http://code.msdn.microsoft.com/SharePoint-workflow-41e5c0f9).</span></span>
  
    
    


## <a name="core-scenario-for-custom-workflow-actions"></a><span data-ttu-id="e7137-113">Основные сценарии для настраиваемые действия рабочих процессов</span><span class="sxs-lookup"><span data-stu-id="e7137-113">Core scenario for custom workflow actions</span></span>
<span data-ttu-id="e7137-114"><a name="bk_corescenario"> </a></span><span class="sxs-lookup"><span data-stu-id="e7137-114"><a name="bk_corescenario"> </a></span></span>

<span data-ttu-id="e7137-115">В следующей строке описательную регистрируются основного сценария для настраиваемые действия рабочих процессов.</span><span class="sxs-lookup"><span data-stu-id="e7137-115">The core scenario for custom workflow actions is captured in the following narrative line:</span></span>
  
    
    

1. <span data-ttu-id="e7137-p104">Бизнес-аналитик или другие не технической информационных работников использует SharePoint Designer для создания рабочих процессов для моделирования внутренних бизнес-процесса  например, процесс утверждения документов. Тем не менее в этой компании последний этап процесса , после окончательного утверждения для автоматически отправки документов на внешние принтер, который печатает и привязывает указанное число копий документа.</span><span class="sxs-lookup"><span data-stu-id="e7137-p104">A business analyst or other non-technical information worker is using SharePoint Designer to author a workflow to model an internal business process—for example, a document-approval process. However, in this company, the final step of the process is, upon final approval, to automatically dispatch the document to an external printer who prints and binds a specified number of copies of the document.</span></span> 
    
  
2. <span data-ttu-id="e7137-p105">Никаких действий рабочего процесса, который включен в SharePoint Designer 2013 поддерживает Отправка документа в внешнего принтера. Таким образом руководители компании решили инвестировать в поддержке этого настраиваемого действия (звонят его действие «Отправить файлы на принтер») для информационных работников компании.</span><span class="sxs-lookup"><span data-stu-id="e7137-p105">No workflow action that is included in SharePoint Designer 2013 supports dispatching a document to an external printer. Therefore, the company managers decide to invest in providing this custom action (they call it the "Send Files to Printer" action) for the company's information workers.</span></span>
    
  
3. <span data-ttu-id="e7137-p106">Поставщики предоставляют доступ к печати веб-служб. Для капитализации, разработчик создает настраиваемое действие **Отправить файлы на принтер**, с именем **SendFilesToPrinter**. Разработчик создает  декларативный рабочий процесс активности. Кроме того, разработчик затем создает действия рабочего процесса для предоставления пользовательского интерфейса и перетащите действие в SharePoint Designer.</span><span class="sxs-lookup"><span data-stu-id="e7137-p106">Vendors expose printing web services. To capitalize, a developer creates a custom **Send Files to Printer** action, named **SendFilesToPrinter**. What the developer creates is a declarative workflow activity. The developer also, then, creates the workflow action to provide the drag-and-drop UI for the action in SharePoint Designer.</span></span>
    
  
4. <span data-ttu-id="e7137-124">Разработчик пакеты **SendFilesToPrinter** активности и **Отправить файлы на принтер** действие в пакет (WSP-файл) файла решения SharePoint и развертывает его как компонент семейства сайтов в ферме SharePoint.</span><span class="sxs-lookup"><span data-stu-id="e7137-124">The developer packages both the **SendFilesToPrinter** activity and the **Send Files to Printer** action in a SharePoint solution package (.wsp) file and deploys it as a site collection feature to the SharePoint farm.</span></span>
    
  
5. <span data-ttu-id="e7137-125">После функцию развернуть и активировать, информационных работников видит нового настраиваемого действия, **Отправить файлы на принтер** в SharePoint Designer пользовательского интерфейса, а также все действия, обычно содержат и можно использовать так же, как все остальные файлы.</span><span class="sxs-lookup"><span data-stu-id="e7137-125">After the feature is deployed and activated, the information worker sees the new custom action, **Send Files to Printer**, in the SharePoint Designer UI along with all of the normally included actions and can use it just like all the others.</span></span>
    
  

## <a name="overview-of-custom-actions"></a><span data-ttu-id="e7137-126">Общие сведения о настраиваемых действий</span><span class="sxs-lookup"><span data-stu-id="e7137-126">Overview of custom actions</span></span>
<span data-ttu-id="e7137-127"><a name="bk_overviewcustact"> </a></span><span class="sxs-lookup"><span data-stu-id="e7137-127"><a name="bk_overviewcustact"> </a></span></span>

<span data-ttu-id="e7137-p107">Действие, которое является оболочкой, выделяет функциональность базового действия в SharePoint Designer. Во время выполнения базового активности не действие, выполняется в Windows Server AppFabric. В этом случае необходимо действия абстракций только во время разработки базовых функций в рабочем процессе SharePoint Designer разработки среды (только элементы SharePoint Designer, с помощью интерфейса.</span><span class="sxs-lookup"><span data-stu-id="e7137-p107">An action is a wrapper that abstracts the functionality of its underlying activity in SharePoint Designer. At run time, the underlying activity, not the action itself, is executed in the Windows Server AppFabric. In this sense, actions are just design-time abstractions of underlying functions in the SharePoint Designer workflow authoring environment (in addition to being elements of the SharePoint Designer using interface.</span></span>
  
    
    
<span data-ttu-id="e7137-131">Как и все действия, настраиваемые действия  «уровня веб-сайта»  то есть, активирован на уровне веб-сайта SharePoint или экземпляра **SharePoint.SPWeb**.</span><span class="sxs-lookup"><span data-stu-id="e7137-131">Like all actions, custom actions are "web scoped"—that is, they are activated at the level of the SharePoint website, or **SharePoint.SPWeb** instance.</span></span>
  
    
    
<span data-ttu-id="e7137-p108">Действия определяются в XML-файлы определений, которые имеют расширение имени файла .actions4. Базовый действие (или действия), с другой стороны, определенные в XAML-файл.</span><span class="sxs-lookup"><span data-stu-id="e7137-p108">Actions are defined in XML definition files that have the .actions4 file name extension. The underlying activity (or activities), on the other hand, are defined in a XAML file.</span></span>
  
    
    

## <a name="writing-custom-activities-in-visual-studio-2012"></a><span data-ttu-id="e7137-134">Создание настраиваемых действий в Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="e7137-134">Writing custom activities in Visual Studio 2012</span></span>
<span data-ttu-id="e7137-135"><a name="bk_writecustact"> </a></span><span class="sxs-lookup"><span data-stu-id="e7137-135"><a name="bk_writecustact"> </a></span></span>

<span data-ttu-id="e7137-p109">Visual Studio 2012 теперь содержит тип элемента "пользовательского действия рабочего процесса" в проекты SharePoint. Тип элемента можно использовать для создания настраиваемого действия, который затем можно импортировать в качестве настраиваемого действия в SharePoint Designer 2013.</span><span class="sxs-lookup"><span data-stu-id="e7137-p109">Visual Studio 2012 now provides a "workflow custom activity" item type within SharePoint projects. You can use the item type to create a custom activity that you can then import as a custom action in SharePoint Designer 2013.</span></span>
  
    
    

## <a name="example-create-package-and-deploy-a-custom-activity"></a><span data-ttu-id="e7137-138">Пример: Создание пакета и развертывание настраиваемого действия</span><span class="sxs-lookup"><span data-stu-id="e7137-138">Example: Create, package, and deploy a custom activity</span></span>
<span data-ttu-id="e7137-139"><a name="bk_createcustact"> </a></span><span class="sxs-lookup"><span data-stu-id="e7137-139"><a name="bk_createcustact"> </a></span></span>


### <a name="to-create-a-workflow-custom-activity"></a><span data-ttu-id="e7137-140">Создание настраиваемого действия рабочего процесса</span><span class="sxs-lookup"><span data-stu-id="e7137-140">To create a workflow custom activity</span></span>


1. <span data-ttu-id="e7137-141">Начните, открыв Visual Studio 2012 и создание нового проекта Visual C# типа **Проекта SharePoint**, как показано на рисунке 1.</span><span class="sxs-lookup"><span data-stu-id="e7137-141">Begin by opening Visual Studio 2012 and creating a new Visual C# project of type **SharePoint Project**, as shown in Figure 1.</span></span>
    
   <span data-ttu-id="e7137-142">**Рис. 1. Диалоговое окно "Новый проект"**</span><span class="sxs-lookup"><span data-stu-id="e7137-142">**Figure 1. New Project dialog box**</span></span>

  

  ![Диалоговое окно "Создание проекта"](../images/wfVS_NewProjectDialog.JPG)
  

  

  
2. <span data-ttu-id="e7137-p110">В **Обозревателе решений** щелкните правой кнопкой мыши узел имя проекта и выберите команду **Добавить** **Новый элемент**. Откроется диалоговое окно **Добавление нового элемента**, как показано на рисунке 2.</span><span class="sxs-lookup"><span data-stu-id="e7137-p110">In **Solution Explorer**, right-click the project name node, and choose **Add**, **New Item**. This opens the **Add New Item** dialog box, as shown in Figure 2.</span></span>
    
   <span data-ttu-id="e7137-146">**На рисунке 2. Добавление нового элемента**</span><span class="sxs-lookup"><span data-stu-id="e7137-146">**Figure 2. Add New Item dialog box**</span></span>

  

  ![Диалоговое окно "Создание элемента"](../images/wfVS_NewItem.JPG)
  

    
    
  
3. <span data-ttu-id="e7137-p111">В диалоговом окне **Добавление нового элемента** выберите тип элемента **Настраиваемого действия рабочего процесса** и присвойте ему понятное имя. На рисунке называется «WorkflowActionsModule1». Нажмите кнопку **Добавить**. Создается новый элемент, а предоставляется в область конструирования активности.</span><span class="sxs-lookup"><span data-stu-id="e7137-p111">In the **Add New Item** dialog box, choose the **Workflow Custom Activity** item type and give it a meaningful name. In the illustration, the name is "WorkflowActionsModule1". Then choose **Add**. The new item is created, and you are presented with the activity design surface.</span></span>
    
  
4. <span data-ttu-id="e7137-152">Если вкладки панели **элементов** не отображается, щелкните ее для предоставления узлы элементов.</span><span class="sxs-lookup"><span data-stu-id="e7137-152">If the **Toolbox** tab is not already showing, click it to expose the toolbox nodes.</span></span> <span data-ttu-id="e7137-153">Выберите узел **Рабочего процесса SharePoint** для отображения объектов разработки рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="e7137-153">Click the **SharePoint Workflow** node to show the workflow development objects.</span></span> <span data-ttu-id="e7137-154">Существует представлением объектов в панель элементов рабочего процесса на рисунке 3.</span><span class="sxs-lookup"><span data-stu-id="e7137-154">There is a partial view of objects in the workflow toolbox in Figure 3.</span></span>
    
   <span data-ttu-id="e7137-155">**На рисунке 3. Частичное представление панель инструментов рабочего процесса SharePoint**</span><span class="sxs-lookup"><span data-stu-id="e7137-155">**Figure 3. Partial view of SharePoint workflow toolbox**</span></span>

  

  ![Панель элементов рабочего процесса](../images/wfVS_WorkflowToolbox.jpg)
  

    
    
  
5. <span data-ttu-id="e7137-p113">Добавление нового действия (.actions4) и файлы действий (включающими) модуле рабочий процесс, при необходимости. Для добавления этих файлов, щелкните правой кнопкой мыши значок модуль действий в **Окне Обозреватель решений**, выберите команду **Добавить** и затем нажмите кнопку **Добавить действие** (для добавления нового файла action4) или **Новое действие** (Добавление нового действия).</span><span class="sxs-lookup"><span data-stu-id="e7137-p113">Add new action (.actions4) and activity (.xaml) files to your workflow module, as needed. To add these files, right-click the actions module icon in **Solution Explorer**, choose **Add**, and then choose either **Add Action** (to add a new action4 file) or **New Activity** (to add a new activity), as appropriate.</span></span>
    
  
<span data-ttu-id="e7137-p114">После создания действия модуль и добавьте действие и файлы действий проект должен быть похож, depicted в на рисунке 5. Вы увидите один файл .actions4 для каждого действия, который вы добавили и один XAML-файл для каждого действия. Кроме того будут иметь старый файл Elements.xml и модуль XAML-файл.</span><span class="sxs-lookup"><span data-stu-id="e7137-p114">After you create your actions module and add your action and activity files, your project should look something like that depicted in Figure 5. You will see one .actions4 file for each action that you added, and one .xaml file for each activity. Additionally, you will have an Elements.xml file and the module's .xaml file.</span></span>
  
    
    

<span data-ttu-id="e7137-162">**На рисунке 5. Модуль действия рабочего процесса в окне Обозреватель решений**</span><span class="sxs-lookup"><span data-stu-id="e7137-162">**Figure 5. Workflow actions module in Solution Explorer**</span></span>

  
    
    

  
    
    
![Узел активности в обозревателе решений](../images/wfVS_ActivityNode.jpg)
  
    
    
<span data-ttu-id="e7137-p115">После создания вашего пользовательского действия рабочего процесса, вы можно упаковать и развернуть его. После развертывания, настраиваемого действия могут использоваться SharePoint Designer 2013 как настраиваемое действие.</span><span class="sxs-lookup"><span data-stu-id="e7137-p115">After you create your custom workflow activity, you can then package and deploy it. After it is deployed, the custom activity can be consumed by SharePoint Designer 2013 as a custom action.</span></span>
  
    
    
<span data-ttu-id="e7137-p116">Настраиваемые действия упакованных и развертываются как компоненты SharePoint в пакет (WSP-файл) файлы решения SharePoint. Пакет решения содержит модуль настраиваемых действий, которая представляет собой набор файлов, которые развертываются в SharePoint. В этом модуле может содержать любое число определений действий рабочего процесса, каждый из которых является XAML-файл. Модуль также содержит файлы действия (.actions4). Каждый файл действия содержит несколько действий, связанные с действиями в модуле или на собственный действия, которые доступны в установке SharePoint по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="e7137-p116">Custom actions are packaged and deployed as SharePoint Features in SharePoint solution package (.wsp) files. The solution package contains a custom actions module, which is a set of files that are deployed on SharePoint. This module can contain any number of workflow activity definitions, each of which is a .xaml file. The module also contains actions (.actions4) files. Each actions file contains multiple actions that refer to the activities in the module, or to native activities that are available on a default SharePoint installation.</span></span>
  
    
    
<span data-ttu-id="e7137-p117">После файла пакета (WSP-файл) решений загружаться и активировать на целевой веб-сайт (то есть, семейство сайтов SharePoint), функции, содержащиеся в пакете, установленных и доступных для активации. После активации дополнительных действий они доступны для использования в рабочем процессе.</span><span class="sxs-lookup"><span data-stu-id="e7137-p117">After a solution package (.wsp) file is uploaded and activated on the target website (that is, the SharePoint site collection), the features that are contained in the package are installed and available for activation. After the custom actions are activated, they are available for use in a workflow.</span></span> 
  
    
    

## <a name="updating-and-deleting-custom-actions"></a><span data-ttu-id="e7137-173">Обновление и удаление настраиваемых действий</span><span class="sxs-lookup"><span data-stu-id="e7137-173">Updating and deleting custom actions</span></span>
<span data-ttu-id="e7137-174"><a name="bk_updatecustact"> </a></span><span class="sxs-lookup"><span data-stu-id="e7137-174"><a name="bk_updatecustact"> </a></span></span>

<span data-ttu-id="e7137-p118">После развертывания настраиваемого действия, можно обновить или удалить очень легко. Все, что вам нужно сделать  откройте проект активности в Visual Studio, внесите изменения, необходимо и затем создание пакета и снова развернуть как описано в предыдущей процедуре. Чтобы удалить настраиваемое действие, только что можно удалить компонента в конечное семейство веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="e7137-p118">After your custom action is deployed, you can update or remove it very easily. All you have to do is open the activity project in Visual Studio, make the changes that you want, and then package and redeploy as described in the preceding procedure. To remove the custom action, you can just uninstall the feature on the target site collection.</span></span>
  
    
    

### <a name="feature-activation"></a><span data-ttu-id="e7137-178">Активация компонента</span><span class="sxs-lookup"><span data-stu-id="e7137-178">Feature activation</span></span>

<span data-ttu-id="e7137-p119">Активация компонента дополнительного действия в семейства веб-сайтов (то есть, экземпляра объекта **SPWeb** ) успешно только в том случае, если Azure / Workflow Manager Client 1.0 (модуль одним экземпляром рабочего процесса) правильно настроен. Следующие два советы, которые могут помочь обеспечить правильную настройку:</span><span class="sxs-lookup"><span data-stu-id="e7137-p119">Activating a custom action feature on a site collection (that is, on an **SPWeb** instance) succeeds only if the Azure/ Workflow Manager Client 1.0 (the multitenant workflow engine) is correctly configured. Two troubleshooting hints that may help ensure a correct configuration include:</span></span>
  
    
    

- <span data-ttu-id="e7137-181">Переход на страницу веб-узла и проверка того, что активации компонента, который содержит настраиваемое действие.</span><span class="sxs-lookup"><span data-stu-id="e7137-181">Going to the Site Features page and ensuring that the feature that contains the custom action is activated.</span></span>
    
  
- <span data-ttu-id="e7137-182">Запроса к базе данных Workflow Manager Client 1.0, чтобы убедиться, что действие успешно развернуты.</span><span class="sxs-lookup"><span data-stu-id="e7137-182">Querying the Workflow Manager Client 1.0 database to ensure that the activity is successfully deployed.</span></span>
    
  

## <a name="additional-resources"></a><span data-ttu-id="e7137-183">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="e7137-183">Additional resources</span></span>
<span data-ttu-id="e7137-184"><a name="bk_addlresources"> </a></span><span class="sxs-lookup"><span data-stu-id="e7137-184"><a name="bk_addlresources"> </a></span></span>


-  [<span data-ttu-id="e7137-185">Основные сведения о рабочих процессах в SharePoint</span><span class="sxs-lookup"><span data-stu-id="e7137-185">SharePoint workflow fundamentals</span></span>](sharepoint-workflow-fundamentals.md)
    
  
-  [<span data-ttu-id="e7137-186">Справочник по действий рабочих процессов для SharePoint</span><span class="sxs-lookup"><span data-stu-id="e7137-186">Workflow actions and activities reference for SharePoint</span></span>](workflow-actions-and-activities-reference-for-sharepoint.md)
    
  
-  [<span data-ttu-id="e7137-187">Разработка рабочих процессов в SharePoint с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e7137-187">Develop SharePoint workflows using Visual Studio</span></span>](develop-sharepoint-workflows-using-visual-studio.md)
    
  

