---
title: "Свойства клиента SharePoint Online"
description: "Управляйте свойствами клиента, которые позволяют администраторам добавлять свойства в каталог приложений для различных компонентов SharePoint Framework."
ms.date: 02/02/2018
ms.prod: sharepoint
ms.openlocfilehash: bd1fcff023d79dcfa06318b8c4e9e18061357a6d
ms.sourcegitcommit: e157d51378190ddfed6394ba154ce66141c8ca33
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/19/2018
---
# <a name="sharepoint-online-tenant-properties"></a><span data-ttu-id="b4a02-103">Свойства клиента SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="b4a02-103">SharePoint Online Tenant Properties</span></span>

<span data-ttu-id="b4a02-104">Свойства клиента позволяют администраторам добавлять свойства в каталог приложений для различных компонентов SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="b4a02-104">Tenant Properties allow tenant administrators to add properties in the app catalog that can be read by various SharePoint Framework components.</span></span> <span data-ttu-id="b4a02-105">Для управления свойствами клиента администраторы клиента используют [командную консоль Microsoft SharePoint Online](https://technet.microsoft.com/ru-RU/library/fp161372.aspx). Это модуль PowerShell для управления подпиской на SharePoint Online в Office 365.</span><span class="sxs-lookup"><span data-stu-id="b4a02-105">The Tenant Properties are managed by tenant administrators using the [Microsoft SharePoint Online Management Shell](https://technet.microsoft.com/ru-RU/library/fp161372.aspx) which is a PowerShell module to manage your SharePoint Online subscription in the Office 365.</span></span>

## <a name="manage-tenant-properties"></a><span data-ttu-id="b4a02-106">Управление свойствами клиента</span><span class="sxs-lookup"><span data-stu-id="b4a02-106">Manage tenant properties</span></span>

<span data-ttu-id="b4a02-107">С помощью [командной консоли Microsoft SharePoint Online](https://www.microsoft.com/en-us/download/details.aspx?id=35588) администраторы клиента могут добавлять и удалять свойства клиента через PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b4a02-107">Using the Microsoft SharePoint Online Management Shell, tenant administrators can add and remove tenant properties using PowerShell.</span></span> 

<span data-ttu-id="b4a02-108">Ниже приведены командлеты PowerShell для управления свойствами клиента.</span><span class="sxs-lookup"><span data-stu-id="b4a02-108">The following PowerShell cmdlets are available to manage the tenant properties:</span></span> <span data-ttu-id="b4a02-109">Так как свойства клиента хранятся в каталоге приложений клиента, в командлетах ниже нужно указать URL-адрес семейства веб-сайтов каталога приложений клиента.</span><span class="sxs-lookup"><span data-stu-id="b4a02-109">Since tenant properties are stored in the tenant app catalog, you will need to provide the tenant app catalog site collection URL in the cmdlets below.</span></span>

### <a name="get-spostorageentity"></a><span data-ttu-id="b4a02-110">Get-SPOStorageEntity</span><span class="sxs-lookup"><span data-stu-id="b4a02-110">Get-SPOStorageEntity</span></span>

- <span data-ttu-id="b4a02-111">**Область применения:** Office 365, SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="b4a02-111">Applies to: Office 365, SharePoint Online</span></span>

- <span data-ttu-id="b4a02-112">**Синтаксис** Get-SPOStorageEntity [-Site] <AppCatalogSiteURL> [-Key] <String></span><span class="sxs-lookup"><span data-stu-id="b4a02-112">Syntax Get-SPOStorageEntity [-Site]  [-Key] <AppCatalogSiteURL></span></span>

### <a name="set-spostorageentity"></a><span data-ttu-id="b4a02-113">Set-SPOStorageEntity</span><span class="sxs-lookup"><span data-stu-id="b4a02-113">Set-SPOStorageEntity</span></span>

- <span data-ttu-id="b4a02-114">**Область применения:** Office 365, SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="b4a02-114">Applies to: Office 365, SharePoint Online</span></span>

- <span data-ttu-id="b4a02-115">**Синтаксис** Set-SPOStorageEntity [-Site] <AppCatalogSiteURL> [-Key] <String> [-Value] <String> [-Description] <String> [-Comments] <String></span><span class="sxs-lookup"><span data-stu-id="b4a02-115">Syntax Set-SPOStorageEntity [-Site]  [-Key] <AppCatalogSiteURL> [-Value] <String> [-Description] <String> [-Comments] <String></span></span>

### <a name="remove-spostorageentity"></a><span data-ttu-id="b4a02-116">Remove-SPOStorageEntity</span><span class="sxs-lookup"><span data-stu-id="b4a02-116">Remove-SPOStorageEntity</span></span>

- <span data-ttu-id="b4a02-117">**Область применения:** Office 365, SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="b4a02-117">Applies to: Office 365, SharePoint Online</span></span>

- <span data-ttu-id="b4a02-118">**Синтаксис** Remove-SPOStorageEntity [-Site] <AppCatalogSiteURL> [-Key] <String></span><span class="sxs-lookup"><span data-stu-id="b4a02-118">Syntax Remove-SPOStorageEntity [-Site]  [-Key] <AppCatalogSiteURL></span></span>


## <a name="read-tenant-properties"></a><span data-ttu-id="b4a02-119">Считывание свойств клиента</span><span class="sxs-lookup"><span data-stu-id="b4a02-119">Read tenant properties</span></span>

<span data-ttu-id="b4a02-120">Разработчики могут считывать свойства клиента с помощью интерфейсов API REST SharePoint и использовать их в компонентах SharePoint Framework, таких как веб-части и расширения.</span><span class="sxs-lookup"><span data-stu-id="b4a02-120">Developers can read tenant properties using the SharePoint REST APIs and use them in SharePoint Framework components such as web parts and extensions.</span></span>

## <a name="http-request"></a><span data-ttu-id="b4a02-121">HTTP-запрос</span><span class="sxs-lookup"><span data-stu-id="b4a02-121">HTTP request</span></span>

### <a name="get-a-tenant-property"></a><span data-ttu-id="b4a02-122">Получение свойства клиента</span><span class="sxs-lookup"><span data-stu-id="b4a02-122">Get a tenant property</span></span>

```text
GET _api/web/GetStorageEntity('key')
```

#### <a name="example"></a><span data-ttu-id="b4a02-123">Пример</span><span class="sxs-lookup"><span data-stu-id="b4a02-123">Example</span></span>

```text
GET _api/web/GetStorageEntity('AnalyticsKey')
```

#### <a name="request-body"></a><span data-ttu-id="b4a02-124">Текст запроса</span><span class="sxs-lookup"><span data-stu-id="b4a02-124">Request body</span></span>

<span data-ttu-id="b4a02-125">Не указывайте тело запроса для этого метода.</span><span class="sxs-lookup"><span data-stu-id="b4a02-125">Do not supply a request body for this method.</span></span>

#### <a name="response"></a><span data-ttu-id="b4a02-126">Отклик</span><span class="sxs-lookup"><span data-stu-id="b4a02-126">Response</span></span>

<span data-ttu-id="b4a02-127">Возвращает сведения об объекте хранилища для указанного ключа.</span><span class="sxs-lookup"><span data-stu-id="b4a02-127">This returns the storage entity information for the given key.</span></span>

```text
HTTP/1.1 200 OK
Content-Type: application/json
{
    "Comment":"Tenant property comment.",
    "Description":"Tenant property description",
    "Value":"Tenant property key value"
}
```

## <a name="see-also"></a><span data-ttu-id="b4a02-128">См. также</span><span class="sxs-lookup"><span data-stu-id="b4a02-128">See also</span></span>

- [<span data-ttu-id="b4a02-129">Обзор SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="b4a02-129">Overview of the SharePoint Framework</span></span>](sharepoint-framework-overview.md)