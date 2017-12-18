---
title: "Веб-перехватчики для списков SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 2b3543885de7fcce75694d368667f17dd690592f
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="sharepoint-list-webhooks"></a><span data-ttu-id="2d1d1-102">Веб-перехватчики для списков SharePoint</span><span class="sxs-lookup"><span data-stu-id="2d1d1-102">SharePoint list webhooks</span></span>

<span data-ttu-id="2d1d1-p101">Веб-перехватчики списков SharePoint обрабатывают события, связанные с изменением элементов в списках или библиотеках документов SharePoint. Веб-перехватчики SharePoint предоставляют простой канал уведомлений, чтобы приложение узнавало об изменениях списка SharePoint, не выполняя опрос службы.</span><span class="sxs-lookup"><span data-stu-id="2d1d1-p101">The SharePoint list webhooks cover the events corresponding to list item changes for a given SharePoint list or a document library. SharePoint webhooks provide a simple notification pipeline so your application can be aware of changes to a SharePoint list without polling the service.</span></span>

## <a name="tasks"></a><span data-ttu-id="2d1d1-105">Задачи</span><span class="sxs-lookup"><span data-stu-id="2d1d1-105">Tasks</span></span>
| <span data-ttu-id="2d1d1-106">Задача</span><span class="sxs-lookup"><span data-stu-id="2d1d1-106">Task</span></span>                                                | <span data-ttu-id="2d1d1-107">Метод HTTP</span><span class="sxs-lookup"><span data-stu-id="2d1d1-107">HTTP method</span></span>                                                  |
|-----------------------------------------------------|--------------------------------------------------------------|
| [<span data-ttu-id="2d1d1-108">Создание подписки</span><span class="sxs-lookup"><span data-stu-id="2d1d1-108">Create a new subscription</span></span>](./create-subscription.md) | `POST    /_api/web/lists('list-guid')/subscriptions`         |
| [<span data-ttu-id="2d1d1-109">Получение подписок</span><span class="sxs-lookup"><span data-stu-id="2d1d1-109">Get subscriptions</span></span>](./get-subscription.md)          | `GET     /_api/web/lists('list-guid')/subscriptions`         |
| [<span data-ttu-id="2d1d1-110">Удаление подписки</span><span class="sxs-lookup"><span data-stu-id="2d1d1-110">Delete a subscription</span></span>](./delete-subscription.md)       | `DELETE  /_api/web/lists('list-guid')/subscriptions('id')`   |
| [<span data-ttu-id="2d1d1-111">Обновление подписки</span><span class="sxs-lookup"><span data-stu-id="2d1d1-111">Update a subscription</span></span>](./update-subscription.md)     | `PATCH   /_api/web/lists('list-guid')/subscriptions('id')`   |

## <a name="list-event-types"></a><span data-ttu-id="2d1d1-112">Типы событий списков</span><span class="sxs-lookup"><span data-stu-id="2d1d1-112">List event types</span></span>
<span data-ttu-id="2d1d1-113">Приложению будут отправляться уведомления о следующих асинхронных событиях с элементами списков в SharePoint:</span><span class="sxs-lookup"><span data-stu-id="2d1d1-113">Notifications will be sent to your application for the following asynchronous list item events in SharePoint:</span></span>

* <span data-ttu-id="2d1d1-114">ItemAdded</span><span class="sxs-lookup"><span data-stu-id="2d1d1-114">ItemAdded</span></span>
* <span data-ttu-id="2d1d1-115">ItemUpdated</span><span class="sxs-lookup"><span data-stu-id="2d1d1-115">ItemUpdated</span></span>
* <span data-ttu-id="2d1d1-116">ItemDeleted</span><span class="sxs-lookup"><span data-stu-id="2d1d1-116">ItemDeleted</span></span>
* <span data-ttu-id="2d1d1-117">ItemCheckedOut</span><span class="sxs-lookup"><span data-stu-id="2d1d1-117">ItemCheckedOut</span></span>
* <span data-ttu-id="2d1d1-118">ItemCheckedIn</span><span class="sxs-lookup"><span data-stu-id="2d1d1-118">ItemCheckedIn</span></span>
* <span data-ttu-id="2d1d1-119">ItemUncheckedOut</span><span class="sxs-lookup"><span data-stu-id="2d1d1-119">ItemUncheckedOut</span></span>
* <span data-ttu-id="2d1d1-120">ItemAttachmentAdded</span><span class="sxs-lookup"><span data-stu-id="2d1d1-120">ItemAttachmentAdded</span></span>
* <span data-ttu-id="2d1d1-121">ItemAttachmentDeleted</span><span class="sxs-lookup"><span data-stu-id="2d1d1-121">ItemAttachmentDeleted</span></span>
* <span data-ttu-id="2d1d1-122">ItemFileMoved</span><span class="sxs-lookup"><span data-stu-id="2d1d1-122">ItemFileMoved</span></span>
* <span data-ttu-id="2d1d1-123">ItemVersionDeleted</span><span class="sxs-lookup"><span data-stu-id="2d1d1-123">ItemVersionDeleted</span></span>
* <span data-ttu-id="2d1d1-124">ItemFileConverted</span><span class="sxs-lookup"><span data-stu-id="2d1d1-124">ItemFileConverted</span></span>

<span data-ttu-id="2d1d1-125">Веб-перехватчики не поддерживают синхронные события.</span><span class="sxs-lookup"><span data-stu-id="2d1d1-125">Synchronous events are not supported in webhooks.</span></span>

## <a name="see-also"></a><span data-ttu-id="2d1d1-126">См. также</span><span class="sxs-lookup"><span data-stu-id="2d1d1-126">See also</span></span>

* [<span data-ttu-id="2d1d1-127">Обзор веб-перехватчиков SharePoint</span><span class="sxs-lookup"><span data-stu-id="2d1d1-127">Overview of SharePoint webhooks</span></span>](../overview-sharepoint-webhooks.md)
