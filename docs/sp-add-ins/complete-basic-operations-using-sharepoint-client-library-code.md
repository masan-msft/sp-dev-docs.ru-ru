---
title: "Выполнение базовых операций с использованием кода клиентской библиотеки SharePoint"
description: "Узнайте, как создавать код для выполнения основных операций с клиентской объектной моделью SharePoint .NET Framework (CSOM)."
ms.date: 12/13/2017
ms.prod: sharepoint
ms.openlocfilehash: 5348dccef032a42af056826626d7d8598360a983
ms.sourcegitcommit: 28690b54f1ef7c811d64393d2eaaff0a8635cc72
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/14/2017
---
# <a name="complete-basic-operations-using-sharepoint-client-library-code"></a>Выполнение базовых операций с использованием кода клиентской библиотеки SharePoint


С помощью клиентской объектной модели SharePoint (CSOM) вы можете получать и изменять данные в SharePoint, а также управлять ими. В SharePoint доступ к CSOM осуществляется несколькими путями: 

- через распространяемые сборки .NET Framework; 
- библиотеку JavaScript;
- конечные точки REST и OData;
- сборки Windows Phone;
- распространяемые сборки Silverlight.
    
Дополнительные сведения о наборах API, доступных на платформе SharePoint, см. в статье [Выбор правильного набора API в SharePoint](../general-development/choose-the-right-api-set-in-sharepoint.md). 

В этой статье описано, как выполнять базовые операции с использованием объектной модели .NET Framework, доступной в виде распространяемого пакета в Центре загрузки Майкрософт (найти его можно по запросу "SharePoint Server 2013 Client Components SDK" или "SharePoint Online Client Components SDK"). 

Сведения об использовании других клиентских API см. в следующих статьях:

- [Выполнение базовых операций с использованием кода библиотеки JavaScript в SharePoint](complete-basic-operations-using-javascript-library-code-in-sharepoint.md)
- [Выполнение базовых операций с использованием конечных точек REST в SharePoint](complete-basic-operations-using-sharepoint-rest-endpoints.md)
- [Создание приложений Windows Phone с доступом к SharePoint](../general-development/build-windows-phone-apps-that-access-sharepoint.md)
- [Использование объектной модели Silverlight](http://msdn.microsoft.com/library/cea7829d-f360-4052-8b76-91d90bcefd2a%28Office.15%29.aspx) в пакете SDK для SharePoint 2010

<a name="BasicOps_SPCSOMOps"> </a>

## <a name="basic-operations-with-the-sharepoint-net-client-object-model"></a>Основные операции с клиентской объектной моделью .NET в SharePoint

В приведенных ниже разделах описаны задачи, которые вы можете выполнять программным путем. Они включают примеры кода на языке C#, в которых демонстрируются операции CSOM.

Когда вы создаете проект **Надстройка для SharePoint** в Visual Studio 2012, ссылки на сборки .NET Framework, **Microsoft.SharePoint.Client.Runtime.dll** и **Microsoft.SharePoint.Client.dll** автоматически добавляются в проект. Для других проектов, таких как приложения .NET Framework или консольные приложения, нужно добавить эти ссылки вручную. Эти файлы можно найти на любом сервере SharePoint, открыв папку %ProgramFiles%\Common Files\Microsoft Shared\web server extensions\15\ISAPI.

Во всех этих примерах предполагается, что код находится в файле кода программной части для веб-страницы Microsoft ASP.NET. В файл кода необходимо добавить указанную ниже инструкцию **using**.

```
using Microsoft.SharePoint.Client;
```

Если не указано иное, предполагается, что каждый из этих примеров относится к методу, не содержащему параметров и определенному в классе страницы. Кроме того, `label1`, `label2` и т. д. — это имена объектов [Label](https://msdn.microsoft.com/ru-RU/library/620f4ses) на странице.
 
> [!NOTE] 
> Создавая размещаемую у поставщика надстройку SharePoint с использованием веб-приложения ASP.NET и добавляя ссылку на сборку в проект веб-приложения в Visual Studio, установите для свойства **Копировать локально** значение **True**, если не знаете, установлена ли сборка на веб-сервере, и не можете ее установить до развертывания надстройки. 

> Платформа .NET Framework установлена для веб-ролей Microsoft Azure и службы приложений Azure. Но сборки клиента SharePoint, а также платформы и расширения управляемого кода Майкрософт не установлены. Инструменты разработчика Office для Visual Studio 2012 автоматически добавляют ссылки на некоторые сборки, часто используемые в надстройках SharePoint, и устанавливают свойство **Копировать локально**.

<a name="BasicOps_SPWebTasks"> </a>

## <a name="sharepoint-website-tasks"></a>Задачи, связанные с веб-сайтом SharePoint

В этих примерах показано, как использовать модель CSOM .NET Framework для выполнения задач, связанных с веб-сайтами.

### <a name="retrieve-the-properties-of-a-website"></a>Получите свойства веб-сайта

Следующий код служит для получения названия веб-сайта SharePoint.


```C#

// Starting with ClientContext, the constructor requires a URL to the 
// server running SharePoint. 
ClientContext context = new ClientContext("http://SiteUrl"); 

// The SharePoint web at the URL.
Web web = context.Web; 

// We want to retrieve the web's properties.
context.Load(web); 

// Execute the query to the server.
context.ExecuteQuery(); 

// Now, the web's properties are available and we could display 
// web properties, such as title. 
label1.Text = web.Title;

```

<br/>

### <a name="retrieve-only-selected-properties-of-a-website"></a>Получение определенных свойств веб-сайта

Иногда клиенту нужны только несколько свойств объекта. Для CSOM .NET Framework SharePoint не требуется получать с сервера все свойства объекта — вы можете использовать анонимные методы, например лямбда-выражения, для запроса определенных свойств. Клиентская библиотека запрашивает на сервере только эти свойства, и сервер отправляет клиенту только эти свойства. Этот метод позволяет уменьшить объем ненужных данных, передаваемых между клиентом и сервером. Он также удобен, когда у пользователя нет разрешений на доступ к одному или нескольким неиспользуемым свойствам объекта. 

Обратите внимание на то, что нужно добавить инструкцию **using** для пространства имен [System.Linq](https://msdn.microsoft.com/ru-RU/library/bb336768).

```C#
// Starting with ClientContext, the constructor requires a URL to the 
// server running SharePoint. 
ClientContext context = new ClientContext("http://SiteUrl"); 

// The SharePoint web at the URL.
Web web = context.Web; 

// We want to retrieve the web's title and description. 
context.Load(web, w => w.Title, w => w.Description); 

// Execute the query to server.
context.ExecuteQuery(); 

// Now, only the web's title and description are available. If you 
// try to print out other properties, the code will throw 
// an exception because other properties are not available. 
label1.Text = web.Title;
label1.Text = web. Description;

```

> [!NOTE] 
> Если вы пытаетесь получить доступ к другим свойствам, код выдает исключение, потому что остальные свойства недоступны.
 
<br/>

### <a name="write-to-websites-properties"></a>Запись значений для свойств веб-сайта

В этом примере показано, как записать значения для свойств веб-сайта.


```C#
// Starting with ClientContext, the constructor requires a URL to the 
// server running SharePoint. 
ClientContext context = new ClientContext("http://SiteUrl"); 

// The SharePoint web at the URL.
Web web = context.Web; 

web.Title = "New Title"; 
web.Description = "New Description"; 

// Note that the web.Update() does not trigger a request to the server
// because the client library until ExecuteQuery() is called. 
web.Update(); 

// Execute the query to server.
context.ExecuteQuery(); 

```
 
<br/>

### <a name="create-a-new-sharepoint-website"></a>Создание веб-сайта SharePoint

В этом примере показано, как создать дочерний сайт текущего веб-сайта SharePoint. Используйте класс **WebCreationInformation** для создания нового веб-сайта. Нужно также добавить инструкцию **using** для пространств имен [System.Collections.Generic](https://msdn.microsoft.com/ru-RU/library/0sbxh9x2) и [System.Text](https://msdn.microsoft.com/ru-RU/library/x76y3wky).

```C#
// Starting with ClientContext, the constructor requires a URL to the 
// server running SharePoint. 
ClientContext context = new ClientContext("http://SiteUrl"); 

WebCreationInformation creation = new WebCreationInformation(); 
creation.Url = "web1"; 
creation.Title = "Hello web1"; 
Web newWeb = context.Web.Webs.Add(creation); 

// Retrieve the new web information. 
context.Load(newWeb, w => w.Title); 
context.ExecuteQuery(); 

label1.Text = newWeb.Title; 

```

<br/>

<a name="BasicOps_SPListTasks"> </a>

## <a name="sharepoint-list-tasks"></a>Задачи, связанные со списками SharePoint

В этих примерах показано, как использовать модель CSOM .NET Framework для выполнения задач, связанных со списками.

### <a name="retrieve-all-sharepoint-lists-in-a-website"></a>Получение всех списков SharePoint на сайте

В этом примере показано, как извлечь все списки SharePoint на веб-сайте SharePoint. Чтобы выполнить компиляцию, нужно добавить инструкцию **using** для пространства имен [System.Linq](http://msdn.microsoft.com/ru-RU/library/bb336768).

```C#
// Starting with ClientContext, the constructor requires a URL to the 
// server running SharePoint. 
ClientContext context = new ClientContext("http://SiteUrl"); 

// The SharePoint web at the URL.
Web web = context.Web; 

// Retrieve all lists from the server. 
context.Load(web.Lists, 
             lists => lists.Include(list => list.Title, // For each list, retrieve Title and Id. 
                                    list => list.Id)); 

// Execute query. 
context.ExecuteQuery(); 

// Enumerate the web.Lists. 
foreach (List list in web.Lists) 
{ 
    label1.Text = label1.Text + ", " + list.Title; 
} 

```

<br/>

> [!NOTE] 
> Вместо свойства **web.Lists** можно использовать метод **LoadQuery**, чтобы хранить возвращаемое значения в другой коллекции. Вам также потребуется добавить инструкцию **using** для пространств имен [System.Collections.Generic](http://msdn.microsoft.com/ru-RU/library/0sbxh9x2) и [System.Linq](http://msdn.microsoft.com/ru-RU/library/bb336768). Добавьте также псевдоним в инструкцию using для пространства имен **Microsoft.SharePoint.Client**, чтобы однозначно ссылаться на его классы. Пример: `using SP = Microsoft.SharePoint.Client;`.
 
<br/>

```C#
// Starting with ClientContext, the constructor requires a URL to the 
// server running SharePoint. 
ClientContext context = new ClientContext("http://SiteUrl"); 

// The SharePoint web at the URL.
Web web = context.Web; 

// Retrieve all lists from the server, and put the return value in another 
// collection instead of the web.Lists. 
IEnumerable<SP.List> result = context.LoadQuery(web.Lists.Include( // For each list, retrieve Title and Id.
                                                                   list => list.Title, 
                                                                   list => list.Id)); 

// Execute query. 
context.ExecuteQuery(); 

// Enumerate the result. 
foreach (List list in web.Lists) 
{ 
    label1.Text = label1.Text + ", " + list.Title; 
} 

```

<br/>

### <a name="create-and-update-a-sharepoint-list"></a>Создание и обновление списка SharePoint

В этом примере список SharePoint создается и обновляется с помощью класса **ListCreationInformation**.

```C#
// Starting with ClientContext, the constructor requires a URL to the 
// server running SharePoint. 
ClientContext context = new ClientContext("http://SiteUrl"); 

// The SharePoint web at the URL.
Web web = context.Web; 

ListCreationInformation creationInfo = new ListCreationInformation(); 
creationInfo.Title = "My List"; 
creationInfo.TemplateType = (int)ListTemplateType.Announcements; 
List list = web.Lists.Add(creationInfo); 
list.Description = "New Description"; 

list.Update(); 
context.ExecuteQuery(); 

```

<br/>

### <a name="delete-a-sharepoint-list"></a>Удаление списка SharePoint

В этом примере удаляется список SharePoint.

```C#
// Starting with ClientContext, the constructor requires a URL to the 
// server running SharePoint. 
ClientContext context = new ClientContext("http://SiteUrl"); 

// The SharePoint web at the URL.
Web web = context.Web; 

List list = web.Lists.GetByTitle("My List"); 
list.DeleteObject(); 

context.ExecuteQuery();  

```

<br/>

### <a name="add-a-field-to-a-sharepoint-list"></a>Добавление поля в список SharePoint

В этом примере показано, как добавить поле в список SharePoint. Добавьте псевдоним в инструкцию using для пространства имен **Microsoft.SharePoint.Client**, чтобы однозначно ссылаться на его классы. Пример: `using SP = Microsoft.SharePoint.Client;`.
 
> [!NOTE] 
> В этом примере для приведения типа используется метод **context.CastTo**. Перед выполнением запроса клиентская библиотека не знает тип возвращаемого объекта, и единственным возможным типом является **SharePoint.Field**. Если вы знаете тип объекта, можете выполнить его приведение, используя метод **ClientContext.CastTo<RealType>**.

```C#
// Starting with ClientContext, the constructor requires a URL to the 
// server running SharePoint. 
ClientContext context = new ClientContext("http://SiteUrl"); 

SP.List list = context.Web.Lists.GetByTitle("Announcements"); 

SP.Field field = list.Fields.AddFieldAsXml("<Field DisplayName='MyField2' Type='Number' />", 
                                           true, 
                                           AddFieldOptions.DefaultValue); 
SP.FieldNumber fldNumber = context.CastTo<FieldNumber>(field); 
fldNumber.MaximumValue = 100; 
fldNumber.MinimumValue = 35; 
fldNumber.Update(); 

context.ExecuteQuery();  

```

<br/>

<a name="BasicOps_SPListItemTasks"> </a>

## <a name="sharepoint-list-item-tasks"></a>Задачи, связанные с элементами списков SharePoint

В этих примерах демонстрируется использование модели CSOM .NET Framework для выполнения задач, связанных с элементами списков.

### <a name="retrieve-items-from-a-sharepoint-list"></a>Получение элементов из списка SharePoint

В этом примере показано, как извлечь элементы из списка SharePoint. Вам также потребуется добавить инструкцию **using** для пространства имен **Microsoft.SharePoint.Client.QueryExpression**.
 
> [!NOTE] 
> С помощью свойства **FolderServerRelativeUrl** вы можете ограничить возвращаемые элементы только теми, которые находятся в указанной папке.

```C#
// Starting with ClientContext, the constructor requires a URL to the 
// server running SharePoint. 
ClientContext context = new ClientContext("http://SiteUrl"); 

// Assume the web has a list named "Announcements". 
List announcementsList = context.Web.Lists.GetByTitle("Announcements"); 

// This creates a CamlQuery that has a RowLimit of 100, and also specifies Scope="RecursiveAll" 
// so that it grabs all list items, regardless of the folder they are in. 
CamlQuery query = CamlQuery.CreateAllItemsQuery(100); 
ListItemCollection items = announcementsList.GetItems(query); 

// Retrieve all items in the ListItemCollection from List.GetItems(Query). 
context.Load(items); 
context.ExecuteQuery(); 
foreach (ListItem listItem in items) 
{ 
    // We have all the list item data. For example, Title. 
    label1.Text = label1.Text + ", " + listItem["Title"]; 
} 

```

<br/>

### <a name="create-a-new-list-item"></a>Создание элемента списка

В этом примере список SharePoint создается с помощью класса **ListItemCreationInformation**.

```C#
// Starting with ClientContext, the constructor requires a URL to the 
// server running SharePoint. 
ClientContext context = new ClientContext("http://SiteUrl"); 

// Assume that the web has a list named "Announcements". 
List announcementsList = context.Web.Lists.GetByTitle("Announcements"); 

// We are just creating a regular list item, so we don't need to 
// set any properties. If we wanted to create a new folder, for 
// example, we would have to set properties such as 
// UnderlyingObjectType to FileSystemObjectType.Folder. 
ListItemCreationInformation itemCreateInfo = new ListItemCreationInformation(); 
ListItem newItem = announcementsList.AddItem(itemCreateInfo); 
newItem["Title"] = "My New Item!"; 
newItem["Body"] = "Hello World!"; 
newItem.Update(); 

context.ExecuteQuery();  

```

<br/>

### <a name="update-a-list-item"></a>Обновление элемента списка

В этом примере обновляется элемент списка SharePoint.

```C#
// Starting with ClientContext, the constructor requires a URL to the 
// server running SharePoint. 
ClientContext context = new ClientContext("http://SiteUrl"); 

// Assume that the web has a list named "Announcements". 
List announcementsList = context.Web.Lists.GetByTitle("Announcements"); 

// Assume there is a list item with ID=1. 
ListItem listItem = announcementsList.GetItemById(1); 

// Write a new value to the Body field of the Announcement item.
listItem["Body"] = "This is my new value!!"; 
listItem.Update(); 

context.ExecuteQuery();  

```

<br/>

### <a name="delete-a-list-item"></a>Удаление элемента списка

В этом примере удаляется элемент списка SharePoint.

```C#
// Starting with ClientContext, the constructor requires a URL to the 
// server running SharePoint. 
ClientContext context = new ClientContext("http://SiteUrl"); 

// Assume that the web has a list named "Announcements". 
List announcementsList = context.Web.Lists.GetByTitle("Announcements"); 

// Assume that there is a list item with ID=2. 
ListItem listItem = announcementsList.GetItemById(2); 
listItem.DeleteObject(); 

context.ExecuteQuery(); } 

```

<br/>

<a name="BasicOps_SPFieldTasks"> </a>

## <a name="sharepoint-field-tasks"></a>Задачи, связанные с полями SharePoint

В этих примерах показано, как использовать модель CSOM .NET Framework в SharePoint для выполнения задач, связанных с полями. 

### <a name="retrieve-all-of-the-fields-in-a-list"></a>Получение всех полей в списке

В этом примере показано, как получить все поля в списке SharePoint. Кроме того, добавьте псевдоним в инструкцию **using** для пространства имен **Microsoft.SharePoint.Client**, чтобы однозначно ссылаться на его классы. Пример: `using SP = Microsoft.SharePoint.Client;`.

```C#
// Starting with ClientContext, the constructor requires a URL to the 
// server running SharePoint. 
ClientContext context = new ClientContext("http://SiteUrl"); 

SP.List list = context.Web.Lists.GetByTitle("Shared Documents"); 
context.Load(list.Fields); 

// We must call ExecuteQuery before enumerate list.Fields. 
context.ExecuteQuery(); 

foreach (SP.Field field in list.Fields) 
{ 
    label1.Text = label1.Text + ", " + field.InternalName;
} 

```

<br/>

### <a name="retrieve-a-specific-field-from-the-list"></a>Получение определенного поля из списка

Если вы хотите получить информацию о конкретном поле, используйте метод **Fields.GetByInternalNameOrTitle**. Тип возвращаемого значения этого метода — **Field**. Перед выполнением запроса клиент не знает тип объекта, и синтаксис C# недоступен для его приведения к производному типу. Поэтому используйте для его приведения метод **ClientContext.CastTo**, который дает клиентской библиотеке указание воссоздать объект. Нужно также добавить инструкцию **using** для пространства имен [System.Collections.Generic](http://msdn.microsoft.com/ru-RU/library/0sbxh9x2). Кроме того, добавьте псевдоним в инструкцию **using** для пространства имен **Microsoft.SharePoint.Client**, чтобы однозначно ссылаться на его классы. Пример: `using SP = Microsoft.SharePoint.Client;`.
 
> [!NOTE] 
> Метод **GetByInternalNameOrTitle**, используемый в этом примере, является удаленным. Он не использует данные из клиентской коллекции, даже если она уже заполнена.

```C#
// Starting with ClientContext, the constructor requires a URL to the 
// server running SharePoint. 
ClientContext context = new ClientContext("http://SiteUrl"); 

SP.List list = context.Web.Lists.GetByTitle("Shared Documents"); 
SP.Field field = list.Fields.GetByInternalNameOrTitle("Title"); 
FieldText textField = context.CastTo<FieldText>(field); 
context.Load(textField); 
context.ExecuteQuery(); 

// Now, we can access the specific text field properties. 
label1.Text = textField.MaxLength; 

```

<br/>

<a name="BasicOps_SPSecurityTasks"> </a>

## <a name="sharepoint-user-tasks"></a>Задачи, связанные с пользователями SharePoint

Вы можете использовать модель CSOM .NET Framework в SharePoint для управления пользователями и группами SharePoint, а также безопасностью пользователей. 

### <a name="add-a-user-to-a-sharepoint-group"></a>Добавление пользователя в группу SharePoint

В этом примере в группу SharePoint с именем Members добавляется пользователь и некоторые сведения о нем.

```C#
// Starting with ClientContext, the constructor requires a URL to the 
// server running SharePoint. 
ClientContext context = new ClientContext("http://SiteUrl"); 

GroupCollection siteGroups = context.Web.SiteGroups; 

// Assume that there is a "Members" group, and the ID=5. 
Group membersGroup = siteGroups.GetById(5); 

// Let's set up the new user info. 
UserCreationInformation userCreationInfo = new UserCreationInformation(); 
userCreationInfo.Email = "user@domain.com"; 
userCreationInfo.LoginName = "domain\\user"; 
userCreationInfo.Title = "Mr User"; 

// Let's add the user to the group. 
User newUser = membersGroup.Users.Add(userCreationInfo); 

context.ExecuteQuery();  

```

<br/>

### <a name="retrieve-all-users-in-a-sharepoint-group"></a>Получение всех пользователей из группы SharePoint

В этом примере извлекаются сведения о всех пользователях в группе SharePoint с именем Members.

```C#
// Starting with ClientContext, the constructor requires a URL to the 
// server running SharePoint. 
ClientContext context = new ClientContext("http://SiteUrl"); 

GroupCollection siteGroups = context.Web.SiteGroups; 

// Assume that there is a "Members" group, and the ID=5. 
Group membersGroup = siteGroups.GetById(5); 
context.Load(membersGroup.Users); 
context.ExecuteQuery(); 

foreach (User member in membersGroup.Users) 
{ 
    // We have all the user info. For example, Title. 
    label1.Text = label1.Text + ", " + member.Title; 
}  

```

<br/>

### <a name="create-a-role"></a>Создание роли

В этом примере создается роль, имеющая разрешения на создание оповещений и управление ими.

```C#
// Starting with ClientContext, the constructor requires a URL to the 
// server running SharePoint. 
ClientContext context = new ClientContext("http://SiteUrl"); 

BasePermissions perm = new BasePermissions(); 
perm.Set(PermissionKind.CreateAlerts); 
perm.Set(PermissionKind.ManageAlerts); 

RoleDefinitionCreationInformation creationInfo = new RoleDefinitionCreationInformation(); 
creationInfo.BasePermissions = perm; 
creationInfo.Description = "A role with create and manage alerts permission"; 
creationInfo.Name = "Alert Manager Role"; 
creationInfo.Order = 0; 
RoleDefinition rd = context.Web.RoleDefinitions.Add(creationInfo); 

context.ExecuteQuery();  

```

<br/>

### <a name="add-a-user-to-a-role"></a>Добавление пользователя к роли

В этом примере к роли добавляется пользователь.

```C#
// Starting with ClientContext, the constructor requires a URL to the 
// server running SharePoint. 
ClientContext context = new ClientContext("http://SiteUrl"); 

// Assume that we have a SiteUser with Login user. 
Principal user = context.Web.SiteUsers.GetByLoginName(@"domain\user"); 

// Assume that we have a RoleDefinition named "Read". 
RoleDefinition readDef = context.Web.RoleDefinitions.GetByName("Read"); 
RoleDefinitionBindingCollection roleDefCollection = new RoleDefinitionBindingCollection(context); 
roleDefCollection.Add(readDef); 
RoleAssignment newRoleAssignment = context.Web.RoleAssignments.Add(user, roleDefCollection); 

context.ExecuteQuery();  

```

<br/>

<a name="Best"> </a>

## <a name="rules-and-best-practices-for-using-the-sharepoint-net-client-object-model"></a>Правила и рекомендации по клиентской объектной модели .NET в SharePoint

В этих примерах демонстрируются некоторые важные рекомендации и требования, которые следует соблюдать при использовании модели CSOM .NET Framework в SharePoint.

### <a name="call-clientcontextexecutequery-before-accessing-any-value-properties"></a>Вызов метода ClientContext.ExecuteQuery перед доступом к свойствам значений

Модель CSOM SharePoint .NET Framework требует использования шаблона программирования наподобие SQL: необходимо объявить запрос и выполнить его перед доступом к данным. Например, при выполнении следующего кода, который пытается отобразить название веб-сайта SharePoint, выдается исключение.


```C#
// Starting with ClientContext, the constructor requires a URL to the 
// server running SharePoint. 
ClientContext context = new ClientContext("http://SiteUrl"); 

Web web = context.Web; 
label1.Text = web.Title;  

```

<br/>

Сбой произойдет по той причине, что в коде CSOM .NET Framework в SharePoint необходимо выполнить следующие действия:

- создать прямой запрос SQL или хранимую процедуру;
- выполнить запрос SQL;
- прочитать результаты из SQL.
    
В модели CSOM SharePoint .NET Framework при вызове метода создается запрос. Запросы накапливаются и не отправляются на сервер, пока не будет вызван метод **ExecuteQuery**. 

Ниже показано код, необходимый для отображения названия веб-сайта. Кроме того, нужно добавить инструкцию **using** для пространства имен [System.Linq](http://msdn.microsoft.com/ru-RU/library/bb336768). Добавьте также псевдоним в инструкцию **using** для пространства имен **Microsoft.SharePoint.Client**, чтобы однозначно ссылаться на его классы. Пример: `using SP = Microsoft.SharePoint.Client;`.
 

```C#
// Starting with ClientContext, the constructor requires a URL to the 
// server running SharePoint. 
ClientContext context = new ClientContext("http://SiteUrl"); 

Web web = context.Web; 

context.Load(web, w => w.Title); 

context.ExecuteQuery(); 

label1.Text = web.Title;   

```

<br/>

Отличие состоит в том, что добавляются указанные ниже строки. Первая из них создает запрос на получение свойства **Title**. Вторая строка выполняет запрос. 

```
context.Load(web, w => w.Title); 
context.ExecuteQuery(); 

```

<br/>

### <a name="do-not-use-value-objects-returned-from-methods-or-properties-in-the-same-query"></a>Не используйте объекты значений, возвращенные методами или свойствами, в том же запросе

Объект значения, возвращаемый методом или свойством, можно использовать только после выполнения запроса. Например, приведенный ниже код пытается создать список SharePoint с тем же названием, что и у родительского веб-сайта, но выдается исключение. 

```C#
// Starting with ClientContext, the constructor requires a URL to the 
// server running SharePoint. 
ClientContext context = new ClientContext("http://SiteUrl"); 

Web web = context.Web; 
ListCreationInformation creationInfo = new ListCreationInformation(); 
creationInfo.Description = web.Title; 
creationInfo.Title = web.Title; 
List newList = web.Lists.Add(creationInfo);  

```

<br/>

Исключение выдается, так как свойство недоступно до выполнения запроса. В SQL можно объявить локальную переменную для хранения значения `web.Title` и использовать ее для создания сайта. В клиентской библиотеке создать локальную переменную нельзя. Вам нужно разбить действие на два отдельных запроса, как показано в приведенном ниже примере. Кроме того, нужно добавить инструкцию **using** для пространства имен [System.Linq](http://msdn.microsoft.com/ru-RU/library/bb336768). Добавьте также псевдоним в инструкцию using для пространства имен **Microsoft.SharePoint.Client**, чтобы однозначно ссылаться на его классы. Пример: `using SP = Microsoft.SharePoint.Client;`.

```C#
// Starting with ClientContext, the constructor requires a URL to the 
// server running SharePoint. 
ClientContext context = new ClientContext("http://SiteUrl"); 

Web web = context.Web; 

context.Load(web, w => w.Title); 

context.ExecuteQuery(); 

ListCreationInformation creationInfo = new ListCreationInformation(); 
creationInfo.Description = web.Description; 
creationInfo.Title = web.Title; 
SP.List newList = web.Lists.Add(creationInfo); 

context.ExecuteQuery();  

```

<br/>

Отличие заключается в следующих трех строках:

```C#
context.Load(web, w => w.Title); 
context.ExecuteQuery(); 
...
context.ExecuteQuery(); 

```

<br/>

### <a name="using-methods-or-properties-that-return-client-objects-in-another-method-call-in-the-same-query"></a>Использование методов или свойств, возвращающих клиентские объекты, в вызове другого метода в том же запросе

В отличие от объекта значения, клиентский объект можно использовать в вызове другого метода в том же запросе. 

В удаленной среде .NET объект значения представляет собой класс или структуру, маршалируемую по значению, а клиентский объект класс или структуру, маршалируемую по ссылке. Например, **ListItem** это клиентский объект, а **UrlFieldValue** и другие значения полей это объекты значений.

В клиентской библиотеке соответствующий объект сервера имеет атрибут `[ClientCallable(ValueObject = true)]`. Эти значения могут иметь только свойства и не иметь методов. Примитивные типы, такие как строки и целочисленные значения, обрабатываются как объекты значений. Для всех значений выполняется маршалинг между клиентом и сервером. Значение **ValueObject** по умолчанию — **false**. 

Альтернативой объекту значения является клиентский объект. Если соответствующий серверный объект имеет атрибут **[ClientCallable(ValueObject = false)]**, объект является клиентским. Процесс создания клиентских объектов отслеживается. В реализации клиентской библиотеки для этого используется класс **ObjectPath**. Например, имеется следующий код.

```C#
ClientContext context = new ClientContext("http://SiteUrl"); 
Web web = context.Web; 
SP.List list = web.Lists.GetByTitle("Announcements"); 

```

Мы знаем, что список создается следующим образом:

- Свойство **Web** извлекается из контекста.
- Из полученного выше свойства извлекается свойство **Lists**.
- Для полученного выше свойства вызывается метод **GetByTitle** с параметром _Announcements_.
    
 
Когда модель CSOM SharePoint .NET Framework передает эту информацию на сервер, вы можете воссоздать объект на сервере. В клиентской библиотеке вы можете отслеживать **ObjectPath**, созданный объектом клиента. Вы знаете, как создан объект, поэтому можете использовать его как параметр для вызова других методов в том же запросе.

### <a name="group-data-retrieval-on-the-same-object-together-to-improve-performance"></a>Получение сгруппированных данных из одного объекта для повышения производительности

Следует пытаться получить все данные из одного объекта в одном запросе, то есть с помощью одного вызова метода **Load<T>(T, [])**. В приведенном ниже коде показаны два способа получения названия и описания веб-сайта, а также описания списка **Announcements**. Чтобы выполнить компиляцию, нужно добавить инструкцию **using** для пространства имен [System.Linq](http://msdn.microsoft.com/ru-RU/library/bb336768). Кроме того, добавьте псевдоним в инструкцию **using** для пространства имен **Microsoft.SharePoint.Client**, чтобы однозначно ссылаться на его классы. Пример: `using SP = Microsoft.SharePoint.Client;`. 

```C#

static void Method1() 
{ 
    ClientContext context = new ClientContext("http://SiteUrl"); 
    Web web = context.Web; 
    SP.List list = web.Lists.GetByTitle("Announcements"); 
    context.Load(web, w => w.Title, w => w.Description); 
    context.Load(list, l => l.Description); 
    context.ExecuteQuery(); 
} 

static void Method2() 
{ 
    ClientContext context = new ClientContext("http://SiteUrl"); 
    Web web = context.Web; 
    SP.List list = web.Lists.GetByTitle("Announcements"); 
    context.Load(web, w => w.Title); 
    context.Load(list, l => l.Description); 
    context.Load(web, w => w.Description); 
    context.ExecuteQuery();  
} 

```

<br/>

Они не являются одинаково эффективными. В методе **Method1** код для извлечения названия и описания сайта сгруппирован. В методе **Method2** код для извлечения названия и описания сайта разделен другими действиями. Это означает, что метод **Method2** инициирует два отдельных запроса к одному веб-объекту и по нему возвращается два набора результатов. Так как клиентская библиотека пытается возвращать согласованные данные, второй набор результатов включает как название, так и описание. Предыдущий код можно представить следующим образом.

```
Method1: 
SELECT Title, Description FROM Webs WHERE ... 
SELECT Description FROM Lists WHERE … 

Method2: 
SELECT Title FROM Webs WHERE … 
SELECT Description FROM Lists WHERE … 
SELECT Title, Description FROM Webs WHERE … 

```

<br/>

### <a name="specify-which-properties-of-objects-you-want-to-return"></a>Указание свойств объектов, которые необходимо вернуть

В серверной объектной модели SharePoint при получении объекта **SPWeb** вы можете просмотреть все его свойства. В SQL для получения всех столбцов таблицы можно выполнить следующий запрос.

```
SELECT * FROM Webs 
```

В клиентской библиотеке ни метод **Load<T>**, ни какой-либо другой метод не возвращает всех свойств, поэтому необходимо явным образом указать требуемые данные. Например, следующий код получает объект веб-сайта, но возвращаемые свойства не указаны. Далее он пытается прочесть два свойства, однако одно из них не относится с свойствам, которые возвращаются методом **Load** автоматически. Создается исключение. 

```C#
// Starting with ClientContext, the constructor requires a URL to the 
// server running SharePoint. 
ClientContext context = new ClientContext("http://SiteUrl"); 

Web web = context.Web; 
context.Load(web); 
context.ExecuteQuery(); 

Console.WriteLine(web.Title); 
Console.WriteLine(web.HasUniqueRoleAssignments);  

```

<br/>

Для успешной компиляции кода обновите его так, как показано ниже. Чтобы выполнить компиляцию, нужно добавить инструкцию **using** для пространства имен [System.Linq](http://msdn.microsoft.com/ru-RU/library/bb336768). Добавьте также псевдоним в инструкцию **using** для пространства имен **Microsoft.SharePoint.Client**, чтобы однозначно ссылаться на его классы. Пример: `using SP = Microsoft.SharePoint.Client;`.

```C#
// Starting with ClientContext, the constructor requires a URL to the 
// server running SharePoint. 
ClientContext context = new ClientContext("http://SiteUrl"); 

Web web = context.Web; 
context.Load(web); 
context.Load(web, web => web.HasUniqueRoleAssignments); 
context.ExecuteQuery(); 

Console.WriteLine(web.Title); 
Console.WriteLine(web.HasUniqueRoleAssignments);  

```

<br/>

### <a name="use-conditional-scope-to-test-for-preconditions-before-loading-data"></a>Использование условной области для проверки предварительных условий перед загрузкой данных

Для условного выполнения кода задайте условную область, используя объект **ConditionalScope**. Например, извлеките свойство списка при условии, что список не пуст. Кроме того, нужно добавить инструкцию **using** для пространств имен [System.Collections.Generic](http://msdn.microsoft.com/ru-RU/library/0sbxh9x2) и [System.Linq](http://msdn.microsoft.com/ru-RU/library/bb336768). Добавьте также псевдоним в инструкцию **using** для пространства имен **Microsoft.SharePoint.Client**, чтобы однозначно ссылаться на его классы. Пример: `using SP = Microsoft.SharePoint.Client;`.
 
> [!NOTE] 
> Вызывать методы и задавать свойства внутри условной области запрещено, так как клиентская библиотека не отслеживает побочные эффекты этих действий. Внутри условной области следует использовать только метод **Load**.

```C#
// Starting with ClientContext, the constructor requires a URL to the 
// server running SharePoint. 
ClientContext context = new ClientContext("http://SiteUrl"); 

SP.List list = context.Web.GetCatalog(ListTemplateType.WebPartCatalog); 
BasePermissions perm = new BasePermissions(); 
perm.Set(PermissionKind.ManageLists); 

ConditionalScope scope = 
    new ConditionalScope(context, 
                         () => list.ServerObjectIsNull &amp;&amp; context.Web.DoesUserHavePermissions(perm).Value); 
using (scope.StartScope()) 
{ 
    context.Load(list, l => l.Title); 
} 
context.ExecuteQuery(); 

label1.Text = scope.TestResult.Value; 

if (scope.TestResult.Value) 
{ 
    label1.Text = list.Title; 
}  

```

<br/>

### <a name="use-an-exception-handling-scope-to-catch-exceptions"></a>Использование области обработки исключений для перехвата исключений

В этом примере показано, как создать и использовать область обработки исключений с помощью объекта **ExceptionHandlingScope**. Сценарий предполагает обновление описания списка и обеспечение создания папок. Существует вероятность того, что список не существует.

```C#


// Starting with ClientContext, the constructor requires a URL to the 
// server running SharePoint. 
ClientContext context = new ClientContext("http://SiteUrl"); 

ExceptionHandlingScope scope = new ExceptionHandlingScope(context); 

using (scope.StartScope()) 
{ 
    using (scope.StartTry()) 
    { 
        List fooList = context.Web.Lists.GetByTitle("Sample"); 
        fooList.Description = "In Try Block"; 
        fooList.Update(); 
    } 
    using (scope.StartCatch()) 
    { 
        // Assume that if there's an exception, 
        // it can be only because there was no "Sample" list. 
        ListCreationInformation listCreateInfo = new ListCreationInformation(); 
        listCreateInfo.Title = "Sample"; 
        listCreateInfo.Description = "In Catch Block"; 
        listCreateInfo.TemplateType = (int)ListTemplateType.Announcements; 
        List fooList = context.Web.Lists.Add(listCreateInfo); 
    } 
    using (scope.StartFinally()) 
    { 
        List fooList = context.Web.Lists.GetByTitle("Sample"); 
        fooList.EnableFolderCreation = true; 
        fooList.Update(); 
    } 
} 

context.ExecuteQuery();  

```

<br/>


## <a name="see-also"></a>См. также
<a name="bk_addresources"> </a>

- [Разработка надстроек SharePoint](develop-sharepoint-add-ins.md)
- [Создание сайтов для SharePoint](../general-development/build-sites-for-sharepoint.md)
    
 

