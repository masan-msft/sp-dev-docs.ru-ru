# <a name="context-token-oauth-flow-for-sharepoint-add-ins"></a><span data-ttu-id="07f2c-101">Поток контекста токена OAuth для надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="07f2c-101">Context Token OAuth flow for SharePoint Add-ins</span></span>
<span data-ttu-id="07f2c-102">В этой статье рассказывается о потоке проверки подлинности и авторизации OAuth для надстроек с низким уровнем доверия в SharePoint, размещаемых у поставщика.</span><span class="sxs-lookup"><span data-stu-id="07f2c-102">Learn about the OAuth authentication and authorization flow for low-trust, provider-hosted add-ins in SharePoint.</span></span>
 

 <span data-ttu-id="07f2c-p101">**Примечание.** В настоящее время идет процесс замены названия "приложения для SharePoint" названием "надстройки SharePoint". Во время этого процесса в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio может по-прежнему использоваться термин "приложения для SharePoint". Дополнительные сведения см. в статье [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="07f2c-p101">The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span></span>
 


## <a name="get-an-overview-of-oauth-and-sharepoint-provider-hosted-sharepoint-add-ins"></a><span data-ttu-id="07f2c-106">Получение общих сведений о надстройках SharePoint, размещаемых у поставщиков OAuth и SharePoint</span><span class="sxs-lookup"><span data-stu-id="07f2c-106">Get an overview of OAuth and SharePoint provider-hosted SharePoint Add-ins</span></span>
<span data-ttu-id="07f2c-107"><a name="OAuth_Actors"> </a></span><span class="sxs-lookup"><span data-stu-id="07f2c-107"></span></span>

<span data-ttu-id="07f2c-p102">В SharePoint **поток проверки подлинности и авторизации OAuth для надстройки, размещаемой у поставщика, с низким уровнем доверия включает ряд операций взаимодействия между надстройкой, SharePoint, сервером авторизации и браузером** во время выполнения надстройки. В качестве сервера авторизации в этом случае выступает Служба контроля доступа (ACS) Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="07f2c-p102">In SharePoint, **the OAuth authentication and authorization flow for a provider-hosted, low-trust, add-in involves a series of interactions between your add-in, SharePoint, the authorization server, and the browser** at runtime. The authorization server in this scenario is Microsoft Azure Access Control Service (ACS).</span></span>
 

 
<span data-ttu-id="07f2c-p103">Размещаемая у поставщика надстройка представляет собой удаленное веб-приложение или службу, отдельные от SharePoint и не входящие в состав фермы SharePoint или клиента SharePoint Online. Она может быть размещена в облаке или на локальном сервере. В этой статье удаленный компонент называется Contoso.com.</span><span class="sxs-lookup"><span data-stu-id="07f2c-p103">With a provider-hosted add-in, you have a remote web application or service that is separate from SharePoint, and not part of the SharePoint farm or SharePoint Online tenancy. It can be hosted in the cloud or on an on-premise server. In this article, the remote component is called Contoso.com.</span></span>
 

 

 <span data-ttu-id="07f2c-p104">**Примечание.** В удаленном компоненте также могут размещаться приемники событий, реагирующие на события, которые происходят с элементами SharePoint, например со списками или элементами списков. Примеры удаленных событий, на которые может реагировать Contoso.com: события списков, например добавление или удаление элемента списка, а также веб-события, например добавление или удаление сайта. Дополнительные сведения о создании удаленных приемников событий см. в статье [Создание удаленного приемника событий в надстройках SharePoint](create-a-remote-event-receiver-in-sharepoint-add-ins).</span><span class="sxs-lookup"><span data-stu-id="07f2c-p104">**Note** The remote component can also host event receivers that respond to events that occur to SharePoint items, such as lists or list items. Examples of remote events that Contoso.com might want to respond to are list events, such as adding or removing a list item; or web events, such as adding or deleting a site. For more information about how to create remote event receivers, see  [Create a remote event receiver in SharePoint Add-ins](create-a-remote-event-receiver-in-sharepoint-add-ins).</span></span>
 

<span data-ttu-id="07f2c-p105">Для вызовов SharePoint в Contoso.com используется клиентская объектная модель (CSOM) SharePoint или интерфейсы REST API SharePoint. В надстройке Contoso.com для проверки подлинности SharePoint используется поток обработки маркеров OAuth. **SharePoint и Contoso.com не являются доверенными между собой, но доверяют ACS** и принимают маркеры, выданные ACS. При этом используется три маркера: SharePoint запрашивает у ACS создание маркера контекста, который SharePoint пересылает в Constoso.com. Contoso.com проверяет, выдан ли маркер контекста ACS, чтобы можно было доверять ему. Затем Contoso.com извлекает маркер обновления из маркера контекста и использует его для получения маркера доступа непосредственно от ACS. Он включает маркер доступа во всех своих запросах в SharePoint. SharePoint проверяет, выдан ли маркер доступа ACS, чтобы отвечать на запросы от Contoso.com.</span><span class="sxs-lookup"><span data-stu-id="07f2c-p105">Contoso.com uses the SharePoint client object model (CSOM) or the SharePoint REST APIs to make calls to SharePoint. The Contoso.com application uses an OAuth token-passing flow to authenticate with SharePoint. **SharePoint and Contoso.com do not trust each other; but both trust ACS** and will accept tokens issued by ACS. There are three tokens involved: SharePoint has ACS create a context token that SharePoint forwards to Constoso.com. Contoso.com validates that the context token was issued by ACS so it trusts it. Contoso.com then extracts a refresh token from the context token and uses it to get an access token directly from ACS. It includes the access token in all its requests to SharePoint. SharePoint validates that the access token was issued by ACS, so it responds to the requests from Contoso.com.</span></span>
 

 
 <span data-ttu-id="07f2c-p106">В удаленном компоненте **указывается код обработки маркеров**. (Но если ваш удаленный компонент размещен в .NET, Инструменты разработчика Microsoft Office для Visual Studio предоставляют пример кода, который выполняет за вас основную часть работы.) Подробнее о коде обработки маркеров см. в статье [Обработка маркеров безопасности в надстройках с низким уровнем доверия для SharePoint, размещаемых у поставщика](handle-security-tokens-in-provider-hosted-low-trust-sharepoint-add-ins).</span><span class="sxs-lookup"><span data-stu-id="07f2c-p106">**You provide the token-handling code** in the remote component. (But if your remote component is hosted on .NET, the Microsoft Office Developer Tools for Visual Studio provide sample code that does most of the work for you.) For details about token-handling code, see [Handle security tokens in provider-hosted low-trust SharePoint Add-ins](handle-security-tokens-in-provider-hosted-low-trust-sharepoint-add-ins).</span></span>
 

 

## <a name="complete-the-prerequisites-for-using-the-flow"></a><span data-ttu-id="07f2c-126">Выполнение необходимых условий для использования потока</span><span class="sxs-lookup"><span data-stu-id="07f2c-126">Complete the prerequisites for using the flow</span></span>
<span data-ttu-id="07f2c-127"><a name="Prerequisites"> </a></span><span class="sxs-lookup"><span data-stu-id="07f2c-127"></span></span>

<span data-ttu-id="07f2c-128">Существует несколько действий, которые необходимо выполнить, прежде чем надстройка SharePoint сможет использовать поток маркера контекста.</span><span class="sxs-lookup"><span data-stu-id="07f2c-128">There are some preliminary steps that must be done before a SharePoint Add-in can use the Context Token flow.</span></span> 
 

 

- <span data-ttu-id="07f2c-129">Если Надстройка SharePoint устанавливается в локальной ферме SharePoint, некоторые требования к установке не применяются для приложений, устанавливаемых только в SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="07f2c-129">If the SharePoint Add-in is to be installed to an on-premise SharePoint farm, there are setup requirements that don't apply if it is only installed to SharePoint Online:</span></span>
    
      - <span data-ttu-id="07f2c-p107">**Необходимо настроить ферму** так, чтобы она поддерживала надстройки. (На самом деле это необходимо для установки любых надстроек SharePoint в ферме, даже тех, которые не используют поток маркеров контекста). Дополнительные сведения см. в статье [Настройка среды надстроек SharePoint](http://technet.microsoft.com/en-us/library/fp161236%28v=office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="07f2c-p107">The **farm must be configured** to support add-ins. (This is actually a requirement for installing any SharePoint Add-ins to the farm, even if they don't use the Context Token flow.) For more information, see [Configure an environment for SharePoint Add-ins](http://technet.microsoft.com/en-us/library/fp161236%28v=office.15%29.aspx).</span></span>
    
 
  - <span data-ttu-id="07f2c-p108">У **клиента**, устанавливающего надстройку, **должна быть учетная запись Office 365**. Это необходимо для получения доступа к ACS. Клиенту необязательно использовать свою учетную запись для других целей.</span><span class="sxs-lookup"><span data-stu-id="07f2c-p108">The **customer** who is installing the add-in **must have an Office 365 account**. This is necessary to get access to ACS. The customer does not have to use their account for any other purpose.</span></span>
    
 
  - <span data-ttu-id="07f2c-p109">Ферму необходимо настроить для совместного использования отношения доверия Office 365 к ACS. Это можно легко сделать с помощью скриптов Windows PowerShell. Подробнее см. в статье  [Использование сайта Office 365 SharePoint для авторизации размещенных у поставщика надстроек на локальном сайте SharePoint](use-an-office-365-sharepoint-site-to-authorize-provider-hosted-add-ins-on-an-on-premises-sharepoint-site).</span><span class="sxs-lookup"><span data-stu-id="07f2c-p109">The farm must be configured to share the trust relationship that Office 365 has with ACS. This is easily done with Windows PowerShell scripts. For details, see  [Use an Office 365 SharePoint site to authorize provider-hosted add-ins on an on-premises SharePoint site](use-an-office-365-sharepoint-site-to-authorize-provider-hosted-add-ins-on-an-on-premises-sharepoint-site).</span></span>
    
 
- <span data-ttu-id="07f2c-p110">Независимо от того, где установлена надстройка (в SharePoint Online или в локальной ферме SharePoint), **необходимо зарегистрировать надстройку SharePoint в ACS**. Дополнительные сведения о том, как сделать это, см. в статье [Регистрация надстроек SharePoint 2013](register-sharepoint-add-ins-2013). Помимо прочего, в ходе регистрации надстройка предоставляет ACS свой идентификатор клиента и секрет клиента.</span><span class="sxs-lookup"><span data-stu-id="07f2c-p110">Regardless of whether the add-in is installed to SharePoint Online or to an on-premise SharePoint farm, the **SharePoint Add-in must be registered with ACS**. For details about how this can be done, see [Register SharePoint Add-ins 2013](register-sharepoint-add-ins-2013). Among other things, the add-in provides ACS with its client ID and client secret as part of the registration.</span></span>
    
 

## <a name="see-the-steps-in-the-context-token-flow"></a><span data-ttu-id="07f2c-141">Просмотр действий в потоке маркера контекста</span><span class="sxs-lookup"><span data-stu-id="07f2c-141">See the steps in the Context Token flow</span></span>
<span data-ttu-id="07f2c-142"><a name="OAuth_ProcessFlowSteps"> </a></span><span class="sxs-lookup"><span data-stu-id="07f2c-142"></span></span>

<span data-ttu-id="07f2c-143">На рисунке ниже показан поток проверки подлинности и авторизации OAuth для надстроек SharePoint, размещаемых у поставщика.</span><span class="sxs-lookup"><span data-stu-id="07f2c-143">The OAuth authentication and authorization flow for a SharePoint provider-hosted add-in is shown in the following figure.</span></span>
 

 

<span data-ttu-id="07f2c-144">**Поток маркеров контекста OAuth**</span><span class="sxs-lookup"><span data-stu-id="07f2c-144">**OAuth Context Token flow**</span></span>

 

 
![Процесс авторизации OAuth](../../images/833fcdcc-1755-438b-9ada-dce9646564c0.gif)
 
<span data-ttu-id="07f2c-146">Вот этапы, соответствующие номерам на рисунке.</span><span class="sxs-lookup"><span data-stu-id="07f2c-146">These are the steps that correspond to the numbers in the figure:</span></span>
 

 

 

1. <span data-ttu-id="07f2c-p111">Пользователь запускает надстройку SharePoint из SharePoint. Конструкция надстройки определяет способ запуска.</span><span class="sxs-lookup"><span data-stu-id="07f2c-p111">A user launches the SharePoint Add-in from SharePoint. The design of the add-in determines how this is done:</span></span>
    
      - <span data-ttu-id="07f2c-p112">Если надстройка получает доступ к удаленному веб-приложению (в Contoso.com) в веб-части надстройки (по сути, представляющей собой оболочку вокруг **IFRAME**), запуск надстройки означает только переход на страницу SharePoint, содержащую веб-часть надстройки. Если пользователь еще не вошел в систему, SharePoint предлагает это сделать. SharePoint обрабатывает страницу и обнаруживает, что на ней есть компонент из надстройки Contoso.com. (Дополнительные сведения о веб-частях надстроек см. в статье  [Создание веб-частей надстройки для установки совместно с надстройкой для SharePoint](create-add-in-parts-to-install-with-your-sharepoint-add-in).)</span><span class="sxs-lookup"><span data-stu-id="07f2c-p112">If the add-in is designed to surface the remote web application (at Contoso.com) in an add-in part (which is essentially a wrapper around an **IFRAME**), then launching the add-in simply means navigating to a SharePoint page that contains the add-in part. (If the user is not already logged on, SharePoint prompts the user to log on.) SharePoint processes the page and detects that there is a component from the Contoso.com application on the page. (For details about add-in parts, see  [Create add-in parts to install with your SharePoint Add-in](create-add-in-parts-to-install-with-your-sharepoint-add-in).)</span></span>
    
 
  - <span data-ttu-id="07f2c-p113">Если надстройка использует полную страницу в браузере, пользователь запускает ее, щелкая соответствующую плитку надстройки на странице **Содержимое сайта** веб-сайта SharePoint. (Надстройка также может включать настраиваемое меню или элемент ленты, запускающий удаленный компонент.)</span><span class="sxs-lookup"><span data-stu-id="07f2c-p113">If the add-in is designed to use as a full page in the browser, then the user launches it by clicking on its add-in tile on the SharePoint website's **Site Contents** page. (A variation of this is when the add-in includes a custom menu or ribbon item that launches the remote component.)</span></span>
    
 
2. <span data-ttu-id="07f2c-p114">Независимо от того, как запускается надстройка, среде SharePoint требуется получить маркер контекста, который она может отправить приложению Contoso.com. Поэтому она посылает запрос в ACS на создание маркера контекста, содержащего сведения о контексте SharePoint, в том числе о текущем пользователе и URL-адресе удаленного приложения, а также другую информацию. Маркер контекста также содержит зашифрованный маркер обновления.</span><span class="sxs-lookup"><span data-stu-id="07f2c-p114">Regardless of how the add-in is launched, SharePoint must get a context token that it can send to the Contoso.com application, so it asks ACS to create a context token that contains information about the SharePoint context including the current user, the remote application URL, and other information. The context token also contains an encrypted refresh token.</span></span>
    
 
3. <span data-ttu-id="07f2c-p115">ACS подписывает маркер контекста с помощью алгоритма, использующего секрет надстройки Contoso.com, и возвращает его в SharePoint. Этот секрет знают только ACS и надстройка Contoso.com.</span><span class="sxs-lookup"><span data-stu-id="07f2c-p115">ACS signs the context token, with an algorithm that uses the Contoso.com add-in secret, and returns it to SharePoint. Only ACS and the Contoso.com add-in know the secret.</span></span>
    
 
4. <span data-ttu-id="07f2c-p116">Если надстройка Contoso.com доступна в веб-части надстройки, SharePoint отрисовывает страницу, на которой она размещена, и добавляет маркер контекста в URL-адрес, вызываемый **IFRAME** в веб-части надстройки, чтобы получить ее контент. Если надстройка Contoso.com представляет собой полную страницу, SharePoint перенаправляет браузер в Constoso.com и включает маркер контекста в ответ перенаправления.</span><span class="sxs-lookup"><span data-stu-id="07f2c-p116">If the Contoso.com application is surfaced in an add-in part, SharePoint renders the page that hosts the add-in part and adds the context token to the URL that the **IFRAME** in the add-in part calls to get its contents. If the Contoso.com application is full page, SharePoint redirects the browser to Constoso.com and includes the context token as a part of the redirect response.</span></span>
    
 
5. <span data-ttu-id="07f2c-160">Маркер контекста включается в запрос браузера, отправляемый на сервер Contoso.com.</span><span class="sxs-lookup"><span data-stu-id="07f2c-160">The context token is included in the browser request that is sent to the Contoso.com server.</span></span>
    
 
6. <span data-ttu-id="07f2c-p117">Сервер Contoso.com получает маркер контекста и проверяет подпись, зная секрет клиента. Таким образом Contoso.com получает подтверждение, что маркер выдан ACS, а не мошенническим сайтом, выдающим себя за SharePoint. Contoso.com извлекает маркер обновления из маркера контекста и отправляет его ACS вместе с другой информацией, включая идентификатор и секрет клиента, в запросе маркера доступа к SharePoint.</span><span class="sxs-lookup"><span data-stu-id="07f2c-p117">The Contoso.com server gets the context token and validates the signature which it can do because it knows the client secret. This assures Contoso.com that the token was issued by ACS and not an imposter pretending to be SharePoint. Contoso.com extracts the refresh token from the context token and sends it, along with other information including the its client ID and client secret, to ACS in a request for an access token that will allow it to access SharePoint,</span></span>
    
 
7. <span data-ttu-id="07f2c-p118">ACS проверяет, выдан ли маркер обновления нею, а затем возвращает маркер доступа Contoso.com. Кроме того, Contoso.com может кэшировать этот маркер доступа, чтобы не запрашивать его у ACS при каждом доступе к SharePoint. По умолчанию маркер доступа остается действительным в течение нескольких часов. (На момент написания данной статьи срок действия маркеров доступа, выдаваемых ACS SharePoint, составлял 12 часов, но это значение могло измениться.) Каждый маркер доступа связан с учетной записью пользователя, указанной в исходном запросе на авторизацию, и предоставляет доступ только к той службе (в данном случае SharePoint), которая указана в запросе. Маркеры обновления действуют дольше (шесть месяцев на момент написания) и также могут кэшироваться. Поэтому для получения нового маркера доступа от ACS можно использовать исходный маркер обновления, пока не истечет срок действия самого маркера обновления. (Подробнее о кэшировании маркеров см. в статье  [Обработка маркеров безопасности в надстройках с низким уровнем доверия для SharePoint, размещаемых у поставщика](handle-security-tokens-in-provider-hosted-low-trust-sharepoint-add-ins).) Когда истекает срок действия маркера обновления, Contoso.com может получить новый, получив для этого новый маркер контекста. Подробнее о том, как это делается, см. в статье  [Получение нового маркера контекста](handle-security-tokens-in-provider-hosted-low-trust-sharepoint-add-ins#GetNewContextToken).</span><span class="sxs-lookup"><span data-stu-id="07f2c-p118">ACS validates the refresh token so that it is assured that it issued the token, and then it returns an access token to Contoso.com. Optionally, Contoso.com can cache this access token so it doesn't have ask ACS for an access token every time that it accesses SharePoint. By default, access tokens are good for a few hours at a time. (When this article was written, the default expiration for ACS-issued access tokens to SharePoint was 12 hours, but that could change.) Each access token is specific to the user account that is specified in the original request for authorization, and grants access only to the service (in this case, SharePoint) that is specified in that request. Refresh tokens are longer lived (six months when this article was written) and can also be cached. So, the same refresh token can be redeemed for a new access token from ACS until the refresh token itself expires. (For more information about caching tokens, see  [Handle security tokens in provider-hosted low-trust SharePoint Add-ins](handle-security-tokens-in-provider-hosted-low-trust-sharepoint-add-ins).) When the refresh token expires, the Contoso.com can get a new one by obtaining a new context token. For details about how this is done, see  [Get a new context token](handle-security-tokens-in-provider-hosted-low-trust-sharepoint-add-ins#GetNewContextToken).</span></span>
    
 
8. <span data-ttu-id="07f2c-p119">Contoso.com использует маркер доступа для вызова REST API SharePoint или отправки запроса CSOM к spnv. Для этого он передает маркер доступа OAuth в заголовке HTTP **Authorization**. (Если ваш удаленный компонент размещен на платформе .NET, то для создания заголовка вы можете использовать пример кода, имеющийся в Инструментах разработчика Office для Visual Studio.)</span><span class="sxs-lookup"><span data-stu-id="07f2c-p119">Contoso.com uses the access token to make a SharePoint REST API call or CSOM request to spnv. It does this by passing the OAuth access token in the HTTP **Authorization** header. (Sample code for creating the header is provided in the Office Developer Tools for Visual Studio if your remote component is hosted on a .NET platform.</span></span>
    
 
9. <span data-ttu-id="07f2c-p120">SharePoint проверяет, выдан ли маркер доступа ACS, а затем отправляет в приложение Contoso.com запрошенные им данные или выполняет операцию создания, чтения, обновления или удаления (CRUD), запрошенную Contoso.com.</span><span class="sxs-lookup"><span data-stu-id="07f2c-p120">SharePoint validates the access token so that it is assured the token was issued by ACS. It then sends the data that Contoso.com requested to Contoso.com or performs the create, read, update, or delete (CRUD) operation that Contoso.com requested.</span></span>
    
 
10. <span data-ttu-id="07f2c-177">Страница надстройки Contoso.com отрисовывается в браузере (или в **IFRAME** веб-части надстройки).</span><span class="sxs-lookup"><span data-stu-id="07f2c-177">The Contoso.com application page renders in the browser (or in the **IFRAME** of the add-in part).</span></span>
    
 

## <a name="additional-resources"></a><span data-ttu-id="07f2c-178">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="07f2c-178">Additional resources</span></span>
<span data-ttu-id="07f2c-179"><a name="Filename_AdditionalResources"> </a></span><span class="sxs-lookup"><span data-stu-id="07f2c-179"></span></span>


-  [<span data-ttu-id="07f2c-180">Авторизация и проверка подлинности надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="07f2c-180">Authorization and authentication of SharePoint Add-ins</span></span>](authorization-and-authentication-of-sharepoint-add-ins)
    
 
-  [<span data-ttu-id="07f2c-181">Разрешения для надстроек в SharePoint</span><span class="sxs-lookup"><span data-stu-id="07f2c-181">Add-in permissions in SharePoint</span></span>](add-in-permissions-in-sharepoint-2013)
    
 
-  [<span data-ttu-id="07f2c-182">Важные аспекты разработки и архитектуры для надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="07f2c-182">Important aspects of the SharePoint Add-in architecture and development landscape</span></span>](important-aspects-of-the-sharepoint-add-in-architecture-and-development-landscape)
    
 
-  [<span data-ttu-id="07f2c-183">Знакомство с созданием надстроек SharePoint с размещением в SharePoint</span><span class="sxs-lookup"><span data-stu-id="07f2c-183">Get started creating SharePoint-hosted SharePoint Add-ins</span></span>](get-started-creating-sharepoint-hosted-sharepoint-add-ins)
    
 

