

# <a name="use-the-experimental-desktop-list-view-widget-in-sharepoint-add-ins"></a><span data-ttu-id="e9169-101">Использование экспериментального мини-приложения Desktop List View в надстройках SharePoint</span><span class="sxs-lookup"><span data-stu-id="e9169-101">Use the experimental Desktop List View widget in SharePoint Add-ins</span></span>
<span data-ttu-id="e9169-p101">Узнайте, как использовать мини-приложение "Представление списка на рабочем столе" на любой веб-странице, даже если она не размещена в SharePoint. Используйте мини-приложение "Представление списка на рабочем столе" в своих надстройках, чтобы отображать данные в списках, размещаемых на сайте SharePoint.</span><span class="sxs-lookup"><span data-stu-id="e9169-p101">Learn how to use the Desktop List View widget on any web page, even if the page is not hosted in SharePoint. Use the List View widget in your add-ins to display data in lists that are hosted in a SharePoint site.</span></span>
 

 <span data-ttu-id="e9169-p102">**Примечание** Название "приложения для SharePoint" меняется на "надстройки SharePoint". В процессе перехода с одного названия на другое в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio по-прежнему может встречаться термин "приложения для SharePoint". Дополнительные сведения см. в статье [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="e9169-p102">The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span></span>
 


 <span data-ttu-id="e9169-p103">**Примечание** Экспериментальная версия мини-приложений Office для веб-страниц предназначена только для ознакомления и сбора отзывов. Не используйте их в производстве. Работа мини-приложений Office для веб-страниц в следующих выпусках может значительно измениться. Прочтите статью [Условия лицензии на экспериментальные мини-приложения Office для веб-страниц](office-web-widgets--experimental-license-terms).</span><span class="sxs-lookup"><span data-stu-id="e9169-p103">**Note** The Office Web Widgets - Experimental are only provided for research and feedback purposes. Do not use in production scenarios. The Office Web Widgets behavior may change significantly in future releases. Read and review the  [Office Web Widgets - Experimental License Terms](office-web-widgets--experimental-license-terms).</span></span>
 


<span data-ttu-id="e9169-111">С помощью мини-приложения "Представление списка" вы можете отображать данные в списке SharePoint подобно тому, как это делается с помощью обычного мини-приложения "Представление списка", но вы можете использовать его даже в тех надстройках и на веб-сайтах, которые не размещены в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="e9169-111">You can use the List View widget to display the data in a SharePoint list similar to the regular List View widget, but you can use it in your add-ins and websites that are not necessarily hosted in SharePoint. Figure 1. Desktop List View widget displaying data in a list</span></span>
 


<span data-ttu-id="e9169-112">**Рисунок 1. Мини-приложение "Представление списка на рабочем столе", в котором показаны данные в списке**</span><span class="sxs-lookup"><span data-stu-id="e9169-112">**Figure 1. Desktop List View widget displaying data in a list**</span></span>

 

 
![Экспериментальный элемент управления "Просмотр списка на рабочем столе"](../../images/DesktopListView_basic.png)
 

 

 

## <a name="introduction"></a><span data-ttu-id="e9169-114">Введение</span><span class="sxs-lookup"><span data-stu-id="e9169-114">Introduction</span></span>

<span data-ttu-id="e9169-p104">Вы можете указать в списке SharePoint представление, которое вы хотите использовать для отображения данных. Виджет "Представление списка" отображает столбцы и элементы в порядке, который указывает представление.</span><span class="sxs-lookup"><span data-stu-id="e9169-p104">You can specify the view in the SharePoint list that you want to use to display the data. The List View widget displays the columns and items in the order specified by the view.</span></span>
 

 
<span data-ttu-id="e9169-p105">Мини-приложение "Представление списка" использует междоменную библиотеку для получения данных списка. Поэтому связь происходит на уровне клиента.</span><span class="sxs-lookup"><span data-stu-id="e9169-p105">The List View widget uses the cross-domain library to get the list data. For this reason, communication happens at the client level.</span></span>
 

 

 <span data-ttu-id="e9169-119">**Внимание!** Мини-приложение "Представление списка на рабочем столе" позволяет выполнять не все сценарии собственного "Представления списка".</span><span class="sxs-lookup"><span data-stu-id="e9169-119">**Caution** The Desktop List View widget doesn't enable all the scenarios of the native List View.</span></span>
 

<span data-ttu-id="e9169-120">В текущей версии мини-приложения не включены следующие сценарии:</span><span class="sxs-lookup"><span data-stu-id="e9169-120">The following scenarios have not been enabled in the current version of the widget:</span></span>
 

 

- <span data-ttu-id="e9169-121">использование виджета в схемах проверки подлинности, неподдерживаемых междоменной библиотекой;</span><span class="sxs-lookup"><span data-stu-id="e9169-121">Use the widget on authentication schemes that aren't natively supported by the cross-domain library.</span></span>
    
 
- <span data-ttu-id="e9169-122">использование виджета с другими источниками данных, кроме библиотек и списков SharePoint;</span><span class="sxs-lookup"><span data-stu-id="e9169-122">Use the widget with data sources other than SharePoint lists or libraries.</span></span>
    
 
- <span data-ttu-id="e9169-123">привязка виджета к данным;</span><span class="sxs-lookup"><span data-stu-id="e9169-123">Data bind the widget.</span></span>
    
 
- <span data-ttu-id="e9169-124">представления с сенсорным управлением;</span><span class="sxs-lookup"><span data-stu-id="e9169-124">User touch-friendly views.</span></span>
    
 
- <span data-ttu-id="e9169-125">встроенная правка пользователями;</span><span class="sxs-lookup"><span data-stu-id="e9169-125">User inline-editing.</span></span>
    
 
- <span data-ttu-id="e9169-126">показ информации о присутствии;</span><span class="sxs-lookup"><span data-stu-id="e9169-126">Show presence information.</span></span>
    
 
- <span data-ttu-id="e9169-127">настраиваемые шаблоны отрисовки;</span><span class="sxs-lookup"><span data-stu-id="e9169-127">Provide custom rendering templates.</span></span>
    
 
- <span data-ttu-id="e9169-p106">локальные сценарии. В данный момент виджет работает только в SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="e9169-p106">On-premises scenarios. At this moment, the widget only works on SharePoint Online.</span></span>
    
 

## <a name="prerequisites-for-using-the-examples-in-this-article"></a><span data-ttu-id="e9169-130">Необходимые условия для использования примеров в этой статье</span><span class="sxs-lookup"><span data-stu-id="e9169-130">Prerequisites for using the examples in this article</span></span>

<span data-ttu-id="e9169-131">Для выполнения примеров, описанных в этой статье, вам необходимо следующее:</span><span class="sxs-lookup"><span data-stu-id="e9169-131">To follow the examples in this article, you need the following:</span></span>
 

 

- <span data-ttu-id="e9169-132">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="e9169-132">Visual Studio 2013</span></span>
    
 
- <span data-ttu-id="e9169-p107">Диспетчер пакетов NuGet. Подробные сведения см. в статье [Установка NuGet](http://go.microsoft.com/fwlink/?LinkId=271465).</span><span class="sxs-lookup"><span data-stu-id="e9169-p107">NuGet Package Manager. For more information, see  [Installing NuGet](http://go.microsoft.com/fwlink/?LinkId=271465).</span></span>
    
 
- <span data-ttu-id="e9169-135">Среда разработки SharePoint (для локальных сценариев требуется изоляция приложений).</span><span class="sxs-lookup"><span data-stu-id="e9169-135">A SharePoint development environment (app isolation required for on-premises scenarios).</span></span> 
    
 
- <span data-ttu-id="e9169-p108">Пакет NuGet экспериментальной версии веб-виджетов Office. Подробнее о том, как устанавливать пакет NuGet, см. в статье  [Управление пакетами NuGet в диалоговом окне](http://docs.nuget.org/docs/start-here/managing-nuget-packages-using-the-dialog). Вы можете также просмотреть  [страницу коллекции NuGet](http://www.nuget.org/packages/Microsoft.Office.WebWidgets.Experimental/).</span><span class="sxs-lookup"><span data-stu-id="e9169-p108">Office Web Widgets - Experimental NuGet package. For more information about how to install a NuGet package, see  [Managing NuGet Packages Using the Dialog](http://docs.nuget.org/docs/start-here/managing-nuget-packages-using-the-dialog). You can also browse the  [NuGet gallery page](http://www.nuget.org/packages/Microsoft.Office.WebWidgets.Experimental/).</span></span>
    
 

## <a name="use-the-desktop-list-view-widget-in-a-provider-hosted-sharepoint-add-in"></a><span data-ttu-id="e9169-139">Использование мини-приложения "Представление списка на рабочем столе" в размещаемой у поставщика надстройке SharePoint</span><span class="sxs-lookup"><span data-stu-id="e9169-139">Use the Desktop List View widget in a provider-hosted SharePoint Add-in</span></span>

<span data-ttu-id="e9169-140">В этом примере показана простая страница, размещенная вне SharePoint, которая объявляет виджет "Представление списка на рабочем столе".</span><span class="sxs-lookup"><span data-stu-id="e9169-140">In this example, there is a simple page hosted outside of SharePoint that declares a Desktop List View widget.</span></span>
 

 
<span data-ttu-id="e9169-141">Чтобы использовать виджет "Представление списка на рабочем столе":</span><span class="sxs-lookup"><span data-stu-id="e9169-141">To use the List View widget, you must do the following:</span></span>
 

 

- <span data-ttu-id="e9169-142">создайте надстройку SharePoint и веб-проекты;</span><span class="sxs-lookup"><span data-stu-id="e9169-142">Create SharePoint Add-in and web projects.</span></span>
    
 
- <span data-ttu-id="e9169-p109">создайте список на сайте надстройки. Этот шаг также гарантирует, что сайт надстройки будет создан, когда пользователи развернут надстройку;</span><span class="sxs-lookup"><span data-stu-id="e9169-p109">Create a list on the add-in web. This step also ensures that an add-in web is created when users deploy the add-in.</span></span>
    
     <span data-ttu-id="e9169-p110">**Примечание** Для междоменной библиотеки требуется наличие сайта надстройки. Мини-приложение "Представление списка" связывается с SharePoint, используя междоменную библиотеку.</span><span class="sxs-lookup"><span data-stu-id="e9169-p110">**Note** The cross-domain library requires the existence of an add-in web. The List View widget communicates with SharePoint by using the cross-domain library.</span></span>
- <span data-ttu-id="e9169-147">создайте страницу надстройки, объявляющую экземпляр мини-приложения "Представление списка" с использованием разметки HTML.</span><span class="sxs-lookup"><span data-stu-id="e9169-147">Create an add-in page that declares a List View widget instance using HTML markup.</span></span>
    
 

### <a name="to-create-a-sharepoint-add-in-and-web-projects"></a><span data-ttu-id="e9169-148">Создание надстройки SharePoint и веб-проектов</span><span class="sxs-lookup"><span data-stu-id="e9169-148">To create a SharePoint Add-in and web projects</span></span>


1. <span data-ttu-id="e9169-p111">Откройте Visual Studio 2013 как администратор. Для этого нажмите значок Visual Studio 2013 в меню **Пуск** и выберите пункт **Запуск от имени администратора**.</span><span class="sxs-lookup"><span data-stu-id="e9169-p111">Open Visual Studio 2013 as administrator. (To do this, choose the Visual Studio 2013 icon on the **Start** menu, and choose **Run as administrator**.)</span></span>
    
 
2. <span data-ttu-id="e9169-p112">Создайте новый проект, используя шаблон **Надстройка SharePoint 2013**. Расположение шаблона Надстройка SharePoint 2013: **Шаблоны**> **Visual C#**, **Office/SharePoint**> **Надстройки**.</span><span class="sxs-lookup"><span data-stu-id="e9169-p112">Create a new project using the **SharePoint Add-in 2013** template. The SharePoint Add-in 2013 template is located under **Templates**> **Visual C#**, **Office/SharePoint**> **Add-ins**.</span></span>
    
 
3. <span data-ttu-id="e9169-153">Укажите URL-адрес веб-сайта SharePoint, который вы хотите использовать для отладки.</span><span class="sxs-lookup"><span data-stu-id="e9169-153">Provide the SharePoint website URL that you want to use for debugging.</span></span>
    
 
4. <span data-ttu-id="e9169-154">Выберите для надстройки вариант размещения **Размещено у поставщика**.</span><span class="sxs-lookup"><span data-stu-id="e9169-154">Select **Provider-hosted** as the hosting option for your add-in.</span></span>
    
     <span data-ttu-id="e9169-155">**Примечание** Вы также можете использовать мини-приложение "Представление списка на рабочем столе" с другими вариантами размещения или даже с надстройками для Office или собственным веб-сайтом.</span><span class="sxs-lookup"><span data-stu-id="e9169-155">**Note** You can also use the Desktop List View widget with other hosting options or even with Office Add-ins or your own website.</span></span>
5. <span data-ttu-id="e9169-156">Выберите **Приложение веб-форм ASP.NET** в качестве типа проекта веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="e9169-156">Select **ASP.NET Web Forms Application** as the type of web application project.</span></span>
    
 
6. <span data-ttu-id="e9169-157">Выберите **службу контроля доступа Windows Azure** в качестве способа проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="e9169-157">Select **Windows Azure Access Control Service** as the authentication option.</span></span>
    
 

### <a name="to-create-a-list-on-the-add-in-web"></a><span data-ttu-id="e9169-158">Создание списка на сайте надстройки</span><span class="sxs-lookup"><span data-stu-id="e9169-158">To create a list on the add-in web</span></span>


1. <span data-ttu-id="e9169-p113">Выберите проект надстройки SharePoint в **обозревателе решений**. Выберите команду **Добавить**> **Создать элемент…**</span><span class="sxs-lookup"><span data-stu-id="e9169-p113">Choose the SharePoint Add-in project in **Solution Explorer**. Choose **Add**> **New Item…**</span></span>
    
 
2. <span data-ttu-id="e9169-p114">Выберите **Элементы Visual C#**> **Office/SharePoint**> **Список**. В текстовое поле **Имя** введите **Объявления**. Выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="e9169-p114">Choose **Visual C# Items**> **Office/SharePoint**> **List**. Type **Announcements** in the **Name** textbox. Choose **Add**.</span></span>
    
 
3. <span data-ttu-id="e9169-p115">Выберите **Создать экземпляр списка на основе существующего шаблона списка**. Выберите шаблон **Объявления**. Нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="e9169-p115">Choose **Create a list instance based on an existing list template**.Choose the **Announcements** template. Choose **Finish**.</span></span>
    
 

### <a name="to-add-a-new-page-that-uses-the-desktop-list-view-widget"></a><span data-ttu-id="e9169-166">Добавление новой страницы, использующей мини-приложение "Представление списка на рабочем столе"</span><span class="sxs-lookup"><span data-stu-id="e9169-166">To add a new page that uses the Desktop List View widget</span></span>


1. <span data-ttu-id="e9169-167">Выберите папку **Страницы** в веб-проекте **Обозреватель решений**.</span><span class="sxs-lookup"><span data-stu-id="e9169-167">Choose the **Pages** folder in the web project in **Solution Explorer**.</span></span>
    
 
2. <span data-ttu-id="e9169-p116">Скопируйте следующий код и вставьте его в файл **ASPX** в проекте. Этот код выполняет следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="e9169-p116">Copy the following code and paste it in an **ASPX** file in the project. The code performs the following tasks:</span></span>
    
      - <span data-ttu-id="e9169-170">добавляет ссылки на необходимые библиотеки и ресурсы Office;</span><span class="sxs-lookup"><span data-stu-id="e9169-170">Adds references to the required Office libraries and resources.</span></span>
    
 
  - <span data-ttu-id="e9169-171">предоставляет заполнитель для виджета "Представление списка";</span><span class="sxs-lookup"><span data-stu-id="e9169-171">Provides a placeholder for the List View widget.</span></span>
    
 
  - <span data-ttu-id="e9169-172">инициализирует среду выполнения элементов управления;</span><span class="sxs-lookup"><span data-stu-id="e9169-172">Initializes the controls runtime.</span></span>
    
 
  - <span data-ttu-id="e9169-173">запускает метод **renderAll** среды выполнения элементов управления Office.</span><span class="sxs-lookup"><span data-stu-id="e9169-173">Runs the **renderAll** method of the Office Controls runtime.</span></span>
    
 

```
  <!DOCTYPE html>
<html>
<head>
    <!-- IE9 or superior -->
    <meta http-equiv="x-ua-compatible" content="IE=10">
    <title>Desktop List View HTML Markup</title>

    <!-- Controls Specific CSS File -->
    <link rel="stylesheet" type="text/css" href="/Scripts/Office.Controls.css" />

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
        Type.registerNamespace("Office.Samples.ListViewBasic");
        //Retrieve context tokens from the querystring
        Office.Samples.ListViewBasic.appWebUrl =
            decodeURIComponent(getQueryStringParameter("SPAppWebUrl"));
        Office.Samples.ListViewBasic.hostWebUrl =
            decodeURIComponent(getQueryStringParameter("SPHostUrl"));
        Office.Samples.ListViewBasic.ctag =
            decodeURIComponent(getQueryStringParameter("SPClientTag"));

        //Pattern to dynamically load JSOM and the cross-domain library
        var scriptbase =
            Office.Samples.ListViewBasic.hostWebUrl + "/_layouts/15/";

        //Get the cross-domain library
        $.getScript(scriptbase + "SP.RequestExecutor.js", 
            //Get the Office controls runtime and 
            //  continue to the createControl function
            function () {
                $.getScript("../Scripts/Office.Controls.js", createControl);
            }
        );
    </script>

    <!-- List View -->
    <script 
        src="../Scripts/Office.Controls.ListView.debug.js" 
        type="text/javascript">
    </script>

    <!-- SharePoint CSS -->
    <script type="text/javascript">
        document.addEventListener("DOMContentLoaded", function () {
            // The resource files are in a URL in the form:
            // web_url/_layouts/15/Resource.ashx
            var scriptbase =
                Office.Samples.ListViewBasic.appWebUrl + "/_layouts/15/";

            // Dynamically create the invisible iframe.
            var blankiframe;
            var blankurl;
            var body;
            blankurl =
                Office.Samples.ListViewBasic.appWebUrl + "/Pages/blank.html";
            blankiframe = document.createElement("iframe");
            blankiframe.setAttribute("src", blankurl);
            blankiframe.setAttribute("style", "display: none");
            body = document.getElementsByTagName("body");
            body[0].appendChild(blankiframe);

            // Dynamically create the link element.
            var dclink;
            var head;
            dclink = document.createElement("link");
            dclink.setAttribute("rel", "stylesheet");
            dclink.setAttribute("href",
                                scriptbase +
                                "defaultcss.ashx?ctag=" +
                                Office.Samples.ListViewBasic.ctag
                                );
            head = document.getElementsByTagName("head");
            head[0].appendChild(dclink);
        }, false);
    </script>
</head>
<body>
    Basic List View sample (HTML markup declaration):
    <div id="ListViewDiv"
         data-office-control="Office.Controls.ListView"
         data-office-options='{"listUrl" : getListUrl()}'>
    </div>

    <script type="text/javascript">
        function createControl() {
            //Initialize Controls Runtime
            Office.Controls.Runtime.initialize({
                sharePointHostUrl: Office.Samples.ListViewBasic.hostWebUrl,
                appWebUrl: Office.Samples.ListViewBasic.appWebUrl
            });

            //Render the widget, this must be executed after the
            //placeholder DOM is loaded
            Office.Controls.Runtime.renderAll();
        }

        function getListUrl() {
            return Office.Samples.ListViewBasic.appWebUrl +
                    "/_api/web/lists/getbytitle('Announcements')";
        }
    </script>
</body>
</html>
```


 <span data-ttu-id="e9169-p117">**Примечание** В приведенном выше примере кода явно указываются URL-адреса хост-сайта и сайта надстройки для инициализации среды выполнения элементов управления Office. Однако если URL-адреса хост-сайта и сайта надстройки указаны в параметрах строк запроса **SPAppWebUrl** и **SPHostUrl** соответственно, можно передать пустой объект, и код попытается получить параметры автоматически. Параметры **SPAppWebUrl** и **SPHostUrl** включаются в строку запроса, когда вы используете маркер **{StandardTokens}**.</span><span class="sxs-lookup"><span data-stu-id="e9169-p117">**Note** The code example above explicitly specifies the host web and add-in web URLs to initialize the Office controls runtime. However, if the add-in web and host web URLs are specified in the **SPAppWebUrl** and **SPHostUrl** query string parameters, respectively; you can pass an empty object and the code will attempt to get the parameters automatically. The **SPAppWebUrl** and **SPHostUrl** parameters are included in the query string when you use the **{StandardTokens}** token.</span></span>
 

<span data-ttu-id="e9169-177">В следующем примере показано, как передавать пустой объект в метод инициализации:</span><span class="sxs-lookup"><span data-stu-id="e9169-177">The following example shows you how to pass an empty object to the initialize method:</span></span>
 

 



```
// Initialize with an empty object and the code 
// will attempt to get the tokens from the
// query string directly.
Office.Controls.Runtime.initialize({});
```


### <a name="to-build-and-run-the-solution"></a><span data-ttu-id="e9169-178">Для создания и запуска решения</span><span class="sxs-lookup"><span data-stu-id="e9169-178">To build and run the solution</span></span>


1. <span data-ttu-id="e9169-179">Нажмите клавишу F5.</span><span class="sxs-lookup"><span data-stu-id="e9169-179">Press the F5 key.</span></span>
    
     <span data-ttu-id="e9169-180">**Примечание** Когда вы нажимаете клавишу F5, Visual Studio выполняет сборку решения, развертывает надстройку и открывает для нее страницу разрешений.</span><span class="sxs-lookup"><span data-stu-id="e9169-180">**Note** When you press F5, Visual Studio builds the solution, deploys the add-in, and opens the permissions page for the add-in.</span></span>
2. <span data-ttu-id="e9169-181">Нажмите кнопку **Доверять**.</span><span class="sxs-lookup"><span data-stu-id="e9169-181">Choose the **Trust It** button.</span></span>
    
 
3. <span data-ttu-id="e9169-182">Выберите значок надстройки на странице **Содержимое сайта**.</span><span class="sxs-lookup"><span data-stu-id="e9169-182">Choose the add-in icon on the **Site Contents** page.</span></span>
    
 
<span data-ttu-id="e9169-183">Вы также можете загрузить этот пример из коллекции кода, см. пример кода [Использование экспериментальной версии мини-приложения "Представление списка на рабочем столе" в надстройке](http://code.msdn.microsoft.com/SharePoint-2013-Use-the-c3edb076).</span><span class="sxs-lookup"><span data-stu-id="e9169-183">You can also download this sample from code gallery, see the  [Use the Desktop List View experimental widget in an add-in](http://code.msdn.microsoft.com/SharePoint-2013-Use-the-c3edb076) code sample.</span></span>
 

 

## 

<span data-ttu-id="e9169-p118">В этой статье показано, как использовать мини-приложение "Представление списка на рабочем столе" в своей надстройке с помощью HTML. Вы также можете ознакомиться со следующими сценариями и сведениями о мини-приложении.</span><span class="sxs-lookup"><span data-stu-id="e9169-p118">This article shows how to use the Desktop List View widget in your add-in by using HTML. You can also explore the following scenarios and details about the widget.</span></span>
 

 

### <a name="use-javascript-to-declare-the-desktop-list-view-widget"></a><span data-ttu-id="e9169-186">Использование JavaScript для объявления виджета "Представление списка на рабочем столе"</span><span class="sxs-lookup"><span data-stu-id="e9169-186">Use JavaScript to declare the Desktop List View widget</span></span>

<span data-ttu-id="e9169-p119">В зависимости от своих предпочтений вы можете объявлять виджет, используя JavaScript вместо HTML. В таком случае вы можете использовать следующую разметку в качестве заполнителя для виджета.</span><span class="sxs-lookup"><span data-stu-id="e9169-p119">Depending on your preference, you might want to use the JavaScript instead of HTML to declare the widget. If this is the case you can use the following markup as the placeholder for the widget.</span></span>
 

 

```HTML
<div id="ListViewDiv"></div>
```

<span data-ttu-id="e9169-189">Используйте следующий код JavaScript, чтобы создавать экземпляры представления списка.</span><span class="sxs-lookup"><span data-stu-id="e9169-189">Use the following JavaScript code to instantiate the List View.</span></span>
 

 



```
new Office.Controls.ListView(
    document.getElementById("ListViewDiv"), {
        listUrl: Office.Samples.ListViewBasic.appWebUrl + "/_api/web/lists/getbytitle('Announcements')"
    });
```

<span data-ttu-id="e9169-190">Пример выполнения задач см. на странице **JSSimple.html** в примере кода [Использование экспериментального мини-приложения "Представление списка на рабочем столе" в надстройке](http://code.msdn.microsoft.com/SharePoint-2013-Use-the-c3edb076).</span><span class="sxs-lookup"><span data-stu-id="e9169-190">For an example that shows how to perform the tasks, see the **JSSimple.html** page in the [Use the Desktop List View experimental widget in an add-in](http://code.msdn.microsoft.com/SharePoint-2013-Use-the-c3edb076) code sample.</span></span>
 

 

### <a name="specify-a-view-to-display-the-data"></a><span data-ttu-id="e9169-191">Указание представления для показа данных</span><span class="sxs-lookup"><span data-stu-id="e9169-191">Specify a view to display the data</span></span>

<span data-ttu-id="e9169-192">Вы можете указать существующее представление в своем списке SharePoint. Виджет "Представление списка" отображает данные, используя спецификацию представления.</span><span class="sxs-lookup"><span data-stu-id="e9169-192">You can specify an existent view in your SharePoint list, the List View widget displays the data using the view specification.</span></span>
 

 
<span data-ttu-id="e9169-193">Если вы объявляете виджет с помощью разметки HTML, вы можете использовать следующий синтаксис для указания представления.</span><span class="sxs-lookup"><span data-stu-id="e9169-193">If you're using HTML markup to declare the widget, you can use the following syntax to specify a view.</span></span>
 

 



```
<div id="ListViewDiv"
        data-office-control="Office.Controls.ListView"
        data-office-options="{listUrl: 'list URL',
                            viewID: 'GUID'
                            }">
</div> 

```

<span data-ttu-id="e9169-194">Если вы объявляете виджет с использованием JavaScript, вы можете использовать следующий синтаксис для указания представления.</span><span class="sxs-lookup"><span data-stu-id="e9169-194">If you're declaring the widget using JavaScript, use the following syntax to specify a view.</span></span>
 

 



```
new Office.Controls.ListView(
    document.getElementById("ListViewDiv"), {
        listUrl: "list URL",
        viewID: "GUID"
    });
```


## <a name="conclusion"></a><span data-ttu-id="e9169-195">Заключение</span><span class="sxs-lookup"><span data-stu-id="e9169-195">Conclusion</span></span>

<span data-ttu-id="e9169-p120">Вы можете использовать экспериментальную версию виджета "Представление списка на рабочем столе" для отображения данных в списках SharePoint. Виджет показывает данные в режиме только для чтения. Оставляйте свои идеи и комментарии на  [сайте Office Developer Platform UserVoice](http://officespdev.uservoice.com/).</span><span class="sxs-lookup"><span data-stu-id="e9169-p120">You can use the experimental Desktop List View widget to display data in SharePoint lists. The widget displays data in read-only mode. Please provide ideas and comments in the  [Office Developer Platform UserVoice site](http://officespdev.uservoice.com/).</span></span>
 

 

## <a name="additional-resources"></a><span data-ttu-id="e9169-199">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="e9169-199">Additional resources</span></span>
<span data-ttu-id="e9169-200"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="e9169-200"></span></span>


-  [<span data-ttu-id="e9169-201">Обзор экспериментальных мини-приложений Office для веб-страниц</span><span class="sxs-lookup"><span data-stu-id="e9169-201">Office Web Widgets - Experimental overview</span></span>](office-web-widgets--experimental-overview)
    
 
-  [<span data-ttu-id="e9169-202">Условия лицензии на экспериментальные мини-приложения Office для веб-страниц</span><span class="sxs-lookup"><span data-stu-id="e9169-202">Office Web Widgets - Experimental License Terms</span></span>](office-web-widgets--experimental-license-terms)
    
 
-  [<span data-ttu-id="e9169-203">Страница коллекции NuGet "Экспериментальные мини-приложения Office для веб-страниц"</span><span class="sxs-lookup"><span data-stu-id="e9169-203">Office Web Widgets - Experimental NuGet gallery page</span></span>](http://www.nuget.org/packages/Microsoft.Office.WebWidgets.Experimental/)
    
 
-  [<span data-ttu-id="e9169-204">Пример кода. Использование экспериментального мини-приложения "Представление списка на рабочем столе"в надстройке</span><span class="sxs-lookup"><span data-stu-id="e9169-204">Code sample: Use the Desktop List View experimental widget in an add-in</span></span>](http://code.msdn.microsoft.com/SharePoint-2013-Use-the-c3edb076)
    
 
-  <span data-ttu-id="e9169-205">[Использование экспериментального мини-приложения "Представление списка на рабочем столе" в надстройках для SharePoint](use-the-experimental-desktop-list-view-widget-in-sharepoint-add-ins).</span><span class="sxs-lookup"><span data-stu-id="e9169-205">[Use the experimental Desktop List View widget in SharePoint Add-ins](use-the-experimental-desktop-list-view-widget-in-sharepoint-add-ins).</span></span>
    
 

