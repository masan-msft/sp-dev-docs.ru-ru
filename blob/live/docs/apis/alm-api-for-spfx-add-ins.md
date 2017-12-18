# <a name="application-lifecycle-management-alm-apis"></a><span data-ttu-id="820f4-101">API управления жизненным циклом приложений (ALM)</span><span class="sxs-lookup"><span data-stu-id="820f4-101">Application Lifecycle Management (ALM) APIs</span></span>  

<span data-ttu-id="820f4-102">API управления жизненным циклом приложений — простые API-интерфейсы для управления развертыванием решений и надстроек SharePoint Framework в клиенте.</span><span class="sxs-lookup"><span data-stu-id="820f4-102">ALM APIs are providing simple APIs to manage deployment of your SharePoint Framework solutions and add-ins cross your tenant.</span></span> <span data-ttu-id="820f4-103">Эти API поддерживают приведенные ниже возможности.</span><span class="sxs-lookup"><span data-stu-id="820f4-103">ALM APIs support following capabilities.</span></span>

- <span data-ttu-id="820f4-104">Добавление решения SharePoint Framework или надстройки SharePoint в каталог приложений клиента.</span><span class="sxs-lookup"><span data-stu-id="820f4-104">Add SharePoint Framework solution or SharePoint add-in to tenant app catalog</span></span>
- <span data-ttu-id="820f4-105">Обеспечение доступности решения SharePoint Framework или надстройки SharePoint для установки в каталоге приложений клиента.</span><span class="sxs-lookup"><span data-stu-id="820f4-105">Enable SharePoint Framework solution or SharePoint add-in to be available for installation in tenant app catalog</span></span>
- <span data-ttu-id="820f4-106">Отключение возможности установки решения SharePoint Framework или надстройки SharePoint в каталоге приложений клиента.</span><span class="sxs-lookup"><span data-stu-id="820f4-106">Disable SharePoint Framework solution or SharePoint add-in not to be available for installation in tenant app catalog</span></span>
- <span data-ttu-id="820f4-107">Установка решения SharePoint Framework или надстройки SharePoint из каталога приложений клиента на сайте.</span><span class="sxs-lookup"><span data-stu-id="820f4-107">Install SharePoint Framework solution or SharePoint add-in from tenant app catalog to a site</span></span>
- <span data-ttu-id="820f4-108">Обновление решения SharePoint Framework или надстройки SharePoint для использования на сайте с более поздней версией, доступной в каталоге приложений клиента.</span><span class="sxs-lookup"><span data-stu-id="820f4-108">Upgrade SharePoint Framework solution or SharePoint add-in to a site, which has a newer version available in the tenant app catalog</span></span>
- <span data-ttu-id="820f4-109">Удаление решения SharePoint Framework или надстройки SharePoint с сайта.</span><span class="sxs-lookup"><span data-stu-id="820f4-109">Uninstall SharePoint Framework solution or SharePoint add-in from the site</span></span>

<span data-ttu-id="820f4-110">API управления жизненным циклом приложений можно использовать для выполнения тех же операций, которые доступны для пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="820f4-110">ALM APIs can be used to perform exactly the same operations which are available from UI perspective.</span></span> <span data-ttu-id="820f4-111">При использовании этих API выполняются все типичные действия.</span><span class="sxs-lookup"><span data-stu-id="820f4-111">When these APIs are used, all typical actions will be performed.</span></span> <span data-ttu-id="820f4-112">Ниже описаны некоторые характеристики API ALM.</span><span class="sxs-lookup"><span data-stu-id="820f4-112">Here are some of the characteristics for ALM APIs.</span></span>

- <span data-ttu-id="820f4-113">При выполнении соответствующих операций происходят события установки и удаления надстроек, размещаемых у поставщика.</span><span class="sxs-lookup"><span data-stu-id="820f4-113">Install and UnInstall events are being fired for provider hosted add-ins when corresponding operations are occurred</span></span>
- <span data-ttu-id="820f4-114">API ALM поддерживают операции только для приложений.</span><span class="sxs-lookup"><span data-stu-id="820f4-114">ALM APIs supports app-only based operations</span></span>

<span data-ttu-id="820f4-115">API ALM изначально предоставляются с использованием REST API, но есть дополнительные расширения CSOM и командлеты PowerShell, доступные благодаря SharePoint PnP.</span><span class="sxs-lookup"><span data-stu-id="820f4-115">ALM APIs are natively provided using REST APIs, but there is also additional CSOM extensions and PowerShell commandlets available through SharePoint Patterns and Practices</span></span> 

## <a name="rest-api"></a><span data-ttu-id="820f4-116">REST API</span><span class="sxs-lookup"><span data-stu-id="820f4-116">REST API</span></span>

### <a name="add-solution-package-to-tenant-app-catalog"></a><span data-ttu-id="820f4-117">Добавление пакета решения в каталог приложений клиента</span><span class="sxs-lookup"><span data-stu-id="820f4-117">Add solution package to tenant app catalog</span></span> 

<span data-ttu-id="820f4-118">Добавление решения в каталог приложений клиента.</span><span class="sxs-lookup"><span data-stu-id="820f4-118">Adding solution to the tenant app catalog.</span></span> <span data-ttu-id="820f4-119">Этот API разработан для выполнения в контексте сайта каталога приложений клиента.</span><span class="sxs-lookup"><span data-stu-id="820f4-119">This API is designed to be executed in the context of the tenant app catalog site.</span></span>

```
/_api/web/tenantappcatalog/Add(overwrite=true, url='test.txt')";
method: POST
binaryStringRequestBody: true
body: 'byte array of the file'
```

### <a name="deploy-solution-package-in-tenant-app-catalog"></a><span data-ttu-id="820f4-120">Развертывание пакета решения в каталоге приложений клиента</span><span class="sxs-lookup"><span data-stu-id="820f4-120">Deploy solution package in tenant app catalog</span></span>

<span data-ttu-id="820f4-121">Обеспечение возможности установить решение на определенных сайтах.</span><span class="sxs-lookup"><span data-stu-id="820f4-121">Enable solution to be available to install to specific sites.</span></span> <span data-ttu-id="820f4-122">Этот API разработан для выполнения в контексте сайта каталога приложений клиента.</span><span class="sxs-lookup"><span data-stu-id="820f4-122">This API is designed to be executed in the context of the tenant app catalog site.</span></span>

```
/_api/web/tenantappcatalog/AvailableApps/GetById('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxx')/Deploy";
```

> [!NOTE]
> <span data-ttu-id="820f4-123">Эта операция должна быть завершена после добавления, прежде чем вы сможете устанавливать пакеты на определенные сайты.</span><span class="sxs-lookup"><span data-stu-id="820f4-123">This operation is required to be completed after add, before you can install packages to specific sites.</span></span> 

### <a name="retract-solution-package-in-the-tenant-app-catalog"></a><span data-ttu-id="820f4-124">Отзыв пакета решения в каталоге приложений клиента</span><span class="sxs-lookup"><span data-stu-id="820f4-124">Retract solution package in the tenant app catalog</span></span>

<span data-ttu-id="820f4-125">Отзыв решения для отмены его доступности на сайтах.</span><span class="sxs-lookup"><span data-stu-id="820f4-125">Retract solution to be available from the sites.</span></span> <span data-ttu-id="820f4-126">Этот API разработан для выполнения в контексте сайта каталога приложений клиента.</span><span class="sxs-lookup"><span data-stu-id="820f4-126">This API is designed to be executed in the context of the tenant app catalog site.</span></span>

```
/_api/web/tenantappcatalog/AvailableApps/GetById('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxx')/Retract";
```

> [!NOTE]
> <span data-ttu-id="820f4-127">Если вы запустите эту операцию уже после установки решений на сайте, они перестанут работать, так как на уровне клиента решения отключены.</span><span class="sxs-lookup"><span data-stu-id="820f4-127">If you run this operation after you have already installed solutions to site, they will stop working since solution is disabled from the tenant level.</span></span>

### <a name="remove-solution-package-from-tenant-app-catalog"></a><span data-ttu-id="820f4-128">Удаление пакета решения из каталога приложений клиента</span><span class="sxs-lookup"><span data-stu-id="820f4-128">Remove solution package from tenant app catalog</span></span>

<span data-ttu-id="820f4-129">Удаляет пакет решения из каталога приложений клиента.</span><span class="sxs-lookup"><span data-stu-id="820f4-129">Remove the solution package from the tenant app catalog.</span></span> <span data-ttu-id="820f4-130">Этот API разработан для выполнения в контексте сайта каталога приложений клиента.</span><span class="sxs-lookup"><span data-stu-id="820f4-130">This API is designed to be executed in the context of the tenant app catalog site.</span></span>

```
/_api/web/tenantappcatalog/AvailableApps/GetById('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxx')/Remove";
```

> [!NOTE]
> <span data-ttu-id="820f4-131">Решение также будет автоматически отозвано, если эта операция не была выполнена до операции удаления.</span><span class="sxs-lookup"><span data-stu-id="820f4-131">Solution will be also automatically retracted, if that operation has not performed before Remove operation.</span></span>

### <a name="list-available-packages-from-tenant-app-catalog"></a><span data-ttu-id="820f4-132">Перечисление доступных пакетов из каталога приложений клиента</span><span class="sxs-lookup"><span data-stu-id="820f4-132">List available packages from tenant app catalog</span></span>

<span data-ttu-id="820f4-133">REST API для получения списка доступных надстроек или решений SharePoint Framework в каталоге приложений клиента.</span><span class="sxs-lookup"><span data-stu-id="820f4-133">REST API for getting list of available SharePoint Framework solutions or add-ins in tenant app catalog.</span></span>

```
url: /_api/web/tenantappcatalog/AvailableApps
method: GET
```

### <a name="details-on-individual-solution-package-from-tenant-app-catalog"></a><span data-ttu-id="820f4-134">Сведения об отдельном пакете решения из каталога приложений клиента</span><span class="sxs-lookup"><span data-stu-id="820f4-134">Details on individual solution package from tenant app catalog</span></span>

<span data-ttu-id="820f4-135">REST API для получения сведений об отдельных надстройках или решениях SharePoint Framework, которые доступны в каталоге приложений клиента.</span><span class="sxs-lookup"><span data-stu-id="820f4-135">REST API for getting details on individual SharePoint Framework solution or add-in available in the tenant app catalog.</span></span>

```
url: /_api/web/tenantappcatalog/AvailableApps/GetById('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxx')
method: GET
```

### <a name="install-solution-package-from-tenant-app-catalog-to-sharepoint-site"></a><span data-ttu-id="820f4-136">Установка пакета решения из каталога приложений клиента на сайте SharePoint</span><span class="sxs-lookup"><span data-stu-id="820f4-136">Install solution package from tenant app catalog to SharePoint site</span></span>

<span data-ttu-id="820f4-137">Установка пакета решения с определенным идентификатором из каталога приложений клиента на сайте с учетом контекста URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="820f4-137">Install a solution package with specific identifier from tenant app catalog to the site based on URL context.</span></span> <span data-ttu-id="820f4-138">Вызов REST может быть выполнен в контексте сайта, на котором должна выполняться операция установки.</span><span class="sxs-lookup"><span data-stu-id="820f4-138">This REST call can be executed in the context of the site where the install operation should happen.</span></span>

```
url: /_api/web/tenantappcatalog/AvailableApps/GetById('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxx')/Install";
method: POST
```

### <a name="upgrade-solution-package-in-sharepoint-site"></a><span data-ttu-id="820f4-139">Обновление пакета решения на сайте SharePoint</span><span class="sxs-lookup"><span data-stu-id="820f4-139">Upgrade solution package in SharePoint site</span></span>

<span data-ttu-id="820f4-140">Обновление пакета решения с сайта до более новой версии, доступной в каталоге приложений клиента.</span><span class="sxs-lookup"><span data-stu-id="820f4-140">Upgrade a solution package from the site to a newer version available in the tenant app catalog.</span></span> <span data-ttu-id="820f4-141">Вызов REST может быть выполнен в контексте сайта, на котором должна выполняться операция обновления.</span><span class="sxs-lookup"><span data-stu-id="820f4-141">This REST call can be executed in the context of the site where the upgrade operation should happen.</span></span>

```
url: /_api/web/tenantappcatalog/AvailableApps/GetById('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxx')/Upgrade";
method: POST
```

### <a name="uninstall-solution-package-from-sharepoint-site"></a><span data-ttu-id="820f4-142">Удаление пакета решения с сайта SharePoint</span><span class="sxs-lookup"><span data-stu-id="820f4-142">Uninstall solution package from SharePoint site</span></span>

<span data-ttu-id="820f4-143">Удаление пакета решения с сайта.</span><span class="sxs-lookup"><span data-stu-id="820f4-143">Uninstall a solution package from the site.</span></span> <span data-ttu-id="820f4-144">Вызов REST может быть выполнен в контексте сайта, на котором должна выполняться операция удаления.</span><span class="sxs-lookup"><span data-stu-id="820f4-144">This REST call can be executed in the context of the site where the uninstall operation should happen.</span></span>

```
url: /_api/web/tenantappcatalog/AvailableApps/GetById('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxx')/Uninstall";
method: POST
```
> [!NOTE]
> <span data-ttu-id="820f4-145">Когда вы используете REST API для удаления пакета решения с сайта, он не перемещается в корзину.</span><span class="sxs-lookup"><span data-stu-id="820f4-145">When you use the REST API to uninstall solution package from the site, it is not relocated to the recycle bin.</span></span>


## <a name="sharepoint-pnp-powershell-cmdlets-to-programmatically-add-and-deploy-sharepoint-apps"></a><span data-ttu-id="820f4-146">Командлеты PnP PowerShell SharePoint для добавления и развертывания приложений SharePoint программным способом</span><span class="sxs-lookup"><span data-stu-id="820f4-146">SharePoint PnP PowerShell cmdlets to programmatically add and deploy SharePoint Apps</span></span>

<span data-ttu-id="820f4-147">При помощи [PnP PowerShell](https://msdn.microsoft.com/ru-RU/pnp_powershell/pnp-powershell-overview) вы можете автоматизировать развертывание, публикацию, установку, обновление и отзыв приложений.</span><span class="sxs-lookup"><span data-stu-id="820f4-147">Using [PnP PowerShell](https://msdn.microsoft.com/ru-RU/pnp_powershell/pnp-powershell-overview) you can automate the deployment, publishing, installing, upgrading and retracting your apps.</span></span> <span data-ttu-id="820f4-148">Дополнительные сведения об этих командлетах вы найдете в приведенном ниже разделе.</span><span class="sxs-lookup"><span data-stu-id="820f4-148">Checkout below chapter to learn more about this cmdlets.</span></span>

### <a name="adding-and-publishing-your-app-to-the-app-catalog"></a><span data-ttu-id="820f4-149">Добавление и публикация приложения в каталоге приложений</span><span class="sxs-lookup"><span data-stu-id="820f4-149">Adding and publishing your app to the app catalog</span></span>
<span data-ttu-id="820f4-150">Добавление приложения (.sppkg, .app) в каталог приложений клиента является обязательным условием для дальнейшего использования этого приложения на сайтах SharePoint.</span><span class="sxs-lookup"><span data-stu-id="820f4-150">Adding your app (.sppkg file, .app file) to the tenant app catalog is a per-requisite to later on make your app available for use in your SharePoint sites.</span></span> <span data-ttu-id="820f4-151">Это можно сделать с помощью приведенного ниже простого командлета.</span><span class="sxs-lookup"><span data-stu-id="820f4-151">Doing so can be done using below simple cmdlet:</span></span>

```PowerShell
Add-PnPApp -Path ./myapp.sppkg"
```

<span data-ttu-id="820f4-152">Следующий после добавления шаг — публикация приложения. Так оно будет доступно пользователям вашего клиента.</span><span class="sxs-lookup"><span data-stu-id="820f4-152">Once added you'll need to continue with publishing your app, effectively making the app available to be used by the users of your tenant.</span></span> <span data-ttu-id="820f4-153">Ниже на примере командлета PnP PowerShell показано, как это можно сделать.</span><span class="sxs-lookup"><span data-stu-id="820f4-153">Below PnP PowerShell cmdlets shows how this can be done:</span></span>

```PowerShell
Publish-PnPApp -Identity <app id> -SkipFeatureDeployment
```


> [!NOTE]
> <span data-ttu-id="820f4-154">Используйте флажок SkipFeatureDeployment, чтобы приложение, разработанное для развертывания на уровне клиента, было фактически доступно в этом качестве.</span><span class="sxs-lookup"><span data-stu-id="820f4-154">Use the SkipFeatureDeployment flag to allow an app that was developed for tenant wide deployment to be actually available as a tenant wide deployed app.</span></span>



### <a name="removing-the-app-from-the-app-catalog"></a><span data-ttu-id="820f4-155">Удаление приложения из каталога приложений</span><span class="sxs-lookup"><span data-stu-id="820f4-155">Removing the app from the app catalog</span></span>
<span data-ttu-id="820f4-156">Вы также можете удалить ранее добавленное приложение с помощью приведенного ниже командлета.</span><span class="sxs-lookup"><span data-stu-id="820f4-156">Obviously you might also want to remove an earlier added app and that can be done using the following cmdlet:</span></span>

```PowerShell
Remove-PnPApp -Identity <app id>
```


### <a name="using-apps-on-your-site"></a><span data-ttu-id="820f4-157">Использование приложений на сайте</span><span class="sxs-lookup"><span data-stu-id="820f4-157">Using apps on your site</span></span>
<span data-ttu-id="820f4-158">После добавления приложения в каталог приложений и его публикации вы можете установить это приложение на своем сайте.</span><span class="sxs-lookup"><span data-stu-id="820f4-158">Once the app was added to the app catalog and published you can continue with installing the app to your site.</span></span>

```PowerShell
Install-PnPApp -Identity <app id>
```


<span data-ttu-id="820f4-159">Добавленное приложение следует обновить:</span><span class="sxs-lookup"><span data-stu-id="820f4-159">An added app also needs be upgraded:</span></span>

```PowerShell
Update-PnPApp -Identity <app id>
```


<span data-ttu-id="820f4-160">Затем приложение можно снова удалить с сайта:</span><span class="sxs-lookup"><span data-stu-id="820f4-160">And you off course also uninstall the app again from your site:</span></span>

```PowerShell
Uninstall-PnPApp -Identity <app id>
```


> [!NOTE]
> <span data-ttu-id="820f4-161">При удалении приложения с сайта оно удаляется полностью, поэтому не попадает в корзину сайта.</span><span class="sxs-lookup"><span data-stu-id="820f4-161">When you uninstall an app from your site the app is completely deleted, so it will not end up in the site's recycle bin.</span></span>



### <a name="knowing-which-apps-are-there-for-you-to-use"></a><span data-ttu-id="820f4-162">Информация о доступных приложениях</span><span class="sxs-lookup"><span data-stu-id="820f4-162">Knowing which apps are there for you to use</span></span>
<span data-ttu-id="820f4-163">При помощи приведенного ниже командлета вы получите список приложений, которые можно добавить на сайт.</span><span class="sxs-lookup"><span data-stu-id="820f4-163">Getting a list of apps that can be added to the site is possible using:</span></span>

```PowerShell
Get-PnPAvailableApp
```
