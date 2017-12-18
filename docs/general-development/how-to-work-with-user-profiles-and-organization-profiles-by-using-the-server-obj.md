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
# <a name="work-with-user-profiles-and-organization-profiles-by-using-the-server-object-model-in-sharepoint"></a>Работа с профилями пользователей и организации с использованием серверной объектной модели в SharePoint

Узнайте, как программно создать, восстановить и изменить профиль пользователя SharePoint и свойства профиля с помощью серверной объектной модели SharePoint.

## <a name="what-are-user-profiles-in-sharepoint"></a>Профили пользователей в SharePoint

В SharePoint профили представляют пользователей SharePoint. Свойства профиля представляют сведения о пользователях, а также о самих свойствах. Например, к свойствам относятся имя учетной записи или электронный адрес пользователя и тип данных свойства. С помощью серверной объектной модели вы можете программными средствами создавать, получать и изменять профили пользователей, подтипы и свойства профилей.
  
    
    

> **Примечание.** Дополнительную информацию о распространенных задачах программирования для работы с профилями пользователей и API для их выполнения см. в [этой статье](work-with-user-profiles-in-sharepoint.md). 
  
    
    


## <a name="prerequisites-for-setting-up-your-development-environment-to-work-with-user-profiles-by-using-the-sharepoint-server-object-model"></a>Необходимые компоненты для настройки среды разработки для работы с профилями пользователей с использованием серверной объектной модели SharePoint
<a name="bkmk_Prereqs"> </a>

Чтобы создать консольное приложение, использующее серверную объектную модель для работы с профилями пользователей и свойствами профиля пользователя, необходимы:
  
    
    

- SharePoint с профилем, созданным для текущего пользователя;
    
  
- Visual Studio 2012;
    
  
- разрешения на создание, извлечение и изменение объектов профилей пользователей. (Для создания и изменения профилей требуется разрешение **Изменение профилей пользователей**.)
    
  

## <a name="create-a-console-application-that-works-with-user-profiles-by-using-the-sharepoint-server-object-model"></a>Создание консольного приложения, работающего с профилями пользователей, с помощью серверной объектной модели SharePoint
<a name="bkmk_CreateConsoleApp"> </a>


1. Откройте Visual Studio и в меню **Файл** последовательно выберите элементы **Создать** и **Проект**.
    
  
2. В диалоговом окне **Новый проект** выберите **.NET Framework 4.5** из раскрывающегося списка в верхней части окна.
    
  
3. В списке **Шаблоны** выберите **Windows** и **Консольное приложение**.
    
  
4. Назовите проект UserProfilesSSOM и нажмите кнопку **OK**.
    
  > Примечание. Убедитесь, что в свойствах **построения** проекта не выбран параметр **Предпочитать 32-разрядн.**

5. Добавьте ссылки на следующие сборки:
    
  - Microsoft.Office.Server
  - Microsoft.Office.Server.UserProfiles
  - Microsoft.SharePoint
  - System.Web

  
6. Замените содержимое класса **Program** в примере кода на класс из следующих сценариев:
    
  -  [Создание профиля пользователя](how-to-work-with-user-profiles-and-organization-profiles-by-using-the-server-obj.md#bkmk_CreateUP)
  -  [Создание свойства профиля пользователя](how-to-work-with-user-profiles-and-organization-profiles-by-using-the-server-obj.md#bkmk_CreateUPProp)
  -  [Извлечение и изменение профилей пользователей](how-to-work-with-user-profiles-and-organization-profiles-by-using-the-server-obj.md#bkmk_GetChangeUP)
  -  [Извлечение и изменение атрибутов свойств профиля пользователя](how-to-work-with-user-profiles-and-organization-profiles-by-using-the-server-obj.md#bkmk_GetChangePropAttributes)
  -  [Извлечение и изменение значений свойств пользователя](how-to-work-with-user-profiles-and-organization-profiles-by-using-the-server-obj.md#bkmk_GetChangePropValues)
    
  
7. Чтобы протестировать консольное приложение, в строке меню выберите **Отладка** и щелкните **Начать отладку**. Изменения можно проверить на странице **Управление службой профилей** для приложения-службы профилей пользователей в центре администрирования.
    
  

## <a name="code-example-create-user-profiles-by-using-the-sharepoint-server-object-model"></a>Пример кода. Создание профилей пользователей с помощью серверной объектной модели SharePoint
<a name="bkmk_CreateUP"> </a>

В SharePoint профили представляют пользователей SharePoint. Типы и подтипы профилей позволяют разбить профили на группы, например на сотрудников или клиентов. Типы и подтипы профилей используются для установки общих свойств и атрибутов профиля на уровне подтипа. В SharePoint Server есть подтип профиля пользователя по умолчанию.
  
    
    
Следующий пример кода создает объект  [UserProfile](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.UserProfile.aspx) , связанный с подтипом профиля пользователя по умолчанию. Некоторые свойства профилей пользователей автоматически заполняются данными, импортированными из каталога, который содержит учетные записи пользователей, например Доменные службы Active Directory. Пример кода, создающий настраиваемый подтип, см. в разделе [ProfileSubtype](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.ProfileSubtype.aspx) .
  
    
    

> **Примечание.** Измените значения заполнителей domain\\username и servername перед запуском кода.
  
    
    




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


## <a name="code-example-create-user-profile-properties-by-using-the-sharepoint-server-object-model"></a>Пример кода: создание свойств профиля пользователя с помощью серверной объектной модели SharePoint
<a name="bkmk_CreateUPProp"> </a>

Свойства профиля пользователя описывают личные и организационные сведения о пользователях. Вы можете создать настраиваемое свойство профиля и добавить его в набор свойств профиля SharePoint по умолчанию.
  
    
    
Свойство профиля и его атрибуты представлены набором связанных объектов:  [CoreProperty](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.CoreProperty.aspx) , [ProfileTypeProperty](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.ProfileTypeProperty.aspx) и [ProfileSubtypeProperty](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.ProfileSubtypeProperty.aspx) .
  
    
    
Следующий пример кода создает объект  [CoreProperty](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.CoreProperty.aspx) с типом данных URL-адреса (или, при необходимости, [CoreProperty](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.CoreProperty.aspx) с многозначным строковым типом данных). Кроме того, он создает объекты [ProfileTypeProperty](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.ProfileTypeProperty.aspx) и [ProfileTypeProperty](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.ProfileTypeProperty.aspx) , определяющие параметры доступности, конфиденциальности и другие параметры свойства. Свойство [ProfileSubtypeProperty.DefaultPrivacy](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.ProfileSubtypeProperty.DefaultPrivacy.aspx) позволяет контролировать видимость свойства и другого контента личного сайта. Полный список возможных типов данных для значений свойств профиля см. в разделе [PropertyDataType](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.PropertyDataType.aspx) .
  
    
    

> **Примечание.** Измените значение заполнителя servername перед запуском кода.
  
    
    




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


## <a name="code-example-retrieve-and-change-user-profiles-by-using-the-sharepoint-server-object-model"></a>Пример кода: получение и изменение профилей пользователей с помощью серверной объектной модели SharePoint
<a name="bkmk_GetChangeUP"> </a>

Следующий пример кода возвращает все профили пользователей в контексте и изменяет значение свойства  [DisplayName](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.UserProfile.DisplayName.aspx) пользователя. Доступ к большинству свойств профилей осуществляется с помощью [UserProfile.Item](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.UserProfile.Item.aspx) .
  
    
    

> **Примечание.** Измените значения заполнителей domain\\username и servername перед запуском кода.
  
    
    


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


## <a name="code-example-retrieve-and-change-attributes-for-user-profile-properties-by-using-the-sharepoint-server-object-model"></a>Пример кода: получение и изменение атрибутов для свойств профилей пользователей с помощью серверной объектной модели SharePoint
<a name="bkmk_GetChangePropAttributes"> </a>

Следующий пример кода получает набор свойств, представляющий определенное свойство пользователя и его атрибуты, а затем изменяет атрибуты  [CoreProperty.DisplayName](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.CoreProperty.DisplayName.aspx) , [ProfileTypeProperty.IsVisibleOnViewer](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.ProfileTypeProperty.IsVisibleOnViewer.aspx) и [ProfileSubtypeProperty.PrivacyPolicy](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.ProfileSubtypeProperty.PrivacyPolicy.aspx) . Эти изменения применяются к набору свойств глобально. [ProfileSubtypeProperty.PrivacyPolicy](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.ProfileSubtypeProperty.PrivacyPolicy.aspx) определяет, должны ли пользователи указывать значение свойства. [PrivacyPolicy](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.ProfileSubtypeProperty.PrivacyPolicy.aspx) применяется только к свойствам профиля пользователя.
  
    
    

> **Примечание.** Измените значение заполнителя servername перед запуском кода.
  
    
    


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


## <a name="code-example-retrieve-and-change-values-for-user-properties-by-using-the-sharepoint-server-object-model"></a>Пример кода: получение и изменение значений для свойств пользователей с помощью серверной объектной модели SharePoint
<a name="bkmk_GetChangePropValues"> </a>

Следующий пример кода возвращает все свойства типа **UserProfile** и извлекает значения свойств для определенного пользователя. Затем он изменяет значение одного свойства [PictureUrl](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.PropertyConstants.PictureUrl.aspx) и свойство [PastProjects](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.PropertyConstants.PastProjects.aspx) с множественным значением. Полный список констант имен свойства профилей см. в разделе [PropertyConstants](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.PropertyConstants.aspx) .
  
    
    

> **Примечание.** Измените значения заполнителей domain\\username, http://servername/docLib/pic.jpg и servername перед запуском кода.
  
    
    


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


## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="bk_addresources"> </a>


-  [Работа с профилями пользователей в SharePoint](work-with-user-profiles-in-sharepoint.md)
    
  
-  [Как: получение свойств профиля пользователя с помощью клиентской объектной модели .NET в SharePoint](how-to-retrieve-user-profile-properties-by-using-the-net-client-object-model-in.md)
    
  
-  [Инструкции. Получение свойств профиля пользователя с помощью объектной модели JavaScript в SharePoint](how-to-retrieve-user-profile-properties-by-using-the-javascript-object-model-in.md)
    
  
-  [Microsoft.Office.Server.UserProfiles](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.aspx)
    
  

