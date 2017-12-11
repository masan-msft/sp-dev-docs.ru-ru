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
# <a name="follow-documents-sites-and-tags-by-using-the-rest-service-in-sharepoint"></a><span data-ttu-id="6b501-102">Выполните указанные документы, сайты и теги с помощью службы REST в SharePoint</span><span class="sxs-lookup"><span data-stu-id="6b501-102">Follow documents, sites, and tags by using the REST service in SharePoint</span></span>

<span data-ttu-id="6b501-103">Создание размещенных в SharePoint приложений, подписка на контент (документы, сайты и теги) с помощью службы REST и для получения отслеживаемого содержимого.</span><span class="sxs-lookup"><span data-stu-id="6b501-103">Create SharePoint-hosted apps that use the REST service to follow content (documents, sites, and tags) and to get followed content.</span></span>

## <a name="how-do-i-use-the-sharepoint-rest-service-to-follow-content"></a><span data-ttu-id="6b501-104">Как использовать службы SharePoint REST для подписка на контент?</span><span class="sxs-lookup"><span data-stu-id="6b501-104">How do I use the SharePoint REST service to follow content?</span></span>
<span data-ttu-id="6b501-105"><a name="bk_intro"> </a></span><span class="sxs-lookup"><span data-stu-id="6b501-105"><a name="bk_intro"> </a></span></span>

<span data-ttu-id="6b501-106">Пользователи SharePoint можно следовать документы, сайты и теги для получения обновлений об элементах в свои каналы новостей и быстро открыть число документов и сайтов.</span><span class="sxs-lookup"><span data-stu-id="6b501-106">SharePoint users can follow documents, sites, and tags to get updates about the items in their newsfeeds and to quickly open followed documents and sites.</span></span> <span data-ttu-id="6b501-107">API-Интерфейс REST SharePoint можно использовать в вашем приложении или решение, которое требуется запустить следующие материалы, остановите следующие материалы и получить отслеживаемого содержимого от имени текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="6b501-107">You can use the SharePoint REST API in your app or solution to start following content, stop following content, and get followed content on behalf of the current user.</span></span>
  
    
    
<span data-ttu-id="6b501-108">Доступны следующие ресурсы REST, основного API для контента следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="6b501-108">The following REST resources are the primary API for Following Content tasks:</span></span>
  
    
    

- <span data-ttu-id="6b501-109">**SocialRestFollowingManager** предоставляет методы для управления пользовательского списка число субъектов.</span><span class="sxs-lookup"><span data-stu-id="6b501-109">**SocialRestFollowingManager** provides methods for managing a user's list of followed actors.</span></span>
    
  
- <span data-ttu-id="6b501-110">**SocialActor** представляет документ, сайта или тег, сервер возвращает в ответ на запрос на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="6b501-110">**SocialActor** represents a document, site, or tag that the server returns in response to a client-side request.</span></span>
    
  
- <span data-ttu-id="6b501-111">**SocialActorInfo** указывает документ, сайта или тега в запросах со стороны клиента к серверу.</span><span class="sxs-lookup"><span data-stu-id="6b501-111">**SocialActorInfo** specifies a document, site, or tag in client-side requests to the server.</span></span>
    
  
- <span data-ttu-id="6b501-112">**SocialActorType** и **SocialActorTypes** укажите типы контента в запросах со стороны клиента к серверу.</span><span class="sxs-lookup"><span data-stu-id="6b501-112">**SocialActorType** and **SocialActorTypes** specify content types in client-side requests to the server.</span></span>
    
  
<span data-ttu-id="6b501-p102">Для выполнения следующих контента задач с помощью интерфейса API REST, службы REST отправки HTTP **GET** и **POST** HTTP-запросов. URI конечных точек REST для следующих контента задач начинаются с **SocialRestFollowingManager** ресурсов ( `<siteUri>/_api/social.following`) и заканчиваются ознакомьтесь со следующими ресурсами:</span><span class="sxs-lookup"><span data-stu-id="6b501-p102">To perform Following Content tasks by using the REST API, you send HTTP **GET** and HTTP **POST** requests to the REST service. REST endpoint URIs for Following Content tasks begin with the **SocialRestFollowingManager** resource ( `<siteUri>/_api/social.following`) and end with one of the following resources:</span></span>
  
    
    

- <span data-ttu-id="6b501-115">**follow** запуск отслеживание документа, сайта или тега</span><span class="sxs-lookup"><span data-stu-id="6b501-115">**follow** to start following a document, site, or tag</span></span>
    
  
- <span data-ttu-id="6b501-116">**stopfollowing**, чтобы отменить подписку на документ, сайта или тега</span><span class="sxs-lookup"><span data-stu-id="6b501-116">**stopfollowing** to stop following a document, site, or tag</span></span>
    
  
- <span data-ttu-id="6b501-117">**isfollowed**, чтобы узнать, совместимо ли после пользователя конкретного документа, сайта или тега</span><span class="sxs-lookup"><span data-stu-id="6b501-117">**isfollowed** to find out whether the user is following a specific document, site, or tag</span></span>
    
  
- <span data-ttu-id="6b501-118">**my/followed**, чтобы получить число документов, сайтов и тегов</span><span class="sxs-lookup"><span data-stu-id="6b501-118">**my/followed** to get followed documents, sites, and tags</span></span>
    
  
- <span data-ttu-id="6b501-119">**my/followedcount** для подсчета число документов, сайтов и тегов</span><span class="sxs-lookup"><span data-stu-id="6b501-119">**my/followedcount** to get the count of followed documents, sites, and tags</span></span>
    
> [!NOTE]
> <span data-ttu-id="6b501-120">Для следующих пользователей задачи, но **последователи** и **предложений** ресурсы, доступные из поддерживают только **SocialRestFollowingManager** , отслеживаемые пользователи не контента также использовать эти конечные точки.</span><span class="sxs-lookup"><span data-stu-id="6b501-120">You also use these endpoints for Following People tasks, but the **followers** and **suggestions** resources available from **SocialRestFollowingManager** only support following people, not content.</span></span> <span data-ttu-id="6b501-121">Дополнительные сведения об использовании **SocialRestFollowingManager**можно [Подписка на контент в SharePoint](follow-content-in-sharepoint.md) и [Подписка на людей в SharePoint](follow-people-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="6b501-121">For more information about how you can use **SocialRestFollowingManager**, see  [Follow content in SharePoint](follow-content-in-sharepoint.md) and [Follow people in SharePoint](follow-people-in-sharepoint.md).</span></span> 
  
    
    


## <a name="prerequisites-for-creating-a-sharepoint-hosted-app-that-manages-followed-content-by-using-the-sharepoint-rest-service"></a><span data-ttu-id="6b501-122">Необходимые условия для создания приложения с размещением в SharePoint, который управляет отслеживаемого содержимого с помощью службы SharePoint REST</span><span class="sxs-lookup"><span data-stu-id="6b501-122">Prerequisites for creating a SharePoint-hosted app that manages followed content by using the SharePoint REST service</span></span>
<span data-ttu-id="6b501-123"><a name="bkmk_Prereqs"> </a></span><span class="sxs-lookup"><span data-stu-id="6b501-123"><a name="bkmk_Prereqs"> </a></span></span>

<span data-ttu-id="6b501-p104">В этой статье предполагается, что вы создаете надстройку для SharePoint с помощью Napa на сайте разработчика Office 365. Если вы используете эту среду разработки, то необходимые условия выполняются.</span><span class="sxs-lookup"><span data-stu-id="6b501-p104">This article assumes that you create the SharePoint Add-in by using Napa on an Office 365 Developer Site. If you're using this development environment, you've already met the prerequisites.</span></span>
  
> [!NOTE]
> <span data-ttu-id="6b501-126">[!Примечание] Перейдите к  [Настройка среды для разработки надстроек SharePoint в Office 365](http://msdn.microsoft.com/library/b22ce52a-ae9e-4831-9b68-c9210af6dc54%28Office.15%29.aspx) Зарегистрируйтесь на сайте разработчика и начать использовать Napa.</span><span class="sxs-lookup"><span data-stu-id="6b501-126">Go to  [Set up a development environment for SharePoint Add-ins on Office 365](http://msdn.microsoft.com/library/b22ce52a-ae9e-4831-9b68-c9210af6dc54%28Office.15%29.aspx) to sign up for a Developer Site and start using Napa.</span></span>
  
    
    

<span data-ttu-id="6b501-127">Если вы не используете Napa на Office 365 сайт разработчика, необходимо перед развертыванием Надстройка SharePoint выполняются следующие требования:</span><span class="sxs-lookup"><span data-stu-id="6b501-127">If you're not using Napa on an Office 365 Developer Site, you'll need to meet the following prerequisites before you can deploy the SharePoint Add-in:</span></span>
  
    
    

- <span data-ttu-id="6b501-128">Среда разработки SharePoint, которые настроены для изоляции приложений.</span><span class="sxs-lookup"><span data-stu-id="6b501-128">A SharePoint development environment that is configured for app isolation.</span></span> <span data-ttu-id="6b501-129">При разработке удаленно, сервер должен поддерживать sideloading приложения или приложения необходимо установить на сайте разработчика.</span><span class="sxs-lookup"><span data-stu-id="6b501-129">If you're developing remotely, the server must support sideloading of apps or you must install the app on a Developer Site.</span></span>
    
  
- <span data-ttu-id="6b501-130">Узел Личный сайт, настроены на личный сайт, созданный для текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="6b501-130">The My Site host configured, with a personal site created for the current user.</span></span>
    
  
- <span data-ttu-id="6b501-131">Visual Studio 2012 или Visual Studio 2013 с Инструменты разработчика Office для Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="6b501-131">Visual Studio 2012 or Visual Studio 2013 with Office Developer Tools for Visual Studio 2013.</span></span>
    
  
- <span data-ttu-id="6b501-132">Достаточные разрешения для пользователя, вошедшего в систему:</span><span class="sxs-lookup"><span data-stu-id="6b501-132">Sufficient permissions for the logged-on user:</span></span>
    
  - <span data-ttu-id="6b501-133">Разрешения локального администратора на компьютере разработчика.</span><span class="sxs-lookup"><span data-stu-id="6b501-133">Local administrator permissions on the development computer.</span></span>
    
  
  - <span data-ttu-id="6b501-p106">Управление разрешениями пользователей веб-сайта и создание дочерних сайтов на сайте SharePoint, на котором устанавливается приложение. По умолчанию эти разрешения доступны только для пользователей, имеющий уровень разрешений полного доступа или пользователей, которые входят в группу владельцев сайта.</span><span class="sxs-lookup"><span data-stu-id="6b501-p106">Manage Web Site and Create Subsites user permissions to the SharePoint site where you're installing the app. By default, these permissions are available only to users who have the Full Control permission level or who are in the site Owners group.</span></span>
    
  
  - <span data-ttu-id="6b501-p107">Необходимо войти в систему как кто-то отличную от учетной записи системы. Системная учетная запись не имеет разрешения, чтобы установить приложение.</span><span class="sxs-lookup"><span data-stu-id="6b501-p107">You must be logged on as someone other than the system account. The system account does not have permission to install the app.</span></span>
    
> [!NOTE]
> <span data-ttu-id="6b501-138">[!Примечание] В разделе  [Настройка локальной среды разработки надстроек SharePoint](http://msdn.microsoft.com/library/b0878c12-27c9-4eea-ae3b-7e79e5a8838d%28Office.15%29.aspx) руководство по локальной установки (включая отключение проверки замыкания на себя при необходимости).</span><span class="sxs-lookup"><span data-stu-id="6b501-138">See  [Set up an on-premises development environment for SharePoint Add-ins](http://msdn.microsoft.com/library/b0878c12-27c9-4eea-ae3b-7e79e5a8838d%28Office.15%29.aspx) for guidance about on-premises setup (including how to disable the loopback check, if necessary).</span></span>
  
    
    


  
    
    

## <a name="create-the-sharepoint-add-in-project"></a><span data-ttu-id="6b501-139">Создайте проект надстройки для SharePoint.</span><span class="sxs-lookup"><span data-stu-id="6b501-139">Create the SharePoint Add-in project</span></span>
<span data-ttu-id="6b501-140"><a name="bkmk_CreateApp"> </a></span><span class="sxs-lookup"><span data-stu-id="6b501-140"><a name="bkmk_CreateApp"> </a></span></span>


1. <span data-ttu-id="6b501-141">На сайте разработчика откройте Napa и выберите **Добавить новый проект**.</span><span class="sxs-lookup"><span data-stu-id="6b501-141">On your Developer Site, open Napa, and then choose **Add New Project**.</span></span>
    
  
2. <span data-ttu-id="6b501-142">Выберите шаблон **приложение для SharePoint**, назовите проект и затем нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="6b501-142">Choose the **App for SharePoint** template, name the project, and then choose the **Create** button.</span></span>
    
  
3. <span data-ttu-id="6b501-143">Установка разрешений для вашего приложения:</span><span class="sxs-lookup"><span data-stu-id="6b501-143">Set the permissions for your app:</span></span>
    
   1. <span data-ttu-id="6b501-144">В нижней части страницы нажмите кнопку **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="6b501-144">Choose the **Properties** button at the bottom of the page.</span></span>
    
  
   2. <span data-ttu-id="6b501-145">В окне **Свойства** выберите **разрешения**.</span><span class="sxs-lookup"><span data-stu-id="6b501-145">In the **Properties** window, choose **Permissions**.</span></span>
    
  
   3. <span data-ttu-id="6b501-146">В разделе категория **контента** задайте разрешения **Write** для области **клиента**.</span><span class="sxs-lookup"><span data-stu-id="6b501-146">In the **Content** category, set **Write** permissions for the **Tenant** scope.</span></span>
    
  
   4. <span data-ttu-id="6b501-147">В разделе категория **социальных** задайте разрешения **Read** для области **Профили пользователей**.</span><span class="sxs-lookup"><span data-stu-id="6b501-147">In the **Social** category, set **Read** permissions for the **User Profiles** scope.</span></span>
    
  
   5. <span data-ttu-id="6b501-148">Закройте окно **свойств**.</span><span class="sxs-lookup"><span data-stu-id="6b501-148">Close the **Properties** window.</span></span>
    
  
4. <span data-ttu-id="6b501-149">Разверните узел **скриптов**, откройте файл App.js и замените его содержимое на код из одного из следующих сценариев:</span><span class="sxs-lookup"><span data-stu-id="6b501-149">Expand the **Scripts** node, choose the App.js file and replace its contents with the code from one of the following scenarios:</span></span>
    
   -  [<span data-ttu-id="6b501-150">Запустите следующие и остановите следующие документа</span><span class="sxs-lookup"><span data-stu-id="6b501-150">Start following and stop following a document</span></span>](how-to-follow-documents-sites-and-tags-by-using-the-rest-service-in-sharepoint-2.md#bkmk_FollowDocs)
   -  [<span data-ttu-id="6b501-151">Запустите следующие и отменить подписку на сайт</span><span class="sxs-lookup"><span data-stu-id="6b501-151">Start following and stop following a site</span></span>](how-to-follow-documents-sites-and-tags-by-using-the-rest-service-in-sharepoint-2.md#bkmk_FollowSites)
   -  [<span data-ttu-id="6b501-152">Запустите следующие и остановить отслеживание тега</span><span class="sxs-lookup"><span data-stu-id="6b501-152">Start following and stop following a tag</span></span>](how-to-follow-documents-sites-and-tags-by-using-the-rest-service-in-sharepoint-2.md#bkmk_FollowTags)
   -  [<span data-ttu-id="6b501-153">Получение следования за контентом</span><span class="sxs-lookup"><span data-stu-id="6b501-153">Get followed content</span></span>](how-to-follow-documents-sites-and-tags-by-using-the-rest-service-in-sharepoint-2.md#bkmk_GetFollowed)
  
5. <span data-ttu-id="6b501-154">Чтобы запустить приложение, нажмите кнопку **Запустить проект** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="6b501-154">To run the app, choose the **Run Project** button at the bottom of the page.</span></span>
    
  
6. <span data-ttu-id="6b501-p108">В **вы доверяете** открывшейся странице нажмите кнопку **Доверять его**. Страница приложения открывает и выполняет код. Чтобы выполнить отладку страницы, нажмите клавишу **F12** и выберите App.js на вкладке **скрипта**.</span><span class="sxs-lookup"><span data-stu-id="6b501-p108">In the **Do you trust** page that opens, choose the **Trust It** button. The app page opens and runs the code. To debug the page, choose the **F12** key and then choose App.js on the **Script** tab.</span></span>
    
  

## <a name="code-example-start-following-and-stop-following-a-document-by-using-the-sharepoint-rest-service"></a><span data-ttu-id="6b501-158">Пример кода: запустите следующие и остановите следующие документа с помощью службы SharePoint REST</span><span class="sxs-lookup"><span data-stu-id="6b501-158">Code example: Start following and stop following a document by using the SharePoint REST service</span></span>
<span data-ttu-id="6b501-159"><a name="bkmk_FollowDocs"> </a></span><span class="sxs-lookup"><span data-stu-id="6b501-159"><a name="bkmk_FollowDocs"> </a></span></span>

<span data-ttu-id="6b501-160">В следующем примере кода представляет содержимое файла App.js и показано, как:</span><span class="sxs-lookup"><span data-stu-id="6b501-160">The following code example represents the contents of the App.js file and shows how to:</span></span>
  
    
    

- <span data-ttu-id="6b501-161">Получение URI сайта приложения из строки запроса и создать URI конечной точки  `<siteUri>/_api/social.following` .</span><span class="sxs-lookup"><span data-stu-id="6b501-161">Get the app web URI from the query string and construct the  `<siteUri>/_api/social.following` endpoint URI.</span></span>
    
  
- <span data-ttu-id="6b501-162">Создание и отправка запроса **POST** к конечной точке `isfollowed` , чтобы узнать, совместимо ли текущий пользователь уже после указанного документа.</span><span class="sxs-lookup"><span data-stu-id="6b501-162">Build and send a **POST** request to the `isfollowed` endpoint to find out whether the current user is already following a specified document.</span></span>
    
  
- <span data-ttu-id="6b501-163">Создание и отправка запроса **POST** к конечной точке `follow` запуск после документа.</span><span class="sxs-lookup"><span data-stu-id="6b501-163">Build and send a **POST** request to the `follow` endpoint to start following the document.</span></span>
    
  
- <span data-ttu-id="6b501-164">Создание и отправка запроса **POST** к конечной точке `stopfollowing` , чтобы отменить подписку на документ.</span><span class="sxs-lookup"><span data-stu-id="6b501-164">Build and send a **POST** request to the `stopfollowing` endpoint to stop following the document.</span></span>
    
  
- <span data-ttu-id="6b501-p109">Ознакомьтесь с JSON ответ, возвращенный запрос  `isfollowed` и `follow` запроса. (Запрос `stopfollowing` не возвращает все действия в ответе.) В разделе [ответы пример JSON](how-to-follow-documents-sites-and-tags-by-using-the-rest-service-in-sharepoint-2.md#bk_exampleResponses).</span><span class="sxs-lookup"><span data-stu-id="6b501-p109">Read the JSON response returned by the  `isfollowed` request and the `follow` request. (The `stopfollowing` request doesn't return anything in the response.) See [Example JSON responses](how-to-follow-documents-sites-and-tags-by-using-the-rest-service-in-sharepoint-2.md#bk_exampleResponses).</span></span>
    
  
<span data-ttu-id="6b501-167">Прежде чем запустить код необходимо отправить документ и измените значение заполнитель для переменной **documentUrl** URL-адрес документа.</span><span class="sxs-lookup"><span data-stu-id="6b501-167">Before you run the code, you'll need to upload a document and change the placeholder value for the **documentUrl** variable to the document's URL.</span></span>
  
    
    



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


## <a name="code-example-start-following-and-stop-following-a-site-by-using-the-sharepoint-rest-service"></a><span data-ttu-id="6b501-168">Пример кода: запустите следующие и отменить подписку на сайт с помощью службы SharePoint REST</span><span class="sxs-lookup"><span data-stu-id="6b501-168">Code example: Start following and stop following a site by using the SharePoint REST service</span></span>
<span data-ttu-id="6b501-169"><a name="bkmk_FollowSites"> </a></span><span class="sxs-lookup"><span data-stu-id="6b501-169"><a name="bkmk_FollowSites"> </a></span></span>

<span data-ttu-id="6b501-170">В следующем примере кода представляет содержимое файла App.js и показано, как:</span><span class="sxs-lookup"><span data-stu-id="6b501-170">The following code example represents the contents of the App.js file and shows how to:</span></span>
  
    
    

- <span data-ttu-id="6b501-171">Получение URI сайта приложения из строки запроса и создать URI конечной точки  `<siteUri>/_api/social.following` .</span><span class="sxs-lookup"><span data-stu-id="6b501-171">Get the app web URI from the query string and construct the  `<siteUri>/_api/social.following` endpoint URI.</span></span>
    
  
- <span data-ttu-id="6b501-172">Создание и отправка запроса **POST** к конечной точке `isfollowed` , чтобы узнать, совместимо ли текущий пользователь уже после указанного сайта.</span><span class="sxs-lookup"><span data-stu-id="6b501-172">Build and send a **POST** request to the `isfollowed` endpoint to find out whether the current user is already following a specified site.</span></span>
    
  
- <span data-ttu-id="6b501-173">Создание и отправка запроса **POST** к конечной точке `follow` для запуска подписки на сайт.</span><span class="sxs-lookup"><span data-stu-id="6b501-173">Build and send a **POST** request to the `follow` endpoint to start following the site.</span></span>
    
  
- <span data-ttu-id="6b501-174">Создание и отправка запроса **POST** к конечной точке `stopfollowing` , чтобы отменить подписку на сайт.</span><span class="sxs-lookup"><span data-stu-id="6b501-174">Build and send a **POST** request to the `stopfollowing` endpoint to stop following the site.</span></span>
    
  
- <span data-ttu-id="6b501-p110">Ознакомьтесь с JSON ответ, возвращенный запрос  `isfollowed` и `follow` запроса. (Запрос `stopfollowing` не возвращает все действия в ответе.) В разделе [ответы пример JSON](how-to-follow-documents-sites-and-tags-by-using-the-rest-service-in-sharepoint-2.md#bk_exampleResponses).</span><span class="sxs-lookup"><span data-stu-id="6b501-p110">Read the JSON response returned by the  `isfollowed` request and the `follow` request. (The `stopfollowing` request doesn't return anything in the response.) See [Example JSON responses](how-to-follow-documents-sites-and-tags-by-using-the-rest-service-in-sharepoint-2.md#bk_exampleResponses).</span></span>
    
  
<span data-ttu-id="6b501-p111">Прежде чем выполнять код измените значение заполнитель для переменной **siteUrl** в соответствии с сайта, которую требуется выполнить. Используйте формат **http://server/siteCollection/site** для сайта в семействе сайтов. Сайта можно выполнить с любой страницы или библиотеки на этом сайте. Если на сайте используется шаблон, который не поддерживает следующие (например, узел личных сайтов или личных сайтов), вы получите ошибку **UnsupportedSite** (код ошибки 10).</span><span class="sxs-lookup"><span data-stu-id="6b501-p111">Before you run the code, change the placeholder value for the **siteUrl** variable to match the site that you want to follow. Use the format **http://server/siteCollection/site** for a site in a site collection. You can follow a site from any page or library in that site. If the site uses a template that doesn't support following (like the My Site host or a personal site), you'll get an **UnsupportedSite** error (error code 10).</span></span>
  
    
    



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


## <a name="code-example-start-following-and-stop-following-a-tag-by-using-the-sharepoint-rest-service"></a><span data-ttu-id="6b501-181">Пример кода: запустите следующие и остановить отслеживание тега с помощью службы SharePoint REST</span><span class="sxs-lookup"><span data-stu-id="6b501-181">Code example: Start following and stop following a tag by using the SharePoint REST service</span></span>
<span data-ttu-id="6b501-182"><a name="bkmk_FollowTags"> </a></span><span class="sxs-lookup"><span data-stu-id="6b501-182"><a name="bkmk_FollowTags"> </a></span></span>

<span data-ttu-id="6b501-183">В следующем примере кода представляет содержимое файла App.js и показано, как:</span><span class="sxs-lookup"><span data-stu-id="6b501-183">The following code example represents the contents of the App.js file and shows how to:</span></span>
  
    
    

- <span data-ttu-id="6b501-184">Получение URI сайта приложения из строки запроса и создать URI конечной точки  `<siteUri>/_api/social.following` .</span><span class="sxs-lookup"><span data-stu-id="6b501-184">Get the app web URI from the query string and construct the  `<siteUri>/_api/social.following` endpoint URI.</span></span>
    
  
- <span data-ttu-id="6b501-185">Создание и отправка запроса **POST** к конечной точке `isfollowed` , чтобы узнать, совместимо ли текущий пользователь уже после указанного тега.</span><span class="sxs-lookup"><span data-stu-id="6b501-185">Build and send a **POST** request to the `isfollowed` endpoint to find out whether the current user is already following a specified tag.</span></span>
    
  
- <span data-ttu-id="6b501-186">Создание и отправка запроса **POST** к конечной точке `follow` запуск после тега.</span><span class="sxs-lookup"><span data-stu-id="6b501-186">Build and send a **POST** request to the `follow` endpoint to start following the tag.</span></span>
    
  
- <span data-ttu-id="6b501-187">Создание и отправка запроса **POST** к конечной точке `stopfollowing` остановка после тега.</span><span class="sxs-lookup"><span data-stu-id="6b501-187">Build and send a **POST** request to the `stopfollowing` endpoint to stop following the tag.</span></span>
    
  
- <span data-ttu-id="6b501-p112">Ознакомьтесь с JSON ответ, возвращенный запрос  `isfollowed` и `follow` запроса. (Запрос `stopfollowing` не возвращает все действия в ответе.) Для получения дополнительных сведений см [ответы пример JSON](how-to-follow-documents-sites-and-tags-by-using-the-rest-service-in-sharepoint-2.md#bk_exampleResponses).</span><span class="sxs-lookup"><span data-stu-id="6b501-p112">Read the JSON response returned by the  `isfollowed` request and the `follow` request. (The `stopfollowing` request doesn't return anything in the response.) For more information, see [Example JSON responses](how-to-follow-documents-sites-and-tags-by-using-the-rest-service-in-sharepoint-2.md#bk_exampleResponses).</span></span>
    
  
<span data-ttu-id="6b501-p113">Прежде чем выполнять код измените значение заполнитель для переменной **tagGuid** GUID существующего тега. Таксономия API, которая используется для извлечения тега из **HashTagsTermSet** не имеет REST-интерфейса, поэтому необходимо с помощью клиентской объектной модели .NET или JavaScript объектной модели. Узнайте, [Как получить идентификатор GUID тега на основании имя тега с помощью объектной модели JavaScript](follow-content-in-sharepoint.md#bk_getTagGuid) для примера.</span><span class="sxs-lookup"><span data-stu-id="6b501-p113">Before you run the code, change the placeholder value for the **tagGuid** variable to the GUID of an existing tag. The taxonomy API that you use to retrieve a tag from the **HashTagsTermSet** doesn't have a REST interface, so you have to use the .NET client object model or the JavaScript object model. See [How to get a tag's GUID based on the tag's name by using the JavaScript object model](follow-content-in-sharepoint.md#bk_getTagGuid) for an example.</span></span>
  
    
    



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


## <a name="code-example-get-followed-content-by-using-the-sharepoint-rest-service"></a><span data-ttu-id="6b501-193">Пример кода: получение отслеживаемого содержимого с помощью службы SharePoint REST</span><span class="sxs-lookup"><span data-stu-id="6b501-193">Code example: Get followed content by using the SharePoint REST service</span></span>
<span data-ttu-id="6b501-194"><a name="bkmk_GetFollowed"> </a></span><span class="sxs-lookup"><span data-stu-id="6b501-194"><a name="bkmk_GetFollowed"> </a></span></span>

<span data-ttu-id="6b501-195">В следующем примере кода представляет содержимое файла App.js и показано, как:</span><span class="sxs-lookup"><span data-stu-id="6b501-195">The following code example represents the contents of the App.js file and shows how to:</span></span>
  
    
    

- <span data-ttu-id="6b501-196">Получение URI сайта приложения из строки запроса и создать URI конечной точки  `<siteUri>/_api/social.following` .</span><span class="sxs-lookup"><span data-stu-id="6b501-196">Get the app web URI from the query string and construct the  `<siteUri>/_api/social.following` endpoint URI.</span></span>
    
  
- <span data-ttu-id="6b501-197">Создание и отправка запроса **GET** к конечной точке `my/followedcount` для подсчета контента, выполнив текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="6b501-197">Build and send a **GET** request to the `my/followedcount` endpoint to get the count of content that the current user is following.</span></span>
    
  
- <span data-ttu-id="6b501-198">Создание и отправка запроса **GET** к конечной точке `my/followed` для получения содержимого, выполнив текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="6b501-198">Build and send a **GET** request to the `my/followed` endpoint to get the content that the current user is following.</span></span>
    
  
- <span data-ttu-id="6b501-p114">Ознакомьтесь с JSON ответ, возвращенный в запросах. В разделе  [ответы пример JSON](how-to-follow-documents-sites-and-tags-by-using-the-rest-service-in-sharepoint-2.md#bk_exampleResponses).</span><span class="sxs-lookup"><span data-stu-id="6b501-p114">Read the JSON response returned by the requests. See  [Example JSON responses](how-to-follow-documents-sites-and-tags-by-using-the-rest-service-in-sharepoint-2.md#bk_exampleResponses).</span></span>
    
  

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


## <a name="example-json-responses-for-following-content-requests"></a><span data-ttu-id="6b501-201">Пример JSON ответы для запросов следующие контента</span><span class="sxs-lookup"><span data-stu-id="6b501-201">Example JSON responses for Following Content requests</span></span>
<span data-ttu-id="6b501-202"><a name="bk_exampleResponses"> </a></span><span class="sxs-lookup"><span data-stu-id="6b501-202"><a name="bk_exampleResponses"> </a></span></span>

<span data-ttu-id="6b501-p115">По умолчанию службы REST возвращает ответы, отформатированные с помощью протокола Atom, но можно запросить формат JSON с помощью **Accept** заголовок HTTP (например: `"accept":"application/json;odata=verbose"`). Данные ответа возвращается в виде строки, и можно использовать функции **JSON.stringify** и **JSON.parse** для преобразования строки в объект, как показано в предыдущих примерах кода.</span><span class="sxs-lookup"><span data-stu-id="6b501-p115">By default, the REST service returns responses that are formatted by using the Atom protocol, but you can request the JSON format by using an HTTP **Accept** header (for example: `"accept":"application/json;odata=verbose"`). The response data is returned as a string, and you can use the **JSON.stringify** function and **JSON.parse** function to convert the string into an object, as shown in the previous code examples.</span></span>
  
    
    
<span data-ttu-id="6b501-p116">Для устранения ошибки, возвращенной службы REST в режиме отладки, посмотрите на свойство **responseText**, как показано в функции обратного вызова **requestFailed** в предыдущих примерах. Также вы можете получить идентификатор корреляции для журнала сервера ULS на прослушивания сети или отладчик HTTP, такие как Fiddler. Идентификатор корреляции  это то же, что код запроса в HTTP-ответа.</span><span class="sxs-lookup"><span data-stu-id="6b501-p116">To troubleshoot an error returned by the REST service, in debug mode, look at the **responseText** property, as shown in the **requestFailed** callback functions in the previous examples. You can also get the correlation ID for the ULS server log from a network sniffer or HTTP debugger, such as Fiddler. The correlation ID is the same as the request ID in the HTTP response.</span></span>
  
    
    

### <a name="example-response-for-the-follow-endpoint"></a><span data-ttu-id="6b501-208">Пример ответа для конечной точки, выполните</span><span class="sxs-lookup"><span data-stu-id="6b501-208">Example response for the Follow endpoint</span></span>

<span data-ttu-id="6b501-209">В ответ на стороне клиента запросы к конечной точке  `follow` службы REST возвращает значение **SocialFollowResult**, представляет ли запрос **Follow** успешно.</span><span class="sxs-lookup"><span data-stu-id="6b501-209">In response to client-side requests to the  `follow` endpoint, the REST service returns a **SocialFollowResult** value that represents whether the **Follow** request succeeded.</span></span>
  
    
    
<span data-ttu-id="6b501-210">Приведенный ниже ответ представляет состояние **AlreadyFollowing**.</span><span class="sxs-lookup"><span data-stu-id="6b501-210">The following response represents the **AlreadyFollowing** status.</span></span>
  
    
    



```

{"d":{"Follow":1}}
```

<span data-ttu-id="6b501-211">В таблице 1 приведены коды состояния **SocialFollowResult** и их значения.</span><span class="sxs-lookup"><span data-stu-id="6b501-211">Table 1 shows **SocialFollowResult** status codes and their values.</span></span>
  
    
    

<span data-ttu-id="6b501-212">**В таблице 1. Коды SocialFollowResult и значения**</span><span class="sxs-lookup"><span data-stu-id="6b501-212">**Table 1. SocialFollowResult codes and values**</span></span>

|<span data-ttu-id="6b501-213">**Код состояния**</span><span class="sxs-lookup"><span data-stu-id="6b501-213">**Status code**</span></span>|<span data-ttu-id="6b501-214">**Значение**</span><span class="sxs-lookup"><span data-stu-id="6b501-214">**Value**</span></span>|
|:-----|:-----|
|<span data-ttu-id="6b501-215">0</span><span class="sxs-lookup"><span data-stu-id="6b501-215">0</span></span>|<span data-ttu-id="6b501-p117">**OK**. Текущий пользователь является теперь следующую субъект.</span><span class="sxs-lookup"><span data-stu-id="6b501-p117">**OK**. The current user is now following the actor.</span></span>|
|<span data-ttu-id="6b501-218">1</span><span class="sxs-lookup"><span data-stu-id="6b501-218">1</span></span>|<span data-ttu-id="6b501-p118">**AlreadyFollowing**. Текущий пользователь уже подписан субъект.</span><span class="sxs-lookup"><span data-stu-id="6b501-p118">**AlreadyFollowing**. The current user is already following the actor.</span></span>|
|<span data-ttu-id="6b501-221">2</span><span class="sxs-lookup"><span data-stu-id="6b501-221">2</span></span>|<span data-ttu-id="6b501-p119">**LimitReached**. Запрос завершился ошибкой, так как достигнут внутренний предел.</span><span class="sxs-lookup"><span data-stu-id="6b501-p119">**LimitReached**. The request failed because an internal limit was reached.</span></span>|
|<span data-ttu-id="6b501-224">3</span><span class="sxs-lookup"><span data-stu-id="6b501-224">3</span></span>|<span data-ttu-id="6b501-p120">**InternalError**. Не удалось выполнить запрос из-за внутренней ошибки.</span><span class="sxs-lookup"><span data-stu-id="6b501-p120">**InternalError**. The request failed due to an internal error.</span></span>|
   
> [!NOTE]
> <span data-ttu-id="6b501-p121">[!Примечание] Службы REST не возвращает ответ на запрос **StopFollowing**. Она возвращает `{"d":{"StopFollowing":null}}`.</span><span class="sxs-lookup"><span data-stu-id="6b501-p121">The REST service doesn't return a response for the **StopFollowing** request. It returns `{"d":{"StopFollowing":null}}`.</span></span> 
  
    
    


### <a name="example-response-for-the-isfollowed-endpoint"></a><span data-ttu-id="6b501-229">Пример ответа для конечной точки IsFollowed</span><span class="sxs-lookup"><span data-stu-id="6b501-229">Example response for the IsFollowed endpoint</span></span>

<span data-ttu-id="6b501-230">В ответ на стороне клиента запросы к конечной точке  `isfollowed` службы REST возвращает значение **bool**, представляет ли текущий пользователь является выполнив указанного субъекта.</span><span class="sxs-lookup"><span data-stu-id="6b501-230">In response to client-side requests to the  `isfollowed` endpoint, the REST service returns a **bool** value that represents whether the current user is following the specified actor.</span></span>
  
    
    
<span data-ttu-id="6b501-231">Приведенный ниже ответ указывает, что текущий пользователь не подписан указанный документ, сайта или тег.</span><span class="sxs-lookup"><span data-stu-id="6b501-231">The following response indicates that the current user is not following the specified document, site, or tag.</span></span>
  
    
    



```
{"d":{"IsFollowed":false}}
```


### <a name="example-response-for-the-myfollowed-endpoint"></a><span data-ttu-id="6b501-232">Пример ответа для конечной точки личных/мотренная</span><span class="sxs-lookup"><span data-stu-id="6b501-232">Example response for the My/Followed endpoint</span></span>

<span data-ttu-id="6b501-233">В ответ на стороне клиента запросы к конечной точке  `my/followed` службы REST возвращает массив объектов **SP.Social.SocialActor**, представляющих документы, сайты и теги, выполнив текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="6b501-233">In response to client-side requests to the  `my/followed` endpoint, the REST service returns an array of **SP.Social.SocialActor** objects that represent documents, sites, and tags that the current user is following.</span></span>
  
    
    
<span data-ttu-id="6b501-p122">Приведенный ниже ответ представляет число документов, сайта и тег. Запрос указывает типы контента для включения.</span><span class="sxs-lookup"><span data-stu-id="6b501-p122">The following response represents a followed document, site, and tag. The request specifies the types of content to include.</span></span>
  
    
    



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


### <a name="example-response-for-the-myfollowedcount-endpoint"></a><span data-ttu-id="6b501-236">Пример ответа для конечной точки личных/FollowedCount</span><span class="sxs-lookup"><span data-stu-id="6b501-236">Example response for the My/FollowedCount endpoint</span></span>

<span data-ttu-id="6b501-237">В ответ на стороне клиента запросы к конечной точке  `my/followedcount` службы REST возвращается значение **Int32**, представляющее общее число типов указанного субъекта, выполнив текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="6b501-237">In response to client-side requests to the  `my/followedcount` endpoint, the REST service returns an **Int32** value that represents the total count of specified actor types that the current user is following.</span></span>
  
    
    
<span data-ttu-id="6b501-p123">Приведенный ниже ответ представляет число три число документов, сайтов и/или теги. Запрос указывает типы контента для включения.</span><span class="sxs-lookup"><span data-stu-id="6b501-p123">The following response represents a count of three followed documents, sites, and/or tags. The request specifies the types of content to include.</span></span>
  
    
    



```

{"d":{"FollowedCount":3}}
```


## <a name="see-also"></a><span data-ttu-id="6b501-240">См. также</span><span class="sxs-lookup"><span data-stu-id="6b501-240">See also</span></span>
<span data-ttu-id="6b501-241"><a name="bkmk_AddtionalResources"> </a></span><span class="sxs-lookup"><span data-stu-id="6b501-241"></span></span>


-  [<span data-ttu-id="6b501-242">Подписка на контент в SharePoint</span><span class="sxs-lookup"><span data-stu-id="6b501-242">Follow content in SharePoint</span></span>](follow-content-in-sharepoint.md)
    
  
-  [<span data-ttu-id="6b501-243">Following people and content REST API reference for SharePoint</span><span class="sxs-lookup"><span data-stu-id="6b501-243">Following people and content REST API reference for SharePoint</span></span>](following-people-and-content-rest-api-reference-for-sharepoint.md)
    
  
-  [<span data-ttu-id="6b501-244">Как подписываться на документы и сайты, используя клиентскую объектную модель .NET в SharePoint</span><span class="sxs-lookup"><span data-stu-id="6b501-244">How to: Follow documents and sites by using the .NET client object model in SharePoint</span></span>](how-to-follow-documents-and-sites-by-using-the-net-client-object-model-in-sharep.md)
    
  

