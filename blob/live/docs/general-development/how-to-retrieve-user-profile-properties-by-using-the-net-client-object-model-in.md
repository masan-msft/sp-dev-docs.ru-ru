---
title: "Порядок извлечения свойств профилей пользователей с помощью клиентской объектной модели .NET в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 236ebaf8-f92e-4192-9b51-0a9de0210885
ms.openlocfilehash: b825ec245435a9d172c8fdc8064be7d92b0de38f
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-retrieve-user-profile-properties-by-using-the-net-client-object-model-in-sharepoint"></a><span data-ttu-id="a3ad8-102">Как: получение свойств профиля пользователя с помощью клиентской объектной модели .NET в SharePoint</span><span class="sxs-lookup"><span data-stu-id="a3ad8-102">How to: Retrieve user profile properties by using the .NET client object model in SharePoint</span></span>
<span data-ttu-id="a3ad8-103">Узнайте, как программно восстановить свойства профиля пользователя с помощью клиентской объектной модели .NET для SharePoint.</span><span class="sxs-lookup"><span data-stu-id="a3ad8-103">Learn how to retrieve user profile properties programmatically by using the SharePoint .NET client object model.</span></span>
## <a name="what-are-user-profile-properties-in-sharepoint"></a><span data-ttu-id="a3ad8-104">Что такое свойства профилей пользователей в SharePoint</span><span class="sxs-lookup"><span data-stu-id="a3ad8-104">What are user profile properties in SharePoint?</span></span>
<span data-ttu-id="a3ad8-105"><a name="bkmk_WhatIs"> </a></span><span class="sxs-lookup"><span data-stu-id="a3ad8-105"><a name="bkmk_WhatIs"> </a></span></span>

<span data-ttu-id="a3ad8-p101">Свойства пользователя и свойств профиля пользователя представлены сведения о пользователей SharePoint, такие как отображаемое имя, электронной почты, должность и других бизнес и личные сведения. В клиентских API доступа к этим свойствам из объекта  [PersonProperties](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PersonProperties.aspx) и его свойство [UserProfileProperties](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PersonProperties.UserProfileProperties.aspx) . Свойство [UserProfileProperties](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PersonProperties.UserProfileProperties.aspx) содержит все свойства профиля пользователя, но объект [PersonProperties](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PersonProperties.aspx) содержит часто используемые свойства (например, [AccountName](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PersonProperties.AccountName.aspx) , [DisplayName](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PersonProperties.DisplayName.aspx) и [Email](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PersonProperties.Email.aspx) ), которые легче доступа.</span><span class="sxs-lookup"><span data-stu-id="a3ad8-p101">User properties and user profile properties provide information about SharePoint users, such as display name, email, title, and other business and personal information. In client-side APIs, you access these properties from the  [PersonProperties](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PersonProperties.aspx) object and its [UserProfileProperties](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PersonProperties.UserProfileProperties.aspx) property. The [UserProfileProperties](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PersonProperties.UserProfileProperties.aspx) property contains all user profile properties, but the [PersonProperties](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PersonProperties.aspx) object contains commonly used properties (such as [AccountName](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PersonProperties.AccountName.aspx) , [DisplayName](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PersonProperties.DisplayName.aspx) , and [Email](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PersonProperties.Email.aspx) ) that are easier to access.</span></span>
  
    
    
<span data-ttu-id="a3ad8-109">Объект  [PeopleManager](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.aspx) содержит следующие методы, которые можно использовать для получения свойств пользователей и свойств профилей пользователей с помощью клиентской объектной модели .NET:</span><span class="sxs-lookup"><span data-stu-id="a3ad8-109">The  [PeopleManager](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.aspx) object includes the following methods that you can use to retrieve user properties and user profile properties by using the .NET client object model:</span></span>
  
    
    

- <span data-ttu-id="a3ad8-110">Метод  [GetMyProperties](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.GetMyProperties.aspx) и метод [GetPropertiesFor](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.GetPropertiesFor.aspx) возвращает объект [PersonProperties](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PersonProperties.aspx) .</span><span class="sxs-lookup"><span data-stu-id="a3ad8-110">The  [GetMyProperties](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.GetMyProperties.aspx) method and the [GetPropertiesFor](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.GetPropertiesFor.aspx) method return a [PersonProperties](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PersonProperties.aspx) object.</span></span>
    
  
- <span data-ttu-id="a3ad8-111">Метод  [GetUserProfilePropertiesFor](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.GetUserProfilePropertiesFor.aspx) и метод [GetUserProfilePropertyFor](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.GetUserProfilePropertyFor.aspx) возвращаемые значения пользователя, задаваемые свойства профиля.</span><span class="sxs-lookup"><span data-stu-id="a3ad8-111">The  [GetUserProfilePropertiesFor](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.GetUserProfilePropertiesFor.aspx) method and the [GetUserProfilePropertyFor](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.GetUserProfilePropertyFor.aspx) method return the values of the user profile properties that you specify.</span></span>
    
  
<span data-ttu-id="a3ad8-p102">Свойства профиля пользователя из клиентских API находятся только для чтения (за исключением изображение профиля можно изменить с помощью метода  [PeopleManager.SetMyProfilePicture](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.SetMyProfilePicture.aspx) ). Если вы хотите изменить другие свойства профиля пользователя, необходимо использовать серверной объектной модели.</span><span class="sxs-lookup"><span data-stu-id="a3ad8-p102">User profile properties from client APIs are read-only (except the profile picture, which you can change by using the  [PeopleManager.SetMyProfilePicture](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.SetMyProfilePicture.aspx) method). If you want to change other user profile properties, you must use the server object model.</span></span>
  
    
    

> <span data-ttu-id="a3ad8-114">**Примечание:** Версия клиентского объекта [UserProfile](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.UserProfile.aspx) , не содержит все свойства пользователя как версию на сервере.</span><span class="sxs-lookup"><span data-stu-id="a3ad8-114">**Note:** The client version of the  [UserProfile](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.UserProfile.aspx) object doesn't contain all of the user properties as the server-side version.</span></span> <span data-ttu-id="a3ad8-115">Тем не менее клиентские версии предоставляет методы для создания личного сайта для текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="a3ad8-115">However, the client-side version does provide the methods for creating a personal site for the current user.</span></span> <span data-ttu-id="a3ad8-116">Чтобы получить клиентские [UserProfile](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.UserProfile.aspx) для текущего пользователя, используйте метод [ProfileLoader.GetUserProfile](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.ProfileLoader.GetUserProfile.aspx) .</span><span class="sxs-lookup"><span data-stu-id="a3ad8-116">To retrieve the client-side [UserProfile](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.UserProfile.aspx) for the current user, use the [ProfileLoader.GetUserProfile](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.ProfileLoader.GetUserProfile.aspx) method.</span></span>
  
    
    

<span data-ttu-id="a3ad8-117">Дополнительные сведения о работе с профилями можно [работы с профилями пользователей в SharePoint](work-with-user-profiles-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="a3ad8-117">For more information about working with profiles, see  [Work with user profiles in SharePoint](work-with-user-profiles-in-sharepoint.md).</span></span>
  
    
    

## <a name="prerequisites-for-setting-up-your-development-environment-to-retrieve-user-profile-properties-by-using-the-sharepoint-net-client-object-model"></a><span data-ttu-id="a3ad8-118">Необходимые условия для настройки среды разработки для извлечения свойств профиля пользователя с помощью объектной модели клиента SharePoint .NET</span><span class="sxs-lookup"><span data-stu-id="a3ad8-118">Prerequisites for setting up your development environment to retrieve user profile properties by using the SharePoint .NET client object model</span></span>
<span data-ttu-id="a3ad8-119"><a name="bk_Prereqs"> </a></span><span class="sxs-lookup"><span data-stu-id="a3ad8-119"><a name="bk_Prereqs"> </a></span></span>

<span data-ttu-id="a3ad8-120">Создание консольного приложения, использующего клиентской объектной модели .NET для извлечения свойств профиля пользователя, необходимо следующее:</span><span class="sxs-lookup"><span data-stu-id="a3ad8-120">To create a console application that uses the .NET client object model to retrieve user profile properties, you'll need the following:</span></span>
  
    
    

- <span data-ttu-id="a3ad8-121">SharePoint с помощью профилей, созданных для текущего пользователя и конечного пользователя</span><span class="sxs-lookup"><span data-stu-id="a3ad8-121">SharePoint with profiles created for the current user and a target user</span></span>
    
  
- <span data-ttu-id="a3ad8-122">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="a3ad8-122">Visual Studio 2012</span></span>
    
  
- <span data-ttu-id="a3ad8-123">разрешения уровня **Полный доступ** для подключения к приложению-службе профиля текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="a3ad8-123">**Full Control** connection permissions to access the User Profile service application for the current user.</span></span>
    
  

> <span data-ttu-id="a3ad8-124">**Примечание:** При разработке не на компьютере, на котором работает SharePoint, загрузить [Клиентские компоненты SharePoint](http://www.microsoft.com/en-us/download/details.aspx?id=35585) , содержащий клиентскую сборку SharePoint.</span><span class="sxs-lookup"><span data-stu-id="a3ad8-124">**Note:** If you're not developing on the computer that is running SharePoint, get the  [SharePoint Client Components](http://www.microsoft.com/en-us/download/details.aspx?id=35585) download that contains SharePoint client assemblies.</span></span>
  
    
    


## <a name="create-the-console-application-that-retrieves-user-profile-properties-by-using-the-sharepoint-net-client-object-model"></a><span data-ttu-id="a3ad8-125">Создайте консольное приложение, которое извлекает свойства профилей пользователей с помощью клиентской объектной модели SharePoint .NET</span><span class="sxs-lookup"><span data-stu-id="a3ad8-125">Create the console application that retrieves user profile properties by using the SharePoint .NET client object model</span></span>
<span data-ttu-id="a3ad8-126"><a name="bk_RetrieveProps"> </a></span><span class="sxs-lookup"><span data-stu-id="a3ad8-126"><a name="bk_RetrieveProps"> </a></span></span>


1. <span data-ttu-id="a3ad8-127">На компьютере для разработки откройте Visual Studio и выберите **файл**, **Создать**, **проект**.</span><span class="sxs-lookup"><span data-stu-id="a3ad8-127">On your development computer, open Visual Studio and choose **File**, **New**, **Project**.</span></span>
    
  
2. <span data-ttu-id="a3ad8-128">В верхней части диалогового окна **Новый проект** выберите **.NET Framework 4.5** в раскрывающемся списке.</span><span class="sxs-lookup"><span data-stu-id="a3ad8-128">In the **New Project** dialog box, choose **.NET Framework 4.5** from the drop-down list at the top of the dialog box.</span></span>
    
  
3. <span data-ttu-id="a3ad8-129">На основе шаблонов проектов выберите **Windows** и выберите **Консольное приложение**.</span><span class="sxs-lookup"><span data-stu-id="a3ad8-129">From the project templates, choose **Windows**, and then choose **Console Application**.</span></span>
    
  
4. <span data-ttu-id="a3ad8-130">Назовите проект UserProfilesCSOMи затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="a3ad8-130">Name the project UserProfilesCSOM, and then choose the **OK** button.</span></span>
    
  
5. <span data-ttu-id="a3ad8-131">Добавьте ссылки на следующие сборки:</span><span class="sxs-lookup"><span data-stu-id="a3ad8-131">Add references to the following assemblies:</span></span>
    
  - <span data-ttu-id="a3ad8-132">**Microsoft.SharePoint.Client**</span><span class="sxs-lookup"><span data-stu-id="a3ad8-132">**Microsoft.SharePoint.Client**</span></span>
  - <span data-ttu-id="a3ad8-133">**Microsoft.SharePoint.ClientRuntime**</span><span class="sxs-lookup"><span data-stu-id="a3ad8-133">**Microsoft.SharePoint.ClientRuntime**</span></span>  
  - <span data-ttu-id="a3ad8-134">**Microsoft.SharePoint.Client.UserProfiles**</span><span class="sxs-lookup"><span data-stu-id="a3ad8-134">**Microsoft.SharePoint.Client.UserProfiles**</span></span>
    
  
6. <span data-ttu-id="a3ad8-135">В методе **Main** определите переменные для URL-адрес сервера и имя конечного пользователя, как показано в следующем коде.</span><span class="sxs-lookup"><span data-stu-id="a3ad8-135">In the **Main** method, define variables for the server URL and the target user name, as shown in the following code.</span></span>
    
```cs
const string serverUrl = "http://serverName/";
const string targetUser = "domainName\\\\userName";
```

   > <span data-ttu-id="a3ad8-136">Примечание: Не забудьте заменить `http://serverName/` и `domainName\\\\userName` заполнитель значения, прежде чем запускать код.</span><span class="sxs-lookup"><span data-stu-id="a3ad8-136">Note: Remember to replace the  `http://serverName/` and `domainName\\\\userName` placeholder values before you run the code.</span></span>

7. <span data-ttu-id="a3ad8-137">Инициализация контекста клиента SharePoint, как показано в следующем коде.</span><span class="sxs-lookup"><span data-stu-id="a3ad8-137">Initialize the SharePoint client context, as shown in the following code.</span></span>
    
```cs
ClientContext clientContext = new ClientContext(serverUrl);
```

8. <span data-ttu-id="a3ad8-138">Получение свойств конечного пользователя из объекта **PeopleManager**, как показано в следующем коде.</span><span class="sxs-lookup"><span data-stu-id="a3ad8-138">Get the target user's properties from the **PeopleManager** object, as shown in the following code.</span></span>
    
```cs
PeopleManager peopleManager = new PeopleManager(clientContext);
PersonProperties personProperties = peopleManager.GetPropertiesFor(targetUser);
```

   <span data-ttu-id="a3ad8-p104">Объект **personProperties**  это объект клиента. Некоторые клиентские объекты не содержат данных до их инициализации. Например значения свойств объекта **personProperties** недоступны до его инициализации. При попытке доступа к свойству до его инициализации, вы получаете исключение **PropertyOrFieldNotInitializedException**.</span><span class="sxs-lookup"><span data-stu-id="a3ad8-p104">The **personProperties** object is a client object. Some client objects contain no data until they are initialized. For example, you cannot access the property values of the **personProperties** object until you initialize it. If you try to access a property before it is initialized, you receive a **PropertyOrFieldNotInitializedException** exception.</span></span>
    
  
9. <span data-ttu-id="a3ad8-143">Для инициализации объекта **personProperties**, регистрация запроса, которую требуется запустить и выполнить запрос на сервере, как показано в следующем коде.</span><span class="sxs-lookup"><span data-stu-id="a3ad8-143">To initialize the **personProperties** object, register the request that you want to run, and then run the request on the server, as shown in the following code.</span></span>
    
```cs
clientContext.Load(personProperties, p => p.AccountName, p => p.UserProfileProperties);
clientContext.ExecuteQuery();
```

   <span data-ttu-id="a3ad8-p105">При вызове метода **Load** (или метод **LoadQuery** ), переданных в объект, который необходимо получить или изменить. В этом примере вызов метода **Load** передает необязательных параметров для фильтрации запроса. Лямбда-выражения, запрашивающих свойство **AccountName** и свойство **UserProfileProperties** объекта **personProperties** используются параметры.</span><span class="sxs-lookup"><span data-stu-id="a3ad8-p105">When you call the **Load** method (or the **LoadQuery** method), you pass in the object that you want to retrieve or change. In this example, the call to the **Load** method passes in optional parameters to filter the request. The parameters are lambda expressions that request only the **AccountName** property and **UserProfileProperties** property of the **personProperties** object.</span></span>
    
   ><span data-ttu-id="a3ad8-147">Совет: Чтобы уменьшить сетевой трафик, запросите только свойства, которые вы хотите работать с при вызове метода **Load** .</span><span class="sxs-lookup"><span data-stu-id="a3ad8-147">Tip: To reduce network traffic, request only the properties that you want to work with when you call the **Load** method.</span></span> <span data-ttu-id="a3ad8-148">Кроме того при работе с несколькими объектами групповой нескольких вызовы метода **нагрузки** по возможности перед вызовом метода **ExecuteQuery** .</span><span class="sxs-lookup"><span data-stu-id="a3ad8-148">In addition, if you're working with multiple objects, group multiple calls to the **Load** method when possible before you call the **ExecuteQuery** method.</span></span>

10. <span data-ttu-id="a3ad8-149">Выполните итерацию по свойств профилей пользователей и чтение имя и значение каждого свойства, как показано в следующем коде.</span><span class="sxs-lookup"><span data-stu-id="a3ad8-149">Iterate through the user profile properties and read the name and value of each property, as shown in the following code.</span></span>
    
```cs
foreach (var property in personProperties.UserProfileProperties)
{
    Console.WriteLine(string.Format("{0}: {1}", 
        property.Key.ToString(), property.Value.ToString()));
}
```


## <a name="code-example-retrieving-all-user-profile-properties-by-using-the-sharepoint-net-client-object-model"></a><span data-ttu-id="a3ad8-150">Пример кода: получение всех свойств профиля пользователя с помощью клиентской объектной модели SharePoint .NET</span><span class="sxs-lookup"><span data-stu-id="a3ad8-150">Code example: Retrieving all user profile properties by using the SharePoint .NET client object model</span></span>
<span data-ttu-id="a3ad8-151"><a name="SP15UserProf_codeexample1"> </a></span><span class="sxs-lookup"><span data-stu-id="a3ad8-151"><a name="SP15UserProf_codeexample1"> </a></span></span>

<span data-ttu-id="a3ad8-152">В следующем примере кода показано, как получить и выполнять итерацию по всем свойства профиля пользователя конечного пользователя, как описано в  [предыдущей процедуре](how-to-retrieve-user-profile-properties-by-using-the-net-client-object-model-in.md#bk_RetrieveProps).</span><span class="sxs-lookup"><span data-stu-id="a3ad8-152">The following code example shows how to retrieve and iterate through all the user profile properties of a target user, as described in the  [previous procedure](how-to-retrieve-user-profile-properties-by-using-the-net-client-object-model-in.md#bk_RetrieveProps).</span></span>
  
    
    

> <span data-ttu-id="a3ad8-153">**Примечание:** Замените `http://serverName/` и `domainName\\\\userName` заполнитель значения, прежде чем запускать код.</span><span class="sxs-lookup"><span data-stu-id="a3ad8-153">**Note:** Replace the  `http://serverName/` and `domainName\\\\userName` placeholder values before you run the code.</span></span>
  
    
    


```cs

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Microsoft.SharePoint.Client;
using Microsoft.SharePoint.Client.UserProfiles;

namespace UserProfilesCSOM
{
    class Program
    {
        static void Main(string[] args)
        {

            // Replace the following placeholder values with the target SharePoint site and
            // target user.
            const string serverUrl = "http://serverName/";  
            const string targetUser = "domainName\\\\userName";  

            // Connect to the client context.
            ClientContext clientContext = new ClientContext(serverUrl);

            // Get the PeopleManager object and then get the target user's properties.
            PeopleManager peopleManager = new PeopleManager(clientContext);
            PersonProperties personProperties = peopleManager.GetPropertiesFor(targetUser);

            // Load the request and run it on the server.
            // This example requests only the AccountName and UserProfileProperties
            // properties of the personProperties object.
            clientContext.Load(personProperties, p => p.AccountName, p => p.UserProfileProperties);
            clientContext.ExecuteQuery();

            foreach (var property in personProperties.UserProfileProperties)
            {
                Console.WriteLine(string.Format("{0}: {1}", 
                    property.Key.ToString(), property.Value.ToString()));
            }
            Console.ReadKey(false);

            // TODO: Add error handling and input validation.
        }
    }
}
```


## <a name="code-example-retrieving-user-profile-properties-of-people-who-are-following-me-by-using-the-sharepoint-net-client-object-model"></a><span data-ttu-id="a3ad8-154">Пример кода: получение свойств профиля пользователя людей, которые отслеживаются меня с помощью клиентской объектной модели SharePoint .NET</span><span class="sxs-lookup"><span data-stu-id="a3ad8-154">Code example: Retrieving user profile properties of people who are following me by using the SharePoint .NET client object model</span></span>
<span data-ttu-id="a3ad8-155"><a name="SP15UserProfilescodeInApp"> </a></span><span class="sxs-lookup"><span data-stu-id="a3ad8-155"><a name="SP15UserProfilescodeInApp"> </a></span></span>

<span data-ttu-id="a3ad8-156">В следующем примере кода показано, как получить Надстройка SharePoint свойства профиля пользователя по пользователей, которые вы подписались.</span><span class="sxs-lookup"><span data-stu-id="a3ad8-156">The following code example shows how to get, in a SharePoint Add-in, the user profile properties of people who are following you.</span></span>
  
    
    

```cs

string contextTokenString = TokenHelper.GetContextTokenFromRequest(Request);

if (contextTokenString != null)
{
    Uri sharepointUrl = new Uri(Request.QueryString["SP.Url"]);

    ClientContext clientContext = TokenHelper.GetClientContextWithContextToken(sharepointUrl.ToString(), contextTokenString, Request.Url.Authority);

    PeopleManager peopleManager = new PeopleManager(clientContext);
    ClientObjectList<PersonProperties> peopleFollowedBy = peopleManager.GetMyFollowers();
    clientContext.Load(peopleFollowedBy, people => people.Include(person => person.PictureUrl, person => person.DisplayName));
    clientContext.ExecuteQuery();

    foreach (PersonProperties personFollowedBy in peopleFollowedBy)
    {
        if (!string.IsNullOrEmpty(personFollowedBy.PictureUrl))
        {
        Response.Write("<img src=\\"" + personFollowedBy.PictureUrl + "\\" alt=\\"" + personFollowedBy.DisplayName + "\\"/>");
        }
    }
    clientContext.Dispose();
}
```


## <a name="code-example-retrieving-a-set-of-user-profile-properties-by-using-the-sharepoint-net-client-object-model"></a><span data-ttu-id="a3ad8-157">Пример кода: получение набор свойств профилей пользователей с помощью клиентской объектной модели SharePoint .NET</span><span class="sxs-lookup"><span data-stu-id="a3ad8-157">Code example: Retrieving a set of user profile properties by using the SharePoint .NET client object model</span></span>
<span data-ttu-id="a3ad8-158"><a name="SP15UserProfilescode2"> </a></span><span class="sxs-lookup"><span data-stu-id="a3ad8-158"><a name="SP15UserProfilescode2"> </a></span></span>

<span data-ttu-id="a3ad8-159">В следующем примере кода показано, как получить определенный набор свойств профилей пользователей для конечного пользователя.</span><span class="sxs-lookup"><span data-stu-id="a3ad8-159">The following code example shows how to retrieve a specific set of user profile properties for a target user.</span></span>
  
    
    

> <span data-ttu-id="a3ad8-160">**Примечание:** Чтобы получить значение для свойства профиля только один пользователь, используйте метод [GetUserProfilePropertyFor](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.GetUserProfilePropertyFor.aspx) .</span><span class="sxs-lookup"><span data-stu-id="a3ad8-160">**Note:** To retrieve the value for only one user profile property, use the  [GetUserProfilePropertyFor](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.GetUserProfilePropertyFor.aspx) method.</span></span>
  
    
    

<span data-ttu-id="a3ad8-p107">В отличие от предыдущего примера кода, который извлекает объект  [PersonProperties](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PersonProperties.aspx) для конечного пользователя в этом примере вызов метода [PeopleManager.GetUserProfilePropertiesFor](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.GetUserProfilePropertiesFor.aspx) и передает в объект [UserProfilePropertiesForUser](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.UserProfilePropertiesForUser.aspx) , который указывает конечного пользователя и свойств профилей пользователей для извлечения. [GetUserProfilePropertiesFor](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.GetUserProfilePropertiesFor.aspx) возвращает коллекцию **IEnumerable<string>**, который содержит значения свойств, которые можно указать.</span><span class="sxs-lookup"><span data-stu-id="a3ad8-p107">Unlike the previous code example that retrieves a  [PersonProperties](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PersonProperties.aspx) object for the target user, this example calls the [PeopleManager.GetUserProfilePropertiesFor](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.GetUserProfilePropertiesFor.aspx) method and passes in a [UserProfilePropertiesForUser](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.UserProfilePropertiesForUser.aspx) object that specifies the target user and the user profile properties to retrieve. [GetUserProfilePropertiesFor](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.GetUserProfilePropertiesFor.aspx) returns an **IEnumerable<string>** collection that contains the values of the properties that you specify.</span></span>
  
    
    

> <span data-ttu-id="a3ad8-163">**Примечание:** Замените `http://serverName/` и `domainName\\\\userName` заполнитель значения, прежде чем запускать код.</span><span class="sxs-lookup"><span data-stu-id="a3ad8-163">**Note:** Replace the  `http://serverName/` and `domainName\\\\userName` placeholder values before you run the code.</span></span>
  
    
    




```cs

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Microsoft.SharePoint.Client;
using Microsoft.SharePoint.Client.UserProfiles;

namespace UserProfilesCSOM
{
    class Program
    {
        static void Main(string[] args)
        {

            // Replace the following placeholder values with the target SharePoint site and the
            // target user.
            const string serverUrl = "http://serverName/";  
            const string targetUser = "domainName\\\\userName";  

            // Connect to the client context.
            ClientContext clientContext = new ClientContext(serverUrl);

            // Get the PeopleManager object.
            PeopleManager peopleManager = new PeopleManager(clientContext);

            // Retrieve specific properties by using the GetUserProfilePropertiesFor method. 
            // The returned collection contains only property values.
            string[] profilePropertyNames = new string[] { "PreferredName", "Department", "Title" };
            UserProfilePropertiesForUser profilePropertiesForUser = new UserProfilePropertiesForUser(
                clientContext, targetUser, profilePropertyNames);
            IEnumerable<string> profilePropertyValues = peopleManager.GetUserProfilePropertiesFor(profilePropertiesForUser);

            // Load the request and run it on the server.
            clientContext.Load(profilePropertiesForUser);
            clientContext.ExecuteQuery();

            // Iterate through the property values.
            foreach (var value in profilePropertyValues)
            {
                Console.Write(value + "\\n");
            }
            Console.ReadKey(false);

            // TO DO: Add error handling and input validation.
        }
    }
}

```


## <a name="additional-resources"></a><span data-ttu-id="a3ad8-164">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="a3ad8-164">Additional resources</span></span>
<span data-ttu-id="a3ad8-165"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="a3ad8-165"><a name="bk_addresources"> </a></span></span>


-  [<span data-ttu-id="a3ad8-166">Работа с профилями пользователей в SharePoint</span><span class="sxs-lookup"><span data-stu-id="a3ad8-166">Work with user profiles in SharePoint</span></span>](work-with-user-profiles-in-sharepoint.md)
    
  
-  [<span data-ttu-id="a3ad8-167">Инструкции. Получение свойств профиля пользователя с помощью объектной модели JavaScript в SharePoint</span><span class="sxs-lookup"><span data-stu-id="a3ad8-167">How to: Retrieve user profile properties by using the JavaScript object model in SharePoint</span></span>](how-to-retrieve-user-profile-properties-by-using-the-javascript-object-model-in.md)
    
  
-  [<span data-ttu-id="a3ad8-168">Инструкции. Работа с профилями пользователей и организации с использованием объектной модели сервера в SharePoint</span><span class="sxs-lookup"><span data-stu-id="a3ad8-168">How to: Work with user profiles and organization profiles by using the server object model in SharePoint</span></span>](how-to-work-with-user-profiles-and-organization-profiles-by-using-the-server-obj.md)
    
  
-  [<span data-ttu-id="a3ad8-169">Microsoft.SharePoint.Client.UserProfiles</span><span class="sxs-lookup"><span data-stu-id="a3ad8-169">Microsoft.SharePoint.Client.UserProfiles</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.aspx)
    
  

