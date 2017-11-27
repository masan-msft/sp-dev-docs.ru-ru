---
title: "Подписка на людей с помощью объектной модели JavaScript в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 2643c286-47c9-4a7a-9273-7474394477d6
ms.openlocfilehash: 32f8d67f05048a15d3c1e2d0d1313f38945ff593
ms.sourcegitcommit: f6ea922341c38e700d0697961f8df9a454a03cba
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/15/2017
---
# <a name="follow-people-by-using-the-javascript-object-model-in-sharepoint"></a><span data-ttu-id="1d7d9-102">Подписка на людей с помощью объектной модели JavaScript в SharePoint</span><span class="sxs-lookup"><span data-stu-id="1d7d9-102">Follow people by using the JavaScript object model in SharePoint</span></span>

<span data-ttu-id="1d7d9-103">Узнайте, как работать с функцией подписки на пользователей с помощью объектной модели JavaScript для SharePoint.</span><span class="sxs-lookup"><span data-stu-id="1d7d9-103">Learn how to work with Following People features by using the SharePoint JavaScript object model.</span></span>

## <a name="why-use-following-people-features-in-sharepoint"></a><span data-ttu-id="1d7d9-104">Причины использования функций следующих пользователей в SharePoint?</span><span class="sxs-lookup"><span data-stu-id="1d7d9-104">Why use Following People features in SharePoint?</span></span>
<span data-ttu-id="1d7d9-105"><a name="bk_FollowingPeopleFeatures"> </a></span><span class="sxs-lookup"><span data-stu-id="1d7d9-105"></span></span>

<span data-ttu-id="1d7d9-106">В SharePoint следующие сотрудники возможности помогают пользователям всегда оставаться на связи друг с другом.</span><span class="sxs-lookup"><span data-stu-id="1d7d9-106">In SharePoint, Following People features help users to stay connected with each other.</span></span> <span data-ttu-id="1d7d9-107">Например когда кто-то подписан пользователь, публикации и действия этого лица отображаются в канал новостей пользователя.</span><span class="sxs-lookup"><span data-stu-id="1d7d9-107">For example, when a user follows someone, that person's posts and activities show up in the user's newsfeed.</span></span> <span data-ttu-id="1d7d9-108">С помощью функции следующие сотрудники сосредоточиться на пользователей, которые важны пользователей, можно улучшить релевантности приложений или решений.</span><span class="sxs-lookup"><span data-stu-id="1d7d9-108">By using Following People features to focus on the people who users care about, you can improve the relevance of your app or solution.</span></span> <span data-ttu-id="1d7d9-109">В объектной модели JavaScript людей, которые вы выполните представлены объектами [SocialActor](http://msdn.microsoft.com/library/4e369fd5-b9b0-9804-957e-b3e39c559cd4%28Office.15%29.aspx) .</span><span class="sxs-lookup"><span data-stu-id="1d7d9-109">In the JavaScript object model, people that you follow are represented by  [SocialActor](http://msdn.microsoft.com/library/4e369fd5-b9b0-9804-957e-b3e39c559cd4%28Office.15%29.aspx) objects.</span></span> <span data-ttu-id="1d7d9-110">Для выполнения основных задач следующие сотрудники в объектной модели JavaScript, используйте объект [SocialFollowingManager](http://msdn.microsoft.com/library/9ee1c0c0-b864-f0c3-f0cb-4dd4f1870dfa%28Office.15%29.aspx) .</span><span class="sxs-lookup"><span data-stu-id="1d7d9-110">To perform core Following People tasks in the JavaScript object model, you use the [SocialFollowingManager](http://msdn.microsoft.com/library/9ee1c0c0-b864-f0c3-f0cb-4dd4f1870dfa%28Office.15%29.aspx) object.</span></span> <span data-ttu-id="1d7d9-111">В этой статье описывается использование объектной модели JavaScript для работы с функциями следующие сотрудники.</span><span class="sxs-lookup"><span data-stu-id="1d7d9-111">This article shows how to use the JavaScript object model to work with Following People features.</span></span>
  
    
    
> <span data-ttu-id="1d7d9-112">**Примечание:**
> [SocialFollowingManager](http://msdn.microsoft.com/library/9ee1c0c0-b864-f0c3-f0cb-4dd4f1870dfa%28Office.15%29.aspx) рекомендуется использовать для следующие людей и контент.</span><span class="sxs-lookup"><span data-stu-id="1d7d9-112">**Note:**
[SocialFollowingManager](http://msdn.microsoft.com/library/9ee1c0c0-b864-f0c3-f0cb-4dd4f1870dfa%28Office.15%29.aspx) is the recommended API to use for following people and content.</span></span> <span data-ttu-id="1d7d9-113">Тем не менее объект [PeopleManager](http://msdn.microsoft.com/library/985fd2df-0e31-6ece-b846-ba2ccb156d00%28Office.15%29.aspx) содержит дополнительные функции для следующих пользователей, таких как метод [amIFollowedBy](http://msdn.microsoft.com/library/3641c469-0063-054d-355d-e56697cb08ae%28Office.15%29.aspx) и методы, которые получить следующие состояния другим пользователям.</span><span class="sxs-lookup"><span data-stu-id="1d7d9-113">However, the [PeopleManager](http://msdn.microsoft.com/library/985fd2df-0e31-6ece-b846-ba2ccb156d00%28Office.15%29.aspx) object contains additional functionality for following people, such as the [amIFollowedBy](http://msdn.microsoft.com/library/3641c469-0063-054d-355d-e56697cb08ae%28Office.15%29.aspx) method and methods that obtain the following status of other users.</span></span>
  
    
    


## <a name="prerequisites-for-setting-up-your-development-environment-to-work-with-following-people-features-by-using-the-sharepoint-javascript-object-model"></a><span data-ttu-id="1d7d9-114">Необходимые условия для настройки среды разработки для работы с функциями следующих пользователей с помощью объектной модели SharePoint JavaScript</span><span class="sxs-lookup"><span data-stu-id="1d7d9-114">Prerequisites for setting up your development environment to work with Following People features by using the SharePoint JavaScript object model</span></span>
<span data-ttu-id="1d7d9-115"><a name="bk_Prereqs"> </a></span><span class="sxs-lookup"><span data-stu-id="1d7d9-115"></span></span>

<span data-ttu-id="1d7d9-116">Чтобы создать решение фермы, которая использует объектную модель JavaScript для работы с функциями следующие сотрудники, то необходимо:</span><span class="sxs-lookup"><span data-stu-id="1d7d9-116">To create the farm solution that uses the JavaScript object model to work with Following People features, you'll need:</span></span>
  
    
    

- <span data-ttu-id="1d7d9-117">SharePoint с личного сайта настроены и профили пользователей и личные сайты, созданные для текущего пользователя и конечного пользователя</span><span class="sxs-lookup"><span data-stu-id="1d7d9-117">SharePoint with My Site configured, and with user profiles and personal sites created for the current user and a target user</span></span>
    
  
- <span data-ttu-id="1d7d9-118">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="1d7d9-118">Visual Studio 2012</span></span>
    
  
- <span data-ttu-id="1d7d9-119">Инструменты разработчика Office для Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="1d7d9-119">Office Developer Tools for Visual Studio 2012</span></span>
    
  
- <span data-ttu-id="1d7d9-120">**Полный** доступ к приложению-службе профилей пользователей для пользователя, вошедшего в систему</span><span class="sxs-lookup"><span data-stu-id="1d7d9-120">**Full Control** access permissions to the User Profile service application for the logged-on user</span></span>
    
  
- <span data-ttu-id="1d7d9-121">Разрешения локального администратора для пользователя, вошедшего в систему</span><span class="sxs-lookup"><span data-stu-id="1d7d9-121">Local administrator permissions for the logged-on user</span></span>
    
  

## <a name="create-a-farm-solution-and-application-page-in-visual-studio-2012"></a><span data-ttu-id="1d7d9-122">Создайте страницу фермы решения и приложения в Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="1d7d9-122">Create a farm solution and application page in Visual Studio 2012</span></span>
<span data-ttu-id="1d7d9-123"><a name="bk_CreateSolution"> </a></span><span class="sxs-lookup"><span data-stu-id="1d7d9-123"></span></span>


1. <span data-ttu-id="1d7d9-124">Запустите Visual Studio от имени администратора и выберите **файл**, **Создать**, **проект**.</span><span class="sxs-lookup"><span data-stu-id="1d7d9-124">Run Visual Studio as administrator, and choose **File**, **New**, **Project**.</span></span>
    
  
2. <span data-ttu-id="1d7d9-125">В диалоговом окне **Новый проект** выберите **.NET Framework 4.5** из раскрывающегося списка в верхней части окна.</span><span class="sxs-lookup"><span data-stu-id="1d7d9-125">In the **New Project** dialog box, choose **.NET Framework 4.5** from the drop-down list at the top of the dialog box.</span></span>
    
  
3. <span data-ttu-id="1d7d9-126">В списке **Шаблоны** разверните узел **Office/SharePoint**, щелкните **Решения SharePoint**и затем выберите шаблон **SharePoint — пустой проект** .</span><span class="sxs-lookup"><span data-stu-id="1d7d9-126">In the **Templates** list, expand **Office/SharePoint**, choose **SharePoint Solutions**, and then choose the **SharePoint - Empty Project** template.</span></span>
    
  
4. <span data-ttu-id="1d7d9-127">Назовите проект FollowPeopleJSOMи затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="1d7d9-127">Name the project FollowPeopleJSOM, and then choose the **OK** button.</span></span>
    
  
5. <span data-ttu-id="1d7d9-128">В диалоговом окне **Мастер настройки SharePoint** выберите **Развернуть как решение фермы** и затем нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="1d7d9-128">In the **SharePoint Customization Wizard** dialog box, choose **Deploy as a farm solution**, and then choose the **Finish** button.</span></span>
    
  
6. <span data-ttu-id="1d7d9-129">В **Обозревателе решений** откройте контекстное меню для проекта **FollowPeopleJSOM** и добавьте SharePoint "Макеты" сопоставленная папка.</span><span class="sxs-lookup"><span data-stu-id="1d7d9-129">In **Solution Explorer**, open the shortcut menu for the **FollowPeopleJSOM** project, and then add a SharePoint "Layouts" mapped folder.</span></span>
    
  
7. <span data-ttu-id="1d7d9-130">В папке **Layouts** откройте контекстное меню для папки **FollowPeopleJSOM** и добавьте новую страницу приложения SharePoint с именемFollowPeople.aspx.</span><span class="sxs-lookup"><span data-stu-id="1d7d9-130">In the **Layouts** folder, open the shortcut menu for the **FollowPeopleJSOM** folder, and then add a new SharePoint application page namedFollowPeople.aspx.</span></span>
    
   > <span data-ttu-id="1d7d9-131">**Примечание:** Примеры кода в этой статье определение пользовательского кода в разметке страницы, но не используйте класс фонового кода, который создает Visual Studio для страницы.</span><span class="sxs-lookup"><span data-stu-id="1d7d9-131">**Note:** The code examples in this article define custom code in the page markup but do not use the code-behind class that Visual Studio creates for the page.</span></span> 

8. <span data-ttu-id="1d7d9-132">Откройте контекстное меню для страницы FollowPeople.aspx и нажмите кнопку **Set as Startup Item**.</span><span class="sxs-lookup"><span data-stu-id="1d7d9-132">Open the shortcut menu for the FollowPeople.aspx page, and then choose **Set as Startup Item**.</span></span>
    
  
9. <span data-ttu-id="1d7d9-p103">В разметке файла FollowPeople.aspx вставьте следующий код в тегах **asp:Content** «Главная». Этот код определяет элементы управления и ссылки на сценарии.</span><span class="sxs-lookup"><span data-stu-id="1d7d9-p103">In the markup of the FollowPeople.aspx file, paste the following code between the "Main" **asp:Content** tags. This code defines controls and script references.</span></span>
    
```HTML
<span id="followResults"></span><br/><br />
<button id="sendRequest" type="button"></button><br/>
<span id="message" style="color: #FF0000;"></span>
<script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2.min.js" type="text/javascript"></script>
<SharePoint:ScriptLink name="SP.js" runat="server" ondemand="false" localizable="false" loadafterui="true" />
<SharePoint:ScriptLink name="SP.UserProfiles.js" runat="server" ondemand="false" localizable="false" loadafterui="true" />
<SharePoint:FormDigest id="FormDigest" runat="server"/>
<script type="text/javascript">
    // Replace this comment with the code for your scenario. 
</script>
```

   > <span data-ttu-id="1d7d9-135">**Примечание:** В примере «Получить последователи и пользователей» не использует элемент управления button или управления дайджест формы, который является только необходимые для операций, которые обновления содержимого сервера.</span><span class="sxs-lookup"><span data-stu-id="1d7d9-135">**Note:** The "Get followers and followed people" example doesn't use the button control or the form digest control, which is only required for operations that update server content.</span></span> <span data-ttu-id="1d7d9-136">Дайджест формы создает дайджест сообщения, используемый для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="1d7d9-136">A form digest generates a message digest used for security validation.</span></span> 

10. <span data-ttu-id="1d7d9-137">Замените комментарий между тегами **script** с пример кода из одного из следующих сценариев:</span><span class="sxs-lookup"><span data-stu-id="1d7d9-137">Replace the comment between the **script** tags with the code example from one of the following scenarios:</span></span>
    
  -  [<span data-ttu-id="1d7d9-138">Запуск или остановка отслеживаемые пользователи</span><span class="sxs-lookup"><span data-stu-id="1d7d9-138">Start or stop following people</span></span>](how-to-follow-people-by-using-the-javascript-object-model-in-sharepoint.md#bk_FollowPeople)  
  -  [<span data-ttu-id="1d7d9-139">Получите последователи и пользователей</span><span class="sxs-lookup"><span data-stu-id="1d7d9-139">Get followers and followed people</span></span>](how-to-follow-people-by-using-the-javascript-object-model-in-sharepoint.md#bk_GetFollowers)
    
11. <span data-ttu-id="1d7d9-140">Тестирование решения, в строке меню выберите **Отладка**, **Начать отладку**.</span><span class="sxs-lookup"><span data-stu-id="1d7d9-140">To test the solution, on the menu bar, choose **Debug**, **Start Debugging**.</span></span>
    
  

## <a name="code-example-start-or-stop-following-people-by-using-the-sharepoint-javascript-object-model"></a><span data-ttu-id="1d7d9-141">Пример кода: запустить или остановить следующие людей с помощью объектной модели SharePoint JavaScript</span><span class="sxs-lookup"><span data-stu-id="1d7d9-141">Code example: Start or stop following people by using the SharePoint JavaScript object model</span></span>
<span data-ttu-id="1d7d9-142"><a name="bk_FollowPeople"> </a></span><span class="sxs-lookup"><span data-stu-id="1d7d9-142"></span></span>

<span data-ttu-id="1d7d9-p105">В следующем примере кода делает текущего пользователя запустить следующие или остановить после конечного пользователя. В нем показано, как:</span><span class="sxs-lookup"><span data-stu-id="1d7d9-p105">The following code example makes the current user start following or stop following a target user. It shows how to:</span></span>
  
    
    

- <span data-ttu-id="1d7d9-145">Проверьте, является ли текущий пользователь выполнив конечного пользователя с помощью метода  [isFollowed](http://msdn.microsoft.com/library/2c1f62e6-fb75-ad4d-c081-36408b418c21%28Office.15%29.aspx) .</span><span class="sxs-lookup"><span data-stu-id="1d7d9-145">Check whether the current user is following a target user by using the  [isFollowed](http://msdn.microsoft.com/library/2c1f62e6-fb75-ad4d-c081-36408b418c21%28Office.15%29.aspx) method.</span></span>
    
  
- <span data-ttu-id="1d7d9-146">Получение числа пользователей, которые текущий пользователь подписан с помощью метода  [getFollowedCount](http://msdn.microsoft.com/library/97b53b4f-481a-cf41-1854-8f3ff860b2bb%28Office.15%29.aspx) .</span><span class="sxs-lookup"><span data-stu-id="1d7d9-146">Get the count of people who the current user is following by using the  [getFollowedCount](http://msdn.microsoft.com/library/97b53b4f-481a-cf41-1854-8f3ff860b2bb%28Office.15%29.aspx) method.</span></span>
    
  
- <span data-ttu-id="1d7d9-147">Запустите следующие конечного пользователя с помощью метода  [выполните](http://msdn.microsoft.com/library/40d14320-27ba-2941-b0e2-be3b5a407c89%28Office.15%29.aspx) .</span><span class="sxs-lookup"><span data-stu-id="1d7d9-147">Start following the target user by using the  [follow](http://msdn.microsoft.com/library/40d14320-27ba-2941-b0e2-be3b5a407c89%28Office.15%29.aspx) method.</span></span>
    
  
- <span data-ttu-id="1d7d9-148">Отменить подписку конечного пользователя с помощью метода  [stopFollowing](http://msdn.microsoft.com/library/65b0e9be-dc5e-09fb-c57f-7a933de09a4c%28Office.15%29.aspx) .</span><span class="sxs-lookup"><span data-stu-id="1d7d9-148">Stop following the target user by using the  [stopFollowing](http://msdn.microsoft.com/library/65b0e9be-dc5e-09fb-c57f-7a933de09a4c%28Office.15%29.aspx) method.</span></span>
    
  

> <span data-ttu-id="1d7d9-149">**Примечание:** Вставьте следующий код между тегами **сценария** , которые добавлены в процедуре [создать решение фермы и страницы приложения](how-to-follow-people-by-using-the-javascript-object-model-in-sharepoint.md#bk_CreateSolution) .</span><span class="sxs-lookup"><span data-stu-id="1d7d9-149">**Note:** Paste the following code between the **script** tags that you added in the [Create a farm solution and application page](how-to-follow-people-by-using-the-javascript-object-model-in-sharepoint.md#bk_CreateSolution) procedure.</span></span> <span data-ttu-id="1d7d9-150">Измените значение заполнитель для переменной **targetUser** до выполнения этого кода.</span><span class="sxs-lookup"><span data-stu-id="1d7d9-150">Then, change the placeholder value for the **targetUser** variable before you run the code.</span></span>
  
    
    


```

// Replace the placeholder value with the account name of the target user.
var targetUser = 'domain\\userName';

var clientContext;
var followingManager;
var actorInfo;
var isFollowed;
var followedCount;

// Ensure that the SP.UserProfiles.js file is loaded before running your code.
$(document).ready(function () {
    SP.SOD.executeOrDelayUntilScriptLoaded(getFollowingStatus, 'SP.UserProfiles.js');
});

// Get the Following status of the current user.
function getFollowingStatus() {

    // Get the current client context.
    clientContext = SP.ClientContext.get_current();

    // Get the SocialFeedManager instance.
    followingManager = new SP.Social.SocialFollowingManager(clientContext);

    // Create a SocialActorInfo object to represent the target user.
    actorInfo = new SP.Social.SocialActorInfo();
    actorInfo.set_accountName(targetUser);

    // Find out whether the current user is following the target user.
    isFollowed = followingManager.isFollowed(actorInfo);
    followedCount = followingManager.getFollowedCount(1);

    // Get the information from the server.
    clientContext.executeQueryAsync(showFollowingStatus, requestFailed)
}

// Show the Following status of the current user.
function showFollowingStatus() {
    var results = '';
    results += 'Is the current user following the target user? ' + isFollowed.get_value();
    results += '<br/>Total count of followed people: ' + followedCount.get_value();
    $('#followResults').html(results);

    // Initialize the button for this example.
    $('#sendRequest').click(
        function () {
            $('#message').empty();
            toggleFollowingStatus();
        });
    $('#sendRequest').text('Toggle following status');
}

// Follow or stop following the target user.
function toggleFollowingStatus() {
    if (isFollowed.get_value() === false) {
        followingManager.follow(actorInfo);
    }
    else if (isFollowed.get_value() === true) {
        followingManager.stopFollowing(actorInfo);
    }
    clientContext.executeQueryAsync(getFollowingStatus, requestFailed);
}

// Failure callback.
function requestFailed(sender, args) {
    $('#message').html('Error: ' + args.get_message());
}
```


## <a name="code-example-get-followers-and-followed-people-by-using-the-sharepoint-javascript-object-model"></a><span data-ttu-id="1d7d9-151">Пример кода: получение последователи и отслеживаемого людей с помощью объектной модели SharePoint JavaScript</span><span class="sxs-lookup"><span data-stu-id="1d7d9-151">Code example: Get followers and followed people by using the SharePoint JavaScript object model</span></span>
<span data-ttu-id="1d7d9-152"><a name="bk_GetFollowers"> </a></span><span class="sxs-lookup"><span data-stu-id="1d7d9-152"></span></span>

<span data-ttu-id="1d7d9-p107">В следующем примере кода получает людей, текущий пользователь отслеживание и получает пользователей, которые следуют текущего пользователя. В нем показано, как:</span><span class="sxs-lookup"><span data-stu-id="1d7d9-p107">The following code example gets the people who the current user is following and gets the people who are followed by the current user. It shows how to:</span></span>
  
    
    

- <span data-ttu-id="1d7d9-155">Получите пользователей, которые текущий пользователь подписан с помощью метода  [getFollowed](http://msdn.microsoft.com/library/432a7cec-6add-fdb1-a79f-a93414ee8cd3%28Office.15%29.aspx) .</span><span class="sxs-lookup"><span data-stu-id="1d7d9-155">Get the people who the current user is following by using the  [getFollowed](http://msdn.microsoft.com/library/432a7cec-6add-fdb1-a79f-a93414ee8cd3%28Office.15%29.aspx) method.</span></span>
    
  
- <span data-ttu-id="1d7d9-156">Получите пользователей, которые отслеживаются текущего пользователя с помощью метода  [getFollowers](http://msdn.microsoft.com/library/ae4a944b-c043-05fb-c74b-101d2ce4a813%28Office.15%29.aspx) , передав **1** для представления типов actor **User**.</span><span class="sxs-lookup"><span data-stu-id="1d7d9-156">Get the people who are following the current user by using the  [getFollowers](http://msdn.microsoft.com/library/ae4a944b-c043-05fb-c74b-101d2ce4a813%28Office.15%29.aspx) method and passing **1** to represent **User** actor types.</span></span>
    
  
- <span data-ttu-id="1d7d9-157">Выполните итерацию по группам людей или get отображения имени, личного сайта URI пользователя, а также рисунок URI.</span><span class="sxs-lookup"><span data-stu-id="1d7d9-157">Iterate through the groups of people and get each person's display name, personal site URI, and picture URI.</span></span>
    
  

> <span data-ttu-id="1d7d9-158">**Примечание:** Вставьте следующий код между тегами **сценария** , которые добавлены в процедуре [создать решение фермы и страницы приложения](how-to-follow-people-by-using-the-javascript-object-model-in-sharepoint.md#bk_CreateSolution) .</span><span class="sxs-lookup"><span data-stu-id="1d7d9-158">**Note:** Paste the following code between the **script** tags that you added in the [Create a farm solution and application page](how-to-follow-people-by-using-the-javascript-object-model-in-sharepoint.md#bk_CreateSolution) procedure.</span></span>
  
    
    


```

var followed;
var followers;

// Ensure that the SP.UserProfiles.js file is loaded before running your code.
$(document).ready(function () {
    SP.SOD.executeOrDelayUntilScriptLoaded(getFollowedAndFollowers, 'SP.UserProfiles.js');

    // Hide the button for this example.
    $('#sendRequest').hide();
});

// Get the Following status of the current user.
function getFollowedAndFollowers() {

    // Get the current client context.
    var clientContext = SP.ClientContext.get_current();

    // Get the SocialFeedManager instance.
    var followingManager = new SP.Social.SocialFollowingManager(clientContext);

    // Get followed people and followers.
    followers = followingManager.getFollowers();
    followed = followingManager.getFollowed(1);

    // Send the request to the server.
    clientContext.executeQueryAsync(showFollowedAndFollowers, requestFailed)
}

// Show the Following status of the current user.
function showFollowedAndFollowers() {
    var results = 'The current user is following ' + followed.length + ' people: <br/>';

    for (var i = 0; i < followed.length; i++) {
        var user = followed[i];
        var name = user.get_name();
        var personalSiteUri = user.get_personalSiteUri();
        var pictureUri = user.get_imageUri();

        results += '<br/>' + name + '<br/>' + personalSiteUri + '<br/>' + pictureUri + '<br/>';
    }

    results += '<br/>The current user is followed by ' + followers.length + ' people: <br/>';

    for (var i = 0; i < followers.length; i++) {
        var user = followers[i];
        var name = user.get_name();
        var personalSiteUri = user.get_personalSiteUri();
        var pictureUri = user.get_imageUri();

        results += '<br/>' + name + '<br/>' + personalSiteUri + '<br/>' + pictureUri + '<br/>';
    }
    $('#followResults').html(results);
}

// Failure callback.
function requestFailed(sender, args) {
    $('#message').html('Error: ' + args.get_message());
}
```


## <a name="additional-resources"></a><span data-ttu-id="1d7d9-159">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="1d7d9-159">Additional resources</span></span>
<span data-ttu-id="1d7d9-160"><a name="bk_AdditionalResources"> </a></span><span class="sxs-lookup"><span data-stu-id="1d7d9-160"></span></span>


-  [<span data-ttu-id="1d7d9-161">Подписка на людей в SharePoint</span><span class="sxs-lookup"><span data-stu-id="1d7d9-161">Follow people in SharePoint</span></span>](follow-people-in-sharepoint.md)
    
  
-  [<span data-ttu-id="1d7d9-162">Как подписываться на пользователей, используя клиентскую объектную модель .NET в SharePoint</span><span class="sxs-lookup"><span data-stu-id="1d7d9-162">How to: Follow people by using the .NET client object model in SharePoint</span></span>](how-to-follow-people-by-using-the-net-client-object-model-in-sharepoint.md)
    
  

