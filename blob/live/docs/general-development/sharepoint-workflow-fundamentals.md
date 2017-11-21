---
title: "Основные сведения о рабочих процессах SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 1e622296-f78b-4e3a-a1e7-8effa24111a8
ms.openlocfilehash: c7b06524d61e25ef28919a0ef5c3ada814afa523
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="sharepoint-workflow-fundamentals"></a><span data-ttu-id="0231e-102">Основные сведения о рабочих процессах SharePoint</span><span class="sxs-lookup"><span data-stu-id="0231e-102">SharePoint workflow fundamentals</span></span>
<span data-ttu-id="0231e-103">В этой статье представлен высокоуровневый обзор инфраструктуры рабочих процессов в SharePoint, в том числе описание архитектуры платформы и мост взаимодействия рабочих процессов.</span><span class="sxs-lookup"><span data-stu-id="0231e-103">Provides a high-level overview of the workflow infrastructure in SharePoint, including a view of the platform architecture and the workflow interop bridge.</span></span>
## <a name="overview-of-workflows-in-sharepoint"></a><span data-ttu-id="0231e-104">Обзор рабочих процессов в SharePoint</span><span class="sxs-lookup"><span data-stu-id="0231e-104">Overview of workflows in SharePoint</span></span>
<span data-ttu-id="0231e-105"><a name="bkm_overview"> </a></span><span class="sxs-lookup"><span data-stu-id="0231e-105"></span></span>

<span data-ttu-id="0231e-p101">Рабочие процессы SharePoint основаны на платформе Windows Workflow Foundation 4, которая была существенно переработана по сравнению с предыдущими версиями. Платформа Windows Workflow Foundation (WF), в свою очередь, основана на функциях обмена сообщениями  [Windows Communication Foundation (WCF)](http://msdn.microsoft.com/ru-RU/library/vstudio/ms735119%28v=vs.90%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="0231e-p101">SharePoint workflows are powered by Windows Workflow Foundation 4, which was substantially redesigned from earlier versions. Windows Workflow Foundation (WF), in turn, is built on the messaging functionality that is provided by  [Windows Communication Foundation (WCF)](http://msdn.microsoft.com/ru-RU/library/vstudio/ms735119%28v=vs.90%29.aspx).</span></span>
  
    
    
<span data-ttu-id="0231e-p102">По сути, модель рабочие процессы моделируют структурированные бизнес-процессы. Поэтому рабочие процессы Windows Workflow Foundation 4  это структурированная коллекция "действий" рабочего процесса, каждое из которых представляет функциональный компонент бизнес-процесса.</span><span class="sxs-lookup"><span data-stu-id="0231e-p102">Conceptually, workflows model structured business processes. Therefore, Windows Workflow Foundation 4 workflows are a structured collection of workflow "activities," each of which represents a functional component of a business process.</span></span>
  
    
    
<span data-ttu-id="0231e-p103">Платформа рабочих процессов в SharePoint использует модель действий Windows Workflow Foundation 4 для представления бизнес-процессов на основе SharePoint. Кроме того, в SharePoint реализована высокоуровневая модель "шлюз-стадия", на основе которой создаются рабочие процессы.</span><span class="sxs-lookup"><span data-stu-id="0231e-p103">The workflow platform in SharePoint uses the Windows Workflow Foundation 4 activity model to represent a SharePoint-based business process. Additionally, SharePoint introduces a higher-level stage-gate model on which to create workflows.</span></span>
  
    
    
<span data-ttu-id="0231e-p104">Важно отметить связь между действиями рабочего процесса идействиями SharePoint. Действия рабочего процесса представляют базовые управляемые объекты, методы которых определяют поведение рабочего процесса. С другой стороны, действия рабочего процесса  это оболочка, инкапсулирующая базовые действия и представляющая их в понятное SharePoint Designer форме. Создатели рабочих процессов взаимодействуют с действиями рабочего процесса, в то время как модуль выполнения рабочих процессов работает на основе соответствующих действий.</span><span class="sxs-lookup"><span data-stu-id="0231e-p104">It is important to note the relationship between workflow activities and SharePointactions. Workflow activities represent the underlying managed objects whose methods drive workflow behaviors. Workflow actions, on the other hand, are wrappers that encapsulate the underlying activities and present them in a user-friendly form in SharePoint Designer. Workflow authors interact with the workflow actions, whereas the workflow execution engine acts on the corresponding activities.</span></span>
  
    
    
<span data-ttu-id="0231e-116">Действия, т. е. реализация классов действий, декларативно реализуются с помощью XAML.</span><span class="sxs-lookup"><span data-stu-id="0231e-116">The activities, which are implementations of activity classes, are implemented declaratively by using XAML.</span></span>
  
    
    
<span data-ttu-id="0231e-p105">Действия рабочих процессов вызываются с помощью слабосвязанных веб-служб, использующих API-интерфейсы для взаимодействия с SharePoint. Эти API-интерфейсы основаны на функциях обмена сообщениями  [Windows Communication Foundation (WCF)](http://msdn.microsoft.com/ru-RU/library/vstudio/ms735119%28v=vs.90%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="0231e-p105">Workflow activities are invoked using loosely coupled web services that use messaging APIs to communicate with SharePoint. These APIs are built on the messaging functionality that is provided by  [Windows Communication Foundation (WCF)](http://msdn.microsoft.com/ru-RU/library/vstudio/ms735119%28v=vs.90%29.aspx).</span></span>
  
    
    
<span data-ttu-id="0231e-p106">Инфраструктура обмена сообщениями очень гибкая и поддерживает практически любой шаблон обмена сообщениями, который вам может понадобиться. Обратите внимание, что в ферме SharePointWindows Workflow Foundation и WCF размещены в Workflow Manager Client 1.0.</span><span class="sxs-lookup"><span data-stu-id="0231e-p106">The messaging framework is very flexible and supports virtually any messaging pattern that you need. Note that on a SharePoint farm, Windows Workflow Foundation and WCF are hosted in Workflow Manager Client 1.0.</span></span>
  
    
    
<span data-ttu-id="0231e-121">Workflow Manager Client 1.0, SharePoint и SharePoint Designer 2013 предоставляют важные компоненты новой инфраструктуры:</span><span class="sxs-lookup"><span data-stu-id="0231e-121">Workflow Manager Client 1.0, SharePoint, and SharePoint Designer 2013 each provide significant parts of the new infrastructure:</span></span>
  
    
    

- <span data-ttu-id="0231e-p107">**Workflow Manager Client 1.0** обеспечивает управление определениями рабочих процессов. В нем также размещаются процессы выполнения экземпляров рабочих процессов.</span><span class="sxs-lookup"><span data-stu-id="0231e-p107">**Workflow Manager Client 1.0** provides the management of workflow definitions. It also hosts the execution processes for workflow instances.</span></span>
    
  
- <span data-ttu-id="0231e-p108">**SharePoint** предоставляет платформу для рабочих процессов SharePoint, которые моделируют бизнес-процессы на основе SharePoint, связанные с документами, списками, пользователями и задачами SharePoint. Кроме того, рабочие процессы, сопоставления, действия и другие метаданные рабочих процессов SharePoint хранятся и контролируются в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="0231e-p108">**SharePoint** provides the framework for SharePoint workflows, which model SharePoint-based business processes that involve SharePoint documents, lists, users, and tasks. Additionally, SharePoint workflows, associations, activities, and other workflow metadata are stored and managed in SharePoint.</span></span>
    
  
- <span data-ttu-id="0231e-p109">**SharePoint Designer 2013**  это основное средство, с помощью которых бизнес-пользователей создают определения рабочего процесса и публикуют их, как и в предыдущих версиях. Оно также используется для упаковки определения рабочего процесса со связанными компонентами SharePoint или без них.</span><span class="sxs-lookup"><span data-stu-id="0231e-p109">**SharePoint Designer 2013** is the primary business-user tool for creating workflow definitions and publishing them, as it was in previous versions. It can also be used to package a workflow definition with or without associated SharePoint components.</span></span>
    
  

## <a name="platform-architecture"></a><span data-ttu-id="0231e-128">Архитектура платформы</span><span class="sxs-lookup"><span data-stu-id="0231e-128">Platform architecture</span></span>
<span data-ttu-id="0231e-129"><a name="bkm_Architecture"> </a></span><span class="sxs-lookup"><span data-stu-id="0231e-129"></span></span>

<span data-ttu-id="0231e-p110">На рис. 1 показано высокоуровневое представление платформы рабочих процессов SharePoint. Во-первых, обратите внимание на то, что в новой инфраструктуре рабочих процессов Workflow Manager Client 1.0 используется в качестве узла выполнения рабочих процессов. В предыдущих же версиях узел выполнения рабочих процессов размещался в самом SharePoint, но это изменилось в SharePoint. Workflow Manager Client 1.0  это внешний компонент, который взаимодействует с SharePoint с помощью общих протоколов через шину обслуживания Microsoft Azure посредством OAuth. Кроме того, SharePoint содержит компоненты, которые можно было ожидать: элементы контента, события, приложения и т. д. Но обратите внимание, что также существует реализация узла выполнения рабочих процессов в SharePoint 2010 (т. е. модуль Windows Workflow Foundation 3) для обеспечения обратной совместимости. Подробнее об этом написано в статье  [Использование средств взаимодействия рабочих процессов для SharePoint](use-workflow-interop-for-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="0231e-p110">Figure 1 depicts a high-level view of the SharePoint workflow framework. Notice, first, how the new workflow infrastructure introduces Workflow Manager Client 1.0 as the new workflow execution host. Whereas in previous versions workflow execution was hosted in SharePoint itself, this has changed in SharePoint. Workflow Manager Client 1.0 is external to SharePoint and communicates using common protocols over the Microsoft Azure service bus, mediated by OAuth. Otherwise, SharePoint includes the feature that you would expect to see: content items, events, apps, and so on. But notice that there is also an implementation of the SharePoint 2010 workflow host (that is, the Windows Workflow Foundation 3 engine) for backward compatibility. You can read more about this in  [Use workflow interop for SharePoint](use-workflow-interop-for-sharepoint.md).</span></span>
  
    
    

<span data-ttu-id="0231e-137">**Рис. 1. Высокоуровневая архитектура инфраструктуры рабочих процессов**</span><span class="sxs-lookup"><span data-stu-id="0231e-137">**Figure 1. High-level architecture of the workflow infrastructure**</span></span>

  
    
    

  
    
    
![Высокоуровневая архитектура рабочего процесса](../images/wfArchitecture1.png)
  
    
    
<span data-ttu-id="0231e-p111">Workflow Manager Client 1.0 представлен в SharePoint в виде прокси приложения-службы Workflow Manager Client 1.0. Этот компонент позволяет SharePoint взаимодействовать с сервером Workflow Manager Client 1.0. Межсерверная проверка подлинности выполняется с помощью OAuth.</span><span class="sxs-lookup"><span data-stu-id="0231e-p111">Workflow Manager Client 1.0 is represented in SharePoint in the form of the Workflow Manager Client 1.0 Service Application Proxy. This component allows SharePoint to communicate and interact with the Workflow Manager Client 1.0 server. Server-to-server authentication is provided using OAuth.</span></span>
  
    
    
<span data-ttu-id="0231e-p112">События SharePoint, которые прослушивает рабочий процесс, например **itemCreated**, **itemUpdated** и т. д., направляются Workflow Manager Client 1.0 с помощью шины обслуживания Microsoft Azure. Для обратного вызова SharePoint платформа использует API REST SharePoint.</span><span class="sxs-lookup"><span data-stu-id="0231e-p112">SharePoint events for which a workflow is listening, like **itemCreated**, **itemUpdated**, and so on, are routed to Workflow Manager Client 1.0 using the Microsoft Azure service bus. For the return trip, the platform uses the SharePoint Representational State Transfer (REST) API to call back into SharePoint.</span></span>
  
    
    
<span data-ttu-id="0231e-p113">Существуют также дополнения к объектной модели рабочих процессов SharePoint, которые коллективно называются диспетчером служб рабочих процессов. Он позволяет управлять рабочими процессами и контролировать их выполнение. Основные зоны взаимодействия диспетчера служб  это развертывание, обмен сообщениями, управление экземплярами и взаимодействие с рабочими процессами SharePoint 2010 (для обеспечения обратной совместимости).</span><span class="sxs-lookup"><span data-stu-id="0231e-p113">There are also additions to the SharePoint workflow object model, called collectively the Workflow Services Manager, which allow you to manage and control your workflows and their execution. The primary zones of interaction for the services manager are deployment, messaging, instance control, and (for backward compatibility) interoperability with SharePoint 2010 workflows.</span></span>
  
    
    
<span data-ttu-id="0231e-p114">Наконец, существует компонент создания рабочих процессов. Теперь SharePoint Designer может создать и развертывать рабочие процессы SharePoint 2010 и SharePoint. Visual Studio 2012 не только предоставляет поверхность разработки для создания декларативных рабочих процессов, но и позволяет создавать Надстройки SharePoint и решения, которые полностью интегрируются с Workflow Manager Client 1.0.</span><span class="sxs-lookup"><span data-stu-id="0231e-p114">Finally, there is the workflow authoring component. SharePoint Designer can now create and deploy both SharePoint 2010 and SharePoint workflows. Visual Studio 2012 not only provides a designer surface for creating declarative workflows, but it can also create SharePoint Add-ins and solutions that fully integrate Workflow Manager Client 1.0 functionality.</span></span>
  
    
    

## <a name="workflow-subscriptions-and-associations"></a><span data-ttu-id="0231e-149">Подписки и сопоставления рабочих процессов</span><span class="sxs-lookup"><span data-stu-id="0231e-149">Workflow subscriptions and associations</span></span>
<span data-ttu-id="0231e-150"><a name="bkm_Subscriptions"> </a></span><span class="sxs-lookup"><span data-stu-id="0231e-150"></span></span>

<span data-ttu-id="0231e-p115">Поскольку наиболее значительное изменение рабочих процессов SharePoint  это перемещение обработки рабочих процессов на внешние узлы, такие как Microsoft Azure, было крайне важно связать сообщения и события SharePoint с инфраструктурой рабочих процессов в Microsoft Azure. Кроме того, в Microsoft Azure было необходимо связать инфраструктуру с данными клиента. Сопоставления рабочих процессов (основанные на концепции подписок WF)  это компоненты инфраструктуры SharePoint, которые поддерживают эти требования.</span><span class="sxs-lookup"><span data-stu-id="0231e-p115">Because the most significant change to SharePoint workflows is the moving of workflow processing onto external workflow hosts like Microsoft Azure, it was essential for SharePoint messages and events to connect to the workflow infrastructure in Microsoft Azure. In addition, it was necessary for Microsoft Azure to connect the infrastructure to customer data. Workflow associations (which are built on the WF concept of subscriptions) are the SharePoint infrastructure pieces that support these requirements.</span></span>
  
    
    

### <a name="microsoft-azure-publicationsubscribe-service"></a><span data-ttu-id="0231e-154">Служба публикации и подписки Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="0231e-154">Microsoft Azure publication/subscribe service</span></span>

<span data-ttu-id="0231e-p116">Перед обсуждением сопоставлений и подписок рабочих процессов необходимо изучить службу публикации и подписки Microsoft Azure, которую иногда называютpub/sub (PubSub). PubSub  это асинхронная платформа обмена сообщениями. Отправители сообщений (издатели) не передают сообщения напрямую получателям (подписчикам). Вместо этого сообщения обрабатываются издателями как классы без каких-либо сведениях о подписчиках. Затем подписчики определяют интересующие их сообщения, независимо от издателя, основываясь на созданных подписках.</span><span class="sxs-lookup"><span data-stu-id="0231e-p116">Before you can discuss workflow associations and subscriptions, you must look at the Microsoft Azure publication/subscribe service, which is sometimes referred to as pub/sub, or simply PubSub. PubSub is an asynchronous messaging framework. Message senders (publishers) do not send messages directly to message receivers (subscribers). Instead, messages are rendered by publishers as classes that have no knowledge of the message subscribers. Subscribers, then, consume published messages by identifying messages of interest, regardless of the publisher, based on subscriptions that they have created.</span></span>
  
    
    
<span data-ttu-id="0231e-p117">Подобное отделение создания сообщения от потребления сообщения обеспечивает масштабируемость и гибкость, а также позволяет отправлять многоадресные сообщения со стороны издателя и потреблять произвольные сообщения со стороны подписчика.</span><span class="sxs-lookup"><span data-stu-id="0231e-p117">This decoupling of message creation from message consumption allows for scalability and flexibility. It enables multicast messaging on the publisher side, and for promiscuous message consumption on the subscriber side.</span></span>
  
    
    

> <span data-ttu-id="0231e-162">**Примечание.** PubSub — это компонент служебной шины Microsoft Azure, который обеспечивает возможности подключения для WCF и других конечных точек службы.</span><span class="sxs-lookup"><span data-stu-id="0231e-162">**Note:** The PubSub feature is a part of the Microsoft Azure Service Bus, which provides connectivity options for WCF and other service endpoints.</span></span> <span data-ttu-id="0231e-163">К ним относятся конечные точки REST, которые могут быть расположены за границами преобразования сетевых адресов (NAT) или могут быть привязаны к часто изменяющимся, динамически назначаемым IP-адресам (или и то, и другое).</span><span class="sxs-lookup"><span data-stu-id="0231e-163">Note The PubSub feature is a part of the Microsoft Azure Service Bus, which provides connectivity options for WCF and other service endpoints. These include REST endpoints, which can be located behind network address translation (NAT) boundaries, or bound to frequently changing, dynamically assigned IP addresses, or both. For more information about the Azure Service Bus, see  Service Bus.</span></span> <span data-ttu-id="0231e-164">Дополнительные сведения о служебной шине Azure см. в разделе [Служебная шина](http://msdn.microsoft.com/ru-RU/library/ee732537.aspx).</span><span class="sxs-lookup"><span data-stu-id="0231e-164">For more information about the Microsoft Azure Service Bus, see  [Managing Service Bus Service Namespaces](http://msdn.microsoft.com/ru-RU/library/ee732537.aspx).</span></span> 
  
    
    


### <a name="workflow-associations-and-association-scope"></a><span data-ttu-id="0231e-165">Сопоставления рабочих процессов и область сопоставлений</span><span class="sxs-lookup"><span data-stu-id="0231e-165">Workflow associations and association scope</span></span>

<span data-ttu-id="0231e-p119">Сопоставления рабочих процессов связывают определения рабочих процессов с областью SharePoint и определенными значениями по умолчанию. Сопоставления сами по себе  это набор правил подписки, которые хранятся в службе публикации и подписки Azure, которые обрабатывают входящие сообщения для их передачи соответствующим (т. е. подписанным) экземплярам рабочих процессов.</span><span class="sxs-lookup"><span data-stu-id="0231e-p119">Workflow associations bind workflow definitions to specific SharePoint scope, with specific default values. The associations themselves represent a set of subscription rules that are stored in the Azure publication/subscription service that process incoming messages to ensure that they are consumed by appropriate (that is, subscribed) workflow instances.</span></span>
  
    
    
<span data-ttu-id="0231e-168">По умолчанию инфраструктуры обмена сообщениями поддерживает рабочие процессы в следующих областях:</span><span class="sxs-lookup"><span data-stu-id="0231e-168">By default, the messaging infrastructure supports workflows at the following scopes:</span></span>
  
    
    

-  <span data-ttu-id="0231e-169">[SPList](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPList.aspx) (для рабочих процессов списка);</span><span class="sxs-lookup"><span data-stu-id="0231e-169">[SPList](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPList.aspx) (for list workflows)</span></span>
    
  
-  <span data-ttu-id="0231e-170">[SPWeb](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPWeb.aspx) (для рабочих процессов сайта).</span><span class="sxs-lookup"><span data-stu-id="0231e-170">[SPWeb](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPWeb.aspx) (for site workflows)</span></span>
    
  
<span data-ttu-id="0231e-p120">В отличие от предыдущих версий SharePoint не поддерживает рабочие процессы, относящиеся к типу контента ( [SPContentType](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPContentType.aspx) ). Тем не менее, инфраструктура обмена сообщениями расширяема, поэтому она может поддерживать произвольные области. Разработчик может задать в свойстве [EventSourceId](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowSubscription.EventSourceId.aspx) экземпляра [WorkflowSubscription](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowSubscription.aspx) любой идентификатор **guid**. Затем можно использовать значение **EventSourceId** для вызова метода **PublishEvent(Guid, String, IDictionary<String, Object>)**, который запускает новый экземпляр рабочего процесса для указанной подписки **WorkflowSubscription**.</span><span class="sxs-lookup"><span data-stu-id="0231e-p120">Unlike previous versions, SharePoint does not support workflows that are scoped to a content type ( [SPContentType](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPContentType.aspx) ). However, the messaging infrastructure is extensible, so it can support any arbitrary scope. As a developer, you can set the [EventSourceId](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowSubscription.EventSourceId.aspx) property on a given [WorkflowSubscription](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowSubscription.aspx) instance to any **guid**. You can then use that **EventSourceId** value to call **PublishEvent(Guid, String, IDictionary<String, Object>)**, which triggers a new workflow instance of the specified **WorkflowSubscription**.</span></span>
  
    
    

### <a name="workflow-service-in-microsoft-azure"></a><span data-ttu-id="0231e-175">Служба рабочих процессов в Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="0231e-175">Workflow service in Microsoft Azure</span></span>

<span data-ttu-id="0231e-p121">Сопоставления рабочих процессов SharePoint представляются службой рабочих процессов в Microsoft Azure. Если приложению требуется получить сопоставление рабочего процесса и его данные, сначала оно запрашивает все службы рабочих процессов, доступные в заданной области.</span><span class="sxs-lookup"><span data-stu-id="0231e-p121">Associations for SharePoint workflows are represented by their workflow service within Microsoft Azure. When an application has to acquire a workflow association and its data, it must first query for all of the workflow services that are available at a given scope.</span></span>
  
    
    
<span data-ttu-id="0231e-p122">Аналогичным образом экземпляры рабочих процессов содержат указатель на соответствующую службу рабочих процессов. С его помощью определяется правильное сопоставление.</span><span class="sxs-lookup"><span data-stu-id="0231e-p122">Similarly, workflow instances carry a pointer back to their respective workflow service. This is the means by which its correct association is determined.</span></span>
  
    
    

### <a name="starting-workflows"></a><span data-ttu-id="0231e-180">Запуск рабочих процессов</span><span class="sxs-lookup"><span data-stu-id="0231e-180">Starting workflows</span></span>

<span data-ttu-id="0231e-181">Рабочие процессы можно запустить вручную или автоматически.</span><span class="sxs-lookup"><span data-stu-id="0231e-181">Workflows can be started either manually or automatically.</span></span>
  
    
    
 <span data-ttu-id="0231e-182">**Ручные рабочие процессы**</span><span class="sxs-lookup"><span data-stu-id="0231e-182">**Manual workflows**</span></span>
  
    
    
<span data-ttu-id="0231e-p123">Ручные рабочие процессы запускаются, когда служба PubSub получает сообщение **StartWorkflow**. Оно содержит следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="0231e-p123">Manual workflows are started when the PubSub service receives a **StartWorkflow** message. The message contains the following descriptive information:</span></span>
  
    
    

- <span data-ttu-id="0231e-185">Идентификатор сопоставления (т. е. экземпляр **WorkflowSubscription**).</span><span class="sxs-lookup"><span data-stu-id="0231e-185">The association identifier (that is, the **WorkflowSubscription** instance).</span></span>
    
  
- <span data-ttu-id="0231e-p124">Идентификатор исходного контекста элемента. Он передается в параметре  _ItemId_ и свойстве **EventSource** при вызове метода **PublishEvent**.</span><span class="sxs-lookup"><span data-stu-id="0231e-p124">The ID of the originating item context. This is passed in with the  _ItemId_ parameter and the **EventSource** property on the **PublishEvent** method call.</span></span>
    
  
- <span data-ttu-id="0231e-188">Тип события для запуска вручную ( **WorkflowStart**).</span><span class="sxs-lookup"><span data-stu-id="0231e-188">The event type for a manual start ( **WorkflowStart**).</span></span>
    
  
- <span data-ttu-id="0231e-p125">Дополнительные параметры запуска рабочих процессов (из подписки или формы **Init**). Это может быть **CorrelationId** для подписки или **WFInstanceId** для формы **Init**.</span><span class="sxs-lookup"><span data-stu-id="0231e-p125">Additional workflow initiation parameters, either from the subscription or from the **Init** form, as appropriate. This would be **CorrelationId** for the subscription and **WFInstanceId** for the **Init** form.</span></span>
    
  
 <span data-ttu-id="0231e-191">**Рабочие процессы с автоматическим запуском**</span><span class="sxs-lookup"><span data-stu-id="0231e-191">**Auto-start workflows**</span></span>
  
    
    
<span data-ttu-id="0231e-p126">Рабочие процессы с автоматическим запуском инициируются с помощью сообщения **Add**, передаваемого службе PubSub. Оно содержит следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="0231e-p126">Auto-start workflows are initiated by using an **Add** message to the PubSub service. The message contains the following descriptive information:</span></span>
  
    
    

- <span data-ttu-id="0231e-194">Идентификатор исходного контекста элемента.</span><span class="sxs-lookup"><span data-stu-id="0231e-194">The ID of the originating item context.</span></span>
    
  
- <span data-ttu-id="0231e-195">Само событие  это обычное событие SharePoint **Add**.</span><span class="sxs-lookup"><span data-stu-id="0231e-195">The event itself is a normal SharePoint **Add** event.</span></span>
    
  
- <span data-ttu-id="0231e-196">Параметры инициации рабочих процессов.</span><span class="sxs-lookup"><span data-stu-id="0231e-196">The workflow initiation parameters.</span></span>
    
  

> <span data-ttu-id="0231e-197">**Примечание.** Если рабочий процесс запускается автоматически для повторяющегося события (например, **OnItemChanged**), он не может запустить другой рабочий процесс данного сопоставления до завершения выполнения существующего экземпляра рабочего процесса сопоставления.</span><span class="sxs-lookup"><span data-stu-id="0231e-197">**Note** If a workflow automatically starts on a repeatable event (for example, the **OnItemChanged** event), it cannot start another workflow of a given association until the existing running instance of the association's workflow has completed running.</span></span>
  
    
    


### <a name="workflow-subscriptions"></a><span data-ttu-id="0231e-198">Подписки рабочих процессов</span><span class="sxs-lookup"><span data-stu-id="0231e-198">Workflow subscriptions</span></span>

<span data-ttu-id="0231e-p127">Естественным дополнением сопоставлений служат подписки, которые позволяют рабочему процессу взаимодействовать с сопоставлениями. Рабочий процесс должен создать подписки в шине обслуживания Azure с помощью методов **create** и **delete**.</span><span class="sxs-lookup"><span data-stu-id="0231e-p127">The natural complement to associations are subscriptions, which allow the workflow to interact with associations. The workflow must create subscriptions on the Azure Service Bus using **create** methods and **delete** methods.</span></span>
  
    
    
<span data-ttu-id="0231e-201">Сигнатуры методов, которые создают подписки и экземпляр рабочего процесса, определяют обязательные и необязательные параметры.</span><span class="sxs-lookup"><span data-stu-id="0231e-201">The signatures of the methods that create the subscription and instantiate the workflow specify the parameters???both optional and required.</span></span> <span data-ttu-id="0231e-202">Списки параметров указывает автор рабочего процесса, поэтому они могут отличаться для разных определений рабочих процессов.</span><span class="sxs-lookup"><span data-stu-id="0231e-202">The list of parameters is determined by the workflow author, so they may differ from one workflow definition to another.</span></span> <span data-ttu-id="0231e-203">Список параметров подписки указывается в виде метаданных в определениях рабочих процессов.</span><span class="sxs-lookup"><span data-stu-id="0231e-203">The list of subscription parameters is specified as metadata of the workflow definitions.</span></span> <span data-ttu-id="0231e-204">Параметры подписки предоставляются при ее создании.</span><span class="sxs-lookup"><span data-stu-id="0231e-204">The subscription parameters are provided when the subscription is created.</span></span> <span data-ttu-id="0231e-205">Список параметров инициализации указывается в XAML как часть определения рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="0231e-205">The list of initialization parameters is specified in XAML as part of the workflow definition.</span></span> <span data-ttu-id="0231e-206">Параметры инициализации предоставляются при создании экземпляра рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="0231e-206">The initialization parameters are provided when the workflow is instantiated.</span></span>
  
    
    
<span data-ttu-id="0231e-207">Подписки привязаны к определенному объекту SharePoint (экземпляру **SPList** или экземпляру **SPWeb**).</span><span class="sxs-lookup"><span data-stu-id="0231e-207">Subscriptions are bound to a specific SharePoint object???either an **SPList** instance or an **SPWeb** instance.</span></span> <span data-ttu-id="0231e-208">Тип объекта подписки передается как значение обязательного параметра при создании подписки.</span><span class="sxs-lookup"><span data-stu-id="0231e-208">The subscription object type is passed in as a value of a required parameter when the subscription is created.</span></span> <span data-ttu-id="0231e-209">Тип объекта определяет область подписки, чтобы последняя реагировала только на события, происходящие в объекте, на который есть подписка.</span><span class="sxs-lookup"><span data-stu-id="0231e-209">Subscriptions are bound to a specific SharePoint object—either an SPList instance or an SPWeb instance. The subscription object type is passed in as a value of a required parameter when the subscription is created. The object type defines the subscription scope so that a subscription can only respond to events that occur on the object to which they are subscribed.</span></span>
  
    
    

## <a name="sharepoint-workflow-interop"></a><span data-ttu-id="0231e-210">Взаимодействие рабочих процессов SharePoint</span><span class="sxs-lookup"><span data-stu-id="0231e-210">SharePoint workflow interop</span></span>
<span data-ttu-id="0231e-211"><a name="bkm_InteropBridge"> </a></span><span class="sxs-lookup"><span data-stu-id="0231e-211"></span></span>

<span data-ttu-id="0231e-p130">Взаимодействие рабочих процессов SharePoint позволяет вызывать рабочие процессы SharePoint 2010 (основанные на Windows Workflow Foundation 3) из рабочих процессов SharePoint, которые основаны на Windows Workflow Foundation 4. Это позволяет выполнять рабочие процессы SharePoint 2010 из рабочих процессов SharePoint.</span><span class="sxs-lookup"><span data-stu-id="0231e-p130">SharePoint workflow interop enables SharePoint 2010 workflows (which are built on Windows Workflow Foundation 3) to be called from SharePoint workflows, which are based on Windows Workflow Foundation 4. This allows you to execute 2010 workflows from within 2013 workflows.</span></span>
  
    
    
<span data-ttu-id="0231e-p131">Это важно, так как у вас может быть среда SharePoint 2010, которую вы можете использовать повторно вместе с рабочими процессами SharePoint. Кроме того, вы можете использовать действия или функции SharePoint 2010, который еще не реализованы в SharePoint</span><span class="sxs-lookup"><span data-stu-id="0231e-p131">This is important because you may have SharePoint 2010 that you may use to reuse in conjunction with your SharePoint workflows. Additionally, you may wish to use activities or features from SharePoint 2010, which are not yet implemented in SharePoint</span></span>
  
    
    
<span data-ttu-id="0231e-216">Полное обсуждение взаимодействия рабочих процессов SharePoint см. в разделе  [Использование средств взаимодействия рабочих процессов для SharePoint](use-workflow-interop-for-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="0231e-216">For a full discussion of SharePoint workflow interop, see  [Use workflow interop for SharePoint](use-workflow-interop-for-sharepoint.md).</span></span>
  
    
    

## <a name="additional-resources"></a><span data-ttu-id="0231e-217">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="0231e-217">Additional resources</span></span>
<span data-ttu-id="0231e-218"><a name="bk_additional"> </a></span><span class="sxs-lookup"><span data-stu-id="0231e-218"></span></span>


-  [<span data-ttu-id="0231e-219">Общие сведения о рабочих процессах в SharePoint</span><span class="sxs-lookup"><span data-stu-id="0231e-219">Get started with workflows in SharePoint</span></span>](get-started-with-workflows-in-sharepoint.md)
    
  
-  [<span data-ttu-id="0231e-220">Справочник по действий рабочих процессов для SharePoint</span><span class="sxs-lookup"><span data-stu-id="0231e-220">Workflow actions and activities reference for SharePoint</span></span>](workflow-actions-and-activities-reference-for-sharepoint.md)
    
  
-  [<span data-ttu-id="0231e-221">Разработка рабочих процессов в SharePoint с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0231e-221">Develop SharePoint workflows using Visual Studio</span></span>](develop-sharepoint-workflows-using-visual-studio.md)
    
  
-  [<span data-ttu-id="0231e-222">Разработка рабочих процессов в SharePoint Designer и Visio</span><span class="sxs-lookup"><span data-stu-id="0231e-222">Workflow development in SharePoint Designer and Visio</span></span>](workflow-development-in-sharepoint-designer-and-visio.md)
    
  
-  [<span data-ttu-id="0231e-223">Рабочие процессы в SharePoint</span><span class="sxs-lookup"><span data-stu-id="0231e-223">Workflows in SharePoint</span></span>](workflows-in-sharepoint.md)
    
  
-  [<span data-ttu-id="0231e-224">Использование средств взаимодействия рабочих процессов для SharePoint</span><span class="sxs-lookup"><span data-stu-id="0231e-224">Use workflow interop for SharePoint</span></span>](use-workflow-interop-for-sharepoint.md)
    
  

