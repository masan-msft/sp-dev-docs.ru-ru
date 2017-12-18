---
title: "Получение свойств профилей пользователей с помощью объектной модели JavaScript в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: c6e1ca38-134f-428a-8d21-b8b2615b161b
ms.openlocfilehash: 364e948834758c1fda52afebd2b1648d0e726b0b
ms.sourcegitcommit: f6ea922341c38e700d0697961f8df9a454a03cba
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/15/2017
---
# <a name="retrieve-user-profile-properties-by-using-the-javascript-object-model-in-sharepoint"></a><span data-ttu-id="6450e-102">Получение свойств профилей пользователей с помощью объектной модели JavaScript в SharePoint</span><span class="sxs-lookup"><span data-stu-id="6450e-102">How to: Retrieve user profile properties by using the JavaScript object model in SharePoint</span></span>

<span data-ttu-id="6450e-103">Узнайте, как программно восстановить свойства и профиль пользователя с помощью объектной модели JavaScript для SharePoint.</span><span class="sxs-lookup"><span data-stu-id="6450e-103">Learn how to retrieve user properties and user profile properties programmatically by using the SharePoint JavaScript object model.</span></span>

## <a name="what-are-user-properties-and-user-profile-properties-in-sharepoint"></a><span data-ttu-id="6450e-104">Что такое свойства пользователей и их профилей в SharePoint?</span><span class="sxs-lookup"><span data-stu-id="6450e-104">What are user properties and user profile properties in SharePoint?</span></span>
<span data-ttu-id="6450e-105"><a name="bkmk_WhatIs"> </a></span><span class="sxs-lookup"><span data-stu-id="6450e-105"><a name="bkmk_WhatIs"> </a></span></span>

<span data-ttu-id="6450e-p101">Свойства пользователей и их профилей предоставляют сведения о пользователях SharePoint, например отображаемое имя, адрес электронной почты, должность, а также другие рабочие и личные сведения. В клиентских интерфейсах API доступ к этим свойствам можно получить с помощью объекта  [PersonProperties](http://msdn.microsoft.com/library/0274d97f-b697-f436-2aaf-f5bcf9b70df8%28Office.15%29.aspx) и его свойства [userProfileProperties](http://msdn.microsoft.com/library/56516666-7425-4993-222f-f745cf266e89%28Office.15%29.aspx). Свойство  [userProfileProperties](http://msdn.microsoft.com/library/56516666-7425-4993-222f-f745cf266e89%28Office.15%29.aspx) содержит все свойства профиля пользователя, но объект [PersonProperties](http://msdn.microsoft.com/library/0274d97f-b697-f436-2aaf-f5bcf9b70df8%28Office.15%29.aspx) содержит часто используемые свойства (например, [accountName](http://msdn.microsoft.com/library/ad1551bf-dad8-d54e-880a-8a4388fad44e%28Office.15%29.aspx),  [displayName](http://msdn.microsoft.com/library/ffc35ed6-5f3e-c86d-6931-97ff9d825a8b%28Office.15%29.aspx) и [email](http://msdn.microsoft.com/library/74302f73-aaf6-920b-0605-812b0dbf4568%28Office.15%29.aspx)), к которым легче получить доступ.</span><span class="sxs-lookup"><span data-stu-id="6450e-p101">User properties and user profile properties provide information about SharePoint users, such as display name, email, title, and other business and personal information. In client-side APIs, you access these properties from the  [PersonProperties](http://msdn.microsoft.com/library/0274d97f-b697-f436-2aaf-f5bcf9b70df8%28Office.15%29.aspx) object and its [userProfileProperties](http://msdn.microsoft.com/library/56516666-7425-4993-222f-f745cf266e89%28Office.15%29.aspx) property. The [userProfileProperties](http://msdn.microsoft.com/library/56516666-7425-4993-222f-f745cf266e89%28Office.15%29.aspx) property contains all user profile properties, but the [PersonProperties](http://msdn.microsoft.com/library/0274d97f-b697-f436-2aaf-f5bcf9b70df8%28Office.15%29.aspx) object contains commonly used properties (such as [accountName](http://msdn.microsoft.com/library/ad1551bf-dad8-d54e-880a-8a4388fad44e%28Office.15%29.aspx),  [displayName](http://msdn.microsoft.com/library/ffc35ed6-5f3e-c86d-6931-97ff9d825a8b%28Office.15%29.aspx), and  [email](http://msdn.microsoft.com/library/74302f73-aaf6-920b-0605-812b0dbf4568%28Office.15%29.aspx)) that are easier to access.</span></span>
  
    
    
<span data-ttu-id="6450e-109">Объект  [PeopleManager](http://msdn.microsoft.com/library/985fd2df-0e31-6ece-b846-ba2ccb156d00%28Office.15%29.aspx) включает следующие методы, которые можно использовать для получения свойств пользователей и их профилей с помощью объектной модели JavaScript:</span><span class="sxs-lookup"><span data-stu-id="6450e-109">The  [PeopleManager](http://msdn.microsoft.com/library/985fd2df-0e31-6ece-b846-ba2ccb156d00%28Office.15%29.aspx) object includes the following methods that you can use to retrieve user properties and user profile properties by using the JavaScript object model:</span></span>
  
    
    

- <span data-ttu-id="6450e-110">Методы  [getMyProperties](http://msdn.microsoft.com/library/be001abc-a431-8d48-8e6f-161251aa19ac%28Office.15%29.aspx) и [getPropertiesFor](http://msdn.microsoft.com/library/097464db-2630-4c7a-fd0c-0f333680b5a4%28Office.15%29.aspx) возвращают объект [PersonProperties](http://msdn.microsoft.com/library/0274d97f-b697-f436-2aaf-f5bcf9b70df8%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="6450e-110">The  [getMyProperties](http://msdn.microsoft.com/library/be001abc-a431-8d48-8e6f-161251aa19ac%28Office.15%29.aspx) method and the [getPropertiesFor](http://msdn.microsoft.com/library/097464db-2630-4c7a-fd0c-0f333680b5a4%28Office.15%29.aspx) method return a [PersonProperties](http://msdn.microsoft.com/library/0274d97f-b697-f436-2aaf-f5bcf9b70df8%28Office.15%29.aspx) object.</span></span>
    
  
- <span data-ttu-id="6450e-111">Методы  [getUserProfilePropertiesFor](http://msdn.microsoft.com/library/8674e96f-d320-4a50-1580-9a4568842ee5%28Office.15%29.aspx) и [getUserProfilePropertyFor](http://msdn.microsoft.com/library/da048bfa-54c6-8216-e8ef-09bd84f68d8d%28Office.15%29.aspx) возвращают значения свойств профиля пользователя, которые можно указать.</span><span class="sxs-lookup"><span data-stu-id="6450e-111">The  [getUserProfilePropertiesFor](http://msdn.microsoft.com/library/8674e96f-d320-4a50-1580-9a4568842ee5%28Office.15%29.aspx) method and the [getUserProfilePropertyFor](http://msdn.microsoft.com/library/da048bfa-54c6-8216-e8ef-09bd84f68d8d%28Office.15%29.aspx) method return the values of the user profile properties that you specify.</span></span>
    
  
<span data-ttu-id="6450e-p102">Свойства профиля пользователя из клиентских интерфейсов API доступны только для чтения (за исключением изображения профиля, которое можно изменить с помощью метода  [PeopleManager.setMyProfilePicture](http://msdn.microsoft.com/library/a4f8d745-f211-e750-4fd0-047091804683%28Office.15%29.aspx)). Чтобы изменить другие свойства профиля пользователя, необходимо использовать серверную объектную модель. Дополнительные сведения о работе с профилями пользователей см. в статье  [Работа с профилями пользователей в SharePoint](work-with-user-profiles-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="6450e-p102">User profile properties from client APIs are read-only (except the profile picture, which you can change by using the  [PeopleManager.setMyProfilePicture](http://msdn.microsoft.com/library/a4f8d745-f211-e750-4fd0-047091804683%28Office.15%29.aspx) method). If you want to change other user profile properties, you must use the server object model. For more information about working with user profiles, see [Work with user profiles in SharePoint](work-with-user-profiles-in-sharepoint.md).</span></span>
  
    
    

> <span data-ttu-id="6450e-115">**Примечание.** Клиентский объект [UserProfile](http://msdn.microsoft.com/library/f8c4a219-fbaa-2e50-1bd5-fdc80051b33d%28Office.15%29.aspx) содержит не все пользовательские свойства, которыми обладает его серверная версия.</span><span class="sxs-lookup"><span data-stu-id="6450e-115">**Note:** The client-side  [UserProfile](http://msdn.microsoft.com/library/f8c4a219-fbaa-2e50-1bd5-fdc80051b33d%28Office.15%29.aspx) object doesn't contain all of the user properties as the server-side version.</span></span> <span data-ttu-id="6450e-116">Однако клиентская версия предоставляет методы для создания личного сайта для текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="6450e-116">However, the client-side version does provide the methods for creating a personal site for the current user.</span></span> <span data-ttu-id="6450e-117">Чтобы получить этот объект, используйте метод [ProfileLoader.getUserProfile](http://msdn.microsoft.com/library/8e30e811-5da1-b6d0-a8b5-befea9b22496%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="6450e-117">To retrieve it, use the [ProfileLoader.getUserProfile](http://msdn.microsoft.com/library/8e30e811-5da1-b6d0-a8b5-befea9b22496%28Office.15%29.aspx) method.</span></span>
  
    
    


## <a name="prerequisites-for-setting-up-your-development-environment-to-retrieve-user-properties-by-using-the-sharepoint-javascript-object-model"></a><span data-ttu-id="6450e-118">Необходимые условия для настройки среды разработки на получение свойств пользователя с помощью объектной модели JavaScript в SharePoint</span><span class="sxs-lookup"><span data-stu-id="6450e-118">Prerequisites for setting up your development environment to retrieve user properties by using the SharePoint JavaScript object model</span></span>
<span data-ttu-id="6450e-119"><a name="bk_Prereqs"> </a></span><span class="sxs-lookup"><span data-stu-id="6450e-119"><a name="bk_Prereqs"> </a></span></span>

<span data-ttu-id="6450e-120">Чтобы создать страницу приложения, которая использует объектную модель JavaScript для получения свойств пользователей, вам потребуются:</span><span class="sxs-lookup"><span data-stu-id="6450e-120">To create an application page that uses the JavaScript object model to retrieve user properties, you'll need:</span></span>
  
    
    

- <span data-ttu-id="6450e-121">SharePoint с профилями для текущего пользователя и целевого пользователя;</span><span class="sxs-lookup"><span data-stu-id="6450e-121">SharePoint with profiles created for the current user and a target user</span></span>
    
  
- <span data-ttu-id="6450e-122">Visual Studio 2012;</span><span class="sxs-lookup"><span data-stu-id="6450e-122">Visual Studio 2012</span></span>
    
  
- <span data-ttu-id="6450e-123">Инструменты разработчика Office для Visual Studio 2013;</span><span class="sxs-lookup"><span data-stu-id="6450e-123">Office Developer Tools for Visual Studio 2013</span></span>
    
  
- <span data-ttu-id="6450e-124">разрешения уровня **Полный доступ** для подключения к приложению-службе профиля текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="6450e-124">**Full Control** connection permissions to access the User Profile service application for the current user</span></span>
    
  

## <a name="create-the-application-page-in-visual-studio-2012"></a><span data-ttu-id="6450e-125">Создание страницы приложения в Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="6450e-125">Create the application page in Visual Studio 2012</span></span>
<span data-ttu-id="6450e-126"><a name="bk_CreateAppPage"> </a></span><span class="sxs-lookup"><span data-stu-id="6450e-126"><a name="bk_CreateAppPage"> </a></span></span>


1. <span data-ttu-id="6450e-127">На сервере под управлением SharePoint откройте Visual Studio и выберите команды **Файл**, **Создать**, **Проект**.</span><span class="sxs-lookup"><span data-stu-id="6450e-127">On the server running SharePoint, open Visual Studio and choose **File**, **New**, **Project**.</span></span>
    
  
2. <span data-ttu-id="6450e-128">В раскрывающемся списке в верхней части диалогового окна **Новый проект** выберите пункт **.NET Framework 4.5**.</span><span class="sxs-lookup"><span data-stu-id="6450e-128">In the **New Project** dialog box, choose **.NET Framework 4.5** from the drop-down list at the top of the dialog box.</span></span>
    
  
3. <span data-ttu-id="6450e-129">В списке **Шаблоны** разверните узел **Office/SharePoint**, выберите категорию **Решения SharePoint**, а затем  шаблон **Проект SharePoint**.</span><span class="sxs-lookup"><span data-stu-id="6450e-129">In the **Templates** list, expand **Office/SharePoint**, choose the **SharePoint Solutions** category, and then choose the **SharePoint Project** template.</span></span>
    
  
4. <span data-ttu-id="6450e-130">Назовите проект UserProfilesJSOM и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="6450e-130">Name the project UserProfilesJSOM, and then choose the **OK** button.</span></span>
    
  
5. <span data-ttu-id="6450e-131">В диалоговом окне **Мастер настройки SharePoint** введите URL-адрес целевого сайта SharePoint, выберите **Развернуть как решение фермы** и нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="6450e-131">In the **SharePoint Customization Wizard** dialog box, enter the URL to your target SharePoint site, choose **Deploy as a farm solution**, and then choose the **Finish** button.</span></span>
    
  
6. <span data-ttu-id="6450e-132">В **диспетчере решений** откройте контекстное меню для проектаUserProfilesJSOM и добавьте сопоставленную папку Layouts для SharePoint.</span><span class="sxs-lookup"><span data-stu-id="6450e-132">In **Solution Explorer**, open the shortcut menu for the UserProfilesJSOM project, and then add a SharePoint "Layouts" mapped folder.</span></span>
    
  
7. <span data-ttu-id="6450e-133">В папке **Layouts** откройте контекстное меню папки UserProfilesJSOM и добавьте новую страницу приложения SharePoint под названием UserProfiles.aspx.</span><span class="sxs-lookup"><span data-stu-id="6450e-133">In the **Layouts** folder, open the shortcut menu for theUserProfilesJSOM folder, and then add a new SharePoint application page namedUserProfiles.aspx.</span></span>
    
   > <span data-ttu-id="6450e-134">Примечание. Примеры кода в этой статье определяют пользовательский код в коде разметки страницы, но не используют файл классов кода программной части, который Visual Studio создает для страницы.</span><span class="sxs-lookup"><span data-stu-id="6450e-134">Note: The code examples in this article define custom code in the page markup but do not use the code-behind class file that Visual Studio creates for the page.</span></span> 

8. <span data-ttu-id="6450e-135">Откройте контекстное меню страницы UserProfiles.aspx и выберите пункт **Назначить автозапускаемым элементом**.</span><span class="sxs-lookup"><span data-stu-id="6450e-135">Open the shortcut menu for the UserProfiles.aspx page, and then choose **Set as Startup Item**.</span></span>
    
  
9. <span data-ttu-id="6450e-p104">В разметке страницы UserProfiles.aspx вставьте приведенный ниже код в теги Main **asp:Content**. Этот код создает элемент управления **span**, который отображает результаты запроса, элементы управления **SharePoint:ScriptLink**, которые ссылаются на файлы библиотеки классов JavaScript в SharePoint, и теги **script** для пользовательской логики.</span><span class="sxs-lookup"><span data-stu-id="6450e-p104">In the markup for the UserProfiles.aspx page, paste the following code inside the "Main" **asp:Content** tags. This code adds a **span** control that displays the results of the query, **SharePoint:ScriptLink** controls that reference SharePoint JavaScript class library files, and **script** tags to contain your custom logic.</span></span>
    
```HTML
<span id="results"></span><br />
<SharePoint:ScriptLink ID="ScriptLink1" name="SP.js" runat="server"
    ondemand="false" localizable="false" loadafterui="true" />
<SharePoint:ScriptLink ID="ScriptLink2" name="SP.UserProfiles.js" runat="server"
    ondemand="false" localizable="false" loadafterui="true" />
<script type="text/javascript">
    // Replace this comment with the code for your scenario.
</script>
```

10. <span data-ttu-id="6450e-138">Чтобы добавить логику для получения свойств профиля пользователя, замените комментарий между тегами **script** примером кода из одного из следующих сценариев:</span><span class="sxs-lookup"><span data-stu-id="6450e-138">To add logic to retrieve user profile properties, replace the comment between the **script** tags with the code example from one of the following scenarios:</span></span>
    
  -  [<span data-ttu-id="6450e-139">Получение свойств профиля пользователя из объекта PersonProperties и его свойства userProfileProperties</span><span class="sxs-lookup"><span data-stu-id="6450e-139">Retrieve user profile properties from the PersonProperties object and its userProfileProperties property</span></span>](how-to-retrieve-user-profile-properties-by-using-the-javascript-object-model-in.md#bk_examplePersonPropsObj)  
  -  [<span data-ttu-id="6450e-140">Получение набора свойств профиля пользователя с помощью метода getUserProfilePropertiesFor</span><span class="sxs-lookup"><span data-stu-id="6450e-140">Retrieve a set of user profile properties by using the getUserProfilePropertiesFor method</span></span>](how-to-retrieve-user-profile-properties-by-using-the-javascript-object-model-in.md#bk_exampleGetUPMethod)
    
  
11. <span data-ttu-id="6450e-p105">Чтобы протестировать страницу приложения, в панели меню выберите команды **Отладка**, **Начать отладку**. Если вам будет предложено изменить файл web.config, нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="6450e-p105">To test the application page, on the menu bar, choose **Debug**, **Start Debugging**. If you're prompted to modify the web.config file, choose the **OK** button.</span></span>
    
  

## <a name="code-example-retrieving-user-profile-properties-from-the-personproperties-object-and-its-userprofileproperties-property-in-the-sharepoint-javascript-object-model"></a><span data-ttu-id="6450e-143">Пример кода. Получение свойств профиля пользователя из объекта PersonProperties и его свойства userProfileProperties в объектной модели SharePoint JavaScript</span><span class="sxs-lookup"><span data-stu-id="6450e-143">Code example: Retrieving user profile properties from the PersonProperties object and its userProfileProperties property in the SharePoint JavaScript object model</span></span>
<span data-ttu-id="6450e-144"><a name="bk_examplePersonPropsObj"> </a></span><span class="sxs-lookup"><span data-stu-id="6450e-144"><a name="bk_examplePersonPropsObj"> </a></span></span>

<span data-ttu-id="6450e-p106">В приведенном ниже примере кода показано, как получить свойства профиля целевого пользователя с помощью запроса к объекту  [PersonProperties](http://msdn.microsoft.com/library/0274d97f-b697-f436-2aaf-f5bcf9b70df8%28Office.15%29.aspx) и его свойству [userProfileProperties](http://msdn.microsoft.com/library/56516666-7425-4993-222f-f745cf266e89%28Office.15%29.aspx). Он показывает, как:</span><span class="sxs-lookup"><span data-stu-id="6450e-p106">The following code example shows how to get user profile properties for a target user by querying the  [PersonProperties](http://msdn.microsoft.com/library/0274d97f-b697-f436-2aaf-f5bcf9b70df8%28Office.15%29.aspx) object and its [userProfileProperties](http://msdn.microsoft.com/library/56516666-7425-4993-222f-f745cf266e89%28Office.15%29.aspx) property. It shows how to:</span></span>
  
    
    

- <span data-ttu-id="6450e-p107">Получить объект  [PersonProperties](http://msdn.microsoft.com/library/0274d97f-b697-f436-2aaf-f5bcf9b70df8%28Office.15%29.aspx), который представляет целевого пользователя, с помощью метода  [getPropertiesFor](http://msdn.microsoft.com/library/097464db-2630-4c7a-fd0c-0f333680b5a4%28Office.15%29.aspx). Чтобы получить объект  [PersonProperties](http://msdn.microsoft.com/library/0274d97f-b697-f436-2aaf-f5bcf9b70df8%28Office.15%29.aspx) для текущего пользователя, используйте метод [getMyProperties](http://msdn.microsoft.com/library/be001abc-a431-8d48-8e6f-161251aa19ac%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="6450e-p107">Get the  [PersonProperties](http://msdn.microsoft.com/library/0274d97f-b697-f436-2aaf-f5bcf9b70df8%28Office.15%29.aspx) object that represents the target user by using the [getPropertiesFor](http://msdn.microsoft.com/library/097464db-2630-4c7a-fd0c-0f333680b5a4%28Office.15%29.aspx) method. (To get the [PersonProperties](http://msdn.microsoft.com/library/0274d97f-b697-f436-2aaf-f5bcf9b70df8%28Office.15%29.aspx) object for the current user, use the [getMyProperties](http://msdn.microsoft.com/library/be001abc-a431-8d48-8e6f-161251aa19ac%28Office.15%29.aspx) method.)</span></span>
    
  
- <span data-ttu-id="6450e-p108">Получить свойство непосредственно из объекта  [PersonProperties](http://msdn.microsoft.com/library/0274d97f-b697-f436-2aaf-f5bcf9b70df8%28Office.15%29.aspx). Этот пример получает свойство  [displayName](http://msdn.microsoft.com/library/ffc35ed6-5f3e-c86d-6931-97ff9d825a8b%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="6450e-p108">Get a property directly from the  [PersonProperties](http://msdn.microsoft.com/library/0274d97f-b697-f436-2aaf-f5bcf9b70df8%28Office.15%29.aspx) object. This example gets the [displayName](http://msdn.microsoft.com/library/ffc35ed6-5f3e-c86d-6931-97ff9d825a8b%28Office.15%29.aspx) property.</span></span>
    
  
- <span data-ttu-id="6450e-p109">Получить свойство из свойства [userProfileProperties](http://msdn.microsoft.com/library/56516666-7425-4993-222f-f745cf266e89%28Office.15%29.aspx) объекта [PersonProperties](http://msdn.microsoft.com/library/0274d97f-b697-f436-2aaf-f5bcf9b70df8%28Office.15%29.aspx). В этом примере показано, как получить свойство **Department**.</span><span class="sxs-lookup"><span data-stu-id="6450e-p109">Get a property from the  [userProfileProperties](http://msdn.microsoft.com/library/56516666-7425-4993-222f-f745cf266e89%28Office.15%29.aspx) property of the [PersonProperties](http://msdn.microsoft.com/library/0274d97f-b697-f436-2aaf-f5bcf9b70df8%28Office.15%29.aspx) object. This example gets the **Department** property.</span></span>
    
  

> <span data-ttu-id="6450e-153">**Примечание.** Вставьте приведенный ниже код между тегами **script**, добавленными в файл UserProfiles.aspx в ходе процедуры [Создание страницы приложения](how-to-retrieve-user-profile-properties-by-using-the-javascript-object-model-in.md#bk_CreateAppPage).</span><span class="sxs-lookup"><span data-stu-id="6450e-153">**Note:** Paste the following code between the **script** tags that you added to the UserProfiles.aspx file in the [Create the application page](how-to-retrieve-user-profile-properties-by-using-the-javascript-object-model-in.md#bk_CreateAppPage) procedure.</span></span> <span data-ttu-id="6450e-154">Замените значение заполнителя `domainName\\userName`, прежде чем запускать код.</span><span class="sxs-lookup"><span data-stu-id="6450e-154">Replace the `domainName\\userName` placeholder value before you run the code.</span></span> <span data-ttu-id="6450e-155">В этом примере кода не используется файл классов кода программной части.</span><span class="sxs-lookup"><span data-stu-id="6450e-155">(This code example does not use the code-behind class file.)</span></span>
  
    
    


```

var personProperties;

// Ensure that the SP.UserProfiles.js file is loaded before the custom code runs.
SP.SOD.executeOrDelayUntilScriptLoaded(getUserProperties, 'SP.UserProfiles.js');

function getUserProperties() {

    // Replace the placeholder value with the target user's credentials.
    var targetUser = "domainName\\userName";

    // Get the current client context and PeopleManager instance.
    var clientContext = new SP.ClientContext.get_current();
    var peopleManager = new SP.UserProfiles.PeopleManager(clientContext);

    // Get user properties for the target user.
    // To get the PersonProperties object for the current user, use the
    // getMyProperties method.
    personProperties = peopleManager.getPropertiesFor(targetUser);

    // Load the PersonProperties object and send the request.
    clientContext.load(personProperties);
    clientContext.executeQueryAsync(onRequestSuccess, onRequestFail);
}

// This function runs if the executeQueryAsync call succeeds.
function onRequestSuccess() {

    // Get a property directly from the PersonProperties object.
    var messageText = " \\"DisplayName\\" property is "
        + personProperties.get_displayName();

    // Get a property from the UserProfileProperties property.
    messageText += "<br />\\"Department\\" property is "
        + personProperties.get_userProfileProperties()['Department'];
    $get("results").innerHTML = messageText;
}

// This function runs if the executeQueryAsync call fails.
function onRequestFail(sender, args) {
    $get("results").innerHTML = "Error: " + args.get_message();
}
```


## <a name="code-example-retrieving-a-set-of-user-profile-properties-by-using-the-getuserprofilepropertiesfor-method-in-the-sharepoint-javascript-object-model"></a><span data-ttu-id="6450e-156">Пример кода. Получение набора свойств профиля пользователя с помощью метода getUserProfilePropertiesFor в объектной модели JavaScript SharePoint</span><span class="sxs-lookup"><span data-stu-id="6450e-156">Code example: Retrieving a set of user profile properties by using the getUserProfilePropertiesFor method in the SharePoint JavaScript object model</span></span>
<span data-ttu-id="6450e-157"><a name="bk_exampleGetUPMethod"> </a></span><span class="sxs-lookup"><span data-stu-id="6450e-157"><a name="bk_exampleGetUPMethod"> </a></span></span>

<span data-ttu-id="6450e-p111">Приведенный ниже пример кода получает значения указанного набора свойств профиля целевого пользователя с помощью метод  [getUserProfilePropertiesFor](http://msdn.microsoft.com/library/8674e96f-d320-4a50-1580-9a4568842ee5%28Office.15%29.aspx). Он показывает, как:</span><span class="sxs-lookup"><span data-stu-id="6450e-p111">The following code example retrieves the values for a specified set of user profile properties for a target user by using the  [getUserProfilePropertiesFor](http://msdn.microsoft.com/library/8674e96f-d320-4a50-1580-9a4568842ee5%28Office.15%29.aspx) method. It shows how to:</span></span>
  
    
    

- <span data-ttu-id="6450e-p112">Создать объект  [UserProfilePropertiesForUser](http://msdn.microsoft.com/library/97bc94ec-62c8-dc38-d204-c5ad9ee8faee%28Office.15%29.aspx), который задает целевого пользователя и получаемые свойства профиля. Этот пример получает свойства **PreferredName** и **Department**.</span><span class="sxs-lookup"><span data-stu-id="6450e-p112">Create a  [UserProfilePropertiesForUser](http://msdn.microsoft.com/library/97bc94ec-62c8-dc38-d204-c5ad9ee8faee%28Office.15%29.aspx) object that specifies the target user and the user profile properties to retrieve. This example gets the **PreferredName** property and the **Department** property.</span></span>
    
  
- <span data-ttu-id="6450e-p113">Получить значения указанных свойств с помощью метода [getUserProfilePropertiesFor](http://msdn.microsoft.com/library/8674e96f-d320-4a50-1580-9a4568842ee5%28Office.15%29.aspx), передав их в объект [UserProfilePropertiesForUser](http://msdn.microsoft.com/library/97bc94ec-62c8-dc38-d204-c5ad9ee8faee%28Office.15%29.aspx). Чтобы получить значение только одного свойства профиля пользователя, используйте метод [getUserProfilePropertyFor](http://msdn.microsoft.com/library/da048bfa-54c6-8216-e8ef-09bd84f68d8d%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="6450e-p113">Get the values of the specified properties by using the  [getUserProfilePropertiesFor](http://msdn.microsoft.com/library/8674e96f-d320-4a50-1580-9a4568842ee5%28Office.15%29.aspx) method and passing in the [UserProfilePropertiesForUser](http://msdn.microsoft.com/library/97bc94ec-62c8-dc38-d204-c5ad9ee8faee%28Office.15%29.aspx) object. (To retrieve the value for only one user profile property, use the [getUserProfilePropertyFor](http://msdn.microsoft.com/library/da048bfa-54c6-8216-e8ef-09bd84f68d8d%28Office.15%29.aspx) method.)</span></span>
    
  
- <span data-ttu-id="6450e-164">Получить значения из возвращаемого массива значений свойств.</span><span class="sxs-lookup"><span data-stu-id="6450e-164">Get the values from the returned array of property values.</span></span>
    
  

> <span data-ttu-id="6450e-165">**Примечание.** Вставьте приведенный ниже код между тегами **script**, добавленными в файл UserProfiles.aspx в ходе процедуры [Создание страницы приложения](how-to-retrieve-user-profile-properties-by-using-the-javascript-object-model-in.md#bk_CreateAppPage).</span><span class="sxs-lookup"><span data-stu-id="6450e-165">**Note:** Paste the following code between the **script** tags that you added to the UserProfiles.aspx file in the [Create the application page](how-to-retrieve-user-profile-properties-by-using-the-javascript-object-model-in.md#bk_CreateAppPage) procedure.</span></span> <span data-ttu-id="6450e-166">Замените значение заполнителя `domainName\\\\userName`, прежде чем запускать код.</span><span class="sxs-lookup"><span data-stu-id="6450e-166">Replace the `domainName\\\\userName` placeholder value before you run the code.</span></span> <span data-ttu-id="6450e-167">В этом примере кода не используется файл классов кода программной части.</span><span class="sxs-lookup"><span data-stu-id="6450e-167">(This code example does not use the code-behind class file.)</span></span>
  
    
    


```

var userProfileProperties;

// Ensure that the SP.UserProfiles.js file is loaded before the custom code runs.
SP.SOD.executeOrDelayUntilScriptLoaded(getUserProperties, 'SP.UserProfiles.js');

function getUserProperties() {

    // Replace the placeholder value with the target user's credentials.
    var targetUser = "domainName\\\\userName";

    // Get the current client context and PeopleManager instance.
    var clientContext = new SP.ClientContext.get_current();
    var peopleManager = new SP.UserProfiles.PeopleManager(clientContext);

    // Specify the properties to retrieve and target user for the 
    // UserProfilePropertiesForUser object.
    var profilePropertyNames = ["PreferredName", "Department"];
    var userProfilePropertiesForUser = 
        new SP.UserProfiles.UserProfilePropertiesForUser(
            clientContext,
            targetUser,
            profilePropertyNames);

    // Get user profile properties for the target user.
    // To get the value for only one user profile property, use the
    // getUserProfilePropertyFor method.
    userProfileProperties = peopleManager.getUserProfilePropertiesFor(
        userProfilePropertiesForUser);

    // Load the UserProfilePropertiesForUser object and send the request.
    clientContext.load(userProfilePropertiesForUser);
    clientContext.executeQueryAsync(onRequestSuccess, onRequestFail);
}

// This function runs if the executeQueryAsync call succeeds.
function onRequestSuccess() {
    var messageText = "\\"PreferredName\\" property is " 
        + userProfileProperties[0];
    messageText += "<br />\\"Department\\" property is " 
        + userProfileProperties[1];
    $get("results").innerHTML = messageText;
}

// This function runs if the executeQueryAsync call fails.
function onRequestFail(sender, args) {
    $get("results").innerHTML = "Error: " + args.get_message();
}
```


## <a name="additional-resources"></a><span data-ttu-id="6450e-168">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="6450e-168">Additional resources</span></span>
<span data-ttu-id="6450e-169"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="6450e-169"><a name="bk_addresources"> </a></span></span>


-  [<span data-ttu-id="6450e-170">Работа с профилями пользователей в SharePoint</span><span class="sxs-lookup"><span data-stu-id="6450e-170">Work with user profiles in SharePoint</span></span>](work-with-user-profiles-in-sharepoint.md)
    
  
-  [<span data-ttu-id="6450e-171">Как: получение свойств профиля пользователя с помощью клиентской объектной модели .NET в SharePoint</span><span class="sxs-lookup"><span data-stu-id="6450e-171">How to: Retrieve user profile properties by using the .NET client object model in SharePoint</span></span>](how-to-retrieve-user-profile-properties-by-using-the-net-client-object-model-in.md)
    
  
-  [<span data-ttu-id="6450e-172">Инструкции. Работа с профилями пользователей и организации с использованием объектной модели сервера в SharePoint</span><span class="sxs-lookup"><span data-stu-id="6450e-172">How to: Work with user profiles and organization profiles by using the server object model in SharePoint</span></span>](how-to-work-with-user-profiles-and-organization-profiles-by-using-the-server-obj.md)
    
  
-  [<span data-ttu-id="6450e-173">SP.UserProfiles Пространства имен (sp.userprofiles)</span><span class="sxs-lookup"><span data-stu-id="6450e-173">SP.UserProfiles namespace (sp.userprofiles)</span></span>](http://msdn.microsoft.com/library/8c1fcceb-cd9a-b25c-32f4-1cfb0578278c%28Office.15%29.aspx)
    
  

