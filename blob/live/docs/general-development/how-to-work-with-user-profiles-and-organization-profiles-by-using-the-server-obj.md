---
title: "Работа с профилями пользователей и организации с использованием серверной объектной модели в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 13f16dc3-f652-4fb3-996b-5f2166236d2b
ms.openlocfilehash: 242d2692b87433f5e33969d6d2dbfb037b366fdf
ms.sourcegitcommit: f6ea922341c38e700d0697961f8df9a454a03cba
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/15/2017
---
# <a name="work-with-user-profiles-and-organization-profiles-by-using-the-server-object-model-in-sharepoint"></a><span data-ttu-id="8e772-102">Работа с профилями пользователей и организации с использованием серверной объектной модели в SharePoint</span><span class="sxs-lookup"><span data-stu-id="8e772-102">How to: Work with user profiles and organization profiles by using the server object model in SharePoint</span></span>

<span data-ttu-id="8e772-103">Узнайте, как программно создать, восстановить и изменить профиль пользователя SharePoint и свойства профиля с помощью серверной объектной модели SharePoint.</span><span class="sxs-lookup"><span data-stu-id="8e772-103">Learn how to create, retrieve, and change SharePoint user profiles and user profile properties programmatically by using the SharePoint server object model.</span></span>

## <a name="what-are-user-profiles-in-sharepoint"></a><span data-ttu-id="8e772-104">Профили пользователей в SharePoint</span><span class="sxs-lookup"><span data-stu-id="8e772-104">What are user profiles in SharePoint?</span></span>

<span data-ttu-id="8e772-p101">В SharePoint профили представляют пользователей SharePoint. Свойства профиля представляют сведения о пользователях, а также о самих свойствах. Например, к свойствам относятся имя учетной записи или электронный адрес пользователя и тип данных свойства. С помощью серверной объектной модели вы можете программными средствами создавать, получать и изменять профили пользователей, подтипы и свойства профилей.</span><span class="sxs-lookup"><span data-stu-id="8e772-p101">In SharePoint, user profiles represent SharePoint users. User profile properties represent information about the users and also about the properties themselves. For example, properties include the account name or email address of a user and the data type of a property. You can use the server object model to programmatically create, retrieve, and change user profiles, profile subtypes, and profile properties.</span></span>
  
    
    

> <span data-ttu-id="8e772-109">**Примечание.** Дополнительную информацию о распространенных задачах программирования для работы с профилями пользователей и API для их выполнения см. в [этой статье](work-with-user-profiles-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="8e772-109">**Note:** For more information about common programming tasks for working with user profiles and the API that you use to perform the tasks, see  [Work with user profiles in SharePoint](work-with-user-profiles-in-sharepoint.md).</span></span> 
  
    
    


## <a name="prerequisites-for-setting-up-your-development-environment-to-work-with-user-profiles-by-using-the-sharepoint-server-object-model"></a><span data-ttu-id="8e772-110">Необходимые компоненты для настройки среды разработки для работы с профилями пользователей с использованием серверной объектной модели SharePoint</span><span class="sxs-lookup"><span data-stu-id="8e772-110">Prerequisites for setting up your development environment to work with user profiles by using the SharePoint server object model</span></span>
<span data-ttu-id="8e772-111"><a name="bkmk_Prereqs"> </a></span><span class="sxs-lookup"><span data-stu-id="8e772-111"><a name="bkmk_Prereqs"> </a></span></span>

<span data-ttu-id="8e772-112">Чтобы создать консольное приложение, использующее серверную объектную модель для работы с профилями пользователей и свойствами профиля пользователя, необходимы:</span><span class="sxs-lookup"><span data-stu-id="8e772-112">To create a console application that uses the server object model to work with user profiles and user profile properties, you'll need:</span></span>
  
    
    

- <span data-ttu-id="8e772-113">SharePoint с профилем, созданным для текущего пользователя;</span><span class="sxs-lookup"><span data-stu-id="8e772-113">SharePoint with the profile created for the current user.</span></span>
    
  
- <span data-ttu-id="8e772-114">Visual Studio 2012;</span><span class="sxs-lookup"><span data-stu-id="8e772-114">Visual Studio 2012.</span></span>
    
  
- <span data-ttu-id="8e772-p102">разрешения на создание, извлечение и изменение объектов профилей пользователей. (Для создания и изменения профилей требуется разрешение **Изменение профилей пользователей**.)</span><span class="sxs-lookup"><span data-stu-id="8e772-p102">Permissions to create, retrieve, and change user profile objects. (Creating and modifying profiles requires the **Modify User Profiles** permission.)</span></span>
    
  

## <a name="create-a-console-application-that-works-with-user-profiles-by-using-the-sharepoint-server-object-model"></a><span data-ttu-id="8e772-117">Создание консольного приложения, работающего с профилями пользователей, с помощью серверной объектной модели SharePoint</span><span class="sxs-lookup"><span data-stu-id="8e772-117">Create a console application that works with user profiles by using the SharePoint server object model</span></span>
<span data-ttu-id="8e772-118"><a name="bkmk_CreateConsoleApp"> </a></span><span class="sxs-lookup"><span data-stu-id="8e772-118"><a name="bkmk_CreateConsoleApp"> </a></span></span>


1. <span data-ttu-id="8e772-119">Откройте Visual Studio и в меню **Файл** последовательно выберите элементы **Создать** и **Проект**.</span><span class="sxs-lookup"><span data-stu-id="8e772-119">Open Visual Studio and choose **File**, **New**, **Project**.</span></span>
    
  
2. <span data-ttu-id="8e772-120">В диалоговом окне **Новый проект** выберите **.NET Framework 4.5** из раскрывающегося списка в верхней части окна.</span><span class="sxs-lookup"><span data-stu-id="8e772-120">In the **New Project** dialog box, choose **.NET Framework 4.5** from the drop-down list at the top of the dialog box.</span></span>
    
  
3. <span data-ttu-id="8e772-121">В списке **Шаблоны** выберите **Windows** и **Консольное приложение**.</span><span class="sxs-lookup"><span data-stu-id="8e772-121">In the **Templates** list, choose **Windows**, and then choose **Console Application**.</span></span>
    
  
4. <span data-ttu-id="8e772-122">Назовите проект UserProfilesSSOM и нажмите кнопку **OK**.</span><span class="sxs-lookup"><span data-stu-id="8e772-122">Name the project UserProfilesSSOM, and then choose the **OK** button.</span></span>
    
  > <span data-ttu-id="8e772-123">Примечание. Убедитесь, что в свойствах **построения** проекта не выбран параметр **Предпочитать 32-разрядн.**</span><span class="sxs-lookup"><span data-stu-id="8e772-123">Note: Make sure the **Prefer 32-bit** setting is not selected in the project's **Build** properties.</span></span>

5. <span data-ttu-id="8e772-124">Добавьте ссылки на следующие сборки:</span><span class="sxs-lookup"><span data-stu-id="8e772-124">Add references to the following assemblies:</span></span>
    
  - <span data-ttu-id="8e772-125">Microsoft.Office.Server</span><span class="sxs-lookup"><span data-stu-id="8e772-125">Microsoft.Office.Server</span></span>
  - <span data-ttu-id="8e772-126">Microsoft.Office.Server.UserProfiles</span><span class="sxs-lookup"><span data-stu-id="8e772-126">Microsoft.Office.Server.UserProfiles</span></span>
  - <span data-ttu-id="8e772-127">Microsoft.SharePoint</span><span class="sxs-lookup"><span data-stu-id="8e772-127">Microsoft.SharePoint</span></span>
  - <span data-ttu-id="8e772-128">System.Web</span><span class="sxs-lookup"><span data-stu-id="8e772-128">System.Web</span></span>

  
6. <span data-ttu-id="8e772-129">Замените содержимое класса **Program** в примере кода на класс из следующих сценариев:</span><span class="sxs-lookup"><span data-stu-id="8e772-129">Replace the contents of the **Program** class with the code example from one of the following scenarios:</span></span>
    
  -  [<span data-ttu-id="8e772-130">Создание профиля пользователя</span><span class="sxs-lookup"><span data-stu-id="8e772-130">Create a user profile</span></span>](how-to-work-with-user-profiles-and-organization-profiles-by-using-the-server-obj.md#bkmk_CreateUP)
  -  [<span data-ttu-id="8e772-131">Создание свойства профиля пользователя</span><span class="sxs-lookup"><span data-stu-id="8e772-131">Create a user profile property</span></span>](how-to-work-with-user-profiles-and-organization-profiles-by-using-the-server-obj.md#bkmk_CreateUPProp)
  -  [<span data-ttu-id="8e772-132">Извлечение и изменение профилей пользователей</span><span class="sxs-lookup"><span data-stu-id="8e772-132">Retrieve and change user profiles</span></span>](how-to-work-with-user-profiles-and-organization-profiles-by-using-the-server-obj.md#bkmk_GetChangeUP)
  -  [<span data-ttu-id="8e772-133">Извлечение и изменение атрибутов свойств профиля пользователя</span><span class="sxs-lookup"><span data-stu-id="8e772-133">Retrieve and change attributes for user profile properties</span></span>](how-to-work-with-user-profiles-and-organization-profiles-by-using-the-server-obj.md#bkmk_GetChangePropAttributes)
  -  [<span data-ttu-id="8e772-134">Извлечение и изменение значений свойств пользователя</span><span class="sxs-lookup"><span data-stu-id="8e772-134">Retrieve and change values for user properties</span></span>](how-to-work-with-user-profiles-and-organization-profiles-by-using-the-server-obj.md#bkmk_GetChangePropValues)
    
  
7. <span data-ttu-id="8e772-p103">Чтобы протестировать консольное приложение, в строке меню выберите **Отладка** и щелкните **Начать отладку**. Изменения можно проверить на странице **Управление службой профилей** для приложения-службы профилей пользователей в центре администрирования.</span><span class="sxs-lookup"><span data-stu-id="8e772-p103">To test the console application, on the menu bar, choose **Debug**, **Start Debugging**. You can check your changes from the **Manage Profile Service** page for the User Profile Service Application in Central Administration.</span></span>
    
  

## <a name="code-example-create-user-profiles-by-using-the-sharepoint-server-object-model"></a><span data-ttu-id="8e772-137">Пример кода. Создание профилей пользователей с помощью серверной объектной модели SharePoint</span><span class="sxs-lookup"><span data-stu-id="8e772-137">Code example: Create user profiles by using the SharePoint server object model</span></span>
<span data-ttu-id="8e772-138"><a name="bkmk_CreateUP"> </a></span><span class="sxs-lookup"><span data-stu-id="8e772-138"><a name="bkmk_CreateUP"> </a></span></span>

<span data-ttu-id="8e772-p104">В SharePoint профили представляют пользователей SharePoint. Типы и подтипы профилей позволяют разбить профили на группы, например на сотрудников или клиентов. Типы и подтипы профилей используются для установки общих свойств и атрибутов профиля на уровне подтипа. В SharePoint Server есть подтип профиля пользователя по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="8e772-p104">In SharePoint, user profiles represent SharePoint users. Profile types and subtypes help categorize profiles into groups, such as employees or customers. Profile types and subtypes are used to set common profile properties and attributes at the subtype level. SharePoint Server includes a default user profile subtype.</span></span>
  
    
    
<span data-ttu-id="8e772-p105">Следующий пример кода создает объект  [UserProfile](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.UserProfile.aspx) , связанный с подтипом профиля пользователя по умолчанию. Некоторые свойства профилей пользователей автоматически заполняются данными, импортированными из каталога, который содержит учетные записи пользователей, например Доменные службы Active Directory. Пример кода, создающий настраиваемый подтип, см. в разделе [ProfileSubtype](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.ProfileSubtype.aspx) .</span><span class="sxs-lookup"><span data-stu-id="8e772-p105">The following code example creates a  [UserProfile](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.UserProfile.aspx) object that is associated with the default user profile subtype. Some user profile properties are automatically populated with information that is imported from the directory that contains user accounts, such as Active Directory Domain Services. For a code example that creates a custom subtype, see [ProfileSubtype](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.ProfileSubtype.aspx) .</span></span>
  
    
    

> <span data-ttu-id="8e772-146">**Примечание.** Измените значения заполнителей domain\\username и servername перед запуском кода.</span><span class="sxs-lookup"><span data-stu-id="8e772-146">**Note:** Change the domain\\username andservername placeholder values before you run the code.</span></span>
  
    
    




```cs

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Microsoft.Office.Server;
using Microsoft.Office.Server.UserProfiles;
using Microsoft.SharePoint;
using System.Web;
namespace UserProfilesSSOM
{
    class Program
    {
        static void Main(string[] args)
        {

            // Replace "domain\\username" and "servername" with actual values.
            string newAccountName = "domain\\username";
            using (SPSite site = new SPSite("http://servername"))
            {
                SPServiceContext serviceContext = SPServiceContext.GetContext(site);
                try
                {

                    // Create a user profile that uses the default user profile
                    // subtype.
                    UserProfileManager userProfileMgr = new UserProfileManager(serviceContext);
                    UserProfile userProfile = userProfileMgr.CreateUserProfile(newAccountName);

                    Console.WriteLine("A profile was created for " + userProfile.DisplayName);
                    Console.Read();
                }

                catch (System.Exception e)
                {
                    Console.WriteLine(e.GetType().ToString() + ": " + e.Message);
                    Console.Read();
                }
            }
        }
    }
}
```


## <a name="code-example-create-user-profile-properties-by-using-the-sharepoint-server-object-model"></a><span data-ttu-id="8e772-147">Пример кода: создание свойств профиля пользователя с помощью серверной объектной модели SharePoint</span><span class="sxs-lookup"><span data-stu-id="8e772-147">Code example: Create user profile properties by using the SharePoint server object model</span></span>
<span data-ttu-id="8e772-148"><a name="bkmk_CreateUPProp"> </a></span><span class="sxs-lookup"><span data-stu-id="8e772-148"><a name="bkmk_CreateUPProp"> </a></span></span>

<span data-ttu-id="8e772-p106">Свойства профиля пользователя описывают личные и организационные сведения о пользователях. Вы можете создать настраиваемое свойство профиля и добавить его в набор свойств профиля SharePoint по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="8e772-p106">User profile properties describe personal and organizational information about users. You can create and add a custom profile property to the default set of SharePoint profile properties.</span></span>
  
    
    
<span data-ttu-id="8e772-151">Свойство профиля и его атрибуты представлены набором связанных объектов:  [CoreProperty](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.CoreProperty.aspx) , [ProfileTypeProperty](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.ProfileTypeProperty.aspx) и [ProfileSubtypeProperty](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.ProfileSubtypeProperty.aspx) .</span><span class="sxs-lookup"><span data-stu-id="8e772-151">A profile property and its attributes are represented by a set of linked objects: a  [CoreProperty](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.CoreProperty.aspx) object, a [ProfileTypeProperty](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.ProfileTypeProperty.aspx) object, and a [ProfileSubtypeProperty](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.ProfileSubtypeProperty.aspx) object.</span></span>
  
    
    
<span data-ttu-id="8e772-p107">Следующий пример кода создает объект  [CoreProperty](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.CoreProperty.aspx) с типом данных URL-адреса (или, при необходимости, [CoreProperty](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.CoreProperty.aspx) с многозначным строковым типом данных). Кроме того, он создает объекты [ProfileTypeProperty](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.ProfileTypeProperty.aspx) и [ProfileTypeProperty](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.ProfileTypeProperty.aspx) , определяющие параметры доступности, конфиденциальности и другие параметры свойства. Свойство [ProfileSubtypeProperty.DefaultPrivacy](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.ProfileSubtypeProperty.DefaultPrivacy.aspx) позволяет контролировать видимость свойства и другого контента личного сайта. Полный список возможных типов данных для значений свойств профиля см. в разделе [PropertyDataType](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.PropertyDataType.aspx) .</span><span class="sxs-lookup"><span data-stu-id="8e772-p107">The following code example creates a  [CoreProperty](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.CoreProperty.aspx) that has a URL data type (or optionally a [CoreProperty](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.CoreProperty.aspx) that has a multivalue string data type). In addition, it creates a [ProfileTypeProperty](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.ProfileTypeProperty.aspx) and a [ProfileTypeProperty](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.ProfileTypeProperty.aspx) that define availability, privacy, and other settings for the property. The [ProfileSubtypeProperty.DefaultPrivacy](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.ProfileSubtypeProperty.DefaultPrivacy.aspx) property controls the visibility of properties and other My Site content. For a complete list of the possible data types for profile property values, see [PropertyDataType](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.PropertyDataType.aspx) .</span></span>
  
    
    

> <span data-ttu-id="8e772-156">**Примечание.** Измените значение заполнителя servername перед запуском кода.</span><span class="sxs-lookup"><span data-stu-id="8e772-156">**Note:** Change the servername placeholder value before you run the code.</span></span>
  
    
    




```cs

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Microsoft.Office.Server;
using Microsoft.Office.Server.Administration;
using Microsoft.Office.Server.UserProfiles;
using Microsoft.SharePoint;
using System.Web;
namespace UserProfilesSSOM
{
    class Program
    {
        static void Main(string[] args)
        {

            // Replace "servername" with an actual value.
            using (SPSite site = new SPSite("http://servername"))
            {
                SPServiceContext serviceContext = SPServiceContext.GetContext(site);
                try
                {
                    ProfilePropertyManager profilePropMgr = new UserProfileConfigManager(serviceContext).ProfilePropertyManager;
                    CorePropertyManager corePropMgr = profilePropMgr.GetCoreProperties();

                    // Create a URL property.
                    CoreProperty coreProp = corePropMgr.Create(false);
                    coreProp.Name = "AppsWebsite";
                    coreProp.DisplayName = "Apps site";
                    coreProp.Type = PropertyDataType.URL;
                    coreProp.Length = 100;
                    corePropMgr.Add(coreProp);

                    //// Create a multivalue property.
                    //// To create this property, comment out the previous
                    //// block of code and uncomment this block of code.
                    //CoreProperty coreProp = corePropMgr.Create(false);
                    //coreProp.Name = "PublishedAppsList";
                    //coreProp.DisplayName = "Published apps";
                    //coreProp.Type = PropertyDataType.StringMultiValue;
                    //coreProp.IsMultivalued = true;
                    //coreProp.Length = 100;
                    //corePropMgr.Add(coreProp);

                    // Create a profile type property and make the core property 
                    // visible in the Details section page.
                    ProfileTypePropertyManager typePropMgr = profilePropMgr.GetProfileTypeProperties(ProfileType.User);
                    ProfileTypeProperty typeProp = typePropMgr.Create(coreProp);
                    typeProp.IsVisibleOnViewer = true;
                    typePropMgr.Add(typeProp);

                    // Create a profile subtype property.
                    ProfileSubtypeManager subtypeMgr = ProfileSubtypeManager.Get(serviceContext);
                    ProfileSubtype subtype = subtypeMgr.GetProfileSubtype(ProfileSubtypeManager.GetDefaultProfileName(ProfileType.User));
                    ProfileSubtypePropertyManager subtypePropMgr = profilePropMgr.GetProfileSubtypeProperties(subtype.Name);
                    ProfileSubtypeProperty subtypeProp = subtypePropMgr.Create(typeProp);
                    subtypeProp.IsUserEditable = true;
                    subtypeProp.DefaultPrivacy = Privacy.Public;
                    subtypeProp.UserOverridePrivacy = true;
                    subtypePropMgr.Add(subtypeProp);

                    Console.WriteLine("The properties were created.");
                    Console.Read();
                }

                catch (System.Exception e)
                {
                    Console.WriteLine(e.GetType().ToString() + ": " + e.Message);
                    Console.Read();
                }
            }
        }
    }
}
```


## <a name="code-example-retrieve-and-change-user-profiles-by-using-the-sharepoint-server-object-model"></a><span data-ttu-id="8e772-157">Пример кода: получение и изменение профилей пользователей с помощью серверной объектной модели SharePoint</span><span class="sxs-lookup"><span data-stu-id="8e772-157">Code example: Retrieve and change user profiles by using the SharePoint server object model</span></span>
<span data-ttu-id="8e772-158"><a name="bkmk_GetChangeUP"> </a></span><span class="sxs-lookup"><span data-stu-id="8e772-158"><a name="bkmk_GetChangeUP"> </a></span></span>

<span data-ttu-id="8e772-p108">Следующий пример кода возвращает все профили пользователей в контексте и изменяет значение свойства  [DisplayName](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.UserProfile.DisplayName.aspx) пользователя. Доступ к большинству свойств профилей осуществляется с помощью [UserProfile.Item](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.UserProfile.Item.aspx) .</span><span class="sxs-lookup"><span data-stu-id="8e772-p108">The following code example retrieves all user profiles within the context and changes the value of a user's  [DisplayName](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.UserProfile.DisplayName.aspx) property. Most profile properties are accessed by using the [UserProfile.Item](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.UserProfile.Item.aspx) accessor.</span></span>
  
    
    

> <span data-ttu-id="8e772-161">**Примечание.** Измените значения заполнителей domain\\username и servername перед запуском кода.</span><span class="sxs-lookup"><span data-stu-id="8e772-161">**Note:** Change the domain\\username andservername placeholder values before you run the code.</span></span>
  
    
    


```cs

using System;
using System.Collections;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Microsoft.Office.Server;
using Microsoft.Office.Server.UserProfiles;
using Microsoft.SharePoint;
using System.Web;
namespace UserProfilesSSOM
{
    class Program
    {
        static void Main(string[] args)
        {

            // Replace "domain\\username" and "servername" with actual values.
            string targetAccountName = "domain\\username";
            using (SPSite site = new SPSite("http://servername"))
            {
                SPServiceContext serviceContext = SPServiceContext.GetContext(site);
                try
                {

                    // Retrieve and iterate through all of the user profiles in this context.
                    Console.WriteLine("Retrieving user profiles:");
                    UserProfileManager userProfileMgr = new UserProfileManager(serviceContext);
                    IEnumerator userProfiles = userProfileMgr.GetEnumerator();
                    while (userProfiles.MoveNext())
                    {
                        UserProfile userProfile = (UserProfile)userProfiles.Current;
                        Console.WriteLine(userProfile.AccountName);
                    }

                    // Retrieve a specific user profile. Change the value of a user profile property
                    // and save (commit) the change on the server.
                    UserProfile user = userProfileMgr.GetUserProfile(targetAccountName);
                    Console.WriteLine("\\nRetrieving user profile for " + user.DisplayName + ".");
                    user.DisplayName = "Pat";
                    user.Commit();
                    Console.WriteLine("\\nThe user\\'s display name has been changed.");
                    Console.Read();
                }

                catch (System.Exception e)
                {
                    Console.WriteLine(e.GetType().ToString() + ": " + e.Message);
                    Console.Read();
                }
            }
        }
    }
}
```


## <a name="code-example-retrieve-and-change-attributes-for-user-profile-properties-by-using-the-sharepoint-server-object-model"></a><span data-ttu-id="8e772-162">Пример кода: получение и изменение атрибутов для свойств профилей пользователей с помощью серверной объектной модели SharePoint</span><span class="sxs-lookup"><span data-stu-id="8e772-162">Code example: Retrieve and change attributes for user profile properties by using the SharePoint server object model</span></span>
<span data-ttu-id="8e772-163"><a name="bkmk_GetChangePropAttributes"> </a></span><span class="sxs-lookup"><span data-stu-id="8e772-163"><a name="bkmk_GetChangePropAttributes"> </a></span></span>

<span data-ttu-id="8e772-p109">Следующий пример кода получает набор свойств, представляющий определенное свойство пользователя и его атрибуты, а затем изменяет атрибуты  [CoreProperty.DisplayName](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.CoreProperty.DisplayName.aspx) , [ProfileTypeProperty.IsVisibleOnViewer](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.ProfileTypeProperty.IsVisibleOnViewer.aspx) и [ProfileSubtypeProperty.PrivacyPolicy](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.ProfileSubtypeProperty.PrivacyPolicy.aspx) . Эти изменения применяются к набору свойств глобально. [ProfileSubtypeProperty.PrivacyPolicy](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.ProfileSubtypeProperty.PrivacyPolicy.aspx) определяет, должны ли пользователи указывать значение свойства. [PrivacyPolicy](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.ProfileSubtypeProperty.PrivacyPolicy.aspx) применяется только к свойствам профиля пользователя.</span><span class="sxs-lookup"><span data-stu-id="8e772-p109">The following code example retrieves the set of properties that represent a specific user property and its attributes, and then it changes the  [CoreProperty.DisplayName](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.CoreProperty.DisplayName.aspx) attribute, [ProfileTypeProperty.IsVisibleOnViewer](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.ProfileTypeProperty.IsVisibleOnViewer.aspx) attribute, and [ProfileSubtypeProperty.PrivacyPolicy](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.ProfileSubtypeProperty.PrivacyPolicy.aspx) attribute. These changes apply globally to the property set. [ProfileSubtypeProperty.PrivacyPolicy](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.ProfileSubtypeProperty.PrivacyPolicy.aspx) specifies whether users are required to provide a value for the property. [PrivacyPolicy](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.ProfileSubtypeProperty.PrivacyPolicy.aspx) applies to user profile properties only.</span></span>
  
    
    

> <span data-ttu-id="8e772-168">**Примечание.** Измените значение заполнителя servername перед запуском кода.</span><span class="sxs-lookup"><span data-stu-id="8e772-168">**Note:** Change the servername placeholder value before you run the code.</span></span>
  
    
    


```cs

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Microsoft.Office.Server;
using Microsoft.Office.Server.UserProfiles;
using Microsoft.SharePoint;
using System.Web;
namespace UserProfilesSSOM
{
    class Program
    {
        static void Main(string[] args)
        {

            // Replace "servername" with an actual value.
            using (SPSite site = new SPSite("http://servername"))
            {
                SPServiceContext serviceContext = SPServiceContext.GetContext(site);
                try
                {
                    ProfilePropertyManager profilePropMgr = new UserProfileConfigManager(serviceContext).ProfilePropertyManager;
                    ProfileSubtypePropertyManager subtypePropMgr = profilePropMgr.GetProfileSubtypeProperties("UserProfile");

                    // Retrieve a specific property set (a profile subtype property and
                    // its associated core and profile type properties).
                    // Changing these properties affects all instances of this property set.
                    ProfileSubtypeProperty subtypeProp = subtypePropMgr.GetPropertyByName(PropertyConstants.Title);
                    CoreProperty coreProp = subtypeProp.CoreProperty;
                    ProfileTypeProperty typeProp = subtypeProp.TypeProperty;

                    Console.WriteLine("Property name: " + coreProp.DisplayName);
                    Console.WriteLine("IsVisibleOnViewer = " + typeProp.IsVisibleOnViewer);
                    Console.WriteLine("PrivacyPolicy = " + subtypeProp.PrivacyPolicy);
                    Console.WriteLine("Press Enter to change the values.");
                    Console.Read();

                    // Change attributes on the properties and save (commit) the changes
                    // on the server.
                    coreProp.DisplayName = "Position";
                    coreProp.Commit();
                    typeProp.IsVisibleOnViewer = true;
                    typeProp.Commit();
                    subtypeProp.PrivacyPolicy = PrivacyPolicy.OptOut;
                    subtypeProp.Commit();
                    Console.WriteLine("The property attributes have been changed.");
                    Console.Read();
                }

                catch (System.Exception e)
                {
                    Console.WriteLine(e.GetType().ToString() + ": " + e.Message);
                    Console.Read();
                }
            }
        }
    }
}
```


## <a name="code-example-retrieve-and-change-values-for-user-properties-by-using-the-sharepoint-server-object-model"></a><span data-ttu-id="8e772-169">Пример кода: получение и изменение значений для свойств пользователей с помощью серверной объектной модели SharePoint</span><span class="sxs-lookup"><span data-stu-id="8e772-169">Code example: Retrieve and change values for user properties by using the SharePoint server object model</span></span>
<span data-ttu-id="8e772-170"><a name="bkmk_GetChangePropValues"> </a></span><span class="sxs-lookup"><span data-stu-id="8e772-170"><a name="bkmk_GetChangePropValues"> </a></span></span>

<span data-ttu-id="8e772-p110">Следующий пример кода возвращает все свойства типа **UserProfile** и извлекает значения свойств для определенного пользователя. Затем он изменяет значение одного свойства [PictureUrl](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.PropertyConstants.PictureUrl.aspx) и свойство [PastProjects](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.PropertyConstants.PastProjects.aspx) с множественным значением. Полный список констант имен свойства профилей см. в разделе [PropertyConstants](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.PropertyConstants.aspx) .</span><span class="sxs-lookup"><span data-stu-id="8e772-p110">The following code example retrieves all **UserProfile** type properties and retrieves the property values for a specific user. Then, it changes the single-value [PictureUrl](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.PropertyConstants.PictureUrl.aspx) property and the multivalue [PastProjects](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.PropertyConstants.PastProjects.aspx) property. For the complete list of profile property name constants, see [PropertyConstants](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.PropertyConstants.aspx) .</span></span>
  
    
    

> <span data-ttu-id="8e772-174">**Примечание.** Измените значения заполнителей domain\\username, http://servername/docLib/pic.jpg и servername перед запуском кода.</span><span class="sxs-lookup"><span data-stu-id="8e772-174">**Note:** Change the domain\\username, http://servername/docLib/pic.jpg, and servername placeholder values before you run the code.</span></span>
  
    
    


```cs

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Microsoft.Office.Server;
using Microsoft.Office.Server.UserProfiles;
using Microsoft.SharePoint;
using System.Web;
namespace UserProfilesSSOM
{
    class Program
    {
        static void Main(string[] args)
        {

            // Replace "domain\\username," "http://servername/docLib/pic.jpg," and "servername" with actual values.
            string accountName = "domain\\username";
            string newPictureUrl = "http://servername/docLib/pic.jpg";
            using (SPSite site = new SPSite("http://servername"))
            {
                SPServiceContext serviceContext = SPServiceContext.GetContext(site);

                try
                {
                    UserProfileManager userProfileMgr = new UserProfileManager(serviceContext);
                    ProfilePropertyManager profilePropMgr = new UserProfileConfigManager(serviceContext).ProfilePropertyManager;
                   
                    // Retrieve all properties for the "UserProfile" profile subtype,
                    // and retrieve the property values for a specific user.
                    ProfileSubtypePropertyManager subtypePropMgr = profilePropMgr.GetProfileSubtypeProperties("UserProfile");
                    UserProfile userProfile = userProfileMgr.GetUserProfile(accountName);
                    IEnumerator<ProfileSubtypeProperty> userProfileSubtypeProperties = subtypePropMgr.GetEnumerator();
                    while (userProfileSubtypeProperties.MoveNext())
                    {
                        string propName = userProfileSubtypeProperties.Current.Name;
                        ProfileValueCollectionBase values = userProfile.GetProfileValueCollection(propName);
                        if (values.Count > 0)
                        {

                            // Handle multivalue properties.
                            foreach (var value in values)
                            {
                                Console.WriteLine(propName + ": " + value.ToString());
                            }
                        }
                        else
                        {
                            Console.WriteLine(propName + ": ");
                        }
                    }
                    Console.WriteLine("Press Enter to change the values.");
                    Console.Read();

                    // Change the value of a single-value user property.
                    userProfile[PropertyConstants.PictureUrl].Value = newPictureUrl;

                    // Add a value to a multivalue user property.
                    userProfile[PropertyConstants.PastProjects].Add((object)"Team Feed App");
                    userProfile[PropertyConstants.PastProjects].Add((object)"Social Ratings View Web Part");

                    // Save the changes to the server.
                    userProfile.Commit();
                    Console.WriteLine("The property values for the user have been changed.");
                    Console.Read();
                }

                catch (System.Exception e)
                {
                    Console.WriteLine(e.GetType().ToString() + ": " + e.Message);
                    Console.Read();
                }
            }
        }
    }
}
```


## <a name="additional-resources"></a><span data-ttu-id="8e772-175">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="8e772-175">Additional resources</span></span>
<span data-ttu-id="8e772-176"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="8e772-176"><a name="bk_addresources"> </a></span></span>


-  [<span data-ttu-id="8e772-177">Работа с профилями пользователей в SharePoint</span><span class="sxs-lookup"><span data-stu-id="8e772-177">Work with user profiles in SharePoint</span></span>](work-with-user-profiles-in-sharepoint.md)
    
  
-  [<span data-ttu-id="8e772-178">Как: получение свойств профиля пользователя с помощью клиентской объектной модели .NET в SharePoint</span><span class="sxs-lookup"><span data-stu-id="8e772-178">How to: Retrieve user profile properties by using the .NET client object model in SharePoint</span></span>](how-to-retrieve-user-profile-properties-by-using-the-net-client-object-model-in.md)
    
  
-  [<span data-ttu-id="8e772-179">Инструкции. Получение свойств профиля пользователя с помощью объектной модели JavaScript в SharePoint</span><span class="sxs-lookup"><span data-stu-id="8e772-179">How to: Retrieve user profile properties by using the JavaScript object model in SharePoint</span></span>](how-to-retrieve-user-profile-properties-by-using-the-javascript-object-model-in.md)
    
  
-  [<span data-ttu-id="8e772-180">Microsoft.Office.Server.UserProfiles</span><span class="sxs-lookup"><span data-stu-id="8e772-180">Microsoft.Office.Server.UserProfiles</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.aspx)
    
  

