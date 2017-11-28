---
title: "Работа с сайтами, в среде с несколькими географически"
ms.date: 11/03/2017
ms.openlocfilehash: 812c141981e383a35c10ff414dbdb4a199160d00
ms.sourcegitcommit: 26a4fb9cfe1ffcd266313c16f2afabfc841fdb71
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/08/2017
---
# <a name="working-with-sites-in-a-multi-geo-environment"></a><span data-ttu-id="887cf-102">Работа с сайтами, в среде с несколькими географически</span><span class="sxs-lookup"><span data-stu-id="887cf-102">Working with sites in a Multi-Geo environment</span></span>

> <span data-ttu-id="887cf-103">**Важные:** OneDrive и SharePoint Online Multi-Geo в данный момент в предварительной версии и может быть изменен.</span><span class="sxs-lookup"><span data-stu-id="887cf-103">**Important:** OneDrive and SharePoint Online Multi-Geo is currently in preview and is subject to change.</span></span>

<span data-ttu-id="887cf-104">Сайты SharePoint можно распределить между расположения географически по умолчанию и вспомогательные несколькими географически клиента.</span><span class="sxs-lookup"><span data-stu-id="887cf-104">SharePoint sites can be spread across the default and satellite geo locations of a Multi-Geo tenant.</span></span> <span data-ttu-id="887cf-105">При настраиваемой разработки (скрипт, приложения, консольное приложение, приложение node.js,...) требуется Подготовка сайтов, а затем важно необходимо учитывать расположения географически несколькими географически клиента.</span><span class="sxs-lookup"><span data-stu-id="887cf-105">When your custom development (script, app, console application, node.js app,...) needs to provision sites then it's important to be aware of the geo locations in your Multi-Geo tenant.</span></span> 

### <a name="provisioning-classic-team-sites"></a><span data-ttu-id="887cf-106">Подготовка веб-сайтов групп классический</span><span class="sxs-lookup"><span data-stu-id="887cf-106">Provisioning classic team sites</span></span>
<span data-ttu-id="887cf-107">При подготовке семейств сайтов классический группы (например STS #0 на основе семейств веб-сайтов) один должно использовать [CSOM `CreateSite` метод](https://msdn.microsoft.com/en-us/library/microsoft.online.sharepoint.tenantadministration.tenant.createsite(v=office.15).aspx) звонок как объяснялось и отображается в следующих статьях и примеры:</span><span class="sxs-lookup"><span data-stu-id="887cf-107">When provisioning classic team site collections (e.g. STS#0 based site collections) one has to use the [CSOM `CreateSite` method](https://msdn.microsoft.com/en-us/library/microsoft.online.sharepoint.tenantadministration.tenant.createsite(v=office.15).aspx) call as explained and shown in following articles and samples:</span></span>
- [<span data-ttu-id="887cf-108">Подготовка сайта в объектная модель SharePoint</span><span class="sxs-lookup"><span data-stu-id="887cf-108">Site provisioning in the SharePoint add-in model</span></span>](site-provisioning-sharepoint-add-in.md)
- [<span data-ttu-id="887cf-109">Подготовка сайтов партиями с моделью надстройки</span><span class="sxs-lookup"><span data-stu-id="887cf-109">Provision sites in batches with the add-in model</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.Batch)
- [<span data-ttu-id="887cf-110">Создание семейства веб-сайтов или веб-узла с помощью библиотеки PnP основных узлов</span><span class="sxs-lookup"><span data-stu-id="887cf-110">Create site collection or sub site using the PnP Sites Core library</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.CreateSite)

<span data-ttu-id="887cf-111">`CreateSite` Вызова метода требуется выполнение на инициализированный `Tenant` ... объектов и клиента необходимо указать URL-адрес центра администрирования SPO будет создан.</span><span class="sxs-lookup"><span data-stu-id="887cf-111">The `CreateSite` method call needs to be executed on an instantiated `Tenant` object...and a tenant object requires you to specify an SPO Admin center URL to be created.</span></span> <span data-ttu-id="887cf-112">Чтобы создать сайт классический группы выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="887cf-112">So to create a classic team site you follow these steps:</span></span>
- <span data-ttu-id="887cf-113">Сначала определите местоположение географически, которую требуется разместить семейства веб-сайтов (например европейских вспомогательной)</span><span class="sxs-lookup"><span data-stu-id="887cf-113">First determine the geo location that needs to host the site collection (e.g. the European satellite)</span></span>
- <span data-ttu-id="887cf-114">Используйте рекомендации, описано в статье [Обнаружения несколькими географически](multigeo-discovery.md) поиск клиента администрирования сайта и SharePoint корневой url для географического расположения</span><span class="sxs-lookup"><span data-stu-id="887cf-114">Use the guidance explained in the [Multi-Geo Discovery](multigeo-discovery.md) article to find the tenant admin site and SharePoint root url's for the geo location</span></span>
- <span data-ttu-id="887cf-115">Создание `Tenant` с помощью URL-адрес сайта обнаруженного администратора</span><span class="sxs-lookup"><span data-stu-id="887cf-115">Create a `Tenant` object using the found admin site url</span></span>
- <span data-ttu-id="887cf-116">Использование `CreateSite` вызова метода для создания семейства веб-сайтов</span><span class="sxs-lookup"><span data-stu-id="887cf-116">Use the `CreateSite` method call to create the site collection</span></span>

<span data-ttu-id="887cf-117">Ниже примере показано, как для подготовки семейства веб-сайтов в расположении европейских географически:</span><span class="sxs-lookup"><span data-stu-id="887cf-117">Below sample shows how to provision a site collection in the European geo location:</span></span>

```C#
// Use the Multi-Geo discovery guidance to discover the tenant admin and root site urls for this geo location
string tenantAdminSiteForMyGeoLocation = "https://contoso-europe-admin.sharepoint.com";
string targetUrl = "https://contoso-europe.sharepoint.com/sites/demosite";
string owner = "UserA@contoso.onmicrosoft.com";

using (var ctx = new ClientRuntimeContext(tenantAdminSiteForMyGeoLocation))
{
    ctx.Credentials = adminCredentials;
    
    var tenant = new Tenant(ctx);
    
    //Create new site
    var newsite = new SiteCreationProperties()
    {
        Url = targetUrl,
        Owner = owner,
        Template = "STS#0",
        Title = title,
        StorageMaximumLevel = 1000,
        StorageWarningLevel = 500,
        TimeZoneId = 7,
    };
    
    var spoOperation = tenant.CreateSite(newsite);
    
    ctx.Load(spoOperation);
    ctx.ExecuteQuery();
    
    while (!spoOperation.IsComplete)
    {
        Thread.Sleep(2000);
        ctx.Load(spoOperation);
        ctx.ExecuteQuery();
        Console.WriteLine("Site creation status: " + (spoOperation.IsComplete ? "waiting" : "complete"));
    }
}
```

><span data-ttu-id="887cf-118">**Примечание:** Если вы хотите узнать больше о необходимых разрешениях и как настроить приложения, затем выполните извлечение в статье [Настройка географически несколько примеров приложений](multigeo-sampleapplicationsetup.md) .</span><span class="sxs-lookup"><span data-stu-id="887cf-118">**Note:** If you want to learn more about the needed permissions and how to configure your applications then please checkout the [Setting up the Multi-Geo sample applications](multigeo-sampleapplicationsetup.md) article.</span></span>

## <a name="resources"></a><span data-ttu-id="887cf-119">Resources</span><span class="sxs-lookup"><span data-stu-id="887cf-119">Resources</span></span>
<span data-ttu-id="887cf-120">Под списком ресурсов полезны при изучении Дополнительные сведения о работе с сайтами.</span><span class="sxs-lookup"><span data-stu-id="887cf-120">Below list of resources are useful when you're learning more about working with sites:</span></span>
- [<span data-ttu-id="887cf-121">Подготовка веб-сайтов современных групп</span><span class="sxs-lookup"><span data-stu-id="887cf-121">Provisioning modern team sites</span></span>](https://msdn.microsoft.com/en-us/pnp_articles/modern-experience-customizations-provisioning-sites)
- [<span data-ttu-id="887cf-122">Подготовка сайта в объектная модель SharePoint</span><span class="sxs-lookup"><span data-stu-id="887cf-122">Site provisioning in the SharePoint add-in model</span></span>](site-provisioning-sharepoint-add-in.md)
- [<span data-ttu-id="887cf-123">Подготовка сайтов партиями с моделью надстройки</span><span class="sxs-lookup"><span data-stu-id="887cf-123">Provision sites in batches with the add-in model</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.Batch)
- [<span data-ttu-id="887cf-124">Создание семейства веб-сайтов или веб-узла с помощью библиотеки PnP основных узлов</span><span class="sxs-lookup"><span data-stu-id="887cf-124">Create site collection or sub site using the PnP Sites Core library</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.CreateSite)