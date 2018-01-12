---
title: "Работа с веб-службами в рабочих процессах SharePoint с помощью Visual Studio 2012"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 5ffaa585-a872-4e14-bc0e-4a38c6a16b04
ms.openlocfilehash: f981ecc14fedcec1b682c472ebccf823ad610605
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="working-with-web-services-in-sharepoint-workflows-using-visual-studio-2012"></a><span data-ttu-id="3cb5a-102">Работа с веб-службами в рабочих процессах SharePoint с помощью Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="3cb5a-102">Working with Web Services in SharePoint Workflows using Visual Studio 2012</span></span>
<span data-ttu-id="3cb5a-p101">Узнайте, как использовать веб-службы в рабочих процессах SharePoint с помощью Visual Studio 2012. **Автор:** [Эндрю Коннел (Andrew Connell)](http://social.msdn.microsoft.com/profile/andrew%20connell%20%5bmvp%5d/), [AndrewConnell.com](http://www.andrewconnell.com)</span><span class="sxs-lookup"><span data-stu-id="3cb5a-p101">Demonstrates how to use web services in SharePoint workflows using Visual Studio 2012. **Provided by:** [Andrew Connell](http://social.msdn.microsoft.com/profile/andrew%20connell%20%5bmvp%5d/),  [AndrewConnell.com](http://www.andrewconnell.com)</span></span>
  
> [!NOTE] 
> <span data-ttu-id="3cb5a-105">К этой статье прилагается пример законченного кода, который можно просматривать во время чтения или брать за основу при создании собственных проектов рабочих процессов SharePoint.</span><span class="sxs-lookup"><span data-stu-id="3cb5a-105">This article is accompanied by an end-to-end code sample that you can use to follow the article, or as a starter for your own SharePoint workflow projects. You can find the downloadable code here: LINK.</span></span> <span data-ttu-id="3cb5a-106">Вы можете скачать код из коллекции кода MSDN на странице [Работа с веб-службами в рабочих процессах SharePoint с помощью Visual Studio 2012](http://code.msdn.microsoft.com/Working-with-Web-in-46148199).</span><span class="sxs-lookup"><span data-stu-id="3cb5a-106">You can find the downloadable code in the MSDN Code Gallery, here:  [Working with Web Services in SharePoint Workflows using Visual Studio 2012](http://code.msdn.microsoft.com/Working-with-Web-in-46148199).</span></span> 
  
    
    


  
    
    
<span data-ttu-id="3cb5a-107">В SharePoint корпорация Майкрософт существенно изменила подход к рабочим процессам.</span><span class="sxs-lookup"><span data-stu-id="3cb5a-107">Microsoft has taken a very different approach to workflow in SharePoint than in previous versions of SharePoint.</span></span> <span data-ttu-id="3cb5a-108">Команда разработчиков рабочих процессов в сотрудничестве с командой разработчиков Azure создала новый продукт под названием Workflow Manager.</span><span class="sxs-lookup"><span data-stu-id="3cb5a-108">The workflow team worked with the Azure team to create a new product called Workflow Manager.</span></span> <span data-ttu-id="3cb5a-109">Workflow Manager служит для размещения последней версии среды выполнения Windows Workflow Foundation (версии 4) и всех необходимых служб с высоким уровнем доступности и масштабируемости.</span><span class="sxs-lookup"><span data-stu-id="3cb5a-109">Workflow Manager serves the role of hosting the latest version of the Windows Workflow Foundation (version 4) runtime and all the necessary services in a highly available and scalable way.</span></span> <span data-ttu-id="3cb5a-110">Производительность и масштабируемость обеспечивает служебная шина Microsoft Azure. Этот диспетчер работает абсолютно одинаково в локальном развертывании и облаке.</span><span class="sxs-lookup"><span data-stu-id="3cb5a-110">It takes advantage of Microsoft Azure Service Bus for performance and scalability, and when deployed, it runs the same whether in an on-premises deployment or a deployment in the cloud.</span></span> <span data-ttu-id="3cb5a-111">Затем SharePoint подключается и настраивается, чтобы поручить выполнение рабочих процессов и все связанные с этим задачи ферме Workflow Manager. Одно из самых важных изменений в новой архитектуре рабочих процессов заключается в том, что все настраиваемые рабочие процессы в SharePoint (в том числе созданные с помощью Visual Studio 2012) являются полностью декларативными.</span><span class="sxs-lookup"><span data-stu-id="3cb5a-111">SharePoint is then connected and configured to hand off all workflow execution and related tasks to the Workflow Manager farm.One of the more important changes in the new workflow architecture is that all custom workflows in SharePoint completely declarative, including those built using Visual Studio 2012.</span></span> <span data-ttu-id="3cb5a-112">В предыдущих версиях SharePoint рабочие процессы, созданные в Visual Studio 2012, не были исключительно декларативными.</span><span class="sxs-lookup"><span data-stu-id="3cb5a-112">In previous versions of SharePoint, workflows developed with Visual Studio 2012 were not exclusively declarative.</span></span> <span data-ttu-id="3cb5a-113">Они представляли собой сочетание декларативного кода XAML со скомпилированной сборкой.</span><span class="sxs-lookup"><span data-stu-id="3cb5a-113">Instead, they were a pairing of declarative XAML with a compiled assembly.</span></span> <span data-ttu-id="3cb5a-114">Управляемая сборка содержала бизнес-логику рабочего процесса. У опытных разработчиков SharePoint может возникнуть следующий вопрос: "Как реализовать пользовательскую бизнес-логику без скомпилированной сборки?".</span><span class="sxs-lookup"><span data-stu-id="3cb5a-114">The managed assembly contained the workflow's business logic.This might come as a shock to seasoned SharePoint developers who may be asking, "so how do I implement my custom business logic without a compiled assembly?".</span></span> <span data-ttu-id="3cb5a-115">Корпорация Майкрософт предлагает вместо этого создать настраиваемую веб-службу (в идеале — WCF, OData или RESTful), которая возвращает данные в формате нотации объектов JavaScript (JSON), и использовать некоторые новые действия и объекты в этой новой версии.</span><span class="sxs-lookup"><span data-stu-id="3cb5a-115">Microsoft suggests that instead you create a custom web service, ideally a WCF, OData, or RESTful web service that returns data in the JavaScript Object Notation (JSON) format, and to use some of the new activities and objects in this new version.</span></span> 
## <a name="scenarios-for-using-web-services-in-sharepoint-workflows"></a><span data-ttu-id="3cb5a-116">Сценарии использования веб-служб в рабочих процессах SharePoint</span><span class="sxs-lookup"><span data-stu-id="3cb5a-116">Scenarios for using web services in SharePoint workflows</span></span>
<span data-ttu-id="3cb5a-117"><a name="sec1"> </a></span><span class="sxs-lookup"><span data-stu-id="3cb5a-117"><a name="sec1"> </a></span></span>

<span data-ttu-id="3cb5a-p104">Не сложно представить сценарии, в которых используются настраиваемые веб-службы в рабочем процессе SharePoint. Разработчики, которые создавали рабочие процессы в SharePoint 2007 или SharePoint 2010, привыкли работать с собственным кодом, так как эти рабочие процессы по своей природе были программными. В эти рабочие процессы не требовалось добавлять собственный код, но разработчики часто делали это.</span><span class="sxs-lookup"><span data-stu-id="3cb5a-p104">It is not difficult to conceive of scenarios where you would leverage a custom web services in a SharePoint workflow. Developers who authored workflows using SharePoint 2007 or SharePoint 2010 are accustomed to working with custom code, since these workflows were inherently programmatic. You were not required to add custom code to these workflows, but doing so was quite common.</span></span>
  
    
    
<span data-ttu-id="3cb5a-121">Так как рабочие процессы SharePoint являются полностью декларативными, теперь часто, вместо того чтобы писать собственный код, необходимо использовать код, созданный во внешней веб-службе, которая вызывается и используется рабочим процессом.</span><span class="sxs-lookup"><span data-stu-id="3cb5a-121">With SharePoint workflows to being purely declarative, many cases where you may have written custom code must now be handled with code written in an external web service that is called and consumed by the workflow.</span></span> 
  
    
    
<span data-ttu-id="3cb5a-p105">Рабочие процессы SharePoint могут использовать любые веб-службы. Тем не менее рабочим процессам проще всего взаимодействовать с веб-службами, которые передают данные по протоколу Open Data ( **OData** ) в форматах **Atom** или **json**. OData  это наиболее подходящий вариант, так как его полностью поддерживают средства разработки рабочих процессов SharePoint (как SharePoint Designer 2013, так и Visual Studio 2012).</span><span class="sxs-lookup"><span data-stu-id="3cb5a-p105">SharePoint workflows can consume any sort of web service. That said, it is easiest for workflows to interact with web services that pass data using the Open Data protocol ( **OData** ), as provided in either of the formats **Atom** or **json**. OData is the best approach because it is fully supported by the SharePoint workflow authoring tools (both SharePoint Designer 2013 and Visual Studio 2012).</span></span>
  
    
    
<span data-ttu-id="3cb5a-p106">Кроме того, поддерживаются как анонимные веб-службы, так и веб-службы, использующие различные типы проверки подлинности. На самом деле, вы полностью контролируете запросы и ответы при каждом вызове службы. Таким образом, например, с помощью ряда действий в рабочем процессе можно сначала выполнить проверку подлинности, используя одну службу для получения токена OAuth, а затем включить этот токен в последующие запросы к службам, защищенные с помощью  [OAuth 2.0](http://oauth.net/2/).</span><span class="sxs-lookup"><span data-stu-id="3cb5a-p106">In addition, both anonymous web services as well as those protected with different types of authentication are supported. In fact, you have full control over the request and response handling for each service call. Thus, for example, you can use a series of activities within a workflow to first authenticate using one service to obtain an OAuth token, and then include that token in future requests to services secured using  [OAuth 2.0](http://oauth.net/2/).</span></span>
  
    
    

## <a name="leveraging-web-services-in-workflows"></a><span data-ttu-id="3cb5a-128">Использование веб-служб в рабочих процессах</span><span class="sxs-lookup"><span data-stu-id="3cb5a-128">Leveraging web services in workflows</span></span>
<span data-ttu-id="3cb5a-129"><a name="sec2"> </a></span><span class="sxs-lookup"><span data-stu-id="3cb5a-129"><a name="sec2"> </a></span></span>

<span data-ttu-id="3cb5a-p107">Работа с веб-службами в рабочих процессах SharePoint включает два этапа. Первый  вызов веб-службы с помощью нового действия **HttpSend**, представленного в SharePoint. Действие **HttpSend** позволяет вызывать простейшие веб-службы, а также предоставляет HTTP-команды и определенные заголовки HTTP для более сложных задач. На рис. 1 показан ряд свойств действия **HttpSend**.</span><span class="sxs-lookup"><span data-stu-id="3cb5a-p107">Working with web services in SharePoint workflows involves two stages. The first is simply calling the web service, which you do by using a new **HttpSend** activity introduced with SharePoint. **HttpSend** lets you call into the simplest web services or, for more complex tasks, provides HTTP verbs and provides specific HTTP headers. Figure 1 shows many of the properties that are available on the **HttpSend** activity.</span></span>
  
    
    

<span data-ttu-id="3cb5a-134">**Рис. 1. Окно "Свойства" для действия HttpSend**</span><span class="sxs-lookup"><span data-stu-id="3cb5a-134">**Figure 1. Properties Tool Window for the HttpSend Activity**</span></span>

  
    
    

  
    
    
![Рис. 1. Окно "Свойства" для HttpSend](../images/ngWSSP2013WorkflowVS201201.png)
  
    
    
<span data-ttu-id="3cb5a-p109">Также необходимо указать тип метода, который вы хотите использовать в запросе на обслуживание. Обратите внимание, что на рисунке 1 в блоке **Запрос** можно указать тип метода (в этом случае  **GET**). Доступны (среди прочих) следующие типы: **GET**, **PUT**, **POST** и **DELETE**. Это основной способ определения действий, которые веб-службы, в частности службы RESTful, должны выполнять с ресурсами, определенными в универсальном коде ресурса (URI) действия.</span><span class="sxs-lookup"><span data-stu-id="3cb5a-p109">You must also specify the method type you wish to use in the service request. Notice in Figure 1 that in the **Request** block you can specify the method type (in this case, **GET**). Available options include **GET**, **PUT**, **POST**, and **DELETE** (although there are others). This is the primary way to tell web services, specifically RESTful services, what to do on the resource defined in the URI of the activity.</span></span>
  
    
    
<span data-ttu-id="3cb5a-p110">Например, чтобы получить все свойства определенного элемента, **Uri** должен содержать уникальный адрес элемента, а в качестве метода необходимо задать **GET**. Чтобы удалить элемент, в качестве **Uri** используется тот же уникальный адрес элемента, только при этом задается метод **DELETE**. Это же касается и обновления элемента, при котором используется метод **POST**. При создании элемента **Uri** должен указывать на уникальный адрес коллекции, в которой будет создан элемент, а в качестве метода нужно задать **POST**. При создании или обновлении элементов службам обычно нужны данные, которые передаются в запросе и указываются с помощью свойства **RequestContent** в действии **HttpSend**.</span><span class="sxs-lookup"><span data-stu-id="3cb5a-p110">For instance, to get all the properties of a specific item, the **Uri** would contain the unique address of the item, and the method would be set to **GET**. To delete the item, the **Uri** would remain the same unique address of the item but the method would be set to **DELETE**. The same is true for updating an item except the method would be set to **POST**. In creating an item, the **Uri** would point to the unique address of the collection where the item is to be created, and the method would be set to **POST**. When creating or updating items, services require the data to use what is passed along as content in the request, indicated using the **RequestContent** property on the **HttpSend** activity.</span></span>
  
    
    
<span data-ttu-id="3cb5a-p111">Второй этап работы с веб-службами, который мы рассмотрим, включает отправку или получение данных из веб-службы. Независимо от того, какое свойство используется в действии **HttpSend** ( **RequestContent** или **ResponseContent**), данные можно передавать в виде сложной структуры в формате строк Нотация объектов JavaScript (JSON). Вам не придется создавать эти строки json и управлять ими вручную. Корпорация Майкрософт предоставляет новый тип объекта:  [DynamicValue](http://msdn.microsoft.com/ru-RU/library/windowsazure/jj193446%28v=azure.10%29.aspx), который значительно упрощает эту задачу.</span><span class="sxs-lookup"><span data-stu-id="3cb5a-p111">The second stage of working with web services that we're going to cover involves submitting or receiving data from a web service. Regardless of whether you use the **RequestContent** or **ResponseContent** properties on the **HttpSend** activity) you can pass the data as a complex structure, which are formatted as JavaScript Object Notation (JSON) strings. The good news is, you don't have to create and manipulate these json strings manually. Instead, Microsoft gives you a new object type, the [DynamicValue](http://msdn.microsoft.com/ru-RU/library/windowsazure/jj193446%28v=azure.10%29.aspx), that makes your task much easier.</span></span> 
  
    
    
 <span data-ttu-id="3cb5a-p112">Объекты **DynamicValue** могут хранить иерархические данные, а также ответ веб-службы. Кроме того, с объектами **DynamicValue** связан ряд действий, с помощью которых можно подсчитать количество элементов в ответе, извлечь значения из ответа либо создать структуру для обновления или создания элементов.</span><span class="sxs-lookup"><span data-stu-id="3cb5a-p112">**DynamicValue** objects can store hierarchal data as well as store the response of a web service call. Furthermore, there is a series of activities associated with **DynamicValue** objects that you can use to count the number of items in the response, extract values from the response, or build up a new structure for updating or creating items.</span></span>
  
    
    

## <a name="creating-web-services-for-sharepoint-workflows"></a><span data-ttu-id="3cb5a-152">Создание веб-служб для рабочих процессов SharePoint</span><span class="sxs-lookup"><span data-stu-id="3cb5a-152">Creating web services for SharePoint workflows</span></span>
<span data-ttu-id="3cb5a-153"><a name="sec3"> </a></span><span class="sxs-lookup"><span data-stu-id="3cb5a-153"><a name="sec3"> </a></span></span>

<span data-ttu-id="3cb5a-p113">Так как добавлена поддержка вызова веб-служб и прекращена поддержка пользовательского кода в рабочих процессах, разработчики теперь должны знать, как создавать службы. Настраиваемые веб-службы для использования в рабочих процессах SharePoint можно создавать по-разному. Действие **HttpSend** и тип данных **DynamicValue** лучше всего подходят для служб RESTful и служб, которые соответствуют протоколу OData.</span><span class="sxs-lookup"><span data-stu-id="3cb5a-p113">With the support for calling web services and the lack of supporting custom code within workflows, developers will now need to know how to create services. There are plenty of options for creating custom web services for use in SharePoint workflows. The **HttpSend** activity and **DynamicValue** data type are best suited for RESTful services and those that conform to the OData Protocol.</span></span>
  
    
    
<span data-ttu-id="3cb5a-p114">OData  это протокол для создания и использования данных на основе принципов служб REST. Он разработан для стандартизации обмена данными с использованием проверенного и надежного протокола HTTP. После создания спецификации OData различные организации реализовали протокол в собственных технологических стеках. Корпорация Майкрософт реализовала собственную версию OData под названием  [Windows Communication Foundation (WCF) Data Services 5.0](http://msdn.microsoft.com/ru-RU/library/hh487257%28v=vs.103%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="3cb5a-p114">OData is a protocol for creating and consuming data based on the principles of REST services. It was developed in an effort to standardize exchanging data using the mature, reliable, and robust HTTP protocol. Once the OData specification was complete, different organizations implemented the protocol on their own technology stacks. Microsoft implemented its own version of OData and branded it  [Windows Communication Foundation (WCF) Data Services 5.0](http://msdn.microsoft.com/ru-RU/library/hh487257%28v=vs.103%29.aspx).</span></span>
  
    
    
<span data-ttu-id="3cb5a-161">Службы RESTful, реализованные в SharePoint, поддерживают протокол OData, так как они разработаны с помощью WCF Data Services, а именно WCF Data Services 5.0, которые используют спецификацию OData 3.0.</span><span class="sxs-lookup"><span data-stu-id="3cb5a-161">The RESTful services implemented by SharePoint actually support OData because they were built using WCF Data Services, specifically WCF Data Services 5.0, which implements the OData 3.0 specification.</span></span>
  
    
    

### <a name="implement-odata-service-crud-q-operations"></a><span data-ttu-id="3cb5a-162">Реализация операций CRUD-Q службы OData</span><span class="sxs-lookup"><span data-stu-id="3cb5a-162">Implement OData Service CRUD-Q operations</span></span>

<span data-ttu-id="3cb5a-p115">Веб-службы обычно используются для простых операций по созданию, чтению, обновлению, удалению и отправке запросов (CRUD-Q) с данными в базе данных. WCF позволяет создать службу OData для использования с рабочим процессом SharePoint. При наличии базы данных необходимо выполнить четыре простых действия, почти не требующих написания кода.</span><span class="sxs-lookup"><span data-stu-id="3cb5a-p115">A common use for web services is performing simple create, read, update, delete, and query (CRUD-Q) operations on data within a database. Creating an OData service for use with a SharePoint workflow is quite simple using WCF. Assuming you have an existing database there are four short steps that require very little coding:</span></span>
  
    
    

1. <span data-ttu-id="3cb5a-p116">Создайте модель базы данных с помощью платформы  [Entity Framework](http://msdn.microsoft.com/ru-RU/library/bb399567%28v=vs.110%29.aspx). При этом не требуется писать код (в Visual Studio доступен мастер).</span><span class="sxs-lookup"><span data-stu-id="3cb5a-p116">Create a model of your database using the  [Entity Framework](http://msdn.microsoft.com/ru-RU/library/bb399567%28v=vs.110%29.aspx). There is no code required (Visual Studio, provides a wizard).</span></span>
    
  
2. <span data-ttu-id="3cb5a-p117">Создайте службу данных WCF. При этом не требуется писать код (в Visual Studio доступен мастер).</span><span class="sxs-lookup"><span data-stu-id="3cb5a-p117">Create a new WCF data service. There is no code required (Visual Studio provides a wizard).</span></span>
    
  
3. <span data-ttu-id="3cb5a-p118">В файле кода службы укажите источник службы в качестве имени модели объекта (созданной на шаге 1), а затем настройте параметры доступа и разрешения для объектов в модели. Для этого требуется написать всего две строки кода.</span><span class="sxs-lookup"><span data-stu-id="3cb5a-p118">In the service code file, set the name of the entity model (created in step #1) to the source of the service, then set the accessibility and permission for the entities in the model. Both steps require as little as two lines of code.</span></span>
    
  
4. <span data-ttu-id="3cb5a-172">Опубликуйте службу в расположении, доступном Workflow Manager.</span><span class="sxs-lookup"><span data-stu-id="3cb5a-172">Publish the service to a location that Workflow Manager can access.</span></span>
    
  

### <a name="implement-odata-service-operations"></a><span data-ttu-id="3cb5a-173">Реализация операций службы OData</span><span class="sxs-lookup"><span data-stu-id="3cb5a-173">Implement OData service operations</span></span>

<span data-ttu-id="3cb5a-p119">Другая задача, для которой используются веб-службы,  реализация бизнес-логики, которая выходит за рамки модели CRUD-Q. Например, рассмотрим службу OData, которая поддерживает операции CRUD-Q для создания банковских кредитов. Предположим, что эта служба также поддерживает вызов со стороны клиентов и предоставление кредитного рейтинга для определения текущей процентной ставки по кредиту. Этот тип задачи выходит за рамки модели CRUD-Q, поскольку включает вызов метода и передачу целого числа для получения ответа.</span><span class="sxs-lookup"><span data-stu-id="3cb5a-p119">Another task you'll want to accomplish using web services is running business logic that may not fit into the CRUDQ model. For example, consider an OData service that supports CRUD-Q operations for creating new bank loans. Suppose this service also supports consumers calling the service and providing a credit score to retrieve a current interest rate for a prospective loan. This type of task does not fall into the CRUDQ model, since it calls a method and passes in an integer to receive a response.</span></span>
  
    
    
<span data-ttu-id="3cb5a-p120">Службы данных OData и WCF поддерживают этот сценарий с помощью  [операций службы](http://msdn.microsoft.com/ru-RU/library/cc668788%28v=vs.110%29.aspx). Операции службы широко распространены и даже используются в службах SharePoint (например, для получения определенного списка с помощью адреса  `http://[..]/_api/web/lists/GetByTitle('ListTitle')`). Метод **GetByTitle**  это оператор службы, созданный командой SharePoint. Разработчики создают собственные операции службы в настраиваемых веб-службах, созданных с помощью WCF Data Services.</span><span class="sxs-lookup"><span data-stu-id="3cb5a-p120">OData and WCF data services support this scenario by providing you with  [service operations](http://msdn.microsoft.com/ru-RU/library/cc668788%28v=vs.110%29.aspx). Service operations are common and are even used within SharePoint services, for instance, when retrieving a specific list using the address  `http://[..]/_api/web/lists/GetByTitle('ListTitle')`. The **GetByTitle** method is a service operator the SharePoint team created. Developers create their own custom service operations in custom web services created using WCF Data Services.</span></span>
  
    
    

## <a name="walkthrough-create-a-workflow-with-visual-studio-2012"></a><span data-ttu-id="3cb5a-182">Пошаговое руководство. Создание рабочего процесса с помощью Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="3cb5a-182">Walkthrough: Create a workflow with Visual Studio 2012</span></span>
<span data-ttu-id="3cb5a-183"><a name="sec4"> </a></span><span class="sxs-lookup"><span data-stu-id="3cb5a-183"><a name="sec4"> </a></span></span>

<span data-ttu-id="3cb5a-p121">В этом пошаговом руководстве показано, как создать собственный рабочий процесс, который вызывает веб-службу OData в базе данных Northwind. База данных Northwind размещается по адресу  [OData.org](http://www.odata.org).</span><span class="sxs-lookup"><span data-stu-id="3cb5a-p121">The following walkthrough demonstrates how to create a custom workflow that calls an OData web service on the Northwind database. You can find the Northwind database hosted at  [OData.org](http://www.odata.org).</span></span> 
  
    
    
<span data-ttu-id="3cb5a-p122">После завершения пользователи введут код идентификатор клиента, а затем запустят рабочий процесс. При запуске рабочий процесс получает дополнительные сведения о клиенте и обновляет элемент списка собранными данными.</span><span class="sxs-lookup"><span data-stu-id="3cb5a-p122">When the workflow is completed, users will enter a customer ID, then start the workflow. When started, the workflow retrieves additional customer information and updates the list item with the data it has retrieved.</span></span>
  
    
    

1. <span data-ttu-id="3cb5a-188">Запустите Visual Studio 2012 и создайте проект приложения, размещенного в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="3cb5a-188">Start Visual Studio 2012 and create a new SharePoint-hosted app project.</span></span>
    
  
2. <span data-ttu-id="3cb5a-189">В этом проекте создайте настраиваемый список и присвойте ему имя Customers.</span><span class="sxs-lookup"><span data-stu-id="3cb5a-189">In this project, create a new custom list and name it "Customers".</span></span>
    
  
3. <span data-ttu-id="3cb5a-p123">В этом новом списке создайте перечисленные ниже поля. Для каждого поля оставьте тип данных по умолчанию **string**.</span><span class="sxs-lookup"><span data-stu-id="3cb5a-p123">In this new list, create the following fields. Leave the default data type for each field as **string**:</span></span>
    
  - <span data-ttu-id="3cb5a-192">Идентификатор клиента (переименованное поле Title, используемое по умолчанию)</span><span class="sxs-lookup"><span data-stu-id="3cb5a-192">CustomerId (renamed from the default "Title" field)</span></span>
    
  
  - <span data-ttu-id="3cb5a-193">Имя клиента</span><span class="sxs-lookup"><span data-stu-id="3cb5a-193">Customer Name</span></span>
    
  
  - <span data-ttu-id="3cb5a-194">Должность</span><span class="sxs-lookup"><span data-stu-id="3cb5a-194">Job Title</span></span>
    
  
  - <span data-ttu-id="3cb5a-195">Адрес</span><span class="sxs-lookup"><span data-stu-id="3cb5a-195">Address</span></span>
    
  
  - <span data-ttu-id="3cb5a-196">Страна или регион</span><span class="sxs-lookup"><span data-stu-id="3cb5a-196">Country/Region</span></span>
    
  
  - <span data-ttu-id="3cb5a-197">Рабочий телефон</span><span class="sxs-lookup"><span data-stu-id="3cb5a-197">Business Phone</span></span>
    
  
  - <span data-ttu-id="3cb5a-198">Номер факса</span><span class="sxs-lookup"><span data-stu-id="3cb5a-198">Fax Number</span></span>
    
  
4. <span data-ttu-id="3cb5a-199">Теперь добавьте в проект рабочий процесс. Для этого в **обозревателе решений** выберите **Добавить** > **Новый элемент**, а затем в диалоговом окне **Добавление нового элемента** выберите элемент проекта **Рабочий процесс** в категории **Office/SharePoint**.</span><span class="sxs-lookup"><span data-stu-id="3cb5a-199">Now, add a workflow to the project by clicking in **Solution Explorer** on **Add** > **New Item**; then, in the **Add New Item** dialog box, select the **Workflow** project item from the **Office/SharePoint** category.</span></span>
    
  
5. <span data-ttu-id="3cb5a-200">Присвойте рабочему процессу имя CompleteCustomerDetails и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="3cb5a-200">Name the workflow "CompleteCustomerDetails" and click **Next**.</span></span>
    
  
6. <span data-ttu-id="3cb5a-p124">Когда появится запрос **мастера настройки**, присвойте рабочему процессу имя Complete Customer Details и задайте для него тип **Список**. Нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="3cb5a-p124">When prompted by the **Customization wizard**, name the workflow "Complete Customer Details" and set it to be a **List** workflow. Cick **Next**.</span></span>
    
  
7. <span data-ttu-id="3cb5a-p125">На следующей странице мастера установите флажок, чтобы создать связь, выберите список **Клиент**, а затем команду **Создать новый** для журнала рабочих процессов и списков задач. Нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="3cb5a-p125">On the next wizard page, check the box to create an association, select the **Customer** list, then select **Create New** for the workflow history and task lists. Click **Next**.</span></span>
    
  
8. <span data-ttu-id="3cb5a-p126">На последней странице мастера установите флажок, чтобы запустить рабочий процесс вручную. **Не** устанавливайте флажок автоматического запуска. Нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="3cb5a-p126">On the final wizard page, check the box to start the workflow manually; leave the option to start automatically **un** -checked. Click **Finish**.</span></span>
    
  
9. <span data-ttu-id="3cb5a-207">На этом этапе в Visual Studio отображается рабочая область конструирования рабочих процессов, содержащая одно действие **Sequence**.</span><span class="sxs-lookup"><span data-stu-id="3cb5a-207">At this point, Visual Studio displays the workflow designer surface that contains a single **Sequence** activity.</span></span>
    
  
10. <span data-ttu-id="3cb5a-208">Измените имя действия **Sequence** на **Root**.</span><span class="sxs-lookup"><span data-stu-id="3cb5a-208">Change the name of the **Sequence** activity to **Root**.</span></span>
    
  
11. <span data-ttu-id="3cb5a-209">Добавьте еще четыре действия **Sequence** внутри действия Root и назовите их, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="3cb5a-209">Add four more **Sequence** activities inside the Root activity and name them as follows:</span></span>
    
  - <span data-ttu-id="3cb5a-210">Инициализация</span><span class="sxs-lookup"><span data-stu-id="3cb5a-210">Init</span></span>
    
  
  - <span data-ttu-id="3cb5a-211">Получение данных клиентов из службы</span><span class="sxs-lookup"><span data-stu-id="3cb5a-211">Get Customer Data From Service</span></span>
    
  
  - <span data-ttu-id="3cb5a-212">Обработка ответа службы</span><span class="sxs-lookup"><span data-stu-id="3cb5a-212">Process Service Response</span></span>
    
  
  - <span data-ttu-id="3cb5a-213">Обновление элемента списка</span><span class="sxs-lookup"><span data-stu-id="3cb5a-213">Update List Item</span></span>
  
    
    

    
  
12. <span data-ttu-id="3cb5a-214">На этом этапе рабочий процесс выглядит, как показано на рис. 2.</span><span class="sxs-lookup"><span data-stu-id="3cb5a-214">At this point, the workflow will appear as shown in Figure 2.</span></span>
    
   <span data-ttu-id="3cb5a-215">**Рис. 2. Рабочий процесс Complete Customer Details с четырьмя пустыми последовательностями**</span><span class="sxs-lookup"><span data-stu-id="3cb5a-215">**Figure 2. Complete Customer Details Workflow with Four Empty Sequences**</span></span>

  

  ![Рис. 2. Завершение рабочего процесса "Сведения о клиенте"](../images/ngWSSP2013WorkflowVS201202.png)
  

  

  

### <a name="get-the-customer-id-entered-by-the-user"></a><span data-ttu-id="3cb5a-218">Получение идентификатора клиента, введенного пользователем</span><span class="sxs-lookup"><span data-stu-id="3cb5a-218">Get the customer ID entered by the user</span></span>

<span data-ttu-id="3cb5a-p128">Рабочий процесс в первую очередь должен получить идентификатор клиента, введенный пользователем. Для этого необходимо создать две переменные.</span><span class="sxs-lookup"><span data-stu-id="3cb5a-p128">The first thing the workflow needs to do is retrieve the customer ID, as entered by the user. To do this, you need to create two variable.</span></span>
  
    
    

1. <span data-ttu-id="3cb5a-221">Перейдите на вкладку **Переменные** в нижней части конструктора рабочих процессов и создайте две переменные.</span><span class="sxs-lookup"><span data-stu-id="3cb5a-221">Click the **Variables** tab at near the bottom of the workflow designer and create two variables</span></span>
    
  - <span data-ttu-id="3cb5a-p129">**CustomerItemProperties** (тип данных = **DynamicValue**; область = **Init**). Эта переменная используется для хранения результирующего набора, возвращаемого действием, которое получает все свойства из элемента списка.</span><span class="sxs-lookup"><span data-stu-id="3cb5a-p129">**CustomerItemProperties** (data type = **DynamicValue**; scope = **Init**). Use this variable to store the result set returned by the activity that gets all properties from the list item.</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="3cb5a-224">Тип данных **DynamicValue** не отображается по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="3cb5a-224">Note: The **DynamicValue** data type is not shown by default.</span></span> <span data-ttu-id="3cb5a-225">Чтобы найти его, выберите **Выбор типов** в столбце **Тип переменной**.</span><span class="sxs-lookup"><span data-stu-id="3cb5a-225">To find it, select the **Browse for Types** option in the **Variable Type** column.</span></span> <span data-ttu-id="3cb5a-226">В поле поиска в верхней части диалогового окна введите **DynamicValue**, а затем выберите **Microsoft.Activities.DynamicValue**.</span><span class="sxs-lookup"><span data-stu-id="3cb5a-226">In the search box at the top of the dialog, enter **DynamicValue**, and then select the **Microsoft.Activities.DynamicValue**.</span></span> 

  - <span data-ttu-id="3cb5a-227">**CustomerId** (тип данных — **String**, область — **Root**): эта переменная используется для хранения идентификатора клиента, указанного пользователем.</span><span class="sxs-lookup"><span data-stu-id="3cb5a-227">**CustomerId** (data type = **String**; scope = **Root**): Use this variable to store the customer ID entered by the user.</span></span>
    
  
2. <span data-ttu-id="3cb5a-p131">Найдите действие **LookupSpListItem** в разделе панели элементов **SharePoint  список** и перетащите его в последовательность **Инициализация**. Задайте свойства действия, как показано на рис. 3.</span><span class="sxs-lookup"><span data-stu-id="3cb5a-p131">Locate the **LookupSpListItem** activity in the **SP - List** section of the toolbox and drag it to the **Init** sequence. Set the activity properties as shown in Figure 3.</span></span>
    
   <span data-ttu-id="3cb5a-230">**Рис. 3. Окно инструментов "Свойства" для действия LookupSPListItem**</span><span class="sxs-lookup"><span data-stu-id="3cb5a-230">**Figure 3. Properties Tool Window for the LookupSPListItem Activity**</span></span>

  

  ![Рис. 3. Окно "Свойства"](../images/ngWSSP2013WorkflowVS201203.png)
  

    <span data-ttu-id="3cb5a-233">Это действие для Workflow Manager определяет получение свойств текущего элемента списка с помощью REST API SharePoint и хранение ответа **JSON** в только что созданной переменной **DynamicValue**.</span><span class="sxs-lookup"><span data-stu-id="3cb5a-233">This activity tells Workflow Manager to use the SharePoint REST API to retrieve the properties of the current list item and to store the **JSON** response in the **DynamicValue** variable that you just created.</span></span>
    
  
3. <span data-ttu-id="3cb5a-p133">Извлеките идентификатор клиента из элемента списка. Для этого щелкните ссылку Получить свойства в действии **LookupSpListItem**. При этом действие **GetDynamicValueProperties** добавляется в рабочую область конструирования.</span><span class="sxs-lookup"><span data-stu-id="3cb5a-p133">Retrieve the customer ID from the list item by clicking the Get Properties link in the **LookupSpListItem** activity. Doing this adds a **GetDynamicValueProperties** activity to the design surface.</span></span>
    
  
4. <span data-ttu-id="3cb5a-236">В диалоговом окне **Свойства** нажмите многоточие (**...**), чтобы открыть окно "Свойства", как показано на рис. 4.</span><span class="sxs-lookup"><span data-stu-id="3cb5a-236">In the **Properties** dialog box, click the ellipsis ( **???**) to open the Property selector, shown in Figure 4.</span></span> <span data-ttu-id="3cb5a-237">В мастере для параметра **Тип объекта** задайте значение **Элемент списка клиентов**, а затем добавьте одно свойство CustomerId, задав в столбце "Путь" значение CustomerId, а в столбце "Назначить" — значение CustomerId (ранее созданную переменную), как показано на рисунке ниже.</span><span class="sxs-lookup"><span data-stu-id="3cb5a-237">In the wizard, set the **Entity Type** to **List Item of Customers**, then add a single property, CustomerId, with the Path set to CustomerId and Assign To set to CustomerId (the variable previously created), as shown in the following figure.</span></span>
    
  
5. <span data-ttu-id="3cb5a-238">Нажмите кнопку **Создать свойство** и введите **CustomerId** в столбце **Путь**.</span><span class="sxs-lookup"><span data-stu-id="3cb5a-238">Click **Create Property** and enter **CustomerId** in the **Path** column.</span></span>
    
  
6. <span data-ttu-id="3cb5a-p135">В столбце **Кому назначить** введите **CustomerId** (ранее созданную переменную). На рис. 4 показано заполненное диалоговое окно **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="3cb5a-p135">In the **Assign To** column, enter **CustomerId**, which is the variable we created earlier. Figure 4 shows the completed **Properties** dialog box.</span></span>
    
   <span data-ttu-id="3cb5a-241">**Рис. 4. Диалоговое окно "Свойства" для действия GetDynamicValueProperties.**</span><span class="sxs-lookup"><span data-stu-id="3cb5a-241">**Figure 4. Properties dialog for the GetDynamicValueProperties Activity.**</span></span>

  

  ![Рис. 4. Диалоговое окно свойств действия](../images/ngWSSP2013WorkflowVS201204.png)
  

  

  

### <a name="call-the-northwind-odata-web-service"></a><span data-ttu-id="3cb5a-244">Вызов веб-службы Northwind OData</span><span class="sxs-lookup"><span data-stu-id="3cb5a-244">Call the Northwind OData web service</span></span>

<span data-ttu-id="3cb5a-p137">Теперь рабочий процесс содержит ссылку на идентификатор клиента, поэтому следующим шагом является вызов веб-службы. Для этого мы в основном будем работать с последовательностью **Получение данных клиентов из службы**.</span><span class="sxs-lookup"><span data-stu-id="3cb5a-p137">The workflow now has a reference to the customer ID, so the next step is to call the web service. To do this, we'll be working primarily with the **Get Customer Data from Service** sequence.</span></span>
  
    
    

1. <span data-ttu-id="3cb5a-247">Выберите последовательность **Получение данных клиентов из службы** и создайте две переменные.</span><span class="sxs-lookup"><span data-stu-id="3cb5a-247">Select the **Get Customer Data from Service** sequence and create two new variables:</span></span>
    
  - <span data-ttu-id="3cb5a-p138">**NorthwindServiceUri** (тип данных = **String**; область = **Получение данных клиентов из службы**). В этой переменной хранится универсальный код ресурса (URI), который используется для запроса веб-службы.</span><span class="sxs-lookup"><span data-stu-id="3cb5a-p138">**NorthwindServiceUri** (data type = **String**; scope = **Get Customer Data from Service**). This variable stores the URI that is used to query the web service.</span></span>
    
  
  - <span data-ttu-id="3cb5a-250">**NorthwindServiceResponse** (тип данных = **DynamicValue**; область = **Root**). В этой переменной будет храниться ответ веб-службы.</span><span class="sxs-lookup"><span data-stu-id="3cb5a-250">**NorthwindServiceResponse** (data type = **DynamicValue**; scope = **Root**): This variable will store the web service response.</span></span>
    
  
2. <span data-ttu-id="3cb5a-p139">Чтобы создать URL-адрес для запроса веб-службы, сначала найдите действие **Назначить** на панели элементов рабочего процесса, а затем перетащите его в последовательность **Получение данных клиентов из службы**. Обратите внимание, что действие **Назначить** состоит из двух частей, представляющий собой пару "имя-значение".</span><span class="sxs-lookup"><span data-stu-id="3cb5a-p139">To create the URL to query the web service, start by locating an **Assign** activity in the workflow toolbox and drag it to the **Get Customer Data from Service** sequence. Notice that the **Assign** activity has two parts representing a name-value pair.</span></span>
    
  
3. <span data-ttu-id="3cb5a-253">В левой части действия **Назначить** укажите **NorthwindServiceUri**.</span><span class="sxs-lookup"><span data-stu-id="3cb5a-253">Set the left portion of the **Assign** activity to **NorthwindServiceUri**.</span></span>
    
  
4. <span data-ttu-id="3cb5a-p140">В правой части действия введите строку  `"http://services.odata.org/Northwind/Northwind.svc/Customers('" + CustomerId + "')?$format=json"`. Завершенное действие показано на рис. 5.</span><span class="sxs-lookup"><span data-stu-id="3cb5a-p140">Set the right portion of the activity to the string  `"http://services.odata.org/Northwind/Northwind.svc/Customers('" + CustomerId + "')?$format=json"`. Figure 5 shows the completed activity.</span></span>
    
   <span data-ttu-id="3cb5a-256">**Рис. 5. Действие "Назначить", используемое для задания переменной со службой OData**</span><span class="sxs-lookup"><span data-stu-id="3cb5a-256">**Figure 5. Assign Activity Used to Set a Variable Containing the OData Service**</span></span>

  

  ![Рис. 5. Назначение действия](../images/ngWSSP2013WorkflowVS201205.png)
  

  

  
5. <span data-ttu-id="3cb5a-259">Перетащите действие **HttpSend** с панели элементов в последовательность **Получение данных клиентов из службы** и поместите его сразу под действием **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="3cb5a-259">Drag an **HttpSend** activity from the toolbox to the **Get Customer Data from Service** sequence, immediately following the **Assign** activity.</span></span>
    
  
6. <span data-ttu-id="3cb5a-260">Задайте для свойств действия **HttpSend** значения, показанные на рис. 6.</span><span class="sxs-lookup"><span data-stu-id="3cb5a-260">Set the properties on the **HttpSend** activity using the values shown in Figure 6.</span></span>
    
   <span data-ttu-id="3cb5a-261">**Рис. 6. Свойства HttpSend**</span><span class="sxs-lookup"><span data-stu-id="3cb5a-261">**Figure 6. HttpSend Properties**</span></span>

  

  ![Рис. 6. Свойства HttpSend](../images/ngWSSP2013WorkflowVS201206.png)
  

  

  

### <a name="process-the-northwind-odata-web-service-response"></a><span data-ttu-id="3cb5a-264">Обработка ответа веб-службы Northwind OData</span><span class="sxs-lookup"><span data-stu-id="3cb5a-264">Process the Northwind OData web service response</span></span>

<span data-ttu-id="3cb5a-p143">Следующим шагом после запроса веб-службы и сохранения результатов в локальной переменной является обработка ответа. Каждое значение в ответе необходимо добавить в отдельную переменную.</span><span class="sxs-lookup"><span data-stu-id="3cb5a-p143">Once the web service request has been made and the results are stored in a local variable, the next step is to process the response. Each value in the response needs to be added to a different variable.</span></span> 
  
    
    

1. <span data-ttu-id="3cb5a-267">Создайте переменную для каждого из полей, созданных в начале этого пошагового руководства (кроме поля "Идентификатор клиента"), которые показаны ниже.</span><span class="sxs-lookup"><span data-stu-id="3cb5a-267">Create a variable for each of the fields that we created at the start of this walkthrough (except the customer ID field), shown here:</span></span>
    
  - <span data-ttu-id="3cb5a-268">Имя клиента</span><span class="sxs-lookup"><span data-stu-id="3cb5a-268">Customer Name</span></span>
    
  
  - <span data-ttu-id="3cb5a-269">Должность</span><span class="sxs-lookup"><span data-stu-id="3cb5a-269">Job Title</span></span>
    
  
  - <span data-ttu-id="3cb5a-270">Адрес</span><span class="sxs-lookup"><span data-stu-id="3cb5a-270">Address</span></span>
    
  
  - <span data-ttu-id="3cb5a-271">Страна или регион</span><span class="sxs-lookup"><span data-stu-id="3cb5a-271">Country/Region</span></span>
    
  
  - <span data-ttu-id="3cb5a-272">Рабочий телефон</span><span class="sxs-lookup"><span data-stu-id="3cb5a-272">Business Phone</span></span>
    
  
  - <span data-ttu-id="3cb5a-273">Номер факса</span><span class="sxs-lookup"><span data-stu-id="3cb5a-273">Fax Number</span></span>
    
  
2. <span data-ttu-id="3cb5a-274">Назовите каждую из этих переменных в соответствии с именем поля.</span><span class="sxs-lookup"><span data-stu-id="3cb5a-274">Name each of these variables according to its respective field name.</span></span>
    
  
3. <span data-ttu-id="3cb5a-275">Для всех переменных необходимо задать тип **String** и область **Root**.</span><span class="sxs-lookup"><span data-stu-id="3cb5a-275">All of the variables should be of type **String**; all of the variables should be scoped to **Root**.</span></span>
    
  
4. <span data-ttu-id="3cb5a-276">Добавьте действие **GetDynamicValueProperties** в последовательность **Обработка ответа службы**.</span><span class="sxs-lookup"><span data-stu-id="3cb5a-276">Add a **GetDynamicValueProperties** activity to the **Process Service Request** sequence.</span></span>
    
  
5. <span data-ttu-id="3cb5a-277">В окне **Свойства** задайте для свойства **Source** значение **NorthwindServiceResponse**, как показано на рис. 7.</span><span class="sxs-lookup"><span data-stu-id="3cb5a-277">In the **Properties** window, set the **Source** value to **NorthwindServiceResponse**, as shown in Figure 7.</span></span>
    
  
6. <span data-ttu-id="3cb5a-278">Нажмите многоточие (**...**) в окне **Свойства**, а затем укажите значения в столбцах **Путь** и **Назначить**, как показано на рис. 7.</span><span class="sxs-lookup"><span data-stu-id="3cb5a-278">Click the ellipsis button ( **???**) button on the **Properties** property and then provide values in the **Path** and **Assign To** columns as shown in Figure 7.</span></span> <span data-ttu-id="3cb5a-279">Обратите внимание, что значения в столбце **Назначить** являются переменными, созданными для каждого из полей списка **Клиенты**.</span><span class="sxs-lookup"><span data-stu-id="3cb5a-279">Notice that the values in the **Assign To** column are the variable you created for each of the **Customers** list fields.</span></span>
    
   <span data-ttu-id="3cb5a-280">**Рис. 7. Окно инструментов "Свойства" для действия GetDynamicValueProperties и содержимое диалогового окна "Свойства"**</span><span class="sxs-lookup"><span data-stu-id="3cb5a-280">**Figure 7. Properties tool window for GetDynamicValueProperties and contents for Properties dialog**</span></span>

  

  ![Рис. 7. Окно "Свойства"](../images/ngWSSP2013WorkflowVS201207.png)
  

  

  

### <a name="update-the-customer-list-item"></a><span data-ttu-id="3cb5a-283">Обновление элемента списка клиентов</span><span class="sxs-lookup"><span data-stu-id="3cb5a-283">Update the customer list item</span></span>

<span data-ttu-id="3cb5a-284">Вам остается лишь обновить элемент списка.</span><span class="sxs-lookup"><span data-stu-id="3cb5a-284">The last step is to update the list item.</span></span> 
  
    
    

1. <span data-ttu-id="3cb5a-285">Добавьте действие **UpdateListItem** в последовательность **Обновление элемента списка** и задайте следующие значения в окне **Свойства**:</span><span class="sxs-lookup"><span data-stu-id="3cb5a-285">Add an **UpdateListItem** activity to the **Update List Item** sequence and use the **Properties** window to set the following values:</span></span>
    
  - <span data-ttu-id="3cb5a-286">**ListId**: (текущий список);</span><span class="sxs-lookup"><span data-stu-id="3cb5a-286">**ListId**: (current list)</span></span>
    
  
  - <span data-ttu-id="3cb5a-287">**ItemId**: (текущий элемент).</span><span class="sxs-lookup"><span data-stu-id="3cb5a-287">**ItemId**: (current item)</span></span>
    
  
2. <span data-ttu-id="3cb5a-288">Нажмите многоточие (**...**) для свойства **ListItemPropertiesDynamicValues** и в появившемся диалоговом окне задайте для параметра **Тип объекта** значение **Элемент списка клиентов**.</span><span class="sxs-lookup"><span data-stu-id="3cb5a-288">Click the ellipsis button ( **???**) button on the **ListItemPropertiesDynamicValues** property and in the resulting dialog box, set **Entity Type** to **List Item of Customers**.</span></span> 
    
  
3. <span data-ttu-id="3cb5a-289">Наконец, для каждого из значений элементов списка, извлеченных из веб-службы, задайте переменные в рабочем процессе, как показано на рис. 8.</span><span class="sxs-lookup"><span data-stu-id="3cb5a-289">Finally, for each of the values extracted from the web service, set the values on the list item to the variables in the workflow, as shown in Figure 8.</span></span>
    
   <span data-ttu-id="3cb5a-290">**Рис. 8. Диалоговое окно ListItemPropertiesDynamicValue с заданными значениями**</span><span class="sxs-lookup"><span data-stu-id="3cb5a-290">**Figure 8. ListItemPropertiesDynamicValue Dialog with Values Set**</span></span>

  

  ![Рис. 8. Диалоговое окно ListItemPropertiesDynamicValue](../images/ngWSSP2013WorkflowVS201208.png)
  

  

  

### <a name="test-the-workflow"></a><span data-ttu-id="3cb5a-293">Проверка рабочего процесса</span><span class="sxs-lookup"><span data-stu-id="3cb5a-293">Test the workflow</span></span>

<span data-ttu-id="3cb5a-p147">Рабочий процесс готов и должен работать. Чтобы убедиться в его стабильности, его следует проверить.</span><span class="sxs-lookup"><span data-stu-id="3cb5a-p147">The workflow is now complete and should function properly. To confirm its stability, you should test it.</span></span>
  
    
    

1. <span data-ttu-id="3cb5a-296">Нажмите клавишу **F5**, чтобы начать отладку. В Visual Studio будет создано и развернуто приложение, размещенное в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="3cb5a-296">Press **F5** to start debugging; Visual Studio builds and deploys the SharePoint-hosted app.</span></span>
    
  
2. <span data-ttu-id="3cb5a-297">Когда откроется браузер, перейдите к списку **Клиенты**, создайте одну запись клиента с **идентификатором** ALFKI, как показано на рис. 9, а затем сохраните этот элемент.</span><span class="sxs-lookup"><span data-stu-id="3cb5a-297">When the browser opens, navigate to the **Customers** list, create a single customer record with a **Customer Id** of "ALFKI", as shown in Figure 9, and then save the item.</span></span>
    
   <span data-ttu-id="3cb5a-298">**Рис. 9. Новый элемент списка**</span><span class="sxs-lookup"><span data-stu-id="3cb5a-298">**Figure 9. New List Item**</span></span>

  

  ![Рис. 9. Новый элемент списка](../images/ngWSSP2013WorkflowVS201209.png)
  

  

  
3. <span data-ttu-id="3cb5a-p149">После этого вручную запустите рабочий процесс и вернитесь к элементу списка. Обновите страницу, чтобы увидеть элемент списка, обновленный рабочим процессом, как показано на рис. 10.</span><span class="sxs-lookup"><span data-stu-id="3cb5a-p149">Next, manually start the workflow and then go back to the list item. Keep refreshing the page to see the workflow update the list item, as shown in Figure 10</span></span>
    
   <span data-ttu-id="3cb5a-303">**Рис. 10. Обновленный элемент списка**</span><span class="sxs-lookup"><span data-stu-id="3cb5a-303">**Figure 10. Updated List Item**</span></span>

  

  ![Рис. 10. Обновленный элемент списка](../images/ngWSSP2013WorkflowVS201210.png)
  

    <span data-ttu-id="3cb5a-p150">Обратите внимание, что элемент списка обновлен приложением, размещенным в SharePoint, от имени пользователя, который запустил рабочий процесс. Однако в этом пошаговом руководстве его запустил администратор.</span><span class="sxs-lookup"><span data-stu-id="3cb5a-p150">Notice that the list item was updated by the SharePoint hosted app on behalf of the person who started the workflow. In this walkthrough, however, it was started by the administrator.</span></span>
    
  

## <a name="conclusion"></a><span data-ttu-id="3cb5a-307">Заключение</span><span class="sxs-lookup"><span data-stu-id="3cb5a-307">Conclusion</span></span>
<span data-ttu-id="3cb5a-308"><a name="sec5"> </a></span><span class="sxs-lookup"><span data-stu-id="3cb5a-308"><a name="sec5"> </a></span></span>

<span data-ttu-id="3cb5a-p151">В SharePoint представлена новая архитектура рабочих процессов на основе нового продукта: Workflow Manager 1.0. Чтобы все пользовательские рабочие процессы работали независимо от типа развертывания SharePoint (локального или путем размещения в Office 365), все рабочие процессы теперь на 100 % декларативные. Пользовательская бизнес-логика, которая в предыдущих версиях SharePoint реализовывалась в виде пользовательского кода в рабочих процессах, созданных с помощью Visual Studio, больше не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="3cb5a-p151">SharePoint introduced a new workflow architecture facilitated by a new product: Workflow Manager 1.0. To ensure that all custom workflows worked regardless of the SharePoint deployment choice, either on-premises or hosted in Office 365, all workflows are now 100-percent declarative. Therefore, custom business logic previously implemented as custom code in Visual Studio-authored workflows in previous versions of SharePoint are no longer supported.</span></span> 
  
    
    
 <span data-ttu-id="3cb5a-p152">Корпорация Майкрософт добавила поддержку вызова веб-служб в Workflow Manager с помощью нового действия **HttpSend**. Кроме того, в Workflow Manager появилась поддержка создания структур для отправки в веб-службы, а также использования их ответов с помощью типа данных **DynamicValue**. Используйте этот тип данных и связанные действия, чтобы упростить создание и использование надежных бизнес-процессов в рабочих процессах SharePoint с помощью внешних веб-служб.</span><span class="sxs-lookup"><span data-stu-id="3cb5a-p152">Microsoft introduced support for calling web services in Workflow Manager using the new **HttpSend** activity. Workflow Manager also introduced support for creating structures to submit to web services as well as consuming their responses called the **DynamicValue** data type. When creating workflows, use this data type and associated actions to facilitate creating and leveraging robust business processes in SharePoint workflows by using external web services.</span></span>
  
    
    

## <a name="see-also"></a><span data-ttu-id="3cb5a-315">См. также</span><span class="sxs-lookup"><span data-stu-id="3cb5a-315">See also</span></span>
<span data-ttu-id="3cb5a-316"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="3cb5a-316"><a name="bk_addresources"> </a></span></span>


-  [<span data-ttu-id="3cb5a-317">Работа со сложными данными в рабочем процессе</span><span class="sxs-lookup"><span data-stu-id="3cb5a-317">Working with complex data in a workflow</span></span>](http://msdn.microsoft.com/ru-RU/library/windowsazure/jj193446%28v=azure.10%29.aspx)
    
  
-  [<span data-ttu-id="3cb5a-318">Рабочие процессы в SharePoint</span><span class="sxs-lookup"><span data-stu-id="3cb5a-318">Workflows in SharePoint</span></span>](http://msdn.microsoft.com/ru-RU/library/jj163986.aspx)
    
  

