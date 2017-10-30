---
title: "Как создать \"и\" Удаление публикации и извлечение социальных сетей канал с помощью клиентской объектной модели .NET в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: c8d68632-1b55-454c-961a-f3ddad731bf6
ms.openlocfilehash: 57c579bd297a0c72fbb26293ce7da18ecc7defcb
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-create-and-delete-posts-and-retrieve-the-social-feed-by-using-the-net-client-object-model-in-sharepoint"></a><span data-ttu-id="6b76e-102">Как: Создание и удаление сообщений и извлечение социальных веб-канал с помощью клиентской объектной модели .NET в SharePoint</span><span class="sxs-lookup"><span data-stu-id="6b76e-102">How to: Create and delete posts and retrieve the social feed by using the .NET client object model in SharePoint</span></span>
<span data-ttu-id="6b76e-103">Узнайте, как создавать и удалять записи микроблогов и восстанавливать каналы социальных сетей с помощью клиентской объектной модели .NET для SharePoint.</span><span class="sxs-lookup"><span data-stu-id="6b76e-103">Learn how to create and delete microblog posts and retrieve social feeds by using the SharePoint .NET client object model.</span></span>
## <a name="what-are-social-feeds-in-sharepoint"></a><span data-ttu-id="6b76e-104">Что такое социальные веб-каналами в SharePoint</span><span class="sxs-lookup"><span data-stu-id="6b76e-104">What are social feeds in SharePoint?</span></span>
<span data-ttu-id="6b76e-105"><a name="bk_intro"> </a></span><span class="sxs-lookup"><span data-stu-id="6b76e-105"><a name="bk_intro"> </a></span></span>

<span data-ttu-id="6b76e-106">В SharePoint социальные веб-канал представляет собой коллекцию потоков, которые представляют бесед, публикации в одном микроблога или уведомления.</span><span class="sxs-lookup"><span data-stu-id="6b76e-106">In SharePoint, a social feed is a collection of threads that represent conversations, single microblog posts, or notifications.</span></span> <span data-ttu-id="6b76e-107">Потоки имеют корневой post и коллекцию публикации в ответ, и они представляют бесед, публикации в одном микроблога или уведомления.</span><span class="sxs-lookup"><span data-stu-id="6b76e-107">Threads contain a root post and a collection of reply posts, and they represent conversations, single microblog posts, or notifications.</span></span> <span data-ttu-id="6b76e-108">В клиентской объектной модели .NET веб-каналов, представленные объектами [SocialFeed](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeed.aspx) , потоки, представленные объектами [SocialThread](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThread.aspx) и публикации и ответы, представленные объектами [SocialPost](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPost.aspx) .</span><span class="sxs-lookup"><span data-stu-id="6b76e-108">In the .NET client object model, feeds are represented by  [SocialFeed](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeed.aspx) objects, threads are represented by [SocialThread](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThread.aspx) objects, and posts and replies are represented by [SocialPost](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPost.aspx) objects.</span></span> <span data-ttu-id="6b76e-109">Для выполнения основных задач, связанных с веб-канала в клиентской объектной модели .NET, используйте объект [SocialFeedManager](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.aspx) .</span><span class="sxs-lookup"><span data-stu-id="6b76e-109">To perform core feed-related tasks in the .NET client object model, you use the [SocialFeedManager](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.aspx) object.</span></span> <span data-ttu-id="6b76e-110">В этой статье мы покажем, как создать консольное приложение, с помощью клиентской объектной модели .NET для работы с социальными веб-каналами.</span><span class="sxs-lookup"><span data-stu-id="6b76e-110">In this article, we'll show you how to create a console application that uses the .NET client object model to work with social feeds.</span></span>
  
    
    
<span data-ttu-id="6b76e-111">Дополнительные сведения о работе с [SocialFeedManager](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.aspx) , а также сведения об использовании других API-интерфейсы для работы с социальными веб-каналами просмотрите [Работа с социальными веб-каналами в SharePoint](work-with-social-feeds-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="6b76e-111">For more information about working with  [SocialFeedManager](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.aspx) or for information about using other APIs to work with social feeds, see [Work with social feeds in SharePoint](work-with-social-feeds-in-sharepoint.md).</span></span>
  
    
    

## <a name="prerequisites-for-setting-up-your-development-environment-to-work-with-social-feeds-by-using-the-sharepoint-net-client-object-model"></a><span data-ttu-id="6b76e-112">Необходимые условия для настройки среды разработки для работы с социальными веб-каналами с помощью клиентской объектной модели SharePoint .NET</span><span class="sxs-lookup"><span data-stu-id="6b76e-112">Prerequisites for setting up your development environment to work with social feeds by using the SharePoint .NET client object model</span></span>
<span data-ttu-id="6b76e-113"><a name="bkmk_SetUpDevEnv"> </a></span><span class="sxs-lookup"><span data-stu-id="6b76e-113"><a name="bkmk_SetUpDevEnv"> </a></span></span>

<span data-ttu-id="6b76e-114">Создание консольного приложения, использующего клиентской объектной модели .NET для работы с социальными веб-каналов, то необходимо:</span><span class="sxs-lookup"><span data-stu-id="6b76e-114">To create a console application that uses the .NET client object model to work with social feeds, you'll need:</span></span>
  
    
    

- <span data-ttu-id="6b76e-115">SharePoint с личного сайта настроены, личные сайты, созданные для текущего пользователя и конечного пользователя, с текущим пользователем после конечного пользователя и несколько записей, записанные центром конечного пользователя</span><span class="sxs-lookup"><span data-stu-id="6b76e-115">SharePoint with My Site configured, with personal sites created for the current user and a target user, with the current user following the target user, and with a few posts written by the target user</span></span>
    
  
- <span data-ttu-id="6b76e-116">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="6b76e-116">Visual Studio 2012</span></span>
    
  
- <span data-ttu-id="6b76e-117">**Полный** доступ к приложению-службе профилей пользователей для пользователя, вошедшего в систему</span><span class="sxs-lookup"><span data-stu-id="6b76e-117">**Full Control** access permissions to the User Profile service application for the logged-on user</span></span>
    
  

> <span data-ttu-id="6b76e-118">**Примечание:** Если вы работаете не на компьютере, на котором работает SharePoint, загрузить [Клиентских компонентов SharePoint](http://www.microsoft.com/en-us/download/details.aspx?id=35585) , содержащий клиентскую сборку SharePoint.</span><span class="sxs-lookup"><span data-stu-id="6b76e-118">**Note:** If you are not developing on the computer that is running SharePoint, get the  [SharePoint Client Components](http://www.microsoft.com/en-us/download/details.aspx?id=35585) download that contains SharePoint client assemblies.</span></span>
  
    
    


## <a name="create-a-console-application-that-works-with-social-feeds-by-using-the-sharepoint-net-client-object-model"></a><span data-ttu-id="6b76e-119">Создание консольного приложения, работающего с социальными веб-каналами с помощью клиентской объектной модели SharePoint .NET</span><span class="sxs-lookup"><span data-stu-id="6b76e-119">Create a console application that works with social feeds by using the SharePoint .NET client object model</span></span>
<span data-ttu-id="6b76e-120"><a name="bk_createconsole"> </a></span><span class="sxs-lookup"><span data-stu-id="6b76e-120"><a name="bk_createconsole"> </a></span></span>


1. <span data-ttu-id="6b76e-121">Откройте Visual Studio и в меню **Файл** последовательно выберите элементы **Создать** и **Проект**.</span><span class="sxs-lookup"><span data-stu-id="6b76e-121">Open Visual Studio and choose **File**, **New**, **Project**.</span></span>
    
  
2. <span data-ttu-id="6b76e-122">В диалоговом окне **Новый проект** выберите **.NET Framework 4.5** из раскрывающегося списка в верхней части окна.</span><span class="sxs-lookup"><span data-stu-id="6b76e-122">In the **New Project** dialog box, choose **.NET Framework 4.5** from the drop-down list at the top of the dialog box.</span></span>
    
  
3. <span data-ttu-id="6b76e-123">В списке **шаблонов** выберите **Windows** и затем выберите шаблон **Консольное приложение**.</span><span class="sxs-lookup"><span data-stu-id="6b76e-123">In the **Templates** list, choose **Windows**, and then choose the **Console Application** template.</span></span>
    
  
4. <span data-ttu-id="6b76e-124">Назовите проект SocialFeedCSOMи затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="6b76e-124">Name the project SocialFeedCSOM, and then choose the **OK** button.</span></span>
    
  
5. <span data-ttu-id="6b76e-125">Добавьте ссылки на следующие сборки:</span><span class="sxs-lookup"><span data-stu-id="6b76e-125">Add references to the following assemblies:</span></span>
    
   - <span data-ttu-id="6b76e-126">**Microsoft.SharePoint.Client**</span><span class="sxs-lookup"><span data-stu-id="6b76e-126">**Microsoft.SharePoint.Client**</span></span>
   - <span data-ttu-id="6b76e-127">**Microsoft.SharePoint.ClientRuntime**</span><span class="sxs-lookup"><span data-stu-id="6b76e-127">**Microsoft.SharePoint.ClientRuntime**</span></span>
   - <span data-ttu-id="6b76e-128">**Microsoft.SharePoint.Client.UserProfiles**</span><span class="sxs-lookup"><span data-stu-id="6b76e-128">**Microsoft.SharePoint.Client.UserProfiles**</span></span>
  
6. <span data-ttu-id="6b76e-129">Замените содержимое класса **Program** в примере кода на класс из следующих сценариев:</span><span class="sxs-lookup"><span data-stu-id="6b76e-129">Replace the contents of the **Program** class with the code example from one of the following scenarios:</span></span>
    
   -  [<span data-ttu-id="6b76e-130">Публикация сообщения и ответы, которые социальные веб-канал</span><span class="sxs-lookup"><span data-stu-id="6b76e-130">Publish posts and replies to the social feed</span></span>](how-to-create-and-delete-posts-and-retrieve-the-social-feed-by-using-the-net-cli.md#bkmk_PubPosts) 
   -  [<span data-ttu-id="6b76e-131">Извлечение социальных веб-каналов</span><span class="sxs-lookup"><span data-stu-id="6b76e-131">Retrieve social feeds</span></span>](how-to-create-and-delete-posts-and-retrieve-the-social-feed-by-using-the-net-cli.md#bkmk_GetFeeds) 
   -  [<span data-ttu-id="6b76e-132">Удаление публикации и ответы из социальных канала</span><span class="sxs-lookup"><span data-stu-id="6b76e-132">Delete posts and replies from the social feed</span></span>](how-to-create-and-delete-posts-and-retrieve-the-social-feed-by-using-the-net-cli.md#bkmk_DeletePosts)
    
7. <span data-ttu-id="6b76e-133">Тестирование консольного приложения в строке меню выберите команду **Отладка**, **Начать отладку**.</span><span class="sxs-lookup"><span data-stu-id="6b76e-133">To test the console application, on the menu bar, choose **Debug**, **Start Debugging**.</span></span>
    
  

## <a name="code-example-publish-posts-and-replies-to-the-social-feed-by-using-the-sharepoint-net-client-object-model"></a><span data-ttu-id="6b76e-134">Пример кода: публикация публикации и ответы, которые социальных сетей канал с помощью клиентской объектной модели SharePoint .NET</span><span class="sxs-lookup"><span data-stu-id="6b76e-134">Code example: Publish posts and replies to the social feed by using the SharePoint .NET client object model</span></span>
<span data-ttu-id="6b76e-135"><a name="bkmk_PubPosts"> </a></span><span class="sxs-lookup"><span data-stu-id="6b76e-135"><a name="bkmk_PubPosts"> </a></span></span>

<span data-ttu-id="6b76e-p102">В следующем примере кода публикует сообщение и ответ от текущего пользователя. В нем показано, как:</span><span class="sxs-lookup"><span data-stu-id="6b76e-p102">The following code example publishes a post and a reply from the current user. It shows how to:</span></span>
  
    
    

- <span data-ttu-id="6b76e-p103">После определения содержимого. В этом примере ссылка в записи.</span><span class="sxs-lookup"><span data-stu-id="6b76e-p103">Define post content. This example includes a link in the post.</span></span>
    
  
- <span data-ttu-id="6b76e-140">Публикация post на канал для текущего пользователя, используя метод  [CreatePost](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.CreatePost.aspx) и передача **null** в качестве параметра _targetId_.</span><span class="sxs-lookup"><span data-stu-id="6b76e-140">Publish a post to the current user's feed by using the  [CreatePost](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.CreatePost.aspx) method and passing **null** as the _targetId_ parameter.</span></span>
    
  
- <span data-ttu-id="6b76e-141">Получите [тип веб-канал](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedType.aspx) **новостей** для текущего пользователя с помощью метода [GetFeed](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.GetFeed.aspx) .</span><span class="sxs-lookup"><span data-stu-id="6b76e-141">Get the **News** [feed type](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedType.aspx) for the current user by using the [GetFeed](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.GetFeed.aspx) method.</span></span>
    
  
- <span data-ttu-id="6b76e-142">Выполните итерацию по веб-канал для поиска всех потоков, которые могут быть дан ответ и для получения сведений о потоков и публикации.</span><span class="sxs-lookup"><span data-stu-id="6b76e-142">Iterate through the feed to find all threads that can be replied to and to get information about threads and posts.</span></span>
    
  
- <span data-ttu-id="6b76e-143">Ответ на публикацию с помощью метода  [CreatePost](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.CreatePost.aspx) , передав в качестве параметра _targetId_ идентификатор потока.</span><span class="sxs-lookup"><span data-stu-id="6b76e-143">Reply to a post by using the  [CreatePost](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.CreatePost.aspx) method and passing the thread identifier as the _targetId_ parameter.</span></span>
    
  

> <span data-ttu-id="6b76e-144">**Примечание:** Измените значение заполнитель для переменной **serverUrl** , прежде чем запускать код.</span><span class="sxs-lookup"><span data-stu-id="6b76e-144">**Note:** Change the placeholder value for the **serverUrl** variable before you run the code.</span></span>
  
    
    


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


## <a name="code-example-retrieve-social-feeds-by-using-the-sharepoint-net-client-object-model"></a><span data-ttu-id="6b76e-145">Пример кода: получение социальными веб-каналами с помощью клиентской объектной модели SharePoint .NET</span><span class="sxs-lookup"><span data-stu-id="6b76e-145">Code example: Retrieve social feeds by using the SharePoint .NET client object model</span></span>
<span data-ttu-id="6b76e-146"><a name="bkmk_GetFeeds"> </a></span><span class="sxs-lookup"><span data-stu-id="6b76e-146"><a name="bkmk_GetFeeds"> </a></span></span>

<span data-ttu-id="6b76e-p104">В следующем примере кода показано получение веб-каналов для текущего пользователя и конечного пользователя. В нем показано, как:</span><span class="sxs-lookup"><span data-stu-id="6b76e-p104">The following code example retrieves feeds for the current user and a target user. It shows how to:</span></span>
  
    
    

- <span data-ttu-id="6b76e-149">Получите **личный**, **Новости**и **временной шкалы**,[типы веб-канала](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedType.aspx) для текущего пользователя с помощью метода [GetFeed](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.GetFeed.aspx) .</span><span class="sxs-lookup"><span data-stu-id="6b76e-149">Get the **Personal**, **News**, and **Timeline**[feed types](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedType.aspx) for the current user by using the [GetFeed](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.GetFeed.aspx) method.</span></span>
    
  
- <span data-ttu-id="6b76e-150">Получение **личных** [веб-канала типа](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedType.Personal.aspx) для конечного пользователя с помощью метода [GetFeedFor](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.GetFeedFor.aspx) .</span><span class="sxs-lookup"><span data-stu-id="6b76e-150">Get the **Personal** [feed type](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedType.Personal.aspx) for a target user by using the [GetFeedFor](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.GetFeedFor.aspx) method.</span></span>
    
  
- <span data-ttu-id="6b76e-p105">Выполните итерацию по веб-каналы, чтобы найти все потоки, не являющиеся ссылку и для получения сведений о потоков и публикации. Справочник по потоков представляют уведомлений, которые содержат сведения о другого потока. Например, если пользователь упоминания другого пользователя в записи, сервера создает **MentionReference**-введите поток, который содержит ссылки на исходное сообщение и другие метаданные о post.</span><span class="sxs-lookup"><span data-stu-id="6b76e-p105">Iterate through the feeds to find all non-reference threads and to get information about threads and posts. Reference threads represent notifications that contain information about another thread. For example, if a user mentions someone in a post, the server generates a **MentionReference**-type thread that contains the link to the original post and other metadata about the post.</span></span>
    
  
<span data-ttu-id="6b76e-154">Дополнительные сведения о типах веб-канала активности можно [Обзор типов веб-канала активности](work-with-social-feeds-in-sharepoint.md#bkmk_FeedTypes).</span><span class="sxs-lookup"><span data-stu-id="6b76e-154">For more information about feed types, see  [Overview of feed types](work-with-social-feeds-in-sharepoint.md#bkmk_FeedTypes).</span></span> <span data-ttu-id="6b76e-155">Дополнительные сведения о потоках ссылку можно [ссылку потоки и потоки дайджест в веб-каналов социальных SharePoint](reference-threads-and-digest-threads-in-sharepoint-server-social-feeds.md).</span><span class="sxs-lookup"><span data-stu-id="6b76e-155">For more information about reference threads, see  [Reference threads and digest threads in SharePoint social feeds](reference-threads-and-digest-threads-in-sharepoint-server-social-feeds.md).</span></span>
  
    
    

> <span data-ttu-id="6b76e-156">**Примечание:** Изменение значений заполнитель для переменных **serverUrl** и **targetUser** , прежде чем запускать код.</span><span class="sxs-lookup"><span data-stu-id="6b76e-156">**Note:** Change the placeholder values for the **serverUrl** and **targetUser** variables before you run the code.</span></span>
  
    
    




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


## <a name="code-example-delete-posts-and-replies-from-the-social-feed-by-using-the-sharepoint-net-client-object-model"></a><span data-ttu-id="6b76e-157">Пример кода: Delete публикации и ответы из социальных канала с помощью клиентской объектной модели SharePoint .NET</span><span class="sxs-lookup"><span data-stu-id="6b76e-157">Code example: Delete posts and replies from the social feed by using the SharePoint .NET client object model</span></span>
<span data-ttu-id="6b76e-158"><a name="bkmk_DeletePosts"> </a></span><span class="sxs-lookup"><span data-stu-id="6b76e-158"><a name="bkmk_DeletePosts"> </a></span></span>

<span data-ttu-id="6b76e-p107">В следующем примере кода удаляет сообщение или ответ из личных веб-канал текущего пользователя. В нем показано, как:</span><span class="sxs-lookup"><span data-stu-id="6b76e-p107">The following code example deletes a post or a reply from the current user's personal feed. It shows how to:</span></span>
  
    
    

- <span data-ttu-id="6b76e-161">Получите **личных** [веб-канала типа](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedType.aspx) для текущего пользователя с помощью метода [GetFeed](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.GetFeed.aspx) .</span><span class="sxs-lookup"><span data-stu-id="6b76e-161">Get the **Personal** [feed type](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedType.aspx) for the current user by using the [GetFeed](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.GetFeed.aspx) method.</span></span>
    
  
- <span data-ttu-id="6b76e-162">Выполните итерацию по потоков в веб-канал для получения сведений о корневой публикации и ответы.</span><span class="sxs-lookup"><span data-stu-id="6b76e-162">Iterate through the threads in the feed to get information about the root post and replies.</span></span>
    
  
- <span data-ttu-id="6b76e-163">Удаление корневого post, ответ или потока с помощью метода  [DeletePost](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.DeletePost.aspx) (корневой post при удалении весь поток).</span><span class="sxs-lookup"><span data-stu-id="6b76e-163">Delete a root post, reply, or thread by using the  [DeletePost](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.DeletePost.aspx) method (deleting a root post deletes the whole thread).</span></span>
    
  

> <span data-ttu-id="6b76e-164">**Примечание:** Измените значение заполнитель для переменной **serverUrl** , прежде чем запускать код.</span><span class="sxs-lookup"><span data-stu-id="6b76e-164">**Note:** Change the placeholder value for the **serverUrl** variable before you run the code.</span></span>
  
    
    


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


## <a name="next-steps"></a><span data-ttu-id="6b76e-165">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6b76e-165">Next steps</span></span>
<span data-ttu-id="6b76e-166"><a name="bkmk_DeletePosts"> </a></span><span class="sxs-lookup"><span data-stu-id="6b76e-166"><a name="bkmk_DeletePosts"> </a></span></span>

 [<span data-ttu-id="6b76e-167">Как: Включение упоминания, теги и ссылки на сайты и документы в публикации в SharePoint</span><span class="sxs-lookup"><span data-stu-id="6b76e-167">How to: Include mentions, tags, and links to sites and documents in posts in SharePoint</span></span>](how-to-include-mentions-tags-and-links-to-sites-and-documents-in-posts-in-sharep.md)
  
    
    

## <a name="additional-resources"></a><span data-ttu-id="6b76e-168">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="6b76e-168">Additional resources</span></span>
<span data-ttu-id="6b76e-169"><a name="bk_addResources"> </a></span><span class="sxs-lookup"><span data-stu-id="6b76e-169"><a name="bk_addResources"> </a></span></span>


-  [<span data-ttu-id="6b76e-170">Работа с социальными веб-каналами в SharePoint</span><span class="sxs-lookup"><span data-stu-id="6b76e-170">Work with social feeds in SharePoint</span></span>](work-with-social-feeds-in-sharepoint.md)
    
  
-  [<span data-ttu-id="6b76e-171">Как: Создание и удаление сообщений и извлечение социальных веб-канал с помощью объектной модели JavaScript в SharePoint</span><span class="sxs-lookup"><span data-stu-id="6b76e-171">How to: Create and delete posts and retrieve the social feed by using the JavaScript object model in SharePoint</span></span>](how-to-create-and-delete-posts-and-retrieve-the-social-feed-by-using-the-javascr.md)
    
  
-  [<span data-ttu-id="6b76e-172">Как: сведения для чтения и записи социальных канал с помощью службы REST в SharePoint</span><span class="sxs-lookup"><span data-stu-id="6b76e-172">How to: Learn to read and write to the social feed by using the REST service in SharePoint</span></span>](how-to-learn-to-read-and-write-to-the-social-feed-by-using-the-rest-service-in-s.md)
    
  
-  [<span data-ttu-id="6b76e-173">Справочник по потоки и потоки дайджест в веб-каналов социальных SharePoint</span><span class="sxs-lookup"><span data-stu-id="6b76e-173">Reference threads and digest threads in SharePoint social feeds</span></span>](reference-threads-and-digest-threads-in-sharepoint-server-social-feeds.md)
    
  

