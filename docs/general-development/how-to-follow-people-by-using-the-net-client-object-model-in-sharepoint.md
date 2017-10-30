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
# <a name="how-to-follow-people-by-using-the-net-client-object-model-in-sharepoint"></a>Как: подписка на людей с помощью клиентской объектной модели .NET в SharePoint
Узнайте, как работа с функциями следующих пользователей с помощью клиентской объектной модели SharePoint .NET.
## <a name="why-use-following-people-features-in-sharepoint"></a>Причины использования функций следующих пользователей в SharePoint?

В SharePoint при подписан пользователь людей, публикации и действий пользователей, а затем отображаются в канале новостей пользователя. С помощью функции следующие сотрудники сосредоточиться на пользователей, которые важны пользователей, можно улучшить релевантности приложений или решений. В клиентской объектной модели .NET людей, которые вы выполните представлены объектами [SocialActor](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialActor.aspx) . Для выполнения основных задач следующие сотрудники в клиентской объектной модели .NET, используйте объект [SocialFollowingManager](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.aspx) . В этой статье описывается использование клиентской объектной модели .NET для работы с функциями следующие сотрудники.
  
    
    

> **Примечание:** Внимание на [SocialFollowingManager](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.aspx) поскольку объединяет основные функциональные возможности для следующих пользователей и контента. Тем не менее объект [PeopleManager](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.PeopleManager.aspx) содержит дополнительные функции для следующих пользователей, таких как метод [AmIFollowedBy(String)](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.AmIFollowedBy.aspx) и методы, которые получить следующие состояния другим пользователям.
  
    
    


## <a name="prerequisites-for-setting-up-your-development-environment-to-work-with-following-people-features-by-using-the-sharepoint-net-client-object-model"></a>Необходимые условия для настройки среды разработки для работы с функциями следующие сотрудники с помощью клиентской объектной модели SharePoint .NET

Создание консольного приложения, использующего клиентской объектной модели .NET для работы с функциями следующие сотрудники, необходимо следующее:
  
    
    

- SharePoint с личного сайта настроены и профили пользователей и личные сайты, созданные для текущего пользователя и конечного пользователя
    
  
- Visual Studio 2012
    
  
- **Полный** доступ к приложению-службе профилей пользователей для пользователя, вошедшего в систему
    
  

> **Примечание:** При разработке не на компьютере, на котором работает SharePoint, загрузить [Клиентские компоненты SharePoint](http://www.microsoft.com/en-us/download/details.aspx?id=35585) , содержащий клиентскую сборку SharePoint.
  
    
    


## <a name="create-a-console-application-in-visual-studio-2012"></a>Создание консольного приложения в Visual Studio 2012
<a name="bkmk_CreateConsoleApp"> </a>


1. Откройте Visual Studio и в меню **Файл** последовательно выберите элементы **Создать** и **Проект**.
    
  
2. В верхней части диалогового окна **Новый проект** выберите **.NET Framework 4.5** в раскрывающемся списке.
    
  
3. В списке **шаблонов** выберите **Windows** и затем выберите шаблон **Консольное приложение**.
    
  
4. Назовите проект FollowPeopleCSOMи затем нажмите кнопку **ОК**.
    
  
5. Добавьте ссылки на следующие сборки:
    
  - **Microsoft.SharePoint.Client**  
  - **Microsoft.SharePoint.ClientRuntime** 
  - **Microsoft.SharePoint.Client.UserProfiles**
    
  
6. Замените содержимое класса **Program** в примере кода на класс из следующих сценариев:
    
  -  [Запуск и остановка отслеживаемые пользователи](how-to-follow-people-by-using-the-net-client-object-model-in-sharepoint.md#bkmk_FollowPeople)  
  -  [Получите последователи и пользователей](how-to-follow-people-by-using-the-net-client-object-model-in-sharepoint.md#bkmk_GetFollowednFollowers)
    
  
7. Тестирование консольного приложения в строке меню выберите команду **Отладка**, **Начать отладку**.
    
  

## <a name="code-example-start-or-stop-following-people-by-using-the-sharepoint-net-client-object-model"></a>Пример кода: запустить или остановить следующие людей с помощью клиентской объектной модели SharePoint .NET
<a name="bkmk_FollowPeople"> </a>

В следующем примере кода делает текущего пользователя запустить следующие или остановить после конечного пользователя. В нем показано, как:
  
    
    

- Проверьте, является ли текущий пользователь выполнив конечного пользователя с помощью метода  [IsFollowed](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.IsFollowed.aspx) .
    
  
- Получение числа пользователей, которые текущий пользователь подписан с помощью метода  [GetFollowedCount](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.GetFollowedCount.aspx) .
    
  
- Запустите следующие конечного пользователя с помощью метода  [Follow](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.Follow.aspx) .
    
  
- Отменить подписку конечного пользователя с помощью метода  [StopFollowing](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.StopFollowing.aspx) .
    
  
В этом примере код использует объект  [SocialFollowResult](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowResult.aspx) , который возвращается методом [Follow](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.Follow.aspx) , чтобы определить, нужно ли запустить или остановить после конечного пользователя.
  
    
    

> **Примечание:** Изменение значений заполнитель для переменных **serverUrl** и **targetUser** , прежде чем запускать код.
  
    
    




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


## <a name="code-example-get-followers-and-followed-people-by-using-the-sharepoint-net-client-object-model"></a>Пример кода: получение последователи и отслеживаемого людей с помощью клиентской объектной модели SharePoint .NET
<a name="bkmk_GetFollowednFollowers"> </a>

Следующий пример возвращает код пользователей, которые следующие текущего пользователя, получает пользователей, которые следуют текущего пользователя и получает сведения о состоянии следующие сотрудники текущего пользователя. В нем показано, как:
  
    
    

- Проверьте, является ли текущий пользователь выполнив конечного пользователя с помощью метода  [IsFollowed](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.IsFollowed.aspx) .
    
  
- Получение числа пользователей, которые текущий пользователь подписан с помощью метода  [GetFollowedCount](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.GetFollowedCount.aspx) .
    
  
- Получите пользователей, которые текущий пользователь подписан с помощью метода  [GetFollowed](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.GetFollowed.aspx) .
    
  
- Получите пользователей, которые отслеживаются текущего пользователя с помощью метода  [GetFollowers](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.GetFollowers.aspx) .
    
  
- Выполните итерацию по группам людей и получить отображаемое имя каждого контакта, личные URI и рисунков URI.
    
  

> **Примечание:** Изменение значений заполнитель для переменных **serverUrl** и **targetUser** , прежде чем запускать код.
  
    
    


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


## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="bkmk_AdditionalResources"> </a>


-  [Подписка на людей в SharePoint](follow-people-in-sharepoint.md)
    
  
-  [Как: подписка на людей с помощью объектной модели JavaScript в SharePoint](how-to-follow-people-by-using-the-javascript-object-model-in-sharepoint.md)
    
  
-  [Как: выполните документов и сайтов с помощью клиентской объектной модели .NET в SharePoint](how-to-follow-documents-and-sites-by-using-the-net-client-object-model-in-sharep.md)
    
  

