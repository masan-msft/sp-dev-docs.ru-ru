---
title: "Получение подписок"
description: "Возвращает одну или несколько подписок на веб-перехватчики в списке SharePoint."
ms.date: 02/08/2018
ms.prod: sharepoint
ms.openlocfilehash: d56b69691eed234f65c2fac25e934a9fe6e00d33
ms.sourcegitcommit: e157d51378190ddfed6394ba154ce66141c8ca33
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/19/2018
---
# <a name="get-subscriptions"></a><span data-ttu-id="a2fda-103">Получение подписок</span><span class="sxs-lookup"><span data-stu-id="a2fda-103">Get subscriptions</span></span>

<span data-ttu-id="a2fda-104">Возвращает одну или несколько подписок на веб-перехватчики в списке SharePoint.</span><span class="sxs-lookup"><span data-stu-id="a2fda-104">Gets one or more webhook subscriptions on a SharePoint list.</span></span>

## <a name="permissions"></a><span data-ttu-id="a2fda-105">Разрешения</span><span class="sxs-lookup"><span data-stu-id="a2fda-105">Permissions</span></span>

### <a name="get-a-single-subscription"></a><span data-ttu-id="a2fda-106">Получение одной подписки</span><span class="sxs-lookup"><span data-stu-id="a2fda-106">Get a single subscription</span></span>

<span data-ttu-id="a2fda-107">У приложения должно быть по крайней мере разрешение на изменение списка SharePoint, из которого извлекается подписка.</span><span class="sxs-lookup"><span data-stu-id="a2fda-107">The application must have at least edit permissions to the SharePoint list where the subscription will be retreived.</span></span>

#### <a name="if-your-application-is-a-microsoft-azure-active-directory-azure-ad-application"></a><span data-ttu-id="a2fda-108">Если приложение является приложением Microsoft Azure Active Directory (AD)</span><span class="sxs-lookup"><span data-stu-id="a2fda-108">If your application is a Microsoft Azure Active Directory (AD) application:</span></span>

<span data-ttu-id="a2fda-p101">Приложению Azure AD необходимо предоставить разрешения, указанные в таблице ниже. Подписку можно получить только из создавшего ее приложения Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a2fda-p101">You must grant the Azure AD application the permissions specified in the following table. A subscription can only be retrieved by the Azure AD application that created it.</span></span> 

<span data-ttu-id="a2fda-111">Приложение</span><span class="sxs-lookup"><span data-stu-id="a2fda-111">Application</span></span> | <span data-ttu-id="a2fda-112">Разрешение</span><span class="sxs-lookup"><span data-stu-id="a2fda-112">Permission</span></span> 
------------|------------
<span data-ttu-id="a2fda-113">SharePoint Online в Office 365</span><span class="sxs-lookup"><span data-stu-id="a2fda-113">Office 365 SharePoint Online</span></span>|<span data-ttu-id="a2fda-114">Чтение и запись элементов и списков во всех семействах веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="a2fda-114">Read and write items and lists in all site collections.</span></span>

#### <a name="if-your-application-is-a-sharepoint-add-in"></a><span data-ttu-id="a2fda-115">Если приложение является надстройкой SharePoint</span><span class="sxs-lookup"><span data-stu-id="a2fda-115">If your application is a SharePoint add-in:</span></span>

<span data-ttu-id="a2fda-116">Надстройке SharePoint необходимо предоставить по крайней мере указанные ниже разрешения.</span><span class="sxs-lookup"><span data-stu-id="a2fda-116">You must grant the SharePoint add-in the following permission(s) or higher:</span></span> <span data-ttu-id="a2fda-117">Подписку можно получить только из создавшей ее надстройки SharePoint.</span><span class="sxs-lookup"><span data-stu-id="a2fda-117">You must grant the SharePoint add-in the following permission(s) or higher. A subscription can only be retrieved by the SharePoint add-in that created it.</span></span> 

<span data-ttu-id="a2fda-118">Область</span><span class="sxs-lookup"><span data-stu-id="a2fda-118">Scope</span></span> | <span data-ttu-id="a2fda-119">Разрешения</span><span class="sxs-lookup"><span data-stu-id="a2fda-119">Permission Rights</span></span> 
------|------------
<span data-ttu-id="a2fda-120">Список</span><span class="sxs-lookup"><span data-stu-id="a2fda-120">List</span></span>|<span data-ttu-id="a2fda-121">Управление</span><span class="sxs-lookup"><span data-stu-id="a2fda-121">Manage</span></span>

### <a name="get-all-subscriptions"></a><span data-ttu-id="a2fda-122">Получение всех подписок</span><span class="sxs-lookup"><span data-stu-id="a2fda-122">Get all subscriptions</span></span>

<span data-ttu-id="a2fda-123">У приложения должны быть разрешения на управление списком SharePoint, из которого извлекается подписка.</span><span class="sxs-lookup"><span data-stu-id="a2fda-123">The application must have manage list permissions to the SharePoint list where the subscription will be retrieved.</span></span>

#### <a name="if-your-application-is-an-azure-ad-application"></a><span data-ttu-id="a2fda-124">Если ваше приложение является приложением Azure AD</span><span class="sxs-lookup"><span data-stu-id="a2fda-124">If your application is an Microsoft Azure Active Directory (AD) application:</span></span>

<span data-ttu-id="a2fda-125">Приложению Azure AD App необходимо предоставить разрешения, указанные в таблице ниже.</span><span class="sxs-lookup"><span data-stu-id="a2fda-125">You must grant the Azure AD app the permissions specified in the following table.</span></span> 

<span data-ttu-id="a2fda-126">Приложение</span><span class="sxs-lookup"><span data-stu-id="a2fda-126">Application</span></span> | <span data-ttu-id="a2fda-127">Разрешение</span><span class="sxs-lookup"><span data-stu-id="a2fda-127">Permission</span></span> 
------------|------------
<span data-ttu-id="a2fda-128">SharePoint Online в Office 365</span><span class="sxs-lookup"><span data-stu-id="a2fda-128">Office 365 SharePoint Online</span></span>|<span data-ttu-id="a2fda-129">Полный доступ ко всем семействам веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="a2fda-129">Have full control of all site collections.</span></span>

#### <a name="if-your-application-is-a-sharepoint-add-in"></a><span data-ttu-id="a2fda-130">Если приложение является надстройкой SharePoint</span><span class="sxs-lookup"><span data-stu-id="a2fda-130">If your application is a SharePoint add-in:</span></span>

<span data-ttu-id="a2fda-131">Надстройке SharePoint необходимо предоставить по крайней мере указанные ниже разрешения.</span><span class="sxs-lookup"><span data-stu-id="a2fda-131">You must grant the SharePoint add-in the following permission(s) or higher:</span></span> 

<span data-ttu-id="a2fda-132">Область</span><span class="sxs-lookup"><span data-stu-id="a2fda-132">Scope</span></span> | <span data-ttu-id="a2fda-133">Разрешения</span><span class="sxs-lookup"><span data-stu-id="a2fda-133">Permission Rights</span></span> 
------|------------
<span data-ttu-id="a2fda-134">Список</span><span class="sxs-lookup"><span data-stu-id="a2fda-134">List</span></span>|<span data-ttu-id="a2fda-135">Полный доступ</span><span class="sxs-lookup"><span data-stu-id="a2fda-135">Full control</span></span>

## <a name="http-request"></a><span data-ttu-id="a2fda-136">HTTP-запрос</span><span class="sxs-lookup"><span data-stu-id="a2fda-136">HTTP request</span></span>

### <a name="get-a-single-subscription"></a><span data-ttu-id="a2fda-137">Получение одной подписки</span><span class="sxs-lookup"><span data-stu-id="a2fda-137">Get a single subscription</span></span>

#### <a name="list-webhook"></a><span data-ttu-id="a2fda-138">Веб-перехватчик списка</span><span class="sxs-lookup"><span data-stu-id="a2fda-138">List webhook</span></span>
```
GET _api/web/lists('list-id')/subscriptions('id')
```

##### <a name="example"></a><span data-ttu-id="a2fda-139">Пример</span><span class="sxs-lookup"><span data-stu-id="a2fda-139">Example</span></span>

```http
GET _api/web/lists('5C77031A-9621-4DFC-BB5D-57803A94E91D')/subscriptions('6D77031A-2345-5GRT-BV3D-55234B56FR43')
```

#### <a name="request-body"></a><span data-ttu-id="a2fda-140">Текст запроса</span><span class="sxs-lookup"><span data-stu-id="a2fda-140">Request body</span></span>

<span data-ttu-id="a2fda-141">Не указывайте тело запроса для этого метода.</span><span class="sxs-lookup"><span data-stu-id="a2fda-141">Do not supply a request body for this method.</span></span>

#### <a name="response"></a><span data-ttu-id="a2fda-142">Отклик</span><span class="sxs-lookup"><span data-stu-id="a2fda-142">Response</span></span>

<span data-ttu-id="a2fda-143">Возвращает подписку, которую можно просмотреть в приложении, отправившем вызов.</span><span class="sxs-lookup"><span data-stu-id="a2fda-143">This returns the subscription viewable by the calling application.</span></span>

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

### <a name="get-all-subscriptions"></a><span data-ttu-id="a2fda-144">Получение всех подписок</span><span class="sxs-lookup"><span data-stu-id="a2fda-144">Get all subscriptions</span></span>

#### <a name="list-webhook"></a><span data-ttu-id="a2fda-145">Веб-перехватчик списка</span><span class="sxs-lookup"><span data-stu-id="a2fda-145">List webhook</span></span>
```
GET _api/web/lists('list-id')/subscriptions
```

##### <a name="example"></a><span data-ttu-id="a2fda-146">Пример</span><span class="sxs-lookup"><span data-stu-id="a2fda-146">Example</span></span>

```http
GET _api/web/lists('5C77031A-9621-4DFC-BB5D-57803A94E91D')/subscriptions
```

#### <a name="request-body"></a><span data-ttu-id="a2fda-147">Текст запроса</span><span class="sxs-lookup"><span data-stu-id="a2fda-147">Request body</span></span>

<span data-ttu-id="a2fda-148">Не указывайте тело запроса для этого метода.</span><span class="sxs-lookup"><span data-stu-id="a2fda-148">Do not supply a request body for this method.</span></span>

#### <a name="response"></a><span data-ttu-id="a2fda-149">Отклик</span><span class="sxs-lookup"><span data-stu-id="a2fda-149">Response</span></span>

<span data-ttu-id="a2fda-150">Возвращает коллекцию всех подписок на ресурсе SharePoint.</span><span class="sxs-lookup"><span data-stu-id="a2fda-150">This returns a collection of all subscriptions on a SharePoint resource.</span></span> 

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

## <a name="see-also"></a><span data-ttu-id="a2fda-151">См. также</span><span class="sxs-lookup"><span data-stu-id="a2fda-151">See also</span></span>

- [<span data-ttu-id="a2fda-152">Веб-перехватчики для списков SharePoint</span><span class="sxs-lookup"><span data-stu-id="a2fda-152">SharePoint list webhooks</span></span>](overview-sharepoint-list-webhooks.md)
- [<span data-ttu-id="a2fda-153">Обзор веб-перехватчиков SharePoint</span><span class="sxs-lookup"><span data-stu-id="a2fda-153">Overview of SharePoint webhooks</span></span>](../overview-sharepoint-webhooks.md)