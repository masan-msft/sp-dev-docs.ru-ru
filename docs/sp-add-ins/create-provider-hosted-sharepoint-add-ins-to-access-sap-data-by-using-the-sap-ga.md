# <a name="create-provider-hosted-sharepoint-add-ins-to-access-sap-data-by-using-the-sap-gateway-for-microsoft"></a><span data-ttu-id="38bc8-101">Создание надстроек SharePoint, размещенных у поставщика, для доступа к данным SAP с помощью шлюза SAP для Майкрософт</span><span class="sxs-lookup"><span data-stu-id="38bc8-101">Create provider-hosted SharePoint Add-ins to access SAP data by using the SAP Gateway for Microsoft</span></span>
<span data-ttu-id="38bc8-102">Узнайте, как создать надстройку SharePoint, имеющую доступ к данным SAP.</span><span class="sxs-lookup"><span data-stu-id="38bc8-102">Learn how you can build an spappsing that can access SAP data.</span></span>
 

 <span data-ttu-id="38bc8-p101">**Примечание.** В настоящее время идет процесс замены названия "приложения для SharePoint" названием "надстройки SharePoint". Во время этого процесса в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio может по-прежнему использоваться термин "приложения для SharePoint". Дополнительные сведения см. в статье [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="38bc8-p101">The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span></span>
 

<span data-ttu-id="38bc8-p102">Вы можете создать надстройку SharePoint, которая считывает и записывает данные SAP, а при необходимости и данные SharePoint, с помощью шлюза SAP для Майкрософт и библиотеки аутентификации Azure AD для .NET. В этой статье описано, как создать надстройку SharePoint для получения авторизованного доступа к SAP.</span><span class="sxs-lookup"><span data-stu-id="38bc8-p102">Learn how you can build a SharePoint Add-in that can access SAP data. You can create a SharePoint Add-in that reads and writes SAP data, and optionally reads and writes SharePoint data, by using SAP Gateway for Microsoft and the Azure AD Authentication Library for .NET. This article provides the procedures for how you can design the SharePoint Add-in to get authorized access to SAP.</span></span> 
 

## <a name="before-you-begin"></a><span data-ttu-id="38bc8-108">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="38bc8-108">Before you begin</span></span>

<span data-ttu-id="38bc8-109">Ниже перечислены компоненты, необходимые для выполнения процедур, которые описаны в этой статье.</span><span class="sxs-lookup"><span data-stu-id="38bc8-109">The following are prerequisites to the procedures in this article:</span></span>
 

 

-  <span data-ttu-id="38bc8-p103">**Сайт разработчиков Office 365** это домен Office 365, связанный с подпиской Microsoft Azure Active Directory. См. статью [Настройка среды для разработки надстроек SharePoint в Office 365](set-up-a-development-environment-for-sharepoint-add-ins-on-office-365) или [Создание сайта разработчика с использованием актуальной подписки на Office 365](create-a-developer-site-on-an-existing-office-365-subscription).</span><span class="sxs-lookup"><span data-stu-id="38bc8-p103">**An Office 365 Developer Site** in an Office 365 domain that is associated with a Microsoft Azure Active Directory subscription. See [Set up a development environment for SharePoint Add-ins on Office 365](set-up-a-development-environment-for-sharepoint-add-ins-on-office-365) or [Create a developer site on an existing Office 365 subscription](create-a-developer-site-on-an-existing-office-365-subscription).</span></span>
    
 
-  <span data-ttu-id="38bc8-112">Среда **Visual Studio 2013 c обновлением 2** или более поздней версии, которую вы можете получить в статье [Вас приветствует Visual Studio 2013](http://msdn.microsoft.com/library/dd831853.aspx).</span><span class="sxs-lookup"><span data-stu-id="38bc8-112">**Visual Studio 2013 Update 2** or later, which you can obtain from [Welcome to Visual Studio 2013](http://msdn.microsoft.com/library/dd831853.aspx).</span></span>
    
 
-  <span data-ttu-id="38bc8-p104">**Инструменты разработчика Microsoft Office для Visual Studio**. Версия, включенная в обновление 2 для Visual Studio 2013 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="38bc8-p104">**Microsoft Office Developer Tools for Visual Studio**. The version that is included in Update 2 of Visual Studio 2013 or later.</span></span>
    
 
-  <span data-ttu-id="38bc8-p105">**Шлюз SAP для Майкрософт**, развернутый и настроенный в Microsoft Azure. Дополнительные сведения см. в документации к [шлюзу SAP для Майкрософт](http://go.microsoft.com/fwlink/?LinkId=507635).</span><span class="sxs-lookup"><span data-stu-id="38bc8-p105">**SAP Gateway for Microsoft** is deployed and configured in Microsoft Azure. See the documentation for [SAP Gateway for Microsoft](http://go.microsoft.com/fwlink/?LinkId=507635).</span></span>
    
 
-  <span data-ttu-id="38bc8-p106">**Учетная запись организации в Microsoft Azure**. См. раздел [Регистрация приложения в Azure AD вручную для доступа к интерфейсам API Office 365](http://msdn.microsoft.com/library/95479f73-15d7-426e-abdf-ae2c72b5cd33%28Office.15%29.aspx#bk_CreateOrganizationAccount).</span><span class="sxs-lookup"><span data-stu-id="38bc8-p106">**An organizational account in Microsoft Azure**. See  [Manually register your app with Azure AD so it can access Office 365 APIs](http://msdn.microsoft.com/library/95479f73-15d7-426e-abdf-ae2c72b5cd33%28Office.15%29.aspx#bk_CreateOrganizationAccount).</span></span>
    
     <span data-ttu-id="38bc8-119">**Примечание.** Войдите в свою учетную запись Office 365 (login.microsoftonline.com), чтобы изменить временный пароль после создания учетной записи.</span><span class="sxs-lookup"><span data-stu-id="38bc8-119">**Note** Login to your Office 365 account (login.microsoftonline.com) to change the temporary password after the account is created.</span></span>
-  <span data-ttu-id="38bc8-p107">**Конечная точка OData для SAP** с примером данных. См. документацию к [шлюзу SAP для Майкрософт](http://go.microsoft.com/fwlink/?LinkId=507635).</span><span class="sxs-lookup"><span data-stu-id="38bc8-p107">**A SAP OData endpoint** with sample data in it. See the documentation for [SAP Gateway for Microsoft](http://go.microsoft.com/fwlink/?LinkId=507635).</span></span>
    
 
-  <span data-ttu-id="38bc8-p108">**Общее представление об Azure AD.** См. статью [Начало работы с Azure AD](http://msdn.microsoft.com/library/azure/dn655157.aspx).</span><span class="sxs-lookup"><span data-stu-id="38bc8-p108">**A basic familiarity with Azure AD.** See [Getting started with Azure AD](http://msdn.microsoft.com/library/azure/dn655157.aspx).</span></span>
    
 
-  <span data-ttu-id="38bc8-p109">**Общее представление о надстройках SharePoint.** См. статью [Знакомство с созданием надстроек SharePoint с размещением у поставщика](get-started-creating-provider-hosted-sharepoint-add-ins).</span><span class="sxs-lookup"><span data-stu-id="38bc8-p109">**A basic familiarity with creating SharePoint Add-ins.** See [Get started creating provider-hosted SharePoint Add-ins](get-started-creating-provider-hosted-sharepoint-add-ins).</span></span>
    
 
-  <span data-ttu-id="38bc8-p110">**Общее представление об OAuth 2.0 в Azure AD**. См. статью [Авторизация доступа к веб-приложениям с помощью OAuth 2.0 и Azure Active Directory](http://msdn.microsoft.com/library/azure/dn645545.aspx) и ее дочерних статей.</span><span class="sxs-lookup"><span data-stu-id="38bc8-p110">**A basic familiarity OAuth 2.0 in Azure AD**. See  [OAuth 2.0 in Azure AD](http://msdn.microsoft.com/library/azure/dn645545.aspx) and its child topics.</span></span>
    
 
 <span data-ttu-id="38bc8-128">**Пример кода.** [SharePoint: использование шлюза SAP для Майкрософт в надстройке SharePoint](http://code.msdn.microsoft.com/SharePoint-2013-Using-the-0931abce)</span><span class="sxs-lookup"><span data-stu-id="38bc8-128">**Code sample:** [SharePoint: Using the SAP Gateway to Microsoft in a SharePoint Add-in](http://code.msdn.microsoft.com/SharePoint-2013-Using-the-0931abce)</span></span>
 

 

## <a name="understand-authentication-and-authorization-to-sap-gateway-for-microsoft-and-sharepoint"></a><span data-ttu-id="38bc8-129">Общие сведения о проверке подлинности и авторизации в шлюзе SAP для Майкрософт и SharePoint</span><span class="sxs-lookup"><span data-stu-id="38bc8-129">Understand authentication and authorization to SAP Gateway for Microsoft and SharePoint</span></span>
<span data-ttu-id="38bc8-130"><a name="AuthOverview"> </a></span><span class="sxs-lookup"><span data-stu-id="38bc8-130"></span></span>

<span data-ttu-id="38bc8-p111">OAuth 2.0 в Azure AD позволяет приложениям получать доступ к различным ресурсам, размещенным в Microsoft Azure, например Шлюз SAP для Майкрософт. В OAuth 2.0 приложения и пользователи субъекты безопасности. Субъектам приложений, как и пользователям (а иногда и вместо пользователей), требуется аутентификация и авторизация на защищенных ресурсах. В этом процессе участвует поток OAuth, в котором приложение (например, Надстройка SharePoint) получает маркеры доступа и обновления. Первый из двух маркеров принимают все службы и приложения, размещенные в Microsoft Azure и использующие Azure AD в качестве сервера авторизации OAuth 2.0. Этот процесс во многом аналогичен тому, как удаленные компоненты размещенного у поставщика приложения для SharePoint авторизируются в SharePoint (см. статью  [Создание надстроек для SharePoint, которые используют авторизацию с низким уровнем доверия](creating-sharepoint-add-ins-that-use-low-trust-authorization) и ее подразделы). Однако система авторизации для контроля доступа использует в качестве доверенного поставщика маркеров Служба контроля доступа Microsoft Azure (ACS), а не Azure AD.</span><span class="sxs-lookup"><span data-stu-id="38bc8-p111">OAuth 2.0 in Azure AD enables applications to access multiple resources hosted by Microsoft Azure and SAP Gateway for Microsoft is one of them. With OAuth 2.0, applications, in addition to users, are security principals. Application principals require authentication and authorization to protected resources in addition to (and sometimes instead of) users. The process involves an OAuth "flow" in which the application, which can be a SharePoint Add-in, obtains an access token (and refresh token) that is accepted by all of the Microsoft Azure-hosted services and applications that are configured to use Azure AD as an OAuth 2.0 authorization server. The process is very similar to the way that the remote components of a provider-hosted SharePoint Add-in gets authorization to SharePoint as described in  [Creating SharePoint Add-ins that use low-trust authorization](creating-sharepoint-add-ins-that-use-low-trust-authorization) and its child articles. However, the ACS authorization system uses Microsoft Azure Access Control Service (ACS) as the trusted token issuer rather than Azure AD.</span></span>
 

 

 <span data-ttu-id="38bc8-p112">**Совет.** Если надстройка SharePoint получает доступ не только к шлюзу SAP для Майкрософт, но и к SharePoint, то ей потребуется использовать *обе* системы: Azure AD, чтобы получить маркер доступа к шлюзу SAP для Майкрософт, и систему авторизации ACS для получения маркера доступа к SharePoint. Маркеры из этих двух источников не являются взаимозаменяемыми. Дополнительные сведения см. в разделе [(Необязательно) Предоставление приложению ASP.NET доступа к SharePoint](#SharePoint).</span><span class="sxs-lookup"><span data-stu-id="38bc8-p112">**TIP** If your SharePoint Add-in accesses SharePoint in addition to accessing SAP Gateway for Microsoft, then it will need to use  *both*  systems: Azure AD to get an access token to SAP Gateway for Microsoft and the ACS authorization system to get an access token to SharePoint. The tokens from the two sources are not interchangeable. For more information, see [Optionally, add SharePoint access to the ASP.NET application](#SharePoint).</span></span>
 

<span data-ttu-id="38bc8-p113">Подробное описание и схему потока OAuth, используемого протоколом OAuth 2.0 в Azure AD, см. в статье  [Поток предоставления кода авторизации](http://msdn.microsoft.com/library/azure/dn645542.aspx). Похожее описание и схему потока доступа к SharePoint см. в статье  [Этапы потока маркеров контекста](context-token-oauth-flow-for-sharepoint-add-ins#OAuth_ProcessFlowSteps).</span><span class="sxs-lookup"><span data-stu-id="38bc8-p113">For a detailed description and diagram of the OAuth flow used by OAuth 2.0 in Azure AD, see  [Authorization Code Grant Flow](http://msdn.microsoft.com/library/azure/dn645542.aspx). (For a similar description, and a diagram, of the flow for accessing SharePoint, see  [See the steps in the Context Token flow](context-token-oauth-flow-for-sharepoint-add-ins#OAuth_ProcessFlowSteps).)</span></span>
 

 

## <a name="create-the-sharepoint-add-in"></a><span data-ttu-id="38bc8-142">Создание надстройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="38bc8-142">Create the SharePoint Add-in</span></span>
<span data-ttu-id="38bc8-143"><a name="AuthOverview"> </a></span><span class="sxs-lookup"><span data-stu-id="38bc8-143"></span></span>


### <a name="create-the-visual-studio-solution"></a><span data-ttu-id="38bc8-144">Создание решения Visual Studio</span><span class="sxs-lookup"><span data-stu-id="38bc8-144">Create the Visual Studio solution</span></span>


1. <span data-ttu-id="38bc8-p114">Чтобы создать проект **Надстройка SharePoint** в Visual Studio, выполните указанные ниже действия. В примере из этой статьи используется язык C#, но вы также можете создать проект надстройки SharePoint с помощью раздела **Visual Basic** шаблонов нового проекта.</span><span class="sxs-lookup"><span data-stu-id="38bc8-p114">Create an **SharePoint Add-in** project in Visual Studio with the following steps. (The continuing example in this article assumes you are using C#; but you can start a SharePoint Add-in project in the **Visual Basic** section of the new project templates as well.)</span></span>
    
      1. <span data-ttu-id="38bc8-p115">В **мастере создания надстройки SharePoint** укажите имя проекта и нажмите кнопку **ОК**. В нашем примере используется SAP2SharePoint.</span><span class="sxs-lookup"><span data-stu-id="38bc8-p115">In the **New SharePoint Add-in** wizard, name the project and click **OK**. For the continuing example, use SAP2SharePoint.</span></span>
    
 
  2. <span data-ttu-id="38bc8-p116">Укажите URL-адрес домена сайта разработчика для Office 365 (включая косую черту в конце) в качестве сайта отладки. Пример: https://<домен_O365>.sharepoint.com/. Выберите тип надстройки **Размещено у поставщика**. Нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="38bc8-p116">Specify the domain URL of your Office 365 Developer Site (including a final forward slash) as the debugging site; for example, https://<O365_domain>.sharepoint.com/. Specify **Provider-hosted** as the add-in type. Click **Next**.</span></span>
    
 
  3. <span data-ttu-id="38bc8-p117">Выберите тип проекта. В нашем примере используется тип **Приложение веб-форм ASP.NET**. Вы также можете создавать приложения на основе ASP.NET и MVC, которые получают доступ к шлюзу SAP для Майкрософт. Нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="38bc8-p117">Choose a project type. For the continuing example, choose **ASP.NET Web Forms Application**. (You can also make ASP.NET MVC applications that access SAP Gateway for Microsoft.) Click **Next**.</span></span>
    
 
  4. <span data-ttu-id="38bc8-p118">Выберите Azure ACS в качестве системы аутентификации. Надстройка SharePoint будет использовать эту систему при доступе к SharePoint. Она не используется при доступе к шлюзу SAP для Майкрософт. Нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="38bc8-p118">Choose Azure ACS as the authentication system. (Your SharePoint Add-in will use this system if it accesses SharePoint. It does not use this system when it accesses SAP Gateway for Microsoft.) Click **Finish**.</span></span>
    
 
2. <span data-ttu-id="38bc8-p119">После создания проекта, вам будет предложено войти в учетную запись Office 365. Используйте учетные данные администраторы учетных записей, например Bob@<домен_O365>.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="38bc8-p119">After the project is created, you are prompted to login to the Office 365 account. Use the credentials of an account administrator; for example Bob@<O365_domain>.onmicrosoft.com.</span></span>
    
 
3. <span data-ttu-id="38bc8-p120">Решение Visual Studio содержит два проекта: основной проект надстройки SharePoint и проект веб-форм ASP.NET. Добавьте пакет **Библиотека аутентификации Active Directory** (ADAL) к проекту ASP.NET, выполнив указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="38bc8-p120">There are two projects in the Visual Studio solution; the SharePoint Add-in proper project and an ASP.NET web forms project. Add the **Active Directory Authentication Library** (ADAL) package to the ASP.NET project with these steps:</span></span>
    
      1. <span data-ttu-id="38bc8-162">Щелкните правой кнопкой мыши папку **Ссылки** проекта ASP.NET (в приведенном примере он называется **SAP2SharePointWeb**) и выберите команду **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="38bc8-162">Right-click the **References** folder in the ASP.NET project (named **SAP2SharePointWeb** in the continuing example) and select **Manage NuGet Packages**.</span></span> 
    
 
  2. <span data-ttu-id="38bc8-p121">В левой части открывшегося диалогового окна выберите пункт **В сети**. Введите в поле поиска запрос Microsoft.IdentityModel.Clients.ActiveDirectory.</span><span class="sxs-lookup"><span data-stu-id="38bc8-p121">In the dialog that opens, select **Online** on the left. EnterMicrosoft.IdentityModel.Clients.ActiveDirectory in the search box.</span></span>
    
 
  3. <span data-ttu-id="38bc8-165">Когда в результатах поиска появится библиотека ADAL, нажмите кнопку **Установить** рядом с ней и примите условия лицензионного соглашения.</span><span class="sxs-lookup"><span data-stu-id="38bc8-165">When the ADAL library appears in the search results, click the **Install** button beside it, and accept the license when prompted.</span></span>
    
 
4. <span data-ttu-id="38bc8-166">Добавьте пакет Json.net в проект ASP.NET, выполнив указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="38bc8-166">Add the Json.net package to the ASP.NET project with these steps:</span></span>
    
      1. <span data-ttu-id="38bc8-p122">Введите запрос Json.net в поле поиска. Если появится слишком много результатов, выполните поиск по запросу Newtonsoft.json.</span><span class="sxs-lookup"><span data-stu-id="38bc8-p122">Enter Json.net in the search box. If this produces too many hits, try searching onNewtonsoft.json.</span></span>
    
 
  2. <span data-ttu-id="38bc8-169">Когда в результатах поиска появится библиотека Json.net, нажмите кнопку **Установить** рядом с этим пунктом.</span><span class="sxs-lookup"><span data-stu-id="38bc8-169">When Json.net appears in the search results, click the **Install** button beside it.</span></span>
    
 
5. <span data-ttu-id="38bc8-170">Нажмите кнопку **Закрыть**.</span><span class="sxs-lookup"><span data-stu-id="38bc8-170">Click **Close**.</span></span>
    
 

### <a name="register-your-web-application-with-azure-ad"></a><span data-ttu-id="38bc8-171">Регистрация веб-приложения в Azure AD</span><span class="sxs-lookup"><span data-stu-id="38bc8-171">Register your web application with Azure AD</span></span>


1. <span data-ttu-id="38bc8-172">Войдите на [портал управления Azure](https://manage.windowsazure.com), используя учетную запись администратора Azure.</span><span class="sxs-lookup"><span data-stu-id="38bc8-172">Login into the  [Azure Management portal](https://manage.windowsazure.com) with your Azure administrator account.</span></span>
    
     <span data-ttu-id="38bc8-173">**Примечание.** Из соображений безопасности не рекомендуется использовать учетную запись администратора при разработке надстроек.</span><span class="sxs-lookup"><span data-stu-id="38bc8-173">**Note** For security purposes, we recommend against using an administrator account when developing add-ins.</span></span>
2. <span data-ttu-id="38bc8-174">Выберите **Active Directory** в левой части страницы.</span><span class="sxs-lookup"><span data-stu-id="38bc8-174">Choose **Active Directory** on the left side.</span></span>
    
 
3. <span data-ttu-id="38bc8-175">Щелкните каталог.</span><span class="sxs-lookup"><span data-stu-id="38bc8-175">Click on your directory.</span></span> 
    
 
4. <span data-ttu-id="38bc8-176">Выберите **ПРИЛОЖЕНИЯ** (на верхней панели навигации).</span><span class="sxs-lookup"><span data-stu-id="38bc8-176">Choose **APPLICATIONS** (on the top navigation bar).</span></span>
    
 
5. <span data-ttu-id="38bc8-177">На панели инструментов в нижней части экрана нажмите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="38bc8-177">Choose **Add** on the toolbar at the bottom of the screen.</span></span>
    
 
6. <span data-ttu-id="38bc8-178">В открывшемся диалоговом окне выберите **Добавить приложение, разрабатываемое моей организацией**.</span><span class="sxs-lookup"><span data-stu-id="38bc8-178">On the dialog that opens, choose **Add an application my organization is developing**.</span></span>
    
 
7. <span data-ttu-id="38bc8-p123">В диалоговом окне **ДОБАВЛЕНИЕ ПРИЛОЖЕНИЯ** укажите имя приложения. В нашем примере используется имя ContosoAutomobileCollection.</span><span class="sxs-lookup"><span data-stu-id="38bc8-p123">On the **ADD APPLICATION** dialog, give the application a name. For the continuing example, useContosoAutomobileCollection.</span></span> 
    
 
8. <span data-ttu-id="38bc8-181">Выберите тип приложения **Веб-приложение и/или веб-API** и нажмите стрелку вправо.</span><span class="sxs-lookup"><span data-stu-id="38bc8-181">Choose **Web Application And/Or Web API** as the application type, and then click the right arrow button.</span></span>
    
 
9. <span data-ttu-id="38bc8-p124">На второй странице диалогового окна укажите URL-адрес отладки SSL из проекта ASP.NET решения Visual Studio в поле **URL-АДРЕС ВХОДА**. Ниже описано, как определить URL-адрес. ***Для начала необходимо зарегистрировать надстройку с URL-адресом отладки, чтобы иметь возможность запускать отладчик Visual Studio (клавиша F5). После этого надстройку можно будет зарегистрировать с URL-адресом промежуточного веб-сайта Azure. См. раздел [Изменение и подготовка надстройки в Azure и Office 365](#Stage).***</span><span class="sxs-lookup"><span data-stu-id="38bc8-p124">On the second page of the dialog, use the SSL debugging URL from the ASP.NET project in the Visual Studio solution as the **SIGN-ON URL**. You can find the URL using the following steps. ***(You need to register the add-in initially with the debugging URL so that you can run the Visual Studio debugger (F5). When your add-in is ready for staging, you will re-register it with its staging Azure Web Site URL.  [Modify the add-in and stage it to Azure and Office 365](#Stage).)***</span></span>
    
      1. <span data-ttu-id="38bc8-185">Выделите проект ASP.NET в **обозревателе решений**.</span><span class="sxs-lookup"><span data-stu-id="38bc8-185">Highlight the ASP.NET project in **Solution Explorer**.</span></span> 
    
 
  2. <span data-ttu-id="38bc8-p125">В окне **Свойства** скопируйте значение свойства **URL-адрес SSL**. Пример: https://localhost:44300/.</span><span class="sxs-lookup"><span data-stu-id="38bc8-p125">In the **Properties** window, copy the value of the **SSL URL** property. An example ishttps://localhost:44300/.</span></span>
    
 
  3. <span data-ttu-id="38bc8-188">Вставьте его в поле **URL-АДРЕС ВХОДА** диалогового окна **ДОБАВЛЕНИЕ ПРИЛОЖЕНИЯ**.</span><span class="sxs-lookup"><span data-stu-id="38bc8-188">Paste it into the **SIGN-ON URL** on the **ADD APPLICATION** dialog.</span></span>
    
 
10. <span data-ttu-id="38bc8-189">В качестве **URI ИДЕНТИФИКАТОРА ПРИЛОЖЕНИЯ** укажите уникальный URI, например имя приложения, добавленное к URL-адресу SSL: https://localhost:44300/ContosoAutomobileCollection.</span><span class="sxs-lookup"><span data-stu-id="38bc8-189">For the **APP ID URI**, give the application a unique URI, such as the application name appended to the end of the SSL URL; for example https://localhost:44300/ContosoAutomobileCollection.</span></span>
    
 
11. <span data-ttu-id="38bc8-p126">Нажмите кнопку с флажком. Откроется информационная панель Azure для приложения с сообщением об успешном выполнении операции.</span><span class="sxs-lookup"><span data-stu-id="38bc8-p126">Click the checkmark button. The Azure dashboard for the application opens with a success message.</span></span>
    
 
12. <span data-ttu-id="38bc8-192">Выберите пункт **НАСТРОЙКА** в верхней части страницы.</span><span class="sxs-lookup"><span data-stu-id="38bc8-192">Choose **CONFIGURE** on the top of the page.</span></span>
    
 
13. <span data-ttu-id="38bc8-p127">Найдите **ИДЕНТИФИКАТОР КЛИЕНТА** и скопируйте его. Он понадобится позже.</span><span class="sxs-lookup"><span data-stu-id="38bc8-p127">Scroll to the **CLIENT ID** and make a copy of it. You will need it for a later procedure.</span></span>
    
 
14. <span data-ttu-id="38bc8-p128">Создайте ключ в разделе **Ключи**. Он появится не сразу. Нажмите кнопку **СОХРАНИТЬ** в нижней части страницы, и ключ станет видимым. Скопируйте его, так как он понадобится позже.</span><span class="sxs-lookup"><span data-stu-id="38bc8-p128">In the **keys** section, create a key. It won't appear initially. Click **SAVE** at the bottom of the page and the key will be visible. Make a copy of it. You will need it for a later procedure.</span></span>
    
 
15. <span data-ttu-id="38bc8-200">Прокрутите вниз до раздела **Разрешения для других приложений** и выберите свое приложение-службу шлюза SAP для Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="38bc8-200">Scroll to **permissions to other applications** and select your SAP Gateway for Microsoft service application.</span></span>
    
 
16. <span data-ttu-id="38bc8-201">Откройте раскрывающийся список **Делегированные разрешения** и выберите разрешения службы шлюза SAP для Майкрософт, которые будет использовать ваша надстройка SharePoint.</span><span class="sxs-lookup"><span data-stu-id="38bc8-201">Open the **Delegated Permissions** drop down list and enable the boxes for the permissions to the SAP Gateway for Microsoft service that your SharePoint Add-in will need.</span></span>
    
 
17. <span data-ttu-id="38bc8-202">Нажмите кнопку **СОХРАНИТЬ** в нижней части экрана.</span><span class="sxs-lookup"><span data-stu-id="38bc8-202">Click **SAVE** at the bottom of the screen.</span></span>
    
 

### <a name="configure-the-application-to-communicate-with-azure-ad"></a><span data-ttu-id="38bc8-203">Настройка приложения для взаимодействия с Azure AD</span><span class="sxs-lookup"><span data-stu-id="38bc8-203">Configure the application to communicate with Azure AD</span></span>


1. <span data-ttu-id="38bc8-204">В Visual Studio откройте файл web.config проекта ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="38bc8-204">In Visual Studio, open the web.config file in the ASP.NET project.</span></span>
    
 
2. <span data-ttu-id="38bc8-p129">В разделе  `<appSettings>` в Инструменты разработчика Office для Visual Studio добавлены элементы для **ClientID** и **ClientSecret**, которые использует Надстройка SharePoint. Они используется в системе авторизации Azure ACS, если приложение ASP.NET получает доступ к SharePoint. В нашем примере на них можно не обращать внимания, но не следует их удалять. Размещаемые у поставщика Надстройки SharePoint используют эти сведения, даже если надстройка не получает доступ к данным SharePoint. Их значения будут изменяться при каждом нажатии клавиши F5 в Visual Studio. Добавьте в раздел два следующих элемента. Приложение использует их для аутентификации в Azure AD. Помните, что в системах аутентификации и авторизации на основе OAuth приложения, как и пользователи, являются субъектами безопасности.</span><span class="sxs-lookup"><span data-stu-id="38bc8-p129">In the  `<appSettings>` section, the Office Developer Tools for Visual Studio have added elements for the **ClientID** and **ClientSecret** of the SharePoint Add-in. (These are used in the Azure ACS authorization system if the ASP.NET application accesses SharePoint. You can ignore them for the continuing example, but do not delete them. They are required in provider-hosted SharePoint Add-ins even if the add-in is not accessing SharePoint data. Their values will change each time you press F5 in Visual Studio.) Add the following two elements to the section. These are used by the application to authenticate to Azure AD. (Remember that applications, as well as users, are security principals in OAuth-based authentication and authorization systems.)</span></span>
    
```
  <add key="ida:ClientID" value="" />
<add key="ida:ClientKey" value="" />
```

3. <span data-ttu-id="38bc8-p130">Вставьте ранее сохраненный идентификатор клиента из каталога Azure AD в качестве значения ключа **ida:ClientID**. Оставьте регистр и пунктуацию без изменений и убедитесь, что в начале и в конце значения нет пробелов. В качестве ключа **ida:ClientKey** используйте *ключ* из каталога. Как и в предыдущем случае, избегайте лишних пробелов и других изменений значения. Теперь раздел `<appSettings>` должен выглядеть примерно так (значением **ClientId** может быть GUID или пустая строка):</span><span class="sxs-lookup"><span data-stu-id="38bc8-p130">Insert the client ID that you saved from your Azure AD directory in the earlier procedure as the value of the **ida:ClientID** key. Leave the casing and punctuation exactly as you copied it and be careful not to include a space character at the beginning or end of the value. For the **ida:ClientKey** key use the *key*  that you saved from the directory. Again, be careful not to introduce any space characters or change the value in any way. The `<appSettings>` section should now look something like the following. (The **ClientId** value may have a GUID or an empty string.)</span></span>
    
```
  <appSettings>
  <add key="ClientId" value="" />
  <add key="ClientSecret" value="LypZu2yVajlHfPLRn5J2hBrwCk5aBOHxE4PtKCjIQkk=" />
  <add key="ida:ClientID" value="4da99afe-08b5-4bce-bc66-5356482ec2df" />
  <add key="ida:ClientKey" value="URwh/oiPay/b5jJWYHgkVdoE/x7gq3zZdtcl/cG14ss=" />
</appSettings>
```


     **Note**  Your application is known to Azure AD by the "localhost" URL you used to register it. The client ID and client key are associated with that identity. When you are ready to stage your application to an Azure Web Site, you will re-register it with a new URL.
4. <span data-ttu-id="38bc8-p131">Не покидая раздел **appSettings**, добавьте ключ **Authority** и укажите в качестве его значения домен Office 365 (*имя_домена*.onmicrosoft.com) учетной записи организации. В нашем примере используется учетная запись Bob@<домен_O365>.onmicrosoft.com, поэтому для ключа Authority задано значение `<O365_domain>.onmicrosoft.com`.</span><span class="sxs-lookup"><span data-stu-id="38bc8-p131">Still in the **appSettings** section, add an **Authority** key and set its value to the Office 365 domain ( *some_domain*  .onmicrosoft.com) of your organizational account. In the continuing example, the organizational account is Bob@<O365_domain>.onmicrosoft.com, so the authority is `<O365_domain>.onmicrosoft.com`.</span></span> 
    
```
  <add key="Authority" value="<O365_domain>.onmicrosoft.com" />
```

5. <span data-ttu-id="38bc8-p132">В разделе **appSettings** добавьте ключ **AppRedirectUrl** и задайте в качестве его значения адрес страницы, на которую браузер пользователя должен перенаправляться после того, как надстройка ASP.NET получит код авторизации из Azure AD. Как правило, пользователь просматривает именно эту страницу во время отправки вызова к Azure AD. В нашем примере используется URL-адрес SSL с приставкой "/Pages/Default.aspx", как показано ниже. Это значение также нужно изменить при подготовке.</span><span class="sxs-lookup"><span data-stu-id="38bc8-p132">Still in the **appSettings** section, add an **AppRedirectUrl** key and set its value to the page that the user's browser should be redirected to after the ASP.NET add-in has obtained an authorization code from Azure AD. Usually, this is the same page that the user was on when the call to Azure AD was made. In the continuing example, use the SSL URL value with "/Pages/Default.aspx" appended to it as shown below. (This is another value that you will change for staging.)</span></span>
    
```
  <add key="AppRedirectUrl" value="https://localhost:44322/Pages/Default.aspx" />
```

6. <span data-ttu-id="38bc8-p133">Не покидая раздел **appSettings**, добавьте ключ **ResourceUrl** и задайте в качестве его значения URI идентификатора приложения шлюза SAP для Майкрософт, а *не* URI идентификатора приложения ASP.NET. Это значение можно узнать у администратора шлюза SAP для Майкрософт. Ниже приведен пример.</span><span class="sxs-lookup"><span data-stu-id="38bc8-p133">Still in the **appSettings** section, add a **ResourceUrl** key and set its value to the APP ID URI of SAP Gateway for Microsoft ( *not*  the APP ID URI of your ASP.NET application). Obtain this value from the SAP Gateway for Microsoft administrator. The following is an example.</span></span>
    
```
  <add key="ResourceUrl" value="http://<SAP_gateway_domain>.cloudapp.net/" />
```


    The  `<appSettings>` section should now look something like this:
    


```
  <appSettings>
  <add key="ClientId" value="06af1059-8916-4851-a271-2705e8cf53c6" />
  <add key="ClientSecret" value="LypZu2yVajlHfPLRn5J2hBrwCk5aBOHxE4PtKCjIQkk=" />
  <add key="ida:ClientID" value="4da99afe-08b5-4bce-bc66-5356482ec2df" />
  <add key="ida:ClientKey" value="URwh/oiPay/b5jJWYHgkVdoE/x7gq3zZdtcl/cG14ss=" />
  <add key="Authority" value="<O365_domain>.onmicrosoft.com" />
  <add key="AppRedirectUrl" value="https://localhost:44322/Pages/Default.aspx" />
  <add key="ResourceUrl" value="http://<SAP_gateway_domain>.cloudapp.net/" />
</appSettings>
```

7. <span data-ttu-id="38bc8-227">Сохраните и закройте файл web.config.</span><span class="sxs-lookup"><span data-stu-id="38bc8-227">Save and close the web.config file.</span></span>
    
     <span data-ttu-id="38bc8-p134">**Совет.** Не оставляйте файл web.config открытым при запуске отладчика Visual Studio (F5). Инструменты разработчика Office для Visual Studio меняют значение **ClientId** (не **ida:ClientID**) при каждом нажатии клавиши F5. При этом вам нужно подтвердить повторную загрузку файла web.config, если он открыт при запуске отладки.</span><span class="sxs-lookup"><span data-stu-id="38bc8-p134">**TIP** Do not leave the web.config file open when you run the Visual Studio debugger (F5). The Office Developer Tools for Visual Studio change the **ClientId** value (not the **ida:ClientID**) every time you press F5. This requires you to respond to a prompt to reload the web.config file, if it is open, before debugging can execute.</span></span>

### <a name="add-a-helper-class-to-authenticate-to-azure-ad"></a><span data-ttu-id="38bc8-231">Добавление вспомогательного класса для проверки подлинности в Azure AD</span><span class="sxs-lookup"><span data-stu-id="38bc8-231">Add a helper class to authenticate to Azure AD</span></span>


1. <span data-ttu-id="38bc8-232">Щелкните проект ASP.NET правой кнопкой мыши и следуйте процессу добавления элемента Visual Studio, чтобы добавить к проекту новый файл класса с именем AADAuthHelper.cs.</span><span class="sxs-lookup"><span data-stu-id="38bc8-232">Right-click the ASP.NET project and use the Visual Studio item adding process to add a new class file to the project named AADAuthHelper.cs.</span></span>
    
 
2. <span data-ttu-id="38bc8-233">Добавьте в файл приведенные ниже операторы **using**.</span><span class="sxs-lookup"><span data-stu-id="38bc8-233">Add the following **using** statements to the file.</span></span>
    
```
  using Microsoft.IdentityModel.Clients.ActiveDirectory;
using System.Configuration;
using System.Web.UI;

```

3. <span data-ttu-id="38bc8-234">Измените ключевое слово доступа с **public** на **internal** и добавьте ключевое слово **static** к объявлению класса.</span><span class="sxs-lookup"><span data-stu-id="38bc8-234">Change the access keyword from **public** to **internal** and add the **static** keyword to the class declaration.</span></span>
    
```
  internal static class AADAuthHelper
```

4. <span data-ttu-id="38bc8-p135">Добавьте в класс приведенные ниже поля. В этих полях хранятся сведения, с помощью которых приложение ASP.NET получает маркеры доступа из AAD.</span><span class="sxs-lookup"><span data-stu-id="38bc8-p135">Add the following fields to the class. These fields store information that your ASP.NET application uses to get access tokens from AAD.</span></span>
    
```
  private static readonly string _authority = ConfigurationManager.AppSettings["Authority"];
private static readonly string _appRedirectUrl = ConfigurationManager.AppSettings["AppRedirectUrl"];
private static readonly string _resourceUrl = ConfigurationManager.AppSettings["ResourceUrl"];     
private static readonly string _clientId = ConfigurationManager.AppSettings["ida:ClientID"];        
private static readonly ClientCredential _clientCredential = new ClientCredential(
                           ConfigurationManager.AppSettings["ida:ClientID"],
                           ConfigurationManager.AppSettings["ida:ClientKey"]);

private static readonly AuthenticationContext _authenticationContext = 
            new AuthenticationContext("https://login.windows.net/common/" + 
                                      ConfigurationManager.AppSettings["Authority"]);
```

5. <span data-ttu-id="38bc8-p136">Добавьте к классу следующее свойство. В нем хранится URL-адрес экрана входа Azure AD.</span><span class="sxs-lookup"><span data-stu-id="38bc8-p136">Add the following property to the class. This property holds the URL to the Azure AD login screen.</span></span>
    
```
  private static string AuthorizeUrl
{
    get
    {
        return string.Format("https://login.windows.net/{0}/oauth2/authorize?response_type=code&amp;redirect_uri={1}&amp;client_id={2}&amp;state={3}",
            _authority,
            _appRedirectUrl,
            _clientId,
            Guid.NewGuid().ToString());
    }
}

```

6. <span data-ttu-id="38bc8-p137">Добавьте в класс следующие свойства. Они кэшируют маркеры доступа и обновления, а также проверяют, действительны ли они.</span><span class="sxs-lookup"><span data-stu-id="38bc8-p137">Add the following properties to the class. These cache the access and refresh tokens and check their validity.</span></span>
    
```
  public static Tuple<string, DateTimeOffset> AccessToken
{
    get {
return HttpContext.Current.Session["AccessTokenWithExpireTime-" + _resourceUrl] 
       as Tuple<string, DateTimeOffset>;
    }

    set { HttpContext.Current.Session["AccessTokenWithExpireTime-" + _resourceUrl] = value; }
}

private static bool IsAccessTokenValid
{
   get 
   { 
       return AccessToken != null &amp;&amp;
       !string.IsNullOrEmpty(AccessToken.Item1) &amp;&amp;
       AccessToken.Item2 > DateTimeOffset.UtcNow;
   }
}

private static string RefreshToken
{
    get { return HttpContext.Current.Session["RefreshToken" + _resourceUrl] as string; }
    set { HttpContext.Current.Session["RefreshToken-" + _resourceUrl] = value; }
}

private static bool IsRefreshTokenValid
{
    get { return !string.IsNullOrEmpty(RefreshToken); }
}

```

7. <span data-ttu-id="38bc8-p138">Добавьте к классу следующие методы. Они используются для проверки кода аутентификации и получения маркера доступа из Azure AD с помощью кода авторизации или маркера обновления.</span><span class="sxs-lookup"><span data-stu-id="38bc8-p138">Add the following methods to the class. These are used to check the validity of the authorization code and to obtain an access token from Azure AD by using either an authentication code or a refresh token.</span></span>
    
```
  private static bool IsAuthorizationCodeNotNull(string authCode)
{
    return !string.IsNullOrEmpty(authCode);
}

private static Tuple<Tuple<string,DateTimeOffset>,string> AcquireTokensUsingAuthCode(string authCode)
{
    var authResult = _authenticationContext.AcquireTokenByAuthorizationCode(
                authCode,
                new Uri(_appRedirectUrl),
                _clientCredential,
                _resourceUrl);

    return new Tuple<Tuple<string, DateTimeOffset>, string>(
                new Tuple<string, DateTimeOffset>(authResult.AccessToken, authResult.ExpiresOn), 
                authResult.RefreshToken);
}

private static Tuple<string, DateTimeOffset> RenewAccessTokenUsingRefreshToken()
{
    var authResult = _authenticationContext.AcquireTokenByRefreshToken(
                         RefreshToken,
                         _clientCredential.OwnerId,
                         _clientCredential,
                         _resourceUrl);

    return new Tuple<string, DateTimeOffset>(authResult.AccessToken, authResult.ExpiresOn);
}

```

8. <span data-ttu-id="38bc8-p139">Добавьте к классу следующий метод. Он вызывается из кода ASP.NET для получения маркера доступа перед отправкой запроса данных SAP через Шлюз SAP для Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="38bc8-p139">Add the following method to the class. It is called from the ASP.NET code behind to obtain a valid access token before a call is made to get SAP data via SAP Gateway for Microsoft.</span></span>
    
```
  internal static void EnsureValidAccessToken(Page page)
{
    if (IsAccessTokenValid) 
    {
        return;
    }
    else if (IsRefreshTokenValid) 
    {
        AccessToken = RenewAccessTokenUsingRefreshToken();
        return;
    }
    else if (IsAuthorizationCodeNotNull(page.Request.QueryString["code"]))
    {
        Tuple<Tuple<string, DateTimeOffset>, string> tokens = null;
        try
        {
            tokens = AcquireTokensUsingAuthCode(page.Request.QueryString["code"]);
        }
        catch 
        {
            page.Response.Redirect(AuthorizeUrl);
        }
        AccessToken = tokens.Item1;
        RefreshToken = tokens.Item2;
        return;
    }
    else
    {
        page.Response.Redirect(AuthorizeUrl);
    }
}
```


 <span data-ttu-id="38bc8-p140">**Совет.** Класс AADAuthHelper содержит минимальный набор обработчиков ошибок. Чтобы создать надежную и профессиональную надстройку SharePoint, добавьте обработчики ошибок, описанные в статье, посвященной [обработке ошибок в OAuth 2.0](http://msdn.microsoft.com/library/561bf289-3ff9-4eea-b165-4f5f02bcc520.aspx) библиотеки MSDN.</span><span class="sxs-lookup"><span data-stu-id="38bc8-p140">**TIP** The AADAuthHelper class has only minimal error handling. For a robust, production quality SharePoint Add-in, add more error handling as described in this MSDN node:  [Error Handling in OAuth 2.0](http://msdn.microsoft.com/library/561bf289-3ff9-4eea-b165-4f5f02bcc520.aspx).</span></span>
 


### <a name="create-data-model-classes"></a><span data-ttu-id="38bc8-247">Создание классов модели данных</span><span class="sxs-lookup"><span data-stu-id="38bc8-247">Create data model classes</span></span>


1. <span data-ttu-id="38bc8-p141">Создайте один или несколько классов модели данных, которые надстройка получает от SAP. В нашем примере используется только один класс модели данных. Щелкните проект ASP.NET правой кнопкой мыши и добавьте новый файл класса к проекту под названием Automobile.cs, следуя процедуре добавления элемента Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="38bc8-p141">Create one or more classes to model the data that your add-in gets from SAP. In the continuing example, there is just one data model class. Right-click the ASP.NET project and use the Visual Studio item adding process to add a new class file to the project named Automobile.cs.</span></span>
    
 
2. <span data-ttu-id="38bc8-251">Добавьте в тело класса следующий код:</span><span class="sxs-lookup"><span data-stu-id="38bc8-251">Add the following code to the body of the class:</span></span>
    
```
  public string Price;
public string Brand;
public string Model;
public int Year;
public string Engine;
public int MaxPower;
public string BodyStyle;
public string Transmission;
```


### <a name="add-code-behind-to-get-data-from-sap-via-the-sap-gateway-for-microsoft"></a><span data-ttu-id="38bc8-252">Добавление кода для получения данных из SAP через шлюз SAP для Майкрософт</span><span class="sxs-lookup"><span data-stu-id="38bc8-252">Add code behind to get data from SAP via the SAP Gateway for Microsoft</span></span>


1. <span data-ttu-id="38bc8-253">Откройте файл Default.aspx.cs и добавьте приведенные ниже операторы **using**.</span><span class="sxs-lookup"><span data-stu-id="38bc8-253">Open the Default.aspx.cs file and add the following **using** statements.</span></span>
    
```
  using System.Net;
using Newtonsoft.Json.Linq;
```

2. <span data-ttu-id="38bc8-p142">Добавьте объявление **const** к классу Default, указав в качестве значения URL-адрес конечной точки OData SAP, которую будет использовать надстройка. Ниже представлен пример такого объявления.</span><span class="sxs-lookup"><span data-stu-id="38bc8-p142">Add a **const** declaration to the Default class whose value is the base URL of the SAP OData endpoint that the add-in will be accessing. The following is an example:</span></span>
    
```
  private const string SAP_ODATA_URL = @"https://<SAP_gateway_domain>.cloudapp.net:8081/perf/sap/opu/odata/sap/ZCAR_POC_SRV/";
```

3. <span data-ttu-id="38bc8-p143">В Инструменты разработчика Office для Visual Studio добавлены методы **Page_PreInit** и **Page_Load**. Закомментируйте код метода **Page_Load** и весь метод **Page_Init**. Этот код не используется в данном примере. Если ваша надстройка SharePoint будет использовать SharePoint, этот код нужно восстановить. См. раздел [(Необязательно) Предоставление приложению ASP.NET доступа к SharePoint](#SharePoint).</span><span class="sxs-lookup"><span data-stu-id="38bc8-p143">The Office Developer Tools for Visual Studio have added a **Page_PreInit** method and a **Page_Load** method. Comment out the code inside the **Page_Load** method and comment out the whole **Page_Init** method. This code is not used in this sample. (If your SharePoint Add-in is going to access SharePoint, then you restore this code. See [Optionally, add SharePoint access to the ASP.NET application](#SharePoint).)</span></span>
    
 
4. <span data-ttu-id="38bc8-p144">Добавьте приведенную ниже строку в начало метода **Page_Load**. Это упростит отладку, так как приложение ASP.NET взаимодействует со шлюзом SAP для Майкрософт с помощью SSL (HTTPS), но сервер localhost:port не доверяет сертификату шлюза SAP для Майкрософт. Без этой строки кода перед открытием страницы Default.aspx появится предупреждение о недействительном сертификате. Некоторые браузеры позволяют пропустить эту ошибку, но в остальных открыть страницу Default.aspx может быть невозможно.</span><span class="sxs-lookup"><span data-stu-id="38bc8-p144">Add the following line to the top of the **Page_Load** method. This will ease the process of debugging because your ASP.NET application is communicating with SAP Gateway for Microsoft using SSL (HTTPS); but your "localhost:port" server is not configured to trust the certificate of SAP Gateway for Microsoft. Without this line of code, you would get an invalid certificate warning before Default.aspx will open. Some browsers allow you to click past this error, but some will not let you open Default.aspx at all.</span></span>
    
```
  ServicePointManager.ServerCertificateValidationCallback = (s, cert, chain, errors) => true;
```


     **Important**  Delete this line when you are ready to deploy the ASP.NET application to staging. See  [Modify the add-in and stage it to Azure and Office 365](#Stage).
5. <span data-ttu-id="38bc8-p145">Добавьте приведенный ниже код в метод **Page_Load**. Строка, передаваемая методу `GetSAPData`, — это запрос OData.</span><span class="sxs-lookup"><span data-stu-id="38bc8-p145">Add the following code to the **Page_Load** method. The string you pass to the `GetSAPData` method is an OData query.</span></span>
    
```
  if (!IsPostBack)
{
    GetSAPData("DataCollection?$top=3");
}

```

6. <span data-ttu-id="38bc8-p146">Добавьте приведенный ниже метод в класс Default. Сначала этот метод обеспечивает наличие в кэше действительного маркера доступа, полученного из Azure AD. Затем он создает HTTP-запрос **GET**, содержащий маркер доступа, и отправляет его конечной точке OData SAP. Результат возвращается в виде объекта JSON, преобразованного в объект **List** платформы .NET. В массиве, привязанном к объекту **DataListView**, используется три свойства элементов.</span><span class="sxs-lookup"><span data-stu-id="38bc8-p146">Add the following method to the Default class. This method first ensures that the cache for the access token has a valid access token in it that has been obtained from Azure AD. It then creates an HTTP **GET** Request that includes the access token and sends it to the SAP OData endpoint. The result is returned as a JSON object that is converted to a .NET **List** object. Three properties of the items are used in an array that is bound to the **DataListView**.</span></span>
    
```
  private void GetSAPData(string oDataQuery)
{
    AADAuthHelper.EnsureValidAccessToken(this);

    using (WebClient client = new WebClient())
    {
        client.Headers[HttpRequestHeader.Accept] = "application/json";
        client.Headers[HttpRequestHeader.Authorization] = "Bearer " + AADAuthHelper.AccessToken.Item1;
        var jsonString = client.DownloadString(SAP_ODATA_URL + oDataQuery);
        var jsonValue = JObject.Parse(jsonString)["d"]["results"];
        var dataCol = jsonValue.ToObject<List<Automobile>>();

        var dataList = dataCol.Select((item) => {
            return item.Brand + " " + item.Model + " " + item.Price;
            }).ToArray();

        DataListView.DataSource = dataList;
        DataListView.DataBind();
    }
}

```


### <a name="create-the-user-interface"></a><span data-ttu-id="38bc8-272">Создание пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="38bc8-272">Create the user interface</span></span>


1. <span data-ttu-id="38bc8-273">Откройте файл Default.aspx и добавьте следующую разметку в **форму** страницы:</span><span class="sxs-lookup"><span data-stu-id="38bc8-273">Open the Default.aspx file and add the following markup to the **form** of the page:</span></span>
    
```
  <div>
  <h3>Data from SAP via SAP Gateway for Microsoft</h3>

  <asp:ListView runat="server" ID="DataListView">
    <ItemTemplate>
      <tr runat="server">
        <td runat="server">
          <asp:Label ID="DataLabel" runat="server"
            Text="<%# Container.DataItem.ToString()%>" /><br />
        </td>
      </tr>
    </ItemTemplate>
  </asp:ListView>
</div>
```

2. <span data-ttu-id="38bc8-274">При желании вы можете придать веб-странице внешний вид страницы SharePoint с помощью SharePoint  [элемента управления хрома](use-the-client-chrome-control-in-sharepoint-add-ins) и [таблицы стилей веб-сайта SharePoint](use-a-sharepoint-website-s-style-sheet-in-sharepoint-add-ins).</span><span class="sxs-lookup"><span data-stu-id="38bc8-274">Optionally, give the web page the "look 'n' feel" of a SharePoint page with the SharePoint  [Chrome Control](use-the-client-chrome-control-in-sharepoint-add-ins) and [the host SharePoint website's style sheet](use-a-sharepoint-website-s-style-sheet-in-sharepoint-add-ins).</span></span>
    
 

### <a name="test-the-add-in-with-f5-in-visual-studio"></a><span data-ttu-id="38bc8-275">Тестирование надстройки с помощью клавиши F5 в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="38bc8-275">Test the add-in with F5 in Visual Studio</span></span>


1. <span data-ttu-id="38bc8-276">Нажмите клавишу F5 в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="38bc8-276">Press F5 in Visual Studio.</span></span>
    
 
2. <span data-ttu-id="38bc8-p147">При первом нажатии клавиши F5 вам может быть предложено войти на ваш Сайт разработчиков. Используйте учетные данные администратора. В нашем примере используется учетная запись Bob@<домен_O365>.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="38bc8-p147">The first time that you use F5, you may be prompted to login to the Developer Site that you are using. Use the site administrator credentials. In the continuing example, it is Bob@<O365_domain>.onmicrosoft.com.</span></span>
    
 
3. <span data-ttu-id="38bc8-p148">При первом нажатии клавиши F5 вам будет предложено предоставить надстройке разрешения. Нажмите кнопку **Доверять**.</span><span class="sxs-lookup"><span data-stu-id="38bc8-p148">The first time that you use F5, you are prompted to grant permissions to the add-in. Click **Trust It**.</span></span>
    
 
4. <span data-ttu-id="38bc8-p149">После краткой задержки для получения маркера доступа открывается страница Default.aspx. Убедитесь, что на ней отображаются данные SAP.</span><span class="sxs-lookup"><span data-stu-id="38bc8-p149">After a brief delay while the access token is being obtained, the Default.aspx page opens. Verify that the SAP data appears.</span></span>
    
 

## <a name="optionally-add-sharepoint-access-to-the-aspnet-application"></a><span data-ttu-id="38bc8-284">(Необязательно) Предоставление приложению ASP.NET доступа к SharePoint</span><span class="sxs-lookup"><span data-stu-id="38bc8-284">Optionally, add SharePoint access to the ASP.NET application</span></span>
<span data-ttu-id="38bc8-285"><a name="SharePoint"> </a></span><span class="sxs-lookup"><span data-stu-id="38bc8-285"></span></span>

<span data-ttu-id="38bc8-p150">Конечно, надстройка SharePoint не обязательно должна показывать только данные SAP на веб-странице, открытой из SharePoint. Она также может выполнять операции CRUD (создание, чтение, обновление и удаление) с данными SharePoint. Их можно реализовать в коде с помощью клиентской объектной модели SharePoint (CSOM) или интерфейсов REST API SharePoint. Модель CSOM развертывается в виде пары сборок, которые Инструменты разработчика Office для Visual Studio автоматически включают в проект ASP.NET и для которых включается параметр **Копировать локально** в Visual Studio, чтобы они добавлялись в пакет приложения ASP.NET. Сведения об использовании CSOM см. в статье [Выполнение базовых операций с помощью кода клиентской библиотеки SharePoint](complete-basic-operations-using-sharepoint-2013-client-library-code). Сведения об использовании интерфейсов REST API см. в статье [Знакомство с REST-интерфейсом SharePoint и его использование](http://msdn.microsoft.com/en-us/magazine/dn198245.aspx).</span><span class="sxs-lookup"><span data-stu-id="38bc8-p150">Of course, your SharePoint Add-in doesn't have to expose only SAP data in a web page launched from SharePoint. It can also create, read, update, and delete (CRUD) SharePoint data. Your code behind can do this using either the SharePoint client object model (CSOM) or the REST APIs of SharePoint. The CSOM is deployed as a pair of assemblies that the Office Developer Tools for Visual Studio automatically included in the ASP.NET project and set to **Copy Local** in Visual Studio so that they are included in the ASP.NET application package. For information about using CSOM, start with [Complete basic operations using SharePoint client library code](complete-basic-operations-using-sharepoint-2013-client-library-code). For information about using the REST APIs, start with  [Understanding and Using the SharePoint REST Interface](http://msdn.microsoft.com/en-us/magazine/dn198245.aspx).</span></span> 
 

 
<span data-ttu-id="38bc8-p151">Независимо от того, используете ли вы CSOM или API REST для доступа к SharePoint, приложению ASP.NET необходимо получить маркер доступа к SharePoint, как и к Шлюз SAP для Майкрософт. См. раздел  [Понимание аутентификации и авторизации в Шлюз SAP для Майкрософт и SharePoint](#AuthOverview) выше. Далее описаны основные действия, необходимые для этого, но для начала рекомендуем прочитать следующие статьи:</span><span class="sxs-lookup"><span data-stu-id="38bc8-p151">Regardless, of whether you use CSOM or the REST APIs to access SharePoint, your ASP.NET application must get an access token to SharePoint, just as it does to SAP Gateway for Microsoft. See  [Understand authentication and authorization to SAP Gateway for Microsoft and SharePoint](#AuthOverview) above. The procedure below provides some basic guidance about how to do this, but we recommend that you first read the following articles:</span></span>
 

 

-  [<span data-ttu-id="38bc8-295">Знакомство с созданием надстроек SharePoint с размещением у поставщика</span><span class="sxs-lookup"><span data-stu-id="38bc8-295">Get started creating provider-hosted SharePoint Add-ins</span></span>](get-started-creating-provider-hosted-sharepoint-add-ins)
    
 
-  [<span data-ttu-id="38bc8-296">Авторизация и проверка подлинности надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="38bc8-296">Authorization and authentication of SharePoint Add-ins</span></span>](authorization-and-authentication-of-sharepoint-add-ins)
    
 
-  [<span data-ttu-id="38bc8-297">Три системы авторизации для надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="38bc8-297">Three authorization systems for SharePoint Add-ins</span></span>](three-authorization-systems-for-sharepoint-add-ins)
    
 
-  [<span data-ttu-id="38bc8-298">Создание надстроек SharePoint, использующих авторизацию с низким уровнем доверия</span><span class="sxs-lookup"><span data-stu-id="38bc8-298">Creating SharePoint Add-ins that use low-trust authorization</span></span>](creating-sharepoint-add-ins-that-use-low-trust-authorization)
    
 
-  [<span data-ttu-id="38bc8-299">Поток OAuth токена контекста для надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="38bc8-299">Context Token OAuth flow for SharePoint Add-ins</span></span>](context-token-oauth-flow-for-sharepoint-add-ins)
    
 

1. <span data-ttu-id="38bc8-p152">Откройте файл Default.aspx.cs и раскомментируйте метод **Page_PreInit**. Затем раскомментируйте код, добавленный Инструментами разработчика Office для Visual Studio к методу **Page_Load**.</span><span class="sxs-lookup"><span data-stu-id="38bc8-p152">Open the Default.aspx.cs file and uncomment the **Page_PreInit** method. Also uncomment the code that the Office Developer Tools for Visual Studio added to the **Page_Load** method.</span></span>
    
 
2. <span data-ttu-id="38bc8-p153">Если ваша Надстройка SharePoint будет обращаться к данным SharePoint, необходимо кэшировать маркер контекста SharePoint, отправленный POST-запросом на страницу Default.aspx при запуске приложения в SharePoint. Это позволит убедиться, что маркер контекста SharePoint не потеряется при перенаправлении браузера после аутентификации в Azure AD. (Кэшировать этот контекст можно несколькими способами.) Инструменты разработчика Office для Visual Studio добавляет файл SharePointContext.cs к проекту ASP.NET, который выполняет основную часть работы. Чтобы использовать кэш сеанса, добавьте следующий код в блок " `if (!IsPostBack)`"  *перед*  кодом, который вызывает Шлюз SAP для Майкрософт:</span><span class="sxs-lookup"><span data-stu-id="38bc8-p153">If your SharePoint Add-in is going to access SharePoint data, then you have to cache the SharePoint context token that is POSTed to the Default.aspx page when the add-in is launched in SharePoint. This is to ensure that the SharePoint context token is not lost when the browser is redirected following the Azure AD authentication. (You have several options for how to cache this context.) The Office Developer Tools for Visual Studio add a SharePointContext.cs file to the ASP.NET project that does most of the work. To use the session cache, you simply add the following code inside the " `if (!IsPostBack)`" block  *before*  the code that calls out to SAP Gateway for Microsoft:</span></span>
    
```
  if (HttpContext.Current.Session["SharePointContext"] == null) 
{
     HttpContext.Current.Session["SharePointContext"]
        = SharePointContextProvider.Current.GetSharePointContext(Context);
}
```

3. <span data-ttu-id="38bc8-p154">Файл SharePointContext.cs отправляет вызовы другому файлу, который Инструменты разработчика Office для Visual Studio добавляет к проекту: TokenHelper.cs. Этот файл содержит большую часть кода, необходимого для получения и использования маркеров доступа для SharePoint. Тем не менее, в нем отсутствует код для продления срока действия устаревшего маркера доступа или маркера обновления. Кроме того, в нем нет кода для кэширования маркеров. Если вы создаете профессиональную надстройку SharePoint, добавить этот код необходимо. Примером может служить логика кэширования из предыдущего этапа. Ваш код также должен кэшировать маркер доступа и продолжать использовать его до истечения срока действия. По истечении срока действия маркера код должен получить новый маркер доступа с помощью маркера обновления.</span><span class="sxs-lookup"><span data-stu-id="38bc8-p154">The SharePointContext.cs file makes calls to another file that the Office Developer Tools for Visual Studio added to the project: TokenHelper.cs. This file provides most of the code needed to obtain and use access tokens for SharePoint. However, it does not provide any code for renewing an expired access token or an expired refresh token. Nor does it contain any token caching code. For a production quality SharePoint Add-in, you need to add such code. The caching logic in the preceding step is an example. Your code should also cache the access token and reuse it until it expires. When the access token is expired, your code should use the refresh token to get a new access token.</span></span>
    
 
4. <span data-ttu-id="38bc8-p155">Добавьте вызовы данных SharePoint с помощью CSOM или REST. Приведенный ниже пример является вариацией кода CSOM, который Инструменты разработчика Office для Visual Studio добавляют к методу **Page_Load**. В этом примере код был перемещен в отдельный метод и начинается с получения кэшированного маркера доступа.</span><span class="sxs-lookup"><span data-stu-id="38bc8-p155">Add the data calls to SharePoint using either CSOM or REST. The following example is a modification of CSOM code that Office Developer Tools for Visual Studio adds to the **Page_Load** method. In this example, the code has been moved to a separate method and it begins by retrieving the cached context token.</span></span>
    
```
  private void GetSharePointTitle()
{
    var spContext = HttpContext.Current.Session["SharePointContext"] as SharePointContext;
    using (var clientContext = spContext.CreateUserClientContextForSPHost())
    {
        clientContext.Load(clientContext.Web, web => web.Title);
        clientContext.ExecuteQuery();
        SharePointTitle.Text = "SharePoint web site title is: " + clientContext.Web.Title;
    }
}
```

5. <span data-ttu-id="38bc8-p156">Добавьте элементы пользовательского интерфейса для отрисовки данных SharePoint. Ниже показан элемент управления HTML, на который ссылается предыдущий метод.</span><span class="sxs-lookup"><span data-stu-id="38bc8-p156">Add UI elements to render the SharePoint data. The following shows the HTML control that is referenced in the preceding method:</span></span>
    
```
  <h3>SharePoint title</h3><asp:Label ID="SharePointTitle" runat="server"></asp:Label><br />
```


 <span data-ttu-id="38bc8-p157">**Примечание.** При отладке надстройки SharePoint Инструменты разработчика Office для Visual Studio заново регистрируют ее в Azure ACS при каждом нажатии клавиши F5 в Visual Studio. Когда вы подготавливаете надстройку SharePoint, ей необходимо назначить долгосрочные регистрационные данные. См. раздел [Изменение и подготовка надстройки в Azure и Office 365](#Stage).</span><span class="sxs-lookup"><span data-stu-id="38bc8-p157">**Note** While you are debugging the SharePoint Add-in, the Office Developer Tools for Visual Studio re-register it with Azure ACS each time you press F5 in Visual Studio. When you stage the SharePoint Add-in, you have to give it a long-term registration. See the section  [Modify the add-in and stage it to Azure and Office 365](#Stage).</span></span>
 


## <a name="modify-the-add-in-and-stage-it-to-azure-and-office-365"></a><span data-ttu-id="38bc8-322">Изменение и подготовка надстройки в Azure и Office 365</span><span class="sxs-lookup"><span data-stu-id="38bc8-322">Modify the add-in and stage it to Azure and Office 365</span></span>
<span data-ttu-id="38bc8-323"><a name="Stage"> </a></span><span class="sxs-lookup"><span data-stu-id="38bc8-323"></span></span>

<span data-ttu-id="38bc8-324">Закончив отлаживать надстройку SharePoint с помощью клавиши F5 в Visual Studio, необходимо выполнить развертывание приложения ASP.NET в Веб-сайт Azure.</span><span class="sxs-lookup"><span data-stu-id="38bc8-324">When you have finished debugging the SharePoint Add-in using F5 in Visual Studio, you need to deploy the ASP.NET application to an actual Azure Web Site.</span></span>
 

 

### <a name="create-the-azure-web-site"></a><span data-ttu-id="38bc8-325">Создание веб-сайта Azure</span><span class="sxs-lookup"><span data-stu-id="38bc8-325">Create the Azure Web Site</span></span>


1. <span data-ttu-id="38bc8-326">На портале Microsoft Azure выберите **ВЕБ-САЙТЫ** в левой области навигации.</span><span class="sxs-lookup"><span data-stu-id="38bc8-326">In the Microsoft Azure portal, open **WEB SITES** on the left navigation bar.</span></span>
    
 
2. <span data-ttu-id="38bc8-327">Нажмите **СОЗДАТЬ** в нижней части страницы, а в диалоговом окне **СОЗДАНИЕ** выберите команды **ВЕБ-САЙТ** |**БЫСТРОЕ СОЗДАНИЕ**.</span><span class="sxs-lookup"><span data-stu-id="38bc8-327">Click **NEW** at the bottom of the page and on the **NEW** dialog select **WEB SITE** |**QUICK CREATE**.</span></span>
    
 
3. <span data-ttu-id="38bc8-p158">Введите имя домена и нажмите **СОЗДАТЬ ВЕБ-САЙТ**. Скопируйте URL-адрес нового сайта. Он будет выглядеть так: `my_domain.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="38bc8-p158">Enter a domain name and click **CREATE WEB SITE**. Make a copy of the new site's URL. It will have the form  `my_domain.azurewebsites.net`.</span></span>
    
 

### <a name="modify-the-code-and-markup-in-the-application"></a><span data-ttu-id="38bc8-331">Изменение кода и разметки в приложении</span><span class="sxs-lookup"><span data-stu-id="38bc8-331">Modify the code and markup in the application</span></span>


1. <span data-ttu-id="38bc8-332">В Visual Studio удалите строку `ServicePointManager.ServerCertificateValidationCallback = (s, cert, chain, errors) => true;` из файла Default.aspx.cs.</span><span class="sxs-lookup"><span data-stu-id="38bc8-332">In Visual Studio, remove the line  `ServicePointManager.ServerCertificateValidationCallback = (s, cert, chain, errors) => true;` from the Default.aspx.cs file.</span></span>
    
 
2. <span data-ttu-id="38bc8-p159">Откройте файл web.config проекта ASP.NET и замените доменную часть значения ключа **AppRedirectUrl** в разделе **appSettings** на домен веб-сайта Azure. Например, замените `<add key="AppRedirectUrl" value="https://localhost:44322/Pages/Default.aspx" />` на `<add key="AppRedirectUrl" value="https://my_domain.azurewebsites.net/Pages/Default.aspx" />`.</span><span class="sxs-lookup"><span data-stu-id="38bc8-p159">Open the web.config file of the ASP.NET project and change the domain part of the value of the **AppRedirectUrl** key in the **appSettings** section to the domain of the Azure Web Site. For example, change `<add key="AppRedirectUrl" value="https://localhost:44322/Pages/Default.aspx" />` to `<add key="AppRedirectUrl" value="https://my_domain.azurewebsites.net/Pages/Default.aspx" />`.</span></span>
    
 
3. <span data-ttu-id="38bc8-335">Щелкните правой кнопкой мыши файл AppManifest.xml в проекте надстройки SharePoint и выберите команду **Перейти к коду**.</span><span class="sxs-lookup"><span data-stu-id="38bc8-335">Right-click the AppManifest.xml file in the SharePoint Add-in project and select **View Code**.</span></span>
    
 
4. <span data-ttu-id="38bc8-p160">В значении **StartPage** замените строку `~remoteAppUrl` на полное доменное имя веб-сайта Azure, включая протокол, например `https://my_domain.azurewebsites.net`. Теперь полное значение **StartPage** должно выглядеть так: `https://my_domain.azurewebsites.net/Pages/Default.aspx` (как правило, значение **StartPage** совпадает со значением ключа **AppRedirectUrl** в файле web.config).</span><span class="sxs-lookup"><span data-stu-id="38bc8-p160">In the **StartPage** value, replace the string `~remoteAppUrl` with the full domain of the Azure Web Site including the protocol; for example `https://my_domain.azurewebsites.net`. The entire **StartPage** value should now be: `https://my_domain.azurewebsites.net/Pages/Default.aspx`. (Usually, the **StartPage** value is exactly the same as the value of the **AppRedirectUrl** key in the web.config file.)</span></span>
    
 

### <a name="modify-the-aad-registration-and-register-the-add-in-with-acs"></a><span data-ttu-id="38bc8-339">Изменение регистрационных данных в AAD и регистрация надстройки в службе контроля доступа</span><span class="sxs-lookup"><span data-stu-id="38bc8-339">Modify the AAD registration and register the add-in with ACS</span></span>


1. <span data-ttu-id="38bc8-340">Войдите на [портал управления Azure](https://manage.windowsazure.com), используя учетную запись администратора Azure.</span><span class="sxs-lookup"><span data-stu-id="38bc8-340">Login into  [Azure Management portal](https://manage.windowsazure.com) with your Azure administrator account.</span></span>
    
 
2. <span data-ttu-id="38bc8-341">Выберите **Active Directory** в левой части страницы.</span><span class="sxs-lookup"><span data-stu-id="38bc8-341">Choose **Active Directory** on the left side.</span></span>
    
 
3. <span data-ttu-id="38bc8-342">Щелкните каталог.</span><span class="sxs-lookup"><span data-stu-id="38bc8-342">Click on your directory.</span></span>
    
 
4. <span data-ttu-id="38bc8-343">Выберите **ПРИЛОЖЕНИЯ** (на верхней панели навигации).</span><span class="sxs-lookup"><span data-stu-id="38bc8-343">Choose **APPLICATIONS** (on the top navigation bar).</span></span>
    
 
5. <span data-ttu-id="38bc8-p161">Откройте созданное приложение. В нашем примере используется имя **ContosoAutomobileCollection**.</span><span class="sxs-lookup"><span data-stu-id="38bc8-p161">Open the application you created. In the continuing example, it is **ContosoAutomobileCollection**.</span></span>
    
 
6. <span data-ttu-id="38bc8-346">В каждом из следующих значений замените фрагмент "localhost: *порт*" на значение домена нового веб-сайта Azure:</span><span class="sxs-lookup"><span data-stu-id="38bc8-346">For each of the following values, change the "localhost: *port*  " part of the value to the domain of your new Azure Web Site:</span></span>
    
      -  <span data-ttu-id="38bc8-347">**URL-АДРЕС ДЛЯ ВХОДА**</span><span class="sxs-lookup"><span data-stu-id="38bc8-347">**SIGN-ON URL**</span></span>
    
 
  -  <span data-ttu-id="38bc8-348">**URI ИДЕНТИФИКАТОРА ПРИЛОЖЕНИЯ**</span><span class="sxs-lookup"><span data-stu-id="38bc8-348">**APP ID URI**</span></span>
    
 
  -  <span data-ttu-id="38bc8-349">**URL-АДРЕС ОТВЕТА**</span><span class="sxs-lookup"><span data-stu-id="38bc8-349">**REPLY URL**</span></span>
    
 

    <span data-ttu-id="38bc8-350">Например, если для **URI ИДЕНТИФИКАТОРА ПРИЛОЖЕНИЯ** задано значение **https://localhost:44304/ContosoAutomobileCollection**, замените его на **https://<мой_домен>.azurewebsites.net/ContosoAutomobileCollection**.</span><span class="sxs-lookup"><span data-stu-id="38bc8-350">For example, if the **APP ID URI** is **https://localhost:44304/ContosoAutomobileCollection**, change it to **https://<my_domain>.azurewebsites.net/ContosoAutomobileCollection**.</span></span>
    
 
7. <span data-ttu-id="38bc8-351">Нажмите кнопку **СОХРАНИТЬ** в нижней части экрана.</span><span class="sxs-lookup"><span data-stu-id="38bc8-351">Click **SAVE** at the bottom of the screen.</span></span>
    
 
8. <span data-ttu-id="38bc8-p162">Зарегистрируйте надстройку в Azure ACS. Это необходимо сделать, даже если надстройка не получает доступ к SharePoint и не будет использовать маркеры из службы контроля доступа, так как при этом надстройка регистрируется еще и в службе управления надстройками для подписки на Office 365, а это обязательно. (Служба управления надстройками получила такое название, так как она используется для управления надстройками SharePoint, которые ранее назывались приложениями для SharePoint.) В случае подписки на Office 365 регистрация выполняется на странице AppRegNew.aspx любого веб-сайта SharePoint. Дополнительные сведения см. в статье [Регистрация надстроек SharePoint 2013](register-sharepoint-add-ins-2013). В ходе регистрации вы получите новые идентификатор и секрет клиента. Вставьте эти значения в файл web.config в качестве ключей **ClientId** (не **ida:ClientID**) и **ClientSecret**.</span><span class="sxs-lookup"><span data-stu-id="38bc8-p162">Register the add-in with Azure ACS. This must be done even if the add-in does not access SharePoint and will not use tokens from ACS, because the same process also registers the add-in with the Add-in Management Service of the Office 365 subscription, which is a requirement. (It is called "Add-in Management Service" because SharePoint Add-ins were originally called "apps for SharePoint".) You perform the registration on the AppRegNew.aspx page of any SharePoint website in the Office 365 subscription. For details, see  [Register SharePoint Add-ins 2013](register-sharepoint-add-ins-2013). As part of this process you will obtain a new client ID and client secret. Insert these values in the web.config for the **ClientId** (not **ida:ClientID**) and **ClientSecret** keys.</span></span>
    
     <span data-ttu-id="38bc8-p163">**Внимание!** Если по какой-либо причине вы нажмете клавишу F5 после внесения этих изменений, Инструменты разработчика Office для Visual Studio заменят одно из этих значений или оба значения. Поэтому следует вести журнал значений, полученных на странице AppRegNew.aspx, и всегда проверять правильность значений в файле web.config непосредственно перед публикацией приложения ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="38bc8-p163">**Caution** If for any reason you press F5 after making this change, the Office Developer Tools for Visual Studio will overwrite one or both of these values. For that reason, you should keep a record of the values obtained with AppRegNew.aspx and always verify that the values in the web.config are correct just before you publish the ASP.NET application.</span></span> 

### <a name="publish-the-aspnet-application-to-azure-and-install-the-add-in-to-sharepoint"></a><span data-ttu-id="38bc8-360">Публикация приложения ASP.NET в Azure и установка надстройки в SharePoint</span><span class="sxs-lookup"><span data-stu-id="38bc8-360">Publish the ASP.NET application to Azure and install the add-in to SharePoint</span></span>


1. <span data-ttu-id="38bc8-p164">Опубликовать приложение ASP.NET в Веб-сайт Azure можно несколькими способами. Дополнительные сведения см. в статье  [Развертывание веб-сайта Azure](http://azure.microsoft.com/en-us/documentation/articles/web-sites-deploy/).</span><span class="sxs-lookup"><span data-stu-id="38bc8-p164">There are several ways to publish an ASP.NET application to an Azure Web Site. For more information, see  [How to Deploy an Azure Web Site](http://azure.microsoft.com/en-us/documentation/articles/web-sites-deploy/).</span></span>
    
 
2. <span data-ttu-id="38bc8-p165">В Visual Studio щелкните правой кнопкой мыши надстройку SharePoint и выберите пункт **Упаковать**. На открывшейся странице **Публикация надстройки** нажмите **Упаковать надстройку**. Откроется окно проводника с папкой, содержащей пакет надстройки.</span><span class="sxs-lookup"><span data-stu-id="38bc8-p165">In Visual Studio, right-click the SharePoint add-in project and select **Package**. On the **Publish your add-in** page that opens, click **Package the add-in**. File explorer opens to the folder with the add-in package.</span></span>
    
 
3. <span data-ttu-id="38bc8-p166">Войдите в Office 365 от имени глобального администратора и перейдите к семейству веб-сайтов каталога надстроек. Если такого семейства нет, создайте его (см. статью  [Использование каталога надстроек для развертывания пользовательских бизнес-надстроек в среде SharePoint Online](http://office.microsoft.com/en-us/sharepoint-help/use-the-app-catalog-to-make-custom-business-apps-available-for-your-sharepoint-online-environment-HA102772362.aspx)).</span><span class="sxs-lookup"><span data-stu-id="38bc8-p166">Login to Office 365 as a global administrator, and navigate to the organization add-in catalog site collection. (If there isn't one, create it. See  [Use the Add-in Catalog to make custom business add-ins available for your SharePoint Online environment](http://office.microsoft.com/en-us/sharepoint-help/use-the-app-catalog-to-make-custom-business-apps-available-for-your-sharepoint-online-environment-HA102772362.aspx).)</span></span>
    
 
4. <span data-ttu-id="38bc8-369">Отправьте пакет надстройки в каталог надстроек.</span><span class="sxs-lookup"><span data-stu-id="38bc8-369">Upload the add-in package to the add-in catalog.</span></span>
    
 
5. <span data-ttu-id="38bc8-370">Откройте на любом сайте подписки страницу **Контент сайта** и нажмите **Добавить надстройку**.</span><span class="sxs-lookup"><span data-stu-id="38bc8-370">Navigate to the **Site Contents** page of any website in the subscription and click **add an add-in**.</span></span>
    
 
6. <span data-ttu-id="38bc8-371">На странице **Надстройки** найдите раздел **Надстройки, которые вы можете добавить** и щелкните значок вашей надстройки правой кнопкой мыши.</span><span class="sxs-lookup"><span data-stu-id="38bc8-371">On the **Your Add-ins** page, scroll to the **Add-ins you can add** section and click the icon for your add-in.</span></span>
    
 
7. <span data-ttu-id="38bc8-372">После установки надстройки щелкните ее значок на странице **Контент сайта**, чтобы запустить надстройку.</span><span class="sxs-lookup"><span data-stu-id="38bc8-372">After the add-in has installed, click it's icon on the **Site Contents** page to launch the add-in.</span></span>
    
 
<span data-ttu-id="38bc8-373">Дополнительные сведения об установке надстроек SharePoint см. в статье [Развертывание и установка надстроек SharePoint: методы и параметры](deploying-and-installing-sharepoint-add-ins-methods-and-options).</span><span class="sxs-lookup"><span data-stu-id="38bc8-373">For more information about installing SharePoint Add-ins, see  [Deploying and installing SharePoint Add-ins: methods and options](deploying-and-installing-sharepoint-add-ins-methods-and-options).</span></span>
 

## <a name="deploying-the-add-in-to-production"></a><span data-ttu-id="38bc8-374">Развертывание надстройки в рабочей среде</span><span class="sxs-lookup"><span data-stu-id="38bc8-374">Deploying the add-in to production</span></span>
<span data-ttu-id="38bc8-375"><a name="Stage"> </a></span><span class="sxs-lookup"><span data-stu-id="38bc8-375"></span></span>

<span data-ttu-id="38bc8-p167">Завершив тестирование, вы можете развернуть надстройку в рабочей среде. Для этого может потребоваться внести некоторые изменения.</span><span class="sxs-lookup"><span data-stu-id="38bc8-p167">When you have finished all testing you can deploy the add-in in production. This may require some changes.</span></span>
 

 

1. <span data-ttu-id="38bc8-p168">Если рабочий домен приложения ASP.NET отличается от промежуточного домена, необходимо изменить значение **AppRedirectUrl** в файле web.config и значение **StartPage** в файле AppManifest.xml, а затем заново упаковать надстройку SharePoint. См. раздел **Изменение кода и разметки приложения** выше.</span><span class="sxs-lookup"><span data-stu-id="38bc8-p168">If the production domain of the ASP.NET application is different from the staging domain, you will have to change **AppRedirectUrl** value in the web.config and the **StartPage** value in the AppManifest.xml file, and repackage the SharePoint Add-in. See the procedure **Modify the code and markup in the application** above.</span></span>
    
 
2. <span data-ttu-id="38bc8-p169">При изменении домена также требуется изменить регистрационные данные надстроек в AAD. См. раздел **Изменение регистрационных данных в AAD и регистрация надстройки в службе контроля доступа** выше.</span><span class="sxs-lookup"><span data-stu-id="38bc8-p169">The change in domain also requires that you edit the add-ins registration with AAD. See the procedure **Modify the AAD registration and register the add-in with ACS** above.</span></span>
    
 
3. <span data-ttu-id="38bc8-p170">Кроме того, при изменении домена необходимо повторно зарегистрировать надстройку в службе ACS (и службе управления надстройками подписки). Этот процесс также описан в вышеупомянутом разделе. *Изменить* регистрационные данные надстройки в службе контроля доступа невозможно. Однако создавать новые идентификатор и секрет клиента на странице AppRegNew.aspx не требуется. Вы можете скопировать исходные значения из ключей **ClientId** (не **ida:ClientID**) и **ClientSecret** файла web.config в форму AppRegNew. *Создавая ключи, не забывайте копировать новые значения в ключи файла web.config.*</span><span class="sxs-lookup"><span data-stu-id="38bc8-p170">The change in domain also requires that you re-register the add-in with ACS (and the subscription's Add-in Management Service) as described in the same procedure. (There is no way to  *edit*  an add-in's registration with ACS.) However, it is not necessary to generate a new client ID or client secret on the AppRegNew.aspx page. You can copy the original values from the **ClientId** (not **ida:ClientID**) and **ClientSecret** keys of the web.config into the AppRegNew form. *If you do generate new ones, be sure to copy the new values to the keys in web.config.*</span></span> 
    
 

