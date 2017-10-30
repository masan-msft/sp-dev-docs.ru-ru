---
title: "Начало работы с помощью клиентской объектной модели с внешними данными в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 8ed91929-fdb6-4fde-ba2a-7942870575f3
ms.openlocfilehash: 2ddd19599a6a88523cb38940355104d178500f3d
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="get-started-using-the-client-object-model-with-external-data-in-sharepoint"></a><span data-ttu-id="6740c-102">Начало работы с помощью клиентской объектной модели с внешними данными в SharePoint</span><span class="sxs-lookup"><span data-stu-id="6740c-102">Get started using the client object model with external data in SharePoint</span></span>
<span data-ttu-id="6740c-103">Сведения об использовании клиентской объектной модели SharePoint для работы с помощью Business Connectivity Services (BCS) в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="6740c-103">Learn how to use the SharePoint client object model to work with Business Connectivity Services (BCS) in SharePoint.</span></span>
## <a name="what-is-the-sharepoint-client-object-model"></a><span data-ttu-id="6740c-104">Что такое клиентской объектной модели SharePoint?</span><span class="sxs-lookup"><span data-stu-id="6740c-104">What is the SharePoint client object model?</span></span>

<span data-ttu-id="6740c-105">Клиентская объектная модель для SharePoint — это набор библиотек на стороне клиента, которые представляют серверной объектной модели.</span><span class="sxs-lookup"><span data-stu-id="6740c-105">The client object model for SharePoint is a set of client-based libraries that represent the server object model.</span></span> <span data-ttu-id="6740c-106">Они собраны в трех разных библиотек DLL с использованием различных типов разработки.</span><span class="sxs-lookup"><span data-stu-id="6740c-106">They are packaged in three different DLLs to accommodate a variety of development types.</span></span> <span data-ttu-id="6740c-107">Клиентская объектная модель содержит большую часть основных функций сервера API.</span><span class="sxs-lookup"><span data-stu-id="6740c-107">The client object model includes most of the major functions of the server API.</span></span> <span data-ttu-id="6740c-108">Позволяет получить доступ к одной типам функциональные возможности из браузера сценариев и также .NET веб-приложений и приложений Silverlight.</span><span class="sxs-lookup"><span data-stu-id="6740c-108">This allows access to the same types of functionality from browser scripting and also .NET web applications and Silverlight applications.</span></span>  <br/> <span data-ttu-id="6740c-109">Чтобы улучшить и расширить возможности по работе с внешними данными, Службы Business Connectivity Services (BCS) расширил клиентской объектной модели, чтобы включить дополнительные функции.</span><span class="sxs-lookup"><span data-stu-id="6740c-109">To enhance and expand the capabilities for working with external data, Business Connectivity Services (BCS) has expanded the client object model to include additional functionality.</span></span>  <br/> 

<a href="#BCScsom_getstarted"><img alt="Get set up" src="../images/mod_icon_getstartbox.gif" /></a>&nbsp;&nbsp;&nbsp;<a href="#BCScsom_Tasks"><img alt="Get to work" src="../images/mod_icon_dobox.gif" /></a>&nbsp;&nbsp;&nbsp;<a href="#BCScsom_Learnmore"><img alt="Learn more" src="../images/mod_icon_startbox.gif" /></a></p>

## <a name="get-started-using-the-sharepoint-client-object-model-with-external-data"></a><span data-ttu-id="6740c-110">Начало работы с помощью клиентской объектной модели SharePoint с внешними данными</span><span class="sxs-lookup"><span data-stu-id="6740c-110">Get started using the SharePoint client object model with external data</span></span>
<span data-ttu-id="6740c-111"><a name="BCScsom_getstarted"> </a></span><span class="sxs-lookup"><span data-stu-id="6740c-111"></span></span>

<span data-ttu-id="6740c-112">Разработка решений с помощью объектной модели клиента SharePoint (CSOM), необходимо следующее:</span><span class="sxs-lookup"><span data-stu-id="6740c-112">To develop solutions using the SharePoint client object model (CSOM), you will need the following:</span></span>
  
    
    

- <span data-ttu-id="6740c-113">SharePoint</span><span class="sxs-lookup"><span data-stu-id="6740c-113">SharePoint</span></span>
    
  
- <span data-ttu-id="6740c-114">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="6740c-114">Visual Studio 2012</span></span>
    
  
- <span data-ttu-id="6740c-115">Инструменты разработчика Office для Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="6740c-115">Office Developer Tools for Visual Studio 2012</span></span>
    
  
<span data-ttu-id="6740c-116">Сведения о том, как настроить среду разработки см [в среде разработки для BCS в SharePoint](setting-up-a-development-environment-for-bcs-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="6740c-116">For information about how to set up your development environment, see  [Setting up a development environment for BCS in SharePoint](setting-up-a-development-environment-for-bcs-in-sharepoint.md).</span></span>
  
    
    
<span data-ttu-id="6740c-p102">Для доступа к возможности, предоставляемые в клиентской объектной модели, требуется только для добавления ссылки на файлы **Microsoft.SharePoint.Client.Runtime.dll** и **Microsoft.SharePoint.Client.dll** в их проектах. Можно также использовать клиентской объектной модели, ссылки на следующие библиотеки DLL в глобальный кэш сборок:</span><span class="sxs-lookup"><span data-stu-id="6740c-p102">To access the capabilities provided by the client object model, you need only to add references to the **Microsoft.SharePoint.Client.Runtime.dll** and **Microsoft.SharePoint.Client.dll** files in their projects. You can also use the client object model by referencing the following DLLs in the global assembly cache:</span></span>
  
    
    

-  `\\Program Files\\Common Files\\Microsoft Shared\\Web Server Extensions\\15\\isapi\\Microsoft.SharePoint.Client.Runtime.dll`
    
  
-  `\\Program Files\\Common Files\\Microsoft Shared\\Web Server Extensions\\15\\isapi\\Microsoft.SharePoint.Client.dll`
    
  

### <a name="sharepoint-client-object-model-essentials"></a><span data-ttu-id="6740c-119">Основные компоненты объектной модели SharePoint клиента</span><span class="sxs-lookup"><span data-stu-id="6740c-119">SharePoint client object model essentials</span></span>

<span data-ttu-id="6740c-120">Следующие статьи поможет вам понять, Дополнительные сведения о клиентской объектной модели в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="6740c-120">The following articles will help you understand more about the client object model in SharePoint.</span></span>
  
    
    

<span data-ttu-id="6740c-121">**В таблице 1. Основные понятия, которые для Общие сведения о клиентской объектной модели**</span><span class="sxs-lookup"><span data-stu-id="6740c-121">**Table 1. Core concepts for understanding the client object model**</span></span>


|<span data-ttu-id="6740c-122">**Статья**</span><span class="sxs-lookup"><span data-stu-id="6740c-122">**Article**</span></span>|<span data-ttu-id="6740c-123">**Описание**</span><span class="sxs-lookup"><span data-stu-id="6740c-123">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="6740c-124">Внешние типы контента в SharePoint</span><span class="sxs-lookup"><span data-stu-id="6740c-124">External content types in SharePoint</span></span>](external-content-types-in-sharepoint.md) <br/> |<span data-ttu-id="6740c-125">Прочитав эту статью, вы узнаете, что можно делать с внешними типами контента и что необходимо для их создания в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="6740c-125">Learn what you can do with external content types and what you need to start creating them in SharePoint.</span></span>  <br/> |
| [<span data-ttu-id="6740c-126">Использование источников OData со службами Business Connectivity Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="6740c-126">Using OData sources with Business Connectivity Services in SharePoint</span></span>](using-odata-sources-with-business-connectivity-services-in-sharepoint.md) <br/> |<span data-ttu-id="6740c-127">Предоставляет сведения, которые помогут приступить к работе Создание внешних типов контента на основе источников OData и использовать эти данные в SharePoint или Office 2013 компонентов.</span><span class="sxs-lookup"><span data-stu-id="6740c-127">Provides information to help get started creating external content types based on OData sources and using that data in SharePoint or Office 2013 components.</span></span>  <br/> |
| [<span data-ttu-id="6740c-128">Выбор правильного набора API в SharePoint</span><span class="sxs-lookup"><span data-stu-id="6740c-128">Choose the right API set in SharePoint</span></span>](choose-the-right-api-set-in-sharepoint.md) <br/> |<span data-ttu-id="6740c-129">Сведения о некоторых наборов API, которые предоставляются в SharePoint, включая серверной объектной модели, различных клиентских объектных моделей и веб-службы REST/OData.</span><span class="sxs-lookup"><span data-stu-id="6740c-129">Learn about the several sets of APIs that are provided in SharePoint, including the server object model, the various client object models, and the REST/OData web service.</span></span>  <br/> |
| [<span data-ttu-id="6740c-130">Справка по API клиента .NET для SharePoint</span><span class="sxs-lookup"><span data-stu-id="6740c-130">.NET client API reference for SharePoint Online</span></span>](http://msdn.microsoft.com/library/88e5e1b9-eab2-4f3b-a3f2-75c96b86f1f4%28Office.15%29.aspx) <br/> |<span data-ttu-id="6740c-131">Сведения о клиенте .NET библиотеки классов в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="6740c-131">Find information about the .NET client class libraries in SharePoint.</span></span>  <br/> |
| [<span data-ttu-id="6740c-132">Справочник по JavaScript API для SharePoint</span><span class="sxs-lookup"><span data-stu-id="6740c-132">JavaScript API reference for SharePoint</span></span>](http://msdn.microsoft.com/library/1ead2f8d-a541-4a50-89fa-f195f2ba14e5%28Office.15%29.aspx) <br/> |<span data-ttu-id="6740c-133">Сведения о библиотеках объектов JavaScript в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="6740c-133">Find information about the JavaScript object libraries in SharePoint.</span></span>  <br/> |
   

## <a name="what-can-you-do-with-the-client-object-model"></a><span data-ttu-id="6740c-134">Что можно делать с помощью клиентской объектной модели</span><span class="sxs-lookup"><span data-stu-id="6740c-134">What can you do with the client object model?</span></span>
<span data-ttu-id="6740c-135"><a name="BCScsom_Tasks"> </a></span><span class="sxs-lookup"><span data-stu-id="6740c-135"></span></span>

<span data-ttu-id="6740c-136">Клиентская объектная модель SharePoint можно использовать для извлечения, обновления и управления данными, содержащимися в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="6740c-136">You can use the SharePoint client object model to retrieve, update, and manage data that is contained in SharePoint.</span></span> <span data-ttu-id="6740c-137">SharePoint предоставляет клиенту библиотек в различные форматы для учета большинства разработчиков.</span><span class="sxs-lookup"><span data-stu-id="6740c-137">SharePoint offers the client libraries in different formats to accommodate most developers.</span></span> <span data-ttu-id="6740c-138">Для разработчиков веб-приложений, использующих языками сценариев клиентская библиотека предлагается в JavaScript.</span><span class="sxs-lookup"><span data-stu-id="6740c-138">For web developers who are using scripting languages, the client library is offered in JavaScript.</span></span> <span data-ttu-id="6740c-139">Для разработчиков .NET предлагается как клиент .NET управляемой библиотеки DLL.</span><span class="sxs-lookup"><span data-stu-id="6740c-139">For .NET developers, it is offered as a .NET client managed DLL.</span></span> <span data-ttu-id="6740c-140">Клиентская библиотека для разработчиков приложений Silverlight, обеспечивается Silverlight DLL.</span><span class="sxs-lookup"><span data-stu-id="6740c-140">For developers of Silverlight applications, the client library is provided by a Silverlight DLL.</span></span>
  
    
    
<span data-ttu-id="6740c-141">Изучение статей в таблице 2, Дополнительные сведения о клиентской объектной модели в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="6740c-141">See the articles in Table 2 for more information about what you can do with the client object model in SharePoint.</span></span>
  
    
    

<span data-ttu-id="6740c-142">**В таблице 2. Основные задачи по использованию клиентской объектной модели с помощью внешних данных**</span><span class="sxs-lookup"><span data-stu-id="6740c-142">**Table 2. Basic tasks for using the client object model with external data**</span></span>


|<span data-ttu-id="6740c-143">**Задача**</span><span class="sxs-lookup"><span data-stu-id="6740c-143">**Task**</span></span>|<span data-ttu-id="6740c-144">**Описание**</span><span class="sxs-lookup"><span data-stu-id="6740c-144">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="6740c-145">Выполнение базовых операций с использованием кода библиотеки клиента в SharePoint</span><span class="sxs-lookup"><span data-stu-id="6740c-145">Complete basic operations using SharePoint client library code</span></span>](http://msdn.microsoft.com/library/5a69c9e3-73bf-4ed5-bc19-182056bdb394%28Office.15%29.aspx) <br/> |<span data-ttu-id="6740c-146">Узнайте, как создавать код для выполнения базовых операций с клиентской объектной модели SharePoint.</span><span class="sxs-lookup"><span data-stu-id="6740c-146">Learn how to write code to perform basic operations with the SharePoint client object model.</span></span>  <br/> |
| [<span data-ttu-id="6740c-147">Как: используйте клиентская библиотека кода для доступа к внешним данным в SharePoint</span><span class="sxs-lookup"><span data-stu-id="6740c-147">How to: Use the client code library to access external data in SharePoint</span></span>](how-to-use-the-client-code-library-to-access-external-data-in-sharepoint.md) <br/> |<span data-ttu-id="6740c-148">Сведения об использовании клиентской объектной модели SharePoint для работы с объектами SharePoint BCS с помощью сценариев на основе браузера.</span><span class="sxs-lookup"><span data-stu-id="6740c-148">Learn how to use the SharePoint client object model to work with SharePoint BCS objects using browser-based scripting.</span></span>  <br/> |
   
<span data-ttu-id="6740c-149">Ниже приведены некоторые основные примеры задач, которые можно выполнить с помощью CSOM.</span><span class="sxs-lookup"><span data-stu-id="6740c-149">The following are some basic examples of tasks you can accomplish using CSOM.</span></span>
  
    
    

### <a name="get-a-specific-entity"></a><span data-ttu-id="6740c-150">Получение определенной сущности</span><span class="sxs-lookup"><span data-stu-id="6740c-150">Get a specific entity</span></span>

<span data-ttu-id="6740c-151">В этом примере показано, как получить контекст из SharePoint, а затем извлеките объект источника данных.</span><span class="sxs-lookup"><span data-stu-id="6740c-151">This example shows how to get context from SharePoint, and then retrieve a specified data source entity.</span></span>
  
    
    

```cs

ClientContext ctx = new ClientContext("http://sharepointservername"); 
Web web = ctx.Web; 
ctx.Load(web); 
Entity entity = ctx.Web.GetEntity("http://sharepointservername", "EntityName"); 
ctx.Load(entity); 
ctx.ExecuteQuery(); 

```


### <a name="create-a-generic-invoker"></a><span data-ttu-id="6740c-152">Создание универсальных вызова</span><span class="sxs-lookup"><span data-stu-id="6740c-152">Create a generic invoker</span></span>

<span data-ttu-id="6740c-153">В этом примере показано, как создавать универсальные вызова таким образом, можно создать объект сущности для работы в коде.</span><span class="sxs-lookup"><span data-stu-id="6740c-153">This example shows how to write a generic invoker so that you can create an entity object to work within your code.</span></span>
  
    
    

```cs

ObjectCollection myObj; 
entity.Execute("MethodInstanceName", lsi, myObj); 
ctx.Load(myObj); 
ctx.ExecuteQuery(); 

```


### <a name="retrieve-paged-result-sets"></a><span data-ttu-id="6740c-154">Получение наборов выгружаемый результатов</span><span class="sxs-lookup"><span data-stu-id="6740c-154">Retrieve paged result sets</span></span>

<span data-ttu-id="6740c-p104">Следующем примере показано, как получить отфильтрованные выгружаемый набор данных. В этом случае значение страницы равно 50.</span><span class="sxs-lookup"><span data-stu-id="6740c-p104">The following example shows how to retrieve a filtered, paged dataset. In this case, the page value is 50.</span></span>
  
    
    

```cs

// Find filters for given Method Name. 
FilterCollection fCollection = entity.GetFilters("methodName"); 
ctx.Load(fCollection); 
ctx.ExecuteQuery(); 
FilterCollection modifiedFCollection = new FilterCollection(); 
foreach( Filter filter in fCollection) 
{ 
    if( filter.FilterField.equals("X.Y.Z.Country")) 
    { 
        filter.FilterValue = "India"; 
        modifiedFCollection.Add(Filter); 
    } 
    if(filter.FilterType == FilterType.Limit) 
    { 
        filter.FilterValue = 50; 
        modifiedFCollection.Add(Filter); 
    } 
} 
EntityInstanceCollection eCollection = entity.FindFiltered(modifiedFCollection, 
"nameOfFinder", lsi); 
ctx.ExecuteQuery(); 

```


### <a name="query-for-filtered-information"></a><span data-ttu-id="6740c-157">Запрос отфильтрованные сведения</span><span class="sxs-lookup"><span data-stu-id="6740c-157">Query for filtered information</span></span>

<span data-ttu-id="6740c-p105">Приведенный ниже показано, как для возврата набора отфильтрованных результатов. В этом случае отфильтровано столбец данных  это поле **X.Y.Z.Country**. Код ищет все действия со значением «Индия» и помещает, в коллекцию.</span><span class="sxs-lookup"><span data-stu-id="6740c-p105">The following example demonstrates how to return a filtered result set. In this case, the data column filtered is the **X.Y.Z.Country** field. The code looks for anything with the value of "India", and then puts that into a collection.</span></span>
  
    
    

```cs

// Find filters for given Method Name. 
FilterCollection fCollection = entity.GetFilters("methodName"); 
ctx.Load(fCollection); 
ctx.ExecuteQuery(); 
FilterCollection modifiedFCollection = new FilterCollection(); 
foreach( Filter filter in fCollection) 
{ 
    if( filter.FilterField.equals("X.Y.Z.Country")) 
    { 
        filter.FilterValue = "India"; 
        modifiedFCollection.Add(Filter); 
    } 
} 
EntityInstanceCollection eCollection = entity.FindFiltered(modifiedFCollection, 
"nameOfFinder", lsi); 
ctx.ExecuteQuery(); 

```


## <a name="beyond-the-basics-learn-more-about-the-client-object-model"></a><span data-ttu-id="6740c-161">От простого к сложному: Дополнительные сведения о клиентской объектной модели</span><span class="sxs-lookup"><span data-stu-id="6740c-161">Beyond the basics: Learn more about the client object model</span></span>
<span data-ttu-id="6740c-162"><a name="BCScsom_Learnmore"> </a></span><span class="sxs-lookup"><span data-stu-id="6740c-162"></span></span>

<span data-ttu-id="6740c-163">Дополнительные сведения об использовании клиентской объектной модели в SharePoint можно сведения, приведенные в таблице 3.</span><span class="sxs-lookup"><span data-stu-id="6740c-163">For more information about using the client object model in SharePoint, see the information in Table 3.</span></span>
  
    
    

<span data-ttu-id="6740c-164">**В таблице 3. Расширенные концепции для клиентской объектной модели**</span><span class="sxs-lookup"><span data-stu-id="6740c-164">**Table 3. Advanced concepts for the client object model**</span></span>


|<span data-ttu-id="6740c-165">**Статья**</span><span class="sxs-lookup"><span data-stu-id="6740c-165">**Article**</span></span>|<span data-ttu-id="6740c-166">**Описание**</span><span class="sxs-lookup"><span data-stu-id="6740c-166">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="6740c-167">BCS клиента Справочник по объектной модели для SharePoint</span><span class="sxs-lookup"><span data-stu-id="6740c-167">BCS client object model reference for SharePoint</span></span>](bcs-client-object-model-reference-for-sharepoint.md) <br/> |<span data-ttu-id="6740c-168">Обобщаются объектов для создания клиентских скриптов с помощью клиентской объектной модели SharePoint для доступа к внешним данным, предоставляемым BCS.</span><span class="sxs-lookup"><span data-stu-id="6740c-168">Summarizes the objects available for creating client-side scripts using the SharePoint client object model to access external data exposed by BCS.</span></span>  <br/> |
   

## <a name="additional-resources"></a><span data-ttu-id="6740c-169">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="6740c-169">Additional resources</span></span>
<span data-ttu-id="6740c-170"><a name="BCScsom_Learnmore"> </a></span><span class="sxs-lookup"><span data-stu-id="6740c-170"></span></span>


-  [<span data-ttu-id="6740c-171">Business Connectivity Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="6740c-171">Business Connectivity Services in SharePoint</span></span>](business-connectivity-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="6740c-172">Надстройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="6740c-172">SharePoint Add-ins</span></span>](http://msdn.microsoft.com/library/cd1eda9e-8e54-4223-93a9-a6ea0d18df70%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="6740c-173">Как: используйте клиентская библиотека кода для доступа к внешним данным в SharePoint</span><span class="sxs-lookup"><span data-stu-id="6740c-173">How to: Use the client code library to access external data in SharePoint</span></span>](how-to-use-the-client-code-library-to-access-external-data-in-sharepoint.md)
    
  
-  [<span data-ttu-id="6740c-174">Выполнение базовых операций с использованием кода библиотеки клиента в SharePoint</span><span class="sxs-lookup"><span data-stu-id="6740c-174">Complete basic operations using SharePoint client library code</span></span>](http://msdn.microsoft.com/library/5a69c9e3-73bf-4ed5-bc19-182056bdb394%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="6740c-175">SharePoint: Доступ к сложным внешним типам контента с помощью CSOM</span><span class="sxs-lookup"><span data-stu-id="6740c-175">SharePoint: Access complex external content types with CSOM</span></span>](http://code.msdn.microsoft.com/office/SharePoint-Accessing-ccbc24cf)
    
  
