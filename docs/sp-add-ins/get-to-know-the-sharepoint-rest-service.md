# <a name="get-to-know-the-sharepoint-rest-service"></a><span data-ttu-id="0793f-101">Знакомство со службой REST в SharePoint</span><span class="sxs-lookup"><span data-stu-id="0793f-101">Get to know the SharePoint REST service</span></span>
<span data-ttu-id="0793f-102">Основы использования службы REST в SharePoint для чтения и изменения данных в SharePoint по веб-протоколам REST и OData.</span><span class="sxs-lookup"><span data-stu-id="0793f-102">Get the basics of using the SharePoint REST service to access and update SharePoint data, using the REST and OData web protocol standards.</span></span>
 

 <span data-ttu-id="0793f-p101">**Примечание.** Название "приложения для SharePoint" меняется на "надстройки SharePoint". Пока изменения не будут внесены полностью, в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio по-прежнему может встречаться термин "приложение". Дополнительные сведения см. в разделе [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="0793f-p101">The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span></span>
 

<span data-ttu-id="0793f-p102">В SharePoint появилась служба передачи репрезентативного состояния (REST), которую можно сравнить с уже входящими в состав SharePoint [клиентскими объектными моделями](http://msdn.microsoft.com/library/88e5e1b9-eab2-4f3b-a3f2-75c96b86f1f4%28Office.15%29.aspx). Теперь разработчики могут удаленно взаимодействовать непосредственно с данными SharePoint, используя любую технологию, поддерживающую веб-запросы REST. Это означает, что разработчики могут совершать операции **Create**, **Read**, **Update** и **Delete** (CRUD) из надстроек, решений и клиентских приложений SharePoint с помощью веб-технологий REST и стандартного синтаксиса Open Data Protocol (OData).</span><span class="sxs-lookup"><span data-stu-id="0793f-p102">SharePoint 2013 introduced a Representational State Transfer (REST) service that is comparable to the existing SharePoint  [client object models](http://msdn.microsoft.com/library/88e5e1b9-eab2-4f3b-a3f2-75c96b86f1f4%28Office.15%29.aspx). Now, developers can interact remotely with SharePoint data by using any technology that supports REST web requests. This means that developers can perform  **Create**,  **Read**,  **Update**, and  **Delete** (CRUD) operations from their SharePoint Add-ins, solutions, and client applications, using REST web technologies and standard Open Data Protocol (OData) syntax.</span></span>
 

## <a name="prerequisites"></a><span data-ttu-id="0793f-109">Необходимые компоненты</span><span class="sxs-lookup"><span data-stu-id="0793f-109">Prerequisites</span></span>

<span data-ttu-id="0793f-110">В этой статье предполагается, что у вас есть базовое представление о службе REST и создании запросов REST.</span><span class="sxs-lookup"><span data-stu-id="0793f-110">This topic assumes you have a basic familiarity with REST and how to construct REST requests.</span></span>
 

 

## <a name="how-the-sharepoint-rest-service-works"></a><span data-ttu-id="0793f-111">Принцип работы службы REST в SharePoint</span><span class="sxs-lookup"><span data-stu-id="0793f-111">How the SharePoint REST service works</span></span>
<span data-ttu-id="0793f-112"><a name="bk_how"> </a></span><span class="sxs-lookup"><span data-stu-id="0793f-112"></span></span>

<span data-ttu-id="0793f-p103">SharePoint позволяет удаленно взаимодействовать с сайтами SharePoint, используя REST. Теперь вы можете взаимодействовать непосредственно с объектами SharePoint, используя любую технологию, поддерживающую стандартные возможности REST.</span><span class="sxs-lookup"><span data-stu-id="0793f-p103">SharePoint adds the ability for you to remotely interact with SharePoint sites by using REST. Now, you can interact directly with SharePoint objects by using any technology that supports standard REST capabilities.</span></span>
 

 
<span data-ttu-id="0793f-p104">Для доступа к ресурсам SharePoint с помощью REST необходимо создать HTTP-запрос RESTful, используя стандарт Open Data Protocol (OData), который соответствует необходимому API клиентской объектной модели. Пример:</span><span class="sxs-lookup"><span data-stu-id="0793f-p104">To access SharePoint resources using REST, construct a RESTful HTTP request, using the Open Data Protocol (OData) standard, which corresponds to the desired client object model API. For example:</span></span>
 

 
 <span data-ttu-id="0793f-117">*Метод клиентской объектной модели:*</span><span class="sxs-lookup"><span data-stu-id="0793f-117">*Client object model method:*</span></span> 
 

 
<span data-ttu-id="0793f-118">List.GetByTitle(listname)</span><span class="sxs-lookup"><span data-stu-id="0793f-118">List.GetByTitle(listname)</span></span> 
 

 
 <span data-ttu-id="0793f-119">*Конечная точка REST:*</span><span class="sxs-lookup"><span data-stu-id="0793f-119">*REST endpoint:*</span></span> 
 

 
 `http://server/site/_api/lists/getbytitle('listname')`
 

 
<span data-ttu-id="0793f-p105">Веб-служба client.svc в SharePoint обрабатывает HTTP-запрос и предоставляет соответствующий ответ в формате Atom или JSON (JavaScript Object Notation). Затем его должно проанализировать ваше клиентское приложение. На следующем рисунке показано высокоуровневое представление архитектуры SharePoint REST.</span><span class="sxs-lookup"><span data-stu-id="0793f-p105">The client.svc web service in SharePoint handles the HTTP request, and serves the appropriate response in either Atom or JSON (JavaScript Object Notation) format. Your client application must then parse that response. The figure below shows a high-level view of the SharePoint REST architecture.</span></span>
 

 

<span data-ttu-id="0793f-123">**Архитектура службы REST в SharePoint**</span><span class="sxs-lookup"><span data-stu-id="0793f-123">**SharePoint REST service architecture**</span></span>

 

 
![Архитектура службы REST в SharePoint](../../images/SPF15Con_REST_RESTStructure.png)
 
<span data-ttu-id="0793f-125">Благодаря функциональности и простоте использования этих клиентских объектных моделей разработчики чаще всего применяют их для обмена данными с сайтами SharePoint, используя управляемый код для .NET Framework, Silverlight или JavaScript.</span><span class="sxs-lookup"><span data-stu-id="0793f-125">Because of the functionality and ease of use that client object models provide, they remain the primary development option for communicating with SharePoint sites by using .NET Framework managed code, Silverlight, or JavaScript.</span></span>
 

 

### <a name="use-http-commands-with-the-sharepoint-rest-service"></a><span data-ttu-id="0793f-126">Использование команд HTTP со службой REST в SharePoint</span><span class="sxs-lookup"><span data-stu-id="0793f-126">Use HTTP commands with the SharePoint REST service</span></span>
<span data-ttu-id="0793f-127"><a name="bk_usingHTTP"> </a></span><span class="sxs-lookup"><span data-stu-id="0793f-127"></span></span>

<span data-ttu-id="0793f-p106">Чтобы использовать возможности REST, встроенные в SharePoint, необходимо создать HTTP-запрос для REST, используя стандартный OData, что соответствует API клиентской объектной модели, которую вы хотите использовать. Веб-служба client.svc обрабатывает HTTP-запрос и предоставляет соответствующий ответ в формате Atom или JSON (JavaScript Object Notation). Затем его должно проанализировать клиентское приложение.</span><span class="sxs-lookup"><span data-stu-id="0793f-p106">To use the REST capabilities that are built into SharePoint, you construct a RESTful HTTP request, using the OData standard, which corresponds to the client object model API you want to use. The client.svc web service handles the HTTP request and serves the appropriate response in either Atom or JavaScript Object Notation (JSON) format. The client application must then parse that response.</span></span>
 

 
<span data-ttu-id="0793f-p107">Конечные точки в службе REST SharePoint соответствуют типам и элементам клиентских объектных моделей SharePoint. С помощью HTTP-запросов вы можете использовать эти конечные точки REST для выполнения типичных операций CRUD с сущностями SharePoint, такими как списки и сайты.</span><span class="sxs-lookup"><span data-stu-id="0793f-p107">The endpoints in the SharePoint REST service correspond to the types and members in the SharePoint client object models. By using HTTP requests, you can use these REST endpoints to perform typical CRUD operations against SharePoint entities, such as lists and sites.</span></span> 
 

 
<span data-ttu-id="0793f-133">Ниже приводится краткое описание этих операций.</span><span class="sxs-lookup"><span data-stu-id="0793f-133">In general:</span></span>
 

 


|<span data-ttu-id="0793f-134">**Задача**</span><span class="sxs-lookup"><span data-stu-id="0793f-134">**If you want to do this to an endpoint**</span></span>|<span data-ttu-id="0793f-135">**HTTP-запрос**</span><span class="sxs-lookup"><span data-stu-id="0793f-135">**Use this HTTP request**</span></span>|<span data-ttu-id="0793f-136">**Примечания**</span><span class="sxs-lookup"><span data-stu-id="0793f-136">**Keep in mind**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="0793f-137">Чтение ресурса</span><span class="sxs-lookup"><span data-stu-id="0793f-137">Read a resource</span></span>|<span data-ttu-id="0793f-138">**GET**</span><span class="sxs-lookup"><span data-stu-id="0793f-138">**GET**</span></span>||
|<span data-ttu-id="0793f-139">Создание или обновление ресурса</span><span class="sxs-lookup"><span data-stu-id="0793f-139">Create or update a resource</span></span>|<span data-ttu-id="0793f-140">**POST**</span><span class="sxs-lookup"><span data-stu-id="0793f-140">**POST**</span></span>|<span data-ttu-id="0793f-p108">С помощью запроса **POST** можно создавать сущности, например списки и сайты. Служба REST в SharePoint поддерживает отправку команд **POST**, включающих определения объектов, конечным точкам, представляющим коллекции. В операциях **POST** для всех необязательных свойств задаются значения по умолчанию. При попытке задать доступное только для чтения свойство в рамках операции **POST** служба возвращает исключение.</span><span class="sxs-lookup"><span data-stu-id="0793f-p108">Use  **POST** to create entities such as lists and sites. The SharePoint REST service supports sending **POST** commands that include object definitions to endpoints that represent collections.For  **POST** operations, any properties that are not required are set to their default values. If you attempt to set a read-only property as part of a **POST** operation, the service returns an exception.</span></span>|
|<span data-ttu-id="0793f-144">Обновление или вставка ресурса</span><span class="sxs-lookup"><span data-stu-id="0793f-144">Update or insert a resource</span></span> |<span data-ttu-id="0793f-145">**PUT**</span><span class="sxs-lookup"><span data-stu-id="0793f-145">**PUT**</span></span>| <span data-ttu-id="0793f-p109">С помощью операций **PUT** и **MERGE** можно обновлять существующие объекты SharePoint. Любая конечная точка службы, представляющая операцию **set** для свойств объектов, поддерживает как запросы **PUT**, так и запросы **MERGE**. В запросах **MERGE** задавать свойства необязательно. Все свойства, не заданные в явном виде, сохраняют свои текущие значения. В запросах **PUT**, если не указать все обязательные свойства в обновлениях объекта, служба REST возвращает исключение. Кроме того, всем необязательным свойствам, не заданным в явном виде, присваиваются значения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="0793f-p109">Use **PUT** and **MERGE** operations to update existing SharePoint objects. Any service endpoint that represents an object property **set** operation supports both **PUT** requests and **MERGE** requests. For **MERGE** requests, setting properties is optional; any properties that you do not explicitly set retain their current property. For **PUT** requests, if you do not specify all required properties in object updates, the REST service returns an exception. In addition, any optional properties you do not explicitly set are set to their default properties.</span></span>|
|<span data-ttu-id="0793f-151">Удаление ресурса</span><span class="sxs-lookup"><span data-stu-id="0793f-151">Delete a resource</span></span>|<span data-ttu-id="0793f-152">**DELETE**</span><span class="sxs-lookup"><span data-stu-id="0793f-152">**DELETE**</span></span>|<span data-ttu-id="0793f-153">Используйте команду HTTP **DELETE** для URL-адреса определенной конечной точки, чтобы удалить объект SharePoint, представленный этой конечной точкой. Для повторно обрабатываемых объектов (например, списков, файлов и элементов списков) это приведет к выполнению операции **Recycle**.</span><span class="sxs-lookup"><span data-stu-id="0793f-153">Use the HTTP  **DELETE** command against the specific endpoint URL to delete the SharePoint object represented by that endpoint.In the case of recyclable objects, such as lists, files, and list items, this results in a  **Recycle** operation.</span></span>|

### <a name="construct-rest-urls-to-access-sharepoint-resources"></a><span data-ttu-id="0793f-154">Составление URL-адресов REST для доступа к ресурсам SharePoint</span><span class="sxs-lookup"><span data-stu-id="0793f-154">Construct REST URLs to access SharePoint resources</span></span>
<span data-ttu-id="0793f-155"><a name="bk_constructURLs"> </a></span><span class="sxs-lookup"><span data-stu-id="0793f-155"></span></span>

<span data-ttu-id="0793f-p110">Когда возможно, URI для этих конечных точек REST близко имитирует подпись API ресурса в клиентской объектной модели SharePoint. Главные точки входа для службы REST представляют семейство веб-сайтов и сайт указанного контекста.</span><span class="sxs-lookup"><span data-stu-id="0793f-p110">Whenever possible, the URI for these REST endpoints closely mimics the API signature of the resource in the SharePoint client object model. The main entry points for the REST service represent the site collection and site of the specified context.</span></span> 
 

 
<span data-ttu-id="0793f-158">Для доступа к определенному семейству веб-сайтов используйте следующую конструкцию:</span><span class="sxs-lookup"><span data-stu-id="0793f-158">To access a specific site collection, use the following construction:</span></span>
 

 
 `http://server/site/_api/site`
 

 
<span data-ttu-id="0793f-159">Для доступа к определенному сайту используйте следующую конструкцию:</span><span class="sxs-lookup"><span data-stu-id="0793f-159">To access a specific site, use the following construction:</span></span>
 

 
 `http://server/site/_api/web`
 

 
<span data-ttu-id="0793f-160">В обоих случаях *server* представляет имя сервера, а *site* — имя определенного сайта или путь к нему.</span><span class="sxs-lookup"><span data-stu-id="0793f-160">In each case,  *server*  represents the name of the server, and *site*  represents the name of, or path to, the specific site.</span></span>
 

 
<span data-ttu-id="0793f-161">С этой начальной точки вы можете создать более конкретные URI REST, ''обходя" объектную модель, с использованием имен API клиентской объектной модели, разделенных знаком косой черты (/).</span><span class="sxs-lookup"><span data-stu-id="0793f-161">From this starting point, you can then construct more specific REST URIs by ''walking" the object model, using the names of the APIs from the client object model separated by a forward slash (/).</span></span>
 

 
<span data-ttu-id="0793f-p111">Этот синтаксис не применяется к API REST SocialFeedManager или SocialFollowingManager. Подробнее см. в статьях  [Social feed REST API reference for SharePoint](http://msdn.microsoft.com/library/f1cb914f-1e91-4e23-bf53-d2ab323eac13%28Office.15%29.aspx) и [Following people and content REST API reference for SharePoint](http://msdn.microsoft.com/library/c05755df-846d-4a39-941d-950d066cc6d4%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="0793f-p111">This syntax doesn't apply to the SocialFeedManager or SocialFollowingManager REST APIs. See  [Social feed REST API reference for SharePoint](http://msdn.microsoft.com/library/f1cb914f-1e91-4e23-bf53-d2ab323eac13%28Office.15%29.aspx) and [Following people and content REST API reference for SharePoint](http://msdn.microsoft.com/library/c05755df-846d-4a39-941d-950d066cc6d4%28Office.15%29.aspx) for more information.</span></span>
 

 
<span data-ttu-id="0793f-164">В статье  [Определение универсальных кодов ресурсов (URI) конечных точек службы SharePoint REST](determine-sharepoint-rest-service-endpoint-uris) представлены дополнительные инструкции по определению URI конечных точек SharePoint REST из подписи соответствующих API клиентской объектной модели.</span><span class="sxs-lookup"><span data-stu-id="0793f-164">See  [Determine SharePoint REST service endpoint URIs](determine-sharepoint-rest-service-endpoint-uris) for more guidelines for determining SharePoint REST endpoint URIs from the signature of the corresponding client object model APIs.</span></span>
 

 

## <a name="sharepoint-rest-endpoint-examples"></a><span data-ttu-id="0793f-165">Примеры конечных точек REST в SharePoint</span><span class="sxs-lookup"><span data-stu-id="0793f-165">SharePoint REST endpoint examples</span></span>
<span data-ttu-id="0793f-166"><a name="bk_URLexamples"> </a></span><span class="sxs-lookup"><span data-stu-id="0793f-166"></span></span>

<span data-ttu-id="0793f-p112">В приведенной ниже таблице представлены типичные примеры URL-адресов для конечных точек REST, которые помогут вам приступить к работе с данными SharePoint. Чтобы составить полный URL-адрес REST, добавьте строку `http://server/site/_api/` в начале фрагментов URL-адресов, показанных в таблице. При необходимости для команд **POST** в таблице приводятся примеры данных, которые необходимо передать в тексте HTTP-запроса для создания указанного элемента SharePoint. Элементы, выделенные курсивом, представляют переменные, вместо которых необходимо подставить свои значения.</span><span class="sxs-lookup"><span data-stu-id="0793f-p112">The following table contains typical REST endpoint URL examples to get you started working with SharePoint data. Prepend  `http://server/site/_api/` to the URL fragments shown in the table to construct a fully qualified REST URL. Where necessary for **POST** commands, the table contains sample data you must pass in the HTTP request body to create the specified SharePoint item. Items in italics represent variables that you must replace with your values.</span></span>
 

 


|<span data-ttu-id="0793f-171">**Описание**</span><span class="sxs-lookup"><span data-stu-id="0793f-171">**Description**</span></span>|<span data-ttu-id="0793f-172">**Конечная точка URL-адреса**</span><span class="sxs-lookup"><span data-stu-id="0793f-172">**URL endpoint**</span></span>|<span data-ttu-id="0793f-173">**Метод HTTP**</span><span class="sxs-lookup"><span data-stu-id="0793f-173">**HTTP method**</span></span>|<span data-ttu-id="0793f-174">**Содержимое текста**</span><span class="sxs-lookup"><span data-stu-id="0793f-174">**Body content**</span></span>|
|:-----|:-----|:-----|:-----|
|<span data-ttu-id="0793f-175">Получает заголовок списка</span><span class="sxs-lookup"><span data-stu-id="0793f-175">Retrieves the title of a list</span></span>| `web/title`|<span data-ttu-id="0793f-176">GET</span><span class="sxs-lookup"><span data-stu-id="0793f-176">GET</span></span>|<span data-ttu-id="0793f-177">Не применимо</span><span class="sxs-lookup"><span data-stu-id="0793f-177">Not applicable</span></span>|
|<span data-ttu-id="0793f-178">Получает все списки на сайте</span><span class="sxs-lookup"><span data-stu-id="0793f-178">Retrieves all lists on a site</span></span>| `lists`|<span data-ttu-id="0793f-179">GET</span><span class="sxs-lookup"><span data-stu-id="0793f-179">GET</span></span>|<span data-ttu-id="0793f-180">Не применимо</span><span class="sxs-lookup"><span data-stu-id="0793f-180">Not applicable</span></span>|
|<span data-ttu-id="0793f-181">Получает метаданные одного списка</span><span class="sxs-lookup"><span data-stu-id="0793f-181">Retrieves a single 'list's metadata</span></span>| `lists/getbytitle('listname')`|<span data-ttu-id="0793f-182">GET</span><span class="sxs-lookup"><span data-stu-id="0793f-182">GET</span></span>|<span data-ttu-id="0793f-183">Не применимо</span><span class="sxs-lookup"><span data-stu-id="0793f-183">Not applicable</span></span>|
|<span data-ttu-id="0793f-184">Получает элементы списка</span><span class="sxs-lookup"><span data-stu-id="0793f-184">Retrieves items within a list</span></span>| `lists/getbytitle('listname')/items`|<span data-ttu-id="0793f-185">GET</span><span class="sxs-lookup"><span data-stu-id="0793f-185">GET</span></span>|<span data-ttu-id="0793f-186">Неприменимо</span><span class="sxs-lookup"><span data-stu-id="0793f-186">Not applicable</span></span>|
|<span data-ttu-id="0793f-p113">Получает определенное свойство документа (в данном случае это заголовок документа)</span><span class="sxs-lookup"><span data-stu-id="0793f-p113">Retrieves a specific property of a document. (In this case, the document title.)</span></span>| `lists/getbytitle('listname')?select=Title`|<span data-ttu-id="0793f-189">GET</span><span class="sxs-lookup"><span data-stu-id="0793f-189">GET</span></span>|<span data-ttu-id="0793f-190">Не применимо</span><span class="sxs-lookup"><span data-stu-id="0793f-190">Not applicable</span></span>|
|<span data-ttu-id="0793f-191">Создает список</span><span class="sxs-lookup"><span data-stu-id="0793f-191">Creates a list</span></span>| `lists`|<span data-ttu-id="0793f-192">POST</span><span class="sxs-lookup"><span data-stu-id="0793f-192">POST</span></span>|
```
{
  '__metadata':{'type':SP.List},
  'AllowContentTypes': true,
  'BaseTemplate': 104 ,
  'ContentTypesEnabled': true,
  'Description': 'My list description ',
  'Title': 'RestTest '
}
```

<span data-ttu-id="0793f-193">|Добавляет элемент в список| `lists/getbytitle('listname')/items`|POST|</span><span class="sxs-lookup"><span data-stu-id="0793f-193">|Adds an item to a list| `lists/getbytitle('listname')/items`|POST|</span></span>
```
{
  '__metadata':{'type': SP.Data.'listname'.ListItem},
  'Title': 'MyItem'
}

```

|

## <a name="batch-job-support"></a><span data-ttu-id="0793f-194">Поддержка пакетных заданий</span><span class="sxs-lookup"><span data-stu-id="0793f-194">Batch job support</span></span>
<span data-ttu-id="0793f-195"><a name="batch"> </a></span><span class="sxs-lookup"><span data-stu-id="0793f-195"></span></span>

<span data-ttu-id="0793f-p114">Служба REST SharePoint Online (а также локального выпуска SharePoint 2016 или более поздней версии) поддерживает объединение нескольких запросов в одном вызове службы с помощью параметра запроса OData  `$batch`. Дополнительные сведения и ссылки на примеры кода см. в разделе  [Создание пакетного запроса с помощью интерфейсов REST API](make-batch-requests-with-the-rest-apis).</span><span class="sxs-lookup"><span data-stu-id="0793f-p114">The SharePoint Online (and on-premise SharePoint 2016 or later) REST service supports combining multiple requests into a single call to the service by using the OData  `$batch` query option. For details and links to code samples, see [Make batch requests with the REST APIs](make-batch-requests-with-the-rest-apis). .</span></span>
 

 

## <a name="additional-resources"></a><span data-ttu-id="0793f-199">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="0793f-199">Additional Resources</span></span>
<span data-ttu-id="0793f-200"><a name="bk_learnmore"> </a></span><span class="sxs-lookup"><span data-stu-id="0793f-200"></span></span>

<span data-ttu-id="0793f-201">Из перечисленных ниже ресурсов вы можете узнать больше об использовании службы REST в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="0793f-201">Use the resources listed below to learn more about using the SharePoint REST service.</span></span>
 

 

|<span data-ttu-id="0793f-202">**Название**</span><span class="sxs-lookup"><span data-stu-id="0793f-202">**Title**</span></span>|<span data-ttu-id="0793f-203">**Описание**</span><span class="sxs-lookup"><span data-stu-id="0793f-203">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="0793f-204">Выполнение базовых операций с использованием конечных точек SharePoint REST</span><span class="sxs-lookup"><span data-stu-id="0793f-204">Complete basic operations using SharePoint REST endpoints</span></span>](complete-basic-operations-using-sharepoint-2013-rest-endpoints)|<span data-ttu-id="0793f-205">Узнайте, как выполнять операции CRUD (создание, чтение, обновление, удаление) с помощью интерфейса REST SharePoint.</span><span class="sxs-lookup"><span data-stu-id="0793f-205">Learn how to perform basic create, read, update, and delete (CRUD) operations with the SharePoint REST interface.</span></span>|
| [<span data-ttu-id="0793f-206">Работа со списками и элементами списков в службе REST</span><span class="sxs-lookup"><span data-stu-id="0793f-206">Working with lists and list items with REST</span></span>](working-with-lists-and-list-items-with-rest)|<span data-ttu-id="0793f-207">Узнайте, как выполнять основные операции по созданию, чтению, обновлению и удалению списков и элементов списков с помощью интерфейса REST SharePoint.</span><span class="sxs-lookup"><span data-stu-id="0793f-207">Learn how to perform basic create, read, update, and delete (CRUD) operations on lists and list items with the SharePoint REST interface.</span></span>|
| [<span data-ttu-id="0793f-208">Работа с папками и файлами в службе REST</span><span class="sxs-lookup"><span data-stu-id="0793f-208">Working with folders and files with REST</span></span>](working-with-folders-and-files-with-rest)|<span data-ttu-id="0793f-209">Узнайте, как выполнять основные операции по созданию, чтению, обновлению и удалению папок и файлов с помощью интерфейса REST SharePoint.</span><span class="sxs-lookup"><span data-stu-id="0793f-209">Learn how to perform basic create, read, update, and delete (CRUD) operations on folders and files with the SharePoint REST interface.</span></span>|
| [<span data-ttu-id="0793f-210">Навигация по структуре данных SharePoint, представленной в службе REST</span><span class="sxs-lookup"><span data-stu-id="0793f-210">Navigate the SharePoint data structure represented in the REST service</span></span>](navigate-the-sharepoint-data-structure-represented-in-the-rest-service)|<span data-ttu-id="0793f-211">Узнайте, как с помощью конечной точки REST в элементе SharePoint получить доступ к связанным элементам, например родительским сайтам или структуре библиотеки, в которой находится этот элемент.</span><span class="sxs-lookup"><span data-stu-id="0793f-211">Learn how to start from a REST endpoint for a given SharePoint item, and navigate to and access related items, such as parent sites or the library structure where that item resides.</span></span>|
| [<span data-ttu-id="0793f-212">Определение универсальных кодов ресурсов (URI) конечных точек службы SharePoint REST</span><span class="sxs-lookup"><span data-stu-id="0793f-212">Determine SharePoint REST service endpoint URIs</span></span>](determine-sharepoint-rest-service-endpoint-uris)|<span data-ttu-id="0793f-213">В этой статье представлены общие инструкции, позволяющие определить URI конечных точек REST в SharePoint, используя подписи соответствующих API клиентской объектной модели.</span><span class="sxs-lookup"><span data-stu-id="0793f-213">Learn general guidelines for determining SharePoint REST endpoint URIs from the signature of the corresponding client object model APIs.</span></span>|
| [<span data-ttu-id="0793f-214">Использование операций запросов OData в запросах SharePoint REST</span><span class="sxs-lookup"><span data-stu-id="0793f-214">Use OData query operations in SharePoint REST requests</span></span>](use-odata-query-operations-in-sharepoint-rest-requests)|<span data-ttu-id="0793f-215">Узнайте, как использовать широкий спектр операторов строки запроса OData для выбора, фильтрации и упорядочивания данных, запрашиваемых у службы REST SharePoint.</span><span class="sxs-lookup"><span data-stu-id="0793f-215">Learn how to use a wide range of OData query string operators to select, filter, and order the data you request from the SharePoint REST service.</span></span>|
| [<span data-ttu-id="0793f-216">SharePoint REST API, конечные точки и примеры</span><span class="sxs-lookup"><span data-stu-id="0793f-216">REST API reference and samples</span></span>](http://msdn.microsoft.com/library/rest-api-reference-and-samples%28Office.15%29.aspx)|<span data-ttu-id="0793f-217">На этой странице приведены ссылки на все ресурсы по REST, доступные для разработчиков SharePoint в MSDN.</span><span class="sxs-lookup"><span data-stu-id="0793f-217">This page contains links to all of the REST resources that are available for SharePoint developers on MSDN.</span></span>|
| [<span data-ttu-id="0793f-218">Общие сведения о REST API для службы поиска SharePoint</span><span class="sxs-lookup"><span data-stu-id="0793f-218">SharePoint Search REST API overview</span></span>](http://msdn.microsoft.com/library/8a4f7863-e4c1-4099-9189-a1894db36930%28Office.15%29.aspx)|<span data-ttu-id="0793f-219">Добавление функции поиска в клиентские и мобильные приложения с помощью службы поиска REST в SharePoint Server 2013 и в любой технологии, поддерживающей веб-запросы REST.</span><span class="sxs-lookup"><span data-stu-id="0793f-219">Add search functionality to client and mobile applications using the Search REST service in SharePoint Server 2013 and any technology that supports REST web requests.</span></span>|
| [<span data-ttu-id="0793f-220">Social feed REST API reference for SharePoint</span><span class="sxs-lookup"><span data-stu-id="0793f-220">Social feed REST API reference for SharePoint</span></span>](http://msdn.microsoft.com/library/f1cb914f-1e91-4e23-bf53-d2ab323eac13%28Office.15%29.aspx)|<span data-ttu-id="0793f-221">Подробнее о конечных точках REST SharePoint для выполнения задач, связанных с каналами.</span><span class="sxs-lookup"><span data-stu-id="0793f-221">Learn about SharePoint REST endpoints for feed-related tasks.</span></span>|
| [<span data-ttu-id="0793f-222">Following people and content REST API reference for SharePoint</span><span class="sxs-lookup"><span data-stu-id="0793f-222">Following people and content REST API reference for SharePoint</span></span>](http://msdn.microsoft.com/library/c05755df-846d-4a39-941d-950d066cc6d4%28Office.15%29.aspx)|<span data-ttu-id="0793f-223">Подробнее о конечных точках REST SharePoint для подписки на людей и контент.</span><span class="sxs-lookup"><span data-stu-id="0793f-223">Learn about SharePoint REST endpoints for following people and content.</span></span>|
| [<span data-ttu-id="0793f-224">Создание пакетного запроса с помощью интерфейсов REST API</span><span class="sxs-lookup"><span data-stu-id="0793f-224">Make batch requests with the REST APIs</span></span>](make-batch-requests-with-the-rest-apis)|<span data-ttu-id="0793f-225">Узнайте, как объединить несколько запросов в один пот вызове службы REST.</span><span class="sxs-lookup"><span data-stu-id="0793f-225">Learn how to combine multiple requests into a single call to the REST service.</span></span>|
| [<span data-ttu-id="0793f-226">Синхронизация элементов SharePoint с помощью службы REST</span><span class="sxs-lookup"><span data-stu-id="0793f-226">Synchronize SharePoint items using the REST service</span></span>](synchronize-sharepoint-items-using-the-rest-service)|<span data-ttu-id="0793f-227">Узнайте, как синхронизировать элементы между SharePoint и надстройками или службами с помощью ресурса **GetListItemChangesSinceToken**, входящего в состав службы REST в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="0793f-227">Learn how to synchronize items between SharePoint and your add-ins or services by using the **GetListItemChangesSinceToken** resource, part of the SharePoint REST service.</span></span>|
| [<span data-ttu-id="0793f-228">Получение версий элементов из списка документов с помощью значений ETag через службы REST</span><span class="sxs-lookup"><span data-stu-id="0793f-228">Use ETag values through the REST service to get document list item versioning</span></span>](http://msdn.microsoft.com/library/5f7e0579-46b7-44ab-b3b4-cdbc622dcd98%28Office.15%29.aspx)|<span data-ttu-id="0793f-229">Узнайте, как использовать теги HTML ETag в службе REST SharePoint для управления параллелизмом списков SharePoint и их элементов.</span><span class="sxs-lookup"><span data-stu-id="0793f-229">Learn how to use HTML ETags with the SharePoint REST service for concurrency control of SharePoint lists and list items.</span></span>|

## <a name="odata-resources"></a><span data-ttu-id="0793f-230">Материалы по OData</span><span class="sxs-lookup"><span data-stu-id="0793f-230">OData resources</span></span>
<span data-ttu-id="0793f-231"><a name="SP15startREST_bk_addlresources"> </a></span><span class="sxs-lookup"><span data-stu-id="0793f-231"></span></span>


 

 

-  [<span data-ttu-id="0793f-232">Знакомство с OData</span><span class="sxs-lookup"><span data-stu-id="0793f-232">Introducing OData</span></span>](http://msdn.microsoft.com/en-us/data/hh237663)
    
 
-  [<span data-ttu-id="0793f-233">Примеры для протокола Open Data Protocol</span><span class="sxs-lookup"><span data-stu-id="0793f-233">Open Data Protocol by Example</span></span>](http://msdn.microsoft.com/ru-ru/library/ff478141.aspx)
    
 
-  [<span data-ttu-id="0793f-234">Open Data Protocol</span><span class="sxs-lookup"><span data-stu-id="0793f-234">Open Data Protocol</span></span>](http://www.odata.org/)
    
 
-  [<span data-ttu-id="0793f-235">Соглашения об URI для протокола OData</span><span class="sxs-lookup"><span data-stu-id="0793f-235">OData Protocol URI Conventions</span></span>](http://www.odata.org/documentation/odata-version-2-0/uri-conventions/)
    
 
-  [<span data-ttu-id="0793f-236">Адресация для операций службы</span><span class="sxs-lookup"><span data-stu-id="0793f-236">Addressing Service Operations</span></span>](http://www.odata.org/documentation/odata-version-2-0/uri-conventions#AddressingServiceOperations)
    
 
-  [<span data-ttu-id="0793f-237">Операции протокола OData</span><span class="sxs-lookup"><span data-stu-id="0793f-237">OData Protocol Operations</span></span>](http://www.odata.org/documentation/odata-version-2-0/operations/)
    
 
-  [<span data-ttu-id="0793f-238">Условия ошибок</span><span class="sxs-lookup"><span data-stu-id="0793f-238">Error Conditions</span></span>](http://www.odata.org/documentation/odata-version-2-0/operations#ErrorConditions)
    
 

