---
title: "Обнаружение несколькими географическая конфигурация для клиента SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: 6b7410867e571742987777d50098fd240dc055bf
ms.sourcegitcommit: 22c896de11491c32b992d797414ba50421969a2e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/28/2018
---
# <a name="discover-a-multi-geo-configuration-for-a-sharepoint-tenant"></a><span data-ttu-id="b5423-102">Обнаружение несколькими географическая конфигурация для клиента SharePoint</span><span class="sxs-lookup"><span data-stu-id="b5423-102">Discover a Multi-Geo configuration for a SharePoint tenant</span></span>

> <span data-ttu-id="b5423-103">**Важные:** OneDrive и SharePoint Online Multi-Geo в данный момент в предварительной версии и может быть изменен.</span><span class="sxs-lookup"><span data-stu-id="b5423-103">**Important:** OneDrive and SharePoint Online Multi-Geo is currently in preview and is subject to change.</span></span>

<span data-ttu-id="b5423-104">При работе с клиента SharePoint, необходимо определить, является ли ферма с несколькими географически клиента и определение географического расположения по умолчанию и вспомогательные.</span><span class="sxs-lookup"><span data-stu-id="b5423-104">When you're working with a SharePoint tenant, you'll need to be able to detect whether it's a Multi-Geo tenant, and identify the default and satellite geo locations.</span></span> 

<span data-ttu-id="b5423-105">На следующем рисунке показана ферма с несколькими географически клиента с:</span><span class="sxs-lookup"><span data-stu-id="b5423-105">The following image shows a Multi-Geo tenant with:</span></span>

- <span data-ttu-id="b5423-106">Расположение по умолчанию geo в Северной Америке</span><span class="sxs-lookup"><span data-stu-id="b5423-106">A default geo location in North America</span></span>
- <span data-ttu-id="b5423-107">Расположение вспомогательных geo в Европе</span><span class="sxs-lookup"><span data-stu-id="b5423-107">A satellite geo location in Europe</span></span>
- <span data-ttu-id="b5423-108">Расположение вспомогательных географически в Азии</span><span class="sxs-lookup"><span data-stu-id="b5423-108">A satellite geo location in Asia</span></span>

![Карта мира, отображение географического расположения по умолчанию в Северной Америке и вспомогательные географического расположения в Европе и Азии, администратор клиента зависящие от языка, корневой и URL-адреса личных сайтов](media/multigeo/multigeodiscovery_intro.png)

<span data-ttu-id="b5423-110">В зависимости от используемого сценария можно использовать один или сочетание следующие интерфейсы API для доступа к узлу несколькими географически клиента:</span><span class="sxs-lookup"><span data-stu-id="b5423-110">Depending on your scenario, you can use one or a combination of the following APIs to access a Multi-Geo tenant site:</span></span>

- <span data-ttu-id="b5423-111">**Microsoft Graph API** - Multi-географически принять во внимание.</span><span class="sxs-lookup"><span data-stu-id="b5423-111">**The Microsoft Graph API** - Multi-Geo aware.</span></span> <span data-ttu-id="b5423-112">Мы рекомендуем использовать Microsoft Graph на сайты клиента доступа несколькими географически.</span><span class="sxs-lookup"><span data-stu-id="b5423-112">We recommend that you use Microsoft Graph to access Multi-Geo tenant sites.</span></span> 
- <span data-ttu-id="b5423-113">**SharePoint CSOM API** - не Multi-географически принять во внимание.</span><span class="sxs-lookup"><span data-stu-id="b5423-113">**SharePoint CSOM API** - Not Multi-Geo aware.</span></span> <span data-ttu-id="b5423-114">В зависимости от сценария вам потребуются для определения целевого правильный географического расположения (например, чтобы получить доступ к профилю пользователя или выполнения операций клиента API).</span><span class="sxs-lookup"><span data-stu-id="b5423-114">Depending on the scenario, you'll need to target the correct geo location (for example, to access a user profile or perform tenant API operations).</span></span>
- <span data-ttu-id="b5423-115">**API -Интерфейс REST SharePoint** - обычно этот интерфейс API используется в контексте URL-адрес сайта, и поэтому ли клиента — ферма с несколькими географически не фактор.</span><span class="sxs-lookup"><span data-stu-id="b5423-115">**SharePoint REST API** - Typically this API is used in the context of a site URL, and therefore whether the tenant is Multi-Geo is not a factor.</span></span> <span data-ttu-id="b5423-116">Некоторые сценарии API-Интерфейс REST (например, поиска или пользовательского профилей) может потребоваться совершать звонки одного географического расположения.</span><span class="sxs-lookup"><span data-stu-id="b5423-116">Some REST API scenarios (such as search or user profiles) might require you to make calls per geo location.</span></span>

## <a name="get-multi-geo-tenant-configuration-information"></a><span data-ttu-id="b5423-117">Получение сведений о конфигурации клиента несколькими географически</span><span class="sxs-lookup"><span data-stu-id="b5423-117">Get Multi-Geo tenant configuration information</span></span>

### <a name="using-the-csom-api"></a><span data-ttu-id="b5423-118">Использование интерфейса API CSOM</span><span class="sxs-lookup"><span data-stu-id="b5423-118">Using the CSOM API</span></span>

<span data-ttu-id="b5423-119">Получение географического расположения клиента можно выполнить с помощью CSOM с помощью `Tenant` класс и `GetTenantInstances` метода, как показано в фрагмент:</span><span class="sxs-lookup"><span data-stu-id="b5423-119">Obtaining the geo location of your tenant can be done via CSOM by using the `Tenant` class and the `GetTenantInstances` method as shown in below snippet:</span></span>

```C#
Tenant tenant = new Tenant(clientContext);
var tenantInstances = tenant.GetTenantInstances();
clientContext.Load(tenantInstances);
clientContext.ExecuteQuery();
```

### <a name="using-the-microsoft-graph-api"></a><span data-ttu-id="b5423-120">С помощью Microsoft Graph API</span><span class="sxs-lookup"><span data-stu-id="b5423-120">Using the Microsoft Graph API</span></span>

<span data-ttu-id="b5423-121">Сведения о расположении географически для клиента можно получить с помощью Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="b5423-121">You can get the geo location information for a tenant by using Microsoft Graph.</span></span> <span data-ttu-id="b5423-122">В следующем примере возвращается коллекция с одного объекта одного географического расположения.</span><span class="sxs-lookup"><span data-stu-id="b5423-122">The following example returns a collection with one object per geo location.</span></span>

```
GET https://graph.microsoft.com/v1.0/sites?filter=siteCollection/root%20ne%20null&select=webUrl,siteCollection
```

<span data-ttu-id="b5423-123">Пример ответа для нескольких географически клиента:</span><span class="sxs-lookup"><span data-stu-id="b5423-123">Example response for a Multi-Geo tenant:</span></span>
```JSON
{
    "@odata.context": "https://graph.microsoft.com/v1.0/$metadata#sites",
    "value": [
        {
            "webUrl": "https://contoso.sharepoint.com/",
            "siteCollection": {
                "dataLocationCode":"NAM",
                "hostname": "contoso.sharepoint.com"
            }
        },
        {
            "webUrl": "https://contosoeur.sharepoint.com/",
            "siteCollection": {
                "dataLocationCode":"EUR",
                "hostname": "contosoeur.sharepoint.com"
            }
        },
        {
            "webUrl": "https://contosoapc.sharepoint.com/",
            "siteCollection": {
                "dataLocationCode":"APC",
                "hostname": "contosoapc.sharepoint.com"
            }
        }
    ]
}
```

<span data-ttu-id="b5423-124">Для получения дополнительных сведений см [MultiGeo.TenantInformationCollection](https://github.com/SharePoint/PnP/tree/dev/Samples/MultiGeo.TenantInformationCollection) .</span><span class="sxs-lookup"><span data-stu-id="b5423-124">To learn more, see the [MultiGeo.TenantInformationCollection](https://github.com/SharePoint/PnP/tree/dev/Samples/MultiGeo.TenantInformationCollection) sample.</span></span>

> [!NOTE] 
> <span data-ttu-id="b5423-125">Дополнительные сведения о разрешениях и настройке приложения см [несколькими географически примера приложения](multigeo-sampleapplicationsetup.md).</span><span class="sxs-lookup"><span data-stu-id="b5423-125">For more information about permissions and how to configure your application, see [Set up a Multi-Geo sample application](multigeo-sampleapplicationsetup.md).</span></span>

## <a name="discover-whether-your-tenant-is-multi-geo"></a><span data-ttu-id="b5423-126">Обнаружение, является ли ферма с несколькими географически вашего клиента</span><span class="sxs-lookup"><span data-stu-id="b5423-126">Discover whether your tenant is Multi-Geo</span></span> 

<span data-ttu-id="b5423-127">Microsoft Graph можно использовать для определения, является ли клиента несколькими географически, так как запросы через Microsoft Graph к клиентам с несколькими географически возвращать более одного элемента в коллекции.</span><span class="sxs-lookup"><span data-stu-id="b5423-127">You can use Microsoft Graph to discover whether a tenant is Multi-Geo since requests via Microsoft Graph to Multi-Geo tenants return more then one item in the collection.</span></span> <span data-ttu-id="b5423-128">В следующем примере показано результаты вызова Microsoft Graph географически отдельного клиента.</span><span class="sxs-lookup"><span data-stu-id="b5423-128">The following example shows the results of a Microsoft Graph call to a single-geo tenant.</span></span>

<!-- Not sure where the output for a Multi-Geo tenant is. Provide a link? -->

```
GET https://graph.microsoft.com/v1.0/sites?filter=siteCollection/root%20ne%20null&select=webUrl,siteCollection
```

<span data-ttu-id="b5423-129">Пример ответа для отдельного географически клиента:</span><span class="sxs-lookup"><span data-stu-id="b5423-129">Example response for a single-geo tenant:</span></span>
```JSON
{
    "@odata.context": "https://graph.microsoft.com/v1.0/$metadata#sites",
    "value": [
        {
            "webUrl": "https://singlegeotest.sharepoint.com/",
            "siteCollection": {
                "dataLocationCode":"",
                "hostname": "singlegeotest.sharepoint.com"
            }
        }
    ]
}
```

## <a name="see-also"></a><span data-ttu-id="b5423-130">См. также</span><span class="sxs-lookup"><span data-stu-id="b5423-130">See also</span></span>

- [<span data-ttu-id="b5423-131">Центр разработчиков Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="b5423-131">Microsoft Graph developer center</span></span>](https://developer.microsoft.com/en-us/graph)
- [<span data-ttu-id="b5423-132">Документация по Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="b5423-132">Microsoft Graph documentation</span></span>](https://developer.microsoft.com/en-us/graph/docs/concepts/overview)
- [<span data-ttu-id="b5423-133">Графическое представление проводника</span><span class="sxs-lookup"><span data-stu-id="b5423-133">Graph Explorer</span></span>](https://developer.microsoft.com/en-us/graph/graph-explorer)
