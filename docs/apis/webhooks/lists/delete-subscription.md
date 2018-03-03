---
title: "Удаление подписки"
description: "Удаляет подписку на веб-перехватчики из списка SharePoint. После удаления подписки доставка уведомлений прекращается."
ms.date: 02/08/2018
ms.prod: sharepoint
ms.openlocfilehash: 69ddbfcc4274b307bd262d72922a7651de5a2745
ms.sourcegitcommit: e157d51378190ddfed6394ba154ce66141c8ca33
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/19/2018
---
# <a name="delete-a-subscription"></a><span data-ttu-id="443e0-104">Удаление подписки</span><span class="sxs-lookup"><span data-stu-id="443e0-104">Delete a subscription</span></span>

<span data-ttu-id="443e0-105">Удаляет подписку на веб-перехватчики из списка SharePoint.</span><span class="sxs-lookup"><span data-stu-id="443e0-105">Deletes a webhook subscription from a SharePoint list. After deleting the subscription notifications will no longer be delivered.</span></span> <span data-ttu-id="443e0-106">После удаления подписки доставка уведомлений прекращается.</span><span class="sxs-lookup"><span data-stu-id="443e0-106">After deleting the subscription, notifications are no longer delivered.</span></span>

## <a name="permissions"></a><span data-ttu-id="443e0-107">Разрешения</span><span class="sxs-lookup"><span data-stu-id="443e0-107">Permissions</span></span>

<span data-ttu-id="443e0-108">У приложения должно быть разрешение по крайней мере на изменение списка SharePoint, из которого удаляется подписка.</span><span class="sxs-lookup"><span data-stu-id="443e0-108">The application must have at least edit permissions to the SharePoint list where the subscription will be deleted.</span></span>

### <a name="if-your-application-is-a-microsoft-azure-active-directory-azure-ad-application"></a><span data-ttu-id="443e0-109">Если приложение является приложением Microsoft Azure Active Directory (AD)</span><span class="sxs-lookup"><span data-stu-id="443e0-109">If your application is a Microsoft Azure Active Directory (AD) application:</span></span>

<span data-ttu-id="443e0-p103">Приложению Azure AD необходимо предоставить разрешения, указанные в таблице ниже. Подписку можно удалить только из приложения Azure AD, в котором она создана.</span><span class="sxs-lookup"><span data-stu-id="443e0-p103">You must grant the Azure AD app the permissions specified in the following table. A subscription can only be deleted by the Azure AD application that created it.</span></span>

<span data-ttu-id="443e0-112">Приложение</span><span class="sxs-lookup"><span data-stu-id="443e0-112">Application</span></span> | <span data-ttu-id="443e0-113">Разрешение</span><span class="sxs-lookup"><span data-stu-id="443e0-113">Permission</span></span> 
------------|------------
<span data-ttu-id="443e0-114">SharePoint Online в Office 365</span><span class="sxs-lookup"><span data-stu-id="443e0-114">Office 365 SharePoint Online</span></span>|<span data-ttu-id="443e0-115">Чтение и запись элементов и списков во всех семействах веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="443e0-115">Read and write items and lists in all site collections.</span></span>

### <a name="if-your-application-is-a-sharepoint-add-in"></a><span data-ttu-id="443e0-116">Если приложение является надстройкой SharePoint</span><span class="sxs-lookup"><span data-stu-id="443e0-116">If your application is a SharePoint add-in:</span></span>

<span data-ttu-id="443e0-117">Надстройке SharePoint необходимо предоставить по крайней мере указанные ниже разрешения.</span><span class="sxs-lookup"><span data-stu-id="443e0-117">You must grant the SharePoint add-in the following permission(s) or higher:</span></span> <span data-ttu-id="443e0-118">Подписку можно удалить только из надстройки SharePoint, в которой она создана.</span><span class="sxs-lookup"><span data-stu-id="443e0-118">You must grant the SharePoint add-in the following permission(s) or higher. A subscription can only be deleted by the SharePoint add-in that created it.</span></span>

<span data-ttu-id="443e0-119">Область</span><span class="sxs-lookup"><span data-stu-id="443e0-119">Scope</span></span> | <span data-ttu-id="443e0-120">Разрешения</span><span class="sxs-lookup"><span data-stu-id="443e0-120">Permission Rights</span></span> 
------|------------
<span data-ttu-id="443e0-121">Список</span><span class="sxs-lookup"><span data-stu-id="443e0-121">List</span></span>|<span data-ttu-id="443e0-122">Управление</span><span class="sxs-lookup"><span data-stu-id="443e0-122">Manage</span></span>

## <a name="http-request"></a><span data-ttu-id="443e0-123">HTTP-запрос</span><span class="sxs-lookup"><span data-stu-id="443e0-123">HTTP request</span></span>

```
DELETE _api/web/lists('list-id')/subscriptions('id')
```

### <a name="example"></a><span data-ttu-id="443e0-124">Пример</span><span class="sxs-lookup"><span data-stu-id="443e0-124">Example</span></span>

```http
DELETE _api/web/lists('5C77031A-9621-4DFC-BB5D-57803A94E91D')/subscriptions('6D77031A-2345-5GRT-BV3D-55234B56FR43')
```

## <a name="request-body"></a><span data-ttu-id="443e0-125">Текст запроса</span><span class="sxs-lookup"><span data-stu-id="443e0-125">Request body</span></span>

<span data-ttu-id="443e0-126">Не указывайте тело запроса для этого метода.</span><span class="sxs-lookup"><span data-stu-id="443e0-126">Do not supply a request body for this method.</span></span>

## <a name="response"></a><span data-ttu-id="443e0-127">Ответ</span><span class="sxs-lookup"><span data-stu-id="443e0-127">Response</span></span>

<span data-ttu-id="443e0-128">Если подписка найдена и удалена, возвращается ответ `204 No Content`.</span><span class="sxs-lookup"><span data-stu-id="443e0-128">If the subscription is found and successfully deleted, then a `204 No Content` response is returned.</span></span>

### <a name="example"></a><span data-ttu-id="443e0-129">Пример</span><span class="sxs-lookup"><span data-stu-id="443e0-129">Example</span></span>

```http
HTTP/1.1 204 No Content
```

## <a name="see-also"></a><span data-ttu-id="443e0-130">См. также</span><span class="sxs-lookup"><span data-stu-id="443e0-130">See also</span></span>

- [<span data-ttu-id="443e0-131">Веб-перехватчики для списков SharePoint</span><span class="sxs-lookup"><span data-stu-id="443e0-131">SharePoint list webhooks</span></span>](overview-sharepoint-list-webhooks.md)
- [<span data-ttu-id="443e0-132">Обзор веб-перехватчиков SharePoint</span><span class="sxs-lookup"><span data-stu-id="443e0-132">Overview of SharePoint webhooks</span></span>](../overview-sharepoint-webhooks.md)