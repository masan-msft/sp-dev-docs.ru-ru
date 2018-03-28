---
title: Создание пользовательской страницы прокси для междоменной библиотеки в SharePoint
description: Создайте настраиваемую страницу прокси для доступа к данным в удаленной службе с веб-страницы SharePoint, используя междоменную библиотеку в SharePoint.
ms.date: 12/22/2017
ms.prod: sharepoint
ms.openlocfilehash: da07fa22d0317199da1d1688adc644f98771a47c
ms.sourcegitcommit: c57fc0e802661b0771f8b022964b6956ab4f6caf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/23/2017
---
# <a name="create-a-custom-proxy-page-for-the-cross-domain-library-in-sharepoint"></a><span data-ttu-id="01228-103">Создание настраиваемой страницы прокси для междоменной библиотеки в SharePoint</span><span class="sxs-lookup"><span data-stu-id="01228-103">Create a custom proxy page for the cross-domain library in SharePoint</span></span>

<span data-ttu-id="01228-p101">В процессе создания создании надстроек SharePoint обычно приходится использовать данные из различных источников. При этом из соображений безопасности применяются механизмы блокировки, которые препятствуют обмену данными с более чем одним доменом одновременно.</span><span class="sxs-lookup"><span data-stu-id="01228-p101">When you are building SharePoint Add-ins, you usually have to incorporate data from various sources. However, for security reasons, there are blocking mechanisms that prevent communication with more than one domain at a time.</span></span>

<span data-ttu-id="01228-p102">Вы можете использовать междоменную библиотеку для доступа к данным в удаленной надстройке, если реализуете настраиваемую прокси-страницу, размещенную в инфраструктуре удаленной надстройки. Как разработчик вы отвечаете за реализацию настраиваемой прокси-страницы и пользовательской логики, например, за механизм проверки подлинности для удаленной надстройки. Используйте междоменную библиотеку с настраиваемой прокси-страницей, если необходимо, чтобы взаимодействие происходило на уровне клиента.</span><span class="sxs-lookup"><span data-stu-id="01228-p102">You can use the cross-domain library to access data in your remote add-in if you provide a custom proxy page that is hosted in the remote add-in infrastructure. As the developer, you are responsible for implementing the custom proxy page, and have to deal with custom logic, such as the authentication mechanism to the remote add-in. Use the cross-domain library with a custom proxy page if you want the communication to occur at the client level.</span></span>
 
<span data-ttu-id="01228-109"><a name="SP15Createcustomproxypage_Prereq"> </a></span><span class="sxs-lookup"><span data-stu-id="01228-109"></span></span>

## <a name="prerequisites-for-using-the-examples-in-this-article"></a><span data-ttu-id="01228-110">Необходимые условия для использования примеров в этой статье</span><span class="sxs-lookup"><span data-stu-id="01228-110">Prerequisites for using the examples in this article</span></span>

<span data-ttu-id="01228-111">Вам необходима среда разработки, описанная в статье [Создание надстроек SharePoint, размещаемых у поставщика](get-started-creating-provider-hosted-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="01228-111">You need a development environment as explained in  [Get started creating provider-hosted SharePoint Add-ins](get-started-creating-provider-hosted-sharepoint-add-ins.md).</span></span>

### <a name="core-concepts-to-know-before-using-a-custom-proxy-page-with-sharepoint-add-ins"></a><span data-ttu-id="01228-112">Ключевые понятия, с которыми необходимо ознакомиться перед использованием настраиваемой страницы прокси вместе с надстройками SharePoint</span><span class="sxs-lookup"><span data-stu-id="01228-112">Core concepts to know before using a custom proxy page with SharePoint Add-ins</span></span>

<span data-ttu-id="01228-113">Ниже перечислены полезные статьи, в которых описано, как запрашивать данные для надстроек SharePoint из удаленного домена.</span><span class="sxs-lookup"><span data-stu-id="01228-113">The following table lists some useful articles that can help you understand the concepts involved in a cross-domain scenario for SharePoint Add-ins.</span></span>

|<span data-ttu-id="01228-114">**Название статьи**</span><span class="sxs-lookup"><span data-stu-id="01228-114">**Article title**</span></span>|<span data-ttu-id="01228-115">**Описание**</span><span class="sxs-lookup"><span data-stu-id="01228-115">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="01228-116">Надстройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="01228-116">SharePoint Add-ins</span></span>](sharepoint-add-ins.md)|<span data-ttu-id="01228-117">Сведения о новой модели надстроек в SharePoint, с помощью которой можно создавать небольшие и удобные в использовании надстройки для пользователей.</span><span class="sxs-lookup"><span data-stu-id="01228-117">Learn about the new add-in model in SharePoint that enables you to create add-ins, which are small, easy-to-use solutions for end users.</span></span>|
| [<span data-ttu-id="01228-118">Безопасный доступ к данным и клиентские объектные модели для надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="01228-118">Secure data access and client object models for SharePoint Add-ins</span></span>](secure-data-access-and-client-object-models-for-sharepoint-add-ins.md)|<span data-ttu-id="01228-119">Узнайте о параметрах доступа к данным в Надстройки SharePoint. В этой статье представлена информация об альтернативах высокого уровня при работе с данными в надстройке.</span><span class="sxs-lookup"><span data-stu-id="01228-119">Learn about data access options in SharePoint Add-ins. This topic provides guidance on the high-level alternatives you have to choose from when working with data in your add-in.</span></span>|
| [<span data-ttu-id="01228-120">Хост-сайты, сайты надстроек и компоненты SharePoint в SharePoint</span><span class="sxs-lookup"><span data-stu-id="01228-120">Host webs, add-in webs, and SharePoint components in SharePoint</span></span>](host-webs-add-in-webs-and-sharepoint-components-in-sharepoint.md)|<span data-ttu-id="01228-p103">Узнайте, в чем разница между хост-сайтами и сайтами надстроек. Узнайте, какие компоненты SharePoint можно включить в Надстройка SharePoint, какие компоненты можно развернуть на хост-сайтах, а какие на сайтах надстроек, а также узнайте, как развертывать сайты надстроек в изолированном домене.</span><span class="sxs-lookup"><span data-stu-id="01228-p103">Learn about the difference between host webs and add-in webs. Find out which SharePoint components can be included in a SharePoint Add-in, which components are deployed to the host web, which components are deployed to the add-in web, and how the add-in web is deployed in an isolated domain.</span></span>|
| [<span data-ttu-id="01228-123">Междоменная безопасность на стороне клиента</span><span class="sxs-lookup"><span data-stu-id="01228-123">Client-side Cross-domain Security</span></span>](http://msdn.microsoft.com/ru-RU/library/cc709423%28v=vs.85%29.aspx)|<span data-ttu-id="01228-124">Изучите междоменные угрозы и примеры использования, а также принципы безопасности для междоменных запросов, и оцените риски разработчиков, связанные с улучшением междоменного доступа из веб-приложений, которые запускаются в браузере.</span><span class="sxs-lookup"><span data-stu-id="01228-124">Explore cross-domain threats and use cases, and security principles for cross-origin requests, and weigh the risks for developers to enhance cross-domain access from web applications that run in the browser.</span></span>|

<span data-ttu-id="01228-125"><a name="SP15Createcustomproxypage_Codeexample"> </a></span><span class="sxs-lookup"><span data-stu-id="01228-125"></span></span>

## <a name="code-example-access-remote-data-using-a-custom-proxy-page-for-the-cross-domain-library"></a><span data-ttu-id="01228-126">Пример кода. Доступ к удаленным данным с помощью настраиваемой страницы прокси для междоменной библиотеки</span><span class="sxs-lookup"><span data-stu-id="01228-126">Code example: Access remote data using a custom proxy page for the cross-domain library</span></span>

<span data-ttu-id="01228-127">Чтобы прочесть данные из удаленной службы, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="01228-127">To read data from the remote service, you must do the following:</span></span> 

1. <span data-ttu-id="01228-128">Создайте проект надстройки для SharePoint.</span><span class="sxs-lookup"><span data-stu-id="01228-128">Create a SharePoint Add-in project.</span></span>
    
2. <span data-ttu-id="01228-129">Измените манифест надстройки, чтобы разрешить связь с удаленной надстройкой.</span><span class="sxs-lookup"><span data-stu-id="01228-129">Modify the add-in manifest to allow communication from the remote add-in.</span></span>

3. <span data-ttu-id="01228-130">Создать настраиваемую прокси-страницу и страницу контента в веб-проекте.</span><span class="sxs-lookup"><span data-stu-id="01228-130">Create the custom proxy page and a content page in the web project.</span></span>

4. <span data-ttu-id="01228-131">Создать страницу, которая использует междоменную библиотеку в проекте Надстройка SharePoint.</span><span class="sxs-lookup"><span data-stu-id="01228-131">Create a page that uses the cross-domain library in the SharePoint Add-in project.</span></span>

### <a name="to-create-the-sharepoint-add-in-project"></a><span data-ttu-id="01228-132">Создание проекта надстройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="01228-132">To create the SharePoint Add-in project</span></span>

1. <span data-ttu-id="01228-133">Откройте Visual Studio от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="01228-133">Open Visual Studio 2015 as administrator.</span></span> <span data-ttu-id="01228-134">(Для этого щелкните правой кнопкой мыши значок Visual Studio в меню **Пуск** и выберите **Запуск от имени администратора**.)</span><span class="sxs-lookup"><span data-stu-id="01228-134">(To do this, right-click the Visual Studio 2015 icon on the **Start** menu, and select **Run as administrator**.)</span></span>
    
2. <span data-ttu-id="01228-135">Создайте надстройку SharePoint с размещением у поставщика, как описано в [этой статье](get-started-creating-provider-hosted-sharepoint-add-ins.md), и назовите ее **ProxyPageApp**.</span><span class="sxs-lookup"><span data-stu-id="01228-135">Create the provider-hosted SharePoint Add-in as explained in  [Get started creating provider-hosted SharePoint Add-ins](get-started-creating-provider-hosted-sharepoint-add-ins.md) and name itProxyPageApp.</span></span> 
    
### <a name="to-edit-the-add-in-manifest-file"></a><span data-ttu-id="01228-136">Изменение файла манифеста надстройки</span><span class="sxs-lookup"><span data-stu-id="01228-136">To edit the add-in manifest file</span></span>

1. <span data-ttu-id="01228-137">В **обозревателе решений** щелкните правой кнопкой мыши файл **AppManifest.xml** и выберите **Просмотреть код**.</span><span class="sxs-lookup"><span data-stu-id="01228-137">In **Solution Explorer**, right-click the **AppManifest.xml** file, and choose **View code**.</span></span>
    
2. <span data-ttu-id="01228-138">Замените весь элемент **AppPrincipal** указанным ниже фрагментом.</span><span class="sxs-lookup"><span data-stu-id="01228-138">Replace the entire **AppPrincipal** element with the following.</span></span>
    
    ```XML
    <AppPrincipal>
        <Internal AllowedRemoteHostUrl="~remoteAppUrl"/>
    </AppPrincipal>
    ```

> [!NOTE] 
> <span data-ttu-id="01228-139">Атрибут **AllowedRemoteHostUrl** используется для указания удаленного домена.</span><span class="sxs-lookup"><span data-stu-id="01228-139">The **AllowedRemoteHostUrl** attribute is used to specify the remote domain.</span></span> <span data-ttu-id="01228-140">**~remoteAppUrl** принимает значение URL-адреса удаленной надстройки.</span><span class="sxs-lookup"><span data-stu-id="01228-140">The **~remoteAppUrl** resolves to the remote add-in URL.</span></span> <span data-ttu-id="01228-141">Дополнительные сведения о маркерах см. в статье [Изучение структуры манифеста приложения и пакета надстройки SharePoint](explore-the-app-manifest-structure-and-the-package-of-a-sharepoint-add-in.md).</span><span class="sxs-lookup"><span data-stu-id="01228-141">For more information, see [Explore the app manifest structure and the package of a SharePoint Add-in](explore-the-app-manifest-structure-and-the-package-of-a-sharepoint-add-in.md).</span></span>

### <a name="to-create-a-custom-proxy-page"></a><span data-ttu-id="01228-142">Создание настраиваемой страницы прокси</span><span class="sxs-lookup"><span data-stu-id="01228-142">To create a custom proxy page</span></span>

1. <span data-ttu-id="01228-143">После создания решения Visual Studio щелкните правой кнопкой мыши проект веб-приложения (не проект надстройки SharePoint) и выберите **Добавить** > **Новый элемент** > **Интернет** > **Веб-форма**, чтобы добавить новую веб-форму.</span><span class="sxs-lookup"><span data-stu-id="01228-143">After the Visual Studio solution has been created, right-click the web application project (not the SharePoint Add-in project) and add a new Web Form by choosing  **Add** > **New Item** > **Web** > **Web Form**. Name the form AppPartContent.aspx.</span></span> <span data-ttu-id="01228-144">Присвойте форме имя **Proxy.aspx**.</span><span class="sxs-lookup"><span data-stu-id="01228-144">Name the form **Proxy.aspx**.</span></span>
 
2. <span data-ttu-id="01228-145">В файле Proxy.aspx замените весь HTML-элемент и его дочерние элементы следующим HTML-кодом.</span><span class="sxs-lookup"><span data-stu-id="01228-145">In the Proxy.aspx file, replace the entire HTML element and its children with the following HTML code.</span></span> <span data-ttu-id="01228-146">Оставьте всю разметку над HTML-элементом без изменений.</span><span class="sxs-lookup"><span data-stu-id="01228-146">Leave all the markup above the HTML element as it is.</span></span> <span data-ttu-id="01228-147">HTML-код содержит разметку и скрипт JavaScript, который выполняет следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="01228-147">The HTML code contains markup and JavaScript that performs the following tasks:</span></span>
    
    - <span data-ttu-id="01228-148">Предоставляет заполнитель для файла междоменной библиотеки JavaScript.</span><span class="sxs-lookup"><span data-stu-id="01228-148">Provides a placeholder for the cross-domain library JavaScript file.</span></span>

    - <span data-ttu-id="01228-149">Извлекает URL-адрес сайта надстройки из источника ссылки.</span><span class="sxs-lookup"><span data-stu-id="01228-149">Extracts the add-in web URL from the referrer.</span></span>
 
    - <span data-ttu-id="01228-150">Динамически загружает файл JavaScript междоменной библиотеки в заполнитель.</span><span class="sxs-lookup"><span data-stu-id="01228-150">Dynamically loads the cross-domain library JavaScript file into the placeholder.</span></span>

    - <span data-ttu-id="01228-151">Предоставляет параметры для объекта **RequestExecutorMessageProcessor**.</span><span class="sxs-lookup"><span data-stu-id="01228-151">Provides settings for the **RequestExecutorMessageProcessor** object.</span></span>

    - <span data-ttu-id="01228-152">Инициализирует объект **RequestExecutorMessageProcessor**.</span><span class="sxs-lookup"><span data-stu-id="01228-152">Initializes the **RequestExecutorMessageProcessor** object.</span></span>

    ```HTML
    <html xmlns="http://www.w3.org/1999/xhtml">
    <head runat="server">
        <meta http-equiv="X-UA-Compatible" content="IE=8" /> 
        <title>Custom Proxy Host Page</title>
        <script 
            src="http://ajax.aspnetcdn.com/ajax/4.0/1/MicrosoftAjax.js" 
            type="text/javascript">
        </script>
        <script 
            type="text/javascript" 
            src="http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.2.min.js">
        </script>

        <!-- Script to load the cross-domain library js file -->
        <script type="text/javascript">
            var hostweburl;

            $(document).ready(function(){
                //Get the URI decoded host web URL.
                hostweburl =
                    decodeURIComponent(
                        getQueryStringParameter("SPHostUrl")
                );

                // The cross-domain js file is in a URL in the form:
                // host_web_url/_layouts/15/SP.RequestExecutor.js
                var scriptbase = hostweburl + "/_layouts/15/";

                // Load the js file 
                $.getScript(scriptbase + "SP.RequestExecutor.js", initCustomProxy);
            });

            //Function to initialize the custom proxy page
            //  must set the appropriate settings and implement
            //  proper authentication mechanism
            function initCustomProxy() {
                var settings =
                {
                    originAuthorityValidator: function (messageOriginAuthority) {
                        // This page must implement the authentication for the
                        //   remote add-in.
                        // You should validate if messageOriginAuthority is
                        //  an approved domain to receive calls from.
                        return true;
                    }
                };
                SP.RequestExecutorMessageProcessor.init(settings);
            }

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
    </head>
    <body>
        
    </body>
    </html>
    ```

<br/>

> [!IMPORTANT] 
> <span data-ttu-id="01228-153">В производственной надстройке SharePoint необходимо предоставить логику авторизации и вернуть соответствующее значение в объект **originAuthorityValidator** в параметрах.</span><span class="sxs-lookup"><span data-stu-id="01228-153">Important In a production SharePoint Add-in, you must provide the authorization logic and return the appropriate value in the **originAuthorityValidator** object in settings.</span></span>

### <a name="to-create-a-content-page"></a><span data-ttu-id="01228-154">Создание страницы содержимого</span><span class="sxs-lookup"><span data-stu-id="01228-154">To create a content page</span></span>

1. <span data-ttu-id="01228-p108">Щелкните правой кнопкой мыши проект веб-приложения в **обозревателе решений** и выберите **Добавить** > **Новый элемент** > **Интернет** > **Веб-форма**, чтобы добавить новую веб-форму. Присвойте форме имя **Content.aspx**.</span><span class="sxs-lookup"><span data-stu-id="01228-p108">Right-click the web application project in Solution Explorer and add a new Web Form by choosing Add  New Item  Web  Web Form. Name the form Content.aspx..</span></span>

2. <span data-ttu-id="01228-p109">Скопируйте указанный ниже код и вставьте его в метод **Page_Load** в файле с выделенным кодом. Этот код выполняет следующие задачи.</span><span class="sxs-lookup"><span data-stu-id="01228-p109">Copy the following code and paste it in the **Page_Load** method in the code-behind file. The code performs the following tasks:</span></span>
    
    - <span data-ttu-id="01228-159">Устанавливает для **content-type** значение **text/plain**.</span><span class="sxs-lookup"><span data-stu-id="01228-159">Sets the output **content-type** to **text/plain**.</span></span>

    - <span data-ttu-id="01228-160">Записывает контент в выходной буфер.</span><span class="sxs-lookup"><span data-stu-id="01228-160">Writes the content to the output buffer.</span></span>

    - <span data-ttu-id="01228-161">Завершает подключение.</span><span class="sxs-lookup"><span data-stu-id="01228-161">Ends the connection.</span></span>

    ```C#
    string content;
    content = "Just some text.";
    Response.ContentType="text/plain";
    Response.Write(content);
    Response.End();

    ```

<br/>

### <a name="to-create-a-sharepoint-webpage-that-uses-the-cross-domain-library"></a><span data-ttu-id="01228-162">Создание веб-страницы SharePoint, использующей междоменную библиотеку</span><span class="sxs-lookup"><span data-stu-id="01228-162">To create a SharePoint webpage that uses the cross-domain library</span></span>

1. <span data-ttu-id="01228-163">Щелкните правой кнопкой мыши проект надстройки SharePoint и выберите **Добавить** > **Новый элемент** > **Office/SharePoint** > **Модуль**.</span><span class="sxs-lookup"><span data-stu-id="01228-163">Right-click the SharePoint Add-in project, and choose  **Add** > **New Item** > **Office/SharePoint** > **Module**.</span></span>

2. <span data-ttu-id="01228-164">Присвойте модулю имя **Pages** и нажмите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="01228-164">Name the module Pages, and then choose  Add.</span></span>

3. <span data-ttu-id="01228-165">Щелкните папку Pages правой кнопкой мыши и выберите **Добавить** > **Новый элемент** > **Office/SharePoint** > **Страница**.</span><span class="sxs-lookup"><span data-stu-id="01228-165">Right-click the  Pages folder and choose Add  New Item  Office/SharePoint  Page.</span></span> 

4. <span data-ttu-id="01228-166">Задайте для страницы имя **Home.aspx** и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="01228-166">Name the page Home.aspx and then choose **Add**.</span></span>

5. <span data-ttu-id="01228-167">Если страница Home.aspx не открылась автоматически, откройте ее.</span><span class="sxs-lookup"><span data-stu-id="01228-167">Open the Home.aspx page if it isn't opened automatically.</span></span>

6. <span data-ttu-id="01228-168">Скопируйте указанный ниже код и вставьте его в тег содержимого **PlaceHolderMain**.</span><span class="sxs-lookup"><span data-stu-id="01228-168">Copy the following code and paste it in the **PlaceHolderMain** content tag.</span></span>
        
    ```js
    <!-- The page dynamically loads the cross-domain library's
        js file, rescript acts as the placeholder. -->
    <script 
        type="text/javascript"
        id="rescript"
        src="../_layouts/15/SP.RequestExecutor.js">
    </script>
        Data from the remote domain: <span id="TextData"></span>

        <!-- Main script to retrieve the host web's title -->
        <script type="text/javascript">
        (function () {
            var executor;
            var hostweburl;
            var remotedomain;

            remotedomain = "<your_remote_add-in_domain>";

            //Get the URI decoded host web URL.
            hostweburl =
                decodeURIComponent(
                    getQueryStringParameter("SPHostUrl")
            );

            // Initialize the RequestExecutor with the custom proxy URL.
            executor = new SP.RequestExecutor(remotedomain);
            executor.iFrameSourceUrl = "Proxy.aspx?SPHostUrl=" + hostweburl;

            // Issue the call against the remote endpoint.
            // The response formats the data in plain text.
            // The functions successHandler and errorHandler attend the
            //      sucess and error events respectively.
            executor.executeAsync(
                {
                    url:
                        remotedomain + "Content.aspx",
                    method: "GET",
                    headers: { "Accept": "text/plain" },
                    success: successHandler,
                    error: errorHandler
                }
            );
        })();

        // Function to handle the success event.
        // Prints the data to the placeholder.
        function successHandler(data) {
            document.getElementById("TextData").innerText =
                data.body;
        }

        // Function to handle the error event.
        // Prints the error message to the page.
        function errorHandler(data, errorCode, errorMessage) {
            document.getElementById("TextData").innerText =
                "Could not complete cross-domain call: " + errorMessage;
        }

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

    ```

    <br/>

7. <span data-ttu-id="01228-p110">В ранее вставленном вами фрагменте кода найдите строку `remotedomain = "<your_remote_add-in_domain>";` и замените заполнитель _<домен_вашей_удаленной_надстройки>_ URL-адресом "localhost", который ваше веб-приложение использует, когда вы запускаете надстройку клавишей F5 в Visual Studio. Чтобы найти это значение, выберите проект веб-приложения в **обозревателе решений**. Свойство **URL** находится на панели **Свойства**. Используйте это значение целиком, включая протокол, порт и закрывающий символ косой черты, например `http://localhost:45072`.</span><span class="sxs-lookup"><span data-stu-id="01228-p110">In the preceding code that you pasted, find the line  , and replace the placeholder  <your_remote_add-in_domain> with the "localhost" URL that your web application uses when you are running the add-in with F5 in Visual Studio. To find this value, select the web application project in Solution Explorer. The  URL property will be in the Properties pane. Use the entire value, including the protocol, the port, and the closing slash; for example "http://localhost:45072".</span></span>
    
8. <span data-ttu-id="01228-173">Сохраните и закройте файл.</span><span class="sxs-lookup"><span data-stu-id="01228-173">Save and close the file.</span></span>
    
9. <span data-ttu-id="01228-174">Откройте файл appmanifest.xml и задайте для параметра **Начальная страница** значение **ProxyPageApp/Pages/Home.aspx**.</span><span class="sxs-lookup"><span data-stu-id="01228-174">Open the appmanifest.xml file, and set the **Start page** value to **ProxyPageApp/Pages/Home.aspx**.</span></span>
    
### <a name="to-build-and-run-the-solution"></a><span data-ttu-id="01228-175">Сборка и запуск решения</span><span class="sxs-lookup"><span data-stu-id="01228-175">To build and run the solution</span></span>

1. <span data-ttu-id="01228-176">Убедитесь, что проект надстройки SharePoint выбран как запускаемый проект.</span><span class="sxs-lookup"><span data-stu-id="01228-176">Make sure that the SharePoint Add-in project is set as the startup project.</span></span>

2. <span data-ttu-id="01228-177">Нажмите клавишу F5.</span><span class="sxs-lookup"><span data-stu-id="01228-177">Select the F5 key.</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="01228-178">При нажатии клавиши F5 Visual Studio выполняет сборку решения, развертывает надстройку и открывает страницу разрешений.</span><span class="sxs-lookup"><span data-stu-id="01228-178">Note  When you press F5, Visual Studio builds the solution, deploys the add-in, and opens the permissions page for the add-in.</span></span>

3. <span data-ttu-id="01228-179">Нажмите кнопку **Доверять**.</span><span class="sxs-lookup"><span data-stu-id="01228-179">Select the **Trust It** button.</span></span>
    
    <span data-ttu-id="01228-p111">Откроется домашняя страница, которая должна выглядеть следующим образом. Может потребоваться несколько секунд, чтобы появилась фраза "Just some text", так как она извлекается со страницы Content.aspx удаленного домена.</span><span class="sxs-lookup"><span data-stu-id="01228-p111">The Home page will open and it should look like the following. It may take a few seconds for the phrase "Just some text" to appear because it is being fetched from the remote domain's Content.aspx page.</span></span>
 
    ![Страница SharePoint с данными из удаленной службы](../images/CustomProxy_result.jpg)

#### <a name="troubleshooting-the-solution"></a><span data-ttu-id="01228-183">Устранение неполадок в решении</span><span class="sxs-lookup"><span data-stu-id="01228-183">Table 2. Troubleshooting the solution</span></span>

|<span data-ttu-id="01228-184">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="01228-184">**Problem**</span></span>|<span data-ttu-id="01228-185">**Решение**</span><span class="sxs-lookup"><span data-stu-id="01228-185">**Solution**</span></span>|
|:-----|:-----|
|<span data-ttu-id="01228-186">Visual Studio не открывает браузер после нажатия клавиши F5.</span><span class="sxs-lookup"><span data-stu-id="01228-186">Visual Studio does not open the browser after you press the F5 key.</span></span>|<span data-ttu-id="01228-187">Сделайте проект надстройки SharePoint запускаемым.</span><span class="sxs-lookup"><span data-stu-id="01228-187">Set the SharePoint Add-in project as the startup project.</span></span>|
|<span data-ttu-id="01228-188">Необработанное исключение **SP не определен**.</span><span class="sxs-lookup"><span data-stu-id="01228-188">Unhandled exception **SP is undefined**.</span></span>|<span data-ttu-id="01228-189">Убедитесь, что у вас есть доступ к файлу SP.RequestExecutor.js в окне браузера.</span><span class="sxs-lookup"><span data-stu-id="01228-189">Make sure that you can access the SP.RequestExecutor.js file in a browser window.</span></span>|

## <a name="see-also"></a><span data-ttu-id="01228-190">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="01228-190">See also</span></span>
<span data-ttu-id="01228-191"><a name="SP15Createcustomproxypage_Addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="01228-191"></span></span>

- [<span data-ttu-id="01228-192">Пример кода. Получение данных с помощью страницы прокси для междоменной библиотеки</span><span class="sxs-lookup"><span data-stu-id="01228-192">Code sample: Get data by using a proxy page for the cross-domain library</span></span>](https://code.msdn.microsoft.com/SharePoint-2013-Get-data-10039ff1)
- [<span data-ttu-id="01228-193">Работа с внешними данными в SharePoint</span><span class="sxs-lookup"><span data-stu-id="01228-193">Work with external data in SharePoint</span></span>](work-with-external-data-in-sharepoint.md)

    
 

