# <a name="creating-sharepoint-add-ins-that-use-low-trust-authorization"></a><span data-ttu-id="c542a-101">Создание надстроек SharePoint, использующих авторизацию с низким уровнем доверия</span><span class="sxs-lookup"><span data-stu-id="c542a-101">Creating SharePoint Add-ins that use low-trust authorization</span></span>
<span data-ttu-id="c542a-102">Сведения о системе авторизации с низким уровнем доверия для надстроек SharePoint.</span><span class="sxs-lookup"><span data-stu-id="c542a-102">Learn about the low-trust authorization system for SharePoint Add-ins.</span></span>
 

 <span data-ttu-id="c542a-p101">**Примечание.** Название "приложения для SharePoint" меняется на "надстройки SharePoint". Пока изменения не будут внесены полностью, в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio по-прежнему может встречаться термин "приложение". Дополнительные сведения см. в статье [Название "приложения для Office и SharePoint" изменилось на "надстройки Office и SharePoint"](new-name-for-apps-for-sharepoint#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="c542a-p101">The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span></span>
 

<span data-ttu-id="c542a-p102">Удаленные компоненты в надстройке SharePoint (или внешнем приложении) могут получить авторизацию для ресурсов SharePoint, передавая маркер доступа в SharePoint с каждым HTTP-запросом. Удаленные компоненты получают маркер доступа от учетной записи службы контроля доступа Microsoft Azure (ACS), связанной с областью клиентов Office 365 клиента. Azure ACS действует как сервер авторизации в транзакции [OAuth 2.0](http://oauth.net/), называемой потоком. При этом SharePoint служит сервером ресурсов, а удаленные компоненты клиентом. Спецификации протокола см. на веб-странице [Протокол веб-авторизации (oauth)](http://datatracker.ietf.org/doc/active/#oauth).</span><span class="sxs-lookup"><span data-stu-id="c542a-p102">Learn about the low-trust authorization system for SharePoint Add-ins. Remote components in a SharePoint Add-in (or external application) can gain authorization to SharePoint resources by passing an access token to SharePoint with each HTTP request. The remote components obtain the access token from a Microsoft Azure Access Control Service (ACS) account that is associated with the customer's Office 365 tenancy. Azure ACS acts as the authorization server in an  [OAuth 2.0](http://oauth.net/) transaction, called aflow, with SharePoint as the resource server and the remote components as the client. For related protocol specifications, see  [Web Authorization Protocol (oauth)](http://datatracker.ietf.org/doc/active/#oauth).</span></span> 
 

<span data-ttu-id="c542a-p103">Надстройки для SharePoint с размещением у поставщика, которые используют систему авторизации с низким уровнем доверия, можно продавать в Магазин Office и устанавливать в Microsoft SharePoint Online или в локальной ферме SharePoint, настроенной для использования области клиентов Office 365 для установки доверия с использованием Azure ACS. У пользователя должна быть область клиентов Office 365 для установки надстроек для SharePoint, которые используют систему с низким уровнем доверия. Но пользователю не обязательно применять область клиентов в других целях. Инструкции по связыванию локальной фермы с областью клиентов Office 365 см. в разделе  [Использование сайта Office 365 SharePoint для авторизации размещенных у поставщика надстроек на локальном сайте SharePoint](use-an-office-365-sharepoint-site-to-authorize-provider-hosted-add-ins-on-an-on-premises-sharepoint-site).</span><span class="sxs-lookup"><span data-stu-id="c542a-p103">Provider-hosted SharePoint Add-ins that use low-trust authorization system can be sold in the Office Store and installed on either Microsoft SharePoint Online or an on-premise SharePoint farm that has been configured to use the customer's Office 365 tenancy to establish trust with Azure ACS. The customer must have an Office 365 tenancy to install SharePoint Add-ins that use the low-trust system. However, it is not necessary for the customer to use the tenancy for any other purpose. For instructions about linking an on-premise farm to a Office 365 tenancy, see  [Use an Office 365 SharePoint site to authorize provider-hosted add-ins on an on-premises SharePoint site](use-an-office-365-sharepoint-site-to-authorize-provider-hosted-add-ins-on-an-on-premises-sharepoint-site).</span></span>
 


## <a name="registration-with-azure-acs"></a><span data-ttu-id="c542a-114">Регистрация в Azure ACS</span><span class="sxs-lookup"><span data-stu-id="c542a-114">Registration with Azure ACS</span></span>
<span data-ttu-id="c542a-115"><a name="Registration"> </a></span><span class="sxs-lookup"><span data-stu-id="c542a-115"></span></span>

<span data-ttu-id="c542a-p104">Чтобы использовать систему с низким уровнем доверия, сначала необходимо зарегистрировать надстройку для SharePoint в Azure ACS и в службе управления приложениями фермы SharePoint или области клиентов SharePoint Online. ("Служба управления приложениями" получила такое название, так как надстройки SharePoint ранее назывались "приложениями для SharePoint".) Надстройки, для продажи которых используется Магазин Office, регистрируются в ACS на Панели мониторинга продаж, при этом регистрация с помощью службы происходит во время установки надстройки. Если надстройки распространяются через каталог надстроек организации, они регистрируются в ACS и службе на странице \_Layouts\15\AppRegNew.aspx любой области клиентов SharePoint или фермы, в которой устанавливается надстройка. Кроме того, необходимо зарегистрировать внешние приложения (не для SharePoint), обращающиеся к SharePoint. К ним относятся надстройки Office, приложения Магазина Windows, веб-приложения и приложения для устройств, например для смартфонов.</span><span class="sxs-lookup"><span data-stu-id="c542a-p104">To use the low-trust system, the SharePoint Add-in must first be registered with Azure ACS and with the App Management Service of the SharePoint farm or SharePoint Online tenancy. (It is called "App Management Service" because SharePoint Add-ins were originally called "apps for SharePoint".) For add-ins that are sold through the Office Store, registration to ACS is performed in the Seller Dashboard and registration with the service is performed when the add-in is installed. For add-ins that are distributed in the organization add-in catalog, registration to both ACS and the service is performed on the _Layouts15\_AppRegNew.aspx page of any SharePoint tenancy or farm where the add-in is to be installed. External, non- SharePoint, applications that access SharePoint, also need to be registered. This category includes Office Add-ins, Windows Store apps, web applications, and device apps such as smartphone apps.</span></span>
 

 

 <span data-ttu-id="c542a-p105">**Примечание.** Для регистрации необходимо, чтобы у приложения был интернет-домен. Для этой цели можно использовать любой существующий домен, но невозможно быть полностью уверенным в том, что домен, который вам не принадлежит, будет существовать всегда. Поэтому веб-приложение должно быть частью приложения для устройства, даже если компонент веб-приложения используется только для регистрации. Расширенный пример кода с таким подходом см. в статье [Пакетная подготовка сайтов с использованием модели надстроек](http://code.msdn.microsoft.com/Provision-sites-in-batches-fcf31bc6).</span><span class="sxs-lookup"><span data-stu-id="c542a-p105">**Note** Registration requires that the application have an Internet domain. Any existing domain can be used for this purpose, but you can't be 100% certain that any domain you don't own will always exist, so a web application would need to be part of a native device application even if the web application component played no other role than to enable registration. For an advanced code sample that is designed in this way, see  [Provision sites in batches with the add-in model](http://code.msdn.microsoft.com/Provision-sites-in-batches-fcf31bc6).</span></span>
 

<span data-ttu-id="c542a-124">Дополнительные сведения о регистрации см. в статье [Регистрация надстроек SharePoint 2013](register-sharepoint-add-ins-2013).</span><span class="sxs-lookup"><span data-stu-id="c542a-124">For more information on registration, see  [Register SharePoint Add-ins 2013](register-sharepoint-add-ins-2013).</span></span>
 

 

### <a name="add-in-secret-expiration"></a><span data-ttu-id="c542a-125">Окончание срока действия секрета надстройки</span><span class="sxs-lookup"><span data-stu-id="c542a-125">Add-in secret expiration</span></span>

<span data-ttu-id="c542a-p106">Секрет надстройки необходимо менять каждые 12 месяцев. Подробнее об этом см. в статье [Замена секрета клиента в надстройке SharePoint с истекающим сроком действия](replace-an-expiring-client-secret-in-a-sharepoint-add-in).</span><span class="sxs-lookup"><span data-stu-id="c542a-p106">The add-in secret must be replaced every 12 months. For details, see  [Replace an expiring client secret in a SharePoint Add-in](replace-an-expiring-client-secret-in-a-sharepoint-add-in).</span></span>
 

 

## <a name="authorization-policies"></a><span data-ttu-id="c542a-128">Политики авторизации</span><span class="sxs-lookup"><span data-stu-id="c542a-128">Authorization policies</span></span>
<span data-ttu-id="c542a-129"><a name="Policies"> </a></span><span class="sxs-lookup"><span data-stu-id="c542a-129"></span></span>

<span data-ttu-id="c542a-130">Надстройка SharePoint может использовать одну из двух политик авторизации:</span><span class="sxs-lookup"><span data-stu-id="c542a-130">A SharePoint Add-in can be designed to use either of two authorization policies:</span></span>
 

 

-  <span data-ttu-id="c542a-p107">**Политика для пользователя и надстройки.** Надстройки, использующие эту политику, могут выполнять только те действия, на которые и у пользователя, и у надстройки есть разрешения. Это политика по умолчанию, которая используется, если разработчик явно не назначит другую политику.</span><span class="sxs-lookup"><span data-stu-id="c542a-p107">**User + add-in Policy:** Add-ins that use this policy can only perform actions that both the add-in and the user have permission to do. This is the default policy that is used unless the developer takes specific steps to use the other.</span></span>
    
 
-  <span data-ttu-id="c542a-p108">**Политика только для надстройки.** Надстройки, использующие эту политику, могут выполнять любые действия, для которых у них есть разрешения, даже если у пользователя нет таких разрешений. Разработчику следует запросить применение этой политики в манифесте надстройки. Пользователь, устанавливающий надстройку, должен утвердить такой запрос. Эта политика разрешена только для надстроек для SharePoint с размещением у поставщика.</span><span class="sxs-lookup"><span data-stu-id="c542a-p108">**App-only Policy:** Add-ins that use this policy can perform any action that it has permission to do, even if the user does not have permission for the action. The developer must request that this policy be used in the add-in manifest of the add-in. The request must be approved by the user who installs the add-in. This policy is allowed for only provider-hosted SharePoint Add-ins.</span></span>
    
 
<span data-ttu-id="c542a-137">Дополнительные сведения о политиках авторизации см. в статье [Типы политик авторизации надстроек в SharePoint](add-in-authorization-policy-types-in-sharepoint-2013).</span><span class="sxs-lookup"><span data-stu-id="c542a-137">For more information about authorization policies, see  [Add-in authorization policy types in SharePoint](add-in-authorization-policy-types-in-sharepoint-2013).</span></span>
 

 

## <a name="two-oauth-runtime-flows"></a><span data-ttu-id="c542a-138">Два потока среды выполнения OAuth</span><span class="sxs-lookup"><span data-stu-id="c542a-138">Two OAuth runtime flows</span></span>
<span data-ttu-id="c542a-139"><a name="Flows"> </a></span><span class="sxs-lookup"><span data-stu-id="c542a-139"></span></span>

<span data-ttu-id="c542a-p109">При каждом запуске надстройки для SharePoint с размещением в облаке или внешнего приложения, обращающихся к SharePoint, возникает поток (ряд операций взаимодействия между надстройкой, SharePoint, ACS и иногда конечным пользователем). В результате SharePoint получает маркер доступа, включенный в каждый запрос на создание, обновление или удаление (CRUD), который приложение отправляет в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="c542a-p109">Each time a cloud-hosted SharePoint Add-in or external application that is accessing SharePoint is run, a flow -- a series of interactions between the add-in, SharePoint, ACS, and sometimes the end user -- occurs. The end result of the flow is that SharePoint receives an access token included with each create, update, delete (CRUD) request that the application makes to SharePoint.</span></span>
 

 
<span data-ttu-id="c542a-p110">Существует два основных потока OAuth, которые используются SharePoint. Один предназначен для размещенных в облаке надстроек для SharePoint, а другой, который называют "динамическим" для приложений на других платформах, получающих доступ к данным SharePoint.</span><span class="sxs-lookup"><span data-stu-id="c542a-p110">There are two major OAuth flows used by SharePoint. One is for cloud-hosted SharePoint Add-ins. The other, called "on the fly," is for applications on other platforms that access SharePoint data.</span></span>
 

 

-  <span data-ttu-id="c542a-p111">**Поток маркеров контекста**. Удаленный компонент, входящий в надстройку для SharePoint, использует клиентскую объектную модель (CSOM) SharePoint или конечные точки REST для вызова SharePoint. SharePoint запрашивает маркер контекста у ACS, который он может отправить удаленному серверу. Удаленный сервер использует маркер контекста, чтобы запросить маркер доступа у ACS. Затем удаленный сервер использует маркер доступа для обратного вызова SharePoint. Дополнительные сведения см. в разделе  [Поток маркеров контекста OAuth для надстроек в SharePoint](context-token-oauth-flow-for-sharepoint-add-ins).</span><span class="sxs-lookup"><span data-stu-id="c542a-p111">**Context Token flow:** The remote component of the SharePoint Add-in uses the SharePoint client object model (CSOM) or REST endpoints to make calls to SharePoint. SharePoint requests a context token from ACS that it can send to the remote server. The remote server uses the context token to request an access token from the ACS. The remote server then uses the access token to talk back to SharePoint. For details about this flow, see [Context Token OAuth flow for SharePoint Add-ins](context-token-oauth-flow-for-sharepoint-add-ins).</span></span>
    
 
-  <span data-ttu-id="c542a-p112">**Поток кода проверки подлинности.** Во время своей установки Надстройка SharePoint получает необходимые разрешения для ресурсов SharePoint. Но приложения, не установленные в SharePoint, должны запрашивать разрешения динамически, т. е. при каждом запуске. В этом потоке маркер контекста SharePoint отсутствует. Вместо этого, когда приложение запускается и пытается получить доступ к SharePoint, SharePoint запрашивает у пользователя разрешения для приложения. Когда пользователь предоставляет разрешения, SharePoint получает код авторизации от ACS, который затем передает приложению. Приложение использует этот код, чтобы получить маркер доступа у ACS, который затем использует для связи с SharePoint. Дополнительные сведения об этом потоке см. в разделе [Поток кода аутентификации OAuth для надстроек в SharePoint](authorization-code-oauth-flow-for-sharepoint-add-ins).</span><span class="sxs-lookup"><span data-stu-id="c542a-p112">**Authenticaton Code flow:** a SharePoint Add-in is granted the permissions it needs to SharePoint resources when it is installed. But applications that are not installed on SharePoint must ask for permissions "on the fly," that is, each time they run. There is no SharePoint context token in this flow. Instead, when the add-in runs and attempts to access SharePoint, SharePoint prompts the user to grant the permissions to the application that it is requesting. When the user grants the permissions, SharePoint obtains an authorization code from ACS which it passes to the application. The application uses the code to obtain an access token from ACS which it can then use to talk to SharePoint. For details about this flow, see [Authorization Code OAuth flow for SharePoint Add-ins](authorization-code-oauth-flow-for-sharepoint-add-ins).</span></span>
    
 

## <a name="troubleshooting-low-trust-sharepoint-add-ins"></a><span data-ttu-id="c542a-157">Устранение неполадок надстроек SharePoint с низким уровнем доверия</span><span class="sxs-lookup"><span data-stu-id="c542a-157">Troubleshooting low-trust SharePoint Add-ins</span></span>
<span data-ttu-id="c542a-158"><a name="Trouble"> </a></span><span class="sxs-lookup"><span data-stu-id="c542a-158"></span></span>

<span data-ttu-id="c542a-159">Эта статья содержит некоторые общие рекомендации по устранению неполадок и сведения об определенных проблемах с надстройками SharePoint, которые используют систему авторизации с низким уровнем доверия.</span><span class="sxs-lookup"><span data-stu-id="c542a-159">This article provides some general troubleshooting guidance and information about some specific issues with SharePoint Add-ins that use the low-trust authorization system.</span></span>
 

 

### <a name="use-the-fiddler-tool"></a><span data-ttu-id="c542a-160">Использование средства Fiddler</span><span class="sxs-lookup"><span data-stu-id="c542a-160">Use the Fiddler tool</span></span>

<span data-ttu-id="c542a-p113">С помощью бесплатного  [средства Fiddler](http://www.telerik.com/fiddler) можно захватывать HTTP-запросы, отправленные удаленным компонентом вашей надстройки в SharePoint. Для этого [средства есть бесплатное расширение](https://github.com/andrewconnell/SPOAuthFiddlerExt), автоматически декодирующее маркеры доступа в запросах.</span><span class="sxs-lookup"><span data-stu-id="c542a-p113">The free  [Fiddler tool](http://www.telerik.com/fiddler) can be used to capture the HTTP Requests sent by the remote component of your add-in to SharePoint. There is a [free extension to the tool](https://github.com/andrewconnell/SPOAuthFiddlerExt) that automatically decodes the access tokens in the requests.</span></span>
 

 

### <a name="turn-off-the-https-requirement-for-oauth-during-development"></a><span data-ttu-id="c542a-163">Отключение требования использовать протокол HTTPS для OAuth во время разработки</span><span class="sxs-lookup"><span data-stu-id="c542a-163">Turn off the HTTPS requirement for OAuth during development</span></span>
<span data-ttu-id="c542a-164"><a name="TurnOffHTTPRequirement"> </a></span><span class="sxs-lookup"><span data-stu-id="c542a-164"></span></span>

<span data-ttu-id="c542a-p114">Для применения OAuth требуется, чтобы служба SharePoint и SharePoint использовали протокол HTTPS. Это мешает при разработке надстройки. Например, вы можете получить сообщение об ошибке 403 ("Запрещено") при попытке вызова SharePoint во время отладки надстройки, так как на компьютере localhost, на котором запущена ваша надстройка, нет поддержки SSL.</span><span class="sxs-lookup"><span data-stu-id="c542a-p114">OAuth requires SharePoint to run HTTPS (not only your service, but SharePoint too). This can get in the away when you are developing the add-in. For example, you may get a 403 (forbidden) message when attempting to make a call to SharePoint when debugging the add-in because the SSL support is not present in the "localhost" where your add-in is running.</span></span>
 

 
<span data-ttu-id="c542a-168">Вы можете отключить обязательное использование HTTPS при разработке с помощью указанных ниже командлетов Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c542a-168">You can turn off the HTTPS requirement during development using the following Windows PowerShell cmdlets.</span></span>
 

 



```
$serviceConfig = Get-SPSecurityTokenServiceConfig
$serviceConfig.AllowOAuthOverHttp = $true
$serviceConfig.Update()

```

<span data-ttu-id="c542a-169">Чтобы позже снова включить обязательное использование HTTPS, воспользуйтесь указанными ниже командлетами Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c542a-169">To turn the HTTPS requirement back on later, use the following Windows PowerShell cmdlets.</span></span>
 

 



```
$serviceConfig = Get-SPSecurityTokenServiceConfig
$serviceConfig.AllowOAuthOverHttp = $false
$serviceConfig.Update()

```


### <a name="miscellaneous-ssl-and-domain-related-authorization-errors"></a><span data-ttu-id="c542a-170">Прочие ошибки авторизации, связанные с протоколом SSL и доменами</span><span class="sxs-lookup"><span data-stu-id="c542a-170">Miscellaneous SSL and domain-related authorization errors</span></span>
<span data-ttu-id="c542a-171"><a name="DomainRelatedErrors"> </a></span><span class="sxs-lookup"><span data-stu-id="c542a-171"></span></span>

<span data-ttu-id="c542a-p115">Авторизации может препятствовать несовпадение доменных имен в файлах конфигурации и регистрационных формах. Следующие четыре значения должны полностью совпадать:</span><span class="sxs-lookup"><span data-stu-id="c542a-p115">A mismatch of domain names in configuration files and registration forms can prevent authorization. The following four values have to be exactly the same:</span></span>
 

 

- <span data-ttu-id="c542a-174">**Домен надстройки**, указываемый при регистрации надстройки SharePoint на странице AppRegNew.aspx или на Панели мониторинга продаж.</span><span class="sxs-lookup"><span data-stu-id="c542a-174">The **Add-in Domain** that is specified when the SharePoint Add-in is registered on either AppRegNew.aspx or Seller Dashboard.</span></span>
    
 
- <span data-ttu-id="c542a-175">Домен, на котором зарегистрирован сертификат безопасности удаленного веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="c542a-175">The domain under which the remote web application's security certificate is registered.</span></span>
    
 
- <span data-ttu-id="c542a-176">Доменная часть значения **StartPage** в файле AppManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="c542a-176">The domain part of the **StartPage** value in the AppManifest.xml file.</span></span>
    
 
- <span data-ttu-id="c542a-177">Доменная часть URL-адресов всех приемников событий, указанных в файле AppManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="c542a-177">The domain part of the URLs of any event receivers specified in the AppManifest.xml.</span></span>
    
 
<span data-ttu-id="c542a-178">В связи с этим учтите указанные ниже особенности.</span><span class="sxs-lookup"><span data-stu-id="c542a-178">In connection with this point, note the following:</span></span>
 

 

- <span data-ttu-id="c542a-p116">Если удаленный компонент вашей надстройки для SharePoint использует какой-либо другой порт, а не порт 443, необходимо явно включить этот порт в качестве части домена во всех четырех местах. Пример:  `contoso.com:3333`. (Необходимо использовать протокол HTTPS, для которого по умолчанию используется порт 443.)</span><span class="sxs-lookup"><span data-stu-id="c542a-p116">If the remote component of your SharePoint Add-in is using any port other than 443, you must explicitly include the port as part of the domain in all four places; for example,  `contoso.com:3333`. (You must use the HTTPS protocol for which the default port is 443.)</span></span>
    
 
- <span data-ttu-id="c542a-p117">Если для своего удаленного веб-приложения вы создаете псевдоним DNS CNAME, укажите псевдоним CNAME для значения домена во всех четырех случаях. Например, если приложение размещено в contoso.cloudapp.net и вы создали для него CNAME contososoftware.com, используйте contososoftware.com в качестве домена.</span><span class="sxs-lookup"><span data-stu-id="c542a-p117">If you create a DNS CNAME alias for your remote web application, use the CNAME alias for the domain value in all four places. For example, if your application is hosted at contoso.cloudapp.net and you create a CNAME of contososoftware.com for it, use contososoftware.com as the domain.</span></span>
    
 
- <span data-ttu-id="c542a-p118">До создания пакета надстройки необходимо задать домен в значении **StartPage** (а также URL-адресе каждого приемника событий) файла AppManifest.xml. Если для создания такого пакета вы используете мастер **публикации** в Visual Studio, то он подскажет вам домен, а Инструменты разработчика Office для Visual Studio автоматически вставят его в значение **StartPage**. То есть маркер `~remoteWebUrl`, который используется при отладке, будет заменен. Но если вы не используете мастер **публикации** (или используете его, но ваше удаленное веб-приложение развернуто в Azure), необходимо вручную заменить маркер на домен (и протокол). Например, на `https://contososoftware.com` или `https://MyCloudVM:3333`).</span><span class="sxs-lookup"><span data-stu-id="c542a-p118">The domain needs to be hardcoded in the **StartPage** value (and any event receiver URLs) of the AppManifest.xml file before the add-in is packaged. If you use the **Publish** wizard in Visual Studio to package the add-in, you will be prompted for the domain and the Office Developer Tools for Visual Studio will insert it into the **StartPage** value for you (in place of the `~remoteWebUrl` token that is used during debugging. But if you are not using the **Publish** wizard, or even if you are but your remote web application is deployed to Azure, you must manually replace the token with the domain (and protocol); for example `https://contososoftware.com` or `https://MyCloudVM:3333`.</span></span>
    
 

### <a name="error-the-underlying-connection-was-closed-could-not-establish-trust-relationship-for-the-ssltls-secure-channel"></a><span data-ttu-id="c542a-186">Ошибка "Базовое соединение закрыто: не удалось установить доверительные отношения для защищенного канала SSL/TLS".</span><span class="sxs-lookup"><span data-stu-id="c542a-186">Error "The underlying connection was closed: Could not establish trust relationship for the SSL/TLS secure channel."</span></span>
<span data-ttu-id="c542a-187"><a name="ErrorConnectionClosed"> </a></span><span class="sxs-lookup"><span data-stu-id="c542a-187"></span></span>

<span data-ttu-id="c542a-p119">Такое сообщение возникает из-за проблемы со связью SSL, а не с OAuth. Убедитесь, что SharePoint доверяет сертификату, который вы используете, и что этот сертификат соответствует имени конечной точки.</span><span class="sxs-lookup"><span data-stu-id="c542a-p119">This error is an SSL handshake issue, not an OAuth issue. Make sure that the certificate you are using is trusted by SharePoint, and that the certificate matches the endpoint name.</span></span>
 

 

### <a name="errors-using-http-dav-method-to-read-files-from-sharepoint"></a><span data-ttu-id="c542a-190">Ошибки при использовании метода HTTP DAV для чтения файлов из SharePoint</span><span class="sxs-lookup"><span data-stu-id="c542a-190">Errors using HTTP DAV method to read files from SharePoint</span></span>
<span data-ttu-id="c542a-191"><a name="ErrorConnectionClosed"> </a></span><span class="sxs-lookup"><span data-stu-id="c542a-191"></span></span>

<span data-ttu-id="c542a-p120">HTTP DAV не работает с OAuth. Если вы используете клиентскую объектную модель (CSOM) SharePoint, то для чтения файла используйте указанный ниже код.</span><span class="sxs-lookup"><span data-stu-id="c542a-p120">HTTP DAV does not work with OAuth. If you are using the SharePoint client object model (CSOM), use the following code to read a file.</span></span>
 

 

```C#
File f = clientContext.Web.GetFileByServerRelativeUrl( url);
ClientResult<Stream> r = f.OpenBinaryStream();
clientContext.ExecuteQuery();

```


## <a name="in-this-section"></a><span data-ttu-id="c542a-194">В этом разделе:</span><span class="sxs-lookup"><span data-stu-id="c542a-194">In this section</span></span>
<span data-ttu-id="c542a-195"><a name="Trouble"> </a></span><span class="sxs-lookup"><span data-stu-id="c542a-195"></span></span>

 [<span data-ttu-id="c542a-196">Использование сайта SharePoint Office 365 для авторизации размещенных у поставщика надстроек на локальном сайте SharePoint</span><span class="sxs-lookup"><span data-stu-id="c542a-196">Use an Office 365 SharePoint site to authorize provider-hosted add-ins on an on-premises SharePoint site</span></span>](use-an-office-365-sharepoint-site-to-authorize-provider-hosted-add-ins-on-an-on-premises-sharepoint-site)
 

 
 [<span data-ttu-id="c542a-197">Поток OAuth токена контекста для надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="c542a-197">Context Token OAuth flow for SharePoint Add-ins</span></span>](context-token-oauth-flow-for-sharepoint-add-ins)
 

 
 [<span data-ttu-id="c542a-198">Поток кода авторизации OAuth для надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="c542a-198">Authorization Code OAuth flow for SharePoint Add-ins</span></span>](authorization-code-oauth-flow-for-sharepoint-add-ins)
 

 
 [<span data-ttu-id="c542a-199">Замена секрета клиента с истекающим сроком действия в надстройке SharePoint</span><span class="sxs-lookup"><span data-stu-id="c542a-199">Replace an expiring client secret in a SharePoint Add-in</span></span>](replace-an-expiring-client-secret-in-a-sharepoint-add-in)
 

 

## <a name="additional-resources"></a><span data-ttu-id="c542a-200">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="c542a-200">Additional resources</span></span>
<span data-ttu-id="c542a-201"><a name="FileName_AdditionalResources"> </a></span><span class="sxs-lookup"><span data-stu-id="c542a-201"></span></span>


-  [<span data-ttu-id="c542a-202">Регистрация надстроек SharePoint 2013</span><span class="sxs-lookup"><span data-stu-id="c542a-202">Register SharePoint Add-ins 2013</span></span>](register-sharepoint-add-ins-2013)
    
 

