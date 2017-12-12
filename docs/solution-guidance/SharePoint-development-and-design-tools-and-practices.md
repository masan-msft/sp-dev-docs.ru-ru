---
title: "Средства разработки и проектирования SharePoint и рекомендации"
ms.date: 11/03/2017
ms.openlocfilehash: 21d48416cdf3b556200e3f7fc2cb29d4d99ad4a6
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="sharepoint-development-and-design-tools-and-practices"></a><span data-ttu-id="cb78c-102">Средства разработки и проектирования SharePoint и рекомендации</span><span class="sxs-lookup"><span data-stu-id="cb78c-102">SharePoint development and design tools and practices</span></span>

<span data-ttu-id="cb78c-103">Средства проектирования и разработки SharePoint можно использовать для применения фирменной символики для сайтов SharePoint.</span><span class="sxs-lookup"><span data-stu-id="cb78c-103">You can use SharePoint design and development tools to apply branding to your SharePoint sites.</span></span>

<span data-ttu-id="cb78c-104">_**Область применения:** Office 365 | SharePoint 2013 | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="cb78c-104">_**Applies to:** Office 365 | SharePoint 2013 | SharePoint Online_</span></span>

<span data-ttu-id="cb78c-105">В этой статье представлены сведения о параметрах проектирования и разработки, доступных в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="cb78c-105">This article provides information about the development and design options that are available in SharePoint.</span></span> <span data-ttu-id="cb78c-106">Кроме того, можно найти сведения об использовании удаленного подготовки шаблон для применения фирменной настройки средств на сайте SharePoint.</span><span class="sxs-lookup"><span data-stu-id="cb78c-106">You can also find information about how to use the remote provisioning pattern to apply branding assets to a SharePoint site.</span></span>

## <a name="key-sharepoint-development-and-design-terms-and-concepts"></a><span data-ttu-id="cb78c-107">Клавиша SharePoint разработки и проектирования термины и концепции</span><span class="sxs-lookup"><span data-stu-id="cb78c-107">Key SharePoint development and design terms and concepts</span></span>
<span data-ttu-id="cb78c-108"><a name="sectionSection0"> </a></span><span class="sxs-lookup"><span data-stu-id="cb78c-108"></span></span>

|<span data-ttu-id="cb78c-109">**Концепция или термин**</span><span class="sxs-lookup"><span data-stu-id="cb78c-109">**Term or concept**</span></span>|<span data-ttu-id="cb78c-110">**Определение**</span><span class="sxs-lookup"><span data-stu-id="cb78c-110">**Definition**</span></span>|<span data-ttu-id="cb78c-111">**Дополнительные сведения**</span><span class="sxs-lookup"><span data-stu-id="cb78c-111">**More information**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="cb78c-112">Дизайнер</span><span class="sxs-lookup"><span data-stu-id="cb78c-112">Design Manager</span></span>|<span data-ttu-id="cb78c-113">Функциональная возможность, активировано в публикации сайтов или сайтов группы с поддержкой публикации SharePoint, который используется для импорта и управление сайтом фирменной символики активы и экспортировать их в пакете разработки.</span><span class="sxs-lookup"><span data-stu-id="cb78c-113">A feature activated in SharePoint publishing sites or Team sites with publishing enabled that is used to import and manage site branding assets and export them to a design package.</span></span>|<span data-ttu-id="cb78c-114">Используйте диспетчер структуры для импорта фирменной настройки средств, созданного в другие средства, такие как Adobe PhotoShop или Adobe DreamWeaver в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="cb78c-114">Use Design Manager to import branding assets created in other tools, such as Adobe PhotoShop or Adobe DreamWeaver, into SharePoint.</span></span><br/><span data-ttu-id="cb78c-115">SharePoint Designer не доступно для использования со службой OneDrive для бизнеса или SharePoint Team сайтов, где публикации не включено.</span><span class="sxs-lookup"><span data-stu-id="cb78c-115">SharePoint Designer is not available for use with OneDrive for Business or SharePoint Team sites where publishing is not enabled.</span></span>|
|<span data-ttu-id="cb78c-116">Пакет разработки</span><span class="sxs-lookup"><span data-stu-id="cb78c-116">Design package</span></span>|<span data-ttu-id="cb78c-117">Предназначен для использования с помощью сайтов публикации SharePoint 2013, содержит фирменной настройки средств, которые хранятся в диспетчере оформления.</span><span class="sxs-lookup"><span data-stu-id="cb78c-117">Designed for use with SharePoint 2013 Publishing sites, contains branding assets that are stored in Design Manager.</span></span>| [<span data-ttu-id="cb78c-118">Пакеты разработки дизайнер SharePoint 2013</span><span class="sxs-lookup"><span data-stu-id="cb78c-118">SharePoint 2013 Design Manager design packages</span></span>](http://msdn.microsoft.com/library/85ad1993-4d75-4806-9097-b934865a899a.aspx)|
|<span data-ttu-id="cb78c-119">Удаленный подготовки</span><span class="sxs-lookup"><span data-stu-id="cb78c-119">Remote provisioning</span></span>|<span data-ttu-id="cb78c-120">Модель, которая включает в себя подготовки сайтов с помощью шаблонов и кода, работающего под управлением SharePoint за пределы организации надстройки размещением у поставщика.</span><span class="sxs-lookup"><span data-stu-id="cb78c-120">A model that involves provisioning sites by using templates and code that runs outside SharePoint in a provider-hosted add-in.</span></span>| [<span data-ttu-id="cb78c-121">Веб-сайтов подготовки методик и удаленных подготовки в SharePoint 2013</span><span class="sxs-lookup"><span data-stu-id="cb78c-121">Site provisioning techniques and remote provisioning in SharePoint 2013</span></span>](http://blogs.msdn.com/b/vesku/archive/2013/08/23/site-provisioning-techniques-and-remote-provisioning-in-sharepoint-2013.aspx)<br/>[<span data-ttu-id="cb78c-122">Подготовка самостоятельного создания сайтов с использованием приложений в SharePoint 2013</span><span class="sxs-lookup"><span data-stu-id="cb78c-122">Self-service site provisioning using apps in SharePoint 2013</span></span>](http://blogs.msdn.com/b/richard_dizeregas_blog/archive/2013/04/04/self-service-site-provisioning-using-apps-for-sharepoint-2013.aspx)|
|<span data-ttu-id="cb78c-123">Корневой веб-узел</span><span class="sxs-lookup"><span data-stu-id="cb78c-123">Root web</span></span>|<span data-ttu-id="cb78c-124">Первый веб-сайта в семействе сайтов.</span><span class="sxs-lookup"><span data-stu-id="cb78c-124">The first web inside a site collection.</span></span> <span data-ttu-id="cb78c-125">Корневого веб-узла иногда называется корня веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="cb78c-125">The root web is also sometimes referred to as the Web Application Root.</span></span>||
|<span data-ttu-id="cb78c-126">Изолированные решения</span><span class="sxs-lookup"><span data-stu-id="cb78c-126">Sandboxed solutions</span></span>|<span data-ttu-id="cb78c-127">WSP-файлов, содержащих сборки, других компонентов не компилируются и XML-файл манифеста.</span><span class="sxs-lookup"><span data-stu-id="cb78c-127">.wsp files that contain assemblies, other non-compiled components, and an XML manifest file.</span></span> <span data-ttu-id="cb78c-128">Изолированные решения с помощью кода с частичным доверием.</span><span class="sxs-lookup"><span data-stu-id="cb78c-128">A sandbox solution uses partial-trust code.</span></span>| [<span data-ttu-id="cb78c-129">Изолированные решения</span><span class="sxs-lookup"><span data-stu-id="cb78c-129">Sandboxed solutions</span></span>](https://msdn.microsoft.com/en-us/library/ff798382.aspx)|
|<span data-ttu-id="cb78c-130">SharePoint Designer 2013</span><span class="sxs-lookup"><span data-stu-id="cb78c-130">SharePoint Designer 2013</span></span>|<span data-ttu-id="cb78c-131">HTML-код конструктора и разработки средства управления средством управления фирменной настройки элементов в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="cb78c-131">An HTML designer and design asset management tool for managing branding elements in SharePoint.</span></span> <span data-ttu-id="cb78c-132">В SharePoint 2013 SharePoint Designer главным образом поддерживает настраиваемых рабочих процессов.</span><span class="sxs-lookup"><span data-stu-id="cb78c-132">In SharePoint 2013, SharePoint Designer mainly supports custom workflows.</span></span>| [<span data-ttu-id="cb78c-133">Изменения в SharePoint Designer 2013?</span><span class="sxs-lookup"><span data-stu-id="cb78c-133">What's changed in SharePoint Designer 2013?</span></span>](https://msdn.microsoft.com/en-us/library/office/jj728659.aspx)<br/>[<span data-ttu-id="cb78c-134">Новые возможности разработки сайтов SharePoint 2013?</span><span class="sxs-lookup"><span data-stu-id="cb78c-134">What's new with SharePoint 2013 site development?</span></span>](https://msdn.microsoft.com/en-us/library/office/jj163942.aspx)|
|<span data-ttu-id="cb78c-135">WSP-файла</span><span class="sxs-lookup"><span data-stu-id="cb78c-135">.wsp file</span></span>|<span data-ttu-id="cb78c-136">Файл решения SharePoint.</span><span class="sxs-lookup"><span data-stu-id="cb78c-136">A SharePoint solution file.</span></span> <span data-ttu-id="cb78c-137">WSP-файл находится в CAB-файле, относящие ресурсах сайта и упорядочивает их с помощью файла manifest.xml.</span><span class="sxs-lookup"><span data-stu-id="cb78c-137">A .wsp is a .cab file that categorizes site assets and organizes them with a manifest.xml file.</span></span>| [<span data-ttu-id="cb78c-138">Обзор решений</span><span class="sxs-lookup"><span data-stu-id="cb78c-138">Solutions overview</span></span>](https://msdn.microsoft.com/en-us/library/office/aa543214%28v=office.14%29.aspx)|

## <a name="development-options"></a><span data-ttu-id="cb78c-139">Параметры разработки</span><span class="sxs-lookup"><span data-stu-id="cb78c-139">Development options</span></span>
<span data-ttu-id="cb78c-140"><a name="sectionSection1"> </a></span><span class="sxs-lookup"><span data-stu-id="cb78c-140"></span></span>

<span data-ttu-id="cb78c-141">При использовании SharePoint 2013 в качестве платформы разработки, вам потребуются для создания среды для разработки, тестирования, построения и развертывания контента.</span><span class="sxs-lookup"><span data-stu-id="cb78c-141">When you use SharePoint 2013 as a development platform, you'll need to create an environment to develop, test, build, and deploy your content.</span></span> <span data-ttu-id="cb78c-142">Сведения о параметрах для разработки см в статье [Управление жизненным циклом приложений SharePoint Server 2013](http://msdn.microsoft.com/library/caaf9a09-2e6a-49e3-a8d6-aaf7f93a842a.aspx) [аспекты среды разработки](http://msdn.microsoft.com/library/caaf9a09-2e6a-49e3-a8d6-aaf7f93a842a.aspx#DevEnvironment) .</span><span class="sxs-lookup"><span data-stu-id="cb78c-142">For information about the options for development, see  [Development environment considerations](http://msdn.microsoft.com/library/caaf9a09-2e6a-49e3-a8d6-aaf7f93a842a.aspx#DevEnvironment) in the article [SharePoint Server 2013 Application Lifecycle Management](http://msdn.microsoft.com/library/caaf9a09-2e6a-49e3-a8d6-aaf7f93a842a.aspx).</span></span> <span data-ttu-id="cb78c-143">В таблице 2 приведены сведения о выполнении для различных вариантов разработки.</span><span class="sxs-lookup"><span data-stu-id="cb78c-143">Table 2 lists the considerations for the various development options.</span></span> 

<span data-ttu-id="cb78c-144">**Параметры для разработки SharePoint, тестирования и приемки**</span><span class="sxs-lookup"><span data-stu-id="cb78c-144">**Options for SharePoint development, testing, and acceptance**</span></span>

|<span data-ttu-id="cb78c-145">**Вариант**</span><span class="sxs-lookup"><span data-stu-id="cb78c-145">**Option**</span></span>|<span data-ttu-id="cb78c-146">**Сведения о выполнении**</span><span class="sxs-lookup"><span data-stu-id="cb78c-146">**Considerations**</span></span>|
|:-----|:-----|
|<span data-ttu-id="cb78c-147">Сервера Team foundation server</span><span class="sxs-lookup"><span data-stu-id="cb78c-147">Team foundation server</span></span>|<span data-ttu-id="cb78c-148">-Находится в Visual Studio Online для быстрого доступа.</span><span class="sxs-lookup"><span data-stu-id="cb78c-148">- Located on Visual Studio Online for easy access.</span></span><br/><span data-ttu-id="cb78c-149">-Включает в себя систему централизованного исходного кода и жизненного цикла управления.</span><span class="sxs-lookup"><span data-stu-id="cb78c-149">- Includes a centralized source code and life cycle management system.</span></span>|
|<span data-ttu-id="cb78c-150">Облако сред тестирования и приемки</span><span class="sxs-lookup"><span data-stu-id="cb78c-150">Cloud test and acceptance environments</span></span>|<span data-ttu-id="cb78c-151">-Используйте отдельные клиента для приемочного тестирования.</span><span class="sxs-lookup"><span data-stu-id="cb78c-151">- Use a separate tenant for acceptance testing.</span></span><br/><span data-ttu-id="cb78c-152">-Отдельные тестовой среды для локальной проверки.</span><span class="sxs-lookup"><span data-stu-id="cb78c-152">- Separate test environment for on-premises testing.</span></span>|
|<span data-ttu-id="cb78c-153">Локальные среды тестирования и приемки</span><span class="sxs-lookup"><span data-stu-id="cb78c-153">On-premises test and acceptance environments</span></span>|<span data-ttu-id="cb78c-154">-Используется для локального развертывания SharePoint.</span><span class="sxs-lookup"><span data-stu-id="cb78c-154">- Use for on-premises SharePoint deployments.</span></span><br/><span data-ttu-id="cb78c-155">-Hosted клиента в локальной или в Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="cb78c-155">- Hosted by customer on-premises or in Microsoft Azure.</span></span>|
 
<span data-ttu-id="cb78c-156">В большинстве случаев потребуется по крайней мере следующие клиенты, однако может изменяться в зависимости от требований.</span><span class="sxs-lookup"><span data-stu-id="cb78c-156">In most cases, you'll need at least the following tenants, although this can vary depending on your requirements:</span></span>

-  <span data-ttu-id="cb78c-157">**Клиент разработчика**.</span><span class="sxs-lookup"><span data-stu-id="cb78c-157">**Developer tenant**.</span></span> <span data-ttu-id="cb78c-158">Рекомендуется подготовки и использования сайта разработчика.</span><span class="sxs-lookup"><span data-stu-id="cb78c-158">As a best practice, provision and use your own developer site.</span></span> <span data-ttu-id="cb78c-159">Таким образом, чтобы избежать совместное использование данных в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="cb78c-159">This way, you avoid mixing your data with the production environment.</span></span> <span data-ttu-id="cb78c-160">Для регистрации и Подготовка сайта разработчика, видеть [Подписка на сайте разработчика Office 365](http://msdn.microsoft.com/library/b22ce52a-ae9e-4831-9b68-c9210af6dc54.aspx#o365_signup) в статье [Подписка на подписку разработчика Office 365 и настройте свои инструменты и среду](http://msdn.microsoft.com/library/b22ce52a-ae9e-4831-9b68-c9210af6dc54.aspx).</span><span class="sxs-lookup"><span data-stu-id="cb78c-160">To sign up for and provision a developer site, see  [Sign up for an Office 365 Developer Site](http://msdn.microsoft.com/library/b22ce52a-ae9e-4831-9b68-c9210af6dc54.aspx#o365_signup) in the article [Sign up for an Office 365 Developer Subscription and set up your tools and environment](http://msdn.microsoft.com/library/b22ce52a-ae9e-4831-9b68-c9210af6dc54.aspx).</span></span>
    
-  <span data-ttu-id="cb78c-161">**Интеграция и тестирование клиента**.</span><span class="sxs-lookup"><span data-stu-id="cb78c-161">**Integration/testing tenant**.</span></span> <span data-ttu-id="cb78c-162">Используйте этот сайт для убедитесь в том, что новые приложения и функциональные возможности работы через более одного семейства веб-сайтов и от служб и данных в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="cb78c-162">Use this site to make sure that new apps and functionality work across more than one site collection and against the services and data in the production environment.</span></span> <span data-ttu-id="cb78c-163">Настройка среды для включения возможности, доступные в режиме предварительного просмотра.</span><span class="sxs-lookup"><span data-stu-id="cb78c-163">Configure the environment to include capabilities that are in preview.</span></span> <span data-ttu-id="cb78c-164">(Для этого в консоль администрирования клиента, выберите **Параметры службы**и выберите в разделе параметра **обновление** **Первого выпуска**.) Интернет-версия Visual Studio можно использовать для запуска автоматического тестирования и любые другие тестирование непрерывной интеграции.</span><span class="sxs-lookup"><span data-stu-id="cb78c-164">(To do this, in your tenant admin console, choose  **Service Settings**, and then under the  **Updates** setting, choose **First Release**.) You can use Visual Studio online to run automated testing and any other continuous integration testing.</span></span>
    
-  <span data-ttu-id="cb78c-165">**Рабочий клиент**.</span><span class="sxs-lookup"><span data-stu-id="cb78c-165">**Production tenant**.</span></span> <span data-ttu-id="cb78c-166">Выпуск проверен, обслуживаемые и утвержденных приложений для клиента.</span><span class="sxs-lookup"><span data-stu-id="cb78c-166">Release tested, accepted, and approved apps to this tenant.</span></span> <span data-ttu-id="cb78c-167">На этом клиента для разработки и тестирования приложений, которые находятся небольшие в область или обнаружили воздействия можно создать на сайте разработчика.</span><span class="sxs-lookup"><span data-stu-id="cb78c-167">You can create a developer site on this tenant to develop and test apps that are small in scope or have isolated impact.</span></span> <span data-ttu-id="cb78c-168">Следует Избегайте, совместное использование вашей разработки и рабочей среды.</span><span class="sxs-lookup"><span data-stu-id="cb78c-168">In general, avoid mixing your development and production environments.</span></span>
    
## <a name="design-tools"></a><span data-ttu-id="cb78c-169">Средства разработки</span><span class="sxs-lookup"><span data-stu-id="cb78c-169">Design tools</span></span>
<span data-ttu-id="cb78c-170"><a name="sectionSection2"> </a></span><span class="sxs-lookup"><span data-stu-id="cb78c-170"></span></span>

<span data-ttu-id="cb78c-171">Используйте стандартные средства веб-проектирования и разработки, таких как HTML, изображений, CSS-файлы и файлы JavaScript для создания сайта SharePoint, фирменная символика активов.</span><span class="sxs-lookup"><span data-stu-id="cb78c-171">Use standard web design and development tools, such as HTML, images, CSS files, and JavaScript files to create SharePoint site branding assets.</span></span> <span data-ttu-id="cb78c-172">Например Adobe DreamWeaver и Adobe PhotoShop можно использовать для разработки HTML, CSS, JavaScript и файлы изображений, которые будут использоваться для фирменной символики на сайтах SharePoint.</span><span class="sxs-lookup"><span data-stu-id="cb78c-172">For example, you can use Adobe DreamWeaver and Adobe PhotoShop to design the HTML, CSS, JavaScript, and image files you'll use to brand your SharePoint sites.</span></span> <span data-ttu-id="cb78c-173">Кроме того можно использовать SharePoint Designer 2013 для создания, управления и Настройка фирменной настройки средств или создание настраиваемых решений в Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="cb78c-173">Alternatively, you can use SharePoint Designer 2013 to create, manage, and customize branding assets, or create custom solutions in Visual Studio 2013.</span></span>

### <a name="sharepoint-design-packages-and-wsp-files"></a><span data-ttu-id="cb78c-174">Пакеты разработки SharePoint и WSP-файлов</span><span class="sxs-lookup"><span data-stu-id="cb78c-174">SharePoint design packages and .wsp files</span></span>

<span data-ttu-id="cb78c-175">Пакеты разработки — WSP-файлы, созданные с дизайнер, соответствующие правилам прогнозируемый для упаковки средств разработки.</span><span class="sxs-lookup"><span data-stu-id="cb78c-175">Design packages are .wsp files created by Design Manager that follow predictable rules for packaging design assets.</span></span> <span data-ttu-id="cb78c-176">Это, по сути, изолированных решений.</span><span class="sxs-lookup"><span data-stu-id="cb78c-176">They are, essentially, sandboxed solutions.</span></span> <span data-ttu-id="cb78c-177">Если вы используете еще одно средство, пакет фирменной символики активами в WSP-файл, фирменной настройки средств будет находиться в состоянии менее основных и предсказуемым.</span><span class="sxs-lookup"><span data-stu-id="cb78c-177">If you're using another tool to package branding assets in a .wsp file, your branding assets will be in a less fixed and predictable state.</span></span>

<span data-ttu-id="cb78c-178">Пакет разработки включает все файлы, которые были настроены.</span><span class="sxs-lookup"><span data-stu-id="cb78c-178">The design package includes all files that have been customized.</span></span> <span data-ttu-id="cb78c-179">Например при создании макета страницы, которая использует пользовательский тип содержимого, пакет разработки включает макет страницы, настраиваемого типа контента, которые он использует и все настраиваемые столбцы сайта.</span><span class="sxs-lookup"><span data-stu-id="cb78c-179">For example, if you create a page layout that uses a custom content type, the design package includes the page layout, the custom content type it uses, and all custom site columns.</span></span> <span data-ttu-id="cb78c-180">Пакет разработки также включает несколько файлов, связанных с вариантов оформления, примененные к сайту SharePoint, включая файлы, загруженные в следующих местоположениях:</span><span class="sxs-lookup"><span data-stu-id="cb78c-180">The design package also includes several files related to any composed looks that have been applied to your SharePoint site, including files uploaded to the following locations:</span></span>

- <span data-ttu-id="cb78c-181">Библиотеки материалы сайта</span><span class="sxs-lookup"><span data-stu-id="cb78c-181">Site assets library</span></span>
    
- <span data-ttu-id="cb78c-182">Библиотека стилей</span><span class="sxs-lookup"><span data-stu-id="cb78c-182">Style library</span></span>
    
- <span data-ttu-id="cb78c-183">Коллекция главных страниц</span><span class="sxs-lookup"><span data-stu-id="cb78c-183">Master Page gallery</span></span>
    
<span data-ttu-id="cb78c-184">Если вариантов оформления применяется к сайту, перед применением настраиваемый фирменный стиль, пакет разработки будут включены файлы с расширениями .themedcss и .themedpng.</span><span class="sxs-lookup"><span data-stu-id="cb78c-184">If you applied composed looks to a site before you applied custom branding, the design package will include files with .themedcss and .themedpng file extensions.</span></span> <span data-ttu-id="cb78c-185">Для применения фирменной настройки средств в пакете разработки на сайте SharePoint, Экспорт пакета проектирования и использование удаленного подготовки шаблон для применения содержимое пакета конструктора.</span><span class="sxs-lookup"><span data-stu-id="cb78c-185">To apply the branding assets in a design package to a SharePoint site, export the design package and use the remote provisioning pattern to apply the contents of the design package.</span></span>

<span data-ttu-id="cb78c-186">SharePoint 2013 включает в себя API-интерфейсы, которые можно использовать для работы с помощью конструктора пакетов.</span><span class="sxs-lookup"><span data-stu-id="cb78c-186">SharePoint 2013 includes the APIs that you can use to work with design packages.</span></span> <span data-ttu-id="cb78c-187">Если вы используете SSOM, CSOM или JSOM, можно использовать классы [DesignPackage](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.publishing.designpackage.aspx) или [DesignPackageInfo](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.publishing.designpackageinfo.aspx) .</span><span class="sxs-lookup"><span data-stu-id="cb78c-187">If you're using either SSOM, CSOM, or JSOM, you can use the  [DesignPackage](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.publishing.designpackage.aspx) or [DesignPackageInfo](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.publishing.designpackageinfo.aspx) classes.</span></span>

#### <a name="using-the-design-package-csom-to-apply-the-contents-of-design-packages-to-a-sharepoint-site"></a><span data-ttu-id="cb78c-188">С помощью пакета проектирования CSOM для применения содержимое пакетов проекта на сайте SharePoint</span><span class="sxs-lookup"><span data-stu-id="cb78c-188">Using the design package CSOM to apply the contents of design packages to a SharePoint site</span></span>

<span data-ttu-id="cb78c-189">Следующем примере показано, как использовать API пакета проектирования в шаблоне удаленного подготовки для применения содержимое пакетов проекта на сайте SharePoint.</span><span class="sxs-lookup"><span data-stu-id="cb78c-189">The following example shows how to use the Design Package APIs in the remote provisioning pattern to apply the contents of design packages to a SharePoint site.</span></span>

<span data-ttu-id="cb78c-190">Этот код был разработан для использования с сайтами публикации.</span><span class="sxs-lookup"><span data-stu-id="cb78c-190">This code was designed for use with Publishing sites.</span></span> <span data-ttu-id="cb78c-191">Несмотря на то, что можно использовать API пакетов разработки для применения фирменной символики для сайтов групп, которые имеют публикации функция включена, это может вызвать проблемы долгосрочного поддержки.</span><span class="sxs-lookup"><span data-stu-id="cb78c-191">Although it is possible to use the Design Packages API to apply branding to Team sites that have the Publishing feature enabled, this can introduce long-term support issues.</span></span>

> [!NOTE] 
> <span data-ttu-id="cb78c-192">Код, приведенный в данной статье предоставляется в качестве-без никаких гарантий, явных или подразумеваемых, включая никаких гарантий соответствие для определенной задачи, окупаемость или не нарушения прав.</span><span class="sxs-lookup"><span data-stu-id="cb78c-192">The code in this article is provided as-is, without warranty of any kind, either express or implied, including any implied warranties of fitness for a particular purpose, merchantability, or non-infringement.</span></span>

```
using Microsoft.SharePoint.Client;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;
using Microsoft.SharePoint.Client.Publishing;
namespace ProviderSharePointAppWeb
{
    public partial class Default : System.Web.UI.Page
    {
        protected void Page_PreInit(object sender, EventArgs e)
        {
            Uri redirectUrl;
            switch (SharePointContextProvider.CheckRedirectionStatus(Context, out redirectUrl))
            {
                case RedirectionStatus.Ok:
                    return;
                case RedirectionStatus.ShouldRedirect:
                    Response.Redirect(redirectUrl.AbsoluteUri, endResponse: true);
                    break;
                case RedirectionStatus.CanNotRedirect:
                    Response.Write("An error occurred while processing your request.");
                    Response.End();
                    break;
            }
        }

        protected void Page_Load(object sender, EventArgs e)
        {
            // Use TokenHelper to get the client context and Title property.
            // To access other properties, the add-in might need to request permissions
            // on the host web.
            var spContext = SharePointContextProvider.Current.GetSharePointContext(Context);
            
            // Publishing feature GUID to use the infrastructure for publishing. 
            Guid PublishingFeature = Guid.Parse("f6924d36-2fa8-4f0b-b16d-06b7250180fa");

            // The site-relative URL of the design package to install.
            // This sandbox design package should be uploaded to a document library.
            // For practical purposes, this can be a configuration setting in web.config.
            string fileRelativePath = @"/sites/devsite/brand/Dev.wsp";

            //string fileUrl = @"https://SPXXXXX.com/sites/devsite/brand/Dev.wsp";
            
        
            using (var clientContext = spContext.CreateUserClientContextForSPHost())
            {
                // Load the site context explicitly or while installing the API, the path for
// the package will not be resolved.
                // If the package cannot be found, an exception is thrown. 
                var site = clientContext.Site;
                clientContext.Load(site);
                clientContext.ExecuteQuery();
              
                // Validate whether the Publishing feature is active. 
                if (IsSiteFeatureActivated(clientContext,PublishingFeature))
                {
                    DesignPackageInfo info = new DesignPackageInfo()
                    {
                        PackageGuid = Guid.Empty,
                        MajorVersion = 1,
                        MinorVersion = 1,
                        PackageName = "Dev"
                    };
                    Console.WriteLine("Installing design package ");
                    
                    DesignPackage.Install(clientContext, clientContext.Site, info, fileRelativePath);
                    clientContext.ExecuteQuery();

                    Console.WriteLine("Applying design package");
                    DesignPackage.Apply(clientContext, clientContext.Site, info);
                    clientContext.ExecuteQuery();
                }
            }
        }
        public  bool IsSiteFeatureActivated( ClientContext context, Guid guid)
        {
            var features = context.Site.Features;
            context.Load(features);
            context.ExecuteQuery();

            foreach (var f in features)
            {
                if (f.DefinitionId.Equals(guid))
                    return true;
            }
            return false;
        }
 
    }
}
```

#### <a name="using-filecreationinformation-to-upload-branding-assets-and-a-master-page-to-a-team-site"></a><span data-ttu-id="cb78c-193">С помощью FileCreationInformation Отправка фирменной настройки активов и Главная страница сайта группы</span><span class="sxs-lookup"><span data-stu-id="cb78c-193">Using FileCreationInformation to upload branding assets and a master page to a Team site</span></span>

<span data-ttu-id="cb78c-194">Установка и удаление конструктора пакетов и экспорт конструктора пакетов в сайты SharePoint Online, можно использовать функциональные возможности SharePoint 2013 CSOM.</span><span class="sxs-lookup"><span data-stu-id="cb78c-194">You can use SharePoint 2013 CSOM functionality to install and uninstall design packages and export design packages to SharePoint Online sites.</span></span> <span data-ttu-id="cb78c-195">Например используйте [SP. Метод Publishing.DesignPackage.install (sp.publishing)](http://msdn.microsoft.com/library/26500127-210f-6c52-c0de-cf2894939a91.aspx) для установки пакета разработки на сайте, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="cb78c-195">For example, use the  [SP.Publishing.DesignPackage.install Method (sp.publishing)](http://msdn.microsoft.com/library/26500127-210f-6c52-c0de-cf2894939a91.aspx) to install the design package on the site, as shown in the following example.</span></span>

```
public static void Install(
        ClientRuntimeContext context,
        Site site,
        DesignPackageInfo info,
        string path
)
```

<span data-ttu-id="cb78c-196">Класс [DesignPackageInfo](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.publishing.designpackageinfo.aspx) указывает метаданные, которые описывают содержимое пакета проектирования для установки.</span><span class="sxs-lookup"><span data-stu-id="cb78c-196">The  [DesignPackageInfo](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.publishing.designpackageinfo.aspx) class specifies metadata that describe the contents of the design package to be installed.</span></span> <span data-ttu-id="cb78c-197">Метод [Uninstall](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.publishing.designpackage.uninstall.aspx) для удаления пакета конструктора с сайта, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="cb78c-197">Use the [Uninstall](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.publishing.designpackage.uninstall.aspx) method to uninstall the design package from the site, as shown in the following example.</span></span>

```
public static void UnInstall(
        ClientRuntimeContext context,
        Site site,
        DesignPackageInfo info
)
```

<span data-ttu-id="cb78c-198">Если вам потребуется фирменной символики сайта группы с публикацией в функциях включено, или публикации на сайт, на SharePoint Online, можно использовать метод [ExportSmallBusiness](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.publishing.designpackage.exportsmallbusiness.aspx) или [ExportEnterprise](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.publishing.designpackage.exportenterprise.aspx) экспорт пакетов разработки для шаблонов сайтов в решение Коллекция.</span><span class="sxs-lookup"><span data-stu-id="cb78c-198">If you need to brand a Team site with the Publishing feature enabled, or a Publishing site on SharePoint Online, you can use the  [ExportEnterprise](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.publishing.designpackage.exportenterprise.aspx) or the [ExportSmallBusiness](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.publishing.designpackage.exportsmallbusiness.aspx) method to export design packages for site templates to the Solution Gallery.</span></span> <span data-ttu-id="cb78c-199">Использование метода **ExportSmallBusiness** с шаблона сайта для малого бизнеса и используйте метод **ExportEnterprise** для всех шаблонов сайта, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="cb78c-199">Use the **ExportSmallBusiness** method with the small business site template, and use the **ExportEnterprise** method for all other site templates, as shown in the following example.</span></span> <span data-ttu-id="cb78c-200">В примере thatpackageName Примечание — это строка, представляющая имя пакета конструктора.</span><span class="sxs-lookup"><span data-stu-id="cb78c-200">In the example, note thatpackageName is a string that represents the name of the design package.</span></span>

```
public static ClientResult<DesignPackageInfo> ExportEnterprise(
        ClientRuntimeContext context,
        Site site,
        bool includeSearchConfiguration
)
```

<span data-ttu-id="cb78c-201">При использовании этого метода можно включить конфигурацию поиска в пакете разработки, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="cb78c-201">When you use this method, you can include the search configuration in the design package, as shown in the next example.</span></span> <span data-ttu-id="cb78c-202">Обратите внимание на то, что все методы пакета проектирования работают на уровне семейства веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="cb78c-202">Note that all design package methods operate at the level of the site collection.</span></span>

```
public static ClientResult<DesignPackageInfo> ExportSmallBusiness(
        ClientRuntimeContext context,
        Site site,
        string packageName,
        bool includeSearchConfiguration
)
```

## <a name="design-tool-options-for-sharepoint-online"></a><span data-ttu-id="cb78c-203">Параметры средства разработки для SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="cb78c-203">Design tool options for SharePoint Online</span></span>
<span data-ttu-id="cb78c-204"><a name="sectionSection3"> </a></span><span class="sxs-lookup"><span data-stu-id="cb78c-204"></span></span>

<span data-ttu-id="cb78c-205">Средства, которые можно использовать для фирменной символики сайта SharePoint Online зависят от SharePoint Online edition и тип сайта, который требуется построить.</span><span class="sxs-lookup"><span data-stu-id="cb78c-205">The tools you can use to brand a SharePoint Online site depend on your SharePoint Online edition and the type of site you want to build.</span></span> <span data-ttu-id="cb78c-206">Выпуск для малого бизнеса, например, включает одного сайта рабочих групп и один общедоступный сайт.</span><span class="sxs-lookup"><span data-stu-id="cb78c-206">The Small Business edition, for example, includes one Team site and one public site.</span></span> <span data-ttu-id="cb78c-207">Не включает публикации сайта.</span><span class="sxs-lookup"><span data-stu-id="cb78c-207">It does not include a Publishing site.</span></span> <span data-ttu-id="cb78c-208">Можно использовать надстройки построитель сайта в SharePoint Online для настройки общедоступного сайта фирменной символики.</span><span class="sxs-lookup"><span data-stu-id="cb78c-208">You can use the Site Builder add-in in SharePoint Online to customize public site branding.</span></span>

<span data-ttu-id="cb78c-209">Enterprise edition включает в себя семейства сайтов групп в корневой веб-приложение для домена, который не включает публикации.</span><span class="sxs-lookup"><span data-stu-id="cb78c-209">The Enterprise edition includes a Team site collection at the root web application for the domain that does not include Publishing.</span></span> <span data-ttu-id="cb78c-210">Он не включает общедоступный сайт.</span><span class="sxs-lookup"><span data-stu-id="cb78c-210">It does not include a public site.</span></span> <span data-ttu-id="cb78c-211">Управление SharePoint с помощью конструктора диспетчера фирменной настройки элементами сайтов для публикации сайта в SharePoint Online Enterprise edition.</span><span class="sxs-lookup"><span data-stu-id="cb78c-211">Use Design Manager to manage SharePoint site branding elements for the Publishing site in the SharePoint Online Enterprise edition.</span></span>

## <a name="see-also"></a><span data-ttu-id="cb78c-212">См. также</span><span class="sxs-lookup"><span data-stu-id="cb78c-212">See also</span></span>
<span data-ttu-id="cb78c-213"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="cb78c-213"></span></span>

-  [<span data-ttu-id="cb78c-214">Фирменная символика и решения для SharePoint 2013 и SharePoint Online по подготовке сайта</span><span class="sxs-lookup"><span data-stu-id="cb78c-214">Branding and site provisioning solutions for SharePoint 2013 and SharePoint Online</span></span>](Branding-and-site-provisioning-solutions-for-SharePoint.md)
    
-  [<span data-ttu-id="cb78c-215">Управление жизненным циклом приложений SharePoint Server 2013</span><span class="sxs-lookup"><span data-stu-id="cb78c-215">SharePoint Server 2013 Application Lifecycle Management</span></span>](http://msdn.microsoft.com/library/caaf9a09-2e6a-49e3-a8d6-aaf7f93a842a.aspx)
    
-  [<span data-ttu-id="cb78c-216">Изолированные решения</span><span class="sxs-lookup"><span data-stu-id="cb78c-216">Sandboxed solutions</span></span>](https://msdn.microsoft.com/en-us/library/ff798382.aspx)
    
-  [<span data-ttu-id="cb78c-217">Веб-сайтов подготовки методик и удаленных подготовки в SharePoint 2013</span><span class="sxs-lookup"><span data-stu-id="cb78c-217">Site provisioning techniques and remote provisioning in SharePoint 2013</span></span>](http://blogs.msdn.com/b/vesku/archive/2013/08/23/site-provisioning-techniques-and-remote-provisioning-in-sharepoint-2013.aspx)
    
-  [<span data-ttu-id="cb78c-218">Пакеты разработки дизайнер SharePoint 2013</span><span class="sxs-lookup"><span data-stu-id="cb78c-218">SharePoint 2013 Design Manager design packages</span></span>](http://msdn.microsoft.com/library/85ad1993-4d75-4806-9097-b934865a899a.aspx)
