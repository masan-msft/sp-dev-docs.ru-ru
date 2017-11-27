---
title: "Выполните указанные документы и веб-узлы с помощью клиентской объектной модели .NET в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 84366e01-4961-459d-8109-2f1d2d714353
ms.openlocfilehash: 6e6690c40b37b65fe58100f7412e68ee827a970e
ms.sourcegitcommit: f6ea922341c38e700d0697961f8df9a454a03cba
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/15/2017
---
# <a name="follow-documents-and-sites-by-using-the-net-client-object-model-in-sharepoint"></a><span data-ttu-id="67120-102">Выполните указанные документы и веб-узлы с помощью клиентской объектной модели .NET в SharePoint</span><span class="sxs-lookup"><span data-stu-id="67120-102">Follow documents and sites by using the .NET client object model in SharePoint</span></span>

<span data-ttu-id="67120-103">Узнайте, как подписываться на контент, используя клиентскую объектную модель .NET в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="67120-103">Learn how to work with Following Content features by using the SharePoint .NET client object model.</span></span>

## <a name="how-do-i-use-the-net-client-object-model-to-follow-content"></a><span data-ttu-id="67120-104">Использование клиентской объектной модели .NET для подписка на контент</span><span class="sxs-lookup"><span data-stu-id="67120-104">How do I use the .NET client object model to follow content?</span></span>
<span data-ttu-id="67120-105"><a name="bk_intro"> </a></span><span class="sxs-lookup"><span data-stu-id="67120-105"><a name="bk_intro"> </a></span></span>

<span data-ttu-id="67120-106">Пользователи SharePoint можно следовать документы, сайты, и теги можно следовать документы, сайты и теги для получения обновлений об элементах в свои каналы новостей и быстро открыть число документов и сайтов.</span><span class="sxs-lookup"><span data-stu-id="67120-106">SharePoint users can follow documents, sites, and tags can follow documents, sites, and tags to get updates about the items in their newsfeeds and to quickly open followed documents and sites.</span></span> <span data-ttu-id="67120-107">Клиентская объектная модель .NET можно использовать в вашем приложении или решение, которое требуется запустить следующие материалы, остановите следующие материалы и получить отслеживаемого содержимого от имени текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="67120-107">You can use the .NET client object model in your app or solution to start following content, stop following content, and get followed content on behalf of the current user.</span></span> <span data-ttu-id="67120-108">В этой статье описывается создание консольного приложения, использующего клиентской объектной модели .NET для работы с контента следующие функции для документов и сайтов.</span><span class="sxs-lookup"><span data-stu-id="67120-108">This article shows you how to create a console application that uses the .NET client object model to work with Following Content features for documents and sites.</span></span>
  
    
    
<span data-ttu-id="67120-109">Основные интерфейсы API для контента следующие задачи являются следующие объекты:</span><span class="sxs-lookup"><span data-stu-id="67120-109">The following objects are the primary APIs for Following Content tasks:</span></span>
  
    
    

-  <span data-ttu-id="67120-110">[SocialFollowingManager](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.aspx) предоставляет методы для управления пользовательского списка число субъектов.</span><span class="sxs-lookup"><span data-stu-id="67120-110">[SocialFollowingManager](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.aspx) provides methods for managing a user's list of followed actors.</span></span>
    
  
-  <span data-ttu-id="67120-111">[SocialActor](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialActor.aspx) представляет документ, сайта или тег, сервер возвращает в ответ на запрос на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="67120-111">[SocialActor](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialActor.aspx) represents a document, site, or tag that the server returns in response to a client-side request.</span></span>
    
  
-  <span data-ttu-id="67120-112">[SocialActorInfo](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialActorInfo.aspx) указывает документ, сайта или тега в запросах со стороны клиента к серверу.</span><span class="sxs-lookup"><span data-stu-id="67120-112">[SocialActorInfo](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialActorInfo.aspx) specifies a document, site, or tag in client-side requests to the server.</span></span>
    
  
-  <span data-ttu-id="67120-113">[Microsoft.SharePoint.Client.Social.SocialActorType](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialActorType.aspx) и [Microsoft.SharePoint.Client.Social.SocialActorTypes](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialActorTypes.aspx) укажите типы контента в запросах со стороны клиента к серверу.</span><span class="sxs-lookup"><span data-stu-id="67120-113">[Microsoft.SharePoint.Client.Social.SocialActorType](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialActorType.aspx) and [Microsoft.SharePoint.Client.Social.SocialActorTypes](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialActorTypes.aspx) specify content types in client-side requests to the server.</span></span>
    
  

> <span data-ttu-id="67120-114">**Примечание:** Также использовать эти API-интерфейсы для задачи следующие сотрудники, но **GetSuggestions** и **GetFollowers** методы, доступные из поддерживают только [SocialFollowingManager](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.aspx) , отслеживаемые пользователи не контента.</span><span class="sxs-lookup"><span data-stu-id="67120-114">**Note:** You also use these APIs for Following People tasks, but the **GetSuggestions** and **GetFollowers** methods available from [SocialFollowingManager](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.aspx) only support following people, not content.</span></span> <span data-ttu-id="67120-115">Дополнительные сведения об использовании [SocialFollowingManager](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.aspx) можно [Подписка на контент в SharePoint](follow-content-in-sharepoint.md) и [Подписка на людей в SharePoint](follow-people-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="67120-115">For more information about how you can use [SocialFollowingManager](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.aspx) , see [Follow content in SharePoint](follow-content-in-sharepoint.md) and [Follow people in SharePoint](follow-people-in-sharepoint.md).</span></span> <span data-ttu-id="67120-116">Примеры кода, показывающие, как следить за людьми, в разделе [как: подписка на людей с помощью клиентской объектной модели .NET в SharePoint](how-to-follow-people-by-using-the-net-client-object-model-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="67120-116">For code examples that show how to follow people, see  [How to: Follow people by using the .NET client object model in SharePoint](how-to-follow-people-by-using-the-net-client-object-model-in-sharepoint.md).</span></span> 
  
    
    


## <a name="prerequisites-for-setting-up-your-development-environment-to-work-with-following-content-features-by-using-the-sharepoint-net-client-object-model"></a><span data-ttu-id="67120-117">Необходимые условия для настройки среды разработки для работы с возможности следующие содержимого с помощью клиентской объектной модели SharePoint .NET</span><span class="sxs-lookup"><span data-stu-id="67120-117">Prerequisites for setting up your development environment to work with Following Content features by using the SharePoint .NET client object model</span></span>
<span data-ttu-id="67120-118"><a name="bkmk_SetUpDevEnv"> </a></span><span class="sxs-lookup"><span data-stu-id="67120-118"><a name="bkmk_SetUpDevEnv"> </a></span></span>

<span data-ttu-id="67120-119">Создание консольного приложения, использующего клиентской объектной модели .NET для работы с контента следующие функции для документов и сайты, необходимо следующее:</span><span class="sxs-lookup"><span data-stu-id="67120-119">To create a console application that uses the .NET client object model to work with Following Content features for documents and sites, you'll need the following:</span></span>
  
    
    

- <span data-ttu-id="67120-120">Настройки SharePoint с помощью личных сайтов, с помощью узла личных сайтов, созданных для текущего пользователя и с документом, загруженные в библиотеку документов SharePoint</span><span class="sxs-lookup"><span data-stu-id="67120-120">SharePoint with My Site configured, with the My Site site created for the current user, and with a document uploaded to a SharePoint document library</span></span>
    
  
- <span data-ttu-id="67120-121">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="67120-121">Visual Studio 2012</span></span>
    
  
- <span data-ttu-id="67120-122">**Полный** доступ к приложению-службе профилей пользователей для пользователя, вошедшего в систему</span><span class="sxs-lookup"><span data-stu-id="67120-122">**Full Control** access permissions to the User Profile service application for the logged-on user</span></span>
    
  

> <span data-ttu-id="67120-123">**Примечание:** Если вы работаете не на компьютере, на котором работает SharePoint, загрузить [Клиентских компонентов SharePoint](http://www.microsoft.com/en-us/download/details.aspx?id=35585) , содержащий клиентскую сборку SharePoint.</span><span class="sxs-lookup"><span data-stu-id="67120-123">**Note:** If you are not developing on the computer that is running SharePoint, get the  [SharePoint Client Components](http://www.microsoft.com/en-us/download/details.aspx?id=35585) download that contains SharePoint client assemblies.</span></span>
  
    
    


## <a name="create-a-console-application-to-work-with-following-content-features-by-using-the-sharepoint-net-client-object-model"></a><span data-ttu-id="67120-124">Создание консольного приложения для работы с возможности следующие содержимого с помощью клиентской объектной модели SharePoint .NET</span><span class="sxs-lookup"><span data-stu-id="67120-124">Create a console application to work with Following Content features by using the SharePoint .NET client object model</span></span>
<span data-ttu-id="67120-125"><a name="bkmk_CreateConsoleApp"> </a></span><span class="sxs-lookup"><span data-stu-id="67120-125"><a name="bkmk_CreateConsoleApp"> </a></span></span>


1. <span data-ttu-id="67120-126">В меню Visual Studio выберите пункт **Файл**, **Создать**, затем **Проект**.</span><span class="sxs-lookup"><span data-stu-id="67120-126">In Visual Studio, choose **File**, **New**, **Project**.</span></span>
    
  
2. <span data-ttu-id="67120-127">В верхней части диалогового окна **Новый проект** выберите **.NET Framework 4.5** в раскрывающемся списке.</span><span class="sxs-lookup"><span data-stu-id="67120-127">In the **New Project** dialog box, choose **.NET Framework 4.5** from the drop-down list at the top of the dialog box.</span></span>
    
  
3. <span data-ttu-id="67120-128">В списке **шаблонов** выберите **Windows** и затем выберите шаблон **Консольное приложение**.</span><span class="sxs-lookup"><span data-stu-id="67120-128">In the **Templates** list, choose **Windows**, and then choose the **Console Application** template.</span></span>
    
  
4. <span data-ttu-id="67120-129">Назовите проект FollowContentCSOMи затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="67120-129">Name the project FollowContentCSOM, and then choose the **OK** button.</span></span>
    
  
5. <span data-ttu-id="67120-130">Добавьте ссылки на следующие сборки:</span><span class="sxs-lookup"><span data-stu-id="67120-130">Add references to the following assemblies:</span></span>
    
  - <span data-ttu-id="67120-131">**Microsoft.SharePoint.Client**</span><span class="sxs-lookup"><span data-stu-id="67120-131">**Microsoft.SharePoint.Client**</span></span>   
  - <span data-ttu-id="67120-132">**Microsoft.SharePoint.ClientRuntime**</span><span class="sxs-lookup"><span data-stu-id="67120-132">**Microsoft.SharePoint.ClientRuntime**</span></span>
  - <span data-ttu-id="67120-133">**Microsoft.SharePoint.Client.UserProfiles**</span><span class="sxs-lookup"><span data-stu-id="67120-133">**Microsoft.SharePoint.Client.UserProfiles**</span></span>
    
6. <span data-ttu-id="67120-134">Замените содержимое класса **Program** в примере кода на класс из следующих сценариев:</span><span class="sxs-lookup"><span data-stu-id="67120-134">Replace the contents of the **Program** class with the code example from one of the following scenarios:</span></span>
    
  -  [<span data-ttu-id="67120-135">Запуск и остановка следующие материалы</span><span class="sxs-lookup"><span data-stu-id="67120-135">Start and stop following content</span></span>](how-to-follow-documents-and-sites-by-using-the-net-client-object-model-in-sharep.md#bkmk_FollowContent)  
  -  [<span data-ttu-id="67120-136">Получение контента для текущего пользователя</span><span class="sxs-lookup"><span data-stu-id="67120-136">Get followed content for the current user</span></span>](how-to-follow-documents-and-sites-by-using-the-net-client-object-model-in-sharep.md#bkmk_GetFollowed)
    
7. <span data-ttu-id="67120-137">Тестирование консольного приложения в строке меню выберите команду **Отладка**, **Начать отладку**.</span><span class="sxs-lookup"><span data-stu-id="67120-137">To test the console application, on the menu bar, choose **Debug**, **Start Debugging**.</span></span>
    
  

## <a name="code-example-start-and-stop-following-content-by-using-the-sharepoint-net-client-object-model"></a><span data-ttu-id="67120-138">Пример кода: Start и stop после содержимого с помощью клиентской объектной модели SharePoint .NET</span><span class="sxs-lookup"><span data-stu-id="67120-138">Code example: Start and stop following content by using the SharePoint .NET client object model</span></span>
<span data-ttu-id="67120-139"><a name="bkmk_FollowContent"> </a></span><span class="sxs-lookup"><span data-stu-id="67120-139"><a name="bkmk_FollowContent"> </a></span></span>

<span data-ttu-id="67120-p103">В следующем примере кода делает текущего пользователя запустить следующие или остановить после конечного элемента. В нем показано, как:</span><span class="sxs-lookup"><span data-stu-id="67120-p103">The following code example makes the current user start following or stop following a target item. It shows how to:</span></span>
  
    
    

- <span data-ttu-id="67120-142">Проверьте, является ли текущий пользователь отслеживание определенного документа или сайта с помощью метода  [IsFollowed](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.IsFollowed.aspx) .</span><span class="sxs-lookup"><span data-stu-id="67120-142">Check whether the current user is following a particular document or site by using the  [IsFollowed](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.IsFollowed.aspx) method.</span></span>
    
  
- <span data-ttu-id="67120-143">Запустите отслеживание документа или сайта с помощью метода  [Follow](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.Follow.aspx) .</span><span class="sxs-lookup"><span data-stu-id="67120-143">Start following a document or site by using the  [Follow](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.Follow.aspx) method.</span></span>
    
  
- <span data-ttu-id="67120-144">Остановите отслеживание документа или сайта с помощью метода  [StopFollowing](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.StopFollowing.aspx) .</span><span class="sxs-lookup"><span data-stu-id="67120-144">Stop following a document or site by using the  [StopFollowing](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.StopFollowing.aspx) method.</span></span>
    
  
- <span data-ttu-id="67120-145">Получение числа документов или сайты, которые текущий пользователь подписан с помощью метода  [GetFollowedCount](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.GetFollowedCount.aspx) .</span><span class="sxs-lookup"><span data-stu-id="67120-145">Get the count of documents or sites that the current user is following by using the  [GetFollowedCount](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.GetFollowedCount.aspx) method.</span></span>
    
  
<span data-ttu-id="67120-146">В этом примере код использует объект  [SocialFollowResult](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowResult.aspx) , который возвращается методом [Follow](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.Follow.aspx) для определения необходимости запустить или остановить после конечного элемента.</span><span class="sxs-lookup"><span data-stu-id="67120-146">This code example uses the  [SocialFollowResult](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowResult.aspx) object that is returned by the [Follow](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.Follow.aspx) method to determine whether to start or stop following the target item.</span></span>
  
    
    

> <span data-ttu-id="67120-147">**Примечание:** Изменение значений заполнитель для переменных **serverUrl** и **contentUrl** , прежде чем запускать код.</span><span class="sxs-lookup"><span data-stu-id="67120-147">**Note:** Change the placeholder values for the **serverUrl** and **contentUrl** variables before you run the code.</span></span> <span data-ttu-id="67120-148">Чтобы использовать вместо документ на сайт, используйте переменные, которые закомментированы.</span><span class="sxs-lookup"><span data-stu-id="67120-148">To use a site instead of a document, use the variables that are commented out.</span></span>
  
    
    




```cs

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Microsoft.SharePoint.Client;
using Microsoft.SharePoint.Client.Social;

namespace FollowContentCSOM
{
    class Program
    {
        static ClientContext clientContext;
        static SocialFollowingManager followingManager;
        static void Main(string[] args)
        {

            // Replace the following placeholder values with the URL of the target
            // server and target document (or site).
            const string serverUrl = "http://serverName";
            const string contentUrl = @"http://serverName/libraryName/fileName";
            const SocialActorType contentType = SocialActorType.Document;
            // Do not use a trailing '/' for a subsite.
            //const string contentUrl = @"http://serverName/subsiteName"; 
            //const SocialActorType contentType = SocialActorType.Site;

            // Get the client context.
            clientContext = new ClientContext(serverUrl);

            // Get the SocialFeedManager instance.
            followingManager = new SocialFollowingManager(clientContext);

            // Create a SocialActorInfo object to represent the target item.
            SocialActorInfo actorInfo = new SocialActorInfo();
            actorInfo.ContentUri = contentUrl;
            actorInfo.ActorType = contentType;

            // Find out whether the current user is following the target item.
            ClientResult<bool> isFollowed = followingManager.IsFollowed(actorInfo);

            // Get the information from the server.
            clientContext.ExecuteQuery();

            Console.WriteLine("Was the current user following the target {0}? {1}\\n",
                actorInfo.ActorType.ToString().ToLower(), isFollowed.Value);
            Console.Write("Initial count: ");

            // Get the current count of followed items.
            WriteFollowedCount(actorInfo.ActorType);

            // Try to follow the target item. If the result is OK, then
            // the request succeeded.
            ClientResult<SocialFollowResult> result = followingManager.Follow(actorInfo);
            clientContext.ExecuteQuery();

            // If the result is AlreadyFollowing, then stop following 
            // the target item.
            if (result.Value == SocialFollowResult.AlreadyFollowing)
            {
                followingManager.StopFollowing(actorInfo);
                clientContext.ExecuteQuery();
            }

            // Handle other SocialFollowResult return values.
            else if (result.Value == SocialFollowResult.LimitReached
                || result.Value == SocialFollowResult.InternalError)
            {
                Console.WriteLine(result.Value);
            }

            // Get the updated count of followed items.
            Console.Write("Updated count: ");
            WriteFollowedCount(actorInfo.ActorType);
            Console.ReadKey();
        }

        // Get the count of the items that the current user is following.
        static void WriteFollowedCount(SocialActorType type)
        {

            // Set the parameter for the GetFollowedCount method, and
            // handle the case where the item is a site. 
            SocialActorTypes types = SocialActorTypes.Documents;
            if (type != SocialActorType.Document)
            {
                types = SocialActorTypes.Sites;
            }

            ClientResult<int> followedCount = followingManager.GetFollowedCount(types);
            clientContext.ExecuteQuery();
            Console.WriteLine("{0} followed {1}", followedCount.Value, types.ToString().ToLower());
        }
    }
}
```


## <a name="code-example-get-followed-content-by-using-the-sharepoint-net-client-object-model"></a><span data-ttu-id="67120-149">Пример кода: получение отслеживаемого содержимого с помощью клиентской объектной модели SharePoint .NET</span><span class="sxs-lookup"><span data-stu-id="67120-149">Code example: Get followed content by using the SharePoint .NET client object model</span></span>
<span data-ttu-id="67120-150"><a name="bkmk_GetFollowed"> </a></span><span class="sxs-lookup"><span data-stu-id="67120-150"><a name="bkmk_GetFollowed"> </a></span></span>

<span data-ttu-id="67120-p105">В следующем примере кода получает документов и сайтов, что текущий пользователь имеет следующие и получает сведения о следующих контента состояния пользователя. В нем показано, как:</span><span class="sxs-lookup"><span data-stu-id="67120-p105">The following code example gets the documents and sites that the current user is following and gets information about the user's Following Content status. It shows how to:</span></span>
  
    
    

- <span data-ttu-id="67120-153">Проверьте, является ли текущий пользователь следующие целевого документа и сайт с помощью метода  [IsFollowed](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.IsFollowed.aspx) .</span><span class="sxs-lookup"><span data-stu-id="67120-153">Check whether the current user is following the target document and site by using the  [IsFollowed](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.IsFollowed.aspx) method.</span></span>
    
  
- <span data-ttu-id="67120-154">Получение числа документов и сайты, которые текущий пользователь подписан с помощью метода  [GetFollowedCount](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.GetFollowedCount.aspx) .</span><span class="sxs-lookup"><span data-stu-id="67120-154">Get the count of documents and sites that the current user is following by using the  [GetFollowedCount](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.GetFollowedCount.aspx) method.</span></span>
    
  
- <span data-ttu-id="67120-155">Получение документов и сайты, которые текущий пользователь подписан с помощью метода  [GetFollowed](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.GetFollowed.aspx) .</span><span class="sxs-lookup"><span data-stu-id="67120-155">Get the documents and sites that the current user is following by using the  [GetFollowed](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.GetFollowed.aspx) method.</span></span>
    
  
- <span data-ttu-id="67120-156">Выполните итерацию по группы содержимого и получение каждого элемента имя контента URI и URI.</span><span class="sxs-lookup"><span data-stu-id="67120-156">Iterate through the groups of content and get each item's name, content URI, and URI.</span></span>
    
  

> <span data-ttu-id="67120-157">**Примечание:** Измените значение заполнитель для переменных **serverUrl**, **docContentUrl**и **siteContentUrl** , прежде чем запускать код.</span><span class="sxs-lookup"><span data-stu-id="67120-157">**Note:** Change the placeholder value for the **serverUrl**, **docContentUrl**, and **siteContentUrl** variables before you run the code.</span></span>
  
    
    


```cs

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Microsoft.SharePoint.Client;
using Microsoft.SharePoint.Client.Social;

namespace FollowContentCSOM
{
    class Program
    {
        static void Main(string[] args)
        {

            // Replace the following placeholder values with the URLs of
            // the target server, document, and site.
            const string serverUrl = "http://serverName";
            const string docContentUrl = @"http://serverName/libraryName/fileName";
            const string siteContentUrl = @"http://serverName/subsiteName"; // do not use a trailing '/' for a subsite

            // Get the client context.
            ClientContext clientContext = new ClientContext(serverUrl);

            // Get the SocialFollowingManager instance.
            SocialFollowingManager followingManager = new SocialFollowingManager(clientContext);

            // Create SocialActorInfo objects to represent the target 
            // document and site.
            SocialActorInfo docActorInfo = new SocialActorInfo();
            docActorInfo.ContentUri = docContentUrl;
            docActorInfo.ActorType = SocialActorType.Document;
            SocialActorInfo siteActorInfo = new SocialActorInfo();
            siteActorInfo.ContentUri = siteContentUrl;
            siteActorInfo.ActorType = SocialActorType.Site;

            // Find out whether the current user is following the target
            // document and site.
            ClientResult<bool> isDocFollowed = followingManager.IsFollowed(docActorInfo);
            ClientResult<bool> isSiteFollowed = followingManager.IsFollowed(siteActorInfo);

            // Get the count of documents and sites that the current
            // user is following.
            ClientResult<int> followedDocCount = followingManager.GetFollowedCount(SocialActorTypes.Documents);
            ClientResult<int> followedSiteCount = followingManager.GetFollowedCount(SocialActorTypes.Sites);

            // Get the documents and the sites that the current user
            // is following.
            ClientResult<SocialActor[]> followedDocResult = followingManager.GetFollowed(SocialActorTypes.Documents);
            ClientResult<SocialActor[]> followedSiteResult = followingManager.GetFollowed(SocialActorTypes.Sites);

            // Get the information from the server.
            clientContext.ExecuteQuery();

            // Write the results to the console window.
            Console.WriteLine("Is the current user following the target document? {0}", isDocFollowed.Value);
            Console.WriteLine("Is the current user following the target site? {0}", isSiteFollowed.Value);
            if (followedDocCount.Value > 0)
            {
                IterateThroughContent(followedDocCount.Value, followedDocResult.Value);
            } if (followedSiteCount.Value > 0)
            {
                IterateThroughContent(followedSiteCount.Value, followedSiteResult.Value);
            }
            Console.ReadKey();
        }

        // Iterate through the items and get each item's display
        // name, content URI, and absolute URI.
        static void IterateThroughContent(int count, SocialActor[] actors)
        {
            SocialActorType actorType = actors[0].ActorType;
            Console.WriteLine("\\nThe current user is following {0} {1}s:", count, actorType.ToString().ToLower());
            foreach (SocialActor actor in actors)
            {
                Console.WriteLine("  - {0}", actor.Name);
                Console.WriteLine("\\tContent URI: {0}", actor.ContentUri);
                Console.WriteLine("\\tURI: {0}", actor.Uri);
            }
        }
    }
}
```


## <a name="additional-resources"></a><span data-ttu-id="67120-158">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="67120-158">Additional resources</span></span>
<span data-ttu-id="67120-159"><a name="bkmk_AddtionalResources"> </a></span><span class="sxs-lookup"><span data-stu-id="67120-159"><a name="bkmk_AddtionalResources"> </a></span></span>


-  [<span data-ttu-id="67120-160">Подписка на контент в SharePoint</span><span class="sxs-lookup"><span data-stu-id="67120-160">Follow content in SharePoint</span></span>](follow-content-in-sharepoint.md)
    
  
-  [<span data-ttu-id="67120-161">Как подписываться на документы, сайты и теги, используя службу REST в SharePoint</span><span class="sxs-lookup"><span data-stu-id="67120-161">How to: Follow documents, sites, and tags by using the REST service in SharePoint</span></span>](how-to-follow-documents-sites-and-tags-by-using-the-rest-service-in-sharepoint-2.md)
    
  
-  [<span data-ttu-id="67120-162">Как подписываться на пользователей, используя клиентскую объектную модель .NET в SharePoint</span><span class="sxs-lookup"><span data-stu-id="67120-162">How to: Follow people by using the .NET client object model in SharePoint</span></span>](how-to-follow-people-by-using-the-net-client-object-model-in-sharepoint.md)
    
  

