# <a name="creating-sharepoint-communication-site-using-rest"></a><span data-ttu-id="82de8-101">Создание сайта SharePoint для общения с помощью REST</span><span class="sxs-lookup"><span data-stu-id="82de8-101">Creating SharePoint Communication Site using REST</span></span>

<span data-ttu-id="82de8-102">Узнайте, как создать современный сайт SharePoint для общения и получить его состояние с помощью интерфейса REST.</span><span class="sxs-lookup"><span data-stu-id="82de8-102">Learn how to create and get the status of a new modern SharePoint Communication site with the REST interface.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="82de8-103">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="82de8-103">Prerequisites</span></span>

<span data-ttu-id="82de8-104">В этой статье предполагается, что вы уже ознакомились со статьями "Знакомство со службой REST для SharePoint" и "Выполнение базовых операций с использованием конечных точек REST в SharePoint".</span><span class="sxs-lookup"><span data-stu-id="82de8-104">This topic assumes that you are already familiar with the topics  Get to know the SharePoint REST service and Complete basic operations using SharePoint REST endpoints. It does not provide code snippets.</span></span> <span data-ttu-id="82de8-105">Здесь не представлены фрагменты кода.</span><span class="sxs-lookup"><span data-stu-id="82de8-105">It does not provide code snippets.</span></span>

<span data-ttu-id="82de8-106">Ниже перечислены команды REST, доступные при создании современного сайта SharePoint для общения.</span><span class="sxs-lookup"><span data-stu-id="82de8-106">The following REST commands are available for creating a modern SharePoint Communication site.</span></span>

- <span data-ttu-id="82de8-107">**Create** — создание сайта SharePoint для общения.</span><span class="sxs-lookup"><span data-stu-id="82de8-107">**Create** - Create a new SharePoint Communication site</span></span>
- <span data-ttu-id="82de8-108">**Status** — получение состояния сайта SharePoint для общения.</span><span class="sxs-lookup"><span data-stu-id="82de8-108">**Status** - Get the status of a SharePoint Communication site</span></span>

<span data-ttu-id="82de8-109">URL-адрес для команд службы REST на сайте для общения основан на конечной точке `_api/sitepages/communicationsite`.</span><span class="sxs-lookup"><span data-stu-id="82de8-109">The URL for communication site REST commands is based on `_api/sitepages/communicationsite`.</span></span> <span data-ttu-id="82de8-110">Например, для вышеуказанных команд используются следующие конечные точки:</span><span class="sxs-lookup"><span data-stu-id="82de8-110">For example, these are the endpoints for the commands listed above:</span></span>

- `http:///_api/sitepages/communicationsite/create`
- `http:///_api/sitepages/communicationsite/status`

## <a name="create-communication-site"></a><span data-ttu-id="82de8-111">Создание сайта для общения</span><span class="sxs-lookup"><span data-stu-id="82de8-111">Create Communication Site</span></span>

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
> <span data-ttu-id="82de8-112">Параметр lcid в данный момент не поддерживается для этого API.</span><span class="sxs-lookup"><span data-stu-id="82de8-112">lcid parameter is not currently supported with this API.</span></span> <span data-ttu-id="82de8-113">В настоящее время можно создавать только сайты на английском языке.</span><span class="sxs-lookup"><span data-stu-id="82de8-113">You can currently only create English sites.</span></span> 

<span data-ttu-id="82de8-114">В этом API появилось понятие SiteDesignID.</span><span class="sxs-lookup"><span data-stu-id="82de8-114">New in this API is the concept of SiteDesignID.</span></span> <span data-ttu-id="82de8-115">Как и поток создания сайтов в продукте, параметр SiteDesignID сопоставляется с включенными вариантами оформления сайтов.</span><span class="sxs-lookup"><span data-stu-id="82de8-115">Much like the in-product site creation flow, the SiteDesignID parameter maps to the included site designs.</span></span> <span data-ttu-id="82de8-116">Они указаны ниже.</span><span class="sxs-lookup"><span data-stu-id="82de8-116">They are:</span></span>

- <span data-ttu-id="82de8-117">Тема: null</span><span class="sxs-lookup"><span data-stu-id="82de8-117">Topic: null</span></span>
- <span data-ttu-id="82de8-118">Демонстрация: 6142d2a0-63a5-4ba0-aede-d9fefca2c767</span><span class="sxs-lookup"><span data-stu-id="82de8-118">Showcase: 6142d2a0-63a5-4ba0-aede-d9fefca2c767</span></span>
- <span data-ttu-id="82de8-119">Пустой: f6cc5403-0d63-442e-96c0-285923709ffc</span><span class="sxs-lookup"><span data-stu-id="82de8-119">Blank: f6cc5403-0d63-442e-96c0-285923709ffc</span></span>

<span data-ttu-id="82de8-120">**Отклик**</span><span class="sxs-lookup"><span data-stu-id="82de8-120">**Response**</span></span>

<span data-ttu-id="82de8-121">В случае успешного выполнения этот метод возвращает код отклика 200 OK и простой объект JSON в тексте отклика с указанными ниже сведениями.</span><span class="sxs-lookup"><span data-stu-id="82de8-121">If successful, this method returns 200, OK response code and simple JSON object in the response body with following details.</span></span>

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


## <a name="get-communication-site-status"></a><span data-ttu-id="82de8-122">Получение состояния сайта для общения</span><span class="sxs-lookup"><span data-stu-id="82de8-122">Get Communication Site Status</span></span>

<span data-ttu-id="82de8-123">REST API для получения состояния современного сайта SharePoint для общения</span><span class="sxs-lookup"><span data-stu-id="82de8-123">REST API for getting the status of a modern SharePoint Communication site</span></span>

```
url: /_api/sitepages/communicationsite/status?url='https%3A%2F%2Fcontoso.sharepoint.com%2Fsites%2Fcomm1'
method: GET
body: none
```

<span data-ttu-id="82de8-124">**Отклик**</span><span class="sxs-lookup"><span data-stu-id="82de8-124">**Response**</span></span>

<span data-ttu-id="82de8-125">В случае успешного выполнения этот метод возвращает код отклика 200 OK и простой объект JSON в тексте отклика с указанными ниже сведениями.</span><span class="sxs-lookup"><span data-stu-id="82de8-125">If successful, this method returns 200, OK response code and simple JSON object in the response body with following details.</span></span>
 
<span data-ttu-id="82de8-126">Если сайт существует, отклик содержит состояние и URL-адрес сайта.</span><span class="sxs-lookup"><span data-stu-id="82de8-126">If the site exists, the response will return the site status and site URL.</span></span>

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

<span data-ttu-id="82de8-127">Если сайт не существует, отклик содержит состояние сайта 0 без URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="82de8-127">If the site does not exist, the response will return site status of 0 with no URL.</span></span>

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