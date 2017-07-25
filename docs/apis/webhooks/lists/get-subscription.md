<span data-ttu-id="f7c7b-p102">Надстройке SharePoint необходимо предоставить по крайней мере указанные ниже разрешения. Подписку можно получить только из создавшей ее надстройки SharePoint.</span><span class="sxs-lookup"><span data-stu-id="f7c7b-p102">You must grant the SharePoint add-in the following permission(s) or higher. A subscription can only be retrieved by the SharePoint add-in that created it.</span></span>

Надстройке SharePoint необходимо предоставить по крайней мере указанные ниже разрешения. Подписку можно получить только из создавшей ее надстройки SharePoint. 

<span data-ttu-id="f7c7b-116">Область</span><span class="sxs-lookup"><span data-stu-id="f7c7b-116">Scope</span></span> | <span data-ttu-id="f7c7b-117">Разрешения</span><span class="sxs-lookup"><span data-stu-id="f7c7b-117">Permission Rights</span></span> 
------|------------
<span data-ttu-id="f7c7b-118">Список</span><span class="sxs-lookup"><span data-stu-id="f7c7b-118">List</span></span>|<span data-ttu-id="f7c7b-119">Управление</span><span class="sxs-lookup"><span data-stu-id="f7c7b-119">Manage</span></span>

### <a name="get-all-subscriptions"></a><span data-ttu-id="f7c7b-120">Получение всех подписок</span><span class="sxs-lookup"><span data-stu-id="f7c7b-120">Get all subscriptions</span></span>

<span data-ttu-id="f7c7b-121">У приложения должны быть разрешения на управление списком SharePoint, из которого извлекается подписка.</span><span class="sxs-lookup"><span data-stu-id="f7c7b-121">The application must have manage list permissions to the SharePoint list where the subscription will be retrieved.</span></span>

<span data-ttu-id="f7c7b-122">**Для приложения Microsoft Azure Active Directory (AD):**</span><span class="sxs-lookup"><span data-stu-id="f7c7b-122">**If your application is a Microsoft Azure Active Directory (AD) application:**</span></span>

<span data-ttu-id="f7c7b-123">Приложению Azure AD необходимо предоставить разрешения, указанные в таблице ниже.</span><span class="sxs-lookup"><span data-stu-id="f7c7b-123">You must grant the Azure AD app the permissions specified in the following table.</span></span> 

<span data-ttu-id="f7c7b-124">Приложение</span><span class="sxs-lookup"><span data-stu-id="f7c7b-124">Application</span></span> | <span data-ttu-id="f7c7b-125">Разрешение</span><span class="sxs-lookup"><span data-stu-id="f7c7b-125">Permission</span></span> 
------------|------------
<span data-ttu-id="f7c7b-126">SharePoint Online в Office 365</span><span class="sxs-lookup"><span data-stu-id="f7c7b-126">Office 365 SharePoint Online</span></span>|<span data-ttu-id="f7c7b-127">Полный доступ ко всем семействам веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="f7c7b-127">Have full control of all site collections.</span></span>

<span data-ttu-id="f7c7b-128">**Для надстройки SharePoint**:</span><span class="sxs-lookup"><span data-stu-id="f7c7b-128">**If your application is a SharePoint add-in:**</span></span>

<span data-ttu-id="f7c7b-129">Надстройке SharePoint необходимо предоставить по крайней мере указанные ниже разрешения.</span><span class="sxs-lookup"><span data-stu-id="f7c7b-129">You must grant the SharePoint add-in the following permission(s) or higher.</span></span> 

<span data-ttu-id="f7c7b-130">Область</span><span class="sxs-lookup"><span data-stu-id="f7c7b-130">Scope</span></span> | <span data-ttu-id="f7c7b-131">Разрешения</span><span class="sxs-lookup"><span data-stu-id="f7c7b-131">Permission Rights</span></span> 
------|------------
<span data-ttu-id="f7c7b-132">Список</span><span class="sxs-lookup"><span data-stu-id="f7c7b-132">List</span></span>|<span data-ttu-id="f7c7b-133">Полный доступ</span><span class="sxs-lookup"><span data-stu-id="f7c7b-133">Full control</span></span>

## <a name="http-request"></a><span data-ttu-id="f7c7b-134">HTTP-запрос</span><span class="sxs-lookup"><span data-stu-id="f7c7b-134">HTTP request</span></span>

### <a name="get-a-single-subscription"></a><span data-ttu-id="f7c7b-135">Получение одной подписки</span><span class="sxs-lookup"><span data-stu-id="f7c7b-135">Get a single subscription</span></span>

#### <a name="list-webhook"></a><span data-ttu-id="f7c7b-136">Веб-перехватчик списка</span><span class="sxs-lookup"><span data-stu-id="f7c7b-136">List webhook</span></span>
```
GET _api/web/lists('list-id')/subscriptions('id')
```

##### <a name="example"></a><span data-ttu-id="f7c7b-137">Пример</span><span class="sxs-lookup"><span data-stu-id="f7c7b-137">Example</span></span>

```http
GET _api/web/lists('5C77031A-9621-4DFC-BB5D-57803A94E91D')/subscriptions('6D77031A-2345-5GRT-BV3D-55234B56FR43')
```

#### <a name="request-body"></a><span data-ttu-id="f7c7b-138">Текст запроса</span><span class="sxs-lookup"><span data-stu-id="f7c7b-138">Request body</span></span>

<span data-ttu-id="f7c7b-139">Не указывайте тело запроса для этого метода.</span><span class="sxs-lookup"><span data-stu-id="f7c7b-139">Do not supply a request body for this method.</span></span>

##### <a name="response"></a><span data-ttu-id="f7c7b-140">Отклик</span><span class="sxs-lookup"><span data-stu-id="f7c7b-140">Response</span></span>

<span data-ttu-id="f7c7b-141">Возвращает подписку, которую можно просмотреть в приложении, отправившем вызов.</span><span class="sxs-lookup"><span data-stu-id="f7c7b-141">This returns the subscription viewable by the calling application.</span></span>

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

### <a name="get-all-subscriptions"></a><span data-ttu-id="f7c7b-142">Получение всех подписок</span><span class="sxs-lookup"><span data-stu-id="f7c7b-142">Get all subscriptions</span></span>

#### <a name="list-webhook"></a><span data-ttu-id="f7c7b-143">Веб-перехватчик списка</span><span class="sxs-lookup"><span data-stu-id="f7c7b-143">List webhook</span></span>
```
GET _api/web/lists('list-id')/subscriptions
```

##### <a name="example"></a><span data-ttu-id="f7c7b-144">Пример</span><span class="sxs-lookup"><span data-stu-id="f7c7b-144">Example</span></span>

```http
GET _api/web/lists('5C77031A-9621-4DFC-BB5D-57803A94E91D')/subscriptions
```

#### <a name="request-body"></a><span data-ttu-id="f7c7b-145">Текст запроса</span><span class="sxs-lookup"><span data-stu-id="f7c7b-145">Request body</span></span>

<span data-ttu-id="f7c7b-146">Не указывайте тело запроса для этого метода.</span><span class="sxs-lookup"><span data-stu-id="f7c7b-146">Do not supply a request body for this method.</span></span>

##### <a name="response"></a><span data-ttu-id="f7c7b-147">Отклик</span><span class="sxs-lookup"><span data-stu-id="f7c7b-147">Response</span></span>

<span data-ttu-id="f7c7b-148">Возвращает коллекцию всех подписок в ресурсе SharePoint.</span><span class="sxs-lookup"><span data-stu-id="f7c7b-148">This returns a collection of all subscriptions on a SharePoint resource.</span></span> 

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
