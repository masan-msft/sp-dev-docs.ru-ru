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
# <a name="complete-basic-operations-using-sharepoint-client-library-code"></a><span data-ttu-id="95e32-103">Выполнение базовых операций с использованием кода клиентской библиотеки SharePoint</span><span class="sxs-lookup"><span data-stu-id="95e32-103">Complete basic operations using SharePoint client library code</span></span>


<span data-ttu-id="95e32-104">С помощью клиентской объектной модели SharePoint (CSOM) вы можете получать и изменять данные в SharePoint, а также управлять ими.</span><span class="sxs-lookup"><span data-stu-id="95e32-104">You can use the SharePoint client object model (CSOM) to retrieve, update, and manage data in SharePoint. SharePoint makes the CSOM available in several forms.</span></span> <span data-ttu-id="95e32-105">В SharePoint доступ к CSOM осуществляется несколькими путями:</span><span class="sxs-lookup"><span data-stu-id="95e32-105">SharePoint makes the CSOM available in several forms:</span></span> 

- <span data-ttu-id="95e32-106">через распространяемые сборки .NET Framework;</span><span class="sxs-lookup"><span data-stu-id="95e32-106">.NET Framework redistributable assemblies</span></span> 
- <span data-ttu-id="95e32-107">библиотеку JavaScript;</span><span class="sxs-lookup"><span data-stu-id="95e32-107">JavaScript library</span></span>
- <span data-ttu-id="95e32-108">конечные точки REST и OData;</span><span class="sxs-lookup"><span data-stu-id="95e32-108">REST/OData endpoints</span></span>
- <span data-ttu-id="95e32-109">сборки Windows Phone;</span><span class="sxs-lookup"><span data-stu-id="95e32-109">Windows Phone assemblies</span></span>
- <span data-ttu-id="95e32-110">распространяемые сборки Silverlight.</span><span class="sxs-lookup"><span data-stu-id="95e32-110">Silverlight redistributable assemblies</span></span>
    
<span data-ttu-id="95e32-111">Дополнительные сведения о наборах API, доступных на платформе SharePoint, см. в статье [Выбор правильного набора API в SharePoint](../general-development/choose-the-right-api-set-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="95e32-111">For more details about the sets of APIs available on the SharePoint platform, see  [Choose the right API set in SharePoint](../general-development/choose-the-right-api-set-in-sharepoint.md).</span></span> 

<span data-ttu-id="95e32-112">В этой статье описано, как выполнять базовые операции с использованием объектной модели .NET Framework, доступной в виде распространяемого пакета в Центре загрузки Майкрософт (найти его можно по запросу "SharePoint Server 2013 Client Components SDK" или "SharePoint Online Client Components SDK").</span><span class="sxs-lookup"><span data-stu-id="95e32-112">This article shows how to perform basic operations by using the .NET Framework object model, which is available as a redistributable package on the Microsoft Download Center (search for "SharePoint Server 2013 Client Components SDK" or "SharePoint Online Client Components SDK").</span></span> 

<span data-ttu-id="95e32-113">Сведения об использовании других клиентских API см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="95e32-113">For information about how to use the other client APIs, see:</span></span>

- [<span data-ttu-id="95e32-114">Выполнение базовых операций с использованием кода библиотеки JavaScript в SharePoint</span><span class="sxs-lookup"><span data-stu-id="95e32-114">Complete basic operations using JavaScript library code in SharePoint</span></span>](complete-basic-operations-using-javascript-library-code-in-sharepoint.md)
- [<span data-ttu-id="95e32-115">Выполнение базовых операций с использованием конечных точек REST в SharePoint</span><span class="sxs-lookup"><span data-stu-id="95e32-115">Complete basic operations using SharePoint REST endpoints</span></span>](complete-basic-operations-using-sharepoint-rest-endpoints.md)
- [<span data-ttu-id="95e32-116">Создание приложений Windows Phone с доступом к SharePoint</span><span class="sxs-lookup"><span data-stu-id="95e32-116">Build Windows Phone apps that access SharePoint</span></span>](../general-development/build-windows-phone-apps-that-access-sharepoint.md)
- <span data-ttu-id="95e32-117">[Использование объектной модели Silverlight](http://msdn.microsoft.com/library/cea7829d-f360-4052-8b76-91d90bcefd2a%28Office.15%29.aspx) в пакете SDK для SharePoint 2010</span><span class="sxs-lookup"><span data-stu-id="95e32-117">[Using the Silverlight Object Model](http://msdn.microsoft.com/library/cea7829d-f360-4052-8b76-91d90bcefd2a%28Office.15%29.aspx) in the SharePoint 2010 SDK</span></span>

<span data-ttu-id="95e32-118"><a name="BasicOps_SPCSOMOps"> </a></span><span class="sxs-lookup"><span data-stu-id="95e32-118"></span></span>

## <a name="basic-operations-with-the-sharepoint-net-client-object-model"></a><span data-ttu-id="95e32-119">Основные операции с клиентской объектной моделью .NET в SharePoint</span><span class="sxs-lookup"><span data-stu-id="95e32-119">Basic operations with the SharePoint .NET client object model</span></span>

<span data-ttu-id="95e32-120">В приведенных ниже разделах описаны задачи, которые вы можете выполнять программным путем. Они включают примеры кода на языке C#, в которых демонстрируются операции CSOM.</span><span class="sxs-lookup"><span data-stu-id="95e32-120">The following sections describe tasks that you can complete programmatically, and they include C# code examples that demonstrate CSOM operations.</span></span>

<span data-ttu-id="95e32-121">Когда вы создаете проект **Надстройка для SharePoint** в Visual Studio 2012, ссылки на сборки .NET Framework, **Microsoft.SharePoint.Client.Runtime.dll** и **Microsoft.SharePoint.Client.dll** автоматически добавляются в проект.</span><span class="sxs-lookup"><span data-stu-id="95e32-121">When you create an  **Add-in for SharePoint** project in Visual Studio 2012, references to the .NET Framework assemblies, **Microsoft.SharePoint.Client.Runtime.dll** and **Microsoft.SharePoint.Client.dll**, are automatically added to the project. For other kinds of projects, such as .NET Framework applications or console applications, you should add these references. The files are located on any SharePoint server at %ProgramFiles%\Common Files\Microsoft Shared\web server extensions\15\ISAPI.</span></span> <span data-ttu-id="95e32-122">Для других проектов, таких как приложения .NET Framework или консольные приложения, нужно добавить эти ссылки вручную.</span><span class="sxs-lookup"><span data-stu-id="95e32-122">For other kinds of projects, such as .NET Framework applications or console applications, you should add these references.</span></span> <span data-ttu-id="95e32-123">Эти файлы можно найти на любом сервере SharePoint, открыв папку %ProgramFiles%\Common Files\Microsoft Shared\web server extensions\15\ISAPI.</span><span class="sxs-lookup"><span data-stu-id="95e32-123">The files are located on any SharePoint server at %ProgramFiles%\Common Files\Microsoft Shared\web server extensions\15\ISAPI.</span></span>

<span data-ttu-id="95e32-124">Во всех этих примерах предполагается, что код находится в файле кода программной части для веб-страницы Microsoft ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="95e32-124">All of these examples assume that the code is in a code-behind file for an Microsoft ASP.NET webpage. You must add the following  using statement to the code file.</span></span> <span data-ttu-id="95e32-125">В файл кода необходимо добавить указанную ниже инструкцию **using**.</span><span class="sxs-lookup"><span data-stu-id="95e32-125">You must add the following **using** statement to the code file.</span></span>

```
using Microsoft.SharePoint.Client;
```

<span data-ttu-id="95e32-126">Если не указано иное, предполагается, что каждый из этих примеров относится к методу, не содержащему параметров и определенному в классе страницы.</span><span class="sxs-lookup"><span data-stu-id="95e32-126">Except where specified otherwise, you can assume that each of these examples is in a parameterless method that is defined in the page's class. Also,  ,  , and so on, are the names of  Label objects on the page.</span></span> <span data-ttu-id="95e32-127">Кроме того, `label1`, `label2` и т. д. — это имена объектов [Label](https://msdn.microsoft.com/ru-RU/library/620f4ses) на странице.</span><span class="sxs-lookup"><span data-stu-id="95e32-127">Also, `label1`, `label2`, and so on, are the names of [Label](https://msdn.microsoft.com/ru-RU/library/620f4ses) objects on the page.</span></span>
 
> [!NOTE] 
> <span data-ttu-id="95e32-128">Создавая размещаемую у поставщика надстройку SharePoint с использованием веб-приложения ASP.NET и добавляя ссылку на сборку в проект веб-приложения в Visual Studio, установите для свойства **Копировать локально** значение **True**, если не знаете, установлена ли сборка на веб-сервере, и не можете ее установить до развертывания надстройки.</span><span class="sxs-lookup"><span data-stu-id="95e32-128">Note  When you are making a provider-hosted SharePoint Add-in with an ASP.NET web application and you add a reference to an assembly to the web application project in Visual Studio, set the  **Copy Local** property of the assembly to **True**, unless you know that the assembly is already installed on the web server, or you can ensure that it is installed before you deploy your add-in. The .NET Framework is installed on Microsoft Azure Web Roles and Azure Web Sites. But the SharePoint client assemblies and the various Microsoft managed code extensions and foundations are not installed. Office Developer Tools for Visual Studio 2012 automatically adds references to some assemblies commonly used in SharePoint Add-ins and sets the  Copy Local property.</span></span> 

> <span data-ttu-id="95e32-129">Платформа .NET Framework установлена для веб-ролей Microsoft Azure и службы приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="95e32-129">The .NET Framework is installed on Microsoft Azure Web Roles and Azure Web Sites.</span></span> <span data-ttu-id="95e32-130">Но сборки клиента SharePoint, а также платформы и расширения управляемого кода Майкрософт не установлены.</span><span class="sxs-lookup"><span data-stu-id="95e32-130">But the SharePoint client assemblies and the various Microsoft managed code extensions and foundations are not installed.</span></span> <span data-ttu-id="95e32-131">Инструменты разработчика Office для Visual Studio 2012 автоматически добавляют ссылки на некоторые сборки, часто используемые в надстройках SharePoint, и устанавливают свойство **Копировать локально**.</span><span class="sxs-lookup"><span data-stu-id="95e32-131">Office Developer Tools for Visual Studio 2012 automatically adds references to some assemblies commonly used in SharePoint Add-ins and sets the **Copy Local** property.</span></span>

<span data-ttu-id="95e32-132"><a name="BasicOps_SPWebTasks"> </a></span><span class="sxs-lookup"><span data-stu-id="95e32-132"></span></span>

## <a name="sharepoint-website-tasks"></a><span data-ttu-id="95e32-133">Задачи, связанные с веб-сайтом SharePoint</span><span class="sxs-lookup"><span data-stu-id="95e32-133">SharePoint website tasks</span></span>

<span data-ttu-id="95e32-134">В этих примерах показано, как использовать модель CSOM .NET Framework для выполнения задач, связанных с веб-сайтами.</span><span class="sxs-lookup"><span data-stu-id="95e32-134">These examples show how to use the .NET Framework CSOM to complete website-related tasks.</span></span>

### <a name="retrieve-the-properties-of-a-website"></a><span data-ttu-id="95e32-135">Получите свойства веб-сайта</span><span class="sxs-lookup"><span data-stu-id="95e32-135">Retrieve the properties of a website</span></span>

<span data-ttu-id="95e32-136">Следующий код служит для получения названия веб-сайта SharePoint.</span><span class="sxs-lookup"><span data-stu-id="95e32-136">Retrieve the title of a SharePoint website.</span></span>


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

### <a name="retrieve-only-selected-properties-of-a-website"></a><span data-ttu-id="95e32-137">Получение определенных свойств веб-сайта</span><span class="sxs-lookup"><span data-stu-id="95e32-137">Retrieve only selected properties of a website</span></span>

<span data-ttu-id="95e32-138">Иногда клиенту нужны только несколько свойств объекта.</span><span class="sxs-lookup"><span data-stu-id="95e32-138">Sometimes, the client is interested only in a few properties of an object.</span></span> <span data-ttu-id="95e32-139">Для CSOM .NET Framework SharePoint не требуется получать с сервера все свойства объекта — вы можете использовать анонимные методы, например лямбда-выражения, для запроса определенных свойств.</span><span class="sxs-lookup"><span data-stu-id="95e32-139">The SharePoint .NET Framework CSOM does not require you to get all properties from the object on a server—you can use anonymous methods, which can be lambda expressions, to specifically request property names.</span></span> <span data-ttu-id="95e32-140">Клиентская библиотека запрашивает на сервере только эти свойства, и сервер отправляет клиенту только эти свойства.</span><span class="sxs-lookup"><span data-stu-id="95e32-140">The client library queries only for those properties on the server, and the server sends only those properties to the client.</span></span> <span data-ttu-id="95e32-141">Этот метод позволяет уменьшить объем ненужных данных, передаваемых между клиентом и сервером.</span><span class="sxs-lookup"><span data-stu-id="95e32-141">This technique reduces unnecessary data transfer between the client and the server.</span></span> <span data-ttu-id="95e32-142">Он также удобен, когда у пользователя нет разрешений на доступ к одному или нескольким неиспользуемым свойствам объекта.</span><span class="sxs-lookup"><span data-stu-id="95e32-142">It is also useful when the user does not have permission to one or more of the other, unused properties on an object.</span></span> 

<span data-ttu-id="95e32-143">Обратите внимание на то, что нужно добавить инструкцию **using** для пространства имен [System.Linq](https://msdn.microsoft.com/ru-RU/library/bb336768).</span><span class="sxs-lookup"><span data-stu-id="95e32-143">Note that you need to add a **using** statement for [System.Linq](https://msdn.microsoft.com/ru-RU/library/bb336768).</span></span>

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
> <span data-ttu-id="95e32-144">Если вы пытаетесь получить доступ к другим свойствам, код выдает исключение, потому что остальные свойства недоступны.</span><span class="sxs-lookup"><span data-stu-id="95e32-144">If you try to access other properties, the code throws an exception because other properties are not available.</span></span>
 
<br/>

### <a name="write-to-websites-properties"></a><span data-ttu-id="95e32-145">Запись значений для свойств веб-сайта</span><span class="sxs-lookup"><span data-stu-id="95e32-145">Write to website's properties</span></span>

<span data-ttu-id="95e32-146">В этом примере показано, как записать значения для свойств веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="95e32-146">This example shows how to write to the website's properties.</span></span>


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

### <a name="create-a-new-sharepoint-website"></a><span data-ttu-id="95e32-147">Создание веб-сайта SharePoint</span><span class="sxs-lookup"><span data-stu-id="95e32-147">Create a new SharePoint website</span></span>

<span data-ttu-id="95e32-148">В этом примере показано, как создать дочерний сайт текущего веб-сайта SharePoint.</span><span class="sxs-lookup"><span data-stu-id="95e32-148">This example shows how to create a new SharePoint site as a subsite of the current website.</span></span> <span data-ttu-id="95e32-149">Используйте класс **WebCreationInformation** для создания нового веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="95e32-149">Use the **WebCreationInformation** class to create a new website.</span></span> <span data-ttu-id="95e32-150">Нужно также добавить инструкцию **using** для пространств имен [System.Collections.Generic](https://msdn.microsoft.com/ru-RU/library/0sbxh9x2) и [System.Text](https://msdn.microsoft.com/ru-RU/library/x76y3wky).</span><span class="sxs-lookup"><span data-stu-id="95e32-150">You also need to add **using** statements for [System.Collections.Generic](https://msdn.microsoft.com/ru-RU/library/0sbxh9x2) and [System.Text](https://msdn.microsoft.com/ru-RU/library/x76y3wky).</span></span>

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

<span data-ttu-id="95e32-151"><a name="BasicOps_SPListTasks"> </a></span><span class="sxs-lookup"><span data-stu-id="95e32-151"></span></span>

## <a name="sharepoint-list-tasks"></a><span data-ttu-id="95e32-152">Задачи, связанные со списками SharePoint</span><span class="sxs-lookup"><span data-stu-id="95e32-152">SharePoint list tasks</span></span>

<span data-ttu-id="95e32-153">В этих примерах показано, как использовать модель CSOM .NET Framework для выполнения задач, связанных со списками.</span><span class="sxs-lookup"><span data-stu-id="95e32-153">These examples show how to use the .NET Framework CSOM to complete list-related tasks.</span></span>

### <a name="retrieve-all-sharepoint-lists-in-a-website"></a><span data-ttu-id="95e32-154">Получение всех списков SharePoint на сайте</span><span class="sxs-lookup"><span data-stu-id="95e32-154">Retrieve all SharePoint lists in a web</span></span>

<span data-ttu-id="95e32-155">В этом примере показано, как извлечь все списки SharePoint на веб-сайте SharePoint.</span><span class="sxs-lookup"><span data-stu-id="95e32-155">This example retrieves all SharePoint lists in a SharePoint website.</span></span> <span data-ttu-id="95e32-156">Чтобы выполнить компиляцию, нужно добавить инструкцию **using** для пространства имен [System.Linq](http://msdn.microsoft.com/ru-RU/library/bb336768).</span><span class="sxs-lookup"><span data-stu-id="95e32-156">This example retrieves all SharePoint lists in a SharePoint website. To compile this code you will need to add a  **using** statement for [System.Linq](http://msdn.microsoft.com/ru-RU/library/bb336768).</span></span>

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
> <span data-ttu-id="95e32-157">Вместо свойства **web.Lists** можно использовать метод **LoadQuery**, чтобы хранить возвращаемое значения в другой коллекции.</span><span class="sxs-lookup"><span data-stu-id="95e32-157">Alternatively, you can use the **LoadQuery** method to store the return value in another collection, rather than use the **web.Lists** property.</span></span> <span data-ttu-id="95e32-158">Вам также потребуется добавить инструкцию **using** для пространств имен [System.Collections.Generic](http://msdn.microsoft.com/ru-RU/library/0sbxh9x2) и [System.Linq](http://msdn.microsoft.com/ru-RU/library/bb336768).</span><span class="sxs-lookup"><span data-stu-id="95e32-158">You will also need to add **using** statements for [System.Collections.Generic](http://msdn.microsoft.com/ru-RU/library/0sbxh9x2) and [System.Linq](http://msdn.microsoft.com/ru-RU/library/bb336768).</span></span> <span data-ttu-id="95e32-159">Добавьте также псевдоним в инструкцию using для пространства имен **Microsoft.SharePoint.Client**, чтобы однозначно ссылаться на его классы.</span><span class="sxs-lookup"><span data-stu-id="95e32-159">This example adds a field to a SharePoint list. add an alias to the using statement for  **Microsoft.SharePoint.Client** namespace so you can refer to its classes unambiguously. For example, .</span></span> <span data-ttu-id="95e32-160">Пример: `using SP = Microsoft.SharePoint.Client;`.</span><span class="sxs-lookup"><span data-stu-id="95e32-160">For example: `using SP = Microsoft.SharePoint.Client;`.</span></span>
 
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

### <a name="create-and-update-a-sharepoint-list"></a><span data-ttu-id="95e32-161">Создание и обновление списка SharePoint</span><span class="sxs-lookup"><span data-stu-id="95e32-161">Create and update a SharePoint list</span></span>

<span data-ttu-id="95e32-162">В этом примере список SharePoint создается и обновляется с помощью класса **ListCreationInformation**.</span><span class="sxs-lookup"><span data-stu-id="95e32-162">This example creates a SharePoint list and updates it using the  **ListCreationInformation** class.</span></span>

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

### <a name="delete-a-sharepoint-list"></a><span data-ttu-id="95e32-163">Удаление списка SharePoint</span><span class="sxs-lookup"><span data-stu-id="95e32-163">Delete a SharePoint list</span></span>

<span data-ttu-id="95e32-164">В этом примере удаляется список SharePoint.</span><span class="sxs-lookup"><span data-stu-id="95e32-164">This example deletes a SharePoint list.</span></span>

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

### <a name="add-a-field-to-a-sharepoint-list"></a><span data-ttu-id="95e32-165">Добавление поля в список SharePoint</span><span class="sxs-lookup"><span data-stu-id="95e32-165">Add a field to a SharePoint list</span></span>

<span data-ttu-id="95e32-166">В этом примере показано, как добавить поле в список SharePoint.</span><span class="sxs-lookup"><span data-stu-id="95e32-166">This example adds a field to a SharePoint list.</span></span> <span data-ttu-id="95e32-167">Добавьте псевдоним в инструкцию using для пространства имен **Microsoft.SharePoint.Client**, чтобы однозначно ссылаться на его классы.</span><span class="sxs-lookup"><span data-stu-id="95e32-167">This example adds a field to a SharePoint list. add an alias to the using statement for  **Microsoft.SharePoint.Client** namespace so you can refer to its classes unambiguously. For example, .</span></span> <span data-ttu-id="95e32-168">Пример: `using SP = Microsoft.SharePoint.Client;`.</span><span class="sxs-lookup"><span data-stu-id="95e32-168">For example: `using SP = Microsoft.SharePoint.Client;`.</span></span>
 
> [!NOTE] 
> <span data-ttu-id="95e32-169">В этом примере для приведения типа используется метод **context.CastTo**.</span><span class="sxs-lookup"><span data-stu-id="95e32-169">The example uses **context.CastTo** to do a cast.</span></span> <span data-ttu-id="95e32-170">Перед выполнением запроса клиентская библиотека не знает тип возвращаемого объекта, и единственным возможным типом является **SharePoint.Field**.</span><span class="sxs-lookup"><span data-stu-id="95e32-170">Note  The example uses  context.CastTo to do a cast. Before executing the query, the client library does not know the real type of the returned object "field" and **SharePoint.Field** is the only possible type. If you know the real type, you can use the ClientContext.CastTo method to cast the object.</span></span> <span data-ttu-id="95e32-171">Если вы знаете тип объекта, можете выполнить его приведение, используя метод **ClientContext.CastTo<RealType>**.</span><span class="sxs-lookup"><span data-stu-id="95e32-171">If you know the real type, you can use the **ClientContext.CastTo<RealType>** method to cast the object.</span></span>

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

<span data-ttu-id="95e32-172"><a name="BasicOps_SPListItemTasks"> </a></span><span class="sxs-lookup"><span data-stu-id="95e32-172"></span></span>

## <a name="sharepoint-list-item-tasks"></a><span data-ttu-id="95e32-173">Задачи, связанные с элементами списков SharePoint</span><span class="sxs-lookup"><span data-stu-id="95e32-173">SharePoint list item tasks</span></span>

<span data-ttu-id="95e32-174">В этих примерах демонстрируется использование модели CSOM .NET Framework для выполнения задач, связанных с элементами списков.</span><span class="sxs-lookup"><span data-stu-id="95e32-174">These examples demonstrate how to use the .NET Framework CSOM to complete tasks that are related to list items.</span></span>

### <a name="retrieve-items-from-a-sharepoint-list"></a><span data-ttu-id="95e32-175">Получение элементов из списка SharePoint</span><span class="sxs-lookup"><span data-stu-id="95e32-175">Retrieve items from a SharePoint list</span></span>

<span data-ttu-id="95e32-176">В этом примере показано, как извлечь элементы из списка SharePoint.</span><span class="sxs-lookup"><span data-stu-id="95e32-176">This example retrieves the items in a SharePoint list.</span></span> <span data-ttu-id="95e32-177">Вам также потребуется добавить инструкцию **using** для пространства имен **Microsoft.SharePoint.Client.QueryExpression**.</span><span class="sxs-lookup"><span data-stu-id="95e32-177">This example retrieves the items in a SharePoint list. You will also need to add a  **using** statement for **Microsoft.SharePoint.Client.QueryExpression**.</span></span>
 
> [!NOTE] 
> <span data-ttu-id="95e32-178">С помощью свойства **FolderServerRelativeUrl** вы можете ограничить возвращаемые элементы только теми, которые находятся в указанной папке.</span><span class="sxs-lookup"><span data-stu-id="95e32-178">Note  You can use the  **FolderServerRelativeUrl** property to further restrict the items that are returned to those in a specified folder.</span></span>

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

### <a name="create-a-new-list-item"></a><span data-ttu-id="95e32-179">Создание элемента списка</span><span class="sxs-lookup"><span data-stu-id="95e32-179">Create a new list item</span></span>

<span data-ttu-id="95e32-180">В этом примере список SharePoint создается с помощью класса **ListItemCreationInformation**.</span><span class="sxs-lookup"><span data-stu-id="95e32-180">This example creates a new SharePoint list item using the  **ListItemCreationInformation** class.</span></span>

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

### <a name="update-a-list-item"></a><span data-ttu-id="95e32-181">Обновление элемента списка</span><span class="sxs-lookup"><span data-stu-id="95e32-181">Update a list item</span></span>

<span data-ttu-id="95e32-182">В этом примере обновляется элемент списка SharePoint.</span><span class="sxs-lookup"><span data-stu-id="95e32-182">This example updates a SharePoint list item.</span></span>

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

### <a name="delete-a-list-item"></a><span data-ttu-id="95e32-183">Удаление элемента списка</span><span class="sxs-lookup"><span data-stu-id="95e32-183">Delete a list item</span></span>

<span data-ttu-id="95e32-184">В этом примере удаляется элемент списка SharePoint.</span><span class="sxs-lookup"><span data-stu-id="95e32-184">This example deletes a SharePoint list item.</span></span>

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

<span data-ttu-id="95e32-185"><a name="BasicOps_SPFieldTasks"> </a></span><span class="sxs-lookup"><span data-stu-id="95e32-185"></span></span>

## <a name="sharepoint-field-tasks"></a><span data-ttu-id="95e32-186">Задачи, связанные с полями SharePoint</span><span class="sxs-lookup"><span data-stu-id="95e32-186">SharePoint field tasks</span></span>

<span data-ttu-id="95e32-187">В этих примерах показано, как использовать модель CSOM .NET Framework в SharePoint для выполнения задач, связанных с полями.</span><span class="sxs-lookup"><span data-stu-id="95e32-187">These examples show how to use the SharePoint .NET Framework CSOM to complete field-related tasks.</span></span> 

### <a name="retrieve-all-of-the-fields-in-a-list"></a><span data-ttu-id="95e32-188">Получение всех полей в списке</span><span class="sxs-lookup"><span data-stu-id="95e32-188">Retrieve all of the fields in a list</span></span>

<span data-ttu-id="95e32-189">В этом примере показано, как получить все поля в списке SharePoint.</span><span class="sxs-lookup"><span data-stu-id="95e32-189">This example retrieves the versions of a listItem in a SharePoint list:</span></span> <span data-ttu-id="95e32-190">Кроме того, добавьте псевдоним в инструкцию **using** для пространства имен **Microsoft.SharePoint.Client**, чтобы однозначно ссылаться на его классы. Пример: `using SP = Microsoft.SharePoint.Client;`.</span><span class="sxs-lookup"><span data-stu-id="95e32-190">This example retrieves all of the fields in a SharePoint list. You will also need to add an alias to the **using** statement for the **Microsoft.SharePoint.Client** namespace so you can refer to its classes unambiguously; for example, `using SP = Microsoft.SharePoint.Client;`.</span></span>

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

### <a name="retrieve-a-specific-field-from-the-list"></a><span data-ttu-id="95e32-191">Получение определенного поля из списка</span><span class="sxs-lookup"><span data-stu-id="95e32-191">Retrieve a specific field from the list</span></span>

<span data-ttu-id="95e32-192">Если вы хотите получить информацию о конкретном поле, используйте метод **Fields.GetByInternalNameOrTitle**.</span><span class="sxs-lookup"><span data-stu-id="95e32-192">If you want to retrieve information about a specific field, use the **Fields.GetByInternalNameOrTitle** method.</span></span> <span data-ttu-id="95e32-193">Тип возвращаемого значения этого метода — **Field**.</span><span class="sxs-lookup"><span data-stu-id="95e32-193">The return type of this method is **Field**.</span></span> <span data-ttu-id="95e32-194">Перед выполнением запроса клиент не знает тип объекта, и синтаксис C# недоступен для его приведения к производному типу.</span><span class="sxs-lookup"><span data-stu-id="95e32-194">Before the query is executed, the client does not know the type of object, and C# syntax is not available for casting it to the derived type.</span></span> <span data-ttu-id="95e32-195">Поэтому используйте для его приведения метод **ClientContext.CastTo**, который дает клиентской библиотеке указание воссоздать объект.</span><span class="sxs-lookup"><span data-stu-id="95e32-195">Therefore, use the **ClientContext.CastTo** method to cast it, which instructs the client library to recreate an object.</span></span> <span data-ttu-id="95e32-196">Нужно также добавить инструкцию **using** для пространства имен [System.Collections.Generic](http://msdn.microsoft.com/ru-RU/library/0sbxh9x2).</span><span class="sxs-lookup"><span data-stu-id="95e32-196">You also need to add a **using** statement for [System.Collections.Generic](http://msdn.microsoft.com/ru-RU/library/0sbxh9x2).</span></span> <span data-ttu-id="95e32-197">Кроме того, добавьте псевдоним в инструкцию **using** для пространства имен **Microsoft.SharePoint.Client**, чтобы однозначно ссылаться на его классы.</span><span class="sxs-lookup"><span data-stu-id="95e32-197">This example adds a field to a SharePoint list. add an alias to the using statement for  **Microsoft.SharePoint.Client** namespace so you can refer to its classes unambiguously. For example, ****.</span></span> <span data-ttu-id="95e32-198">Пример: `using SP = Microsoft.SharePoint.Client;`.</span><span class="sxs-lookup"><span data-stu-id="95e32-198">For example: `using SP = Microsoft.SharePoint.Client;`.</span></span>
 
> [!NOTE] 
> <span data-ttu-id="95e32-199">Метод **GetByInternalNameOrTitle**, используемый в этом примере, является удаленным.</span><span class="sxs-lookup"><span data-stu-id="95e32-199">The **GetByInternalNameOrTitle** method used in this example is a remote method.</span></span> <span data-ttu-id="95e32-200">Он не использует данные из клиентской коллекции, даже если она уже заполнена.</span><span class="sxs-lookup"><span data-stu-id="95e32-200">Note  The  GetByInternalNameOrTitle method used in this example is a remote method. It does not use the data from the client collection even if the client collection is already populated.</span></span>

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

<span data-ttu-id="95e32-201"><a name="BasicOps_SPSecurityTasks"> </a></span><span class="sxs-lookup"><span data-stu-id="95e32-201"></span></span>

## <a name="sharepoint-user-tasks"></a><span data-ttu-id="95e32-202">Задачи, связанные с пользователями SharePoint</span><span class="sxs-lookup"><span data-stu-id="95e32-202">SharePoint user tasks</span></span>

<span data-ttu-id="95e32-203">Вы можете использовать модель CSOM .NET Framework в SharePoint для управления пользователями и группами SharePoint, а также безопасностью пользователей.</span><span class="sxs-lookup"><span data-stu-id="95e32-203">You can use the SharePoint .NET Framework CSOM to manage SharePoint users, groups, and user security.</span></span> 

### <a name="add-a-user-to-a-sharepoint-group"></a><span data-ttu-id="95e32-204">Добавление пользователя в группу SharePoint</span><span class="sxs-lookup"><span data-stu-id="95e32-204">Add a user to a SharePoint group</span></span>

<span data-ttu-id="95e32-205">В этом примере в группу SharePoint с именем Members добавляется пользователь и некоторые сведения о нем.</span><span class="sxs-lookup"><span data-stu-id="95e32-205">This example adds a user and some user information to a SharePoint group named Members.</span></span>

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

### <a name="retrieve-all-users-in-a-sharepoint-group"></a><span data-ttu-id="95e32-206">Получение всех пользователей из группы SharePoint</span><span class="sxs-lookup"><span data-stu-id="95e32-206">Retrieve all users in a SharePoint group</span></span>

<span data-ttu-id="95e32-207">В этом примере извлекаются сведения о всех пользователях в группе SharePoint с именем Members.</span><span class="sxs-lookup"><span data-stu-id="95e32-207">This example retrieves information about all users from a SharePoint group named Members.</span></span>

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

### <a name="create-a-role"></a><span data-ttu-id="95e32-208">Создание роли</span><span class="sxs-lookup"><span data-stu-id="95e32-208">Create a role</span></span>

<span data-ttu-id="95e32-209">В этом примере создается роль, имеющая разрешения на создание оповещений и управление ими.</span><span class="sxs-lookup"><span data-stu-id="95e32-209">This example creates a role that has create and manage alerts permissions.</span></span>

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

### <a name="add-a-user-to-a-role"></a><span data-ttu-id="95e32-210">Добавление пользователя к роли</span><span class="sxs-lookup"><span data-stu-id="95e32-210">Add a user to a role</span></span>

<span data-ttu-id="95e32-211">В этом примере к роли добавляется пользователь.</span><span class="sxs-lookup"><span data-stu-id="95e32-211">This example adds a user to a role.</span></span>

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

<span data-ttu-id="95e32-212"><a name="Best"> </a></span><span class="sxs-lookup"><span data-stu-id="95e32-212"></span></span>

## <a name="rules-and-best-practices-for-using-the-sharepoint-net-client-object-model"></a><span data-ttu-id="95e32-213">Правила и рекомендации по клиентской объектной модели .NET в SharePoint</span><span class="sxs-lookup"><span data-stu-id="95e32-213">Rules and best practices for using the SharePoint .NET client object model</span></span>

<span data-ttu-id="95e32-214">В этих примерах демонстрируются некоторые важные рекомендации и требования, которые следует соблюдать при использовании модели CSOM .NET Framework в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="95e32-214">These examples illustrate some important best practices and requirements you should conform to when using the SharePoint .NET Framework CSOM.</span></span>

### <a name="call-clientcontextexecutequery-before-accessing-any-value-properties"></a><span data-ttu-id="95e32-215">Вызов метода ClientContext.ExecuteQuery перед доступом к свойствам значений</span><span class="sxs-lookup"><span data-stu-id="95e32-215">Call ClientContext.ExecuteQuery before accessing any value properties</span></span>

<span data-ttu-id="95e32-216">Модель CSOM SharePoint .NET Framework требует использования шаблона программирования наподобие SQL: необходимо объявить запрос и выполнить его перед доступом к данным.</span><span class="sxs-lookup"><span data-stu-id="95e32-216">The SharePoint .NET Framework CSOM requires that you use a SQL-like programming pattern: declare what you want and execute the query before you access the data. For example, the following code, attempts to display the SharePoint website's title, will throw an exception.</span></span> <span data-ttu-id="95e32-217">Например, при выполнении следующего кода, который пытается отобразить название веб-сайта SharePoint, выдается исключение.</span><span class="sxs-lookup"><span data-stu-id="95e32-217">For example, the following code, which attempts to display the SharePoint website's title, throws an exception.</span></span>


```C#
// Starting with ClientContext, the constructor requires a URL to the 
// server running SharePoint. 
ClientContext context = new ClientContext("http://SiteUrl"); 

Web web = context.Web; 
label1.Text = web.Title;  

```

<br/>

<span data-ttu-id="95e32-218">Сбой произойдет по той причине, что в коде CSOM .NET Framework в SharePoint необходимо выполнить следующие действия:</span><span class="sxs-lookup"><span data-stu-id="95e32-218">This code fails because SharePoint .NET Framework CSOM code must:</span></span>

- <span data-ttu-id="95e32-219">создать прямой запрос SQL или хранимую процедуру;</span><span class="sxs-lookup"><span data-stu-id="95e32-219">Build either an ad hoc SQL query or a stored procedure.</span></span>
- <span data-ttu-id="95e32-220">выполнить запрос SQL;</span><span class="sxs-lookup"><span data-stu-id="95e32-220">Execute the SQL query.</span></span>
- <span data-ttu-id="95e32-221">прочитать результаты из SQL.</span><span class="sxs-lookup"><span data-stu-id="95e32-221">Read results from SQL.</span></span>
    
<span data-ttu-id="95e32-222">В модели CSOM SharePoint .NET Framework при вызове метода создается запрос.</span><span class="sxs-lookup"><span data-stu-id="95e32-222">In SharePoint .NET Framework CSOM, when you call a method, you build a query.</span></span> <span data-ttu-id="95e32-223">Запросы накапливаются и не отправляются на сервер, пока не будет вызван метод **ExecuteQuery**.</span><span class="sxs-lookup"><span data-stu-id="95e32-223">Queries accumulate and are not sent to the server until  **ExecuteQuery** is called.</span></span> 

<span data-ttu-id="95e32-224">Ниже показано код, необходимый для отображения названия веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="95e32-224">The following example shows the code that is required to display the website's title.</span></span> <span data-ttu-id="95e32-225">Кроме того, нужно добавить инструкцию **using** для пространства имен [System.Linq](http://msdn.microsoft.com/ru-RU/library/bb336768).</span><span class="sxs-lookup"><span data-stu-id="95e32-225">You also need to add a **using** statement for [System.Linq](http://msdn.microsoft.com/ru-RU/library/bb336768).</span></span> <span data-ttu-id="95e32-226">Добавьте также псевдоним в инструкцию **using** для пространства имен **Microsoft.SharePoint.Client**, чтобы однозначно ссылаться на его классы.</span><span class="sxs-lookup"><span data-stu-id="95e32-226">This example adds a field to a SharePoint list. add an alias to the using statement for  **Microsoft.SharePoint.Client** namespace so you can refer to its classes unambiguously. For example, ****.</span></span> <span data-ttu-id="95e32-227">Пример: `using SP = Microsoft.SharePoint.Client;`.</span><span class="sxs-lookup"><span data-stu-id="95e32-227">For example: `using SP = Microsoft.SharePoint.Client;`.</span></span>
 

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

<span data-ttu-id="95e32-228">Отличие состоит в том, что добавляются указанные ниже строки. Первая из них создает запрос на получение свойства **Title**.</span><span class="sxs-lookup"><span data-stu-id="95e32-228">The differences are the addition of these lines; the first line creates a query for the web's **Title** property.</span></span> <span data-ttu-id="95e32-229">Вторая строка выполняет запрос.</span><span class="sxs-lookup"><span data-stu-id="95e32-229">The second line executes the query.</span></span> 

```
context.Load(web, w => w.Title); 
context.ExecuteQuery(); 

```

<br/>

### <a name="do-not-use-value-objects-returned-from-methods-or-properties-in-the-same-query"></a><span data-ttu-id="95e32-230">Не используйте объекты значений, возвращенные методами или свойствами, в том же запросе</span><span class="sxs-lookup"><span data-stu-id="95e32-230">Do not use value objects returned from methods or properties in the same query</span></span>

<span data-ttu-id="95e32-231">Объект значения, возвращаемый методом или свойством, можно использовать только после выполнения запроса.</span><span class="sxs-lookup"><span data-stu-id="95e32-231">When a value object is returned from a method or property, you cannot use that object until after you have executed the query. For example, the following code tries to create a SharePoint list that has the same title as the parent website, but it will throw an exception.</span></span> <span data-ttu-id="95e32-232">Например, приведенный ниже код пытается создать список SharePoint с тем же названием, что и у родительского веб-сайта, но выдается исключение.</span><span class="sxs-lookup"><span data-stu-id="95e32-232">When a value object is returned from a method or property, you cannot use that object until after you have executed the query. For example, the following code tries to create a SharePoint list that has the same title as the parent website, but it will throw an exception.</span></span> 

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

<span data-ttu-id="95e32-233">Исключение выдается, так как свойство недоступно до выполнения запроса.</span><span class="sxs-lookup"><span data-stu-id="95e32-233">An exception is thrown because the property is not available before you execute the query.</span></span> <span data-ttu-id="95e32-234">В SQL можно объявить локальную переменную для хранения значения `web.Title` и использовать ее для создания сайта.</span><span class="sxs-lookup"><span data-stu-id="95e32-234">In SQL, you would declare a local variable to hold the value for `web.Title` and use the local variable for web creation.</span></span> <span data-ttu-id="95e32-235">В клиентской библиотеке создать локальную переменную нельзя.</span><span class="sxs-lookup"><span data-stu-id="95e32-235">In the client library, you can't create a local variable.</span></span> <span data-ttu-id="95e32-236">Вам нужно разбить действие на два отдельных запроса, как показано в приведенном ниже примере.</span><span class="sxs-lookup"><span data-stu-id="95e32-236">You have to split functionality into two separate queries as is shown in the following example.</span></span> <span data-ttu-id="95e32-237">Кроме того, нужно добавить инструкцию **using** для пространства имен [System.Linq](http://msdn.microsoft.com/ru-RU/library/bb336768).</span><span class="sxs-lookup"><span data-stu-id="95e32-237">You also need to add a **using** statement for [System.Linq](http://msdn.microsoft.com/ru-RU/library/bb336768).</span></span> <span data-ttu-id="95e32-238">Добавьте также псевдоним в инструкцию using для пространства имен **Microsoft.SharePoint.Client**, чтобы однозначно ссылаться на его классы.</span><span class="sxs-lookup"><span data-stu-id="95e32-238">This example adds a field to a SharePoint list. add an alias to the using statement for  **Microsoft.SharePoint.Client** namespace so you can refer to its classes unambiguously. For example, .</span></span> <span data-ttu-id="95e32-239">Пример: `using SP = Microsoft.SharePoint.Client;`.</span><span class="sxs-lookup"><span data-stu-id="95e32-239">For example: `using SP = Microsoft.SharePoint.Client;`.</span></span>

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

<span data-ttu-id="95e32-240">Отличие заключается в следующих трех строках:</span><span class="sxs-lookup"><span data-stu-id="95e32-240">The difference is the following three lines:</span></span>

```C#
context.Load(web, w => w.Title); 
context.ExecuteQuery(); 
...
context.ExecuteQuery(); 

```

<br/>

### <a name="using-methods-or-properties-that-return-client-objects-in-another-method-call-in-the-same-query"></a><span data-ttu-id="95e32-241">Использование методов или свойств, возвращающих клиентские объекты, в вызове другого метода в том же запросе</span><span class="sxs-lookup"><span data-stu-id="95e32-241">Using methods or properties that return client objects in another method call in the same query</span></span>

<span data-ttu-id="95e32-242">В отличие от объекта значения, клиентский объект можно использовать в вызове другого метода в том же запросе.</span><span class="sxs-lookup"><span data-stu-id="95e32-242">Unlike a value object, a client object can be used in another method call in the same query.</span></span> 

<span data-ttu-id="95e32-p122">В удаленной среде .NET объект значения представляет собой класс или структуру, маршалируемую по значению, а клиентский объект класс или структуру, маршалируемую по ссылке. Например, **ListItem** это клиентский объект, а **UrlFieldValue** и другие значения полей это объекты значений.</span><span class="sxs-lookup"><span data-stu-id="95e32-p122">In .NET remoting, the value object is a class or struct that is marshaled by value, while the client object is a class or struct that is marshaled by reference. For example, the **ListItem** is a client object, while the **UrlFieldValue** and other field values are value objects.</span></span>

<span data-ttu-id="95e32-245">В клиентской библиотеке соответствующий объект сервера имеет атрибут `[ClientCallable(ValueObject = true)]`.</span><span class="sxs-lookup"><span data-stu-id="95e32-245">In the client library, the corresponding server object has the `[ClientCallable(ValueObject = true)]` attribute.</span></span> <span data-ttu-id="95e32-246">Эти значения могут иметь только свойства и не иметь методов.</span><span class="sxs-lookup"><span data-stu-id="95e32-246">Those values could have only properties and no methods.</span></span> <span data-ttu-id="95e32-247">Примитивные типы, такие как строки и целочисленные значения, обрабатываются как объекты значений.</span><span class="sxs-lookup"><span data-stu-id="95e32-247">Primitive types, such as strings and ints, are treated as value objects.</span></span> <span data-ttu-id="95e32-248">Для всех значений выполняется маршалинг между клиентом и сервером.</span><span class="sxs-lookup"><span data-stu-id="95e32-248">All the values are marshaled between the client and the server.</span></span> <span data-ttu-id="95e32-249">Значение **ValueObject** по умолчанию — **false**.</span><span class="sxs-lookup"><span data-stu-id="95e32-249">The default value of the **ValueObject** is **false**.</span></span> 

<span data-ttu-id="95e32-p124">Альтернативой объекту значения является клиентский объект. Если соответствующий серверный объект имеет атрибут **[ClientCallable(ValueObject = false)]**, объект является клиентским. Процесс создания клиентских объектов отслеживается. В реализации клиентской библиотеки для этого используется класс **ObjectPath**. Например, имеется следующий код.</span><span class="sxs-lookup"><span data-stu-id="95e32-p124">The counterpart to the value object is the client object. If the corresponding server object has the **[ClientCallable(ValueObject = false)]** attribute, the object is a client object. For client objects, we keep track of how the object is created; this is called **ObjectPath** in the client library implementation. For example, if we have code like the following:</span></span>

```C#
ClientContext context = new ClientContext("http://SiteUrl"); 
Web web = context.Web; 
SP.List list = web.Lists.GetByTitle("Announcements"); 

```

<span data-ttu-id="95e32-254">Мы знаем, что список создается следующим образом:</span><span class="sxs-lookup"><span data-stu-id="95e32-254">We know that the list is created by:</span></span>

- <span data-ttu-id="95e32-255">Свойство **Web** извлекается из контекста.</span><span class="sxs-lookup"><span data-stu-id="95e32-255">Getting the **Web** property from the context.</span></span>
- <span data-ttu-id="95e32-256">Из полученного выше свойства извлекается свойство **Lists**.</span><span class="sxs-lookup"><span data-stu-id="95e32-256">Getting the **Lists** property from the above result.</span></span>
- <span data-ttu-id="95e32-257">Для полученного выше свойства вызывается метод **GetByTitle** с параметром _Announcements_.</span><span class="sxs-lookup"><span data-stu-id="95e32-257">Invoking the **GetByTitle** method with the _Announcements_ parameter from the above result.</span></span>
    
 
<span data-ttu-id="95e32-258">Когда модель CSOM SharePoint .NET Framework передает эту информацию на сервер, вы можете воссоздать объект на сервере.</span><span class="sxs-lookup"><span data-stu-id="95e32-258">When the SharePoint .NET Framework CSOM passes this information to the server, you can recreate the object on the server.</span></span> <span data-ttu-id="95e32-259">В клиентской библиотеке вы можете отслеживать **ObjectPath**, созданный объектом клиента.</span><span class="sxs-lookup"><span data-stu-id="95e32-259">In the client library, you can keep track of the **ObjectPath** that the client object created.</span></span> <span data-ttu-id="95e32-260">Вы знаете, как создан объект, поэтому можете использовать его как параметр для вызова других методов в том же запросе.</span><span class="sxs-lookup"><span data-stu-id="95e32-260">Because you know how the object is created, you could use the object as a parameter to invoke other methods within the same query.</span></span>

### <a name="group-data-retrieval-on-the-same-object-together-to-improve-performance"></a><span data-ttu-id="95e32-261">Получение сгруппированных данных из одного объекта для повышения производительности</span><span class="sxs-lookup"><span data-stu-id="95e32-261">Group data retrieval on the same object together to improve performance</span></span>

<span data-ttu-id="95e32-262">Следует пытаться получить все данные из одного объекта в одном запросе, то есть с помощью одного вызова метода **Load<T>(T, [])**.</span><span class="sxs-lookup"><span data-stu-id="95e32-262">When reading multiple pieces of data from the same object, you should try to get all of it in a single query; that is, a single call to the  **Load<T>(T, [])** method.</span></span> <span data-ttu-id="95e32-263">В приведенном ниже коде показаны два способа получения названия и описания веб-сайта, а также описания списка **Announcements**.</span><span class="sxs-lookup"><span data-stu-id="95e32-263">The following code shows two ways to retrieve a website's title and description and the **Announcements** list's description.</span></span> <span data-ttu-id="95e32-264">Чтобы выполнить компиляцию, нужно добавить инструкцию **using** для пространства имен [System.Linq](http://msdn.microsoft.com/ru-RU/library/bb336768).</span><span class="sxs-lookup"><span data-stu-id="95e32-264">This example retrieves all SharePoint lists in a SharePoint website. To compile this code you will need to add a  **using** statement for [System.Linq](http://msdn.microsoft.com/ru-RU/library/bb336768).</span></span> <span data-ttu-id="95e32-265">Кроме того, добавьте псевдоним в инструкцию **using** для пространства имен **Microsoft.SharePoint.Client**, чтобы однозначно ссылаться на его классы.</span><span class="sxs-lookup"><span data-stu-id="95e32-265">This example adds a field to a SharePoint list. add an alias to the using statement for  **Microsoft.SharePoint.Client** namespace so you can refer to its classes unambiguously. For example, ****.</span></span> <span data-ttu-id="95e32-266">Пример: `using SP = Microsoft.SharePoint.Client;`.</span><span class="sxs-lookup"><span data-stu-id="95e32-266">For example: `using SP = Microsoft.SharePoint.Client;`.</span></span> 

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

<span data-ttu-id="95e32-267">Они не являются одинаково эффективными.</span><span class="sxs-lookup"><span data-stu-id="95e32-267">These are not equally efficient.</span></span> <span data-ttu-id="95e32-268">В методе **Method1** код для извлечения названия и описания сайта сгруппирован.</span><span class="sxs-lookup"><span data-stu-id="95e32-268">In **Method1**, the code to retrieve the web's title and description is grouped together.</span></span> <span data-ttu-id="95e32-269">В методе **Method2** код для извлечения названия и описания сайта разделен другими действиями.</span><span class="sxs-lookup"><span data-stu-id="95e32-269">In **Method2**, the code to retrieve the web's title and description is separated by other actions.</span></span> <span data-ttu-id="95e32-270">Это означает, что метод **Method2** инициирует два отдельных запроса к одному веб-объекту и по нему возвращается два набора результатов.</span><span class="sxs-lookup"><span data-stu-id="95e32-270">This means that **Method2** triggers two separated queries on the same web object, and there are two result sets for the same web.</span></span> <span data-ttu-id="95e32-271">Так как клиентская библиотека пытается возвращать согласованные данные, второй набор результатов включает как название, так и описание.</span><span class="sxs-lookup"><span data-stu-id="95e32-271">Because the client library tries to return consistent data, the second result set includes both the title and description.</span></span> <span data-ttu-id="95e32-272">Предыдущий код можно представить следующим образом.</span><span class="sxs-lookup"><span data-stu-id="95e32-272">You could think of the previous code as the following.</span></span>

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

### <a name="specify-which-properties-of-objects-you-want-to-return"></a><span data-ttu-id="95e32-273">Указание свойств объектов, которые необходимо вернуть</span><span class="sxs-lookup"><span data-stu-id="95e32-273">Specify which properties of objects you want to return</span></span>

<span data-ttu-id="95e32-p128">В серверной объектной модели SharePoint при получении объекта **SPWeb** вы можете просмотреть все его свойства. В SQL для получения всех столбцов таблицы можно выполнить следующий запрос.</span><span class="sxs-lookup"><span data-stu-id="95e32-p128">In the SharePoint server object model, if you get an **SPWeb** object, you can inspect all of its properties. In SQL, to get all of the columns of a table you can run:</span></span>

```
SELECT * FROM Webs 
```

<span data-ttu-id="95e32-p129">В клиентской библиотеке ни метод **Load<T>**, ни какой-либо другой метод не возвращает всех свойств, поэтому необходимо явным образом указать требуемые данные. Например, следующий код получает объект веб-сайта, но возвращаемые свойства не указаны. Далее он пытается прочесть два свойства, однако одно из них не относится с свойствам, которые возвращаются методом **Load** автоматически. Создается исключение.</span><span class="sxs-lookup"><span data-stu-id="95e32-p129">In the client library, neither **Load<T>** nor any other method returns all properties, so you have to explicitly specify what you want. For example, the following code retrieves the website object without specifying which properties to return. It then tries to read two properties and one of them is not among the properties that is automatically returned by **Load**. This code throws an exception.</span></span> 

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

<span data-ttu-id="95e32-280">Для успешной компиляции кода обновите его так, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="95e32-280">To get the code to compile successfully, update it to the following.</span></span> <span data-ttu-id="95e32-281">Чтобы выполнить компиляцию, нужно добавить инструкцию **using** для пространства имен [System.Linq](http://msdn.microsoft.com/ru-RU/library/bb336768).</span><span class="sxs-lookup"><span data-stu-id="95e32-281">This example retrieves all SharePoint lists in a SharePoint website. To compile this code you will need to add a  **using** statement for [System.Linq](http://msdn.microsoft.com/ru-RU/library/bb336768).</span></span> <span data-ttu-id="95e32-282">Добавьте также псевдоним в инструкцию **using** для пространства имен **Microsoft.SharePoint.Client**, чтобы однозначно ссылаться на его классы.</span><span class="sxs-lookup"><span data-stu-id="95e32-282">This example adds a field to a SharePoint list. add an alias to the using statement for  **Microsoft.SharePoint.Client** namespace so you can refer to its classes unambiguously. For example, ****.</span></span> <span data-ttu-id="95e32-283">Пример: `using SP = Microsoft.SharePoint.Client;`.</span><span class="sxs-lookup"><span data-stu-id="95e32-283">For example: `using SP = Microsoft.SharePoint.Client;`.</span></span>

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

### <a name="use-conditional-scope-to-test-for-preconditions-before-loading-data"></a><span data-ttu-id="95e32-284">Использование условной области для проверки предварительных условий перед загрузкой данных</span><span class="sxs-lookup"><span data-stu-id="95e32-284">Use conditional scope to test for preconditions before loading data</span></span>

<span data-ttu-id="95e32-285">Для условного выполнения кода задайте условную область, используя объект **ConditionalScope**.</span><span class="sxs-lookup"><span data-stu-id="95e32-285">To conditionally execute code, set a conditional scope by using a **ConditionalScope** object.</span></span> <span data-ttu-id="95e32-286">Например, извлеките свойство списка при условии, что список не пуст.</span><span class="sxs-lookup"><span data-stu-id="95e32-286">For example, retrieve the list property when the list is not null.</span></span> <span data-ttu-id="95e32-287">Кроме того, нужно добавить инструкцию **using** для пространств имен [System.Collections.Generic](http://msdn.microsoft.com/ru-RU/library/0sbxh9x2) и [System.Linq](http://msdn.microsoft.com/ru-RU/library/bb336768).</span><span class="sxs-lookup"><span data-stu-id="95e32-287">You also need to add **using** statements for [System.Collections.Generic](http://msdn.microsoft.com/ru-RU/library/0sbxh9x2) and [System.Linq](http://msdn.microsoft.com/ru-RU/library/bb336768).</span></span> <span data-ttu-id="95e32-288">Добавьте также псевдоним в инструкцию **using** для пространства имен **Microsoft.SharePoint.Client**, чтобы однозначно ссылаться на его классы.</span><span class="sxs-lookup"><span data-stu-id="95e32-288">This example adds a field to a SharePoint list. add an alias to the using statement for  **Microsoft.SharePoint.Client** namespace so you can refer to its classes unambiguously. For example, ****.</span></span> <span data-ttu-id="95e32-289">Пример: `using SP = Microsoft.SharePoint.Client;`.</span><span class="sxs-lookup"><span data-stu-id="95e32-289">For example: `using SP = Microsoft.SharePoint.Client;`.</span></span>
 
> [!NOTE] 
> <span data-ttu-id="95e32-290">Вызывать методы и задавать свойства внутри условной области запрещено, так как клиентская библиотека не отслеживает побочные эффекты этих действий.</span><span class="sxs-lookup"><span data-stu-id="95e32-290">Calling method and setting properties within a conditional scope are not permitted, because the client library does not track the side effects of method calls and property settings. You should use only Load inside the conditional scope.</span></span> <span data-ttu-id="95e32-291">Внутри условной области следует использовать только метод **Load**.</span><span class="sxs-lookup"><span data-stu-id="95e32-291">You should use only **Load** inside the conditional scope.</span></span>

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

### <a name="use-an-exception-handling-scope-to-catch-exceptions"></a><span data-ttu-id="95e32-292">Использование области обработки исключений для перехвата исключений</span><span class="sxs-lookup"><span data-stu-id="95e32-292">Use an exception handling scope to catch exceptions</span></span>

<span data-ttu-id="95e32-293">В этом примере показано, как создать и использовать область обработки исключений с помощью объекта **ExceptionHandlingScope**.</span><span class="sxs-lookup"><span data-stu-id="95e32-293">This example shows how to create and use an exception handling scope with an **ExceptionHandlingScope** object.</span></span> <span data-ttu-id="95e32-294">Сценарий предполагает обновление описания списка и обеспечение создания папок.</span><span class="sxs-lookup"><span data-stu-id="95e32-294">The scenario is to update the description of a list and also enable folder creation.</span></span> <span data-ttu-id="95e32-295">Существует вероятность того, что список не существует.</span><span class="sxs-lookup"><span data-stu-id="95e32-295">There is a possibility that the list might not exist.</span></span>

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


## <a name="see-also"></a><span data-ttu-id="95e32-296">См. также</span><span class="sxs-lookup"><span data-stu-id="95e32-296">See also</span></span>
<span data-ttu-id="95e32-297"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="95e32-297"></span></span>

- [<span data-ttu-id="95e32-298">Разработка надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="95e32-298">Develop SharePoint Add-ins</span></span>](develop-sharepoint-add-ins.md)
- [<span data-ttu-id="95e32-299">Создание сайтов для SharePoint</span><span class="sxs-lookup"><span data-stu-id="95e32-299">Build sites for SharePoint</span></span>](../general-development/build-sites-for-sharepoint.md)
    
 

