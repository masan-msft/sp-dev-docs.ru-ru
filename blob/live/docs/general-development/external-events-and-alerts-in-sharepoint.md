---
title: "Внешние события и оповещения в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: e48e4812-a185-43c5-b243-04b1d79b88ee
ms.openlocfilehash: 3d5a845f0865ac51c1a02d561bb55049e305a808
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="external-events-and-alerts-in-sharepoint"></a><span data-ttu-id="860f2-102">Внешние события и оповещения в SharePoint</span><span class="sxs-lookup"><span data-stu-id="860f2-102">External events and alerts in SharePoint</span></span>
<span data-ttu-id="860f2-103">Узнайте концепции создания приемников удаленных событий в SharePoint, которые можно присоединить к внешним спискам и выполнить при обновлении внешних данных, представляемых списком.</span><span class="sxs-lookup"><span data-stu-id="860f2-103">Learn the concepts behind creating remote event receivers in SharePoint that can be attached to external lists and execute when the external data that the list represents is updated.</span></span>
## <a name="what-are-event-receivers"></a><span data-ttu-id="860f2-104">Что представляют собой приемники событий?</span><span class="sxs-lookup"><span data-stu-id="860f2-104">What are event receivers?</span></span>
<span data-ttu-id="860f2-105"><a name="Externalevents_overview"> </a></span><span class="sxs-lookup"><span data-stu-id="860f2-105"></span></span>

<span data-ttu-id="860f2-p101">Приемник событий  это управляемого кода, реагирующего на запуск событиями, например добавление, перемещение, удаление, возврат и извлечение SharePoint. При возникновении этих событий и условий приемника событий, выполняется код, написанный для предоставления дополнительных функциональных возможностей. При настройке объектов SharePoint, такие как списки, рабочие процессы и компоненты, Ожидание этих событий они называются узлов событий.</span><span class="sxs-lookup"><span data-stu-id="860f2-p101">An event receiver is a piece of managed code that responds to SharePoint triggering events such as adding, moving, deleting, checking in, and checking out. When these events occur, and the event receiver's criteria are met, the code that you write to provide additional functionality is executed. When SharePoint objects, such as lists, workflows and features, are configured to wait on these events to occur, they are called event hosts.</span></span> 
  
    
    
<span data-ttu-id="860f2-p102">Приемники событий позволяют выполнять бизнес-логики при возникновении определенных событий. По сути это обработчики, где можно создать код, чтобы обрабатывать некоторые условия, сделать уведомлений, обновление других систем и т.д. При создании приемников событий создается библиотеки DLL. Можно поместить эту Библиотеку в глобальном кэше сборок, чтобы приемников событий, вызываются в ответ на изменения в внешней системы.</span><span class="sxs-lookup"><span data-stu-id="860f2-p102">Event receivers let you perform business logic when a specific event occurs. Essentially, these are the hooks where you can create code to handle certain conditions, make notifications, update other systems, and so on. When you create event receivers, a DLL is generated. You can place that DLL into the global assembly cache, so that the event receivers are invoked in response to any changes in an external system.</span></span>
  
    
    
<span data-ttu-id="860f2-112">Следующий пример содержит приемник простой внешних событий в C#, который выполняется при добавлении нового элемента в список.</span><span class="sxs-lookup"><span data-stu-id="860f2-112">The following example contains a simple external event receiver in C# that executes when a new item is added to the list.</span></span>
  
    
    



```cs

public class EntryContentEventReceiver : SPItemEventReceiver
{
   public override void ItemAdded(SPItemEventProperties properties)
   {
      base.ItemAdded(properties);

      // properties.ExternalNotificationMessage holds the message sent by the external 
      // system.
   }
```

<span data-ttu-id="860f2-113">Приемники событий внешнего можно расширить также работать с приемника событий сущности, а также как удаленных приемников событий развернут как службы на месте или в Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="860f2-113">External event receivers can also be extended to work against an entity event receiver and as remote event receivers deployed as a service on-premise or in Microsoft Azure.</span></span> 
  
    
    

## <a name="what-are-remote-event-receivers"></a><span data-ttu-id="860f2-114">Что такое удаленные приемники событий?</span><span class="sxs-lookup"><span data-stu-id="860f2-114">What are remote event receivers?</span></span>
<span data-ttu-id="860f2-115"><a name="WhatIsARemoteEventReceiver"> </a></span><span class="sxs-lookup"><span data-stu-id="860f2-115"></span></span>

<span data-ttu-id="860f2-116">Удаленные приемники событий являются новыми для SharePoint.</span><span class="sxs-lookup"><span data-stu-id="860f2-116">Remote event receivers are new for SharePoint.</span></span> <span data-ttu-id="860f2-117">Традиционные решения SharePoint используйте приемника событий для обработки событий, таких как пользователи, создание и удаление списков и элементов списка.</span><span class="sxs-lookup"><span data-stu-id="860f2-117">In a traditional SharePoint solution, you use an event receiver to handle events such as users creating or deleting lists or items in lists.</span></span> <span data-ttu-id="860f2-118">В SharePoint надстройки, используйте удаленного приемника событий для обработки событий, аналогичные.</span><span class="sxs-lookup"><span data-stu-id="860f2-118">In an SharePoint Add-in, you use a remote event receiver to handle similar events.</span></span> <span data-ttu-id="860f2-119">Удаленные приемники событий действуют подобно приемников событий регулярных, за исключением того, что удаленные приемники событий обработки событий, происходящих при надстройки SharePoint на другой системе с его узла веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="860f2-119">Remote event receivers work similarly to regular event receivers, except that remote event receivers handle events that occur when an SharePoint Add-in is on a different system from its host web application.</span></span>
  
    
    
<span data-ttu-id="860f2-120">Службы Business Connectivity Services (BCS) использует удаленных приемников событий подключенного к внешних списков и entities можно написать код, который может реагировать на изменения в данные, размещаемые во внешней системе.</span><span class="sxs-lookup"><span data-stu-id="860f2-120">Business Connectivity Services (BCS) uses remote event receivers attached to external lists and entities to allow you to write code that can react to changes in data hosted in the external system.</span></span>
  
    
    
<span data-ttu-id="860f2-121">Чтобы решить эту проблему, были добавлены два стереотипов схеме модели BDC: **EventSubscriber** и **EventUnsubscriber**.</span><span class="sxs-lookup"><span data-stu-id="860f2-121">To accommodate this, two stereotypes have been added to the schema of the BDC model: **EventSubscriber** and **EventUnsubscriber**.</span></span>
  
    
    

> <span data-ttu-id="860f2-122">**Примечание:** Приемники событий не поддерживаются в изолированных решениях.</span><span class="sxs-lookup"><span data-stu-id="860f2-122">**Note:** Event receivers are not supported in sandboxed solutions.</span></span> 
  
    
    


## <a name="what-features-and-capabilities-does-the-new-external-event-receiver-infrastructure-provide"></a><span data-ttu-id="860f2-123">Какие функции и возможности нового инфраструктура приемника внешних событий предоставляет?</span><span class="sxs-lookup"><span data-stu-id="860f2-123">What features and capabilities does the new external event receiver infrastructure provide?</span></span>
<span data-ttu-id="860f2-124"><a name="FeaturesAddedWithRER"> </a></span><span class="sxs-lookup"><span data-stu-id="860f2-124"></span></span>

<span data-ttu-id="860f2-125">По использованию и расширению возможностей приемника событий SharePoint, BCS имеет возможность добавления предупреждения, приемники событий внешний список и приемники сущности для предоставления расширенных функциональных возможностей.</span><span class="sxs-lookup"><span data-stu-id="860f2-125">By using and extending the SharePoint event receiver features, BCS is able to add alerts, external list event receivers, and entity receivers to provide extended functionality.</span></span>
  
    
    

- <span data-ttu-id="860f2-126">**Оповещения:** Оповещения были неотъемлемой частью SharePoint для нескольких версий, но до того времени SharePoint, они не будет работать с внешними списками.</span><span class="sxs-lookup"><span data-stu-id="860f2-126">**Alerts:** Alerts have been an integral part of SharePoint for several versions, but until SharePoint, they would not work with external lists.</span></span> <span data-ttu-id="860f2-127">Теперь пользователь может создавать оповещения на внешний список, для которого отличается от оповещений для стандартного списка SharePoint.</span><span class="sxs-lookup"><span data-stu-id="860f2-127">Now a user can create alerts on an external list that have the same behavior as alerts on a standard SharePoint list.</span></span>
    
  
- <span data-ttu-id="860f2-p105">**Приемников событий внешнего списка:** Приемники событий теперь могут быть присоединены к внешним спискам так же, как они могут для Стандартные списки. Это обеспечивает механизм расширяемости, позволяющее создавать код, выполняемый на определенное время.</span><span class="sxs-lookup"><span data-stu-id="860f2-p105">**External list event receivers:** Event receivers can now be attached to external lists just like they can for standard lists. This provides an extensibility mechanism that lets you write code that is executed at specific times.</span></span>
    
  
- <span data-ttu-id="860f2-p106">**Приемников событий сущности:** Приемники событий сущности обеспечивают гибкость, позволяя создавать более надежный код, обеспечивающий других операций, например контекста пользователя, для фильтрации данных. Это позволяет лучше личной настройки и настройку безопасности.</span><span class="sxs-lookup"><span data-stu-id="860f2-p106">**Entity event receivers:** Entity event receivers provide flexibility by letting you write more robust code that allows other operations like providing user context for filtering data. This can allow better personalization and customized security.</span></span>
    
  
<span data-ttu-id="860f2-132">Несколько интересных сценариев делает удаленных событий в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="860f2-132">Remote eventing in SharePoint makes several interesting scenarios possible.</span></span> <span data-ttu-id="860f2-133">Например возможно, «Продажи отслеживание потенциальных клиентов» приложение, которое позволяет получать уведомления при вводе нового сбыту в приложение внешнего интереса продажах.</span><span class="sxs-lookup"><span data-stu-id="860f2-133">For example, you might have a "Sales Lead Tracking" application that lets a sales team be notified when new sales leads are entered into an external lead application.</span></span> <span data-ttu-id="860f2-134">При вводе нового ведущего сотрудника отдела продаж через систему уведомлений, который является частью приложения интереса уведомляется SharePoint.</span><span class="sxs-lookup"><span data-stu-id="860f2-134">When a new sales lead is entered, SharePoint is notified through the notification system that is part of the lead application.</span></span> <span data-ttu-id="860f2-135">SharePoint получает уведомления и затем создает новые задачи для указанного сотрудников отдела продаж к исполнению на каждый новый ведущий сотрудник.</span><span class="sxs-lookup"><span data-stu-id="860f2-135">SharePoint receives the notification and then creates new tasks for the specified salespeople to follow up on each new lead.</span></span> <span data-ttu-id="860f2-136">При настройке приложения запись ведущего сотрудника отдела продаж на внешнюю систему, чтобы отправить уведомление SharePoint при создании каждого нового интереса, SharePoint будет храниться полностью в актуальном состоянии.</span><span class="sxs-lookup"><span data-stu-id="860f2-136">By configuring the sales lead entry application on the external system to send a notification to SharePoint on the creation of each new lead, SharePoint is kept completely up to date.</span></span>
  
    
    

## <a name="prerequisites-for-using-event-receivers-for-external-lists"></a><span data-ttu-id="860f2-137">Необходимые условия для использования приемников событий для внешних списков</span><span class="sxs-lookup"><span data-stu-id="860f2-137">Prerequisites for using event receivers for external lists</span></span>
<span data-ttu-id="860f2-138"><a name="bkmk_Prerequisites"> </a></span><span class="sxs-lookup"><span data-stu-id="860f2-138"></span></span>

<span data-ttu-id="860f2-139">Чтобы использовать приемники событий для внешних списков, вам необходимо следующее:</span><span class="sxs-lookup"><span data-stu-id="860f2-139">To use event receivers for external lists, you need the following:</span></span>
  
    
    

- <span data-ttu-id="860f2-140">SharePoint</span><span class="sxs-lookup"><span data-stu-id="860f2-140">SharePoint</span></span>
    
  
- <span data-ttu-id="860f2-141">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="860f2-141">Visual Studio 2012</span></span>
    
  
<span data-ttu-id="860f2-142">Дополнительные сведения о настройке среды разработки SharePoint видеть [настроить среду разработки, общие для SharePoint](set-up-a-general-development-environment-for-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="860f2-142">For more information about setting up a SharePoint development environment, see  [Set up a general development environment for SharePoint](set-up-a-general-development-environment-for-sharepoint.md).</span></span>
  
    
    

## <a name="configure-the-external-system-to-notify-sharepoint-of-external-events"></a><span data-ttu-id="860f2-143">Настройка внешней системы для уведомления SharePoint внешние события</span><span class="sxs-lookup"><span data-stu-id="860f2-143">Configure the external system to notify SharePoint of external events</span></span>
<span data-ttu-id="860f2-144"><a name="Externalevents_components"> </a></span><span class="sxs-lookup"><span data-stu-id="860f2-144"></span></span>

<span data-ttu-id="860f2-145">Для внешних событий для работы число компонентов нужно установить и настроить на узел SharePoint и внешняя система.</span><span class="sxs-lookup"><span data-stu-id="860f2-145">For external events to work, a number of components have to be installed and configured on both the SharePoint host and the external system.</span></span>
  
    
    
<span data-ttu-id="860f2-146">Необходимо настроить для внешней системы, чтобы его можно сделать следующее:</span><span class="sxs-lookup"><span data-stu-id="860f2-146">You have to configure the external system so that it can do the following:</span></span>
  
    
    

- <span data-ttu-id="860f2-p108">**Определение при изменении базовых данных.** Для внешней системы, чтобы узнать, когда были внесены изменения необходимо создать механизм опроса для конкретных изменений. Это можно сделать с помощью запланированных служба, которая опрашивает источника данных через определенные интервалы времени.</span><span class="sxs-lookup"><span data-stu-id="860f2-p108">**Determine when underlying data changes.** For the external system to know when changes have been made, you have to create a mechanism for polling for specific changes. You can do this by using a timed service that polls the data source at specific intervals.</span></span>
    
  
- <span data-ttu-id="860f2-p109">**Получения и записи запросов для подписки на уведомления об изменениях.** Реализация хранилища подписок, чтобы его можно хранить получателей уведомлений об изменении имеет во внешней системе. Самое простое решение, вероятно,  это таблица базы данных. В таблице (или выберите любой механизм) должны записать SubscriptionID, адрес доставки, тип события и имя сущности.</span><span class="sxs-lookup"><span data-stu-id="860f2-p109">**Receive and record requests for subscriptions to change notifications.** The external system has to implement a subscription store so that it can store who should receive change notifications. The simplest solution is probably a database table. The table (or whatever mechanism you choose) should record SubscriptionID, Delivery Address, Event Type, and Entity Name.</span></span>
    
  
- <span data-ttu-id="860f2-p110">**Регистрации уведомлений конечным точкам представлений состояния (REST).** Чтобы позволить SharePoint подписчики знать, что было изменено, внешняя система приложению необходимо отправить HTTP WebRequest на адрес доставки, записанные в хранилища подписок. Этот адрес доставки  это RESTful конечной точки, создаваемая программой SharePoint во время процесса подписки.</span><span class="sxs-lookup"><span data-stu-id="860f2-p110">**Post notifications to Representational State Transfer (REST) endpoints.** To let SharePoint subscribers know that a change has occurred, the external system application needs to send an HTTP WebRequest to the delivery address recorded in the subscription store. This delivery address is a RESTful endpoint generated by SharePoint during the subscription process.</span></span>
    
  

## <a name="configure-sharepoint-to-allow-communication-with-external-systems"></a><span data-ttu-id="860f2-157">Настройка SharePoint, чтобы разрешить связь с внешними системами</span><span class="sxs-lookup"><span data-stu-id="860f2-157">Configure SharePoint to allow communication with external systems</span></span>
<span data-ttu-id="860f2-158"><a name="bkmk_configureSP"> </a></span><span class="sxs-lookup"><span data-stu-id="860f2-158"></span></span>

<span data-ttu-id="860f2-159">Чтобы разрешить связь с внешней системы, SharePoint должны быть настроены следующие:</span><span class="sxs-lookup"><span data-stu-id="860f2-159">To allow communication with the external system, SharePoint must be configured with the following:</span></span>
  
    
    

- <span data-ttu-id="860f2-160">Модели BDC с **EventSubscriber** и **EventUnsubscriber** стереотипов настроены</span><span class="sxs-lookup"><span data-stu-id="860f2-160">A BDC model with **EventSubscriber** and **EventUnsubscriber** stereotypes configured</span></span>
    
  
- <span data-ttu-id="860f2-161">Приемники событий</span><span class="sxs-lookup"><span data-stu-id="860f2-161">Event receivers</span></span>
    
  

### <a name="how-is-external-eventing-enabled"></a><span data-ttu-id="860f2-162">Как включить внешние события</span><span class="sxs-lookup"><span data-stu-id="860f2-162">How is external eventing enabled?</span></span>

<span data-ttu-id="860f2-163">Можно включить внешние события в SharePoint через **Параметры сайта** или, добавив следующий код пользовательского компонента в проект</span><span class="sxs-lookup"><span data-stu-id="860f2-163">You can enable external eventing in SharePoint through **Site Settings** or by adding the following custom feature id to your project</span></span>
  
    
    

```XML

<ActivationDependency FeatureTitle="BCSEvents" FeatureId="60c8481d-4b54-4853-ab9f-ed7e1c21d7e4" />
```

<span data-ttu-id="860f2-164">Включается событий для внешней системы, когда SharePoint создает адрес доставки и отправляет его к внешней системе во время процесса подписки на.</span><span class="sxs-lookup"><span data-stu-id="860f2-164">Eventing for an external system is enabled when SharePoint creates the delivery address and sends it to the external system during the Subscribe process.</span></span>
  
    
    

## <a name="overall-flow-of-external-eventing-between-sharepoint-and-external-systems"></a><span data-ttu-id="860f2-165">Общий поток внешние события между SharePoint и внешними системами</span><span class="sxs-lookup"><span data-stu-id="860f2-165">Overall flow of external eventing between SharePoint and external systems</span></span>
<span data-ttu-id="860f2-166"><a name="bkmk_overallflow"> </a></span><span class="sxs-lookup"><span data-stu-id="860f2-166"></span></span>

<span data-ttu-id="860f2-167">На рисунке 1, обратите внимание, что состоит из трех различных шагов при использовании приемников событий внешнего: подписка, уведомления и отменить подписку.</span><span class="sxs-lookup"><span data-stu-id="860f2-167">In Figure 1, notice that there are three distinct steps involved when using external event receivers: subscribe, notification, and unsubscribe.</span></span>
  
    
    

<span data-ttu-id="860f2-168">**На рисунке 1 поток завершения данных для внешних уведомлений**</span><span class="sxs-lookup"><span data-stu-id="860f2-168">**Figure 1 Complete data flow for external notifications**</span></span>

  
    
    

  
    
    
![Поток данных для уведомлений о внешних событиях](../images/ExtEvtsAndAlrts_Figure1.jpg)
  
    
    

  
    
    

  
    
    

## <a name="eventsubscriber-subscribe-to-notifications"></a><span data-ttu-id="860f2-170">EventSubscriber: подписки на уведомления</span><span class="sxs-lookup"><span data-stu-id="860f2-170">EventSubscriber: subscribe to notifications</span></span>
<span data-ttu-id="860f2-171"><a name="bkmk_eventsubscriber"> </a></span><span class="sxs-lookup"><span data-stu-id="860f2-171"></span></span>

<span data-ttu-id="860f2-p111">Для пользователя (объект SharePoint) для получения уведомлений при изменении базовых данных пользователю необходимо подписаться на уведомления для сущности. Для этого схемы модели BDC был расширен стереотипа **Subscribe**. Стереотипа **Subscribe** используемые SharePoint для внешней системы знать, что отправитель запрашивает уведомлений об изменениях в базовые данные.</span><span class="sxs-lookup"><span data-stu-id="860f2-p111">For a user (SharePoint object) to receive notifications when the underlying data has changed, the user must subscribe to the notifications for an entity. To allow this, the BDC Model schema has been extended to include the **Subscribe** stereotype. The **Subscribe** stereotype is used by SharePoint to let the external system know that the sender is requesting to be notified of changes to the underlying data.</span></span>
  
    
    
<span data-ttu-id="860f2-175">На рисунке 2 показано обмен информацией между SharePoint и внешней системы во время процесса подписки на.</span><span class="sxs-lookup"><span data-stu-id="860f2-175">Figure 2 demonstrates the flow of information between SharePoint and the external system during the Subscribe process.</span></span>
  
    
    

<span data-ttu-id="860f2-176">**На рисунке 2. Подписка Технологическая схема**</span><span class="sxs-lookup"><span data-stu-id="860f2-176">**Figure 2. Subscribe process flow**</span></span>

  
    
    

  
    
    
![Последовательность операций метода подписки на внешние события](../images/ExtEvtsAndAlerts_Figure2.jpg)
  
    
    
<span data-ttu-id="860f2-178">Ниже описаны общие поток в процедуре подписки.</span><span class="sxs-lookup"><span data-stu-id="860f2-178">The following describes the general flow of the subscription process:</span></span>
  
    
    

  
    
    

1. <span data-ttu-id="860f2-p112">**Пользователь запрашивает подписки для уведомлений.** Использование настраиваемого пользовательского интерфейса (кнопка на странице или ленты), SharePoint инициирует запрос на приложение внешней системе для уведомлений.</span><span class="sxs-lookup"><span data-stu-id="860f2-p112">**User requests a subscription for notifications.** Using a custom user interface (a button on a page or a ribbon), SharePoint initiates a request to the external system app for notifications.</span></span>
    
  
2. <span data-ttu-id="860f2-p113">**SharePoint создает адрес доставки.** В ходе процесса подписки на SharePoint создает конечных точек REST, где доставки уведомлений.</span><span class="sxs-lookup"><span data-stu-id="860f2-p113">**SharePoint generates a delivery address.** As part of the Subscribe process, SharePoint creates a REST endpoint where notifications will be delivered.</span></span>
    
  
3. <span data-ttu-id="860f2-p114">**К внешней системе отправляется запрос подписки.** SharePoint инкапсулирует запросившей информации наряду с динамически созданные URL-адрес REST и отправляет веб-запрос к внешней системе.</span><span class="sxs-lookup"><span data-stu-id="860f2-p114">**Subscription request is sent to the external system.** SharePoint then encapsulates the requestor information along with the dynamically generated REST URL, and sends a web request to the external system.</span></span>
    
  
4. <span data-ttu-id="860f2-p115">**Внешняя система получает запрос.** Существуют разные возможности по внедрению хранилища подписок. В этом примере необходимо использовать таблицу базы данных SQL Server.</span><span class="sxs-lookup"><span data-stu-id="860f2-p115">**External system receives request.** There are different possibilities for implementing a subscription store. In this example, you will use a SQL Server database table.</span></span>
    
  
5. <span data-ttu-id="860f2-p116">**Внешняя система генерирует subscriptionId.** Новые **subscriptionId** создается с помощью кода в приложении бизнес (LOB). **subscriptionId** должно быть идентификатором GUID.</span><span class="sxs-lookup"><span data-stu-id="860f2-p116">**External system generates a subscriptionId.** A new **subscriptionId** is generated using code in the line-of-business (LOB) application. The **subscriptionId** should be a GUID.</span></span>
    
  
6. <span data-ttu-id="860f2-p117">**Внешняя система записывает подписки.** Приложение внешняя система записывает **subscriptionId**, адрес доставки, тип события и другие сведения, отправленные из SharePoint в хранилище данных подписки.</span><span class="sxs-lookup"><span data-stu-id="860f2-p117">**External system records the subscription.** The external system application records the **subscriptionId**, delivery address, event type, and other information sent from SharePoint into the subscription store.</span></span>
    
  
7. <span data-ttu-id="860f2-p118">**Внешняя система отправляет subscriptionId SharePoint.** Для SharePoint для правильной маршрутизации обновлений, отправляемые с внешней системы **subscriptionId** отправляется SharePoint и SharePoint записывает эти данные в базе данных.</span><span class="sxs-lookup"><span data-stu-id="860f2-p118">**External system sends the subscriptionId back to SharePoint.** For SharePoint to correctly route the updates that are sent by the external system, the **subscriptionId** is sent back to SharePoint and SharePoint records that information in its database.</span></span>
    
    <span data-ttu-id="860f2-p119">Модели BDC работает на импорт функции **Subscribe**. Метаданные для функции импорта показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="860f2-p119">The BDC model is working against a **Subscribe** function import. The metadata for function import is shown in this example.</span></span>
    


```XML
  FunctionImport
 
<EntityType Name="EntitySubscribe">
   <Key>
      <PropertyRef Name="SubscriptionId" />
   </Key>
   <Property Name="SubscriptionId" Type="Edm.Int32" Nullable="false" 
      p6:StoreGeneratedPattern="Identity" 
      xmlns:p6="http://schemas.microsoft.com/ado/2009/02/edm/annotation" />
   <Property Name="EntityName" Type="Edm.String" MaxLength="250" FixedLength="false" 
      Unicode="true" />
   <Property Name="DeliveryURL" Type="Edm.String" MaxLength="250" FixedLength="false" 
      Unicode="true" />
   <Property Name="EventType" Type="Edm.Int32" />
   <Property Name="UserId" Type="Edm.String" MaxLength="50" FixedLength="false" 
      Unicode="true" />
   <Property Name="SubscribeTime" Type="Edm.Binary" MaxLength="8" FixedLength="true" 
      p6:StoreGeneratedPattern="Computed" 
      xmlns:p6="http://schemas.microsoft.com/ado/2009/02/edm/annotation" />
   <Property Name="SelectColumns" Type="Edm.String" MaxLength="10" FixedLength="false" 
      Unicode="true" />
</EntityType>

```


### <a name="code-example-bdc-model-with-subscribe"></a><span data-ttu-id="860f2-197">Пример кода: модели BDC с подписки на</span><span class="sxs-lookup"><span data-stu-id="860f2-197">Code example: BDC model with Subscribe</span></span>

<span data-ttu-id="860f2-198">Ниже приведен пример модели BDC с помощью метода **Subscribe** добавлена.</span><span class="sxs-lookup"><span data-stu-id="860f2-198">The following is an example of a BDC model with the **Subscribe** method added.</span></span>
  
    
    

```XML

<Method Name="SubscribeCustomer" DefaultDisplayName="Customer Subscribe" IsStatic="true">
   <Properties>
     <Property Name="ODataEntityUrl" Type="System.String">/EntitySubscribes</Property>
     <Property Name="ODataHttpMethod" Type="System.String">POST</Property>
     <Property Name="ODataPayloadKind" Type="System.String">Entry</Property>
     <Property Name="ODataFormat" Type="System.String">application/atom+xml</Property>
     <Property Name="ODataServiceOperation" Type="System.Boolean">false</Property>
   </Properties>
   <AccessControlList>
      <AccessControlEntry Principal="NT Authority\\Authenticated Users">
         <Right BdcRight="Edit" />
         <Right BdcRight="Execute" />
         <Right BdcRight="SetPermissions" />
         <Right BdcRight="SelectableInClients" />
      </AccessControlEntry>
   </AccessControlList>
   <Parameters>
      <Parameter Direction="In" Name="@DeliveryURL">
         <TypeDescriptor TypeName="System.String" Name="DeliveryURL" >
            <Properties>
               <Property Name="IsDeliveryAddress" Type="System.Boolean">true</Property>
            </Properties>
         </TypeDescriptor>
      </Parameter>
      <Parameter Direction="In" Name="@EventType">
         <TypeDescriptor TypeName="System.Int32" Name="EventType" >
            <Properties>
               <Property Name="IsEventType" Type="System.Boolean">true</Property>
            </Properties>
         </TypeDescriptor>
      </Parameter>
      <Parameter Direction="In" Name="@EntityName">
         <TypeDescriptor TypeName="System.String" Name="EntityName" >
            <DefaultValues>
               <DefaultValue MethodInstanceName="SubscribeCustomer" 
                  Type="System.String">Customers</DefaultValue>
            </DefaultValues>
      </TypeDescriptor>
    </Parameter>
    <Parameter Direction="In" Name="@SelectColumns">
      <TypeDescriptor TypeName="System.String" Name="SelectColumns" >
        <DefaultValues>
          <DefaultValue MethodInstanceName="SubscribeCustomer" Type="System.String">*</DefaultValue>
        </DefaultValues>
      </TypeDescriptor>
    </Parameter>
    <Parameter Direction="Return" Name="SubscribeReturn">
      <TypeDescriptor Name="SubscribeReturnRootTd" TypeName="Microsoft.BusinessData.Runtime.DynamicType">
        <TypeDescriptors>
          <TypeDescriptor Name="SubscriptionId" TypeName="System.String" >
            <Properties>
              <Property Name="SubscriptionIdName" Type="System.String">Default</Property>
            </Properties>
            <Interpretation>
              <ConvertType LOBType="System.Int32" BDCType="System.String"/>
            </Interpretation>
          </TypeDescriptor>
          <TypeDescriptor Name="DeliveryURL" TypeName="System.String" />
          <TypeDescriptor Name="SelectColumns" TypeName="System.String" >
          </TypeDescriptor>
          <TypeDescriptor Name="EntityName" TypeName="System.String" />
          <TypeDescriptor Name="EventType" TypeName="System.Int32" />
          <TypeDescriptor Name="UserId" TypeName="System.String" />
          <!--TypeDescriptor Name="SubscribeTime" TypeName="System." /-->
        </TypeDescriptors>
      </TypeDescriptor>
    </Parameter>
  </Parameters>
  <MethodInstances>
    <MethodInstance Type="EventSubscriber" ReturnParameterName="SubscribeReturn" ReturnTypeDescriptorPath="SubscribeReturnRootTd" Default="true" Name="SubscribeCustomer" DefaultDisplayName="Customer Subscribe">
      <AccessControlList>
        <AccessControlEntry Principal="NT Authority\\Authenticated Users">
          <Right BdcRight="Edit" />
          <Right BdcRight="Execute" />
          <Right BdcRight="SetPermissions" />
          <Right BdcRight="SelectableInClients" />
        </AccessControlEntry>
      </AccessControlList>
    </MethodInstance>
  </MethodInstances>
</Method>
```

<span data-ttu-id="860f2-199">В таблице 1 перечислены важные атрибуты модели BDC, необходимые для стереотипа **Subscribe** работы.</span><span class="sxs-lookup"><span data-stu-id="860f2-199">Table 1 lists the important attributes of the BDC model that are needed to make the **Subscribe** stereotype work.</span></span>
  
    
    

<span data-ttu-id="860f2-200">**В таблице 1. Атрибуты модели BDC**</span><span class="sxs-lookup"><span data-stu-id="860f2-200">**Table 1. BDC model attributes**</span></span>


|<span data-ttu-id="860f2-201">**Атрибут**</span><span class="sxs-lookup"><span data-stu-id="860f2-201">**Attribute**</span></span>|<span data-ttu-id="860f2-202">**Описание**</span><span class="sxs-lookup"><span data-stu-id="860f2-202">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="860f2-203">**IsDeliveryAddress**</span><span class="sxs-lookup"><span data-stu-id="860f2-203">**IsDeliveryAddress**</span></span> <br/> |<span data-ttu-id="860f2-204">Флаг **Boolean**, используемый в **TypeDescriptor** указывает, является ли указанный адрес доставки для доставки уведомлений.</span><span class="sxs-lookup"><span data-stu-id="860f2-204">A **Boolean** flag used on a **TypeDescriptor** to indicate whether the delivery address provided is to be used to deliver notifications.</span></span> <br/> |
|<span data-ttu-id="860f2-205">**IsEventType**</span><span class="sxs-lookup"><span data-stu-id="860f2-205">**IsEventType**</span></span> <br/> |<span data-ttu-id="860f2-p120">Флаг **Boolean**, используемый в **TypeDescriptor** указывает, является ли предоставленный тип события для использования в качестве типа события. Допустимые типы событий, **ItemAdded**, **ItemUpdated**, **ItemDeleted**и т. д. </span><span class="sxs-lookup"><span data-stu-id="860f2-p120">A **Boolean** flag used on a **TypeDescriptor** to indicate whether the event type provided is to be used as the event type. Valid event types are **ItemAdded**, **ItemUpdated**, **ItemDeleted**, and so on.  </span></span><br/> |
|<span data-ttu-id="860f2-208">**SubscriptionIdName**</span><span class="sxs-lookup"><span data-stu-id="860f2-208">**SubscriptionIdName**</span></span> <br/> |<span data-ttu-id="860f2-209">Строка, используемая на **TypeDescriptor**, который представляет имя **subscriptionId** части.</span><span class="sxs-lookup"><span data-stu-id="860f2-209">A string used on a **TypeDescriptor** that represents the name of a **subscriptionId** part.</span></span> <br/> |
   

## <a name="notifications"></a><span data-ttu-id="860f2-210">Уведомления</span><span class="sxs-lookup"><span data-stu-id="860f2-210">Notifications</span></span>
<span data-ttu-id="860f2-211"><a name="bkmk_notifications"> </a></span><span class="sxs-lookup"><span data-stu-id="860f2-211"></span></span>

<span data-ttu-id="860f2-212">В SharePoint чтобы разрешить внешние источники данных для уведомления SharePoint при сведения во внешней системе, были ли изменены был улучшен инфраструктуру обработку событий.</span><span class="sxs-lookup"><span data-stu-id="860f2-212">In SharePoint, the event-handling infrastructure has been enhanced to allow external data sources to notify SharePoint when information in the external system has been modified.</span></span> <span data-ttu-id="860f2-213">Затем когда SharePoint получает уведомление, приемники событий, связанных с внешним списком SharePoint или сущности может выполнять код для выполнения указанного действия.</span><span class="sxs-lookup"><span data-stu-id="860f2-213">Then, when SharePoint receives a notification, event receivers that are associated with the SharePoint external list or entity can execute code to perform specified actions.</span></span>
  
    
    
<span data-ttu-id="860f2-p122">При создании подписки во внешней системе требуется способ сообщить SharePoint о изменений, внесенных в конкретной сущности. Предполагается, что во внешней системе доставки уведомлений на адрес доставки в соответствии с требованиями SharePoint к внешней системе во время процесса подписки на использование формате OData Atom полезных данных.</span><span class="sxs-lookup"><span data-stu-id="860f2-p122">When a subscription is created, the external system needs a way to tell SharePoint about the changes that have occurred on a particular entity. The external system is expected to deliver notifications to the delivery address as provided by SharePoint to the external system during the Subscribe process using an OData Atom-formatted payload.</span></span>
  
    
    
<span data-ttu-id="860f2-216">На рисунке 3 показаны поток обмена данными между внешней системы и SharePoint, при добавлении новой записи данных во внешней системе.</span><span class="sxs-lookup"><span data-stu-id="860f2-216">Figure 3 shows the communication flow between the external system and SharePoint when a new record is added to the data in the external system.</span></span>
  
    
    

<span data-ttu-id="860f2-217">**Процесс уведомления на рисунке 3**</span><span class="sxs-lookup"><span data-stu-id="860f2-217">**Figure 3 Notification process**</span></span>

  
    
    

  
    
    
![Процесс уведомления о внешних событиях](../images/ExtEvtsAndAlerts_Figure3.jpg)
  
    
    

  
    
    

1. <span data-ttu-id="860f2-p123">**Новую запись добавляется к внешней системе.** В этом примере новая запись добавляется к внешней системе, с помощью пользовательского интерфейса приложения или непосредственно в базе данных.</span><span class="sxs-lookup"><span data-stu-id="860f2-p123">**New record is added to external system.** In this example, a new record is added to the external system using the application user interface or directly into the database.</span></span>
    
  
2. <span data-ttu-id="860f2-p124">**Внешней системы приложение получает уведомление об изменении.** Приложение внешней системы имеет будут получать уведомления об изменениях, происходящих в базовые данные. Существует несколько способов это сделать. Можно использовать SQL триггеров, которые запускаются при изменении данных на отдельных таблиц или создать механизм опроса для запроса хранилища данных для изменения. Существуют другие способы выполнения этой задачи, но каждая будет иметь оценку с повышения производительности.</span><span class="sxs-lookup"><span data-stu-id="860f2-p124">**External system application is notified of the change.** The external system application has to be made aware of the changes that are happening to the underlying data. There are a number of ways to do this. You can use SQL triggers that fire when data changes on specific tables, or you can create a polling mechanism to query the data store for changes. There are other ways to accomplish this, but each will have to be evaluated with performance in mind.</span></span>
    
  
3. <span data-ttu-id="860f2-p125">**Внешняя система отправляет запрос уведомления SharePoint по адресу доставки.** Для передачи изменений, запрос формате Atom должен отправляться на адрес доставки, который хранится в хранилище подписки бизнес-приложения.</span><span class="sxs-lookup"><span data-stu-id="860f2-p125">**External system sends notification request to SharePoint through delivery address.** To communicate the changes, an Atom-formatted request has to be sent to the delivery address that is stored in the LOB application's subscription store.</span></span>
    
  

### <a name="notification-payload"></a><span data-ttu-id="860f2-228">Полезные данные уведомления</span><span class="sxs-lookup"><span data-stu-id="860f2-228">Notification payload</span></span>

<span data-ttu-id="860f2-229">Создание уведомлений, бизнес-системы имеет для создания полезных данных HTTP, который включает в себя полные сведения изменения элемента или идентификатор изменения элемента.</span><span class="sxs-lookup"><span data-stu-id="860f2-229">In constructing the notification, the LOB system has to create an HTTP payload that includes either the full details of the item that changed, or just the identity of the item that changed.</span></span>
  
    
    

- <span data-ttu-id="860f2-p126">**Удостоверений:** При отправке полезных данных как удостоверение, полезных данных должен иметь только сведения об идентификации измененный элемент. Например для клиента в сущности клиентов, полезные данные только будет содержать идентификатор клиента, который был изменен.</span><span class="sxs-lookup"><span data-stu-id="860f2-p126">**Identity:** When the payload is sent as an identity, the payload is expected to have only information about the identity of the changed item. For example, for a customer in a Customers entity, the payload would only contain the ID of the customer that has changed.</span></span>
    
  
- <span data-ttu-id="860f2-p127">**Полное элемента:** В этом случае полезных данных  это запись, который был изменен во внешней системе. В примере клиента включается запись всей измененных клиента.</span><span class="sxs-lookup"><span data-stu-id="860f2-p127">**Full item:** In this case, the payload is an entire record that has changed in the external system. In the customer example, the entire changed customer record is included.</span></span>
    
  

> <span data-ttu-id="860f2-234">**Примечание:** Все элементы поддерживается только при использовании соединитель OData.</span><span class="sxs-lookup"><span data-stu-id="860f2-234">**Note:** The full item is only supported when you use the OData connector.</span></span> 
  
    
    

<span data-ttu-id="860f2-235">Во время процесса подписки должен задаваться тип полезной нагрузки, отправляемого во внешней системе.</span><span class="sxs-lookup"><span data-stu-id="860f2-235">The type of payload that is being sent by the external system must be indicated during the subscription process.</span></span>
  
    
    
<span data-ttu-id="860f2-236">Ниже приведен пример свойства модели BDC, используемого для уведомлений.</span><span class="sxs-lookup"><span data-stu-id="860f2-236">The following is an example of the BDC model property used for notifications.</span></span>
  
    
    



```XML

<Property Name="NotificationParserType" Type="System.String">
   ODataEntryContentNotificationParser
</Property>

```

<span data-ttu-id="860f2-237">Если не указан, полезных данных по умолчанию является учетные данные.</span><span class="sxs-lookup"><span data-stu-id="860f2-237">If it is not specified, the default payload is an identity payload.</span></span>
  
    
    

### <a name="notification-delivery-address-virtual-address"></a><span data-ttu-id="860f2-238">Адрес доставки уведомлений (виртуальный адрес)</span><span class="sxs-lookup"><span data-stu-id="860f2-238">Notification delivery address (virtual address)</span></span>

<span data-ttu-id="860f2-p128">Процесс подписки, запущенного из результаты SharePoint в виртуального адреса, создаваемого с SharePoint, позволяя точки входа для внешней системы для регистрации уведомлений. Адрес доставки используется во внешней системе для отправки этих уведомлений. Адрес доставки также передается внешней системы во время запроса подписки.</span><span class="sxs-lookup"><span data-stu-id="860f2-p128">The subscription process initiated from SharePoint results in a virtual address being created by SharePoint, allowing an entry point for the external system to post notifications. The delivery address is used by the external system to post those notifications. The delivery address is also passed to the external system during the subscription request.</span></span>
  
    
    

## <a name="eventunsubscriber-remove-subscription-from-the-notifications-list"></a><span data-ttu-id="860f2-242">EventUnsubscriber: удаление подписки в списке уведомлений</span><span class="sxs-lookup"><span data-stu-id="860f2-242">EventUnsubscriber: remove subscription from the notifications list</span></span>
<span data-ttu-id="860f2-243"><a name="bkmk_eventunsubscriber"> </a></span><span class="sxs-lookup"><span data-stu-id="860f2-243"></span></span>

<span data-ttu-id="860f2-244">Операция **Unsubscribe** удаляет подписку в списке уведомлений.</span><span class="sxs-lookup"><span data-stu-id="860f2-244">The **Unsubscribe** operation removes a subscription from the notifications list.</span></span>
  
    
    
 <span data-ttu-id="860f2-p129">На рисунке 4 показано, что метод **UnSubscribe** намного проще. Так как идентификатор подписки отправлено обратно в SharePoint и SharePoint записать его, все, что требуется  отправить запрос отказа от подписки с идентификатором подписки на правильные.</span><span class="sxs-lookup"><span data-stu-id="860f2-p129">Figure 4 shows that the **UnSubscribe** method is much simpler. Because the subscription ID was sent back to SharePoint, and SharePoint recorded it, all that is needed is to send the UnSubscribe request with the correct subscription ID.</span></span>
  
    
    

<span data-ttu-id="860f2-247">**На рисунке 4 потока кода для метода отказа от подписки**</span><span class="sxs-lookup"><span data-stu-id="860f2-247">**Figure 4 Code flow for UnSubscribe method**</span></span>

  
    
    

  
    
    
![Процесс отмены подписки на внешние уведомления](../images/ExternalEventsAndAlerts_UnsubscribeFlow.jpg)
  
    
    

### <a name="bdc-model-for-unsubscribe"></a><span data-ttu-id="860f2-249">Модели BDC для отказа от подписки</span><span class="sxs-lookup"><span data-stu-id="860f2-249">BDC model for Unsubscribe</span></span>

<span data-ttu-id="860f2-250">В следующем примере XML показано, как создать модели BDC, которая отменяет подписку из уведомления о событиях внешней системы.</span><span class="sxs-lookup"><span data-stu-id="860f2-250">The following XML example shows how you can create a BDC model that unsubscribes from the external system event notifications.</span></span>
  
    
    

```XML

<Method Name="UnSubscribeExpenseReport" DefaultDisplayName="ExpenseReport
    Unsubscribe">
    <Properties>
        <Property Name="ODataEntityUrl" Type="System.String">
            /Subscriptions(@ID)</Property>
        <Property Name="ODataHttpMethod" Type="System.String">DELETE</Property>
        <Property Name="ODataPayloadKind" Type="System.String">Property</Property>
        <Property Name="ODataServiceOperation" Type="System.Boolean">false</Property>
    </Properties>
    <AccessControlList>
        <AccessControlEntry Principal="NT Authority\\Authenticated Users">
            <Right BdcRight="Edit" />
            <Right BdcRight="Execute" />
            <Right BdcRight="SetPermissions" />
            <Right BdcRight="SelectableInClients" />
        </AccessControlEntry>
    </AccessControlList>
    <Parameters>
        <Parameter Name="@ID" Direction="In">
            <TypeDescriptor Name="ID" TypeName="System.Int32">
                <Properties>
                    <Property Name="SubscriptionIdName" Type="System.String">ID</Property>
                </Properties>
                <Interpretation>
                    <ConvertType LOBType="System.Int32" BDCType="System.String" />
                </Interpretation>
            </TypeDescriptor>
        </Parameter>
    </Parameters>
    <MethodInstances>
        <MethodInstance Name="UnSubscribeExpenseReport" DefaultDisplayName="ExpenseReport 
             Unsubscribe" Type="EventUnsubscriber" Default="true">
            <AccessControlList>
                <AccessControlEntry Principal="NT Authority\\Authenticated Users">
                    <Right BdcRight="Edit" />
                    <Right BdcRight="Execute" />
                    <Right BdcRight="SetPermissions" />
                    <Right BdcRight="SelectableInClients" />
                </AccessControlEntry>
            </AccessControlList>
        </MethodInstance>
    </MethodInstances>
</Method>



<Method IsStatic="false" Name="Unsubscribe">
    <AccessControlList>
        <AccessControlEntry Principal="NT AUTHORITY\\Authenticated Users">
            <Right BdcRight="Edit" />
            <Right BdcRight="Execute" />
            <Right BdcRight="SetPermissions" />
            <Right BdcRight="SelectableInClients" />
        </AccessControlEntry>
    </AccessControlList>
    <Parameters>
        <Parameter Direction="In" Name="subscriptionId">
            <TypeDescriptor TypeName="System.String" Name="subscriptionId" 
                IsSubscriptionId="true" />
         </Parameter>
    </Parameters>
    <MethodInstances>
        <MethodInstance Type="EventUnsubscriber" Default="true" Name="Unsubscribe" 
            DefaultDisplayName="UnSubscriber">
            <Properties>
                <Property Name="LastDesignedOfficeItemType" Type="System.String">None</Property>
            </Properties>
            <AccessControlList>
                <AccessControlEntry Principal=" NT AUTHORITY\\Authenticated Users ">
                    <Right BdcRight="Edit" />
                    <Right BdcRight="Execute" />
                    <Right BdcRight="SetPermissions" />
                    <Right BdcRight="SelectableInClients" />
                </AccessControlEntry>
            </AccessControlList>
        </MethodInstance>
    </MethodInstances>
</Method>

```


## <a name="code-example-attach-an-event-receiver-to-an-external-list"></a><span data-ttu-id="860f2-251">Пример кода: подключение к внешнему списку приемника событий</span><span class="sxs-lookup"><span data-stu-id="860f2-251">Code example: Attach an event receiver to an external list</span></span>
<span data-ttu-id="860f2-252"><a name="AttachingRER"> </a></span><span class="sxs-lookup"><span data-stu-id="860f2-252"></span></span>

<span data-ttu-id="860f2-p130">В следующем коде приведен пример того, как для подключения к внешнему списку приемника событий. После подключения, приемник событий прослушивание уведомлений из внешней системы о обновления, добавления и удаления, которые выполняются на исходные данные.</span><span class="sxs-lookup"><span data-stu-id="860f2-p130">The following code provides an example of how to attach an event receiver to an external list. After it is attached, the event receiver listens for notifications from the external system about updates, additions, and deletions that are performed on the native data.</span></span>
  
    
    

```XML

private static void AddEventReceiver(string siteUrl, string listTitle)
{ 
   string assembly = "SampleEventReceiver, Culture=neutral, Version=1.0.0.0, 
      PublicKeyToken=1bfafa687d2e46a7";
   string className = "SampleEventReceiver.EntryContentEventReceiver"; 
   
   try
   {
      using (SPSite site = new SPSite(siteUrl)) 
      { 
         using (SPWeb web = site.OpenWeb()) 
         {
            SPList list = web.Lists[listTitle]; 
            list.EventReceivers.Add(SPEventReceiverType.ItemAdded, 
               assembly, className); 
         }
      }
   }
   catch (Exception e) 
   { 
      Console.WriteLine(e); 
   }
}

```


## <a name="beyond-the-basics-learn-more-about-using-external-event-receivers"></a><span data-ttu-id="860f2-255">От простого к сложному: Дополнительные сведения об использовании приемников внешних событий</span><span class="sxs-lookup"><span data-stu-id="860f2-255">Beyond the basics: Learn more about using external event receivers</span></span>
<span data-ttu-id="860f2-256"><a name="Externalevents_Learnmore"> </a></span><span class="sxs-lookup"><span data-stu-id="860f2-256"></span></span>

<span data-ttu-id="860f2-257">Дополнительные сведения о внешние события и оповещения содержатся в следующих разделах.</span><span class="sxs-lookup"><span data-stu-id="860f2-257">For more information about external events and alerts, see the following.</span></span>
  
    
    

<span data-ttu-id="860f2-258">**В таблице 2. Расширенные концепции для работы с приемниками внешних событий**</span><span class="sxs-lookup"><span data-stu-id="860f2-258">**Table 2. Advanced concepts for working with external event receivers**</span></span>


|<span data-ttu-id="860f2-259">**Статья**</span><span class="sxs-lookup"><span data-stu-id="860f2-259">**Article**</span></span>|<span data-ttu-id="860f2-260">**Описание**</span><span class="sxs-lookup"><span data-stu-id="860f2-260">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="860f2-261">Как: создать службу данных OData для использования в качестве внешней системы BCS</span><span class="sxs-lookup"><span data-stu-id="860f2-261">How to: Create an OData data service for use as a BCS external system</span></span>](how-to-create-an-odata-data-service-for-use-as-a-bcs-external-system.md) <br/> |<span data-ttu-id="860f2-262">Узнайте, как создать службу Интернет адресации Windows Communication Foundation (WCF), который используется для отправки уведомлений SharePoint при изменении базовых данных OData.</span><span class="sxs-lookup"><span data-stu-id="860f2-262">Learn how to create an Internet-addressable Windows Communication Foundation (WCF) service that uses OData to send notifications to SharePoint when the underlying data changes.</span></span> <span data-ttu-id="860f2-263">Такие уведомления используются для активируют события, подключенные к внешним спискам.</span><span class="sxs-lookup"><span data-stu-id="860f2-263">These notifications are used to trigger events that are attached to external lists.</span></span>  <br/> |
   

## <a name="additional-resources"></a><span data-ttu-id="860f2-264">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="860f2-264">Additional resources</span></span>
<span data-ttu-id="860f2-265"><a name="Externalevents_Addres"> </a></span><span class="sxs-lookup"><span data-stu-id="860f2-265"></span></span>


-  [<span data-ttu-id="860f2-266">Новые возможности служб Business Connectivity Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="860f2-266">What's new in Business Connectivity Services in SharePoint</span></span>](what-s-new-in-business-connectivity-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="860f2-267">Business Connectivity Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="860f2-267">Business Connectivity Services in SharePoint</span></span>](business-connectivity-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="860f2-268">Справочник по программистов Business Connectivity Services для SharePoint</span><span class="sxs-lookup"><span data-stu-id="860f2-268">Business Connectivity Services programmers reference for SharePoint</span></span>](business-connectivity-services-programmers-reference-for-sharepoint.md)
    
  
-  [<span data-ttu-id="860f2-269">Как: создание приемников внешних событий</span><span class="sxs-lookup"><span data-stu-id="860f2-269">How to: Create external event receivers</span></span>](how-to-create-external-event-receivers.md)
    
  

