---
title: "Создание подписки"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 374200568aa1151e58b9ae76fc48fb2465921af7
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="create-a-new-subscription"></a><span data-ttu-id="4e03a-102">Создание подписки</span><span class="sxs-lookup"><span data-stu-id="4e03a-102">Create a new subscription</span></span> 

<span data-ttu-id="4e03a-103">Создает подписку на веб-перехватчики в списке SharePoint.</span><span class="sxs-lookup"><span data-stu-id="4e03a-103">Creates a new webhook subscription on a SharePoint list.</span></span> 

## <a name="permissions"></a><span data-ttu-id="4e03a-104">Разрешения</span><span class="sxs-lookup"><span data-stu-id="4e03a-104">Permissions</span></span>

<span data-ttu-id="4e03a-105">У приложения должно быть разрешение на изменение списка SharePoint, в котором создается подписка.</span><span class="sxs-lookup"><span data-stu-id="4e03a-105">The application must have at least edit permissions to the SharePoint list where the subscription will be created.</span></span>

<span data-ttu-id="4e03a-106">**Если приложение является приложением Microsoft Azure Active Directory (AD):**</span><span class="sxs-lookup"><span data-stu-id="4e03a-106">**If your application is a Microsoft Azure Active Directory (AD) application:**</span></span>

<span data-ttu-id="4e03a-107">Приложению Azure AD необходимо предоставить разрешения, указанные в следующей таблице:</span><span class="sxs-lookup"><span data-stu-id="4e03a-107">You must grant the Azure AD app the permissions specified in the following table:</span></span>

<span data-ttu-id="4e03a-108">Приложение</span><span class="sxs-lookup"><span data-stu-id="4e03a-108">Application</span></span> | <span data-ttu-id="4e03a-109">Разрешение</span><span class="sxs-lookup"><span data-stu-id="4e03a-109">Permission</span></span> 
------------|------------
<span data-ttu-id="4e03a-110">SharePoint Online в Office 365</span><span class="sxs-lookup"><span data-stu-id="4e03a-110">Office 365 SharePoint Online</span></span>|<span data-ttu-id="4e03a-111">Чтение и запись элементов и списков во всех семействах веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="4e03a-111">Read and write items and lists in all site collections.</span></span>

<span data-ttu-id="4e03a-112">**Если приложение является надстройкой SharePoint:**</span><span class="sxs-lookup"><span data-stu-id="4e03a-112">**If your application is a SharePoint add-in:**</span></span>

<span data-ttu-id="4e03a-113">Надстройке SharePoint необходимо предоставить по крайней мере следующие разрешения:</span><span class="sxs-lookup"><span data-stu-id="4e03a-113">You must grant the SharePoint add-in the following permission(s) or higher:</span></span>

<span data-ttu-id="4e03a-114">Область</span><span class="sxs-lookup"><span data-stu-id="4e03a-114">Scope</span></span> | <span data-ttu-id="4e03a-115">Разрешения</span><span class="sxs-lookup"><span data-stu-id="4e03a-115">Permission Rights</span></span> 
------|------------
<span data-ttu-id="4e03a-116">Список</span><span class="sxs-lookup"><span data-stu-id="4e03a-116">List</span></span>|<span data-ttu-id="4e03a-117">Управление</span><span class="sxs-lookup"><span data-stu-id="4e03a-117">Manage</span></span>

## <a name="http-request"></a><span data-ttu-id="4e03a-118">HTTP-запрос</span><span class="sxs-lookup"><span data-stu-id="4e03a-118">HTTP request</span></span>

```
POST /_api/web/lists('list-id')/subscriptions
```

## <a name="request-body"></a><span data-ttu-id="4e03a-119">Текст запроса</span><span class="sxs-lookup"><span data-stu-id="4e03a-119">Request body</span></span>

<span data-ttu-id="4e03a-120">Включите в запрос указанные ниже свойства.</span><span class="sxs-lookup"><span data-stu-id="4e03a-120">Include the following properties in the request body.</span></span>

<span data-ttu-id="4e03a-121">Имя</span><span class="sxs-lookup"><span data-stu-id="4e03a-121">Name</span></span> | <span data-ttu-id="4e03a-122">Тип</span><span class="sxs-lookup"><span data-stu-id="4e03a-122">Type</span></span> | <span data-ttu-id="4e03a-123">Описание</span><span class="sxs-lookup"><span data-stu-id="4e03a-123">Description</span></span> 
-----|------|------------
<span data-ttu-id="4e03a-124">resource</span><span class="sxs-lookup"><span data-stu-id="4e03a-124">resource</span></span>|<span data-ttu-id="4e03a-125">строка</span><span class="sxs-lookup"><span data-stu-id="4e03a-125">string</span></span>|<span data-ttu-id="4e03a-126">URL-адрес списка для получения уведомлений.</span><span class="sxs-lookup"><span data-stu-id="4e03a-126">The URL of the list to receive notifications from.</span></span>
<span data-ttu-id="4e03a-127">notificationUrl</span><span class="sxs-lookup"><span data-stu-id="4e03a-127">notificationUrl</span></span>|<span data-ttu-id="4e03a-128">строка</span><span class="sxs-lookup"><span data-stu-id="4e03a-128">string</span></span>|<span data-ttu-id="4e03a-129">URL-адрес службы для отправки уведомлений.</span><span class="sxs-lookup"><span data-stu-id="4e03a-129">The service URL to send notifications to.</span></span>
<span data-ttu-id="4e03a-130">expirationDateTime</span><span class="sxs-lookup"><span data-stu-id="4e03a-130">expirationDateTime</span></span>|<span data-ttu-id="4e03a-131">дата</span><span class="sxs-lookup"><span data-stu-id="4e03a-131">date</span></span>|<span data-ttu-id="4e03a-132">Срок хранения уведомления.</span><span class="sxs-lookup"><span data-stu-id="4e03a-132">The date the notification will expire and be deleted.</span></span>
<span data-ttu-id="4e03a-133">client-clientState</span><span class="sxs-lookup"><span data-stu-id="4e03a-133">client-clientState</span></span>|<span data-ttu-id="4e03a-134">string</span><span class="sxs-lookup"><span data-stu-id="4e03a-134">string</span></span>|<span data-ttu-id="4e03a-p101">Необязательный. Непрозрачная строка, которая передаются клиенту со всеми уведомлениями. Ее можно использовать для проверки уведомлений и маркировки различных подписок.</span><span class="sxs-lookup"><span data-stu-id="4e03a-p101">Optional. Opaque string passed back to the client on all notifications. You can use this for validating notifications, or tagging different subscriptions.</span></span>


### <a name="example"></a><span data-ttu-id="4e03a-138">Пример</span><span class="sxs-lookup"><span data-stu-id="4e03a-138">Example</span></span>

```http
POST /_api/web/lists('5C77031A-9621-4DFC-BB5D-57803A94E91D')/subscriptions
Accept: application/json
Content-Type: application/json

{
  "resource": "https://contoso.sharepoint.com/_api/web/lists('5C77031A-9621-4DFC-BB5D-57803A94E91D')",
  "notificationUrl": "https://91e383a5.ngrok.io/api/webhook/handlerequest",
  "expirationDateTime": "2016-04-27T16:17:57+00:00"
}
```

## <a name="response"></a><span data-ttu-id="4e03a-139">Ответ</span><span class="sxs-lookup"><span data-stu-id="4e03a-139">Response</span></span>

<span data-ttu-id="4e03a-140">Когда вы добавляете подписку, возвращается ответ `201 Created`, который включает новый объект подписки.</span><span class="sxs-lookup"><span data-stu-id="4e03a-140">If the subscription is added, then a `201 Created` response is returned that includes the newly created subscription object.</span></span>

### <a name="example"></a><span data-ttu-id="4e03a-141">Пример</span><span class="sxs-lookup"><span data-stu-id="4e03a-141">Example</span></span>

```http
HTTP/1.1 201 Created
Content-Type: application/json

{
    "id": "a8e6d5e6-9f7f-497a-b97f-8ffe8f559dc7",
    "expirationDateTime": "2016-04-27T16:17:57Z",    
    "notificationUrl": "https://91e383a5.ngrok.io/api/webhook/handlerequest",
    "resource": "5c77031a-9621-4dfc-bb5d-57803a94e91d"
}
```

## <a name="url-validation"></a><span data-ttu-id="4e03a-142">Проверка URL-адреса</span><span class="sxs-lookup"><span data-stu-id="4e03a-142">URL validation</span></span>

<span data-ttu-id="4e03a-p102">Перед созданием подписки SharePoint отправит запрос с токеном проверки на указанный URL-адрес службы. Служба должна ответить на него, вернув токен проверки.</span><span class="sxs-lookup"><span data-stu-id="4e03a-p102">Before a new subscription is created, SharePoint will send a request with a validation token in the body of the request to the service URL provided. Your service must respond to this request by returning the validation token.</span></span>

<span data-ttu-id="4e03a-145">В противном случае подписка не будет создана.</span><span class="sxs-lookup"><span data-stu-id="4e03a-145">If your service fails to validate the request in this way, the subscription will fail to be created.</span></span> <span data-ttu-id="4e03a-146">Дополнительные сведения см. в статье [Обзор веб-перехватчиков SharePoint](../overview-sharepoint-webhooks.md).</span><span class="sxs-lookup"><span data-stu-id="4e03a-146">See [Overview of SharePoint webhooks](../overview-sharepoint-webhooks.md) for more information.</span></span>
