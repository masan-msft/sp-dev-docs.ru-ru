---
title: "Извлечение свойств профиля пользователя с помощью клиентской объектной модели .NET в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 236ebaf8-f92e-4192-9b51-0a9de0210885
ms.openlocfilehash: 1d77fdaccfeeefafc9a7d43476140a0c8a632515
ms.sourcegitcommit: f6ea922341c38e700d0697961f8df9a454a03cba
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/15/2017
---
# <a name="retrieve-user-profile-properties-by-using-the-net-client-object-model-in-sharepoint"></a>Извлечение свойств профиля пользователя с помощью клиентской объектной модели .NET в SharePoint

Узнайте, как программно восстановить свойства профиля пользователя с помощью клиентской объектной модели .NET для SharePoint.

## <a name="what-are-user-profile-properties-in-sharepoint"></a>Что такое свойства профилей пользователей в SharePoint
<a name="bkmk_WhatIs"> </a>

Свойства пользователя и свойств профиля пользователя представлены сведения о пользователей SharePoint, такие как отображаемое имя, электронной почты, должность и других бизнес и личные сведения. В клиентских API доступа к этим свойствам из объекта  [PersonProperties](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PersonProperties.aspx) и его свойство [UserProfileProperties](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PersonProperties.UserProfileProperties.aspx) . Свойство [UserProfileProperties](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PersonProperties.UserProfileProperties.aspx) содержит все свойства профиля пользователя, но объект [PersonProperties](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PersonProperties.aspx) содержит часто используемые свойства (например, [AccountName](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PersonProperties.AccountName.aspx) , [DisplayName](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PersonProperties.DisplayName.aspx) и [Email](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PersonProperties.Email.aspx) ), которые легче доступа.
  
    
    
Объект  [PeopleManager](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.aspx) содержит следующие методы, которые можно использовать для получения свойств пользователей и свойств профилей пользователей с помощью клиентской объектной модели .NET:
  
    
    

- Метод  [GetMyProperties](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.GetMyProperties.aspx) и метод [GetPropertiesFor](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.GetPropertiesFor.aspx) возвращает объект [PersonProperties](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PersonProperties.aspx) .
    
  
- Метод  [GetUserProfilePropertiesFor](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.GetUserProfilePropertiesFor.aspx) и метод [GetUserProfilePropertyFor](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.GetUserProfilePropertyFor.aspx) возвращаемые значения пользователя, задаваемые свойства профиля.
    
  
Свойства профиля пользователя из клиентских API находятся только для чтения (за исключением изображение профиля можно изменить с помощью метода  [PeopleManager.SetMyProfilePicture](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.SetMyProfilePicture.aspx) ). Если вы хотите изменить другие свойства профиля пользователя, необходимо использовать серверной объектной модели.
  
    
    

> **Примечание:** Версия клиентского объекта [UserProfile](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.UserProfile.aspx) , не содержит все свойства пользователя как версию на сервере. Однако клиентская версия предоставляет методы для создания личного сайта для текущего пользователя. Чтобы получить клиентские [UserProfile](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.UserProfile.aspx) для текущего пользователя, используйте метод [ProfileLoader.GetUserProfile](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.ProfileLoader.GetUserProfile.aspx) .
  
    
    

Дополнительные сведения о работе с профилями можно [работы с профилями пользователей в SharePoint](work-with-user-profiles-in-sharepoint.md).
  
    
    

## <a name="prerequisites-for-setting-up-your-development-environment-to-retrieve-user-profile-properties-by-using-the-sharepoint-net-client-object-model"></a>Необходимые условия для настройки среды разработки для извлечения свойств профиля пользователя с помощью объектной модели клиента SharePoint .NET
<a name="bk_Prereqs"> </a>

Создание консольного приложения, использующего клиентской объектной модели .NET для извлечения свойств профиля пользователя, необходимо следующее:
  
    
    

- SharePoint с профилями для текущего пользователя и целевого пользователя;
    
  
- Visual Studio 2012
    
  
- разрешения уровня **Полный доступ** для подключения к приложению-службе профиля текущего пользователя.
    
  

> **Примечание:** При разработке не на компьютере, на котором работает SharePoint, загрузить [Клиентские компоненты SharePoint](http://www.microsoft.com/en-us/download/details.aspx?id=35585) , содержащий клиентскую сборку SharePoint.
  
    
    


## <a name="create-the-console-application-that-retrieves-user-profile-properties-by-using-the-sharepoint-net-client-object-model"></a>Создайте консольное приложение, которое извлекает свойства профилей пользователей с помощью клиентской объектной модели SharePoint .NET
<a name="bk_RetrieveProps"> </a>


1. На компьютере для разработки откройте Visual Studio и выберите **файл**, **Создать**, **проект**.
    
  
2. В верхней части диалогового окна **Новый проект** выберите **.NET Framework 4.5** в раскрывающемся списке.
    
  
3. На основе шаблонов проектов выберите **Windows** и выберите **Консольное приложение**.
    
  
4. Назовите проект UserProfilesCSOMи затем нажмите кнопку **ОК**.
    
  
5. Добавьте ссылки на следующие сборки:
    
  - **Microsoft.SharePoint.Client**
  - **Microsoft.SharePoint.ClientRuntime**  
  - **Microsoft.SharePoint.Client.UserProfiles**
    
  
6. В методе **Main** определите переменные для URL-адрес сервера и имя конечного пользователя, как показано в следующем коде.
    
```cs
const string serverUrl = "http://serverName/";
const string targetUser = "domainName\\\\userName";
```

   > Примечание: Не забудьте заменить `http://serverName/` и `domainName\\\\userName` заполнитель значения, прежде чем запускать код.

7. Инициализация контекста клиента SharePoint, как показано в следующем коде.
    
```cs
ClientContext clientContext = new ClientContext(serverUrl);
```

8. Получение свойств конечного пользователя из объекта **PeopleManager**, как показано в следующем коде.
    
```cs
PeopleManager peopleManager = new PeopleManager(clientContext);
PersonProperties personProperties = peopleManager.GetPropertiesFor(targetUser);
```

   Объект **personProperties**  это объект клиента. Некоторые клиентские объекты не содержат данных до их инициализации. Например значения свойств объекта **personProperties** недоступны до его инициализации. При попытке доступа к свойству до его инициализации, вы получаете исключение **PropertyOrFieldNotInitializedException**.
    
  
9. Для инициализации объекта **personProperties**, регистрация запроса, которую требуется запустить и выполнить запрос на сервере, как показано в следующем коде.
    
```cs
clientContext.Load(personProperties, p => p.AccountName, p => p.UserProfileProperties);
clientContext.ExecuteQuery();
```

   При вызове метода **Load** (или метод **LoadQuery** ), переданных в объект, который необходимо получить или изменить. В этом примере вызов метода **Load** передает необязательных параметров для фильтрации запроса. Лямбда-выражения, запрашивающих свойство **AccountName** и свойство **UserProfileProperties** объекта **personProperties** используются параметры.
    
   >Совет: Чтобы уменьшить сетевой трафик, запросите только свойства, которые вы хотите работать с при вызове метода **Load** . Кроме того при работе с несколькими объектами групповой нескольких вызовы метода **нагрузки** по возможности перед вызовом метода **ExecuteQuery** .

10. Выполните итерацию по свойств профилей пользователей и чтение имя и значение каждого свойства, как показано в следующем коде.
    
```cs
foreach (var property in personProperties.UserProfileProperties)
{
    Console.WriteLine(string.Format("{0}: {1}", 
        property.Key.ToString(), property.Value.ToString()));
}
```


## <a name="code-example-retrieving-all-user-profile-properties-by-using-the-sharepoint-net-client-object-model"></a>Пример кода: получение всех свойств профиля пользователя с помощью клиентской объектной модели SharePoint .NET
<a name="SP15UserProf_codeexample1"> </a>

В следующем примере кода показано, как получить и выполнять итерацию по всем свойства профиля пользователя конечного пользователя, как описано в  [предыдущей процедуре](how-to-retrieve-user-profile-properties-by-using-the-net-client-object-model-in.md#bk_RetrieveProps).
  
    
    

> **Примечание:** Замените `http://serverName/` и `domainName\\\\userName` заполнитель значения, прежде чем запускать код.
  
    
    


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


## <a name="code-example-retrieving-user-profile-properties-of-people-who-are-following-me-by-using-the-sharepoint-net-client-object-model"></a>Пример кода: получение свойств профиля пользователя людей, которые отслеживаются меня с помощью клиентской объектной модели SharePoint .NET
<a name="SP15UserProfilescodeInApp"> </a>

В следующем примере кода показано, как получить Надстройка SharePoint свойства профиля пользователя по пользователей, которые вы подписались.
  
    
    

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


## <a name="code-example-retrieving-a-set-of-user-profile-properties-by-using-the-sharepoint-net-client-object-model"></a>Пример кода: получение набор свойств профилей пользователей с помощью клиентской объектной модели SharePoint .NET
<a name="SP15UserProfilescode2"> </a>

В следующем примере кода показано, как получить определенный набор свойств профилей пользователей для конечного пользователя.
  
    
    

> **Примечание:** Чтобы получить значение для свойства профиля только один пользователь, используйте метод [GetUserProfilePropertyFor](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.GetUserProfilePropertyFor.aspx) .
  
    
    

В отличие от предыдущего примера кода, который извлекает объект  [PersonProperties](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PersonProperties.aspx) для конечного пользователя в этом примере вызов метода [PeopleManager.GetUserProfilePropertiesFor](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.GetUserProfilePropertiesFor.aspx) и передает в объект [UserProfilePropertiesForUser](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.UserProfilePropertiesForUser.aspx) , который указывает конечного пользователя и свойств профилей пользователей для извлечения. [GetUserProfilePropertiesFor](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.GetUserProfilePropertiesFor.aspx) возвращает коллекцию **IEnumerable<string>**, который содержит значения свойств, которые можно указать.
  
    
    

> **Примечание:** Замените `http://serverName/` и `domainName\\\\userName` заполнитель значения, прежде чем запускать код.
  
    
    




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


## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="bk_addresources"> </a>


-  [Работа с профилями пользователей в SharePoint](work-with-user-profiles-in-sharepoint.md)
    
  
-  [Инструкции. Получение свойств профиля пользователя с помощью объектной модели JavaScript в SharePoint](how-to-retrieve-user-profile-properties-by-using-the-javascript-object-model-in.md)
    
  
-  [Инструкции. Работа с профилями пользователей и организации с использованием объектной модели сервера в SharePoint](how-to-work-with-user-profiles-and-organization-profiles-by-using-the-server-obj.md)
    
  
-  [Microsoft.SharePoint.Client.UserProfiles](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.aspx)
    
  

