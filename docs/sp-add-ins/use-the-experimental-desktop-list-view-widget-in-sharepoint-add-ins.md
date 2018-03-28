---
title: Использование экспериментального мини-приложения Desktop List View в надстройках SharePoint
description: Используйте мини-приложение Desktop List View в своих надстройках, чтобы показывать данные из списков, размещенных на сайте SharePoint.
ms.date: 12/20/2017
ms.prod: sharepoint
ms.openlocfilehash: 0dbcff715dcaebb27878c2c23de8b4dbb6c5ff0a
ms.sourcegitcommit: 6f2b3b5bd81c2de4f761e10ed5e2f0b9c3c485bf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/21/2017
---
# <a name="use-the-experimental-desktop-list-view-widget-in-sharepoint-add-ins"></a><span data-ttu-id="03ffb-103">Использование экспериментального мини-приложения Desktop List View в надстройках SharePoint</span><span class="sxs-lookup"><span data-stu-id="03ffb-103">Use the experimental Desktop List View widget in SharePoint Add-ins</span></span>

<span data-ttu-id="03ffb-104">Используйте мини-приложение Desktop List View на любой веб-странице, даже если она не размещена в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="03ffb-104">You can use the Desktop List View widget on any web page, even if the page is not hosted in SharePoint.</span></span> <span data-ttu-id="03ffb-105">Используйте мини-приложение List View в своих надстройках, чтобы показывать данные из списков, размещенных на сайте SharePoint.</span><span class="sxs-lookup"><span data-stu-id="03ffb-105">Learn how to use the Desktop List View widget on any web page, even if the page is not hosted in SharePoint. Use the List View widget in your add-ins to display data in lists that are hosted in a SharePoint site.</span></span>
 
> [!WARNING] 
> <span data-ttu-id="03ffb-106">Экспериментальные мини-приложения Office для веб-страниц предоставляются только в целях исследования и сбора отзывов.</span><span class="sxs-lookup"><span data-stu-id="03ffb-106">The Office Web Widgets - Experimental are only provided for research and feedback purposes.</span></span> <span data-ttu-id="03ffb-107">Не следует использовать их в производственных сценариях.</span><span class="sxs-lookup"><span data-stu-id="03ffb-107">Do not use in production scenarios.</span></span> <span data-ttu-id="03ffb-108">Поведение мини-приложений Office для веб-страниц может существенно измениться в будущих выпусках.</span><span class="sxs-lookup"><span data-stu-id="03ffb-108">The Office Web Widgets behavior may change significantly in future releases.</span></span> <span data-ttu-id="03ffb-109">Ознакомьтесь с [условиями лицензии на экспериментальные мини-приложения Office для веб-страниц](office-web-widgetsexperimental-license-terms.md).</span><span class="sxs-lookup"><span data-stu-id="03ffb-109">Read and review the [Office Web Widgets - Experimental License Terms](office-web-widgetsexperimental-license-terms.md).</span></span>

<span data-ttu-id="03ffb-110">С помощью мини-приложения "Представление списка" вы можете отображать данные в списке SharePoint подобно тому, как это делается с помощью обычного мини-приложения "Представление списка", но вы можете использовать его даже в тех надстройках и на веб-сайтах, которые не размещены в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="03ffb-110">You can use the List View widget to display the data in a SharePoint list similar to the regular List View widget, but you can use it in your add-ins and websites that are not necessarily hosted in SharePoint.</span></span>

<br/>

<span data-ttu-id="03ffb-111">**Мини-приложение Desktop List View, в котором показаны данные в списке**</span><span class="sxs-lookup"><span data-stu-id="03ffb-111">**Figure 1. Desktop List View widget displaying data in a list**</span></span>

![Экспериментальный элемент управления Desktop List View на странице](../images/DesktopListView_basic.png)

<br/>

<span data-ttu-id="03ffb-p103">Вы можете указать в списке SharePoint представление, которое вы хотите использовать для отображения данных. Виджет "Представление списка" отображает столбцы и элементы в порядке, который указывает представление.</span><span class="sxs-lookup"><span data-stu-id="03ffb-p103">You can specify the view in the SharePoint list that you want to use to display the data. The List View widget displays the columns and items in the order specified by the view.</span></span>

<span data-ttu-id="03ffb-p104">Мини-приложение List View использует междоменную библиотеку для получения данных списка, поэтому передача информации происходит на уровне клиента.</span><span class="sxs-lookup"><span data-stu-id="03ffb-p104">The List View widget uses the cross-domain library to get the list data. For this reason, communication happens at the client level.</span></span>
 
> [!NOTE] 
> <span data-ttu-id="03ffb-117">Мини-приложение Desktop List View позволяет выполнять не все сценарии собственного представления списка.</span><span class="sxs-lookup"><span data-stu-id="03ffb-117">The Desktop List View widget doesn’t enable all the scenarios of the native List View.</span></span>

<span data-ttu-id="03ffb-118">В текущей версии мини-приложения не включены следующие сценарии:</span><span class="sxs-lookup"><span data-stu-id="03ffb-118">The following scenarios have not been enabled in the current version of the widget:</span></span>

- <span data-ttu-id="03ffb-119">использование виджета в схемах проверки подлинности, неподдерживаемых междоменной библиотекой;</span><span class="sxs-lookup"><span data-stu-id="03ffb-119">Use the widget on authentication schemes that aren't natively supported by the cross-domain library.</span></span>
- <span data-ttu-id="03ffb-120">использование виджета с другими источниками данных, кроме библиотек и списков SharePoint;</span><span class="sxs-lookup"><span data-stu-id="03ffb-120">Use the widget with data sources other than SharePoint lists or libraries.</span></span>
- <span data-ttu-id="03ffb-121">привязка виджета к данным;</span><span class="sxs-lookup"><span data-stu-id="03ffb-121">Data bind the widget.</span></span>
- <span data-ttu-id="03ffb-122">представления с сенсорным управлением;</span><span class="sxs-lookup"><span data-stu-id="03ffb-122">User touch-friendly views.</span></span>
- <span data-ttu-id="03ffb-123">встроенная правка пользователями;</span><span class="sxs-lookup"><span data-stu-id="03ffb-123">User inline-editing.</span></span>
- <span data-ttu-id="03ffb-124">показ информации о присутствии;</span><span class="sxs-lookup"><span data-stu-id="03ffb-124">Show presence information.</span></span>
- <span data-ttu-id="03ffb-125">настраиваемые шаблоны отрисовки;</span><span class="sxs-lookup"><span data-stu-id="03ffb-125">Provide custom rendering templates.</span></span>
- <span data-ttu-id="03ffb-p105">локальные сценарии. В данный момент виджет работает только в SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="03ffb-p105">On-premises scenarios. At this moment, the widget only works on SharePoint Online.</span></span>


## <a name="prerequisites-for-using-the-examples-in-this-article"></a><span data-ttu-id="03ffb-128">Необходимые условия для использования примеров в этой статье</span><span class="sxs-lookup"><span data-stu-id="03ffb-128">Prerequisites for using the examples in this article</span></span>

<span data-ttu-id="03ffb-129">Для выполнения примеров, описанных в этой статье, вам необходимо следующее:</span><span class="sxs-lookup"><span data-stu-id="03ffb-129">To follow the examples in this article, you need the following:</span></span>

- <span data-ttu-id="03ffb-130">Visual Studio 2013 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="03ffb-130">Visual Studio 2015 or later.</span></span>

- <span data-ttu-id="03ffb-131">Диспетчер пакетов NuGet.</span><span class="sxs-lookup"><span data-stu-id="03ffb-131">NuGet Package Manager.</span></span> <span data-ttu-id="03ffb-132">Дополнительные сведения см. в статье [Установка клиентских средств NuGet](https://docs.microsoft.com/ru-RU/nuget/guides/install-nuget).</span><span class="sxs-lookup"><span data-stu-id="03ffb-132">For more information, see  [Installing NuGet client tools](https://docs.microsoft.com/ru-RU/nuget/guides/install-nuget).</span></span>
    
- <span data-ttu-id="03ffb-133">Среда разработки SharePoint (для локальных сценариев требуется изоляция приложений).</span><span class="sxs-lookup"><span data-stu-id="03ffb-133">A SharePoint development environment (app isolation required for on-premises scenarios).</span></span> 
    
- <span data-ttu-id="03ffb-134">Пакет NuGet "Экспериментальные мини-приложения Office для веб-страниц".</span><span class="sxs-lookup"><span data-stu-id="03ffb-134">Office Web Widgets - Experimental NuGet gallery page</span></span> <span data-ttu-id="03ffb-135">Дополнительные сведения об установке пакетов NuGet см. в статье [Пользовательский интерфейс диспетчера пакетов NuGet](https://docs.microsoft.com/ru-RU/nuget/tools/package-manager-ui).</span><span class="sxs-lookup"><span data-stu-id="03ffb-135">For more information about how to install a NuGet package, see [NuGet Package Manager UI](https://docs.microsoft.com/ru-RU/nuget/tools/package-manager-ui).</span></span> <span data-ttu-id="03ffb-136">Вы также можете просмотреть [страницу коллекции NuGet](https://www.nuget.org/packages/Microsoft.Office.WebWidgets.Experimental/).</span><span class="sxs-lookup"><span data-stu-id="03ffb-136">You can also browse the [NuGet gallery page](https://www.nuget.org/packages/Microsoft.Office.WebWidgets.Experimental/).</span></span>
    
## <a name="use-the-desktop-list-view-widget-in-a-provider-hosted-sharepoint-add-in"></a><span data-ttu-id="03ffb-137">Использование мини-приложения Desktop List View в надстройке SharePoint с размещением у поставщика</span><span class="sxs-lookup"><span data-stu-id="03ffb-137">Use the Desktop List View widget in a provider-hosted SharePoint Add-in</span></span>

<span data-ttu-id="03ffb-138">В этом примере показана простая страница, размещенная вне SharePoint, которая объявляет мини-приложение Desktop List View.</span><span class="sxs-lookup"><span data-stu-id="03ffb-138">In this example, there is a simple page hosted outside of SharePoint that declares a Desktop List View widget.</span></span>

<span data-ttu-id="03ffb-139">Чтобы использовать мини-приложение Desktop List View:</span><span class="sxs-lookup"><span data-stu-id="03ffb-139">To use the List View widget, you must do the following:</span></span>

- <span data-ttu-id="03ffb-140">Создайте надстройку SharePoint и веб-проекты.</span><span class="sxs-lookup"><span data-stu-id="03ffb-140">Create SharePoint Add-in and web projects.</span></span>
    
- <span data-ttu-id="03ffb-p108">Создайте список на сайте надстройки. Этот шаг также гарантирует создание сайта надстройки при ее развертывании.</span><span class="sxs-lookup"><span data-stu-id="03ffb-p108">Create a list on the add-in web. This step also ensures that an add-in web is created when users deploy the add-in.</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="03ffb-143">Междоменная библиотека требует наличия сайта надстройки.</span><span class="sxs-lookup"><span data-stu-id="03ffb-143">Note The cross-domain library requires the existence of an add-in web. The List View widget communicates with SharePoint by using the cross-domain library.</span></span> <span data-ttu-id="03ffb-144">Мини-приложение List View связывается с SharePoint с помощью междоменной библиотеки.</span><span class="sxs-lookup"><span data-stu-id="03ffb-144">Note  The cross-domain library requires the existence of an add-in web. The List View widget communicates with SharePoint by using the cross-domain library.</span></span>

- <span data-ttu-id="03ffb-145">Создайте страницу надстройки, которая объявляет экземпляр мини-приложения List View, используя разметку HTML.</span><span class="sxs-lookup"><span data-stu-id="03ffb-145">Create an add-in page that declares a List View widget instance using HTML markup.</span></span>

### <a name="to-create-a-sharepoint-add-in-and-web-projects"></a><span data-ttu-id="03ffb-146">Создание надстройки SharePoint и веб-проектов</span><span class="sxs-lookup"><span data-stu-id="03ffb-146">To create a SharePoint Add-in and web projects</span></span>

1. <span data-ttu-id="03ffb-147">Откройте Visual Studio от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="03ffb-147">Open Visual Studio 2015 as administrator.</span></span> <span data-ttu-id="03ffb-148">(Для этого выберите значок Visual Studio в меню **Пуск** и пункт **Запуск от имени администратора**.)</span><span class="sxs-lookup"><span data-stu-id="03ffb-148">(To do this, right-click the Visual Studio 2015 icon on the **Start** menu, and select **Run as administrator**.)</span></span>

2. <span data-ttu-id="03ffb-149">Создайте проект, используя шаблон **Надстройка SharePoint**.</span><span class="sxs-lookup"><span data-stu-id="03ffb-149">Create a new project by using the **SharePoint Add-in** template.</span></span> <span data-ttu-id="03ffb-150">Шаблон "Надстройка SharePoint" находится в разделе **Шаблоны** > **Visual C#** > **Office/SharePoint** > **Надстройки**.</span><span class="sxs-lookup"><span data-stu-id="03ffb-150">The SharePoint Add-in template is located under **Templates** > **Visual C#** > **Office/SharePoint** > **Add-ins**.</span></span>

3. <span data-ttu-id="03ffb-151">Укажите URL-адрес веб-сайта SharePoint, который вы хотите использовать для отладки.</span><span class="sxs-lookup"><span data-stu-id="03ffb-151">Provide the SharePoint website URL that you want to use for debugging.</span></span>

4. <span data-ttu-id="03ffb-152">Выберите для надстройки вариант размещения **Размещено у поставщика**.</span><span class="sxs-lookup"><span data-stu-id="03ffb-152">Select **Provider-hosted** as the hosting option for your add-in.</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="03ffb-153">Вы также можете использовать мини-приложение Desktop List View с другими вариантами размещения или даже с надстройками Office или собственным веб-сайтом.</span><span class="sxs-lookup"><span data-stu-id="03ffb-153">Note You can also use the Desktop List View widget with other hosting options or even with Office Add-ins or your own website.</span></span>

5. <span data-ttu-id="03ffb-154">Выберите **Приложение веб-форм ASP.NET** в качестве типа проекта веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="03ffb-154">Select **ASP.NET Web Forms Application** as the type of web application project.</span></span>
 
6. <span data-ttu-id="03ffb-155">Выберите **службу контроля доступа Windows Azure** в качестве способа проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="03ffb-155">Select **Windows Azure Access Control Service** as the authentication option.</span></span>
    
 

### <a name="to-create-a-list-on-the-add-in-web"></a><span data-ttu-id="03ffb-156">Создание списка на сайте надстройки</span><span class="sxs-lookup"><span data-stu-id="03ffb-156">To create a list on the add-in web</span></span>

1. <span data-ttu-id="03ffb-157">Выберите проект надстройки SharePoint в **обозревателе решений**, а затем — команду **Добавить** > **Создать элемент**.</span><span class="sxs-lookup"><span data-stu-id="03ffb-157">Right-click the ChainStore project in Solution Explorer, and then select Add  New Item.</span></span>
    
2. <span data-ttu-id="03ffb-158">Выберите **Элементы Visual C#** > **Office/SharePoint** > **Список**.</span><span class="sxs-lookup"><span data-stu-id="03ffb-158">Select **Visual C# Items** > **Office/SharePoint** > **List**.</span></span> <span data-ttu-id="03ffb-159">Введите **Объявления** в текстовое поле **Имя** и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="03ffb-159">Enter **Announcements** in the **Name** text box, and then select **Add**.</span></span>
 
3. <span data-ttu-id="03ffb-160">Выберите **Создать экземпляр списка на основе существующего шаблона списка**.</span><span class="sxs-lookup"><span data-stu-id="03ffb-160">Choose  **Create a list instance based on an existing list template**.Choose the  Announcements template. Choose Finish.</span></span> <span data-ttu-id="03ffb-161">Выберите шаблон **Объявления** и нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="03ffb-161">Select the **Announcements** template, and then select **Finish**.</span></span>
    
 

### <a name="to-add-a-new-page-that-uses-the-desktop-list-view-widget"></a><span data-ttu-id="03ffb-162">Добавление новой страницы, использующей мини-приложение Desktop List View</span><span class="sxs-lookup"><span data-stu-id="03ffb-162">To add a new page that uses the Desktop List View widget</span></span>


1. <span data-ttu-id="03ffb-163">Выберите папку **Страницы** веб-проекта в **обозревателе решений**.</span><span class="sxs-lookup"><span data-stu-id="03ffb-163">Choose the **Pages** folder in the web project in **Solution Explorer**.</span></span>
    
 
2. <span data-ttu-id="03ffb-p114">Скопируйте приведенный ниже код и вставьте его в **ASPX**-файл проекта. Код выполняет следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="03ffb-p114">Copy the following code and paste it in an **ASPX** file in the project. The code performs the following tasks:</span></span>
    
    - <span data-ttu-id="03ffb-166">добавляет ссылки на необходимые библиотеки и ресурсы Office;</span><span class="sxs-lookup"><span data-stu-id="03ffb-166">Adds references to the required Office libraries and resources.</span></span>

    - <span data-ttu-id="03ffb-167">предоставляет заполнитель для виджета "Представление списка";</span><span class="sxs-lookup"><span data-stu-id="03ffb-167">Provides a placeholder for the List View widget.</span></span>

    - <span data-ttu-id="03ffb-168">инициализирует среду выполнения элементов управления;</span><span class="sxs-lookup"><span data-stu-id="03ffb-168">Initializes the controls runtime.</span></span>

    - <span data-ttu-id="03ffb-169">запускает метод **renderAll** среды выполнения для элементов управления Office.</span><span class="sxs-lookup"><span data-stu-id="03ffb-169">Runs the **renderAll** method of the Office Controls runtime.</span></span>
        
    ```HTML
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

<br/>

> [!NOTE] 
> <span data-ttu-id="03ffb-170">В приведенном выше примере кода явно указаны URL-адреса хост-сайта и сайта надстройки для инициализации среды выполнения для элементов управления Office.</span><span class="sxs-lookup"><span data-stu-id="03ffb-170">The code example above explicitly specifies the host web and add-in web URLs to initialize the Office controls runtime.</span></span> <span data-ttu-id="03ffb-171">Однако если URL-адреса хост-сайта и сайта надстройки указаны в параметрах строки запроса **SPAppWebUrl** и **SPHostUrl** соответственно, то вы можете передать пустой объект, и код попытается получить параметры автоматически.</span><span class="sxs-lookup"><span data-stu-id="03ffb-171">Note  The code example above explicitly specifies the host web and add-in web URLs to initialize the Office controls runtime. However, if the add-in web and host web URLs are specified in the  **SPAppWebUrl** and **SPHostUrl** query string parameters, respectively; you can pass an empty object and the code will attempt to get the parameters automatically. The SPAppWebUrl and SPHostUrl parameters are included in the query string when you use the {StandardTokens} token.</span></span> <span data-ttu-id="03ffb-172">Параметры **SPAppWebUrl** и **SPHostUrl** включаются в строку запроса при использовании маркера **{StandardTokens}**.</span><span class="sxs-lookup"><span data-stu-id="03ffb-172">The **SPAppWebUrl** and **SPHostUrl** parameters are included in the query string when you use the **{StandardTokens}** token.</span></span>
 
<br/>

<span data-ttu-id="03ffb-173">В следующем примере показано, как передавать пустой объект в метод инициализации.</span><span class="sxs-lookup"><span data-stu-id="03ffb-173">The following example shows you how to pass an empty object to the initialize method:</span></span>

```
// Initialize with an empty object and the code 
// will attempt to get the tokens from the
// query string directly.
Office.Controls.Runtime.initialize({});
```

<br/>

### <a name="to-build-and-run-the-solution"></a><span data-ttu-id="03ffb-174">Сборка и запуск решения</span><span class="sxs-lookup"><span data-stu-id="03ffb-174">To build and run the solution</span></span>


1. <span data-ttu-id="03ffb-175">Нажмите клавишу F5.</span><span class="sxs-lookup"><span data-stu-id="03ffb-175">Select the F5 key.</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="03ffb-176">При нажатии клавиши F5 Visual Studio выполняет сборку решения, развертывает надстройку и открывает страницу разрешений.</span><span class="sxs-lookup"><span data-stu-id="03ffb-176">Note  When you press F5, Visual Studio builds the solution, deploys the add-in, and opens the permissions page for the add-in.</span></span>

2. <span data-ttu-id="03ffb-177">Нажмите кнопку **Доверять**.</span><span class="sxs-lookup"><span data-stu-id="03ffb-177">Select the **Trust It** button.</span></span>
    
3. <span data-ttu-id="03ffb-178">Выберите значок надстройки на странице **Содержимое сайта**.</span><span class="sxs-lookup"><span data-stu-id="03ffb-178">Choose the add-in icon on the  **Site Contents** page.</span></span>
    
<span data-ttu-id="03ffb-179">Чтобы скачать этот пример из коллекции кода, см. пример кода [Использование экспериментального мини-приложения Desktop List View в надстройке](https://code.msdn.microsoft.com/office/sharepoint-2013-use-the-c3edb076).</span><span class="sxs-lookup"><span data-stu-id="03ffb-179">You can also download this sample from code gallery, see the  [Use the Desktop List View experimental widget in an add-in](https://code.msdn.microsoft.com/office/sharepoint-2013-use-the-c3edb076) code sample.</span></span>
 
## <a name="next-steps"></a><span data-ttu-id="03ffb-180">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="03ffb-180">Next steps</span></span>

<span data-ttu-id="03ffb-p116">В этой статье показано, как использовать мини-приложение "Представление списка на рабочем столе" в своей надстройке с помощью HTML. Вы также можете ознакомиться со следующими сценариями и сведениями о мини-приложении.</span><span class="sxs-lookup"><span data-stu-id="03ffb-p116">This article shows how to use the Desktop List View widget in your add-in by using HTML. You can also explore the following scenarios and details about the widget.</span></span>

### <a name="use-javascript-to-declare-the-desktop-list-view-widget"></a><span data-ttu-id="03ffb-183">Использование JavaScript для объявления мини-приложения Desktop List View</span><span class="sxs-lookup"><span data-stu-id="03ffb-183">Use JavaScript to declare the Desktop List View widget</span></span>

<span data-ttu-id="03ffb-184">Для объявления мини-приложения можно использовать JavaScript, а не HTML.</span><span class="sxs-lookup"><span data-stu-id="03ffb-184">Depending on your preference, you might want to use the JavaScript instead of HTML to declare the widget. If this is the case you can use the following markup as the placeholder for the widget.</span></span> <span data-ttu-id="03ffb-185">В этом случае в качестве заполнителя для мини-приложения можно использовать следующую разметку:</span><span class="sxs-lookup"><span data-stu-id="03ffb-185">Depending on your preference, you might want to use the JavaScript instead of HTML to declare the widget. If this is the case you can use the following markup as the placeholder for the widget.</span></span>

```HTML
<div id="ListViewDiv"></div>
```

<br/>

<span data-ttu-id="03ffb-186">Для создания экземпляра List View используйте следующий код JavaScript:</span><span class="sxs-lookup"><span data-stu-id="03ffb-186">Use the following JavaScript code to instantiate the List View.</span></span>

```js
new Office.Controls.ListView(
    document.getElementById("ListViewDiv"), {
        listUrl: Office.Samples.ListViewBasic.appWebUrl + "/_api/web/lists/getbytitle('Announcements')"
    });
```

<br/>

<span data-ttu-id="03ffb-187">Пример выполнения задач см. на странице **JSSimple.html** в примере кода [Использование экспериментального мини-приложения "Представление списка на рабочем столе" в надстройке](https://code.msdn.microsoft.com/office/sharepoint-2013-use-the-c3edb076).</span><span class="sxs-lookup"><span data-stu-id="03ffb-187">For an example that shows how to perform the tasks, see the **JSSimple.html** page in the [Use the Desktop List View experimental widget in an add-in](https://code.msdn.microsoft.com/office/sharepoint-2013-use-the-c3edb076) code sample.</span></span>

### <a name="specify-a-view-to-display-the-data"></a><span data-ttu-id="03ffb-188">Указание представления для отображения данных</span><span class="sxs-lookup"><span data-stu-id="03ffb-188">Specify a view to display the data</span></span>

<span data-ttu-id="03ffb-189">Мини-приложение List View показывает данные, используя спецификацию представления в списке SharePoint.</span><span class="sxs-lookup"><span data-stu-id="03ffb-189">You can specify an existent view in your SharePoint list, the List View widget displays the data using the view specification.</span></span>

<span data-ttu-id="03ffb-190">Если вы объявляете мини-приложение, используя разметки HTML, вы можете использовать следующий синтаксис для указания представления.</span><span class="sxs-lookup"><span data-stu-id="03ffb-190">If you're using HTML markup to declare the widget, you can use the following syntax to specify a view.</span></span>

```HTML
<div id="ListViewDiv"
        data-office-control="Office.Controls.ListView"
        data-office-options="{listUrl: 'list URL',
                            viewID: 'GUID'
                            }">
</div> 

```

<br/>

<span data-ttu-id="03ffb-191">Если вы объявляете мини-приложение, используя JavaScript, используйте следующий синтаксис для указания представления.</span><span class="sxs-lookup"><span data-stu-id="03ffb-191">If you're declaring the widget using JavaScript, use the following syntax to specify a view.</span></span>

```js
new Office.Controls.ListView(
    document.getElementById("ListViewDiv"), {
        listUrl: "list URL",
        viewID: "GUID"
    });
```

<br/>

<span data-ttu-id="03ffb-192">Вы можете использовать экспериментальную версию мини-приложения Desktop List View для показа данных в списках SharePoint.</span><span class="sxs-lookup"><span data-stu-id="03ffb-192">You can use the experimental Desktop List View widget to display data in SharePoint lists. The widget displays data in read-only mode. Please provide ideas and comments in the  Office Developer Platform UserVoice site.</span></span> <span data-ttu-id="03ffb-193">Мини-приложение показывает данные в режиме только для чтения.</span><span class="sxs-lookup"><span data-stu-id="03ffb-193">The widget displays data in read-only mode.</span></span> <span data-ttu-id="03ffb-194">Свои идеи и комментарии вы можете оставить на [сайте UserVoice для разработчиков Office](http://officespdev.uservoice.com/).</span><span class="sxs-lookup"><span data-stu-id="03ffb-194">Please provide ideas and comments at the [Office Developer Platform UserVoice site](http://officespdev.uservoice.com/).</span></span>
 

## <a name="see-also"></a><span data-ttu-id="03ffb-195">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="03ffb-195">See also</span></span>
<span data-ttu-id="03ffb-196"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="03ffb-196"></span></span>

-  [<span data-ttu-id="03ffb-197">Использование экспериментального мини-приложения People Picker в надстройках SharePoint</span><span class="sxs-lookup"><span data-stu-id="03ffb-197">Use the experimental People Picker widget in SharePoint Add-ins</span></span>](use-the-experimental-people-picker-widget-in-sharepoint-add-ins.md)
-  [<span data-ttu-id="03ffb-198">Обзор экспериментальных мини-приложений Office для веб-страниц</span><span class="sxs-lookup"><span data-stu-id="03ffb-198">Office Web Widgets - Experimental overview</span></span>](office-web-widgetsexperimental-overview.md)
-  [<span data-ttu-id="03ffb-199">Создание компонентов взаимодействия с пользователем в SharePoint</span><span class="sxs-lookup"><span data-stu-id="03ffb-199">Create UX components in SharePoint</span></span>](create-ux-components-in-sharepoint.md)
 

