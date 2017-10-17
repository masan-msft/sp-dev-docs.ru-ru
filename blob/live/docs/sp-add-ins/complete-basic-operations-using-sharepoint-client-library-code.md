---
title: "Выполнение базовых операций с использованием кода библиотеки клиента в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 6d6856643f6dfb8501478f0d8384445900d03679
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="complete-basic-operations-using-sharepoint-client-library-code"></a><span data-ttu-id="9dbff-102">Выполнение базовых операций с использованием кода библиотеки клиента в SharePoint</span><span class="sxs-lookup"><span data-stu-id="9dbff-102">Complete basic operations using SharePoint client library code</span></span>
<span data-ttu-id="9dbff-103">Узнайте, как создавать код для выполнения основных операций с клиентской объектной моделью SharePoint .NET Framework (CSOM).</span><span class="sxs-lookup"><span data-stu-id="9dbff-103">Learn how to write code to perform basic operations with the SharePoint .NET Framework client object model (CSOM).</span></span>
 

 <span data-ttu-id="9dbff-p101">**Примечание.** В настоящее время идет процесс замены названия "приложения для SharePoint" названием "надстройки SharePoint". Во время этого процесса в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio может по-прежнему использоваться термин "приложения для SharePoint". Дополнительные сведения см. в статье [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="9dbff-p101">**Note**  The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see  [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span></span>
 


## <a name="sharepoint-client-apis"></a><span data-ttu-id="9dbff-107">Клиентские интерфейсы API SharePoint</span><span class="sxs-lookup"><span data-stu-id="9dbff-107">SharePoint client APIs</span></span>
<span data-ttu-id="9dbff-108"><a name="ClientAPIs"> </a></span><span class="sxs-lookup"><span data-stu-id="9dbff-108"></span></span>

<span data-ttu-id="9dbff-p102">С помощью клиентской объектной модели SharePoint (CSOM) вы можете получать и изменять данные в SharePoint, а также управлять ими. В SharePoint доступ к CSOM осуществляется несколькими путями:</span><span class="sxs-lookup"><span data-stu-id="9dbff-p102">You can use the SharePoint client object model (CSOM) to retrieve, update, and manage data in SharePoint. SharePoint makes the CSOM available in several forms.</span></span> 
 

 

- <span data-ttu-id="9dbff-111">распространяемые сборки .NET Framework;</span><span class="sxs-lookup"><span data-stu-id="9dbff-111">.NET Framework redistributable assemblies</span></span>
    
 
- <span data-ttu-id="9dbff-112">библиотека JavaScript;</span><span class="sxs-lookup"><span data-stu-id="9dbff-112">JavaScript library</span></span>
    
 
- <span data-ttu-id="9dbff-113">конечные точки REST и OData;</span><span class="sxs-lookup"><span data-stu-id="9dbff-113">REST/OData endpoints</span></span>
    
 
- <span data-ttu-id="9dbff-114">Сборки Windows Phone</span><span class="sxs-lookup"><span data-stu-id="9dbff-114">Windows Phone assemblies</span></span>
    
 
- <span data-ttu-id="9dbff-115">Распространяемые сборки Silverlight</span><span class="sxs-lookup"><span data-stu-id="9dbff-115">Silverlight redistributable assemblies</span></span>
    
 
<span data-ttu-id="9dbff-116">Дополнительные сведения о наборах API, доступных на платформе SharePoint, см. в статье [Выбор правильного набора API в SharePoint 2013](http://msdn.microsoft.com/library/f36645da-77c5-47f1-a2ca-13d4b62b320d%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="9dbff-116">For more details about the sets of APIs available on the SharePoint platform, see  [Choose the right API set in SharePoint](http://msdn.microsoft.com/library/f36645da-77c5-47f1-a2ca-13d4b62b320d%28Office.15%29.aspx).</span></span> 
 

 
<span data-ttu-id="9dbff-p103">В этой статье описывается выполнение базовых операций с помощью объектной модели .NET Framework, доступной в Центре загрузки Майкрософт в качестве распространяемого пакета. Найти его можно по поисковым фразам "пакет SDK для клиентских компонентов SharePoint Server 2013" или "пакет SDK для клиентских компонентов SharePoint Online". Сведения об использовании других клиентских интерфейсов API см. в статьях  [Выполнение базовых операций с использованием кода библиотеки JavaScript в SharePoint](complete-basic-operations-using-javascript-library-code-in-sharepoint.md),  [Выполнение базовых операций с использованием конечных точек SharePoint REST](complete-basic-operations-using-sharepoint-rest-endpoints.md),  [Построение приложений Windows Phone, обращающихся к SharePoint](http://msdn.microsoft.com/library/36681335-f772-4499-8445-f94481bc18e7%28Office.15%29.aspx) и [Использование объектной модели Silverlight](http://msdn.microsoft.com/library/cea7829d-f360-4052-8b76-91d90bcefd2a%28Office.15%29.aspx) в Пакет SDK для SharePoint 2010.</span><span class="sxs-lookup"><span data-stu-id="9dbff-p103">This article is shows how to perform basic operations using the .NET Framework object model, which is available as a redistributable package on the Microsoft Download Center. Search for "SharePoint Server 2013 Client Components SDK" or "SharePoint Online Client Components SDK". For information about how to use the other client APIs see,  [Complete basic operations using JavaScript library code in SharePoint](complete-basic-operations-using-javascript-library-code-in-sharepoint.md),  [Complete basic operations using SharePoint REST endpoints](complete-basic-operations-using-sharepoint-rest-endpoints.md),  [Build Windows Phone apps that access SharePoint](http://msdn.microsoft.com/library/36681335-f772-4499-8445-f94481bc18e7%28Office.15%29.aspx), and  [Using the Silverlight Object Model](http://msdn.microsoft.com/library/cea7829d-f360-4052-8b76-91d90bcefd2a%28Office.15%29.aspx) in the SharePoint 2010 SDK.</span></span>
 

 

## <a name="basic-operations-with-the-sharepoint-net-client-object-model"></a><span data-ttu-id="9dbff-120">Основные операции с клиентской объектной моделью .NET в SharePoint</span><span class="sxs-lookup"><span data-stu-id="9dbff-120">Basic operations with the SharePoint .NET client object model</span></span>
<span data-ttu-id="9dbff-121"><a name="BasicOps_SPCSOMOps"> </a></span><span class="sxs-lookup"><span data-stu-id="9dbff-121"></span></span>

<span data-ttu-id="9dbff-122">В следующих разделах описываются задачи, которые вы можете выполнять программным путем. Они включают примеры кода на языке C#, в которых демонстрируются операции CSOM.</span><span class="sxs-lookup"><span data-stu-id="9dbff-122">The following sections describe tasks that you can complete programmatically, and they include C# code examples that demonstrate CSOM operations.</span></span>
 

 
<span data-ttu-id="9dbff-p104">Когда вы создаете проект **надстройки для SharePoint** в Visual Studio 2012, в него автоматически добавляются ссылки на сборки .NET Framework, **Microsoft.SharePoint.Client.Runtime.dll** и **Microsoft.SharePoint.Client.dll**. Для других типов проектов, например приложений .NET Framework или консольных приложений, эти ссылки необходимо добавлять вручную. Файлы находятся на любом сервере SharePoint в папке %ProgramFiles%\Common Files\Microsoft Shared\web server extensions\15\ISAPI.</span><span class="sxs-lookup"><span data-stu-id="9dbff-p104">When you create an  **Add-in for SharePoint** project in Visual Studio 2012, references to the .NET Framework assemblies, **Microsoft.SharePoint.Client.Runtime.dll** and **Microsoft.SharePoint.Client.dll**, are automatically added to the project. For other kinds of projects, such as .NET Framework applications or console applications, you should add these references. The files are located on any SharePoint server at %ProgramFiles%\Common Files\Microsoft Shared\web server extensions\15\ISAPI.</span></span>
 

 
<span data-ttu-id="9dbff-p105">Во всех этих примерах предполагается, что код содержится в файле кода программной части для веб-страницы Microsoft ASP.NET. Вам нужно добавить в файл кода следующую инструкцию **using**:</span><span class="sxs-lookup"><span data-stu-id="9dbff-p105">All of these examples assume that the code is in a code-behind file for an Microsoft ASP.NET webpage. You must add the following  **using** statement to the code file.</span></span>
 

 



```
using Microsoft.SharePoint.Client;
```

<span data-ttu-id="9dbff-p106">Если не указано иное, предполагается, что каждый из этих примеров содержится в методе без параметров, определенном в классе страницы. Кроме того,  `label1`,  `label2` и так далее это имена объектов [Label](http://msdn2.microsoft.com/EN-US/library/620f4ses) на странице.</span><span class="sxs-lookup"><span data-stu-id="9dbff-p106">Except where specified otherwise, you can assume that each of these examples is in a parameterless method that is defined in the page's class. Also,  `label1`,  `label2`, and so on, are the names of  [Label](http://msdn2.microsoft.com/EN-US/library/620f4ses) objects on the page.</span></span>
 

 

 <span data-ttu-id="9dbff-p107">**Примечание.** При создании размещаемой у поставщика надстройки SharePoint с помощью веб-приложения ASP.NET и добавлении ссылки на сборку проекта веб-приложения в Visual Studio присвойте свойству сборки **Копировать локально** значение **True**. Это не относится к случаям, когда сборка уже установлена на веб-сервере или вы знаете, что она установлена до того, как была развернута надстройка. Платформа .NET Framework устанавливается в веб-ролях Microsoft Azure и на веб-сайтах Azure, но не устанавливаются сборки клиента SharePoint и различные расширения управляемого кода и платформы Microsoft. Инструменты разработчика Office для Visual Studio 2012 автоматически добавляют ссылки на некоторые сборки, часто используемые в надстройках SharePoint, и задают свойство **Копировать локально**.</span><span class="sxs-lookup"><span data-stu-id="9dbff-p107">**Note**  When you are making a provider-hosted SharePoint Add-in with an ASP.NET web application and you add a reference to an assembly to the web application project in Visual Studio, set the  **Copy Local** property of the assembly to **True**, unless you know that the assembly is already installed on the web server, or you can ensure that it is installed before you deploy your add-in. The .NET Framework is installed on Microsoft Azure Web Roles and Azure Web Sites. But the SharePoint client assemblies and the various Microsoft managed code extensions and foundations are not installed. Office Developer Tools for Visual Studio 2012 automatically adds references to some assemblies commonly used in SharePoint Add-ins and sets the  **Copy Local** property.</span></span>
 


## <a name="sharepoint-website-tasks"></a><span data-ttu-id="9dbff-134">Задачи, связанные с веб-сайтом SharePoint</span><span class="sxs-lookup"><span data-stu-id="9dbff-134">SharePoint website tasks</span></span>
<span data-ttu-id="9dbff-135"><a name="BasicOps_SPWebTasks"> </a></span><span class="sxs-lookup"><span data-stu-id="9dbff-135"></span></span>

<span data-ttu-id="9dbff-136">В этих примерах показано, как использовать модель CSOM .NET Framework для выполнения задач, связанных с веб-сайтами.</span><span class="sxs-lookup"><span data-stu-id="9dbff-136">These examples show how to use the .NET Framework CSOM to complete website-related tasks.</span></span>
 

 

### <a name="retrieve-the-properties-of-a-website"></a><span data-ttu-id="9dbff-137">Получите свойства веб-сайта</span><span class="sxs-lookup"><span data-stu-id="9dbff-137">Retrieve the properties of a website</span></span>

<span data-ttu-id="9dbff-138">Следующий код служит для получения названия веб-сайта SharePoint.</span><span class="sxs-lookup"><span data-stu-id="9dbff-138">Retrieve the title of a SharePoint website.</span></span>
 

 

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


### <a name="retrieve-only-selected-properties-of-a-website"></a><span data-ttu-id="9dbff-139">Получение только выбранных свойств веб-сайта</span><span class="sxs-lookup"><span data-stu-id="9dbff-139">Retrieve only selected properties of a website</span></span>

<span data-ttu-id="9dbff-p108">Иногда клиенту требуются только некоторые свойства объекта. Модель CSOM .NET Framework в SharePoint позволяет получать только некоторые свойства объекта на сервере. Вы можете использовать анонимные методы, которые могут представлять собой лямбда-выражения, для запроса свойств с определенными именами. Клиентская библиотека запросит с сервера только эти свойства, и сервер отправит только их клиенту. Таким образом можно избежать передачи ненужных данных между клиентом и сервером. Это также полезно в том случае, если у пользователя нет разрешения на доступ к одному или нескольким другим ненужным свойствам объекта. Обратите внимание на то, что вам потребуется добавить инструкцию **using** для пространства имен [System.Linq](http://msdn2.microsoft.com/EN-US/library/bb336768).</span><span class="sxs-lookup"><span data-stu-id="9dbff-p108">Sometimes, the client is interested only in a few properties of an object. The SharePoint .NET Framework CSOM does not require you to get all properties from the object on a server—you can use anonymous methods, which can be lambda expressions, to specifically request property names. The client library will query only for those properties on the server, and the server will send only those properties to the client. This technique reduces unnecessary data transfer between the client and the server. It is also useful when the user does not have permission to one or more of the other, unused properties on an object. Note that you will need to add a  **using** statement for [System.Linq](http://msdn2.microsoft.com/EN-US/library/bb336768).</span></span>
 

 

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


 <span data-ttu-id="9dbff-146">**Примечание.** Если вы попытаетесь обратиться к другим свойствам, код создаст исключение, поскольку они недоступны.</span><span class="sxs-lookup"><span data-stu-id="9dbff-146">**Note**  If you try to access other properties, the code throws an exception because other properties are not available.</span></span>
 


### <a name="write-to-websites-properties"></a><span data-ttu-id="9dbff-147">Запись значений для свойств веб-сайта</span><span class="sxs-lookup"><span data-stu-id="9dbff-147">Write to website's properties</span></span>

<span data-ttu-id="9dbff-148">В этом примере показано, как записать значения для свойств веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="9dbff-148">This example shows how to write to the website's properties.</span></span>
 

 

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


### <a name="create-a-new-sharepoint-website"></a><span data-ttu-id="9dbff-149">Создание веб-сайта SharePoint</span><span class="sxs-lookup"><span data-stu-id="9dbff-149">Create a new SharePoint website</span></span>

<span data-ttu-id="9dbff-p109">В этом примере показано, как создать дочерний сайт SharePoint текущего веб-сайта. Для создания веб-сайта используйте класс **WebCreationInformation**. Вам также потребуется добавить инструкции **using** для пространств имен [System.Collections.Generic](http://msdn2.microsoft.com/EN-US/library/0sbxh9x2) и [System.Text](http://msdn2.microsoft.com/EN-US/library/x76y3wky).</span><span class="sxs-lookup"><span data-stu-id="9dbff-p109">This example shows how to create a new SharePoint site as a subsite of the current website. Use the  **WebCreationInformation** class to create a new website. You will also need to add **using** statements for [System.Collections.Generic](http://msdn2.microsoft.com/EN-US/library/0sbxh9x2) and [System.Text](http://msdn2.microsoft.com/EN-US/library/x76y3wky).</span></span>
 

 

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


## <a name="sharepoint-list-tasks"></a><span data-ttu-id="9dbff-153">Задачи по работе со списками SharePoint</span><span class="sxs-lookup"><span data-stu-id="9dbff-153">SharePoint list tasks</span></span>
<span data-ttu-id="9dbff-154"><a name="BasicOps_SPListTasks"> </a></span><span class="sxs-lookup"><span data-stu-id="9dbff-154"></span></span>

<span data-ttu-id="9dbff-155">В этих примерах показано, как использовать модель CSOM .NET Framework для выполнения задач, связанных со списками.</span><span class="sxs-lookup"><span data-stu-id="9dbff-155">These examples show how to use the .NET Framework CSOM to complete list-related tasks.</span></span>
 

 

### <a name="retrieve-all-sharepoint-lists-in-a-web"></a><span data-ttu-id="9dbff-156">Получение всех списков SharePoint на сайте</span><span class="sxs-lookup"><span data-stu-id="9dbff-156">Retrieve all SharePoint lists in a web</span></span>

<span data-ttu-id="9dbff-p110">В этом примере извлекаются все списки SharePoint, имеющиеся на веб-сайте SharePoint. Для выполнения этого кода вам потребуется добавить инструкцию **using** для пространства имен [System.Linq](http://msdn2.microsoft.com/EN-US/library/bb336768).</span><span class="sxs-lookup"><span data-stu-id="9dbff-p110">This example retrieves all SharePoint lists in a SharePoint website. To compile this code you will need to add a  **using** statement for [System.Linq](http://msdn2.microsoft.com/EN-US/library/bb336768).</span></span>
 

 

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


 <span data-ttu-id="9dbff-p111">**Примечание.** Кроме того, вы можете сохранить возвращенное значение в другой коллекции с помощью метода **LoadQuery**, вместо того чтобы использовать свойство **web.Lists**. Вам также потребуется добавить инструкции **using** для пространств имен [System.Collections.Generic](http://msdn2.microsoft.com/EN-US/library/0sbxh9x2) и [System.Linq](http://msdn2.microsoft.com/EN-US/library/bb336768). Помимо этого, добавьте псевдоним в инструкцию using для пространства имен **Microsoft.SharePoint.Client**, чтобы получить возможность ссылаться на его классы однозначно. Пример: `using SP = Microsoft.SharePoint.Client;`.</span><span class="sxs-lookup"><span data-stu-id="9dbff-p111">**Note**  Alternatively, you can use the  **LoadQuery** method to store the return value in another collection, rather than use the **web.Lists** property. You will also need to add **using** statements for [System.Collections.Generic](http://msdn2.microsoft.com/EN-US/library/0sbxh9x2) and [System.Linq](http://msdn2.microsoft.com/EN-US/library/bb336768). Also, add an alias to the using statement for  **Microsoft.SharePoint.Client** namespace so you can refer to its classes unambiguously. For example, `using SP = Microsoft.SharePoint.Client;`.</span></span>
 


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


### <a name="create-and-update-a-sharepoint-list"></a><span data-ttu-id="9dbff-163">Создание и обновление списка SharePoint</span><span class="sxs-lookup"><span data-stu-id="9dbff-163">Create and update a SharePoint list</span></span>

<span data-ttu-id="9dbff-164">В этом примере список SharePoint создается и обновляется с помощью класса **ListCreationInformation**.</span><span class="sxs-lookup"><span data-stu-id="9dbff-164">This example creates a SharePoint list and updates it using the  **ListCreationInformation** class.</span></span>
 

 

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


### <a name="delete-a-sharepoint-list"></a><span data-ttu-id="9dbff-165">Удаление списка SharePoint</span><span class="sxs-lookup"><span data-stu-id="9dbff-165">Delete a SharePoint list</span></span>

<span data-ttu-id="9dbff-166">В этом примере удаляется список SharePoint.</span><span class="sxs-lookup"><span data-stu-id="9dbff-166">This example deletes a SharePoint list.</span></span>
 

 

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


### <a name="add-a-field-to-a-sharepoint-list"></a><span data-ttu-id="9dbff-167">Добавление поля в список SharePoint</span><span class="sxs-lookup"><span data-stu-id="9dbff-167">Add a field to a SharePoint list</span></span>

<span data-ttu-id="9dbff-p112">В этом примере в список SharePoint добавляется поле. Добавьте псевдоним в инструкцию using для пространства имен  **Microsoft.SharePoint.Client** , чтобы получить возможность ссылаться на его классы однозначно. Пример: `using SP = Microsoft.SharePoint.Client;`.</span><span class="sxs-lookup"><span data-stu-id="9dbff-p112">This example adds a field to a SharePoint list. add an alias to the using statement for  **Microsoft.SharePoint.Client** namespace so you can refer to its classes unambiguously. For example, `using SP = Microsoft.SharePoint.Client;`.</span></span>
 

 

 <span data-ttu-id="9dbff-p113">**Примечание.** В этом примере для приведения типа используется метод **context.CastTo**. Перед выполнением запроса клиентская библиотека не знает тип возвращаемого объекта, и единственным возможным типом является **SharePoint.Field**. Если тип объекта известен, вы можете воспользоваться методом **ClientContext.CastTo<RealType>**, чтобы привести его.</span><span class="sxs-lookup"><span data-stu-id="9dbff-p113">**Note**  The example uses  **context.CastTo** to do a cast. Before executing the query, the client library does not know the real type of the returned object "field" and **SharePoint.Field** is the only possible type. If you know the real type, you can use the **ClientContext.CastTo<RealType>** method to cast the object.</span></span>
 


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


## <a name="sharepoint-list-item-tasks"></a><span data-ttu-id="9dbff-174">Задачи, связанные с элементами списков SharePoint</span><span class="sxs-lookup"><span data-stu-id="9dbff-174">SharePoint list item tasks</span></span>
<span data-ttu-id="9dbff-175"><a name="BasicOps_SPListItemTasks"> </a></span><span class="sxs-lookup"><span data-stu-id="9dbff-175"></span></span>

<span data-ttu-id="9dbff-176">В этих примерах демонстрируется использование модели CSOM .NET Framework для выполнения задач, связанных с элементами списков.</span><span class="sxs-lookup"><span data-stu-id="9dbff-176">These examples demonstrate how to use the .NET Framework CSOM to complete tasks that are related to list items.</span></span>
 

 

### <a name="retrieve-items-from-a-sharepoint-list"></a><span data-ttu-id="9dbff-177">Получение элементов из списка SharePoint</span><span class="sxs-lookup"><span data-stu-id="9dbff-177">Retrieve items from a SharePoint list</span></span>

<span data-ttu-id="9dbff-p114">В этом примере извлекаются элементы из списка SharePoint. Вам также потребуется добавить инструкцию **using** для пространства имен **Microsoft.SharePoint.Client.QueryExpression**.</span><span class="sxs-lookup"><span data-stu-id="9dbff-p114">This example retrieves the items in a SharePoint list. You will also need to add a  **using** statement for **Microsoft.SharePoint.Client.QueryExpression**.</span></span>
 

 

 <span data-ttu-id="9dbff-180">**Примечание.** С помощью свойства **FolderServerRelativeUrl** вы можете ограничить возвращаемые элементы только теми, которые находятся в указанной папке.</span><span class="sxs-lookup"><span data-stu-id="9dbff-180">**Note**  You can use the  **FolderServerRelativeUrl** property to further restrict the items that are returned to those in a specified folder.</span></span>
 


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


### <a name="create-a-new-list-item"></a><span data-ttu-id="9dbff-181">Создание элемента списка</span><span class="sxs-lookup"><span data-stu-id="9dbff-181">Create a new list item</span></span>

<span data-ttu-id="9dbff-182">В этом примере список SharePoint создается с помощью класса **ListItemCreationInformation**.</span><span class="sxs-lookup"><span data-stu-id="9dbff-182">This example creates a new SharePoint list item using the  **ListItemCreationInformation** class.</span></span>
 

 

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


### <a name="update-a-list-item"></a><span data-ttu-id="9dbff-183">Обновление элемента списка</span><span class="sxs-lookup"><span data-stu-id="9dbff-183">Update a list item</span></span>

<span data-ttu-id="9dbff-184">В этом примере обновляется элемент списка SharePoint.</span><span class="sxs-lookup"><span data-stu-id="9dbff-184">This example updates a SharePoint list item.</span></span>
 

 

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


### <a name="delete-a-list-item"></a><span data-ttu-id="9dbff-185">Удаление элемента списка</span><span class="sxs-lookup"><span data-stu-id="9dbff-185">Delete a list item</span></span>

<span data-ttu-id="9dbff-186">В этом примере удаляется элемент списка SharePoint.</span><span class="sxs-lookup"><span data-stu-id="9dbff-186">This example deletes a SharePoint list item.</span></span>
 

 

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


## <a name="sharepoint-field-tasks"></a><span data-ttu-id="9dbff-187">Задачи, связанные с полями SharePoint</span><span class="sxs-lookup"><span data-stu-id="9dbff-187">SharePoint field tasks</span></span>
<span data-ttu-id="9dbff-188"><a name="BasicOps_SPFieldTasks"> </a></span><span class="sxs-lookup"><span data-stu-id="9dbff-188"></span></span>

<span data-ttu-id="9dbff-189">В этих примерах показано, как использовать модель CSOM .NET Framework в SharePoint для выполнения задач, связанных с полями.</span><span class="sxs-lookup"><span data-stu-id="9dbff-189">These examples show how to use the SharePoint .NET Framework CSOM to complete field-related tasks.</span></span> 
 

 

### <a name="retrieve-all-of-the-fields-in-a-list"></a><span data-ttu-id="9dbff-190">Получение всех полей в списке</span><span class="sxs-lookup"><span data-stu-id="9dbff-190">Retrieve all of the fields in a list</span></span>

<span data-ttu-id="9dbff-p115">В этом примере извлекаются все поля, имеющиеся в списке SharePoint. Вам также потребуется добавить псевдоним в инструкцию **using** для пространства имен **Microsoft.SharePoint.Client**, чтобы получить возможность ссылаться на его классы однозначно. Пример: `using SP = Microsoft.SharePoint.Client;`.</span><span class="sxs-lookup"><span data-stu-id="9dbff-p115">This example retrieves all of the fields in a SharePoint list. You will also need to add an alias to the  **using** statement for the **Microsoft.SharePoint.Client** namespace so you can refer to its classes unambiguously; for example, `using SP = Microsoft.SharePoint.Client;`.</span></span>
 

 

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


### <a name="retrieve-a-specific-field-from-the-list"></a><span data-ttu-id="9dbff-193">Получение определенного поля из списка</span><span class="sxs-lookup"><span data-stu-id="9dbff-193">Retrieve a specific field from the list</span></span>

<span data-ttu-id="9dbff-p116">Если вы хотите получить сведения об определенном поле, воспользуйтесь методом **Fields.GetByInternalNameOrTitle**. Он возвращает объект типа **Field**. Перед выполнением запроса клиент не знает тип объекта, а в C# нет синтаксической конструкции для приведения его к производному типу. Поэтому для его приведения используйте метод **ClientContext.CastTo**, который указывает клиентской библиотеке на то, что объект нужно создать повторно. Вам также потребуется добавить инструкцию **using** для пространства имен [System.Collections.Generic](http://msdn2.microsoft.com/EN-US/library/0sbxh9x2). Кроме того, вам нужно добавить псевдоним в инструкцию **using** для пространства имен **Microsoft.SharePoint.Client**, чтобы получить возможность ссылаться на его классы однозначно. Пример: `using SP = Microsoft.SharePoint.Client;`.</span><span class="sxs-lookup"><span data-stu-id="9dbff-p116">If you want to retrieve information about a specific field, use the  **Fields.GetByInternalNameOrTitle** method. The return type of this method is **Field**. Before the query is executed, the client does not know the type of object, and C# syntax is not available for casting it to the derived type. Therefore, use the  **ClientContext.CastTo** method to cast it, which instructs the client library to recreate an object. You will also need to add a **using** statement for [System.Collections.Generic](http://msdn2.microsoft.com/EN-US/library/0sbxh9x2). You will also need to add an alias to the  **using** statement for the **Microsoft.SharePoint.Client** namespace so you can refer to its classes unambiguously. For example, `using SP = Microsoft.SharePoint.Client;`.</span></span>
 

 

 <span data-ttu-id="9dbff-p117">**Примечание.** Метод **GetByInternalNameOrTitle**, используемый в этом примере, является удаленным. Он не использует данные из клиентской коллекции, даже если она уже заполнена.</span><span class="sxs-lookup"><span data-stu-id="9dbff-p117">**Note**  The  **GetByInternalNameOrTitle** method used in this example is a remote method. It does not use the data from the client collection even if the client collection is already populated.</span></span>
 


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


## <a name="sharepoint-user-tasks"></a><span data-ttu-id="9dbff-203">Задачи, связанные с пользователями SharePoint</span><span class="sxs-lookup"><span data-stu-id="9dbff-203">SharePoint user tasks</span></span>
<span data-ttu-id="9dbff-204"><a name="BasicOps_SPSecurityTasks"> </a></span><span class="sxs-lookup"><span data-stu-id="9dbff-204"></span></span>

<span data-ttu-id="9dbff-205">Вы можете использовать модель CSOM .NET Framework в SharePoint для управления пользователями и группами SharePoint, а также безопасностью пользователей.</span><span class="sxs-lookup"><span data-stu-id="9dbff-205">You can use the SharePoint .NET Framework CSOM to manage SharePoint users, groups, and user security.</span></span> 
 

 

### <a name="add-a-user-to-a-sharepoint-group"></a><span data-ttu-id="9dbff-206">Добавление пользователя в группу SharePoint</span><span class="sxs-lookup"><span data-stu-id="9dbff-206">Add a user to a SharePoint group</span></span>

<span data-ttu-id="9dbff-207">В этом примере в группу SharePoint с именем Members добавляется пользователь и некоторые сведения о нем.</span><span class="sxs-lookup"><span data-stu-id="9dbff-207">This example adds a user and some user information to a SharePoint group named Members.</span></span>
 

 

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


### <a name="retrieve-all-users-in-a-sharepoint-group"></a><span data-ttu-id="9dbff-208">Получение всех пользователей из группы SharePoint</span><span class="sxs-lookup"><span data-stu-id="9dbff-208">Retrieve all users in a SharePoint group</span></span>

<span data-ttu-id="9dbff-209">В этом примере извлекаются сведения о всех пользователях в группе SharePoint с именем Members.</span><span class="sxs-lookup"><span data-stu-id="9dbff-209">This example retrieves information about all users from a SharePoint group named Members.</span></span>
 

 

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


### <a name="create-a-role"></a><span data-ttu-id="9dbff-210">Создание роли</span><span class="sxs-lookup"><span data-stu-id="9dbff-210">Create a role</span></span>

<span data-ttu-id="9dbff-211">В этом примере создается роль, имеющая разрешения на создание оповещений и управление ими.</span><span class="sxs-lookup"><span data-stu-id="9dbff-211">This example creates a role that has create and manage alerts permissions.</span></span>
 

 

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


### <a name="add-a-user-to-a-role"></a><span data-ttu-id="9dbff-212">Добавление пользователя к роли</span><span class="sxs-lookup"><span data-stu-id="9dbff-212">Add a user to a role</span></span>

<span data-ttu-id="9dbff-213">В этом примере к роли добавляется пользователь.</span><span class="sxs-lookup"><span data-stu-id="9dbff-213">This example adds a user to a role.</span></span>
 

 

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


## <a name="rules-and-best-practices-for-using-the-sharepoint-net-client-object-model"></a><span data-ttu-id="9dbff-214">Правила и рекомендации по клиентской объектной модели .NET в SharePoint</span><span class="sxs-lookup"><span data-stu-id="9dbff-214">Rules and best practices for using the SharePoint .NET client object model</span></span>
<span data-ttu-id="9dbff-215"><a name="Best"> </a></span><span class="sxs-lookup"><span data-stu-id="9dbff-215"></span></span>

<span data-ttu-id="9dbff-216">В этих примерах демонстрируются некоторые важные рекомендации и требования, которые следует соблюдать при использовании модели CSOM .NET Framework в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="9dbff-216">These examples illustrate some important best practices and requirements you should conform to when using the SharePoint .NET Framework CSOM.</span></span>
 

 

### <a name="call-clientcontextexecutequery-before-accessing-any-value-properties"></a><span data-ttu-id="9dbff-217">Вызов метода ClientContext.ExecuteQuery перед доступом к свойствам значения</span><span class="sxs-lookup"><span data-stu-id="9dbff-217">Call ClientContext.ExecuteQuery before accessing any value properties</span></span>

<span data-ttu-id="9dbff-p118">Модель CSOM .NET Framework в SharePoint требует использования шаблона программирования наподобие SQL: необходимо объявить запрос и выполнить его перед доступом к данным. Например, следующий код, в котором выполняется попытка отобразить название веб-сайта SharePoint, создаст исключение.</span><span class="sxs-lookup"><span data-stu-id="9dbff-p118">The SharePoint .NET Framework CSOM requires that you use a SQL-like programming pattern: declare what you want and execute the query before you access the data. For example, the following code, attempts to display the SharePoint website's title, will throw an exception.</span></span>
 

 

```C#
// Starting with ClientContext, the constructor requires a URL to the 
// server running SharePoint. 
ClientContext context = new ClientContext("http://SiteUrl"); 

Web web = context.Web; 
label1.Text = web.Title;  

```

<span data-ttu-id="9dbff-220">Сбой произойдет по той причине, что в коде CSOM .NET Framework в SharePoint необходимо выполнить следующие действия:</span><span class="sxs-lookup"><span data-stu-id="9dbff-220">This code fails because SharePoint .NET Framework CSOM code must:</span></span>
 

 

1. <span data-ttu-id="9dbff-221">создать прямой запрос SQL или хранимую процедуру;</span><span class="sxs-lookup"><span data-stu-id="9dbff-221">Build either an ad hoc SQL query or a stored procedure.</span></span>
    
 
2. <span data-ttu-id="9dbff-222">выполнить запрос SQL;</span><span class="sxs-lookup"><span data-stu-id="9dbff-222">Execute the SQL query.</span></span>
    
 
3. <span data-ttu-id="9dbff-223">прочитать результаты из SQL.</span><span class="sxs-lookup"><span data-stu-id="9dbff-223">Read results from SQL.</span></span>
    
 
<span data-ttu-id="9dbff-p119">В модели CSOM .NET Framework в SharePoint при вызове метода вы создаете запрос. Запросы накапливаются и не отправляются на сервер, пока не будет вызван метод **ExecuteQuery**. В следующем примере показан код, необходимый для отображения названия веб-сайта. Вам также потребуется добавить инструкцию **using** для пространства имен [System.Linq](http://msdn2.microsoft.com/EN-US/library/bb336768). Кроме того, добавьте псевдоним в инструкцию **using** для пространства имен **Microsoft.SharePoint.Client**, чтобы получить возможность ссылаться на его классы однозначно. Пример: `using SP = Microsoft.SharePoint.Client;`.</span><span class="sxs-lookup"><span data-stu-id="9dbff-p119">In SharePoint .NET Framework CSOM , when you call a method you build a query. Queries accumulate and are not sent to the server until  **ExecuteQuery** is called. The following example shows the code that is required to display the website's title. You will also need to add a **using** statement for [System.Linq](http://msdn2.microsoft.com/EN-US/library/bb336768). Also, add an alias to the  **using** statement for the **Microsoft.SharePoint.Client** namespace so you can refer to its classes unambiguously. For example, `using SP = Microsoft.SharePoint.Client;`.</span></span>
 

 



```C#
// Starting with ClientContext, the constructor requires a URL to the 
// server running SharePoint. 
ClientContext context = new ClientContext("http://SiteUrl"); 

Web web = context.Web; 

context.Load(web, w => w.Title); 

context.ExecuteQuery(); 

label1.Text = web.Title;   

```

<span data-ttu-id="9dbff-230">Отличие в том, что добавлены следующие строки:</span><span class="sxs-lookup"><span data-stu-id="9dbff-230">The differences are the addition of these lines:</span></span>
 

 



```
context.Load(web, w => w.Title); 
context.ExecuteQuery(); 

```

<span data-ttu-id="9dbff-p120">В первой строке создается запрос для свойства **Title** сайта. Во второй строке выполняется запрос.</span><span class="sxs-lookup"><span data-stu-id="9dbff-p120">The first line creates a query for the web's  **Title** property. The second line executes the query.</span></span>
 

 

### <a name="do-not-use-value-objects-returned-from-methods-or-properties-in-the-same-query"></a><span data-ttu-id="9dbff-233">Не используйте объекты значений, возвращенные методами или свойствами, в том же запросе</span><span class="sxs-lookup"><span data-stu-id="9dbff-233">Do not use value objects returned from methods or properties in the same query</span></span>

<span data-ttu-id="9dbff-p121">Когда метод или свойство возвращает объект значения, вы не можете использовать этот объект, пока запрос не будет выполнен. Например, в следующем коде выполняется попытка создать список SharePoint с тем же названием, что и у родительского веб-сайта, однако создается исключение.</span><span class="sxs-lookup"><span data-stu-id="9dbff-p121">When a value object is returned from a method or property, you cannot use that object until after you have executed the query. For example, the following code tries to create a SharePoint list that has the same title as the parent website, but it will throw an exception.</span></span> 
 

 

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

<span data-ttu-id="9dbff-p122">Исключение создается по той причине, что свойство недоступно, пока запрос не будет выполнен. В SQL можно объявить локальную переменную для хранения значения `web.Title` и использовать ее для создания сайта. В клиентской библиотеке создать локальную переменную невозможно. Вам придется реализовать эту функцию в двух отдельных запросах, как показано в следующем примере. Вам также потребуется добавить инструкцию **using** для пространства имен [System.Linq](http://msdn2.microsoft.com/EN-US/library/bb336768). Кроме того, добавьте псевдоним в инструкцию using для пространства имен **Microsoft.SharePoint.Client**, чтобы получить возможность ссылаться на его классы однозначно. Пример: `using SP = Microsoft.SharePoint.Client;`.</span><span class="sxs-lookup"><span data-stu-id="9dbff-p122">An exception is thrown because the property is not available before you execute the query. In SQL, you would declare a local variable to hold the value for  `web.Title` and use the local variable for web creation. In the client library, you can't create a local variable. You have to split functionality into two separate queries as is shown in the following example. You will also need to add a **using** statement for [System.Linq](http://msdn2.microsoft.com/EN-US/library/bb336768). Also, add an alias to the using statement for  **Microsoft.SharePoint.Client** namespace so you can refer to its classes unambiguously. For example, `using SP = Microsoft.SharePoint.Client;`.</span></span>
 

 



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

<span data-ttu-id="9dbff-243">Отличие заключается в следующих трех строках:</span><span class="sxs-lookup"><span data-stu-id="9dbff-243">The difference is the following three lines:</span></span>
 

 



```C#
context.Load(web, w => w.Title); 
context.ExecuteQuery(); 
...
context.ExecuteQuery(); 

```


### <a name="using-methods-or-properties-that-return-client-objects-in-another-method-call-in-the-same-query"></a><span data-ttu-id="9dbff-244">Использование методов или свойств, возвращающих клиентские объекты, в вызове другого метода в том же запросе</span><span class="sxs-lookup"><span data-stu-id="9dbff-244">Using methods or properties that return client objects in another method call in the same query</span></span>

<span data-ttu-id="9dbff-245">В отличие от объекта значения, клиентский объект можно использовать в вызове другого метода в том же запросе.</span><span class="sxs-lookup"><span data-stu-id="9dbff-245">Unlike a value object, a client object can be used in another method call in the same query.</span></span> 
 

 
<span data-ttu-id="9dbff-p123">В удаленной среде .NET объект значения представляет собой класс или структуру, маршалируемую по значению, а клиентский объект — класс или структуру, маршалируемую по ссылке. Например, **ListItem** — это клиентский объект, а **UrlFieldValue** и другие значения полей — это объекты значений.</span><span class="sxs-lookup"><span data-stu-id="9dbff-p123">In .NET remoting, the value object is a class or struct that is marshaled by value, while the client object is a class or struct that is marshaled by reference. For example, the  **ListItem** is a client object, while the **UrlFieldValue** and other field values are value objects.</span></span>
 

 
<span data-ttu-id="9dbff-p124">В клиентской библиотеке соответствующий объект сервера имеет атрибут  `[ClientCallable(ValueObject = true)]`. Эти значения могут иметь только свойства, но не иметь методов. Примитивные типы, такие как строки и целочисленные значения, обрабатываются как объекты значений. Все значения маршалируются между клиентом и сервером. Значение **ValueObject** по умолчанию **false**.</span><span class="sxs-lookup"><span data-stu-id="9dbff-p124">In the client library, the corresponding server object has the  `[ClientCallable(ValueObject = true)]` attribute. Those values could have only properties and no methods. Primitive types, such as strings and ints, are treated as value objects. All the values are marshaled between the client and the server. The default value of the **ValueObject** is **false**.</span></span> 
 

 
<span data-ttu-id="9dbff-p125">Альтернативой объекту значения является клиентский объект. Если соответствующий серверный объект имеет атрибут **[ClientCallable(ValueObject = false)]**, объект является клиентским. Процесс создания клиентских объектов отслеживается. В реализации клиентской библиотеки для этого используется класс **ObjectPath**. Например, имеется следующий код:</span><span class="sxs-lookup"><span data-stu-id="9dbff-p125">The counterpart to the value object is the client object. If the corresponding server object has the  **[ClientCallable(ValueObject = false)]** attribute, the object is a client object. For client objects, we keep track of how the object is created; this is called **ObjectPath** in the client library implementation. For example, if we have code like the following:</span></span>
 

 



```C#
ClientContext context = new ClientContext("http://SiteUrl"); 
Web web = context.Web; 
SP.List list = web.Lists.GetByTitle("Announcements"); 

```

<span data-ttu-id="9dbff-257">Мы знаем, что список создается следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9dbff-257">We know that the list is created by:</span></span>
 

 

- <span data-ttu-id="9dbff-258">Свойство **Web** извлекается из контекста.</span><span class="sxs-lookup"><span data-stu-id="9dbff-258">Getting the  **Web** property from the context.</span></span>
    
 
- <span data-ttu-id="9dbff-259">Из полученного выше свойства извлекается свойство **Lists**.</span><span class="sxs-lookup"><span data-stu-id="9dbff-259">Getting the  **Lists** property from the above result.</span></span>
    
 
- <span data-ttu-id="9dbff-260">Для полученного выше свойства вызывается метод **GetByTitle** с параметром _Announcements_.</span><span class="sxs-lookup"><span data-stu-id="9dbff-260">Invoking the  **GetByTitle** method with the _Announcements_ parameter from the above result.</span></span>
    
 
<span data-ttu-id="9dbff-p126">Когда модель CSOM .NET Framework в SharePoint передает эти сведения на сервер, вы можете повторно создать объект на нем. В клиентской библиотеке вы можете отслеживать процесс создания клиентского объекта с помощью **ObjectPath**. Так как вы знаете, как был создан объект, вы можете использовать его как параметр для вызова других методов в том же запросе.</span><span class="sxs-lookup"><span data-stu-id="9dbff-p126">When the SharePoint .NET Framework CSOM passes this information to the server, you can recreate the object on the server. In the client library, you can keep track of the  **ObjectPath** that the client object is created. Because you know how the object is created, you could use the object as a parameter to invoke other methods within the same query.</span></span>
 

 

### <a name="group-data-retrieval-on-the-same-object-together-to-improve-performance"></a><span data-ttu-id="9dbff-264">Получение групповых данных из одного объекта для повышения производительности</span><span class="sxs-lookup"><span data-stu-id="9dbff-264">Group data retrieval on the same object together to improve performance</span></span>

<span data-ttu-id="9dbff-p127">Если необходимо получить различные данные из одного объекта, следует попытаться сделать это в одном запросе, то есть использовать один вызов метода **Load<T>(T, [])**. В следующем коде показаны два способа получения названия и описания веб-сайта, а также описания списка **Announcements**. Чтобы скомпилировать этот код, необходимо добавить инструкцию **using** для пространства имен [System.Linq](http://msdn2.microsoft.com/EN-US/library/bb336768). Кроме того, добавьте псевдоним в **инструкцию** using для пространства имен **Microsoft.SharePoint.Client**, чтобы получить возможность ссылаться на его классы однозначно. Пример: `using SP = Microsoft.SharePoint.Client;`.</span><span class="sxs-lookup"><span data-stu-id="9dbff-p127">When reading multiple pieces of data from the same object, you should try to get all of it in a single query; that is, a single call to the  **Load<T>(T, [])** method. The following code shows two ways to retrieve a website's title and description and the **Announcements** list's description. To compile this code, you need to add a **using** statement for [System.Linq](http://msdn2.microsoft.com/EN-US/library/bb336768). Also, add an alias to the using  **statement** for the **Microsoft.SharePoint.Client** namespace so you can refer to its classes unambiguously. For example, `using SP = Microsoft.SharePoint.Client;`.</span></span> 
 

 

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

<span data-ttu-id="9dbff-p128">Эти способы различаются по эффективности. В методе **Method1** код для извлечения названия и описания веб-сайта сгруппирован вместе. В методе **Method2** он разделен другими действиями. Это означает, что метод **Method2** вызывает два отдельных запроса к одному и тому же объекту сайта, и для него будет получено два набора результатов. Поскольку клиентская библиотека стремится возвращать согласованные данные, второй набор результатов будет включать как название, так и описание. Предыдущий код можно представить следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9dbff-p128">These are not equally efficient. In  **Method1**, the code to retrieve the web's title and description is grouped together. In  **Method2**, the code to retrieve the web's title and description is separated by other actions. This means that  **Method2** will trigger two separated queries on the same web object, and there will be two result sets for the same web. Because the client library tries to return consistent data, the second result set will include both the title and description. You could think of the previous code as the following.</span></span>
 

 



```
Method1: 
SELECT Title, Description FROM Webs WHERE ... 
SELECT Description FROM Lists WHERE … 

Method2: 
SELECT Title FROM Webs WHERE … 
SELECT Description FROM Lists WHERE … 
SELECT Title, Description FROM Webs WHERE … 

```


### <a name="specify-which-properties-of-objects-you-want-to-return"></a><span data-ttu-id="9dbff-276">Указание свойств объектов, которые необходимо вернуть</span><span class="sxs-lookup"><span data-stu-id="9dbff-276">Specify which properties of objects you want to return</span></span>

<span data-ttu-id="9dbff-p129">В серверной объектной модели SharePoint при получении объекта **SPWeb** вы можете просмотреть все его свойства. В SQL для получения всех столбцов таблицы можно выполнить следующий запрос:</span><span class="sxs-lookup"><span data-stu-id="9dbff-p129">In the SharePoint server object model, if you get an  **SPWeb** object, you can inspect all of its properties. In SQL, to get all of the columns of a table you can run:</span></span>
 

 

```
SELECT * FROM Webs 
```

<span data-ttu-id="9dbff-p130">В клиентской библиотеке ни метод **Load<T>**, ни какой-либо другой метод не возвращает всех свойств, поэтому необходимо явным образом указать требуемые данные. Например, следующий код получает объект веб-сайта, но возвращаемые свойства не указаны. Далее он пытается прочесть два свойства, однако одно из них не относится к свойствам, которые возвращаются методом **Load** автоматически. Создается исключение.</span><span class="sxs-lookup"><span data-stu-id="9dbff-p130">In the client library, neither  **Load<T>** nor any other method returns all properties, so you have to explicitly specify what you want. For example, the following code retrieves the website object without specifying which properties to return. It then tries to read two properties and one of them is not among the properties that is automatically returned by **Load**. This code throws an exception.</span></span> 
 

 



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

 <span data-ttu-id="9dbff-p131">Чтобы успешно скомпилировать код, обновите его следующим образом. Для компиляции кода необходимо добавить инструкцию **using** для пространства имен [System.Linq](http://msdn2.microsoft.com/EN-US/library/bb336768). Кроме того, добавьте псевдоним в инструкцию **using** для пространства имен **Microsoft.SharePoint.Client**, чтобы получить возможность ссылаться на его классы однозначно. Пример: `using SP = Microsoft.SharePoint.Client;`.</span><span class="sxs-lookup"><span data-stu-id="9dbff-p131">To get the code to compile successfully, update it to the following. To compile this code, you need to add a **using** statement for [System.Linq](http://msdn2.microsoft.com/EN-US/library/bb336768). Also, add an alias to the  **using** statement for the **Microsoft.SharePoint.Client** namespace so you can refer to its classes unambiguously. For example, `using SP = Microsoft.SharePoint.Client;`.</span></span>
 

 



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


### <a name="use-conditional-scope-to-test-for-preconditions-before-loading-data"></a><span data-ttu-id="9dbff-287">Использование условной области для проверки предварительных условий перед загрузкой данных</span><span class="sxs-lookup"><span data-stu-id="9dbff-287">Use conditional scope to test for preconditions before loading data</span></span>

<span data-ttu-id="9dbff-p132">Для выполнения кода по условию задайте условную область с помощью объекта **ConditionalScope**. Например, так можно извлечь свойство списка, если список не равен null. Вам также потребуется добавить инструкции **using** для пространств имен [System.Collections.Generic](http://msdn2.microsoft.com/EN-US/library/0sbxh9x2) и [System.Linq](http://msdn2.microsoft.com/EN-US/library/bb336768). Кроме этого, добавьте псевдоним в инструкцию **using** для пространства имен **Microsoft.SharePoint.Client**, чтобы получить возможность ссылаться на его классы однозначно. Пример: `using SP = Microsoft.SharePoint.Client;`.</span><span class="sxs-lookup"><span data-stu-id="9dbff-p132">To conditionally execute code, set a conditional scope by using a  **ConditionalScope** object. For example, retrieve the list property when the list is not null. You will also need to add **using** statements for [System.Collections.Generic](http://msdn2.microsoft.com/EN-US/library/0sbxh9x2) and [System.Linq](http://msdn2.microsoft.com/EN-US/library/bb336768). Also, add an alias to the  **using** statement for the **Microsoft.SharePoint.Client** namespace so you can refer to its classes unambiguously. For example, `using SP = Microsoft.SharePoint.Client;`.</span></span>
 

 

 <span data-ttu-id="9dbff-p133">**Примечание.** Вызывать методы и задавать свойства внутри условной области запрещено, так как клиентская библиотека не отслеживает побочные эффекты этих действий. Внутри условной области следует использовать только метод **Load**.</span><span class="sxs-lookup"><span data-stu-id="9dbff-p133">**Note**  Calling method and setting properties within a conditional scope are not permitted, because the client library does not track the side effects of method calls and property settings. You should use only  **Load** inside the conditional scope.</span></span>
 


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


### <a name="use-an-exception-handling-scope-to-catch-exceptions"></a><span data-ttu-id="9dbff-295">Использование области обработки исключений для перехвата исключений</span><span class="sxs-lookup"><span data-stu-id="9dbff-295">Use an exception handling scope to catch exceptions</span></span>

<span data-ttu-id="9dbff-p134">В этом примере показано, как создать и использовать область обработки исключений с помощью объекта  **ExceptionHandlingScope** . Код должен изменить описание списка и создать папку. Существует вероятность, что список не существует.</span><span class="sxs-lookup"><span data-stu-id="9dbff-p134">This example shows how to create and use an exception handling scope with an  **ExceptionHandlingScope** object. The scenario is to update the description of a list and also enable folder creation. There is a possibility that the list might not exist.</span></span>
 

 

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


## <a name="additional-resources"></a><span data-ttu-id="9dbff-299">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="9dbff-299">Additional resources</span></span>
<span data-ttu-id="9dbff-300"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="9dbff-300"></span></span>


-  [<span data-ttu-id="9dbff-301">Выполнение базовых операций с использованием кода библиотеки JavaScript в SharePoint</span><span class="sxs-lookup"><span data-stu-id="9dbff-301">Complete basic operations using JavaScript library code in SharePoint</span></span>](complete-basic-operations-using-javascript-library-code-in-sharepoint.md)
    
 
-  [<span data-ttu-id="9dbff-302">Разработка надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="9dbff-302">Develop SharePoint Add-ins</span></span>](develop-sharepoint-add-ins.md)
    
 
-  [<span data-ttu-id="9dbff-303">Создание сайтов для SharePoint</span><span class="sxs-lookup"><span data-stu-id="9dbff-303">Build sites for SharePoint</span></span>](http://msdn.microsoft.com/library/3b372a63-7cdf-462a-abb4-750e611e967d%28Office.15%29.aspx)
    
 

