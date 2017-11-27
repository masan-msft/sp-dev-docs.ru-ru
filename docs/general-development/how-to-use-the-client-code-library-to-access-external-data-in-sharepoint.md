---
title: "Использование клиентской библиотеки кода для доступа к внешним данным в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: c280ae92-c52b-4658-b0f3-805fb215ef8e
ms.openlocfilehash: 2f4e7a87db95ee5d1105111a5f5cdab9d1d6242b
ms.sourcegitcommit: f6ea922341c38e700d0697961f8df9a454a03cba
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/15/2017
---
# <a name="use-the-client-code-library-to-access-external-data-in-sharepoint"></a><span data-ttu-id="a15a6-102">Использование клиентской библиотеки кода для доступа к внешним данным в SharePoint</span><span class="sxs-lookup"><span data-stu-id="a15a6-102">Use the client code library to access external data in SharePoint</span></span>

<span data-ttu-id="a15a6-103">Сведения об использовании клиентской объектной модели SharePoint для работы с объектами Business Connectivity Services (BCS) в SharePoint с использованием сценариев на основе браузера.</span><span class="sxs-lookup"><span data-stu-id="a15a6-103">Learn how to use the SharePoint client object model to work with Business Connectivity Services (BCS) objects in SharePoint using browser-based scripting.</span></span>

<span data-ttu-id="a15a6-104">В этой статье показано, как настроить внешний список, который получает данные из источника Open Data protocol (OData) с помощью клиентской объектной модели в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="a15a6-104">This article demonstrates how to set up an external list that retrieves data from an Open Data protocol (OData) source using the client object model in SharePoint.</span></span>
  
    
    


## <a name="prerequisites-for-accessing-external-data-using-the-sharepoint-client-object-model"></a><span data-ttu-id="a15a6-105">Необходимые условия для доступа к внешним данным с помощью клиентской объектной модели SharePoint</span><span class="sxs-lookup"><span data-stu-id="a15a6-105">Prerequisites for accessing external data using the SharePoint client object model</span></span>
<span data-ttu-id="a15a6-106"><a name="bkmk_Prerequisites"> </a></span><span class="sxs-lookup"><span data-stu-id="a15a6-106"></span></span>

<span data-ttu-id="a15a6-107">Ниже приведены требования к возможности разработки приложений с использованием клиентской объектной модели SharePoint.</span><span class="sxs-lookup"><span data-stu-id="a15a6-107">The following are requirements for being able to develop apps using the SharePoint client object model:</span></span>
  
    
    

- <span data-ttu-id="a15a6-108">SharePoint</span><span class="sxs-lookup"><span data-stu-id="a15a6-108">SharePoint</span></span>
    
  
- <span data-ttu-id="a15a6-109">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="a15a6-109">Visual Studio 2012</span></span>
    
  
- <span data-ttu-id="a15a6-110">Инструменты разработчика Office для Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="a15a6-110">Office Developer Tools for Visual Studio 2012</span></span>
    
  
- <span data-ttu-id="a15a6-111">Работает среды разработки SharePoint надстройки: следуйте инструкциям в [настроить среду разработки, общие для SharePoint](set-up-a-general-development-environment-for-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="a15a6-111">A functioning SharePoint Add-ins development environment: Follow the instructions in  [Set up a general development environment for SharePoint](set-up-a-general-development-environment-for-sharepoint.md).</span></span>
    
  
- <span data-ttu-id="a15a6-112">Доступ к общедоступной поставщики OData.org</span><span class="sxs-lookup"><span data-stu-id="a15a6-112">Access to the public OData.org producers</span></span>
    
  

### <a name="core-concepts-to-know-when-accessing-external-data-with-the-sharepoint-client-object-model"></a><span data-ttu-id="a15a6-113">Основные понятия, которые необходимо знать при доступе к внешним данным с помощью клиентской объектной модели SharePoint</span><span class="sxs-lookup"><span data-stu-id="a15a6-113">Core concepts to know when accessing external data with the SharePoint client object model</span></span>

<span data-ttu-id="a15a6-114">Клиентская объектная модель SharePoint предоставляет способ доступа к внешним данным с помощью клиентских вызовов, которые копируют интерфейсов API на сервере.</span><span class="sxs-lookup"><span data-stu-id="a15a6-114">The SharePoint client object model provides a way to access external data using client-side calls that mimic the server-side APIs.</span></span> <span data-ttu-id="a15a6-115">Чтобы понять, как это работает и как его использовать, обратитесь к статьям в таблице 1.</span><span class="sxs-lookup"><span data-stu-id="a15a6-115">To understand how it works and how to use it, see the articles in Table 1.</span></span>
  
    
    

<span data-ttu-id="a15a6-116">**В таблице 1. Основные понятия, которые по использованию клиентской объектной модели**</span><span class="sxs-lookup"><span data-stu-id="a15a6-116">**Table 1. Core concepts for using the client object model**</span></span>


|<span data-ttu-id="a15a6-117">**Статья**</span><span class="sxs-lookup"><span data-stu-id="a15a6-117">**Article**</span></span>|<span data-ttu-id="a15a6-118">**Описание**</span><span class="sxs-lookup"><span data-stu-id="a15a6-118">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="a15a6-119">Выполнение базовых операций с использованием кода библиотеки клиента в SharePoint</span><span class="sxs-lookup"><span data-stu-id="a15a6-119">Complete basic operations using SharePoint client library code</span></span>](http://msdn.microsoft.com/library/5a69c9e3-73bf-4ed5-bc19-182056bdb394%28Office.15%29.aspx) <br/> |<span data-ttu-id="a15a6-120">Узнайте, как писать код выполните основные операции с клиента SharePoint .NET Framework объектной модели (CSOM).</span><span class="sxs-lookup"><span data-stu-id="a15a6-120">Learn how to write code to peform basic operations with the SharePoint .NET Framework client object model (CSOM).</span></span>  <br/> |
   

## <a name="create-an-sharepoint-add-in-to-access-external-data-using-the-client-object-model"></a><span data-ttu-id="a15a6-121">Создание Надстройка SharePoint для доступа к внешним данным с помощью клиентской объектной модели</span><span class="sxs-lookup"><span data-stu-id="a15a6-121">Create an SharePoint Add-in to access external data using the client object model</span></span>
<span data-ttu-id="a15a6-122"><a name="bkmk_CreateApp"> </a></span><span class="sxs-lookup"><span data-stu-id="a15a6-122"></span></span>

<span data-ttu-id="a15a6-123">Следующих процедурах показано, как настроить Надстройка SharePoint и настройка веб-страницы мог выполнять запросы, с помощью метода объектной модели клиента и объектов для извлечения данных из внешнего источника данных.</span><span class="sxs-lookup"><span data-stu-id="a15a6-123">The following procedures show how to set up an SharePoint Add-in and configure a webpage to make requests using client object model methods and objects to retrieve data from an external data source.</span></span>
  
    
    

### <a name="to-create-an-sharepoint-add-in"></a><span data-ttu-id="a15a6-124">Создание Надстройка SharePoint</span><span class="sxs-lookup"><span data-stu-id="a15a6-124">To create an SharePoint Add-in</span></span>


1. <span data-ttu-id="a15a6-125">Откройте Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="a15a6-125">Open Visual Studio 2012.</span></span>
    
  
2. <span data-ttu-id="a15a6-126">Создайте проект **приложения для SharePoint** .</span><span class="sxs-lookup"><span data-stu-id="a15a6-126">Create an **App for SharePoint** project.</span></span>
    
  
3. <span data-ttu-id="a15a6-p102">Укажите параметры приложения, включая имя приложения, URL-адрес сайта для отладки приложения, и как будут размещены приложения (автоматическим размещением, размещением у поставщика, размещенных в SharePoint). Дополнительные сведения о параметры размещения можно  [Выбор шаблонов для разработки и размещения надстройки SharePoint](http://msdn.microsoft.com/library/05ce5435-0a03-4ddc-976b-c33b08d03457%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="a15a6-p102">Specify the app settings, including app name, the site URL for debugging the app, and how you want to host the app (Autohosted, Provider-hosted, SharePoint-hosted). For more information about hosting options, see  [Choose patterns for developing and hosting your SharePoint Add-in](http://msdn.microsoft.com/library/05ce5435-0a03-4ddc-976b-c33b08d03457%28Office.15%29.aspx).</span></span>
    
  
4. <span data-ttu-id="a15a6-129">Нажмите кнопку **Готово** для создания приложения.</span><span class="sxs-lookup"><span data-stu-id="a15a6-129">Click **Finish** to create the app.</span></span>
    
  

### <a name="to-generate-the-external-content-type"></a><span data-ttu-id="a15a6-130">Для создания внешнего типа контента</span><span class="sxs-lookup"><span data-stu-id="a15a6-130">To generate the external content type</span></span>


1. <span data-ttu-id="a15a6-131">В **Обозревателе решений** откройте контекстное меню для проекта и выберите команду **Добавить**, **типы контента для внешнего источника данных**.</span><span class="sxs-lookup"><span data-stu-id="a15a6-131">In **Solution Explorer**, open the shortcut menu for the project, and choose **Add**, **Content types for External Data source**.</span></span>
    
  
2. <span data-ttu-id="a15a6-p103">В мастере **Укажите источника OData** введите URL-адрес службы OData, чтобы подключиться к. В этом случае будет использоваться источника Northwind OData, опубликованные в [http://www.odata.org/ecosystem](http://www.odata.org/ecosystem). Задать URL-адрес для службы OData  `http://services.odata.org/Northwind/Northwind.svc/`</span><span class="sxs-lookup"><span data-stu-id="a15a6-p103">In the **Specify OData Source** wizard, enter the URL of the OData service that you want to connect to. In this case, you will use the Northwind OData source published at [http://www.odata.org/ecosystem](http://www.odata.org/ecosystem). Set the URL for the OData service to  `http://services.odata.org/Northwind/Northwind.svc/`</span></span>
    
    <span data-ttu-id="a15a6-135">Укажите имя для источника данных и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="a15a6-135">Specify a name for the data source, and choose **Next**.</span></span>
    
  
3. <span data-ttu-id="a15a6-p104">Появится список сущностей, предоставляемые интерфейсом службы OData. Выберите сущности **клиентов**. Убедитесь, что установлен флажок **создать экземпляры списков для выбранных данных сущностей (за исключением операции службы)**.</span><span class="sxs-lookup"><span data-stu-id="a15a6-p104">A list of entities that are exposed by the OData Service will appear. Choose the **Customers** entity. Ensure that the **Create list instances for the selected data entities (except Service Operations)** check box is selected.</span></span>
    
  
4. <span data-ttu-id="a15a6-139">Нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="a15a6-139">Choose **Finish**.</span></span>
    
  

## <a name="code-example-add-scripts-and-html-to-the-defaultaspx-page"></a><span data-ttu-id="a15a6-140">Пример кода: Добавление скриптов и HTML-код на страницу Default.aspx</span><span class="sxs-lookup"><span data-stu-id="a15a6-140">Code example: Add scripts and HTML to the Default.aspx page</span></span>
<span data-ttu-id="a15a6-141"><a name="bkmk_AddUIelements"> </a></span><span class="sxs-lookup"><span data-stu-id="a15a6-141"></span></span>

<span data-ttu-id="a15a6-142">На этом этапе у вас есть внешнего типа контента и внешний список, который отображает данные из источника Netflix OData.</span><span class="sxs-lookup"><span data-stu-id="a15a6-142">At this point, you have the external content type and an external list that displays the data from the Netflix OData source.</span></span> 
  
    
    
<span data-ttu-id="a15a6-p105">Далее цель  это изменение страницы default.aspx, созданный при создании приложения. Добавить контейнер, который будет использоваться для хранения результатов запроса, который выполняется с помощью загрузки страницы. Выполнение сценариев на события загрузки страницы, позволяет гарантировать, что скрипт будет выполняться каждый раз при просмотре страницы, а полученные вызовы объектной модели клиента будет создан источник Netflix OData для добавления записей на страницу.</span><span class="sxs-lookup"><span data-stu-id="a15a6-p105">The next objective is to modify the default.aspx page that you created when you created your app. You add a container that will hold the results of the query that is executed with the page loads. By executing the scripts on the page load event, you ensure that the script will be executed every time the page is browsed, and the resulting client object model calls will be made to the Netflix OData source to add records to the page.</span></span> 
  
    
    

### <a name="to-add-the-container-to-the-defaultaspx-page"></a><span data-ttu-id="a15a6-146">Чтобы добавить в контейнер на страницу Default.aspx</span><span class="sxs-lookup"><span data-stu-id="a15a6-146">To add the container to the Default.aspx page</span></span>


1. <span data-ttu-id="a15a6-147">В **Обозревателе решений** откройте страницу Default.aspx, расположенной в модуле **страниц**.</span><span class="sxs-lookup"><span data-stu-id="a15a6-147">In **Solution Explorer**, open the Default.aspx page located in the **Pages** module.</span></span>
    
  
2. <span data-ttu-id="a15a6-148">Добавьте следующий элемент **div** на страницу:</span><span class="sxs-lookup"><span data-stu-id="a15a6-148">Add the following **div** element to the page:</span></span>
    
```HTML
  
<div id="displayDiv"></div>
```

3. <span data-ttu-id="a15a6-149">Сохраните страницу.</span><span class="sxs-lookup"><span data-stu-id="a15a6-149">Save the page.</span></span>
    
  
<span data-ttu-id="a15a6-150">И, наконец добавьте код в файл App.js, который выполняется при загрузке страницы.</span><span class="sxs-lookup"><span data-stu-id="a15a6-150">Finally, you add code to the App.js file that executes when the page loads.</span></span>
  
    
    

### <a name="to-modify-the-appjs-file-to-make-client-object-model-calls"></a><span data-ttu-id="a15a6-151">Чтобы изменить файл App.js для облегчения клиента вызывает объектной модели</span><span class="sxs-lookup"><span data-stu-id="a15a6-151">To modify the App.js file to make client object model calls</span></span>


1. <span data-ttu-id="a15a6-152">Откройте файл App.js в модуле сценариев проекта SharePoint.</span><span class="sxs-lookup"><span data-stu-id="a15a6-152">Open the App.js file in the Scripts module of your SharePoint project.</span></span>
    
  
2. <span data-ttu-id="a15a6-153">Вставьте следующий код в конец файла.</span><span class="sxs-lookup"><span data-stu-id="a15a6-153">Paste the following code at the end of the file.</span></span>
    
```
  $(document).ready(function () {

    // Namespace
    window.AppLevelECT = window.AppLevelECT || {};

    // Constructor
    AppLevelECT.Grid = function (hostElement, surlWeb) {
        this.hostElement = hostElement;
        if (surlWeb.length > 0 &amp;&amp; surlWeb.substring(surlWeb.length - 1, surlWeb.length) != "/")
            surlWeb += "/";
        this.surlWeb = surlWeb;
    }

    // Prototype
    AppLevelECT.Grid.prototype = {

        init: function () {

            $.ajax({
                url: this.surlWeb + "_api/lists/getbytitle('Customer')/items?$select=BdcIdentity,CustomerID,ContactName",
                headers: {
                    "accept": "application/json",
                    "X-RequestDigest": $("#__REQUESTDIGEST").val()
                },
                success: this.showItems
            });
        },

        showItems: function (data) {
            var items = [];

            items.push("<table>");
            items.push('<tr><td>Customer ID</td><td>Customer Name</td></tr>');

            $.each(data.d.results, function (key, val) {
                items.push('<tr id="' + val.BdcIdentity + '"><td>' +
                    val.CustomerID + '</td><td>' +
                    val.ContactName + '</td></tr>');
            });

            items.push("</table>");

            $("#displayDiv").html(items.join(''));
        }
    }

    ExecuteOrDelayUntilScriptLoaded(getCustomers, "sp.js");
});

function getCustomers() {
    var grid = new AppLevelECT.Grid($("#displayDiv"), _spPageContextInfo.webServerRelativeUrl);
    grid.init();
}
```

<span data-ttu-id="a15a6-p106">Нажмите клавишу F5, чтобы развернуть приложение для SharePoint. Перейдите на страницу Default.aspx в приложении и на странице отображается список клиентов.</span><span class="sxs-lookup"><span data-stu-id="a15a6-p106">Press F5 to deploy the app to SharePoint. Browse to the Default.aspx page in the app, and a list of customers appears on the page.</span></span>
  
    
    

## <a name="additional-resources"></a><span data-ttu-id="a15a6-156">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="a15a6-156">Additional resources</span></span>
<span data-ttu-id="a15a6-157"><a name="bkmk_Addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="a15a6-157"></span></span>


-  [<span data-ttu-id="a15a6-158">Business Connectivity Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="a15a6-158">Business Connectivity Services in SharePoint</span></span>](business-connectivity-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="a15a6-159">Начало работы с помощью клиентской объектной модели с внешними данными в SharePoint</span><span class="sxs-lookup"><span data-stu-id="a15a6-159">Get started using the client object model with external data in SharePoint</span></span>](get-started-using-the-client-object-model-with-external-data-in-sharepoint.md)
    
  
-  [<span data-ttu-id="a15a6-160">Надстройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="a15a6-160">SharePoint Add-ins</span></span>](http://msdn.microsoft.com/library/cd1eda9e-8e54-4223-93a9-a6ea0d18df70%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="a15a6-161">Выбор шаблонов для разработки и размещения надстройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="a15a6-161">Choose patterns for developing and hosting your SharePoint Add-in</span></span>](http://msdn.microsoft.com/library/05ce5435-0a03-4ddc-976b-c33b08d03457%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="a15a6-162">BCS клиента Справочник по объектной модели для SharePoint</span><span class="sxs-lookup"><span data-stu-id="a15a6-162">BCS client object model reference for SharePoint</span></span>](bcs-client-object-model-reference-for-sharepoint.md)
    
  
-  [<span data-ttu-id="a15a6-163">Новые возможности служб Business Connectivity Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="a15a6-163">What's new in Business Connectivity Services in SharePoint</span></span>](what-s-new-in-business-connectivity-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="a15a6-164">Выполнение базовых операций с использованием кода библиотеки клиента в SharePoint</span><span class="sxs-lookup"><span data-stu-id="a15a6-164">Complete basic operations using SharePoint client library code</span></span>](http://msdn.microsoft.com/library/5a69c9e3-73bf-4ed5-bc19-182056bdb394%28Office.15%29.aspx)
    
  

