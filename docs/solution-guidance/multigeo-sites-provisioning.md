---
title: "Работа с сайтами, в среде с несколькими географически"
ms.date: 11/03/2017
ms.openlocfilehash: 581df53ac1a9527d8078401c90bf472a93849b7d
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="working-with-sites-in-a-multi-geo-environment"></a>Работа с сайтами, в среде с несколькими географически

> **Важные:** OneDrive и SharePoint Online Multi-Geo в данный момент в предварительной версии и может быть изменен.

Сайты SharePoint можно распределить между расположения географически по умолчанию и вспомогательные несколькими географически клиента. При настраиваемой разработки (скрипт, приложения, консольное приложение, приложение node.js,...) требуется Подготовка сайтов, а затем важно необходимо учитывать расположения географически несколькими географически клиента. 

### <a name="provisioning-classic-team-sites"></a>Подготовка веб-сайтов групп классический
При подготовке семейств сайтов классический группы (например STS #0 на основе семейств веб-сайтов) один должно использовать [CSOM `CreateSite` метод](https://msdn.microsoft.com/en-us/library/microsoft.online.sharepoint.tenantadministration.tenant.createsite(v=office.15).aspx) звонок как объяснялось и отображается в следующих статьях и примеры:
- [Подготовка сайта в объектная модель SharePoint](site-provisioning-sharepoint-add-in.md)
- [Подготовка сайтов партиями с моделью надстройки](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.Batch)
- [Создание семейства веб-сайтов или веб-узла с помощью библиотеки PnP основных узлов](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.CreateSite)

`CreateSite` Вызова метода требуется выполнение на инициализированный `Tenant` ... объектов и клиента необходимо указать URL-адрес центра администрирования SPO будет создан. Чтобы создать сайт классический группы выполните следующие действия.
- Сначала определите местоположение географически, которую требуется разместить семейства веб-сайтов (например европейских вспомогательной)
- Используйте рекомендации, описано в статье [Обнаружения несколькими географически](multigeo-discovery.md) поиск клиента администрирования сайта и SharePoint корневой url для географического расположения
- Создание `Tenant` с помощью URL-адрес сайта обнаруженного администратора
- Использование `CreateSite` вызова метода для создания семейства веб-сайтов

Ниже примере показано, как для подготовки семейства веб-сайтов в расположении европейских географически:

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

> [!NOTE] 
> Если вы хотите узнать больше о необходимых разрешениях и как настроить приложения, затем выполните извлечение в статье [Настройка географически несколько примеров приложений](multigeo-sampleapplicationsetup.md) .

## <a name="resources"></a>Resources
Под списком ресурсов полезны при изучении Дополнительные сведения о работе с сайтами.
- [Подготовка веб-сайтов современных групп](https://msdn.microsoft.com/en-us/pnp_articles/modern-experience-customizations-provisioning-sites)
- [Подготовка сайта в объектная модель SharePoint](site-provisioning-sharepoint-add-in.md)
- [Подготовка сайтов партиями с моделью надстройки](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.Batch)
- [Создание семейства веб-сайтов или веб-узла с помощью библиотеки PnP основных узлов](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.CreateSite)