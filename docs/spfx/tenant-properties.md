---
title: "Свойства клиента SharePoint Online"
description: "Управляйте свойствами клиента, которые позволяют администраторам добавлять свойства в каталог приложений для различных компонентов SharePoint Framework."
ms.date: 02/02/2018
ms.prod: sharepoint
ms.openlocfilehash: 3ef0906645da5479fcac8e5f2f188063283300ee
ms.sourcegitcommit: 4e65e89f3ad8ef1d953e2fdd04d7ab5c0e7df174
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/27/2018
---
# <a name="sharepoint-online-tenant-properties"></a><span data-ttu-id="fb28a-103">Свойства клиента SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="fb28a-103">SharePoint Online tenant properties</span></span>

<span data-ttu-id="fb28a-104">Свойства клиента позволяют администраторам добавлять свойства в каталог приложений для различных компонентов SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="fb28a-104">Tenant properties allow tenant administrators to add properties in the App Catalog that can be read by various SharePoint Framework components.</span></span> <span data-ttu-id="fb28a-105">Для управления свойствами клиента администраторы клиента используют [командную консоль Microsoft SharePoint Online](https://technet.microsoft.com/ru-RU/library/fp161372.aspx). Это модуль PowerShell для управления подпиской на SharePoint Online в Office 365.</span><span class="sxs-lookup"><span data-stu-id="fb28a-105">The tenant properties are managed by tenant administrators by using the [Microsoft SharePoint Online Management Shell](https://technet.microsoft.com/ru-RU/library/fp161372.aspx), which is a PowerShell module to manage your SharePoint Online subscription in Office 365.</span></span>

<span data-ttu-id="fb28a-106">Для управления свойствами клиента также можно использовать [Office 365 CLI](https://sharepoint.github.io/office365-cli?utm_source=msft_docs&utm_medium=page&utm_campaign=Use+SharePoint+Online+tenant+properties).</span><span class="sxs-lookup"><span data-stu-id="fb28a-106">Alternatively, the [Office 365 CLI](https://sharepoint.github.io/office365-cli?utm_source=msft_docs&utm_medium=page&utm_campaign=Use+SharePoint+Online+tenant+properties) can be used to manage the tenant properties.</span></span> <span data-ttu-id="fb28a-107">Office 365 CLI — это межплатформенный интерфейс командной строки, который можно использовать на любой платформе, в том числе Windows, MacOS и Linux.</span><span class="sxs-lookup"><span data-stu-id="fb28a-107">The Office 365 CLI is a cross-platform command line interface that can be used on any platform, including Windows, MacOS and Linux.</span></span>

## <a name="manage-tenant-properties"></a><span data-ttu-id="fb28a-108">Управление свойствами клиента</span><span class="sxs-lookup"><span data-stu-id="fb28a-108">Manage tenant properties</span></span>

<span data-ttu-id="fb28a-109">С помощью [командной консоли Microsoft SharePoint Online](https://www.microsoft.com/en-us/download/details.aspx?id=35588) администраторы клиента могут добавлять и удалять свойства клиента через PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fb28a-109">Using the [Microsoft SharePoint Online Management Shell](https://www.microsoft.com/en-us/download/details.aspx?id=35588), tenant administrators can use PowerShell to add and remove tenant properties.</span></span> 

<span data-ttu-id="fb28a-110">Ниже приведены командлеты PowerShell для управления свойствами клиента.</span><span class="sxs-lookup"><span data-stu-id="fb28a-110">The following PowerShell cmdlets are available to manage the tenant properties.</span></span> <span data-ttu-id="fb28a-111">Так как свойства клиента хранятся в каталоге приложений клиента, в приведенных ниже командлетах нужно указать URL-адрес семейства веб-сайтов с каталогом приложений клиента.</span><span class="sxs-lookup"><span data-stu-id="fb28a-111">Because tenant properties are stored in the tenant App Catalog, you must provide the tenant App Catalog site collection URL in the following cmdlets.</span></span>

<span data-ttu-id="fb28a-112">Прежде чем запускать приведенный ниже скрипт, подключитесь к клиенту SharePoint Online, используя командлет `Connect-SPOService` в SharePoint Online PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fb28a-112">Before running the following script, connect to your SharePoint Online tenant using the `Connect-SPOService` cmdlet.</span></span>

### <a name="get-spostorageentity"></a><span data-ttu-id="fb28a-113">Get-SPOStorageEntity</span><span class="sxs-lookup"><span data-stu-id="fb28a-113">Get-SPOStorageEntity</span></span>

- <span data-ttu-id="fb28a-114">**Область применения:** Office 365, SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="fb28a-114">**Applies to** Office 365, SharePoint Online</span></span>

- <span data-ttu-id="fb28a-115">**Синтаксис** Get-SPOStorageEntity [-Site] <AppCatalogSiteURL> [-Key] <String></span><span class="sxs-lookup"><span data-stu-id="fb28a-115">**Syntax** Get-SPOStorageEntity [-Site] <AppCatalogSiteURL> [-Key] <String></span></span>

### <a name="set-spostorageentity"></a><span data-ttu-id="fb28a-116">Set-SPOStorageEntity</span><span class="sxs-lookup"><span data-stu-id="fb28a-116">Set-SPOStorageEntity</span></span>

- <span data-ttu-id="fb28a-117">**Область применения:** Office 365, SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="fb28a-117">**Applies to** Office 365, SharePoint Online</span></span>

- <span data-ttu-id="fb28a-118">**Синтаксис** Set-SPOStorageEntity [-Site] <AppCatalogSiteURL> [-Key] <String> [-Value] <String> [-Description] <String> [-Comments] <String></span><span class="sxs-lookup"><span data-stu-id="fb28a-118">**Syntax** Set-SPOStorageEntity [-Site] <AppCatalogSiteURL> [-Key] <String> [-Value] <String> [-Description] <String> [-Comments] <String></span></span>

### <a name="remove-spostorageentity"></a><span data-ttu-id="fb28a-119">Remove-SPOStorageEntity</span><span class="sxs-lookup"><span data-stu-id="fb28a-119">Remove-SPOStorageEntity</span></span>

- <span data-ttu-id="fb28a-120">**Область применения:** Office 365, SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="fb28a-120">**Applies to** Office 365, SharePoint Online</span></span>

- <span data-ttu-id="fb28a-121">**Синтаксис** Remove-SPOStorageEntity [-Site] <AppCatalogSiteURL> [-Key] <String></span><span class="sxs-lookup"><span data-stu-id="fb28a-121">**Syntax** Remove-SPOStorageEntity [-Site] <AppCatalogSiteURL> [-Key] <String></span></span>

## <a name="office-365-cli-commands-to-get-set-remove-and-list-tenant-properties-cross-platform"></a><span data-ttu-id="fb28a-122">Команды Office 365 CLI для получения, задания, удаления и отображения свойств клиента на любой платформе</span><span class="sxs-lookup"><span data-stu-id="fb28a-122">Office 365 CLI commands to get, set, remove and list tenant properties cross-platform</span></span>

<span data-ttu-id="fb28a-123">Используя [Office 365 CLI](https://sharepoint.github.io/office365-cli?utm_source=msft_docs&utm_medium=page&utm_campaign=Use+SharePoint+Online+tenant+properties), администраторы клиента могут управлять свойствами клиента с помощью команд оболочки.</span><span class="sxs-lookup"><span data-stu-id="fb28a-123">Using the [Office 365 CLI](https://sharepoint.github.io/office365-cli?utm_source=msft_docs&utm_medium=page&utm_campaign=Use+SharePoint+Online+tenant+properties), tenant administrators can use shell commands to manage tenant properties.</span></span>

<span data-ttu-id="fb28a-124">Прежде чем использовать команды, подключитесь к сайту SharePoint Online с помощью команды `spo connect`.</span><span class="sxs-lookup"><span data-stu-id="fb28a-124">Before using the commands, connect to a SharePoint Online site, using the `spo connect` command.</span></span>

### <a name="get-details-for-the-specified-tenant-property"></a><span data-ttu-id="fb28a-125">Получение сведений об указанном свойстве клиента</span><span class="sxs-lookup"><span data-stu-id="fb28a-125">Get details for the specified tenant property</span></span>

<span data-ttu-id="fb28a-126">Команду [spo storageentity get](https://sharepoint.github.io/office365-cli/cmd/spo/storageentity/storageentity-get/?utm_source=msft_docs&utm_medium=page&utm_campaign=Use+SharePoint+Online+tenant+properties) можно использовать для получения сведений о свойстве клиента Office 365 или SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="fb28a-126">The [spo storageentity get](https://sharepoint.github.io/office365-cli/cmd/spo/storageentity/storageentity-get/?utm_source=msft_docs&utm_medium=page&utm_campaign=Use+SharePoint+Online+tenant+properties) command can be used to get details for Office 365, SharePoint Online tenant property</span></span>

```shell
spo storageentity get --key <key>
```

### <a name="list-tenant-properties-stored-on-the-specified-sharepoint-online-app-catalog"></a><span data-ttu-id="fb28a-127">Отображение свойств клиента, хранящихся в указанном каталоге приложений SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="fb28a-127">List tenant properties stored on the specified SharePoint Online app catalog</span></span>

<span data-ttu-id="fb28a-128">Команду [spo storageentity list](https://sharepoint.github.io/office365-cli/cmd/spo/storageentity/storageentity-list/?utm_source=msft_docs&utm_medium=page&utm_campaign=Use+SharePoint+Online+tenant+properties) можно использовать для отображения всех свойств клиента.</span><span class="sxs-lookup"><span data-stu-id="fb28a-128">The [spo storageentity list](https://sharepoint.github.io/office365-cli/cmd/spo/storageentity/storageentity-list/?utm_source=msft_docs&utm_medium=page&utm_campaign=Use+SharePoint+Online+tenant+properties) command can be used to list all the tenant properties.</span></span>

```shell
spo storageentity list --appCatalogUrl <appCatalogUrl>
```

### <a name="set-tenant-property-on-a-specified-sharepoint-online-app-catalog"></a><span data-ttu-id="fb28a-129">Задание свойства клиента в указанном каталоге приложений SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="fb28a-129">Set tenant property on a specified SharePoint Online app catalog</span></span>

<span data-ttu-id="fb28a-130">Команду [spo storageentity set](https://sharepoint.github.io/office365-cli/cmd/spo/storageentity/storageentity-set/?utm_source=msft_docs&utm_medium=page&utm_campaign=Use+SharePoint+Online+tenant+properties) можно использовать для задания свойства клиента.</span><span class="sxs-lookup"><span data-stu-id="fb28a-130">The [spo storageentity set](https://sharepoint.github.io/office365-cli/cmd/spo/storageentity/storageentity-set/?utm_source=msft_docs&utm_medium=page&utm_campaign=Use+SharePoint+Online+tenant+properties) command can be used to set tenant property</span></span>

```shell
spo storageentity set --appCatalogUrl <appCatalogUrl> --key <key> --value <value>
```

### <a name="remove-tenant-property-stored-on-the-specified-sharepoint-online-app-catalog"></a><span data-ttu-id="fb28a-131">Удаление свойства клиента, хранящегося в указанном каталоге приложений SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="fb28a-131">Remove tenant property stored on the specified SharePoint Online app catalog</span></span>

<span data-ttu-id="fb28a-132">Команду [spo storageentity remove](https://sharepoint.github.io/office365-cli/cmd/spo/storageentity/storageentity-remove/?utm_source=msft_docs&utm_medium=page&utm_campaign=Use+SharePoint+Online+tenant+properties) можно использовать для удаления свойства клиента.</span><span class="sxs-lookup"><span data-stu-id="fb28a-132">The [spo storageentity remove](https://sharepoint.github.io/office365-cli/cmd/spo/storageentity/storageentity-remove/?utm_source=msft_docs&utm_medium=page&utm_campaign=Use+SharePoint+Online+tenant+properties) command can be used to remove tenant property</span></span>

```shell
spo storageentity remove --appCatalogUrl <appCatalogUrl> --key <key>
```

### <a name="remarks-when-using-the-office-365-cli-set-and-remove-commands"></a><span data-ttu-id="fb28a-133">Что нужно учитывать при задании и удалении свойств с помощью команд Office 365 CLI</span><span class="sxs-lookup"><span data-stu-id="fb28a-133">Remarks when using the Office 365 CLI set and remove commands</span></span>

<span data-ttu-id="fb28a-134">Чтобы задать или удалить свойство клиента, сначала нужно подключиться к сайту администрирования клиента, используя команду spo connect, например</span><span class="sxs-lookup"><span data-stu-id="fb28a-134">To set or remove a tenant property, you have to first connect to a tenant admin site using the spo connect command, eg.</span></span> <span data-ttu-id="fb28a-135">spo connect https://contoso-admin.sharepoint.com. Если вы подключены к другому сайту, вы не сможете управлять свойствами клиента.</span><span class="sxs-lookup"><span data-stu-id="fb28a-135">spo connect https://contoso-admin.sharepoint.com. If you are connected to a different site and will try to manage tenant properties, you will get an error.</span></span>

<span data-ttu-id="fb28a-136">Свойства клиента хранятся на сайте каталога приложений, связанном с этим клиентом.</span><span class="sxs-lookup"><span data-stu-id="fb28a-136">Tenant properties are stored in the app catalog site associated with that tenant.</span></span> <span data-ttu-id="fb28a-137">Чтобы задать или удалить свойство, необходимо указать абсолютный URL-адрес сайта каталога приложений.</span><span class="sxs-lookup"><span data-stu-id="fb28a-137">To set or remove a property, you have to specify the absolute URL of the app catalog site.</span></span> <span data-ttu-id="fb28a-138">Если вы укажете URL-адрес сайта, отличный от каталога приложений, вам будет отказано в доступе.</span><span class="sxs-lookup"><span data-stu-id="fb28a-138">If you specify the URL of a site different than the app catalog, you will get an access denied error.</span></span>

## <a name="read-tenant-properties"></a><span data-ttu-id="fb28a-139">Считывание свойств клиента</span><span class="sxs-lookup"><span data-stu-id="fb28a-139">Read tenant properties</span></span>

<span data-ttu-id="fb28a-140">Разработчики могут считывать свойства клиента с помощью интерфейсов API REST SharePoint и использовать их в компонентах SharePoint Framework, таких как веб-части и расширения.</span><span class="sxs-lookup"><span data-stu-id="fb28a-140">Developers can read tenant properties by using the SharePoint REST APIs and use them in SharePoint Framework components such as web parts and extensions.</span></span>

## <a name="http-request"></a><span data-ttu-id="fb28a-141">HTTP-запрос</span><span class="sxs-lookup"><span data-stu-id="fb28a-141">HTTP request</span></span>

### <a name="get-a-tenant-property"></a><span data-ttu-id="fb28a-142">Получение свойства клиента</span><span class="sxs-lookup"><span data-stu-id="fb28a-142">Get a tenant property</span></span>

```text
GET _api/web/GetStorageEntity('key')
```

#### <a name="example"></a><span data-ttu-id="fb28a-143">Пример</span><span class="sxs-lookup"><span data-stu-id="fb28a-143">Example</span></span>

```text
GET _api/web/GetStorageEntity('AnalyticsKey')
```

#### <a name="request-body"></a><span data-ttu-id="fb28a-144">Текст запроса</span><span class="sxs-lookup"><span data-stu-id="fb28a-144">Request body</span></span>

<span data-ttu-id="fb28a-145">Не указывайте тело запроса для этого метода.</span><span class="sxs-lookup"><span data-stu-id="fb28a-145">Do not supply a request body for this method.</span></span>

#### <a name="response"></a><span data-ttu-id="fb28a-146">Отклик</span><span class="sxs-lookup"><span data-stu-id="fb28a-146">Response</span></span>

<span data-ttu-id="fb28a-147">Возвращает сведения об объекте хранилища для указанного ключа.</span><span class="sxs-lookup"><span data-stu-id="fb28a-147">This returns the storage entity information for the given key.</span></span>

```text
HTTP/1.1 200 OK
Content-Type: application/json
{
    "Comment":"Tenant property comment.",
    "Description":"Tenant property description",
    "Value":"Tenant property key value"
}
```

## <a name="see-also"></a><span data-ttu-id="fb28a-148">См. также</span><span class="sxs-lookup"><span data-stu-id="fb28a-148">See also</span></span>

- [<span data-ttu-id="fb28a-149">Обзор SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="fb28a-149">Overview of the SharePoint Framework</span></span>](sharepoint-framework-overview.md)
- [<span data-ttu-id="fb28a-150">Office 365 CLI</span><span class="sxs-lookup"><span data-stu-id="fb28a-150">Office 365 CLI</span></span>](https://sharepoint.github.io/office365-cli?utm_source=msft_docs&utm_medium=page&utm_campaign=Use+SharePoint+Online+tenant+properties)