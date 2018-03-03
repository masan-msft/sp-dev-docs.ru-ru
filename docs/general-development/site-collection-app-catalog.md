---
title: "Использование каталога приложений в семействе веб-сайтов"
ms.date: 12/14/2017
ms.prod: sharepoint
ms.assetid: fdf7ecb1-9951-475b-b058-3285fba77b68
ms.openlocfilehash: 28d98344b8cab6334b86394aa190eca2cf32cb65
ms.sourcegitcommit: e157d51378190ddfed6394ba154ce66141c8ca33
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/19/2018
---
# <a name="use-the-site-collection-app-catalog"></a><span data-ttu-id="f146a-102">Использование каталога приложений в семействе веб-сайтов</span><span class="sxs-lookup"><span data-stu-id="f146a-102">Use the site collection app catalog</span></span>

<span data-ttu-id="f146a-103">_**Область применения:** Office 365_</span><span class="sxs-lookup"><span data-stu-id="f146a-103">_**Applies to:** Office 365_</span></span>

<span data-ttu-id="f146a-104">С помощью каталогов приложений в семействах веб-сайтов администраторы клиентов SharePoint могут рассредоточить управление и ограничить развертывание надстроек SharePoint и решений SharePoint Framework определенными сайтами.</span><span class="sxs-lookup"><span data-stu-id="f146a-104">Using site collection app catalogs, SharePoint tenant administrators can decentralize the management and scope the deployment of SharePoint add-ins and SharePoint Framework solutions to specific sites.</span></span>

## <a name="why-site-collection-app-catalogs"></a><span data-ttu-id="f146a-105">Зачем нужны каталоги приложений в семействах веб-сайтов</span><span class="sxs-lookup"><span data-stu-id="f146a-105">Why site collection app catalogs</span></span>

<span data-ttu-id="f146a-106">Ранее всеми надстройками и решениями SharePoint Framework необходимо было централизованно управлять в каталоге приложений клиента.</span><span class="sxs-lookup"><span data-stu-id="f146a-106">Previously, all add-ins and SharePoint Framework solutions had to be managed centrally in the tenant app catalog.</span></span> <span data-ttu-id="f146a-107">Администраторы клиентов могли делегировать доступ другим пользователям в организации, но развернутый пакет был виден во всех семействах веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="f146a-107">While tenant administrators could delegate the access to other people in the organization, a deployed package was visible on all site collections.</span></span> <span data-ttu-id="f146a-108">В SharePoint нет поддерживаемого способа развертывания надстроек и решений SharePoint Framework только на определенных сайтах.</span><span class="sxs-lookup"><span data-stu-id="f146a-108">SharePoint offered no supported way of deploying add-ins and SharePoint Framework solutions only to specific sites.</span></span>

<span data-ttu-id="f146a-109">С появлением каталогов приложений для семейств веб-сайтов у администраторов клиентов появилась возможность включать каталог на определенных сайтах.</span><span class="sxs-lookup"><span data-stu-id="f146a-109">With the introduction of site collection app catalogs, tenant administrators can enable app catalog on the specific sites.</span></span> <span data-ttu-id="f146a-110">После этого администраторы семейств веб-сайтов могут развертывать надстройки SharePoint и решения SharePoint Framework, которые будут доступны только в соответствующем семействе веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="f146a-110">Once enabled, site collection administrators can deploy SharePoint add-ins and SharePoint Framework solutions that will be available only in that particular site collection.</span></span>

<span data-ttu-id="f146a-111">На приведенной ниже схеме показано использование каталогов приложений в семействе веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="f146a-111">The following schema illustrates using site collection app catalogs:</span></span>

![Схема, иллюстрирующая понятие каталога приложений для семейства веб-сайтов](../images/site-collection-app-catalog-diagram.png)

<span data-ttu-id="f146a-113">В клиенте Office 365 есть клиентский каталог приложений.</span><span class="sxs-lookup"><span data-stu-id="f146a-113">In your Office 365 tenant you have a tenant app catalog.</span></span> <span data-ttu-id="f146a-114">Решения, развернутые в этом каталоге, можно установить в любом семействе веб-сайтов в клиенте.</span><span class="sxs-lookup"><span data-stu-id="f146a-114">Solutions deployed to this app catalog, can be installed in any site collection in the tenant.</span></span> <span data-ttu-id="f146a-115">Администраторы клиентов могут включать каталоги приложений в определенных семействах веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="f146a-115">Tenant administrators can choose to enable site collection app catalogs on specific site collections.</span></span> <span data-ttu-id="f146a-116">Решения, развернутые в таких каталогах, можно устанавливать только в соответствующем семействе веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="f146a-116">Solutions deployed to the site collection app catalogs can only be installed in that particular site collection.</span></span>

## <a name="supported-capabilities"></a><span data-ttu-id="f146a-117">Поддерживаемые возможности</span><span class="sxs-lookup"><span data-stu-id="f146a-117">Supported capabilities</span></span>

### <a name="support-for-both-sharepoint-add-ins-and-sharepoint-framework-packages"></a><span data-ttu-id="f146a-118">Поддержка надстроек SharePoint и пакетов SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="f146a-118">Support for both SharePoint add-ins and SharePoint Framework packages</span></span>

<span data-ttu-id="f146a-119">В каталогах приложений для семейств веб-сайтов, как и в каталоге приложений для клиента, можно развертывать не только надстройки SharePoint, но и решения SharePoint Framework (SPPKG-файлы).</span><span class="sxs-lookup"><span data-stu-id="f146a-119">In site collection app catalogs, just as in tenant app catalog, you can deploy both SharePoint add-ins and SharePoint Framework solutions (.sppkg).</span></span>

### <a name="including-assets-in-solution-packages"></a><span data-ttu-id="f146a-120">Включение ресурсов в пакеты решений</span><span class="sxs-lookup"><span data-stu-id="f146a-120">Including assets in solution packages</span></span>

<span data-ttu-id="f146a-121">Пакеты решений SharePoint Framework, содержащие ресурсы, можно развертывать в каталогах приложений для семейств веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="f146a-121">SharePoint Framework solution packages that contain assets, can be deployed to site collection app catalogs.</span></span> <span data-ttu-id="f146a-122">Включенные в них ресурсы развертываются в заранее настроенной библиотеке документов в том же семействе веб-сайтов, где находится каталог приложений.</span><span class="sxs-lookup"><span data-stu-id="f146a-122">Included assets will be deployed to a preconfigured document library in the same site collection as where the site collection app catalog is located.</span></span> <span data-ttu-id="f146a-123">Если настроена общедоступная сеть доставки содержимого Office 365, ресурсы будут предоставляться из нее.</span><span class="sxs-lookup"><span data-stu-id="f146a-123">If the Office 365 Public CDN is configured, assets will be served from the CDN.</span></span> <span data-ttu-id="f146a-124">В противном случае они будут поступать непосредственно из библиотеки документов.</span><span class="sxs-lookup"><span data-stu-id="f146a-124">Otherwise, assets will be served directly from the document library.</span></span>

> [!NOTE]
> <span data-ttu-id="f146a-125">В настоящее время развертывается исправление для корректной поддержки упаковывания ресурсов в каталогах приложений для семейств веб-сайтов. Оно должно стать доступным во всех клиентах до окончания 2017 г.</span><span class="sxs-lookup"><span data-stu-id="f146a-125">A bugfix for correctly supporting assets packaging in site collection app catalogs is currently being rolled out and should be available on all tenants before the end of the calendar year 2017.</span></span>

### <a name="tenant-scoped-deployment"></a><span data-ttu-id="f146a-126">Развертывание на уровне клиента</span><span class="sxs-lookup"><span data-stu-id="f146a-126">Tenant-scoped deployment</span></span>

<span data-ttu-id="f146a-127">При развертывании решений SharePoint Framework, поддерживающих развертывание на уровне клиента, в каталоге приложений для семейства веб-сайтов вам будет предложено сделать решение доступным на всех сайтах в организации.</span><span class="sxs-lookup"><span data-stu-id="f146a-127">When deploying SharePoint Framework solutions that support tenant-wide deployment to a site collection app catalog, you will be prompted if you want to make this solution available to all sites in the organization.</span></span> <span data-ttu-id="f146a-128">Несмотря на такую формулировку, при установке этого флажка решение сразу станет доступным **только в том семействе веб-сайтов, где находится каталог приложений**.</span><span class="sxs-lookup"><span data-stu-id="f146a-128">Despite the wording, if you check this box, the solution will be available immediately **only in the same site collection as where the app catalog is**.</span></span> <span data-ttu-id="f146a-129">Другие семейства веб-сайтов в организациях не смогут использовать решение.</span><span class="sxs-lookup"><span data-stu-id="f146a-129">Other site collections in your organizations will not be able to use the solution.</span></span> <span data-ttu-id="f146a-130">Если не включить этот параметр, потребуется явно установить решение на сайте, прежде чем использовать его.</span><span class="sxs-lookup"><span data-stu-id="f146a-130">If you don't check this option, you will have to explicitly install the solution in your site, before you will be able to use it.</span></span>

## <a name="current-limitations"></a><span data-ttu-id="f146a-131">Текущие ограничения</span><span class="sxs-lookup"><span data-stu-id="f146a-131">Current limitations</span></span>

### <a name="application-lifecycle-management-alm-apis-are-not-yet-supported"></a><span data-ttu-id="f146a-132">API управления жизненным циклом приложений (ALM) пока что не поддерживаются</span><span class="sxs-lookup"><span data-stu-id="f146a-132">Application Lifecycle Management (ALM) APIs are not yet supported</span></span>

<span data-ttu-id="f146a-133">В данный момент невозможно использовать недавно выпущенные API ALM для управления жизненным циклом решений в каталогах приложений для семейств веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="f146a-133">At this moment, it's not possible to use the recently released ALM APIs to manage the lifecycle of solutions in site collection app catalogs.</span></span> <span data-ttu-id="f146a-134">Эта функция находится на стадии разработки. Она должна появиться в начале 2018 г.</span><span class="sxs-lookup"><span data-stu-id="f146a-134">This is currently being worked on and should be available in the early 2018.</span></span>

## <a name="configure-and-manage-site-collection-app-catalogs"></a><span data-ttu-id="f146a-135">Настройка каталогов приложений для семейств веб-сайтов и управление ими</span><span class="sxs-lookup"><span data-stu-id="f146a-135">Configure and manage site collection app catalogs</span></span>

<span data-ttu-id="f146a-136">Вы можете настраивать каталоги приложений для семейств веб-сайтов и управлять ими с помощью командной консоли SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="f146a-136">You can configure and manage site collection app catalogs using the SharePoint Online Management Shell.</span></span>

> [!NOTE]
> <span data-ttu-id="f146a-137">Чтобы управлять каталогами приложений в клиенте, установите [командную консоль SharePoint Online](https://www.microsoft.com/en-us/download/details.aspx?id=35588), выпущенную в ноябре 2017 г., или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="f146a-137">Before you can manage site collection app catalogs in your tenant, ensure that you have installed [SharePoint Online Management Shell](https://www.microsoft.com/en-us/download/details.aspx?id=35588) from November '17 or newer.</span></span>

### <a name="create-a-site-collection-app-catalog"></a><span data-ttu-id="f146a-138">Создание каталога приложений в семействе веб-сайтов</span><span class="sxs-lookup"><span data-stu-id="f146a-138">Create a site collection app catalog</span></span>

> [!NOTE]
> <span data-ttu-id="f146a-139">Прежде чем запускать приведенный ниже скрипт, подключитесь к клиенту SharePoint Online с помощью командлета `Connect-SPOService`.</span><span class="sxs-lookup"><span data-stu-id="f146a-139">Before running the following script, connect to your SharePoint Online tenant using the `Connect-SPOService` cmdlet.</span></span> <span data-ttu-id="f146a-140">Кроме того, убедитесь, что в клиенте создан каталог приложений.</span><span class="sxs-lookup"><span data-stu-id="f146a-140">Also ensure, that you have a tenant app catalog created in your tenant.</span></span> <span data-ttu-id="f146a-141">В противном случае командлет вернет следующую ошибку:</span><span class="sxs-lookup"><span data-stu-id="f146a-141">If you don't, the cmdlet will fail with the following error:</span></span>
> ```text
> Cannot invoke method or retrieve property from null object. Object returned by the
> following call stack is null. "TenantAppCatalog
> RootWeb
> GetSiteByUrl
> new Microsoft.Online.SharePoint.TenantAdministration.Tenant()
> "
> ```

<span data-ttu-id="f146a-142">Чтобы создать каталог приложений в семействе веб-сайтов, используйте командлет `Add-SPOSiteCollectionAppCatalog`, передав имя нужного семейства веб-сайтов в параметре `-Site`.</span><span class="sxs-lookup"><span data-stu-id="f146a-142">To create a site collection app catalog, use the `Add-SPOSiteCollectionAppCatalog` cmdlet passing the site collection where the app catalog should be created as the `-Site` parameter.</span></span>

```powershell
# get a reference to the site collection where the
# site collection app catalog should be created
$site = Get-SPOSite https://contoso.sharepoint.com/sites/marketing

# create site collection app catalog
Add-SPOSiteCollectionAppCatalog -Site $site
```

<span data-ttu-id="f146a-143">После выполнения скрипта в семейство веб-сайтов будет добавлена библиотека **Приложения для SharePoint**, где можно будет развертывать надстройки SharePoint и решения SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="f146a-143">After executing this script, the **Apps for SharePoint** library will be added to your site collection where you will be able to deploy SharePoint add-ins and SharePoint Framework solutions.</span></span>

### <a name="disable-the-site-collection-app-catalog"></a><span data-ttu-id="f146a-144">Отключение каталога приложений в семействе веб-сайтов</span><span class="sxs-lookup"><span data-stu-id="f146a-144">Disable the site collection app catalog</span></span>

> [!NOTE]
> <span data-ttu-id="f146a-145">Прежде чем запускать приведенный ниже скрипт, подключитесь к клиенту SharePoint Online с помощью командлета `Connect-SPOService`.</span><span class="sxs-lookup"><span data-stu-id="f146a-145">Before running the following script, connect to your SharePoint Online tenant using the `Connect-SPOService` cmdlet.</span></span>

<span data-ttu-id="f146a-146">Чтобы отключить каталог приложений в семействе веб-сайтов, используйте командлет `Remove-SPOSiteCollectionAppCatalog`, передав имя нужного семейства веб-сайтов в параметре `-Site`.</span><span class="sxs-lookup"><span data-stu-id="f146a-146">To disable the site collection app catalog in your site collection, use the `Remove-SPOSiteCollectionAppCatalog` cmdlet passing the site collection where the app catalog should be disabled as the `-Site` parameter.</span></span> <span data-ttu-id="f146a-147">Кроме того, если вы знаете ИД семейства веб-сайтов, можно использовать командлет `Remove-SPOSiteCollectionAppCatalogById`.</span><span class="sxs-lookup"><span data-stu-id="f146a-147">Alternatively, if you have your site collection's ID, you can use the `Remove-SPOSiteCollectionAppCatalogById` cmdlet instead.</span></span>

> [!NOTE]
> <span data-ttu-id="f146a-148">Несмотря на их названия, командлеты `Remove-SPOSiteCollectionAppCatalog` и `Remove-SPOSiteCollectionAppCatalogById` не удаляют каталог приложений из семейства веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="f146a-148">Despite the naming, the `Remove-SPOSiteCollectionAppCatalog` and `Remove-SPOSiteCollectionAppCatalogById` cmdlets don't remove the site collection app catalog from the site collection.</span></span> <span data-ttu-id="f146a-149">Они просто отключают его, чтобы в нем нельзя было развертывать решения и использовать их.</span><span class="sxs-lookup"><span data-stu-id="f146a-149">Instead, they disable it so that it's not possible to deploy or use any solutions deployed in it.</span></span>

```powershell
# get a reference to the site collection in which
# the site collection app catalog should be disabled
$site = Get-SPOSite https://contoso.sharepoint.com/sites/marketing

# disable the site collection app catalog
Remove-SPOSiteCollectionAppCatalog -Site $site
```

<span data-ttu-id="f146a-150">После выполнения этого скрипта библиотека **Приложения для SharePoint** по-прежнему будет видна в семействе веб-сайтов, но в ней будет невозможно развертывать решения и использовать их.</span><span class="sxs-lookup"><span data-stu-id="f146a-150">After executing this script, the **Apps for SharePoint** library will be still visible in your site collection, but you will not be able to deploy or use any solutions deployed in it.</span></span>

## <a name="considerations"></a><span data-ttu-id="f146a-151">Замечания</span><span class="sxs-lookup"><span data-stu-id="f146a-151">Considerations</span></span>

### <a name="governance"></a><span data-ttu-id="f146a-152">Управление</span><span class="sxs-lookup"><span data-stu-id="f146a-152">Governance</span></span>

<span data-ttu-id="f146a-153">В настоящее время невозможно получить список всех семейств веб-сайтов в клиенте, для которых включен каталог приложений.</span><span class="sxs-lookup"><span data-stu-id="f146a-153">Currently, it's not possible to list all site collections in the tenant that have the site collection app catalog enabled.</span></span>

### <a name="security"></a><span data-ttu-id="f146a-154">Безопасность</span><span class="sxs-lookup"><span data-stu-id="f146a-154">Security</span></span>

<span data-ttu-id="f146a-155">Перед развертыванием решений в каталогах приложений для семейств веб-сайтов администраторы этих семейств должны проверять соответствие решений политикам организации.</span><span class="sxs-lookup"><span data-stu-id="f146a-155">Before deploying solutions to site collection app catalogs, site collection administrators should verify that these solutions meet organizational policies.</span></span> <span data-ttu-id="f146a-156">Решения, установленные в каталогах приложений для семейств веб-сайтов, можно использовать только в соответствующих семействах, но они могут получать доступ к ресурсам с других сайтов клиента, поэтому администраторам следует убедиться, что развертываемые решения работают надлежащим образом.</span><span class="sxs-lookup"><span data-stu-id="f146a-156">Although solutions installed in site collection app catalogs can only be used in these particular site collections, they can potentially access resources from other sites in the tenant so administrators should ensure that the solutions they are about to deploy work as intended.</span></span>

## <a name="see-also"></a><span data-ttu-id="f146a-157">См. также</span><span class="sxs-lookup"><span data-stu-id="f146a-157">See also</span></span>

- [<span data-ttu-id="f146a-158">Управление каталогом приложений для семейства веб-сайтов</span><span class="sxs-lookup"><span data-stu-id="f146a-158">Manage the Site Collection App Catalog</span></span>](https://support.office.com/ru-RU/article/Manage-the-Site-Collection-App-Catalog-928b9b61-a9de-4563-a7d1-6231aa9d4d19)