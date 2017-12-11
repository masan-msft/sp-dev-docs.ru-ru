---
title: "Чтение и запись на социальные веб-канал с помощью клиентской объектной модели .NET в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 3c15ede5-8a59-47e6-a0b2-c17ec6bf4ae1
ms.openlocfilehash: 74fe67537137ffd6665a1ee0d00afdfa944ecdfa
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="read-and-write-to-the-social-feed-by-using-the-net-client-object-model-in-sharepoint"></a>Чтение и запись на социальные веб-канал с помощью клиентской объектной модели .NET в SharePoint

Создайте консольное приложение, которое читает канал социальных сетей и пишет в него с помощью клиентской объектной модели .NET для SharePoint.

## <a name="prerequisites-for-creating-a-console-application-that-reads-and-writes-to-the-social-feed-by-using-the-sharepoint-net-client-object-model"></a>Необходимые условия для создания консольного приложения, которое считывает и записывает социальных канал, чтобы с помощью клиентской объектной модели SharePoint .NET
<a name="bkmk_Prereqs"> </a>

Консольное приложение, которое вы создадите получает канал для конечного пользователя и печатает post корневой из каждого потока нумерованного списка. Затем публикует ответ простой текст для выбранного потока. Один и тот же метод ( [CreatePost](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.CreatePost.aspx) ) используется для публикации обоих публикации и ответы на канал.
  
    
    
Создание консольного приложения, необходимо следующее:
  
    
    

- SharePoint настроен личного сайта, личные сайты, созданные для текущего пользователя и конечного пользователя и несколько записей, записанные центром конечного пользователя
    
  
- Visual Studio 2012
    
  
- **Полный** доступ к приложению-службе профилей пользователей для пользователя, вошедшего в систему
    
> [!NOTE]
> При разработке не на компьютере, на котором работает SharePoint, загрузить [Клиентские компоненты SharePoint](http://www.microsoft.com/en-us/download/details.aspx?id=35585) , содержащий клиентскую сборку SharePoint.
  
    
    


### <a name="core-concepts-to-know-about-working-with-sharepoint-social-feeds"></a>Основные сведения о работе с социальными веб-каналами SharePoint
<a name="bkmk_CoreConcepts"> </a>

В таблице 1 приведены ссылки на статьи, в которых описываются основные понятия, которые нужно знать перед началом работы.
  
    
    

**В таблице 1. Основные понятия по работе с социальными веб-каналами SharePoint**


|**Название статьи**|**Описание**|
|:-----|:-----|
| [Начало разработки с использованием социальных функций в SharePoint](get-started-developing-with-social-features-in-sharepoint.md) <br/> |Узнайте, как приступить к программированию с социальными веб-каналов и микроблога публикации, следуя людей и содержимое (документы, сайты и tags.md) и работа с профилями пользователей.  <br/> |
| [Работа с социальными веб-каналами в SharePoint](work-with-social-feeds-in-sharepoint.md) <br/> |Сведения о распространенных задач программирования по работе с социальными веб-каналов и API, которое используется для выполнения задачи.  <br/> |
   

## <a name="create-the-console-application-in-visual-studio-2012-and-add-references-to-client-assemblies"></a>Создание консольного приложения в Visual Studio 2012 и добавление ссылок на сборки клиента
<a name="bkmk_CreateApp"> </a>


1. Откройте Visual Studio 2012 на компьютере разработчика.
    
  
2. В строке меню выберите пункты **Файл**, **Создать** и **Проект**.
    
  
3. В верхней части диалогового окна **Новый проект** выберите **.NET Framework 4.5** в раскрывающемся списке.
    
  
4. В списке **шаблонов** выберите **Windows** и затем выберите шаблон **Консольное приложение**.
    
  
5. Назовите проект ReadWriteMySiteи затем нажмите кнопку **ОК**.
    
  
6. Добавление ссылки на сборки клиента следующим образом:
    
   А. В **Обозревателе решений** откройте контекстное меню для проекта **ReadWriteMySite** и затем выберите команду **Добавить ссылку**.
  
   Б. В диалоговом окне **Диспетчер ссылок** выберите следующие сборки:
    
     - **Microsoft.SharePoint.Client**
    
     - **Microsoft.SharePoint.Client.Runtime**
    
     - **Microsoft.SharePoint.Client.UserProfiles**  

   Если вы работаете на компьютере, на котором работает SharePoint, сборки находятся в категории **расширения** . В противном случае перейдите к папке, которая имеет клиентских сборок, загруженный (см [Клиентских компонентов SharePoint](http://www.microsoft.com/downloads/details.aspx?FamilyID=66da4a3e-e3b0-45d9-9e84-a84946fbf239)).
    
  
7. В файле Program.cs добавьте следующие инструкции **using**.
    
```cs
using Microsoft.SharePoint.Client;
using Microsoft.SharePoint.Client.Social;
```


## <a name="retrieve-the-social-feed-for-a-target-user-by-using-the-sharepoint-net-client-object-model"></a>Извлечение социальных веб-канал для конечного пользователя с помощью клиентской объектной модели SharePoint .NET
<a name="bkmk_RetrieveFeed"> </a>


1. Объявите переменные для URL-адрес сервера и создания решений учетные данные учетной записи пользователя.
    
    ```cs
    const string serverUrl = "http://serverName/";
    const string targetUser = "domainName\\userName";
    ```

    > [!NOTE]
    > [!Примечание] Не забудьте заменить заполнитель значения  `http://serverName/` и `domainName\\userName` , прежде чем запускать код.
   
2. В методе **Main** инициализации контекста клиента SharePoint.
    
    ```cs
    ClientContext clientContext = new ClientContext(serverUrl);
    ```

3. Создайте экземпляр  [SocialFeedManager](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.aspx) .
    
    ```cs
    SocialFeedManager feedManager = new SocialFeedManager(clientContext);
    ```

4. Задание параметров для веб-канала активности контент, который требуется получить.
    
    ```cs
    SocialFeedOptions feedOptions = new SocialFeedOptions();
    feedOptions.MaxThreadCount = 10;
    ```

    Параметры по умолчанию возвращения первых 20 потоков в веб-канал, отсортированные по дату последнего изменения.
  
5. Получите конечного пользователя веб-канал.
    
    ```cs 
    ClientResult<SocialFeed> feed = feedManager.GetFeedFor(targetUser, feedOptions);
    clientContext.ExecuteQuery();
    ```

    [GetFeedFor](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.GetFeedFor.aspx) возвращает объект **ClientResult<T>**, в которой хранится коллекция потоков в своем свойстве [Value](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.ClientResult`1.Value.aspx) .
    
  

## <a name="iterate-through-and-read-from-the-social-feed-by-using-the-sharepoint-net-client-object-model"></a>Выполните итерацию по и ознакомьтесь с социальными веб-канал с помощью клиентской объектной модели SharePoint .NET
<a name="bkmk_ReadFeed"> </a>

Приведенный ниже код перебирает потоков в веб-канал. Проверяется, является ли каждый поток имеет атрибут  [CanReply](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThreadAttributes.CanReply.aspx) и затем получает идентификатор потока и текста post корневой. Код также создает словарь для хранения идентификатор потока (который используется для ответов на поток) и записывает текста post корневой на консоль.

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


## <a name="post-a-reply-to-the-social-feed-by-using-the-sharepoint-net-client-object-model"></a>Ответить социальные веб-канал с помощью клиента SharePoint .NET объектной модели
<a name="bkmk_WriteFeed"> </a>


1. (Связанные с Интерфейсом только) Получите поток для ответов, чтобы и запрос ответа пользователя.
    
```cs
Console.Write("Which post number do you want to reply to?  ");
string threadToReplyTo = "";
int threadNumber = int.Parse(Console.ReadLine()) - 1;
idDictionary.TryGetValue(threadNumber, out threadToReplyTo);
Console.Write("Type your reply:  ");
```

2. Определите ответ. Следующий код получает текст ответа из консольного приложения.
    
```cs
SocialPostCreationData postCreationData = new SocialPostCreationData();
postCreationData.ContentText = Console.ReadLine();
```

3. Публикация ответ. Параметр  _threadToReplyTo_ представляет свойства [Id](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialThread.Id.aspx) потока.
    
```cs
feedManager.CreatePost(threadToReplyTo, postCreationData);
clientContext.ExecuteQuery();
```

    > [!NOTE]
    > The  [CreatePost](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.CreatePost.aspx) method is also used to publish a root post to the current user's feed by passing **null** for the first parameter.

4. (Связанные с Интерфейсом только) Выйти из программы.
    
    ```cs
    Console.WriteLine("Your reply was published.");
    Console.ReadKey(false);
    ```

5. Тестирование консольного приложения в строке меню выберите команду **Отладка**, **Начать отладку**.
    
  

## <a name="code-example-retrieve-a-feed-and-reply-to-a-post-by-using-the-sharepoint-net-client-object-model"></a>Пример кода: получение веб-канал и ответить на сообщение с помощью клиентской объектной модели SharePoint .NET
<a name="bkmk_CodeExample"> </a>

Следующий пример является полный код из файла Program.cs.
  
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


## <a name="next-steps"></a>Дальнейшие действия
<a name="SP15ReadWriteSocial_nextsteps"> </a>

Чтобы узнать, как для более чтения задачи и записи задач с социальными веб-канал с помощью клиентской объектной модели .NET, см.:
  
    
    

-  [Как: Создание и удаление сообщений и извлечение социальных веб-канал с помощью клиентской объектной модели .NET в SharePoint](how-to-create-and-delete-posts-and-retrieve-the-social-feed-by-using-the-net-cli.md)
    
  

## <a name="see-also"></a>См. также
<a name="SP15ReadWriteSocial_addlresources"> </a>


-  [Начало разработки с использованием социальных функций в SharePoint](get-started-developing-with-social-features-in-sharepoint.md)
    
  
-  [Работа с социальными веб-каналами в SharePoint](work-with-social-feeds-in-sharepoint.md)
    
  

