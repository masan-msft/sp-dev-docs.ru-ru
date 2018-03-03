---
title: "Создание сайта SharePoint для общения с помощью REST"
description: "Создайте современный сайт SharePoint для общения и получите его состояние, используя интерфейс REST."
ms.date: 02/08/2018
ms.prod: sharepoint
ms.openlocfilehash: c691bdf6a6dcdc3402eabb9b9ce198d630b23704
ms.sourcegitcommit: e157d51378190ddfed6394ba154ce66141c8ca33
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/19/2018
---
# <a name="create-sharepoint-communication-site-using-rest"></a><span data-ttu-id="8354b-103">Создание сайта SharePoint для общения с помощью REST</span><span class="sxs-lookup"><span data-stu-id="8354b-103">Create SharePoint Communication site using REST</span></span>

<span data-ttu-id="8354b-104">В этой статье предполагается, что вы уже ознакомились со следующими статьями:</span><span class="sxs-lookup"><span data-stu-id="8354b-104">This topic assumes that you are already familiar with the following topics:</span></span>

- [<span data-ttu-id="8354b-105">Знакомство со службой REST в SharePoint</span><span class="sxs-lookup"><span data-stu-id="8354b-105">Get to know the SharePoint REST service</span></span>](../sp-add-ins/get-to-know-the-sharepoint-rest-service.md)
- [<span data-ttu-id="8354b-106">Выполнение базовых операций с использованием конечных точек REST SharePoint</span><span class="sxs-lookup"><span data-stu-id="8354b-106">Complete basic operations using SharePoint REST endpoints</span></span>](../sp-add-ins/complete-basic-operations-using-sharepoint-rest-endpoints.md)

<span data-ttu-id="8354b-107">В этой статье нет фрагментов кода.</span><span class="sxs-lookup"><span data-stu-id="8354b-107">It does not provide code snippets.</span></span>

<span data-ttu-id="8354b-108">Ниже перечислены команды REST для создания современного сайта SharePoint для общения.</span><span class="sxs-lookup"><span data-stu-id="8354b-108">The following REST commands are available for creating a modern SharePoint Communication site.</span></span>

- <span data-ttu-id="8354b-109">**Create**.</span><span class="sxs-lookup"><span data-stu-id="8354b-109">**Create**</span></span> <span data-ttu-id="8354b-110">Создание сайта SharePoint для общения.</span><span class="sxs-lookup"><span data-stu-id="8354b-110">Create - Create a new SharePoint Communication site</span></span>
- <span data-ttu-id="8354b-111">**Status**.</span><span class="sxs-lookup"><span data-stu-id="8354b-111">status</span></span> <span data-ttu-id="8354b-112">Получение состояния сайта SharePoint для общения.</span><span class="sxs-lookup"><span data-stu-id="8354b-112">Status - Get the status of a SharePoint Communication site</span></span>

<span data-ttu-id="8354b-113">URL-адрес для команд службы REST на сайте для общения основан на конечной точке `_api/sitepages/communicationsite`.</span><span class="sxs-lookup"><span data-stu-id="8354b-113">The URL for communication site REST commands is based on `_api/sitepages/communicationsite`.</span></span> <span data-ttu-id="8354b-114">Например, для указанных выше команд REST используются следующие конечные точки:</span><span class="sxs-lookup"><span data-stu-id="8354b-114">For example, these are the endpoints for the commands listed above:</span></span>

- `http:///_api/sitepages/communicationsite/create`
- `http:///_api/sitepages/communicationsite/status`

## <a name="create-communication-site"></a><span data-ttu-id="8354b-115">Создание сайта для общения</span><span class="sxs-lookup"><span data-stu-id="8354b-115">Create Communication Site</span></span>

```
url: /_api/sitepages/communicationsite/create
method: POST
body:
{
   "request":{
      "__metadata":{
         "type":"SP.Publishing.CommunicationSiteCreationRequest"
      },
      "AllowFileSharingForGuestUsers":false,
      "Classification":"LBI",
      "Description":"Description",
      "SiteDesignId":"6142d2a0-63a5-4ba0-aede-d9fefca2c767",
      "Title":"Comm Site 1",
      "Url":"https://vesku.sharepoint.com/sites/commsite132",
      "lcid":1033
   }
}
```

> [!IMPORTANT]
> <span data-ttu-id="8354b-116">Параметр `lcid` в данный момент не поддерживается для этого API.</span><span class="sxs-lookup"><span data-stu-id="8354b-116">lcid parameter is not currently supported with this API.</span></span> <span data-ttu-id="8354b-117">В настоящее время можно создавать сайты только на английском языке.</span><span class="sxs-lookup"><span data-stu-id="8354b-117">You can currently only create English sites.</span></span> 

<span data-ttu-id="8354b-118">В этом API появилось понятие `SiteDesignID`.</span><span class="sxs-lookup"><span data-stu-id="8354b-118">New in this API is the concept of SiteDesignID.</span></span> <span data-ttu-id="8354b-119">Как и поток создания сайтов в продукте, параметр `SiteDesignID` сопоставляется с включенными вариантами оформления сайтов.</span><span class="sxs-lookup"><span data-stu-id="8354b-119">Much like the in-product site creation flow, the SiteDesignID parameter maps to the included site designs.</span></span> <span data-ttu-id="8354b-120">Они указаны ниже.</span><span class="sxs-lookup"><span data-stu-id="8354b-120">They are:</span></span>

- <span data-ttu-id="8354b-121">Тема: null</span><span class="sxs-lookup"><span data-stu-id="8354b-121">Topic: null</span></span>
- <span data-ttu-id="8354b-122">Демонстрация: 6142d2a0-63a5-4ba0-aede-d9fefca2c767</span><span class="sxs-lookup"><span data-stu-id="8354b-122">Showcase: 6142d2a0-63a5-4ba0-aede-d9fefca2c767</span></span>
- <span data-ttu-id="8354b-123">Пустой: f6cc5403-0d63-442e-96c0-285923709ffc</span><span class="sxs-lookup"><span data-stu-id="8354b-123">Blank: f6cc5403-0d63-442e-96c0-285923709ffc</span></span>

### <a name="response"></a><span data-ttu-id="8354b-124">Ответ</span><span class="sxs-lookup"><span data-stu-id="8354b-124">Response</span></span>

<span data-ttu-id="8354b-125">В случае успешного выполнения этот метод возвращает код ответа `200, OK` и простой объект JSON в тексте ответа с указанными ниже сведениями.</span><span class="sxs-lookup"><span data-stu-id="8354b-125">If successful, this method returns 200, OK response code and simple JSON object in the response body with following details.</span></span>

```
{
  "d":{
      "Create":{
           "__metadata":{"type":"SP.Publishing.CommunicationSiteCreationResponse"},
          "SiteStatus":2,
          "SiteUrl":"https://contoso.sharepoint.com/sites/comm1"
      }
  }
}
```


## <a name="get-communication-site-status"></a><span data-ttu-id="8354b-126">Получение состояния сайта для общения</span><span class="sxs-lookup"><span data-stu-id="8354b-126">Get Communication Site Status</span></span>

<span data-ttu-id="8354b-127">REST API для получения состояния современного сайта SharePoint для общения:</span><span class="sxs-lookup"><span data-stu-id="8354b-127">REST API for getting the status of a modern SharePoint Communication site</span></span>

```
url: /_api/sitepages/communicationsite/status?url='https%3A%2F%2Fcontoso.sharepoint.com%2Fsites%2Fcomm1'
method: GET
body: none
```

### <a name="response"></a><span data-ttu-id="8354b-128">Ответ</span><span class="sxs-lookup"><span data-stu-id="8354b-128">Response</span></span>

<span data-ttu-id="8354b-129">В случае успешного выполнения этот метод возвращает код ответа `200, OK` и простой объект JSON в тексте ответа с указанными ниже сведениями.</span><span class="sxs-lookup"><span data-stu-id="8354b-129">If successful, this method returns 200, OK response code and simple JSON object in the response body with following details.</span></span>
 
<span data-ttu-id="8354b-130">Если сайт существует, ответ содержит состояние и URL-адрес сайта.</span><span class="sxs-lookup"><span data-stu-id="8354b-130">If the site exists, the response will return the site status and site URL.</span></span>

```
{
  "d":{
      "Status":{
           "__metadata":{"type":"SP.Publishing.CommunicationSiteCreationResponse"},
          "SiteStatus":2,
          "SiteUrl":"https://contoso.sharepoint.com/sites/comm1"
      }
  }
}
```

<span data-ttu-id="8354b-131">Если сайт не существует, ответ содержит состояние сайта 0 без URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="8354b-131">If the site does not exist, the response will return site status of 0 with no URL.</span></span>

```
{
  "d":{
      "Status":{
           "__metadata":{"type":"SP.Publishing.CommunicationSiteCreationResponse"},
          "SiteStatus":0,
          "SiteUrl":
      }
  }
}
```

## <a name="see-also"></a><span data-ttu-id="8354b-132">См. также</span><span class="sxs-lookup"><span data-stu-id="8354b-132">See also</span></span>

- [<span data-ttu-id="8354b-133">Знакомство со службой REST в SharePoint</span><span class="sxs-lookup"><span data-stu-id="8354b-133">Get to know the SharePoint REST service</span></span>](../sp-add-ins/get-to-know-the-sharepoint-rest-service.md)