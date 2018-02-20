---
title: "REST API для работы с макетами сайтов SharePoint"
description: "Узнайте, как работать с макетами сайтов SharePoint при помощи интерфейса REST для SharePoint, выполняя базовые операции создания, чтения, обновления и удаления (CRUD)."
ms.date: 12/14/2017
ms.openlocfilehash: a230c66d55ab60b900ae60a31c37f0cf75f1a789
ms.sourcegitcommit: e157d51378190ddfed6394ba154ce66141c8ca33
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/19/2018
---
# <a name="site-design-and-site-script-rest-api"></a><span data-ttu-id="7a49d-103">REST API для работы с макетами и скриптами сайтов</span><span class="sxs-lookup"><span data-stu-id="7a49d-103">Site design and site script REST API</span></span>

> [!NOTE]
> <span data-ttu-id="7a49d-104">Макеты и скрипты сайтов находятся на стадии тестирования и могут меняться.</span><span class="sxs-lookup"><span data-stu-id="7a49d-104">Site designs and site scripts are in preview and are subject to change.</span></span> <span data-ttu-id="7a49d-105">В настоящее время в рабочих средах их можно использовать только в выпуске Targeted.</span><span class="sxs-lookup"><span data-stu-id="7a49d-105">They are currently only supported for use in production environments in Targeted Release.</span></span>

<span data-ttu-id="7a49d-106">При помощи интерфейса REST для SharePoint можно выполнять операции CRUD (создание, чтение, обновление и удаление) с макетами и скриптами сайтов.</span><span class="sxs-lookup"><span data-stu-id="7a49d-106">You can use the the SharePoint REST interface to perform basic create, read, update, and delete (CRUD) operations on site designs and site scripts.</span></span>

<span data-ttu-id="7a49d-107">Служба REST в SharePoint Online (а также локальной среде SharePoint 2016 или более поздней версии) поддерживает объединение нескольких запросов в один вызов службы с помощью параметра запроса OData $batch.</span><span class="sxs-lookup"><span data-stu-id="7a49d-107">The SharePoint Online (and SharePoint 2016 and later on-premises) REST service supports combining multiple requests into a single call to the service by using the OData $batch query option.</span></span> <span data-ttu-id="7a49d-108">Подробные сведения и ссылки на примеры кода см. в статье [Отправка пакетных запросов с помощью интерфейсов REST API](../sp-add-ins/make-batch-requests-with-the-rest-apis.md).</span><span class="sxs-lookup"><span data-stu-id="7a49d-108">For details and links to code samples, see [Make batch requests with the REST APIs](../sp-add-ins/make-batch-requests-with-the-rest-apis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7a49d-109">Необходимые условия</span><span class="sxs-lookup"><span data-stu-id="7a49d-109">Prerequisites</span></span>
<span data-ttu-id="7a49d-110">Прежде чем приступить к работе, убедитесь, что вы знакомы с понятиями, описанными в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="7a49d-110">Before you get started, make sure that you're familiar with the following:</span></span>
- <span data-ttu-id="7a49d-111">[Знакомство со службой REST в SharePoint](../sp-add-ins/get-to-know-the-sharepoint-rest-service.md);</span><span class="sxs-lookup"><span data-stu-id="7a49d-111">[Get to know the SharePoint REST service](../sp-add-ins/get-to-know-the-sharepoint-rest-service.md)</span></span> 
- [<span data-ttu-id="7a49d-112">Выполнение базовых операций с использованием конечных точек SharePoint REST</span><span class="sxs-lookup"><span data-stu-id="7a49d-112">Complete basic operations using SharePoint REST endpoints</span></span>](../sp-add-ins/complete-basic-operations-using-sharepoint-rest-endpoints.md)

## <a name="rest-commands"></a><span data-ttu-id="7a49d-113">Команды REST</span><span class="sxs-lookup"><span data-stu-id="7a49d-113">REST commands</span></span>

<span data-ttu-id="7a49d-114">Для работы с макетами и скриптами сайтов доступны следующие команды REST:</span><span class="sxs-lookup"><span data-stu-id="7a49d-114">The following REST commands are available for working with site designs and site scripts:</span></span>

- <span data-ttu-id="7a49d-115">**CreateSiteScript** &mdash; создание скрипта сайта.</span><span class="sxs-lookup"><span data-stu-id="7a49d-115">**CreateSiteScript** &mdash; Creates a new site script.</span></span>
- <span data-ttu-id="7a49d-116">**GetSiteScripts** &mdash; получение списка сведений об имеющихся скриптах сайтов.</span><span class="sxs-lookup"><span data-stu-id="7a49d-116">**GetSiteScripts** &mdash; Gets a list of information on existing site scripts.</span></span>
- <span data-ttu-id="7a49d-117">**GetSiteScriptMetadata** &mdash; получение сведений об определенном скрипте сайта.</span><span class="sxs-lookup"><span data-stu-id="7a49d-117">**GetSiteScriptMetadata** &mdash; Gets information about a specific site script.</span></span>
- <span data-ttu-id="7a49d-118">**UpdateSiteScript** &mdash; обновление скрипта сайта с использованием новых значений.</span><span class="sxs-lookup"><span data-stu-id="7a49d-118">**UpdateSiteScript** &mdash; Updates a site script with new values.</span></span>
- <span data-ttu-id="7a49d-119">**DeleteSiteScript** &mdash; удаление скрипта сайта.</span><span class="sxs-lookup"><span data-stu-id="7a49d-119">**DeleteSiteScript** &mdash; Deletes a site script.</span></span>
- <span data-ttu-id="7a49d-120">**CreateSiteDesign** &mdash; создание макета сайта.</span><span class="sxs-lookup"><span data-stu-id="7a49d-120">**CreateSiteDesign** &mdash; Creates a site design.</span></span>
- <span data-ttu-id="7a49d-121">**GetSiteDesigns** &mdash; получение списка сведений об имеющихся макетах сайтов.</span><span class="sxs-lookup"><span data-stu-id="7a49d-121">**GetSiteDesigns** &mdash; Gets a list of information on existing site designs.</span></span>
- <span data-ttu-id="7a49d-122">**GetSiteDesignMetadata** &mdash; получение сведений об определенном макете сайта.</span><span class="sxs-lookup"><span data-stu-id="7a49d-122">**GetSiteDesignMetadata** &mdash; Gets information about a sepcific site design.</span></span>
- <span data-ttu-id="7a49d-123">**UpdateSiteDesign** &mdash; обновление макета сайта с использованием новых значений.</span><span class="sxs-lookup"><span data-stu-id="7a49d-123">**UpdateSiteDesign** &mdash; Updates a site design with new values.</span></span>
- <span data-ttu-id="7a49d-124">**DeleteSiteDesign** &mdash; удаление макета сайта.</span><span class="sxs-lookup"><span data-stu-id="7a49d-124">**DeleteSiteDesign** &mdash; Deletes a site design.</span></span>
- <span data-ttu-id="7a49d-125">**GetSiteDesignRights** &mdash; получение списка субъектов, имеющих доступ к макету сайта.</span><span class="sxs-lookup"><span data-stu-id="7a49d-125">**GetSiteDesignRights** &mdash; Gets a list of principals that have access to a site design.</span></span>
- <span data-ttu-id="7a49d-126">**GrantSiteDesignRights** &mdash; предоставление доступа к макету сайта для одного или нескольких субъектов.</span><span class="sxs-lookup"><span data-stu-id="7a49d-126">**GrantSiteDesignRights** &mdash; Grants access to a site design for one or more principals.</span></span>
- <span data-ttu-id="7a49d-127">**RevokeSiteDesignRights** &mdash; отзыв доступа к макету сайта для одного или нескольких субъектов.</span><span class="sxs-lookup"><span data-stu-id="7a49d-127">**RevokeSiteDesignRights** &mdash; Revokes access from a site design for one or more principals.</span></span>

## <a name="create-a-function-to-send-rest-requests"></a><span data-ttu-id="7a49d-128">Создание функции для отправки запросов REST</span><span class="sxs-lookup"><span data-stu-id="7a49d-128">Create a function to send REST requests</span></span>

<span data-ttu-id="7a49d-129">Чтобы работать с REST API, рекомендуем создать вспомогательную функцию для отправки вызовов REST.</span><span class="sxs-lookup"><span data-stu-id="7a49d-129">To work with the REST API we recommend creating a helper function to make the REST calls.</span></span> <span data-ttu-id="7a49d-130">Приведенная ниже функция **RestRequest** вызывает метод REST, указанный в параметре **url**, и передает дополнительные параметры из аргумента **params**.</span><span class="sxs-lookup"><span data-stu-id="7a49d-130">The following **RestRequest** function will call the REST method specified in the **url** parameter and pass the additional parameters in **params**.</span></span>

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

## <a name="createsitescript"></a><span data-ttu-id="7a49d-131">CreateSiteScript</span><span class="sxs-lookup"><span data-stu-id="7a49d-131">CreateSiteScript</span></span>

<span data-ttu-id="7a49d-132">Создает скрипт сайта.</span><span class="sxs-lookup"><span data-stu-id="7a49d-132">Creates a new site script.</span></span>

### <a name="parameters"></a><span data-ttu-id="7a49d-133">Параметры</span><span class="sxs-lookup"><span data-stu-id="7a49d-133">Parameters</span></span>

|<span data-ttu-id="7a49d-134">Параметр</span><span class="sxs-lookup"><span data-stu-id="7a49d-134">Parameter</span></span>     | <span data-ttu-id="7a49d-135">Описание</span><span class="sxs-lookup"><span data-stu-id="7a49d-135">Description</span></span>  |
|--------------|--------------|
| <span data-ttu-id="7a49d-136">Название</span><span class="sxs-lookup"><span data-stu-id="7a49d-136">Title</span></span>       | <span data-ttu-id="7a49d-137">Отображаемое имя макета сайта.</span><span class="sxs-lookup"><span data-stu-id="7a49d-137">The display name of the site design.</span></span> |
| <span data-ttu-id="7a49d-138">Статья</span><span class="sxs-lookup"><span data-stu-id="7a49d-138">Content</span></span>     | <span data-ttu-id="7a49d-139">Значение JSON, описывающее скрипт.</span><span class="sxs-lookup"><span data-stu-id="7a49d-139">JSON value that describes the script.</span></span> <span data-ttu-id="7a49d-140">Дополнительные сведения см. в [справочнике по JSON](site-design-json-schema.md).</span><span class="sxs-lookup"><span data-stu-id="7a49d-140">For more information, see [JSON reference](site-design-json-schema.md).</span></span>|

<span data-ttu-id="7a49d-141">В примере ниже создается скрипт сайта, где применяется настраиваемая тема.</span><span class="sxs-lookup"><span data-stu-id="7a49d-141">The following example creates a new site script that applies a custom theme.</span></span>

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

<span data-ttu-id="7a49d-142">В этом примере после вызова команды **CreateSiteScript** возвращается нотация объектов JavaScript (JSON),</span><span class="sxs-lookup"><span data-stu-id="7a49d-142">Here is an example of the JSON returned after calling **CreateSiteScript**.</span></span> <span data-ttu-id="7a49d-143">содержащая идентификатор нового скрипта сайта.</span><span class="sxs-lookup"><span data-stu-id="7a49d-143">It contains the ID of the new site script.</span></span>

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

## <a name="getsitescripts"></a><span data-ttu-id="7a49d-144">GetSiteScripts</span><span class="sxs-lookup"><span data-stu-id="7a49d-144">GetSiteScripts</span></span>

<span data-ttu-id="7a49d-145">Получает список сведений обо всех имеющихся скриптах сайтов.</span><span class="sxs-lookup"><span data-stu-id="7a49d-145">Gets a list of information on all existing site scripts.</span></span>

### <a name="parameters"></a><span data-ttu-id="7a49d-146">Параметры</span><span class="sxs-lookup"><span data-stu-id="7a49d-146">Parameters</span></span>

<span data-ttu-id="7a49d-147">Нет.</span><span class="sxs-lookup"><span data-stu-id="7a49d-147">None.</span></span>

<span data-ttu-id="7a49d-148">В приведенном ниже примере показано, как получить информацию о скрипте сайта для всех скриптов.</span><span class="sxs-lookup"><span data-stu-id="7a49d-148">The following example gets the site script information for all site scripts.</span></span>

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.GetSiteScripts");
```

<span data-ttu-id="7a49d-149">В этом примере JSON возвращается после вызова команды **GetSiteScripts**.</span><span class="sxs-lookup"><span data-stu-id="7a49d-149">Here is an example of the JSON returned after calling **GetSiteScripts**.</span></span>

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

## <a name="getsitescriptmetadata"></a><span data-ttu-id="7a49d-150">GetSiteScriptMetadata</span><span class="sxs-lookup"><span data-stu-id="7a49d-150">GetSiteScriptMetadata</span></span>

<span data-ttu-id="7a49d-151">Получает сведения об определенном скрипте сайта,</span><span class="sxs-lookup"><span data-stu-id="7a49d-151">Gets information about a specific site script.</span></span> <span data-ttu-id="7a49d-152">а также возвращает JSON для скрипта.</span><span class="sxs-lookup"><span data-stu-id="7a49d-152">It also returns the JSON of the script.</span></span>

### <a name="parameters"></a><span data-ttu-id="7a49d-153">Параметры</span><span class="sxs-lookup"><span data-stu-id="7a49d-153">Parameters</span></span>

|<span data-ttu-id="7a49d-154">Параметр</span><span class="sxs-lookup"><span data-stu-id="7a49d-154">Parameter</span></span>     | <span data-ttu-id="7a49d-155">Описание</span><span class="sxs-lookup"><span data-stu-id="7a49d-155">Description</span></span>  |
|--------------|--------------|
| <span data-ttu-id="7a49d-156">id</span><span class="sxs-lookup"><span data-stu-id="7a49d-156">id</span></span>    | <span data-ttu-id="7a49d-157">Идентификатор скрипта сайта, сведения о котором требуется получить.</span><span class="sxs-lookup"><span data-stu-id="7a49d-157">The ID of the site script to get information about.</span></span> |

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.GetSiteScriptMetadata",
{id:"07702c07-0485-426f-b710-4704241caad9"});
```

<span data-ttu-id="7a49d-158">Ниже приведен пример возвращаемой JSON после вызова команды **GetSiteScriptMetadata**.</span><span class="sxs-lookup"><span data-stu-id="7a49d-158">Here is an example of the JSON returned after calling **GetSiteScriptMetadata**.</span></span>

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

## <a name="updatesitescript"></a><span data-ttu-id="7a49d-159">UpdateSiteScript</span><span class="sxs-lookup"><span data-stu-id="7a49d-159">UpdateSiteScript</span></span>

<span data-ttu-id="7a49d-160">Обновляет скрипт сайта.</span><span class="sxs-lookup"><span data-stu-id="7a49d-160">Updates a site script with new values.</span></span> <span data-ttu-id="7a49d-161">В вызове REST единственным обязательным параметром является идентификатор скрипта сайта.</span><span class="sxs-lookup"><span data-stu-id="7a49d-161">In the REST call all parameters are optional except the site script Id.</span></span>

### <a name="parameters"></a><span data-ttu-id="7a49d-162">Параметры</span><span class="sxs-lookup"><span data-stu-id="7a49d-162">Parameters</span></span>

|<span data-ttu-id="7a49d-163">Параметр</span><span class="sxs-lookup"><span data-stu-id="7a49d-163">Parameter</span></span>   | <span data-ttu-id="7a49d-164">Описание</span><span class="sxs-lookup"><span data-stu-id="7a49d-164">Description</span></span>  |
|------------|--------------|
| <span data-ttu-id="7a49d-165">Id</span><span class="sxs-lookup"><span data-stu-id="7a49d-165">Id</span></span>         | <span data-ttu-id="7a49d-166">Идентификатор скрипта сайта, который требуется обновить.</span><span class="sxs-lookup"><span data-stu-id="7a49d-166">The ID of the site script to update.</span></span> |
|<span data-ttu-id="7a49d-167">Название</span><span class="sxs-lookup"><span data-stu-id="7a49d-167">Title</span></span>       | <span data-ttu-id="7a49d-168">(Необязательный.) Новое отображаемое имя скрипта сайта.</span><span class="sxs-lookup"><span data-stu-id="7a49d-168">(optional) The new display name of the site script.</span></span> |
|<span data-ttu-id="7a49d-169">Description</span><span class="sxs-lookup"><span data-stu-id="7a49d-169">Description</span></span> | <span data-ttu-id="7a49d-170">(Необязательный.) Новое описание скрипта сайта.</span><span class="sxs-lookup"><span data-stu-id="7a49d-170">(Optional) The new description of the site script.</span></span> |
| <span data-ttu-id="7a49d-171">Version</span><span class="sxs-lookup"><span data-stu-id="7a49d-171">Version</span></span>    | <span data-ttu-id="7a49d-172">(Необязательный.) Новый номер версии для скрипта сайта.</span><span class="sxs-lookup"><span data-stu-id="7a49d-172">(Optional) The new version number of the site script.</span></span> |
| <span data-ttu-id="7a49d-173">Статья</span><span class="sxs-lookup"><span data-stu-id="7a49d-173">Content</span></span>    | <span data-ttu-id="7a49d-174">(Необязательный.) Новый скрипт JSON, определяющий действия скрипта.</span><span class="sxs-lookup"><span data-stu-id="7a49d-174">(Optional) A new JSON script defining the script actions.</span></span> <span data-ttu-id="7a49d-175">Дополнительные сведения см. в статье [Схема JSON для макетов сайтов](site-design-json-schema.md).</span><span class="sxs-lookup"><span data-stu-id="7a49d-175">For more information, see [Site design JSON schema](site-design-json-schema.md)</span></span> |

<span data-ttu-id="7a49d-176">Ниже приведен пример обновления скрипта сайта с помощью новых значений и скрипта JSON.</span><span class="sxs-lookup"><span data-stu-id="7a49d-176">Here's an example of updating an existing site script with a new JSON script and values.</span></span>

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

<span data-ttu-id="7a49d-177">Вот пример JSON, возвращаемой после вызова команды **UpdateSiteScript**.</span><span class="sxs-lookup"><span data-stu-id="7a49d-177">Here is an example of the JSON returned after calling **UpdateSiteScript**.</span></span>

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

## <a name="deletesitescript"></a><span data-ttu-id="7a49d-178">DeleteSiteScript</span><span class="sxs-lookup"><span data-stu-id="7a49d-178">DeleteSiteScript</span></span>

<span data-ttu-id="7a49d-179">Удаляет скрипт сайта.</span><span class="sxs-lookup"><span data-stu-id="7a49d-179">Deletes a site script.</span></span>

### <a name="parameters"></a><span data-ttu-id="7a49d-180">Параметры</span><span class="sxs-lookup"><span data-stu-id="7a49d-180">Parameters</span></span>

|<span data-ttu-id="7a49d-181">Параметр</span><span class="sxs-lookup"><span data-stu-id="7a49d-181">Parameter</span></span>   | <span data-ttu-id="7a49d-182">Описание</span><span class="sxs-lookup"><span data-stu-id="7a49d-182">Description</span></span>  |
|------------|--------------|
| <span data-ttu-id="7a49d-183">id</span><span class="sxs-lookup"><span data-stu-id="7a49d-183">id</span></span>         | <span data-ttu-id="7a49d-184">Идентификатор скрипта сайта, который нужно удалить.</span><span class="sxs-lookup"><span data-stu-id="7a49d-184">The ID of the site script to delete.</span></span> |

<span data-ttu-id="7a49d-185">В примере ниже показано, как удалить скрипт сайта.</span><span class="sxs-lookup"><span data-stu-id="7a49d-185">Here's an example of deleting a site script.</span></span>

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.DeleteSiteScript", 
{id:"07702c07-0485-426f-b710-4704241caad9"});
```

## <a name="createsitedesign"></a><span data-ttu-id="7a49d-186">CreateSiteDesign</span><span class="sxs-lookup"><span data-stu-id="7a49d-186">CreateSiteDesign</span></span>

<span data-ttu-id="7a49d-187">Создает макет сайта, доступный пользователям при создании сайта на домашней странице SharePoint.</span><span class="sxs-lookup"><span data-stu-id="7a49d-187">Creates a new site design available to users when they create a new site from the SharePoint home page.</span></span>

### <a name="parameters"></a><span data-ttu-id="7a49d-188">Параметры</span><span class="sxs-lookup"><span data-stu-id="7a49d-188">Parameters</span></span>

|<span data-ttu-id="7a49d-189">Параметр</span><span class="sxs-lookup"><span data-stu-id="7a49d-189">Parameter</span></span>  | <span data-ttu-id="7a49d-190">Описание</span><span class="sxs-lookup"><span data-stu-id="7a49d-190">Description</span></span>  |
|-----------|--------------|
|<span data-ttu-id="7a49d-191">Название</span><span class="sxs-lookup"><span data-stu-id="7a49d-191">Title</span></span>                 | <span data-ttu-id="7a49d-192">Отображаемое имя макета сайта.</span><span class="sxs-lookup"><span data-stu-id="7a49d-192">The display name of the site design.</span></span> |
|<span data-ttu-id="7a49d-193">WebTemplate</span><span class="sxs-lookup"><span data-stu-id="7a49d-193">WebTemplate</span></span>           | <span data-ttu-id="7a49d-194">Указывает, к какому базовому шаблону будет добавлен макет.</span><span class="sxs-lookup"><span data-stu-id="7a49d-194">Identifies which base template to add the design to.</span></span> <span data-ttu-id="7a49d-195">Значение **64** обозначает шаблон сайта группы, а значение **68** — шаблон сайта для общения.</span><span class="sxs-lookup"><span data-stu-id="7a49d-195">Use the value **64** for the Team site template, and the value **68** for the Communication site template.</span></span> |
|<span data-ttu-id="7a49d-196">SiteScripts</span><span class="sxs-lookup"><span data-stu-id="7a49d-196">SiteScripts</span></span>           | <span data-ttu-id="7a49d-197">Массив из одного или нескольких скриптов сайта.</span><span class="sxs-lookup"><span data-stu-id="7a49d-197">An array of one or more site scripts.</span></span> <span data-ttu-id="7a49d-198">Каждый из них определяется по идентификатору.</span><span class="sxs-lookup"><span data-stu-id="7a49d-198">Each is identified by an ID.</span></span> <span data-ttu-id="7a49d-199">Скрипты будут выполняться в указанном порядке.</span><span class="sxs-lookup"><span data-stu-id="7a49d-199">The scripts will run in the order listed.</span></span> |
|<span data-ttu-id="7a49d-200">Description</span><span class="sxs-lookup"><span data-stu-id="7a49d-200">Description</span></span>         | <span data-ttu-id="7a49d-201">(Необязательный.) Отображаемое описание макета сайта.</span><span class="sxs-lookup"><span data-stu-id="7a49d-201">(Optional) The display description of site design.</span></span> |
|<span data-ttu-id="7a49d-202">PreviewImageUrl</span><span class="sxs-lookup"><span data-stu-id="7a49d-202">PreviewImageUrl</span></span>     | <span data-ttu-id="7a49d-203">(Необязательный.) URL-адрес изображения для предварительного просмотра.</span><span class="sxs-lookup"><span data-stu-id="7a49d-203">(Optional) The URL of a preview image.</span></span> <span data-ttu-id="7a49d-204">Если он не указан, в SharePoint будет использоваться стандартное изображение.</span><span class="sxs-lookup"><span data-stu-id="7a49d-204">If none is specified SharePoint will use a generic image.</span></span> |
|<span data-ttu-id="7a49d-205">PreviewImageAltText</span><span class="sxs-lookup"><span data-stu-id="7a49d-205">PreviewImageAltText</span></span> | <span data-ttu-id="7a49d-206">(Необязательный.) Замещающий текст с описанием изображения для специальных возможностей.</span><span class="sxs-lookup"><span data-stu-id="7a49d-206">(Optional) The alt text description of the image for accessibility.</span></span> |
|<span data-ttu-id="7a49d-207">IsDefault</span><span class="sxs-lookup"><span data-stu-id="7a49d-207">IsDefault</span></span>           | <span data-ttu-id="7a49d-208">(Необязательный.) Выберите значение **true**, чтобы макет сайта применялся как стандартный. В противном случае установите **false**.</span><span class="sxs-lookup"><span data-stu-id="7a49d-208">(Optional) **true** if the site design is applied as the default site design; otherwise, **false**.</span></span> <span data-ttu-id="7a49d-209">Дополнительные сведения см. в статье [Настройка стандартного макета сайта](customize-default-site-design.md)</span><span class="sxs-lookup"><span data-stu-id="7a49d-209">For more information see [Customize a default site design](customize-default-site-design.md)</span></span> |

<span data-ttu-id="7a49d-210">Ниже представлен пример создания макета сайта.</span><span class="sxs-lookup"><span data-stu-id="7a49d-210">Here's an example of creating a new site design.</span></span>

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

<span data-ttu-id="7a49d-211">Вот пример JSON, возвращаемой после вызова команды **CreateSiteDesign**.</span><span class="sxs-lookup"><span data-stu-id="7a49d-211">Here is an example of the JSON returned after calling **CreateSiteDesign**.</span></span> <span data-ttu-id="7a49d-212">В ней также содержится идентификатор нового макета сайта.</span><span class="sxs-lookup"><span data-stu-id="7a49d-212">It contains the ID of the new site design.</span></span>

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

## <a name="getsitedesigns"></a><span data-ttu-id="7a49d-213">GetSiteDesigns</span><span class="sxs-lookup"><span data-stu-id="7a49d-213">GetSiteDesigns</span></span>

<span data-ttu-id="7a49d-214">Получает список сведений об имеющихся макетах сайтов.</span><span class="sxs-lookup"><span data-stu-id="7a49d-214">Gets a list of information on existing site designs.</span></span>

### <a name="parameters"></a><span data-ttu-id="7a49d-215">Параметры</span><span class="sxs-lookup"><span data-stu-id="7a49d-215">Parameters</span></span>

<span data-ttu-id="7a49d-216">None</span><span class="sxs-lookup"><span data-stu-id="7a49d-216">None</span></span>

<span data-ttu-id="7a49d-217">Ниже приведен пример получения всех макетов сайта.</span><span class="sxs-lookup"><span data-stu-id="7a49d-217">Here's an example of getting all the site designs.</span></span>

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.GetSiteDesigns");
```

<span data-ttu-id="7a49d-218">Вот пример JSON, возвращаемой после вызова команды **GetSiteDesigns**.</span><span class="sxs-lookup"><span data-stu-id="7a49d-218">Here is an example of the JSON returned after calling **GetSiteDesigns**.</span></span>

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

## <a name="getsitedesignmetadata"></a><span data-ttu-id="7a49d-219">GetSiteDesignMetadata</span><span class="sxs-lookup"><span data-stu-id="7a49d-219">GetSiteDesignMetadata</span></span>

<span data-ttu-id="7a49d-220">Получает сведения об определенном макете сайта.</span><span class="sxs-lookup"><span data-stu-id="7a49d-220">Gets information about a specific site design.</span></span>

### <a name="parameters"></a><span data-ttu-id="7a49d-221">Параметры</span><span class="sxs-lookup"><span data-stu-id="7a49d-221">Parameters</span></span>

|<span data-ttu-id="7a49d-222">Параметр</span><span class="sxs-lookup"><span data-stu-id="7a49d-222">Parameter</span></span>   | <span data-ttu-id="7a49d-223">Описание</span><span class="sxs-lookup"><span data-stu-id="7a49d-223">Description</span></span>  |
|------------|--------------|
| <span data-ttu-id="7a49d-224">id</span><span class="sxs-lookup"><span data-stu-id="7a49d-224">id</span></span>         | <span data-ttu-id="7a49d-225">Идентификатор макета сайта, сведения о котором требуется получить.</span><span class="sxs-lookup"><span data-stu-id="7a49d-225">The ID of the site design to get information about.</span></span> |

<span data-ttu-id="7a49d-226">В примере ниже показано, как получить сведения об определенном макете сайта с помощью его идентификатора.</span><span class="sxs-lookup"><span data-stu-id="7a49d-226">Here's an example of getting information about a specific site design by ID.</span></span>

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.GetSiteDesignMetadata", 
{id:"614f9b28-3e85-4ec9-a961-5971ea086cca"});
```

<span data-ttu-id="7a49d-227">Вот пример JSON, возвращаемой после вызова команды **GetSiteDesignMetadata**.</span><span class="sxs-lookup"><span data-stu-id="7a49d-227">Here is an example of the JSON returned after calling **GetSiteDesignMetadata**.</span></span>

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

## <a name="updatesitedesign"></a><span data-ttu-id="7a49d-228">UpdateSiteDesign</span><span class="sxs-lookup"><span data-stu-id="7a49d-228">UpdateSiteDesign</span></span>

<span data-ttu-id="7a49d-229">Обновляет макет сайта.</span><span class="sxs-lookup"><span data-stu-id="7a49d-229">Updates a site design with new values.</span></span> <span data-ttu-id="7a49d-230">В вызове REST единственным обязательным параметром является идентификатор скрипта сайта. ПРИМЕЧАНИЕ. Если вы присвоили параметру IsDefault значение TRUE и хотите, чтобы это значение сохранилось, передайте этот параметр еще раз (иначе будет восстановлено значение FALSE).</span><span class="sxs-lookup"><span data-stu-id="7a49d-230">In the REST call all parameters are optional except the site script Id. NOTE: if you had previously set the IsDefault parameter to TRUE and wish it to remain true, you must pass in this parameter again (otherwise it will be reset to FALSE).</span></span> 

### <a name="parameters"></a><span data-ttu-id="7a49d-231">Параметры</span><span class="sxs-lookup"><span data-stu-id="7a49d-231">Parameters</span></span>

|<span data-ttu-id="7a49d-232">Параметр</span><span class="sxs-lookup"><span data-stu-id="7a49d-232">Parameter</span></span>  | <span data-ttu-id="7a49d-233">Описание</span><span class="sxs-lookup"><span data-stu-id="7a49d-233">Description</span></span>  |
|-----------|--------------|
|<span data-ttu-id="7a49d-234">Id</span><span class="sxs-lookup"><span data-stu-id="7a49d-234">Id</span></span>         | <span data-ttu-id="7a49d-235">Идентификатор макета сайта, который требуется обновить.</span><span class="sxs-lookup"><span data-stu-id="7a49d-235">The ID of the site design to update.</span></span> |
|<span data-ttu-id="7a49d-236">Название</span><span class="sxs-lookup"><span data-stu-id="7a49d-236">Title</span></span>                 |  <span data-ttu-id="7a49d-237">(Необязательный.) Новое отображаемое имя обновленного макета сайта.</span><span class="sxs-lookup"><span data-stu-id="7a49d-237">(optional) The new display name of the updated site design.</span></span> |
|<span data-ttu-id="7a49d-238">WebTemplate</span><span class="sxs-lookup"><span data-stu-id="7a49d-238">WebTemplate</span></span>           | <span data-ttu-id="7a49d-239">(Необязательный.) Новый шаблон для добавления макета сайта.</span><span class="sxs-lookup"><span data-stu-id="7a49d-239">(optional) The new template to add the site design to.</span></span> <span data-ttu-id="7a49d-240">Значение **64** обозначает шаблон сайта группы, а значение **68** — шаблон сайта для общения.</span><span class="sxs-lookup"><span data-stu-id="7a49d-240">Use the value **64** for the Team site template, and the value **68** for the Communication site template.</span></span> |
|<span data-ttu-id="7a49d-241">SiteScripts</span><span class="sxs-lookup"><span data-stu-id="7a49d-241">SiteScripts</span></span>           | <span data-ttu-id="7a49d-242">(Необязательный.) Новый массив из одного или нескольких скриптов сайта.</span><span class="sxs-lookup"><span data-stu-id="7a49d-242">(optional) A new array of one or more site scripts.</span></span> <span data-ttu-id="7a49d-243">Каждый из них определяется по идентификатору.</span><span class="sxs-lookup"><span data-stu-id="7a49d-243">Each is identified by an ID.</span></span> <span data-ttu-id="7a49d-244">Скрипты будут выполняться в указанном порядке.</span><span class="sxs-lookup"><span data-stu-id="7a49d-244">The scripts will run in the order listed.</span></span> |
|<span data-ttu-id="7a49d-245">Description</span><span class="sxs-lookup"><span data-stu-id="7a49d-245">Description</span></span>         | <span data-ttu-id="7a49d-246">(Необязательный.) Новое отображаемое описание обновленного макета сайта.</span><span class="sxs-lookup"><span data-stu-id="7a49d-246">(Optional) The new display description of updated site design.</span></span> |
|<span data-ttu-id="7a49d-247">PreviewImageUrl</span><span class="sxs-lookup"><span data-stu-id="7a49d-247">PreviewImageUrl</span></span>     | <span data-ttu-id="7a49d-248">(Необязательный.) Новый URL-адрес для предварительного просмотра изображения.</span><span class="sxs-lookup"><span data-stu-id="7a49d-248">(Optional) The new URL of a preview image.</span></span> |
|<span data-ttu-id="7a49d-249">PreviewImageAltText</span><span class="sxs-lookup"><span data-stu-id="7a49d-249">PreviewImageAltText</span></span> | <span data-ttu-id="7a49d-250">(Необязательный.) Новый замещающий текст с описанием изображения для специальных возможностей.</span><span class="sxs-lookup"><span data-stu-id="7a49d-250">(Optional) The new alt text description of the image for accessibility.</span></span> |
|<span data-ttu-id="7a49d-251">IsDefault</span><span class="sxs-lookup"><span data-stu-id="7a49d-251">IsDefault</span></span>           | <span data-ttu-id="7a49d-252">(Необязательный.) Выберите значение **true**, чтобы макет сайта применялся как стандартный. В противном случае установите **false**.</span><span class="sxs-lookup"><span data-stu-id="7a49d-252">(Optional) **true** if the site design is applied as the default site design; otherwise, **false**.</span></span> <span data-ttu-id="7a49d-253">Дополнительные сведения см. в статье [Настройка стандартного макета сайта](customize-default-site-design.md)</span><span class="sxs-lookup"><span data-stu-id="7a49d-253">For more information see [Customize a default site design](customize-default-site-design.md)</span></span> |

<span data-ttu-id="7a49d-254">В примере ниже обновляются все значения существующего макета сайта.</span><span class="sxs-lookup"><span data-stu-id="7a49d-254">Here's an example that updates every value on an existing site design.</span></span>

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

<span data-ttu-id="7a49d-255">Вот пример JSON, возвращаемой после вызова команды **UpdateSiteDesign**.</span><span class="sxs-lookup"><span data-stu-id="7a49d-255">Here is an example of the JSON returned after calling **UpdateSiteDesign**.</span></span>

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

## <a name="deletesitedesign"></a><span data-ttu-id="7a49d-256">DeleteSiteDesign</span><span class="sxs-lookup"><span data-stu-id="7a49d-256">DeleteSiteDesign</span></span>

<span data-ttu-id="7a49d-257">Удаляет макет сайта.</span><span class="sxs-lookup"><span data-stu-id="7a49d-257">Deletes a site design.</span></span>

### <a name="parameters"></a><span data-ttu-id="7a49d-258">Параметры</span><span class="sxs-lookup"><span data-stu-id="7a49d-258">Parameters</span></span>

|<span data-ttu-id="7a49d-259">Параметр</span><span class="sxs-lookup"><span data-stu-id="7a49d-259">Parameter</span></span>   | <span data-ttu-id="7a49d-260">Описание</span><span class="sxs-lookup"><span data-stu-id="7a49d-260">Description</span></span>  |
|------------|--------------|
| <span data-ttu-id="7a49d-261">id</span><span class="sxs-lookup"><span data-stu-id="7a49d-261">id</span></span>         | <span data-ttu-id="7a49d-262">Идентификатор макета сайта, который требуется удалить.</span><span class="sxs-lookup"><span data-stu-id="7a49d-262">The ID of the site design to delete.</span></span> |

<span data-ttu-id="7a49d-263">В примере ниже показано, как удалить макет сайта.</span><span class="sxs-lookup"><span data-stu-id="7a49d-263">Here's an example of deleting a site design.</span></span>

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.DeleteSiteDesign", 
{id:"f9e76746-5076-4bd2-bad3-e611c488fa85"});
```

## <a name="getsitedesignrights"></a><span data-ttu-id="7a49d-264">GetSiteDesignRights</span><span class="sxs-lookup"><span data-stu-id="7a49d-264">GetSiteDesignRights</span></span>

<span data-ttu-id="7a49d-265">Получает список субъектов, имеющих доступ к макету сайта.</span><span class="sxs-lookup"><span data-stu-id="7a49d-265">Gets a list of principals that have access to a site design.</span></span>


### <a name="parameters"></a><span data-ttu-id="7a49d-266">Параметры</span><span class="sxs-lookup"><span data-stu-id="7a49d-266">Parameters</span></span>

|<span data-ttu-id="7a49d-267">Параметр</span><span class="sxs-lookup"><span data-stu-id="7a49d-267">Parameter</span></span>   | <span data-ttu-id="7a49d-268">Описание</span><span class="sxs-lookup"><span data-stu-id="7a49d-268">Description</span></span>  |
|------------|--------------|
| <span data-ttu-id="7a49d-269">id</span><span class="sxs-lookup"><span data-stu-id="7a49d-269">id</span></span>         | <span data-ttu-id="7a49d-270">Идентификатор макета сайта, откуда требуется получить сведения о правах.</span><span class="sxs-lookup"><span data-stu-id="7a49d-270">The ID of the site design to get rights information from.</span></span> |

<span data-ttu-id="7a49d-271">Ниже приведен пример получения сведений о правах на просмотр для определенного макета сайта.</span><span class="sxs-lookup"><span data-stu-id="7a49d-271">Here's an example of getting view rights for a specific site design.</span></span>

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.GetSiteDesignRights", 
{id:"dc076f7b-6c15-4d76-8f85-948a17f5dd18"});
```

<span data-ttu-id="7a49d-272">Вот пример JSON, возвращаемой после вызова команды **GetSiteDesignRights**.</span><span class="sxs-lookup"><span data-stu-id="7a49d-272">Here is an example of the JSON returned after calling **GetSiteDesignRights**.</span></span>

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

## <a name="grantsitedesignrights"></a><span data-ttu-id="7a49d-273">GrantSiteDesignRights</span><span class="sxs-lookup"><span data-stu-id="7a49d-273">GrantSiteDesignRights</span></span>

<span data-ttu-id="7a49d-274">Предоставляет доступ к макету сайта для одного или нескольких субъектов.</span><span class="sxs-lookup"><span data-stu-id="7a49d-274">Grants access to a site design for one or more principals.</span></span>

### <a name="parameters"></a><span data-ttu-id="7a49d-275">Параметры</span><span class="sxs-lookup"><span data-stu-id="7a49d-275">Parameters</span></span>

|<span data-ttu-id="7a49d-276">Параметр</span><span class="sxs-lookup"><span data-stu-id="7a49d-276">Parameter</span></span>   | <span data-ttu-id="7a49d-277">Описание</span><span class="sxs-lookup"><span data-stu-id="7a49d-277">Description</span></span>  |
|------------|--------------|
| <span data-ttu-id="7a49d-278">id</span><span class="sxs-lookup"><span data-stu-id="7a49d-278">id</span></span>         | <span data-ttu-id="7a49d-279">Идентификатор макета сайта, которому необходимо предоставить права.</span><span class="sxs-lookup"><span data-stu-id="7a49d-279">The ID of the site design to grant rights on.</span></span> |
| <span data-ttu-id="7a49d-280">principalNames</span><span class="sxs-lookup"><span data-stu-id="7a49d-280">principalNames</span></span> | <span data-ttu-id="7a49d-281">Массив из одного или нескольких субъектов, которым необходимо предоставить права на просмотр.</span><span class="sxs-lookup"><span data-stu-id="7a49d-281">An array of one or more principals to grant view rights.</span></span> <span data-ttu-id="7a49d-282">Субъектами могут быть пользователи или группы безопасности, поддерживающие почту, в формате "псевдоним" или "псевдоним@\<*доменное имя*\>.com"</span><span class="sxs-lookup"><span data-stu-id="7a49d-282">Principals can be users or mail-enabled security groups in the form of "alias" or "alias@\<*domain name*\>.com"</span></span> |
| <span data-ttu-id="7a49d-283">grantedRights</span><span class="sxs-lookup"><span data-stu-id="7a49d-283">grantedRights</span></span> | <span data-ttu-id="7a49d-284">Всегда задавайте значение **1**,</span><span class="sxs-lookup"><span data-stu-id="7a49d-284">Always set to **1**.</span></span> <span data-ttu-id="7a49d-285">соответствующее праву **Просмотр**.</span><span class="sxs-lookup"><span data-stu-id="7a49d-285">This represents the **View** right.</span></span> |

<span data-ttu-id="7a49d-286">В примере ниже показано, как предоставить права на просмотр макету сайта для пользователей Nestor и Patti (вымышленные пользователи в корпорации Contoso.)</span><span class="sxs-lookup"><span data-stu-id="7a49d-286">Here's an example of granting view rights to a site design for Nestor and Patti (fictional users at Contoso.)</span></span>

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.GrantSiteDesignRights", {
  "id": "dc076f7b-6c15-4d76-8f85-948a17f5dd18",
  "principalNames": [ "NestorW@contoso.onmicrosoft.com", "PattiF@contoso.onmicrosoft.com" ],
  "grantedRights": 1
});
```

## <a name="revokesitedesignrights"></a><span data-ttu-id="7a49d-287">RevokeSiteDesignRights</span><span class="sxs-lookup"><span data-stu-id="7a49d-287">RevokeSiteDesignRights</span></span>

<span data-ttu-id="7a49d-288">Отзывает доступ к макету сайта для одного или нескольких субъектов.</span><span class="sxs-lookup"><span data-stu-id="7a49d-288">Revokes access from a site design for one or more principals.</span></span>

### <a name="parameters"></a><span data-ttu-id="7a49d-289">Параметры</span><span class="sxs-lookup"><span data-stu-id="7a49d-289">Parameters</span></span>

|<span data-ttu-id="7a49d-290">Параметр</span><span class="sxs-lookup"><span data-stu-id="7a49d-290">Parameter</span></span>   | <span data-ttu-id="7a49d-291">Описание</span><span class="sxs-lookup"><span data-stu-id="7a49d-291">Description</span></span>  |
|------------|--------------|
| <span data-ttu-id="7a49d-292">id</span><span class="sxs-lookup"><span data-stu-id="7a49d-292">id</span></span>         | <span data-ttu-id="7a49d-293">Идентификатор макета сайта, у которого требуется отозвать права.</span><span class="sxs-lookup"><span data-stu-id="7a49d-293">The ID of the site design to revoke rights from.</span></span> |
| <span data-ttu-id="7a49d-294">principalNames</span><span class="sxs-lookup"><span data-stu-id="7a49d-294">principalNames</span></span> | <span data-ttu-id="7a49d-295">Массив из одного или нескольких субъектов, для которых необходимо отозвать права.</span><span class="sxs-lookup"><span data-stu-id="7a49d-295">An array of one or more principals to revoke view rights from.</span></span> <span data-ttu-id="7a49d-296">Если права на макет сайта отозваны для всех субъектов, макет сайта становится видимым для всех.</span><span class="sxs-lookup"><span data-stu-id="7a49d-296">If all principals have rights revoked on the site design, the site design becomes viewable to everyone.</span></span> |

<span data-ttu-id="7a49d-297">В примере ниже показано, как у макета сайта отзываются права на просмотр для пользователя Patti (вымышленного пользователя в корпорации Contoso).</span><span class="sxs-lookup"><span data-stu-id="7a49d-297">Here's an example of revoking view rights from a site design for Patti (fictional user at Contoso.)</span></span>

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.RevokeSiteDesignRights", 
{id:"5d4756e9-e1f5-42f7-afa7-5fa5aac170aa",
 principalNames:["debrab@Contoso.sharepoint.com"] });
```
