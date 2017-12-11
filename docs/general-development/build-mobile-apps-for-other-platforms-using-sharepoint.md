---
title: "Создание мобильных приложений для других платформ с помощью SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 017df869-44fb-4ffe-82fb-4654e01329ad
ms.openlocfilehash: 9332b25b93ea89d0bafc4a7074d1b0895f82f0f8
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="build-mobile-apps-for-other-platforms-using-sharepoint"></a><span data-ttu-id="d1721-102">Создание мобильных приложений для других платформ с помощью SharePoint</span><span class="sxs-lookup"><span data-stu-id="d1721-102">Build mobile apps for other platforms using SharePoint</span></span>
<span data-ttu-id="d1721-103">Сведения об использовании представлений состояния (REST) для создания мобильного приложения SharePoint для любой платформы.</span><span class="sxs-lookup"><span data-stu-id="d1721-103">Learn how to use Representational State Transfer (REST) to create a SharePoint mobile app for any platform.</span></span>
<span data-ttu-id="d1721-104">Мобильные устройства становятся более мощные и удобные в настоящее время.</span><span class="sxs-lookup"><span data-stu-id="d1721-104">Mobile devices have become more powerful and easy to use nowadays.</span></span> <span data-ttu-id="d1721-105">Ноутбуки, нетбуков, планшетных ПК и мобильных телефонов предоставляют доступ к информации и приложений, которые необходимы для выполнения их работы сотрудников.</span><span class="sxs-lookup"><span data-stu-id="d1721-105">Laptops, netbooks, tablet PCs, and mobile phones provide workers access to the information and applications that they need to do their jobs.</span></span> <span data-ttu-id="d1721-106">И разработка приложений для мобильных устройств является теперь проще, чем когда-либо.</span><span class="sxs-lookup"><span data-stu-id="d1721-106">And developing applications for mobile devices is now easier than ever.</span></span> <span data-ttu-id="d1721-107">В результате больше бизнес-сценарии запросами интеграции клиентских приложений с бизнес-процессами.</span><span class="sxs-lookup"><span data-stu-id="d1721-107">As a result, more and more business scenarios demand integrating client applications together with their business processes.</span></span> <span data-ttu-id="d1721-108">В этой статье описывается, как интегрировать приложения мобильного клиента вместе с SharePoint.</span><span class="sxs-lookup"><span data-stu-id="d1721-108">This article describes how to integrate mobile client apps together with SharePoint.</span></span> <span data-ttu-id="d1721-109">Можно создать мобильного приложения для просмотра SharePoint содержимого из любого места и подключать к спискам SharePoint и библиотеки для доступа к данным.</span><span class="sxs-lookup"><span data-stu-id="d1721-109">You can create a mobile app to browse SharePoint content from any location and connect with SharePoint lists and libraries to access data.</span></span>
  
    
    

<span data-ttu-id="d1721-110">Для разработки мобильных приложений, который взаимодействует с SharePoint, можно использовать общие службы, которые может осуществляться с использованием open протоколы.</span><span class="sxs-lookup"><span data-stu-id="d1721-110">To develop a mobile app that interacts with SharePoint, you can use common services that can be accessed using open protocols.</span></span> <span data-ttu-id="d1721-111">SharePoint Foundation 2010 представлено клиентских объектных моделей, которые включены разработчиков выполнение удаленной связи с SharePoint с помощью веб-программирования технологии выбранного: .NET Framework, Microsoft Silverlight или JavaScript.</span><span class="sxs-lookup"><span data-stu-id="d1721-111">SharePoint Foundation 2010 introduced the client object models, which enabled developers to perform remote communication with SharePoint by using the web programming technology of their choice: .NET Framework, Microsoft Silverlight, or JavaScript.</span></span> <span data-ttu-id="d1721-112">SharePoint представляется представлений состояния (REST) служба, которая полностью сравнимые клиентской объектной модели.</span><span class="sxs-lookup"><span data-stu-id="d1721-112">SharePoint introduces a Representational State Transfer (REST) service that is fully comparable to the client object models.</span></span> <span data-ttu-id="d1721-113">В SharePoint практически все API клиентской объектной модели будет иметь соответствующую конечную точку REST.</span><span class="sxs-lookup"><span data-stu-id="d1721-113">In SharePoint, nearly every API in the client object models will have a corresponding REST endpoint.</span></span> <span data-ttu-id="d1721-114">Теперь разработчики могут удаленного взаимодействия с помощью объектной модели SharePoint с помощью любой технологии, поддерживающей веб-запросы REST.</span><span class="sxs-lookup"><span data-stu-id="d1721-114">Now, developers can interact remotely with the SharePoint object model by using any technology that supports REST web requests.</span></span> <span data-ttu-id="d1721-115">REST может использоваться любой язык программирования, который вы хотите использовать для разработки мобильных приложений.</span><span class="sxs-lookup"><span data-stu-id="d1721-115">REST can be consumed by any programming language that you want to use for your mobile application development.</span></span>
<span data-ttu-id="d1721-116">Можно выполнять базовые создания, чтения, обновления и удаления (CRUD) операции с помощью интерфейса REST, доступного в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="d1721-116">You can perform basic create, read, update, and delete (CRUD) operations by using the REST interface provided by SharePoint.</span></span> <span data-ttu-id="d1721-117">REST предоставляет всех объектов SharePoint и операции, доступные в другие клиентские интерфейсы API SharePoint.</span><span class="sxs-lookup"><span data-stu-id="d1721-117">REST exposes all of the SharePoint entities and operations that are available in the other SharePoint client APIs.</span></span> <span data-ttu-id="d1721-118">Одно из преимуществ использования REST состоит в том, что вам не требуется добавлять ссылки на библиотеки и клиентские сборки SharePoint.</span><span class="sxs-lookup"><span data-stu-id="d1721-118">One advantage of using REST is that you don't have to add references to any SharePoint libraries or client assemblies.</span></span> <span data-ttu-id="d1721-119">Вместо этого соответствующим конечным точкам отправляются HTTP-запросы на получение или обновление сущностей SharePoint, таких как веб-сайты, списки и элементы списков.</span><span class="sxs-lookup"><span data-stu-id="d1721-119">Instead, you make HTTP requests to the appropriate endpoints to retrieve or update SharePoint entities, such as webs, lists, and list items.</span></span> <span data-ttu-id="d1721-120">Подробное введение в интерфейс SharePoint REST и ее архитектуры в разделе [операции запросов OData используется в запросах SharePoint REST](http://msdn.microsoft.com/library/d4b5c277-ed50-420c-8a9b-860342284b72%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="d1721-120">For a thorough introduction to the SharePoint REST interface and its architecture, see  [Use OData query operations in SharePoint REST requests](http://msdn.microsoft.com/library/d4b5c277-ed50-420c-8a9b-860342284b72%28Office.15%29.aspx).</span></span>
  
    
    


## <a name="rest-endpoints-in-sharepoint"></a><span data-ttu-id="d1721-121">Конечные точки REST в SharePoint</span><span class="sxs-lookup"><span data-stu-id="d1721-121">REST endpoints in SharePoint</span></span>
<span data-ttu-id="d1721-122"><a name="BuildMobileAppsInSharePoint2013ForNonWindowsPhone_REST_EndpointsInSharePoint2013"> </a></span><span class="sxs-lookup"><span data-stu-id="d1721-122"></span></span>

<span data-ttu-id="d1721-123">Чтобы использовать возможности REST, которые встроены в SharePoint, можно создать RESTful HTTP-запросов с использованием стандарта Open Data Protocol (OData), соответствующий API желаемую клиентской объектной модели.</span><span class="sxs-lookup"><span data-stu-id="d1721-123">To use the REST capabilities that are built into SharePoint, you can construct a RESTful HTTP request using the Open Data Protocol (OData) standard that corresponds to the desired client object model API.</span></span> <span data-ttu-id="d1721-124">Веб-службы client.svc обрабатывает HTTP-запрос и обслуживает соответствующий ответ в формате Atom или JavaScript Object Notation (JSON).</span><span class="sxs-lookup"><span data-stu-id="d1721-124">The client.svc web service handles the HTTP request and serves the appropriate response, in either Atom or JavaScript Object Notation (JSON) format.</span></span> <span data-ttu-id="d1721-125">Затем клиентское приложение должно проанализировать этот отклик.</span><span class="sxs-lookup"><span data-stu-id="d1721-125">The client application must then parse that response.</span></span> <span data-ttu-id="d1721-126">На рисунке 1 показано высокоуровневое представление архитектуры SharePoint REST.</span><span class="sxs-lookup"><span data-stu-id="d1721-126">Figure 1 shows a high-level view of the SharePoint REST architecture.</span></span>
  
    
    

<span data-ttu-id="d1721-127">**На рисунке 1. Архитектура SharePoint REST**</span><span class="sxs-lookup"><span data-stu-id="d1721-127">**Figure 1. SharePoint REST architecture**</span></span>

  
    
    

  
    
    
![Архитектура REST SharePoint](../images/SP15Con_BuildSharePointAppsForMobileDevices_Fig2.png)
  
    
    
<span data-ttu-id="d1721-129">Конечные точки в службе SharePoint REST соответствуют типы и элементы в объектной модели клиента SharePoint.</span><span class="sxs-lookup"><span data-stu-id="d1721-129">The endpoints in the SharePoint REST service correspond to the types and members in the SharePoint client object models.</span></span> <span data-ttu-id="d1721-130">С помощью HTTP-запросов, можно использовать эти конечные точки REST для выполнения типичных операций CRUD с SharePoint артефакты, такие как списки и сайты.</span><span class="sxs-lookup"><span data-stu-id="d1721-130">By using HTTP requests, you can use these REST endpoints to perform typical CRUD operations against SharePoint artifacts, such as lists and sites.</span></span>
  
    
    
<span data-ttu-id="d1721-131">В следующей таблице приведены общие правила.</span><span class="sxs-lookup"><span data-stu-id="d1721-131">In general:</span></span>
  
    
    

- <span data-ttu-id="d1721-132">Конечные точки, представляющие операций чтения сопоставление команд **GET** HTTP.</span><span class="sxs-lookup"><span data-stu-id="d1721-132">Endpoints that represent read operations map to HTTP **GET** commands.</span></span>
    
  
- <span data-ttu-id="d1721-133">Конечные точки, представляющие карты операции обновления **POST** команд HTTP.</span><span class="sxs-lookup"><span data-stu-id="d1721-133">Endpoints that represent update operations map to HTTP **POST** commands.</span></span>
    
  
- <span data-ttu-id="d1721-134">Конечные точки, представляющие обновление или Вставка карты операции по командам **PUT** HTTP.</span><span class="sxs-lookup"><span data-stu-id="d1721-134">Endpoints that represent update or insert operations map to HTTP **PUT** commands.</span></span>
    
  
<span data-ttu-id="d1721-135">При выборе HTTP-запросы для использования, необходимо учитывать следующее:</span><span class="sxs-lookup"><span data-stu-id="d1721-135">In choosing an HTTP request to use, you should also consider the following:</span></span>
  
    
    

- <span data-ttu-id="d1721-136">**POST** используется для создания артефакты, такие как списки и сайты.</span><span class="sxs-lookup"><span data-stu-id="d1721-136">Use **POST** to create artifacts such as lists and sites.</span></span> <span data-ttu-id="d1721-137">Службы SharePoint REST поддерживает отправку **POST** -команд, включая определения объектов, конечные точки, представляющие семейств сайтов.</span><span class="sxs-lookup"><span data-stu-id="d1721-137">The SharePoint REST service supports sending **POST** commands that include object definitions to endpoints that represent collections.</span></span>
    
  
- <span data-ttu-id="d1721-p106">Для операций **POST** значения по умолчанию устанавливаются все свойства, которые не являются обязательными. При попытке задать свойство только для чтения в процессе выполнения операции **POST** служба возвращает исключение.</span><span class="sxs-lookup"><span data-stu-id="d1721-p106">For **POST** operations, any properties that are not required are set to their default values. If you try to set a read-only property as part of a **POST** operation, the service returns an exception.</span></span>
    
  
- <span data-ttu-id="d1721-p107">Используйте **PUT**, **PATCH**и **MERGE** операций для обновления существующих объектов SharePoint. Каждая конечная точка службы, представляющий операцию **set** свойства объектов поддерживает **PUT** запросы и запросы на **MERGE**. Для запросов **MERGE** Установка свойств является необязательным; все свойства, которые явно не задана сохранение их текущее свойство. Но для команды **PUT** свойств, которые явно не задан значение их свойства по умолчанию. Кроме того Если не указать все настраиваемые свойства в объект обновления при использовании команд **PUT** HTTP, службы REST возвращает исключение.</span><span class="sxs-lookup"><span data-stu-id="d1721-p107">Use **PUT**, **PATCH**, and **MERGE** operations to update existing SharePoint objects. Any service endpoint that represents an object property **set** operation supports both **PUT** requests and **MERGE** requests. For **MERGE** requests, setting properties is optional; any properties that you do not explicitly set retain their current property. But for **PUT** commands, any properties you do not explicitly set are set to their default properties. In addition, if you do not specify all settable properties in object updates when you use HTTP **PUT** commands, the REST service returns an exception.</span></span>
    
  
- <span data-ttu-id="d1721-145">Используйте команду HTTP **DELETE** для определенного URL-адреса конечной точки, чтобы удалить объект SharePoint, представленный этой конечной точкой.</span><span class="sxs-lookup"><span data-stu-id="d1721-145">Use the HTTP **DELETE** command against the specific endpoint URL to delete the SharePoint object represented by that endpoint.</span></span> <span data-ttu-id="d1721-146">Для пригодными объекты, такие как списки, файлов и элементов списка в результате **перезапуска** операции.</span><span class="sxs-lookup"><span data-stu-id="d1721-146">For recyclable objects, such as lists, files, and list items, this results in a **Recycle** operation.</span></span> <span data-ttu-id="d1721-147">Дополнительные сведения можно [узнать службы SharePoint REST](http://msdn.microsoft.com/library/2de035a0-ac75-43bd-9665-5c5a59c4c590%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="d1721-147">For more information, see [Get to know the SharePoint REST service](http://msdn.microsoft.com/library/2de035a0-ac75-43bd-9665-5c5a59c4c590%28Office.15%29.aspx).</span></span>
    
  

## <a name="authenticate-users-to-sharepoint"></a><span data-ttu-id="d1721-148">Проверка подлинности пользователей в SharePoint</span><span class="sxs-lookup"><span data-stu-id="d1721-148">Authenticate users to SharePoint</span></span>
<span data-ttu-id="d1721-149"><a name="BuildMobileAppsInSharePoint2013ForNonWindowsPhone_AuthenticatingNonWindowsAppForSharePoint"> </a></span><span class="sxs-lookup"><span data-stu-id="d1721-149"></span></span>

<span data-ttu-id="d1721-p109">Чтобы проверить подлинность мобильного приложения с помощью SharePoint, можно использовать протокол MS-OFBA. Дополнительные сведения можно  [[MS-OFBA]: спецификация протокола проверки подлинности на основе Office Forms](http://msdn.microsoft.com/library/30c7bbe9-b284-421f-b866-4e7ed4866027%28Office.15%29.aspx). Клиент протокола настроен для хранения и передачи файлов cookie. Клиента протокола использует протокол удаленного сервера для установки удостоверение пользователя как один или несколько файлов cookie HTTP. После установки удостоверение пользователя, затем клиент передает каждый файл cookie с каждого последующего запроса HHT.</span><span class="sxs-lookup"><span data-stu-id="d1721-p109">To authenticate your mobile app with SharePoint, you can use the MS-OFBA protocol. For more information, see  [[MS-OFBA]: Office Forms Based Authentication Protocol Specification](http://msdn.microsoft.com/library/30c7bbe9-b284-421f-b866-4e7ed4866027%28Office.15%29.aspx). The protocol client is configured to store and transmit cookies. The protocol client relies on the remote protocol server to set the user's identity as one or more HTTP cookies. After the user's identity is established, the client then sends each cookie with each subsequent HHT request.</span></span>
  
    
    
<span data-ttu-id="d1721-155">При входе пользователя в систему SharePoint, маркер пользователя проверка и затем используется для входа в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="d1721-155">When a user signs in to SharePoint, the user's token is validated and then used to sign in to SharePoint.</span></span> <span data-ttu-id="d1721-156">Маркер пользователя — это маркер безопасности, выданный поставщика удостоверений.</span><span class="sxs-lookup"><span data-stu-id="d1721-156">The user's token is a security token that is issued by an identity provider.</span></span> <span data-ttu-id="d1721-157">SharePoint поддерживает несколько типов проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="d1721-157">SharePoint supports several kinds of authentication.</span></span> <span data-ttu-id="d1721-158">Для получения дополнительных сведений см [проверки подлинности, авторизации и безопасности в SharePoint](authentication-authorization-and-security-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="d1721-158">For more information, see  [Authentication, authorization, and security in SharePoint](authentication-authorization-and-security-in-sharepoint.md).</span></span> <span data-ttu-id="d1721-159">Для проверки подлинности пользователя, можно использовать интерфейс REST.</span><span class="sxs-lookup"><span data-stu-id="d1721-159">To authenticate a user, you can use the REST interface.</span></span> <span data-ttu-id="d1721-160">Процесс авторизации проверяет наличие прошедшего проверку подлинности темы, (приложения или пользователя, который на of.md имени действует приложение) разрешения для выполнения определенных операций или получить доступ к определенным ресурсам (например, список или folder.md документов SharePoint).</span><span class="sxs-lookup"><span data-stu-id="d1721-160">The authorization process verifies that an authenticated subject (an app or a user the app is acting on behalf of.md) has permission to perform certain operations or to access specific resources (for example, a list or a SharePoint document folder.md).</span></span>
  
    
    
<span data-ttu-id="d1721-p111">OData позволяет получить доступ к источнику данных, таких как базы данных, просмотрев имеющиеся специально созданный URL-адрес. Это позволяет упрощенный подход для подключений и работа с источниками данных, размещенным внутри организации. OData  это протокол, который используется HTTP, Atom и Нотация объектов JavaScript (JSON) позволяет разработчикам создавать приложения, которые взаимодействуют с возрастающих число источников данных. Microsoft поддерживает создание этот стандарт, чтобы разрешить обмен данными между приложениями и хранилища данных, доступных из Интернета. Новый соединитель OData позволяет связываться с поставщиками OData SharePoint. Для получения дополнительных сведений см  [Open Data Protocol](http://www.odata.org).</span><span class="sxs-lookup"><span data-stu-id="d1721-p111">OData lets you access a data source, such as a database, by browsing to a specially constructed URL. This allows for a simplified approach for connecting to, and working with, data sources that are hosted within an organization. OData is a protocol that uses HTTP, Atom, and JavaScript Object Notation (JSON) to enable developers to write applications that communicate with an ever-growing number of data sources. Microsoft supports the creation of this standard as a way to enable the exchange of data between applications and data stores that can be accessed from the web. The new OData connector enables SharePoint to communicate with OData providers. For more information, see  [Open Data Protocol](http://www.odata.org).</span></span>
  
    
    
<span data-ttu-id="d1721-167">Следующий код демонстрирует способ проверки подлинности приложения для SharePoint с использованием конечные точки REST для проверки подлинности basic или на основе форм.</span><span class="sxs-lookup"><span data-stu-id="d1721-167">The following code demonstrates how to authenticate your app to SharePoint using REST endpoints for basic or forms-based authentication.</span></span> <span data-ttu-id="d1721-168">В следующем примере кода, записывается в C#, но можно использовать другие языки программирования для создания запроса Http, согласно требования платформы.</span><span class="sxs-lookup"><span data-stu-id="d1721-168">The following code example is written in C#, but any other programming language can be used to create the Http request, as per the requirement of the platform.</span></span>
  
    
    



```cs

string SharePointUrl = "https://Target SharePoint site";

private void AuthenticateToSharePoint(object sender, RoutedEventArgs e)
{
    ODataAuthenticator odataAt = new ODataAuthenticator("<Username>", "<password>");
    odataAt.CookieCachingEnabled = true;
    odataAt.AuthenticationCompleted += new EventHandler<AuthenticationCompletedEventArgs>(odataAt_AuthenticationCompleted);
    odataAt.Authenticate(new Uri(SharePointUrl, UriKind.Absolute));
}

void odataAt_AuthenticationCompleted(object sender, AuthenticationCompletedEventArgs e)
{
    HttpWebRequest endpointRequest = (HttpWebRequest)HttpWebRequest.Create(SharePointUrl.ToString() + "/_api/web/lists");
    endpointRequest.Method = "GET";
    endpointRequest.Accept = "application/json;odata=verbose";
          endpointRequest.CookieContainer = (sender as ODataAuthenticator).CookieContainer;
    
    endpointRequest.BeginGetResponse(new AsyncCallback((IAsyncResult res) =>
    {
        HttpWebRequest webReq = res.AsyncState as HttpWebRequest;
        WebResponse response = webReq.EndGetResponse(res);

        HttpWebResponse httpResponse = response as HttpWebResponse;
        HttpStatusCode code = httpResponse.StatusCode;
        this.Dispatcher.BeginInvoke(() =>
        {
            MessageBox.Show(code.ToString());
        });
    }), endpointRequest);
}

```

<span data-ttu-id="d1721-p113">Для проверки подлинности **HttpWebrequest** в конечную точку, вы должны сначала выполнять проверку подлинности в SharePoint с классом **ODataAuthenticator**. До вызова метода **Authenticate**, зарегистрируйте объект **ODataAuthenticator** к событию **AuthenticationCompleted**.</span><span class="sxs-lookup"><span data-stu-id="d1721-p113">To authenticate an **HttpWebrequest** to the endpoint, you should first authenticate to SharePoint with the **ODataAuthenticator** class. Before calling the **Authenticate** method, register the **ODataAuthenticator** object to the **AuthenticationCompleted** event.</span></span>
  
    
    
<span data-ttu-id="d1721-171">После проверки подлинности выполняется внутри события **OnAuthenticationCompleted**, можно использовать свойство **CookieContainer** на объект **ODataAuthenticator**, который можно присоединить к объекту **HttpWebRequest** для проверки подлинности вызовов REST для SharePoint.</span><span class="sxs-lookup"><span data-stu-id="d1721-171">After authentication is done inside the **OnAuthenticationCompleted** event, you can use the **CookieContainer** property on the **ODataAuthenticator** object, which can be attached to the **HttpWebRequest** object to authenticate the REST calls to SharePoint.</span></span>
  
    
    

## <a name="work-with-sharepoint-list-items-using-rest"></a><span data-ttu-id="d1721-172">Работа с элементами списков SharePoint с помощью REST</span><span class="sxs-lookup"><span data-stu-id="d1721-172">Work with SharePoint list items using REST</span></span>
<span data-ttu-id="d1721-173"><a name="BuildMobileAppsInSharePoint2013ForNonWindowsPhone_WorkingWithTheSharePointListItemUsingREST"> </a></span><span class="sxs-lookup"><span data-stu-id="d1721-173"></span></span>

<span data-ttu-id="d1721-174">В следующем примере показывается, как **получить** все элементы списка.</span><span class="sxs-lookup"><span data-stu-id="d1721-174">The following example shows how to **retrieve** all of a list's items.</span></span>
  
    
    

```

url: http://site url/_api/web/lists/GetByTitle('Test')/items
method: GET
headers:
// MS-OFBA protocol returns a cookie.
  Cookie: cookie


    accept: "application/json;odata=verbose" or "application/atom+xml"

```

<span data-ttu-id="d1721-175">В следующем примере показывается, как **получить** определенный элемент списка.</span><span class="sxs-lookup"><span data-stu-id="d1721-175">The following example shows how to **retrieve** a specific list item.</span></span>
  
    
    



```

url: http://site url/_api/web/lists/GetByTitle('Test')/items(item id)
method: GET
headers:
    
// MS-OFBA protocol return a cookie.
  Cookie: cookie
    accept: "application/json;odata=verbose" or "application/atom+xml"

```

<span data-ttu-id="d1721-176">В следующем XML показывается пример свойств элементов списка, которые возвращаются при вашем запросе типа контента XML.</span><span class="sxs-lookup"><span data-stu-id="d1721-176">The following XML shows an example of the list item properties that are returned when you request the XML content type.</span></span>
  
    
    



```XML

<content type="application/xml">
        <m:properties>
        <d:FileSystemObjectType m:type="Edm.Int32">0</d:FileSystemObjectType>
        <d:Id m:type="Edm.Int32">1</d:Id>
        <d:ID m:type="Edm.Int32">1</d:ID>
        <d:ContentTypeId>0x010049564F321A0F0543BA8C6303316C8C0F</d:ContentTypeId>
        <d:Title>an item</d:Title>
        <d:Modified m:type="Edm.DateTime">2012-07-24T22:47:26Z</d:Modified>
        <d:Created m:type="Edm.DateTime">2012-07-24T22:47:26Z</d:Created>
        <d:AuthorId m:type="Edm.Int32">11</d:AuthorId>
        <d:EditorId m:type="Edm.Int32">11</d:EditorId>
        <d:OData__UIVersionString>1.0</d:OData__UIVersionString>
        <d:Attachments m:type="Edm.Boolean">false</d:Attachments>
        <d:GUID m:type="Edm.Guid">eb6850c5-9a30-4636-b282-234eda8b1057</d:GUID>
    </m:properties>
</content>
```

<span data-ttu-id="d1721-177">В следующем примере показывается, как **создать** элемент списка.</span><span class="sxs-lookup"><span data-stu-id="d1721-177">The following example shows how to **create** a list item.</span></span>
  
> [!NOTE]
> 
> <span data-ttu-id="d1721-178">[!Примечание] Для выполнения этой операции вам необходимо знать свойство **ListItemEntityTypeFullName** списка и передать его как значение **type** в тексте запроса HTTP.</span><span class="sxs-lookup"><span data-stu-id="d1721-178">To do this operation, you must know the **ListItemEntityTypeFullName** property of the list and pass that as the value of **type** in the HTTP request body.</span></span>
  
    
    




```

url: http://site url/_api/web/lists/GetByTitle('Test')/items
method: POST
body: { '__metadata': { 'type': 'SP.Data.TestListItem' }, 'Title': 'Test'}
headers:
    
// MS-OFBA protocol returns a cookie.
  Cookie: cookie
     X-RequestDigest = form digest value
    accept: "application/json;odata=verbose"
    content-type: "application/json;odata=verbose"
    content-length:length of post body
```

<span data-ttu-id="d1721-179">В следующем примере показывается, как **обновить** элемент списка.</span><span class="sxs-lookup"><span data-stu-id="d1721-179">The following example shows how to **update** a list item.</span></span>
  
> [!NOTE]
> <span data-ttu-id="d1721-180">[!Примечание] Для выполнения этой операции вам необходимо знать свойство **ListItemEntityTypeFullName** списка и передать его как значение **type** в тексте запроса HTTP.</span><span class="sxs-lookup"><span data-stu-id="d1721-180">To do this operation, you must know the **ListItemEntityTypeFullName** property of the list and pass that as the value of **type** in the HTTP request body.</span></span>
  
    
    




```

url: http://site url/_api/web/lists/GetByTitle('Test')/items(item id)
method: POST
body: { '__metadata': { 'type': 'SP.Data.TestListItem' }, 'Title': 'TestUpdated'}
headers:
// MS-OFBA protocol returns a cookie.
  Cookie: cookie
     X-RequestDigest = form digest value
    "IF-MATCH": etag or "*"
    "X-HTTP-Method":"MERGE",
    accept: "application/json;odata=verbose"
    content-type: "application/json;odata=verbose"
    content-length:length of post body
```

<span data-ttu-id="d1721-181">В следующем примере показывается, как **удалить** элемент списка.</span><span class="sxs-lookup"><span data-stu-id="d1721-181">The following example shows how to **delete** a list item.</span></span>
  
    
    



```

url: http://site url/_api/web/lists/GetByTitle('Test')/items(item id)
method: POST
headers:
// MS-OFBA protocol returns a cookie.
  Cookie: cookie
     X-RequestDigest = form digest value
    "IF-MATCH": etag or "*"
    "X-HTTP-Method":"DELETE"

```

<span data-ttu-id="d1721-182">Для получения дополнительных сведений см [выполнения базовых операций с помощью конечных точек SharePoint REST](http://msdn.microsoft.com/library/e3000415-50a0-426e-b304-b7de18f2f7d9%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="d1721-182">For more information, see  [Complete basic operations using SharePoint REST endpoints](http://msdn.microsoft.com/library/e3000415-50a0-426e-b304-b7de18f2f7d9%28Office.15%29.aspx).</span></span>
  
    
    

## <a name="see-also"></a><span data-ttu-id="d1721-183">См. также</span><span class="sxs-lookup"><span data-stu-id="d1721-183">See also</span></span>
<span data-ttu-id="d1721-184"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="d1721-184"></span></span>


-  [<span data-ttu-id="d1721-185">Построение приложений Windows Phone, обращающихся к SharePoint</span><span class="sxs-lookup"><span data-stu-id="d1721-185">Build Windows Phone apps that access SharePoint</span></span>](build-windows-phone-apps-that-access-sharepoint.md)
    
  
-  [<span data-ttu-id="d1721-186">С помощью службы SharePoint REST</span><span class="sxs-lookup"><span data-stu-id="d1721-186">Using the SharePoint REST service</span></span>](http://msdn.microsoft.com/library/e1ff2979-1c16-4cb0-a57e-9168dfe20a7c.aspx)
    
  
-  [<span data-ttu-id="d1721-187">Построение приложений Windows Phone, обращающихся к SharePoint</span><span class="sxs-lookup"><span data-stu-id="d1721-187">Build Windows Phone apps that access SharePoint</span></span>](build-windows-phone-apps-that-access-sharepoint.md)
    
  
-  [<span data-ttu-id="d1721-188">Выбор правильного набора API в SharePoint</span><span class="sxs-lookup"><span data-stu-id="d1721-188">Choose the right API set in SharePoint</span></span>](choose-the-right-api-set-in-sharepoint.md)
    
  
-  [<span data-ttu-id="d1721-189">Использование операций запросов OData в запросах REST SharePoint</span><span class="sxs-lookup"><span data-stu-id="d1721-189">Use OData query operations in SharePoint REST requests</span></span>](http://msdn.microsoft.com/library/d4b5c277-ed50-420c-8a9b-860342284b72%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="d1721-190">Знакомство со службой REST в SharePoint</span><span class="sxs-lookup"><span data-stu-id="d1721-190">Get to know the SharePoint REST service</span></span>](http://msdn.microsoft.com/library/2de035a0-ac75-43bd-9665-5c5a59c4c590%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="d1721-191">Выполнение вызовов REST при помощи C# и JavaScript для SharePoint</span><span class="sxs-lookup"><span data-stu-id="d1721-191">Making REST calls with C# and JavaScript for SharePoint</span></span>](http://www.microsoft.com/resources/msdn/en-us/office/media/video/videol?cid=sdc&amp;from=mscomsdc&amp;VideoID=4e4cc094-ff69-405b-852f-2ac7c41293c5)
    
  
-  [<span data-ttu-id="d1721-192">Выполнение вызовов REST при помощи C# и JavaScript для демоверсии SharePoint</span><span class="sxs-lookup"><span data-stu-id="d1721-192">Making REST calls with C# and JavaScript for SharePoint demo</span></span>](http://www.microsoft.com/resources/msdn/en-us/office/media/video/videol?cid=sdc&amp;from=mscomsdc&amp;VideoID=b1e7c9c5-0f62-4a78-bb7b-8e283c86145c)
    
  
-  [<span data-ttu-id="d1721-193">Open Data Protocol</span><span class="sxs-lookup"><span data-stu-id="d1721-193">Open Data Protocol</span></span>](http://www.odata.org/)
    
  
-  [<span data-ttu-id="d1721-194">Авторизация и проверка подлинности для надстроек в SharePoint 2013</span><span class="sxs-lookup"><span data-stu-id="d1721-194">Authorization and authentication of SharePoint Add-ins</span></span>](http://msdn.microsoft.com/library/bde5647a-fff1-4b51-b67b-2139de79ce4a%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="d1721-195">Windows Phone SDK 8.0</span><span class="sxs-lookup"><span data-stu-id="d1721-195">Windows Phone SDK 8.0</span></span>](http://www.microsoft.com/en-us/download/details.aspx?id=35471)
    
  
-  [<span data-ttu-id="d1721-196">Пакет SDK Microsoft SharePoint для Windows Phone 8</span><span class="sxs-lookup"><span data-stu-id="d1721-196">Microsoft SharePoint SDK for Windows Phone 8</span></span>](http://www.microsoft.com/en-us/download/details.aspx?id=36818)
    
  

