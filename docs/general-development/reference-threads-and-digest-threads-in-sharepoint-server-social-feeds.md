---
title: "Справочник по потоки и потоки дайджест в веб-каналов социальных SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 58e68fb2-ba40-4861-912f-355e119a1c41
ms.openlocfilehash: 93a0b2fde471617bf82b4132ceaeb9df0f1ba9de
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="reference-threads-and-digest-threads-in-sharepoint-social-feeds"></a><span data-ttu-id="56278-102">Справочник по потоки и потоки дайджест в веб-каналов социальных SharePoint</span><span class="sxs-lookup"><span data-stu-id="56278-102">Reference threads and digest threads in SharePoint social feeds</span></span>
<span data-ttu-id="56278-103">Узнайте о ссылку потоки и потоки дайджест, которые являются типы потоков, которые могут быть включены в коллекцию потоков, которые составляют социальные веб-канала в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="56278-103">Learn about reference threads and digest threads, which are thread types that may be included in the collection of threads that make up a social feed in SharePoint.</span></span>
<span data-ttu-id="56278-104">При извлечении социальных канал SharePoint возвращает объект [SocialFeed](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeed.aspx) , который содержит коллекцию объектов [SocialThread](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThread.aspx) , которые составляют веб-канал.</span><span class="sxs-lookup"><span data-stu-id="56278-104">When you retrieve a social feed, SharePoint returns a  [SocialFeed](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeed.aspx) object that contains the collection of [SocialThread](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThread.aspx) objects that make up the feed.</span></span> <span data-ttu-id="56278-105">Эти потоки может представлять бесед, публикации в одном микроблога и уведомлений, которые включают событий и справочной потоков.</span><span class="sxs-lookup"><span data-stu-id="56278-105">These threads can represent conversations, single microblog posts, and notifications, which include events and reference threads.</span></span> <span data-ttu-id="56278-106">Потоки, которые представляют бесед может быть возвращено сервером как дайджест потоков.</span><span class="sxs-lookup"><span data-stu-id="56278-106">Threads that represent conversations may be returned by the server as digest threads.</span></span>
  
    
    


> <span data-ttu-id="56278-107">**Примечание:** В этой статье API — от клиентской объектной модели .NET.</span><span class="sxs-lookup"><span data-stu-id="56278-107">**Note:** The API referenced in this article is from the .NET client object model.</span></span> <span data-ttu-id="56278-108">Тем не менее соответствующих объектов в другие API-интерфейсы могут отличаться.</span><span class="sxs-lookup"><span data-stu-id="56278-108">However, corresponding objects in other APIs might be different.</span></span> <span data-ttu-id="56278-109">Для ссылки на другие связанные интерфейсы API в разделе [Дополнительные ресурсы](#bk_addresources) .</span><span class="sxs-lookup"><span data-stu-id="56278-109">See  [Additional resources](#bk_addresources) for links to other related APIs.</span></span>
  
    
    


## <a name="what-are-reference-threads-in-sharepoint-social-feeds"></a><span data-ttu-id="56278-110">Что такое потоков ссылку в каналы социальных SharePoint?</span><span class="sxs-lookup"><span data-stu-id="56278-110">What are reference threads in SharePoint social feeds?</span></span>
<span data-ttu-id="56278-111"><a name="bk_whatAreRefThreads"> </a></span><span class="sxs-lookup"><span data-stu-id="56278-111"></span></span>

<span data-ttu-id="56278-112">Если пользователь нравится post, упоминания другого пользователя в записи, ответов на публикацию или содержит тег в сообщение, SharePoint создает ссылку потока.</span><span class="sxs-lookup"><span data-stu-id="56278-112">When a user likes a post, mentions someone in a post, replies to a post, or includes a tag in a post, SharePoint generates a reference thread.</span></span> <span data-ttu-id="56278-113">Потоки ссылки имеют два свойства, используемые для получения сведений о указанный поток или размещать: [ThreadType](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThread.ThreadType.aspx) и [PostReference](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThread.PostReference.aspx) .</span><span class="sxs-lookup"><span data-stu-id="56278-113">Reference threads have two properties that you use to get information about the referenced thread or post:  [ThreadType](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThread.ThreadType.aspx) and [PostReference](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThread.PostReference.aspx) .</span></span>
  
    
    
<span data-ttu-id="56278-114">Справочник по потока можно определить, его свойство  [ThreadType](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThread.ThreadType.aspx) , которое может возвратить одно из значений, показано в таблице 1.</span><span class="sxs-lookup"><span data-stu-id="56278-114">You can identify a reference thread by its  [ThreadType](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThread.ThreadType.aspx) property, which can return one of the values shown in Table 1.</span></span>
  
    
    

<span data-ttu-id="56278-115">**В таблице 1. Типы потока ссылки**</span><span class="sxs-lookup"><span data-stu-id="56278-115">**Table 1. Types of reference thread**</span></span>


|<span data-ttu-id="56278-116">**Тип ссылки**</span><span class="sxs-lookup"><span data-stu-id="56278-116">**Reference type**</span></span>|<span data-ttu-id="56278-117">**Описание**</span><span class="sxs-lookup"><span data-stu-id="56278-117">**Description**</span></span>|
|:-----|:-----|
| <span data-ttu-id="56278-118">[LikeReference](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThreadType.LikeReference.aspx) **** </span><span class="sxs-lookup"><span data-stu-id="56278-118">[LikeReference](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThreadType.LikeReference.aspx) **** </span></span><br/> |<span data-ttu-id="56278-119">Ссылка на публикацию, оценки пользователя.</span><span class="sxs-lookup"><span data-stu-id="56278-119">A reference to a post that a user likes.</span></span>  <br/> |
| [<span data-ttu-id="56278-120">MentionReference</span><span class="sxs-lookup"><span data-stu-id="56278-120">MentionReference</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThreadType.MentionReference.aspx) <br/> |<span data-ttu-id="56278-121">Ссылка на публикацию, в котором упомянут пользователь.</span><span class="sxs-lookup"><span data-stu-id="56278-121">A reference to a post that mentions a user.</span></span>  <br/> |
| [<span data-ttu-id="56278-122">ReplyReference</span><span class="sxs-lookup"><span data-stu-id="56278-122">ReplyReference</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThreadType.ReplyReference.aspx) <br/> |<span data-ttu-id="56278-123">Ссылка на ее в ответ.</span><span class="sxs-lookup"><span data-stu-id="56278-123">A reference to a reply.</span></span>  <br/> |
| [<span data-ttu-id="56278-124">TagReference</span><span class="sxs-lookup"><span data-stu-id="56278-124">TagReference</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThreadType.TagReference.aspx) <br/> |<span data-ttu-id="56278-125">Ссылка на сообщение, которое содержит тег.</span><span class="sxs-lookup"><span data-stu-id="56278-125">A reference to a post that contains a tag.</span></span>  <br/> |
| [<span data-ttu-id="56278-126">Normal</span><span class="sxs-lookup"><span data-stu-id="56278-126">Normal</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThreadType.Normal.aspx) <br/> |<span data-ttu-id="56278-127">Не потока ссылку.</span><span class="sxs-lookup"><span data-stu-id="56278-127">Not a reference thread.</span></span>  <br/> |
   
<span data-ttu-id="56278-p104">Свойство  [PostReference](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThread.PostReference.aspx) возвращает объект [SocialPostReference](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostReference.aspx) , который содержит сведения о потоке, которая вызвала событие. Как минимум он содержит идентификатор потока источника, которое затем используется с методом [SocialFeedManager.GetFullThread](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.GetFullThread.aspx) для извлечения потока, если он существует.</span><span class="sxs-lookup"><span data-stu-id="56278-p104">The  [PostReference](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThread.PostReference.aspx) property returns a [SocialPostReference](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostReference.aspx) object that contains information about the thread that triggered the event. At a minimum, it contains the ID of the source thread, which you can then use with the [SocialFeedManager.GetFullThread](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.GetFullThread.aspx) method to retrieve the thread if it still exists.</span></span>
  
    
    
 <span data-ttu-id="56278-p105">[SocialPostReference](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostReference.aspx) также может содержать копию исходного post или потока. В этом доступности зависит от типа канала, тип потока и фильтрация по ролям безопасности. Если ссылка содержит сообщение или поток, эти объекты представляют моментальные снимки post или потока во время события.</span><span class="sxs-lookup"><span data-stu-id="56278-p105">[SocialPostReference](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostReference.aspx) might also contain a copy of the source post or thread. This availability depends on the feed type, thread type, and security trimming. If the reference does contain a post or thread, these objects represent snapshots of the post or thread at the time the event occurred.</span></span>
  
    
    
<span data-ttu-id="56278-p106">Не все действия, связанные с веб-канал учитываются на канал как ссылку потоков. Например после уведомления (например, когда кто-то начинается после сайта) не потоков ссылку.</span><span class="sxs-lookup"><span data-stu-id="56278-p106">Not all feed-related activities are posted to the feed as reference threads. For example, Following notifications (such as when someone starts following a site) are not reference threads.</span></span>
  
    
    

> <span data-ttu-id="56278-135">**Примечание:** SharePoint автоматически безопасности сокращает контент в автоматически созданный публикации, а также для доступа к сайту в все сообщения, которые направлены на сайт веб-канала.</span><span class="sxs-lookup"><span data-stu-id="56278-135">**Note:** SharePoint automatically security trims for content in autogenerated posts and for site access in all posts that are directed to a site feed.</span></span> <span data-ttu-id="56278-136">Тем не менее можно использовать атрибут **SecurityUris** для безопасности удаления любого post, указав URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="56278-136">However, you can use the **SecurityUris** attribute to security trim any post by specifying a URL.</span></span> <span data-ttu-id="56278-137">Пользователи, у которых нет доступа на URL-адрес не получают post.</span><span class="sxs-lookup"><span data-stu-id="56278-137">Users who do not have access to the URL do not receive the post.</span></span>
  
    
    

<span data-ttu-id="56278-138">Ответ, как и ссылки на неограниченное время хранятся в пользователя личные веб-канала в видео.</span><span class="sxs-lookup"><span data-stu-id="56278-138">Reply, like, and mention references are stored indefinitely in the user's personal feed.</span></span> <span data-ttu-id="56278-139">Тег ссылки хранятся в распределенного кэша, поэтому временно хранятся.</span><span class="sxs-lookup"><span data-stu-id="56278-139">Tag references are stored in the Distributed Cache, so they are stored temporarily.</span></span> <span data-ttu-id="56278-140">Дополнительные сведения о кэшировании можно [Обзор функций микроблога, веб-каналов и службы распределенного кэша в SharePoint](http://technet.microsoft.com/ru-ru/library/jj219700%28v=office.15%29.aspx#cache).</span><span class="sxs-lookup"><span data-stu-id="56278-140">For more information about caching, see  [Overview of microblog features, feeds, and the Distributed Cache service in SharePoint](http://technet.microsoft.com/ru-ru/library/jj219700%28v=office.15%29.aspx#cache).</span></span>
  
    
    

## <a name="what-are-digest-threads-in-sharepoint-social-feeds"></a><span data-ttu-id="56278-141">Что такое дайджест потоков в веб-каналов социальных SharePoint?</span><span class="sxs-lookup"><span data-stu-id="56278-141">What are digest threads in SharePoint social feeds?</span></span>
<span data-ttu-id="56278-142"><a name="bk_whatAreDigests"> </a></span><span class="sxs-lookup"><span data-stu-id="56278-142"></span></span>

<span data-ttu-id="56278-p109">Поток дайджест представляет компактной версии беседы, он содержит корневой post и два последних ответы потока. Можно определить поток дайджест, проверяя, имеет ли поток атрибут  [IsDigest](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThreadAttributes.IsDigest.aspx) в своем свойстве [Attributes](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThread.Attributes.aspx) . Чтобы проверить, имеет ли поток более двух потоков, щелкните свойство [TotalReplyCount](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThread.TotalReplyCount.aspx) .</span><span class="sxs-lookup"><span data-stu-id="56278-p109">A digest thread represents a compact version of a conversation—it contains the thread's root post and two most recent replies. You can identify a digest thread by checking whether the thread has the  [IsDigest](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThreadAttributes.IsDigest.aspx) attribute applied in its [Attributes](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThread.Attributes.aspx) property. To see whether a thread has more than two threads, check the [TotalReplyCount](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThread.TotalReplyCount.aspx) property.</span></span>
  
    
    
<span data-ttu-id="56278-p110">Для оптимизации производительности, когда поток содержит более двух ответов, сервер возвращает дайджест потока. Если вы хотите получить все ответы для потока, вызовите метод  [SocialFeedManager.GetFullThread](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.GetFullThread.aspx) и передает идентификатор потока.</span><span class="sxs-lookup"><span data-stu-id="56278-p110">To optimize performance, when a thread contains more than two replies, the server returns a digest thread. If you want to get all the replies for a thread, call the  [SocialFeedManager.GetFullThread](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.GetFullThread.aspx) method and pass in the thread ID.</span></span>
  
    
    

## <a name="additional-resources"></a><span data-ttu-id="56278-148">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="56278-148">Additional resources</span></span>
<span data-ttu-id="56278-149"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="56278-149"></span></span>


-  [<span data-ttu-id="56278-150">Работа с социальными веб-каналами в SharePoint</span><span class="sxs-lookup"><span data-stu-id="56278-150">Work with social feeds in SharePoint</span></span>](work-with-social-feeds-in-sharepoint.md)
    
  
-  <span data-ttu-id="56278-151">[SocialThread](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThread.aspx) в клиентской объектной модели .NET</span><span class="sxs-lookup"><span data-stu-id="56278-151">[SocialThread](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThread.aspx) in the .NET client object model</span></span>
    
  
-  <span data-ttu-id="56278-152">[SocialThread](http://msdn.microsoft.com/library/46aa4beb-d708-f20e-471e-626c8a7efab7%28Office.15%29.aspx) в объектной модели JavaScript</span><span class="sxs-lookup"><span data-stu-id="56278-152">[SocialThread](http://msdn.microsoft.com/library/46aa4beb-d708-f20e-471e-626c8a7efab7%28Office.15%29.aspx) in the JavaScript object model</span></span>
    
  
-  <span data-ttu-id="56278-153">[SPSocialThread](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialThread.aspx) в серверной объектной модели</span><span class="sxs-lookup"><span data-stu-id="56278-153">[SPSocialThread](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialThread.aspx) in the server object model</span></span>
    
  

