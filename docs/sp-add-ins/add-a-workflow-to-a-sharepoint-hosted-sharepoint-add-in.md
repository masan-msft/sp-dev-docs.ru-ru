# <a name="add-a-workflow-to-a-sharepoint-hosted-sharepoint-add-in"></a><span data-ttu-id="c8b66-101">Добавление рабочего процесса в надстройку с размещением в SharePoint</span><span class="sxs-lookup"><span data-stu-id="c8b66-101">Add a workflow to a SharePoint-hosted SharePoint Add-in</span></span>
<span data-ttu-id="c8b66-102">Узнайте, как добавить рабочий процесс в надстройку SharePoint.</span><span class="sxs-lookup"><span data-stu-id="c8b66-102">Learn how to include a workflow in a spappsing.</span></span>
 

 <span data-ttu-id="c8b66-p101">**Примечание.** Название "приложения для SharePoint" меняется на "надстройки SharePoint". В процессе перехода с одного названия на другое в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio по-прежнему может встречаться термин "приложения для SharePoint". Дополнительные сведения см. в статье [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="c8b66-p101">The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span></span>
 

<span data-ttu-id="c8b66-p102">Это шестая статья о разработке надстроек с размещением в SharePoint. Для начала вам следует ознакомиться со статьей [Надстройки SharePoint](sharepoint-add-ins) и предыдущими статьями из этой серии:</span><span class="sxs-lookup"><span data-stu-id="c8b66-p102">Learn how to surface a remote web form in a SharePoint page in a provider-hosted SharePoint Add-in. This is the sixth in a series of articles about the basics of developing provider-hosted SharePoint Add-ins. You should first be familiar with  [SharePoint Add-ins](sharepoint-add-ins) and the previous articles in this series:</span></span>
 

-  [<span data-ttu-id="c8b66-108">Знакомство с созданием надстроек SharePoint с размещением в SharePoint</span><span class="sxs-lookup"><span data-stu-id="c8b66-108">Get started creating SharePoint-hosted SharePoint Add-ins</span></span>](get-started-creating-sharepoint-hosted-sharepoint-add-ins)
    
 
-  [<span data-ttu-id="c8b66-109">Развертывание и установка надстроек SharePoint, размещаемых в SharePoint</span><span class="sxs-lookup"><span data-stu-id="c8b66-109">Deploy and install a SharePoint-hosted SharePoint Add-in</span></span>](deploy-and-install-a-sharepoint-hosted-sharepoint-add-in)
    
 
-  [<span data-ttu-id="c8b66-110">Добавление настраиваемых столбцов в надстройки, размещаемые в SharePoint</span><span class="sxs-lookup"><span data-stu-id="c8b66-110">Add custom columns to a SharePoint-hostedSharePoint Add-in</span></span>](add-custom-columns-to-a-sharepoint-hostedsharepoint-add-in)
    
 
-  [<span data-ttu-id="c8b66-111">Добавление настраиваемого типа контента в надстройки, размещаемые в SharePoint</span><span class="sxs-lookup"><span data-stu-id="c8b66-111">Add a custom content type to a SharePoint-hostedSharePoint Add-in</span></span>](add-a-custom-content-type-to-a-sharepoint-hostedsharepoint-add-in)
    
 
-  [<span data-ttu-id="c8b66-112">Добавление веб-части на страницу в надстройке с размещением в SharePoint</span><span class="sxs-lookup"><span data-stu-id="c8b66-112">Add a Web Part to a page in a SharePoint-hosted SharePoint Add-in</span></span>](add-a-web-part-to-a-page-in-a-sharepoint-hosted-sharepoint-add-in)
    
 

 <span data-ttu-id="c8b66-p103">**Примечание.** Если вы выполняли действия из предыдущих статей этой серии, у вас уже есть решение Visual Studio, которое можно использовать для работы с этой статьей. Вы также можете скачать репозиторий [SharePoint_SP-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_SP-hosted_Add-Ins_Tutorials) и открыть файл BeforeWorkflow.sln.</span><span class="sxs-lookup"><span data-stu-id="c8b66-p103">**Note** If you have been working through this series about SharePoint-hosted add-ins, then you have a Visual Studio solution that you can use to continue with this topic. You can also download the repository at  [SharePoint_SP-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_SP-hosted_Add-Ins_Tutorials) and open the BeforeColumns.sln file.</span></span>
 

<span data-ttu-id="c8b66-115">В этой статье в надстройку SharePoint добавляется рабочий процесс, который уведомляет отдел кадров о том, что новый сотрудник готов к заполнению документов.</span><span class="sxs-lookup"><span data-stu-id="c8b66-115">In this article you add a workflow the Employee Orientation spappsing that notifies the Human Resources (HR) department that a new employee is ready to fill out the HR paperwork.</span></span>
 

## <a name="add-a-workflow-to-an-add-in"></a><span data-ttu-id="c8b66-116">Добавление рабочего процесса в надстройку</span><span class="sxs-lookup"><span data-stu-id="c8b66-116">Add  a workflow to an add-in</span></span>


 

 

1. <span data-ttu-id="c8b66-p104">В **обозревателе решений** щелкните проект правой кнопкой мыши и выберите **Добавить** > **Новая папка**. Назовите папку "Рабочие процессы".</span><span class="sxs-lookup"><span data-stu-id="c8b66-p104">In  **Solution Explorer**, right-click the project and choose  **Add** > **New Folder**. Name the folder Workflows.</span></span>
    
 
2. <span data-ttu-id="c8b66-p105">Щелкните новую папку правой кнопкой мыши и выберите **Добавить** > **Новый элемент**. Откроется диалоговое окно **Добавление нового элемента** (узел **Office/SharePoint**).</span><span class="sxs-lookup"><span data-stu-id="c8b66-p105">Right-click the new folder and choose **Add** > **New Item**. The **Add New Item** dialog opens to the **Office/SharePoint** node.</span></span>
    
 
3. <span data-ttu-id="c8b66-p106">Выберите **Рабочий процесс** и присвойте ему имя HR_Intake. Выберите **Рабочий процесс списка** в качестве типа рабочего процесса и нажмите **Далее**.</span><span class="sxs-lookup"><span data-stu-id="c8b66-p106">Choose Workflow and give it the name HR_Intake. When prompted to choose the type of workflow, choose List Workflow, and choose Next.</span></span>
    
 
4. <span data-ttu-id="c8b66-123">На следующей странице мастера включите параметр **Да, связать...** и выберите в раскрывающихся списках следующие значения:</span><span class="sxs-lookup"><span data-stu-id="c8b66-123">On the next page of the wizard, enable the **Yes, associate ... **option and then set the drop down controls to the following values:</span></span>
    
      -  <span data-ttu-id="c8b66-124">**Библиотека или список, связываемые с рабочим процессом**</span><span class="sxs-lookup"><span data-stu-id="c8b66-124">**The library or list to associate your workflow with**</span></span>
    
    <span data-ttu-id="c8b66-125">Новые сотрудники в Москве</span><span class="sxs-lookup"><span data-stu-id="c8b66-125">New Employees in Seattle</span></span>
    
 
  -  <span data-ttu-id="c8b66-126">**Список журналов...**</span><span class="sxs-lookup"><span data-stu-id="c8b66-126">**The history list ...**</span></span>
    
    <create new>
    
 
  -  <span data-ttu-id="c8b66-127">**Список задач...**</span><span class="sxs-lookup"><span data-stu-id="c8b66-127">**The Task list ...**</span></span>
    
    <create new>
    
 

    <span data-ttu-id="c8b66-128">Нажмите **Далее**.</span><span class="sxs-lookup"><span data-stu-id="c8b66-128">Click **Next**.</span></span>
    
 
5. <span data-ttu-id="c8b66-129">На последней странице мастера включите *только* автоматический запуск рабочего процесса при *изменении* элемента.</span><span class="sxs-lookup"><span data-stu-id="c8b66-129">On the last page of the wizard, enable *only* the option to start the workflow automatically when an item is *changed*.</span></span>
    
 
6. <span data-ttu-id="c8b66-130">Нажмите **Готово**.</span><span class="sxs-lookup"><span data-stu-id="c8b66-130">Choose **Finish**.</span></span>
    
    <span data-ttu-id="c8b66-131">После этого Инструменты разработчика Office для Visual Studio сделают следующее:</span><span class="sxs-lookup"><span data-stu-id="c8b66-131">The Office Developer Tools for Visual Studio will do the following:</span></span>
    
      - <span data-ttu-id="c8b66-132">создадут рабочий процесс HR_Intake в папке **Рабочий процесс** с дочерним файлом Workflow.xaml, который открыт в конструкторе рабочих процессов;</span><span class="sxs-lookup"><span data-stu-id="c8b66-132">Create an HR_Intake workflow  in the **Workflow** folder, with a child Workflow.xaml file that is open in the workflow designer.</span></span>
    
 
  - <span data-ttu-id="c8b66-133">создадут экземпляр списка **WorkflowTaskList**, в котором создаются и обновляются задачи, входящие в рабочий процесс;</span><span class="sxs-lookup"><span data-stu-id="c8b66-133">Create a **WorkflowTaskList** list instance where tasks that are part of the workflow are created and updated.</span></span>
    
 
  - <span data-ttu-id="c8b66-134">создадут экземпляр списка **WorkflowHistoryList**, в который записываются различные этапы выполнения рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="c8b66-134">Create a **WorkflowHistoryList** list instance, which is a log of the various steps in each execution of the workflow as they occur.</span></span>
    
 
7. <span data-ttu-id="c8b66-135">Перетащите два новых экземпляра списка в папку **Списки**.</span><span class="sxs-lookup"><span data-stu-id="c8b66-135">Drag the two new list instances into the **Lists** folder.</span></span>
    
 

## <a name="design-the-workflow"></a><span data-ttu-id="c8b66-136">Создание рабочего процесса</span><span class="sxs-lookup"><span data-stu-id="c8b66-136">Design the workflow</span></span>

<span data-ttu-id="c8b66-p107">Рабочий процесс отправляет в отдел кадров уведомление о том, что новый сотрудник завершил этап ориентации **Экскурсия по офису** и готов к заполнению бумаг. Рабочий процесс запускают любые изменения в элементе списка "Новые сотрудники в Москве", но он работает, только если в поле "Этап ориентации" указано значение "Оформление документов в отделе кадров". В этом случае сотруднику отделку кадров отправляется сообщение, и в **WorkflowTaskList** добавляется соответствующая задача.</span><span class="sxs-lookup"><span data-stu-id="c8b66-p107">The workflow sends an email to notify an HR staffer that the new employee has finished the Tour of building stage of orientation and is ready to fill out the HR intake paperwork. Any change in an existing item on the New Employees in Seattle list triggers the workflow, but the workflow does nothing unless the Orientation Stage field of the list item is set to HR paperwork.  If it is, then an email is sent to an HR staffer and a task for that employee will be added to the WorkflowTaskList.</span></span> 
 

 

 <span data-ttu-id="c8b66-140">**Примечание.** При создании рабочего процесса на одном или нескольких элементах в конструкторе рабочих процессов будет появляться синий ромб с восклицательным знаком.</span><span class="sxs-lookup"><span data-stu-id="c8b66-140">**Note**  At various times when designing your workflow, a blue diamond symbol with an exclamation mark in it,</span></span> 
 
![Небольшой синий ромб с белым восклицательным знаком.](../../images/f7b82a70-80fe-4e7e-a0f5-5a78cd12b367.PNG)
 
<span data-ttu-id="c8b66-p108">Он указывает на временные ошибки. (Наведите указатель на символ, чтобы просмотреть краткое описание или откройте **список ошибок** в Visual Studio, чтобы узнать больше). Это побочные эффекты незавершенности рабочего процесса. Все они исчезнут после завершения этой процедуры.</span><span class="sxs-lookup"><span data-stu-id="c8b66-p108">At various times when designing your workflow, a blue diamond symbol with an exclamation mark in it, , will appear on one or more items in the workflow designer. These report temporary errors. (Hover the cursor over the symbol to see a brief message, or look in the Visual Studio **Error List** for details.) These are side effects of the incompleteness of the workflow. They should all be gone when you have finished this procedure.</span></span>
 


1. <span data-ttu-id="c8b66-146">Откройте панель элементов в Visual Studio, разверните узел **SharePoint — список** и перетащите **LookupSPListItem** в **Последовательность** в конструкторе.</span><span class="sxs-lookup"><span data-stu-id="c8b66-146">Open the Toolbox pane in vsnv, expand the  SP - List node, and then drag LookupSPListItem into the Sequence in the designer.</span></span>
    
 
2. <span data-ttu-id="c8b66-p109">Выберите элемент **LookupSPListItem**, чтобы его свойства появились в области **Свойства** Visual Studio. Присвойте свойствам следующие значения:</span><span class="sxs-lookup"><span data-stu-id="c8b66-p109">Select the **LookupSPListItem** so that its properties appear in the Visual Studio **Properties** pane. Set the following properties to these values:</span></span>
    
      -  <span data-ttu-id="c8b66-149">**ItemID:** (текущий элемент)</span><span class="sxs-lookup"><span data-stu-id="c8b66-149">**ItemId**: (current item)</span></span>
    
 
  -  <span data-ttu-id="c8b66-150">**ListID:** (текущий список)</span><span class="sxs-lookup"><span data-stu-id="c8b66-150">**ListId**: (current list)</span></span>
    
 
  -  <span data-ttu-id="c8b66-151">**DisplayName:** LookupCurrentNewEmployee</span><span class="sxs-lookup"><span data-stu-id="c8b66-151">**DisplayName:** LookupCurrentNewEmployee</span></span>
    
 

    <span data-ttu-id="c8b66-152">Теперь область **Свойства** должна выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c8b66-152">The **Properties** pane should now look like the following:</span></span>
    

    <span data-ttu-id="c8b66-153">**Область свойств LookupSPListItem**</span><span class="sxs-lookup"><span data-stu-id="c8b66-153">**Properties pane of LookupSPListItem**</span></span>

 

  ![Область свойств действия рабочего процесса "Поиск элемента списка". Заданы свойства ItemID, ListID и DisplayName.](../../images/60f3302e-ca9c-45be-b785-0c9f636181da.PNG)
 

    <span data-ttu-id="c8b66-155">Щелкните в любом месте за пределами области, чтобы сохранить изменения. Теперь рабочая область конструктора должна выглядеть следующим образом.</span><span class="sxs-lookup"><span data-stu-id="c8b66-155">Click anywhere outside the pane to save your changes and the designer surface should now look like this.</span></span>
    

    <span data-ttu-id="c8b66-156">**Последовательность в конструкторе рабочих процессов**</span><span class="sxs-lookup"><span data-stu-id="c8b66-156">**Sequence in the workflow designer**</span></span>

 

  ![Конструктор рабочих процессов с полем "Последовательность" и действием "Поиск текущего нового сотрудника".](../../images/c8fbf801-e8e4-444a-9d2e-c14e29f537de.PNG)
 

    
    
 
3. <span data-ttu-id="c8b66-p110">Щелкните ссылку **Получить свойства** внутри переименованного действия LookupCurrentNewEmployee в конструкторе. После этого в последовательность будет добавлено действие **GetDynamicValueProperties**.</span><span class="sxs-lookup"><span data-stu-id="c8b66-p110">Click the Get Properties link inside the (newly renamed) LookupCurrentNewEmployee activity in the designer. This adds a GetDynamicValueProperties activity to the sequence.</span></span>
    
 
4. <span data-ttu-id="c8b66-p111">Щелкните текст **Определить...** в действии **GetDynamicValueProperties**. После того откроется диалоговое окно **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="c8b66-p111">Click the **Define…** text in the **GetDynamicValueProperties** activity. This will open the **Properties** dialog.</span></span>
    
 
5. <span data-ttu-id="c8b66-163">В поле **Тип сущности** выберите **Элемент списка** _имя_экземпляра_списка_, где _имя_экземпляра_списка_ — это "Новые сотрудники в Москве".</span><span class="sxs-lookup"><span data-stu-id="c8b66-163">Set the Entity Type to List Item of  list_instance_name, where list_instance_name is New Employees in Seattle.</span></span>
    
 
6. <span data-ttu-id="c8b66-164">В столбце **Путь** щелкните верхнюю ячейку и выберите "Этап ориентации" из раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="c8b66-164">In the **Path** column, click the top cell and then choose Orientation Stage from the drop down.</span></span>
    
 
7. <span data-ttu-id="c8b66-165">Щелкните ячейку, расположенную ниже, и выберите **Обращение (Обращение)** из раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="c8b66-165">Click the cell below it and then choose **Title (Title)** from the drop down.</span></span>
    
 
8. <span data-ttu-id="c8b66-p112">Щелкните **Заполнить переменные**. Будут созданы переменные OrientationStage и **Title**, которые будут присвоены соответствующим полям в текущего элементе списка "Новые сотрудники в Москве". Диалоговое окно **Свойства** теперь должно выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c8b66-p112">Click **Populate Variables**. This will create a variables named OrientationStage and **Title** and assign each of the value of corresponding fields in the current item of the New Employees in Seattle list. The **Properties** dialog should now look like the following:</span></span>
    
    <span data-ttu-id="c8b66-169">**Диалоговое окно свойств действия рабочего процесса**</span><span class="sxs-lookup"><span data-stu-id="c8b66-169">**Properties dialog of workflow activity**</span></span>

 

  ![Диалоговое окно "Свойства" для действия получения динамических значений, в котором значение типа сущности задано для элементов списка новых сотрудников, а переменные Title и OrientationStage присвоены полям с теми же названиями.](../../images/36a841e7-ce1b-444c-9bfe-7cdc56399ec1.PNG)
 

 

 
9. <span data-ttu-id="c8b66-p113">Нажмите **ОК**. Рабочая область конструктора теперь должна выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c8b66-p113">Choose **OK**. The designer surface should now look like the following:</span></span>
    
    <span data-ttu-id="c8b66-173">**Конструктор рабочих процессов**</span><span class="sxs-lookup"><span data-stu-id="c8b66-173">**Workflow Designer**</span></span>

 

  ![Конструктор рабочих процессов с двумя действиями: поиск элемента списка и получение динамических значений.](../../images/cd8eb456-d883-491a-b171-38c1b9f64018.PNG)
 

    
    
 
10. <span data-ttu-id="c8b66-175">Откройте панель элементов в Visual Studio, разверните узел **Поток управления** и перетащите элемент **Если** в нижнюю часть области **Последовательность** под элемент **GetDynamicValueProperties**.</span><span class="sxs-lookup"><span data-stu-id="c8b66-175">Open the Toolbox pane in vsnv, expand the Control Flow node, and then drag If into the bottom of the Sequence below the GetDynamicValueProperties.</span></span>
    
 
11. <span data-ttu-id="c8b66-176">В поле **Условие** элемента **Если** введите OrientationStage=="Оформление документов в отделе кадров".</span><span class="sxs-lookup"><span data-stu-id="c8b66-176">In the Condition box of the If, enter OrientationStage=="HR paperwork".</span></span>
    
 
12. <span data-ttu-id="c8b66-177">Откройте панель элементов в Visual Studio, разверните узел **SharePoint — служебные программы** и перетащите элемент **Электронная почта** в поле **То** действия **Если**.</span><span class="sxs-lookup"><span data-stu-id="c8b66-177">Open the Toolbox pane in vsnv, expand the  SP - Utilities node, and then drag Email into the Then box of the If activity.</span></span>
    
 
13. <span data-ttu-id="c8b66-p114">Выберите действие **Электронная почта**. В области **Свойства** задайте значения свойств "Основной текст", "Тема" и "Кому". В каждом случае нажимайте кнопку выноски **. . .** и используйте открывшийся **редактор выражений**, чтобы ввести значение свойства, как показано в таблице ниже. Это строковые выражения C#, поэтому необходимо использовать кавычки именно так, как показано. `Title` здесь — это переменная, присвоенная ранее полю **Title** элемента списка (оно содержит имя сотрудника).</span><span class="sxs-lookup"><span data-stu-id="c8b66-p114">Select the **Email** activity. In the **Properties** pane,  set the values of the Body, Subject, and To properties. In each case, choose the callout button, **. . .**, for the property and use the **Expression Editor** that opens to  set the property's value as in the following table. These are C# string expressions, so use quotation marks exactly as shown. The Title`Title` here is a variable that you assigned earlier to the **Title** field  of the list item (which holds the name of the employee).</span></span>
    
      -  <span data-ttu-id="c8b66-183">**Основной текст:** `Title + " is waiting in the lobby to fill out benefits and employment forms."`</span><span class="sxs-lookup"><span data-stu-id="c8b66-183">body</span></span>
    
 
  -  <span data-ttu-id="c8b66-184">**Тема:** `Title + " is ready for HR paperwork"`</span><span class="sxs-lookup"><span data-stu-id="c8b66-184">subject</span></span>
    
 
  -  <span data-ttu-id="c8b66-185">**Кому:** `new System.Collections.ObjectModel.Collection<string>() {"your_O365_email"}`</span><span class="sxs-lookup"><span data-stu-id="c8b66-185">**to** `new System.Collections.ObjectModel.Collection<string>() {"your_O365_email"}`</span></span>
    
    <span data-ttu-id="c8b66-p115">Замените заполнитель *your_O365_email* идентификатором, который вы используете для входа в свою учетную запись разработчика Office 365, например *псевдоним*  @ *доменO365*  .sharepoint.com. Это строка C#, поэтому она должна быть в кавычках.</span><span class="sxs-lookup"><span data-stu-id="c8b66-p115">Replace the placeholder, your_O365_email, with the identity that you use to login to your Office 365 developer account, such as alias@O365domain.sharepoint.com. This is a C# string so it must be in quotation  marks.</span></span>
    
 
14. <span data-ttu-id="c8b66-188">Откройте панель элементов в Visual Studio, разверните узел **Среда выполнения** и перетащите элемент **TerminateWorkflow** в поле **Иначе** действия **Если**.</span><span class="sxs-lookup"><span data-stu-id="c8b66-188">Open the Toolbox pane in vsnv, expand the Runtime node, and then drag TerminateWorkflow into the Else box of the If activity.</span></span>
    
 
15. <span data-ttu-id="c8b66-p116">Выберите действие **TerminateWorkflow** в области **Свойства** и введите в поле **Причина** следующее значение, включая кавычки: "Не на этапе оформления документов в отделе кадров". Теперь конструктор должен выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c8b66-p116">Select the TerminateWorkflow activity and in the Properties pane, set the Reason to the following,  including the quotation marks: "Not at HR paperwork stage.". The designer should now look the following:</span></span>
    
    <span data-ttu-id="c8b66-191">**Конструктор рабочих процессов после завершения рабочего процесса**</span><span class="sxs-lookup"><span data-stu-id="c8b66-191">**Workflow designer when the workflow is complete**</span></span>

 

  ![Конструктор рабочих процессов с действиями поиска элемента списка, получения динамических значений, а также структурой "If Then Else". Действие обработки электронной почты относится к части с Then, а действие завершения рабочего процесса — к части с Else.](../../images/c1230e3b-d149-413c-aa66-d258250a4512.PNG)
 

 

 

## <a name="run-and-test-the-add-in"></a><span data-ttu-id="c8b66-194">Запуск и тестирование надстройки</span><span class="sxs-lookup"><span data-stu-id="c8b66-194">Run and test the add-in</span></span>


 

 

1. <span data-ttu-id="c8b66-p118">Нажмите клавишу F5, чтобы развернуть и запустить надстройку. Visual Studio установит надстройку на вашем тестовом сайте SharePoint и немедленно запустит её. Кроме того, откроется консоль **Узел службы тестирования** диспетчера рабочих процессов.</span><span class="sxs-lookup"><span data-stu-id="c8b66-p118">Use the F5 key to deploy and run your add-in. vsnv makes a temporary installation of the add-in on your test SharePoint site and immediately runs the add-in. The Workflow Manager's Test Service Host console also opens.</span></span>
    
 
2. <span data-ttu-id="c8b66-198">Когда откроется страница надстройки по умолчанию, откройте один из элементов для редактирования и присвойте параметру "Этап ориентации" значение "Оформление документов в отделе кадров".</span><span class="sxs-lookup"><span data-stu-id="c8b66-198">When the add-in's default page opens,  open one of the items for editing, and set the value of Orientation Stage to HR paperwork.</span></span> 
    
    <span data-ttu-id="c8b66-p119">В консоли **Узел службы тестирования** появится индикатор запуска рабочего процесса. Вскоре после этого появится индикатор завершения рабочего процесса. Ниже приведен пример:</span><span class="sxs-lookup"><span data-stu-id="c8b66-p119">In the **Test Service Host** console, an indication appears that the workflow has started. Shortly after, there is an indication that the workflow has completed. The following is an example:</span></span>
    

    <span data-ttu-id="c8b66-202">**Консоль "Узел службы тестирования"**</span><span class="sxs-lookup"><span data-stu-id="c8b66-202">**Service Test Host console**</span></span>

 

  ![Окно "Узел службы тестирования" рабочего процесса со строкой о начале рабочего процесса и строкой о его завершении. GUID экземпляра рабочего процесса указан в начале каждой строки.](../../images/2422936d-7ef6-4c90-a03f-30053fbb9743.PNG)
 

    
    
    
     <span data-ttu-id="c8b66-p121">**Примечание.** Если консоль **Узел службы тестирования** не открывается, включите отладку рабочего процесса. Щелкните правой кнопкой мыши имя проекта в **обозревателе решений** и выберите **Свойства**. Откройте вкладку **SharePoint** в области **Свойства** и установите флажок **Включить отладку рабочего процесса**.</span><span class="sxs-lookup"><span data-stu-id="c8b66-p121">If the **Test Service Host** console does not open, you may need to enable workflow debugging. Right-click the project name in **Solution Explorer** and choose **Properties**. Open the **SharePoint** tab on the **Properties** pane and check the box for **Enable Workflow debugging**.</span></span>
3. <span data-ttu-id="c8b66-p122">Перейдите в папку "Входящие" (Outlook) вашей учетной записи разработчика Office 365. В ней будет сообщение с темой "*Сотрудник* готов к оформлению документов в отделе кадров", где *Сотрудник* — имя сотрудника, чей элемент вы изменили. Текст сообщения будет таким: "*Сотрудник* ожидает в вестибюле для заполнения заявлений на соцобеспечение и трудоустройство". Ниже приведен пример:</span><span class="sxs-lookup"><span data-stu-id="c8b66-p122">Navigate to the email inbox (Outlook) of your Office 365 developer account. There is an email with the subject "*Employee* is ready for HR paperwork." where *Employee* is the name of the employee whose item you edited. The body of the email says "*Employee* is waiting in the lobby to fill out benefits and employment forms." The following is an example:</span></span>
    
    <span data-ttu-id="c8b66-213">**Письмо, отправленное рабочим процессом**</span><span class="sxs-lookup"><span data-stu-id="c8b66-213">**Email sent by workflow**</span></span>

 

  ![Электронное сообщение в Outlook из рабочего процесса. Указано сообщение в теме о готовности пользователя к оформлению документов для отдела кадров, а также текст об ожидании пользователя в зале, который планирует заполнить формы зачисления и соцобеспечения.](../../images/7b1d8f47-9c34-441e-af6a-3af4a8c65533.PNG)
 

    
    
    
     <span data-ttu-id="c8b66-p123">**Совет.** Если рабочий процесс начинает, но не завершает работу, и письмо не отправляется, завершите сеанс отладки и повторите запуск (F5) еще несколько раз, прежде чем решать, что в коде ошибка. Иногда проблема заключается в SharePoint Online. Если проблемы не исчезают, добавьте тип контента ** ListFieldsContentType **, если он еще не добавлен, в раздел **ContentTypes** файла schema.xml. Ниже приведен пример разметки. `<ContentType ID="0x0100781dd48170b94fdc9706313c82b3d04c" Name="ListFieldsContentType" Hidden="TRUE">`</span><span class="sxs-lookup"><span data-stu-id="c8b66-p123">**Tip**  If the workflow begins but never completes, and the email is not sent, try ending the debugging session and trying F5 again a few times before you conclude there is something wrong in your code. Sometimes the problem is in SharePoint Online. If you are still having problems, try adding a content type called  **ListFieldsContentType**, if there isn't one already, to the  **ContentTypes** section of the schema.xml file. The following is an example of the markup. `<ContentType ID="0x0100781dd48170b94fdc9706313c82b3d04c" Name="ListFieldsContentType" Hidden="TRUE">`</span></span>
 
 <span data-ttu-id="c8b66-219">`</ContentType>`Скопируйте весь раздел **FieldRefs** типа контента **NewEmployee** в этот новый тип контента. Сохраните проект, выполните отзыв и повторите запуск (F5).</span><span class="sxs-lookup"><span data-stu-id="c8b66-219">Then copy the whole of the **FieldRefs** section of the **NewEmployee** content type into this new content type.</span></span>
4. <span data-ttu-id="c8b66-p124">Чтобы завершить сеанс отладки, закройте окно браузера или остановите отладку в Visual Studio. При каждом нажатии клавиши F5 Visual Studio будет отзывать предыдущую версию надстройки и устанавливать ее последнюю версию.</span><span class="sxs-lookup"><span data-stu-id="c8b66-p124">To end the debugging session, close the browser window or stop debugging in Visual Studio. Each time that you press F5, Visual Studio will retract the previous version of the add-in and install the latest one.</span></span>
    
 
5. <span data-ttu-id="c8b66-p125">Эти надстройка и решение Visual Studio будут рассматриваться и в других статьях, поэтому при перерывах в работе рекомендуется отзывать надстройку. В **обозревателе решений** щелкните проект правой кнопкой мыши и выберите пункт **Отозвать**.</span><span class="sxs-lookup"><span data-stu-id="c8b66-p125">You will work with this add-in and Visual Studio solution in other articles, and it's a good practice to retract the add-in one last time when you are done working with it for a while. Right-click the project in **Solution Explorer** and choose **Retract**.</span></span>
    
 

## 
<span data-ttu-id="c8b66-224"><a name="Nextsteps"> </a></span><span class="sxs-lookup"><span data-stu-id="c8b66-224"></span></span>

<span data-ttu-id="c8b66-225">Следующая статья серии: [Добавление пользовательских страницы и стиля в надстройку с размещением в SharePoint](add-a-custom-page-and-style-to-a-sharepoint-hosted-sharepoint-add-in).</span><span class="sxs-lookup"><span data-stu-id="c8b66-225">In the next article in this series, you'll add  a custom page and style to the spappsing: Add a custom page and styles to a SharePoint-hosted Add-in.</span></span>
 

 

