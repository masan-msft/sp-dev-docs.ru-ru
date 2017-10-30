---
title: "Как следить за пользователями с помощью клиентской объектной модели .NET в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 0fdb7ca5-d408-4256-b52b-886c4bc3b5b8
ms.openlocfilehash: 3c097c476f3bb020a26f0baf9b2dcdb23babb1a3
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-follow-people-by-using-the-net-client-object-model-in-sharepoint"></a><span data-ttu-id="4034d-102">Как: подписка на людей с помощью клиентской объектной модели .NET в SharePoint</span><span class="sxs-lookup"><span data-stu-id="4034d-102">How to: Follow people by using the .NET client object model in SharePoint</span></span>
<span data-ttu-id="4034d-103">Узнайте, как работа с функциями следующих пользователей с помощью клиентской объектной модели SharePoint .NET.</span><span class="sxs-lookup"><span data-stu-id="4034d-103">Learn how to work with Following People features by using the SharePoint .NET client object model.</span></span>
## <a name="why-use-following-people-features-in-sharepoint"></a><span data-ttu-id="4034d-104">Причины использования функций следующих пользователей в SharePoint?</span><span class="sxs-lookup"><span data-stu-id="4034d-104">Why use Following People features in SharePoint?</span></span>

<span data-ttu-id="4034d-105">В SharePoint при подписан пользователь людей, публикации и действий пользователей, а затем отображаются в канале новостей пользователя.</span><span class="sxs-lookup"><span data-stu-id="4034d-105">In SharePoint, when a user follows people, the posts and activities of the followed people show up in the user's newsfeed.</span></span> <span data-ttu-id="4034d-106">С помощью функции следующие сотрудники сосредоточиться на пользователей, которые важны пользователей, можно улучшить релевантности приложений или решений.</span><span class="sxs-lookup"><span data-stu-id="4034d-106">By using Following People features to focus on the people who users care about, you can improve the relevance of your app or solution.</span></span> <span data-ttu-id="4034d-107">В клиентской объектной модели .NET людей, которые вы выполните представлены объектами [SocialActor](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialActor.aspx) .</span><span class="sxs-lookup"><span data-stu-id="4034d-107">In the .NET client object model, people that you follow are represented by  [SocialActor](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialActor.aspx) objects.</span></span> <span data-ttu-id="4034d-108">Для выполнения основных задач следующие сотрудники в клиентской объектной модели .NET, используйте объект [SocialFollowingManager](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.aspx) .</span><span class="sxs-lookup"><span data-stu-id="4034d-108">To perform core Following People tasks in the .NET client object model, you use the [SocialFollowingManager](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.aspx) object.</span></span> <span data-ttu-id="4034d-109">В этой статье описывается использование клиентской объектной модели .NET для работы с функциями следующие сотрудники.</span><span class="sxs-lookup"><span data-stu-id="4034d-109">This article shows how to use the .NET client object model to work with Following People features.</span></span>
  
    
    

> <span data-ttu-id="4034d-110">**Примечание:** Внимание на [SocialFollowingManager](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.aspx) поскольку объединяет основные функциональные возможности для следующих пользователей и контента.</span><span class="sxs-lookup"><span data-stu-id="4034d-110">**Note:** We focus on  [SocialFollowingManager](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.aspx) because it consolidates the core functionality for following people and content.</span></span> <span data-ttu-id="4034d-111">Тем не менее объект [PeopleManager](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.PeopleManager.aspx) содержит дополнительные функции для следующих пользователей, таких как метод [AmIFollowedBy(String)](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.AmIFollowedBy.aspx) и методы, которые получить следующие состояния другим пользователям.</span><span class="sxs-lookup"><span data-stu-id="4034d-111">However, the [PeopleManager](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.PeopleManager.aspx) object contains additional functionality for following people, such as the [AmIFollowedBy(String)](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.AmIFollowedBy.aspx) method and methods that obtain the following status of other users.</span></span>
  
    
    


## <a name="prerequisites-for-setting-up-your-development-environment-to-work-with-following-people-features-by-using-the-sharepoint-net-client-object-model"></a><span data-ttu-id="4034d-112">Необходимые условия для настройки среды разработки для работы с функциями следующие сотрудники с помощью клиентской объектной модели SharePoint .NET</span><span class="sxs-lookup"><span data-stu-id="4034d-112">Prerequisites for setting up your development environment to work with Following People features by using the SharePoint .NET client object model</span></span>

<span data-ttu-id="4034d-113">Создание консольного приложения, использующего клиентской объектной модели .NET для работы с функциями следующие сотрудники, необходимо следующее:</span><span class="sxs-lookup"><span data-stu-id="4034d-113">To create a console application that uses the .NET client object model to work with Following People features, you'll need the following:</span></span>
  
    
    

- <span data-ttu-id="4034d-114">SharePoint с личного сайта настроены и профили пользователей и личные сайты, созданные для текущего пользователя и конечного пользователя</span><span class="sxs-lookup"><span data-stu-id="4034d-114">SharePoint with My Site configured, and with user profiles and personal sites created for the current user and a target user</span></span>
    
  
- <span data-ttu-id="4034d-115">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="4034d-115">Visual Studio 2012</span></span>
    
  
- <span data-ttu-id="4034d-116">**Полный** доступ к приложению-службе профилей пользователей для пользователя, вошедшего в систему</span><span class="sxs-lookup"><span data-stu-id="4034d-116">**Full Control** access permissions to the User Profile service application for the logged-on user</span></span>
    
  

> <span data-ttu-id="4034d-117">**Примечание:** При разработке не на компьютере, на котором работает SharePoint, загрузить [Клиентские компоненты SharePoint](http://www.microsoft.com/en-us/download/details.aspx?id=35585) , содержащий клиентскую сборку SharePoint.</span><span class="sxs-lookup"><span data-stu-id="4034d-117">**Note:** If you're not developing on the computer that is running SharePoint, get the  [SharePoint Client Components](http://www.microsoft.com/en-us/download/details.aspx?id=35585) download that contains SharePoint client assemblies.</span></span>
  
    
    


## <a name="create-a-console-application-in-visual-studio-2012"></a><span data-ttu-id="4034d-118">Создание консольного приложения в Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="4034d-118">Create a console application in Visual Studio 2012</span></span>
<span data-ttu-id="4034d-119"><a name="bkmk_CreateConsoleApp"> </a></span><span class="sxs-lookup"><span data-stu-id="4034d-119"></span></span>


1. <span data-ttu-id="4034d-120">Откройте Visual Studio и в меню **Файл** последовательно выберите элементы **Создать** и **Проект**.</span><span class="sxs-lookup"><span data-stu-id="4034d-120">Open Visual Studio, and choose **File**, **New**, **Project**.</span></span>
    
  
2. <span data-ttu-id="4034d-121">В верхней части диалогового окна **Новый проект** выберите **.NET Framework 4.5** в раскрывающемся списке.</span><span class="sxs-lookup"><span data-stu-id="4034d-121">In the **New Project** dialog box, choose **.NET Framework 4.5** from the drop-down list at the top of the dialog box.</span></span>
    
  
3. <span data-ttu-id="4034d-122">В списке **шаблонов** выберите **Windows** и затем выберите шаблон **Консольное приложение**.</span><span class="sxs-lookup"><span data-stu-id="4034d-122">In the **Templates** list, choose **Windows**, and then choose the **Console Application** template.</span></span>
    
  
4. <span data-ttu-id="4034d-123">Назовите проект FollowPeopleCSOMи затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="4034d-123">Name the project FollowPeopleCSOM, and then choose the **OK** button.</span></span>
    
  
5. <span data-ttu-id="4034d-124">Добавьте ссылки на следующие сборки:</span><span class="sxs-lookup"><span data-stu-id="4034d-124">Add references to the following assemblies:</span></span>
    
  - <span data-ttu-id="4034d-125">**Microsoft.SharePoint.Client**</span><span class="sxs-lookup"><span data-stu-id="4034d-125">**Microsoft.SharePoint.Client**</span></span>  
  - <span data-ttu-id="4034d-126">**Microsoft.SharePoint.ClientRuntime**</span><span class="sxs-lookup"><span data-stu-id="4034d-126">**Microsoft.SharePoint.ClientRuntime**</span></span> 
  - <span data-ttu-id="4034d-127">**Microsoft.SharePoint.Client.UserProfiles**</span><span class="sxs-lookup"><span data-stu-id="4034d-127">**Microsoft.SharePoint.Client.UserProfiles**</span></span>
    
  
6. <span data-ttu-id="4034d-128">Замените содержимое класса **Program** в примере кода на класс из следующих сценариев:</span><span class="sxs-lookup"><span data-stu-id="4034d-128">Replace the contents of the **Program** class with the code example from one of the following scenarios:</span></span>
    
  -  [<span data-ttu-id="4034d-129">Запуск и остановка отслеживаемые пользователи</span><span class="sxs-lookup"><span data-stu-id="4034d-129">Start and stop following people</span></span>](how-to-follow-people-by-using-the-net-client-object-model-in-sharepoint.md#bkmk_FollowPeople)  
  -  [<span data-ttu-id="4034d-130">Получите последователи и пользователей</span><span class="sxs-lookup"><span data-stu-id="4034d-130">Get followers and followed people</span></span>](how-to-follow-people-by-using-the-net-client-object-model-in-sharepoint.md#bkmk_GetFollowednFollowers)
    
  
7. <span data-ttu-id="4034d-131">Тестирование консольного приложения в строке меню выберите команду **Отладка**, **Начать отладку**.</span><span class="sxs-lookup"><span data-stu-id="4034d-131">To test the console application, on the menu bar, choose **Debug**, **Start Debugging**.</span></span>
    
  

## <a name="code-example-start-or-stop-following-people-by-using-the-sharepoint-net-client-object-model"></a><span data-ttu-id="4034d-132">Пример кода: запустить или остановить следующие людей с помощью клиентской объектной модели SharePoint .NET</span><span class="sxs-lookup"><span data-stu-id="4034d-132">Code example: Start or stop following people by using the SharePoint .NET client object model</span></span>
<span data-ttu-id="4034d-133"><a name="bkmk_FollowPeople"> </a></span><span class="sxs-lookup"><span data-stu-id="4034d-133"></span></span>

<span data-ttu-id="4034d-p103">В следующем примере кода делает текущего пользователя запустить следующие или остановить после конечного пользователя. В нем показано, как:</span><span class="sxs-lookup"><span data-stu-id="4034d-p103">The following code example makes the current user start following or stop following a target user. It shows how to:</span></span>
  
    
    

- <span data-ttu-id="4034d-136">Проверьте, является ли текущий пользователь выполнив конечного пользователя с помощью метода  [IsFollowed](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.IsFollowed.aspx) .</span><span class="sxs-lookup"><span data-stu-id="4034d-136">Check whether the current user is following a target user by using the  [IsFollowed](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.IsFollowed.aspx) method.</span></span>
    
  
- <span data-ttu-id="4034d-137">Получение числа пользователей, которые текущий пользователь подписан с помощью метода  [GetFollowedCount](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.GetFollowedCount.aspx) .</span><span class="sxs-lookup"><span data-stu-id="4034d-137">Get the count of people who the current user is following by using the  [GetFollowedCount](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.GetFollowedCount.aspx) method.</span></span>
    
  
- <span data-ttu-id="4034d-138">Запустите следующие конечного пользователя с помощью метода  [Follow](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.Follow.aspx) .</span><span class="sxs-lookup"><span data-stu-id="4034d-138">Start following the target user by using the  [Follow](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.Follow.aspx) method.</span></span>
    
  
- <span data-ttu-id="4034d-139">Отменить подписку конечного пользователя с помощью метода  [StopFollowing](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.StopFollowing.aspx) .</span><span class="sxs-lookup"><span data-stu-id="4034d-139">Stop following the target user by using the  [StopFollowing](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.StopFollowing.aspx) method.</span></span>
    
  
<span data-ttu-id="4034d-140">В этом примере код использует объект  [SocialFollowResult](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowResult.aspx) , который возвращается методом [Follow](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.Follow.aspx) , чтобы определить, нужно ли запустить или остановить после конечного пользователя.</span><span class="sxs-lookup"><span data-stu-id="4034d-140">This code example uses the  [SocialFollowResult](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowResult.aspx) object that is returned by the [Follow](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.Follow.aspx) method to determine whether to start or stop following the target user.</span></span>
  
    
    

> <span data-ttu-id="4034d-141">**Примечание:** Изменение значений заполнитель для переменных **serverUrl** и **targetUser** , прежде чем запускать код.</span><span class="sxs-lookup"><span data-stu-id="4034d-141">**Note:** Change the placeholder values for the **serverUrl** and **targetUser** variables before you run the code.</span></span>
  
    
    




```cs

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Microsoft.SharePoint.Client;
using Microsoft.SharePoint.Client.Social;

namespace FollowPeopleCSOM
{
    class Program
    {
        static ClientContext clientContext;
        static SocialFollowingManager followingManager;
        static void Main(string[] args)
        {

            // Replace the following placeholder values with the target
            // server URL and target user.
            const string serverUrl = "http://serverName";
            const string targetUser = "domainName\\\\userName";

            // Get the client context.
            clientContext = new ClientContext(serverUrl);

            // Get the SocialFeedManager instance.
            followingManager = new SocialFollowingManager(clientContext);

            // Create a SocialActorInfo object to represent the target user.
            SocialActorInfo actorInfo = new SocialActorInfo();
            actorInfo.AccountName = targetUser;

            // Find out whether the current user is following the target user.
            ClientResult<bool> isFollowed = followingManager.IsFollowed(actorInfo);

            // Get the information from the server.
            clientContext.ExecuteQuery();

            Console.WriteLine("Was the current user following the target user? {0}\\n", isFollowed.Value);
            Console.Write("Initial count: ");

            // Get the current count of followed people.
            WriteFollowedCount();

            // Try to follow the target user. If the result is OK, then
            // the request succeeded.
            ClientResult<SocialFollowResult> result = followingManager.Follow(actorInfo);
            clientContext.ExecuteQuery();

            // If the result is AlreadyFollowing, then stop following 
            // the target user.
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

            // Get the updated count of followed people.
            Console.Write("Updated count: ");
            WriteFollowedCount();
            Console.ReadKey();
        }

        // Get the count of the people who the current user is following.
        static void WriteFollowedCount()
        {
            ClientResult<int> followedCount = followingManager.GetFollowedCount(SocialActorTypes.Users);
            clientContext.ExecuteQuery();
            Console.WriteLine("The current user is following {0} people.", followedCount.Value);
        }
    }
}

```


## <a name="code-example-get-followers-and-followed-people-by-using-the-sharepoint-net-client-object-model"></a><span data-ttu-id="4034d-142">Пример кода: получение последователи и отслеживаемого людей с помощью клиентской объектной модели SharePoint .NET</span><span class="sxs-lookup"><span data-stu-id="4034d-142">Code example: Get followers and followed people by using the SharePoint .NET client object model</span></span>
<span data-ttu-id="4034d-143"><a name="bkmk_GetFollowednFollowers"> </a></span><span class="sxs-lookup"><span data-stu-id="4034d-143"></span></span>

<span data-ttu-id="4034d-p104">Следующий пример возвращает код пользователей, которые следующие текущего пользователя, получает пользователей, которые следуют текущего пользователя и получает сведения о состоянии следующие сотрудники текущего пользователя. В нем показано, как:</span><span class="sxs-lookup"><span data-stu-id="4034d-p104">The following code example gets the people who the current user is following, gets the people who are followed by the current user, and gets information about the current user's Following People status. It shows how to:</span></span>
  
    
    

- <span data-ttu-id="4034d-146">Проверьте, является ли текущий пользователь выполнив конечного пользователя с помощью метода  [IsFollowed](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.IsFollowed.aspx) .</span><span class="sxs-lookup"><span data-stu-id="4034d-146">Check whether the current user is following a target user by using the  [IsFollowed](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.IsFollowed.aspx) method.</span></span>
    
  
- <span data-ttu-id="4034d-147">Получение числа пользователей, которые текущий пользователь подписан с помощью метода  [GetFollowedCount](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.GetFollowedCount.aspx) .</span><span class="sxs-lookup"><span data-stu-id="4034d-147">Get the count of people who the current user is following by using the  [GetFollowedCount](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.GetFollowedCount.aspx) method.</span></span>
    
  
- <span data-ttu-id="4034d-148">Получите пользователей, которые текущий пользователь подписан с помощью метода  [GetFollowed](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.GetFollowed.aspx) .</span><span class="sxs-lookup"><span data-stu-id="4034d-148">Get the people who the current user is following by using the  [GetFollowed](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.GetFollowed.aspx) method.</span></span>
    
  
- <span data-ttu-id="4034d-149">Получите пользователей, которые отслеживаются текущего пользователя с помощью метода  [GetFollowers](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.GetFollowers.aspx) .</span><span class="sxs-lookup"><span data-stu-id="4034d-149">Get the people who are following the current user by using the  [GetFollowers](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.GetFollowers.aspx) method.</span></span>
    
  
- <span data-ttu-id="4034d-150">Выполните итерацию по группам людей и получить отображаемое имя каждого контакта, личные URI и рисунков URI.</span><span class="sxs-lookup"><span data-stu-id="4034d-150">Iterate through the groups of people and get each person's display name, personal URI, and picture URI.</span></span>
    
  

> <span data-ttu-id="4034d-151">**Примечание:** Изменение значений заполнитель для переменных **serverUrl** и **targetUser** , прежде чем запускать код.</span><span class="sxs-lookup"><span data-stu-id="4034d-151">**Note:** Change the placeholder values for the **serverUrl** and **targetUser** variables before you run the code.</span></span>
  
    
    


```cs

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Microsoft.SharePoint.Client;
using Microsoft.SharePoint.Client.Social;

namespace FollowPeopleCSOM
{
    class Program
    {
        static void Main(string[] args)
        {

            // Replace the following placeholder values with the target
            // server URL and target user.
            const string serverUrl = "http://serverName";
            const string targetUser = "domainName\\\\userName";

            // Get the client context.
            ClientContext clientContext = new ClientContext(serverUrl);
            
            // Get the SocialFeedManager instance.
            SocialFollowingManager followingManager = new SocialFollowingManager(clientContext);

            // Create a SocialActorInfo object to represent the target user.
            SocialActorInfo actorInfo = new SocialActorInfo();
            actorInfo.AccountName = targetUser;

            // Find out whether the current user is following the target user.
            ClientResult<bool> isFollowed = followingManager.IsFollowed(actorInfo);

            // Get the count of people who the current user is following.
            ClientResult<int> followedCount = followingManager.GetFollowedCount(SocialActorTypes.Users);

            // Get the people who the current user is following.
            ClientResult<SocialActor[]> followedResult = followingManager.GetFollowed(SocialActorTypes.Users);

            // Get the people who are following the current user.
            ClientResult<SocialActor[]> followersResult = followingManager.GetFollowers();

            // Get the information from the server.
            clientContext.ExecuteQuery();

            // Write the results to the console window.
            Console.WriteLine("Is the current user following the target user? {0}\\n", isFollowed.Value);
            Console.WriteLine("People who the current user is following: ({0} count)", followedCount.Value);
            IterateThroughPeople(followedResult.Value);
            Console.WriteLine("\\nPeople who are following the current user:");
            IterateThroughPeople(followersResult.Value);
            Console.ReadKey();
        }

        // Iterate through the people and get each person's display
        // name, personal URI, and picture URI.
        static void IterateThroughPeople(SocialActor[] actors)
        {
            foreach (SocialActor actor in actors)
            {
                Console.WriteLine("  - {0}", actor.Name);
                Console.WriteLine("\\tPersonal URI: {0}", actor.PersonalSiteUri);
                Console.WriteLine("\\tPicture URI: {0}", actor.ImageUri);
            }
        }
    }
}

```


## <a name="additional-resources"></a><span data-ttu-id="4034d-152">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="4034d-152">Additional resources</span></span>
<span data-ttu-id="4034d-153"><a name="bkmk_AdditionalResources"> </a></span><span class="sxs-lookup"><span data-stu-id="4034d-153"></span></span>


-  [<span data-ttu-id="4034d-154">Подписка на людей в SharePoint</span><span class="sxs-lookup"><span data-stu-id="4034d-154">Follow people in SharePoint</span></span>](follow-people-in-sharepoint.md)
    
  
-  [<span data-ttu-id="4034d-155">Как: подписка на людей с помощью объектной модели JavaScript в SharePoint</span><span class="sxs-lookup"><span data-stu-id="4034d-155">How to: Follow people by using the JavaScript object model in SharePoint</span></span>](how-to-follow-people-by-using-the-javascript-object-model-in-sharepoint.md)
    
  
-  [<span data-ttu-id="4034d-156">Как: выполните документов и сайтов с помощью клиентской объектной модели .NET в SharePoint</span><span class="sxs-lookup"><span data-stu-id="4034d-156">How to: Follow documents and sites by using the .NET client object model in SharePoint</span></span>](how-to-follow-documents-and-sites-by-using-the-net-client-object-model-in-sharep.md)
    
  

