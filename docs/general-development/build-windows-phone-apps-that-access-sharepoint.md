---
title: "Построение приложений Windows Phone, обращающимися к SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 36681335-f772-4499-8445-f94481bc18e7
ms.openlocfilehash: 7e9f0794b49f41ac405378c73fd38bf5f9323881
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="build-windows-phone-apps-that-access-sharepoint"></a><span data-ttu-id="fa553-102">Построение приложений Windows Phone, обращающимися к SharePoint</span><span class="sxs-lookup"><span data-stu-id="fa553-102">Build Windows Phone apps that access SharePoint</span></span>
<span data-ttu-id="fa553-103">Сведения о создании SharePoint Add-ins, интеграции SharePoint и мобильных устройств, такие как Windows Phone 8 и Windows Phone 7.</span><span class="sxs-lookup"><span data-stu-id="fa553-103">Learn how to create SharePoint Add-ins that integrate SharePoint and mobile devices such as Windows Phone 8 and Windows Phone 7.</span></span>
## <a name="introduction-to-building-mobile-apps-with-sharepoint"></a><span data-ttu-id="fa553-104">Введение в создание мобильных приложений с помощью SharePoint</span><span class="sxs-lookup"><span data-stu-id="fa553-104">Introduction to building mobile apps with SharePoint</span></span>
<span data-ttu-id="fa553-105"><a name="SP15mobileapp_intro"> </a></span><span class="sxs-lookup"><span data-stu-id="fa553-105"></span></span>

<span data-ttu-id="fa553-106">SharePoint предоставляет замечательные возможности для разработчиков для создания мобильного приложения, которые передаются с пользователями, являются интерактивные и привлекательных и доступны всякий раз, когда и где это необходимо работать с ними пользователей.</span><span class="sxs-lookup"><span data-stu-id="fa553-106">SharePoint provides an exciting opportunity for developers to build mobile apps that travel with users, are interactive and attractive, and are available whenever and wherever users want to work with them.</span></span> <span data-ttu-id="fa553-107">Вы можете сочетать приложений Windows Phone 8 и Windows Phone 7 с локальной службы SharePoint и приложения или удаленных SharePoint services и приложений, работающих в облаке (например, те, которые используют SharePoint Online) для создания мощных приложения, расширения функциональных возможностей за пределы традиционного рабочего стола и ноутбуков и в среде действительно портативных, так и намного более доступными.</span><span class="sxs-lookup"><span data-stu-id="fa553-107">You can combine Windows Phone 8 and Windows Phone 7 applications with on-premises SharePoint services and applications, or with remote SharePoint services and applications that run in the cloud (such as those that use SharePoint Online) to create powerful applications that extend the functionality beyond the traditional desktop or laptop, and into a truly portable and much more accessible environment.</span></span>
  
    
    
<span data-ttu-id="fa553-108">Новые возможности мобильности, предоставляемые SharePoint, основанные на существующих Microsoft средства и технологии, такие как SharePoint, Windows Phone, Visual Studio и Silverlight.</span><span class="sxs-lookup"><span data-stu-id="fa553-108">The new mobility features offered by SharePoint are built on existing Microsoft tools and technologies, such as SharePoint, Windows Phone, Visual Studio, and Silverlight.</span></span> <span data-ttu-id="fa553-109">Разработчики, имеющие опыт работы с этими технологиями и их средства будет для создания на базе SharePoint мобильных приложений для Windows Phone без некоторого обучения.</span><span class="sxs-lookup"><span data-stu-id="fa553-109">Developers who are already familiar with those technologies and their related tools will be able to create SharePoint-powered mobile apps for Windows Phone without a steep learning curve.</span></span> <span data-ttu-id="fa553-110">В этом разделе мы изучение некоторых типов мобильных приложений на базе SharePoint, можно создать для Windows Phone 8 и Windows Phone 7 и наиболее распространенные способы настройки этих приложений.</span><span class="sxs-lookup"><span data-stu-id="fa553-110">In this section, we explore some of the types of SharePoint-powered mobile apps you can build for Windows Phone 8 and Windows Phone 7 and the most common ways to customize those applications.</span></span> <span data-ttu-id="fa553-111">SharePoint предоставляет платформу и средства для разработчиков, шаблоны проектов Visual Studio 2010, включая создание решений для мобильных устройств, которые взаимодействуют с данными SharePoint в локальных установок SharePoint и в облаке, используя SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="fa553-111">SharePoint provides a framework and tools for developers, including Visual Studio 2010 project templates, to create mobile solutions that interact with SharePoint data both in on-premises SharePoint installations and in the cloud, using SharePoint Online.</span></span> <span data-ttu-id="fa553-112">На рисунке 1 показано, как может выглядеть приложение простого списка на Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="fa553-112">Figure 1 shows how a simple list application could look on Windows Phone.</span></span>
  
    
    

<span data-ttu-id="fa553-113">**На рисунке 1. Элементы списка SharePoint в приложении Windows Phone**</span><span class="sxs-lookup"><span data-stu-id="fa553-113">**Figure 1. SharePoint list items in a Windows Phone app**</span></span>

  
    
    

  
    
    
![Элементы списка SharePoint в приложении Windows Phone](../images/9159345c-ce12-41a6-8994-fc2e9aa26fd6.gif)
  
    
    

  
    
    

  
    
    

## <a name="what-skills-do-you-need-to-create-mobile-apps"></a><span data-ttu-id="fa553-115">Какие навыки работы необходимые для создания мобильных приложений?</span><span class="sxs-lookup"><span data-stu-id="fa553-115">What skills do you need to create mobile apps?</span></span>
<span data-ttu-id="fa553-116"><a name="SP15buildmobile_needtoknow"> </a></span><span class="sxs-lookup"><span data-stu-id="fa553-116"></span></span>

<span data-ttu-id="fa553-p103">В этом разделе предполагается, что вы знакомы с SharePoint, .NET Framework, система разработки Visual Studio и Visual C#. Также полезно некоторые сравнению с Windows Phone 8 или Windows Phone 7 при разработке приложений с Silverlight и приводятся рекомендации по можно ознакомиться с XAML, StackPanel и Pivot элементы управления для Windows Phone и основные понятия, такие как деактивация, привязка данных Silverlight и т. д. Если вы не знакомы с помощью Silverlight при разработке приложений Windows Phone, рекомендуется ознакомиться со следующими ресурсами.</span><span class="sxs-lookup"><span data-stu-id="fa553-p103">In this section, we assume that you're familiar with SharePoint, the .NET Framework, the Visual Studio development system, and Visual C#. It's also good to have some experience with Windows Phone 8 or Windows Phone 7 application development using Silverlight, and it helps to be familiar with XAML, the StackPanel and Pivot controls for Windows Phone, and concepts such as tombstoning, Silverlight data binding, and so on. If you are new to Windows Phone application development using Silverlight, we recommend that you check out the following resources.</span></span>
  
    
    

-  [<span data-ttu-id="fa553-120">Разработка Windows Phone приложения от начала до конца</span><span class="sxs-lookup"><span data-stu-id="fa553-120">Developing a Windows Phone Application from Start to Finish</span></span>](http://msdn.microsoft.com/en-us/library/gg680270%28v=pandp.11%29.aspx)
    
  
-  [<span data-ttu-id="fa553-121">Пользовательский интерфейс для Windows Phone</span><span class="sxs-lookup"><span data-stu-id="fa553-121">User interface for Windows Phone</span></span>](http://msdn.microsoft.com/en-us/library/windowsphone/develop/ff967556%28v=vs.105%29.aspx)
    
  
-  [<span data-ttu-id="fa553-122">Краткое руководство: Создание пользовательского интерфейса с помощью XAML для Windows Phone</span><span class="sxs-lookup"><span data-stu-id="fa553-122">Quickstart: Creating a user interface with XAML for Windows Phone</span></span>](http://msdn.microsoft.com/en-us/library/windowsphone/develop/jj207025%28v=vs.105%29.aspx)
    
  
-  [<span data-ttu-id="fa553-123">Архитектура управления PIVOT для Windows Phone</span><span class="sxs-lookup"><span data-stu-id="fa553-123">Pivot control architecture for Windows Phone</span></span>](http://msdn.microsoft.com/en-us/library/windowsphone/develop/ff941097%28v=vs.105%29.aspx)
    
  

## <a name="development-overview-for-mobile-apps-using-sharepoint"></a><span data-ttu-id="fa553-124">Общие сведения о разработке для мобильных приложений с помощью SharePoint</span><span class="sxs-lookup"><span data-stu-id="fa553-124">Development overview for mobile apps using SharePoint</span></span>
<span data-ttu-id="fa553-125"><a name="SP15buildmobile_devoverview"> </a></span><span class="sxs-lookup"><span data-stu-id="fa553-125"></span></span>

<span data-ttu-id="fa553-126">Может создавать широкий спектр мобильных приложений с помощью SharePoint.</span><span class="sxs-lookup"><span data-stu-id="fa553-126">You can build a wide variety of mobile apps using SharePoint.</span></span> <span data-ttu-id="fa553-127">В этом разделе описаны новые или измененные выпуска SharePoint, с помощью простого разработки мобильных приложений для разработчиков.</span><span class="sxs-lookup"><span data-stu-id="fa553-127">This section describes what's new or changed in the SharePoint release that makes mobile app development simple for developers.</span></span>
  
    
    

### <a name="windows-phone-sharepoint-application-template"></a><span data-ttu-id="fa553-128">Шаблон приложения SharePoint для Windows Phone</span><span class="sxs-lookup"><span data-stu-id="fa553-128">Windows Phone SharePoint Application template</span></span>

<span data-ttu-id="fa553-129">Это простой тип мобильного приложения, которые вы можете создать для переноса регулярного списка на номер телефона.</span><span class="sxs-lookup"><span data-stu-id="fa553-129">This is the simplest type of mobile app you can build to bring a regular list to the phone.</span></span> <span data-ttu-id="fa553-130">SharePoint предоставляет шаблон Visual Studio, чтобы обеспечить возможность быстро и легко создавать приложения списка SharePoint для Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="fa553-130">SharePoint offers a Visual Studio template to enable you to quickly and easily create SharePoint list applications for the Windows Phone.</span></span> <span data-ttu-id="fa553-131">Например, можно создать «Список дел»-введите приложения Windows Phone, которое возвращает список задач из SharePoint в Windows Phone и позволяет использовать телефон для обновления состояния задач в дороге.</span><span class="sxs-lookup"><span data-stu-id="fa553-131">For example, you can build a "To Do List"-type Windows Phone application that brings your task list from SharePoint into the Windows Phone and enables the you to use your phone to update the status of a task on the go.</span></span> <span data-ttu-id="fa553-132">Другой пример возникли каталог продуктов для список в SharePoint, доступные на телефоне для сотрудников отдела продаж.</span><span class="sxs-lookup"><span data-stu-id="fa553-132">Another example is having the product catalog for an inventory list in SharePoint available on the phone for the sales people.</span></span> <span data-ttu-id="fa553-133">Установка пакета SDK SharePoint для Windows Phone предоставляет два шаблоны Windows Phone приложений SharePoint в Visual Studio 2010 или Visual Studio 2010 Express для Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="fa553-133">Installing the Windows Phone SharePoint SDK makes two Windows Phone SharePoint Application templates available to you in Visual Studio 2010 or Visual Studio 2010 Express for Windows Phone.</span></span> <span data-ttu-id="fa553-134">(Увидеть [как: Настройка среды разработки мобильных приложений для SharePoint](how-to-set-up-an-environment-for-developing-mobile-apps-for-sharepoint.md).) На основе шаблона приложения списка SharePoint для Windows Phone, можно следуйте указаниям мастера для создания приложения Windows Phone с работы, которые можно получить доступ к и работы с данными в списке SharePoint.</span><span class="sxs-lookup"><span data-stu-id="fa553-134">(See  [How to: Set up an environment for developing mobile apps for SharePoint](how-to-set-up-an-environment-for-developing-mobile-apps-for-sharepoint.md).) Using the Windows Phone SharePoint List Application template, you can follow the steps of a wizard to create a functional Windows Phone app that can access and manipulate data in a SharePoint list.</span></span>
  
    
    

### <a name="new-and-enhanced-mobility-object-model-in-sharepoint"></a><span data-ttu-id="fa553-135">Новые и усовершенствованные мобильности объектная модель в SharePoint</span><span class="sxs-lookup"><span data-stu-id="fa553-135">New and enhanced mobility object model in SharePoint</span></span>

<span data-ttu-id="fa553-136">SharePoint добавляет несколько новых классов на сервере и клиентских объектных моделей, чтобы включить сценарии мобильности SharePoint, которые мы описано ранее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="fa553-136">SharePoint adds several new classes to both the server and client object models to enable the SharePoint mobility scenarios that we described earlier in this article.</span></span>
  
    
    
<span data-ttu-id="fa553-137">Чтобы включить приложений с поддержкой местоположения, существует новые собственные класс типа поля, **SPFieldGeoLocation**вместе с несколькими связанные с ним классы для структурирования значение поля расположения и отображения их.</span><span class="sxs-lookup"><span data-stu-id="fa553-137">To enable location-aware apps, there is a new native field type class, **SPFieldGeoLocation**, along with several associated classes for structuring the value of location fields and rendering them.</span></span> <span data-ttu-id="fa553-138">Эти классы можно также вызвать в клиентской объектной модели SharePoint для Silverlight.</span><span class="sxs-lookup"><span data-stu-id="fa553-138">These classes are also callable in the SharePoint client object model for Silverlight.</span></span> <span data-ttu-id="fa553-139">Новый тип поля также есть определение добавляемого стандартных файла fldtypes.xml SharePoint и новые пользовательские элементы управления для отображения поля в формах отображения, редактирования и создания.</span><span class="sxs-lookup"><span data-stu-id="fa553-139">The new field type also has a definition added to the standard SharePoint fldtypes.xml file and new user controls for rendering the field on the Display, Edit, and New forms.</span></span> <span data-ttu-id="fa553-140">Общие сведения в разделе [Интеграция расположение и карты функциональные возможности в SharePoint](integrating-location-and-map-functionality-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="fa553-140">For an overview, see  [Integrating location and map functionality in SharePoint](integrating-location-and-map-functionality-in-sharepoint.md).</span></span> 
  
    
    
<span data-ttu-id="fa553-141">Для включения проверки подлинности SharePoint для пользователей Windows Phone, клиентская объектная модель содержит несколько связанных классов и новый класс **проверки подлинности** .</span><span class="sxs-lookup"><span data-stu-id="fa553-141">To enable SharePoint authentication for Windows Phone users, the client object model includes a new **Authenticator** class and several associated classes.</span></span> <span data-ttu-id="fa553-142">Дополнительные сведения см [Обзор объектной модели SharePoint мобильного клиента проверки подлинности](overview-of-the-sharepoint-mobile-client-authentication-object-model.md).</span><span class="sxs-lookup"><span data-stu-id="fa553-142">For an overview, see [Overview of the SharePoint mobile client authentication object model](overview-of-the-sharepoint-mobile-client-authentication-object-model.md).</span></span>
  
    
    
<span data-ttu-id="fa553-143">Чтобы включить автоматическое уведомлений для пользователей Windows Phone событий в ферме SharePoint, серверной объектной модели включает несколько новых классов, каждый из которых также может быть вызван из клиентской объектной модели.</span><span class="sxs-lookup"><span data-stu-id="fa553-143">To enable automatic notifications to Windows Phone users of events on a SharePoint farm, the server object model includes several new classes, each of which is also callable from the client object model.</span></span> <span data-ttu-id="fa553-144">Эти классы содержат методы, позволяющие телефона приложений для регистрации для уведомлений об указанных типов событий приложений SharePoint server.</span><span class="sxs-lookup"><span data-stu-id="fa553-144">These classes include methods that enable phone apps to register with SharePoint server apps for notifications about specified types of events.</span></span> <span data-ttu-id="fa553-145">Существуют также методы, которые используют серверные приложения для отправки уведомления о зарегистрированных подписчикам.</span><span class="sxs-lookup"><span data-stu-id="fa553-145">There are also methods that the server apps use to send notifications to registered subscribers.</span></span> <span data-ttu-id="fa553-146">Обзор перейдите в раздел [Create приложения списка SharePoint для Windows Phone для приема push-уведомлений](how-to-configure-and-use-push-notifications-in-sharepoint-apps-for-windows.md#BKMK_NotificationPhoneApp).</span><span class="sxs-lookup"><span data-stu-id="fa553-146">For an overview, see  [Create a Windows Phone SharePoint list app to receive push notifications](how-to-configure-and-use-push-notifications-in-sharepoint-apps-for-windows.md#BKMK_NotificationPhoneApp).</span></span>
  
    
    
<span data-ttu-id="fa553-147">С помощью SharePoint можно не только для разработки мобильных приложений для Windows Phone 8 и Windows Phone 7.</span><span class="sxs-lookup"><span data-stu-id="fa553-147">With SharePoint, you're not limited to mobile app development just for Windows Phone 8 and Windows Phone 7.</span></span> <span data-ttu-id="fa553-148">С программирования интерфейс и новых представлений состояния (REST) интерфейс программирования предоставлено SharePoint JavaScript можно создавать приложения для мобильных устройств, отличных от Windows Phone; могут взаимодействовать с сайтами SharePoint, используя JavaScript, который выполняется в качестве скрипты в браузере или удаленно с помощью любая технология, которая поддерживает стандартные возможности REST.</span><span class="sxs-lookup"><span data-stu-id="fa553-148">With the JavaScript programming interface and the new Representational State Transfer (REST) programming interface provided by SharePoint, you can create applications for non-Windows Phone mobile devices; you can interact with SharePoint sites by using JavaScript that executes as scripts in the browser, or remotely by using any technology that supports standard REST capabilities.</span></span> <span data-ttu-id="fa553-149">Следующий раздел Обзор программных интерфейсов REST и JavaScript.</span><span class="sxs-lookup"><span data-stu-id="fa553-149">The following section provides an overview of the REST and JavaScript programming interfaces.</span></span>
  
    
    

#### <a name="ecmascript-javascript-jscript-object-model-architecture"></a><span data-ttu-id="fa553-150">Архитектура объектной модели ECMAScript (JavaScript, JScript)</span><span class="sxs-lookup"><span data-stu-id="fa553-150">ECMAScript (JavaScript, JScript) object model architecture</span></span>

<span data-ttu-id="fa553-151">SharePoint Foundation 2010 представлено клиентских объектных моделей, которые включены разработчиков выполнение удаленной связи с SharePoint с помощью веб-программирования технологии выбранного: .NET Framework, Silverlight и JavaScript.</span><span class="sxs-lookup"><span data-stu-id="fa553-151">SharePoint Foundation 2010 introduced the client object models, which enabled developers to perform remote communication with SharePoint by using the web programming technology of their choice: the .NET Framework, Silverlight, or JavaScript.</span></span>
  
    
    
<span data-ttu-id="fa553-p110">В SharePoint Foundation 2010 клиентских объектных моделей предоставляют API, которые позволяют разработчикам взаимодействовать с сайтами SharePoint из скрипта, который выполняется в браузере, из кода (на основе .NET Framework 3.5 или более поздней версии), который выполняется в .NET Framework управляемых приложений или из кода, выполняющегося в приложении Silverlight 2.0. Прокси-сервер с расширением js и управляемых DLL-файлы, которые составляют объектные модели клиента основанные на веб-службы client.svc и обработки эффективной сериализации пакетной обработки, запросов и синтаксический анализ для ответов. На рисунке 2 показана высокоуровневая архитектура клиентских объектных моделей SharePoint.</span><span class="sxs-lookup"><span data-stu-id="fa553-p110">In SharePoint Foundation 2010, the client object models provide APIs that enable developers to interact with SharePoint sites from script that executes in the browser, from code (based on the .NET Framework 3.5 or later) that executes in a .NET Framework-managed application, or from code that executes in a Silverlight 2.0 application. The proxy .js and managed .dll files that compose the client object models are built on the client.svc web service, and handle the effective batching, serialization of requests, and parsing of replies. Figure 2 shows a high-level view of the SharePoint client object model architecture.</span></span>
  
    
    

<span data-ttu-id="fa553-155">**На рисунке 2. Архитектура объектной модели клиента SharePoint**</span><span class="sxs-lookup"><span data-stu-id="fa553-155">**Figure 2. SharePoint client object model architecture**</span></span>

  
    
    

  
    
    
![Архитектура клиентских объектных моделей SharePoint](../images/SP15Con_BuildSharePointAppsForMobileDevices_Fig3.png)
  
    
    
<span data-ttu-id="fa553-157">Чтобы сведения об использовании клиентской объектной модели JavaScript с данными SharePoint, перейдите в раздел  [ECMAScript клиентской объектной модели](http://channel9.msdn.com/learn/courses/SharePoint2010Developer/ClientObjectModel/ECMAScriptClientObjectModel)</span><span class="sxs-lookup"><span data-stu-id="fa553-157">To learn how to use the JavaScript client object model against SharePoint data, see  [ECMAScript Client Object Model](http://channel9.msdn.com/learn/courses/SharePoint2010Developer/ClientObjectModel/ECMAScriptClientObjectModel)</span></span>
  
    
    

#### <a name="rest-endpoints-in-sharepoint"></a><span data-ttu-id="fa553-158">Конечные точки REST в SharePoint</span><span class="sxs-lookup"><span data-stu-id="fa553-158">REST endpoints in SharePoint</span></span>

<span data-ttu-id="fa553-159">Чтобы использовать возможности REST, которые встроены в SharePoint, можно создать RESTful HTTP-запросов с использованием стандарта Open Data Protocol (OData), соответствующий API желаемую клиентской объектной модели.</span><span class="sxs-lookup"><span data-stu-id="fa553-159">To use the REST capabilities that are built into SharePoint, you can construct a RESTful HTTP request using the Open Data Protocol (OData) standard that corresponds to the desired client object model API.</span></span> <span data-ttu-id="fa553-160">Веб-службы client.svc обрабатывает HTTP-запрос и обслуживает соответствующий ответ в формате Atom или JavaScript Object Notation (JSON).</span><span class="sxs-lookup"><span data-stu-id="fa553-160">The client.svc web service handles the HTTP request and serves the appropriate response, in either Atom or JavaScript Object Notation (JSON) format.</span></span> <span data-ttu-id="fa553-161">Клиентское приложение затем необходимо выполнить синтаксический анализ этого ответа.</span><span class="sxs-lookup"><span data-stu-id="fa553-161">The client application must then parse that response.</span></span> <span data-ttu-id="fa553-162">На рисунке 3 показано высокоуровневое представление архитектуры SharePoint REST.</span><span class="sxs-lookup"><span data-stu-id="fa553-162">Figure 3 shows a high-level view of the SharePoint REST architecture.</span></span>
  
    
    

<span data-ttu-id="fa553-163">**На рисунке 3. Архитектура SharePoint REST**</span><span class="sxs-lookup"><span data-stu-id="fa553-163">**Figure 3. SharePoint REST architecture**</span></span>

  
    
    

  
    
    
![Архитектура REST SharePoint](../images/SP15Con_BuildSharePointAppsForMobileDevices_Fig2.png)
  
    
    
<span data-ttu-id="fa553-165">На данный момент службы REST в SharePoint доступен только для чтения.</span><span class="sxs-lookup"><span data-stu-id="fa553-165">Currently, the REST service in SharePoint is read-only.</span></span> <span data-ttu-id="fa553-166">То есть доступны только конечные точки REST, которые представляют операции HTTP GET</span><span class="sxs-lookup"><span data-stu-id="fa553-166">That is, only REST endpoints that represent an HTTP GET operation are available</span></span>
  
    
    
<span data-ttu-id="fa553-167">По умолчанию ответы службы SharePoint REST форматируются с помощью протокола Atom спецификации OData.</span><span class="sxs-lookup"><span data-stu-id="fa553-167">By default, the SharePoint REST service responses are formatted using the Atom protocol, according to the OData specification.</span></span> <span data-ttu-id="fa553-168">Кроме того служба REST поддерживает заголовков HTTP Accept, которые позволяют разработчикам указать, что ответ возвращается в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="fa553-168">In addition, the REST service supports HTTP Accept headers that enable developers to specify that the response is returned in JSON format.</span></span> <span data-ttu-id="fa553-169">Для получения дополнительных сведений о служб REST в SharePoint, видеть [операции запросов OData используется в запросах SharePoint REST](http://msdn.microsoft.com/library/d4b5c277-ed50-420c-8a9b-860342284b72%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="fa553-169">To learn more about REST services in SharePoint, see  [Use OData query operations in SharePoint REST requests](http://msdn.microsoft.com/library/d4b5c277-ed50-420c-8a9b-860342284b72%28Office.15%29.aspx).</span></span>
  
    
    
<span data-ttu-id="fa553-170">Службы SharePoint REST поддерживает следующие операторы запросов OData.</span><span class="sxs-lookup"><span data-stu-id="fa553-170">The SharePoint REST service supports the following OData query operators:</span></span>
  
    
    

- <span data-ttu-id="fa553-171">Фильтр</span><span class="sxs-lookup"><span data-stu-id="fa553-171">Filter</span></span>
    
  
- <span data-ttu-id="fa553-172">Перевод</span><span class="sxs-lookup"><span data-stu-id="fa553-172">Take</span></span>
    
  
- <span data-ttu-id="fa553-173">expand</span><span class="sxs-lookup"><span data-stu-id="fa553-173">Expand</span></span>
    
  

## <a name="start-developing-mobile-apps-for-sharepoint"></a><span data-ttu-id="fa553-174">Начало разработки мобильных приложений для SharePoint</span><span class="sxs-lookup"><span data-stu-id="fa553-174">Start developing mobile apps for SharePoint</span></span>
<span data-ttu-id="fa553-175"><a name="SP15buildmobile_start"> </a></span><span class="sxs-lookup"><span data-stu-id="fa553-175"></span></span>

<span data-ttu-id="fa553-176">Следующие руководства и обзоры подробно определенные сведения, необходимые для разработки мобильных приложений:</span><span class="sxs-lookup"><span data-stu-id="fa553-176">The following how-tos and overviews delve into the specific information you need to start your mobile app development:</span></span>
  
    
    

-  [<span data-ttu-id="fa553-177">Как: Настройка среды разработки мобильных приложений для SharePoint</span><span class="sxs-lookup"><span data-stu-id="fa553-177">How to: Set up an environment for developing mobile apps for SharePoint</span></span>](how-to-set-up-an-environment-for-developing-mobile-apps-for-sharepoint.md)
    
  
-  [<span data-ttu-id="fa553-178">Обзор шаблонов приложений Windows Phone SharePoint в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="fa553-178">Overview of Windows Phone SharePoint application templates in Visual Studio</span></span>](overview-of-windows-phone-sharepoint-application-templates-in-visual-studio.md)
    
  
-  [<span data-ttu-id="fa553-179">Архитектура шаблона приложения списка SharePoint для Windows Phone</span><span class="sxs-lookup"><span data-stu-id="fa553-179">Architecture of the Windows Phone SharePoint List Application template</span></span>](architecture-of-the-windows-phone-sharepoint-list-application-template.md)
    
  
-  [<span data-ttu-id="fa553-180">Как: Создание приложения списка Windows Phone SharePoint</span><span class="sxs-lookup"><span data-stu-id="fa553-180">How to: Create a Windows Phone SharePoint list app</span></span>](how-to-create-a-windows-phone-sharepoint-list-app.md)
    
  
-  [<span data-ttu-id="fa553-181">Как: хранения и извлечения SharePoint списка элементов на ОС Windows Phone</span><span class="sxs-lookup"><span data-stu-id="fa553-181">How to: Store and retrieve SharePoint list items on a Windows Phone</span></span>](how-to-store-and-retrieve-sharepoint-list-items-on-a-windows-phone.md)
    
  
-  [<span data-ttu-id="fa553-182">Как: реализация бизнес-логики и данных проверок в приложении Windows Phone для SharePoint</span><span class="sxs-lookup"><span data-stu-id="fa553-182">How to: Implement business logic and data validation in a Windows Phone app for SharePoint</span></span>](how-to-implement-business-logic-and-data-validation-in-a-windows-phone-app-for-s.md)
    
  
-  [<span data-ttu-id="fa553-183">Как: поддержка и convert SharePoint полей типов для приложения для Windows Phone</span><span class="sxs-lookup"><span data-stu-id="fa553-183">How to: Support and convert SharePoint field types for Windows Phone apps</span></span>](how-to-support-and-convert-sharepoint-field-types-for-windows-phone-apps.md)
    
  
-  [<span data-ttu-id="fa553-184">Как: Настройка запросов элементов списка и фильтрация данных для приложения для Windows Phone</span><span class="sxs-lookup"><span data-stu-id="fa553-184">How to: Customize list item queries and filter data for Windows Phone apps</span></span>](how-to-customize-list-item-queries-and-filter-data-for-windows-phone-apps.md)
    
  
-  [<span data-ttu-id="fa553-185">Как: Настройка пользовательского интерфейса приложения списка SharePoint для Windows Phone</span><span class="sxs-lookup"><span data-stu-id="fa553-185">How to: Customize the user interface of a SharePoint list app for Windows Phone</span></span>](how-to-customize-the-user-interface-of-a-sharepoint-list-app-for-windows-ph.md)
    
  
-  [<span data-ttu-id="fa553-186">Способ: использование нескольких SharePoint спискам в приложении Windows Phone</span><span class="sxs-lookup"><span data-stu-id="fa553-186">How to: Use multiple SharePoint lists in a Windows Phone app</span></span>](how-to-use-multiple-sharepoint-lists-in-a-windows-phone-app.md)
    
  
-  [<span data-ttu-id="fa553-187">Как: Настройка и использование push-уведомлений в SharePoint приложений для Windows Phone</span><span class="sxs-lookup"><span data-stu-id="fa553-187">How to: Configure and use push notifications in SharePoint apps for Windows Phone</span></span>](how-to-configure-and-use-push-notifications-in-sharepoint-apps-for-windows.md)
    
  
-  [<span data-ttu-id="fa553-188">Интеграция расположение и карты функциональные возможности в SharePoint</span><span class="sxs-lookup"><span data-stu-id="fa553-188">Integrating location and map functionality in SharePoint</span></span>](integrating-location-and-map-functionality-in-sharepoint.md)
    
  
-  [<span data-ttu-id="fa553-189">Как: Создание мобильных приложений в SharePoint, содержащую данные из внешнего источника данных</span><span class="sxs-lookup"><span data-stu-id="fa553-189">How to: Create a mobile app in SharePoint that contains data from an external data source</span></span>](how-to-create-a-mobile-app-in-sharepoint-that-contains-data-from-an-externa.md)
    
  
-  [<span data-ttu-id="fa553-190">Как: интеграция карт с помощью приложения для Windows Phone и списки SharePoint</span><span class="sxs-lookup"><span data-stu-id="fa553-190">How to: Integrate maps with Windows Phone apps and SharePoint lists</span></span>](how-to-integrate-maps-with-windows-phone-apps-and-sharepoint-lists.md)
    
  
-  [<span data-ttu-id="fa553-191">Как: создание на основе механизмов поиска мобильных приложений с помощью интерфейсов навигации и REST ведение журнала событий</span><span class="sxs-lookup"><span data-stu-id="fa553-191">How to: Build search-driven mobile apps with the Navigation and Event Logging REST interfaces</span></span>](how-to-build-search-driven-mobile-apps-with-the-navigation-and-event-logging-res.md)
    
  

## <a name="additional-resources"></a><span data-ttu-id="fa553-192">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="fa553-192">Additional resources</span></span>
<span data-ttu-id="fa553-193"><a name="SP15buildmobile_addlresources"> </a></span><span class="sxs-lookup"><span data-stu-id="fa553-193"></span></span>


  
    
    

-  [<span data-ttu-id="fa553-194">Модели программирования в SharePoint</span><span class="sxs-lookup"><span data-stu-id="fa553-194">Programming models in SharePoint</span></span>](programming-models-in-sharepoint.md)
    
  
-  [<span data-ttu-id="fa553-195">Как: Настройка среды разработки мобильных приложений для SharePoint</span><span class="sxs-lookup"><span data-stu-id="fa553-195">How to: Set up an environment for developing mobile apps for SharePoint</span></span>](how-to-set-up-an-environment-for-developing-mobile-apps-for-sharepoint.md)
    
  
-  [<span data-ttu-id="fa553-196">Windows Phone SDK 8.0</span><span class="sxs-lookup"><span data-stu-id="fa553-196">Windows Phone SDK 8.0</span></span>](http://www.microsoft.com/en-us/download/details.aspx?id=35471)
    
  
-  [<span data-ttu-id="fa553-197">Пакет SDK Microsoft SharePoint для Windows Phone 8</span><span class="sxs-lookup"><span data-stu-id="fa553-197">Microsoft SharePoint SDK for Windows Phone 8</span></span>](http://www.microsoft.com/en-us/download/details.aspx?id=36818)
    
  
-  [<span data-ttu-id="fa553-198">Пакет SDK для Windows Phone 7.1</span><span class="sxs-lookup"><span data-stu-id="fa553-198">Windows Phone SDK 7.1</span></span>](http://www.microsoft.com/en-us/download/details.aspx?id=27570)
    
  
-  [<span data-ttu-id="fa553-199">Пакет SDK Microsoft SharePoint для Windows Phone 7.1</span><span class="sxs-lookup"><span data-stu-id="fa553-199">Microsoft SharePoint SDK for Windows Phone 7.1</span></span>](http://www.microsoft.com/en-us/download/details.aspx?id=30476)
    
  
-  [<span data-ttu-id="fa553-200">О Expression Blend</span><span class="sxs-lookup"><span data-stu-id="fa553-200">About Expression Blend</span></span>](http://msdn.microsoft.com/en-us/library/cc296376%28Expression.40%29.aspx)
    
  

