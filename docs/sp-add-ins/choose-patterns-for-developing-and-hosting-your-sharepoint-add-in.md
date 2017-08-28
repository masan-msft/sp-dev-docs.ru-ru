# <a name="choose-patterns-for-developing-and-hosting-your-sharepoint-add-in"></a><span data-ttu-id="f8163-101">Выбор шаблонов для разработки и размещения надстройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="f8163-101">Choose patterns for developing and hosting your SharePoint Add-in</span></span>
<span data-ttu-id="f8163-102">Информация о различных способах размещения компонентов надстроек SharePoint.</span><span class="sxs-lookup"><span data-stu-id="f8163-102">Learn about the different ways that you can host the components of SharePoint Add-ins.</span></span>
 

 <span data-ttu-id="f8163-p101">**Примечание.** Название "приложения для SharePoint" меняется на "надстройки SharePoint". Пока изменения не будут внесены полностью, в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio по-прежнему может встречаться термин "приложение". Дополнительные сведения см. в статье [Название "приложения для Office и SharePoint" изменилось на "надстройки Office и SharePoint"](new-name-for-apps-for-sharepoint#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="f8163-p101">The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span></span>
 

<span data-ttu-id="f8163-p102">В модели надстроек SharePoint представлен широкий выбор шаблонов размещения и разработки. Некоторые из них можно использовать в комбинации друг с другом. Например, надстройки могут одновременно содержать размещаемые в SharePoint и удаленно размещаемые компоненты. Чтобы решить, какие шаблоны лучше использовать, следует сначала определить собственные требования, технологии и цели, а затем сопоставить их с возможностями и вариантами, предлагаемыми надстройками SharePoint.</span><span class="sxs-lookup"><span data-stu-id="f8163-p102">Learn about the different ways that you can host the components of SharePoint Add-ins. The SharePoint add-in model introduces a wide range of hosting and development patterns. Some of these patterns can be used in combination with each other. For example, your add-ins can mix SharePoint-hosted and remotely hosted components. The most useful way to determine which patterns you'll want to use is to start with your own requirements, technologies, and goals and match them with the options and possibilities that are enabled by SharePoint Add-ins.</span></span>
 

## <a name="what-to-think-about-when-choosing-your-development-pattern"></a><span data-ttu-id="f8163-110">Что нужно учитывать при выборе шаблона разработки</span><span class="sxs-lookup"><span data-stu-id="f8163-110">What to think about when choosing your development pattern</span></span>
<span data-ttu-id="f8163-111"><a name="ChoosePattern"> </a></span><span class="sxs-lookup"><span data-stu-id="f8163-111"></span></span>

<span data-ttu-id="f8163-p103">Надстройки SharePoint расширяет диапазон языков программирования и стеков технологий, которые можно использовать при работе с ресурсами и службами SharePoint. Точный набор возможностей зависит от выбранного типа надстройки и шаблона размещения. Кроме того, можно совмещать различные шаблоны.</span><span class="sxs-lookup"><span data-stu-id="f8163-p103">SharePoint Add-ins widen the range of possible programming languages and technology stacks that you can use when you work with SharePoint resources and services. The precise range of options depends on both the type of add-in and the hosting pattern that you choose. It's also possible to mix patterns.</span></span>
 

 

### <a name="sharepoint-hosted-add-ins"></a><span data-ttu-id="f8163-115">Размещаемые в SharePoint надстройки</span><span class="sxs-lookup"><span data-stu-id="f8163-115">SharePoint-hosted add-ins</span></span>
<span data-ttu-id="f8163-116"><a name="SPHosted"> </a></span><span class="sxs-lookup"><span data-stu-id="f8163-116"></span></span>

<span data-ttu-id="f8163-p104">Начните с самого простого варианта: надстройки, размещаемые в SharePoint, или надстройки, все компоненты которых размещены локально или в ферме SharePoint Office 365. Надстройки, размещаемые в SharePoint, устанавливаются на веб-сайте SharePoint, который называется хост-сайтом. Их ресурсы размещаются на изолированном дочернем сайте хост-сайта, который называется сайтом надстройки. Важно понимать,  [чем различаются хост-сайты и сайты надстроек](host-webs-add-in-webs-and-sharepoint-components-in-sharepoint-2013). На рисунке 1 показана базовая архитектура надстройки, размещаемой в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="f8163-p104">Start with the simplest option: SharePoint-hosted add-ins, or add-ins where all components are hosted on either an on-premises or Office 365 SharePoint farm. SharePoint-hosted add-ins are installed on a SharePoint website, called the host web. They have their resources hosted on an isolated subsite of a host web, called the add-in web. It's important to know  [the difference between host webs and add-in webs](host-webs-add-in-webs-and-sharepoint-components-in-sharepoint-2013). Figure 1 illustrates the basic architecture of a SharePoint-hosted add-in.</span></span>
 

 

<span data-ttu-id="f8163-122">**Рис. 1. Архитектура надстройки, размещаемой в SharePoint**</span><span class="sxs-lookup"><span data-stu-id="f8163-122">**Figure 1. SharePoint-hosted add-in architecture**</span></span>

 

 
![Компоненты приложения, размещаемого в SharePoint, находятся на сайте приложения фермы SharePoint.](../../images/SP15_hosting_SPhosted.gif)
 
<span data-ttu-id="f8163-124">Надстройку, размещенную в SharePoint, можно использовать с надстройками, имеющими удаленно размещенные компоненты, но каждая надстройка или часть надстройки, работающей на сайте надстройки, имеет следующий набор требований к трем ключевым компонентам: где размещена надстройка, как в ней выполняется авторизация и какой язык может в ней использоваться.</span><span class="sxs-lookup"><span data-stu-id="f8163-124">You can combine a SharePoint-hosted add-in with add-ins that have remotely hosted components, but any add-in or portion of an add-in that runs on an add-in web has the following set of requirements for three key components: where the add-in is hosted, how the add-in gets authorization, and what language it can use.</span></span>
 

 


|<span data-ttu-id="f8163-125">**Компонент**</span><span class="sxs-lookup"><span data-stu-id="f8163-125">**Component**</span></span>|<span data-ttu-id="f8163-126">**Требование к надстройкам, размещаемым в SharePoint**</span><span class="sxs-lookup"><span data-stu-id="f8163-126">**SharePoint-hosted add-in requirement**</span></span>|
|:-----|:-----|
|<span data-ttu-id="f8163-127">Место размещения компонентов надстроек</span><span class="sxs-lookup"><span data-stu-id="f8163-127">Where the add-in components are hosted</span></span>|<span data-ttu-id="f8163-128">Изолированный домен надстроек вашей фермы SharePoint</span><span class="sxs-lookup"><span data-stu-id="f8163-128">In the isolated add-in domain of your SharePoint farm</span></span>|
|<span data-ttu-id="f8163-129">Авторизация надстройки</span><span class="sxs-lookup"><span data-stu-id="f8163-129">How the add-in gets authorized</span></span>|<span data-ttu-id="f8163-130">Права пользователя, выполнившего вход</span><span class="sxs-lookup"><span data-stu-id="f8163-130">The privileges of the signed-in user</span></span>|
|<span data-ttu-id="f8163-131">Язык, который можно использовать в надстройке</span><span class="sxs-lookup"><span data-stu-id="f8163-131">What language the add-in can use</span></span>|<span data-ttu-id="f8163-132">JavaScript (с библиотекой SharePoint JSOM) + HTML</span><span class="sxs-lookup"><span data-stu-id="f8163-132">JavaScript (with the SharePoint JSOM library) + HTML</span></span>|
<span data-ttu-id="f8163-p105">Такой шаблон проще всего развертывать, и вы можете использовать  [Создание простой надстройки для SharePoint с размещением в SharePoint с помощью средств разработки Napa для Office 365](create-a-basic-sharepoint-hosted-add-in-by-using-napa-office-365-development-tools). Прежде чем принять решение о создании надстройки, размещаемой в SharePoint, учтите следующее.</span><span class="sxs-lookup"><span data-stu-id="f8163-p105">This pattern is the easiest to deploy, and you can use the  [Create a basic SharePoint-hosted add-in by using Napa Office 365 Development Tools](create-a-basic-sharepoint-hosted-add-in-by-using-napa-office-365-development-tools). You'll want to consider the following before deciding to create a SharePoint-hosted add-in.</span></span>
 

 


|<span data-ttu-id="f8163-135">**Преимущества**</span><span class="sxs-lookup"><span data-stu-id="f8163-135">**Get these benefits**</span></span>|<span data-ttu-id="f8163-136">**Недостатки**</span><span class="sxs-lookup"><span data-stu-id="f8163-136">**But consider this**</span></span>|
|:-----|:-----|
|<span data-ttu-id="f8163-137">Можно повторно использовать общие элементы SharePoint, например списки и веб-части.</span><span class="sxs-lookup"><span data-stu-id="f8163-137">Reuse common SharePoint items, like lists and Web Parts.</span></span>|<span data-ttu-id="f8163-138">В надстройке можно использовать только JavaScript, при этом нельзя использовать код на стороне сервера.</span><span class="sxs-lookup"><span data-stu-id="f8163-138">You can use only JavaScript in the add-in—you can't use any server-side code.</span></span>|
|<span data-ttu-id="f8163-139">Такие надстройки относительно просты в создании и развертывании, поэтому они подходят для создания полезных приложений для небольших команд и автоматизации бизнес-процесса с несложными бизнес-правилами.</span><span class="sxs-lookup"><span data-stu-id="f8163-139">Relatively easy to create and deploy, so they are good for small team productivity add-ins and business process automation, with lower complexity business rules.</span></span>|<span data-ttu-id="f8163-140">Надстройка получает лишь права авторизации, которые есть у выполнившего вход пользователя.</span><span class="sxs-lookup"><span data-stu-id="f8163-140">Your add-in has only the authorization privileges of the signed-in user.</span></span>|
 [<span data-ttu-id="f8163-141">Приступая к созданию надстроек SharePoint с размещением в SharePoint</span><span class="sxs-lookup"><span data-stu-id="f8163-141">Get started creating SharePoint-hosted SharePoint Add-ins</span></span>](get-started-creating-sharepoint-hosted-sharepoint-add-ins)
 

 

### <a name="provider-hosted-add-ins"></a><span data-ttu-id="f8163-142">Надстройки, размещаемые у поставщика</span><span class="sxs-lookup"><span data-stu-id="f8163-142">Provider-hosted add-ins</span></span>
<span data-ttu-id="f8163-143"><a name="SelfHosted"> </a></span><span class="sxs-lookup"><span data-stu-id="f8163-143"></span></span>

<span data-ttu-id="f8163-p106">Надстройки SharePoint, размещаемые у поставщика, включают компоненты, разворачиваемые и размещаемые вне фермы SharePoint. Они устанавливаются на хост-сайте, но их удаленные компоненты размещены на другом сервере,  *который не должен входить в состав фермы SharePoint*  . На рисунке 2 показана базовая архитектура надстройки, размещаемой у поставщика.</span><span class="sxs-lookup"><span data-stu-id="f8163-p106">Provider-hosted SharePoint Add-ins include components that are deployed and hosted outside the SharePoint farm. They are installed to the host web, but their remote components are hosted on another server  *that should not be a server in the SharePoint farm*  . Figure 2 illustrates the basic architecture of a provider-hosted add-in.</span></span>
 

 

<span data-ttu-id="f8163-147">**Рис. 2. Архитектура надстройки, размещаемой у поставщика**</span><span class="sxs-lookup"><span data-stu-id="f8163-147">**Figure 2. Provider-hosted add-in architecture**</span></span>

 

 
![Компоненты приложения, размещаемого у поставщика, находятся на любом веб-сервере или в службе размещения.](../../images/SP15_hosting_Provider.gif)
 
<span data-ttu-id="f8163-149">В таблице ниже показано, что требования к месту размещения, авторизации и языкам для надстроек, размещаемых у поставщика, существенно менее жесткие, чем для надстроек, размещаемых в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="f8163-149">The following table shows how the requirements for hosting location, add-in authorization, and languages are much less fixed for provider-hosted add-ins than they are for SharePoint-hosted add-ins.</span></span>
 

 


|<span data-ttu-id="f8163-150">**Компонент**</span><span class="sxs-lookup"><span data-stu-id="f8163-150">**Component**</span></span>|<span data-ttu-id="f8163-151">**Требования к надстройкам, размещаемым у поставщика**</span><span class="sxs-lookup"><span data-stu-id="f8163-151">**Provider-hosted add-in requirement**</span></span>|
|:-----|:-----|
|<span data-ttu-id="f8163-152">Место размещения компонентов надстроек</span><span class="sxs-lookup"><span data-stu-id="f8163-152">Where the add-in components are hosted</span></span>|<span data-ttu-id="f8163-153">Любой веб-сервер или служба размещения</span><span class="sxs-lookup"><span data-stu-id="f8163-153">Any web server or hosting service</span></span>|
|<span data-ttu-id="f8163-154">Авторизация надстройки</span><span class="sxs-lookup"><span data-stu-id="f8163-154">How the add-in gets authorized</span></span>|<span data-ttu-id="f8163-155">OAuth или междоменная библиотека JavaScript</span><span class="sxs-lookup"><span data-stu-id="f8163-155">OAuth or the JavaScript cross-domain library</span></span>|
|<span data-ttu-id="f8163-156">Язык, который можно использовать в надстройке</span><span class="sxs-lookup"><span data-stu-id="f8163-156">What language the add-in can use</span></span>|<span data-ttu-id="f8163-157">Любой язык, поддерживаемый вашим веб-сервером или службой размещения</span><span class="sxs-lookup"><span data-stu-id="f8163-157">Any language supported by your web server or hosting service</span></span>|
<span data-ttu-id="f8163-p107">Размещаемая у поставщика надстройка взаимодействует с сайтом SharePoint, но использует ресурсы и службы, находящиеся на удаленном сайте. Прежде чем принять решение о создании надстройки, размещаемой у поставщика, учтите следующее.</span><span class="sxs-lookup"><span data-stu-id="f8163-p107">A provider-hosted add-in interacts with a SharePoint site but also uses resources and services that are located on the remote site. You'll want to consider the following before deciding to create a provider-hosted add-in.</span></span>
 

 


|<span data-ttu-id="f8163-160">**Преимущества**</span><span class="sxs-lookup"><span data-stu-id="f8163-160">**Get these benefits**</span></span>|<span data-ttu-id="f8163-161">**Недостатки**</span><span class="sxs-lookup"><span data-stu-id="f8163-161">**But consider this**</span></span>|
|:-----|:-----|
|<span data-ttu-id="f8163-162">Приложение можно размещать в Microsoft Azure или на любой другой удаленной веб-платформе, включая сторонние (не от Майкрософт).</span><span class="sxs-lookup"><span data-stu-id="f8163-162">Host the add-in on Microsoft Azure or any remote web platform, including non-Microsoft platforms.</span></span> |<span data-ttu-id="f8163-163">Вы отвечаете за создание логики установки, обновления и удаления удаленных компонентов.</span><span class="sxs-lookup"><span data-stu-id="f8163-163">You are responsible for creating the installation, upgrade, and uninstallation logic of the remote components.</span></span>|
|<span data-ttu-id="f8163-164">Для взаимодействия с SharePoint можно использовать одну из клиентских объектных моделей SharePoint, междоменную библиотеку JavaScript или [веб-службу SharePoint на основе REST/OData](http://msdn.microsoft.com/magazine/dn198245.aspx).</span><span class="sxs-lookup"><span data-stu-id="f8163-164">Use one of the SharePoint client object models, the JavaScript cross-domain library, or the SharePoint  [REST/OData-based web service](http://msdn.microsoft.com/magazine/dn198245.aspx) to interact with SharePoint.</span></span>|<span data-ttu-id="f8163-165">Каждый способ взаимодействия с SharePoint предусматривает [соответствующие варианты доступа к данным](secure-data-access-and-client-object-models-for-sharepoint-add-ins).</span><span class="sxs-lookup"><span data-stu-id="f8163-165">Each way of interacting with SharePoint has  [corresponding options for approaches to data access](secure-data-access-and-client-object-models-for-sharepoint-add-ins).</span></span>|
|<span data-ttu-id="f8163-166">Для доступа к данным SharePoint можно авторизоваться с помощью одной из [трех систем авторизации](three-authorization-systems-for-sharepoint-add-ins).</span><span class="sxs-lookup"><span data-stu-id="f8163-166">Gain authorization to SharePoint data using one of  [the three authorization systems](three-authorization-systems-for-sharepoint-add-ins).</span></span>|<span data-ttu-id="f8163-167">Нужно выбрать один из двух способов авторизации доступа надстройки к SharePoint: с помощью OAuth или междоменной библиотеки.</span><span class="sxs-lookup"><span data-stu-id="f8163-167">You need to decide between OAuth and the cross-domain library to authorize your add-in's access to SharePoint.</span></span>|

## <a name="match-your-hosting-pattern-with-your-development-goals"></a><span data-ttu-id="f8163-168">Выберите шаблон размещения, соответствующий целям разработки</span><span class="sxs-lookup"><span data-stu-id="f8163-168">Match your hosting pattern with your development goals</span></span>
<span data-ttu-id="f8163-169"><a name="MatchPattern"> </a></span><span class="sxs-lookup"><span data-stu-id="f8163-169"></span></span>

<span data-ttu-id="f8163-p108">Помимо технических преимуществ и ограничений каждого варианта, при выборе шаблона размещения также необходимо принимать во внимание цели разработки. Следующая таблица поможет определить, какой шаблон размещения лучше всего подходит для ваших требований.</span><span class="sxs-lookup"><span data-stu-id="f8163-p108">In addition to considering the technical advantages and constraints of each option, you'll also need to think about your development goals when deciding on a hosting pattern. You can use the following table to help sort out which hosting pattern best fits your needs.</span></span>
 

 


|<span data-ttu-id="f8163-172">**Ваши требования**</span><span class="sxs-lookup"><span data-stu-id="f8163-172">**Your requirements**</span></span>|<span data-ttu-id="f8163-173">**Рекомендуемый шаблон размещения**</span><span class="sxs-lookup"><span data-stu-id="f8163-173">**Recommended Hosting pattern**</span></span>|<span data-ttu-id="f8163-174">**Пример**</span><span class="sxs-lookup"><span data-stu-id="f8163-174">**Example**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="f8163-175">Работа с новыми объектами SharePoint и их подготовка в монопольном режиме</span><span class="sxs-lookup"><span data-stu-id="f8163-175">Work with and provision new SharePoint entities exclusively</span></span>|<span data-ttu-id="f8163-176">Размещение в SharePoint</span><span class="sxs-lookup"><span data-stu-id="f8163-176">SharePoint-hosted add-in</span></span>|<span data-ttu-id="f8163-177">Надстройка, включающая в себя элемент управления "Выбор людей", который сохраняет информацию о пользователях SharePoint в списке SharePoint</span><span class="sxs-lookup"><span data-stu-id="f8163-177">An add-in that includes a people picker control and that stores information about SharePoint users in a SharePoint list</span></span>|
|<span data-ttu-id="f8163-178">Использование существующих объектов SharePoint и взаимодействие с внешними веб-службами (размещенными вне SharePoint)</span><span class="sxs-lookup"><span data-stu-id="f8163-178">Use existing SharePoint entities and interact with external (non-SharePoint) web services</span></span>|<span data-ttu-id="f8163-179">Размещение на ресурсах поставщика</span><span class="sxs-lookup"><span data-stu-id="f8163-179">Provider-hosted</span></span>|<span data-ttu-id="f8163-180">Надстройка, которая получает адреса клиентов из существующего списка SharePoint на хост-сайте и отображает их с помощью службы сопоставления в веб-приложении</span><span class="sxs-lookup"><span data-stu-id="f8163-180">An add-in that gets customer addresses from an existing SharePoint list in the host web and uses a mapping service in a web application to display their locations</span></span>|
|<span data-ttu-id="f8163-181">Подготовка к работе новых объектов SharePoint и взаимодействие с внешними веб-службами</span><span class="sxs-lookup"><span data-stu-id="f8163-181">Provision new SharePoint entities and interact with external web services</span></span>|<span data-ttu-id="f8163-182">Комбинированное размещение в SharePoint и у поставщика</span><span class="sxs-lookup"><span data-stu-id="f8163-182">Combined SharePoint-hosted and provider-hosted</span></span>|<span data-ttu-id="f8163-183">Надстройка сопоставления, которая подготавливает к работе список SharePoint на сайте надстройки для хранения координат широты и долготы адресов, предоставленных пользователем или полученных из существующего списка SharePoint</span><span class="sxs-lookup"><span data-stu-id="f8163-183">A mapping add-in that provisions a SharePoint list on the appweb so that it can store latitude and longitude coordinates for addresses that are supplied by the user or pulled from an existing SharePoint list</span></span>|

## <a name="what-to-think-about-when-choosing-your-hosting-pattern-for-provider-hosted-add-ins"></a><span data-ttu-id="f8163-184">Что нужно учитывать при выборе шаблона размещения для надстроек, размещаемых у поставщика</span><span class="sxs-lookup"><span data-stu-id="f8163-184">What to think about when choosing your hosting pattern for provider-hosted add-ins</span></span>
<span data-ttu-id="f8163-185"><a name="ThinkAbout"> </a></span><span class="sxs-lookup"><span data-stu-id="f8163-185"></span></span>

<span data-ttu-id="f8163-p109">Надстройки, размещаемые в SharePoint, имеют фиксированный шаблон размещения в связи с размещением на сайте надстройки. Надстройки, размещаемые у поставщика, обеспечивают повышенную гибкость для размещения различных компонентов надстройки. Поэтому, если вы решите создать такую надстройку, вам понадобится сопоставить свои цели и требования с соответствующим шаблоном размещения.</span><span class="sxs-lookup"><span data-stu-id="f8163-p109">SharePoint-hosted add-ins have a fixed hosting pattern, since they are hosted on the add-in web. Provider-hosted add-ins provide more flexibility for hosting the various components of your add-in, so if you choose to create one, you'll need to match your goals and requirements to the appropriate hosting pattern.</span></span> 
 

 

### <a name="oauth-or-the-cross-domain-library"></a><span data-ttu-id="f8163-188">OAuth или междоменная библиотека</span><span class="sxs-lookup"><span data-stu-id="f8163-188">OAuth or the cross-domain library</span></span>

<span data-ttu-id="f8163-p110">Один из самых важных вопросов, который необходимо задать при рассмотрении и сборке размещаемых у поставщика надстроек, каким образом надстройка будет проходить авторизацию на взаимодействие с SharePoint. Для надстроек, размещаемых у поставщика, доступно два варианта: междоменная библиотека JavaScript и OAuth.</span><span class="sxs-lookup"><span data-stu-id="f8163-p110">One of the most important questions you need to ask when considering provider-hosted add-ins and how you'll build them is how the add-in will get authorization to interact with SharePoint. Provider-hosted add-ins give you two choices: the JavaScript cross-domain library and OAuth.</span></span> 
 

 
<span data-ttu-id="f8163-p111">[Междоменная библиотека](access-sharepoint-2013-data-from-add-ins-using-the-cross-domain-library) позволяет взаимодействовать с несколькими доменами из удаленных компонентов надстройки через прокси-сервер. Если достаточно кода на стороне клиента и разрешений пользователя, вошедшего в SharePoint, междоменная библиотека это хороший выбор. Междоменная библиотека также удобна, когда необходимо совершать удаленные вызовы через брандмауэр.</span><span class="sxs-lookup"><span data-stu-id="f8163-p111">The  [cross-domain library](access-sharepoint-2013-data-from-add-ins-using-the-cross-domain-library) lets you interact with more than one domain from the remote components of your add-in through a proxy. If client-side code and the permissions of a user who is signed in to SharePoint are sufficient, the cross-domain library is a good option. The cross-domain library is also convenient whenever you are making remote calls through a firewall.</span></span>
 

 
<span data-ttu-id="f8163-p112">OAuth это открытый протокол для авторизации, обеспечивающий надежную авторизацию из клиентских приложений (классических, мобильных и веб-приложений) легким в управлении способом. Если планируется собрать надстройку SharePoint, работающую в удаленном веб-приложении и взаимодействующую с SharePoint, то придется часто использовать OAuth: при каждом вызове SharePoint из удаленно размещенного веб-приложения, которое не может эксклюзивно использовать код на клиентской стороне (HTML + JavaScript).  [Подробнее о том, как OAuth работает в надстройках SharePoint.](creating-sharepoint-add-ins-that-use-low-trust-authorization)</span><span class="sxs-lookup"><span data-stu-id="f8163-p112">OAuth is an open protocol for authorization that enables secure authorization from client applications (desktop, web, and mobile applications) in an easily manageable way. If you plan to build a SharePoint Add-in that runs in a remote web application and communicates back to SharePoint, you will often need to use OAuth. OAuth is required whenever you are calling into SharePoint from a remotely hosted web application that can't use client-side code (HTML + JavaScript) exclusively.  [Learn more about how OAuth works in SharePoint Add-ins.](creating-sharepoint-add-ins-that-use-low-trust-authorization)</span></span>
 

 
 <span data-ttu-id="f8163-198">В статьях  [Безопасный доступ к данным и клиентские объектные модели для надстроек SharePoint](secure-data-access-and-client-object-models-for-sharepoint-add-ins) и [Три системы авторизации для надстроек для SharePoint](three-authorization-systems-for-sharepoint-add-ins) подробнее объясняется выбор между OAuth и междоменной библиотекой.</span><span class="sxs-lookup"><span data-stu-id="f8163-198">[Secure data access and client object models for SharePoint Add-ins](secure-data-access-and-client-object-models-for-sharepoint-add-ins) and [Three authorization systems for SharePoint Add-ins](three-authorization-systems-for-sharepoint-add-ins) explain the choice between OAuth and the cross-domain library more thoroughly.</span></span>
 

 

### <a name="oauth-with-on-premises-sharepoint-farms"></a><span data-ttu-id="f8163-199">OAuth с локальными фермами SharePoint</span><span class="sxs-lookup"><span data-stu-id="f8163-199">OAuth with on-premises SharePoint farms</span></span>

<span data-ttu-id="f8163-p113">При локальном развертывании SharePoint можно использовать OAuth, но необходимо выбрать между созданием надстроек с высоким уровнем доверия и клиентом Office 365. Office 365 использует службу контроля доступа Microsoft Azure в качестве посредника доверия. Если у вас нет доступа к клиенту Office 365, вам понадобится  [Создание надстроек с высоким уровнем доверия для SharePoint](create-high-trust-sharepoint-add-ins), которая использует сертификаты для установления доверия между вашей надстройкой и SharePoint. Вы можете добавить надстройки с высоким уровнем доверия в каталог надстроек своей фермы SharePoint, но вы не можете продавать их в Магазин Office. Если у вас есть доступ к клиенту Office 365, вы можете связать его со своей локальной средой SharePoint и  [использовать службу контроля доступа в качестве посредника доверия для надстроек, установленных в локальной среде SharePoint](use-an-office-365-sharepoint-site-to-authorize-provider-hosted-add-ins-on-an-on-premises-sharepoint-site).</span><span class="sxs-lookup"><span data-stu-id="f8163-p113">If you are using an on-premises deployment of SharePoint, you can use OAuth, but you will have to choose between creating high-trust add-ins and using an Office 365 tenancy. Office 365 uses Microsoft Azure Access Control Service (ACS) as the trust broker, and if you do not have access to an Office 365 tenancy, you'll need to use  [Create high-trust SharePoint Add-ins](create-high-trust-sharepoint-add-ins), which uses certificates to establish trust between your add-in and SharePoint. You can add high trust add-ins to the add-in catalog of your SharePoint farm, but you can't sell them in the Office Store. If you do have access to an Office 365 tenancy, you can link it to your on-premises installation of SharePoint and  [use ACS as the trust broker for add-ins that are installed to your on-premises SharePoint](use-an-office-365-sharepoint-site-to-authorize-provider-hosted-add-ins-on-an-on-premises-sharepoint-site).</span></span>
 

 
<span data-ttu-id="f8163-p114">В таблице ниже представлены все возможные шаблоны размещения как компонентов SharePoint, так и удаленных компонентов надстройки вместе с посредниками доверия, которые доступны в случае использования OAuth. Обратите внимание, что вам понадобится доступ к клиенту Office 365, чтобы использовать службу контроля доступа для установления доверия между SharePoint и Надстройка SharePoint, установленного в локальном экземпляре SharePoint.</span><span class="sxs-lookup"><span data-stu-id="f8163-p114">The following table lists all of the possible patterns for hosting both the SharePoint components and the remote components of your add-in, along with the trust brokers that are available to you if you're using OAuth. Note that you'll need access to an Office 365 tenant in order to use ACS to establish trust between SharePoint and a SharePoint Add-in that is installed to an on-premises installation of SharePoint.</span></span>
 

 


|<span data-ttu-id="f8163-206">**Расположение компонентов в SharePoint**</span><span class="sxs-lookup"><span data-stu-id="f8163-206">**SharePoint component location**</span></span>|<span data-ttu-id="f8163-207">**Удаленное расположение компонентов**</span><span class="sxs-lookup"><span data-stu-id="f8163-207">**Remote component location**</span></span>|<span data-ttu-id="f8163-208">**Брокер доверия**</span><span class="sxs-lookup"><span data-stu-id="f8163-208">**Trust broker**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="f8163-209">Локальная среда</span><span class="sxs-lookup"><span data-stu-id="f8163-209">On premises</span></span>|<span data-ttu-id="f8163-210">В облаке</span><span class="sxs-lookup"><span data-stu-id="f8163-210">In cloud</span></span>|<span data-ttu-id="f8163-211">Служба контроля доступа, сертификат</span><span class="sxs-lookup"><span data-stu-id="f8163-211">ACS, certificate</span></span>|
|<span data-ttu-id="f8163-212">Локальная среда</span><span class="sxs-lookup"><span data-stu-id="f8163-212">On premises</span></span>|<span data-ttu-id="f8163-213">Локальная среда</span><span class="sxs-lookup"><span data-stu-id="f8163-213">On premises</span></span>|<span data-ttu-id="f8163-214">Служба контроля доступа, сертификат</span><span class="sxs-lookup"><span data-stu-id="f8163-214">ACS, certificate</span></span>|
|<span data-ttu-id="f8163-215">Сайт SharePoint Office 365</span><span class="sxs-lookup"><span data-stu-id="f8163-215">Office 365 SharePoint site</span></span>|<span data-ttu-id="f8163-216">В облаке</span><span class="sxs-lookup"><span data-stu-id="f8163-216">In cloud</span></span>|<span data-ttu-id="f8163-217">ACS</span><span class="sxs-lookup"><span data-stu-id="f8163-217">ACS</span></span>|
|<span data-ttu-id="f8163-218">Сайт SharePoint Office 365</span><span class="sxs-lookup"><span data-stu-id="f8163-218">Office 365 SharePoint site</span></span>|<span data-ttu-id="f8163-219">Локальная среда</span><span class="sxs-lookup"><span data-stu-id="f8163-219">On premises</span></span>|<span data-ttu-id="f8163-220">ACS</span><span class="sxs-lookup"><span data-stu-id="f8163-220">ACS</span></span>|

## <a name="combine-provider-hosting-and-sharepoint-hosting"></a><span data-ttu-id="f8163-221">Сочетание размещения у поставщика и в SharePoint</span><span class="sxs-lookup"><span data-stu-id="f8163-221">Combine provider hosting and SharePoint hosting</span></span>
<span data-ttu-id="f8163-222"><a name="Combined"> </a></span><span class="sxs-lookup"><span data-stu-id="f8163-222"></span></span>

<span data-ttu-id="f8163-p115">Компоненты создаваемых надстроек могут размещаться как в облаке, так и в SharePoint. Например, можно создать  [размещенную в облаке надстройку, которая содержит настраиваемый список SharePoint и тип содержимого](create-a-provider-hosted-add-in-that-includes-a-custom-sharepoint-list-and-content-type). В этой архитектуре необходимо учитывать ограничения по безопасности, встроенные в модель. JavaScript можно использовать только в компонентах кода, размещенных в SharePoint, а для взаимодействия удаленно размещенных компонентов с веб-сайтом SharePoint необходимо использовать OAuth или междоменную библиотеку. Используйте этот подход, только если вы понимаете,  [как выполняется авторизация надстроек в SharePoint](authorization-and-authentication-of-sharepoint-add-ins). На рисунке 4 показано, как работает архитектура, когда для размещения удаленных компонентов надстройки используется Microsoft Azure и применяется OAuth.</span><span class="sxs-lookup"><span data-stu-id="f8163-p115">You can also build add-ins that include both SharePoint-hosted and cloud-hosted components. For example, you can create a  [cloud-hosted add-in that includes a custom SharePoint list and content type](create-a-provider-hosted-add-in-that-includes-a-custom-sharepoint-list-and-content-type). If you choose to use this architecture, your design and approach must account for security limitations that are built into the model. You can use only JavaScript in the code components that are hosted by SharePoint, and the remotely hosted components must use either OAuth or the cross-domain library to interact with the SharePoint website. When considering this approach, make sure that you understand how  [add-in authorization works in SharePoint](authorization-and-authentication-of-sharepoint-add-ins). Figure 4 shows you how this architecture works if you use Microsoft Azure to host the remote components of your add-in, and you use OAuth.</span></span>
 

 

<span data-ttu-id="f8163-229">**Рис. 4. Взаимодействие сервер-сервер для надстроек SharePoint при использовании OAuth и Windows Azure**</span><span class="sxs-lookup"><span data-stu-id="f8163-229">**Figure 4. SharePoint add-in server-to-server communication when you use OAuth and Windows Azure**</span></span>

 

 
![Ограничения взаимодействия сервер-сервер](../../images/SP15HelloWorldSPApp_Fig01.png)
 
 [<span data-ttu-id="f8163-231">Узнайте, как создать надстройку, сочетающую размещение в облаке и в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="f8163-231">Learn how to create an add-in that combines cloud hosting and SharePoint hosting.</span></span>](create-a-provider-hosted-add-in-that-includes-a-custom-sharepoint-list-and-content-type)
 

 
<span data-ttu-id="f8163-232">Вот что нужно учесть, если вы рассматриваете возможность сочетания размещения у поставщика и в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="f8163-232">Here are some things to think about when you're considering a combination of provider hosting and SharePoint hosting.</span></span>
 

 


|<span data-ttu-id="f8163-233">**Преимущества**</span><span class="sxs-lookup"><span data-stu-id="f8163-233">**Get these benefits**</span></span>|<span data-ttu-id="f8163-234">**Недостатки**</span><span class="sxs-lookup"><span data-stu-id="f8163-234">**But consider this**</span></span>|
|:-----|:-----|
|<span data-ttu-id="f8163-235">Все преимущества двух подходов.</span><span class="sxs-lookup"><span data-stu-id="f8163-235">All the benefits of the two approaches.</span></span>|<span data-ttu-id="f8163-236">Более сложная архитектура потребует тщательного планирования взаимодействия сервер-сервер и наложит ограничения на межсайтовые сценарии.</span><span class="sxs-lookup"><span data-stu-id="f8163-236">More complex architecture requires careful planning around server-to-server communication and cross-site scripting restrictions.</span></span>|

## <a name="provider-hosted-add-ins-in-azure-web-roles"></a><span data-ttu-id="f8163-237">Размещаемые у поставщика надстройки в веб-ролях Azure</span><span class="sxs-lookup"><span data-stu-id="f8163-237">Provider-hosted add-ins in Azure Web Roles</span></span>
<span data-ttu-id="f8163-238"><a name="AzureWebRole"> </a></span><span class="sxs-lookup"><span data-stu-id="f8163-238"></span></span>

<span data-ttu-id="f8163-p116">Размещенная у поставщика Надстройка SharePoint может быть размещена не в веб-приложении (локальном или Веб-сайт Azure), а в веб-роли Microsoft Azure. По существу, веб-роль Azure это веб-сайт, основанный на службах IIS и размещенный в Azure. Можно воспользоваться службами размещения и масштабируемостью веб-ролей Azure. Кроме того, можно повысить производительность и удобство использования Надстройка SharePoint, особенно, если надстройка активно используется или спрос на нее со временем возрастает. Если для Надстройка SharePoint понадобится больше серверных ресурсов, Azure может динамично распределить их с учетом потребностей надстройки.</span><span class="sxs-lookup"><span data-stu-id="f8163-p116">You can host a provider-hosted SharePoint Add-in on a Microsoft Azure web role instead of a web application (whether the web application is on-premises or a Azure Web Site). An Azure web role is, essentially, a website that's based on Internet Information Services (IIS) and hosted on Azure. You can take advantage of the hosting services and scalability of Azure web roles. You can also enhance the performance and usability of your SharePoint Add-in, especially if the add-in is heavily used or demand for it changes over time. If the SharePoint Add-in ever requires more server resources, Azure can dynamically allocate them to the add-in.</span></span>
 

 
<span data-ttu-id="f8163-244">Дополнительные сведения о веб-ролях Azure см. по следующим ссылкам.</span><span class="sxs-lookup"><span data-stu-id="f8163-244">See the following links for more information about Azure web roles.</span></span>
 

 

-  [<span data-ttu-id="f8163-245">Что такое облачная служба?</span><span class="sxs-lookup"><span data-stu-id="f8163-245">What is a cloud service?</span></span>](http://www.windowsazure.com/en-us/manage/services/cloud-services/what-is-a-cloud-service/)
    
 
-  [<span data-ttu-id="f8163-246">Представляем Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="f8163-246">Introducing Microsoft Azure</span></span>](http://www.windowsazure.com/en-us/develop/net/fundamentals/intro-to-windows-azure/)
    
 
-  [<span data-ttu-id="f8163-247">Автоматическое масштабирование и Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="f8163-247">Autoscaling and Microsoft Azure</span></span>](http://msdn.microsoft.com/en-us/library/hh680945%28v=pandp.50%29.aspx)
    
 
<span data-ttu-id="f8163-248">В качестве необходимого компонента вам понадобится пакет Microsoft Azure SDK для .NET (VS 2012) 1.8.1, который можно установить с помощью  [установщика веб-платформы](http://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="f8163-248">As a prerequisite, you will need the Microsoft Azure SDK for .NET (VS 2012) 1.8.1, which you can install by using the  [Web Platform Installer](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
 

 
<span data-ttu-id="f8163-249">Способ создания проекта в vsnv зависит от того, начинаете ли вы с проекта надстройки SharePoint и затем добавляете проект веб-роли Azure, или начинаете с проекта Azure и затем добавляете проект SharePoint.</span><span class="sxs-lookup"><span data-stu-id="f8163-249">The way that you use create the project in vsnv depends on whether you start with a SharePoint Add-in project and then add the Azure web role project, or you start with the Azure project and then add the SharePoint project.</span></span>
 

 

### <a name="add-a-cloud-service-to-an-existing-add-in"></a><span data-ttu-id="f8163-250">Добавление облачной службы в существующую надстройку</span><span class="sxs-lookup"><span data-stu-id="f8163-250">Add a cloud service to an existing add-in</span></span>

<span data-ttu-id="f8163-p117">Если у вас уже есть надстройка SharePoint с размещением у поставщика, которую вы хотите разместить в Azure, выберите проект веб-приложения в решении для надстройки SharePoint. В строке меню выберите **Проект**, **Добавить проект облачной службы Microsoft Azure**. Проект Azure с именем _NameOfTheWebAppProject_.Azure будет добавлен в решение для вашей надстройки SharePoint. Веб-роль для этого веб-проекта также добавляется в проект для облачной службы Azure. Инструменты разработчика Office для Visual Studio 2012 устанавливают необходимые свойства проекта, чтобы веб-роль могла работать с надстройкой SharePoint.</span><span class="sxs-lookup"><span data-stu-id="f8163-p117">If you already have a provider-hosted SharePoint Add-in that you want to host on Azure, choose the web application project in the solution for the SharePoint Add-in. On the menu bar, choose **Project**, **Add Microsoft Azure Cloud Service Project**. A Azure project, called  _NameOfTheWebAppProject_.Azure, is added to the solution for your SharePoint Add-in. A web role for the web project is also added to the project for the Azure cloud service. The Office Developer Tools for Visual Studio 2012 sets the necessary project properties so that the web role can work with the SharePoint Add-in.</span></span>
 

 

### <a name="add-an-add-in-to-an-existing-web-role"></a><span data-ttu-id="f8163-256">Добавление надстройки к существующей веб-роли</span><span class="sxs-lookup"><span data-stu-id="f8163-256">Add an add-in to an existing web role</span></span>

<span data-ttu-id="f8163-p118">Если у вас уже есть веб-роль в облачной службе Azure, которую вы хотите использовать в качестве узла для надстройки SharePoint с размещением у поставщика, откройте облачный проект Azure в Visual Studio, а затем в **обозревателе решений** выберите проект веб-роли. В строке меню выберите **Проект**, **Добавить надстройку для проекта SharePoint**. Будет создан и добавлен в решение проект для надстройки SharePoint с размещением у поставщика с именем _NameOfTheWebAppProject_.Azure. Visual Studio ссылается на веб-роль Azure как на узел веб-проекта для надстройки SharePoint.</span><span class="sxs-lookup"><span data-stu-id="f8163-p118">If you already have a web role in an Azure cloud service that you want to use as a host for a provider-hosted SharePoint Add-in, open the Azure cloud project in Visual Studio, and then, in **Solution Explorer**, choose the web role project. On the menu bar, choose **Project**, **Add Add-in for SharePoint Project**. A project for a provider-hosted SharePoint Add-in is created, called  _NameOfTheWebAppProject_.Azure, and added to the solution. Visual Studio references the Azure web role as the web project host for the SharePoint Add-in.</span></span>
 

 

## <a name="additional-resources"></a><span data-ttu-id="f8163-261">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="f8163-261">Additional resources</span></span>
<span data-ttu-id="f8163-262"><a name="SPAppModelArch_AdditionalResources"> </a></span><span class="sxs-lookup"><span data-stu-id="f8163-262"></span></span>

<span data-ttu-id="f8163-263">Дополнительные сведения см. в следующих источниках:</span><span class="sxs-lookup"><span data-stu-id="f8163-263">For more information, see the following resources:</span></span>
 

 

-  [<span data-ttu-id="f8163-264">Важные аспекты разработки и архитектуры для надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="f8163-264">Important aspects of the SharePoint Add-in architecture and development landscape</span></span>](important-aspects-of-the-sharepoint-add-in-architecture-and-development-landscape)
    
 
-  [<span data-ttu-id="f8163-265">Надстройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="f8163-265">SharePoint Add-ins</span></span>](sharepoint-add-ins)
    
 
-  [<span data-ttu-id="f8163-266">Хост-сайты, сайты надстроек и компоненты SharePoint в SharePoint</span><span class="sxs-lookup"><span data-stu-id="f8163-266">Host webs, add-in webs, and SharePoint components in SharePoint</span></span>](host-webs-add-in-webs-and-sharepoint-components-in-sharepoint-2013)
    
 
-  [<span data-ttu-id="f8163-267">Авторизация и проверка подлинности надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="f8163-267">Authorization and authentication of SharePoint Add-ins</span></span>](authorization-and-authentication-of-sharepoint-add-ins)
    
 
-  [<span data-ttu-id="f8163-268">Поток OAuth токена контекста для надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="f8163-268">Context Token OAuth flow for SharePoint Add-ins</span></span>](context-token-oauth-flow-for-sharepoint-add-ins)
    
 
-  [<span data-ttu-id="f8163-269">Использование сайта SharePoint Office 365 для авторизации размещенных у поставщика надстроек на локальном сайте SharePoint</span><span class="sxs-lookup"><span data-stu-id="f8163-269">Use an Office 365 SharePoint site to authorize provider-hosted add-ins on an on-premises SharePoint site</span></span>](use-an-office-365-sharepoint-site-to-authorize-provider-hosted-add-ins-on-an-on-premises-sharepoint-site)
    
 
-  [<span data-ttu-id="f8163-270">Надстройки SharePoint в сравнении с решениями для SharePoint</span><span class="sxs-lookup"><span data-stu-id="f8163-270">SharePoint Add-ins compared with SharePoint solutions</span></span>](http://msdn.microsoft.com/library/0e9efadb-aaf2-4c0d-afd5-d6cf25c4e7a8%28Office.15%29.aspx)
    
 
-  [<span data-ttu-id="f8163-271">Приступая к созданию надстроек SharePoint с размещением у поставщика</span><span class="sxs-lookup"><span data-stu-id="f8163-271">Get started creating provider-hosted SharePoint Add-ins</span></span>](get-started-creating-provider-hosted-sharepoint-add-ins)
    
 
-  [<span data-ttu-id="f8163-272">Приступая к созданию надстроек SharePoint с размещением в SharePoint</span><span class="sxs-lookup"><span data-stu-id="f8163-272">Get started creating SharePoint-hosted SharePoint Add-ins</span></span>](get-started-creating-sharepoint-hosted-sharepoint-add-ins)
    
 
-  [<span data-ttu-id="f8163-273">Создание надстройки с размещением у поставщика, включающей настраиваемый список SharePoint и пользовательский тип контента</span><span class="sxs-lookup"><span data-stu-id="f8163-273">Create a provider-hosted add-in that includes a custom SharePoint list and content type</span></span>](create-a-provider-hosted-add-in-that-includes-a-custom-sharepoint-list-and-content-type)
    
 

