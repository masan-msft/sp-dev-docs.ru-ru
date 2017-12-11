---
title: "Подписка на людей с помощью объектной модели JavaScript в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 2643c286-47c9-4a7a-9273-7474394477d6
ms.openlocfilehash: 441c7e8085f28ddf58e627b8f8261d04a035c916
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="follow-people-by-using-the-javascript-object-model-in-sharepoint"></a>Подписка на людей с помощью объектной модели JavaScript в SharePoint

Узнайте, как работать с функцией подписки на пользователей с помощью объектной модели JavaScript для SharePoint.

## <a name="why-use-following-people-features-in-sharepoint"></a>Причины использования функций следующих пользователей в SharePoint?
<a name="bk_FollowingPeopleFeatures"> </a>

В SharePoint следующие сотрудники возможности помогают пользователям всегда оставаться на связи друг с другом. Например когда кто-то подписан пользователь, публикации и действия этого лица отображаются в канал новостей пользователя. С помощью функции следующие сотрудники сосредоточиться на пользователей, которые важны пользователей, можно улучшить релевантности приложений или решений. В объектной модели JavaScript людей, которые вы выполните представлены объектами [SocialActor](http://msdn.microsoft.com/library/4e369fd5-b9b0-9804-957e-b3e39c559cd4%28Office.15%29.aspx) . Для выполнения основных задач следующие сотрудники в объектной модели JavaScript, используйте объект [SocialFollowingManager](http://msdn.microsoft.com/library/9ee1c0c0-b864-f0c3-f0cb-4dd4f1870dfa%28Office.15%29.aspx) . В этой статье описывается использование объектной модели JavaScript для работы с функциями следующие сотрудники.
  
> [!NOTE]
> [!Примечание]  [SocialFollowingManager](http://msdn.microsoft.com/library/9ee1c0c0-b864-f0c3-f0cb-4dd4f1870dfa%28Office.15%29.aspx) рекомендуется использовать для подписки на людей и контент. Тем не менее объект [PeopleManager](http://msdn.microsoft.com/library/985fd2df-0e31-6ece-b846-ba2ccb156d00%28Office.15%29.aspx) содержит дополнительные функции для следующих пользователей, таких как метод [amIFollowedBy](http://msdn.microsoft.com/library/3641c469-0063-054d-355d-e56697cb08ae%28Office.15%29.aspx) и методы, которые получить следующие состояния другим пользователям.
  
    
    


## <a name="prerequisites-for-setting-up-your-development-environment-to-work-with-following-people-features-by-using-the-sharepoint-javascript-object-model"></a>Необходимые условия для настройки среды разработки для работы с функциями следующих пользователей с помощью объектной модели SharePoint JavaScript
<a name="bk_Prereqs"> </a>

Чтобы создать решение фермы, которая использует объектную модель JavaScript для работы с функциями следующие сотрудники, то необходимо:
  
    
    

- SharePoint с личного сайта настроены и профили пользователей и личные сайты, созданные для текущего пользователя и конечного пользователя
    
  
- Visual Studio 2012
    
  
- Инструменты разработчика Office для Visual Studio 2012
    
  
- **Полный** доступ к приложению-службе профилей пользователей для пользователя, вошедшего в систему
    
  
- Разрешения локального администратора для пользователя, вошедшего в систему
    
  

## <a name="create-a-farm-solution-and-application-page-in-visual-studio-2012"></a>Создайте страницу фермы решения и приложения в Visual Studio 2012
<a name="bk_CreateSolution"> </a>


1. Запустите Visual Studio от имени администратора и выберите **файл**, **Создать**, **проект**.
    
  
2. В диалоговом окне **Новый проект** выберите **.NET Framework 4.5** из раскрывающегося списка в верхней части окна.
    
  
3. В списке **Шаблоны** разверните узел **Office/SharePoint**, щелкните **Решения SharePoint**и затем выберите шаблон **SharePoint — пустой проект** .
    
  
4. Назовите проект FollowPeopleJSOMи затем нажмите кнопку **ОК**.
    
  
5. В диалоговом окне **Мастер настройки SharePoint** выберите **Развернуть как решение фермы** и затем нажмите кнопку **Готово**.
    
  
6. В **Обозревателе решений** откройте контекстное меню для проекта **FollowPeopleJSOM** и добавьте SharePoint "Макеты" сопоставленная папка.
    
  
7. В папке **Layouts** откройте контекстное меню для папки **FollowPeopleJSOM** и добавьте новую страницу приложения SharePoint с именемFollowPeople.aspx.
    
    > [!NOTE]
    > [!Примечание] Примеры кода в этой статье определение пользовательского кода в разметке страницы, но не используйте класс фонового кода, Visual Studio создает для этой страницы. 

8. Откройте контекстное меню для страницы FollowPeople.aspx и нажмите кнопку **Set as Startup Item**.
    
  
9. В разметке файла FollowPeople.aspx вставьте следующий код в тегах **asp:Content** «Главная». Этот код определяет элементы управления и ссылки на сценарии.
    
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

    > [!NOTE]
    > The "Get followers and followed people" example doesn't use the button control or the form digest control, which is only required for operations that update server content. A form digest generates a message digest used for security validation. 

10. Замените комментарий между тегами **script** с пример кода из одного из следующих сценариев:
    
  -  [Запуск или остановка отслеживаемые пользователи](how-to-follow-people-by-using-the-javascript-object-model-in-sharepoint.md#bk_FollowPeople)  
  -  [Получите последователи и пользователей](how-to-follow-people-by-using-the-javascript-object-model-in-sharepoint.md#bk_GetFollowers)
    
11. Тестирование решения, в строке меню выберите **Отладка**, **Начать отладку**.
    
  

## <a name="code-example-start-or-stop-following-people-by-using-the-sharepoint-javascript-object-model"></a>Пример кода: запустить или остановить следующие людей с помощью объектной модели SharePoint JavaScript
<a name="bk_FollowPeople"> </a>

В следующем примере кода делает текущего пользователя запустить следующие или остановить после конечного пользователя. В нем показано, как:
  
    
    

- Проверьте, является ли текущий пользователь выполнив конечного пользователя с помощью метода  [isFollowed](http://msdn.microsoft.com/library/2c1f62e6-fb75-ad4d-c081-36408b418c21%28Office.15%29.aspx) .
    
  
- Получение числа пользователей, которые текущий пользователь подписан с помощью метода  [getFollowedCount](http://msdn.microsoft.com/library/97b53b4f-481a-cf41-1854-8f3ff860b2bb%28Office.15%29.aspx) .
    
  
- Запустите следующие конечного пользователя с помощью метода  [выполните](http://msdn.microsoft.com/library/40d14320-27ba-2941-b0e2-be3b5a407c89%28Office.15%29.aspx) .
    
  
- Отменить подписку конечного пользователя с помощью метода  [stopFollowing](http://msdn.microsoft.com/library/65b0e9be-dc5e-09fb-c57f-7a933de09a4c%28Office.15%29.aspx) .
    
  

> [!NOTE]
>  [!Примечание] Вставьте следующий код в тегах **script**, которые добавлены в процедуре [создать решение фермы и страницы приложения](how-to-follow-people-by-using-the-javascript-object-model-in-sharepoint.md#bk_CreateSolution) . Измените значение заполнитель для переменной **targetUser** до выполнения этого кода.
  
    
    


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


## <a name="code-example-get-followers-and-followed-people-by-using-the-sharepoint-javascript-object-model"></a>Пример кода: получение последователи и отслеживаемого людей с помощью объектной модели SharePoint JavaScript
<a name="bk_GetFollowers"> </a>

В следующем примере кода получает людей, текущий пользователь отслеживание и получает пользователей, которые следуют текущего пользователя. В нем показано, как:
  
    
    

- Получите пользователей, которые текущий пользователь подписан с помощью метода  [getFollowed](http://msdn.microsoft.com/library/432a7cec-6add-fdb1-a79f-a93414ee8cd3%28Office.15%29.aspx) .
    
  
- Получите пользователей, которые отслеживаются текущего пользователя с помощью метода  [getFollowers](http://msdn.microsoft.com/library/ae4a944b-c043-05fb-c74b-101d2ce4a813%28Office.15%29.aspx) , передав **1** для представления типов actor **User**.
    
  
- Выполните итерацию по группам людей или get отображения имени, личного сайта URI пользователя, а также рисунок URI.
    
> [!NOTE]
> [!Примечание] Вставьте следующий код в тегах **script**, которые добавлены в процедуре [создать решение фермы и страницы приложения](how-to-follow-people-by-using-the-javascript-object-model-in-sharepoint.md#bk_CreateSolution) .
  
    
    


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


## <a name="see-also"></a>См. также
<a name="bk_AdditionalResources"> </a>


-  [Подписка на людей в SharePoint](follow-people-in-sharepoint.md)
    
  
-  [Как подписываться на пользователей, используя клиентскую объектную модель .NET в SharePoint](how-to-follow-people-by-using-the-net-client-object-model-in-sharepoint.md)
    
  

