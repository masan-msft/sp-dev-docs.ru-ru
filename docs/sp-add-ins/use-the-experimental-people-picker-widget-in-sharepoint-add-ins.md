
# <a name="use-the-experimental-people-picker-widget-in-sharepoint-add-ins"></a><span data-ttu-id="560b9-101">Использование экспериментального мини-приложения "Выбор людей" в надстройках SharePoint</span><span class="sxs-lookup"><span data-stu-id="560b9-101">Use the experimental People Picker widget in SharePoint Add-ins</span></span>
<span data-ttu-id="560b9-p101">Узнайте, как использовать мини-приложение "Выбор людей" на любой веб-странице, даже если страница не размещена в SharePoint. С помощью мини-приложения "Выбор людей" можно помочь пользователям надстройки находить и выбирать людей и группы.</span><span class="sxs-lookup"><span data-stu-id="560b9-p101">Learn how to use the People Picker widget on any web page, even if the page is not hosted in SharePoint. Use the People Picker widget in your add-ins to help users find and select people and groups.</span></span>
 

 <span data-ttu-id="560b9-p102">**Примечание.** В настоящее время идет процесс замены названия "приложения для SharePoint" названием "надстройки SharePoint". Во время этого процесса в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio может по-прежнему использоваться термин "приложения для SharePoint". Дополнительные сведения см. в статье [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="560b9-p102">The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span></span>
 


 <span data-ttu-id="560b9-p103">**Внимание!** Экспериментальные мини-приложения Office для веб-страниц предоставляются только в целях исследований и сбора отзывов. Не следует использовать их в производственных сценариях. Принцип работы мини-приложений Office для веб-страниц может существенно измениться в будущих выпусках. Ознакомьтесь с [условиями лицензии на экспериментальные мини-приложения Office для веб-страниц](office-web-widgets--experimental-license-terms).</span><span class="sxs-lookup"><span data-stu-id="560b9-p103">**Caution** The Office Web Widgets - Experimental are only provided for research and feedback purposes. Do not use in production scenarios. The Office Web Widgets behavior may change significantly in future releases. Read and review the  [Office Web Widgets - Experimental License Terms](office-web-widgets--experimental-license-terms).</span></span>
 


<span data-ttu-id="560b9-p104">Используя в надстройках экспериментальный виджет "Выбор людей", вы можете помочь пользователям находить и выбирать людей и группы в клиенте. Когда пользователь вводит текст в текстовом поле, виджет загружает контакты, чьи имена или адреса электронной почты соответствуют запросу.</span><span class="sxs-lookup"><span data-stu-id="560b9-p104">You can use the experimental People Picker widget in add-ins to help your users find and select people and groups in a tenant. Users can start typing in the text box and the widget retrieves the people whose name or e-mail matches the text.</span></span>
 


<span data-ttu-id="560b9-113">**Рис. 1. Обработка запроса мини-приложением "Выбор людей"**</span><span class="sxs-lookup"><span data-stu-id="560b9-113">**Figure 1. People Picker widget solving a query**</span></span>

 

 
![Экспериментальный элемент управления "Выбор людей" на странице](../../images/PeoplePicker_basic.png)
 

 

 
<span data-ttu-id="560b9-p105">Надстройка может получать доступ к выбранным пользователям, считывая свойство **selectedItems** мини-приложения. Свойство selectedItems является массивом объектов, которые представляют людей или группы. В приведенной ниже таблице показаны доступные свойства объекта пользователя.</span><span class="sxs-lookup"><span data-stu-id="560b9-p105">Your add-in can access the selected people by reading the **selectedItems** property of the widget. The selectedItems property is an array of objects that represent people or groups. The following table shows the available properties of the user object.</span></span>
 


|<span data-ttu-id="560b9-118">**Свойство**</span><span class="sxs-lookup"><span data-stu-id="560b9-118">**Property**</span></span>|<span data-ttu-id="560b9-119">**Описание**</span><span class="sxs-lookup"><span data-stu-id="560b9-119">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="560b9-120">**department**</span><span class="sxs-lookup"><span data-stu-id="560b9-120">**department**</span></span>|<span data-ttu-id="560b9-121">Представляет подразделение пользователя или группы.</span><span class="sxs-lookup"><span data-stu-id="560b9-121">Represents the department of the user or group.</span></span>|
|<span data-ttu-id="560b9-122">**displayName**</span><span class="sxs-lookup"><span data-stu-id="560b9-122">**displayName**</span></span>|<span data-ttu-id="560b9-123">Представляет отображаемое имя пользователя или группы.</span><span class="sxs-lookup"><span data-stu-id="560b9-123">Represents the display name of the user or group.</span></span>|
|<span data-ttu-id="560b9-124">**email**</span><span class="sxs-lookup"><span data-stu-id="560b9-124">**email**</span></span>|<span data-ttu-id="560b9-125">Представляет электронный адрес пользователя или группы.</span><span class="sxs-lookup"><span data-stu-id="560b9-125">Represents the e-mail address of the user or group.</span></span>|
|<span data-ttu-id="560b9-126">**isResolved**</span><span class="sxs-lookup"><span data-stu-id="560b9-126">**isResolved**</span></span>|<span data-ttu-id="560b9-127">Указывает, удалось ли мини-приложению разрешить текст для пользователя или группы в клиенте.</span><span class="sxs-lookup"><span data-stu-id="560b9-127">Indicates if the widget has successfully resolved the text in the widget against a user or group in the tenant.</span></span>|
|<span data-ttu-id="560b9-128">**jobTitle**</span><span class="sxs-lookup"><span data-stu-id="560b9-128">**jobTitle**</span></span>|<span data-ttu-id="560b9-129">Представляет должность пользователя.</span><span class="sxs-lookup"><span data-stu-id="560b9-129">Represents the job title of the user.</span></span>|
|<span data-ttu-id="560b9-130">**loginName**</span><span class="sxs-lookup"><span data-stu-id="560b9-130">**loginName**</span></span>|<span data-ttu-id="560b9-131">Представляет имя для входа пользователя или группы.</span><span class="sxs-lookup"><span data-stu-id="560b9-131">Represents the login name of the user or group.</span></span>|
|<span data-ttu-id="560b9-132">**mobile**</span><span class="sxs-lookup"><span data-stu-id="560b9-132">**mobile**</span></span>|<span data-ttu-id="560b9-133">Представляет номер мобильного телефона пользователя или группы.</span><span class="sxs-lookup"><span data-stu-id="560b9-133">Represents the mobile phone number of the user or group.</span></span>|
|<span data-ttu-id="560b9-134">**principalId**</span><span class="sxs-lookup"><span data-stu-id="560b9-134">**principalId**</span></span>|<span data-ttu-id="560b9-135">Представляет идентификатор субъекта пользователя или группы.</span><span class="sxs-lookup"><span data-stu-id="560b9-135">Represents the principal ID of the user or group.</span></span>|
|<span data-ttu-id="560b9-136">**principalType**</span><span class="sxs-lookup"><span data-stu-id="560b9-136">**principalType**</span></span>|<span data-ttu-id="560b9-p106">Указывает, является ли элемент пользователем или группой. Принимает значение 1, если это пользователь, и 4, если это группа.</span><span class="sxs-lookup"><span data-stu-id="560b9-p106">Indicates if the item is a user or a group. It has a value of 1 if it's a user, 4 if it's a group.</span></span>|
|<span data-ttu-id="560b9-139">**sipAddress**</span><span class="sxs-lookup"><span data-stu-id="560b9-139">**sipAddress**</span></span>|<span data-ttu-id="560b9-140">Представляет SIP-адрес пользователя или группы.</span><span class="sxs-lookup"><span data-stu-id="560b9-140">Represents the sip address of the user or group.</span></span>|
|<span data-ttu-id="560b9-141">**text**</span><span class="sxs-lookup"><span data-stu-id="560b9-141">**text**</span></span>|<span data-ttu-id="560b9-142">Представляет текст имени пользователя или группы.</span><span class="sxs-lookup"><span data-stu-id="560b9-142">Represents the text title of the user or group name.</span></span>|
<span data-ttu-id="560b9-p107">Мини-приложение "Выбор людей" имеет кэш последних использовавшихся записей (MRU). В кэше хранятся пять последних записей, которые были обработаны мини-приложением.</span><span class="sxs-lookup"><span data-stu-id="560b9-p107">The People Picker widget has a cache of the most recently used (MRU) entries. The cache stores the five latest entries that the widget resolved.</span></span>
 

## <a name="prerequisites-for-using-the-examples-in-this-article"></a><span data-ttu-id="560b9-145">Необходимые условия для использования примеров в этой статье</span><span class="sxs-lookup"><span data-stu-id="560b9-145">Prerequisites for using the examples in this article</span></span>

<span data-ttu-id="560b9-146">Для использования примеров, описанных в этой статье, вам необходимо следующее:</span><span class="sxs-lookup"><span data-stu-id="560b9-146">To use the examples in this article, you need the following:</span></span>
 

 

- <span data-ttu-id="560b9-147">Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="560b9-147">Visual Studio 2013.</span></span>
    
 
- <span data-ttu-id="560b9-p108">Диспетчер пакетов NuGet. Дополнительные сведения см. в статье [Установка NuGet](http://go.microsoft.com/fwlink/?LinkId=271465).</span><span class="sxs-lookup"><span data-stu-id="560b9-p108">NuGet Package Manager. For more information, see  [Installing NuGet](http://go.microsoft.com/fwlink/?LinkId=271465).</span></span>
    
 
- <span data-ttu-id="560b9-150">Среда разработки SharePoint (для локальных сценариев требуется изоляция приложений).</span><span class="sxs-lookup"><span data-stu-id="560b9-150">A SharePoint development environment (app isolation required for on-premises scenarios).</span></span>
    
 
- <span data-ttu-id="560b9-p109">Пакет NuGet "Веб-виджеты Office (экспериментальная версия)". Дополнительные сведения об установке пакетов NuGet см. в разделе  [Управление пакетами NuGet с помощью диалогового окна](http://docs.nuget.org/docs/start-here/managing-nuget-packages-using-the-dialog). Вы также можете просмотреть  [коллекцию NuGet](http://www.nuget.org/packages/Microsoft.Office.WebWidgets.Experimental/).</span><span class="sxs-lookup"><span data-stu-id="560b9-p109">Office Web Widgets - Experimental NuGet package. For more information about how to install a NuGet package, see  [Managing NuGet Packages Using the Dialog](http://docs.nuget.org/docs/start-here/managing-nuget-packages-using-the-dialog). You can also browse the  [NuGet gallery page](http://www.nuget.org/packages/Microsoft.Office.WebWidgets.Experimental/).</span></span>
    
 

## <a name="use-the-people-picker-widget-in-a-provider-hosted-sharepoint-add-in"></a><span data-ttu-id="560b9-154">Использование мини-приложения "Выбор людей" в размещаемой у поставщика надстройке SharePoint</span><span class="sxs-lookup"><span data-stu-id="560b9-154">Use the People Picker widget in a provider-hosted SharePoint Add-in</span></span>

<span data-ttu-id="560b9-p110">В этом примере представлена простая страница, размещенная вне SharePoint, которая объявляет мини-приложение "Выбор людей" с использованием разметки. Для простоты в этом примере не объявлено никаких параметров. Пример с параметрами приведен в разделе [Следующие шаги](use-the-experimental-people-picker-widget-in-sharepoint-add-ins#NextSteps).</span><span class="sxs-lookup"><span data-stu-id="560b9-p110">In this example, there is a simple page hosted outside of SharePoint that declares a People Picker widget using markup. To keep things simple, this example doesn't declare any options, but you can see an example with options in the  [NextSteps](use-the-experimental-people-picker-widget-in-sharepoint-add-ins#NextSteps) section.</span></span>
 

 
<span data-ttu-id="560b9-157">Чтобы использовать мини-приложение "Выбор людей", выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="560b9-157">To use the People Picker widget, you must do the following:</span></span>
 

 

- <span data-ttu-id="560b9-158">Создайте надстройку SharePoint и веб-проекты.</span><span class="sxs-lookup"><span data-stu-id="560b9-158">Create SharePoint Add-in and web projects.</span></span>
    
 
- <span data-ttu-id="560b9-p111">Создайте модуль на сайте надстройки. Это также гарантирует, что сайт надстройки будет создан при развертывании надстройки пользователем.</span><span class="sxs-lookup"><span data-stu-id="560b9-p111">Create a module on the add-in web. This step ensures that an add-in web is created when users deploy the add-in.</span></span>
    
     <span data-ttu-id="560b9-p112">**Примечание.** Междоменная библиотека требует наличия сайта надстройки. Мини-приложение "Выбор людей" взаимодействует с SharePoint посредством междоменной библиотеки.</span><span class="sxs-lookup"><span data-stu-id="560b9-p112">**Note** The cross-domain library requires the existence of an add-in web. The People Picker widget communicates with SharePoint by using the cross-domain library.</span></span>
- <span data-ttu-id="560b9-163">Создайте страницу надстройки, в которой с помощью части кода объявляется экземпляр мини-приложения "Выбор людей".</span><span class="sxs-lookup"><span data-stu-id="560b9-163">Create an add-in page that declares a People Picker widget instance using markup.</span></span>
    
 

### <a name="to-create-a-sharepoint-add-in-and-web-projects"></a><span data-ttu-id="560b9-164">Создание надстройки SharePoint и веб-проектов</span><span class="sxs-lookup"><span data-stu-id="560b9-164">To create a SharePoint Add-in and web projects</span></span>


1. <span data-ttu-id="560b9-p113">Откройте Visual Studio 2013 от имени администратора. Для этого нажмите значок Visual Studio 2013 в меню **Пуск** и выберите пункт **Запуск от имени администратора**.</span><span class="sxs-lookup"><span data-stu-id="560b9-p113">Open Visual Studio 2013 as administrator. (To do this, choose the Visual Studio 2013 icon on the **Start** menu, and choose **Run as administrator**.)</span></span>
    
 
2. <span data-ttu-id="560b9-167">Создайте проект, используя шаблон "Надстройка SharePoint 2013". Шаблон **Надстройка SharePoint 2013** находится в следующем разделе: **Шаблоны**> **Visual C#**, **Office/SharePoint**> **Надстройки**.</span><span class="sxs-lookup"><span data-stu-id="560b9-167">Create a new project using the SharePoint Add-in 2013 template.The **SharePoint Add-in 2013** template is located under **Templates**> **Visual C#**, **Office/SharePoint**> **Add-ins**.</span></span>
    
 
3. <span data-ttu-id="560b9-168">Укажите URL-адрес веб-сайта SharePoint, который вы хотите использовать для отладки.</span><span class="sxs-lookup"><span data-stu-id="560b9-168">Provide the SharePoint website URL that you want to use for debugging.</span></span>
    
 
4. <span data-ttu-id="560b9-169">Выберите для надстройки вариант размещения **Размещено у поставщика**.</span><span class="sxs-lookup"><span data-stu-id="560b9-169">Select **Provider-hosted** as the hosting option for your add-in.</span></span>
    
     <span data-ttu-id="560b9-170">**Примечание.** Мини-приложение "Выбор людей" можно использовать и с другими вариантами размещения, а также с надстройками Office и собственным веб-сайтом.</span><span class="sxs-lookup"><span data-stu-id="560b9-170">**Note** You can also use the People Picker widget with other hosting options or even with Office Add-ins or your own website.</span></span>
5. <span data-ttu-id="560b9-171">Выберите **Приложение веб-форм ASP.NET** в качестве типа проекта веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="560b9-171">Select **ASP.NET Web Forms Application** as the type of web application project.</span></span>
    
 
6. <span data-ttu-id="560b9-172">Выберите **службу контроля доступа Windows Azure** в качестве способа проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="560b9-172">Select **Windows Azure Access Control Service** as the authentication option.</span></span>
    
 

### <a name="to-create-a-module-on-the-add-in-web"></a><span data-ttu-id="560b9-173">Создание модуля на сайте надстройки</span><span class="sxs-lookup"><span data-stu-id="560b9-173">To create a module on the add-in web</span></span>


1. <span data-ttu-id="560b9-p114">Выберите проект надстройки SharePoint в **обозревателе решений**. Выберите команду **Добавить**> **Создать элемент…**</span><span class="sxs-lookup"><span data-stu-id="560b9-p114">Choose the SharePoint Add-in project in **Solution Explorer**. Choose **Add**> **New Item…**</span></span>
    
 
2. <span data-ttu-id="560b9-p115">Выберите **Элементы Visual C#**> **Office/SharePoint**> **Модуль**. Укажите имя модуля.</span><span class="sxs-lookup"><span data-stu-id="560b9-p115">Choose **Visual C# Items**> **Office/SharePoint**> **Module**. Provide a name for your module.</span></span>
    
     <span data-ttu-id="560b9-178">**Примечание.** При создании надстройки, размещаемой в SharePoint, нет необходимости создавать дополнительный модуль.</span><span class="sxs-lookup"><span data-stu-id="560b9-178">**Note** If you're building a SharePoint-hosted add-in, you don't need to create an extra module.</span></span>

### <a name="to-add-a-new-page-that-uses-the-people-picker-widget"></a><span data-ttu-id="560b9-179">Добавление новой страницы, использующей мини-приложение "Выбор людей"</span><span class="sxs-lookup"><span data-stu-id="560b9-179">To add a new page that uses the People Picker widget</span></span>


1. <span data-ttu-id="560b9-180">Выберите папку **Страницы** веб-проекта в **обозревателе решений**.</span><span class="sxs-lookup"><span data-stu-id="560b9-180">Choose the **Pages** folder in the web project in **Solution Explorer**.</span></span>
    
 
2. <span data-ttu-id="560b9-p116">Скопируйте приведенный ниже код и вставьте его в **ASPX**-файл в проекте. Этот код выполняет следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="560b9-p116">Copy the following code and paste it in an **ASPX** file in the project. The code performs the following tasks:</span></span>
    
      - <span data-ttu-id="560b9-183">добавляет ссылки на необходимые библиотеки и ресурсы Office;</span><span class="sxs-lookup"><span data-stu-id="560b9-183">Adds references to the required Office libraries and resources.</span></span>
    
 
  - <span data-ttu-id="560b9-184">инициализирует среду выполнения элементов управления;</span><span class="sxs-lookup"><span data-stu-id="560b9-184">Initializes the controls runtime.</span></span>
    
 
  - <span data-ttu-id="560b9-185">запускает метод **renderAll** среды выполнения для элементов управления Office;</span><span class="sxs-lookup"><span data-stu-id="560b9-185">Runs the **renderAll** method of the Office Controls runtime.</span></span>
    
 
  - <span data-ttu-id="560b9-186">объявляет заполнитель для мини-приложения "Выбор людей".</span><span class="sxs-lookup"><span data-stu-id="560b9-186">Declares a placeholder for the People Picker widget.</span></span>
    
 

```
  <!DOCTYPE html>
<html>
<head>
    <!-- IE9 or superior -->
    <meta http-equiv="X-UA-Compatible" content="IE=9" >
    <title>People Picker HTML Markup</title>

    <!-- Widgets Specific CSS File -->
    <link 
        rel="stylesheet" 
        type="text/css" 
        href="../Scripts/Office.Controls.css" 
    />

    <!-- Ajax, jQuery, and utils --> 
    <script 
        src=" https://ajax.aspnetcdn.com/ajax/4.0/1/MicrosoftAjax.js.js">
    </script>
    <script 
        src=" https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.min.js">
    </script>
    <script type="text/javascript">
        // Function to retrieve a query string value.
        // For production purposes you may want to use
        //  a library to handle the query string.
        function getQueryStringParameter(paramToRetrieve) {
            var params =
                document.URL.split("?")[1].split("&amp;");
            var strParams = "";
            for (var i = 0; i < params.length; i = i + 1) {
                var singleParam = params[i].split("=");
                if (singleParam[0] == paramToRetrieve)
                    return singleParam[1];
            }
        }
    </script>

    <!-- Cross-Domain Library and Office controls runtime -->
    <script type="text/javascript">
        //Register namespace and variables used through the sample
        Type.registerNamespace("Office.Samples.PeoplePickerBasic");
        //Retrieve context tokens from the querystring
        Office.Samples.PeoplePickerBasic.appWebUrl =
            decodeURIComponent(getQueryStringParameter("SPAppWebUrl"));
        Office.Samples.PeoplePickerBasic.hostWebUrl =
            decodeURIComponent(getQueryStringParameter("SPHostUrl"));

        //Pattern to dynamically load JSOM and and the cross-domain library
        var scriptbase =
            Office.Samples.PeoplePickerBasic.hostWebUrl + "/_layouts/15/";

        //Get the cross-domain library
        $.getScript(scriptbase + "SP.RequestExecutor.js",
            //Get the Office controls runtime and 
            //  continue to the createControl function
            function () {
                $.getScript("../Scripts/Office.Controls.js", createControl)
            }
        );
    </script>

    <!--People Picker -->
    <script 
        src="../Scripts/Office.Controls.PeoplePicker.js" 
        type="text/javascript">
    </script>
</head>
<body>
Basic People Picker sample (HTML markup declaration):
<div 
        id="PeoplePickerDiv" 
        data-office-control="Office.Controls.PeoplePicker">
</div>

<script type="text/javascript">
    function createControl() {
        //Initialize Controls Runtime
        Office.Controls.Runtime.initialize({
            sharePointHostUrl: Office.Samples.PeoplePickerBasic.hostWebUrl,
            appWebUrl: Office.Samples.PeoplePickerBasic.appWebUrl
        });

        //Render the widget, this must be executed after the
        //placeholder DOM is loaded
        Office.Controls.Runtime.renderAll();
    }
</script>
</body>
</html>

```


 <span data-ttu-id="560b9-p117">**Примечание.** В приведенном выше примере кода явно указываются URL-адреса хост-сайта и сайта надстройки, чтобы инициализировать среду выполнения для элементов управления Office. Однако если URL-адреса хост-сайта и сайта надстройки указаны в параметрах строки запроса **SPAppWebUrl** и **SPHostUrl** соответственно, то вы можете передать пустой объект, и код попытается получить параметры автоматически. Параметры **SPAppWebUrl** и **SPHostUrl** включаются в строку запроса при использовании маркера **{StandardTokens}**.</span><span class="sxs-lookup"><span data-stu-id="560b9-p117">**Note** The code example above explicitly specifies the host web and add-in web URLs to initialize the Office controls runtime. However, if the add-in web and host web URLs are specified in the **SPAppWebUrl** and **SPHostUrl** query string parameters, respectively; you can pass an empty object and the code will attempt to get the parameters automatically. The **SPAppWebUrl** and **SPHostUrl** parameters are included in the query string when you use the **{StandardTokens}** token.</span></span>
 

<span data-ttu-id="560b9-190">В приведенной ниже примере показано, как передавать пустой объект в метод инициализации.</span><span class="sxs-lookup"><span data-stu-id="560b9-190">The following example shows you how to pass an empty object to the initialize method:</span></span>
 

 



```
// Initialize with an empty object and the code 
// will attempt to get the tokens from the
// query string directly.
Office.Controls.Runtime.initialize({});
```


### <a name="to-build-and-run-the-solution"></a><span data-ttu-id="560b9-191">Для создания и запуска решения</span><span class="sxs-lookup"><span data-stu-id="560b9-191">To build and run the solution</span></span>


1. <span data-ttu-id="560b9-192">Нажмите клавишу F5.</span><span class="sxs-lookup"><span data-stu-id="560b9-192">Press the F5 key.</span></span>
    
     <span data-ttu-id="560b9-193">**Примечание.** При нажатии клавиши F5 Visual Studio выполняет сборку решения, развертывает надстройку и открывает для нее страницу разрешений.</span><span class="sxs-lookup"><span data-stu-id="560b9-193">**Note** When you press F5, Visual Studio builds the solution, deploys the add-in, and opens the permissions page for the add-in.</span></span>
2. <span data-ttu-id="560b9-194">Нажмите кнопку **Доверять**.</span><span class="sxs-lookup"><span data-stu-id="560b9-194">Choose the **Trust It** button.</span></span>
    
 
3. <span data-ttu-id="560b9-195">Выберите значок надстройки на странице **Содержимое сайта**.</span><span class="sxs-lookup"><span data-stu-id="560b9-195">Choose the add-in icon on the **Site Contents** page.</span></span>
    
 
<span data-ttu-id="560b9-196">Вы также можете загрузить этот пример из коллекции кода. См. пример кода [Использование экспериментальной версии мини-приложения "Выбор людей" в надстройке](http://code.msdn.microsoft.com/SharePoint-2013-Use-the-57859f85).</span><span class="sxs-lookup"><span data-stu-id="560b9-196">You can also download this sample from code gallery, see the  [Use the People Picker experimental widget in an add-in](http://code.msdn.microsoft.com/SharePoint-2013-Use-the-57859f85) code sample.</span></span>
 

 

## 
<span data-ttu-id="560b9-197"><a name="NextSteps"> </a></span><span class="sxs-lookup"><span data-stu-id="560b9-197"></span></span>

<span data-ttu-id="560b9-p118">В этой статье описано, как использовать мини-приложение "Выбор людей" в своей надстройке с помощью HTML. Кроме того, вы можете ознакомиться со следующими сценариями и сведениями о мини-приложении.</span><span class="sxs-lookup"><span data-stu-id="560b9-p118">This article shows how to use the People Picker widget in your add-in by using HTML. You can also explore the following scenarios and details about the widget.</span></span>
 

 

### <a name="use-javascript-to-declare-the-people-picker-widget"></a><span data-ttu-id="560b9-200">Использование JavaScript для объявления мини-приложения "Выбор людей"</span><span class="sxs-lookup"><span data-stu-id="560b9-200">Use JavaScript to declare the People Picker widget</span></span>

<span data-ttu-id="560b9-p119">В зависимости от своих предпочтений, вы можете использовать JavaScript вместо HTML для объявления мини-приложения. В этом случае вы можете применить следующую разметку в качестве заполнителя для мини-приложения.</span><span class="sxs-lookup"><span data-stu-id="560b9-p119">Depending on your preference, you might want to use the JavaScript instead of HTML to declare the widget. If this is the case you can use the following markup as the placeholder for the widget.</span></span>
 

 

```HTML
<div id="PeoplePickerDiv"></div>
```

<span data-ttu-id="560b9-203">Используйте приведенный ниже код JavaScript, чтобы создавать экземпляры мини-приложения "Выбор людей".</span><span class="sxs-lookup"><span data-stu-id="560b9-203">Use the following JavaScript code to instantiate the People Picker.</span></span>
 

 



```
new Office.Controls.PeoplePicker(
    document.getElementById("PeoplePickerDiv"), {});
```

<span data-ttu-id="560b9-204">Пример кода, иллюстрирующий выполнение этих задач, представлен на странице **JSSimple.html** образца [Использование экспериментального мини-приложения "Выбор людей" в надстройке](http://code.msdn.microsoft.com/SharePoint-2013-Use-the-57859f85).</span><span class="sxs-lookup"><span data-stu-id="560b9-204">For a code sample that shows how to perform the tasks, see the **JSSimple.html** page in the [Use the People Picker experimental widget in an add-in](http://code.msdn.microsoft.com/SharePoint-2013-Use-the-57859f85) code sample.</span></span>
 

 

### <a name="specify-options-for-the-widget"></a><span data-ttu-id="560b9-205">Указание параметров мини-приложения</span><span class="sxs-lookup"><span data-stu-id="560b9-205">Specify options for the widget</span></span>

<span data-ttu-id="560b9-p120">Вы можете задавать параметры мини-приложения с помощью атрибута **data-office-options** в объявлении мини-приложения. Приведенный ниже код HTML иллюстрирует настройку параметров мини-приложения "Выбор людей".</span><span class="sxs-lookup"><span data-stu-id="560b9-p120">You can specify options for the widget by using the **data-office-options** attribute in the widget declaration. The following HTML shows how to specify options for the PeoplePicker widget.</span></span>
 

 

```HTML
<div id="PeoplePickerDiv"
        data-office-control="Office.Controls.PeoplePicker"
        data-office-options='{
        "allowMultipleSelections" : true,
        "onChange" : handleChange,
        "placeholder" : "Check the count message, it changes when you add names..."
    }'>
</div>
```

<span data-ttu-id="560b9-208">В приведенном ниже коде показано, как задать параметры при объявлении мини-приложения "Выбор людей" с помощью JavaScript.</span><span class="sxs-lookup"><span data-stu-id="560b9-208">The following code shows how to specify options when you declare the PeoplePicker widget using JavaScript.</span></span>
 

 



```
new Office.Controls.PeoplePicker(
    document.getElementById("PeoplePickerDiv"), {
        allowMultipleSelections: true,
        placeholder: "Check the count message, it changes when you add names...",
        onChange: function (ctrl) {
            document.getElementById("count").textContent = 
ctrl.selectedItems.length.toString();
        }
    });
```

<span data-ttu-id="560b9-p121">Кроме того, вы можете указать обработчики для таких событий, как **onChange**, **onAdded** и **onRemoved**. Обратите внимание, что в приведенном выше коде обработчик события onChange принимает единственный параметр **ctrl**, который является ссылкой на мини-приложение.</span><span class="sxs-lookup"><span data-stu-id="560b9-p121">You can also specify event handlers for the **onChange**, **onAdded**, and **onRemoved** events. Note in the code above that the event handler for the onChange event receives a single parameter **ctrl**, which is a reference to the widget.</span></span>
 

 
<span data-ttu-id="560b9-211">Пример указания параметров приведен на страницах **MarkupOptions.html** и **JSOptions.html** образца [Использование экспериментального мини-приложения "Выбор людей" в надстройке](http://code.msdn.microsoft.com/SharePoint-2013-Use-the-57859f85).</span><span class="sxs-lookup"><span data-stu-id="560b9-211">For an example of how to specify options, see the **MarkupOptions.html** and **JSOptions.html** pages in the [Use the People Picker experimental widget in an add-in](http://code.msdn.microsoft.com/SharePoint-2013-Use-the-57859f85) code sample.</span></span>
 

 

### <a name="retrieve-the-people-or-groups-selected-in-the-widget"></a><span data-ttu-id="560b9-212">Получение пользователей или групп, выбранных в мини-приложении</span><span class="sxs-lookup"><span data-stu-id="560b9-212">Retrieve the people or groups selected in the widget</span></span>

<span data-ttu-id="560b9-213">Чтобы определить, какие люди выбраны в мини-приложении, необходимо выполнить следующие действия.</span><span class="sxs-lookup"><span data-stu-id="560b9-213">To retrieve the people in the widget you must perform the following tasks:</span></span>
 

 

- <span data-ttu-id="560b9-214">Получите ссылку на мини-приложение.</span><span class="sxs-lookup"><span data-stu-id="560b9-214">Get a reference to the widget.</span></span>
    
 
- <span data-ttu-id="560b9-215">Получите доступ к свойству **selectedItems** мини-приложения.</span><span class="sxs-lookup"><span data-stu-id="560b9-215">Access the **selectedItems** property of the widget.</span></span>
    
 
<span data-ttu-id="560b9-216">Вы можете получить ссылку на мини-приложение с помощью приведенного ниже синтаксиса.</span><span class="sxs-lookup"><span data-stu-id="560b9-216">You can get a reference to the widget using the following syntax.</span></span>
 

 



```
var pplPicker = document.getElementById("PeoplePickerDiv")._officeControl;
```

<span data-ttu-id="560b9-217">Вы также можете сохранить ссылку при создании экземпляра мини-приложения.</span><span class="sxs-lookup"><span data-stu-id="560b9-217">You can also save a reference when you instantiate the widget.</span></span>
 

 



```
var pplPicker = new Office.Controls.PeoplePicker(
                        document.getElementById("PeoplePickerDiv"), {});
```

<span data-ttu-id="560b9-p122">Свойство **selectedItems** — это массив объектов, представляющих людей или группы. Люди или группы в массиве selectedItems могут быть разрешенными или неразрешенными. Это можно проверить с помощью свойства **isResolved**. В приведенном ниже примере показано, как получить доступ к элементу *i* в массиве и использовать имя пользователя или группы.</span><span class="sxs-lookup"><span data-stu-id="560b9-p122">The **selectedItems** property is an array of objects that represent people or groups. People or groups in the selectedItems array can either be resolved or unresolved, which you can check in the **isResolved** property. The following example shows how to access the element *i*  in the array and use the name of the person or group.</span></span>
 

 



```
var principal = pplPicker.selectedItems[i];
$("#msg").text(principal.text + " is selected in the control.");
```

<span data-ttu-id="560b9-221">Пример получения выбранных пользователей или групп из мини-приложения приведен на странице **demo.html** в разделе [Мини-приложения Office для веб-страниц: экспериментальная демо-версия](http://code.msdn.microsoft.com/SharePoint-2013-Office-Web-6d44aa9e).</span><span class="sxs-lookup"><span data-stu-id="560b9-221">For an example of how to retrieve the selected people or groups from the widget, see the **demo.html** page of the [Office Web Widgets - Experimental Demo](http://code.msdn.microsoft.com/SharePoint-2013-Office-Web-6d44aa9e) code sample.</span></span>
 

 

### <a name="customize-the-style-of-the-widget"></a><span data-ttu-id="560b9-222">Настройка стиля мини-приложения</span><span class="sxs-lookup"><span data-stu-id="560b9-222">Customize the style of the widget</span></span>

<span data-ttu-id="560b9-p123">Разработчику может потребоваться настроить пользовательский интерфейс мини-приложения. На приведенном ниже рисунке показана иерархия HTML в мини-приложении после его преобразования.</span><span class="sxs-lookup"><span data-stu-id="560b9-p123">As a developer, you might want to customize the look &amp; feel of the widget. The following image shows the HTML hierarchy in the widget after it has been rendered.</span></span>
 

 

<span data-ttu-id="560b9-225">**Рис. 2. Иерархия HTML в мини-приложении "Выбор людей"**</span><span class="sxs-lookup"><span data-stu-id="560b9-225">**Figure 2. HTML hierarchy in the People Picker widget**</span></span>

 

 
![Иерархия HTML в мини-приложении "Выбор людей"](../../images/PeoplePicker_HTMLHierarchy.png)
 
<span data-ttu-id="560b9-227">Мини-приложение определяет множество классов с префиксом **office-peoplepicker**, которые можно найти и настроить в таблице стилей **Office.Controls.css**.</span><span class="sxs-lookup"><span data-stu-id="560b9-227">The widget defines many classes prefixed by **office-peoplepicker**, which you can find and customize in the **Office.Controls.css** style sheet.</span></span>
 

 

## <a name="conclusion"></a><span data-ttu-id="560b9-228">Заключение</span><span class="sxs-lookup"><span data-stu-id="560b9-228">Conclusion</span></span>
<span data-ttu-id="560b9-229"><a name="NextSteps"> </a></span><span class="sxs-lookup"><span data-stu-id="560b9-229"></span></span>

<span data-ttu-id="560b9-p124">С помощью экспериментального мини-приложения "Выбор людей" можно искать людей и группы в клиенте, после чего ваша надстройка сможет использовать участников, выбранных вашими пользователями. Свои идеи и комментарии вы можете оставить на сайте  [Office Developer Platform UserVoice](http://officespdev.uservoice.com/).</span><span class="sxs-lookup"><span data-stu-id="560b9-p124">You can use the experimental People Picker widget to select people and groups in your tenant, your add-in can then use the principals selected by your users. Please, provide ideas and comments in the  [Office Developer Platform UserVoice site](http://officespdev.uservoice.com/).</span></span>
 

 

## <a name="additional-resources"></a><span data-ttu-id="560b9-232">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="560b9-232">Additional resources</span></span>
<span data-ttu-id="560b9-233"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="560b9-233"></span></span>


-  [<span data-ttu-id="560b9-234">Обзор экспериментальных мини-приложений Office для веб-страниц</span><span class="sxs-lookup"><span data-stu-id="560b9-234">Office Web Widgets - Experimental overview</span></span>](office-web-widgets--experimental-overview)
    
 
-  [<span data-ttu-id="560b9-235">Условия лицензии на экспериментальные мини-приложения Office для веб-страниц</span><span class="sxs-lookup"><span data-stu-id="560b9-235">Office Web Widgets - Experimental License Terms</span></span>](office-web-widgets--experimental-license-terms)
    
 
-  [<span data-ttu-id="560b9-236">Страница коллекции NuGet "Экспериментальные мини-приложения Office для веб-страниц"</span><span class="sxs-lookup"><span data-stu-id="560b9-236">Office Web Widgets - Experimental NuGet gallery page</span></span>](http://www.nuget.org/packages/Microsoft.Office.WebWidgets.Experimental/)
    
 
-  <span data-ttu-id="560b9-237">[Пример кода. Использование экспериментального мини-приложения "Выбор людей" в надстройке](http://code.msdn.microsoft.com/SharePoint-2013-Use-the-57859f85).</span><span class="sxs-lookup"><span data-stu-id="560b9-237">[Code sample: Use the People Picker experimental widget in an add-in](http://code.msdn.microsoft.com/SharePoint-2013-Use-the-57859f85).</span></span>
    
 
-  <span data-ttu-id="560b9-238">[Использование экспериментального мини-приложения "Просмотр списка на рабочем столе" в надстройках для SharePoint](use-the-experimental-desktop-list-view-widget-in-sharepoint-add-ins).</span><span class="sxs-lookup"><span data-stu-id="560b9-238">[Use the experimental Desktop List View widget in SharePoint Add-ins](use-the-experimental-desktop-list-view-widget-in-sharepoint-add-ins).</span></span>
    
 

