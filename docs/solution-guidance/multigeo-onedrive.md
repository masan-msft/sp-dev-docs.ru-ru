---
title: "С помощью OneDrive для бизнеса в географически нескольких клиентов"
ms.date: 11/03/2017
ms.openlocfilehash: 4373f4073a36326d250317bf05f4dd82cd19a84f
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
# <a name="using-onedrive-for-business-in-a-multi-geo-tenant"></a>С помощью OneDrive для бизнеса в географически нескольких клиентов

> **Важные:** OneDrive и SharePoint Online Multi-Geo в данный момент в предварительной версии и может быть изменен.

Доступ к пользователя OneDrive для бизнеса сайта, также известной как личный сайт или личных сайтов — это типично для пользовательских приложений. В этой статье описывается, как для работы со службой OneDrive для бизнеса сайтов в географически нескольких клиентов.

Можно использовать один из несколько интерфейсов API для доступа к службе OneDrive для бизнеса сайта:

- Microsoft Graph (рекомендуется)
- SharePoint CSOM 
- API-Интерфейс REST SharePoint


## <a name="read-onedrive-for-business-files-using-microsoft-graph"></a>Чтение файлы OneDrive для бизнеса с помощью Microsoft Graph
При использовании Microsoft Graph для чтения OneDrive для бизнеса файла не нужно знать, где расположен сайт OneDrive пользователя. При запросе диске, как показано в следующих примерах, вы получите необходимые файлы. 

```
GET https://graph.microsoft.com/v1.0/users/bert@contoso.onmicrosoft.com/drive/root/children


GET https://graph.microsoft.com/v1.0/users/me/drive/root/children
```

## <a name="get-the-location-of-a-users-onedrive-for-business-site-using-microsoft-graph"></a>Получение расположения пользователя OneDrive для бизнеса сайта с помощью Microsoft Graph
В приведенных ниже примерах показано, как получить расположение OneDrive для бизнеса сайта с помощью API-Интерфейс Microsoft Graph.

```
GET https://graph.microsoft.com/v1.0/users/admin@a830edad9050849524e17052212.onmicrosoft.com/mySite


GET https://graph.microsoft.com/v1.0/users/me/mySite
```

Для получения дополнительных сведений см [MultiGeo.UserProfileUpdates](https://github.com/SharePoint/PnP/tree/dev/Samples/MultiGeo.UserProfileUpdates) .

## <a name="get-the-location-of-a-users-onedrive-for-business-site-using-csom-and-rest"></a>Получение расположения пользователя OneDrive для бизнеса сайта с помощью CSOM и REST
В следующем примере показано запросов на основе REST для получения местоположения OneDrive для бизнеса сайта.

```
GET https://contoso.sharepoint.com/_api/SP.UserProfiles.PeopleManager/GetPropertiesFor(accountName=@v)/PersonalUrl?%40v=%27i%3A0%23.f%7Cmembership%7Cbert%40contoso.onmicrosoft.com%27
```

Если вы используете C#, CSOM можно использовать для получения местоположения OneDrive для бизнеса сайта.

```C#
public string GetUserPersonalUrlCSOM(ClientContext ctx, string userPrincipalName)
{
    string result = null;

    PeopleManager peopleManager = new PeopleManager(ctx);
    var userProperties = peopleManager.GetPropertiesFor(userPrincipalName);
    this.clientContext.ExecuteQuery();
    result = userProperties.PersonalUrl;

    return result;
}
```

## <a name="read-onedrive-for-business-files-using-csom-and-rest"></a>Чтение файлы OneDrive для бизнеса с помощью CSOM и REST

Чтение файлов с помощью CSOM идентична чтение файлов в других семействах сайтов, OneDrive для бизнеса сайта является регулярное семейства сайтов SharePoint с библиотекой документов, где хранятся файлы. В разделе ресурсы для примеров на использование CSOM и REST для загрузки файлов.

## <a name="see-also"></a>См. также

- [Чтение файлов с помощью API-Интерфейс Microsoft Graph](https://developer.microsoft.com/en-us/graph/docs/api-reference/v1.0/api/item_list_children)
- [Передача файлов с помощью REST](https://github.com/SharePoint/PnP/tree/master/Samples/Core.RestFileUpload)
- [Файл загрузки надстройки CSOM SharePoint](https://github.com/SharePoint/PnP/tree/master/Samples/Core.FileUpload)
- [Загрузка больших файлов с помощью CSOM](https://github.com/SharePoint/PnP/tree/master/Samples/Core.LargeFileUpload)


