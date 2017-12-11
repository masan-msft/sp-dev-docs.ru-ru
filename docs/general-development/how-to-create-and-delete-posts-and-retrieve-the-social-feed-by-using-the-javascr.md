---
title: "Создание и удаление сообщений и извлечение социальных веб-канал с помощью объектной модели JavaScript в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: e8c21960-6ea0-43c0-821e-2db2a0ecec90
ms.openlocfilehash: 4963dbb97f6106c9536353112e9f4a2ffb15c5b4
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="create-and-delete-posts-and-retrieve-the-social-feed-by-using-the-javascript-object-model-in-sharepoint"></a><span data-ttu-id="36f2c-102">Создание и удаление сообщений и извлечение социальных веб-канал с помощью объектной модели JavaScript в SharePoint</span><span class="sxs-lookup"><span data-stu-id="36f2c-102">Create and delete posts and retrieve the social feed by using the JavaScript object model in SharePoint</span></span>

<span data-ttu-id="36f2c-103">Узнайте, как создавать и удалять записи микроблогов, а также восстанавливать каналы, используя объектную модель JavaScript для SharePoint.</span><span class="sxs-lookup"><span data-stu-id="36f2c-103">Learn how to create and delete microblog posts and retrieve social feeds by using the SharePoint JavaScript object model.</span></span>

## <a name="what-are-social-feeds-in-sharepoint"></a><span data-ttu-id="36f2c-104">Что такое социальные веб-каналами в SharePoint</span><span class="sxs-lookup"><span data-stu-id="36f2c-104">What are social feeds in SharePoint?</span></span>
<span data-ttu-id="36f2c-105"><a name="bk_intro"> </a></span><span class="sxs-lookup"><span data-stu-id="36f2c-105"><a name="bk_intro"> </a></span></span>

<span data-ttu-id="36f2c-106">В SharePoint социальные веб-канал представляет собой коллекцию потоков, которые представляют бесед, публикации в одном микроблога или уведомления.</span><span class="sxs-lookup"><span data-stu-id="36f2c-106">In SharePoint, a social feed is a collection of threads that represent conversations, single microblog posts, or notifications.</span></span> <span data-ttu-id="36f2c-107">Потоки имеют корневой post и коллекцию публикации в ответ.</span><span class="sxs-lookup"><span data-stu-id="36f2c-107">Threads contain a root post and a collection of reply posts.</span></span> <span data-ttu-id="36f2c-108">В объектной модели JavaScript веб-каналов, представленные объектами [SocialFeed](http://msdn.microsoft.com/library/356c5475-2fd6-a655-c271-5d7f21af45e2%28Office.15%29.aspx) , потоки, представленные объектами [SocialThread](http://msdn.microsoft.com/library/46aa4beb-d708-f20e-471e-626c8a7efab7%28Office.15%29.aspx) и публикации и ответы, представленные объектами [SocialPost](http://msdn.microsoft.com/library/a761ce71-d3d7-420a-1e06-962674124dfa%28Office.15%29.aspx) .</span><span class="sxs-lookup"><span data-stu-id="36f2c-108">In the JavaScript object model, feeds are represented by  [SocialFeed](http://msdn.microsoft.com/library/356c5475-2fd6-a655-c271-5d7f21af45e2%28Office.15%29.aspx) objects, threads are represented by [SocialThread](http://msdn.microsoft.com/library/46aa4beb-d708-f20e-471e-626c8a7efab7%28Office.15%29.aspx) objects, and post and replies are represented by [SocialPost](http://msdn.microsoft.com/library/a761ce71-d3d7-420a-1e06-962674124dfa%28Office.15%29.aspx) objects.</span></span> <span data-ttu-id="36f2c-109">Для выполнения основных задач, связанных с веб-канал, используйте объект [SocialFeedManager](http://msdn.microsoft.com/library/651fdf0f-841d-88f9-1e07-fcb3ad8c9410%28Office.15%29.aspx) .</span><span class="sxs-lookup"><span data-stu-id="36f2c-109">To perform core feed-related tasks, you use the [SocialFeedManager](http://msdn.microsoft.com/library/651fdf0f-841d-88f9-1e07-fcb3ad8c9410%28Office.15%29.aspx) object.</span></span> <span data-ttu-id="36f2c-110">В этой статье мы покажем, как создать страницу приложения, использующего объектной модели JavaScript для работы с социальными веб-каналами.</span><span class="sxs-lookup"><span data-stu-id="36f2c-110">In this article, we'll show you how to create an application page that uses the JavaScript object model to work with social feeds.</span></span>
  
    
    
<span data-ttu-id="36f2c-111">Дополнительные сведения о работе с [SocialFeedManager](http://msdn.microsoft.com/library/651fdf0f-841d-88f9-1e07-fcb3ad8c9410%28Office.15%29.aspx) , а также сведения об использовании других API-интерфейсы для работы с социальными веб-каналами просмотрите [Работа с социальными веб-каналами в SharePoint](work-with-social-feeds-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="36f2c-111">For more information about working with  [SocialFeedManager](http://msdn.microsoft.com/library/651fdf0f-841d-88f9-1e07-fcb3ad8c9410%28Office.15%29.aspx) or for information about using other APIs to work with social feeds, see [Work with social feeds in SharePoint](work-with-social-feeds-in-sharepoint.md).</span></span>
  
    
    

## <a name="prerequisites-for-setting-up-your-development-environment-to-work-with-social-feeds-in-the-sharepoint-javascript-object-model"></a><span data-ttu-id="36f2c-112">Необходимые условия для настройки среды разработки для работы с социальными веб-каналами в объектной модели SharePoint JavaScript</span><span class="sxs-lookup"><span data-stu-id="36f2c-112">Prerequisites for setting up your development environment to work with social feeds in the SharePoint JavaScript object model</span></span>
<span data-ttu-id="36f2c-113"><a name="bkmk_SetUpDevEnv"> </a></span><span class="sxs-lookup"><span data-stu-id="36f2c-113"><a name="bkmk_SetUpDevEnv"> </a></span></span>

<span data-ttu-id="36f2c-114">Чтобы создать страницу приложения, использующего JavaScript объектной модели для работы с социальными веб-каналов, то необходимо:</span><span class="sxs-lookup"><span data-stu-id="36f2c-114">To create an application page that uses the JavaScript object model to work with social feeds, you'll need:</span></span>
  
    
    

- <span data-ttu-id="36f2c-115">SharePoint с помощью личного сайта настроен в открытом виде, личные сайты, созданные для текущего пользователя и конечного пользователя, выполнив конечного пользователя текущего пользователя и несколько записей, записанные центром конечного пользователя</span><span class="sxs-lookup"><span data-stu-id="36f2c-115">SharePoint with My Site configured as public, with personal sites created for the current user and a target user, with the current user following the target user, and with a few posts written by the target user</span></span>
    
  
- <span data-ttu-id="36f2c-116">Visual Studio 2012 или Visual Studio 2013 с Инструменты разработчика Office для Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="36f2c-116">Visual Studio 2012 or Visual Studio 2013 with Office Developer Tools for Visual Studio 2013</span></span>
    
  
- <span data-ttu-id="36f2c-117">**Полный** доступ для приложения-службы профилей пользователей и разрешения на развертывание решения фермы для пользователя, вошедшего в систему</span><span class="sxs-lookup"><span data-stu-id="36f2c-117">**Full Control** access permissions to the User Profile service application and permissions to deploy a farm solution for the logged-on user</span></span>
    
  
- <span data-ttu-id="36f2c-118">Достаточные разрешения для учетной записи пула приложений для доступа к базе данных контента личных сайтов веб-приложения</span><span class="sxs-lookup"><span data-stu-id="36f2c-118">Sufficient permissions for the application pool account to access the content database of the My Sites web application</span></span>
    
  

## <a name="create-an-application-page-that-works-with-social-feeds-by-using-the-sharepoint-javascript-object-model"></a><span data-ttu-id="36f2c-119">Создайте страницу приложения, работающего с социальными веб-каналами с помощью объектной модели SharePoint JavaScript</span><span class="sxs-lookup"><span data-stu-id="36f2c-119">Create an application page that works with social feeds by using the SharePoint JavaScript object model</span></span>
<span data-ttu-id="36f2c-120"><a name="bk_CreateApp"> </a></span><span class="sxs-lookup"><span data-stu-id="36f2c-120"><a name="bk_CreateApp"> </a></span></span>


1. <span data-ttu-id="36f2c-121">Откройте Visual Studio и в меню **Файл** последовательно выберите элементы **Создать** и **Проект**.</span><span class="sxs-lookup"><span data-stu-id="36f2c-121">Open Visual Studio and choose **File**, **New**, **Project**.</span></span>
    
  
2. <span data-ttu-id="36f2c-122">В диалоговом окне **Новый проект** выберите **.NET Framework 4.5** из раскрывающегося списка в верхней части окна.</span><span class="sxs-lookup"><span data-stu-id="36f2c-122">In the **New Project** dialog box, choose **.NET Framework 4.5** from the drop-down list at the top of the dialog box.</span></span>
    
  
3. <span data-ttu-id="36f2c-123">В списке **Шаблоны** разверните узел **Office SharePoint**, выберите категорию **Решений SharePoint** и затем выберите шаблон **Проекта SharePoint** .</span><span class="sxs-lookup"><span data-stu-id="36f2c-123">In the **Templates** list, expand **Office SharePoint**, choose the **SharePoint Solutions** category, and then choose the **SharePoint Project** template.</span></span>
    
  
4. <span data-ttu-id="36f2c-124">Назовите проект SocialFeedJSOMи затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="36f2c-124">Name the project SocialFeedJSOM, and then choose the **OK** button.</span></span>
    
  
5. <span data-ttu-id="36f2c-125">В диалоговом окне **Мастер настройки SharePoint** выберите **Развернуть как решение фермы** и затем нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="36f2c-125">In the **SharePoint Customization Wizard** dialog box, choose **Deploy as a farm solution**, and then choose the **Finish** button.</span></span>
    
  
6. <span data-ttu-id="36f2c-126">В **Обозревателе решений** откройте контекстное меню для проектаSocialFeedJSOM и добавьте SharePoint "Макеты" сопоставленная папка.</span><span class="sxs-lookup"><span data-stu-id="36f2c-126">In **Solution Explorer**, open the shortcut menu for the SocialFeedJSOM project, and then add a SharePoint "Layouts" mapped folder.</span></span>
    
  
7. <span data-ttu-id="36f2c-127">В папке **Layouts** откройте контекстное меню для папкиSocialFeedJSOM и добавьте новую страницу приложения SharePoint с именемSocialFeed.aspx.</span><span class="sxs-lookup"><span data-stu-id="36f2c-127">In the **Layouts** folder, open the shortcut menu for theSocialFeedJSOM folder, and then add a new SharePoint application page namedSocialFeed.aspx.</span></span>
    
  > <span data-ttu-id="36f2c-128">Примечание: Примеры кода в этой статье определить пользовательский код в разметке страницы, но не используйте класс фонового кода, который создает Visual Studio для страницы.</span><span class="sxs-lookup"><span data-stu-id="36f2c-128">Note: The code examples in this article define custom code in the page markup but do not use the code-behind class that Visual Studio creates for the page.</span></span> 

8. <span data-ttu-id="36f2c-129">Откройте контекстное меню для страницы SocialFeed.aspx и затем выберите команду **назначить элемент**.</span><span class="sxs-lookup"><span data-stu-id="36f2c-129">Open the shortcut menu for the SocialFeed.aspx page, and then choose **Set as Startup Item**.</span></span>
    
  
9. <span data-ttu-id="36f2c-130">В разметке страницы SocialFeed.aspx определяющие элементы управления внутри тегов **asp:Content** «Главная», как показано в следующем коде.</span><span class="sxs-lookup"><span data-stu-id="36f2c-130">In the markup for the SocialFeed.aspx page, define controls inside the "Main" **asp:Content** tags, as shown in the following code.</span></span>
    
```HTML
<table width="100%" id="tblPosts"></table><br/>
<button id="btnDelete" type="button"></button><br />
<span id="spanMessage" style="color: #FF0000;"></span>
```

  > <span data-ttu-id="36f2c-131">Примечание: Эти элементы управления не могут быть использованы в каждом сценарии.</span><span class="sxs-lookup"><span data-stu-id="36f2c-131">Note: These controls may not be used in every scenario.</span></span> <span data-ttu-id="36f2c-132">Например «опубликовать публикации и ответы» сценарий только использует элемент управления **охватывать** .</span><span class="sxs-lookup"><span data-stu-id="36f2c-132">For example, the "Publish posts and replies" scenario only uses the **span** control.</span></span>

10. <span data-ttu-id="36f2c-p103">После закрывающего тега **span**, добавьте элементы управления **SharePoint:ScriptLink**, элемент управления **SharePoint:FormDigest** и **script** тегов, как показано в следующем коде. Теги **SharePoint:ScriptLink** ссылку файлов библиотеки классов, которые определяют JavaScript объектной модели, которые можно использовать для разработки Личный сайт. Тег **SharePoint:FormDigest** создает сообщение дайджеста для проверки подлинности при необходимости в операции, обновлять содержимое сервера.</span><span class="sxs-lookup"><span data-stu-id="36f2c-p103">After the closing **span** tag, add **SharePoint:ScriptLink** controls, a **SharePoint:FormDigest** control, and **script** tags, as shown in the following code. The **SharePoint:ScriptLink** tags reference the class library files that define the JavaScript object model that you can use for My Site Social development. The **SharePoint:FormDigest** tag generates a message digest for security validation when required by operations that update server content.</span></span>
    
```HTML
<SharePoint:ScriptLink ID="ScriptLink1" name="SP.js" runat="server" ondemand="false" localizable="false" loadafterui="true" />
<SharePoint:ScriptLink ID="ScriptLink2" name="SP.UserProfiles.js" runat="server" ondemand="false" localizable="false" loadafterui="true" />
<SharePoint:FormDigest id="FormDigest" runat="server"/>
<script type="text/javascript">
    // Replace this comment with the code for your scenario.
</script>
```

11. <span data-ttu-id="36f2c-136">Чтобы добавить логику для работы с веб-каналами, замените комментарий между тегами **script** с пример кода из одного из следующих сценариев:</span><span class="sxs-lookup"><span data-stu-id="36f2c-136">To add the logic to work with feeds, replace the comment between the **script** tags with the code example from one of the following scenarios:</span></span>
    
  -  [<span data-ttu-id="36f2c-137">Публикация сообщения и ответы, которые социальные веб-канал</span><span class="sxs-lookup"><span data-stu-id="36f2c-137">Publish posts and replies to the social feed</span></span>](how-to-create-and-delete-posts-and-retrieve-the-social-feed-by-using-the-javascr.md#bkmk_PubPosts)
  -  [<span data-ttu-id="36f2c-138">Извлечение социальных веб-каналов</span><span class="sxs-lookup"><span data-stu-id="36f2c-138">Retrieve social feeds</span></span>](how-to-create-and-delete-posts-and-retrieve-the-social-feed-by-using-the-javascr.md#bkmk_GetFeeds)
  -  [<span data-ttu-id="36f2c-139">Удаление публикации и ответы из социальных канала</span><span class="sxs-lookup"><span data-stu-id="36f2c-139">Delete posts and replies from the social feed</span></span>](how-to-create-and-delete-posts-and-retrieve-the-social-feed-by-using-the-javascr.md#bkmk_DeletePosts)
    
  
12. <span data-ttu-id="36f2c-p104">Тестирование страницы приложения в строке меню выберите **Отладка**, **Начать отладку**. Если запрос на изменение файла web.config, нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="36f2c-p104">To test the application page, on the menu bar, choose **Debug**, **Start Debugging**. If you are prompted to modify the web.config file, choose the **OK** button.</span></span>
    
  <span data-ttu-id="36f2c-142">Если ответ вызывает метод обратного вызова сбоя, задайте точку останова в методе и Добавить контрольное значение в объекте **args** или проверьте журналы ULS и средство просмотра событий для получения дополнительных сведений.</span><span class="sxs-lookup"><span data-stu-id="36f2c-142">If the response calls the failure callback method, set a breakpoint in the method and add a watch on the **args** object or check the ULS logs and the event viewer for more information.</span></span>
    
  

## <a name="code-example-publish-posts-and-replies-to-the-social-feed-by-using-the-sharepoint-javascript-object-model"></a><span data-ttu-id="36f2c-143">Пример кода: публикация публикации и ответы, которые социальные веб-канал с помощью объектной модели SharePoint JavaScript</span><span class="sxs-lookup"><span data-stu-id="36f2c-143">Code example: Publish posts and replies to the social feed by using the SharePoint JavaScript object model</span></span>
<span data-ttu-id="36f2c-144"><a name="bkmk_PubPosts"> </a></span><span class="sxs-lookup"><span data-stu-id="36f2c-144"><a name="bkmk_PubPosts"> </a></span></span>

<span data-ttu-id="36f2c-p105">В следующем примере кода публикует сообщение и ее в ответ. В нем показано, как:</span><span class="sxs-lookup"><span data-stu-id="36f2c-p105">The following code example publishes a post and a reply. It shows how to:</span></span>
  
    
    

- <span data-ttu-id="36f2c-p106">После определения содержимого. В этом примере ссылка в записи.</span><span class="sxs-lookup"><span data-stu-id="36f2c-p106">Define post content. This example includes a link in the post.</span></span>
    
  
- <span data-ttu-id="36f2c-149">Публикация post на канал для текущего пользователя, используя метод **createPost** и передача **null** в качестве параметра _targetId_.</span><span class="sxs-lookup"><span data-stu-id="36f2c-149">Publish a post to the current user's feed by using the **createPost** method and passing **null** as the _targetId_ parameter.</span></span>
    
  
- <span data-ttu-id="36f2c-150">Ответ на публикацию с помощью метода **createPost**, передав в качестве параметра _targetId_ идентификатор потока.</span><span class="sxs-lookup"><span data-stu-id="36f2c-150">Reply to a post by using the **createPost** method and passing the thread identifier as the _targetId_ parameter.</span></span>
    
> [!NOTE]
> <span data-ttu-id="36f2c-151">[!Примечание] Вставьте следующий код в тегах **script**, которые добавлены в процедуре ["создать приложение"](how-to-create-and-delete-posts-and-retrieve-the-social-feed-by-using-the-javascr.md#bk_CreateApp) .</span><span class="sxs-lookup"><span data-stu-id="36f2c-151">Paste the following code between the **script** tags that you added in the [Create the application page](how-to-create-and-delete-posts-and-retrieve-the-social-feed-by-using-the-javascr.md#bk_CreateApp) procedure.</span></span>
  
    
    


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


## <a name="code-example-retrieve-social-feeds-by-using-the-sharepoint-javascript-object-model"></a><span data-ttu-id="36f2c-152">Пример кода: получение социальными веб-каналами с помощью объектной модели SharePoint JavaScript</span><span class="sxs-lookup"><span data-stu-id="36f2c-152">Code example: Retrieve social feeds by using the SharePoint JavaScript object model</span></span>
<span data-ttu-id="36f2c-153"><a name="bkmk_GetFeeds"> </a></span><span class="sxs-lookup"><span data-stu-id="36f2c-153"><a name="bkmk_GetFeeds"> </a></span></span>

<span data-ttu-id="36f2c-p107">В следующем примере кода показано получение веб-каналов для текущего пользователя и конечного пользователя. В нем показано, как:</span><span class="sxs-lookup"><span data-stu-id="36f2c-p107">The following code example retrieves feeds for the current user and a target user. It shows how to:</span></span>
  
    
    

- <span data-ttu-id="36f2c-156">Получите **Personal**, **News**и **Timeline** канал типов для текущего пользователя с помощью метода **getFeed**.</span><span class="sxs-lookup"><span data-stu-id="36f2c-156">Get the **Personal**, **News**, and **Timeline** feed types for the current user by using the **getFeed** method.</span></span>
    
  
- <span data-ttu-id="36f2c-157">Получите **Personal** канал типа для конечного пользователя с помощью метода **getFeedFor**.</span><span class="sxs-lookup"><span data-stu-id="36f2c-157">Get the **Personal** feed type for a target user by using the **getFeedFor** method.</span></span>
    
  
- <span data-ttu-id="36f2c-p108">Выполните итерацию по веб-каналы, чтобы найти все потоки, не являющиеся ссылку и для получения сведений о потоков и публикации. Справочник по потоков представляют уведомлений, которые содержат сведения о другого потока. Например, если пользователь упоминания другого пользователя в записи, сервера создает **MentionReference**-введите поток, который содержит ссылки на исходное сообщение и другие метаданные о post.</span><span class="sxs-lookup"><span data-stu-id="36f2c-p108">Iterate through the feeds to find all non-reference threads and to get information about threads and posts. Reference threads represent notifications that contain information about another thread. For example, if a user mentions someone in a post, the server generates a **MentionReference**-type thread that contains the link to the original post and other metadata about the post.</span></span>
    
  
<span data-ttu-id="36f2c-161">Дополнительные сведения о типах веб-канала активности можно [Обзор типов веб-канала активности в социальных API личных сайтов](work-with-social-feeds-in-sharepoint.md#bkmk_FeedTypes).</span><span class="sxs-lookup"><span data-stu-id="36f2c-161">For more information about feed types, see  [Overview of feed types in the My Site Social API](work-with-social-feeds-in-sharepoint.md#bkmk_FeedTypes).</span></span> <span data-ttu-id="36f2c-162">Дополнительные сведения о потоках ссылку можно [ссылку потоки и потоки дайджест в веб-каналов социальных SharePoint](reference-threads-and-digest-threads-in-sharepoint-server-social-feeds.md).</span><span class="sxs-lookup"><span data-stu-id="36f2c-162">For more information about reference threads, see  [Reference threads and digest threads in SharePoint social feeds](reference-threads-and-digest-threads-in-sharepoint-server-social-feeds.md).</span></span>
  
> [!NOTE]
> <span data-ttu-id="36f2c-p110">[!Примечание] Вставьте следующий код в тегах **script**, которые добавлены в процедуре ["создать приложение"](how-to-create-and-delete-posts-and-retrieve-the-social-feed-by-using-the-javascr.md#bk_CreateApp) . Измените значение заполнитель для переменной **targetUser** до выполнения этого кода.</span><span class="sxs-lookup"><span data-stu-id="36f2c-p110">Paste the following code between the **script** tags that you added in the [Create the application page](how-to-create-and-delete-posts-and-retrieve-the-social-feed-by-using-the-javascr.md#bk_CreateApp) procedure. Then, change the placeholder value for the **targetUser** variable before you run the code.</span></span>
  
    
    




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


## <a name="code-example-delete-posts-and-replies-from-the-social-feed-by-using-the-sharepoint-javascript-object-model"></a><span data-ttu-id="36f2c-165">Пример кода: Delete публикации и ответы из социальных канала с помощью объектной модели SharePoint JavaScript</span><span class="sxs-lookup"><span data-stu-id="36f2c-165">Code example: Delete posts and replies from the social feed by using the SharePoint JavaScript object model</span></span>
<span data-ttu-id="36f2c-166"><a name="bkmk_DeletePosts"> </a></span><span class="sxs-lookup"><span data-stu-id="36f2c-166"><a name="bkmk_DeletePosts"> </a></span></span>

<span data-ttu-id="36f2c-p111">В следующем примере кода удаляется публикация или ответ. В нем показано, как:</span><span class="sxs-lookup"><span data-stu-id="36f2c-p111">The following code example deletes a post or a reply. It shows how to:</span></span>
  
    
    

- <span data-ttu-id="36f2c-169">Получите **News** канал типа для текущего пользователя с помощью метода **getFeed**.</span><span class="sxs-lookup"><span data-stu-id="36f2c-169">Get the **News** feed type for the current user by using the **getFeed** method.</span></span>
    
  
- <span data-ttu-id="36f2c-170">Выполните итерацию по публикации и ответы в веб-канал, чтобы получить свойство **id**, которая используется для удаления публикация или ответ.</span><span class="sxs-lookup"><span data-stu-id="36f2c-170">Iterate through the posts and replies in the feed to get the **id** property that you use to delete the post or reply.</span></span>
    
  
- <span data-ttu-id="36f2c-171">Удаление корневого публикация или ответ с помощью метода **deletePost** (корневой post при удалении весь поток).</span><span class="sxs-lookup"><span data-stu-id="36f2c-171">Delete a root post or reply by using the **deletePost** method (deleting a root post deletes the whole thread).</span></span>
    
> [!NOTE]
> <span data-ttu-id="36f2c-p112">[!Примечание] Вставьте следующий код в тегах **script**, которые добавлены в процедуре ["создать приложение"](how-to-create-and-delete-posts-and-retrieve-the-social-feed-by-using-the-javascr.md#bk_CreateApp) . В этом примере предполагается, что текущий пользователь канал новостей содержит по крайней мере один post.</span><span class="sxs-lookup"><span data-stu-id="36f2c-p112">Paste the following code between the **script** tags that you added in the [Create the application page](how-to-create-and-delete-posts-and-retrieve-the-social-feed-by-using-the-javascr.md#bk_CreateApp) procedure. This example assumes that the current user's newsfeed contains at least one post.</span></span>
  
    
    


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


## <a name="see-also"></a><span data-ttu-id="36f2c-174">См. также</span><span class="sxs-lookup"><span data-stu-id="36f2c-174">See also</span></span>
<span data-ttu-id="36f2c-175"><a name="bk_addResources"> </a></span><span class="sxs-lookup"><span data-stu-id="36f2c-175"><a name="bk_addResources"> </a></span></span>


-  [<span data-ttu-id="36f2c-176">Работа с социальными веб-каналами в SharePoint</span><span class="sxs-lookup"><span data-stu-id="36f2c-176">Work with social feeds in SharePoint</span></span>](work-with-social-feeds-in-sharepoint.md)
    
  
-  [<span data-ttu-id="36f2c-177">SP. Пространство имен социальных (sp.userprofiles)</span><span class="sxs-lookup"><span data-stu-id="36f2c-177">SP.Social namespace (sp.userprofiles)</span></span>](http://msdn.microsoft.com/library/43d47f01-c085-0e77-bd01-48bcb7d5bb35%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="36f2c-178">Как: Создание и удаление сообщений и извлечение социальных веб-канал с помощью клиентской объектной модели .NET в SharePoint</span><span class="sxs-lookup"><span data-stu-id="36f2c-178">How to: Create and delete posts and retrieve the social feed by using the .NET client object model in SharePoint</span></span>](how-to-create-and-delete-posts-and-retrieve-the-social-feed-by-using-the-net-cli.md)
    
  
-  [<span data-ttu-id="36f2c-179">Как: сведения для чтения и записи социальных канал с помощью службы REST в SharePoint</span><span class="sxs-lookup"><span data-stu-id="36f2c-179">How to: Learn to read and write to the social feed by using the REST service in SharePoint</span></span>](how-to-learn-to-read-and-write-to-the-social-feed-by-using-the-rest-service-in-s.md)
    
  
-  [<span data-ttu-id="36f2c-180">Справочник по потоки и потоки дайджест в веб-каналов социальных SharePoint</span><span class="sxs-lookup"><span data-stu-id="36f2c-180">Reference threads and digest threads in SharePoint social feeds</span></span>](reference-threads-and-digest-threads-in-sharepoint-server-social-feeds.md)
    
  

