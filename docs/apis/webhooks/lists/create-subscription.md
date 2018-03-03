---
title: "Создание подписки"
description: "Создает подписку на веб-перехватчики в списке SharePoint."
ms.date: 02/08/2018
ms.prod: sharepoint
ms.openlocfilehash: 8a93bdd5c7891ac275e18c1c9f50620c44b760af
ms.sourcegitcommit: e157d51378190ddfed6394ba154ce66141c8ca33
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/19/2018
---
# <a name="create-a-new-subscription"></a><span data-ttu-id="2d011-103">Создание подписки</span><span class="sxs-lookup"><span data-stu-id="2d011-103">Create a new subscription</span></span> 

<span data-ttu-id="2d011-104">Создает подписку на веб-перехватчики в списке SharePoint.</span><span class="sxs-lookup"><span data-stu-id="2d011-104">Creates a new webhook subscription on a SharePoint list.</span></span> 

## <a name="permissions"></a><span data-ttu-id="2d011-105">Разрешения</span><span class="sxs-lookup"><span data-stu-id="2d011-105">Permissions</span></span>

<span data-ttu-id="2d011-106">У приложения должно быть разрешение на изменение списка SharePoint, в котором создается подписка.</span><span class="sxs-lookup"><span data-stu-id="2d011-106">The application must have at least edit permissions to the SharePoint list where the subscription will be created.</span></span>

### <a name="if-your-application-is-a-microsoft-azure-active-directory-azure-ad-application"></a><span data-ttu-id="2d011-107">Если приложение является приложением Microsoft Azure Active Directory (AD)</span><span class="sxs-lookup"><span data-stu-id="2d011-107">If your application is a Microsoft Azure Active Directory (AD) application:</span></span>

<span data-ttu-id="2d011-108">Приложению Azure AD необходимо предоставить разрешения, указанные в следующей таблице:</span><span class="sxs-lookup"><span data-stu-id="2d011-108">You must grant the Azure AD app the permissions specified in the following table:</span></span>

<span data-ttu-id="2d011-109">Приложение</span><span class="sxs-lookup"><span data-stu-id="2d011-109">Application</span></span> | <span data-ttu-id="2d011-110">Разрешение</span><span class="sxs-lookup"><span data-stu-id="2d011-110">Permission</span></span> 
------------|------------
<span data-ttu-id="2d011-111">SharePoint Online в Office 365</span><span class="sxs-lookup"><span data-stu-id="2d011-111">Office 365 SharePoint Online</span></span>|<span data-ttu-id="2d011-112">Чтение и запись элементов и списков во всех семействах веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="2d011-112">Read and write items and lists in all site collections.</span></span>

### <a name="if-your-application-is-a-sharepoint-add-in"></a><span data-ttu-id="2d011-113">Если приложение является надстройкой SharePoint</span><span class="sxs-lookup"><span data-stu-id="2d011-113">If your application is a SharePoint add-in:</span></span>

<span data-ttu-id="2d011-114">Надстройке SharePoint необходимо предоставить по крайней мере следующие разрешения:</span><span class="sxs-lookup"><span data-stu-id="2d011-114">You must grant the SharePoint add-in the following permission(s) or higher:</span></span>

<span data-ttu-id="2d011-115">Область</span><span class="sxs-lookup"><span data-stu-id="2d011-115">Scope</span></span> | <span data-ttu-id="2d011-116">Разрешения</span><span class="sxs-lookup"><span data-stu-id="2d011-116">Permission Rights</span></span> 
------|------------
<span data-ttu-id="2d011-117">Список</span><span class="sxs-lookup"><span data-stu-id="2d011-117">List</span></span>|<span data-ttu-id="2d011-118">Управление</span><span class="sxs-lookup"><span data-stu-id="2d011-118">Manage</span></span>

## <a name="http-request"></a><span data-ttu-id="2d011-119">HTTP-запрос</span><span class="sxs-lookup"><span data-stu-id="2d011-119">HTTP request</span></span>

```
POST /_api/web/lists('list-id')/subscriptions
```

## <a name="request-body"></a><span data-ttu-id="2d011-120">Текст запроса</span><span class="sxs-lookup"><span data-stu-id="2d011-120">Request body</span></span>

<span data-ttu-id="2d011-121">Включите в запрос указанные ниже свойства.</span><span class="sxs-lookup"><span data-stu-id="2d011-121">Include the following properties in the request body.</span></span>

<span data-ttu-id="2d011-122">Имя</span><span class="sxs-lookup"><span data-stu-id="2d011-122">Name</span></span> | <span data-ttu-id="2d011-123">Тип</span><span class="sxs-lookup"><span data-stu-id="2d011-123">Type</span></span> | <span data-ttu-id="2d011-124">Описание</span><span class="sxs-lookup"><span data-stu-id="2d011-124">Description</span></span> 
-----|------|------------
<span data-ttu-id="2d011-125">resource</span><span class="sxs-lookup"><span data-stu-id="2d011-125">resource</span></span>|<span data-ttu-id="2d011-126">строка</span><span class="sxs-lookup"><span data-stu-id="2d011-126">string</span></span>|<span data-ttu-id="2d011-127">URL-адрес списка для получения уведомлений.</span><span class="sxs-lookup"><span data-stu-id="2d011-127">The URL of the list to receive notifications from.</span></span>
<span data-ttu-id="2d011-128">notificationUrl</span><span class="sxs-lookup"><span data-stu-id="2d011-128">notificationUrl</span></span>|<span data-ttu-id="2d011-129">строка</span><span class="sxs-lookup"><span data-stu-id="2d011-129">string</span></span>|<span data-ttu-id="2d011-130">URL-адрес службы для отправки уведомлений.</span><span class="sxs-lookup"><span data-stu-id="2d011-130">The service URL to send notifications to.</span></span>
<span data-ttu-id="2d011-131">expirationDateTime</span><span class="sxs-lookup"><span data-stu-id="2d011-131">expirationDateTime</span></span>|<span data-ttu-id="2d011-132">дата</span><span class="sxs-lookup"><span data-stu-id="2d011-132">date</span></span>|<span data-ttu-id="2d011-133">Срок хранения уведомления.</span><span class="sxs-lookup"><span data-stu-id="2d011-133">The date the notification will expire and be deleted.</span></span>
<span data-ttu-id="2d011-134">client-clientState</span><span class="sxs-lookup"><span data-stu-id="2d011-134">client-clientState</span></span>|<span data-ttu-id="2d011-135">строка</span><span class="sxs-lookup"><span data-stu-id="2d011-135">string</span></span>|<span data-ttu-id="2d011-136">Необязательный.</span><span class="sxs-lookup"><span data-stu-id="2d011-136">Optional.</span></span> <span data-ttu-id="2d011-137">Непрозрачная строка, которая передается клиенту со всеми уведомлениями.</span><span class="sxs-lookup"><span data-stu-id="2d011-137">Optional. Opaque string passed back to the client on all notifications. You can use this for validating notifications, or tagging different subscriptions.</span></span><br/><span data-ttu-id="2d011-138">Ее можно использовать для проверки уведомлений или маркировки различных подписок.</span><span class="sxs-lookup"><span data-stu-id="2d011-138">Optional. Opaque string passed back to the client on all notifications. You can use this for validating notifications, or tagging different subscriptions.</span></span>


### <a name="example"></a><span data-ttu-id="2d011-139">Пример</span><span class="sxs-lookup"><span data-stu-id="2d011-139">Example</span></span>

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

## <a name="response"></a><span data-ttu-id="2d011-140">Ответ</span><span class="sxs-lookup"><span data-stu-id="2d011-140">Response</span></span>

<span data-ttu-id="2d011-141">Если подписка добавлена, возвращается ответ `201 Created`, который содержит новый объект подписки.</span><span class="sxs-lookup"><span data-stu-id="2d011-141">If the subscription is added, then a `201 Created` response is returned that includes the newly created subscription object.</span></span>

### <a name="example"></a><span data-ttu-id="2d011-142">Пример</span><span class="sxs-lookup"><span data-stu-id="2d011-142">Example</span></span>

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

## <a name="url-validation"></a><span data-ttu-id="2d011-143">Проверка URL-адреса</span><span class="sxs-lookup"><span data-stu-id="2d011-143">URL validation</span></span>

<span data-ttu-id="2d011-144">Перед созданием подписки SharePoint отправляет запрос с токеном проверки на указанный URL-адрес службы.</span><span class="sxs-lookup"><span data-stu-id="2d011-144">Before a new subscription is created, SharePoint will send a request with a validation token in the body of the request to the service URL provided. Your service must respond to this request by returning the validation token.</span></span> <span data-ttu-id="2d011-145">Служба должна ответить на него, вернув токен проверки.</span><span class="sxs-lookup"><span data-stu-id="2d011-145">Your service must respond to this request by returning the validation key.</span></span>

<span data-ttu-id="2d011-146">В противном случае подписка не создается.</span><span class="sxs-lookup"><span data-stu-id="2d011-146">If your service fails to validate the request in this way, the subscription will not be created.</span></span>

## <a name="see-also"></a><span data-ttu-id="2d011-147">См. также</span><span class="sxs-lookup"><span data-stu-id="2d011-147">See also</span></span>

- [<span data-ttu-id="2d011-148">Веб-перехватчики для списков SharePoint</span><span class="sxs-lookup"><span data-stu-id="2d011-148">SharePoint list webhooks</span></span>](overview-sharepoint-list-webhooks.md)
- [<span data-ttu-id="2d011-149">Обзор веб-перехватчиков SharePoint</span><span class="sxs-lookup"><span data-stu-id="2d011-149">Overview of SharePoint webhooks</span></span>](../overview-sharepoint-webhooks.md)