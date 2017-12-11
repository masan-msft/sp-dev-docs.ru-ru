---
title: "Создание и удаление сообщений и извлечение социальных веб-канал с помощью клиентской объектной модели .NET в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: c8d68632-1b55-454c-961a-f3ddad731bf6
ms.openlocfilehash: 5ffd9e779ffeb7db7a09144912777dcfc0f417e0
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="create-and-delete-posts-and-retrieve-the-social-feed-by-using-the-net-client-object-model-in-sharepoint"></a>Создание и удаление сообщений и извлечение социальных веб-канал с помощью клиентской объектной модели .NET в SharePoint

Узнайте, как создавать и удалять записи микроблогов и восстанавливать каналы социальных сетей с помощью клиентской объектной модели .NET для SharePoint.

## <a name="what-are-social-feeds-in-sharepoint"></a>Что такое социальные веб-каналами в SharePoint
<a name="bk_intro"> </a>

В SharePoint социальные веб-канал представляет собой коллекцию потоков, которые представляют бесед, публикации в одном микроблога или уведомления. Потоки имеют корневой post и коллекцию публикации в ответ, и они представляют бесед, публикации в одном микроблога или уведомления. В клиентской объектной модели .NET веб-каналов, представленные объектами [SocialFeed](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeed.aspx) , потоки, представленные объектами [SocialThread](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThread.aspx) и публикации и ответы, представленные объектами [SocialPost](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPost.aspx) . Для выполнения основных задач, связанных с веб-канала в клиентской объектной модели .NET, используйте объект [SocialFeedManager](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.aspx) . В этой статье мы покажем, как создать консольное приложение, с помощью клиентской объектной модели .NET для работы с социальными веб-каналами.
  
    
    
Дополнительные сведения о работе с [SocialFeedManager](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.aspx) , а также сведения об использовании других API-интерфейсы для работы с социальными веб-каналами просмотрите [Работа с социальными веб-каналами в SharePoint](work-with-social-feeds-in-sharepoint.md).
  
    
    

## <a name="prerequisites-for-setting-up-your-development-environment-to-work-with-social-feeds-by-using-the-sharepoint-net-client-object-model"></a>Необходимые условия для настройки среды разработки для работы с социальными веб-каналами с помощью клиентской объектной модели SharePoint .NET
<a name="bkmk_SetUpDevEnv"> </a>

Создание консольного приложения, использующего клиентской объектной модели .NET для работы с социальными веб-каналов, то необходимо:
  
    
    

- SharePoint с личного сайта настроены, личные сайты, созданные для текущего пользователя и конечного пользователя, с текущим пользователем после конечного пользователя и несколько записей, записанные центром конечного пользователя
    
  
- Visual Studio 2012
    
  
- **Полный** доступ к приложению-службе профилей пользователей для пользователя, вошедшего в систему
    
> [!NOTE]
> Если вы работаете не на компьютере, на котором работает SharePoint, загрузить [Клиентских компонентов SharePoint](http://www.microsoft.com/en-us/download/details.aspx?id=35585) , содержащий клиентскую сборку SharePoint.
  
    
    


## <a name="create-a-console-application-that-works-with-social-feeds-by-using-the-sharepoint-net-client-object-model"></a>Создание консольного приложения, работающего с социальными веб-каналами с помощью клиентской объектной модели SharePoint .NET
<a name="bk_createconsole"> </a>


1. Откройте Visual Studio и в меню **Файл** последовательно выберите элементы **Создать** и **Проект**.
    
  
2. В диалоговом окне **Новый проект** выберите **.NET Framework 4.5** из раскрывающегося списка в верхней части окна.
    
  
3. В списке **шаблонов** выберите **Windows** и затем выберите шаблон **Консольное приложение**.
    
  
4. Назовите проект SocialFeedCSOMи затем нажмите кнопку **ОК**.
    
  
5. Добавьте ссылки на следующие сборки:
    
   - **Microsoft.SharePoint.Client**
   - **Microsoft.SharePoint.ClientRuntime**
   - **Microsoft.SharePoint.Client.UserProfiles**
  
6. Замените содержимое класса **Program** в примере кода на класс из следующих сценариев:
    
   -  [Публикация сообщения и ответы, которые социальные веб-канал](how-to-create-and-delete-posts-and-retrieve-the-social-feed-by-using-the-net-cli.md#bkmk_PubPosts) 
   -  [Извлечение социальных веб-каналов](how-to-create-and-delete-posts-and-retrieve-the-social-feed-by-using-the-net-cli.md#bkmk_GetFeeds) 
   -  [Удаление публикации и ответы из социальных канала](how-to-create-and-delete-posts-and-retrieve-the-social-feed-by-using-the-net-cli.md#bkmk_DeletePosts)
    
7. Тестирование консольного приложения в строке меню выберите команду **Отладка**, **Начать отладку**.
    
  

## <a name="code-example-publish-posts-and-replies-to-the-social-feed-by-using-the-sharepoint-net-client-object-model"></a>Пример кода: публикация публикации и ответы, которые социальных сетей канал с помощью клиентской объектной модели SharePoint .NET
<a name="bkmk_PubPosts"> </a>

В следующем примере кода публикует сообщение и ответ от текущего пользователя. В нем показано, как:
  
    
    

- После определения содержимого. В этом примере ссылка в записи.
    
  
- Публикация post на канал для текущего пользователя, используя метод  [CreatePost](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.CreatePost.aspx) и передача **null** в качестве параметра _targetId_.
    
  
- Получите [тип веб-канал](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedType.aspx) **новостей** для текущего пользователя с помощью метода [GetFeed](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.GetFeed.aspx) .
    
  
- Выполните итерацию по веб-канал для поиска всех потоков, которые могут быть дан ответ и для получения сведений о потоков и публикации.
    
  
- Ответ на публикацию с помощью метода  [CreatePost](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.CreatePost.aspx) , передав в качестве параметра _targetId_ идентификатор потока.
    
> [!NOTE]
> [!Примечание] Измените значение заполнитель для переменной **serverUrl**, прежде чем запускать код.
  
    
    


```cs

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Microsoft.SharePoint.Client;
using Microsoft.SharePoint.Client.Social;

namespace SocialFeedCSOM
{
    class Program
    {
        static void Main(string[] args)
        {
            // Replace the following placeholder value with the target server URL.
            const string serverUrl = "http://serverName/";

            Console.Write("Type your post text:  ");

            // Create a link to include in the post.
            SocialDataItem linkDataItem = new SocialDataItem();
            linkDataItem.ItemType = SocialDataItemType.Link;
            linkDataItem.Text = "link";
            linkDataItem.Uri = "http://bing.com";

            // Define properties for the post.
            SocialPostCreationData postCreationData = new SocialPostCreationData();
            postCreationData.ContentText = Console.ReadLine() + " Plus a {0}.";
            postCreationData.ContentItems = new SocialDataItem[1] { linkDataItem };

            // Get the client context.
            ClientContext clientContext = new ClientContext(serverUrl);

            // Get the SocialFeedManager instance.
            SocialFeedManager feedManager = new SocialFeedManager(clientContext);

            // Publish the post. This is a root post, so specify null for the
            // targetId parameter. 
            feedManager.CreatePost(null, postCreationData); 
            clientContext.ExecuteQuery();

            Console.WriteLine("\\nCurrent user's newsfeed:");

            // Set parameters for the feed content that you want to retrieve.
            SocialFeedOptions feedOptions = new SocialFeedOptions();

            // Get the target owner's feed and then run the request on the server.
            ClientResult<SocialFeed> feed = feedManager.GetFeed(SocialFeedType.News, feedOptions);
            clientContext.ExecuteQuery();

            // Create a dictionary to store the Id property of each thread. This 
            // code example stores the Id so you can select a thread to reply to.
            Dictionary<int, string> idDictionary = new Dictionary<int, string>();

            // Iterate through each thread in the feed.
            for (int i = 0; i < feed.Value.Threads.Length; i++)
            {
                SocialThread thread = feed.Value.Threads[i];

                // Keep only the threads that can be replied to.
                if (thread.Attributes.HasFlag(SocialThreadAttributes.CanReply))
                {
                    idDictionary.Add(i, thread.Id);

                    // Get properties from the root post and thread.
                    // If a thread contains more than two replies, the server returns
                    // a thread digest that contains only the two most recent replies.
                    // To get all replies, call SocialFeedManager.GetFullThread.
                    SocialPost rootPost = thread.RootPost;
                    SocialActor author = thread.Actors[rootPost.AuthorIndex];
                    Console.WriteLine(string.Format("{0}. {1} said \\"{2}\\" ({3} replies)",
                        (i + 1), author.Name, rootPost.Text, thread.TotalReplyCount));
                }
            }
            Console.Write("\\nWhich thread number do you want to reply to?  ");

            string threadToReplyTo = "";
            int threadNumber = int.Parse(Console.ReadLine()) - 1;
            idDictionary.TryGetValue(threadNumber, out threadToReplyTo);

            Console.Write("Type your reply:  ");

            // Define properties for the reply. This example reuses the 
            // SocialPostCreationData object that was used to create a post.
            postCreationData.ContentText = Console.ReadLine();

            // Publish the reply and make the changes on the server.
            ClientResult<SocialThread> result = feedManager.CreatePost(threadToReplyTo, postCreationData);
            clientContext.ExecuteQuery();

            Console.WriteLine("\\nThe reply was published. The thread now has {0} replies.", result.Value.TotalReplyCount);
            Console.ReadLine();
         }
    }
}
```


## <a name="code-example-retrieve-social-feeds-by-using-the-sharepoint-net-client-object-model"></a>Пример кода: получение социальными веб-каналами с помощью клиентской объектной модели SharePoint .NET
<a name="bkmk_GetFeeds"> </a>

В следующем примере кода показано получение веб-каналов для текущего пользователя и конечного пользователя. В нем показано, как:
  
    
    

- Получите **личный**, **Новости**и **временной шкалы**,[типы веб-канала](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedType.aspx) для текущего пользователя с помощью метода [GetFeed](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.GetFeed.aspx) .
    
  
- Получение **личных** [веб-канала типа](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedType.Personal.aspx) для конечного пользователя с помощью метода [GetFeedFor](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.GetFeedFor.aspx) .
    
  
- Выполните итерацию по веб-каналы, чтобы найти все потоки, не являющиеся ссылку и для получения сведений о потоков и публикации. Справочник по потоков представляют уведомлений, которые содержат сведения о другого потока. Например, если пользователь упоминания другого пользователя в записи, сервера создает **MentionReference**-введите поток, который содержит ссылки на исходное сообщение и другие метаданные о post.
    
  
Дополнительные сведения о типах веб-канала активности можно [Обзор типов веб-канала активности](work-with-social-feeds-in-sharepoint.md#bkmk_FeedTypes). Дополнительные сведения о потоках ссылку можно [ссылку потоки и потоки дайджест в веб-каналов социальных SharePoint](reference-threads-and-digest-threads-in-sharepoint-server-social-feeds.md).
  
> [!NOTE]
> [!Примечание] Изменение значений заполнитель для переменных **serverUrl** и **targetUser**, прежде чем запускать код.
  
    
    




```cs

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Microsoft.SharePoint.Client;
using Microsoft.SharePoint.Client.Social;

namespace SocialFeedCSOM
{
    class Program
    {
        static string owner;
        static void Main(string[] args)
        {

            // Replace the following placeholder values with the target
            // server URL and target thread owner.
            const string serverUrl = "http://serverName/";
            const string targetUser = "domainName\\\\userName";

            // Get the client context.
            ClientContext clientContext = new ClientContext(serverUrl);

            // Get the SocialFeedManager instance. 
            // Load the instance to get the Owner property.
            SocialFeedManager feedManager = new SocialFeedManager(clientContext);
            clientContext.Load(feedManager, f => f.Owner);

            // Set parameters for the feed content that you want to retrieve.
            SocialFeedOptions feedOptions = new SocialFeedOptions();
            feedOptions.MaxThreadCount = 10; // default is 20

            // Get all feed types for current user and get the Personal feed
            // for the target user.
            ClientResult<SocialFeed> personalFeed = feedManager.GetFeed(SocialFeedType.Personal, feedOptions);
            ClientResult<SocialFeed> newsFeed = feedManager.GetFeed(SocialFeedType.News, feedOptions);
            ClientResult<SocialFeed> targetUserFeed = feedManager.GetFeedFor(targetUser, feedOptions);

            // Change the sort order to optimize the Timeline feed results.
            feedOptions.SortOrder = SocialFeedSortOrder.ByCreatedTime;
            ClientResult<SocialFeed> timelineFeed = feedManager.GetFeed(SocialFeedType.Timeline, feedOptions);

            // Run the request on the server.
            clientContext.ExecuteQuery();

            // Get the name of the current user within this instance.
            owner = feedManager.Owner.Name;

            // Iterate through the feeds and write the content.
            IterateThroughFeed(personalFeed.Value, SocialFeedType.Personal, true);
            IterateThroughFeed(newsFeed.Value, SocialFeedType.News, true);
            IterateThroughFeed(timelineFeed.Value, SocialFeedType.Timeline, true);
            IterateThroughFeed(targetUserFeed.Value, SocialFeedType.Personal, false);

            Console.ReadKey(false);
        }

        // Iterate through the feed and write to the console window.
        static void IterateThroughFeed(SocialFeed feed, SocialFeedType feedType, bool isCurrentUserOwner)
        {
            SocialThread[] threads = feed.Threads;

            // If this is the target user's feed, get the user's name.
            // A user is the owner of all threads in his or her Personal feed.
            if (!isCurrentUserOwner)
            {
                SocialThread firstThread = threads[0];
                owner = firstThread.Actors[firstThread.OwnerIndex].Name;
            }
            Console.WriteLine(string.Format("\\n{0} feed type for {1}:", feedType.ToString(), owner));

            // Iterate through each thread in the feed.
            foreach (SocialThread thread in threads)
            {

                // Ignore reference thread types.
                if (thread.ThreadType == SocialThreadType.Normal)
                {

                    // Get properties from the root post and thread. 
                    // If a thread contains more than two replies, the server returns
                    // a thread digest that contains only the two most recent replies.
                    // To get all replies, call SocialFeedManager.GetFullThread.
                    SocialPost rootPost = thread.RootPost;
                    SocialActor author = thread.Actors[rootPost.AuthorIndex];
                    Console.WriteLine(string.Format("  - {0} posted \\"{1}\\" on {2}. This thread has {3} replies.",
                        author.Name, rootPost.Text, rootPost.CreatedTime.ToShortDateString(), thread.TotalReplyCount));
                }
            }
        }
    }
}
```


## <a name="code-example-delete-posts-and-replies-from-the-social-feed-by-using-the-sharepoint-net-client-object-model"></a>Пример кода: Delete публикации и ответы из социальных канала с помощью клиентской объектной модели SharePoint .NET
<a name="bkmk_DeletePosts"> </a>

В следующем примере кода удаляет сообщение или ответ из личных веб-канал текущего пользователя. В нем показано, как:
  
    
    

- Получите **личных** [веб-канала типа](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedType.aspx) для текущего пользователя с помощью метода [GetFeed](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.GetFeed.aspx) .
    
  
- Выполните итерацию по потоков в веб-канал для получения сведений о корневой публикации и ответы.
    
  
- Удаление корневого post, ответ или потока с помощью метода  [DeletePost](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.DeletePost.aspx) (корневой post при удалении весь поток).
    
> [!NOTE]
> [!Примечание] Измените значение заполнитель для переменной **serverUrl**, прежде чем запускать код.
  
    
    


```cs

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Microsoft.SharePoint.Client;
using Microsoft.SharePoint.Client.Social;

namespace SocialFeedCSOM
{
    class Program
    {
        static void Main(string[] args)
        {

            // Replace the following placeholder value with the target SharePoint server.
            const string serverUrl = "http://serverName/";

            // Get the client context.
            ClientContext clientContext = new ClientContext(serverUrl);

            // Get the SocialFeedManager instance.
            SocialFeedManager feedManager = new SocialFeedManager(clientContext);

            Console.WriteLine("\\nCurrent user's personal feed:");

            // Set the parameters for the feed content that you want to retrieve.
            SocialFeedOptions feedOptions = new SocialFeedOptions();

            // Get the target owner's feed (posts and activities) and
            // then run the request on the server.
            ClientResult<SocialFeed> feed = feedManager.GetFeed(SocialFeedType.Personal, feedOptions);
            clientContext.ExecuteQuery();

            // Create a dictionary to store the Id property of each post and
            // reply. This code example stores the Id so you can select a post
            // or a reply to delete.
            Dictionary<int, string> idDictionary = new Dictionary<int, string>();

            // Iterate through each thread in the feed.
            for (int i = 0; i < feed.Value.Threads.Length; i++)
            {
                SocialThread thread = feed.Value.Threads[i];
                SocialPost rootPost = thread.RootPost;

                // Only keep posts that can be deleted.
                if (rootPost.Attributes.HasFlag(SocialPostAttributes.CanDelete)) 
                {
                    idDictionary.Add(i, rootPost.Id);

                    Console.WriteLine(string.Format("{0}. \\"{1}\\" has {2} replies.",
                        (i + 1), rootPost.Text, thread.TotalReplyCount));

                    // Get the replies.
                    // If a thread contains more than two replies, the server returns
                    // a thread digest that contains only the two most recent replies.
                    // To get all replies, call SocialFeedManager.GetFullThread.
                    if (thread.TotalReplyCount > 0)
                    {
                        foreach (SocialPost reply in thread.Replies)
                        {

                            // Only keep replies that can be deleted.
                            if (reply.Attributes.HasFlag(SocialPostAttributes.CanDelete)) 
                            {
                                i++;
                                idDictionary.Add(i, reply.Id);

                                SocialActor author = thread.Actors[reply.AuthorIndex];
                                Console.WriteLine(string.Format("\\t{0}. {1} replied \\"{2}\\"",
                                    (i + 1), author.Name, reply.Text));
                            }
                        }
                    }
                }
            }
            Console.Write("\\nEnter the number of the post or reply to delete. "
                + "(If you choose a root post, the whole thread is deleted.)");
            string postToDelete = "";
            int postNumber = int.Parse(Console.ReadLine()) - 1;
            idDictionary.TryGetValue(postNumber, out postToDelete);

            // Delete the reply and make the changes on the server.
            ClientResult<SocialThread> result = feedManager.DeletePost(postToDelete);
            clientContext.ExecuteQuery();

            // DeletePost returns digest thread if the deleted post is not the
            // root post. If it is the root post, the whole thread is deleted
            // and DeletePost returns null.
            if (result.Value != null)
            {
                SocialThread threadResult = result.Value;
                Console.WriteLine("\\nThe reply was deleted. The thread now has {0} replies.", threadResult.TotalReplyCount);
            }
            else
            {
                Console.WriteLine("\\nThe post and thread were deleted.");
            }
            Console.ReadKey(false);
        }
    }
}
```


## <a name="next-steps"></a>Дальнейшие действия
<a name="bkmk_DeletePosts"> </a>

 [Как добавлять в записи упоминания, теги и ссылки на сайты и документы в SharePoint](how-to-include-mentions-tags-and-links-to-sites-and-documents-in-posts-in-sharep.md)
  
    
    

## <a name="see-also"></a>См. также
<a name="bk_addResources"> </a>


-  [Работа с социальными веб-каналами в SharePoint](work-with-social-feeds-in-sharepoint.md)
    
  
-  [Как: Создание и удаление сообщений и извлечение социальных веб-канал с помощью объектной модели JavaScript в SharePoint](how-to-create-and-delete-posts-and-retrieve-the-social-feed-by-using-the-javascr.md)
    
  
-  [Как: сведения для чтения и записи социальных канал с помощью службы REST в SharePoint](how-to-learn-to-read-and-write-to-the-social-feed-by-using-the-rest-service-in-s.md)
    
  
-  [Справочник по потоки и потоки дайджест в веб-каналов социальных SharePoint](reference-threads-and-digest-threads-in-sharepoint-server-social-feeds.md)
    
  

