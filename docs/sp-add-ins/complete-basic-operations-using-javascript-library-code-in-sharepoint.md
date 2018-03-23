---
title: Выполнение базовых операций с использованием кода библиотеки JavaScript в SharePoint
description: Узнайте, как писать код для выполнения базовых операций с помощью клиентской объектной модели JavaScript в SharePoint.
ms.date: 12/13/2017
ms.prod: sharepoint
ms.openlocfilehash: 7b4dffceb3f91f7af466cac401342a4449c2549f
ms.sourcegitcommit: 28690b54f1ef7c811d64393d2eaaff0a8635cc72
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/14/2017
---
# <a name="complete-basic-operations-using-javascript-library-code-in-sharepoint"></a><span data-ttu-id="16d7a-103">Выполнение базовых операций с использованием кода библиотеки JavaScript в SharePoint</span><span class="sxs-lookup"><span data-stu-id="16d7a-103">Complete basic operations using JavaScript library code in SharePoint</span></span>

<span data-ttu-id="16d7a-104">С помощью клиентской объектной модели SharePoint вы можете получать и обновлять данные в SharePoint, а также управлять ими.</span><span class="sxs-lookup"><span data-stu-id="16d7a-104">You can use the SharePoint client object model to retrieve, update, and manage data in SharePoint. SharePoint makes the object model available in several forms.</span></span> <span data-ttu-id="16d7a-105">В SharePoint объектная модель доступна в нескольких формах:</span><span class="sxs-lookup"><span data-stu-id="16d7a-105">SharePoint makes the object model available in several forms:</span></span>

- <span data-ttu-id="16d7a-106">распространяемые сборки .NET Framework;</span><span class="sxs-lookup"><span data-stu-id="16d7a-106">.NET Framework redistributable assemblies</span></span>
- <span data-ttu-id="16d7a-107">библиотека JavaScript;</span><span class="sxs-lookup"><span data-stu-id="16d7a-107">JavaScript library</span></span>
- <span data-ttu-id="16d7a-108">конечные точки REST и OData;</span><span class="sxs-lookup"><span data-stu-id="16d7a-108">REST/OData endpoints</span></span>
- <span data-ttu-id="16d7a-109">Сборки Windows Phone</span><span class="sxs-lookup"><span data-stu-id="16d7a-109">Windows Phone assemblies</span></span>
- <span data-ttu-id="16d7a-110">распространяемые сборки Silverlight.</span><span class="sxs-lookup"><span data-stu-id="16d7a-110">Silverlight redistributable assemblies</span></span>
    
<span data-ttu-id="16d7a-111">Дополнительные сведения о наборах API, доступных для SharePoint, см. в статье [Выбор правильного набора API в SharePoint](../general-development/choose-the-right-api-set-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="16d7a-111">For more information about the sets of APIs that are available for SharePoint, see  [Choose the right API set in SharePoint](../general-development/choose-the-right-api-set-in-sharepoint.md).</span></span>  
 
> [!NOTE] 
> <span data-ttu-id="16d7a-112">Пример создания надстройки SharePoint "Hello World", использующей библиотеку JavaScript, см. в статье [Работа с данными SharePoint с помощью API JavaScript для SharePoint](use-the-sharepoint-javascript-apis-to-work-with-sharepoint-data.md).</span><span class="sxs-lookup"><span data-stu-id="16d7a-112">Note  For a "Hello World" level sample SharePoint Add-in that uses the JavaScript library, see  [Use the SharePoint JavaScript APIs to work with SharePoint data](use-the-sharepoint-javascript-apis-to-work-with-sharepoint-data.md).</span></span>
 
<span data-ttu-id="16d7a-113">В этой статье описано, как выполнять базовые операции с помощью объектной модели JavaScript.</span><span class="sxs-lookup"><span data-stu-id="16d7a-113">This article shows how to perform basic operations using the JavaScript object model.</span></span> <span data-ttu-id="16d7a-114">Вы можете добавить ссылку на объектную модель, используя HTML-теги &lt;script&gt;.</span><span class="sxs-lookup"><span data-stu-id="16d7a-114">You can add a reference to the object model by using HTML &lt;script&gt; tags.</span></span> <span data-ttu-id="16d7a-115">Сведения об использовании других клиентских API см. в статьях ниже.</span><span class="sxs-lookup"><span data-stu-id="16d7a-115">For information about how to use the other client APIs, see the following:</span></span>

- [<span data-ttu-id="16d7a-116">Выполнение базовых операций с использованием кода клиентской библиотеки SharePoint</span><span class="sxs-lookup"><span data-stu-id="16d7a-116">Complete basic operations using SharePoint client library code</span></span>](complete-basic-operations-using-sharepoint-client-library-code.md)
- [<span data-ttu-id="16d7a-117">Выполнение базовых операций с использованием конечных точек SharePoint REST</span><span class="sxs-lookup"><span data-stu-id="16d7a-117">Complete basic operations using SharePoint REST endpoints</span></span>](complete-basic-operations-using-sharepoint-rest-endpoints.md)
- [<span data-ttu-id="16d7a-118">Построение приложений Windows Phone, обращающихся к SharePoint</span><span class="sxs-lookup"><span data-stu-id="16d7a-118">Build Windows Phone apps that access SharePoint</span></span>](../general-development/build-windows-phone-apps-that-access-sharepoint.md)
- <span data-ttu-id="16d7a-119">[Использование объектной модели Silverlight](http://msdn.microsoft.com/library/cea7829d-f360-4052-8b76-91d90bcefd2a%28Office.15%29.aspx) в пакете SDK для SharePoint 2010</span><span class="sxs-lookup"><span data-stu-id="16d7a-119">[Using the Silverlight Object Model](http://msdn.microsoft.com/library/cea7829d-f360-4052-8b76-91d90bcefd2a%28Office.15%29.aspx) in the SharePoint 2010 SDK</span></span>

<span data-ttu-id="16d7a-120"><a name="BasicOps_SPJSOMOps"> </a></span><span class="sxs-lookup"><span data-stu-id="16d7a-120"></span></span>

## <a name="perform-basic-tasks-in-sharepoint-using-the-javascript-client-object-model"></a><span data-ttu-id="16d7a-121">Выполнение основных задач в SharePoint с помощью клиентской объектной модели JavaScript</span><span class="sxs-lookup"><span data-stu-id="16d7a-121">Perform basic tasks in SharePoint using the JavaScript client object model</span></span>

<span data-ttu-id="16d7a-122">В следующих разделах описываются задачи, которые вы можете выполнять программным путем. Они включают примеры кода на языке JavaScript, в которых демонстрируются эти операции.</span><span class="sxs-lookup"><span data-stu-id="16d7a-122">The following sections describe tasks that you can complete programmatically, and they include JavaScript code examples that demonstrate the operations.</span></span>

<span data-ttu-id="16d7a-123">При создании облачной надстройки вы можете добавить ссылку на объектную модель, используя HTML-теги &lt;script&gt;.</span><span class="sxs-lookup"><span data-stu-id="16d7a-123">When you create a cloud-hosted add-in, you can add a reference to the object model by using HTML &lt;script&gt; tags.</span></span> <span data-ttu-id="16d7a-124">Рекомендуем создать ссылку на хост-сайт, так как сайт надстройки может быть доступен не в каждом сценарии работы с облачными надстройками. Вы можете получить URL-адрес хост-сайта из параметра строки запроса _SPHostUrl_, если используете маркер **{StandardTokens}**.</span><span class="sxs-lookup"><span data-stu-id="16d7a-124">When you create a cloud-hosted add-in, you can add a reference to the object model by using HTML  tags. We recommend that you reference the host web because the add-in web may not exist in every scenario in cloud-hosted add-ins. You can retrieve the host web URL from the  _SPHostUrl_ query string parameter if you are using the **{StandardTokens} token. You can also use your custom defined query string parameter if you are using the {HostUrl}** token. After you have the host web URL, you must use JavaScript code to dynamically create the reference to the object model.</span></span> <span data-ttu-id="16d7a-125">Вы также можете использовать специальный параметр строки запроса, если применяете токен **{HostUrl}**.</span><span class="sxs-lookup"><span data-stu-id="16d7a-125">You can also use your custom defined query string parameter if you are using the **{HostUrl}** token.</span></span> <span data-ttu-id="16d7a-126">Получив URL-адрес хост-сайта, вам нужно с помощью кода JavaScript динамично создать ссылку на объектную модель.</span><span class="sxs-lookup"><span data-stu-id="16d7a-126">After you have the host web URL, you must use JavaScript code to dynamically create the reference to the object model.</span></span>
 
<span data-ttu-id="16d7a-127">В примере кода ниже выполняются такие задачи для добавления ссылки на объектную модель JavaScript:</span><span class="sxs-lookup"><span data-stu-id="16d7a-127">The following code example performs these tasks to add a reference to the JavaScript object model:</span></span>

- <span data-ttu-id="16d7a-128">Создание ссылки на библиотеку AJAX из сети Microsoft Content Delivery Network (CDN).</span><span class="sxs-lookup"><span data-stu-id="16d7a-128">References the AJAX library from the Microsoft Content Delivery Network (CDN).</span></span>
- <span data-ttu-id="16d7a-129">Создание ссылки на библиотеку jQuery из сети Microsoft CDN.</span><span class="sxs-lookup"><span data-stu-id="16d7a-129">References the jQuery library from the Microsoft CDN.</span></span>
- <span data-ttu-id="16d7a-130">Извлечение URL-адреса хост-сайта из строки запроса.</span><span class="sxs-lookup"><span data-stu-id="16d7a-130">Extracts the host web URL from the query string.</span></span>
- <span data-ttu-id="16d7a-p104">Загрузка файлов SP.Runtime.js и SP.js с помощью функции **getScript** в jQuery. После загрузки файлов программа получает доступ к объектной модели JavaScript для SharePoint.</span><span class="sxs-lookup"><span data-stu-id="16d7a-p104">Loads the SP.Runtime.js and SP.js files by using the **getScript** function in jQuery. After loading the files, your program has access to the JavaScript object model for SharePoint.</span></span>
- <span data-ttu-id="16d7a-133">Продолжение рабочего процесса функции **execOperation**.</span><span class="sxs-lookup"><span data-stu-id="16d7a-133">Continues the flow in the **execOperation** function.</span></span>


```
<script 
    src="//ajax.aspnetcdn.com/ajax/4.0/1/MicrosoftAjax.js" 
    type="text/javascript">
</script>
<script
    type="text/javascript"
    src="//ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.2.min.js">
</script>
<script type="text/javascript">
    var hostweburl;

    // Load the required SharePoint libraries.
    $(document).ready(function () {

        // Get the URI decoded URLs.
        hostweburl =
            decodeURIComponent(
                getQueryStringParameter("SPHostUrl")
        );

        // The js files are in a URL in the form:
        // web_url/_layouts/15/resource_file
        var scriptbase = hostweburl + "/_layouts/15/";

        // Load the js files and continue to
        // the execOperation function.
        $.getScript(scriptbase + "SP.Runtime.js",
            function () {
                $.getScript(scriptbase + "SP.js", execOperation);
            }
        );
    });

    // Function to execute basic operations.
    function execOperation() {

        // Continue your program flow here.

    }

    // Function to retrieve a query string value.
    // For production purposes you may want to use
    // a library to handle the query string.
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

<span data-ttu-id="16d7a-p105">При создании надстройки, размещаемой в SharePoint, можно добавить ссылку на объектную модель с помощью HTML-тегов &lt;script&gt;. Сайт надстройки, размещаемой в SharePoint, позволяет ссылаться на обязательные файлы для использования в объектной модели JavaScript, указывая относительные пути.</span><span class="sxs-lookup"><span data-stu-id="16d7a-p105">When you create a SharePoint-hosted add-in, you can add a reference to the object model by using HTML &lt;script&gt; tags. The add-in web in a SharePoint-hosted add-in allows you to use relative paths to reference the required files to use the JavaScript object model.</span></span>

<span data-ttu-id="16d7a-136">Следующая разметка выполняет указанные далее задачи для добавления ссылки на объектную модель JavaScript:</span><span class="sxs-lookup"><span data-stu-id="16d7a-136">The following markup performs these tasks to add a reference to the JavaScript object model:</span></span>

- <span data-ttu-id="16d7a-137">Создание ссылки на библиотеку AJAX из сети Microsoft CDN.</span><span class="sxs-lookup"><span data-stu-id="16d7a-137">References the AJAX library from the Microsoft CDN.</span></span>
- <span data-ttu-id="16d7a-138">Создание ссылки на файл SP.Runtime.js с использованием относительного URL-адреса сайта надстройки.</span><span class="sxs-lookup"><span data-stu-id="16d7a-138">References the SP.Runtime.js file by using a URL relative to the add-in web.</span></span>
- <span data-ttu-id="16d7a-139">Создание ссылки на файл SP.js с использованием относительного URL-адреса сайта надстройки.</span><span class="sxs-lookup"><span data-stu-id="16d7a-139">References the SP.js file by using a URL relative to the add-in web.</span></span>

```
<script 
    src="//ajax.aspnetcdn.com/ajax/4.0/1/MicrosoftAjax.js" 
    type="text/javascript">
</script>
<script 
    type="text/javascript" 
    src="/_layouts/15/sp.runtime.js">
</script>
<script 
    type="text/javascript" 
    src="/_layouts/15/sp.js">
</script>
<script type="text/javascript">

    // Continue your program flow here.

</script>
```

<br/>

<span data-ttu-id="16d7a-140"><a name="BasicOps_SPWebTasks"> </a></span><span class="sxs-lookup"><span data-stu-id="16d7a-140"></span></span>

## <a name="sharepoint-website-tasks"></a><span data-ttu-id="16d7a-141">Задачи, связанные с веб-сайтом SharePoint</span><span class="sxs-lookup"><span data-stu-id="16d7a-141">SharePoint website tasks</span></span>

<span data-ttu-id="16d7a-142">Для работы с веб-сайтами с использованием JavaScript начните с использования конструктора **ClientContext(serverRelativeUrl)** и передачи URL-адреса или URI-кода для возврата определенного контекста запроса.</span><span class="sxs-lookup"><span data-stu-id="16d7a-142">To work with websites using JavaScript, start by using the **ClientContext(serverRelativeUrl)** constructor and pass a URL or URI to return a specific request context.</span></span>

### <a name="retrieve-the-properties-of-a-website"></a><span data-ttu-id="16d7a-143">Получение свойств веб-сайта</span><span class="sxs-lookup"><span data-stu-id="16d7a-143">Retrieve the properties of a website</span></span>

<span data-ttu-id="16d7a-144">Используйте веб-свойства класса **ClientContext**, чтобы указать свойства объекта веб-сайта, который размещен по указанному URL-адресу контекста.</span><span class="sxs-lookup"><span data-stu-id="16d7a-144">Use the web property of the **ClientContext** class to specify the properties of the website object that is located at the specified context URL.</span></span> <span data-ttu-id="16d7a-145">После загрузки объекта веб-сайта с помощью метода **load(clientObject)** и последующего вызова **executeQueryAsync(succeededCallback, failedCallback)** вы можете получить доступ ко всем свойствам этого веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="16d7a-145">After you load the website object through the **load(clientObject)** method and then call **executeQueryAsync(succeededCallback, failedCallback)**, you acquire access to all the properties of that website.</span></span> 

<span data-ttu-id="16d7a-146">В примере ниже отображается заголовок и описание указанного веб-сайта, хотя все другие возвращаемые свойства по умолчанию становятся доступными после загрузки объекта веб-сайта и выполнения запроса.</span><span class="sxs-lookup"><span data-stu-id="16d7a-146">The following example displays the title and description of the specified website, although all other properties that are returned by default become available after you load the website object and execute the query.</span></span>

```

function retrieveWebSite(siteUrl) {
    var clientContext = new SP.ClientContext(siteUrl);
    this.oWebsite = clientContext.get_web();

    clientContext.load(this.oWebsite);

    clientContext.executeQueryAsync(
        Function.createDelegate(this, this.onQuerySucceeded), 
        Function.createDelegate(this, this.onQueryFailed)
    );
}

function onQuerySucceeded(sender, args) {
    alert('Title: ' + this.oWebsite.get_title() + 
        ' Description: ' + this.oWebsite.get_description());
}
    
function onQueryFailed(sender, args) {
    alert('Request failed. ' + args.get_message() + 
        '\n' + args.get_stackTrace());
}
```

<br/>

### <a name="retrieve-only-selected-properties-of-a-website"></a><span data-ttu-id="16d7a-147">Получение определенных свойств веб-сайта</span><span class="sxs-lookup"><span data-stu-id="16d7a-147">Retrieve only selected properties of a website</span></span>

<span data-ttu-id="16d7a-p107">Для снижения объема передаваемых данных между клиентом и сервером можно получать только указанные свойства объекта веб-сайта, а не все свойства. В этом случае используйте запрос LINQ или синтаксис лямбда-выражений с методом **load(clientObject)** для определения того, какие свойства следует получать от сервера. В следующем примере после вызова запроса **executeQueryAsync(succeededCallback, failedCallback)** доступны только заголовок и дата создания объекта веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="16d7a-p107">To reduce unnecessary data transference between client and server, you might want to return only specified properties of the website object, not all of its properties. In this case, use LINQ query or lambda expression syntax with the **load(clientObject)** method to specify which properties to return from the server. In the following example, only the title and creation date of the website object become available after **executeQueryAsync(succeededCallback, failedCallback)** is called.</span></span>

```
function retrieveWebSiteProperties(siteUrl) {
    var clientContext = new SP.ClientContext(siteUrl);
    this.oWebsite = clientContext.get_web();

    clientContext.load(this.oWebsite, 'Title', 'Created');

    clientContext.executeQueryAsync(
        Function.createDelegate(this, this.onQuerySucceeded), 
        Function.createDelegate(this, this.onQueryFailed)
    );
}

function onQuerySucceeded(sender, args) {
    alert('Title: ' + this.oWebsite.get_title() + 
        ' Created: ' + this.oWebsite.get_created());
}
    
function onQueryFailed(sender, args) {
    alert('Request failed. ' + args.get_message() + 
        '\n' + args.get_stackTrace());
}
```

> [!NOTE] 
> <span data-ttu-id="16d7a-151">Если вы попытаетесь получить доступ к другим свойствам, код создает исключение, так как они недоступны.</span><span class="sxs-lookup"><span data-stu-id="16d7a-151">If you try to access other properties, the code throws an exception because other properties are not available.</span></span>
 
<br/>

### <a name="write-to-a-websites-properties"></a><span data-ttu-id="16d7a-152">Запись значений для свойств веб-сайта</span><span class="sxs-lookup"><span data-stu-id="16d7a-152">Write to a website's properties</span></span>

<span data-ttu-id="16d7a-p108">Для изменения веб-сайта следует задать его свойства и вызвать метод **update()** аналогично применению серверной объектной модели. Однако в клиентской объектной модели следует вызвать **executeQueryAsync(succeededCallback, failedCallback)** для запроса пакетной обработки всех указанных команд. В следующем примере изменяется заголовок и описание указанного веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="16d7a-p108">To modify a website, you set its properties and call the **update()** method, similarly to how the server object model functions. However, in the client object model, you must call **executeQueryAsync(succeededCallback, failedCallback)** to request batch processing of all commands that you specify. The following example changes the title and description of a specified website.</span></span>

```
function updateWebSite(siteUrl) {
    var clientContext = new SP.ClientContext(siteUrl);
    this.oWebsite = clientContext.get_web();

    this.oWebsite.set_title('Updated Web Site');
    this.oWebsite.set_description('This is an updated Web site.');
    this.oWebsite.update();

    clientContext.load(this.oWebsite, 'Title', 'Description');

    clientContext.executeQueryAsync(
        Function.createDelegate(this, this.onQuerySucceeded), 
        Function.createDelegate(this, this.onQueryFailed)
    );
}

function onQuerySucceeded(sender, args) {
    alert('Title: ' + this.oWebsite.get_title() + 
        ' Description: ' + this.oWebsite.get_description());
}
    
function onQueryFailed(sender, args) {
    alert('Request failed. ' + args.get_message() + 
        '\n' + args.get_stackTrace());
}
```

<br/>

<span data-ttu-id="16d7a-156"><a name="BasicOps_SPListTasks"> </a></span><span class="sxs-lookup"><span data-stu-id="16d7a-156"></span></span>

## <a name="sharepoint-list-tasks"></a><span data-ttu-id="16d7a-157">Задачи по работе со списками SharePoint</span><span class="sxs-lookup"><span data-stu-id="16d7a-157">SharePoint list tasks</span></span>

<span data-ttu-id="16d7a-p109">Работа с объектами списков с использованием JavaScript похожа на работу с объектами веб-сайтов. Начинайте работу с использования конструктора **ClientContext(serverRelativeUrl)** и передачи URL-адреса или URI-кода для возврата определенного контекста запроса. После этого можно использовать свойство **lists** класса **Web** для получения коллекции списков на веб-сайте.</span><span class="sxs-lookup"><span data-stu-id="16d7a-p109">Working with list objects using JavaScript is similar to working with website objects. Start by using the **ClientContext(serverRelativeUrl)** constructor and passing a URL or URI to return a specific request context. You can then use the **lists** property of the **Web** class to get the collection of lists in the website.</span></span>

### <a name="retrieve-all-properties-of-all-lists-in-a-website"></a><span data-ttu-id="16d7a-161">Извлечение всех свойств всех списков на веб-сайте</span><span class="sxs-lookup"><span data-stu-id="16d7a-161">Retrieve all properties of all lists in a website</span></span>

<span data-ttu-id="16d7a-p110">Для возврата всех списков веб-сайта загрузите коллекцию списков с помощью метода **load(clientObject)**, а затем вызовите **executeQueryAsync(succeededCallback, failedCallback)**. В следующем примере представлен URL-адрес веб-сайта, а также дата и время создания списка.</span><span class="sxs-lookup"><span data-stu-id="16d7a-p110">To return all the lists of a website, load the list collection through the **load(clientObject)** method, and then call **executeQueryAsync(succeededCallback, failedCallback)**. The following example displays the URL of the website and the date and time that the list was created.</span></span>

```
function retrieveAllListProperties(siteUrl) {
    var clientContext = new SP.ClientContext(siteUrl);
    var oWebsite = clientContext.get_web();
    this.collList = oWebsite.get_lists();
    clientContext.load(collList);

    clientContext.executeQueryAsync(
        Function.createDelegate(this, this.onQuerySucceeded), 
        Function.createDelegate(this, this.onQueryFailed)
    );
}

function onQuerySucceeded() {
    var listInfo = '';
    var listEnumerator = collList.getEnumerator();

    while (listEnumerator.moveNext()) {
        var oList = listEnumerator.get_current();
        listInfo += 'Title: ' + oList.get_title() + ' Created: ' + 
            oList.get_created().toString() + '\n';
    }
    alert(listInfo);
}

function onQueryFailed(sender, args) {
    alert('Request failed. ' + args.get_message() + 
        '\n' + args.get_stackTrace());
}
```

<br/>

### <a name="retrieve-only-specified-properties-of-lists"></a><span data-ttu-id="16d7a-164">Извлечение только заданных свойств списков</span><span class="sxs-lookup"><span data-stu-id="16d7a-164">Retrieve only specified properties of lists</span></span>

<span data-ttu-id="16d7a-p111">В предыдущем примере выполнялся возврат всех свойств списков на веб-сайте. Для уменьшения ненужных данных, передаваемых между клиентом и сервером, можно использовать выражения запросов LINQ, чтобы указать возвращаемые свойства. В JavaScript следует указать **Include** как часть строки запроса, который передается в метод **load(clientObject)** для указания возвращаемых свойств. В следующем примере этот подход используется для возврата только заголовка и идентификатора каждого из списков в коллекции.</span><span class="sxs-lookup"><span data-stu-id="16d7a-p111">The previous example returns all properties of the lists in a website. To reduce unnecessary data transference between client and server, you can use LINQ query expressions to specify which properties to return. In JavaScript, you specify **Include** as part of the query string that is passed to the **load(clientObject)** method to specify which properties to return. The following example uses this approach to return only the title and ID of each list in the collection.</span></span>

```
function retrieveSpecificListProperties(siteUrl) {
    var clientContext = new SP.ClientContext(siteUrl);
    var oWebsite = clientContext.get_web();
    this.collList = oWebsite.get_lists();

    clientContext.load(collList, 'Include(Title, Id)');
    clientContext.executeQueryAsync(
        Function.createDelegate(this, this.onQuerySucceeded), 
        Function.createDelegate(this, this.onQueryFailed)
    );
}

function onQuerySucceeded() {
    var listInfo = '';
    var listEnumerator = collList.getEnumerator();

    while (listEnumerator.moveNext()) {
        var oList = listEnumerator.get_current();
        listInfo += 'Title: ' + oList.get_title() + 
            ' ID: ' + oList.get_id().toString() + '\n';
    }
    alert(listInfo);
}

function onQueryFailed(sender, args) {
    alert('Request failed. ' + args.get_message() + 
        '\n' + args.get_stackTrace());
}

```

<br/>

### <a name="store-retrieved-lists-in-a-collection"></a><span data-ttu-id="16d7a-169">Хранение полученных списков в коллекции</span><span class="sxs-lookup"><span data-stu-id="16d7a-169">Store retrieved lists in a collection</span></span>

<span data-ttu-id="16d7a-170">Как показывает следующий пример, вы можете использовать метод **loadQuery(clientObjectCollection, exp)** вместо метода **load(clientObject)** для хранения возвращаемого значения в другой коллекции вместо его сохранения в свойстве списков.</span><span class="sxs-lookup"><span data-stu-id="16d7a-170">As the following example shows, you can use the **loadQuery(clientObjectCollection, exp)** method instead of the **load(clientObject)** method to store the return value in another collection instead of storing it in the lists property.</span></span>

```
function retrieveSpecificListPropertiesToCollection(siteUrl) {
    var clientContext = new SP.ClientContext(siteUrl);
    var oWebsite = clientContext.get_web();
    var collList = oWebsite.get_lists();

    this.listInfoCollection = clientContext.loadQuery(collList, 'Include(Title, Id)');
    clientContext.executeQueryAsync(
        Function.createDelegate(this, this.onQuerySucceeded), 
        Function.createDelegate(this, this.onQueryFailed)
    );
}

function onQuerySucceeded() {
    var listInfo = '';

    for (var i = 0; i < this.listInfoCollection.length; i++) {
        var oList = this.listInfoCollection[i];
        listInfo += 'Title: ' + oList.get_title() + 
            ' ID: ' + oList.get_id().toString();
    }
    alert(listInfo.toString());
}

function onQueryFailed(sender, args) {
    alert('Request failed. ' + args.get_message() + 
        '\n' + args.get_stackTrace());
}
```

<br/>

### <a name="apply-filters-to-list-retrieval"></a><span data-ttu-id="16d7a-171">Применение фильтров для извлечения списков</span><span class="sxs-lookup"><span data-stu-id="16d7a-171">Apply filters to list retrieval</span></span>

<span data-ttu-id="16d7a-p112">Как показано в следующем примере, операторы **Include** можно вкладывать в запрос JavaScript, чтобы возвратить метаданные как для списка, так и для его полей. В примере возвращаются все поля из всех списков на веб-сайте, а также отображаются заголовок и внутреннее имя всех полей, внутреннее имя которых содержит строку "name".</span><span class="sxs-lookup"><span data-stu-id="16d7a-p112">As the following example shows, you can nest **Include** statements in a JavaScript query to return metadata for both a list and its fields. The example returns all fields from all lists within a website and displays the title and internal name of all fields whose internal name contains the string "name".</span></span>

```
function retrieveAllListsAllFields(siteUrl) {
    var clientContext = new SP.ClientContext(siteUrl);
    var oWebsite = clientContext.get_web();
    var collList = oWebsite.get_lists();

    this.listInfoArray = clientContext.loadQuery(collList, 
        'Include(Title,Fields.Include(Title,InternalName))');

    clientContext.executeQueryAsync(
        Function.createDelegate(this, this.onQuerySucceeded), 
        Function.createDelegate(this, this._onQueryFailed)
    );
}

function onQuerySucceeded() {
    var listInfo = '';

    for (var i = 0; i < this.listInfoArray.length; i++) {
        var oList = this.listInfoArray[i];
        var collField = oList.get_fields();
        var fieldEnumerator = collField.getEnumerator();
            
        while (fieldEnumerator.moveNext()) {
            var oField = fieldEnumerator.get_current();
            var regEx = new RegExp('name', 'ig');
            
            if (regEx.test(oField.get_internalName())) {
                listInfo += '\nList: ' + oList.get_title() + 
                    '\n\tField Title: ' + oField.get_title() + 
                    '\n\tField Name: ' + oField.get_internalName();
            }
        }
    }
    alert(listInfo);
}

function onQueryFailed(sender, args) {
    alert('Request failed. ' + args.get_message() + 
        '\n' + args.get_stackTrace());
}

```

<br/>

<span data-ttu-id="16d7a-174"><a name="BasicOps_SPListCRUD"> </a></span><span class="sxs-lookup"><span data-stu-id="16d7a-174"></span></span>

## <a name="create-update-and-delete-lists"></a><span data-ttu-id="16d7a-175">Создание, обновление и удаление списков</span><span class="sxs-lookup"><span data-stu-id="16d7a-175">Create, update, and delete lists</span></span>

<span data-ttu-id="16d7a-176">Создание, обновление и удаление списков с использованием клиентской объектной модели аналогично выполнению этих операций с помощью серверной объектной модели .NET, хотя клиентские операции не будут завершены до вызова функции **executeQueryAsync(succeededCallback, failedCallback)**.</span><span class="sxs-lookup"><span data-stu-id="16d7a-176">Creating, updating, and deleting lists through the client object model works similarly to how you perform these tasks using the .NET client object model, although client operations do not complete until you call the **executeQueryAsync(succeededCallback, failedCallback)** function.</span></span>

### <a name="create-and-update-a-list"></a><span data-ttu-id="16d7a-177">Создание и обновление списка</span><span class="sxs-lookup"><span data-stu-id="16d7a-177">Create and update a list</span></span>

<span data-ttu-id="16d7a-p113">Для создания объекта списка с помощью JavaScript, используйте объект **ListCreationInformation**, чтобы определить его свойства, и передайте объект функции **add(parameters)** объекта **ListCollection**. В следующем примере создается новый список объявлений.</span><span class="sxs-lookup"><span data-stu-id="16d7a-p113">To create a list object using JavaScript, use the **ListCreationInformation** object to define its properties, and then pass this object to the **add(parameters)** function of the **ListCollection** object. The following example creates a new announcements list.</span></span>

```
function createList(siteUrl) {
    var clientContext = new SP.ClientContext(siteUrl);
    var oWebsite = clientContext.get_web();
    
    var listCreationInfo = new SP.ListCreationInformation();
    listCreationInfo.set_title('My Announcements List');
    listCreationInfo.set_templateType(SP.ListTemplateType.announcements);

    this.oList = oWebsite.get_lists().add(listCreationInfo);

    clientContext.load(oList);
    clientContext.executeQueryAsync(
        Function.createDelegate(this, this.onQuerySucceeded), 
        Function.createDelegate(this, this.onQueryFailed)
    );
}

function onQuerySucceeded() {
    var result = oList.get_title() + ' created.';
    alert(result);
}

function onQueryFailed(sender, args) {
    alert('Request failed. ' + args.get_message() + 
        '\n' + args.get_stackTrace());
}
```

<br/>

<span data-ttu-id="16d7a-180">Если нужно обновить список после его создания, можно задать свойства списка и вызвать функцию **update()** перед вызовом **executeQueryAsync(succeededCallback, failedCallback)**, как показано далее в измененном примере.</span><span class="sxs-lookup"><span data-stu-id="16d7a-180">If you need to update the list after it has been created, you can set list properties and call the **update()** function before calling **executeQueryAsync(succeededCallback, failedCallback)**, as shown in the following modifications of the previous example.</span></span>

```
.
.
.
.
this.oList = oWebsite.get_lists().add(listCreationInfo);

oList.set_description('New Announcements List');
oList.update();

clientContext.load(oList);
clientContext.executeQueryAsync(
    Function.createDelegate(this, this.onQuerySucceeded), 
    Function.createDelegate(this, this.onQueryFailed)
);
```

<br/>

### <a name="add-a-field-to-a-list"></a><span data-ttu-id="16d7a-181">Добавление поля в список</span><span class="sxs-lookup"><span data-stu-id="16d7a-181">Add a field to a list</span></span>

<span data-ttu-id="16d7a-p114">Используйте функцию **add(field)** или **addFieldAsXml(schemaXml, addToDefaultView, options)** объекта **FieldCollection** для добавления поля в коллекцию полей списка. В следующем примере создается поле, которое затем обновляется перед вызовом **executeQueryAsync(succeededCallback, failedCallback)**.</span><span class="sxs-lookup"><span data-stu-id="16d7a-p114">Use the **add(field)** or **addFieldAsXml(schemaXml, addToDefaultView, options)** function of the **FieldCollection** object to add a field to the field collection of a list. The following example creates a field and then updates it before calling **executeQueryAsync(succeededCallback, failedCallback)**.</span></span>

```
function addFieldToList(siteUrl) {
    var clientContext = new SP.ClientContext(siteUrl);

    var oList = clientContext.get_web().get_lists().getByTitle('Announcements');
    this.oField = oList.get_fields().addFieldAsXml(
        '<Field DisplayName=\'MyField\' Type=\'Number\' />', 
        true, 
        SP.AddFieldOptions.defaultValue
    );

    var fieldNumber = clientContext.castTo(oField,SP.FieldNumber);
    fieldNumber.set_maximumValue(100);
    fieldNumber.set_minimumValue(35);
    fieldNumber.update();

    clientContext.load(oField);
    clientContext.executeQueryAsync(
        Function.createDelegate(this, this.onQuerySucceeded), 
        Function.createDelegate(this, this.onQueryFailed)
    );
}

function onQuerySucceeded() {
    var result = oField.get_title() + ' added.';
    alert(result);
}

function onQueryFailed(sender, args) {
    alert('Request failed. ' + args.get_message() + 
        '\n' + args.get_stackTrace());
}
```

<br/>

### <a name="delete-a-list"></a><span data-ttu-id="16d7a-184">Удаление списка</span><span class="sxs-lookup"><span data-stu-id="16d7a-184">Delete a list</span></span>

<span data-ttu-id="16d7a-185">Чтобы удалить список, вызовите функцию **deleteObject()** объекта списка, как показано в примере ниже.</span><span class="sxs-lookup"><span data-stu-id="16d7a-185">To delete a list, call the **deleteObject()** function of the list object, as shown in the following example.</span></span>

```
function deleteList(siteUrl) {
    var clientContext = new SP.ClientContext(siteUrl);
    var oWebsite = clientContext.get_web();
    this.listTitle = 'My Announcements List';

    this.oList = oWebsite.get_lists().getByTitle(listTitle);
    oList.deleteObject();

    clientContext.executeQueryAsync(
        Function.createDelegate(this, this.onQuerySucceeded), 
        Function.createDelegate(this, this.onQueryFailed)
    );
}

function onQuerySucceeded() {
    var result = listTitle + ' deleted.';
    alert(result);
}

function onQueryFailed(sender, args) {
    alert('Request failed. ' + args.get_message() + 
        '\n' + args.get_stackTrace());
}
```

<br/>

<span data-ttu-id="16d7a-186"><a name="BasicOps_FolderTasks"> </a></span><span class="sxs-lookup"><span data-stu-id="16d7a-186"></span></span>

## <a name="create-update-and-delete-folders"></a><span data-ttu-id="16d7a-187">Создание, обновление и удаление папок</span><span class="sxs-lookup"><span data-stu-id="16d7a-187">Create, update, and delete folders</span></span>

<span data-ttu-id="16d7a-p115">Вы можете работать с папками, упорядочивая контент, с помощью объектной модели JavaScript. В следующих разделах рассказывается об основных операциях с папками.</span><span class="sxs-lookup"><span data-stu-id="16d7a-p115">You can manipulate folders to organize your content by using the JavaScript object model. The following sections show you how to perform basic operations on folders.</span></span>

### <a name="create-a-folder-in-a-document-library"></a><span data-ttu-id="16d7a-190">Создание папки в библиотеке документов</span><span class="sxs-lookup"><span data-stu-id="16d7a-190">Create a folder in a document library</span></span>

<span data-ttu-id="16d7a-191">Чтобы создать папку, нужно использовать объект **ListItemCreationInformation**, задать базовый тип объекта как **SP.FileSystemObjectType.folder**, а затем передать его в виде параметра в функцию **addItem(parameters)** объекта **List**.</span><span class="sxs-lookup"><span data-stu-id="16d7a-191">To create a folder, you use a  **ListItemCreationInformation** object, set the underlying object type to **SP.FileSystemObjectType.folder**, and pass it as parameter to the  **addItem(parameters)** function of the **List** object. Set properties on the list item object that this method returns, and then call the update() function, as shown in the following example.</span></span> <span data-ttu-id="16d7a-192">Затем необходимо задать свойства для объекта элемента списка, возвращенного этим методом, и вызвать функцию **update()**, как показано в примере ниже.</span><span class="sxs-lookup"><span data-stu-id="16d7a-192">To create list items, you create a  ListItemCreationInformation object, set its properties, and pass it as parameter to the addItem(parameters) function of the List object. Set properties on the list item object that this method returns, and then call the **update()** function, as shown in the following example.</span></span>


```
function createFolder(resultpanel) {
    var clientContext;
    var oWebsite;
    var oList;
    var itemCreateInfo;

    clientContext = new SP.ClientContext.get_current();
    oWebsite = clientContext.get_web();
    oList = oWebsite.get_lists().getByTitle("Shared Documents");

    itemCreateInfo = new SP.ListItemCreationInformation();
    itemCreateInfo.set_underlyingObjectType(SP.FileSystemObjectType.folder);
    itemCreateInfo.set_leafName("My new folder!");
    this.oListItem = oList.addItem(itemCreateInfo);
    this.oListItem.set_item("Title", "My new folder!");
    this.oListItem.update();

    clientContext.load(this.oListItem);
    clientContext.executeQueryAsync(
        Function.createDelegate(this, successHandler),
        Function.createDelegate(this, errorHandler)
    );

    function successHandler() {
        resultpanel.innerHTML = "Go to the " +
            "<a href='../Lists/Shared Documents'>document library</a> " +
            "to see your new folder.";
    }

    function errorHandler() {
        resultpanel.innerHTML =
            "Request failed: " + arguments[1].get_message();
    }
}
```

<br/>

### <a name="update-a-folder-in-a-document-library"></a><span data-ttu-id="16d7a-193">Обновление папки в библиотеке документов</span><span class="sxs-lookup"><span data-stu-id="16d7a-193">Update a folder in a document library</span></span>

<span data-ttu-id="16d7a-194">Чтобы изменить имя папки, вы можете записать его в свойство **FileLeafRef** и вызвать функцию **update()**, чтобы изменения вступили в силу при вызове метода **executeQueryAsync**.</span><span class="sxs-lookup"><span data-stu-id="16d7a-194">To update the folder name, you can write to the **FileLeafRef** property and call the **update()** function so that changes take effect when you call the **executeQueryAsync** method.</span></span>

```
function updateFolder(resultpanel) {
    var clientContext;
    var oWebsite;
    var oList;

    clientContext = new SP.ClientContext.get_current();
    oWebsite = clientContext.get_web();
    oList = oWebsite.get_lists().getByTitle("Shared Documents");

    this.oListItem = oList.getItemById(1);
    this.oListItem.set_item("FileLeafRef", "My updated folder");
    this.oListItem.update();

    clientContext.load(this.oListItem);
    clientContext.executeQueryAsync(
        Function.createDelegate(this, successHandler),
        Function.createDelegate(this, errorHandler)
    );

    function successHandler() {
        resultpanel.innerHTML = "Go to the " +
            "<a href='../Lists/Shared Documents'>document library</a> " +
            "to see your updated folder.";
    }

    function errorHandler() {
        resultpanel.innerHTML = "Request failed: " + arguments[1].get_message();
    }
}
```

<br/>

### <a name="delete-a-folder-in-a-document-library"></a><span data-ttu-id="16d7a-195">Удаление папки в библиотеке документов</span><span class="sxs-lookup"><span data-stu-id="16d7a-195">Delete a folder in a document library</span></span>

<span data-ttu-id="16d7a-p117">Чтобы удалить папку, следует вызвать функцию **deleteObject()** объекта. В следующем примере метод **getFolderByServerRelativeUrl** используется для извлечения папки из библиотеки документов и удаления элемента.</span><span class="sxs-lookup"><span data-stu-id="16d7a-p117">To delete a folder, call the **deleteObject()** function on the object. The following example uses the **getFolderByServerRelativeUrl** method to retrieve the folder from the document library and then deletes the item.</span></span>

```
function deleteFolder(resultpanel) {
    var clientContext;
    var oWebsite;
    var folderUrl;

    clientContext = new SP.ClientContext.get_current();
    oWebsite = clientContext.get_web();

    clientContext.load(oWebsite);
    clientContext.executeQueryAsync(function () {
        folderUrl = oWebsite.get_serverRelativeUrl() + "/Lists/Shared Documents/Folder1";
        this.folderToDelete = oWebsite.getFolderByServerRelativeUrl(folderUrl);
        this.folderToDelete.deleteObject();

        clientContext.executeQueryAsync(
            Function.createDelegate(this, successHandler),
            Function.createDelegate(this, errorHandler)
        );
    }, errorHandler);

    function successHandler() {
        resultpanel.innerHTML = "Go to the " +
            "<a href='../Lists/Shared Documents'>document library</a> " +
            "to make sure the folder is no longer there.";
    }

    function errorHandler() {
        resultpanel.innerHTML = "Request failed: " + arguments[1].get_message();
    }
}
```

<br/>

<span data-ttu-id="16d7a-198"><a name="BasicOps_FileTasks"> </a></span><span class="sxs-lookup"><span data-stu-id="16d7a-198"></span></span>

## <a name="create-read-update-and-delete-files"></a><span data-ttu-id="16d7a-199">Создание, чтение, обновление и удаление файлов</span><span class="sxs-lookup"><span data-stu-id="16d7a-199">Create, read, update, and delete files</span></span>

<span data-ttu-id="16d7a-p118">Вы можете работать с файлами с помощью объектной модели JavaScript. В разделах ниже описаны основные операции с файлами.</span><span class="sxs-lookup"><span data-stu-id="16d7a-p118">You can manipulate files by using the JavaScript object model. The following sections show you how to perform basic operations on files.</span></span>
 
> [!NOTE] 
> <span data-ttu-id="16d7a-202">С помощью объектной модели JavaScript можно работать только с файлами размером до 1,5 МБ.</span><span class="sxs-lookup"><span data-stu-id="16d7a-202">Note  You can only work with files up to 1.5 MB by using the JavaScript object model. To upload larger files, use REST (Representational State Transfer). For more information, see  .</span></span> <span data-ttu-id="16d7a-203">Чтобы отправлять более крупные файлы, используйте REST.</span><span class="sxs-lookup"><span data-stu-id="16d7a-203">To upload larger files, use REST (Representational State Transfer).</span></span> <span data-ttu-id="16d7a-204">Подробнее см. в статье [Выполнение базовых операций с использованием конечных точек REST SharePoint](complete-basic-operations-using-sharepoint-rest-endpoints.md).</span><span class="sxs-lookup"><span data-stu-id="16d7a-204">For more information, see  [Complete basic operations using SharePoint 2013 REST endpoints](complete-basic-operations-using-sharepoint-rest-endpoints.md).</span></span>

### <a name="create-a-file-in-a-document-library"></a><span data-ttu-id="16d7a-205">Создание файла в библиотеке документов</span><span class="sxs-lookup"><span data-stu-id="16d7a-205">Create a file in a document library</span></span>

<span data-ttu-id="16d7a-206">Для создания файлов используйте объект **FileCreationInformation**, задав атрибут URL и добавив контент как байтовый массив в кодировке Base64, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="16d7a-206">To create files, you use a **FileCreationInformation** object, set the URL attribute, and append content as a base64 encoded array of bytes, as shown in this example.</span></span>

```
function createFile(resultpanel) {
    var clientContext;
    var oWebsite;
    var oList;
    var fileCreateInfo;
    var fileContent;

    clientContext = new SP.ClientContext.get_current();
    oWebsite = clientContext.get_web();
    oList = oWebsite.get_lists().getByTitle("Shared Documents");

    fileCreateInfo = new SP.FileCreationInformation();
    fileCreateInfo.set_url("my new file.txt");
    fileCreateInfo.set_content(new SP.Base64EncodedByteArray());
    fileContent = "The content of my new file";

    for (var i = 0; i < fileContent.length; i++) {
        
        fileCreateInfo.get_content().append(fileContent.charCodeAt(i));
    }

    this.newFile = oList.get_rootFolder().get_files().add(fileCreateInfo);

    clientContext.load(this.newFile);
    clientContext.executeQueryAsync(
        Function.createDelegate(this, successHandler),
        Function.createDelegate(this, errorHandler)
    );

    function successHandler() {
        resultpanel.innerHTML =
            "Go to the " +
            "<a href='../Lists/Shared Documents'>document library</a> " +
            "to see your new file.";
    }

    function errorHandler() {
        resultpanel.innerHTML = "Request failed: " + arguments[1].get_message();
    }
}
```

<br/>

### <a name="read-a-file-in-a-document-library"></a><span data-ttu-id="16d7a-207">Чтение файла в библиотеке документов</span><span class="sxs-lookup"><span data-stu-id="16d7a-207">Read a file in a document library</span></span>

<span data-ttu-id="16d7a-208">Для чтения контента файла используйте операцию **GET** с URL-адресом файла, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="16d7a-208">To read a file's content, you perform a **GET** operation on the file's URL, as shown in the following example.</span></span>
 
```
function readFile(resultpanel) {
    var clientContext;
    var oWebsite;
    var fileUrl;

    clientContext = new SP.ClientContext.get_current();
    oWebsite = clientContext.get_web();

    clientContext.load(oWebsite);
    clientContext.executeQueryAsync(function () {
        fileUrl = oWebsite.get_serverRelativeUrl() +
            "/Lists/Shared Documents/TextFile1.txt";
        $.ajax({
            url: fileUrl,
            type: "GET"
        })
            .done(Function.createDelegate(this, successHandler))
            .error(Function.createDelegate(this, errorHandler));
    }, errorHandler);

    function successHandler(data) {
        resultpanel.innerHTML =
            "The content of file \"TextFile1.txt\": " + data
    }

    function errorHandler() {
        resultpanel.innerHTML =
            "Request failed: " + arguments[2];
    }
}
```

<br/>

### <a name="update-a-file-in-a-document-library"></a><span data-ttu-id="16d7a-209">Обновление файла в библиотеке документов</span><span class="sxs-lookup"><span data-stu-id="16d7a-209">Update a file in a document library</span></span>

<span data-ttu-id="16d7a-210">Чтобы изменить контент файла, используйте объект **FileCreationInformation**, задав атрибут перезаписи равным "true" с помощью метода **set_overwrite()**, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="16d7a-210">To update the file's content, you can use a **FileCreationInformation** object, and set the overwrite attribute to true by using the **set_overwrite()** method, as shown in this example.</span></span>
 
```
function updateFile(resultpanel) {
    var clientContext;
    var oWebsite;
    var oList;
    var fileCreateInfo;
    var fileContent;

    clientContext = new SP.ClientContext.get_current();
    oWebsite = clientContext.get_web();
    oList = oWebsite.get_lists().getByTitle("Shared Documents");

    fileCreateInfo = new SP.FileCreationInformation();
    fileCreateInfo.set_url("TextFile1.txt");
    fileCreateInfo.set_content(new SP.Base64EncodedByteArray());
    fileCreateInfo.set_overwrite(true);
    fileContent = "The updated content of my file";

    for (var i = 0; i < fileContent.length; i++) {

        fileCreateInfo.get_content().append(fileContent.charCodeAt(i));
    }

    this.existingFile = oList.get_rootFolder().get_files().add(fileCreateInfo);

    clientContext.load(this.existingFile);
    clientContext.executeQueryAsync(
        Function.createDelegate(this, successHandler),
        Function.createDelegate(this, errorHandler)
    );

    function successHandler() {
        resultpanel.innerHTML =
            "Go to the " +
            "<a href='../Lists/Shared Documents'>document library</a> " +
            "to see the updated \"TextFile1.txt\" file.";
    }

    function errorHandler() {
        resultpanel.innerHTML =
            "Request failed: " + arguments[1].get_message();
    }
}
```

<br/>

### <a name="delete-a-file-in-a-document-library"></a><span data-ttu-id="16d7a-211">Удаление файла в библиотеке документов</span><span class="sxs-lookup"><span data-stu-id="16d7a-211">Delete a file in a document library</span></span>

<span data-ttu-id="16d7a-p120">Чтобы удалить файл, следует вызвать функцию **deleteObject()** объекта. В следующем примере метод **getFileByServerRelativeUrl** используется для извлечения файла из библиотеки документов и удаления элемента.</span><span class="sxs-lookup"><span data-stu-id="16d7a-p120">To delete a file, call the **deleteObject()** function on the object. The following example uses the **getFileByServerRelativeUrl** method to retrieve the file from the document library, and then deletes the item.</span></span>
 
```
function deleteFile(resultpanel) {
    var clientContext;
    var oWebsite;
    var fileUrl;

    clientContext = new SP.ClientContext.get_current();
    oWebsite = clientContext.get_web();

    clientContext.load(oWebsite);
    clientContext.executeQueryAsync(function () {
        fileUrl = oWebsite.get_serverRelativeUrl() +
            "/Lists/Shared Documents/TextFile1.txt";
        this.fileToDelete = oWebsite.getFileByServerRelativeUrl(fileUrl);
        this.fileToDelete.deleteObject();

        clientContext.executeQueryAsync(
            Function.createDelegate(this, successHandler),
            Function.createDelegate(this, errorHandler)
        );
    }, errorHandler);

    function successHandler() {
        resultpanel.innerHTML =
            "Go to the " +
            "<a href='../Lists/Shared Documents'>document library</a> " +
            "to confirm that the \"TextFile1.txt\" file has been deleted.";
    }

    function errorHandler() {
        resultpanel.innerHTML = "Request failed: " + arguments[1].get_message();
    }
}
```

<br/>

<span data-ttu-id="16d7a-214"><a name="BasicOps_SPListItemTasks"> </a></span><span class="sxs-lookup"><span data-stu-id="16d7a-214"></span></span>

## <a name="sharepoint-list-item-tasks"></a><span data-ttu-id="16d7a-215">Задачи, связанные с элементами списков SharePoint</span><span class="sxs-lookup"><span data-stu-id="16d7a-215">SharePoint list item tasks</span></span>

<span data-ttu-id="16d7a-216">Чтобы получить элементы из списка с помощью JavaScript, используйте функцию **getItemById(id)** для возврата одного элемента или функцию **getItems(query)** для извлечения нескольких элементов.</span><span class="sxs-lookup"><span data-stu-id="16d7a-216">To return items from a list using JavaScript, use the  **getItemById(id)** function to return a single item, or use the **getItems(query)** function to return multiple items. You then use the load(clientObject) function to attain list item objects that represent the items.</span></span> <span data-ttu-id="16d7a-217">Затем можно использовать функцию **load(clientObject)**, чтобы получить объекты, представляющие элементы списка.</span><span class="sxs-lookup"><span data-stu-id="16d7a-217">You then use the **load(clientObject)** function to attain list item objects that represent the items.</span></span>

### <a name="retrieve-items-from-a-list"></a><span data-ttu-id="16d7a-218">Получение элементов из списка</span><span class="sxs-lookup"><span data-stu-id="16d7a-218">Retrieve items from a list</span></span>

<span data-ttu-id="16d7a-p122">Функция **getItems(query)** позволяет задавать запрос Язык CAML, который определяет возвращаемые элементы. Вы можете передать неопределенный объект **CamlQuery** для возврата всех элементов из списка или использовать функцию **set_viewXml** для определения запроса CAML и возврата элементов, которые отвечают определенным критериям. В следующем примере отображается идентификатор (помимо значений столбцов Title и Body) первых 100 элементов списка объявлений, начиная с элементов списка, идентификатор коллекции которых превышает 10.</span><span class="sxs-lookup"><span data-stu-id="16d7a-p122">The **getItems(query)** function enables you to define a Collaborative Application Markup Language (CAML) query that specifies which items to return. You can pass an undefined **CamlQuery** object to return all items from the list, or use the **set_viewXml** function to define a CAML query and return items that meet specific criteria. The following example displays the ID, in addition to the Title and Body column values, of the first 100 items in the Announcements list, starting with list items whose collection ID is greater than 10.</span></span>
 
```
function retrieveListItems(siteUrl) {
    var clientContext = new SP.ClientContext(siteUrl);
    var oList = clientContext.get_web().get_lists().getByTitle('Announcements');
        
    var camlQuery = new SP.CamlQuery();
    camlQuery.set_viewXml(
        '<View><Query><Where><Geq><FieldRef Name=\'ID\'/>' + 
        '<Value Type=\'Number\'>1</Value></Geq></Where></Query>' + 
        '<RowLimit>10</RowLimit></View>'
    );
    this.collListItem = oList.getItems(camlQuery);
        
    clientContext.load(collListItem);
    clientContext.executeQueryAsync(
        Function.createDelegate(this, this.onQuerySucceeded), 
        Function.createDelegate(this, this.onQueryFailed)
    ); 
}

function onQuerySucceeded(sender, args) {
    var listItemInfo = '';
    var listItemEnumerator = collListItem.getEnumerator();
        
    while (listItemEnumerator.moveNext()) {
        var oListItem = listItemEnumerator.get_current();
        listItemInfo += '\nID: ' + oListItem.get_id() + 
            '\nTitle: ' + oListItem.get_item('Title') + 
            '\nBody: ' + oListItem.get_item('Body');
    }

    alert(listItemInfo.toString());
}

function onQueryFailed(sender, args) {
    alert('Request failed. ' + args.get_message() + 
        '\n' + args.get_stackTrace());
}
```

<br/>

### <a name="use-the-include-method-to-access-properties-of-listitem-objects"></a><span data-ttu-id="16d7a-222">Использование метода Include для доступа к свойствам объектов ListItem</span><span class="sxs-lookup"><span data-stu-id="16d7a-222">Use the Include method to access properties of ListItem objects</span></span>

<span data-ttu-id="16d7a-223">При возврате элементов списка четыре свойства объектов **ListItem** недоступны по умолчанию: **displayName**, **effectiveBasePermissions**, **hasUniqueRoleAssignments** и **roleAssignments**.</span><span class="sxs-lookup"><span data-stu-id="16d7a-223">Four properties of **ListItem** objects are not available by default when you return the list items **displayName**, **effectiveBasePermissions**, **hasUniqueRoleAssignments**, and **roleAssignments**.</span></span> <span data-ttu-id="16d7a-224">Если в предыдущем примере попытаться получить доступ к одному из этих свойств, возвращается исключение **PropertyOrFieldNotInitializedException**.</span><span class="sxs-lookup"><span data-stu-id="16d7a-224">The previous example returns a **PropertyOrFieldNotInitializedException** if you try to access one of these properties.</span></span> <span data-ttu-id="16d7a-225">Чтобы получить доступ к этим свойствам, используйте метод **Include** в строке запроса, как показано в примере ниже.</span><span class="sxs-lookup"><span data-stu-id="16d7a-225">To access these properties, use the **Include** method as part of the query string, as shown in the following example.</span></span>
 
> [!NOTE] 
> <span data-ttu-id="16d7a-226">Когда вы создаете запросы для клиентской объектной модели с помощью LINQ, применяется поставщик [LINQ to Objects](http://msdn.microsoft.com/library/bb397919), а не [LINQ to SharePoint](http://msdn.microsoft.com/library/ee535491), который можно использовать только при написании кода для серверной объектной модели.</span><span class="sxs-lookup"><span data-stu-id="16d7a-226">When you use LINQ to create queries against the client object model, you are using [LINQ to Objects](http://msdn.microsoft.com/library/bb397919), not the [LINQ to SharePoint provider](http://msdn.microsoft.com/library/ee535491), which can only be used when you write code against the server object model.</span></span>

```
function retrieveListItemsInclude(siteUrl) {
    var clientContext = new SP.ClientContext(siteUrl);
    var oList = clientContext.get_web().get_lists().getByTitle('Announcements');

    var camlQuery = new SP.CamlQuery();
    camlQuery.set_viewXml('<View><RowLimit>100</RowLimit></View>');
    this.collListItem = oList.getItems(camlQuery);

    clientContext.load(
        collListItem, 
        'Include(Id, DisplayName, HasUniqueRoleAssignments)'
    );
    clientContext.executeQueryAsync(
        Function.createDelegate(this, this.onQuerySucceeded), 
        Function.createDelegate(this, this.onQueryFailed)
    );
}

function onQuerySucceeded(sender, args) {
    var listItemInfo = '';
    var listItemEnumerator = collListItem.getEnumerator();
        
    while (listItemEnumerator.moveNext()) {
        var oListItem = listItemEnumerator.get_current();
        listItemInfo += '\nID: ' + oListItem.get_id() + 
            '\nDisplay name: ' + oListItem.get_displayName() + 
            '\nUnique role assignments: ' + 
            oListItem.get_hasUniqueRoleAssignments();
    }

    alert(listItemInfo.toString());
}

function onQueryFailed(sender, args) {
    alert('Request failed. ' + args.get_message() + 
        '\n' + args.get_stackTrace());
}

```

<br/>

<span data-ttu-id="16d7a-227">Так как в этом примере используется метод **Include**, после выполнения запроса доступны только указанные свойства.</span><span class="sxs-lookup"><span data-stu-id="16d7a-227">Because this example uses an **Include**, only the specified properties are available after query execution.</span></span> <span data-ttu-id="16d7a-228">Поэтому если вы попытаетесь получить доступ к другим свойствам помимо указанных, будет возвращено исключение **PropertyOrFieldNotInitializedException**.</span><span class="sxs-lookup"><span data-stu-id="16d7a-228">Therefore, you receive a **PropertyOrFieldNotInitializedException** if you try to access other properties beyond those that have been specified.</span></span> <span data-ttu-id="16d7a-229">Кроме того, эта ошибка возникнет, если вы попытаетесь получить доступ к объектам, которые они содержат, с помощью таких функций, как **get\_contentType** или **get\_parentList**.</span><span class="sxs-lookup"><span data-stu-id="16d7a-229">In addition, you receive this error if you try to use functions such as **get\_contentType** or **get\_parentList** to access the properties of containing objects.</span></span>

### <a name="restrictions-on-retrieving-items"></a><span data-ttu-id="16d7a-230">Ограничения на получение элементов</span><span class="sxs-lookup"><span data-stu-id="16d7a-230">Restrictions on retrieving items</span></span>

<span data-ttu-id="16d7a-231">Метод **loadQuery(clientObjectCollection, exp)** объектной модели JavaScript в SharePoint Foundation 2010 не поддерживает методы и операторы LINQ, которые используются в управляемой объектной модели.</span><span class="sxs-lookup"><span data-stu-id="16d7a-231">The **loadQuery(clientObjectCollection, exp)** method of the JavaScript object model in SharePoint Foundation 2010 does not support LINQ methods and operators that are used by the managed object model.</span></span>
 
<br/>

<span data-ttu-id="16d7a-232"><a name="BasicOps_SPListItemCRUD"> </a></span><span class="sxs-lookup"><span data-stu-id="16d7a-232"></span></span> 

## <a name="create-update-and-delete-list-items"></a><span data-ttu-id="16d7a-233">Создание, обновление и удаление элементов списков</span><span class="sxs-lookup"><span data-stu-id="16d7a-233">Create, update, and delete list items</span></span>

<span data-ttu-id="16d7a-p125">Создание, обновление и удаление элементов списка с помощью клиентской объектной модели работает аналогично выполнению этих задач с помощью серверной объектной модели. Можно создать объект элемента списка, установить его свойства, а затем обновить этот объект. Чтобы изменить или удалить объект "list item", необходимо вернуть этот объект с помощью функции **getById(id)** объекта **ListItemCollection**, а затем либо установить свойства и вызвать обновление в объекте, возвращенном методом, либо вызвать собственный метод объекта для удаления. В отличие от серверной объектной модели, каждая из этих операций в клиентской объектной модели должна завершаться вызовом метода **to executeQueryAsync(succeededCallback, failedCallback)**, чтобы изменения вступили в силу на сервере</span><span class="sxs-lookup"><span data-stu-id="16d7a-p125">Creating, updating, or deleting list items through the client object model works similarly to performing these tasks through the server object model. You create a list item object, set its properties, and then update the object. To modify or delete a list item object, use the **getById(id)** function of the **ListItemCollection** object to return the object, and then either set properties and call update on the object that this method returns, or call the object's own method for deletion. Unlike the server object model, each of these operations in the client object model must conclude with a call **to executeQueryAsync(succeededCallback, failedCallback)** for changes to take effect on the server.</span></span>

### <a name="create-a-list-item"></a><span data-ttu-id="16d7a-238">Создание элемента списка</span><span class="sxs-lookup"><span data-stu-id="16d7a-238">Create a list item</span></span>

<span data-ttu-id="16d7a-239">Чтобы создать элементы списка, следует создать объект **ListItemCreationInformation**, установить его свойства и передать его как параметр в функцию **addItem(parameters)** объекта **List**.</span><span class="sxs-lookup"><span data-stu-id="16d7a-239">To create list items, you create a  **ListItemCreationInformation** object, set its properties, and pass it as parameter to the **addItem(parameters)** function of the **List** object. Set properties on the list item object that this method returns, and then call the update() function, as shown in the following example.</span></span> <span data-ttu-id="16d7a-240">Затем необходимо задать свойства для объекта элемента списка, возвращенного этим методом, и вызвать функцию **update()**, как показано в примере ниже.</span><span class="sxs-lookup"><span data-stu-id="16d7a-240">To create list items, you create a  ListItemCreationInformation object, set its properties, and pass it as parameter to the addItem(parameters) function of the List object. Set properties on the list item object that this method returns, and then call the **update()** function, as shown in the following example.</span></span>


```
function createListItem(siteUrl) {
    var clientContext = new SP.ClientContext(siteUrl);
    var oList = clientContext.get_web().get_lists().getByTitle('Announcements');
        
    var itemCreateInfo = new SP.ListItemCreationInformation();
    this.oListItem = oList.addItem(itemCreateInfo);
    oListItem.set_item('Title', 'My New Item!');
    oListItem.set_item('Body', 'Hello World!');
    oListItem.update();

    clientContext.load(oListItem);
    clientContext.executeQueryAsync(
        Function.createDelegate(this, this.onQuerySucceeded), 
        Function.createDelegate(this, this.onQueryFailed)
    );
}

function onQuerySucceeded() {
    alert('Item created: ' + oListItem.get_id());
}

function onQueryFailed(sender, args) {
    alert('Request failed. ' + args.get_message() + 
        '\n' + args.get_stackTrace());
}
```

<br/>

### <a name="update-a-list-item"></a><span data-ttu-id="16d7a-241">Обновление элемента списка</span><span class="sxs-lookup"><span data-stu-id="16d7a-241">Update a list item</span></span>

<span data-ttu-id="16d7a-242">Для установки большинства свойств элемента списка можно с помощью индексатора столбца создать назначение, а затем вызвать функцию **update()**, чтобы изменения вступили в силу при вызове **executeQueryAsync(succeededCallback, failedCallback)**.</span><span class="sxs-lookup"><span data-stu-id="16d7a-242">To set most list item properties, you can use a column indexer to make an assignment, and call the  **update()** function so that changes will take effect when you call **executeQueryAsync(succeededCallback, failedCallback)**. The following example sets the title of the third item in the Announcements list.</span></span> <span data-ttu-id="16d7a-243">В примере ниже устанавливается заголовок третьего элемента списка Announcements.</span><span class="sxs-lookup"><span data-stu-id="16d7a-243">The following example sets the title of the third item in the Announcements list.</span></span>

```
function updateListItem(siteUrl) {
    var clientContext = new SP.ClientContext(siteUrl);
    var oList = clientContext.get_web().get_lists().getByTitle('Announcements');

    this.oListItem = oList.getItemById(3);
    oListItem.set_item('Title', 'My Updated Title');
    oListItem.update();

    clientContext.executeQueryAsync(
        Function.createDelegate(this, this.onQuerySucceeded), 
        Function.createDelegate(this, this.onQueryFailed)
    );
}

function onQuerySucceeded() {
    alert('Item updated!');
}

function onQueryFailed(sender, args) {
    alert('Request failed. ' + args.get_message() + 
        '\n' + args.get_stackTrace());
}
```

<br/>

### <a name="delete-a-list-item"></a><span data-ttu-id="16d7a-244">Удаление элемента списка</span><span class="sxs-lookup"><span data-stu-id="16d7a-244">Delete a list item</span></span>

<span data-ttu-id="16d7a-p128">Чтобы удалить элемент списка, следует вызвать функцию **deleteObject()** объекта. В следующем примере используется функция **getItemById(id)** для возврата второго элемента списка, а затем выполняется удаление элемента. SharePoint обслуживает целочисленные идентификаторы элементов в коллекциях, даже если эти элементы удаляются. Поэтому, например, второй элемент списка должен иметь идентификатор, отличный от 2. **ServerException** возвращается, если функция **deleteObject()** вызывается для несуществующего элемента.</span><span class="sxs-lookup"><span data-stu-id="16d7a-p128">To delete a list item, call the **deleteObject()** function on the object. The following example uses the **getItemById(id)** function to return the second item from the list, and then deletes the item. SharePoint maintains the integer IDs of items within collections, even if they have been deleted. So, for example, the second item in a list might not have 2 as its identifier. A **ServerException** is returned if the **deleteObject()** function is called for an item that does not exist.</span></span>

```
function deleteListItem(siteUrl) {
    this.itemId = 2;
    var clientContext = new SP.ClientContext(siteUrl);
    var oList = clientContext.get_web().get_lists().getByTitle('Announcements');
    this.oListItem = oList.getItemById(itemId);
    oListItem.deleteObject();

    clientContext.executeQueryAsync(
        Function.createDelegate(this, this.onQuerySucceeded), 
        Function.createDelegate(this, this.onQueryFailed)
    );
}

function onQuerySucceeded() {
    alert('Item deleted: ' + itemId);
}

function onQueryFailed(sender, args) {
    alert('Request failed. ' + args.get_message() + 
        '\n' + args.get_stackTrace());
}
```
<br/>

<span data-ttu-id="16d7a-p129">Если, например, требуется получить новое количество элементов, появившееся в результате операции удаления, следует включить вызов метода update(), чтобы обновить список. Кроме того, перед выполнением запроса необходимо загрузить либо сам объект "list", либо его свойство **itemCount**. Если требуется получить как исходное, так и итоговое количество элементов списка, то необходимо выполнить два запроса и получить число элементов дважды, как показано в следующем варианте предыдущего примера.</span><span class="sxs-lookup"><span data-stu-id="16d7a-p129">If you want to retrieve, for example, the new item count that results from a delete operation, include a call to the update() method to refresh the list. In addition, you must load either the list object itself or the **itemCount** property on the list object before executing the query. If you want to retrieve both a start and end count of the list items, you must execute two queries and return the item count twice, as shown in the following modification of the previous example.</span></span>

```
function deleteListItemDisplayCount(siteUrl) {
    this.clientContext = new SP.ClientContext(siteUrl);
    this.oList = clientContext.get_web().get_lists().getByTitle('Announcements');
    clientContext.load(oList);

    clientContext.executeQueryAsync(
        Function.createDelegate(this, this.deleteItem), 
        Function.createDelegate(this, this.onQueryFailed)
    );
}

function deleteItem() {
    this.itemId = 58;
    this.startCount = oList.get_itemCount();
    this.oListItem = oList.getItemById(itemId);
    oListItem.deleteObject();

    oList.update();
    clientContext.load(oList);
        
    clientContext.executeQueryAsync(
        Function.createDelegate(this, this.displayCount), 
        Function.createDelegate(this, this.onQueryFailed)
    );
}

function displayCount() {
    var endCount = oList.get_itemCount();
    var listItemInfo = 'Item deleted: ' + itemId + 
        '\nStart Count: ' +  startCount + 
        ' End Count: ' + endCount;
        
    alert(listItemInfo)
}

function onQueryFailed(sender, args) {
    alert('Request failed. ' + args.get_message() + 
        '\n' + args.get_stackTrace());
}
```

<br/>

<span data-ttu-id="16d7a-253"><a name="BasicOps_AccessHostweb"> </a></span><span class="sxs-lookup"><span data-stu-id="16d7a-253"></span></span>

## <a name="access-objects-in-the-host-web"></a><span data-ttu-id="16d7a-254">Доступ к объектам на хост-сайте</span><span class="sxs-lookup"><span data-stu-id="16d7a-254">Access objects in the host web</span></span>

<span data-ttu-id="16d7a-p130">При разработке надстройки может потребоваться доступ к хост-сайту для работы с элементами на нем. Используйте объект **AppContextSite** для ссылки на хост-сайт или другие сайты SharePoint, как показано в следующем примере. Полный пример кода см. в разделе [Получение названия хост-сайта с помощью междоменной библиотеки (JSOM)](http://code.msdn.microsoft.com/office/SharePoint-Get-the-563f2a3d).</span><span class="sxs-lookup"><span data-stu-id="16d7a-p130">While developing your add-in, you might need to access the host web to interact with items in it. Use the **AppContextSite** object to reference the host web or other SharePoint sites, as shown in the following example. For a full code sample, see [Get the host web title using the cross-domain library (JSOM)](http://code.msdn.microsoft.com/office/SharePoint-Get-the-563f2a3d).</span></span>

```
function execCrossDomainRequest(appweburl, hostweburl) {
    // context: The ClientContext object provides access to
    //      the web and lists objects.
    // factory: Initialize the factory object with the
    //      add-in web URL.
    var context;
    var factory;
    var appContextSite;

    context = new SP.ClientContext(appweburl);
    factory = new SP.ProxyWebRequestExecutorFactory(appweburl);
    context.set_webRequestExecutorFactory(factory);
    appContextSite = new SP.AppContextSite(context, hostweburl);

    this.web = appContextSite.get_web();
    context.load(this.web);

    // Execute the query with all the previous 
    //  options and parameters.
    context.executeQueryAsync(
        Function.createDelegate(this, successHandler), 
        Function.createDelegate(this, errorHandler)
    );

    // Function to handle the success event.
    // Prints the host web's title to the page.
    function successHandler() {
        alert(this.web.get_title());
    }

    // Function to handle the error event.
    // Prints the error message to the page.
    function errorHandler(data, errorCode, errorMessage) {
        alert("Could not complete cross-domain call: " + errorMessage);
    }
}
```

<br/>

<span data-ttu-id="16d7a-258">В предыдущем примере для доступа к хост-сайту используется междоменная библиотека в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="16d7a-258">The previous example uses the cross-domain library in SharePoint to access the host web. For more information, see  Access SharePoint data from add-ins using the cross-domain library.</span></span> <span data-ttu-id="16d7a-259">Дополнительные сведения см. в статье [Обращение к данным SharePoint из надстроек с помощью междоменной библиотеки](access-sharepoint-data-from-add-ins-using-the-cross-domain-library.md).</span><span class="sxs-lookup"><span data-stu-id="16d7a-259">For more information, see [Access SharePoint data from add-ins using the cross-domain library](access-sharepoint-data-from-add-ins-using-the-cross-domain-library.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="16d7a-260">См. также</span><span class="sxs-lookup"><span data-stu-id="16d7a-260">See also</span></span>
<span data-ttu-id="16d7a-261"><a name="BasicOps_AddRes"> </a></span><span class="sxs-lookup"><span data-stu-id="16d7a-261"></span></span>

- [<span data-ttu-id="16d7a-262">Разработка надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="16d7a-262">Develop SharePoint Add-ins</span></span>](develop-sharepoint-add-ins.md)
- [<span data-ttu-id="16d7a-263">Безопасный доступ к данным и клиентские объектные модели для надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="16d7a-263">Secure data access and client object models for SharePoint Add-ins</span></span>](secure-data-access-and-client-object-models-for-sharepoint-add-ins.md)
- [<span data-ttu-id="16d7a-264">Работа с внешними данными в SharePoint</span><span class="sxs-lookup"><span data-stu-id="16d7a-264">Work with external data in SharePoint</span></span>](work-with-external-data-in-sharepoint.md)
    
 

