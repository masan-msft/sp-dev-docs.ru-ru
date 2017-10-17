---
title: "Обращение к данным SharePoint из надстроек с помощью междоменной библиотеки"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: e7b5afc5617df0998f34dc2d6e353ffd8a4d4998
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="access-sharepoint-data-from-add-ins-using-the-cross-domain-library"></a><span data-ttu-id="09261-102">Обращение к данным SharePoint из надстроек с помощью междоменной библиотеки</span><span class="sxs-lookup"><span data-stu-id="09261-102">Access SharePoint data from add-ins using the cross-domain library</span></span>
<span data-ttu-id="09261-103">Узнайте, как работать с данными на веб-сайте SharePoint из надстройки, используя междоменную библиотеку в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="09261-103">Learn how to access data in a SharePoint website from your add-in by using the cross domain library in SharePoint.</span></span>
 

 <span data-ttu-id="09261-p101">**Примечание.** В настоящее время идет процесс замены названия "приложения для SharePoint" названием "надстройки SharePoint". Во время этого процесса в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio может по-прежнему использоваться термин "приложения для SharePoint". Дополнительные сведения см. в статье [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="09261-p101">**Note**  The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see  [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span></span>
 

<span data-ttu-id="09261-p102">При создании надстроек SharePoint обычно необходимо объединять данные из различных источников. Но по [соображениям безопасности](http://msdn.microsoft.com/library/cc709423.aspx) используются механизмы блокировки, которые предотвращают одновременный обмен данными с несколькими доменами. Эти механизмы безопасности реализованы в большинстве браузеров, что усложняет или делает невозможным выполнение клиентских вызовов в разных доменах.</span><span class="sxs-lookup"><span data-stu-id="09261-p102">When you build SharePoint Add-ins, you usually have to incorporate data from various sources. But for  [security reasons](http://msdn.microsoft.com/library/cc709423.aspx), there are blocking mechanisms that prevent communication with more than one domain at a time. These security mechanisms are implemented in most browsers, making difficult or impossible to accomplish client-side calls across domains.</span></span>
 

<span data-ttu-id="09261-110">На рис. 1 показан заблокированный запрос для нескольких доменов.</span><span class="sxs-lookup"><span data-stu-id="09261-110">Figure 1 shows a blocked request across domains.</span></span>
 


<span data-ttu-id="09261-111">**Рис. 1. Заблокированный запрос в нескольких доменах**</span><span class="sxs-lookup"><span data-stu-id="09261-111">**Figure 1. Blocked request across domains**</span></span>

 
<span data-ttu-id="09261-p103">Когда пользователь запрашивает страницу из домена надстройки (1), коммуникации на стороне клиента привязаны только к этому домену. Надстройка может выполнять клиентские вызовы с этой страницы только для других ресурсов в том же домене. Однако надстройкам обычно требуются ресурсы из других доменов, например домена SharePoint, для реализации своих функций. В коде на странице можно попытаться отправить запрос домену SharePoint (2), который будет заблокирован браузером. Обычно появляется ошибка **Доступ запрещен**. Она не означает, что у вас нет разрешений для запрошенных ресурсов. Скорее всего, вы просто не можете отправлять запросы указанным ресурсам.</span><span class="sxs-lookup"><span data-stu-id="09261-p103">When a user requests a page from your add-in domain (1), the client-side communication is bound only to that domain. Your add-in can issue client-side calls from the page only to other resources in the same domain. However, add-ins usually require resources from other domains, such as the SharePoint domain, to fulfill their scenarios. In the code in your page, you may try to issue a request to the SharePoint domain (2), which is blocked by the browser. You usually see an  **Access is denied** error. The error doesn't imply that you don't have permissions to the requested resources but, most likely, you can't even issue a request to the mentioned resources.</span></span>
 
<span data-ttu-id="09261-p104">При использовании междоменной библиотеки веб-страницы надстройки могут получать доступ к данным в вашем домене надстройки и домене SharePoint. Междоменная библиотека — это клиентский вариант библиотеки в виде файла JavaScript (SP.RequestExecutor.js), расположенного на веб-сайте SharePoint, на который можно ссылаться в вашей удаленной надстройке. Она позволяет взаимодействовать с несколькими доменами на странице удаленной надстройки через прокси-сервер. Рекомендуем использовать библиотеку в том случае, если ваша надстройка выполняется на клиенте, а не на сервере, или при наличии таких барьеров, как брандмауэры, между SharePoint и вашей удаленной инфраструктурой. Вы можете получить доступ к данным на хост-сайте, например к спискам, с которыми взаимодействуют конечные пользователи, независимо от вашей надстройки, или к данным в веб-надстройке, таким как списки, настроенные для надстройки. Кроме того, вы можете получить доступ к другим семействам сайтов и веб-сайтам, если для надстройки настроены разрешения на уровне клиента и она развернута в пакетной установке с помощью каталога надстроек.</span><span class="sxs-lookup"><span data-stu-id="09261-p104">When you use the cross-domain library, the webpages in your add-in can access data in your add-in domain and the SharePoint domain. The cross-domain library is a client-side alternative in the form of a JavaScript file (SP.RequestExecutor.js) that is hosted in the SharePoint website that you can reference in your remote add-in. The cross-domain library lets you interact with more than one domain in your remote add-in page through a proxy. It is a good option if you like your add-in code to run on the client instead of on the server, and if there are connectivity barriers, such as firewalls, between SharePoint and your remote infrastructure. You can access data in the host web—for example, you can access lists that end users interact with regardless of your add-in. Or you can access data in the add-in web, such as lists specifically provisioned for your add-in. Add-ins can also access other site collections and websites as long as the add-in has tenant-scoped permissions and it has been deployed as a batch installation using the add-in catalog.</span></span>
 

 <span data-ttu-id="09261-p105">**Примечание.** В этом разделе **домен надстройки** означает домен, в котором размещаются страницы надстройки. Это может быть домен удаленной веб-надстройки с размещением у поставщика. Но страницы надстройки также могут содержаться в SharePoint на сайте надстройки и отправлять запросы в домен хост-сайта. В последнем случае домен надстройки — это домен сайта надстройки.</span><span class="sxs-lookup"><span data-stu-id="09261-p105">**Note**  In this topic,  **add-in domain** refers to the domain that hosts the add-in pages. This can be the domain of a remote web application in a provider-hosted, but add-in pages can also be on SharePoint in the add-in web and make calls to the host web domain. In the latter scenario, the add-in domain is the domain of the add-in web.</span></span>
 

<span data-ttu-id="09261-p106">В главном примере в данной статье показано, как создать надстройку, считывающую данные на сайте надстройки и отображающую их на веб-странице. В разделе  [Дальнейшие действия](access-sharepoint-data-from-add-ins-using-the-cross-domain-library.md#SP15Accessdatafromremoteapp_Next) показаны дополнительные сценарии, основанные на главном примере.</span><span class="sxs-lookup"><span data-stu-id="09261-p106">The main example in this article shows how to build an add-in that reads data on the add-in web and displays it in a webpage. The  [Next steps](access-sharepoint-data-from-add-ins-using-the-cross-domain-library.md#SP15Accessdatafromremoteapp_Next) section shows more scenarios that build on top of the main example.</span></span>
 

## <a name="prerequisites-for-using-the-examples-in-this-article"></a><span data-ttu-id="09261-130">Необходимые условия для использования примеров в этой статье</span><span class="sxs-lookup"><span data-stu-id="09261-130">Prerequisites for using the examples in this article</span></span>
<span data-ttu-id="09261-131"><a name="SP15Accessdatafromremoteapp_Prereq"> </a></span><span class="sxs-lookup"><span data-stu-id="09261-131"></span></span>

<span data-ttu-id="09261-132">Для выполнения примеров, описанных в этой статье, вам необходимо следующее:</span><span class="sxs-lookup"><span data-stu-id="09261-132">To follow the examples in this article, you need the following:</span></span>
 

 

-  [<span data-ttu-id="09261-133">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="09261-133">Visual Studio 2012</span></span>](https://www.microsoft.com/en-us/download/details.aspx?id=30682)
    
 
-  [<span data-ttu-id="09261-134">Инструменты разработчика Microsoft Office для Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="09261-134">Microsoft Office Developer Tools for Visual Studio 2012</span></span>](https://msdn.microsoft.com/en-us/office/aa905340.aspx)
    
 
- <span data-ttu-id="09261-135">Среда разработки SharePoint (для локальных сценариев необходима изоляция приложений)</span><span class="sxs-lookup"><span data-stu-id="09261-135">A SharePoint development environment (app isolation required for on-premises scenarios)</span></span>
    
 

## <a name="read-data-on-the-add-in-web-using-the-cross-domain-library"></a><span data-ttu-id="09261-136">Чтение данных с сайта надстройки с помощью междоменной библиотеки</span><span class="sxs-lookup"><span data-stu-id="09261-136">Read data on the add-in web using the cross-domain library</span></span>
<span data-ttu-id="09261-137"><a name="SP15Accessdatafromremoteapp_Codeexample"> </a></span><span class="sxs-lookup"><span data-stu-id="09261-137"></span></span>

<span data-ttu-id="09261-p107">В этом примере за пределами SharePoint размещена простая страница, которая использует конечную точку REST, чтобы читать данные на веб-сайте SharePoint (сайте надстройки). Так как для междоменной библиотеки требуется сайт надстройки, имеет смысл начать с этого сценария.</span><span class="sxs-lookup"><span data-stu-id="09261-p107">In this example, there is a simple page hosted outside of SharePoint that uses a Representational State Transfer (REST) endpoint to read data in a SharePoint website (the add-in web). Since the cross-domain library requires an add-in web, it makes sense to start with this scenario.</span></span>
 

 
<span data-ttu-id="09261-140">Для чтения данных с сайта надстройки вы должны сделать следующее:</span><span class="sxs-lookup"><span data-stu-id="09261-140">To read data from the add-in web, you must do the following:</span></span>
 

 

1. <span data-ttu-id="09261-141">Создайте Надстройка SharePoint и веб-проекты.</span><span class="sxs-lookup"><span data-stu-id="09261-141">Create a SharePoint Add-in and web projects.</span></span>
    
 
2. <span data-ttu-id="09261-p108">Создайте элементы списка на сайте надстройки. Этот шаг также гарантирует, что сайт надстройки будет создан, когда пользователи развернут надстройку.</span><span class="sxs-lookup"><span data-stu-id="09261-p108">Create list items in the add-in web. This step also ensures that an add-in web is created when users deploy the add-in.</span></span>
    
 
3. <span data-ttu-id="09261-144">Создайте страницу надстройки, которая использует междоменную библиотеку для чтения элементов списка.</span><span class="sxs-lookup"><span data-stu-id="09261-144">Create an add-in page that uses the cross-domain library to read the list items.</span></span>
    
 
<span data-ttu-id="09261-145">На рис. 2 показана веб-страница, на которой отображаются данные на сайте надстройки.</span><span class="sxs-lookup"><span data-stu-id="09261-145">Figure 2 shows a webpage that displays the data on the add-in web.</span></span>
 

 

<span data-ttu-id="09261-146">**Рис. 2. Веб-страница, на которой отображаются данные на сайте надстройки**</span><span class="sxs-lookup"><span data-stu-id="09261-146">**Figure 2. Webpage that displays the data on the add-in web**</span></span>

 

 
![Пример экрана с междоменными результатами чтения элементов](../images/CrossDomainReadItemsResult.png)
 

### <a name="create-a-sharepoint-add-in-and-web-projects"></a><span data-ttu-id="09261-148">Создание надстройки SharePoint и веб-проектов</span><span class="sxs-lookup"><span data-stu-id="09261-148">Create a SharePoint Add-in and web projects</span></span>


1. <span data-ttu-id="09261-p109">Откройте Visual Studio 2012 от имени администратора. Для этого щелкните правой кнопкой мыши значок Visual Studio 2012 в меню **Пуск** и выберите пункт **Запуск от имени администратора**.</span><span class="sxs-lookup"><span data-stu-id="09261-p109">Open Visual Studio 2012 as administrator. (To do this, right-click the Visual Studio 2012 icon on the  **Start** menu, and choose **Run as administrator**.)</span></span>
    
 
2. <span data-ttu-id="09261-151">Создайте новый проект с помощью шаблона **Надстройка для SharePoint**.</span><span class="sxs-lookup"><span data-stu-id="09261-151">Create a new project using the  **Add-in for SharePoint** template.</span></span>
    
    <span data-ttu-id="09261-152">Шаблон **Надстройка для SharePoint** в Visual Studio 2012 расположен в области **Шаблоны****>****Visual C#**, **Office SharePoint****>****Надстройки**.</span><span class="sxs-lookup"><span data-stu-id="09261-152">The  **Add-in for SharePoint** template in Visual Studio 2012 is located under **Templates** **>** **Visual C#**,  **Office SharePoint** **>** **Add-ins**.</span></span>
    
 
3. <span data-ttu-id="09261-153">Укажите URL-адрес веб-сайта SharePoint, который вы хотите использовать для отладки.</span><span class="sxs-lookup"><span data-stu-id="09261-153">Provide the SharePoint website URL that you want to use for debugging.</span></span>
    
 
4. <span data-ttu-id="09261-154">Выберите для надстройки вариант размещения **Размещено у поставщика**.</span><span class="sxs-lookup"><span data-stu-id="09261-154">Select  **Provider-hosted** as the hosting option for your add-in.</span></span>
    
     <span data-ttu-id="09261-p110">**Примечание.** Вы также можете использовать междоменную библиотеку в надстройке, размещаемой в SharePoint. Однако в такой надстройке ее страница уже находится на сайте надстройки, т. е. вам не нужна междоменная библиотека для чтения элементов списка. Пример такой надстройки, которая читает данные на хост-сайте, см. в статье, посвященной [использованию междоменной библиотеки в надстройке, размещаемой в SharePoint (REST)](http://code.msdn.microsoft.com/SharePoint-2013-Use-the-00c37814), или в разделе [Доступ к данным на хост-сайте](access-sharepoint-data-from-add-ins-using-the-cross-domain-library.md#SP15Accessdatafromremoteapp_Hostweb) далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="09261-p110">**Note**  You can also use the cross-domain library in a SharePoint-hosted add-in. However, in a SharePoint-hosted add-in the add-in page is already in the add-in web, in which case it wouldn't need the cross-domain library to read the list items. For a SharePoint-hosted add-in sample that reads data in the host web, see  [Use the cross-domain library in a SharePoint-hosted add-in (REST)](http://code.msdn.microsoft.com/SharePoint-2013-Use-the-00c37814) or see [Access data from the host web](access-sharepoint-data-from-add-ins-using-the-cross-domain-library.md#SP15Accessdatafromremoteapp_Hostweb) later in this article.</span></span>

### <a name="create-list-items-on-the-add-in-web"></a><span data-ttu-id="09261-158">Создание элементов списка на сайте надстройки</span><span class="sxs-lookup"><span data-stu-id="09261-158">Create list items on the add-in web</span></span>


1. <span data-ttu-id="09261-p111">Щелкните правой кнопкой мыши проект надстройки SharePoint в **обозревателе решений**. Выберите **Добавить****>****Новый элемент…**</span><span class="sxs-lookup"><span data-stu-id="09261-p111">Right-click the SharePoint Add-in project in  **Solution Explorer**. Choose  **Add** **>** **New Item…**</span></span>
    
 
2. <span data-ttu-id="09261-p112">Выберите **Элементы Visual C#** **>** **Office/SharePoint** **>** **Список**. Введите для списка имя **Объявления**.</span><span class="sxs-lookup"><span data-stu-id="09261-p112">Choose  **Visual C# Items** **>** **Office/SharePoint** **>** **List**. Set the name of your list to  **Announcements**.</span></span>
    
 
3. <span data-ttu-id="09261-p113">Дважды щелкните **Объявления** **>** **Elements.xml**. Вставьте следующие узлы XML как потомки элемента **ListInstance**.</span><span class="sxs-lookup"><span data-stu-id="09261-p113">Double click  **Announcements** **>** **Elements.xml**. Paste the following XML nodes as children of the  **ListInstance** element.</span></span>
    
```
  <Data>
    <Rows>
        <Row>
            <Field Name="Title">Lorem ipsum 1</Field>
            <Field Name="Body">Sed ut perspiciatis, unde omnis iste...</Field>
        </Row>
        <Row>
            <Field Name="Title">Lorem ipsum 2</Field>
            <Field Name="Body">Sed ut perspiciatis, unde omnis iste...</Field>
        </Row>
    </Rows>
</Data>
```


### <a name="to-add-a-new-page-that-uses-the-cross-domain-library"></a><span data-ttu-id="09261-165">Добавление новой страницы, которая использует междоменную библиотеку</span><span class="sxs-lookup"><span data-stu-id="09261-165">To add a new page that uses the cross-domain library</span></span>


1. <span data-ttu-id="09261-166">Дважды щелкните файл **Default.aspx** в веб-проекте в **обозревателе решений**.</span><span class="sxs-lookup"><span data-stu-id="09261-166">Double-click  **Default.aspx** in the web project in **Solution Explorer**.</span></span>
    
 
2. <span data-ttu-id="09261-p114">Скопируйте следующий код и вставьте его в файл Default.aspx. Этот код выполняет следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="09261-p114">Copy the following code and paste it in the Default.aspx file. The code performs the following tasks:</span></span>
    
      - <span data-ttu-id="09261-169">Загружает библиотеку jQuery из сети CDN Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="09261-169">Loads the jQuery library from the Microsoft CDN.</span></span>
    
 
  - <span data-ttu-id="09261-170">Задает заполнитель для результатов.</span><span class="sxs-lookup"><span data-stu-id="09261-170">Provides a placeholder for the result.</span></span>
    
 
  - <span data-ttu-id="09261-171">Извлекает URL-адрес сайта надстройки из строки запроса.</span><span class="sxs-lookup"><span data-stu-id="09261-171">Extracts the add-in web URL from the query string.</span></span>
    
 
  - <span data-ttu-id="09261-172">Загружает междоменную библиотеку JavaScript с помощью функции **getScript** в jQuery.</span><span class="sxs-lookup"><span data-stu-id="09261-172">Loads the cross-domain library JavaScript using the  **getScript** function in jQuery.</span></span>
    
    <span data-ttu-id="09261-173">Функция загружает необходимые ресурсы и переходит к указанной функции, обеспечивая загрузку междоменной библиотеке и предоставляя к ней доступ последующему коду.</span><span class="sxs-lookup"><span data-stu-id="09261-173">The function loads the required resources and then continues to the specified function, ensuring that the cross-domain library is loaded and available to use by the subsequent code.</span></span>
    
 
  - <span data-ttu-id="09261-p115">Создает экземпляр объекта **RequestExecutor**. По умолчанию RequestExecutor использует сайт надстройки как сайт контекста.</span><span class="sxs-lookup"><span data-stu-id="09261-p115">Instantiates the  **RequestExecutor** object. By default, RequestExecutor uses the add-in web as the context site.</span></span>
    
     <span data-ttu-id="09261-p116">**Примечание.** Вы можете изменить сайт контекста на сайты, отличные от сайта надстройки, с помощью конечной точки **AppContextSite** (REST) или объекта (JSOM). Дополнительные сведения об AppContextSite см. в разделе [Доступ к данным на хост-сайте](access-sharepoint-data-from-add-ins-using-the-cross-domain-library.md#SP15Accessdatafromremoteapp_Hostweb) далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="09261-p116">**Note**  You can change the context site to other sites different than the add-in web by using the  **AppContextSite** endpoint (REST) or object (JSOM). To learn more about AppContextSite, see [Access data from the host web](access-sharepoint-data-from-add-ins-using-the-cross-domain-library.md#SP15Accessdatafromremoteapp_Hostweb) later in this article.</span></span>
  - <span data-ttu-id="09261-178">Выполняет REST-вызов к конечной точке элементов списка.</span><span class="sxs-lookup"><span data-stu-id="09261-178">Issues a REST call to the list items endpoint.</span></span>
    
 
  - <span data-ttu-id="09261-179">Обрабатывает успешное выполнение с отображением элементов списка на веб-странице.</span><span class="sxs-lookup"><span data-stu-id="09261-179">Handles successful completion, displaying the list items on the webpage.</span></span>
    
 
  - <span data-ttu-id="09261-180">Обрабатывает ошибки с отображением сообщения об ошибке на веб-странице.</span><span class="sxs-lookup"><span data-stu-id="09261-180">Handles errors, displaying the error message on the webpage.</span></span>
    
 

```
  
<html>
    <head>
        <title>Cross-domain sample</title>
    </head>
    <body>
        <!-- This is the placeholder for the announcements -->
        <div id="renderAnnouncements"></div>
        <script 
            type="text/javascript" 
            src="//ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.2.min.js">
        </script>
        <script type="text/javascript">
          var hostweburl;
          var appweburl;

          // Load the required SharePoint libraries
          $(document).ready(function () {
            //Get the URI decoded URLs.
            hostweburl =
                decodeURIComponent(
                    getQueryStringParameter("SPHostUrl")
            );
            appweburl =
                decodeURIComponent(
                    getQueryStringParameter("SPAppWebUrl")
            );

            // resources are in URLs in the form:
            // web_url/_layouts/15/resource
            var scriptbase = hostweburl + "/_layouts/15/";

            // Load the js files and continue to the successHandler
            $.getScript(scriptbase + "SP.RequestExecutor.js", execCrossDomainRequest);
          });

          // Function to prepare and issue the request to get
          //  SharePoint data
          function execCrossDomainRequest() {
            // executor: The RequestExecutor object
            // Initialize the RequestExecutor with the add-in web URL.
            var executor = new SP.RequestExecutor(appweburl);

            // Issue the call against the add-in web.
            // To get the title using REST we can hit the endpoint:
            //      appweburl/_api/web/lists/getbytitle('listname')/items
            // The response formats the data in the JSON format.
            // The functions successHandler and errorHandler attend the
            //      sucess and error events respectively.
            executor.executeAsync(
                {
                  url:
                      appweburl +
                      "/_api/web/lists/getbytitle('Announcements')/items",
                  method: "GET",
                  headers: { "Accept": "application/json; odata=verbose" },
                  success: successHandler,
                  error: errorHandler
                }
            );
          }

          // Function to handle the success event.
          // Prints the data to the page.
          function successHandler(data) {
            var jsonObject = JSON.parse(data.body);
            var announcementsHTML = "";

            var results = jsonObject.d.results;
            for (var i = 0; i < results.length; i++) {
              announcementsHTML = announcementsHTML +
                  "<p><h1>" + results[i].Title +
                  "</h1>" + results[i].Body +
                  "</p><hr>";
            }

            document.getElementById("renderAnnouncements").innerHTML =
                announcementsHTML;
          }

          // Function to handle the error event.
          // Prints the error message to the page.
          function errorHandler(data, errorCode, errorMessage) {
            document.getElementById("renderAnnouncements").innerText =
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
    </body>
</html>
```


### <a name="to-build-and-run-the-solution"></a><span data-ttu-id="09261-181">Создание и запуск решения</span><span class="sxs-lookup"><span data-stu-id="09261-181">To build and run the solution</span></span>


1. <span data-ttu-id="09261-182">Нажмите клавишу F5.</span><span class="sxs-lookup"><span data-stu-id="09261-182">Press the F5 key.</span></span>
    
     <span data-ttu-id="09261-183">**Примечание.** При нажатии клавиши F5 Visual Studio выполняет сборку решения, развертывает надстройку и открывает для нее страницу разрешений.</span><span class="sxs-lookup"><span data-stu-id="09261-183">**Note**  When you press F5, Visual Studio builds the solution, deploys the add-in, and opens the permissions page for the add-in.</span></span>
2. <span data-ttu-id="09261-184">Нажмите кнопку **Доверять**.</span><span class="sxs-lookup"><span data-stu-id="09261-184">Choose the  **Trust It** button.</span></span>
    
 
3. <span data-ttu-id="09261-185">Выберите значок надстройки на странице **Содержимое сайта**.</span><span class="sxs-lookup"><span data-stu-id="09261-185">Choose the add-in icon on the  **Site Contents** page.</span></span>
    
 
<span data-ttu-id="09261-p117">Если вы предпочитаете работать с загруженными примерами кода, этот пример можно скачать в коллекции исходных кодов. **Пример кода: получение элементов списка с помощью междоменной библиотеки** с использованием [SharePoint-Add-in-REST-OData-CrossDomain](https://github.com/OfficeDev/SharePoint-Add-in-REST-OData-CrossDomain) или [SharePoint-Add-in-JSOM-CrossDomain](https://github.com/OfficeDev/SharePoint-Add-in-JSOM-CrossDomain).</span><span class="sxs-lookup"><span data-stu-id="09261-p117">If you prefer downloadable code samples, you can get this one from code gallery.  **Code sample: Get list items by using the cross-domain library** using [SharePoint-Add-in-REST-OData-CrossDomain](https://github.com/OfficeDev/SharePoint-Add-in-REST-OData-CrossDomain) or [SharePoint-Add-in-JSOM-CrossDomain](https://github.com/OfficeDev/SharePoint-Add-in-JSOM-CrossDomain).</span></span>
 

 

<span data-ttu-id="09261-188">**Табл. 2. Поиск и устранение неполадок в решении**</span><span class="sxs-lookup"><span data-stu-id="09261-188">**Table 2. Troubleshooting the solution**</span></span>


|<span data-ttu-id="09261-189">**Если вы видите...**</span><span class="sxs-lookup"><span data-stu-id="09261-189">**If you see…**</span></span>|<span data-ttu-id="09261-190">**Попробуйте...**</span><span class="sxs-lookup"><span data-stu-id="09261-190">**Then try…**</span></span>|
|:-----|:-----|
|<span data-ttu-id="09261-191">Сообщение об ошибке: "К сожалению, у нас возникли проблемы с доступом к сайту". К тому же, появляется кнопка, предназначенная для исправления ошибки, но она не устраняет проблему.</span><span class="sxs-lookup"><span data-stu-id="09261-191">Error message: Sorry, we had some trouble accessing your site.There is also a button to fix the error, but it doesn't correct the problem.</span></span>|<span data-ttu-id="09261-192">Возможно, вы столкнулись с проблемой с зонами безопасности в Internet Explorer, см. статью [Работа с междоменной библиотекой в различных зонах безопасности Internet Explorer в надстройках SharePoint](work-with-the-cross-domain-library-across-different-internet-explorer-security-z.md).</span><span class="sxs-lookup"><span data-stu-id="09261-192">You may have hit a known problem with security zones in Internet Explorer, see  [Work with the cross-domain library across different Internet Explorer security zones in SharePoint Add-ins](work-with-the-cross-domain-library-across-different-internet-explorer-security-z.md).</span></span>|
|<span data-ttu-id="09261-p118">Сообщение об ошибке: требуемые функции не поддерживаются вашим браузером. Используйте IE 8 или более позднюю версию либо другой современный браузер. Метатег "X-UA-Compatible" должен быть равен "IE=8" или более высокому значению.</span><span class="sxs-lookup"><span data-stu-id="09261-p118">Error message: The required functionalities are not supported by your browser. Please make sure you are using IE 8 or above, or other modern browser. Please make sure the 'X-UA-Compatible' meta tag is set to be 'IE=8' or above.</span></span>|<span data-ttu-id="09261-p119">Для междоменной библиотеки требуется режим документа в **IE8** или более поздней версии. В ряде случаев он по умолчанию задан как **IE7**. Можно использовать средства разработчика Internet Explorer, чтобы определить или изменить режим документа для страницы. Дополнительные сведения см. в разделе [Определение совместимости документов](http://msdn.microsoft.com/library/cc288325.aspx).</span><span class="sxs-lookup"><span data-stu-id="09261-p119">The cross-domain library requires a document mode of  **IE8** or above. In some scenarios, the document mode is set to **IE7** by default. You can use the Internet Explorer developer tools to determine and change the document mode of your page. For more information, see [Defining Document Compatibility](http://msdn.microsoft.com/library/cc288325.aspx).</span></span>|
|<span data-ttu-id="09261-200">Сообщение об ошибке: "Тип не определен". Кроме того, надстройка использует объектную модель JavaScript (JSOM).</span><span class="sxs-lookup"><span data-stu-id="09261-200">Error message: 'Type' is undefined.Additionally, your add-in uses the JavaScript Object Model (JSOM).</span></span>|<span data-ttu-id="09261-p120">JSOM использует метод **Type.registerNamespace** в библиотеке Microsoft Ajax для регистрации пространства имен **SP**. Используйте следующий код, чтобы добавить ссылку на библиотеку Microsoft Ajax на вашей странице: ```HTML<script  type="text/javascript"  src="//ajax.aspnetcdn.com/ajax/4.0/1/MicrosoftAjax.js"></script>```.</span><span class="sxs-lookup"><span data-stu-id="09261-p120">The JSOM uses the  **Type.registerNamespace** method in the Microsoft Ajax library to register the **SP** namespace. Use the following code to add a reference to the Microsoft Ajax library from your page:```HTML<script  type="text/javascript"  src="//ajax.aspnetcdn.com/ajax/4.0/1/MicrosoftAjax.js"></script>```</span></span>|

## <a name="next-steps"></a><span data-ttu-id="09261-203">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="09261-203">Next steps</span></span>
<span data-ttu-id="09261-204"><a name="SP15Accessdatafromremoteapp_Next"> </a></span><span class="sxs-lookup"><span data-stu-id="09261-204"></span></span>

<span data-ttu-id="09261-p121">В этой статье показано, как отправить запрос конечной точке REST для чтения данных с сайта надстройки с помощью страницы надстройки, не размещенной в SharePoint. Вы также можете изучить следующие сценарии и сведения о междоменной библиотеке.</span><span class="sxs-lookup"><span data-stu-id="09261-p121">This article shows how to query a REST endpoint to read data from the add-in web by using an add-in page that is not hosted on SharePoint. You can also explore the following scenarios and details about the cross-domain library.</span></span>
 

 

### <a name="use-the-jsom-to-read-data-from-the-add-in-web"></a><span data-ttu-id="09261-207">Использование JSOM для чтения данных с сайта надстройки</span><span class="sxs-lookup"><span data-stu-id="09261-207">Use the JSOM to read data from the add-in web</span></span>
<span data-ttu-id="09261-208"><a name="SP15Accessdatafromremoteapp_JSOM"> </a></span><span class="sxs-lookup"><span data-stu-id="09261-208"></span></span>

<span data-ttu-id="09261-p122">В зависимости от ваших предпочтений вы можете использовать JSOM вместо REST для запроса данных с сайта надстройки. Чтобы использовать междоменную библиотеку с JSOM, необходимо выполнить дополнительные задачи:</span><span class="sxs-lookup"><span data-stu-id="09261-p122">Depending on your preference, you might want to use the JSOM instead of REST to query data from the add-in web. You must complete additional tasks to use the cross-domain library with JSOM:</span></span>
 

 

- <span data-ttu-id="09261-211">Добавить ссылку на SharePoint JSOM на страницу надстройки.</span><span class="sxs-lookup"><span data-stu-id="09261-211">Reference the SharePoint JSOM in your add-in page.</span></span>
    
 
- <span data-ttu-id="09261-212">Инициализировать объект **ProxyWebRequestExecutorFactory** и сделать его фабрикой объекта контекста.</span><span class="sxs-lookup"><span data-stu-id="09261-212">Initialize the  **ProxyWebRequestExecutorFactory** object and set it as the factory of the context object.</span></span>
    
 
- <span data-ttu-id="09261-213">Получить доступ к объектам SharePoint для чтения данных из списка.</span><span class="sxs-lookup"><span data-stu-id="09261-213">Access the SharePoint objects to read the data from the list.</span></span>
    
 
- <span data-ttu-id="09261-214">Загрузить объекты в контекст и выполнить запрос.</span><span class="sxs-lookup"><span data-stu-id="09261-214">Load the objects in the context and execute the query.</span></span>
    
 
<span data-ttu-id="09261-p123">Пример кода, в котором показано, как выполнить эти задачи, см. в репозитории  [SharePoint-Add-in-JSOM-CrossDomain](https://github.com/OfficeDev/SharePoint-Add-in-JSOM-CrossDomain). Дополнительные сведения об использовании JSOM см. в статье  [Использование объектной модели JavaScript (JSOM) в надстройках для SharePoint](http://blogs.msdn.com/b/officeapps/archive/2012/09/04/using-the-javascript-object-model-jsom-in-apps-for-sharepoint.aspx).</span><span class="sxs-lookup"><span data-stu-id="09261-p123">For a code sample that shows how to perform the tasks, see  [SharePoint-Add-in-JSOM-CrossDomain](https://github.com/OfficeDev/SharePoint-Add-in-JSOM-CrossDomain). For more information on how to use the JSOM, see  [Using the JavaScript object model (JSOM) in SharePoint Add-ins](http://blogs.msdn.com/b/officeapps/archive/2012/09/04/using-the-javascript-object-model-jsom-in-apps-for-sharepoint.aspx).</span></span>
 

 

### <a name="access-data-from-the-host-web"></a><span data-ttu-id="09261-217">Доступ к данным на хост-сайте</span><span class="sxs-lookup"><span data-stu-id="09261-217">Access data from the host web</span></span>
<span data-ttu-id="09261-218"><a name="SP15Accessdatafromremoteapp_Hostweb"> </a></span><span class="sxs-lookup"><span data-stu-id="09261-218"></span></span>

<span data-ttu-id="09261-p124">В примере на этой странице показано, как читать данные с сайта надстройки. Это хорошая начальная точка, так как междоменная библиотека изначально использует надстройку как сайт контекста. Однако существует множество сценариев, в которых необходимо получить доступ к данным на хост-сайте. Для этого требуется выполнить несколько задач:</span><span class="sxs-lookup"><span data-stu-id="09261-p124">The example in this page shows how to read data from the add-in web. This works fine as the starting example because the cross-domain library initially uses the add-in as the context site. However, there are many scenarios where you want to access data on the host web. There are a few tasks required to access data on the host web:</span></span> 
 

 

- <span data-ttu-id="09261-223">Сделать хост-сайт сайтом контекста для междоменной библиотеки.</span><span class="sxs-lookup"><span data-stu-id="09261-223">Set the host web as the context site for the cross-domain library.</span></span>
    
 
- <span data-ttu-id="09261-224">Задать необходимые разрешения для надстройки.</span><span class="sxs-lookup"><span data-stu-id="09261-224">Provide appropriate permissions to the add-in.</span></span>
    
 
<span data-ttu-id="09261-p125">Вы можете изменить сайт контекста с помощью конечной точки **AppContextSite** (REST) или объекта (JSOM). В следующем примере показано, как изменить сайт контекста с помощью конечной точки REST:</span><span class="sxs-lookup"><span data-stu-id="09261-p125">You can change the context site by using the  **AppContextSite** endpoint (REST) or object (JSOM). The following example shows how to change the context site using the REST endpoint:</span></span>
 

 



```
executor.executeAsync(
    {
        url:
            appweburl +
            "/_api/SP.AppContextSite(@target)/web/title?@target='" +
            hostweburl + "'",
        method: "GET",
        headers: { "Accept": "application/json; odata=verbose" },
        success: successHandler,
        error: errorHandler
    }
);
```

<span data-ttu-id="09261-227">В следующем примере кода показано, как изменить сайт контекста с помощью JSOM:</span><span class="sxs-lookup"><span data-stu-id="09261-227">The following code example shows how to change the context site using JSOM:</span></span>
 

 



```
context = new SP.ClientContext(appweburl);
factory = new SP.ProxyWebRequestExecutorFactory(appweburl);
context.set_webRequestExecutorFactory(factory);
appContextSite = new SP.AppContextSite(context, hostweburl);

this.web = appContextSite.get_web();
context.load(this.web);
```

<span data-ttu-id="09261-p126">По умолчанию у вашей надстройки есть разрешения для сайта надстройки, но не для хост-сайта. В следующем примере показан раздел манифеста, в котором объявляется запрос разрешений для чтения данных с хост-сайта:</span><span class="sxs-lookup"><span data-stu-id="09261-p126">By default, your add-in has permissions to the add-in web, but not to the host web. The following example shows a manifest section that declares a permission request to read data from the host web:</span></span>
 

 



```XML
<AppPermissionRequests>
    <AppPermissionRequest 
        Scope="http://sharepoint/content/sitecollection/web" 
        Right="Read" />
</AppPermissionRequests>
```

<span data-ttu-id="09261-230">Создайте ресурс на сайте надстройки (например, пустую страницу или список), чтобы принудительно создать сайт надстройки, так как это необходимо для использования междоменной библиотеки.</span><span class="sxs-lookup"><span data-stu-id="09261-230">Make sure that you create a resource on the add-in web (like an empty page or list) to force the provisioning of the add-in web, which is required to use the cross-domain library.</span></span>
 

 

### <a name="access-data-across-site-collections"></a><span data-ttu-id="09261-231">Доступ к данным на нескольких семействах веб-сайтов</span><span class="sxs-lookup"><span data-stu-id="09261-231">Access data across site collections</span></span>
<span data-ttu-id="09261-232"><a name="SP15Accessdatafromremoteapp_TenantScope"> </a></span><span class="sxs-lookup"><span data-stu-id="09261-232"></span></span>

<span data-ttu-id="09261-p127">С помощью междоменной библиотеки можно получать доступ к данным на нескольких семействах веб-сайтов в одном клиенте. Для этого необходимо выполнить несколько задач:</span><span class="sxs-lookup"><span data-stu-id="09261-p127">With the cross-domain library, you can access data across site collections in the same tenant. There are some tasks that you need to complete to access data across site collections:</span></span>
 

 

- <span data-ttu-id="09261-235">Добавить запрос разрешений для доступа к данным в клиенте.</span><span class="sxs-lookup"><span data-stu-id="09261-235">Add a permission request to access data in the tenant.</span></span>
    
 
- <span data-ttu-id="09261-236">Заменить сайт контекста на семейства сайтов, к которым нужно выполнить запрос, в коде.</span><span class="sxs-lookup"><span data-stu-id="09261-236">In your code, switch the context site to the site collections that you want to query.</span></span>
    
 
- <span data-ttu-id="09261-237">Добавить надстройку в каталог надстроек.</span><span class="sxs-lookup"><span data-stu-id="09261-237">Add the add-in to the add-in catalog.</span></span>
    
 
- <span data-ttu-id="09261-p128">Развернуть надстройку с разрешениями на уровне клиента на веб-сайте. Пример см. в описании примера кода  [Использование междоменной библиотеки в надстройке с разрешениями на уровне клиента (REST)](http://code.msdn.microsoft.com/SharePoint-2013-Use-the-6b3e4c1e).</span><span class="sxs-lookup"><span data-stu-id="09261-p128">Deploy the add-in as a tenant-scoped add-in to a website. For an example on how to deploy as a tenant-scoped add-in, see the description of the  [Use the cross-domain library in a tenant-scoped add-in (REST)](http://code.msdn.microsoft.com/SharePoint-2013-Use-the-6b3e4c1e) code sample.</span></span>
    
 
<span data-ttu-id="09261-p129">Надстройке также требуются разрешения для доступа к данным клиента. В следующем примере показан раздел манифеста, в котором объявляется запрос разрешений для чтения данных клиента:</span><span class="sxs-lookup"><span data-stu-id="09261-p129">Your add-in also needs permission to access data from the tenant. The following example shows a manifest section that declares a permission request to read data from the tenant:</span></span>
 

 



```XML
<AppPermissionRequests>
  <AppPermissionRequest 
    Scope="http://sharepoint/content/tenant" 
    Right="Read" />
</AppPermissionRequests>
```

<span data-ttu-id="09261-p130">Чтобы заменить сайт контекста в коде, используйте конечную точку **AppContextSite** (REST) или объект (JSOM), как в разделе [Доступ к данным на хост-сайте](access-sharepoint-data-from-add-ins-using-the-cross-domain-library.md#SP15Accessdatafromremoteapp_Hostweb). Вот напоминание о конечной точке REST: /_api/SP.AppContextSite(@target)/web/title?@target='weburl', а также пример того, как создать экземпляр объекта в JSOM: `appContextSite = new SP.AppContextSite(context, weburl);`.</span><span class="sxs-lookup"><span data-stu-id="09261-p130">To switch the context site in your code, use the  **AppContextSite** endpoint (REST) or object (JSOM), just like in the [Access data from the host web](access-sharepoint-data-from-add-ins-using-the-cross-domain-library.md#SP15Accessdatafromremoteapp_Hostweb) section. Here is a reminder of the REST endpoint: /_api/SP.AppContextSite(@target)/web/title?@target='weburl', and an example on how to instantiate the object in JSOM: `appContextSite = new SP.AppContextSite(context, weburl);`.</span></span>
 

 
<span data-ttu-id="09261-p131">Вы как разработчик можете развернуть только надстройки с разрешениями на уровне клиента из каталога надстроек. Можно настроить каталог надстроек для локальной среды или среды SharePoint Online. Отправить надстройку в каталог надстроек так же просто, как загрузить файл в библиотеку документов. Подробные инструкции см. в статье о  [добавлении настраиваемых надстроек на сайт каталога надстроек](http://office.microsoft.com/en-us/sharepoint-help/use-the-app-catalog-to-make-custom-business-apps-available-for-your-sharepoint-online-environment-HA102772362.aspx).</span><span class="sxs-lookup"><span data-stu-id="09261-p131">As a developer, you can only deploy tenant-scoped add-ins from the add-in catalog. You can provision an add-in catalog to your on-premises or SharePoint Online environments. Uploading your add-in to the add-in catalog is as simple as uploading a file to a document library. See  [Add custom add-ins to the Add-in Catalog site](http://office.microsoft.com/en-us/sharepoint-help/use-the-app-catalog-to-make-custom-business-apps-available-for-your-sharepoint-online-environment-HA102772362.aspx) for detailed instructions.</span></span>
 

 
<span data-ttu-id="09261-p132">Из каталога надстроек вы сможете развернуть надстройку на одном или нескольких веб-сайтах в клиенте. Так как у надстройки есть разрешения для доступа к данным клиента, нужно развернуть её только на одном веб-сайте для доступа к всем данным клиента. Инструкции по развертыванию надстройки из каталога надстроек см. в статье  [Развертывание настраиваемой надстройки](http://office.microsoft.com/en-us/sharepoint-help/use-the-app-catalog-to-make-custom-business-apps-available-for-your-sharepoint-online-environment-HA102772362.aspx).</span><span class="sxs-lookup"><span data-stu-id="09261-p132">From the add-in catalog you can deploy the add-in to one or more websites in the tenant. Since your add-in has permissions to access data in the tenant, you only have to deploy to one website to access data on the whole tenant. See  [Deploy a custom add-in](http://office.microsoft.com/en-us/sharepoint-help/use-the-app-catalog-to-make-custom-business-apps-available-for-your-sharepoint-online-environment-HA102772362.aspx) for instructions on how to deploy an add-in from the add-in catalog.</span></span>
 

 
<span data-ttu-id="09261-251">Сведения о том, как скачать пример кода, в котором показано, как получить доступ к данным на разных семействах веб-сайтов, см. в статье  [Использование междоменной библиотеки в надстройке с разрешениями на уровне клиента (REST)](http://code.msdn.microsoft.com/SharePoint-2013-Use-the-6b3e4c1e).</span><span class="sxs-lookup"><span data-stu-id="09261-251">To download a code sample that shows how to access data across site collections, see  [Use the cross-domain library in a tenant-scoped add-in (REST)](http://code.msdn.microsoft.com/SharePoint-2013-Use-the-6b3e4c1e).</span></span>
 

 

### <a name="issuing-calls-across-different-security-zones"></a><span data-ttu-id="09261-252">Выполнение запросов для разных зон безопасности</span><span class="sxs-lookup"><span data-stu-id="09261-252">Issuing calls across different security zones</span></span>
<span data-ttu-id="09261-253"><a name="SP15Accessdatafromremoteapp_IEZones"> </a></span><span class="sxs-lookup"><span data-stu-id="09261-253"></span></span>

<span data-ttu-id="09261-p133">Для взаимодействия междоменная библиотека использует страницу прокси-сервера, размещенную в **IFrame** на странице надстройки. Если страница надстройки и веб-сайт SharePoint находятся в разных зонах безопасности, отправка файлов cookie авторизации невозможна. Если эти файлы отсутствуют и элемент IFrame пытается загрузить прокси-страницу, он перенаправляется на страницу входа SharePoint. В целях безопасности страница входа SharePoint не может содержаться в элементе IFrame. В такой ситуации библиотека не может загрузить прокси-страницу, и связь с SharePoint невозможна.</span><span class="sxs-lookup"><span data-stu-id="09261-p133">The cross-domain library uses a proxy page that is hosted in an  **IFrame** on the add-in page to enable communication. When the add-in page and SharePoint website are in different security zones, authorization cookies can't be sent. If there are no authorization cookies, and the IFrame tries to load the proxy page, it will be redirected to the SharePoint sign-in page. The SharePoint sign-in page can't be contained in an IFrame for security reasons. In these scenarios, the library cannot load the proxy page, and communication with SharePoint is not possible.</span></span>
 

 
<span data-ttu-id="09261-p134">Однако для этих сценариев существует решение. Это **шаблон apphost**, который создает оболочку для страниц надстройки на странице, размещенной на сайте надстройки. Рекомендуем использовать шаблон apphost в надстройках, которые используют междоменную библиотеку, даже если очевидных границ безопасности нет. Дополнительные сведения см. в статье [Работа с междоменной библиотекой в различных зонах безопасности Internet Explorer в надстройках SharePoint](work-with-the-cross-domain-library-across-different-internet-explorer-security-z.md).</span><span class="sxs-lookup"><span data-stu-id="09261-p134">However, there is a solution for these scenarios. The solution is the  **apphost pattern**, which consists in wrapping the add-in pages in a page hosted in the add-in web. It's a good idea to use the apphost pattern in add-ins that use the cross-domain library, even if there are no evident security boundaries. For more information, see [Work with the cross-domain library across different Internet Explorer security zones in SharePoint Add-ins](work-with-the-cross-domain-library-across-different-internet-explorer-security-z.md).</span></span>
 

 

### <a name="access-data-from-an-additional-remote-host-in-a-sharepoint-hosted-add-in"></a><span data-ttu-id="09261-263">Доступ к данным на дополнительном удаленном узле в надстройках, размещаемых в SharePoint</span><span class="sxs-lookup"><span data-stu-id="09261-263">Access data from an additional remote host in a SharePoint-hosted add-in</span></span>
<span data-ttu-id="09261-264"><a name="SP15Accessdatafromremoteapp_SPhosted"> </a></span><span class="sxs-lookup"><span data-stu-id="09261-264"></span></span>

<span data-ttu-id="09261-p135">По умолчанию надстройке, размещаемой в SharePoint, разрешено выполнять междоменные вызовы для хост-сайта, если у нее есть необходимые разрешения. Однако такая надстройка также может указать удаленный узел в атрибуте **AllowedRemoteHostUrl**, принадлежащему **AppPrincipal**. Это позволяет эффективно выполнять междоменные вызовы из сайта надстройки и других узлов.</span><span class="sxs-lookup"><span data-stu-id="09261-p135">By default, a SharePoint-hosted add-in is allowed to issue cross-domain calls to the host web, provided that it has proper permissions. However, a SharePoint-hosted add-in can also specify a remote host in the  **AllowedRemoteHostUrl** attribute of its **AppPrincipal**. This effectively lets you issue cross-domain calls from the add-in web and from another host elsewhere.</span></span>
 

 
<span data-ttu-id="09261-268">Сведения о том, как скачать пример Надстройки, размещаемые в SharePoint, использующего междоменную библиотеку, см. в статье  [Пример кода: использование междоменной библиотеки в надстройке, размещенной в SharePoint (REST)](http://code.msdn.microsoft.com/SharePoint-2013-Use-the-00c37814).</span><span class="sxs-lookup"><span data-stu-id="09261-268">To download a sample of a SharePoint-hosted add-in that uses the cross-domain library, see  [Code sample: Use the cross-domain library in a SharePoint-hosted add-in (REST)](http://code.msdn.microsoft.com/SharePoint-2013-Use-the-00c37814).</span></span>
 

 

## <a name="additional-resources"></a><span data-ttu-id="09261-269">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="09261-269">Additional resources</span></span>
<span data-ttu-id="09261-270"><a name="SP15Accessdatafromremoteapp_Addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="09261-270"></span></span>


-  [<span data-ttu-id="09261-271">SharePoint-Add-in-REST-OData-CrossDomain</span><span class="sxs-lookup"><span data-stu-id="09261-271">SharePoint-Add-in-REST-OData-CrossDomain</span></span>](https://github.com/OfficeDev/SharePoint-Add-in-REST-OData-CrossDomain)
    
 
-  [<span data-ttu-id="09261-272">SharePoint-Add-in-JSOM-CrossDomain</span><span class="sxs-lookup"><span data-stu-id="09261-272">SharePoint-Add-in-JSOM-CrossDomain</span></span>](https://github.com/OfficeDev/SharePoint-Add-in-JSOM-CrossDomain)
    
 
-  [<span data-ttu-id="09261-273">Пример кода: запрос названия хост-сайта с помощью междоменной библиотеки (REST)</span><span class="sxs-lookup"><span data-stu-id="09261-273">Code sample: Get the host web title using the cross-domain library (REST)</span></span>](http://code.msdn.microsoft.com/SharePoint-2013-Get-the-0ec36bb6)
    
 
-  [<span data-ttu-id="09261-274">Пример кода: запрос названия хост-сайта с помощью междоменной библиотеки (JSOM)</span><span class="sxs-lookup"><span data-stu-id="09261-274">Code sample: Get the host web title using the cross-domain library (JSOM)</span></span>](http://code.msdn.microsoft.com/office/SharePoint-2013-Get-the-563f2a3d)
    
 
-  [<span data-ttu-id="09261-275">Пример кода: использование междоменной библиотеки в надстройке, размещаемой в SharePoint</span><span class="sxs-lookup"><span data-stu-id="09261-275">Code sample: Use the cross-domain library in a SharePoint-hosted add-in (REST)</span></span>](http://code.msdn.microsoft.com/SharePoint-2013-Use-the-00c37814)
    
 
-  [<span data-ttu-id="09261-276">Пример кода: использование междоменной библиотеки в надстройке с разрешениями на уровне клиента (REST)</span><span class="sxs-lookup"><span data-stu-id="09261-276">Code sample: Use the cross-domain library in a tenant-scoped add-in (REST)</span></span>](http://code.msdn.microsoft.com/SharePoint-2013-Use-the-6b3e4c1e)
    
 
-  [<span data-ttu-id="09261-277">Пример кода: использование элемента управления хрома и междоменной библиотеки (REST)</span><span class="sxs-lookup"><span data-stu-id="09261-277">Code sample: Use the chrome control and the cross-domain library (REST)</span></span>](http://code.msdn.microsoft.com/SharePoint-2013-Use-the-a759e9f8)
    
 
-  [<span data-ttu-id="09261-278">Пример кода: использование элемента управления хрома и междоменной библиотеки (JSOM)</span><span class="sxs-lookup"><span data-stu-id="09261-278">Code sample: Use the chrome control and the cross-domain library (JSOM)</span></span>](http://code.msdn.microsoft.com/SharePoint-2013-Use-the-97c30a2e)
    
 
-  [<span data-ttu-id="09261-279">Пример кода: использование дополнительных действий и междоменной библиотеки для заказа книг</span><span class="sxs-lookup"><span data-stu-id="09261-279">Code sample: Use custom actions and the cross-domain library to order books</span></span>](http://code.msdn.microsoft.com/SharePoint-2013-Open-a-36d1598d)
    
 
-  [<span data-ttu-id="09261-280">Безопасный доступ к данным и клиентские объектные модели для надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="09261-280">Secure data access and client object models for SharePoint Add-ins</span></span>](secure-data-access-and-client-object-models-for-sharepoint-add-ins.md)
    
 
-  [<span data-ttu-id="09261-281">Работа с междоменной библиотекой в различных зонах безопасности Internet Explorer в надстройках SharePoint</span><span class="sxs-lookup"><span data-stu-id="09261-281">Work with the cross-domain library across different Internet Explorer security zones in SharePoint Add-ins</span></span>](work-with-the-cross-domain-library-across-different-internet-explorer-security-z.md)
    
 
-  [<span data-ttu-id="09261-282">Создание настраиваемой страницы прокси для междоменной библиотеки в SharePoint</span><span class="sxs-lookup"><span data-stu-id="09261-282">Create a custom proxy page for the cross-domain library in SharePoint</span></span>](create-a-custom-proxy-page-for-the-cross-domain-library-in-sharepoint.md)
    
 
-  [<span data-ttu-id="09261-283">Отправка запросов удаленной службе с помощью веб-прокси в SharePoint</span><span class="sxs-lookup"><span data-stu-id="09261-283">Query a remote service using the web proxy in SharePoint</span></span>](query-a-remote-service-using-the-web-proxy-in-sharepoint.md)
    
 
-  [<span data-ttu-id="09261-284">Настройка локальной среды разработки надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="09261-284">Set up an on-premises development environment for SharePoint Add-ins</span></span>](set-up-an-on-premises-development-environment-for-sharepoint-add-ins.md)
    
 
