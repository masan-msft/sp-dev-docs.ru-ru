---
title: "Удаление подписки"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 553a20757c0849f5033bc3345c4645f1754945bc
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="delete-a-subscription"></a><span data-ttu-id="30529-102">Удаление подписки</span><span class="sxs-lookup"><span data-stu-id="30529-102">Delete a subscription</span></span>

<span data-ttu-id="30529-p101">Удаляет подписку на веб-перехватчики из списка SharePoint. После удаления доставка уведомлений по подписке прекратится.</span><span class="sxs-lookup"><span data-stu-id="30529-p101">Deletes a webhook subscription from a SharePoint list. After deleting the subscription notifications will no longer be delivered.</span></span>

## <a name="permissions"></a><span data-ttu-id="30529-105">Permissions</span><span class="sxs-lookup"><span data-stu-id="30529-105">Permissions</span></span>

<span data-ttu-id="30529-106">У приложения должно быть разрешение на изменение списка SharePoint, из которого удаляется подписка.</span><span class="sxs-lookup"><span data-stu-id="30529-106">The application must have at least edit permissions to the SharePoint list where the subscription will be deleted.</span></span>

<span data-ttu-id="30529-107">**Для приложения Microsoft Azure Active Directory (AD):**</span><span class="sxs-lookup"><span data-stu-id="30529-107">**If your application is a Microsoft Azure Active Directory (AD) application:**</span></span>

<span data-ttu-id="30529-p102">Приложению Azure AD необходимо предоставить разрешения, указанные в таблице ниже. Подписку можно удалить только из приложения Azure AD, в котором она создана.</span><span class="sxs-lookup"><span data-stu-id="30529-p102">You must grant the Azure AD app the permissions specified in the following table. A subscription can only be deleted by the Azure AD application that created it.</span></span>

<span data-ttu-id="30529-110">Приложение</span><span class="sxs-lookup"><span data-stu-id="30529-110">Application</span></span> | <span data-ttu-id="30529-111">Разрешение</span><span class="sxs-lookup"><span data-stu-id="30529-111">Permission</span></span> 
------------|------------
<span data-ttu-id="30529-112">SharePoint Online в Office 365</span><span class="sxs-lookup"><span data-stu-id="30529-112">Office 365 SharePoint Online</span></span>|<span data-ttu-id="30529-113">Чтение и запись элементов и списков во всех семействах веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="30529-113">Read and write items and lists in all site collections.</span></span>

<span data-ttu-id="30529-114">**Для надстройки SharePoint**:</span><span class="sxs-lookup"><span data-stu-id="30529-114">**If your application is a SharePoint add-in:**</span></span>

<span data-ttu-id="30529-p103">Надстройке SharePoint необходимо предоставить по крайней мере следующие разрешения: Подписку можно удалить только из надстройки SharePoint, в которой она создана.</span><span class="sxs-lookup"><span data-stu-id="30529-p103">You must grant the SharePoint add-in the following permission(s) or higher. A subscription can only be deleted by the SharePoint add-in that created it.</span></span>

<span data-ttu-id="30529-117">Область</span><span class="sxs-lookup"><span data-stu-id="30529-117">Scope</span></span> | <span data-ttu-id="30529-118">Разрешения</span><span class="sxs-lookup"><span data-stu-id="30529-118">Permission Rights</span></span> 
------|------------
<span data-ttu-id="30529-119">Список</span><span class="sxs-lookup"><span data-stu-id="30529-119">List</span></span>|<span data-ttu-id="30529-120">Управление</span><span class="sxs-lookup"><span data-stu-id="30529-120">Manage</span></span>

## <a name="http-request"></a><span data-ttu-id="30529-121">HTTP-запрос</span><span class="sxs-lookup"><span data-stu-id="30529-121">HTTP request</span></span>

```
DELETE _api/web/lists('list-id')/subscriptions('id')
```

### <a name="example"></a><span data-ttu-id="30529-122">Пример</span><span class="sxs-lookup"><span data-stu-id="30529-122">Example</span></span>

```http
DELETE _api/web/lists('5C77031A-9621-4DFC-BB5D-57803A94E91D')/subscriptions('6D77031A-2345-5GRT-BV3D-55234B56FR43')
```

## <a name="request-body"></a><span data-ttu-id="30529-123">Текст запроса</span><span class="sxs-lookup"><span data-stu-id="30529-123">Request body</span></span>

<span data-ttu-id="30529-124">Не указывайте тело запроса для этого метода.</span><span class="sxs-lookup"><span data-stu-id="30529-124">Do not supply a request body for this method.</span></span>

## <a name="response"></a><span data-ttu-id="30529-125">Ответ</span><span class="sxs-lookup"><span data-stu-id="30529-125">Response</span></span>

<span data-ttu-id="30529-126">Если подписка найдена и удалена, возвращается ответ `204 No Content`.</span><span class="sxs-lookup"><span data-stu-id="30529-126">If the subscription is found and successfully deleted, then a `204 No Content` response is returned.</span></span>

### <a name="example"></a><span data-ttu-id="30529-127">Пример</span><span class="sxs-lookup"><span data-stu-id="30529-127">Example</span></span>

```http
HTTP/1.1 204 No Content
```
