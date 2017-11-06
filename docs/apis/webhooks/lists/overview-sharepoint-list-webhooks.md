---
title: "Веб-перехватчики для списков SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 81657f3bcaf45eeea4e0999d3c6eb6dfad0407b1
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="sharepoint-list-webhooks"></a><span data-ttu-id="d861e-102">Веб-перехватчики для списков SharePoint</span><span class="sxs-lookup"><span data-stu-id="d861e-102">SharePoint list webhooks</span></span>

<span data-ttu-id="d861e-p101">Веб-перехватчики списков SharePoint обрабатывают события, связанные с изменением элементов в списках или библиотеках документов SharePoint. Веб-перехватчики SharePoint предоставляют простой канал уведомлений, чтобы приложение узнавало об изменениях списка SharePoint, не выполняя опрос службы.</span><span class="sxs-lookup"><span data-stu-id="d861e-p101">The SharePoint list webhooks cover the events corresponding to list item changes for a given SharePoint list or a document library. SharePoint webhooks provide a simple notification pipeline so your application can be aware of changes to a SharePoint list without polling the service.</span></span>

## <a name="tasks"></a><span data-ttu-id="d861e-105">Задачи</span><span class="sxs-lookup"><span data-stu-id="d861e-105">Tasks</span></span>
| <span data-ttu-id="d861e-106">Задача</span><span class="sxs-lookup"><span data-stu-id="d861e-106">Task</span></span>                                                | <span data-ttu-id="d861e-107">Метод HTTP</span><span class="sxs-lookup"><span data-stu-id="d861e-107">HTTP method</span></span>                                                  |
|-----------------------------------------------------|--------------------------------------------------------------|
| [<span data-ttu-id="d861e-108">Создание подписки</span><span class="sxs-lookup"><span data-stu-id="d861e-108">Create a new subscription</span></span>](./create-subscription.md) | `POST    /_api/web/lists('list-guid')/subscriptions`         |
| [<span data-ttu-id="d861e-109">Получение подписок</span><span class="sxs-lookup"><span data-stu-id="d861e-109">Get subscriptions</span></span>](./get-subscription.md)          | `GET     /_api/web/lists('list-guid')/subscriptions`         |
| [<span data-ttu-id="d861e-110">Удаление подписки</span><span class="sxs-lookup"><span data-stu-id="d861e-110">Delete a subscription.</span></span>](./delete-subscription.md)       | `DELETE  /_api/web/lists('list-guid')/subscriptions('id')`   |
| [<span data-ttu-id="d861e-111">Обновление подписки</span><span class="sxs-lookup"><span data-stu-id="d861e-111">Update a subscription</span></span>](./update-subscription.md)     | `PATCH   /_api/web/lists('list-guid')/subscriptions('id')`   |

## <a name="list-event-types"></a><span data-ttu-id="d861e-112">Типы событий списков</span><span class="sxs-lookup"><span data-stu-id="d861e-112">List event types</span></span>
<span data-ttu-id="d861e-113">Приложению будут отправляться уведомления о следующих асинхронных событиях с элементами списков в SharePoint:</span><span class="sxs-lookup"><span data-stu-id="d861e-113">Notifications will be sent to your application for the following asynchronous list item events in SharePoint:</span></span>

* <span data-ttu-id="d861e-114">ItemAdded</span><span class="sxs-lookup"><span data-stu-id="d861e-114">ItemAdded</span></span>
* <span data-ttu-id="d861e-115">ItemUpdated</span><span class="sxs-lookup"><span data-stu-id="d861e-115">ItemUpdated</span></span>
* <span data-ttu-id="d861e-116">ItemDeleted</span><span class="sxs-lookup"><span data-stu-id="d861e-116">ItemDeleted</span></span>
* <span data-ttu-id="d861e-117">ItemCheckedOut</span><span class="sxs-lookup"><span data-stu-id="d861e-117">ItemCheckedOut</span></span>
* <span data-ttu-id="d861e-118">ItemCheckedIn</span><span class="sxs-lookup"><span data-stu-id="d861e-118">ItemCheckedIn</span></span>
* <span data-ttu-id="d861e-119">ItemUncheckedOut</span><span class="sxs-lookup"><span data-stu-id="d861e-119">ItemUncheckedOut</span></span>
* <span data-ttu-id="d861e-120">ItemAttachmentAdded</span><span class="sxs-lookup"><span data-stu-id="d861e-120">ItemAttachmentAdded</span></span>
* <span data-ttu-id="d861e-121">ItemAttachmentDeleted</span><span class="sxs-lookup"><span data-stu-id="d861e-121">ItemAttachmentDeleted</span></span>
* <span data-ttu-id="d861e-122">ItemFileMoved</span><span class="sxs-lookup"><span data-stu-id="d861e-122">ItemFileMoved</span></span>
* <span data-ttu-id="d861e-123">ItemVersionDeleted</span><span class="sxs-lookup"><span data-stu-id="d861e-123">ItemVersionDeleted</span></span>
* <span data-ttu-id="d861e-124">ItemFileConverted</span><span class="sxs-lookup"><span data-stu-id="d861e-124">ItemFileConverted</span></span>

<span data-ttu-id="d861e-125">Веб-перехватчики не поддерживают синхронные события.</span><span class="sxs-lookup"><span data-stu-id="d861e-125">Synchronous events are not supported in webhooks.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d861e-126">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="d861e-126">Additional resources</span></span>

* [<span data-ttu-id="d861e-127">Обзор веб-перехватчиков SharePoint</span><span class="sxs-lookup"><span data-stu-id="d861e-127">Overview of SharePoint webhooks</span></span>](../overview-sharepoint-webhooks.md)
