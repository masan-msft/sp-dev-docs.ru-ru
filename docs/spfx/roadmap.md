# <a name="sharepoint-framework-roadmap"></a><span data-ttu-id="38ee8-101">План развития SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="38ee8-101">SharePoint Framework roadmap</span></span>

<span data-ttu-id="38ee8-p101">Первый выпуск SharePoint Framework будет поддерживать клиентские веб-части. В дальнейшем современные возможности настройки SharePoint будут расширяться. В этой статье перечислены перспективные направления развития SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="38ee8-p101">First release of the SharePoint Framework will contain support for client-side web parts. This is however just a start on the journey for providing additional modern customization capabilities to SharePoint. This article lists the different areas which are in our backlog for the future releases of SharePoint Framework.</span></span>

> <span data-ttu-id="38ee8-p102">Примечание. Это список областей, над которыми работают инженеры SharePoint. Элементы и разделы из этого списка будут постепенно находить воплощение в будущих выпусках SharePoint Framework (**необязательно** все идеи будут реализованы).</span><span class="sxs-lookup"><span data-stu-id="38ee8-p102">Notice. This is a list of areas which SharePoint engineering is having in the backlog and are looking into. This does **NOT** mean that all of them will be necessarily delivered, but we are looking for getting items and topics from this list gradually released with the future releases of SharePoint Framework.</span></span>  

## <a name="on-premises-support"></a><span data-ttu-id="38ee8-108">Поддержка локальных сред</span><span class="sxs-lookup"><span data-stu-id="38ee8-108">On-premises support</span></span>

- <span data-ttu-id="38ee8-109">Предоставление в составе пакета дополнительных компонентов 2 для SharePoint 2016.</span><span class="sxs-lookup"><span data-stu-id="38ee8-109">Shipping as part of Feature Pack 2 for SharePoint 2016</span></span>
- <span data-ttu-id="38ee8-110">Те же возможности, что и в SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="38ee8-110">Similar feature capabilities as in SharePoint Online</span></span>
- <span data-ttu-id="38ee8-111">Предоставление общей платформы разработки в локальной среде и облаке.</span><span class="sxs-lookup"><span data-stu-id="38ee8-111">Target is to provide common development platform across on-premises and the cloud</span></span>
- <span data-ttu-id="38ee8-112">Использование современной цепочки инструментов и открытого кода в локальных средах.</span><span class="sxs-lookup"><span data-stu-id="38ee8-112">Leveraging modern toolchain and open source on on-premises environments</span></span>
- <span data-ttu-id="38ee8-113">Ориентация на версию SharePoint 2016 в 2017 г.</span><span class="sxs-lookup"><span data-stu-id="38ee8-113">Targeting SharePoint 2016 version during calendar year 2017</span></span>

## <a name="general-improvements"></a><span data-ttu-id="38ee8-114">Общие улучшения</span><span class="sxs-lookup"><span data-stu-id="38ee8-114">General improvements</span></span>

- <span data-ttu-id="38ee8-115">Удобство вызова API Graph для доступа к данным пользователей (GraphHttpClient в предварительной версии для разработчиков).</span><span class="sxs-lookup"><span data-stu-id="38ee8-115">Easy access to Graph API to access user specific information (GraphHttpClient in dev preview)</span></span>
- <span data-ttu-id="38ee8-116">Каталог приложений семейства веб-сайтов с управлением на уровне клиента для обеспечения более простого развертывания решений.</span><span class="sxs-lookup"><span data-stu-id="38ee8-116">Site collection app catalog with tenant level control for enabling easier solution deployed</span></span> 
- <span data-ttu-id="38ee8-117">Веб-перехватчики уровня сайта</span><span class="sxs-lookup"><span data-stu-id="38ee8-117">Site level WebHooks</span></span>

## <a name="client-side-web-parts-and-add-ins"></a><span data-ttu-id="38ee8-118">Клиентские веб-части++ и надстройки</span><span class="sxs-lookup"><span data-stu-id="38ee8-118">Client-side web parts++ and add-ins</span></span>

- <span data-ttu-id="38ee8-119">Поддержка более сложных сценариев и взаимодействий с веб-частями</span><span class="sxs-lookup"><span data-stu-id="38ee8-119">Supporting more complex scenarios and interactions with web parts</span></span>
    - <span data-ttu-id="38ee8-120">Обмен данными между веб-частями</span><span class="sxs-lookup"><span data-stu-id="38ee8-120">Part-to-part communication</span></span>
    - <span data-ttu-id="38ee8-121">Изоляция платформы JS</span><span class="sxs-lookup"><span data-stu-id="38ee8-121">JS Framework isolation</span></span>
    - <span data-ttu-id="38ee8-122">Модель "разработчик-любитель" для простых задач разработки</span><span class="sxs-lookup"><span data-stu-id="38ee8-122">"citizen developer" model for lightweight development</span></span>

- <span data-ttu-id="38ee8-123">Реализация современных технологий оформления веб-частей.</span><span class="sxs-lookup"><span data-stu-id="38ee8-123">Bring add-ins to the modern world: Let’s make them play nicer with the new UX.</span></span> 
    - <span data-ttu-id="38ee8-124">Регистрация в Azure AD</span><span class="sxs-lookup"><span data-stu-id="38ee8-124">Azure AD Registration</span></span>
    - <span data-ttu-id="38ee8-125">Встроенная поддержка адаптивного дизайна</span><span class="sxs-lookup"><span data-stu-id="38ee8-125">Native responsive support</span></span> 
    - <span data-ttu-id="38ee8-126">Создание надстроек с помощью SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="38ee8-126">Build Add-Ins with SharePoint Framework</span></span>

## <a name="javascript-embedding-support-jslink-user-custom-actions"></a><span data-ttu-id="38ee8-127">Поддержка внедрения JavaScript (JSLink, дополнительные действия пользователей)</span><span class="sxs-lookup"><span data-stu-id="38ee8-127">JavaScript embedding support (JSLink, User Custom Actions)</span></span>

- <span data-ttu-id="38ee8-128">Те же цепочка инструментов и модель развертывания, что и для клиентских веб-частей.</span><span class="sxs-lookup"><span data-stu-id="38ee8-128">The same tool chain and deployment model as client-side web parts</span></span>
- <span data-ttu-id="38ee8-129">Наследование от строго типизированного базового класса везде, где это возможно, вместо прямого управления моделью DOM страницы.</span><span class="sxs-lookup"><span data-stu-id="38ee8-129">Derive from a strongly typed base class wherever possible rather than manipulating the page DOM directly.</span></span>
- <span data-ttu-id="38ee8-130">Обеспечение использования современных расширений и возможностей, подобных дополнительным действиям и JSLink, в случае классического варианта.</span><span class="sxs-lookup"><span data-stu-id="38ee8-130">Enable modern extension usage with modern experiences similar as Custom Actions and JS Link in classic experience</span></span>
- <span data-ttu-id="38ee8-131">Работа с NoScript через каталог приложений клиента.</span><span class="sxs-lookup"><span data-stu-id="38ee8-131">Work with NoScript via tenant app catalog</span></span>

> <span data-ttu-id="38ee8-132">Эта возможность теперь доступна в [предварительной версии для разработчиков](https://dev.office.com/blogs/announcing-availability-of-sharepoint-framework-extensions-developer-preview).</span><span class="sxs-lookup"><span data-stu-id="38ee8-132">This is now available in [developer preview](https://dev.office.com/blogs/announcing-availability-of-sharepoint-framework-extensions-developer-preview).</span></span>

## <a name="application-lifecycle-management"></a><span data-ttu-id="38ee8-133">Управление жизненным циклом приложений</span><span class="sxs-lookup"><span data-stu-id="38ee8-133">Application Lifecycle Management</span></span>

- <span data-ttu-id="38ee8-134">Упрощенная процедура утверждения: больше не нужно знать администратора клиента.</span><span class="sxs-lookup"><span data-stu-id="38ee8-134">Streamlined approval experience: no need to know who your tenant admin is anymore</span></span>
    - <span data-ttu-id="38ee8-135">Владелец инициирует процедуру утверждения.</span><span class="sxs-lookup"><span data-stu-id="38ee8-135">Owner initiate the approval process</span></span>
    - <span data-ttu-id="38ee8-136">Администратор клиента автоматически получает уведомление.</span><span class="sxs-lookup"><span data-stu-id="38ee8-136">Tenant admin gets automatically notified</span></span> 
    - <span data-ttu-id="38ee8-137">Параметры управления процедурой утверждения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="38ee8-137">Settings to control the default experience around approval process</span></span>

- <span data-ttu-id="38ee8-138">ALM REST API — развертывание, активация, удаление и обновление приложений и надстроек.</span><span class="sxs-lookup"><span data-stu-id="38ee8-138">ALM REST APIs - Deploy, activate, delete and upgrade apps and add-ins</span></span>
- <span data-ttu-id="38ee8-139">Предполагается, что ALM REST API будут поддерживать *все* объекты в каталоге приложений, в том числе надстройки.</span><span class="sxs-lookup"><span data-stu-id="38ee8-139">ALM REST APIs targeted to support *everything* in the App Catalog, including add-ins</span></span>
- <span data-ttu-id="38ee8-140">Автоматическое размещение кода в CDN.</span><span class="sxs-lookup"><span data-stu-id="38ee8-140">Automatic CDN hosting for code</span></span>
    - <span data-ttu-id="38ee8-141">Добавление пакета JavaScript в пакет приложения, который затем автоматически развертывается в библиотеке, размещаемой в сети CDN Office 365 клиента.</span><span class="sxs-lookup"><span data-stu-id="38ee8-141">Package JavaScript bundle into app package, which is automatically then deployed to a library that gets hosted on your tenant Office 365 CDN</span></span>


## <a name="developer-experience"></a><span data-ttu-id="38ee8-142">Удобство для разработчиков</span><span class="sxs-lookup"><span data-stu-id="38ee8-142">Developer Experience</span></span>
- <span data-ttu-id="38ee8-143">SharePoint Framework Workbench 2.0: поддержка не только клиентских веб-частей, но и новых типов компонентов.</span><span class="sxs-lookup"><span data-stu-id="38ee8-143">SharePoint Framework Workbench 2.0: Development story beyond web parts with support for new component types on top of client-side web parts</span></span>
- <span data-ttu-id="38ee8-144">Компоненты цепочки инструментов.</span><span class="sxs-lookup"><span data-stu-id="38ee8-144">Tool Chain Components</span></span>
- <span data-ttu-id="38ee8-145">Дополнительные шаблоны yeoman.</span><span class="sxs-lookup"><span data-stu-id="38ee8-145">Additional Yeoman Templates</span></span>


## <a name="additional-resources"></a><span data-ttu-id="38ee8-146">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="38ee8-146">Additional resources</span></span>
<span data-ttu-id="38ee8-147">Узнавайте о новых выпусках и возможностях SharePoint Framework из следующих ресурсов.</span><span class="sxs-lookup"><span data-stu-id="38ee8-147">Please use following resources to stay up to date on the new releases and capabilities being released for SharePoint Framework.</span></span>

* [<span data-ttu-id="38ee8-148">dev.office.com blog</span><span class="sxs-lookup"><span data-stu-id="38ee8-148">dev.office.com blog</span></span>](https://dev.office.com/blogs)
* [<span data-ttu-id="38ee8-149">Учетная запись OfficeDev в Твиттере</span><span class="sxs-lookup"><span data-stu-id="38ee8-149">OfficeDev Twitter account</span></span>](https://twitter.com/officedev)
