---
title: "Обзор объектной модели SharePoint мобильного клиента проверки подлинности"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 00ee657f-a32a-495e-80b4-83ac0f60df44
ms.openlocfilehash: c28e4bfd51af86ae91d859432851f31cf4c2b629
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="overview-of-the-sharepoint-mobile-client-authentication-object-model"></a><span data-ttu-id="27e37-102">Обзор объектной модели SharePoint мобильного клиента проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="27e37-102">Overview of the SharePoint mobile client authentication object model</span></span>
<span data-ttu-id="27e37-103">Обзор разработки с помощью проверки подлинности интерфейсы API клиентской объектной модели SharePoint для Silverlight.</span><span class="sxs-lookup"><span data-stu-id="27e37-103">Get an overview of development with the authentication APIs of the SharePoint client object model for Silverlight.</span></span>
## <a name="authentication-and-client-context-on-a-windows-phone"></a><span data-ttu-id="27e37-104">Проверка подлинности и клиентского контекста на ОС Windows Phone</span><span class="sxs-lookup"><span data-stu-id="27e37-104">Authentication and client context on a Windows Phone</span></span>
<span data-ttu-id="27e37-105"><a name="SP15Mobileclientauth_auth"> </a></span><span class="sxs-lookup"><span data-stu-id="27e37-105"></span></span>

<span data-ttu-id="27e37-106">Процесс проверки подлинности пользователя SharePoint на Windows Phone 7.5 немного отличается от тот же самый процесс на клиентском компьютере.</span><span class="sxs-lookup"><span data-stu-id="27e37-106">The process of authenticating a SharePoint user on a Windows Phone 7.5 is a little different from the same process on a client computer.</span></span> <span data-ttu-id="27e37-107">Клиентский код на Windows Phone 7.5 сначала создает объект класса **средства проверки подлинности** или **ODataAuthenticator** класс, который были добавлены в объектную модель SharePointclient для Microsoft Silverlight для Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="27e37-107">Client code on a Windows Phone 7.5 first creates an object of the **Authenticator** class or **ODataAuthenticator** class, which were added to the SharePointclient object model for Microsoft Silverlight for Windows Phone.</span></span> <span data-ttu-id="27e37-108">Затем этот объект используется как учетные данные пользователя.</span><span class="sxs-lookup"><span data-stu-id="27e37-108">It then uses this object as the user's credentials.</span></span>
  
    
    

> <span data-ttu-id="27e37-109">**Примечание:** Дополнительные сведения об API-интерфейсы, описанные в этом разделе можно [Общие сведения о мобильных объектной модели SharePoint](overview-of-the-sharepoint-mobile-object-model.md).</span><span class="sxs-lookup"><span data-stu-id="27e37-109">**Note:** For more information about the APIs that are discussed in this section, see  [Overview of the SharePoint mobile object model](overview-of-the-sharepoint-mobile-object-model.md).</span></span> <span data-ttu-id="27e37-110">Дополнительные сведения о клиентской объектной модели SharePoint для Silverlight см [Управляемой клиентской объектной модели](http://msdn.microsoft.com/en-us/library/ee537247.aspx) и [с помощью объектной модели Silverlight](http://msdn.microsoft.com/en-us/library/ee538971.aspx).</span><span class="sxs-lookup"><span data-stu-id="27e37-110">For more information about the SharePoint client object model for Silverlight, see  [Managed Client Object Model](http://msdn.microsoft.com/en-us/library/ee537247.aspx) and [Using the Silverlight Object Model](http://msdn.microsoft.com/en-us/library/ee538971.aspx).</span></span> 
  
    
    


## <a name="authenticating-the-user-in-the-sharepoint-client-object-model-for-silverlight"></a><span data-ttu-id="27e37-111">Проверка подлинности пользователя в клиентской объектной модели SharePoint для Silverlight</span><span class="sxs-lookup"><span data-stu-id="27e37-111">Authenticating the user in the SharePoint client object model for Silverlight</span></span>
<span data-ttu-id="27e37-112"><a name="SP15Mobileclientauth_user"> </a></span><span class="sxs-lookup"><span data-stu-id="27e37-112"></span></span>

<span data-ttu-id="27e37-113">Ниже приведены действия, необходимые для получения объекта контекста прошедшим проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="27e37-113">The following are the required steps to get an authenticated client context object:</span></span>
  
    
    

1. <span data-ttu-id="27e37-114">Получите объект  [ClientContext](http://msdn.microsoft.com/en-us/library/microsoft.sharepoint.client.clientcontext.aspx) .</span><span class="sxs-lookup"><span data-stu-id="27e37-114">Obtain a  [ClientContext](http://msdn.microsoft.com/en-us/library/microsoft.sharepoint.client.clientcontext.aspx) object.</span></span>
    
  
2. <span data-ttu-id="27e37-115">Создайте новый объект **Authenticator** и инициализация его свойств.</span><span class="sxs-lookup"><span data-stu-id="27e37-115">Construct a new **Authenticator** object and initialize its properties.</span></span>
    
    > <span data-ttu-id="27e37-116">**Примечание:** Можно использовать один объект **проверки подлинности** с помощью только один объект **ClientContext** .</span><span class="sxs-lookup"><span data-stu-id="27e37-116">**Note:** One **Authenticator** object can be used with one **ClientContext** object only.</span></span> <span data-ttu-id="27e37-117">Объект **проверки подлинности** не могут совместно использоваться несколько объектов **ClientContext** с разных URL-адресов.</span><span class="sxs-lookup"><span data-stu-id="27e37-117">You can't share an **Authenticator** object across multiple **ClientContext** objects with different URLs.</span></span>
3. <span data-ttu-id="27e37-118">Класс **Authenticator** реализует интерфейс [ICredentials](http://msdn.microsoft.com/en-us/library/system.net.icredentials.aspx) , поэтому назначить объект свойство [учетные данные](http://msdn.microsoft.com/en-us/library/microsoft.sharepoint.client.clientruntimecontext.credentials.aspx) объекта **ClientContext**.</span><span class="sxs-lookup"><span data-stu-id="27e37-118">The **Authenticator** class implements the [ICredentials](http://msdn.microsoft.com/en-us/library/system.net.icredentials.aspx) interface, so you assign the object to the [Credentials](http://msdn.microsoft.com/en-us/library/microsoft.sharepoint.client.clientruntimecontext.credentials.aspx) property of the **ClientContext** object.</span></span>
    
  
<span data-ttu-id="27e37-119">Затем можно добавить остальную часть вашего кода объектной модели клиента и вызвать **ExecuteQueryAsync**.</span><span class="sxs-lookup"><span data-stu-id="27e37-119">You can then add the rest of your client object model code and call **ExecuteQueryAsync**.</span></span>
  
    
    
<span data-ttu-id="27e37-120">В следующем коде показан следующие действия.</span><span class="sxs-lookup"><span data-stu-id="27e37-120">The following code shows these steps.</span></span>
  
    
    



```cs

ClientContext context = new ClientContext(ListUrl);

// Create an instance of Authenticator object.
Authenticator at = new Authenticator();

// Replace <username> and <password> with valid values. 
at.UserName = "<username>";
at.Password = "<password>";
at.AuthenticationMode = ClientAuthenticationMode.FormsAuthentication;

at.CookieCachingEnabled = true;

// Assign the instance of Authenticator object to the ClientContext.Credential property.
// ClientContext is the object that is central to the client object model for making calls to the server running SharePoint 
// for fetching and updating data.
context.Credentials = at;

ListItemCollection items = context.Web.Lists.GetByTitle(ListName).GetItems(CamlQuery.CreateAllItemsQuery());

// Load the query and execute the request to fetch data.
context.Load(items);
context.ExecuteQueryAsync(
    (object obj, ClientRequestSucceededEventArgs args) =>
    {
// Success logic
    },

    (object obj, ClientRequestFailedEventArgs args) =>
    {
// Failure logic
    });


```

<span data-ttu-id="27e37-121">При необходимости можно указать сервер Unified Access Gateway (UAG) с помощью свойства **Authenticator.UagServerUrl**.</span><span class="sxs-lookup"><span data-stu-id="27e37-121">Optionally, you can specify a Unified Access Gateway (UAG) server by setting the **Authenticator.UagServerUrl** property.</span></span>
  
    
    
<span data-ttu-id="27e37-p104">Если URL-адрес SharePoint поддержка проверки подлинности basic или на основе форм, вызовы **ExecuteQueryAsync** запрашивать у пользователя для входа в систему сведения, как показано на рисунке 1. В противном случае вызов завершится с ошибкой. Включение проверки подлинности basic или на основе форм авторизации на сайте SharePoint избежать ошибки проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="27e37-p104">If the SharePoint URL has basic or forms-based authentication support, the **ExecuteQueryAsync** calls prompt the user for logon information, as shown in Figure 1. Otherwise, the call will fail. Enable basic or forms-based authentication authorization on the SharePoint site to avoid an authentication error.</span></span>
  
    
    

<span data-ttu-id="27e37-125">**На рисунке 1. Проверка подлинности клиента SharePoint**</span><span class="sxs-lookup"><span data-stu-id="27e37-125">**Figure 1. SharePoint client authentication**</span></span>

  
    
    

  
    
    
![SharePointClientAuthentication](../images/SP15Con_SharePointClientAuthenticationFig1.png)
  
    
    
<span data-ttu-id="27e37-p105">Пользователь вводит имя пользователя и пароль и выбирает **Вход в систему**, как показано на рисунке 1. Пользователь имеет возможность выбора **Запомнить мои** установить для имени пользователя и могут выбрать **Сохранить пароль** пароли, как показано на рисунке 1. Когда пользователь имя и пароль запоминается, у пользователя нет введите учетные данные при следующем запуске приложения. **ExecuteQueryAsync** использует вошедшего в систему на учетные данные для выполнения веб-запросов на сервере под управлением SharePoint для извлечения данных.</span><span class="sxs-lookup"><span data-stu-id="27e37-p105">The user enters the user name and password and chooses **Log On**, as shown in Figure 1. The user has the option to choose **Remember me** to remember their user name and has the option to choose **Remember my password** to remember their password, as shown in Figure 1. After the user name or password is remembered, the user doesn't have to enter credentials the next time the app is started. The **ExecuteQueryAsync** then uses the logged on credentials to make web requests to the server running SharePoint to fetch data.</span></span>
  
    
    

## <a name="authenticating-the-user-in-the-sharepoint-odata-object-model"></a><span data-ttu-id="27e37-131">Проверка подлинности пользователя в объектной модели SharePoint OData</span><span class="sxs-lookup"><span data-stu-id="27e37-131">Authenticating the user in the SharePoint OData object model</span></span>
<span data-ttu-id="27e37-132"><a name="SP15Mobileclientauth_OData"> </a></span><span class="sxs-lookup"><span data-stu-id="27e37-132"></span></span>

<span data-ttu-id="27e37-133">Ниже приведены действия, необходимые для получения контекста объекта OData, прошедшего проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="27e37-133">The following are the required steps to get an authenticated OData context object.</span></span>
  
    
    

1. <span data-ttu-id="27e37-134">Создайте новый объект **ODataAuthenticator** и инициализация его свойств.</span><span class="sxs-lookup"><span data-stu-id="27e37-134">Construct a new **ODataAuthenticator** object and initialize its properties.</span></span>
    
  
2. <span data-ttu-id="27e37-135">Зарегистрируйте обработчик для события **AuthenticationCompleted**.</span><span class="sxs-lookup"><span data-stu-id="27e37-135">Register a handler for the **AuthenticationCompleted** event.</span></span>
    
  
3. <span data-ttu-id="27e37-136">Вызовите метод **ODataAuthenticator.Authenticate**, который будет вызвано событие **AuthenticationCompleted**.</span><span class="sxs-lookup"><span data-stu-id="27e37-136">Call the **ODataAuthenticator.Authenticate** method, which will raise the **AuthenticationCompleted** event.</span></span>
    
  
4. <span data-ttu-id="27e37-137">Получите объект контекста OData в обработчике **OnAuthenticationCompleted**.</span><span class="sxs-lookup"><span data-stu-id="27e37-137">Obtain an OData context object inside the **OnAuthenticationCompleted** handler.</span></span>
    
  
<span data-ttu-id="27e37-138">Затем можно добавить вызовов rest вашей OData в обработчике **OnAuthenticationCompleted**.</span><span class="sxs-lookup"><span data-stu-id="27e37-138">You can then add the rest of your OData calls in the **OnAuthenticationCompleted** handler.</span></span>
  
    
    
<span data-ttu-id="27e37-139">В следующем коде показан следующие действия.</span><span class="sxs-lookup"><span data-stu-id="27e37-139">The following code shows these steps.</span></span>
  
    
    



```cs

ODataAuthenticator oat = new ODataAuthenticator();

// Replace <username> and <password> with valid values. 
oat.UserName = "<username>";
oat.Password = "<password>";

oat.AuthenticationMode = ClientAuthenticationMode.FormsAuthentication;


oat.AuthenticationCompleted += 
           new EventHandler<SendingRequestEventArgs>(OnAuthenticationCompleted);

// The Authenticate method will raise the AuthenticationCompleted event.
oat.Authenticate("My_service_URL");  

```

<span data-ttu-id="27e37-140">Также должен реализовывать два обработчика событий, код, как описано в следующем разделе.</span><span class="sxs-lookup"><span data-stu-id="27e37-140">Your code must also implement two event handlers, as described in the following section.</span></span>
  
    
    

### <a name="implementing-the-onauthenticationcompleted-and-onsendingrequest-handlers-and-getting-the-clientcontext-object"></a><span data-ttu-id="27e37-141">Реализация обработчиков OnAuthenticationCompleted и OnSendingRequest и получение объекта ClientContext</span><span class="sxs-lookup"><span data-stu-id="27e37-141">Implementing the OnAuthenticationCompleted and OnSendingRequest handlers and getting the ClientContext object</span></span>

<span data-ttu-id="27e37-p106">Реализация обработчика **OnAuthenticationCompleted** необходимо проверить наличие ошибок при проверке подлинности. Если они существуют, его следует обрабатывать их соответствующим образом, например с сообщением об ошибке пользователю и выйти из режима.</span><span class="sxs-lookup"><span data-stu-id="27e37-p106">An implementation of the **OnAuthenticationCompleted** handler should first check for any errors in the authentication. If there are any, it should handle them appropriately, such as displaying an error message to the user, and then exit.</span></span>
  
    
    
<span data-ttu-id="27e37-p107">Если нет ошибок, обработчик должен создать экземпляр объекта **DataServiceContext** и затем зарегистрировать обработчик для события **SendingRequest**. С этого момента вашей OData, вызов кода запрограммирован объекта **DataServiceContext** так же, как работает на компьютере.</span><span class="sxs-lookup"><span data-stu-id="27e37-p107">If there are no errors, the handler should create an instance of a new **DataServiceContext** object and then register a handler for the **SendingRequest** event. From that point, your OData calling code is programmed against the **DataServiceContext** object just as it is on a computer.</span></span>
  
    
    
<span data-ttu-id="27e37-146">Ниже приведен пример реализации обработчика **OnAuthenticationCompleted**.</span><span class="sxs-lookup"><span data-stu-id="27e37-146">The following is an example of an implementation of an **OnAuthenticationCompleted** handler.</span></span>
  
    
    



```cs

void OnAuthenticationCompleted(object sender, AuthenticationCompletedEventArgs e)
{
    if (e.Error != null)
    {
        MessageBox.Show(error);
        return;
    }
    ODataAuthenticator oat = sender as ODataAuthenticator;

    // Construct an OData context object.
    contextObj = new DataServiceContext(oat.ResolvedUrl);

    // Register the SendingRequest event handler.
    contextObj.SendingRequest += 
        new EventHandler<SendingRequestEventArgs>(OnSendingRequest);  
    
    // Your data retrieval logic goes here. 
    // For example, if there is a GetData method: 
    // contextObj.GetData();   
}


```

<span data-ttu-id="27e37-p108">Все, что **OnSendingRequest** обработчика необходимо лишь имеет значение контейнер файл cookie для объекта **Request** контейнер файл cookie для объекта **ODataAuthenticator**. Ниже приведен пример.</span><span class="sxs-lookup"><span data-stu-id="27e37-p108">All that the **OnSendingRequest** handler needs to do is set the cookie container of the **Request** object to the cookie container of the **ODataAuthenticator** object. The following is an example.</span></span>
  
    
    



```cs

void OnSendingRequest(object sender, SendingRequestEventArgs e)
{ 
    ODataAuthenticator oat = sender as ODataAuthenticator;
    ((HttpWebRequest)e.Request).CookieContainer = oat.CookieContainer;
}

```


## <a name="advanced-usage"></a><span data-ttu-id="27e37-149">Расширенное использование</span><span class="sxs-lookup"><span data-stu-id="27e37-149">Advanced usage</span></span>
<span data-ttu-id="27e37-150"><a name="SP15Mobileclientauth_advance"> </a></span><span class="sxs-lookup"><span data-stu-id="27e37-150"></span></span>


1. <span data-ttu-id="27e37-p109">Можно создать объект **Authenticator** с жестко пользовательская настройка имени и пароля. Пользователь приложения не предлагается ввести имя пользователя и пароль, а жестко учетные данные будут использоваться для проверки подлинности пользователя.</span><span class="sxs-lookup"><span data-stu-id="27e37-p109">You can choose to construct an **Authenticator** object with a hard-coded user name/password option. The user of the app will not be prompted for a user name and password, and hard-coded credentials will be used for authenticating the user.</span></span>
    
     `public Authenticator(string userName, string password)`
    
     `public Authenticator(string userName, string password, string domain)`
    
    <span data-ttu-id="27e37-p110">Же конструктор может использоваться для создания страницы входа в систему. Можно написать на страницу входа в систему путем передачи учетных данных из файлов с выделенным кодом.</span><span class="sxs-lookup"><span data-stu-id="27e37-p110">The same constructor can be used to create a custom logon page. You can write a custom logon page by passing the credentials from code-behind files.</span></span>
    


```cs
  
Authenticator at = new Authenticator();
at.AuthenticationMode = ClientAuthenticationMode.MicrosoftOnline;                          

```

2. <span data-ttu-id="27e37-p111">Тип проверки подлинности можно задать соответствующим образом. По умолчанию используется обычная проверка подлинности.</span><span class="sxs-lookup"><span data-stu-id="27e37-p111">Authentication type can be set accordingly. By default, basic authentication is used.</span></span>
    
  

### <a name="authenticating-against-sharepoint-online"></a><span data-ttu-id="27e37-157">Проверка подлинности в SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="27e37-157">Authenticating against SharePoint Online</span></span>

<span data-ttu-id="27e37-p112">Для проверки подлинности URL-адрес SharePoint Online, присвойте свойству **AuthenticationMode** объекта **Authenticator** в режим **MicrosoftOnline**. Остальные действия, описанные в процедуре такие же, как для URL-адреса локального SharePoint.</span><span class="sxs-lookup"><span data-stu-id="27e37-p112">To authenticate against a SharePoint Online URL, set the **AuthenticationMode** property of the **Authenticator** object to **MicrosoftOnline** mode. The remaining steps in the procedure are the same as those for an on-premises SharePoint URL.</span></span>
  
    
    

> <span data-ttu-id="27e37-160">**Примечание:** Имя пользователя и пароль не может быть жестко для SharePoint Online.The, пользователю предлагается ввести учетные данные для входа.</span><span class="sxs-lookup"><span data-stu-id="27e37-160">**Note:** The user name and password cannot be hard-coded for SharePoint Online.The user will be prompted for logon credentials.</span></span> 
  
    
    


#### <a name="federation-authentication"></a><span data-ttu-id="27e37-161">Проверка подлинности федерации</span><span class="sxs-lookup"><span data-stu-id="27e37-161">Federation Authentication</span></span>

 <span data-ttu-id="27e37-p113">Свойство **FederationAuthURI** используется для передачи **ADFS** предпочтений схемы проверки подлинности, где, **ADFS** настроен для использования нескольких обработчиков проверки подлинности. **FederationAuthURI** указывает тип проверки подлинности, необходимые для запросов проверки подлинности, используется проверка подлинности SharePoint Online с федерацией. Этот параметр может переопределять значение приоритета, заданные в порядке, в котором настроены обработчики проверки подлинности. Чтобы узнать больше о обработчик проверки подлинности, обратитесь к разделу [Обзор проверки подлинности обработчик](http://msdn.microsoft.com/en-us/library/ee895365.aspx).</span><span class="sxs-lookup"><span data-stu-id="27e37-p113">**FederationAuthURI** property is used to pass **ADFS** authentication scheme preference where, **ADFS** is configured to use multiple authentication handlers. **FederationAuthURI** specifies the type of authentication required by Authentication request when, SharePoint Online authentication is used with Federation. This parameter can override the priority established by the order in which authentication handlers are configured. To know more about Authentication handler, see [Authentication Handler Overview](http://msdn.microsoft.com/en-us/library/ee895365.aspx).</span></span>
  
    
    

```cs

 Authenticator auth = new Authenticator("domain\\\\name", "xyz"); 
 auth.FederationPassiveAuthUri = "urn:oasis:names:tc:SAML:2.0:ac:classes:Password"; 
//Replace <SiteUrl> with valid value 
ClientContext ctx = new ClientContext("SiteUrl"); 
               ctx.Credentials = auth; 
               ctx.ExecuteQueryAsync( 
 (object sender, ClientRequestSucceededEventArgs args) => 
   { 
    /* successful callback code */ 
   }, 
 (object sender, ClientRequestFailedEventArgs args) => 
   { 
   /* failure callback code */ 
  });

```

 <span data-ttu-id="27e37-p114">**ADFS**  это необязательное свойство, который будет действовать только при использовании с помощью Microsoft SharePoint Online. С помощью **ADFS** проверка подлинности с помощью других схемы проверки подлинности не оказывает никакого влияния. С помощью Microsoft SharePoint online, если не указано **ADFS** затем схемы по умолчанию будет использоваться, то есть настройки сервера.</span><span class="sxs-lookup"><span data-stu-id="27e37-p114">**ADFS** is an optional property which will be effective only when it is used with Microsoft SharePoint Online. Using **ADFS** authentication with any other authentication scheme will not have any effect. With Microsoft SharePoint online, if **ADFS** is not set then default scheme will be used, i.e. server preference.</span></span>
  
    
    

## <a name="cookie-caching"></a><span data-ttu-id="27e37-169">Кэширование файлов cookie</span><span class="sxs-lookup"><span data-stu-id="27e37-169">Cookie caching</span></span>
<span data-ttu-id="27e37-170"><a name="SP15Mobileclientauth_cookie"> </a></span><span class="sxs-lookup"><span data-stu-id="27e37-170"></span></span>

<span data-ttu-id="27e37-171">Класс **проверки подлинности** также включает в себя элементы, которые можно использовать для включения и управления кэширование файлов cookie или учетные данные.</span><span class="sxs-lookup"><span data-stu-id="27e37-171">The **Authenticator** class also includes members that you can use to enable and manage caching of cookies or credentials or both.</span></span> <span data-ttu-id="27e37-172">Сведения о этих членов класса **проверки подлинности** и способам их использования содержатся [Общие сведения о мобильных объектной модели SharePoint](overview-of-the-sharepoint-mobile-object-model.md).</span><span class="sxs-lookup"><span data-stu-id="27e37-172">For information about these members of the **Authenticator** class and their uses, see [Overview of the SharePoint mobile object model](overview-of-the-sharepoint-mobile-object-model.md).</span></span>
  
    
    

## <a name="additional-resources"></a><span data-ttu-id="27e37-173">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="27e37-173">Additional resources</span></span>
<span data-ttu-id="27e37-174"><a name="SP15Mobileclientauth_addlresources"> </a></span><span class="sxs-lookup"><span data-stu-id="27e37-174"></span></span>


-  [<span data-ttu-id="27e37-175">Построение приложений Windows Phone, обращающихся к SharePoint</span><span class="sxs-lookup"><span data-stu-id="27e37-175">Build Windows Phone apps that access SharePoint</span></span>](build-windows-phone-apps-that-access-sharepoint.md)
    
  
-  [<span data-ttu-id="27e37-176">Обзор мобильных устройств объектной модели SharePoint</span><span class="sxs-lookup"><span data-stu-id="27e37-176">Overview of the SharePoint mobile object model</span></span>](overview-of-the-sharepoint-mobile-object-model.md)
    
  

