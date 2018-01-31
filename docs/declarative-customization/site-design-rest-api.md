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
# <a name="site-design-and-site-script-rest-api"></a><span data-ttu-id="32941-103">REST API для работы с макетами и скриптами сайтов</span><span class="sxs-lookup"><span data-stu-id="32941-103">Site design and site script REST API</span></span>

> [!NOTE]
> <span data-ttu-id="32941-104">Макеты и скрипты сайтов находятся на стадии тестирования и могут меняться.</span><span class="sxs-lookup"><span data-stu-id="32941-104">Site designs and site scripts are currently in preview and are subject to change.</span></span> <span data-ttu-id="32941-105">В настоящее время в рабочих средах их можно использовать только в выпуске Targeted.</span><span class="sxs-lookup"><span data-stu-id="32941-105">They are currently only supported for use in production environments in Targeted Release.</span></span>

<span data-ttu-id="32941-106">При помощи интерфейса REST для SharePoint можно выполнять операции CRUD (создание, чтение, обновление и удаление) с макетами и скриптами сайтов.</span><span class="sxs-lookup"><span data-stu-id="32941-106">You can use the the SharePoint REST interface to perform basic create, read, update, and delete (CRUD) operations on site designs and site scripts.</span></span>

<span data-ttu-id="32941-107">Служба REST в SharePoint Online (а также локальной среде SharePoint 2016 или более поздней версии) поддерживает объединение нескольких запросов в один вызов службы с помощью параметра запроса OData $batch.</span><span class="sxs-lookup"><span data-stu-id="32941-107">The SharePoint Online (and SharePoint 2016 and later on-premises) REST service supports combining multiple requests into a single call to the service by using the OData $batch query option.</span></span> <span data-ttu-id="32941-108">Подробные сведения и ссылки на примеры кода см. в статье [Отправка пакетных запросов с помощью интерфейсов REST API](https://dev.office.com/sharepoint/docs/apis/rest/make-batch-requests-with-the-rest-apis.md).</span><span class="sxs-lookup"><span data-stu-id="32941-108">For details and links to code samples, see [Make batch requests with the REST APIs](https://dev.office.com/sharepoint/docs/apis/rest/make-batch-requests-with-the-rest-apis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="32941-109">Необходимые условия</span><span class="sxs-lookup"><span data-stu-id="32941-109">Prerequisites</span></span>
<span data-ttu-id="32941-110">Прежде чем приступить к работе, убедитесь, что вы знакомы с понятиями, описанными в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="32941-110">Before you get started, make sure that you're familiar with the following:</span></span>
- <span data-ttu-id="32941-111">[Знакомство со службой REST в SharePoint](https://dev.office.com/sharepoint/docs/apis/rest/get-to-know-the-sharepoint-rest-service.md);</span><span class="sxs-lookup"><span data-stu-id="32941-111">[Get to know the SharePoint REST service](https://dev.office.com/sharepoint/docs/apis/rest/get-to-know-the-sharepoint-rest-service.md)</span></span> 
- [<span data-ttu-id="32941-112">Выполнение базовых операций с использованием конечных точек REST SharePoint</span><span class="sxs-lookup"><span data-stu-id="32941-112">Complete basic operations using SharePoint REST endpoints</span></span>](https://dev.office.com/sharepoint/docs/apis/rest/complete-basic-operations-using-sharepoint-rest-endpoints.md)

## <a name="rest-commands"></a><span data-ttu-id="32941-113">Команды REST</span><span class="sxs-lookup"><span data-stu-id="32941-113">REST commands</span></span>

<span data-ttu-id="32941-114">Для работы с макетами и скриптами сайтов доступны следующие команды REST:</span><span class="sxs-lookup"><span data-stu-id="32941-114">The following REST commands are available for working with site designs and site scripts:</span></span>

- <span data-ttu-id="32941-115">**CreateSiteScript** &mdash; создание скрипта сайта.</span><span class="sxs-lookup"><span data-stu-id="32941-115">**CreateSiteScript** &mdash; Creates a new site script.</span></span>
- <span data-ttu-id="32941-116">**GetSiteScripts** &mdash; получение списка сведений об имеющихся скриптах сайтов.</span><span class="sxs-lookup"><span data-stu-id="32941-116">**GetSiteScripts** &mdash; Gets a list of information on existing site scripts.</span></span>
- <span data-ttu-id="32941-117">**GetSiteScriptMetadata** &mdash; получение сведений об определенном скрипте сайта.</span><span class="sxs-lookup"><span data-stu-id="32941-117">**GetSiteScriptMetadata** &mdash; Gets information about a specific site script.</span></span>
- <span data-ttu-id="32941-118">**UpdateSiteScript** &mdash; обновление скрипта сайта с использованием новых значений.</span><span class="sxs-lookup"><span data-stu-id="32941-118">**UpdateSiteScript** &mdash; Updates a site script with new values.</span></span>
- <span data-ttu-id="32941-119">**DeleteSiteScript** &mdash; удаление скрипта сайта.</span><span class="sxs-lookup"><span data-stu-id="32941-119">**DeleteSiteScript** &mdash; Deletes a site script.</span></span>
- <span data-ttu-id="32941-120">**CreateSiteDesign** &mdash; создание макета сайта.</span><span class="sxs-lookup"><span data-stu-id="32941-120">**CreateSiteDesign** &mdash; Creates a site design.</span></span>
- <span data-ttu-id="32941-121">**GetSiteDesigns** &mdash; получение списка сведений об имеющихся макетах сайтов.</span><span class="sxs-lookup"><span data-stu-id="32941-121">**GetSiteDesigns** &mdash; Gets a list of information on existing site designs.</span></span>
- <span data-ttu-id="32941-122">**GetSiteDesignMetadata** &mdash; получение сведений об определенном макете сайта.</span><span class="sxs-lookup"><span data-stu-id="32941-122">**GetSiteDesignMetadata** &mdash; Gets information about a sepcific site design.</span></span>
- <span data-ttu-id="32941-123">**UpdateSiteDesign** &mdash; обновление макета сайта с использованием новых значений.</span><span class="sxs-lookup"><span data-stu-id="32941-123">**UpdateSiteDesign** &mdash; Updates a site design with new values.</span></span>
- <span data-ttu-id="32941-124">**DeleteSiteDesign** &mdash; удаление макета сайта.</span><span class="sxs-lookup"><span data-stu-id="32941-124">**DeleteSiteDesign** &mdash; Deletes a site design.</span></span>
- <span data-ttu-id="32941-125">**GetSiteDesignRights** &mdash; получение списка субъектов, имеющих доступ к макету сайта.</span><span class="sxs-lookup"><span data-stu-id="32941-125">**GetSiteDesignRights** &mdash; Gets a list of principals that have access to a site design.</span></span>
- <span data-ttu-id="32941-126">**GrantSiteDesignRights** &mdash; предоставление доступа к макету сайта для одного или нескольких субъектов.</span><span class="sxs-lookup"><span data-stu-id="32941-126">**GrantSiteDesignRights** &mdash; Grants access to a site design for one or more principals.</span></span>
- <span data-ttu-id="32941-127">**RevokeSiteDesignRights** &mdash; отзыв доступа к макету сайта для одного или нескольких субъектов.</span><span class="sxs-lookup"><span data-stu-id="32941-127">**RevokeSiteDesignRights** &mdash; Revokes access from a site design for one or more principals.</span></span>

## <a name="create-a-function-to-send-rest-requests"></a><span data-ttu-id="32941-128">Создание функции для отправки запросов REST</span><span class="sxs-lookup"><span data-stu-id="32941-128">Create a function to send REST requests</span></span>

<span data-ttu-id="32941-129">Чтобы работать с REST API, рекомендуем создать вспомогательную функцию для отправки вызовов REST.</span><span class="sxs-lookup"><span data-stu-id="32941-129">To work with the REST API we recommend creating a helper function to make the REST calls.</span></span> <span data-ttu-id="32941-130">Приведенная ниже функция **RestRequest** вызывает метод REST, указанный в параметре **url**, и передает дополнительные параметры из аргумента **params**.</span><span class="sxs-lookup"><span data-stu-id="32941-130">The following **RestRequest** function will call the REST method specified in the **url** parameter and pass the additional parameters in **params**.</span></span>

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

## <a name="createsitescript"></a><span data-ttu-id="32941-131">CreateSiteScript</span><span class="sxs-lookup"><span data-stu-id="32941-131">CreateSiteScript</span></span>

<span data-ttu-id="32941-132">Создает скрипт сайта.</span><span class="sxs-lookup"><span data-stu-id="32941-132">Creates a new site script.</span></span>

### <a name="parameters"></a><span data-ttu-id="32941-133">Параметры</span><span class="sxs-lookup"><span data-stu-id="32941-133">Parameters</span></span>

|<span data-ttu-id="32941-134">Параметр</span><span class="sxs-lookup"><span data-stu-id="32941-134">Parameter</span></span>     | <span data-ttu-id="32941-135">Описание</span><span class="sxs-lookup"><span data-stu-id="32941-135">Description</span></span>  |
|--------------|--------------|
| <span data-ttu-id="32941-136">Название</span><span class="sxs-lookup"><span data-stu-id="32941-136">Title</span></span>       | <span data-ttu-id="32941-137">Отображаемое имя макета сайта.</span><span class="sxs-lookup"><span data-stu-id="32941-137">The display name of the site design.</span></span> |
| <span data-ttu-id="32941-138">Статья</span><span class="sxs-lookup"><span data-stu-id="32941-138">Content</span></span>     | <span data-ttu-id="32941-139">Значение JSON, описывающее скрипт.</span><span class="sxs-lookup"><span data-stu-id="32941-139">JSON value that describes the script.</span></span> <span data-ttu-id="32941-140">Дополнительные сведения см. в [справочнике по JSON](site-design-json-schema.md).</span><span class="sxs-lookup"><span data-stu-id="32941-140">For more information, see [JSON reference](site-design-json-schema.md).</span></span>|

<span data-ttu-id="32941-141">В примере ниже создается скрипт сайта, где применяется настраиваемая тема.</span><span class="sxs-lookup"><span data-stu-id="32941-141">The following example creates a new site script that applies a custom theme.</span></span>

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

<span data-ttu-id="32941-142">В этом примере после вызова команды **CreateSiteScript** возвращается нотация объектов JavaScript (JSON),</span><span class="sxs-lookup"><span data-stu-id="32941-142">Here is an example of the JSON returned after calling **CreateSiteScript**.</span></span> <span data-ttu-id="32941-143">содержащая идентификатор нового скрипта сайта.</span><span class="sxs-lookup"><span data-stu-id="32941-143">It contains the ID of the new site script.</span></span>

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

## <a name="getsitescripts"></a><span data-ttu-id="32941-144">GetSiteScripts</span><span class="sxs-lookup"><span data-stu-id="32941-144">GetSiteScripts</span></span>

<span data-ttu-id="32941-145">Получает список сведений обо всех имеющихся скриптах сайтов.</span><span class="sxs-lookup"><span data-stu-id="32941-145">Gets a list of information on all existing site scripts.</span></span>

### <a name="parameters"></a><span data-ttu-id="32941-146">Параметры</span><span class="sxs-lookup"><span data-stu-id="32941-146">Parameters</span></span>

<span data-ttu-id="32941-147">Нет.</span><span class="sxs-lookup"><span data-stu-id="32941-147">None.</span></span>

<span data-ttu-id="32941-148">В приведенном ниже примере показано, как получить информацию о скрипте сайта для всех скриптов.</span><span class="sxs-lookup"><span data-stu-id="32941-148">The following example gets the site script information for all site scripts.</span></span>

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.GetSiteScripts");
```

<span data-ttu-id="32941-149">В этом примере JSON возвращается после вызова команды **GetSiteScripts**.</span><span class="sxs-lookup"><span data-stu-id="32941-149">Here is an example of the JSON returned after calling **GetSiteScripts**.</span></span>

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

## <a name="getsitescriptmetadata"></a><span data-ttu-id="32941-150">GetSiteScriptMetadata</span><span class="sxs-lookup"><span data-stu-id="32941-150">GetSiteScriptMetadata</span></span>

<span data-ttu-id="32941-151">Получает сведения об определенном скрипте сайта,</span><span class="sxs-lookup"><span data-stu-id="32941-151">Gets information about a specific site script.</span></span> <span data-ttu-id="32941-152">а также возвращает JSON для скрипта.</span><span class="sxs-lookup"><span data-stu-id="32941-152">It also returns the JSON of the script.</span></span>

### <a name="parameters"></a><span data-ttu-id="32941-153">Параметры</span><span class="sxs-lookup"><span data-stu-id="32941-153">Parameters</span></span>

|<span data-ttu-id="32941-154">Параметр</span><span class="sxs-lookup"><span data-stu-id="32941-154">Parameter</span></span>     | <span data-ttu-id="32941-155">Описание</span><span class="sxs-lookup"><span data-stu-id="32941-155">Description</span></span>  |
|--------------|--------------|
| <span data-ttu-id="32941-156">id</span><span class="sxs-lookup"><span data-stu-id="32941-156">id</span></span>    | <span data-ttu-id="32941-157">Идентификатор скрипта сайта, сведения о котором требуется получить.</span><span class="sxs-lookup"><span data-stu-id="32941-157">The ID of the site script to get information about.</span></span> |

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.GetSiteScriptMetadata",
{id:"07702c07-0485-426f-b710-4704241caad9"});
```

<span data-ttu-id="32941-158">Ниже приведен пример возвращаемой JSON после вызова команды **GetSiteScriptMetadata**.</span><span class="sxs-lookup"><span data-stu-id="32941-158">Here is an example of the JSON returned after calling **GetSiteScriptMetadata**.</span></span>

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

## <a name="updatesitescript"></a><span data-ttu-id="32941-159">UpdateSiteScript</span><span class="sxs-lookup"><span data-stu-id="32941-159">UpdateSiteScript</span></span>

<span data-ttu-id="32941-160">Обновляет скрипт сайта с использованием новых значений.</span><span class="sxs-lookup"><span data-stu-id="32941-160">Updates a site script with new values.</span></span>

### <a name="parameters"></a><span data-ttu-id="32941-161">Параметры</span><span class="sxs-lookup"><span data-stu-id="32941-161">Parameters</span></span>

|<span data-ttu-id="32941-162">Параметр</span><span class="sxs-lookup"><span data-stu-id="32941-162">Parameter</span></span>   | <span data-ttu-id="32941-163">Описание</span><span class="sxs-lookup"><span data-stu-id="32941-163">Description</span></span>  |
|------------|--------------|
| <span data-ttu-id="32941-164">Id</span><span class="sxs-lookup"><span data-stu-id="32941-164">Id</span></span>         | <span data-ttu-id="32941-165">Идентификатор скрипта сайта, который требуется обновить.</span><span class="sxs-lookup"><span data-stu-id="32941-165">The ID of the site script to update.</span></span> |
|<span data-ttu-id="32941-166">Название</span><span class="sxs-lookup"><span data-stu-id="32941-166">Title</span></span>       | <span data-ttu-id="32941-167">(Необязательный.) Новое отображаемое имя скрипта сайта.</span><span class="sxs-lookup"><span data-stu-id="32941-167">(optional) The new display name of the site script.</span></span> |
|<span data-ttu-id="32941-168">Description</span><span class="sxs-lookup"><span data-stu-id="32941-168">Description</span></span> | <span data-ttu-id="32941-169">(Необязательный.) Новое описание скрипта сайта.</span><span class="sxs-lookup"><span data-stu-id="32941-169">(Optional) The new description of the site script.</span></span> |
| <span data-ttu-id="32941-170">Version</span><span class="sxs-lookup"><span data-stu-id="32941-170">Version</span></span>    | <span data-ttu-id="32941-171">(Необязательный.) Новый номер версии для скрипта сайта.</span><span class="sxs-lookup"><span data-stu-id="32941-171">(Optional) The new version number of the site script.</span></span> |
| <span data-ttu-id="32941-172">Статья</span><span class="sxs-lookup"><span data-stu-id="32941-172">Content</span></span>    | <span data-ttu-id="32941-173">(Необязательный.) Новый скрипт JSON, определяющий действия скрипта.</span><span class="sxs-lookup"><span data-stu-id="32941-173">(Optional) A new JSON script defining the script actions.</span></span> <span data-ttu-id="32941-174">Дополнительные сведения см. в статье [Схема JSON для макетов сайтов](site-design-json-schema.md).</span><span class="sxs-lookup"><span data-stu-id="32941-174">For more information, see [Site design JSON schema](site-design-json-schema.md)</span></span> |

<span data-ttu-id="32941-175">Ниже приведен пример обновления скрипта сайта с помощью новых значений и скрипта JSON.</span><span class="sxs-lookup"><span data-stu-id="32941-175">Here's an example of updating an existing site script with a new JSON script and values.</span></span>

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

<span data-ttu-id="32941-176">Вот пример JSON, возвращаемой после вызова команды **UpdateSiteScript**.</span><span class="sxs-lookup"><span data-stu-id="32941-176">Here is an example of the JSON returned after calling **UpdateSiteScript**.</span></span>

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

## <a name="deletesitescript"></a><span data-ttu-id="32941-177">DeleteSiteScript</span><span class="sxs-lookup"><span data-stu-id="32941-177">DeleteSiteScript</span></span>

<span data-ttu-id="32941-178">Удаляет скрипт сайта.</span><span class="sxs-lookup"><span data-stu-id="32941-178">Deletes a site script.</span></span>

### <a name="parameters"></a><span data-ttu-id="32941-179">Параметры</span><span class="sxs-lookup"><span data-stu-id="32941-179">Parameters</span></span>

|<span data-ttu-id="32941-180">Параметр</span><span class="sxs-lookup"><span data-stu-id="32941-180">Parameter</span></span>   | <span data-ttu-id="32941-181">Описание</span><span class="sxs-lookup"><span data-stu-id="32941-181">Description</span></span>  |
|------------|--------------|
| <span data-ttu-id="32941-182">id</span><span class="sxs-lookup"><span data-stu-id="32941-182">id</span></span>         | <span data-ttu-id="32941-183">Идентификатор скрипта сайта, который нужно удалить.</span><span class="sxs-lookup"><span data-stu-id="32941-183">The ID of the site script to delete.</span></span> |

<span data-ttu-id="32941-184">В примере ниже показано, как удалить скрипт сайта.</span><span class="sxs-lookup"><span data-stu-id="32941-184">Here's an example of deleting a site script.</span></span>

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.DeleteSiteScript", 
{id:"07702c07-0485-426f-b710-4704241caad9"});
```

## <a name="createsitedesign"></a><span data-ttu-id="32941-185">CreateSiteDesign</span><span class="sxs-lookup"><span data-stu-id="32941-185">CreateSiteDesign</span></span>

<span data-ttu-id="32941-186">Создает макет сайта, доступный пользователям при создании сайта на домашней странице SharePoint.</span><span class="sxs-lookup"><span data-stu-id="32941-186">Creates a new site design available to users when they create a new site from the SharePoint home page.</span></span>

### <a name="parameters"></a><span data-ttu-id="32941-187">Параметры</span><span class="sxs-lookup"><span data-stu-id="32941-187">Parameters</span></span>

|<span data-ttu-id="32941-188">Параметр</span><span class="sxs-lookup"><span data-stu-id="32941-188">Parameter</span></span>  | <span data-ttu-id="32941-189">Описание</span><span class="sxs-lookup"><span data-stu-id="32941-189">Description</span></span>  |
|-----------|--------------|
|<span data-ttu-id="32941-190">Название</span><span class="sxs-lookup"><span data-stu-id="32941-190">Title</span></span>                 | <span data-ttu-id="32941-191">Отображаемое имя макета сайта.</span><span class="sxs-lookup"><span data-stu-id="32941-191">The display name of the site design.</span></span> |
|<span data-ttu-id="32941-192">WebTemplate</span><span class="sxs-lookup"><span data-stu-id="32941-192">WebTemplate</span></span>           | <span data-ttu-id="32941-193">Указывает, к какому базовому шаблону будет добавлен макет.</span><span class="sxs-lookup"><span data-stu-id="32941-193">Identifies which base template to add the design to.</span></span> <span data-ttu-id="32941-194">Значение **64** обозначает шаблон сайта группы, а значение **68** — шаблон сайта для общения.</span><span class="sxs-lookup"><span data-stu-id="32941-194">Use the value **64** for the Team site template, and the value **68** for the Communication site template.</span></span> |
|<span data-ttu-id="32941-195">SiteScripts</span><span class="sxs-lookup"><span data-stu-id="32941-195">SiteScripts</span></span>           | <span data-ttu-id="32941-196">Массив из одного или нескольких скриптов сайта.</span><span class="sxs-lookup"><span data-stu-id="32941-196">An array of one or more site scripts.</span></span> <span data-ttu-id="32941-197">Каждый из них определяется по идентификатору.</span><span class="sxs-lookup"><span data-stu-id="32941-197">Each is identified by an ID.</span></span> <span data-ttu-id="32941-198">Скрипты будут выполняться в указанном порядке.</span><span class="sxs-lookup"><span data-stu-id="32941-198">The scripts will run in the order listed.</span></span> |
|<span data-ttu-id="32941-199">Description</span><span class="sxs-lookup"><span data-stu-id="32941-199">Description</span></span>         | <span data-ttu-id="32941-200">(Необязательный.) Отображаемое описание макета сайта.</span><span class="sxs-lookup"><span data-stu-id="32941-200">(Optional) The display description of site design.</span></span> |
|<span data-ttu-id="32941-201">PreviewImageUrl</span><span class="sxs-lookup"><span data-stu-id="32941-201">PreviewImageUrl</span></span>     | <span data-ttu-id="32941-202">(Необязательный.) URL-адрес изображения для предварительного просмотра.</span><span class="sxs-lookup"><span data-stu-id="32941-202">(Optional) The URL of a preview image.</span></span> <span data-ttu-id="32941-203">Если он не указан, в SharePoint будет использоваться стандартное изображение.</span><span class="sxs-lookup"><span data-stu-id="32941-203">If none is specified SharePoint will use a generic image.</span></span> |
|<span data-ttu-id="32941-204">PreviewImageAltText</span><span class="sxs-lookup"><span data-stu-id="32941-204">PreviewImageAltText</span></span> | <span data-ttu-id="32941-205">(Необязательный.) Замещающий текст с описанием изображения для специальных возможностей.</span><span class="sxs-lookup"><span data-stu-id="32941-205">(Optional) The alt text description of the image for accessibility.</span></span> |
|<span data-ttu-id="32941-206">IsDefault</span><span class="sxs-lookup"><span data-stu-id="32941-206">IsDefault</span></span>           | <span data-ttu-id="32941-207">(Необязательный.) Выберите значение **true**, чтобы макет сайта применялся как стандартный. В противном случае установите **false**.</span><span class="sxs-lookup"><span data-stu-id="32941-207">(Optional) **true** if the site design is applied as the default site design; otherwise, **false**.</span></span> <span data-ttu-id="32941-208">Дополнительные сведения см. в статье [Настройка стандартного макета сайта](customize-default-site-design.md)</span><span class="sxs-lookup"><span data-stu-id="32941-208">For more information see [Customize a default site design](customize-default-site-design.md)</span></span> |

<span data-ttu-id="32941-209">Ниже представлен пример создания макета сайта.</span><span class="sxs-lookup"><span data-stu-id="32941-209">Here's an example of creating a new site design.</span></span>

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

<span data-ttu-id="32941-210">Вот пример JSON, возвращаемой после вызова команды **CreateSiteDesign**.</span><span class="sxs-lookup"><span data-stu-id="32941-210">Here is an example of the JSON returned after calling **CreateSiteDesign**.</span></span> <span data-ttu-id="32941-211">В ней также содержится идентификатор нового макета сайта.</span><span class="sxs-lookup"><span data-stu-id="32941-211">It contains the ID of the new site design.</span></span>

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

## <a name="getsitedesigns"></a><span data-ttu-id="32941-212">GetSiteDesigns</span><span class="sxs-lookup"><span data-stu-id="32941-212">GetSiteDesigns</span></span>

<span data-ttu-id="32941-213">Получает список сведений об имеющихся макетах сайтов.</span><span class="sxs-lookup"><span data-stu-id="32941-213">Gets a list of information on existing site designs.</span></span>

### <a name="parameters"></a><span data-ttu-id="32941-214">Параметры</span><span class="sxs-lookup"><span data-stu-id="32941-214">Parameters</span></span>

<span data-ttu-id="32941-215">None</span><span class="sxs-lookup"><span data-stu-id="32941-215">None</span></span>

<span data-ttu-id="32941-216">Ниже приведен пример получения всех макетов сайта.</span><span class="sxs-lookup"><span data-stu-id="32941-216">Here's an example of getting all the site designs.</span></span>

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.GetSiteDesigns");
```

<span data-ttu-id="32941-217">Вот пример JSON, возвращаемой после вызова команды **GetSiteDesigns**.</span><span class="sxs-lookup"><span data-stu-id="32941-217">Here is an example of the JSON returned after calling **GetSiteDesigns**.</span></span>

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

## <a name="getsitedesignmetadata"></a><span data-ttu-id="32941-218">GetSiteDesignMetadata</span><span class="sxs-lookup"><span data-stu-id="32941-218">GetSiteDesignMetadata</span></span>

<span data-ttu-id="32941-219">Получает сведения об определенном макете сайта.</span><span class="sxs-lookup"><span data-stu-id="32941-219">Gets information about a specific site design.</span></span>

### <a name="parameters"></a><span data-ttu-id="32941-220">Параметры</span><span class="sxs-lookup"><span data-stu-id="32941-220">Parameters</span></span>

|<span data-ttu-id="32941-221">Параметр</span><span class="sxs-lookup"><span data-stu-id="32941-221">Parameter</span></span>   | <span data-ttu-id="32941-222">Описание</span><span class="sxs-lookup"><span data-stu-id="32941-222">Description</span></span>  |
|------------|--------------|
| <span data-ttu-id="32941-223">id</span><span class="sxs-lookup"><span data-stu-id="32941-223">id</span></span>         | <span data-ttu-id="32941-224">Идентификатор макета сайта, сведения о котором требуется получить.</span><span class="sxs-lookup"><span data-stu-id="32941-224">The ID of the site design to get information about.</span></span> |

<span data-ttu-id="32941-225">В примере ниже показано, как получить сведения об определенном макете сайта с помощью его идентификатора.</span><span class="sxs-lookup"><span data-stu-id="32941-225">Here's an example of getting information about a specific site design by ID.</span></span>

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.GetSiteDesignMetadata", 
{id:"614f9b28-3e85-4ec9-a961-5971ea086cca"});
```

<span data-ttu-id="32941-226">Вот пример JSON, возвращаемой после вызова команды **GetSiteDesignMetadata**.</span><span class="sxs-lookup"><span data-stu-id="32941-226">Here is an example of the JSON returned after calling **GetSiteDesignMetadata**.</span></span>

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

## <a name="updatesitedesign"></a><span data-ttu-id="32941-227">UpdateSiteDesign</span><span class="sxs-lookup"><span data-stu-id="32941-227">UpdateSiteDesign</span></span>

<span data-ttu-id="32941-228">Обновляет макет сайта с использованием новых значений.</span><span class="sxs-lookup"><span data-stu-id="32941-228">Updates a site design with new values.</span></span>

### <a name="parameters"></a><span data-ttu-id="32941-229">Параметры</span><span class="sxs-lookup"><span data-stu-id="32941-229">Parameters</span></span>

|<span data-ttu-id="32941-230">Параметр</span><span class="sxs-lookup"><span data-stu-id="32941-230">Parameter</span></span>  | <span data-ttu-id="32941-231">Описание</span><span class="sxs-lookup"><span data-stu-id="32941-231">Description</span></span>  |
|-----------|--------------|
|<span data-ttu-id="32941-232">Id</span><span class="sxs-lookup"><span data-stu-id="32941-232">Id</span></span>         | <span data-ttu-id="32941-233">Идентификатор макета сайта, который требуется обновить.</span><span class="sxs-lookup"><span data-stu-id="32941-233">The ID of the site design to update.</span></span> |
|<span data-ttu-id="32941-234">Название</span><span class="sxs-lookup"><span data-stu-id="32941-234">Title</span></span>                 |  <span data-ttu-id="32941-235">(Необязательный.) Новое отображаемое имя обновленного макета сайта.</span><span class="sxs-lookup"><span data-stu-id="32941-235">(optional) The new display name of the updated site design.</span></span> |
|<span data-ttu-id="32941-236">WebTemplate</span><span class="sxs-lookup"><span data-stu-id="32941-236">WebTemplate</span></span>           | <span data-ttu-id="32941-237">(Необязательный.) Новый шаблон для добавления макета сайта.</span><span class="sxs-lookup"><span data-stu-id="32941-237">(optional) The new template to add the site design to.</span></span> <span data-ttu-id="32941-238">Значение **64** обозначает шаблон сайта группы, а значение **68** — шаблон сайта для общения.</span><span class="sxs-lookup"><span data-stu-id="32941-238">Use the value **64** for the Team site template, and the value **68** for the Communication site template.</span></span> |
|<span data-ttu-id="32941-239">SiteScripts</span><span class="sxs-lookup"><span data-stu-id="32941-239">SiteScripts</span></span>           | <span data-ttu-id="32941-240">(Необязательный.) Новый массив из одного или нескольких скриптов сайта.</span><span class="sxs-lookup"><span data-stu-id="32941-240">(optional) A new array of one or more site scripts.</span></span> <span data-ttu-id="32941-241">Каждый из них определяется по идентификатору.</span><span class="sxs-lookup"><span data-stu-id="32941-241">Each is identified by an ID.</span></span> <span data-ttu-id="32941-242">Скрипты будут выполняться в указанном порядке.</span><span class="sxs-lookup"><span data-stu-id="32941-242">The scripts will run in the order listed.</span></span> |
|<span data-ttu-id="32941-243">Description</span><span class="sxs-lookup"><span data-stu-id="32941-243">Description</span></span>         | <span data-ttu-id="32941-244">(Необязательный.) Новое отображаемое описание обновленного макета сайта.</span><span class="sxs-lookup"><span data-stu-id="32941-244">(Optional) The new display description of updated site design.</span></span> |
|<span data-ttu-id="32941-245">PreviewImageUrl</span><span class="sxs-lookup"><span data-stu-id="32941-245">PreviewImageUrl</span></span>     | <span data-ttu-id="32941-246">(Необязательный.) Новый URL-адрес для предварительного просмотра изображения.</span><span class="sxs-lookup"><span data-stu-id="32941-246">(Optional) The new URL of a preview image.</span></span> |
|<span data-ttu-id="32941-247">PreviewImageAltText</span><span class="sxs-lookup"><span data-stu-id="32941-247">PreviewImageAltText</span></span> | <span data-ttu-id="32941-248">(Необязательный.) Новый замещающий текст с описанием изображения для специальных возможностей.</span><span class="sxs-lookup"><span data-stu-id="32941-248">(Optional) The new alt text description of the image for accessibility.</span></span> |
|<span data-ttu-id="32941-249">IsDefault</span><span class="sxs-lookup"><span data-stu-id="32941-249">IsDefault</span></span>           | <span data-ttu-id="32941-250">(Необязательный.) Выберите значение **true**, чтобы макет сайта применялся как стандартный. В противном случае установите **false**.</span><span class="sxs-lookup"><span data-stu-id="32941-250">(Optional) **true** if the site design is applied as the default site design; otherwise, **false**.</span></span> <span data-ttu-id="32941-251">Дополнительные сведения см. в статье [Настройка стандартного макета сайта](customize-default-site-design.md)</span><span class="sxs-lookup"><span data-stu-id="32941-251">For more information see [Customize a default site design](customize-default-site-design.md)</span></span> |

<span data-ttu-id="32941-252">В примере ниже обновляются все значения существующего макета сайта.</span><span class="sxs-lookup"><span data-stu-id="32941-252">Here's an example that updates every value on an existing site design.</span></span>

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

<span data-ttu-id="32941-253">Вот пример JSON, возвращаемой после вызова команды **UpdateSiteDesign**.</span><span class="sxs-lookup"><span data-stu-id="32941-253">Here is an example of the JSON returned after calling **UpdateSiteDesign**.</span></span>

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

## <a name="deletesitedesign"></a><span data-ttu-id="32941-254">DeleteSiteDesign</span><span class="sxs-lookup"><span data-stu-id="32941-254">DeleteSiteDesign</span></span>

<span data-ttu-id="32941-255">Удаляет макет сайта.</span><span class="sxs-lookup"><span data-stu-id="32941-255">Deletes a site design.</span></span>

### <a name="parameters"></a><span data-ttu-id="32941-256">Параметры</span><span class="sxs-lookup"><span data-stu-id="32941-256">Parameters</span></span>

|<span data-ttu-id="32941-257">Параметр</span><span class="sxs-lookup"><span data-stu-id="32941-257">Parameter</span></span>   | <span data-ttu-id="32941-258">Описание</span><span class="sxs-lookup"><span data-stu-id="32941-258">Description</span></span>  |
|------------|--------------|
| <span data-ttu-id="32941-259">id</span><span class="sxs-lookup"><span data-stu-id="32941-259">id</span></span>         | <span data-ttu-id="32941-260">Идентификатор макета сайта, который требуется удалить.</span><span class="sxs-lookup"><span data-stu-id="32941-260">The ID of the site design to delete.</span></span> |

<span data-ttu-id="32941-261">В примере ниже показано, как удалить макет сайта.</span><span class="sxs-lookup"><span data-stu-id="32941-261">Here's an example of deleting a site design.</span></span>

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.DeleteSiteDesign", 
{id:"f9e76746-5076-4bd2-bad3-e611c488fa85"});
```

## <a name="getsitedesignrights"></a><span data-ttu-id="32941-262">GetSiteDesignRights</span><span class="sxs-lookup"><span data-stu-id="32941-262">GetSiteDesignRights</span></span>

<span data-ttu-id="32941-263">Получает список субъектов, имеющих доступ к макету сайта.</span><span class="sxs-lookup"><span data-stu-id="32941-263">Gets a list of principals that have access to a site design.</span></span>


### <a name="parameters"></a><span data-ttu-id="32941-264">Параметры</span><span class="sxs-lookup"><span data-stu-id="32941-264">Parameters</span></span>

|<span data-ttu-id="32941-265">Параметр</span><span class="sxs-lookup"><span data-stu-id="32941-265">Parameter</span></span>   | <span data-ttu-id="32941-266">Описание</span><span class="sxs-lookup"><span data-stu-id="32941-266">Description</span></span>  |
|------------|--------------|
| <span data-ttu-id="32941-267">id</span><span class="sxs-lookup"><span data-stu-id="32941-267">id</span></span>         | <span data-ttu-id="32941-268">Идентификатор макета сайта, откуда требуется получить сведения о правах.</span><span class="sxs-lookup"><span data-stu-id="32941-268">The ID of the site design to get rights information from.</span></span> |

<span data-ttu-id="32941-269">Ниже приведен пример получения сведений о правах на просмотр для определенного макета сайта.</span><span class="sxs-lookup"><span data-stu-id="32941-269">Here's an example of getting view rights for a specific site design.</span></span>

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.GetSiteDesignRights", 
{id:"dc076f7b-6c15-4d76-8f85-948a17f5dd18"});
```

<span data-ttu-id="32941-270">Вот пример JSON, возвращаемой после вызова команды **GetSiteDesignRights**.</span><span class="sxs-lookup"><span data-stu-id="32941-270">Here is an example of the JSON returned after calling **GetSiteDesignRights**.</span></span>

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

## <a name="grantsitedesignrights"></a><span data-ttu-id="32941-271">GrantSiteDesignRights</span><span class="sxs-lookup"><span data-stu-id="32941-271">GrantSiteDesignRights</span></span>

<span data-ttu-id="32941-272">Предоставляет доступ к макету сайта для одного или нескольких субъектов.</span><span class="sxs-lookup"><span data-stu-id="32941-272">Grants access to a site design for one or more principals.</span></span>

### <a name="parameters"></a><span data-ttu-id="32941-273">Параметры</span><span class="sxs-lookup"><span data-stu-id="32941-273">Parameters</span></span>

|<span data-ttu-id="32941-274">Параметр</span><span class="sxs-lookup"><span data-stu-id="32941-274">Parameter</span></span>   | <span data-ttu-id="32941-275">Описание</span><span class="sxs-lookup"><span data-stu-id="32941-275">Description</span></span>  |
|------------|--------------|
| <span data-ttu-id="32941-276">id</span><span class="sxs-lookup"><span data-stu-id="32941-276">id</span></span>         | <span data-ttu-id="32941-277">Идентификатор макета сайта, которому необходимо предоставить права.</span><span class="sxs-lookup"><span data-stu-id="32941-277">The ID of the site design to grant rights on.</span></span> |
| <span data-ttu-id="32941-278">principalNames</span><span class="sxs-lookup"><span data-stu-id="32941-278">principalNames</span></span> | <span data-ttu-id="32941-279">Массив из одного или нескольких субъектов, которым необходимо предоставить права на просмотр.</span><span class="sxs-lookup"><span data-stu-id="32941-279">An array of one or more principals to grant view rights.</span></span> <span data-ttu-id="32941-280">Субъектами могут быть пользователи или группы безопасности, поддерживающие почту, в формате "псевдоним" или "псевдоним@\<*доменное имя*\>.com"</span><span class="sxs-lookup"><span data-stu-id="32941-280">Principals can be users or mail-enabled security groups in the form of "alias" or "alias@\<*domain name*\>.com"</span></span> |
| <span data-ttu-id="32941-281">grantedRights</span><span class="sxs-lookup"><span data-stu-id="32941-281">grantedRights</span></span> | <span data-ttu-id="32941-282">Всегда задавайте значение **1**,</span><span class="sxs-lookup"><span data-stu-id="32941-282">Always set to **1**.</span></span> <span data-ttu-id="32941-283">соответствующее праву **Просмотр**.</span><span class="sxs-lookup"><span data-stu-id="32941-283">This represents the **View** right.</span></span> |

<span data-ttu-id="32941-284">В примере ниже показано, как предоставить права на просмотр макету сайта для пользователей Nestor и Patti (вымышленные пользователи в корпорации Contoso.)</span><span class="sxs-lookup"><span data-stu-id="32941-284">Here's an example of granting view rights to a site design for Nestor and Patti (fictional users at Contoso.)</span></span>

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.GrantSiteDesignRights", {
  "id": "dc076f7b-6c15-4d76-8f85-948a17f5dd18",
  "principalNames": [ "NestorW@contoso.onmicrosoft.com", "PattiF@contoso.onmicrosoft.com" ],
  "grantedRights": 1
});
```

## <a name="revokesitedesignrights"></a><span data-ttu-id="32941-285">RevokeSiteDesignRights</span><span class="sxs-lookup"><span data-stu-id="32941-285">RevokeSiteDesignRights</span></span>

<span data-ttu-id="32941-286">Отзывает доступ к макету сайта для одного или нескольких субъектов.</span><span class="sxs-lookup"><span data-stu-id="32941-286">Revokes access from a site design for one or more principals.</span></span>

### <a name="parameters"></a><span data-ttu-id="32941-287">Параметры</span><span class="sxs-lookup"><span data-stu-id="32941-287">Parameters</span></span>

|<span data-ttu-id="32941-288">Параметр</span><span class="sxs-lookup"><span data-stu-id="32941-288">Parameter</span></span>   | <span data-ttu-id="32941-289">Описание</span><span class="sxs-lookup"><span data-stu-id="32941-289">Description</span></span>  |
|------------|--------------|
| <span data-ttu-id="32941-290">id</span><span class="sxs-lookup"><span data-stu-id="32941-290">id</span></span>         | <span data-ttu-id="32941-291">Идентификатор макета сайта, у которого требуется отозвать права.</span><span class="sxs-lookup"><span data-stu-id="32941-291">The ID of the site design to revoke rights from.</span></span> |
| <span data-ttu-id="32941-292">principalNames</span><span class="sxs-lookup"><span data-stu-id="32941-292">principalNames</span></span> | <span data-ttu-id="32941-293">Массив из одного или нескольких субъектов, для которых необходимо отозвать права.</span><span class="sxs-lookup"><span data-stu-id="32941-293">An array of one or more principals to revoke view rights from.</span></span> <span data-ttu-id="32941-294">Если права на макет сайта отозваны для всех субъектов, макет сайта становится видимым для всех.</span><span class="sxs-lookup"><span data-stu-id="32941-294">If all principals have rights revoked on the site design, the site design becomes viewable to everyone.</span></span> |

<span data-ttu-id="32941-295">В примере ниже показано, как у макета сайта отзываются права на просмотр для пользователя Patti (вымышленного пользователя в корпорации Contoso).</span><span class="sxs-lookup"><span data-stu-id="32941-295">Here's an example of revoking view rights from a site design for Patti (fictional user at Contoso.)</span></span>

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.RevokeSiteDesignRights", 
{id:"5d4756e9-e1f5-42f7-afa7-5fa5aac170aa",
 principalNames:["debrab@Contoso.sharepoint.com"] });
```
