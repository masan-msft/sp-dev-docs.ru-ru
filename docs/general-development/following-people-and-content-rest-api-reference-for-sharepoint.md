---
title: "Подписки на людей и контент Справочник по интерфейсу API службы REST для SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: c05755df-846d-4a39-941d-950d066cc6d4
ms.openlocfilehash: d18faadfbb6ea259fb073609e892d2fa4dcd344d
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="following-people-and-content-rest-api-reference-for-sharepoint"></a><span data-ttu-id="6dbda-102">Подписки на людей и контент Справочник по интерфейсу API службы REST для SharePoint</span><span class="sxs-lookup"><span data-stu-id="6dbda-102">Following people and content REST API reference for SharePoint</span></span>
<span data-ttu-id="6dbda-103">Поиск конечных точек SharePoint REST для подписки на людей и контент с помощью **SocialRestFollowingManager** ресурсов и ресурсов **PeopleManager** .</span><span class="sxs-lookup"><span data-stu-id="6dbda-103">Find SharePoint REST endpoints for following people and content by using the **SocialRestFollowingManager** resource and the **PeopleManager** resource.</span></span>
<span data-ttu-id="6dbda-104">Чтобы выполнить те же задачи, которые можно выполнить при использовании клиентской объектной модели .NET и объектной модели JavaScript, можно использовать службу SharePoint представлений состояния (REST).</span><span class="sxs-lookup"><span data-stu-id="6dbda-104">You can use the SharePoint Representational State Transfer (REST) service to do the same tasks you can do when you use the .NET client object models and the JavaScript object model.</span></span> <span data-ttu-id="6dbda-105">Для использования службы REST, построение и отправлять запросы **POST** и HTTP **GET** конечных точек ресурсов, которые представляют задачи, которые необходимо выполнить.</span><span class="sxs-lookup"><span data-stu-id="6dbda-105">To use the REST service, you build and send HTTP **GET** and **POST** requests to the resource endpoints that represent the tasks you want to do.</span></span> <span data-ttu-id="6dbda-106">Эти конечные точки ресурсов соответствуют объектов SharePoint, свойств и методов.</span><span class="sxs-lookup"><span data-stu-id="6dbda-106">These resource endpoints correspond to SharePoint objects, properties, and methods.</span></span>
  
    
    

<span data-ttu-id="6dbda-p102">URI конечной точки для большинства следующие задачи начинается с ресурсом **SocialRestFollowingManager** ( `social.following`) и заканчивается ресурсов, используемая для выполнения определенной задачи. Например необходимо использовать URI  `http://www.contoso.com/_api/social.following/follow` текущего пользователя запустите следующие людей или содержимого и URI `https://www.contoso.com/sites/devSite/_api/social.following/followed` люди или контента  это следующий текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="6dbda-p102">The endpoint URI for most Following tasks begins with the **SocialRestFollowingManager** resource ( `social.following`) and ends with the resource that performs the specific task. For example, you use the URI  `http://www.contoso.com/_api/social.following/follow` to make the current user start following people or content, and the URI `https://www.contoso.com/sites/devSite/_api/social.following/followed` to get the people or content the current user is following.</span></span>
> <span data-ttu-id="6dbda-109">**Примечание:** В этой статье показаны конечной точке URI и параметр компоненты HTTP-запросов.</span><span class="sxs-lookup"><span data-stu-id="6dbda-109">**Note:** This article shows the endpoint URI and parameter components of HTTP requests.</span></span> <span data-ttu-id="6dbda-110">В разделе примеры запросов на полный [как: с помощью службы REST в SharePoint, выполните документы, сайты и тегов](how-to-follow-documents-sites-and-tags-by-using-the-rest-service-in-sharepoint-2.md).</span><span class="sxs-lookup"><span data-stu-id="6dbda-110">For examples of complete requests, see  [How to: Follow documents, sites, and tags by using the REST service in SharePoint](how-to-follow-documents-sites-and-tags-by-using-the-rest-service-in-sharepoint-2.md).</span></span> 
  
    
    

<span data-ttu-id="6dbda-p104">Мы рекомендуем использовать **SocialRestFollowingManager** API для следующих пользователей и контента следующие задачи, что вы можете использовать **PeopleManager** ресурсов для некоторых следующие сотрудники обзор задач, **SocialRestFollowingManager** не поддерживает. К примеру можно узнать ли кто-то после текущего пользователя или получить последователи другому пользователю. Для выполнения этих задач отправлять **GET** HTTP-запросов к конечной точке URI, которые начинаются с ресурсом **PeopleManager** ( `sp.userprofiles.peoplemanager`) и заканчиваются ресурсов, используемая для выполнения определенной задачи.Если конечная точка с параметром, метаданные параметров отправляется в URI или в тексте запроса в формате XML или Нотация объектов JavaScript (JSON). Можно сделать HTTP-запросов на любом языке, включая JavaScript и C#. По умолчанию службы REST возвращает ответы, отформатированные с помощью протокола Atom, но можно запросить формат JSON с помощью **Accept** заголовки HTTP. В разделе [Программирование с использованием службы SharePoint 2013 REST](http://msdn.microsoft.com/library/d4b5c277-ed50-420c-8a9b-860342284b72%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="6dbda-p104">We recommend that you use the **SocialRestFollowingManager** API for Following People and Following Content tasks, but you can use the **PeopleManager** resource for some Following People tasks that **SocialRestFollowingManager** doesn't support. For example, you can find out whether someone is following the current user or get another user's followers. For these tasks, you send HTTP **GET** requests to endpoint URIs that begin with the **PeopleManager** resource ( `sp.userprofiles.peoplemanager`) and end with the resource that performs the specific task.If the endpoint takes a parameter, the parameter metadata is sent in the URI or in the request body in XML or JavaScript Object Notation (JSON) format. You can make HTTP requests in any language, including JavaScript and C#. By default, the REST service returns responses that are formatted by using the Atom protocol, but you can request the JSON format by using HTTP **Accept** headers. See [Use OData query operations in SharePoint REST requests](http://msdn.microsoft.com/library/d4b5c277-ed50-420c-8a9b-860342284b72%28Office.15%29.aspx).</span></span>
## <a name="resource-endpoints-for-following-people-and-following-content-tasks"></a><span data-ttu-id="6dbda-117">Конечные точки ресурсов для задач, следующие сотрудники и следующие контента</span><span class="sxs-lookup"><span data-stu-id="6dbda-117">Resource endpoints for Following People and Following Content tasks</span></span>
<span data-ttu-id="6dbda-118"><a name="bk_Overview"> </a></span><span class="sxs-lookup"><span data-stu-id="6dbda-118"></span></span>


[<span data-ttu-id="6dbda-119">Follow</span><span class="sxs-lookup"><span data-stu-id="6dbda-119">Follow</span></span>](#bk_Follow)  
[<span data-ttu-id="6dbda-120">StopFollowing</span><span class="sxs-lookup"><span data-stu-id="6dbda-120">StopFollowing</span></span>](#bk_StopFollowing)  
[<span data-ttu-id="6dbda-121">IsFollowed</span><span class="sxs-lookup"><span data-stu-id="6dbda-121">IsFollowed</span></span>](#bk_IsFollowed)  
[<span data-ttu-id="6dbda-122">Мои</span><span class="sxs-lookup"><span data-stu-id="6dbda-122">My</span></span>](#bk_My)  
[<span data-ttu-id="6dbda-123">Мои/FollowedDocumentsUri</span><span class="sxs-lookup"><span data-stu-id="6dbda-123">My/FollowedDocumentsUri</span></span>](#bk_MyFollowedDocumentsUri)  
[<span data-ttu-id="6dbda-124">Мои/FollowedSitesUri</span><span class="sxs-lookup"><span data-stu-id="6dbda-124">My/FollowedSitesUri</span></span>](#bk_MyFollowedSitesUri)  
[<span data-ttu-id="6dbda-125">Мои/за</span><span class="sxs-lookup"><span data-stu-id="6dbda-125">My/Followed</span></span>](#bk_Followed)  
[<span data-ttu-id="6dbda-126">Мои/FollowedCount</span><span class="sxs-lookup"><span data-stu-id="6dbda-126">My/FollowedCount</span></span>](#bk_FollowedCount)  
[<span data-ttu-id="6dbda-127">Мои / последователи</span><span class="sxs-lookup"><span data-stu-id="6dbda-127">My/Followers</span></span>](#bk_Followers)  
[<span data-ttu-id="6dbda-128">Мои / предложений</span><span class="sxs-lookup"><span data-stu-id="6dbda-128">My/Suggestions</span></span>](#bk_Suggestions)  
[<span data-ttu-id="6dbda-129">GetMySuggestions</span><span class="sxs-lookup"><span data-stu-id="6dbda-129">GetMySuggestions</span></span>](#bk_GetMySuggestions)  
[<span data-ttu-id="6dbda-130">IsMyPeopleListPublic</span><span class="sxs-lookup"><span data-stu-id="6dbda-130">IsMyPeopleListPublic</span></span>](#bk_IsMyPeopleListPublic)  
[<span data-ttu-id="6dbda-131">AmIFollowedBy</span><span class="sxs-lookup"><span data-stu-id="6dbda-131">AmIFollowedBy</span></span>](#bk_AmIFollowedBy)  
[<span data-ttu-id="6dbda-132">GetPeopleFollowedBy</span><span class="sxs-lookup"><span data-stu-id="6dbda-132">GetPeopleFollowedBy</span></span>](#bk_GetPeopleFollowedBy)  
[<span data-ttu-id="6dbda-133">GetFollowersFor</span><span class="sxs-lookup"><span data-stu-id="6dbda-133">GetFollowersFor</span></span>](#bk_GetFollowersFor)  
   

## <a name="follow"></a><span data-ttu-id="6dbda-134">Подписка</span><span class="sxs-lookup"><span data-stu-id="6dbda-134">Follow</span></span>
<span data-ttu-id="6dbda-135"><a name="bk_Follow"> </a></span><span class="sxs-lookup"><span data-stu-id="6dbda-135"></span></span>

<span data-ttu-id="6dbda-136">Делает создайте пользователя, документов, сайта или тег текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="6dbda-136">Makes the current user start following a user, document, site, or tag.</span></span>
  
    
    

### <a name="endpoint-uri-structure"></a><span data-ttu-id="6dbda-137">Структура URI конечной точки</span><span class="sxs-lookup"><span data-stu-id="6dbda-137">Endpoint URI structure</span></span>

 <span data-ttu-id="6dbda-138">**POST** `http://<siteCollection>/<site>/_api/social.following/follow`</span><span class="sxs-lookup"><span data-stu-id="6dbda-138">**POST** `http://<siteCollection>/<site>/_api/social.following/follow`</span></span>
  
    
    

### <a name="request-parameter"></a><span data-ttu-id="6dbda-139">Параметр запроса</span><span class="sxs-lookup"><span data-stu-id="6dbda-139">Request parameter</span></span>

 <span data-ttu-id="6dbda-140">_actor_</span><span class="sxs-lookup"><span data-stu-id="6dbda-140">_actor_</span></span>
  
    
    
<span data-ttu-id="6dbda-141">тип: **SP.Social.SocialActorInfo**</span><span class="sxs-lookup"><span data-stu-id="6dbda-141">Type: **SP.Social.SocialActorInfo**</span></span>
  
    
    
<span data-ttu-id="6dbda-142">actor для запуска подписки.</span><span class="sxs-lookup"><span data-stu-id="6dbda-142">The actor to start following.</span></span>
  
    
    
 <span data-ttu-id="6dbda-143">**Пользователь  _actor_ в URI**</span><span class="sxs-lookup"><span data-stu-id="6dbda-143">**User  _actor_ in the URI**</span></span>
  
    
    



```

http://<siteCollection>/<site>/_api/social.following/follow(ActorType=0,AccountName=@v,Id=null)?@v='domain\\user'
```

 <span data-ttu-id="6dbda-144">**Пользователь  _actor_ в теле запроса**</span><span class="sxs-lookup"><span data-stu-id="6dbda-144">**User  _actor_ in the request body**</span></span>
  
    
    



```
"actor":{
  "__metadata":{"type":"SP.Social.SocialActorInfo"},
  "ActorType":0,
  "AccountName":"domain\\user",
  "Id":null
}
```

<span data-ttu-id="6dbda-145">Если вы используете модели удостоверений на основе утверждений, вы можете передать имя учетной записи с помощью формата  `@v='i:0"%23".f|membership|user@domain.com'` в строке запроса или `"i:0#.f|membership|user@domain.com"` в тексте запроса.</span><span class="sxs-lookup"><span data-stu-id="6dbda-145">If you're using a claims-based identity model, you can pass the account name by using the format  `@v='i:0"%23".f|membership|user@domain.com'` in the query string or `"i:0#.f|membership|user@domain.com"` in the request body.</span></span>
  
    
    
 <span data-ttu-id="6dbda-146">**Документ  _actor_ в URI**</span><span class="sxs-lookup"><span data-stu-id="6dbda-146">**Document  _actor_ in the URI**</span></span>
  
    
    



```

http://<siteCollection>/<site>/_api/social.following/follow(ActorType=1,ContentUri=@v,Id=null)?@v='http://server/Shared%20Documents/fileName.docx'
```

 <span data-ttu-id="6dbda-147">**Документ  _actor_ в теле запроса**</span><span class="sxs-lookup"><span data-stu-id="6dbda-147">**Document  _actor_ in the request body**</span></span>
  
    
    



```
"actor":{
  "__metadata":{"type":"SP.Social.SocialActorInfo"},
  "ActorType":1,
  "ContentUri":"http://server/Shared%20Documents/fileName.docx",
  "Id":null
}
```

 <span data-ttu-id="6dbda-148">**Сайт  _actor_ в URI**</span><span class="sxs-lookup"><span data-stu-id="6dbda-148">**Site  _actor_ in the URI**</span></span>
  
    
    



```

http://<siteCollection>/<site>/_api/social.following/follow(ActorType=2,ContentUri=@v,Id=null)?@v='http://server/site'
```

 <span data-ttu-id="6dbda-149">**Сайт  _actor_ в теле запроса**</span><span class="sxs-lookup"><span data-stu-id="6dbda-149">**Site  _actor_ in the request body**</span></span>
  
    
    



```
"actor":{
  "__metadata":{"type":"SP.Social.SocialActorInfo"},
  "ActorType":2,
  "ContentUri":"http://siteCollection/site",
  "Id":null
}
```

 <span data-ttu-id="6dbda-150">**Тег  _actor_ в URI**</span><span class="sxs-lookup"><span data-stu-id="6dbda-150">**Tag  _actor_ in the URI**</span></span>
  
    
    



```

http://<siteCollection>/<site>/_api/social.following/follow(ActorType=3,TagGuid='19a4a484-c1dc-4bc5-8c93-bb96245ce928',Id=null)
```

 <span data-ttu-id="6dbda-151">**Тег  _actor_ в теле запроса**</span><span class="sxs-lookup"><span data-stu-id="6dbda-151">**Tag  _actor_ in the request body**</span></span>
  
    
    



```
"actor":{
  "__metadata":{"type":"SP.Social.SocialActorInfo"},
  "ActorType":3,
  "TagGuid":"19a4a484-c1dc-4bc5-8c93-bb96245ce928",
  "Id":null
}
```

<span data-ttu-id="6dbda-p105">Требуется тег идентификатор GUID для запуска отслеживание тега. Не удается получить GUID с помощью службы REST, но вы можете использовать клиентской объектной модели .NET или JavaScript объектной модели. Узнайте,  [как получить идентификатор GUID тега на основе имени тега с помощью объектной модели JavaScript](follow-content-in-sharepoint.md#bk_getTagGuid).</span><span class="sxs-lookup"><span data-stu-id="6dbda-p105">You need the tag GUID to start following a tag. You can't get the GUID by using the REST service, but you can use the .NET client object model or the JavaScript object model. See  [How to get a tag's GUID based on the tag's name by using the JavaScript object model](follow-content-in-sharepoint.md#bk_getTagGuid).</span></span>
  
    
    

### <a name="response"></a><span data-ttu-id="6dbda-155">Ответ</span><span class="sxs-lookup"><span data-stu-id="6dbda-155">Response</span></span>

 <span data-ttu-id="6dbda-156">**Follow**</span><span class="sxs-lookup"><span data-stu-id="6dbda-156">**Follow**</span></span>
  
    
    
<span data-ttu-id="6dbda-157">тип: **SP.Social.SocialFollowResult**</span><span class="sxs-lookup"><span data-stu-id="6dbda-157">Type: **SP.Social.SocialFollowResult**</span></span>
  
    
    
<span data-ttu-id="6dbda-158">состояние запроса: 0 = ОК. 1 = AlreadyFollowing; 2 = LimitReached; или 3 = InternalError.</span><span class="sxs-lookup"><span data-stu-id="6dbda-158">The status of the request: 0 = OK; 1 = AlreadyFollowing; 2 = LimitReached; or 3 = InternalError.</span></span>
  
    
    
<span data-ttu-id="6dbda-159">Приведенный ниже ответ указывает, что запрос завершился успешно.</span><span class="sxs-lookup"><span data-stu-id="6dbda-159">The following response indicates that the request succeeded.</span></span>
  
    
    



```

{"d":{"Follow":0}}
```


## <a name="stopfollowing"></a><span data-ttu-id="6dbda-160">StopFollowing</span><span class="sxs-lookup"><span data-stu-id="6dbda-160">StopFollowing</span></span>
<span data-ttu-id="6dbda-161"><a name="bk_StopFollowing"> </a></span><span class="sxs-lookup"><span data-stu-id="6dbda-161"></span></span>

<span data-ttu-id="6dbda-162">Делает остановите следующие пользователей, документов, сайта или тег текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="6dbda-162">Makes the current user stop following a user, document, site, or tag.</span></span>
  
    
    

### <a name="endpoint-uri-structure"></a><span data-ttu-id="6dbda-163">Структура URI конечной точки</span><span class="sxs-lookup"><span data-stu-id="6dbda-163">Endpoint URI structure</span></span>

 <span data-ttu-id="6dbda-164">**POST** `http://<siteCollection>/<site>/_api/social.following/stopfollowing`</span><span class="sxs-lookup"><span data-stu-id="6dbda-164">**POST** `http://<siteCollection>/<site>/_api/social.following/stopfollowing`</span></span>
  
    
    

### <a name="request-parameter"></a><span data-ttu-id="6dbda-165">Параметр запроса</span><span class="sxs-lookup"><span data-stu-id="6dbda-165">Request parameter</span></span>

 <span data-ttu-id="6dbda-166">_actor_</span><span class="sxs-lookup"><span data-stu-id="6dbda-166">_actor_</span></span>
  
    
    
<span data-ttu-id="6dbda-167">тип: **SP.Social.SocialActorInfo**</span><span class="sxs-lookup"><span data-stu-id="6dbda-167">Type: **SP.Social.SocialActorInfo**</span></span>
  
    
    
<span data-ttu-id="6dbda-168">actor, чтобы отменить подписку.</span><span class="sxs-lookup"><span data-stu-id="6dbda-168">The actor to stop following.</span></span>
  
    
    
 <span data-ttu-id="6dbda-169">**Пользователь  _actor_ в URI**</span><span class="sxs-lookup"><span data-stu-id="6dbda-169">**User  _actor_ in the URI**</span></span>
  
    
    



```
http://<siteCollection>/<site>/_api/social.following/stopfollowing(ActorType=0,AccountName=@v,Id=null)?@v='domain\\user'
```

 <span data-ttu-id="6dbda-170">**Пользователь  _actor_ в теле запроса**</span><span class="sxs-lookup"><span data-stu-id="6dbda-170">**User  _actor_ in the request body**</span></span>
  
    
    



```
"actor":{
  "__metadata":{"type":"SP.Social.SocialActorInfo"},
  "ActorType":0,
  "AccountName":"domain\\user",
  "Id":null
}
```

<span data-ttu-id="6dbda-171">Если вы используете модели удостоверений на основе утверждений, вы можете передать имя учетной записи с помощью формата  `@v='i:0"%23".f|membership|user@domain.com'` в строке запроса или `"i:0#.f|membership|user@domain.com"` в тексте запроса.</span><span class="sxs-lookup"><span data-stu-id="6dbda-171">If you're using a claims-based identity model, you can pass the account name by using the format  `@v='i:0"%23".f|membership|user@domain.com'` in the query string or `"i:0#.f|membership|user@domain.com"` in the request body.</span></span>
  
    
    
 <span data-ttu-id="6dbda-172">**Документ  _actor_ в URI**</span><span class="sxs-lookup"><span data-stu-id="6dbda-172">**Document  _actor_ in the URI**</span></span>
  
    
    



```

http://<siteCollection>/<site>/_api/social.following/stopfollowing(ActorType=1,ContentUri=@v,Id=null)?@v='http://server/Shared%20Documents/fileName.docx'
```

 <span data-ttu-id="6dbda-173">**Документ  _actor_ в теле запроса**</span><span class="sxs-lookup"><span data-stu-id="6dbda-173">**Document  _actor_ in the request body**</span></span>
  
    
    



```
"actor":{
  "__metadata":{"type":"SP.Social.SocialActorInfo"},
  "ActorType":1,
  "ContentUri":"http://server/Shared%20Documents/fileName.docx",
  "Id":null
}
```

 <span data-ttu-id="6dbda-174">**Сайт  _actor_ в URI**</span><span class="sxs-lookup"><span data-stu-id="6dbda-174">**Site  _actor_ in the URI**</span></span>
  
    
    



```

http://<siteCollection>/<site>/_api/social.following/stopfollowing(ActorType=2,ContentUri=@v,Id=null)?@v='http://server/site'
```

 <span data-ttu-id="6dbda-175">**Сайт  _actor_ в теле запроса**</span><span class="sxs-lookup"><span data-stu-id="6dbda-175">**Site  _actor_ in the request body**</span></span>
  
    
    



```
"actor":{
  "__metadata":{"type":"SP.Social.SocialActorInfo"},
  "ActorType":2,
  "ContentUri":"http://siteCollection/site",
  "Id":null
}
```

 <span data-ttu-id="6dbda-176">**Тег  _actor_ в URI**</span><span class="sxs-lookup"><span data-stu-id="6dbda-176">**Tag  _actor_ in the URI**</span></span>
  
    
    



```

http://<siteCollection>/<site>/_api/social.following/stopfollowing(ActorType=3,TagGuid='19a4a484-c1dc-4bc5-8c93-bb96245ce928',Id=null)
```

 <span data-ttu-id="6dbda-177">**Тег  _actor_ в теле запроса**</span><span class="sxs-lookup"><span data-stu-id="6dbda-177">**Tag  _actor_ in the request body**</span></span>
  
    
    



```
"actor":{
  "__metadata":{"type":"SP.Social.SocialActorInfo"},
  "ActorType":3,
  "TagGuid":"19a4a484-c1dc-4bc5-8c93-bb96245ce928",
  "Id":null
}
```

<span data-ttu-id="6dbda-p106">Требуется тег идентификатор GUID для запуска отслеживание тега. Не удается получить GUID с помощью службы REST, но вы можете использовать клиентской объектной модели .NET или JavaScript объектной модели. Узнайте,  [как получить идентификатор GUID тега на основе имени тега с помощью объектной модели JavaScript](follow-content-in-sharepoint.md#bk_getTagGuid).</span><span class="sxs-lookup"><span data-stu-id="6dbda-p106">You need the tag GUID to start following a tag. You can't get the GUID by using the REST service, but you can use the .NET client object model or the JavaScript object model. See  [How to get a tag's GUID based on the tag's name by using the JavaScript object model](follow-content-in-sharepoint.md#bk_getTagGuid).</span></span>
  
    
    

### <a name="response"></a><span data-ttu-id="6dbda-181">Ответ</span><span class="sxs-lookup"><span data-stu-id="6dbda-181">Response</span></span>

<span data-ttu-id="6dbda-182">Нет.</span><span class="sxs-lookup"><span data-stu-id="6dbda-182">None.</span></span>
  
    
    

```

{"d":{"StopFollowing":null}}
```


## <a name="isfollowed"></a><span data-ttu-id="6dbda-183">IsFollowed</span><span class="sxs-lookup"><span data-stu-id="6dbda-183">IsFollowed</span></span>
<span data-ttu-id="6dbda-184"><a name="bk_IsFollowed"> </a></span><span class="sxs-lookup"><span data-stu-id="6dbda-184"></span></span>

<span data-ttu-id="6dbda-185">Указывает, является ли текущий пользователь следующие указанного пользователя, документов, сайта или тег.</span><span class="sxs-lookup"><span data-stu-id="6dbda-185">Indicates whether the current user is following a specified user, document, site, or tag.</span></span>
  
    
    

### <a name="endpoint-uri-structure"></a><span data-ttu-id="6dbda-186">Структура URI конечной точки</span><span class="sxs-lookup"><span data-stu-id="6dbda-186">Endpoint URI structure</span></span>

 <span data-ttu-id="6dbda-187">**POST** `http://<siteCollection>/<site>/_api/social.following/isfollowed`</span><span class="sxs-lookup"><span data-stu-id="6dbda-187">**POST** `http://<siteCollection>/<site>/_api/social.following/isfollowed`</span></span>
  
    
    

### <a name="request-parameter"></a><span data-ttu-id="6dbda-188">Параметр запроса</span><span class="sxs-lookup"><span data-stu-id="6dbda-188">Request parameter</span></span>

 <span data-ttu-id="6dbda-189">_actor_</span><span class="sxs-lookup"><span data-stu-id="6dbda-189">_actor_</span></span>
  
    
    
<span data-ttu-id="6dbda-190">тип: **SP.Social.SocialActorInfo**</span><span class="sxs-lookup"><span data-stu-id="6dbda-190">Type: **SP.Social.SocialActorInfo**</span></span>
  
    
    
<span data-ttu-id="6dbda-191">actor, чтобы найти сведения о следующих состоянии.</span><span class="sxs-lookup"><span data-stu-id="6dbda-191">The actor to find the following status for.</span></span>
  
    
    
 <span data-ttu-id="6dbda-192">**Пользователь  _actor_ в URI**</span><span class="sxs-lookup"><span data-stu-id="6dbda-192">**User  _actor_ in the URI**</span></span>
  
    
    



```
http://<siteCollection>/<site>/_api/social.following/isfollowed(ActorType=0,AccountName=@v,Id=null)?@v='domain\\user'
```

 <span data-ttu-id="6dbda-193">**Пользователь  _actor_ в теле запроса**</span><span class="sxs-lookup"><span data-stu-id="6dbda-193">**User  _actor_ in the request body**</span></span>
  
    
    



```
"actor":{
  "__metadata":{"type":"SP.Social.SocialActorInfo"},
  "ActorType":0,
  "AccountName":"domain\\user",
  "Id":null
}
```

<span data-ttu-id="6dbda-194">Если вы используете модели удостоверений на основе утверждений, вы можете передать имя учетной записи с помощью формата  `@v='i:0"%23".f|membership|user@domain.com'` в строке запроса или `"i:0#.f|membership|user@domain.com"` в тексте запроса.</span><span class="sxs-lookup"><span data-stu-id="6dbda-194">If you're using a claims-based identity model, you can pass the account name by using the format  `@v='i:0"%23".f|membership|user@domain.com'` in the query string or `"i:0#.f|membership|user@domain.com"` in the request body.</span></span>
  
    
    
 <span data-ttu-id="6dbda-195">**Документ  _actor_ в URI**</span><span class="sxs-lookup"><span data-stu-id="6dbda-195">**Document  _actor_ in the URI**</span></span>
  
    
    



```

http://<siteCollection>/<site>/_api/social.following/isfollowed(ActorType=1,ContentUri=@v,Id=null)?@v='https://domain.sharepoint.com/Shared%20Documents/fileName.docx'
```

 <span data-ttu-id="6dbda-196">**Документ  _actor_ в теле запроса**</span><span class="sxs-lookup"><span data-stu-id="6dbda-196">**Document  _actor_ in the request body**</span></span>
  
    
    



```
"actor":{
  "__metadata":{"type":"SP.Social.SocialActorInfo"},
  "ActorType":1,
  "ContentUri":"http://server/Shared%20Documents/fileName.docx",
  "Id":null
}
```

 <span data-ttu-id="6dbda-197">**Сайт  _actor_ в URI**</span><span class="sxs-lookup"><span data-stu-id="6dbda-197">**Site  _actor_ in the URI**</span></span>
  
    
    



```

http://<siteCollection>/<site>/_api/social.following/isfollowed(ActorType=2,ContentUri=@v,Id=null)?@v='http://domain.sharepoint.com'
```

 <span data-ttu-id="6dbda-198">**Сайт  _actor_ в теле запроса**</span><span class="sxs-lookup"><span data-stu-id="6dbda-198">**Site  _actor_ in the request body**</span></span>
  
    
    



```
"actor":{
  "__metadata":{"type":"SP.Social.SocialActorInfo"},
  "ActorType":2,
  "ContentUri":"http://siteCollection/site",
  "Id":null
}
```

 <span data-ttu-id="6dbda-199">**Тег  _actor_ в URI**</span><span class="sxs-lookup"><span data-stu-id="6dbda-199">**Tag  _actor_ in the URI**</span></span>
  
    
    



```

http://<siteCollection>/<site>/_api/social.following/isfollowed(ActorType=3,TagGuid='19a4a484-c1dc-4bc5-8c93-bb96245ce928',Id=null)
```

 <span data-ttu-id="6dbda-200">**Тег  _actor_ в теле запроса**</span><span class="sxs-lookup"><span data-stu-id="6dbda-200">**Tag  _actor_ in the request body**</span></span>
  
    
    



```
"actor":{
  "__metadata":{"type":"SP.Social.SocialActorInfo"},
  "ActorType":3,
  "TagGuid":"19a4a484-c1dc-4bc5-8c93-bb96245ce928",
  "Id":null
}
```

<span data-ttu-id="6dbda-p107">Требуется тег идентификатор GUID для запуска отслеживание тега. Не удается получить GUID с помощью службы REST, но вы можете использовать клиентской объектной модели .NET или JavaScript объектной модели. Узнайте,  [как получить идентификатор GUID тега на основе имени тега с помощью объектной модели JavaScript](follow-content-in-sharepoint.md#bk_getTagGuid).</span><span class="sxs-lookup"><span data-stu-id="6dbda-p107">You need the tag GUID to start following a tag. You can't get the GUID by using the REST service, but you can use the .NET client object model or the JavaScript object model. See  [How to get a tag's GUID based on the tag's name by using the JavaScript object model](follow-content-in-sharepoint.md#bk_getTagGuid).</span></span>
  
    
    

### <a name="response"></a><span data-ttu-id="6dbda-204">Ответ</span><span class="sxs-lookup"><span data-stu-id="6dbda-204">Response</span></span>

 <span data-ttu-id="6dbda-205">**IsFollowed**</span><span class="sxs-lookup"><span data-stu-id="6dbda-205">**IsFollowed**</span></span>
  
    
    
<span data-ttu-id="6dbda-206">тип: **bool**</span><span class="sxs-lookup"><span data-stu-id="6dbda-206">Type: **bool**</span></span>
  
    
    
 <span data-ttu-id="6dbda-207">**true**, если текущий пользователь  это пример результата; в противном случае  **false**.</span><span class="sxs-lookup"><span data-stu-id="6dbda-207">**true** if the current user is following the actor; otherwise **false**.</span></span>
  
    
    
<span data-ttu-id="6dbda-208">Приведенный ниже ответ указывает, что пользователь не подписан указанного субъекта.</span><span class="sxs-lookup"><span data-stu-id="6dbda-208">The following response indicates that the user is not following the specified actor.</span></span>
  
    
    



```

{"d":{"IsFollowed":false}}
```


## <a name="my"></a><span data-ttu-id="6dbda-209">Мои</span><span class="sxs-lookup"><span data-stu-id="6dbda-209">My</span></span>
<span data-ttu-id="6dbda-210"><a name="bk_My"> </a></span><span class="sxs-lookup"><span data-stu-id="6dbda-210"></span></span>

<span data-ttu-id="6dbda-211">Получает сведения о **SocialRestFollowingManager** экземпляра и сведения о текущем пользователе.</span><span class="sxs-lookup"><span data-stu-id="6dbda-211">Gets information about the **SocialRestFollowingManager** instance and information about the current user.</span></span>
  
    
    

### <a name="endpoint-uri-structure"></a><span data-ttu-id="6dbda-212">Структура URI конечной точки</span><span class="sxs-lookup"><span data-stu-id="6dbda-212">Endpoint URI structure</span></span>

 <span data-ttu-id="6dbda-213">**GET** `http://<siteCollection>/<site>/_api/social.following/my`</span><span class="sxs-lookup"><span data-stu-id="6dbda-213">**GET** `http://<siteCollection>/<site>/_api/social.following/my`</span></span>
  
    
    

### <a name="request-parameter"></a><span data-ttu-id="6dbda-214">Параметр запроса</span><span class="sxs-lookup"><span data-stu-id="6dbda-214">Request parameter</span></span>

<span data-ttu-id="6dbda-215">Нет.</span><span class="sxs-lookup"><span data-stu-id="6dbda-215">None.</span></span>
  
    
    

### <a name="response"></a><span data-ttu-id="6dbda-216">Ответ</span><span class="sxs-lookup"><span data-stu-id="6dbda-216">Response</span></span>

<span data-ttu-id="6dbda-217">Тип: **SP.Social.SocialRestFollowingManager**</span><span class="sxs-lookup"><span data-stu-id="6dbda-217">Type: **SP.Social.SocialRestFollowingManager**</span></span>
  
    
    
<span data-ttu-id="6dbda-218">сведения об экземпляре **SocialRestFollowingManager** и **MyFollowedDocumentsUri**, **MyFollowedSitesUri**и **SocialActor** свойства для текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="6dbda-218">Information about the **SocialRestFollowingManager** instance, and the **MyFollowedDocumentsUri**, **MyFollowedSitesUri**, and **SocialActor** properties for the current user.</span></span>
  
    
    
<span data-ttu-id="6dbda-219">Приведенный ниже ответ представляет экземпляр **SocialRestFollowingManager** для текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="6dbda-219">The following response represents the **SocialRestFollowingManager** instance for the current user.</span></span>
  
    
    



```
{"d":{
  "__metadata":{
    "id":"https://somecompany-a2ef5dfc05b1da.sharepoint.com/appInstance/_api/social.following/my/following",
    "uri":"https://somecompany-a2ef5dfc05b1da.sharepoint.com/appInstance/_api/social.following/my/following",
    "type":"SP.Social.SocialRestFollowingManager"
  },
  "MyFollowedDocumentsUri":"https://somecompany-my.sharepoint.com/personal/someone_somecompany_onmicrosoft_com/Social/FollowedContent.aspx",
  "MyFollowedSitesUri":"https://somecompany-my.sharepoint.com/personal/someone_somecompany_onmicrosoft_com/Social/Sites.aspx",
  "SocialActor":
    {"__metadata":{"type":"SP.Social.SocialActor"},
    "AccountName":"i:0#.f|membership|someone@somecompany.onmicrosoft.com",
    "ActorType":0,
    "CanFollow":false,
    "ContentUri":null,
    "EmailAddress":"someone@somecompany.onmicrosoft.com",
    "FollowedContentUri":null,
    "Id":"1.0f435d74164149cfa76e19ad21dc7c2e.8a7874906a9348189f2fb83295b598d5.06ff4087162c48dcb43828e4ddf82c38.98b9fc73d5224265b039586688b15b98",
    "ImageUri":"https://somecompany-my.sharepoint.com/User%20Photos/Profile%20Pictures/someone_somecompany_onmicrosoft_com_MThumb.jpg",
    "IsFollowed":false,
    "LibraryUri":null,
    "Name":"User Name",
    "PersonalSiteUri":"https://somecompany-my.sharepoint.com/personal/someone_somecompany_onmicrosoft_com/",
    "Status":0,
    "StatusText":"I like rabbits.",
    "TagGuid":"00000000-0000-0000-0000-000000000000",
    "Title":null,
    "Uri":"https://somecompany-my.sharepoint.com:443/Person.aspx?accountname=i%3A0%23%2Ef%7Cmembership%7Csomeone%40somecompany%2Eonmicrosoft%2Ecom"
  }
}}
```


## <a name="myfolloweddocumentsuri"></a><span data-ttu-id="6dbda-220">Мои/FollowedDocumentsUri</span><span class="sxs-lookup"><span data-stu-id="6dbda-220">My/FollowedDocumentsUri</span></span>
<span data-ttu-id="6dbda-221"><a name="bk_MyFollowedDocumentsUri"> </a></span><span class="sxs-lookup"><span data-stu-id="6dbda-221"></span></span>

<span data-ttu-id="6dbda-222">Возвращает URI на страницу **у меня есть подписка: документы** для текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="6dbda-222">Gets the URI to the **Docs I'm following** page for the current user.</span></span>
  
    
    

### <a name="endpoint-uri-structure"></a><span data-ttu-id="6dbda-223">Структура URI конечной точки</span><span class="sxs-lookup"><span data-stu-id="6dbda-223">Endpoint URI structure</span></span>

 <span data-ttu-id="6dbda-224">**GET** `http://<siteCollection>/<site>/_api/social.following/my/followeddocumentsuri`</span><span class="sxs-lookup"><span data-stu-id="6dbda-224">**GET** `http://<siteCollection>/<site>/_api/social.following/my/followeddocumentsuri`</span></span>
  
    
    

### <a name="request-parameter"></a><span data-ttu-id="6dbda-225">Параметр запроса</span><span class="sxs-lookup"><span data-stu-id="6dbda-225">Request parameter</span></span>

<span data-ttu-id="6dbda-226">Нет.</span><span class="sxs-lookup"><span data-stu-id="6dbda-226">None.</span></span>
  
    
    

### <a name="response"></a><span data-ttu-id="6dbda-227">Ответ</span><span class="sxs-lookup"><span data-stu-id="6dbda-227">Response</span></span>

 <span data-ttu-id="6dbda-228">**FollowedDocumentsUri**</span><span class="sxs-lookup"><span data-stu-id="6dbda-228">**FollowedDocumentsUri**</span></span>
  
    
    
<span data-ttu-id="6dbda-229">тип: **String**</span><span class="sxs-lookup"><span data-stu-id="6dbda-229">Type: **String**</span></span>
  
    
    
<span data-ttu-id="6dbda-230">URI на страницу **у меня есть подписка: документы** для текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="6dbda-230">The URI to the **Docs I'm following** page for the current user.</span></span>
  
    
    
<span data-ttu-id="6dbda-231">Приведенный ниже ответ представляет **FollowedDocumentsUri** для текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="6dbda-231">The following response represents the **FollowedDocumentsUri** for the current user.</span></span>
  
    
    



```

{"d":{"FollowedDocumentsUri":"https://somecompany-my.sharepoint.com/personal/someone_somecompany_onmicrosoft_com/Social/FollowedContent.aspx"}}
```


## <a name="myfollowedsitesuri"></a><span data-ttu-id="6dbda-232">Мои/FollowedSitesUri</span><span class="sxs-lookup"><span data-stu-id="6dbda-232">My/FollowedSitesUri</span></span>
<span data-ttu-id="6dbda-233"><a name="bk_MyFollowedSitesUri"> </a></span><span class="sxs-lookup"><span data-stu-id="6dbda-233"></span></span>

<span data-ttu-id="6dbda-234">Возвращает URI для страницы **сайты, у меня есть подписка** для текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="6dbda-234">Gets the URI to the **Sites I'm following** page for the current user.</span></span>
  
    
    

### <a name="endpoint-uri-structure"></a><span data-ttu-id="6dbda-235">Структура URI конечной точки</span><span class="sxs-lookup"><span data-stu-id="6dbda-235">Endpoint URI structure</span></span>

 <span data-ttu-id="6dbda-236">**GET** `http://<siteCollection>/<site>/_api/social.following/my/followedsitesuri`</span><span class="sxs-lookup"><span data-stu-id="6dbda-236">**GET** `http://<siteCollection>/<site>/_api/social.following/my/followedsitesuri`</span></span>
  
    
    

### <a name="request-parameter"></a><span data-ttu-id="6dbda-237">Параметр запроса</span><span class="sxs-lookup"><span data-stu-id="6dbda-237">Request parameter</span></span>

<span data-ttu-id="6dbda-238">Нет.</span><span class="sxs-lookup"><span data-stu-id="6dbda-238">None.</span></span>
  
    
    

### <a name="response"></a><span data-ttu-id="6dbda-239">Ответ</span><span class="sxs-lookup"><span data-stu-id="6dbda-239">Response</span></span>

 <span data-ttu-id="6dbda-240">**FollowedSitesUri**</span><span class="sxs-lookup"><span data-stu-id="6dbda-240">**FollowedSitesUri**</span></span>
  
    
    
<span data-ttu-id="6dbda-241">тип: **String**</span><span class="sxs-lookup"><span data-stu-id="6dbda-241">Type: **String**</span></span>
  
    
    
<span data-ttu-id="6dbda-242">URI для страницы **сайты, у меня есть подписка** для текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="6dbda-242">The URI to the **Sites I'm following** page for the current user.</span></span>
  
    
    
<span data-ttu-id="6dbda-243">Приведенный ниже ответ представляет **FollowedSitesUri** для текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="6dbda-243">The following response represents the **FollowedSitesUri** for the current user.</span></span>
  
    
    



```
{"d":{"FollowedSitesUri":"https://somecompany-my.sharepoint.com/personal/someone_somecompany_onmicrosoft_com/Social/Sites.aspx"}}
```


## <a name="myfollowed"></a><span data-ttu-id="6dbda-244">Мои/за</span><span class="sxs-lookup"><span data-stu-id="6dbda-244">My/Followed</span></span>
<span data-ttu-id="6dbda-245"><a name="bk_Followed"> </a></span><span class="sxs-lookup"><span data-stu-id="6dbda-245"></span></span>

<span data-ttu-id="6dbda-246">Получает пользователей, документы, сайты и теги, выполнив текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="6dbda-246">Gets users, documents, sites, and tags that the current user is following.</span></span>
  
    
    

### <a name="endpoint-uri-structure"></a><span data-ttu-id="6dbda-247">Структура URI конечной точки</span><span class="sxs-lookup"><span data-stu-id="6dbda-247">Endpoint URI structure</span></span>

 <span data-ttu-id="6dbda-248">**GET** `http://<siteCollection>/<site>/_api/social.following/my/followed(types=15)`</span><span class="sxs-lookup"><span data-stu-id="6dbda-248">**GET** `http://<siteCollection>/<site>/_api/social.following/my/followed(types=15)`</span></span>
  
    
    

### <a name="request-parameter"></a><span data-ttu-id="6dbda-249">Параметр запроса</span><span class="sxs-lookup"><span data-stu-id="6dbda-249">Request parameter</span></span>

 <span data-ttu-id="6dbda-250">_types_</span><span class="sxs-lookup"><span data-stu-id="6dbda-250">_types_</span></span>
  
    
    
<span data-ttu-id="6dbda-251">тип: **Int32**</span><span class="sxs-lookup"><span data-stu-id="6dbda-251">Type: **Int32**</span></span>
  
    
    
<span data-ttu-id="6dbda-p108">типы субъектов для включения. Пользователи = 1, документы = 2, сайты = 4, теги = 8. Побитовое комбинации разрешено.</span><span class="sxs-lookup"><span data-stu-id="6dbda-p108">The actor types to include. Users = 1, Documents = 2, Sites = 4, Tags = 8. Bitwise combinations are allowed.</span></span>
  
    
    

### <a name="response"></a><span data-ttu-id="6dbda-255">Ответ</span><span class="sxs-lookup"><span data-stu-id="6dbda-255">Response</span></span>

 <span data-ttu-id="6dbda-256">**Followed**</span><span class="sxs-lookup"><span data-stu-id="6dbda-256">**Followed**</span></span>
  
    
    
<span data-ttu-id="6dbda-257">тип: массив **SP.Social.SocialActor**</span><span class="sxs-lookup"><span data-stu-id="6dbda-257">Type: Array of **SP.Social.SocialActor**</span></span>
  
    
    
<span data-ttu-id="6dbda-258">пользователей, документы, сайты и теги, выполнив текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="6dbda-258">The users, documents, sites, and tags that the current user is following.</span></span>
  
    
    
<span data-ttu-id="6dbda-p109">Приведенный ниже ответ представляет документ, сайта и тега. Параметр  _types_ в запросе Указывает типы субъектов для включения.</span><span class="sxs-lookup"><span data-stu-id="6dbda-p109">The following response represents a document, a site, and a tag. The  _types_ parameter in the request specifies the types of actors to include.</span></span>
  
    
    



```
{"d":{"Followed":{"results":[
  {"__metadata":{"type":"SP.Social.SocialActor"}
  "AccountName":null
  "ActorType":1
  "CanFollow":true
  "ContentUri":"https://domain.sharepoint.com:443/Shared%20Documents/fileName.docx"
  "EmailAddress":null
  "FollowedContentUri":null
  "Id":"2.089f4944a6374a64b52b7af5ba140392.9340a4837688405daa6b83f2b58f973d.51bbb5d8e214457ba794669345d23040.98b9fc73d5224265b039586688b15b98"
  "ImageUri":null
  "IsFollowed":true
  "LibraryUri":null
  "Name":"snippets.txt"
  "PersonalSiteUri":null
  "Status":0
  "StatusText":null
  "TagGuid":"00000000-0000-0000-0000-000000000000"
  "Title":null
  "Uri":"https://domain.sharepoint.com:443/Shared%20Documents/fileName.docx"}
  {"__metadata":{"type":"SP.Social.SocialActor"}
  "AccountName":null
  "ActorType":2
  "CanFollow":true
  "ContentUri":"https://domain.sharepoint.com:443/"
  "EmailAddress":null
  "FollowedContentUri":null
  "Id":"8.089f4944a6374a64b52b7af5ba140392.9340a4837688405daa6b83f2b58f973d.089f4944a6374a64b52b7af5ba140392.98b9fc73d5224265b039586688b15b98"
  "ImageUri":null
  "IsFollowed":true
  "LibraryUri":null
  "Name":"Developer Site"
  "PersonalSiteUri":null
  "Status":0
  "StatusText":null
  "TagGuid":"00000000-0000-0000-0000-000000000000"
  "Title":null
  "Uri":"https://domain.sharepoint.com:443/"}
  {"__metadata":{"type":"SP.Social.SocialActor"}
  "AccountName":null
  "ActorType":3
  "CanFollow":true
  "ContentUri":null
  "EmailAddress":null
  "FollowedContentUri":null
  "Id":"16.00000000000000000000000000000000.00000000000000000000000000000000.19a4a484c1dc4bc58c93bb96245ce928.98b9fc73d5224265b039586688b15b98"
  "ImageUri":null
  "IsFollowed":true
  "LibraryUri":null
  "Name":"#someTag"
  "PersonalSiteUri":null
  "Status":0
  "StatusText":null
  "TagGuid":"19a4a484-c1dc-4bc5-8c93-bb96245ce928"
  "Title":null
  "Uri":"https://somecompany-my.sharepoint.com:443/_layouts/15/HashTagProfile.aspx?
    TermID=19a4a484-c1dc-4bc5-8c93-bb96245ce928"}
]}}}
```


## <a name="myfollowedcount"></a><span data-ttu-id="6dbda-261">Мои/FollowedCount</span><span class="sxs-lookup"><span data-stu-id="6dbda-261">My/FollowedCount</span></span>
<span data-ttu-id="6dbda-262"><a name="bk_FollowedCount"> </a></span><span class="sxs-lookup"><span data-stu-id="6dbda-262"></span></span>

<span data-ttu-id="6dbda-263">Получает количество пользователей, документы, сайты и теги, выполнив текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="6dbda-263">Gets the count of users, documents, sites, and tags that the current user is following.</span></span>
  
    
    

### <a name="endpoint-uri-structure"></a><span data-ttu-id="6dbda-264">Структура URI конечной точки</span><span class="sxs-lookup"><span data-stu-id="6dbda-264">Endpoint URI structure</span></span>

 <span data-ttu-id="6dbda-265">**GET** `http://<siteCollection>/<site>/_api/social.following/my/followedcount(types=15)`</span><span class="sxs-lookup"><span data-stu-id="6dbda-265">**GET** `http://<siteCollection>/<site>/_api/social.following/my/followedcount(types=15)`</span></span>
  
    
    

### <a name="request-parameter"></a><span data-ttu-id="6dbda-266">Параметр запроса</span><span class="sxs-lookup"><span data-stu-id="6dbda-266">Request parameter</span></span>

 <span data-ttu-id="6dbda-267">_types_</span><span class="sxs-lookup"><span data-stu-id="6dbda-267">_types_</span></span>
  
    
    
<span data-ttu-id="6dbda-268">тип: **Int32**</span><span class="sxs-lookup"><span data-stu-id="6dbda-268">Type: **Int32**</span></span>
  
    
    
<span data-ttu-id="6dbda-p110">типы субъектов для включения. Пользователи = 1, документы = 2, сайты = 4, теги = 8. Побитовое комбинации разрешено.</span><span class="sxs-lookup"><span data-stu-id="6dbda-p110">The types of actors to include. Users = 1, Documents = 2, Sites = 4, Tags = 8. Bitwise combinations are allowed.</span></span>
  
    
    

### <a name="response"></a><span data-ttu-id="6dbda-272">Ответ</span><span class="sxs-lookup"><span data-stu-id="6dbda-272">Response</span></span>

 <span data-ttu-id="6dbda-273">**FollowedCount**</span><span class="sxs-lookup"><span data-stu-id="6dbda-273">**FollowedCount**</span></span>
  
    
    
<span data-ttu-id="6dbda-274">тип: **Int32**</span><span class="sxs-lookup"><span data-stu-id="6dbda-274">Type: **Int32**</span></span>
  
    
    
<span data-ttu-id="6dbda-275">число пользователей, документы, сайты и теги, выполнив текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="6dbda-275">The count of users, documents, sites, and tags that the current user is following.</span></span>
  
    
    
<span data-ttu-id="6dbda-p111">Приведенный ниже ответ указывает, что текущий пользователь является следующие 3 субъекты указанного типа. Параметр  _types_ в запросе Указывает типы субъектов для включения.</span><span class="sxs-lookup"><span data-stu-id="6dbda-p111">The following response indicates that the current user is following 3 actors of the specified type. The  _types_ parameter in the request specifies the types of actors to include.</span></span>
  
    
    



```

{"d":{"FollowedCount":3}}
```


## <a name="myfollowers"></a><span data-ttu-id="6dbda-278">Мои / последователи</span><span class="sxs-lookup"><span data-stu-id="6dbda-278">My/Followers</span></span>
<span data-ttu-id="6dbda-279"><a name="bk_Followers"> </a></span><span class="sxs-lookup"><span data-stu-id="6dbda-279"></span></span>

<span data-ttu-id="6dbda-280">Получает пользователей, которые отслеживаются текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="6dbda-280">Gets the users who are following the current user.</span></span>
  
    
    

### <a name="endpoint-uri-structure"></a><span data-ttu-id="6dbda-281">Структура URI конечной точки</span><span class="sxs-lookup"><span data-stu-id="6dbda-281">Endpoint URI structure</span></span>

 <span data-ttu-id="6dbda-282">**GET** `http://<siteCollection>/<site>/_api/social.following/my/followers`</span><span class="sxs-lookup"><span data-stu-id="6dbda-282">**GET** `http://<siteCollection>/<site>/_api/social.following/my/followers`</span></span>
  
    
    

### <a name="request-parameter"></a><span data-ttu-id="6dbda-283">Параметр запроса</span><span class="sxs-lookup"><span data-stu-id="6dbda-283">Request parameter</span></span>

<span data-ttu-id="6dbda-284">Нет.</span><span class="sxs-lookup"><span data-stu-id="6dbda-284">None.</span></span>
  
    
    

### <a name="response"></a><span data-ttu-id="6dbda-285">Ответ</span><span class="sxs-lookup"><span data-stu-id="6dbda-285">Response</span></span>

 <span data-ttu-id="6dbda-286">**Followers**</span><span class="sxs-lookup"><span data-stu-id="6dbda-286">**Followers**</span></span>
  
    
    
<span data-ttu-id="6dbda-287">тип: массив **SP.Social.SocialActor**</span><span class="sxs-lookup"><span data-stu-id="6dbda-287">Type: Array of **SP.Social.SocialActor**</span></span>
  
    
    

  
    
    
<span data-ttu-id="6dbda-288">Приведенный ниже ответ представляет одного пользователя, выполнив текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="6dbda-288">The following response represents one user who is following the current user.</span></span>
  
    
    



```
{"d":{"Followers":{"results":[
  {"__metadata":{"type":"SP.Social.SocialActor"},
  "AccountName":"domain\\user",
  "ActorType":0, 
  "CanFollow":true, 
  "ContentUri":null, 
  "EmailAddress":"user@domain.com", 
  "FollowedContentUri":null, 
  "Id":"1.60a6bd2d1537446880bb4a5a5b07fd63.3a6c6893e6b549cebffefcfa97412dcf.00093edb336e47ac8791bab0a0b77c5d.0c37852b34d0418e91c62ac25af4be5b",
  "ImageUri":null, 
  "IsFollowed":true, 
  "LibraryUri":null, 
  "Name":"User Name",
  "PersonalSiteUri":"http://server/my/personal/user/",
  "Status":0, 
  "StatusText":"",
  "TagGuid":"00000000-0000-0000-0000-000000000000",
  "Title":"SALES DIRECTOR", 
  "Uri":"http://server:80/my/Person.aspx?accountname=domain%5Cuser"}
]}}}
```


## <a name="mysuggestions"></a><span data-ttu-id="6dbda-289">Мои / предложений</span><span class="sxs-lookup"><span data-stu-id="6dbda-289">My/Suggestions</span></span>
<span data-ttu-id="6dbda-290"><a name="bk_Suggestions"> </a></span><span class="sxs-lookup"><span data-stu-id="6dbda-290"></span></span>

<span data-ttu-id="6dbda-291">Получает пользователей, которые текущий пользователь может потребоваться выполнить.</span><span class="sxs-lookup"><span data-stu-id="6dbda-291">Gets users who the current user might want to follow.</span></span>
  
    
    

> <span data-ttu-id="6dbda-292">**Примечание:** Рекомендации людей функциональные возможности, зависит от следующих действий пользователей, обходы при поиске и аналитика поиска.</span><span class="sxs-lookup"><span data-stu-id="6dbda-292">**Note:** People Suggestions functionality depends on users' following activities, search crawls, and search analytics.</span></span> <span data-ttu-id="6dbda-293">Просмотрите, [как предложения людей можно устанавливать в SharePoint Online](follow-people-in-sharepoint.md#bk_PeopleSuggestions).</span><span class="sxs-lookup"><span data-stu-id="6dbda-293">See  [How People Suggestions works on SharePoint Online](follow-people-in-sharepoint.md#bk_PeopleSuggestions).</span></span> 
  
    
    


### <a name="endpoint-uri-structure"></a><span data-ttu-id="6dbda-294">Структура URI конечной точки</span><span class="sxs-lookup"><span data-stu-id="6dbda-294">Endpoint URI structure</span></span>

 <span data-ttu-id="6dbda-295">**GET** `http://<siteCollection>/<site>/_api/social.following/my/suggestions`</span><span class="sxs-lookup"><span data-stu-id="6dbda-295">**GET** `http://<siteCollection>/<site>/_api/social.following/my/suggestions`</span></span>
  
    
    

### <a name="request-parameter"></a><span data-ttu-id="6dbda-296">Параметр запроса</span><span class="sxs-lookup"><span data-stu-id="6dbda-296">Request parameter</span></span>

<span data-ttu-id="6dbda-297">Нет.</span><span class="sxs-lookup"><span data-stu-id="6dbda-297">None.</span></span>
  
    
    

### <a name="response"></a><span data-ttu-id="6dbda-298">Ответ</span><span class="sxs-lookup"><span data-stu-id="6dbda-298">Response</span></span>

 <span data-ttu-id="6dbda-299">**Suggestions**</span><span class="sxs-lookup"><span data-stu-id="6dbda-299">**Suggestions**</span></span>
  
    
    
<span data-ttu-id="6dbda-300">тип: массив **SP.Social.SocialActor**</span><span class="sxs-lookup"><span data-stu-id="6dbda-300">Type: Array of **SP.Social.SocialActor**</span></span>
  
    
    
<span data-ttu-id="6dbda-301">пользователей, которые текущий пользователь может потребоваться выполнить.</span><span class="sxs-lookup"><span data-stu-id="6dbda-301">Users who the current user might want to follow.</span></span>
  
    
    

## <a name="getmysuggestions"></a><span data-ttu-id="6dbda-302">GetMySuggestions</span><span class="sxs-lookup"><span data-stu-id="6dbda-302">GetMySuggestions</span></span>
<span data-ttu-id="6dbda-303"><a name="bk_GetMySuggestions"> </a></span><span class="sxs-lookup"><span data-stu-id="6dbda-303"></span></span>

<span data-ttu-id="6dbda-304">Получает пользователей, которые текущий пользователь может потребоваться выполнить.</span><span class="sxs-lookup"><span data-stu-id="6dbda-304">Gets users who the current user might want to follow.</span></span>
  
    
    

> <span data-ttu-id="6dbda-305">**Примечание:** Рекомендации людей функциональные возможности, зависит от следующих действий пользователей, обходы при поиске и аналитика поиска.</span><span class="sxs-lookup"><span data-stu-id="6dbda-305">**Note:** People Suggestions functionality depends on users' following activities, search crawls, and search analytics.</span></span> <span data-ttu-id="6dbda-306">Просмотрите, [как предложения людей можно устанавливать в SharePoint Online](follow-people-in-sharepoint.md#bk_PeopleSuggestions).</span><span class="sxs-lookup"><span data-stu-id="6dbda-306">See  [How People Suggestions works on SharePoint Online](follow-people-in-sharepoint.md#bk_PeopleSuggestions).</span></span> 
  
    
    


### <a name="endpoint-uri-structure"></a><span data-ttu-id="6dbda-307">Структура URI конечной точки</span><span class="sxs-lookup"><span data-stu-id="6dbda-307">Endpoint URI structure</span></span>

 <span data-ttu-id="6dbda-308">**GET** `http://<siteCollection>/<site>/_api/sp.userprofiles.peoplemanager/getmysuggestions`</span><span class="sxs-lookup"><span data-stu-id="6dbda-308">**GET** `http://<siteCollection>/<site>/_api/sp.userprofiles.peoplemanager/getmysuggestions`</span></span>
  
    
    

### <a name="request-parameter"></a><span data-ttu-id="6dbda-309">Параметр запроса</span><span class="sxs-lookup"><span data-stu-id="6dbda-309">Request parameter</span></span>

<span data-ttu-id="6dbda-310">Нет.</span><span class="sxs-lookup"><span data-stu-id="6dbda-310">None.</span></span>
  
    
    

### <a name="response"></a><span data-ttu-id="6dbda-311">Ответ</span><span class="sxs-lookup"><span data-stu-id="6dbda-311">Response</span></span>

 <span data-ttu-id="6dbda-312">**Suggestions**</span><span class="sxs-lookup"><span data-stu-id="6dbda-312">**Suggestions**</span></span>
  
    
    
<span data-ttu-id="6dbda-313">тип: список **SP.UserProfiles.PersonProperties**</span><span class="sxs-lookup"><span data-stu-id="6dbda-313">Type: List of **SP.UserProfiles.PersonProperties**</span></span>
  
    
    
<span data-ttu-id="6dbda-314">пользователей, которые текущий пользователь может потребоваться выполнить.</span><span class="sxs-lookup"><span data-stu-id="6dbda-314">Users who the current user might want to follow.</span></span>
  
    
    

## <a name="ismypeoplelistpublic"></a><span data-ttu-id="6dbda-315">IsMyPeopleListPublic</span><span class="sxs-lookup"><span data-stu-id="6dbda-315">IsMyPeopleListPublic</span></span>
<span data-ttu-id="6dbda-316"><a name="bk_IsMyPeopleListPublic"> </a></span><span class="sxs-lookup"><span data-stu-id="6dbda-316"></span></span>

<span data-ttu-id="6dbda-317">Находит ли список **людей, у меня есть подписка** для текущего пользователя, открытый в работе.</span><span class="sxs-lookup"><span data-stu-id="6dbda-317">Finds out whether the **People I'm Following** list for the current user is public.</span></span>
  
    
    

### <a name="endpoint-uri-structure"></a><span data-ttu-id="6dbda-318">Структура URI конечной точки</span><span class="sxs-lookup"><span data-stu-id="6dbda-318">Endpoint URI structure</span></span>

 <span data-ttu-id="6dbda-319">**GET** `http://<siteCollection>/<site>/_api/sp.userprofiles.peoplemanager/ismypeoplelistpublic`</span><span class="sxs-lookup"><span data-stu-id="6dbda-319">**GET** `http://<siteCollection>/<site>/_api/sp.userprofiles.peoplemanager/ismypeoplelistpublic`</span></span>
  
    
    

### <a name="request-parameter"></a><span data-ttu-id="6dbda-320">Параметр запроса</span><span class="sxs-lookup"><span data-stu-id="6dbda-320">Request parameter</span></span>

<span data-ttu-id="6dbda-321">Нет.</span><span class="sxs-lookup"><span data-stu-id="6dbda-321">None.</span></span>
  
    
    

### <a name="response"></a><span data-ttu-id="6dbda-322">Ответ</span><span class="sxs-lookup"><span data-stu-id="6dbda-322">Response</span></span>

 <span data-ttu-id="6dbda-323">**IsMyPeopleListPublic**</span><span class="sxs-lookup"><span data-stu-id="6dbda-323">**IsMyPeopleListPublic**</span></span>
  
    
    
<span data-ttu-id="6dbda-324">тип: **bool**</span><span class="sxs-lookup"><span data-stu-id="6dbda-324">Type: **bool**</span></span>
  
    
    
 <span data-ttu-id="6dbda-325">**true** Если список людей текущий пользователь является открытым; в противном случае  **false**.</span><span class="sxs-lookup"><span data-stu-id="6dbda-325">**true** if the current user's people list is public; otherwise **false**.</span></span>
  
    
    
<span data-ttu-id="6dbda-326">Приведенный ниже ответ указывает, что общедоступные список людей текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="6dbda-326">The following response indicates that the current user's people list is public.</span></span>
  
    
    



```

{"d":{"IsMyPeopleListPublic":true}}
```


## <a name="amifollowedby"></a><span data-ttu-id="6dbda-327">AmIFollowedBy</span><span class="sxs-lookup"><span data-stu-id="6dbda-327">AmIFollowedBy</span></span>
<span data-ttu-id="6dbda-328"><a name="bk_AmIFollowedBy"> </a></span><span class="sxs-lookup"><span data-stu-id="6dbda-328"></span></span>

<span data-ttu-id="6dbda-329">Поиск в работе ли указанный пользователь после текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="6dbda-329">Finds out whether a specified user is following the current user.</span></span>
  
    
    

### <a name="endpoint-uri-structure"></a><span data-ttu-id="6dbda-330">Структура URI конечной точки</span><span class="sxs-lookup"><span data-stu-id="6dbda-330">Endpoint URI structure</span></span>

 <span data-ttu-id="6dbda-331">**GET** `http://<siteCollection>/<site>/_api/sp.userprofiles.peoplemanager/amifollowedby(accountName=@v)?@v='domain\\user'`</span><span class="sxs-lookup"><span data-stu-id="6dbda-331">**GET** `http://<siteCollection>/<site>/_api/sp.userprofiles.peoplemanager/amifollowedby(accountName=@v)?@v='domain\\user'`</span></span>
  
    
    
 <span data-ttu-id="6dbda-332">**GET** `http://<siteCollection>/<site>/_api/sp.userprofiles.peoplemanager/amifollowedby(accountName=@v)?@v='i:0"%23".f|membership|user@domain.com'`</span><span class="sxs-lookup"><span data-stu-id="6dbda-332">**GET** `http://<siteCollection>/<site>/_api/sp.userprofiles.peoplemanager/amifollowedby(accountName=@v)?@v='i:0"%23".f|membership|user@domain.com'`</span></span>
  
    
    

### <a name="request-parameter"></a><span data-ttu-id="6dbda-333">Параметр запроса</span><span class="sxs-lookup"><span data-stu-id="6dbda-333">Request parameter</span></span>

 <span data-ttu-id="6dbda-334">_Имя учетной записи_</span><span class="sxs-lookup"><span data-stu-id="6dbda-334">_accountName_</span></span>
  
    
    
<span data-ttu-id="6dbda-335">тип: **String**</span><span class="sxs-lookup"><span data-stu-id="6dbda-335">Type: **String**</span></span>
  
    
    
<span data-ttu-id="6dbda-336">имя учетной записи конечного пользователя.</span><span class="sxs-lookup"><span data-stu-id="6dbda-336">The account name of the target user.</span></span>
  
    
    

### <a name="response"></a><span data-ttu-id="6dbda-337">Ответ</span><span class="sxs-lookup"><span data-stu-id="6dbda-337">Response</span></span>

 <span data-ttu-id="6dbda-338">**AmIFollowedBy**</span><span class="sxs-lookup"><span data-stu-id="6dbda-338">**AmIFollowedBy**</span></span>
  
    
    
<span data-ttu-id="6dbda-339">тип: **bool**</span><span class="sxs-lookup"><span data-stu-id="6dbda-339">Type: **bool**</span></span>
  
    
    
 <span data-ttu-id="6dbda-340">**true**, если указанный пользователь  это пример текущего пользователя; в противном случае  **false**.</span><span class="sxs-lookup"><span data-stu-id="6dbda-340">**true** if the specified user is following the current user; otherwise **false**.</span></span>
  
    
    
<span data-ttu-id="6dbda-341">Приведенный ниже ответ указывает, что указанный пользователь не подписан текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="6dbda-341">The following response indicates that the specified user is not following the current user.</span></span>
  
    
    



```
{"d":{"AmIFollowedBy":false}}
```


## <a name="getpeoplefollowedby"></a><span data-ttu-id="6dbda-342">GetPeopleFollowedBy</span><span class="sxs-lookup"><span data-stu-id="6dbda-342">GetPeopleFollowedBy</span></span>
<span data-ttu-id="6dbda-343"><a name="bk_GetPeopleFollowedBy"> </a></span><span class="sxs-lookup"><span data-stu-id="6dbda-343"></span></span>

<span data-ttu-id="6dbda-344">Получает пользователей, а затем указанного пользователя.</span><span class="sxs-lookup"><span data-stu-id="6dbda-344">Gets the users followed by a specified user.</span></span>
  
    
    

### <a name="endpoint-uri-structure"></a><span data-ttu-id="6dbda-345">Структура URI конечной точки</span><span class="sxs-lookup"><span data-stu-id="6dbda-345">Endpoint URI structure</span></span>

 <span data-ttu-id="6dbda-346">**GET** `http://<siteCollection>/<site>/_api/sp.userprofiles.peoplemanager/getpeoplefollowedby(accountName=@v)?@v='domain\\user'`</span><span class="sxs-lookup"><span data-stu-id="6dbda-346">**GET** `http://<siteCollection>/<site>/_api/sp.userprofiles.peoplemanager/getpeoplefollowedby(accountName=@v)?@v='domain\\user'`</span></span>
  
    
    
 <span data-ttu-id="6dbda-347">**GET** `http://<siteCollection>/<site>/_api/sp.userprofiles.peoplemanager/getpeoplefollowedby(accountName=@v)?@v='i:0"%23".f|membership|user@domain.com'`</span><span class="sxs-lookup"><span data-stu-id="6dbda-347">**GET** `http://<siteCollection>/<site>/_api/sp.userprofiles.peoplemanager/getpeoplefollowedby(accountName=@v)?@v='i:0"%23".f|membership|user@domain.com'`</span></span>
  
    
    

### <a name="request-parameter"></a><span data-ttu-id="6dbda-348">Параметр запроса</span><span class="sxs-lookup"><span data-stu-id="6dbda-348">Request parameter</span></span>

 <span data-ttu-id="6dbda-349">_Имя учетной записи_</span><span class="sxs-lookup"><span data-stu-id="6dbda-349">_accountName_</span></span>
  
    
    
<span data-ttu-id="6dbda-350">тип: **String**</span><span class="sxs-lookup"><span data-stu-id="6dbda-350">Type: **String**</span></span>
  
    
    
<span data-ttu-id="6dbda-351">имя учетной записи конечного пользователя.</span><span class="sxs-lookup"><span data-stu-id="6dbda-351">The account name of the target user.</span></span>
  
    
    

### <a name="response"></a><span data-ttu-id="6dbda-352">Ответ</span><span class="sxs-lookup"><span data-stu-id="6dbda-352">Response</span></span>

 <span data-ttu-id="6dbda-353">**GetPeopleFollowedBy**</span><span class="sxs-lookup"><span data-stu-id="6dbda-353">**GetPeopleFollowedBy**</span></span>
  
    
    
<span data-ttu-id="6dbda-354">тип: список **SP.UserProfiles.PersonProperties**</span><span class="sxs-lookup"><span data-stu-id="6dbda-354">Type: List of **SP.UserProfiles.PersonProperties**</span></span>
  
    
    
<span data-ttu-id="6dbda-355">пользователей, а затем указанного пользователя.</span><span class="sxs-lookup"><span data-stu-id="6dbda-355">The users followed by the specified user.</span></span>
  
    
    
<span data-ttu-id="6dbda-356">Приведенный ниже ответ представляет два пользователя, а затем указанного пользователя.</span><span class="sxs-lookup"><span data-stu-id="6dbda-356">The following response represents two users followed by the specified user.</span></span>
  
    
    



```
{"d":{"results":[
  {"__metadata":{
    "id":"http://server/sites/dev/_api/SP.UserProfiles.PersonPropertiesa776ccd0-5566-47d2-9d59-3422cf1fb362",
    "uri":"http://server/sites/dev/_api/SP.UserProfiles.PersonPropertiesa776ccd0-5566-47d2-9d59-3422cf1fb362",
    "type":"SP.UserProfiles.PersonProperties"
  },
  "AccountName":"domain\\user1",
  "DirectReports":{"results":[]},
  "DisplayName":"User Name",
  "Email":"user@domain.com",
  "ExtendedManagers":{"results":[]},
  "ExtendedReports":{"results":["domain\\user1"]},
  "IsFollowed":true,
  "LatestPost":null,
  "Peers":{"results":[]},
  "PersonalUrl":"http://server/my/personal/user1/",
  "PictureUrl":null,
  "Title":null,
  "UserProfileProperties":{"results":[
    {"__metadata":{"type":"SP.KeyValue"},"Key":"UserProfile_GUID","Value":"00093edb-336e-47ac-8791-bab0a0b77c5d","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SID","Value":"S-1-5-09-4830882673-197582990-1037597527-29477","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"ADGuid","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"AccountName","Value":"domain\\user1","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"FirstName","Value":"User","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-PhoneticFirstName","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"LastName","Value":"Name","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-PhoneticLastName","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"PreferredName","Value":"User Name","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-PhoneticDisplayName","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"WorkPhone","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"Department","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"Title","Value":"SALES DIRECTOR","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-JobTitle","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-Department","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"Manager","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"AboutMe","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"PersonalSpace","Value":"/my/personal/user1/","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"PictureURL","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"UserName","Value":"user1","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"QuickLinks","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"WebSite","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"PublicSiteRedirect","Value":"http://cox64-096/my/personal/user1/","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-Dotted-line","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-Peers","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-Responsibility","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-SipAddress","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-MySiteUpgrade","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-ProxyAddresses","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-HireDate","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-DisplayOrder","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-ClaimID","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-ClaimProviderID","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-ClaimProviderType","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-SavedAccountName","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-SavedSID","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-ResourceSID","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-ResourceAccountName","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-ObjectExists","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-MasterAccountName","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-UserPrincipalName","Value":"user1@company.com","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-PersonalSiteCapabilities","Value":"14","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-O15FirstRunExperience","Value":"15","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-PersonalSiteInstantiationState","Value":"2","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-DistinguishedName","Value":"CN=user1 (User Name),OU=UserAccounts,DC=domain,DC=corp,DC=company,DC=com","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-SourceObjectDN","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-FeedIdentifier","Value":"http://server/my/personal/user1;1.60a6bd2d1537446880bb4a5a5b07fd63.3a6c6893e6b549cebffefcfa97412dcf.50dcee8186ae4dd6904d1650d3d39e54.0c37852b34d0418e91c62ac25af4be5b","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"WorkEmail","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"CellPhone","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"Fax","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"HomePhone","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"Office","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-Location","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"Assistant","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-PastProjects","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-Skills","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-School","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-Birthday","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-StatusNotes","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-Interests","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-HashTags","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-EmailOptin","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-PrivacyPeople","Value":"True","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-PrivacyActivity","Value":"4095","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-TimeZone","Value":"","ValueType":"Edm.String"}]
  },
  "UserUrl":"http://server:80/my/Person.aspx?accountname=domain%5Cuser1"},
  {"__metadata":{
    "id":"http://server/sites/dev/_api/SP.UserProfiles.PersonPropertiesf0ddf6e4-e69c-453f-9a7f-44e0e47d89d4",
    "uri":"http://server/sites/dev/_api/SP.UserProfiles.PersonPropertiesf0ddf6e4-e69c-453f-9a7f-44e0e47d89d4",
    "type":"SP.UserProfiles.PersonProperties"},
  "AccountName":"domain\\user2",
  "DirectReports":{"results":[]},
  "DisplayName":"User Name",
  "Email":"user2@company.com", 
  "ExtendedManagers":{"results":[]},
  "ExtendedReports":{"results":["domain\\user2"]},
  "IsFollowed":true,"LatestPost":null, 
  "Peers":{"results":[]},
  "PersonalUrl":"http://server/my/Person.aspx?accountname=domain%5Cuser2",
  "PictureUrl":null, 
  "Title":null, 
  "UserProfileProperties":{"results":[
    {"__metadata":{"type":"SP.KeyValue"},"Key":"UserProfile_GUID","Value":"40deca2e-6231-43f9-9559-9a51b0135067","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SID","Value":" S-1-5-09-4830882673-197582990-1037597527-0688328","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"ADGuid","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"AccountName","Value":"domain\\user2","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"FirstName","Value":"User","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-PhoneticFirstName","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"LastName","Value":"Name","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-PhoneticLastName","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"PreferredName","Value":"User2","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-PhoneticDisplayName","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"WorkPhone","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"Department","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"Title","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-JobTitle","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-Department","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"Manager","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"AboutMe","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"PersonalSpace","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"PictureURL","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"UserName","Value":"user2","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"QuickLinks","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"WebSite","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"PublicSiteRedirect","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-Dotted-line","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-Peers","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-Responsibility","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-SipAddress","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-MySiteUpgrade","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-ProxyAddresses","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-HireDate","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-DisplayOrder","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-ClaimID","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-ClaimProviderID","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-ClaimProviderType","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-SavedAccountName","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-SavedSID","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-ResourceSID","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-ResourceAccountName","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-ObjectExists","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-MasterAccountName","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-UserPrincipalName","Value":"user2@company.com","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-PersonalSiteCapabilities","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-O15FirstRunExperience","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-PersonalSiteInstantiationState","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-DistinguishedName","Value":"CN=User2,OU=UserAccounts,DC=domain,DC=corp,DC=company,DC=com","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-SourceObjectDN","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-FeedIdentifier","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"WorkEmail","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"CellPhone","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"Fax","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"HomePhone","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"Office","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-Location","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"Assistant","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-PastProjects","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-Skills","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-School","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-Birthday","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-StatusNotes","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-Interests","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-HashTags","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-EmailOptin","Value":"0","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-PrivacyPeople","Value":"True","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-PrivacyActivity","Value":"4095","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-TimeZone","Value":"","ValueType":"Edm.String"}]
  },
  "UserUrl":"http://server:80/my/Person.aspx?accountname=domain%5Cuser2"}
]}}
```


## <a name="getfollowersfor"></a><span data-ttu-id="6dbda-357">GetFollowersFor</span><span class="sxs-lookup"><span data-stu-id="6dbda-357">GetFollowersFor</span></span>
<span data-ttu-id="6dbda-358"><a name="bk_GetFollowersFor"> </a></span><span class="sxs-lookup"><span data-stu-id="6dbda-358"></span></span>

<span data-ttu-id="6dbda-359">Получает пользователей, которые отслеживаются указанного пользователя.</span><span class="sxs-lookup"><span data-stu-id="6dbda-359">Gets the users who are following a specified user.</span></span>
  
    
    

### <a name="endpoint-uri-structure"></a><span data-ttu-id="6dbda-360">Структура URI конечной точки</span><span class="sxs-lookup"><span data-stu-id="6dbda-360">Endpoint URI structure</span></span>

 <span data-ttu-id="6dbda-361">**GET** `http://<siteCollection>/<site>/_api/sp.userprofiles.peoplemanager/getfollowersfor(accountName=@v)?@v='domain\\user'`</span><span class="sxs-lookup"><span data-stu-id="6dbda-361">**GET** `http://<siteCollection>/<site>/_api/sp.userprofiles.peoplemanager/getfollowersfor(accountName=@v)?@v='domain\\user'`</span></span>
  
    
    
 <span data-ttu-id="6dbda-362">**GET** `http://<siteCollection>/<site>/_api/sp.userprofiles.peoplemanager/getfollowersfor(accountName=@v)?@v='i:0"%23".f|membership|user@domain.com'`</span><span class="sxs-lookup"><span data-stu-id="6dbda-362">**GET** `http://<siteCollection>/<site>/_api/sp.userprofiles.peoplemanager/getfollowersfor(accountName=@v)?@v='i:0"%23".f|membership|user@domain.com'`</span></span>
  
    
    

### <a name="request-parameter"></a><span data-ttu-id="6dbda-363">Параметр запроса</span><span class="sxs-lookup"><span data-stu-id="6dbda-363">Request parameter</span></span>

 <span data-ttu-id="6dbda-364">_Имя учетной записи_</span><span class="sxs-lookup"><span data-stu-id="6dbda-364">_accountName_</span></span>
  
    
    
<span data-ttu-id="6dbda-365">тип: **String**</span><span class="sxs-lookup"><span data-stu-id="6dbda-365">Type: **String**</span></span>
  
    
    
<span data-ttu-id="6dbda-366">имя учетной записи конечного пользователя.</span><span class="sxs-lookup"><span data-stu-id="6dbda-366">The account name of the target user.</span></span>
  
    
    

### <a name="response"></a><span data-ttu-id="6dbda-367">Ответ</span><span class="sxs-lookup"><span data-stu-id="6dbda-367">Response</span></span>

 <span data-ttu-id="6dbda-368">**GetFollowersFor**</span><span class="sxs-lookup"><span data-stu-id="6dbda-368">**GetFollowersFor**</span></span>
  
    
    
<span data-ttu-id="6dbda-369">тип: список **SP.UserProfiles.PersonProperties**</span><span class="sxs-lookup"><span data-stu-id="6dbda-369">Type: List of **SP.UserProfiles.PersonProperties**</span></span>
  
    
    
<span data-ttu-id="6dbda-370">пользователей, которые отслеживаются указанного пользователя.</span><span class="sxs-lookup"><span data-stu-id="6dbda-370">The users who are following the specified user.</span></span>
  
    
    
<span data-ttu-id="6dbda-371">Приведенный ниже ответ  пользователь, которому после указанного пользователя.</span><span class="sxs-lookup"><span data-stu-id="6dbda-371">The following response represents a user who is following the specified user.</span></span>
  
    
    



```

{"d":{"results":[
  {"__metadata":{
    "id":"http://server/sites/dev/_api/SP.UserProfiles.PersonPropertiesabe0c40e-ce77-4631-9fc9-ec20b859061c",
    "uri":"http://server/sites/dev/_api/SP.UserProfiles.PersonPropertiesabe0c40e-ce77-4631-9fc9-ec20b859061c",
    "type":"SP.UserProfiles.PersonProperties"
  },
  "AccountName":"domain\\user",
  "DirectReports":{"results":[]},
  "DisplayName":"User Name",
  "Email":"user@domain.com",
  "ExtendedManagers":{"results":[]},
  "ExtendedReports":{"results":["domain\\user"]},
  "IsFollowed":false,
  "LatestPost":"#tally",
  "Peers":{"results":[]},
  "PersonalUrl":"http://server/my/personal/user/",
  "PictureUrl":null,
  "Title":"MARKETING DIRECTOR",
  "UserProfileProperties":{"results":[
    {"__metadata":{"type":"SP.KeyValue"},"Key":"UserProfile_GUID","Value":"fa59ba73-edd4-4dc9-97d1-8ada702aae7f","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SID","Value":" S-1-5-09-4830882673-197582990-1037597527-002428","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"ADGuid","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"AccountName","Value":"domain\\user","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"FirstName","Value":"User","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-PhoneticFirstName","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"LastName","Value":"Name","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-PhoneticLastName","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"PreferredName","Value":"User Name","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-PhoneticDisplayName","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"WorkPhone","Value":"+1 (208) 3192190 X2190","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"Department","Value":"Marketing","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"Title","Value":"MARKETING DIRECTOR","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-JobTitle","Value":"MARKETING DIRECTOR","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-Department","Value":"Marketing","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"Manager","Value":"DOMAIN\\randalli","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"AboutMe","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"PersonalSpace","Value":"/my/personal/user/","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"PictureURL","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"UserName","Value":"user","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"QuickLinks","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"WebSite","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"PublicSiteRedirect","Value":"http://my/sites/user/","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-DataSource","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-MemberOf","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-Dotted-line","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-Peers","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-Responsibility","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-SipAddress","Value":"user@domain.com","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-MySiteUpgrade","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-DontSuggestList","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-ProxyAddresses","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-HireDate","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-DisplayOrder","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-ClaimID","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-ClaimProviderID","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-ClaimProviderType","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-LastColleagueAdded","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-OWAUrl","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-SavedAccountName","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-SavedSID","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-ResourceSID","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-ResourceAccountName","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-ObjectExists","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-MasterAccountName","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-UserPrincipalName","Value":"user@domain.com","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-PersonalSiteCapabilities","Value":"14","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-O15FirstRunExperience","Value":"15","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-PersonalSiteInstantiationState","Value":"2","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-DistinguishedName","Value":"CN=User Name,OU=UserAccounts,DC=domain,DC=corp,DC=company,DC=com","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-SourceObjectDN","Value":"CN=User Name,OU=UserAccounts,DC=domain,DC=corp,DC=company,DC=com","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-LastKeywordAdded","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-FeedIdentifier","Value":"http://server/my/personal/user;1.64769ec247734e699a5616f1701f7d94.ab42c829ec534daa99fc5909ef940213.3fb2a502be274948a665fcb5e8b2a58d.0c37852b34d0418e91c62ac25af4be5b","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"WorkEmail","Value":"user@domain.com","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"CellPhone","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"Fax","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"HomePhone","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"Office","Value":"2253","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-Location","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"Assistant","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-PastProjects","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-Skills","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-School","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-Birthday","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-StatusNotes","Value":"#tally","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-Interests","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-HashTags","Value":"#tally","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-EmailOptin","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-PrivacyPeople","Value":"True","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-PrivacyActivity","Value":"4095","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-MUILanguages","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-ContentLanguages","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-TimeZone","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-RegionalSettings-FollowWeb","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-Locale","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-CalendarType","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-AltCalendarType","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-AdjustHijriDays","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-ShowWeeks","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-WorkDays","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-WorkDayStartHour","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-WorkDayEndHour","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-Time24","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-FirstDayOfWeek","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-FirstWeekOfYear","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SPS-RegionalSettings-Initialized","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"EduUserRole","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"EduPersonalSiteState","Value":"","ValueType":"Edm.String"}, 
    {"__metadata":{"type":"SP.KeyValue"},"Key":"EduOAuthTokenProviders","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"SISUserId","Value":"","ValueType":"Edm.String"},
    {"__metadata":{"type":"SP.KeyValue"},"Key":"EduExternalSyncState","Value":"","ValueType":"Edm.String"}]
  },
  "UserUrl":"http://server:80/my/Person.aspx?accountname=domain%5Cuser"}
]}}
```


## <a name="additional-resources"></a><span data-ttu-id="6dbda-372">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="6dbda-372">Additional resources</span></span>
<span data-ttu-id="6dbda-373"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="6dbda-373"></span></span>


-  [<span data-ttu-id="6dbda-374">Как: выполните документы, сайты и теги с помощью службы REST в SharePoint</span><span class="sxs-lookup"><span data-stu-id="6dbda-374">How to: Follow documents, sites, and tags by using the REST service in SharePoint</span></span>](how-to-follow-documents-sites-and-tags-by-using-the-rest-service-in-sharepoint-2.md)
    
  
-  [<span data-ttu-id="6dbda-375">Social feed REST API reference for SharePoint</span><span class="sxs-lookup"><span data-stu-id="6dbda-375">Social feed REST API reference for SharePoint</span></span>](social-feed-rest-api-reference-for-sharepoint.md)
    
  
-  [<span data-ttu-id="6dbda-376">SharePoint User Profiles JavaScript Reference (sp.userprofiles.js)</span><span class="sxs-lookup"><span data-stu-id="6dbda-376">SharePoint User Profiles JavaScript Reference (sp.userprofiles.js)</span></span>](http://msdn.microsoft.com/library/80cf5436-6aa2-6f11-a782-66a04f6e2fb0%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="6dbda-377">Начало разработки с использованием социальных функций в SharePoint</span><span class="sxs-lookup"><span data-stu-id="6dbda-377">Get started developing with social features in SharePoint</span></span>](get-started-developing-with-social-features-in-sharepoint.md)
    
  
