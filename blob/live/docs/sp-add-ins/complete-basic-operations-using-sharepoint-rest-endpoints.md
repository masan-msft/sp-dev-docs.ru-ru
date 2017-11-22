---
title: "Выполнение базовых операций с использованием конечных точек REST SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 8123b3bfa78cd43f337633618c3ed0453c396702
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="complete-basic-operations-using-sharepoint-rest-endpoints"></a><span data-ttu-id="f10f1-102">Выполнение базовых операций с использованием конечных точек REST SharePoint</span><span class="sxs-lookup"><span data-stu-id="f10f1-102">Complete basic operations using SharePoint REST endpoints</span></span>
<span data-ttu-id="f10f1-103">Узнайте, как выполнять операции CRUD (создание, чтение, обновление, удаление) с помощью интерфейса REST SharePoint.</span><span class="sxs-lookup"><span data-stu-id="f10f1-103">Learn how to perform basic create, read, update, and delete (CRUD) operations with the SharePoint REST interface.</span></span>
 

 <span data-ttu-id="f10f1-p101">**Примечание.** В настоящее время идет процесс замены названия "приложения для SharePoint" названием "надстройки SharePoint". Во время этого процесса в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio может по-прежнему использоваться термин "приложения для SharePoint". Дополнительные сведения см. в статье [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="f10f1-p101">**Note**  The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see  [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span></span>
 


## <a name="developing-with-the-sharepoint-client-apis-and-rest"></a><span data-ttu-id="f10f1-107">Разработка с помощью клиентских интерфейсов API и REST для SharePoint</span><span class="sxs-lookup"><span data-stu-id="f10f1-107">Developing with the SharePoint client APIs and REST</span></span>
<span data-ttu-id="f10f1-108"><a name="ClientAPIs"> </a></span><span class="sxs-lookup"><span data-stu-id="f10f1-108"><a name="ClientAPIs"> </a></span></span>

<span data-ttu-id="f10f1-p102">Вы можете выполнять базовые операции создания, чтения, обновления и удаления (CRUD) с помощью интерфейса Representational State Transfer (REST), предоставленного SharePoint. REST позволяет использовать все объекты и операции SharePoint, которые доступны в других клиентских интерфейсах API для SharePoint. Одно из преимуществ REST заключается в том, что вам не придется добавлять ссылки на библиотеки или клиентские сборки SharePoint. Вместо этого вы отправляете HTTP-запросы в соответствующие конечные точки для получения или обновления объектов SharePoint, например веб-сайтов, списков и элементов списков. Подробный обзор интерфейса REST SharePoint и его архитектуры см. в статье  [Знакомство со службой REST для SharePoint](get-to-know-the-sharepoint-rest-service.md).</span><span class="sxs-lookup"><span data-stu-id="f10f1-p102">You can perform basic create, read, update, and delete (CRUD) operations by using the Representational State Transfer (REST) interface provided by SharePoint. The REST interface exposes all of the SharePoint entities and operations that are available in the other SharePoint client APIs. One advantage of using REST is that you don't have to add references to any SharePoint libraries or client assemblies. Instead, you make HTTP requests to the appropriate endpoints to retrieve or update SharePoint entities, such as webs, lists, and list items. See  [Get to know the SharePoint REST service](get-to-know-the-sharepoint-rest-service.md) for a thorough introduction to the SharePoint REST interface and its architecture.</span></span>
 

 
 <span data-ttu-id="f10f1-p103">Больше о работе с базовыми сущностями можно узнать в статьях SharePoint [Работа со списками и элементами списков в службе REST](working-with-lists-and-list-items-with-rest.md) и [Работа с папками и файлами в службе REST](working-with-folders-and-files-with-rest.md). С примерами выполнения многих из этих операций в контексте веб-приложения ASP.NET, написанного на C#, можно ознакомиться в репозитории  [SharePoint-Add-in-REST-OData-BasicDataOperations](https://github.com/OfficeDev/SharePoint-Add-in-REST-OData-BasicDataOperations.md).</span><span class="sxs-lookup"><span data-stu-id="f10f1-p103">[Working with lists and list items with REST](working-with-lists-and-list-items-with-rest.md) and [Working with folders and files with REST](working-with-folders-and-files-with-rest.md) explain in greater detail how to work with core SharePoint entities. See [SharePoint-Add-in-REST-OData-BasicDataOperations](https://github.com/OfficeDev/SharePoint-Add-in-REST-OData-BasicDataOperations.md) for a sample that shows you how to do many of these operations in the context of an ASP.NET web application written in C#.</span></span>
 

 
<span data-ttu-id="f10f1-p104">Более подробные сведения о наборах API, доступных на платформе SharePoint, см. в статье  [Выбор правильного набора API в SharePoint](http://msdn.microsoft.com/library/f36645da-77c5-47f1-a2ca-13d4b62b320d%28Office.15%29.aspx). Дополнительные сведения об использовании других клиентских интерфейсов API см. в статьях  [Выполнение базовых операций с использованием кода библиотеки JavaScript в SharePoint](complete-basic-operations-using-javascript-library-code-in-sharepoint.md),  [Выполнение базовых операций с использованием кода библиотеки JavaScript в SharePoint](complete-basic-operations-using-javascript-library-code-in-sharepoint.md) и [Построение приложений Windows Phone, обращающихся к SharePoint](http://msdn.microsoft.com/library/36681335-f772-4499-8445-f94481bc18e7%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="f10f1-p104">For more details about the sets of APIs available on the SharePoint platform, see  [Choose the right API set in SharePoint](http://msdn.microsoft.com/library/f36645da-77c5-47f1-a2ca-13d4b62b320d%28Office.15%29.aspx). For information about how to use the other client APIs, see  [Complete basic operations using JavaScript library code in SharePoint](complete-basic-operations-using-javascript-library-code-in-sharepoint.md),  [Complete basic operations using JavaScript library code in SharePoint](complete-basic-operations-using-javascript-library-code-in-sharepoint.md), and  [Build Windows Phone apps that access SharePoint](http://msdn.microsoft.com/library/36681335-f772-4499-8445-f94481bc18e7%28Office.15%29.aspx).</span></span>
 

 

## <a name="http-operations-in-sharepoint-rest-services"></a><span data-ttu-id="f10f1-118">Операции HTTP в службах REST SharePoint</span><span class="sxs-lookup"><span data-stu-id="f10f1-118">HTTP operations in SharePoint REST services</span></span>
<span data-ttu-id="f10f1-119"><a name="HTTPOps"> </a></span><span class="sxs-lookup"><span data-stu-id="f10f1-119"><a name="HTTPOps"> </a></span></span>

<span data-ttu-id="f10f1-p105">Конечные точки в службе REST SharePoint соответствуют типам и элементам из клиентских объектных моделей SharePoint. С помощью HTTP-запросов можно использовать конечные точки REST для выполнения типичных операций CRUD (**Create**, **Read**, **Update** и **Delete**) с сущностями SharePoint, такими как списки и сайты.</span><span class="sxs-lookup"><span data-stu-id="f10f1-p105">The endpoints in the SharePoint REST service correspond to the types and members in the SharePoint client object models. By using HTTP requests, you can use these REST endpoints to perform typical CRUD ( **Create**,  **Read**,  **Update**, and  **Delete**) operations against SharePoint entities, such as lists and sites.</span></span> 
 

 
<span data-ttu-id="f10f1-p106">Как правило, конечные точки, представляющие операции **Read**, сопоставляются с HTTP-командами **GET**. Конечные точки, представляющие операции обновления, сопоставляются с HTTP-командами **POST**, а конечные точки, представляющие операции обновления или вставки, — с HTTP-командами **PUT**.</span><span class="sxs-lookup"><span data-stu-id="f10f1-p106">Typically, endpoints that represent  **Read** operations map to HTTP **GET** commands. Endpoints that represent update operations map to HTTP **POST** commands, and endpoints that represent update or insert operations map to HTTP **PUT** commands.</span></span>
 

 
<span data-ttu-id="f10f1-p107">В SharePoint для создания таких сущностей, как списки и сайты, используется команда **POST**. Служба REST SharePoint поддерживает отправку команд **POST**, содержащих определения объектов для конечных точек, представляющих коллекции. Например, вы можете отправить команду **POST**, включающую определение нового объекта списка в формате ATOM, на следующий URL-адрес, чтобы создать список SharePoint:</span><span class="sxs-lookup"><span data-stu-id="f10f1-p107">In SharePoint, use  **POST** to create entities such as lists and sites. The SharePoint REST service supports sending **POST** commands that include object definitions to endpoints that represent collections. For example, you could send a **POST** command that included a new list object definition in ATOM to the following URL, to create a SharePoint list:</span></span>
 

 
 `http://<site url>/_api/web/lists`
 

 
<span data-ttu-id="f10f1-p108">В операциях **POST** для всех необязательных свойств заданы значения по умолчанию. При попытке задать в операции **POST** свойство, доступное только для чтения, служба возвращает исключение.</span><span class="sxs-lookup"><span data-stu-id="f10f1-p108">For  **POST** operations, any properties that are not required are set to their default values. If you attempt to set a read-only property as part of a **POST** operation, the service returns an exception.</span></span>
 

 
<span data-ttu-id="f10f1-p109">Для обновления существующих объектов SharePoint используйте операции **PUT** и **MERGE**. Все конечные точки службы, представляющие операцию **set** для свойства объекта, поддерживают как запросы **PUT**, так и запросы **MERGE**. Для запросов **MERGE** необязательно задавать свойства. Все свойства, не заданные явно, сохраняют текущие значения. Однако в командах **PUT** для всех свойств, не заданных явно, задаются значения по умолчанию. Кроме того, если указать не все обязательные свойства в операции обновления объекта при использовании HTTP-команд **PUT**, служба REST вернет исключение.</span><span class="sxs-lookup"><span data-stu-id="f10f1-p109">Use  **PUT** and **MERGE** operations to update existing SharePoint objects. Any service endpoint that represents an object property **set** operation supports both **PUT** requests and **MERGE** requests. For **MERGE** requests, setting properties is optional; any properties that you do not explicitly set retain their current property. For **PUT** commands, however, any properties you do not explicitly set are set to their default properties. In addition, if you do not specify all required properties in object updates when using HTTP **PUT** commands, the REST service returns an exception.</span></span>
 

 
<span data-ttu-id="f10f1-p110">Используйте команду HTTP **DELETE** для URL-адреса определенной конечной точки, чтобы удалить объект SharePoint, представленный этой конечной точкой. Для повторно обрабатываемых объектов (например, списков, файлов и элементов списков) это приведет к выполнению операции **Recycle**.</span><span class="sxs-lookup"><span data-stu-id="f10f1-p110">Use the HTTP  **DELETE** command against the specific endpoint URL to delete the SharePoint object represented by that endpoint. In the case of recyclable objects, such as lists, files, and list items, this results in a **Recycle** operation.</span></span>
 

 

## <a name="reading-data-with-the-sharepoint-rest-interface"></a><span data-ttu-id="f10f1-136">Считывание данных с помощью интерфейса REST SharePoint</span><span class="sxs-lookup"><span data-stu-id="f10f1-136">Reading data with the SharePoint REST interface</span></span>
<span data-ttu-id="f10f1-137"><a name="ReadingData"> </a></span><span class="sxs-lookup"><span data-stu-id="f10f1-137"><a name="ReadingData"> </a></span></span>

<span data-ttu-id="f10f1-p111">Для использования возможностей REST, которые встроены в SharePoint, вы создаете HTTP-запрос с поддержкой REST, используя стандарт OData, что соответствует клиентской объектной модели API, которую вы хотите использовать. Каждый объект SharePoint предоставляется в конечной точке на странице SharePoint, на которую вы ориентируетесь, а метаданные представлены в формате XML или JSON. Вы можете создавать HTTP-запросы на любом языке, в том числе на JavaScript, C# и многих других.</span><span class="sxs-lookup"><span data-stu-id="f10f1-p111">To use the REST capabilities that are built into SharePoint, you construct a RESTful HTTP request, using the OData standard, which corresponds to the client object model API you want to use. Each SharePoint entity is exposed at an endpoint on the SharePoint site that you are targeting, and its metadata is represented in either XML or JSON format. You can make the HTTP requests in any language, including but not limited to JavaScript and C#.</span></span>
 

 
<span data-ttu-id="f10f1-p112">Чтобы прочитать данные из конечной точки REST, необходимо знать URL-адрес конечной точки и представление OData сущности SharePoint, которая предоставляется в этой конечной точке. Например, чтобы получить все списки на определенном сайте SharePoint, нужно создать запрос **GET** для `http://<site url>/_api/web/lists`. Вы можете перейти к этому URL-адресу в браузере и посмотреть на полученный код XML. Создавая запрос в коде, вы можете указать, в каком формате вы будете получать списки OData: XML или JSON.</span><span class="sxs-lookup"><span data-stu-id="f10f1-p112">To read information from a REST endpoint, you must know both the URL of the endpoint and the OData representation of the SharePoint entity that is exposed at that endpoint. For example, to retrieve all of the lists in a specific SharePoint site, you would make a  **GET** request to `http://<site url>/_api/web/lists`. You can navigate to this URL in your browser and see the XML that gets returned. When you make the request in code, you can specify whether to receive the OData representation of the lists in XML or JSON.</span></span>
 

 
<span data-ttu-id="f10f1-p113">Приведенный ниже код на C# иллюстрирует создание запроса **GET**, который возвращает представление JSON для всех списков на сайте с помощью JQuery. Предполагается, что у вас есть действительный маркер доступа OAuth, хранящийся в переменной **accessToken**. Маркер доступа не нужен, если вы выполняете вызов с сайта надстройки, как в надстройке, размещенной в SharePoint. Обратите внимание, что невозможно получить маркер доступа из кода, который выполняется в браузерном клиенте. Маркер доступа необходимо получить из кода, выполняемого на сервере. В статьях [Поток маркеров контекста OAuth для надстроек в SharePoint](context-token-oauth-flow-for-sharepoint-add-ins.md) и [Поток кода аутентификации OAuth для надстроек в SharePoint](authorization-code-oauth-flow-for-sharepoint-add-ins.md) рассказывается, как получить маркер доступа.</span><span class="sxs-lookup"><span data-stu-id="f10f1-p113">The following C# code demonstrates how to make this  **GET** request that returns a JSON representation of all of a site's lists by using JQuery. It also assumes that you have a valid OAuth access token that is stored in the **accessToken** variable. You do not need the access token if you make this call from inside an add-in web, as you would in a SharePoint-hosted add-in. Note that you cannot obtain an access token from code that is running on a browser client. You must obtain the access token from code that is running on a server. [Context Token OAuth flow for SharePoint Add-ins](context-token-oauth-flow-for-sharepoint-add-ins.md) and [Authorization Code OAuth flow for SharePoint Add-ins](authorization-code-oauth-flow-for-sharepoint-add-ins.md) explain how you can obtain an access token.</span></span>
 

 



```C#

HttpWebRequest endpointRequest =
  (HttpWebRequest)HttpWebRequest.Create(
  "http://<site url>/_api/web/lists");
endpointRequest.Method = "GET";
endpointRequest.Accept = "application/json;odata=verbose";
endpointRequest.Headers.Add("Authorization", 
  "Bearer " + accessToken);
HttpWebResponse endpointResponse =
  (HttpWebResponse)endpointRequest.GetResponse();

```

<span data-ttu-id="f10f1-p114">Этот запрос будет выглядеть немного по-другому, если вы создаете надстройку на JavaScript, но с использованием междоменной библиотеки SharePoint. В этом случае предоставлять маркер доступа не нужно. Ниже показано, как выглядел бы запрос, если бы вы использовали междоменную библиотеку и хотели получить представление списков OData в формате XML, а не JSON. Так как по умолчанию отклик представлен в формате Atom, добавлять заголовок **Accept** необязательно. Дополнительные сведения об использовании междоменной библиотеки см. в статье [Обращение к данным SharePoint из надстроек с помощью междоменной библиотеки](access-sharepoint-data-from-add-ins-using-the-cross-domain-library.md).</span><span class="sxs-lookup"><span data-stu-id="f10f1-p114">This request would look a little different if you are writing your add-in in JavaScript but using the SharePoint cross-domain library. In this case, you don't need to provide an access token. The following code demonstrates how this request would look if you are using the cross-domain library and want to receive the OData representation of the lists as XML instead of JSON. (Because Atom is the default response format, you don't have to include an  **Accept** header.) See [Access SharePoint data from add-ins using the cross-domain library](access-sharepoint-data-from-add-ins-using-the-cross-domain-library.md) for more information about using the cross-domain library.</span></span>
 

 



```
var executor = new SP.RequestExecutor(appweburl);
executor.executeAsync(
    {
        url:
            appweburl +
            "/_api/SP.AppContextSite(@target)/web/lists?@target='" +
            hostweburl + "'",
        method: "GET",
        success: successHandler,
        error: errorHandler
    }
);
```

<span data-ttu-id="f10f1-p115">В следующем примере показано, как запросить представление JSON всех списков сайта, используя C#. Предполагается, что у вас есть маркер доступа OAuth, который вы храните в переменной  `accessToken`.</span><span class="sxs-lookup"><span data-stu-id="f10f1-p115">The code in the following example shows you how to request a JSON representation of all of the lists in a site by using C#. It assumes that you have an OAuth access token that you are storing in the  `accessToken` variable.</span></span>
 

 



```C#
HttpWebRequest endpointRequest = (HttpWebRequest)HttpWebRequest.Create(sharepointUrl.ToString() + "/_api/web/lists");
endpointRequest.Method = "GET";
endpointRequest.Accept = "application/json;odata=verbose";
endpointRequest.Headers.Add("Authorization", "Bearer " + accessToken);
HttpWebResponse endpointResponse = (HttpWebResponse)endpointRequest.GetResponse();

```


### <a name="getting-properties-that-arent-returned-with-the-resource"></a><span data-ttu-id="f10f1-157">Получение свойств, не возвращаемых с ресурсом</span><span class="sxs-lookup"><span data-stu-id="f10f1-157">Getting properties that aren't returned with the resource</span></span>
<span data-ttu-id="f10f1-158"><a name="NavigationProperties"> </a></span><span class="sxs-lookup"><span data-stu-id="f10f1-158"><a name="NavigationProperties"> </a></span></span>

<span data-ttu-id="f10f1-p116">Многие значения свойств возвращаются при получении ресурса, но для некоторых свойств необходимо отправить запрос **GET** непосредственно конечной точке свойства. Это типично для свойств, представляющих сущности SharePoint.</span><span class="sxs-lookup"><span data-stu-id="f10f1-p116">Many property values are returned when you retrieve a resource, but for some properties, you have to send a  **GET** request directly to the property endpoint. This is typical of properties that represent SharePoint entities.</span></span>
 

 
<span data-ttu-id="f10f1-p117">В приведенном ниже примере показано, как получить свойство, добавив его имя в конечную точку ресурса. В примере значение свойства **Author** получается от ресурса **File**.</span><span class="sxs-lookup"><span data-stu-id="f10f1-p117">The following example shows how to get a property by appending the property name to the resource endpoint. The example gets the value of the  **Author** property from a **File** resource.</span></span>
 

 
 <span data-ttu-id="f10f1-163">http:// _<site url>_/_api/web/getfilebyserverrelativeurl('/ _<folder name>_/ _<file name>_')/author</span><span class="sxs-lookup"><span data-stu-id="f10f1-163">http:// _<site url>_/_api/web/getfilebyserverrelativeurl('/ _<folder name>_/ _<file name>_')/author</span></span>
 

 
<span data-ttu-id="f10f1-164">Чтобы получить результаты в формате JSON, включите в запрос заголовок **Accept** со значением `"application/json;odata=verbose"`.</span><span class="sxs-lookup"><span data-stu-id="f10f1-164">To get the results in JSON format, include an  **Accept** header set to `"application/json;odata=verbose"`.</span></span>
 

 

## <a name="writing-data-by-using-the-rest-interface"></a><span data-ttu-id="f10f1-165">Запись данных с помощью интерфейса REST</span><span class="sxs-lookup"><span data-stu-id="f10f1-165">Writing data by using the REST interface</span></span>
<span data-ttu-id="f10f1-166"><a name="WritingData"> </a></span><span class="sxs-lookup"><span data-stu-id="f10f1-166"><a name="WritingData"> </a></span></span>

<span data-ttu-id="f10f1-p118">Вы можете создавать и обновлять сущности SharePoint, создавая HTTP-запросы с поддержкой RESTful для соответствующих конечных точек, как и при чтении данных. Одно из ключевых отличий заключается в использовании запроса **POST**. При обновлении сущностей вы также передаете метод **PUT** или **MERGE** HTTP-запроса, добавляя один из этих терминов в заголовки запроса в качестве значения ключа **X-HTTP-Method**. Метод **MERGE** обновляет только указанные свойства сущности, в то время как метод **PUT** заменяет существующую сущность на новую, которая указана в тексте запроса **POST**. Для удаления объекта используйте метод **DELETE**. При создании или обновлении сущности необходимо указать ее представление OData в тексте HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="f10f1-p118">You can create and update SharePoint entities by constructing RESTful HTTP requests to the appropriate endpoints, just as you do when you're reading data. One key difference, however, is that you use a  **POST** request. When you're updating entities, you also pass a **PUT** or **MERGE** HTTP request method by adding one of those terms to the headers of your request as the value of the **X-HTTP-Method** key. The **MERGE** method updates only the properties of the entity that you specify, while the **PUT** method replaces the existing entity with a new one that you supply in the body of the **POST**. Use the  **DELETE** method to delete the entity. When you create or update an entity, you must provide an OData representation of the entity that you want to create or change in the body of your HTTP request.</span></span>
 

 
<span data-ttu-id="f10f1-p119">Еще одна важная особенность создания, обновления и удаления сущностей SharePoint заключается в том, что если вы не используете OAuth для авторизации своих запросов, то для выполнения этих операций потребуется передавать значение дайджеста формы запроса с сервера в качестве значения заголовка **X-RequestDigest**. Чтобы получить это значение, выполните запрос **POST** с пустым текстом к конечной точке `http://<site url>/_api/contextinfo` и извлеките значение узла `d:FormDigestValue` в XML-коде, возвращаемом конечной точкой **contextinfo**. В приведенном ниже примере показан HTTP-запрос к конечной точке **contextinfo**, написанный на C#.</span><span class="sxs-lookup"><span data-stu-id="f10f1-p119">Another important consideration when creating, updating, and deleting SharePoint entities is that if you aren't using OAuth to authorize your requests, these operations require the server's request form digest value as the value of the  **X-RequestDigest** header. You can retrieve this value by making a **POST** request with an empty body to `http://<site url>/_api/contextinfo` and extracting the value of the `d:FormDigestValue` node in the XML that the **contextinfo** endpoint returns. The following example shows an HTTP request to the **contextinfo** endpoint in C#.</span></span>
 

 



```C#

HttpWebRequest endpointRequest =
  (HttpWebRequest)HttpWebRequest.Create(
  "http://<site url>/_api/contextinfo");
endpointRequest.Method = "POST";
endpointRequest.Accept = "application/json;odata=verbose";
HttpWebResponse endpointResponse =
  (HttpWebResponse)endpointRequest.GetResponse();

```

<span data-ttu-id="f10f1-176">Если вы используете поток аутентификации и авторизации, описанный в статье  [Авторизация и проверка подлинности для надстроек в SharePoint](authorization-and-authentication-of-sharepoint-add-ins.md), нет необходимости включать в свои запросы дайджест запроса.</span><span class="sxs-lookup"><span data-stu-id="f10f1-176">If you're using the authentication and authorization flow described in  [Authorization and authentication of SharePoint Add-ins](authorization-and-authentication-of-sharepoint-add-ins.md), you don't need to include the request digest in your requests.</span></span>
 

 
<span data-ttu-id="f10f1-177">Если вы используете междоменную библиотеку JavaScript, объект SP.RequestExecutor обрабатывает получение и отправку значения дайджеста формы.</span><span class="sxs-lookup"><span data-stu-id="f10f1-177">If you're using the JavaScript cross-domain library, SP.RequestExecutor handles getting and sending the form digest value for you.</span></span>
 

 
<span data-ttu-id="f10f1-p120">Если вы создаете Надстройка SharePoint, размещенное в SharePoint, то вам не придется выполнять отдельный HTTP-запрос для получения обработанного значения. Вместо этого вы можете получить значение в коде JavaScript со страницы SharePoint (если страница использует эталонную страницу по умолчанию), как показано в следующем примере, в котором используется JQuery и создается список.</span><span class="sxs-lookup"><span data-stu-id="f10f1-p120">If you're creating a SharePoint-hosted SharePoint Add-in, you don't have to make a separate HTTP request to retrieve the form digest value. Instead, you can retrieve the value in JavaScript code from the SharePoint a page (if the page uses the default master page), as shown in the following example, which uses JQuery and creates a list.</span></span>
 

 



```
jQuery.ajax({
        url: "http://<site url>/_api/web/lists",
        type: "POST",
        data:  JSON.stringify({ '__metadata': { 'type': 'SP.List' }, 'AllowContentTypes': true,
 'BaseTemplate': 100, 'ContentTypesEnabled': true, 'Description': 'My list description', 'Title': 'Test' }
),
        headers: { 
            "accept": "application/json;odata=verbose",
            "content-type": "application/json;odata=verbose",
            "content-length": <length of post body>,
            "X-RequestDigest": $("#__REQUESTDIGEST").val()
        },
        success: doSuccess,
        error: doError
});


```

<span data-ttu-id="f10f1-p121">В следующем примере показано, как обновить список, созданный в предыдущем примере. В примере меняется название списка, используется JQuery и предполагается, что вы выполняете эту операцию в надстройке, размещенной в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="f10f1-p121">The following example shows how to update the list that is created in the previous example. The example changes the title of the list, uses JQuery, and assumes that you are doing this operation in a SharePoint-hosted add-in.</span></span>
 

 



```
jQuery.ajax({
        url: "http://<site url>/_api/web/lists/GetByTitle('Test')",
        type: "POST",
        data: JSON.stringify({ '__metadata': { 'type': 'SP.List' }, 'Title': 'New title' }),
        headers: { 
            "X-HTTP-Method":"MERGE",
            "accept": "application/json;odata=verbose",
            "content-type": "application/json;odata=verbose",
            "content-length": <length of post body>,
            "X-RequestDigest": $("#__REQUESTDIGEST").val(),
            "IF-MATCH": "*"
        },
        success: doSuccess,
        error: doError
});

```

<span data-ttu-id="f10f1-p122">В ключе **IF-MATCH** в заголовках запроса указывается значение **etag** для списка или его элемента. Это значение применяется только для списков и их элементов и помогает избежать проблем с одновременной обработкой при обновлении этих сущностей. В предыдущем примере вместо этого значения используется звездочка (*). Вы можете использовать это значение, если у вас нет причин беспокоиться о проблемах с одновременной обработкой. В противном случае необходимо получить значение **etag** либо список или его элемент, выполнив запрос **GET**, который извлекает сущность. Заголовки полученного HTTP-запроса передают etag в качестве значения ключа **ETag**. Это значение также включено в метаданные сущности. В приведенном ниже примере показан открывающий тег `<entry>` для узла XML, который содержит данные списка. Свойство **m:etag** содержит значение **etag**.</span><span class="sxs-lookup"><span data-stu-id="f10f1-p122">The value of the  **IF-MATCH** key in the request headers is where you specify the **etag** value of a list or list item. This particular value applies only to lists and list items, and it is intended to help you avoid concurrency problems when you update those entities. The previous example uses an asterisk (*) for this value, and you can use that value whenever you don't have any reason to worry about concurrency issues. Otherwise, you should obtain the **etag** value or a list or list item by performing a **GET** request that retrieves the entity. The response headers of the resulting HTTP response will pass the etag as the value of the **ETag** key. This value is also included in the entity metadata. The following example shows the opening `<entry>` tag for the XML node that contains the list information. The **m:etag** property contains the **etag** value.</span></span>
 

 



```XML
<entry xml:base="http://site url/_api/" xmlns=http://www.w3.org/2005/Atom 
xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" 
xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata"
xmlns:georss="http://www.georss.org/georss" xmlns:gml="http://www.opengis.net/gml" m:etag=""1"">
```


## <a name="creating-a-site-with-rest"></a><span data-ttu-id="f10f1-190">Создание сайта с помощью REST</span><span class="sxs-lookup"><span data-stu-id="f10f1-190">Creating a site with REST</span></span>
<span data-ttu-id="f10f1-191"><a name="bk_CreateSite"> </a></span><span class="sxs-lookup"><span data-stu-id="f10f1-191"><a name="bk_CreateSite"> </a></span></span>

<span data-ttu-id="f10f1-192">В приведенном ниже примере показано, как создать сайт на JavaScript.</span><span class="sxs-lookup"><span data-stu-id="f10f1-192">The following example shows how to create a site in JavaScript.</span></span>
 

 

```
jQuery.ajax({
    url: "http://<site url>/_api/web/webinfos/add",
    type: "POST",
    data: JSON.stringify(
        {'parameters': {
            '__metadata':  {'type': 'SP.WebInfoCreationInformation' },
            'Url': 'RestSubWeb',
            'Title': 'RestSubWeb',
            'Description': 'REST created web',
            'Language':1033,
            'WebTemplate':'sts',
            'UseUniquePermissions':false}
        }
    ),
    headers: { 
        "accept": "application/json; odata=verbose", 
        "content-type":"application/json;odata=verbose",
        "content-length": <length of post body>,
        "X-RequestDigest": $("#__REQUESTDIGEST").val() 
    },
    success: doSuccess,
    error: doError
});
```


## <a name="how-rest-requests-differ-by-environment"></a><span data-ttu-id="f10f1-193">Отличия между запросами REST в разных средах</span><span class="sxs-lookup"><span data-stu-id="f10f1-193">How REST requests differ by environment</span></span>
<span data-ttu-id="f10f1-194"><a name="bk_HowRequestsDiffer"> </a></span><span class="sxs-lookup"><span data-stu-id="f10f1-194"><a name="bk_HowRequestsDiffer"> </a></span></span>

<span data-ttu-id="f10f1-p123">Методы составления и отправки HTTP-запросов могут различаться в зависимости от языка, библиотеки и типа надстройки, поэтому при переводе запроса из одной среды в другую часто требуется менять один или несколько его компонентов. Например, в запросах jQuery AJAX текст и тип запроса указываются с помощью параметров **data** и **type**, а в запросах к междоменной библиотеке — с помощью параметров **body** и **method**.</span><span class="sxs-lookup"><span data-stu-id="f10f1-p123">Building and sending an HTTP request may vary according to language, library, and add-in type, so you often need to change one or more request components when you're translating a request from one environment to another. For example, jQuery AJAX requests use  **data** and **type** parameters to specify the request body and type, but cross-domain library requests use **body** and **method** parameters to specify those values.</span></span>
 

 
<span data-ttu-id="f10f1-197">В следующих разделах описываются другие распространенные отличия между средами.</span><span class="sxs-lookup"><span data-stu-id="f10f1-197">The following sections describe other common differences across environments.</span></span>
 

 

### <a name="the-way-you-get-and-send-the-form-digest-value-depends-on-the-add-in"></a><span data-ttu-id="f10f1-198">Способ получения и отправки значение дайджеста формы зависит от надстройки</span><span class="sxs-lookup"><span data-stu-id="f10f1-198">The way you get and send the form digest value depends on the add-in</span></span>
<span data-ttu-id="f10f1-199"><a name="FormDigest"> </a></span><span class="sxs-lookup"><span data-stu-id="f10f1-199"><a name="FormDigest"> </a></span></span>

<span data-ttu-id="f10f1-p124">При отправке запроса POST в его заголовке **X-RequestDigest** должно быть указано значение дайджеста формы. Однако способ получения и отправки значения зависит от надстройки.</span><span class="sxs-lookup"><span data-stu-id="f10f1-p124">When you send a POST request, the request must include the form digest value in the  **X-RequestDigest** header. However, the way you get and send the value differs by add-in:</span></span>
 

 

- <span data-ttu-id="f10f1-202">В надстройках, размещаемых в SharePoint, можно передавать следующий заголовок:</span><span class="sxs-lookup"><span data-stu-id="f10f1-202">In SharePoint-hosted add-ins, you can just pass the following header:</span></span> 
 
 <span data-ttu-id="f10f1-203">"X-RequestDigest": $("#__REQUESTDIGEST").val()</span><span class="sxs-lookup"><span data-stu-id="f10f1-203">"X-RequestDigest": $("#__REQUESTDIGEST").val()</span></span>
    
 
- <span data-ttu-id="f10f1-204">В надстройках с размещением в облаке, использующих OAuth, для начала необходимо получить значение дайджеста формы, отправив запрос конечной точке **contextinfo**, а затем добавить его в запросы, как показано в разделе [Запись данных с помощью интерфейса REST](complete-basic-operations-using-sharepoint-rest-endpoints.md#WritingData).</span><span class="sxs-lookup"><span data-stu-id="f10f1-204">In cloud-hosted add-ins that use OAuth, first retrieve the form digest value by sending a request to the  **contextinfo** endpoint, and then add it to requests, as shown in [Writing data by using the REST interface](complete-basic-operations-using-sharepoint-rest-endpoints.md#WritingData).</span></span>
    
 
- <span data-ttu-id="f10f1-p125">В надстройках с размещением в облаке, которые используют междоменную библиотеку JavaScript, не требуется указывать значение дайджеста формы. По умолчанию SP.RequestExecutor делает это автоматически. (Метод также обрабатывает значение content-length.)</span><span class="sxs-lookup"><span data-stu-id="f10f1-p125">In cloud-hosted add-ins that use the JavaScript cross-domain library, you don't need to specify the form digest value. By default, SP.RequestExecutor automatically handles this for you. (It also handles the content-length value.)</span></span>
    
 

### <a name="add-ins-that-use-oauth-must-pass-access-tokens-in-requests"></a><span data-ttu-id="f10f1-208">Надстройки, использующие OAuth, должны передавать маркеры доступа в запросах</span><span class="sxs-lookup"><span data-stu-id="f10f1-208">Add-ins that use OAuth must pass access tokens in requests</span></span>
<span data-ttu-id="f10f1-209"><a name="OAuthTokens"> </a></span><span class="sxs-lookup"><span data-stu-id="f10f1-209"><a name="OAuthTokens"> </a></span></span>

<span data-ttu-id="f10f1-p126">Чтобы авторизовать доступ к данным в SharePoint, надстройки с размещением в облаке используют OAuth или междоменную библиотеку. Компоненты надстроек с кодом, выполняемым на удаленном веб-сервере, должны использовать OAuth для авторизации доступа к данным в SharePoint. В этом случае необходимо включить заголовок **Authorization** для отправки маркера доступа. Пример добавления заголовка авторизации к объекту **HTTPWebRequest** см. в разделе [Чтение данных с помощью интерфейса SharePoint REST](complete-basic-operations-using-sharepoint-rest-endpoints.md#ReadingData).</span><span class="sxs-lookup"><span data-stu-id="f10f1-p126">Cloud-hosted add-ins use either OAuth or the cross-domain library to authorize access to SharePoint data. Add-in components with code that runs on a remote web server must use OAuth to authorize access to SharePoint data. In this case, you need to include an  **Authorization** header to send the access token. See [Reading data with the SharePoint REST interface](complete-basic-operations-using-sharepoint-rest-endpoints.md#ReadingData) for an example that adds an authorization header to an **HTTPWebRequest** object.</span></span>
 

 

 <span data-ttu-id="f10f1-p127">**Примечание.** Компоненты надстроек с размещением в облаке, написанные на JavaScript, должны использовать объект **SP.RequestExecutor** из междоменной библиотеки для доступа к данным SharePoint. В запросы к междоменной библиотеке не обязательно включать маркер доступа.</span><span class="sxs-lookup"><span data-stu-id="f10f1-p127">**Note**  Cloud-hosted add-in components that are written in JavaScript must use the  **SP.RequestExecutor** object in the cross-domain library to access to SharePoint data. Cross-domain library requests don't need to include an access token.</span></span>
 

<span data-ttu-id="f10f1-216">Подробнее о маркерах доступа OAuth и их получении см. в статьях  [Поток маркеров контекста OAuth для надстроек в SharePoint](context-token-oauth-flow-for-sharepoint-add-ins.md) и [Поток кода аутентификации OAuth для надстроек в SharePoint](authorization-code-oauth-flow-for-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="f10f1-216">To learn more about OAuth access tokens and how to get them, see  [Context Token OAuth flow for SharePoint Add-ins](context-token-oauth-flow-for-sharepoint-add-ins.md) and [Authorization Code OAuth flow for SharePoint Add-ins](authorization-code-oauth-flow-for-sharepoint-add-ins.md).</span></span>
 

 

### <a name="endpoint-uris-in-cross-domain-requests-use-spappcontextsite-to-change-the-context"></a><span data-ttu-id="f10f1-217">URI конечных точек в междоменных запросах используют объект SP.AppContextSite для изменения контекста</span><span class="sxs-lookup"><span data-stu-id="f10f1-217">Endpoint URIs in cross-domain requests use SP.AppContextSite to change the context</span></span>
<span data-ttu-id="f10f1-218"><a name="AppContextSite"> </a></span><span class="sxs-lookup"><span data-stu-id="f10f1-218"><a name="AppContextSite"> </a></span></span>

<span data-ttu-id="f10f1-p128">Запросы отправляются конечной точке ресурсов, указанной в свойстве **url** запроса. URI конечных точек представляются в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="f10f1-p128">Requests are sent to the resource endpoint that's specified in the  **url** property of the request. Endpoint URIs use the following format:</span></span>
 

 
 <span data-ttu-id="f10f1-221">_<site url>_/_api/ _<context>_/ _<resource>_ (например, https://contoso.com/_api/web/lists)</span><span class="sxs-lookup"><span data-stu-id="f10f1-221">_<site url>_/_api/ _<context>_/ _<resource>_ (example, https://contoso.com/_api/web/lists)</span></span>
 

 
<span data-ttu-id="f10f1-p129">Этот формат используется в запросах к междоменной библиотеке при доступе к данным на сайте надстройки — стандартном контексте таких запросов. Однако для доступа к данным на хост-сайте или в другом семействе веб-сайтов запросам необходимо инициализировать хост-сайт или другое семейство веб-сайтов в качестве контекста. Для этого они используют конечную точку **SP.AppContextSite** в URI, как показано в таблице 1. В примерах URI из таблицы 1 используется псевдоним **@target** для отправки целевого URL-адреса в строке запроса, так как URL-адрес содержит специальный символ (":").</span><span class="sxs-lookup"><span data-stu-id="f10f1-p129">Cross-domain library requests use this format when they access data on the add-in web, which is the default context for cross-domain library requests. But to access data on the host web or on another site collection, the requests need to initialize the host web or other site collection as the context. To do this, they use the  **SP.AppContextSite** endpoint in the URI, as shown in Table 1. The example URIs in Table 1 use the **@target** alias to send the target URL in the query string because the URL contains a special character (':').</span></span>
 

 

 <span data-ttu-id="f10f1-226">**Примечание.** Для доступа к данным SharePoint при использовании междоменной библиотеки надстройке с размещением в облаке необходим экземпляр сайта надстройки.</span><span class="sxs-lookup"><span data-stu-id="f10f1-226">**Note**  An add-in web instance is required for a cloud-hosted add-in to access SharePoint data when using the cross-domain library.</span></span>
 


<span data-ttu-id="f10f1-227">**Таблица 1. Изменение контекста запроса с помощью конечной точки SP.AppContextSite**</span><span class="sxs-lookup"><span data-stu-id="f10f1-227">**Table 1. Using the SP.AppContextSite endpoint to change the context of the request**</span></span>


|<span data-ttu-id="f10f1-228">**Тип надстройки**</span><span class="sxs-lookup"><span data-stu-id="f10f1-228">**Add-in type**</span></span>|<span data-ttu-id="f10f1-229">**Сценарий междоменного доступа к данным**</span><span class="sxs-lookup"><span data-stu-id="f10f1-229">**Cross-domain data access scenario**</span></span>|<span data-ttu-id="f10f1-230">**Пример URI конечной точки**</span><span class="sxs-lookup"><span data-stu-id="f10f1-230">**Example endpoint URI**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="f10f1-231">С размещением в облаке</span><span class="sxs-lookup"><span data-stu-id="f10f1-231">Cloud-hosted</span></span>|<span data-ttu-id="f10f1-232">Компонент надстройки JavaScript получает доступ к данным хост-сайта с помощью междоменной библиотеки</span><span class="sxs-lookup"><span data-stu-id="f10f1-232">JavaScript add-in component accessing host web data by using the cross-domain library</span></span>| <span data-ttu-id="f10f1-233">_<app web url>_/_api/SP.AppContextSite(@target)/web/lists?@target=' _<host web url>_'</span><span class="sxs-lookup"><span data-stu-id="f10f1-233">_<app web url>_/_api/SP.AppContextSite(@target)/web/lists?@target=' _<host web url>_'</span></span>|
|<span data-ttu-id="f10f1-234">Размещение в облаке</span><span class="sxs-lookup"><span data-stu-id="f10f1-234">Cloud-hosted</span></span>|<span data-ttu-id="f10f1-235">Компонент надстройки JavaScript получает доступ к данным в семействе веб-сайтов, не включающем хост-сайт, с помощью междоменной библиотеки (только для надстроек с разрешениями на уровне клиента)</span><span class="sxs-lookup"><span data-stu-id="f10f1-235">JavaScript add-in component accessing data in a site collection other than the host web by using the cross-domain library (tenant-scoped add-ins only)</span></span>| <span data-ttu-id="f10f1-236">_<app web url>_/_api/SP.AppContextSite(@target)/web/title?@target=' _<target site url>_'</span><span class="sxs-lookup"><span data-stu-id="f10f1-236">_<app web url>_/_api/SP.AppContextSite(@target)/web/title?@target=' _<target site url>_'</span></span>|
|<span data-ttu-id="f10f1-237">Размещение в SharePoint</span><span class="sxs-lookup"><span data-stu-id="f10f1-237">SharePoint-hosted</span></span>|<span data-ttu-id="f10f1-238">Компонент сайта надстройки получает доступ к данным в другом семействе веб-сайтов (только для надстроек с разрешениями на уровне клиента)</span><span class="sxs-lookup"><span data-stu-id="f10f1-238">Add-in web component accessing data in another site collection (tenant-scoped add-ins only)</span></span>| <span data-ttu-id="f10f1-239">_<app web url>_/_api/SP.AppContextSite(@target)/web/title?@target=' _<target site url>_'</span><span class="sxs-lookup"><span data-stu-id="f10f1-239">_<app web url>_/_api/SP.AppContextSite(@target)/web/title?@target=' _<target site url>_'</span></span>|

 <span data-ttu-id="f10f1-p130">**Примечание.** Для междоменного доступа к данным также требуются соответствующие разрешения для надстроек. Дополнительные сведения см. в разделах [Доступ к данным на хост-сайте](access-sharepoint-data-from-add-ins-using-the-cross-domain-library.md#SP15Accessdatafromremoteapp_Hostweb) и [Доступ к данным в нескольких семействах веб-сайтов](access-sharepoint-data-from-add-ins-using-the-cross-domain-library.md#SP15Accessdatafromremoteapp_TenantScope).</span><span class="sxs-lookup"><span data-stu-id="f10f1-p130">**Note**  Cross-domain data access scenarios also require appropriate add-in permissions. For more information, see  [Access data from the host web](access-sharepoint-data-from-add-ins-using-the-cross-domain-library.md#SP15Accessdatafromremoteapp_Hostweb) and [Access data across site collections](access-sharepoint-data-from-add-ins-using-the-cross-domain-library.md#SP15Accessdatafromremoteapp_TenantScope).</span></span>
 

<span data-ttu-id="f10f1-p131">Надстройки SharePoint могут получать URL-адреса сайта надстройки и хост-сайта из строки запроса страницы надстройки, как показано в следующем примере кода. Кроме того, в этом примере показывается, как ссылаться на междоменную библиотеку, определенную в файле SP.RequestExecutor.js на хост-сайте. Этот пример предполагает, что ваша надстройка запускается из SharePoint. Указания по правильной настройке контекста SharePoint, если надстройка запускается не из SharePoint, см. в статье  [Поток кода аутентификации OAuth для надстроек в SharePoint](authorization-code-oauth-flow-for-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="f10f1-p131">SharePoint Add-ins can get the add-in web URL and host web URL from the query string of the add-in page, as shown in the following code example. The example also shows how to reference the cross-domain library, which is defined in the SP.RequestExecutor.js file on the host web. The example assumes that your add-in launches from SharePoint. See  [Authorization Code OAuth flow for SharePoint Add-ins](authorization-code-oauth-flow-for-sharepoint-add-ins.md) for guidance on setting your SharePoint context correctly when your add-in does not launch from SharePoint.</span></span>
 

 



```
var hostweburl;
var appweburl;

// Get the URLs for the add-in web the host web URL from the query string.
$(document).ready(function () {
  //Get the URI decoded URLs.
  hostweburl = decodeURIComponent(getQueryStringParameter("SPHostUrl"));
  appweburl = decodeURIComponent(getQueryStringParameter("SPAppWebUrl"));

  // Load the SP.RequestExecutor.js file.
  $.getScript(hostweburl + "/_layouts/15/SP.RequestExecutor.js", runCrossDomainRequest);
});

// Build and send the HTTP request.
function runCrossDomainRequest() {
  var executor = new SP.RequestExecutor(appweburl); 
  executor.executeAsync({
      url: appweburl + "/_api/SP.AppContextSite(@target)/web/lists?@target='" + hostweburl + "'",
      method: "GET", 
      headers: { "Accept": "application/json; odata=verbose" }, 
      success: successHandler, 
      error: errorHandler 
  });
}

// Get a query string value.
// For production add-ins, you may want to use a library to handle the query string.
function getQueryStringParameter(paramToRetrieve) {
  var params = document.URL.split("?")[1].split("&amp;");
  var strParams = "";
  for (var i = 0; i < params.length; i = i + 1) {
    var singleParam = params[i].split("=");
    if (singleParam[0] == paramToRetrieve) return singleParam[1];
  }
}
??? // success and error callback functions
```


## <a name="properties-used-in-rest-requests"></a><span data-ttu-id="f10f1-246">Свойства, используемые в запросах REST</span><span class="sxs-lookup"><span data-stu-id="f10f1-246">Properties used in REST requests</span></span>
<span data-ttu-id="f10f1-247"><a name="bk_requestElements"> </a></span><span class="sxs-lookup"><span data-stu-id="f10f1-247"><a name="bk_requestElements"> </a></span></span>

<span data-ttu-id="f10f1-248">В таблице 2 показаны свойства, которые часто используются в HTTP-запросах для службы REST SharePoint.</span><span class="sxs-lookup"><span data-stu-id="f10f1-248">Table 2 shows properties that are commonly used in HTTP requests for the SharePoint REST service.</span></span>
 

 

<span data-ttu-id="f10f1-249">**Таблица 2. Использование свойств запроса REST в HTTP-запросах**</span><span class="sxs-lookup"><span data-stu-id="f10f1-249">**Table 2. When to use REST request properties in HTTP requests**</span></span>


|<span data-ttu-id="f10f1-250">**Свойства**</span><span class="sxs-lookup"><span data-stu-id="f10f1-250">**Properties**</span></span>|<span data-ttu-id="f10f1-251">**Когда требуется**</span><span class="sxs-lookup"><span data-stu-id="f10f1-251">**When required**</span></span>|<span data-ttu-id="f10f1-252">**Описание**</span><span class="sxs-lookup"><span data-stu-id="f10f1-252">**Description**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="f10f1-253">**url**</span><span class="sxs-lookup"><span data-stu-id="f10f1-253">**url**</span></span>|<span data-ttu-id="f10f1-254">Все запросы</span><span class="sxs-lookup"><span data-stu-id="f10f1-254">All requests</span></span>|<span data-ttu-id="f10f1-p132">URL-адрес конечной точки ресурса REST. Например:  `http://<site url>/_api/web/lists`</span><span class="sxs-lookup"><span data-stu-id="f10f1-p132">The URL of the REST resource endpoint. Example:  `http://<site url>/_api/web/lists`</span></span>|
|<span data-ttu-id="f10f1-257">**method** (или **type**)</span><span class="sxs-lookup"><span data-stu-id="f10f1-257">**method** (or **type**)</span></span>|<span data-ttu-id="f10f1-258">Все запросы</span><span class="sxs-lookup"><span data-stu-id="f10f1-258">All requests</span></span>|<span data-ttu-id="f10f1-p133">Метод HTTP-запроса: **GET** для операций чтения и **POST** для операций записи. Запросы **POST** могут выполнять операции обновления или удаления с помощью команды **DELETE**, **MERGE** или **PUT** в заголовке **X-HTTP-Method**.</span><span class="sxs-lookup"><span data-stu-id="f10f1-p133">The HTTP request method:  **GET** for read operations and **POST** for write operations. **POST** requests can perform update or delete operations by specifying a **DELETE**,  **MERGE**, or  **PUT** verb in the **X-HTTP-Method** header.</span></span>|
|<span data-ttu-id="f10f1-261">**body** (или **data**)</span><span class="sxs-lookup"><span data-stu-id="f10f1-261">**body** (or **data**)</span></span>|<span data-ttu-id="f10f1-262">Запросы **POST**, которые отправляют данные в тексте запроса</span><span class="sxs-lookup"><span data-stu-id="f10f1-262">**POST** requests that send data in the request body</span></span>|<span data-ttu-id="f10f1-p134">Текст запроса POST. Отправляет данные (например, сложные типы), которые невозможно передать в URI конечной точки. Используется с заголовком **content-length**.</span><span class="sxs-lookup"><span data-stu-id="f10f1-p134">The body of the POST request. Sends data (such as complex types) that can't be sent in the endpoint URI. Used with the  **content-length** header.</span></span>|
|<span data-ttu-id="f10f1-266">Заголовок **Authentication**</span><span class="sxs-lookup"><span data-stu-id="f10f1-266">**Authentication** header</span></span>|<span data-ttu-id="f10f1-p135">Удаленные надстройки, которые используют OAuth для проверки подлинности пользователей. Не применяется при использовании JavaScript или междоменной библиотеки.</span><span class="sxs-lookup"><span data-stu-id="f10f1-p135">Remote add-ins that are using OAuth to authenticate users. Does not apply when using JavaScript or the cross domain library.</span></span>|<span data-ttu-id="f10f1-p136">Отправляет маркер доступа (полученный от сервера токенов безопасности для службы контроля доступа Microsoft Azure), который используется для проверки подлинности пользователя для запроса. Например:  `"Authorization": "Bearer " + accessToken`, где  `accessToken` представляет переменную, которая сохраняет маркер. Маркеры должны загружаться с использованием кода на стороне сервера. </span><span class="sxs-lookup"><span data-stu-id="f10f1-p136">Sends the OAuth access token (obtained from a Microsoft Access Control Service (ACS) secure token server) that's used to authenticate the user for the request. Example:  `"Authorization": "Bearer " + accessToken`, where  `accessToken` represents the variable that stores the token. Tokens must be retrieved by using server-side code.</span></span>|
|<span data-ttu-id="f10f1-272">Заголовок **X-RequestDigest**</span><span class="sxs-lookup"><span data-stu-id="f10f1-272">**X-RequestDigest** header</span></span>|<span data-ttu-id="f10f1-273">Запросы **POST** (кроме запросов SP.RequestExecutor)</span><span class="sxs-lookup"><span data-stu-id="f10f1-273">**POST** requests (except SP.RequestExecutor requests)</span></span>|<span data-ttu-id="f10f1-p137">Удаленные надстройки, использующие протокол OAuth, могут получить значение дайджеста формы от конечной точки  `http://<site url>/_api/contextinfo`. Надстройки, размещенные в SharePoint, могут получить это значение от элемента управления страницей **#__REQUESTDIGEST**, если он доступен на странице SharePoint. См. раздел  [Запись данных с помощью интерфейса REST](#WritingData).  </span><span class="sxs-lookup"><span data-stu-id="f10f1-p137">Remote add-ins that use OAuth can get the form digest value from the  `http://<site url>/_api/contextinfo` endpoint. SharePoint-hosted add-ins can get the value from the **#__REQUESTDIGEST** page control if it's available on the SharePoint page. See [Writing data by using the REST interface](#WritingData).</span></span>|
|<span data-ttu-id="f10f1-277">Заголовок **accept**</span><span class="sxs-lookup"><span data-stu-id="f10f1-277">**accept** header</span></span>|<span data-ttu-id="f10f1-278">Запросы, которые возвращают метаданные SharePoint</span><span class="sxs-lookup"><span data-stu-id="f10f1-278">Requests that return SharePoint metadata</span></span>|<span data-ttu-id="f10f1-p138">Указывает формат данных ответа от сервера. Форматом по умолчанию является  `application/atom+xml`, например:  `"accept":"application/json;odata=verbose"`</span><span class="sxs-lookup"><span data-stu-id="f10f1-p138">Specifies the format for response data from the server. The default format is  `application/atom+xml`. Example:  `"accept":"application/json;odata=verbose"`</span></span>|
|<span data-ttu-id="f10f1-282">Заголовок **content-type**</span><span class="sxs-lookup"><span data-stu-id="f10f1-282">**content-type** header</span></span>|<span data-ttu-id="f10f1-283">Запросы **POST**, которые отправляют данные в тексте запроса</span><span class="sxs-lookup"><span data-stu-id="f10f1-283">**POST** requests that send data in the request body</span></span>|<span data-ttu-id="f10f1-p139">Указывает формат данных, которые клиент отправляет серверу. Форматом по умолчанию является  `application/atom+xml`, например:  `"content-type":"application/json;odata=verbose"`</span><span class="sxs-lookup"><span data-stu-id="f10f1-p139">Specifies the format of the data that the client is sending to the server. The default format is  `application/atom+xml`. Example:  `"content-type":"application/json;odata=verbose"`</span></span>|
|<span data-ttu-id="f10f1-287">Заголовок **content-length**</span><span class="sxs-lookup"><span data-stu-id="f10f1-287">**content-length** header</span></span>|<span data-ttu-id="f10f1-288">Запросы **POST**, которые отправляют данные в тексте запроса (кроме запросов SP.RequestExecutor)</span><span class="sxs-lookup"><span data-stu-id="f10f1-288">**POST** requests that send data in the request body (except SP.RequestExecutor requests)</span></span>|<span data-ttu-id="f10f1-p140">Указывает длину содержимого, например:  `"content-length":requestBody.length`</span><span class="sxs-lookup"><span data-stu-id="f10f1-p140">Specifies the length of the content. Example:  `"content-length":requestBody.length`</span></span>|
|<span data-ttu-id="f10f1-291">Заголовок **IF-MATCH**</span><span class="sxs-lookup"><span data-stu-id="f10f1-291">**IF-MATCH** header</span></span>|<span data-ttu-id="f10f1-292">Запросы **POST** для операций **DELETE**, **MERGE** и **PUT**, в первую очередь для изменения списков и библиотек.</span><span class="sxs-lookup"><span data-stu-id="f10f1-292">**POST** requests for **DELETE**,  **MERGE**, or  **PUT** operations, primarily for changing lists and libraries.</span></span>|<span data-ttu-id="f10f1-p141">Предоставляет способ проверки того, что изменяемый объект не менялся с момента его последней загрузки. Или позволяет включить перезапись любых изменений, как показано в следующем примере:  `"IF-MATCH":"*"`</span><span class="sxs-lookup"><span data-stu-id="f10f1-p141">Provides a way to verify that the object being changed has not been changed since it was last retrieved. Or, lets you specify to overwrite any changes, as shown in the following example:  `"IF-MATCH":"*"`</span></span>|
|<span data-ttu-id="f10f1-295">Заголовок **X-HTTP-Method**</span><span class="sxs-lookup"><span data-stu-id="f10f1-295">**X-HTTP-Method** header</span></span>|<span data-ttu-id="f10f1-296">Запросы **POST** для операций **DELETE**, **MERGE** и **PUT**</span><span class="sxs-lookup"><span data-stu-id="f10f1-296">**POST** requests for **DELETE**,  **MERGE**, or  **PUT** operations</span></span>|<span data-ttu-id="f10f1-p142">Указывает, что запрос выполняет операцию обновления или удаления. Пример: `"X-HTTP-Method":"PUT"`</span><span class="sxs-lookup"><span data-stu-id="f10f1-p142">Used to specify that the request performs an update or delete operation. Example:  `"X-HTTP-Method":"PUT"`</span></span>|
|<span data-ttu-id="f10f1-299">**binaryStringRequestBody**</span><span class="sxs-lookup"><span data-stu-id="f10f1-299">**binaryStringRequestBody**</span></span>|<span data-ttu-id="f10f1-300">Запросы **POST** для SP.RequestExecutor, которые отправляют двоичные данные в тексте запроса</span><span class="sxs-lookup"><span data-stu-id="f10f1-300">SP.RequestExecutor  **POST** requests that send binary data in the body</span></span>|<span data-ttu-id="f10f1-p143">Указывает, является ли текст запроса двоичной строкой. **Boolean**.</span><span class="sxs-lookup"><span data-stu-id="f10f1-p143">Specifies whether the request body is a binary string.  **Boolean**.</span></span>|
|<span data-ttu-id="f10f1-303">**binaryStringResponseBody**</span><span class="sxs-lookup"><span data-stu-id="f10f1-303">**binaryStringResponseBody**</span></span>|<span data-ttu-id="f10f1-304">Запросы SP.RequestExecutor, возвращающие двоичные данные</span><span class="sxs-lookup"><span data-stu-id="f10f1-304">SP.RequestExecutor requests that return binary data</span></span>|<span data-ttu-id="f10f1-p144">Указывает, является ли отклик двоичной строкой. **Логическое значение**.</span><span class="sxs-lookup"><span data-stu-id="f10f1-p144">Specifies whether the response is a binary string.  **Boolean**.</span></span>|

## <a name="batch-job-support"></a><span data-ttu-id="f10f1-307">Поддержка пакетных заданий</span><span class="sxs-lookup"><span data-stu-id="f10f1-307">Batch job support</span></span>
<span data-ttu-id="f10f1-308"><a name="batch"> </a></span><span class="sxs-lookup"><span data-stu-id="f10f1-308"><a name="batch"> </a></span></span>

<span data-ttu-id="f10f1-p145">Служба REST SharePoint Online (а также локальной версии SharePoint 2016 и последующих выпусков) поддерживает объединение нескольких запросов в одном вызове службы с помощью параметра запроса OData  `$batch`. Дополнительные сведения и ссылки на примеры кода см. в разделе  [Создание пакетного запроса с помощью интерфейсов REST API](make-batch-requests-with-the-rest-apis.md).</span><span class="sxs-lookup"><span data-stu-id="f10f1-p145">The SharePoint Online (and on-premise SharePoint 2016 and later) REST service supports combining multiple requests into a single call to the service by using the OData  `$batch` query option. For details and links to code samples, see [Make batch requests with the REST APIs](make-batch-requests-with-the-rest-apis.md).</span></span>
 

 

## <a name="additional-resources"></a><span data-ttu-id="f10f1-311">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="f10f1-311">Additional resources</span></span>
<span data-ttu-id="f10f1-312"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="f10f1-312"><a name="bk_addresources"> </a></span></span>


-  [<span data-ttu-id="f10f1-313">Работа со списками и элементами списков в службе REST</span><span class="sxs-lookup"><span data-stu-id="f10f1-313">Working with lists and list items with REST</span></span>](working-with-lists-and-list-items-with-rest.md)
    
 
-  [<span data-ttu-id="f10f1-314">Работа с папками и файлами в службе REST</span><span class="sxs-lookup"><span data-stu-id="f10f1-314">Working with folders and files with REST</span></span>](working-with-folders-and-files-with-rest.md)
    
 
-  [<span data-ttu-id="f10f1-315">SharePoint-Add-in-REST-OData-BasicDataOperations</span><span class="sxs-lookup"><span data-stu-id="f10f1-315">SharePoint-Add-in-REST-OData-BasicDataOperations</span></span>](https://github.com/OfficeDev/SharePoint-Add-in-REST-OData-BasicDataOperations)
    
 
-  [<span data-ttu-id="f10f1-316">SharePoint: выполнение основных операций доступа к данным в файлах и папках с помощью REST</span><span class="sxs-lookup"><span data-stu-id="f10f1-316">SharePoint: Perform basic data access operations on files and folders by using REST</span></span>](http://code.msdn.microsoft.com/SharePoint-Perform-ab9c4ae5)
    
 
-  [<span data-ttu-id="f10f1-317">Выполнение базовых операций с использованием кода библиотеки клиента в SharePoint</span><span class="sxs-lookup"><span data-stu-id="f10f1-317">Complete basic operations using SharePoint client library code</span></span>](complete-basic-operations-using-sharepoint-client-library-code.md)
    
 
-  [<span data-ttu-id="f10f1-318">Выполнение базовых операций с использованием кода библиотеки JavaScript в SharePoint</span><span class="sxs-lookup"><span data-stu-id="f10f1-318">Complete basic operations using JavaScript library code in SharePoint</span></span>](complete-basic-operations-using-javascript-library-code-in-sharepoint.md)
    
 
-  [<span data-ttu-id="f10f1-319">Разработка надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="f10f1-319">Develop SharePoint Add-ins</span></span>](develop-sharepoint-add-ins.md)
    
 
-  [<span data-ttu-id="f10f1-320">Безопасный доступ к данным и клиентские объектные модели для надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="f10f1-320">Secure data access and client object models for SharePoint Add-ins</span></span>](secure-data-access-and-client-object-models-for-sharepoint-add-ins.md)
    
 
-  [<span data-ttu-id="f10f1-321">Работа с внешними данными в SharePoint</span><span class="sxs-lookup"><span data-stu-id="f10f1-321">Work with external data in SharePoint</span></span>](work-with-external-data-in-sharepoint.md)
    
 
-  [<span data-ttu-id="f10f1-322">Протокол OData</span><span class="sxs-lookup"><span data-stu-id="f10f1-322">Open Data Protocol</span></span>](http://www.odata.org/)
    
 
-  [<span data-ttu-id="f10f1-323">OData: формат нотации объектов JavaScript (JSON)</span><span class="sxs-lookup"><span data-stu-id="f10f1-323">OData: JavaScript Object Notation (JSON) Format</span></span>](http://www.odata.org/documentation/odata-version-2-0/JSON-format/)
    
 
-  [<span data-ttu-id="f10f1-324">Назначение настраиваемых разрешений для списка с помощью интерфейса REST</span><span class="sxs-lookup"><span data-stu-id="f10f1-324">Set custom permissions on a list by using the REST interface</span></span>](set-custom-permissions-on-a-list-by-using-the-rest-interface.md)
    
 

 

 
