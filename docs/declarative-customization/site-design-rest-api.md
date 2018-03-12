---
title: "REST API для работы с макетами сайтов SharePoint"
description: "Узнайте, как работать с макетами сайтов SharePoint при помощи интерфейса REST для SharePoint, выполняя базовые операции создания, чтения, обновления и удаления (CRUD)."
ms.date: 12/14/2017
ms.openlocfilehash: 8a0ca7e4c0add061401a7c128fc15c155cf4f637
ms.sourcegitcommit: 4e65e89f3ad8ef1d953e2fdd04d7ab5c0e7df174
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/27/2018
---
# <a name="site-design-and-site-script-rest-api"></a><span data-ttu-id="78fea-103">REST API для работы с макетами и скриптами сайтов</span><span class="sxs-lookup"><span data-stu-id="78fea-103">Site design and site script REST API</span></span>

<span data-ttu-id="78fea-104">При помощи интерфейса REST для SharePoint можно выполнять операции CRUD (создание, чтение, обновление и удаление) с макетами и скриптами сайтов.</span><span class="sxs-lookup"><span data-stu-id="78fea-104">You can use the the SharePoint REST interface to perform basic create, read, update, and delete (CRUD) operations on site designs and site scripts.</span></span>

<span data-ttu-id="78fea-105">Служба REST в SharePoint Online (а также локальной среде SharePoint 2016 или более поздней версии) поддерживает объединение нескольких запросов в один вызов службы с помощью параметра запроса OData $batch.</span><span class="sxs-lookup"><span data-stu-id="78fea-105">The SharePoint Online (and SharePoint 2016 and later on-premises) REST service supports combining multiple requests into a single call to the service by using the OData $batch query option.</span></span> <span data-ttu-id="78fea-106">Подробные сведения и ссылки на примеры кода см. в статье [Отправка пакетных запросов с помощью интерфейсов REST API](../sp-add-ins/make-batch-requests-with-the-rest-apis.md).</span><span class="sxs-lookup"><span data-stu-id="78fea-106">For details and links to code samples, see [Make batch requests with the REST APIs](../sp-add-ins/make-batch-requests-with-the-rest-apis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="78fea-107">Предварительные условия</span><span class="sxs-lookup"><span data-stu-id="78fea-107">Prerequisites</span></span>
<span data-ttu-id="78fea-108">Прежде чем приступить к работе, убедитесь, что вы знакомы с понятиями, описанными в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="78fea-108">Before you get started, make sure that you're familiar with the following:</span></span>
- [<span data-ttu-id="78fea-109">Знакомство со службой REST в SharePoint</span><span class="sxs-lookup"><span data-stu-id="78fea-109">Get to know the SharePoint REST service</span></span>](../sp-add-ins/get-to-know-the-sharepoint-rest-service.md) 
- [<span data-ttu-id="78fea-110">Выполнение базовых операций с использованием конечных точек REST SharePoint</span><span class="sxs-lookup"><span data-stu-id="78fea-110">Complete basic operations using SharePoint REST endpoints</span></span>](../sp-add-ins/complete-basic-operations-using-sharepoint-rest-endpoints.md)

## <a name="rest-commands"></a><span data-ttu-id="78fea-111">Команды REST</span><span class="sxs-lookup"><span data-stu-id="78fea-111">REST commands</span></span>

<span data-ttu-id="78fea-112">Для работы с макетами и скриптами сайтов доступны следующие команды REST:</span><span class="sxs-lookup"><span data-stu-id="78fea-112">The following REST commands are available for working with site designs and site scripts:</span></span>

- <span data-ttu-id="78fea-113">**CreateSiteScript** &mdash; создание скрипта сайта.</span><span class="sxs-lookup"><span data-stu-id="78fea-113">**CreateSiteScript** &mdash; Creates a new site script.</span></span>
- <span data-ttu-id="78fea-114">**GetSiteScripts** &mdash; получение списка сведений об имеющихся скриптах сайтов.</span><span class="sxs-lookup"><span data-stu-id="78fea-114">**GetSiteScripts** &mdash; Gets a list of information on existing site scripts.</span></span>
- <span data-ttu-id="78fea-115">**GetSiteScriptMetadata** &mdash; получение сведений об определенном скрипте сайта.</span><span class="sxs-lookup"><span data-stu-id="78fea-115">**GetSiteScriptMetadata** &mdash; Gets information about a specific site script.</span></span>
- <span data-ttu-id="78fea-116">**UpdateSiteScript** &mdash; обновление скрипта сайта с использованием новых значений.</span><span class="sxs-lookup"><span data-stu-id="78fea-116">**UpdateSiteScript** &mdash; Updates a site script with new values.</span></span>
- <span data-ttu-id="78fea-117">**DeleteSiteScript** &mdash; удаление скрипта сайта.</span><span class="sxs-lookup"><span data-stu-id="78fea-117">**DeleteSiteScript** &mdash; Deletes a site script.</span></span>
- <span data-ttu-id="78fea-118">**CreateSiteDesign** &mdash; создание макета сайта.</span><span class="sxs-lookup"><span data-stu-id="78fea-118">**CreateSiteDesign** &mdash; Creates a site design.</span></span>
- <span data-ttu-id="78fea-119">**ApplySiteDesign** &mdash; применение макета сайта к существующему семейству веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="78fea-119">**ApplySiteDesign** &mdash; Applies a site design to an existing site collection.</span></span>
- <span data-ttu-id="78fea-120">**GetSiteDesigns** &mdash; получение списка сведений об имеющихся макетах сайтов.</span><span class="sxs-lookup"><span data-stu-id="78fea-120">**GetSiteDesigns** &mdash; Gets a list of information on existing site designs.</span></span>
- <span data-ttu-id="78fea-121">**GetSiteDesignMetadata** &mdash; получение сведений об определенном макете сайта.</span><span class="sxs-lookup"><span data-stu-id="78fea-121">**GetSiteDesignMetadata** &mdash; Gets information about a sepcific site design.</span></span>
- <span data-ttu-id="78fea-122">**UpdateSiteDesign** &mdash; обновление макета сайта с использованием новых значений.</span><span class="sxs-lookup"><span data-stu-id="78fea-122">**UpdateSiteDesign** &mdash; Updates a site design with new values.</span></span>
- <span data-ttu-id="78fea-123">**DeleteSiteDesign** &mdash; удаление макета сайта.</span><span class="sxs-lookup"><span data-stu-id="78fea-123">**DeleteSiteDesign** &mdash; Deletes a site design.</span></span>
- <span data-ttu-id="78fea-124">**GetSiteDesignRights** &mdash; получение списка субъектов, имеющих доступ к макету сайта.</span><span class="sxs-lookup"><span data-stu-id="78fea-124">**GetSiteDesignRights** &mdash; Gets a list of principals that have access to a site design.</span></span>
- <span data-ttu-id="78fea-125">**GrantSiteDesignRights** &mdash; предоставление доступа к макету сайта для одного или нескольких субъектов.</span><span class="sxs-lookup"><span data-stu-id="78fea-125">**GrantSiteDesignRights** &mdash; Grants access to a site design for one or more principals.</span></span>
- <span data-ttu-id="78fea-126">**RevokeSiteDesignRights** &mdash; отзыв доступа к макету сайта для одного или нескольких субъектов.</span><span class="sxs-lookup"><span data-stu-id="78fea-126">**RevokeSiteDesignRights** &mdash; Revokes access from a site design for one or more principals.</span></span>

## <a name="create-a-function-to-send-rest-requests"></a><span data-ttu-id="78fea-127">Создание функции для отправки запросов REST</span><span class="sxs-lookup"><span data-stu-id="78fea-127">Create a function to send REST requests</span></span>

<span data-ttu-id="78fea-128">Чтобы работать с REST API, рекомендуем создать вспомогательную функцию для отправки вызовов REST.</span><span class="sxs-lookup"><span data-stu-id="78fea-128">To work with the REST API we recommend creating a helper function to make the REST calls.</span></span> <span data-ttu-id="78fea-129">Приведенная ниже функция **RestRequest** вызывает метод REST, указанный в параметре **url**, и передает дополнительные параметры из аргумента **params**.</span><span class="sxs-lookup"><span data-stu-id="78fea-129">The following **RestRequest** function will call the REST method specified in the **url** parameter and pass the additional parameters in **params**.</span></span>

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

## <a name="createsitescript"></a><span data-ttu-id="78fea-130">CreateSiteScript</span><span class="sxs-lookup"><span data-stu-id="78fea-130">CreateSiteScript</span></span>

<span data-ttu-id="78fea-131">Создает скрипт сайта.</span><span class="sxs-lookup"><span data-stu-id="78fea-131">Creates a new site script.</span></span>

### <a name="parameters"></a><span data-ttu-id="78fea-132">Параметры</span><span class="sxs-lookup"><span data-stu-id="78fea-132">Parameters</span></span>

|<span data-ttu-id="78fea-133">Параметр</span><span class="sxs-lookup"><span data-stu-id="78fea-133">Parameter</span></span>     | <span data-ttu-id="78fea-134">Описание</span><span class="sxs-lookup"><span data-stu-id="78fea-134">Description</span></span>  |
|--------------|--------------|
| <span data-ttu-id="78fea-135">Название</span><span class="sxs-lookup"><span data-stu-id="78fea-135">Title</span></span>       | <span data-ttu-id="78fea-136">Отображаемое имя макета сайта.</span><span class="sxs-lookup"><span data-stu-id="78fea-136">The display name of the site design.</span></span> |
| <span data-ttu-id="78fea-137">Статья</span><span class="sxs-lookup"><span data-stu-id="78fea-137">Content</span></span>     | <span data-ttu-id="78fea-138">Значение JSON, описывающее скрипт.</span><span class="sxs-lookup"><span data-stu-id="78fea-138">JSON value that describes the script.</span></span> <span data-ttu-id="78fea-139">Дополнительные сведения см. в [справочнике по JSON](site-design-json-schema.md).</span><span class="sxs-lookup"><span data-stu-id="78fea-139">For more information, see [JSON reference](site-design-json-schema.md).</span></span>|

<span data-ttu-id="78fea-140">В примере ниже создается скрипт сайта, где применяется настраиваемая тема.</span><span class="sxs-lookup"><span data-stu-id="78fea-140">The following example creates a new site script that applies a custom theme.</span></span>

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

<span data-ttu-id="78fea-141">В этом примере после вызова команды **CreateSiteScript** возвращается нотация объектов JavaScript (JSON),</span><span class="sxs-lookup"><span data-stu-id="78fea-141">Here is an example of the JSON returned after calling **CreateSiteScript**.</span></span> <span data-ttu-id="78fea-142">содержащая идентификатор нового скрипта сайта.</span><span class="sxs-lookup"><span data-stu-id="78fea-142">It contains the ID of the new site script.</span></span>

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

## <a name="getsitescripts"></a><span data-ttu-id="78fea-143">GetSiteScripts</span><span class="sxs-lookup"><span data-stu-id="78fea-143">GetSiteScripts</span></span>

<span data-ttu-id="78fea-144">Получает список сведений обо всех имеющихся скриптах сайтов.</span><span class="sxs-lookup"><span data-stu-id="78fea-144">Gets a list of information on all existing site scripts.</span></span>

### <a name="parameters"></a><span data-ttu-id="78fea-145">Параметры</span><span class="sxs-lookup"><span data-stu-id="78fea-145">Parameters</span></span>

<span data-ttu-id="78fea-146">Нет.</span><span class="sxs-lookup"><span data-stu-id="78fea-146">None.</span></span>

<span data-ttu-id="78fea-147">В приведенном ниже примере показано, как получить информацию о скрипте сайта для всех скриптов.</span><span class="sxs-lookup"><span data-stu-id="78fea-147">The following example gets the site script information for all site scripts.</span></span>

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.GetSiteScripts");
```

<span data-ttu-id="78fea-148">В этом примере JSON возвращается после вызова команды **GetSiteScripts**.</span><span class="sxs-lookup"><span data-stu-id="78fea-148">Here is an example of the JSON returned after calling **GetSiteScripts**.</span></span>

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

## <a name="getsitescriptmetadata"></a><span data-ttu-id="78fea-149">GetSiteScriptMetadata</span><span class="sxs-lookup"><span data-stu-id="78fea-149">GetSiteScriptMetadata</span></span>

<span data-ttu-id="78fea-150">Получает сведения об определенном скрипте сайта,</span><span class="sxs-lookup"><span data-stu-id="78fea-150">Gets information about a specific site script.</span></span> <span data-ttu-id="78fea-151">а также возвращает JSON для скрипта.</span><span class="sxs-lookup"><span data-stu-id="78fea-151">It also returns the JSON of the script.</span></span>

### <a name="parameters"></a><span data-ttu-id="78fea-152">Параметры</span><span class="sxs-lookup"><span data-stu-id="78fea-152">Parameters</span></span>

|<span data-ttu-id="78fea-153">Параметр</span><span class="sxs-lookup"><span data-stu-id="78fea-153">Parameter</span></span>     | <span data-ttu-id="78fea-154">Описание</span><span class="sxs-lookup"><span data-stu-id="78fea-154">Description</span></span>  |
|--------------|--------------|
| <span data-ttu-id="78fea-155">id</span><span class="sxs-lookup"><span data-stu-id="78fea-155">id</span></span>    | <span data-ttu-id="78fea-156">Идентификатор скрипта сайта, сведения о котором требуется получить.</span><span class="sxs-lookup"><span data-stu-id="78fea-156">The ID of the site script to get information about.</span></span> |

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.GetSiteScriptMetadata",
{id:"07702c07-0485-426f-b710-4704241caad9"});
```

<span data-ttu-id="78fea-157">Ниже приведен пример возвращаемой JSON после вызова команды **GetSiteScriptMetadata**.</span><span class="sxs-lookup"><span data-stu-id="78fea-157">Here is an example of the JSON returned after calling **GetSiteScriptMetadata**.</span></span>

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

## <a name="updatesitescript"></a><span data-ttu-id="78fea-158">UpdateSiteScript</span><span class="sxs-lookup"><span data-stu-id="78fea-158">UpdateSiteScript</span></span>

<span data-ttu-id="78fea-159">Обновляет скрипт сайта.</span><span class="sxs-lookup"><span data-stu-id="78fea-159">Updates a site script with new values.</span></span> <span data-ttu-id="78fea-160">В вызове REST единственным обязательным параметром является идентификатор скрипта сайта.</span><span class="sxs-lookup"><span data-stu-id="78fea-160">In the REST call all parameters are optional except the site script Id.</span></span>

### <a name="parameters"></a><span data-ttu-id="78fea-161">Параметры</span><span class="sxs-lookup"><span data-stu-id="78fea-161">Parameters</span></span>

|<span data-ttu-id="78fea-162">Параметр</span><span class="sxs-lookup"><span data-stu-id="78fea-162">Parameter</span></span>   | <span data-ttu-id="78fea-163">Описание</span><span class="sxs-lookup"><span data-stu-id="78fea-163">Description</span></span>  |
|------------|--------------|
| <span data-ttu-id="78fea-164">Id</span><span class="sxs-lookup"><span data-stu-id="78fea-164">Id</span></span>         | <span data-ttu-id="78fea-165">Идентификатор скрипта сайта, который требуется обновить.</span><span class="sxs-lookup"><span data-stu-id="78fea-165">The ID of the site script to update.</span></span> |
|<span data-ttu-id="78fea-166">Название</span><span class="sxs-lookup"><span data-stu-id="78fea-166">Title</span></span>       | <span data-ttu-id="78fea-167">(Необязательный.) Новое отображаемое имя скрипта сайта.</span><span class="sxs-lookup"><span data-stu-id="78fea-167">(optional) The new display name of the site script.</span></span> |
|<span data-ttu-id="78fea-168">Description</span><span class="sxs-lookup"><span data-stu-id="78fea-168">Description</span></span> | <span data-ttu-id="78fea-169">(Необязательный.) Новое описание скрипта сайта.</span><span class="sxs-lookup"><span data-stu-id="78fea-169">(Optional) The new description of the site script.</span></span> |
| <span data-ttu-id="78fea-170">Version</span><span class="sxs-lookup"><span data-stu-id="78fea-170">Version</span></span>    | <span data-ttu-id="78fea-171">(Необязательный.) Новый номер версии для скрипта сайта.</span><span class="sxs-lookup"><span data-stu-id="78fea-171">(Optional) The new version number of the site script.</span></span> |
| <span data-ttu-id="78fea-172">Статья</span><span class="sxs-lookup"><span data-stu-id="78fea-172">Content</span></span>    | <span data-ttu-id="78fea-173">(Необязательный.) Новый скрипт JSON, определяющий действия скрипта.</span><span class="sxs-lookup"><span data-stu-id="78fea-173">(Optional) A new JSON script defining the script actions.</span></span> <span data-ttu-id="78fea-174">Дополнительные сведения см. в статье [Схема JSON для макетов сайтов](site-design-json-schema.md).</span><span class="sxs-lookup"><span data-stu-id="78fea-174">For more information, see [Site design JSON schema](site-design-json-schema.md)</span></span> |

<span data-ttu-id="78fea-175">Ниже приведен пример обновления скрипта сайта с помощью новых значений и скрипта JSON.</span><span class="sxs-lookup"><span data-stu-id="78fea-175">Here's an example of updating an existing site script with a new JSON script and values.</span></span>

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

<span data-ttu-id="78fea-176">Вот пример JSON, возвращаемой после вызова команды **UpdateSiteScript**.</span><span class="sxs-lookup"><span data-stu-id="78fea-176">Here is an example of the JSON returned after calling **UpdateSiteScript**.</span></span>

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

## <a name="deletesitescript"></a><span data-ttu-id="78fea-177">DeleteSiteScript</span><span class="sxs-lookup"><span data-stu-id="78fea-177">DeleteSiteScript</span></span>

<span data-ttu-id="78fea-178">Удаляет скрипт сайта.</span><span class="sxs-lookup"><span data-stu-id="78fea-178">Deletes a site script.</span></span>

### <a name="parameters"></a><span data-ttu-id="78fea-179">Параметры</span><span class="sxs-lookup"><span data-stu-id="78fea-179">Parameters</span></span>

|<span data-ttu-id="78fea-180">Параметр</span><span class="sxs-lookup"><span data-stu-id="78fea-180">Parameter</span></span>   | <span data-ttu-id="78fea-181">Описание</span><span class="sxs-lookup"><span data-stu-id="78fea-181">Description</span></span>  |
|------------|--------------|
| <span data-ttu-id="78fea-182">id</span><span class="sxs-lookup"><span data-stu-id="78fea-182">id</span></span>         | <span data-ttu-id="78fea-183">Идентификатор скрипта сайта, который нужно удалить.</span><span class="sxs-lookup"><span data-stu-id="78fea-183">The ID of the site script to delete.</span></span> |

<span data-ttu-id="78fea-184">В примере ниже показано, как удалить скрипт сайта.</span><span class="sxs-lookup"><span data-stu-id="78fea-184">Here's an example of deleting a site script.</span></span>

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.DeleteSiteScript", 
{id:"07702c07-0485-426f-b710-4704241caad9"});
```

## <a name="createsitedesign"></a><span data-ttu-id="78fea-185">CreateSiteDesign</span><span class="sxs-lookup"><span data-stu-id="78fea-185">CreateSiteDesign</span></span>

<span data-ttu-id="78fea-186">Создает макет сайта, доступный пользователям при создании сайта на домашней странице SharePoint.</span><span class="sxs-lookup"><span data-stu-id="78fea-186">Creates a new site design available to users when they create a new site from the SharePoint home page.</span></span>

### <a name="parameters"></a><span data-ttu-id="78fea-187">Параметры</span><span class="sxs-lookup"><span data-stu-id="78fea-187">Parameters</span></span>

|<span data-ttu-id="78fea-188">Параметр</span><span class="sxs-lookup"><span data-stu-id="78fea-188">Parameter</span></span>  | <span data-ttu-id="78fea-189">Описание</span><span class="sxs-lookup"><span data-stu-id="78fea-189">Description</span></span>  |
|-----------|--------------|
| <span data-ttu-id="78fea-190">id</span><span class="sxs-lookup"><span data-stu-id="78fea-190">id</span></span>         | <span data-ttu-id="78fea-191">Идентификатор макета сайта, который требуется применить.</span><span class="sxs-lookup"><span data-stu-id="78fea-191">The ID of the site design to delete.</span></span> |
|<span data-ttu-id="78fea-192">Title</span><span class="sxs-lookup"><span data-stu-id="78fea-192">Title</span></span>                 | <span data-ttu-id="78fea-193">Отображаемое имя макета сайта.</span><span class="sxs-lookup"><span data-stu-id="78fea-193">The display name of the site design.</span></span> |
|<span data-ttu-id="78fea-194">WebTemplate</span><span class="sxs-lookup"><span data-stu-id="78fea-194">WebTemplate</span></span>           | <span data-ttu-id="78fea-195">Указывает, к какому базовому шаблону будет добавлен макет.</span><span class="sxs-lookup"><span data-stu-id="78fea-195">Identifies which base template to add the design to.</span></span> <span data-ttu-id="78fea-196">Значение **64** обозначает шаблон сайта группы, а значение **68** — шаблон сайта для общения.</span><span class="sxs-lookup"><span data-stu-id="78fea-196">Use the value **64** for the Team site template, and the value **68** for the Communication site template.</span></span> |
|<span data-ttu-id="78fea-197">SiteScripts</span><span class="sxs-lookup"><span data-stu-id="78fea-197">SiteScripts</span></span>           | <span data-ttu-id="78fea-198">Массив из одного или нескольких скриптов сайта.</span><span class="sxs-lookup"><span data-stu-id="78fea-198">An array of one or more site scripts.</span></span> <span data-ttu-id="78fea-199">Каждый из них определяется по идентификатору.</span><span class="sxs-lookup"><span data-stu-id="78fea-199">Each is identified by an ID.</span></span> <span data-ttu-id="78fea-200">Скрипты будут выполняться в указанном порядке.</span><span class="sxs-lookup"><span data-stu-id="78fea-200">The scripts will run in the order listed.</span></span> |
|<span data-ttu-id="78fea-201">Description</span><span class="sxs-lookup"><span data-stu-id="78fea-201">Description</span></span>         | <span data-ttu-id="78fea-202">(Необязательный.) Отображаемое описание макета сайта.</span><span class="sxs-lookup"><span data-stu-id="78fea-202">(Optional) The display description of site design.</span></span> |
|<span data-ttu-id="78fea-203">PreviewImageUrl</span><span class="sxs-lookup"><span data-stu-id="78fea-203">PreviewImageUrl</span></span>     | <span data-ttu-id="78fea-204">(Необязательный.) URL-адрес изображения для предварительного просмотра.</span><span class="sxs-lookup"><span data-stu-id="78fea-204">(Optional) The URL of a preview image.</span></span> <span data-ttu-id="78fea-205">Если он не указан, в SharePoint будет использоваться стандартное изображение.</span><span class="sxs-lookup"><span data-stu-id="78fea-205">If none is specified SharePoint will use a generic image.</span></span> |
|<span data-ttu-id="78fea-206">PreviewImageAltText</span><span class="sxs-lookup"><span data-stu-id="78fea-206">PreviewImageAltText</span></span> | <span data-ttu-id="78fea-207">(Необязательный.) Замещающий текст с описанием изображения для специальных возможностей.</span><span class="sxs-lookup"><span data-stu-id="78fea-207">(Optional) The alt text description of the image for accessibility.</span></span> |
|<span data-ttu-id="78fea-208">IsDefault</span><span class="sxs-lookup"><span data-stu-id="78fea-208">IsDefault</span></span>           | <span data-ttu-id="78fea-209">(Необязательный.) Выберите значение **true**, чтобы макет сайта применялся как стандартный. В противном случае установите **false**.</span><span class="sxs-lookup"><span data-stu-id="78fea-209">(Optional) **true** if the site design is applied as the default site design; otherwise, **false**.</span></span> <span data-ttu-id="78fea-210">Дополнительные сведения см. в статье [Настройка стандартного макета сайта](customize-default-site-design.md)</span><span class="sxs-lookup"><span data-stu-id="78fea-210">For more information see [Customize a default site design](customize-default-site-design.md)</span></span> |

<span data-ttu-id="78fea-211">Ниже представлен пример создания макета сайта.</span><span class="sxs-lookup"><span data-stu-id="78fea-211">Here's an example of creating a new site design.</span></span>

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

<span data-ttu-id="78fea-212">Вот пример JSON, возвращаемой после вызова команды **CreateSiteDesign**.</span><span class="sxs-lookup"><span data-stu-id="78fea-212">Here is an example of the JSON returned after calling **CreateSiteDesign**.</span></span> <span data-ttu-id="78fea-213">В ней также содержится идентификатор нового макета сайта.</span><span class="sxs-lookup"><span data-stu-id="78fea-213">It contains the ID of the new site design.</span></span>

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

## <a name="applysitedesign"></a><span data-ttu-id="78fea-214">ApplySiteDesign</span><span class="sxs-lookup"><span data-stu-id="78fea-214">ApplySiteDesign</span></span>

<span data-ttu-id="78fea-215">Применяет макет сайта к существующему семейству веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="78fea-215">Applies a site design to an existing site collection.</span></span>

### <a name="parameters"></a><span data-ttu-id="78fea-216">Параметры</span><span class="sxs-lookup"><span data-stu-id="78fea-216">Parameters</span></span>

|<span data-ttu-id="78fea-217">Параметр</span><span class="sxs-lookup"><span data-stu-id="78fea-217">Parameter</span></span>   | <span data-ttu-id="78fea-218">Описание</span><span class="sxs-lookup"><span data-stu-id="78fea-218">Description</span></span>  |
|------------|--------------|
| <span data-ttu-id="78fea-219">id</span><span class="sxs-lookup"><span data-stu-id="78fea-219">id</span></span>         | <span data-ttu-id="78fea-220">Идентификатор макета сайта, который требуется применить.</span><span class="sxs-lookup"><span data-stu-id="78fea-220">The ID of the site design to delete.</span></span> |
| <span data-ttu-id="78fea-221">webUrl</span><span class="sxs-lookup"><span data-stu-id="78fea-221">webUrl</span></span>         | <span data-ttu-id="78fea-222">URL-адрес семейства веб-сайтов, к которому необходимо применить макет сайта.</span><span class="sxs-lookup"><span data-stu-id="78fea-222">The Url of the site collection where you want to apply the site design.</span></span> |

<span data-ttu-id="78fea-223">В примере ниже показано применение макета сайта к семейству веб-сайтов ProjectGo.</span><span class="sxs-lookup"><span data-stu-id="78fea-223">Here's an example of applying a site design to the ProjectGo site collection.</span></span>

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.ApplySiteDesign", {siteDesignId: "614f9b28-3e85-4ec9-a961-5971ea086cca", "webUrl":"https://contoso.microsoft.com/sites/projectgo"});
```

## <a name="getsitedesigns"></a><span data-ttu-id="78fea-224">GetSiteDesigns</span><span class="sxs-lookup"><span data-stu-id="78fea-224">GetSiteDesigns</span></span>

<span data-ttu-id="78fea-225">Получает список сведений об имеющихся макетах сайтов.</span><span class="sxs-lookup"><span data-stu-id="78fea-225">Gets a list of information on existing site designs.</span></span>

### <a name="parameters"></a><span data-ttu-id="78fea-226">Параметры</span><span class="sxs-lookup"><span data-stu-id="78fea-226">Parameters</span></span>

<span data-ttu-id="78fea-227">None</span><span class="sxs-lookup"><span data-stu-id="78fea-227">None</span></span>

<span data-ttu-id="78fea-228">Ниже приведен пример получения всех макетов сайта.</span><span class="sxs-lookup"><span data-stu-id="78fea-228">Here's an example of getting all the site designs.</span></span>

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.GetSiteDesigns");
```

<span data-ttu-id="78fea-229">Вот пример JSON, возвращаемой после вызова команды **GetSiteDesigns**.</span><span class="sxs-lookup"><span data-stu-id="78fea-229">Here is an example of the JSON returned after calling **GetSiteDesigns**.</span></span>

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

## <a name="getsitedesignmetadata"></a><span data-ttu-id="78fea-230">GetSiteDesignMetadata</span><span class="sxs-lookup"><span data-stu-id="78fea-230">GetSiteDesignMetadata</span></span>

<span data-ttu-id="78fea-231">Получает сведения об определенном макете сайта.</span><span class="sxs-lookup"><span data-stu-id="78fea-231">Gets information about a specific site design.</span></span>

### <a name="parameters"></a><span data-ttu-id="78fea-232">Параметры</span><span class="sxs-lookup"><span data-stu-id="78fea-232">Parameters</span></span>

|<span data-ttu-id="78fea-233">Параметр</span><span class="sxs-lookup"><span data-stu-id="78fea-233">Parameter</span></span>   | <span data-ttu-id="78fea-234">Описание</span><span class="sxs-lookup"><span data-stu-id="78fea-234">Description</span></span>  |
|------------|--------------|
| <span data-ttu-id="78fea-235">id</span><span class="sxs-lookup"><span data-stu-id="78fea-235">id</span></span>         | <span data-ttu-id="78fea-236">Идентификатор макета сайта, сведения о котором требуется получить.</span><span class="sxs-lookup"><span data-stu-id="78fea-236">The ID of the site design to get information about.</span></span> |

<span data-ttu-id="78fea-237">В примере ниже показано, как получить сведения об определенном макете сайта с помощью его идентификатора.</span><span class="sxs-lookup"><span data-stu-id="78fea-237">Here's an example of getting information about a specific site design by ID.</span></span>

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.GetSiteDesignMetadata", 
{id:"614f9b28-3e85-4ec9-a961-5971ea086cca"});
```

<span data-ttu-id="78fea-238">Вот пример JSON, возвращаемой после вызова команды **GetSiteDesignMetadata**.</span><span class="sxs-lookup"><span data-stu-id="78fea-238">Here is an example of the JSON returned after calling **GetSiteDesignMetadata**.</span></span>

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

## <a name="updatesitedesign"></a><span data-ttu-id="78fea-239">UpdateSiteDesign</span><span class="sxs-lookup"><span data-stu-id="78fea-239">UpdateSiteDesign</span></span>

<span data-ttu-id="78fea-240">Обновляет макет сайта.</span><span class="sxs-lookup"><span data-stu-id="78fea-240">Updates a site design with new values.</span></span> <span data-ttu-id="78fea-241">В вызове REST единственным обязательным параметром является идентификатор скрипта сайта. ПРИМЕЧАНИЕ. Если вы присвоили параметру IsDefault значение TRUE и хотите, чтобы это значение сохранилось, передайте этот параметр еще раз (иначе будет восстановлено значение FALSE).</span><span class="sxs-lookup"><span data-stu-id="78fea-241">In the REST call all parameters are optional except the site script Id. NOTE: if you had previously set the IsDefault parameter to TRUE and wish it to remain true, you must pass in this parameter again (otherwise it will be reset to FALSE).</span></span> 

### <a name="parameters"></a><span data-ttu-id="78fea-242">Параметры</span><span class="sxs-lookup"><span data-stu-id="78fea-242">Parameters</span></span>

|<span data-ttu-id="78fea-243">Параметр</span><span class="sxs-lookup"><span data-stu-id="78fea-243">Parameter</span></span>  | <span data-ttu-id="78fea-244">Описание</span><span class="sxs-lookup"><span data-stu-id="78fea-244">Description</span></span>  |
|-----------|--------------|
|<span data-ttu-id="78fea-245">Id</span><span class="sxs-lookup"><span data-stu-id="78fea-245">Id</span></span>         | <span data-ttu-id="78fea-246">Идентификатор макета сайта, который требуется обновить.</span><span class="sxs-lookup"><span data-stu-id="78fea-246">The ID of the site design to update.</span></span> |
|<span data-ttu-id="78fea-247">Название</span><span class="sxs-lookup"><span data-stu-id="78fea-247">Title</span></span>                 |  <span data-ttu-id="78fea-248">(Необязательный.) Новое отображаемое имя обновленного макета сайта.</span><span class="sxs-lookup"><span data-stu-id="78fea-248">(optional) The new display name of the updated site design.</span></span> |
|<span data-ttu-id="78fea-249">WebTemplate</span><span class="sxs-lookup"><span data-stu-id="78fea-249">WebTemplate</span></span>           | <span data-ttu-id="78fea-250">(Необязательный.) Новый шаблон для добавления макета сайта.</span><span class="sxs-lookup"><span data-stu-id="78fea-250">(optional) The new template to add the site design to.</span></span> <span data-ttu-id="78fea-251">Значение **64** обозначает шаблон сайта группы, а значение **68** — шаблон сайта для общения.</span><span class="sxs-lookup"><span data-stu-id="78fea-251">Use the value **64** for the Team site template, and the value **68** for the Communication site template.</span></span> |
|<span data-ttu-id="78fea-252">SiteScripts</span><span class="sxs-lookup"><span data-stu-id="78fea-252">SiteScripts</span></span>           | <span data-ttu-id="78fea-253">(Необязательный.) Новый массив из одного или нескольких скриптов сайта.</span><span class="sxs-lookup"><span data-stu-id="78fea-253">(optional) A new array of one or more site scripts.</span></span> <span data-ttu-id="78fea-254">Каждый из них определяется по идентификатору.</span><span class="sxs-lookup"><span data-stu-id="78fea-254">Each is identified by an ID.</span></span> <span data-ttu-id="78fea-255">Скрипты будут выполняться в указанном порядке.</span><span class="sxs-lookup"><span data-stu-id="78fea-255">The scripts will run in the order listed.</span></span> |
|<span data-ttu-id="78fea-256">Description</span><span class="sxs-lookup"><span data-stu-id="78fea-256">Description</span></span>         | <span data-ttu-id="78fea-257">(Необязательный.) Новое отображаемое описание обновленного макета сайта.</span><span class="sxs-lookup"><span data-stu-id="78fea-257">(Optional) The new display description of updated site design.</span></span> |
|<span data-ttu-id="78fea-258">PreviewImageUrl</span><span class="sxs-lookup"><span data-stu-id="78fea-258">PreviewImageUrl</span></span>     | <span data-ttu-id="78fea-259">(Необязательный.) Новый URL-адрес для предварительного просмотра изображения.</span><span class="sxs-lookup"><span data-stu-id="78fea-259">(Optional) The new URL of a preview image.</span></span> |
|<span data-ttu-id="78fea-260">PreviewImageAltText</span><span class="sxs-lookup"><span data-stu-id="78fea-260">PreviewImageAltText</span></span> | <span data-ttu-id="78fea-261">(Необязательный.) Новый замещающий текст с описанием изображения для специальных возможностей.</span><span class="sxs-lookup"><span data-stu-id="78fea-261">(Optional) The new alt text description of the image for accessibility.</span></span> |
|<span data-ttu-id="78fea-262">IsDefault</span><span class="sxs-lookup"><span data-stu-id="78fea-262">IsDefault</span></span>           | <span data-ttu-id="78fea-263">(Необязательный.) Выберите значение **true**, чтобы макет сайта применялся как стандартный. В противном случае установите **false**.</span><span class="sxs-lookup"><span data-stu-id="78fea-263">(Optional) **true** if the site design is applied as the default site design; otherwise, **false**.</span></span> <span data-ttu-id="78fea-264">Дополнительные сведения см. в статье [Настройка стандартного макета сайта](customize-default-site-design.md)</span><span class="sxs-lookup"><span data-stu-id="78fea-264">For more information see [Customize a default site design](customize-default-site-design.md)</span></span> |

<span data-ttu-id="78fea-265">В примере ниже обновляются все значения существующего макета сайта.</span><span class="sxs-lookup"><span data-stu-id="78fea-265">Here's an example that updates every value on an existing site design.</span></span>

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

<span data-ttu-id="78fea-266">Вот пример JSON, возвращаемой после вызова команды **UpdateSiteDesign**.</span><span class="sxs-lookup"><span data-stu-id="78fea-266">Here is an example of the JSON returned after calling **UpdateSiteDesign**.</span></span>

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

## <a name="deletesitedesign"></a><span data-ttu-id="78fea-267">DeleteSiteDesign</span><span class="sxs-lookup"><span data-stu-id="78fea-267">DeleteSiteDesign</span></span>

<span data-ttu-id="78fea-268">Удаляет макет сайта.</span><span class="sxs-lookup"><span data-stu-id="78fea-268">Deletes a site design.</span></span>

### <a name="parameters"></a><span data-ttu-id="78fea-269">Параметры</span><span class="sxs-lookup"><span data-stu-id="78fea-269">Parameters</span></span>

|<span data-ttu-id="78fea-270">Параметр</span><span class="sxs-lookup"><span data-stu-id="78fea-270">Parameter</span></span>   | <span data-ttu-id="78fea-271">Описание</span><span class="sxs-lookup"><span data-stu-id="78fea-271">Description</span></span>  |
|------------|--------------|
| <span data-ttu-id="78fea-272">id</span><span class="sxs-lookup"><span data-stu-id="78fea-272">id</span></span>         | <span data-ttu-id="78fea-273">Идентификатор макета сайта, который требуется удалить.</span><span class="sxs-lookup"><span data-stu-id="78fea-273">The ID of the site design to delete.</span></span> |

<span data-ttu-id="78fea-274">В примере ниже показано, как удалить макет сайта.</span><span class="sxs-lookup"><span data-stu-id="78fea-274">Here's an example of deleting a site design.</span></span>

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.DeleteSiteDesign", 
{id:"f9e76746-5076-4bd2-bad3-e611c488fa85"});
```

## <a name="getsitedesignrights"></a><span data-ttu-id="78fea-275">GetSiteDesignRights</span><span class="sxs-lookup"><span data-stu-id="78fea-275">GetSiteDesignRights</span></span>

<span data-ttu-id="78fea-276">Получает список субъектов, имеющих доступ к макету сайта.</span><span class="sxs-lookup"><span data-stu-id="78fea-276">Gets a list of principals that have access to a site design.</span></span>


### <a name="parameters"></a><span data-ttu-id="78fea-277">Параметры</span><span class="sxs-lookup"><span data-stu-id="78fea-277">Parameters</span></span>

|<span data-ttu-id="78fea-278">Параметр</span><span class="sxs-lookup"><span data-stu-id="78fea-278">Parameter</span></span>   | <span data-ttu-id="78fea-279">Описание</span><span class="sxs-lookup"><span data-stu-id="78fea-279">Description</span></span>  |
|------------|--------------|
| <span data-ttu-id="78fea-280">id</span><span class="sxs-lookup"><span data-stu-id="78fea-280">id</span></span>         | <span data-ttu-id="78fea-281">Идентификатор макета сайта, откуда требуется получить сведения о правах.</span><span class="sxs-lookup"><span data-stu-id="78fea-281">The ID of the site design to get rights information from.</span></span> |

<span data-ttu-id="78fea-282">Ниже приведен пример получения сведений о правах на просмотр для определенного макета сайта.</span><span class="sxs-lookup"><span data-stu-id="78fea-282">Here's an example of getting view rights for a specific site design.</span></span>

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.GetSiteDesignRights", 
{id:"dc076f7b-6c15-4d76-8f85-948a17f5dd18"});
```

<span data-ttu-id="78fea-283">Вот пример JSON, возвращаемой после вызова команды **GetSiteDesignRights**.</span><span class="sxs-lookup"><span data-stu-id="78fea-283">Here is an example of the JSON returned after calling **GetSiteDesignRights**.</span></span>

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

## <a name="grantsitedesignrights"></a><span data-ttu-id="78fea-284">GrantSiteDesignRights</span><span class="sxs-lookup"><span data-stu-id="78fea-284">GrantSiteDesignRights</span></span>

<span data-ttu-id="78fea-285">Предоставляет доступ к макету сайта для одного или нескольких субъектов.</span><span class="sxs-lookup"><span data-stu-id="78fea-285">Grants access to a site design for one or more principals.</span></span>

### <a name="parameters"></a><span data-ttu-id="78fea-286">Параметры</span><span class="sxs-lookup"><span data-stu-id="78fea-286">Parameters</span></span>

|<span data-ttu-id="78fea-287">Параметр</span><span class="sxs-lookup"><span data-stu-id="78fea-287">Parameter</span></span>   | <span data-ttu-id="78fea-288">Описание</span><span class="sxs-lookup"><span data-stu-id="78fea-288">Description</span></span>  |
|------------|--------------|
| <span data-ttu-id="78fea-289">id</span><span class="sxs-lookup"><span data-stu-id="78fea-289">id</span></span>         | <span data-ttu-id="78fea-290">Идентификатор макета сайта, которому необходимо предоставить права.</span><span class="sxs-lookup"><span data-stu-id="78fea-290">The ID of the site design to grant rights on.</span></span> |
| <span data-ttu-id="78fea-291">principalNames</span><span class="sxs-lookup"><span data-stu-id="78fea-291">principalNames</span></span> | <span data-ttu-id="78fea-292">Массив из одного или нескольких субъектов, которым необходимо предоставить права на просмотр.</span><span class="sxs-lookup"><span data-stu-id="78fea-292">An array of one or more principals to grant view rights.</span></span> <span data-ttu-id="78fea-293">Субъектами могут быть пользователи или группы безопасности, поддерживающие почту, в формате "псевдоним" или "псевдоним@\<*доменное имя*\>.com"</span><span class="sxs-lookup"><span data-stu-id="78fea-293">Principals can be users or mail-enabled security groups in the form of "alias" or "alias@\<*domain name*\>.com"</span></span> |
| <span data-ttu-id="78fea-294">grantedRights</span><span class="sxs-lookup"><span data-stu-id="78fea-294">grantedRights</span></span> | <span data-ttu-id="78fea-295">Всегда задавайте значение **1**,</span><span class="sxs-lookup"><span data-stu-id="78fea-295">Always set to **1**.</span></span> <span data-ttu-id="78fea-296">соответствующее праву **Просмотр**.</span><span class="sxs-lookup"><span data-stu-id="78fea-296">This represents the **View** right.</span></span> |

<span data-ttu-id="78fea-297">В примере ниже показано, как предоставить права на просмотр макету сайта для пользователей Nestor и Patti (вымышленные пользователи в корпорации Contoso.)</span><span class="sxs-lookup"><span data-stu-id="78fea-297">Here's an example of granting view rights to a site design for Nestor and Patti (fictional users at Contoso.)</span></span>

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.GrantSiteDesignRights", {
  "id": "dc076f7b-6c15-4d76-8f85-948a17f5dd18",
  "principalNames": [ "NestorW@contoso.onmicrosoft.com", "PattiF@contoso.onmicrosoft.com" ],
  "grantedRights": 1
});
```

## <a name="revokesitedesignrights"></a><span data-ttu-id="78fea-298">RevokeSiteDesignRights</span><span class="sxs-lookup"><span data-stu-id="78fea-298">RevokeSiteDesignRights</span></span>

<span data-ttu-id="78fea-299">Отзывает доступ к макету сайта для одного или нескольких субъектов.</span><span class="sxs-lookup"><span data-stu-id="78fea-299">Revokes access from a site design for one or more principals.</span></span>

### <a name="parameters"></a><span data-ttu-id="78fea-300">Параметры</span><span class="sxs-lookup"><span data-stu-id="78fea-300">Parameters</span></span>

|<span data-ttu-id="78fea-301">Параметр</span><span class="sxs-lookup"><span data-stu-id="78fea-301">Parameter</span></span>   | <span data-ttu-id="78fea-302">Описание</span><span class="sxs-lookup"><span data-stu-id="78fea-302">Description</span></span>  |
|------------|--------------|
| <span data-ttu-id="78fea-303">id</span><span class="sxs-lookup"><span data-stu-id="78fea-303">id</span></span>         | <span data-ttu-id="78fea-304">Идентификатор макета сайта, у которого требуется отозвать права.</span><span class="sxs-lookup"><span data-stu-id="78fea-304">The ID of the site design to revoke rights from.</span></span> |
| <span data-ttu-id="78fea-305">principalNames</span><span class="sxs-lookup"><span data-stu-id="78fea-305">principalNames</span></span> | <span data-ttu-id="78fea-306">Массив из одного или нескольких субъектов, для которых необходимо отозвать права.</span><span class="sxs-lookup"><span data-stu-id="78fea-306">An array of one or more principals to revoke view rights from.</span></span> <span data-ttu-id="78fea-307">Если права на макет сайта отозваны для всех субъектов, макет сайта становится видимым для всех.</span><span class="sxs-lookup"><span data-stu-id="78fea-307">If all principals have rights revoked on the site design, the site design becomes viewable to everyone.</span></span> |

<span data-ttu-id="78fea-308">В примере ниже показано, как у макета сайта отзываются права на просмотр для пользователя Patti (вымышленного пользователя в корпорации Contoso).</span><span class="sxs-lookup"><span data-stu-id="78fea-308">Here's an example of revoking view rights from a site design for Patti (fictional user at Contoso.)</span></span>

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.RevokeSiteDesignRights", 
{id:"5d4756e9-e1f5-42f7-afa7-5fa5aac170aa",
 principalNames:["debrab@Contoso.sharepoint.com"] });
```
