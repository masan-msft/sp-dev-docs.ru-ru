---
title: "Обновление подписки"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 6638ad3f3919f9e14497adb7dacc1c1a09c139f6
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="update-a-subscription"></a><span data-ttu-id="e77f5-102">Обновление подписки</span><span class="sxs-lookup"><span data-stu-id="e77f5-102">Update a subscription</span></span>

<span data-ttu-id="e77f5-103">Обновляет подписку на веб-перехватчики для списка SharePoint.</span><span class="sxs-lookup"><span data-stu-id="e77f5-103">Updates a webhook subscription on a SharePoint list.</span></span>

## <a name="permissions"></a><span data-ttu-id="e77f5-104">Разрешения</span><span class="sxs-lookup"><span data-stu-id="e77f5-104">Permissions</span></span>

<span data-ttu-id="e77f5-105">У приложения должно быть разрешение на изменение списка SharePoint, в котором обновляется подписка.</span><span class="sxs-lookup"><span data-stu-id="e77f5-105">The application must have at least edit permissions to the SharePoint list where the subscription will be updated.</span></span>  

<span data-ttu-id="e77f5-106">**Если приложение является приложением Microsoft Azure Active Directory (AD)**:</span><span class="sxs-lookup"><span data-stu-id="e77f5-106">**If your application is an Microsoft Azure Active Directory (AD) application:**</span></span>

<span data-ttu-id="e77f5-p101">Приложению Azure AD необходимо предоставить разрешения, указанные в таблице ниже. Подписку можно обновить только из приложения Azure AD, в котором она создана.</span><span class="sxs-lookup"><span data-stu-id="e77f5-p101">You must grant the Azure AD application the permissions specified in the following table. A subscription can only be updated by the Azure AD application that created it.</span></span>

<span data-ttu-id="e77f5-109">Приложение</span><span class="sxs-lookup"><span data-stu-id="e77f5-109">Application</span></span> | <span data-ttu-id="e77f5-110">Разрешение</span><span class="sxs-lookup"><span data-stu-id="e77f5-110">Permission</span></span> 
------------|------------
<span data-ttu-id="e77f5-111">SharePoint Online в Office 365</span><span class="sxs-lookup"><span data-stu-id="e77f5-111">Office 365 SharePoint Online</span></span>|<span data-ttu-id="e77f5-112">Чтение и запись элементов и списков во всех семействах веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="e77f5-112">Read and write items and lists in all site collections.</span></span> 

<span data-ttu-id="e77f5-113">**Для надстройки SharePoint**:</span><span class="sxs-lookup"><span data-stu-id="e77f5-113">**If your application is a SharePoint add-in:**</span></span>

<span data-ttu-id="e77f5-p102">Надстройке SharePoint необходимо предоставить по крайней мере указанные ниже разрешения. Подписку можно обновить только из надстройки SharePoint, в которой она создана.</span><span class="sxs-lookup"><span data-stu-id="e77f5-p102">You must grant the SharePoint add-in the following permission(s) or higher. A subscription can only be updated by the SharePoint add-in that created it.</span></span>

<span data-ttu-id="e77f5-116">Область</span><span class="sxs-lookup"><span data-stu-id="e77f5-116">Scope</span></span> | <span data-ttu-id="e77f5-117">Разрешения</span><span class="sxs-lookup"><span data-stu-id="e77f5-117">Permission Rights</span></span> 
------|------------
<span data-ttu-id="e77f5-118">Список</span><span class="sxs-lookup"><span data-stu-id="e77f5-118">List</span></span>|<span data-ttu-id="e77f5-119">Управление</span><span class="sxs-lookup"><span data-stu-id="e77f5-119">Manage</span></span>

## <a name="http-request"></a><span data-ttu-id="e77f5-120">HTTP-запрос</span><span class="sxs-lookup"><span data-stu-id="e77f5-120">HTTP request</span></span>

```
PATCH _api/web/lists('list-id')/subscriptions('id')
```

### <a name="example"></a><span data-ttu-id="e77f5-121">Пример</span><span class="sxs-lookup"><span data-stu-id="e77f5-121">Example</span></span>

```http
PATCH _api/web/lists('5C77031A-9621-4DFC-BB5D-57803A94E91D')/subscriptions('6D77031A-2345-5GRT-BV3D-55234B56FR43')
Content-Type: application/json

{
  "notificationUrl": "https://contoso.azurewebsites.net/api/v2/webhook-receiver",
  "expirationDateTime": "2016-01-03T11:23:00.000Z"
}
```

## <a name="request-body"></a><span data-ttu-id="e77f5-122">Тело запроса</span><span class="sxs-lookup"><span data-stu-id="e77f5-122">Request body</span></span>

<span data-ttu-id="e77f5-123">Включите в запрос указанные ниже свойства.</span><span class="sxs-lookup"><span data-stu-id="e77f5-123">Include the following properties in the request body.</span></span>

<span data-ttu-id="e77f5-124">Имя</span><span class="sxs-lookup"><span data-stu-id="e77f5-124">Name</span></span> | <span data-ttu-id="e77f5-125">Тип</span><span class="sxs-lookup"><span data-stu-id="e77f5-125">Type</span></span> | <span data-ttu-id="e77f5-126">Описание</span><span class="sxs-lookup"><span data-stu-id="e77f5-126">Description</span></span> 
-----|------|------------
<span data-ttu-id="e77f5-127">notificationUrl</span><span class="sxs-lookup"><span data-stu-id="e77f5-127">notificationUrl</span></span>|<span data-ttu-id="e77f5-128">строка</span><span class="sxs-lookup"><span data-stu-id="e77f5-128">string</span></span>|<span data-ttu-id="e77f5-129">URL-адрес службы для отправки уведомлений.</span><span class="sxs-lookup"><span data-stu-id="e77f5-129">The service URL to send notifications to.</span></span>
<span data-ttu-id="e77f5-130">expirationDateTime</span><span class="sxs-lookup"><span data-stu-id="e77f5-130">expirationDateTime</span></span>|<span data-ttu-id="e77f5-131">дата</span><span class="sxs-lookup"><span data-stu-id="e77f5-131">date</span></span>|<span data-ttu-id="e77f5-132">Срок хранения уведомления.</span><span class="sxs-lookup"><span data-stu-id="e77f5-132">The date the notification will expire and be deleted.</span></span>
<span data-ttu-id="e77f5-133">client-clientState</span><span class="sxs-lookup"><span data-stu-id="e77f5-133">client-clientState</span></span>|<span data-ttu-id="e77f5-134">string</span><span class="sxs-lookup"><span data-stu-id="e77f5-134">string</span></span>|<span data-ttu-id="e77f5-p103">Необязательный. Непрозрачная строка, которая передается клиенту со всеми уведомлениями. Ее можно использовать для проверки уведомлений и маркировки различных подписок.</span><span class="sxs-lookup"><span data-stu-id="e77f5-p103">Optional. Opaque string passed back to the client on all notifications. You can use this for validating notifications, or tagging different subscriptions.</span></span>


## <a name="response"></a><span data-ttu-id="e77f5-138">Отклик</span><span class="sxs-lookup"><span data-stu-id="e77f5-138">Response</span></span>

<span data-ttu-id="e77f5-139">Если подписка найдена и обновление выполнено успешно, возвращается отклик `204 No Content`.</span><span class="sxs-lookup"><span data-stu-id="e77f5-139">If the subscription is found and successfully updated, then a `204 No Content` response is returned:</span></span>

### <a name="example"></a><span data-ttu-id="e77f5-140">Пример</span><span class="sxs-lookup"><span data-stu-id="e77f5-140">Example</span></span>

```http
HTTP/1.1 204 No Content
```
