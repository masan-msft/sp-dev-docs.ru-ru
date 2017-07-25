<span data-ttu-id="76f58-p103">Надстройке SharePoint необходимо предоставить по крайней мере следующие разрешения: Подписку можно удалить только из надстройки SharePoint, в которой она создана.</span><span class="sxs-lookup"><span data-stu-id="76f58-p103">You must grant the SharePoint add-in the following permission(s) or higher. A subscription can only be deleted by the SharePoint add-in that created it.</span></span>

Надстройке SharePoint необходимо предоставить по крайней мере следующие разрешения: Подписку можно удалить только из надстройки SharePoint, в которой она создана.

<span data-ttu-id="76f58-116">Область</span><span class="sxs-lookup"><span data-stu-id="76f58-116">Scope</span></span> | <span data-ttu-id="76f58-117">Разрешения</span><span class="sxs-lookup"><span data-stu-id="76f58-117">Permission Rights</span></span> 
------|------------
<span data-ttu-id="76f58-118">Список</span><span class="sxs-lookup"><span data-stu-id="76f58-118">List</span></span>|<span data-ttu-id="76f58-119">Управление</span><span class="sxs-lookup"><span data-stu-id="76f58-119">Manage</span></span>

## <a name="http-request"></a><span data-ttu-id="76f58-120">HTTP-запрос</span><span class="sxs-lookup"><span data-stu-id="76f58-120">HTTP request</span></span>

```
DELETE _api/web/lists('list-id')/subscriptions('id')
```

### <a name="example"></a><span data-ttu-id="76f58-121">Пример</span><span class="sxs-lookup"><span data-stu-id="76f58-121">Example</span></span>

```http
DELETE _api/web/lists('5C77031A-9621-4DFC-BB5D-57803A94E91D')/subscriptions('6D77031A-2345-5GRT-BV3D-55234B56FR43')
```

## <a name="request-body"></a><span data-ttu-id="76f58-122">Текст запроса</span><span class="sxs-lookup"><span data-stu-id="76f58-122">Request body</span></span>

<span data-ttu-id="76f58-123">Не указывайте тело запроса для этого метода.</span><span class="sxs-lookup"><span data-stu-id="76f58-123">Do not supply a request body for this method.</span></span>

## <a name="response"></a><span data-ttu-id="76f58-124">Ответ</span><span class="sxs-lookup"><span data-stu-id="76f58-124">Response</span></span>

<span data-ttu-id="76f58-125">Если подписка найдена и удалена, возвращается ответ `204 No Content`.</span><span class="sxs-lookup"><span data-stu-id="76f58-125">If the subscription is found and successfully deleted, then a `204 No Content` response is returned.</span></span>

### <a name="example"></a><span data-ttu-id="76f58-126">Пример</span><span class="sxs-lookup"><span data-stu-id="76f58-126">Example</span></span>

```http
HTTP/1.1 204 No Content
```
