---
title: "Обзор веб-перехватчиков SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 519ed85118d4295772c74fcc06ded68110497262
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="overview-of-sharepoint-webhooks"></a><span data-ttu-id="18cd8-102">Обзор веб-перехватчиков SharePoint</span><span class="sxs-lookup"><span data-stu-id="18cd8-102">Overview of SharePoint webhooks</span></span>

<span data-ttu-id="18cd8-103">[Веб-перехватчики](http://en.wikipedia.org/wiki/Webhook) SharePoint позволяют разработчикам создавать приложения, которые подписываются на уведомления о событиях, происходящих в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="18cd8-103">SharePoint [webhooks](http://en.wikipedia.org/wiki/Webhook) enable developers to build applications that subscribe to receive notifications on specific events that occur in SharePoint.</span></span> <span data-ttu-id="18cd8-104">При вызове события SharePoint отправляет подписчику полезные данные HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="18cd8-104">When an event is triggered, SharePoint sends an HTTP POST payload to the subscriber.</span></span> <span data-ttu-id="18cd8-105">Веб-перехватчики легче разрабатывать и использовать, чем службы Windows Communication Foundation (WCF), используемые удаленными приемниками событий в надстройках SharePoint.</span><span class="sxs-lookup"><span data-stu-id="18cd8-105">Webhooks are easier to develop and consume than Windows Communication Foundation (WCF) services used by SharePoint add-in remote event receivers.</span></span> <span data-ttu-id="18cd8-106">Это связано с тем, что веб-перехватчики представляют собой обычные HTTP-службы (веб-API).</span><span class="sxs-lookup"><span data-stu-id="18cd8-106">This is because webhooks are regular HTTP services (web API).</span></span>

<span data-ttu-id="18cd8-107">В настоящее время веб-перехватчики поддерживаются только для элементов списков SharePoint.</span><span class="sxs-lookup"><span data-stu-id="18cd8-107">Currently webhooks are only enabled for SharePoint list items.</span></span> <span data-ttu-id="18cd8-108">Веб-перехватчики элементов списков SharePoint обрабатывают события, связанные с изменением элементов списков для списка или библиотеки документов SharePoint.</span><span class="sxs-lookup"><span data-stu-id="18cd8-108">The SharePoint list webhooks cover the events corresponding to list item changes for a given SharePoint list or a document library. SharePoint webhooks provide a simple notification pipeline so your application can be aware of changes to a SharePoint list without polling the service.</span></span> <span data-ttu-id="18cd8-109">Веб-перехватчики SharePoint предоставляют простой канал уведомлений, чтобы приложение узнавало об изменениях списка SharePoint, не выполняя опрос службы.</span><span class="sxs-lookup"><span data-stu-id="18cd8-109">The SharePoint list webhooks cover the events corresponding to list item changes for a given SharePoint list or a document library. SharePoint webhooks provide a simple notification pipeline so your application can be aware of changes to a SharePoint list without polling the service.</span></span> <span data-ttu-id="18cd8-110">Дополнительные сведения см. в статье [Веб-перехватчики для списков SharePoint](./lists/overview-sharepoint-list-webhooks.md).</span><span class="sxs-lookup"><span data-stu-id="18cd8-110">For more information, see  [SharePoint Add-ins](./lists/overview-sharepoint-list-webhooks.md).</span></span> 

## <a name="creating-webhooks"></a><span data-ttu-id="18cd8-111">Создание веб-перехватчиков</span><span class="sxs-lookup"><span data-stu-id="18cd8-111">Creating webhooks</span></span>
<span data-ttu-id="18cd8-112">Чтобы создать веб-перехватчик SharePoint, необходимо добавить подписку на определенный ресурс SharePoint, например список SharePoint.</span><span class="sxs-lookup"><span data-stu-id="18cd8-112">To create a new SharePoint webhook, you add a new subscription to the specific SharePoint resource, such as a SharePoint list.</span></span> 

<span data-ttu-id="18cd8-113">Для создания подписки необходимы следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="18cd8-113">The following information is required for creating a new subscription:</span></span>

- <span data-ttu-id="18cd8-p103">Ресурс — URL-адрес конечной точки ресурса, для которого создается подписка. Например, это может быть URL-адрес API списков SharePoint.</span><span class="sxs-lookup"><span data-stu-id="18cd8-p103">Resource - The resource endpoint URL you are creating the subscription for. For example a SharePoint List API URL.</span></span>
- <span data-ttu-id="18cd8-p104">URL-адрес уведомления сервера — URL-адрес конечной точки службы. SharePoint будет отправлять запрос HTTP POST к этой конечной точке, когда в указанном ресурсе происходят события.</span><span class="sxs-lookup"><span data-stu-id="18cd8-p104">Server notification URL - Your service endpoint URL. SharePoint will send an HTTP POST to this endpoint when events occur in the specified resource.</span></span>
- <span data-ttu-id="18cd8-p105">Конечная дата — дата окончания срока действия подписки. Срок действия не должен превышать 6 месяцев. По умолчанию срок действия подписки завершается спустя 6 месяцев после ее создания.</span><span class="sxs-lookup"><span data-stu-id="18cd8-p105">Expiration date - The expiration date for your subscription. The expiration date should not be more than 6 months. By default, subscriptions are set to expire 6 months from when they are created.</span></span> 

<span data-ttu-id="18cd8-121">При необходимости вы также можете указать дополнительные сведения:</span><span class="sxs-lookup"><span data-stu-id="18cd8-121">You can also include the following additional information if needed:</span></span>

- <span data-ttu-id="18cd8-p106">Состояние клиента — непрозрачная строка, возвращаемая клиенту при всех уведомлениях. Ее можно использовать для проверки уведомлений, добавления тегов к разным подпискам и других целей.</span><span class="sxs-lookup"><span data-stu-id="18cd8-p106">Client State - An opaque string passed back to the client on all notifications. You can use this for validating notifications, tagging different subscriptions, or other reasons.</span></span>

## <a name="handling-webhook-validation-requests"></a><span data-ttu-id="18cd8-124">Обработка запросов на проверку веб-перехватчиков</span><span class="sxs-lookup"><span data-stu-id="18cd8-124">Handling webhook validation requests</span></span>

<span data-ttu-id="18cd8-p107">При создании подписки SharePoint проверяет, может ли URL-адрес получать уведомления веб-перехватчиков. Эта проверка выполняется при запросе на создание подписки. Подписка будет создана, только если служба своевременно отправит отклик с маркером проверки.</span><span class="sxs-lookup"><span data-stu-id="18cd8-p107">When a new subscription is created, SharePoint will validate whether the notification URL supports receiving webhook notifications. This validation is performed during the subscription creation request. The subscription will only be created if your service responds in a timely manner back with the validation token.</span></span>

### <a name="example-validation-request"></a><span data-ttu-id="18cd8-128">Пример запроса на проверку</span><span class="sxs-lookup"><span data-stu-id="18cd8-128">Example validation request</span></span>

<span data-ttu-id="18cd8-129">При создании подписки SharePoint отправляет запрос HTTP POST на зарегистрированный URL-адрес в формате, подобном следующему:</span><span class="sxs-lookup"><span data-stu-id="18cd8-129">When a new subscription is created, SharePoint will send an HTTP POST request to the registered URL in a format similar to the following example:</span></span>


```http
POST https://contoso.azurewebsites.net/your/webhook/service?validationToken={randomString}
Content-Length: 0
```

### <a name="response"></a><span data-ttu-id="18cd8-130">Отклик</span><span class="sxs-lookup"><span data-stu-id="18cd8-130">Response</span></span>

<span data-ttu-id="18cd8-131">Чтобы подписка была успешно создана, служба должна ответить на запрос, возвращая значение параметра строки запроса **validationToken** в виде обычного текстового отклика.</span><span class="sxs-lookup"><span data-stu-id="18cd8-131">For the subscription to be created successfully, your service must respond to the request by returning the value of the **validationToken** query string parameter as a plain-text response.</span></span>

```http
HTTP/1.1 200 OK
Content-Type: text/plain

{randomString}
```

<span data-ttu-id="18cd8-132">Если приложение возвращает код состояния, отличный от `200`, или не возвращает значение параметра **validationToken**, запрос на создание подписки не выполняется.</span><span class="sxs-lookup"><span data-stu-id="18cd8-132">If your application returns a status code other than `200` or fails to respond with the value of the **validationToken** parameter, the request to create a new subscription will fail.</span></span>

## <a name="receiving-notifications"></a><span data-ttu-id="18cd8-133">Получение уведомлений</span><span class="sxs-lookup"><span data-stu-id="18cd8-133">Receiving notifications</span></span>
<span data-ttu-id="18cd8-p108">Полезные данные уведомления сообщают приложению, что в определенном ресурсе для той или иной подписки произошло событие. Несколько уведомлений для приложения могут быть объединены в один запрос, если за один период времени в ресурсе произошло несколько событий.</span><span class="sxs-lookup"><span data-stu-id="18cd8-p108">The notification payload will inform your application that an event occurred in a given resource for a given subscription. Multiple notifications to your application may be batched together into a single request, if multiple changes occurred in the resource within the same time period.</span></span>

<span data-ttu-id="18cd8-136">Кроме того, полезные данные уведомления содержат состояние клиента, если он использовался при создании подписки.</span><span class="sxs-lookup"><span data-stu-id="18cd8-136">The notification payload body will also contain your client state if you used it when creating the subscription.</span></span>

### <a name="webhook-notification-resource"></a><span data-ttu-id="18cd8-137">Ресурс уведомлений веб-перехватчиков</span><span class="sxs-lookup"><span data-stu-id="18cd8-137">Webhook notification resource</span></span>

<span data-ttu-id="18cd8-138">В ресурсе уведомлений определяется форма данных, предоставляемых службе при отправке запроса уведомления веб-перехватчика SharePoint на зарегистрированный URL-адрес уведомлений.</span><span class="sxs-lookup"><span data-stu-id="18cd8-138">The notification resource defines the shape of the data provided to your service when a SharePoint webhook notification request is submitted to your registered notification URL.</span></span>

#### <a name="json-representation"></a><span data-ttu-id="18cd8-139">Представление JSON</span><span class="sxs-lookup"><span data-stu-id="18cd8-139">JSON representation</span></span>

<span data-ttu-id="18cd8-140">Каждое уведомление, созданное службой, сериализуется в экземпляр **webhookNotifiation**:</span><span class="sxs-lookup"><span data-stu-id="18cd8-140">Each notification generated by the service is serialized into a **webhookNotifiation** instance:</span></span>

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

<span data-ttu-id="18cd8-141">Так как в одном запросе службе может отправляться несколько уведомлений, они объединяются в объект с одним массивом **value**:</span><span class="sxs-lookup"><span data-stu-id="18cd8-141">Since multiple notifications may be submitted to your service in a single request, these are combined together in an object with a single array **value**:</span></span>

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

#### <a name="properties"></a><span data-ttu-id="18cd8-142">Свойства</span><span class="sxs-lookup"><span data-stu-id="18cd8-142">Properties</span></span>

| <span data-ttu-id="18cd8-143">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="18cd8-143">Property Name</span></span>          | <span data-ttu-id="18cd8-144">Тип</span><span class="sxs-lookup"><span data-stu-id="18cd8-144">Type</span></span>              | <span data-ttu-id="18cd8-145">description</span><span class="sxs-lookup"><span data-stu-id="18cd8-145">description</span></span>                                                                                                                         |
|:-----------------------|:------------------|:------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="18cd8-146">**resource**</span><span class="sxs-lookup"><span data-stu-id="18cd8-146">**resource**</span></span>           | <span data-ttu-id="18cd8-147">String</span><span class="sxs-lookup"><span data-stu-id="18cd8-147">String</span></span>            | <span data-ttu-id="18cd8-148">Уникальный идентификатор списка, в котором зарегистрирована подписка.</span><span class="sxs-lookup"><span data-stu-id="18cd8-148">Unique identifier of the list where the subscription is registered.</span></span>                                                                 |
| <span data-ttu-id="18cd8-149">**subscriptionId**</span><span class="sxs-lookup"><span data-stu-id="18cd8-149">**subscriptionId**</span></span>     | <span data-ttu-id="18cd8-150">String</span><span class="sxs-lookup"><span data-stu-id="18cd8-150">String</span></span>            | <span data-ttu-id="18cd8-151">Уникальный идентификатор ресурса подписки</span><span class="sxs-lookup"><span data-stu-id="18cd8-151">The unique identifier for the subscription resource</span></span>                                                                                 |
| <span data-ttu-id="18cd8-152">**clientState**</span><span class="sxs-lookup"><span data-stu-id="18cd8-152">**clientState**</span></span>        | <span data-ttu-id="18cd8-153">String (необязательный)</span><span class="sxs-lookup"><span data-stu-id="18cd8-153">String - optional</span></span> | <span data-ttu-id="18cd8-154">Необязательное строковое значение, возвращаемое в сообщении уведомления для подписки.</span><span class="sxs-lookup"><span data-stu-id="18cd8-154">An optional string value that is passed back in the notification message for this subscription.</span></span>                                     |
| <span data-ttu-id="18cd8-155">**expirationDateTime**</span><span class="sxs-lookup"><span data-stu-id="18cd8-155">**expirationDateTime**</span></span> | <span data-ttu-id="18cd8-156">DateTime</span><span class="sxs-lookup"><span data-stu-id="18cd8-156">DateTime</span></span>          | <span data-ttu-id="18cd8-157">Дата и время окончания срока подписки, если она не будет обновлена или возобновлена.</span><span class="sxs-lookup"><span data-stu-id="18cd8-157">The date and time when the subscription will expire if not updated or renewed.</span></span>                                                      |
| <span data-ttu-id="18cd8-158">**tenantId**</span><span class="sxs-lookup"><span data-stu-id="18cd8-158">**tenantId**</span></span>           | <span data-ttu-id="18cd8-159">String</span><span class="sxs-lookup"><span data-stu-id="18cd8-159">String</span></span>            | <span data-ttu-id="18cd8-160">Уникальный идентификатор клиента, создавшего уведомление.</span><span class="sxs-lookup"><span data-stu-id="18cd8-160">Unique identifier for the tenant which generated this notification.</span></span>                                                                 |
| <span data-ttu-id="18cd8-161">**siteUrl**</span><span class="sxs-lookup"><span data-stu-id="18cd8-161">**siteUrl**</span></span>            | <span data-ttu-id="18cd8-162">String</span><span class="sxs-lookup"><span data-stu-id="18cd8-162">String</span></span>            | <span data-ttu-id="18cd8-163">Относительный (от сервера) URL-адрес сайта, на котором зарегистрирована подписка.</span><span class="sxs-lookup"><span data-stu-id="18cd8-163">Server relative URL of the site where the subscription is registered.</span></span>                                                               |
| <span data-ttu-id="18cd8-164">**webId**</span><span class="sxs-lookup"><span data-stu-id="18cd8-164">**webId**</span></span>              | <span data-ttu-id="18cd8-165">String</span><span class="sxs-lookup"><span data-stu-id="18cd8-165">String</span></span>            | <span data-ttu-id="18cd8-166">Уникальный идентификатор сети, в которой зарегистрирована подписка.</span><span class="sxs-lookup"><span data-stu-id="18cd8-166">Unique identifier of the web where the subscription is registered.</span></span>                                                                  |

#### <a name="example-notification"></a><span data-ttu-id="18cd8-167">Пример уведомления</span><span class="sxs-lookup"><span data-stu-id="18cd8-167">Example notification</span></span>
<span data-ttu-id="18cd8-p109">Текст HTTP-запроса на URL-адрес уведомлений службы содержит уведомление веб-перехватчика. В следующем примере показаны полезные данные одного уведомления:</span><span class="sxs-lookup"><span data-stu-id="18cd8-p109">The body of the HTTP request to your service notification URL will contain a webhook notification. The following example shows a payload with one notification:</span></span>

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

<span data-ttu-id="18cd8-170">Уведомление не включает сведения о вызвавших его изменениях.</span><span class="sxs-lookup"><span data-stu-id="18cd8-170">You'll notice that the notification doesn't include any information about the changes that triggered it.</span></span> <span data-ttu-id="18cd8-171">Ожидается, что при получении уведомления приложение будет использовать для списка [API GetChanges](https://msdn.microsoft.com/EN-US/library/office/dn531433.aspx#bk_ListGetChanges), чтобы запросить коллекцию изменений из журнала изменений и сохранить значение маркера изменений для последующих вызовов.</span><span class="sxs-lookup"><span data-stu-id="18cd8-171">The notification doesn't include any information about the changes that triggered it. Your application is expected to use the [GetChanges API](https://msdn.microsoft.com/EN-US/library/office/dn531433.aspx#bk_ListGetChanges) on the list to query the collection of changes from the change log and store the change token value for any subsequent calls when the application is notified.</span></span>

## <a name="event-types"></a><span data-ttu-id="18cd8-172">Типы событий</span><span class="sxs-lookup"><span data-stu-id="18cd8-172">Event types</span></span>
<span data-ttu-id="18cd8-173">Веб-перехватчики SharePoint поддерживают только асинхронные события.</span><span class="sxs-lookup"><span data-stu-id="18cd8-173">SharePoint webhooks only support asynchronous events.</span></span> <span data-ttu-id="18cd8-174">Это означает, что веб-перехватчики вызываются только после изменения (подобно событиям **-ed**), поэтому использовать синхронные события (**-ing**) невозможно.</span><span class="sxs-lookup"><span data-stu-id="18cd8-174">SharePoint webhooks only support asynchronous events. This means that webhooks are only fired after a change happened (similar to **-ed** events), and thus synchronous (**-ing** events) are not possible.</span></span>

## <a name="error-handling"></a><span data-ttu-id="18cd8-175">Обработка ошибок</span><span class="sxs-lookup"><span data-stu-id="18cd8-175">Error handling</span></span>
<span data-ttu-id="18cd8-p112">Если при отправке уведомления приложению возникает ошибка, SharePoint следует логике экспоненциального отхода. Любой отклик с кодом состояния HTTP, который не находится в диапазоне 200–299, или с истекшим временем ожидания выполняется повторно в течение следующих нескольких минут. Если спустя 15 минут запрос не был успешно выполнен, уведомление отменяется.</span><span class="sxs-lookup"><span data-stu-id="18cd8-p112">If an error occurs while sending the notification to your application, SharePoint will follow exponential back-off logic. Any response with an HTTP status code outside of the 200-299 range, or that times out, will be attempted again over the next several minutes. If the request is not successful after 15 minutes, the notification is dropped.</span></span>

<span data-ttu-id="18cd8-179">Последующие уведомления будут отправляться приложению, но служба может удалить подписку после достаточного количества неудачных попыток.</span><span class="sxs-lookup"><span data-stu-id="18cd8-179">Future notifications will still be attempted to your application, although the service may remove the subscription if a sufficient number of failures are detected.</span></span>

## <a name="expiration"></a><span data-ttu-id="18cd8-180">Срок действия</span><span class="sxs-lookup"><span data-stu-id="18cd8-180">Expiration</span></span>
<span data-ttu-id="18cd8-181">По умолчанию срок действия подписок на веб-перехватчики истекает спустя 6 месяцев, если не указано значение **expirationDateTime**.</span><span class="sxs-lookup"><span data-stu-id="18cd8-181">Webhook subscriptions are set to expire after 6 months by default if an **expirationDateTime** value is not specified.</span></span> 

<span data-ttu-id="18cd8-p113">При создании подписки необходимо указать дату окончания срока действия. Срок действия подписки должен быть меньше 6 месяцев. Ожидается, что приложение будет обрабатывать дату окончания срока действия в соответствии со своими потребностями, периодически обновляя подписку.</span><span class="sxs-lookup"><span data-stu-id="18cd8-p113">You need to set an expiration date when creating the subscription. The expiration date should be less than 6 months. Your application is expected to handle the expiration date according to your application's needs by updating the subscription periodically.</span></span> 

## <a name="retry-mechanism"></a><span data-ttu-id="18cd8-185">Механизм повторных попыток</span><span class="sxs-lookup"><span data-stu-id="18cd8-185">Retry mechanism</span></span>

<span data-ttu-id="18cd8-186">Если в SharePoint происходит событие, а конечная точка службы недоступна (например, во время технического обслуживания), SharePoint повторит попытку отправки уведомления.</span><span class="sxs-lookup"><span data-stu-id="18cd8-186">If an event occurs in SharePoint and your service endpoint is not reachable (e.g., due to maintenance) SharePoint will retry sending the notification.</span></span> <span data-ttu-id="18cd8-187">SharePoint повторяет попытку **5 раз с 5-минутными интервалами**.</span><span class="sxs-lookup"><span data-stu-id="18cd8-187">SharePoint performs a retry of **5 times with a 5 minute wait time** between the attempts.</span></span> <span data-ttu-id="18cd8-188">Если по какой-либо причине служба отключается на продолжительное время, то при следующем включении и вызове от SharePoint метод `GetChanges()` восстановит изменения, пропущенные, пока служба была недоступна.</span><span class="sxs-lookup"><span data-stu-id="18cd8-188">If an event occurs in SharePoint and your service endpoint is not reachable (e.g., due to maintenance) SharePoint will retry sending the notification. SharePoint performs a retry of 5 times with a 5 minute wait time between the attempts. If for some reason your service is down for a longer time, the next time when it's up and gets called by SharePoint, the call to the `GetChanges()` will recover the changes that were missed when your service was not available.</span></span>
