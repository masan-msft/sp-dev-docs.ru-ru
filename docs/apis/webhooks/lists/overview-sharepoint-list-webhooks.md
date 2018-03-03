---
title: "Веб-перехватчики для списков SharePoint"
description: "Веб-перехватчики списков обрабатывают события, связанные с изменением элементов в списках или библиотеках документов SharePoint."
ms.date: 02/08/2018
ms.prod: sharepoint
ms.openlocfilehash: 085ff54834ea0c9e1e40c25001586b35970d69cf
ms.sourcegitcommit: e157d51378190ddfed6394ba154ce66141c8ca33
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/19/2018
---
# <a name="sharepoint-list-webhooks"></a><span data-ttu-id="45564-103">Веб-перехватчики для списков SharePoint</span><span class="sxs-lookup"><span data-stu-id="45564-103">SharePoint list webhooks</span></span>

<span data-ttu-id="45564-p101">Веб-перехватчики списков SharePoint обрабатывают события, связанные с изменением элементов в списках или библиотеках документов SharePoint. Веб-перехватчики SharePoint предоставляют простой канал уведомлений, чтобы приложение узнавало об изменениях списка SharePoint, не выполняя опрос службы.</span><span class="sxs-lookup"><span data-stu-id="45564-p101">The SharePoint list webhooks cover the events corresponding to list item changes for a given SharePoint list or a document library. SharePoint webhooks provide a simple notification pipeline so your application can be aware of changes to a SharePoint list without polling the service.</span></span>

## <a name="tasks"></a><span data-ttu-id="45564-106">Задачи</span><span class="sxs-lookup"><span data-stu-id="45564-106">Tasks</span></span>

| <span data-ttu-id="45564-107">Задача</span><span class="sxs-lookup"><span data-stu-id="45564-107">Task</span></span>                                                | <span data-ttu-id="45564-108">Метод HTTP</span><span class="sxs-lookup"><span data-stu-id="45564-108">HTTP method</span></span>                                            |     
|-----------------------------------------------------|--------------------------------------------------------|
| [<span data-ttu-id="45564-109">Создание подписки</span><span class="sxs-lookup"><span data-stu-id="45564-109">Create a new subscription</span></span>](./create-subscription.md) | `POST    /_api/web/lists('list-guid')/subscriptions` |
| [<span data-ttu-id="45564-110">Получение подписок</span><span class="sxs-lookup"><span data-stu-id="45564-110">Get subscriptions</span></span>](./get-subscription.md)          | `GET     /_api/web/lists('list-guid')/subscriptions`   |
| [<span data-ttu-id="45564-111">Удаление подписки</span><span class="sxs-lookup"><span data-stu-id="45564-111">Delete a subscription</span></span>](./delete-subscription.md)   | `DELETE  /_api/web/lists('list-guid')/subscriptions('id')`|
| [<span data-ttu-id="45564-112">Обновление подписки</span><span class="sxs-lookup"><span data-stu-id="45564-112">Update a subscription</span></span>](./update-subscription.md)   | `PATCH   /_api/web/lists('list-guid')/subscriptions('id')`|

## <a name="list-event-types"></a><span data-ttu-id="45564-113">Типы событий в списках</span><span class="sxs-lookup"><span data-stu-id="45564-113">List event types</span></span>
<span data-ttu-id="45564-114">Приложению будут отправляться уведомления о следующих асинхронных событиях в элементах списков в SharePoint:</span><span class="sxs-lookup"><span data-stu-id="45564-114">Notifications will be sent to your application for the following asynchronous list item events in SharePoint:</span></span>

* <span data-ttu-id="45564-115">ItemAdded</span><span class="sxs-lookup"><span data-stu-id="45564-115">ItemAdded</span></span>
* <span data-ttu-id="45564-116">ItemUpdated</span><span class="sxs-lookup"><span data-stu-id="45564-116">ItemUpdated</span></span>
* <span data-ttu-id="45564-117">ItemDeleted</span><span class="sxs-lookup"><span data-stu-id="45564-117">ItemDeleted</span></span>
* <span data-ttu-id="45564-118">ItemCheckedOut</span><span class="sxs-lookup"><span data-stu-id="45564-118">ItemCheckedOut</span></span>
* <span data-ttu-id="45564-119">ItemCheckedIn</span><span class="sxs-lookup"><span data-stu-id="45564-119">ItemCheckedIn</span></span>
* <span data-ttu-id="45564-120">ItemUncheckedOut</span><span class="sxs-lookup"><span data-stu-id="45564-120">ItemUncheckedOut</span></span>
* <span data-ttu-id="45564-121">ItemAttachmentAdded</span><span class="sxs-lookup"><span data-stu-id="45564-121">ItemAttachmentAdded</span></span>
* <span data-ttu-id="45564-122">ItemAttachmentDeleted</span><span class="sxs-lookup"><span data-stu-id="45564-122">ItemAttachmentDeleted</span></span>
* <span data-ttu-id="45564-123">ItemFileMoved</span><span class="sxs-lookup"><span data-stu-id="45564-123">ItemFileMoved</span></span>
* <span data-ttu-id="45564-124">ItemVersionDeleted</span><span class="sxs-lookup"><span data-stu-id="45564-124">ItemVersionDeleted</span></span>
* <span data-ttu-id="45564-125">ItemFileConverted</span><span class="sxs-lookup"><span data-stu-id="45564-125">ItemFileConverted</span></span>

<span data-ttu-id="45564-126">Веб-перехватчики не поддерживают синхронные события.</span><span class="sxs-lookup"><span data-stu-id="45564-126">Synchronous events are not supported in webhooks.</span></span>

## <a name="see-also"></a><span data-ttu-id="45564-127">См. также</span><span class="sxs-lookup"><span data-stu-id="45564-127">See also</span></span>

* [<span data-ttu-id="45564-128">Обзор веб-перехватчиков SharePoint</span><span class="sxs-lookup"><span data-stu-id="45564-128">Overview of SharePoint webhooks</span></span>](../overview-sharepoint-webhooks.md)
