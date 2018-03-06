---
title: "Обнаружение несколькими географическая конфигурация для клиента SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: 6b7410867e571742987777d50098fd240dc055bf
ms.sourcegitcommit: 22c896de11491c32b992d797414ba50421969a2e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/28/2018
---
# <a name="discover-a-multi-geo-configuration-for-a-sharepoint-tenant"></a>Обнаружение несколькими географическая конфигурация для клиента SharePoint

> **Важные:** OneDrive и SharePoint Online Multi-Geo в данный момент в предварительной версии и может быть изменен.

При работе с клиента SharePoint, необходимо определить, является ли ферма с несколькими географически клиента и определение географического расположения по умолчанию и вспомогательные. 

На следующем рисунке показана ферма с несколькими географически клиента с:

- Расположение по умолчанию geo в Северной Америке
- Расположение вспомогательных geo в Европе
- Расположение вспомогательных географически в Азии

![Карта мира, отображение географического расположения по умолчанию в Северной Америке и вспомогательные географического расположения в Европе и Азии, администратор клиента зависящие от языка, корневой и URL-адреса личных сайтов](media/multigeo/multigeodiscovery_intro.png)

В зависимости от используемого сценария можно использовать один или сочетание следующие интерфейсы API для доступа к узлу несколькими географически клиента:

- **Microsoft Graph API** - Multi-географически принять во внимание. Мы рекомендуем использовать Microsoft Graph на сайты клиента доступа несколькими географически. 
- **SharePoint CSOM API** - не Multi-географически принять во внимание. В зависимости от сценария вам потребуются для определения целевого правильный географического расположения (например, чтобы получить доступ к профилю пользователя или выполнения операций клиента API).
- **API -Интерфейс REST SharePoint** - обычно этот интерфейс API используется в контексте URL-адрес сайта, и поэтому ли клиента — ферма с несколькими географически не фактор. Некоторые сценарии API-Интерфейс REST (например, поиска или пользовательского профилей) может потребоваться совершать звонки одного географического расположения.

## <a name="get-multi-geo-tenant-configuration-information"></a>Получение сведений о конфигурации клиента несколькими географически

### <a name="using-the-csom-api"></a>Использование интерфейса API CSOM

Получение географического расположения клиента можно выполнить с помощью CSOM с помощью `Tenant` класс и `GetTenantInstances` метода, как показано в фрагмент:

```C#
Tenant tenant = new Tenant(clientContext);
var tenantInstances = tenant.GetTenantInstances();
clientContext.Load(tenantInstances);
clientContext.ExecuteQuery();
```

### <a name="using-the-microsoft-graph-api"></a>С помощью Microsoft Graph API

Сведения о расположении географически для клиента можно получить с помощью Microsoft Graph. В следующем примере возвращается коллекция с одного объекта одного географического расположения.

```
GET https://graph.microsoft.com/v1.0/sites?filter=siteCollection/root%20ne%20null&select=webUrl,siteCollection
```

Пример ответа для нескольких географически клиента:
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

Для получения дополнительных сведений см [MultiGeo.TenantInformationCollection](https://github.com/SharePoint/PnP/tree/dev/Samples/MultiGeo.TenantInformationCollection) .

> [!NOTE] 
> Дополнительные сведения о разрешениях и настройке приложения см [несколькими географически примера приложения](multigeo-sampleapplicationsetup.md).

## <a name="discover-whether-your-tenant-is-multi-geo"></a>Обнаружение, является ли ферма с несколькими географически вашего клиента 

Microsoft Graph можно использовать для определения, является ли клиента несколькими географически, так как запросы через Microsoft Graph к клиентам с несколькими географически возвращать более одного элемента в коллекции. В следующем примере показано результаты вызова Microsoft Graph географически отдельного клиента.

<!-- Not sure where the output for a Multi-Geo tenant is. Provide a link? -->

```
GET https://graph.microsoft.com/v1.0/sites?filter=siteCollection/root%20ne%20null&select=webUrl,siteCollection
```

Пример ответа для отдельного географически клиента:
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

## <a name="see-also"></a>См. также

- [Центр разработчиков Microsoft Graph](https://developer.microsoft.com/en-us/graph)
- [Документация по Microsoft Graph](https://developer.microsoft.com/en-us/graph/docs/concepts/overview)
- [Графическое представление проводника](https://developer.microsoft.com/en-us/graph/graph-explorer)
