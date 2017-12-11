---
title: "Подписки на людей и контент Справочник по интерфейсу API службы REST для SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: c05755df-846d-4a39-941d-950d066cc6d4
ms.openlocfilehash: 4e2cbe5819a0e5d2e5c58a1675503d5e899d6805
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="following-people-and-content-rest-api-reference-for-sharepoint"></a>Подписки на людей и контент Справочник по интерфейсу API службы REST для SharePoint
Поиск конечных точек SharePoint REST для подписки на людей и контент с помощью **SocialRestFollowingManager** ресурсов и ресурсов **PeopleManager** .
Чтобы выполнить те же задачи, которые можно выполнить при использовании клиентской объектной модели .NET и объектной модели JavaScript, можно использовать службу SharePoint представлений состояния (REST). Для использования службы REST, построение и отправлять запросы **POST** и HTTP **GET** конечных точек ресурсов, которые представляют задачи, которые необходимо выполнить. Эти конечные точки ресурсов соответствуют объектов SharePoint, свойств и методов.
  
    
    

URI конечной точки для большинства следующие задачи начинается с ресурсом **SocialRestFollowingManager** ( `social.following`) и заканчивается ресурсов, используемая для выполнения определенной задачи. Например необходимо использовать URI  `http://www.contoso.com/_api/social.following/follow` текущего пользователя запустите следующие людей или содержимого и URI `https://www.contoso.com/sites/devSite/_api/social.following/followed` люди или контента  это следующий текущего пользователя.

> [!NOTE]
> В этой статье показаны конечной точке URI и параметр компоненты HTTP-запросов. В разделе примеры запросов на полный [как: с помощью службы REST в SharePoint, выполните документы, сайты и тегов](how-to-follow-documents-sites-and-tags-by-using-the-rest-service-in-sharepoint-2.md). 
  
    
    

Мы рекомендуем использовать **SocialRestFollowingManager** API для следующих пользователей и контента следующие задачи, что вы можете использовать **PeopleManager** ресурсов для некоторых следующие сотрудники обзор задач, **SocialRestFollowingManager** не поддерживает. К примеру можно узнать ли кто-то после текущего пользователя или получить последователи другому пользователю. Для выполнения этих задач отправлять **GET** HTTP-запросов к конечной точке URI, которые начинаются с ресурсом **PeopleManager** ( `sp.userprofiles.peoplemanager`) и заканчиваются ресурсов, используемая для выполнения определенной задачи.Если конечная точка с параметром, метаданные параметров отправляется в URI или в тексте запроса в формате XML или Нотация объектов JavaScript (JSON). Можно сделать HTTP-запросов на любом языке, включая JavaScript и C#. По умолчанию службы REST возвращает ответы, отформатированные с помощью протокола Atom, но можно запросить формат JSON с помощью **Accept** заголовки HTTP. В разделе [Программирование с использованием службы SharePoint 2013 REST](http://msdn.microsoft.com/library/d4b5c277-ed50-420c-8a9b-860342284b72%28Office.15%29.aspx).
## <a name="resource-endpoints-for-following-people-and-following-content-tasks"></a>Конечные точки ресурсов для задач, следующие сотрудники и следующие контента
<a name="bk_Overview"> </a>


[Follow](#bk_Follow)  
[StopFollowing](#bk_StopFollowing)  
[IsFollowed](#bk_IsFollowed)  
[Мои](#bk_My)  
[Мои/FollowedDocumentsUri](#bk_MyFollowedDocumentsUri)  
[Мои/FollowedSitesUri](#bk_MyFollowedSitesUri)  
[Мои/за](#bk_Followed)  
[Мои/FollowedCount](#bk_FollowedCount)  
[Мои / последователи](#bk_Followers)  
[Мои / предложений](#bk_Suggestions)  
[GetMySuggestions](#bk_GetMySuggestions)  
[IsMyPeopleListPublic](#bk_IsMyPeopleListPublic)  
[AmIFollowedBy](#bk_AmIFollowedBy)  
[GetPeopleFollowedBy](#bk_GetPeopleFollowedBy)  
[GetFollowersFor](#bk_GetFollowersFor)  
   

## <a name="follow"></a>Подписка
<a name="bk_Follow"> </a>

Делает создайте пользователя, документов, сайта или тег текущего пользователя.
  
    
    

### <a name="endpoint-uri-structure"></a>Структура URI конечной точки

 **POST** `http://<siteCollection>/<site>/_api/social.following/follow`
  
    
    

### <a name="request-parameter"></a>Параметр запроса

 _actor_
  
    
    
тип: **SP.Social.SocialActorInfo**
  
    
    
actor для запуска подписки.
  
    
    
 **Пользователь  _actor_ в URI**
  
    
    



```

http://<siteCollection>/<site>/_api/social.following/follow(ActorType=0,AccountName=@v,Id=null)?@v='domain\\user'
```

 **Пользователь  _actor_ в теле запроса**
  
    
    



```
"actor":{
  "__metadata":{"type":"SP.Social.SocialActorInfo"},
  "ActorType":0,
  "AccountName":"domain\\user",
  "Id":null
}
```

Если вы используете модели удостоверений на основе утверждений, вы можете передать имя учетной записи с помощью формата  `@v='i:0"%23".f|membership|user@domain.com'` в строке запроса или `"i:0#.f|membership|user@domain.com"` в тексте запроса.
  
    
    
 **Документ  _actor_ в URI**
  
    
    



```

http://<siteCollection>/<site>/_api/social.following/follow(ActorType=1,ContentUri=@v,Id=null)?@v='http://server/Shared%20Documents/fileName.docx'
```

 **Документ  _actor_ в теле запроса**
  
    
    



```
"actor":{
  "__metadata":{"type":"SP.Social.SocialActorInfo"},
  "ActorType":1,
  "ContentUri":"http://server/Shared%20Documents/fileName.docx",
  "Id":null
}
```

 **Сайт  _actor_ в URI**
  
    
    



```

http://<siteCollection>/<site>/_api/social.following/follow(ActorType=2,ContentUri=@v,Id=null)?@v='http://server/site'
```

 **Сайт  _actor_ в теле запроса**
  
    
    



```
"actor":{
  "__metadata":{"type":"SP.Social.SocialActorInfo"},
  "ActorType":2,
  "ContentUri":"http://siteCollection/site",
  "Id":null
}
```

 **Тег  _actor_ в URI**
  
    
    



```

http://<siteCollection>/<site>/_api/social.following/follow(ActorType=3,TagGuid='19a4a484-c1dc-4bc5-8c93-bb96245ce928',Id=null)
```

 **Тег  _actor_ в теле запроса**
  
    
    



```
"actor":{
  "__metadata":{"type":"SP.Social.SocialActorInfo"},
  "ActorType":3,
  "TagGuid":"19a4a484-c1dc-4bc5-8c93-bb96245ce928",
  "Id":null
}
```

Требуется тег идентификатор GUID для запуска отслеживание тега. Не удается получить GUID с помощью службы REST, но вы можете использовать клиентской объектной модели .NET или JavaScript объектной модели. Узнайте,  [как получить идентификатор GUID тега на основе имени тега с помощью объектной модели JavaScript](follow-content-in-sharepoint.md#bk_getTagGuid).
  
    
    

### <a name="response"></a>Ответ

 **Follow**
  
    
    
тип: **SP.Social.SocialFollowResult**
  
    
    
состояние запроса: 0 = ОК. 1 = AlreadyFollowing; 2 = LimitReached; или 3 = InternalError.
  
    
    
Приведенный ниже ответ указывает, что запрос завершился успешно.
  
    
    



```

{"d":{"Follow":0}}
```


## <a name="stopfollowing"></a>StopFollowing
<a name="bk_StopFollowing"> </a>

Делает остановите следующие пользователей, документов, сайта или тег текущего пользователя.
  
    
    

### <a name="endpoint-uri-structure"></a>Структура URI конечной точки

 **POST** `http://<siteCollection>/<site>/_api/social.following/stopfollowing`
  
    
    

### <a name="request-parameter"></a>Параметр запроса

 _actor_
  
    
    
тип: **SP.Social.SocialActorInfo**
  
    
    
actor, чтобы отменить подписку.
  
    
    
 **Пользователь  _actor_ в URI**
  
    
    



```
http://<siteCollection>/<site>/_api/social.following/stopfollowing(ActorType=0,AccountName=@v,Id=null)?@v='domain\\user'
```

 **Пользователь  _actor_ в теле запроса**
  
    
    



```
"actor":{
  "__metadata":{"type":"SP.Social.SocialActorInfo"},
  "ActorType":0,
  "AccountName":"domain\\user",
  "Id":null
}
```

Если вы используете модели удостоверений на основе утверждений, вы можете передать имя учетной записи с помощью формата  `@v='i:0"%23".f|membership|user@domain.com'` в строке запроса или `"i:0#.f|membership|user@domain.com"` в тексте запроса.
  
    
    
 **Документ  _actor_ в URI**
  
    
    



```

http://<siteCollection>/<site>/_api/social.following/stopfollowing(ActorType=1,ContentUri=@v,Id=null)?@v='http://server/Shared%20Documents/fileName.docx'
```

 **Документ  _actor_ в теле запроса**
  
    
    



```
"actor":{
  "__metadata":{"type":"SP.Social.SocialActorInfo"},
  "ActorType":1,
  "ContentUri":"http://server/Shared%20Documents/fileName.docx",
  "Id":null
}
```

 **Сайт  _actor_ в URI**
  
    
    



```

http://<siteCollection>/<site>/_api/social.following/stopfollowing(ActorType=2,ContentUri=@v,Id=null)?@v='http://server/site'
```

 **Сайт  _actor_ в теле запроса**
  
    
    



```
"actor":{
  "__metadata":{"type":"SP.Social.SocialActorInfo"},
  "ActorType":2,
  "ContentUri":"http://siteCollection/site",
  "Id":null
}
```

 **Тег  _actor_ в URI**
  
    
    



```

http://<siteCollection>/<site>/_api/social.following/stopfollowing(ActorType=3,TagGuid='19a4a484-c1dc-4bc5-8c93-bb96245ce928',Id=null)
```

 **Тег  _actor_ в теле запроса**
  
    
    



```
"actor":{
  "__metadata":{"type":"SP.Social.SocialActorInfo"},
  "ActorType":3,
  "TagGuid":"19a4a484-c1dc-4bc5-8c93-bb96245ce928",
  "Id":null
}
```

Требуется тег идентификатор GUID для запуска отслеживание тега. Не удается получить GUID с помощью службы REST, но вы можете использовать клиентской объектной модели .NET или JavaScript объектной модели. Узнайте,  [как получить идентификатор GUID тега на основе имени тега с помощью объектной модели JavaScript](follow-content-in-sharepoint.md#bk_getTagGuid).
  
    
    

### <a name="response"></a>Ответ

Нет.
  
    
    

```

{"d":{"StopFollowing":null}}
```


## <a name="isfollowed"></a>IsFollowed
<a name="bk_IsFollowed"> </a>

Указывает, является ли текущий пользователь следующие указанного пользователя, документов, сайта или тег.
  
    
    

### <a name="endpoint-uri-structure"></a>Структура URI конечной точки

 **POST** `http://<siteCollection>/<site>/_api/social.following/isfollowed`
  
    
    

### <a name="request-parameter"></a>Параметр запроса

 _actor_
  
    
    
тип: **SP.Social.SocialActorInfo**
  
    
    
actor, чтобы найти сведения о следующих состоянии.
  
    
    
 **Пользователь  _actor_ в URI**
  
    
    



```
http://<siteCollection>/<site>/_api/social.following/isfollowed(ActorType=0,AccountName=@v,Id=null)?@v='domain\\user'
```

 **Пользователь  _actor_ в теле запроса**
  
    
    



```
"actor":{
  "__metadata":{"type":"SP.Social.SocialActorInfo"},
  "ActorType":0,
  "AccountName":"domain\\user",
  "Id":null
}
```

Если вы используете модели удостоверений на основе утверждений, вы можете передать имя учетной записи с помощью формата  `@v='i:0"%23".f|membership|user@domain.com'` в строке запроса или `"i:0#.f|membership|user@domain.com"` в тексте запроса.
  
    
    
 **Документ  _actor_ в URI**
  
    
    



```

http://<siteCollection>/<site>/_api/social.following/isfollowed(ActorType=1,ContentUri=@v,Id=null)?@v='https://domain.sharepoint.com/Shared%20Documents/fileName.docx'
```

 **Документ  _actor_ в теле запроса**
  
    
    



```
"actor":{
  "__metadata":{"type":"SP.Social.SocialActorInfo"},
  "ActorType":1,
  "ContentUri":"http://server/Shared%20Documents/fileName.docx",
  "Id":null
}
```

 **Сайт  _actor_ в URI**
  
    
    



```

http://<siteCollection>/<site>/_api/social.following/isfollowed(ActorType=2,ContentUri=@v,Id=null)?@v='http://domain.sharepoint.com'
```

 **Сайт  _actor_ в теле запроса**
  
    
    



```
"actor":{
  "__metadata":{"type":"SP.Social.SocialActorInfo"},
  "ActorType":2,
  "ContentUri":"http://siteCollection/site",
  "Id":null
}
```

 **Тег  _actor_ в URI**
  
    
    



```

http://<siteCollection>/<site>/_api/social.following/isfollowed(ActorType=3,TagGuid='19a4a484-c1dc-4bc5-8c93-bb96245ce928',Id=null)
```

 **Тег  _actor_ в теле запроса**
  
    
    



```
"actor":{
  "__metadata":{"type":"SP.Social.SocialActorInfo"},
  "ActorType":3,
  "TagGuid":"19a4a484-c1dc-4bc5-8c93-bb96245ce928",
  "Id":null
}
```

Требуется тег идентификатор GUID для запуска отслеживание тега. Не удается получить GUID с помощью службы REST, но вы можете использовать клиентской объектной модели .NET или JavaScript объектной модели. Узнайте,  [как получить идентификатор GUID тега на основе имени тега с помощью объектной модели JavaScript](follow-content-in-sharepoint.md#bk_getTagGuid).
  
    
    

### <a name="response"></a>Ответ

 **IsFollowed**
  
    
    
тип: **bool**
  
    
    
 **true**, если текущий пользователь  это пример результата; в противном случае  **false**.
  
    
    
Приведенный ниже ответ указывает, что пользователь не подписан указанного субъекта.
  
    
    



```

{"d":{"IsFollowed":false}}
```


## <a name="my"></a>Мои
<a name="bk_My"> </a>

Получает сведения о **SocialRestFollowingManager** экземпляра и сведения о текущем пользователе.
  
    
    

### <a name="endpoint-uri-structure"></a>Структура URI конечной точки

 **GET** `http://<siteCollection>/<site>/_api/social.following/my`
  
    
    

### <a name="request-parameter"></a>Параметр запроса

Нет.
  
    
    

### <a name="response"></a>Ответ

Тип: **SP.Social.SocialRestFollowingManager**
  
    
    
сведения об экземпляре **SocialRestFollowingManager** и **MyFollowedDocumentsUri**, **MyFollowedSitesUri**и **SocialActor** свойства для текущего пользователя.
  
    
    
Приведенный ниже ответ представляет экземпляр **SocialRestFollowingManager** для текущего пользователя.
  
    
    



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


## <a name="myfolloweddocumentsuri"></a>Мои/FollowedDocumentsUri
<a name="bk_MyFollowedDocumentsUri"> </a>

Возвращает URI на страницу **у меня есть подписка: документы** для текущего пользователя.
  
    
    

### <a name="endpoint-uri-structure"></a>Структура URI конечной точки

 **GET** `http://<siteCollection>/<site>/_api/social.following/my/followeddocumentsuri`
  
    
    

### <a name="request-parameter"></a>Параметр запроса

Нет.
  
    
    

### <a name="response"></a>Ответ

 **FollowedDocumentsUri**
  
    
    
тип: **String**
  
    
    
URI на страницу **у меня есть подписка: документы** для текущего пользователя.
  
    
    
Приведенный ниже ответ представляет **FollowedDocumentsUri** для текущего пользователя.
  
    
    



```

{"d":{"FollowedDocumentsUri":"https://somecompany-my.sharepoint.com/personal/someone_somecompany_onmicrosoft_com/Social/FollowedContent.aspx"}}
```


## <a name="myfollowedsitesuri"></a>Мои/FollowedSitesUri
<a name="bk_MyFollowedSitesUri"> </a>

Возвращает URI для страницы **сайты, у меня есть подписка** для текущего пользователя.
  
    
    

### <a name="endpoint-uri-structure"></a>Структура URI конечной точки

 **GET** `http://<siteCollection>/<site>/_api/social.following/my/followedsitesuri`
  
    
    

### <a name="request-parameter"></a>Параметр запроса

Нет.
  
    
    

### <a name="response"></a>Ответ

 **FollowedSitesUri**
  
    
    
тип: **String**
  
    
    
URI для страницы **сайты, у меня есть подписка** для текущего пользователя.
  
    
    
Приведенный ниже ответ представляет **FollowedSitesUri** для текущего пользователя.
  
    
    



```
{"d":{"FollowedSitesUri":"https://somecompany-my.sharepoint.com/personal/someone_somecompany_onmicrosoft_com/Social/Sites.aspx"}}
```


## <a name="myfollowed"></a>Мои/за
<a name="bk_Followed"> </a>

Получает пользователей, документы, сайты и теги, выполнив текущего пользователя.
  
    
    

### <a name="endpoint-uri-structure"></a>Структура URI конечной точки

 **GET** `http://<siteCollection>/<site>/_api/social.following/my/followed(types=15)`
  
    
    

### <a name="request-parameter"></a>Параметр запроса

 _types_
  
    
    
тип: **Int32**
  
    
    
типы субъектов для включения. Пользователи = 1, документы = 2, сайты = 4, теги = 8. Побитовое комбинации разрешено.
  
    
    

### <a name="response"></a>Ответ

 **Followed**
  
    
    
тип: массив **SP.Social.SocialActor**
  
    
    
пользователей, документы, сайты и теги, выполнив текущего пользователя.
  
    
    
Приведенный ниже ответ представляет документ, сайта и тега. Параметр  _types_ в запросе Указывает типы субъектов для включения.
  
    
    



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


## <a name="myfollowedcount"></a>Мои/FollowedCount
<a name="bk_FollowedCount"> </a>

Получает количество пользователей, документы, сайты и теги, выполнив текущего пользователя.
  
    
    

### <a name="endpoint-uri-structure"></a>Структура URI конечной точки

 **GET** `http://<siteCollection>/<site>/_api/social.following/my/followedcount(types=15)`
  
    
    

### <a name="request-parameter"></a>Параметр запроса

 _types_
  
    
    
тип: **Int32**
  
    
    
типы субъектов для включения. Пользователи = 1, документы = 2, сайты = 4, теги = 8. Побитовое комбинации разрешено.
  
    
    

### <a name="response"></a>Ответ

 **FollowedCount**
  
    
    
тип: **Int32**
  
    
    
число пользователей, документы, сайты и теги, выполнив текущего пользователя.
  
    
    
Приведенный ниже ответ указывает, что текущий пользователь является следующие 3 субъекты указанного типа. Параметр  _types_ в запросе Указывает типы субъектов для включения.
  
    
    



```

{"d":{"FollowedCount":3}}
```


## <a name="myfollowers"></a>Мои / последователи
<a name="bk_Followers"> </a>

Получает пользователей, которые отслеживаются текущего пользователя.
  
    
    

### <a name="endpoint-uri-structure"></a>Структура URI конечной точки

 **GET** `http://<siteCollection>/<site>/_api/social.following/my/followers`
  
    
    

### <a name="request-parameter"></a>Параметр запроса

Нет.
  
    
    

### <a name="response"></a>Ответ

 **Followers**
  
    
    
тип: массив **SP.Social.SocialActor**
  
    
    

  
    
    
Приведенный ниже ответ представляет одного пользователя, выполнив текущего пользователя.
  
    
    



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


## <a name="mysuggestions"></a>Мои / предложений
<a name="bk_Suggestions"> </a>

Получает пользователей, которые текущий пользователь может потребоваться выполнить.
  
> [!NOTE]
> [!Примечание] Рекомендации людей функциональные возможности, зависит от следующих действий пользователей, обходы при поиске и аналитика поиска. Увидеть  [Как работают предложения людей на SharePoint Online](follow-people-in-sharepoint.md#bk_PeopleSuggestions). 
  
    
    


### <a name="endpoint-uri-structure"></a>Структура URI конечной точки

 **GET** `http://<siteCollection>/<site>/_api/social.following/my/suggestions`
  
    
    

### <a name="request-parameter"></a>Параметр запроса

Нет.
  
    
    

### <a name="response"></a>Ответ

 **Suggestions**
  
    
    
тип: массив **SP.Social.SocialActor**
  
    
    
пользователей, которые текущий пользователь может потребоваться выполнить.
  
    
    

## <a name="getmysuggestions"></a>GetMySuggestions
<a name="bk_GetMySuggestions"> </a>

Получает пользователей, которые текущий пользователь может потребоваться выполнить.
  
> [!NOTE]
> [!Примечание] Рекомендации людей функциональные возможности, зависит от следующих действий пользователей, обходы при поиске и аналитика поиска. Увидеть  [Как работают предложения людей на SharePoint Online](follow-people-in-sharepoint.md#bk_PeopleSuggestions). 
  
    
    


### <a name="endpoint-uri-structure"></a>Структура URI конечной точки

 **GET** `http://<siteCollection>/<site>/_api/sp.userprofiles.peoplemanager/getmysuggestions`
  
    
    

### <a name="request-parameter"></a>Параметр запроса

Нет.
  
    
    

### <a name="response"></a>Ответ

 **Suggestions**
  
    
    
тип: список **SP.UserProfiles.PersonProperties**
  
    
    
пользователей, которые текущий пользователь может потребоваться выполнить.
  
    
    

## <a name="ismypeoplelistpublic"></a>IsMyPeopleListPublic
<a name="bk_IsMyPeopleListPublic"> </a>

Находит ли список **людей, у меня есть подписка** для текущего пользователя, открытый в работе.
  
    
    

### <a name="endpoint-uri-structure"></a>Структура URI конечной точки

 **GET** `http://<siteCollection>/<site>/_api/sp.userprofiles.peoplemanager/ismypeoplelistpublic`
  
    
    

### <a name="request-parameter"></a>Параметр запроса

Нет.
  
    
    

### <a name="response"></a>Ответ

 **IsMyPeopleListPublic**
  
    
    
тип: **bool**
  
    
    
 **true** Если список людей текущий пользователь является открытым; в противном случае  **false**.
  
    
    
Приведенный ниже ответ указывает, что общедоступные список людей текущего пользователя.
  
    
    



```

{"d":{"IsMyPeopleListPublic":true}}
```


## <a name="amifollowedby"></a>AmIFollowedBy
<a name="bk_AmIFollowedBy"> </a>

Поиск в работе ли указанный пользователь после текущего пользователя.
  
    
    

### <a name="endpoint-uri-structure"></a>Структура URI конечной точки

 **GET** `http://<siteCollection>/<site>/_api/sp.userprofiles.peoplemanager/amifollowedby(accountName=@v)?@v='domain\\user'`
  
    
    
 **GET** `http://<siteCollection>/<site>/_api/sp.userprofiles.peoplemanager/amifollowedby(accountName=@v)?@v='i:0"%23".f|membership|user@domain.com'`
  
    
    

### <a name="request-parameter"></a>Параметр запроса

 _Имя учетной записи_
  
    
    
тип: **String**
  
    
    
имя учетной записи конечного пользователя.
  
    
    

### <a name="response"></a>Ответ

 **AmIFollowedBy**
  
    
    
тип: **bool**
  
    
    
 **true**, если указанный пользователь  это пример текущего пользователя; в противном случае  **false**.
  
    
    
Приведенный ниже ответ указывает, что указанный пользователь не подписан текущего пользователя.
  
    
    



```
{"d":{"AmIFollowedBy":false}}
```


## <a name="getpeoplefollowedby"></a>GetPeopleFollowedBy
<a name="bk_GetPeopleFollowedBy"> </a>

Получает пользователей, а затем указанного пользователя.
  
    
    

### <a name="endpoint-uri-structure"></a>Структура URI конечной точки

 **GET** `http://<siteCollection>/<site>/_api/sp.userprofiles.peoplemanager/getpeoplefollowedby(accountName=@v)?@v='domain\\user'`
  
    
    
 **GET** `http://<siteCollection>/<site>/_api/sp.userprofiles.peoplemanager/getpeoplefollowedby(accountName=@v)?@v='i:0"%23".f|membership|user@domain.com'`
  
    
    

### <a name="request-parameter"></a>Параметр запроса

 _Имя учетной записи_
  
    
    
тип: **String**
  
    
    
имя учетной записи конечного пользователя.
  
    
    

### <a name="response"></a>Ответ

 **GetPeopleFollowedBy**
  
    
    
тип: список **SP.UserProfiles.PersonProperties**
  
    
    
пользователей, а затем указанного пользователя.
  
    
    
Приведенный ниже ответ представляет два пользователя, а затем указанного пользователя.
  
    
    



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


## <a name="getfollowersfor"></a>GetFollowersFor
<a name="bk_GetFollowersFor"> </a>

Получает пользователей, которые отслеживаются указанного пользователя.
  
    
    

### <a name="endpoint-uri-structure"></a>Структура URI конечной точки

 **GET** `http://<siteCollection>/<site>/_api/sp.userprofiles.peoplemanager/getfollowersfor(accountName=@v)?@v='domain\\user'`
  
    
    
 **GET** `http://<siteCollection>/<site>/_api/sp.userprofiles.peoplemanager/getfollowersfor(accountName=@v)?@v='i:0"%23".f|membership|user@domain.com'`
  
    
    

### <a name="request-parameter"></a>Параметр запроса

 _Имя учетной записи_
  
    
    
тип: **String**
  
    
    
имя учетной записи конечного пользователя.
  
    
    

### <a name="response"></a>Ответ

 **GetFollowersFor**
  
    
    
тип: список **SP.UserProfiles.PersonProperties**
  
    
    
пользователей, которые отслеживаются указанного пользователя.
  
    
    
Приведенный ниже ответ  пользователь, которому после указанного пользователя.
  
    
    



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


## <a name="see-also"></a>См. также
<a name="bk_addresources"> </a>


-  [Как подписываться на документы, сайты и теги, используя службу REST в SharePoint](how-to-follow-documents-sites-and-tags-by-using-the-rest-service-in-sharepoint-2.md)
    
  
-  [Social feed REST API reference for SharePoint](social-feed-rest-api-reference-for-sharepoint.md)
    
  
-  [SharePoint User Profiles JavaScript Reference (sp.userprofiles.js)](http://msdn.microsoft.com/library/80cf5436-6aa2-6f11-a782-66a04f6e2fb0%28Office.15%29.aspx)
    
  
-  [Начало разработки с использованием социальных функций в SharePoint](get-started-developing-with-social-features-in-sharepoint.md)
    
  
