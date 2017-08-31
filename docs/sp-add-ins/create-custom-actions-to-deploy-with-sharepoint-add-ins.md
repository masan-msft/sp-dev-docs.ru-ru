# <a name="create-custom-actions-to-deploy-with-sharepoint-add-ins"></a><span data-ttu-id="acaed-101">Создание дополнительных действий для развертывания с надстройками SharePoint</span><span class="sxs-lookup"><span data-stu-id="acaed-101">Create custom actions to deploy with SharePoint Add-ins</span></span>
<span data-ttu-id="acaed-102">Узнайте, как создать дополнительное действие в SharePoint, которое разворачивается на хост-сайте во время развертывания надстройки SharePoint.</span><span class="sxs-lookup"><span data-stu-id="acaed-102">Learn how to create a custom action in SharePoint that deploys to the host web when you deploy an SharePoint Add-in.</span></span>
 

 <span data-ttu-id="acaed-p101">**Примечание.** Название "приложения для SharePoint" меняется на "надстройки SharePoint". В процессе перехода с одного названия на другое в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio по-прежнему может встречаться термин "приложения для SharePoint". Дополнительные сведения см. в статье [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="acaed-p101">The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span></span>
 

<span data-ttu-id="acaed-p102">Дополнительные действия позволяют взаимодействовать со списками и лентой на хост-сайте. Дополнительное действие разворачивается на хост-сайте, когда конечные пользователи устанавливают вашу надстройку. Дополнительные действия могут открывать удаленную веб-страницу и передавать информацию через строку запроса. Для надстроек доступны дополнительные действия ленты и элемента меню.</span><span class="sxs-lookup"><span data-stu-id="acaed-p102">When you are creating a SharePoint Add-in, custom actions let you interact with the lists and the ribbon in the host web. A custom action deploys to the host web when end users install your add-in. Custom actions can open a remote webpage and pass information through the query string. There are two types of custom actions available for add-ins: Ribbon and Edit Control Block.</span></span>
 

## <a name="prerequisites-for-using-the-examples-in-this-article"></a><span data-ttu-id="acaed-110">Необходимые условия для использования примеров в этой статье</span><span class="sxs-lookup"><span data-stu-id="acaed-110">Prerequisites for using the examples in this article</span></span>
<span data-ttu-id="acaed-111"><a name="SP15Createcustomactionsapps_Prereq"> </a></span><span class="sxs-lookup"><span data-stu-id="acaed-111"></span></span>

<span data-ttu-id="acaed-112">Вам необходима среда разработки, описанная в статье [Знакомство с созданием надстроек SharePoint с размещением у поставщика](get-started-creating-provider-hosted-sharepoint-add-ins).</span><span class="sxs-lookup"><span data-stu-id="acaed-112">You need a development environment as explained in  [Get started creating provider-hosted SharePoint Add-ins](get-started-creating-provider-hosted-sharepoint-add-ins).</span></span>
 

 

### <a name="core-concepts-to-help-you-understand-custom-actions"></a><span data-ttu-id="acaed-113">Основные понятия по дополнительным действиям</span><span class="sxs-lookup"><span data-stu-id="acaed-113">Core concepts to help you understand custom actions</span></span>

<span data-ttu-id="acaed-114">В таблице ниже перечислены полезные статьи, в которых описаны понятия и действия, связанные с настройкой дополнительных действий.</span><span class="sxs-lookup"><span data-stu-id="acaed-114">The following table lists useful articles that can help you understand the concepts and steps that are involved in a custom action scenario.</span></span>
 

 

<span data-ttu-id="acaed-115">**Таблица 1. Основные понятия по дополнительным действиям**</span><span class="sxs-lookup"><span data-stu-id="acaed-115">**Table 1. Core concepts for custom actions**</span></span>


|<span data-ttu-id="acaed-116">**Статья**</span><span class="sxs-lookup"><span data-stu-id="acaed-116">**Article**</span></span>|<span data-ttu-id="acaed-117">**Описание**</span><span class="sxs-lookup"><span data-stu-id="acaed-117">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="acaed-118">Надстройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="acaed-118">SharePoint Add-ins</span></span>](sharepoint-add-ins)|<span data-ttu-id="acaed-119">Сведения о новой модели надстроек в SharePoint, с помощью которой можно создавать надстройки — небольшие и удобные в использовании решения для пользователей.</span><span class="sxs-lookup"><span data-stu-id="acaed-119">Learn about the new add-in model in SharePoint that enables you to create add-ins, which are small, easy-to-use solutions for end users.</span></span>|
| [<span data-ttu-id="acaed-120">Проектирование пользовательского интерфейса надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="acaed-120">UX design for SharePoint Add-ins</span></span>](ux-design-for-sharepoint-add-ins)|<span data-ttu-id="acaed-121">Узнайте, как создать удобную надстройку SharePoint.</span><span class="sxs-lookup"><span data-stu-id="acaed-121">Learn about the user experience (UX) options that you have when you are building SharePoint Add-ins.</span></span>|
| [<span data-ttu-id="acaed-122">Хост-сайты, сайты надстроек и компоненты SharePoint в SharePoint</span><span class="sxs-lookup"><span data-stu-id="acaed-122">Host webs, add-in webs, and SharePoint components in SharePoint</span></span>](host-webs-add-in-webs-and-sharepoint-components-in-sharepoint-2013)|<span data-ttu-id="acaed-p103">Изучите различия между хост-сайтами и сайтами надстроек. Узнайте, какие компоненты SharePoint можно включать в надстройку для SharePoint, какие компоненты необходимо разворачивать на хост-сайте, а какие на сайте надстройки, и как выполнить развертывание сайта надстройки в изолированном домене.</span><span class="sxs-lookup"><span data-stu-id="acaed-p103">Learn about the difference between host webs and add-in webs. Find out which SharePoint components can be included in a SharePoint Add-in, which components are deployed to the host web, which components are deployed to the add-in web, and how the add-in web is deployed in an isolated domain.</span></span>|

## <a name="code-example-create-a-custom-action-in-the-host-web-document-libraries"></a><span data-ttu-id="acaed-125">Пример кода. Создание дополнительного действия в библиотеках документов хост-сайта</span><span class="sxs-lookup"><span data-stu-id="acaed-125">Code example: Create a custom action in the host web document libraries</span></span>
<span data-ttu-id="acaed-126"><a name="SP15Createcustomactionsapps_Codeexample"> </a></span><span class="sxs-lookup"><span data-stu-id="acaed-126"></span></span>

<span data-ttu-id="acaed-127">Чтобы создать дополнительное действие в библиотеках документов хост-сайта, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="acaed-127">Follow these steps to create a custom action in the host web document libraries:</span></span>
 

 

1. <span data-ttu-id="acaed-128">Создайте проект надстройки для SharePoint и удаленный веб-проект.</span><span class="sxs-lookup"><span data-stu-id="acaed-128">Create the SharePoint Add-in and remote web projects.</span></span>
    
 
2. <span data-ttu-id="acaed-129">Добавьте компонент дополнительного действия в проект надстройки для SharePoint.</span><span class="sxs-lookup"><span data-stu-id="acaed-129">Add a custom action feature to the SharePoint Add-in project.</span></span>
    
 
3. <span data-ttu-id="acaed-130">Добавьте веб-страницу надстройки в веб-проект.</span><span class="sxs-lookup"><span data-stu-id="acaed-130">Add an add-in webpage to the web project.</span></span>
    
 

### <a name="to-create-the-sharepoint-add-in-and-remote-web-projects"></a><span data-ttu-id="acaed-131">Создание надстройки SharePoint и удаленных веб-проектов</span><span class="sxs-lookup"><span data-stu-id="acaed-131">To create the SharePoint Add-in and remote web projects</span></span>


1. <span data-ttu-id="acaed-p104">Откройте Visual Studio от имени администратора. (Для этого щелкните правой кнопкой мыши значок Visual Studio в меню **Пуск** и выберите **Запуск от имени администратора**.)</span><span class="sxs-lookup"><span data-stu-id="acaed-p104">Open Visual Studio as administrator. (To do this, right-click the Visual Studio icon on the **Start** menu, and choose **Run as administrator**.)</span></span>
    
 
2. <span data-ttu-id="acaed-134">Создайте надстройку SharePoint с размещением у поставщика, как описано в статье [Знакомство с созданием надстроек SharePoint с размещением у поставщика](get-started-creating-provider-hosted-sharepoint-add-ins), и назовите ее itCustomActionsApp.</span><span class="sxs-lookup"><span data-stu-id="acaed-134">Create the provider-hosted SharePoint Add-in as explained in  [Get started creating provider-hosted SharePoint Add-ins](get-started-creating-provider-hosted-sharepoint-add-ins) and name itCustomActionsApp.</span></span> 
    
 

### <a name="to-add-an-add-in-webpage-for-the-custom-actions"></a><span data-ttu-id="acaed-135">Добавление веб-страницы надстройки для дополнительных действий</span><span class="sxs-lookup"><span data-stu-id="acaed-135">To add an add-in webpage for the custom actions</span></span>


1. <span data-ttu-id="acaed-p105">После создания решения Visual Studio щелкните правой кнопкой проект веб-приложения (не проект надстройки SharePoint) и добавьте новую веб-форму. Для этого выберите **Добавить** > **Новый элемент** > **Веб** > **Веб-форма**. Назовите форму CustomActionTarget.aspx.</span><span class="sxs-lookup"><span data-stu-id="acaed-p105">After the Visual Studio solution has been created, right-click the web application project (not the SharePoint Add-in project) and add a new Web Form by choosing **Add** > **New Item** > **Web** > **Web Form**. Name the form CustomActionTarget.aspx.</span></span>
    
 
2. <span data-ttu-id="acaed-p106">В файле CustomActionTarget.aspx замените весь элемент **html** и его дочерние элементы следующим кодом HTML. Оставьте всю разметку над элементом **html** без изменений. Код HTML содержит скрипт JavaScript, который выполняет следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="acaed-p106">In the CustomActionTarget.aspx file, replace the entire **html** element and it's children with the following HTML code. Leave all the markup above the **html** element as it is. The HTML code contains JavaScript that performs the following tasks:</span></span>
    
      - <span data-ttu-id="acaed-141">Предоставляет заполнитель для параметров строки запроса.</span><span class="sxs-lookup"><span data-stu-id="acaed-141">Provides a placeholder for the query string parameters.</span></span>
    
 
  - <span data-ttu-id="acaed-142">Извлекает параметры из строки запроса.</span><span class="sxs-lookup"><span data-stu-id="acaed-142">Extracts the parameters from the query string.</span></span>
    
 
  - <span data-ttu-id="acaed-143">Отображает параметры в заполнителе.</span><span class="sxs-lookup"><span data-stu-id="acaed-143">Renders the parameters in the placeholder.</span></span>
    
 

     <span data-ttu-id="acaed-p107">**Важно!** Маркеры ItemURL и ItemID передаются, только когда выбран элемент. В производственной надстройке SharePoint код должен обрабатывать ситуации, когда элемент не выбран. В этом примере код предупреждает пользователя о том, что элемент не выбран.</span><span class="sxs-lookup"><span data-stu-id="acaed-p107">**Important** The ItemURL and ItemID tokens only get passed when there is an item selected. In a production quality SharePoint Add-in, your code needs to handle situations where no item is selected. In this example the code alerts the user that no item has been selected.</span></span> 

```HTML
  <html xmlns="http://www.w3.org/1999/xhtml">
<head>
    <title>Custom action target</title>
</head>
<body>
    <h2>Query string parameters passed by the custom action:</h2>

    <!-- Placeholder for query string parameters -->
    <ul id="qsparams"/>

    <!-- Main JavaScript function, renders
         the query string parameters -->
    <script lang="javascript">
        var params = document.URL.split("?")[1].split("&amp;");
        var paramsHTML = "";
      
        // Extracts the parameters from the query string.
        // Parameters are URLencoded, decode for rendering
        // in page.
        for (var i = 0; i < params.length; i = i + 1) {
            params[i] = decodeURIComponent(params[i]);
            paramsHTML += "<li>" + params[i] + "</li>";
        }

         // Alert the user when no item has been selected.
         // (The SPListItemId is the 5th parameter.)
         if (params[5] === undefined) {
            paramsHTML += "<div> <h3> No item has been selected from the list.  Please select an item. </h3> </div> ";
         }

        // Render parameters in the placeholder.
        document.getElementById("qsparams").innerHTML =
            paramsHTML;
    </script>
</body>
</html>
```


### <a name="to-add-a-menu-item-custom-action-to-the-sharepoint-add-in-project"></a><span data-ttu-id="acaed-147">Добавление дополнительного действия элемента меню в проект надстройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="acaed-147">To add a menu item custom action to the SharePoint Add-in project</span></span>


1. <span data-ttu-id="acaed-148">Щелкните правой кнопкой мыши проект надстройки SharePoint и выберите **Добавить** > **Новый элемент** > **Office/SharePoint** > **Настраиваемое действие элемента меню**.</span><span class="sxs-lookup"><span data-stu-id="acaed-148">Right-click the SharePoint Add-in project, and choose **Add** > **New Item** > **Office/SharePoint** > **Menu Item Custom Action**.</span></span> 
    
 
2. <span data-ttu-id="acaed-149">Оставьте имя по умолчанию и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="acaed-149">Keep the default name and choose **Add**.</span></span>
    
 
3. <span data-ttu-id="acaed-p108">Мастер **Создание настраиваемого действия для пункта меню** задаст вам несколько вопросов. Ответьте на них, используя следующую таблицу:</span><span class="sxs-lookup"><span data-stu-id="acaed-p108">The **Create Custom Action for Menu Item** wizard asks you a series of questions. Give the answers from the following table:</span></span>
    
    <span data-ttu-id="acaed-152">**Таблица 2. Свойства дополнительного действия элемента меню**</span><span class="sxs-lookup"><span data-stu-id="acaed-152">**Table 2. Menu Item custom action properties**</span></span>


|<span data-ttu-id="acaed-153">**Вопрос о свойстве**</span><span class="sxs-lookup"><span data-stu-id="acaed-153">**Property question**</span></span>|<span data-ttu-id="acaed-154">**Ответ**</span><span class="sxs-lookup"><span data-stu-id="acaed-154">**Answer**</span></span>|
|:-----|:-----|
|<span data-ttu-id="acaed-155">Где вы хотите разместить дополнительное действие?</span><span class="sxs-lookup"><span data-stu-id="acaed-155">Where do you want to expose the custom action?</span></span>|<span data-ttu-id="acaed-156">Выберите вариант **хост-сайт**.</span><span class="sxs-lookup"><span data-stu-id="acaed-156">Choose **Host Web**.</span></span>|
|<span data-ttu-id="acaed-157">К какой области относится дополнительное действие?</span><span class="sxs-lookup"><span data-stu-id="acaed-157">Where is the custom action scoped to?</span></span>|<span data-ttu-id="acaed-158">Выберите **Шаблон списка**.</span><span class="sxs-lookup"><span data-stu-id="acaed-158">Choose **List Template**.</span></span>|
|<span data-ttu-id="acaed-159">К какому элементу относится дополнительное действие?</span><span class="sxs-lookup"><span data-stu-id="acaed-159">Which particular item is the custom action scoped to?</span></span>|<span data-ttu-id="acaed-160">Выберите **Библиотека документов**.</span><span class="sxs-lookup"><span data-stu-id="acaed-160">Choose **Document Library**.</span></span>|
|<span data-ttu-id="acaed-161">Какой текст будет указан в элементе меню?</span><span class="sxs-lookup"><span data-stu-id="acaed-161">What is the text on the menu item?</span></span>|<span data-ttu-id="acaed-162">Введите **Мое дополнительное действие**.</span><span class="sxs-lookup"><span data-stu-id="acaed-162">Type **My Custom Action**.</span></span>|
|<span data-ttu-id="acaed-163">Куда будет вести дополнительное действие?</span><span class="sxs-lookup"><span data-stu-id="acaed-163">Where does the custom action navigate to?</span></span>|<span data-ttu-id="acaed-164">Выберите страницу **CustomActionAppWeb\CustomActionTarget.aspx**.</span><span class="sxs-lookup"><span data-stu-id="acaed-164">Choose the CustomActionAppWeb**CustomActionTarget.aspx** page.</span></span>|
4. <span data-ttu-id="acaed-165">Нажмите **Готово**.</span><span class="sxs-lookup"><span data-stu-id="acaed-165">Choose **Finish**.</span></span>
    
    <span data-ttu-id="acaed-166">Visual Studio создает следующую разметку в файле elements.xml функции дополнительного действия элемента меню:</span><span class="sxs-lookup"><span data-stu-id="acaed-166">Visual Studio generates the following markup in the elements.xml file of the menu item custom action feature:</span></span>
    


```XML
  <?xml version="1.0" encoding="utf-8"?>
<Elements 
    xmlns="http://schemas.microsoft.com/sharepoint/">
    <!-- RegistrationId attribute is the list type id,
        in this case, a document library (id=101). -->
  <CustomAction 
      Id="65695319-4784-478e-8dcd-4e541cb1d682.CustomAction"
      RegistrationType="List"
      RegistrationId="101"
      Location="EditControlBlock"
      Sequence="10001"
      Title="Invoke custom action">
    <!-- 
    Update the Url below to the page you want the custom action to use.
    Start the URL with the token ~remoteAppUrl if the page is in the
    associated web project, use ~appWebUrl if page is in the add-in project.
    -->
    <UrlAction Url=
"~remoteAppUrl/CustomActionTarget.aspx?{StandardTokens}&amp;amp;SPListItemId={ItemId}&amp;amp;SPListId={ListId}" />
  </CustomAction>
</Elements>

```

5. <span data-ttu-id="acaed-167">Добавьте следующие параметры запроса в конец атрибута **Url** элемента **UrlAction**:</span><span class="sxs-lookup"><span data-stu-id="acaed-167">Add the following query parameters to the end of the **Url** attribute of the **UrlAction** element:</span></span>
    
     `&amp;amp;SPSource={Source}&amp;amp;SPListURLDir={ListUrlDir}&amp;amp;SPItemURL={ItemUrl}`
    
    <span data-ttu-id="acaed-168">Элемент **UrlAction** должен выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="acaed-168">The **UrlAction** element should look like the following:</span></span>
    
     ` <UrlAction Url= "~remoteAppUrl/CustomActionTarget.aspx?{StandardTokens}&amp;amp;SPListItemId={ItemId}&amp;amp;SPListId={ListId}&amp;amp;SPSource={Source}&amp;amp;SPListURLDir={ListUrlDir}&amp;amp;SPItemURL={ItemUrl}" />`
    
 

 <span data-ttu-id="acaed-p109">**Примечание.** В этом примере удаленная веб-страница открывается в полном окне, когда пользователь выбирает дополнительное действие в меню. Удаленную веб-страницу также можно открывать в диалоговом окне с помощью атрибута **HostWebDialog**. Дополнительные сведения см. в репозитории [SharePoint-Add-in-Localization](https://github.com/OfficeDev/SharePoint-Add-in-Localization).</span><span class="sxs-lookup"><span data-stu-id="acaed-p109">**Note** In this example, the remote web page opens in a full window when the user selects the custom action from the menu. Custom menu actions can also open a remote webpage in a dialog box by using the **HostWebDialog** attribute. For more information, see [SharePoint-Add-in-Localization](https://github.com/OfficeDev/SharePoint-Add-in-Localization).</span></span>
 


### <a name="to-add-a-ribbon-custom-action-to-the-sharepoint-add-in-project"></a><span data-ttu-id="acaed-172">Добавление дополнительного действия ленты в проект надстройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="acaed-172">To add a Ribbon custom action to the SharePoint Add-in project</span></span>


1. <span data-ttu-id="acaed-173">Щелкните правой кнопкой мыши проект надстройки SharePoint и выберите **Добавить** > **Новый элемент** > **Office/SharePoint** > **Настраиваемое действие ленты**.</span><span class="sxs-lookup"><span data-stu-id="acaed-173">Right-click the SharePoint Add-in project, and choose **Add** > **New Item** > **Office/SharePoint** > **Ribbon Custom Action**.</span></span> 
    
 
2. <span data-ttu-id="acaed-174">Оставьте имя по умолчанию и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="acaed-174">Keep the default name and choose **Add**.</span></span>
    
 
3. <span data-ttu-id="acaed-p110">Мастер **Создание настраиваемого действия для ленты** задаст вам несколько вопросов. Ответьте на них, используя следующую таблицу:</span><span class="sxs-lookup"><span data-stu-id="acaed-p110">The **Create Custom Action for Ribbon** wizard asks you a series of questions. Give the answers from the following table:</span></span>
    
    <span data-ttu-id="acaed-177">**Таблица 3. Свойства дополнительного действия ленты**</span><span class="sxs-lookup"><span data-stu-id="acaed-177">**Table 3. Ribbon custom action properties**</span></span>


|<span data-ttu-id="acaed-178">**Вопрос о свойстве**</span><span class="sxs-lookup"><span data-stu-id="acaed-178">**Property question**</span></span>|<span data-ttu-id="acaed-179">**Ответ**</span><span class="sxs-lookup"><span data-stu-id="acaed-179">**Answer**</span></span>|
|:-----|:-----|
|<span data-ttu-id="acaed-180">Где вы хотите разместить дополнительное действие?</span><span class="sxs-lookup"><span data-stu-id="acaed-180">Where do you want to expose the custom action?</span></span>|<span data-ttu-id="acaed-181">Выберите вариант **хост-сайт**.</span><span class="sxs-lookup"><span data-stu-id="acaed-181">Choose **Host Web**.</span></span>|
|<span data-ttu-id="acaed-182">К какой области относится дополнительное действие?</span><span class="sxs-lookup"><span data-stu-id="acaed-182">Where is the custom action scoped to?</span></span>|<span data-ttu-id="acaed-183">Выберите **Шаблон списка**.</span><span class="sxs-lookup"><span data-stu-id="acaed-183">Choose **List Template**.</span></span>|
|<span data-ttu-id="acaed-184">К какому элементу относится дополнительное действие?</span><span class="sxs-lookup"><span data-stu-id="acaed-184">Which particular item is the custom action scoped to?</span></span>|<span data-ttu-id="acaed-185">Выберите **Библиотека документов**.</span><span class="sxs-lookup"><span data-stu-id="acaed-185">Choose **Document Library**.</span></span>|
|<span data-ttu-id="acaed-186">Где находится элемент управления?</span><span class="sxs-lookup"><span data-stu-id="acaed-186">Where is the control located?</span></span>|<span data-ttu-id="acaed-187">Выберите **Ribbon.Documents.Manage**.</span><span class="sxs-lookup"><span data-stu-id="acaed-187">Choose **Ribbon.Documents.Manage**.</span></span>|
|<span data-ttu-id="acaed-188">Какой текст будет указан в элементе меню?</span><span class="sxs-lookup"><span data-stu-id="acaed-188">What is the text on the menu item?</span></span>|<span data-ttu-id="acaed-189">Введите **Моя дополнительная кнопка ленты**.</span><span class="sxs-lookup"><span data-stu-id="acaed-189">Type **My Custom Ribbon Button**.</span></span>|
|<span data-ttu-id="acaed-190">Куда будет вести дополнительное действие?</span><span class="sxs-lookup"><span data-stu-id="acaed-190">Where does the custom action navigate to?</span></span>|<span data-ttu-id="acaed-191">Выберите страницу **CustomActionAppWeb\CustomActionTarget.aspx**.</span><span class="sxs-lookup"><span data-stu-id="acaed-191">Choose the CustomActionAppWeb**CustomActionTarget.aspx** page.</span></span>|
4. <span data-ttu-id="acaed-192">Visual Studio создает следующую разметку в файле elements.xml функции дополнительного действия ленты:</span><span class="sxs-lookup"><span data-stu-id="acaed-192">Visual Studio generates the following markup in the elements.xml file of the Ribbon custom action feature:</span></span>
    
```XML
  <?xml version="1.0" encoding="utf-8"?>
<Elements xmlns="http://schemas.microsoft.com/sharepoint/">
  <CustomAction Id="85691508-c076-4f43-93d4-96b4d5253a09.RibbonCustomAction1"
                RegistrationType="List"
                RegistrationId="101"
                Location="CommandUI.Ribbon"
                Sequence="10001"
                Title="Invoke &amp;apos;RibbonCustomAction1&amp;apos; action">
    <CommandUIExtension>
      <!-- 
      Update the UI definitions below with the controls and the command actions
      that you want to enable for the custom action.
      -->
      <CommandUIDefinitions>
        <CommandUIDefinition Location="Ribbon.Documents.Manage.Controls._children">
          <Button Id="Ribbon.Documents.Manage.RibbonCustomAction1Button"
                  Alt="My Custom Ribbon Button"
                  Sequence="100"
                  Command="Invoke_RibbonCustomAction1ButtonRequest"
                  LabelText="My Custom Ribbon Button"
                  TemplateAlias="o1"
                  Image32by32="_layouts/15/images/placeholder32x32.png"
                  Image16by16="_layouts/15/images/placeholder16x16.png" />
        </CommandUIDefinition>
      </CommandUIDefinitions>
      <CommandUIHandlers>
        <CommandUIHandler Command="Invoke_RibbonCustomAction1ButtonRequest"
                          CommandAction="~remoteAppUrl/CustomActionTarget.aspx?{StandardTokens}&amp;amp;SPListItemId={SelectedItemId}&amp;amp;SPListId={SelectedListId}"/>
      </CommandUIHandlers>
    </CommandUIExtension >
  </CustomAction>
</Elements> 

```

5. <span data-ttu-id="acaed-193">Добавьте следующие параметры запроса в конец атрибута **CommandAction** элемента **CommandUIHandler**:</span><span class="sxs-lookup"><span data-stu-id="acaed-193">Add the following query parameters to the end of the **CommandAction** attribute of the **CommandUIHandler** element:</span></span>
    
     `&amp;amp;SPSource={Source}&amp;amp;SPListURLDir={ListUrlDir}`
    
    <span data-ttu-id="acaed-194">Элемент **CommandUIHandler** должен выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="acaed-194">The **CommandUIHandler** element should look like the following:</span></span>
    
     ` <CommandUIHandler Command="Invoke_RibbonCustomAction1ButtonRequest" CommandAction="~remoteAppUrl/CustomActionTarget.aspx?{StandardTokens}&amp;amp;SPListItemId={SelectedItemId}&amp;amp;SPListId={SelectedListId}&amp;amp;SPSource={Source}&amp;amp;SPListURLDir={ListUrlDir}" />`
    
     <span data-ttu-id="acaed-p111">**Примечание.** Дополнительные действия ленты используют **SelectedListId** и **SelectedItemId**. **ListId** и **ItemId** работают только с дополнительными действиями элементов меню.</span><span class="sxs-lookup"><span data-stu-id="acaed-p111">**Note** Ribbon custom actions use **SelectedListId** and **SelectedItemId**. **ListId** and **ItemId** work only with menu item custom actions.</span></span>

### <a name="set-the-add-in-start-page-to-the-host-web-home-page"></a><span data-ttu-id="acaed-197">Установка домашней страницы хост-сайта в качестве начальной страницы надстройки</span><span class="sxs-lookup"><span data-stu-id="acaed-197">Set the add-in start page to the host web home page</span></span>


1. <span data-ttu-id="acaed-p112">В примере ниже у надстройки для SharePoint нет сайта надстройки, а ее удаленное веб-приложение существует только для размещения формы. Поэтому начальной страницей надстройки следует сделать домашнюю страницу хост-сайта.</span><span class="sxs-lookup"><span data-stu-id="acaed-p112">The continuing sample SharePoint Add-in doesn't have any add-in web and its remote web application exists only to host the form. So the start page of the add-in should be set to the home page of the host web.</span></span> 
    
    <span data-ttu-id="acaed-200">Для начала выберите проект надстройки SharePoint (не проект веб-приложения) в **обозревателе решений** и скопируйте значение свойства **URL-адрес сайта**, включая протокол (например, **https://contoso.sharepoint.com**) в буфер обмена.</span><span class="sxs-lookup"><span data-stu-id="acaed-200">To begin, select the SharePoint Add-in project (not the web application project) in **Solution Explorer** and copy the value of the **Site URL** property, including the protocol (for example **https://contoso.sharepoint.com**) into the clipboard.</span></span> 
    
 
2. <span data-ttu-id="acaed-201">Откройте манифест надстройки и вставьте URL-адрес в поле **Начальная страница**.</span><span class="sxs-lookup"><span data-stu-id="acaed-201">Open the add-in manifest, and then paste the URL into the **Start Page** box.</span></span>
    
 
3. <span data-ttu-id="acaed-202">При необходимости можно удалить страницу Default.aspx из проекта веб-приложения, так как она не используется в надстройке SharePoint.</span><span class="sxs-lookup"><span data-stu-id="acaed-202">Optionally, you can delete the Default.aspx page from the web application project, because it is not used in the SharePoint Add-in.</span></span>
    
 

### <a name="to-build-and-run-the-solution"></a><span data-ttu-id="acaed-203">Для создания и запуска решения</span><span class="sxs-lookup"><span data-stu-id="acaed-203">To build and run the solution</span></span>


1. <span data-ttu-id="acaed-204">Нажмите клавишу F5.</span><span class="sxs-lookup"><span data-stu-id="acaed-204">Press the F5 key.</span></span>
    
     <span data-ttu-id="acaed-205">**Примечание.** После нажатия клавиши F5 Visual Studio выполняет сборку решения, развертывает надстройку и открывает для нее страницу разрешений.</span><span class="sxs-lookup"><span data-stu-id="acaed-205">**Note** When you press F5, Visual Studio builds the solution, deploys the add-in, and opens the permissions page for the add-in.</span></span>
2. <span data-ttu-id="acaed-p113">Нажмите кнопку **Доверять**. Откроется страница сайта разработчика по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="acaed-p113">Choose the **Trust It** button. The default page of your developer site opens.</span></span>
    
 
3. <span data-ttu-id="acaed-208">Перейдите в любую библиотеку документов на хост-сайте.</span><span class="sxs-lookup"><span data-stu-id="acaed-208">Navigate to any document library in the host web.</span></span>
    
    <span data-ttu-id="acaed-209">**Запуск дополнительного действия меню**</span><span class="sxs-lookup"><span data-stu-id="acaed-209">**Launching a custom menu action**</span></span>

 

  ![Библиотека документов с открытой выноской для документа, меню, которое открывает кнопка выноски, и открытое меню "Дополнительно".](../../images/477cecf5-03ff-46ff-9c25-a5f9a86d43f4.png)
 

 

 
4. <span data-ttu-id="acaed-p114">Нажмите кнопку выноски (**...**) для любого документа. Откроется выноска.</span><span class="sxs-lookup"><span data-stu-id="acaed-p114">Choose the callout button ( **...**) for any document. The callout opens.</span></span>
    
 
5. <span data-ttu-id="acaed-213">Нажмите кнопку выноски (**...**) на выноске.</span><span class="sxs-lookup"><span data-stu-id="acaed-213">Choose the callout button ( **...**) on the callout.</span></span> 
    
 
6. <span data-ttu-id="acaed-214">Выберите **Дополнительно**.</span><span class="sxs-lookup"><span data-stu-id="acaed-214">Choose **Advanced**.</span></span>
    
 
7. <span data-ttu-id="acaed-p115">Выберите **Мое дополнительное действие меню** в контекстном меню. На открывшейся удаленной веб-странице вы увидите следующее:</span><span class="sxs-lookup"><span data-stu-id="acaed-p115">Choose **My Custom Menu Action** in the context menu. You should see something like the following on the remote webpage that opens:</span></span>
    
    <span data-ttu-id="acaed-217">**Удаленная веб-страница с параметрами из дополнительного действия**</span><span class="sxs-lookup"><span data-stu-id="acaed-217">**Remote webpage with parameters from the custom action**</span></span>

 

  ![Веб-страница с параметрами из дополнительного действия](../../images/CustomActions_target.png)
 

 

 
8. <span data-ttu-id="acaed-219">Нажмите кнопку **Назад** в браузере, чтобы вернуться в библиотеку.</span><span class="sxs-lookup"><span data-stu-id="acaed-219">Click the **Back** button on your browser to return to the library.</span></span>
    
    <span data-ttu-id="acaed-220">**Запуск дополнительного действия ленты**</span><span class="sxs-lookup"><span data-stu-id="acaed-220">**Launching a custom ribbon action**</span></span>

 

  ![Библиотека документов с выбранным документом, открытой вкладкой "Файл" и дополнительной кнопкой на ленте.](../../images/b315cb68-ff6a-4770-a1dc-738696ab71d2.png)
 

 

 
9. <span data-ttu-id="acaed-222">Выберите любой документ.</span><span class="sxs-lookup"><span data-stu-id="acaed-222">Select any document.</span></span>
    
 
10. <span data-ttu-id="acaed-223">Откройте вкладку **Файл** на ленте.</span><span class="sxs-lookup"><span data-stu-id="acaed-223">Open the **File** tab on the ribbon.</span></span>
    
 
11. <span data-ttu-id="acaed-p116">Выберите **Моя дополнительная кнопка ленты**. Отобразится та же удаленная веб-страница.</span><span class="sxs-lookup"><span data-stu-id="acaed-p116">Choose **My Custom Ribbon Button**. You see the same remote web page.</span></span>
    
 

<span data-ttu-id="acaed-226">**Таблица 4. Поиск и устранение неполадок в решении**</span><span class="sxs-lookup"><span data-stu-id="acaed-226">**Table 4. Troubleshooting the solution**</span></span>


|<span data-ttu-id="acaed-227">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="acaed-227">**Problem**</span></span>|<span data-ttu-id="acaed-228">**Решение**</span><span class="sxs-lookup"><span data-stu-id="acaed-228">**Solution**</span></span>|
|:-----|:-----|
|<span data-ttu-id="acaed-229">Visual Studio не открывает браузер после нажатия клавиши F5.</span><span class="sxs-lookup"><span data-stu-id="acaed-229">Visual Studio does not open the browser after you press the F5 key.</span></span>|<span data-ttu-id="acaed-230">Установите проект надстройки для SharePoint в качестве запускаемого проекта.</span><span class="sxs-lookup"><span data-stu-id="acaed-230">Set the SharePoint Add-in project as the startup project.</span></span>|
|<span data-ttu-id="acaed-231">Маркеры в URL-адресе не разрешаются после нажатия клавиши F5 в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="acaed-231">The tokens in the URL are not resolved after you press the F5 key in Visual Studio.</span></span>|<span data-ttu-id="acaed-232">Перейдите на страницу **Контент сайта** на хост-сайте и щелкните значок надстройки.</span><span class="sxs-lookup"><span data-stu-id="acaed-232">Go to the **Site Contents** page in the host web, and click the icon for your add-in.</span></span>|

## <a name="next-steps"></a><span data-ttu-id="acaed-233">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="acaed-233">Next steps</span></span>
<span data-ttu-id="acaed-234"><a name="SP15Createcustomactionsapps_Nextsteps"> </a></span><span class="sxs-lookup"><span data-stu-id="acaed-234"></span></span>

<span data-ttu-id="acaed-p117">В данной статье рассказывается, как создать дополнительное действие в надстройке для SharePoint. Далее вы можете изучить другие компоненты взаимодействия с пользователем, доступные в надстройках для SharePoint. Дополнительные сведения см. в указанных далее статьях.</span><span class="sxs-lookup"><span data-stu-id="acaed-p117">This article demonstrated how to create a custom action in a SharePoint Add-in. As a next step, you can learn about other UX components that are available for SharePoint Add-ins. To learn more, see the following:</span></span>
 

 

-  [<span data-ttu-id="acaed-238">Пример кода. Открытие удаленной веб-страницы надстройки с помощью дополнительного действия ECB</span><span class="sxs-lookup"><span data-stu-id="acaed-238">Code sample: Open a remote add-in webpage using an ECB custom action</span></span>](http://code.msdn.microsoft.com/SharePoint-2013-Open-e0ca1826)
    
 
-  [<span data-ttu-id="acaed-239">SharePoint-Add-in-Localization</span><span class="sxs-lookup"><span data-stu-id="acaed-239">SharePoint-Add-in-Localization</span></span>](https://github.com/OfficeDev/SharePoint-Add-in-Localization)
    
 
-  [<span data-ttu-id="acaed-240">Пример кода. Использование дополнительных действий и междоменной библиотеки для заказа книг</span><span class="sxs-lookup"><span data-stu-id="acaed-240">Code sample: Use custom actions and the cross-domain library to order books</span></span>](http://code.msdn.microsoft.com/SharePoint-2013-Open-a-36d1598d)
    
 
-  [<span data-ttu-id="acaed-241">Использование таблицы стилей веб-сайта SharePoint в надстройках SharePoint</span><span class="sxs-lookup"><span data-stu-id="acaed-241">Use a SharePoint website's style sheet in SharePoint Add-ins</span></span>](use-a-sharepoint-website-s-style-sheet-in-sharepoint-add-ins)
    
 
-  [<span data-ttu-id="acaed-242">Использование клиентского элемента управления хрома в надстройках SharePoint</span><span class="sxs-lookup"><span data-stu-id="acaed-242">Use the client chrome control in SharePoint Add-ins</span></span>](use-the-client-chrome-control-in-sharepoint-add-ins)
    
 
-  [<span data-ttu-id="acaed-243">Создание частей надстройки для установки совместно с надстройкой SharePoint</span><span class="sxs-lookup"><span data-stu-id="acaed-243">Create add-in parts to install with your SharePoint Add-in</span></span>](create-add-in-parts-to-install-with-your-sharepoint-add-in)
    
 

## <a name="additional-resources"></a><span data-ttu-id="acaed-244">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="acaed-244">Additional resources</span></span>
<span data-ttu-id="acaed-245"><a name="SP15Createcustomactionsapps_AddResources"> </a></span><span class="sxs-lookup"><span data-stu-id="acaed-245"></span></span>


-  [<span data-ttu-id="acaed-246">Настройка локальной среды разработки для надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="acaed-246">Set up an on-premises development environment for SharePoint Add-ins</span></span>](set-up-an-on-premises-development-environment-for-sharepoint-add-ins)
    
 
-  [<span data-ttu-id="acaed-247">Дизайн пользовательского интерфейса надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="acaed-247">UX design for SharePoint Add-ins</span></span>](ux-design-for-sharepoint-add-ins)
    
 
-  [<span data-ttu-id="acaed-248">Рекомендации по проектированию пользовательского интерфейса надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="acaed-248">SharePoint Add-ins UX design guidelines</span></span>](sharepoint-add-ins-ux-design-guidelines)
    
 
-  [<span data-ttu-id="acaed-249">Создание компонентов пользовательского интерфейса в SharePoint</span><span class="sxs-lookup"><span data-stu-id="acaed-249">Create UX components in SharePoint</span></span>](create-ux-components-in-sharepoint-2013)
    
 
-  [<span data-ttu-id="acaed-250">Что следует рассмотреть, прежде чем приступать к разработке надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="acaed-250">Three ways to think about design options for SharePoint Add-ins</span></span>](three-ways-to-think-about-design-options-for-sharepoint-add-ins)
    
 
-  [<span data-ttu-id="acaed-251">Важные аспекты разработки и архитектуры для надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="acaed-251">Important aspects of the SharePoint Add-in architecture and development landscape</span></span>](important-aspects-of-the-sharepoint-add-in-architecture-and-development-landscape)
    
 

