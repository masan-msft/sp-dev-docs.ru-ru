---
title: Отправка запросов удаленной службе с помощью веб-прокси в SharePoint
description: Доступ к данным в удаленном домене со страницы, размещенной в SharePoint, с помощью веб-прокси.
ms.date: 12/22/2017
ms.prod: sharepoint
ms.openlocfilehash: 4a1a8516ad4496b977f4191608946bb25b31d9dc
ms.sourcegitcommit: c57fc0e802661b0771f8b022964b6956ab4f6caf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/23/2017
---
# <a name="query-a-remote-service-using-the-web-proxy-in-sharepoint"></a><span data-ttu-id="659c3-103">Запрос данных в удаленной службе с помощью веб-прокси в SharePoint</span><span class="sxs-lookup"><span data-stu-id="659c3-103">Query a remote service using the web proxy in SharePoint</span></span>

<span data-ttu-id="659c3-p101">При создании надстроек SharePoint обычно необходимо объединять данные из различных источников. Из соображений безопасности связь между доменами блокируется. Если вы используете веб-прокси, веб-страницам в надстройке доступны данные на удаленном домене и домене SharePoint.</span><span class="sxs-lookup"><span data-stu-id="659c3-p101">When you are building SharePoint Add-ins, you usually have to incorporate data from various sources. For security reasons, there are blocking mechanisms that prevent cross-domain communication. When you use the web proxy, the webpages in your add-in can access data in your remote domain and the SharePoint domain.</span></span>

<span data-ttu-id="659c3-107">Разработчики могут использовать веб-прокси, предоставляемый в клиентских объектных моделях JavaScript и .NET.</span><span class="sxs-lookup"><span data-stu-id="659c3-107">As a developer, you can use the web proxy exposed in client APIs, such as the JavaScript and .NET client object models.</span></span> <span data-ttu-id="659c3-108">При использовании веб-прокси вы передаете запрос инициализации в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="659c3-108">When you use the web proxy, you issue the initial request to SharePoint.</span></span> <span data-ttu-id="659c3-109">SharePoint в свою очередь запрашивает данные в определенной конечной точке и передает ответ обратно на вашу страницу.</span><span class="sxs-lookup"><span data-stu-id="659c3-109">In turn, SharePoint requests the data to the specified endpoint and forwards the response back to your page.</span></span>

<span data-ttu-id="659c3-110">Используйте веб-прокси, если нужно, чтобы связь осуществлялась на уровне сервера.</span><span class="sxs-lookup"><span data-stu-id="659c3-110">Use the web proxy when you want the communication to occur at the server level.</span></span> <span data-ttu-id="659c3-111">Дополнительные сведения см. в статье [Безопасный доступ к данным и клиентские объектные модели для надстроек SharePoint](secure-data-access-and-client-object-models-for-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="659c3-111">For more information, see [Secure data access and client object models for SharePoint Add-ins](secure-data-access-and-client-object-models-for-sharepoint-add-ins.md).</span></span>

<span data-ttu-id="659c3-112">**Веб-прокси SharePoint — это посредник между вашим кодом и внешним источником данных**</span><span class="sxs-lookup"><span data-stu-id="659c3-112">**SharePoint Web Proxy is middle man between your code and external data source**</span></span>

![Символы "ваш код", "веб-прокси SharePoint" и "источник данных", показывающие, что запросы данных проходят через веб-прокси.](../images/3fbdcfae-6af9-452b-9a07-48575de7e86a.png)

<span data-ttu-id="659c3-114"><a name="SP15Queryremoteservice_Prereq"> </a></span><span class="sxs-lookup"><span data-stu-id="659c3-114"></span></span>

## <a name="prerequisites-for-using-the-examples-in-this-article"></a><span data-ttu-id="659c3-115">Необходимые условия для использования примеров в этой статье</span><span class="sxs-lookup"><span data-stu-id="659c3-115">Prerequisites for using the examples in this article</span></span>

<span data-ttu-id="659c3-116">Для выполнения действий, описанных в этом примере, вам потребуется следующее:</span><span class="sxs-lookup"><span data-stu-id="659c3-116">To follow the steps in this example, you need the following:</span></span>

-  [<span data-ttu-id="659c3-117">Visual Studio 2015 и Инструменты разработчика Microsoft Office последней версии</span><span class="sxs-lookup"><span data-stu-id="659c3-117">Visual Studio 2015 and the latest Microsoft Office Developer Tools</span></span>](https://www.visualstudio.com/features/office-tools-vs.aspx)

- <span data-ttu-id="659c3-118">Среда разработки SharePoint (для локальных сценариев необходимо изолировать надстройку).</span><span class="sxs-lookup"><span data-stu-id="659c3-118">A SharePoint development environment (add-in isolation required for on-premises scenarios)</span></span>

### <a name="core-concepts-to-know-before-using-the-web-proxy"></a><span data-ttu-id="659c3-119">Ключевые понятия, с которыми необходимо ознакомиться до использования веб-прокси</span><span class="sxs-lookup"><span data-stu-id="659c3-119">Core concepts to know before using the web proxy</span></span>

<span data-ttu-id="659c3-120">Ниже перечислены полезные статьи, в которых описано, как запрашивать данные для надстроек SharePoint из удаленного домена.</span><span class="sxs-lookup"><span data-stu-id="659c3-120">The following table lists some useful articles that can help you understand the concepts involved in a cross-domain scenario in SharePoint Add-ins.</span></span>

|<span data-ttu-id="659c3-121">**Название статьи**</span><span class="sxs-lookup"><span data-stu-id="659c3-121">**Article title**</span></span>|<span data-ttu-id="659c3-122">**Описание**</span><span class="sxs-lookup"><span data-stu-id="659c3-122">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="659c3-123">Надстройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="659c3-123">SharePoint Add-ins</span></span>](sharepoint-add-ins.md)|<span data-ttu-id="659c3-124">Сведения о новой модели надстроек в SharePoint, с помощью которой можно создавать небольшие и удобные в использовании надстройки для пользователей.</span><span class="sxs-lookup"><span data-stu-id="659c3-124">Learn about the new add-in model in SharePoint that enables you to create add-ins, which are small, easy-to-use solutions for end users.</span></span>|
| [<span data-ttu-id="659c3-125">Безопасный доступ к данным и клиентские объектные модели для надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="659c3-125">Secure data access and client object models for SharePoint Add-ins</span></span>](secure-data-access-and-client-object-models-for-sharepoint-add-ins.md)|<span data-ttu-id="659c3-126">Узнайте о вариантах доступа к данным в надстройках SharePoint. В этой статье представлена информация о вариантах работы с данными в надстройке.</span><span class="sxs-lookup"><span data-stu-id="659c3-126">Learn about data access options in SharePoint Add-ins. This article provides guidance on the high-level alternatives you have to choose from when working with data in your add-in.</span></span>|
| [<span data-ttu-id="659c3-127">Хост-сайты, сайты надстроек и компоненты SharePoint в SharePoint</span><span class="sxs-lookup"><span data-stu-id="659c3-127">Host webs, add-in webs, and SharePoint components in SharePoint</span></span>](host-webs-add-in-webs-and-sharepoint-components-in-sharepoint.md)|<span data-ttu-id="659c3-p104">Узнайте, в чем разница между хост-сайтами и сайтами надстроек. Узнайте, какие компоненты SharePoint можно включить в Надстройка SharePoint, какие компоненты можно развернуть на хост-сайтах, а какие на сайтах надстроек, а также узнайте, как развертывать сайты надстроек в изолированном домене.</span><span class="sxs-lookup"><span data-stu-id="659c3-p104">Learn about the difference between host webs and add-in webs. Find out which SharePoint components can be included in a SharePoint Add-in, which components are deployed to the host web, which components are deployed to the add-in web, and how the add-in web is deployed in an isolated domain.</span></span>|
| [<span data-ttu-id="659c3-130">Междоменная безопасность на стороне клиента</span><span class="sxs-lookup"><span data-stu-id="659c3-130">Client-side Cross-domain Security</span></span>](http://msdn.microsoft.com/ru-RU/library/cc709423%28v=vs.85%29.aspx)|<span data-ttu-id="659c3-131">Ознакомьтесь с междоменными угрозами, случаями использования и принципами безопасности для междоменных запросов, а также оцените риски для разработчиков, возникающие при расширении междоменного доступа из веб-приложений, которые запускаются в браузере.</span><span class="sxs-lookup"><span data-stu-id="659c3-131">Explore cross-domain threats and use cases, security principles for cross-origin requests, and weigh the risks for developers to enhance cross-domain access from web applications that run in the browser.</span></span>|

<span data-ttu-id="659c3-132"><a name="SP15Queryremoteservice_Codeexample"> </a></span><span class="sxs-lookup"><span data-stu-id="659c3-132"></span></span>

## <a name="code-example-access-data-in-a-remote-service-using-the-web-proxy"></a><span data-ttu-id="659c3-133">Пример кода. Доступ к данным в удаленной службе с помощью веб-прокси</span><span class="sxs-lookup"><span data-stu-id="659c3-133">Code example: Access data in a remote service using the web proxy</span></span>

<span data-ttu-id="659c3-134">Чтобы прочитать данные из удаленной службы, необходимо выполнить указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="659c3-134">To read data from a remote service, you must do the following:</span></span> 

1. <span data-ttu-id="659c3-135">Создайте проект надстройки для SharePoint.</span><span class="sxs-lookup"><span data-stu-id="659c3-135">Create a SharePoint Add-in project.</span></span>

2. <span data-ttu-id="659c3-136">Измените страницу **Default.aspx**, чтобы использовать веб-прокси для запроса удаленной службы.</span><span class="sxs-lookup"><span data-stu-id="659c3-136">Modify the **Default.aspx** page to use the web proxy to query the remote service.</span></span>

3. <span data-ttu-id="659c3-137">Измените манифест надстройки, чтобы разрешить связь с удаленным доменом.</span><span class="sxs-lookup"><span data-stu-id="659c3-137">Modify the add-in manifest to allow communication to the remote domain.</span></span>

<span data-ttu-id="659c3-138">На следующем рисунке показано окно браузера с данными из удаленной службы на веб-странице SharePoint.</span><span class="sxs-lookup"><span data-stu-id="659c3-138">Figure 1 shows the browser window with data from the remote service in a SharePoint webpage.</span></span>

<span data-ttu-id="659c3-139">**Веб-страница SharePoint с данными из удаленной службы**</span><span class="sxs-lookup"><span data-stu-id="659c3-139">**Figure 1. SharePoint webpage with data from the remote service**</span></span>

![Страница SharePoint с данными из удаленной службы](../images/WebProxy_result.png)
 

### <a name="to-create-the-sharepoint-add-in-project"></a><span data-ttu-id="659c3-141">Создание проекта надстройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="659c3-141">To create the SharePoint Add-in project</span></span>

1. <span data-ttu-id="659c3-142">Откройте Visual Studio 2015 от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="659c3-142">Open Visual Studio 2015 as administrator.</span></span> <span data-ttu-id="659c3-143">Для этого щелкните правой кнопкой мыши значок Visual Studio 2015 в меню **Пуск** и выберите **Запуск от имени администратора**.</span><span class="sxs-lookup"><span data-stu-id="659c3-143">(To do this, right-click the Visual Studio 2015 icon on the **Start** menu, and select **Run as administrator**.)</span></span>
    
2. <span data-ttu-id="659c3-144">Создайте новый проект с помощью шаблона **Надстройка SharePoint**.</span><span class="sxs-lookup"><span data-stu-id="659c3-144">Create a new project using the **SharePoint Add-in** template.</span></span>
    
    <span data-ttu-id="659c3-145">На следующем рисунке показано расположение шаблона **Надстройка SharePoint** в 2015: **Шаблоны** > **Visual C#** > **Office/SharePoint** > **Надстройки Office**.</span><span class="sxs-lookup"><span data-stu-id="659c3-145">Figure 2 shows the location of the **SharePoint Add-in** template in Visual Studio 2015, under **Templates** > **Visual C#** > **Office/SharePoint** > **Office Add-ins**.</span></span>
    
    <span data-ttu-id="659c3-146">**Шаблон надстройки SharePoint в Visual Studio**</span><span class="sxs-lookup"><span data-stu-id="659c3-146">**Figure 2. SharePoint Add-in Visual Studio template**</span></span>

    ![Шаблон приложения для SharePoint в Visual Studio](../images/AppForSharePointVSTemplate.PNG)

    <br/>

3. <span data-ttu-id="659c3-148">Укажите URL-адрес веб-сайта SharePoint, который планируется использовать для отладки.</span><span class="sxs-lookup"><span data-stu-id="659c3-148">Provide the URL of the SharePoint website that you want to use for debugging.</span></span>
    
4. <span data-ttu-id="659c3-149">Выберите **SharePoint-hosted** (Размещение в SharePoint) в качестве варианта размещения надстройки.</span><span class="sxs-lookup"><span data-stu-id="659c3-149">Select **SharePoint-hosted** as the hosting option for your add-in.</span></span>
    

### <a name="to-modify-the-defaultaspx-page-to-use-the-web-proxy-by-using-the-javascript-object-model"></a><span data-ttu-id="659c3-150">Изменение страницы Default.aspx для использования веб-прокси с помощью объектной модели JavaScript</span><span class="sxs-lookup"><span data-stu-id="659c3-150">To modify the Default.aspx page to use the web proxy by using the JavaScript object model</span></span>

1. <span data-ttu-id="659c3-151">Дважды щелкните страницу **Default.aspx** в папке **Страницы**.</span><span class="sxs-lookup"><span data-stu-id="659c3-151">Double-click the **Default.aspx** page in the **Pages** folder.</span></span>
    
2. <span data-ttu-id="659c3-p106">Скопируйте следующую разметку и вставьте ее в тег содержимого **PlaceHolderMain** страницы. Разметка выполняет следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="659c3-p106">Copy the following markup and paste it in the **PlaceHolderMain** content tag of the page. The markup performs the following tasks:</span></span>
    
    - <span data-ttu-id="659c3-154">Предоставление заполнителя для удаленных данных.</span><span class="sxs-lookup"><span data-stu-id="659c3-154">Provides a placeholder for the remote data.</span></span>
    
    - <span data-ttu-id="659c3-155">Создание ссылки на файлы JavaScript в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="659c3-155">References the SharePoint JavaScript files.</span></span>
        
    - <span data-ttu-id="659c3-156">Подготовка запроса с объектом **WebRequestInfo**.</span><span class="sxs-lookup"><span data-stu-id="659c3-156">Prepares the request with a **WebRequestInfo** object.</span></span>
        
    - <span data-ttu-id="659c3-157">Подготовка заголовка запроса **Accept** для указания ответа в формате Нотация объектов JavaScript (JSON).</span><span class="sxs-lookup"><span data-stu-id="659c3-157">Prepares the request **Accept** header to specify the response in the JavaScript Object Notation (JSON) format.</span></span>
    
    - <span data-ttu-id="659c3-158">Отправка вызова удаленной конечной точке.</span><span class="sxs-lookup"><span data-stu-id="659c3-158">Issues a call to the remote endpoint.</span></span>
        
    - <span data-ttu-id="659c3-159">Обработка успешного выполнения с отображением удаленных данных на веб-странице SharePoint.</span><span class="sxs-lookup"><span data-stu-id="659c3-159">Handles successful completion, rendering the remote data in the SharePoint webpage.</span></span>
    
    - <span data-ttu-id="659c3-160">Обработка любых ошибок с отображением сообщения об ошибке на веб-странице SharePoint.</span><span class="sxs-lookup"><span data-stu-id="659c3-160">Handles any errors, rendering the error message in the SharePoint webpage.</span></span>
 
    ```js
    Categories from the Northwind database exposed as an OData service: 
        
    <!-- Placeholder for the remote content -->
    <span id="categories"></span>

    <!-- Add references to the JavaScript libraries. -->
    <script 
        type="text/javascript" 
        src="../_layouts/15/SP.Runtime.js">
    </script>
    <script 
        type="text/javascript" 
        src="../_layouts/15/SP.js">
    </script>
    <script type="text/javascript">
    (function () {
        "use strict";

        // Prepare the request to an OData source
        // using the GET verb.
        var context = SP.ClientContext.get_current();
        var request = new SP.WebRequestInfo();
        request.set_url(
            "http://services.odata.org/Northwind/Northwind.svc/Categories"
            );
        request.set_method("GET");

        // We need the response formatted as JSON.
        request.set_headers({ "Accept": "application/json;odata=verbose" });
        var response = SP.WebProxy.invoke(context, request);

        // Let users know that there is some
        // processing going on.
        document.getElementById("categories").innerHTML =
                    "<P>Loading categories...</P>";

        // Set the event handlers and invoke the request.
        context.executeQueryAsync(successHandler, errorHandler);

        // Event handler for the success event.
        // Get the totalResults node in the response.
        // Render the value in the placeholder.
        function successHandler() {

            // Check for status code == 200
            // Some other status codes, such as 302 redirect
            // do not trigger the errorHandler. 
            if (response.get_statusCode() == 200) {
                var categories;
                var output;

                // Load the OData source from the response.
                categories = JSON.parse(response.get_body());

                // Extract the CategoryName and Description
                // from each result in the response.
                // Build the output as a list.
                output = "<UL>";
                for (var i = 0; i < categories.d.results.length; i++) {
                    var categoryName;
                    var description;
                    categoryName = categories.d.results[i].CategoryName;
                    description = categories.d.results[i].Description;
                    output += "<LI>" + categoryName + ":&amp;nbsp;" +
                        description + "</LI>";
                }
                output += "</UL>";

                document.getElementById("categories").innerHTML = output;
            }
            else {
                var errordesc;

                errordesc = "<P>Status code: " +
                    response.get_statusCode() + "<br/>";
                errordesc += response.get_body();
                document.getElementById("categories").innerHTML = errordesc;
            }
        }

        // Event handler for the error event.
        // Render the response body in the placeholder.
        // The body includes the error message.
        function errorHandler() {
            document.getElementById("categories").innerHTML =
                response.get_body();
        }
    })();
    </script>
    ```

    <br/>


### <a name="optional-to-modify-the-defaultaspx-page-to-use-the-web-proxy-by-using-the-rest-endpoint"></a><span data-ttu-id="659c3-161">(Необязательно) Изменение страницы Default.aspx для использования веб-прокси с помощью конечной точки REST</span><span class="sxs-lookup"><span data-stu-id="659c3-161">(Optional) To modify the Default.aspx page to use the web proxy by using the REST endpoint</span></span>

1. <span data-ttu-id="659c3-162">Дважды щелкните страницу **Default.aspx** в папке **Страницы**.</span><span class="sxs-lookup"><span data-stu-id="659c3-162">Double-click the **Default.aspx** page in the **Pages** folder.</span></span>
    
2. <span data-ttu-id="659c3-p107">Скопируйте следующую разметку и вставьте ее в тег содержимого **PlaceHolderMain** страницы. Разметка выполняет следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="659c3-p107">Copy the following markup and paste it in the **PlaceHolderMain** content tag of the page. The markup performs the following tasks:</span></span>
    
    - <span data-ttu-id="659c3-165">Предоставление заполнителя для удаленных данных.</span><span class="sxs-lookup"><span data-stu-id="659c3-165">Provides a placeholder for the remote data.</span></span>
     
    - <span data-ttu-id="659c3-166">Обращение к библиотеке jQuery.</span><span class="sxs-lookup"><span data-stu-id="659c3-166">References the jQuery library.</span></span>
    
    - <span data-ttu-id="659c3-167">Подготовка запроса к конечной точке **SP.WebRequest.Invoke**.</span><span class="sxs-lookup"><span data-stu-id="659c3-167">Prepares the request to the **SP.WebRequest.Invoke** endpoint.</span></span>
    
    - <span data-ttu-id="659c3-p108">Подготовка текста запроса с объектом **SP.WebrequestInfo**. Он включает заголовок **Accept** для указания ответа в формате Нотация объектов JavaScript (JSON).</span><span class="sxs-lookup"><span data-stu-id="659c3-p108">Prepares the body of the request with a **SP.WebrequestInfo** object. The object includes an **Accept** header to specify the response in the JavaScript Object Notation (JSON) format.</span></span>
    
    - <span data-ttu-id="659c3-170">Отправка вызова удаленной конечной точке.</span><span class="sxs-lookup"><span data-stu-id="659c3-170">Issues a call to the remote endpoint.</span></span>
    
    - <span data-ttu-id="659c3-171">Обработка успешного выполнения с отображением удаленных данных на веб-странице SharePoint.</span><span class="sxs-lookup"><span data-stu-id="659c3-171">Handles successful completion, rendering the remote data in the SharePoint webpage.</span></span>
    
    - <span data-ttu-id="659c3-172">Обработка любых ошибок с отображением сообщения об ошибке на веб-странице SharePoint.</span><span class="sxs-lookup"><span data-stu-id="659c3-172">Handles any errors, rendering the error message in the SharePoint webpage.</span></span>
    
    ```js
    Categories from the Northwind database exposed as an OData service: 
        
    <!-- Placeholder for the remote content -->
    <span id="categories"></span>

    <script 
        type="text/javascript" 
        src="//ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.min.js">
    </script>

    <script type="text/javascript">
    (function () {
        "use strict";

        // The Northwind categories endpoint.
        var url =
            "http://services.odata.org/Northwind/Northwind.svc/Categories";

        // Let users know that there is some
        // processing going on.
        document.getElementById("categories").innerHTML =
                    "<P>Loading categories...</P>";

        // Issue a POST request to the SP.WebProxy.Invoke endpoint.
        // The body has the information to issue a GET request
        // to the Northwind service.
        $.ajax({
            url: "../_api/SP.WebProxy.invoke",
            type: "POST",
            data: JSON.stringify(
                {
                    "requestInfo": {
                        "__metadata": { "type": "SP.WebRequestInfo" },
                        "Url": url,
                        "Method": "GET",
                        "Headers": {
                            "results": [{
                                "__metadata": { "type": "SP.KeyValue" },
                                "Key": "Accept",
                                "Value": "application/json;odata=verbose",
                                "ValueType": "Edm.String"
                            }]
                        }
                    }
                }),
            headers: {
                "Accept": "application/json;odata=verbose",
                "Content-Type": "application/json;odata=verbose",
                "X-RequestDigest": $("#__REQUESTDIGEST").val()
            },
            success: successHandler,
            error: errorHandler
        });

        // Event handler for the success event.
        // Get the totalResults node in the response.
        // Render the value in the placeholder.
        function successHandler(data) {
            // Check for status code == 200
            // Some other status codes, such as 302 redirect,
            // do not trigger the errorHandler. 
            if (data.d.Invoke.StatusCode == 200) {
                var categories;
                var output;

                // Load the OData source from the response.
                categories = JSON.parse(data.d.Invoke.Body);

                // Extract the CategoryName and Description
                // from each result in the response.
                // Build the output as a list
                output = "<UL>";
                for (var i = 0; i < categories.d.results.length; i++) {
                    var categoryName;
                    var description;
                    categoryName = categories.d.results[i].CategoryName;
                    description = categories.d.results[i].Description;
                    output += "<LI>" + categoryName + ":&amp;nbsp;" +
                        description + "</LI>";
                }
                output += "</UL>";

                document.getElementById("categories").innerHTML = output;
            }
            else {
                var errordesc;

                errordesc = "<P>Status code: " +
                    data.d.Invoke.StatusCode + "<br/>";
                errordesc += response.get_body();
                document.getElementById("categories").innerHTML = errordesc;
            }
        }

        // Event handler for the error event.
        // Render the response body in the placeholder.
        // The 2nd argument includes the error message.
        function errorHandler() {
            document.getElementById("categories").innerHTML =
                arguments[2];
        }
    })();
    </script>

    ```

<br/>

### <a name="to-edit-the-add-in-manifest-file"></a><span data-ttu-id="659c3-173">Изменение файла манифеста надстройки</span><span class="sxs-lookup"><span data-stu-id="659c3-173">To edit the add-in manifest file</span></span>

1. <span data-ttu-id="659c3-174">В **обозревателе решений** откройте контекстное меню файла **AppManifest.xml** и выберите **Просмотреть код**.</span><span class="sxs-lookup"><span data-stu-id="659c3-174">In **Solution Explorer**, open the shortcut menu for the **AppManifest.xml** file, and choose **View code**.</span></span>
    
2. <span data-ttu-id="659c3-175">Скопируйте следующее определение **RemoteEndPoints** в качестве дочернего элемента узла **App**.</span><span class="sxs-lookup"><span data-stu-id="659c3-175">Copy the following **RemoteEndPoints** definition as a child of the **App** node.</span></span>
    
    ```XML
    <RemoteEndpoints>
        <RemoteEndpoint Url=" http://services.odata.org" />
    </RemoteEndpoints>
    ```

<span data-ttu-id="659c3-p109">Элемент **RemoteEndpoint** используется для указания удаленного домена. Веб-прокси проверяет, объявлены ли запросы к удаленным доменам в манифесте надстройки. Вы можете создать до 20 записей в элементе **RemoteEndpoints**. Учитывается только часть источника;  `http://domain:port` и `http://domain:port/website` считаются одной и той же конечной точкой. Вы можете осуществлять вызовы множества различных конечных точек в одном домене с помощью одного определения **RemoteEndpoint**.</span><span class="sxs-lookup"><span data-stu-id="659c3-p109">The **RemoteEndpoint** element is used to specify the remote domain. The web proxy validates that the requests issued to remote domains are declared in the add-in manifest. You can create up to 20 entries in the **RemoteEndpoints** element. Only the authority part is considered; `http://domain:port` and `http://domain:port/website` are considered the same endpoint. You can issue calls to many different endpoints within the same domain with just one **RemoteEndpoint** definition.</span></span>

### <a name="to-build-and-run-the-solution"></a><span data-ttu-id="659c3-181">Сборка и запуск решения</span><span class="sxs-lookup"><span data-stu-id="659c3-181">To build and run the solution</span></span>

1. <span data-ttu-id="659c3-182">Нажмите клавишу F5.</span><span class="sxs-lookup"><span data-stu-id="659c3-182">Select the F5 key.</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="659c3-183">При нажатии клавиши F5 Visual Studio выполняет сборку решения, развертывает надстройку и открывает страницу разрешений.</span><span class="sxs-lookup"><span data-stu-id="659c3-183">Note  When you press F5, Visual Studio builds the solution, deploys the add-in, and opens the permissions page for the add-in.</span></span>

2. <span data-ttu-id="659c3-184">Нажмите кнопку **Доверять**.</span><span class="sxs-lookup"><span data-stu-id="659c3-184">Select the **Trust It** button.</span></span>
 
3. <span data-ttu-id="659c3-185">Выберите значок надстройки на странице "Содержимое сайта".</span><span class="sxs-lookup"><span data-stu-id="659c3-185">Click the add-in icon in the Site Contents page.</span></span>
    
    <span data-ttu-id="659c3-186">Ниже показаны удаленные данные на веб-странице SharePoint.</span><span class="sxs-lookup"><span data-stu-id="659c3-186">Figure 3 shows the remote data in the SharePoint webpage.</span></span>
    
    <span data-ttu-id="659c3-187">**Удаленные данные на веб-странице SharePoint**</span><span class="sxs-lookup"><span data-stu-id="659c3-187">**Figure 3. Remote data in the SharePoint webpage**</span></span>

    ![Страница SharePoint с данными из удаленной службы](../images/WebProxy_result.png)
 

#### <a name="troubleshooting-the-solution"></a><span data-ttu-id="659c3-189">Устранение неполадок в решении</span><span class="sxs-lookup"><span data-stu-id="659c3-189">Table 2. Troubleshooting the solution</span></span>

|<span data-ttu-id="659c3-190">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="659c3-190">**Problem**</span></span>|<span data-ttu-id="659c3-191">**Решение**</span><span class="sxs-lookup"><span data-stu-id="659c3-191">**Solution**</span></span>|
|:-----|:-----|
|<span data-ttu-id="659c3-192">Visual Studio не открывает браузер после нажатия клавиши F5.</span><span class="sxs-lookup"><span data-stu-id="659c3-192">Visual Studio does not open the browser after you press the F5 key.</span></span>|<span data-ttu-id="659c3-193">Сделайте проект надстройки SharePoint запускаемым.</span><span class="sxs-lookup"><span data-stu-id="659c3-193">Set the SharePoint Add-in project as the startup project.</span></span>|
|<span data-ttu-id="659c3-194">Необработанное исключение **SP не определен**.</span><span class="sxs-lookup"><span data-stu-id="659c3-194">Unhandled exception **SP is undefined**.</span></span>|<span data-ttu-id="659c3-195">Убедитесь, что вы можете получить доступ к файлу SP.RequestExecutor.js в окне браузера.</span><span class="sxs-lookup"><span data-stu-id="659c3-195">Make sure you can access the SP.RequestExecutor.js file in a browser window.</span></span> <span data-ttu-id="659c3-196">Если в качестве среды разработки используется локальный сервер, необходимо отключить проверку обратной связи IIS.</span><span class="sxs-lookup"><span data-stu-id="659c3-196">If you are using your local server as your development environment, you must disable IIS loopback check. Run the following command from a powershellnv command prompt.</span></span> <br/><br/><span data-ttu-id="659c3-197">Выполните следующую команду с помощью командной строки Windows PowerShell: `New-ItemProperty HKLM:\System\CurrentControlSet\Control\Lsa -Name "DisableLoopbackCheck" -value "1" -PropertyType dword`.</span><span class="sxs-lookup"><span data-stu-id="659c3-197">Run the following command from a Windows PowerShell command prompt: `New-ItemProperty HKLM:\System\CurrentControlSet\Control\Lsa -Name "DisableLoopbackCheck" -value "1" -PropertyType dword`</span></span><br/><br/><span data-ttu-id="659c3-198">**Внимание!** Не рекомендуется отключать проверку обратной связи IIS в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="659c3-198">Disabling the IIS loopback check is not recommended in a production environment.</span></span> |
|<span data-ttu-id="659c3-199">Размер ответа от удаленной конечной точки превышает заданный лимит.</span><span class="sxs-lookup"><span data-stu-id="659c3-199">The size of the response from the remote endpoint exceeds the configured limit.</span></span>|<span data-ttu-id="659c3-200">Размер ответа для запросов веб-прокси не должен превышать 200 КБ.</span><span class="sxs-lookup"><span data-stu-id="659c3-200">The response’s size of web proxy requests must not be larger than 200 KB.</span></span>|
|<span data-ttu-id="659c3-201">Комбинация "схема-порт" не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="659c3-201">The scheme-port combination is not supported.</span></span>|<span data-ttu-id="659c3-202">Комбинация "схема-порт" вызова должна отвечать следующим критериям:</span><span class="sxs-lookup"><span data-stu-id="659c3-202">The call schema-port combination must fall within the following criteria:</span></span><br/><br/><span data-ttu-id="659c3-203">**Схема** - **порт**</span><span class="sxs-lookup"><span data-stu-id="659c3-203">**Scheme** - **Port**</span></span><br/><span data-ttu-id="659c3-204">HTTP — 80</span><span class="sxs-lookup"><span data-stu-id="659c3-204">http - 80</span></span><br/><span data-ttu-id="659c3-205">HTTPS — 443</span><span class="sxs-lookup"><span data-stu-id="659c3-205">https - 443</span></span><br/><span data-ttu-id="659c3-206">HTTP или HTTPS — 7000–10000</span><span class="sxs-lookup"><span data-stu-id="659c3-206">http or https - 7000-10000</span></span><br/><br/><span data-ttu-id="659c3-207">**Важно!** Исходящие порты зависят от доступности брандмауэра узла.</span><span class="sxs-lookup"><span data-stu-id="659c3-207">**Important**  The outbound ports are subject to host firewall availability. In particular, only http-80 and https-443 are available on SharePoint Online.</span></span> <span data-ttu-id="659c3-208">В частности, в SharePoint Online доступны только порты HTTP-80 и HTTPS-443.</span><span class="sxs-lookup"><span data-stu-id="659c3-208">Important  The outbound ports are subject to host firewall availability. In particular, only http-80 and https-443 are available on SharePoint Online.</span></span> |


## <a name="see-also"></a><span data-ttu-id="659c3-209">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="659c3-209">See also</span></span>
<span data-ttu-id="659c3-210"><a name="SP15Createcustomproxypage_Addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="659c3-210"></span></span>

- [<span data-ttu-id="659c3-211">Пример кода. Получение данных из удаленной службы с помощью веб-прокси</span><span class="sxs-lookup"><span data-stu-id="659c3-211">Code sample: Get data from a remote service using the web proxy</span></span>](https://code.msdn.microsoft.com/office/SharePoint-2013-Get-data-705bdcd5)
- [<span data-ttu-id="659c3-212">Работа с внешними данными в SharePoint</span><span class="sxs-lookup"><span data-stu-id="659c3-212">Work with external data in SharePoint</span></span>](work-with-external-data-in-sharepoint.md)
