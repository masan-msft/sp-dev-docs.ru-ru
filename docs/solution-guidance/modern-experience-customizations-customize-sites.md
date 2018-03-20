---
title: "Настройка веб-сайтов «современный» групп"
description: "Применение пользовательской темы на сайте команды «современный» в SharePoint Online."
ms.date: 11/08/2017
ms.openlocfilehash: 7046d8f6424497073a9003711f5652b8e8f5ed22
ms.sourcegitcommit: 895d31071e73aa23e62593c9ffa46b38701ba801
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/19/2018
---
# <a name="customizing-modern-team-sites"></a><span data-ttu-id="f5ceb-103">Настройка веб-сайтов «современный» групп</span><span class="sxs-lookup"><span data-stu-id="f5ceb-103">Customizing "modern" team sites</span></span>

<span data-ttu-id="f5ceb-104">В 2016 группы SharePoint Online выпущен сайты для совместной работы «современный».</span><span class="sxs-lookup"><span data-stu-id="f5ceb-104">In 2016, the SharePoint Online team released "modern" collaboration sites.</span></span> <span data-ttu-id="f5ceb-105">Эти сайты групп «современный» интегрированных с Office 365 групп и перевести была существенно увеличена конечным пользователем.</span><span class="sxs-lookup"><span data-stu-id="f5ceb-105">These "modern" team sites are integrated with Office 365 groups and bring a greatly improved end user experience.</span></span> <span data-ttu-id="f5ceb-106">Сайты рабочих групп «Современный» реагирует предусмотрено при проектировании и значительно быстрее создавать и использовать с точки зрения конечного пользователя.</span><span class="sxs-lookup"><span data-stu-id="f5ceb-106">"Modern" team sites are responsive by design and are much faster to create and use from an end user perspective.</span></span> <span data-ttu-id="f5ceb-107">Ниже перечислены некоторые из основных преимуществ веб-сайтов «современный» групп:</span><span class="sxs-lookup"><span data-stu-id="f5ceb-107">Following are some of the key benefits of the "modern" team sites:</span></span>

- <span data-ttu-id="f5ceb-108">Предназначен для масштабирования для любого устройства изначально без настройки для полностью отклика программой.</span><span class="sxs-lookup"><span data-stu-id="f5ceb-108">Designed to scale for any device natively without customizations for a fully responsive experience.</span></span>
- <span data-ttu-id="f5ceb-109">Содержит собственный новости, быстрые ссылки и возможности активности.</span><span class="sxs-lookup"><span data-stu-id="f5ceb-109">Contain native news, quick links, and activity capabilities.</span></span> 
- <span data-ttu-id="f5ceb-110">Интеграция с Office 365 групп.</span><span class="sxs-lookup"><span data-stu-id="f5ceb-110">Integrated with Office 365 groups.</span></span> 
- <span data-ttu-id="f5ceb-111">Значительно более быстрого создания сайтов по сравнению с веб-сайтов «классический» групп.</span><span class="sxs-lookup"><span data-stu-id="f5ceb-111">Significantly faster site creation compared to "classic" team sites.</span></span>
- <span data-ttu-id="f5ceb-112">Включить «современный» списки и библиотеки с поддержкой Microsoft потока и PowerApps.</span><span class="sxs-lookup"><span data-stu-id="f5ceb-112">Include "modern" lists and libraries with support for Microsoft Flow and PowerApps.</span></span>
- <span data-ttu-id="f5ceb-113">Содержит страницы «современный», возможность редактирования.</span><span class="sxs-lookup"><span data-stu-id="f5ceb-113">Contain "modern" page editing capabilities.</span></span>
- <span data-ttu-id="f5ceb-114">Включить на странице содержимое обновленного сайта с помощью дополнительных дополнительная информация об использовании узла.</span><span class="sxs-lookup"><span data-stu-id="f5ceb-114">Include an updated site contents page with additional insights on site usage.</span></span>

<span data-ttu-id="f5ceb-115">В данной статье описываются параметры расширяемости в рамках веб-сайтов «современный» групп:</span><span class="sxs-lookup"><span data-stu-id="f5ceb-115">This article concentrates on the available extensibility options within "modern" team sites:</span></span>

- [<span data-ttu-id="f5ceb-116">Новые возможности в SharePoint Online сайты групп, включая интеграцию с группами Office 365</span><span class="sxs-lookup"><span data-stu-id="f5ceb-116">New capabilities in SharePoint Online team sites including integration with Office 365 Groups</span></span>](https://blogs.office.com/2016/08/31/new-capabilities-in-sharepoint-online-team-sites-including-integration-with-office-365-groups)
- [<span data-ttu-id="f5ceb-117">Создание связи сайтов группы SharePoint Online в секундах</span><span class="sxs-lookup"><span data-stu-id="f5ceb-117">Create connected SharePoint Online team sites in seconds</span></span>](https://blogs.office.com/2016/11/08/create-connected-sharepoint-online-team-sites-in-seconds)
- [<span data-ttu-id="f5ceb-118">Разрешить или запретить сценария</span><span class="sxs-lookup"><span data-stu-id="f5ceb-118">Allow or prevent custom script</span></span>](https://support.office.com/en-us/article/Allow-or-prevent-custom-script-1f2c515f-5d7e-448a-9fd7-835da935584f?ui=en-US&rs=en-US&ad=US)

> [!IMPORTANT]
> <span data-ttu-id="f5ceb-119">Мы в случае неподдерживаемые взаимодействия «классический»; будет сосуществовать «классический» и «современный».</span><span class="sxs-lookup"><span data-stu-id="f5ceb-119">We're not deprecating the "classic" experience; both "classic" and "modern" will coexist.</span></span>

<span data-ttu-id="f5ceb-120"><a name="supportedcustomizations"> </a></span><span class="sxs-lookup"><span data-stu-id="f5ceb-120"></span></span>
## <a name="supported-customizations-on-modern-team-sites"></a><span data-ttu-id="f5ceb-121">Поддерживаемые настроек веб-сайтов «современный» групп</span><span class="sxs-lookup"><span data-stu-id="f5ceb-121">Supported customizations on "modern" team sites</span></span>

<span data-ttu-id="f5ceb-122">«Современный» сайты имеют разные возможности параметров настройки, по сравнению с веб-сайтов «классический» групп.</span><span class="sxs-lookup"><span data-stu-id="f5ceb-122">"Modern" sites have a different level of customization options compared to "classic" team sites.</span></span> <span data-ttu-id="f5ceb-123">Со временем описываются параметры дополнительной настройки, главным образом повышения расширяемость и фирменной символики.</span><span class="sxs-lookup"><span data-stu-id="f5ceb-123">Over time we'll introduce additional customization options, mainly focusing on extensibility and branding.</span></span> <span data-ttu-id="f5ceb-124">В следующем списке приведено краткий обзор поддерживаемые возможности для веб-сайтов «современный» групп.</span><span class="sxs-lookup"><span data-stu-id="f5ceb-124">The following list gives a quick overview of the supported capabilities for "modern" team sites.</span></span> <span data-ttu-id="f5ceb-125">Можно выполнить следующие действия.</span><span class="sxs-lookup"><span data-stu-id="f5ceb-125">You can:</span></span>

- <span data-ttu-id="f5ceb-126">Использование [Среды SharePoint](http://aka.ms/spfx) для изменения пользовательского интерфейса на веб-сайтах путем отправки со стороны клиента веб-частей или включая другие элементы пользовательского интерфейса с расширениями Framework SharePoint.</span><span class="sxs-lookup"><span data-stu-id="f5ceb-126">Use [SharePoint Framework](http://aka.ms/spfx) to modify user experience in the sites by providing client-side web parts or including other user interface elements with SharePoint Framework Extensions.</span></span>
- <span data-ttu-id="f5ceb-127">Применение пользовательской темы или изменение логотипа.</span><span class="sxs-lookup"><span data-stu-id="f5ceb-127">Apply a custom theme or change the logo.</span></span>
- <span data-ttu-id="f5ceb-128">Применить тему ожидания введите.</span><span class="sxs-lookup"><span data-stu-id="f5ceb-128">Apply an out-of-the-box theme.</span></span>
- <span data-ttu-id="f5ceb-129">Создайте настраиваемые столбцы сайта (поля) и типов контента.</span><span class="sxs-lookup"><span data-stu-id="f5ceb-129">Create custom site columns (fields) and content types.</span></span>
- <span data-ttu-id="f5ceb-130">Создание списков и библиотек.</span><span class="sxs-lookup"><span data-stu-id="f5ceb-130">Create lists and libraries.</span></span>
- <span data-ttu-id="f5ceb-131">Настройте параметры сайта, такие как региональные параметры, языков и параметров аудита.</span><span class="sxs-lookup"><span data-stu-id="f5ceb-131">Configure site settings, such as regional settings, languages, and auditing settings.</span></span>

> [!NOTE]
> <span data-ttu-id="f5ceb-132">По умолчанию сайта группы «современный» имеет отключены возможности создания сценариев.</span><span class="sxs-lookup"><span data-stu-id="f5ceb-132">By default, a "modern" team site has scripting capabilities turned off.</span></span> <span data-ttu-id="f5ceb-133">По-прежнему можно применять пользовательскую тему, но нельзя добавлять пользовательской темы в коллекцию тем как вариант для конечных пользователей.</span><span class="sxs-lookup"><span data-stu-id="f5ceb-133">You can still apply a custom theme, but you cannot introduce a custom theme to the theme gallery as an option for end users.</span></span> <span data-ttu-id="f5ceb-134">Если вы хотите добавить тему в коллекцию тем, необходимо [Включить поддержку сценариев](https://support.office.com/en-us/article/Turn-scripting-capabilities-on-or-off-1f2c515f-5d7e-448a-9fd7-835da935584f) на сайте.</span><span class="sxs-lookup"><span data-stu-id="f5ceb-134">If you want to add a theme to the theme gallery, you need to [enable scripting](https://support.office.com/en-us/article/Turn-scripting-capabilities-on-or-off-1f2c515f-5d7e-448a-9fd7-835da935584f) on the site.</span></span>

<span data-ttu-id="f5ceb-135"><a name="notsupported"> </a></span><span class="sxs-lookup"><span data-stu-id="f5ceb-135"></span></span>
### <a name="whats-not-supported-on-modern-team-sites"></a><span data-ttu-id="f5ceb-136">Что не поддерживается для веб-сайтов «современный» групп</span><span class="sxs-lookup"><span data-stu-id="f5ceb-136">What's not supported on "modern" team sites</span></span>

<span data-ttu-id="f5ceb-137">В различных областях веб-сайтов групп «современный» типичные настроек, в настоящее время недоступны.</span><span class="sxs-lookup"><span data-stu-id="f5ceb-137">In numerous areas on the "modern" team sites, the typical customizations are not currently available.</span></span> <span data-ttu-id="f5ceb-138">Дальнейший поддержки будут доступны для некоторых из этих разделов, если они готовы нужно освободить.</span><span class="sxs-lookup"><span data-stu-id="f5ceb-138">Further support will be available for some of these topics when they are ready to be released.</span></span> <span data-ttu-id="f5ceb-139">Ниже приведен список в настоящее время не поддерживается настроек веб-сайтов «современный» групп:</span><span class="sxs-lookup"><span data-stu-id="f5ceb-139">Following is a list of currently unsupported customizations on "modern" team sites:</span></span>

- <span data-ttu-id="f5ceb-140">Настраиваемые главные страницы; Расширенный фирменной символики будет поддерживаться более поздней версии с помощью альтернативные варианты.</span><span class="sxs-lookup"><span data-stu-id="f5ceb-140">Custom master pages; more extensive branding will be supported later using alternative options.</span></span>
- <span data-ttu-id="f5ceb-141">Изменение «современный» сайт «классический» seattle.master или oslo.master.</span><span class="sxs-lookup"><span data-stu-id="f5ceb-141">Changing "modern" site to use "classic" seattle.master or oslo.master.</span></span>
- <span data-ttu-id="f5ceb-142">Пользовательские макеты страниц; Мы стремятся имеют поддержку нескольких полотна в будущем.</span><span class="sxs-lookup"><span data-stu-id="f5ceb-142">Custom page layouts; we are looking to have support for multiple canvases in the future.</span></span>
- <span data-ttu-id="f5ceb-143">Включение сайта или семейства веб-сайтов ограниченные функции публикации; технически в настоящее время можно активировать функции, но это не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="f5ceb-143">Enabling site or site collection scoped publishing features; technically, features can be currently activated, but this is not a supported configuration.</span></span>
- <span data-ttu-id="f5ceb-144">Настраиваемые действия пользователя / пользовательский JavaScript; будет более управляемым способ внедрения JavaScript на страницах через расширения Framework SharePoint (в настоящее время в предварительной версии dev).</span><span class="sxs-lookup"><span data-stu-id="f5ceb-144">User custom actions / custom JavaScript; there will be a more controlled way to embed JavaScript on the pages through the SharePoint Framework Extensions (currently in dev preview).</span></span>
- <span data-ttu-id="f5ceb-145">Дочерние сайты «Современный»; дочерние сайты, созданные на веб-сайтов «современный» групп используйте «классический» качества, но вы можете изменить взаимодействие с пользователем похоже на «современный» сайты.</span><span class="sxs-lookup"><span data-stu-id="f5ceb-145">"Modern" subsites; subsites created on "modern" team sites use the "classic" experience, but you can change the user experience to be similar to "modern" sites.</span></span>
- <span data-ttu-id="f5ceb-146">Возможность управления параметры шаблона доступные дочернего сайта.</span><span class="sxs-lookup"><span data-stu-id="f5ceb-146">Ability to control available subsite template options.</span></span>
- <span data-ttu-id="f5ceb-147">«Классический» публикация компонентов (WCM).</span><span class="sxs-lookup"><span data-stu-id="f5ceb-147">"Classic" publishing features (WCM).</span></span>
- <span data-ttu-id="f5ceb-148">Активация функции сообщества или создание дочерних сайтов сообществ в разделе «современный» группового сайта.</span><span class="sxs-lookup"><span data-stu-id="f5ceb-148">Activation of community feature or creation of community subsites under "modern" team site.</span></span>

<span data-ttu-id="f5ceb-149">Потому, что веб-сайтов «современный» групп также отключены возможности создания сценариев (это так называемое NoScript сайта), не могут настраивать самых разных областях.</span><span class="sxs-lookup"><span data-stu-id="f5ceb-149">Because "modern" team sites also have scripting capabilities disabled (it's a so called NoScript site), numerous areas cannot be customized.</span></span> <span data-ttu-id="f5ceb-150">Влияние NoScript аналогична для сайтов «современный» или «классический».</span><span class="sxs-lookup"><span data-stu-id="f5ceb-150">The impact of NoScript is the same for "modern" or "classic" sites.</span></span> <span data-ttu-id="f5ceb-151">«Современный» сайты имеют NoScript включена по умолчанию, то есть возможность написания сценариев, недоступны.</span><span class="sxs-lookup"><span data-stu-id="f5ceb-151">"Modern" sites have NoScript enabled by default, meaning that scripting capabilities are not available.</span></span> <span data-ttu-id="f5ceb-152">Тем не менее это возможно и поддерживаемые для отключения NoScript параметров «современный» и «классический» сайты в дальнейшем включить некоторые возможности.</span><span class="sxs-lookup"><span data-stu-id="f5ceb-152">However, it is possible and supported to disable NoScript settings in both "modern" and "classic" sites to further enable some capabilities.</span></span> 

<span data-ttu-id="f5ceb-153">При разработке решений, необходимо учитывайте следующие основные области, связанные с NoScript параметр:</span><span class="sxs-lookup"><span data-stu-id="f5ceb-153">When you design your solutions, consider these key areas related to the NoScript setting:</span></span>

- <span data-ttu-id="f5ceb-154">Изолированные решения, не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="f5ceb-154">Sandbox solutions are not supported.</span></span>
- <span data-ttu-id="f5ceb-155">Настраиваемый JavaScript нельзя включить на сайтах с помощью параметров «классический» расширяемость (например, с помощью пользовательских дополнительных действий).</span><span class="sxs-lookup"><span data-stu-id="f5ceb-155">Custom JavaScript cannot be enabled on the sites by using "classic" extensibility options (for example, via user custom actions).</span></span>
- <span data-ttu-id="f5ceb-156">Не удается получить доступ к сайтам с помощью SharePoint Designer.</span><span class="sxs-lookup"><span data-stu-id="f5ceb-156">You cannot access sites using SharePoint Designer.</span></span>
- <span data-ttu-id="f5ceb-157">Некоторые веб-частей, недоступны для конечных пользователей.</span><span class="sxs-lookup"><span data-stu-id="f5ceb-157">Some web parts are not available for end users.</span></span>
- <span data-ttu-id="f5ceb-158">Возможность доступа или обновление записи контейнера свойств сайта.</span><span class="sxs-lookup"><span data-stu-id="f5ceb-158">Ability to access or update site property bag entries.</span></span>

> [!NOTE]
> <span data-ttu-id="f5ceb-159">Можно найти полный список задействованной возможности из статьи технической поддержки Майкрософт [Разрешить или запретить пользовательский сценарий](https://support.office.com/en-us/article/Allow-or-prevent-custom-script-1f2c515f-5d7e-448a-9fd7-835da935584f?ui=en-US&rs=en-US&ad=US) в разделе «Функции влияет на настраиваемых сценарий заблокирован».</span><span class="sxs-lookup"><span data-stu-id="f5ceb-159">You can find the full list of impacted capabilities from the Microsoft Support article [Allow or prevent custom script](https://support.office.com/en-us/article/Allow-or-prevent-custom-script-1f2c515f-5d7e-448a-9fd7-835da935584f?ui=en-US&rs=en-US&ad=US) under the "Features affected when custom script is blocked" section.</span></span>

<span data-ttu-id="f5ceb-160"><a name="pnpprovisioningengine"> </a></span><span class="sxs-lookup"><span data-stu-id="f5ceb-160"></span></span>
### <a name="using-pnp-provisioning-engine-with-modern-team-sites"></a><span data-ttu-id="f5ceb-161">С помощью PnP модуля подготовки с веб-сайтов «современный» групп</span><span class="sxs-lookup"><span data-stu-id="f5ceb-161">Using PnP provisioning engine with "modern" team sites</span></span>

<span data-ttu-id="f5ceb-162">Можно использовать [PnP модуля подготовки](https://msdn.microsoft.com/en-us/pnp_articles/pnp-provisioning-engine-and-the-core-library) с веб-сайтов «современный» групп.</span><span class="sxs-lookup"><span data-stu-id="f5ceb-162">You can use the [PnP provisioning engine](https://msdn.microsoft.com/en-us/pnp_articles/pnp-provisioning-engine-and-the-core-library) with "modern" team sites.</span></span> <span data-ttu-id="f5ceb-163">PnP модуля подготовки автоматически определяет, если сайт — это сайт группы «современный» и настраивает поведение на основании поддерживаемые возможности.</span><span class="sxs-lookup"><span data-stu-id="f5ceb-163">The PnP provisioning engine automatically detects if a site is a "modern" team site and adjusts its behavior based on the supported capabilities.</span></span> <span data-ttu-id="f5ceb-164">Процесс — это именно то же, как с помощью PnP модуля подготовки с помощью «классический» сайтов, где не отключены возможности использования сценариев.</span><span class="sxs-lookup"><span data-stu-id="f5ceb-164">The process is exactly the same as using the PnP provisioning engine with "classic" sites where the scripting capabilities are not disabled.</span></span>

<span data-ttu-id="f5ceb-165">При применении шаблона удаленного сайта «современный» группы или сайта с поддержкой NoScript, учитываются следующие элементы:</span><span class="sxs-lookup"><span data-stu-id="f5ceb-165">The following elements are ignored when a remote template is applied to a "modern" team site or a site that has NoScript enabled:</span></span>

- <span data-ttu-id="f5ceb-166">Конфигурация **AuditLogTrimmingRetention** семейства сайтов в параметры аудита</span><span class="sxs-lookup"><span data-stu-id="f5ceb-166">Site collection **AuditLogTrimmingRetention** configuration in the auditing settings</span></span>
- <span data-ttu-id="f5ceb-167">Применение пользовательской темы на основе шаблона; Текущая реализация имеет зависимости на хранение пользовательской темы в каталог, который не поддерживается</span><span class="sxs-lookup"><span data-stu-id="f5ceb-167">Applying a custom theme from the template; current implementation has a dependency on storing a custom theme to the catalog, which is not supported</span></span>
- <span data-ttu-id="f5ceb-168">Параметры формы для типов контента</span><span class="sxs-lookup"><span data-stu-id="f5ceb-168">Form settings for content types</span></span>
- <span data-ttu-id="f5ceb-169">Добавление настраиваемых пользовательских действий для сайта, web или уровень списка</span><span class="sxs-lookup"><span data-stu-id="f5ceb-169">Adding custom user actions to site, web, or list level</span></span>
- <span data-ttu-id="f5ceb-170">Добавление файлов с типами файлов «.asmx», «.ascx», «.aspx», «.htc», «.jar», «.master», «.swf», «.xap», «.xsf»</span><span class="sxs-lookup"><span data-stu-id="f5ceb-170">Adding files with file types of ".asmx", ".ascx", ".aspx", ".htc", ".jar", ".master", ".swf", ".xap", ".xsf"</span></span>
- <span data-ttu-id="f5ceb-171">Добавление файлов в библиотеках со следующим URL-адресам `"_catalogs/theme"`, `"style library"`, `"_catalogs/lt"`,`"_catalogs/wp"`</span><span class="sxs-lookup"><span data-stu-id="f5ceb-171">Adding files to libraries with the following urls `"_catalogs/theme"`, `"style library"`, `"_catalogs/lt"`, `"_catalogs/wp"`</span></span>
- <span data-ttu-id="f5ceb-172">Добавление веб-частей для страницы сайта</span><span class="sxs-lookup"><span data-stu-id="f5ceb-172">Adding web parts to site pages</span></span>
- <span data-ttu-id="f5ceb-173">Хранение данных для подготовки шаблона для контейнера свойств подготовленный сайт</span><span class="sxs-lookup"><span data-stu-id="f5ceb-173">Storing provisioning template information to the property bag of the provisioned site</span></span>
- <span data-ttu-id="f5ceb-174">Добавление или обновление записи контейнера свойства контейнера свойств сайта</span><span class="sxs-lookup"><span data-stu-id="f5ceb-174">Adding or updating property bag entries to the site property bag</span></span>
- <span data-ttu-id="f5ceb-175">«Классический» публикации параметров и средств</span><span class="sxs-lookup"><span data-stu-id="f5ceb-175">"Classic" publishing settings and assets</span></span>
- <span data-ttu-id="f5ceb-176">Нет параметров обхода контента сайтов</span><span class="sxs-lookup"><span data-stu-id="f5ceb-176">Site No Crawl settings</span></span>
- <span data-ttu-id="f5ceb-177">Параметры главной страницы сайта</span><span class="sxs-lookup"><span data-stu-id="f5ceb-177">Site master page settings</span></span>

## <a name="apply-a-custom-theme-to-a-modern-team-site"></a><span data-ttu-id="f5ceb-178">Применение пользовательской темы на сайте команды «современный»</span><span class="sxs-lookup"><span data-stu-id="f5ceb-178">Apply a custom theme to a "modern" team site</span></span>

<span data-ttu-id="f5ceb-179">«Современный» веб-сайтов групп поддержки пользовательских тем, несмотря на то, что не удается загрузить новую запись коллекции для конечных пользователей.</span><span class="sxs-lookup"><span data-stu-id="f5ceb-179">"Modern" team sites support custom themes even though you cannot upload a new gallery entry for end users.</span></span> <span data-ttu-id="f5ceb-180">Это можно сделать, отправка необходимых средств на сайт и затем выполняется метод **ApplyTheme** .</span><span class="sxs-lookup"><span data-stu-id="f5ceb-180">This can be achieved by uploading the needed assets to the site and then executing the **ApplyTheme** method.</span></span> <span data-ttu-id="f5ceb-181">Приведенный ниже сценарий PowerShell показано, как выполнить это для сайта группы «современный».</span><span class="sxs-lookup"><span data-stu-id="f5ceb-181">The following PowerShell script shows how to perform this for a "modern" team site.</span></span>

```PowerShell

# Connect to a previously created Modern Site
$cred = Get-Credential
Connect-PnPOnline https://[tenant].sharepoint.com/sites/siteurl -Credentials $cred

# Apply a custom theme to a Modern Site

# First, upload the theme assets
Add-PnPFile -Path .\sppnp.spcolor -Folder SiteAssets
Add-PnPFile -Path .\sppnp-bg.png -Folder SiteAssets

# Second, apply the theme assets to the site
$web = Get-PnPWeb
$palette = $web.ServerRelativeUrl + "/SiteAssets/sppnp.spcolor"
$background = $web.ServerRelativeUrl + "/SiteAssets/sppnp-bg.png"

# We use OOTB CSOM operation for this
$web.ApplyTheme($palette, [NullString]::Value, $background, $true)
$web.Update()
# Set timeout as high as possible and execute
$web.Context.RequestTimeout = [System.Threading.Timeout]::Infinite
$web.Context.ExecuteQuery()

```

<br/>

<span data-ttu-id="f5ceb-182">*На рисунке 1. Сайт группы «Современный» с пользовательской темы*</span><span class="sxs-lookup"><span data-stu-id="f5ceb-182">*Figure 1. "Modern" team site with custom theme*</span></span>

![Сайт группы «Современный» с пользовательской темы](media/modern-experiences/modern-site-with-custom-theme.png)

> [!NOTE]
> - <span data-ttu-id="f5ceb-184">[Средство палитры цветов SharePoint](https://www.microsoft.com/en-us/download/details.aspx?id=38182) можно использовать для создания файла пользовательскую тему (.spcolor) с определением настраиваемые цвета.</span><span class="sxs-lookup"><span data-stu-id="f5ceb-184">You can use the [SharePoint Color Palette Tool](https://www.microsoft.com/en-us/download/details.aspx?id=38182) to create a custom theme file (.spcolor) with the custom color definition.</span></span> <span data-ttu-id="f5ceb-185">Как правило веб-сайтов групп «современный» попробуйте сохранить особенности темы, автоматически перейдя элементы темы «классический» сайт «современный» со стороны.</span><span class="sxs-lookup"><span data-stu-id="f5ceb-185">In general, "modern" team sites try to preserve the feel of the theme by automatically converting "classic" site theming elements to the "modern" side.</span></span> <span data-ttu-id="f5ceb-186">Сохраняемые области являются фонового изображения и разъемов следующие темы: ContentAccent1, PageBackground и BackgroundOverlay.</span><span class="sxs-lookup"><span data-stu-id="f5ceb-186">Preserved areas are background image and the following theme slots: ContentAccent1, PageBackground, and BackgroundOverlay.</span></span>
> - <span data-ttu-id="f5ceb-187">Эмблема сайта группы «современный» можно изменить с помощью API график групп, как показано SharePoint [PnP UpdateUnifiedGroup метод](https://github.com/SharePoint/PnP-Sites-Core/blob/master/Core/OfficeDevPnP.Core/Framework/Graph/UnifiedGroupsUtility.cs#L350).</span><span class="sxs-lookup"><span data-stu-id="f5ceb-187">You can change the logo of "modern" team site by using the Groups Graph API as shown by the SharePoint [PnP UpdateUnifiedGroup method](https://github.com/SharePoint/PnP-Sites-Core/blob/master/Core/OfficeDevPnP.Core/Framework/Graph/UnifiedGroupsUtility.cs#L350).</span></span>
> - <span data-ttu-id="f5ceb-188">Применение пользовательской темы на сайте «современный» команды может привести к времени ожидания.</span><span class="sxs-lookup"><span data-stu-id="f5ceb-188">Applying a custom theme to a "modern" team site can cause timeouts.</span></span> <span data-ttu-id="f5ceb-189">Решение для этой — отключить всех доступных [языков пользовательского интерфейса](https://support.office.com/en-us/article/Choose-the-languages-you-want-to-make-available-for-a-site-s-user-interface-16d3a83c-05ab-4b50-8fbb-ff576a3351e8) для сайта перед применением темы и снова включить их позже.</span><span class="sxs-lookup"><span data-stu-id="f5ceb-189">The resolution for this is to turn off all available [user interface languages](https://support.office.com/en-us/article/Choose-the-languages-you-want-to-make-available-for-a-site-s-user-interface-16d3a83c-05ab-4b50-8fbb-ff576a3351e8) for the site before applying the theme, and turn them back on afterwards.</span></span>

## <a name="determine-if-a-site-is-a-modern-team-site"></a><span data-ttu-id="f5ceb-190">Определение возможности сайта «современный» группы сайта</span><span class="sxs-lookup"><span data-stu-id="f5ceb-190">Determine if a site is a "modern" team site</span></span>

<span data-ttu-id="f5ceb-191">Можно определить, что сайт является сайтом «современный» team, проверив значение «Web.WebTemplate» сайта.</span><span class="sxs-lookup"><span data-stu-id="f5ceb-191">You can detect that a site is a "modern" team site by checking the 'Web.WebTemplate' value of the site.</span></span> <span data-ttu-id="f5ceb-192">«Современный» веб-сайтов групп с помощью шаблона «ГРУППА».</span><span class="sxs-lookup"><span data-stu-id="f5ceb-192">"Modern" team sites use the "GROUP" template.</span></span> <span data-ttu-id="f5ceb-193">Из-за поддерживаемые возможности общим для сайта группы «классический» при отключении сценариев, вы должны проверять оба параметра в коде для определения поведения вправо или поддерживаемые возможности.</span><span class="sxs-lookup"><span data-stu-id="f5ceb-193">Because the supported capabilities are the same for a "classic" team site when the scripting is disabled, you should be checking both settings in your code to determine the right behavior or supported capabilities.</span></span>

<span data-ttu-id="f5ceb-194">Так как нет прямого свойства для проверки, если сценарии разрешены или нет, можно использовать разрешения для определения текущего состояния.</span><span class="sxs-lookup"><span data-stu-id="f5ceb-194">Because there's no direct property to check if the scripting is enabled or not, you can use permissions to determine the current status.</span></span> <span data-ttu-id="f5ceb-195">При включении сценариев, не имеет разрешения AddAndCustomizePages в базовые разрешения сайта.</span><span class="sxs-lookup"><span data-stu-id="f5ceb-195">When scripting is enabled, there's no AddAndCustomizePages permission in the base permissions of the site.</span></span>

```C#
/// <summary>
/// Can be used to check if site has noscript enabled.
/// </summary>
/// <param name="web">site object to inspect</param>
/// <returns>True if no scripting is enabled, False if it's not</returns>
public static bool IsNoScriptSite(Web web)
{
    // Ensure that we have the needed properties - Notice that these are 
    // PnP CSOM extension capabilities
    web.EnsureProperties(w => w.WebTemplate, w => w.EffectiveBasePermissions);

    // Definition of no-script is not having the AddAndCustomizePages permission
    if (!web.EffectiveBasePermissions.Has(PermissionKind.AddAndCustomizePages))
    {
        return true;
    }

    // It's a site without noscript enabled
    return false;
}
```

## <a name="additional-considerations"></a><span data-ttu-id="f5ceb-196">Дополнительные сведения о выполнении</span><span class="sxs-lookup"><span data-stu-id="f5ceb-196">Additional considerations</span></span>

<span data-ttu-id="f5ceb-197">Постепенно описываются дополнительные параметры настройки для сайтов «современный» групп, которые способ выравнивания в выпуске дополнительные возможности среды SharePoint.</span><span class="sxs-lookup"><span data-stu-id="f5ceb-197">We'll gradually introduce more customization options for "modern" team sites that will be aligned with the release of additional SharePoint Framework capabilities.</span></span> <span data-ttu-id="f5ceb-198">В настоящее время недоступен расписание не точное, но при выпуске новых возможностей взаимодействия «современный» статьи будут обновляться.</span><span class="sxs-lookup"><span data-stu-id="f5ceb-198">Currently there is no exact schedule available, but we'll update the "modern" experience articles whenever new capabilities are released.</span></span>

## <a name="see-also"></a><span data-ttu-id="f5ceb-199">См. также</span><span class="sxs-lookup"><span data-stu-id="f5ceb-199">See also</span></span>

- [<span data-ttu-id="f5ceb-200">Настройка "современных" интерфейсов в SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="f5ceb-200">Customizing the "modern" experiences in SharePoint Online</span></span>](modern-experience-customizations.md)
- [<span data-ttu-id="f5ceb-201">PnP удаленного подготовки</span><span class="sxs-lookup"><span data-stu-id="f5ceb-201">PnP Remote Provisioning</span></span>](https://msdn.microsoft.com/en-us/pnp_articles/pnp-remote-provisioning)

