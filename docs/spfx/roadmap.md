<span data-ttu-id="6535c-p102">Примечание. Это список областей, над которыми работают инженеры SharePoint. Элементы и разделы из этого списка будут постепенно находить воплощение в будущих выпусках SharePoint Framework (**необязательно** все идеи будут реализованы).</span><span class="sxs-lookup"><span data-stu-id="6535c-p102">Notice. This is a list of areas which SharePoint engineering is having in the backlog and are looking into. This does **NOT** mean that all of them will be necessarily delivered, but we are looking for getting items and topics from this list gradually released with the future releases of SharePoint Framework.</span></span>

> Примечание. Это список областей, над которыми работают инженеры SharePoint. Элементы и разделы из этого списка будут постепенно находить воплощение в будущих выпусках SharePoint Framework (**необязательно** все идеи будут реализованы).  

## <a name="on-premises-support"></a><span data-ttu-id="6535c-108">Поддержка локальных сред</span><span class="sxs-lookup"><span data-stu-id="6535c-108">On-premises support</span></span>

- <span data-ttu-id="6535c-109">Предоставление в составе пакета дополнительных компонентов 2 для SharePoint 2016.</span><span class="sxs-lookup"><span data-stu-id="6535c-109">Shipping as part of Feature Pack 2 for SharePoint 2016</span></span>
- <span data-ttu-id="6535c-110">Те же возможности, что и в SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="6535c-110">Similar feature capabilities as in SharePoint Online</span></span>
- <span data-ttu-id="6535c-111">Предоставление общей платформы разработки в локальной среде и облаке.</span><span class="sxs-lookup"><span data-stu-id="6535c-111">Target is to provide common development platform across on-premises and the cloud</span></span>
- <span data-ttu-id="6535c-112">Использование современной цепочки инструментов и открытого кода в локальных средах.</span><span class="sxs-lookup"><span data-stu-id="6535c-112">Leveraging modern toolchain and open source on “legacy” environments</span></span>
- <span data-ttu-id="6535c-113">Ориентация на версию SharePoint 2016 в 2017 г.</span><span class="sxs-lookup"><span data-stu-id="6535c-113">Targeting SharePoint 2016 version during calendar year 2017</span></span>

## <a name="general-improvements"></a><span data-ttu-id="6535c-114">Общие улучшения</span><span class="sxs-lookup"><span data-stu-id="6535c-114">General improvements</span></span>

- <span data-ttu-id="6535c-115">Удобство вызова API Graph для доступа к данным пользователей (GraphHttpClient в предварительной версии для разработчиков).</span><span class="sxs-lookup"><span data-stu-id="6535c-115">Easy access to Graph API to access user specific information</span></span>
- <span data-ttu-id="6535c-116">Каталог приложений семейства веб-сайтов с управлением на уровне клиента для обеспечения более простого развертывания решений.</span><span class="sxs-lookup"><span data-stu-id="6535c-116">Site collection app catalog with tenant level control for enabling easier solution deployed</span></span> 

## <a name="client-side-web-parts-and-add-ins"></a><span data-ttu-id="6535c-117">Клиентские веб-части++ и надстройки</span><span class="sxs-lookup"><span data-stu-id="6535c-117">Client-side web parts++ and add-ins</span></span>

- <span data-ttu-id="6535c-118">Поддержка более сложных сценариев и взаимодействий с веб-частями</span><span class="sxs-lookup"><span data-stu-id="6535c-118">Supporting more complex scenarios and interactions with web parts</span></span>
    - <span data-ttu-id="6535c-119">Обмен данными между веб-частями</span><span class="sxs-lookup"><span data-stu-id="6535c-119">Part-to-part communication</span></span>
    - <span data-ttu-id="6535c-120">Изоляция платформы JS</span><span class="sxs-lookup"><span data-stu-id="6535c-120">JS Framework isolation</span></span>
    - <span data-ttu-id="6535c-121">Модель "разработчик-любитель" для простых задач разработки</span><span class="sxs-lookup"><span data-stu-id="6535c-121">"citizen developer" model for lightweight development</span></span>

- <span data-ttu-id="6535c-122">Реализация современных технологий оформления веб-частей.</span><span class="sxs-lookup"><span data-stu-id="6535c-122">Bring add-ins to the modern world: Let’s make them play nicer with the new UX.</span></span> 
    - <span data-ttu-id="6535c-123">Регистрация в Azure AD</span><span class="sxs-lookup"><span data-stu-id="6535c-123">Azure AD Registration</span></span>
    - <span data-ttu-id="6535c-124">Встроенная поддержка адаптивного дизайна</span><span class="sxs-lookup"><span data-stu-id="6535c-124">Native responsive support</span></span> 
    - <span data-ttu-id="6535c-125">Создание надстроек с помощью SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="6535c-125">Build Add-Ins with SharePoint Framework</span></span>

## <a name="javascript-embedding-support-jslink-user-custom-actions"></a><span data-ttu-id="6535c-126">Поддержка внедрения JavaScript (JSLink, дополнительные действия пользователей)</span><span class="sxs-lookup"><span data-stu-id="6535c-126">JavaScript embedding support (JSLink, User Custom Actions)</span></span>

- <span data-ttu-id="6535c-127">Те же цепочка инструментов и модель развертывания, что и для клиентских веб-частей.</span><span class="sxs-lookup"><span data-stu-id="6535c-127">The same tool chain and deployment model as client side web parts.</span></span>
- <span data-ttu-id="6535c-128">Наследование от строго типизированного базового класса везде, где это возможно, вместо прямого управления моделью DOM страницы.</span><span class="sxs-lookup"><span data-stu-id="6535c-128">Derive from a strongly typed base class wherever possible rather than manipulating the page DOM directly.</span></span>
- <span data-ttu-id="6535c-129">Обеспечение использования современных расширений и возможностей, подобных дополнительным действиям и JSLink, в случае классического варианта.</span><span class="sxs-lookup"><span data-stu-id="6535c-129">Enable modern extension usage with modern experiences similar as Custom Actions and JS Link in classic experience</span></span>
- <span data-ttu-id="6535c-130">Работа с NoScript через каталог приложений клиента.</span><span class="sxs-lookup"><span data-stu-id="6535c-130">Work with NoScript via tenant app catalog</span></span>

> <span data-ttu-id="6535c-131">Эта возможность теперь доступна в [предварительной версии для разработчиков](https://dev.office.com/blogs/announcing-availability-of-sharepoint-framework-extensions-developer-preview).</span><span class="sxs-lookup"><span data-stu-id="6535c-131">This is now available in [developer preview](https://dev.office.com/blogs/announcing-availability-of-sharepoint-framework-extensions-developer-preview).</span></span>

## <a name="application-lifecycle-management"></a><span data-ttu-id="6535c-132">Управление жизненным циклом приложений</span><span class="sxs-lookup"><span data-stu-id="6535c-132">SharePoint Server 2013 Application Lifecycle Management</span></span>

- <span data-ttu-id="6535c-133">Упрощенная процедура утверждения: больше не нужно знать администратора клиента.</span><span class="sxs-lookup"><span data-stu-id="6535c-133">Streamlined approval experience: no need to know who your tenant admin is anymore</span></span>
    - <span data-ttu-id="6535c-134">Владелец инициирует процедуру утверждения.</span><span class="sxs-lookup"><span data-stu-id="6535c-134">Owner initiate the approval process</span></span>
    - <span data-ttu-id="6535c-135">Администратор клиента автоматически получает уведомление.</span><span class="sxs-lookup"><span data-stu-id="6535c-135">Tenant admin gets automatically notified</span></span> 
    - <span data-ttu-id="6535c-136">Параметры управления процедурой утверждения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="6535c-136">Settings to control the default experience around approval process</span></span>

- <span data-ttu-id="6535c-137">ALM REST API — развертывание, активация, удаление и обновление приложений и надстроек.</span><span class="sxs-lookup"><span data-stu-id="6535c-137">ALM REST APIs - Deploy, activate, delete and upgrade apps and add-ins</span></span>
- <span data-ttu-id="6535c-138">Предполагается, что ALM REST API будут поддерживать *все* объекты в каталоге приложений, в том числе надстройки.</span><span class="sxs-lookup"><span data-stu-id="6535c-138">ALM REST APIs targeted to support *everything* in the App Catalog, including add-ins</span></span>
- <span data-ttu-id="6535c-139">Автоматическое размещение кода в CDN.</span><span class="sxs-lookup"><span data-stu-id="6535c-139">Automatic CDN hosting for code</span></span>
    - <span data-ttu-id="6535c-140">Добавление пакета JavaScript в пакет приложения, который затем автоматически развертывается в библиотеке, размещаемой в сети CDN Office 365 клиента.</span><span class="sxs-lookup"><span data-stu-id="6535c-140">Package JavaScript bundle into app package, which is automatically then deployed to a library that gets hosted on your tenant Office 365 CDN</span></span>


## <a name="developer-experience"></a><span data-ttu-id="6535c-141">Удобство для разработчиков</span><span class="sxs-lookup"><span data-stu-id="6535c-141">Developer Experience</span></span>
- <span data-ttu-id="6535c-142">SharePoint Framework Workbench 2.0: поддержка не только клиентских веб-частей, но и новых типов компонентов.</span><span class="sxs-lookup"><span data-stu-id="6535c-142">SharePoint Framework Workbench 2.0: Development story beyond web parts with support for new component types on top of client-side web parts</span></span>
- <span data-ttu-id="6535c-143">Компоненты цепочки инструментов.</span><span class="sxs-lookup"><span data-stu-id="6535c-143">Tool Chain Components</span></span>
- <span data-ttu-id="6535c-144">Дополнительные шаблоны yeoman.</span><span class="sxs-lookup"><span data-stu-id="6535c-144">Additional Yeoman Templates</span></span>


## <a name="additional-resources"></a><span data-ttu-id="6535c-145">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="6535c-145">Additional resources</span></span>
<span data-ttu-id="6535c-146">Узнавайте о новых выпусках и возможностях SharePoint Framework из следующих ресурсов.</span><span class="sxs-lookup"><span data-stu-id="6535c-146">Please use following resources to stay up to date on the new releases and capabilities being released for SharePoint Framework.</span></span>

* [<span data-ttu-id="6535c-147">dev.office.com blog</span><span class="sxs-lookup"><span data-stu-id="6535c-147">dev.office.com blog</span></span>](https://dev.office.com/blogs)
* [<span data-ttu-id="6535c-148">Учетная запись OfficeDev в Твиттере</span><span class="sxs-lookup"><span data-stu-id="6535c-148">OfficeDev Twitter account</span></span>](https://twitter.com/officedev)
