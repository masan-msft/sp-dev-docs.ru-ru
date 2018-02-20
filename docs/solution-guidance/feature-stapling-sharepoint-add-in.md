---
title: "Ассоциация в объектная модель SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: 204f53d47256b51ef6c2495deae4c69ce810fa23
ms.sourcegitcommit: e157d51378190ddfed6394ba154ce66141c8ca33
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/19/2018
---
<a name="feature-stapling-in-the-sharepoint-add-in-model"></a><span data-ttu-id="c5c77-102">Ассоциация в объектная модель SharePoint</span><span class="sxs-lookup"><span data-stu-id="c5c77-102">Feature Stapling in the SharePoint add-in model</span></span>
===============================================

<a name="summary"></a><span data-ttu-id="c5c77-103">Summary</span><span class="sxs-lookup"><span data-stu-id="c5c77-103">Summary</span></span>
-------

<span data-ttu-id="c5c77-104">Подхода, можно выполнять код и развертывание артефактов при подготовке сайта SharePoint будет разным в новой модели надстройки SharePoint не был с кодом полного доверия.</span><span class="sxs-lookup"><span data-stu-id="c5c77-104">The approach you take to run code and deploy artifacts when a SharePoint site is provisioned is different in the new SharePoint Add-in model than it was with Full Trust Code.</span></span>  <span data-ttu-id="c5c77-105">В типичных полного доверия кода (FTC) / сценарий решения фермы, определения были изменены с сайта ожидания введите сшивания функций.</span><span class="sxs-lookup"><span data-stu-id="c5c77-105">In a typical Full Trust Code (FTC) / Farm Solution scenario, out-of-the-box site definitions were modified with stapled features.</span></span>  <span data-ttu-id="c5c77-106">Функции использовались для упаковки и развертывания артефактов, конфигураций и фирменной настройки основных средств, связанных с сайтом SharePoint и были сшивания функций для определения сайта.</span><span class="sxs-lookup"><span data-stu-id="c5c77-106">Features were used to package and deploy artifacts, configurations, and branding assets associated with a SharePoint site and features were stapled to the site definition.</span></span>  <span data-ttu-id="c5c77-107">Затем сшитого функции были автоматически устанавливается и активируется при инициализации сайта.</span><span class="sxs-lookup"><span data-stu-id="c5c77-107">Then the stapled features were automatically installed and activated upon site provisioning.</span></span>

<span data-ttu-id="c5c77-108">В SharePoint надстройки модели сценарии может сшивания функций, сшивания надстройки или с помощью SharePoint клиента со стороны объектной модели (CSOM) Создание и настройка семейств веб-сайтов и sub сайтам затем развертывание артефактов, конфигураций и фирменной настройки ресурсов.</span><span class="sxs-lookup"><span data-stu-id="c5c77-108">In an SharePoint Add-in model scenario, you may staple features, staple Add-ins, or use the SharePoint Client Side Object Model (CSOM) to create and configure site collections and sub sites then deploy artifacts, configurations, and branding assets to them.</span></span> <span data-ttu-id="c5c77-109">Этот шаблон обычно называемую *удаленного подготовки шаблон*.</span><span class="sxs-lookup"><span data-stu-id="c5c77-109">This pattern is commonly referred to as the *remote provisioning pattern*.</span></span>

<a name="high-level-guidelines"></a><span data-ttu-id="c5c77-110">Рекомендации по высокого уровня</span><span class="sxs-lookup"><span data-stu-id="c5c77-110">High Level Guidelines</span></span>
---------------------

<span data-ttu-id="c5c77-111">Как правило эскиз мы предлагаем для обеспечения высокого уровня следующее Создание и настройка семейств веб-сайтов и sub сайтам затем развертывание артефактов, конфигураций и фирменной настройки ресурсов.</span><span class="sxs-lookup"><span data-stu-id="c5c77-111">As a rule of a thumb, we would like to provide the following high level guidelines to create and configure site collections and sub sites then deploy artifacts, configurations, and branding assets to them.</span></span>

- <span data-ttu-id="c5c77-112">Единственным способом, можно использовать функции ассоциация при Ассоциация возможности для семейств веб-сайтов и развертывание определения сайта и сшитого возможности с помощью изолированных решений.</span><span class="sxs-lookup"><span data-stu-id="c5c77-112">The only way you can still use feature stapling is when you are stapling features to site collections and you are using sandbox solutions to deploy the site definitions and the stapled features.</span></span>    
- <span data-ttu-id="c5c77-113">Можно использовать надстройку ассоциация модели с помощью клиента развернут надстройки для реализации функциональные возможности, аналогичные ассоциации возможности.</span><span class="sxs-lookup"><span data-stu-id="c5c77-113">You can use the Add-in stapling model with tenant deployed Add-ins to implement functionality similar to feature stapling.</span></span>
- <span data-ttu-id="c5c77-114">Удаленный подготовки шаблон можно использовать для реализации функциональные возможности, аналогичные прикреплять по активации дополнительных функций на основе определения сайта ожидания введите поле с помощью API удаленного.</span><span class="sxs-lookup"><span data-stu-id="c5c77-114">You can use the remote provisioning pattern to implement functionality similar to feature stapling by activating additional features on top of the out-of-the-box box site definition via remote APIs.</span></span>

<a name="options-to-create-and-configure-site-collections-and-sub-sites-then-deploy-artifacts-configurations-and-branding-assets-to-them"></a><span data-ttu-id="c5c77-115">Параметры, чтобы создание и настройка семейств веб-сайтов и затем sub сайтам развертывания артефактов, конфигураций и фирменной настройки средств им</span><span class="sxs-lookup"><span data-stu-id="c5c77-115">Options to create and configure site collections and sub sites then deploy artifacts, configurations, and branding assets to them</span></span>
---------------------------------------------------------------------------------------------------------------------------------

<span data-ttu-id="c5c77-116">Необходимо некоторые параметры, чтобы создать и настроить семейств веб-сайтов и sub сайтам затем развертывание артефактов, конфигураций и фирменной настройки средств.</span><span class="sxs-lookup"><span data-stu-id="c5c77-116">You have a few options to to create and configure site collections and sub sites then deploy artifacts, configurations, and branding assets to them.</span></span>

- <span data-ttu-id="c5c77-117">Функции скобка</span><span class="sxs-lookup"><span data-stu-id="c5c77-117">Staple features</span></span>
- <span data-ttu-id="c5c77-118">Скобка надстроек</span><span class="sxs-lookup"><span data-stu-id="c5c77-118">Staple Add-ins</span></span>
- <span data-ttu-id="c5c77-119">Использование удаленных подготовки схемы</span><span class="sxs-lookup"><span data-stu-id="c5c77-119">Use the remote provisioning pattern</span></span>   

<a name="staple-features"></a><span data-ttu-id="c5c77-120">Функции скобка</span><span class="sxs-lookup"><span data-stu-id="c5c77-120">Staple features</span></span>
---------------
<span data-ttu-id="c5c77-121">В этом шаблоне сшивания функций для определения сайтов.</span><span class="sxs-lookup"><span data-stu-id="c5c77-121">In this pattern you staple features to site definitions.</span></span>
    
- <span data-ttu-id="c5c77-122">Этот шаблон доступен только на уровне семейства сайтов.</span><span class="sxs-lookup"><span data-stu-id="c5c77-122">This pattern is only available at the site collection level.</span></span>
- <span data-ttu-id="c5c77-123">Не поддерживается для сшивания функций для вложенных сайтов.</span><span class="sxs-lookup"><span data-stu-id="c5c77-123">It is not possible to staple features to sub sites.</span></span>
- <span data-ttu-id="c5c77-124">Это не оптимальную или рекомендуемый подход, так как он использует не рекомендуемые для использования изолированных решений и не настроена вы контейнер для обновлений.</span><span class="sxs-lookup"><span data-stu-id="c5c77-124">This is not an optimal or recommended approach because it uses deprecated sandbox solutions and does not set you up well for upgrades.</span></span>

<span data-ttu-id="c5c77-125">**Когда это подходит?**</span><span class="sxs-lookup"><span data-stu-id="c5c77-125">**When is it a good fit?**</span></span>

<span data-ttu-id="c5c77-126">При переносе кода прежних версий в локальной среде SharePoint и у вас время повторно создавать должным образом.</span><span class="sxs-lookup"><span data-stu-id="c5c77-126">When you are migrating legacy code in an on-premises SharePoint environment and you do not have time to re-write it properly.</span></span>

<span data-ttu-id="c5c77-127">**Приступая к работе**</span><span class="sxs-lookup"><span data-stu-id="c5c77-127">**Getting Started**</span></span>

<span data-ttu-id="c5c77-128">Следующие статьи описывается сшивания функций для определения сайта.</span><span class="sxs-lookup"><span data-stu-id="c5c77-128">The following article describes how to staple features to a site definition.</span></span>

- [<span data-ttu-id="c5c77-129">Ассоциации возможности в SharePoint 2010 (статья блога MSDN)</span><span class="sxs-lookup"><span data-stu-id="c5c77-129">Feature Stapling In SharePoint 2010 (MSDN Blog Article)</span></span>](http://blogs.msdn.com/b/kunal_mukherjee/archive/2011/01/11/feature-stapling-in-sharepoint-2010.aspx)

<a name="staple-add-ins"></a><span data-ttu-id="c5c77-130">Скобка надстроек</span><span class="sxs-lookup"><span data-stu-id="c5c77-130">Staple Add-ins</span></span>
--------------
<span data-ttu-id="c5c77-131">В этом шаблоне развертывание надстройки хранятся в каталоге приложений для определенных семейств сайтов, управляемых путей и шаблонах сайтов.</span><span class="sxs-lookup"><span data-stu-id="c5c77-131">In this pattern you deploy Add-ins stored in the app catalog to specific site collections, managed paths, and site templates.</span></span>

- <span data-ttu-id="c5c77-132">В разделе [Развертывание приложений SharePoint 2013 через «приложение ассоциация» (блог статья MSDN - Richard DiZerega)](http://blogs.msdn.com/b/richard_dizeregas_blog/archive/2013/09/18/10399333.aspx) для получения дополнительных сведений о сшивания модели надстройки.</span><span class="sxs-lookup"><span data-stu-id="c5c77-132">See the [SharePoint 2013 App Deployment through 'App Stapling' (MSDN Blog Article - Richard DiZerega)](http://blogs.msdn.com/b/richard_dizeregas_blog/archive/2013/09/18/10399333.aspx) for more details about the Add-in stapling model.</span></span>
- <span data-ttu-id="c5c77-133">Так как надстройки помещается администратором, владельцы веб-сайтов не будет возможность удалить надстройку из сайта, отвечающую критерии развертывания.</span><span class="sxs-lookup"><span data-stu-id="c5c77-133">Because the add-in is pushed by an administrator, site owners will not be able to remove the add-in from a site that meets the deployment criteria.</span></span>  <span data-ttu-id="c5c77-134">Даже не администратором семейства сайтов можно удалить надстройку.</span><span class="sxs-lookup"><span data-stu-id="c5c77-134">Not even a site collection administrator can remove the add-in.</span></span>
- <span data-ttu-id="c5c77-135">В этом централизованного развертывания также использует те же централизованного надстройки ресурсы (Add-in веб-серверы и удаленного сайта).</span><span class="sxs-lookup"><span data-stu-id="c5c77-135">This centralized deployment also shares the same centralized add-in resources (Add-in Web and Remote Web).</span></span>  <span data-ttu-id="c5c77-136">По сути добавить в развертывание, но не установлен на веб-сайтах.</span><span class="sxs-lookup"><span data-stu-id="c5c77-136">Essentially, the Add-in is deployed, but not installed in the sites.</span></span>  <span data-ttu-id="c5c77-137">Все сайты значение будет использовать Add-in Web и удаленного веб-из экземпляра, установленные в каталоге приложений.</span><span class="sxs-lookup"><span data-stu-id="c5c77-137">All sites will leverage the Add-in Web and Remote Web from the instance installed in the app catalog.</span></span>
- <span data-ttu-id="c5c77-138">Из-за централизованного развертывания удаленных событий, таких как «Управление установленными приложениями», «Обработка удалении приложения» и «Обработка обновления приложения» возникает только один раз (если надстройка установлен в каталог приложений).</span><span class="sxs-lookup"><span data-stu-id="c5c77-138">Because of centralized deployment, remote events such as 'Handle App Installed', 'Handle App Uninstalled', and 'Handle App Upgrade' will only fire once (when the Add-In is installed in the app catalog).</span></span>
    + <span data-ttu-id="c5c77-139">Это может усложнить использование сшивания шаблон надстройки для автоматически применить изменения к сайтам, где он будет развернут, так как эти события не возникают при развертывании на сайты.</span><span class="sxs-lookup"><span data-stu-id="c5c77-139">This can make it difficult to use the Add-in stapling pattern to automatically apply changes to sites where it is deployed because these events do not fire when it is deployed to sites.</span></span>
- <span data-ttu-id="c5c77-140">Добавить в части не поддерживаются при Add-ins сшивания на сайты.</span><span class="sxs-lookup"><span data-stu-id="c5c77-140">Add-in parts are not supported when Add-ins are stapled to sites.</span></span>
- <span data-ttu-id="c5c77-141">Этот шаблон требует ручной пользовательских действий для развертывания надстройки.</span><span class="sxs-lookup"><span data-stu-id="c5c77-141">This pattern requires manual user actions to deploy the Add-ins.</span></span>

<a name="use-the-remote-provisioning-pattern"></a><span data-ttu-id="c5c77-142">Использование удаленных подготовки схемы</span><span class="sxs-lookup"><span data-stu-id="c5c77-142">Use the remote provisioning pattern</span></span>
-----------------------------------

<span data-ttu-id="c5c77-143">В этом шаблоне используйте SharePoint клиента со стороны объектной модели (CSOM) для создания и настройка семейств веб-сайтов и sub сайтам затем развертывание артефактов, конфигураций и фирменной настройки средств.</span><span class="sxs-lookup"><span data-stu-id="c5c77-143">In this pattern you use the SharePoint Client Side Object Model (CSOM) to create and configure site collections and sub sites then deploy artifacts, configurations, and branding assets to them.</span></span>

- <span data-ttu-id="c5c77-144">Этот шаблон не требует упаковки артефакты, конфигураций и фирменной символики активами в отдельные функции или надстроек.  Все, что может упакованный в одной надстройки.</span><span class="sxs-lookup"><span data-stu-id="c5c77-144">This pattern does not require packaging artifacts, configurations, and branding assets in separate features, or Add-ins.  Everything may be packaged in a single Add-in.</span></span>
- <span data-ttu-id="c5c77-145">При использовании этого шаблона для подготовки сайта обычно переопределить вне поля страницы, чтобы создать новый сайт.</span><span class="sxs-lookup"><span data-stu-id="c5c77-145">When you use this pattern for site provisioning you typically override the out of the box page to create a new site.</span></span>
- <span data-ttu-id="c5c77-146">Дополнительные сведения об этом шаблоне можно [Подготовки сайта (добавить в SharePoint набора команд)](site-provisioning-sharepoint-add-in.md)</span><span class="sxs-lookup"><span data-stu-id="c5c77-146">For more information about this pattern see the [Site Provisioning (SharePoint Add-in Recipe)](site-provisioning-sharepoint-add-in.md)</span></span>
- <span data-ttu-id="c5c77-147">Если вы хотите развернуть надстройки на сайте SharePoint, это можно сделать с помощью CSOM.</span><span class="sxs-lookup"><span data-stu-id="c5c77-147">If you wish to deploy Add-ins to a SharePoint site, this can be done via CSOM.</span></span>  <span data-ttu-id="c5c77-148">Ниже приведен пример которого надстройка Office с помощью файла манифеста .app загружает и устанавливает ее на сайте SharePoint.</span><span class="sxs-lookup"><span data-stu-id="c5c77-148">Here is an example which loads an Office Add-in via a .app manifest file and installs it in a SharePoint site.</span></span>

    ```
    //Create a FileStream object to access the Mail Office Add-in .app file 
    using (FileStream fsSource = new FileStream(System.Web.Hosting.HostingEnvironment.ApplicationPhysicalPath + "Innovation.Management.AFO.app",
    FileMode.Open, FileAccess.Read))
    {
        //Return the subweb where you want to install the Add-in
        var subweb = ctx.Web;
        ctx.Load(subweb);
        ctx.ExecuteQuery();

        //Load and Install the Add-in on the subweb
        AppInstance appInstance = subweb.LoadAndInstallApp(fsSource);
        ctx.Load(appInstance);
        ctx.ExecuteQuery();
    }
    ```

    + <span data-ttu-id="c5c77-149">Контрольное значение [Создание облачных размещенных строки из бизнес-приложения с помощью надстройки для Office, O365, Azure и WP8 (Todd Baginski, Майкл Sherman - конференции SharePoint 2014 г.)](https://channel9.msdn.com/Events/SharePoint-Conference/2014/SPC361) видео, чтобы увидеть, как этот подход был использован для установки надстройки Office на сайтах SharePoint После подготовки сайта.</span><span class="sxs-lookup"><span data-stu-id="c5c77-149">Watch the [Creating Cloud Hosted Line Of Business Applications with Add-ins for Office, O365, Azure, and WP8 (Todd Baginski, Michael Sherman - SharePoint Conference 2014)](https://channel9.msdn.com/Events/SharePoint-Conference/2014/SPC361) video to see how this approach was used to install Office Add-ins in SharePoint sites upon site provisioning.</span></span>
    + <span data-ttu-id="c5c77-150">Полный автоматизации можно только с помощью надстройки COM, иметь разрешение полного клиента, которые уже были надежные.</span><span class="sxs-lookup"><span data-stu-id="c5c77-150">Full automation is only possible with Add-ins that have full tenant permission that have already been trusted.</span></span>
        + <span data-ttu-id="c5c77-151">В разделе [Core.Sideloading (PnP образец O365)](https://github.com/SharePoint/PnP/tree/master/Samples/Core.SideLoading) в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="c5c77-151">See the [Core.Sideloading (O365 PnP Sample)](https://github.com/SharePoint/PnP/tree/master/Samples/Core.SideLoading) for an example.</span></span> 

<a name="related-links"></a><span data-ttu-id="c5c77-152">Ссылки по теме</span><span class="sxs-lookup"><span data-stu-id="c5c77-152">Related links</span></span>
=============
- [<span data-ttu-id="c5c77-153">Ассоциации возможности в SharePoint 2010 (статья блога MSDN)</span><span class="sxs-lookup"><span data-stu-id="c5c77-153">Feature Stapling In SharePoint 2010 (MSDN Blog Article)</span></span>](http://blogs.msdn.com/b/kunal_mukherjee/archive/2011/01/11/feature-stapling-in-sharepoint-2010.aspx)
- [<span data-ttu-id="c5c77-154">Самостоятельное подготовки сайта с помощью надстройки для SharePoint 2013 (блог MSDN)</span><span class="sxs-lookup"><span data-stu-id="c5c77-154">Self-Service Site Provisioning using add-ins for SharePoint 2013 (MSDN Blog)</span></span>](http://blogs.msdn.com/b/richard_dizeregas_blog/archive/2013/04/04/self-service-site-provisioning-using-apps-for-sharepoint-2013.aspx)
- [<span data-ttu-id="c5c77-155">Развертывание приложений SharePoint 2013 через «Ассоциация приложения» (блог статья MSDN - Richard DiZerega)</span><span class="sxs-lookup"><span data-stu-id="c5c77-155">SharePoint 2013 App Deployment through 'App Stapling' (MSDN Blog Article - Richard DiZerega)</span></span>](http://blogs.msdn.com/b/richard_dizeregas_blog/archive/2013/09/18/10399333.aspx)
- [<span data-ttu-id="c5c77-156">(Надстройка SharePoint набора команд) по подготовке сайта</span><span class="sxs-lookup"><span data-stu-id="c5c77-156">Site Provisioning (SharePoint Add-in Recipe)</span></span>](site-provisioning-sharepoint-add-in.md)
- [<span data-ttu-id="c5c77-157">Создание облачных размещенных бизнес-приложения с помощью надстройки для Office, O365, Azure и WP8 (Todd Baginski, Майкл Sherman - конференции SharePoint 2014 г.)</span><span class="sxs-lookup"><span data-stu-id="c5c77-157">Creating Cloud Hosted Line Of Business Applications with Add-ins for Office, O365, Azure, and WP8 (Todd Baginski, Michael Sherman - SharePoint Conference 2014)</span></span>](https://channel9.msdn.com/Events/SharePoint-Conference/2014/SPC361)
- <span data-ttu-id="c5c77-158">Руководств по [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Руководств")</span><span class="sxs-lookup"><span data-stu-id="c5c77-158">Guidance articles at [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Guidance Articles")</span></span>
- <span data-ttu-id="c5c77-159">Справочные материалы в библиотеке MSDN по [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "Справочные материалы в библиотеке MSDN")</span><span class="sxs-lookup"><span data-stu-id="c5c77-159">References in MSDN at [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "References in MSDN")</span></span>
- <span data-ttu-id="c5c77-160">Видеозаписи по [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "видео")</span><span class="sxs-lookup"><span data-stu-id="c5c77-160">Videos at [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")</span></span>

<a name="related-pnp-samples"></a><span data-ttu-id="c5c77-161">Примеры связанных с ними PnP</span><span class="sxs-lookup"><span data-stu-id="c5c77-161">Related PnP samples</span></span>
===================

- [<span data-ttu-id="c5c77-162">Provisioning.Cloud.Sync (O365 PnP образец)</span><span class="sxs-lookup"><span data-stu-id="c5c77-162">Provisioning.Cloud.Sync (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Solutions/Provisioning.Cloud.Sync)
- [<span data-ttu-id="c5c77-163">Provisioning.SubSiteCreationApp (O365 PnP образец)</span><span class="sxs-lookup"><span data-stu-id="c5c77-163">Provisioning.SubSiteCreationApp (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.SubSiteCreationApp)
- [<span data-ttu-id="c5c77-164">Provisioning.Services.SiteManager (O365 PnP образец)</span><span class="sxs-lookup"><span data-stu-id="c5c77-164">Provisioning.Services.SiteManager (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.Services.SiteManager)
- [<span data-ttu-id="c5c77-165">Provisioning.SiteCollectionCreation (O365 PnP образец)</span><span class="sxs-lookup"><span data-stu-id="c5c77-165">Provisioning.SiteCollectionCreation (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.SiteCollectionCreation)
- <span data-ttu-id="c5c77-166">Примеры и содержимое в [http://aka.ms/OfficeDevPnP](http://aka.ms/OfficeDevPnP)</span><span class="sxs-lookup"><span data-stu-id="c5c77-166">Samples and content at [http://aka.ms/OfficeDevPnP](http://aka.ms/OfficeDevPnP)</span></span>

<a name="applies-to"></a><span data-ttu-id="c5c77-167">Применимо к</span><span class="sxs-lookup"><span data-stu-id="c5c77-167">Applies to</span></span>
==========
- <span data-ttu-id="c5c77-168">Office 365 нескольких клиентов (MT)</span><span class="sxs-lookup"><span data-stu-id="c5c77-168">Office 365 Multi Tenant (MT)</span></span>
- <span data-ttu-id="c5c77-169">Office 365 выделенных (D)</span><span class="sxs-lookup"><span data-stu-id="c5c77-169">Office 365 Dedicated (D)</span></span>
- <span data-ttu-id="c5c77-170">SharePoint 2013 в локальной</span><span class="sxs-lookup"><span data-stu-id="c5c77-170">SharePoint 2013 on-premises</span></span>
