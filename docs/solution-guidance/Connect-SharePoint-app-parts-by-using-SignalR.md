---
title: "Подключение части приложения SharePoint с помощью SignalR"
ms.date: 11/03/2017
ms.openlocfilehash: 0219f20e399522c1b41b093fe23f2480b4273822
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="connect-sharepoint-app-parts-by-using-signalr"></a><span data-ttu-id="88491-102">Подключение части приложения SharePoint с помощью SignalR</span><span class="sxs-lookup"><span data-stu-id="88491-102">Connect SharePoint app parts by using SignalR</span></span>

<span data-ttu-id="88491-103">Реализация общение в реальном времени между частями приложения SharePoint с помощью SignalR.</span><span class="sxs-lookup"><span data-stu-id="88491-103">Implement real-time communication between SharePoint app parts by using SignalR.</span></span>

<span data-ttu-id="88491-104">_**Применимо к:** надстройки для SharePoint | SharePoint 2013 | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="88491-104">_**Applies to:** add-ins for SharePoint | SharePoint 2013 | SharePoint Online_</span></span>

<span data-ttu-id="88491-105">Пример [Core.ConnectedAppParts](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ConnectedAppParts) показано, как использовать приложения с размещением у поставщика в качестве сообщения брокера или пообщаться концентратора отправлять и получать сообщения от всех частей приложения, подключенных к чата сервера-концентратора.</span><span class="sxs-lookup"><span data-stu-id="88491-105">The  [Core.ConnectedAppParts](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ConnectedAppParts) sample shows you how to use a provider-hosted app as a message broker or chat hub to send and receive messages from all app parts connected to the chat hub.</span></span> <span data-ttu-id="88491-106">Используйте это решение, если преобразование веб-частей SharePoint в части приложения и требуется части вашего приложения для взаимодействия друг с другом.</span><span class="sxs-lookup"><span data-stu-id="88491-106">Use this solution if you are converting your SharePoint web parts to app parts, and need your app parts to communicate with each other.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="88491-107">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="88491-107">Before you begin</span></span>
<span data-ttu-id="88491-108"><a name="sectionSection0"> </a></span><span class="sxs-lookup"><span data-stu-id="88491-108"></span></span>

<span data-ttu-id="88491-109">Чтобы начать работу, загрузите [Core.ConnectedAppParts](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ConnectedAppParts) пример приложения из project [для разработчиков Office 365 шаблоны и рекомендации](https://github.com/SharePoint/PnP/tree/dev) на репозиториев.</span><span class="sxs-lookup"><span data-stu-id="88491-109">To get started, download the  [Core.ConnectedAppParts](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ConnectedAppParts) sample app from the [Office 365 Developer patterns and practices](https://github.com/SharePoint/PnP/tree/dev) project on GitHub.</span></span>

## <a name="connected-app-parts-and-chat-hub-architecture"></a><span data-ttu-id="88491-110">Подключенные части приложения и архитектура сервера-концентратора чата</span><span class="sxs-lookup"><span data-stu-id="88491-110">Connected app parts and chat hub architecture</span></span>
<span data-ttu-id="88491-111"><a name="sectionSection1"> </a></span><span class="sxs-lookup"><span data-stu-id="88491-111"></span></span>

<span data-ttu-id="88491-112">На рисунке 1 показано части подключенных приложения и архитектура сервера-концентратора чата.</span><span class="sxs-lookup"><span data-stu-id="88491-112">Figure 1 shows the connected app parts and chat hub architecture.</span></span>

<span data-ttu-id="88491-113">**На рисунке 1. Подключенные части приложения и архитектура сервера-концентратора чата**</span><span class="sxs-lookup"><span data-stu-id="88491-113">**Figure 1. Connected app parts and chat hub architecture**</span></span>

![Иллюстрация, показывающая архитектура примера кода Core.ConnectedAppParts](media/f835d4b8-a84e-4484-8fdf-370d9f308b53.png)

<span data-ttu-id="88491-115">Части подключенных приложения и чата архитектура сервера-концентратора включает в себя следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="88491-115">The connected app parts and chat hub architecture includes the following components:</span></span>

1. <span data-ttu-id="88491-116">Страницы SharePoint, включая части приложения.</span><span class="sxs-lookup"><span data-stu-id="88491-116">SharePoint pages that include app parts.</span></span> <span data-ttu-id="88491-117">Части приложения используйте библиотеку jQuery SignalR.</span><span class="sxs-lookup"><span data-stu-id="88491-117">The app parts use the SignalR jQuery library.</span></span> <span data-ttu-id="88491-118">Части приложения содержат код JavaScript, которой отправки и получения сообщений из концентратора чата под управлением в надстройке размещением у поставщика.</span><span class="sxs-lookup"><span data-stu-id="88491-118">The app parts contain JavaScript code, which send and receive messages from the chat hub running in the provider-hosted add-in.</span></span> <span data-ttu-id="88491-119">Каждый веб-часть приложения сначала необходимо подключить к чата сервера-концентратора.</span><span class="sxs-lookup"><span data-stu-id="88491-119">Each app part must first connect to the chat hub.</span></span> <span data-ttu-id="88491-120">После подключения к сервера-концентратора чата части приложения можно отправлять и принимать сообщения от других частей подключенных приложения.</span><span class="sxs-lookup"><span data-stu-id="88491-120">After connecting to the chat hub, app parts can send and receive messages from other connected app parts.</span></span>
    
2. <span data-ttu-id="88491-121">SignalR сервера-концентратора прокси-сервер, который устанавливает подключение к чата сервера-концентратора.</span><span class="sxs-lookup"><span data-stu-id="88491-121">A SignalR Hub Proxy, which establishes a socket connection to the chat hub.</span></span> <span data-ttu-id="88491-122">Прокси-сервер SignalR сервера-концентратора является посредником сообщений между веб-части приложения в код JavaScript и кода C#, сервер-концентратор чата.</span><span class="sxs-lookup"><span data-stu-id="88491-122">The SignalR Hub Proxy brokers messages between the app part's JavaScript code and the chat hub's C# code.</span></span>
    
3. <span data-ttu-id="88491-123">Концентратор чата использует библиотеку SignalR для маршрутизации сообщений может отправлять получения части приложения.</span><span class="sxs-lookup"><span data-stu-id="88491-123">The chat hub, which uses the SignalR library to route messages from sending to receiving app parts.</span></span> <span data-ttu-id="88491-124">В этом примере кода все части приложения получать сообщения от сервера-концентратора чата, включая веб-части приложения, отправившего сообщение.</span><span class="sxs-lookup"><span data-stu-id="88491-124">In this code sample, all app parts receive messages from the chat hub, including the app part that sent the message.</span></span>
    
> [!NOTE] 
> <span data-ttu-id="88491-125">Так как части приложения выполняются в IFRAME, нельзя использовать JavaScript только для обмена данными между части приложения.</span><span class="sxs-lookup"><span data-stu-id="88491-125">Because app parts run in an IFRAME, you cannot use JavaScript only to communicate between app parts.</span></span> 

## <a name="use-the-coreconnectedappparts-app"></a><span data-ttu-id="88491-126">Использование приложения Core.ConnectedAppParts</span><span class="sxs-lookup"><span data-stu-id="88491-126">Use the Core.ConnectedAppParts app</span></span>
<span data-ttu-id="88491-127"><a name="sectionSection2"> </a></span><span class="sxs-lookup"><span data-stu-id="88491-127"></span></span>

<span data-ttu-id="88491-128">Чтобы просмотреть демонстрационный из двух частей приложения, связь с использованием SignalR:</span><span class="sxs-lookup"><span data-stu-id="88491-128">To see a demo of two app parts communicating by using SignalR:</span></span> 

1. <span data-ttu-id="88491-129">При запуске приложения и начальной страницы отображается, нажмите кнопку **Назад на сайт**.</span><span class="sxs-lookup"><span data-stu-id="88491-129">When you run the app and the start page is displayed, choose  **Back to Site**.</span></span>
    
2. <span data-ttu-id="88491-130">Выбор **параметров** > **"Добавление"**.</span><span class="sxs-lookup"><span data-stu-id="88491-130">Choose  **Settings** > **Add a page**.</span></span>
    
3. <span data-ttu-id="88491-131">В поле **новое имя страницы**введите **ConnectedAppParts**и нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="88491-131">In  **New page name**, enter  **ConnectedAppParts**, and then choose  **Create**.</span></span>
    
4. <span data-ttu-id="88491-132">Нажмите кнопку **Вставить** > **Веб-части приложения**.</span><span class="sxs-lookup"><span data-stu-id="88491-132">Choose  **Insert** > **App Part**.</span></span>
    
5. <span data-ttu-id="88491-133">Выберите **подключенных часть — один** > **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="88491-133">Choose  **Connected Part - One** > **Add**.</span></span>
    
6. <span data-ttu-id="88491-134">Нажмите кнопку **Вставить** > **Веб-части приложения**.</span><span class="sxs-lookup"><span data-stu-id="88491-134">Choose  **Insert** > **App Part**.</span></span>
    
7. <span data-ttu-id="88491-135">Выберите **подключенных часть - два** > **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="88491-135">Choose  **Connected Part - Two** > **Add**.</span></span>
    
8. <span data-ttu-id="88491-136">Выберите команду **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="88491-136">Choose  **Save**.</span></span>
    
9. <span data-ttu-id="88491-137">В **подключенных часть — один**, введите **Hello World с первой части приложения**и нажмите кнопку **Отправить**.</span><span class="sxs-lookup"><span data-stu-id="88491-137">In  **Connected Part - One**, enter  **Hello World from App Part 1**, and then choose  **Send**.</span></span>
    
10. <span data-ttu-id="88491-138">Убедитесь, что сообщение **Hello World с первой части приложения** отображается в обоих **подключенных часть — один** и **подключенных часть - два** части приложения.</span><span class="sxs-lookup"><span data-stu-id="88491-138">Verify that the message  **Hello World from App Part 1** appears in both **Connected Part - One** and **Connected Part - Two** app parts.</span></span>
    
<span data-ttu-id="88491-139">В этом примере кода Core.ConnectedAppParts проект содержит две части приложения (ConnectedPartOne и ConnectedPartTwo), которые развертываются на хост-сайт.</span><span class="sxs-lookup"><span data-stu-id="88491-139">In this code sample, the Core.ConnectedAppParts project contains two app parts (ConnectedPartOne and ConnectedPartTwo) that are deployed to the host web.</span></span> <span data-ttu-id="88491-140">ConnectedPartOne и ConnectedPartTwo запущено в IFRAME.</span><span class="sxs-lookup"><span data-stu-id="88491-140">ConnectedPartOne and ConnectedPartTwo run in an IFRAME.</span></span> <span data-ttu-id="88491-141">Содержимое веб-страницы для ConnectedPartOne и ConnectedPartTwo определены в проекте Core.ConnectedAppPartsWeb в Pages\ConnectedPartOne.aspx и Pages\ConnectedPartTwo.aspx.</span><span class="sxs-lookup"><span data-stu-id="88491-141">The web page contents for ConnectedPartOne and ConnectedPartTwo are defined in the Core.ConnectedAppPartsWeb project in Pages\ConnectedPartOne.aspx and Pages\ConnectedPartTwo.aspx.</span></span> <span data-ttu-id="88491-142">Обе страницы выполняются в приложения, размещенного поставщиком, с сервера-концентратора чата (ChatHub.cs) и используют встроенные JavaScript для:</span><span class="sxs-lookup"><span data-stu-id="88491-142">Both pages run in the provider-hosted app with the chat hub (ChatHub.cs) and use inline JavaScript to:</span></span>

1. <span data-ttu-id="88491-143">Включите библиотеку jQuery SignalR.</span><span class="sxs-lookup"><span data-stu-id="88491-143">Include the SignalR jQuery library.</span></span>
    
2. <span data-ttu-id="88491-144">Подключение сервера-концентратора SignalR прокси-сервера, с помощью **connection.chatHub**.</span><span class="sxs-lookup"><span data-stu-id="88491-144">Connect to the SignalR Hub Proxy using  **connection.chatHub**.</span></span> 
    
3. <span data-ttu-id="88491-145">Используйте **chat.client.broadcastMessage** для определения функции для получения широковещательные сообщения, отправленные с сервера-концентратора чата.</span><span class="sxs-lookup"><span data-stu-id="88491-145">Use  **chat.client.broadcastMessage** to define a function to receive broadcasted messages sent by the chat hub.</span></span> <span data-ttu-id="88491-146">В этом примере кода имя веб-части приложения и выполняется широковещательные сообщения отображается в списке **обсуждений** .</span><span class="sxs-lookup"><span data-stu-id="88491-146">In this code sample, the name of the app part and the message being broadcasted is displayed in the **discussion** list.</span></span>
    
4. <span data-ttu-id="88491-147">Запуск подключения сервера-концентратора чата, используя **$. .done () connection.hub.start**.</span><span class="sxs-lookup"><span data-stu-id="88491-147">Start the connection to the chat hub using  **$.connection.hub.start().done**.</span></span> <span data-ttu-id="88491-148">При установке подключения определяется обработчика событий на **sendmessage** события нажатия кнопки.</span><span class="sxs-lookup"><span data-stu-id="88491-148">When the connection is established, an event handler is defined on the  **sendmessage** button's click event.</span></span> <span data-ttu-id="88491-149">Этот обработчик событий вызывает **chat.server.send** для отправки имя веб-части приложения и сообщения, введенный пользователем для сервера-концентратора чата.</span><span class="sxs-lookup"><span data-stu-id="88491-149">This event handler calls **chat.server.send** to send the name of the app part and the message entered by the user to the chat hub.</span></span>

> [!NOTE] 
> <span data-ttu-id="88491-150">Код, приведенный в данной статье предоставляется в качестве-без никаких гарантий, явных или подразумеваемых, включая никаких гарантий соответствие для определенной задачи, окупаемость или не нарушения прав.</span><span class="sxs-lookup"><span data-stu-id="88491-150">The code in this article is provided as-is, without warranty of any kind, either express or implied, including any implied warranties of fitness for a particular purpose, merchantability, or non-infringement.</span></span>

```
    <!--Script references. -->
    <!--Reference the jQuery library. -->
    <script src="../Scripts/jquery-1.6.4.min.js" ></script>
    <!--Reference the SignalR library. -->
    <script src="../Scripts/jquery.signalR-2.0.3.min.js"></script>
    <!--Reference the autogenerated SignalR hub script. -->
    <script src="../signalr/hubs"></script>
    <!--Add script to update the page and send messages.--> 
    <script type="text/javascript">
        $(function () {
            // Declare a proxy to reference the hub. 
            var chat = $.connection.chatHub;
            // Create a function that the hub can call to broadcast messages.
            chat.client.broadcastMessage = function (name, message) {
                // Html encode display name and message. 
                var encodedName = $('<div />').text(name).html();
                var encodedMsg = $('<div />').text(message).html();
                // Add the message to the page. 
                $('#discussion').append('<li><strong>' + encodedName
                    + '</strong>:&amp;nbsp;&amp;nbsp;' + encodedMsg + '</li>');
            };
            // Set initial focus to message input box.  
            $('#message').focus();
            // Start the connection.
            $.connection.hub.start().done(function () {
                $('#sendmessage').click(function () {
                    // Call the Send method on the hub. 
                    chat.server.send($('#displayname').val(), $('#message').val());
                    // Clear text box and reset focus for next comment. 
                    $('#message').val('').focus();
                });
            });
        });
    </script>
```

<span data-ttu-id="88491-151">При выполнении **chat.server.send**встроенного кода JavaScript в ConnectedPartOne.aspx вызов метода **отправки** в ChatHub.cs.</span><span class="sxs-lookup"><span data-stu-id="88491-151">When the inline JavaScript code in ConnectedPartOne.aspx runs  **chat.server.send**, a call is made to the  **Send** method in ChatHub.cs.</span></span> <span data-ttu-id="88491-152">Метод **отправки** в ChatHub.cs получает имя части приложения вещания и сообщения и затем рассылает сведения о ко всем частям подключенных приложения с помощью **Clients.All.broadcastMessage**.</span><span class="sxs-lookup"><span data-stu-id="88491-152">The **Send** method in ChatHub.cs receives the broadcasting app part's name and the message, and then broadcasts the information to all connected app parts by using **Clients.All.broadcastMessage**.</span></span>  <span data-ttu-id="88491-153">**Clients.All.broadcastMessage** вызывает функцию JavaScript (в части всех подключенных приложения), который был определен с помощью **chat.client.broadcastMessage**.</span><span class="sxs-lookup"><span data-stu-id="88491-153">**Clients.All.broadcastMessage** calls the JavaScript function (in all connected app parts) that was defined by using **chat.client.broadcastMessage**.</span></span>

```C#
 public void Send(string name, string message)
        {
            // Call the broadcastMessage method to update the app parts.
            Clients.All.broadcastMessage(name, message);
        }
```

<span data-ttu-id="88491-154">**Важные**  В этом примере кода все части приложения, подключенных к сервера-концентратора чата получают все сообщения, отправленные через сервер-концентратор чата.</span><span class="sxs-lookup"><span data-stu-id="88491-154">**Important**  In this code sample, all app parts connected to the chat hub receive all messages sent through the chat hub.</span></span> <span data-ttu-id="88491-155">Рассмотрите возможность фильтрации сообщений на основе идентификатора сеанса, чтобы определить, какие части приложения должны принимать какие сообщения.</span><span class="sxs-lookup"><span data-stu-id="88491-155">Consider filtering messages based on session ID to determine which app parts should receive which messages.</span></span>

## <a name="see-also"></a><span data-ttu-id="88491-156">См. также</span><span class="sxs-lookup"><span data-stu-id="88491-156">See also</span></span>
<span data-ttu-id="88491-157"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="88491-157"></span></span>

-  [<span data-ttu-id="88491-158">Шаблоны и рекомендации решений разработки Office 365</span><span class="sxs-lookup"><span data-stu-id="88491-158">Office 365 development patterns and practices solution guidance</span></span>](Office-365-development-patterns-and-practices-solution-guidance.md)
    
-  [<span data-ttu-id="88491-159">Общие сведения о SignalR</span><span class="sxs-lookup"><span data-stu-id="88491-159">Introduction to SignalR</span></span>](http://www.asp.net/signalr/overview/getting-started/introduction-to-signalr)
    
-  [<span data-ttu-id="88491-160">При помощи учебника по: Приступая к работе с SignalR 2</span><span class="sxs-lookup"><span data-stu-id="88491-160">Tutorial: Getting Started with SignalR 2</span></span>](http://www.asp.net/signalr/overview/getting-started/tutorial-getting-started-with-signalr)
    
