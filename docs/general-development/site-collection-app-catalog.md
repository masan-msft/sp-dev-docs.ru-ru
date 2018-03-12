---
title: "Использование каталога приложений в семействе веб-сайтов"
ms.date: 12/14/2017
ms.prod: sharepoint
ms.assetid: fdf7ecb1-9951-475b-b058-3285fba77b68
ms.openlocfilehash: 52c1eec380752cbf2bee7879b06a420ae66c52be
ms.sourcegitcommit: 4e65e89f3ad8ef1d953e2fdd04d7ab5c0e7df174
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/27/2018
---
# <a name="use-the-site-collection-app-catalog"></a><span data-ttu-id="47db2-102">Использование каталога приложений в семействе веб-сайтов</span><span class="sxs-lookup"><span data-stu-id="47db2-102">Use the site collection app catalog</span></span>

<span data-ttu-id="47db2-103">_**Область применения:** Office 365_</span><span class="sxs-lookup"><span data-stu-id="47db2-103">_**Applies to:** Office 365_</span></span>

<span data-ttu-id="47db2-104">С помощью каталогов приложений в семействах веб-сайтов администраторы клиентов SharePoint могут рассредоточить управление и ограничить развертывание надстроек SharePoint и решений SharePoint Framework определенными сайтами.</span><span class="sxs-lookup"><span data-stu-id="47db2-104">Using site collection app catalogs, SharePoint tenant administrators can decentralize the management and scope the deployment of SharePoint add-ins and SharePoint Framework solutions to specific sites.</span></span>

## <a name="why-site-collection-app-catalogs"></a><span data-ttu-id="47db2-105">Зачем нужны каталоги приложений в семействах веб-сайтов</span><span class="sxs-lookup"><span data-stu-id="47db2-105">Why site collection app catalogs</span></span>

<span data-ttu-id="47db2-106">Ранее всеми надстройками и решениями SharePoint Framework необходимо было централизованно управлять в каталоге приложений клиента.</span><span class="sxs-lookup"><span data-stu-id="47db2-106">Previously, all add-ins and SharePoint Framework solutions had to be managed centrally in the tenant app catalog.</span></span> <span data-ttu-id="47db2-107">Администраторы клиентов могли делегировать доступ другим пользователям в организации, но развернутый пакет был виден во всех семействах веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="47db2-107">While tenant administrators could delegate the access to other people in the organization, a deployed package was visible on all site collections.</span></span> <span data-ttu-id="47db2-108">В SharePoint нет поддерживаемого способа развертывания надстроек и решений SharePoint Framework только на определенных сайтах.</span><span class="sxs-lookup"><span data-stu-id="47db2-108">SharePoint offered no supported way of deploying add-ins and SharePoint Framework solutions only to specific sites.</span></span>

<span data-ttu-id="47db2-109">С появлением каталогов приложений для семейств веб-сайтов у администраторов клиентов появилась возможность включать каталог на определенных сайтах.</span><span class="sxs-lookup"><span data-stu-id="47db2-109">With the introduction of site collection app catalogs, tenant administrators can enable app catalog on the specific sites.</span></span> <span data-ttu-id="47db2-110">После этого администраторы семейств веб-сайтов могут развертывать надстройки SharePoint и решения SharePoint Framework, которые будут доступны только в соответствующем семействе веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="47db2-110">Once enabled, site collection administrators can deploy SharePoint add-ins and SharePoint Framework solutions that will be available only in that particular site collection.</span></span>

<span data-ttu-id="47db2-111">На приведенной ниже схеме показано использование каталогов приложений в семействе веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="47db2-111">The following schema illustrates using site collection app catalogs:</span></span>

![Схема, иллюстрирующая понятие каталога приложений для семейства веб-сайтов](../images/site-collection-app-catalog-diagram.png)

<span data-ttu-id="47db2-113">В клиенте Office 365 есть клиентский каталог приложений.</span><span class="sxs-lookup"><span data-stu-id="47db2-113">In your Office 365 tenant you have a tenant app catalog.</span></span> <span data-ttu-id="47db2-114">Решения, развернутые в этом каталоге, можно установить в любом семействе веб-сайтов в клиенте.</span><span class="sxs-lookup"><span data-stu-id="47db2-114">Solutions deployed to this app catalog, can be installed in any site collection in the tenant.</span></span> <span data-ttu-id="47db2-115">Администраторы клиентов могут включать каталоги приложений в определенных семействах веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="47db2-115">Tenant administrators can choose to enable site collection app catalogs on specific site collections.</span></span> <span data-ttu-id="47db2-116">Решения, развернутые в таких каталогах, можно устанавливать только в соответствующем семействе веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="47db2-116">Solutions deployed to the site collection app catalogs can only be installed in that particular site collection.</span></span>

## <a name="supported-capabilities"></a><span data-ttu-id="47db2-117">Поддерживаемые возможности</span><span class="sxs-lookup"><span data-stu-id="47db2-117">Supported capabilities</span></span>

### <a name="support-for-both-sharepoint-add-ins-and-sharepoint-framework-packages"></a><span data-ttu-id="47db2-118">Поддержка надстроек SharePoint и пакетов SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="47db2-118">Support for both SharePoint add-ins and SharePoint Framework packages</span></span>

<span data-ttu-id="47db2-119">В каталогах приложений для семейств веб-сайтов, как и в каталоге приложений для клиента, можно развертывать не только надстройки SharePoint, но и решения SharePoint Framework (SPPKG-файлы).</span><span class="sxs-lookup"><span data-stu-id="47db2-119">In site collection app catalogs, just as in tenant app catalog, you can deploy both SharePoint add-ins and SharePoint Framework solutions (.sppkg).</span></span>

### <a name="including-assets-in-solution-packages"></a><span data-ttu-id="47db2-120">Включение ресурсов в пакеты решений</span><span class="sxs-lookup"><span data-stu-id="47db2-120">Including assets in solution packages</span></span>

<span data-ttu-id="47db2-121">Пакеты решений SharePoint Framework, содержащие ресурсы, можно развертывать в каталогах приложений для семейств веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="47db2-121">SharePoint Framework solution packages that contain assets, can be deployed to site collection app catalogs.</span></span> <span data-ttu-id="47db2-122">Включенные в них ресурсы развертываются в заранее настроенной библиотеке документов в том же семействе веб-сайтов, где находится каталог приложений.</span><span class="sxs-lookup"><span data-stu-id="47db2-122">Included assets will be deployed to a preconfigured document library in the same site collection as where the site collection app catalog is located.</span></span> <span data-ttu-id="47db2-123">Если настроена общедоступная сеть доставки содержимого Office 365, ресурсы будут предоставляться из нее.</span><span class="sxs-lookup"><span data-stu-id="47db2-123">If the Office 365 Public CDN is configured, assets will be served from the CDN.</span></span> <span data-ttu-id="47db2-124">В противном случае они будут поступать непосредственно из библиотеки документов.</span><span class="sxs-lookup"><span data-stu-id="47db2-124">Otherwise, assets will be served directly from the document library.</span></span>

> [!NOTE]
> <span data-ttu-id="47db2-125">В настоящее время развертывается исправление для корректной поддержки упаковывания ресурсов в каталогах приложений для семейств веб-сайтов. Оно должно стать доступным во всех клиентах до окончания 2017 г.</span><span class="sxs-lookup"><span data-stu-id="47db2-125">A bugfix for correctly supporting assets packaging in site collection app catalogs is currently being rolled out and should be available on all tenants before the end of the calendar year 2017.</span></span>

### <a name="tenant-scoped-deployment"></a><span data-ttu-id="47db2-126">Развертывание на уровне клиента</span><span class="sxs-lookup"><span data-stu-id="47db2-126">Tenant-scoped deployment</span></span>

<span data-ttu-id="47db2-127">При развертывании решений SharePoint Framework, поддерживающих развертывание на уровне клиента, в каталоге приложений для семейства веб-сайтов вам будет предложено сделать решение доступным на всех сайтах в организации.</span><span class="sxs-lookup"><span data-stu-id="47db2-127">When deploying SharePoint Framework solutions that support tenant-wide deployment to a site collection app catalog, you will be prompted if you want to make this solution available to all sites in the organization.</span></span> <span data-ttu-id="47db2-128">Несмотря на такую формулировку, при установке этого флажка решение сразу станет доступным **только в том семействе веб-сайтов, где находится каталог приложений**.</span><span class="sxs-lookup"><span data-stu-id="47db2-128">Despite the wording, if you check this box, the solution will be available immediately **only in the same site collection as where the app catalog is**.</span></span> <span data-ttu-id="47db2-129">Другие семейства веб-сайтов в организациях не смогут использовать решение.</span><span class="sxs-lookup"><span data-stu-id="47db2-129">Other site collections in your organizations will not be able to use the solution.</span></span> <span data-ttu-id="47db2-130">Если не включить этот параметр, потребуется явно установить решение на сайте, прежде чем использовать его.</span><span class="sxs-lookup"><span data-stu-id="47db2-130">If you don't check this option, you will have to explicitly install the solution in your site, before you will be able to use it.</span></span>

## <a name="current-limitations"></a><span data-ttu-id="47db2-131">Текущие ограничения</span><span class="sxs-lookup"><span data-stu-id="47db2-131">Current limitations</span></span>

### <a name="application-lifecycle-management-alm-apis-are-not-yet-supported"></a><span data-ttu-id="47db2-132">API управления жизненным циклом приложений (ALM) пока что не поддерживаются</span><span class="sxs-lookup"><span data-stu-id="47db2-132">Application Lifecycle Management (ALM) APIs are not yet supported</span></span>

<span data-ttu-id="47db2-133">В данный момент невозможно использовать недавно выпущенные API ALM для управления жизненным циклом решений в каталогах приложений для семейств веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="47db2-133">At this moment, it's not possible to use the recently released ALM APIs to manage the lifecycle of solutions in site collection app catalogs.</span></span> <span data-ttu-id="47db2-134">Эта функция находится на стадии разработки. Она должна появиться в начале 2018 г.</span><span class="sxs-lookup"><span data-stu-id="47db2-134">This is currently being worked on and should be available in the early 2018.</span></span>

## <a name="configure-and-manage-site-collection-app-catalogs"></a><span data-ttu-id="47db2-135">Настройка каталогов приложений для семейств веб-сайтов и управление ими</span><span class="sxs-lookup"><span data-stu-id="47db2-135">Configure and manage site collection app catalogs</span></span>

<span data-ttu-id="47db2-136">Вы можете настраивать каталоги приложений для семейств веб-сайтов и управлять ими с помощью командной консоли SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="47db2-136">You can configure and manage site collection app catalogs using the SharePoint Online Management Shell.</span></span>

> [!NOTE]
> <span data-ttu-id="47db2-137">Чтобы управлять каталогами приложений в семействе веб-сайтов в клиенте, установите [командную консоль SharePoint Online](https://www.microsoft.com/en-us/download/details.aspx?id=35588), выпущенную в ноябре 2017 г., или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="47db2-137">Before you can manage site collection app catalogs in your tenant, ensure that you have installed [SharePoint Online Management Shell](https://www.microsoft.com/en-us/download/details.aspx?id=35588) from November '17 or newer.</span></span>

<span data-ttu-id="47db2-138">Вы также можете управлять каталогами приложений в семействе-веб-сайтов в SharePoint с помощью [Office 365 CLI](https://sharepoint.github.io/office365-cli?utm_source=msft_docs&utm_medium=page&utm_campaign=Use+the+site+collection+app+catalog).</span><span class="sxs-lookup"><span data-stu-id="47db2-138">Alternatively, you can use the [Office 365 CLI](https://sharepoint.github.io/office365-cli?utm_source=msft_docs&utm_medium=page&utm_campaign=Use+the+site+collection+app+catalog) to manage your SharePoint site collection app catalogs.</span></span> <span data-ttu-id="47db2-139">Office 365 CLI — это межплатформенный интерфейс командной строки, который можно использовать на любой платформе, в том числе Windows, MacOS и Linux.</span><span class="sxs-lookup"><span data-stu-id="47db2-139">The Office 365 CLI is a cross-platform command line interface that can be used on any platform, including Windows, MacOS and Linux.</span></span>

### <a name="create-a-site-collection-app-catalog"></a><span data-ttu-id="47db2-140">Создание каталога приложений в семействе веб-сайтов</span><span class="sxs-lookup"><span data-stu-id="47db2-140">Create a site collection app catalog</span></span>

> [!NOTE]
> <span data-ttu-id="47db2-141">Прежде чем запускать приведенный ниже скрипт, подключитесь к клиенту SharePoint Online, используя командлет `Connect-SPOService` в оболочке PowerShell.</span><span class="sxs-lookup"><span data-stu-id="47db2-141">Before running the following script, connect to your SharePoint Online tenant using the `Connect-SPOService` cmdlet.</span></span> <span data-ttu-id="47db2-142">Кроме того, убедитесь, что в клиенте создан каталог приложений.</span><span class="sxs-lookup"><span data-stu-id="47db2-142">Also ensure, that you have a tenant app catalog created in your tenant.</span></span> <span data-ttu-id="47db2-143">В противном случае командлет вернет следующую ошибку:</span><span class="sxs-lookup"><span data-stu-id="47db2-143">If you don't, the cmdlet will fail with the following error:</span></span>
> ```text
> Cannot invoke method or retrieve property from null object. Object returned by the
> following call stack is null. "TenantAppCatalog
> RootWeb
> GetSiteByUrl
> new Microsoft.Online.SharePoint.TenantAdministration.Tenant()
> "
> ```
>
> <span data-ttu-id="47db2-144">Если вы используете Office 365 CLI, сначала подключитесь к клиенту с помощью команды `spo connect`.</span><span class="sxs-lookup"><span data-stu-id="47db2-144">Alternatively, if you are using the Office 365 CLI, you must first connect to your tenant using the `spo connect` command.</span></span>

<span data-ttu-id="47db2-145">Чтобы создать каталог приложений в семействе веб-сайтов, используйте командлет `Add-SPOSiteCollectionAppCatalog`, передав имя нужного семейства веб-сайтов в параметре `-Site`.</span><span class="sxs-lookup"><span data-stu-id="47db2-145">To create a site collection app catalog, use the `Add-SPOSiteCollectionAppCatalog` cmdlet passing the site collection where the app catalog should be created as the `-Site` parameter.</span></span>

```powershell
# get a reference to the site collection where the
# site collection app catalog should be created
$site = Get-SPOSite https://contoso.sharepoint.com/sites/marketing

# create site collection app catalog
Add-SPOSiteCollectionAppCatalog -Site $site
```

<span data-ttu-id="47db2-146">Кроме того, при работе с Office 365 CLI можно использовать команду `spo site appcatalog add`</span><span class="sxs-lookup"><span data-stu-id="47db2-146">Alternatively, use the `spo site appcatalog add` command if you are using the Office 365 CLI</span></span>

```shell
spo site appcatalog add --url https://contoso.sharepoint.com/sites/marketing
```

<span data-ttu-id="47db2-147">После выполнения скрипта в семейство веб-сайтов будет добавлена библиотека **Приложения для SharePoint**, где можно будет развертывать надстройки SharePoint и решения SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="47db2-147">After executing this script, the **Apps for SharePoint** library will be added to your site collection where you will be able to deploy SharePoint add-ins and SharePoint Framework solutions.</span></span>

### <a name="disable-the-site-collection-app-catalog"></a><span data-ttu-id="47db2-148">Отключение каталога приложений в семействе веб-сайтов</span><span class="sxs-lookup"><span data-stu-id="47db2-148">Disable the site collection app catalog</span></span>

> [!NOTE]
> <span data-ttu-id="47db2-149">Прежде чем запускать приведенный ниже скрипт, подключитесь к клиенту SharePoint Online, используя командлет `Connect-SPOService` в оболочке PowerShell, или команду `spo connect` при работе с Office 365 CLI.</span><span class="sxs-lookup"><span data-stu-id="47db2-149">Before running the following script, connect to your SharePoint Online tenant using the `Connect-SPOService` cmdlet for the SharePoint Online Powershell or `spo connect` command for the Office 365 CLI.</span></span>

<span data-ttu-id="47db2-150">Чтобы отключить каталог приложений в семействе веб-сайтов, используйте командлет `Remove-SPOSiteCollectionAppCatalog`, передав имя нужного семейства веб-сайтов в параметре `-Site`.</span><span class="sxs-lookup"><span data-stu-id="47db2-150">To disable the site collection app catalog in your site collection, use the `Remove-SPOSiteCollectionAppCatalog` cmdlet passing the site collection where the app catalog should be disabled as the `-Site` parameter.</span></span> <span data-ttu-id="47db2-151">Кроме того, если вы знаете ИД семейства веб-сайтов, можно использовать командлет `Remove-SPOSiteCollectionAppCatalogById`.</span><span class="sxs-lookup"><span data-stu-id="47db2-151">Alternatively, if you have your site collection's ID, you can use the `Remove-SPOSiteCollectionAppCatalogById` cmdlet instead.</span></span>

> [!NOTE]
> <span data-ttu-id="47db2-152">Несмотря на их названия, командлеты `Remove-SPOSiteCollectionAppCatalog` и `Remove-SPOSiteCollectionAppCatalogById` не удаляют каталог приложений из семейства веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="47db2-152">Despite the naming, the `Remove-SPOSiteCollectionAppCatalog` and `Remove-SPOSiteCollectionAppCatalogById` cmdlets don't remove the site collection app catalog from the site collection.</span></span> <span data-ttu-id="47db2-153">Они просто отключают его, чтобы в нем нельзя было развертывать решения и использовать их.</span><span class="sxs-lookup"><span data-stu-id="47db2-153">Instead, they disable it so that it's not possible to deploy or use any solutions deployed in it.</span></span>

```powershell
# get a reference to the site collection in which
# the site collection app catalog should be disabled
$site = Get-SPOSite https://contoso.sharepoint.com/sites/marketing

# disable the site collection app catalog
Remove-SPOSiteCollectionAppCatalog -Site $site
```

<span data-ttu-id="47db2-154">Кроме того, при работе с Office 365 CLI можно использовать команду `spo site appcatalog remove`</span><span class="sxs-lookup"><span data-stu-id="47db2-154">Alternatively, use the `spo site appcatalog remove` command if you are using the Office 365 CLI</span></span>

```shell
spo site appcatalog remove --url https://contoso.sharepoint.com/sites/marketing
```

<span data-ttu-id="47db2-155">После выполнения этого скрипта библиотека **Приложения для SharePoint** по-прежнему будет видна в семействе веб-сайтов, но в ней будет невозможно развертывать решения и использовать их.</span><span class="sxs-lookup"><span data-stu-id="47db2-155">After executing this script, the **Apps for SharePoint** library will be still visible in your site collection, but you will not be able to deploy or use any solutions deployed in it.</span></span>

## <a name="considerations"></a><span data-ttu-id="47db2-156">Замечания</span><span class="sxs-lookup"><span data-stu-id="47db2-156">Considerations</span></span>

### <a name="governance"></a><span data-ttu-id="47db2-157">Управление</span><span class="sxs-lookup"><span data-stu-id="47db2-157">Governance</span></span>

<span data-ttu-id="47db2-158">В настоящее время невозможно получить список всех семейств веб-сайтов в клиенте, для которых включен каталог приложений.</span><span class="sxs-lookup"><span data-stu-id="47db2-158">Currently, it's not possible to list all site collections in the tenant that have the site collection app catalog enabled.</span></span>

### <a name="security"></a><span data-ttu-id="47db2-159">Безопасность</span><span class="sxs-lookup"><span data-stu-id="47db2-159">Security</span></span>

<span data-ttu-id="47db2-160">Перед развертыванием решений в каталогах приложений для семейств веб-сайтов администраторы этих семейств должны проверять соответствие решений политикам организации.</span><span class="sxs-lookup"><span data-stu-id="47db2-160">Before deploying solutions to site collection app catalogs, site collection administrators should verify that these solutions meet organizational policies.</span></span> <span data-ttu-id="47db2-161">Решения, установленные в каталогах приложений для семейств веб-сайтов, можно использовать только в соответствующих семействах, но они могут получать доступ к ресурсам с других сайтов клиента, поэтому администраторам следует убедиться, что развертываемые решения работают надлежащим образом.</span><span class="sxs-lookup"><span data-stu-id="47db2-161">Although solutions installed in site collection app catalogs can only be used in these particular site collections, they can potentially access resources from other sites in the tenant so administrators should ensure that the solutions they are about to deploy work as intended.</span></span>

## <a name="see-also"></a><span data-ttu-id="47db2-162">См. также</span><span class="sxs-lookup"><span data-stu-id="47db2-162">See also</span></span>

- [<span data-ttu-id="47db2-163">Управление каталогом приложений для семейства веб-сайтов</span><span class="sxs-lookup"><span data-stu-id="47db2-163">Manage the Site Collection App Catalog</span></span>](https://support.office.com/ru-RU/article/Manage-the-Site-Collection-App-Catalog-928b9b61-a9de-4563-a7d1-6231aa9d4d19)
- [<span data-ttu-id="47db2-164">Office 365 CLI</span><span class="sxs-lookup"><span data-stu-id="47db2-164">Office 365 CLI</span></span>](https://sharepoint.github.io/office365-cli?utm_source=msft_docs&utm_medium=page&utm_campaign=Use+the+site+collection+app+catalog)

