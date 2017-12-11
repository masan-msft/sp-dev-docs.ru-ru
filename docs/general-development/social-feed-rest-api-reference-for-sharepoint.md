---
title: "Социальные канал Справочник по интерфейсу API службы REST для SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: f1cb914f-1e91-4e23-bf53-d2ab323eac13
ms.openlocfilehash: 2cb778e590d8c504bcaf5b962a6345cf581e9e6b
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="social-feed-rest-api-reference-for-sharepoint"></a><span data-ttu-id="43a62-102">Социальные канал Справочник по интерфейсу API службы REST для SharePoint</span><span class="sxs-lookup"><span data-stu-id="43a62-102">Social feed REST API reference for SharePoint</span></span>
<span data-ttu-id="43a62-103">Поиск конечных точек SharePoint REST для чтения и записи в социальных веб-каналов с помощью **SocialRestFeedManager** ресурсов.</span><span class="sxs-lookup"><span data-stu-id="43a62-103">Find SharePoint REST endpoints for reading and writing to social feeds by using the **SocialRestFeedManager** resource.</span></span>
<span data-ttu-id="43a62-104">Службы SharePoint представлений состояния (REST) позволяет выполнять те же действия, которые можно выполнять с помощью клиентской объектной модели .NET и объектной модели JavaScript.</span><span class="sxs-lookup"><span data-stu-id="43a62-104">You can use the SharePoint Representational State Transfer (REST) service to do the same things that you can do with the .NET client object models and the JavaScript object model.</span></span> <span data-ttu-id="43a62-105">Служба REST предоставляет ресурсы, которые соответствуют объектов SharePoint, свойств и методов.</span><span class="sxs-lookup"><span data-stu-id="43a62-105">The REST service exposes resources that correspond to SharePoint objects, properties, and methods.</span></span> <span data-ttu-id="43a62-106">Для использования службы REST, построение и отправлять запросы **POST** и HTTP **GET** конечных точек ресурсов, которые представляют задачи, которые необходимо выполнить.</span><span class="sxs-lookup"><span data-stu-id="43a62-106">To use the REST service, you build and send HTTP **GET** and **POST** requests to the resource endpoints that represent the tasks you want to do.</span></span>
  
    
    

<span data-ttu-id="43a62-107">URI конечных точек для задач, наиболее веб-канала активности начинаются с ресурсом **SocialRestFeedManager** ( `social.feed`), за которым следует  `my` ресурсов или ресурсов `post` :</span><span class="sxs-lookup"><span data-stu-id="43a62-107">The endpoint URIs for most feed tasks begin with the **SocialRestFeedManager** resource ( `social.feed`), followed by the  `my` resource or the `post` resource:</span></span>
- <span data-ttu-id="43a62-p102">Ресурс  `my` представляет текущего пользователя. При использовании встроенных в URI конечной точки контекста запроса задает для текущего пользователя. Например `http://contoso.com/_api/social.feed/my/news` возвращает канала новостей для текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="43a62-p102">The  `my` resource represents the current user. When used inline in the endpoint URI, it sets the context of the request to the current user. For example, `http://contoso.com/_api/social.feed/my/news` gets the newsfeed for the current user.</span></span>
    
  
- <span data-ttu-id="43a62-p103">Представляет ресурс  `post` конкретного потока или post. При использовании встроенных в URI конечной точки контекста запроса задает для указанного потока или post. Например `http://contoso.com/_api/social.feed/post/lock` блокирует указанного потока.</span><span class="sxs-lookup"><span data-stu-id="43a62-p103">The  `post` resource represents a specific thread or post. When used inline in the endpoint URI, it sets the context of the request to the specified thread or post. For example, `http://contoso.com/_api/social.feed/post/lock` locks the specified thread.</span></span>
    
  
<span data-ttu-id="43a62-p104">Если в конечную точку ресурса с параметром, метаданные параметров указан в URI или в тексте запроса. По умолчанию службы REST возвращает ответов, отформатированные в протоколе Atom, но можно запросить формат JSON с помощью **Accept** заголовки HTTP. В разделе примеры запросов на полный [Пример запросов REST для задач, веб-канала активности](social-feed-rest-api-reference-for-sharepoint.md#bk_exampleRequests) .</span><span class="sxs-lookup"><span data-stu-id="43a62-p104">If the resource endpoint takes a parameter, the parameter metadata is specified in the URI or in the request body. By default, the REST service returns responses formatted in the Atom protocol, but you can request the JSON format by using HTTP **Accept** headers. See [Example REST requests for feed tasks](social-feed-rest-api-reference-for-sharepoint.md#bk_exampleRequests) for examples of complete requests.</span></span>
## <a name="resource-endpoints-for-feed-tasks"></a><span data-ttu-id="43a62-117">Конечные точки ресурсов для задач, веб-канала активности</span><span class="sxs-lookup"><span data-stu-id="43a62-117">Resource endpoints for feed tasks</span></span>
<span data-ttu-id="43a62-118"><a name="bk_Overview"> </a></span><span class="sxs-lookup"><span data-stu-id="43a62-118"></span></span>


|<span data-ttu-id="43a62-119">**Конечная точка**</span><span class="sxs-lookup"><span data-stu-id="43a62-119">**Endpoint**</span></span>|<span data-ttu-id="43a62-120">**Описание**</span><span class="sxs-lookup"><span data-stu-id="43a62-120">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="43a62-121">Мои</span><span class="sxs-lookup"><span data-stu-id="43a62-121">My</span></span>](social-feed-rest-api-reference-for-sharepoint.md#bk_my)|<span data-ttu-id="43a62-122">Получает сведения о текущем пользователе.</span><span class="sxs-lookup"><span data-stu-id="43a62-122">Gets information about the current user.</span></span>|
| [<span data-ttu-id="43a62-123">Мои/канал/Post</span><span class="sxs-lookup"><span data-stu-id="43a62-123">My/Feed/Post</span></span>](social-feed-rest-api-reference-for-sharepoint.md#bk_myFeedPost)|<span data-ttu-id="43a62-124">Создает корневой post в канал для текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="43a62-124">Creates a root post in the current user's feed.</span></span>|
| [<span data-ttu-id="43a62-125">Мой канал /</span><span class="sxs-lookup"><span data-stu-id="43a62-125">My/Feed</span></span>](social-feed-rest-api-reference-for-sharepoint.md#bk_myFeed)|<span data-ttu-id="43a62-126">Получает веб-канал активности для текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="43a62-126">Gets the feed of activity by the current user.</span></span>|
| [<span data-ttu-id="43a62-127">Мои / новостей</span><span class="sxs-lookup"><span data-stu-id="43a62-127">My/News</span></span>](social-feed-rest-api-reference-for-sharepoint.md#bk_myNews)|<span data-ttu-id="43a62-128">Получает веб-канал активности для текущего пользователя и людей и контент, который подписан пользователь.</span><span class="sxs-lookup"><span data-stu-id="43a62-128">Gets the feed of activity by the current user and by people and content the user is following.</span></span>|
| [<span data-ttu-id="43a62-129">Мои/TimelineFeed</span><span class="sxs-lookup"><span data-stu-id="43a62-129">My/TimelineFeed</span></span>](social-feed-rest-api-reference-for-sharepoint.md#bk_myTimelineFeed)|<span data-ttu-id="43a62-130">Получает веб-канал активности путем текущего пользователя и людей и содержимое, выполнив пользователя, отсортированные по дате создания.</span><span class="sxs-lookup"><span data-stu-id="43a62-130">Gets the feed of activity by the current user and by people and content the user is following, sorted by created date.</span></span>|
| [<span data-ttu-id="43a62-131">Мои аудио- и оценки</span><span class="sxs-lookup"><span data-stu-id="43a62-131">My/Likes</span></span>](social-feed-rest-api-reference-for-sharepoint.md#bk_myLikes)|<span data-ttu-id="43a62-132">Получает веб-канал публикации, которые нравится текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="43a62-132">Gets the feed of posts that the current user likes.</span></span>|
| [<span data-ttu-id="43a62-133">Мои/MentionFeed</span><span class="sxs-lookup"><span data-stu-id="43a62-133">My/MentionFeed</span></span>](social-feed-rest-api-reference-for-sharepoint.md#bk_myMentionFeed)|<span data-ttu-id="43a62-134">Получает веб-канал сообщения, содержащие упоминание текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="43a62-134">Gets the feed of posts that mention the current user.</span></span>|
| [<span data-ttu-id="43a62-135">Мои/MentionFeed/ClearUnreadMentionCount</span><span class="sxs-lookup"><span data-stu-id="43a62-135">My/MentionFeed/ClearUnreadMentionCount</span></span>](social-feed-rest-api-reference-for-sharepoint.md#bk_myMentionFeedClearUnreadMentionCount)|<span data-ttu-id="43a62-136">Получает веб-канал сообщения, содержащие упоминание текущего пользователя и очищает счетчик непрочитанных упоминание.</span><span class="sxs-lookup"><span data-stu-id="43a62-136">Gets the feed of posts that mention the current user and clears the unread mention count.</span></span>|
| [<span data-ttu-id="43a62-137">Мои/UnreadMentionCount</span><span class="sxs-lookup"><span data-stu-id="43a62-137">My/UnreadMentionCount</span></span>](social-feed-rest-api-reference-for-sharepoint.md#bk_myUnreadMentionCount)|<span data-ttu-id="43a62-138">Возвращает количество непрочитанных упоминания для текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="43a62-138">Gets the count of unread mentions for the current user.</span></span>|
| [<span data-ttu-id="43a62-139">Actor (субъект)</span><span class="sxs-lookup"><span data-stu-id="43a62-139">Actor</span></span>](social-feed-rest-api-reference-for-sharepoint.md#bk_actor)|<span data-ttu-id="43a62-140">Получает сведения о указанного пользователя и текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="43a62-140">Gets information about the specified user and the current user.</span></span>|
| [<span data-ttu-id="43a62-141">Actor/веб-канал</span><span class="sxs-lookup"><span data-stu-id="43a62-141">Actor/Feed</span></span>](social-feed-rest-api-reference-for-sharepoint.md#bk_actorFeed)|<span data-ttu-id="43a62-142">Получает веб-канал активности по указанному пользователю.</span><span class="sxs-lookup"><span data-stu-id="43a62-142">Gets the feed of activity by the specified user.</span></span>|
| [<span data-ttu-id="43a62-143">Actor/канал/Post</span><span class="sxs-lookup"><span data-stu-id="43a62-143">Actor/Feed/Post</span></span>](social-feed-rest-api-reference-for-sharepoint.md#bk_actorFeedPost)|<span data-ttu-id="43a62-144">Создает корневой post в указанном веб-канал сайта.</span><span class="sxs-lookup"><span data-stu-id="43a62-144">Creates a root post in the specified site feed.</span></span>|
| [<span data-ttu-id="43a62-145">Публикация</span><span class="sxs-lookup"><span data-stu-id="43a62-145">Post</span></span>](social-feed-rest-api-reference-for-sharepoint.md#bk_post)|<span data-ttu-id="43a62-146">Получает полный поток, который содержит указанный post.</span><span class="sxs-lookup"><span data-stu-id="43a62-146">Gets a full thread that contains the specified post.</span></span>|
| [<span data-ttu-id="43a62-147">Поместить/ответ</span><span class="sxs-lookup"><span data-stu-id="43a62-147">Post/Reply</span></span>](social-feed-rest-api-reference-for-sharepoint.md#bk_postReply)|<span data-ttu-id="43a62-148">Публикации в ответ на указанном post.</span><span class="sxs-lookup"><span data-stu-id="43a62-148">Posts a reply to the specified post.</span></span>|
| [<span data-ttu-id="43a62-149">Запись и удаление</span><span class="sxs-lookup"><span data-stu-id="43a62-149">Post/Delete</span></span>](social-feed-rest-api-reference-for-sharepoint.md#bk_postDelete)|<span data-ttu-id="43a62-150">Удаляет указанный post.</span><span class="sxs-lookup"><span data-stu-id="43a62-150">Deletes the specified post.</span></span>|
| [<span data-ttu-id="43a62-151">Публикация/Like</span><span class="sxs-lookup"><span data-stu-id="43a62-151">Post/Like</span></span>](social-feed-rest-api-reference-for-sharepoint.md#bk_postLike)|<span data-ttu-id="43a62-152">Делает текущий пользователь liker из указанного сообщения.</span><span class="sxs-lookup"><span data-stu-id="43a62-152">Makes the current user a liker of the specified post.</span></span>|
| [<span data-ttu-id="43a62-153">Учет аудио- и в отличие от</span><span class="sxs-lookup"><span data-stu-id="43a62-153">Post/Unlike</span></span>](social-feed-rest-api-reference-for-sharepoint.md#bk_postUnlike)|<span data-ttu-id="43a62-154">Текущий пользователь удаляется из списка likers для указанного сообщения.</span><span class="sxs-lookup"><span data-stu-id="43a62-154">Removes the current user from the list of likers for the specified post.</span></span>|
| [<span data-ttu-id="43a62-155">Публикация/Likers</span><span class="sxs-lookup"><span data-stu-id="43a62-155">Post/Likers</span></span>](social-feed-rest-api-reference-for-sharepoint.md#bk_postLikers)|<span data-ttu-id="43a62-156">Получает пользователей, как указанного сообщения.</span><span class="sxs-lookup"><span data-stu-id="43a62-156">Gets the users who like the specified post.</span></span>|
| [<span data-ttu-id="43a62-157">Публикация/блокировки</span><span class="sxs-lookup"><span data-stu-id="43a62-157">Post/Lock</span></span>](social-feed-rest-api-reference-for-sharepoint.md#bk_postLock)|<span data-ttu-id="43a62-158">Блокирует указанного потока.</span><span class="sxs-lookup"><span data-stu-id="43a62-158">Locks the specified thread.</span></span>|
| [<span data-ttu-id="43a62-159">POST или разблокировать</span><span class="sxs-lookup"><span data-stu-id="43a62-159">Post/Unlock</span></span>](social-feed-rest-api-reference-for-sharepoint.md#bk_postUnlock)|<span data-ttu-id="43a62-160">Разблокирует указанного потока.</span><span class="sxs-lookup"><span data-stu-id="43a62-160">Unlocks the specified thread.</span></span>|
   
> [!NOTE]
> <span data-ttu-id="43a62-161">[!Примечание] Следующие ресурсы REST, связанных с каналами использовать по той же схеме как другие интерфейсы API REST SharePoint для построения URI конечной точки.> Для **CreateImageAttachment**отправьте запрос **POST** `http://<siteCollection>/<site>/_api/SP.Social.SocialFeedManager/CreateImageAttachment`> Для **GetPreview**отправьте запрос **POST** `http://<siteCollection>/<site>/_api/SP.Social.SocialFeedManager/GetPreview`> Для **SuppressThreadNotifications**отправьте запрос **POST** `http://<siteCollection>/<site>/_api/SP.Social.SocialFeedManager/SuppressThreadNotifications`</span><span class="sxs-lookup"><span data-stu-id="43a62-161">The following feed-related REST resources use the same pattern as the other SharePoint REST APIs to construct the endpoint URI.>  For **CreateImageAttachment**, send a **POST** request to `http://<siteCollection>/<site>/_api/SP.Social.SocialFeedManager/CreateImageAttachment`>  For **GetPreview**, send a **POST** request to `http://<siteCollection>/<site>/_api/SP.Social.SocialFeedManager/GetPreview`>  For **SuppressThreadNotifications**, send a **POST** request to `http://<siteCollection>/<site>/_api/SP.Social.SocialFeedManager/SuppressThreadNotifications`</span></span>
  
    
    


## <a name="my"></a><span data-ttu-id="43a62-162">Мои</span><span class="sxs-lookup"><span data-stu-id="43a62-162">My</span></span>
<span data-ttu-id="43a62-163"><a name="bk_my"> </a></span><span class="sxs-lookup"><span data-stu-id="43a62-163"></span></span>

<span data-ttu-id="43a62-164">Получает сведения о текущем пользователе.</span><span class="sxs-lookup"><span data-stu-id="43a62-164">Gets information about the current user.</span></span>
  
    
    
<span data-ttu-id="43a62-p105">Конечная точка **my** устанавливает текущего пользователя в качестве контекста для любой последующих ресурсов в URI. Например `http://contoso.com/_api/social.feed/my/news` возвращает канала новостей для текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="43a62-p105">The **my** endpoint sets the current user as the context for any subsequent resource in the URI. For example, `http://contoso.com/_api/social.feed/my/news` gets the newsfeed for the current user.</span></span>
  
    
    

### <a name="endpoint-uri-structure"></a><span data-ttu-id="43a62-167">Структура URI конечной точки</span><span class="sxs-lookup"><span data-stu-id="43a62-167">Endpoint URI structure</span></span>

 <span data-ttu-id="43a62-168">**GET** `http://<siteCollection>/<site>/_api/social.feed/my`</span><span class="sxs-lookup"><span data-stu-id="43a62-168">**GET** `http://<siteCollection>/<site>/_api/social.feed/my`</span></span>
  
    
    

### <a name="request-parameter"></a><span data-ttu-id="43a62-169">Параметр запроса</span><span class="sxs-lookup"><span data-stu-id="43a62-169">Request parameter</span></span>

<span data-ttu-id="43a62-170">Нет.</span><span class="sxs-lookup"><span data-stu-id="43a62-170">None.</span></span>
  
    
    

### <a name="response"></a><span data-ttu-id="43a62-171">Ответ</span><span class="sxs-lookup"><span data-stu-id="43a62-171">Response</span></span>

<span data-ttu-id="43a62-172">Тип:  [SP. Social.SocialRestActor](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestActor)</span><span class="sxs-lookup"><span data-stu-id="43a62-172">Type:  [SP.Social.SocialRestActor](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestActor)</span></span>
  
    
    
<span data-ttu-id="43a62-173">сведения о текущем пользователе.</span><span class="sxs-lookup"><span data-stu-id="43a62-173">Information about the current user.</span></span>
  
    
    
<span data-ttu-id="43a62-174">Свойства **SocialRestActor** можно вызвать по отдельности в URI, например `http://<siteCollection>/<site>/_api/social.feed/my/me` возвращает только свойство **Me**.</span><span class="sxs-lookup"><span data-stu-id="43a62-174">You can call **SocialRestActor** properties individually in the URI, for example `http://<siteCollection>/<site>/_api/social.feed/my/me` gets only the **Me** property.</span></span>
  
    
    
<span data-ttu-id="43a62-175">В следующем примере ответа представляет сведения о текущем пользователе.</span><span class="sxs-lookup"><span data-stu-id="43a62-175">The following response example represents information about the current user.</span></span>
  
    
    



```

{"d":{
  "__metadata":{
    "id":"http://serverName/sites/dev/_api/social.feed/my",
    "uri":"http://serverName/sites/dev/_api/social.feed/my",
    "type":"SP.Social.SocialRestActor"
   },
  "FollowableItem":"domain\\username1",
  "FollowableItemActor":null,
  "Me":{
    "__metadata":{"type":"SP.Social.SocialActor"},
    "AccountName":"domain\\username1",
    "ActorType":0,
    "CanFollow":false,
    "ContentUri":null,
    "EmailAddress":null,
    "FollowedContentUri":null,
    "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b",
    "ImageUri":null,
    "IsFollowed":false,
    "LibraryUri":null,
    "Name":"User1 Name",
    "PersonalSiteUri":"http://serverName/my/personal/username1/",
    "Status":0,
    "StatusText":"This is post 2",
    "TagGuid":"00000000-0000-0000-0000-000000000000",
    "Title":null,
    "Uri":"http://serverName:80/my/Person.aspx?accountname=domain%5Cusername1"
  }
}}
```


## <a name="myfeedpost"></a><span data-ttu-id="43a62-176">Мои/канал/Post</span><span class="sxs-lookup"><span data-stu-id="43a62-176">My/Feed/Post</span></span>
<span data-ttu-id="43a62-177"><a name="bk_myFeedPost"> </a></span><span class="sxs-lookup"><span data-stu-id="43a62-177"></span></span>

<span data-ttu-id="43a62-178">Создает корневой post в канал для текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="43a62-178">Creates a root post in the current user's feed.</span></span>
  
    
    
<span data-ttu-id="43a62-p106">Вы можете разместить только в контексте текущего пользователя. Не удается создать корневой post в веб-канал другого пользователя, но можно ответить на post другому пользователю. В разделе  [Поместить/ответ](social-feed-rest-api-reference-for-sharepoint.md#bk_postReply).</span><span class="sxs-lookup"><span data-stu-id="43a62-p106">You can post only in the context of the current user. You cannot create a root post in a different user's feed, but you can reply to another user's post. See  [Post/Reply](social-feed-rest-api-reference-for-sharepoint.md#bk_postReply).</span></span>
  
> [!NOTE]
> <span data-ttu-id="43a62-182">[!Примечание] Не следует путать этот ресурс  `Post` с ресурсом `Post` , представляющий конкретный поток или post.</span><span class="sxs-lookup"><span data-stu-id="43a62-182">Don't confuse this  `Post` resource with the `Post` resource that represents a specific thread or post.</span></span>
  
    
    


### <a name="endpoint-uri-structure"></a><span data-ttu-id="43a62-183">Структура URI конечной точки</span><span class="sxs-lookup"><span data-stu-id="43a62-183">Endpoint URI structure</span></span>

 <span data-ttu-id="43a62-184">**POST** `http://<siteCollection>/<site>/_api/social.feed/my/feed/post`</span><span class="sxs-lookup"><span data-stu-id="43a62-184">**POST** `http://<siteCollection>/<site>/_api/social.feed/my/feed/post`</span></span>
  
    
    

### <a name="request-parameter"></a><span data-ttu-id="43a62-185">Параметр запроса</span><span class="sxs-lookup"><span data-stu-id="43a62-185">Request parameter</span></span>

 <span data-ttu-id="43a62-186">_restCreationData_</span><span class="sxs-lookup"><span data-stu-id="43a62-186">_restCreationData_</span></span>
  
    
    
<span data-ttu-id="43a62-187">тип:  [SP. Social.SocialRestPostCreationData](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestPostCreationData)</span><span class="sxs-lookup"><span data-stu-id="43a62-187">Type:  [SP.Social.SocialRestPostCreationData](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestPostCreationData)</span></span>
  
    
    
<span data-ttu-id="43a62-188">**null** идентификатор и свойства нового post, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="43a62-188">A **null** ID and the properties of the new post, as shown in the following example.</span></span>
  
    
    

```

"restCreationData":{
  "__metadata":{
    "type":"SP.Social.SocialRestPostCreationData"
  },
  "ID":null,
  "creationData":{
    "__metadata":{
      "type":"SP.Social.SocialPostCreationData"
    },
    "ContentText":"This post was published using REST.", 
    "UpdateStatusText":false
  }
}
```


### <a name="response"></a><span data-ttu-id="43a62-189">Ответ</span><span class="sxs-lookup"><span data-stu-id="43a62-189">Response</span></span>

<span data-ttu-id="43a62-190">Тип:  [SP. Social.SocialRestThread](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestThread)</span><span class="sxs-lookup"><span data-stu-id="43a62-190">Type:  [SP.Social.SocialRestThread](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestThread)</span></span>
  
    
    
<span data-ttu-id="43a62-191">поток, который содержит новый корневой post.</span><span class="sxs-lookup"><span data-stu-id="43a62-191">A thread that contains the new root post.</span></span>
  
    
    
<span data-ttu-id="43a62-192">В следующем примере ответа представляет поток, который содержит новый корневой post.</span><span class="sxs-lookup"><span data-stu-id="43a62-192">The following response example represents the thread that contains the new root post.</span></span>
  
    
    



```

{"d":{
  "__metadata":{
    "id":"http://serverName/sites/dev/_api/social.feed/post(ID=@ai)/?@ai='1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.4316bdaa94bf4984be5dfea1ba96954e.26.26.S-1-5-21-2127521184-1604012920-1887927527-66602'",
    "uri":"http://serverName/sites/dev/_api/social.feed/post(ID=@ai)/?@ai='1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.4316bdaa94bf4984be5dfea1ba96954e.26.26.S-1-5-21-2127521184-1604012920-1887927527-66602'",
    "type":"SP.Social.SocialRestThread"
  },
  "ID":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.4316bdaa94bf4984be5dfea1ba96954e.26.26.S-1-5-21-2127521184-1604012920-1887927527-66602",
  "SocialThread":{
    "__metadata":{"type":"SP.Social.SocialThread"},
    "Actors":{
      "results":[{
        "__metadata":{"type":"SP.Social.SocialActor"},
        "AccountName":"domain\\username1",
        "ActorType":0, 
        "CanFollow":false, 
        "ContentUri":null, 
        "EmailAddress":null, 
        "FollowedContentUri":null, 
        "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b",
        "ImageUri":null, 
        "IsFollowed":false, 
        "LibraryUri":null, 
        "Name":"User1 Name",
        "PersonalSiteUri":"http://serverName:80/my/personal/username1/",
        "Status":0, 
        "StatusText":"",
        "TagGuid":"00000000-0000-0000-0000-000000000000",
        "Title":null, 
        "Uri":"http://serverName:80/my/Person.aspx?accountname=domain%5Cusername1"
      }]
    },
    "Attributes":6,
    "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.4316bdaa94bf4984be5dfea1ba96954e.26.26.S-1-5-21-2127521184-1604012920-1887927527-66602",
    "OwnerIndex":0,
    "Permalink":"http://serverName:80/my/ThreadView.aspx?ThreadID=1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.4316bdaa94bf4984be5dfea1ba96954e.26.26.S-1-5-21-2127521184-1604012920-1887927527-66602",
    "PostReference":null, 
    "Replies":{"results":[]},
    "RootPost":{
      "__metadata":{"type":"SP.Social.SocialPost"},
      "Attachment":null, 
      "Attributes":23, 
      "AuthorIndex":0, 
      "CreatedTime":"2013-04-17T19:31:57.204511Z",
      "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.4316bdaa94bf4984be5dfea1ba96954e.26.26.S-1-5-21-2127521184-1604012920-1887927527-66602",
      "LikerInfo":{
        "__metadata":{"type":"SP.Social.SocialPostActorInfo"},
        "IncludesCurrentUser":false, 
        "Indexes":{"results":[]},
        "TotalCount":0
      },
      "ModifiedTime":"2013-04-17T19:31:57.204511Z",
      "Overlays":{"results":[]},
      "PostType":0, 
      "PreferredImageUri":null, 
      "Source":{
        "__metadata":{"type":"SP.Social.SocialLink"},
        "Text":null, 
        "Uri":null
      },
      "Text":"Posted with REST." 
    },
    "Status":0,
    "ThreadType":0,
    "TotalReplyCount":0
  }
}}
```


## <a name="myfeed"></a><span data-ttu-id="43a62-193">Мой канал /</span><span class="sxs-lookup"><span data-stu-id="43a62-193">My/Feed</span></span>
<span data-ttu-id="43a62-194"><a name="bk_myFeed"> </a></span><span class="sxs-lookup"><span data-stu-id="43a62-194"></span></span>

<span data-ttu-id="43a62-195">Получает веб-канал активности текущим пользователем ( **Personal** канал типа).</span><span class="sxs-lookup"><span data-stu-id="43a62-195">Gets the feed of activity by the current user ( **Personal** feed type).</span></span>
  
    
    

### <a name="endpoint-uri-structure"></a><span data-ttu-id="43a62-196">Структура URI конечной точки</span><span class="sxs-lookup"><span data-stu-id="43a62-196">Endpoint URI structure</span></span>

 <span data-ttu-id="43a62-197">**GET** `http://<siteCollection>/<site>/_api/social.feed/my/feed`</span><span class="sxs-lookup"><span data-stu-id="43a62-197">**GET** `http://<siteCollection>/<site>/_api/social.feed/my/feed`</span></span>
  
    
    
 <span data-ttu-id="43a62-198">**GET** `http://<siteCollection>/<site>/_api/social.feed/my/feed(MaxThreadCount=10,SortOrder=1,NewerThan=@v)?@v=datetime'2013-01-01T08:00'`</span><span class="sxs-lookup"><span data-stu-id="43a62-198">**GET** `http://<siteCollection>/<site>/_api/social.feed/my/feed(MaxThreadCount=10,SortOrder=1,NewerThan=@v)?@v=datetime'2013-01-01T08:00'`</span></span>
  
    
    

### <a name="request-parameter"></a><span data-ttu-id="43a62-199">Параметр запроса</span><span class="sxs-lookup"><span data-stu-id="43a62-199">Request parameter</span></span>

 <span data-ttu-id="43a62-200">_feedOptions_ (необязательно)</span><span class="sxs-lookup"><span data-stu-id="43a62-200">_feedOptions_ (optional)</span></span>
  
    
    
<span data-ttu-id="43a62-201">Тип:  [SP. Social.SocialFeedOptions](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialFeedOptions)</span><span class="sxs-lookup"><span data-stu-id="43a62-201">Type:  [SP.Social.SocialFeedOptions](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialFeedOptions)</span></span>
  
    
    
<span data-ttu-id="43a62-p107">максимальное число потоков, диапазон даты и времени и порядок сортировки. Можно указать любое сочетание следующих свойств, например, можно указать только свойство **MaxThreadCount**.</span><span class="sxs-lookup"><span data-stu-id="43a62-p107">The maximum number of threads, date-time range, and sort order. You can optionally specify any combination of these properties, for example, you can specify only the **MaxThreadCount** property.</span></span>
  
    
    
<span data-ttu-id="43a62-p108">Псевдоним **@** можно использовать для передачи специальные символы. Например `<siteUri>/_api/social.feed/my/feed(OlderThan=@v)?@v=datetime'2013-01-01T08:00'` используется псевдоним **@v** для отправки **:** символов.</span><span class="sxs-lookup"><span data-stu-id="43a62-p108">You can use an **@** alias to pass special characters. For example, `<siteUri>/_api/social.feed/my/feed(OlderThan=@v)?@v=datetime'2013-01-01T08:00'` uses the **@v** alias to send a **:** character.</span></span>
  
    
    

### <a name="response"></a><span data-ttu-id="43a62-206">Ответ</span><span class="sxs-lookup"><span data-stu-id="43a62-206">Response</span></span>

<span data-ttu-id="43a62-207">Тип:  [SP. Social.SocialRestFeed](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestFeed)</span><span class="sxs-lookup"><span data-stu-id="43a62-207">Type:  [SP.Social.SocialRestFeed](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestFeed)</span></span>
  
    
    
<span data-ttu-id="43a62-208">личные веб-канал текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="43a62-208">The current user's personal feed.</span></span>
  
    
    
<span data-ttu-id="43a62-209">В следующем примере ответа представляет текущего пользователя личные веб-канал.</span><span class="sxs-lookup"><span data-stu-id="43a62-209">The following response example represents the current user's personal feed.</span></span>
  
    
    



```

{"d":{
  "__metadata":{
    "id":"http://serverName/sites/dev/_api/social.feed/my/feed",
    "uri":"http://serverName/sites/dev/_api/social.feed/my/feed",
    "type":"SP.Social.SocialRestFeed"
  },
  "SocialFeed":{
    "__metadata":{"type":"SP.Social.SocialFeed"},
    "Attributes":1, 
    "NewestProcessed":"2013-04-15T06:10:11Z",
    "OldestProcessed":"2013-04-15T05:33:12Z",
    "Threads":{
      "results":[{
        "__metadata":{"type":"SP.Social.SocialThread"},
        "Actors":{
          "results":[{
            "__metadata":{"type":"SP.Social.SocialActor"},
            "AccountName":"domain\\username1",
            "ActorType":0, 
            "CanFollow":false, 
            "ContentUri":null, 
            "EmailAddress":null, 
            "FollowedContentUri":null, 
            "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b",
            "ImageUri":null, 
            "IsFollowed":false, 
            "LibraryUri":null, 
            "Name":"User1 Name",
            "PersonalSiteUri":"http://serverName:80/my/personal/username1/",
            "Status":0, 
            "StatusText":"",
            "TagGuid":"00000000-0000-0000-0000-000000000000",
            "Title":null, 
            "Uri":"http://serverName:80/my/Person.aspx?accountname=domain%5Cusername1"
          },{
            "__metadata":{"type":"SP.Social.SocialActor"},
            "AccountName":"domain\\username2",
            "ActorType":0, 
            "CanFollow":true, 
            "ContentUri":null, 
            "EmailAddress":"username2@somecompany.com",
            "FollowedContentUri":null, 
            "Id":"1.ed418efb7f984ee49ce276c9c5441938.de1675d4929d431894c18908ac53516a.65da910de21f4e40abb318ba33520931.0c37852b34d0418e91c62ac25af4be5b",
            "ImageUri":"http://serverName:80/my/User Photos/Profile Pictures/username2_MThumb.jpg",
            "IsFollowed":true, 
            "LibraryUri":null, 
            "Name":"User2 Name",
            "PersonalSiteUri":"http://serverName/my/personal/username2",
            "Status":6, 
            "StatusText":"",
            "TagGuid":"00000000-0000-0000-0000-000000000000",
            "Title":"SOME TITLE",
            "Uri":"http://serverName:80/my/Person.aspx?accountname=domain%5Cusername2"
          }]
        },
        "Attributes":6, 
        "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.c554cbf1934b4c82bb1d43ebf961de92.17.17.S-1-5-21-2127521184-1604012920-1887927527-66602",
        "OwnerIndex":0, 
        "Permalink":"http://serverName:80/my/ThreadView.aspx?ThreadID=1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.c554cbf1934b4c82bb1d43ebf961de92.17.17.S-1-5-21-2127521184-1604012920-1887927527-66602",
        "PostReference":null, 
        "Replies":{
          "results":[{
            "__metadata":{"type":"SP.Social.SocialPost"},
            "Attachment":null, 
            "Attributes":23, 
            "AuthorIndex":1, 
            "CreatedTime":"2013-04-15T06:10:11.3480926Z",
          "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.59c0273c6c7b41e784b496c9aaa909a8.17.24.S-1-5-21-2127521184-1604012920-1887927527-66602",
            "LikerInfo":{
              "__metadata":{"type":"SP.Social.SocialPostActorInfo"},
              "IncludesCurrentUser":false,
              "Indexes":{"results":[]},
              "TotalCount":0
            },
            "ModifiedTime":"2013-04-15T06:10:11.3480926Z",
            "Overlays":{"results":[]},
            "PostType":1, 
            "PreferredImageUri":null, 
            "Source":{
              "__metadata":{"type":"SP.Social.SocialLink"},
              "Text":null, 
              "Uri":null
            },
            "Text":"This is a reply to post 1."
          }]
        },
        "RootPost":{
          "__metadata":{"type":"SP.Social.SocialPost"},
          "Attachment":null,
          "Attributes":23, 
          "AuthorIndex":0, 
          "CreatedTime":"2013-04-15T05:58:24Z",
          "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.c554cbf1934b4c82bb1d43ebf961de92.17.17.S-1-5-21-2127521184-1604012920-1887927527-66602",
          "LikerInfo":{
            "__metadata":{"type":"SP.Social.SocialPostActorInfo"},
            "IncludesCurrentUser":false,
            "Indexes":{"results":[]},
            "TotalCount":0
          },
          "ModifiedTime":"2013-04-15T06:10:11Z",
          "Overlays":{"results":[]},
          "PostType":0, 
          "PreferredImageUri":null, 
          "Source":{
            "__metadata":{"type":"SP.Social.SocialLink"},
            "Text":null, 
            "Uri":null
          },
          "Text":"This is post 1." 
        },
        "Status":0, 
        "ThreadType":0, 
        "TotalReplyCount":1
      },{
      "__metadata":{"type":"SP.Social.SocialThread"},
      "Actors":{
        "results":[{
          "__metadata":{"type":"SP.Social.SocialActor"},
          "AccountName":"domain\\username1",
          "ActorType":0, 
          "CanFollow":false, 
          "ContentUri":null, 
          "EmailAddress":null, 
          "FollowedContentUri":null, 
          "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b",
          "ImageUri":null, 
          "IsFollowed":false, 
          "LibraryUri":null, 
          "Name":"User1 Name",
          "PersonalSiteUri":"http://serverName:80/my/personal/username1/",
          "Status":0, 
          "StatusText":"",
          "TagGuid":"00000000-0000-0000-0000-000000000000",
          "Title":null, 
          "Uri":"http://serverName:80/my/Person.aspx?accountname=domain%5Cusername1"
        }]
      },
      "Attributes":6, 
      "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.82e71ca2381b4657935546e57f1992d5.23.23.S-1-5-21-2127521184-1604012920-1887927527-66602",
      "OwnerIndex":0, 
      "Permalink":"http://serverName:80/my/ThreadView.aspx?ThreadID=1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.82e71ca2381b4657935546e57f1992d5.23.23.S-1-5-21-2127521184-1604012920-1887927527-66602",
      "PostReference":null, 
      "Replies":{"results":[]},
      "RootPost":{
        "__metadata":{"type":"SP.Social.SocialPost"},
        "Attachment":null, 
        "Attributes":23, 
        "AuthorIndex":0, 
        "CreatedTime":"2013-04-15T06:07:05Z",
        "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.82e71ca2381b4657935546e57f1992d5.23.23.S-1-5-21-2127521184-1604012920-1887927527-66602",
        "LikerInfo":{
          "__metadata":{"type":"SP.Social.SocialPostActorInfo"},
          "IncludesCurrentUser":false, 
          "Indexes":{"results":[]},
          "TotalCount":0},
          "ModifiedTime":"2013-04-15T06:07:05Z",
          "Overlays":{"results":[]},
          "PostType":0, 
          "PreferredImageUri":null, 
          "Source":{
            "__metadata":{"type":"SP.Social.SocialLink"},
            "Text":null,"Uri":null},
            "Text":"This is post 2." 
          }, 
          "Status":0, 
          "ThreadType":0, 
          "TotalReplyCount":0
        },{
        "__metadata":{"type":"SP.Social.SocialThread"},
        "Actors":{
          "results":[{
            "__metadata":{"type":"SP.Social.SocialActor"},
            "AccountName":"domain\\username1",
            "ActorType":0, 
            "CanFollow":false, 
            "ContentUri":null, 
            "EmailAddress":null, 
            "FollowedContentUri":null, 
            "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b",
            "ImageUri":null, 
            "IsFollowed":false, 
            "LibraryUri":null, 
            "Name":"User1 Name",
            "PersonalSiteUri":"http://serverName:80/my/personal/username1/",
            "Status":0, 
            "StatusText":"",
            "TagGuid":"00000000-0000-0000-0000-000000000000",
            "Title":null, 
            "Uri":"http://serverName:80/my/Person.aspx?accountname=domain%5Cusername1"
          },{
            "__metadata":{"type":"SP.Social.SocialActor"},
            "AccountName":"domain\\username2",
            "ActorType":0, 
            "CanFollow":true, 
            "ContentUri":null, 
            "EmailAddress":"username2@somecompany.com",
            "FollowedContentUri":null, 
            "Id":"1.ed418efb7f984ee49ce276c9c5441938.de1675d4929d431894c18908ac53516a.65da910de21f4e40abb318ba33520931.0c37852b34d0418e91c62ac25af4be5b",
            "ImageUri":"http://serverName:80/my/User Photos/Profile Pictures/username2_MThumb.jpg",
            "IsFollowed":true, 
            "LibraryUri":null, 
            "Name":"User2 Name",
            "PersonalSiteUri":"http://serverName/my/personal/username2",
            "Status":6, 
            "StatusText":"",
            "TagGuid":"00000000-0000-0000-0000-000000000000",
            "Title":"SOME TITLE",
            "Uri":"http://serverName:80/my/Person.aspx?accountname=domain%5Cusername2"
          }]
      },
      "Attributes":0, 
      "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.cecc0de3d7d04520bb87a181b24c105a.16.16.S-1-5-21-2127521184-1604012920-1887927527-66602",
      "OwnerIndex":0, 
      "Permalink":"http://serverName:80/my/ThreadView.aspx?ThreadID=1.ed418efb7f984ee49ce276c9c5441938.de1675d4929d431894c18908ac53516a.65da910de21f4e40abb318ba33520931.0c37852b34d0418e91c62ac25af4be5b.ca83f758aab04065bc303398f2701eb9.10.10.S-1-5-21-124525095-708259637-1543119021-628175",
      "PostReference":{
        "__metadata":{"type":"SP.Social.SocialPostReference"},
        "Digest":null, 
        "Post":{
          "__metadata":{"type":"SP.Social.SocialPost"},
          "Attachment":null, 
          "Attributes":23, 
          "AuthorIndex":1, 
          "CreatedTime":"2013-04-15T05:05:13Z",
          "Id":"1.ed418efb7f984ee49ce276c9c5441938.de1675d4929d431894c18908ac53516a.65da910de21f4e40abb318ba33520931.0c37852b34d0418e91c62ac25af4be5b.ca83f758aab04065bc303398f2701eb9.10.10.S-1-5-21-124525095-708259637-1543119021-628175",
          "LikerInfo":{
            "__metadata":{"type":"SP.Social.SocialPostActorInfo"},
            "IncludesCurrentUser":true, 
            "Indexes":{"results":[]},
            "TotalCount":1
          },
          "ModifiedTime":"2013-04-15T05:05:13Z",
          "Overlays":{
            "results":[{
              "__metadata":{"type":"SP.Social.SocialDataOverlay"},
              "ActorIndexes":{"results":[0]}, 
              "Index":1, 
              "Length":18, 
              "LinkUri":null, 
              "OverlayType":1
            }]
          },
          "PostType":0, 
          "PreferredImageUri":null, 
          "Source":{
            "__metadata":{"type":"SP.Social.SocialLink"},
            "Text":null, 
            "Uri":null
          },
          "Text":"@User1 Name presented at the conference."}, 
          "ThreadId":"1.ed418efb7f984ee49ce276c9c5441938.de1675d4929d431894c18908ac53516a.65da910de21f4e40abb318ba33520931.0c37852b34d0418e91c62ac25af4be5b.ca83f758aab04065bc303398f2701eb9.10.10.S-1-5-21-124525095-708259637-1543119021-628175",
          "ThreadOwnerIndex":1
        },
        "Replies":{"results":[]},
        "RootPost":{
          "__metadata":{"type":"SP.Social.SocialPost"},
          "Attachment":null, 
          "Attributes":14, 
          "AuthorIndex":0, 
          "CreatedTime":"2013-04-15T05:33:12Z",
          "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.cecc0de3d7d04520bb87a181b24c105a.16.16.S-1-5-21-2127521184-1604012920-1887927527-66602",
          "LikerInfo":null, 
          "ModifiedTime":"2013-04-15T05:33:12Z",
          "Overlays":{
            "results":[{
              "__metadata":{"type":"SP.Social.SocialDataOverlay"},
              "ActorIndexes":{"results":[0]}, 
              "Index":0, 
              "Length":18, 
              "LinkUri":null, 
              "OverlayType":1
            },{
            "__metadata":{"type":"SP.Social.SocialDataOverlay"},
              "ActorIndexes":{"results":[1]}, 
              "Index":35, 
              "Length":10, 
              "LinkUri":null, 
              "OverlayType":1
            }]
          },
          "PostType":0, 
          "PreferredImageUri":"http://serverName:80/_layouts/15/Images/Like.11x11x32.png",
          "Source":{
            "__metadata":{"type":"SP.Social.SocialLink"},
            "Text":null,"Uri":null
          },
          "Text":"User1 Name liked a post by User2 Name."
        }, 
        "Status":0, 
        "ThreadType":1, 
        "TotalReplyCount":0
      }]
    },
    "UnreadMentionCount":1
  }
}}
```


## <a name="mynews"></a><span data-ttu-id="43a62-210">Мои / новостей</span><span class="sxs-lookup"><span data-stu-id="43a62-210">My/News</span></span>
<span data-ttu-id="43a62-211"><a name="bk_myNews"> </a></span><span class="sxs-lookup"><span data-stu-id="43a62-211"></span></span>

<span data-ttu-id="43a62-212">Получает веб-канал активности текущим пользователем и людей и содержимое, которое пользователь следующие, отсортированные по дату последнего изменения ( **News** канал типа).</span><span class="sxs-lookup"><span data-stu-id="43a62-212">Gets the feed of activity by the current user and by people and content the user is following, sorted by last modified date ( **News** feed type).</span></span>
  
    
    

### <a name="endpoint-uri-structure"></a><span data-ttu-id="43a62-213">Структура URI конечной точки</span><span class="sxs-lookup"><span data-stu-id="43a62-213">Endpoint URI structure</span></span>

 <span data-ttu-id="43a62-214">**GET** `http://<siteCollection>/<site>/_api/social.feed/my/news`</span><span class="sxs-lookup"><span data-stu-id="43a62-214">**GET** `http://<siteCollection>/<site>/_api/social.feed/my/news`</span></span>
  
    
    
 <span data-ttu-id="43a62-215">**GET** `http://<siteCollection>/<site>/_api/social.feed/my/news(MaxThreadCount=10,NewerThan=@v)?@v=datetime'2013-01-01T08:00'`</span><span class="sxs-lookup"><span data-stu-id="43a62-215">**GET** `http://<siteCollection>/<site>/_api/social.feed/my/news(MaxThreadCount=10,NewerThan=@v)?@v=datetime'2013-01-01T08:00'`</span></span>
  
    
    

### <a name="request-parameter"></a><span data-ttu-id="43a62-216">Параметр запроса</span><span class="sxs-lookup"><span data-stu-id="43a62-216">Request parameter</span></span>

 <span data-ttu-id="43a62-217">_feedOptions_ (необязательно)</span><span class="sxs-lookup"><span data-stu-id="43a62-217">_feedOptions_ (optional)</span></span>
  
    
    
<span data-ttu-id="43a62-218">Тип:  [SP. Social.SocialFeedOptions](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialFeedOptions)</span><span class="sxs-lookup"><span data-stu-id="43a62-218">Type:  [SP.Social.SocialFeedOptions](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialFeedOptions)</span></span>
  
    
    
<span data-ttu-id="43a62-p109">максимальное число потоков, диапазон даты и времени и порядок сортировки. Можно указать любое сочетание следующих свойств, например, можно указать только свойство **MaxThreadCount**.</span><span class="sxs-lookup"><span data-stu-id="43a62-p109">The maximum number of threads, date-time range, and sort order. You can optionally specify any combination of these properties, for example, you can specify only the **MaxThreadCount** property.</span></span>
  
    
    
<span data-ttu-id="43a62-p110">Псевдоним **@** можно использовать для передачи специальные символы. Например `<siteUri>/_api/social.feed/my/News(OlderThan=@v)?@v=datetime'2013-01-01T08:00'` используется псевдоним **@v** для отправки **:** символов.</span><span class="sxs-lookup"><span data-stu-id="43a62-p110">You can use an **@** alias to pass special characters. For example, `<siteUri>/_api/social.feed/my/News(OlderThan=@v)?@v=datetime'2013-01-01T08:00'` uses the **@v** alias to send a **:** character.</span></span>
  
    
    

### <a name="response"></a><span data-ttu-id="43a62-223">Ответ</span><span class="sxs-lookup"><span data-stu-id="43a62-223">Response</span></span>

<span data-ttu-id="43a62-224">Тип:  [SP. Social.SocialRestFeed](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestFeed)</span><span class="sxs-lookup"><span data-stu-id="43a62-224">Type:  [SP.Social.SocialRestFeed](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestFeed)</span></span>
  
    
    
<span data-ttu-id="43a62-225">канала новостей текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="43a62-225">The current user's newsfeed.</span></span>
  
    
    
<span data-ttu-id="43a62-226">В следующем примере ответа представляет текущего пользователя на канал новостей.</span><span class="sxs-lookup"><span data-stu-id="43a62-226">The following response example represents the current user's newsfeed.</span></span>
  
    
    



```

{"d":{
  "__metadata":{
    "id":"http://serverName/sites/dev/_api/social.feed/my/news",
    "uri":"http://serverName/sites/dev/_api/social.feed/my/news",
    "type":"SP.Social.SocialRestFeed"
  },
  "SocialFeed":{
    "__metadata":{"type":"SP.Social.SocialFeed"},
    "Attributes":1, 
    "NewestProcessed":"2013-04-15T06:10:11.4730902Z",
    "OldestProcessed":"2013-04-12T20:51:51Z",
    "Threads":{
      "results":[{
        "__metadata":{"type":"SP.Social.SocialThread"},
        "Actors":{
          "results":[{
            "__metadata":{"type":"SP.Social.SocialActor"},
            "AccountName":"domain\\username1",
            "ActorType":0, 
            "CanFollow":false, 
            "ContentUri":null, 
            "EmailAddress":null, 
            "FollowedContentUri":"http://serverName:80/my/_layouts/15/MySite.aspx?MySiteRedirect=FollowedDocuments",
            "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b",
            "ImageUri":null, 
            "IsFollowed":false, 
            "LibraryUri":null, 
            "Name":"User1 Name",
            "PersonalSiteUri":"http://serverName:80/my/personal/username1/",
            "Status":0, 
            "StatusText":"",
            "TagGuid":"00000000-0000-0000-0000-000000000000",
            "Title":null, 
            "Uri":"http://serverName:80/my/Person.aspx?accountname=domain%5Cusername1"
          },{
            "__metadata":{"type":"SP.Social.SocialActor"},
            "AccountName":"domain\\username2",
            "ActorType":0, 
            "CanFollow":true, 
            "ContentUri":null, 
            "EmailAddress":"username2@somecompany.com",
            "FollowedContentUri":null, 
            "Id":"1.ed418efb7f984ee49ce276c9c5441938.de1675d4929d431894c18908ac53516a.65da910de21f4e40abb318ba33520931.0c37852b34d0418e91c62ac25af4be5b",
            "ImageUri":"http://serverName:80/my/User Photos/Profile Pictures/username2_MThumb.jpg",
            "IsFollowed":true, 
            "LibraryUri":null, 
            "Name":"User2 Name",
            "PersonalSiteUri":"http://serverName/my/personal/username2",
            "Status":0, 
            "StatusText":"",
            "TagGuid":"00000000-0000-0000-0000-000000000000",
            "Title":"SOME TITLE",
            "Uri":"http://serverName:80/my/Person.aspx?accountname=domain%5Cusername2"
          }]
        },
        "Attributes":6, 
        "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.c554cbf1934b4c82bb1d43ebf961de92.17.17.S-1-5-21-2127521184-1604012920-1887927527-66602",
        "OwnerIndex":0, 
        "Permalink":"http://serverName:80/my/ThreadView.aspx?ThreadID=1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.c554cbf1934b4c82bb1d43ebf961de92.17.17.S-1-5-21-2127521184-1604012920-1887927527-66602",
        "PostReference":null, 
        "Replies":{
          "results":[{
            "__metadata":{"type":"SP.Social.SocialPost"},
            "Attachment":null, 
            "Attributes":23, 
            "AuthorIndex":1, 
            "CreatedTime":"2013-04-15T06:10:11.3480926Z",
            "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.59c0273c6c7b41e784b496c9aaa909a8.17.24.S-1-5-21-2127521184-1604012920-1887927527-66602",
            "LikerInfo":{
              "__metadata":{"type":"SP.Social.SocialPostActorInfo"},
              "IncludesCurrentUser":false, 
              "Indexes":{"results":[]},
              "TotalCount":0
            },
            "ModifiedTime":"2013-04-15T06:10:11.3480926Z",
            "Overlays":{"results":[]},
            "PostType":1, 
            "PreferredImageUri":null, 
            "Source":{
              "__metadata":{"type":"SP.Social.SocialLink"},
              "Text":null, 
              "Uri":null
            },
            "Text":"This is a reply to post 1." 
          }]
        },
        "RootPost":{
          "__metadata":{"type":"SP.Social.SocialPost"},
          "Attachment":null, 
          "Attributes":23, 
          "AuthorIndex":0, 
          "CreatedTime":"2013-04-15T05:58:24Z",
          "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.c554cbf1934b4c82bb1d43ebf961de92.17.17.S-1-5-21-2127521184-1604012920-1887927527-66602",
          "LikerInfo":{
            "__metadata":{"type":"SP.Social.SocialPostActorInfo"},
            "IncludesCurrentUser":false, 
            "Indexes":{"results":[]},
            "TotalCount":0},
            "ModifiedTime":"2013-04-15T06:10:11.4730902Z",
            "Overlays":{"results":[]},
            "PostType":0, 
            "PreferredImageUri":null, 
            "Source":{
              "__metadata":{"type":"SP.Social.SocialLink"},
              "Text":null, 
              "Uri":null
            },
            "Text":"This is post 1." 
          },
          "Status":0, 
          "ThreadType":0, 
          "TotalReplyCount":1
        },{
        "__metadata":{"type":"SP.Social.SocialThread"},
        "Actors":{
          "results":[{
            "__metadata":{"type":"SP.Social.SocialActor"},
            "AccountName":"domain\\username1",
            "ActorType":0, 
            "CanFollow":false, 
            "ContentUri":null, 
            "EmailAddress":null, 
            "FollowedContentUri":"http://serverName:80/my/_layouts/15/MySite.aspx?MySiteRedirect=FollowedDocuments",
            "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b",
            "ImageUri":null, 
            "IsFollowed":false, 
            "LibraryUri":null, 
            "Name":"User1 Name",
            "PersonalSiteUri":"http://serverName:80/my/personal/username1/",
            "Status":0, 
            "StatusText":"",
            "TagGuid":"00000000-0000-0000-0000-000000000000",
            "Title":null, 
            "Uri":"http://serverName:80/my/Person.aspx?accountname=domain%5Cusername1"
          }]
        },
        "Attributes":6, 
        "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.82e71ca2381b4657935546e57f1992d5.23.23.S-1-5-21-2127521184-1604012920-1887927527-66602",
        "OwnerIndex":0, 
        "Permalink":"http://serverName:80/my/ThreadView.aspx?ThreadID=1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.82e71ca2381b4657935546e57f1992d5.23.23.S-1-5-21-2127521184-1604012920-1887927527-66602",
        "PostReference":null, 
        "Replies":{"results":[]},
        "RootPost":{
          "__metadata":{"type":"SP.Social.SocialPost"},
          "Attachment":null, 
          "Attributes":23, 
          "AuthorIndex":0, 
          "CreatedTime":"2013-04-15T06:07:05.4804434Z","Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.82e71ca2381b4657935546e57f1992d5.23.23.S-1-5-21-2127521184-1604012920-1887927527-66602",
          "LikerInfo":{
            "__metadata":{"type":"SP.Social.SocialPostActorInfo"},
            "IncludesCurrentUser":false, 
            "Indexes":{"results":[]},
            "TotalCount":0
          },
          "ModifiedTime":"2013-04-15T06:07:05.4804434Z",
          "Overlays":{"results":[]},
          "PostType":0, 
          "PreferredImageUri":null, 
          "Source":{
            "__metadata":{"type":"SP.Social.SocialLink"},
            "Text":null, 
            "Uri":null
          },
          "Text":"This is post 2." 
        },
        "Status":0, 
        "ThreadType":0, 
        "TotalReplyCount":0
      }]
    },
    "UnreadMentionCount":1
  }
}}
```


## <a name="mytimelinefeed"></a><span data-ttu-id="43a62-227">Мои/TimelineFeed</span><span class="sxs-lookup"><span data-stu-id="43a62-227">My/TimelineFeed</span></span>
<span data-ttu-id="43a62-228"><a name="bk_myTimelineFeed"> </a></span><span class="sxs-lookup"><span data-stu-id="43a62-228"></span></span>

<span data-ttu-id="43a62-229">Получает веб-канал активности текущим пользователем и людей и содержимое, которое пользователь следующие, отсортированные по дате создания ( **Timeline** канал типа).</span><span class="sxs-lookup"><span data-stu-id="43a62-229">Gets the feed of activity by the current user and by people and content the user is following, sorted by created date ( **Timeline** feed type).</span></span>
  
    
    

### <a name="endpoint-uri-structure"></a><span data-ttu-id="43a62-230">Структура URI конечной точки</span><span class="sxs-lookup"><span data-stu-id="43a62-230">Endpoint URI structure</span></span>

 <span data-ttu-id="43a62-231">**GET** `http://<siteCollection>/<site>/_api/social.feed/my/timelinefeed`</span><span class="sxs-lookup"><span data-stu-id="43a62-231">**GET** `http://<siteCollection>/<site>/_api/social.feed/my/timelinefeed`</span></span>
  
    
    
 <span data-ttu-id="43a62-232">**GET** `http://<siteCollection>/<site>/_api/social.feed/my/timelinefeed(MaxThreadCount=10,NewerThan=@v)?@v=datetime'2013-01-01T08:00'`</span><span class="sxs-lookup"><span data-stu-id="43a62-232">**GET** `http://<siteCollection>/<site>/_api/social.feed/my/timelinefeed(MaxThreadCount=10,NewerThan=@v)?@v=datetime'2013-01-01T08:00'`</span></span>
  
    
    

### <a name="request-parameter"></a><span data-ttu-id="43a62-233">Параметр запроса</span><span class="sxs-lookup"><span data-stu-id="43a62-233">Request parameter</span></span>

 <span data-ttu-id="43a62-234">_feedOptions_ (необязательно)</span><span class="sxs-lookup"><span data-stu-id="43a62-234">_feedOptions_ (optional)</span></span>
  
    
    
<span data-ttu-id="43a62-235">Тип:  [SP. Social.SocialFeedOptions](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialFeedOptions)</span><span class="sxs-lookup"><span data-stu-id="43a62-235">Type:  [SP.Social.SocialFeedOptions](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialFeedOptions)</span></span>
  
    
    
<span data-ttu-id="43a62-p111">максимальное число потоков, диапазон даты и времени и порядок сортировки. Можно указать любое сочетание следующих свойств, например, можно указать только свойство **MaxThreadCount**.</span><span class="sxs-lookup"><span data-stu-id="43a62-p111">The maximum number of threads, date-time range, and sort order. You can optionally specify any combination of these properties, for example, you can specify only the **MaxThreadCount** property.</span></span>
  
    
    
<span data-ttu-id="43a62-p112">Псевдоним **@** можно использовать для передачи специальные символы. Например `<siteUri>/_api/social.feed/my/timelinefeed(OlderThan=@v)?@v=datetime'2013-01-01T08:00'` используется псевдоним **@v** для отправки **:** символов.</span><span class="sxs-lookup"><span data-stu-id="43a62-p112">You can use an **@** alias to pass special characters. For example, `<siteUri>/_api/social.feed/my/timelinefeed(OlderThan=@v)?@v=datetime'2013-01-01T08:00'` uses the **@v** alias to send a **:** character.</span></span>
  
    
    

### <a name="response"></a><span data-ttu-id="43a62-240">Ответ</span><span class="sxs-lookup"><span data-stu-id="43a62-240">Response</span></span>

<span data-ttu-id="43a62-241">Тип:  [SP. Social.SocialRestFeed](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestFeed)</span><span class="sxs-lookup"><span data-stu-id="43a62-241">Type:  [SP.Social.SocialRestFeed](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestFeed)</span></span>
  
    
    
<span data-ttu-id="43a62-242">временной шкалы текущего пользователя веб-канала.</span><span class="sxs-lookup"><span data-stu-id="43a62-242">The current user's timeline feed.</span></span>
  
    
    
<span data-ttu-id="43a62-243">В следующем примере ответа представляет временной шкалы текущего пользователя веб-канала, который отсортированы по дате создания.</span><span class="sxs-lookup"><span data-stu-id="43a62-243">The following response example represents the current user's timeline feed, which is sorted by created date.</span></span>
  
    
    



```

{"d":{
  "__metadata":{
    "id":"http://serverName/sites/dev/_api/social.feed/my/timelinefeed",
    "uri":"http://serverName/sites/dev/_api/social.feed/my/timelinefeed",
    "type":"SP.Social.SocialRestFeed"
  },
  "SocialFeed":{
    "__metadata":{"type":"SP.Social.SocialFeed"},
    "Attributes":1, 
    "NewestProcessed":"2013-04-15T06:07:05.4804434Z",
    "OldestProcessed":"2013-04-12T20:51:51Z",
    "Threads":{
      "results":[{
        "__metadata":{"type":"SP.Social.SocialThread"},
        "Actors":{
          "results":[{
            "__metadata":{"type":"SP.Social.SocialActor"},
            "AccountName":"domain\\username1",
            "ActorType":0, 
            "CanFollow":false, 
            "ContentUri":null, 
            "EmailAddress":null, 
            "FollowedContentUri":"http://serverName:80/my/_layouts/15/MySite.aspx?MySiteRedirect=FollowedDocuments",
            "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b",
            "ImageUri":null, 
            "IsFollowed":false, 
            "LibraryUri":null, 
            "Name":"User1 Name",
            "PersonalSiteUri":"http://serverName:80/my/personal/username1/",
            "Status":0, 
            "StatusText":"This is post 2.", 
            "TagGuid":"00000000-0000-0000-0000-000000000000",
            "Title":null, 
            "Uri":"http://serverName:80/my/Person.aspx?accountname=domain%5Cusername1"
          }]
        },
        "Attributes":6, 
        "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.82e71ca2381b4657935546e57f1992d5.23.23.S-1-5-21-2127521184-1604012920-1887927527-66602",
        "OwnerIndex":0, 
        "Permalink":"http://serverName:80/my/ThreadView.aspx?ThreadID=1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.82e71ca2381b4657935546e57f1992d5.23.23.S-1-5-21-2127521184-1604012920-1887927527-66602",
        "PostReference":null, 
        "Replies":{"results":[]},
        "RootPost":{
          "__metadata":{"type":"SP.Social.SocialPost"},
          "Attachment":null, 
          "Attributes":23, 
          "AuthorIndex":0, 
          "CreatedTime":"2013-04-15T06:07:05.4804434Z",
          "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.82e71ca2381b4657935546e57f1992d5.23.23.S-1-5-21-2127521184-1604012920-1887927527-66602",
          "LikerInfo":{
            "__metadata":{"type":"SP.Social.SocialPostActorInfo"},
            "IncludesCurrentUser":false, 
            "Indexes":{"results":[]},
            "TotalCount":0
          },
          "ModifiedTime":"2013-04-15T06:07:05.4804434Z",
          "Overlays":{"results":[]},
          "PostType":0, 
          "PreferredImageUri":null, 
          "Source":{
            "__metadata":{"type":"SP.Social.SocialLink"},
            "Text":null, 
            "Uri":null
          },
          "Text":"This is post 2." 
        },
        "Status":0, 
        "ThreadType":0, 
        "TotalReplyCount":0
      },{
        "__metadata":{"type":"SP.Social.SocialThread"},
        "Actors":{
          "results":[{
            "__metadata":{"type":"SP.Social.SocialActor"},
            "AccountName":"domain\\username1",
            "ActorType":0, 
            "CanFollow":false, 
            "ContentUri":null, 
            "EmailAddress":null, 
            "FollowedContentUri":"http://serverName:80/my/_layouts/15/MySite.aspx?MySiteRedirect=FollowedDocuments",
            "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b",
            "ImageUri":null, 
            "IsFollowed":false, 
            "LibraryUri":null, 
            "Name":"User1 Name",
            "PersonalSiteUri":"http://serverName:80/my/personal/username1/",
            "Status":0, 
            "StatusText":"This is post 2.", 
            "TagGuid":"00000000-0000-0000-0000-000000000000",
            "Title":null, 
            "Uri":"http://serverName:80/my/Person.aspx?accountname=domain%5Cusername1"
          }]
        },
        "Attributes":6, 
        "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.c554cbf1934b4c82bb1d43ebf961de92.17.17.S-1-5-21-2127521184-1604012920-1887927527-66602",
        "OwnerIndex":0, 
        "Permalink":"http://serverName:80/my/ThreadView.aspx?ThreadID=1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.c554cbf1934b4c82bb1d43ebf961de92.17.17.S-1-5-21-2127521184-1604012920-1887927527-66602",
        "PostReference":null, 
        "Replies":{"results":[]},
        "RootPost":{
          "__metadata":{"type":"SP.Social.SocialPost"},
          "Attachment":null, 
          "Attributes":23, 
          "AuthorIndex":0, 
          "CreatedTime":"2013-04-15T05:58:24Z",
          "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.c554cbf1934b4c82bb1d43ebf961de92.17.17.S-1-5-21-2127521184-1604012920-1887927527-66602",
          "LikerInfo":{
            "__metadata":{"type":"SP.Social.SocialPostActorInfo"},
            "IncludesCurrentUser":false, 
            "Indexes":{"results":[]},
            "TotalCount":0
          },
          "ModifiedTime":"2013-04-15T06:04:49Z",
          "Overlays":{"results":[]},
          "PostType":0, 
          "PreferredImageUri":null, 
          "Source":{
            "__metadata":{"type":"SP.Social.SocialLink"},
            "Text":null, 
            "Uri":null
          },
          "Text":"This is post 1." 
        },
        "Status":0, 
        "ThreadType":0, 
        "TotalReplyCount":0
      }]
    },
    "UnreadMentionCount":1
  }
}}
```


## <a name="mylikes"></a><span data-ttu-id="43a62-244">Мои аудио- и оценки</span><span class="sxs-lookup"><span data-stu-id="43a62-244">My/Likes</span></span>
<span data-ttu-id="43a62-245"><a name="bk_myLikes"> </a></span><span class="sxs-lookup"><span data-stu-id="43a62-245"></span></span>

<span data-ttu-id="43a62-246">Получает веб-канал микроблога записи в блогах, текущего пользователя мне нравится, представленное типы потоков **LikeReference** .</span><span class="sxs-lookup"><span data-stu-id="43a62-246">Gets the feed of microblog posts that the current user likes, represented by **LikeReference** thread types.</span></span> <span data-ttu-id="43a62-247">В разделе [Справочник по потоки и потоки дайджест в веб-каналов социальных SharePoint](reference-threads-and-digest-threads-in-sharepoint-server-social-feeds.md).</span><span class="sxs-lookup"><span data-stu-id="43a62-247">See [Reference threads and digest threads in SharePoint social feeds](reference-threads-and-digest-threads-in-sharepoint-server-social-feeds.md).</span></span>
  
    
    

### <a name="endpoint-uri-structure"></a><span data-ttu-id="43a62-248">Структура URI конечной точки</span><span class="sxs-lookup"><span data-stu-id="43a62-248">Endpoint URI structure</span></span>

 <span data-ttu-id="43a62-249">**GET** `http://<siteCollection>/<site>/_api/social.feed/my/likes`</span><span class="sxs-lookup"><span data-stu-id="43a62-249">**GET** `http://<siteCollection>/<site>/_api/social.feed/my/likes`</span></span>
  
    
    
 <span data-ttu-id="43a62-250">**GET** `http://<siteCollection>/<site>/_api/social.feed/my/likes(MaxThreadCount=10,SortOrder=1,NewerThan=@v)?@v=datetime'2013-01-01T08:00'`</span><span class="sxs-lookup"><span data-stu-id="43a62-250">**GET** `http://<siteCollection>/<site>/_api/social.feed/my/likes(MaxThreadCount=10,SortOrder=1,NewerThan=@v)?@v=datetime'2013-01-01T08:00'`</span></span>
  
    
    

### <a name="request-parameter"></a><span data-ttu-id="43a62-251">Параметр запроса</span><span class="sxs-lookup"><span data-stu-id="43a62-251">Request parameter</span></span>

 <span data-ttu-id="43a62-252">_feedOptions_ (необязательно)</span><span class="sxs-lookup"><span data-stu-id="43a62-252">_feedOptions_ (optional)</span></span>
  
    
    
<span data-ttu-id="43a62-253">Тип:  [SP. Social.SocialFeedOptions](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialFeedOptions)</span><span class="sxs-lookup"><span data-stu-id="43a62-253">Type:  [SP.Social.SocialFeedOptions](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialFeedOptions)</span></span>
  
    
    
<span data-ttu-id="43a62-p114">максимальное число потоков, диапазон даты и времени и порядок сортировки. Можно указать любое сочетание следующих свойств, например, можно указать только свойство **MaxThreadCount**.</span><span class="sxs-lookup"><span data-stu-id="43a62-p114">The maximum number of threads, date-time range, and sort order. You can optionally specify any combination of these properties, for example, you can specify only the **MaxThreadCount** property.</span></span>
  
    
    
<span data-ttu-id="43a62-p115">При необходимости можно указать параметры получения в строке запроса. Псевдоним **@** можно использовать для передачи специальные символы. Например `<siteUri>/_api/social.feed/my/likes(OlderThan=@v)?@v=datetime'2013-01-01T08:00'` используется псевдоним **@v** для отправки **:** символов.</span><span class="sxs-lookup"><span data-stu-id="43a62-p115">You can optionally specify retrieval options in the query string. You can use an **@** alias to pass special characters. For example, `<siteUri>/_api/social.feed/my/likes(OlderThan=@v)?@v=datetime'2013-01-01T08:00'` uses the **@v** alias to send a **:** character.</span></span>
  
    
    

### <a name="response"></a><span data-ttu-id="43a62-259">Ответ</span><span class="sxs-lookup"><span data-stu-id="43a62-259">Response</span></span>

<span data-ttu-id="43a62-260">Тип:  [SP. Social.SocialRestFeed](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestFeed)</span><span class="sxs-lookup"><span data-stu-id="43a62-260">Type:  [SP.Social.SocialRestFeed](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestFeed)</span></span>
  
    
    
<span data-ttu-id="43a62-261">канала, который содержит сообщения, которые нравится текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="43a62-261">A feed that contains posts that the current user likes.</span></span>
  
    
    
<span data-ttu-id="43a62-p116">В следующем примере ответа представляет ссылку на публикацию, нравится текущего пользователя. Поток  это тип потока **LikeReference** (значение = **1**), для свойства **PostReference** ссылается на фактический post.</span><span class="sxs-lookup"><span data-stu-id="43a62-p116">The following response example represents a reference to a post that the current user likes. The thread is a **LikeReference** thread type (value = **1**) whose **PostReference** property references the actual post.</span></span>
  
    
    



```

{"d":{
  "__metadata":{
    "id":"http://serverName/sites/dev/_api/social.feed/my/likes",
    "uri":"http://serverName/sites/dev/_api/social.feed/my/likes",
    "type":"SP.Social.SocialRestFeed"
  },
  "SocialFeed":{
    "__metadata":{"type":"SP.Social.SocialFeed"}.
    "Attributes":1,
    "NewestProcessed":"2013-04-15T05:33:12Z",
    "OldestProcessed":"2013-04-15T05:33:12Z",
    "Threads":{
      "results":[{
        "__metadata":{"type":"SP.Social.SocialThread"},
        "Actors":{
          "results":[{
            "__metadata":{"type":"SP.Social.SocialActor"},
            "AccountName":"domain\\username1",
            "ActorType":0,
            "CanFollow":false,
            "ContentUri":null,
            "EmailAddress":null,
            "FollowedContentUri":null,
            "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b",
            "ImageUri":null
            "IsFollowed":false, 
            "LibraryUri":null, 
            "Name":"User1 Name",
            "PersonalSiteUri":"http://serverName:80/my/personal/username1/",
            "Status":0, 
            "StatusText":"This is post 2",
            "TagGuid":"00000000-0000-0000-0000-000000000000",
            "Title":null,
            "Uri":"http://serverName:80/my/Person.aspx?accountname=domain%5Cusername1"
          },{
            "__metadata":{"type":"SP.Social.SocialActor"},
            "AccountName":"domain\\username2",
            "ActorType":0, 
            "CanFollow":true, 
            "ContentUri":null, 
            "EmailAddress":"username2@somecompany.com",
            "FollowedContentUri":null, 
            "Id":"1.ed418efb7f984ee49ce276c9c5441938.de1675d4929d431894c18908ac53516a.65da910de21f4e40abb318ba33520931.0c37852b34d0418e91c62ac25af4be5b",
            "ImageUri":"http://serverName:80/my/User Photos/Profile Pictures/username2_MThumb.jpg",
            "IsFollowed":true, 
            "LibraryUri":null, 
            "Name":"User2 Name",
            "PersonalSiteUri":"http://serverName/my/personal/username2",
            "Status":6, 
            "StatusText":"@User1 Name presented at the conference.",
            "TagGuid":"00000000-0000-0000-0000-000000000000",
            "Title":"SOME TITLE",
            "Uri":"http://serverName:80/my/Person.aspx?accountname=domain%5Cusername2"}]
          },
          "Attributes":0, 
          "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.cecc0de3d7d04520bb87a181b24c105a.16.16.S-1-5-21-2127521184-1604012920-1887927527-66602",
          "OwnerIndex":0, 
          "Permalink":"http://serverName:80/my/ThreadView.aspx?ThreadID=1.ed418efb7f984ee49ce276c9c5441938.de1675d4929d431894c18908ac53516a.65da910de21f4e40abb318ba33520931.0c37852b34d0418e91c62ac25af4be5b.ca83f758aab04065bc303398f2701eb9.10.10.S-1-5-21-124525095-708259637-1543119021-628175",
          "PostReference":{
            "__metadata":{"type":"SP.Social.SocialPostReference"},
            "Digest":null, 
            "Post":{
              "__metadata":{"type":"SP.Social.SocialPost"},
              "Attachment":null, 
              "Attributes":23, 
              "AuthorIndex":1, 
              "CreatedTime":"2013-04-15T05:05:13Z",
              "Id":"1.ed418efb7f984ee49ce276c9c5441938.de1675d4929d431894c18908ac53516a.65da910de21f4e40abb318ba33520931.0c37852b34d0418e91c62ac25af4be5b.ca83f758aab04065bc303398f2701eb9.10.10.S-1-5-21-124525095-708259637-1543119021-628175",
              "LikerInfo":{
                "__metadata":{"type":"SP.Social.SocialPostActorInfo"},
                "IncludesCurrentUser":true, 
                "Indexes":{"results":[]},
                "TotalCount":1
              },
              "ModifiedTime":"2013-04-15T05:05:13Z",
              "Overlays":{
                "results":[{
                  "__metadata":{"type":"SP.Social.SocialDataOverlay"},
                  "ActorIndexes":{"results":[0]}, 
                  "Index":1, 
                  "Length":18, 
                  "LinkUri":null, 
                  "OverlayType":1
                }]
              },
              "PostType":0, 
              "PreferredImageUri":null, 
              "Source":{
                "__metadata":{"type":"SP.Social.SocialLink"},
                "Text":null, 
                "Uri":null
              },
              "Text":"@User1 Name presented at the conference." 
            },
            "ThreadId":"1.ed418efb7f984ee49ce276c9c5441938.de1675d4929d431894c18908ac53516a.65da910de21f4e40abb318ba33520931.0c37852b34d0418e91c62ac25af4be5b.ca83f758aab04065bc303398f2701eb9.10.10.S-1-5-21-124525095-708259637-1543119021-628175",
            "ThreadOwnerIndex":1
          },
          "Replies":{"results":[]},
          "RootPost":{
            "__metadata":{"type":"SP.Social.SocialPost"},
            "Attachment":null, 
            "Attributes":14, 
            "AuthorIndex":0, 
            "CreatedTime":"2013-04-15T05:33:12Z",
            "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.cecc0de3d7d04520bb87a181b24c105a.16.16.S-1-5-21-2127521184-1604012920-1887927527-66602",
            "LikerInfo":null, 
            "ModifiedTime":"2013-04-15T05:33:12Z",
            "Overlays":{
              "results":[{
                "__metadata":{"type":"SP.Social.SocialDataOverlay"},
                "ActorIndexes":{"results":[0]}, 
                "Index":0, 
                "Length":18, 
                "LinkUri":null, 
                "OverlayType":1
              },{
                "__metadata":{"type":"SP.Social.SocialDataOverlay"},
                "ActorIndexes":{"results":[1]}, 
                "Index":35, 
                "Length":10, 
                "LinkUri":null, 
                "OverlayType":1
              }]
            },
            "PostType":0, 
            "PreferredImageUri":"http://serverName:80/_layouts/15/Images/Like.11x11x32.png",
            "Source":{
              "__metadata":{"type":"SP.Social.SocialLink"},
              "Text":null, 
              "Uri":null
            },
            "Text":"User1 Name liked a post by User2 Name." 
          },
          "Status":0, 
          "ThreadType":1, 
          "TotalReplyCount":0
        }]
      },
    "UnreadMentionCount":1
  }
}}
```


## <a name="mymentionfeed"></a><span data-ttu-id="43a62-264">Мои/MentionFeed</span><span class="sxs-lookup"><span data-stu-id="43a62-264">My/MentionFeed</span></span>
<span data-ttu-id="43a62-265"><a name="bk_myMentionFeed"> </a></span><span class="sxs-lookup"><span data-stu-id="43a62-265"></span></span>

<span data-ttu-id="43a62-266">Получает веб-канал микроблога сообщения, содержащие упоминание текущего пользователя, представленного типы потоков **MentionReference** .</span><span class="sxs-lookup"><span data-stu-id="43a62-266">Gets the feed of microblog posts that mention the current user, represented by **MentionReference** thread types.</span></span> <span data-ttu-id="43a62-267">В разделе [Справочник по потоки и потоки дайджест в веб-каналов социальных SharePoint](reference-threads-and-digest-threads-in-sharepoint-server-social-feeds.md).</span><span class="sxs-lookup"><span data-stu-id="43a62-267">See [Reference threads and digest threads in SharePoint social feeds](reference-threads-and-digest-threads-in-sharepoint-server-social-feeds.md).</span></span>
  
    
    

### <a name="endpoint-uri-structure"></a><span data-ttu-id="43a62-268">Структура URI конечной точки</span><span class="sxs-lookup"><span data-stu-id="43a62-268">Endpoint URI structure</span></span>

 <span data-ttu-id="43a62-269">**GET** `http://<siteCollection>/<site>/_api/social.feed/my/mentionfeed`</span><span class="sxs-lookup"><span data-stu-id="43a62-269">**GET** `http://<siteCollection>/<site>/_api/social.feed/my/mentionfeed`</span></span>
  
    
    
 <span data-ttu-id="43a62-270">**GET** `http://<siteCollection>/<site>/_api/social.feed/my/mentionfeed(MaxThreadCount=10,SortOrder=1,NewerThan=@v)?@v=datetime'2013-01-01T08:00'`</span><span class="sxs-lookup"><span data-stu-id="43a62-270">**GET** `http://<siteCollection>/<site>/_api/social.feed/my/mentionfeed(MaxThreadCount=10,SortOrder=1,NewerThan=@v)?@v=datetime'2013-01-01T08:00'`</span></span>
  
    
    

### <a name="request-parameter"></a><span data-ttu-id="43a62-271">Параметр запроса</span><span class="sxs-lookup"><span data-stu-id="43a62-271">Request parameter</span></span>

 <span data-ttu-id="43a62-272">_feedOptions_ (необязательно)</span><span class="sxs-lookup"><span data-stu-id="43a62-272">_feedOptions_ (optional)</span></span>
  
    
    
<span data-ttu-id="43a62-273">Тип:  [SP. Social.SocialFeedOptions](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialFeedOptions)</span><span class="sxs-lookup"><span data-stu-id="43a62-273">Type:  [SP.Social.SocialFeedOptions](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialFeedOptions)</span></span>
  
    
    
<span data-ttu-id="43a62-p118">максимальное число потоков, диапазон даты и времени и порядок сортировки. Можно указать любое сочетание следующих свойств, например, можно указать только свойство **MaxThreadCount**.</span><span class="sxs-lookup"><span data-stu-id="43a62-p118">The maximum number of threads, date-time range, and sort order. You can optionally specify any combination of these properties, for example, you can specify only the **MaxThreadCount** property.</span></span>
  
    
    
<span data-ttu-id="43a62-p119">Псевдоним **@** можно использовать для передачи специальные символы. Например `<siteUri>/_api/social.feed/my/likes(OlderThan=@v)?@v=datetime'2013-01-01T08:00'` используется псевдоним **@v** для отправки **:** символов.</span><span class="sxs-lookup"><span data-stu-id="43a62-p119">You can use an **@** alias to pass special characters. For example, `<siteUri>/_api/social.feed/my/likes(OlderThan=@v)?@v=datetime'2013-01-01T08:00'` uses the **@v** alias to send a **:** character.</span></span>
  
    
    

### <a name="response"></a><span data-ttu-id="43a62-278">Ответ</span><span class="sxs-lookup"><span data-stu-id="43a62-278">Response</span></span>

<span data-ttu-id="43a62-279">Тип:  [SP. Social.SocialRestFeed](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestFeed)</span><span class="sxs-lookup"><span data-stu-id="43a62-279">Type:  [SP.Social.SocialRestFeed](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestFeed)</span></span>
  
    
    
<span data-ttu-id="43a62-280">канала, который содержит сообщения, содержащие упоминание текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="43a62-280">A feed that contains posts that mention the current user.</span></span>
  
    
    
<span data-ttu-id="43a62-p120">В следующем примере ответа представляет один поток, который упоминания текущего пользователя. Поток  это тип потока **MentionReference** (значение = **3**), для свойства **PostReference** ссылается на фактический post.</span><span class="sxs-lookup"><span data-stu-id="43a62-p120">The following response example represents one thread that mentions the current user. The thread is a **MentionReference** thread type (value = **3**) whose **PostReference** property references the actual post.</span></span>
  
    
    



```

{"d":{
  "__metadata":{
    "id":"http://serverName/sites/dev/_api/social.feed/my/mentionfeed",
    "uri":"http://serverName/sites/dev/_api/social.feed/my/mentionfeed",
    "type":"SP.Social.SocialRestFeed"
  },
  "SocialFeed":{
    "__metadata":{"type":"SP.Social.SocialFeed"},
    "Attributes":1,
    "NewestProcessed":"2013-04-15T05:05:19Z",
    "OldestProcessed":"2013-04-15T05:05:19Z",
    "Threads":{
      "results":[{
        "__metadata":{"type":"SP.Social.SocialThread"},
        "Actors":{
          "results":[{
            "__metadata":{"type":"SP.Social.SocialActor"},
            "AccountName":"domain\\username1",
            "ActorType":0, 
            "CanFollow":false, 
            "ContentUri":null, 
            "EmailAddress":null, 
            "FollowedContentUri":null, 
            "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b",
            "ImageUri":null, 
            "IsFollowed":false, 
            "LibraryUri":null, 
            "Name":"User1 Name",
            "PersonalSiteUri":"http://serverName:80/my/personal/username1/",
            "Status":0, 
            "StatusText":"This is post 2",
            "TagGuid":"00000000-0000-0000-0000-000000000000",
            "Title":null, 
            "Uri":"http://serverName:80/my/Person.aspx?accountname=domain%5Cusername1"
          },{
            "__metadata":{"type":"SP.Social.SocialActor"},
            "AccountName":"domain\\username2",
            "ActorType":0, 
            "CanFollow":true, 
            "ContentUri":null, 
            "EmailAddress":"username2@somecompany.com",
            "FollowedContentUri":null, 
            "Id":"1.ed418efb7f984ee49ce276c9c5441938.de1675d4929d431894c18908ac53516a.65da910de21f4e40abb318ba33520931.0c37852b34d0418e91c62ac25af4be5b",
            "ImageUri":"http://serverName:80/my/User Photos/Profile Pictures/username2_MThumb.jpg",
            "IsFollowed":true, 
            "LibraryUri":null, 
            "Name":"User2 Name",
            "PersonalSiteUri":"http://serverName/my/personal/username2",
            "Status":6, 
            "StatusText":"@User1 Name presented at the conference.", 
            "TagGuid":"00000000-0000-0000-0000-000000000000",
            "Title":"SOME TITLE",
            "Uri":"http://serverName:80/my/Person.aspx?accountname=domain%5Cusername2"
          }]
        },
        "Attributes":0, 
        "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.ec5198399300401fb44f0f5c9d8dea80.15.15.S-1-5-21-2127521184-1604012920-1887927527-66602",
        "OwnerIndex":0, 
        "Permalink":"http://serverName:80/my/ThreadView.aspx?ThreadID=1.ed418efb7f984ee49ce276c9c5441938.de1675d4929d431894c18908ac53516a.65da910de21f4e40abb318ba33520931.0c37852b34d0418e91c62ac25af4be5b.ca83f758aab04065bc303398f2701eb9.10.10.S-1-5-21-124525095-708259637-1543119021-628175",
        "PostReference":{
          "__metadata":{"type":"SP.Social.SocialPostReference"},
          "Digest":null,
          "Post":{
            "__metadata":{"type":"SP.Social.SocialPost"},
            "Attachment":null,
            "Attributes":23,
            "AuthorIndex":1,
            "CreatedTime":"2013-04-15T05:05:12.0102795Z",
            "Id":"1.ed418efb7f984ee49ce276c9c5441938.de1675d4929d431894c18908ac53516a.65da910de21f4e40abb318ba33520931.0c37852b34d0418e91c62ac25af4be5b.ca83f758aab04065bc303398f2701eb9.10.10.S-1-5-21-124525095-708259637-1543119021-628175",
            "LikerInfo":{
              "__metadata":{"type":"SP.Social.SocialPostActorInfo"},
              "IncludesCurrentUser":false,
              "Indexes":{"results":[]},
              "TotalCount":0
            },
            "ModifiedTime":"2013-04-15T05:05:12.0102795Z",
            "Overlays":{
              "results":[{
                "__metadata":{"type":"SP.Social.SocialDataOverlay"},
                "ActorIndexes":{"results":[0]},
                "Index":1,
                "Length":18,
                "LinkUri":null,
                "OverlayType":1
              }]
            },
            "PostType":0,
            "PreferredImageUri":null,
            "Source":{
              "__metadata":{"type":"SP.Social.SocialLink"},
              "Text":null,
              "Uri":null
            },
            "Text":"@User1 Name presented at the conference."
          },
          "ThreadId":"1.ed418efb7f984ee49ce276c9c5441938.de1675d4929d431894c18908ac53516a.65da910de21f4e40abb318ba33520931.0c37852b34d0418e91c62ac25af4be5b.ca83f758aab04065bc303398f2701eb9.10.10.S-1-5-21-124525095-708259637-1543119021-628175",
          "ThreadOwnerIndex":1
        },
        "Replies":{"results":[]},
        "RootPost":{
          "__metadata":{"type":"SP.Social.SocialPost"},
          "Attachment":null,
          "Attributes":14, 
          "AuthorIndex":1, 
          "CreatedTime":"2013-04-15T05:05:19Z",
          "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.ec5198399300401fb44f0f5c9d8dea80.15.15.S-1-5-21-2127521184-1604012920-1887927527-66602",
          "LikerInfo":null, 
          "ModifiedTime":"2013-04-15T05:05:19Z",
          "Overlays":{
          "results":[{
            "__metadata":{"type":"SP.Social.SocialDataOverlay"},
            "ActorIndexes":{"results":[1]}, 
            "Index":13, 
            "Length":10, 
            "LinkUri":null, 
            "OverlayType":1
          }]
        },
        "PostType":0, 
        "PreferredImageUri":"http://serverName:80/_layouts/15/Images/mention.11x11x32.png",
        "Source":{
          "__metadata":{"type":"SP.Social.SocialLink"},
          "Text":null,
          "Uri":null
        },
        "Text":"Mentioned by User2 Name."},
        "Status":0,
        "ThreadType":3,
        "TotalReplyCount":0
      }]
    },
    "UnreadMentionCount":1
  }
}}
```


## <a name="mymentionfeedclearunreadmentioncount"></a><span data-ttu-id="43a62-283">Мои/MentionFeed/ClearUnreadMentionCount</span><span class="sxs-lookup"><span data-stu-id="43a62-283">My/MentionFeed/ClearUnreadMentionCount</span></span>
<span data-ttu-id="43a62-284"><a name="bk_myMentionFeedClearUnreadMentionCount"> </a></span><span class="sxs-lookup"><span data-stu-id="43a62-284"></span></span>

<span data-ttu-id="43a62-285">Получает канал микроблога сообщения, содержащие упоминание текущего пользователя, представленного типы **MentionReference** потоков и число непрочитанных упоминание пользователей на 0.</span><span class="sxs-lookup"><span data-stu-id="43a62-285">Gets the feed of microblog posts that mention the current user, represented by **MentionReference** thread types, and sets the user's unread mention count to 0.</span></span> <span data-ttu-id="43a62-286">В разделе [Справочник по потоки и потоки дайджест в веб-каналов социальных SharePoint](reference-threads-and-digest-threads-in-sharepoint-server-social-feeds.md).</span><span class="sxs-lookup"><span data-stu-id="43a62-286">See [Reference threads and digest threads in SharePoint social feeds](reference-threads-and-digest-threads-in-sharepoint-server-social-feeds.md).</span></span>
  
    
    

### <a name="endpoint-uri-structure"></a><span data-ttu-id="43a62-287">Структура URI конечной точки</span><span class="sxs-lookup"><span data-stu-id="43a62-287">Endpoint URI structure</span></span>

 <span data-ttu-id="43a62-288">**POST** `http://<siteCollection>/<site>/_api/social.feed/my/mentionfeed/clearunreadmentioncount`</span><span class="sxs-lookup"><span data-stu-id="43a62-288">**POST** `http://<siteCollection>/<site>/_api/social.feed/my/mentionfeed/clearunreadmentioncount`</span></span>
  
    
    

### <a name="request-parameter"></a><span data-ttu-id="43a62-289">Параметр запроса</span><span class="sxs-lookup"><span data-stu-id="43a62-289">Request parameter</span></span>

 <span data-ttu-id="43a62-290">_feedOptions_</span><span class="sxs-lookup"><span data-stu-id="43a62-290">_feedOptions_</span></span>
  
    
    
<span data-ttu-id="43a62-291">тип:  [SP. Social.SocialFeedOptions](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialFeedOptions)</span><span class="sxs-lookup"><span data-stu-id="43a62-291">Type:  [SP.Social.SocialFeedOptions](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialFeedOptions)</span></span>
  
    
    
<span data-ttu-id="43a62-292">этого параметра необходимо отправить как пустая строка в атрибуте **data** текст запроса, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="43a62-292">This parameter must be sent as an empty string in the **data** attribute of the request body, as shown in the following example.</span></span>
  
    
    

```

'feedOptions': {
  '__metadata': {
    'type': 'SP.Social.SocialFeedOptions'
  }, 
}
```


### <a name="response"></a><span data-ttu-id="43a62-293">Ответ</span><span class="sxs-lookup"><span data-stu-id="43a62-293">Response</span></span>

<span data-ttu-id="43a62-294">Тип:  [SP. Social.SocialRestFeed](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestFeed)</span><span class="sxs-lookup"><span data-stu-id="43a62-294">Type:  [SP.Social.SocialRestFeed](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestFeed)</span></span>
  
    
    
<span data-ttu-id="43a62-295">упоминание текущего пользователя веб-канала.</span><span class="sxs-lookup"><span data-stu-id="43a62-295">The current user's mention feed.</span></span>
  
    
    
<span data-ttu-id="43a62-p122">В следующем примере ответа представляет канал упоминание для текущего пользователя. Поток  это тип потока **MentionReference** (значение = **3**), для свойства **PostReference** ссылается на фактический post. Счетчик непрочитанных упоминание удаляется после загрузки веб-канал.</span><span class="sxs-lookup"><span data-stu-id="43a62-p122">The following response example represents the current user's mention feed. The thread is a **MentionReference** thread type (value = **3**) whose **PostReference** property references the actual post. The unread mention count is cleared after the feed is retrieved.</span></span>
  
    
    



```

{"d":{
  "__metadata":{
    "id":"http://serverName/sites/dev/_api/social.feed/my/mentionfeed",
    "uri":"http://serverName/sites/dev/_api/social.feed/my/mentionfeed",
    "type":"SP.Social.SocialRestFeed" 
  },
  "SocialFeed":{
    "__metadata":{"type":"SP.Social.SocialFeed"},
    "Attributes":1,
    "NewestProcessed":"2013-04-15T05:05:19Z",
    "OldestProcessed":"2013-04-15T05:05:19Z",
    "Threads":{
      "results":[{
      "__metadata":{"type":"SP.Social.SocialThread"},
      "Actors":{
        "results":[{
          "__metadata":{"type":"SP.Social.SocialActor"},
          "AccountName":"domain\\username1",
          "ActorType":0, 
          "CanFollow":false, 
          "ContentUri":null, 
          "EmailAddress":null, 
          "FollowedContentUri":null, 
          "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b",
          "ImageUri":null, 
          "IsFollowed":false, 
          "LibraryUri":null, 
          "Name":"User1 Name",
          "PersonalSiteUri":"http://serverName:80/my/personal/username1/",
          "Status":0, 
          "StatusText":"Posted with REST.", 
          "TagGuid":"00000000-0000-0000-0000-000000000000",
          "Title":null, 
          "Uri":"http://serverName:80/my/Person.aspx?accountname=domain%5Cusername1"
        },{
          "__metadata":{"type":"SP.Social.SocialActor"},
          "AccountName":"domain\\username2",
          "ActorType":0, 
          "CanFollow":true, 
          "ContentUri":null, 
          "EmailAddress":"username2@somecompany.com",
          "FollowedContentUri":null, 
          "Id":"1.ed418efb7f984ee49ce276c9c5441938.de1675d4929d431894c18908ac53516a.65da910de21f4e40abb318ba33520931.0c37852b34d0418e91c62ac25af4be5b",
          "ImageUri":"http://serverName:80/my/User Photos/Profile Pictures/username2_MThumb.jpg",
          "IsFollowed":true, 
          "LibraryUri":null, 
          "Name":"User2 Name",
          "PersonalSiteUri":"http://serverName/my/personal/username2",
          "Status":6, 
          "StatusText":"This is post 1 from the specified user.", 
          "TagGuid":"00000000-0000-0000-0000-000000000000",
          "Title":"SOME TITLE",
          "Uri":"http://serverName:80/my/Person.aspx?accountname=domain%5Cusername2"
        }]
      },
      "Attributes":0, 
      "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.ec5198399300401fb44f0f5c9d8dea80.15.15.S-1-5-21-2127521184-1604012920-1887927527-66602",
      "OwnerIndex":0, 
      "Permalink":"http://serverName:80/my/ThreadView.aspx?ThreadID=1.ed418efb7f984ee49ce276c9c5441938.de1675d4929d431894c18908ac53516a.65da910de21f4e40abb318ba33520931.0c37852b34d0418e91c62ac25af4be5b.ca83f758aab04065bc303398f2701eb9.10.10.S-1-5-21-124525095-708259637-1543119021-628175",
      "PostReference":{
        "__metadata":{"type":"SP.Social.SocialPostReference"},
        "Digest":null, 
        "Post":{
          "__metadata":{"type":"SP.Social.SocialPost"},
          "Attachment":null, 
          "Attributes":23, 
          "AuthorIndex":1, 
          "CreatedTime":"2013-04-15T05:05:12.0102795Z",
          "Id":"1.ed418efb7f984ee49ce276c9c5441938.de1675d4929d431894c18908ac53516a.65da910de21f4e40abb318ba33520931.0c37852b34d0418e91c62ac25af4be5b.ca83f758aab04065bc303398f2701eb9.10.10.S-1-5-21-124525095-708259637-1543119021-628175",
          "LikerInfo":{
            "__metadata":{"type":"SP.Social.SocialPostActorInfo"},
            "IncludesCurrentUser":false, 
            "Indexes":{"results":[]},
            "TotalCount":0
          },
          "ModifiedTime":"2013-04-15T05:05:12.0102795Z",
          "Overlays":{
            "results":[{
              "__metadata":{"type":"SP.Social.SocialDataOverlay"},
              "ActorIndexes":{"results":[0]}, 
              "Index":1, 
              "Length":18, 
              "LinkUri":null, 
              "OverlayType":1
            }]
          },
          "PostType":0, 
          "PreferredImageUri":null, 
          "Source":{
            "__metadata":{"type":"SP.Social.SocialLink"},
            "Text":null, 
            "Uri":null
          },
          "Text":"@User1 Name presented at the conference."}, 
          "ThreadId":"1.ed418efb7f984ee49ce276c9c5441938.de1675d4929d431894c18908ac53516a.65da910de21f4e40abb318ba33520931.0c37852b34d0418e91c62ac25af4be5b.ca83f758aab04065bc303398f2701eb9.10.10.S-1-5-21-124525095-708259637-1543119021-628175",
          "ThreadOwnerIndex":1
        },
        "Replies":{"results":[]},
        "RootPost":{
          "__metadata":{"type":"SP.Social.SocialPost"},
          "Attachment":null, 
          "Attributes":14, 
          "AuthorIndex":1, 
          "CreatedTime":"2013-04-15T05:05:19Z",
          "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.ec5198399300401fb44f0f5c9d8dea80.15.15.S-1-5-21-2127521184-1604012920-1887927527-66602",
          "LikerInfo":null, 
          "ModifiedTime":"2013-04-15T05:05:19Z",
          "Overlays":{
            "results":[{
              "__metadata":{"type":"SP.Social.SocialDataOverlay"},
              "ActorIndexes":{"results":[1]}, 
              "Index":13, 
              "Length":10, 
              "LinkUri":null, 
              "OverlayType":1
            }]
          },
          "PostType":0, 
          "PreferredImageUri":"http://serverName:80/_layouts/15/Images/mention.11x11x32.png",
          "Source":{
            "__metadata":{"type":"SP.Social.SocialLink"},
            "Text":null, 
            "Uri":null
          },
          "Text":"Mentioned by User2 Name."
        }, 
        "Status":0, 
        "ThreadType":3, 
        "TotalReplyCount":0
      }]
    },
    "UnreadMentionCount":1
  }
}}
```


## <a name="myunreadmentioncount"></a><span data-ttu-id="43a62-299">Мои/UnreadMentionCount</span><span class="sxs-lookup"><span data-stu-id="43a62-299">My/UnreadMentionCount</span></span>
<span data-ttu-id="43a62-300"><a name="bk_myUnreadMentionCount"> </a></span><span class="sxs-lookup"><span data-stu-id="43a62-300"></span></span>

<span data-ttu-id="43a62-301">Возвращает количество непрочитанных упоминания для текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="43a62-301">Gets the count of unread mentions for the current user.</span></span>
  
    
    

### <a name="endpoint-uri-structure"></a><span data-ttu-id="43a62-302">Структура URI конечной точки</span><span class="sxs-lookup"><span data-stu-id="43a62-302">Endpoint URI structure</span></span>

 <span data-ttu-id="43a62-303">**GET** `http://<siteCollection>/<site>/_api/social.feed/my/unreadmentioncount`</span><span class="sxs-lookup"><span data-stu-id="43a62-303">**GET** `http://<siteCollection>/<site>/_api/social.feed/my/unreadmentioncount`</span></span>
  
    
    

### <a name="request-parameter"></a><span data-ttu-id="43a62-304">Параметр запроса</span><span class="sxs-lookup"><span data-stu-id="43a62-304">Request parameter</span></span>

<span data-ttu-id="43a62-305">Нет.</span><span class="sxs-lookup"><span data-stu-id="43a62-305">None.</span></span>
  
    
    

### <a name="response"></a><span data-ttu-id="43a62-306">Ответ</span><span class="sxs-lookup"><span data-stu-id="43a62-306">Response</span></span>

<span data-ttu-id="43a62-307">Тип: **Int32**</span><span class="sxs-lookup"><span data-stu-id="43a62-307">Type: **Int32**</span></span>
  
    
    
<span data-ttu-id="43a62-308">счетчик непрочитанных упоминания для текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="43a62-308">The count of unread mentions for the current user.</span></span>
  
    
    
<span data-ttu-id="43a62-309">В следующем примере ответа представляет счетчик непрочитанных упоминание 1.</span><span class="sxs-lookup"><span data-stu-id="43a62-309">The following response example represents an unread mention count of 1.</span></span>
  
    
    



```

{"d":{"UnreadMentionCount":1}}
```


## <a name="actor"></a><span data-ttu-id="43a62-310">Actor (субъект)</span><span class="sxs-lookup"><span data-stu-id="43a62-310">Actor</span></span>
<span data-ttu-id="43a62-311"><a name="bk_actor"> </a></span><span class="sxs-lookup"><span data-stu-id="43a62-311"></span></span>

<span data-ttu-id="43a62-312">Получает сведения о указанного пользователя и текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="43a62-312">Gets information about the specified user and the current user.</span></span>
  
> [!NOTE]
> <span data-ttu-id="43a62-p123">[!Примечание] Конечная точка  `actor` устанавливает указанного пользователя или сайта веб-канала в качестве контекста для любой последующих ресурсов в URI. Например `http://contoso.com/_api/social.feed/actor(item='domain\\user')/feed` получает личные веб-канала для указанного пользователя и `http://contoso.com/_api/social.feed/actor(item=@v)/feed?@v='http://<server>/<teamSite>/newsfeed.aspx'` получает веб-канал сайта team указанного сайта.</span><span class="sxs-lookup"><span data-stu-id="43a62-p123">The  `actor` endpoint sets the specified user or site feed as the context for any subsequent resource in the URI. For example, `http://contoso.com/_api/social.feed/actor(item='domain\\user')/feed` gets the personal feed for the specified user and `http://contoso.com/_api/social.feed/actor(item=@v)/feed?@v='http://<server>/<teamSite>/newsfeed.aspx'` gets the site feed for the specified team site.</span></span>
  
    
    


### <a name="endpoint-uri-structure"></a><span data-ttu-id="43a62-315">Структура URI конечной точки</span><span class="sxs-lookup"><span data-stu-id="43a62-315">Endpoint URI structure</span></span>

 <span data-ttu-id="43a62-316">**GET** `http://<siteCollection>/<site>/_api/social.feed/actor(item='domain\\user')`</span><span class="sxs-lookup"><span data-stu-id="43a62-316">**GET** `http://<siteCollection>/<site>/_api/social.feed/actor(item='domain\\user')`</span></span>
  
    
    
 <span data-ttu-id="43a62-317">**GET** `http://<siteCollection>/<site>/_api/social.feed/actor(item=@v)?@v='i:0"%23".f|membership|user@domain.com'`</span><span class="sxs-lookup"><span data-stu-id="43a62-317">**GET** `http://<siteCollection>/<site>/_api/social.feed/actor(item=@v)?@v='i:0"%23".f|membership|user@domain.com'`</span></span>
  
    
    

### <a name="request-parameter"></a><span data-ttu-id="43a62-318">Параметр запроса</span><span class="sxs-lookup"><span data-stu-id="43a62-318">Request parameter</span></span>

 <span data-ttu-id="43a62-319">_item_</span><span class="sxs-lookup"><span data-stu-id="43a62-319">_item_</span></span>
  
    
    
<span data-ttu-id="43a62-320">тип: **String**</span><span class="sxs-lookup"><span data-stu-id="43a62-320">Type: **String**</span></span>
  
    
    
<span data-ttu-id="43a62-321">имя учетной записи указанного пользователя.</span><span class="sxs-lookup"><span data-stu-id="43a62-321">The account name of the specified user.</span></span>
  
    
    
<span data-ttu-id="43a62-p124">Параметр  _item_ отправить в строке запроса. Псевдоним **@** можно использовать для передачи специальные символы. К примеру `<siteUri>/_api/social.feed/actor(item=@v)?@v='i:0"%23".f|membership|user@domain.com'` использует псевдоним **@v** и **"%23"** кодирования для отправки **#** символов.</span><span class="sxs-lookup"><span data-stu-id="43a62-p124">You send the  _item_ parameter in the query string. You can use an **@** alias to pass special characters. For example, `<siteUri>/_api/social.feed/actor(item=@v)?@v='i:0"%23".f|membership|user@domain.com'` uses the **@v** alias and the **"%23"** encoding to send a **#** character.</span></span>
  
    
    

### <a name="response"></a><span data-ttu-id="43a62-325">Ответ</span><span class="sxs-lookup"><span data-stu-id="43a62-325">Response</span></span>

<span data-ttu-id="43a62-326">Тип:  [SP. Social.SocialRestActor](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestActor)</span><span class="sxs-lookup"><span data-stu-id="43a62-326">Type:  [SP.Social.SocialRestActor](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestActor)</span></span>
  
    
    
<span data-ttu-id="43a62-327">сведения о указанного пользователя и текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="43a62-327">Information about the specified user and the current user.</span></span>
  
    
    
<span data-ttu-id="43a62-328">Свойства **SocialRestActor** можно вызвать по отдельности в URI, например `http://<siteCollection>/<site>/_api/social.feed/actor(item='domain\\user')/followableitem` возвращает только свойство **FollowableItem** для указанного субъекта.</span><span class="sxs-lookup"><span data-stu-id="43a62-328">You can call **SocialRestActor** properties individually in the URI, for example `http://<siteCollection>/<site>/_api/social.feed/actor(item='domain\\user')/followableitem` gets only the **FollowableItem** property for the specified actor.</span></span>
  
    
    
<span data-ttu-id="43a62-329">В следующем примере ответа представляет сведения о указанного пользователя и текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="43a62-329">The following response example represents information about the specified user and the current user.</span></span>
  
    
    



```
{"d":{
  "__metadata":{
    "id":"http://serverName/sites/dev/_api/social.feed/actor(Item=@ai)/?@ai='domain\\username2'",
    "uri":"http://serverName/sites/dev/_api/social.feed/actor(Item=@ai)/?@ai='domain%5cusername2'",
    "type":"SP.Social.SocialRestActor"
  },
  "FollowableItem":"domain\\username2",
  "FollowableItemActor":{
    "__metadata":{"type":"SP.Social.SocialActor"},
    "AccountName":"domain\\username2",
    "ActorType":0,
    "CanFollow":true,
    "ContentUri":null,
    "EmailAddress":"username2@somecompany.com",
    "FollowedContentUri":null,
    "Id":"1.ed418efb7f984ee49ce276c9c5441938.de1675d4929d431894c18908ac53516a.65da910de21f4e40abb318ba33520931.0c37852b34d0418e91c62ac25af4be5b",
    "ImageUri":"http://serverName:80/my/User Photos/Profile Pictures/username2_MThumb.jpg",
    "IsFollowed":true,
    "LibraryUri":null,
    "Name":"User2 Name",
    "PersonalSiteUri":"http://serverName/my/personal/username2",
    "Status":0,
    "StatusText":"",
    "TagGuid":"00000000-0000-0000-0000-000000000000",
    "Title":"SOME TITLE",
    "Uri":"http://serverName:80/my/Person.aspx?accountname=domain%5Cusername2"
  },
  "Me":{
    "__metadata":{"type":"SP.Social.SocialActor"},
    "AccountName":"domain\\username1",
    "ActorType":0,
    "CanFollow":false,
    "ContentUri":null,
    "EmailAddress":null,
    "FollowedContentUri":null,
    "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b",
    "ImageUri":null,
    "IsFollowed":false,
    "LibraryUri":null,
    "Name":"User1 Name",
    "PersonalSiteUri":"http://serverName/my/personal/username1/",
    "Status":0,
    "StatusText":"This is post 2",
    "TagGuid":"00000000-0000-0000-0000-000000000000",
    "Title":null,
    "Uri":"http://serverName:80/my/Person.aspx?accountname=domain%5Cusername1"
  }
}}
```


## <a name="actorfeed"></a><span data-ttu-id="43a62-330">Actor/веб-канал</span><span class="sxs-lookup"><span data-stu-id="43a62-330">Actor/Feed</span></span>
<span data-ttu-id="43a62-331"><a name="bk_actorFeed"> </a></span><span class="sxs-lookup"><span data-stu-id="43a62-331"></span></span>

<span data-ttu-id="43a62-332">Получает веб-канал активности по указанному пользователю ( **Personal** канал типа) или получает указанного веб-канал сайта.</span><span class="sxs-lookup"><span data-stu-id="43a62-332">Gets the feed of activity by the specified user ( **Personal** feed type) or gets the specified site feed.</span></span>
  
    
    

### <a name="endpoint-uri-structure"></a><span data-ttu-id="43a62-333">Структура URI конечной точки</span><span class="sxs-lookup"><span data-stu-id="43a62-333">Endpoint URI structure</span></span>

 <span data-ttu-id="43a62-334">**GET** `http://<siteCollection>/<site>/_api/social.feed/actor(item='domain\\user')/feed`</span><span class="sxs-lookup"><span data-stu-id="43a62-334">**GET** `http://<siteCollection>/<site>/_api/social.feed/actor(item='domain\\user')/feed`</span></span>
  
    
    
 <span data-ttu-id="43a62-335">**GET** `http://<siteCollection>/<site>/_api/social.feed/actor(item=@v)/feed?@v='i:0"%23".f|membership|user@domain.com'`</span><span class="sxs-lookup"><span data-stu-id="43a62-335">**GET** `http://<siteCollection>/<site>/_api/social.feed/actor(item=@v)/feed?@v='i:0"%23".f|membership|user@domain.com'`</span></span>
  
    
    
 <span data-ttu-id="43a62-336">**GET** `http://<siteCollection>/<site>/_api/social.feed/actor(item='domain\\user')/feed(MaxThreadCount=10,SortOrder=1,NewerThan=@v)?@v=datetime'2013-01-01T08:00'`</span><span class="sxs-lookup"><span data-stu-id="43a62-336">**GET** `http://<siteCollection>/<site>/_api/social.feed/actor(item='domain\\user')/feed(MaxThreadCount=10,SortOrder=1,NewerThan=@v)?@v=datetime'2013-01-01T08:00'`</span></span>
  
    
    
 <span data-ttu-id="43a62-337">**GET** `http://<siteCollection>/<site>/_api/social.feed/actor(item=@v)/feed?@v='http://<teamSiteUri>/newsfeed.aspx'`</span><span class="sxs-lookup"><span data-stu-id="43a62-337">**GET** `http://<siteCollection>/<site>/_api/social.feed/actor(item=@v)/feed?@v='http://<teamSiteUri>/newsfeed.aspx'`</span></span>
  
    
    

### <a name="request-parameter"></a><span data-ttu-id="43a62-338">Параметр запроса</span><span class="sxs-lookup"><span data-stu-id="43a62-338">Request parameter</span></span>

 <span data-ttu-id="43a62-339">_feedOptions_ (необязательно)</span><span class="sxs-lookup"><span data-stu-id="43a62-339">_feedOptions_ (optional)</span></span>
  
    
    
<span data-ttu-id="43a62-340">Тип:  [SP. Social.SocialFeedOptions](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialFeedOptions)</span><span class="sxs-lookup"><span data-stu-id="43a62-340">Type:  [SP.Social.SocialFeedOptions](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialFeedOptions)</span></span>
  
    
    
<span data-ttu-id="43a62-p125">максимальное число потоков, диапазон даты и времени и порядок сортировки. Можно указать любое сочетание следующих свойств, например, можно указать только свойство **MaxThreadCount**.</span><span class="sxs-lookup"><span data-stu-id="43a62-p125">The maximum number of threads, date-time range, and sort order. You can optionally specify any combination of these properties, for example, you can specify only the **MaxThreadCount** property.</span></span>
  
    
    
<span data-ttu-id="43a62-p126">Псевдоним **@** можно использовать для передачи специальные символы. К примеру `<siteUri>/_api/social.feed/actor(item=@v)/feed(NewerThan=@x)?@v='i:0"%23".f|membership|user@domain.com'&amp;@x=datetime'2013-01-01T08:00'` использует псевдоним **@v** и **"%23"** кодировку для отправки **#** символов и псевдоним **@x** для отправки **:** символов.</span><span class="sxs-lookup"><span data-stu-id="43a62-p126">You can use an **@** alias to pass special characters. For example, `<siteUri>/_api/social.feed/actor(item=@v)/feed(NewerThan=@x)?@v='i:0"%23".f|membership|user@domain.com'&amp;@x=datetime'2013-01-01T08:00'` uses the **@v** alias and the **"%23"** encoding to send a **#** character, and the **@x** alias to send a **:** character.</span></span>
  
    
    

### <a name="response"></a><span data-ttu-id="43a62-345">Ответ</span><span class="sxs-lookup"><span data-stu-id="43a62-345">Response</span></span>

<span data-ttu-id="43a62-346">Тип:  [SP. Social.SocialRestFeed](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestFeed)</span><span class="sxs-lookup"><span data-stu-id="43a62-346">Type:  [SP.Social.SocialRestFeed](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestFeed)</span></span>
  
    
    
<span data-ttu-id="43a62-347">личные веб-канал указанного пользователя или сайта, веб-канал с указанным URI.</span><span class="sxs-lookup"><span data-stu-id="43a62-347">The personal feed of the specified user or the site feed at the specified URI.</span></span>
  
    
    
<span data-ttu-id="43a62-348">В следующем примере ответа представляет личных веб-канал указанного пользователя.</span><span class="sxs-lookup"><span data-stu-id="43a62-348">The following response example represents personal feed of the specified user.</span></span>
  
    
    



```

{"d":{
  "__metadata":{
    "id":"http://serverName/sites/dev/_api/social.feed/actor(Item=@ai)/feed/?@ai='domain\\username2'",
    "uri":"http://serverName/sites/dev/_api/social.feed/actor(Item=@ai)/feed/?@ai='domain%5cusername2'",
    "type":"SP.Social.SocialRestFeed"
  },
  "SocialFeed":{
    "__metadata":{"type":"SP.Social.SocialFeed"},
    "Attributes":1, 
    "NewestProcessed":"2013-04-16T22:40:55Z",
    "OldestProcessed":"2013-04-16T22:40:07Z",
    "Threads":{
      "results":[{
        "__metadata":{"type":"SP.Social.SocialThread"},
        "Actors":{
          "results":[{
            "__metadata":{"type":"SP.Social.SocialActor"},
            "AccountName":"domain\\username2",
            "ActorType":0, 
            "CanFollow":true, 
            "ContentUri":null, 
            "EmailAddress":"username2@somecompany.com",
            "FollowedContentUri":null, 
            "Id":"1.ed418efb7f984ee49ce276c9c5441938.de1675d4929d431894c18908ac53516a.65da910de21f4e40abb318ba33520931.0c37852b34d0418e91c62ac25af4be5b",
            "ImageUri":"http://serverName:80/my/User%20Photos/Profile%20Pictures/username2_MThumb.jpg",
            "IsFollowed":true, 
            "LibraryUri":null, 
            "Name":"User2 Name",
            "PersonalSiteUri":"http://serverName:80/my/personal/username2",
            "Status":0, 
            "StatusText":"This is post 1 from the specified user.", 
            "TagGuid":"00000000-0000-0000-0000-000000000000",
            "Title":"SOME TITLE",
            "Uri":"http://serverName:80/my/Person.aspx?accountname=domain%5Cusername2"
          },{
            "__metadata":{"type":"SP.Social.SocialActor"},
            "AccountName":"domain\\username1",
            "ActorType":0, 
            "CanFollow":false, 
            "ContentUri":null, 
            "EmailAddress":null, 
            "FollowedContentUri":null, 
            "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b",
            "ImageUri":null, 
            "IsFollowed":false, 
            "LibraryUri":null, 
            "Name":"User1 Name",
            "PersonalSiteUri":"http://serverName/my/personal/username1/",
            "Status":0, 
            "StatusText":"",
            "TagGuid":"00000000-0000-0000-0000-000000000000",
            "Title":null, 
            "Uri":"http://serverName:80/my/Person.aspx?accountname=domain%5Cusername1"
          }]
        },
        "Attributes":0, 
        "Id":"1.ed418efb7f984ee49ce276c9c5441938.de1675d4929d431894c18908ac53516a.65da910de21f4e40abb318ba33520931.0c37852b34d0418e91c62ac25af4be5b.4cb7a5d36cb14d62b0fb68ef98f9765e.15.15.S-1-5-21-124525095-708259637-1543119021-628175",
        "OwnerIndex":0, 
        "Permalink":"http://serverName:80/my/ThreadView.aspx?ThreadID=1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.c554cbf1934b4c82bb1d43ebf961de92.17.17.S-1-5-21-2127521184-1604012920-1887927527-66602",
        "PostReference":{
          "__metadata":{"type":"SP.Social.SocialPostReference"},
          "Digest":null, 
          "Post":null, 
          "ThreadId":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.c554cbf1934b4c82bb1d43ebf961de92.17.17.S-1-5-21-2127521184-1604012920-1887927527-66602",
          "ThreadOwnerIndex":1
        },
        "Replies":{"results":[]},
        "RootPost":{
          "__metadata":{"type":"SP.Social.SocialPost"},
          "Attachment":null, 
          "Attributes":14, 
          "AuthorIndex":0, 
          "CreatedTime":"2013-04-16T22:40:55Z",
          "Id":"1.ed418efb7f984ee49ce276c9c5441938.de1675d4929d431894c18908ac53516a.65da910de21f4e40abb318ba33520931.0c37852b34d0418e91c62ac25af4be5b.4cb7a5d36cb14d62b0fb68ef98f9765e.15.15.S-1-5-21-124525095-708259637-1543119021-628175",
          "LikerInfo":null, 
          "ModifiedTime":"2013-04-16T22:40:55Z",
          "Overlays":{
            "results":[{
              "__metadata":{"type":"SP.Social.SocialDataOverlay"},
              "ActorIndexes":{"results":[0]}, 
              "Index":0, 
              "Length":10, 
              "LinkUri":null, 
              "OverlayType":1
            },{
              "__metadata":{"type":"SP.Social.SocialDataOverlay"},
              "ActorIndexes":{"results":[1]}, 
              "Index":32, 
              "Length":18, 
              "LinkUri":null, 
              "OverlayType":1
            }]
          },
          "PostType":0, 
          "PreferredImageUri":"http://serverName:80/_layouts/15/Images/RepliedTo.11x11x32.png",
          "Source":{
            "__metadata":{"type":"SP.Social.SocialLink"},
            "Text":null, 
            "Uri":null
          },
          "Text":"User2 Name replied to a post by User1 Name." 
        },
        "Status":0, 
        "ThreadType":2, 
        "TotalReplyCount":0
      },{
        "__metadata":{"type":"SP.Social.SocialThread"},
        "Actors":{
          "results":[{
            "__metadata":{"type":"SP.Social.SocialActor"},
            "AccountName":"domain\\username2",
            "ActorType":0, 
            "CanFollow":true, 
            "ContentUri":null, 
            "EmailAddress":"username2@somecompany.com",
            "FollowedContentUri":null, 
            "Id":"1.ed418efb7f984ee49ce276c9c5441938.de1675d4929d431894c18908ac53516a.65da910de21f4e40abb318ba33520931.0c37852b34d0418e91c62ac25af4be5b",
            "ImageUri":"http://serverName:80/my/User%20Photos/Profile%20Pictures/username2_MThumb.jpg",
            "IsFollowed":true,
            "LibraryUri":null,
            "Name":"User2 Name",
            "PersonalSiteUri":"http://serverName:80/my/personal/username2",
            "Status":0, 
            "StatusText":"This is post 1 from the specified user.", 
            "TagGuid":"00000000-0000-0000-0000-000000000000",
            "Title":"SOME TITLE",
            "Uri":"http://serverName:80/my/Person.aspx?accountname=domain%5Cusername2"
          }]
        },
        "Attributes":6, 
        "Id":"1.ed418efb7f984ee49ce276c9c5441938.de1675d4929d431894c18908ac53516a.65da910de21f4e40abb318ba33520931.0c37852b34d0418e91c62ac25af4be5b.b83675d28e264e69823205ad4e76df9f.14.14.S-1-5-21-124525095-708259637-1543119021-628175",
        "OwnerIndex":0, 
        "Permalink":"http://serverName:80/my/ThreadView.aspx?ThreadID=1.ed418efb7f984ee49ce276c9c5441938.de1675d4929d431894c18908ac53516a.65da910de21f4e40abb318ba33520931.0c37852b34d0418e91c62ac25af4be5b.b83675d28e264e69823205ad4e76df9f.14.14.S-1-5-21-124525095-708259637-1543119021-628175",
        "PostReference":null, 
        "Replies":{"results":[]},
        "RootPost":{
          "__metadata":{"type":"SP.Social.SocialPost"},
          "Attachment":null, 
          "Attributes":23, 
          "AuthorIndex":0, 
          "CreatedTime":"2013-04-16T22:40:07Z",
          "Id":"1.ed418efb7f984ee49ce276c9c5441938.de1675d4929d431894c18908ac53516a.65da910de21f4e40abb318ba33520931.0c37852b34d0418e91c62ac25af4be5b.b83675d28e264e69823205ad4e76df9f.14.14.S-1-5-21-124525095-708259637-1543119021-628175",
          "LikerInfo":{
            "__metadata":{"type":"SP.Social.SocialPostActorInfo"},
            "IncludesCurrentUser":false, 
            "Indexes":{"results":[]},
            "TotalCount":0
          },
          "ModifiedTime":"2013-04-16T22:40:07Z",
          "Overlays":{"results":[]},
          "PostType":0, 
          "PreferredImageUri":null, 
          "Source":{
            "__metadata":{"type":"SP.Social.SocialLink"},
            "Text":null, 
            "Uri":null
          },
          "Text":"This is post 1 from the specified user."
        }, 
        "Status":0, 
        "ThreadType":0, 
        "TotalReplyCount":0
      }]
    },
    "UnreadMentionCount":0
  }
}}
```


## <a name="actorfeedpost"></a><span data-ttu-id="43a62-349">Actor/канал/Post</span><span class="sxs-lookup"><span data-stu-id="43a62-349">Actor/Feed/Post</span></span>
<span data-ttu-id="43a62-350"><a name="bk_actorFeedPost"> </a></span><span class="sxs-lookup"><span data-stu-id="43a62-350"></span></span>

<span data-ttu-id="43a62-351">Создает корневой post в указанном веб-канал сайта.</span><span class="sxs-lookup"><span data-stu-id="43a62-351">Creates a root post in the specified site feed.</span></span>
  
    
    
<span data-ttu-id="43a62-p127">Вы можете разместить только в контексте текущего пользователя. Не удается создать корневой post в веб-канал другого пользователя, но можно ответить на post другому пользователю. В разделе  [Поместить/ответ](social-feed-rest-api-reference-for-sharepoint.md#bk_postReply).</span><span class="sxs-lookup"><span data-stu-id="43a62-p127">You can post only in the context of the current user. You cannot create a root post in a different user's feed, but you can reply to another user's post. See  [Post/Reply](social-feed-rest-api-reference-for-sharepoint.md#bk_postReply).</span></span>
  
> [!NOTE]
> <span data-ttu-id="43a62-355">[!Примечание] Не следует путать этот ресурс  `Post` с ресурсом `Post` , представляющий конкретный поток или post.</span><span class="sxs-lookup"><span data-stu-id="43a62-355">Don't confuse this  `Post` resource with the `Post` resource that represents a specific thread or post.</span></span>
  
    
    


### <a name="endpoint-uri-structure"></a><span data-ttu-id="43a62-356">Структура URI конечной точки</span><span class="sxs-lookup"><span data-stu-id="43a62-356">Endpoint URI structure</span></span>

 <span data-ttu-id="43a62-357">**POST** `http://<siteCollection>/<site>/_api/social.feed/actor(item=@v)/feed/post?@v='http://<siteCollection>/<teamSite>/newsfeed.aspx'`</span><span class="sxs-lookup"><span data-stu-id="43a62-357">**POST** `http://<siteCollection>/<site>/_api/social.feed/actor(item=@v)/feed/post?@v='http://<siteCollection>/<teamSite>/newsfeed.aspx'`</span></span>
  
    
    

### <a name="request-parameter"></a><span data-ttu-id="43a62-358">Параметр запроса</span><span class="sxs-lookup"><span data-stu-id="43a62-358">Request parameter</span></span>

 <span data-ttu-id="43a62-359">_restCreationData_</span><span class="sxs-lookup"><span data-stu-id="43a62-359">_restCreationData_</span></span>
  
    
    
<span data-ttu-id="43a62-360">тип:  [SP. Social.SocialRestPostCreationData](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestPostCreationData)</span><span class="sxs-lookup"><span data-stu-id="43a62-360">Type:  [SP.Social.SocialRestPostCreationData](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestPostCreationData)</span></span>
  
    
    
<span data-ttu-id="43a62-361">**null** идентификатор и свойства нового post, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="43a62-361">A **null** ID and the properties of the new post, as shown in the following example.</span></span>
  
    
    

```

'restCreationData':{
  '__metadata':{ 
    'type':'SP.Social.SocialRestPostCreationData'
  },
  'ID':null, 
  'creationData':{ 
    '__metadata':{ 
      'type':'SP.Social.SocialPostCreationData'
    },
    'ContentText':'This post was published using REST.', 
    'UpdateStatusText':false
  } 
}
```


### <a name="response"></a><span data-ttu-id="43a62-362">Ответ</span><span class="sxs-lookup"><span data-stu-id="43a62-362">Response</span></span>

<span data-ttu-id="43a62-363">Тип:  [SP. Social.SocialRestThread](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestThread)</span><span class="sxs-lookup"><span data-stu-id="43a62-363">Type:  [SP.Social.SocialRestThread](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestThread)</span></span>
  
    
    
<span data-ttu-id="43a62-364">поток, который содержит новый корневой post.</span><span class="sxs-lookup"><span data-stu-id="43a62-364">A thread that contains the new root post.</span></span>
  
    
    
<span data-ttu-id="43a62-365">В следующем примере ответа представляет поток, который содержит новый корневой post.</span><span class="sxs-lookup"><span data-stu-id="43a62-365">The following response example represents the thread that contains the new root post.</span></span>
  
    
    



```

{"d":{
  "__metadata":{
    "id":"http://serverName/sites/dev/_api/social.feed/post(ID=@ai)/?@ai='8.c4bb19b167a448a3be9b597522152420.c305b669c2b649e9b820e7feabe3c095.c4bb19b167a448a3be9b597522152420.0c37852b34d0418e91c62ac25af4be5b.866d920d78d949a394f26073b767cb19.3.3.1'",
    "uri":"http://serverName/sites/dev/_api/social.feed/post(ID=@ai)/?@ai='8.c4bb19b167a448a3be9b597522152420.c305b669c2b649e9b820e7feabe3c095.c4bb19b167a448a3be9b597522152420.0c37852b34d0418e91c62ac25af4be5b.866d920d78d949a394f26073b767cb19.3.3.1'",
    "type":"SP.Social.SocialRestThread"
  },
  "ID":"8.c4bb19b167a448a3be9b597522152420.c305b669c2b649e9b820e7feabe3c095.c4bb19b167a448a3be9b597522152420.0c37852b34d0418e91c62ac25af4be5b.866d920d78d949a394f26073b767cb19.3.3.1",
  "SocialThread":{
    "__metadata":{"type":"SP.Social.SocialThread"},
    "Actors":{
      "results":[{
        "__metadata":{"type":"SP.Social.SocialActor"},
        "AccountName":null, 
        "ActorType":2, 
        "CanFollow":true, 
        "ContentUri":"http://serverName:80/sites/teamSite",
        "EmailAddress":null, 
        "FollowedContentUri":null, 
        "Id":"8.c4bb19b167a448a3be9b597522152420.c305b669c2b649e9b820e7feabe3c095.c4bb19b167a448a3be9b597522152420.0c37852b34d0418e91c62ac25af4be5b",
        "ImageUri":null, 
        "IsFollowed":true, 
        "LibraryUri":null, 
        "Name":"Team Site",
        "PersonalSiteUri":null, 
        "Status":0, 
        "StatusText":null, 
        "TagGuid":"00000000-0000-0000-0000-000000000000",
        "Title":null, 
        "Uri":"http://serverName:80/sites/teamSite"
      },{
        "__metadata":{"type":"SP.Social.SocialActor"},
        "AccountName":"domain\\username1",
        "ActorType":0, 
        "CanFollow":false, 
        "ContentUri":null, 
        "EmailAddress":null, 
        "FollowedContentUri":null, 
        "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b",
        "ImageUri":null, 
        "IsFollowed":false, 
        "LibraryUri":null, 
        "Name":"User1 Name",
        "PersonalSiteUri":"http://serverName:80/my/personal/username1/",
        "Status":0, 
        "StatusText":"Posted with REST.", 
        "TagGuid":"00000000-0000-0000-0000-000000000000",
        "Title":null, 
        "Uri":"http://serverName:80/my/Person.aspx?accountname=domain%5Cusername1"
      }]
    },
    "Attributes":6,
    "Id":"8.c4bb19b167a448a3be9b597522152420.c305b669c2b649e9b820e7feabe3c095.c4bb19b167a448a3be9b597522152420.0c37852b34d0418e91c62ac25af4be5b.866d920d78d949a394f26073b767cb19.3.3.1",
    "OwnerIndex":0,
    "Permalink":"http://serverName/sites/teamSite/newsfeed.aspx?ThreadID=8.c4bb19b167a448a3be9b597522152420.c305b669c2b649e9b820e7feabe3c095.c4bb19b167a448a3be9b597522152420.0c37852b34d0418e91c62ac25af4be5b.866d920d78d949a394f26073b767cb19.3.3.1",
    "PostReference":null,
    "Replies":{"results":[]},
    "RootPost":{
      "__metadata":{"type":"SP.Social.SocialPost"},
      "Attachment":null, 
      "Attributes":23, 
      "AuthorIndex":1, 
      "CreatedTime":"2013-04-18T22:44:11.8485085Z",
      "Id":"8.c4bb19b167a448a3be9b597522152420.c305b669c2b649e9b820e7feabe3c095.c4bb19b167a448a3be9b597522152420.0c37852b34d0418e91c62ac25af4be5b.866d920d78d949a394f26073b767cb19.3.3.1",
      "LikerInfo":{
        "__metadata":{"type":"SP.Social.SocialPostActorInfo"},
        "IncludesCurrentUser":false, 
        "Indexes":{"results":[]},
        "TotalCount":0
      },
      "ModifiedTime":"2013-04-18T22:44:11.8485085Z",
      "Overlays":{"results":[]},
      "PostType":0, 
      "PreferredImageUri":null, 
      "Source":{
        "__metadata":{"type":"SP.Social.SocialLink"},
        "Text":null, 
        "Uri":null
      },
      "Text":"Posted with REST." 
    },
    "Status":0, 
    "ThreadType":0, 
    "TotalReplyCount":0
  }
}}
```


## <a name="post"></a><span data-ttu-id="43a62-366">Публикация</span><span class="sxs-lookup"><span data-stu-id="43a62-366">Post</span></span>
<span data-ttu-id="43a62-367"><a name="bk_post"> </a></span><span class="sxs-lookup"><span data-stu-id="43a62-367"></span></span>

<span data-ttu-id="43a62-368">Получает полный поток, который содержит запись указанного микроблога.</span><span class="sxs-lookup"><span data-stu-id="43a62-368">Gets a full thread that contains the specified microblog post.</span></span>
  
    
    

### <a name="endpoint-uri-structure"></a><span data-ttu-id="43a62-369">Структура URI конечной точки</span><span class="sxs-lookup"><span data-stu-id="43a62-369">Endpoint URI structure</span></span>

 <span data-ttu-id="43a62-370">**POST** `http://<siteCollection>/<site>/_api/social.feed/post`</span><span class="sxs-lookup"><span data-stu-id="43a62-370">**POST** `http://<siteCollection>/<site>/_api/social.feed/post`</span></span>
  
    
    

### <a name="request-parameter"></a><span data-ttu-id="43a62-371">Параметр запроса</span><span class="sxs-lookup"><span data-stu-id="43a62-371">Request parameter</span></span>

 <span data-ttu-id="43a62-372">**ID**</span><span class="sxs-lookup"><span data-stu-id="43a62-372">**ID**</span></span>
  
    
    
<span data-ttu-id="43a62-373">тип: **String**</span><span class="sxs-lookup"><span data-stu-id="43a62-373">Type: **String**</span></span>
  
    
    
<span data-ttu-id="43a62-374">уникальный идентификатор post, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="43a62-374">The unique identifier of the post, as shown in the following example.</span></span>
  
    
    

```

'ID':'1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.644240140e0b43379883ebcb859deaab.27.32.S-1-5-21-2127521184-1604012920-1887927527-66602'
```


### <a name="response"></a><span data-ttu-id="43a62-375">Ответ</span><span class="sxs-lookup"><span data-stu-id="43a62-375">Response</span></span>

<span data-ttu-id="43a62-376">Тип:  [SP. Social.SocialRestThread](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestThread)</span><span class="sxs-lookup"><span data-stu-id="43a62-376">Type:  [SP.Social.SocialRestThread](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestThread)</span></span>
  
    
    
<span data-ttu-id="43a62-377">полный поток, который содержит указанный post.</span><span class="sxs-lookup"><span data-stu-id="43a62-377">A full thread that contains the specified post.</span></span>
  
    
    
<span data-ttu-id="43a62-p128">В следующем примере ответа представляет полный поток, который содержит указанный post. В отличие от потоков дайджест (которые содержат только два последних ответов) полного потока содержит все ответы.</span><span class="sxs-lookup"><span data-stu-id="43a62-p128">The following response example represents the full thread that contains the specified post. Unlike digest threads (which contain only the two most recent replies), a full thread contains all replies.</span></span>
  
    
    



```
{"d":{
  "__metadata":{
    "id":"http://serverName/sites/dev/_api/social.feed/post(ID=@ai)/?@ai='1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.62bff48184bd433b8f7b04f6ea76268b.27.27.S-1-5-21-2127521184-1604012920-1887927527-66602'",
    "uri":"http://serverName/sites/dev/_api/social.feed/post(ID=@ai)/?@ai='1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.62bff48184bd433b8f7b04f6ea76268b.27.27.S-1-5-21-2127521184-1604012920-1887927527-66602'",
    "type":"SP.Social.SocialRestThread"
  },
  "ID":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.62bff48184bd433b8f7b04f6ea76268b.27.27.S-1-5-21-2127521184-1604012920-1887927527-66602",
  "SocialThread":{
    "__metadata":{"type":"SP.Social.SocialThread"},
    "Actors":{
      "results":[{
        "__metadata":{"type":"SP.Social.SocialActor"},
        "AccountName":"domain\\username1",
        "ActorType":0, 
        "CanFollow":false, 
        "ContentUri":null, 
        "EmailAddress":null, 
        "FollowedContentUri":null, 
        "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b",
        "ImageUri":null, 
        "IsFollowed":false, 
        "LibraryUri":null, 
        "Name":"User1 Name",
        "PersonalSiteUri":"http://serverName:80/my/personal/username1/",
        "Status":0, 
        "StatusText":"Posted with REST.", 
        "TagGuid":"00000000-0000-0000-0000-000000000000",
        "Title":null, 
        "Uri":"http://serverName:80/my/Person.aspx?accountname=domain%5Cusername1"
      },{
        "__metadata":{"type":"SP.Social.SocialActor"},
        "AccountName":"domain\\username2",
        "ActorType":0, 
        "CanFollow":true, 
        "ContentUri":null, 
        "EmailAddress":"username2@somecompany.com",
        "FollowedContentUri":null, 
        "Id":"1.ed418efb7f984ee49ce276c9c5441938.de1675d4929d431894c18908ac53516a.65da910de21f4e40abb318ba33520931.0c37852b34d0418e91c62ac25af4be5b","ImageUri":"http://serverName:80/my/User Photos/Profile Pictures/username2_MThumb.jpg",
        "IsFollowed":true, 
        "LibraryUri":null,"Name":"User2 Name","PersonalSiteUri":"http://serverName/my/personal/username2","Status":6,"StatusText":"This is post 1 from the specified user.", 
        "TagGuid":"00000000-0000-0000-0000-000000000000",
        "Title":"SOME TITLE",
        "Uri":"http://serverName:80/my/Person.aspx?accountname=domain%5Cusername2"
      }]
    },
    "Attributes":6, 
    "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.62bff48184bd433b8f7b04f6ea76268b.27.27.S-1-5-21-2127521184-1604012920-1887927527-66602",
    "OwnerIndex":0, 
    "Permalink":"http://serverName:80/my/ThreadView.aspx?ThreadID=1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.62bff48184bd433b8f7b04f6ea76268b.27.27.S-1-5-21-2127521184-1604012920-1887927527-66602",
    "PostReference":null, 
    "Replies":{
      "results":[{
        "__metadata":{"type":"SP.Social.SocialPost"},
        "Attachment":null, 
        "Attributes":23, 
        "AuthorIndex":1, 
        "CreatedTime":"2013-04-23T23:02:40Z",
        "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.644240140e0b43379883ebcb859deaab.27.32.S-1-5-21-2127521184-1604012920-1887927527-66602",
        "LikerInfo":{
          "__metadata":{"type":"SP.Social.SocialPostActorInfo"},
          "IncludesCurrentUser":false, 
          "Indexes":{"results":[]},
          "TotalCount":0
        },
        "ModifiedTime":"2013-04-23T23:02:40Z",
        "Overlays":{"results":[]},
        "PostType":1, 
        "PreferredImageUri":null, 
        "Source":{
          "__metadata":{"type":"SP.Social.SocialLink"},
          "Text":null, 
          "Uri":null
        },
        "Text":"This is a reply." 
      }]
    },
    "RootPost":{
      "__metadata":{"type":"SP.Social.SocialPost"},
      "Attachment":null, 
      "Attributes":23, 
      "AuthorIndex":0, 
      "CreatedTime":"2013-04-17T19:45:45Z",
      "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.62bff48184bd433b8f7b04f6ea76268b.27.27.S-1-5-21-2127521184-1604012920-1887927527-66602",
      "LikerInfo":{
        "__metadata":{"type":"SP.Social.SocialPostActorInfo"},
        "IncludesCurrentUser":false, 
        "Indexes":{"results":[1]}, 
        "TotalCount":1
      },
      "ModifiedTime":"2013-04-23T23:02:41Z",
      "Overlays":{"results":[]},
      "PostType":0, 
      "PreferredImageUri":null, 
      "Source":{
        "__metadata":{"type":"SP.Social.SocialLink"},
        "Text":null, 
        "Uri":null
      },
      "Text":"Posted with REST." 
    },
    "Status":0, 
    "ThreadType":0, 
    "TotalReplyCount":1
  }
}}
```


## <a name="postreply"></a><span data-ttu-id="43a62-380">Поместить/ответ</span><span class="sxs-lookup"><span data-stu-id="43a62-380">Post/Reply</span></span>
<span data-ttu-id="43a62-381"><a name="bk_postReply"> </a></span><span class="sxs-lookup"><span data-stu-id="43a62-381"></span></span>

<span data-ttu-id="43a62-382">Публикации в ответ на указанном post.</span><span class="sxs-lookup"><span data-stu-id="43a62-382">Posts a reply to the specified post.</span></span>
  
    
    

### <a name="endpoint-uri-structure"></a><span data-ttu-id="43a62-383">Структура URI конечной точки</span><span class="sxs-lookup"><span data-stu-id="43a62-383">Endpoint URI structure</span></span>

 <span data-ttu-id="43a62-384">**POST** `http://<siteCollection>/<site>/_api/social.feed/post/reply`</span><span class="sxs-lookup"><span data-stu-id="43a62-384">**POST** `http://<siteCollection>/<site>/_api/social.feed/post/reply`</span></span>
  
    
    

### <a name="request-parameter"></a><span data-ttu-id="43a62-385">Параметр запроса</span><span class="sxs-lookup"><span data-stu-id="43a62-385">Request parameter</span></span>

 <span data-ttu-id="43a62-386">_restCreationData_</span><span class="sxs-lookup"><span data-stu-id="43a62-386">_restCreationData_</span></span>
  
    
    
<span data-ttu-id="43a62-387">тип:  [SP. Social.SocialRestPostCreationData](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestPostCreationData)</span><span class="sxs-lookup"><span data-stu-id="43a62-387">Type:  [SP.Social.SocialRestPostCreationData](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestPostCreationData)</span></span>
  
    
    
<span data-ttu-id="43a62-388">идентификатор post отвечать и свойства ответ, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="43a62-388">The ID of the post to reply to and the properties of the reply, as shown in the following example.</span></span>
  
    
    

```

'restCreationData':{
  '__metadata':{
    'type': 'SP.Social.SocialRestPostCreationData'
  },
  'ID':'1.4975bef1e1bc42608c1dfae9f320c751.35c9fd7b79904800aaa5f74684bf0f75.623664921f034e8d814c000267d3e5e4.0c37852b34d0418e91c62ac25af4be5b.230d3c5272fc499f88ac0b74b2f4512f.119.119.S-1-5-21-124525095-708259637-1543119021-565461',
  'creationData':{
    '__metadata':{
      'type':'SP.Social.SocialPostCreationData'
    },
    'ContentText':'Posted with REST.', 
    'UpdateStatusText':false
  }
}
```


### <a name="response"></a><span data-ttu-id="43a62-389">Ответ</span><span class="sxs-lookup"><span data-stu-id="43a62-389">Response</span></span>

<span data-ttu-id="43a62-390">Тип:  [SP. Social.SocialRestThread](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestThread)</span><span class="sxs-lookup"><span data-stu-id="43a62-390">Type:  [SP.Social.SocialRestThread](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestThread)</span></span>
  
    
    
<span data-ttu-id="43a62-391">дайджест измененные потока, который включает в себя указанного сообщения.</span><span class="sxs-lookup"><span data-stu-id="43a62-391">A digest of the modified thread that includes the specified post.</span></span>
  
    
    
<span data-ttu-id="43a62-392">В следующем примере ответа представляет поток, который содержит указанный post и ответ.</span><span class="sxs-lookup"><span data-stu-id="43a62-392">The following response example represents the thread that contains the specified post and reply.</span></span>
  
    
    



```

{"d":{
  "__metadata":{
    "id":"http://serverName/sites/dev/_api/social.feed/post(ID=@ai)/?@ai='1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.4316bdaa94bf4984be5dfea1ba96954e.26.26.S-1-5-21-2127521184-1604012920-1887927527-66602'",
    "uri":"http://serverName/sites/dev/_api/social.feed/post(ID=@ai)/?@ai='1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.4316bdaa94bf4984be5dfea1ba96954e.26.26.S-1-5-21-2127521184-1604012920-1887927527-66602'",
    "type":"SP.Social.SocialRestThread"
  },
  "ID":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.4316bdaa94bf4984be5dfea1ba96954e.26.26.S-1-5-21-2127521184-1604012920-1887927527-66602",
  "SocialThread":{
    "__metadata":{"type":"SP.Social.SocialThread"},
    "Actors":{
      "results":[{
      "__metadata":{
        "type":"SP.Social.SocialActor"
      },
      "AccountName":"domain\\username1",
      "ActorType":0, 
      "CanFollow":false, 
      "ContentUri":null, 
      "EmailAddress":null, 
      "FollowedContentUri":null, 
      "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b",
      "ImageUri":null, 
      "IsFollowed":false, 
      "LibraryUri":null, 
      "Name":"User1 Name",
      "PersonalSiteUri":"http://serverName:80/my/personal/username1/",
      "Status":0, 
      "StatusText":"Posted with REST.", 
      "TagGuid":"00000000-0000-0000-0000-000000000000",
      "Title":null,"Uri":"http://serverName:80/my/Person.aspx?accountname=domain%5Cusername1"}
    ]}, 
    "Attributes":6, 
    "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.4316bdaa94bf4984be5dfea1ba96954e.26.26.S-1-5-21-2127521184-1604012920-1887927527-66602",
    "OwnerIndex":0, 
    "Permalink":"http://serverName:80/my/ThreadView.aspx?ThreadID=1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.4316bdaa94bf4984be5dfea1ba96954e.26.26.S-1-5-21-2127521184-1604012920-1887927527-66602",
    "PostReference":null, 
    "Replies":{
      "results":[{
        "__metadata":{"type":"SP.Social.SocialPost"},
        "Attachment":null, 
        "Attributes":23, 
        "AuthorIndex":0, 
        "CreatedTime":"2013-04-17T20:52:51.0650454Z",
        "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.ce3ac812293c4903b5c406efe01b9432.26.29.S-1-5-21-2127521184-1604012920-1887927527-66602",
        "LikerInfo":{
          "__metadata":{"type":"SP.Social.SocialPostActorInfo"},
          "IncludesCurrentUser":false, 
          "Indexes":{"results":[]},
          "TotalCount":0
        },
        "ModifiedTime":"2013-04-17T20:52:51.0650454Z",
        "Overlays":{"results":[]},
        "PostType":1, 
        "PreferredImageUri":null, 
        "Source":{
          "__metadata":{"type":"SP.Social.SocialLink"},
          "Text":null, 
          "Uri":null
        },
        "Text":"Replied with REST." 
      }]
    },
    "RootPost":{
      "__metadata":{"type":"SP.Social.SocialPost"},
      "Attachment":null, 
      "Attributes":23, 
      "AuthorIndex":0, 
      "CreatedTime":"2013-04-17T19:33:17Z",
      "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.4316bdaa94bf4984be5dfea1ba96954e.26.26.S-1-5-21-2127521184-1604012920-1887927527-66602",
      "LikerInfo":{
        "__metadata":{"type":"SP.Social.SocialPostActorInfo"},
        "IncludesCurrentUser":false, 
        "Indexes":{"results":[]},
        "TotalCount":0
      },
      "ModifiedTime":"2013-04-17T20:52:51.6900774Z",
      "Overlays":{"results":[]},
      "PostType":0, 
      "PreferredImageUri":null, 
      "Source":{
        "__metadata":{"type":"SP.Social.SocialLink"},
        "Text":null, 
        "Uri":null
      },
      "Text":"Posted with REST." 
    },
    "Status":0, 
    "ThreadType":0, 
    "TotalReplyCount":1
  }
}}
```


## <a name="postdelete"></a><span data-ttu-id="43a62-393">Запись и удаление</span><span class="sxs-lookup"><span data-stu-id="43a62-393">Post/Delete</span></span>
<span data-ttu-id="43a62-394"><a name="bk_postDelete"> </a></span><span class="sxs-lookup"><span data-stu-id="43a62-394"></span></span>

<span data-ttu-id="43a62-p129">Удаляет указанный микроблога post. Если процедуры post корневого, удаляется весь поток.</span><span class="sxs-lookup"><span data-stu-id="43a62-p129">Deletes the specified microblog post. If the post is the root post, the whole thread is deleted.</span></span>
  
    
    

### <a name="endpoint-uri-structure"></a><span data-ttu-id="43a62-397">Структура URI конечной точки</span><span class="sxs-lookup"><span data-stu-id="43a62-397">Endpoint URI structure</span></span>

 <span data-ttu-id="43a62-398">**POST** `http://<siteCollection>/<site>/_api/social.feed/post/delete`</span><span class="sxs-lookup"><span data-stu-id="43a62-398">**POST** `http://<siteCollection>/<site>/_api/social.feed/post/delete`</span></span>
  
    
    

### <a name="request-parameter"></a><span data-ttu-id="43a62-399">Параметр запроса</span><span class="sxs-lookup"><span data-stu-id="43a62-399">Request parameter</span></span>

 <span data-ttu-id="43a62-400">**ID**</span><span class="sxs-lookup"><span data-stu-id="43a62-400">**ID**</span></span>
  
    
    
<span data-ttu-id="43a62-401">тип: **String**</span><span class="sxs-lookup"><span data-stu-id="43a62-401">Type: **String**</span></span>
  
    
    
<span data-ttu-id="43a62-402">идентификатор записи, чтобы удалить, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="43a62-402">The ID of the post to delete, as shown in the following example.</span></span>
  
    
    

```

'ID':'1.94fdcc5fc39b4a2c99ae4570caf02321.d0a03fb1761a404a9a8e7f9f5ec58e17.5a1067e8af65410b9e2ba6a74a4b718a.0c37852b34d0418e91c62ac25af4be5b.9dbfb5598e2248d7b57eee57abf2e7c1.31.31.S-1-5-21-124525095-708259637-1543119021-565461'
```


### <a name="response"></a><span data-ttu-id="43a62-403">Ответ</span><span class="sxs-lookup"><span data-stu-id="43a62-403">Response</span></span>

<span data-ttu-id="43a62-404">Нет.</span><span class="sxs-lookup"><span data-stu-id="43a62-404">None.</span></span>
  
    
    

```
{"d":{"Delete":null}}
```


## <a name="postlike"></a><span data-ttu-id="43a62-405">Публикация/Like</span><span class="sxs-lookup"><span data-stu-id="43a62-405">Post/Like</span></span>
<span data-ttu-id="43a62-406"><a name="bk_postLike"> </a></span><span class="sxs-lookup"><span data-stu-id="43a62-406"></span></span>

<span data-ttu-id="43a62-407">Делает liker запись указанного микроблога текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="43a62-407">Makes the current user a liker of the specified microblog post.</span></span>
  
    
    

### <a name="endpoint-uri-structure"></a><span data-ttu-id="43a62-408">Структура URI конечной точки</span><span class="sxs-lookup"><span data-stu-id="43a62-408">Endpoint URI structure</span></span>

 <span data-ttu-id="43a62-409">**POST** `http://<siteCollection>/<site>/_api/social.feed/post/like`</span><span class="sxs-lookup"><span data-stu-id="43a62-409">**POST** `http://<siteCollection>/<site>/_api/social.feed/post/like`</span></span>
  
    
    

### <a name="request-parameter"></a><span data-ttu-id="43a62-410">Параметр запроса</span><span class="sxs-lookup"><span data-stu-id="43a62-410">Request parameter</span></span>

 <span data-ttu-id="43a62-411">**ID**</span><span class="sxs-lookup"><span data-stu-id="43a62-411">**ID**</span></span>
  
    
    
<span data-ttu-id="43a62-412">тип: **String**</span><span class="sxs-lookup"><span data-stu-id="43a62-412">Type: **String**</span></span>
  
    
    
<span data-ttu-id="43a62-413">идентификатор post нравится, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="43a62-413">The ID of the post to like, as shown in the following example.</span></span>
  
    
    

```
'ID':'1.94fdcc5fc39b4a2c99ae4570caf02321.d0a03fb1761a404a9a8e7f9f5ec58e17.5a1067e8af65410b9e2ba6a74a4b718a.0c37852b34d0418e91c62ac25af4be5b.9dbfb5598e2248d7b57eee57abf2e7c1.31.31.S-1-5-21-124525095-708259637-1543119021-565461'
```


### <a name="response"></a><span data-ttu-id="43a62-414">Ответ</span><span class="sxs-lookup"><span data-stu-id="43a62-414">Response</span></span>

<span data-ttu-id="43a62-415">Тип:  [SP. Social.SocialRestThread](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestThread)</span><span class="sxs-lookup"><span data-stu-id="43a62-415">Type:  [SP.Social.SocialRestThread](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestThread)</span></span>
  
    
    
<span data-ttu-id="43a62-416">дайджест поток, который содержит указанный post.</span><span class="sxs-lookup"><span data-stu-id="43a62-416">A digest thread that contains the specified post.</span></span>
  
    
    
<span data-ttu-id="43a62-417">В следующем примере ответа представляет поток, который содержит liked post.</span><span class="sxs-lookup"><span data-stu-id="43a62-417">The following response example represents the thread that contains the liked post.</span></span>
  
    
    



```
{"d":{
  "__metadata":{
    "id":"http://serverName/sites/dev/_api/social.feed/post(ID=@ai)/?@ai='1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.4316bdaa94bf4984be5dfea1ba96954e.26.26.S-1-5-21-2127521184-1604012920-1887927527-66602'",
    "uri":"http://serverName/sites/dev/_api/social.feed/post(ID=@ai)/?@ai='1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.4316bdaa94bf4984be5dfea1ba96954e.26.26.S-1-5-21-2127521184-1604012920-1887927527-66602'",
    "type":"SP.Social.SocialRestThread"
  },
  "ID":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.4316bdaa94bf4984be5dfea1ba96954e.26.26.S-1-5-21-2127521184-1604012920-1887927527-66602",
  "SocialThread":{
    "__metadata":{"type":"SP.Social.SocialThread"},
    "Actors":{
      "results":[{
        "__metadata":{"type":"SP.Social.SocialActor"},
        "AccountName":"domain\\username1",
        "ActorType":0, 
        "CanFollow":false, 
        "ContentUri":null, 
        "EmailAddress":null, 
        "FollowedContentUri":null, 
        "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b",
        "ImageUri":null, 
        "IsFollowed":false, 
        "LibraryUri":null, 
        "Name":"User1 Name",
        "PersonalSiteUri":"http://serverName:80/my/personal/username1/",
        "Status":0, 
        "StatusText":"Posted with REST.", 
        "TagGuid":"00000000-0000-0000-0000-000000000000",
        "Title":null, 
        "Uri":"http://serverName:80/my/Person.aspx?accountname=domain%5Cusername1"
      }]
    },
    "Attributes":6, 
    "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.4316bdaa94bf4984be5dfea1ba96954e.26.26.S-1-5-21-2127521184-1604012920-1887927527-66602",
    "OwnerIndex":0, 
    "Permalink":"http://serverName:80/my/ThreadView.aspx?ThreadID=1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.4316bdaa94bf4984be5dfea1ba96954e.26.26.S-1-5-21-2127521184-1604012920-1887927527-66602",
    "PostReference":null, 
    "Replies":{
      "results":[{
        "__metadata":{"type":"SP.Social.SocialPost"},
        "Attachment":null, 
        "Attributes":23, 
        "AuthorIndex":0, 
        "CreatedTime":"2013-04-17T20:52:51.0650454Z",
        "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.ce3ac812293c4903b5c406efe01b9432.26.29.S-1-5-21-2127521184-1604012920-1887927527-66602",
        "LikerInfo":{
          "__metadata":{"type":"SP.Social.SocialPostActorInfo"},
          "IncludesCurrentUser":false, 
          "Indexes":{"results":[]},
          "TotalCount":0
        },
        "ModifiedTime":"2013-04-17T20:52:51.0650454Z",
        "Overlays":{"results":[]},
        "PostType":1, 
        "PreferredImageUri":null, 
        "Source":{
          "__metadata":{"type":"SP.Social.SocialLink"},
          "Text":null, 
          "Uri":null
        },
        "Text":"Replied with REST." 
      }]
    },
    "RootPost":{
      "__metadata":{"type":"SP.Social.SocialPost"},
      "Attachment":null, 
      "Attributes":23, 
      "AuthorIndex":0, 
      "CreatedTime":"2013-04-17T19:33:17Z",
      "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.4316bdaa94bf4984be5dfea1ba96954e.26.26.S-1-5-21-2127521184-1604012920-1887927527-66602",
      "LikerInfo":{
        "__metadata":{"type":"SP.Social.SocialPostActorInfo"},
        "IncludesCurrentUser":true, 
        "Indexes":{"results":[]},
        "TotalCount":1
      },
      "ModifiedTime":"2013-04-17T20:52:51Z",
      "Overlays":{"results":[]},
      "PostType":0, 
      "PreferredImageUri":null, 
      "Source":{
        "__metadata":{"type":"SP.Social.SocialLink"},
        "Text":null, 
        "Uri":null
      },
      "Text":"Posted with REST." 
    },
    "Status":0, 
    "ThreadType":0, 
    "TotalReplyCount":1
  }
}}
```


## <a name="postunlike"></a><span data-ttu-id="43a62-418">Учет аудио- и в отличие от</span><span class="sxs-lookup"><span data-stu-id="43a62-418">Post/Unlike</span></span>
<span data-ttu-id="43a62-419"><a name="bk_postUnlike"> </a></span><span class="sxs-lookup"><span data-stu-id="43a62-419"></span></span>

<span data-ttu-id="43a62-p130">Удаляет текущий пользователь в списке likers для указанного микроблога post. Если текущий пользователь не liker метода post, этот запрос игнорируется.</span><span class="sxs-lookup"><span data-stu-id="43a62-p130">Removes the current user from the list of likers for the specified microblog post. If the current user is not a liker of the post, this request is ignored.</span></span>
  
    
    

### <a name="endpoint-uri-structure"></a><span data-ttu-id="43a62-422">Структура URI конечной точки</span><span class="sxs-lookup"><span data-stu-id="43a62-422">Endpoint URI structure</span></span>

 <span data-ttu-id="43a62-423">**POST** `http://<siteCollection>/<site>/_api/social.feed/post/unlike`</span><span class="sxs-lookup"><span data-stu-id="43a62-423">**POST** `http://<siteCollection>/<site>/_api/social.feed/post/unlike`</span></span>
  
    
    

### <a name="request-parameter"></a><span data-ttu-id="43a62-424">Параметр запроса</span><span class="sxs-lookup"><span data-stu-id="43a62-424">Request parameter</span></span>

 <span data-ttu-id="43a62-425">**ID**</span><span class="sxs-lookup"><span data-stu-id="43a62-425">**ID**</span></span>
  
    
    
<span data-ttu-id="43a62-426">тип: **String**</span><span class="sxs-lookup"><span data-stu-id="43a62-426">Type: **String**</span></span>
  
    
    
<span data-ttu-id="43a62-427">идентификатор post, чтобы остановить возможность, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="43a62-427">The ID of the post to stop liking, as shown in the following example.</span></span>
  
    
    

```

'ID':'1.94fdcc5fc39b4a2c99ae4570caf02321.d0a03fb1761a404a9a8e7f9f5ec58e17.5a1067e8af65410b9e2ba6a74a4b718a.0c37852b34d0418e91c62ac25af4be5b.9dbfb5598e2248d7b57eee57abf2e7c1.31.31.S-1-5-21-124525095-708259637-1543119021-565461'
```


### <a name="response"></a><span data-ttu-id="43a62-428">Ответ</span><span class="sxs-lookup"><span data-stu-id="43a62-428">Response</span></span>

<span data-ttu-id="43a62-429">Тип:  [SP. Social.SocialRestThread](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestThread)</span><span class="sxs-lookup"><span data-stu-id="43a62-429">Type:  [SP.Social.SocialRestThread](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestThread)</span></span>
  
    
    
<span data-ttu-id="43a62-430">дайджест измененные потока, который включает в себя указанного сообщения.</span><span class="sxs-lookup"><span data-stu-id="43a62-430">A digest of the modified thread that includes the specified post.</span></span>
  
    
    
<span data-ttu-id="43a62-431">В следующем примере ответа представляет поток, который содержит post, который пользователь остановил возможность.</span><span class="sxs-lookup"><span data-stu-id="43a62-431">The following response example represents the thread that contains the post that the user stopped liking.</span></span>
  
    
    



```
{"d":{
  "__metadata":{
    "id":"http://serverName/sites/dev/_api/social.feed/post(ID=@ai)/?@ai='1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.4316bdaa94bf4984be5dfea1ba96954e.26.26.S-1-5-21-2127521184-1604012920-1887927527-66602'",
    "uri":"http://serverName/sites/dev/_api/social.feed/post(ID=@ai)/?@ai='1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.4316bdaa94bf4984be5dfea1ba96954e.26.26.S-1-5-21-2127521184-1604012920-1887927527-66602'",
    "type":"SP.Social.SocialRestThread"
  },
  "ID":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.4316bdaa94bf4984be5dfea1ba96954e.26.26.S-1-5-21-2127521184-1604012920-1887927527-66602",
  "SocialThread":{
    "__metadata":{"type":"SP.Social.SocialThread"},
    "Actors":{
      "results":[{
        "__metadata":{"type":"SP.Social.SocialActor"},
        "AccountName":"domain\\username1",
        "ActorType":0, 
        "CanFollow":false, 
        "ContentUri":null, 
        "EmailAddress":null, 
        "FollowedContentUri":null, 
        "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b",
        "ImageUri":null, 
        "IsFollowed":false, 
        "LibraryUri":null, 
        "Name":"User1 Name",
        "PersonalSiteUri":"http://serverName:80/my/personal/username1/",
        "Status":0, 
        "StatusText":"Posted with REST.", 
        "TagGuid":"00000000-0000-0000-0000-000000000000",
        "Title":null, 
        "Uri":"http://serverName:80/my/Person.aspx?accountname=domain%5Cusername1"
      }]
    },
    "Attributes":6, 
    "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.4316bdaa94bf4984be5dfea1ba96954e.26.26.S-1-5-21-2127521184-1604012920-1887927527-66602",
    "OwnerIndex":0, 
    "Permalink":"http://serverName:80/my/ThreadView.aspx?ThreadID=1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.4316bdaa94bf4984be5dfea1ba96954e.26.26.S-1-5-21-2127521184-1604012920-1887927527-66602",
    "PostReference":null, 
    "Replies":{
      "results":[{
        "__metadata":{"type":"SP.Social.SocialPost"},
        "Attachment":null, 
        "Attributes":23, 
        "AuthorIndex":0, 
        "CreatedTime":"2013-04-17T20:52:51.0650454Z",
        "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.ce3ac812293c4903b5c406efe01b9432.26.29.S-1-5-21-2127521184-1604012920-1887927527-66602",
        "LikerInfo":{
          "__metadata":{"type":"SP.Social.SocialPostActorInfo"},
          "IncludesCurrentUser":false, 
          "Indexes":{"results":[]},
          "TotalCount":0
        },
        "ModifiedTime":"2013-04-17T20:52:51.0650454Z",
        "Overlays":{"results":[]},
        "PostType":1, 
        "PreferredImageUri":null, 
        "Source":{
          "__metadata":{"type":"SP.Social.SocialLink"},
          "Text":null, 
          "Uri":null
        },
        "Text":"Replied with REST." 
      }]
    },
    "RootPost":{
      "__metadata":{"type":"SP.Social.SocialPost"},
      "Attachment":null, 
      "Attributes":23, 
      "AuthorIndex":0, 
      "CreatedTime":"2013-04-17T19:33:17Z","Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.4316bdaa94bf4984be5dfea1ba96954e.26.26.S-1-5-21-2127521184-1604012920-1887927527-66602",
      "LikerInfo":{
        "__metadata":{"type":"SP.Social.SocialPostActorInfo"},
        "IncludesCurrentUser":false, 
        "Indexes":{"results":[]},
        "TotalCount":0
      },
      "ModifiedTime":"2013-04-17T20:52:51Z",
      "Overlays":{"results":[]},
      "PostType":0, 
      "PreferredImageUri":null, 
      "Source":{
        "__metadata":{"type":"SP.Social.SocialLink"},
        "Text":null, 
        "Uri":null
      },
      "Text":"Posted with REST." 
    },
    "Status":0,
    "ThreadType":0,
    "TotalReplyCount":1
  }
}}
```


## <a name="postlikers"></a><span data-ttu-id="43a62-432">Публикация/Likers</span><span class="sxs-lookup"><span data-stu-id="43a62-432">Post/Likers</span></span>
<span data-ttu-id="43a62-433"><a name="bk_postLikers"> </a></span><span class="sxs-lookup"><span data-stu-id="43a62-433"></span></span>

<span data-ttu-id="43a62-434">Получает пользователей, как запись указанного микроблога.</span><span class="sxs-lookup"><span data-stu-id="43a62-434">Gets the users who like the specified microblog post.</span></span>
  
    
    

### <a name="endpoint-uri-structure"></a><span data-ttu-id="43a62-435">Структура URI конечной точки</span><span class="sxs-lookup"><span data-stu-id="43a62-435">Endpoint URI structure</span></span>

 <span data-ttu-id="43a62-436">**POST** `http://<siteCollection>/<site>/_api/social.feed/post/likers`</span><span class="sxs-lookup"><span data-stu-id="43a62-436">**POST** `http://<siteCollection>/<site>/_api/social.feed/post/likers`</span></span>
  
    
    

### <a name="request-parameter"></a><span data-ttu-id="43a62-437">Параметр запроса</span><span class="sxs-lookup"><span data-stu-id="43a62-437">Request parameter</span></span>

 <span data-ttu-id="43a62-438">**ID**</span><span class="sxs-lookup"><span data-stu-id="43a62-438">**ID**</span></span>
  
    
    
<span data-ttu-id="43a62-439">тип: **String**</span><span class="sxs-lookup"><span data-stu-id="43a62-439">Type: **String**</span></span>
  
    
    
<span data-ttu-id="43a62-440">идентификатор записи, чтобы получить likers, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="43a62-440">The ID of the post to get the likers for, as shown in the following example.</span></span>
  
    
    

```

'ID':'1.94fdcc5fc39b4a2c99ae4570caf02321.d0a03fb1761a404a9a8e7f9f5ec58e17.5a1067e8af65410b9e2ba6a74a4b718a.0c37852b34d0418e91c62ac25af4be5b.9dbfb5598e2248d7b57eee57abf2e7c1.31.31.S-1-5-21-124525095-708259637-1543119021-565461'
```


### <a name="response"></a><span data-ttu-id="43a62-441">Ответ</span><span class="sxs-lookup"><span data-stu-id="43a62-441">Response</span></span>

 <span data-ttu-id="43a62-442">**Likers**</span><span class="sxs-lookup"><span data-stu-id="43a62-442">**Likers**</span></span>
  
    
    
<span data-ttu-id="43a62-443">тип:  [SP. Social.SocialActor](http://msdn.microsoft.com/library/4e369fd5-b9b0-9804-957e-b3e39c559cd4%28Office.15%29.aspx)[]</span><span class="sxs-lookup"><span data-stu-id="43a62-443">Type:  [SP.Social.SocialActor](http://msdn.microsoft.com/library/4e369fd5-b9b0-9804-957e-b3e39c559cd4%28Office.15%29.aspx)[]</span></span>
  
    
    
<span data-ttu-id="43a62-444">пользователей, как указанного сообщения.</span><span class="sxs-lookup"><span data-stu-id="43a62-444">The users who like the specified post.</span></span>
  
    
    
<span data-ttu-id="43a62-445">В следующем примере ответа представляет пользователей, которые указанного сообщения.</span><span class="sxs-lookup"><span data-stu-id="43a62-445">The following response example represents the users that like the specified post.</span></span>
  
    
    



```
{"d":{
  "Likers":{
    "results":[{
      "__metadata":{"type":"SP.Social.SocialActor"},
      "AccountName":"domain\\username1",
      "ActorType":0, 
      "CanFollow":false, 
      "ContentUri":null, 
      "EmailAddress":null, 
      "FollowedContentUri":null, 
      "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b",
      "ImageUri":null, 
      "IsFollowed":false, 
      "LibraryUri":null, 
      "Name":"User1 Name",
      "PersonalSiteUri":"http://serverName/my/personal/username1/",
      "Status":0, 
      "StatusText":"Posted with REST.", 
      "TagGuid":"00000000-0000-0000-0000-000000000000",
      "Title":null, 
      "Uri":"http://serverName:80/my/Person.aspx?accountname=domain%5Cusername1"
    }]
  }
}}
```


## <a name="postlock"></a><span data-ttu-id="43a62-446">Публикация/блокировки</span><span class="sxs-lookup"><span data-stu-id="43a62-446">Post/Lock</span></span>
<span data-ttu-id="43a62-447"><a name="bk_postLock"> </a></span><span class="sxs-lookup"><span data-stu-id="43a62-447"></span></span>

<span data-ttu-id="43a62-p131">Блокирует указанного потока. Если заблокированный поток записей ответа можно добавить к потоку пока она не заблокирована.</span><span class="sxs-lookup"><span data-stu-id="43a62-p131">Locks the specified thread. If a thread is locked, no reply posts can be added to the thread until it is unlocked.</span></span>
  
    
    

### <a name="endpoint-uri-structure"></a><span data-ttu-id="43a62-450">Структура URI конечной точки</span><span class="sxs-lookup"><span data-stu-id="43a62-450">Endpoint URI structure</span></span>

 <span data-ttu-id="43a62-451">**POST** `http://<siteCollection>/<site>/_api/social.feed/post/lock`</span><span class="sxs-lookup"><span data-stu-id="43a62-451">**POST** `http://<siteCollection>/<site>/_api/social.feed/post/lock`</span></span>
  
    
    

### <a name="request-parameter"></a><span data-ttu-id="43a62-452">Параметр запроса</span><span class="sxs-lookup"><span data-stu-id="43a62-452">Request parameter</span></span>

 <span data-ttu-id="43a62-453">**ID**</span><span class="sxs-lookup"><span data-stu-id="43a62-453">**ID**</span></span>
  
    
    
<span data-ttu-id="43a62-454">тип: **String**</span><span class="sxs-lookup"><span data-stu-id="43a62-454">Type: **String**</span></span>
  
    
    
<span data-ttu-id="43a62-455">идентификатор потока для блокировки, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="43a62-455">The ID of the thread to lock, as shown in the following example.</span></span>
  
    
    

```

'ID':'1.94fdcc5fc39b4a2c99ae4570caf02321.d0a03fb1761a404a9a8e7f9f5ec58e17.5a1067e8af65410b9e2ba6a74a4b718a.0c37852b34d0418e91c62ac25af4be5b.9dbfb5598e2248d7b57eee57abf2e7c1.31.31.S-1-5-21-124525095-708259637-1543119021-565461'
```


### <a name="response"></a><span data-ttu-id="43a62-456">Ответ</span><span class="sxs-lookup"><span data-stu-id="43a62-456">Response</span></span>

<span data-ttu-id="43a62-457">Тип:  [SP. Social.SocialRestThread](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestThread)</span><span class="sxs-lookup"><span data-stu-id="43a62-457">Type:  [SP.Social.SocialRestThread](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestThread)</span></span>
  
    
    
<span data-ttu-id="43a62-458">дайджест блокировки потока.</span><span class="sxs-lookup"><span data-stu-id="43a62-458">A digest of the locked thread.</span></span>
  
    
    
<span data-ttu-id="43a62-p132">В следующем примере ответа представляет блокировки потока. Свойство **Attributes** потока содержит значение побитовое из [SP. Social.SocialThreadAttributes](http://msdn.microsoft.com/library/21ff9f92-3223-bcc7-ceec-7b899ee29b6e%28Office.15%29.aspx) перечисление, указывающее, заблокирован ли потока.</span><span class="sxs-lookup"><span data-stu-id="43a62-p132">The following response example represents a locked thread. The **Attributes** property of the thread contains a bitwise value from the [SP.Social.SocialThreadAttributes](http://msdn.microsoft.com/library/21ff9f92-3223-bcc7-ceec-7b899ee29b6e%28Office.15%29.aspx) enumeration, which indicates whether the thread is locked.</span></span>
  
    
    



```
{"d":{
  "__metadata":{
    "id":"http://serverName/sites/dev/_api/social.feed/post(ID=@ai)/?@ai='1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.4316bdaa94bf4984be5dfea1ba96954e.26.26.S-1-5-21-2127521184-1604012920-1887927527-66602'
    uri":"http://serverName/sites/dev/_api/social.feed/post(ID=@ai)/?@ai='1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.4316bdaa94bf4984be5dfea1ba96954e.26.26.S-1-5-21-2127521184-1604012920-1887927527-66602'",
    "type":"SP.Social.SocialRestThread"
  },
  "ID":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.4316bdaa94bf4984be5dfea1ba96954e.26.26.S-1-5-21-2127521184-1604012920-1887927527-66602",
  "SocialThread":{
  "__metadata":{"type":"SP.Social.SocialThread"},
  "Actors":{
    "results":[{
      "__metadata":{"type":"SP.Social.SocialActor"},
      "AccountName":"domain\\username1",
      "ActorType":0, 
      "CanFollow":false, 
      "ContentUri":null, 
      EmailAddress":null, 
      "FollowedContentUri":null, 
      "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b",
      "ImageUri":null, 
      "IsFollowed":false, 
      "LibraryUri":null, 
      "Name":"User1 Name",
      "PersonalSiteUri":"http://serverName:80/my/personal/username1/",
      "Status":0, 
      "StatusText":"Posted with REST.", 
      "TagGuid":"00000000-0000-0000-0000-000000000000",
      "Title":null, 
      "Uri":"http://serverName:80/my/Person.aspx?accountname=domain%5Cusername1"
    }]
  },
  "Attributes":12,
  "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.4316bdaa94bf4984be5dfea1ba96954e.26.26.S-1-5-21-2127521184-1604012920-1887927527-66602",
  "OwnerIndex":0,
  "Permalink":"http://serverName:80/my/ThreadView.aspx?ThreadID=1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.4316bdaa94bf4984be5dfea1ba96954e.26.26.S-1-5-21-2127521184-1604012920-1887927527-66602",
  "PostReference":null,
  "Replies":{
    "results":[{
      "__metadata":{"type":"SP.Social.SocialPost"},
      "Attachment":null, 
      "Attributes":22, 
      "AuthorIndex":0, 
      "CreatedTime":"2013-04-17T20:52:51.0650454Z",
      "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.ce3ac812293c4903b5c406efe01b9432.26.29.S-1-5-21-2127521184-1604012920-1887927527-66602",
      "LikerInfo":{
        "__metadata":{"type":"SP.Social.SocialPostActorInfo"},
        "IncludesCurrentUser":false, 
        "Indexes":{"results":[]},
        "TotalCount":0
      },
      "ModifiedTime":"2013-04-17T20:52:51.0650454Z",
      "Overlays":{"results":[]},
      "PostType":1, 
      "PreferredImageUri":null, 
      "Source":{
        "__metadata":{"type":"SP.Social.SocialLink"},
        "Text":null, 
        "Uri":null
      },
      "Text":"Replied with REST." 
    }]
  },
  "RootPost":{
    "__metadata":{
      "type":"SP.Social.SocialPost"},
      "Attachment":null, 
      "Attributes":22, 
      "AuthorIndex":0, 
      "CreatedTime":"2013-04-17T19:33:17Z",
      "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.4316bdaa94bf4984be5dfea1ba96954e.26.26.S-1-5-21-2127521184-1604012920-1887927527-66602",
      "LikerInfo":{
        "__metadata":{"type":"SP.Social.SocialPostActorInfo"},
        "IncludesCurrentUser":false, 
        "Indexes":{"results":[]},
        "TotalCount":0
      },
      "ModifiedTime":"2013-04-17T20:52:51Z",
      "Overlays":{"results":[]},
      "PostType":0, 
      "PreferredImageUri":null, 
      "Source":{
        "__metadata":{"type":"SP.Social.SocialLink"},
        "Text":null, 
        "Uri":null
      },
      "Text":"Posted with REST." 
    },
    "Status":0,
    "ThreadType":0,
    "TotalReplyCount":1
  }
}}
```


## <a name="postunlock"></a><span data-ttu-id="43a62-461">POST или разблокировать</span><span class="sxs-lookup"><span data-stu-id="43a62-461">Post/Unlock</span></span>
<span data-ttu-id="43a62-462"><a name="bk_postUnlock"> </a></span><span class="sxs-lookup"><span data-stu-id="43a62-462"></span></span>

<span data-ttu-id="43a62-463">Разблокирует указанного потока.</span><span class="sxs-lookup"><span data-stu-id="43a62-463">Unlocks the specified thread.</span></span>
  
    
    

### <a name="endpoint-uri-structure"></a><span data-ttu-id="43a62-464">Структура URI конечной точки</span><span class="sxs-lookup"><span data-stu-id="43a62-464">Endpoint URI structure</span></span>

 <span data-ttu-id="43a62-465">**POST** `http://<siteCollection>/<site>/_api/social.feed/post/unlock`</span><span class="sxs-lookup"><span data-stu-id="43a62-465">**POST** `http://<siteCollection>/<site>/_api/social.feed/post/unlock`</span></span>
  
    
    

### <a name="request-parameter"></a><span data-ttu-id="43a62-466">Параметр запроса</span><span class="sxs-lookup"><span data-stu-id="43a62-466">Request parameter</span></span>

 <span data-ttu-id="43a62-467">**ID**</span><span class="sxs-lookup"><span data-stu-id="43a62-467">**ID**</span></span>
  
    
    
<span data-ttu-id="43a62-468">тип: **String**</span><span class="sxs-lookup"><span data-stu-id="43a62-468">Type: **String**</span></span>
  
    
    
<span data-ttu-id="43a62-469">идентификатор потока для разблокировки, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="43a62-469">The ID of the thread to unlock, as shown in the following example.</span></span>
  
    
    

```

'ID':'1.94fdcc5fc39b4a2c99ae4570caf02321.d0a03fb1761a404a9a8e7f9f5ec58e17.5a1067e8af65410b9e2ba6a74a4b718a.0c37852b34d0418e91c62ac25af4be5b.9dbfb5598e2248d7b57eee57abf2e7c1.31.31.S-1-5-21-124525095-708259637-1543119021-565461'
```


### <a name="response"></a><span data-ttu-id="43a62-470">Ответ</span><span class="sxs-lookup"><span data-stu-id="43a62-470">Response</span></span>

<span data-ttu-id="43a62-471">Тип:  [SP. Social.SocialRestThread](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestThread)</span><span class="sxs-lookup"><span data-stu-id="43a62-471">Type:  [SP.Social.SocialRestThread](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestThread)</span></span>
  
    
    
<span data-ttu-id="43a62-472">дайджест разблокированными потока.</span><span class="sxs-lookup"><span data-stu-id="43a62-472">A digest of the unlocked thread.</span></span>
  
    
    
<span data-ttu-id="43a62-p133">В следующем примере ответа представляет разблокированными потока. Свойство **Attributes** потока содержит значение побитовое из [SP. Social.SocialThreadAttributes](http://msdn.microsoft.com/library/21ff9f92-3223-bcc7-ceec-7b899ee29b6e%28Office.15%29.aspx) перечисление, указывающее, заблокирован ли потока.</span><span class="sxs-lookup"><span data-stu-id="43a62-p133">The following response example represents the unlocked thread. The **Attributes** property of the thread contains a bitwise value from the [SP.Social.SocialThreadAttributes](http://msdn.microsoft.com/library/21ff9f92-3223-bcc7-ceec-7b899ee29b6e%28Office.15%29.aspx) enumeration, which indicates whether the thread is locked.</span></span>
  
    
    



```
{"d":{
  "__metadata":{
    "id":"http://serverName/sites/dev/_api/social.feed/post(ID=@ai)/?@ai='1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.4316bdaa94bf4984be5dfea1ba96954e.26.26.S-1-5-21-2127521184-1604012920-1887927527-66602'",
    "uri":"http://serverName/sites/dev/_api/social.feed/post(ID=@ai)/?@ai='1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.4316bdaa94bf4984be5dfea1ba96954e.26.26.S-1-5-21-2127521184-1604012920-1887927527-66602'",
    "type":"SP.Social.SocialRestThread"
  },
  "ID":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.4316bdaa94bf4984be5dfea1ba96954e.26.26.S-1-5-21-2127521184-1604012920-1887927527-66602",
  "SocialThread":{
    "__metadata":{"type":"SP.Social.SocialThread"},
    "Actors":{
      "results":[{
        "__metadata":{"type":"SP.Social.SocialActor"},
        "AccountName":"domain\\username1",
        "ActorType":0, 
        "CanFollow":false, 
        "ContentUri":null, 
        "EmailAddress":null, 
        "FollowedContentUri":null, 
        "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b",
        "ImageUri":null, 
        "IsFollowed":false, 
        "LibraryUri":null, 
        "Name":"User1 Name",
        "PersonalSiteUri":"http://serverName:80/my/personal/username1/",
        "Status":0, 
        "StatusText":"Posted with REST.", 
        "TagGuid":"00000000-0000-0000-0000-000000000000",
        "Title":null, 
        "Uri":"http://serverName:80/my/Person.aspx?accountname=domain%5Cusername1"
      }
    ]}, 
    "Attributes":6, 
    "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.4316bdaa94bf4984be5dfea1ba96954e.26.26.S-1-5-21-2127521184-1604012920-1887927527-66602",
    "OwnerIndex":0, 
    "Permalink":"http://serverName:80/my/ThreadView.aspx?ThreadID=1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.4316bdaa94bf4984be5dfea1ba96954e.26.26.S-1-5-21-2127521184-1604012920-1887927527-66602",
    "PostReference":null, 
    "Replies":{
      "results":[{
        "__metadata":{"type":"SP.Social.SocialPost"},
        "Attachment":null, 
        "Attributes":23, 
        "AuthorIndex":0, 
        "CreatedTime":"2013-04-17T20:52:51.0650454Z",
        "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.ce3ac812293c4903b5c406efe01b9432.26.29.S-1-5-21-2127521184-1604012920-1887927527-66602",
        "LikerInfo":{
          "__metadata":{"type":"SP.Social.SocialPostActorInfo"},
          "IncludesCurrentUser":false, 
          "Indexes":{"results":[]},
          "TotalCount":0
        },
        "ModifiedTime":"2013-04-17T20:52:51.0650454Z",
        "Overlays":{"results":[]},
        "PostType":1, 
        "PreferredImageUri":null, 
        "Source":{
          "__metadata":{"type":"SP.Social.SocialLink"},
          "Text":null, 
          "Uri":null
        },
        "Text":"Replied with REST." 
      }]
    },
    "RootPost":{
      "__metadata":{"type":"SP.Social.SocialPost"},
      
      "Attachment":null, 
      "Attributes":23, 
      "AuthorIndex":0, 
      "CreatedTime":"2013-04-17T19:33:17Z",
      "Id":"1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.4316bdaa94bf4984be5dfea1ba96954e.26.26.S-1-5-21-2127521184-1604012920-1887927527-66602",
      "LikerInfo":{
        "__metadata":{"type":"SP.Social.SocialPostActorInfo"},
        "IncludesCurrentUser":false, 
        "Indexes":{"results":[]},
        "TotalCount":0
      },
      "ModifiedTime":"2013-04-17T20:52:51Z",
      "Overlays":{"results":[]},
      "PostType":0, 
      "PreferredImageUri":null, 
      "Source":{
        "__metadata":{"type":"SP.Social.SocialLink"},
        "Text":null, 
        "Uri":null
      },
      "Text":"Posted with REST." 
    },
    "Status":5,
    "ThreadType":0,
    "TotalReplyCount":1
  }
}}
```


## <a name="example-rest-requests-for-feed-tasks"></a><span data-ttu-id="43a62-475">Пример запросов REST для задач, веб-канала активности</span><span class="sxs-lookup"><span data-stu-id="43a62-475">Example REST requests for feed tasks</span></span>
<span data-ttu-id="43a62-476"><a name="bk_exampleRequests"> </a></span><span class="sxs-lookup"><span data-stu-id="43a62-476"></span></span>

 <span data-ttu-id="43a62-p134">**GET** -запросов для веб-канала активности задачи укажите параметры в URI или в качестве атрибута **url** запроса. запросы на **POST** укажите параметры в атрибуте **data** текст запроса в формате XML или Нотация объектов JavaScript (JSON). Можно сделать HTTP-запросов на любом языке, включая JavaScript и C#. Следующие запросы на примере показано, как мог выполнять запросы с помощью JavaScript и порядок передачи данных сущностей в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="43a62-p134">**GET** requests for feed tasks specify parameters in the URI or in the **url** attribute of the request. **POST** requests specify parameters in the **data** attribute of the request body in XML or JavaScript Object Notation (JSON) format. You can make HTTP requests in any language, including JavaScript and C#. The following example requests show how to make requests by using JavaScript and how to pass entity information in JSON format.</span></span>
  
    
    
 <span data-ttu-id="43a62-481">**Пример:** Как задать параметр _ID_ в тексте запроса (в атрибуте **data** ).</span><span class="sxs-lookup"><span data-stu-id="43a62-481">**Example:** How to specify the _ID_ parameter in the request body (in the **data** attribute).</span></span>
  
> [!NOTE]
> <span data-ttu-id="43a62-p135">[!Примечание] Значения свойств **Id** потока и запись: слишком много времени для отправки в URL-адрес, поэтому должны отправлять их в тексте запроса. В результате даже только операции чтения, логически **GET** запросов необходимо отправить как **POST** запросы. Например для получения потока, необходимо отправить запрос **POST** и передайте поток **Id** как сущность в тексте запроса.</span><span class="sxs-lookup"><span data-stu-id="43a62-p135">The values of thread and post **Id** properties are too long to send in a URL, so you have to send them in the request body. As a result, even read-only operations that are logically **GET** requests must be sent as **POST** requests. For example, to get a thread, you have to send a **POST** request and pass the thread **Id** as an entity in the request body.</span></span>
  
    
    




```

var endpoint = siteUrl + '/_api/social.feed/post';
var postId = '1.655c70c348374d48839daabc24a360f0.82baa3bdfa2f481a8185802eb9c6c6cd.5d227a6fa3894f0c9dde26876b71d619.0c37852b34d0418e91c62ac25af4be5b.4316bdaa94bf4984be5dfea1ba96954e.26.26.S-1-5-21-2127521184-1604012920-1887927527-66602';

$.ajax({
    url: endpoint,
    type: 'POST',
    data: JSON.stringify({
        'ID': postId
    }),
    headers: {
        "accept": "application/json;odata=verbose",
        "content-type": "application/json;odata=verbose",
        "X-RequestDigest": $("#__REQUESTDIGEST").val()
    },
    success: function(data) { 
        var stringData = JSON.stringify(data);
        alert(stringData);

        // Converts the response data into an object that you can work with.
        var jsonObject = JSON.parse(stringData);
    },
    error: function(xhr, ajaxOptions, thrownError) {
        alert("Error: " + xhr.status + " " + thrownError + "\\nResponseText: " + xhr.responseText);
    }
});
```

 <span data-ttu-id="43a62-485">**Пример:** Как опубликовать запись корневой и указать параметр _restCreationData_ в атрибуте **data**.</span><span class="sxs-lookup"><span data-stu-id="43a62-485">**Example:** How to publish a root post and specify the _restCreationData_ parameter in the **data** attribute.</span></span>
  
    
    



```

var endpoint = <site url> + '/_api/social.feed/my/feed/post';
var postContent = 'Posted with REST.';

$.ajax({
    url: endpoint,
    type: 'POST',
    data: JSON.stringify({
        'restCreationData': {
            '__metadata': {
                'type': 'SP.Social.SocialRestPostCreationData'
            },
            'ID': null,
            'creationData': {
                '__metadata': {
                    'type': 'SP.Social.SocialPostCreationData'
                },
                'ContentText': postContent
            }
        }
    }),
    headers: {
        "accept": "application/json;odata=verbose",
        "content-type": "application/json;odata=verbose",
        "X-RequestDigest": $("#__REQUESTDIGEST").val()
    },
    success: function(data) { 
        var stringData = JSON.stringify(data);
        alert(stringData);

        // Converts the response data into an object that you can work with.
        var jsonObject = JSON.parse(stringData);
    },
    error: function(xhr, ajaxOptions, thrownError) {
        alert("Error: " + xhr.status + " " + thrownError + "\\nResponseText: " + xhr.responseText);
    }
});
```

<span data-ttu-id="43a62-486">Чтобы опубликовать ее в ответ для указанного потока, отправьте запрос **POST** ресурсов **Reply** ( `<site url>/_api/social.feed/Post/Reply`) и передайте **restCreationData** информации, которая включает в себя идентификатор конечного post</span><span class="sxs-lookup"><span data-stu-id="43a62-486">To publish a reply to a specified thread, send a **POST** request to the **Reply** resource ( `<site url>/_api/social.feed/Post/Reply`) and pass **restCreationData** information that includes the target post ID.</span></span>
  
    
    



```

{ 'restCreationData': {
    '__metadata': { 'type': 'SP.Social.SocialRestPostCreationData' },
    'ID':'1.4975bef1e1bc42608c1dfae9f320c751.35c9fd7b79904800aaa5f74684bf0f75.623664921f034e8d814c000267d3e5e4.0c37852b34d0418e91c62ac25af4be5b.230d3c5272fc499f88ac0b74b2f4512f.119.119.S-1-5-21-124525095-708259637-1543119021-565461',
    'creationData':{
        '__metadata':{ 'type':'SP.Social.SocialPostCreationData' },
        'ContentText':'This is a reply to the specified post.',
        'UpdateStatusText':false
    }
} }
```


## <a name="resources-used-in-feed-related-rest-requests-and-responses"></a><span data-ttu-id="43a62-487">Ресурсы, используемые в связанных с каналами REST запросы и ответы</span><span class="sxs-lookup"><span data-stu-id="43a62-487">Resources used in feed-related REST requests and responses</span></span>
<span data-ttu-id="43a62-488"><a name="bk_FeedRelatedRestResources"> </a></span><span class="sxs-lookup"><span data-stu-id="43a62-488"></span></span>

<span data-ttu-id="43a62-489">Следующие ресурсы REST возвращаются в ответы сервера и используются в качестве параметров в запросов на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="43a62-489">The following REST resources are used as parameters in client-side requests or are returned in server responses.</span></span>
  
    
    

### <a name="spsocialsocialfeedoptions"></a><span data-ttu-id="43a62-490">SP. Social.SocialFeedOptions</span><span class="sxs-lookup"><span data-stu-id="43a62-490">SP.Social.SocialFeedOptions</span></span>
<span data-ttu-id="43a62-491"><a name="bk_SocialFeedOptions"> </a></span><span class="sxs-lookup"><span data-stu-id="43a62-491"></span></span>

<span data-ttu-id="43a62-492">Представляет параметры, которые можно указать при получении веб-канал.</span><span class="sxs-lookup"><span data-stu-id="43a62-492">Represents options that you can specify when retrieving a feed.</span></span>
  
    
    
<span data-ttu-id="43a62-p136">Клиентские **GET** -запросов для веб-каналов при необходимости можно указать **SocialFeedOptions** свойства в качестве параметров. Эти свойства задаются в строке запроса.</span><span class="sxs-lookup"><span data-stu-id="43a62-p136">Client-side **GET** requests for feeds can optionally specify **SocialFeedOptions** properties as parameters. These properties are specified in the query string.</span></span>
  
    
    

|<span data-ttu-id="43a62-495">**Вариант**</span><span class="sxs-lookup"><span data-stu-id="43a62-495">**Option**</span></span>|<span data-ttu-id="43a62-496">**Тип**</span><span class="sxs-lookup"><span data-stu-id="43a62-496">**Type**</span></span>|<span data-ttu-id="43a62-497">**Описание**</span><span class="sxs-lookup"><span data-stu-id="43a62-497">**Description**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="43a62-498">MaxThreadCount</span><span class="sxs-lookup"><span data-stu-id="43a62-498">MaxThreadCount</span></span>|<span data-ttu-id="43a62-499">**Int32**</span><span class="sxs-lookup"><span data-stu-id="43a62-499">**Int32**</span></span>|<span data-ttu-id="43a62-p137">Максимальное число потоков для извлечения. Значение по умолчанию  20.</span><span class="sxs-lookup"><span data-stu-id="43a62-p137">The maximum number of threads to retrieve. The default number is 20.</span></span>|
|<span data-ttu-id="43a62-502">NewerThan</span><span class="sxs-lookup"><span data-stu-id="43a62-502">NewerThan</span></span>|<span data-ttu-id="43a62-503">**String**</span><span class="sxs-lookup"><span data-stu-id="43a62-503">**String**</span></span>|<span data-ttu-id="43a62-p138">«Новее» граница интервала времени, чтобы получить, как строковое представление объекта **DateTime**. Значение по умолчанию  без указанной границы.</span><span class="sxs-lookup"><span data-stu-id="43a62-p138">The "newer than" boundary of the time span to retrieve, as a string representation of a **DateTime** object. The default is no specified boundary.</span></span>|
|<span data-ttu-id="43a62-506">OlderThan</span><span class="sxs-lookup"><span data-stu-id="43a62-506">OlderThan</span></span>|<span data-ttu-id="43a62-507">**String**</span><span class="sxs-lookup"><span data-stu-id="43a62-507">**String**</span></span>|<span data-ttu-id="43a62-p139">«Старше» граница интервала времени, чтобы получить, как строковое представление объекта **DateTime**. Значение по умолчанию  без указанной границы.</span><span class="sxs-lookup"><span data-stu-id="43a62-p139">The "older than" boundary of the time span to retrieve, as a string representation of a **DateTime** object. The default is no specified boundary.</span></span>|
|<span data-ttu-id="43a62-510">SortOrder</span><span class="sxs-lookup"><span data-stu-id="43a62-510">SortOrder</span></span>|<span data-ttu-id="43a62-511">**Int32**</span><span class="sxs-lookup"><span data-stu-id="43a62-511">**Int32**</span></span>|<span data-ttu-id="43a62-512">Порядок сортировки потоков в веб-канал.</span><span class="sxs-lookup"><span data-stu-id="43a62-512">The sort order of the threads in the feed.</span></span> <span data-ttu-id="43a62-513">Порядок сортировки по умолчанию — по дате изменения, за исключением временной шкалы, канала, который отсортированы по дате создания.</span><span class="sxs-lookup"><span data-stu-id="43a62-513">The default sort order is by modified date, except for the timeline feed, which is sorted by created date.</span></span><br/>          <span data-ttu-id="43a62-514">**0** Сортировка потоков по время изменения в соответствии с самыми последними время изменения их публикации.</span><span class="sxs-lookup"><span data-stu-id="43a62-514">**0** sorts threads by modified time, according to the most recent modification times of their posts.</span></span><br/>          <span data-ttu-id="43a62-515">**1** Сортировка потоков по время создания определяется время создания их публикации в корневом.</span><span class="sxs-lookup"><span data-stu-id="43a62-515">**1** sorts threads by created time, according to the creation times of their root posts.</span></span>|
   

  
    
    

  
    
    

### <a name="spsocialsocialrestactor"></a><span data-ttu-id="43a62-516">SP. Social.SocialRestActor</span><span class="sxs-lookup"><span data-stu-id="43a62-516">SP.Social.SocialRestActor</span></span>
<span data-ttu-id="43a62-517"><a name="bk_SocialRestActor"> </a></span><span class="sxs-lookup"><span data-stu-id="43a62-517"></span></span>

<span data-ttu-id="43a62-518">Представляет пользователя, документов, сайта или тег.</span><span class="sxs-lookup"><span data-stu-id="43a62-518">Represents a user, document, site, or tag.</span></span>
  
    
    
<span data-ttu-id="43a62-519">Сервер возвращает **SocialRestActor** ресурсов в ответ на запрос со стороны клиента actor сведения.</span><span class="sxs-lookup"><span data-stu-id="43a62-519">The server returns a **SocialRestActor** resource in the response to a client-side request for actor information.</span></span>
  
    
    
 <span data-ttu-id="43a62-520">**SocialRestActor** имеет следующие свойства.</span><span class="sxs-lookup"><span data-stu-id="43a62-520">**SocialRestActor** has the following properties.</span></span>
  
    
    

|<span data-ttu-id="43a62-521">**Свойство**</span><span class="sxs-lookup"><span data-stu-id="43a62-521">**Property**</span></span>|<span data-ttu-id="43a62-522">**Тип**</span><span class="sxs-lookup"><span data-stu-id="43a62-522">**Type**</span></span>|<span data-ttu-id="43a62-523">**Описание**</span><span class="sxs-lookup"><span data-stu-id="43a62-523">**Description**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="43a62-524">FollowableItem</span><span class="sxs-lookup"><span data-stu-id="43a62-524">FollowableItem</span></span>|<span data-ttu-id="43a62-525">**String**</span><span class="sxs-lookup"><span data-stu-id="43a62-525">**String**</span></span>|<span data-ttu-id="43a62-p141">Уникальный идентификатор указанного субъекта. Возвращает имя учетной записи для пользователя или URI для документов, сайта или тег.</span><span class="sxs-lookup"><span data-stu-id="43a62-p141">The unique identifier of the specified actor. Returns the account name for a user or the URI for a document, site, or tag.</span></span>|
|<span data-ttu-id="43a62-528">FollowableItemActor</span><span class="sxs-lookup"><span data-stu-id="43a62-528">FollowableItemActor</span></span>| [<span data-ttu-id="43a62-529">SP. Social.SocialActor</span><span class="sxs-lookup"><span data-stu-id="43a62-529">SP.Social.SocialActor</span></span>](http://msdn.microsoft.com/library/4e369fd5-b9b0-9804-957e-b3e39c559cd4%28Office.15%29.aspx)|<span data-ttu-id="43a62-p142">Указанный пользователь. Возвращает **null**, если пользователь является текущим пользователем, или если ресурс не actor пользовательского типа.</span><span class="sxs-lookup"><span data-stu-id="43a62-p142">The specified user. Returns **null** if the user is the current user or if the resource is not a user-type actor.</span></span>|
|<span data-ttu-id="43a62-532">Me</span><span class="sxs-lookup"><span data-stu-id="43a62-532">Me</span></span>| [<span data-ttu-id="43a62-533">SP. Social.SocialActor</span><span class="sxs-lookup"><span data-stu-id="43a62-533">SP.Social.SocialActor</span></span>](http://msdn.microsoft.com/library/4e369fd5-b9b0-9804-957e-b3e39c559cd4%28Office.15%29.aspx)|<span data-ttu-id="43a62-534">Текущий пользователь.</span><span class="sxs-lookup"><span data-stu-id="43a62-534">The current user.</span></span>|
   

  
    
    

  
    
    

### <a name="spsocialsocialrestfeed"></a><span data-ttu-id="43a62-535">SP. Social.SocialRestFeed</span><span class="sxs-lookup"><span data-stu-id="43a62-535">SP.Social.SocialRestFeed</span></span>
<span data-ttu-id="43a62-536"><a name="bk_SocialRestFeed"> </a></span><span class="sxs-lookup"><span data-stu-id="43a62-536"></span></span>

<span data-ttu-id="43a62-537">Представляет социальные веб-канал.</span><span class="sxs-lookup"><span data-stu-id="43a62-537">Represents a social feed.</span></span>
  
    
    
<span data-ttu-id="43a62-538">Сервер возвращает **SocialRestFeed** ресурсов в ответ на запрос со стороны клиента веб-канала активности содержимое.</span><span class="sxs-lookup"><span data-stu-id="43a62-538">The server returns a **SocialRestFeed** resource in the response to a client-side request for feed content.</span></span>
  
    
    
 <span data-ttu-id="43a62-539">**SocialRestFeed** содержит оболочку [SP. Social.SocialFeed](http://msdn.microsoft.com/library/356c5475-2fd6-a655-c271-5d7f21af45e2%28Office.15%29.aspx) объект, который имеет следующие свойства.</span><span class="sxs-lookup"><span data-stu-id="43a62-539">**SocialRestFeed** contains a wrapped [SP.Social.SocialFeed](http://msdn.microsoft.com/library/356c5475-2fd6-a655-c271-5d7f21af45e2%28Office.15%29.aspx) object, which has the following properties.</span></span>
  
    
    

|<span data-ttu-id="43a62-540">**Свойство**</span><span class="sxs-lookup"><span data-stu-id="43a62-540">**Property**</span></span>|<span data-ttu-id="43a62-541">**Тип**</span><span class="sxs-lookup"><span data-stu-id="43a62-541">**Type**</span></span>|<span data-ttu-id="43a62-542">**Описание**</span><span class="sxs-lookup"><span data-stu-id="43a62-542">**Description**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="43a62-543">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="43a62-543">Attributes</span></span>| [<span data-ttu-id="43a62-544">SP. Social.SocialFeedAttributes</span><span class="sxs-lookup"><span data-stu-id="43a62-544">SP.Social.SocialFeedAttributes</span></span>](http://msdn.microsoft.com/library/9ea7d3c5-7f96-88a6-5bdf-d7749b044ad3%28Office.15%29.aspx)|<span data-ttu-id="43a62-545">Побитовое набор атрибутов, которые применяются к веб-канал.</span><span class="sxs-lookup"><span data-stu-id="43a62-545">A bitwise set of attributes that apply to the feed.</span></span>|
|<span data-ttu-id="43a62-546">NewestProcessed</span><span class="sxs-lookup"><span data-stu-id="43a62-546">NewestProcessed</span></span>|<span data-ttu-id="43a62-547">**DateTime**</span><span class="sxs-lookup"><span data-stu-id="43a62-547">**DateTime**</span></span>|<span data-ttu-id="43a62-548">Дата и время последней получить post.</span><span class="sxs-lookup"><span data-stu-id="43a62-548">The date and time of the newest retrieved post.</span></span>|
|<span data-ttu-id="43a62-549">OldestProcessed</span><span class="sxs-lookup"><span data-stu-id="43a62-549">OldestProcessed</span></span>|<span data-ttu-id="43a62-550">**DateTime**</span><span class="sxs-lookup"><span data-stu-id="43a62-550">**DateTime**</span></span>|<span data-ttu-id="43a62-551">Дата и время наиболее старых получить post.</span><span class="sxs-lookup"><span data-stu-id="43a62-551">The date and time of the oldest retrieved post.</span></span>|
|<span data-ttu-id="43a62-552">Потоки</span><span class="sxs-lookup"><span data-stu-id="43a62-552">Threads</span></span>| <span data-ttu-id="43a62-553">[SP. Social.SocialThread](http://msdn.microsoft.com/library/46aa4beb-d708-f20e-471e-626c8a7efab7%28Office.15%29.aspx)]</span><span class="sxs-lookup"><span data-stu-id="43a62-553">[SP.Social.SocialThread](http://msdn.microsoft.com/library/46aa4beb-d708-f20e-471e-626c8a7efab7%28Office.15%29.aspx)[]</span></span>|<span data-ttu-id="43a62-554">Потоки, которые составляют веб-канал.</span><span class="sxs-lookup"><span data-stu-id="43a62-554">The threads that make up the feed.</span></span>|
|<span data-ttu-id="43a62-555">UnreadMentionCount</span><span class="sxs-lookup"><span data-stu-id="43a62-555">UnreadMentionCount</span></span>|<span data-ttu-id="43a62-556">**Int32**</span><span class="sxs-lookup"><span data-stu-id="43a62-556">**Int32**</span></span>|<span data-ttu-id="43a62-557">Счетчик непрочитанных упоминания для текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="43a62-557">The count of unread mentions for the current user.</span></span>|
   

  
    
    

  
    
    

### <a name="spsocialsocialrestpostcreationdata"></a><span data-ttu-id="43a62-558">SP. Social.SocialRestPostCreationData</span><span class="sxs-lookup"><span data-stu-id="43a62-558">SP.Social.SocialRestPostCreationData</span></span>
<span data-ttu-id="43a62-559"><a name="bk_SocialRestPostCreationData"> </a></span><span class="sxs-lookup"><span data-stu-id="43a62-559"></span></span>

<span data-ttu-id="43a62-560">Представляет сведения о новых post контента и связанных с ними.</span><span class="sxs-lookup"><span data-stu-id="43a62-560">Represents content and related information for a new post.</span></span>
  
    
    
<span data-ttu-id="43a62-p143">Клиенты указывают **SocialRestPostCreationData** свойства в качестве параметров в запросе для публикации корневой записью или ее в ответ. Эти свойства задаются в атрибуте **data** текст запроса.</span><span class="sxs-lookup"><span data-stu-id="43a62-p143">Clients specify **SocialRestPostCreationData** properties as parameters in a request to publish a root post or a reply. These properties are specified in the **data** attribute of the request body.</span></span>
  
    
    
 <span data-ttu-id="43a62-p144">**SocialRestPostCreationData** содержит свойство **ID** и оболочку [SP. Social.SocialPostCreationData](http://msdn.microsoft.com/library/f0e1fa3e-6fc9-48e0-5570-92091abfef33%28Office.15%29.aspx) объекта. **ID** является обязательным, но **SocialPostCreationData** свойства являются необязательными.</span><span class="sxs-lookup"><span data-stu-id="43a62-p144">**SocialRestPostCreationData** contains an **ID** property and a wrapped [SP.Social.SocialPostCreationData](http://msdn.microsoft.com/library/f0e1fa3e-6fc9-48e0-5570-92091abfef33%28Office.15%29.aspx) object. **ID** is required but the **SocialPostCreationData** properties are optional.</span></span>
  
    
    

|<span data-ttu-id="43a62-565">**Свойство**</span><span class="sxs-lookup"><span data-stu-id="43a62-565">**Property**</span></span>|<span data-ttu-id="43a62-566">**Тип**</span><span class="sxs-lookup"><span data-stu-id="43a62-566">**Type**</span></span>|<span data-ttu-id="43a62-567">**Описание**</span><span class="sxs-lookup"><span data-stu-id="43a62-567">**Description**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="43a62-568">Идентификатор (обязательный)</span><span class="sxs-lookup"><span data-stu-id="43a62-568">ID (required)</span></span>|<span data-ttu-id="43a62-569">**null** или **String**</span><span class="sxs-lookup"><span data-stu-id="43a62-569">**null** or **String**</span></span>|<span data-ttu-id="43a62-570">Назначение post.</span><span class="sxs-lookup"><span data-stu-id="43a62-570">The target destination for the post.</span></span> <span data-ttu-id="43a62-571">Возможны следующие значения:</span><span class="sxs-lookup"><span data-stu-id="43a62-571">The value can be one of the following:</span></span><br/>           <span data-ttu-id="43a62-572">**значение null,** публикация корневого post для текущего пользователя в веб-канала</span><span class="sxs-lookup"><span data-stu-id="43a62-572">**null** to publish a root post to the current user's feed</span></span><br/>           <span data-ttu-id="43a62-573">Идентификатор записи отвечать на</span><span class="sxs-lookup"><span data-stu-id="43a62-573">The ID of a post to reply to</span></span><br/>           <span data-ttu-id="43a62-574">URL-адрес сайта веб-канала публикации (например: `http://<teamSiteURL>/newsfeed.aspx`)</span><span class="sxs-lookup"><span data-stu-id="43a62-574">The URL of a site feed to post to (for example: `http://<teamSiteURL>/newsfeed.aspx`)</span></span>|
   
<span data-ttu-id="43a62-575">Объект **SocialPostCreationData** относятся следующие свойства.</span><span class="sxs-lookup"><span data-stu-id="43a62-575">The following properties belong to the **SocialPostCreationData** object.</span></span>
  
    
    

|<span data-ttu-id="43a62-576">**Свойство**</span><span class="sxs-lookup"><span data-stu-id="43a62-576">**Property**</span></span>|<span data-ttu-id="43a62-577">**Тип**</span><span class="sxs-lookup"><span data-stu-id="43a62-577">**Type**</span></span>|<span data-ttu-id="43a62-578">**Описание**</span><span class="sxs-lookup"><span data-stu-id="43a62-578">**Description**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="43a62-579">Attachment</span><span class="sxs-lookup"><span data-stu-id="43a62-579">Attachment</span></span>| [<span data-ttu-id="43a62-580">SP. Social.SocialAttachment</span><span class="sxs-lookup"><span data-stu-id="43a62-580">SP.Social.SocialAttachment</span></span>](http://msdn.microsoft.com/library/dfdee790-a1b0-19c8-0e92-5a6e058ba4db%28Office.15%29.aspx)|<span data-ttu-id="43a62-581">Изображение, видео или вложение документов для post.</span><span class="sxs-lookup"><span data-stu-id="43a62-581">An image, video, or document attachment for the post.</span></span>|
|<span data-ttu-id="43a62-582">ContentItems</span><span class="sxs-lookup"><span data-stu-id="43a62-582">ContentItems</span></span>| <span data-ttu-id="43a62-583">[SP. Social.SocialDataItem](http://msdn.microsoft.com/library/757e7b62-66a6-b03f-0ff0-769a42eb2b4a%28Office.15%29.aspx)]</span><span class="sxs-lookup"><span data-stu-id="43a62-583">[SP.Social.SocialDataItem](http://msdn.microsoft.com/library/757e7b62-66a6-b03f-0ff0-769a42eb2b4a%28Office.15%29.aspx)[]</span></span>|<span data-ttu-id="43a62-584">Элементы для замены соответствующие маркеры в контента текста post</span><span class="sxs-lookup"><span data-stu-id="43a62-584">The items to replace the corresponding tokens in the post's content text</span></span>|
|<span data-ttu-id="43a62-585">ContentText</span><span class="sxs-lookup"><span data-stu-id="43a62-585">ContentText</span></span>|<span data-ttu-id="43a62-586">**String**</span><span class="sxs-lookup"><span data-stu-id="43a62-586">**String**</span></span>|<span data-ttu-id="43a62-587">Обычный текст post, которые могут включать маркеры позиционные вставки (например, "сегодня  {0} день рождения!").</span><span class="sxs-lookup"><span data-stu-id="43a62-587">The plain text of the post, which can include positional insertion tokens (for example, "Today is {0}'s birthday!").</span></span>|
|<span data-ttu-id="43a62-588">SecurityUris</span><span class="sxs-lookup"><span data-stu-id="43a62-588">SecurityUris</span></span>|<span data-ttu-id="43a62-589">**String[]**</span><span class="sxs-lookup"><span data-stu-id="43a62-589">**String[]**</span></span>|<span data-ttu-id="43a62-590">Строковое представление коды URI для объектов SharePoint, которые определяют права доступа для записи.</span><span class="sxs-lookup"><span data-stu-id="43a62-590">String representations of the URIs to SharePoint objects that define access permissions for the post.</span></span>|
|<span data-ttu-id="43a62-591">Источник</span><span class="sxs-lookup"><span data-stu-id="43a62-591">Source</span></span>| [<span data-ttu-id="43a62-592">SP. Social.SocialLink</span><span class="sxs-lookup"><span data-stu-id="43a62-592">SP.Social.SocialLink</span></span>](http://msdn.microsoft.com/library/c71efc66-c9ca-ea35-b1c0-cb9ec3bbfcd3%28Office.15%29.aspx)|<span data-ttu-id="43a62-593">Источник post.</span><span class="sxs-lookup"><span data-stu-id="43a62-593">The source of the post.</span></span>|
|<span data-ttu-id="43a62-594">UpdateStatusText</span><span class="sxs-lookup"><span data-stu-id="43a62-594">UpdateStatusText</span></span>|<span data-ttu-id="43a62-595">**Boolean**</span><span class="sxs-lookup"><span data-stu-id="43a62-595">**Boolean**</span></span>|<span data-ttu-id="43a62-596">Значение, определяющее, будет ли содержимое обычного текста post необходимо заменить текст состояния текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="43a62-596">A value that controls whether the post's plain-text content should replace the current user's status text.</span></span>|
   

  
    
    

  
    
    

### <a name="spsocialsocialrestthread"></a><span data-ttu-id="43a62-597">SP. Social.SocialRestThread</span><span class="sxs-lookup"><span data-stu-id="43a62-597">SP.Social.SocialRestThread</span></span>
<span data-ttu-id="43a62-598"><a name="bk_SocialRestThread"> </a></span><span class="sxs-lookup"><span data-stu-id="43a62-598"></span></span>

<span data-ttu-id="43a62-599">Представляет поток, который содержит корневой post и набор ответов.</span><span class="sxs-lookup"><span data-stu-id="43a62-599">Represents a thread that contains a root post and a set of replies.</span></span>
  
    
    
<span data-ttu-id="43a62-600">Сервер возвращает **SocialRestThread** ресурсов в ответ на запрос со стороны клиента для создания post или Получение полного потока.</span><span class="sxs-lookup"><span data-stu-id="43a62-600">The server returns a **SocialRestThread** resource in the response to a client-side request to create a post or to get a full thread.</span></span>
  
    
    
 <span data-ttu-id="43a62-601">**SocialRestThread** содержит свойство **ID** и оболочку [SP. Social.SocialThread](http://msdn.microsoft.com/library/46aa4beb-d708-f20e-471e-626c8a7efab7%28Office.15%29.aspx) объекта.</span><span class="sxs-lookup"><span data-stu-id="43a62-601">**SocialRestThread** contains an **ID** property and a wrapped [SP.Social.SocialThread](http://msdn.microsoft.com/library/46aa4beb-d708-f20e-471e-626c8a7efab7%28Office.15%29.aspx) object.</span></span>
  
    
    

|<span data-ttu-id="43a62-602">**Свойство**</span><span class="sxs-lookup"><span data-stu-id="43a62-602">**Property**</span></span>|<span data-ttu-id="43a62-603">**Тип**</span><span class="sxs-lookup"><span data-stu-id="43a62-603">**Type**</span></span>|<span data-ttu-id="43a62-604">**Описание**</span><span class="sxs-lookup"><span data-stu-id="43a62-604">**Description**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="43a62-605">ID</span><span class="sxs-lookup"><span data-stu-id="43a62-605">ID</span></span>|<span data-ttu-id="43a62-606">**String**</span><span class="sxs-lookup"><span data-stu-id="43a62-606">**String**</span></span>|<span data-ttu-id="43a62-607">Уникальный идентификатор потока.</span><span class="sxs-lookup"><span data-stu-id="43a62-607">The unique identifier of the thread.</span></span>|
   
<span data-ttu-id="43a62-608">Объект **SocialThread** относятся следующие свойства.</span><span class="sxs-lookup"><span data-stu-id="43a62-608">The following properties belong to the **SocialThread** object.</span></span>
  
    
    

|<span data-ttu-id="43a62-609">**Свойство**</span><span class="sxs-lookup"><span data-stu-id="43a62-609">**Property**</span></span>|<span data-ttu-id="43a62-610">**Тип**</span><span class="sxs-lookup"><span data-stu-id="43a62-610">**Type**</span></span>|<span data-ttu-id="43a62-611">**Описание**</span><span class="sxs-lookup"><span data-stu-id="43a62-611">**Description**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="43a62-612">Субъекты</span><span class="sxs-lookup"><span data-stu-id="43a62-612">Actors</span></span>| <span data-ttu-id="43a62-613">[SP. Social.SocialActor](http://msdn.microsoft.com/library/4e369fd5-b9b0-9804-957e-b3e39c559cd4%28Office.15%29.aspx)]</span><span class="sxs-lookup"><span data-stu-id="43a62-613">[SP.Social.SocialActor](http://msdn.microsoft.com/library/4e369fd5-b9b0-9804-957e-b3e39c559cd4%28Office.15%29.aspx)[]</span></span>|<span data-ttu-id="43a62-614">Объединенные массива все вовлеченные субъекты.</span><span class="sxs-lookup"><span data-stu-id="43a62-614">The merged array of participating actors.</span></span>|
|<span data-ttu-id="43a62-615">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="43a62-615">Attributes</span></span>|<span data-ttu-id="43a62-616">**Int32**</span><span class="sxs-lookup"><span data-stu-id="43a62-616">**Int32**</span></span>|<span data-ttu-id="43a62-p146">Побитовое значение, которое представляет набор атрибутов для потока. Просмотреть  [SP. Social.SocialThreadAttributes](http://msdn.microsoft.com/library/21ff9f92-3223-bcc7-ceec-7b899ee29b6e%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="43a62-p146">The bitwise value that represents the set of attributes for the thread. See  [SP.Social.SocialThreadAttributes](http://msdn.microsoft.com/library/21ff9f92-3223-bcc7-ceec-7b899ee29b6e%28Office.15%29.aspx).</span></span>|
|<span data-ttu-id="43a62-619">Id</span><span class="sxs-lookup"><span data-stu-id="43a62-619">Id</span></span>|<span data-ttu-id="43a62-620">**String**</span><span class="sxs-lookup"><span data-stu-id="43a62-620">**String**</span></span>|<span data-ttu-id="43a62-621">Уникальный идентификатор потока.</span><span class="sxs-lookup"><span data-stu-id="43a62-621">The unique identifier of the thread.</span></span>|
|<span data-ttu-id="43a62-622">OwnerIndex</span><span class="sxs-lookup"><span data-stu-id="43a62-622">OwnerIndex</span></span>|<span data-ttu-id="43a62-623">**Int32**</span><span class="sxs-lookup"><span data-stu-id="43a62-623">**Int32**</span></span>|<span data-ttu-id="43a62-624">Индекс владелец потока в рамках субъекты потока.</span><span class="sxs-lookup"><span data-stu-id="43a62-624">The index of the thread's owner within the thread's actors.</span></span>|
|<span data-ttu-id="43a62-625">Постоянная ссылка</span><span class="sxs-lookup"><span data-stu-id="43a62-625">Permalink</span></span>|<span data-ttu-id="43a62-626">**String**</span><span class="sxs-lookup"><span data-stu-id="43a62-626">**String**</span></span>|<span data-ttu-id="43a62-627">Строковое представление стабильным URI для перемещения по непосредственно к потоку, если он доступен.</span><span class="sxs-lookup"><span data-stu-id="43a62-627">The string representation of the stable URI for navigating directly to the thread, if one is available.</span></span>|
|<span data-ttu-id="43a62-628">PostReference</span><span class="sxs-lookup"><span data-stu-id="43a62-628">PostReference</span></span>| [<span data-ttu-id="43a62-629">SP. Social.SocialPostReference</span><span class="sxs-lookup"><span data-stu-id="43a62-629">SP.Social.SocialPostReference</span></span>](http://msdn.microsoft.com/library/529e1db7-2e9a-5141-6b1e-94a5c63e7c16%28Office.15%29.aspx)|<span data-ttu-id="43a62-630">Публикация, в который указывает ссылка.</span><span class="sxs-lookup"><span data-stu-id="43a62-630">The referenced post.</span></span>|
|<span data-ttu-id="43a62-631">Ответы</span><span class="sxs-lookup"><span data-stu-id="43a62-631">Replies</span></span>| <span data-ttu-id="43a62-632">[SP. Social.SocialPost](http://msdn.microsoft.com/library/a761ce71-d3d7-420a-1e06-962674124dfa%28Office.15%29.aspx)]</span><span class="sxs-lookup"><span data-stu-id="43a62-632">[SP.Social.SocialPost](http://msdn.microsoft.com/library/a761ce71-d3d7-420a-1e06-962674124dfa%28Office.15%29.aspx)[]</span></span>|<span data-ttu-id="43a62-633">Ответы, которые потока.</span><span class="sxs-lookup"><span data-stu-id="43a62-633">The replies to the thread.</span></span>|
|<span data-ttu-id="43a62-634">RootPost</span><span class="sxs-lookup"><span data-stu-id="43a62-634">RootPost</span></span>| [<span data-ttu-id="43a62-635">SP. Social.SocialPost</span><span class="sxs-lookup"><span data-stu-id="43a62-635">SP.Social.SocialPost</span></span>](http://msdn.microsoft.com/library/a761ce71-d3d7-420a-1e06-962674124dfa%28Office.15%29.aspx)|<span data-ttu-id="43a62-636">Публикация корневого потока.</span><span class="sxs-lookup"><span data-stu-id="43a62-636">The root post of the thread.</span></span>|
|<span data-ttu-id="43a62-637">Status</span><span class="sxs-lookup"><span data-stu-id="43a62-637">Status</span></span>|<span data-ttu-id="43a62-638">**Int32**</span><span class="sxs-lookup"><span data-stu-id="43a62-638">**Int32**</span></span>|<span data-ttu-id="43a62-p147">Код, определяющий устранимых ошибок, возникших во время извлечения потока. Просмотреть  [SP. Social.SocialStatusCode](http://msdn.microsoft.com/library/79292329-19de-43e1-5928-60b0edc36c94%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="43a62-p147">The code that identifies recoverable errors that occurred during thread retrieval. See  [SP.Social.SocialStatusCode](http://msdn.microsoft.com/library/79292329-19de-43e1-5928-60b0edc36c94%28Office.15%29.aspx).</span></span>|
|<span data-ttu-id="43a62-641">ThreadType</span><span class="sxs-lookup"><span data-stu-id="43a62-641">ThreadType</span></span>| [<span data-ttu-id="43a62-642">SP. Social.SocialThreadType</span><span class="sxs-lookup"><span data-stu-id="43a62-642">SP.Social.SocialThreadType</span></span>](http://msdn.microsoft.com/library/7444217e-ddda-d3a0-b19f-146cf8c6fcaa%28Office.15%29.aspx)|<span data-ttu-id="43a62-643">Тип потока.</span><span class="sxs-lookup"><span data-stu-id="43a62-643">The thread type.</span></span>|
|<span data-ttu-id="43a62-644">TotalReplyCount</span><span class="sxs-lookup"><span data-stu-id="43a62-644">TotalReplyCount</span></span>|<span data-ttu-id="43a62-645">**Int32**</span><span class="sxs-lookup"><span data-stu-id="43a62-645">**Int32**</span></span>|<span data-ttu-id="43a62-646">Счетчик общее число ответов для потока.</span><span class="sxs-lookup"><span data-stu-id="43a62-646">The count of the total number of replies for the thread.</span></span>|
   

## <a name="see-also"></a><span data-ttu-id="43a62-647">См. также</span><span class="sxs-lookup"><span data-stu-id="43a62-647">See also</span></span>
<span data-ttu-id="43a62-648"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="43a62-648"></span></span>


-  [<span data-ttu-id="43a62-649">Начало разработки с использованием социальных функций в SharePoint</span><span class="sxs-lookup"><span data-stu-id="43a62-649">Get started developing with social features in SharePoint</span></span>](get-started-developing-with-social-features-in-sharepoint.md)
    
  
-  [<span data-ttu-id="43a62-650">Как: сведения для чтения и записи социальных канал с помощью службы REST в SharePoint</span><span class="sxs-lookup"><span data-stu-id="43a62-650">How to: Learn to read and write to the social feed by using the REST service in SharePoint</span></span>](how-to-learn-to-read-and-write-to-the-social-feed-by-using-the-rest-service-in-s.md)
    
  
-  [<span data-ttu-id="43a62-651">Работа с социальными веб-каналами в SharePoint</span><span class="sxs-lookup"><span data-stu-id="43a62-651">Work with social feeds in SharePoint</span></span>](work-with-social-feeds-in-sharepoint.md)
    
  
-  [<span data-ttu-id="43a62-652">Following people and content REST API reference for SharePoint</span><span class="sxs-lookup"><span data-stu-id="43a62-652">Following people and content REST API reference for SharePoint</span></span>](following-people-and-content-rest-api-reference-for-sharepoint.md)
    
  
- <span data-ttu-id="43a62-653">Чтобы просмотреть список членов **SP. Социальные** OData схемы, используемой службой SharePoint REST, перейдите к `http://<siteUri>/_api/$metadata`.</span><span class="sxs-lookup"><span data-stu-id="43a62-653">To see the members in the **SP.Social** OData schema used by the SharePoint REST service, browse to `http://<siteUri>/_api/$metadata`.</span></span>
    
  
