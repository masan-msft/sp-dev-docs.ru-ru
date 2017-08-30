
# <a name="include-a-custom-button-in-the-provider-hosted-add-in"></a><span data-ttu-id="2210a-101">Добавление настраиваемой кнопки в надстройку, размещенную у поставщика</span><span class="sxs-lookup"><span data-stu-id="2210a-101">Include a custom button in the provider-hosted add-in</span></span>
<span data-ttu-id="2210a-102">Узнайте, как добавить настраиваемую кнопку ленты в надстройку SharePoint, размещаемую у поставщика.</span><span class="sxs-lookup"><span data-stu-id="2210a-102">Learn how to include a custom ribbon button in a provider-hosted spappsing.</span></span>
 

 <span data-ttu-id="2210a-p101">**Примечание.** В настоящее время идет процесс замены названия "приложения для SharePoint" названием "надстройки SharePoint". Во время этого процесса в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio может по-прежнему использоваться термин "приложения для SharePoint". Дополнительные сведения см. в статье [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="2210a-p101">The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span></span>
 

<span data-ttu-id="2210a-p102">Это третья часть серии статей, посвященной основам разработки надстроек SharePoint, размещаемых у поставщика. Для начала вам следует ознакомиться со статьей [Надстройки SharePoint](sharepoint-add-ins) и предыдущими статьями из этой серии.</span><span class="sxs-lookup"><span data-stu-id="2210a-p102">Learn how to include a custom ribbon button in a provider-hosted SharePoint Add-in. This is the third in a series of articles about the basics of developing provider-hosted SharePoint Add-ins. You should first be familiar with  [SharePoint Add-ins](sharepoint-add-ins) and the previous articles in this series:</span></span>
 

-  [<span data-ttu-id="2210a-108">Знакомство с созданием надстроек SharePoint с размещением у поставщика</span><span class="sxs-lookup"><span data-stu-id="2210a-108">Get started creating provider-hosted SharePoint Add-ins</span></span>](get-started-creating-provider-hosted-sharepoint-add-ins)
    
 
-  [<span data-ttu-id="2210a-109">Настройка внешнего вида надстройки SharePoint, размещенной у поставщика</span><span class="sxs-lookup"><span data-stu-id="2210a-109">Give your provider-hosted add-in the SharePoint look-and-feel</span></span>](give-your-provider-hosted-add-in-the-sharepoint-look-and-feel)
    
 

 <span data-ttu-id="2210a-p103">**Примечание.** Если вы изучали предыдущие статьи этой серии о надстройках, размещаемых у поставщика, то у вас уже есть решение для Visual Studio, которое можно использовать для работы с данной статьей. Кроме того, вы можете скачать репозиторий [SharePoint_SP-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_Provider-hosted_Add-ins_Tutorials) и открыть файл BeforeRibbonButton.sln.</span><span class="sxs-lookup"><span data-stu-id="2210a-p103">**Note** If you have been working through this series about provider-hosted add-ins, then you have a Visual Studio solution that you can use to continue with this topic. You can also download the repository at  [SharePoint_Provider-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_Provider-hosted_Add-ins_Tutorials) and open the BeforeRibbonButton.sln file.</span></span>
 

<span data-ttu-id="2210a-p104">Надстройка SharePoint может включать дополнительные действия, представляющие собой условие SharePoint для настраиваемых элементов меню или кнопок ленты. В данной статье рассказывается, как создать настраиваемую кнопку, которая синхронизирует список SharePoint с удаленной базой данных.</span><span class="sxs-lookup"><span data-stu-id="2210a-p104">A SharePoint Add-in can include custom actions, which is the SharePoint term for a custom menu items or ribbon buttons. In this article you'll learn how to create a custom button that synchronizes a SharePoint list with a remote database.</span></span>
 

## <a name="create-a-custom-list-on-the-host-website"></a><span data-ttu-id="2210a-114">Создание настраиваемого списка на хост-сайте</span><span class="sxs-lookup"><span data-stu-id="2210a-114">Create a custom list on the host website</span></span>

<span data-ttu-id="2210a-p105">Предполагается, что настраиваемая кнопка будет размещена на ленте определенного списка, в котором записаны сведения о сотрудниках местного магазина. В одной из следующих статей этой серии вы узнаете, как программным способом добавить настраиваемый список на хост-сайт, а при изучении данной статьи вы добавите такой список вручную.</span><span class="sxs-lookup"><span data-stu-id="2210a-p105">The custom button is going to be on the ribbon of a specific list that records the employees of the local store. In a later article in this series, you'll learn how to programmatically add a custom list to a host website, but for now you'll add one manually.</span></span> 
 

 

1. <span data-ttu-id="2210a-117">На начальной странице магазина Fabrikam в Гонконге выберите пункты **Содержимое сайта | Добавить надстройку | Настраиваемый список**.</span><span class="sxs-lookup"><span data-stu-id="2210a-117">From the home page of the Fabrikam Hong Kong Store, navigate to **Site Contents | add an add-in | Custom List**.</span></span> 
    
 
2. <span data-ttu-id="2210a-118">В диалоговом окне **Добавление настраиваемого списка** укажите имя "Local Employees" (Местные сотрудники) и нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="2210a-118">In the **Adding Custom List** dialog, specifyLocal Employees as the name and press **Create**.</span></span> 
    
 
3. <span data-ttu-id="2210a-119">На странице **Содержимое сайта** откройте список **Местные сотрудники**.</span><span class="sxs-lookup"><span data-stu-id="2210a-119">On the **Site Contents** page, open the **Local Employees** list.</span></span>
    
 
4. <span data-ttu-id="2210a-120">Откройте вкладку **Список** на ленте, а затем нажмите кнопку **Параметры списка**.</span><span class="sxs-lookup"><span data-stu-id="2210a-120">Open the **List** tab on the ribbon, and then click the **List Settings** button.</span></span>
    
 
5. <span data-ttu-id="2210a-121">В разделе **Столбцы** на странице **Параметры списка** выберите столбец **Название**.</span><span class="sxs-lookup"><span data-stu-id="2210a-121">In the **Columns** section of the **List Settings** page, click the **Title** column.</span></span>
    
 
6. <span data-ttu-id="2210a-122">В форме **Изменение столбца** измените значение в поле **Имя столбца** с "Название" на "Имя", а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="2210a-122">In the **Edit Column** form, change the **Column name** from Title toName; and then click **OK**.</span></span>
    
 
7. <span data-ttu-id="2210a-123">На странице **Параметры** нажмите **Создать столбец**.</span><span class="sxs-lookup"><span data-stu-id="2210a-123">On the **Settings** page, click **Create column**.</span></span>
    
 
8. <span data-ttu-id="2210a-124">В форме **Создание столбца** выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="2210a-124">In the **Create Column** form, do the following:</span></span>
    
      1. <span data-ttu-id="2210a-125">В поле **Имя столбца** введите "Добавлено в корпоративную базу данных".</span><span class="sxs-lookup"><span data-stu-id="2210a-125">Enter Added to Corporate DB as the **Column name**.</span></span>
    
 
  2. <span data-ttu-id="2210a-126">Выберите тип **Да/нет (флажок)**.</span><span class="sxs-lookup"><span data-stu-id="2210a-126">Set the type to **Yes/No (check box)**.</span></span>
    
 
  3. <span data-ttu-id="2210a-127">В поле **Значение по умолчанию** укажите значение **Нет**.</span><span class="sxs-lookup"><span data-stu-id="2210a-127">Set the **Default value** to **No**.</span></span>
    
 
  4. <span data-ttu-id="2210a-p106">Нажмите кнопку **ОК**. Снова откроется страница **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="2210a-p106">Press **OK**. You are taken back to the **Settings** page.</span></span>
    
 
9. <span data-ttu-id="2210a-p107">Выберите **Содержимое сайта**, чтобы открыть страницу **Содержимое сайта**. Она содержит плитку нового списка. Откройте ее.</span><span class="sxs-lookup"><span data-stu-id="2210a-p107">Click **Site Contents** to open the **Site Contents** page. The tile for the new list is there. Open it.</span></span>
    
 
10. <span data-ttu-id="2210a-p108">Нажмите **Создать элемент**, а затем в форме создания элемента введите имя, но *не* устанавливайте флажок **Добавлено в корпоративную базу данных**. Затем нажмите кнопку **Сохранить**. Список должен выглядеть примерно так:</span><span class="sxs-lookup"><span data-stu-id="2210a-p108">Click **new item** and on the create item form, enter a name, but do *not*  check **Added to Corporate DB**. Then click **Save**. The list should look similar to the following:</span></span>
    
  ![Список местных сотрудников с одним элементом. Имя — Григорий Иванов. В столбце "Добавлено в корпоративную базу данных" указано значение "Нет".](../../images/a3371859-e42f-49ea-8f17-48d8a248b075.PNG)
 

 

 

## <a name="add-the-custom-button"></a><span data-ttu-id="2210a-139">Добавление настраиваемой кнопки</span><span class="sxs-lookup"><span data-stu-id="2210a-139">Add the custom button</span></span>

<span data-ttu-id="2210a-p110">В этом разделе вы добавите в надстройку часть кода, которая будет развертывать кнопку на ленте списка. Когда пользователь выделяет сотрудника в списке и нажимает кнопку, имя сотрудника добавляется в корпоративную базу данных, а в поле **Добавлено в корпоративную базу данных** для этого сотрудника значение "Нет" меняется на "Да".</span><span class="sxs-lookup"><span data-stu-id="2210a-p110">In this section, you include markup in the add-in that will deploy a button to the list's ribbon. When a user highlights an employee on the list and clicks the button, the employee's name will be added to the corporate database and the **Added to Corporate DB** field for the employee will be switched from No to Yes.</span></span>
 

 

1.  <span data-ttu-id="2210a-p111">*Если открыт Visual Studio, вам придется закрыть его*  и повторно открыть решение Chain Store, чтобы Visual Studio обнаружил новый список. (Запустите Visual Studio от имени администратора.)</span><span class="sxs-lookup"><span data-stu-id="2210a-p111">*If Visual Studio is open, you have to close it*  and reopen the Chain Store solution so that Visual Studio can discover your new list. (Run Visual Studio as an administrator.)</span></span>
    
     <span data-ttu-id="2210a-p112">**Примечание.** Параметры запускаемых проектов в Visual Studio обычно возвращаются к значениям по умолчанию каждый раз, когда вы заново открываете решение. Открывая пример решения, рассматриваемый в этой серии статей, всегда выполняйте следующие действия: щелкните правой кнопкой мыши узел решения в **обозревателе решений** и выберите пункт **Назначить запускаемые проекты**, а затем убедитесь, что для всех трех проектов в столбце **Действие** задано значение **Запуск**.</span><span class="sxs-lookup"><span data-stu-id="2210a-p112">**Note**   The settings for Startup Projects in Visual Studio tend to revert to defaults whenever the solution is reopened. Always take these steps immediately after reopening the sample solution in this series of articles: Right-click the solution node at the top of **Solution Explorer** and select **Set startup projects**.  Make sure all three projects are set to **Start** in the **Action** column.</span></span>
2. <span data-ttu-id="2210a-147">В **обозревателе решений** щелкните правой кнопкой мыши проект **ChainStore** и выберите пункты **Добавить | Создать элемент**.</span><span class="sxs-lookup"><span data-stu-id="2210a-147">Right-click the **ChainStore** project in **Solution Explorer** and choose **Add | New Item**.</span></span> 
    
 
3. <span data-ttu-id="2210a-148">В диалоговом окне **Добавление нового элемента** выберите **Настраиваемое действие ленты**, укажите имя AddEmployeeToCorpDB, а затем нажмите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="2210a-148">In the **Add New Item** dialog, select **Ribbon Custom Action**, give it the name AddEmployeeToCorpDB, and then click **Add**.</span></span>
    
 
4. <span data-ttu-id="2210a-p113">Откроется диалоговое окно с тремя вопросами. Выберите следующие ответы:</span><span class="sxs-lookup"><span data-stu-id="2210a-p113">The dialog that opens asks three questions. Give the following answers:</span></span>
    

|<span data-ttu-id="2210a-151">**Вопрос**</span><span class="sxs-lookup"><span data-stu-id="2210a-151">**Question**</span></span>|<span data-ttu-id="2210a-152">**Ответ**</span><span class="sxs-lookup"><span data-stu-id="2210a-152">**Give this answer:**</span></span>|
|:-----|:-----|
|<span data-ttu-id="2210a-153">**Где требуется предоставить настраиваемое действие?**</span><span class="sxs-lookup"><span data-stu-id="2210a-153">**Where do you want to expose the custom action?**</span></span>|<span data-ttu-id="2210a-154">Хост-сайт</span><span class="sxs-lookup"><span data-stu-id="2210a-154">Host Web</span></span>|
|<span data-ttu-id="2210a-155">**К какой области относится настраиваемое действие?**</span><span class="sxs-lookup"><span data-stu-id="2210a-155">**Where is the custom action scoped to?**</span></span>|<span data-ttu-id="2210a-156">Экземпляр списка</span><span class="sxs-lookup"><span data-stu-id="2210a-156">List Instance</span></span>|
|<span data-ttu-id="2210a-157">**Каким конкретным элементом ограничена область настраиваемого действия?**</span><span class="sxs-lookup"><span data-stu-id="2210a-157">**Which particular item is the custom action scoped to?**</span></span>|<span data-ttu-id="2210a-158">Местные сотрудники</span><span class="sxs-lookup"><span data-stu-id="2210a-158">Local Employees</span></span>|
5. <span data-ttu-id="2210a-159">Нажмите кнопку **Далее**. Появятся еще три вопроса.</span><span class="sxs-lookup"><span data-stu-id="2210a-159">Click **Next** and you get three more questions:</span></span>
    

|<span data-ttu-id="2210a-160">**Вопрос**</span><span class="sxs-lookup"><span data-stu-id="2210a-160">**Question**</span></span>|<span data-ttu-id="2210a-161">**Ответ**</span><span class="sxs-lookup"><span data-stu-id="2210a-161">**Give this answer:**</span></span>|
|:-----|:-----|
|<span data-ttu-id="2210a-162">**Где расположен этот элемент управления?**</span><span class="sxs-lookup"><span data-stu-id="2210a-162">**Where is the control located?**</span></span>|<span data-ttu-id="2210a-163">Ribbon.ListItem.Actions</span><span class="sxs-lookup"><span data-stu-id="2210a-163">Ribbon.ListItem.Actions</span></span>|
|<span data-ttu-id="2210a-164">**Какой текст должен отображаться на подписи этой кнопки?**</span><span class="sxs-lookup"><span data-stu-id="2210a-164">**What is the label text for the button control?**</span></span>|<span data-ttu-id="2210a-165">Добавить в корпоративную базу данных</span><span class="sxs-lookup"><span data-stu-id="2210a-165">Add to Corporate DB</span></span>|
|<span data-ttu-id="2210a-166">**Куда ведет элемент управления "кнопка"?**</span><span class="sxs-lookup"><span data-stu-id="2210a-166">**Where does the button control navigate to?**</span></span>|<span data-ttu-id="2210a-167">ChainStoreWeb\Pages\EmployeeAdder.aspx (это страница, код которой будет добавлять сотрудника в базу данных)</span><span class="sxs-lookup"><span data-stu-id="2210a-167">ChainStoreWebPagesEmployeeAdder.aspx (This is a page whose code behind is going to add the employee to the database.)</span></span>|
6. <span data-ttu-id="2210a-168">Нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="2210a-168">Click **Finish**.</span></span>
    
    <span data-ttu-id="2210a-p114">Файл elements.xml, который определяет дополнительное действие, будет добавлен в проект и открыт. Вы можете обращаться с этим файлом как с "черным ящиком". Вам не потребуется вносить в него изменения до знакомства со следующими частями этой серии. А сейчас обратите внимание на указанный ниже момент.</span><span class="sxs-lookup"><span data-stu-id="2210a-p114">An elements.xml file that defines the custom action is added to the project and opened. For the most part, you can treat this file as a black box, and you won't need to make any changes in it untill a later article in this series. For now, note only the following:</span></span>
    
      - <span data-ttu-id="2210a-p115">Для атрибута **Location** элемента **CommandUIDefinition** задано значение `Ribbon.ListItem.Actions.Controls_children`. Его вторая часть (`ListItem`) идентифицирует вкладку на ленте, на которую будет помещена кнопка (но это может и не быть точным отображаемым именем вкладки), а третья часть (`Actions`) — это имя раздела ленты, в который будет помещена кнопка.</span><span class="sxs-lookup"><span data-stu-id="2210a-p115">The **Location** attribute of the **CommandUIDefinition** element has the value `Ribbon.ListItem.Actions.Controls_children`. The second part of this,  `ListItem`, identifies the tab on the ribbon where the button will be placed (but that may not be the exact display name of the tab) and the third part,  `Actions`, is the name of the section of the ribbon where the button will be placed.</span></span>
    
 
  - <span data-ttu-id="2210a-p116">Атрибут **CommandAction** элемента **CommandUIHandler** начинается с заполнителя `~remoteAppUrl`. При развертывании кнопки он будет заменен на URL-адрес удаленного веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="2210a-p116">The **CommandAction** attribute of the **CommandUIHandler** element begins with the placeholder `~remoteAppUrl`. This will be replaced with the URL of the remote web application when the button is deployed.</span></span>
    
 
  - <span data-ttu-id="2210a-p117">В значение **CommandAction** добавлены несколько параметров запроса с временными значениями в фигурных скобках. Эти заполнители разрешаются во время выполнения. Обратите внимание, что один из них представляет собой идентификатор элемента списка, выбранного пользователем перед нажатием настраиваемой кнопки на ленте.</span><span class="sxs-lookup"><span data-stu-id="2210a-p117">A few query parameters have been added to the **CommandAction** value with placeholder values in braces "{ }". These placeholders are resolved at runtime. Note that one of them is the ID of the list item that is selected by the user before she presses the custom button on the ribbon.</span></span>
    
 
7. <span data-ttu-id="2210a-p118">В проекте **ChainStoreWeb** откройте файл **Pages/EmployeeAdder.aspx**. Обратите внимание, что он не содержит пользовательского интерфейса. Надстройка будет использовать эту страницу в качестве веб-службы. Это возможно благодаря тому, что в классе **System.Web.UI.Page** ASP.NET реализован объект **System.Web.IHttpHandler**, а событие **Page\_Load** автоматически выполняется при запросе страницы.</span><span class="sxs-lookup"><span data-stu-id="2210a-p118">In the ChainStoreWeb project, open the Pages/EmployeeAdder.aspx file. Notice that it doesn't have any UI. The add-in is going to use this page as a kind of web service. This is possible because the ASP.NET System.Web.UI.Page class implements System.Web.IHttpHandler and because the Page_Load event runs automatically when the page is requested.</span></span>
    
 
8. <span data-ttu-id="2210a-p119">Откройте файл с кодом **Pages/EmployeeAdder.aspx.cs**. В нем уже есть метод, который добавляет сотрудника в удаленную базу данных (`AddLocalEmployeeToCorpDB`). В нем используется объект **SharePointContext** для получения URL-адреса хост-сайта, который надстройка использует в качестве своего дискриминатора клиента. Таким образом, в первую очередь метод **Page_Load** должен инициализировать этот объект. Объект создается и помещается в кэш в том же сеансе, в котором загружается начальная страница надстройки, поэтому добавьте приведенный ниже код в метод **Page_Load** (объект **SharePointContext** определен в файле SharePointContext.cs, который Инструменты разработчика Office для Visual Studio создают при создании решения надстройки).</span><span class="sxs-lookup"><span data-stu-id="2210a-p119">Open the code behind file **Pages/EmployeeAdder.aspx.cs**. The method that adds the employee to the remote database,  `AddLocalEmployeeToCorpDB`, is already present. It uses the **SharePointContext** object to get the host web's URL, which the add-in uses as its tenant discriminator. So the first thing the **Page_Load** method needs to do is initialize this object. The object is created and cached in the Session when the add-in's start page loads, so add the following code to the **Page_Load** method. (The **SharePointContext** object is defined in the SharePointContext.cs file that the Office Developer Tools for Visual Studio generate when the add-in solution is created.)</span></span>
    
```C#
  spContext = Session["SPContext"] as SharePointContext;
```

9. <span data-ttu-id="2210a-p120">Метод  `AddLocalEmployeeToCorpDB` использует имя сотрудника в качестве параметра, поэтому добавьте указанную ниже строку в метод **Page_Load**. Вы создадите метод  `GetLocalEmployeeName` на одном из следующих этапов.</span><span class="sxs-lookup"><span data-stu-id="2210a-p120">The  `AddLocalEmployeeToCorpDB` method takes the employee's name as a parameter, so add the following line to the **Page_Load** method. You'll create the `GetLocalEmployeeName` method in a later step.</span></span>
    
```C#
  // Read from SharePoint 
string employeeName = GetLocalEmployeeName();
```

10. <span data-ttu-id="2210a-191">Под этой строкой добавьте вызов метода `AddLocalEmployeeToCorpDB`.</span><span class="sxs-lookup"><span data-stu-id="2210a-191">Below this line, add the call to the  `AddLocalEmployeeToCorpDB` method.</span></span>
    
```C#
  // Write to remote database 
AddLocalEmployeeToCorpDB(employeeName);
```

11. <span data-ttu-id="2210a-p121">Добавьте в файл оператор **using** для пространства имен `Microsoft.SharePoint.Client` (при создании проекта **ChainStoreWeb** Инструменты разработчика Office для Visual Studio включили в него сборку Microsoft.SharePoint.Client).</span><span class="sxs-lookup"><span data-stu-id="2210a-p121">Add a **using** statement to file for the namespace `Microsoft.SharePoint.Client`. (The Office Developer Tools for Visual Studio included the Microsoft.SharePoint.Client assembly in the **ChainStoreWeb** project when it was created.)</span></span>
    
 
12. <span data-ttu-id="2210a-p122">Теперь добавьте указанный ниже метод в класс  `EmployeeAdder`. Клиентская объектная модель (CSOM) .NET для SharePoint подробно задокументирована на MSDN и мы рекомендуем вам изучить ее, когда вы закончите работу с этой серией статей. Для целей данной статьи обратите внимание, что класс **ListItem** представляет элемент в списке SharePoint и что на значение поля в элементе можно сослаться с помощью синтаксиса "индексатора". Кроме того, учтите, что код ссылается на поле, используя имя Title (Название) даже если вы изменили его на Name (Имя). Это происходит из-за того, что в коде необходимо ссылаться на поля, используя их *внутренние*  , а не отображаемые имена. Внутреннее имя поля указывается при создании поля и его не удастся изменить. Вы выполните `TODO1` на одном из следующих этапов.</span><span class="sxs-lookup"><span data-stu-id="2210a-p122">Now add the following method to the  `EmployeeAdder` class. The SharePoint .NET Client-side Object Model (CSOM) is documented in detail elsewhere on MSDN and we encourage you to explore it when you are finished with this series of articles. For this article, note that the **ListItem** class represents an item in a SharePoint list and that the value of a field in the item can be referenced with "indexer" syntax. Notice also, that the code refers to the field as "Title" even though you changed the field name to "Name". This is because fields are always referred to in code by their *internal*  name, not their display name. The internal name of a field is set when the field is created and can never change. You complete the `TODO1` in a later step.</span></span>
    
```C#
  private string GetLocalEmployeeName()
{
    ListItem localEmployee;

    // TODO1: Initialize the localEmployee object by getting  
    // the item from SharePoint.
 
    return localEmployee["Title"].ToString();
}
```

13. <span data-ttu-id="2210a-p123">Чтобы наш код смог получить элемент списка из SharePoint, ему потребуется идентификатор этого элемента. Добавьте указанное ниже объявление в класс  `EmployeeAdder` сразу же после объявления для объекта `spContext`.</span><span class="sxs-lookup"><span data-stu-id="2210a-p123">Our code will need the list item's ID before it can retrieve it from SharePoint. Add the following declaration to the  `EmployeeAdder` class just below the declaration for the `spContext` object.</span></span>
    
```C#
  private int listItemID;
```

14. <span data-ttu-id="2210a-203">Теперь добавьте в класс `EmployeeAdder` приведенный ниже метод, чтобы получить идентификатор элемента из параметра запроса.</span><span class="sxs-lookup"><span data-stu-id="2210a-203">Now add the following method to the  `EmployeeAdder` class to get the list item's ID from the query parameter.</span></span>
    
```C#
  private int GetListItemIDFromQueryParameter()
{
    int result;
    Int32.TryParse(Request.QueryString["SPListItemId"], out result);
    return result;
}
```

15. <span data-ttu-id="2210a-204">Чтобы инициализировать переменную `listItemID`, добавьте приведенную ниже строку в метод **Page_Load** сразу после строки, инициализирующей переменную `spContext`.</span><span class="sxs-lookup"><span data-stu-id="2210a-204">To initialize the  `listItemID` variable, add the following line to the **Page_Load** method just below the line that initializes the `spContext` variable.</span></span>
    
```C#
  listItemID = GetListItemIDFromQueryParameter();
```

16. <span data-ttu-id="2210a-p124">В  `GetLocalEmployeeName` замените `TODO1` указанным ниже кодом. На данный момент относитесь к этому коду как к "черному ящику", потому что сейчас нас интересует то, как заставить работать настраиваемую кнопку. Мы более подробно рассмотрим этот код в следующей статье серии, которая будет целиком посвящена клиентской объектной модели SharePoint.</span><span class="sxs-lookup"><span data-stu-id="2210a-p124">In the  `GetLocalEmployeeName`, replace the  `TODO1` with the following code. For the time being, just treat this code as a black box while we concentrate on getting the custom button working. We'll learn more about this code in the next article in this series, which is all about the SharePoint client-side object model.</span></span>
    
```C#
  using (var clientContext = spContext.CreateUserClientContextForSPHost())
{
    List localEmployeesList = clientContext.Web.Lists.GetByTitle("Local Employees");
    localEmployee = localEmployeesList.GetItemById(listItemID);
    clientContext.Load(localEmployee);
    clientContext.ExecuteQuery();
}

```


    The whole method should now look like the following.
    


```C#
  private string GetLocalEmployeeName()
{
    ListItem localEmployee;

    using (var clientContext = spContext.CreateUserClientContextForSPHost())
    {
        List localEmployeesList = clientContext.Web.Lists.GetByTitle("Local Employees");
        selectedLocalEmployee = localEmployeesList.GetItemById(listItemID);
        clientContext.Load(selectedLocalEmployee);
        clientContext.ExecuteQuery();
    }
    return localEmployee["Title"].ToString();
}
```

17. <span data-ttu-id="2210a-p125">Страница EmployeeAdder не должна отрисовываться, поэтому добавьте приведенный ниже код в метод **Page_Load** в качестве последней строки. Она будет перенаправлять браузер обратно на страницу представления списка **Местные сотрудники**.</span><span class="sxs-lookup"><span data-stu-id="2210a-p125">The EmployeeAdder page should not actually render, so add the following as the last line in the **Page_Load** method. This will redirect the browser back to the list view page for the **Local Employees** list.</span></span>
    
```C#
  // Go back to the Local Employees page
Response.Redirect(spContext.SPHostUrl.ToString() + "Lists/LocalEmployees/AllItems.aspx", true);

```


    The whole  **Page_Load** method should now look like the following.
    


```C#
  protected void Page_Load(object sender, EventArgs e)
{
    spContext = Session["SPContext"] as SharePointContext;
    listItemID = GetListItemIDFromQueryParameter();

    // Read from SharePoint
    string employeeName = GetLocalEmployeeName();

    // Write to remote database
    AddLocalEmployeeToCorpDB(employeeName);

    // Go back to the preceding page
    Response.Redirect(spContext.SPHostUrl.ToString() + "Lists/LocalEmployees/AllItems.aspx", true);
}
```


## <a name="request-permission-to-read-the-host-web-list"></a><span data-ttu-id="2210a-210">Запрос разрешения на чтение списка на хост-сайте</span><span class="sxs-lookup"><span data-stu-id="2210a-210">Request permission to read the host web list</span></span>

<span data-ttu-id="2210a-p126">Как вы уже видели, при установке надстройки SharePoint предлагает предоставить ей разрешения на доступ к хост-сайту. Каждый раз, когда вы нажимали клавишу F5, выполнялась переустановка надстройки. До настоящего момента у надстройки были только минимально необходимые разрешения, но методу  `GetLocalEmployeeName` необходимо разрешение на чтение списков хост-сайта. Надстройка использует свой манифест, чтобы сообщить SharePoint, какие разрешения ей необходимы. Выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="2210a-p126">As you have seen, SharePoint prompts you to grant the add-in permissions to the host web when it is installed. You have been re-installing the add-in every time you press F5. So far, the add-in has only needed minimal permissions, but the  `GetLocalEmployeeName` method requires permission to read the lists of the host website. The add-in uses its add-in manifest to tell SharePoint what permissions it needs. Follow these steps.</span></span>
 

 

1. <span data-ttu-id="2210a-p127">В **обозревателе решений** откройте файл AppManifest.xml проекта **ChainStore** (файл называется AppManifest, потому что ранее надстройки назывались приложениями). Откроется конструктор манифестов.</span><span class="sxs-lookup"><span data-stu-id="2210a-p127">In **Solution Explorer**, open the AppManifest.xml file in the **ChainStore** project. (The file is called AppManifest because add-ins used to be called "apps".) The manifest designer opens.</span></span>
    
 
2. <span data-ttu-id="2210a-218">Откройте вкладку **Разрешения** и щелкните пустую ячейку под столбцом **Область**. Затем в раскрывающемся списке выберите **Список**.</span><span class="sxs-lookup"><span data-stu-id="2210a-218">Open the **Permissions** tab and click the empty cell under the **Scope** column; and then select **List** from the drop down.</span></span>
    
 
3. <span data-ttu-id="2210a-219">В поле **Разрешение** выберите из раскрывающегося списка пункт **Чтение**.</span><span class="sxs-lookup"><span data-stu-id="2210a-219">In the **Permission** field, select **Read** from the drop down.</span></span>
    
 
4. <span data-ttu-id="2210a-p128">Оставьте поле **Свойства** пустым и сохраните файл. Вкладка **Разрешение** должна выглядеть примерно так:</span><span class="sxs-lookup"><span data-stu-id="2210a-p128">Leave the **Properties** field empty and save the file. The **Permission** tab should look similar to the following:</span></span>
    
  ![Вкладка "Разрешения" конструктора манифеста надстройки, где в качестве области задан список и предоставлено разрешение на чтение.](../../images/8dd2a25f-103a-42af-aa88-c8ec796315db.PNG)
 

 

 

## <a name="run-the-add-in-and-test-the-button"></a><span data-ttu-id="2210a-223">Запуск надстройки и тестирование кнопки</span><span class="sxs-lookup"><span data-stu-id="2210a-223">Run the add-in and test the button</span></span>


 

 

1. <span data-ttu-id="2210a-p129">Нажмите клавишу F5, чтобы развернуть и запустить вашу надстройку. Visual Studio размещает удаленное веб-приложение в IIS Express, а базу данных SQL в SQL Express. Кроме того, он создает временную установку надстройки на вашем тестовом сайте SharePoint и сразу же запускает ее. Прежде чем откроется начальная страница надстройки, вам будет предложено предоставить надстройке необходимые разрешения. В этот раз будет предложен раскрывающийся список, в котором вы можете выбрать список, данные из которого необходимо считывать приложению, как показано на снимке экрана ниже.</span><span class="sxs-lookup"><span data-stu-id="2210a-p129">Use the F5 key to deploy and run your add-in. Visual Studio hosts the remote web application in IIS Express and hosts the SQL database in a SQL Express. It also makes a temporary installation of the add-in on your test SharePoint site and immediately runs the add-in. You are prompted to grant permissions to the add-in before it's start page opens. This time the prompt has a drop down where you select the list that the app needs to read as seen in the following screenshot.</span></span> 
    
  ![Приглашение разрешения надстройки SharePoint со списком "Местные сотрудники", выбранным в раскрывающемся списке "Чтение элементов в списке"](../../images/84e8b42c-4800-4947-acbd-21c6f096f4ea.PNG)
 

 

 
2. <span data-ttu-id="2210a-230">В списке выберите пункт **Местные сотрудники**, а затем нажмите кнопку **Доверять**.</span><span class="sxs-lookup"><span data-stu-id="2210a-230">Choose **Local Employees** from the list and then click **Trust it**.</span></span>
    
 
3. <span data-ttu-id="2210a-231">Когда откроется начальная страница, на расположенном в верхней части элементе управления хрома нажмите кнопку **Вернуться на сайт**.</span><span class="sxs-lookup"><span data-stu-id="2210a-231">When the add-in's start page opens, click **Back to Site** on the chrome control at the top.</span></span>
    
 
4. <span data-ttu-id="2210a-p130">На домашней странице веб-сайта выберите пункты **Содержимое сайта | Местные сотрудники**. Откроется страница представления списка.</span><span class="sxs-lookup"><span data-stu-id="2210a-p130">From the website's home page navigate to **Site Contents | Local Employees**. The list view page opens.</span></span>
    
 
5. <span data-ttu-id="2210a-p131">Добавьте нескольких сотрудников в список. *Не устанавливайте флажок **Добавлено в корпоративную базу данных**.*</span><span class="sxs-lookup"><span data-stu-id="2210a-p131">Add a few employees to the list.  *Do not check the **Added to Corporate DB** checkbox.*</span></span> 
    
 
6. <span data-ttu-id="2210a-p132">На ленте откройте вкладку **Элементы**. В разделе **Действия** вы увидите настраиваемую кнопку **Добавить в корпоративную базу данных**.</span><span class="sxs-lookup"><span data-stu-id="2210a-p132">On the ribbon, open the **Items** tab. In the **Actions** section of the tab, is the custom button **Add to Corporate DB**.</span></span>
    
 
7. <span data-ttu-id="2210a-p133">Выберите элемент в списке. Страница и лента должны выглядеть примерно так:</span><span class="sxs-lookup"><span data-stu-id="2210a-p133">Select an item on the list. The page and ribbon should look similar to the following:</span></span>
    
  ![Список местных сотрудников. Один элемент выделен. Над ним лента и кнопка с текстом "Добавить в базу данных предприятия" в разделе "Действия".](../../images/797a5ceb-7291-4b62-8075-2bb6a1b8e8a1.PNG)
 

 

 
8. <span data-ttu-id="2210a-p135">Нажмите кнопку **Добавить в корпоративную базу данных**. * **Перед этим необходимо выбрать элемент.***</span><span class="sxs-lookup"><span data-stu-id="2210a-p135">Press the **Add to Corporate DB** button. * **An item must be selected first!***</span></span> 
    
 
9. <span data-ttu-id="2210a-245">Вам покажется, что страница перезагружается, так как метод **Page_Load** страницы EmployeeAdder выполняет перенаправление на нее.</span><span class="sxs-lookup"><span data-stu-id="2210a-245">The page will seem to reload because the **Page_Load** method of the EmployeeAdder page redirects back to it.</span></span>
    
 
10. <span data-ttu-id="2210a-246">Дважды нажмите кнопку "Назад" в браузере, чтобы вернуться на начальную страницу надстройки.</span><span class="sxs-lookup"><span data-stu-id="2210a-246">Use the browser's back button twice to go back to the add-in's start page.</span></span> 
    
 
11. <span data-ttu-id="2210a-p136">Нажмите кнопку **Показать сотрудников**. Список сотрудников будет заполнен добавленными вами сотрудниками. Он должен выглядеть примерно так:</span><span class="sxs-lookup"><span data-stu-id="2210a-p136">Click **Show Employees** and the list of employees will be populated with the employee that you added. It should look similar to the following:</span></span>
    
  ![Список сотрудников организации на начальной странице надстройки, где отображается сотрудник, выбранный в предыдущем действии.](../../images/4a300a4e-f479-4f63-b536-6315c5d9ba4d.PNG)
 

 

 
12. <span data-ttu-id="2210a-p137">Чтобы завершить сеанс отладки, закройте окно браузера или остановите отладку в Visual Studio. При каждом нажатии клавиши F5 Visual Studio будет отзывать предыдущую версию надстройки и устанавливать ее последнюю версию.</span><span class="sxs-lookup"><span data-stu-id="2210a-p137">To end the debugging session, close the browser window or stop debugging in Visual Studio. Each time that you press F5, Visual Studio will retract the previous version of the add-in and install the latest one.</span></span>
    
 
13. <span data-ttu-id="2210a-p138">Эти надстройка и решение Visual Studio будут рассматриваться и в других статьях, поэтому при перерывах в работе рекомендуется отзывать надстройку. В **обозревателе решений** щелкните проект правой кнопкой мыши и выберите пункт **Отозвать**.</span><span class="sxs-lookup"><span data-stu-id="2210a-p138">You will work with this add-in and Visual Studio solution in other articles, and it's a good practice to retract the add-in one last time when you are done working with it for a while. Right-click the project in **Solution Explorer** and choose **Retract**.</span></span>
    
 

## 
<span data-ttu-id="2210a-254"><a name="Nextsteps"> </a></span><span class="sxs-lookup"><span data-stu-id="2210a-254"></span></span>

 <span data-ttu-id="2210a-255">В следующей статье мы немного отвлечемся от программирования и изучим клиентскую объектную модель SharePoint: [Краткий обзор объектной модели SharePoint](get-a-quick-overview-of-the-sharepoint-object-model).</span><span class="sxs-lookup"><span data-stu-id="2210a-255">In the next article, we'll take a brief break from coding for an overview of the SharePoint client-side object model: [Get a quick overview of the SharePoint object model](get-a-quick-overview-of-the-sharepoint-object-model).</span></span>
 

 

