---
title: "Главные страницы в объектная модель SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: 1db93cc9e993dd09e83974ce254d3b4031281a4a
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
<a name="master-pages-in-the-sharepoint-add-in-model"></a><span data-ttu-id="560da-102">Главные страницы в объектная модель SharePoint</span><span class="sxs-lookup"><span data-stu-id="560da-102">Master pages in the SharePoint add-in model</span></span>
===========================================

<a name="summary"></a><span data-ttu-id="560da-103">Summary</span><span class="sxs-lookup"><span data-stu-id="560da-103">Summary</span></span>
-------

<span data-ttu-id="560da-104">Подход, необходимое для реализации настраиваемых главных страниц на сайтах SharePoint отличается в новой модели надстройки SharePoint не был с кодом полного доверия / решений фермы.</span><span class="sxs-lookup"><span data-stu-id="560da-104">The approach you take to implement custom master pages in SharePoint sites is different in the new SharePoint Add-in model than it was with Full Trust Code / Farm Solutions.</span></span> <span data-ttu-id="560da-105">В типичных полного доверия кода (FTC) аудио- и фирменной символики сценарий решения фермы, настраиваемые главные страницы создаются для реализации настраиваемого марки.</span><span class="sxs-lookup"><span data-stu-id="560da-105">In a typical Full Trust Code (FTC) / Farm Solution branding scenario, custom master pages are created to implement a custom brand.</span></span> <span data-ttu-id="560da-106">Главные страницы обычно упакованный в функциональная возможность, которая использует декларативного кода и FTC / решения фермы для развертывания главные страницы и регистрировать их с сайта SharePoint.</span><span class="sxs-lookup"><span data-stu-id="560da-106">The master pages are typically packaged in a feature that uses declarative code and a FTC / Farm Solution to deploy the master pages and register them with the SharePoint site.</span></span>

<span data-ttu-id="560da-107">В SharePoint надстройки модели фирменной настройки сценарии, может быть настраиваемых главных страниц также можно использовать.</span><span class="sxs-lookup"><span data-stu-id="560da-107">In a SharePoint Add-in model branding scenario, custom master pages may be also be used.</span></span> <span data-ttu-id="560da-108">Можно развернуть и зарегистрировать настраиваемых главных страниц на сайтах SharePoint с помощью шаблона подготовки удаленного.</span><span class="sxs-lookup"><span data-stu-id="560da-108">You can deploy and register your custom master pages on SharePoint sites via the remote-provisioning pattern.</span></span>

<a name="high-level-guidelines-for-custom-master-pages"></a><span data-ttu-id="560da-109">Высокоуровневая рекомендаций для настраиваемых главных страниц</span><span class="sxs-lookup"><span data-stu-id="560da-109">High-level guidelines for custom master pages</span></span>
---------------------------------------------

<span data-ttu-id="560da-110">Как правило эскиз мы предлагаем для обеспечения высокого уровня следующие рекомендации для настраиваемых главных страниц.</span><span class="sxs-lookup"><span data-stu-id="560da-110">As a rule of a thumb, we would like to provide the following high-level guidelines for custom master pages.</span></span>

- <span data-ttu-id="560da-111">Настройка сайтов SharePoint с помощью настраиваемых главных страниц, но оставьте учитывать в результате вы дополнительные долгосрочные затраты и проблемы, связанные с с будущими обновлениями.</span><span class="sxs-lookup"><span data-stu-id="560da-111">You can customize SharePoint sites using custom master pages, but keep in mind this will cause you additional long-term costs and challenges with future updates.</span></span>
    + <span data-ttu-id="560da-112">В большинстве случаев можно достичь все распространенные сценарии фирменной настройки с темами, вариантов оформления и альтернативной таблицы CSS.</span><span class="sxs-lookup"><span data-stu-id="560da-112">In most cases, you can achieve all common branding scenarios with themes, composed looks and alternate CSS.</span></span>
    
        <span data-ttu-id="560da-113">В разделе [Фирменный стиль сайтов SharePoint (SharePoint надстройки набора)](branding-sharepoint-sites-sharepoint-add-in.md) , узнайте все об параметры фирменной символики для сайтов SharePoint с помощью модели надстройки SharePoint.</span><span class="sxs-lookup"><span data-stu-id="560da-113">See the [Branding SharePoint Sites (SharePoint Add-in Recipe)](branding-sharepoint-sites-sharepoint-add-in.md) to learn all about the different branding options you have for SharePoint sites with the SharePoint Add-in model.</span></span>  <span data-ttu-id="560da-114">Рецептов позволит учесть короткие и долгосрочного влияния настройки из рабочий и точки зрения обслуживания.</span><span class="sxs-lookup"><span data-stu-id="560da-114">The recipe will help you consider the short and long-term impact of customization from an operational and a maintenance perspective.</span></span> <span data-ttu-id="560da-115">Может оказаться, что настраиваемой главной страницы не требуется реализовать особые требования к фирменной настройки.</span><span class="sxs-lookup"><span data-stu-id="560da-115">You may discover that a custom master page is not required to implement your specific branding requirements.</span></span> 

    + <span data-ttu-id="560da-116">Если вы решили использовать настраиваемые главные страницы, будьте готовым применить изменения к настраиваемых главных страниц, когда основные функциональные обновления применяются к Office 365.</span><span class="sxs-lookup"><span data-stu-id="560da-116">If you chose to use custom master pages, be prepared to apply changes to the custom master pages when major functional updates are applied to Office 365.</span></span>
- <span data-ttu-id="560da-117">Используйте удаленного подготовки для развертывания и регистрации настраиваемых главных страниц с сайтами SharePoint.</span><span class="sxs-lookup"><span data-stu-id="560da-117">Use remote provisioning to deploy and register custom master pages with SharePoint sites.</span></span>
- <span data-ttu-id="560da-118">Не используйте декларативный код или изолированной среды для развертывания и регистрации главных страниц с сайтами SharePoint.</span><span class="sxs-lookup"><span data-stu-id="560da-118">Do not use declarative code or sandbox code to deploy and register master pages with SharePoint sites.</span></span>  

<a name="team-sites-vs-publishing-sites"></a><span data-ttu-id="560da-119">Сайты рабочих групп и веб-сайтах публикации</span><span class="sxs-lookup"><span data-stu-id="560da-119">Team sites vs. publishing sites</span></span>
-------------------------------

<span data-ttu-id="560da-120">**При необходимости настраиваемой главной страницы**</span><span class="sxs-lookup"><span data-stu-id="560da-120">**When is a custom master page needed?**</span></span>

<span data-ttu-id="560da-121">При применении пользовательских фирменной символики для сайтов SharePoint, возникнет необходимость фирменной символики сайтов публикации и веб-сайтов групп.</span><span class="sxs-lookup"><span data-stu-id="560da-121">When applying custom branding to SharePoint sites, you will encounter the need to brand both team sites and publishing sites.</span></span> <span data-ttu-id="560da-122">В целом сайты в интрасетях, построенный на SharePoint в локальных и сценарии в Office 365 использовать сочетание сайтов публикации и веб-сайтов групп.</span><span class="sxs-lookup"><span data-stu-id="560da-122">Generally speaking, intranets built on SharePoint in both on-premises and Office 365 scenarios use a combination of team sites and publishing sites.</span></span>  

<span data-ttu-id="560da-123">С фирменными требования к зачастую требуют определенных макет изменяется, тем и не может выполнять JavaScript, внедрение методов.</span><span class="sxs-lookup"><span data-stu-id="560da-123">Custom branding requirements often times require specific layout changes that themes and JavaScript embedding techniques cannot accomplish.</span></span>

<span data-ttu-id="560da-124">В этом случае веб-сайтов групп обычно не требуется объем настраиваемый фирменный стиль, что выполните сайтов публикации и обычно достаточно для поддержки мобильных устройств для веб-сайтов групп SharePoint ожидания введите, современное представление для мобильных устройств.</span><span class="sxs-lookup"><span data-stu-id="560da-124">In such a scenario, team sites usually do not require the amount of custom branding that publishing sites do and the out-of-the-box SharePoint Contemporary View for mobile devices is usually sufficient to support mobile devices for team sites.</span></span> <span data-ttu-id="560da-125">Поскольку это так, лучше использовать только настраиваемые главные страницы для публикации сайтов и использовать AlternativeCSS и пользовательских тем SharePoint (.spcolor-файлы), схемы шрифтов (.spfont-файлы) и фоновые изображения, определенного как вариантов оформления для веб-сайтов групп торговых марок.</span><span class="sxs-lookup"><span data-stu-id="560da-125">Since this is the case, it is best to only use custom master pages for publishing sites and to use AlternativeCSS and custom SharePoint themes (.spcolor files), font schemes (.spfont files) and background images defined as composed looks to brand team sites.</span></span>

<span data-ttu-id="560da-126">**Рекомендации по развертыванию**</span><span class="sxs-lookup"><span data-stu-id="560da-126">**Deployment considerations**</span></span>

- <span data-ttu-id="560da-127">При развертывании настраиваемых главных страниц для *сайтов публикации* необходимо развернуть настраиваемых главных страниц корневого сайта.</span><span class="sxs-lookup"><span data-stu-id="560da-127">When deploying custom master pages to *publishing sites* you only need to deploy the custom master pages to the root site.</span></span>
    + <span data-ttu-id="560da-128">[Provisioning.PublishingFeatures (PnP образец O365)](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.PublishingFeatures) демонстрирует развертывание настраиваемых главных страниц на сайтах публикации.</span><span class="sxs-lookup"><span data-stu-id="560da-128">The [Provisioning.PublishingFeatures (O365 PnP Sample)](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.PublishingFeatures) demonstrates how to deploy custom master pages to publishing sites.</span></span> 
    + <span data-ttu-id="560da-129">[Подготовка SharePoint компоненты публикации (O365 PnP видео)](http://channel9.msdn.com/Blogs/Office-365-Dev/Provisioning-SharePoint-Publishing-Features-Office-365-Developer-Patterns-and-Practices) — описание примера.</span><span class="sxs-lookup"><span data-stu-id="560da-129">The [Provisioning SharePoint Publishing Features (O365 PnP Video)](http://channel9.msdn.com/Blogs/Office-365-Dev/Provisioning-SharePoint-Publishing-Features-Office-365-Developer-Patterns-and-Practices) walks you through the sample.</span></span>   
- <span data-ttu-id="560da-130">При развертывании настраиваемых главных страниц на *сайтах не для публикации* , необходимые для развертывания настраиваемых главных страниц для каждого сайта.</span><span class="sxs-lookup"><span data-stu-id="560da-130">When deploying custom master pages to *non-publishing sites* you need to deploy the custom master pages to each site.</span></span>

<span data-ttu-id="560da-131">Настраиваемые главные страницы, обычно применяются при подготовке сайта.</span><span class="sxs-lookup"><span data-stu-id="560da-131">Custom master pages are typically applied when a site is provisioned.</span></span> <span data-ttu-id="560da-132">Процесс подготовки удаленной очень хорошо подходит при использовании этого подхода.</span><span class="sxs-lookup"><span data-stu-id="560da-132">The remote provisioning process fits very well with this approach.</span></span> <span data-ttu-id="560da-133">Обычно только времени, чтобы вручную применить фирменной настройки SharePoint будет использоваться веб-браузер — после создания прототипов или изменение одного сайта SharePoint, которого не запланировано на случай увеличения для включения других семейств веб-сайтов или sub сайтам.</span><span class="sxs-lookup"><span data-stu-id="560da-133">Usually the only time you will use the web browser to manually apply SharePoint branding customization is when you are prototyping or modifying a single SharePoint site that is not planned to grow to include other site collections or sub sites.</span></span> 

+ <span data-ttu-id="560da-134">Дополнительные сведения о развертывании и Дополнительные примеры в разделе [модулей (добавить в SharePoint набора команд)](modules-sharepoint-add-in.md) и [Подготовки сайта (добавить в SharePoint набора команд)](site-provisioning-sharepoint-add-in.md) .</span><span class="sxs-lookup"><span data-stu-id="560da-134">See the [Modules (SharePoint Add-in Recipe)](modules-sharepoint-add-in.md) and [Site Provisioning (SharePoint Add-in Recipe)](site-provisioning-sharepoint-add-in.md) for more deployment details and additional samples.</span></span>

<a name="more-details-about-custom-master-pages-and-page-layouts-for-sharepoint-sites"></a><span data-ttu-id="560da-135">Дополнительные сведения о настраиваемых главных страниц и макетов страниц для сайтов SharePoint</span><span class="sxs-lookup"><span data-stu-id="560da-135">More details about custom master pages and page layouts for SharePoint sites</span></span>
----------------------------------------------------------------------------

<span data-ttu-id="560da-136">В сценариях, где настраиваемой главной страницы — это единственный способ реализации пользовательского брендинга требований можно создать настраиваемую главную страницу и макеты страниц.</span><span class="sxs-lookup"><span data-stu-id="560da-136">In scenarios where a custom master page is the only way to implement your custom branding requirements you can create a custom master page and page layouts.</span></span> <span data-ttu-id="560da-137">Имейте в виду точки в начале этой статьи по отношению к долгосрочного обслуживания расходы, связанные с этого подхода.</span><span class="sxs-lookup"><span data-stu-id="560da-137">Keep in mind the points made at the beginning of this article with regard to the long-term maintenance costs associated with this approach.</span></span>

- <span data-ttu-id="560da-138">Использование настраиваемых главных страниц для сайтов SharePoint обеспечивает максимальный уровень настройки (без ограничений).</span><span class="sxs-lookup"><span data-stu-id="560da-138">Using custom master pages for SharePoint sites provides the ultimate level of customization (unlimited).</span></span>
- <span data-ttu-id="560da-139">Использование настраиваемых главных страниц для сайтов SharePoint требуется наибольшее количество времени, в реализации и обслуживании в короткие и длинные терминов.</span><span class="sxs-lookup"><span data-stu-id="560da-139">Using custom master pages for SharePoint sites requires the largest amount of time to implement and maintain in the short and long term.</span></span>
- <span data-ttu-id="560da-140">Любые изменения ожидания введите главных страниц, входящие в состав обновления не будут отражены в настраиваемых главных страниц.</span><span class="sxs-lookup"><span data-stu-id="560da-140">Any changes to out-of-the-box master pages that come with service updates will not be reflected in custom master pages.</span></span>
- <span data-ttu-id="560da-141">Можно применить настраиваемых главных страниц на уровне отдельных веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="560da-141">You can apply custom master pages at a per-site level.</span></span>
- <span data-ttu-id="560da-142">При использовании настраиваемой главной страницы, рекомендуется начать с одно-стандартной главные страницы и измените его в соответствии со своими потребностями.</span><span class="sxs-lookup"><span data-stu-id="560da-142">When using a custom master page it is recommended to start with one of the out-of-the-box master pages and modify it to meet your needs.</span></span>
    + <span data-ttu-id="560da-143">Попробуйте минимизировать объем настроек, создаваемые с помощью настраиваемых главных страниц; Это облегчит обновлять их, если изменения в службе Office 365 ожидания введите главных страницах, которые необходимо переместить на настраиваемых главных страниц.</span><span class="sxs-lookup"><span data-stu-id="560da-143">Try to minimize the amount of customization you make with custom master pages; this will make it easier to update them when Office 365 service changes to out-of-the-box master pages must be replicated to custom master pages.</span></span>  
- <span data-ttu-id="560da-144">Существует множество необходимых заполнителей контента в главных страницах SharePoint, которые не должны быть удалены или они приводят страницы на ошибки.</span><span class="sxs-lookup"><span data-stu-id="560da-144">There are many required content placeholders in SharePoint master pages that must not be removed or they will cause the pages to error.</span></span> <span data-ttu-id="560da-145">Вы будете знать, после удаления требуется заполнитель контента так, как минуты развернуть его и назначить главной страницы на свой сайт будет отображаться ошибки.</span><span class="sxs-lookup"><span data-stu-id="560da-145">You will know when you have removed a required content placeholder because the minute you deploy it and assign the master page to your site, errors will appear.</span></span>

<span data-ttu-id="560da-146">**Когда завершается настраиваемые главные страницы и макеты страниц для сайта SharePoint подходит?**</span><span class="sxs-lookup"><span data-stu-id="560da-146">**When are custom master pages and page layouts for a SharePoint site a good fit?**</span></span>

<span data-ttu-id="560da-147">Этот параметр работает, когда потребностей фирменной настройки находятся или использовании сайтов публикации.</span><span class="sxs-lookup"><span data-stu-id="560da-147">This option works well when your branding needs are very specific or you are using publishing sites.</span></span>

<span data-ttu-id="560da-148">**Рекомендуется методах развертывания**</span><span class="sxs-lookup"><span data-stu-id="560da-148">**Recommended deployment approaches**</span></span>

- <span data-ttu-id="560da-149">Настраиваемые главные страницы может вручную отправляется через веб-браузер и вручную назначаться вариантов оформления.</span><span class="sxs-lookup"><span data-stu-id="560da-149">Custom master pages may be uploaded manually via the web browser and manually assigned to composed looks.</span></span>
- <span data-ttu-id="560da-150">Настраиваемых главных страниц может отправить и назначить для сайта SharePoint с помощью удаленного подготовки шаблоне также.</span><span class="sxs-lookup"><span data-stu-id="560da-150">Custom master pages may be uploaded and assigned to a SharePoint site via the remote provisioning pattern as well.</span></span>
    + <span data-ttu-id="560da-151">Дополнительные сведения о развертывании и Дополнительные примеры в разделе [модулей (добавить в SharePoint набора команд)](modules-sharepoint-add-in.md) и [Подготовки сайта (добавить в SharePoint набора команд)](site-provisioning-sharepoint-add-in.md) .</span><span class="sxs-lookup"><span data-stu-id="560da-151">See the [Modules (SharePoint Add-in Recipe)](modules-sharepoint-add-in.md) and [Site Provisioning (SharePoint Add-in Recipe)](site-provisioning-sharepoint-add-in.md) for more deployment details and additional samples.</span></span>

<a name="related-links"></a><span data-ttu-id="560da-152">Ссылки по теме</span><span class="sxs-lookup"><span data-stu-id="560da-152">Related links</span></span>
=============
- [<span data-ttu-id="560da-153">Модули (надстройки SharePoint набора команд)</span><span class="sxs-lookup"><span data-stu-id="560da-153">Modules (SharePoint Add-in Recipe)</span></span>](modules-sharepoint-add-in.md)
- [<span data-ttu-id="560da-154">(Надстройка SharePoint набора команд) по подготовке сайта</span><span class="sxs-lookup"><span data-stu-id="560da-154">Site Provisioning (SharePoint Add-in Recipe)</span></span>](site-provisioning-sharepoint-add-in.md)
- [<span data-ttu-id="560da-155">Фирменный стиль сайтов SharePoint (надстройки SharePoint набора команд)</span><span class="sxs-lookup"><span data-stu-id="560da-155">Branding SharePoint Sites (SharePoint Add-in Recipe)</span></span>](branding-sharepoint-sites-sharepoint-add-in.md)
- <span data-ttu-id="560da-156">Ignite 2015 - [глубокое погружение в безопасном SharePoint фирменной символики в Office 365 с помощью возможности повторяемого шаблоны и рекомендации](https://channel9.msdn.com/Events/Ignite/2015/BRK3164)</span><span class="sxs-lookup"><span data-stu-id="560da-156">Ignite 2015 - [Deep Dive into Safe SharePoint Branding in Office 365 Using Repeatable Patterns and Practices](https://channel9.msdn.com/Events/Ignite/2015/BRK3164)</span></span>
- <span data-ttu-id="560da-157">Руководств по [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Руководств")</span><span class="sxs-lookup"><span data-stu-id="560da-157">Guidance articles at [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Guidance Articles")</span></span>
- <span data-ttu-id="560da-158">Справочные материалы в библиотеке MSDN по [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "Справочные материалы в библиотеке MSDN")</span><span class="sxs-lookup"><span data-stu-id="560da-158">References in MSDN at [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "References in MSDN")</span></span>
- <span data-ttu-id="560da-159">Видеозаписи по [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "видео")</span><span class="sxs-lookup"><span data-stu-id="560da-159">Videos at [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")</span></span>

<a name="related-pnp-samples"></a><span data-ttu-id="560da-160">Примеры связанных с ними PnP</span><span class="sxs-lookup"><span data-stu-id="560da-160">Related PnP samples</span></span>
===================

- [<span data-ttu-id="560da-161">Управление темы, с помощью CSOM (O365 PnP образец)</span><span class="sxs-lookup"><span data-stu-id="560da-161">Theme management using CSOM (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Branding.DeployCustomThemeWeb)
- [<span data-ttu-id="560da-162">AlternateCSSUrl и SiteLogoUrl свойствами в веб-объект (O365 PnP образец)</span><span class="sxs-lookup"><span data-stu-id="560da-162">AlternateCSSUrl and SiteLogoUrl Properties in the web object (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Branding.AlternateCSSAndSiteLogo)
- [<span data-ttu-id="560da-163">Задать тему к сайту (O365 PnP образец)</span><span class="sxs-lookup"><span data-stu-id="560da-163">Set theme to site (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Branding.SetThemeToSite)
- [<span data-ttu-id="560da-164">Установка темы SharePoint в приложении для SharePoint (O365 PnP образец)</span><span class="sxs-lookup"><span data-stu-id="560da-164">Setting a SharePoint Theme in an App for SharePoint (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Branding.Themes)
- [<span data-ttu-id="560da-165">Отображение совершенно новом уровне Сиэтл главных отклика (O365 PnP образец)</span><span class="sxs-lookup"><span data-stu-id="560da-165">Making out of the box Seattle master responsive (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Branding.InjectResponsiveCSS)
- <span data-ttu-id="560da-166">Примеры и содержимое в [https://github.com/SharePoint/PnP](https://github.com/SharePoint/PnP)</span><span class="sxs-lookup"><span data-stu-id="560da-166">Samples and content at [https://github.com/SharePoint/PnP](https://github.com/SharePoint/PnP)</span></span>

<a name="applies-to"></a><span data-ttu-id="560da-167">Применимо к</span><span class="sxs-lookup"><span data-stu-id="560da-167">Applies to</span></span>
==========
- <span data-ttu-id="560da-168">Office 365 нескольких клиентов (MT)</span><span class="sxs-lookup"><span data-stu-id="560da-168">Office 365 Multi Tenant (MT)</span></span>
- <span data-ttu-id="560da-169">Office 365 выделенных (D) *частично*</span><span class="sxs-lookup"><span data-stu-id="560da-169">Office 365 Dedicated (D) *partly*</span></span>
- <span data-ttu-id="560da-170">SharePoint 2013 в локальной — *частично*</span><span class="sxs-lookup"><span data-stu-id="560da-170">SharePoint 2013 on-premises – *partly*</span></span>

<span data-ttu-id="560da-171">*Шаблоны для выделенных и локальной идентичны с помощью надстройки SharePoint методики модели, но возможных технологий, которые могут использоваться отличаются.*</span><span class="sxs-lookup"><span data-stu-id="560da-171">*Patterns for dedicated and on-premises are identical with SharePoint Add-in model techniques, but there are differences on the possible technologies that can be used.*</span></span>