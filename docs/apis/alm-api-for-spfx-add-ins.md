---
title: "API управления жизненным циклом приложений (ALM)"
description: "API ALM представляют собой простые API для управления развертыванием решений и надстроек SharePoint Framework в клиенте."
ms.date: 02/08/2018
ms.prod: sharepoint
ms.assetid: fdf7ecb2-8851-425b-b058-3285fba77b68
ms.openlocfilehash: a0980afd0679398c60e3f5e9ef8ae158d5b719ee
ms.sourcegitcommit: e157d51378190ddfed6394ba154ce66141c8ca33
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/19/2018
---
# <a name="application-lifecycle-management-alm-apis"></a><span data-ttu-id="8a784-103">API управления жизненным циклом приложений (ALM)</span><span class="sxs-lookup"><span data-stu-id="8a784-103">Application Lifecycle Management (ALM) APIs</span></span>  

<span data-ttu-id="8a784-104">API ALM представляют собой простые API для управления развертыванием решений и надстроек SharePoint Framework в клиенте.</span><span class="sxs-lookup"><span data-stu-id="8a784-104">ALM APIs are providing simple APIs to manage deployment of your SharePoint Framework solutions and add-ins cross your tenant.</span></span> <span data-ttu-id="8a784-105">Эти API поддерживают указанные ниже возможности.</span><span class="sxs-lookup"><span data-stu-id="8a784-105">ALM APIs support following capabilities.</span></span>

- <span data-ttu-id="8a784-106">Добавление решения SharePoint Framework или надстройки SharePoint в каталог приложений клиента.</span><span class="sxs-lookup"><span data-stu-id="8a784-106">Add SharePoint Framework solution or SharePoint add-in to tenant app catalog</span></span>
- <span data-ttu-id="8a784-107">Обеспечение доступности решения SharePoint Framework или надстройки SharePoint для установки в каталоге приложений клиента.</span><span class="sxs-lookup"><span data-stu-id="8a784-107">Enable SharePoint Framework solution or SharePoint add-in to be available for installation in tenant app catalog</span></span>
- <span data-ttu-id="8a784-108">Отключение возможности установки решения SharePoint Framework или надстройки SharePoint в каталоге приложений клиента.</span><span class="sxs-lookup"><span data-stu-id="8a784-108">Disable SharePoint Framework solution or SharePoint add-in not to be available for installation in tenant app catalog</span></span>
- <span data-ttu-id="8a784-109">Установка решения SharePoint Framework или надстройки SharePoint из каталога приложений клиента на сайте.</span><span class="sxs-lookup"><span data-stu-id="8a784-109">Install SharePoint Framework solution or SharePoint add-in from tenant app catalog to a site</span></span>
- <span data-ttu-id="8a784-110">Обновление решения SharePoint Framework или надстройки SharePoint на сайте до более поздней версии, доступной в каталоге приложений клиента.</span><span class="sxs-lookup"><span data-stu-id="8a784-110">Upgrade SharePoint Framework solution or SharePoint add-in to a site, which has a newer version available in the tenant app catalog</span></span>
- <span data-ttu-id="8a784-111">Удаление решения SharePoint Framework или надстройки SharePoint с сайта.</span><span class="sxs-lookup"><span data-stu-id="8a784-111">Uninstall SharePoint Framework solution or SharePoint add-in from the site</span></span>

<span data-ttu-id="8a784-112">С помощью API ALM можно выполнять те же операции, что и в пользовательском интерфейсе.</span><span class="sxs-lookup"><span data-stu-id="8a784-112">ALM APIs can be used to perform exactly the same operations which are available from UI perspective.</span></span> <span data-ttu-id="8a784-113">При использовании этих API выполняются все типичные действия.</span><span class="sxs-lookup"><span data-stu-id="8a784-113">When these APIs are used, all typical actions will be performed.</span></span> <span data-ttu-id="8a784-114">Ниже описаны некоторые характеристики API ALM.</span><span class="sxs-lookup"><span data-stu-id="8a784-114">Here are some of the characteristics for ALM APIs.</span></span>

- <span data-ttu-id="8a784-115">События `Install` и `UnInstall` вызываются для надстроек с размещением у поставщика при выполнении соответствующих операций.</span><span class="sxs-lookup"><span data-stu-id="8a784-115">Install and UnInstall events are being fired for provider hosted add-ins when corresponding operations are occurred</span></span>
- <span data-ttu-id="8a784-116">API ALM поддерживают операции только для приложений.</span><span class="sxs-lookup"><span data-stu-id="8a784-116">ALM APIs support app-only-based operations.</span></span>

<span data-ttu-id="8a784-117">API ALM изначально предоставляются с использованием REST API, но есть дополнительные расширения CSOM и командлеты PowerShell, доступные благодаря SharePoint PnP.</span><span class="sxs-lookup"><span data-stu-id="8a784-117">ALM APIs are natively provided using REST APIs, but there is also additional CSOM extensions and PowerShell commandlets available through SharePoint Patterns and Practices.</span></span>

> [!NOTE] 
> <span data-ttu-id="8a784-118">API управления жизненным циклом приложений для [каталога приложений семейства сайтов](../general-development/site-collection-app-catalog.md) в настоящее время не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="8a784-118">ALM APIs are not currently supported for [site collection app catalog](../general-development/site-collection-app-catalog.md).</span></span> <span data-ttu-id="8a784-119">Поддержка будет добавлена в начале 2018 г.</span><span class="sxs-lookup"><span data-stu-id="8a784-119">Support will be added early 2018.</span></span>

## <a name="rest-api"></a><span data-ttu-id="8a784-120">REST API</span><span class="sxs-lookup"><span data-stu-id="8a784-120">REST API</span></span>

### <a name="add-solution-packages-to-the-tenant-app-catalog"></a><span data-ttu-id="8a784-121">Добавление пакетов решений в каталог приложений клиента</span><span class="sxs-lookup"><span data-stu-id="8a784-121">Adding solution to the tenant app catalog.</span></span> 

<span data-ttu-id="8a784-122">Этот API разработан для выполнения в контексте каталога приложений клиента.</span><span class="sxs-lookup"><span data-stu-id="8a784-122">This API is designed to be executed in the context of the tenant app catalog site.</span></span>

```
url: /_api/web/tenantappcatalog/Add(overwrite=true, url='test.txt')
method: POST
binaryStringRequestBody: true
body: 'byte array of the file'
```

### <a name="deploy-solution-packages-in-the-tenant-app-catalog"></a><span data-ttu-id="8a784-123">Развертывание пакетов решений в каталоге приложений клиента</span><span class="sxs-lookup"><span data-stu-id="8a784-123">Deploy solution package in tenant app catalog</span></span>

<span data-ttu-id="8a784-124">Это позволяет устанавливать решение на определенных сайтах.</span><span class="sxs-lookup"><span data-stu-id="8a784-124">Enable solution to be available to install to specific sites.</span></span> <span data-ttu-id="8a784-125">Этот API разработан для выполнения в контексте каталога приложений клиента.</span><span class="sxs-lookup"><span data-stu-id="8a784-125">This API is designed to be executed in the context of the tenant app catalog site.</span></span>

```
url: /_api/web/tenantappcatalog/AvailableApps/GetById('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxx')/Deploy
```

> [!NOTE]
> <span data-ttu-id="8a784-126">Эта операция должна быть завершена после добавления, прежде чем вы сможете устанавливать пакеты на определенные сайты.</span><span class="sxs-lookup"><span data-stu-id="8a784-126">This operation is required to be completed after add, before you can install packages to specific sites.</span></span> 

### <a name="retract-solution-packages-in-the-tenant-app-catalog"></a><span data-ttu-id="8a784-127">Отзыв пакетов решений в каталоге приложений клиента</span><span class="sxs-lookup"><span data-stu-id="8a784-127">Retract solution package in the tenant app catalog</span></span>

<span data-ttu-id="8a784-128">При этом решение становится недоступно на сайтах.</span><span class="sxs-lookup"><span data-stu-id="8a784-128">This retracts the solution to be available from the sites.</span></span> <span data-ttu-id="8a784-129">Этот API разработан для выполнения в контексте каталога приложений клиента.</span><span class="sxs-lookup"><span data-stu-id="8a784-129">This API is designed to be executed in the context of the tenant app catalog site.</span></span>

```
url: /_api/web/tenantappcatalog/AvailableApps/GetById('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxx')/Retract
```

> [!NOTE]
> <span data-ttu-id="8a784-130">Если выполнить эту операцию после установки решений на сайте, они перестанут работать, так как на уровне клиента решения отключены.</span><span class="sxs-lookup"><span data-stu-id="8a784-130">If you run this operation after you have already installed solutions to site, they will stop working since solution is disabled from the tenant level.</span></span>

### <a name="remove-solution-packages-from-the-tenant-app-catalog"></a><span data-ttu-id="8a784-131">Удаление пакетов решений из каталога приложений клиента</span><span class="sxs-lookup"><span data-stu-id="8a784-131">Remove the solution package from the tenant app catalog.</span></span>

<span data-ttu-id="8a784-132">Этот API разработан для выполнения в контексте каталога приложений клиента.</span><span class="sxs-lookup"><span data-stu-id="8a784-132">This API is designed to be executed in the context of the tenant app catalog site.</span></span>

```
url: /_api/web/tenantappcatalog/AvailableApps/GetById('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxx')/Remove
```

> [!NOTE]
> <span data-ttu-id="8a784-133">Если не отозвать решение перед его удалением, то решение будет отозвано автоматически.</span><span class="sxs-lookup"><span data-stu-id="8a784-133">If the Retract operation is not performed before the Remove operation, the solution is automatically retracted.</span></span>

### <a name="list-available-packages-from-the-tenant-app-catalog"></a><span data-ttu-id="8a784-134">Перечисление доступных пакетов из каталога приложений клиента</span><span class="sxs-lookup"><span data-stu-id="8a784-134">List available packages from tenant app catalog</span></span>

<span data-ttu-id="8a784-135">С помощью этого REST API можно получить список доступных надстроек или решений SharePoint Framework в каталоге приложений клиента.</span><span class="sxs-lookup"><span data-stu-id="8a784-135">REST API for getting list of available SharePoint Framework solutions or add-ins in tenant app catalog.</span></span>

```
url: /_api/web/tenantappcatalog/AvailableApps
method: GET
```

### <a name="details-about-individual-solution-packages-in-the-tenant-app-catalog"></a><span data-ttu-id="8a784-136">Сведения об отдельных пакетах решений в каталоге приложений клиента</span><span class="sxs-lookup"><span data-stu-id="8a784-136">Details about individual solution packages in the tenant app catalog</span></span>

<span data-ttu-id="8a784-137">С помощью этого REST API можно получать сведения об отдельных надстройках или решениях SharePoint Framework, которые доступны в каталоге приложений клиента.</span><span class="sxs-lookup"><span data-stu-id="8a784-137">REST API for getting details on individual SharePoint Framework solution or add-in available in the tenant app catalog.</span></span>

```
url: /_api/web/tenantappcatalog/AvailableApps/GetById('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxx')
method: GET
```

### <a name="install-solution-package-from-the-tenant-app-catalog-to-a-sharepoint-site"></a><span data-ttu-id="8a784-138">Установка пакета решения из каталога приложений клиента на сайте SharePoint</span><span class="sxs-lookup"><span data-stu-id="8a784-138">Install solution package from tenant app catalog to SharePoint site</span></span>

<span data-ttu-id="8a784-139">Установка пакета решения с определенным идентификатором из каталога приложений клиента на сайте на основе контекста URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="8a784-139">Install a solution package with specific identifier from tenant app catalog to the site based on URL context.</span></span> <span data-ttu-id="8a784-140">Этот вызов REST может выполняться в контексте сайта, на котором запланирована установка.</span><span class="sxs-lookup"><span data-stu-id="8a784-140">This REST call can be executed in the context of the site where the install operation should happen.</span></span>

```
url: /_api/web/tenantappcatalog/AvailableApps/GetById('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxx')/Install
method: POST
```

### <a name="upgrade-solution-packages-on-the-sharepoint-site"></a><span data-ttu-id="8a784-141">Обновление пакета решения на сайте SharePoint</span><span class="sxs-lookup"><span data-stu-id="8a784-141">Upgrade solution packages on the SharePoint site</span></span>

<span data-ttu-id="8a784-142">Обновите пакет решения на сайте до более новой версии, доступной в каталоге приложений клиента.</span><span class="sxs-lookup"><span data-stu-id="8a784-142">Upgrade a solution package from the site to a newer version available in the tenant app catalog.</span></span> <span data-ttu-id="8a784-143">Этот вызов REST может выполняться в контексте сайта, на котором запланировано обновление.</span><span class="sxs-lookup"><span data-stu-id="8a784-143">This REST call can be executed in the context of the site where the upgrade operation should happen.</span></span>

```
url: /_api/web/tenantappcatalog/AvailableApps/GetById('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxx')/Upgrade
method: POST
```

### <a name="uninstall-solution-packages-from-the-sharepoint-site"></a><span data-ttu-id="8a784-144">Удаление пакетов решений с сайта SharePoint</span><span class="sxs-lookup"><span data-stu-id="8a784-144">Uninstall solution package from SharePoint site</span></span>

<span data-ttu-id="8a784-145">Этот вызов REST может выполняться в контексте сайта, на котором запланировано удаление.</span><span class="sxs-lookup"><span data-stu-id="8a784-145">This REST call can be executed in the context of the site where the uninstall operation should happen.</span></span>

```
url: /_api/web/tenantappcatalog/AvailableApps/GetById('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxx')/Uninstall
method: POST
```
> [!NOTE]
> <span data-ttu-id="8a784-146">При удалении пакета решения с сайта с помощью REST API он не перемещается в корзину.</span><span class="sxs-lookup"><span data-stu-id="8a784-146">When you use the REST API to uninstall solution package from the site, it is not relocated to the recycle bin.</span></span>


## <a name="sharepoint-pnp-powershell-cmdlets"></a><span data-ttu-id="8a784-147">Командлеты PowerShell в SharePoint PnP</span><span class="sxs-lookup"><span data-stu-id="8a784-147">SharePoint PnP PowerShell cmdlets</span></span> 

<span data-ttu-id="8a784-148">При помощи [PnP PowerShell](https://docs.microsoft.com/en-us/powershell/sharepoint/sharepoint-pnp/sharepoint-pnp-cmdlets?view=sharepoint-ps) вы можете автоматизировать развертывание, публикацию, установку, обновление и отзыв приложений.</span><span class="sxs-lookup"><span data-stu-id="8a784-148">Using [PnP PowerShell](https://docs.microsoft.com/en-us/powershell/sharepoint/sharepoint-pnp/sharepoint-pnp-cmdlets?view=sharepoint-ps) you can automate the deployment, publishing, installing, upgrading and retracting your apps.</span></span> 

### <a name="add-and-publish-your-app-to-the-app-catalog"></a><span data-ttu-id="8a784-149">Добавление и публикация приложения в каталоге приложений</span><span class="sxs-lookup"><span data-stu-id="8a784-149">Adding and publishing your app to the app catalog</span></span>

<span data-ttu-id="8a784-150">Добавление приложения (SPPKG, APP) в каталог приложений клиента является обязательным условием для использования этого приложения на сайтах SharePoint.</span><span class="sxs-lookup"><span data-stu-id="8a784-150">Adding your app (.sppkg file, .app file) to the tenant app catalog is a per-requisite to later on make your app available for use in your SharePoint sites.</span></span> <span data-ttu-id="8a784-151">Для этого можно использовать следующий командлет:</span><span class="sxs-lookup"><span data-stu-id="8a784-151">You can do so by using the following cmdlet:</span></span>

```PowerShell
Add-PnPApp -Path ./myapp.sppkg
```

<span data-ttu-id="8a784-152">Добавив приложение, следует опубликовать его. Так оно будет доступно пользователям вашего клиента.</span><span class="sxs-lookup"><span data-stu-id="8a784-152">Once added you'll need to continue with publishing your app, effectively making the app available to be used by the users of your tenant.</span></span> <span data-ttu-id="8a784-153">Ниже на примере командлета PnP PowerShell показано, как это можно сделать.</span><span class="sxs-lookup"><span data-stu-id="8a784-153">Below PnP PowerShell cmdlets shows how this can be done:</span></span>

```PowerShell
Publish-PnPApp -Identity <app id> -SkipFeatureDeployment
```


> [!NOTE]
> <span data-ttu-id="8a784-154">Используйте флаг `SkipFeatureDeployment`, чтобы приложение, разработанное для развертывания на уровне клиента, было доступно в этом качестве.</span><span class="sxs-lookup"><span data-stu-id="8a784-154">Use the SkipFeatureDeployment flag to allow an app that was developed for tenant wide deployment to be actually available as a tenant wide deployed app.</span></span>



### <a name="remove-the-app-from-the-app-catalog"></a><span data-ttu-id="8a784-155">Удаление приложения из каталога приложений</span><span class="sxs-lookup"><span data-stu-id="8a784-155">Removing the app from the app catalog</span></span>

<span data-ttu-id="8a784-156">Чтобы удалить добавленное ранее приложение, используйте следующий командлет:</span><span class="sxs-lookup"><span data-stu-id="8a784-156">To remove an app added earlier, use the following cmdlet:</span></span>

```PowerShell
Remove-PnPApp -Identity <app id>
```


### <a name="use-apps-on-your-site"></a><span data-ttu-id="8a784-157">Использование приложений на сайте</span><span class="sxs-lookup"><span data-stu-id="8a784-157">Using apps on your site</span></span>

<span data-ttu-id="8a784-158">Добавив приложение в каталог и опубликовав его, вы можете установить приложение на своем сайте:</span><span class="sxs-lookup"><span data-stu-id="8a784-158">Once the app was added to the app catalog and published you can continue with installing the app to your site.</span></span>

```PowerShell
Install-PnPApp -Identity <app id>
```


<span data-ttu-id="8a784-159">Обновление приложения:</span><span class="sxs-lookup"><span data-stu-id="8a784-159">To upgrade the app:</span></span>

```PowerShell
Update-PnPApp -Identity <app id>
```


<span data-ttu-id="8a784-160">Удаление приложения с сайта:</span><span class="sxs-lookup"><span data-stu-id="8a784-160">To uninstall the app from your site:</span></span>

```PowerShell
Uninstall-PnPApp -Identity <app id>
```


> [!NOTE]
> <span data-ttu-id="8a784-161">При удалении приложения с сайта оно удаляется полностью, не попадая в корзину сайта.</span><span class="sxs-lookup"><span data-stu-id="8a784-161">When you uninstall an app from your site the app is completely deleted, so it will not end up in the site's recycle bin.</span></span>



### <a name="know-which-apps-are-there-for-you-to-use"></a><span data-ttu-id="8a784-162">Сведения о доступных приложениях</span><span class="sxs-lookup"><span data-stu-id="8a784-162">Knowing which apps are there for you to use</span></span>

<span data-ttu-id="8a784-163">Вы можете получить список приложений, доступных для добавления на сайт, используя следующий командлет:</span><span class="sxs-lookup"><span data-stu-id="8a784-163">Getting a list of apps that can be added to the site is possible using:</span></span>

```PowerShell
Get-PnPApp
```

## <a name="see-also"></a><span data-ttu-id="8a784-164">См. также</span><span class="sxs-lookup"><span data-stu-id="8a784-164">See also</span></span>

- [<span data-ttu-id="8a784-165">Знакомство со службой REST в SharePoint</span><span class="sxs-lookup"><span data-stu-id="8a784-165">Get to know the SharePoint REST service</span></span>](../sp-add-ins/get-to-know-the-sharepoint-rest-service.md)