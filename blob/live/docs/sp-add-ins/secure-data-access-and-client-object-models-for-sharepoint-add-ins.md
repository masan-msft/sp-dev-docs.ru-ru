---
title: "Безопасный доступ к данным и клиентские объектные модели для надстроек SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: f58b7ccfdd775b9378c5cf4f8a36ca14b12709b3
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="secure-data-access-and-client-object-models-for-sharepoint-add-ins"></a><span data-ttu-id="6b9a2-102">Безопасный доступ к данным и клиентские объектные модели для надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="6b9a2-102">Secure data access and client object models for SharePoint Add-ins</span></span>
<span data-ttu-id="6b9a2-103">В этой статье рассказывается о вариантах доступа к данным, которые вы можете использовать при создании надстроек SharePoint (включая варианты подключения для доступа к данным в SharePoint и во внешних системах) и об API, которые можно использовать при доступе к данным из надстройки.</span><span class="sxs-lookup"><span data-stu-id="6b9a2-103">Learn about the data access options you have when you build SharePoint Add-ins, including connectivity options for accessing data on SharePoint and on external systems, as well as the APIs that are available when you want to access data from your add-in.</span></span>
 

 <span data-ttu-id="6b9a2-p101">**Примечание.** В настоящее время идет процесс замены названия "приложения для SharePoint" названием "надстройки SharePoint". Во время этого процесса в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio может по-прежнему использоваться термин "приложения для SharePoint". Дополнительные сведения см. в статье [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="6b9a2-p101">**Note**  The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see  [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span></span>
 

<span data-ttu-id="6b9a2-p102">При оценке вариантов доступа к данным для надстроек SharePoint вам потребуется оценить среду своей надстройки и учесть несколько факторов, например канал связи между клиентом и сервером, а также необходимый уровень разрешений, чтобы ваша надстройка могла выполнять поставленные перед ней задачи. Кроме того, вам придется оценить API, доступные в модели для надстроек SharePoint Add.</span><span class="sxs-lookup"><span data-stu-id="6b9a2-p102">In evaluating your data access options for SharePoint Add-ins, you have to assess your add-in environment and consider several factors, such as communication between the client and server, and the permission level that is required for your add-in to perform the required tasks. You also have to evaluate the APIs that are available in the model for SharePoint Add-ins.</span></span>
 

## <a name="high-level-overview-of-data-in-sharepoint-add-ins"></a><span data-ttu-id="6b9a2-109">Общие сведения о данных в надстройках SharePoint</span><span class="sxs-lookup"><span data-stu-id="6b9a2-109">High-level overview of data in SharePoint Add-ins</span></span>
<span data-ttu-id="6b9a2-110"><a name="SP15_dataaccessoptions_considerations"> </a></span><span class="sxs-lookup"><span data-stu-id="6b9a2-110"><a name="SP15_dataaccessoptions_considerations"> </a></span></span>

<span data-ttu-id="6b9a2-p103">Трудно представить себе Надстройка SharePoint (или, собственно говоря, любую надстройку), которой не требуется запрашивать, хранить данные или управлять ими. При работе с надстройкой часто требуется извлекать данные SharePoint и управлять ими, включая элементы в библиотеках документов и списках, метаданные и профили пользователей. Кроме того, могут возникать сценарии, в которых необходимо получать доступ к внешним данным, в вашей надстройке. Модель для надстроек SharePoint предоставляет несколько вариантов подключения и обширный набор API-интерфейсов для доступа к полноформатным данным и службам, которые находятся в SharePoint и во внешних системах.</span><span class="sxs-lookup"><span data-stu-id="6b9a2-p103">It is hard to imagine a SharePoint Add-in (or any add-in for that matter) that does not need to query, store, or manipulate data. In your add-in, you will frequently have to retrieve and manipulate SharePoint data, such as items in document libraries and lists, metadata, or user profiles. Similarly, you might have scenarios where you need to access external data in your add-in. The model for SharePoint Add-ins provides multiple connectivity options and a rich set of APIs for accessing the data and services that reside on SharePoint and on external systems.</span></span>
 

 
<span data-ttu-id="6b9a2-115">Когда вы разрабатываете свою надстройку и планируете доступ к данным, необходимо принять два ключевых решения:</span><span class="sxs-lookup"><span data-stu-id="6b9a2-115">As you design your add-in and plan for data access, you have to make two key decisions:</span></span>
 

 

1. <span data-ttu-id="6b9a2-116">Какой вариант подключения следует использовать?</span><span class="sxs-lookup"><span data-stu-id="6b9a2-116">Which connectivity option should I use?</span></span>
    
 
2. <span data-ttu-id="6b9a2-117">Какие API-интерфейсы следует использовать для доступа к необходимым данным?</span><span class="sxs-lookup"><span data-stu-id="6b9a2-117">What APIs should I use for accessing the data I need?</span></span>
    
 
<span data-ttu-id="6b9a2-118">На следующих рисунках приведена сводная информация о различных вариантах, которые предоставляются Модель для надстроек SharePoint. В следующих разделах мы подробно рассмотрим каждый вариант и узнаем, когда следует их использовать.</span><span class="sxs-lookup"><span data-stu-id="6b9a2-118">The following figures summarize the different options that are provided by the model for SharePoint Add-ins. In the sections that follow, you will examine each option in detail and learn when to use them.</span></span>
 

 
<span data-ttu-id="6b9a2-p104">На рис. 1 представлены имеющиеся в наличии варианты для доступа к данным SharePoint из надстройки. При работе с этими сценариями необходимо выбрать способ проверки подлинности и связи с SharePoint: с использованием (1) OAuth или (2)междоменной библиотеки. Затем, когда речь идет об API-интерфейсе доступа к данным, необходимо выбрать между (3) клиентской объектной моделью (клиентские объектные модели JavaScript/.NET) или (4)службой REST.</span><span class="sxs-lookup"><span data-stu-id="6b9a2-p104">Figure 1 illustrates the options you have for accessing SharePoint data in your add-in. When you are dealing with these scenarios, you have to decide whether you want to authenticate and communicate to SharePoint by using (1) OAuth, or (2) the cross-domain library. Then, for the data access API, you must decide between (3) the client object model (JavaScript/.NET client object models), or (4) Representational State Transfer (REST).</span></span>
 

 
<span data-ttu-id="6b9a2-122">Помните, что вы также можете получить доступ к определенным данным с помощью (5)  *удаленных приемников событий*  , однако основной сценарий для удаленных приемников событий удаленное выполнение кода.</span><span class="sxs-lookup"><span data-stu-id="6b9a2-122">Keep in mind that you can also access certain data using (5)  *remote event receivers*  , however, the main scenario for remote event receivers is remote code execution.</span></span>
 

 

<span data-ttu-id="6b9a2-123">**Рис. 1. Варианты использования данных SharePoint в надстройке**</span><span class="sxs-lookup"><span data-stu-id="6b9a2-123">**Figure 1. Options for using SharePoint data in your add-in**</span></span>

 

 
![Варианты использования данных SharePoint в надстройке](../images/DataAccess_SharePointData.png)
 
<span data-ttu-id="6b9a2-p105">На рис. 2 представлены варианты доступа к внешним данным в надстройке. При работе с этими сценариями необходимо выбрать использование (1)  *веб-прокси*  , (2) *внешних типов контента*  или (3) *междоменной библиотеки с пользовательской прокси-страницей*  для проверки подлинности и взаимодействия с внешними службами или системами. Также можно использовать (4)клиентскую объектную модель (клиентские объектные модели JavaScript или .NET) или (5)REST.</span><span class="sxs-lookup"><span data-stu-id="6b9a2-p105">Figure 2 shows the options that you have for accessing external data on your add-in. When you are working with these scenarios, you have to decide whether you want to use (1) the  *web proxy*  , (2) *external content types*  , or (3) the *cross-domain library with a custom proxy page*  to authenticate and communicate with external services or systems. You can also use (4) theclient object model (JavaScript/.NET client object models), or (5) Representational State Transfer (REST).</span></span>
 

 

<span data-ttu-id="6b9a2-128">**Рис. 2. Варианты использования внешних данных в надстройке**</span><span class="sxs-lookup"><span data-stu-id="6b9a2-128">**Figure 2. Options for using external data in your add-in**</span></span>

 

 
![Варианты использования внешних данных в надстройке](../images/5950bc8a-ed73-4f14-b616-a88c14c4fe56.png)
 

 

 

## <a name="data-connectivity-options-for-sharepoint-add-ins"></a><span data-ttu-id="6b9a2-130">Варианты подключения к данным для надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="6b9a2-130">Data connectivity options for SharePoint Add-ins</span></span>
<span data-ttu-id="6b9a2-131"><a name="SP15_dataaccessoptions_connectivity"> </a></span><span class="sxs-lookup"><span data-stu-id="6b9a2-131"><a name="SP15_dataaccessoptions_connectivity"> </a></span></span>

<span data-ttu-id="6b9a2-p106">При работе с данными в надстройке следует учитывать ряд аспектов. Например, какой маршрут используется для передачи данных? Передаются ли данные с сервера или проходят через него? Проходят ли данные через клиента? Можно ли проходить проверку подлинности в качестве пользователя, вошедшего в систему? Требуются ли надстройке повышенные полномочия? Следующие разделы помогут вам ответить на эти и другие вопросы, которые могут у вас возникнуть.</span><span class="sxs-lookup"><span data-stu-id="6b9a2-p106">You have to consider several aspects when you work with data in your add-in. For example, what route is the data using? Is it coming from or going through the server? Is it going through the client? Is it OK to authenticate as the logged-on user? Does the add-in need elevated privileges? The following sections can help you with these and other questions you may have.</span></span>
 

 

### <a name="sharepoint-data-connectivity"></a><span data-ttu-id="6b9a2-139">Возможности подключения к данным SharePoint</span><span class="sxs-lookup"><span data-stu-id="6b9a2-139">SharePoint data connectivity</span></span>

<span data-ttu-id="6b9a2-140">Указанные ниже варианты подключения можно использовать при доступе к данным SharePoint (см. рис. 1).</span><span class="sxs-lookup"><span data-stu-id="6b9a2-140">The following connectivity options are available when accessing SharePoint data (see Figure 1):</span></span>
 

 

-  <span data-ttu-id="6b9a2-p107">**OAuth:** открытый протокол, который позволяет выполнять безопасную авторизацию простым и стандартным способом. OAuth позволяет пользователям утверждать заявки на выполнение действий от их имени без раскрытия имени пользователя и пароля. Вы можете использовать OAuth с серверным кодом. Это отличный вариант, если необходимо выполнять неинтерактивный процесс или повышать привилегии, предоставляя вошедшему в систему пользователю расширенные полномочия. Для получения информации о OAuth см. [Авторизация и проверка подлинности для надстроек в SharePoint](authorization-and-authentication-of-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="6b9a2-p107">**OAuth:** An open protocol that enables secure authorization in a simple and standard way. OAuth enables users to approve an application to act on their behalf without sharing their user name and password. You can use OAuth with server-side code. It is a good option if you need to run a non-interactive process, or if you need to elevate privileges to other than those of the logged-on user. For information about OAuth, see [Authorization and authentication of SharePoint Add-ins](authorization-and-authentication-of-sharepoint-add-ins.md).</span></span>
    
 
-  <span data-ttu-id="6b9a2-p108">**Междоменная библиотека:** клиентская альтернатива в форме файла JavaScript ( **SP.RequestExecutor.js** ), который размещается на веб-сайте SharePoint и ссылку на который может содержать удаленная надстройка. Междоменная библиотека позволяет взаимодействовать с несколькими доменами на удаленной странице надстройки через прокси-сервер. Это отличный вариант, если вы предпочитаете, чтобы код надстройки выполнялся в клиенте, а не на сервере, или если существуют препятствия для подключения, такие как брандмауэры, между SharePoint и удаленной инфраструктурой. Дополнительные сведения см. в статье [Обращение к данным SharePoint из надстроек с помощью междоменной библиотеки](access-sharepoint-data-from-add-ins-using-the-cross-domain-library.md).</span><span class="sxs-lookup"><span data-stu-id="6b9a2-p108">**Cross-domain library:** A client-side alternative in the form of a JavaScript file ( **SP.RequestExecutor.js** ) hosted in the SharePoint website that you can reference in your remote add-in. The cross-domain library allows you to interact with more than one domain in your remote add-in page through a proxy. This is a good option if you prefer your add-in code to run in the client rather than in the server, or if there are connectivity barriers, such as firewalls, between SharePoint and your remote infrastructure. For more information, see [Access SharePoint data from add-ins using the cross-domain library](access-sharepoint-data-from-add-ins-using-the-cross-domain-library.md).</span></span>
    
 
-  <span data-ttu-id="6b9a2-p109">**Приемники удаленных событий.** Они обрабатывают события, которые происходят с элементом в надстройке (например, это может быть список, элемент списка или веб-страница). Эти события похожи на события в традиционном решении SharePoint, однако поддерживают также работу с удаленными компонентами Надстройка SharePoint. Обратите внимание на то, что некоторые свойства элемента доступны приемнику удаленных событий. Дополнительные сведения см. в статье [Создание удаленного приемника событий в надстройках SharePoint](create-a-remote-event-receiver-in-sharepoint-add-ins.md). Аналогичным образом с помощью приемников событий можно настраивать установку, обновление и удаление надстройки. Дополнительные сведения см. в статье  [Создание приемника событий надстройки в надстройках для SharePoint](create-an-add-in-event-receiver-in-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="6b9a2-p109">**Remote event receivers:** You can use remote event receivers to handle events that occur to an item in the add-in, such as a list, a list item, or a web. These events resemble those in a traditional SharePoint solution, except that they can work with the remote components of the SharePoint Add-in. Note that some properties of the item are available to the remote event receiver. For more information, see [Create a remote event receiver in SharePoint Add-ins](create-a-remote-event-receiver-in-sharepoint-add-ins.md). In a similar way, you can use add-in event receivers to customize how your add-in is installed, updated, and uninstalled. For more information, see  [Create an add-in event receiver in SharePoint Add-ins](create-an-add-in-event-receiver-in-sharepoint-add-ins.md).</span></span>
    
 

### <a name="sharepoint-data-connectivity-options-which-one-should-i-use"></a><span data-ttu-id="6b9a2-155">Варианты подключения к данным SharePoint: выбор подходящего варианта</span><span class="sxs-lookup"><span data-stu-id="6b9a2-155">SharePoint data connectivity options: Which one should I use?</span></span>

<span data-ttu-id="6b9a2-156">В таблице ниже перечислены стандартные требования и сценарии, с которыми вы можете столкнуться при создании надстроек. Знак **x** в столбце указывает, какой вариант вы можете использовать в каждом случае.</span><span class="sxs-lookup"><span data-stu-id="6b9a2-156">The following table lists the common requirements and scenarios you might encounter when you are building add-ins. An  **x** in the column indicates which option you can use in each case.</span></span>
 

 

<span data-ttu-id="6b9a2-157">**Табл. 1. Варианты подключения к данным SharePoint**</span><span class="sxs-lookup"><span data-stu-id="6b9a2-157">**Table 1. SharePoint data connectivity options**</span></span>


|<span data-ttu-id="6b9a2-158">**Требование или сценарий**</span><span class="sxs-lookup"><span data-stu-id="6b9a2-158">**Requirement/Scenario**</span></span>|<span data-ttu-id="6b9a2-159">**OAuth**</span><span class="sxs-lookup"><span data-stu-id="6b9a2-159">**OAuth**</span></span>|<span data-ttu-id="6b9a2-160">**Междоменная библиотека**</span><span class="sxs-lookup"><span data-stu-id="6b9a2-160">**Cross-domain library**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="6b9a2-161">Я использую клиентские технологии (HTML и JavaScript).</span><span class="sxs-lookup"><span data-stu-id="6b9a2-161">I use client-side technologies (HTML + JavaScript).</span></span>||<span data-ttu-id="6b9a2-162">x</span><span class="sxs-lookup"><span data-stu-id="6b9a2-162">x</span></span>|
|<span data-ttu-id="6b9a2-163">Я хочу использовать интерфейсы REST.</span><span class="sxs-lookup"><span data-stu-id="6b9a2-163">I want to use REST interfaces.</span></span>|<span data-ttu-id="6b9a2-164">x</span><span class="sxs-lookup"><span data-stu-id="6b9a2-164">x</span></span>|<span data-ttu-id="6b9a2-165">x</span><span class="sxs-lookup"><span data-stu-id="6b9a2-165">x</span></span>|
|<span data-ttu-id="6b9a2-166">Между SharePoint и удаленной надстройкой имеется брандмауэр, и необходимо осуществлять вызовы через браузер.</span><span class="sxs-lookup"><span data-stu-id="6b9a2-166">There is a firewall between SharePoint and my remote add-in, and I need to issue the calls through the browser.</span></span>||<span data-ttu-id="6b9a2-167">x</span><span class="sxs-lookup"><span data-stu-id="6b9a2-167">x</span></span>|
|<span data-ttu-id="6b9a2-168">Надстройка должна осуществлять доступ к ресурсам как вошедший в систему пользователь.</span><span class="sxs-lookup"><span data-stu-id="6b9a2-168">My add-in needs to access resources as the logged-on user.</span></span>|<span data-ttu-id="6b9a2-169">x</span><span class="sxs-lookup"><span data-stu-id="6b9a2-169">x</span></span>|<span data-ttu-id="6b9a2-170">x</span><span class="sxs-lookup"><span data-stu-id="6b9a2-170">x</span></span>|
|<span data-ttu-id="6b9a2-171">Надстройка должна повышать уровень разрешений, предоставляя вошедшему в систему пользователю расширенные полномочия.</span><span class="sxs-lookup"><span data-stu-id="6b9a2-171">My add-in needs to elevate privileges to other than those of the current logged-on user.</span></span>|<span data-ttu-id="6b9a2-172">x</span><span class="sxs-lookup"><span data-stu-id="6b9a2-172">x</span></span>||
|<span data-ttu-id="6b9a2-173">Надстройка должна действовать от имени пользователя, отличного от пользователя, который вошел в систему.</span><span class="sxs-lookup"><span data-stu-id="6b9a2-173">My add-in needs to act on behalf of a user other than the one who is logged on.</span></span>|<span data-ttu-id="6b9a2-174">x</span><span class="sxs-lookup"><span data-stu-id="6b9a2-174">x</span></span>||
|<span data-ttu-id="6b9a2-175">Надстройка должна выполнять операции только в том случае, если пользователь вошел в систему.</span><span class="sxs-lookup"><span data-stu-id="6b9a2-175">My add-in needs to perform operations only while the user is logged on.</span></span>|<span data-ttu-id="6b9a2-176">x</span><span class="sxs-lookup"><span data-stu-id="6b9a2-176">x</span></span>|<span data-ttu-id="6b9a2-177">x</span><span class="sxs-lookup"><span data-stu-id="6b9a2-177">x</span></span>|
|<span data-ttu-id="6b9a2-178">Надстройка должна выполнять операции, даже если пользователь не вошел в систему.</span><span class="sxs-lookup"><span data-stu-id="6b9a2-178">My add-in needs to perform operations even when the user is not logged on.</span></span>|<span data-ttu-id="6b9a2-179">x</span><span class="sxs-lookup"><span data-stu-id="6b9a2-179">x</span></span>||
|<span data-ttu-id="6b9a2-180">Надстройка должна выполнять удаленный код в ответ на событие в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="6b9a2-180">My add-in needs to execute remote code as a response to an event in SharePoint.</span></span>|||
<span data-ttu-id="6b9a2-p110">Так как удаленные приемники событий основаны на OAuth, сравнение в этой таблице не представляет собой лучший способ для принятия решения об использовании того или иного варианта. Используйте удаленные приемники событий, если вам нужно выполнить удаленный код в дополнение к обмену данными.</span><span class="sxs-lookup"><span data-stu-id="6b9a2-p110">Since Remote Event Receivers are built on top of OAuth, a comparison in this table is not the best way to decide whether you should use them or not. Use Remote Event Receivers when you need to execute remote code in addition to data exchange.</span></span>
 

 

### <a name="external-data-connectivity"></a><span data-ttu-id="6b9a2-183">Подключение к внешним данным</span><span class="sxs-lookup"><span data-stu-id="6b9a2-183">External data connectivity</span></span>

<span data-ttu-id="6b9a2-184">При доступе к внешним данным можно использовать указанные ниже варианты подключения (см. рис. 2).</span><span class="sxs-lookup"><span data-stu-id="6b9a2-184">The following connectivity options are available when accessing external data (see Figure 2):</span></span>
 

 

-  <span data-ttu-id="6b9a2-p111">**Веб-прокси:** как разработчик, вы можете использовать веб-прокси, предоставляемый в API-интерфейсах клиента, такие как JSOM. Если вы используете веб-прокси, вы отправляете первоначальный запрос на SharePoint. В свою очередь, SharePoint запрашивает данные на определенной конечной точке и передает ответ обратно на свою страницу. Используйте веб-прокси, если вы хотите, чтобы связь осуществлялась на уровне сервера. Веб-прокси предназначен для доступа к неструктурированным данным, не требующим проверки подлинности. Дополнительные сведения см. в статье [Отправка запросов удаленной службе с помощью веб-прокси в SharePoint](query-a-remote-service-using-the-web-proxy-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="6b9a2-p111">**Web proxy:** As a developer, you can use the web proxy exposed in client APIs such as the JSOM. When you use the web proxy, you issue the initial request to SharePoint. In turn, SharePoint requests the data to the specified endpoint and forwards the response back to your page. Use the web proxy when you want the communication to occur at the server level. The web proxy is designed to access unstructured data that doesn't require authentication. For more information, see [Query a remote service using the web proxy in SharePoint](query-a-remote-service-using-the-web-proxy-in-sharepoint.md).</span></span>
    
 
-  <span data-ttu-id="6b9a2-p112">**Внешние типы контента:** вы можете создавать надстройки, получающие доступ к внешним данным из SAP, Netflix и другим типам данных без администратора клиента. Доступ к внешним приложениям осуществляется с помощью служб Business Connectivity Services (BCS), которые предоставляют согласованный интерфейс, доступный другим приложениям SharePoint. ECT с разрешениями на уровне приложения хороший вариант, если вы используете модель BCS и получаете доступ к данным, требующим проверки подлинности. Дополнительные сведения см. в статье [Добавьте в пределах внешних типов контента в SharePoint](http://msdn.microsoft.com/library/a34cbbba-dc38-4d3d-b796-d54b5848bdfb%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="6b9a2-p112">**External content types:** You can create add-ins that access external data from SAP, Netflix, and proprietary and other types of data without involving the tenant administrator.Access to external applications is maintained through Business Connectivity Services (BCS), which provides a consistent and uniform interface that can be used by other SharePoint applications. App-scoped ECTs are a good option when you are using a BCS model and access to the data requires authentication. For more information, see [Add-in-scoped external content types in SharePoint](http://msdn.microsoft.com/library/a34cbbba-dc38-4d3d-b796-d54b5848bdfb%28Office.15%29.aspx).</span></span>
    
 
-  <span data-ttu-id="6b9a2-p113">**Пользовательская прокси-страница для междоменной библиотеки:** вы можете использовать междоменную библиотеку для доступа к данным в удаленной надстройке, если вы предоставляете пользовательскую прокси-страницу, которая размещается в инфраструктуре удаленной надстройки. Как разработчик, вы несете ответственность за реализацию пользовательской прокси-страницы и должны использовать настраиваемую логику, например механизм проверки подлинности, для удаленной надстройки Используйте междоменную библиотеку с пользовательской прокси-страницей, если требуется, чтобы связь осуществлялась на уровне клиента. Для получения дополнительной информации см. [Создание пользовательской прокси-страницы для междоменной библиотеки в SharePoint](create-a-custom-proxy-page-for-the-cross-domain-library-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="6b9a2-p113">**Custom proxy page for the cross-domain library:** You can use the cross-domain library to access data in your remote add-in if you provide a custom proxy page that is hosted in the remote add-in infrastructure. As the developer, you are responsible for the custom proxy page implementation and must provide custom logic, such as the authentication mechanism to the remote add-in. Use the cross-domain library with a custom proxy page if you want the communication to occur at the client level. For more information, see [Create a custom proxy page for the cross-domain library in SharePoint](create-a-custom-proxy-page-for-the-cross-domain-library-in-sharepoint.md).</span></span>
    
 

### <a name="external-data-connectivity-options-which-one-should-i-use"></a><span data-ttu-id="6b9a2-198">Варианты подключения к внешним данным: выбор подходящего варианта</span><span class="sxs-lookup"><span data-stu-id="6b9a2-198">External data connectivity options: Which one should I use?</span></span>

<span data-ttu-id="6b9a2-199">В таблице ниже перечислены стандартные требования и сценарии, с которыми вы можете столкнуться при создании надстроек. Знак **x** в столбце указывает, какой вариант вы можете использовать в каждом случае.</span><span class="sxs-lookup"><span data-stu-id="6b9a2-199">The following table lists the common requirements and scenarios you might encounter when you are building add-ins. An  **x** in the column indicates which option you can use in each case.</span></span>
 

 

<span data-ttu-id="6b9a2-200">**Табл. 2. Варианты подключения к внешним данным**</span><span class="sxs-lookup"><span data-stu-id="6b9a2-200">**Table 2. External data connectivity options**</span></span>


|<span data-ttu-id="6b9a2-201">**Требование или сценарий**</span><span class="sxs-lookup"><span data-stu-id="6b9a2-201">**Requirement/Scenario**</span></span>|<span data-ttu-id="6b9a2-202">**Веб-прокси**</span><span class="sxs-lookup"><span data-stu-id="6b9a2-202">**Web proxy**</span></span>|<span data-ttu-id="6b9a2-203">**Внешние типы контента**</span><span class="sxs-lookup"><span data-stu-id="6b9a2-203">**External content types**</span></span>|<span data-ttu-id="6b9a2-204">**Междоменная библиотека с настраиваемой страницей прокси**</span><span class="sxs-lookup"><span data-stu-id="6b9a2-204">**Cross-domain library with custom proxy page**</span></span>|
|:-----|:-----|:-----|:-----|
|<span data-ttu-id="6b9a2-205">Я использую клиентские технологии (HTML и JavaScript).</span><span class="sxs-lookup"><span data-stu-id="6b9a2-205">I use client-side technologies (HTML + JavaScript).</span></span>|<span data-ttu-id="6b9a2-206">x</span><span class="sxs-lookup"><span data-stu-id="6b9a2-206">x</span></span>|<span data-ttu-id="6b9a2-207">x</span><span class="sxs-lookup"><span data-stu-id="6b9a2-207">x</span></span>|<span data-ttu-id="6b9a2-208">x</span><span class="sxs-lookup"><span data-stu-id="6b9a2-208">x</span></span>|
|<span data-ttu-id="6b9a2-209">Не удается добавлять страницы или компоненты в удаленную надстройку или службу.</span><span class="sxs-lookup"><span data-stu-id="6b9a2-209">I cannot add pages or components to the remote add-in or service.</span></span>|<span data-ttu-id="6b9a2-210">x</span><span class="sxs-lookup"><span data-stu-id="6b9a2-210">x</span></span>|<span data-ttu-id="6b9a2-211">x</span><span class="sxs-lookup"><span data-stu-id="6b9a2-211">x</span></span>||
|<span data-ttu-id="6b9a2-212">Я хочу использовать интерфейсы REST.</span><span class="sxs-lookup"><span data-stu-id="6b9a2-212">I want to use REST interfaces.</span></span>|<span data-ttu-id="6b9a2-213">x</span><span class="sxs-lookup"><span data-stu-id="6b9a2-213">x</span></span>|<span data-ttu-id="6b9a2-214">x</span><span class="sxs-lookup"><span data-stu-id="6b9a2-214">x</span></span>|<span data-ttu-id="6b9a2-215">x</span><span class="sxs-lookup"><span data-stu-id="6b9a2-215">x</span></span>|
|<span data-ttu-id="6b9a2-216">Я хочу использовать JavaScript CSOM.</span><span class="sxs-lookup"><span data-stu-id="6b9a2-216">I want to use the JavaScript CSOM.</span></span>|<span data-ttu-id="6b9a2-217">x</span><span class="sxs-lookup"><span data-stu-id="6b9a2-217">x</span></span>|<span data-ttu-id="6b9a2-218">x</span><span class="sxs-lookup"><span data-stu-id="6b9a2-218">x</span></span>|<span data-ttu-id="6b9a2-219">x</span><span class="sxs-lookup"><span data-stu-id="6b9a2-219">x</span></span>|
|<span data-ttu-id="6b9a2-220">Я хочу использовать .NET CSOM.</span><span class="sxs-lookup"><span data-stu-id="6b9a2-220">I want to use the .NET CSOM.</span></span>|<span data-ttu-id="6b9a2-221">x</span><span class="sxs-lookup"><span data-stu-id="6b9a2-221">x</span></span>|<span data-ttu-id="6b9a2-222">x</span><span class="sxs-lookup"><span data-stu-id="6b9a2-222">x</span></span>||
|<span data-ttu-id="6b9a2-p114">Прямая связь между инфраструктурой SharePoint и надстройкой отсутствует, и мне необходимо осуществлять вызовы через браузер.</span><span class="sxs-lookup"><span data-stu-id="6b9a2-p114">There is no direct connectivity between the SharePoint infrastructure and my add-in. I need to issue calls through the browser.</span></span>||<span data-ttu-id="6b9a2-225">x</span><span class="sxs-lookup"><span data-stu-id="6b9a2-225">x</span></span>|<span data-ttu-id="6b9a2-226">x</span><span class="sxs-lookup"><span data-stu-id="6b9a2-226">x</span></span>|
|<span data-ttu-id="6b9a2-227">Надстройка должна осуществлять доступ к ресурсам как вошедший в систему пользователь.</span><span class="sxs-lookup"><span data-stu-id="6b9a2-227">My add-in needs to access resources as the logged-on user.</span></span>|<span data-ttu-id="6b9a2-228">x</span><span class="sxs-lookup"><span data-stu-id="6b9a2-228">x</span></span>|<span data-ttu-id="6b9a2-229">x</span><span class="sxs-lookup"><span data-stu-id="6b9a2-229">x</span></span>|<span data-ttu-id="6b9a2-230">x</span><span class="sxs-lookup"><span data-stu-id="6b9a2-230">x</span></span>|

## <a name="available-data-access-apis-for-sharepoint-add-ins"></a><span data-ttu-id="6b9a2-231">API доступа к данным, которые можно использовать в надстройках SharePoint</span><span class="sxs-lookup"><span data-stu-id="6b9a2-231">Available data access APIs for SharePoint Add-ins</span></span>
<span data-ttu-id="6b9a2-232"><a name="SP15_dataaccessoptions_availableAPIs"> </a></span><span class="sxs-lookup"><span data-stu-id="6b9a2-232"><a name="SP15_dataaccessoptions_availableAPIs"> </a></span></span>

<span data-ttu-id="6b9a2-233">Для доступа к данным SharePoint из надстройки можно использовать указанные ниже API.</span><span class="sxs-lookup"><span data-stu-id="6b9a2-233">The following API choices are available when you want to access SharePoint data from your add-in:</span></span>
 

 

-  <span data-ttu-id="6b9a2-p115">**Служба REST:** для сценариев, в которых требуется доступ к сущностям SharePoint из клиентских технологий, которые не используют JavaScript и созданы не на основе платформы .NET Framework, SharePoint предоставляет реализацию веб-службы REST, которая использует [протокол Open Data (OData)](http://www.odata.org/) для выполнения операций CRUDQ (Create, Read, Update, Delete, Query создание, чтение, обновление, удаление, запрос) с данными SharePoint. Кроме того, практически каждый API-интерфейс в клиентских объектных моделях обладает соответствующей конечной точкой REST. Это позволяет коду взаимодействовать напрямую с SharePoint с использованием любой технологии, которая поддерживает стандартные возможности REST. Для использования возможностей REST, которые встроены в SharePoint, код создает запрос RESTful HTTP, передаваемый на конечную точку, которая соответствует необходимому объекту SharePoint. Служба REST обрабатывает запрос HTTP и запрос в формате Atom или Нотация объектов JavaScript (JSON). Для получения более подробных сведений о REST в SharePoint см. [Использование операций запросов OData в запросах SharePoint REST](use-odata-query-operations-in-sharepoint-rest-requests.md).</span><span class="sxs-lookup"><span data-stu-id="6b9a2-p115">**Representational State Transfer (REST):** For scenarios in which you need to access SharePoint entities from client technologies that do not use JavaScript and are not built on the .NET Framework platform, SharePoint provides an implementation of a REST web service that uses the [Open Data (OData) protocol](http://www.odata.org/) to perform CRUDQ (Create, Read, Update, Delete, and Query) operations on SharePoint data. In addition, nearly every API in the client object models has a corresponding REST endpoint. This enables your code to interact directly with SharePoint by using any technology that supports standard REST capabilities. To use the REST capabilities that are built into SharePoint, your code constructs a RESTful HTTP request to an endpoint that corresponds to the desired SharePoint object. The REST service handles the HTTP request and serves a response in either Atom or JavaScript Object Notation (JSON) format. To learn more about REST in SharePoint, see [Use OData query operations in SharePoint REST requests](use-odata-query-operations-in-sharepoint-rest-requests.md).</span></span>
    
 
-  <span data-ttu-id="6b9a2-p116">**Клиентская объектная модель .NET Framework (.NET client OM):** практически каждый класс на основном узле и в объектной модели на стороне сервера обладают соответствующим классом в клиентской объектной модели .NET Framework. Кроме того, клиентская объектная модель .NET Framework также предоставляет полный набор API-интерфейсов для расширения других функций, включая некоторые функции уровня SharePoint, в том числе ECM, таксономию, профили пользователей, расширенный поиск, аналитику, BCS и т. д. Для получения дополнительных сведений об объектных моделях на стороне клиента см. [Выбор правильного набора API в SharePoint](http://msdn.microsoft.com/library/f36645da-77c5-47f1-a2ca-13d4b62b320d%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="6b9a2-p116">**.NET Framework client object model (.NET client OM):** Almost every class in the core site and list server-side object model has a corresponding class in the .NET Framework client object model. In addition, the .NET Framework client object model also exposes a full set of APIs for extending other features, including some SharePoint-level features such as ECM, taxonomy, user profiles, advanced search, analytics, BCS, and others. To learn more about client-side object models, see [Choose the right API set in SharePoint](http://msdn.microsoft.com/library/f36645da-77c5-47f1-a2ca-13d4b62b320d%28Office.15%29.aspx).</span></span>
    
 
-  <span data-ttu-id="6b9a2-p117">**Клиентская объектная модель JavaScript (JSOM):** SharePoint предоставляет объектную модель JavaScript для использования во встроенном скрипте или отдельных JS-файлах. Она включает те же функциональные возможности, что и клиентская объектная модель .NET Framework. JSOM это удобный способ включения пользовательского кода SharePoint в надстройку, особенно в Надстройки, размещаемые в SharePoint, где пользовательский код на стороне сервера не разрешен. Эта модель также позволяет веб-разработчикам использовать существующие навыки работы с JavaScript для создания Надстройки SharePoint при прохождении минимального обучения. Дополнительные сведения о клиентских объектных моделях см. в статье [Выбор правильного набора API в SharePoint](http://msdn.microsoft.com/library/f36645da-77c5-47f1-a2ca-13d4b62b320d%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="6b9a2-p117">**JavaScript client object model (JSOM):** SharePoint provides a JavaScript object model for use in either inline script or separate .js files. It includes all the same functionality as the .NET Framework client object model. The JSOM is a useful way of including custom SharePoint code in an add-in, especially in a SharePoint-hosted add-in, where custom server-side code is not allowed. It also enables web developers to use their existing JavaScript skills to create SharePoint Add-ins with a minimal learning curve. To learn more about client-side object models, see [Choose the right API set in SharePoint](http://msdn.microsoft.com/library/f36645da-77c5-47f1-a2ca-13d4b62b320d%28Office.15%29.aspx).</span></span>
    
 
<span data-ttu-id="6b9a2-p118">Возможно, существуют другие API, которые можно использовать в Надстройка SharePoint при доступе к внешним данным. Это зависит от интерфейсов с внешними системами и возможностями этих систем. Данные интерфейсы также следует учитывать при создании приложения.</span><span class="sxs-lookup"><span data-stu-id="6b9a2-p118">There might be additional APIs that you can use in your SharePoint Add-in when accessing external data. It depends on what interfaces the external services and systems have to offer. You should also consider these interfaces in your design.</span></span>
 

 

## <a name="additional-resources"></a><span data-ttu-id="6b9a2-251">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="6b9a2-251">Additional resources</span></span>
<span data-ttu-id="6b9a2-252"><a name="SP15_dataaccessoptions_addResources"> </a></span><span class="sxs-lookup"><span data-stu-id="6b9a2-252"><a name="SP15_dataaccessoptions_addResources"> </a></span></span>


-  [<span data-ttu-id="6b9a2-253">Авторизация и проверка подлинности для надстроек в SharePoint</span><span class="sxs-lookup"><span data-stu-id="6b9a2-253">Authorization and authentication of SharePoint Add-ins</span></span>](authorization-and-authentication-of-sharepoint-add-ins.md)
    
 
-  [<span data-ttu-id="6b9a2-254">Доступ к данным SharePoint из надстроек с помощью междоменной библиотеки</span><span class="sxs-lookup"><span data-stu-id="6b9a2-254">Access SharePoint data from add-ins using the cross-domain library</span></span>](access-sharepoint-data-from-add-ins-using-the-cross-domain-library.md)
    
 
-  [<span data-ttu-id="6b9a2-255">Создание настраиваемой страницы прокси для междоменной библиотеки в SharePoint</span><span class="sxs-lookup"><span data-stu-id="6b9a2-255">Create a custom proxy page for the cross-domain library in SharePoint</span></span>](create-a-custom-proxy-page-for-the-cross-domain-library-in-sharepoint.md)
    
 
-  [<span data-ttu-id="6b9a2-256">Отправка запросов удаленной службе с помощью веб-прокси в SharePoint</span><span class="sxs-lookup"><span data-stu-id="6b9a2-256">Query a remote service using the web proxy in SharePoint</span></span>](query-a-remote-service-using-the-web-proxy-in-sharepoint.md)
    
 
-  [<span data-ttu-id="6b9a2-257">Создание удаленного приемника событий в надстройках SharePoint</span><span class="sxs-lookup"><span data-stu-id="6b9a2-257">Create a remote event receiver in SharePoint Add-ins</span></span>](create-a-remote-event-receiver-in-sharepoint-add-ins.md)
    
 
-  [<span data-ttu-id="6b9a2-258">Выбор правильного набора API в SharePoint</span><span class="sxs-lookup"><span data-stu-id="6b9a2-258">Choose the right API set in SharePoint</span></span>](http://msdn.microsoft.com/library/f36645da-77c5-47f1-a2ca-13d4b62b320d%28Office.15%29.aspx)
    
 
-  [<span data-ttu-id="6b9a2-259">Использование операций запросов OData в запросах REST SharePoint</span><span class="sxs-lookup"><span data-stu-id="6b9a2-259">Use OData query operations in SharePoint REST requests</span></span>](use-odata-query-operations-in-sharepoint-rest-requests.md)
    
 
