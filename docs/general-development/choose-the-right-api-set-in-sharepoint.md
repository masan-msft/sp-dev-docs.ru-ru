---
title: "Выбор правильного набора API в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: f36645da-77c5-47f1-a2ca-13d4b62b320d
ms.openlocfilehash: 2cfe9766b0a765fc3ca2abedfa91c92f6db7b9b1
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="choose-the-right-api-set-in-sharepoint"></a><span data-ttu-id="ac766-102">Выбор правильного набора API в SharePoint</span><span class="sxs-lookup"><span data-stu-id="ac766-102">Choose the right API set in SharePoint</span></span>
<span data-ttu-id="ac766-103">Сведения о нескольких наборах API, включенных в SharePoint, в том числе для серверной объектной модели, различных клиентских объектных моделей и веб-службы REST или OData.</span><span class="sxs-lookup"><span data-stu-id="ac766-103">Learn about the several sets of APIs that are provided in SharePoint, including the server object model and the various client object models, and the REST/OData web service.</span></span>
    
    

## <a name="factors-that-determine-which-api-set-to-use"></a><span data-ttu-id="ac766-104">Факторы, определяющие, какой набор API нужно использовать</span><span class="sxs-lookup"><span data-stu-id="ac766-104">Factors that determine which API set to use</span></span>
<span data-ttu-id="ac766-105"><a name="Factors"> </a></span><span class="sxs-lookup"><span data-stu-id="ac766-105"></span></span>

<span data-ttu-id="ac766-p101">Доступ к платформе SharePoint можно получить с помощью нескольких наборов интерфейсов API. Какой из них использовать, зависит от следующих факторов:</span><span class="sxs-lookup"><span data-stu-id="ac766-p101">You can choose from several sets of APIs to access the SharePoint platform. Which one you use depends on the following factors:</span></span>
  
    
    

- <span data-ttu-id="ac766-p102">**Тип приложения.** Можно использовать, помимо прочего, следующие не взаимоисключающие типы: Надстройка SharePoint, веб-часть на странице SharePoint, приложение Silverlight, которое запускается на клиентском компьютере или клиентском мобильном устройстве, приложение ASP.NET, которое представлено в SharePoint благодаря IFrame, код JavaScript, который выполняется на странице веб-сайта SharePoint, страница приложения SharePoint, приложение Microsoft .NET Framework, которое выполняется на клиентском компьютере, сценарий Windows PowerShell и задание таймера, которое выполняется на сервере SharePoint.</span><span class="sxs-lookup"><span data-stu-id="ac766-p102">**The type of application.** The possibilities include, but are not limited to, the following, which are not mutually exclusive categories: an SharePoint Add-in, a Web Part on a SharePoint page, a Silverlight application running on either a client computer or a client mobile device, an ASP.NET application exposed in SharePoint by an IFrame, JavaScript running in a SharePoint site page, a SharePoint application page, a Microsoft .NET Framework application running on a client computer, a Windows PowerShell script, and a timer job running on a SharePoint server.</span></span>
    
  
- <span data-ttu-id="ac766-p103">**Ваши навыки.** Вы удивитесь, но в SharePoint можно создавать приложения, не вникая особо в программирование для SharePoint. Можно сразу приступить к разработке приложений для SharePoint, имея опыт работы с одной из следующих моделей программирования:</span><span class="sxs-lookup"><span data-stu-id="ac766-p103">**Your existing skills.** To a surprising degree, you can create applications in SharePoint without needing to learn a lot about SharePoint programming. You can jump right into SharePoint development if you already have experience in any of the following programming models:</span></span>
    
  - <span data-ttu-id="ac766-113">JavaScript</span><span class="sxs-lookup"><span data-stu-id="ac766-113">JavaScript</span></span>
    
  
  - <span data-ttu-id="ac766-114">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="ac766-114">ASP.NET</span></span>
    
  
  - <span data-ttu-id="ac766-115">REST или OData</span><span class="sxs-lookup"><span data-stu-id="ac766-115">REST/OData</span></span>
    
  
  - <span data-ttu-id="ac766-116">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="ac766-116">.NET Framework</span></span>
    
  
  - <span data-ttu-id="ac766-117">Windows Phone</span><span class="sxs-lookup"><span data-stu-id="ac766-117">Windows Phone</span></span>
    
  
  - <span data-ttu-id="ac766-118">Silverlight</span><span class="sxs-lookup"><span data-stu-id="ac766-118">Silverlight</span></span>
    
  
  - <span data-ttu-id="ac766-119">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="ac766-119">Windows PowerShell</span></span>
    
  
- <span data-ttu-id="ac766-p104">**Устройство, на котором выполняется код.** Можно использовать сервер фермы SharePoint, внешний сервер (например, облачный сервер), клиентский компьютер и мобильное устройство.</span><span class="sxs-lookup"><span data-stu-id="ac766-p104">**The device on which the code runs.** The possibilities include a server in the SharePoint farm, an external server such as a server in the cloud, a client computer, and a mobile device.</span></span>
    
  
<span data-ttu-id="ac766-p105">В этом разделе предлагается обзор различных наборов интерфейсов API, предоставляемых в SharePoint. На рисунке 1 показано, какие наборы интерфейсов API можно использовать для разработки каждого из 13 стандартных приложений для SharePoint. В большинстве случаев для этого доступны несколько интерфейсов API.</span><span class="sxs-lookup"><span data-stu-id="ac766-p105">This topic provides an overview of the various API sets that are provided by SharePoint. Figure 1 shows which sets of APIs can be used to develop each of 13 common SharePoint-related applications. For many applications, you can choose from more than one API.</span></span>
  
    
    

<span data-ttu-id="ac766-125">**Рисунок 1. Выбранные типы расширений SharePoint и наборы интерфейсов API для SharePoint**</span><span class="sxs-lookup"><span data-stu-id="ac766-125">**Figure 1. Selected SharePoint extension types and SharePoint sets of APIs**</span></span>

  
    
    

  
    
    
![Диаграмма Венна наборов API и типов приложений SharePoint](../images/SharePointAPIsetsandselectedSharePointextensions.png)
  
    
    

  
    
    
<span data-ttu-id="ac766-p106">В таблице ниже представлены рекомендации о том, какой набор API использовать для списка выбранных стандартных проектов расширений SharePoint. В оставшихся разделах статьи описаны различные наборы интерфейсов API.</span><span class="sxs-lookup"><span data-stu-id="ac766-p106">The following table provides guidance on which set of APIs to use for a selected list of common SharePoint extensibility projects. The remaining sections of this topic describe the various sets of APIs.</span></span>
  
    
    


|<span data-ttu-id="ac766-129">**Что нужно сделать**</span><span class="sxs-lookup"><span data-stu-id="ac766-129">**If you want to do this ...**</span></span>|<span data-ttu-id="ac766-130">**Какой интерфейс API подойдет**</span><span class="sxs-lookup"><span data-stu-id="ac766-130">**... use these APIs**</span></span>|
|:-----|:-----|
|<span data-ttu-id="ac766-131">Создать веб-приложение ASP.NET, выполняющее операции создания, чтения, обновления и удаления (CRUD) данных SharePoint или внешних данных, подключаемых в SharePoint через внешний тип контента Службы Microsoft Business Connectivity Services (BCS), с использованием брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="ac766-131">Create an ASP.NET web application that performs create/read/update/deleted (CRUD) operations across a firewall on SharePoint data or external data that is surfaced in SharePoint by a Microsoft Business Connectivity Services (BCS) external content type</span></span>  <br/> |<span data-ttu-id="ac766-132">Клиентская объектная модель JavaScript.</span><span class="sxs-lookup"><span data-stu-id="ac766-132">JavaScript client object model</span></span>  <br/> |
|<span data-ttu-id="ac766-133">Создать веб-приложение ASP.NET, выполняющее операции CRUD с данными SharePoint или внешними данными, подключаемыми в SharePoint с использованием внешнего типа контента BCS, не вызывая SharePoint через брандмауэр.</span><span class="sxs-lookup"><span data-stu-id="ac766-133">Create an ASP.NET web application that performs CRUD operations on SharePoint data or external data that is surfaced in SharePoint by a BCS external content type, but does not have to call SharePoint across a firewall</span></span>  <br/> |<span data-ttu-id="ac766-134">Клиентская объектная модель .NET Framework или Silverlight, а также конечные точки REST или OData.</span><span class="sxs-lookup"><span data-stu-id="ac766-134">.NET Framework client object model, Silverlight client object model, or REST/OData endpoints</span></span>  <br/> |
|<span data-ttu-id="ac766-135">Создать веб-приложение LAMP, выполняющее операции CRUD с данными SharePoint или внешними данными, подключаемыми в SharePoint с использованием внешнего типа контента BCS.</span><span class="sxs-lookup"><span data-stu-id="ac766-135">Create a LAMP web application that performs CRUD operations on SharePoint data or external data that is surfaced in SharePoint by a BCS external content type</span></span>  <br/> |<span data-ttu-id="ac766-136">Конечные точки REST или OData.</span><span class="sxs-lookup"><span data-stu-id="ac766-136">REST/OData endpoints</span></span>  <br/> |
|<span data-ttu-id="ac766-137">Создать приложение для Windows Phone, выполняющее операции CRUD с данными SharePoint.</span><span class="sxs-lookup"><span data-stu-id="ac766-137">Create a Windows Phone app that performs CRUD operations on SharePoint data</span></span>  <br/> |<span data-ttu-id="ac766-138">Клиентская объектная модель для мобильных устройств.</span><span class="sxs-lookup"><span data-stu-id="ac766-138">Mobile client object model</span></span>  <br/> |
|<span data-ttu-id="ac766-139">Создать приложение для Windows Phone, использующее службу push-уведомлений (Майкрософт), чтобы оповещать мобильное устройство о событиях в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="ac766-139">Create a Windows Phone app that uses the Microsoft Push Notification Service to alert the mobile device of events in SharePoint</span></span>  <br/> |<span data-ttu-id="ac766-140">Клиентская объектная модель для мобильных устройств и серверная объектная модель.</span><span class="sxs-lookup"><span data-stu-id="ac766-140">Mobile client object model and the server object model</span></span>  <br/> |
|<span data-ttu-id="ac766-141">Создать приложение для iOS или Android, выполняющее операции CRUD с данными SharePoint.</span><span class="sxs-lookup"><span data-stu-id="ac766-141">Create an iOS or Android app that performs CRUD operations on SharePoint data</span></span>  <br/> |<span data-ttu-id="ac766-142">конечные точки REST и OData;</span><span class="sxs-lookup"><span data-stu-id="ac766-142">REST/OData endpoints</span></span>  <br/> |
|<span data-ttu-id="ac766-143">Создать приложение .NET Framework, выполняющее операции CRUD с данными SharePoint.</span><span class="sxs-lookup"><span data-stu-id="ac766-143">Create a .NET Framework application that performs CRUD operations on SharePoint data</span></span>  <br/> |<span data-ttu-id="ac766-144">Клиентская объектная модель .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="ac766-144">.NET Framework client object model</span></span>  <br/> |
|<span data-ttu-id="ac766-145">Создать приложение Silverlight, выполняющее операции CRUD с данными SharePoint.</span><span class="sxs-lookup"><span data-stu-id="ac766-145">Create a Silverlight application that performs CRUD operations on SharePoint data</span></span>  <br/> |<span data-ttu-id="ac766-146">Клиентская объектная модель Silverlight</span><span class="sxs-lookup"><span data-stu-id="ac766-146">Silverlight client object model</span></span>  <br/> |
|<span data-ttu-id="ac766-147">Создать приложение HTML или JavaScript, выполняющее операции CRUD с данными SharePoint.</span><span class="sxs-lookup"><span data-stu-id="ac766-147">Create an HTML/JavaScript application that performs CRUD operations on SharePoint data</span></span>  <br/> |<span data-ttu-id="ac766-148">Клиентская объектная модель JavaScript.</span><span class="sxs-lookup"><span data-stu-id="ac766-148">JavaScript client object model</span></span>  <br/> |
|<span data-ttu-id="ac766-149">Создать Надстройка Office, совместимое с SharePoint.</span><span class="sxs-lookup"><span data-stu-id="ac766-149">Create an Office Add-in that works with SharePoint</span></span>  <br/> |<span data-ttu-id="ac766-150">Клиентская объектная модель JavaScript.</span><span class="sxs-lookup"><span data-stu-id="ac766-150">JavaScript client object model</span></span>  <br/> |
|<span data-ttu-id="ac766-151">Создать пользовательскую команду Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ac766-151">Create a custom Windows PowerShell command</span></span>  <br/> |<span data-ttu-id="ac766-152">Объектная модель сервера</span><span class="sxs-lookup"><span data-stu-id="ac766-152">Server object model</span></span>  <br/> |
|<span data-ttu-id="ac766-153">Создать задание таймера.</span><span class="sxs-lookup"><span data-stu-id="ac766-153">Create a timer job</span></span>  <br/> |<span data-ttu-id="ac766-154">Серверная объектная модель.</span><span class="sxs-lookup"><span data-stu-id="ac766-154">Server object model</span></span>  <br/> |
|<span data-ttu-id="ac766-155">Создать расширение центра администрирования.</span><span class="sxs-lookup"><span data-stu-id="ac766-155">Create an extension of Central Administration</span></span>  <br/> |<span data-ttu-id="ac766-156">Серверная объектная модель.</span><span class="sxs-lookup"><span data-stu-id="ac766-156">Server object model</span></span>  <br/> |
|<span data-ttu-id="ac766-157">Создать единую фирменную символику для всей ферме SharePoint.</span><span class="sxs-lookup"><span data-stu-id="ac766-157">Create consistent branding across an entire SharePoint farm</span></span>  <br/> |<span data-ttu-id="ac766-158">Объектная модель сервера</span><span class="sxs-lookup"><span data-stu-id="ac766-158">Server object model</span></span>  <br/> |
|<span data-ttu-id="ac766-159">Создать пользовательскую веб-часть, страницу приложения или пользовательский элемент управления ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="ac766-159">Create a custom Web Part, application page, or ASP.NET user control</span></span>  <br/> |<span data-ttu-id="ac766-160">Серверная объектная модель</span><span class="sxs-lookup"><span data-stu-id="ac766-160">Server object model</span></span>  <br/> <span data-ttu-id="ac766-161">**Важно!** Если функции, которые вы планируете предложить клиентам, не рассчитаны на администрирование с помощью SharePoint за пределами семейства веб-сайтов, то вместо использования серверной объектной модели рекомендуем создать надстройку SharePoint, включающую удаленное веб-приложение ASP.NET с необходимыми настраиваемыми веб-частями и пользовательскими элементами управления.</span><span class="sxs-lookup"><span data-stu-id="ac766-161">If the functionality you want to offer customers is not oriented to SharePoint administration at a scope broader than site collection, we recommend that, instead of using the server object model, you create an SharePoint Add-in that includes a remote ASP.NET web application with custom Web Parts and user controls as needed. See the top two rows of this table.</span></span> <span data-ttu-id="ac766-162">Обратите внимание на первые две строки этой таблицы.</span><span class="sxs-lookup"><span data-stu-id="ac766-162">See the top two rows of this table.</span></span>           |
   

## <a name="server-object-model"></a><span data-ttu-id="ac766-163">Серверная объектная модель</span><span class="sxs-lookup"><span data-stu-id="ac766-163">Server object model</span></span>
<span data-ttu-id="ac766-164"><a name="ServerOM"> </a></span><span class="sxs-lookup"><span data-stu-id="ac766-164"></span></span>

<span data-ttu-id="ac766-p108">Серверная объектная модель управляемых классов содержит самый большой набор интерфейсов API. На уровне SharePoint Foundation 2013 в ее состав входят классы и элементы, обеспечивающие программный способ управления базовым сайтом, и структура списка SharePoint Foundation. Большая часть этих классов находится в пространстве имен  [Microsoft.SharePoint](https://msdn.microsoft.com/library/Microsoft.SharePoint.aspx) . Кроме того, с помощью серверной объектной модели можно расширить возможности практически каждого компонента SharePoint Foundation, в том числе рабочих процессов, оповещений, веб-частей, базового поиска и Службы Microsoft Business Connectivity Services (BCS). Серверная объектная модель также содержит расширенный набор интерфейсов API, чтобы обеспечить расширение возможностей системы администрирования и безопасности SharePoint Foundation, в том числе резервного копирования, диагностики работоспособности фермы, ведения журнала, управления веб-приложениями и фермой, обновления версии, развертывания, кэширования и настройки Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ac766-p108">The largest set of APIs is in the server object model of managed classes. At the level of SharePoint Foundation 2013, this object model includes classes and members that enable programmatic control of the basic site and list structure of SharePoint Foundation. Most of these classes are in the  [Microsoft.SharePoint](https://msdn.microsoft.com/library/Microsoft.SharePoint.aspx) namespace. In addition, you can extend almost every SharePoint Foundation component by using the server object model, including workflows, alerts, Web Parts, basic search, and Microsoft Business Connectivity Services (BCS). The server object model also includes an extensive set of APIs enable extensions of the administration and security system of SharePoint Foundation, including backup, farm health and diagnostics, logging, farm and web application management, upgrade, deployment, caching, and Windows PowerShell customization.</span></span>
  
    
    
<span data-ttu-id="ac766-170">На уровне SharePoint добавляется намного больше классов для программирования управления корпоративным информационным содержимым (ECM), профилей пользователей, таксономии, расширенного поиска и других функций SharePoint.</span><span class="sxs-lookup"><span data-stu-id="ac766-170">At the level of SharePoint Server 2013, many more classes are added to enable programming of Enterprise Content Management (ECM), user profiles, taxonomy, advanced search, and other features of SharePoint Server 2013.</span></span>
  
    
    
<span data-ttu-id="ac766-p109">Можно использовать  [LINQ to Objects](http://msdn.microsoft.com/ru-ru/library/bb397919.aspx), чтобы отправлять запросы к любой коллекции **IEnumerable**, но  [Поставщик LINQ to SharePoint](http://msdn.microsoft.com/library/3fa2dc5f-d308-4337-aefd-191a5df8dbbe%28Office.15%29.aspx) позволяет отправлять прямые запросы к спискам в базах данных контента SharePoint. Строго говоря, этот поставщик недоступен в случае любого другого набора интерфейсов API, упомянутого в этой статье. Но использование синтаксиса LINQ возможно с большинством других наборов.</span><span class="sxs-lookup"><span data-stu-id="ac766-p109">You can use  [LINQ to Objects](http://msdn.microsoft.com/ru-ru/library/bb397919.aspx) to query any **IEnumerable** collection in memory, but a [LINQ to SharePoint provider](http://msdn.microsoft.com/library/3fa2dc5f-d308-4337-aefd-191a5df8dbbe%28Office.15%29.aspx) enables direct querying of the lists in the SharePoint content databases. Strictly speaking, this provider is not available with any other set of APIs discussed in this topic; however, there are ways to use LINQ syntax in most of the others.</span></span>
  
    
    
<span data-ttu-id="ac766-p110">Сборки, определяющие встроенные серверные классы, устанавливаются в глобальный кэш сборок каждого сервера при установке SharePoint. Когда программирование выполняется для серверной объектной модели, сборки устанавливаются как решения ферм в глобальный кэш сборок.</span><span class="sxs-lookup"><span data-stu-id="ac766-p110">The assemblies that define the built-in server-side classes are installed to the global assembly cache of each server when SharePoint is installed. When you program against the server object model, your assemblies are installed as farm solutions to the global assembly cache.</span></span>
  
    
    

> <span data-ttu-id="ac766-175">**Примечание.** Вместо новых изолированных решений в SharePoint теперь рекомендуется разрабатывать надстройки SharePoint, но изолированные решения все еще можно устанавливать в семействах веб-сайтов в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="ac766-175">**Note:** Developing new sandboxed solutions against SharePoint is deprecated in favor of developing SharePoint Add-ins, but sandboxed solutions can still be installed to site collections on SharePoint.</span></span> <span data-ttu-id="ac766-176">Сборки этих решений остаются в пакете, пока они не используются. При использовании они временно устанавливаются в папке на сервере.</span><span class="sxs-lookup"><span data-stu-id="ac766-176">Developing new spusercode against sp15allshort is deprecated in favor of developing spappplural, but spusercode can still be installed to site collections on sp15allshort. The assemblies of these solutions remain in the package except when they are actually in use, at which time they are temporarily installed to a folder on the server. For more information, see Where are Assemblies in Sandboxed Solutions Deployed?.</span></span> <span data-ttu-id="ac766-177">Дополнительные сведения см. в статье [Где развертываются сборки изолированных решений?](http://msdn.microsoft.com/library/dadbb20b-1bf7-442c-9eeb-bd9f01dbda45%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="ac766-177">For more information, see  [Where are Assemblies in Sandboxed Solutions Deployed?](http://msdn.microsoft.com/library/dadbb20b-1bf7-442c-9eeb-bd9f01dbda45%28Office.15%29.aspx).</span></span> 
  
    
    


### <a name="limitations-on-when-you-can-use-the-server-object-model"></a><span data-ttu-id="ac766-178">Ограничения на использование серверной объектной модели</span><span class="sxs-lookup"><span data-stu-id="ac766-178">Limitations on when you can use the server object model</span></span>

<span data-ttu-id="ac766-p112">Настраиваемая логика Надстройки SharePoint всегда распространяется "вниз" (к клиенту), "вверх" (в облако) или "через" (к определенному серверу, не входящему в ферму SharePoint). Во всех этих моделях распространения необходимо использовать одну из клиентских объектных моделей либо конечные точки REST или OData. (Вы не можете использовать серверную объектную модель в Надстройка SharePoint.) Например, если приложение содержит страницы с размещением в SharePoint, они могут получать доступ к данным SharePoint с помощью клиентской объектной модели JavaScript. На таких страницах также могут быть представлены приложения Silverlight, использующие клиентскую объектную модель Silverlight SharePoint. Дополнительные сведения о Надстройки SharePoint см. в статье  [Важные аспекты архитектуры и разработки надстройки SharePoint](http://msdn.microsoft.com/library/ae96572b-8f06-4fd3-854f-fc312f7f2d88%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="ac766-p112">Custom logic in SharePoint Add-ins is always distributed "down" to the client or "up" to the cloud (or "over" to some server outside the SharePoint farm). In all of these distribution models, one of the client object models or the REST/OData endpoints must be used. (You cannot use the server object model in an SharePoint Add-in.) For example, if the app contains SharePoint-hosted pages, those pages can access SharePoint data by using the JavaScript client object model. Such pages could also expose Silverlight applications that use the SharePoint Silverlight client object model. For more information about SharePoint Add-ins, see  [Important aspects of the SharePoint Add-in architecture and development landscape](http://msdn.microsoft.com/library/ae96572b-8f06-4fd3-854f-fc312f7f2d88%28Office.15%29.aspx).</span></span>
  
    
    

## <a name="client-object-models-for-managed-code"></a><span data-ttu-id="ac766-184">Клиентские объектные модели для управляемого кода</span><span class="sxs-lookup"><span data-stu-id="ac766-184">Client object models for managed code</span></span>
<span data-ttu-id="ac766-185"><a name="ClientManagedOM"> </a></span><span class="sxs-lookup"><span data-stu-id="ac766-185"></span></span>

<span data-ttu-id="ac766-186">В SharePoint используются три клиентские объектные модели для управляемого кода: Silverlight, .NET и модель для мобильных устройств.</span><span class="sxs-lookup"><span data-stu-id="ac766-186">SharePoint has three client object models for managed code: .NET, Silverlight, and mobile.</span></span>
  
    
    

### <a name="net-client-object-model"></a><span data-ttu-id="ac766-187">Клиентская объектная модель .NET</span><span class="sxs-lookup"><span data-stu-id="ac766-187">.NET client object model</span></span>

<span data-ttu-id="ac766-p113">Объектная модель SharePoint для .NET Framework используется в приложениях .NET Framework, которые работают с клиентом Windows, отличном от телефона. Таким клиентом можно считать любое из следующих устройств:</span><span class="sxs-lookup"><span data-stu-id="ac766-p113">The SharePoint object model for .NET Framework is used in .NET Framework applications that run on a non-phone Windows client. Any of the following counts as such a client:</span></span>
  
    
    

- <span data-ttu-id="ac766-190">компьютер пользователя;</span><span class="sxs-lookup"><span data-stu-id="ac766-190">A user's computer</span></span>
    
  
- <span data-ttu-id="ac766-191">сервер, не входящий в ферму SharePoint;</span><span class="sxs-lookup"><span data-stu-id="ac766-191">A server that is external to the SharePoint farm</span></span>
    
  
- <span data-ttu-id="ac766-192">веб-роль или рабочая роль в Microsoft Azure;</span><span class="sxs-lookup"><span data-stu-id="ac766-192">A web role or worker role on Microsoft Azure</span></span>
    
  
<span data-ttu-id="ac766-193">Практически каждому классу на основном сайте и в объектной модели сервера списков соответствует класс в клиентской объектной модели .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="ac766-193">Almost every class in the core site and list server object model has a corresponding class in the .NET Framework client object model.</span></span> <span data-ttu-id="ac766-194">Кроме того, клиентская объектная модель .NET Framework предоставляет полный набор API для расширения других компонентов, включая некоторые функции SharePoint, например ECM, таксономию, профили пользователей, расширенный поиск, аналитика, службы BCS и другие.</span><span class="sxs-lookup"><span data-stu-id="ac766-194">Almost every class in the core site and list server object model has a corresponding class in the .NET Framework client object model. In addition, the .NET Framework client object model exposes a full set of APIs for extending other features, including some SharePoint Server 2013 features such as ECM, taxonomy, user profiles, advanced search, analytics, BCS, and others.</span></span>
  
    
    
<span data-ttu-id="ac766-p115">Для повышения производительности строки кода, написанные с помощью клиентской объектной модели .NET Framework, отправляются на сервер SharePoint в виде пакетов. Там эти строки преобразовываются в серверный код, который выполняется. Затем запрашиваемые результаты и информация о новом состоянии всех переменных возвращаются клиенту. Как разработчик вы определяете, будет ли код пакета выполняться синхронно или асинхронно. (В случае синхронного выполнения приложение .NET Framework сначала подождет, пока будут возвращены результаты с сервера. При асинхронном выполнении сразу же продолжится обработка на стороне клиента, а пользовательский интерфейс не перестанет отвечать.)</span><span class="sxs-lookup"><span data-stu-id="ac766-p115">To improve performance, lines of code written against in the .NET Framework client object model are sent to the SharePoint server in batches where they are converted to server-side code and executed. The queried results, and the new state of all variables, are then returned to the client. You as the developer determine whether a batch runs synchronously or asynchronously. (In a synchronous batch, the .NET Framework application waits for the returned results from the server before continuing; in an asynchronous batch, client-side processing continues immediately and the client user interface (UI) remains responsive.)</span></span>
  
    
    
<span data-ttu-id="ac766-p116">Чтобы запрашивать любой объект **IEnumerable**, в том числе объекты SharePoint, которые реализуют **IEnumerable**, вы можете использовать синтаксис запросов LINQ в клиентском коде. Но для этого необходимо использовать  [LINQ to Objects](http://msdn.microsoft.com/ru-ru/library/bb397919.aspx), а не  [поставщик LINQ to SharePoint](http://msdn.microsoft.com/library/3fa2dc5f-d308-4337-aefd-191a5df8dbbe%28Office.15%29.aspx), так как документация последнего не подходит для клиентского кода.</span><span class="sxs-lookup"><span data-stu-id="ac766-p116">You can use LINQ query syntax in your client code to query any **IEnumerable** object, including SharePoint objects that implement **IEnumerable**. However, when you do this, you are using  [LINQ to Objects](http://msdn.microsoft.com/ru-ru/library/bb397919.aspx), not the  [LINQ to SharePoint provider](http://msdn.microsoft.com/library/3fa2dc5f-d308-4337-aefd-191a5df8dbbe%28Office.15%29.aspx), so documentation of the latter is not relevant to client-side code.</span></span>
  
    
    
<span data-ttu-id="ac766-p117">Сборки для клиентской объектной модели .NET Framework должны устанавливаться на клиенте. Они входят в состав распространяемого пакета, который можно получить на странице  [Клиентские компоненты SharePoint](http://www.microsoft.com/en-us/download/details.aspx?id=35585).</span><span class="sxs-lookup"><span data-stu-id="ac766-p117">The assemblies for the .NET Framework client object model must be installed on the client. They are included in a redistributable package that you can obtain on the  [SharePoint Client Components](http://www.microsoft.com/en-us/download/details.aspx?id=35585).</span></span>
  
    
    
<span data-ttu-id="ac766-203">Примеры использования объектной модели .NET Framework см. в статье [Выполнение базовых операций с использованием кода библиотеки клиента в SharePoint](http://msdn.microsoft.com/library/5a69c9e3-73bf-4ed5-bc19-182056bdb394%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="ac766-203">For examples of using the .NET Framework object model, see  [Complete basic operations using SharePoint client library code](http://msdn.microsoft.com/library/5a69c9e3-73bf-4ed5-bc19-182056bdb394%28Office.15%29.aspx).</span></span>
  
    
    

> <span data-ttu-id="ac766-204">**Примечание.** Вы также можете использовать конечные точки SharePoint REST или OData в приложении .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="ac766-204">**Note:** You can also use the SharePoint REST/OData endpoints in a .NET Framework application.</span></span> <span data-ttu-id="ac766-205">Сравнение клиентской объектной модели .NET Framework с конечными точками SharePoint REST и OData представлено в разделе [Конечные точки REST и OData](#RESTOData) далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="ac766-205">Note You can also use the SharePoint REST/OData endpoints in a .NET Framework application. For a comparison of the .NET Framework client object model with the SharePoint REST/OData endpoints, see the section  [REST/OData endpoints](#RESTOData) later in this article.</span></span>
  
    
    


### <a name="silverlight-client-object-model"></a><span data-ttu-id="ac766-206">Клиентская объектная модель Silverlight</span><span class="sxs-lookup"><span data-stu-id="ac766-206">Silverlight client object model</span></span>

<span data-ttu-id="ac766-p119">Объектная модель SharePoint для Silverlight используется в приложениях Silverlight независимо от места сохранения компилированного XAP-файла. Это может быть библиотека на веб-сайте SharePoint, на клиентском компьютере, в облачном хранилище или на внешнем сервере. Обычно приложение Silverlight подключается в SharePoint в объекте  [SilverlightWebPart](https://msdn.microsoft.com/library/Microsoft.SharePoint.WebPartPages.SilverlightWebPart.aspx) . Клиентская объектная модель Silverlight в SharePoint практически идентична клиентской объектной модели .NET Framework и предусматривает поддержку тех же областей расширений. Главное отличие состоит в том, что в версии Silverlight все пакеты команд отправляются на сервер асинхронно, чтобы элементы пользовательского интерфейса приложения оставались активны.</span><span class="sxs-lookup"><span data-stu-id="ac766-p119">The SharePoint object model for Silverlight is used in Silverlight applications, regardless of where the compiled .xap file is persisted. It may be in an assets library on a SharePoint website, on a client computer, in cloud storage, or on an external server. Typically, a Silverlight application is surfaced in SharePoint in a  [SilverlightWebPart](https://msdn.microsoft.com/library/Microsoft.SharePoint.WebPartPages.SilverlightWebPart.aspx) object. The Silverlight client object model in SharePoint is nearly identical to the .NET Framework client object model, and it includes support for the same extensibility areas. The principal difference is that in the Silverlight version, all batches of commands are sent to the server asynchronously so that the UI of the application remains active.</span></span>
  
    
    
<span data-ttu-id="ac766-p120">Сборки для клиентской объектной модели Silverlight сохраняются на каждом сервере SharePoint в папке %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\TEMPLATE\\LAYOUTS\\ClientBin. Их не нужно устанавливать на компьютер, на котором установлено приложение Silverlight, хотя это предусмотрено. Кроме того, вы их можете сохранить в XAP-файл приложения.</span><span class="sxs-lookup"><span data-stu-id="ac766-p120">The assemblies for the Silverlight client object model are persisted on every SharePoint server at %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\TEMPLATE\\LAYOUTS\\ClientBin. They do not have to be installed on the computer that is running the Silverlight application, although you have the option of doing so. Also, you can package them into the .xap file of the application.</span></span>
  
    
    
<span data-ttu-id="ac766-p121">XAP-файлы Silverlight можно включить в Надстройки SharePoint, в том числе в приложения с размещением в SharePoint. В последнем случае выполняется развертывание XAP-файла в библиотеке на сайте приложения. (Дополнительные сведения о сайтах приложения см в статье  [Хост-сайты, сайты надстроек и компоненты SharePoint в SharePoint](http://msdn.microsoft.com/library/b791cdf5-8aa2-47fa-bc4c-aee437354759%28Office.15%29.aspx).) Поэтому благодаря приложению Silverlight можно включить настраиваемый код SharePoint в состав любого приложения, так как настраиваемый серверный код недопустим в Надстройки SharePoint. Это также позволяет разработчикам Silverlight использовать свои навыки для создания приложений SharePoint, почти не тратя время на обучение.</span><span class="sxs-lookup"><span data-stu-id="ac766-p121">Silverlight .xap files can be included in SharePoint Add-ins, including SharePoint-hosted apps. In the latter case, the .xap file is deployed to a library on the app web. (For more information about app webs, see  [Host webs, add-in webs, and SharePoint components in SharePoint](http://msdn.microsoft.com/library/b791cdf5-8aa2-47fa-bc4c-aee437354759%28Office.15%29.aspx).) This makes a Silverlight application a useful way of including custom SharePoint code in an app, because custom server-side code is not allowed in SharePoint Add-ins. It also enables Silverlight developers to use their existing skills to create SharePoint applications with a minimal learning curve.</span></span>
  
    
    

> <span data-ttu-id="ac766-218">**Примечание.** Вы также можете использовать конечные точки SharePoint REST или OData в приложении Silverlight.</span><span class="sxs-lookup"><span data-stu-id="ac766-218">**Note:** You can also use the SharePoint REST/OData endpoints in a Silverlight application.</span></span> <span data-ttu-id="ac766-219">Сравнение клиентской объектной модели Silverlight с конечными точками SharePoint REST и OData представлено в разделе [Конечные точки REST и OData](#RESTOData) далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="ac766-219">Note You can also use the SharePoint REST/OData endpoints in a Silverlight application. For a comparison of the Silverlight client object model with the SharePoint REST/OData endpoints, see the section  [REST/OData endpoints](#RESTOData) later in this article.</span></span>
  
    
    


### <a name="mobile-object-model"></a><span data-ttu-id="ac766-220">Объектная модель для мобильных устройств</span><span class="sxs-lookup"><span data-stu-id="ac766-220">Mobile object model</span></span>

<span data-ttu-id="ac766-p123">Специальная версия клиентской объектной модели Silverlight доступна для устройств Windows Phone. Она содержит дополнительные интерфейсы API, которые подходят только для телефонов. Например, интерфейсы API, позволяющие регистрацию телефона для получения сообщений службы push-уведомлений (Майкрософт). Эта модель поддерживает все основные функции SharePoint. Но поддержка не распространяется на дополнительные расширения, которые поддерживаются двумя другими клиентскими объектными моделями для управляемого кода. Для доступа к этим дополнительным функциям используйте конечные точки REST или OData SharePoint в мобильном приложении. См. раздел  [Конечные точки REST или OData](#RESTOData) далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="ac766-p123">A special version of the Silverlight client object model is available for Windows Phone devices. It includes some additional APIs that are relevant only to telephones, such as APIs that enable a phone app to register for notifications from the Microsoft Push Notification Service. It supports all core SharePoint functionality; however, it does not provide support for any of the non-core extensibility areas that are supported by the other two client object models for managed code. To access those additional areas, use the SharePoint REST/OData endpoints in your mobile app. See the section  [REST/OData endpoints](#RESTOData) later in this article.</span></span>
  
    
    
<span data-ttu-id="ac766-p124">Сборки для объектной модели для мобильных устройств сохраняются на каждом сервере SharePoint в папке %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\TEMPLATE\\LAYOUTS\\ClientBin. Их необходимо поместить в XAP-файл приложения для Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="ac766-p124">The assemblies for the mobile object model are persisted on every SharePoint server at %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\TEMPLATE\\LAYOUTS\\ClientBin. You package them into the .xap file of your Windows Phone application.</span></span>
  
    
    

## <a name="javascript-object-model"></a><span data-ttu-id="ac766-228">Объектная модель JavaScript</span><span class="sxs-lookup"><span data-stu-id="ac766-228">JavaScript object model</span></span>
<span data-ttu-id="ac766-229"><a name="JavaScriptOM"> </a></span><span class="sxs-lookup"><span data-stu-id="ac766-229"></span></span>

<span data-ttu-id="ac766-p125">В SharePoint предоставлена объектная модель JavaScript, которую можно использовать во встроенном сценарии или отдельных JS-файлах. В ней предусмотрены те же функции, что и в клиентских объектных моделях .NET Framework и Silverlight. Как и клиентская объектная модель Silverlight, объектная модель JavaScript позволяет включить настраиваемый код SharePoint в состав любого приложения, так как настраиваемый код недопустим в Надстройки SharePoint. Это также позволяет веб-разработчикам использовать свои навыки работы с JavaScript, чтобы создавать приложения для SharePoint, почти не тратя время на обучение.</span><span class="sxs-lookup"><span data-stu-id="ac766-p125">SharePoint provides a JavaScript object model for use in either inline script or separate .js files. It includes all the same functionality as the .NET Framework and Silverlight client object models. Like the Silverlight client object model, the JavaScript object model is a useful way of including custom SharePoint code in an app, because custom server-side code is not allowed in SharePoint Add-ins. It also enables web developers to use their existing JavaScript skills to create SharePoint applications with a minimal learning curve.</span></span>
  
    
    
<span data-ttu-id="ac766-p126">Как и клиентские объектные модели для управляемого кода, инфраструктура JavaScript для SharePoint взаимодействует с серверами фермы с помощью пакетов с кодом, который всегда выполняется асинхронно. Кроме того, сейчас возможно получать доступ к данным SharePoint на разных доменах с помощью JavaScript (но только к данным одного и того же родительского семейства веб-сайтов), что было недопустимо в предыдущих версиях SharePoint. Дополнительные сведения см. в статье  [Обращение к данным SharePoint из надстроек с помощью междоменной библиотеки](http://msdn.microsoft.com/library/bc37ff5c-1285-40af-98ae-01286696242d%28Office.15%29.aspx). Данные возвращаются с сервера с помощью Нотация объектов JavaScript (JSON).</span><span class="sxs-lookup"><span data-stu-id="ac766-p126">Just like the managed-code client object models, the JavaScript infrastructure for SharePoint interacts with the farm servers in batches. These batches always run asynchronously. In addition, it is now possible to access SharePoint data across domains in JavaScript (but only data that is within the same parent site collection), which was not allowed in previous versions of SharePoint. For more information, see  [Access SharePoint data from add-ins using the cross-domain library](http://msdn.microsoft.com/library/bc37ff5c-1285-40af-98ae-01286696242d%28Office.15%29.aspx). Data is returned from the server in JavaScript Object Notation (JSON).</span></span>
  
    
    
<span data-ttu-id="ac766-238">Объектная модель JavaScript определяется в наборе JS-файлов, размещенных в папке %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\TEMPLATE\\LAYOUTS на каждом сервере.</span><span class="sxs-lookup"><span data-stu-id="ac766-238">The JavaScript object model is defined in a set of *.js files located at %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\TEMPLATE\\LAYOUTS on each server.</span></span>
  
    
    
<span data-ttu-id="ac766-239">Примеры использования объектной модели .NET Framework см. в статье [Выполнение базовых операций с использованием кода библиотеки JavaScript в SharePoint](http://msdn.microsoft.com/library/29089af8-dbc0-49b7-a1a0-9e311f49c826%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="ac766-239">For examples of using the .NET Framework object model, see  [Complete basic operations using JavaScript library code in SharePoint](http://msdn.microsoft.com/library/29089af8-dbc0-49b7-a1a0-9e311f49c826%28Office.15%29.aspx).</span></span>
  
    
    

> <span data-ttu-id="ac766-240">**Примечание.** Вы также можете использовать конечные точки SharePoint REST или OData в приложении JavaScript.</span><span class="sxs-lookup"><span data-stu-id="ac766-240">**Note:** You can also use the SharePoint REST/OData endpoints in a JavaScript application.</span></span> <span data-ttu-id="ac766-241">Сравнение клиентской объектной модели JavaScript с конечными точками REST и OData в SharePoint представлено в следующем разделе, [Конечные точки REST и OData](#RESTOData).</span><span class="sxs-lookup"><span data-stu-id="ac766-241">Note You can also use the SharePoint REST/OData endpoints in a JavaScript application. For a comparison of the JavaScript client object model with SharePoint's REST/OData endpoints, see the following section,  [REST/OData endpoints](#RESTOData).</span></span> 
  
    
    


## <a name="restodata-endpoints"></a><span data-ttu-id="ac766-242">Конечные точки REST и OData</span><span class="sxs-lookup"><span data-stu-id="ac766-242">REST/OData endpoints</span></span>
<span data-ttu-id="ac766-243"><a name="RESTOData"> </a></span><span class="sxs-lookup"><span data-stu-id="ac766-243"></span></span>

<span data-ttu-id="ac766-p128">В случае сценариев, при которых необходимо получить доступ к объектам SharePoint со стороны клиентских технологий, которые не используют JavaScript и не созданы на платформах .NET Framework или Silverlight, SharePoint обеспечивает реализацию веб-службы передачи репрезентативного состояния (REST), использующей  [протокол ODatal](http://www.odata.org/) для выполнения операций CRUD с данными списков SharePoint. Кроме того, почти каждый интерфейс API клиентской объектной модели имеет соответствующую конечную точку REST. Это позволяет коду напрямую взаимодействовать с артефактами SharePoint с помощью любой технологии, поддерживающей стандартные HTTP-запросы и отклики. Чтобы использовать возможности REST, встроенные в SharePoint, код создает запрос RESTful HTTP для конечной точки, соответствующей необходимому интерфейсу API клиентской объектной модели. Веб-служба client.svc обрабатывает HTTP-запрос и направляет отклик в формате Atom или JSON.</span><span class="sxs-lookup"><span data-stu-id="ac766-p128">For scenarios in which you need to access SharePoint entities from client technologies that do not use JavaScript and are not built on the .NET Framework or Silverlight platforms, SharePoint provides an implementation of a Representational State Transfer (REST) web service that uses the  [OData protocol](http://www.odata.org/) to perform CRUD operations on SharePoint list data. In addition, almost every API in the client object models has a corresponding REST endpoint. This enables your code to interact directly with SharePoint artifacts by using any technology that supports standard HTTP requests and responses. To use the REST capabilities that are built into SharePoint, your code constructs a RESTful HTTP request to an endpoint that corresponds to the desired client object model API. The client.svc web service handles the HTTP request and serves a response in either Atom or JSON format.</span></span>
  
    
    
<span data-ttu-id="ac766-249">Дополнительные сведения об использовании веб-службы REST или OData см. в статье  [Программирование с использованием службы SharePoint REST](http://msdn.microsoft.com/library/d4b5c277-ed50-420c-8a9b-860342284b72%28Office.15%29.aspx), примеры  в статье  [Выполнение базовых операций с использованием конечных точек SharePoint REST](http://msdn.microsoft.com/library/e3000415-50a0-426e-b304-b7de18f2f7d9%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="ac766-249">For more information about using the REST/OData web service, see the node  [Use OData query operations in SharePoint REST requests](http://msdn.microsoft.com/library/d4b5c277-ed50-420c-8a9b-860342284b72%28Office.15%29.aspx); for examples, see the topic  [Complete basic operations using SharePoint REST endpoints](http://msdn.microsoft.com/library/e3000415-50a0-426e-b304-b7de18f2f7d9%28Office.15%29.aspx).</span></span>
  
    
    

### <a name="comparing-restodata-programming-with-client-object-model-programming"></a><span data-ttu-id="ac766-250">Сравнение программирования с помощью REST или OData с программированием с помощью клиентской объектной модели</span><span class="sxs-lookup"><span data-stu-id="ac766-250">Comparing REST/OData programming with client object model programming</span></span>

<span data-ttu-id="ac766-p129">В некоторых случаях, возможно, лучше использовать конечные точки REST даже в приложениях, для которых доступна объектная модель SharePoint. Это в первую очередь касается разработчиков, не имеющих опыта разработки для Windows. В таблице ниже сравниваются основные функции этих типов программирования при создании приложения на платформе Windows или платформе, поддерживающей JavaScript.</span><span class="sxs-lookup"><span data-stu-id="ac766-p129">In some situations, it might be preferable to use the REST endpoints even in applications for which a SharePoint object model is available, especially for developers who do not have Windows development experience. The following table provides a comparison of the major features of these programming choices for a developer creating an application on a Windows platform or with a platform that supports JavaScript.</span></span>
  
    
    


|<span data-ttu-id="ac766-253">**Функция**</span><span class="sxs-lookup"><span data-stu-id="ac766-253">**Feature**</span></span>|<span data-ttu-id="ac766-254">**Объектная модель .NET Framework или Silverlight**</span><span class="sxs-lookup"><span data-stu-id="ac766-254">**.NET Framework or Silverlight object models**</span></span>|<span data-ttu-id="ac766-255">**Объектная модель JavaScript**</span><span class="sxs-lookup"><span data-stu-id="ac766-255">**JavaScript object model**</span></span>|<span data-ttu-id="ac766-256">**Конечные точки REST или OData, вызываемые с помощью платформы Windows или JavaScript**</span><span class="sxs-lookup"><span data-stu-id="ac766-256">**REST/OData endpoints called from a Windows platform or JavaScript**</span></span>|
|:-----|:-----|:-----|:-----|
|<span data-ttu-id="ac766-257">Объектно-ориентированное программирование</span><span class="sxs-lookup"><span data-stu-id="ac766-257">Object-oriented programming</span></span>  <br/> |<span data-ttu-id="ac766-258">Да</span><span class="sxs-lookup"><span data-stu-id="ac766-258">Yes</span></span>  <br/> |<span data-ttu-id="ac766-259">Да</span><span class="sxs-lookup"><span data-stu-id="ac766-259">Yes</span></span>  <br/> |<span data-ttu-id="ac766-260">Нет</span><span class="sxs-lookup"><span data-stu-id="ac766-260">No</span></span>  <br/> |
|<span data-ttu-id="ac766-261">Пакетная обработка</span><span class="sxs-lookup"><span data-stu-id="ac766-261">Batch processing</span></span>  <br/> |<span data-ttu-id="ac766-262">Да</span><span class="sxs-lookup"><span data-stu-id="ac766-262">Yes</span></span>  <br/> |<span data-ttu-id="ac766-263">Да</span><span class="sxs-lookup"><span data-stu-id="ac766-263">Yes</span></span>  <br/> |<span data-ttu-id="ac766-264">Да</span><span class="sxs-lookup"><span data-stu-id="ac766-264">Yes</span></span>  <br/> |
|<span data-ttu-id="ac766-265">Интерфейсы API для условной обработки и обработки исключений</span><span class="sxs-lookup"><span data-stu-id="ac766-265">APIs for conditional processing and exception handling</span></span>  <br/> |<span data-ttu-id="ac766-266">Да</span><span class="sxs-lookup"><span data-stu-id="ac766-266">Yes</span></span>  <br/> |<span data-ttu-id="ac766-267">Нет</span><span class="sxs-lookup"><span data-stu-id="ac766-267">No</span></span>  <br/> |<span data-ttu-id="ac766-268">Нет</span><span class="sxs-lookup"><span data-stu-id="ac766-268">No</span></span>  <br/> |
|<span data-ttu-id="ac766-269">Доступность синтаксиса LINQ</span><span class="sxs-lookup"><span data-stu-id="ac766-269">Availability of LINQ syntax</span></span>  <br/> |<span data-ttu-id="ac766-270">Да</span><span class="sxs-lookup"><span data-stu-id="ac766-270">Yes</span></span>  <br/> |<span data-ttu-id="ac766-271">Нет</span><span class="sxs-lookup"><span data-stu-id="ac766-271">No</span></span>  <br/> |<span data-ttu-id="ac766-272">Нет</span><span class="sxs-lookup"><span data-stu-id="ac766-272">No</span></span>  <br/> |
|<span data-ttu-id="ac766-273">Объединение данных списков из различных веб-приложений SharePoint</span><span class="sxs-lookup"><span data-stu-id="ac766-273">Combining list data from different SharePoint web applications</span></span>  <br/> |<span data-ttu-id="ac766-274">Да</span><span class="sxs-lookup"><span data-stu-id="ac766-274">Yes</span></span>  <br/> |<span data-ttu-id="ac766-275">Нет</span><span class="sxs-lookup"><span data-stu-id="ac766-275">No</span></span>  <br/> |<span data-ttu-id="ac766-276">Да</span><span class="sxs-lookup"><span data-stu-id="ac766-276">Yes</span></span>  <br/> |
|<span data-ttu-id="ac766-277">Знание разработчиками, использующим REST или OData</span><span class="sxs-lookup"><span data-stu-id="ac766-277">Familiarity to experienced REST/OData developers</span></span>  <br/> |<span data-ttu-id="ac766-278">Нет</span><span class="sxs-lookup"><span data-stu-id="ac766-278">No</span></span>  <br/> |<span data-ttu-id="ac766-279">Нет</span><span class="sxs-lookup"><span data-stu-id="ac766-279">No</span></span>  <br/> |<span data-ttu-id="ac766-280">Да</span><span class="sxs-lookup"><span data-stu-id="ac766-280">Yes</span></span>  <br/> |
|<span data-ttu-id="ac766-281">Сходство с программированием не для Windows или с помощью JavaScript</span><span class="sxs-lookup"><span data-stu-id="ac766-281">Similarity to non-Windows programming or JavaScript programming</span></span>  <br/> |<span data-ttu-id="ac766-282">Нет</span><span class="sxs-lookup"><span data-stu-id="ac766-282">No</span></span>  <br/> |<span data-ttu-id="ac766-283">Да</span><span class="sxs-lookup"><span data-stu-id="ac766-283">Yes</span></span>  <br/> |<span data-ttu-id="ac766-284">Да</span><span class="sxs-lookup"><span data-stu-id="ac766-284">Yes</span></span>  <br/> |
|<span data-ttu-id="ac766-285">Строгая типизация полей элементов списка</span><span class="sxs-lookup"><span data-stu-id="ac766-285">Strong typing for list item fields</span></span>  <br/> |<span data-ttu-id="ac766-286">Нет (если не использовать LINQ)</span><span class="sxs-lookup"><span data-stu-id="ac766-286">No (except with LINQ)</span></span>  <br/> |<span data-ttu-id="ac766-287">Нет</span><span class="sxs-lookup"><span data-stu-id="ac766-287">No</span></span>  <br/> |<span data-ttu-id="ac766-288">Да (в случае платформы Windows)          Нет (в случае JavaScript)</span><span class="sxs-lookup"><span data-stu-id="ac766-288">Yes, from Windows platform          No, from JavaScript</span></span>  <br/> |
|<span data-ttu-id="ac766-289">Использование jQuery, Knockout и других библиотек JavaScript</span><span class="sxs-lookup"><span data-stu-id="ac766-289">Leveraging jQuery, Knockout, and other JavaScript libraries</span></span>  <br/> |<span data-ttu-id="ac766-290">Нет</span><span class="sxs-lookup"><span data-stu-id="ac766-290">No</span></span>  <br/> |<span data-ttu-id="ac766-291">Да</span><span class="sxs-lookup"><span data-stu-id="ac766-291">Yes</span></span>  <br/> |<span data-ttu-id="ac766-292">Нет (в случае платформы Windows)          Да (в случае JavaScript)</span><span class="sxs-lookup"><span data-stu-id="ac766-292">No, from Windows platform          Yes, from JavaScript</span></span>  <br/> |
   

## <a name="wcf-data-services-framework"></a><span data-ttu-id="ac766-293">Платформа WCF Data Services</span><span class="sxs-lookup"><span data-stu-id="ac766-293">WCF Data Services Framework</span></span>
<span data-ttu-id="ac766-294"><a name="WCFDataServices"> </a></span><span class="sxs-lookup"><span data-stu-id="ac766-294"></span></span>

<span data-ttu-id="ac766-p130">Предпочитаете использовать синтаксис LINQ в клиентских приложениях .NET Framework или Silverlight? SharePoint поддерживает  [WCF Data Services](http://msdn.microsoft.com/ru-ru/library/cc668792.aspx) как поставщика LINQ. Можно ориентироваться на файл listdata.svc для доступа к данным списка, как в ранних версиях SharePoint Foundation, или на тот же файл client.svc, который поддерживает интерфейс OData, чтобы получить доступ ко всем объектам SharePoint (в дополнение к данным списка). Дополнительные сведения см. в статье [Запрос SharePoint Foundation с помощью служб данных ADO.NET](http://msdn.microsoft.com/library/3e3e16f7-620a-4710-a3f3-19d0236f4b4a%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="ac766-p130">If you prefer to use LINQ syntax in .NET Framework or Silverlight client applications, SharePoint supports  [WCF Data Services](http://msdn.microsoft.com/ru-ru/library/cc668792.aspx) as a LINQ provider. You can target either the listdata.svc (for list data only) as in earlier versions of SharePoint Foundation, or you can target the same client.svc that supports the OData interface for access to all SharePoint entities in addition to list data. For more information, see [Query SharePoint Foundation with ADO.NET Data Services](http://msdn.microsoft.com/library/3e3e16f7-620a-4710-a3f3-19d0236f4b4a%28Office.15%29.aspx).</span></span>
  
    
    
<span data-ttu-id="ac766-p131">На рисунке 2 показаны отношения между различными клиентскими интерфейсами API, клиентскими приложениями и SharePoint. URL-адреса _api*  URL-адреса конечных точек REST, связанные с фермой. Дополнительные сведения см. в статье  [Дополнительные сведения о службе REST в SharePoint 15](http://msdn.microsoft.com/library/2de035a0-ac75-43bd-9665-5c5a59c4c590%28Office.15%29.aspx#bk_learnmore).</span><span class="sxs-lookup"><span data-stu-id="ac766-p131">Figure 2 illustrates the relationship of the various client APIs, various types of client applications, and SharePoint. The various _api* URLs are the farm-relative URLs for the REST endpoints. For more information, see the topic  [Learning more about the SharePoint 15 REST service](http://msdn.microsoft.com/library/2de035a0-ac75-43bd-9665-5c5a59c4c590%28Office.15%29.aspx#bk_learnmore).</span></span>
  
    
    

<span data-ttu-id="ac766-301">**Рисунок 2. Клиентские приложения и интерфейсы API в SharePoint**</span><span class="sxs-lookup"><span data-stu-id="ac766-301">**Figure 2. Client applications and APIs in SharePoint**</span></span>

  
    
    

  
    
    
![Модель программирования для приложений для SharePoint](../images/Sp15_app_.png)
  
    
    

  
    
    

  
    
    

## <a name="deprecated-api-sets"></a><span data-ttu-id="ac766-303">Нерекомендуемые наборы интерфейсов API</span><span class="sxs-lookup"><span data-stu-id="ac766-303">Deprecated API sets</span></span>
<span data-ttu-id="ac766-304"><a name="DeprecatedAPIs"> </a></span><span class="sxs-lookup"><span data-stu-id="ac766-304"></span></span>

<span data-ttu-id="ac766-305">Платформа SharePoint до сих пор поддерживает обратную совместимость двух наборов API, но мы не рекомендуем их использовать в новых проектах. Эти наборы относятся к  [веб-службам ASP.NET (asmx)](http://msdn.microsoft.com/library/c587ee90-1f88-43f3-b1a7-5f3072d038f8%28Office.15%29.aspx) и [прямым RPC-вызовам файла owssvr.dll](http://msdn.microsoft.com/library/4aa5c82b-90fb-4be5-b30c-d35ecae42a81%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="ac766-305">Two API sets are still supported in the SharePoint framework for backward compatibility, but we recommend that you not use them for new projects: the  [ASP.NET (asmx) web services](http://msdn.microsoft.com/library/c587ee90-1f88-43f3-b1a7-5f3072d038f8%28Office.15%29.aspx), and  [direct Remote Procedure Calls (RPC) calls to the owssvr.dll](http://msdn.microsoft.com/library/4aa5c82b-90fb-4be5-b30c-d35ecae42a81%28Office.15%29.aspx) file.</span></span>
  
    
    

## <a name="additional-resources"></a><span data-ttu-id="ac766-306">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="ac766-306">Additional resources</span></span>
<span data-ttu-id="ac766-307"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="ac766-307"></span></span>


-  [<span data-ttu-id="ac766-308">Обзор разработки решений с помощью SharePoint</span><span class="sxs-lookup"><span data-stu-id="ac766-308">SharePoint development overview</span></span>](sharepoint-development-overview.md)
    
  
-  [<span data-ttu-id="ac766-309">Модели программирования в SharePoint</span><span class="sxs-lookup"><span data-stu-id="ac766-309">Programming models in SharePoint</span></span>](programming-models-in-sharepoint.md)
    
  
-  [<span data-ttu-id="ac766-310">Сравнение надстроек SharePoint с решениями SharePoint</span><span class="sxs-lookup"><span data-stu-id="ac766-310">SharePoint Add-ins compared with SharePoint solutions</span></span>](sharepoint-add-ins-compared-with-sharepoint-solutions.md)
    
  
-  [<span data-ttu-id="ac766-311">Программирование с использованием службы SharePoint REST</span><span class="sxs-lookup"><span data-stu-id="ac766-311">Use OData query operations in SharePoint REST requests</span></span>](http://msdn.microsoft.com/library/d4b5c277-ed50-420c-8a9b-860342284b72%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="ac766-312">Выполнение базовых операций с использованием конечных точек SharePoint REST</span><span class="sxs-lookup"><span data-stu-id="ac766-312">Complete basic operations using SharePoint REST endpoints</span></span>](http://msdn.microsoft.com/library/e3000415-50a0-426e-b304-b7de18f2f7d9%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="ac766-313">Выполнение базовых операций с использованием кода библиотеки клиента в SharePoint</span><span class="sxs-lookup"><span data-stu-id="ac766-313">Complete basic operations using SharePoint client library code</span></span>](http://msdn.microsoft.com/library/5a69c9e3-73bf-4ed5-bc19-182056bdb394%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="ac766-314">Выполнение базовых операций с использованием кода библиотеки JavaScript в SharePoint</span><span class="sxs-lookup"><span data-stu-id="ac766-314">Complete basic operations using JavaScript library code in SharePoint</span></span>](http://msdn.microsoft.com/library/29089af8-dbc0-49b7-a1a0-9e311f49c826%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="ac766-315">Запрос SharePoint Foundation с помощью служб данных ADO.NET</span><span class="sxs-lookup"><span data-stu-id="ac766-315">Query SharePoint Foundation with ADO.NET Data Services</span></span>](http://msdn.microsoft.com/library/3e3e16f7-620a-4710-a3f3-19d0236f4b4a%28Office.15%29.aspx)
    
  

  
    
    
