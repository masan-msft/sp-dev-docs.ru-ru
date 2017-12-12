---
title: "Подключение части приложения SharePoint с помощью SignalR"
ms.date: 11/03/2017
ms.openlocfilehash: 0219f20e399522c1b41b093fe23f2480b4273822
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="connect-sharepoint-app-parts-by-using-signalr"></a>Подключение части приложения SharePoint с помощью SignalR

Реализация общение в реальном времени между частями приложения SharePoint с помощью SignalR.

_**Применимо к:** надстройки для SharePoint | SharePoint 2013 | SharePoint Online_

Пример [Core.ConnectedAppParts](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ConnectedAppParts) показано, как использовать приложения с размещением у поставщика в качестве сообщения брокера или пообщаться концентратора отправлять и получать сообщения от всех частей приложения, подключенных к чата сервера-концентратора. Используйте это решение, если преобразование веб-частей SharePoint в части приложения и требуется части вашего приложения для взаимодействия друг с другом.

## <a name="before-you-begin"></a>Перед началом работы
<a name="sectionSection0"> </a>

Чтобы начать работу, загрузите [Core.ConnectedAppParts](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ConnectedAppParts) пример приложения из project [для разработчиков Office 365 шаблоны и рекомендации](https://github.com/SharePoint/PnP/tree/dev) на репозиториев.

## <a name="connected-app-parts-and-chat-hub-architecture"></a>Подключенные части приложения и архитектура сервера-концентратора чата
<a name="sectionSection1"> </a>

На рисунке 1 показано части подключенных приложения и архитектура сервера-концентратора чата.

**На рисунке 1. Подключенные части приложения и архитектура сервера-концентратора чата**

![Иллюстрация, показывающая архитектура примера кода Core.ConnectedAppParts](media/f835d4b8-a84e-4484-8fdf-370d9f308b53.png)

Части подключенных приложения и чата архитектура сервера-концентратора включает в себя следующие компоненты:

1. Страницы SharePoint, включая части приложения. Части приложения используйте библиотеку jQuery SignalR. Части приложения содержат код JavaScript, которой отправки и получения сообщений из концентратора чата под управлением в надстройке размещением у поставщика. Каждый веб-часть приложения сначала необходимо подключить к чата сервера-концентратора. После подключения к сервера-концентратора чата части приложения можно отправлять и принимать сообщения от других частей подключенных приложения.
    
2. SignalR сервера-концентратора прокси-сервер, который устанавливает подключение к чата сервера-концентратора. Прокси-сервер SignalR сервера-концентратора является посредником сообщений между веб-части приложения в код JavaScript и кода C#, сервер-концентратор чата.
    
3. Концентратор чата использует библиотеку SignalR для маршрутизации сообщений может отправлять получения части приложения. В этом примере кода все части приложения получать сообщения от сервера-концентратора чата, включая веб-части приложения, отправившего сообщение.
    
> [!NOTE] 
> Так как части приложения выполняются в IFRAME, нельзя использовать JavaScript только для обмена данными между части приложения. 

## <a name="use-the-coreconnectedappparts-app"></a>Использование приложения Core.ConnectedAppParts
<a name="sectionSection2"> </a>

Чтобы просмотреть демонстрационный из двух частей приложения, связь с использованием SignalR: 

1. При запуске приложения и начальной страницы отображается, нажмите кнопку **Назад на сайт**.
    
2. Выбор **параметров** > **"Добавление"**.
    
3. В поле **новое имя страницы**введите **ConnectedAppParts**и нажмите кнопку **Создать**.
    
4. Нажмите кнопку **Вставить** > **Веб-части приложения**.
    
5. Выберите **подключенных часть — один** > **Добавить**.
    
6. Нажмите кнопку **Вставить** > **Веб-части приложения**.
    
7. Выберите **подключенных часть - два** > **Добавить**.
    
8. Выберите команду **Сохранить**.
    
9. В **подключенных часть — один**, введите **Hello World с первой части приложения**и нажмите кнопку **Отправить**.
    
10. Убедитесь, что сообщение **Hello World с первой части приложения** отображается в обоих **подключенных часть — один** и **подключенных часть - два** части приложения.
    
В этом примере кода Core.ConnectedAppParts проект содержит две части приложения (ConnectedPartOne и ConnectedPartTwo), которые развертываются на хост-сайт. ConnectedPartOne и ConnectedPartTwo запущено в IFRAME. Содержимое веб-страницы для ConnectedPartOne и ConnectedPartTwo определены в проекте Core.ConnectedAppPartsWeb в Pages\ConnectedPartOne.aspx и Pages\ConnectedPartTwo.aspx. Обе страницы выполняются в приложения, размещенного поставщиком, с сервера-концентратора чата (ChatHub.cs) и используют встроенные JavaScript для:

1. Включите библиотеку jQuery SignalR.
    
2. Подключение сервера-концентратора SignalR прокси-сервера, с помощью **connection.chatHub**. 
    
3. Используйте **chat.client.broadcastMessage** для определения функции для получения широковещательные сообщения, отправленные с сервера-концентратора чата. В этом примере кода имя веб-части приложения и выполняется широковещательные сообщения отображается в списке **обсуждений** .
    
4. Запуск подключения сервера-концентратора чата, используя **$. .done () connection.hub.start**. При установке подключения определяется обработчика событий на **sendmessage** события нажатия кнопки. Этот обработчик событий вызывает **chat.server.send** для отправки имя веб-части приложения и сообщения, введенный пользователем для сервера-концентратора чата.

> [!NOTE] 
> Код, приведенный в данной статье предоставляется в качестве-без никаких гарантий, явных или подразумеваемых, включая никаких гарантий соответствие для определенной задачи, окупаемость или не нарушения прав.

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

При выполнении **chat.server.send**встроенного кода JavaScript в ConnectedPartOne.aspx вызов метода **отправки** в ChatHub.cs. Метод **отправки** в ChatHub.cs получает имя части приложения вещания и сообщения и затем рассылает сведения о ко всем частям подключенных приложения с помощью **Clients.All.broadcastMessage**.  **Clients.All.broadcastMessage** вызывает функцию JavaScript (в части всех подключенных приложения), который был определен с помощью **chat.client.broadcastMessage**.

```C#
 public void Send(string name, string message)
        {
            // Call the broadcastMessage method to update the app parts.
            Clients.All.broadcastMessage(name, message);
        }
```

**Важные**  В этом примере кода все части приложения, подключенных к сервера-концентратора чата получают все сообщения, отправленные через сервер-концентратор чата. Рассмотрите возможность фильтрации сообщений на основе идентификатора сеанса, чтобы определить, какие части приложения должны принимать какие сообщения.

## <a name="see-also"></a>См. также
<a name="bk_addresources"> </a>

-  [Шаблоны и рекомендации решений разработки Office 365](Office-365-development-patterns-and-practices-solution-guidance.md)
    
-  [Общие сведения о SignalR](http://www.asp.net/signalr/overview/getting-started/introduction-to-signalr)
    
-  [При помощи учебника по: Приступая к работе с SignalR 2](http://www.asp.net/signalr/overview/getting-started/tutorial-getting-started-with-signalr)
    
