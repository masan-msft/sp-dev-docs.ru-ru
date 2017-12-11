---
title: "Выполните указанные документы, сайты и теги с помощью службы REST в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 989a5873-49f9-49e4-8d0f-439dde891cc2
ms.openlocfilehash: 1c27c11c49be77941fd7c7b2e4876f43938dea66
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="follow-documents-sites-and-tags-by-using-the-rest-service-in-sharepoint"></a>Выполните указанные документы, сайты и теги с помощью службы REST в SharePoint

Создание размещенных в SharePoint приложений, подписка на контент (документы, сайты и теги) с помощью службы REST и для получения отслеживаемого содержимого.

## <a name="how-do-i-use-the-sharepoint-rest-service-to-follow-content"></a>Как использовать службы SharePoint REST для подписка на контент?
<a name="bk_intro"> </a>

Пользователи SharePoint можно следовать документы, сайты и теги для получения обновлений об элементах в свои каналы новостей и быстро открыть число документов и сайтов. API-Интерфейс REST SharePoint можно использовать в вашем приложении или решение, которое требуется запустить следующие материалы, остановите следующие материалы и получить отслеживаемого содержимого от имени текущего пользователя.
  
    
    
Доступны следующие ресурсы REST, основного API для контента следующие задачи:
  
    
    

- **SocialRestFollowingManager** предоставляет методы для управления пользовательского списка число субъектов.
    
  
- **SocialActor** представляет документ, сайта или тег, сервер возвращает в ответ на запрос на стороне клиента.
    
  
- **SocialActorInfo** указывает документ, сайта или тега в запросах со стороны клиента к серверу.
    
  
- **SocialActorType** и **SocialActorTypes** укажите типы контента в запросах со стороны клиента к серверу.
    
  
Для выполнения следующих контента задач с помощью интерфейса API REST, службы REST отправки HTTP **GET** и **POST** HTTP-запросов. URI конечных точек REST для следующих контента задач начинаются с **SocialRestFollowingManager** ресурсов ( `<siteUri>/_api/social.following`) и заканчиваются ознакомьтесь со следующими ресурсами:
  
    
    

- **follow** запуск отслеживание документа, сайта или тега
    
  
- **stopfollowing**, чтобы отменить подписку на документ, сайта или тега
    
  
- **isfollowed**, чтобы узнать, совместимо ли после пользователя конкретного документа, сайта или тега
    
  
- **my/followed**, чтобы получить число документов, сайтов и тегов
    
  
- **my/followedcount** для подсчета число документов, сайтов и тегов
    
> [!NOTE]
> Для следующих пользователей задачи, но **последователи** и **предложений** ресурсы, доступные из поддерживают только **SocialRestFollowingManager** , отслеживаемые пользователи не контента также использовать эти конечные точки. Дополнительные сведения об использовании **SocialRestFollowingManager**можно [Подписка на контент в SharePoint](follow-content-in-sharepoint.md) и [Подписка на людей в SharePoint](follow-people-in-sharepoint.md). 
  
    
    


## <a name="prerequisites-for-creating-a-sharepoint-hosted-app-that-manages-followed-content-by-using-the-sharepoint-rest-service"></a>Необходимые условия для создания приложения с размещением в SharePoint, который управляет отслеживаемого содержимого с помощью службы SharePoint REST
<a name="bkmk_Prereqs"> </a>

В этой статье предполагается, что вы создаете надстройку для SharePoint с помощью Napa на сайте разработчика Office 365. Если вы используете эту среду разработки, то необходимые условия выполняются.
  
> [!NOTE]
> [!Примечание] Перейдите к  [Настройка среды для разработки надстроек SharePoint в Office 365](http://msdn.microsoft.com/library/b22ce52a-ae9e-4831-9b68-c9210af6dc54%28Office.15%29.aspx) Зарегистрируйтесь на сайте разработчика и начать использовать Napa.
  
    
    

Если вы не используете Napa на Office 365 сайт разработчика, необходимо перед развертыванием Надстройка SharePoint выполняются следующие требования:
  
    
    

- Среда разработки SharePoint, которые настроены для изоляции приложений. При разработке удаленно, сервер должен поддерживать sideloading приложения или приложения необходимо установить на сайте разработчика.
    
  
- Узел Личный сайт, настроены на личный сайт, созданный для текущего пользователя.
    
  
- Visual Studio 2012 или Visual Studio 2013 с Инструменты разработчика Office для Visual Studio 2013.
    
  
- Достаточные разрешения для пользователя, вошедшего в систему:
    
  - Разрешения локального администратора на компьютере разработчика.
    
  
  - Управление разрешениями пользователей веб-сайта и создание дочерних сайтов на сайте SharePoint, на котором устанавливается приложение. По умолчанию эти разрешения доступны только для пользователей, имеющий уровень разрешений полного доступа или пользователей, которые входят в группу владельцев сайта.
    
  
  - Необходимо войти в систему как кто-то отличную от учетной записи системы. Системная учетная запись не имеет разрешения, чтобы установить приложение.
    
> [!NOTE]
> [!Примечание] В разделе  [Настройка локальной среды разработки надстроек SharePoint](http://msdn.microsoft.com/library/b0878c12-27c9-4eea-ae3b-7e79e5a8838d%28Office.15%29.aspx) руководство по локальной установки (включая отключение проверки замыкания на себя при необходимости).
  
    
    


  
    
    

## <a name="create-the-sharepoint-add-in-project"></a>Создайте проект надстройки для SharePoint.
<a name="bkmk_CreateApp"> </a>


1. На сайте разработчика откройте Napa и выберите **Добавить новый проект**.
    
  
2. Выберите шаблон **приложение для SharePoint**, назовите проект и затем нажмите кнопку **Создать**.
    
  
3. Установка разрешений для вашего приложения:
    
   1. В нижней части страницы нажмите кнопку **Свойства**.
    
  
   2. В окне **Свойства** выберите **разрешения**.
    
  
   3. В разделе категория **контента** задайте разрешения **Write** для области **клиента**.
    
  
   4. В разделе категория **социальных** задайте разрешения **Read** для области **Профили пользователей**.
    
  
   5. Закройте окно **свойств**.
    
  
4. Разверните узел **скриптов**, откройте файл App.js и замените его содержимое на код из одного из следующих сценариев:
    
   -  [Запустите следующие и остановите следующие документа](how-to-follow-documents-sites-and-tags-by-using-the-rest-service-in-sharepoint-2.md#bkmk_FollowDocs)
   -  [Запустите следующие и отменить подписку на сайт](how-to-follow-documents-sites-and-tags-by-using-the-rest-service-in-sharepoint-2.md#bkmk_FollowSites)
   -  [Запустите следующие и остановить отслеживание тега](how-to-follow-documents-sites-and-tags-by-using-the-rest-service-in-sharepoint-2.md#bkmk_FollowTags)
   -  [Получение следования за контентом](how-to-follow-documents-sites-and-tags-by-using-the-rest-service-in-sharepoint-2.md#bkmk_GetFollowed)
  
5. Чтобы запустить приложение, нажмите кнопку **Запустить проект** в нижней части страницы.
    
  
6. В **вы доверяете** открывшейся странице нажмите кнопку **Доверять его**. Страница приложения открывает и выполняет код. Чтобы выполнить отладку страницы, нажмите клавишу **F12** и выберите App.js на вкладке **скрипта**.
    
  

## <a name="code-example-start-following-and-stop-following-a-document-by-using-the-sharepoint-rest-service"></a>Пример кода: запустите следующие и остановите следующие документа с помощью службы SharePoint REST
<a name="bkmk_FollowDocs"> </a>

В следующем примере кода представляет содержимое файла App.js и показано, как:
  
    
    

- Получение URI сайта приложения из строки запроса и создать URI конечной точки  `<siteUri>/_api/social.following` .
    
  
- Создание и отправка запроса **POST** к конечной точке `isfollowed` , чтобы узнать, совместимо ли текущий пользователь уже после указанного документа.
    
  
- Создание и отправка запроса **POST** к конечной точке `follow` запуск после документа.
    
  
- Создание и отправка запроса **POST** к конечной точке `stopfollowing` , чтобы отменить подписку на документ.
    
  
- Ознакомьтесь с JSON ответ, возвращенный запрос  `isfollowed` и `follow` запроса. (Запрос `stopfollowing` не возвращает все действия в ответе.) В разделе [ответы пример JSON](how-to-follow-documents-sites-and-tags-by-using-the-rest-service-in-sharepoint-2.md#bk_exampleResponses).
    
  
Прежде чем запустить код необходимо отправить документ и измените значение заполнитель для переменной **documentUrl** URL-адрес документа.
  
    
    



```

// Replace the documentUrl placeholder value before you run the code.
var documentUrl = "https://domain.sharepoint.com/Shared%20Documents/fileName.docx";
var followingManagerEndpoint;

// Get the SPAppWebUrl parameter from the query string and build
// the Following manager endpoint.
$(document).ready(function () {
    var appweburl;
    var params = document.URL.split("?")[1].split("&amp;");
    for (var i = 0; i < params.length; i = i + 1) {
        var param = params[i].split("=");
        if (param[0] === "SPAppWebUrl") appweburl = param[1];
    }
    followingManagerEndpoint = decodeURIComponent(appweburl) + "/_api/social.following";
    isFollowed();
});

// Check whether the current user is already following the document.
// The request body includes a SocialActorInfo object that represents
// the specified item. 
// The success function reads the response from the REST service and then
// toggles the user's following status by calling the appropriate method.
function isFollowed() {
    $.ajax( {
        url: followingManagerEndpoint + "/isfollowed",
        type: "POST",
        data: JSON.stringify( { 
            "actor": {
                "__metadata": {
                    "type":"SP.Social.SocialActorInfo"
                },
                "ActorType":1,
                "ContentUri":documentUrl,
                "Id":null
            } 
        }),
        headers: { 
            "accept":"application/json;odata=verbose",
            "content-type":"application/json;odata=verbose",
            "X-RequestDigest":$("#__REQUESTDIGEST").val()
        },
        success: function (responseData) { 
            stringData = JSON.stringify(responseData);
            jsonObject = JSON.parse(stringData);
            if (jsonObject.d.IsFollowed === true ) {
                alert('The user is currently following the document.');
                stopFollowDocument();
            }
            else {
                alert('The user is currently NOT following the document.');
                followDocument();
            }
        },
        error: requestFailed
    });
}

// Make the current user start following a document.
// The request body includes a SocialActorInfo object that represents
// the document to follow.
// The success function reads the response from the REST service.
function followDocument() {
    $.ajax( {
        url: followingManagerEndpoint + "/follow",
        type: "POST",
        data: JSON.stringify( { 
            "actor": {
                "__metadata": {
                    "type":"SP.Social.SocialActorInfo"
                },
                "ActorType":1,
                "ContentUri":documentUrl,
                "Id":null
            } 
        } ),
        headers: { 
            "accept":"application/json;odata=verbose",
            "content-type":"application/json;odata=verbose",
            "X-RequestDigest":$("#__REQUESTDIGEST").val()
        },
        success: function (responseData) { 
            stringData = JSON.stringify(responseData);
            jsonObject = JSON.parse(stringData);
            var statusMessage = {
                0 : 'The user has started following the document. ',
                1 : 'The user is already following the document. ',
                2 : 'An internal limit was reached. ',
                3 : 'An internal error occurred. '
            }
            alert(statusMessage[jsonObject.d.Follow] + 'Status code = ' + jsonObject.d.Follow);
        },
        error: requestFailed
    } );
}

// Make the current user stop following a document.
// The request body includes a SocialActorInfo object that represents
// the document to stop following.
function stopFollowDocument() {
    $.ajax( {
        url: followingManagerEndpoint + "/stopfollowing",
        type: "POST",
        data: JSON.stringify( { 
            "actor": {
                "__metadata": {
                    "type":"SP.Social.SocialActorInfo"
                },
                "ActorType":1,
                "ContentUri":documentUrl,
                "Id":null
            } 
        } ),
        headers: { 
            "accept":"application/json;odata=verbose",
            "content-type":"application/json;odata=verbose",
            "X-RequestDigest":$("#__REQUESTDIGEST").val()
        },
        success: function () { 
            alert('The user has stopped following the document.');
        },
        error: requestFailed
    } );
}

function requestFailed(xhr, ajaxOptions, thrownError) {
    alert('Error:\\n' + xhr.status + '\\n' + thrownError + '\\n' + xhr.responseText);
}
```


## <a name="code-example-start-following-and-stop-following-a-site-by-using-the-sharepoint-rest-service"></a>Пример кода: запустите следующие и отменить подписку на сайт с помощью службы SharePoint REST
<a name="bkmk_FollowSites"> </a>

В следующем примере кода представляет содержимое файла App.js и показано, как:
  
    
    

- Получение URI сайта приложения из строки запроса и создать URI конечной точки  `<siteUri>/_api/social.following` .
    
  
- Создание и отправка запроса **POST** к конечной точке `isfollowed` , чтобы узнать, совместимо ли текущий пользователь уже после указанного сайта.
    
  
- Создание и отправка запроса **POST** к конечной точке `follow` для запуска подписки на сайт.
    
  
- Создание и отправка запроса **POST** к конечной точке `stopfollowing` , чтобы отменить подписку на сайт.
    
  
- Ознакомьтесь с JSON ответ, возвращенный запрос  `isfollowed` и `follow` запроса. (Запрос `stopfollowing` не возвращает все действия в ответе.) В разделе [ответы пример JSON](how-to-follow-documents-sites-and-tags-by-using-the-rest-service-in-sharepoint-2.md#bk_exampleResponses).
    
  
Прежде чем выполнять код измените значение заполнитель для переменной **siteUrl** в соответствии с сайта, которую требуется выполнить. Используйте формат **http://server/siteCollection/site** для сайта в семействе сайтов. Сайта можно выполнить с любой страницы или библиотеки на этом сайте. Если на сайте используется шаблон, который не поддерживает следующие (например, узел личных сайтов или личных сайтов), вы получите ошибку **UnsupportedSite** (код ошибки 10).
  
    
    



```

// Replace the siteUrl placeholder value before you run the code.
var siteUrl = "https://domain.sharepoint.com";
var followingManagerEndpoint;

// Get the SPAppWebUrl parameter from the query string and build
// the Following manager endpoint.
$(document).ready(function () {
    var appweburl;
    var params = document.URL.split("?")[1].split("&amp;");
    for (var i = 0; i < params.length; i = i + 1) {
        var param = params[i].split("=");
        if (param[0] === "SPAppWebUrl") appweburl = param[1];
    }
    followingManagerEndpoint = decodeURIComponent(appweburl) + "/_api/social.following";
    isFollowed();
});

// Check whether the current user is already following the site.
// The request body includes a SocialActorInfo object that represents
// the specified item. 
// The success function reads the response from the REST service and then
// toggles the user's following status by calling the appropriate method.
function isFollowed() {
    $.ajax( {
        url: followingManagerEndpoint + "/isfollowed",
        type: "POST",
        data: JSON.stringify( { 
            "actor": {
                "__metadata": {
                    "type":"SP.Social.SocialActorInfo"
                },
                "ActorType":2,
                "ContentUri":siteUrl,
                "Id":null
            } 
        }),
        headers: { 
            "accept":"application/json;odata=verbose",
            "content-type":"application/json;odata=verbose",
            "X-RequestDigest":$("#__REQUESTDIGEST").val()
        },
        success: function (responseData) { 
            stringData = JSON.stringify(responseData);
            jsonObject = JSON.parse(stringData);
            if (jsonObject.d.IsFollowed === true ) {
                alert('The user is currently following the site.');
                stopFollowSite();
            }
            else {
                alert('The user is currently NOT following the site.');
                followSite();
            }
        },
        error: requestFailed
    });
}

// Make the current user start following a site.
// The request body includes a SocialActorInfo object that represents
// the site to follow.
// The success function reads the response from the REST service.
function followSite() {
    $.ajax( {
        url: followingManagerEndpoint + "/follow",
        type: "POST",
        data: JSON.stringify( { 
            "actor": {
                "__metadata": {
                    "type":"SP.Social.SocialActorInfo"
                },
                "ActorType":2,
                "ContentUri":siteUrl,
                "Id":null
            } 
        } ),
        headers: { 
            "accept":"application/json;odata=verbose",
            "content-type":"application/json;odata=verbose",
            "X-RequestDigest":$("#__REQUESTDIGEST").val()
        },
        success: function (responseData) { 
            stringData = JSON.stringify(responseData);
            jsonObject = JSON.parse(stringData);
            var statusMessage = {
                0 : 'The user has started following the site. ',
                1 : 'The user is already following the site. ',
                2 : 'An internal limit was reached. ',
                3 : 'An internal error occurred. '
            }
            alert(statusMessage[jsonObject.d.Follow] + 'Status code = ' + jsonObject.d.Follow);
        },
        error: requestFailed
    } );
}

// Make the current user stop following a site.
// The request body includes a SocialActorInfo object that represents
// the site to stop following.
function stopFollowSite() {
    $.ajax( {
        url: followingManagerEndpoint + "/stopfollowing",
        type: "POST",
        data: JSON.stringify( { 
            "actor": {
                "__metadata": {
                    "type":"SP.Social.SocialActorInfo"
                },
                "ActorType":2,
                "ContentUri":siteUrl,
                "Id":null
            } 
        } ),
        headers: { 
            "accept":"application/json;odata=verbose",
            "content-type":"application/json;odata=verbose",
            "X-RequestDigest":$("#__REQUESTDIGEST").val()
        },
        success: function () { 
            alert('The user has stopped following the site.');
        },
        error: requestFailed
    } );
}

function requestFailed(xhr, ajaxOptions, thrownError) {
    alert('Error:\\n' + xhr.status + '\\n' + thrownError + '\\n' + xhr.responseText);
}
```


## <a name="code-example-start-following-and-stop-following-a-tag-by-using-the-sharepoint-rest-service"></a>Пример кода: запустите следующие и остановить отслеживание тега с помощью службы SharePoint REST
<a name="bkmk_FollowTags"> </a>

В следующем примере кода представляет содержимое файла App.js и показано, как:
  
    
    

- Получение URI сайта приложения из строки запроса и создать URI конечной точки  `<siteUri>/_api/social.following` .
    
  
- Создание и отправка запроса **POST** к конечной точке `isfollowed` , чтобы узнать, совместимо ли текущий пользователь уже после указанного тега.
    
  
- Создание и отправка запроса **POST** к конечной точке `follow` запуск после тега.
    
  
- Создание и отправка запроса **POST** к конечной точке `stopfollowing` остановка после тега.
    
  
- Ознакомьтесь с JSON ответ, возвращенный запрос  `isfollowed` и `follow` запроса. (Запрос `stopfollowing` не возвращает все действия в ответе.) Для получения дополнительных сведений см [ответы пример JSON](how-to-follow-documents-sites-and-tags-by-using-the-rest-service-in-sharepoint-2.md#bk_exampleResponses).
    
  
Прежде чем выполнять код измените значение заполнитель для переменной **tagGuid** GUID существующего тега. Таксономия API, которая используется для извлечения тега из **HashTagsTermSet** не имеет REST-интерфейса, поэтому необходимо с помощью клиентской объектной модели .NET или JavaScript объектной модели. Узнайте, [Как получить идентификатор GUID тега на основании имя тега с помощью объектной модели JavaScript](follow-content-in-sharepoint.md#bk_getTagGuid) для примера.
  
    
    



```

// Replace the tagGuid placeholder value before you run the code.
var tagGuid = "19a4a484-c1dc-4bc5-8c93-bb96245ce928";
var followingManagerEndpoint;

// Get the SPAppWebUrl parameter from the query string and build
// the Following manager endpoint.
$(document).ready(function () {
    var appweburl;
    var params = document.URL.split("?")[1].split("&amp;");
    for (var i = 0; i < params.length; i = i + 1) {
        var param = params[i].split("=");
        if (param[0] === "SPAppWebUrl") appweburl = param[1];
    }
    followingManagerEndpoint = decodeURIComponent(appweburl) + "/_api/social.following";
    isFollowed();
});

// Check whether the current user is already following the tag.
// The request body includes a SocialActorInfo object that represents
// the specified item. 
// The success function reads the response from the REST service and then
// toggles the user's following status by calling the appropriate method.
function isFollowed() {
    $.ajax( {
        url: followingManagerEndpoint + "/isfollowed",
        type: "POST",
        data: JSON.stringify( { 
            "actor": {
                "__metadata": {
                    "type":"SP.Social.SocialActorInfo"
                },
                "ActorType":3,
                "TagGuid":tagGuid,
                "Id":null
            } 
        }),
        headers: { 
            "accept":"application/json;odata=verbose",
            "content-type":"application/json;odata=verbose",
            "X-RequestDigest":$("#__REQUESTDIGEST").val()
        },
        success: function (responseData) { 
            stringData = JSON.stringify(responseData);
            jsonObject = JSON.parse(stringData);
            if (jsonObject.d.IsFollowed === true ) {
                alert('The user is currently following the tag.');
                stopFollowTag();
            }
            else {
                alert('The user is currently NOT following the tag.');
                followTag();
            }
        },
        error: requestFailed
    });
}

// Make the current user start following a tag.
// The request body includes a SocialActorInfo object that represents
// the tag to follow.
// The success function reads the response from the REST service.
function followTag() {
    $.ajax( {
        url: followingManagerEndpoint + "/follow",
        type: "POST",
        data: JSON.stringify( { 
            "actor": {
                "__metadata": {
                    "type":"SP.Social.SocialActorInfo"
                },
                "ActorType":3,
                "TagGuid":tagGuid,
                "Id":null
            } 
        } ),
        headers: { 
            "accept":"application/json;odata=verbose",
            "content-type":"application/json;odata=verbose",
            "X-RequestDigest":$("#__REQUESTDIGEST").val()
        },
        success: function (responseData) { 
            stringData = JSON.stringify(responseData);
            jsonObject = JSON.parse(stringData);
            var statusMessage = {
                0 : 'The user has started following the tag. ',
                1 : 'The user is already following the tag. ',
                2 : 'An internal limit was reached. ',
                3 : 'An internal error occurred. '
            }
            alert(statusMessage[jsonObject.d.Follow] + 'Status code = ' + jsonObject.d.Follow);
        },
        error: requestFailed
    } );
}

// Make the current user stop following a tag.
// The request body includes a SocialActorInfo object that represents
// the tag to stop following.
function stopFollowTag() {
    $.ajax( {
        url: followingManagerEndpoint + "/stopfollowing",
        type: "POST",
        data: JSON.stringify( { 
            "actor": {
                "__metadata": {
                    "type":"SP.Social.SocialActorInfo"
                },
                "ActorType":3,
                "TagGuid":tagGuid,
                "Id":null
            } 
        } ),
        headers: { 
            "accept":"application/json;odata=verbose",
            "content-type":"application/json;odata=verbose",
            "X-RequestDigest":$("#__REQUESTDIGEST").val()
        },
        success: function () { 
            alert('The user has stopped following the tag.');
        },
        error: requestFailed
    } );
}

function requestFailed(xhr, ajaxOptions, thrownError) {
    alert('Error:\\n' + xhr.status + '\\n' + thrownError + '\\n' + xhr.responseText);
}
```


## <a name="code-example-get-followed-content-by-using-the-sharepoint-rest-service"></a>Пример кода: получение отслеживаемого содержимого с помощью службы SharePoint REST
<a name="bkmk_GetFollowed"> </a>

В следующем примере кода представляет содержимое файла App.js и показано, как:
  
    
    

- Получение URI сайта приложения из строки запроса и создать URI конечной точки  `<siteUri>/_api/social.following` .
    
  
- Создание и отправка запроса **GET** к конечной точке `my/followedcount` для подсчета контента, выполнив текущего пользователя.
    
  
- Создание и отправка запроса **GET** к конечной точке `my/followed` для получения содержимого, выполнив текущего пользователя.
    
  
- Ознакомьтесь с JSON ответ, возвращенный в запросах. В разделе  [ответы пример JSON](how-to-follow-documents-sites-and-tags-by-using-the-rest-service-in-sharepoint-2.md#bk_exampleResponses).
    
  

```

var followingManagerEndpoint;
var followedCount;

// Get the SPAppWebUrl parameter from the query string and build
// the following manager endpoint.
$(document).ready(function () {
    var appweburl;
    var params = document.URL.split("?")[1].split("&amp;");
    for (var i = 0; i < params.length; i = i + 1) {
        var param = params[i].split("=");
        if (param[0] === "SPAppWebUrl") appweburl = param[1];
    }
    followingManagerEndpoint = decodeURIComponent(appweburl)+ "/_api/social.following";
    getMyFollowedCount();
} );

// Get the count of content that the current user is following.
// The "types=14" parameter specifies all content types
// (documents = 2 + sites = 4 + tags = 8).
function getMyFollowedCount() {
    $.ajax( {
        url: followingManagerEndpoint + "/my/followedcount(types=14)",
        headers: { 
            "accept": "application/json;odata=verbose"
        },
        success: function (data) { 
            followedCount = data.d.FollowedCount;
            getMyFollowedContent();
        },
        error: requestFailed
    } );
}

// Get the content that the current user is following.
// The "types=14" parameter specifies all content types
// (documents = 2 + sites = 4 + tags = 8).
function getMyFollowedContent() {
    $.ajax( {
        url: followingManagerEndpoint + "/my/followed(types=14)",
        headers: { 
            "accept": "application/json;odata=verbose"
        },
        success: followedContentRetrieved,
        error: requestFailed
    });
}

// Parse the JSON data and iterate through the collection.
function followedContentRetrieved(data) {
    var stringData = JSON.stringify(data);
    var jsonObject = JSON.parse(stringData); 
    var types = {
        1: "document",
        2: "site",
        3: "tag" 
    };
 
    var followedActors = jsonObject.d.Followed.results; 
    var followedList = "You're following " + followedCount + " items:";
    for (var i = 0; i < followedActors.length; i++) {
        var actor = followedActors[i];
        followedList += "<p>The " + types[actor.ActorType] + ": \\"" +
        actor.Name + "\\"</p>";
    } 
    $("#message").html(followedList); 
}

function requestFailed(xhr, ajaxOptions, thrownError) {
    alert('Error:\\n' + xhr.status + '\\n' + thrownError + '\\n' + xhr.responseText);
}
```


## <a name="example-json-responses-for-following-content-requests"></a>Пример JSON ответы для запросов следующие контента
<a name="bk_exampleResponses"> </a>

По умолчанию службы REST возвращает ответы, отформатированные с помощью протокола Atom, но можно запросить формат JSON с помощью **Accept** заголовок HTTP (например: `"accept":"application/json;odata=verbose"`). Данные ответа возвращается в виде строки, и можно использовать функции **JSON.stringify** и **JSON.parse** для преобразования строки в объект, как показано в предыдущих примерах кода.
  
    
    
Для устранения ошибки, возвращенной службы REST в режиме отладки, посмотрите на свойство **responseText**, как показано в функции обратного вызова **requestFailed** в предыдущих примерах. Также вы можете получить идентификатор корреляции для журнала сервера ULS на прослушивания сети или отладчик HTTP, такие как Fiddler. Идентификатор корреляции  это то же, что код запроса в HTTP-ответа.
  
    
    

### <a name="example-response-for-the-follow-endpoint"></a>Пример ответа для конечной точки, выполните

В ответ на стороне клиента запросы к конечной точке  `follow` службы REST возвращает значение **SocialFollowResult**, представляет ли запрос **Follow** успешно.
  
    
    
Приведенный ниже ответ представляет состояние **AlreadyFollowing**.
  
    
    



```

{"d":{"Follow":1}}
```

В таблице 1 приведены коды состояния **SocialFollowResult** и их значения.
  
    
    

**В таблице 1. Коды SocialFollowResult и значения**

|**Код состояния**|**Значение**|
|:-----|:-----|
|0|**OK**. Текущий пользователь является теперь следующую субъект.|
|1|**AlreadyFollowing**. Текущий пользователь уже подписан субъект.|
|2|**LimitReached**. Запрос завершился ошибкой, так как достигнут внутренний предел.|
|3|**InternalError**. Не удалось выполнить запрос из-за внутренней ошибки.|
   
> [!NOTE]
> [!Примечание] Службы REST не возвращает ответ на запрос **StopFollowing**. Она возвращает `{"d":{"StopFollowing":null}}`. 
  
    
    


### <a name="example-response-for-the-isfollowed-endpoint"></a>Пример ответа для конечной точки IsFollowed

В ответ на стороне клиента запросы к конечной точке  `isfollowed` службы REST возвращает значение **bool**, представляет ли текущий пользователь является выполнив указанного субъекта.
  
    
    
Приведенный ниже ответ указывает, что текущий пользователь не подписан указанный документ, сайта или тег.
  
    
    



```
{"d":{"IsFollowed":false}}
```


### <a name="example-response-for-the-myfollowed-endpoint"></a>Пример ответа для конечной точки личных/мотренная

В ответ на стороне клиента запросы к конечной точке  `my/followed` службы REST возвращает массив объектов **SP.Social.SocialActor**, представляющих документы, сайты и теги, выполнив текущего пользователя.
  
    
    
Приведенный ниже ответ представляет число документов, сайта и тег. Запрос указывает типы контента для включения.
  
    
    



```
{"d":{"Followed":{"results":[
  {"__metadata":{"type":"SP.Social.SocialActor"}
    "AccountName":null
    "ActorType":1
    "CanFollow":true
    "ContentUri":"https://domain.sharepoint.com:443/Shared%20Documents/fileName.docx"
    "EmailAddress":null
    "FollowedContentUri":null
    "Id":"2.089f4944a6374a64b52b7af5ba140392.9340a4837688405daa6b83f2b58f973d.
      51bbb5d8e214457ba794669345d23040.98b9fc73d5224265b039586688b15b98"
    "ImageUri":null
    "IsFollowed":true
    "LibraryUri":null
    "Name":"snippets.txt"
    "PersonalSiteUri":null
    "Status":0
    "StatusText":null
    "TagGuid":"00000000-0000-0000-0000-000000000000"
    "Title":null
    "Uri":"https://domain.sharepoint.com:443/Shared%20Documents/fileName.docx"
  }
  {"__metadata":{"type":"SP.Social.SocialActor"}
    "AccountName":null
    "ActorType":2
    "CanFollow":true
    "ContentUri":"https://domain.sharepoint.com:443/"
    "EmailAddress":null
    "FollowedContentUri":null
    "Id":"8.089f4944a6374a64b52b7af5ba140392.9340a4837688405daa6b83f2b58f973d.
      089f4944a6374a64b52b7af5ba140392.98b9fc73d5224265b039586688b15b98"
    "ImageUri":null
    "IsFollowed":true
    "LibraryUri":null
    "Name":"Developer Site"
    "PersonalSiteUri":null
    "Status":0
    "StatusText":null
    "TagGuid":"00000000-0000-0000-0000-000000000000"
    "Title":null
    "Uri":"https://domain.sharepoint.com:443/"
  }
  {"__metadata":{"type":"SP.Social.SocialActor"}
    "AccountName":null
    "ActorType":3
    "CanFollow":true
    "ContentUri":null
    "EmailAddress":null
    "FollowedContentUri":null
    "Id":"16.00000000000000000000000000000000.00000000000000000000000000000000.
      19a4a484c1dc4bc58c93bb96245ce928.98b9fc73d5224265b039586688b15b98"
    "ImageUri":null
    "IsFollowed":true
    "LibraryUri":null
    "Name":"#someTag"
    "PersonalSiteUri":null
    "Status":0
    "StatusText":null
    "TagGuid":"19a4a484-c1dc-4bc5-8c93-bb96245ce928"
    "Title":null
    "Uri":"https://domain-my.sharepoint.com:443/_layouts/15/HashTagProfile.aspx?
      TermID=19a4a484-c1dc-4bc5-8c93-bb96245ce928"
  }
]}}}
```


### <a name="example-response-for-the-myfollowedcount-endpoint"></a>Пример ответа для конечной точки личных/FollowedCount

В ответ на стороне клиента запросы к конечной точке  `my/followedcount` службы REST возвращается значение **Int32**, представляющее общее число типов указанного субъекта, выполнив текущего пользователя.
  
    
    
Приведенный ниже ответ представляет число три число документов, сайтов и/или теги. Запрос указывает типы контента для включения.
  
    
    



```

{"d":{"FollowedCount":3}}
```


## <a name="see-also"></a>См. также
<a name="bkmk_AddtionalResources"> </a>


-  [Подписка на контент в SharePoint](follow-content-in-sharepoint.md)
    
  
-  [Following people and content REST API reference for SharePoint](following-people-and-content-rest-api-reference-for-sharepoint.md)
    
  
-  [Как подписываться на документы и сайты, используя клиентскую объектную модель .NET в SharePoint](how-to-follow-documents-and-sites-by-using-the-net-client-object-model-in-sharep.md)
    
  

