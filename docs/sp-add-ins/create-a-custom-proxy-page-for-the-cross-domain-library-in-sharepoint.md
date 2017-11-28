---
title: "Создание пользовательской страницы прокси для междоменной библиотеки в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 78bd322c79ed6c26c5b44b11042064896274f2b7
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="create-a-custom-proxy-page-for-the-cross-domain-library-in-sharepoint"></a><span data-ttu-id="495e5-102">Создание пользовательской страницы прокси для междоменной библиотеки в SharePoint</span><span class="sxs-lookup"><span data-stu-id="495e5-102">Create a custom proxy page for the cross-domain library in SharePoint</span></span>
<span data-ttu-id="495e5-103">Узнайте, как создать пользовательскую страницу прокси для доступа к данным в удаленной службе с веб-страницы SharePoint, используя междоменную библиотеку в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="495e5-103">Learn how to create a custom proxy page to access data in a remote service from a SharePoint webpage by using the cross domain library in SharePoint.</span></span> 
 

 <span data-ttu-id="495e5-p101">**Примечание.** В настоящее время идет процесс замены названия "приложения для SharePoint" названием "надстройки SharePoint". Во время этого процесса в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio может по-прежнему использоваться термин "приложения для SharePoint". Дополнительные сведения см. в статье [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="495e5-p101">**Note**  The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see  [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span></span>
 

<span data-ttu-id="495e5-p102">В процессе создания создании надстроек SharePoint обычно приходится использовать данные из различных источников. При этом из соображений безопасности применяются механизмы блокировки, которые препятствуют обмену данными с более чем одним доменом одновременно.</span><span class="sxs-lookup"><span data-stu-id="495e5-p102">When you are building SharePoint Add-ins, you usually have to incorporate data from various sources. However, for security reasons, there are blocking mechanisms that prevent communication with more than one domain at a time.</span></span>
 

<span data-ttu-id="495e5-p103">Вы можете использовать междоменную библиотеку для доступа к данным в удаленной надстройке, если реализуете настраиваемую прокси-страницу, размещенную в инфраструктуре удаленной надстройки. Как разработчик вы отвечаете за реализацию настраиваемой прокси-страницы и пользовательской логики, например, за механизм проверки подлинности для удаленной надстройки. Используйте междоменную библиотеку с настраиваемой прокси-страницей, если необходимо, чтобы взаимодействие происходило на уровне клиента.</span><span class="sxs-lookup"><span data-stu-id="495e5-p103">You can use the cross-domain library to access data in your remote add-in if you provide a custom proxy page that is hosted in the remote add-in infrastructure. As the developer, you are responsible for implementing the custom proxy page, and have to deal with custom logic, such as the authentication mechanism to the remote add-in. Use the cross-domain library with a custom proxy page if you want the communication to occur at the client level.</span></span>
 


## <a name="prerequisites-for-using-the-examples-in-this-article"></a><span data-ttu-id="495e5-112">Компоненты, необходимые для использования примеров в этой статье</span><span class="sxs-lookup"><span data-stu-id="495e5-112">Prerequisites for using the examples in this article</span></span>
<span data-ttu-id="495e5-113"><a name="SP15Createcustomproxypage_Prereq"> </a></span><span class="sxs-lookup"><span data-stu-id="495e5-113"></span></span>

<span data-ttu-id="495e5-114">Вам необходима среда разработки, описанная в статье [Приступая к созданию надстроек SharePoint, размещаемых у поставщика](get-started-creating-provider-hosted-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="495e5-114">You need a development environment as explained in  [Get started creating provider-hosted SharePoint Add-ins](get-started-creating-provider-hosted-sharepoint-add-ins.md).</span></span>
 

 

### <a name="core-concepts-to-know-before-using-a-custom-proxy-page-with-sharepoint-add-ins"></a><span data-ttu-id="495e5-115">Основные понятия, которые необходимо знать, прежде чем использовать настраиваемые страницы прокси совместно с надстройками SharePoint</span><span class="sxs-lookup"><span data-stu-id="495e5-115">Core concepts to know before using a custom proxy page with SharePoint Add-ins</span></span>

<span data-ttu-id="495e5-116">В таблице ниже перечислены полезные статьи, с помощью которых вам будет проще разобраться с понятиями, используемыми в междоменных сценариях для надстроек SharePoint.</span><span class="sxs-lookup"><span data-stu-id="495e5-116">The following table lists some useful articles that can help you understand the concepts involved in a cross-domain scenario for SharePoint Add-ins.</span></span>
 

 

<span data-ttu-id="495e5-117">**Табл. 1. Основные понятия, необходимые для использования настраиваемой страницы прокси**</span><span class="sxs-lookup"><span data-stu-id="495e5-117">**Table 1. Core concepts for using a custom proxy page**</span></span>


|<span data-ttu-id="495e5-118">**Название статьи**</span><span class="sxs-lookup"><span data-stu-id="495e5-118">**Article title**</span></span>|<span data-ttu-id="495e5-119">**Описание**</span><span class="sxs-lookup"><span data-stu-id="495e5-119">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="495e5-120">Надстройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="495e5-120">SharePoint Add-ins</span></span>](sharepoint-add-ins.md)|<span data-ttu-id="495e5-121">Сведения о новой модели надстроек в SharePoint, с помощью которой можно создавать небольшие и удобные в использовании надстройки для пользователей.</span><span class="sxs-lookup"><span data-stu-id="495e5-121">Learn about the new add-in model in SharePoint that enables you to create add-ins, which are small, easy-to-use solutions for end users.</span></span>|
| [<span data-ttu-id="495e5-122">Безопасный доступ к данным и клиентские объектные модели для надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="495e5-122">Secure data access and client object models for SharePoint Add-ins</span></span>](secure-data-access-and-client-object-models-for-sharepoint-add-ins.md)|<span data-ttu-id="495e5-123">Узнайте о параметрах доступа к данным в Надстройки SharePoint. В этой статье представлена информация об альтернативах высокого уровня при работе с данными в надстройке.</span><span class="sxs-lookup"><span data-stu-id="495e5-123">Learn about data access options in SharePoint Add-ins. This topic provides guidance on the high-level alternatives you have to choose from when working with data in your add-in.</span></span>|
| [<span data-ttu-id="495e5-124">Хост-сайты, сайты надстроек и компоненты SharePoint в SharePoint</span><span class="sxs-lookup"><span data-stu-id="495e5-124">Host webs, add-in webs, and SharePoint components in SharePoint</span></span>](host-webs-add-in-webs-and-sharepoint-components-in-sharepoint.md)|<span data-ttu-id="495e5-p104">Узнайте, в чем разница между хост-сайтами и сайтами надстроек. Узнайте, какие компоненты SharePoint можно включить в Надстройка SharePoint, какие компоненты можно развернуть на хост-сайтах, а какие на сайтах надстроек, а также узнайте, как развертывать сайты надстроек в изолированном домене.</span><span class="sxs-lookup"><span data-stu-id="495e5-p104">Learn about the difference between host webs and add-in webs. Find out which SharePoint components can be included in a SharePoint Add-in, which components are deployed to the host web, which components are deployed to the add-in web, and how the add-in web is deployed in an isolated domain.</span></span>|
| [<span data-ttu-id="495e5-127">Междоменная безопасность на стороне клиента</span><span class="sxs-lookup"><span data-stu-id="495e5-127">Client-side Cross-domain Security</span></span>](http://msdn.microsoft.com/ru-RU/library/cc709423%28v=vs.85%29.aspx)|<span data-ttu-id="495e5-128">Изучите междоменные угрозы и примеры использования, а также принципы безопасности для междоменных запросов, и оцените риски разработчиков, связанные с улучшением междоменного доступа из веб-приложений, которые запускаются в браузере.</span><span class="sxs-lookup"><span data-stu-id="495e5-128">Explore cross-domain threats and use cases, and security principles for cross-origin requests, and weigh the risks for developers to enhance cross-domain access from web applications that run in the browser.</span></span>|

## <a name="code-example-access-remote-data-using-a-custom-proxy-page-for-the-cross-domain-library"></a><span data-ttu-id="495e5-129">Пример кода: доступ к удаленным данным с помощью настраиваемой страницы прокси для междоменной библиотеки</span><span class="sxs-lookup"><span data-stu-id="495e5-129">Code example: Access remote data using a custom proxy page for the cross-domain library</span></span>
<span data-ttu-id="495e5-130"><a name="SP15Createcustomproxypage_Codeexample"> </a></span><span class="sxs-lookup"><span data-stu-id="495e5-130"></span></span>

<span data-ttu-id="495e5-131">Чтобы прочесть данные из удаленной службы, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="495e5-131">To read data from the remote service, you must do the following:</span></span> 
 

 

1. <span data-ttu-id="495e5-132">Создайте проект надстройки для SharePoint.</span><span class="sxs-lookup"><span data-stu-id="495e5-132">Create a SharePoint Add-in project.</span></span>
    
 
2. <span data-ttu-id="495e5-133">Измените манифест надстройки, чтобы разрешить связь с удаленной надстройкой.</span><span class="sxs-lookup"><span data-stu-id="495e5-133">Modify the add-in manifest to allow communication from the remote add-in.</span></span>
    
 
3. <span data-ttu-id="495e5-134">Создать настраиваемую прокси-страницу и страницу контента в веб-проекте.</span><span class="sxs-lookup"><span data-stu-id="495e5-134">Create the custom proxy page and a content page in the web project.</span></span>
    
 
4. <span data-ttu-id="495e5-135">Создать страницу, которая использует междоменную библиотеку в проекте Надстройка SharePoint.</span><span class="sxs-lookup"><span data-stu-id="495e5-135">Create a page that uses the cross-domain library in the SharePoint Add-in project.</span></span>
    
 

### <a name="to-create-the-sharepoint-add-in-project"></a><span data-ttu-id="495e5-136">Создание проекта надстройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="495e5-136">To create the SharePoint Add-in project</span></span>


1. <span data-ttu-id="495e5-p105">Откройте Visual Studio от имени администратора. (Для этого щелкните правой кнопкой мыши значок Visual Studio в меню **Пуск** и выберите пункт **Запуск от имени администратора**.)</span><span class="sxs-lookup"><span data-stu-id="495e5-p105">Open Visual Studio as administrator. (To do this, right-click the Visual Studio icon on the  **Start** menu, and choose **Run as administrator**.)</span></span>
    
 
2. <span data-ttu-id="495e5-139">Создайте надстройку SharePoint, размещаемую у поставщика, как описано в статье [Приступая к созданию надстроек SharePoint, размещаемых у поставщика](get-started-creating-provider-hosted-sharepoint-add-ins.md), и назовите ее ProxyPageApp.</span><span class="sxs-lookup"><span data-stu-id="495e5-139">Create the provider-hosted SharePoint Add-in as explained in  [Get started creating provider-hosted SharePoint Add-ins](get-started-creating-provider-hosted-sharepoint-add-ins.md) and name itProxyPageApp.</span></span> 
    
 

### <a name="to-edit-the-add-in-manifest-file"></a><span data-ttu-id="495e5-140">Изменение файла манифеста надстройки</span><span class="sxs-lookup"><span data-stu-id="495e5-140">To edit the add-in manifest file</span></span>


1. <span data-ttu-id="495e5-141">В **обозревателе решений** щелкните правой кнопкой мыши файл **AppManifest.xml** и выберите пункт **Просмотреть код**.</span><span class="sxs-lookup"><span data-stu-id="495e5-141">In  **Solution Explorer**, right-click the  **AppManifest.xml** file, and choose **View code**.</span></span>
    
 
2. <span data-ttu-id="495e5-142">Замените весь элемент **AppPrincipal** указанным ниже фрагментом.</span><span class="sxs-lookup"><span data-stu-id="495e5-142">Replace the entire  **AppPrincipal** element with the following.</span></span>
    
```XML
  <AppPrincipal>
    <Internal AllowedRemoteHostUrl="~remoteAppUrl"/>
</AppPrincipal>
```


     **Note**  The  **AllowedRemoteHostUrl** attribute is used to specify the remote domain. The **~remoteAppUrl** resolves to the remote add-in URL. For more information about tokens, see [Explore the app manifest structure and the package of a SharePoint Add-in](explore-the-app-manifest-structure-and-the-package-of-a-sharepoint-add-in.md).

### <a name="to-create-a-custom-proxy-page"></a><span data-ttu-id="495e5-143">Создание настраиваемой страницы прокси</span><span class="sxs-lookup"><span data-stu-id="495e5-143">To create a custom proxy page</span></span>


1. <span data-ttu-id="495e5-p106">После создания решения Visual Studio щелкните правой кнопкой мыши проект веб-приложения (но не проект надстройки SharePoint) и добавьте новую веб-форму, последовательно выбрав пункты **Добавить** > **Новый элемент** > **Интернет** > **Веб-форма**. Присвойте форме имя Proxy.aspx.</span><span class="sxs-lookup"><span data-stu-id="495e5-p106">After the Visual Studio solution has been created, right-click the web application project (not the SharePoint Add-in project) and add a new Web Form by choosing  **Add** > **New Item** > **Web** > **Web Form**. Name the form Proxy.aspx.</span></span>
    
 
2. <span data-ttu-id="495e5-p107">В файле Proxy.aspx замените весь HTML-элемент и его дочерние элементы на следующий код HTML. Оставьте всю разметку над HTML-элементом без изменений. Код HTML содержит разметку и скрипт JavaScript, который выполняет следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="495e5-p107">In the Proxy.aspx file, replace the entire html element and it's children with the following HTML code. Leave all the markup above the html element as it is. The HTML code contains markup and JavaScript that performs the following tasks:</span></span>
    
      - <span data-ttu-id="495e5-149">Предоставляет заполнитель для файл междоменной библиотеки JavaScript.</span><span class="sxs-lookup"><span data-stu-id="495e5-149">Provides a placeholder for the cross-domain library JavaScript file.</span></span>
    
 
  - <span data-ttu-id="495e5-150">Извлекает URL-адрес сайта надстройки из источника ссылки.</span><span class="sxs-lookup"><span data-stu-id="495e5-150">Extracts the add-in web URL from the referrer.</span></span>
    
 
  - <span data-ttu-id="495e5-151">Динамически загружает файл JavaScript междоменной библиотеки в заполнитель.</span><span class="sxs-lookup"><span data-stu-id="495e5-151">Dynamically loads the cross-domain library JavaScript file into the placeholder.</span></span>
    
 
  - <span data-ttu-id="495e5-152">Предоставляет параметры для объекта **RequestExecutorMessageProcessor**.</span><span class="sxs-lookup"><span data-stu-id="495e5-152">Provides settings for the  **RequestExecutorMessageProcessor** object.</span></span>
    
 
  - <span data-ttu-id="495e5-153">Инициализирует объект **RequestExecutorMessageProcessor**.</span><span class="sxs-lookup"><span data-stu-id="495e5-153">Initializes the  **RequestExecutorMessageProcessor** object.</span></span>
    
 

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


     **Important**  In a production SharePoint Add-in, you must provide the authorization logic and return the appropriate value in the  **originAuthorityValidator** object in settings.

### <a name="to-create-a-content-page"></a><span data-ttu-id="495e5-154">Создание страницы содержимого</span><span class="sxs-lookup"><span data-stu-id="495e5-154">To create a content page</span></span>


1. <span data-ttu-id="495e5-p108">Щелкните правой кнопкой мыши проект веб-приложения в **обозревателе решений** и добавьте новую веб-форму, последовательно выбрав пункты **Добавить** > **Новый элемент** > **Интернет** > **Веб-форма**. Присвойте форме имя Content.aspx.</span><span class="sxs-lookup"><span data-stu-id="495e5-p108">Right-click the web application project in  **Solution Explorer** and add a new Web Form by choosing **Add** > **New Item** > **Web** > **Web Form**. Name the form Content.aspx..</span></span>
    
 
2. <span data-ttu-id="495e5-p109">Скопируйте указанный ниже код и вставьте его в метод **Page_Load** в файле с выделенным кодом. Этот код выполняет указанные ниже задачи.</span><span class="sxs-lookup"><span data-stu-id="495e5-p109">Copy the following code and paste it in the  **Page_Load** method in the code-behind file. The code performs the following tasks:</span></span>
    
      - <span data-ttu-id="495e5-159">Задает в качестве выходного **типа контента** **текст или обычный текст**.</span><span class="sxs-lookup"><span data-stu-id="495e5-159">Sets the output  **content-type** to **text/plain**.</span></span>
    
 
  - <span data-ttu-id="495e5-160">Записывает контент в выходной буфер.</span><span class="sxs-lookup"><span data-stu-id="495e5-160">Writes the content to the output buffer.</span></span>
    
 
  - <span data-ttu-id="495e5-161">Завершает подключение.</span><span class="sxs-lookup"><span data-stu-id="495e5-161">Ends the connection.</span></span>
    
 

```C#
  string content;
content = "Just some text.";
Response.ContentType="text/plain";
Response.Write(content);
Response.End();

```


### <a name="to-create-a-sharepoint-webpage-that-uses-the-cross-domain-library"></a><span data-ttu-id="495e5-162">Создание веб-страницы SharePoint, использующей междоменную библиотеку</span><span class="sxs-lookup"><span data-stu-id="495e5-162">To create a SharePoint webpage that uses the cross-domain library</span></span>


1. <span data-ttu-id="495e5-163">Щелкните правой кнопкой мыши проект надстройки SharePoint и последовательно выберите пункты **Добавить** > **Новый элемент** > **Office и SharePoint** > **Модуль**.</span><span class="sxs-lookup"><span data-stu-id="495e5-163">Right-click the SharePoint Add-in project, and choose  **Add** > **New Item** > **Office/SharePoint** > **Module**.</span></span>
    
 
2. <span data-ttu-id="495e5-164">Присвойте модулю имя Pages и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="495e5-164">Name the module Pages, and then choose  **Add**.</span></span>
    
 
3. <span data-ttu-id="495e5-165">Щелкните папку **Pages** правой кнопкой мыши и последовательно выберите пункты **Добавить** > **Новый элемент**>  **Office и SharePoint** > **Страница**.</span><span class="sxs-lookup"><span data-stu-id="495e5-165">Right-click the  **Pages** folder and choose **Add** > **New Item**>  **Office/SharePoint** > **Page**.</span></span> 
    
 
4. <span data-ttu-id="495e5-166">Задайте для страницы имя Home.aspx и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="495e5-166">Name the page Home.aspx and then choose **Add**.</span></span>
    
 
5. <span data-ttu-id="495e5-167">Если страница **Home.aspx** не открылась автоматически, откройте ее.</span><span class="sxs-lookup"><span data-stu-id="495e5-167">Open the  **Home.aspx** page if it isn't opened automatically.</span></span>
    
 
6. <span data-ttu-id="495e5-168">Скопируйте указанный ниже код и вставьте его в тег контента **PlaceHolderMain**.</span><span class="sxs-lookup"><span data-stu-id="495e5-168">Copy the following code and paste it in the  **PlaceHolderMain** content tag.</span></span>
    
```
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

7. <span data-ttu-id="495e5-p110">В ранее вставленном вами фрагменте кода найдите строку `remotedomain = "<your_remote_add-in_domain>";` и замените заполнитель _<домен_вашей_удаленной_надстройки>_ URL-адресом localhost, который ваше веб-приложение использует, когда вы запускаете надстройку клавишей F5 в Visual Studio. Чтобы найти это значение, выберите проект веб-приложения в **обозревателе решений**. Свойство **URL** находится в области **Свойства**. Используйте это значение целиком, включая протокол, порт и закрывающий символ косой черты, например http://localhost:45072.</span><span class="sxs-lookup"><span data-stu-id="495e5-p110">In the preceding code that you pasted, find the line  `remotedomain = "<your_remote_add-in_domain>";`, and replace the placeholder  _<your_remote_add-in_domain>_ with the "localhost" URL that your web application uses when you are running the add-in with F5 in Visual Studio. To find this value, select the web application project in **Solution Explorer**. The  **URL** property will be in the **Properties** pane. Use the entire value, including the protocol, the port, and the closing slash; for example "http://localhost:45072".</span></span>
    
 
8. <span data-ttu-id="495e5-173">Сохраните и закройте файл.</span><span class="sxs-lookup"><span data-stu-id="495e5-173">Save and close the file.</span></span>
    
 
9. <span data-ttu-id="495e5-174">Откройте файл appmanifest.xml и задайте для параметра **Start page** (Начальная страница) значение **ProxyPageApp/Pages/Home.aspx**.</span><span class="sxs-lookup"><span data-stu-id="495e5-174">Open the appmanifest.xml file, and set the  **Start page** value to **ProxyPageApp/Pages/Home.aspx**.</span></span>
    
 

### <a name="to-build-and-run-the-solution"></a><span data-ttu-id="495e5-175">Сборка и запуск решения</span><span class="sxs-lookup"><span data-stu-id="495e5-175">To build and run the solution</span></span>


1. <span data-ttu-id="495e5-176">Убедитесь, что проект Надстройка SharePoint выбран как запускаемый проект.</span><span class="sxs-lookup"><span data-stu-id="495e5-176">Make sure that the SharePoint Add-in project is set as the startup project.</span></span>
    
 
2. <span data-ttu-id="495e5-177">Нажмите клавишу F5.</span><span class="sxs-lookup"><span data-stu-id="495e5-177">Press the F5 key.</span></span>
    
     <span data-ttu-id="495e5-178">**Примечание.** При нажатии клавиши F5 Visual Studio выполняет сборку решения, развертывает надстройку и открывает для нее страницу разрешений.</span><span class="sxs-lookup"><span data-stu-id="495e5-178">**Note**  When you press F5, Visual Studio builds the solution, deploys the add-in, and opens the permissions page for the add-in.</span></span>
3. <span data-ttu-id="495e5-179">Нажмите кнопку **Доверять**.</span><span class="sxs-lookup"><span data-stu-id="495e5-179">Choose the  **Trust It** button.</span></span>
    
    <span data-ttu-id="495e5-p111">Откроется домашняя страница, которая должна выглядеть следующим образом. Может потребоваться несколько секунд, чтобы появилась фраза "Just some text", так как она извлекается со страницы Content.aspx удаленного домена.</span><span class="sxs-lookup"><span data-stu-id="495e5-p111">The Home page will open and it should look like the following. It may take a few seconds for the phrase "Just some text" to appear because it is being fetched from the remote domain's Content.aspx page.</span></span>
    

    <span data-ttu-id="495e5-182">**Данные из удаленной службы на веб-странице SharePoint**</span><span class="sxs-lookup"><span data-stu-id="495e5-182">**Data from the remote service in a SharePoint webpage**</span></span>

 

  ![Страница SharePoint с данными из удаленной службы](../images/CustomProxy_result.jpg)
 

 

 

<span data-ttu-id="495e5-184">**Табл. 2. Поиск и устранение неполадок в решении**</span><span class="sxs-lookup"><span data-stu-id="495e5-184">**Table 2. Troubleshooting the solution**</span></span>


|<span data-ttu-id="495e5-185">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="495e5-185">**Problem**</span></span>|<span data-ttu-id="495e5-186">**Решение**</span><span class="sxs-lookup"><span data-stu-id="495e5-186">**Solution**</span></span>|
|:-----|:-----|
|<span data-ttu-id="495e5-187">Visual Studio не открывает браузер после нажатия клавиши F5.</span><span class="sxs-lookup"><span data-stu-id="495e5-187">Visual Studio does not open the browser after you press the F5 key.</span></span>|<span data-ttu-id="495e5-188">Настройте проект надстройки SharePoint в качестве запускаемого проекта.</span><span class="sxs-lookup"><span data-stu-id="495e5-188">Set the SharePoint Add-in project as the startup project.</span></span>|
|<span data-ttu-id="495e5-189">Необработанное исключение **Не определен указатель стека**.</span><span class="sxs-lookup"><span data-stu-id="495e5-189">Unhandled exception  **SP is undefined**.</span></span>|<span data-ttu-id="495e5-190">Убедитесь, что у вас есть доступ к файлу SP.RequestExecutor.js в окне браузера.</span><span class="sxs-lookup"><span data-stu-id="495e5-190">Make sure that you can access the SP.RequestExecutor.js file in a browser window.</span></span>|

## <a name="next-steps"></a><span data-ttu-id="495e5-191">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="495e5-191">Next steps</span></span>
<span data-ttu-id="495e5-192"><a name="SP15Createcustomproxypage_Nextsteps"> </a></span><span class="sxs-lookup"><span data-stu-id="495e5-192"></span></span>

<span data-ttu-id="495e5-p112">В этой статье показано, как получить доступ к удаленным данным с помощью настраиваемой прокси-страницы для междоменной библиотеки в SharePoint. На следующем этапе вы можете узнать о других вариантах доступа к данным, доступным в Надстройки SharePoint. Дополнительные сведения см. в следующих ресурсах:</span><span class="sxs-lookup"><span data-stu-id="495e5-p112">This article demonstrated how to access remote data by using a custom proxy page for the cross-domain library in SharePoint. As a next step, you can learn about other data access options available in SharePoint Add-ins. To learn more, see the following:</span></span>
 

 

-  [<span data-ttu-id="495e5-195">Пример кода: получение данных с помощью страницы прокси для междоменной библиотеки</span><span class="sxs-lookup"><span data-stu-id="495e5-195">Code sample: Get data by using a proxy page for the cross-domain library</span></span>](http://code.msdn.microsoft.com/SharePoint-Get-data-10039ff1)
    
 
-  [<span data-ttu-id="495e5-196">Доступ к данным SharePoint из надстроек с помощью междоменной библиотеки</span><span class="sxs-lookup"><span data-stu-id="495e5-196">Access SharePoint data from add-ins using the cross-domain library</span></span>](access-sharepoint-data-from-add-ins-using-the-cross-domain-library.md)
    
 
-  [<span data-ttu-id="495e5-197">Отправка запросов удаленной службе с помощью веб-прокси в SharePoint</span><span class="sxs-lookup"><span data-stu-id="495e5-197">Query a remote service using the web proxy in SharePoint</span></span>](query-a-remote-service-using-the-web-proxy-in-sharepoint.md)
    
 

## <a name="additional-resources"></a><span data-ttu-id="495e5-198">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="495e5-198">Additional resources</span></span>
<span data-ttu-id="495e5-199"><a name="SP15Createcustomproxypage_Addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="495e5-199"></span></span>


-  [<span data-ttu-id="495e5-200">Настройка локальной среды разработки надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="495e5-200">Set up an on-premises development environment for SharePoint Add-ins</span></span>](set-up-an-on-premises-development-environment-for-sharepoint-add-ins.md)
    
 
-  [<span data-ttu-id="495e5-201">Работа с внешними данными в SharePoint</span><span class="sxs-lookup"><span data-stu-id="495e5-201">Work with external data in SharePoint</span></span>](work-with-external-data-in-sharepoint.md)
    
 
-  [<span data-ttu-id="495e5-202">Безопасный доступ к данным и клиентские объектные модели для надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="495e5-202">Secure data access and client object models for SharePoint Add-ins</span></span>](secure-data-access-and-client-object-models-for-sharepoint-add-ins.md)
    
 
-  [<span data-ttu-id="495e5-203">Авторизация и проверка подлинности для надстроек в SharePoint</span><span class="sxs-lookup"><span data-stu-id="495e5-203">Authorization and authentication of SharePoint Add-ins</span></span>](authorization-and-authentication-of-sharepoint-add-ins.md)
    
 
-  [<span data-ttu-id="495e5-204">Использование операций запросов OData в запросах REST SharePoint</span><span class="sxs-lookup"><span data-stu-id="495e5-204">Use OData query operations in SharePoint REST requests</span></span>](use-odata-query-operations-in-sharepoint-rest-requests.md)
    
 
-  [<span data-ttu-id="495e5-205">Что следует рассмотреть, прежде чем приступать к разработке надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="495e5-205">Three ways to think about design options for SharePoint Add-ins</span></span>](three-ways-to-think-about-design-options-for-sharepoint-add-ins.md)
    
 
-  [<span data-ttu-id="495e5-206">Важные аспекты разработки и архитектуры для надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="495e5-206">Important aspects of the SharePoint Add-in architecture and development landscape</span></span>](important-aspects-of-the-sharepoint-add-in-architecture-and-development-landscap.md)
    
 
-  [<span data-ttu-id="495e5-207">Хранение данных в надстройках SharePoint</span><span class="sxs-lookup"><span data-stu-id="495e5-207">Data storage in SharePoint Add-ins</span></span>](important-aspects-of-the-sharepoint-add-in-architecture-and-development-landscap.md#Data)
    
 

