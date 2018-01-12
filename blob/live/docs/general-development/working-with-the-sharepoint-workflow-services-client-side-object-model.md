---
title: "Работа с клиентской объектной моделью для служб рабочих процессов SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: e180c2fb-a903-4ded-884e-b7584fa99189
ms.openlocfilehash: b1c9e9e4e08004a0b190292b70add1c70ccb4e75
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="working-with-the-sharepoint-workflow-services-client-side-object-model"></a><span data-ttu-id="187b8-102">Работа с клиентской объектной моделью для служб рабочих процессов SharePoint</span><span class="sxs-lookup"><span data-stu-id="187b8-102">Working with the SharePoint Workflow Services Client Side Object Model</span></span>
<span data-ttu-id="187b8-p101">Демонстрация использования API клиентской объектной модели SharePoint (CSOM) для создания определений и экземпляров рабочих процессов Workflow Manager 1.0, а также управления ими. **Автор:** [Эндрю Коннелл (Andrew Connell)](http://social.msdn.microsoft.com/profile/andrew%20connell%20%5bmvp%5d/),  [AndrewConnell.com](http://www.andrewconnell.com)</span><span class="sxs-lookup"><span data-stu-id="187b8-p101">Demonstrates how to use the SharePoint client-side object model (CSOM) API to create and control Workflow Manager 1.0 workflow definitions and instances. **Provided by:** [Andrew Connell](http://social.msdn.microsoft.com/profile/andrew%20connell%20%5bmvp%5d/),  [AndrewConnell.com](http://www.andrewconnell.com)</span></span>
  
    
    


## <a name="working-with-the-sharepoint-workflow-services-client-side-object-model"></a><span data-ttu-id="187b8-105">Работа с клиентской объектной моделью для служб рабочих процессов SharePoint</span><span class="sxs-lookup"><span data-stu-id="187b8-105">Working with the SharePoint Workflow Services Client Side Object Model</span></span>

<span data-ttu-id="187b8-p102">Реализация рабочих процессов в SharePoint 2007 и SharePoint 2010 практически не менялась от версии к версии. Корпорация Майкрософт добавила в SharePoint 2010 некоторые функции, например возможность связывать рабочие процессы с сайтами, а также улучшила средства создания рабочих процессов, SharePoint Designer 2010 и Visual Studio 2010, по сравнению с их предшественниками. Тем не менее, реализация задач, форм и серверных интерфейсов API рабочих процессов осталась практически без изменений.</span><span class="sxs-lookup"><span data-stu-id="187b8-p102">The implementation of workflows in SharePoint 2007 and SharePoint 2010 remained largely the same from version to version. Microsoft did add some new functionality in SharePoint 2010, such as the ability to associate workflows with sites, and improved the workflow authoring tools, SharePoint Designer 2010 and Visual Studio 2010, from their predecessors. However, the implementation of workflow tasks, workflow forms, and the workflow server-side APIs remains largely unchanged.</span></span> 
  
    
    
<span data-ttu-id="187b8-p103">В SharePoint 2010 корпорация Майкрософт добавила функции и возможности, которые поощряли перенос настроек в изолированные решения. Они работали в изолированном процессе и были совместимы с обоими типами развертываний SharePoint: локальными, где SharePoint устанавливается на серверах компании, и облачными, в частности Office 365.</span><span class="sxs-lookup"><span data-stu-id="187b8-p103">In SharePoint 2010, Microsoft introduced features and capabilities that encouraged customers to move their customizations into sandboxed solution. These would run in an isolated process and were friendly to both types of SharePoint deployments: on-premises, where the SharePoint was installed on company servers and maintained by the company , and to the cloud, or more specifically, Office 365.</span></span> 
  
    
    
<span data-ttu-id="187b8-p104">В SharePoint добавила еще больше возможностей. Эти обновления были ориентированы на облачные развертывания. В частности, появилась новая модель приложений SharePoint, которая превзошла изолированные решения, поскольку, в отличие от изолированные решения, эти приложения в явной форме блокировали выполнение серверного кода в процессе SharePoint. Кроме того, корпорация Майкрософт усовершенствовала имеющиеся технологии SharePoint, например клиентскую объектную модель (CSOM), и добавила новые возможности, например поддержку удостоверений приложений с использованием  [OAuth](http://msdn.microsoft.com/library/office/fp142382.aspx).</span><span class="sxs-lookup"><span data-stu-id="187b8-p104">In SharePoint, Microsoft added even more capabilities; these updates were oriented toward cloud deployments. Specifically, Microsoft introduced the new SharePoint app model, which went further than the sandboxed solution in that, unlike sandboxed solution, they explicitly blocked server-side code from running in the SharePoint process. Microsoft also built up existing technologies in SharePoint, such as the client-side object model (CSOM), and introduced new capabilities, like support for app identities using  [OAuth](http://msdn.microsoft.com/library/office/fp142382.aspx).</span></span>
  
    
    
<span data-ttu-id="187b8-114">Затем, с выпуском SharePoint, корпорация Майкрософт создала совершенно новые архитектуру и платформу рабочих процессов, которые отражали фундаментальные изменения в направлении развития продукта.</span><span class="sxs-lookup"><span data-stu-id="187b8-114">And then, with the introduction of SharePoint, Microsoft introduced an entirely new workflow architecture and platform that reflect fundamental shifts in the product direction.</span></span> 
  
    
    
<span data-ttu-id="187b8-115">Наиболее заметное изменение — это новая архитектура, в которой рабочие процессы SharePoint больше не выполняются в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="187b8-115">The most prominent change in the new architecture is that workflow execution in SharePoint no longer takes place in SharePoint.</span></span> <span data-ttu-id="187b8-116">Вместо этого SharePoint использует совершенно новый обработчик выполнения: Workflow Manager 1.0.</span><span class="sxs-lookup"><span data-stu-id="187b8-116">Instead, SharePoint uses a completely new execution engine: Workflow Manager 1.0.</span></span> <span data-ttu-id="187b8-117">В Workflow Manager размещаются среда выполнения и все необходимые службы для платформы Windows Workflow.</span><span class="sxs-lookup"><span data-stu-id="187b8-117">Workflow Manager hosts the Windows Workflow Foundation runtime and all the necessary services required by Windows Workflow Foundation.</span></span> <span data-ttu-id="187b8-118">При публикации рабочего процесса или запуске нового экземпляра опубликованного рабочего процесса SharePoint сообщает об этом компоненту Workflow Manager, который затем обрабатывает эпизоды рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="187b8-118">When a workflow is published, or a new instance of a published workflow is started, SharePoint notifies Workflow Manager, which in turn processes the workflow episodes.</span></span> <span data-ttu-id="187b8-119">Если рабочий процесс получает доступ к данным в SharePoint, например свойствам элементов списков или пользователей, он проходит проверку подлинности с помощью протокола OAuth и работает с новыми, улучшенными интерфейсами REST API.</span><span class="sxs-lookup"><span data-stu-id="187b8-119">When the workflow access information in SharePoint, such as list item properties or user properties, it authenticates using the OAuth support and communicates over new and improved REST APIs.</span></span>
  
    
    
<span data-ttu-id="187b8-120">Эти изменения архитектуры рабочих процессов оказывали значительное влияние на некоторые сферы, например настраиваемые формы рабочих процессов, как упоминается в статье "Инструкции. Создание настраиваемых форм рабочих процессов SharePoint с помощью Visual Studio 2012" на сайте MSDN.</span><span class="sxs-lookup"><span data-stu-id="187b8-120">These changes in the workflow architecture had significant impacts in certain areas, such as custom workflow forms, as discussed in the MSDN article How to: Create Custom SharePoint Workflow Forms with Visual Studio 2012.</span></span> <span data-ttu-id="187b8-121">В этой статье упоминается одно из нововведений в SharePoint, связанных поддержкой нового стиля создания настраиваемых форм рабочих процессов: улучшения модели CSOM и добавление API CSOM служб рабочих процессов.</span><span class="sxs-lookup"><span data-stu-id="187b8-121">This article touches on one of the things that Microsoft added to SharePoint to support the new style of creating custom workflow forms: the improvements to the CSOM and addition of the Workflow Services CSOM API.</span></span>
  
    
    

## <a name="introduction-to-the-workflow-services-csom-api-in-sharepoint"></a><span data-ttu-id="187b8-122">Общие сведения об API CSOM служб рабочих процессов в SharePoint</span><span class="sxs-lookup"><span data-stu-id="187b8-122">Introduction to the Workflow Services CSOM API in SharePoint</span></span>

<span data-ttu-id="187b8-p107">В SharePoint 2007 и SharePoint 2010 API рабочих процессов использовался только в серверной объектной модели. В SharePoint по-прежнему присутствует этот API рабочих процессов, поскольку SharePoint включает старую подсистему выполнения рабочих процессов в SharePoint для обратной совместимости.</span><span class="sxs-lookup"><span data-stu-id="187b8-p107">In SharePoint 2007 and SharePoint 2010, the workflow API was manifested only in the server-side object model. In SharePoint, this same workflow API is still present, since SharePoint includes the old workflow execution engine in SharePoint for backward compatibility.</span></span> 
  
    
    
<span data-ttu-id="187b8-p108">Тем не менее, новая и предпочитаемая архитектура рабочих процессов, которая появилась в SharePoint и использует Workflow Manager, включает совершенно новый серверный API. В SharePoint корпорация Майкрософт расширила CSOM, добавив надежный API для новой архитектуры рабочих процессов. Обратите внимание, что это дополнение к CSOM применяется только к новой архитектуры рабочих процессов SharePoint и Workflow Manager 1.0, а не старой версии, которая еще размещается в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="187b8-p108">However, the new and preferred workflow architecture introduced with SharePoint that uses Workflow Manager includes a brand new server-side API. In SharePoint, Microsoft extended the CSOM to include a robust API for the new workflow architecture. Note that this addition to the CSOM only applies to the new SharePoint and Workflow Manager 1.0 workflow architecture, not the legacy version that is still hosted by SharePoint.</span></span>
  
    
    
<span data-ttu-id="187b8-p109">API CSOM служб рабочих процессов, как и другие компоненты CSOM, реализуется как в управляемом API .NET Silverlight, так и в API JavaScript, известном как объектная модель JavaScript (JSOM). Разработчики должны использовать JSOM при создании пользовательских форм рабочих процессов, так как эти формы должны быть веб-формами ASP.NET, которые не содержат код на стороне сервера. Следовательно, API JSOM служб рабочих процессов используется в пользовательских формах сопоставления для создания сопоставлений рабочих процессов, а также в формах запуска для создания экземпляров рабочих процессов.</span><span class="sxs-lookup"><span data-stu-id="187b8-p109">The Workflow Services CSOM API, like the rest of the CSOM, is implemented both in a .NET Silverlight managed API and a JavaScript API known as the JavaScript Object Model (JSOM). JSOM is what developers must use when creating custom workflow forms as those forms will be ASP.NET web forms that must not have any server-side code. Thus the Workflow Services JSOM API is used in custom association forms to create workflow associations as well as on initiation forms to start new workflow instances.</span></span>
  
    
    
<span data-ttu-id="187b8-p110">Тем не менее, возможности этим не ограничиваются. CSOM и JSOM служб рабочих процессов очень надежны и позволяют разработчикам выполнять практически любые действия с рабочими процессами в SharePoint. Разработчики могут не только создавать сопоставления и экземпляры рабочих процессов, но и программным образом развертывать новые определения рабочих процессов, а также связываться с запущенными экземплярами рабочих процессов из CSOM и JSOM, как описано далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="187b8-p110">However, the possibilities do not stop there. The Workflow Services CSOM and JSOM is very robust and enables developers to do almost anything with workflows in SharePoint. Aside from creating workflow associations and instances, developers can also programmatically deploy new workflow definitions and even communicate with running workflow instances from the CSOM and JSOM, as is discussed in the remainder of this article.</span></span>
  
    
    
<span data-ttu-id="187b8-134">В этой статье основное внимание уделяется формам рабочих процессов в контексте SharePoint Server 2013.</span><span class="sxs-lookup"><span data-stu-id="187b8-134">This article focuses on the topic of workflow forms in the context of SharePoint Sever 2013.</span></span> <span data-ttu-id="187b8-135">При написании этой статьи использовались Инструменты разработчика Office для Visual Studio 2013 и SharePoint с общедоступным обновлением за март 2013 г.</span><span class="sxs-lookup"><span data-stu-id="187b8-135">It is based on the SharePoint with the March 2013 Public Update applied and Office Developer Tools for Visual Studio 2013.</span></span> <span data-ttu-id="187b8-136">Все представленные в этой статье сведения применимы как к локальным развертываниям SharePoint, так и к Office 365.</span><span class="sxs-lookup"><span data-stu-id="187b8-136">Everything in this article applies to both SharePoint on-premises deployments as well as Office 365.</span></span>
  
    
    

## <a name="workflow-services-csom-and-jsom-api-components"></a><span data-ttu-id="187b8-137">Компоненты модели CSOM служб рабочих процессов и API JSOM</span><span class="sxs-lookup"><span data-stu-id="187b8-137">Workflow Services CSOM and JSOM API components</span></span>

<span data-ttu-id="187b8-p112">Эта статья посвящена API CSOM служб рабочих процессов, а значит и API JSOM, но в ней не рассматривается серверный API служб рабочих процессов. CSOM служб рабочих процессов состоит нескольких разных служб, которые используются для выполнения различных задач. Все они описываются в последующих разделах.</span><span class="sxs-lookup"><span data-stu-id="187b8-p112">This article focuses on the Workflow Services CSOM API and thus, by extension, the JSOM API as well; the server side Workflow Services API is not discussed here. The Workflow Services CSOM consists of several different services that are used to perform different tasks. Each of these is discussed in the following sections.</span></span> 
  
> [!NOTE] 
> <span data-ttu-id="187b8-p113">Есть еще одна дополнительная служба, которая отсутствует в CSOM, но присутствует в серверном API. Это служба обмена сообщениями, которая используется для управления очередями сообщений и их передачей.</span><span class="sxs-lookup"><span data-stu-id="187b8-p113">There is one additional service that is not present in the CSOM, but is present instead with the server-side API. This is the Messaging Service, which is used to manage message queuing and message transport.</span></span> 
  
    
    

<span data-ttu-id="187b8-p114">Чтобы работать с API CSOM и JSOM разработчики должны добавить необходимые ссылки на свои проекты (в случае CSOM) и страницы (в случае JSOM). Обе реализации имеют одинаковые требования:</span><span class="sxs-lookup"><span data-stu-id="187b8-p114">To work with the Workflow Services CSOM and JSOM APIs, developers must add the necessary references to their projects (in the case of CSOM) and pages (in the case of JSOM). Both implementations have the same requirements:</span></span>
  
    
    

- <span data-ttu-id="187b8-145">Добавьте ссылки на основные библиотеки CSOM и JSOM SharePoint:</span><span class="sxs-lookup"><span data-stu-id="187b8-145">Reference the core SharePoint CSOM and JSOM libraries:</span></span>
    
  - <span data-ttu-id="187b8-146">Microsoft.SharePoint.Client.dll</span><span class="sxs-lookup"><span data-stu-id="187b8-146">Microsoft.SharePoint.Client.dll</span></span>
    
  
  - <span data-ttu-id="187b8-147">Microsoft.SharePoint.Client.Runtime.dll</span><span class="sxs-lookup"><span data-stu-id="187b8-147">Microsoft.SharePoint.Client.Runtime.dll</span></span>
    
  
  - <span data-ttu-id="187b8-148">Microsoft.SharePoint.Client.WorkflowServices.dll</span><span class="sxs-lookup"><span data-stu-id="187b8-148">Microsoft.SharePoint.Client.WorkflowServices.dll</span></span>
    
  

- <span data-ttu-id="187b8-149">Добавьте ссылки на библиотеки CSOM и JSOM служб рабочих процессов:</span><span class="sxs-lookup"><span data-stu-id="187b8-149">Reference the Workflow Services CSOM and JSOM libraries:</span></span>
    
  - <span data-ttu-id="187b8-150">SP.js</span><span class="sxs-lookup"><span data-stu-id="187b8-150">SP.js</span></span>
    
  
  - <span data-ttu-id="187b8-151">SP.Runtime.js</span><span class="sxs-lookup"><span data-stu-id="187b8-151">SP.Runtime.js</span></span>
    
  
  - <span data-ttu-id="187b8-152">SP.WorkflowServices.js</span><span class="sxs-lookup"><span data-stu-id="187b8-152">SP.WorkflowServices.js</span></span>
    
  

### <a name="workflow-service-manager"></a><span data-ttu-id="187b8-153">Диспетчер службы рабочих процессов</span><span class="sxs-lookup"><span data-stu-id="187b8-153">Workflow Service Manager</span></span>

<span data-ttu-id="187b8-p115">Управлять всеми службами, включенными в API CSOM служб рабочих процессов, позволяет диспетчер службы рабочих процессов. Разработчики используют этот объект, чтобы получать экземпляры всех остальных служб, описанных в следующих разделах. Подобно остальным реализациям API CSOM,  [WorkflowServicesManager](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowServicesManager.aspx) имеет зависимость на основную клиентскую объектную модель SharePoint, поэтому на сайт SharePoint, к которому требуется подключиться, нужно передать правильные контекст клиента и ссылку, как показано в следующих примерах кода CSOM и JSOM.</span><span class="sxs-lookup"><span data-stu-id="187b8-p115">The gateway to all services included in the Workflow Services CSOM API is the Workflow Service Manager. This object is what developers use to obtain instances to all the other services described in the following sections. Similar to other CSOM API implementations, the  [WorkflowServicesManager](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowServicesManager.aspx) has a dependency on the core SharePoint CSOM and, therefore, you must pass in a valid client context and reference to the SharePoint site you want to connect to, as shown in the following CSOM and JSOM code examples.</span></span>
  
    
    

#### <a name="csom-creating-a-workflowservicesmanager-instance"></a><span data-ttu-id="187b8-157">CSOM: создание экземпляра объекта WorkflowServicesManager</span><span class="sxs-lookup"><span data-stu-id="187b8-157">CSOM: Creating a WorkflowServicesManager instance</span></span>


```

var clientContext = new ClientContext(siteCollectionUrl);
var workflowServicesManager = new WorkflowServicesManager(clientContext, clientContext.Web); 

```


#### <a name="jsom-creating-a-workflowservicesmanager-instance"></a><span data-ttu-id="187b8-158">JSOM: создание экземпляра объекта WorkflowServicesManager</span><span class="sxs-lookup"><span data-stu-id="187b8-158">JSOM: Creating a WorkflowServicesManager instance</span></span>


```

var clientContext = SP.ClientContext.get_current();
var workflowServicesManager = SP.WorkflowServices.WorkflowServicesManager.newObject(context, context.get_web()); 

```


### <a name="deployment-service"></a><span data-ttu-id="187b8-159">Служба развертывания</span><span class="sxs-lookup"><span data-stu-id="187b8-159">Deployment service</span></span>

<span data-ttu-id="187b8-p116">При создании пользовательских рабочих процессов с помощью Visual Studio 2012, используя пакет решения (*.wsp) или приложение SharePoint (*.app), вы создаете определения рабочих процессов. Определение  это рабочий процесс, а также все бизнес-правила и атрибуты, определенные в нем, например расположение пользовательских форм сопоставления и запуска. Сами по себе эти определения не очень полезны, поскольку их невозможно запускать вне контекста сопоставления с сайтом, списком или библиотекой документов. Определения рабочих процессов, опубликованные и доступные на сайте, можно найти на странице создания сопоставления рабочего процесса, как показано на следующем рисунке.</span><span class="sxs-lookup"><span data-stu-id="187b8-p116">When you create custom workflows using Visual Studio 2012, either using a solution package (*.wsp) or as a SharePoint app (*.app), you are creating workflow definitions. A definition is the workflow process and all business rules and attributes defined within it, such as the location of custom association and initiation forms. On their own, these definitions are not very useful because they cannot be run outside the context of an association with a site, list, or document library. The workflow definitions published and available in a site can be found by going to the page where a new workflow association can be created, as shown in the following figure.</span></span>
  
    
    

<span data-ttu-id="187b8-164">**Рисунок 1. Добавление сопоставления рабочего процесса**</span><span class="sxs-lookup"><span data-stu-id="187b8-164">**Figure 1. Add a workflow association**</span></span>

  
    
    

  
    
    
![Рис. 1. Добавление сопоставления рабочих процессов](../images/ngSP2013WorkflowCSOM01.png)
  
    
    
<span data-ttu-id="187b8-p118">Коллекция опубликованных определений рабочих процессов доступна через службу развертывания. Эта служба позволяет получить список всех сохраненных и опубликованных на данный момент на сайте определений, а также публиковать сохраненные и новые определения, удалять имеющиеся определения и определять, какие действия доступны для рабочих процессов, созданных в SharePoint Designer 2013.</span><span class="sxs-lookup"><span data-stu-id="187b8-p118">The collection of published workflow definitions is accessible through the deployment service. This service enables you to get a list of all currently saved and published definitions on the site, as well as to publish both saved and new definitions, remove existing definitions, and determine what workflow actions are available to SharePoint Designer 2013-authored workflows.</span></span>
  
    
    
<span data-ttu-id="187b8-169">Объект **WorkflowDeploymentService** доступен через класс **WorkflowServicesManager**, как показано в следующих примерах кода.</span><span class="sxs-lookup"><span data-stu-id="187b8-169">The **WorkflowDeploymentService** object is available through the **WorkflowServicesManager** class, as shown in the following code examples.</span></span>
  
    
    

#### <a name="csom-obtaining-a-workflowdeploymentservice-instance"></a><span data-ttu-id="187b8-170">CSOM: получение экземпляра объекта WorkflowDeploymentService</span><span class="sxs-lookup"><span data-stu-id="187b8-170">CSOM: Obtaining a WorkflowDeploymentService instance</span></span>


```

var clientContext = new ClientContext(siteCollectionUrl);
var workflowServicesManager = new WorkflowServicesManager(clientContext, clientContext.Web);
var workflowDeploymentService = workflowServicesManager.GetWorkflowDeploymentService(); 

```


#### <a name="jsom-obtaining-a-workflowdeploymentservice-instance"></a><span data-ttu-id="187b8-171">JSOM: получение экземпляра объекта WorkflowDeploymentService</span><span class="sxs-lookup"><span data-stu-id="187b8-171">JSOM: Obtaining a WorkflowDeploymentService instance</span></span>


```

var clientContext = SP.ClientContext.get_current();
var workflowServicesManager = SP.WorkflowServices.WorkflowServicesManager.newObject(context, context.get_web()); 
var workflowDeploymentService = workflowServicesManager.getWorkflowDeploymentService();

```


### <a name="subscription-service"></a><span data-ttu-id="187b8-172">Служба подписки</span><span class="sxs-lookup"><span data-stu-id="187b8-172">Subscription service</span></span>

<span data-ttu-id="187b8-p119">В предыдущих разделах описывались создание и публикация рабочих процессов в SharePoint в виде определений. Чтобы использовать эти определения, пользователь должен создать сопоставление, которое связывает определение с конкретными сайтом, списком или библиотекой документов SharePoint, а также дополнительными метаданными. В целом этот процесс работает аналогичным образом в SharePoint 2010, но реализация в SharePoint во многом отличается. Workflow Manager 1.0 использует преимущества экземпляра шины обслуживания Microsoft Azure версии 1.0.</span><span class="sxs-lookup"><span data-stu-id="187b8-p119">Recall from the previous section that you create workflows and publish them to SharePoint as definitions. To use these definitions, a user must create an association that links the definition to a specific SharePoint site, list, or document library along with additional metadata. This process basically works and behaves the same way in SharePoint 2010 but the implementation in SharePoint is very different. Workflow Manager 1.0 takes advantage of an instance of Microsoft Azure Service Bus 1.0.</span></span>
  
    
    
<span data-ttu-id="187b8-p120">Шина обслуживания необходима, поскольку она поддерживает службу публикации и подписки (также называемую PubSub). Это асинхронная платформа обмена сообщениями, которая поддерживает отправку сообщений в беседы, сохраненные в шине обслуживания. Любому количеству подписчиков может быть отправлено уведомление, когда в беседе публикуется сообщение, соответствующее определенным условиям.</span><span class="sxs-lookup"><span data-stu-id="187b8-p120">Service Bus is instrumental because it supports the publication and subscription service (also known as PubSub). This is an asynchronous messaging framework that supports a publisher sending a message to a topic stored in Service Bus. Any number of subscribers can request to be notified when a message is published to that topic that meets specific criteria.</span></span> 
  
    
    
<span data-ttu-id="187b8-p121">В SharePoint и Workflow Manager 1.0 для создания сопоставлений используется модель PubSub. Сопоставления рабочих процессов создаются как подписки на беседы. Например, сопоставление с определением рабочего процесса можно создать в списке и настроить для автоматического запуска при добавлении элементов в этот список. Когда в список добавляется элемент, SharePoint публикует в Workflow Manager 1.0 событие, которое затем отсылается в беседу шины обслуживания. Сообщение оценивается, а зарегистрированные подписки получают уведомления о событии. Находится подписанное сопоставление, и запускается рабочий процесс. Дополнительные сведения об этом процессе см. в статье MSDN  [Основные сведения о рабочих процессах в SharePoint](sharepoint-workflow-fundamentals.md).</span><span class="sxs-lookup"><span data-stu-id="187b8-p121">SharePoint and Workflow Manager 1.0 use the PubSub model to create associations. Workflow associations are created as subscriptions on topics. For instance, an association for workflow definition may be created on list and set to start automatically when items are added to the list. When an item is added to the list, SharePoint publishes an event to Workflow Manager 1.0, which it sends to the Service Bus topic. The message is evaluated and the registered subscriptions are notified of the event. The subscribed association is found and the workflow is started. For more information about how this process works, see the MSDN article,  [SharePoint workflow fundamentals](sharepoint-workflow-fundamentals.md).</span></span> 
  
    
    
<span data-ttu-id="187b8-p122">Теперь вам должно быть понятно, почему сопоставления рабочих процессов теперь называются подписками в API (то есть "под капотом"). Вы можете использовать службу подписки в CSOM служб рабочих процессов, чтобы изучать существующие сопоставления и подписки, создавать и удалять их, а также запрашивать уведомления о событиях.</span><span class="sxs-lookup"><span data-stu-id="187b8-p122">This should clarify, then, why workflow associations are now called subscriptions within the API (that is, under the covers). You can use a Subscription Service in the Workflow Services CSOM to explore existing associations and subscriptions, create and delete associations and subscriptions, and request to be notified of events.</span></span>
  
    
    
<span data-ttu-id="187b8-189">Объект  [WorkflowSubscriptionService](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowSubscriptionService.aspx) доступен через класс **WorkflowServicesManager**, как показано в следующих примерах кода.</span><span class="sxs-lookup"><span data-stu-id="187b8-189">The  [WorkflowSubscriptionService](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowSubscriptionService.aspx) object is available through the **WorkflowServicesManager** class, as shown in the following code examples.</span></span>
  
    
    

#### <a name="csom-obtaining-a-workflowsubscriptionservice-instance"></a><span data-ttu-id="187b8-190">CSOM: получение экземпляра объекта WorkflowSubscriptionService</span><span class="sxs-lookup"><span data-stu-id="187b8-190">CSOM: Obtaining a WorkflowSubscriptionService instance</span></span>


```

var clientContext = new ClientContext(siteCollectionUrl);
var workflowServicesManager = new WorkflowServicesManager(clientContext, clientContext.Web);
var workflowSubscriptionService = workflowServicesManager.GetWorkflowSubscriptionService();

```


#### <a name="jsom-obtaining-a-workflowsubscriptionservice-instance"></a><span data-ttu-id="187b8-191">JSOM: получение экземпляра объекта WorkflowSubscriptionService</span><span class="sxs-lookup"><span data-stu-id="187b8-191">JSOM: Obtaining a WorkflowSubscriptionService instance</span></span>


```

var clientContext = SP.ClientContext.get_current();
var workflowServicesManager = SP.WorkflowServices.WorkflowServicesManager.newObject(context, context.get_web()); 
var workflowSubscriptionService = workflowServicesManager.getWorkflowSubscriptionService();

```


### <a name="instance-service"></a><span data-ttu-id="187b8-192">Служба экземпляров</span><span class="sxs-lookup"><span data-stu-id="187b8-192">Instance service</span></span>

<span data-ttu-id="187b8-p123">Последняя служба, которую мы рассмотрим  служба экземпляров. Вы можете использовать эту службу для выполнения нескольких задач, например запуска, приостановки, возобновления, удаления и отмены экземпляров рабочих процессов. Вы также можете использовать ее, чтобы собирать данные отладки, а также перечислять все запущенные на данный момент рабочие процессы. Наконец, вы можете использовать эту службу для публикации событий в запущенных рабочих процессах, как будет показано далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="187b8-p123">The final service that we'll cover is the instance service. You can use this service to perform several tasks with workflow instances, such as starting, suspending, resuming, terminating, and cancelling workflow instances. You can also use it to collect debug information, as well as enumerate through all currently running workflows, as well as those that have already completed. Finally, you can use this service to publish events to workflows that are currently running, as we'll see later in this article.</span></span>
  
    
    
<span data-ttu-id="187b8-197">Объект  [WorkflowInstanceService](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowInstanceService.aspx) доступен через класс **WorkflowServicesManager**, как показано в следующих примерах кода.</span><span class="sxs-lookup"><span data-stu-id="187b8-197">The  [WorkflowInstanceService](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowInstanceService.aspx) object is available through the **WorkflowServicesManager** class, as shown in the following code examples.</span></span>
  
    
    

#### <a name="csom-obtaining-a-workflowinstanceservice-instance"></a><span data-ttu-id="187b8-198">CSOM: получение экземпляра объекта WorkflowInstanceService</span><span class="sxs-lookup"><span data-stu-id="187b8-198">CSOM: Obtaining a WorkflowInstanceService instance</span></span>


```

var clientContext = new ClientContext(siteCollectionUrl);
var workflowServicesManager = new WorkflowServicesManager(clientContext, clientContext.Web);
var workflowInstanceService = workflowServicesManager.GetWorkflowInstanceService();

```


#### <a name="jsom-obtaining-a-workflowinstanceservice-instance"></a><span data-ttu-id="187b8-199">JSOM: получение экземпляра объекта WorkflowInstanceService</span><span class="sxs-lookup"><span data-stu-id="187b8-199">JSOM: Obtaining a WorkflowInstanceService instance</span></span>


```

var clientContext = SP.ClientContext.get_current();
var workflowServicesManager = SP.WorkflowServices.WorkflowServicesManager.newObject(context, context.get_web()); 
var workflowInstanceService = workflowServicesManager.getWorkflowInstanceService();

```


### <a name="interop-service"></a><span data-ttu-id="187b8-200">Служба взаимодействия</span><span class="sxs-lookup"><span data-stu-id="187b8-200">Interop service</span></span>

<span data-ttu-id="187b8-p124">В предыдущих версиях SharePoint, в частности SharePoint 2007 и SharePoint 2010, размещалась среда выполнения Windows Workflow Foundation. Как описывалось ранее, корпорация Майкрософт отказалась от этого подхода в SharePoint, добавив зависимость от Workflow Manager 1.0, в которой размещается среда выполнения рабочих процессов за пределами SharePoint. Следовательно, выполнение рабочих процессов и управление ими больше не выполняются в SharePoint. Вместо этого SharePoint передает управление рабочими процессами и обязанности по выполнению серверу Workflow Manager 1.0.</span><span class="sxs-lookup"><span data-stu-id="187b8-p124">In previous versions of SharePoint, specifically SharePoint 2007 and SharePoint 2010, SharePoint hosted the Windows Workflow Foundation runtime. As previously explained, Microsoft moved away from this approach in SharePoint by introducing a dependency on Workflow Manager 1.0, which hosts the workflow runtime outside of SharePoint. Consequently, workflows are no longer executed and managed within SharePoint; instead, SharePoint hands off workflow management and execution responsibilities to Workflow Manager 1.0.</span></span>
  
    
    
<span data-ttu-id="187b8-p125">Тем не менее, для обеспечения обратной совместимости корпорация Майкрософт сохранила устаревшую модель размещения рабочих процессов в стиле SharePoint в SharePoint, сохранив подсистему среды выполнения Windows Workflow Foundation. Следовательно, все рабочие процессы, созданные в SharePoint 2010, будут выполняться в среде SharePoint как обычно. Кроме того, корпорация Майкрософт добавила новое действие, **InvokeSharePointWorkflow**, которое можно использовать в рабочем процессе SharePoint для запуска существующего рабочего процесса на узле SharePoint 2010, включенном в SharePoint. Это позволяет пользоваться преимуществами существующих инвестиций в рабочие процессы, перенесенные из предыдущих версий.</span><span class="sxs-lookup"><span data-stu-id="187b8-p125">However, to provide backward compatibility, Microsoft retained the legacy model of hosting pre-SharePoint-style workflows within SharePoint by keeping the Windows Workflow Foundation runtime engine. Therefore, all workflows created in SharePoint 2010 will still run as expected in a SharePoint environment. In addition, Microsoft included a new activity, **InvokeSharePointWorkflow**, which can be used in a SharePoint workflow to start an existing workflow in the SharePoint 2010 workflow host that is included in SharePoint. This allows you to take advantage of existing workflow investments migrated from previous versions.</span></span>
  
> [!NOTE] 
> <span data-ttu-id="187b8-208">Действие **InvokeSharePointWorkflow** представляет собой оболочку для метода CSOM [StartWorkflow](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.WorkflowServices.InteropService.StartWorkflow.aspx).</span><span class="sxs-lookup"><span data-stu-id="187b8-208">**Note:** The [InvokeSharePointWorkflow](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.WorkflowServices.InteropService.StartWorkflow.aspx) activity is a wrapper for the CSOM method, StartWorkflow .</span></span>
  
    
    

<span data-ttu-id="187b8-p126">CSOM служб рабочих процессов SharePoint также включает специальную службу, которая позволяет разработчикам взаимодействовать с устаревшими рабочими процессами.  [InteropService](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.WorkflowServices.InteropService.aspx) позволяет запускать и останавливать рабочие процессы, а также включать и отключать уведомления о событиях для запущенных рабочих процессов.</span><span class="sxs-lookup"><span data-stu-id="187b8-p126">The SharePoint Workflow Services CSOM also includes a special service that enables developers to interact with these legacy workflows. The  [InteropService](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.WorkflowServices.InteropService.aspx) lets you start and stop workflows, as well as enable and disable event notifications for running workflows.</span></span>
  
    
    
<span data-ttu-id="187b8-211">Объект  [WorkflowDeploymentService](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.WorkflowServices.WorkflowDeploymentService.aspx) доступен через класс **WorkflowServicesManager**, как показано в следующих примерах кода CSOM и JSOM.</span><span class="sxs-lookup"><span data-stu-id="187b8-211">The  [WorkflowDeploymentService](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.WorkflowServices.WorkflowDeploymentService.aspx) object is available through the **WorkflowServicesManager** class, as shown in the following CSOM and JSOM code examples.</span></span>
  
    
    

#### <a name="csom-obtaining-an-interopservice-instance"></a><span data-ttu-id="187b8-212">CSOM: получение экземпляра объекта InteropService</span><span class="sxs-lookup"><span data-stu-id="187b8-212">CSOM: Obtaining an InteropService instance</span></span>


```

var clientContext = new ClientContext(siteCollectionUrl);
var workflowServicesManager = new WorkflowServicesManager(clientContext, clientContext.Web);
var workflowInteropService = workflowServicesManager.GetWorkflowInteropService();

```


#### <a name="jsom-obtaining-an-interopservice-instance"></a><span data-ttu-id="187b8-213">JSOM: получение экземпляра объекта InteropService</span><span class="sxs-lookup"><span data-stu-id="187b8-213">JSOM: Obtaining an InteropService instance</span></span>


```

var clientContext = SP.ClientContext.get_current();
var workflowServicesManager = SP.WorkflowServices.WorkflowServicesManager.newObject(context, context.get_web()); 
var workflowInteropService = serviceManager.getWorkflowInteropService();

```


## <a name="example-workflow-services-csom-scenarios"></a><span data-ttu-id="187b8-214">Пример. Сценарии CSOM служб рабочих процессов</span><span class="sxs-lookup"><span data-stu-id="187b8-214">Example: Workflow Services CSOM scenarios</span></span>

<span data-ttu-id="187b8-215">В следующих разделах описывается использование разных служб в CSOM служб рабочих процессов для выполнения распространенных задач в пользовательских решениях.</span><span class="sxs-lookup"><span data-stu-id="187b8-215">The following sections demonstrate how to use the different services in the Workflow Services CSOM to perform common tasks in custom solutions.</span></span> 
  
    
    

### <a name="get-all-workflows-installed"></a><span data-ttu-id="187b8-216">Получение всех установленных рабочих процессов</span><span class="sxs-lookup"><span data-stu-id="187b8-216">Get all workflows installed</span></span>

<span data-ttu-id="187b8-p127">Большинство других служб в CSOM служб рабочих процессов требуют, чтобы вы получали ссылки на ранее опубликованное определение рабочего процесса. Как правило, для ссылок на определения рабочих процессов используются их идентификаторы, то есть GUID.</span><span class="sxs-lookup"><span data-stu-id="187b8-p127">Most of the other services in the Workflow Services CSOM require that you get references to the workflow definition that was previously published. Workflow definitions are usually referenced by their IDs, which are GUIDs.</span></span> 
  
    
    
<span data-ttu-id="187b8-p128">Чтобы получить список всех опубликованных определений рабочих процессов, сначала получите экземпляр службы развертывания с помощью метода  [GetWorkflowDeploymentService](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.WorkflowServices.WorkflowServicesManager.GetWorkflowDeploymentService.aspx) . Затем получите коллекцию всех определений рабочих процессов с помощью метода [EnumerateDefinitions(Boolean)](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.WorkflowServices.WorkflowDeploymentService.EnumerateDefinitions.aspx) . Ниже приводится пример кода:</span><span class="sxs-lookup"><span data-stu-id="187b8-p128">To get a list of all the published workflow definitions, first get an instance of the deployment service by using the  [GetWorkflowDeploymentService](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.WorkflowServices.WorkflowServicesManager.GetWorkflowDeploymentService.aspx) method. Then, retrieve the collection of all workflow definitions by using the [EnumerateDefinitions(Boolean)](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.WorkflowServices.WorkflowDeploymentService.EnumerateDefinitions.aspx) method. Here is example code:</span></span>
  
    
    



```

// connect to the workflow services via a CSOM client context
var clientContext = new ClientContext(siteCollectionUrl);
var workflowServicesManager = new WorkflowServicesManager(clientContext, clientContext.Web);

// connect to the deployment service 
var workflowDeploymentService = workflowServicesManager.GetWorkflowDeploymentService();

// get all installed workflows
var publishedWorkflowDefinitions = workflowDeploymentService.EnumerateDefinitions(true);
clientContext.Load(publishedWorkflowDefinitions);
clientContext.ExecuteQuery();

// display list of all installed workflows
foreach (var workflowDefinition in publishedWorkflowDefinitions) {
  Console.WriteLine("{0} - {1}", workflowDefinition.Id.ToString(), workflowDefinition.DisplayName);
}

```


### <a name="get-all-associations-and-subscriptions"></a><span data-ttu-id="187b8-222">Получение всех сопоставлений и подписок</span><span class="sxs-lookup"><span data-stu-id="187b8-222">Get all associations and subscriptions</span></span>

<span data-ttu-id="187b8-p129">Чтобы запустить новый экземпляр рабочего процесса, необходимо сначала получить ссылку на существующее сопоставление рабочего процесса. Следующий пример кода, основанный на предыдущем, демонстрирует, как получить список всех сопоставлений рабочих процессов для заданного определения на сайте.</span><span class="sxs-lookup"><span data-stu-id="187b8-p129">To start a new workflow instance, you need to first get a reference to an existing workflow association. Building on the previous code example, the following example demonstrates how to get a list of all workflow associations for a specific workflow definition in a site.</span></span> 
  
    
    
<span data-ttu-id="187b8-p130">Получив определение рабочего процесса с помощью приведенного выше примера, используйте метод  [GetWorkflowSubscriptionService](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.WorkflowServices.WorkflowServicesManager.GetWorkflowSubscriptionService.aspx) для создания экземпляра службы подписки. Затем используйте метод [EnumerateSubscriptionsByDefinition](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.WorkflowServices.WorkflowSubscriptionService.EnumerateSubscriptionsByDefinition.aspx) (передав идентификатор определения рабочего процесса), чтобы получить список всех сопоставлений для указанного рабочего процесса. Обратите внимание, что доступно несколько методов получения рабочих процессов, включая следующие:</span><span class="sxs-lookup"><span data-stu-id="187b8-p130">Once you have obtained a workflow definition using the example above, use the  [GetWorkflowSubscriptionService](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.WorkflowServices.WorkflowServicesManager.GetWorkflowSubscriptionService.aspx) method to create an instance of the subscription service. Next, use the [EnumerateSubscriptionsByDefinition](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.WorkflowServices.WorkflowSubscriptionService.EnumerateSubscriptionsByDefinition.aspx) method (passing in the ID of a workflow definition) to get a list of all the associations that exist for the specified workflow. Note that there are several methods available for getting workflow associations, including the following:</span></span>
  
    
    

-  [<span data-ttu-id="187b8-228">EnumerateSubscriptions</span><span class="sxs-lookup"><span data-stu-id="187b8-228">EnumerateSubscriptions</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.WorkflowServices.WorkflowSubscriptionService.EnumerateSubscriptions.aspx)
    
  
-  [<span data-ttu-id="187b8-229">EnumerateSubscriptionsByDefinition</span><span class="sxs-lookup"><span data-stu-id="187b8-229">EnumerateSubscriptionsByDefinition</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.WorkflowServices.WorkflowSubscriptionService.EnumerateSubscriptionsByDefinition.aspx)
    
  
-  [<span data-ttu-id="187b8-230">EnumerateSubscriptionsByEventSource</span><span class="sxs-lookup"><span data-stu-id="187b8-230">EnumerateSubscriptionsByEventSource</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.WorkflowServices.WorkflowSubscriptionService.EnumerateSubscriptionsByEventSource.aspx)
    
  
-  [<span data-ttu-id="187b8-231">EnumerateSubscriptionsByList</span><span class="sxs-lookup"><span data-stu-id="187b8-231">EnumerateSubscriptionsByList</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.WorkflowServices.WorkflowSubscriptionService.EnumerateSubscriptionsByList.aspx)
    
  
<span data-ttu-id="187b8-232">Следующий пример кода демонстрирует получение сопоставлений и подписок.</span><span class="sxs-lookup"><span data-stu-id="187b8-232">The following code example demonstrates getting associations and subscriptions.</span></span>
  
    
    



```

// connect to the workflow services via a CSOM client context
var clientContext = new ClientContext(siteCollectionUrl);
var workflowServicesManager = new WorkflowServicesManager(clientContext, clientContext.Web);

// connect to the deployment service
var workflowDeploymentService = workflowServicesManager.GetWorkflowDeploymentService();

// get all installed workflows
var publishedWorkflowDefinitions = workflowDeploymentService.EnumerateDefinitions(true);
clientContext.Load(publishedWorkflowDefinitions);
clientContext.ExecuteQuery();

// find the first workflow definition
var firstWorkflowDefinition = publishedWorkflowDefinitions.First();

// connect to the subscription service
var workflowSubscriptionService = workflowServicesManager.GetWorkflowSubscriptionService();

// get all workflow associations
var workflowAssociations = workflowSubscriptionService.EnumerateSubscriptionsByDefinition(firstWorkflowDefinition.Id);
clientContext.Load(workflowAssociations);
clientContext.ExecuteQuery();

foreach (var association in workflowAssociations) {
  Console.WriteLine("{0} - {1}",
    association.Id, association.Name);
}

```


### <a name="creating-a-workflow-association"></a><span data-ttu-id="187b8-233">Создание сопоставления рабочего процесса</span><span class="sxs-lookup"><span data-stu-id="187b8-233">Creating a workflow association</span></span>

<span data-ttu-id="187b8-p131">Для создания нового сопоставления рабочего процесса, на которое также можно ссылаться как на подписку, необходимы дополнительные действия, прежде чем вы сможете опубликовать сопоставление в SharePoint. Это вызвано тем, что каждая подписка должна включать дополнительные сведения, которые обычно собираются на странице сопоставления. Эти метаданные включают следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="187b8-p131">Creating a new workflow association, which can also be referred to as a subscription, requires additional effort before actually publishing the association to SharePoint. This is because each subscription needs to have additional information, which is usually collected on the association page. This metadata includes the following:</span></span>
  
    
    

- <span data-ttu-id="187b8-237">Идентификатор определения рабочего процесса, на котором основано сопоставление.</span><span class="sxs-lookup"><span data-stu-id="187b8-237">The ID of the workflow definition the association is based on.</span></span>
    
  
- <span data-ttu-id="187b8-238">Идентификатор сайта, списка или библиотеки документов SharePoint, где создано сопоставление.</span><span class="sxs-lookup"><span data-stu-id="187b8-238">The ID of the SharePoint site, list or document library the workflow association is created on.</span></span>
    
  
- <span data-ttu-id="187b8-239">Отображаемое имя сопоставления.</span><span class="sxs-lookup"><span data-stu-id="187b8-239">The display name of the association.</span></span> 
    
  
- <span data-ttu-id="187b8-240">Параметры запуска (ручной или автоматический запуск при добавлении или изменении элемента).</span><span class="sxs-lookup"><span data-stu-id="187b8-240">The startup options (whether started manually or automatically when a list item is added or updated).</span></span>
    
  
- <span data-ttu-id="187b8-241">Идентификатор списка, в котором будут храниться все сообщения списка журнала для этого сопоставления.</span><span class="sxs-lookup"><span data-stu-id="187b8-241">The ID of the list that will store all history list messages for this association.</span></span>
    
  
- <span data-ttu-id="187b8-242">Идентификатор списка, в котором будут храниться все задачи для этого сопоставления.</span><span class="sxs-lookup"><span data-stu-id="187b8-242">The ID of the list that will store all tasks for this association.</span></span>
    
  
- <span data-ttu-id="187b8-p132">Коллекция пар "имя-значение", которые следует отправлять в рабочий процесс (необязательно). Эти поля обычно передаются из пользовательской формы сопоставления.</span><span class="sxs-lookup"><span data-stu-id="187b8-p132">Optionally, a collection of any name/value pairs that should be sent to the workflow. These are the fields that are usually passed in from a custom association form.</span></span>
    
  

### <a name="creating-a-custom-workflow-association"></a><span data-ttu-id="187b8-245">Создание пользовательского сопоставления рабочего процесса</span><span class="sxs-lookup"><span data-stu-id="187b8-245">Creating a custom workflow association</span></span>


1. <span data-ttu-id="187b8-246">Чтобы создать пользовательское сопоставление, сначала воспользуйтесь методом  [GetWorkflowSubscriptionService](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.WorkflowServices.WorkflowServicesManager.GetWorkflowSubscriptionService.aspx) , чтобы получить ссылку на службу подписки.</span><span class="sxs-lookup"><span data-stu-id="187b8-246">To create a custom association, first use the  [GetWorkflowSubscriptionService](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.WorkflowServices.WorkflowServicesManager.GetWorkflowSubscriptionService.aspx) method to get a reference to the subscription service.</span></span>
    
```
  
// connect to the deployment service
var workflowDeploymentService = workflowServicesManager.GetWorkflowDeploymentService();

// get all installed workflows
var publishedWorkflowDefinitions = workflowDeploymentService.EnumerateDefinitions(true);
clientContext.Load(publishedWorkflowDefinitions);
clientContext.ExecuteQuery();

// find the first workflow definition
var firstWorkflowDefinition = publishedWorkflowDefinitions.First();

// connect to the subscription service
var workflowSubscriptionService = workflowServicesManager.GetWorkflowSubscriptionService();

```

2. <span data-ttu-id="187b8-247">Создайте новый экземпляр объекта для класса  [WorkflowSubscription](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.WorkflowServices.WorkflowSubscription.aspx) .</span><span class="sxs-lookup"><span data-stu-id="187b8-247">Create a new object instance of the  [WorkflowSubscription](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.WorkflowServices.WorkflowSubscription.aspx) class.</span></span>
    
  
3. <span data-ttu-id="187b8-p133">Задайте необходимые свойства объекта **WorkflowSubscription**, как показано в следующем примере кода. В комментариях к этому примеру описывается каждый из параметров свойств. Обратите внимание, что некоторые свойства, которые не связаны со службами рабочих процессов CSOM, не включены в пример для удобочитаемости. Пропущены следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="187b8-p133">Set the required properties on the **WorkflowSubscription** object, as illustrated in the following code example. In the example, code comments explain each of the property settings. Note that some properties that are not relevant to CSOM workflow services have been left out for readability. These properties have been omitted:</span></span>
    
1. <span data-ttu-id="187b8-p134">**listId**. Идентификатор списка, в котором создано сопоставление.</span><span class="sxs-lookup"><span data-stu-id="187b8-p134">**listId**. The ID of the list on which the association is created.</span></span>
    
  
2. <span data-ttu-id="187b8-p135">**historyListId**. Идентификатор списка, в котором хранятся все сообщения списка журнала для сопоставления.</span><span class="sxs-lookup"><span data-stu-id="187b8-p135">**historyListId**. The ID of the list that stores all history list messages for the association.</span></span>
    
  
3. <span data-ttu-id="187b8-p136">**taskListId**. Идентификатор списка, в котором будут храниться все задачи для сопоставления.</span><span class="sxs-lookup"><span data-stu-id="187b8-p136">**taskListId**. The ID of the list that will store all tasks for the association.</span></span>
    
  
4. <span data-ttu-id="187b8-258">После создания подписки ее необходимо опубликовать в SharePoint с помощью метода  [PublishSubscriptionForList](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.WorkflowServices.WorkflowSubscriptionService.PublishSubscriptionForList.aspx) , как показано в следующем примере кода:</span><span class="sxs-lookup"><span data-stu-id="187b8-258">Once created, the subscription must be published to SharePoint using the  [PublishSubscriptionForList](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.WorkflowServices.WorkflowSubscriptionService.PublishSubscriptionForList.aspx) method, as demonstrated in the following code example:</span></span>
    
```
  
// create a new association / subscription
WorkflowSubscription newSubscription = new WorkflowSubscription(clientContext) {
  DefinitionId = firstWorkflowDefinition.Id,
  Enabled = true,
  Name = "New Workflow Association"
};


var startupOptions = new List<string>();
// automatic start
startupOptions.Add("ItemAdded");
startupOptions.Add("ItemUpdated");
// manual start
startupOptions.Add("WorkflowStart");

// set the workflow start settings
newSubscription.EventTypes = startupOptions;


// set the associated task and history lists
newSubscription.SetProperty("HistoryListId", workflowHistoryListId.ToString());
newSubscription.SetProperty("TaskListId", workflowTaskListId.ToString());

// OPTIONAL: add any association form values
newSubscription.SetProperty("Prop1","Value1");
newSubscription.SetProperty("Prop2","Value2");

// create the association
workflowSubscriptionService.PublishSubscriptionForList(newSubscription, listId);
clientContext.ExecuteQuery();

```


### <a name="get-all-workflow-instances"></a><span data-ttu-id="187b8-259">Получение всех экземпляров рабочих процессов</span><span class="sxs-lookup"><span data-stu-id="187b8-259">Get all workflow instances</span></span>

<span data-ttu-id="187b8-p137">Вы также можете использовать службу экземпляров служб рабочих процессов, чтобы просматривать все экземпляры рабочих процессов, запущенные на сайте, в списке или в библиотеке документов SharePoint. Возвращаемый объект экземпляра содержит сведения об экземпляре, например время последнего обновления, текущее состояние и все ошибки, которые могли возникнуть во время предыдущих запусков. Кроме того, он предоставляет коллекцию пар "имя-значение", которые были отправлены рабочему процессу из пользовательской формы запуска.</span><span class="sxs-lookup"><span data-stu-id="187b8-p137">You can also use the Workflow Services instance service to view all workflow instances that are running on a SharePoint site, list, or document library. The instance object that is returned contains information on the instance, such as when it was last updated, the current status, and any errors that may have occurred when it ran previously. Additionally, it provides a collection of name/value pairs that were submitted to the workflow from the custom initiation form.</span></span>
  
    
    
<span data-ttu-id="187b8-p138">Для этого сначала используйте метод  [GetWorkflowInstanceService](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.WorkflowServices.WorkflowServicesManager.GetWorkflowInstanceService.aspx) , чтобы получить ссылку на службу экземпляров. Обратите внимание, что [WorkflowInstanceService](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.WorkflowServices.WorkflowInstanceService.aspx) предоставляет несколько методов для получения коллекции запущенных экземпляров рабочих процессов:</span><span class="sxs-lookup"><span data-stu-id="187b8-p138">To do this, start by using the  [GetWorkflowInstanceService](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.WorkflowServices.WorkflowServicesManager.GetWorkflowInstanceService.aspx) method to get a reference to the instance service. Note that the [WorkflowInstanceService](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.WorkflowServices.WorkflowInstanceService.aspx) provides several methods for obtaining the collection of running workflow instances:</span></span>
  
    
    

-  <span data-ttu-id="187b8-p139">[Enumerate](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.WorkflowServices.WorkflowInstanceService.Enumerate.aspx) . Принимает сопоставление рабочего процесса (то есть подписку) в качестве параметра, и его можно использовать для получения всех созданных экземпляров по указанному сопоставлению.</span><span class="sxs-lookup"><span data-stu-id="187b8-p139">[Enumerate](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.WorkflowServices.WorkflowInstanceService.Enumerate.aspx) . Accepts a workflow association (that is, a subscription) as a parameter, and can be used to get all the instances that have been created based on the specified association.</span></span>
    
  
-  <span data-ttu-id="187b8-267">[EnumerateInstancesForSite](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.WorkflowServices.WorkflowInstanceService.EnumerateInstancesForSite.aspx) . Получает список всех экземпляров рабочих процессов, запущенных на сайте SharePoint, заданном при создании объекта **WorkflowServiceManager**.</span><span class="sxs-lookup"><span data-stu-id="187b8-267">[EnumerateInstancesForSite](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.WorkflowServices.WorkflowInstanceService.EnumerateInstancesForSite.aspx) : Gets a list of all workflow instances that have been started on the SharePoint site that was set when creating the original **WorkflowServiceManager** object.</span></span>
    
  
-  <span data-ttu-id="187b8-p140">[EnumerateInstancesForListItem](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.WorkflowServices.WorkflowInstanceService.EnumerateInstancesForListItem.aspx) . Принимает идентификаторы списка и элементы: используйте этот метод, чтобы получить все экземпляры рабочих процессов, созданные в определенном элементе списка.</span><span class="sxs-lookup"><span data-stu-id="187b8-p140">[EnumerateInstancesForListItem](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.WorkflowServices.WorkflowInstanceService.EnumerateInstancesForListItem.aspx) . Accepts a list ID and item ID; use this method to get all workflow instances that have been created on a specific list item.</span></span>
    
  
<span data-ttu-id="187b8-p141">У каждого из этих методов также есть альтернативный метод \***WithOffset()** (например, [EnumerateWithOffset](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.WorkflowServices.WorkflowInstanceService.EnumerateWithOffset.aspx) ). Эти альтернативные методы позволяют получить подмножество экземпляров рабочего процесса в тех случаях, когда работать со всей коллекцией неудобно. Чтобы получить количество экземпляров рабочих процессов, используйте метод [CountInstances](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.WorkflowServices.WorkflowInstanceService.CountInstances.aspx) или [CountInstancesWithStatus](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.WorkflowServices.WorkflowInstanceService.CountInstancesWithStatus.aspx) .</span><span class="sxs-lookup"><span data-stu-id="187b8-p141">Each of theses methods also has an alternate \***WithOffset()** method (for example, [EnumerateWithOffset](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.WorkflowServices.WorkflowInstanceService.EnumerateWithOffset.aspx) ). These alternative methods allow you to get a subset of the workflow instances in cases where working with the entire collection would be cumbersome. To get a count of the number of workflow instances, use the [CountInstances](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.WorkflowServices.WorkflowInstanceService.CountInstances.aspx) method, or the [CountInstancesWithStatus](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.WorkflowServices.WorkflowInstanceService.CountInstancesWithStatus.aspx) method.</span></span>
  
    
    
<span data-ttu-id="187b8-273">Следующий пример кода иллюстрирует получение экземпляров рабочих процессов:</span><span class="sxs-lookup"><span data-stu-id="187b8-273">The following code example illustrates getting workflow instances:</span></span>
  
    
    



```

// connect to the instance service
var workflowInstanceService = workflowServicesManager.GetWorkflowInstanceService();

// get all instances
var workflowInstances = workflowInstanceService.EnumerateInstancesForListItem(listId, listItemId);
foreach (var instance in workflowInstances)
{
  Console.WriteLine("{0} - {1} - {2}",
                    instance.Id.ToString(),
                    instance.LastUpdated,
                    instance.Status.ToString());
}
```


### <a name="start-a-workflow-instance"></a><span data-ttu-id="187b8-274">Запуск экземпляра рабочего процесса</span><span class="sxs-lookup"><span data-stu-id="187b8-274">Start a workflow instance</span></span>

<span data-ttu-id="187b8-p142">Чтобы запустить экземпляр сопоставления рабочего процесса, необходимо повторить многие из действий, показанных в предыдущих примерах. Чтобы запустить рабочий процесс для элемента в списке или библиотеке документов, сначала получите ссылку на сопоставление рабочего процесса и идентификатор элемента в списке. Коллекцию пар "имя-значение" можно отправить рабочему процессу при его запуске. Это происходит, если для сбора данных пользователя, запускающего рабочий процесс, используется пользовательская форма запуска. Затем при запуске необходимо передать коллекцию, даже если она пустая, иначе рабочий процесс не запустится и возвратит ошибку.</span><span class="sxs-lookup"><span data-stu-id="187b8-p142">Starting a new instance of a workflow association involves repeating many of the steps that have been demonstrated in the previous examples. To start a workflow on an item in a list or document library, first obtain a reference to the workflow association and the ID of the item in the list. A collection of name/value pairs of information can be sent to the workflow when it is started. This happens when there is a custom initiation form that is used to collect data from the user starting the workflow. Then pass in a collection, even if it is an empty collection, when starting the workflow or the workflow will fail to start and return an error.</span></span>
  
    
    
<span data-ttu-id="187b8-p143">Отталкиваясь от предыдущих примеров, используйте метод  [GetWorkflowInstanceService](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.WorkflowServices.WorkflowServicesManager.GetWorkflowInstanceService.aspx) , чтобы получить экземпляр службы экземпляров рабочих процессов. Затем запустите рабочий процесс, вызвав один из двух методов. Один запускает рабочие процессы на сайте, а другой  в элементе списка.</span><span class="sxs-lookup"><span data-stu-id="187b8-p143">Building from previous examples, use the  [GetWorkflowInstanceService](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.WorkflowServices.WorkflowServicesManager.GetWorkflowInstanceService.aspx) method to get an instance of the workflow instance service. Next, start the workflow by calling one of two methods. One starts workflows on a site, while the other starts a workflow on a list item.</span></span>
  
    
    

-  <span data-ttu-id="187b8-p144">[StartWorkflow](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.WorkflowServices.WorkflowInstanceService.StartWorkflow.aspx) . Запускает рабочий процесс на сайте SharePoint, заданном при создании исходного объекта [WorkflowServicesManager](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.WorkflowServices.WorkflowServicesManager.aspx) . При использовании этого метода необходимо передать сопоставление рабочего процесса и все дополнительные свойства, присутствующие в форме запуска.</span><span class="sxs-lookup"><span data-stu-id="187b8-p144">[StartWorkflow](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.WorkflowServices.WorkflowInstanceService.StartWorkflow.aspx) . Starts a workflow on the SharePoint site that was set when creating the original [WorkflowServicesManager](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.WorkflowServices.WorkflowServicesManager.aspx) object. When using this method, you must pass in the workflow association and any additional startup properties present on the initiation form.</span></span>
    
  
-  <span data-ttu-id="187b8-p145">[StartWorkflowOnListItem](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.WorkflowServices.WorkflowInstanceService.StartWorkflowOnListItem.aspx) . Запускает рабочий процесс для определенного элемента списка. При использовании этого метода необходимо передать идентификатор нужного элемента списка помимо значений других параметров, необходимых методу **StartWorkflow**.</span><span class="sxs-lookup"><span data-stu-id="187b8-p145">[StartWorkflowOnListItem](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.WorkflowServices.WorkflowInstanceService.StartWorkflowOnListItem.aspx) . Starts a workflow on a specific list item. Using this method requires you to pass in the ID of the desired list item, in addition to other parameter values required by the **StartWorkflow** method.</span></span>
    
  
<span data-ttu-id="187b8-289">Следующий пример кода демонстрирует, как запустить экземпляр рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="187b8-289">The following code example demonstrates how to start a workflow instance.</span></span>
  
    
    



```

// connect to the deployment service
var workflowDeploymentService = workflowServicesManager.GetWorkflowDeploymentService();

// get all installed workflows
var publishedWorkflowDefinitions = workflowDeploymentService.EnumerateDefinitions(true);
clientContext.Load(publishedWorkflowDefinitions);
clientContext.ExecuteQuery();

// find the first workflow definition
var firstWorkflowDefinition = publishedWorkflowDefinitions.First();

// connect to the subscription service
var workflowSubscriptionService = workflowServicesManager.GetWorkflowSubscriptionService();

// get all workflow associations
var workflowAssociations = workflowSubscriptionService.EnumerateSubscriptionsByDefinition(firstWorkflowDefinition.Id);
clientContext.Load(workflowAssociations);
clientContext.ExecuteQuery();

// find the first association
var firstWorkflowAssociation = workflowAssociations.First();

// connect to the instance service
var workflowInstanceService = workflowServicesManager.GetWorkflowInstanceService();

// start the workflow
var startParameters = new Dictionary<string, object>();
workflowInstanceService.StartWorkflowOnListItem(firstWorkflowAssociation, listItemId, startParameters);
clientContext.ExecuteQuery();

```


### <a name="publishing-messages-and-events-to-running-workflows"></a><span data-ttu-id="187b8-290">Публикация сообщений и событий в запущенных рабочих процессах</span><span class="sxs-lookup"><span data-stu-id="187b8-290">Publishing messages and events to running workflows</span></span>

<span data-ttu-id="187b8-p146">Еще одна полезная функция, добавленная в SharePoint,  возможность публиковать пользовательские события в запущенных экземплярах рабочих процессов. Эти рабочие процессы могут включать действие **WaitForCustomEvent**, которое ожидает публикации определенного события в рабочем процессе. Событие также может содержать строку в виде части сообщения, которую действие может сохранить как переменную.</span><span class="sxs-lookup"><span data-stu-id="187b8-p146">Another powerful feature that was added in SharePoint is the ability to publish custom events to running workflow instances. These workflows can have an activity, **WaitForCustomEvent**, which listens for a specific event to be published to the workflow. The event can also contain a string as part of the message, which the activity can store as a variable.</span></span>
  
    
    
<span data-ttu-id="187b8-p147">Чтобы опубликовать событие из клиента с помощью CSOM службы рабочих процессов, сначала необходимо сослаться на определенный экземпляр рабочего процесса, в котором нужно опубликовать событие. Затем опубликуйте событие с помощью службы экземпляров, используя метод  [PublishCustomEvent](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.WorkflowServices.WorkflowInstanceService.PublishCustomEvent.aspx) . При использовании этого метода необходимо передать нужный экземпляр, имя события и, при необходимости, полезную нагрузку, как показано в следующем примере кода.</span><span class="sxs-lookup"><span data-stu-id="187b8-p147">To publish an event from the client using the Workflow Service CSOM, first get a reference to the specific workflow instance that the event should be published to. Then, using the instance service, publish the event using the  [PublishCustomEvent](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.WorkflowServices.WorkflowInstanceService.PublishCustomEvent.aspx) method. When using this method, you must pass in the desired instance, event name, and an optional payload, as shown in the following code example.</span></span>
  
    
    



```

// connect to the instance service
var workflowInstanceService = workflowServicesManager.GetWorkflowInstanceService();

// get all instances
var workflowInstances = workflowInstanceService.EnumerateInstancesForListItem(listId, listItemId);

var targetInstance = workflowInstances.First();

// publish custom event
instanceService.PublishCustomEvent(targetInstance, "AdHocMaintenanceRequest", "Flat Tire");
clientContext.ExecuteQuery();
```

<span data-ttu-id="187b8-p148">Чтобы получить сообщение в рабочем процессе, добавьте действие **WaitForCustomEvent**, а затем в окне **Свойства** задайте в свойстве **EventName** имя события, которое ожидает действие (в приведенном выше примере это строка "AdHocMaintenanceRequest"). Затем задайте для свойства **Result** значение переменной, в которой хранится полезная нагрузка события, как показано на рисунке 2.</span><span class="sxs-lookup"><span data-stu-id="187b8-p148">To receive the message in the workflow, add a **WaitForCustomEvent** activity and, using the **Properties** window, set the **EventName** property to the name of the event the activity is listening for (in the example above, this would be the string, "AdHocMaintenanceRequest"). Then, set the **Result** property to the variable in which the event's payload is stored, as shown in Figure 2.</span></span>
  
    
    

<span data-ttu-id="187b8-299">**Рисунок 2. Входной параметр EventName и значение Result**</span><span class="sxs-lookup"><span data-stu-id="187b8-299">**Figure 2. Input EventName and output Result**</span></span>

  
    
    

  
    
    
![Рис. 2. Ввод EventName и вывод результата](../images/ngSP2013WorkflowCSOM02.png)
  
    
    
<span data-ttu-id="187b8-302">Эта техника публикации пользовательского события демонстрируется в примере кода MSDN "SharePoint: маршрутизация рабочих процессов к состояниям в зависимости от действий и событий".</span><span class="sxs-lookup"><span data-stu-id="187b8-302">This technique of publishing a custom event is demonstrated in the MSDN Code Sample: SharePoint: Route Workflows to States Depending on Actions and Events.</span></span>
  
    
    

## <a name="conclusion"></a><span data-ttu-id="187b8-303">Заключение</span><span class="sxs-lookup"><span data-stu-id="187b8-303">Conclusion</span></span>

<span data-ttu-id="187b8-p150">Корпорация Майкрософт добавила рабочие процессы на платформу SharePoint 2007, а платформа рабочих процессов практически не изменилась в SharePoint 2010. Это относится и к пользовательским формам в рабочих процессах SharePoint. В SharePoint, с другой стороны, произошло много изменений платформы и архитектуры рабочих процессов.</span><span class="sxs-lookup"><span data-stu-id="187b8-p150">Microsoft introduced workflows into the SharePoint 2007 platform, and the workflow platform remained largely unchanged in SharePoint 2010. This was also true when it came to Custom Forms in SharePoint workflows. SharePoint, on the other hand, introduced many changes to workflow platform and architecture.</span></span>
  
    
    
<span data-ttu-id="187b8-p151">Одно из основных улучшений рабочих процессов в SharePoint  расширение CSOM с добавлением полноценного API служб рабочих процессов. Это позволяет разработчикам взаимодействовать с определениями, сопоставлениями и подписками рабочих процессов, а также создавать экземпляры этих рабочих процессов и работать с ними.</span><span class="sxs-lookup"><span data-stu-id="187b8-p151">One of the major improvements to workflows in SharePoint is the expansion of CSOM to include a complete Workflow Services API. This addition enables developers to interact with workflow definitions, associations, and subscriptions, and to create and interact with instances of these workflows.</span></span>
  
    
    

## <a name="see-also"></a><span data-ttu-id="187b8-309">См. также</span><span class="sxs-lookup"><span data-stu-id="187b8-309">See also</span></span>
<span data-ttu-id="187b8-310"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="187b8-310"><a name="bk_addresources"> </a></span></span>


-  <span data-ttu-id="187b8-311">
  [Рабочие процессы в SharePoint](http://msdn.microsoft.com/en-us/library/jj163986.aspx)</span><span class="sxs-lookup"><span data-stu-id="187b8-311">[Workflows in SharePoint](http://msdn.microsoft.com/en-us/library/jj163986.aspx)</span></span>
    
  
-  <span data-ttu-id="187b8-312">
  [Что такое Workflow Manager 1.0?](http://msdn.microsoft.com/en-us/library/windowsazure/jj193471%28v=azure.10%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="187b8-312">[What is Workflow Manager 1.0?](http://msdn.microsoft.com/en-us/library/windowsazure/jj193471%28v=azure.10%29.aspx)</span></span>
    
  

