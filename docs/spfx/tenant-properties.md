---
title: "Свойства клиента SharePoint Online"
description: "Управляйте свойствами клиента, которые позволяют администраторам добавлять свойства в каталог приложений для различных компонентов SharePoint Framework."
ms.date: 02/02/2018
ms.prod: sharepoint
ms.openlocfilehash: 391d2860a25c2eec553c8ce034bbf100bdb3c82c
ms.sourcegitcommit: 7a40bb847e8753810ab7f907d638f3cac022d444
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/05/2018
---
# <a name="sharepoint-online-tenant-properties"></a><span data-ttu-id="6da09-103">Свойства клиента SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="6da09-103">SharePoint Online Tenant Properties</span></span>

<span data-ttu-id="6da09-104">Свойства клиента позволяют администраторам добавлять свойства в каталог приложений для различных компонентов SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="6da09-104">Tenant Properties allow tenant administrators to add properties in the app catalog that can be read by various SharePoint Framework components.</span></span> <span data-ttu-id="6da09-105">Для управления свойствами клиента администраторы клиента используют [командную консоль Microsoft SharePoint Online](https://technet.microsoft.com/ru-RU/library/fp161372.aspx). Это модуль PowerShell для управления подпиской SharePoint Online в Office 365.</span><span class="sxs-lookup"><span data-stu-id="6da09-105">The Tenant Properties are managed by tenant administrators using the [Microsoft SharePoint Online Management Shell](https://technet.microsoft.com/ru-RU/library/fp161372.aspx) which is a PowerShell module to manage your SharePoint Online subscription in the Office 365.</span></span>

## <a name="manage-tenant-properties"></a><span data-ttu-id="6da09-106">Управление свойствами клиента</span><span class="sxs-lookup"><span data-stu-id="6da09-106">Manage tenant properties</span></span>

<span data-ttu-id="6da09-107">С помощью [командной консоли Microsoft SharePoint Online](https://www.microsoft.com/en-us/download/details.aspx?id=35588) администраторы клиента могут добавлять и удалять свойства клиента через PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6da09-107">Using the Microsoft SharePoint Online Management Shell, tenant administrators can add and remove tenant properties using PowerShell.</span></span> 

<span data-ttu-id="6da09-108">Эти командлеты PowerShell доступны для управления свойствами клиента:</span><span class="sxs-lookup"><span data-stu-id="6da09-108">The following PowerShell cmdlets are available to manage the tenant properties:</span></span> <span data-ttu-id="6da09-109">Так как свойства клиента хранятся в каталоге приложений клиента, в командлетах ниже нужно указать URL-адрес семейства веб-сайтов каталога приложений клиента.</span><span class="sxs-lookup"><span data-stu-id="6da09-109">Because tenant properties are stored in the tenant App Catalog, you must provide the tenant App Catalog site collection URL in the following cmdlets.</span></span>

### <a name="get-spostorageentity"></a><span data-ttu-id="6da09-110">Get-SPOStorageEntity</span><span class="sxs-lookup"><span data-stu-id="6da09-110">Get-SPOStorageEntity</span></span>

- <span data-ttu-id="6da09-111">**Область применения:** Office 365, SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="6da09-111">Applies to: Office 365, SharePoint Online</span></span>

- <span data-ttu-id="6da09-112">**Синтаксис** Get-SPOStorageEntity [-Site] <AppCatalogSiteURL> [-Key] <String></span><span class="sxs-lookup"><span data-stu-id="6da09-112">Syntax Get-SPOStorageEntity [-Site]  [-Key] <AppCatalogSiteURL></span></span>

### <a name="set-spostorageentity"></a><span data-ttu-id="6da09-113">Set-SPOStorageEntity</span><span class="sxs-lookup"><span data-stu-id="6da09-113">Set-SPOStorageEntity</span></span>

- <span data-ttu-id="6da09-114">**Область применения:** Office 365, SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="6da09-114">Applies to: Office 365, SharePoint Online</span></span>

- <span data-ttu-id="6da09-115">**Синтаксис** Set-SPOStorageEntity [-Site] <AppCatalogSiteURL> [-Key] <String> [-Value] <String> [-Description] <String> [-Comments] <String></span><span class="sxs-lookup"><span data-stu-id="6da09-115">Syntax Set-SPOStorageEntity [-Site]  [-Key] <AppCatalogSiteURL> [-Value] <String> [-Description] <String> [-Comments] <String></span></span>

### <a name="remove-spostorageentity"></a><span data-ttu-id="6da09-116">Remove-SPOStorageEntity</span><span class="sxs-lookup"><span data-stu-id="6da09-116">Remove-SPOStorageEntity</span></span>

- <span data-ttu-id="6da09-117">**Область применения:** Office 365, SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="6da09-117">Applies to: Office 365, SharePoint Online</span></span>

- <span data-ttu-id="6da09-118">**Синтаксис** Remove-SPOStorageEntity [-Site] <AppCatalogSiteURL> [-Key] <String></span><span class="sxs-lookup"><span data-stu-id="6da09-118">Syntax Remove-SPOStorageEntity [-Site]  [-Key] <AppCatalogSiteURL></span></span>


## <a name="read-tenant-properties"></a><span data-ttu-id="6da09-119">Считывание свойств клиента</span><span class="sxs-lookup"><span data-stu-id="6da09-119">Read tenant properties</span></span>

<span data-ttu-id="6da09-120">Разработчики могут считывать свойства клиента с помощью интерфейсов API REST SharePoint и использовать их в компонентах SharePoint Framework, таких как веб-части и расширения.</span><span class="sxs-lookup"><span data-stu-id="6da09-120">Developers can read tenant properties using the SharePoint REST APIs and use them in SharePoint Framework components such as web parts and extensions.</span></span>

## <a name="http-request"></a><span data-ttu-id="6da09-121">HTTP-запрос</span><span class="sxs-lookup"><span data-stu-id="6da09-121">HTTP request</span></span>

### <a name="get-a-tenant-property"></a><span data-ttu-id="6da09-122">Получение свойства клиента</span><span class="sxs-lookup"><span data-stu-id="6da09-122">Get a tenant property</span></span>

```text
GET _api/web/GetStorageEntity('key')
```

#### <a name="example"></a><span data-ttu-id="6da09-123">Пример</span><span class="sxs-lookup"><span data-stu-id="6da09-123">Example</span></span>

```text
GET _api/web/GetStorageEntity('AnalyticsKey')
```

#### <a name="request-body"></a><span data-ttu-id="6da09-124">Текст запроса</span><span class="sxs-lookup"><span data-stu-id="6da09-124">Request body</span></span>

<span data-ttu-id="6da09-125">Не указывайте тело запроса для этого метода.</span><span class="sxs-lookup"><span data-stu-id="6da09-125">Do not supply a request body for this method.</span></span>

#### <a name="response"></a><span data-ttu-id="6da09-126">Отклик</span><span class="sxs-lookup"><span data-stu-id="6da09-126">Response</span></span>

<span data-ttu-id="6da09-127">Возвращает сведения об объекте хранилища для указанного ключа.</span><span class="sxs-lookup"><span data-stu-id="6da09-127">This returns the storage entity information for the given key.</span></span>

```text
HTTP/1.1 200 OK
Content-Type: application/json
{
    "Comment":"Tenant property comment.",
    "Description":"Tenant property description",
    "Value":"Tenant property key value"
}
```

## <a name="see-also"></a><span data-ttu-id="6da09-128">См. также</span><span class="sxs-lookup"><span data-stu-id="6da09-128">See also</span></span>

- [<span data-ttu-id="6da09-129">Обзор SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="6da09-129">Overview of the SharePoint Framework</span></span>](sharepoint-framework-overview.md)