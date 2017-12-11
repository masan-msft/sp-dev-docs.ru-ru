---
title: "Доступ к внешним данным с помощью REST в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 0663cc8c-a736-434d-9858-6ce12ce7f748
ms.openlocfilehash: 9b1cab4d79db115c705cf0264bafee0593dfd5bc
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="access-external-data-by-using-rest-in-sharepoint"></a><span data-ttu-id="7b4cd-102">Доступ к внешним данным с помощью REST в SharePoint</span><span class="sxs-lookup"><span data-stu-id="7b4cd-102">Access external data by using REST in SharePoint</span></span>

<span data-ttu-id="7b4cd-103">Узнайте, как получить доступ к внешним данным из SharePoint с помощью представлений состояния (REST) URL-адреса Business Connectivity Services (BCS).</span><span class="sxs-lookup"><span data-stu-id="7b4cd-103">Learn how to access external data from SharePoint by using Representational State Transfer (REST) URLs for Business Connectivity Services (BCS).</span></span>
<span data-ttu-id="7b4cd-104">В этой статье показано, как настроить внешний список, который получает данные из источника Open Data protocol (OData).</span><span class="sxs-lookup"><span data-stu-id="7b4cd-104">This article shows how to set up an external list that retrieves data from an Open Data protocol (OData) source.</span></span>
  
    
    


## <a name="prerequisites-for-accessing-external-data-using-rest"></a><span data-ttu-id="7b4cd-105">Необходимые условия для доступа к внешним данным использовать REST</span><span class="sxs-lookup"><span data-stu-id="7b4cd-105">Prerequisites for accessing external data using REST</span></span>
<span data-ttu-id="7b4cd-106"><a name="bkmk_Prerequisites"> </a></span><span class="sxs-lookup"><span data-stu-id="7b4cd-106"></span></span>

<span data-ttu-id="7b4cd-107">Для доступа к внешним данным из SharePoint с помощью REST, вам необходимо следующее:</span><span class="sxs-lookup"><span data-stu-id="7b4cd-107">To access external data from SharePoint by using REST, you need the following:</span></span>
  
    
    

- <span data-ttu-id="7b4cd-108">SharePoint</span><span class="sxs-lookup"><span data-stu-id="7b4cd-108">SharePoint</span></span>
    
  
- <span data-ttu-id="7b4cd-109">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="7b4cd-109">Visual Studio 2012</span></span>
    
  
- <span data-ttu-id="7b4cd-110">Инструменты разработчика Office для Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="7b4cd-110">Office Developer Tools for Visual Studio 2012</span></span>
    
  
- <span data-ttu-id="7b4cd-111">Работает среды разработки SharePoint надстройки: следуйте инструкциям в [настроить среду разработки, общие для SharePoint](set-up-a-general-development-environment-for-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="7b4cd-111">A functioning SharePoint Add-ins development environment: Follow the instructions in  [Set up a general development environment for SharePoint](set-up-a-general-development-environment-for-sharepoint.md).</span></span>
    
  
- <span data-ttu-id="7b4cd-112">Доступ к общедоступной поставщики OData.org</span><span class="sxs-lookup"><span data-stu-id="7b4cd-112">Access to the public OData.org producers</span></span>
    
  

### <a name="core-concepts-to-know-when-accessing-external-data-with-rest"></a><span data-ttu-id="7b4cd-113">Основные понятия, которые необходимо знать при доступе к внешним данным с помощью REST</span><span class="sxs-lookup"><span data-stu-id="7b4cd-113">Core concepts to know when accessing external data with REST</span></span>

<span data-ttu-id="7b4cd-114">Службы SharePoint REST предоставляет способ доступа к внешним данным с помощью специально созданного URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="7b4cd-114">The SharePoint REST service provides a way to access external data using a specially constructed URL.</span></span> <span data-ttu-id="7b4cd-115">Чтобы понять, как это работает и как его использовать, обратитесь к следующим документам.</span><span class="sxs-lookup"><span data-stu-id="7b4cd-115">To understand how it works and how to use it, see the following articles.</span></span>
  
    
    

<span data-ttu-id="7b4cd-116">**В таблице 1. Основные понятия, которые REST в SharePoint**</span><span class="sxs-lookup"><span data-stu-id="7b4cd-116">**Table 1. Core concepts for REST in SharePoint**</span></span>


|<span data-ttu-id="7b4cd-117">**Название статьи**</span><span class="sxs-lookup"><span data-stu-id="7b4cd-117">**Article title**</span></span>|<span data-ttu-id="7b4cd-118">**Описание**</span><span class="sxs-lookup"><span data-stu-id="7b4cd-118">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="7b4cd-119">Программирование с использованием службы SharePoint 2013 REST</span><span class="sxs-lookup"><span data-stu-id="7b4cd-119">Use OData query operations in SharePoint REST requests</span></span>](http://msdn.microsoft.com/library/d4b5c277-ed50-420c-8a9b-860342284b72%28Office.15%29.aspx) <br/> |<span data-ttu-id="7b4cd-120">Узнайте, как использовать службы SharePoint REST, содержащей REST, интерфейс сравнимые существующей клиентской объектной модели программирования.</span><span class="sxs-lookup"><span data-stu-id="7b4cd-120">Learn how to use the SharePoint REST service, which provides a REST programming interface comparable to the existing client object model.</span></span>  <br/> |
| [<span data-ttu-id="7b4cd-121">Знакомство со службой REST в SharePoint</span><span class="sxs-lookup"><span data-stu-id="7b4cd-121">Get to know the SharePoint REST service</span></span>](http://msdn.microsoft.com/library/2de035a0-ac75-43bd-9665-5c5a59c4c590%28Office.15%29.aspx) <br/> |<span data-ttu-id="7b4cd-122">Основы использования службы REST в SharePoint для чтения и изменения данных в SharePoint по веб-протоколам REST и OData.</span><span class="sxs-lookup"><span data-stu-id="7b4cd-122">Get the basics of using the SharePoint REST service to access and update SharePoint data, using the REST and OData web protocol standards.</span></span>  <br/> |
| [<span data-ttu-id="7b4cd-123">С помощью службы SharePoint REST</span><span class="sxs-lookup"><span data-stu-id="7b4cd-123">Using the SharePoint REST service</span></span>](http://msdn.microsoft.com/library/e1ff2979-1c16-4cb0-a57e-9168dfe20a7c.aspx) <br/> |<span data-ttu-id="7b4cd-124">Узнайте, как для перемещения по структуре данных SharePoint, представленным в службе REST, выполнять распространенные CRUD (Создание, чтение, обновление и удаление) операций для элементов SharePoint с помощью службы REST синхронизация элементов SharePoint в приложениях и управления параллелизм элемента.</span><span class="sxs-lookup"><span data-stu-id="7b4cd-124">Learn how to navigate the SharePoint data structure as it is represented in the REST service, perform common CRUD (create, read, update, and delete) operations on SharePoint items via the REST service, synchronize SharePoint items across applications, and control item concurrency.</span></span>  <br/> |
   

## <a name="create-an-sharepoint-add-in-to-access-external-data-using-rest"></a><span data-ttu-id="7b4cd-125">Создание Надстройка SharePoint для доступа к внешним данным использовать REST</span><span class="sxs-lookup"><span data-stu-id="7b4cd-125">Create an SharePoint Add-in to access external data using REST</span></span>
<span data-ttu-id="7b4cd-126"><a name="bkmk_CreateApp"> </a></span><span class="sxs-lookup"><span data-stu-id="7b4cd-126"></span></span>

<span data-ttu-id="7b4cd-127">Следующие процедуры рекомендации по установке Надстройка SharePoint и настройке веб-страницы мог выполнять запросы, с помощью функции REST для извлечения данных из внешнего источника данных.</span><span class="sxs-lookup"><span data-stu-id="7b4cd-127">The following procedures guide you through setting up an SharePoint Add-in and configuring a webpage to make requests using REST functions to retrieve data from an external data source.</span></span>
  
    
    

### <a name="to-create-an-sharepoint-add-in"></a><span data-ttu-id="7b4cd-128">Создание Надстройка SharePoint</span><span class="sxs-lookup"><span data-stu-id="7b4cd-128">To create an SharePoint Add-in</span></span>


1. <span data-ttu-id="7b4cd-129">Откройте Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="7b4cd-129">Open Visual Studio 2012.</span></span>
    
  
2. <span data-ttu-id="7b4cd-130">Создайте проект **приложения для SharePoint** .</span><span class="sxs-lookup"><span data-stu-id="7b4cd-130">Create an **App for SharePoint** project.</span></span>
    
  
3. <span data-ttu-id="7b4cd-p103">Укажите параметры приложения, включая имя приложения, URL-адрес сайта для отладки приложения, и как будут размещены приложения (автоматическим размещением, размещением у поставщика, размещенных в SharePoint). Дополнительные сведения о параметры размещения можно  [Выбор шаблонов для разработки и размещения надстройки SharePoint](http://msdn.microsoft.com/library/05ce5435-0a03-4ddc-976b-c33b08d03457%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="7b4cd-p103">Specify the app settings, including app name, the site URL for debugging the app, and how you want to host the app (Autohosted, Provider-hosted, SharePoint-hosted). For more information about hosting options, see  [Choose patterns for developing and hosting your SharePoint Add-in](http://msdn.microsoft.com/library/05ce5435-0a03-4ddc-976b-c33b08d03457%28Office.15%29.aspx).</span></span>
    
  
4. <span data-ttu-id="7b4cd-133">Нажмите кнопку **Готово**, чтобы создать приложение.</span><span class="sxs-lookup"><span data-stu-id="7b4cd-133">Choose **Finish** to create the app.</span></span>
    
  

### <a name="to-generate-the-external-content-type"></a><span data-ttu-id="7b4cd-134">Для создания внешнего типа контента</span><span class="sxs-lookup"><span data-stu-id="7b4cd-134">To generate the external content type</span></span>


1. <span data-ttu-id="7b4cd-135">В **Обозревателе решений** откройте контекстное меню для проекта и выберите команду **Добавить**, **Типы контента для внешнего источника данных**.</span><span class="sxs-lookup"><span data-stu-id="7b4cd-135">In **Solution Explorer**, open the shortcut menu for the project, and choose **Add**, **Content Types for External Data Source**.</span></span>
    
  
2. <span data-ttu-id="7b4cd-p104">На странице **Указание источника OData** введите URL-адрес службы OData, который требуется подключение к. В этом случае используйте источника Northwind OData, опубликованные в [http://www.odata.org/ecosystem](http://www.odata.org/ecosystem). Значение  `http://services.odata.org/Northwind/Northwind.svc/`URL-адрес для службы OData и укажите имя для источника данных.</span><span class="sxs-lookup"><span data-stu-id="7b4cd-p104">In the **Specify OData Source** page, enter the URL of the OData service you want to connect to. In this case, use the Northwind OData source published at [http://www.odata.org/ecosystem](http://www.odata.org/ecosystem). Set the URL for the OData service to  `http://services.odata.org/Northwind/Northwind.svc/`, and provide a name for the data source.</span></span>
    
    <span data-ttu-id="7b4cd-139">Нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="7b4cd-139">Choose **Next**.</span></span>
    
  
3. <span data-ttu-id="7b4cd-p105">Эта команда выводит список сущностей данные, предоставляемые интерфейсом службы OData. Выберите лицо, **Клиенты**. Убедитесь, что установлен флажок **создать экземпляры списков для выбранных данных сущностей (за исключением операции службы)**.</span><span class="sxs-lookup"><span data-stu-id="7b4cd-p105">This displays a list of data entities that are being exposed by the OData Service. Select the **Customers** entity. Ensure that the **Create list instances for the selected data entities (except Service Operations)** check box is selected.</span></span>
    
  
4. <span data-ttu-id="7b4cd-143">Нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="7b4cd-143">Choose **Finish**.</span></span>
    
  

## <a name="code-example-add-scripts-and-html-to-the-homeaspx-page"></a><span data-ttu-id="7b4cd-144">Пример кода: Добавление скриптов и HTML-код страницы Home.aspx</span><span class="sxs-lookup"><span data-stu-id="7b4cd-144">Code example: Add scripts and HTML to the Home.aspx page</span></span>
<span data-ttu-id="7b4cd-145"><a name="bkmk_AddUIelements"> </a></span><span class="sxs-lookup"><span data-stu-id="7b4cd-145"></span></span>

<span data-ttu-id="7b4cd-146">На этом этапе у вас есть внешнего типа контента и внешний список, который отображает данные из источника данных "Борей" OData.</span><span class="sxs-lookup"><span data-stu-id="7b4cd-146">At this point, you have an external content type and an external list that will display the data from the Northwind OData source.</span></span> 
  
    
    
<span data-ttu-id="7b4cd-p106">Далее основная задача заключается в том, чтобы изменить страницу default.aspx, созданную при создании приложения. Добавьте контейнер для хранения результатов запроса, который выполняется с помощью загрузки страницы. Выполнение сценариев на события загрузки страницы, убедитесь, что скрипт будет выполняться каждый раз при просмотре страницы, а полученные вызовы REST выполняются в источник данных "Борей" OData для добавления записей на страницу.</span><span class="sxs-lookup"><span data-stu-id="7b4cd-p106">The next objective is to modify the default.aspx page that was created when you created your app. You will add a container to hold the results of the query that is executed with the page loads. By executing the scripts on the page load event, you ensure that the script is executed every time the page is browsed, and the resulting REST calls are made to the Northwind OData source to add records to the page.</span></span>
  
    
    

### <a name="to-add-the-container-to-the-defaultaspx-page"></a><span data-ttu-id="7b4cd-150">Чтобы добавить в контейнер на страницу Default.aspx</span><span class="sxs-lookup"><span data-stu-id="7b4cd-150">To add the container to the Default.aspx page</span></span>


1. <span data-ttu-id="7b4cd-151">В **Обозревателе решений** откройте страницу Default.aspx в модуле **страниц**.</span><span class="sxs-lookup"><span data-stu-id="7b4cd-151">In **Solution Explorer**, open the Default.aspx page in the **Pages** module.</span></span>
    
  
2. <span data-ttu-id="7b4cd-152">Добавьте следующий элемент **div** на страницу.</span><span class="sxs-lookup"><span data-stu-id="7b4cd-152">Add the following **div** element to the page.</span></span>
    
```HTML
  
<div id="displayDiv"></div>
```

3. <span data-ttu-id="7b4cd-153">Сохраните страницу.</span><span class="sxs-lookup"><span data-stu-id="7b4cd-153">Save the page.</span></span>
    
  
<span data-ttu-id="7b4cd-154">И, наконец добавьте код в файл App.js, который выполняется при загрузке страницы.</span><span class="sxs-lookup"><span data-stu-id="7b4cd-154">Finally, you add code to the App.js file that executes when the page loads.</span></span>
  
    
    

### <a name="to-modify-the-appjs-file-to-make-rest-calls"></a><span data-ttu-id="7b4cd-155">Чтобы изменить файл App.js для выполнения вызовов REST</span><span class="sxs-lookup"><span data-stu-id="7b4cd-155">To modify the App.js file to make REST calls</span></span>


1. <span data-ttu-id="7b4cd-156">Откройте файл App.js в модуле сценариев проекта SharePoint.</span><span class="sxs-lookup"><span data-stu-id="7b4cd-156">Open the App.js file in the Scripts module of your SharePoint project.</span></span>
    
  
2. <span data-ttu-id="7b4cd-157">Вставьте следующий код в конец файла.</span><span class="sxs-lookup"><span data-stu-id="7b4cd-157">Paste the following code at the end of the file.</span></span>
    
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

<span data-ttu-id="7b4cd-p107">Нажмите клавишу F5, чтобы развернуть приложение для SharePoint. Перейдите на страницу Default.aspx в приложении и на странице отображается список клиентов.</span><span class="sxs-lookup"><span data-stu-id="7b4cd-p107">Press F5 to deploy the app to SharePoint. Browse to the Default.aspx page in the app, and a list of customers appears on the page.</span></span>
  
    
    

## <a name="see-also"></a><span data-ttu-id="7b4cd-160">См. также</span><span class="sxs-lookup"><span data-stu-id="7b4cd-160">See also</span></span>
<span data-ttu-id="7b4cd-161"><a name="bkmk_Addres"> </a></span><span class="sxs-lookup"><span data-stu-id="7b4cd-161"></span></span>


-  [<span data-ttu-id="7b4cd-162">Business Connectivity Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="7b4cd-162">Business Connectivity Services in SharePoint</span></span>](business-connectivity-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="7b4cd-163">Знакомство со службой REST в SharePoint</span><span class="sxs-lookup"><span data-stu-id="7b4cd-163">Get to know the SharePoint REST service</span></span>](http://msdn.microsoft.com/library/2de035a0-ac75-43bd-9665-5c5a59c4c590%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="7b4cd-164">С помощью службы SharePoint REST</span><span class="sxs-lookup"><span data-stu-id="7b4cd-164">Using the SharePoint REST service</span></span>](http://msdn.microsoft.com/library/e1ff2979-1c16-4cb0-a57e-9168dfe20a7c.aspx)
    
  
-  [<span data-ttu-id="7b4cd-165">Добавьте в пределах внешних типов контента в SharePoint</span><span class="sxs-lookup"><span data-stu-id="7b4cd-165">Add-in-scoped external content types in SharePoint</span></span>](add-in-scoped-external-content-types-in-sharepoint.md)
    
  
-  [<span data-ttu-id="7b4cd-166">Новые возможности служб Business Connectivity Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="7b4cd-166">What's new in Business Connectivity Services in SharePoint</span></span>](what-s-new-in-business-connectivity-services-in-sharepoint.md)
    
  

