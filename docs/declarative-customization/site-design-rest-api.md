---
title: "REST API для работы с макетами сайтов SharePoint"
description: "Узнайте, как работать с макетами сайтов SharePoint при помощи интерфейса REST для SharePoint, выполняя базовые операции создания, чтения, обновления и удаления (CRUD)."
ms.date: 12/14/2017
ms.openlocfilehash: 3670ffabcebd5146abb155906dce341324404815
ms.sourcegitcommit: 8e63066ad9591e51bbda419b1b9527452111081b
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/14/2017
---
# <a name="site-design-and-site-script-rest-api"></a>REST API для работы с макетами и скриптами сайтов

> [!NOTE]
> Макеты и скрипты сайтов в настоящий момент пересматриваются и могут быть изменены. Сейчас они не поддерживаются для использования в рабочих средах.

При помощи интерфейса REST для SharePoint можно выполнять операции CRUD (создание, чтение, обновление и удаление) с макетами и скриптами сайтов.

Служба REST в SharePoint Online (а также локальной среде SharePoint 2016 или более поздней версии) поддерживает объединение нескольких запросов в один вызов службы с помощью параметра запроса OData $batch. Подробные сведения и ссылки на примеры кода см. в статье [Отправка пакетных запросов с помощью интерфейсов REST API]((https://dev.office.com/sharepoint/docs/apis/rest/make-batch-requests-with-the-rest-apis.md)).

## <a name="prerequisites"></a>Необходимые условия
Прежде чем приступить к работе, убедитесь, что вы знакомы с понятиями, описанными в следующих статьях:
- [Знакомство со службой REST в SharePoint]((https://dev.office.com/sharepoint/docs/apis/rest/get-to-know-the-sharepoint-rest-service.md)); 
- [Выполнение базовых операций с использованием конечных точек REST SharePoint]((https://dev.office.com/sharepoint/docs/apis/rest/complete-basic-operations-using-sharepoint-rest-endpoints.md))

## <a name="rest-commands"></a>Команды REST

Для работы с макетами и скриптами сайтов доступны следующие команды REST:

- **CreateSiteScript** &mdash; создание скрипта сайта.
- **GetSiteScripts** &mdash; получение списка сведений об имеющихся скриптах сайтов.
- **GetSiteScriptMetadata** &mdash; получение сведений об определенном скрипте сайта.
- **UpdateSiteScript** &mdash; обновление скрипта сайта с использованием новых значений.
- **DeleteSiteScript** &mdash; удаление скрипта сайта.
- **CreateSiteDesign** &mdash; создание макета сайта.
- **GetSiteDesigns** &mdash; получение списка сведений об имеющихся макетах сайтов.
- **GetSiteDesignMetadata** &mdash; получение сведений об определенном макете сайта.
- **UpdateSiteDesign** &mdash; обновление макета сайта с использованием новых значений.
- **DeleteSiteDesign** &mdash; удаление макета сайта.
- **GetSiteDesignRights** &mdash; получение списка субъектов, имеющих доступ к макету сайта.
- **GrantSiteDesignRights** &mdash; предоставление доступа к макету сайта для одного или нескольких субъектов.
- **RevokeSiteDesignRights** &mdash; отзыв доступа к макету сайта для одного или нескольких субъектов.

## <a name="create-a-function-to-send-rest-requests"></a>Создание функции для отправки запросов REST

Чтобы работать с REST API, рекомендуем создать вспомогательную функцию для отправки вызовов REST. Приведенная ниже функция **RestRequest** вызывает метод REST, указанный в параметре **url**, и передает дополнительные параметры из аргумента **params**.

```javascript
function RestRequest(url,params) {
  var req = new XMLHttpRequest();
  req.onreadystatechange = function ()
  {
    if (req.readyState != 4) // Loaded
      return;
    console.log(req.responseText);
  };

  // Prepend web URL to url and remove duplicated slashes.
  var webBasedUrl = (_spPageContextInfo.webServerRelativeUrl + "//" + url).replace(/\/{2,}/,"/");
  req.open("POST",webBasedUrl,true);
  req.setRequestHeader("Content-Type", "application/json;charset=utf-8");
  req.setRequestHeader("ACCEPT", "application/json; odata.metadata=minimal");
  req.setRequestHeader("x-requestdigest", _spPageContextInfo.formDigestValue);
  req.setRequestHeader("ODATA-VERSION","4.0");
  req.send(params ? JSON.stringify(params) : void 0);
}
```

## <a name="createsitescript"></a>CreateSiteScript

Создает макет сайта, доступный пользователям при создании сайта на домашней странице SharePoint.

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.CreateSiteScript(Title=@title)?@title='TITLE'", VARIABLE);
```

## <a name="getsitescripts"></a>GetSiteScripts

Получает список сведений об имеющихся скриптах сайтов.

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.GetSiteScripts");
```

## <a name="getsitescriptmetadata"></a>GetSiteScriptMetadata

Получает сведения об определенном скрипте сайта.

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.GetSiteScriptMetadata", {id:"<ID>"});
```

## <a name="updatesitescript"></a>UpdateSiteScript

Обновляет скрипт сайта с использованием новых значений.

```javascript
VAR = site script content

RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.UpdateSiteScript", {updateInfo:{Id:"<siteScriptID>", Title:"<updated title>", Description:"<updated description>", Version: 2, Content: JSON.stringify(<VAR>)}});
```

## <a name="deletesitescript"></a>DeleteSiteScript

Удаляет скрипт сайта.

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.DeleteSiteScript", {id:"<ID>"});
```

## <a name="createsitedesign"></a>CreateSiteDesign

Создает макет сайта.

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.CreateSiteDesign", {info:{Title:"<title>", Description:"<description>", SiteScriptIds:["NNN"],  WebTemplate:"<64 | 68>", IsDefault: <false | true>}});
```

## <a name="getsitedesigns"></a>GetSiteDesigns

Получает список сведений об имеющихся макетах сайтов.

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.GetSiteDesigns");
```

## <a name="getsitedesignmetadata"></a>GetSiteDesignMetadata

Получает сведения об определенном макете сайта.

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.GetSiteDesignMetadata", {id:"<ID>"});
```

## <a name="updatesitedesign"></a>UpdateSiteDesign

Обновляет макет сайта с использованием новых значений.

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.UpdateSiteDesign", {updateInfo:{Id:"<siteDesignID>", Title:"<updated site design title>", Description:"<updated site design description>", SiteScriptIds:["<ID>"], PreviewImageUrl:"<url to image asset for site design preview image>",PreviewImageAltText:"<alt text for preview image>" WebTemplate:"68", Version: 7, IsDefault: false}});
```

## <a name="deletesitedesign"></a>DeleteSiteDesign

Удаляет макет сайта.

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.DeleteSiteDesign", {id:"<ID>"});
```

## <a name="getsitedesignrights"></a>GetSiteDesignRights

Получает список субъектов, имеющих доступ к макету сайта.

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.GetSiteDesignRights", {id:"<ID>"});
```

## <a name="grantsitedesignrights"></a>GrantSiteDesignRights

Предоставляет доступ к макету сайта для одного или нескольких субъектов.

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.GrantSiteDesignRights", {id:"<ID>", principalNames:["alias", “alias@domain.com”], grantedRights:1});
```

## <a name="revokesitedesignrights"></a>RevokeSiteDesignRights

Отзывает доступ к макету сайта для одного или нескольких субъектов.

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.RevokeSiteDesignRights", {id:"5d4756e9-e1f5-42f7-afa7-5fa5aac170aa", principalNames:["debrab@Contoso.sharepoint.com"] });
```
