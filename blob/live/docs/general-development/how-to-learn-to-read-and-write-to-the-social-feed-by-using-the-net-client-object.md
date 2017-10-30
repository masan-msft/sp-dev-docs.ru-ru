---
title: "Как сведения для чтения и записи социальных канал, чтобы с помощью клиентской объектной модели .NET в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 3c15ede5-8a59-47e6-a0b2-c17ec6bf4ae1
ms.openlocfilehash: 52a67e44daccd4a9d86bb110f16f99da011e64ea
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-learn-to-read-and-write-to-the-social-feed-by-using-the-net-client-object-model-in-sharepoint"></a><span data-ttu-id="bd17a-102">Как: сведения для чтения и записи социальных канал, чтобы с помощью клиентской объектной модели .NET в SharePoint</span><span class="sxs-lookup"><span data-stu-id="bd17a-102">How to: Learn to read and write to the social feed by using the .NET client object model in SharePoint</span></span>
<span data-ttu-id="bd17a-103">Создайте консольное приложение, которое читает канал социальных сетей и пишет в него с помощью клиентской объектной модели .NET для SharePoint.</span><span class="sxs-lookup"><span data-stu-id="bd17a-103">Create a console application that reads and writes to the social feed by using the SharePoint .NET client object model.</span></span>
## <a name="prerequisites-for-creating-a-console-application-that-reads-and-writes-to-the-social-feed-by-using-the-sharepoint-net-client-object-model"></a><span data-ttu-id="bd17a-104">Необходимые условия для создания консольного приложения, которое считывает и записывает социальных канал, чтобы с помощью клиентской объектной модели SharePoint .NET</span><span class="sxs-lookup"><span data-stu-id="bd17a-104">Prerequisites for creating a console application that reads and writes to the social feed by using the SharePoint .NET client object model</span></span>
<span data-ttu-id="bd17a-105"><a name="bkmk_Prereqs"> </a></span><span class="sxs-lookup"><span data-stu-id="bd17a-105"><a name="bkmk_Prereqs"> </a></span></span>

<span data-ttu-id="bd17a-p101">Консольное приложение, которое вы создадите получает канал для конечного пользователя и печатает post корневой из каждого потока нумерованного списка. Затем публикует ответ простой текст для выбранного потока. Один и тот же метод ( [CreatePost](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.CreatePost.aspx) ) используется для публикации обоих публикации и ответы на канал.</span><span class="sxs-lookup"><span data-stu-id="bd17a-p101">The console application that you'll create retrieves a target user's feed and prints the root post from each thread in a numbered list. Then, it publishes a simple text reply to the selected thread. The same method ( [CreatePost](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.CreatePost.aspx) ) is used to publish both posts and replies to the feed.</span></span>
  
    
    
<span data-ttu-id="bd17a-109">Создание консольного приложения, необходимо следующее:</span><span class="sxs-lookup"><span data-stu-id="bd17a-109">To create the console application, you'll need the following:</span></span>
  
    
    

- <span data-ttu-id="bd17a-110">SharePoint настроен личного сайта, личные сайты, созданные для текущего пользователя и конечного пользователя и несколько записей, записанные центром конечного пользователя</span><span class="sxs-lookup"><span data-stu-id="bd17a-110">SharePoint with My Site configured, with personal sites created for the current user and a target user, and with a few posts written by the target user</span></span>
    
  
- <span data-ttu-id="bd17a-111">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="bd17a-111">Visual Studio 2012</span></span>
    
  
- <span data-ttu-id="bd17a-112">**Полный** доступ к приложению-службе профилей пользователей для пользователя, вошедшего в систему</span><span class="sxs-lookup"><span data-stu-id="bd17a-112">**Full Control** access permissions to the User Profile service application for the logged-on user</span></span>
    
  

> <span data-ttu-id="bd17a-113">**Примечание:** При разработке не на компьютере, на котором работает SharePoint, загрузить [Клиентские компоненты SharePoint](http://www.microsoft.com/en-us/download/details.aspx?id=35585) , содержащий клиентскую сборку SharePoint.</span><span class="sxs-lookup"><span data-stu-id="bd17a-113">**Note:** If you're not developing on the computer that is running SharePoint, get the  [SharePoint Client Components](http://www.microsoft.com/en-us/download/details.aspx?id=35585) download that contains SharePoint client assemblies.</span></span>
  
    
    


### <a name="core-concepts-to-know-about-working-with-sharepoint-social-feeds"></a><span data-ttu-id="bd17a-114">Основные сведения о работе с социальными веб-каналами SharePoint</span><span class="sxs-lookup"><span data-stu-id="bd17a-114">Core concepts to know about working with SharePoint social feeds</span></span>
<span data-ttu-id="bd17a-115"><a name="bkmk_CoreConcepts"> </a></span><span class="sxs-lookup"><span data-stu-id="bd17a-115"><a name="bkmk_CoreConcepts"> </a></span></span>

<span data-ttu-id="bd17a-116">В таблице 1 приведены ссылки на статьи, в которых описываются основные понятия, которые нужно знать перед началом работы.</span><span class="sxs-lookup"><span data-stu-id="bd17a-116">Table 1 contains links to articles that describe core concepts you should know before you get started.</span></span>
  
    
    

<span data-ttu-id="bd17a-117">**В таблице 1. Основные понятия по работе с социальными веб-каналами SharePoint**</span><span class="sxs-lookup"><span data-stu-id="bd17a-117">**Table 1. Core concepts for working with SharePoint social feeds**</span></span>


|<span data-ttu-id="bd17a-118">**Название статьи**</span><span class="sxs-lookup"><span data-stu-id="bd17a-118">**Article title**</span></span>|<span data-ttu-id="bd17a-119">**Описание**</span><span class="sxs-lookup"><span data-stu-id="bd17a-119">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="bd17a-120">Начало разработки с использованием социальных функций в SharePoint</span><span class="sxs-lookup"><span data-stu-id="bd17a-120">Get started developing with social features in SharePoint</span></span>](get-started-developing-with-social-features-in-sharepoint.md) <br/> |<span data-ttu-id="bd17a-121">Узнайте, как приступить к программированию с социальными веб-каналов и микроблога публикации, следуя людей и содержимое (документы, сайты и tags.md) и работа с профилями пользователей.</span><span class="sxs-lookup"><span data-stu-id="bd17a-121">Find out how to get started programming with social feeds and microblog posts, following people and content (documents, sites, and tags.md), and working with user profiles.</span></span>  <br/> |
| [<span data-ttu-id="bd17a-122">Работа с социальными веб-каналами в SharePoint</span><span class="sxs-lookup"><span data-stu-id="bd17a-122">Work with social feeds in SharePoint</span></span>](work-with-social-feeds-in-sharepoint.md) <br/> |<span data-ttu-id="bd17a-123">Сведения о распространенных задач программирования по работе с социальными веб-каналов и API, которое используется для выполнения задачи.</span><span class="sxs-lookup"><span data-stu-id="bd17a-123">Learn about common programming tasks for working with social feeds and the API that you use to perform the tasks.</span></span>  <br/> |
   

## <a name="create-the-console-application-in-visual-studio-2012-and-add-references-to-client-assemblies"></a><span data-ttu-id="bd17a-124">Создание консольного приложения в Visual Studio 2012 и добавление ссылок на сборки клиента</span><span class="sxs-lookup"><span data-stu-id="bd17a-124">Create the console application in Visual Studio 2012 and add references to client assemblies</span></span>
<span data-ttu-id="bd17a-125"><a name="bkmk_CreateApp"> </a></span><span class="sxs-lookup"><span data-stu-id="bd17a-125"><a name="bkmk_CreateApp"> </a></span></span>


1. <span data-ttu-id="bd17a-126">Откройте Visual Studio 2012 на компьютере разработчика.</span><span class="sxs-lookup"><span data-stu-id="bd17a-126">On your development computer, open Visual Studio 2012.</span></span>
    
  
2. <span data-ttu-id="bd17a-127">В строке меню выберите пункты **Файл**, **Создать** и **Проект**.</span><span class="sxs-lookup"><span data-stu-id="bd17a-127">On the menu bar, choose **File**, **New**, **Project**.</span></span>
    
  
3. <span data-ttu-id="bd17a-128">В верхней части диалогового окна **Новый проект** выберите **.NET Framework 4.5** в раскрывающемся списке.</span><span class="sxs-lookup"><span data-stu-id="bd17a-128">In the **New Project** dialog box, choose **.NET Framework 4.5** from the drop-down list at the top of the dialog box.</span></span>
    
  
4. <span data-ttu-id="bd17a-129">В списке **шаблонов** выберите **Windows** и затем выберите шаблон **Консольное приложение**.</span><span class="sxs-lookup"><span data-stu-id="bd17a-129">From the **Templates** list, choose **Windows**, and then choose the **Console Application** template.</span></span>
    
  
5. <span data-ttu-id="bd17a-130">Назовите проект ReadWriteMySiteи затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="bd17a-130">Name the project ReadWriteMySite, and then choose the **OK** button.</span></span>
    
  
6. <span data-ttu-id="bd17a-131">Добавление ссылки на сборки клиента следующим образом:</span><span class="sxs-lookup"><span data-stu-id="bd17a-131">Add references to the client assemblies, as follows:</span></span>
    
   <span data-ttu-id="bd17a-132">А.</span><span class="sxs-lookup"><span data-stu-id="bd17a-132">a.</span></span> <span data-ttu-id="bd17a-133">В **Обозревателе решений** откройте контекстное меню для проекта **ReadWriteMySite** и затем выберите команду **Добавить ссылку**.</span><span class="sxs-lookup"><span data-stu-id="bd17a-133">In **Solution Explorer**, open the shortcut menu for the **ReadWriteMySite** project, and then choose **Add Reference**.</span></span>
  
   <span data-ttu-id="bd17a-134">Б.</span><span class="sxs-lookup"><span data-stu-id="bd17a-134">b.</span></span> <span data-ttu-id="bd17a-135">В диалоговом окне **Диспетчер ссылок** выберите следующие сборки:</span><span class="sxs-lookup"><span data-stu-id="bd17a-135">In the **Reference Manager** dialog box, choose the following assemblies:</span></span>
    
     - <span data-ttu-id="bd17a-136">**Microsoft.SharePoint.Client**</span><span class="sxs-lookup"><span data-stu-id="bd17a-136">**Microsoft.SharePoint.Client**</span></span>
    
     - <span data-ttu-id="bd17a-137">**Microsoft.SharePoint.Client.Runtime**</span><span class="sxs-lookup"><span data-stu-id="bd17a-137">**Microsoft.SharePoint.Client.Runtime**</span></span>
    
     - <span data-ttu-id="bd17a-138">**Microsoft.SharePoint.Client.UserProfiles**</span><span class="sxs-lookup"><span data-stu-id="bd17a-138">**Microsoft.SharePoint.Client.UserProfiles**</span></span>  

   <span data-ttu-id="bd17a-139">Если вы работаете на компьютере, на котором работает SharePoint, сборки находятся в категории **расширения** .</span><span class="sxs-lookup"><span data-stu-id="bd17a-139">If you are developing on the computer that is running SharePoint, the assemblies are in the **Extensions** category.</span></span> <span data-ttu-id="bd17a-140">В противном случае перейдите к папке, которая имеет клиентских сборок, загруженный (см [Клиентских компонентов SharePoint](http://www.microsoft.com/downloads/details.aspx?FamilyID=66da4a3e-e3b0-45d9-9e84-a84946fbf239)).</span><span class="sxs-lookup"><span data-stu-id="bd17a-140">Otherwise, browse to the location that has the client assemblies you downloaded (see [SharePoint Client Components](http://www.microsoft.com/downloads/details.aspx?FamilyID=66da4a3e-e3b0-45d9-9e84-a84946fbf239)).</span></span>
    
  
7. <span data-ttu-id="bd17a-141">В файле Program.cs добавьте следующие инструкции **using**.</span><span class="sxs-lookup"><span data-stu-id="bd17a-141">In the Program.cs file, add the following **using** statements.</span></span>
    
```cs
using Microsoft.SharePoint.Client;
using Microsoft.SharePoint.Client.Social;
```


## <a name="retrieve-the-social-feed-for-a-target-user-by-using-the-sharepoint-net-client-object-model"></a><span data-ttu-id="bd17a-142">Извлечение социальных веб-канал для конечного пользователя с помощью клиентской объектной модели SharePoint .NET</span><span class="sxs-lookup"><span data-stu-id="bd17a-142">Retrieve the social feed for a target user by using the SharePoint .NET client object model</span></span>
<span data-ttu-id="bd17a-143"><a name="bkmk_RetrieveFeed"> </a></span><span class="sxs-lookup"><span data-stu-id="bd17a-143"></span></span>


1. <span data-ttu-id="bd17a-144">Объявите переменные для URL-адрес сервера и создания решений учетные данные учетной записи пользователя.</span><span class="sxs-lookup"><span data-stu-id="bd17a-144">Declare variables for the server URL and target user's account credentials.</span></span>
    
```cs
const string serverUrl = "http://serverName/";
const string targetUser = "domainName\\userName";
```

   > <span data-ttu-id="bd17a-145">**Примечание:** Не забудьте заменить `http://serverName/` и `domainName\\userName` заполнитель значения, прежде чем запускать код.</span><span class="sxs-lookup"><span data-stu-id="bd17a-145">**Note:** Remember to replace the  `http://serverName/` and `domainName\\userName` placeholder values before you run the code.</span></span>
   
2. <span data-ttu-id="bd17a-146">В методе **Main** инициализации контекста клиента SharePoint.</span><span class="sxs-lookup"><span data-stu-id="bd17a-146">In the **Main** method, initialize the SharePoint client context.</span></span>
    
```cs
ClientContext clientContext = new ClientContext(serverUrl);
```

3. <span data-ttu-id="bd17a-147">Создайте экземпляр  [SocialFeedManager](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.aspx) .</span><span class="sxs-lookup"><span data-stu-id="bd17a-147">Create the  [SocialFeedManager](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.aspx) instance.</span></span>
    
```cs
SocialFeedManager feedManager = new SocialFeedManager(clientContext);
```

4. <span data-ttu-id="bd17a-148">Задание параметров для веб-канала активности контент, который требуется получить.</span><span class="sxs-lookup"><span data-stu-id="bd17a-148">Specify the parameters for the feed content that you want to retrieve.</span></span>
    
```cs
  SocialFeedOptions feedOptions = new SocialFeedOptions();
feedOptions.MaxThreadCount = 10;
```

    The default options return the first 20 threads in the feed, sorted by last modified date.
  
5. <span data-ttu-id="bd17a-149">Получите конечного пользователя веб-канал.</span><span class="sxs-lookup"><span data-stu-id="bd17a-149">Get the target user's feed.</span></span>
    
```cs 
ClientResult<SocialFeed> feed = feedManager.GetFeedFor(targetUser, feedOptions);
clientContext.ExecuteQuery();
```

     [GetFeedFor](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.GetFeedFor.aspx) returns a **ClientResult<T>** object that stores the collection of threads in its [Value](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.ClientResult`1.Value.aspx) property.
    
  

## <a name="iterate-through-and-read-from-the-social-feed-by-using-the-sharepoint-net-client-object-model"></a><span data-ttu-id="bd17a-150">Выполните итерацию по и ознакомьтесь с социальными веб-канал с помощью клиентской объектной модели SharePoint .NET</span><span class="sxs-lookup"><span data-stu-id="bd17a-150">Iterate through and read from the social feed by using the SharePoint .NET client object model</span></span>
<span data-ttu-id="bd17a-151"><a name="bkmk_ReadFeed"> </a></span><span class="sxs-lookup"><span data-stu-id="bd17a-151"></span></span>

<span data-ttu-id="bd17a-p105">Приведенный ниже код перебирает потоков в веб-канал. Проверяется, является ли каждый поток имеет атрибут  [CanReply](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThreadAttributes.CanReply.aspx) и затем получает идентификатор потока и текста post корневой. Код также создает словарь для хранения идентификатор потока (который используется для ответов на поток) и записывает текста post корневой на консоль.</span><span class="sxs-lookup"><span data-stu-id="bd17a-p105">The following code iterates through the threads in the feed. It checks whether each thread has the  [CanReply](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThreadAttributes.CanReply.aspx) attribute and then gets the thread identifier and the text of the root post. The code also creates a dictionary to store the thread identifier (which is used to reply to a thread) and writes the text of the root post to the console.</span></span>

```cs
Dictionary<int, string> idDictionary = new Dictionary<int, string>();
for (int i = 0; i < feed.Value.Threads.Length; i++)
{
    SocialThread thread = feed.Value.Threads[i];
    string postText = thread.RootPost.Text;
    if (thread.Attributes.HasFlag(SocialThreadAttributes.CanReply))
    {
        idDictionary.Add(i, thread.Id);
        Console.WriteLine("\\t" + (i + 1) + ". " + postText);
    }
}
```


## <a name="post-a-reply-to-the-social-feed-by-using-the-sharepoint-net-client-object-model"></a><span data-ttu-id="bd17a-155">Ответить социальные веб-канал с помощью клиента SharePoint .NET объектной модели</span><span class="sxs-lookup"><span data-stu-id="bd17a-155">Post a reply to the social feed by using the SharePoint .NET client object model</span></span>
<span data-ttu-id="bd17a-156"><a name="bkmk_WriteFeed"> </a></span><span class="sxs-lookup"><span data-stu-id="bd17a-156"></span></span>


1. <span data-ttu-id="bd17a-157">(Связанные с Интерфейсом только) Получите поток для ответов, чтобы и запрос ответа пользователя.</span><span class="sxs-lookup"><span data-stu-id="bd17a-157">(UI-related only) Get the thread to reply to and prompt for the user's reply.</span></span>
    
```cs
Console.Write("Which post number do you want to reply to?  ");
string threadToReplyTo = "";
int threadNumber = int.Parse(Console.ReadLine()) - 1;
idDictionary.TryGetValue(threadNumber, out threadToReplyTo);
Console.Write("Type your reply:  ");
```

2. <span data-ttu-id="bd17a-p106">Определите ответ. Следующий код получает текст ответа из консольного приложения.</span><span class="sxs-lookup"><span data-stu-id="bd17a-p106">Define the reply. The following code gets the reply's text from the console application.</span></span>
    
```cs
SocialPostCreationData postCreationData = new SocialPostCreationData();
postCreationData.ContentText = Console.ReadLine();
```

3. <span data-ttu-id="bd17a-p107">Публикация ответ. Параметр  _threadToReplyTo_ представляет свойства [Id](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThread.Id.aspx) потока.</span><span class="sxs-lookup"><span data-stu-id="bd17a-p107">Publish the reply. The  _threadToReplyTo_ parameter represents of the thread's [Id](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThread.Id.aspx) property.</span></span>
    
```cs
feedManager.CreatePost(threadToReplyTo, postCreationData);
clientContext.ExecuteQuery();
```

   > <span data-ttu-id="bd17a-162">**Примечание:** Метод [CreatePost](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.CreatePost.aspx) также используется для публикации корневого post для текущего пользователя веб-канал, передав **значение null** для первого параметра.</span><span class="sxs-lookup"><span data-stu-id="bd17a-162">**Note:** The  [CreatePost](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.CreatePost.aspx) method is also used to publish a root post to the current user's feed by passing **null** for the first parameter.</span></span>
4. <span data-ttu-id="bd17a-163">(Связанные с Интерфейсом только) Выйти из программы.</span><span class="sxs-lookup"><span data-stu-id="bd17a-163">(UI-related only) Exit the program.</span></span>
    
```cs
Console.WriteLine("Your reply was published.");
Console.ReadKey(false);
```

5. <span data-ttu-id="bd17a-164">Тестирование консольного приложения в строке меню выберите команду **Отладка**, **Начать отладку**.</span><span class="sxs-lookup"><span data-stu-id="bd17a-164">To test the console application, on the menu bar, choose **Debug**, **Start Debugging**.</span></span>
    
  

## <a name="code-example-retrieve-a-feed-and-reply-to-a-post-by-using-the-sharepoint-net-client-object-model"></a><span data-ttu-id="bd17a-165">Пример кода: получение веб-канал и ответить на сообщение с помощью клиентской объектной модели SharePoint .NET</span><span class="sxs-lookup"><span data-stu-id="bd17a-165">Code example: Retrieve a feed and reply to a post by using the SharePoint .NET client object model</span></span>
<span data-ttu-id="bd17a-166"><a name="bkmk_CodeExample"> </a></span><span class="sxs-lookup"><span data-stu-id="bd17a-166"></span></span>

<span data-ttu-id="bd17a-167">Следующий пример является полный код из файла Program.cs.</span><span class="sxs-lookup"><span data-stu-id="bd17a-167">The following example is the complete code from the Program.cs file.</span></span>
  
```cs
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Microsoft.SharePoint.Client;
using Microsoft.SharePoint.Client.Social;

namespace ReadWriteMySite
{
    class Program
    {
        static void Main(string[] args)
        {

            // Replace the following placeholder values with the target server running SharePoint and the
            // target thread owner.
            const string serverUrl = "http://serverName/";
            const string targetUser = "domainName\\userName";

            // Connect to the client context.
            ClientContext clientContext = new ClientContext(serverUrl);

            // Get the SocialFeedManager instance.
            SocialFeedManager feedManager = new SocialFeedManager(clientContext);

            // Specify the parameters for the feed content that you want to retrieve.
            SocialFeedOptions feedOptions = new SocialFeedOptions();
            feedOptions.MaxThreadCount = 10;

            // Get the target owner's feed (posts and activities) and then run the request on the server.
            ClientResult<SocialFeed> feed = feedManager.GetFeedFor(targetUser, feedOptions);
            clientContext.ExecuteQuery();

            // Create a dictionary to store the Id property of each thread. This code example stores
            // the ID so a user can select a thread to reply to from the console application.
            Dictionary<int, string> idDictionary = new Dictionary<int, string>();
            for (int i = 0; i < feed.Value.Threads.Length; i++)
            {
                SocialThread thread = feed.Value.Threads[i];

                // Keep only the threads that can be replied to.
                if (thread.Attributes.HasFlag(SocialThreadAttributes.CanReply))
                {
                    idDictionary.Add(i, thread.Id);

                    // Write out the text of the post.
                    Console.WriteLine("\\t" + (i + 1) + ". " + thread.RootPost.Text);
                }
            }
            Console.Write("Which post number do you want to reply to?  ");

            string threadToReplyTo = "";
            int threadNumber = int.Parse(Console.ReadLine()) - 1;
            idDictionary.TryGetValue(threadNumber, out threadToReplyTo);

            Console.Write("Type your reply:  ");

            // Define properties for the reply.
            SocialPostCreationData postCreationData = new SocialPostCreationData();
            postCreationData.ContentText = Console.ReadLine();
            
            // Post the reply and make the changes on the server.
            feedManager.CreatePost(threadToReplyTo, postCreationData);
            clientContext.ExecuteQuery();

            Console.WriteLine("Your reply was published.");
            Console.ReadKey(false);

            // TODO: Add error handling and input validation.
        }
    }
}
```


## <a name="next-steps"></a><span data-ttu-id="bd17a-168">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="bd17a-168">Next steps</span></span>
<span data-ttu-id="bd17a-169"><a name="SP15ReadWriteSocial_nextsteps"> </a></span><span class="sxs-lookup"><span data-stu-id="bd17a-169"></span></span>

<span data-ttu-id="bd17a-170">Чтобы узнать, как для более чтения задачи и записи задач с социальными веб-канал с помощью клиентской объектной модели .NET, см.:</span><span class="sxs-lookup"><span data-stu-id="bd17a-170">To learn how to do more read tasks and write tasks with the social feed by using the .NET client object model, see the following:</span></span>
  
    
    

-  [<span data-ttu-id="bd17a-171">Как: Создание и удаление сообщений и извлечение социальных веб-канал с помощью клиентской объектной модели .NET в SharePoint</span><span class="sxs-lookup"><span data-stu-id="bd17a-171">How to: Create and delete posts and retrieve the social feed by using the .NET client object model in SharePoint</span></span>](how-to-create-and-delete-posts-and-retrieve-the-social-feed-by-using-the-net-cli.md)
    
  

## <a name="additional-resources"></a><span data-ttu-id="bd17a-172">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="bd17a-172">Additional resources</span></span>
<span data-ttu-id="bd17a-173"><a name="SP15ReadWriteSocial_addlresources"> </a></span><span class="sxs-lookup"><span data-stu-id="bd17a-173"></span></span>


-  [<span data-ttu-id="bd17a-174">Начало разработки с использованием социальных функций в SharePoint</span><span class="sxs-lookup"><span data-stu-id="bd17a-174">Get started developing with social features in SharePoint</span></span>](get-started-developing-with-social-features-in-sharepoint.md)
    
  
-  [<span data-ttu-id="bd17a-175">Работа с социальными веб-каналами в SharePoint</span><span class="sxs-lookup"><span data-stu-id="bd17a-175">Work with social feeds in SharePoint</span></span>](work-with-social-feeds-in-sharepoint.md)
    
  

