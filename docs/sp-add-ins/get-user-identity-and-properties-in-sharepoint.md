# <a name="get-user-identity-and-properties-in-sharepoint"></a><span data-ttu-id="267f9-101">Получение свойств и удостоверения пользователя в SharePoint</span><span class="sxs-lookup"><span data-stu-id="267f9-101">Get user identity and properties in SharePoint</span></span>
<span data-ttu-id="267f9-102">Узнайте, как получить удостоверение пользователя и сведения о нем в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="267f9-102">Learn the different ways to retrieve user identity and user information in SharePoint.</span></span>
 

 <span data-ttu-id="267f9-p101">**Примечание.** Название "приложения для SharePoint" меняется на "надстройки SharePoint". Пока изменения не будут внесены полностью, в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio по-прежнему может встречаться термин "приложение". Дополнительные сведения см. в разделе [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="267f9-p101">The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span></span>
 

<span data-ttu-id="267f9-p102">Существуют разные способы получения удостоверения и сведений о пользователе, в зависимости от сведений, которые требуется получить. В этой статье рассматриваются некоторые способы, с помощью которых это можно сделать.</span><span class="sxs-lookup"><span data-stu-id="267f9-p102">There are different ways to retrieve user identity and information, depending on what information you want to retrieve. This article shows you some of the ways you can accomplish that.</span></span>
 

## <a name="prerequisites-for-retrieving-user-identity-and-properties"></a><span data-ttu-id="267f9-108">Необходимые условия для получения свойств и удостоверения пользователя</span><span class="sxs-lookup"><span data-stu-id="267f9-108">Prerequisites for retrieving user identity and properties</span></span>
<span data-ttu-id="267f9-109"><a name="Prereq"> </a></span><span class="sxs-lookup"><span data-stu-id="267f9-109"></span></span>


- <span data-ttu-id="267f9-110">Подготовьте среду разработки надстроек, как описано в статье [Настройка локальной среды разработки для надстроек SharePoint](set-up-an-on-premises-development-environment-for-sharepoint-add-ins).</span><span class="sxs-lookup"><span data-stu-id="267f9-110">Prepare your add-in development environment as described in  [Set up an on-premises development environment for SharePoint Add-ins](set-up-an-on-premises-development-environment-for-sharepoint-add-ins).</span></span>
    
 
- <span data-ttu-id="267f9-111">Установите Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="267f9-111">Install Visual Studio.</span></span>
    
 
- <span data-ttu-id="267f9-112">Установите последнюю версию [Инструментов разработчика Office для Visual Studio 2013](http://aka.ms/OfficeDevToolsForVS2013) или [Инструментов разработчика Office для Visual Studio 2015](http://aka.ms/OfficeDevToolsForVS2015).</span><span class="sxs-lookup"><span data-stu-id="267f9-112">Install the most recent version of  [Office Developer Tools for Visual Studio 2013](http://aka.ms/OfficeDevToolsForVS2013) or [Office Developer Tools for Visual Studio 2015](http://aka.ms/OfficeDevToolsForVS2015).</span></span>
    
 

 <span data-ttu-id="267f9-113">**Примечание.** Руководство по настройке среды разработки, соответствующей вашим потребностям, см. в статье [Знакомство с созданием надстроек SharePoint с размещением у поставщика](get-started-creating-provider-hosted-sharepoint-add-ins).</span><span class="sxs-lookup"><span data-stu-id="267f9-113">**Note** For guidance on how to setup a development environment that fits your needs, see  [Get started creating provider-hosted SharePoint Add-ins](get-started-creating-provider-hosted-sharepoint-add-ins).</span></span>
 


### <a name="core-concepts-to-know-for-retrieving-user-identity-and-properties"></a><span data-ttu-id="267f9-114">Основные понятия, связанные с получением свойств и удостоверения пользователя</span><span class="sxs-lookup"><span data-stu-id="267f9-114">Core concepts to know for retrieving user identity and properties</span></span>

<span data-ttu-id="267f9-115">В приведенной ниже таблице перечислены некоторые полезные статьи, которые помогут разобраться в понятиях, используемых при создании надстроек SharePoint.</span><span class="sxs-lookup"><span data-stu-id="267f9-115">The following table lists some useful articles that can help you to understand the concepts involved in creating SharePoint Add-ins.</span></span>
 

 


|<span data-ttu-id="267f9-116">**Статья **</span><span class="sxs-lookup"><span data-stu-id="267f9-116">**Article **</span></span>|<span data-ttu-id="267f9-117">**Описание**</span><span class="sxs-lookup"><span data-stu-id="267f9-117">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="267f9-118">Разрешения надстроек в SharePoint</span><span class="sxs-lookup"><span data-stu-id="267f9-118">Add-in permissions in SharePoint</span></span>](add-in-permissions-in-sharepoint-2013)|<span data-ttu-id="267f9-p103">Сведения о разрешениях надстроек SharePoint для работы с SharePoint, включая типы разрешений надстроек, уровни запроса разрешений и управление разрешениями. В этой статье также рассматриваются различия между правами разрешений надстройки и правами пользователя.</span><span class="sxs-lookup"><span data-stu-id="267f9-p103">Learn about SharePoint add-in permissions for working with SharePoint, including types of add-in permissions, permission request scopes, and managing permissions. This article also discusses the differences in add-in permission rights, and user rights.</span></span>|
| [<span data-ttu-id="267f9-121">Поток OAuth маркера контекста для надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="267f9-121">Context Token OAuth flow for SharePoint Add-ins</span></span>](context-token-oauth-flow-for-sharepoint-add-ins)|<span data-ttu-id="267f9-122">Сведения о потоке проверки подлинности и авторизации OAuth для надстроек, размещаемых в облаке.</span><span class="sxs-lookup"><span data-stu-id="267f9-122">Learn about the OAuth authentication and authorization flow for cloud-hosted add-ins.</span></span>|
| [<span data-ttu-id="267f9-123">Знакомство с созданием надстроек SharePoint с размещением у поставщика</span><span class="sxs-lookup"><span data-stu-id="267f9-123">Get started creating provider-hosted SharePoint Add-ins</span></span>](get-started-creating-provider-hosted-sharepoint-add-ins)|<span data-ttu-id="267f9-124">Узнайте, как создавать базовое размещенное у поставщика Надстройка SharePoint с помощью Инструменты разработчика Office для Visual Studio 2012, как взаимодействовать с сайтами Microsoft SharePoint с помощью CSOM (клиентской объектной модели) SharePoint, и как реализовать OAuth в Надстройка SharePoint.</span><span class="sxs-lookup"><span data-stu-id="267f9-124">Learn how to create a basic provider-hosted SharePoint Add-in with the Office Developer Tools for Visual Studio 2012, how to interact with Microsoft SharePoint sites by using the SharePoint CSOM, and how to implement OAuth in a SharePoint Add-in.</span></span>|

## <a name="retrieving-current-website-user-identity"></a><span data-ttu-id="267f9-125">Получение удостоверения текущего пользователя веб-сайта</span><span class="sxs-lookup"><span data-stu-id="267f9-125">Retrieving current website user identity</span></span>
<span data-ttu-id="267f9-126"><a name="WebsiteUserID"> </a></span><span class="sxs-lookup"><span data-stu-id="267f9-126"></span></span>

<span data-ttu-id="267f9-p104">Получить удостоверение текущего пользователя веб-сайта легче всего через объект **Web**. С помощью файла TokenHelper.cs из проекта вы можете получить удостоверение текущего пользователя веб-сайта с помощью приведенного ниже фрагмента кода.</span><span class="sxs-lookup"><span data-stu-id="267f9-p104">The easiest way to retrieve the identity of the current user of the website is via the **Web** object. With the TokenHelper.cs file in your project, you can get the current website user identity using the following code snippet.</span></span>
 

 

```C#
ClientContext clientContext =
                    TokenHelper.GetClientContextWithAccessToken(
                        sharepointUrl.ToString(), accessToken);
 
 
            //Load the properties for the Web object.
            Web web = clientContext.Web;
            clientContext.Load(web);
            clientContext.ExecuteQuery();
 
            //Get the site name.
            siteName = web.Title;
 
            //Get the current user.
            clientContext.Load(web.CurrentUser);
            clientContext.ExecuteQuery();
            currentUser = clientContext.Web.CurrentUser.LoginName;

```


- <span data-ttu-id="267f9-129">Если вы используете Office 365, полученное имя для входа будет примерно таким: `i:0#.f|membership|adam@contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="267f9-129">If you are using Office 365, the login name you get is similar to  `i:0#.f|membership|adam@contoso.com`.</span></span>
    
 
- <span data-ttu-id="267f9-130">Если вы используете Microsoft SharePoint локально, и пользователь вошел как обычный пользователь с помощью NTLM, то полученное имя для входа будет аналогично следующему:  `i:0#.w|contoso\adam`.</span><span class="sxs-lookup"><span data-stu-id="267f9-130">If you are using Microsoft SharePoint on-premises and the user is logged in as a normal user using NTLM, the login name you get is similar to  `i:0#.w|contoso\adam`.</span></span>
    
 
- <span data-ttu-id="267f9-131">Если вы используете локальную среду SharePoint, а пользователь выполняет вход с помощью учетной записи фермы, то будет получено имя для входа `SHAREPOINT\System`.</span><span class="sxs-lookup"><span data-stu-id="267f9-131">If you are using SharePoint on-premises and the user is logged in using a farm account, the login name you get is  `SHAREPOINT\System`.</span></span>
    
 

## <a name="retrieving-user-identity-using-the-resolveprincipal-method"></a><span data-ttu-id="267f9-132">Получение удостоверения пользователя с помощью метода ResolvePrincipal</span><span class="sxs-lookup"><span data-stu-id="267f9-132">Retrieving user identity using the ResolvePrincipal method</span></span>
<span data-ttu-id="267f9-133"><a name="ResolvePrincipal"> </a></span><span class="sxs-lookup"><span data-stu-id="267f9-133"></span></span>

<span data-ttu-id="267f9-p105">Далее приводится другой способ получения имени для входа пользователя. Если у вас есть адрес электронной почты или отображаемое имя пользователя, то для получения его имени для входа можно использовать метод  **ResolvePrincipal** .</span><span class="sxs-lookup"><span data-stu-id="267f9-p105">The following is another way to retrieve user's login name. If you have the user's email address or display name, you can use the  **ResolvePrincipal** method to get the user's login name.</span></span>
 

 

 <span data-ttu-id="267f9-136">**Примечание.** API находятся в пространстве имен Microsoft.SharePoint.Client.Utilities в сборке [Microsoft.SharePoint.Client.dll](http://msdn.microsoft.com/ru-ru/library/microsoft.sharepoint.client.utilities.utility.resolveprincipal.aspx).</span><span class="sxs-lookup"><span data-stu-id="267f9-136">**Note** The APIs are in the Microsoft.SharePoint.Client.Utilities namespace in the  [Microsoft.SharePoint.Client.dll](http://msdn.microsoft.com/ru-ru/library/microsoft.sharepoint.client.utilities.utility.resolveprincipal.aspx) assembly.</span></span>
 

<span data-ttu-id="267f9-137">Ниже представлен пример кода, иллюстрирующей получение данных для входа пользователя.</span><span class="sxs-lookup"><span data-stu-id="267f9-137">The following is sample code to show how to get the user login information.</span></span>
 

 



```C#
ClientResult<Microsoft.SharePoint.Client.Utilities.PrincipalInfo> persons = Microsoft.SharePoint.Client.Utilities.Utility.ResolvePrincipal(clientContext, clientContext.Web, <email>, Microsoft.SharePoint.Client.Utilities.PrincipalType.User, Microsoft.SharePoint.Client.Utilities.PrincipalSource.All, null, true);
                    clientContext.ExecuteQuery();
                    Microsoft.SharePoint.Client.Utilities.PrincipalInfo person = persons.Value;

```

<span data-ttu-id="267f9-138">Значение **Person.LoginName** предоставляет сведения для входа.</span><span class="sxs-lookup"><span data-stu-id="267f9-138">The **Person.LoginName** value gives the login information.</span></span>
 

 

## <a name="retrieving-user-identity-and-profile-properties"></a><span data-ttu-id="267f9-139">Получение удостоверения пользователя и свойств профиля</span><span class="sxs-lookup"><span data-stu-id="267f9-139">Retrieving user identity and profile properties</span></span>
<span data-ttu-id="267f9-140"><a name="Profile"> </a></span><span class="sxs-lookup"><span data-stu-id="267f9-140"></span></span>

<span data-ttu-id="267f9-p106">Если требуется получить удостоверение и свойства пользователя, можно использовать маркер OAuth и API социальных компонентов. Сначала получите маркер OAuth и установите его в контекст клиента. В следующем примере кода показывается, как получить свойства профиля пользователя.</span><span class="sxs-lookup"><span data-stu-id="267f9-p106">If you want to retrieve the user's identity and properties, you can use the OAuth token and the social features APIs. First get the OAuth token and then set it to the client context. The following sample code shows how to get the user profile properties.</span></span>
 

 

```C#

ClientContext clientContext = new ClientContext(<sharepointurl>);
clientContext.AuthenticationMode = ClientAuthenticationMode.Anonymous;
clientContext.FormDigestHandlingEnabled = false;
clientContext.ExecutingWebRequest +=
delegate(object oSender, WebRequestEventArgs webRequestEventArgs)
{                      
    webRequestEventArgs.WebRequestExecutor.RequestHeaders["Authorization"] =
        "Bearer " + accessToken;
};

```

<span data-ttu-id="267f9-144">Затем используйте API **UserProfilesPeopleManager**, чтобы получить свойства пользователя надстройки.</span><span class="sxs-lookup"><span data-stu-id="267f9-144">Then, use the  **UserProfilesPeopleManager** API to get the properties of the user who is using the add-in.</span></span>
 

 



```C#

PeopleManager peopleManager = new PeopleManager(clientContext);
PersonProperties personDetails = peopleManager.GetMyProperties();
clientContext.Load(personDetails, personsD => personsD.AccountName, personsD => personsD.Email,  personsD => personsD.DisplayName);
                clientContext.ExecuteQuery();

```

<span data-ttu-id="267f9-145">Чтобы код работал, должны соблюдаться приведенные ниже условия.</span><span class="sxs-lookup"><span data-stu-id="267f9-145">For the code to work:</span></span>
 

 

- <span data-ttu-id="267f9-146">Необходимо настроить и синхронизировать общую службу профилей пользователей в SharePoint для пользователей.</span><span class="sxs-lookup"><span data-stu-id="267f9-146">The user profile shared service should be configured and synced on SharePoint for the users.</span></span>
    
 
- <span data-ttu-id="267f9-147">Необходимо добавить в манифест надстройки следующий уровень разрешений для социальных компонентов:</span><span class="sxs-lookup"><span data-stu-id="267f9-147">You must add the following permission scope for social features in the add-in manifest:</span></span>
    
```XML
  <AppPermissionRequest Right="Read" Scope="http://sharepoint/social/tenant" />

```

<span data-ttu-id="267f9-148">API находятся в библиотеке Microsoft.SharePoint.Client.UserProfiles.dll.</span><span class="sxs-lookup"><span data-stu-id="267f9-148">The APIs are in Microsoft.SharePoint.Client.UserProfiles.dll.</span></span>
 

 
<span data-ttu-id="267f9-149">Далее приводится еще один пример фрагмента кода, показывающий, как можно получить доступ к хранилищу профилей пользователей.</span><span class="sxs-lookup"><span data-stu-id="267f9-149">The following is another sample code snippet that shows how to access the user profile store.</span></span>
 

 



```C#

ClientContext clientContext; //Create this like you normally would.               
PeopleManager peopleManager = new PeopleManager(clientContext);
PersonProperties myProperties = peopleManager.GetMyProperties();
clientContext.Load(myProperties);
clientContext.ExecuteQuery();

```


## <a name="additional-resources"></a><span data-ttu-id="267f9-150">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="267f9-150">Additional resources</span></span>
<span data-ttu-id="267f9-151"><a name="AdditionalResources"> </a></span><span class="sxs-lookup"><span data-stu-id="267f9-151"></span></span>


-  [<span data-ttu-id="267f9-152">Разрешения надстроек в SharePoint</span><span class="sxs-lookup"><span data-stu-id="267f9-152">Add-in permissions in SharePoint</span></span>](add-in-permissions-in-sharepoint-2013)
    
 
-  [<span data-ttu-id="267f9-153">Поток OAuth маркера контекста для надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="267f9-153">Context Token OAuth flow for SharePoint Add-ins</span></span>](context-token-oauth-flow-for-sharepoint-add-ins)
    
 
-  [<span data-ttu-id="267f9-154">Надстройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="267f9-154">SharePoint Add-ins</span></span>](sharepoint-add-ins)
    
 
-  [<span data-ttu-id="267f9-155">Настройка локальной среды разработки для надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="267f9-155">Set up an on-premises development environment for SharePoint Add-ins</span></span>](set-up-an-on-premises-development-environment-for-sharepoint-add-ins)
    
 
-  [<span data-ttu-id="267f9-156">Знакомство с созданием надстроек SharePoint с размещением у поставщика</span><span class="sxs-lookup"><span data-stu-id="267f9-156">Get started creating provider-hosted SharePoint Add-ins</span></span>](get-started-creating-provider-hosted-sharepoint-add-ins)
    
 

