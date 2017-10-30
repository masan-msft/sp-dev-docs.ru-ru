---
title: "Как выполнить документов и сайтов с помощью клиентской объектной модели .NET в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 84366e01-4961-459d-8109-2f1d2d714353
ms.openlocfilehash: 7b5ba3031c5c02784b00da46d91105c729119d4a
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-follow-documents-and-sites-by-using-the-net-client-object-model-in-sharepoint"></a>Как: выполните документов и сайтов с помощью клиентской объектной модели .NET в SharePoint
Узнайте, как работа с функциями следующие контента с помощью клиентской объектной модели SharePoint .NET.
## <a name="how-do-i-use-the-net-client-object-model-to-follow-content"></a>Использование клиентской объектной модели .NET для подписка на контент
<a name="bk_intro"> </a>

Пользователи SharePoint можно следовать документы, сайты, и теги можно следовать документы, сайты и теги для получения обновлений об элементах в свои каналы новостей и быстро открыть число документов и сайтов. Клиентская объектная модель .NET можно использовать в вашем приложении или решение, которое требуется запустить следующие материалы, остановите следующие материалы и получить отслеживаемого содержимого от имени текущего пользователя. В этой статье описывается создание консольного приложения, использующего клиентской объектной модели .NET для работы с контента следующие функции для документов и сайтов.
  
    
    
Основные интерфейсы API для контента следующие задачи являются следующие объекты:
  
    
    

-  [SocialFollowingManager](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.aspx) предоставляет методы для управления пользовательского списка число субъектов.
    
  
-  [SocialActor](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialActor.aspx) представляет документ, сайта или тег, сервер возвращает в ответ на запрос на стороне клиента.
    
  
-  [SocialActorInfo](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialActorInfo.aspx) указывает документ, сайта или тега в запросах со стороны клиента к серверу.
    
  
-  [Microsoft.SharePoint.Client.Social.SocialActorType](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialActorType.aspx) и [Microsoft.SharePoint.Client.Social.SocialActorTypes](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialActorTypes.aspx) укажите типы контента в запросах со стороны клиента к серверу.
    
  

> **Примечание:** Также использовать эти API-интерфейсы для задачи следующие сотрудники, но **GetSuggestions** и **GetFollowers** методы, доступные из поддерживают только [SocialFollowingManager](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.aspx) , отслеживаемые пользователи не контента. Дополнительные сведения об использовании [SocialFollowingManager](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.aspx) можно [Подписка на контент в SharePoint](follow-content-in-sharepoint.md) и [Подписка на людей в SharePoint](follow-people-in-sharepoint.md). Примеры кода, показывающие, как следить за людьми, в разделе [как: подписка на людей с помощью клиентской объектной модели .NET в SharePoint](how-to-follow-people-by-using-the-net-client-object-model-in-sharepoint.md). 
  
    
    


## <a name="prerequisites-for-setting-up-your-development-environment-to-work-with-following-content-features-by-using-the-sharepoint-net-client-object-model"></a>Необходимые условия для настройки среды разработки для работы с возможности следующие содержимого с помощью клиентской объектной модели SharePoint .NET
<a name="bkmk_SetUpDevEnv"> </a>

Создание консольного приложения, использующего клиентской объектной модели .NET для работы с контента следующие функции для документов и сайты, необходимо следующее:
  
    
    

- Настройки SharePoint с помощью личных сайтов, с помощью узла личных сайтов, созданных для текущего пользователя и с документом, загруженные в библиотеку документов SharePoint
    
  
- Visual Studio 2012
    
  
- **Полный** доступ к приложению-службе профилей пользователей для пользователя, вошедшего в систему
    
  

> **Примечание:** Если вы работаете не на компьютере, на котором работает SharePoint, загрузить [Клиентских компонентов SharePoint](http://www.microsoft.com/en-us/download/details.aspx?id=35585) , содержащий клиентскую сборку SharePoint.
  
    
    


## <a name="create-a-console-application-to-work-with-following-content-features-by-using-the-sharepoint-net-client-object-model"></a>Создание консольного приложения для работы с возможности следующие содержимого с помощью клиентской объектной модели SharePoint .NET
<a name="bkmk_CreateConsoleApp"> </a>


1. В меню Visual Studio выберите пункт **Файл**, **Создать**, затем **Проект**.
    
  
2. В верхней части диалогового окна **Новый проект** выберите **.NET Framework 4.5** в раскрывающемся списке.
    
  
3. В списке **шаблонов** выберите **Windows** и затем выберите шаблон **Консольное приложение**.
    
  
4. Назовите проект FollowContentCSOMи затем нажмите кнопку **ОК**.
    
  
5. Добавьте ссылки на следующие сборки:
    
  - **Microsoft.SharePoint.Client**   
  - **Microsoft.SharePoint.ClientRuntime**
  - **Microsoft.SharePoint.Client.UserProfiles**
    
6. Замените содержимое класса **Program** в примере кода на класс из следующих сценариев:
    
  -  [Запуск и остановка следующие материалы](how-to-follow-documents-and-sites-by-using-the-net-client-object-model-in-sharep.md#bkmk_FollowContent)  
  -  [Получение контента для текущего пользователя](how-to-follow-documents-and-sites-by-using-the-net-client-object-model-in-sharep.md#bkmk_GetFollowed)
    
7. Тестирование консольного приложения в строке меню выберите команду **Отладка**, **Начать отладку**.
    
  

## <a name="code-example-start-and-stop-following-content-by-using-the-sharepoint-net-client-object-model"></a>Пример кода: Start и stop после содержимого с помощью клиентской объектной модели SharePoint .NET
<a name="bkmk_FollowContent"> </a>

В следующем примере кода делает текущего пользователя запустить следующие или остановить после конечного элемента. В нем показано, как:
  
    
    

- Проверьте, является ли текущий пользователь отслеживание определенного документа или сайта с помощью метода  [IsFollowed](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.IsFollowed.aspx) .
    
  
- Запустите отслеживание документа или сайта с помощью метода  [Follow](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.Follow.aspx) .
    
  
- Остановите отслеживание документа или сайта с помощью метода  [StopFollowing](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.StopFollowing.aspx) .
    
  
- Получение числа документов или сайты, которые текущий пользователь подписан с помощью метода  [GetFollowedCount](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.GetFollowedCount.aspx) .
    
  
В этом примере код использует объект  [SocialFollowResult](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowResult.aspx) , который возвращается методом [Follow](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.Follow.aspx) для определения необходимости запустить или остановить после конечного элемента.
  
    
    

> **Примечание:** Изменение значений заполнитель для переменных **serverUrl** и **contentUrl** , прежде чем запускать код. Чтобы использовать вместо документ на сайт, используйте переменные, которые закомментированы.
  
    
    




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


## <a name="code-example-get-followed-content-by-using-the-sharepoint-net-client-object-model"></a>Пример кода: получение отслеживаемого содержимого с помощью клиентской объектной модели SharePoint .NET
<a name="bkmk_GetFollowed"> </a>

В следующем примере кода получает документов и сайтов, что текущий пользователь имеет следующие и получает сведения о следующих контента состояния пользователя. В нем показано, как:
  
    
    

- Проверьте, является ли текущий пользователь следующие целевого документа и сайт с помощью метода  [IsFollowed](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.IsFollowed.aspx) .
    
  
- Получение числа документов и сайты, которые текущий пользователь подписан с помощью метода  [GetFollowedCount](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.GetFollowedCount.aspx) .
    
  
- Получение документов и сайты, которые текущий пользователь подписан с помощью метода  [GetFollowed](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.GetFollowed.aspx) .
    
  
- Выполните итерацию по группы содержимого и получение каждого элемента имя контента URI и URI.
    
  

> **Примечание:** Измените значение заполнитель для переменных **serverUrl**, **docContentUrl**и **siteContentUrl** , прежде чем запускать код.
  
    
    


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


## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="bkmk_AddtionalResources"> </a>


-  [Подписка на контент в SharePoint](follow-content-in-sharepoint.md)
    
  
-  [Как: выполните документы, сайты и теги с помощью службы REST в SharePoint](how-to-follow-documents-sites-and-tags-by-using-the-rest-service-in-sharepoint-2.md)
    
  
-  [Как: подписка на людей с помощью клиентской объектной модели .NET в SharePoint](how-to-follow-people-by-using-the-net-client-object-model-in-sharepoint.md)
    
  

