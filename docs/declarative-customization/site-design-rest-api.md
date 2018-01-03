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
# <a name="site-design-and-site-script-rest-api"></a><span data-ttu-id="56819-103">REST API для работы с макетами и скриптами сайтов</span><span class="sxs-lookup"><span data-stu-id="56819-103">Site design and site script REST API</span></span>

> [!NOTE]
> <span data-ttu-id="56819-104">Макеты и скрипты сайтов в настоящий момент пересматриваются и могут быть изменены.</span><span class="sxs-lookup"><span data-stu-id="56819-104">Site designs and site scripts are currently in preview and are subject to change.</span></span> <span data-ttu-id="56819-105">Сейчас они не поддерживаются для использования в рабочих средах.</span><span class="sxs-lookup"><span data-stu-id="56819-105">They are currently not supported for use in production environments.</span></span>

<span data-ttu-id="56819-106">При помощи интерфейса REST для SharePoint можно выполнять операции CRUD (создание, чтение, обновление и удаление) с макетами и скриптами сайтов.</span><span class="sxs-lookup"><span data-stu-id="56819-106">You can use the the SharePoint REST interface to perform basic create, read, update, and delete (CRUD) operations on site themes.</span></span>

<span data-ttu-id="56819-107">Служба REST в SharePoint Online (а также локальной среде SharePoint 2016 или более поздней версии) поддерживает объединение нескольких запросов в один вызов службы с помощью параметра запроса OData $batch.</span><span class="sxs-lookup"><span data-stu-id="56819-107">The SharePoint Online (and SharePoint 2016 and later on-premises) REST service supports combining multiple requests into a single call to the service by using the OData $batch query option.</span></span> <span data-ttu-id="56819-108">Подробные сведения и ссылки на примеры кода см. в статье [Отправка пакетных запросов с помощью интерфейсов REST API]((https://dev.office.com/sharepoint/docs/apis/rest/make-batch-requests-with-the-rest-apis.md)).</span><span class="sxs-lookup"><span data-stu-id="56819-108">For details and links to code samples, see [Make batch requests with the REST APIs]((https://dev.office.com/sharepoint/docs/apis/rest/make-batch-requests-with-the-rest-apis.md)).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="56819-109">Необходимые условия</span><span class="sxs-lookup"><span data-stu-id="56819-109">Prerequisites</span></span>
<span data-ttu-id="56819-110">Прежде чем приступить к работе, убедитесь, что вы знакомы с понятиями, описанными в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="56819-110">Before you get started, make sure that you're familiar with the following:</span></span>
- <span data-ttu-id="56819-111">[Знакомство со службой REST в SharePoint]((https://dev.office.com/sharepoint/docs/apis/rest/get-to-know-the-sharepoint-rest-service.md));</span><span class="sxs-lookup"><span data-stu-id="56819-111">[Get to know the SharePoint REST service]((https://dev.office.com/sharepoint/docs/apis/rest/get-to-know-the-sharepoint-rest-service.md))</span></span> 
- <span data-ttu-id="56819-112">[Выполнение базовых операций с использованием конечных точек REST SharePoint]((https://dev.office.com/sharepoint/docs/apis/rest/complete-basic-operations-using-sharepoint-rest-endpoints.md))</span><span class="sxs-lookup"><span data-stu-id="56819-112">[Complete basic operations using SharePoint REST endpoints]((https://dev.office.com/sharepoint/docs/apis/rest/complete-basic-operations-using-sharepoint-rest-endpoints.md))</span></span>

## <a name="rest-commands"></a><span data-ttu-id="56819-113">Команды REST</span><span class="sxs-lookup"><span data-stu-id="56819-113">REST commands</span></span>

<span data-ttu-id="56819-114">Для работы с макетами и скриптами сайтов доступны следующие команды REST:</span><span class="sxs-lookup"><span data-stu-id="56819-114">The following REST commands are available for working with site themes:</span></span>

- <span data-ttu-id="56819-115">**CreateSiteScript** &mdash; создание скрипта сайта.</span><span class="sxs-lookup"><span data-stu-id="56819-115">**CreateSiteScript** &mdash; Create a new site script.</span></span>
- <span data-ttu-id="56819-116">**GetSiteScripts** &mdash; получение списка сведений об имеющихся скриптах сайтов.</span><span class="sxs-lookup"><span data-stu-id="56819-116">**GetSiteScripts** &mdash; Get a list of information on existing site scripts.</span></span>
- <span data-ttu-id="56819-117">**GetSiteScriptMetadata** &mdash; получение сведений об определенном скрипте сайта.</span><span class="sxs-lookup"><span data-stu-id="56819-117">**GetSiteScriptMetadata** &mdash; Get information about a specific site script.</span></span>
- <span data-ttu-id="56819-118">**UpdateSiteScript** &mdash; обновление скрипта сайта с использованием новых значений.</span><span class="sxs-lookup"><span data-stu-id="56819-118">**UpdateSiteScript** &mdash; Update a site script with new values.</span></span>
- <span data-ttu-id="56819-119">**DeleteSiteScript** &mdash; удаление скрипта сайта.</span><span class="sxs-lookup"><span data-stu-id="56819-119">**DeleteSiteScript** &mdash; Delete a site script.</span></span>
- <span data-ttu-id="56819-120">**CreateSiteDesign** &mdash; создание макета сайта.</span><span class="sxs-lookup"><span data-stu-id="56819-120">**CreateSiteDesign** &mdash; Create a site design.</span></span>
- <span data-ttu-id="56819-121">**GetSiteDesigns** &mdash; получение списка сведений об имеющихся макетах сайтов.</span><span class="sxs-lookup"><span data-stu-id="56819-121">**GetSiteDesigns** &mdash; Get a list of information on existing site designs.</span></span>
- <span data-ttu-id="56819-122">**GetSiteDesignMetadata** &mdash; получение сведений об определенном макете сайта.</span><span class="sxs-lookup"><span data-stu-id="56819-122">**GetSiteDesignMetadata** &mdash; Get information about a sepcific site design.</span></span>
- <span data-ttu-id="56819-123">**UpdateSiteDesign** &mdash; обновление макета сайта с использованием новых значений.</span><span class="sxs-lookup"><span data-stu-id="56819-123">**UpdateSiteDesign** &mdash; Update a site design with new values.</span></span>
- <span data-ttu-id="56819-124">**DeleteSiteDesign** &mdash; удаление макета сайта.</span><span class="sxs-lookup"><span data-stu-id="56819-124">**DeleteSiteDesign** &mdash; Delete a site design.</span></span>
- <span data-ttu-id="56819-125">**GetSiteDesignRights** &mdash; получение списка субъектов, имеющих доступ к макету сайта.</span><span class="sxs-lookup"><span data-stu-id="56819-125">**GetSiteDesignRights** &mdash; Get a list of principals that have access to a site design.</span></span>
- <span data-ttu-id="56819-126">**GrantSiteDesignRights** &mdash; предоставление доступа к макету сайта для одного или нескольких субъектов.</span><span class="sxs-lookup"><span data-stu-id="56819-126">**GrantSiteDesignRights** &mdash; Grant access to a site design for one or more principals.</span></span>
- <span data-ttu-id="56819-127">**RevokeSiteDesignRights** &mdash; отзыв доступа к макету сайта для одного или нескольких субъектов.</span><span class="sxs-lookup"><span data-stu-id="56819-127">**RevokeSiteDesignRights** &mdash; Revoke access from a site design for one or more principals.</span></span>

## <a name="create-a-function-to-send-rest-requests"></a><span data-ttu-id="56819-128">Создание функции для отправки запросов REST</span><span class="sxs-lookup"><span data-stu-id="56819-128">Create a function to send REST requests</span></span>

<span data-ttu-id="56819-129">Чтобы работать с REST API, рекомендуем создать вспомогательную функцию для отправки вызовов REST.</span><span class="sxs-lookup"><span data-stu-id="56819-129">To work with the REST API we recommend creating a helper function to make the REST calls.</span></span> <span data-ttu-id="56819-130">Приведенная ниже функция **RestRequest** вызывает метод REST, указанный в параметре **url**, и передает дополнительные параметры из аргумента **params**.</span><span class="sxs-lookup"><span data-stu-id="56819-130">The following **RestRequest** function will call the REST method specified in the **url** parameter and pass the additional parameters in **params**.</span></span>

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

## <a name="createsitescript"></a><span data-ttu-id="56819-131">CreateSiteScript</span><span class="sxs-lookup"><span data-stu-id="56819-131">CreateSiteScript</span></span>

<span data-ttu-id="56819-132">Создает макет сайта, доступный пользователям при создании сайта на домашней странице SharePoint.</span><span class="sxs-lookup"><span data-stu-id="56819-132">Creates a new site design available to users when they create a new site from the SharePoint home page.</span></span>

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.CreateSiteScript(Title=@title)?@title='TITLE'", VARIABLE);
```

## <a name="getsitescripts"></a><span data-ttu-id="56819-133">GetSiteScripts</span><span class="sxs-lookup"><span data-stu-id="56819-133">GetSiteScripts</span></span>

<span data-ttu-id="56819-134">Получает список сведений об имеющихся скриптах сайтов.</span><span class="sxs-lookup"><span data-stu-id="56819-134">Gets a list of information on existing site scripts.</span></span>

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.GetSiteScripts");
```

## <a name="getsitescriptmetadata"></a><span data-ttu-id="56819-135">GetSiteScriptMetadata</span><span class="sxs-lookup"><span data-stu-id="56819-135">GetSiteScriptMetadata</span></span>

<span data-ttu-id="56819-136">Получает сведения об определенном скрипте сайта.</span><span class="sxs-lookup"><span data-stu-id="56819-136">Gets information about a specific site script.</span></span>

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.GetSiteScriptMetadata", {id:"<ID>"});
```

## <a name="updatesitescript"></a><span data-ttu-id="56819-137">UpdateSiteScript</span><span class="sxs-lookup"><span data-stu-id="56819-137">UpdateSiteScript</span></span>

<span data-ttu-id="56819-138">Обновляет скрипт сайта с использованием новых значений.</span><span class="sxs-lookup"><span data-stu-id="56819-138">Updates a site script with new values.</span></span>

```javascript
VAR = site script content

RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.UpdateSiteScript", {updateInfo:{Id:"<siteScriptID>", Title:"<updated title>", Description:"<updated description>", Version: 2, Content: JSON.stringify(<VAR>)}});
```

## <a name="deletesitescript"></a><span data-ttu-id="56819-139">DeleteSiteScript</span><span class="sxs-lookup"><span data-stu-id="56819-139">DeleteSiteScript</span></span>

<span data-ttu-id="56819-140">Удаляет скрипт сайта.</span><span class="sxs-lookup"><span data-stu-id="56819-140">Deletes a site script.</span></span>

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.DeleteSiteScript", {id:"<ID>"});
```

## <a name="createsitedesign"></a><span data-ttu-id="56819-141">CreateSiteDesign</span><span class="sxs-lookup"><span data-stu-id="56819-141">CreateSiteDesign</span></span>

<span data-ttu-id="56819-142">Создает макет сайта.</span><span class="sxs-lookup"><span data-stu-id="56819-142">Create a design package</span></span>

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.CreateSiteDesign", {info:{Title:"<title>", Description:"<description>", SiteScriptIds:["NNN"],  WebTemplate:"<64 | 68>", IsDefault: <false | true>}});
```

## <a name="getsitedesigns"></a><span data-ttu-id="56819-143">GetSiteDesigns</span><span class="sxs-lookup"><span data-stu-id="56819-143">GetSiteDesigns</span></span>

<span data-ttu-id="56819-144">Получает список сведений об имеющихся макетах сайтов.</span><span class="sxs-lookup"><span data-stu-id="56819-144">Get a list of information on existing site designs.</span></span>

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.GetSiteDesigns");
```

## <a name="getsitedesignmetadata"></a><span data-ttu-id="56819-145">GetSiteDesignMetadata</span><span class="sxs-lookup"><span data-stu-id="56819-145">GetSiteDesignMetadata</span></span>

<span data-ttu-id="56819-146">Получает сведения об определенном макете сайта.</span><span class="sxs-lookup"><span data-stu-id="56819-146">Get information about a specific site design.</span></span>

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.GetSiteDesignMetadata", {id:"<ID>"});
```

## <a name="updatesitedesign"></a><span data-ttu-id="56819-147">UpdateSiteDesign</span><span class="sxs-lookup"><span data-stu-id="56819-147">UpdateSiteDesign</span></span>

<span data-ttu-id="56819-148">Обновляет макет сайта с использованием новых значений.</span><span class="sxs-lookup"><span data-stu-id="56819-148">Update a resource with new values.</span></span>

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.UpdateSiteDesign", {updateInfo:{Id:"<siteDesignID>", Title:"<updated site design title>", Description:"<updated site design description>", SiteScriptIds:["<ID>"], PreviewImageUrl:"<url to image asset for site design preview image>",PreviewImageAltText:"<alt text for preview image>" WebTemplate:"68", Version: 7, IsDefault: false}});
```

## <a name="deletesitedesign"></a><span data-ttu-id="56819-149">DeleteSiteDesign</span><span class="sxs-lookup"><span data-stu-id="56819-149">DeleteSiteDesign</span></span>

<span data-ttu-id="56819-150">Удаляет макет сайта.</span><span class="sxs-lookup"><span data-stu-id="56819-150">Delete a site design.</span></span>

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.DeleteSiteDesign", {id:"<ID>"});
```

## <a name="getsitedesignrights"></a><span data-ttu-id="56819-151">GetSiteDesignRights</span><span class="sxs-lookup"><span data-stu-id="56819-151">GetSiteDesignRights</span></span>

<span data-ttu-id="56819-152">Получает список субъектов, имеющих доступ к макету сайта.</span><span class="sxs-lookup"><span data-stu-id="56819-152">Get a list of principals that have access to a site design.</span></span>

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.GetSiteDesignRights", {id:"<ID>"});
```

## <a name="grantsitedesignrights"></a><span data-ttu-id="56819-153">GrantSiteDesignRights</span><span class="sxs-lookup"><span data-stu-id="56819-153">GrantSiteDesignRights</span></span>

<span data-ttu-id="56819-154">Предоставляет доступ к макету сайта для одного или нескольких субъектов.</span><span class="sxs-lookup"><span data-stu-id="56819-154">Grant access to a site design for one or more principals.</span></span>

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.GrantSiteDesignRights", {id:"<ID>", principalNames:["alias", “alias@domain.com”], grantedRights:1});
```

## <a name="revokesitedesignrights"></a><span data-ttu-id="56819-155">RevokeSiteDesignRights</span><span class="sxs-lookup"><span data-stu-id="56819-155">RevokeSiteDesignRights</span></span>

<span data-ttu-id="56819-156">Отзывает доступ к макету сайта для одного или нескольких субъектов.</span><span class="sxs-lookup"><span data-stu-id="56819-156">Revoke access from a site design for one or more principals.</span></span>

```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.RevokeSiteDesignRights", {id:"5d4756e9-e1f5-42f7-afa7-5fa5aac170aa", principalNames:["debrab@Contoso.sharepoint.com"] });
```
