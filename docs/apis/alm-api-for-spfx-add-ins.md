---
title: "API управления жизненным циклом приложений (ALM)"
ms.date: 12/19/2017
ms.prod: sharepoint
ms.assetid: fdf7ecb2-8851-425b-b058-3285fba77b68
ms.openlocfilehash: 967ff4d456ee839f347c07605ec90adff7d3b2fc
ms.sourcegitcommit: 6bc4c8e43c260deabc60d41d633586bfa3e6024a
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/28/2017
---
# <a name="application-lifecycle-management-alm-apis"></a><span data-ttu-id="41188-102">API управления жизненным циклом приложений (ALM)</span><span class="sxs-lookup"><span data-stu-id="41188-102">Application Lifecycle Management (ALM) APIs</span></span>  

<span data-ttu-id="41188-103">API управления жизненным циклом приложений — простые API-интерфейсы для управления развертыванием решений и надстроек SharePoint Framework в клиенте.</span><span class="sxs-lookup"><span data-stu-id="41188-103">ALM APIs are providing simple APIs to manage deployment of your SharePoint Framework solutions and add-ins cross your tenant.</span></span> <span data-ttu-id="41188-104">Эти API поддерживают приведенные ниже возможности.</span><span class="sxs-lookup"><span data-stu-id="41188-104">ALM APIs support following capabilities.</span></span>

- <span data-ttu-id="41188-105">Добавление решения SharePoint Framework или надстройки SharePoint в каталог приложений клиента.</span><span class="sxs-lookup"><span data-stu-id="41188-105">Add SharePoint Framework solution or SharePoint add-in to tenant app catalog</span></span>
- <span data-ttu-id="41188-106">Обеспечение доступности решения SharePoint Framework или надстройки SharePoint для установки в каталоге приложений клиента.</span><span class="sxs-lookup"><span data-stu-id="41188-106">Enable SharePoint Framework solution or SharePoint add-in to be available for installation in tenant app catalog</span></span>
- <span data-ttu-id="41188-107">Отключение возможности установки решения SharePoint Framework или надстройки SharePoint в каталоге приложений клиента.</span><span class="sxs-lookup"><span data-stu-id="41188-107">Disable SharePoint Framework solution or SharePoint add-in not to be available for installation in tenant app catalog</span></span>
- <span data-ttu-id="41188-108">Установка решения SharePoint Framework или надстройки SharePoint из каталога приложений клиента на сайте.</span><span class="sxs-lookup"><span data-stu-id="41188-108">Install SharePoint Framework solution or SharePoint add-in from tenant app catalog to a site</span></span>
- <span data-ttu-id="41188-109">Обновление решения SharePoint Framework или надстройки SharePoint для использования на сайте с более поздней версией, доступной в каталоге приложений клиента.</span><span class="sxs-lookup"><span data-stu-id="41188-109">Upgrade SharePoint Framework solution or SharePoint add-in to a site, which has a newer version available in the tenant app catalog</span></span>
- <span data-ttu-id="41188-110">Удаление решения SharePoint Framework или надстройки SharePoint с сайта.</span><span class="sxs-lookup"><span data-stu-id="41188-110">Uninstall SharePoint Framework solution or SharePoint add-in from the site</span></span>

<span data-ttu-id="41188-111">API управления жизненным циклом приложений можно использовать для выполнения тех же операций, которые доступны для пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="41188-111">ALM APIs can be used to perform exactly the same operations which are available from UI perspective.</span></span> <span data-ttu-id="41188-112">При использовании этих API выполняются все типичные действия.</span><span class="sxs-lookup"><span data-stu-id="41188-112">When these APIs are used, all typical actions will be performed.</span></span> <span data-ttu-id="41188-113">Ниже описаны некоторые характеристики API ALM.</span><span class="sxs-lookup"><span data-stu-id="41188-113">Here are some of the characteristics for ALM APIs.</span></span>

- <span data-ttu-id="41188-114">При выполнении соответствующих операций происходят события установки и удаления надстроек, размещаемых у поставщика.</span><span class="sxs-lookup"><span data-stu-id="41188-114">Install and UnInstall events are being fired for provider hosted add-ins when corresponding operations are occurred</span></span>
- <span data-ttu-id="41188-115">API ALM поддерживают операции только для приложений.</span><span class="sxs-lookup"><span data-stu-id="41188-115">ALM APIs supports app-only based operations</span></span>

<span data-ttu-id="41188-116">API ALM изначально предоставляются с использованием REST API, но есть дополнительные расширения CSOM и командлеты PowerShell, доступные благодаря SharePoint PnP.</span><span class="sxs-lookup"><span data-stu-id="41188-116">ALM APIs are natively provided using REST APIs, but there is also additional CSOM extensions and PowerShell commandlets available through SharePoint Patterns and Practices.</span></span>

> [!NOTE] 
> <span data-ttu-id="41188-117">API управления жизненным циклом приложений для [каталога приложений семейства сайтов](../general-development/site-collection-app-catalog.md) в настоящее время не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="41188-117">ALM APIs are not currently supported for [site collection app catalog](../general-development/site-collection-app-catalog.md).</span></span> <span data-ttu-id="41188-118">Поддержка будет добавлена в начале 2018 г.</span><span class="sxs-lookup"><span data-stu-id="41188-118">Support will be added early 2018.</span></span>

## <a name="rest-api"></a><span data-ttu-id="41188-119">API REST</span><span class="sxs-lookup"><span data-stu-id="41188-119">REST API</span></span>

### <a name="add-solution-package-to-tenant-app-catalog"></a><span data-ttu-id="41188-120">Добавление пакета решения в каталог приложений клиента</span><span class="sxs-lookup"><span data-stu-id="41188-120">Add solution package to tenant app catalog</span></span> 

<span data-ttu-id="41188-121">Добавление решения в каталог приложений клиента.</span><span class="sxs-lookup"><span data-stu-id="41188-121">Adding solution to the tenant app catalog.</span></span> <span data-ttu-id="41188-122">Этот API разработан для выполнения в контексте сайта каталога приложений клиента.</span><span class="sxs-lookup"><span data-stu-id="41188-122">This API is designed to be executed in the context of the tenant app catalog site.</span></span>

```
/_api/web/tenantappcatalog/Add(overwrite=true, url='test.txt')";
method: POST
binaryStringRequestBody: true
body: 'byte array of the file'
```

### <a name="deploy-solution-package-in-tenant-app-catalog"></a><span data-ttu-id="41188-123">Развертывание пакета решения в каталоге приложений клиента</span><span class="sxs-lookup"><span data-stu-id="41188-123">Deploy solution package in tenant app catalog</span></span>

<span data-ttu-id="41188-124">Обеспечение возможности установить решение на определенных сайтах.</span><span class="sxs-lookup"><span data-stu-id="41188-124">Enable solution to be available to install to specific sites.</span></span> <span data-ttu-id="41188-125">Этот API разработан для выполнения в контексте сайта каталога приложений клиента.</span><span class="sxs-lookup"><span data-stu-id="41188-125">This API is designed to be executed in the context of the tenant app catalog site.</span></span>

```
/_api/web/tenantappcatalog/AvailableApps/GetById('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxx')/Deploy";
```

> [!NOTE]
> <span data-ttu-id="41188-126">Эта операция должна быть завершена после добавления, прежде чем вы сможете устанавливать пакеты на определенные сайты.</span><span class="sxs-lookup"><span data-stu-id="41188-126">This operation is required to be completed after add, before you can install packages to specific sites.</span></span> 

### <a name="retract-solution-package-in-the-tenant-app-catalog"></a><span data-ttu-id="41188-127">Отзыв пакета решения в каталоге приложений клиента</span><span class="sxs-lookup"><span data-stu-id="41188-127">Retract solution package in the tenant app catalog</span></span>

<span data-ttu-id="41188-128">Отзыв решения для отмены его доступности на сайтах.</span><span class="sxs-lookup"><span data-stu-id="41188-128">Retract solution to be available from the sites.</span></span> <span data-ttu-id="41188-129">Этот API разработан для выполнения в контексте сайта каталога приложений клиента.</span><span class="sxs-lookup"><span data-stu-id="41188-129">This API is designed to be executed in the context of the tenant app catalog site.</span></span>

```
/_api/web/tenantappcatalog/AvailableApps/GetById('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxx')/Retract";
```

> [!NOTE]
> <span data-ttu-id="41188-130">Если вы запустите эту операцию уже после установки решений на сайте, они перестанут работать, так как на уровне клиента решения отключены.</span><span class="sxs-lookup"><span data-stu-id="41188-130">If you run this operation after you have already installed solutions to site, they will stop working since solution is disabled from the tenant level.</span></span>

### <a name="remove-solution-package-from-tenant-app-catalog"></a><span data-ttu-id="41188-131">Удаление пакета решения из каталога приложений клиента</span><span class="sxs-lookup"><span data-stu-id="41188-131">Remove solution package from tenant app catalog</span></span>

<span data-ttu-id="41188-132">Удаляет пакет решения из каталога приложений клиента.</span><span class="sxs-lookup"><span data-stu-id="41188-132">Remove the solution package from the tenant app catalog.</span></span> <span data-ttu-id="41188-133">Этот API разработан для выполнения в контексте сайта каталога приложений клиента.</span><span class="sxs-lookup"><span data-stu-id="41188-133">This API is designed to be executed in the context of the tenant app catalog site.</span></span>

```
/_api/web/tenantappcatalog/AvailableApps/GetById('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxx')/Remove";
```

> [!NOTE]
> <span data-ttu-id="41188-134">Решение также будет автоматически отозвано, если эта операция не была выполнена до операции удаления.</span><span class="sxs-lookup"><span data-stu-id="41188-134">Solution will be also automatically retracted, if that operation has not performed before Remove operation.</span></span>

### <a name="list-available-packages-from-tenant-app-catalog"></a><span data-ttu-id="41188-135">Перечисление доступных пакетов из каталога приложений клиента</span><span class="sxs-lookup"><span data-stu-id="41188-135">List available packages from tenant app catalog</span></span>

<span data-ttu-id="41188-136">REST API для получения списка доступных надстроек или решений SharePoint Framework в каталоге приложений клиента.</span><span class="sxs-lookup"><span data-stu-id="41188-136">REST API for getting list of available SharePoint Framework solutions or add-ins in tenant app catalog.</span></span>

```
url: /_api/web/tenantappcatalog/AvailableApps
method: GET
```

### <a name="details-on-individual-solution-package-from-tenant-app-catalog"></a><span data-ttu-id="41188-137">Сведения об отдельном пакете решения из каталога приложений клиента</span><span class="sxs-lookup"><span data-stu-id="41188-137">Details on individual solution package from tenant app catalog</span></span>

<span data-ttu-id="41188-138">REST API для получения сведений об отдельных надстройках или решениях SharePoint Framework, которые доступны в каталоге приложений клиента.</span><span class="sxs-lookup"><span data-stu-id="41188-138">REST API for getting details on individual SharePoint Framework solution or add-in available in the tenant app catalog.</span></span>

```
url: /_api/web/tenantappcatalog/AvailableApps/GetById('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxx')
method: GET
```

### <a name="install-solution-package-from-tenant-app-catalog-to-sharepoint-site"></a><span data-ttu-id="41188-139">Установка пакета решения из каталога приложений клиента на сайте SharePoint</span><span class="sxs-lookup"><span data-stu-id="41188-139">Install solution package from tenant app catalog to SharePoint site</span></span>

<span data-ttu-id="41188-140">Установка пакета решения с определенным идентификатором из каталога приложений клиента на сайте с учетом контекста URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="41188-140">Install a solution package with specific identifier from tenant app catalog to the site based on URL context.</span></span> <span data-ttu-id="41188-141">Вызов REST может быть выполнен в контексте сайта, на котором должна выполняться операция установки.</span><span class="sxs-lookup"><span data-stu-id="41188-141">This REST call can be executed in the context of the site where the install operation should happen.</span></span>

```
url: /_api/web/tenantappcatalog/AvailableApps/GetById('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxx')/Install";
method: POST
```

### <a name="upgrade-solution-package-in-sharepoint-site"></a><span data-ttu-id="41188-142">Обновление пакета решения на сайте SharePoint</span><span class="sxs-lookup"><span data-stu-id="41188-142">Upgrade solution package in SharePoint site</span></span>

<span data-ttu-id="41188-143">Обновление пакета решения с сайта до более новой версии, доступной в каталоге приложений клиента.</span><span class="sxs-lookup"><span data-stu-id="41188-143">Upgrade a solution package from the site to a newer version available in the tenant app catalog.</span></span> <span data-ttu-id="41188-144">Вызов REST может быть выполнен в контексте сайта, на котором должна выполняться операция обновления.</span><span class="sxs-lookup"><span data-stu-id="41188-144">This REST call can be executed in the context of the site where the upgrade operation should happen.</span></span>

```
url: /_api/web/tenantappcatalog/AvailableApps/GetById('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxx')/Upgrade";
method: POST
```

### <a name="uninstall-solution-package-from-sharepoint-site"></a><span data-ttu-id="41188-145">Удаление пакета решения с сайта SharePoint</span><span class="sxs-lookup"><span data-stu-id="41188-145">Uninstall solution package from SharePoint site</span></span>

<span data-ttu-id="41188-146">Удаление пакета решения с сайта.</span><span class="sxs-lookup"><span data-stu-id="41188-146">Uninstall a solution package from the site.</span></span> <span data-ttu-id="41188-147">Вызов REST может быть выполнен в контексте сайта, на котором должна выполняться операция удаления.</span><span class="sxs-lookup"><span data-stu-id="41188-147">This REST call can be executed in the context of the site where the uninstall operation should happen.</span></span>

```
url: /_api/web/tenantappcatalog/AvailableApps/GetById('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxx')/Uninstall";
method: POST
```
> [!NOTE]
> <span data-ttu-id="41188-148">Когда вы используете REST API для удаления пакета решения с сайта, он не перемещается в корзину.</span><span class="sxs-lookup"><span data-stu-id="41188-148">When you use the REST API to uninstall solution package from the site, it is not relocated to the recycle bin.</span></span>


## <a name="sharepoint-pnp-powershell-cmdlets-to-programmatically-add-and-deploy-sharepoint-apps"></a><span data-ttu-id="41188-149">Командлеты PnP PowerShell SharePoint для добавления и развертывания приложений SharePoint программным способом</span><span class="sxs-lookup"><span data-stu-id="41188-149">SharePoint PnP PowerShell cmdlets to programmatically add and deploy SharePoint Apps</span></span>

<span data-ttu-id="41188-150">При помощи [PnP PowerShell]((https://msdn.microsoft.com/ru-RU/pnp_powershell/pnp-powershell-overview)) вы можете автоматизировать развертывание, публикацию, установку, обновление и отзыв приложений.</span><span class="sxs-lookup"><span data-stu-id="41188-150">Using [PnP PowerShell]((https://msdn.microsoft.com/ru-RU/pnp_powershell/pnp-powershell-overview)) you can automate the deployment, publishing, installing, upgrading and retracting your apps.</span></span> <span data-ttu-id="41188-151">Дополнительные сведения об этих командлетах вы найдете в приведенном ниже разделе.</span><span class="sxs-lookup"><span data-stu-id="41188-151">Checkout below chapter to learn more about this cmdlets.</span></span>

### <a name="adding-and-publishing-your-app-to-the-app-catalog"></a><span data-ttu-id="41188-152">Добавление и публикация приложения в каталоге приложений</span><span class="sxs-lookup"><span data-stu-id="41188-152">Adding and publishing your app to the app catalog</span></span>
<span data-ttu-id="41188-153">Добавление приложения (.sppkg, .app) в каталог приложений клиента является обязательным условием для дальнейшего использования этого приложения на сайтах SharePoint.</span><span class="sxs-lookup"><span data-stu-id="41188-153">Adding your app (.sppkg file, .app file) to the tenant app catalog is a per-requisite to later on make your app available for use in your SharePoint sites.</span></span> <span data-ttu-id="41188-154">Это можно сделать с помощью приведенного ниже простого командлета.</span><span class="sxs-lookup"><span data-stu-id="41188-154">Doing so can be done using below simple cmdlet:</span></span>

```PowerShell
Add-PnPApp -Path ./myapp.sppkg"
```

<span data-ttu-id="41188-155">Следующий после добавления шаг — публикация приложения. Так оно будет доступно пользователям вашего клиента.</span><span class="sxs-lookup"><span data-stu-id="41188-155">Once added you'll need to continue with publishing your app, effectively making the app available to be used by the users of your tenant.</span></span> <span data-ttu-id="41188-156">Ниже на примере командлета PnP PowerShell показано, как это можно сделать.</span><span class="sxs-lookup"><span data-stu-id="41188-156">Below PnP PowerShell cmdlets shows how this can be done:</span></span>

```PowerShell
Publish-PnPApp -Identity <app id> -SkipFeatureDeployment
```


> [!NOTE]
> <span data-ttu-id="41188-157">Используйте флажок SkipFeatureDeployment, чтобы приложение, разработанное для развертывания на уровне клиента, было фактически доступно в этом качестве.</span><span class="sxs-lookup"><span data-stu-id="41188-157">Use the SkipFeatureDeployment flag to allow an app that was developed for tenant wide deployment to be actually available as a tenant wide deployed app.</span></span>



### <a name="removing-the-app-from-the-app-catalog"></a><span data-ttu-id="41188-158">Удаление приложения из каталога приложений</span><span class="sxs-lookup"><span data-stu-id="41188-158">Removing the app from the app catalog</span></span>
<span data-ttu-id="41188-159">Вы также можете удалить ранее добавленное приложение с помощью приведенного ниже командлета.</span><span class="sxs-lookup"><span data-stu-id="41188-159">Obviously you might also want to remove an earlier added app and that can be done using the following cmdlet:</span></span>

```PowerShell
Remove-PnPApp -Identity <app id>
```


### <a name="using-apps-on-your-site"></a><span data-ttu-id="41188-160">Использование приложений на сайте</span><span class="sxs-lookup"><span data-stu-id="41188-160">Using apps on your site</span></span>
<span data-ttu-id="41188-161">После добавления приложения в каталог приложений и его публикации вы можете установить это приложение на своем сайте.</span><span class="sxs-lookup"><span data-stu-id="41188-161">Once the app was added to the app catalog and published you can continue with installing the app to your site.</span></span>

```PowerShell
Install-PnPApp -Identity <app id>
```


<span data-ttu-id="41188-162">Добавленное приложение следует обновить:</span><span class="sxs-lookup"><span data-stu-id="41188-162">An added app also needs be upgraded:</span></span>

```PowerShell
Update-PnPApp -Identity <app id>
```


<span data-ttu-id="41188-163">Затем приложение можно снова удалить с сайта:</span><span class="sxs-lookup"><span data-stu-id="41188-163">And you off course also uninstall the app again from your site:</span></span>

```PowerShell
Uninstall-PnPApp -Identity <app id>
```


> [!NOTE]
> <span data-ttu-id="41188-164">При удалении приложения с сайта оно удаляется полностью, поэтому не попадает в корзину сайта.</span><span class="sxs-lookup"><span data-stu-id="41188-164">When you uninstall an app from your site the app is completely deleted, so it will not end up in the site's recycle bin.</span></span>



### <a name="knowing-which-apps-are-there-for-you-to-use"></a><span data-ttu-id="41188-165">Информация о доступных приложениях</span><span class="sxs-lookup"><span data-stu-id="41188-165">Knowing which apps are there for you to use</span></span>
<span data-ttu-id="41188-166">При помощи приведенного ниже командлета вы получите список приложений, которые можно добавить на сайт.</span><span class="sxs-lookup"><span data-stu-id="41188-166">Getting a list of apps that can be added to the site is possible using:</span></span>

```PowerShell
Get-PnPApp
```
