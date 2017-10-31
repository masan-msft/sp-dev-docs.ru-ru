---
title: "Создание приемника событий надстройки в надстройках для SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: cd2e90745acbc17353db12c350127dc793126337
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="create-an-add-in-event-receiver-in-sharepoint-add-ins"></a><span data-ttu-id="2e22c-102">Создание приемника событий надстройки в надстройках для SharePoint</span><span class="sxs-lookup"><span data-stu-id="2e22c-102">Create an add-in event receiver in SharePoint Add-ins</span></span>
<span data-ttu-id="2e22c-103">Создайте обработчики для событий установки и удаления надстройки в надстройках SharePoint.</span><span class="sxs-lookup"><span data-stu-id="2e22c-103">Create handlers for the SharePoint Add-in install and uninstall events in SharePoint Add-ins.</span></span>
 

 <span data-ttu-id="2e22c-p101">**Примечание.** В настоящее время идет процесс замены названия "приложения для SharePoint" названием "надстройки SharePoint". Во время этого процесса в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio может по-прежнему использоваться термин "приложения для SharePoint". Дополнительные сведения см. в статье [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="2e22c-p101">**Note**  The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see  [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span></span>
 


## <a name="prerequisites"></a><span data-ttu-id="2e22c-107">Необходимые компоненты</span><span class="sxs-lookup"><span data-stu-id="2e22c-107">Prerequisites</span></span>
<span data-ttu-id="2e22c-108"><a name="SP15appevent_prereq"> </a></span><span class="sxs-lookup"><span data-stu-id="2e22c-108"><a name="SP15appevent_prereq"> </a></span></span>

<span data-ttu-id="2e22c-p102">В этой статье предполагается, что вы уже имеете представление о Надстройки SharePoint с размещением у поставщика, а также создали несколько приложений, которые хоть немного сложнее, чем "Hello World". Кроме того, предполагается, что вы прочли статью  [Обработка событий в надстройках SharePoint](handle-events-in-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="2e22c-p102">This article presupposes that you have an understanding of provider-hosted SharePoint Add-ins, and that you have developed a few that go a least a little beyond the "Hello World" level. Also, you should be familiar with  [Handle events in SharePoint Add-ins](handle-events-in-sharepoint-add-ins.md).</span></span> 
 

 

## <a name="get-more-code-samples"></a><span data-ttu-id="2e22c-111">Дополнительные примеры кода</span><span class="sxs-lookup"><span data-stu-id="2e22c-111">Get more code samples</span></span>
<span data-ttu-id="2e22c-112"><a name="SP15appevent_prereq"> </a></span><span class="sxs-lookup"><span data-stu-id="2e22c-112"><a name="SP15appevent_prereq"> </a></span></span>

<span data-ttu-id="2e22c-p103">Ознакомившись с развернутым примером, приведенным в этой статье, вы получите готовый пример кода. Ниже представлены другие примеры. Не все они соответствуют архитектуре, описанной в этой статье. Существует несколько хороших способов создать приемник событий надстроек. Кроме того, помните, что руководства от Майкрософт могут изменяться со временем.</span><span class="sxs-lookup"><span data-stu-id="2e22c-p103">If you work through the continuing example in this article, you will have a finished code sample. The following are some other samples. They don't all follow the architecture described in this article. There can be more than one good way to architect an add-in event receiver, and keep in mind also that Microsoft's guidance can evolve over time.</span></span> 
 

 

-  <span data-ttu-id="2e22c-117">Пример кода [OfficeDev/PnP/Samples/Core.AppEvents.HandlerDelegation](https://github.com/OfficeDev/PnP/tree/master/Samples/Core.AppEvents.HandlerDelegation) наиболее близко соответствует примеру, приведенному в этой статье.</span><span class="sxs-lookup"><span data-stu-id="2e22c-117">[OfficeDev/PnP/Samples/Core.AppEvents.HandlerDelegation](https://github.com/OfficeDev/PnP/tree/master/Samples/Core.AppEvents.HandlerDelegation) is a close match to the continuing example in this article.</span></span>
    
 
-  <span data-ttu-id="2e22c-118">В [OfficeDev/PnP/Samples/Core.AppEvents](https://github.com/OfficeDev/PnP/tree/master/Samples/Core.AppEvents) показано, как решить задачу, которая аналогична приведенной в предыдущем примере кода, в сценариях, где для обработчика не может использоваться стратегия делегирования.</span><span class="sxs-lookup"><span data-stu-id="2e22c-118">[OfficeDev/PnP/Samples/Core.AppEvents](https://github.com/OfficeDev/PnP/tree/master/Samples/Core.AppEvents) shows how to do the same task as the preceding sample in scenarios where the handler delegation strategy cannot be used.</span></span>
    
 
-  [<span data-ttu-id="2e22c-119">OfficeDev/PnP/Samples/Core.EventReceivers</span><span class="sxs-lookup"><span data-stu-id="2e22c-119">OfficeDev/PnP/Samples/Core.EventReceivers</span></span>](https://github.com/OfficeDev/PnP/tree/master/Samples/Core.EventReceivers)
    
 
-  [<span data-ttu-id="2e22c-120">Создание размещаемой у поставщика надстройки, которая настраивает установку надстройки</span><span class="sxs-lookup"><span data-stu-id="2e22c-120">Create a provider-hosted add-in that customizes add-in installation</span></span>](https://code.msdn.microsoft.com/SharePoint-Create-a-f27752e0)
    
 

## <a name="add-an-add-in-installed-event-receiver"></a><span data-ttu-id="2e22c-121">Добавление приемника для события установки надстройки</span><span class="sxs-lookup"><span data-stu-id="2e22c-121">Add an add-in installed event receiver</span></span>
<span data-ttu-id="2e22c-122"><a name="SP15appevent_prereq"> </a></span><span class="sxs-lookup"><span data-stu-id="2e22c-122"><a name="SP15appevent_prereq"> </a></span></span>


1. <span data-ttu-id="2e22c-p104">Откройте в Visual Studio проект размещаемого у поставщика Надстройка SharePoint (при добавлении обработчика события к надстройке, размещаемой в SharePoint, Инструменты разработчика Office для Visual Studio преобразует ее в надстройку, размещаемую у поставщика).</span><span class="sxs-lookup"><span data-stu-id="2e22c-p104">In Visual Studio, open the project for the provider-hosted SharePoint Add-in. (If you add an add-in event handler to a SharePoint-hosted add-in, the Office Developer Tools for Visual Studio convert it to a provider-hosted app.)</span></span>
    
 
2. <span data-ttu-id="2e22c-125">В **обозревателе решений** выберите узел для надстройки SharePoint.</span><span class="sxs-lookup"><span data-stu-id="2e22c-125">In  **Solution Explorer**, choose the node for the SharePoint Add-in.</span></span>
    
 
3. <span data-ttu-id="2e22c-126">В окне **Свойства** задайте для параметра **Управление установленными надстройками** значение **True**.</span><span class="sxs-lookup"><span data-stu-id="2e22c-126">In the  **Properties** window, set the value of **Handle Add-in Installed** to **True**.</span></span> 
    
    <span data-ttu-id="2e22c-127">**Рис. 1. События надстройки в окне свойств**</span><span class="sxs-lookup"><span data-stu-id="2e22c-127">**Figure 1. Add-in events in the properties window**</span></span>

 

  ![События приложения в окне свойств](../images/SP_VS_Properties_Window_AppEvents.PNG)
 

    <span data-ttu-id="2e22c-129">Инструменты разработчика Office для Visual Studio сделает следующее:</span><span class="sxs-lookup"><span data-stu-id="2e22c-129">The Office Developer Tools for Visual Studio will do the following:</span></span>
    
 

      - <span data-ttu-id="2e22c-p105">Добавьте файл с именем AppEventReceiver.svc, содержащий скелетный код на языке C# (или VB.NET). Это служба, которая будет обрабатывать событие надстройки.</span><span class="sxs-lookup"><span data-stu-id="2e22c-p105">Add a file named AppEventReceiver.svc. that contains some skeletal C# (or VB.NET) code. This is the service that will handle the add-in event.</span></span>
    
 
  - <span data-ttu-id="2e22c-p106">В раздел **Свойства** файла AppManifest.xml добавляется следующая запись: `<InstalledEventEndpoint>~remoteAppUrl/AppEventReceiver.svc</InstalledEventEndpoint>`. Она регистрирует приемник событий надстройки в SharePoint. Обратите внимание, что маркер **~remoteAppUrl** также используется для удаленного веб-приложения в надстройке SharePoint, размещаемой у поставщика. Инструменты разработчика Office для Visual Studio предполагают, что домены веб-приложения и обработчика событий совпадают. В редких случаях, когда это не так, необходимо вручную заменить маркер **~remoteAppUrl** настоящим доменом службы.</span><span class="sxs-lookup"><span data-stu-id="2e22c-p106">The following entry is added to the  **Properties** section of the AppManifest.xml file: `<InstalledEventEndpoint>~remoteAppUrl/AppEventReceiver.svc</InstalledEventEndpoint>`. This entry registers the add-in event receiver to SharePoint. (Note that the  **~remoteAppUrl** token is the same one used for the remote web application in the provider-hosted SharePoint Add-in. The Office Developer Tools for Visual Studio assume the domain of the web application and the event handler is the same. In the rare case where it is not, you need to manually replace the token **~remoteAppUrl** with the actual domain of your service.)</span></span>
    
 
  - <span data-ttu-id="2e22c-p107">Если в проекте надстройки SharePoint еще нет веб-проекта, Инструменты разработчика Office для Visual Studio создадут его. Кроме того, эти инструменты настроят манифест надстройки для размещения у поставщика. Они также добавят страницы, сценарии, CSS-файлы и другие элементы. Если из удаленных компонентов надстройки требуется только веб-служба обработки событий, вы можете удалить их из проекта. Кроме того, проследите, чтобы элемент **StartPage** в манифесте надстройки не указывал на удаленную страницу.</span><span class="sxs-lookup"><span data-stu-id="2e22c-p107">If the SharePoint Add-in project doesn't already have a web project, the Office Developer Tools for Visual Studio create one. The tools also ensure that add-in manifest is configured for a provider-hosted add-in. They will also add pages, scripts, CSS files, and other artifacts. (If the only remote component that your add-in needs is the event-handling web service, you can delete these from the project. You also should ensure that the  **StartPage** element in the add-in manifest is not pointing to a page that you have deleted.)</span></span>
    
 
4. <span data-ttu-id="2e22c-p108">Если Visual Studio и ваша тестовая ферма SharePoint развернуты на разных компьютерах, настройте проект для отладки с помощью служебной шины Microsoft Azure. Дополнительные сведения см. в статье  [Устранение неполадок и отладка удаленного приемника событий в надстройке для SharePoint](debug-and-troubleshoot-a-remote-event-receiver-in-a-sharepoint-add-in.md).</span><span class="sxs-lookup"><span data-stu-id="2e22c-p108">If your test SharePoint farm is not on the same computer that is running Visual Studio, configure the project for debugging using the Microsoft Azure Service Bus. For more information, see  [Debug and troubleshoot a remote event receiver in a SharePoint Add-in](debug-and-troubleshoot-a-remote-event-receiver-in-a-sharepoint-add-in.md).</span></span> 
    
 
5. <span data-ttu-id="2e22c-p109">Если в файле AppEventReceiver.svc есть метод  `ProcessOneWayEvent`, его реализация должна содержать только строку  `throw new NotImplementedException();`, поскольку этот метод невозможно использовать в обработчике событий надстройки.  *Обработчики событий надстройки должны возвращать объект, который сообщает среде SharePoint, следует ли завершить событие или отменить его, а метод  `ProcessOneWayEvent` не возвращает никаких данных.*</span><span class="sxs-lookup"><span data-stu-id="2e22c-p109">If there is a  `ProcessOneWayEvent` method in the AppEventReceiver.svc file, it's implementation should consist of just the line `throw new NotImplementedException();`, because this method cannot be used in an add-in event handler.  *Add-in event handlers have to return an object that tells SharePoint whether to finish or roll back the event and the  `ProcessOneWayEvent` method doesn't return anything.*</span></span> 
    
 
6. <span data-ttu-id="2e22c-p110">Файл будет включать метод  `ProcessEvent`, который имеет следующий вид. (Он также может содержать блок кода, который иллюстрирует получение контекста клиента. Удалите или закомментируйте его.)</span><span class="sxs-lookup"><span data-stu-id="2e22c-p110">The file will include a  `ProcessEvent` method that looks something like the following. (There may also a block of code that illustrates how to get a client context. Delete it or comment out.)</span></span>
    
    <span data-ttu-id="2e22c-150">Обратите внимание на следующие особенности этого кода:</span><span class="sxs-lookup"><span data-stu-id="2e22c-150">Note the following about this code:</span></span>
    
      - <span data-ttu-id="2e22c-151">Объект  **SPRemoteEventProperties** отправляется веб-службе обработчика в виде сообщения SOAP, которое содержит контекстные сведения из SharePoint, включая свойство **EventType** , которое идентифицирует событие.</span><span class="sxs-lookup"><span data-stu-id="2e22c-151">The  **SPRemoteEventProperties** object is sent to your handler web service as a SOAP message that contains context information from SharePoint, including an **EventType** property that identifies the event.</span></span>
    
 
  - <span data-ttu-id="2e22c-p111">Объект **SPRemoteEventResult**, возвращаемый обработчиком, содержит свойство **Status**, которое может принимать значения **SPRemoteEventServiceStatus**.**Continue**, **SPRemoteEventServiceStatus.CancelNoError** и **SPRemoteEventServiceStatus.CancelWithError**. По умолчанию свойство **Status** имеет значение **Continue**, которое сообщает среде SharePoint, что необходимо завершить событие. Остальные два значения сообщают SharePoint, что нужно:</span><span class="sxs-lookup"><span data-stu-id="2e22c-p111">The  **SPRemoteEventResult** object that your handler returns contains a **Status** property whose possible values are **SPRemoteEventServiceStatus**. **Continue**,  **SPRemoteEventServiceStatus.CancelNoError**, and  **SPRemoteEventServiceStatus.CancelWithError**. The default value of the  **Status** property is **Continue**, which tells SharePoint to finish the event. The other two values tell SharePoint to:</span></span>
    
      - <span data-ttu-id="2e22c-156">Запустить обработчик более трех раз.</span><span class="sxs-lookup"><span data-stu-id="2e22c-156">Run your handler up to three more times.</span></span>
    
 
  - <span data-ttu-id="2e22c-157">Если обработчик по-прежнему получает состояние "Отмена", отмените событие и выполните полный откат всех изменений, выполненных в рамках этого события.</span><span class="sxs-lookup"><span data-stu-id="2e22c-157">If it is still getting a cancel status, cancel the event and roll back anything it has done as part of the event.</span></span> 
    
 



```C#
  public SPRemoteEventResult ProcessEvent(SPRemoteEventProperties properties)
{
    SPRemoteEventResult result = new SPRemoteEventResult();

    return result;
}
```

7. <span data-ttu-id="2e22c-158">Сразу после строки объявления переменной `result` добавьте следующую развилку, чтобы определить, какое событие обрабатывается.</span><span class="sxs-lookup"><span data-stu-id="2e22c-158">Immediately below the line that declares the  `result` variable, add the following switch structure to identify which event is being handled.</span></span>
    
```C#
  switch (properties.EventType)
{
    case SPRemoteEventType.AppInstalled:
        break;
    case SPRemoteEventType.AppUpgraded:
        break;
    case SPRemoteEventType.AppUninstalling:
        break;
}
```


     **Note**  The  **AppInstalled**,  **AppUpdated**, and  **AppInstalling** events, if you have handlers for them, will each get their own URL registered in the add-in manifest. So you *can*  have different endpoints for them; but this article (and the Office Developer Tools for Visual Studio) assume they have exactly the same endpoint; that's why the code needs to determine which event called it.
8. <span data-ttu-id="2e22c-p112">Как объясняется в разделе [Включение логики отката и логики проверки выполненных действий в обработчики событий надстроек](handle-events-in-sharepoint-add-ins.md#Rollback), если в логике установки происходит сбой, почти всегда следует отменять установку: среда SharePoint должна отменить действия, выполненные для установки, а вам нужно отменить все действия, выполненные обработчиком. Для этого можно добавить следующий код в оператор **case** для события AppInstalled.</span><span class="sxs-lookup"><span data-stu-id="2e22c-p112">As explained in  [Include rollback logic and "already done" logic in your add-in event handlers](handle-events-in-sharepoint-add-ins.md#Rollback), if anything goes wrong in your installation logic, you almost always want the add-in installation canceled, and you want SharePoint to roll back what it has done for the installation, and you want to roll back what your handler has done. One way to accomplish these goals is to add the following code inside the  **case** for the AppInstalled event.</span></span>
    
```C#
  case SPRemoteEventType.AppInstalled:
  try
  {
      // Add-in installed event logic goes here.
  }
  catch (Exception e)
  {
      result.ErrorMessage = e.ErrorMessage;
      result.Status = SPRemoteEventServiceStatus.CancelWithError;

      // Rollback logic goes here.
  }
  break;
```


     **Note**  Move installation code that takes more than 30 seconds into the add-in itself. You can add it to "first run" logic that executes the first time the add-in runs. The add-in can display a message saying something like "We're getting things ready for you." Alternatively, the add-in can prompt the user to run the initialization code.If "first run" logic is not feasible for your add-in, another option is to have your event handler start a remote asynchronous process and then immediately return a  **SPRemoteEventResult** object with the **Status** set to **Continue**. A weakness of this strategy is that if the remote process fails, it has no way to tell SharePoint to roll back the add-in installation.
9. <span data-ttu-id="2e22c-p113">Как описано в разделе  [Стратегии архитектуры обработчиков событий надстройки](handle-events-in-sharepoint-add-ins.md#Strategies), стратегия делегирования обработчиков, предпочтительна, но ее можно использовать не во всех сценариях. В данном примере показано, как реализовать стратегию делегирования обработчиков при добавлении списка на хост-сайт. (Сведения о том, как создать похожий обработчик события AppInstalled, не использующий стратегию делегирования обработчиков, см. в примере  [OfficeDev/PnP/Samples/Core.AppEvents](https://github.com/OfficeDev/PnP/tree/master/Samples/Core.AppEvents).)</span><span class="sxs-lookup"><span data-stu-id="2e22c-p113">As explained in  [Add-in event handler architecture strategies](handle-events-in-sharepoint-add-ins.md#Strategies), the handler delegation strategy is preferred, although not possible in every scenario. In the continuing example, we show you how to implement the handler delegation strategy when adding a list to the host web. (For information on how to create a similar AppInstalled event handler that does not use the handler delegation strategy, see the sample  [OfficeDev/PnP/Samples/Core.AppEvents](https://github.com/OfficeDev/PnP/tree/master/Samples/Core.AppEvents).)</span></span>
    
    <span data-ttu-id="2e22c-p114">Ниже представлена новая версия блока **case** для события AppInstalled. Обратите внимание, что логика инициализации, которая применяется ко всем событиям, находится над блоком **switch**. Так как устанавливаемый список будет удален в обработчике события AppUninstalling, этот список определяется там же.</span><span class="sxs-lookup"><span data-stu-id="2e22c-p114">The following is the new version of the AppInstalled  **case** block. Note that initialization logic that applies to all events goes above the **switch** block. Since the same list that is installed will be removed in the AppUninstalling handler, the list is identified there.</span></span>
    


```C#
  SPRemoteEventResult result = new SPRemoteEventResult();
String listTitle = "MyList";

switch (properties.EventType)
{               
    case SPRemoteEventType.AppInstalled:
                    
   try
   {
        string error = TryCreateList(listTitle, properties);
        if (error != String.Empty)
        {
            throw new Exception(error);            
        }
   }
    catch (Exception e)
   {
        // Tell SharePoint to cancel the event.
        result.ErrorMessage = e.Message;
        result.Status = SPRemoteEventServiceStatus.CancelWithError;               
    }
        break;
    case SPRemoteEventType.AppUpgraded:
       break;
    case SPRemoteEventType.AppUninstalling:
       break;
}                      
```

10. <span data-ttu-id="2e22c-p115">Добавьте метод создания списка в класс **AppEventReceiver** как частный метод **private** со следующим кодом. Обратите внимание, что класс `TokenHelper` содержит специальный метод, оптимизированный для получения контекста клиента для события надстройки. Значение **false** для последнего параметра указывает, что контекст предназначен для хост-сайта.</span><span class="sxs-lookup"><span data-stu-id="2e22c-p115">Add the list creation method to the  **AppEventReceiver** class as a **private** method with the following code. Note that the `TokenHelper` class has a special method that is optimized for getting a client context for an add-in event. Passing **false** for the last parameter ensures that the context is for the host web.</span></span>
    
```C#
  private string TryCreateList(String listTitle, SPRemoteEventProperties properties)
 {    
    string errorMessage = String.Empty;          

    using (ClientContext clientContext =
        TokenHelper.CreateAppEventClientContext(properties, useAppWeb: false))
    {
        if (clientContext != null)
        {
        }
    }
    return errorMessage;
}

```

11. <span data-ttu-id="2e22c-p116">Логика отката, по сути, является логикой обработки исключений, а SharePoint CSOM (клиентская объектная модель) включает область **ExceptionHandlingScope**, которая позволяет веб-службе делегировать обработку исключений серверу SharePoint (см. также статью [Использование области обработки исключений](http://msdn.microsoft.com/library/103619ef-1ba3-44e3-93e1-5e0685bc616e%28Office.15%29.aspx)). Добавьте следующий код в блок **if** предыдущего фрагмента.</span><span class="sxs-lookup"><span data-stu-id="2e22c-p116">Rollback logic is basically exception handling logic and the SharePoint CSOM (Client-side object model) has a  **ExceptionHandlingScope** that enables your web service to delegate exception handling to the SharePoint server. (See also, [How to: Use Exception Handling Scope](http://msdn.microsoft.com/library/103619ef-1ba3-44e3-93e1-5e0685bc616e%28Office.15%29.aspx).) Add the following code to the  **if** block in the preceding snippet.</span></span>
    
```C#
  ExceptionHandlingScope scope = new ExceptionHandlingScope(clientContext); 

using (scope.StartScope()) 
{ 
    using (scope.StartTry()) 
    { 
    }         
    using (scope.StartCatch()) 
    {                                 
    } 
    using (scope.StartFinally()) 
    { 
    } 
} 
 clientContext.ExecuteQuery();

if (scope.HasException)
{
    errorMessage = String.Format("{0}: {1}; {2}; {3}; {4}; {5}", 
        scope.ServerErrorTypeName, scope.ErrorMessage, 
        scope.ServerErrorDetails, scope.ServerErrorValue, 
        scope.ServerStackTrace, scope.ServerErrorCode);
}
```

12. <span data-ttu-id="2e22c-p117">В предыдущем фрагменте указан только один вызов SharePoint ( **ExecuteQuery**), но его недостаточно. Каждый объект, на который будет ссылаться область исключений, необходимо сначала загрузить в клиент. Для этого добавьте следующий код  *перед*  конструктором **ExceptionHandlingScope**.</span><span class="sxs-lookup"><span data-stu-id="2e22c-p117">There is only one call to SharePoint ( **ExecuteQuery**) in the preceding snippet, but unfortunately we can't quite do with only one. Every object that is going to be referenced in our exception scope has to first be loaded to the client. So add the following code  *above*  the constructor for the **ExceptionHandlingScope**.</span></span>
    
```C#
  ListCollection allLists = clientContext.Web.Lists;
IEnumerable<List> matchingLists =
    clientContext.LoadQuery(allLists.Where(list => list.Title == listTitle));
clientContext.ExecuteQuery();

var foundList = matchingLists.FirstOrDefault();
 List createdList = null;
```

13. <span data-ttu-id="2e22c-p118">Код для создания списка хост-сайтов добавляется в блок **StartTry**, но сначала код должен проверить, был ли уже добавлен этот список (как описывается в разделе [Включение логики отката и логики проверки выполненных действий в обработчики событий надстроек](handle-events-in-sharepoint-add-ins.md#Rollback)). Логику If-Then-Else можно делегировать серверу SharePoint с помощью класса **ConditionalScope** (см. также статью [Использование условной области](http://msdn.microsoft.com/library/560112e9-c3ed-4b8f-9cd4-c8bc5d60d63c%28Office.15%29.aspx)). Добавьте следующий код в блок **StartTry**.</span><span class="sxs-lookup"><span data-stu-id="2e22c-p118">The code to create a host web list will go into the  **StartTry** block, but the code must first check whether the list has already been added (as explained in [Include rollback logic and "already done" logic in your add-in event handlers](handle-events-in-sharepoint-add-ins.md#Rollback)). If-then-else logic can be delegated to the SharePoint server by using the  **ConditionalScope** class. (See also, [How to: Use Conditional Scope](http://msdn.microsoft.com/library/560112e9-c3ed-4b8f-9cd4-c8bc5d60d63c%28Office.15%29.aspx).) Add the following code inside the  **StartTry** block.</span></span>
    
```C#
  ConditionalScope condScope = new ConditionalScope(clientContext, 
        () => foundList.ServerObjectIsNull.Value == true, true);
using (condScope.StartScope())
{
    ListCreationInformation listInfo = new ListCreationInformation();
    listInfo.Title = listTitle;
    listInfo.TemplateType = (int)ListTemplateType.GenericList;
    listInfo.Url = listTitle;
    createdList = clientContext.Web.Lists.Add(listInfo);                                
}
```

14. <span data-ttu-id="2e22c-p119">Блок  **StartCatch** должен отменить создание списка, но для начала он должен проверить, создан ли список, так как исключение могло быть вызвано в блоке **StartTry** до того, как создание списка было завершено. Добавьте следующий код в блок **StartCatch**.</span><span class="sxs-lookup"><span data-stu-id="2e22c-p119">The  **StartCatch** block should undo the creation of the list, but it needs to first check that the list was created, because an exception might have been thrown in the **StartTry** block before it finished creating the list. Add the following code to the **StartCatch** block.</span></span>
    
```C#
  ConditionalScope condScope = new ConditionalScope(clientContext, 
        () => createdList.ServerObjectIsNull.Value != true, true);
using (condScope.StartScope())
{
    createdList.DeleteObject();
} 
```


     **Tip**   **TROUBLESHOOTING:** To test whether your **StartCatch** block is entered when it should be, you need a way to throw a runtime exception on the SharePoint server. Using a **throw** or dividing by zero won't work because they cause *client-side*  exceptions before the client runtime can even bundle up the code and send it to the server (with the **ExecuteQuery** method). Instead, add the following lines to the **StartTry** block. The client-side runtime accepts this, but it causes a server-side exception, which is what you want. `List fakeList = clientContext.Web.Lists.GetByTitle("NoSuchList");`
 
 `clientContext.Load(fakeList);`

    The entire TryCreateList method should look like the following. (The  **StartFinally** block is required even when it is not being used.)
    


```C#
  private string TryCreateList(String listTitle, SPRemoteEventProperties properties)
{    
    string errorMessage = String.Empty;  

    using (ClientContext clientContext = 
        TokenHelper.CreateAppEventClientContext(properties, useAppWeb: false))
    {
        if (clientContext != null)
        {
            ListCollection allLists = clientContext.Web.Lists;
            IEnumerable<List> matchingLists = 
                clientContext.LoadQuery(allLists.Where(list => list.Title == listTitle));
            clientContext.ExecuteQuery();
            var foundList = matchingLists.FirstOrDefault();
            List createdList = null;

            ExceptionHandlingScope scope = new ExceptionHandlingScope(clientContext); 
            using (scope.StartScope()) 
            { 
                using (scope.StartTry()) 
                { 
                    ConditionalScope condScope = new ConditionalScope(clientContext, 
                            () => foundList.ServerObjectIsNull.Value == true, true);  
                    using (condScope.StartScope())
                    {
                        ListCreationInformation listInfo = new ListCreationInformation();
                        listInfo.Title = listTitle;
                        listInfo.TemplateType = (int)ListTemplateType.GenericList;
                        listInfo.Url = listTitle;
                        createdList = clientContext.Web.Lists.Add(listInfo);
                    }
                } 
                
                using (scope.StartCatch()) 
                { 
                    ConditionalScope condScope = new ConditionalScope(clientContext, 
                            () => createdList.ServerObjectIsNull.Value != true, true);
                    using (condScope.StartScope())
                    {
                        createdList.DeleteObject();
                    }    
                } 

                using (scope.StartFinally()) 
                { 
                } 
            } 
            clientContext.ExecuteQuery();

            if (scope.HasException)
            {
                    errorMessage = String.Format("{0}: {1}; {2}; {3}; {4}; {5}", 
                    scope.ServerErrorTypeName, scope.ErrorMessage, 
                    scope.ServerErrorDetails, scope.ServerErrorValue, 
                    scope.ServerStackTrace, scope.ServerErrorCode);
            }
        }
    }
    return errorMessage;
}
```


     **Tip**   **DEBUGGING:** Regardless of whether you are using the handler delegation strategy, when you are stepping through the code with the debugger, keep in mind that, in any scenario in which your handler returns a cancel status, SharePoint is going to call your handler again, up to three more times. So the debugger will cycle through the code up to four times.

     **Tip**   **CODE ARCHITECTURE:** Since you can install components on the add-in web with declarative markup outside your handler, you usually won't want to use up any of the 30 seconds your handler has available to interact with the add-in web. But if you do, keep in mind that your code requires a separate **ClientContext** object for the add-in web. This means that the add-in web and host web are different components, just as much as an SQL Server database is different from each of them. So a method that calls to the add-in web is in the **try** block of the AppInstalled **case** block, just like the TryCreateList method in the continuing example. However, your handler does *not*  need to roll back actions taken on the add-in web. If it encounters an error, it only needs to cancel the event, because SharePoint will delete the entire add-in web if the event is cancelled.

## <a name="create-an-add-in-uninstalling-event-receiver"></a><span data-ttu-id="2e22c-180">Создание приемника для события удаления надстройки</span><span class="sxs-lookup"><span data-stu-id="2e22c-180">Create an add-in uninstalling event receiver</span></span>
<span data-ttu-id="2e22c-181"><a name="SP15appevent_prereq"> </a></span><span class="sxs-lookup"><span data-stu-id="2e22c-181"><a name="SP15appevent_prereq"> </a></span></span>


1. <span data-ttu-id="2e22c-p120">Задайте для свойства **Управление удалением надстроек** проекта значение **True**. Инструменты *не* создают еще один файл веб-службы, если такой файл уже существует, но добавляют элемент **UninstallingEventEndpoint** в манифест надстройки.</span><span class="sxs-lookup"><span data-stu-id="2e22c-p120">Set the  **Handle Add-in Uninstalling** property of the project to **True**. The tools do  *not*  create another web service file, if one already exists; but they do add an **UninstallingEventEndpoint** element to the add-in manifest.</span></span>
    
 
2. <span data-ttu-id="2e22c-p121">Код в блоке **case** события AppUninstalling должен удалять элементы надстройки, в которых нет необходимости после удаления этой надстройки из второй корзины. Тем не менее, по мере возможности следует "утилизировать" компоненты, а не полностью удалять их. Это связано с тем, что в случае отмены события удаления их потребуется восстановить. В этом случае надстройка останется во второй корзине, а пользователь сможет восстановить ее и использовать снова. Для восстановления работоспособности надстройки может быть достаточно заново создать удаленный компонент, но все данные и параметры конфигурации в компоненте будут потеряны.</span><span class="sxs-lookup"><span data-stu-id="2e22c-p121">Code in the AppUninstalling  **case** block should remove artifacts of the add-in that aren't needed after the add-in is removed from the second stage recycle bin, which is what triggers the event. However, whenever possible you need to "retire" the components rather than totally delete them. This is because, you need to restore them if the uninstalling event has to be rolled back. If that happens, the add-in is still in the second stage recycle bin and a user could restore it and start using it again. Merely recreating a deleted component in your rollback logic might be enough to enable the add-in to work again, but any data or configuration settings in the component would be lost.</span></span>
    
    <span data-ttu-id="2e22c-p122">Эту стратегию относительно легко использовать для компонентов SharePoint, так как в SharePoint есть корзина, из которой можно восстанавливать объекты, а также существуют API-интерфейсы CSOM для доступа к ней. В следующих разделах показано, как это сделать. Для других платформ могут потребоваться другие методы. Например, если вам нужно удалить строку из таблицы SQL Server в обработчике удаления надстройки, хранимая процедура T-SQL в обработчике может добавить в таблицу столбец IsDeleted и присвоить ему значение **True** в этой строке. Если в процедуре произойдет ошибка, логика отката восстановит значение **False**. Если процедура выполнится без ошибок, то непосредственно перед возвратом соответствующего флага она может задать таймер, чтобы удалить эту строку позже.</span><span class="sxs-lookup"><span data-stu-id="2e22c-p122">This strategy is relatively easy for SharePoint components, since SharePoint has a recycle bin from which things can be restored, and there are CSOM APIs for accessing it. Later steps of this procedure show how. For other platforms, different techniques may be needed. For example, if you want to retire a row in an SQL Server table in your add-in uninstalling handler, a T-SQL stored procedure in the handler can add an IsDeleted column to the table and set it to  **True** for the row. If the procedure encounters an error, the rollback logic resets the value to **False**. If the procedure completes without error, then just before it returns a success flag, it can set a timer job to delete the row later.</span></span>
    
    <span data-ttu-id="2e22c-195">Иногда требуется сохранить данные, например списки, даже после удаления надстройки, но в качестве примера ниже представлен обработчик события, который удаляет список, созданный обработчиком события установки.</span><span class="sxs-lookup"><span data-stu-id="2e22c-195">Sometimes you want to keep data, such as lists, even after the add-in is deleted; but as an example for this article, the following is an uninstalling event handler that deletes the list that was created with the installed event handler.</span></span>
    


```C#
  case SPRemoteEventType.AppUninstalling:

try
{
    string error = TryRecycleList(listTitle, properties);
    if (error != String.Empty)
    {
        throw new Exception(error);
    }
}
catch (Exception e)
{
    // Tell SharePoint to cancel the event.
    result.ErrorMessage = e.Message;
    result.Status = SPRemoteEventServiceStatus.CancelWithError;
}
break;
```

3. <span data-ttu-id="2e22c-p123">Добавьте вспомогательный метод для повторного использования списка. Обратите внимание на следующие особенности этого кода:</span><span class="sxs-lookup"><span data-stu-id="2e22c-p123">Add the helper method for recycling the list. Note the following about this code:</span></span>
    
      - <span data-ttu-id="2e22c-p124">Код перемещает список в корзину, а не безвозвратно удаляет его. Это позволяет восстановить список, включая все данные, в случае сбоя события, что и делает блок **StartCatch**. Таким образом, если метод выполнится успешно, а событие завершится, то надстройка будет безвозвратно удалена из второй корзины, но список останется в первой корзине.</span><span class="sxs-lookup"><span data-stu-id="2e22c-p124">The code recycles the list, instead of permanently deleting it. This makes it possible to restore it, including its data, if the event fails, which is what the  **StartCatch** block does. So, if the method succeeds and the event completes, the add-in is permanently deleted from the second stage recycle bin, but the list is still in the first stage recycle bin.</span></span>
    
 
  - <span data-ttu-id="2e22c-p125">Код проверяет наличие списка, прежде чем удалять его, поскольку пользователь уже мог удалить список с помощью пользовательского интерфейса SharePoint. Аналогичным образом, код отката проверяет наличие списка в корзине, прежде чем восстанавливать его, поскольку пользователь мог восстановить список или переместить его на второй уровень корзины.</span><span class="sxs-lookup"><span data-stu-id="2e22c-p125">The code tests for the existence of the list before it recycles it because a user might have already recycled it in the SharePoint UI. Similiarly, the rollback code checks for the existence of the list in the recycle bin before it restores it, because a user might have already restored it or moved it to the second-stage recycle bin.</span></span> 
    
 
  - <span data-ttu-id="2e22c-p126">Есть две условных области, которые проверяют существование списка, определяя, имеет ли ссылка на него значение **null**. Но обе области содержат внутренний блок **if**, который повторно проверяет тот же объект на нулевое значение. Внешние проверки с блоками условных областей выполняются на сервере, но внутренние проверки также необходимы. Это связано с тем, что среда выполнения клиента построчно просматривает код для создания XML-сообщения, которое метод **ExecuteQuery** отправит на сервер. По достижении ссылок на объекты **foundList** и **recycledList** одна из этих строк вызывает исключение Null Reference, если они не заключены во внутренние проверки на нулевые ссылки.</span><span class="sxs-lookup"><span data-stu-id="2e22c-p126">There are two conditional scopes that test for a list's existence by checking to see if a reference to it is  **null**. But both of them have an inner  **if** block that test the very same object for nullity a second time. The outer tests, with conditional scope blocks, run on the server, but the inner nullity tests are also needed. This is because the client runtime moves through the code line-by-line to create the XML message that the **ExecuteQuery** method will send to the server. When the references to the **foundList** and **recycledList** objects are reached, one or another of these lines throws a Null Reference exception unless they are encased inside the inner nullity checks.</span></span>
    
 

```C#
  private string TryRecycleList(String listTitle, SPRemoteEventProperties properties)
{
    string errorMessage = String.Empty;

    using (ClientContext clientContext = 
        TokenHelper.CreateAppEventClientContext(properties, useAppWeb: false))
    {
        if (clientContext != null)
        {
            ListCollection allLists = clientContext.Web.Lists;
            IEnumerable<List> matchingLists = 
                clientContext.LoadQuery(allLists.Where(list => list.Title == listTitle));
            RecycleBinItemCollection bin = clientContext.Web.RecycleBin;
            IEnumerable<RecycleBinItem> matchingRecycleBinItems = 
                clientContext.LoadQuery(bin.Where(item => item.Title == listTitle));        
            clientContext.ExecuteQuery();

            List foundList = matchingLists.FirstOrDefault();
            RecycleBinItem recycledList = matchingRecycleBinItems.FirstOrDefault();    

            ExceptionHandlingScope scope = new ExceptionHandlingScope(clientContext);
            using (scope.StartScope())
            {
                using (scope.StartTry())
                {
                    ConditionalScope condScope = new ConditionalScope(clientContext, 
                        () => foundList.ServerObjectIsNull.Value == false, true);
                    using (condScope.StartScope())
                    {
                        if (foundList != null)
                        {
                            foundList.Recycle();
                        }
                    }
                }
                using (scope.StartCatch())
                {
                    ConditionalScope condScope = new ConditionalScope(clientContext, 
                         () => recycledList.ServerObjectIsNull.Value == false, true);
                    using (condScope.StartScope())
                    {
                        if (recycledList != null)
                        {
                            recycledList.Restore(); 
                        }
                    }
                }
                using (scope.StartFinally())
                {
                }
            }
            clientContext.ExecuteQuery();

            if (scope.HasException)
            {
                errorMessage = String.Format("{0}: {1}; {2}; {3}; {4}; {5}", 
                    scope.ServerErrorTypeName, scope.ErrorMessage, 
                    scope.ServerErrorDetails, scope.ServerErrorValue, 
                    scope.ServerStackTrace, scope.ServerErrorCode);
            }
        }
    }
    return errorMessage;
}
```


### <a name="to-debug-and-test-an-add-in-uninstalling-event-receiver"></a><span data-ttu-id="2e22c-208">Отладка и проверка приемника для события удаления надстройки</span><span class="sxs-lookup"><span data-stu-id="2e22c-208">To debug and test an add-in uninstalling event receiver</span></span>


1. <span data-ttu-id="2e22c-209">Откройте все перечисленные ниже страницы в отдельных окнах или вкладках.</span><span class="sxs-lookup"><span data-stu-id="2e22c-209">Open all of the following pages in separate windows or tabs:</span></span>
    
      -  <span data-ttu-id="2e22c-210">**Контент сайта**.</span><span class="sxs-lookup"><span data-stu-id="2e22c-210">**Site Contents**</span></span>
    
 
  -  <span data-ttu-id="2e22c-211">**Контент сайта — Корзина** (_layouts/15/AdminRecycleBin.aspx?ql=1).</span><span class="sxs-lookup"><span data-stu-id="2e22c-211">**Site Settings - Recycle Bin** (_layouts/15/AdminRecycleBin.aspx?ql=1)</span></span>
    
 
  -  <span data-ttu-id="2e22c-212">**Корзина — Вторая корзина** (_layouts/15/AdminRecycleBin.aspxView=2&amp;?ql=1).</span><span class="sxs-lookup"><span data-stu-id="2e22c-212">**Recycle Bin - Second-Stage Recycle Bin** (_layouts/15/AdminRecycleBin.aspxView=2&amp;?ql=1)</span></span>
    
 
2. <span data-ttu-id="2e22c-p127">Нажмите клавишу F5 и подтвердите доверие надстройке по запросу. Откроется начальная страница надстройки. Если вы собираетесь лишь протестировать обработчик удаления, окно браузера можно закрыть.  *Но если вы отлаживаете обработчик, оставьте его открытым. При закрытии окна сеанс отладки завершится.*</span><span class="sxs-lookup"><span data-stu-id="2e22c-p127">Press F5 and trust the add-in when prompted. The add-in's start page opens. If you are only going to test the uninstallation handler, you can close this browser window.  *But if you are debugging the handler, leave it open. Closing it will end the debugging session.*</span></span> 
    
 
3. <span data-ttu-id="2e22c-217">Обновите страницу **Контент сайта**, а когда откроется надстройка, удалите ее.</span><span class="sxs-lookup"><span data-stu-id="2e22c-217">Refresh the  **Site Contents** page, and when the add-in appears, remove it.</span></span>
    
 
4. <span data-ttu-id="2e22c-p128">Обновите страницу **Параметры сайта — Корзина**. Надстройка появится в начале списка. Установите флажок рядом с ней и выберите **Удалить выделенные объекты**.</span><span class="sxs-lookup"><span data-stu-id="2e22c-p128">Refresh the  **Site Settings - Recycle Bin** page. The add-in will appear as the top item. Select the check box beside it and click **Delete Selection**.</span></span>
    
 
5. <span data-ttu-id="2e22c-p129">Обновите страницу **Корзина — Вторая корзина**. Надстройка появится в начале списка. Установите флажок рядом с ней и выберите элемент **Удалить выделенные объекты**. SharePoint сразу вызовет обработчик удаления надстройки.</span><span class="sxs-lookup"><span data-stu-id="2e22c-p129">Refresh the  **Recycle Bin - Second-Stage Recycle Bin** page. The add-in will appear as the top item. Select the checkbox beside it and click **Delete Selection**. SharePoint will immediately call your add-in uninstalling handler.</span></span>
    
 

## <a name="create-an-add-in-updated-event-receiver"></a><span data-ttu-id="2e22c-225">Создание приемника для события обновления надстройки</span><span class="sxs-lookup"><span data-stu-id="2e22c-225">Create an add-in updated event receiver</span></span>
<span data-ttu-id="2e22c-226"><a name="SP15appevent_prereq"> </a></span><span class="sxs-lookup"><span data-stu-id="2e22c-226"><a name="SP15appevent_prereq"> </a></span></span>

<span data-ttu-id="2e22c-227">Дополнительные сведения о создании обработчика для события обновления надстройки см. в статье [Создание обработчика для события обновления в надстройках SharePoint](create-a-handler-for-the-update-event-in-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="2e22c-227">For details about creating an add-in updated handler, see  [Create a handler for the update event in SharePoint Add-ins](create-a-handler-for-the-update-event-in-sharepoint-add-ins.md).</span></span>
 

 

## <a name="url-and-hosting-restrictions-on-production-add-in-event-receivers"></a><span data-ttu-id="2e22c-228">Ограничения, налагаемые на URL-адрес и размещение производственных приемников для событий надстройки</span><span class="sxs-lookup"><span data-stu-id="2e22c-228">URL and hosting restrictions on production add-in event receivers</span></span>
<span data-ttu-id="2e22c-229"><a name="SP15appevent_prereq"> </a></span><span class="sxs-lookup"><span data-stu-id="2e22c-229"><a name="SP15appevent_prereq"> </a></span></span>

<span data-ttu-id="2e22c-p130">Приемник событий надстройки можно разместить в облаке или на локальном сервере, который не используется в качестве сервера SharePoint. URL-адрес производственного приемника не может использовать определенный порт. Это значит, что вам необходимо использовать порт 443 для HTTPS (рекомендовано) или порт 80 для HTTP. При использовании HTTPS, если приемник размещен локально, а надстройка на Microsoft SharePoint Online, сервер размещения должен иметь доверенный сертификат, выданный центром сертификации. (Самозаверяющий сертификат действует, только если надстройка расположена в локальной ферме SharePoint.)</span><span class="sxs-lookup"><span data-stu-id="2e22c-p130">The add-in event receiver can be hosted in the cloud or in an on-premise server that is not also being used as a SharePoint server. The URL of a production receiver cannot specify a particular port. This means that you must use either port 443 for HTTPS, which we recommend, or port 80 for HTTP. If you are using HTTPS and the receiver service is hosted on-premise, but the add-in is on Microsoft SharePoint Online, then the hosting server must have a publically trusted certificate from a certificate authority. (A self-signed certificate works only if the add-in is in an on-premise SharePoint farm.)</span></span>
 

 

## <a name="additional-resources"></a><span data-ttu-id="2e22c-235">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="2e22c-235">Additional resources</span></span>
<span data-ttu-id="2e22c-236"><a name="SP15appevent_addlresources"> </a></span><span class="sxs-lookup"><span data-stu-id="2e22c-236"><a name="SP15appevent_addlresources"> </a></span></span>


-  [<span data-ttu-id="2e22c-237">Обработка событий в надстройках SharePoint</span><span class="sxs-lookup"><span data-stu-id="2e22c-237">Handle events in SharePoint Add-ins</span></span>](handle-events-in-sharepoint-add-ins.md)
    
 

