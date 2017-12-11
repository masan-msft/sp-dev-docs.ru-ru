---
title: "Чтение и запись на социальные веб-канал с помощью службы REST в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 1da8d484-3666-42c3-8a8f-8b3ef93e96e9
ms.openlocfilehash: 51db8b71573045c030ce7b941344c1203fed2b27
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="read-and-write-to-the-social-feed-by-using-the-rest-service-in-sharepoint"></a>Чтение и запись на социальные веб-канал с помощью службы REST в SharePoint

Создайте приложение, размещенное в SharePoint, которое использует службу REST для публикации записи блога и получения личного веб-канала для текущего пользователя.

## <a name="prerequisites-for-creating-a-sharepoint-hosted-sharepoint-add-in-that-publishes-a-post-and-gets-the-social-feed-by-using-the-sharepoint-rest-service"></a>Необходимые условия для создания SharePoint хостингом SharePoint надстройки, которая публикует сообщение и получает социальные веб-канал с помощью службы SharePoint REST
<a name="bkmk_Prereqs"> </a>

В этой статье предполагается, что вы создаете надстройку для SharePoint с помощью Napa на сайте разработчика Office 365. Если вы используете эту среду разработки, то необходимые условия выполняются.
  
> [!NOTE]
> [!Примечание] В статье  [Настройка среды для разработки надстроек SharePoint в Office 365](http://msdn.microsoft.com/library/b22ce52a-ae9e-4831-9b68-c9210af6dc54%28Office.15%29.aspx) можно найти сведения о том, как зарегистрироваться на сайте разработчика и начать использовать Napa.
  
    
    

Если вы не используете Napa на сайте разработчика, то необходимо следующее:
  
    
    

- SharePoint с личного сайта настроены и на личный сайт, созданный для текущего пользователя
    
  
- Visual Studio 2012 и Инструменты разработчика Office для Visual Studio 2013
    
  
- **Полный** доступ к приложению-службе профилей пользователей для пользователя, вошедшего в систему
    
> [!NOTE]
> [!Примечание] Руководство по настройке среды разработки, соответствующей вашим потребностям, см. в статье  [Начало создания приложений для Office и SharePoint](http://msdn.microsoft.com/library/187f8c8c-1b15-471c-80b5-69a40e67deea.aspx). 
  
    
    


## <a name="core-concepts-to-know-about-working-with-sharepoint-social-feeds"></a>Основные сведения о работе с социальными веб-каналами SharePoint
<a name="bkmk_CoreConcepts"> </a>

Размещение в SharePoint приложение, создайте в этой статье использует JavaScript для создания и отправки HTTP-запросов к конечным точкам представлений состояния (REST). Эти запросы публикация отправку и получение личные веб-канала для текущего пользователя. В таблице 1 приведены ссылки на статьи, в которых описываются общие понятия, которые необходимо знать перед началом работы.
  
    
    

**В таблице 1. Основные понятия по работе с социальными веб-каналами SharePoint**


|**Название статьи**|**Описание**|
|:-----|:-----|
| [Надстройки SharePoint](http://msdn.microsoft.com/library/cd1eda9e-8e54-4223-93a9-a6ea0d18df70%28Office.15%29.aspx) <br/> |Сведения о Надстройки SharePoint и принципы их создания.  <br/> |
| [Начало разработки с использованием социальных функций в SharePoint](get-started-developing-with-social-features-in-sharepoint.md) <br/> |Узнайте, как начать программирование с социальными веб-каналов и микроблога публикации, следуя людей и содержимое (документы, сайты и tags.md) и работа с профилями пользователей.  <br/> |
| [Работа с социальными веб-каналами в SharePoint](work-with-social-feeds-in-sharepoint.md) <br/> |Сведения о распространенных задач программирования по работе с социальными веб-каналов и API, которое используется для выполнения задачи.  <br/> |
   

## <a name="create-the-sharepoint-add-in-project"></a>Создайте проект надстройки для SharePoint.
<a name="bkmk_CreateApp"> </a>


1. На сайте разработчика откройте Napa и выберите **Добавить новый проект**.
    
  
2. Выберите шаблон **приложение для SharePoint**, назовите проект SocialFeedRESTи затем нажмите кнопку **Создать**.
    
  
3. Укажите разрешения, которые ваше приложение должно:
    
  А. В нижней части страницы нажмите кнопку **Свойства**.
     
  Б. В окне **Свойства** выберите **разрешения**.
    
  В. В разделе категория **контента** задайте разрешения **Write** для области **клиента**.
    
  Г. В разделе категория **социальных** задайте разрешения **Read** для области **Профили пользователей**.
    
  Д. Закройте окно **свойств**.
    
4. Разверните узел **скриптов**, выберите файл App.js и удалите содержимое файла.
    
  

## <a name="post-to-the-social-feed-by-using-the-sharepoint-rest-service"></a>Публикация для социальных веб-канал с помощью службы SharePoint REST
<a name="bkmk_PubPost"> </a>


1. В файле App.js объявите глобальную переменную для URL-адреса конечной точки **SocialFeedManager**.
    
```
var feedManagerEndpoint;
```

2. Добавьте следующий код, который получает параметр **SPAppWebUrl** из строки запроса, который используется для создания конечной точки **SocialFeedManager**.
    
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

3. Добавьте следующий код, который создает **POST** в HTTP-запрос для конечной точки `/my/Feed/Post` , определяет post создания данных, а также публикует post.
    
    Ресурс **SocialRestPostCreationData** отправляет запрос в тексте запроса. **SocialRestPostCreationData** содержит в целевом объекте post (в данном случае `null` , чтобы указать корневой записью для текущего пользователя) и **SocialPostCreationData** сложный тип, который определяет свойства post.
    


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


## <a name="retrieve-the-social-feed-for-the-current-user-by-using-the-sharepoint-rest-service"></a>Извлечение социальных веб-канал для текущего пользователя с помощью службы SharePoint REST
<a name="bkmk_GetFeed"> </a>

Добавьте следующий код, который получает **Personal** канал типа для текущего пользователя с помощью конечной точки `/my/Feed` . Заголовок **accept** запросов, что сервер вернуть представление Нотация объектов JavaScript (JSON) веб-канала в свой ответ.
  
    
    

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


## <a name="iterate-through-the-social-feed-and-read-from-it-by-using-the-sharepoint-rest-service"></a>Выполните итерацию по социальных сетей веб-канала и чтение из нее с помощью службы SharePoint REST
<a name="bkmk_ReadFeed"> </a>

Добавьте следующий код, который готовит возвращаемые данные с помощью функции **JSON.stringify** и **JSON.parse** и выполняется итерация по веб-канал и получает владельца потока и текста post корневой.
  
    
    

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


## <a name="run-the-app-for-sharepoint-on-the-developer-site"></a>Запуск приложения для SharePoint на сайте разработчика
<a name="bkmk_ReadFeed"> </a>


1. Чтобы запустить приложение, нажмите кнопку **Запустить проект** в нижней части страницы.
    
  
2. В **вы доверяете** открывшейся странице нажмите кнопку **Доверять его**. Страница приложения открывает и отображает имя владельца и текст каждого post корневого веб-канала.
    
  

  
    
    

## <a name="code-example-publish-a-post-and-get-the-feed-for-the-current-user-by-using-the-sharepoint-rest-service"></a>Пример кода: публикация отправку и получение веб-канал для текущего пользователя с помощью службы SharePoint REST
<a name="bkmk_PubPosts1"> </a>

Ниже приведен полный пример кода для файла App.js. Публикует сообщение, а также получает личные веб-канала для текущего пользователя, который возвращается как объект JSON. Затем выполняется итерация веб-канал.
  
    
    

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


## <a name="next-steps"></a>Дальнейшие действия
<a name="bkmk_PubPosts1"> </a>

Другие конечные точки REST, которые можно использовать для доступа к социальных функций в разделе [социальных веб-канала активности Справочник по интерфейсу API службы REST для SharePoint](social-feed-rest-api-reference-for-sharepoint.md) , используя [следующую людей и контент Справочник по интерфейсу API службы REST для SharePoint](following-people-and-content-rest-api-reference-for-sharepoint.md) .
  
    
    

## <a name="see-also"></a>См. также
<a name="bk_addResources"> </a>


-  [Social feed REST API reference for SharePoint](social-feed-rest-api-reference-for-sharepoint.md)
    
  
-  [Начало разработки с использованием социальных функций в SharePoint](get-started-developing-with-social-features-in-sharepoint.md)
    
  
-  [Работа с социальными веб-каналами в SharePoint](work-with-social-feeds-in-sharepoint.md)
    
  

