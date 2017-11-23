# <a name="create-a-sharepoint-add-in-that-contains-a-document-template-and-a-task-pane-add-in"></a><span data-ttu-id="924fe-101">Создание надстройки SharePoint, содержащей шаблон документов и надстройку области задач</span><span class="sxs-lookup"><span data-stu-id="924fe-101">Create a SharePoint Add-in that contains a document template and a task pane add-in</span></span>
<span data-ttu-id="924fe-102">Разработка надстройки Office, которая отображается в документе, открытом из надстройки SharePoint, с помощью Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="924fe-102">Use Visual Studio to develop an Office Add-in that appears in a document that is opened from a SharePoint Add-in.</span></span>
 

 <span data-ttu-id="924fe-p101">**Примечание.** Название "приложения для SharePoint" меняется на "надстройки SharePoint". Пока изменения не будут внесены полностью, в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio по-прежнему может встречаться термин "приложение". Дополнительные сведения см. в разделе [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="924fe-p101">The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span></span>
 

<span data-ttu-id="924fe-p102">Вы можете создать надстройку SharePoint, которая включает в себя шаблон документа (например, авансовый отчет). Этот документ может содержать надстройку области задач, взаимодействующую с данными SharePoint. Например, пользователи могут заполнить поля счета, используя данные из Business Connectivity Services (BCS), или создать авансовый отчет, выбрав категорию расходов из списка SharePoint.</span><span class="sxs-lookup"><span data-stu-id="924fe-p102">You can create a SharePoint Add-in that includes a document template (for example, an expense report). The document can include a task pane add-in that interacts with SharePoint data. For example, users can populate fields of an invoice by using data from the Business Connectivity Services (BCS) or create an expense report by selecting an expense category from a SharePoint list.</span></span>
 

<span data-ttu-id="924fe-p103">В этом пошаговом руководстве показано, как создать надстройку SharePoint, которая включает в себя книгу Excel. Книга Excel содержит надстройку области задач, использующую интерфейс REST, предоставленный SharePoint, для заполнения поля раскрывающегося списка данными SharePoint.</span><span class="sxs-lookup"><span data-stu-id="924fe-p103">This walkthrough shows you how to create a SharePoint Add-in that includes an Excel workbook. The Excel workbook contains a task pane add-in that uses the REST interface provided by SharePoint to populate a drop-down list box with SharePoint date in the task pane add-in.</span></span>
 


## <a name="prerequisites"></a><span data-ttu-id="924fe-111">Необходимые компоненты</span><span class="sxs-lookup"><span data-stu-id="924fe-111">Prerequisites</span></span>
<span data-ttu-id="924fe-112"><a name="Prerequisites"> </a></span><span class="sxs-lookup"><span data-stu-id="924fe-112"></span></span>

<span data-ttu-id="924fe-113">Установите следующие компоненты перед началом работы:</span><span class="sxs-lookup"><span data-stu-id="924fe-113">Install the following components before you get started:</span></span>
 

 

 

 

- <span data-ttu-id="924fe-114">Среда разработки для SharePoint:</span><span class="sxs-lookup"><span data-stu-id="924fe-114">A SharePoint development environment:</span></span>
    
      - <span data-ttu-id="924fe-115">О разработке надстроек SharePoint для Office 365 см. в статье[ Настройка среды для разработки надстроек SharePoint в Office 365](http://msdn.microsoft.com/ru-ru/library/office/apps/fp161179%28v=office.15%29).</span><span class="sxs-lookup"><span data-stu-id="924fe-115">To develop SharePoint Add-ins that target SharePoint in Office 365, see  [How to: Set up an environment for developing SharePoint Add-ins on Office 365](http://msdn.microsoft.com/ru-ru/library/office/apps/fp161179%28v=office.15%29).</span></span>
    
 
  - <span data-ttu-id="924fe-116">Если вы собираетесь создавать надстройки SharePoint, предназначенные для локальной установки SharePoint, см. статью [Настройка локальной среды разработки надстроек SharePoint](http://msdn.microsoft.com/ru-ru/library/office/apps/fp179923%28v=office.15%29).</span><span class="sxs-lookup"><span data-stu-id="924fe-116">To develop SharePoint Add-ins that target an on-premises installation of SharePoint, see [How to: Set up an on-premises development environment for SharePoint Add-ins](http://msdn.microsoft.com/ru-ru/library/office/apps/fp179923%28v=office.15%29).</span></span>
    
 
-  [<span data-ttu-id="924fe-117">Visual Studio 2015 и Инструменты разработчика Microsoft Office</span><span class="sxs-lookup"><span data-stu-id="924fe-117">Visual Studio 2015 and the Microsoft Office Developer Tools</span></span>](https://www.visualstudio.com/features/office-tools-vs)
    
 
- <span data-ttu-id="924fe-118">Excel 2013 или учетная запись Office 365.</span><span class="sxs-lookup"><span data-stu-id="924fe-118">Excel 2013 or an Office 365 account.</span></span>
    
 

## <a name="create-a-sharepoint-add-in-project-in-visual-studio"></a><span data-ttu-id="924fe-119">Создание проекта надстройки SharePoint в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="924fe-119">Create a SharePoint Add-in project in Visual Studio</span></span>
<span data-ttu-id="924fe-120"><a name="Create"> </a></span><span class="sxs-lookup"><span data-stu-id="924fe-120"></span></span>


1. <span data-ttu-id="924fe-121">Запустите Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="924fe-121">Start Visual Studio.</span></span>
    
 
2. <span data-ttu-id="924fe-122">В строке меню выберите пункты **Файл**, **Создать** и **Проект**.</span><span class="sxs-lookup"><span data-stu-id="924fe-122">On the menu bar, choose  **File**,  **New**,  **Project**.</span></span>
    
    <span data-ttu-id="924fe-123">Откроется диалоговое окно **Создание проекта**.</span><span class="sxs-lookup"><span data-stu-id="924fe-123">The  **New Project** dialog box opens.</span></span>
    
 
3. <span data-ttu-id="924fe-124">Перейдите к области шаблонов и в узле необходимого языка разверните узел **Office/SharePoint**, затем выберите элемент **Office Add-ins** (Надстройки Office).</span><span class="sxs-lookup"><span data-stu-id="924fe-124">In the templates pane, under the node for the language you want to use, expand  **Office/SharePoint**, and then choose  **Office Add-ins**.</span></span>
    
 
4. <span data-ttu-id="924fe-125">В списке типов проектов выберите элемент **Надстройка SharePoint**, назовите проект OfficeEnabledAddin и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="924fe-125">In the list of project types, choose  **SharePoint Add-in**, name the project OfficeEnabledAddin, and then choose the  **OK** button.</span></span>
    
    <span data-ttu-id="924fe-126">Откроется диалоговое окно **Создание надстройки SharePoint**.</span><span class="sxs-lookup"><span data-stu-id="924fe-126">The  **New SharePoint Add-in** dialog box appears.</span></span>
    
 
5. <span data-ttu-id="924fe-127">В раскрывающемся списке **Какой сайт SharePoint использовать для отладки надстройки?** выберите или введите URL-адрес сайта SharePoint.</span><span class="sxs-lookup"><span data-stu-id="924fe-127">In the  **What SharePoint site do you want to use for debugging your add-in?** drop-down list, choose or enter the URL of a SharePoint site.</span></span>
    
 
6. <span data-ttu-id="924fe-128">В раскрывающемся списке **Как разместить надстройку SharePoint?** выберите **Размещено в SharePoint** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="924fe-128">In the  **How do you want to host your SharePoint Add-in?** drop-down list, choose **SharePoint-hosted** and then choose **Next**.</span></span>
    
     <span data-ttu-id="924fe-129">**Примечание**. Этот сценарий подходит только для вариантов размещения в SharePoint и у поставщика, указанных в раскрывающемся списке **Как требуется разместить надстройку SharePoint?**.</span><span class="sxs-lookup"><span data-stu-id="924fe-129">**Note**  This scenario works only with the SharePoint-hosted and provider-hosted options presented in the  **How do you want to host your SharePoint Add-in?** drop-down list.</span></span>
7. <span data-ttu-id="924fe-130">На следующей странице выберите **SharePoint**, а затем нажмите кнопку **Готово**, чтобы закрыть диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="924fe-130">On the next page, select **SharePoint** and then choose the **Finish** button to close the dialog box.</span></span>
    
 

## <a name="add-a-task-pane-add-in-item"></a><span data-ttu-id="924fe-131">Добавление надстройки области задач</span><span class="sxs-lookup"><span data-stu-id="924fe-131">Add a task pane add-in item</span></span>
<span data-ttu-id="924fe-132"><a name="Add"> </a></span><span class="sxs-lookup"><span data-stu-id="924fe-132"></span></span>

<span data-ttu-id="924fe-p104">Затем добавьте в проект надстройку Office. Вы можете добавить надстройку любого типа. В этом руководстве мы добавим надстройку области задач.</span><span class="sxs-lookup"><span data-stu-id="924fe-p104">Next, add an Office Add-in to the project. You can add any type of add-in that you want. For this walkthrough, we will add a task pane add-in.</span></span>
 

 

1. <span data-ttu-id="924fe-136">В **обозревателе решений** выберите узел проекта **OfficeEnabledAddin**.</span><span class="sxs-lookup"><span data-stu-id="924fe-136">In  **Solution Explorer**, choose the  **OfficeEnabledAddin** project node.</span></span>
    
 
2. <span data-ttu-id="924fe-137">В меню **Проект** выберите пункт **Добавить новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="924fe-137">On the  **Project** menu, choose **Add New Item**.</span></span>
    
 
3. <span data-ttu-id="924fe-138">В диалоговом окне **Добавление нового элемента** последовательно выберите элементы **Office/SharePoint** и **Надстройка Office**.</span><span class="sxs-lookup"><span data-stu-id="924fe-138">In the  **Add New Item** dialog box, select **Office/SharePoint** and then choose **Office Add-in**.</span></span>
    
 
4. <span data-ttu-id="924fe-139">Назовите надстройку области задач MyTaskPaneAddin и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="924fe-139">Name the task pane add-in MyTaskPaneAddin, and then choose the  **Add** button.</span></span>
    
    <span data-ttu-id="924fe-140">Откроется диалоговое окно **Создание надстройки для Office**.</span><span class="sxs-lookup"><span data-stu-id="924fe-140">The  **Create Add-in for Office** dialog box opens.</span></span>
    
 
5. <span data-ttu-id="924fe-p105">В диалоговом окне **Создание надстройки для Office** выберите **Область задач** и нажмите кнопку **Далее**. На следующей странице снимите флажки **Word** и **PowerPoint** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="924fe-p105">In the  **Create Add-in for Office** dialog box, select **Task pane** and then choose **Next**. On the next page, clear the  **Word** and **PowerPoint** check boxes, and then choose **Next**.</span></span>
    
 
6. <span data-ttu-id="924fe-143">На странице  **Добавить надстройку Office в новый или существующий документ?** выберите вариант **Создать документ и вставить надстройку** и нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="924fe-143">In the  **Would you like your Office Add-in to appear in a new document or in an existing document?** page, choose **Create a new document and insert my add-in**, and then choose  **Finish**.</span></span>
    
    <span data-ttu-id="924fe-p106">Visual Studio добавляет библиотеку документов и шаблон книги для библиотеки. Книга содержит надстройку области задач.</span><span class="sxs-lookup"><span data-stu-id="924fe-p106">Visual Studio adds a document library and a workbook template for the library. The workbook contains a task pane add-in.</span></span>
    
 

## <a name="add-a-document-library"></a><span data-ttu-id="924fe-146">Добавление библиотеки документов</span><span class="sxs-lookup"><span data-stu-id="924fe-146">Add a document library</span></span>
<span data-ttu-id="924fe-147"><a name="Library"> </a></span><span class="sxs-lookup"><span data-stu-id="924fe-147"></span></span>

<span data-ttu-id="924fe-148">В этом разделе описано, как добавить библиотеку документов и сделать книгу шаблоном по умолчанию для этой библиотеки.</span><span class="sxs-lookup"><span data-stu-id="924fe-148">In this procedure, you will add a document library and make the workbook the default template of the document library.</span></span>
 

 

1. <span data-ttu-id="924fe-149">В **обозревателе решений** выберите узел проекта **OfficeEnabledAddin**.</span><span class="sxs-lookup"><span data-stu-id="924fe-149">In  **Solution Explorer**, choose the  **OfficeEnabledAddin** project node.</span></span>
    
 
2. <span data-ttu-id="924fe-150">В меню **Проект** выберите пункт **Добавить новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="924fe-150">On the  **Project** menu, choose **Add New Item**.</span></span>
    
 
3. <span data-ttu-id="924fe-151">В диалоговом окне **Добавление нового элемента** последовательно выберите элементы **Office/SharePoint** и **Список**. Назовите список MyDocumentLibrary и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="924fe-151">In the  **Add New Item** dialog box, select **Office/SharePoint**, then choose  **List**, name the list MyDocumentLibrary, and then choose the  **Add** button.</span></span>
    
 
4. <span data-ttu-id="924fe-152">В **мастере настройки SharePoint** выберите параметр **Создать шаблон настраиваемого списка и отобразить его экземпляр в списке**.</span><span class="sxs-lookup"><span data-stu-id="924fe-152">In  **SharePoint Customization Wizard**, select the  **Create a customizable list template and list instance of it** option.</span></span>
    
 
5. <span data-ttu-id="924fe-153">В раскрывающемся списке под этим параметром выберите **Библиотека документов**, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="924fe-153">In the drop-down list beneath this option, select  **Document Library**, and then choose the  **Next** button.</span></span>
    
 
6. <span data-ttu-id="924fe-154">На странице **Выбор шаблона для библиотеки документов. Документы, создаваемые в библиотеке, будут основаны на этом шаблоне** выберите **Использовать следующий документ в качестве шаблона для библиотеки**, а затем нажмите кнопку **Обзор**.</span><span class="sxs-lookup"><span data-stu-id="924fe-154">In the  **Choose a template for this document library. Documents that users create in this library will be based on that template** page, choose **Use the following document as the template for this library**, and then choose the  **Browse** button.</span></span>
    
 
7. <span data-ttu-id="924fe-155">В диалоговом окне **Открыть** откройте папку **OfficeDocuments**, выберите файл **MyTaskPaneApp.xlsx**, нажмите кнопку **Открыть**, затем нажмите кнопку **Готово** и закройте конструктор списка.</span><span class="sxs-lookup"><span data-stu-id="924fe-155">In the  **Open** dialog box, open the **OfficeDocuments** folder, select the **MyTaskPaneApp.xlsx** file, choose the **Open** button, choose the **Finish** button, and then close the list designer.</span></span>
    
 
8. <span data-ttu-id="924fe-156">В **обозревателе решений** выберите узел проекта **OfficeEnabledAddin**.</span><span class="sxs-lookup"><span data-stu-id="924fe-156">In  **Solution Explorer**, choose the  **OfficeEnabledAddin** project node.</span></span>
    
 
9. <span data-ttu-id="924fe-157">В меню **Вид** выберите пункт **Окно свойств**.</span><span class="sxs-lookup"><span data-stu-id="924fe-157">On the  **View** menu, choose **Properties Window**.</span></span>
    
 
10. <span data-ttu-id="924fe-158">В **обозревателе решений** выберите файл **AppManifest.xml**.</span><span class="sxs-lookup"><span data-stu-id="924fe-158">In  **Solution Explorer**, choose the  **AppManifest.xml** file.</span></span>
    
 
11. <span data-ttu-id="924fe-159">Выберите **Вид**, **Конструктор**.</span><span class="sxs-lookup"><span data-stu-id="924fe-159">Choose  **View**,  **Designer**.</span></span>
    
 
12. <span data-ttu-id="924fe-p107">В конструкторе манифестов задайте для элемента **Начальная страница** значение ~appWebUrl/Lists/MyDocumentLibrary. Оно будет преобразовано в значение OfficeEnabledAddin/Lists/MyDocumentLibrary.</span><span class="sxs-lookup"><span data-stu-id="924fe-p107">In the manifest designer, set the value of the  **Start page** value to~appWebUrl/Lists/MyDocumentLibrary. This converts to a value of OfficeEnabledAddin/Lists/MyDocumentLibrary.</span></span>
    
     <span data-ttu-id="924fe-p108">**Примечание.** Этот URL-адрес относится к библиотеке документов. В начале любого URL-адреса в манифесте надстройки Office, указывающего на элементы веб-сайта надстройки, необходимо указывать токен ~appWebUrl. Дополнительные сведения о токенах URL-адреса в проекте надстройки SharePoint см. в статье [Токены и строки URL-адресов в надстройках SharePoint](url-strings-and-tokens-in-sharepoint-add-ins).</span><span class="sxs-lookup"><span data-stu-id="924fe-p108">**Note**  This URL refers to the document library. You must use the ~appWebUrl token at the beginning of any URL in your Office Add-in manifest that refers to items within the add-in web. For more information about URL tokens in a SharePoint Add-in project, see [URL strings and tokens in SharePoint Add-ins](url-strings-and-tokens-in-sharepoint-add-ins).</span></span>
13. <span data-ttu-id="924fe-165">Закройте конструктор манифестов, чтобы сохранить изменения.</span><span class="sxs-lookup"><span data-stu-id="924fe-165">Close the manifest designer to save the change.</span></span>
    
 

## <a name="consume-sharepoint-data-in-the-task-pane"></a><span data-ttu-id="924fe-166">Использование данных SharePoint в области задач</span><span class="sxs-lookup"><span data-stu-id="924fe-166">Consume SharePoint data in the task pane</span></span>
<span data-ttu-id="924fe-167"><a name="Consume"> </a></span><span class="sxs-lookup"><span data-stu-id="924fe-167"></span></span>

<span data-ttu-id="924fe-168">В этом разделе описано, как показать список пользователей сайта с помощью интерфейса REST, доступного в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="924fe-168">In this procedure, you'll show a list of site users by using the REST interface provided by SharePoint.</span></span>
 

 
<span data-ttu-id="924fe-p109">В этом примере отображаются только данные списка SharePoint, но вы можете использовать их в надстройке утверждения документа. Когда пользователь выбирает имя из этого списка, код устанавливает значение столбца "Рецензент" в списке отслеживания документа. Этому пользователю может быть отправлено уведомление о проверке. Кроме того, вы можете сохранить выбранное имя в параметрах документа. Тогда элементы управления в надстройке области задач будут отображаться, только если документ откроет пользователь, указанный в параметрах документа. Дополнительные сведения:</span><span class="sxs-lookup"><span data-stu-id="924fe-p109">In this example, the SharePoint list data is only displayed, but you might use this sort of data as part of a document approval add-in. When a user chooses a name from that list, your code sets the value of the reviewer column in a document tracking list. A workflow associated with that list could send a review notification to that user. Alternatively, you might save the selected name to the document settings. Then, when a user opens the document, you could show controls in the task pane add-in only if the current user and the user stored to the document settings are the same. See the following topics for more information:</span></span>
 

 

-  [<span data-ttu-id="924fe-175">Выполнение базовых операций с использованием конечных точек SharePoint REST</span><span class="sxs-lookup"><span data-stu-id="924fe-175">Complete basic operations using SharePoint REST endpoints</span></span>](complete-basic-operations-using-sharepoint-2013-rest-endpoints)
    
 
-  [<span data-ttu-id="924fe-176">Выполнение базовых операций с использованием кода библиотеки JavaScript в SharePoint</span><span class="sxs-lookup"><span data-stu-id="924fe-176">Complete basic operations using JavaScript library code in SharePoint</span></span>](complete-basic-operations-using-javascript-library-code-in-sharepoint-2013)
    
 
-  [<span data-ttu-id="924fe-177">Сохранение состояния и параметров надстройки</span><span class="sxs-lookup"><span data-stu-id="924fe-177">Persisting add-in state and settings</span></span>](http://msdn.microsoft.com/library/407df6e8-c237-4d6a-b357-3000fe3de9ff%28Office.15%29.aspx)
    
 

1. <span data-ttu-id="924fe-178">В **обозревателе решений** последовательно откройте папки **MyTaskPaneAddin** и **Home**, а затем выберите файл **Home.html**.</span><span class="sxs-lookup"><span data-stu-id="924fe-178">In  **Solution Explorer**, expand the  **MyTaskPaneAddin** folder, expand the **Home** folder, and then choose the **Home.html** file.</span></span>
    
    <span data-ttu-id="924fe-179">Файл Home.html откроется в редакторе кода.</span><span class="sxs-lookup"><span data-stu-id="924fe-179">The Home.html file opens in the code editor.</span></span>
    
 
2. <span data-ttu-id="924fe-180">Добавьте следующий HTML-код под кнопкой `get-data-from-selection`.</span><span class="sxs-lookup"><span data-stu-id="924fe-180">Add the following HTML beneath the  `get-data-from-selection` button.</span></span>
    
```HTML
  <p>Select Reviewer:</p> <select class="select" id="select-reviewer" name="D1"> </select>
```

3. <span data-ttu-id="924fe-181">Выберите файл **Home.js**, чтобы открыть его в редакторе кода.</span><span class="sxs-lookup"><span data-stu-id="924fe-181">Choose the  **Home.js** file to open the Home.js file in the code editor.</span></span>
    
 
4. <span data-ttu-id="924fe-182">В начало файла Home.js добавьте следующие объявления.</span><span class="sxs-lookup"><span data-stu-id="924fe-182">Add the following declarations to the top of the Home.js file.</span></span>
    
```
  var appWebURL; var web;
```

5. <span data-ttu-id="924fe-183">Замените функцию `Initialize` следующим кодом.</span><span class="sxs-lookup"><span data-stu-id="924fe-183">Replace the  `Initialize` function with the following code.</span></span>
    
    <span data-ttu-id="924fe-184">Этот код выполняет такие задачи:</span><span class="sxs-lookup"><span data-stu-id="924fe-184">This code performs the following tasks:</span></span>
    
      - <span data-ttu-id="924fe-p110">Загрузка файлов SP.Runtime.js и SP.js с помощью функции `getScript` в jQuery. После загрузки файлов программа получит доступ к объектной модели JavaScript для SharePoint.</span><span class="sxs-lookup"><span data-stu-id="924fe-p110">Loads the SP.Runtime.js and SP.js files by using the  `getScript` function in jQuery. After loading the files, your program has access to the JavaScript object model for SharePoint.</span></span>
    
 
  - <span data-ttu-id="924fe-187">Загрузка текущего объекта веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="924fe-187">Loads the current website object.</span></span>
    
 
  - <span data-ttu-id="924fe-p111">Вызов функции, получающей всех пользователей сайта. Код для этой функции будет добавлен на следующем этапе.</span><span class="sxs-lookup"><span data-stu-id="924fe-p111">Calls a function that gets all of the users of the site. You will add the code for that function in the next step.</span></span>
    
 



```JS
   // The initialize function must be run each time a new page is loaded 
   Office.initialize = function (reason) { $(document).ready(function () { app.initialize(); var scriptbase = "/_layouts/15/"; $.getScript(scriptbase + "SP.Runtime.js", function () { $.getScript(scriptbase + "SP.js", function () { getAppWeb(function () { getSPUsers(populateUsersDropDown); }); }); }); function getAppWeb(functionToExecuteOnReady) { var context = SP.ClientContext.get_current(); web = context.get_web(); context.load(web); context.executeQueryAsync(onSuccess, onFailure); function onSuccess() { appWebURL = web.get_url(); functionToExecuteOnReady(); } function onFailure(sender, args) { app.initialize(); app.showNotification("Failed to connect to SharePoint. Error: " + args.get_message()); } } $('#get-data-from-selection').click(getDataFromSelection); }); };
```

6. <span data-ttu-id="924fe-190">Добавьте следующий код в конец файла Home.js.</span><span class="sxs-lookup"><span data-stu-id="924fe-190">Add the following code to the bottom of the Home.js file.</span></span>
    
    <span data-ttu-id="924fe-p112">This code obtains a list of website users by using the REST interface provided by SharePoint. Then, this code populates a drop-down list with the name and ID of each user.</span><span class="sxs-lookup"><span data-stu-id="924fe-p112">This code obtains a list of website users by using the REST interface provided by SharePoint. Then, this code populates a drop-down list with the name and ID of each user.</span></span>
    


```JS
  function getSPUsers(functionToExecuteOnReady) { var url = appWebURL + "/../_api/web/siteUsers"; jQuery.ajax({ url: url, type: "GET", headers: { "ACCEPT": "application/json;odata=verbose" }, success: onSuccess, error: onFailure }); function onSuccess(data) { var results = data.d.results; functionToExecuteOnReady(results); } function onFailure(jaXHR, textStatus, errorThrown) { var error = textStatus + " " + errorThrown; app.showNotification(error); } } function populateUsersDropDown(results) { for (var i = 0; i < results.length; i++) { var IDTemp = results[i].Id; $('#select-reviewer').append("<option value='" + IDTemp + "'>" + results[i].Title + "</option>"); } }
```

7. <span data-ttu-id="924fe-193">В **обозревателе решений** откройте контекстное меню файла **AppManifest.xml** и выберите пункт **Конструктор представлений**.</span><span class="sxs-lookup"><span data-stu-id="924fe-193">In  **Solution Explorer**, open the shortcut menu for the  **AppManifest.xml** file, and then choose **View Designer**.</span></span>
    
 
8. <span data-ttu-id="924fe-194">В конструкторе перейдите на страницу **Разрешения**.</span><span class="sxs-lookup"><span data-stu-id="924fe-194">On the designer, choose the  **Permissions** page.</span></span>
    
 
9. <span data-ttu-id="924fe-195">В раскрывающемся списке в столбце **Область** выберите элемент **Интернет**.</span><span class="sxs-lookup"><span data-stu-id="924fe-195">From the drop-down list under the  **Scope** column, choose the **Web** item.</span></span>
    
 
10. <span data-ttu-id="924fe-196">В раскрывающемся списке в столбце **Разрешения** выберите элемент **Чтение**.</span><span class="sxs-lookup"><span data-stu-id="924fe-196">From the drop-down list under the  **Permission** column, choose the **Read** item.</span></span>
    
 

## <a name="debug-the-task-pane-add-in"></a><span data-ttu-id="924fe-197">Отладка надстройки области задач</span><span class="sxs-lookup"><span data-stu-id="924fe-197">Debug the task pane add-in</span></span>
<span data-ttu-id="924fe-198"><a name="debug"> </a></span><span class="sxs-lookup"><span data-stu-id="924fe-198"></span></span>

<span data-ttu-id="924fe-199">Чтобы отладить надстройку области задач, откройте документ или запустите надстройку SharePoint, а затем откройте документ из библиотеки документов.</span><span class="sxs-lookup"><span data-stu-id="924fe-199">You can debug your task pane add-in by starting the document or by starting the SharePoint Add-in, and then opening a document from the document library.</span></span>
 

 

### <a name="debugging-your-task-pane-add-in-by-starting-the-document"></a><span data-ttu-id="924fe-200">Отладка надстройки области задач с помощью открытия документа</span><span class="sxs-lookup"><span data-stu-id="924fe-200">Debugging your task pane add-in by starting the document</span></span>


 

 

 <span data-ttu-id="924fe-p113">**Примечание**. Так как эта процедура открывает Microsoft Excel, она работает только в том случае, если на компьютере установлен пакет Office. В противном случае возникает ошибка "Приложение, связанное с этим типом проекта, не установлено на компьютере".</span><span class="sxs-lookup"><span data-stu-id="924fe-p113">**Note**  Because this procedure opens Excel, it works only when Office is installed on the system. Otherwise, you get an error that the "application associated with this project type isn't installed on this computer."</span></span>
 


1. <span data-ttu-id="924fe-203">Откройте файл Home.js в редакторе кода, а затем задайте точку останова рядом с методом `getDataFromSelection`.</span><span class="sxs-lookup"><span data-stu-id="924fe-203">Open the Home.js file in the code editor, and then set a breakpoint next to the  `getDataFromSelection` method.</span></span>
    
 
2. <span data-ttu-id="924fe-204">В **обозревателе решений** выберите узел проекта **OfficeEnabledApp**.</span><span class="sxs-lookup"><span data-stu-id="924fe-204">In  **Solution Explorer**, choose the  **OfficeEnabledApp** project node.</span></span>
    
 
3. <span data-ttu-id="924fe-205">В меню **Вид** выберите пункт **Окно свойств**.</span><span class="sxs-lookup"><span data-stu-id="924fe-205">On the  **View** menu, choose **Properties Window**.</span></span>
    
 
4. <span data-ttu-id="924fe-p114">В окне свойств в раскрывающемся списке **Действие при запуске** выберите элемент **Настольный клиент Office**. При этом появится новое свойство, **Документ при запуске**.</span><span class="sxs-lookup"><span data-stu-id="924fe-p114">In the Properties windows, from the  **Start Action** drop-down list, choose the **Office Desktop Client** item. When you do this, a new property appears, **Start Document**.</span></span>
    
 
5. <span data-ttu-id="924fe-208">В раскрывающемся списке **Документ при запуске** выберите элемент **OfficeDocuments\TaskPaneApp.xlsx**.</span><span class="sxs-lookup"><span data-stu-id="924fe-208">From the  **Start Document** drop-down list, choose the **OfficeDocuments\TaskPaneApp.xlsx** item.</span></span>
    
 
6. <span data-ttu-id="924fe-209">В меню **Отладка** выберите команду **Начать отладку**.</span><span class="sxs-lookup"><span data-stu-id="924fe-209">On the  **Debug** menu, choose **Start Debugging**.</span></span>
    
    <span data-ttu-id="924fe-p115">Это приведет к тому, что при запуске надстройки области задач в ней отобразится книга. Откроется книга, и появится надстройка области задач.</span><span class="sxs-lookup"><span data-stu-id="924fe-p115">This setting makes the workbook in the task pane add-in appear when the add-in runs. The workbook opens and the task pane add-in appears.</span></span>
    
 
7. <span data-ttu-id="924fe-212">В надстройке области задач щелкните раскрывающийся список **Выбор рецензента**, чтобы просмотреть список пользователей SharePoint.</span><span class="sxs-lookup"><span data-stu-id="924fe-212">In the task pane add-in, choose the  **Select Reviewer** drop down list to view a list of SharePoint users.</span></span>
    
 
8. <span data-ttu-id="924fe-213">В книге Excel выберите любую ячейку.</span><span class="sxs-lookup"><span data-stu-id="924fe-213">In the Excel workbook, select any cell.</span></span>
    
 
9. <span data-ttu-id="924fe-214">В надстройке области задач нажмите кнопку **Получение данных из выделения**.</span><span class="sxs-lookup"><span data-stu-id="924fe-214">In the task pane add-in, choose the  **Get data from selection** button.</span></span>
    
    <span data-ttu-id="924fe-215">Выполнение остановится в месте точки останова, указанной для метода `getDataFromSelection`.</span><span class="sxs-lookup"><span data-stu-id="924fe-215">Execution stops at the breakpoint that you set next to the  `getDataFromSelection` method.</span></span>
    
 

### <a name="debugging-your-task-pane-add-in-by-starting-sharepoint"></a><span data-ttu-id="924fe-216">Отладка надстройки области задач путем запуска SharePoint</span><span class="sxs-lookup"><span data-stu-id="924fe-216">Debugging your task pane add-in by starting SharePoint</span></span>


 

 

 <span data-ttu-id="924fe-p116">**Примечание.** При выполнении инструкций из этого раздела открывается Excel Online, поэтому обязательно наличие учетной записи Office 365. См. статью [Настройка среды для разработки надстроек SharePoint в Office 365](http://msdn.microsoft.com/ru-ru/library/office/apps/fp161179%28v=office.15%29).</span><span class="sxs-lookup"><span data-stu-id="924fe-p116">**Note**  This procedure opens the Excel Online. It works only when you have an Office 365 account. See [How to: Set up an environment for developing SharePoint Add-ins on Office 365](http://msdn.microsoft.com/ru-ru/library/office/apps/fp161179%28v=office.15%29).</span></span>
 


1. <span data-ttu-id="924fe-220">Откройте файл Home.js в редакторе кода, а затем задайте точку останова рядом с методом `getDataFromSelection`.</span><span class="sxs-lookup"><span data-stu-id="924fe-220">Open the Home.js file in the code editor, and then set a breakpoint next to the  `getDataFromSelection` method.</span></span>
    
 
2. <span data-ttu-id="924fe-221">В **обозревателе решений** выберите узел проекта **OfficeEnabledApp**.</span><span class="sxs-lookup"><span data-stu-id="924fe-221">In  **Solution Explorer**, choose the  **OfficeEnabledApp** project node.</span></span>
    
 
3. <span data-ttu-id="924fe-222">В меню **Вид** выберите пункт **Окно свойств**.</span><span class="sxs-lookup"><span data-stu-id="924fe-222">On the  **View** menu, choose **Properties Window**.</span></span>
    
 
4. <span data-ttu-id="924fe-223">В окне свойств в раскрывающемся списке **Действие при запуске** выберите элемент **Internet Explorer**.</span><span class="sxs-lookup"><span data-stu-id="924fe-223">In the Properties windows, from the  **Start Action** drop-down list, choose the **Internet Explorer** item.</span></span>
    
 
5. <span data-ttu-id="924fe-224">В меню **Отладка** выберите команду **Начать отладку**.</span><span class="sxs-lookup"><span data-stu-id="924fe-224">On the  **Debug** menu, **Start Debugging**.</span></span>
    
    <span data-ttu-id="924fe-225">Visual Studio откроет SharePoint и отобразит библиотеку **MyDocumentLibrary**.</span><span class="sxs-lookup"><span data-stu-id="924fe-225">Visual Studio opens SharePoint and shows the  **MyDocumentLibrary** library.</span></span>
    
 
6. <span data-ttu-id="924fe-226">В SharePoint на вкладке **Файлы**, выберите команду **Создать документ**.</span><span class="sxs-lookup"><span data-stu-id="924fe-226">In SharePoint, on the  **Files** tab, choose **New Document**.</span></span> 
    
 
7. <span data-ttu-id="924fe-227">Перейдите к книге в проекте MyTaskPaneApp.xlsx.</span><span class="sxs-lookup"><span data-stu-id="924fe-227">Navigate to the workbook in your project, MyTaskPaneApp.xlsx.</span></span>
    
    <span data-ttu-id="924fe-228">Откроется книга, и появится надстройка области задач.</span><span class="sxs-lookup"><span data-stu-id="924fe-228">The workbook opens and the task pane add-in appears.</span></span>
    
 
8. <span data-ttu-id="924fe-p117">Проверьте, что в браузере включена отладка скриптов. Чтобы включить отладку в Internet Explorer, откройте диалоговое окно **Свойства обозревателя**, перейдите на вкладку **Дополнительно** и снимите флажки **Отключить отладку сценариев (Internet Explorer)** и **Отключить отладку сценариев (другие)**.</span><span class="sxs-lookup"><span data-stu-id="924fe-p117">Ensure that script debugging is enabled in your browser. In Internet Explorer, you can enable script debugging by opening the  **Internet Options** dialog box, choosing the **Advanced** tab, and then clearing the **Disable Script Debugging (Internet Explorer)** and **Disable Script Debugging (Other)** check boxes.</span></span>
    
 
9. <span data-ttu-id="924fe-231">В Visual Studio откройте меню **Отладка** и выберите команду **Присоединиться к процессу**.</span><span class="sxs-lookup"><span data-stu-id="924fe-231">In Visual Studio, on the  **Debug** menu, choose **Attach to Process**.</span></span>
    
 
10. <span data-ttu-id="924fe-232">В диалоговом окне **Присоединение к процессу** выберите все доступные процессы **iexplore.exe**, а затем нажмите кнопку **Присоединиться**.</span><span class="sxs-lookup"><span data-stu-id="924fe-232">In the  **Attach to Process** dialog box, choose all of the available **iexplore.exe** processes, and then choose the **Attach** button.</span></span>
    
 
11. <span data-ttu-id="924fe-233">В надстройке области задач щелкните раскрывающийся список **Выбор рецензента**, чтобы просмотреть список пользователей SharePoint.</span><span class="sxs-lookup"><span data-stu-id="924fe-233">In the task pane add-in, choose the  **Select Reviewer** drop-down list to view a list of SharePoint users.</span></span>
    
    <span data-ttu-id="924fe-234">Данные в списке извлекаются из SharePoint с помощью вызова REST.</span><span class="sxs-lookup"><span data-stu-id="924fe-234">The data in the list is retrieved from SharePoint by using a REST call.</span></span>
    
 
12. <span data-ttu-id="924fe-235">В книге Excel выберите любую ячейку.</span><span class="sxs-lookup"><span data-stu-id="924fe-235">In the Excel workbook, choose any cell.</span></span>
    
 
13. <span data-ttu-id="924fe-236">В надстройке области задач нажмите кнопку **Получение данных из выделения**.</span><span class="sxs-lookup"><span data-stu-id="924fe-236">In the task pane add-in, choose the  **Get data from selection** button.</span></span>
    
    <span data-ttu-id="924fe-237">Выполнение остановится в месте точки останова, указанной для метода `getDataFromSelection`.</span><span class="sxs-lookup"><span data-stu-id="924fe-237">Execution stops at the breakpoint that you set next to the  `getDataFromSelection` method.</span></span>
    
     <span data-ttu-id="924fe-238">**Примечание**. Если книга не содержит данных, вы можете добавить их, выбрав элементы **Изменить книгу**, **Изменить в Excel Online** на панели инструментов в книге.</span><span class="sxs-lookup"><span data-stu-id="924fe-238">**Note**  If the workbook doesn't contain any data, you can add some by choosing  **EDIT WORBOOK**,  **Edit in Excel Online** on the toolbar in the workbook.</span></span>

## <a name="package-and-publish-the-add-in"></a><span data-ttu-id="924fe-239">Упаковка и публикация надстройки</span><span class="sxs-lookup"><span data-stu-id="924fe-239">Package and publish the add-in</span></span>
<span data-ttu-id="924fe-240"><a name="Package"> </a></span><span class="sxs-lookup"><span data-stu-id="924fe-240"></span></span>

<span data-ttu-id="924fe-241">Когда надстройка будет готова к упаковке для публикации, откройте мастер **публикации надстроек Office и SharePoint**.</span><span class="sxs-lookup"><span data-stu-id="924fe-241">When you are ready to package your add-in for publishing, open the  **Publish Office and SharePoint Add-ins** wizard.</span></span>
 

 

- <span data-ttu-id="924fe-242">В  **обозревателе решений** откройте контекстное меню для проекта надстройки SharePoint и выберите элемент **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="924fe-242">In  **Solution Explorer**, open the shortcut menu for the SharePoint Add-in project, and then choose  **Publish**.</span></span>
    
    <span data-ttu-id="924fe-p118">Откроется **мастер публикации надстроек для Office и SharePoint**. Дополнительные сведения см. в статье [Публикация надстройки для SharePoint с помощью Visual Studio](publish-sharepoint-add-ins-by-using-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="924fe-p118">The  **Publish Office and SharePoint Add-ins** wizard appears. For more information, see [Publish SharePoint Add-ins by using Visual Studio](publish-sharepoint-add-ins-by-using-visual-studio).</span></span>
    
 

## <a name="additional-resources"></a><span data-ttu-id="924fe-245">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="924fe-245">Additional resources</span></span>
<span data-ttu-id="924fe-246"><a name="AdditionalResources"> </a></span><span class="sxs-lookup"><span data-stu-id="924fe-246"></span></span>


-  [<span data-ttu-id="924fe-247">Надстройки области задач и контентные надстройки для Office 2013</span><span class="sxs-lookup"><span data-stu-id="924fe-247">Task pane and content add-ins for Office 2013</span></span>](http://msdn.microsoft.com/library/baf73b23-4429-4b7f-bcb9-a99a9618ae38%28Office.15%29.aspx)
    
 
-  [<span data-ttu-id="924fe-248">Рекомендации по разработке надстроек для Office</span><span class="sxs-lookup"><span data-stu-id="924fe-248">Design guidelines for Office Add-ins</span></span>](http://msdn.microsoft.com/library/d5b2ab2e-dfc8-47c8-919c-e9c23358d70c%28Office.15%29.aspx)
    
 
-  [<span data-ttu-id="924fe-249">Жизненный цикл разработки надстроек Office</span><span class="sxs-lookup"><span data-stu-id="924fe-249">Office Add-ins development lifecycle</span></span>](http://msdn.microsoft.com/library/c35b4b2b-7869-4501-9f10-888c8e74c98c%28Office.15%29.aspx)
    
 
-  [<span data-ttu-id="924fe-250">Публикация надстройки Office</span><span class="sxs-lookup"><span data-stu-id="924fe-250">Publish your Office Add-in</span></span>](http://msdn.microsoft.com/library/7f3ae6a0-06e9-438c-8899-bd9f605e6d9e%28Office.15%29.aspx)
    
 
-  [<span data-ttu-id="924fe-251">Общие сведения об интерфейсе API JavaScript для Office</span><span class="sxs-lookup"><span data-stu-id="924fe-251">Understanding the JavaScript API for Office</span></span>](http://msdn.microsoft.com/library/01180dae-ca45-40c8-b3dd-fd2a85651c0c%28Office.15%29.aspx)
    
 
-  [<span data-ttu-id="924fe-252">XML-манифест надстроек для Office</span><span class="sxs-lookup"><span data-stu-id="924fe-252">Office Add-ins XML manifest</span></span>](http://msdn.microsoft.com/library/4139ff24-afac-472a-af7d-9d069587ac9b%28Office.15%29.aspx)
    
 
-  [<span data-ttu-id="924fe-253">Справка по API и схеме надстроек для Office</span><span class="sxs-lookup"><span data-stu-id="924fe-253">Office Add-ins API and schema references</span></span>](http://msdn.microsoft.com/library/afcc2908-1e1b-4297-b554-11e6eb404804%28Office.15%29.aspx)
    
 

