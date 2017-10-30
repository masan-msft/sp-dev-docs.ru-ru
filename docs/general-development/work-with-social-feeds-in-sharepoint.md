---
title: "Работа с социальными веб-каналами в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 39f2163e-15cc-43bc-b131-041d5afdcd90
ms.openlocfilehash: 20e31de9a616bdc48746ff7bba6949d404c7d02d
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="work-with-social-feeds-in-sharepoint"></a>Работа с социальными веб-каналами в SharePoint
Сведения о распространенных задач программирования по работе с социальными веб-каналов и микроблога публикации в SharePoint.
## <a name="apis-for-working-with-social-feeds-in-sharepoint"></a>API-интерфейсы для работы с социальными веб-каналами в SharePoint
<a name="bkmk_APIversions"> </a>

В локальной фермы SharePoint интерактивных социальными веб-каналами предназначены для обеспечения их для обмена информацией и оставайтесь на связи с людьми и контент. Многие из функций веб-канала активности можно просмотреть на странице **канала новостей** личного сайта пользователя. Веб-каналы содержат коллекции потоков, которые представляют микроблога публикации, бесед, обновления состояния и других уведомлений.
  
    
    
SharePoint предоставляет следующие интерфейсы API, которые можно использовать для программной работы с социальными веб-каналами.
  
    
    

- Клиентские объектные модели для управляемого кода:
    
  - клиентская объектная модель .NET;
    
  
  - клиентская объектная модель Silverlight;
    
  
  - мобильная клиентская объектная модель.
    
  
- Объектная модель JavaScript.
    
  
- Служба передачи репрезентативного состояния (REST).
    
  
- Серверная объектная модель
    
  
Рекомендуется при разработке для SharePoint при вы можете Используйте клиентские API-интерфейсы. API-интерфейсов клиента включают клиентской объектной модели, объектной модели JavaScript и службы REST. Дополнительные сведения об интерфейсах API в SharePoint и их использовании см. раздел [Выбор право API в SharePoint](choose-the-right-api-set-in-sharepoint.md).
  
    
    
Each API includes a manager object that you use to perform core feed-related tasks. Table 1 shows the manager and other key objects (or REST resources) in the APIs and the class library (or endpoint URI) where you can find them.
  
    
    

> **Примечание:** Silverlight и мобильных устройств клиентской объектной модели не указан явно в таблице 1 или в таблице 2, так как они обеспечивают основные функциональные возможности, аналогичные клиентской объектной модели .NET и использовать же цифровые подписи. Клиентская объектная модель Silverlight определяется в Microsoft.SharePoint.Client.UserProfiles.Silverlight.dll и мобильных устройств клиентской объектной модели определяется в Microsoft.SharePoint.Client.UserProfiles.Phone.dll. 
  
    
    


**В таблице 1. API-интерфейсов SharePoint используется для работы с социальными веб-каналами программными средствами**

|**API**|**Основные объекты**|
|:-----|:-----|
|Клиентская объектная модель .NET  <br/> См.: [как: Создание и удаление сообщений и извлечение социальных веб-канал с помощью клиентской объектной модели .NET в SharePoint](how-to-create-and-delete-posts-and-retrieve-the-social-feed-by-using-the-net-cli.md)|Manager object:            [SocialFeedManager](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.aspx) <br/> Primary namespace:            [Microsoft.SharePoint.Client.Social](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.aspx) <br/> Other key objects:            [SocialFeed](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeed.aspx) , [SocialThread](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThread.aspx) , [SocialPost](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPost.aspx) , [SocialPostCreationData](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.aspx) , [SocialFeedOptions](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedOptions.aspx) , [SocialActor](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialActor.aspx) <br/> Библиотека классов:           Microsoft.SharePoint.Client.UserProfiles.dll|
|Объектная модель JavaScript  <br/> Просмотреть [как: Создание и удаление сообщений и извлечение социальных веб-канал с помощью объектной модели JavaScript в SharePoint](how-to-create-and-delete-posts-and-retrieve-the-social-feed-by-using-the-javascr.md)|Manager object:            [SocialFeedManager](http://msdn.microsoft.com/library/651fdf0f-841d-88f9-1e07-fcb3ad8c9410%28Office.15%29.aspx) <br/> Primary namespace:            [SP.Social](http://msdn.microsoft.com/library/43d47f01-c085-0e77-bd01-48bcb7d5bb35%28Office.15%29.aspx) <br/> Other key objects:            [SocialFeed](http://msdn.microsoft.com/library/356c5475-2fd6-a655-c271-5d7f21af45e2%28Office.15%29.aspx),  [SocialThread](http://msdn.microsoft.com/library/46aa4beb-d708-f20e-471e-626c8a7efab7%28Office.15%29.aspx),  [SocialPost](http://msdn.microsoft.com/library/a761ce71-d3d7-420a-1e06-962674124dfa%28Office.15%29.aspx),  [SocialPostCreationData](http://msdn.microsoft.com/library/f0e1fa3e-6fc9-48e0-5570-92091abfef33%28Office.15%29.aspx),  [SocialFeedOptions](http://msdn.microsoft.com/library/65caf283-6e7a-50dc-ef8e-a4e12bd237ac%28Office.15%29.aspx),  [SocialActor](http://msdn.microsoft.com/library/4e369fd5-b9b0-9804-957e-b3e39c559cd4%28Office.15%29.aspx) <br/> Библиотека классов:           SP.UserProfiles.js|
|Служба REST  <br/> Просмотреть [как: сведения для чтения и записи социальных канал с помощью службы REST в SharePoint](how-to-learn-to-read-and-write-to-the-social-feed-by-using-the-rest-service-in-s.md)|Manager resource:            [social.feed](social-feed-rest-api-reference-for-sharepoint.md) (SocialRestFeedManager) <br/> Primary namespace (OData):           **SP.Social** <br/> Other key resources:           SocialFeed,  [SocialRestFeed](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestFeed), SocialThread,  [SocialRestThread](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestThread), SocialPost, SocialPostCreationData,  [SocialRestPostCreationData](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestPostCreationData),  [SocialFeedOptions](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialFeedOptions), SocialActor,  [SociaRestActor](social-feed-rest-api-reference-for-sharepoint.md#bk_SocialRestActor) <br/> Access point:            `<siteUri>/_api/social.feed`|
|Серверная объектная модель <br/>Примечание: Код, который использует серверной объектной модели для доступа к данным веб-канала активности и запускает удаленно необходимо использовать объект [SPServiceContextScope](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPServiceContextScope.aspx) .|Manager object:            [SPSocialFeedManager](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFeedManager.aspx) <br/> Primary namespace:            [Microsoft.Office.Server.Social](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.aspx) <br/> Other key objects:            [SPSocialFeed](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFeed.aspx) , [SPSocialThread](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialThread.aspx) , [SPSocialPost](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialPost.aspx) , [SPSocialFeedOptions](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFeedOptions.aspx) , [SPSocialActor](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialActor.aspx) <br/> Библиотека классов:           Microsoft.Office.Server.UserProfiles.dll|
   
If you're using the server object model to access feed content and your code isn't running in a SharePoint instance (in other words, if your extension is not installed in the LAYOUTS folder on the application server), use an  [SPServiceContextScope](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPServiceContextScope.aspx) object in your code. The following code example shows one way to incorporate the [SPServiceContextScope](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPServiceContextScope.aspx) object into your code.
  
    
    



```cs

using (SPSite site = new SPSite(<siteURL>))
{
    using (new Microsoft.SharePoint.SPServiceContextScope(SPServiceContext.GetContext(site)))
    {
        // code
    }
}

```


## <a name="common-programming-tasks-for-working-with-social-feeds-in-sharepoint"></a>Типичные задачи программирования по работе с социальными веб-каналами в SharePoint
<a name="bkmk_CommonTasks"> </a>

Table 2 shows common programming tasks for working with social feeds and the members that you use to perform them. Members are from the .NET client object model (CSOM), JavaScript object model (JSOM), REST service, and server object model (SSOM).
  
    
    

**В таблице 2. API-Интерфейс для распространенных задач программирования по работе с социальными веб-каналами в SharePoint**


|**Задача**|**Участники**|
|:-----|:-----|
|Create an instance of the manager object in the context of the current user|CSOM:  [SocialFeedManager](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.aspx) <br/> JSOM:  [SocialFeedManager](http://msdn.microsoft.com/library/f7cf172f-970b-6b71-9eb4-b9a8bb7a0001%28Office.15%29.aspx) <br/> **Получение** REST:[`<siteUri>/_api/social.feed`](social-feed-rest-api-reference-for-sharepoint.md) <br/> SSOM:  [SPSocialFeedManager](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFeedManager.aspx)|
|Create an instance of the manager object in the context of a particular user|CSOM: не реализовано  <br/> JSOM: не реализовано  <br/> REST: не реализовано  <br/> SSOM:  [SPSocialFeedManager](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFeedManager.aspx)|
|Get the user for the current context|CSOM:  [Owner](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.Owner.aspx) <br/> JSOM:  [owner](http://msdn.microsoft.com/library/0307264e-d733-77f0-edae-f5468e58d0b7%28Office.15%29.aspx) <br/> **Получение** REST:[`<siteUri>/_api/social.feed/my`](social-feed-rest-api-reference-for-sharepoint.md#bk_my) <br/> SSOM:  [Owner](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFeedManager.Owner.aspx)|
|Get the feed for the current user  <br/> (specify the feed type)|CSOM:  [GetFeed](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.GetFeed.aspx) <br/> JSOM:  [getFeed](http://msdn.microsoft.com/library/cddaccd8-28da-6798-d8cb-4e9351efddf3%28Office.15%29.aspx) <br/> REST: **Получение** [`<siteUri>/_api/social.feed/my/Feed`](social-feed-rest-api-reference-for-sharepoint.md#bk_myFeed) (личные feed.md), [`<siteUri>/_api/social.feed/my/News`](social-feed-rest-api-reference-for-sharepoint.md#bk_myNews), [`<siteUri>/_api/social.feed/my/TimelineFeed`](social-feed-rest-api-reference-for-sharepoint.md#bk_myTimelineFeed), или[`<siteUri>/_api/social.feed/my/Likes`](social-feed-rest-api-reference-for-sharepoint.md#bk_myLikes) <br/> SSOM:  [GetFeed](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFeedManager.GetFeed.aspx)|
|Get the personal feed for a particular user|CSOM:  [GetFeedFor](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.GetFeedFor.aspx) <br/> JSOM:  [getFeedFor](http://msdn.microsoft.com/library/074ed255-9393-448d-1f7e-720fdeb05f48%28Office.15%29.aspx) <br/> **Получение** REST:[`<siteUri>/_api/social.feed/actor(item='domain\\user')/Feed`](social-feed-rest-api-reference-for-sharepoint.md#bk_actorFeed) <br/> SSOM:  [GetFeedFor](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFeedManager.GetFeedFor.aspx)|
|Get the site feed for a team site  <br/> (specify the URL of the site feed as the actor (example: http://<siteCollection>/<teamSite>/newsfeed.aspx))|CSOM:  [GetFeedFor](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.GetFeedFor.aspx) <br/> JSOM:  [getFeedFor](http://msdn.microsoft.com/library/074ed255-9393-448d-1f7e-720fdeb05f48%28Office.15%29.aspx) <br/> **Получение** REST:[`<siteUri>/_api/social.feed/actor(item=@v)/Feed?@v='http://<siteCollection>/<teamSite>/newsfeed.aspx'`](social-feed-rest-api-reference-for-sharepoint.md#bk_actorFeed) <br/> SSOM:  [GetFeedFor](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFeedManager.GetFeedFor.aspx)|
|Publish a root post to the current user's feed  <br/> (specify **null** for the target)|CSOM:  [CreatePost](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.CreatePost.aspx) <br/> JSOM:  [createPost](http://msdn.microsoft.com/library/e9ad06a1-831d-8ed0-c76e-8b049f14216f%28Office.15%29.aspx) <br/> REST: **POST** [`<siteUri>/_api/social.feed/my/Feed/Post`](social-feed-rest-api-reference-for-sharepoint.md#bk_myFeedPost) и передайте параметр _restCreationData_ в тексте запроса <br/> SSOM:  [CreatePost](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFeedManager.CreatePost.aspx)|
|Publish a post to a site feed  <br/> (specify the URL of the site feed as the target (example: http://<siteCollection>/teamSite>/newsfeed.aspx))|CSOM:  [CreatePost](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.CreatePost.aspx) <br/> JSOM:  [createPost](http://msdn.microsoft.com/library/e9ad06a1-831d-8ed0-c76e-8b049f14216f%28Office.15%29.aspx) <br/> REST: **POST** [`<siteUri>/_api/social.feed/actor(item=@av)/feed/post/?@av='<teamSiteUri>/newsfeed.aspx'`](social-feed-rest-api-reference-for-sharepoint.md#bk_actorFeedPost) и передайте параметр _restCreationData_ в тексте запроса (указать **значение null** для параметра _ID_ ) <br/> SSOM:  [CreatePost](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFeedManager.CreatePost.aspx)|
|Publish a reply to a post  <br/> (specify the ID of the target thread)|CSOM:  [CreatePost](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.CreatePost.aspx) <br/> JSOM:  [createPost](http://msdn.microsoft.com/library/e9ad06a1-831d-8ed0-c76e-8b049f14216f%28Office.15%29.aspx) <br/> REST: **POST** [`<siteUri>/_api/social.feed/Post/Reply`](social-feed-rest-api-reference-for-sharepoint.md#bk_postReply) и передайте параметр _restCreationData_ в тексте запроса <br/> SSOM:  [CreatePost](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFeedManager.CreatePost.aspx)|
|Delete a post, reply, or thread in the current user's feed (deleting a root post deletes the whole thread)|CSOM:  [DeletePost](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.DeletePost.aspx) <br/> JSOM:  [deletePost](http://msdn.microsoft.com/library/06e03f87-c97d-8634-a02b-f7812eb7beeb%28Office.15%29.aspx) <br/> REST: **POST** [`<siteUri>/_api/social.feed/Post/Delete`](social-feed-rest-api-reference-for-sharepoint.md#bk_postDelete) и передайте параметр _ID_ в теле запроса <br/> SSOM:  [DeletePost](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFeedManager.DeletePost.aspx)|
|Get a thread (a root post and all its replies) from the user's feed|CSOM:  [GetFullThread](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.GetFullThread.aspx) <br/> JSOM:  [getFullThread](http://msdn.microsoft.com/library/6bb384f3-9474-581f-e18d-e8c4f44c3cdf%28Office.15%29.aspx) <br/> REST: **POST** [`<siteUri>/_api/social.feed/Post`](social-feed-rest-api-reference-for-sharepoint.md#bk_post) и передайте параметр _ID_ в теле запроса <br/> SSOM:  [GetFullThread](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFeedManager.GetFullThread.aspx)|
|Have the user like (unlike) a post or reply|CSOM:  [LikePost](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.LikePost.aspx) ( [UnlikePost](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.UnlikePost.aspx) ) <br/> JSOM:  [likePost](http://msdn.microsoft.com/library/f401a584-1712-50af-ee08-2999a16388d6%28Office.15%29.aspx) ( [unlikePost](http://msdn.microsoft.com/library/c778bd7d-91e5-15dc-eeb8-b571957e8338%28Office.15%29.aspx))  <br/> REST: **POST** [`<siteUri>/_api/social.feed/Post/Like`](social-feed-rest-api-reference-for-sharepoint.md#bk_postLike) ( [`<siteUri>/_api/social.feed/Post/Unlike`](social-feed-rest-api-reference-for-sharepoint.md#bk_postUnlike)) и передайте параметр _ID_ в теле запроса <br/> SSOM:  [LikePost](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFeedManager.LikePost.aspx) ( [UnlikePost](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFeedManager.UnlikePost.aspx) )|
|Get all likers for a post|CSOM:  [GetAllLikers](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.GetAllLikers.aspx) <br/> JSOM:  [getAllLikers](http://msdn.microsoft.com/library/76286fdc-002f-2b13-dc26-53097eb2e3a2%28Office.15%29.aspx) <br/> REST: **POST** [`<siteUri>/_api/social.feed/Post/Likers`](social-feed-rest-api-reference-for-sharepoint.md#bk_postLikers) и передайте параметр _ID_ в теле запроса <br/> SSOM:  [GetAllLikers](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFeedManager.GetAllLikers.aspx)|
|Get the posts that mention a user|CSOM:  [GetMentions](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.GetMentions.aspx) <br/> JSOM:  [getMentions](http://msdn.microsoft.com/library/78f064c3-5b96-373e-e7f0-8603aedc5ded%28Office.15%29.aspx) <br/> **Получение** REST:[`<siteUri>/_api/social.feed/my/MentionFeed`](social-feed-rest-api-reference-for-sharepoint.md#bk_myMentionFeed) <br/> SSOM:  [GetMentions](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFeedManager.GetMentions.aspx)|
|Get the number of unread mentions for the current user|CSOM:  [GetUnreadMentionCount](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.GetUnreadMentionCount.aspx) <br/> JSOM:  [getUnreadMentionCount](http://msdn.microsoft.com/library/18dde16a-f78f-f65e-0644-4eb737b1ae00%28Office.15%29.aspx) <br/> **Получение** REST:[`<siteUri>/_api/social.feed/my/UnreadMentionCount`](social-feed-rest-api-reference-for-sharepoint.md#bk_myUnreadMentionCount) <br/> SSOM:  [GetUnreadMentionCount](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFeedManager.GetUnreadMentionCount.aspx)|
|Lock (unlock) a thread in the current user's feed|CSOM:  [LockThread](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.LockThread.aspx) ( [UnlockThread](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.UnlockThread.aspx) ) <br/> JSOM:  [lockThread](http://msdn.microsoft.com/library/cc696bb7-e7fd-7a57-5db5-736c3733589e%28Office.15%29.aspx) ( [unlockThread](http://msdn.microsoft.com/library/ee9288d6-ace0-1ec2-ea7c-0ee300b6e1ea%28Office.15%29.aspx))  <br/> REST: **POST** [`<siteUri>/_api/social.feed/Post/Lock`](social-feed-rest-api-reference-for-sharepoint.md#bk_postLock) ( [`<siteUri>/_api/social.feed/Post/Unlock`](social-feed-rest-api-reference-for-sharepoint.md#bk_postUnlock)) и передайте параметр _ID_ в теле запроса <br/> SSOM: [LockThread](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFeedManager.LockThread.aspx) (публикацию повторно [UnlockThread](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFeedManager.UnlockThread.aspx) )|
   

> **Примечание:** _Домена\\пользователя_ значение заполнителя в примере REST должно быть заменено имя учетной записи реального пользователя. Как передать параметр REST в тексте запроса, см в [примерах](social-feed-rest-api-reference-for-sharepoint.md#bk_exampleRequests) социальные веб-канала активности Справочник по API-Интерфейс REST.
  
    
    

SharePoint не поддерживает API для настройки макета или отображения публикации микроблога напрямую. Только SharePoint предоставляет данные и позволяет кроссплатформенный и между устройствами клиентским приложениям для определения макетов, подходящие для своих потребностей и форм-факторов. При разработке для SharePoint можно использовать переопределений JavaScript в обработки на стороне клиента, как описано в разделе [Настройка представления списка в SharePoint надстройки с использованием обработки на стороне клиента](http://msdn.microsoft.com/library/8d5cabb2-70d0-46a0-bfe0-9e21f8d67d86%28Office.15%29.aspx).
  
    
    

## <a name="overview-of-feed-types-in-the-my-site-social-api"></a>Overview of feed types in the Личный сайт API
<a name="bkmk_FeedTypes"> </a>

Feed types represent slices of feed data. When you retrieve a feed for the current user, you can specify one of the following feed types:
  
    
    

- **Personal** contains the posts and updates that are generated from a user. On Личный сайт, this feed is shown on a user's **About me** page.
    
  
- **News** contains the posts and updates that are generated from the current user and from the people and the content that the user is following. When you retrieve the **News** feed type, use the **ByModifiedTime** sort order option to get the most recent (cached) activities from the people who the user is following. On Личный сайт, this feed is shown on a user's **Newsfeed** page.
    
  
- **Timeline** contains the posts and updates that are generated from the current user and from the people and the content that the user is following. **Timeline** is particularly useful when you want feed data from a specific time range or when you want to sort with the **ByCreatedTime** option (which includes the largest sampling of people).
    
  
- **Likes** contains reference threads with a **PostReference** property that represents a post that the current user has flagged with the **Like** attribute.
    
  
- **Everyone** contains the threads from the current user's whole organization.
    
  
The server, client, and JavaScript object models provide the **GetFeed** method that you can use to retrieve any feed type for the current user and the **GetFeedFor** method that you can use to retrieve the **Personal** feed type (only) for a specified user. Both methods take a **SocialFeedOptions** object as a parameter, which you use to specify the time-based sort order, date range, and maximum number of threads to return.
  
    
    

> **Примечание:** Служба REST предоставляет отдельные ресурсы для получения каждого веб-канала активности, как показано в таблице 2. 
  
    
    

If a thread contains more than two replies, the server returns a digest of the thread that contains only the two most recent replies. (Thread digests have the **IsDigest** thread attribute applied.) If you want to get all the replies in a thread, call the **GetFullThread** method from the feed manager object and pass in the thread identifier.
  
    
    

## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="bkmk_AdditionalResources"> </a>


- **Conceptual and how-to articles**
    
  
-  [Социальные функции и функции совместной работы в SharePoint](social-and-collaboration-features-in-sharepoint.md)
    
  
-  [Начало разработки с использованием социальных функций в SharePoint](get-started-developing-with-social-features-in-sharepoint.md)
    
  
-  [Как: Создание и удаление сообщений и извлечение социальных веб-канал с помощью клиентской объектной модели .NET в SharePoint](how-to-create-and-delete-posts-and-retrieve-the-social-feed-by-using-the-net-cli.md)
    
  
-  [Как: Создание и удаление сообщений и извлечение социальных веб-канал с помощью объектной модели JavaScript в SharePoint](how-to-create-and-delete-posts-and-retrieve-the-social-feed-by-using-the-javascr.md)
    
  
-  [Как: сведения для чтения и записи социальных канал с помощью службы REST в SharePoint](how-to-learn-to-read-and-write-to-the-social-feed-by-using-the-rest-service-in-s.md)
    
  
-  [Как: Включение упоминания, теги и ссылки на сайты и документы в публикации в SharePoint](how-to-include-mentions-tags-and-links-to-sites-and-documents-in-posts-in-sharep.md)
    
  
-  [Как: Внедрение изображения, видео и документы в публикации в SharePoint](how-to-embed-images-videos-and-documents-in-posts-in-sharepoint-server.md)
    
  
-  [Справочник по потоки и потоки дайджест в веб-каналов социальных SharePoint](reference-threads-and-digest-threads-in-sharepoint-server-social-feeds.md)
    
  
- **API reference documentation**
    
  
-  [Microsoft.SharePoint.Client.Social](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.aspx) (client object model)
    
  
-  [SP.Social namespace](http://msdn.microsoft.com/library/43d47f01-c085-0e77-bd01-48bcb7d5bb35%28Office.15%29.aspx) (JavaScript object model)
    
  
-  [Social feed REST API reference for SharePoint](social-feed-rest-api-reference-for-sharepoint.md)
    
  
-  [Microsoft.Office.Server.Social](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.aspx) (server object model)
    
  
