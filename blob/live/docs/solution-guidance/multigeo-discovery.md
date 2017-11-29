---
title: "Обнаружение несколькими географическая конфигурация для клиента SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: f33e63a49dd8ec52b5ba6cb83874bbdafb916b8d
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
# <a name="discover-a-multi-geo-configuration-for-a-sharepoint-tenant"></a><span data-ttu-id="69230-102">Обнаружение несколькими географическая конфигурация для клиента SharePoint</span><span class="sxs-lookup"><span data-stu-id="69230-102">Discover a Multi-Geo configuration for a SharePoint tenant</span></span>

> <span data-ttu-id="69230-103">**Важные:** OneDrive и SharePoint Online Multi-Geo в данный момент в предварительной версии и может быть изменен.</span><span class="sxs-lookup"><span data-stu-id="69230-103">**Important:** OneDrive and SharePoint Online Multi-Geo is currently in preview and is subject to change.</span></span>

<span data-ttu-id="69230-104">При работе с клиента SharePoint, необходимо определить, является ли ферма с несколькими географически клиента и определение географического расположения по умолчанию и вспомогательные.</span><span class="sxs-lookup"><span data-stu-id="69230-104">When you're working with a SharePoint tenant, you'll need to be able to detect whether it's a Multi-Geo tenant, and identify the default and satellite geo locations.</span></span> 

<span data-ttu-id="69230-105">На следующем рисунке показана ферма с несколькими географически клиента с:</span><span class="sxs-lookup"><span data-stu-id="69230-105">The following image shows a Multi-Geo tenant with:</span></span>

- <span data-ttu-id="69230-106">Расположение по умолчанию geo в Северной Америке</span><span class="sxs-lookup"><span data-stu-id="69230-106">A default geo location in North America</span></span>
- <span data-ttu-id="69230-107">Расположение вспомогательных geo в Европе</span><span class="sxs-lookup"><span data-stu-id="69230-107">A satellite geo location in Europe</span></span>
- <span data-ttu-id="69230-108">Расположение вспомогательных географически в Азии</span><span class="sxs-lookup"><span data-stu-id="69230-108">A satellite geo location in Asia</span></span>

![Карта мира, отображение географического расположения по умолчанию в Северной Америке и вспомогательные географического расположения в Европе и Азии, администратор клиента зависящие от языка, корневой и URL-адреса личных сайтов](media/multigeo/multigeodiscovery_intro.png)

<span data-ttu-id="69230-110">В зависимости от используемого сценария можно использовать один или сочетание следующие интерфейсы API для доступа к узлу несколькими географически клиента:</span><span class="sxs-lookup"><span data-stu-id="69230-110">Depending on your scenario, you can use one or a combination of the following APIs to access a Multi-Geo tenant site:</span></span>

- <span data-ttu-id="69230-111">**Microsoft Graph API** - Multi-географически принять во внимание.</span><span class="sxs-lookup"><span data-stu-id="69230-111">**The Microsoft Graph API** - Multi-Geo aware.</span></span> <span data-ttu-id="69230-112">Мы рекомендуем использовать Microsoft Graph на сайты клиента доступа несколькими географически.</span><span class="sxs-lookup"><span data-stu-id="69230-112">We recommend that you use Microsoft Graph to access Multi-Geo tenant sites.</span></span> 
- <span data-ttu-id="69230-113">**SharePoint CSOM API** - не Multi-географически принять во внимание.</span><span class="sxs-lookup"><span data-stu-id="69230-113">**SharePoint CSOM API** - Not Multi-Geo aware.</span></span> <span data-ttu-id="69230-114">В зависимости от сценария вам потребуются для определения целевого правильный географического расположения (например, чтобы получить доступ к профилю пользователя или выполнения операций клиента API).</span><span class="sxs-lookup"><span data-stu-id="69230-114">Depending on the scenario, you'll need to target the correct geo location (for example, to access a user profile or perform tenant API operations).</span></span>
- <span data-ttu-id="69230-115">**API -Интерфейс REST SharePoint** - обычно этот интерфейс API используется в контексте URL-адрес сайта, и поэтому ли клиента — ферма с несколькими географически не фактор.</span><span class="sxs-lookup"><span data-stu-id="69230-115">**SharePoint REST API** - Typically this API is used in the context of a site URL, and therefore whether the tenant is Multi-Geo is not a factor.</span></span> <span data-ttu-id="69230-116">Некоторые сценарии API-Интерфейс REST (например, поиска или пользовательского профилей) может потребоваться совершать звонки одного географического расположения.</span><span class="sxs-lookup"><span data-stu-id="69230-116">Some REST API scenarios (such as search or user profiles) might require you to make calls per geo location.</span></span>

## <a name="get-multi-geo-tenant-configuration-information"></a><span data-ttu-id="69230-117">Получение сведений о конфигурации клиента несколькими географически</span><span class="sxs-lookup"><span data-stu-id="69230-117">Get Multi-Geo tenant configuration information</span></span>

<span data-ttu-id="69230-118">Сведения о расположении географически для клиента можно получить с помощью Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="69230-118">You can get the geo location information for a tenant by using Microsoft Graph.</span></span> <span data-ttu-id="69230-119">В следующем примере возвращается коллекция с одного объекта одного географического расположения.</span><span class="sxs-lookup"><span data-stu-id="69230-119">The following example returns a collection with one object per geo location.</span></span>

```
GET https://graph.microsoft.com/v1.0/sites?filter=siteCollection/root%20ne%20null&select=webUrl,siteCollection
```

<span data-ttu-id="69230-120">Пример ответа для нескольких географически клиента:</span><span class="sxs-lookup"><span data-stu-id="69230-120">Example response for a Multi-Geo tenant:</span></span>
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

<span data-ttu-id="69230-121">Для получения дополнительных сведений см [MultiGeo.TenantInformationCollection](https://github.com/SharePoint/PnP/tree/dev/Samples/MultiGeo.TenantInformationCollection) .</span><span class="sxs-lookup"><span data-stu-id="69230-121">To learn more, see the [MultiGeo.TenantInformationCollection](https://github.com/SharePoint/PnP/tree/dev/Samples/MultiGeo.TenantInformationCollection) sample.</span></span>

><span data-ttu-id="69230-122">**Примечание:** Дополнительные сведения о разрешениях и настройке приложения см [несколькими географически примера приложения](multigeo-sampleapplicationsetup.md).</span><span class="sxs-lookup"><span data-stu-id="69230-122">**Note:** For more information about permissions and how to configure your application, see [Set up a Multi-Geo sample application](multigeo-sampleapplicationsetup.md).</span></span>

## <a name="discover-whether-your-tenant-is-multi-geo"></a><span data-ttu-id="69230-123">Обнаружение, является ли ферма с несколькими географически вашего клиента</span><span class="sxs-lookup"><span data-stu-id="69230-123">Discover whether your tenant is Multi-Geo</span></span> 

<span data-ttu-id="69230-124">Microsoft Graph можно использовать для определения, является ли клиента несколькими географически, так как запросы через Microsoft Graph к клиентам с несколькими географически возвращать более одного элемента в коллекции.</span><span class="sxs-lookup"><span data-stu-id="69230-124">You can use Microsoft Graph to discover whether a tenant is Multi-Geo since requests via Microsoft Graph to Multi-Geo tenants return more then one item in the collection.</span></span> <span data-ttu-id="69230-125">В следующем примере показано результаты вызова Microsoft Graph географически отдельного клиента.</span><span class="sxs-lookup"><span data-stu-id="69230-125">The following example shows the results of a Microsoft Graph call to a single-geo tenant.</span></span>

<!-- Not sure where the output for a Multi-Geo tenant is. Provide a link? -->

```
GET https://graph.microsoft.com/v1.0/sites?filter=siteCollection/root%20ne%20null&select=webUrl,siteCollection
```

<span data-ttu-id="69230-126">Пример ответа для отдельного географически клиента:</span><span class="sxs-lookup"><span data-stu-id="69230-126">Example response for a single-geo tenant:</span></span>
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

## <a name="see-also"></a><span data-ttu-id="69230-127">См. также</span><span class="sxs-lookup"><span data-stu-id="69230-127">See also</span></span>

- [<span data-ttu-id="69230-128">Центр разработчиков Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="69230-128">Microsoft Graph developer center</span></span>](https://developer.microsoft.com/en-us/graph)
- [<span data-ttu-id="69230-129">Документация по Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="69230-129">Microsoft Graph documentation</span></span>](https://developer.microsoft.com/en-us/graph/docs/concepts/overview)
- [<span data-ttu-id="69230-130">Графическое представление проводника</span><span class="sxs-lookup"><span data-stu-id="69230-130">Graph Explorer</span></span>](https://developer.microsoft.com/en-us/graph/graph-explorer)
