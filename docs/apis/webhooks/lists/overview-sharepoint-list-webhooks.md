<span data-ttu-id="f5e9c-p101">Веб-перехватчики списков SharePoint обрабатывают события, связанные с изменением элементов в списках или библиотеках документов SharePoint. Веб-перехватчики SharePoint предоставляют простой канал уведомлений, чтобы приложение узнавало об изменениях списка SharePoint, не выполняя опрос службы.</span><span class="sxs-lookup"><span data-stu-id="f5e9c-p101">The SharePoint list webhooks cover the events corresponding to list item changes for a given SharePoint list or a document library. SharePoint webhooks provide a simple notification pipeline so your application can be aware of changes to a SharePoint list without polling the service.</span></span>

Веб-перехватчики списков SharePoint обрабатывают события, связанные с изменением элементов в списках или библиотеках документов SharePoint. Веб-перехватчики SharePoint предоставляют простой канал уведомлений, чтобы приложение узнавало об изменениях списка SharePoint, не выполняя опрос службы.

## <a name="tasks"></a><span data-ttu-id="f5e9c-104">Задачи</span><span class="sxs-lookup"><span data-stu-id="f5e9c-104">Tasks</span></span>
| <span data-ttu-id="f5e9c-105">Задача</span><span class="sxs-lookup"><span data-stu-id="f5e9c-105">Task</span></span>                                                | <span data-ttu-id="f5e9c-106">Метод HTTP</span><span class="sxs-lookup"><span data-stu-id="f5e9c-106">HTTP method</span></span>                                                  |
|-----------------------------------------------------|--------------------------------------------------------------|
| [<span data-ttu-id="f5e9c-107">Создание подписки</span><span class="sxs-lookup"><span data-stu-id="f5e9c-107">Create a new subscription</span></span>](./create-subscription) | `POST    /_api/web/lists('list-guid')/subscriptions`         |
| [<span data-ttu-id="f5e9c-108">Получение подписок</span><span class="sxs-lookup"><span data-stu-id="f5e9c-108">Get subscriptions</span></span>](./get-subscription)          | `GET     /_api/web/lists('list-guid')/subscriptions`         |
| [<span data-ttu-id="f5e9c-109">Удаление подписки</span><span class="sxs-lookup"><span data-stu-id="f5e9c-109">Delete a subscription</span></span>](./delete-subscription)       | `DELETE  /_api/web/lists('list-guid')/subscriptions('id')`   |
| [<span data-ttu-id="f5e9c-110">Обновление подписки</span><span class="sxs-lookup"><span data-stu-id="f5e9c-110">Update a subscription</span></span>](./update-subscription)     | `PATCH   /_api/web/lists('list-guid')/subscriptions('id')`   |

## <a name="list-event-types"></a><span data-ttu-id="f5e9c-111">Типы событий списков</span><span class="sxs-lookup"><span data-stu-id="f5e9c-111">List event types</span></span>
<span data-ttu-id="f5e9c-112">Приложению будут отправляться уведомления о следующих асинхронных событиях с элементами списков в SharePoint:</span><span class="sxs-lookup"><span data-stu-id="f5e9c-112">Notifications will be sent to your application for the following asynchronous list item events in SharePoint:</span></span>

* <span data-ttu-id="f5e9c-113">ItemAdded</span><span class="sxs-lookup"><span data-stu-id="f5e9c-113">ItemAdded</span></span>
* <span data-ttu-id="f5e9c-114">ItemUpdated</span><span class="sxs-lookup"><span data-stu-id="f5e9c-114">ItemUpdated</span></span>
* <span data-ttu-id="f5e9c-115">ItemDeleted</span><span class="sxs-lookup"><span data-stu-id="f5e9c-115">ItemDeleted</span></span>
* <span data-ttu-id="f5e9c-116">ItemCheckedOut</span><span class="sxs-lookup"><span data-stu-id="f5e9c-116">ItemCheckedOut</span></span>
* <span data-ttu-id="f5e9c-117">ItemCheckedIn</span><span class="sxs-lookup"><span data-stu-id="f5e9c-117">ItemCheckedIn</span></span>
* <span data-ttu-id="f5e9c-118">ItemUncheckedOut</span><span class="sxs-lookup"><span data-stu-id="f5e9c-118">ItemUncheckedOut</span></span>
* <span data-ttu-id="f5e9c-119">ItemAttachmentAdded</span><span class="sxs-lookup"><span data-stu-id="f5e9c-119">ItemAttachmentAdded</span></span>
* <span data-ttu-id="f5e9c-120">ItemAttachmentDeleted</span><span class="sxs-lookup"><span data-stu-id="f5e9c-120">ItemAttachmentDeleted</span></span>
* <span data-ttu-id="f5e9c-121">ItemFileMoved</span><span class="sxs-lookup"><span data-stu-id="f5e9c-121">ItemFileMoved</span></span>
* <span data-ttu-id="f5e9c-122">ItemVersionDeleted</span><span class="sxs-lookup"><span data-stu-id="f5e9c-122">ItemVersionDeleted</span></span>
* <span data-ttu-id="f5e9c-123">ItemFileConverted</span><span class="sxs-lookup"><span data-stu-id="f5e9c-123">ItemFileConverted</span></span>

<span data-ttu-id="f5e9c-124">Веб-перехватчики не поддерживают синхронные события.</span><span class="sxs-lookup"><span data-stu-id="f5e9c-124">Synchronous events are not supported in webhooks.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f5e9c-125">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="f5e9c-125">Additional resources</span></span>

* [<span data-ttu-id="f5e9c-126">Обзор веб-перехватчиков SharePoint</span><span class="sxs-lookup"><span data-stu-id="f5e9c-126">Overview of SharePoint webhooks</span></span>](../overview-sharepoint-webhooks)
