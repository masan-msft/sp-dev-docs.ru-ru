---
title: "Обзор веб-перехватчиков SharePoint"
description: "Создавайте приложения, которые подписываются на уведомления о событиях, происходящих в SharePoint."
ms.date: 02/08/2018
ms.prod: sharepoint
ms.openlocfilehash: f6bcdd7f306bb621598996868525db7bb1727161
ms.sourcegitcommit: e157d51378190ddfed6394ba154ce66141c8ca33
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/19/2018
---
# <a name="overview-of-sharepoint-webhooks"></a><span data-ttu-id="1df06-103">Обзор веб-перехватчиков SharePoint</span><span class="sxs-lookup"><span data-stu-id="1df06-103">Overview of SharePoint webhooks</span></span>

<span data-ttu-id="1df06-104">Используя веб-перехватчики SharePoint, разработчики могут создавать приложения, которые подписываются на уведомления о событиях, происходящих в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="1df06-104">SharePoint webhooks enable developers to build applications that subscribe to receive notifications on specific events that occur in SharePoint.</span></span> <span data-ttu-id="1df06-105">При вызове события SharePoint отправляет подписчику полезные данные HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="1df06-105">When an event is triggered, SharePoint sends an HTTP POST payload to the subscriber.</span></span> <span data-ttu-id="1df06-106">Веб-перехватчики легче разрабатывать и задействовать, чем службы Windows Communication Foundation (WCF), используемые удаленными приемниками событий в надстройках SharePoint, так как веб-перехватчики представляют собой обычные HTTP-службы (веб-API).</span><span class="sxs-lookup"><span data-stu-id="1df06-106">Webhooks are easier to develop and consume than Windows Communication Foundation (WCF) services used by SharePoint Add-in remote event receivers because webhooks are regular HTTP services (web API).</span></span>

<span data-ttu-id="1df06-107">В настоящее время веб-перехватчики поддерживаются только для элементов списков SharePoint.</span><span class="sxs-lookup"><span data-stu-id="1df06-107">Currently webhooks are only enabled for SharePoint list items.</span></span> <span data-ttu-id="1df06-108">Веб-перехватчики SharePoint обрабатывают события, связанные с изменением элементов списка или библиотеки документов SharePoint.</span><span class="sxs-lookup"><span data-stu-id="1df06-108">SharePoint list item webhooks cover the events corresponding to list item changes for a given SharePoint list or a document library.</span></span> <span data-ttu-id="1df06-109">Веб-перехватчики SharePoint предоставляют простой канал уведомлений, чтобы приложение узнавало об изменениях списка SharePoint, не выполняя опрос службы.</span><span class="sxs-lookup"><span data-stu-id="1df06-109">SharePoint webhooks provide a simple notification pipeline so your application can be aware of changes to a SharePoint list without polling the service.</span></span> <span data-ttu-id="1df06-110">Дополнительные сведения см. в статье [Веб-перехватчики для списков SharePoint](./lists/overview-sharepoint-list-webhooks.md).</span><span class="sxs-lookup"><span data-stu-id="1df06-110">For more information see [SharePoint list webhooks](./lists/overview-sharepoint-list-webhooks.md).</span></span> 

## <a name="creating-webhooks"></a><span data-ttu-id="1df06-111">Создание веб-перехватчиков</span><span class="sxs-lookup"><span data-stu-id="1df06-111">Creating webhooks</span></span>

<span data-ttu-id="1df06-112">Чтобы создать веб-перехватчик SharePoint, необходимо добавить подписку на определенный ресурс SharePoint, например список SharePoint.</span><span class="sxs-lookup"><span data-stu-id="1df06-112">To create a new SharePoint webhook, you add a new subscription to the specific SharePoint resource, such as a SharePoint list.</span></span> 

<span data-ttu-id="1df06-113">Для создания подписки необходимы следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="1df06-113">The following information is required for creating a new subscription:</span></span>

- <span data-ttu-id="1df06-p103">**Ресурс**. URL-адрес конечной точки ресурса, для которого создается подписка. Например, это может быть URL-адрес API списка SharePoint.</span><span class="sxs-lookup"><span data-stu-id="1df06-p103">Resource - The resource endpoint URL you are creating the subscription for. For example a SharePoint List API URL.</span></span>
- <span data-ttu-id="1df06-117">**Серверный URL-адрес уведомлений**.</span><span class="sxs-lookup"><span data-stu-id="1df06-117">**Server notification UR**.</span></span> <span data-ttu-id="1df06-118">URL-адрес конечной точки службы.</span><span class="sxs-lookup"><span data-stu-id="1df06-118">Your service endpoint URL.</span></span> <span data-ttu-id="1df06-119">SharePoint отправляет запрос HTTP POST в эту конечную точку, когда в указанном ресурсе происходят события.</span><span class="sxs-lookup"><span data-stu-id="1df06-119">Server notification URL - Your service endpoint URL. SharePoint will send an HTTP POST to this endpoint when events occur in the specified resource.</span></span>
- <span data-ttu-id="1df06-120">**Срок действия**.</span><span class="sxs-lookup"><span data-stu-id="1df06-120">**Expiration Date**</span></span> <span data-ttu-id="1df06-121">Дата окончания срока действия подписки.</span><span class="sxs-lookup"><span data-stu-id="1df06-121">The expiration date for your subscription.</span></span> <span data-ttu-id="1df06-122">Срок действия не должен превышать 6 месяцев.</span><span class="sxs-lookup"><span data-stu-id="1df06-122">The expiration date should not be more than 6 months.</span></span> <span data-ttu-id="1df06-123">По умолчанию срок действия подписки истекает через 6 месяцев после ее создания.</span><span class="sxs-lookup"><span data-stu-id="1df06-123">By default, subscriptions are set to expire 6 months from when they are created.</span></span> 

<span data-ttu-id="1df06-124">При необходимости вы также можете указать следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="1df06-124">You can also include the following additional information if needed:</span></span>

- <span data-ttu-id="1df06-125">**Состояние клиента**.</span><span class="sxs-lookup"><span data-stu-id="1df06-125">**Client State**.</span></span> <span data-ttu-id="1df06-126">Непрозрачная строка, которая передается клиенту со всеми уведомлениями.</span><span class="sxs-lookup"><span data-stu-id="1df06-126">An opaque string passed back to the client on all notifications.</span></span> <span data-ttu-id="1df06-127">Ее можно использовать для проверки уведомлений, добавления тегов к подпискам и других целей.</span><span class="sxs-lookup"><span data-stu-id="1df06-127">Client State - An opaque string passed back to the client on all notifications. You can use this for validating notifications, tagging different subscriptions, or other reasons.</span></span>

## <a name="handling-webhook-validation-requests"></a><span data-ttu-id="1df06-128">Обработка запросов на проверку веб-перехватчиков</span><span class="sxs-lookup"><span data-stu-id="1df06-128">Handling webhook validation requests</span></span>

<span data-ttu-id="1df06-129">При создании подписки SharePoint проверяет, поддерживает ли указанный URL-адрес получение уведомлений веб-перехватчиков.</span><span class="sxs-lookup"><span data-stu-id="1df06-129">When a new subscription is created, SharePoint validates whether the notification URL supports receiving webhook notifications.</span></span> <span data-ttu-id="1df06-130">Эта проверка выполняется при запросе на создание подписки.</span><span class="sxs-lookup"><span data-stu-id="1df06-130">This validation is performed during the subscription creation request.</span></span> <span data-ttu-id="1df06-131">Подписка будет создана, только если служба своевременно отправит ответ с маркером проверки.</span><span class="sxs-lookup"><span data-stu-id="1df06-131">The subscription is only created if your service responds in a timely manner back with the validation token.</span></span>

### <a name="example-validation-request"></a><span data-ttu-id="1df06-132">Пример запроса на проверку</span><span class="sxs-lookup"><span data-stu-id="1df06-132">Example validation request</span></span>

<span data-ttu-id="1df06-133">При создании подписки SharePoint отправляет запрос HTTP POST на зарегистрированный URL-адрес в формате, подобном следующему:</span><span class="sxs-lookup"><span data-stu-id="1df06-133">When a new subscription is created, SharePoint will send an HTTP POST request to the registered URL in a format similar to the following example:</span></span>


```http
POST https://contoso.azurewebsites.net/your/webhook/service?validationToken={randomString}
Content-Length: 0
```

### <a name="response"></a><span data-ttu-id="1df06-134">Ответ</span><span class="sxs-lookup"><span data-stu-id="1df06-134">Response</span></span>

<span data-ttu-id="1df06-135">Чтобы подписка была успешно создана, служба должна ответить на запрос, возвращая значение параметра строки запроса **validationToken** в виде обычного текстового отклика.</span><span class="sxs-lookup"><span data-stu-id="1df06-135">For the subscription to be created successfully, your service must respond to the request by returning the value of the **validationToken** query string parameter as a plain-text response.</span></span>

```http
HTTP/1.1 200 OK
Content-Type: text/plain

{randomString}
```

<span data-ttu-id="1df06-136">Если приложение возвращает код состояния, отличный от `200`, или не возвращает значение параметра **validationToken**, запрос на создание подписки не выполняется.</span><span class="sxs-lookup"><span data-stu-id="1df06-136">If your application returns a status code other than `200` or fails to respond with the value of the **validationToken** parameter, the request to create a new subscription will fail.</span></span>

## <a name="receiving-notifications"></a><span data-ttu-id="1df06-137">Получение уведомлений</span><span class="sxs-lookup"><span data-stu-id="1df06-137">Receiving notifications</span></span>

<span data-ttu-id="1df06-138">Полезные данные уведомления сообщают приложению, что в определенном ресурсе для той или иной подписки произошло событие.</span><span class="sxs-lookup"><span data-stu-id="1df06-138">The notification payload informs your application that an event occurred in a given resource for a given subscription.</span></span> <span data-ttu-id="1df06-139">Несколько уведомлений для приложения могут быть объединены в один запрос, если за один период времени в ресурсе произошло несколько событий.</span><span class="sxs-lookup"><span data-stu-id="1df06-139">The notification payload will inform your application that an event occurred in a given resource for a given subscription. Multiple notifications to your application may be batched together into a single request, if multiple changes occurred in the resource within the same time period.</span></span>

<span data-ttu-id="1df06-140">Кроме того, полезные данные уведомления содержат состояние клиента, если он использовался при создании подписки.</span><span class="sxs-lookup"><span data-stu-id="1df06-140">The notification payload body will also contain your client state if you used it when creating the subscription.</span></span>

### <a name="webhook-notification-resource"></a><span data-ttu-id="1df06-141">Ресурс уведомлений веб-перехватчиков</span><span class="sxs-lookup"><span data-stu-id="1df06-141">Webhook notification resource</span></span>

<span data-ttu-id="1df06-142">В ресурсе уведомлений определяется форма данных, предоставляемых службе при отправке запроса уведомления веб-перехватчика SharePoint на зарегистрированный URL-адрес уведомлений.</span><span class="sxs-lookup"><span data-stu-id="1df06-142">The notification resource defines the shape of the data provided to your service when a SharePoint webhook notification request is submitted to your registered notification URL.</span></span>

#### <a name="json-representation"></a><span data-ttu-id="1df06-143">Представление JSON</span><span class="sxs-lookup"><span data-stu-id="1df06-143">JSON representation</span></span>

<span data-ttu-id="1df06-144">Каждое уведомление, созданное службой, сериализуется в экземпляр **webhookNotifiation**:</span><span class="sxs-lookup"><span data-stu-id="1df06-144">Each notification generated by the service is serialized into a **webhookNotifiation** instance:</span></span>

```json
{
    "subscriptionId":"91779246-afe9-4525-b122-6c199ae89211",
    "clientState":"00000000-0000-0000-0000-000000000000",
    "expirationDateTime":"2016-04-30T17:27:00.0000000Z",
    "resource":"b9f6f714-9df8-470b-b22e-653855e1c181",
    "tenantId":"00000000-0000-0000-0000-000000000000",
    "siteUrl":"/",
    "webId":"dbc5a806-e4d4-46e5-951c-6344d70b62fa"
}
```

<br/>

<span data-ttu-id="1df06-145">Так как в одном запросе службе может отправляться несколько уведомлений, они объединяются в объект с одним массивом **value**:</span><span class="sxs-lookup"><span data-stu-id="1df06-145">Since multiple notifications may be submitted to your service in a single request, these are combined together in an object with a single array **value**:</span></span>

```json
{
   "value":[
      {
         "subscriptionId":"91779246-afe9-4525-b122-6c199ae89211",
         "clientState":"00000000-0000-0000-0000-000000000000",
         "expirationDateTime":"2016-04-30T17:27:00.0000000Z",
         "resource":"b9f6f714-9df8-470b-b22e-653855e1c181",
         "tenantId":"00000000-0000-0000-0000-000000000000",
         "siteUrl":"/",
         "webId":"dbc5a806-e4d4-46e5-951c-6344d70b62fa"
      }
   ]
}
```


#### <a name="properties"></a><span data-ttu-id="1df06-146">Свойства</span><span class="sxs-lookup"><span data-stu-id="1df06-146">Properties</span></span>

| <span data-ttu-id="1df06-147">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="1df06-147">Property name</span></span>          | <span data-ttu-id="1df06-148">Тип</span><span class="sxs-lookup"><span data-stu-id="1df06-148">Type</span></span>              | <span data-ttu-id="1df06-149">Описание</span><span class="sxs-lookup"><span data-stu-id="1df06-149">Description</span></span>                                                                                                                         |
|:---------------------  |:------------------|----------------|
| <span data-ttu-id="1df06-150">**resource**</span><span class="sxs-lookup"><span data-stu-id="1df06-150">**resource**</span></span>           | <span data-ttu-id="1df06-151">String</span><span class="sxs-lookup"><span data-stu-id="1df06-151">String</span></span>            | <span data-ttu-id="1df06-152">Уникальный идентификатор списка, в котором зарегистрирована подписка.</span><span class="sxs-lookup"><span data-stu-id="1df06-152">Unique identifier of the list where the subscription is registered.</span></span> |
| <span data-ttu-id="1df06-153">**subscriptionId**</span><span class="sxs-lookup"><span data-stu-id="1df06-153">**subscriptionId**</span></span>     | <span data-ttu-id="1df06-154">Строка</span><span class="sxs-lookup"><span data-stu-id="1df06-154">String</span></span>            | <span data-ttu-id="1df06-155">Уникальный идентификатор ресурса подписки.</span><span class="sxs-lookup"><span data-stu-id="1df06-155">The unique identifier for the subscription resource.</span></span>                |
| <span data-ttu-id="1df06-156">**clientState**</span><span class="sxs-lookup"><span data-stu-id="1df06-156">**clientState**</span></span>        | <span data-ttu-id="1df06-157">Строка (необязательный)</span><span class="sxs-lookup"><span data-stu-id="1df06-157">String - optional</span></span> | <span data-ttu-id="1df06-158">Необязательное строковое значение, возвращаемое в</span><span class="sxs-lookup"><span data-stu-id="1df06-158">An optional string value that is passed back in the notification message for this subscription.</span></span> <span data-ttu-id="1df06-159">уведомлении для подписки.</span><span class="sxs-lookup"><span data-stu-id="1df06-159">message for this subscription.</span></span> |
| <span data-ttu-id="1df06-160">**expirationDateTime**</span><span class="sxs-lookup"><span data-stu-id="1df06-160">**expirationDateTime**</span></span> | <span data-ttu-id="1df06-161">DateTime</span><span class="sxs-lookup"><span data-stu-id="1df06-161">DateTime</span></span>          | <span data-ttu-id="1df06-162">Дата и время окончания срока действия подписки, если она не будет обновлена или возобновлена.</span><span class="sxs-lookup"><span data-stu-id="1df06-162">The date and time when the subscription will expire if not updated or renewed.</span></span> |
| <span data-ttu-id="1df06-163">**tenantId**</span><span class="sxs-lookup"><span data-stu-id="1df06-163">**tenantId**</span></span>           | <span data-ttu-id="1df06-164">Строка</span><span class="sxs-lookup"><span data-stu-id="1df06-164">String</span></span>            | <span data-ttu-id="1df06-165">Уникальный идентификатор клиента, создавшего это уведомление.</span><span class="sxs-lookup"><span data-stu-id="1df06-165">Unique identifier for the tenant which generated this notification.</span></span>   |
| <span data-ttu-id="1df06-166">**siteUrl**</span><span class="sxs-lookup"><span data-stu-id="1df06-166">**siteUrl**</span></span>            | <span data-ttu-id="1df06-167">String</span><span class="sxs-lookup"><span data-stu-id="1df06-167">String</span></span>            | <span data-ttu-id="1df06-168">Относительный (от сервера) URL-адрес сайта, на котором зарегистрирована подписка.</span><span class="sxs-lookup"><span data-stu-id="1df06-168">Server relative URL of the site where the subscription is registered.</span></span>|
| <span data-ttu-id="1df06-169">**webId**</span><span class="sxs-lookup"><span data-stu-id="1df06-169">**webId**</span></span>              | <span data-ttu-id="1df06-170">String</span><span class="sxs-lookup"><span data-stu-id="1df06-170">String</span></span>            | <span data-ttu-id="1df06-171">Уникальный идентификатор сети, в которой зарегистрирована подписка.</span><span class="sxs-lookup"><span data-stu-id="1df06-171">Unique identifier of the web where the subscription is registered.</span></span>   |

#### <a name="example-notification"></a><span data-ttu-id="1df06-172">Пример уведомления</span><span class="sxs-lookup"><span data-stu-id="1df06-172">Example notification</span></span>

<span data-ttu-id="1df06-173">Текст HTTP-запроса на URL-адрес уведомлений службы содержит уведомление веб-перехватчика.</span><span class="sxs-lookup"><span data-stu-id="1df06-173">The body of the HTTP request to your service notification URL will contain a webhook notification. The following example shows a payload with one notification:</span></span> <span data-ttu-id="1df06-174">В следующем примере показаны полезные данные одного уведомления:</span><span class="sxs-lookup"><span data-stu-id="1df06-174">The following example shows a payload with one notification:</span></span>

```json
{
   "value":[
      {
         "subscriptionId":"91779246-afe9-4525-b122-6c199ae89211",
         "clientState":"00000000-0000-0000-0000-000000000000",
         "expirationDateTime":"2016-04-30T17:27:00.0000000Z",
         "resource":"b9f6f714-9df8-470b-b22e-653855e1c181",
         "tenantId":"00000000-0000-0000-0000-000000000000",
         "siteUrl":"/",
         "webId":"dbc5a806-e4d4-46e5-951c-6344d70b62fa"
      }
   ]
}
```

<span data-ttu-id="1df06-175">Уведомление не включает сведения о вызвавших его изменениях.</span><span class="sxs-lookup"><span data-stu-id="1df06-175">The notification doesn't include any information about the changes that triggered it.</span></span> <span data-ttu-id="1df06-176">Ожидается, что при получении уведомления приложение будет использовать для списка [API GetChanges](https://msdn.microsoft.com/ru-RU/library/office/dn531433.aspx#bk_ListGetChanges), чтобы запросить коллекцию изменений из журнала изменений и сохранить значение маркера изменений для последующих вызовов.</span><span class="sxs-lookup"><span data-stu-id="1df06-176">Your application is expected to use the [GetChanges API](https://msdn.microsoft.com/ru-RU/library/office/dn531433.aspx#bk_ListGetChanges) on the list to query the collection of changes from the change log and store the change token value for any subsequent calls when the application is notified.</span></span>

## <a name="event-types"></a><span data-ttu-id="1df06-177">Типы событий</span><span class="sxs-lookup"><span data-stu-id="1df06-177">Event types</span></span>

<span data-ttu-id="1df06-178">Веб-перехватчики SharePoint поддерживают только асинхронные события.</span><span class="sxs-lookup"><span data-stu-id="1df06-178">SharePoint webhooks only support asynchronous events.</span></span> <span data-ttu-id="1df06-179">Это означает, что веб-перехватчики вызываются только после изменения (подобно событиям **-ed**), поэтому использовать синхронные события (**-ing**) невозможно.</span><span class="sxs-lookup"><span data-stu-id="1df06-179">This means that webhooks are only fired after a change happened (similar to **-ed** events), and thus synchronous (**-ing** events) are not possible.</span></span>

## <a name="error-handling"></a><span data-ttu-id="1df06-180">Обработка ошибок</span><span class="sxs-lookup"><span data-stu-id="1df06-180">Error handling</span></span>

<span data-ttu-id="1df06-181">Если при отправке уведомления приложению возникает ошибка, SharePoint пытается доставить его еще 5 раз.</span><span class="sxs-lookup"><span data-stu-id="1df06-181">If an error occurs while sending the notification to your application, SharePoint will retry up to 5 times to deliver the notification.</span></span> <span data-ttu-id="1df06-182">Любой ответ с кодом состояния HTTP, который не находится в диапазоне 200–299, или с истекшим временем ожидания выполняется повторно через 5 минут.</span><span class="sxs-lookup"><span data-stu-id="1df06-182">Any response with an HTTP status code outside of the 200-299 range, or that times out, will be attempted again 5 minute later.</span></span> <span data-ttu-id="1df06-183">Если все 5 попыток выполнить запрос ни к чему не привели, уведомление удаляется.</span><span class="sxs-lookup"><span data-stu-id="1df06-183">If the request is not successful after 5 attempts, the notification is dropped.</span></span> <span data-ttu-id="1df06-184">В дальнейшем попытки доставить уведомления приложению будут повторяться.</span><span class="sxs-lookup"><span data-stu-id="1df06-184">Future notifications will still be attempted to your application.</span></span>

## <a name="expiration"></a><span data-ttu-id="1df06-185">Срок действия</span><span class="sxs-lookup"><span data-stu-id="1df06-185">Expiration</span></span>

<span data-ttu-id="1df06-186">По умолчанию срок действия подписок на веб-перехватчики истекает спустя 6 месяцев, если не указано значение **expirationDateTime**.</span><span class="sxs-lookup"><span data-stu-id="1df06-186">Webhook subscriptions are set to expire after 6 months by default if an **expirationDateTime** value is not specified.</span></span> 

<span data-ttu-id="1df06-p114">При создании подписки необходимо указать дату окончания срока действия. Срок действия подписки должен быть меньше 6 месяцев. Ожидается, что приложение будет обрабатывать дату окончания срока действия в соответствии со своими потребностями, периодически обновляя подписку.</span><span class="sxs-lookup"><span data-stu-id="1df06-p114">You need to set an expiration date when creating the subscription. The expiration date should be less than 6 months. Your application is expected to handle the expiration date according to your application's needs by updating the subscription periodically.</span></span> 

## <a name="retry-mechanism"></a><span data-ttu-id="1df06-190">Механизм повтора</span><span class="sxs-lookup"><span data-stu-id="1df06-190">Retry mechanism</span></span>

<span data-ttu-id="1df06-191">Если в SharePoint происходит событие, а конечная точка службы недоступна (например, во время технического обслуживания), SharePoint пытается отправить уведомление еще раз.</span><span class="sxs-lookup"><span data-stu-id="1df06-191">If an event occurs in SharePoint and your service endpoint is not reachable (e.g., due to maintenance) SharePoint will retry sending the notification.</span></span> <span data-ttu-id="1df06-192">SharePoint повторяет попытку **5 раз с 5-минутными интервалами**.</span><span class="sxs-lookup"><span data-stu-id="1df06-192">SharePoint performs a retry of **5 times with a 5 minute wait time** between the attempts.</span></span> <span data-ttu-id="1df06-193">Если по той или иной причине служба недоступна дольше этого времени, то при следующем включении и вызове от SharePoint вызов метода `GetChanges()` восстанавливает пропущенные изменения.</span><span class="sxs-lookup"><span data-stu-id="1df06-193">If for some reason your service is down for a longer time, the next time when it's up and gets called by SharePoint, the call to the `GetChanges()` will recover the changes that were missed when your service was not available.</span></span>
