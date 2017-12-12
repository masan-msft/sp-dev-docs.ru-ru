---
title: "Настройка страниц сайта «современный»"
description: "Использовать настраиваемый фирменный стиль в SharePoint Online, добавления «современный» страницы программными средствами и добавление, удаление или обновление со стороны клиента веб-частей на страницах «современный»."
ms.date: 11/09/2017
ms.openlocfilehash: b22eabf437eab007a1f58a3ebfcb9c8b830805f8
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="customizing-modern-site-pages"></a><span data-ttu-id="848a3-103">Настройка страниц сайта «современный»</span><span class="sxs-lookup"><span data-stu-id="848a3-103">Customizing "modern" site pages</span></span>

<span data-ttu-id="848a3-104">В 2016 взаимодействия «современный» страница была выпущена с SharePoint team.</span><span class="sxs-lookup"><span data-stu-id="848a3-104">In 2016, the "modern" page experience was released by the SharePoint team.</span></span> <span data-ttu-id="848a3-105">Страницы сайта современных рабочих групп быстро и легко автора и поддерживает расширенный мультимедийного содержимого.</span><span class="sxs-lookup"><span data-stu-id="848a3-105">Modern team site pages are fast, easy to author, and support rich multimedia content.</span></span> <span data-ttu-id="848a3-106">Кроме того, документы будут отображаться на любом устройстве, в браузере или из мобильного приложения SharePoint.</span><span class="sxs-lookup"><span data-stu-id="848a3-106">Additionally, pages look great on any device, in a browser, or from within the SharePoint mobile app.</span></span> 

<span data-ttu-id="848a3-107">Страницы SharePoint созданных с помощью веб-части, которые можно настроить в соответствии со своими потребностями.</span><span class="sxs-lookup"><span data-stu-id="848a3-107">SharePoint pages are built with web parts, which you can customize according to your needs.</span></span> <span data-ttu-id="848a3-108">Можно добавить документы, видео, изображений, действия сайта, веб-каналы Yammer и другие.</span><span class="sxs-lookup"><span data-stu-id="848a3-108">You can add documents, videos, images, site activities, Yammer feeds, and more.</span></span> <span data-ttu-id="848a3-109">Выберите + входа и выберите веб-часть из панели элементов, чтобы добавить содержимое на страницу.</span><span class="sxs-lookup"><span data-stu-id="848a3-109">Just select the + sign and pick a web part from the toolbox to add content to your page.</span></span> <span data-ttu-id="848a3-110">Новый «выделена содержимого» веб-часть позволяет установить критерии, чтобы определенного содержимого динамически и автоматически заполняет в этой области страницы.</span><span class="sxs-lookup"><span data-stu-id="848a3-110">The new “highlighted content” web part lets you set criteria so that specific content automatically and dynamically populates in that area of the page.</span></span> <span data-ttu-id="848a3-111">С помощью платформы SharePoint, разработчики могут создавать настраиваемые веб-части, отображаются справа на панели элементов.</span><span class="sxs-lookup"><span data-stu-id="848a3-111">By using the SharePoint Framework, developers can build custom web parts that show up right in the toolbox.</span></span>

![](https://blogs.office.com/wp-content/uploads/2016/08/New-capabilities-in-SharePoint-Online-team-sites-including-integration-with-Office-365-Groups-1.gif)

<span data-ttu-id="848a3-112">В этой статье основное внимание уделяется вариантов расширения в рамках взаимодействия пользователя со страницы «современный».</span><span class="sxs-lookup"><span data-stu-id="848a3-112">This article focuses on the extensibility options within the "modern" page experience.</span></span> <span data-ttu-id="848a3-113">Если вы хотите узнать больше о функциональных возможностей, предоставляемых «современный» каждый раз, просмотрите [новые возможности в SharePoint Online веб-сайтов групп включая интеграцию с Office 365 группами](https://blogs.office.com/2016/08/31/new-capabilities-in-sharepoint-online-team-sites-including-integration-with-office-365-groups).</span><span class="sxs-lookup"><span data-stu-id="848a3-113">However, if you want to learn more about the functionalities offered by the "modern" experiences, see [New capabilities in SharePoint Online team sites including integration with Office 365 Groups](https://blogs.office.com/2016/08/31/new-capabilities-in-sharepoint-online-team-sites-including-integration-with-office-365-groups).</span></span>

<span data-ttu-id="848a3-114">В оставшейся части этой статьи мы будем использовать «современный» для нового пользовательского интерфейса и «классический» для прежних версий пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="848a3-114">In the remainder of this article, we'll use "modern" for the new user experience and "classic" for the legacy user experience.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="848a3-115">Мы в случае неподдерживаемые взаимодействия «классический»; будет сосуществовать «классический» и «современный».</span><span class="sxs-lookup"><span data-stu-id="848a3-115">We're not deprecating the "classic" experience; both "classic" and "modern" will coexist.</span></span>

## <a name="supported-customizations-for-modern-pages"></a><span data-ttu-id="848a3-116">Поддерживаемые настроек для страниц «современный»</span><span class="sxs-lookup"><span data-stu-id="848a3-116">Supported customizations for "modern" pages</span></span>

<span data-ttu-id="848a3-117">Число настройки, доступные для страниц «современный» отслеживает передовых и в этой статье, мы предлагаем сведения и примеры поддерживаемые параметры.</span><span class="sxs-lookup"><span data-stu-id="848a3-117">The number of customizations available for "modern" pages keeps on growing, and in this article, we'll provide details and examples of the supported options.</span></span> <span data-ttu-id="848a3-118">Группы разработчиков SharePoint работает на другие варианты технической поддержки в будущем.</span><span class="sxs-lookup"><span data-stu-id="848a3-118">The SharePoint team is working to support more options in the future.</span></span> <span data-ttu-id="848a3-119">В следующем списке приведено краткий обзор поддерживаемые возможности для «современный» страниц:</span><span class="sxs-lookup"><span data-stu-id="848a3-119">The following list gives a quick overview of the supported capabilities for "modern" pages:</span></span>

 - <span data-ttu-id="848a3-120">Настраиваемый фирменный стиль</span><span class="sxs-lookup"><span data-stu-id="848a3-120">Custom branding</span></span>
 - <span data-ttu-id="848a3-121">Добавление «современный» страницы программными средствами</span><span class="sxs-lookup"><span data-stu-id="848a3-121">Adding "modern" pages programmatically</span></span>
 - <span data-ttu-id="848a3-122">Добавление, удаление и обновление со стороны клиента веб-частей на страницах «современный»</span><span class="sxs-lookup"><span data-stu-id="848a3-122">Adding, deleting, and updating client-side web parts on "modern" pages</span></span>
 - <span data-ttu-id="848a3-123">Альтернативные макеты (Примечание на *Виртуальный Summit SharePoint*)</span><span class="sxs-lookup"><span data-stu-id="848a3-123">Alternative layouts (see note on *SharePoint Virtual Summit*)</span></span>

<span data-ttu-id="848a3-124">Эти настройки в настоящее время не поддерживается для «современный» страниц:</span><span class="sxs-lookup"><span data-stu-id="848a3-124">These customizations are currently not supported for "modern" pages:</span></span>

 - <span data-ttu-id="848a3-125">Добавление «классический» веб-частей на страницах «современный»</span><span class="sxs-lookup"><span data-stu-id="848a3-125">Adding "classic" web parts on "modern" pages</span></span>
 - <span data-ttu-id="848a3-126">Настраиваемые CSS с помощью свойства web AlternateCSSUrl</span><span class="sxs-lookup"><span data-stu-id="848a3-126">Custom CSS via AlternateCSSUrl web property</span></span>
 - <span data-ttu-id="848a3-127">Настраиваемый JavaScript, внедренные с помощью пользовательских дополнительных действий (Примечание на *Расширения Framework SharePoint*)</span><span class="sxs-lookup"><span data-stu-id="848a3-127">Custom JavaScript embedded via user custom actions (see note on *SharePoint Framework Extensions*)</span></span>
 - <span data-ttu-id="848a3-128">Настраиваемые главные страницы (расширенный фирменной символики будет поддерживаться более поздней версии с помощью альтернативных параметров)</span><span class="sxs-lookup"><span data-stu-id="848a3-128">Custom master pages (more extensive branding will be supported later using alternative options)</span></span>
 - <span data-ttu-id="848a3-129">Стратегия минимальной загрузки (MDS)</span><span class="sxs-lookup"><span data-stu-id="848a3-129">Minimal Download Strategy (MDS)</span></span>

> [!NOTE]
> - <span data-ttu-id="848a3-130">Не рекомендуется совместное использование функции «современный» страница с «классический» порталов публикации SharePoint.</span><span class="sxs-lookup"><span data-stu-id="848a3-130">We don't recommend combining "modern" page functionality with "classic" SharePoint publishing portals.</span></span> <span data-ttu-id="848a3-131">По умолчанию функциональные возможности «современный» страница не включена «классический» публикации порталов SharePoint.</span><span class="sxs-lookup"><span data-stu-id="848a3-131">By default, the "modern" page functionality is not enabled on "classic" SharePoint publishing portals.</span></span>
> - <span data-ttu-id="848a3-132">В 2017 июня [расширения Framework SharePoint занялся preview для разработчиков](https://dev.office.com/blogs/announcing-availability-of-sharepoint-framework-extensions-developer-preview).</span><span class="sxs-lookup"><span data-stu-id="848a3-132">In June 2017, [SharePoint Framework Extensions went into developer preview](https://dev.office.com/blogs/announcing-availability-of-sharepoint-framework-extensions-developer-preview).</span></span> <span data-ttu-id="848a3-133">Использование этих расширений Framework SharePoint, можно управлять визуализации поля с помощью пользовательского кода и создание пользователя настраиваемых действий, выполняемых пользовательского кода.</span><span class="sxs-lookup"><span data-stu-id="848a3-133">Using these SharePoint Framework Extensions, you can control the rendering of a field via custom code, and you can create user custom actions that execute your custom code.</span></span> <span data-ttu-id="848a3-134">Для получения дополнительных сведений см [Overview of Framework расширения SharePoint](http://aka.ms/spfx-extensions).</span><span class="sxs-lookup"><span data-stu-id="848a3-134">To learn more, see [Overview of SharePoint Framework Extensions](http://aka.ms/spfx-extensions).</span></span> 
> - <span data-ttu-id="848a3-135">В 2017 мая, во время Summit виртуального SharePoint мы объявили об изменении [сайты обмена данными с макетами настраиваемая страница](https://blogs.office.com/2017/05/16/new-sharepoint-and-onedrive-capabilities-accelerate-your-digital-transformation/).</span><span class="sxs-lookup"><span data-stu-id="848a3-135">In May 2017, during the SharePoint Virtual Summit, we announced [communication sites with configurable page layouts](https://blogs.office.com/2017/05/16/new-sharepoint-and-onedrive-capabilities-accelerate-your-digital-transformation/).</span></span>  

<span data-ttu-id="848a3-136"><a name="themingimpact"> </a></span><span class="sxs-lookup"><span data-stu-id="848a3-136"></span></span>
## <a name="custom-branding"></a><span data-ttu-id="848a3-137">Настраиваемый фирменный стиль</span><span class="sxs-lookup"><span data-stu-id="848a3-137">Custom branding</span></span>

<span data-ttu-id="848a3-138">Если использовать пользовательскую тему веб-узла, эта тема учитывается сайтами «современный» страницы, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="848a3-138">If your site happens to use a custom theme, this theme is respected in the "modern" page experience as shown in the following sample.</span></span>

<span data-ttu-id="848a3-139">*На рисунке 1. Современный страница с настраиваемой фирменной настройки поступающих от параметры темы*</span><span class="sxs-lookup"><span data-stu-id="848a3-139">*Figure 1. Modern page with custom branding coming from theme settings*</span></span>

<img src="media/modern-experiences/modern-page-with-custom-theme.png" alt="Modern page with custom branding coming from theme settings" width="600">

<span data-ttu-id="848a3-140"><a name="sitesversusmodernpages"> </a></span><span class="sxs-lookup"><span data-stu-id="848a3-140"></span></span>
## <a name="why-a-site-may-not-have-modern-pages-functionality"></a><span data-ttu-id="848a3-141">Почему сайта не предусмотрено функциональные возможности «современный» страниц</span><span class="sxs-lookup"><span data-stu-id="848a3-141">Why a site may not have "modern" pages functionality</span></span>

<span data-ttu-id="848a3-142">«Современный» страницы будут доставляться с помощью компонента уровня веб-страниц сайта (B6917CB1-93A0-4B97-A84D-7CF49975D4EC), поэтому при активации этого компонента веб-узла есть параметр, чтобы использовать «современный» страницы.</span><span class="sxs-lookup"><span data-stu-id="848a3-142">The "modern" pages are delivered by using the Site Pages web scoped feature (B6917CB1-93A0-4B97-A84D-7CF49975D4EC), so when this feature is activated, your site has the option to use "modern" pages.</span></span> <span data-ttu-id="848a3-143">Когда Microsoft для развертывания этой функции, мы включено это для всех сайтов «современный» team (ГРУППА #0 сайтов), а также для большинства «классический» веб-сайтов групп (STS #0).</span><span class="sxs-lookup"><span data-stu-id="848a3-143">When Microsoft rolled out this feature, we enabled this for all "modern" team sites (GROUP#0 sites) and for most "classic" team sites (STS#0).</span></span> 

<span data-ttu-id="848a3-144">Если сайт группы «классический» наибольшее количество веб-частей или вики-страницы, компонент не был включен автоматически и то же самое применяется к веб-сайтов «классический» групп с помощью функции публикации включен.</span><span class="sxs-lookup"><span data-stu-id="848a3-144">If a "classic" team site had a high count of web parts or wiki pages, the feature was not automatically enabled, and the same applies to "classic" team sites with the publishing feature enabled.</span></span> <span data-ttu-id="848a3-145">Если необходимо, чтобы функциональность «современный» страницы на этих сайтах, по-прежнему можно включить функцию страниц сайта.</span><span class="sxs-lookup"><span data-stu-id="848a3-145">If you want "modern" page functionality on these sites, you can still activate the Site Pages feature.</span></span> <span data-ttu-id="848a3-146">Это также означает, что на основании других шаблонах узлов нет доступных функциональных возможностей «современный» страниц.</span><span class="sxs-lookup"><span data-stu-id="848a3-146">This also implies that sites based on other templates do not have the "modern" pages functionality enabled.</span></span> 

<span data-ttu-id="848a3-147">Выше говорили о как компонента «современный» страница была включена на существующих сайтах.</span><span class="sxs-lookup"><span data-stu-id="848a3-147">The previous paragraph talked about how the "modern" page feature was enabled on existing sites.</span></span> <span data-ttu-id="848a3-148">При создании нового «современный» или «классический» сайт группы (ГРУППА #0 или STS #0), «современный» страниц сайта она включена во время подготовки.</span><span class="sxs-lookup"><span data-stu-id="848a3-148">When you create a new "modern" or "classic" team site (GROUP#0 or STS#0), the "modern" Site Pages feature is enabled at provisioning time.</span></span> <span data-ttu-id="848a3-149">На веб-сайтах, основанных на другие шаблоны не включается «современный» компонент страницы сайта.</span><span class="sxs-lookup"><span data-stu-id="848a3-149">The "modern" Site Pages feature is not enabled on sites that are based on other templates.</span></span>

<span data-ttu-id="848a3-150"><a name="configuremodernpages"> </a></span><span class="sxs-lookup"><span data-stu-id="848a3-150"></span></span>
## <a name="configuring-the-end-user-experience"></a><span data-ttu-id="848a3-151">Настройка конечных пользователей</span><span class="sxs-lookup"><span data-stu-id="848a3-151">Configuring the end user experience</span></span>

<span data-ttu-id="848a3-152">Имеется несколько возможностей для управления ли использовать взаимодействия пользователя со страницы «современный» или «классический».</span><span class="sxs-lookup"><span data-stu-id="848a3-152">You have multiple options to control whether the "modern" or "classic" page experience is used.</span></span> 

### <a name="tenant-level-configuration"></a><span data-ttu-id="848a3-153">Конфигурирование на уровне клиента</span><span class="sxs-lookup"><span data-stu-id="848a3-153">Tenant level configuration</span></span>

<span data-ttu-id="848a3-154">Если необходимо полностью отключить «современный» качества, рекомендуется использовать параметр базы данных для клиента.</span><span class="sxs-lookup"><span data-stu-id="848a3-154">If you want to completely disable the "modern" experience, it's best to use the tenant setting for this.</span></span> <span data-ttu-id="848a3-155">Перейдите в центр администрирования клиента (например, contoso-admin.sharepoint.com), перейдите в раздел Параметры и выберите «классический» качества.</span><span class="sxs-lookup"><span data-stu-id="848a3-155">Go to your tenant admin center (for example, contoso-admin.sharepoint.com), go to Settings, and select the "classic" experience.</span></span>

<span data-ttu-id="848a3-156">*На рисунке 2. Раздел страницы сайта в SharePoint для клиентов, областью действия параметров в пользовательский Интерфейс администрирования*</span><span class="sxs-lookup"><span data-stu-id="848a3-156">*Figure 2. Site Pages section in the SharePoint tenant scoped settings in Admin UI*</span></span>

![Раздел страницы сайта в SharePoint для клиентов, областью действия параметров в пользовательский Интерфейс администрирования](media/modern-experiences/site-pages-setting-admin-ui.png)

> [!NOTE]
> - <span data-ttu-id="848a3-158">Установка уровня клиента может быть несколько некоторая путаница; **Запретить пользователям Создание страниц сайта** фактически возвращает «классический» качества.</span><span class="sxs-lookup"><span data-stu-id="848a3-158">The tenant level setting can be a little confusing; **Prevent users from creating Site Pages** actually brings back the "classic" experience.</span></span>
> - <span data-ttu-id="848a3-159">Кэширования текущей конфигурации и приемку сеанса сразу же показано влияние это изменение.</span><span class="sxs-lookup"><span data-stu-id="848a3-159">The current configuration is cached, and signing off the session immediately shows the effect of this change.</span></span>

### <a name="web-level-configuration"></a><span data-ttu-id="848a3-160">Уровень веб-конфигурации</span><span class="sxs-lookup"><span data-stu-id="848a3-160">Web level configuration</span></span>

<span data-ttu-id="848a3-161">Вы можете запретить веб-сайт с помощью взаимодействия пользователя со страницы «современный», отключив функцию уровня веб-сайта с Идентификатором **B6917CB1-93A0-4B97-A84D-7CF49975D4EC** (имя = «Страницы сайта»).</span><span class="sxs-lookup"><span data-stu-id="848a3-161">You can prevent a web from using the "modern" page experience by disabling the web scoped feature with ID **B6917CB1-93A0-4B97-A84D-7CF49975D4EC** (name = "Site Pages").</span></span> <span data-ttu-id="848a3-162">Чтобы повторно включить взаимодействия пользователя со страницы «современный» на уровне веб-, необходимо снова включить функцию.</span><span class="sxs-lookup"><span data-stu-id="848a3-162">To re-enable the "modern" page experience at the web level, you need to activate the feature again.</span></span>

<span data-ttu-id="848a3-163">Чтобы включить или отключить необходимых компонентов с помощью следующих [PnP PowerShell](http://aka.ms/sppnp-powershell) :</span><span class="sxs-lookup"><span data-stu-id="848a3-163">Use the following [PnP PowerShell](http://aka.ms/sppnp-powershell) to enable/disable the needed features:</span></span>

```PowerShell
# Connect to a site
$cred = Get-Credential
Connect-PnPOnline -Url https://[tenant].sharepoint.com/sites/siteurl -Credentials $cred

# Prevent site pages at web level
Disable-PnPFeature -Identity B6917CB1-93A0-4B97-A84D-7CF49975D4EC -Scope Web 
# And again enable site pages at web
#Enable-PnPFeature -Identity B6917CB1-93A0-4B97-A84D-7CF49975D4EC -Scope Web 
```

> [!NOTE]
> <span data-ttu-id="848a3-164">При отключении компонента, больше не создаются новые страницы «современный», но уже созданную страниц всегда оставаться на работу с помощью «современный» пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="848a3-164">When you disable the feature, you can no longer create new "modern" pages, but the already created pages stay working using the "modern" user experience.</span></span> 

### <a name="commenting-configuration"></a><span data-ttu-id="848a3-165">Комментирования конфигурации</span><span class="sxs-lookup"><span data-stu-id="848a3-165">Commenting configuration</span></span>

<span data-ttu-id="848a3-166">По умолчанию пользователи могут добавлять комментарии (июля 2017) на страницах «современный».</span><span class="sxs-lookup"><span data-stu-id="848a3-166">By default, users can add comments (July 2017) on "modern" pages.</span></span> <span data-ttu-id="848a3-167">Если ваша организация не требуется эта функция, она может быть отключена от клиента центра администрирования на странице "Параметры".</span><span class="sxs-lookup"><span data-stu-id="848a3-167">If your organization does not want this feature, it can be disabled from the tenant Admin center on the Settings page.</span></span>

<span data-ttu-id="848a3-168">*На рисунке 3. Включение или отключение комментариев*</span><span class="sxs-lookup"><span data-stu-id="848a3-168">*Figure 3. Enable or disable comments*</span></span>

![Включение или отключение комментариев](http://i.imgur.com/atl91Vh.png)

> [!NOTE]
> <span data-ttu-id="848a3-170">Можно также программными средствами управлять комментирования поведение с помощью сайта и клиентов интерфейсы API (требуется SharePoint со стороны клиента объектной модели (CSOM) версии 16.1.6621.1200 или более поздней версии):</span><span class="sxs-lookup"><span data-stu-id="848a3-170">You can also programmatically manage the commenting behavior by using site and tenant level APIs (requires SharePoint Client-Side Object Model (CSOM) version 16.1.6621.1200 or later):</span></span>
> - <span data-ttu-id="848a3-171">Microsoft.Online.SharePoint.TenantAdministration.SiteProperties.CommentsOnSitePagesDisabled</span><span class="sxs-lookup"><span data-stu-id="848a3-171">Microsoft.Online.SharePoint.TenantAdministration.SiteProperties.CommentsOnSitePagesDisabled</span></span> 
> - <span data-ttu-id="848a3-172">Microsoft.SharePoint.Client.Site.CommentsOnSitePagesDisabled</span><span class="sxs-lookup"><span data-stu-id="848a3-172">Microsoft.SharePoint.Client.Site.CommentsOnSitePagesDisabled</span></span>


## <a name="programming-modern-pages"></a><span data-ttu-id="848a3-173">Программирование «современный» страниц</span><span class="sxs-lookup"><span data-stu-id="848a3-173">Programming "modern" pages</span></span>

### <a name="adding-modern-pages"></a><span data-ttu-id="848a3-174">Добавление страниц «современный»</span><span class="sxs-lookup"><span data-stu-id="848a3-174">Adding "modern" pages</span></span>
<span data-ttu-id="848a3-175">Создание страницы «современный» сводится к Создание элемента списка в библиотеке страниц сайта и ее назначения правильный тип контента в сочетании с параметру некоторые дополнительные свойства, как показано в следующем фрагменте кода:</span><span class="sxs-lookup"><span data-stu-id="848a3-175">Creating a "modern" page comes down to creating a list item in the site pages library and assigning it the correct content type combined with setting some additional properties as shown in the following code snippet:</span></span>

```C#
// pagesLibrary is List object for the "site pages" library of the site
ListItem item = pagesLibrary.RootFolder.Files.AddTemplateFile(serverRelativePageName, TemplateFileType.ClientSidePage).ListItemAllFields;

// Make this page a "modern" page
item["ContentTypeId"] = "0x0101009D1CB255DA76424F860D91F20E6C4118";
item["Title"] = System.IO.Path.GetFileNameWithoutExtension("mypage.aspx");
item["ClientSideApplicationId"] = "b6917cb1-93a0-4b97-a84d-7cf49975d4ec";
item["PageLayoutType"] = "Article";
item["PromotedState"] = "0";
item["CanvasContent1"] = "<div></div>";
item["BannerImageUrl"] = "/_layouts/15/images/sitepagethumbnail.png";
item.Update();
clientContext.Load(item);
clientContext.ExecuteQuery();

```

<br/>

<span data-ttu-id="848a3-176">При использовании PnP (по состоянию на выпуск 2017 марта), вы можете использовать возможности наших методы расширения, которое позволяет модели для добавления на страницу легко:</span><span class="sxs-lookup"><span data-stu-id="848a3-176">When using PnP (as of the March 2017 release), you can leverage our extension methods, which gives you a model for adding a page easily:</span></span>

```C#
cc.Web.AddClientSidePage("mypage.aspx", true);
```

> [!IMPORTANT]
> <span data-ttu-id="848a3-177">По состоянию на сентябрь 2017, страниц, созданных с помощью `AddTemplateFile` метод имеет предварительного просмотра при наведении на странице результатов поиска.</span><span class="sxs-lookup"><span data-stu-id="848a3-177">As of September 2017, pages created using the `AddTemplateFile` method do not have a preview when you hover over them from the search results page.</span></span> <span data-ttu-id="848a3-178">Корпорация Майкрософт работает на исправление/alternative решения базы данных для.</span><span class="sxs-lookup"><span data-stu-id="848a3-178">Microsoft is working on a fix/alternative solution for this.</span></span>

### <a name="using-the-pnp-support-for-modern-pages-and-client-side-web-parts"></a><span data-ttu-id="848a3-179">С помощью PnP поддержки для клиентских веб-частей и страниц «современный»</span><span class="sxs-lookup"><span data-stu-id="848a3-179">Using the PnP support for "modern" pages and client-side web parts</span></span>

<span data-ttu-id="848a3-180">По состоянию на выпуска 2017 марта [PnP сайты core библиотека](http://aka.ms/sppnp) поддерживает создание, обновление и удаление страницы со стороны клиента.</span><span class="sxs-lookup"><span data-stu-id="848a3-180">As of the March 2017 release, the [PnP Sites core library](http://aka.ms/sppnp) offers support for creating, updating, and deleting client-side pages.</span></span> <span data-ttu-id="848a3-181">В этом разделе представлены сведения о работе со страницы со стороны клиента с помощью [PnP сайты core библиотеки на репозиториев](https://github.com/SharePoint/PnP-Sites-Core).</span><span class="sxs-lookup"><span data-stu-id="848a3-181">This section gives you information about how to work with client-side pages using the [PnP Sites core library on GitHub](https://github.com/SharePoint/PnP-Sites-Core).</span></span>

#### <a name="create-a-new-page-and-add-a-text-web-part"></a><span data-ttu-id="848a3-182">Создайте новую страницу и добавьте веб-часть текста</span><span class="sxs-lookup"><span data-stu-id="848a3-182">Create a new page and add a text web part</span></span>

<span data-ttu-id="848a3-183">В этом примере мы создайте новую страницу со стороны клиента в памяти, добавление элемента управления редактора форматированного текста и наконец сохранить страницу в библиотеке страниц сайта с mypage.aspx.</span><span class="sxs-lookup"><span data-stu-id="848a3-183">In this sample, we create a new client-side page in memory, add a rich text editor control, and finally save the page to the site pages library as mypage.aspx.</span></span> <span data-ttu-id="848a3-184">Первым шагом является создание экземпляра ClientSidePage, а затем мы создать элемент управления, который мы добавьте на страницу с помощью `AddControl` метод.</span><span class="sxs-lookup"><span data-stu-id="848a3-184">The first step is creating a ClientSidePage instance, and then we instantiate a control that we add on the page by using the `AddControl` method.</span></span> <span data-ttu-id="848a3-185">После этого страница сохраняется.</span><span class="sxs-lookup"><span data-stu-id="848a3-185">After that's done, the page is saved.</span></span>

```C#
// cc is the ClientContext instance for the site you're working with
ClientSidePage myPage = new ClientSidePage(cc);

ClientSideText txt1 = new ClientSideText() { Text = "PnP Rocks" };
myPage.AddControl(txt1, 0);
myPage.Save("mypage.aspx");
```

#### <a name="load-an-existing-page"></a><span data-ttu-id="848a3-186">Загрузить существующей страницы</span><span class="sxs-lookup"><span data-stu-id="848a3-186">Load an existing page</span></span> 

<span data-ttu-id="848a3-187">Изменение или копирование существующей страницы, необходимо этой странице можно загрузить в PnP клиентской объектной модели; Загрузка «преобразований» HTML-контент в объектную модель, которую можно изменять.</span><span class="sxs-lookup"><span data-stu-id="848a3-187">When you want to modify or copy an existing page, you can load that page into the PnP client-side object model; the loading "transforms" the HTML content into an object model that you can manipulate.</span></span> <span data-ttu-id="848a3-188">Загрузка существующей страницы выполняется с помощью `Load` метод.</span><span class="sxs-lookup"><span data-stu-id="848a3-188">Loading an existing page is done by using the `Load` method.</span></span>

```C#
// load the page with name "page3.aspx"
ClientSidePage p = ClientSidePage.Load(cc, "page3.aspx");

// perform your page updates
...

// save the page back to SharePoint
p.Save()
```

#### <a name="add-a-section"></a><span data-ttu-id="848a3-189">Добавление раздела</span><span class="sxs-lookup"><span data-stu-id="848a3-189">Add a section</span></span>

<span data-ttu-id="848a3-190">Страницы могут иметь гибкий макет; можно добавить один или несколько разделов на странице, и эти разделы могут иметь до трех столбцов.</span><span class="sxs-lookup"><span data-stu-id="848a3-190">Pages can have a flexible layout; you can add one or more sections on a page, and these sections can have up to three columns.</span></span> <span data-ttu-id="848a3-191">Разделы можно добавить на страницы с помощью пользовательского интерфейса SharePoint или это можно сделать программным способом.</span><span class="sxs-lookup"><span data-stu-id="848a3-191">You can add sections to your pages by using the SharePoint user interface, or you can do this programmatically.</span></span>

```C#
var page2 = cc.Web.AddClientSidePage("PageWithSections.aspx", true);
page2.AddSection(CanvasSectionTemplate.ThreeColumn, 5);
page2.AddSection(CanvasSectionTemplate.TwoColumn, 10);
```

#### <a name="add-an-out-of-the-box-web-part"></a><span data-ttu-id="848a3-192">Добавление ожидания введите веб-части</span><span class="sxs-lookup"><span data-stu-id="848a3-192">Add an out-of-the-box web part</span></span> 
<span data-ttu-id="848a3-193">В следующем примере показано, как добавить клиентские веб-части вне поля **изображения** на странице.</span><span class="sxs-lookup"><span data-stu-id="848a3-193">The following sample shows how you can add an out-of-the-box **image** client-side web part on a page.</span></span> <span data-ttu-id="848a3-194">Обратите внимание, что мы экземпляра веб-части объект с помощью `InstantiateDefaultWebPart` вызова метода.</span><span class="sxs-lookup"><span data-stu-id="848a3-194">Note that we instantiate the web part object by using the `InstantiateDefaultWebPart` method call.</span></span> <span data-ttu-id="848a3-195">После начала веб-части ее задано значение свойства по умолчанию, определенных в манифесте части web.</span><span class="sxs-lookup"><span data-stu-id="848a3-195">After the web part is initiated, its properties are set to the default properties defined in the web part manifest.</span></span> <span data-ttu-id="848a3-196">Для большинства веб-частей вам потребуется обновить свойства, как показано в этом примере.</span><span class="sxs-lookup"><span data-stu-id="848a3-196">For most web parts, you need to update the properties as shown in this sample.</span></span>

```C#
ClientSidePage page5 = new ClientSidePage(cc);
var imageWebPart = page5.InstantiateDefaultWebPart(DefaultClientSideWebParts.Image);
imageWebPart.Properties["imageSourceType"] = 2;
imageWebPart.Properties["siteId"] = "c827cb03-d059-4956-83d0-cd60e02e3b41";
imageWebPart.Properties["webId"] = "9fafd7c0-e8c3-4a3c-9e87-4232c481ca26";
imageWebPart.Properties["listId"] = "78d1b1ac-7590-49e7-b812-55f37c018c4b";
imageWebPart.Properties["uniqueId"] = "3C27A419-66D0-4C36-BF24-BD6147719052";
imageWebPart.Properties["imgWidth"] = 1002;
imageWebPart.Properties["imgHeight"] = 469;
page5.AddControl(imageWebPart);
page5.Save("page5.aspx");

```

#### <a name="add-a-custom-client-side-web-part"></a><span data-ttu-id="848a3-197">Добавление настраиваемых со стороны клиента веб-части</span><span class="sxs-lookup"><span data-stu-id="848a3-197">Add a custom client-side web part</span></span>

<span data-ttu-id="848a3-198">Предыдущих примерах показано, как работать с ожидания введите веб-частями, но можно также добавить настраиваемые встроенные со стороны клиента веб-частей на страницу.</span><span class="sxs-lookup"><span data-stu-id="848a3-198">Previous samples showed how to work with out-of-the-box web parts, but you can also add your custom built client-side web parts to a page.</span></span> <span data-ttu-id="848a3-199">Сначала необходимо получение часть информации в сети с помощью `AvailableClientSideComponents` метод и выполните поиск веб-часть и сведения, поиск для создания экземпляра `ClientSideWebPart` экземпляра, который добавляется на страницу на предыдущем этапе.</span><span class="sxs-lookup"><span data-stu-id="848a3-199">You would start by getting your web part information by using the `AvailableClientSideComponents` method, and then search for your web part and use the information you find to instantiate a `ClientSideWebPart` instance, which is added to the page in the last step.</span></span>

```C#
ClientSidePage p = new ClientSidePage(cc);

// get a list of possible client side web parts that can be added
var components = p.AvailableClientSideComponents();

// Find our custom "HelloWord" web part
var myWebPart = components.Where(s => s.ComponentType == 1 && s.Name == "HelloWorld").FirstOrDefault();
if (myWebPart != null)
{
    // Instantiate a client side web part from our found web part information
    ClientSideWebPart helloWp = new ClientSideWebPart(myWebPart) { Order = 10 };
    // Add the custom client side web part to the page
    p.AddControl(helloWp);
}

// Persist the page to SharePoint
p.Save("PnPRocks.aspx");
```

#### <a name="adjust-control-order"></a><span data-ttu-id="848a3-200">Измените порядок элементов управления</span><span class="sxs-lookup"><span data-stu-id="848a3-200">Adjust control order</span></span>
<span data-ttu-id="848a3-201">Существуют различные методы для управления порядком, в котором отображаются элементы управления на странице.</span><span class="sxs-lookup"><span data-stu-id="848a3-201">You have different methods to control the order in which the controls appear on the page.</span></span> <span data-ttu-id="848a3-202">— Это ключевой аспект `Order` атрибут на фактический элемент управления: список элементов управления сортироваться по значению, `Order` атрибут при созданный HTML-страницы, и порядок, в HTML-код также порядок во время отображения страницы.</span><span class="sxs-lookup"><span data-stu-id="848a3-202">The key aspect is the `Order` attribute on the actual control: the list of controls is sorted by the value of that `Order` attribute when the page HTML is generated, and the order in the HTML is also the order at page rendering time.</span></span>

```C#
// Set the order when initiating the control
ClientSideText txt1 = new ClientSideText() { Text = "PnP Rocks", Order = 5 };

// Set the order when you add the control to the page, in this case we want the control to be the first
myPage.AddControl(txt1, -1);

// Manipulate the control order on the page...e.g. move a control to the back
myPage.Controls[1].Order = 10;

```

#### <a name="delete-a-control"></a><span data-ttu-id="848a3-203">Удаление элемента управления</span><span class="sxs-lookup"><span data-stu-id="848a3-203">Delete a control</span></span>

<span data-ttu-id="848a3-204">Если вы хотите удалить элемент управления со страницы, просто можно вызвать `Delete` метод в элементе управления и сохранить страницу назад.</span><span class="sxs-lookup"><span data-stu-id="848a3-204">If you want to delete a control from a page, you can simply call the `Delete` method on the control and save the page back.</span></span>

```C#
ClientSidePage deleteDemoPage = ClientSidePage.Load(cc, "page3.aspx");
deleteDemoPage.Controls[0].Delete();
deleteDemoPage.Save();
```

#### <a name="delete-a-page"></a><span data-ttu-id="848a3-205">Удаление страницы</span><span class="sxs-lookup"><span data-stu-id="848a3-205">Delete a page</span></span> 

<span data-ttu-id="848a3-206">И, наконец можно удалить страницу со стороны клиента.</span><span class="sxs-lookup"><span data-stu-id="848a3-206">Finally, you can delete a client-side page.</span></span>

```C#
ClientSidePage p = ClientSidePage.Load(cc, "deleteme.aspx");
p.Delete();
```

#### <a name="class-model"></a><span data-ttu-id="848a3-207">Класс модели</span><span class="sxs-lookup"><span data-stu-id="848a3-207">Class model</span></span>

<span data-ttu-id="848a3-208">На следующем рисунке показаны наиболее важные классы, которые вы будете работать с при использовании объектной модели PnP страницы со стороны клиента.</span><span class="sxs-lookup"><span data-stu-id="848a3-208">The following figure shows the most important classes you'll be working with when using the PnP client-side page object model.</span></span>

<span data-ttu-id="848a3-209">*На рисунке 4. PnP клиентской объектной модели*</span><span class="sxs-lookup"><span data-stu-id="848a3-209">*Figure 4. PnP client-side object model*</span></span>

![PnP клиентской объектной модели](media/pnpclientsideobjectmodel.png)

## <a name="additional-considerations"></a><span data-ttu-id="848a3-211">Дополнительные сведения о выполнении</span><span class="sxs-lookup"><span data-stu-id="848a3-211">Additional considerations</span></span>

<span data-ttu-id="848a3-212">Постепенно описываются дополнительные параметры настройки для взаимодействия пользователя со страницы «современный».</span><span class="sxs-lookup"><span data-stu-id="848a3-212">We'll gradually introduce more customization options for the "modern" pages experience.</span></span> <span data-ttu-id="848a3-213">Эти параметры способ выравнивания в выпуске дополнительные возможности среды SharePoint.</span><span class="sxs-lookup"><span data-stu-id="848a3-213">These options will be aligned with the release of additional SharePoint Framework capabilities.</span></span> <span data-ttu-id="848a3-214">На данный момент нет расписание не точное, но при выпуске новых возможностей взаимодействия «современный» статьи будут обновляться.</span><span class="sxs-lookup"><span data-stu-id="848a3-214">Currently, there is no exact schedule available, but we'll update the "modern" experience articles whenever new capabilities are released.</span></span>

## <a name="see-also"></a><span data-ttu-id="848a3-215">См. также</span><span class="sxs-lookup"><span data-stu-id="848a3-215">See also</span></span>

- [<span data-ttu-id="848a3-216">Настройка "современных" интерфейсов в SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="848a3-216">Customizing the "modern" experiences in SharePoint Online</span></span>](modern-experience-customizations.md)
- [<span data-ttu-id="848a3-217">Разрешить или запретить создание современных веб-страниц конечными пользователями</span><span class="sxs-lookup"><span data-stu-id="848a3-217">Allow or prevent creation of modern site pages by end users</span></span>](https://support.office.com/en-us/article/Allow-or-prevent-creation-of-modern-site-pages-by-end-users-c41d9cc8-c5c0-46b4-8b87-ea66abc6e63b?ui=en-US&rs=en-US&ad=US)
