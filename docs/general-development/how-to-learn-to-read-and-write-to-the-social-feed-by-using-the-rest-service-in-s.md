---
title: "Чтение и запись на социальные веб-канал с помощью службы REST в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 1da8d484-3666-42c3-8a8f-8b3ef93e96e9
ms.openlocfilehash: 2fafda13f6d5c6e62f7519bd9896c91a87dcc5f3
ms.sourcegitcommit: f6ea922341c38e700d0697961f8df9a454a03cba
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/15/2017
---
# <a name="read-and-write-to-the-social-feed-by-using-the-rest-service-in-sharepoint"></a><span data-ttu-id="2199e-102">Чтение и запись на социальные веб-канал с помощью службы REST в SharePoint</span><span class="sxs-lookup"><span data-stu-id="2199e-102">Read and write to the social feed by using the REST service in SharePoint</span></span>

<span data-ttu-id="2199e-103">Создайте приложение, размещенное в SharePoint, которое использует службу REST для публикации записи блога и получения личного веб-канала для текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="2199e-103">Create a SharePoint-hosted app that uses the REST service to publish a post and get the personal feed for the current user.</span></span>

## <a name="prerequisites-for-creating-a-sharepoint-hosted-sharepoint-add-in-that-publishes-a-post-and-gets-the-social-feed-by-using-the-sharepoint-rest-service"></a><span data-ttu-id="2199e-104">Необходимые условия для создания SharePoint хостингом SharePoint надстройки, которая публикует сообщение и получает социальные веб-канал с помощью службы SharePoint REST</span><span class="sxs-lookup"><span data-stu-id="2199e-104">Prerequisites for creating a SharePoint-hosted SharePoint Add-in that publishes a post and gets the social feed by using the SharePoint REST service</span></span>
<span data-ttu-id="2199e-105"><a name="bkmk_Prereqs"> </a></span><span class="sxs-lookup"><span data-stu-id="2199e-105"><a name="bkmk_Prereqs"> </a></span></span>

<span data-ttu-id="2199e-p101">В этой статье предполагается, что вы создаете надстройку для SharePoint с помощью Napa на сайте разработчика Office 365. Если вы используете эту среду разработки, то необходимые условия выполняются.</span><span class="sxs-lookup"><span data-stu-id="2199e-p101">This article assumes that you create the SharePoint Add-in by using Napa on an Office 365 Developer Site. If you're using this development environment, you've already met the prerequisites.</span></span>
  
    
    

> <span data-ttu-id="2199e-108">**Примечание:** Перейдите к [Настройка среды разработки для SharePoint надстройки на Office 365](http://msdn.microsoft.com/library/b22ce52a-ae9e-4831-9b68-c9210af6dc54%28Office.15%29.aspx) и узнайте, как зарегистрироваться на сайте разработчика и начать работу с использованием Napa.</span><span class="sxs-lookup"><span data-stu-id="2199e-108">**Note:** Go to  [Set up a development environment for SharePoint Add-ins on Office 365](http://msdn.microsoft.com/library/b22ce52a-ae9e-4831-9b68-c9210af6dc54%28Office.15%29.aspx) to find out how to sign up for a Developer Site and start using Napa.</span></span>
  
    
    

<span data-ttu-id="2199e-109">Если вы не используете Napa на сайте разработчика, то необходимо следующее:</span><span class="sxs-lookup"><span data-stu-id="2199e-109">If you're not using Napa on a Developer Site, you'll need the following:</span></span>
  
    
    

- <span data-ttu-id="2199e-110">SharePoint с личного сайта настроены и на личный сайт, созданный для текущего пользователя</span><span class="sxs-lookup"><span data-stu-id="2199e-110">SharePoint with My Site configured, and with a personal site created for the current user</span></span>
    
  
- <span data-ttu-id="2199e-111">Visual Studio 2012 и Инструменты разработчика Office для Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="2199e-111">Visual Studio 2012 and Office Developer Tools for Visual Studio 2013</span></span>
    
  
- <span data-ttu-id="2199e-112">**Полный** доступ к приложению-службе профилей пользователей для пользователя, вошедшего в систему</span><span class="sxs-lookup"><span data-stu-id="2199e-112">**Full Control** access permissions to the User Profile service application for the logged-on user</span></span>
    
  

> <span data-ttu-id="2199e-113">**Примечание:** [Начните создавать приложения для Office и SharePoint](http://msdn.microsoft.com/library/187f8c8c-1b15-471c-80b5-69a40e67deea.aspx)рекомендации о том, как настроить среду разработки, который соответствует требованиям, см.</span><span class="sxs-lookup"><span data-stu-id="2199e-113">**Note:** For guidance about how to set up a development environment that fits your needs, see  [Start building apps for Office and SharePoint](http://msdn.microsoft.com/library/187f8c8c-1b15-471c-80b5-69a40e67deea.aspx).</span></span> 
  
    
    


## <a name="core-concepts-to-know-about-working-with-sharepoint-social-feeds"></a><span data-ttu-id="2199e-114">Основные сведения о работе с социальными веб-каналами SharePoint</span><span class="sxs-lookup"><span data-stu-id="2199e-114">Core concepts to know about working with SharePoint social feeds</span></span>
<span data-ttu-id="2199e-115"><a name="bkmk_CoreConcepts"> </a></span><span class="sxs-lookup"><span data-stu-id="2199e-115"><a name="bkmk_CoreConcepts"> </a></span></span>

<span data-ttu-id="2199e-p102">Размещение в SharePoint приложение, создайте в этой статье использует JavaScript для создания и отправки HTTP-запросов к конечным точкам представлений состояния (REST). Эти запросы публикация отправку и получение личные веб-канала для текущего пользователя. В таблице 1 приведены ссылки на статьи, в которых описываются общие понятия, которые необходимо знать перед началом работы.</span><span class="sxs-lookup"><span data-stu-id="2199e-p102">The SharePoint-hosted app that you create in this article uses JavaScript to build and send HTTP requests to Representational State Transfer (REST) endpoints. These requests publish a post and get the personal feed for the current user. Table 1 contains links to articles that describe general concepts you should understand before you get started.</span></span>
  
    
    

<span data-ttu-id="2199e-119">**В таблице 1. Основные понятия по работе с социальными веб-каналами SharePoint**</span><span class="sxs-lookup"><span data-stu-id="2199e-119">**Table 1. Core concepts for working with SharePoint social feeds**</span></span>


|<span data-ttu-id="2199e-120">**Название статьи**</span><span class="sxs-lookup"><span data-stu-id="2199e-120">**Article title**</span></span>|<span data-ttu-id="2199e-121">**Описание**</span><span class="sxs-lookup"><span data-stu-id="2199e-121">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="2199e-122">Надстройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="2199e-122">SharePoint Add-ins</span></span>](http://msdn.microsoft.com/library/cd1eda9e-8e54-4223-93a9-a6ea0d18df70%28Office.15%29.aspx) <br/> |<span data-ttu-id="2199e-123">Сведения о Надстройки SharePoint и принципы их создания.</span><span class="sxs-lookup"><span data-stu-id="2199e-123">Learn about SharePoint Add-ins and fundamental concepts for building them.</span></span>  <br/> |
| [<span data-ttu-id="2199e-124">Начало разработки с использованием социальных функций в SharePoint</span><span class="sxs-lookup"><span data-stu-id="2199e-124">Get started developing with social features in SharePoint</span></span>](get-started-developing-with-social-features-in-sharepoint.md) <br/> |<span data-ttu-id="2199e-125">Узнайте, как начать программирование с социальными веб-каналов и микроблога публикации, следуя людей и содержимое (документы, сайты и tags.md) и работа с профилями пользователей.</span><span class="sxs-lookup"><span data-stu-id="2199e-125">Find out how to start programming with social feeds and microblog posts, following people and content (documents, sites, and tags.md), and working with user profiles.</span></span>  <br/> |
| [<span data-ttu-id="2199e-126">Работа с социальными веб-каналами в SharePoint</span><span class="sxs-lookup"><span data-stu-id="2199e-126">Work with social feeds in SharePoint</span></span>](work-with-social-feeds-in-sharepoint.md) <br/> |<span data-ttu-id="2199e-127">Сведения о распространенных задач программирования по работе с социальными веб-каналов и API, которое используется для выполнения задачи.</span><span class="sxs-lookup"><span data-stu-id="2199e-127">Learn about common programming tasks for working with social feeds and the API that you use to perform the tasks.</span></span>  <br/> |
   

## <a name="create-the-sharepoint-add-in-project"></a><span data-ttu-id="2199e-128">Создайте проект надстройки для SharePoint.</span><span class="sxs-lookup"><span data-stu-id="2199e-128">Create the SharePoint Add-in project</span></span>
<span data-ttu-id="2199e-129"><a name="bkmk_CreateApp"> </a></span><span class="sxs-lookup"><span data-stu-id="2199e-129"><a name="bkmk_CreateApp"> </a></span></span>


1. <span data-ttu-id="2199e-130">На сайте разработчика откройте Napa и выберите **Добавить новый проект**.</span><span class="sxs-lookup"><span data-stu-id="2199e-130">On your Developer Site, open Napa, and then choose **Add New Project**.</span></span>
    
  
2. <span data-ttu-id="2199e-131">Выберите шаблон **приложение для SharePoint**, назовите проект SocialFeedRESTи затем нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="2199e-131">Choose the **App for SharePoint** template, name the projectSocialFeedREST, and then choose the **Create** button.</span></span>
    
  
3. <span data-ttu-id="2199e-132">Укажите разрешения, которые ваше приложение должно:</span><span class="sxs-lookup"><span data-stu-id="2199e-132">Specify the permissions that your app needs:</span></span>
    
  <span data-ttu-id="2199e-133">А.</span><span class="sxs-lookup"><span data-stu-id="2199e-133">a.</span></span> <span data-ttu-id="2199e-134">В нижней части страницы нажмите кнопку **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="2199e-134">Choose the **Properties** button at the bottom of the page.</span></span>
     
  <span data-ttu-id="2199e-135">Б.</span><span class="sxs-lookup"><span data-stu-id="2199e-135">b.</span></span> <span data-ttu-id="2199e-136">В окне **Свойства** выберите **разрешения**.</span><span class="sxs-lookup"><span data-stu-id="2199e-136">In the **Properties** window, choose **Permissions**.</span></span>
    
  <span data-ttu-id="2199e-137">В.</span><span class="sxs-lookup"><span data-stu-id="2199e-137">c.</span></span> <span data-ttu-id="2199e-138">В разделе категория **контента** задайте разрешения **Write** для области **клиента**.</span><span class="sxs-lookup"><span data-stu-id="2199e-138">In the **Content** category, set **Write** permissions for the **Tenant** scope.</span></span>
    
  <span data-ttu-id="2199e-139">Г.</span><span class="sxs-lookup"><span data-stu-id="2199e-139">d.</span></span> <span data-ttu-id="2199e-140">В разделе категория **социальных** задайте разрешения **Read** для области **Профили пользователей**.</span><span class="sxs-lookup"><span data-stu-id="2199e-140">In the **Social** category, set **Read** permissions for the **User Profiles** scope.</span></span>
    
  <span data-ttu-id="2199e-141">Д.</span><span class="sxs-lookup"><span data-stu-id="2199e-141">e.</span></span> <span data-ttu-id="2199e-142">Закройте окно **свойств**.</span><span class="sxs-lookup"><span data-stu-id="2199e-142">Close the **Properties** window.</span></span>
    
4. <span data-ttu-id="2199e-143">Разверните узел **скриптов**, выберите файл App.js и удалите содержимое файла.</span><span class="sxs-lookup"><span data-stu-id="2199e-143">Expand the **Scripts** node, choose the App.js file, and delete the contents of the file.</span></span>
    
  

## <a name="post-to-the-social-feed-by-using-the-sharepoint-rest-service"></a><span data-ttu-id="2199e-144">Публикация для социальных веб-канал с помощью службы SharePoint REST</span><span class="sxs-lookup"><span data-stu-id="2199e-144">Post to the social feed by using the SharePoint REST service</span></span>
<span data-ttu-id="2199e-145"><a name="bkmk_PubPost"> </a></span><span class="sxs-lookup"><span data-stu-id="2199e-145"></span></span>


1. <span data-ttu-id="2199e-146">В файле App.js объявите глобальную переменную для URL-адреса конечной точки **SocialFeedManager**.</span><span class="sxs-lookup"><span data-stu-id="2199e-146">In the App.js file, declare a global variable for the URL of the **SocialFeedManager** endpoint.</span></span>
    
```
var feedManagerEndpoint;
```

2. <span data-ttu-id="2199e-147">Добавьте следующий код, который получает параметр **SPAppWebUrl** из строки запроса, который используется для создания конечной точки **SocialFeedManager**.</span><span class="sxs-lookup"><span data-stu-id="2199e-147">Add the following code, which gets the **SPAppWebUrl** parameter from the query string and uses it to build the **SocialFeedManager** endpoint.</span></span>
    
```
  $(document).ready(function () {
    var appweburl;
    var params = document.URL.split("?")[1].split("&amp;");
    for (var i = 0; i < params.length; i = i + 1) {
        var param = params[i].split("=");
        if (param[0] === "SPAppWebUrl") appweburl = param[1];
    }
    feedManagerEndpoint = decodeURIComponent(appweburl) + "/_api/social.feed";
    postToMyFeed();
});
```

3. <span data-ttu-id="2199e-148">Добавьте следующий код, который создает **POST** в HTTP-запрос для конечной точки `/my/Feed/Post` , определяет post создания данных, а также публикует post.</span><span class="sxs-lookup"><span data-stu-id="2199e-148">Add the following code, which builds the HTTP **POST** request for the `/my/Feed/Post` endpoint, defines the post's creation data, and publishes the post.</span></span>
    
    <span data-ttu-id="2199e-p108">Ресурс **SocialRestPostCreationData** отправляет запрос в тексте запроса. **SocialRestPostCreationData** содержит в целевом объекте post (в данном случае `null` , чтобы указать корневой записью для текущего пользователя) и **SocialPostCreationData** сложный тип, который определяет свойства post.</span><span class="sxs-lookup"><span data-stu-id="2199e-p108">The request sends a **SocialRestPostCreationData** resource in the request body. **SocialRestPostCreationData** contains the target for the post (in this case, `null` to specify a root post for the current user) and a **SocialPostCreationData** complex type that defines the post's properties.</span></span>
    


```
  
function postToMyFeed() {
    $.ajax( {
        url: feedManagerEndpoint + "/my/Feed/Post",
        type: "POST",
        data: JSON.stringify( { 
            'restCreationData':{
                '__metadata':{ 
                    'type':'SP.Social.SocialRestPostCreationData'
                },
                'ID':null, 
                'creationData':{ 
                    '__metadata':{ 
                        'type':'SP.Social.SocialPostCreationData'
                    },
                'ContentText':'This post was published using REST.',
                'UpdateStatusText':false
                } 
            } 
        }),
        headers: { 
            "accept": "application/json;odata=verbose",
            "content-type":"application/json;odata=verbose",
            "X-RequestDigest": $("#__REQUESTDIGEST").val()
        },
        success: getMyFeed,
        error: function (xhr, ajaxOptions, thrownError) { 
            alert("POST error:\\n" + xhr.status + "\\n" + thrownError);
        }
    });
}

```


## <a name="retrieve-the-social-feed-for-the-current-user-by-using-the-sharepoint-rest-service"></a><span data-ttu-id="2199e-151">Извлечение социальных веб-канал для текущего пользователя с помощью службы SharePoint REST</span><span class="sxs-lookup"><span data-stu-id="2199e-151">Retrieve the social feed for the current user by using the SharePoint REST service</span></span>
<span data-ttu-id="2199e-152"><a name="bkmk_GetFeed"> </a></span><span class="sxs-lookup"><span data-stu-id="2199e-152"></span></span>

<span data-ttu-id="2199e-p109">Добавьте следующий код, который получает **Personal** канал типа для текущего пользователя с помощью конечной точки `/my/Feed` . Заголовок **accept** запросов, что сервер вернуть представление Нотация объектов JavaScript (JSON) веб-канала в свой ответ.</span><span class="sxs-lookup"><span data-stu-id="2199e-p109">Add the following code, which gets the **Personal** feed type for the current user by using the `/my/Feed` endpoint. The **accept** header requests that the server return a JavaScript Object Notation (JSON) representation of the feed in its response.</span></span>
  
    
    

```

function getMyFeed() {
    $.ajax( {
        url: feedManagerEndpoint + "/my/Feed",
        headers: { 
            "accept": "application/json;odata=verbose"
        },
        success: feedRetrieved,
        error: function (xhr, ajaxOptions, thrownError) { 
            alert("GET error:\\n" + xhr.status + "\\n" + thrownError);
        }
    });    
}

```


## <a name="iterate-through-the-social-feed-and-read-from-it-by-using-the-sharepoint-rest-service"></a><span data-ttu-id="2199e-155">Выполните итерацию по социальных сетей веб-канала и чтение из нее с помощью службы SharePoint REST</span><span class="sxs-lookup"><span data-stu-id="2199e-155">Iterate through the social feed and read from it by using the SharePoint REST service</span></span>
<span data-ttu-id="2199e-156"><a name="bkmk_ReadFeed"> </a></span><span class="sxs-lookup"><span data-stu-id="2199e-156"></span></span>

<span data-ttu-id="2199e-157">Добавьте следующий код, который готовит возвращаемые данные с помощью функции **JSON.stringify** и **JSON.parse** и выполняется итерация по веб-канал и получает владельца потока и текста post корневой.</span><span class="sxs-lookup"><span data-stu-id="2199e-157">Add the following code, which prepares the returned data by using the **JSON.stringify** function and the **JSON.parse** function, and then iterates through the feed and gets the thread's owner and the root post's text.</span></span>
  
    
    

```

function feedRetrieved(data) {
    var stringData = JSON.stringify(data);
    var jsonObject = JSON.parse(stringData); 
 
    var feed = jsonObject.d.SocialFeed.Threads; 
    var threads = feed.results;
    var feedContent = "";
    for (var i = 0; i < threads.length; i++) {
        var thread = threads[i];
        var participants = thread.Actors;
        var owner = participants.results[thread.OwnerIndex].Name;
        feedContent += '<p>' + owner + 
            ' said "' + thread.RootPost.Text + '"</p>';
    }  
    $("#message").html(feedContent); 
}
```


## <a name="run-the-app-for-sharepoint-on-the-developer-site"></a><span data-ttu-id="2199e-158">Запуск приложения для SharePoint на сайте разработчика</span><span class="sxs-lookup"><span data-stu-id="2199e-158">Run the app for SharePoint on the Developer Site</span></span>
<span data-ttu-id="2199e-159"><a name="bkmk_ReadFeed"> </a></span><span class="sxs-lookup"><span data-stu-id="2199e-159"></span></span>


1. <span data-ttu-id="2199e-160">Чтобы запустить приложение, нажмите кнопку **Запустить проект** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="2199e-160">To run the app, choose the **Run Project** button at the bottom of the page.</span></span>
    
  
2. <span data-ttu-id="2199e-p110">В **вы доверяете** открывшейся странице нажмите кнопку **Доверять его**. Страница приложения открывает и отображает имя владельца и текст каждого post корневого веб-канала.</span><span class="sxs-lookup"><span data-stu-id="2199e-p110">In the **Do you trust** page that opens, choose the **Trust It** button. The app page opens and displays the owner's name and the text of each root post in the feed.</span></span>
    
  

  
    
    

## <a name="code-example-publish-a-post-and-get-the-feed-for-the-current-user-by-using-the-sharepoint-rest-service"></a><span data-ttu-id="2199e-163">Пример кода: публикация отправку и получение веб-канал для текущего пользователя с помощью службы SharePoint REST</span><span class="sxs-lookup"><span data-stu-id="2199e-163">Code example: Publish a post and get the feed for the current user by using the SharePoint REST service</span></span>
<span data-ttu-id="2199e-164"><a name="bkmk_PubPosts1"> </a></span><span class="sxs-lookup"><span data-stu-id="2199e-164"></span></span>

<span data-ttu-id="2199e-p111">Ниже приведен полный пример кода для файла App.js. Публикует сообщение, а также получает личные веб-канала для текущего пользователя, который возвращается как объект JSON. Затем выполняется итерация веб-канал.</span><span class="sxs-lookup"><span data-stu-id="2199e-p111">The following is the complete code example for the App.js file. It publishes a post and gets the personal feed for the current user, which is returned as a JSON object. Then it iterates through the feed.</span></span>
  
    
    

```

var feedManagerEndpoint;

// Get the SPAppWebUrl parameter from the query string and build
// the feed manager endpoint.
$(document).ready(function () {
    var appweburl;
    var params = document.URL.split("?")[1].split("&amp;");
    for (var i = 0; i < params.length; i = i + 1) {
        var param = params[i].split("=");
        if (param[0] === "SPAppWebUrl") appweburl = param[1];
    }
    feedManagerEndpoint = decodeURIComponent(appweburl)+ "/_api/social.feed";
    postToMyFeed();
});

// Publish a post to the current user's feed by using the 
// "<app web URL>/_api/social.feed/my/Feed/Post" endpoint.
function postToMyFeed() {
    $.ajax( {
        url: feedManagerEndpoint + "/my/Feed/Post",
        type: "POST",
        data: JSON.stringify( { 
            'restCreationData':{
                '__metadata':{ 
                    'type':'SP.Social.SocialRestPostCreationData'
                },
                'ID':null, 
                'creationData':{ 
                    '__metadata':{ 
                        'type':'SP.Social.SocialPostCreationData'
                    },
                'ContentText':'This post was published using REST.',
                'UpdateStatusText':false
                } 
            } 
        }),
        headers: { 
            "accept": "application/json;odata=verbose",
            "content-type":"application/json;odata=verbose",
            "X-RequestDigest": $("#__REQUESTDIGEST").val()
        },
        success: getMyFeed,
        error: function (xhr, ajaxOptions, thrownError) { 
            alert("POST error:\\n" + xhr.status + "\\n" + thrownError);
        }
    });
}

// Get the current user's feed by using the 
// "<app web URL>/_api/social.feed/my/Feed" endpoint.
function getMyFeed() {
    $.ajax( {
        url: feedManagerEndpoint + "/my/Feed",
        headers: { 
            "accept": "application/json;odata=verbose"
        },
        success: feedRetrieved,
        error: function (xhr, ajaxOptions, thrownError) { 
            alert("GET error:\\n" + xhr.status + "\\n" + thrownError);
        }
    });    
}

// Parse the JSON data and iterate through the feed.
function feedRetrieved(data) {
    var stringData = JSON.stringify(data);
    var jsonObject = JSON.parse(stringData); 
 
    var feed = jsonObject.d.SocialFeed.Threads; 
    var threads = feed.results;
    var feedContent = "";
    for (var i = 0; i < threads.length; i++) {
        var thread = threads[i];
        var participants = thread.Actors;
        var owner = participants.results[thread.OwnerIndex].Name;
        feedContent += '<p>' + owner + 
            ' said "' + thread.RootPost.Text + '"</p>';
    }  
    $("#message").html(feedContent); 
}
```


## <a name="next-steps"></a><span data-ttu-id="2199e-168">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2199e-168">Next steps</span></span>
<span data-ttu-id="2199e-169"><a name="bkmk_PubPosts1"> </a></span><span class="sxs-lookup"><span data-stu-id="2199e-169"></span></span>

<span data-ttu-id="2199e-170">Другие конечные точки REST, которые можно использовать для доступа к социальных функций в разделе [социальных веб-канала активности Справочник по интерфейсу API службы REST для SharePoint](social-feed-rest-api-reference-for-sharepoint.md) , используя [следующую людей и контент Справочник по интерфейсу API службы REST для SharePoint](following-people-and-content-rest-api-reference-for-sharepoint.md) .</span><span class="sxs-lookup"><span data-stu-id="2199e-170">See  [Social feed REST API reference for SharePoint](social-feed-rest-api-reference-for-sharepoint.md) and [Following people and content REST API reference for SharePoint](following-people-and-content-rest-api-reference-for-sharepoint.md) for other REST endpoints that you can use to access social features.</span></span>
  
    
    

## <a name="additional-resources"></a><span data-ttu-id="2199e-171">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="2199e-171">Additional resources</span></span>
<span data-ttu-id="2199e-172"><a name="bk_addResources"> </a></span><span class="sxs-lookup"><span data-stu-id="2199e-172"></span></span>


-  [<span data-ttu-id="2199e-173">Social feed REST API reference for SharePoint</span><span class="sxs-lookup"><span data-stu-id="2199e-173">Social feed REST API reference for SharePoint</span></span>](social-feed-rest-api-reference-for-sharepoint.md)
    
  
-  [<span data-ttu-id="2199e-174">Начало разработки с использованием социальных функций в SharePoint</span><span class="sxs-lookup"><span data-stu-id="2199e-174">Get started developing with social features in SharePoint</span></span>](get-started-developing-with-social-features-in-sharepoint.md)
    
  
-  [<span data-ttu-id="2199e-175">Работа с социальными веб-каналами в SharePoint</span><span class="sxs-lookup"><span data-stu-id="2199e-175">Work with social feeds in SharePoint</span></span>](work-with-social-feeds-in-sharepoint.md)
    
  

