---
title: "Как создать \"и\" Удаление публикации и извлечение социальных веб-канал с помощью объектной модели JavaScript в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: e8c21960-6ea0-43c0-821e-2db2a0ecec90
ms.openlocfilehash: 168352c7225b43a54be6e39fc8bdf2eb1f8b7173
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-create-and-delete-posts-and-retrieve-the-social-feed-by-using-the-javascript-object-model-in-sharepoint"></a>Как: Создание и удаление сообщений и извлечение социальных веб-канал с помощью объектной модели JavaScript в SharePoint
Узнайте, как создавать и удалять записи микроблогов и восстанавливать каналы социальных сетей с помощью объектной модели JavaScript для SharePoint.
## <a name="what-are-social-feeds-in-sharepoint"></a>Что такое социальные веб-каналами в SharePoint
<a name="bk_intro"> </a>

В SharePoint социальные веб-канал представляет собой коллекцию потоков, которые представляют бесед, публикации в одном микроблога или уведомления. Потоки имеют корневой post и коллекцию публикации в ответ. В объектной модели JavaScript веб-каналов, представленные объектами [SocialFeed](http://msdn.microsoft.com/library/356c5475-2fd6-a655-c271-5d7f21af45e2%28Office.15%29.aspx) , потоки, представленные объектами [SocialThread](http://msdn.microsoft.com/library/46aa4beb-d708-f20e-471e-626c8a7efab7%28Office.15%29.aspx) и публикации и ответы, представленные объектами [SocialPost](http://msdn.microsoft.com/library/a761ce71-d3d7-420a-1e06-962674124dfa%28Office.15%29.aspx) . Для выполнения основных задач, связанных с веб-канал, используйте объект [SocialFeedManager](http://msdn.microsoft.com/library/651fdf0f-841d-88f9-1e07-fcb3ad8c9410%28Office.15%29.aspx) . В этой статье мы покажем, как создать страницу приложения, использующего объектной модели JavaScript для работы с социальными веб-каналами.
  
    
    
Дополнительные сведения о работе с [SocialFeedManager](http://msdn.microsoft.com/library/651fdf0f-841d-88f9-1e07-fcb3ad8c9410%28Office.15%29.aspx) , а также сведения об использовании других API-интерфейсы для работы с социальными веб-каналами просмотрите [Работа с социальными веб-каналами в SharePoint](work-with-social-feeds-in-sharepoint.md).
  
    
    

## <a name="prerequisites-for-setting-up-your-development-environment-to-work-with-social-feeds-in-the-sharepoint-javascript-object-model"></a>Необходимые условия для настройки среды разработки для работы с социальными веб-каналами в объектной модели SharePoint JavaScript
<a name="bkmk_SetUpDevEnv"> </a>

Чтобы создать страницу приложения, использующего JavaScript объектной модели для работы с социальными веб-каналов, то необходимо:
  
    
    

- SharePoint с помощью личного сайта настроен в открытом виде, личные сайты, созданные для текущего пользователя и конечного пользователя, выполнив конечного пользователя текущего пользователя и несколько записей, записанные центром конечного пользователя
    
  
- Visual Studio 2012 или Visual Studio 2013 с Инструменты разработчика Office для Visual Studio 2013
    
  
- **Полный** доступ для приложения-службы профилей пользователей и разрешения на развертывание решения фермы для пользователя, вошедшего в систему
    
  
- Достаточные разрешения для учетной записи пула приложений для доступа к базе данных контента личных сайтов веб-приложения
    
  

## <a name="create-an-application-page-that-works-with-social-feeds-by-using-the-sharepoint-javascript-object-model"></a>Создайте страницу приложения, работающего с социальными веб-каналами с помощью объектной модели SharePoint JavaScript
<a name="bk_CreateApp"> </a>


1. Откройте Visual Studio и в меню **Файл** последовательно выберите элементы **Создать** и **Проект**.
    
  
2. В диалоговом окне **Новый проект** выберите **.NET Framework 4.5** из раскрывающегося списка в верхней части окна.
    
  
3. В списке **Шаблоны** разверните узел **Office SharePoint**, выберите категорию **Решений SharePoint** и затем выберите шаблон **Проекта SharePoint** .
    
  
4. Назовите проект SocialFeedJSOMи затем нажмите кнопку **ОК**.
    
  
5. В диалоговом окне **Мастер настройки SharePoint** выберите **Развернуть как решение фермы** и затем нажмите кнопку **Готово**.
    
  
6. В **Обозревателе решений** откройте контекстное меню для проектаSocialFeedJSOM и добавьте SharePoint "Макеты" сопоставленная папка.
    
  
7. В папке **Layouts** откройте контекстное меню для папкиSocialFeedJSOM и добавьте новую страницу приложения SharePoint с именемSocialFeed.aspx.
    
  > Примечание: Примеры кода в этой статье определить пользовательский код в разметке страницы, но не используйте класс фонового кода, который создает Visual Studio для страницы. 

8. Откройте контекстное меню для страницы SocialFeed.aspx и затем выберите команду **назначить элемент**.
    
  
9. В разметке страницы SocialFeed.aspx определяющие элементы управления внутри тегов **asp:Content** «Главная», как показано в следующем коде.
    
```HTML
<table width="100%" id="tblPosts"></table><br/>
<button id="btnDelete" type="button"></button><br />
<span id="spanMessage" style="color: #FF0000;"></span>
```

  > Примечание: Эти элементы управления не могут быть использованы в каждом сценарии. Например «опубликовать публикации и ответы» сценарий только использует элемент управления **охватывать** .

10. После закрывающего тега **span**, добавьте элементы управления **SharePoint:ScriptLink**, элемент управления **SharePoint:FormDigest** и **script** тегов, как показано в следующем коде. Теги **SharePoint:ScriptLink** ссылку файлов библиотеки классов, которые определяют JavaScript объектной модели, которые можно использовать для разработки Личный сайт. Тег **SharePoint:FormDigest** создает сообщение дайджеста для проверки подлинности при необходимости в операции, обновлять содержимое сервера.
    
```HTML
<SharePoint:ScriptLink ID="ScriptLink1" name="SP.js" runat="server" ondemand="false" localizable="false" loadafterui="true" />
<SharePoint:ScriptLink ID="ScriptLink2" name="SP.UserProfiles.js" runat="server" ondemand="false" localizable="false" loadafterui="true" />
<SharePoint:FormDigest id="FormDigest" runat="server"/>
<script type="text/javascript">
    // Replace this comment with the code for your scenario.
</script>
```

11. Чтобы добавить логику для работы с веб-каналами, замените комментарий между тегами **script** с пример кода из одного из следующих сценариев:
    
  -  [Публикация сообщения и ответы, которые социальные веб-канал](how-to-create-and-delete-posts-and-retrieve-the-social-feed-by-using-the-javascr.md#bkmk_PubPosts)
  -  [Извлечение социальных веб-каналов](how-to-create-and-delete-posts-and-retrieve-the-social-feed-by-using-the-javascr.md#bkmk_GetFeeds)
  -  [Удаление публикации и ответы из социальных канала](how-to-create-and-delete-posts-and-retrieve-the-social-feed-by-using-the-javascr.md#bkmk_DeletePosts)
    
  
12. Тестирование страницы приложения в строке меню выберите **Отладка**, **Начать отладку**. Если запрос на изменение файла web.config, нажмите кнопку **ОК**.
    
  Если ответ вызывает метод обратного вызова сбоя, задайте точку останова в методе и Добавить контрольное значение в объекте **args** или проверьте журналы ULS и средство просмотра событий для получения дополнительных сведений.
    
  

## <a name="code-example-publish-posts-and-replies-to-the-social-feed-by-using-the-sharepoint-javascript-object-model"></a>Пример кода: публикация публикации и ответы, которые социальные веб-канал с помощью объектной модели SharePoint JavaScript
<a name="bkmk_PubPosts"> </a>

В следующем примере кода публикует сообщение и ее в ответ. В нем показано, как:
  
    
    

- После определения содержимого. В этом примере ссылка в записи.
    
  
- Публикация post на канал для текущего пользователя, используя метод **createPost** и передача **null** в качестве параметра _targetId_.
    
  
- Ответ на публикацию с помощью метода **createPost**, передав в качестве параметра _targetId_ идентификатор потока.
    
  

> **Примечание:** Вставьте следующий код между тегами **сценария** , которые добавлены в процедуре ["создать приложение"](how-to-create-and-delete-posts-and-retrieve-the-social-feed-by-using-the-javascr.md#bk_CreateApp) .
  
    
    


```javascript
// Ensure that the SP.UserProfiles.js file is loaded before the custom code runs.
SP.SOD.executeOrDelayUntilScriptLoaded(PublishPost, 'SP.UserProfiles.js');

// Declare global variables.
var clientContext;
var feedManager;
var resultThread;

function PublishPost() {

    // Initialize the current client context and the SocialFeedManager instance.
    clientContext = SP.ClientContext.get_current();
    feedManager = new SP.Social.SocialFeedManager(clientContext);

    // Create a link to include in the post.
    var linkDataItem = new SP.Social.SocialDataItem();
    linkDataItem.set_itemType(SP.Social.SocialDataItemType.link);
    linkDataItem.set_text('link');
    linkDataItem.set_uri('http://bing.com');
    var socialDataItems = [ linkDataItem ];

    // Create the post content.
    var postCreationData = new SP.Social.SocialPostCreationData();
    postCreationData.set_contentText('The text for the post, which contains a {0}.');
    postCreationData.set_contentItems(socialDataItems);

    // Publish the post. Pass null for the "targetId" parameter because this is a root post.
    resultThread = feedManager.createPost(null, postCreationData);
    clientContext.executeQueryAsync(PublishReply, PostFailed);
    }
function PublishReply(sender, args) {

    // Create the reply content.
    var postCreationData = new SP.Social.SocialPostCreationData();
    postCreationData.set_contentText('The text for the reply.');

    // Publish the reply.
    resultThread = feedManager.createPost(resultThread.get_id(), postCreationData);
    clientContext.executeQueryAsync(PostSucceeded, PostFailed);
}
function PostSucceeded(sender, args) {
    $get("spanMessage").innerText = 'The post and reply were published.';
}
function PostFailed(sender, args) {
    $get("spanMessage").innerText = 'Request failed: ' + args.get_message();
}
```


## <a name="code-example-retrieve-social-feeds-by-using-the-sharepoint-javascript-object-model"></a>Пример кода: получение социальными веб-каналами с помощью объектной модели SharePoint JavaScript
<a name="bkmk_GetFeeds"> </a>

В следующем примере кода показано получение веб-каналов для текущего пользователя и конечного пользователя. В нем показано, как:
  
    
    

- Получите **Personal**, **News**и **Timeline** канал типов для текущего пользователя с помощью метода **getFeed**.
    
  
- Получите **Personal** канал типа для конечного пользователя с помощью метода **getFeedFor**.
    
  
- Выполните итерацию по веб-каналы, чтобы найти все потоки, не являющиеся ссылку и для получения сведений о потоков и публикации. Справочник по потоков представляют уведомлений, которые содержат сведения о другого потока. Например, если пользователь упоминания другого пользователя в записи, сервера создает **MentionReference**-введите поток, который содержит ссылки на исходное сообщение и другие метаданные о post.
    
  
Дополнительные сведения о типах веб-канала активности можно [Обзор типов веб-канала активности в социальных API личных сайтов](work-with-social-feeds-in-sharepoint.md#bkmk_FeedTypes). Дополнительные сведения о потоках ссылку можно [ссылку потоки и потоки дайджест в веб-каналов социальных SharePoint](reference-threads-and-digest-threads-in-sharepoint-server-social-feeds.md).
  
    
    

> **Примечание:** Вставьте следующий код между тегами **сценария** , которые добавлены в процедуре ["создать приложение"](how-to-create-and-delete-posts-and-retrieve-the-social-feed-by-using-the-javascr.md#bk_CreateApp) . Измените значение заполнитель для переменной **targetUser** до выполнения этого кода.
  
    
    




```cs
// Replace the placeholder value with the account name of the target user.
var targetUser = 'domainName\\\\userName';

// Ensure that the SP.UserProfiles.js file is loaded before the custom code runs.
SP.SOD.executeOrDelayUntilScriptLoaded(GetFeeds, 'SP.UserProfiles.js');

// Declare global variables.
var clientContext;
var feedManager;
var personalFeed;
var newsFeed;
var timelineFeed;
var targetUserFeed;

function GetFeeds() {

    // Initialize the current client context and the SocialFeedManager instance.
    clientContext = SP.ClientContext.get_current();
    feedManager = new SP.Social.SocialFeedManager(clientContext);

    // Set parameters for the feed content that you want to retrieve.
    var feedOptions = new SP.Social.SocialFeedOptions();
    feedOptions.set_maxThreadCount(10); // default is 20

    // Get all feed types for current user and get the Personal feed
    // for the target user.
    personalFeed = feedManager.getFeed(SP.Social.SocialFeedType.personal, feedOptions);
    newsFeed = feedManager.getFeed(SP.Social.SocialFeedType.news, feedOptions);
    targetUserFeed = feedManager.getFeedFor(targetUser, feedOptions);

    // Change the sort order to optimize the Timeline feed results.
    feedOptions.set_sortOrder(SP.Social.SocialFeedSortOrder.byCreatedTime); 
    timelineFeed = feedManager.getFeed(SP.Social.SocialFeedType.timeline, feedOptions);

    clientContext.load(feedManager);
    clientContext.executeQueryAsync(CallIterateFunctionForFeeds, RequestFailed);
}
function CallIterateFunctionForFeeds() {
    IterateThroughFeed(personalFeed, "Personal", true);
    IterateThroughFeed(newsFeed, "News", true);
    IterateThroughFeed(timelineFeed, "Timeline", true); 
    IterateThroughFeed(targetUserFeed, "Personal", false);
}
function IterateThroughFeed(feed, feedType, isCurrentUser) {
    tblPosts.insertRow().insertCell();
    var feedHeaderRow = tblPosts.insertRow();
    var feedOwner = feedManager.get_owner().get_name();

    // Iterate through the array of threads in the feed.
    var threads = feed.get_threads();
    for (var i = 0; i < threads.length ; i++) {
        var thread = threads[i];
        var actors = thread.get_actors();

        if (i == 0) {

            // Get the name of the target user for the feed header row. Users are 
            // owners of all threads in their Personal feed.
            if (!isCurrentUser) {
                feedOwner = actors[thread.get_ownerIndex()].get_name();
            }
            feedHeaderRow.insertCell().innerText = feedType.toUpperCase() + ' FEED FOR '
                + feedOwner.toUpperCase();
        }

        // Use only Normal-type threads and ignore reference-type threads. (SocialThreadType.Normal = 0)
        if (thread.get_threadType() == 0) {

            // Get the root post's author, content, and number of replies.
            var post = thread.get_rootPost();
            var authorName = actors[post.get_authorIndex()].get_name();
            var postContent = post.get_text();
            var totalReplies = thread.get_totalReplyCount();

            var postRow = tblPosts.insertRow();
            postRow.insertCell().innerText = authorName + ' posted \\"' + postContent
                + '\\" (' + totalReplies + ' replies)';

            // If there are any replies, iterate through the array and
            // get the author and content. 
            // If a thread contains more than two replies, the server
            // returns a thread digest that contains only the two most
            // recent replies. To get all replies, call the 
            // SocialFeedManager.getFullThread method.
            if (totalReplies > 0) {
                var replies = thread.get_replies();

                for (var j = 0; j < replies.length; j++) {
                    var replyRow = tblPosts.insertRow();

                    var reply = replies[j];
                    replyRow.insertCell().innerText = '  - ' + actors[reply.get_authorIndex()].get_name()
                        + ' replied \\"' + reply.get_text() + '\\"';
                }
            }
        }
    }
}
function RequestFailed(sender, args) {
    $get("spanMessage").innerText = 'Request failed: ' + args.get_message();
}
```


## <a name="code-example-delete-posts-and-replies-from-the-social-feed-by-using-the-sharepoint-javascript-object-model"></a>Пример кода: Delete публикации и ответы из социальных канала с помощью объектной модели SharePoint JavaScript
<a name="bkmk_DeletePosts"> </a>

В следующем примере кода удаляется публикация или ответ. В нем показано, как:
  
    
    

- Получите **News** канал типа для текущего пользователя с помощью метода **getFeed**.
    
  
- Выполните итерацию по публикации и ответы в веб-канал, чтобы получить свойство **id**, которая используется для удаления публикация или ответ.
    
  
- Удаление корневого публикация или ответ с помощью метода **deletePost** (корневой post при удалении весь поток).
    
  

> **Примечание:** Вставьте следующий код между тегами **сценария** , которые добавлены в процедуре ["создать приложение"](how-to-create-and-delete-posts-and-retrieve-the-social-feed-by-using-the-javascr.md#bk_CreateApp) . В этом примере предполагается, что текущий пользователь канал новостей содержит по крайней мере один post.
  
    
    


```cs
// Ensure that the SP.UserProfiles.js file is loaded before the custom code runs.
SP.SOD.executeOrDelayUntilScriptLoaded(GetFeeds, 'SP.UserProfiles.js');

// Declare global variables.
var clientContext;
var feedManager;
var feed;
var postOrReplyToDelete;

function GetFeeds() {

    // Initialize the current client context and the SocialFeedManager instance.
    clientContext = SP.ClientContext.get_current();
    feedManager = new SP.Social.SocialFeedManager(clientContext);

    // Set parameters for the feed content that you want to retrieve.
    var feedOptions = new SP.Social.SocialFeedOptions();
    feedOptions.set_maxThreadCount(10); // default is 20

    // Get all the News feed type for current user.
    feed = feedManager.getFeed(SP.Social.SocialFeedType.news, feedOptions);
    clientContext.executeQueryAsync(IterateThroughFeed, RequestFailed);
}
function IterateThroughFeed() {

    // Iterate through the array of threads in the feed.
    var threads = feed.get_threads();
    for (var i = 0; i < threads.length ; i++) {
        var thread = threads[i];
        var actors = thread.get_actors();

        // Get the root post's author, content, and number of replies.
        var post = thread.get_rootPost();

        var authorName = actors[post.get_authorIndex()].get_name();
        var postContent = post.get_text();
        var totalReplies = thread.get_totalReplyCount();

        var postRow = tblPosts.insertRow();
        postRow.insertCell().innerText = authorName + ' posted \\"' + postContent
            + '\\" (' + totalReplies + ' replies)';
        postOrReplyToDelete = post.get_id();

        // If there are any replies, iterate through the array and
        // get the author and content.
            // If a thread contains more than two replies, the server
            // returns a thread digest that contains only the two most
            // recent replies. To get all replies, call the 
            // SocialFeedManager.getFullThread method.
        if (totalReplies > 0) {
            var replies = thread.get_replies();
            for (var j = 0; j < replies.length; j++) {
                var replyRow = tblPosts.insertRow();

                var reply = replies[j];
                replyRow.insertCell().innerText = '  - ' + actors[reply.get_authorIndex()].get_name()
                    + ' replied \\"' + reply.get_text() + '\\"';
                postOrReplyToDelete = reply.get_id();
            }
        }

        // Initialize button properties.
        $get("btnDelete").onclick = function () { DeletePostOrReply(); };
        $get("btnDelete").innerText = 'Click to delete the last post or reply';
    }
}

// Delete the last post or reply listed on the page.
function DeletePostOrReply() {
    feedManager.deletePost(postOrReplyToDelete);
    clientContext.executeQueryAsync(DeleteSucceeded, RequestFailed);
}
function DeleteSucceeded(sender, args) {
    $get("spanMessage").innerText = 'The post or reply was deleted. Refresh the page to see your changes.';
}
function RequestFailed(sender, args) {
    $get("spanMessage").innerText = 'Request failed: ' + args.get_message();
}
```


## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="bk_addResources"> </a>


-  [Работа с социальными веб-каналами в SharePoint](work-with-social-feeds-in-sharepoint.md)
    
  
-  [SP. Пространство имен социальных (sp.userprofiles)](http://msdn.microsoft.com/library/43d47f01-c085-0e77-bd01-48bcb7d5bb35%28Office.15%29.aspx)
    
  
-  [Как: Создание и удаление сообщений и извлечение социальных веб-канал с помощью клиентской объектной модели .NET в SharePoint](how-to-create-and-delete-posts-and-retrieve-the-social-feed-by-using-the-net-cli.md)
    
  
-  [Как: сведения для чтения и записи социальных канал с помощью службы REST в SharePoint](how-to-learn-to-read-and-write-to-the-social-feed-by-using-the-rest-service-in-s.md)
    
  
-  [Справочник по потоки и потоки дайджест в веб-каналов социальных SharePoint](reference-threads-and-digest-threads-in-sharepoint-server-social-feeds.md)
    
  

