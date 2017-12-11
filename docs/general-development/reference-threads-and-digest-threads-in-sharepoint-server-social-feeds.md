---
title: "Справочник по потоки и потоки дайджест в веб-каналов социальных SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 58e68fb2-ba40-4861-912f-355e119a1c41
ms.openlocfilehash: b902efe9ba6579d534ebc15bda7a15cf7d7c4ec6
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="reference-threads-and-digest-threads-in-sharepoint-social-feeds"></a>Справочник по потоки и потоки дайджест в веб-каналов социальных SharePoint
Узнайте о ссылку потоки и потоки дайджест, которые являются типы потоков, которые могут быть включены в коллекцию потоков, которые составляют социальные веб-канала в SharePoint.
При извлечении социальных канал SharePoint возвращает объект [SocialFeed](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeed.aspx) , который содержит коллекцию объектов [SocialThread](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThread.aspx) , которые составляют веб-канал. Эти потоки может представлять бесед, публикации в одном микроблога и уведомлений, которые включают событий и справочной потоков. Потоки, которые представляют бесед может быть возвращено сервером как дайджест потоков.
  
> [!NOTE]
> [!Примечание] В этой статье API  от клиентской объектной модели .NET. Тем не менее соответствующих объектов в другие API-интерфейсы могут отличаться. Для ссылки на другие связанные интерфейсы API в разделе  [Дополнительные ресурсы](#bk_addresources) .
  
    
    


## <a name="what-are-reference-threads-in-sharepoint-social-feeds"></a>Что такое потоков ссылку в каналы социальных SharePoint?
<a name="bk_whatAreRefThreads"> </a>

Если пользователь нравится post, упоминания другого пользователя в записи, ответов на публикацию или содержит тег в сообщение, SharePoint создает ссылку потока. Потоки ссылки имеют два свойства, используемые для получения сведений о указанный поток или размещать: [ThreadType](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThread.ThreadType.aspx) и [PostReference](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThread.PostReference.aspx) .
  
    
    
Справочник по потока можно определить, его свойство  [ThreadType](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThread.ThreadType.aspx) , которое может возвратить одно из значений, показано в таблице 1.
  
    
    

**В таблице 1. Типы потока ссылки**


|**Тип ссылки**|**Описание**|
|:-----|:-----|
| [LikeReference](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThreadType.LikeReference.aspx) **** <br/> |Ссылка на публикацию, оценки пользователя.  <br/> |
| [MentionReference](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThreadType.MentionReference.aspx) <br/> |Ссылка на публикацию, в котором упомянут пользователь.  <br/> |
| [ReplyReference](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThreadType.ReplyReference.aspx) <br/> |Ссылка на ее в ответ.  <br/> |
| [TagReference](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThreadType.TagReference.aspx) <br/> |Ссылка на сообщение, которое содержит тег.  <br/> |
| [Normal](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThreadType.Normal.aspx) <br/> |Не потока ссылку.  <br/> |
   
Свойство  [PostReference](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThread.PostReference.aspx) возвращает объект [SocialPostReference](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostReference.aspx) , который содержит сведения о потоке, которая вызвала событие. Как минимум он содержит идентификатор потока источника, которое затем используется с методом [SocialFeedManager.GetFullThread](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.GetFullThread.aspx) для извлечения потока, если он существует.
  
    
    
 [SocialPostReference](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostReference.aspx) также может содержать копию исходного post или потока. В этом доступности зависит от типа канала, тип потока и фильтрация по ролям безопасности. Если ссылка содержит сообщение или поток, эти объекты представляют моментальные снимки post или потока во время события.
  
    
    
Не все действия, связанные с веб-канал учитываются на канал как ссылку потоков. Например после уведомления (например, когда кто-то начинается после сайта) не потоков ссылку.
  
> [!NOTE]
> SharePoint автоматически безопасности сокращает контент в автоматически созданный публикации, а также для доступа к сайту в все сообщения, которые направлены на сайт веб-канала. Тем не менее можно использовать атрибут **SecurityUris** для безопасности удаления любого post, указав URL-адрес. Пользователи, у которых нет доступа на URL-адрес не получают post.
  
    
    

Ответ, как и ссылки на неограниченное время хранятся в пользователя личные веб-канала в видео. Тег ссылки хранятся в распределенного кэша, поэтому временно хранятся. Дополнительные сведения о кэшировании можно [Обзор функций микроблога, веб-каналов и службы распределенного кэша в SharePoint](http://technet.microsoft.com/en-us/library/jj219700%28v=office.15%29.aspx#cache).
  
    
    

## <a name="what-are-digest-threads-in-sharepoint-social-feeds"></a>Что такое дайджест потоков в веб-каналов социальных SharePoint?
<a name="bk_whatAreDigests"> </a>

Поток дайджест представляет компактной версии беседы, он содержит корневой post и два последних ответы потока. Можно определить поток дайджест, проверяя, имеет ли поток атрибут  [IsDigest](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThreadAttributes.IsDigest.aspx) в своем свойстве [Attributes](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThread.Attributes.aspx) . Чтобы проверить, имеет ли поток более двух потоков, щелкните свойство [TotalReplyCount](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThread.TotalReplyCount.aspx) .
  
    
    
Для оптимизации производительности, когда поток содержит более двух ответов, сервер возвращает дайджест потока. Если вы хотите получить все ответы для потока, вызовите метод  [SocialFeedManager.GetFullThread](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.GetFullThread.aspx) и передает идентификатор потока.
  
    
    

## <a name="see-also"></a>См. также
<a name="bk_addresources"> </a>


-  [Работа с социальными веб-каналами в SharePoint](work-with-social-feeds-in-sharepoint.md)
    
  
-  [SocialThread](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThread.aspx) в клиентской объектной модели .NET
    
  
-  [SocialThread](http://msdn.microsoft.com/library/46aa4beb-d708-f20e-471e-626c8a7efab7%28Office.15%29.aspx) в объектной модели JavaScript
    
  
-  [SPSocialThread](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialThread.aspx) в серверной объектной модели
    
  

