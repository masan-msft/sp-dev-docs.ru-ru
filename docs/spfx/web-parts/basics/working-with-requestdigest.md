---
title: "Работа с __REQUESTDIGEST"
description: "Добавляйте действительный дайджест к каждому запросу API SharePoint, отличному от GET REST."
ms.date: 01/09/2018
ms.prod: sharepoint
ms.openlocfilehash: 8a357c2a199566dbbf24f209c18b5f4673bd8b1a
ms.sourcegitcommit: 2188f21ce207c9d62d7d8af93822bd101058ba2f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/10/2018
---
# <a name="work-with-requestdigest"></a><span data-ttu-id="001d8-103">Работа с __REQUESTDIGEST</span><span class="sxs-lookup"><span data-stu-id="001d8-103">Work with __REQUESTDIGEST</span></span>

<span data-ttu-id="001d8-104">К каждому запросу API SharePoint, отличному от GET REST, необходимо добавлять действительный дайджест.</span><span class="sxs-lookup"><span data-stu-id="001d8-104">When executing non-GET REST requests to the SharePoint API, you must add a valid request digest to your request.</span></span> <span data-ttu-id="001d8-105">Этот дайджест доказывает, что запрос к SharePoint является действительным.</span><span class="sxs-lookup"><span data-stu-id="001d8-105">This digest proves validity of your request to SharePoint.</span></span> <span data-ttu-id="001d8-106">Так как срок действия этого токена ограничен, необходимо убедиться, что токен действителен, прежде чем добавлять его к запросу. В противном случае запрос будет отклонен.</span><span class="sxs-lookup"><span data-stu-id="001d8-106">Because this token is valid only for a limited period of time, you have to ensure that the token you have is valid before adding it to your request or the request fails.</span></span> 

<span data-ttu-id="001d8-107">На классических страницах SharePoint дайджест-токен запроса включается в скрытое поле с именем **__REQUESTDIGEST**.</span><span class="sxs-lookup"><span data-stu-id="001d8-107">In classic pages, SharePoint includes a request digest token on the page in a hidden field named **__REQUESTDIGEST**.</span></span> <span data-ttu-id="001d8-108">Часто дайджест извлекают из этого поля и добавляют к запросу, например:</span><span class="sxs-lookup"><span data-stu-id="001d8-108">In classic pages, SharePoint includes a request digest token on the page in a hidden field named __REQUESTDIGEST. One of the most common approaches to work with the request digest, is to obtain it from that field and add it to the request, for example:</span></span>

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

<span data-ttu-id="001d8-109">Поначалу такой запрос будет работать, но если страница будет открыта долго, срок действия дайджеста запроса на странице истечет и возникнет ошибка **403 FORBIDDEN**.</span><span class="sxs-lookup"><span data-stu-id="001d8-109">Such a request would work initially, but if the user has the page open for a longer period of time, the request digest on the page expires and the request fails with a **403 FORBIDDEN** result.</span></span> <span data-ttu-id="001d8-110">По умолчанию срок действия дайджест-токена запроса составляет 30 минут, поэтому перед его использованием необходимо убедиться, что он еще действителен.</span><span class="sxs-lookup"><span data-stu-id="001d8-110">By default, a request digest token is valid for 30 minutes, so before using it, you have to ensure that it's still valid.</span></span> <span data-ttu-id="001d8-111">В прошлом это требовалось делать вручную, сравнивая метку времени из дайджеста запроса с текущим временем.</span><span class="sxs-lookup"><span data-stu-id="001d8-111">In the past you had to do this manually, by comparing the timestamp from the request digest with the current time.</span></span> 

<span data-ttu-id="001d8-112">SharePoint Framework упрощает этот процесс, позволяя проверить, действителен ли дайджест-токен запроса одним из двух способов.</span><span class="sxs-lookup"><span data-stu-id="001d8-112">SharePoint Framework simplifies this process by offering you two ways of ensuring that your request has a valid request digest token.</span></span>

## <a name="use-the-sphttpclient-to-communicate-with-the-sharepoint-rest-api"></a><span data-ttu-id="001d8-113">Использование класса SPHttpClient для связи с REST API SharePoint</span><span class="sxs-lookup"><span data-stu-id="001d8-113">Use the SPHttpClient to communicate with the SharePoint REST API</span></span>

<span data-ttu-id="001d8-114">Рекомендуемый способ связи с REST API SharePoint — использование класса SPHttpClient, входящего в состав SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="001d8-114">The recommended way to communicate with the SharePoint REST API is to use the SPHttpClient provided with the SharePoint Framework.</span></span> <span data-ttu-id="001d8-115">Этот класс представляет собой оболочку для отправки запросов REST к REST API SharePoint с удобной логикой, упрощающей код.</span><span class="sxs-lookup"><span data-stu-id="001d8-115">This class wraps issuing REST requests to the SharePoint REST API with convenient logic that simplifies your code.</span></span> 

<span data-ttu-id="001d8-116">Например, при отправке отличного от GET запроса с помощью SPHttpClient автоматически возвращается действительный дайджест, который добавляется к запросу.</span><span class="sxs-lookup"><span data-stu-id="001d8-116">For example, whenever you issue a non-GET request using the SPHttpClient, it automatically obtains a valid request digest and adds it to the request.</span></span> <span data-ttu-id="001d8-117">Это значительно упрощает решение, так как вам не требуется писать код для управления дайджест-токенами запросов и проверять, являются ли они действительными.</span><span class="sxs-lookup"><span data-stu-id="001d8-117">This significantly simplifies your solution because you don't need to build code to manage request digest tokens and ensure their validity.</span></span>

<span data-ttu-id="001d8-118">При создании новых настроек на платформе SharePoint Framework следует всегда использовать класс SPHttpClient для работы с REST API SharePoint.</span><span class="sxs-lookup"><span data-stu-id="001d8-118">If you're building new customizations on the SharePoint Framework, you should always use the SPHttpClient to communicate with the SharePoint REST API.</span></span> 

<span data-ttu-id="001d8-119">Но иногда может не быть возможности использовать SPHttpClient.</span><span class="sxs-lookup"><span data-stu-id="001d8-119">Sometimes, however, you might not be able to use the SPHttpClient.</span></span> <span data-ttu-id="001d8-120">Например, такая проблема может возникать при переносе имеющейся настройки на платформу SharePoint Framework, если требуется сохранить как можно больше первоначального кода, или при создании настроек с помощью таких библиотек, как Angular(JS), где предусмотрены собственные службы для отправки веб-запросов.</span><span class="sxs-lookup"><span data-stu-id="001d8-120">If you're building new customizations on the SharePoint Framework, you should always use the SPHttpClient to communicate with the SharePoint REST API. Sometimes however, you might not be able to use the SPHttpClient. This can be the case for example when you're migrating an existing customization to the SharePoint Framework and want to keep as much of the original code as possible, or you're building a customization using a library such as Angular(JS), that has its own services for issuing web requests. In such cases you can obtain a valid request digest token from the DigestCache.</span></span> <span data-ttu-id="001d8-121">В таких случаях действительный дайджест-токен запроса можно получить из службы **DigestCache**.</span><span class="sxs-lookup"><span data-stu-id="001d8-121">In such cases you can obtain a valid request digest token from the **DigestCache**.</span></span>

## <a name="retrieve-a-valid-request-digest-by-using-the-digestcache-service"></a><span data-ttu-id="001d8-122">Получение действительного дайджеста запроса из службы DigestCache</span><span class="sxs-lookup"><span data-stu-id="001d8-122">Retrieve valid request digest using the DigestCache service</span></span>

<span data-ttu-id="001d8-123">Если у вас нет возможности использовать класс SPHttpClient для работы с REST API SharePoint, то вы можете получить действительный дайджест-токен запроса из службы **DigestCache**, входящей в состав SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="001d8-123">If you can't use the SPHttpClient for communicating with the SharePoint REST API, you can obtain a valid request digest token by using the **DigestCache** service provided with the SharePoint Framework.</span></span> 

<span data-ttu-id="001d8-124">Преимущество использования службы DigestCache по сравнению с получением действительного дайджест-токена запроса вручную заключается в том, что DigestCache автоматически проверяет, действителен ли ранее полученный дайджест запроса.</span><span class="sxs-lookup"><span data-stu-id="001d8-124">The benefit of using the DigestCache service over manually obtaining a valid request digest token is that the DigestCache automatically checks if the previously retrieved request digest is still valid.</span></span> <span data-ttu-id="001d8-125">Если срок его действия истек, служба DigestCache автоматически запрашивает новый дайджест-токен из SharePoint и сохраняет его для последующих запросов.</span><span class="sxs-lookup"><span data-stu-id="001d8-125">If it's expired, the DigestCache service automatically requests a new request digest token from SharePoint and stores it from subsequent requests.</span></span> <span data-ttu-id="001d8-126">Использование DigestCache упрощает код и делает решение более надежным.</span><span class="sxs-lookup"><span data-stu-id="001d8-126">Using the DigestCache simplifies your code and makes your solution more robust.</span></span>

### <a name="to-use-the-digestcache-service-in-your-code"></a><span data-ttu-id="001d8-127">Использование службы DigestCache в коде</span><span class="sxs-lookup"><span data-stu-id="001d8-127">To use the DigestCache service in your code, first import the DigestCache and IDigestCache types from the @microsoft/sp-http package:</span></span>

1. <span data-ttu-id="001d8-128">Импортируйте типы **DigestCache** и **IDigestCache** из пакета **@microsoft/sp-http**:</span><span class="sxs-lookup"><span data-stu-id="001d8-128">Import the **DigestCache** and **IDigestCache** types from the **@microsoft/sp-http** package:</span></span>

  ```ts
  // ...
  import { IDigestCache, DigestCache } from '@microsoft/sp-http';

  export default class HelloWorldWebPart extends BaseClientSideWebPart<IHelloWorldWebPartProps> {
    // ...
  }
  ```

2. <span data-ttu-id="001d8-129">Когда вам понадобится действительный дайджест-токен запроса, получите ссылку на службу DigestCache и вызовите ее метод **fetchDigest**:</span><span class="sxs-lookup"><span data-stu-id="001d8-129">Next, whenever you need a valid request digest token, retrieve a reference to the DigestCache service and call its **fetchDigest** method:</span></span>

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