---
title: "API управления жизненным циклом приложений (ALM)"
description: "API ALM представляют собой простые API для управления развертыванием решений и надстроек SharePoint Framework в клиенте."
ms.date: 02/08/2018
ms.prod: sharepoint
ms.assetid: fdf7ecb2-8851-425b-b058-3285fba77b68
ms.openlocfilehash: 3e3b9aa836bf6242bf2fe2ef4f1b3fdc5d2bcb62
ms.sourcegitcommit: 860b40b91f01c5b781517e3cd4057b971ce90b6e
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/02/2018
---
# <a name="application-lifecycle-management-alm-apis"></a><span data-ttu-id="01c8a-103">API управления жизненным циклом приложений (ALM)</span><span class="sxs-lookup"><span data-stu-id="01c8a-103">Application Lifecycle Management (ALM) APIs</span></span>

<span data-ttu-id="01c8a-104">API ALM представляют собой простые API для управления развертыванием решений и надстроек SharePoint Framework в клиенте.</span><span class="sxs-lookup"><span data-stu-id="01c8a-104">ALM APIs provide simple APIs to manage deployment of your SharePoint Framework solutions and add-ins across your tenant.</span></span> <span data-ttu-id="01c8a-105">Эти API поддерживают указанные ниже возможности.</span><span class="sxs-lookup"><span data-stu-id="01c8a-105">ALM APIs support the following capabilities:</span></span>

- <span data-ttu-id="01c8a-106">Добавление решения SharePoint Framework или надстройки SharePoint в каталог приложений клиента.</span><span class="sxs-lookup"><span data-stu-id="01c8a-106">Add SharePoint Framework solution or SharePoint Add-in to tenant app catalog.</span></span>
- <span data-ttu-id="01c8a-107">Удаление решения SharePoint Framework или надстройки SharePoint из каталога приложений клиента.</span><span class="sxs-lookup"><span data-stu-id="01c8a-107">Install SharePoint Framework solution or SharePoint Add-in from tenant app catalog to a site.</span></span>
- <span data-ttu-id="01c8a-108">Обеспечение доступности решения SharePoint Framework или надстройки SharePoint для установки в каталоге приложений клиента.</span><span class="sxs-lookup"><span data-stu-id="01c8a-108">Enable SharePoint Framework solution or SharePoint Add-in to be available for installation in tenant app catalog.</span></span>
- <span data-ttu-id="01c8a-109">Отключение возможности установки решения SharePoint Framework или надстройки SharePoint в каталоге приложений клиента.</span><span class="sxs-lookup"><span data-stu-id="01c8a-109">Disable SharePoint Framework solution or SharePoint Add-in not to be available for installation in tenant app catalog.</span></span>
- <span data-ttu-id="01c8a-110">Установка решения SharePoint Framework или надстройки SharePoint из каталога приложений клиента на сайте.</span><span class="sxs-lookup"><span data-stu-id="01c8a-110">Install SharePoint Framework solution or SharePoint Add-in from tenant app catalog to a site.</span></span>
- <span data-ttu-id="01c8a-111">Обновление решения SharePoint Framework или надстройки SharePoint на сайте до более поздней версии, доступной в каталоге приложений клиента.</span><span class="sxs-lookup"><span data-stu-id="01c8a-111">Upgrade SharePoint Framework solution or SharePoint Add-in to a site, which has a newer version available in the tenant app catalog.</span></span>
- <span data-ttu-id="01c8a-112">Удаление решения SharePoint Framework или надстройки SharePoint с сайта.</span><span class="sxs-lookup"><span data-stu-id="01c8a-112">Uninstall SharePoint Framework solution or SharePoint Add-in from the site.</span></span>
- <span data-ttu-id="01c8a-113">Перечисление и получение всех сведений о решениях SharePoint Framework или надстройках SharePoint в каталоге приложений клиента.</span><span class="sxs-lookup"><span data-stu-id="01c8a-113">List all and get details about SharePoint Framework solutions or SharePoint Add-ins in the tenant app catalog.</span></span>

<span data-ttu-id="01c8a-114">С помощью API ALM можно выполнять те же операции, что и в пользовательском интерфейсе.</span><span class="sxs-lookup"><span data-stu-id="01c8a-114">ALM APIs can be used to perform exactly the same operations that are available from a UI perspective.</span></span> <span data-ttu-id="01c8a-115">При использовании этих API выполняются все типичные действия.</span><span class="sxs-lookup"><span data-stu-id="01c8a-115">When these APIs are used, all typical actions are performed.</span></span> <span data-ttu-id="01c8a-116">Ниже описаны некоторые характеристики API ALM.</span><span class="sxs-lookup"><span data-stu-id="01c8a-116">Following are some of the characteristics of ALM APIs:</span></span>

- <span data-ttu-id="01c8a-117">События `Install` и `UnInstall` вызываются для надстроек с размещением у поставщика при выполнении соответствующих операций.</span><span class="sxs-lookup"><span data-stu-id="01c8a-117">`Install` and `UnInstall` events are being fired for provider-hosted add-ins when corresponding operations occur.</span></span>
- <span data-ttu-id="01c8a-118">API ALM поддерживают операции только для приложений.</span><span class="sxs-lookup"><span data-stu-id="01c8a-118">ALM APIs support app-only-based operations.</span></span>

<span data-ttu-id="01c8a-119">API ALM изначально предоставляются с использованием REST API, но есть дополнительные расширения CSOM, командлеты PowerShell и межплатформенный интерфейс командной строки Office 365, доступные благодаря SharePoint PnP.</span><span class="sxs-lookup"><span data-stu-id="01c8a-119">ALM APIs are natively provided by using REST APIs, but there are also additional CSOM extensions and PowerShell cmdlets available through SharePoint Patterns and Practices.</span></span>

> [!NOTE] 
> <span data-ttu-id="01c8a-120">API управления жизненным циклом приложений для [каталога приложений семейства сайтов](../general-development/site-collection-app-catalog.md) в настоящее время не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="01c8a-120">ALM APIs are not currently supported for the [site collection app catalog](../general-development/site-collection-app-catalog.md).</span></span> <span data-ttu-id="01c8a-121">Поддержка будет добавлена в начале 2018 г.</span><span class="sxs-lookup"><span data-stu-id="01c8a-121">Support will be added in early 2018.</span></span>

## <a name="rest-api"></a><span data-ttu-id="01c8a-122">REST API</span><span class="sxs-lookup"><span data-stu-id="01c8a-122">REST API</span></span>

### <a name="add-solution-package-to-the-tenant-app-catalog"></a><span data-ttu-id="01c8a-123">Добавление пакета решений в каталог приложений клиента</span><span class="sxs-lookup"><span data-stu-id="01c8a-123">Add solution package to tenant app catalog</span></span>

<span data-ttu-id="01c8a-124">Этот API разработан для выполнения в контексте каталога приложений клиента.</span><span class="sxs-lookup"><span data-stu-id="01c8a-124">This API is designed to be executed in the context of the tenant app catalog site.</span></span>

```
url: /_api/web/tenantappcatalog/Add(overwrite=true, url='test.txt')
method: POST
Authorization: Bearer <access token>
X-RequestDigest: <form digest>
Accept: 'application/json;odata=nometadata'
binaryStringRequestBody: true
body: 'byte array of the file'
```

### <a name="deploy-solution-packages-in-the-tenant-app-catalog"></a><span data-ttu-id="01c8a-125">Развертывание пакетов решений в каталоге приложений клиента</span><span class="sxs-lookup"><span data-stu-id="01c8a-125">Deploy solution packages in the tenant app catalog</span></span>

<span data-ttu-id="01c8a-126">Это позволяет устанавливать решение на определенных сайтах.</span><span class="sxs-lookup"><span data-stu-id="01c8a-126">This enables the solution to be available to install to specific sites.</span></span> <span data-ttu-id="01c8a-127">Этот API разработан для выполнения в контексте каталога приложений клиента.</span><span class="sxs-lookup"><span data-stu-id="01c8a-127">This API is designed to be executed in the context of the tenant app catalog site.</span></span>

```
url: /_api/web/tenantappcatalog/AvailableApps/GetById('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxx')/Deploy
method: POST
Authorization: Bearer <access token>
X-RequestDigest: <form digest>
Accept: 'application/json;odata=nometadata'
Content-Type: 'application/json;odata=nometadata;charset=utf-8'
```

> [!NOTE]
> <span data-ttu-id="01c8a-128">Эта операция должна быть завершена после добавления, прежде чем вы сможете устанавливать пакеты на определенные сайты.</span><span class="sxs-lookup"><span data-stu-id="01c8a-128">This operation is required to be completed after Add before you can install packages to specific sites.</span></span> 

### <a name="retract-solution-packages-in-the-tenant-app-catalog"></a><span data-ttu-id="01c8a-129">Отзыв пакетов решений в каталоге приложений клиента</span><span class="sxs-lookup"><span data-stu-id="01c8a-129">Retract solution packages in the tenant app catalog</span></span>

<span data-ttu-id="01c8a-130">При этом решение становится недоступно на сайтах.</span><span class="sxs-lookup"><span data-stu-id="01c8a-130">This retracts the solution to be available from the sites.</span></span> <span data-ttu-id="01c8a-131">Этот API разработан для выполнения в контексте каталога приложений клиента.</span><span class="sxs-lookup"><span data-stu-id="01c8a-131">This API is designed to be executed in the context of the tenant app catalog site.</span></span>

```
url: /_api/web/tenantappcatalog/AvailableApps/GetById('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxx')/Retract
method: POST
Authorization: Bearer <access token>
X-RequestDigest: <form digest>
Accept: 'application/json;odata=nometadata'
```

> [!NOTE]
> <span data-ttu-id="01c8a-132">Если выполнить эту операцию после установки решений на сайте, они перестанут работать, так как на уровне клиента решения отключены.</span><span class="sxs-lookup"><span data-stu-id="01c8a-132">If you run this operation after you have installed solutions to the site, they will stop working because the solution is disabled from the tenant level.</span></span>

### <a name="remove-solution-packages-from-the-tenant-app-catalog"></a><span data-ttu-id="01c8a-133">Удаление пакетов решений из каталога приложений клиента</span><span class="sxs-lookup"><span data-stu-id="01c8a-133">Remove solution packages from the tenant app catalog</span></span>

<span data-ttu-id="01c8a-134">Этот API разработан для выполнения в контексте каталога приложений клиента.</span><span class="sxs-lookup"><span data-stu-id="01c8a-134">This API is designed to be executed in the context of the tenant app catalog site.</span></span>

```
url: /_api/web/tenantappcatalog/AvailableApps/GetById('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxx')/Remove
method: POST
Authorization: Bearer <access token>
Accept: 'application/json;odata=nometadata'
```

> [!NOTE]
> <span data-ttu-id="01c8a-135">Если не отозвать решение перед его удалением, то решение будет отозвано автоматически.</span><span class="sxs-lookup"><span data-stu-id="01c8a-135">If the Retract operation is not performed before the Remove operation, the solution is automatically retracted.</span></span>

### <a name="list-available-packages-from-the-tenant-app-catalog"></a><span data-ttu-id="01c8a-136">Перечисление доступных пакетов из каталога приложений клиента</span><span class="sxs-lookup"><span data-stu-id="01c8a-136">List available packages from the tenant app catalog</span></span>

<span data-ttu-id="01c8a-137">С помощью этого REST API можно получить список доступных надстроек или решений SharePoint Framework в каталоге приложений клиента.</span><span class="sxs-lookup"><span data-stu-id="01c8a-137">Use this REST API for getting a list of available SharePoint Framework solutions or add-ins in the tenant app catalog.</span></span>

```
url: /_api/web/tenantappcatalog/AvailableApps
method: GET
Authorization: Bearer <access token>
Accept: 'application/json;odata=nometadata'
```

### <a name="get-details-about-individual-solution-packages-in-the-tenant-app-catalog"></a><span data-ttu-id="01c8a-138">Получение сведений об отдельных пакетах решений в каталоге приложений клиента</span><span class="sxs-lookup"><span data-stu-id="01c8a-138">Details about individual solution packages in the tenant app catalog</span></span>

<span data-ttu-id="01c8a-139">С помощью этого REST API можно получать сведения об отдельных надстройках или решениях SharePoint Framework, которые доступны в каталоге приложений клиента.</span><span class="sxs-lookup"><span data-stu-id="01c8a-139">Use this REST API for getting details about individual SharePoint Framework solutions or add-ins available in the tenant app catalog.</span></span>

```
url: /_api/web/tenantappcatalog/AvailableApps/GetById('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxx')
method: GET
Authorization: Bearer <access token>
Accept: 'application/json;odata=nometadata'
```

### <a name="install-solution-package-from-the-tenant-app-catalog-to-a-sharepoint-site"></a><span data-ttu-id="01c8a-140">Установка пакета решения из каталога приложений клиента на сайте SharePoint</span><span class="sxs-lookup"><span data-stu-id="01c8a-140">Install solution package from the tenant app catalog to a SharePoint site</span></span>

<span data-ttu-id="01c8a-141">Установка пакета решения с определенным идентификатором из каталога приложений клиента на сайте на основе контекста URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="01c8a-141">Install a solution package with a specific identifier from the tenant app catalog to the site based on URL context.</span></span> <span data-ttu-id="01c8a-142">Этот вызов REST может выполняться в контексте сайта, на котором запланирована установка.</span><span class="sxs-lookup"><span data-stu-id="01c8a-142">This REST call can be executed in the context of the site where the install operation should happen.</span></span>

```
url: /_api/web/tenantappcatalog/AvailableApps/GetById('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxx')/Install
method: POST
Authorization: Bearer <access token>
X-RequestDigest: <form digest>
Accept: 'application/json;odata=nometadata'
```

### <a name="upgrade-solution-packages-on-the-sharepoint-site"></a><span data-ttu-id="01c8a-143">Обновление пакета решения на сайте SharePoint</span><span class="sxs-lookup"><span data-stu-id="01c8a-143">Upgrade solution packages on the SharePoint site</span></span>

<span data-ttu-id="01c8a-144">Обновите пакет решения на сайте до более новой версии, доступной в каталоге приложений клиента.</span><span class="sxs-lookup"><span data-stu-id="01c8a-144">Upgrade a solution package from the site to a newer version available in the tenant app catalog.</span></span> <span data-ttu-id="01c8a-145">Этот вызов REST может выполняться в контексте сайта, на котором запланировано обновление.</span><span class="sxs-lookup"><span data-stu-id="01c8a-145">This REST call can be executed in the context of the site where the upgrade operation should happen.</span></span>

```
url: /_api/web/tenantappcatalog/AvailableApps/GetById('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxx')/Upgrade
method: POST
Authorization: Bearer <access token>
X-RequestDigest: <form digest>
Accept: 'application/json;odata=nometadata'
```

### <a name="uninstall-solution-packages-from-the-sharepoint-site"></a><span data-ttu-id="01c8a-146">Удаление пакетов решений с сайта SharePoint</span><span class="sxs-lookup"><span data-stu-id="01c8a-146">Uninstall solution packages from the SharePoint site</span></span>

<span data-ttu-id="01c8a-147">Этот вызов REST может выполняться в контексте сайта, на котором запланировано удаление.</span><span class="sxs-lookup"><span data-stu-id="01c8a-147">This REST call can be executed in the context of the site where the uninstall operation should happen.</span></span>

```
url: /_api/web/tenantappcatalog/AvailableApps/GetById('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxx')/Uninstall
method: POST
Authorization: Bearer <access token>
X-RequestDigest: <form digest>
Accept: 'application/json;odata=nometadata'
```
> [!NOTE]
> <span data-ttu-id="01c8a-148">При удалении пакета решения с сайта с помощью REST API он не перемещается в корзину.</span><span class="sxs-lookup"><span data-stu-id="01c8a-148">When you use the REST API to uninstall a solution package from the site, it is not relocated to the recycle bin.</span></span>


## <a name="sharepoint-pnp-powershell-cmdlets"></a><span data-ttu-id="01c8a-149">Командлеты PowerShell в SharePoint PnP</span><span class="sxs-lookup"><span data-stu-id="01c8a-149">SharePoint PnP PowerShell cmdlets</span></span> 

<span data-ttu-id="01c8a-150">При помощи [PnP PowerShell](https://docs.microsoft.com/en-us/powershell/sharepoint/sharepoint-pnp/sharepoint-pnp-cmdlets?view=sharepoint-ps) вы можете автоматизировать развертывание, публикацию, установку, обновление и отзыв приложений.</span><span class="sxs-lookup"><span data-stu-id="01c8a-150">By using [PnP PowerShell](https://docs.microsoft.com/en-us/powershell/sharepoint/sharepoint-pnp/sharepoint-pnp-cmdlets?view=sharepoint-ps), you can automate deploying, publishing, installing, upgrading, and retracting your apps.</span></span> 

### <a name="add-and-publish-your-app-to-the-app-catalog"></a><span data-ttu-id="01c8a-151">Добавление и публикация приложения в каталоге приложений</span><span class="sxs-lookup"><span data-stu-id="01c8a-151">Add and publish your app to the app catalog</span></span>
<span data-ttu-id="01c8a-152">Добавление приложения (SPPKG, APP) в каталог приложений клиента является обязательным условием для использования этого приложения на сайтах SharePoint.</span><span class="sxs-lookup"><span data-stu-id="01c8a-152">Adding your app (.sppkg file, .app file) to the tenant app catalog is a prerequisite to making your app available for use on your SharePoint sites.</span></span> <span data-ttu-id="01c8a-153">Для этого можно использовать следующий командлет:</span><span class="sxs-lookup"><span data-stu-id="01c8a-153">You can do so by using the following cmdlet:</span></span>

```PowerShell
Add-PnPApp -Path ./myapp.sppkg
```

<span data-ttu-id="01c8a-154">Следующий после добавления шаг — публикация приложения. Так оно будет доступно пользователям вашего клиента.</span><span class="sxs-lookup"><span data-stu-id="01c8a-154">Once added you'll need to continue with publishing your app, effectively making the app available to be used by the users of your tenant.</span></span> <span data-ttu-id="01c8a-155">Ниже на примере командлета PnP PowerShell показано, как это можно сделать.</span><span class="sxs-lookup"><span data-stu-id="01c8a-155">The following PnP PowerShell cmdlet shows how this can be done:</span></span>

```PowerShell
Publish-PnPApp -Identity <app id> -SkipFeatureDeployment
```


> [!NOTE]
> <span data-ttu-id="01c8a-156">Используйте флаг `SkipFeatureDeployment`, чтобы приложение, разработанное для развертывания на уровне клиента, было доступно в этом качестве.</span><span class="sxs-lookup"><span data-stu-id="01c8a-156">Use the `SkipFeatureDeployment` flag to allow an app that was developed for tenant-wide deployment to be actually available as a tenant-wide deployed app.</span></span>



### <a name="remove-the-app-from-the-app-catalog"></a><span data-ttu-id="01c8a-157">Удаление приложения из каталога приложений</span><span class="sxs-lookup"><span data-stu-id="01c8a-157">Remove the app from the app catalog</span></span>

<span data-ttu-id="01c8a-158">Чтобы удалить добавленное ранее приложение, используйте следующий командлет:</span><span class="sxs-lookup"><span data-stu-id="01c8a-158">To remove an app added earlier, use the following cmdlet:</span></span>

```PowerShell
Remove-PnPApp -Identity <app id>
```


### <a name="use-apps-on-your-site"></a><span data-ttu-id="01c8a-159">Использование приложений на сайте</span><span class="sxs-lookup"><span data-stu-id="01c8a-159">Use apps on your site</span></span>

<span data-ttu-id="01c8a-160">Добавив приложение в каталог и опубликовав его, вы можете установить приложение на своем сайте:</span><span class="sxs-lookup"><span data-stu-id="01c8a-160">After the app is added to the app catalog and published, you can install the app to your site:</span></span>

```PowerShell
Install-PnPApp -Identity <app id>
```


<span data-ttu-id="01c8a-161">Обновление приложения:</span><span class="sxs-lookup"><span data-stu-id="01c8a-161">To upgrade the app:</span></span>

```PowerShell
Update-PnPApp -Identity <app id>
```

<span data-ttu-id="01c8a-162">Удаление приложения с сайта:</span><span class="sxs-lookup"><span data-stu-id="01c8a-162">To uninstall the app from your site:</span></span>

```PowerShell
Uninstall-PnPApp -Identity <app id>
```


> [!NOTE]
> <span data-ttu-id="01c8a-163">При удалении приложения с сайта оно удаляется полностью, не попадая в корзину сайта.</span><span class="sxs-lookup"><span data-stu-id="01c8a-163">When you uninstall an app from your site, the app is completely deleted, so it does not end up in the site's recycle bin.</span></span>



### <a name="know-which-apps-are-there-for-you-to-use"></a><span data-ttu-id="01c8a-164">Сведения о доступных приложениях</span><span class="sxs-lookup"><span data-stu-id="01c8a-164">Know which apps are there for you to use</span></span>

<span data-ttu-id="01c8a-165">Вы можете получить список приложений, доступных для добавления на сайт, используя следующий командлет:</span><span class="sxs-lookup"><span data-stu-id="01c8a-165">You can get a list of apps that can be added to the site by using:</span></span>

```PowerShell
Get-PnPApp
```

## <a name="office-365-cli-commands-to-add-deploy-and-manage-sharepoint-apps-cross-platform"></a><span data-ttu-id="01c8a-166">Команды Office 365 CLI для добавления и развертывания приложений SharePoint на нескольких платформах, а также управления ими</span><span class="sxs-lookup"><span data-stu-id="01c8a-166">Office 365 CLI commands to add, deploy, and manage SharePoint apps cross-platform</span></span>

<span data-ttu-id="01c8a-167">При помощи [Office 365 CLI](https://sharepoint.github.io/office365-cli?utm_source=msft_docs&utm_medium=page&utm_campaign=Application+Lifecycle+Management+ALM+APIs) вы можете автоматизировать развертывание, публикацию, установку, обновление и отзыв приложений.</span><span class="sxs-lookup"><span data-stu-id="01c8a-167">Using the [Office 365 CLI](https://sharepoint.github.io/office365-cli?utm_source=msft_docs&utm_medium=page&utm_campaign=Application+Lifecycle+Management+ALM+APIs), you can automate deploying, publishing, installing, upgrading, and retracting your apps.</span></span> <span data-ttu-id="01c8a-168">Office 365 CLI — это межплатформенный интерфейс командной строки, который можно использовать на любой платформе, в том числе Windows, MacOS и Linux.</span><span class="sxs-lookup"><span data-stu-id="01c8a-168">The Office 365 CLI is a cross-platform command-line interface that can be used on any platform, including Windows, MacOS, and Linux.</span></span> <span data-ttu-id="01c8a-169">С дополнительными сведениями об этих командах можно ознакомиться в указанных ниже разделах.</span><span class="sxs-lookup"><span data-stu-id="01c8a-169">To learn more about developing offapplongplur, see the following sections of the documentation:</span></span>

### <a name="add-and-publish-your-app-to-the-app-catalog"></a><span data-ttu-id="01c8a-170">Добавление и публикация приложения в каталоге приложений</span><span class="sxs-lookup"><span data-stu-id="01c8a-170">Add and publish your app to the app catalog</span></span>
<span data-ttu-id="01c8a-171">Добавление приложения (SPPKG, APP) в каталог приложений клиента является обязательным условием для использования этого приложения на сайтах SharePoint.</span><span class="sxs-lookup"><span data-stu-id="01c8a-171">Adding your app (.sppkg file, .app file) to the tenant app catalog is a prerequisite to making your app available for use on your SharePoint sites.</span></span> <span data-ttu-id="01c8a-172">Для этого используйте команду [add](https://sharepoint.github.io/office365-cli/cmd/spo/app/app-add/?utm_source=msft_docs&utm_medium=page&utm_campaign=Application+Lifecycle+Management+ALM+APIs):</span><span class="sxs-lookup"><span data-stu-id="01c8a-172">Use the [add](https://sharepoint.github.io/office365-cli/cmd/spo/app/app-add/?utm_source=msft_docs&utm_medium=page&utm_campaign=Application+Lifecycle+Management+ALM+APIs) command to do this:</span></span>

```shell
spo app add --filePath ./spfx.sppkg
```

<span data-ttu-id="01c8a-173">Следующий после добавления шаг — публикация приложения. Так оно будет доступно пользователям вашего клиента.</span><span class="sxs-lookup"><span data-stu-id="01c8a-173">Once added you'll need to continue with publishing your app, effectively making the app available to be used by the users of your tenant.</span></span> <span data-ttu-id="01c8a-174">Опубликовать приложение можно с помощью команды [deploy](https://sharepoint.github.io/office365-cli/cmd/spo/app/app-deploy/?utm_source=msft_docs&utm_medium=page&utm_campaign=Application+Lifecycle+Management+ALM+APIs):</span><span class="sxs-lookup"><span data-stu-id="01c8a-174">Use the [deploy](https://sharepoint.github.io/office365-cli/cmd/spo/app/app-deploy/?utm_source=msft_docs&utm_medium=page&utm_campaign=Application+Lifecycle+Management+ALM+APIs) command to do this:</span></span>

```shell
spo app deploy --id <app id> --skipFeatureDeployment
```


> [!NOTE]
> <span data-ttu-id="01c8a-175">Используйте флажок **SkipFeatureDeployment**, чтобы приложение, разработанное для развертывания на уровне клиента, было фактически доступно в этом качестве.</span><span class="sxs-lookup"><span data-stu-id="01c8a-175">Use the **** flag to allow an app that was developed for tenant-wide deployment to be actually available as a tenant-wide deployed app.</span></span>



### <a name="remove-the-app-from-the-app-catalog"></a><span data-ttu-id="01c8a-176">Удаление приложения из каталога приложений</span><span class="sxs-lookup"><span data-stu-id="01c8a-176">Remove the app from the app catalog</span></span>
<span data-ttu-id="01c8a-177">Вам может потребоваться удалить добавленное ранее приложение. Это можно сделать с помощью команды [remove](https://sharepoint.github.io/office365-cli/cmd/spo/app/app-remove/?utm_source=msft_docs&utm_medium=page&utm_campaign=Application+Lifecycle+Management+ALM+APIs):</span><span class="sxs-lookup"><span data-stu-id="01c8a-177">You may want to remove an app that you added earlier, and you can do this by using the [remove](https://sharepoint.github.io/office365-cli/cmd/spo/app/app-remove/?utm_source=msft_docs&utm_medium=page&utm_campaign=Application+Lifecycle+Management+ALM+APIs) command:</span></span>

```shell
spo app remove --id <app id>
```


### <a name="use-apps-on-your-site"></a><span data-ttu-id="01c8a-178">Использование приложений на сайте</span><span class="sxs-lookup"><span data-stu-id="01c8a-178">Use apps on your site</span></span>
<span data-ttu-id="01c8a-179">Добавив приложение в каталог и опубликовав его, вы можете установить приложение на своем сайте с помощью команды [install](https://sharepoint.github.io/office365-cli/cmd/spo/app/app-install/?utm_source=msft_docs&utm_medium=page&utm_campaign=Application+Lifecycle+Management+ALM+APIs):</span><span class="sxs-lookup"><span data-stu-id="01c8a-179">After the app is added to the app catalog and published, you can install the app to your site:</span></span>

```shell
spo app install --id <app id> --siteUrl <url>
```


<span data-ttu-id="01c8a-180">Для обновления приложения используйте команду [upgrade](https://sharepoint.github.io/office365-cli/cmd/spo/app/app-upgrade/?utm_source=msft_docs&utm_medium=page&utm_campaign=Application+Lifecycle+Management+ALM+APIs):</span><span class="sxs-lookup"><span data-stu-id="01c8a-180">To upgrade the app, use the [upgrade](https://sharepoint.github.io/office365-cli/cmd/spo/app/app-upgrade/?utm_source=msft_docs&utm_medium=page&utm_campaign=Application+Lifecycle+Management+ALM+APIs) command:</span></span>

```shell
spo app upgrade --id <app id> --siteUrl <url>
```


<span data-ttu-id="01c8a-181">С помощью команды [uninstall](https://sharepoint.github.io/office365-cli/cmd/spo/app/app-uninstall/?utm_source=msft_docs&utm_medium=page&utm_campaign=Application+Lifecycle+Management+ALM+APIs) можно удалить приложение с сайта:</span><span class="sxs-lookup"><span data-stu-id="01c8a-181">To uninstall the app from your site, use the [uninstall](https://sharepoint.github.io/office365-cli/cmd/spo/app/app-uninstall/?utm_source=msft_docs&utm_medium=page&utm_campaign=Application+Lifecycle+Management+ALM+APIs) command:</span></span>

```shell
spo app uninstall --id <app id> --siteUrl <url>
```


> [!NOTE]
> <span data-ttu-id="01c8a-182">При этом оно удаляется полностью, поэтому не попадает в корзину сайта.</span><span class="sxs-lookup"><span data-stu-id="01c8a-182">When you uninstall an app from your site the app is completely deleted, so it will not end up in the site's recycle bin.</span></span>


### <a name="list-and-get-apps-in-the-app-catalog"></a><span data-ttu-id="01c8a-183">Перечисление приложений в каталоге и их получение</span><span class="sxs-lookup"><span data-stu-id="01c8a-183">List and get apps in the app catalog</span></span>
<span data-ttu-id="01c8a-184">С помощью команды [list](https://sharepoint.github.io/office365-cli/cmd/spo/app/app-list/?utm_source=msft_docs&utm_medium=page&utm_campaign=Application+Lifecycle+Management+ALM+APIs) можно узнать, какие приложения были добавлены в каталог:</span><span class="sxs-lookup"><span data-stu-id="01c8a-184">You can see what apps have been added to the app catalog by using the [list](https://sharepoint.github.io/office365-cli/cmd/spo/app/app-list/?utm_source=msft_docs&utm_medium=page&utm_campaign=Application+Lifecycle+Management+ALM+APIs) command:</span></span>

```shell
spo app list
```


<span data-ttu-id="01c8a-185">Чтобы получить сведения об отдельном приложении, используйте команду [get](https://sharepoint.github.io/office365-cli/cmd/spo/app/app-get/?utm_source=msft_docs&utm_medium=page&utm_campaign=Application+Lifecycle+Management+ALM+APIs):</span><span class="sxs-lookup"><span data-stu-id="01c8a-185">You can get a single app's details by using the [get](https://sharepoint.github.io/office365-cli/cmd/spo/app/app-get/?utm_source=msft_docs&utm_medium=page&utm_campaign=Application+Lifecycle+Management+ALM+APIs) command:</span></span>

```shell
spo app get --id <app id>
```

## <a name="see-also"></a><span data-ttu-id="01c8a-186">См. также</span><span class="sxs-lookup"><span data-stu-id="01c8a-186">See also</span></span>

- [<span data-ttu-id="01c8a-187">Знакомство со службой REST в SharePoint</span><span class="sxs-lookup"><span data-stu-id="01c8a-187">Get to know the SharePoint REST service</span></span>](../sp-add-ins/get-to-know-the-sharepoint-rest-service.md)
