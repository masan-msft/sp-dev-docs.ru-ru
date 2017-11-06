---
title: "Получение подписок"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 6dea5da88388c0787c9295141cee2fed50a5fa65
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="get-subscriptions"></a><span data-ttu-id="8d1a2-102">Получение подписок</span><span class="sxs-lookup"><span data-stu-id="8d1a2-102">Get subscriptions</span></span>

<span data-ttu-id="8d1a2-103">Возвращает одну или несколько подписок на веб-перехватчики в списке SharePoint.</span><span class="sxs-lookup"><span data-stu-id="8d1a2-103">Gets one or more webhook subscriptions on a SharePoint list.</span></span>

## <a name="permissions"></a><span data-ttu-id="8d1a2-104">Разрешения</span><span class="sxs-lookup"><span data-stu-id="8d1a2-104">Permissions</span></span>

### <a name="get-a-single-subscription"></a><span data-ttu-id="8d1a2-105">Получение одной подписки</span><span class="sxs-lookup"><span data-stu-id="8d1a2-105">Get a single subscription</span></span>

<span data-ttu-id="8d1a2-106">У приложения должно быть разрешение на изменение списка SharePoint, из которого извлекается подписка.</span><span class="sxs-lookup"><span data-stu-id="8d1a2-106">The application must have at least edit permissions to the SharePoint list where the subscription will be retreived.</span></span>

<span data-ttu-id="8d1a2-107">**Для приложения Microsoft Azure Active Directory (AD):**</span><span class="sxs-lookup"><span data-stu-id="8d1a2-107">**If your application is a Microsoft Azure Active Directory (AD) application:**</span></span>

<span data-ttu-id="8d1a2-p101">Приложению Azure AD необходимо предоставить разрешения, указанные в таблице ниже. Подписку можно получить только из создавшего ее приложения Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8d1a2-p101">You must grant the Azure AD application the permissions specified in the following table. A subscription can only be retrieved by the Azure AD application that created it.</span></span> 

<span data-ttu-id="8d1a2-110">Приложение</span><span class="sxs-lookup"><span data-stu-id="8d1a2-110">Application</span></span> | <span data-ttu-id="8d1a2-111">Разрешение</span><span class="sxs-lookup"><span data-stu-id="8d1a2-111">Permission</span></span> 
------------|------------
<span data-ttu-id="8d1a2-112">SharePoint Online в Office 365</span><span class="sxs-lookup"><span data-stu-id="8d1a2-112">Office 365 SharePoint Online</span></span>|<span data-ttu-id="8d1a2-113">Чтение и запись элементов и списков во всех семействах веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="8d1a2-113">Read and write items and lists in all site collections.</span></span>

<span data-ttu-id="8d1a2-114">**Для надстройки SharePoint**:</span><span class="sxs-lookup"><span data-stu-id="8d1a2-114">**If your application is a SharePoint add-in:**</span></span>

<span data-ttu-id="8d1a2-p102">Надстройке SharePoint необходимо предоставить по крайней мере указанные ниже разрешения. Подписку можно получить только из создавшей ее надстройки SharePoint.</span><span class="sxs-lookup"><span data-stu-id="8d1a2-p102">You must grant the SharePoint add-in the following permission(s) or higher. A subscription can only be retrieved by the SharePoint add-in that created it.</span></span> 

<span data-ttu-id="8d1a2-117">Область</span><span class="sxs-lookup"><span data-stu-id="8d1a2-117">Scope</span></span> | <span data-ttu-id="8d1a2-118">Разрешения</span><span class="sxs-lookup"><span data-stu-id="8d1a2-118">Permission Rights</span></span> 
------|------------
<span data-ttu-id="8d1a2-119">Список</span><span class="sxs-lookup"><span data-stu-id="8d1a2-119">List</span></span>|<span data-ttu-id="8d1a2-120">Управление</span><span class="sxs-lookup"><span data-stu-id="8d1a2-120">Manage</span></span>

### <a name="get-all-subscriptions"></a><span data-ttu-id="8d1a2-121">Получение всех подписок</span><span class="sxs-lookup"><span data-stu-id="8d1a2-121">Get all subscriptions</span></span>

<span data-ttu-id="8d1a2-122">У приложения должны быть разрешения на управление списком SharePoint, из которого извлекается подписка.</span><span class="sxs-lookup"><span data-stu-id="8d1a2-122">The application must have manage list permissions to the SharePoint list where the subscription will be retrieved.</span></span>

<span data-ttu-id="8d1a2-123">**Для приложения Microsoft Azure Active Directory (AD):**</span><span class="sxs-lookup"><span data-stu-id="8d1a2-123">**If your application is a Microsoft Azure Active Directory (AD) application:**</span></span>

<span data-ttu-id="8d1a2-124">Приложению Azure AD необходимо предоставить разрешения, указанные в таблице ниже.</span><span class="sxs-lookup"><span data-stu-id="8d1a2-124">You must grant the Azure AD app the permissions specified in the following table.</span></span> 

<span data-ttu-id="8d1a2-125">Приложение</span><span class="sxs-lookup"><span data-stu-id="8d1a2-125">Application</span></span> | <span data-ttu-id="8d1a2-126">Разрешение</span><span class="sxs-lookup"><span data-stu-id="8d1a2-126">Permission</span></span> 
------------|------------
<span data-ttu-id="8d1a2-127">SharePoint Online в Office 365</span><span class="sxs-lookup"><span data-stu-id="8d1a2-127">Office 365 SharePoint Online</span></span>|<span data-ttu-id="8d1a2-128">Полный доступ ко всем семействам веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="8d1a2-128">Have full control of all site collections.</span></span>

<span data-ttu-id="8d1a2-129">**Для надстройки SharePoint**:</span><span class="sxs-lookup"><span data-stu-id="8d1a2-129">**If your application is a SharePoint add-in:**</span></span>

<span data-ttu-id="8d1a2-130">Надстройке SharePoint необходимо предоставить по крайней мере указанные ниже разрешения.</span><span class="sxs-lookup"><span data-stu-id="8d1a2-130">You must grant the SharePoint add-in the following permission(s) or higher.</span></span> 

<span data-ttu-id="8d1a2-131">Область</span><span class="sxs-lookup"><span data-stu-id="8d1a2-131">Scope</span></span> | <span data-ttu-id="8d1a2-132">Разрешения</span><span class="sxs-lookup"><span data-stu-id="8d1a2-132">Permission Rights</span></span> 
------|------------
<span data-ttu-id="8d1a2-133">Список</span><span class="sxs-lookup"><span data-stu-id="8d1a2-133">List</span></span>|<span data-ttu-id="8d1a2-134">Полный доступ</span><span class="sxs-lookup"><span data-stu-id="8d1a2-134">Full control</span></span>

## <a name="http-request"></a><span data-ttu-id="8d1a2-135">HTTP-запрос</span><span class="sxs-lookup"><span data-stu-id="8d1a2-135">HTTP request</span></span>

### <a name="get-a-single-subscription"></a><span data-ttu-id="8d1a2-136">Получение одной подписки</span><span class="sxs-lookup"><span data-stu-id="8d1a2-136">Get a single subscription</span></span>

#### <a name="list-webhook"></a><span data-ttu-id="8d1a2-137">Веб-перехватчик списка</span><span class="sxs-lookup"><span data-stu-id="8d1a2-137">List webhook</span></span>
```
GET _api/web/lists('list-id')/subscriptions('id')
```

##### <a name="example"></a><span data-ttu-id="8d1a2-138">Пример</span><span class="sxs-lookup"><span data-stu-id="8d1a2-138">Example</span></span>

```http
GET _api/web/lists('5C77031A-9621-4DFC-BB5D-57803A94E91D')/subscriptions('6D77031A-2345-5GRT-BV3D-55234B56FR43')
```

#### <a name="request-body"></a><span data-ttu-id="8d1a2-139">Текст запроса</span><span class="sxs-lookup"><span data-stu-id="8d1a2-139">Request body</span></span>

<span data-ttu-id="8d1a2-140">Не указывайте тело запроса для этого метода.</span><span class="sxs-lookup"><span data-stu-id="8d1a2-140">Do not supply a request body for this method.</span></span>

##### <a name="response"></a><span data-ttu-id="8d1a2-141">Отклик</span><span class="sxs-lookup"><span data-stu-id="8d1a2-141">Response</span></span>

<span data-ttu-id="8d1a2-142">Возвращает подписку, которую можно просмотреть в приложении, отправившем вызов.</span><span class="sxs-lookup"><span data-stu-id="8d1a2-142">This returns the subscription viewable by the calling application.</span></span>

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "odata.metadata": "https://contoso.sharepoint.com/_api/$metadata#SP.ApiData.Subscriptions/@Element",
  "odata.type": "Microsoft.SharePoint.Webhooks.Subscription",
  "odata.id": "https://contoso.sharepoint.com/_api/web/lists('5C77031A-9621-4DFC-BB5D-57803A94E91D')/subscriptions('a8e6d5e6-9f7f-497a-b97f-8ffe8f559dc7')",
  "odata.editLink": "web/lists('5C77031A-9621-4DFC-BB5D-57803A94E91D')/subscriptions('a8e6d5e6-9f7f-497a-b97f-8ffe8f559dc7')",
  "expirationDateTime": "2016-04-30T16:17:57Z",
  "id": "a8e6d5e6-9f7f-497a-b97f-8ffe8f559dc7",
  "notificationUrl": "https://contoso.azurewebistes.net/api/webhook/handlerequest",
  "resource": "5c77031a-9621-4dfc-bb5d-57803a94e91d"
}
```

### <a name="get-all-subscriptions"></a><span data-ttu-id="8d1a2-143">Получение всех подписок</span><span class="sxs-lookup"><span data-stu-id="8d1a2-143">Get all subscriptions</span></span>

#### <a name="list-webhook"></a><span data-ttu-id="8d1a2-144">Веб-перехватчик списка</span><span class="sxs-lookup"><span data-stu-id="8d1a2-144">List webhook</span></span>
```
GET _api/web/lists('list-id')/subscriptions
```

##### <a name="example"></a><span data-ttu-id="8d1a2-145">Пример</span><span class="sxs-lookup"><span data-stu-id="8d1a2-145">Example</span></span>

```http
GET _api/web/lists('5C77031A-9621-4DFC-BB5D-57803A94E91D')/subscriptions
```

#### <a name="request-body"></a><span data-ttu-id="8d1a2-146">Текст запроса</span><span class="sxs-lookup"><span data-stu-id="8d1a2-146">Request body</span></span>

<span data-ttu-id="8d1a2-147">Не указывайте тело запроса для этого метода.</span><span class="sxs-lookup"><span data-stu-id="8d1a2-147">Do not supply a request body for this method.</span></span>

##### <a name="response"></a><span data-ttu-id="8d1a2-148">Отклик</span><span class="sxs-lookup"><span data-stu-id="8d1a2-148">Response</span></span>

<span data-ttu-id="8d1a2-149">Возвращает коллекцию всех подписок в ресурсе SharePoint.</span><span class="sxs-lookup"><span data-stu-id="8d1a2-149">This returns a collection of all subscriptions on a SharePoint resource.</span></span> 

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "odata.metadata": "https://a830edad9050849295j16032914.sharepoint.com/_api/$metadata#SP.ApiData.Subscriptions",
  "value": [
    {
      "odata.type": "Microsoft.SharePoint.Webhooks.Subscription",
      "odata.id": "https://contoso.sharepoint.com/_api/Microsoft.SharePoint.Webhooks.Subscriptionc3175b9c-1491-454f-b5da-980431e36146",
      "odata.editLink": "Microsoft.SharePoint.Webhooks.Subscriptionc3175b9c-1491-454f-b5da-980431e36146",
      "clientState": "{A0A354EC-97D4-4D83-9DDB-144077ADB449}",
      "expirationDateTime": "2016-04-30T16:17:57Z",
      "id": "a8e6d5e6-9f7f-497a-b97f-8ffe8f559dc7",
      "notificationUrl": "https://contoso.azurewebsites.net/api/webhook/handlerequest",
      "resource": "5c77031a-9621-4dfc-bb5d-57803a94e91d"
    }
  ]
}
```
