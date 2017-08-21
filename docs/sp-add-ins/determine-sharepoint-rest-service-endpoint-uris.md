# <a name="determine-sharepoint-rest-service-endpoint-uris"></a><span data-ttu-id="ced2f-101">Как определить URI конечных точек службы REST в SharePoint</span><span class="sxs-lookup"><span data-stu-id="ced2f-101">Determine SharePoint REST service endpoint URIs</span></span>
<span data-ttu-id="ced2f-102">В этой статье представлены общие рекомендации по определению URI конечных точек REST в SharePoint с помощью подписей соответствующих API клиентской объектной модели.</span><span class="sxs-lookup"><span data-stu-id="ced2f-102">Learn general guidelines for determining SharePoint REST endpoint URIs from the signature of the corresponding client object model APIs.</span></span>
 

 <span data-ttu-id="ced2f-p101">**Примечание.** Название "приложения для SharePoint" меняется на "надстройки SharePoint". Пока изменения не будут внесены полностью, в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio по-прежнему может встречаться термин "приложение". Дополнительные сведения см. в разделе [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="ced2f-p101">The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span></span>
 

 <span data-ttu-id="ced2f-106">**Перед началом работы**</span><span class="sxs-lookup"><span data-stu-id="ced2f-106">**Before you start**</span></span>
 

-  [<span data-ttu-id="ced2f-107">Знакомство со службой REST в SharePoint</span><span class="sxs-lookup"><span data-stu-id="ced2f-107">Get to know the SharePoint REST service</span></span>](get-to-know-the-sharepoint-2013-rest-service)
    
 
-  [<span data-ttu-id="ced2f-108">Навигация по структуре данных SharePoint, представленной в службе REST</span><span class="sxs-lookup"><span data-stu-id="ced2f-108">Navigate the SharePoint data structure represented in the REST service</span></span>](navigate-the-sharepoint-data-structure-represented-in-the-rest-service)
    
 
<span data-ttu-id="ced2f-109">**Дальнейшие действия**</span><span class="sxs-lookup"><span data-stu-id="ced2f-109">**Next steps**</span></span>
 

-  [<span data-ttu-id="ced2f-110">Использование операций запросов OData в запросах REST SharePoint</span><span class="sxs-lookup"><span data-stu-id="ced2f-110">Use OData query operations in SharePoint REST requests</span></span>](use-odata-query-operations-in-sharepoint-rest-requests)
    
 

## <a name="sharepoint-rest-endpoint-uri-structure"></a><span data-ttu-id="ced2f-111">Структура URI конечной точки REST в SharePoint</span><span class="sxs-lookup"><span data-stu-id="ced2f-111">SharePoint REST endpoint URI structure</span></span>

<span data-ttu-id="ced2f-p102">Чтобы иметь возможность доступа к ресурсу SharePoint с помощью службы REST, сначала необходимо определить конечную точку URI, которая указывает на этот ресурс. Когда возможно, URI для этих конечных точек REST близко имитирует подпись API ресурса в клиентской объектной модели SharePoint. Пример:</span><span class="sxs-lookup"><span data-stu-id="ced2f-p102">Before you can access a SharePoint resource using the REST service, you first have to figure out the URI endpoint that points to that resource. Whenever possible, the URI for these REST endpoints closely mimics the API signature of the resource in the SharePoint client object model. For example:</span></span>
 

 
 <span data-ttu-id="ced2f-115">*Метод клиентской объектной модели:*</span><span class="sxs-lookup"><span data-stu-id="ced2f-115">*Client object model method:*</span></span> 
 

 
<span data-ttu-id="ced2f-116">List.GetByTitle(listname).GetItems()</span><span class="sxs-lookup"><span data-stu-id="ced2f-116">List.GetByTitle(listname).GetItems()</span></span>
 

 
 <span data-ttu-id="ced2f-117">*Конечная точка REST:*</span><span class="sxs-lookup"><span data-stu-id="ced2f-117">*REST endpoint:*</span></span> 
 

 
 `http://server/site/_api/lists/getbytitle('listname')/items`
 

 
<span data-ttu-id="ced2f-118">Но в некоторых случаях URI конечной точки отличается от соответствующей подписи клиентской объектной модели для соответствия соглашениям REST или OData.</span><span class="sxs-lookup"><span data-stu-id="ced2f-118">In some cases, however, the endpoint URI differs from the corresponding client object model signature, in order to comply with REST or OData conventions.</span></span>
 

 
<span data-ttu-id="ced2f-119">На приведенном ниже рисунке показана общая структура синтаксиса для URI конечных точек REST в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="ced2f-119">The following figure shows the general syntax structure of SharePoint REST URIs.</span></span> 
 

 

<span data-ttu-id="ced2f-120">**Структура синтаксиса URI REST в SharePoint**</span><span class="sxs-lookup"><span data-stu-id="ced2f-120">**SharePoint REST URI syntax structure**</span></span>

 

 
![Синтаксис запроса REST SharePoint](../../images/SPF15Con_REST_OverallSyntax.png)
 
<span data-ttu-id="ced2f-122">Синтаксис некоторых конечных точек для ресурсов SharePoint не соответствует этой структуре:</span><span class="sxs-lookup"><span data-stu-id="ced2f-122">Some endpoints for SharePoint resources deviate from this syntax structure:</span></span>
 

 

 

- <span data-ttu-id="ced2f-123">Методы, в качестве параметров которых требуются сложные типы.</span><span class="sxs-lookup"><span data-stu-id="ced2f-123">Methods that require complex types as parameters.</span></span> 
    
    <span data-ttu-id="ced2f-124">Если соответствующий метод клиентской объектной модели требует, чтобы в качестве параметров передавались сложные типы, конечная точка REST может отклоняться от этой структуры синтаксиса в связи с ограничениями REST.</span><span class="sxs-lookup"><span data-stu-id="ced2f-124">If the corresponding client object model method requires that complex types are passed as parameters, the REST endpoint may deviate from this syntax construction to account for REST limitations.</span></span>
    
 
- <span data-ttu-id="ced2f-125">Статические методы и свойства.</span><span class="sxs-lookup"><span data-stu-id="ced2f-125">Static methods and properties.</span></span> 
    
    <span data-ttu-id="ced2f-126">Синтаксис конечных точек REST отличается от структуры синтаксиса для URI, представляющих статические методы и свойства.</span><span class="sxs-lookup"><span data-stu-id="ced2f-126">REST endpoints deviate from this syntax structure for URIs that represent static methods and properties.</span></span>
    
 

## <a name="determine-sharepoint-rest-service-endpoints"></a><span data-ttu-id="ced2f-127">Как определить конечные точки службы REST в SharePoint</span><span class="sxs-lookup"><span data-stu-id="ced2f-127">Determine SharePoint REST service endpoints</span></span>

<span data-ttu-id="ced2f-128">Чтобы создать конечную точку REST для ресурса SharePoint, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="ced2f-128">To construct a REST endpoint for a SharePoint resource, follow these steps:</span></span>
 

 

1. <span data-ttu-id="ced2f-129">Начните со ссылки на службу REST:</span><span class="sxs-lookup"><span data-stu-id="ced2f-129">Start with the REST service reference:</span></span>
    
     `http://server/site/_api`
    
 
2. <span data-ttu-id="ced2f-p103">Укажите соответствующую точку входа. Например:</span><span class="sxs-lookup"><span data-stu-id="ced2f-p103">Specify the appropriate entry point. For example:</span></span>
    
     `http://server/site/_api/web`
    
 
3. <span data-ttu-id="ced2f-p104">Перейдите от точки входа к конкретным ресурсам, к которым нужно получить доступ. Это включает указание параметров для конечных точек, которые соответствуют методам в клиентской объектной модели. Например:</span><span class="sxs-lookup"><span data-stu-id="ced2f-p104">Navigate from the entry point to the specific resources you want to access. This includes specifying parameters for endpoints that correspond to methods in the client object model. For example:</span></span>
    
     `http://server/site/_api/web/lists/getbytitle('listname')`
    
 

### <a name="reference-the-sharepoint-rest-service-in-your-endpoint-uri"></a><span data-ttu-id="ced2f-135">Ссылка на службу REST SharePoint в URI конечной точки</span><span class="sxs-lookup"><span data-stu-id="ced2f-135">Reference the SharePoint REST service in your endpoint URI</span></span>

<span data-ttu-id="ced2f-p105">Используйте `_api`, чтобы указать ссылку на службу REST SharePoint в URI конечной точки. Служба REST входит в состав веб-службы client.svc. Но чтобы упростить создание URI REST и сократить базовый путь к URI REST, служба REST использует `_api`, избавляя от необходимости явно ссылаться на веб-службу client.svc. Служба REST по-прежнему распознает и принимает URI, которые ссылаются на веб-службу client.svc. Например, вы можете использовать `http://server/site/_vti_bin/client.svc/web/lists` вместо `http://server/site/_api/web/lists`. Однако предпочтительней использовать `_api`. Максимальная длина URL-адреса составляет 256 символов, а `_api` сокращает базовый URI, оставляя в запасе больше символов для составления URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="ced2f-p105">Use  `_api` to denote the SharePoint REST service in your endpoint URIs. The REST service is part of the client.svc web service. However, to make REST URI construction easier and to shorten the base REST URI path, the REST service uses `_api` to abstract away the need to explicitly reference the client.svc web service. The REST service still recognizes and accepts URIs that reference the client.svc web service. For example, you can use `http://server/site/_vti_bin/client.svc/web/lists` instead of `http://server/site/_api/web/lists`. However, using  `_api` is the preferred convention. URLs have a 256 character limit, so using `_api` shortens the base URI, leaving more characters for use in constructing the rest of the URL.</span></span>
 

 

### <a name="specify-entry-points-for-the-sharepoint-rest-service"></a><span data-ttu-id="ced2f-143">Указание точек входа для службы REST SharePoint</span><span class="sxs-lookup"><span data-stu-id="ced2f-143">Specify entry points for the SharePoint REST service</span></span>

<span data-ttu-id="ced2f-p106">Основные точки входа для службы REST представляют семейство веб-сайтов и сайт указанного контекста. Таким образом, эти точки входа соответствуют свойствам **ClientContext.Site** и **ClientContext.Web** клиентских объектных моделей.</span><span class="sxs-lookup"><span data-stu-id="ced2f-p106">The main entry points for the REST service represent the site collection and site of the specified context. In this way, these entry points correspond to the  **ClientContext.Site** property and **ClientContext.Web** property in the client object models.</span></span>
 

 
<span data-ttu-id="ced2f-146">Для доступа к определенному семейству веб-сайтов используйте следующую конструкцию:</span><span class="sxs-lookup"><span data-stu-id="ced2f-146">To access a specific site collection, use the following construction:</span></span>
 

 
 `http://server/site/_api/site`
 

 
<span data-ttu-id="ced2f-147">Для доступа к определенному сайту используйте следующую конструкцию:</span><span class="sxs-lookup"><span data-stu-id="ced2f-147">To access a specific site, use the following construction:</span></span>
 

 
 `http://server/site/_api/web`
 

 
<span data-ttu-id="ced2f-148">В этих примерах *server* представляет имя сервера, а *site* — имя определенного сайта или путь к нему.</span><span class="sxs-lookup"><span data-stu-id="ced2f-148">Where  *server*  represents the name of the server, and *site*  represents the name of, or path to, the specific site.</span></span>
 

 
<span data-ttu-id="ced2f-p107">Помимо `/site` и `/web`, служба REST включает несколько других точек доступа, которые позволяют разработчикам переходить к определенным компонентам. В приведенной ниже таблице перечислены эти точки доступа.</span><span class="sxs-lookup"><span data-stu-id="ced2f-p107">In addition to  `/site` and `/web`, the REST service includes several other access points that enable developers to navigate to specific functionality. The table below lists some of these access points.</span></span>
 

 


|<span data-ttu-id="ced2f-151">**Область функций**</span><span class="sxs-lookup"><span data-stu-id="ced2f-151">**Feature area**</span></span>|<span data-ttu-id="ced2f-152">**Точка доступа**</span><span class="sxs-lookup"><span data-stu-id="ced2f-152">**Access point**</span></span>|
|:-----|:-----|
|<span data-ttu-id="ced2f-153">Сайт</span><span class="sxs-lookup"><span data-stu-id="ced2f-153">Site</span></span>|<span data-ttu-id="ced2f-154">http:// _server/site_/_api/site</span><span class="sxs-lookup"><span data-stu-id="ced2f-154">http:// _server/site_/_api/site</span></span>|
|<span data-ttu-id="ced2f-155">Интернет</span><span class="sxs-lookup"><span data-stu-id="ced2f-155">Web</span></span>|<span data-ttu-id="ced2f-156">http:// _server/site_/_api/web</span><span class="sxs-lookup"><span data-stu-id="ced2f-156">http:// _server/site_/_api/web</span></span>|
|<span data-ttu-id="ced2f-157">Профили пользователей</span><span class="sxs-lookup"><span data-stu-id="ced2f-157">User Profile</span></span>|<span data-ttu-id="ced2f-158">http:// _server/site_/_api/SP.UserProfiles.PeopleManager</span><span class="sxs-lookup"><span data-stu-id="ced2f-158">http:// _server/site_/_api/SP.UserProfiles.PeopleManager</span></span>|
|<span data-ttu-id="ced2f-159">Поиск</span><span class="sxs-lookup"><span data-stu-id="ced2f-159">Search</span></span>|<span data-ttu-id="ced2f-160">http:// _server/site_/_api/search</span><span class="sxs-lookup"><span data-stu-id="ced2f-160">http:// _server/site_/_api/search</span></span>|

### <a name="navigate-to-the-specific-resources-you-want-to-access"></a><span data-ttu-id="ced2f-161">Переход к определенным ресурсам, к которым требуется получить доступ</span><span class="sxs-lookup"><span data-stu-id="ced2f-161">Navigate to the specific resources you want to access</span></span>

<span data-ttu-id="ced2f-p108">С этой точки можно создавать более конкретные конечные точки REST, ''обходя" объектную модель, с использованием имен API клиентской объектной модели, разделенных знаком косой черты (/). В таблице ниже показаны примеры вызовов клиентских объектных моделей и эквивалентные им конечные точки.</span><span class="sxs-lookup"><span data-stu-id="ced2f-p108">From here, construct more specific REST endpoints by ''walking" the object model, using the names of the APIs from the client object model separated by a forward slash (/). The table below shows examples of client object model calls and the equivalent REST endpoint.</span></span> 
 

 


|<span data-ttu-id="ced2f-164">**API клиентской объектной модели**</span><span class="sxs-lookup"><span data-stu-id="ced2f-164">**Client object model API **</span></span>|<span data-ttu-id="ced2f-165">**Конечная точка REST**</span><span class="sxs-lookup"><span data-stu-id="ced2f-165">**REST endpoint**</span></span>|
|:-----|:-----|
|<span data-ttu-id="ced2f-166">ClientContext.Web.Lists</span><span class="sxs-lookup"><span data-stu-id="ced2f-166">ClientContext.Web.Lists</span></span>|<span data-ttu-id="ced2f-167">http:// _server_/ _site_/_api/web/lists</span><span class="sxs-lookup"><span data-stu-id="ced2f-167">http:// _server_/ _site_/_api/web/lists</span></span>|
|<span data-ttu-id="ced2f-168">ClientContext.Web.Lists[guid]</span><span class="sxs-lookup"><span data-stu-id="ced2f-168">ClientContext.Web.Lists[guid]</span></span>|<span data-ttu-id="ced2f-169">http:// _server_/ _site_/_api/web/lists('_guid_')</span><span class="sxs-lookup"><span data-stu-id="ced2f-169">http:// _server_/ _site_/_api/web/lists(' _guid_')</span></span>|
|<span data-ttu-id="ced2f-170">ClientContext.Web.Lists.GetByTitle("Title")</span><span class="sxs-lookup"><span data-stu-id="ced2f-170">ClientContext.Web.Lists.GetByTitle("Title")</span></span>|<span data-ttu-id="ced2f-171">http:// _server_/ _site_/_api/web/lists/getbytitle('_Title_')</span><span class="sxs-lookup"><span data-stu-id="ced2f-171">http:// _server_/ _site_/_api/web/lists/getbytitle(' _Title_')</span></span>|
<span data-ttu-id="ced2f-p109">URI конечных точек указываются с учетом регистра. В примере из предыдущей таблицы используется метод `/getbytitle` — аналог метода **GetByTitle()** в службе REST.</span><span class="sxs-lookup"><span data-stu-id="ced2f-p109">Endpoint URIs are case-insensitive. In the previous table, for example, use  `/getbytitle` to specify the REST equivalent of the **GetByTitle()** method.</span></span>
 

 

## <a name="specify-parameters-in-rest-endpoint-uris"></a><span data-ttu-id="ced2f-174">Как указать параметры в URI конечных точек REST</span><span class="sxs-lookup"><span data-stu-id="ced2f-174">Specify parameters in REST endpoint URIs</span></span>

<span data-ttu-id="ced2f-p110">SharePoint расширяет спецификацию OData, позволяя использовать скобки для указания параметров метода и значений индекса. Это предотвращает потенциальные проблемы из-за неоднозначности в URI, содержащих несколько параметров с одинаковым именем. Например, два следующих URI содержат параметры с одинаковым именем:</span><span class="sxs-lookup"><span data-stu-id="ced2f-p110">SharePoint extends the OData specification to enable you to use parentheses to specify method parameters and index values. This prevents potential disambiguation issues in URIs that contain multiple parameters with the same name. For example, the following two URIs contain parameters that have the same name:</span></span>
 

 
 `http://server/site/_api/web/lists/getByTitle('Announcements')/fields/getByTitle('Description')`
 

 
 `http://server/site/_api/web/lists('<guid>')/fields/getById('<guid>')`
 

 
<span data-ttu-id="ced2f-p111">Чтобы указать несколько параметров, включите параметр в формате "значение-имя" и разделите параметры запятыми. Например:</span><span class="sxs-lookup"><span data-stu-id="ced2f-p111">To specify multiple parameters, include the parameter as a name-value pair, and separate the parameters with commas. For example:</span></span>
 

 
 `http://server/site/_api/web/getAvailableWebTemplates(lcid=1033, includeCrossLanguage=true)`
 

 
<span data-ttu-id="ced2f-180">На приведенном ниже рисунке показан синтаксис параметров службы REST в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="ced2f-180">The following figure shows the SharePoint REST parameter syntax.</span></span>
 

 

<span data-ttu-id="ced2f-181">**Синтаксис параметров службы REST в SharePoint**</span><span class="sxs-lookup"><span data-stu-id="ced2f-181">**SharePoint REST parameter syntax**</span></span>

 

 
![Синтаксис параметров метода службы REST в SharePoint](../../images/SPF15Con_REST_parameterSyntax.png)
 

### <a name="complex-types-as-parameters-for-the-rest-service"></a><span data-ttu-id="ced2f-183">Сложные типы в качестве параметров для службы REST</span><span class="sxs-lookup"><span data-stu-id="ced2f-183">Complex types as parameters for the REST service</span></span>

<span data-ttu-id="ced2f-p112">Некоторые методы клиентской объектной модели принимают полезные данные больших размеров в качестве параметра. Для обеспечения паритета функциональности между конечными точками REST и соответствующими API клиентской объектной модели необходимо, чтобы конечные точки принимали параметр сложного типа. В таких случаях служба REST расширяет существующий протокол OData, позволяя этим конечным точкам REST принимать один параметр сложного типа. Это относится только к операциям **POST**, а сложный тип необходимо передавать в формате [Atom](http://www.odata.org/developers/protocols/atom-format#RepresentingComplexTypesProperties) или [JSON](http://www.odata.org/developers/protocols/json-format#RepresentingComplexTypeProperties) согласно стандартам OData.</span><span class="sxs-lookup"><span data-stu-id="ced2f-p112">Some methods in the client object model require a large payload as a parameter. For REST endpoints to maintain functionality parity with their corresponding client object model APIs, the endpoints must accept a complex type as a parameter. In these cases, the REST service extends the existing OData protocol to enable these REST endpoints to accept a single complex type as a parameter. This applies to  **POST** operations only, and you have to pass the complex type in [Atom](http://www.odata.org/developers/protocols/atom-format#RepresentingComplexTypesProperties) format or [JSON](http://www.odata.org/developers/protocols/json-format#RepresentingComplexTypeProperties) format, according to OData standards.</span></span>
 

 
<span data-ttu-id="ced2f-p113">Например, метод **ListCollection.Add** принимает в качестве параметра объект **Microsoft.SharePoint.Client.ListCreationInformation**. Чтобы добавить список на указанный сайт, создайте соответствующую конечную точку REST следующим образом:</span><span class="sxs-lookup"><span data-stu-id="ced2f-p113">For example, the  **ListCollection.Add** method takes a **Microsoft.SharePoint.Client.ListCreationInformation** object as a parameter. To add a list to a specified site, construct the appropriate REST endpoint as follows:</span></span>
 

 
 `http://server/site/_api/web/lists/add`
 

 
<span data-ttu-id="ced2f-190">Затем передайте в тексте запроса сложный тип, отформатированный здесь с помощью JSON.</span><span class="sxs-lookup"><span data-stu-id="ced2f-190">Then, pass the complex type in the request body, formatted here using JSON.</span></span>
 

 



```
{ "d" : {
   "results": {
     "__metadata": {
       "type": "SP.ListCreationInformation"
     }, 
     "CustomSchemaXml": "…large payload…/", 
     "Description": "desc", 
     "DocumentTemplateType": "1", 
     "TemplateType": "101", 
     "Title": "Announcements"
   }
} 
}

```


### <a name="using-parameter-aliases-in-rest-service-calls"></a><span data-ttu-id="ced2f-191">Использование псевдонимов параметров в вызовах службы REST</span><span class="sxs-lookup"><span data-stu-id="ced2f-191">Using parameter aliases in REST service calls</span></span>

<span data-ttu-id="ced2f-p114">В OData можно передавать параметры в конечную точку SharePoint REST с помощью семантики псевдонимов параметров. При таком подходе значение параметра идентифицируется с псевдонимом в вызове параметра и в строке запроса URI указывается фактическое значение. Это позволяет поддерживать больше типов символов и единообразное форматирование, используя строку запроса.</span><span class="sxs-lookup"><span data-stu-id="ced2f-p114">You can use the "parameter aliasing" semantic in OData to pass parameters to a SharePoint REST endpoint. In parameter aliasing, the parameter value is identified with an alias in the parameter call, and the actual value is specified in the query string of the URI. This enables you to support more types of characters and consistent formatting by using the query string.</span></span>
 

 
<span data-ttu-id="ced2f-195">Например, два приведенных ниже URI REST эквивалентны.</span><span class="sxs-lookup"><span data-stu-id="ced2f-195">For example, the following two REST URIs are equivalent:</span></span> 
 

 
 <span data-ttu-id="ced2f-196">*Непосредственное указание значения параметра:*</span><span class="sxs-lookup"><span data-stu-id="ced2f-196">*Specify the parameter value directly:*</span></span> 
 

 
 `http://server/site/_api/web/applyWebTemplate("STS#0")`
 

 
 <span data-ttu-id="ced2f-197">*Использование псевдонима параметра и указание фактического значения параметра в строке запроса URI:*</span><span class="sxs-lookup"><span data-stu-id="ced2f-197">*Use a parameter alias, and specify the actual parameter value in the query string of the URI:*</span></span> 
 

 
 `http://server/site/_api/web/applyWebTemplate(title=@template)?@template="STS#0"`
 

 
<span data-ttu-id="ced2f-p115">Однако служба SharePoint REST не поддерживает передачу комплексных типов через псевдонимы параметров. Например, следующий URI, содержащий комплексный тип в качестве параметра, не поддерживается:</span><span class="sxs-lookup"><span data-stu-id="ced2f-p115">However, the SharePoint REST service does not support passing complex types via parameter aliasing. For example, the following URI, which contains a complex type in the parameter alias, is not supported:</span></span>
 

 
 `http://server/site/_api/userProfiles/People(7)/GetWorkplace(@address)?@address={"__metadata":{"type: "ODataDemo.Address"},"Street":"NE 228th", "City":"Sammamish","State":"WA","ZipCode":"98074","Country": "USA"}`
 

 

<span data-ttu-id="ced2f-200">**Синтаксис присвоения псевдонима параметру службы REST в SharePoint**</span><span class="sxs-lookup"><span data-stu-id="ced2f-200">**SharePoint REST service parameter aliasing syntax**</span></span>

 

 
![Синтаксис присвоения псевдонима параметру службы REST в SharePoint](../../images/SPF15Con_REST_parameterAliasSyntax.png)
 

 

 

### <a name="specifying-dictionaries-as-parameter-values"></a><span data-ttu-id="ced2f-202">Указание словарей в качестве значений параметров</span><span class="sxs-lookup"><span data-stu-id="ced2f-202">Specifying dictionaries as parameter values</span></span>

<span data-ttu-id="ced2f-203">Для конечных точек REST, которые соответствуют методам, принимающим в качестве параметров словари `Dictionary<String, String>`, словарь следует передавать в строке запроса в формате разделенных запятыми пар "имя-значение".</span><span class="sxs-lookup"><span data-stu-id="ced2f-203">For REST endpoints that correspond to methods that take  `Dictionary<String, String>` dictionaries as parameters, pass the dictionary as a series of comma delimited name-value pairs in the query string.</span></span>
 

 

<span data-ttu-id="ced2f-204">**Синтаксис службы REST для параметров словаря**</span><span class="sxs-lookup"><span data-stu-id="ced2f-204">**REST service syntax for Dictionary parameters**</span></span>

 

 
![Синтаксис службы REST для параметров словаря](../../images/SPF15Con_REST_parameterDictionarySyntax.png)
 
<span data-ttu-id="ced2f-206">Словарь `Dictionary<String, object>` представлен как многозначный объект с именем KeyedPropertyValue, содержащий следующие строковые свойства:</span><span class="sxs-lookup"><span data-stu-id="ced2f-206">A  `Dictionary<String, object>` is represented as a multi-value object, named KeyedPropertyValue, with the following string properties:</span></span>
 

 

 

-  <span data-ttu-id="ced2f-207">**Key**. Ключ многозначного объекта.</span><span class="sxs-lookup"><span data-stu-id="ced2f-207">**Key** The key of the multi-value object.</span></span>
    
 
-  <span data-ttu-id="ced2f-208">**Value**. Значение объекта.</span><span class="sxs-lookup"><span data-stu-id="ced2f-208">**Value** The value of the object</span></span>
    
 
-  <span data-ttu-id="ced2f-p116">**ValueType**. Тип значения объекта. Для простых типов, которые соответствуют существующим типам модели данных с использованием сущностей (EDM), служба REST возвращает соответствующую строку типа EDM, например "Edm.String". В противном случае служба REST возвращает тип значения, возвращенный функцией **Type.ToString**.</span><span class="sxs-lookup"><span data-stu-id="ced2f-p116">**ValueType** The value type of the object. For simple value types that map to existing Entity Data Model (EDM) types, the REST service returns the appropriate EDM type string; for example, "Edm.String." If not, the REST service returns the value type returned by the **Type.ToString** function.</span></span>
    
 

### <a name="specifying-parameter-values-in-the-query-string"></a><span data-ttu-id="ced2f-212">Указание значений параметров в строке запроса</span><span class="sxs-lookup"><span data-stu-id="ced2f-212">Specifying parameter values in the query string</span></span>

<span data-ttu-id="ced2f-p117">Если URI REST завершается вызовом метода, с помощью синтаксиса строки запроса можно указать значения параметров метода. Например:</span><span class="sxs-lookup"><span data-stu-id="ced2f-p117">If your REST URI terminates in a method call, you can use query string syntax to specify the parameter values of the method. For example:</span></span>
 

 
 `http://<server>/<site>/_api/web/applyWebTemplate?template="STS#0"`
 

 
<span data-ttu-id="ced2f-215">На приведенном ниже рисунке показан синтаксис службы REST для параметров в строке запроса.</span><span class="sxs-lookup"><span data-stu-id="ced2f-215">the figure below shows the REST service syntax for parameters in query string.</span></span>
 

 

<span data-ttu-id="ced2f-216">**Синтаксис службы REST для параметров в строке запроса**</span><span class="sxs-lookup"><span data-stu-id="ced2f-216">**REST service syntax for parameters in query string**</span></span>

 

 
![Синтаксис службы REST для параметров в строке запроса](../../images/SPF15Con_REST_parameterQuerySyntax.png)
 

 

 

## <a name="specifying-static-methods-and-properties-as-rest-service-uris"></a><span data-ttu-id="ced2f-218">Указание статических методов и свойств в качестве URI службы REST</span><span class="sxs-lookup"><span data-stu-id="ced2f-218">Specifying static methods and properties as REST service URIs</span></span>

<span data-ttu-id="ced2f-p118">Для создания URI, соответствующих статическим методам или свойствам, используйте имя соответствующего API из объектной модели ECMAScript, начиная с объявления пространства имен и использования точечной нотации. Например, [SP.Utilities.Utility.getImageUrl(imageName)](http://msdn.microsoft.com/en-us/library/ee658947.aspx) в клиентской объектной модели ECMAScript имеет следующий аналог в службе REST:</span><span class="sxs-lookup"><span data-stu-id="ced2f-p118">To construct URIs that correspond to static methods or properties, use the corresponding API name from the ECMAScript object model, starting with the namespace declaration and using dot notation. For example,  [SP.Utilities.Utility.getImageUrl(imageName)](http://msdn.microsoft.com/en-us/library/ee658947.aspx) in the ECMAScript client object model would have the following REST equivalent:</span></span>
 

 
 `http://server/site/_api/SP.Utilities.Utility.getImageUrl('imageName')`
 

 
<span data-ttu-id="ced2f-p119">Однако к статическим свойствам возможен только прямой доступ, и их не разрешается указывать в составе более длинных URI. Например, прямой доступ к методу **SP.Utility.AssetsLibrary** в REST можно получить следующим образом:</span><span class="sxs-lookup"><span data-stu-id="ced2f-p119">However, static properties can be accessed only directly, and are not allowed as part of a larger URI composition. For example, directly accessing the  **SP.Utility.AssetsLibrary** method in REST is allowable, as follows:</span></span>
 

 
 `http://server/site/_api/SP.Utility.assetsLibrary/id`
 

 
<span data-ttu-id="ced2f-223">При этом не допускается использовать расположение ресурса в качестве параметра для более сложного URI, как показано в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="ced2f-223">However, using that resource location as a parameter for a more complex URI, as shown in the following example, is not allowed:</span></span>
 

 
 `http://server/site/_api/getList(~SP.Utility/assetsLibrary/id)`
 

 
<span data-ttu-id="ced2f-224">На приведенном ниже рисунке показан синтаксис статического элемента для службы REST в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="ced2f-224">The figure below shows the SharePoint REST service static member syntax.</span></span>
 

 

<span data-ttu-id="ced2f-225">**Синтаксис статического элемента для службы REST в SharePoint**</span><span class="sxs-lookup"><span data-stu-id="ced2f-225">**SharePoint REST service static member syntax**</span></span>

 

 
![Синтаксис службы REST для параметров в строке запроса](../../images/SPF15Con_REST_parameterQuerySyntax.png)
 

 

 

## <a name="next-steps"></a><span data-ttu-id="ced2f-227">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ced2f-227">Next steps</span></span>

<span data-ttu-id="ced2f-228">Служба SharePoint REST поддерживает широкий набор операторов строки запроса OData, позволяющих выбирать, фильтровать и упорядочивать данные, запрошенные у конечной точки.</span><span class="sxs-lookup"><span data-stu-id="ced2f-228">If you want to select, filter, or order the data you requested from an endpoint, the SharePoint REST service supports a wide range of OData query string operators.</span></span> 
 

 

## <a name="additional-resources"></a><span data-ttu-id="ced2f-229">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="ced2f-229">Additional resources</span></span>
<span data-ttu-id="ced2f-230"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="ced2f-230"></span></span>


-  [<span data-ttu-id="ced2f-231">Знакомство со службой REST в SharePoint</span><span class="sxs-lookup"><span data-stu-id="ced2f-231">Get to know the SharePoint REST service</span></span>](get-to-know-the-sharepoint-2013-rest-service)
    
 
-  [<span data-ttu-id="ced2f-232">Выполнение базовых операций с использованием конечных точек SharePoint REST</span><span class="sxs-lookup"><span data-stu-id="ced2f-232">Complete basic operations using SharePoint REST endpoints</span></span>](complete-basic-operations-using-sharepoint-2013-rest-endpoints)
    
 
-  [<span data-ttu-id="ced2f-233">Работа со списками и элементами списков в интерфейсе REST</span><span class="sxs-lookup"><span data-stu-id="ced2f-233">Working with lists and list items with REST</span></span>](working-with-lists-and-list-items-with-rest)
    
 
-  [<span data-ttu-id="ced2f-234">Работа с папками и файлами в службе REST</span><span class="sxs-lookup"><span data-stu-id="ced2f-234">Working with folders and files with REST</span></span>](working-with-folders-and-files-with-rest)
    
 
-  [<span data-ttu-id="ced2f-235">Навигация по структуре данных SharePoint, представленной в службе REST</span><span class="sxs-lookup"><span data-stu-id="ced2f-235">Navigate the SharePoint data structure represented in the REST service</span></span>](navigate-the-sharepoint-data-structure-represented-in-the-rest-service)
    
 
-  [<span data-ttu-id="ced2f-236">Использование операций запросов OData в запросах REST SharePoint</span><span class="sxs-lookup"><span data-stu-id="ced2f-236">Use OData query operations in SharePoint REST requests</span></span>](use-odata-query-operations-in-sharepoint-rest-requests)
    
 
-  [<span data-ttu-id="ced2f-237">Справочные материалы и примеры по REST API</span><span class="sxs-lookup"><span data-stu-id="ced2f-237">REST API reference and samples</span></span>](http://msdn.microsoft.com/library/rest-api-reference-and-samples%28Office.15%29.aspx)
    
 
-  [<span data-ttu-id="ced2f-238">Синхронизация элементов SharePoint с помощью службы REST</span><span class="sxs-lookup"><span data-stu-id="ced2f-238">Synchronize SharePoint items using the REST service</span></span>](synchronize-sharepoint-items-using-the-rest-service)
    
 
-  [<span data-ttu-id="ced2f-239">Получение версий элементов списков и документов с помощью значений ETag в службе REST</span><span class="sxs-lookup"><span data-stu-id="ced2f-239">Use ETag values through the REST service to get document list item versioning</span></span>](http://msdn.microsoft.com/library/5f7e0579-46b7-44ab-b3b4-cdbc622dcd98%28Office.15%29.aspx)
    
 

 

 

