---
title: "Обновление подписки"
description: "Обновляет подписку на веб-перехватчики для списка SharePoint."
ms.date: 02/08/2018
ms.prod: sharepoint
ms.openlocfilehash: fe8a0960f597d50d77b22a29f14f21afec20c422
ms.sourcegitcommit: e157d51378190ddfed6394ba154ce66141c8ca33
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/19/2018
---
# <a name="update-a-subscription"></a><span data-ttu-id="dac8b-103">Обновление подписки</span><span class="sxs-lookup"><span data-stu-id="dac8b-103">Update a subscription</span></span>

<span data-ttu-id="dac8b-104">Обновляет подписку на веб-перехватчики для списка SharePoint.</span><span class="sxs-lookup"><span data-stu-id="dac8b-104">Updates a webhook subscription on a SharePoint list.</span></span>

## <a name="permissions"></a><span data-ttu-id="dac8b-105">Разрешения</span><span class="sxs-lookup"><span data-stu-id="dac8b-105">Permissions</span></span>

<span data-ttu-id="dac8b-106">Приложение должно иметь по крайней мере разрешение на изменение списка SharePoint, в котором обновляется подписка.</span><span class="sxs-lookup"><span data-stu-id="dac8b-106">The application must have at least edit permissions to the SharePoint list where the subscription will be updated.</span></span>  

### <a name="if-your-application-is-a-microsoft-azure-active-directory-azure-ad-application"></a><span data-ttu-id="dac8b-107">Если приложение является приложением Microsoft Azure Active Directory (AD)</span><span class="sxs-lookup"><span data-stu-id="dac8b-107">If your application is a Microsoft Azure Active Directory (AD) application:</span></span>

<span data-ttu-id="dac8b-p101">Приложению Azure AD необходимо предоставить разрешения, указанные в таблице ниже. Подписку можно обновить только из приложения Azure AD, в котором она создана.</span><span class="sxs-lookup"><span data-stu-id="dac8b-p101">You must grant the Azure AD application the permissions specified in the following table. A subscription can only be updated by the Azure AD application that created it.</span></span>

<span data-ttu-id="dac8b-110">Приложение</span><span class="sxs-lookup"><span data-stu-id="dac8b-110">Application</span></span> | <span data-ttu-id="dac8b-111">Разрешение</span><span class="sxs-lookup"><span data-stu-id="dac8b-111">Permission</span></span> 
------------|------------
<span data-ttu-id="dac8b-112">SharePoint Online в Office 365</span><span class="sxs-lookup"><span data-stu-id="dac8b-112">Office 365 SharePoint Online</span></span>|<span data-ttu-id="dac8b-113">Чтение и запись элементов и списков во всех семействах веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="dac8b-113">Read and write items and lists in all site collections.</span></span> 

### <a name="if-your-application-is-a-sharepoint-add-in"></a><span data-ttu-id="dac8b-114">Если приложение является надстройкой SharePoint</span><span class="sxs-lookup"><span data-stu-id="dac8b-114">If your application is a SharePoint add-in:</span></span>

<span data-ttu-id="dac8b-115">Надстройке SharePoint необходимо предоставить по крайней мере указанные ниже разрешения.</span><span class="sxs-lookup"><span data-stu-id="dac8b-115">You must grant the SharePoint add-in the following permission(s) or higher:</span></span> <span data-ttu-id="dac8b-116">Подписку можно обновить только из надстройки SharePoint, в которой она создана.</span><span class="sxs-lookup"><span data-stu-id="dac8b-116">You must grant the SharePoint add-in the following permission(s) or higher. A subscription can only be updated by the SharePoint add-in that created it.</span></span>

<span data-ttu-id="dac8b-117">Область</span><span class="sxs-lookup"><span data-stu-id="dac8b-117">Scope</span></span> | <span data-ttu-id="dac8b-118">Разрешения</span><span class="sxs-lookup"><span data-stu-id="dac8b-118">Permission Rights</span></span> 
------|------------
<span data-ttu-id="dac8b-119">Список</span><span class="sxs-lookup"><span data-stu-id="dac8b-119">List</span></span>|<span data-ttu-id="dac8b-120">Управление</span><span class="sxs-lookup"><span data-stu-id="dac8b-120">Manage</span></span>

## <a name="http-request"></a><span data-ttu-id="dac8b-121">HTTP-запрос</span><span class="sxs-lookup"><span data-stu-id="dac8b-121">HTTP request</span></span>

```
PATCH _api/web/lists('list-id')/subscriptions('id')
```

### <a name="example"></a><span data-ttu-id="dac8b-122">Пример</span><span class="sxs-lookup"><span data-stu-id="dac8b-122">Example</span></span>

```http
PATCH _api/web/lists('5C77031A-9621-4DFC-BB5D-57803A94E91D')/subscriptions('6D77031A-2345-5GRT-BV3D-55234B56FR43')
Content-Type: application/json

{
  "notificationUrl": "https://contoso.azurewebsites.net/api/v2/webhook-receiver",
  "expirationDateTime": "2016-01-03T11:23:00.000Z"
}
```

## <a name="request-body"></a><span data-ttu-id="dac8b-123">Тело запроса</span><span class="sxs-lookup"><span data-stu-id="dac8b-123">Request body</span></span>

<span data-ttu-id="dac8b-124">Включите в запрос указанные ниже свойства.</span><span class="sxs-lookup"><span data-stu-id="dac8b-124">Include the following properties in the request body.</span></span>

<span data-ttu-id="dac8b-125">Имя</span><span class="sxs-lookup"><span data-stu-id="dac8b-125">Name</span></span> | <span data-ttu-id="dac8b-126">Тип</span><span class="sxs-lookup"><span data-stu-id="dac8b-126">Type</span></span> | <span data-ttu-id="dac8b-127">Описание</span><span class="sxs-lookup"><span data-stu-id="dac8b-127">Description</span></span> 
-----|------|------------
<span data-ttu-id="dac8b-128">notificationUrl</span><span class="sxs-lookup"><span data-stu-id="dac8b-128">notificationUrl</span></span>|<span data-ttu-id="dac8b-129">строка</span><span class="sxs-lookup"><span data-stu-id="dac8b-129">string</span></span>|<span data-ttu-id="dac8b-130">URL-адрес службы для отправки уведомлений.</span><span class="sxs-lookup"><span data-stu-id="dac8b-130">The service URL to send notifications to.</span></span>
<span data-ttu-id="dac8b-131">expirationDateTime</span><span class="sxs-lookup"><span data-stu-id="dac8b-131">expirationDateTime</span></span>|<span data-ttu-id="dac8b-132">дата</span><span class="sxs-lookup"><span data-stu-id="dac8b-132">date</span></span>|<span data-ttu-id="dac8b-133">Срок хранения уведомления.</span><span class="sxs-lookup"><span data-stu-id="dac8b-133">The date the notification will expire and be deleted.</span></span>
<span data-ttu-id="dac8b-134">client-clientState</span><span class="sxs-lookup"><span data-stu-id="dac8b-134">client-clientState</span></span>|<span data-ttu-id="dac8b-135">строка</span><span class="sxs-lookup"><span data-stu-id="dac8b-135">string</span></span>|<span data-ttu-id="dac8b-136">Необязательный.</span><span class="sxs-lookup"><span data-stu-id="dac8b-136">Optional.</span></span> <span data-ttu-id="dac8b-137">Непрозрачная строка, которая передается клиенту со всеми уведомлениями.</span><span class="sxs-lookup"><span data-stu-id="dac8b-137">Optional. Opaque string passed back to the client on all notifications. You can use this for validating notifications, or tagging different subscriptions.</span></span><br/><span data-ttu-id="dac8b-138">Ее можно использовать для проверки уведомлений или маркировки различных подписок.</span><span class="sxs-lookup"><span data-stu-id="dac8b-138">Optional. Opaque string passed back to the client on all notifications. You can use this for validating notifications, or tagging different subscriptions.</span></span>


## <a name="response"></a><span data-ttu-id="dac8b-139">Ответ</span><span class="sxs-lookup"><span data-stu-id="dac8b-139">Response</span></span>

<span data-ttu-id="dac8b-140">Если подписка найдена и успешно обновлена, возвращается ответ `204 No Content`.</span><span class="sxs-lookup"><span data-stu-id="dac8b-140">If the subscription is found and successfully updated, then a `204 No Content` response is returned:</span></span>

### <a name="example"></a><span data-ttu-id="dac8b-141">Пример</span><span class="sxs-lookup"><span data-stu-id="dac8b-141">Example</span></span>

```http
HTTP/1.1 204 No Content
```

## <a name="see-also"></a><span data-ttu-id="dac8b-142">См. также</span><span class="sxs-lookup"><span data-stu-id="dac8b-142">See also</span></span>

- [<span data-ttu-id="dac8b-143">Веб-перехватчики для списков SharePoint</span><span class="sxs-lookup"><span data-stu-id="dac8b-143">SharePoint list webhooks</span></span>](overview-sharepoint-list-webhooks.md)
- [<span data-ttu-id="dac8b-144">Обзор веб-перехватчиков SharePoint</span><span class="sxs-lookup"><span data-stu-id="dac8b-144">Overview of SharePoint webhooks</span></span>](../overview-sharepoint-webhooks.md)