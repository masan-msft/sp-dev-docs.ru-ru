# <a name="working-with-requestdigest"></a><span data-ttu-id="27961-101">Работа с __REQUESTDIGEST</span><span class="sxs-lookup"><span data-stu-id="27961-101">Working with __REQUESTDIGEST</span></span>

<span data-ttu-id="27961-p101">При выполнении запросов REST к API SharePoint (всех, кроме GET) в них необходимо добавлять действительный дайджест. Он подтверждает действительность вашего запроса к SharePoint. Так как срок действия этого токена ограничен, его необходимо проверить, прежде чем добавлять в запрос, иначе возникнет ошибка. В этой статье описано, как получить действительный дайджест запроса и избежать ошибок.</span><span class="sxs-lookup"><span data-stu-id="27961-p101">When executing non-GET REST requests to the SharePoint API, you must add a valid request digest to your request. This digest proves validity of your request to SharePoint. Because this token is valid only for a limited period of time, you have to ensure that the token you have is valid, before adding it to your request or the request will fail. This article describes the different approaches to obtain a valid request digest and pitfalls of some commonly used approaches.</span></span>

## <a name="considerations-when-using-request-digest-from-the-hidden-requestdigest-field"></a><span data-ttu-id="27961-106">Что следует учитывать при использовании дайджеста запроса из скрытого поля __REQUESTDIGEST</span><span class="sxs-lookup"><span data-stu-id="27961-106">Considerations when using request digest from the hidden __REQUESTDIGEST field</span></span>

<span data-ttu-id="27961-p102">На классических страницах SharePoint включает токен дайджеста запроса в скрытом поле **__REQUESTDIGEST**. Один из наиболее распространенных способов работы с дайджестом запроса — извлечение его из этого поля и добавление в запрос, например:</span><span class="sxs-lookup"><span data-stu-id="27961-p102">In classic pages, SharePoint includes a request digest token on the page in a hidden field named **__REQUESTDIGEST**. One of the most common approaches to work with the request digest, is to obtain it from that field and add it to the request, for example:</span></span>

```js
var digest = $('#__REQUESTDIGEST').val();
$.ajax({
    url: '/_api/web/...'
    method: "POST",
    headers: {
        "Accept": "application/json; odata=nometadata",
        "X-RequestDigest": digest
    },
    success: function (data) {
      // ...
    },
    error: function (data, errorCode, errorMessage) {
      // ...
    }
});
```

<span data-ttu-id="27961-p103">Первоначально такой запрос будет работать, но если страница будет открыта в течение долгого времени, срок действия дайджеста запроса истечет и возникнет ошибка **403 FORBIDDEN**. По умолчанию токен дайджеста запроса действителен в течение 30 минут, поэтому перед использованием его необходимо проверить. Раньше для этого нужно было сравнить метку времени из дайджеста запроса с текущим временем. SharePoint Framework упрощает этот процесс. Проверить токен дайджеста запроса можно двумя способами.</span><span class="sxs-lookup"><span data-stu-id="27961-p103">Such request would work initially, but if the user would have the page open for a longer period of time, the request digest on the page would expire and the request would fail with a **403 FORBIDDEN** result. By default, a request digest token is valid for 30 minutes, so before using it, you have to ensure that it's still valid. In the past you had to do this manually, by comparing the timestamp from the request digest with the current time. SharePoint Framework simplifies this process by offering you two ways of ensuring that your request has a valid request digest token.</span></span>

## <a name="use-the-sphttpclient-to-communicate-with-the-sharepoint-rest-api"></a><span data-ttu-id="27961-113">Использование SPHttpClient для связи с REST API SharePoint</span><span class="sxs-lookup"><span data-stu-id="27961-113">Use the SPHttpClient to communicate with the SharePoint REST API</span></span>

<span data-ttu-id="27961-p104">Для связи с REST API SharePoint рекомендуется использовать SPHttpClient, предоставляемый вместе с SharePoint Framework. Этот класс содержит удобную логику для отправки запросов REST к API SharePoint, которая упрощает код. Например, когда вы отправляете запрос, отличный от GET, используя SPHttpClient, он автоматически получает действительный дайджест запроса и добавляет его в запрос. Это значительно упрощает решение, так как не нужно создавать код для управления токенами дайджеста запросов и их проверки.</span><span class="sxs-lookup"><span data-stu-id="27961-p104">The recommended way to communicate with the SharePoint REST API is using the SPHttpClient provided with the SharePoint Framework. This class wraps issuing REST requests to the SharePoint REST API with convenient logic that simplifies your code. For example, whenever you issue a non-GET request using the SPHttpClient, it will automatically obtain a valid request digest and add it to the request. This significantly simplifies your solution as you don't need to build code to manage request digest tokens and ensure their validity.</span></span>

<span data-ttu-id="27961-p105">При создании новых настроек в SharePoint Framework для связи с REST API SharePoint всегда следует использовать SPHttpClient. Однако, иногда это невозможно, например, когда вы переносите существующую настройку в SharePoint Framework и хотите сохранить как можно больше исходного кода или создаете настройку, используя библиотеку, такую как Angular(JS), с собственными службами для отправки веб-запросов. В таких случаях действительный токен дайджеста запроса можно получить из службы **DigestCache**.</span><span class="sxs-lookup"><span data-stu-id="27961-p105">If you're building new customizations on the SharePoint Framework, you should always use the SPHttpClient to communicate with the SharePoint REST API. Sometimes however, you might not be able to use the SPHttpClient. This can be the case for example when you're migrating an existing customization to the SharePoint Framework and want to keep as much of the original code as possible, or you're building a customization using a library such as Angular(JS), that has its own services for issuing web requests. In such cases you can obtain a valid request digest token from the **DigestCache**.</span></span>

## <a name="retrieve-valid-request-digest-using-the-digestcache-service"></a><span data-ttu-id="27961-122">Извлечение действительного дайджеста запроса с помощью службы DigestCache</span><span class="sxs-lookup"><span data-stu-id="27961-122">Retrieve valid request digest using the DigestCache service</span></span>

<span data-ttu-id="27961-p106">Если использовать SPHttpClient для связи с REST API SharePoint невозможно, действительный токен дайджеста запроса можно получить, используя службу **DigestCache**, предоставляемую вместе с SharePoint Framework. Использовать службу DigestCache удобнее, чем получать действительный токен дайджеста запроса вручную, так как DigestCache автоматически проверяет полученный ранее дайджест запроса. Если срок его действия истек, служба DigestCache автоматически запрашивает новый токен дайджеста запроса в SharePoint и сохраняет его для последующих запросов. Использование DigestCache упрощает код и делает решение более надежным.</span><span class="sxs-lookup"><span data-stu-id="27961-p106">If you can't use the SPHttpClient for communicating with the SharePoint REST API, you can obtain a valid request digest token using the **DigestCache** service provided with the SharePoint Framework. The benefit of using the DigestCache service over manually obtaining a valid request digest token is, that the DigestCache automatically checks if the previously retrieved request digest is still valid or not. If it's expired, the DigestCache service will automatically request a new request digest token from SharePoint and store it from subsequent requests. Using the DigestCache simplifies your code and makes your solution more robust.</span></span>

<span data-ttu-id="27961-127">Чтобы использовать службу DigestCache в коде, сначала импортируйте типы **DigestCache** и **IDigestCache** из пакета **@microsoft/sp-http**:</span><span class="sxs-lookup"><span data-stu-id="27961-127">To use the DigestCache service in your code, first import the **DigestCache** and **IDigestCache** types from the **@microsoft/sp-http** package:</span></span>

```ts
// ...
import { IDigestCache, DigestCache } from '@microsoft/sp-http';

export default class HelloWorldWebPart extends BaseClientSideWebPart<IHelloWorldWebPartProps> {
  // ...
}
```

<span data-ttu-id="27961-128">После этого, когда вам понадобится действительный токен дайджеста запроса, получите ссылку на службу DigestCache и вызовите ее метод **fetchDigest**:</span><span class="sxs-lookup"><span data-stu-id="27961-128">Next, whenever you need a valid request digest token, retrieve a reference to the DigestCache service and call its **fetchDigest** method:</span></span>

```ts
// ...
import { IDigestCache, DigestCache } from '@microsoft/sp-http';

export default class HelloWorldWebPart extends BaseClientSideWebPart<IHelloWorldWebPartProps> {
  protected onInit(): Promise<void> {
    return new Promise<void>((resolve: () => void, reject: (error: any) => void): void => {
      const digestCache: IDigestCache = this.context.serviceScope.consume(DigestCache.serviceKey);
      digestCache.fetchDigest(this.context.pageContext.web.serverRelativeUrl).then((digest: string): void => {
        // use the digest here
        resolve();
      });
    });
  }

  // ...
}
```