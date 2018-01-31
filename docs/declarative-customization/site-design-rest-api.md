---
title: "REST API для работы с макетами сайтов SharePoint"
description: "Узнайте, как работать с макетами сайтов SharePoint при помощи интерфейса REST для SharePoint, выполняя базовые операции создания, чтения, обновления и удаления (CRUD)."
ms.date: 12/14/2017
ms.openlocfilehash: 978a5c2b58e418ae9f7d99783a95352cdd3977a5
ms.sourcegitcommit: 9f492519d4eeb3f62a1fddc71cdca79263651a56
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/19/2018
---
# <a name="site-design-and-site-script-rest-api"></a>REST API для работы с макетами и скриптами сайтов

> [!NOTE]
> Макеты и скрипты сайтов находятся на стадии тестирования и могут меняться. В настоящее время в рабочих средах их можно использовать только в выпуске Targeted.

При помощи интерфейса REST для SharePoint можно выполнять операции CRUD (создание, чтение, обновление и удаление) с макетами и скриптами сайтов.

Служба REST в SharePoint Online (а также локальной среде SharePoint 2016 или более поздней версии) поддерживает объединение нескольких запросов в один вызов службы с помощью параметра запроса OData $batch. Подробные сведения и ссылки на примеры кода см. в статье [Отправка пакетных запросов с помощью интерфейсов REST API](https://dev.office.com/sharepoint/docs/apis/rest/make-batch-requests-with-the-rest-apis.md).

## <a name="prerequisites"></a>Необходимые условия
Прежде чем приступить к работе, убедитесь, что вы знакомы с понятиями, описанными в следующих статьях:
- [Знакомство со службой REST в SharePoint](https://dev.office.com/sharepoint/docs/apis/rest/get-to-know-the-sharepoint-rest-service.md); 
- [Выполнение базовых операций с использованием конечных точек REST SharePoint](https://dev.office.com/sharepoint/docs/apis/rest/complete-basic-operations-using-sharepoint-rest-endpoints.md)

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

Создает скрипт сайта.

### <a name="parameters"></a>Параметры

|Параметр     | Описание  |
|--------------|--------------|
| Название       | Отображаемое имя макета сайта. |
| Статья     | Значение JSON, описывающее скрипт. Дополнительные сведения см. в [справочнике по JSON](site-design-json-schema.md).|

В примере ниже создается скрипт сайта, где применяется настраиваемая тема.

```javascript
var site_script = 
{
  "$schema": "schema.json",
  "actions": [
    {
      "verb": "applyTheme",
      "themeName": "Contoso Theme"
    }
  ],
  "bindata": { },
  "version": 1
};

RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.CreateSiteScript(Title=@title)?@title='Contoso theme script'", site_script);
```

В этом примере после вызова команды **CreateSiteScript** возвращается нотация объектов JavaScript (JSON), содержащая идентификатор нового скрипта сайта.

```json
{
  "@odata.context": "https://contoso.sharepoint.com/_api/$metadata#Microsoft.SharePoint.Utilities.WebTemplateExtensions.SiteScriptMetadata",
  "Content": null,
  "Description": null,
  "Id": "7647d3d6-1046-41fe-a798-4ff66b099d12",
  "Title": "Contoso customer list",
  "Version": 0
}
```

## <a name="getsitescripts"></a>GetSiteScripts

Получает список сведений обо всех имеющихся скриптах сайтов.

### <a name="parameters"></a>Параметры

Нет.

В приведенном ниже примере показано, как получить информацию о скрипте сайта для всех скриптов.

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.GetSiteScripts");
```

В этом примере JSON возвращается после вызова команды **GetSiteScripts**.

```json
{
  "@odata.context": "https://contoso.sharepoint.com/_api/$metadata#Collection(Microsoft.SharePoint.Utilities.WebTemplateExtensions.SiteScriptMetadata)",
  "value": [
    {
      "Content": null,
      "Description": null,
      "Id": "6dfedb96-c090-44e3-875a-1c38032715fc",
      "Title": "Customer orders",
      "Version": 1
    },
    {
      "Content": null,
      "Description": null,
      "Id": "07702c07-0485-426f-b710-4704241caad9",
      "Title": "Contoso theme",
      "Version": 1
    }
  ]
}
```

## <a name="getsitescriptmetadata"></a>GetSiteScriptMetadata

Получает сведения об определенном скрипте сайта, а также возвращает JSON для скрипта.

### <a name="parameters"></a>Параметры

|Параметр     | Описание  |
|--------------|--------------|
| id    | Идентификатор скрипта сайта, сведения о котором требуется получить. |

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.GetSiteScriptMetadata",
{id:"07702c07-0485-426f-b710-4704241caad9"});
```

Ниже приведен пример возвращаемой JSON после вызова команды **GetSiteScriptMetadata**.

```json
{
  "@odata.context": "https://contoso.sharepoint.com/_api/$metadata#Microsoft.SharePoint.Utilities.WebTemplateExtensions.SiteScriptMetadata",
  "Content": "{\r\n    \"$schema\": \"schema.json\",\r\n        \"actions\": [\r\n            {\r\n               \"verb\": \"applyTheme\",\r\n               \"themeName\": \"Custom Cyan\"\r\n            }\r\n        ],\r\n            \"bindata\": { },\r\n    \"version\": 1\r\n}",
  "Description": null,
  "Id": "07702c07-0485-426f-b710-4704241caad9",
  "Title": "Contoso theme",
  "Version": 1
}
```

## <a name="updatesitescript"></a>UpdateSiteScript

Обновляет скрипт сайта с использованием новых значений.

### <a name="parameters"></a>Параметры

|Параметр   | Описание  |
|------------|--------------|
| Id         | Идентификатор скрипта сайта, который требуется обновить. |
|Название       | (Необязательный.) Новое отображаемое имя скрипта сайта. |
|Description | (Необязательный.) Новое описание скрипта сайта. |
| Version    | (Необязательный.) Новый номер версии для скрипта сайта. |
| Статья    | (Необязательный.) Новый скрипт JSON, определяющий действия скрипта. Дополнительные сведения см. в статье [Схема JSON для макетов сайтов](site-design-json-schema.md). |

Ниже приведен пример обновления скрипта сайта с помощью новых значений и скрипта JSON.

```javascript
var updated_site_script = 
{
  "$schema": "schema.json",
  "actions": [
    {
      "verb": "applyTheme",
      "themeName": "Contoso Theme"
    }
  ],
  "bindata": { },
  "version": 2
};


RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.UpdateSiteScript", 
{updateInfo:{
  Id:"07702c07-0485-426f-b710-4704241caad9",
  Title:"New Contoso theme", 
  Description:"Updated Contoso site script", 
  Version: 2, 
  Content: JSON.stringify(updated_site_script)}});
```

Вот пример JSON, возвращаемой после вызова команды **UpdateSiteScript**.

```json
{
  "@odata.context": "https://contoso.sharepoint.com/_api/$metadata#Microsoft.SharePoint.Utilities.WebTemplateExtensions.SiteScriptMetadata",
  "Content": "{\"$schema\":\"schema.json\",\"actions\":[{\"verb\":\"applyTheme\",\"themeName\":\"Contoso Theme\"}],\"bindata\":{},\"version\":2}",
  "Description": "Updated Contoso site script",
  "Id": "07702c07-0485-426f-b710-4704241caad9",
  "Title": "New Contoso theme",
  "Version": 2
}
```

## <a name="deletesitescript"></a>DeleteSiteScript

Удаляет скрипт сайта.

### <a name="parameters"></a>Параметры

|Параметр   | Описание  |
|------------|--------------|
| id         | Идентификатор скрипта сайта, который нужно удалить. |

В примере ниже показано, как удалить скрипт сайта.

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.DeleteSiteScript", 
{id:"07702c07-0485-426f-b710-4704241caad9"});
```

## <a name="createsitedesign"></a>CreateSiteDesign

Создает макет сайта, доступный пользователям при создании сайта на домашней странице SharePoint.

### <a name="parameters"></a>Параметры

|Параметр  | Описание  |
|-----------|--------------|
|Название                 | Отображаемое имя макета сайта. |
|WebTemplate           | Указывает, к какому базовому шаблону будет добавлен макет. Значение **64** обозначает шаблон сайта группы, а значение **68** — шаблон сайта для общения. |
|SiteScripts           | Массив из одного или нескольких скриптов сайта. Каждый из них определяется по идентификатору. Скрипты будут выполняться в указанном порядке. |
|Description         | (Необязательный.) Отображаемое описание макета сайта. |
|PreviewImageUrl     | (Необязательный.) URL-адрес изображения для предварительного просмотра. Если он не указан, в SharePoint будет использоваться стандартное изображение. |
|PreviewImageAltText | (Необязательный.) Замещающий текст с описанием изображения для специальных возможностей. |
|IsDefault           | (Необязательный.) Выберите значение **true**, чтобы макет сайта применялся как стандартный. В противном случае установите **false**. Дополнительные сведения см. в статье [Настройка стандартного макета сайта](customize-default-site-design.md) |

Ниже представлен пример создания макета сайта.

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.CreateSiteDesign",{
  info:{
    Title:"Contoso customer tracking",
    Description:"Creates customer list and applies standard theme",
    SiteScriptIds:["07702c07-0485-426f-b710-4704241caad9"],
    WebTemplate:"64",
    PreviewImageUrl: "https://contoso.sharepoint.com/SiteAssets/contoso-design.png",
    PreviewImageAltText: "Customer tracking site design theme"
    }
  });
```

Вот пример JSON, возвращаемой после вызова команды **CreateSiteDesign**. В ней также содержится идентификатор нового макета сайта.

```json
{
  "@odata.context": "https://contoso.sharepoint.com/_api/$metadata#Microsoft.SharePoint.Utilities.WebTemplateExtensions.SiteDesignMetadata",
  "Description": "Creates customer list and applies standard theme",
  "PreviewImageAltText": "Customer tracking site design theme",
  "PreviewImageUrl": "https://contoso.sharepoint.com/SiteAssets/contoso-design.png",
  "SiteScriptIds": [ "07702c07-0485-426f-b710-4704241caad9" ],
  "Title": "Contoso customer tracking",
  "WebTemplate": "64",
  "Id": "614f9b28-3e85-4ec9-a961-5971ea086cca",
  "Version": 1
}
```

## <a name="getsitedesigns"></a>GetSiteDesigns

Получает список сведений об имеющихся макетах сайтов.

### <a name="parameters"></a>Параметры

None

Ниже приведен пример получения всех макетов сайта.

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.GetSiteDesigns");
```

Вот пример JSON, возвращаемой после вызова команды **GetSiteDesigns**.

```json
{
  "@odata.context": "https://contoso.sharepoint.com/_api/$metadata#Collection(Microsoft.SharePoint.Utilities.WebTemplateExtensions.SiteDesignMetadata)",
  "value": [
    {
      "Description": "Tracks customer orders",
      "IsDefault": false,
      "PreviewImageAltText": null,
      "PreviewImageUrl": null,
      "SiteScriptIds": [ "6dfedb96-c090-44e3-875a-1c38032715fc" ],
      "Title": "customer orders",
      "WebTemplate": "64",
      "Id": "bbbd5740-ed97-461b-8b8e-e682f3fa167b",
      "Version": 1
    },
    {
      "Description": "Creates customer list and applies standard theme",
      "IsDefault": true,
      "PreviewImageAltText": "Customer tracking site design theme",
      "PreviewImageUrl": "https://contoso.sharepoint.com/SiteAssets/site_design.png",
      "SiteScriptIds": [ "07702c07-0485-426f-b710-4704241caad9" ],
      "Title": "Contoso customer tracking",
      "WebTemplate": "64",
      "Id": "614f9b28-3e85-4ec9-a961-5971ea086cca",
      "Version": 1
    }
  ]
}
```

## <a name="getsitedesignmetadata"></a>GetSiteDesignMetadata

Получает сведения об определенном макете сайта.

### <a name="parameters"></a>Параметры

|Параметр   | Описание  |
|------------|--------------|
| id         | Идентификатор макета сайта, сведения о котором требуется получить. |

В примере ниже показано, как получить сведения об определенном макете сайта с помощью его идентификатора.

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.GetSiteDesignMetadata", 
{id:"614f9b28-3e85-4ec9-a961-5971ea086cca"});
```

Вот пример JSON, возвращаемой после вызова команды **GetSiteDesignMetadata**.

```json
{
  "@odata.context": "https://contoso.sharepoint.com/_api/$metadata#Microsoft.SharePoint.Utilities.WebTemplateExtensions.SiteDesignMetadata",
  "Description": "Creates customer list and applies standard theme",
  "IsDefault": true,
  "PreviewImageAltText": "Customer tracking site design theme",
  "PreviewImageUrl": "https://contoso.sharepoint.com/SiteAssets/site_design.png",
  "SiteScriptIds": [ "07702c07-0485-426f-b710-4704241caad9" ],
  "Title": "Contoso customer tracking",
  "WebTemplate": "64",
  "Id": "614f9b28-3e85-4ec9-a961-5971ea086cca",
  "Version": 1
}
```

## <a name="updatesitedesign"></a>UpdateSiteDesign

Обновляет макет сайта с использованием новых значений.

### <a name="parameters"></a>Параметры

|Параметр  | Описание  |
|-----------|--------------|
|Id         | Идентификатор макета сайта, который требуется обновить. |
|Название                 |  (Необязательный.) Новое отображаемое имя обновленного макета сайта. |
|WebTemplate           | (Необязательный.) Новый шаблон для добавления макета сайта. Значение **64** обозначает шаблон сайта группы, а значение **68** — шаблон сайта для общения. |
|SiteScripts           | (Необязательный.) Новый массив из одного или нескольких скриптов сайта. Каждый из них определяется по идентификатору. Скрипты будут выполняться в указанном порядке. |
|Description         | (Необязательный.) Новое отображаемое описание обновленного макета сайта. |
|PreviewImageUrl     | (Необязательный.) Новый URL-адрес для предварительного просмотра изображения. |
|PreviewImageAltText | (Необязательный.) Новый замещающий текст с описанием изображения для специальных возможностей. |
|IsDefault           | (Необязательный.) Выберите значение **true**, чтобы макет сайта применялся как стандартный. В противном случае установите **false**. Дополнительные сведения см. в статье [Настройка стандартного макета сайта](customize-default-site-design.md) |

В примере ниже обновляются все значения существующего макета сайта.

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.UpdateSiteDesign",
 {updateInfo:{
   Id:"614f9b28-3e85-4ec9-a961-5971ea086cca", 
   Title:"Contoso customer site", 
   Description:"Creates site with customer theme and list", 
   SiteScriptIds:["6b2b79e4-5da3-4352-8565-42a896fabd57","2b997981-258b-4e1e-81ff-f6fbf7235a1f"], 
   PreviewImageUrl:"https://contoso.sharepoint.com/SiteAssets/customer_site.png",
   PreviewImageAltText:"Customer site with list and theme", 
   WebTemplate:"68", 
   Version: 7, 
   IsDefault: false}});
```

Вот пример JSON, возвращаемой после вызова команды **UpdateSiteDesign**.

```json{
  "@odata.context": "https://contoso.sharepoint.com/_api/$metadata#Microsoft.SharePoint.Utilities.WebTemplateExtensions.SiteDesignMetadata",
  "Description": "Creates site with customer theme and list",
  "IsDefault": false,
  "PreviewImageAltText": "Customer site with list and theme",
  "PreviewImageUrl": "https://contoso.sharepoint.com/SiteAssets/customer_site.png",
  "SiteScriptIds": [ "6b2b79e4-5da3-4352-8565-42a896fabd57", "2b997981-258b-4e1e-81ff-f6fbf7235a1f" ],
  "Title": "Contoso customer site",
  "WebTemplate": "68",
  "Id": "614f9b28-3e85-4ec9-a961-5971ea086cca",
  "Version": 7
}
```

## <a name="deletesitedesign"></a>DeleteSiteDesign

Удаляет макет сайта.

### <a name="parameters"></a>Параметры

|Параметр   | Описание  |
|------------|--------------|
| id         | Идентификатор макета сайта, который требуется удалить. |

В примере ниже показано, как удалить макет сайта.

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.DeleteSiteDesign", 
{id:"f9e76746-5076-4bd2-bad3-e611c488fa85"});
```

## <a name="getsitedesignrights"></a>GetSiteDesignRights

Получает список субъектов, имеющих доступ к макету сайта.


### <a name="parameters"></a>Параметры

|Параметр   | Описание  |
|------------|--------------|
| id         | Идентификатор макета сайта, откуда требуется получить сведения о правах. |

Ниже приведен пример получения сведений о правах на просмотр для определенного макета сайта.

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.GetSiteDesignRights", 
{id:"dc076f7b-6c15-4d76-8f85-948a17f5dd18"});
```

Вот пример JSON, возвращаемой после вызова команды **GetSiteDesignRights**.

```json
{
  "@odata.context": "https://contoso.sharepoint.com/_api/$metadata#SiteDesignPrincipals",
  "value": [
    {
      "@odata.type": "#Microsoft.SharePoint.Utilities.WebTemplateExtensions.SiteDesignPrincipal",
      "@odata.id": "https://contoso.sharepoint.com/_api/Microsoft.SharePoint.Utilities.WebTemplateExtensions.SiteDesignPrincipalfca62a9f-e43e-49a0-9139-6ae4df212859",
      "@odata.editLink": "Microsoft.SharePoint.Utilities.WebTemplateExtensions.SiteDesignPrincipalfca62a9f-e43e-49a0-9139-6ae4df212859",
      "DisplayName": "Nestor Wilke",
      "PrincipalName": "i:0#.f|membership|nestorw@contoso.onmicrosoft.com",
      "Rights": 1
    },
    {
      "@odata.type": "#Microsoft.SharePoint.Utilities.WebTemplateExtensions.SiteDesignPrincipal",
      "@odata.id": "https://contoso.sharepoint.com/_api/Microsoft.SharePoint.Utilities.WebTemplateExtensions.SiteDesignPrincipalce4cd6f6-553b-4a55-9364-1d39125be0ef",
      "@odata.editLink": "Microsoft.SharePoint.Utilities.WebTemplateExtensions.SiteDesignPrincipalce4cd6f6-553b-4a55-9364-1d39125be0ef",
      "DisplayName": "Patti Fernandez",
      "PrincipalName": "i:0#.f|membership|pattif@contoso.onmicrosoft.com",
      "Rights": 1
    }
  ]
}
```

## <a name="grantsitedesignrights"></a>GrantSiteDesignRights

Предоставляет доступ к макету сайта для одного или нескольких субъектов.

### <a name="parameters"></a>Параметры

|Параметр   | Описание  |
|------------|--------------|
| id         | Идентификатор макета сайта, которому необходимо предоставить права. |
| principalNames | Массив из одного или нескольких субъектов, которым необходимо предоставить права на просмотр. Субъектами могут быть пользователи или группы безопасности, поддерживающие почту, в формате "псевдоним" или "псевдоним@\<*доменное имя*\>.com" |
| grantedRights | Всегда задавайте значение **1**, соответствующее праву **Просмотр**. |

В примере ниже показано, как предоставить права на просмотр макету сайта для пользователей Nestor и Patti (вымышленные пользователи в корпорации Contoso.)

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.GrantSiteDesignRights", {
  "id": "dc076f7b-6c15-4d76-8f85-948a17f5dd18",
  "principalNames": [ "NestorW@contoso.onmicrosoft.com", "PattiF@contoso.onmicrosoft.com" ],
  "grantedRights": 1
});
```

## <a name="revokesitedesignrights"></a>RevokeSiteDesignRights

Отзывает доступ к макету сайта для одного или нескольких субъектов.

### <a name="parameters"></a>Параметры

|Параметр   | Описание  |
|------------|--------------|
| id         | Идентификатор макета сайта, у которого требуется отозвать права. |
| principalNames | Массив из одного или нескольких субъектов, для которых необходимо отозвать права. Если права на макет сайта отозваны для всех субъектов, макет сайта становится видимым для всех. |

В примере ниже показано, как у макета сайта отзываются права на просмотр для пользователя Patti (вымышленного пользователя в корпорации Contoso).

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.RevokeSiteDesignRights", 
{id:"5d4756e9-e1f5-42f7-afa7-5fa5aac170aa",
 principalNames:["debrab@Contoso.sharepoint.com"] });
```
