# <a name="create-a-remote-event-receiver-in-sharepoint-add-ins"></a><span data-ttu-id="c2dae-101">Создание удаленного приемника событий в надстройках SharePoint</span><span class="sxs-lookup"><span data-stu-id="c2dae-101">Create a remote event receiver in SharePoint Add-ins</span></span>
<span data-ttu-id="c2dae-102">Создание удаленного приемника событий, обрабатывающего события списка и элементов списка в надстройке SharePoint.</span><span class="sxs-lookup"><span data-stu-id="c2dae-102">Create a remote event receiver (RER) that handles list and list item events in a SharePoint Add-in.</span></span>
 

 <span data-ttu-id="c2dae-p101">**Примечание.** В настоящее время идет процесс замены названия "приложения для SharePoint" названием "надстройки SharePoint". Во время этого процесса в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio может по-прежнему использоваться термин "приложения для SharePoint". Дополнительные сведения см. в статье [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="c2dae-p101">The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span></span>
 


## <a name="prerequisites"></a><span data-ttu-id="c2dae-106">Необходимые компоненты</span><span class="sxs-lookup"><span data-stu-id="c2dae-106">Prerequisites</span></span>
<span data-ttu-id="c2dae-107"><a name="SP15appevent_prereq"> </a></span><span class="sxs-lookup"><span data-stu-id="c2dae-107"></span></span>

<span data-ttu-id="c2dae-p102">Для начала желательно иметь представление о надстройках Надстройки SharePoint с размещением у поставщика, а также разработать несколько надстроек, которые были бы хоть немного сложнее, чем "Hello World". Кроме того, следует ознакомиться со статьей  [Обработка событий в надстройках SharePoint](handle-events-in-sharepoint-add-ins).</span><span class="sxs-lookup"><span data-stu-id="c2dae-p102">It is helpful if you first have an understanding of provider-hosted SharePoint Add-ins, and for you to have developed a few that go a least a little beyond the "Hello World" level. Also, you should be familiar with  [Handle events in SharePoint Add-ins](handle-events-in-sharepoint-add-ins).</span></span> 
 

 

## <a name="create-a-remote-event-receiver"></a><span data-ttu-id="c2dae-110">Создание удаленного приемника событий</span><span class="sxs-lookup"><span data-stu-id="c2dae-110">Create a remote event receiver</span></span>
<span data-ttu-id="c2dae-111"><a name="MakeRER"> </a></span><span class="sxs-lookup"><span data-stu-id="c2dae-111"></span></span>

<span data-ttu-id="c2dae-p103">В этой статье показано, как усовершенствовать Надстройка SharePoint, добавив удаленный приемник событий (RER), который обрабатывает событие ItemAdded для пользовательского списка на сайте надстройки. Удаленный приемник событий регистрируется на сайте надстройки с помощью декларативной разметки. (Удаленные приемники событий регистрируются на  *хост-сайте*  программно. Соответствующий пример кода см. в статье [OfficeDev/PnP/Samples/Core.EventReceivers](https://github.com/OfficeDev/PnP/tree/master/Samples/Core.EventReceivers).)</span><span class="sxs-lookup"><span data-stu-id="c2dae-p103">This article shows how you extend a SharePoint Add-in by adding a remote event receiver (RER) that handles the ItemAdded event for a custom list in the add-in web. The RER is registered with the add-in web using declarative markup. RERs are registered with the  *host web*  programmatically. For a code sample that does so, see [OfficeDev/PnP/Samples/Core.EventReceivers](https://github.com/OfficeDev/PnP/tree/master/Samples/Core.EventReceivers).</span></span>
 

 
<span data-ttu-id="c2dae-p104">Приемник удаленных событий должен быть веб-службой SOAP. В этом примере он реализован как служба Windows Communication Foundation (WCF). Но его возможно реализовать в стеке не от Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="c2dae-p104">An RER must be a SOAP web service. The continuing example implements this as a Windows Communication Foundation (WCF) service; but it is possible in principle to implement an RER on a non-Microsoft stack.</span></span>
 

 
<span data-ttu-id="c2dae-118">Чтобы следовать приведенным здесь указаниям и ввести код самостоятельно, скачайте пример из репозитория  [SharePoint-Add-in-CSOM-BasicDataOperations](https://github.com/OfficeDev/SharePoint-Add-in-CSOM-BasicDataOperations), а затем откройте его в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c2dae-118">To follow along with this article and enter the code yourself, download the sample from  [SharePoint-Add-in-CSOM-BasicDataOperations](https://github.com/OfficeDev/SharePoint-Add-in-CSOM-BasicDataOperations), and then open the sample in Visual Studio.</span></span>
 

 

 <span data-ttu-id="c2dae-p105">**Примечание.** В этом примере используется файл TokenHelper.cs, созданный пакетом Инструменты разработчика Office для Visual Studio. На момент создания примера это была последняя версия, но сейчас она может быть устаревшей. Тем не менее этот пример отлично подходит для создания первого удаленного приемника событий. Когда вы будете готовы двигаться дальше, ознакомьтесь с примерами в разделе "Дальнейшие действия" ниже. Скорее всего, они будут оставаться актуальными.</span><span class="sxs-lookup"><span data-stu-id="c2dae-p105">**Note** This sample use a TokenHelper.cs file that is generated by Office Developer Tools for Visual Studio. It was the current version when the sample was created, but may not be the most recent version when you read this. The sample is still great for creating your first RER. But when you are ready to move beyond that, you should look at the samples listed in the Next Steps section below. They are more likely to be kept up-to-date.</span></span>
 


### <a name="to-register-a-remote-event-receiver"></a><span data-ttu-id="c2dae-124">Регистрация удаленного приемника событий</span><span class="sxs-lookup"><span data-stu-id="c2dae-124">To register a remote event receiver</span></span>


1. <span data-ttu-id="c2dae-125">Откройте проект надстройки SharePoint в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c2dae-125">Open the SharePoint Add-in project in Visual Studio.</span></span> 
    
 
2.  <span data-ttu-id="c2dae-126">В **обозревателе решений** выберите узел проекта надстройки.</span><span class="sxs-lookup"><span data-stu-id="c2dae-126">In **Solution Explorer**, choose the add-in project's node.</span></span>
    
 
3. <span data-ttu-id="c2dae-127">В строке меню выберите пункты **Проект** и **Добавить новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="c2dae-127">On the menu bar, choose **Project**, **Add New Item**.</span></span>
    
 
4. <span data-ttu-id="c2dae-128">В области **Установленные шаблоны** выберите узел **Office/SharePoint**.</span><span class="sxs-lookup"><span data-stu-id="c2dae-128">In the **Installed Templates** pane, choose the **Office SharePoint** node.</span></span>
    
 
5. <span data-ttu-id="c2dae-129">В области **Шаблоны** выберите шаблон **Удаленный приемник событий**.</span><span class="sxs-lookup"><span data-stu-id="c2dae-129">In the **Templates** pane, choose the **Remote Event Receiver** template.</span></span>
    
 
6. <span data-ttu-id="c2dae-130">В поле **Имя** оставьте имя, указанное по умолчанию (RemoteEventReceiver1), а затем нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="c2dae-130">In the **Name** box, keep the default name (RemoteEventReceiver1), and then choose the **Add** button.</span></span>
    
 
7. <span data-ttu-id="c2dae-131">В списке **Тип приемника событий:** выберите пункт **События элемента списка**.</span><span class="sxs-lookup"><span data-stu-id="c2dae-131">In the **What type of event receiver do you want?** list, choose **List Item Events**.</span></span>
    
 
8. <span data-ttu-id="c2dae-132">В списке **Элемент, который должен быть источником событий:** выберите **Настраиваемый список**.</span><span class="sxs-lookup"><span data-stu-id="c2dae-132">In the **What item should be the event source?** list, choose **Custom List**.</span></span>
    
    <span data-ttu-id="c2dae-p106">В этом примере используется настраиваемый универсальный список. Тем не менее удаленный приемник событий также может обрабатывать события, которые возникают в стандартных списках SharePoint, например **Объявления** или **Контакты**.</span><span class="sxs-lookup"><span data-stu-id="c2dae-p106">The continuing example uses a custom generic list. But an RER can also handle events that occur in standard SharePoint lists, such as **Announcements** or **Contacts**.</span></span>
    
 
9. <span data-ttu-id="c2dae-135">В списке **Обработать следующие события:** выберите пункт **Добавляется элемент**, а затем нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="c2dae-135">In the **Handle the following events** list, choose **An item is being added**, and then choose the **Finish** button.</span></span>
    
    <span data-ttu-id="c2dae-p107">К веб-приложению добавляется веб-служба, чтобы обрабатывать указанное удаленное событие. В Надстройка SharePoint добавляется приемник удаленных событий, а ссылка на элемент списка добавляется в файл Elements.xml приемника, который хранится в компоненте сайта надстройки.</span><span class="sxs-lookup"><span data-stu-id="c2dae-p107">A web service is added to the web application to handle the remote event that you specified. A remote event receiver is added to the SharePoint Add-in and the list item event is referenced in the receiver's Elements.xml file that is itself contained in the add-in web Feature.</span></span>
    
 

### <a name="to-create-the-list"></a><span data-ttu-id="c2dae-138">Создание списка</span><span class="sxs-lookup"><span data-stu-id="c2dae-138">To create the list</span></span>


1. <span data-ttu-id="c2dae-139">В **обозревателе решений** выберите узел проекта надстройки.</span><span class="sxs-lookup"><span data-stu-id="c2dae-139">In **Solution Explorer** select the add-in project's node.</span></span>
    
 
2. <span data-ttu-id="c2dae-140">В строке меню выберите пункты **Проект** и **Добавить новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="c2dae-140">On the menu bar, choose **Project**, **Add New Item**.</span></span>
    
 
3. <span data-ttu-id="c2dae-141">В области **Установленные шаблоны** выберите узел **Office/SharePoint**.</span><span class="sxs-lookup"><span data-stu-id="c2dae-141">In the **Installed Templates** pane, choose the **Office SharePoint** node.</span></span>
    
 
4. <span data-ttu-id="c2dae-142">В области **Шаблоны** выберите шаблон **Список**.</span><span class="sxs-lookup"><span data-stu-id="c2dae-142">In the **Templates** pane, choose the **List** template.</span></span>
    
 
5. <span data-ttu-id="c2dae-143">В поле **Имя** оставьте имя, указанное по умолчанию (List1), а затем нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="c2dae-143">In the **Name** box, leave the default name (List1), and then choose the **Add** button.</span></span>
    
 
6. <span data-ttu-id="c2dae-144">Выберите вариант **Создать экземпляр списка на основе существующего шаблона списка**, щелкните в списке пункт **Настраиваемый список** и нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="c2dae-144">Choose the **Create a list instance based on an existing list template** option button, choose **Custom List** in the list, and then choose the **Finish** button.</span></span>
    
 

### <a name="to-add-functionality-to-the-remote-event-receiver"></a><span data-ttu-id="c2dae-145">Добавление функций в удаленный приемник событий</span><span class="sxs-lookup"><span data-stu-id="c2dae-145">To add functionality to the remote event receiver</span></span>


1. <span data-ttu-id="c2dae-p108">Если тестовая ферма SharePoint и Visual Studio работают на разных компьютерах (или в качестве тестового сайта SharePoint используется область клиентов SharePoint Online), настройте проект для отладки с помощью служебной шины Microsoft Azure. Дополнительные сведения см. в статье  [Устранение неполадок и отладка удаленного приемника событий в надстройке для SharePoint](debug-and-troubleshoot-a-remote-event-receiver-in-a-sharepoint-add-in).</span><span class="sxs-lookup"><span data-stu-id="c2dae-p108">If your test SharePoint farm is not on the same computer that is running Visual Studio, (or you are using an SharePoint Online tenancy as your test SharePoint site), configure the project for debugging using the Microsoft Azure Service Bus. For more information, see the  [Debug and troubleshoot a remote event receiver in a SharePoint Add-in](debug-and-troubleshoot-a-remote-event-receiver-in-a-sharepoint-add-in).</span></span> 
    
 
2. <span data-ttu-id="c2dae-148">Замените содержимое файла кода для службы удаленного приемника событий (то есть в файле RemoteEventReceiver1.svc.cs) указанным ниже кодом.</span><span class="sxs-lookup"><span data-stu-id="c2dae-148">In the code file for the service of the remote event receiver (that is, RemoteEventReceiver1.svc.cs), replace the contents with the following code.</span></span>
    
    <span data-ttu-id="c2dae-149">Этот код выполняет следующие задачи.</span><span class="sxs-lookup"><span data-stu-id="c2dae-149">This code performs the following tasks.</span></span>
    
      - <span data-ttu-id="c2dae-150">Возвращает допустимый объект контекста клиента.</span><span class="sxs-lookup"><span data-stu-id="c2dae-150">Gets a valid client context object.</span></span> 
    
 
  - <span data-ttu-id="c2dae-151">Если списка с именем **EventLog** еще не существует, код создает такой список и заполняет его именами возникающих удаленных событий.</span><span class="sxs-lookup"><span data-stu-id="c2dae-151">If a list that's named **EventLog** doesn't already exist, creates one to contain the names of the remote events that occur.</span></span>
    
 
  - <span data-ttu-id="c2dae-152">Добавляет запись в список для события, включая метку даты и времени.</span><span class="sxs-lookup"><span data-stu-id="c2dae-152">Adds an entry to the list for the event, including a time and date stamp.</span></span>
    
 

     <span data-ttu-id="c2dae-p109">**Примечание.** На момент написания статьи при создании приемника пакет Инструменты разработчика Office для Visual Studio добавляет ссылки на все необходимые сборки, но в более поздних версиях такой возможности может не быть. Если компилятор выдает ошибку, просто добавьте недостающие ссылки например, на System.ServiceModel или System.ComponentModel.DataAnnotations.</span><span class="sxs-lookup"><span data-stu-id="c2dae-p109">**Note** At the time this article was written the Office Developer Tools for Visual Studio add references to all the needed assemblies when the receiver is created, but later versions of the tools may not. If you get compiler errors, simply add the missing references; for example, you may need to add references to System.ServiceModel or System.ComponentModel.DataAnnotations.</span></span>



```C#
  using System;
using System.Collections.Generic;
using System.Linq;
using System.Net;
using System.Text;
using Microsoft.SharePoint.Client;
using Microsoft.SharePoint.Client.EventReceivers;
using System.Runtime.Serialization;
using System.ServiceModel;
using System.ServiceModel.Channels;


namespace BasicDataOperationsWeb.Services
{
    public class RemoteEventReceiver1 : IRemoteEventService
    {
        public SPRemoteEventResult ProcessEvent(SPRemoteEventProperties properties)
        {
            // When a "before" event occurs (such as ItemAdding), call the event 
            // receiver code.
            ListRemoteEventReceiver(properties);
            return new SPRemoteEventResult();
        }

        public void ProcessOneWayEvent(SPRemoteEventProperties properties)
        {
            // When an "after" event occurs (such as ItemAdded), call the event 
            // receiver code.            
        }

        public static void ListRemoteEventReceiver(SPRemoteEventProperties properties)
        {
            string logListTitle = "EventLog";

            // Return if the event is from the EventLog list itself. Otherwise, it may go into
            // an infinite loop.
            if (string.Equals(properties.ItemEventProperties.ListTitle, logListTitle, 
                  StringComparison.OrdinalIgnoreCase))
                return;

            // Get the token from the request header.
            HttpRequestMessageProperty requestProperty = 
                  (HttpRequestMessageProperty)OperationContext
                   .Current.IncomingMessageProperties[HttpRequestMessageProperty.Name];
            string contextTokenString = requestProperty.Headers["X-SP-ContextToken"];

            // If there is a valid token, continue.
            if (contextTokenString != null)
            {
                SharePointContextToken contextToken =
                    TokenHelper.ReadAndValidateContextToken(contextTokenString, 
                         requestProperty.Headers[HttpRequestHeader.Host]);

                Uri sharepointUrl = new Uri(properties.ItemEventProperties.WebUrl);
                string accessToken = TokenHelper.GetAccessToken(contextToken, 
                                                      sharepointUrl.Authority).AccessToken;
                bool exists = false;

                // Retrieve the log list "EventLog" and add the name of the event that occurred
                // to it with a date/time stamp.
                using (ClientContext clientContext = 
                     TokenHelper.GetClientContextWithAccessToken(sharepointUrl.ToString(), 
                                                                                                         accessToken))
                {
                    clientContext.Load(clientContext.Web);
                    clientContext.ExecuteQuery();
                    List logList = clientContext.Web.Lists.GetByTitle(logListTitle);

                    try
                    {
                        clientContext.Load(logList);
                        clientContext.ExecuteQuery();
                        exists = true;
                    }

                    catch (Microsoft.SharePoint.Client.ServerUnauthorizedAccessException)
                    {
                        // If the user doesn't have permissions to access the server that's 
                        // running SharePoint, return.
                        return;
                    }

                    catch (Microsoft.SharePoint.Client.ServerException)
                    {
                        // If an error occurs on the server that's running SharePoint, return.
                        exists = false;
                    }

                    // Create a log list called "EventLog" if it doesn't already exist.
                    if (!exists)
                    {
                        ListCreationInformation listInfo = new ListCreationInformation();
                        listInfo.Title = logListTitle;
                        // Create a generic custom list.
                        listInfo.TemplateType = 100;
                        clientContext.Web.Lists.Add(listInfo);
                        clientContext.Web.Context.ExecuteQuery();
                    }

                    // Add the event entry to the EventLog list.
                    string itemTitle = "Event: " + properties.EventType.ToString() + 
                          " occurred on: " + 
                          DateTime.Now.ToString(" yyyy/MM/dd/HH:mm:ss:fffffff");
                    ListCollection lists = clientContext.Web.Lists;
                    List selectedList = lists.GetByTitle(logListTitle);
                    clientContext.Load<ListCollection>(lists);
                    clientContext.Load<List>(selectedList);
                    ListItemCreationInformation listItemCreationInfo = 
                          new ListItemCreationInformation();
                    var listItem = selectedList.AddItem(listItemCreationInfo);
                    listItem["Title"] = itemTitle;
                    listItem.Update();
                    clientContext.ExecuteQuery();
                }
            }
        }
    }
}
```

3. <span data-ttu-id="c2dae-155">В файле Home.aspx.cs замените все экземпляры `SPHostUrl` на `SPAppWebUrl`.</span><span class="sxs-lookup"><span data-stu-id="c2dae-155">In Home.aspx.cs, change all instances of  `SPHostUrl` to `SPAppWebUrl`.</span></span>
    
    <span data-ttu-id="c2dae-156">Например, следует заменить `sharepointUrl = new Uri(Request.QueryString["SPHostUrl"]);` на `sharepointUrl = new Uri(Request.QueryString["SPAppWebUrl"]);`.</span><span class="sxs-lookup"><span data-stu-id="c2dae-156">For example,  `sharepointUrl = new Uri(Request.QueryString["SPHostUrl"]);` should be changed to `sharepointUrl = new Uri(Request.QueryString["SPAppWebUrl"]);`.</span></span> 
    
 

## <a name="run-and-test-the-event-handler"></a><span data-ttu-id="c2dae-157">Запуск и тестирование обработчика событий</span><span class="sxs-lookup"><span data-stu-id="c2dae-157">Run and test the event handler</span></span>
<span data-ttu-id="c2dae-158"><a name="RunAndTest"> </a></span><span class="sxs-lookup"><span data-stu-id="c2dae-158"></span></span>

<span data-ttu-id="c2dae-159">Протестируйте обработчик, выполнив указанную ниже процедуру.</span><span class="sxs-lookup"><span data-stu-id="c2dae-159">Test your handler with the following procedure.</span></span>
 

 

1. <span data-ttu-id="c2dae-160">Нажмите клавишу **F5**, чтобы запустить проект.</span><span class="sxs-lookup"><span data-stu-id="c2dae-160">Press **F5** key to run the project.</span></span>
    
 
2. <span data-ttu-id="c2dae-161">Когда отобразится соответствующий запрос, укажите, что необходимо доверять надстройке.</span><span class="sxs-lookup"><span data-stu-id="c2dae-161">Trust the add-in when prompted to do so.</span></span>
    
    <span data-ttu-id="c2dae-162">Ваша надстройка SharePoint запустится. После этого отобразится таблица доступных списков, в которой будет список **List1**.</span><span class="sxs-lookup"><span data-stu-id="c2dae-162">Your SharePoint Add-in runs, and a table of available lists appears and includes **List1**.</span></span>
    
 
3. <span data-ttu-id="c2dae-163">Выберите идентификатор списка **List1**.</span><span class="sxs-lookup"><span data-stu-id="c2dae-163">Choose the ID of **List1**.</span></span>
    
    <span data-ttu-id="c2dae-164">Этот идентификатор будет скопирован в поле **Получение элементов списка**.</span><span class="sxs-lookup"><span data-stu-id="c2dae-164">That ID is copied to the **Retrieve List Items** box.</span></span>
    
 
4. <span data-ttu-id="c2dae-165">Нажмите кнопку **Получить элементы списка**.</span><span class="sxs-lookup"><span data-stu-id="c2dae-165">Choose the **Retrieve List Items** button.</span></span>
    
     <span data-ttu-id="c2dae-166">Отобразится список **List1**, причем в нем не будет ни одного элемента.</span><span class="sxs-lookup"><span data-stu-id="c2dae-166">**List1** appears with no items in it.</span></span>
    
 
5. <span data-ttu-id="c2dae-167">В поле **Добавить элемент** введите First Item (Первый элемент), а затем нажмите кнопку **Добавить элемент**.</span><span class="sxs-lookup"><span data-stu-id="c2dae-167">In the **Add Item** box, specifyFirst Item, and then choose the **Add Item** button.</span></span>
    
    <span data-ttu-id="c2dae-168">Элемент с именем **First Item** (Первый элемент) будет добавлен в список **List1**. При этом будет активирован удаленный приемник событий, а в список EventLog (Журнал событий) будет добавлена запись.</span><span class="sxs-lookup"><span data-stu-id="c2dae-168">A list item that's named **First Item** is added to **List1**, which causes the remote event receiver to fire and add an entry to the EventLog list.</span></span>
    
 
6. <span data-ttu-id="c2dae-169">Нажмите кнопку **Обновить списки**, чтобы вернуться к таблице списков.</span><span class="sxs-lookup"><span data-stu-id="c2dae-169">Choose the **Refresh Lists** button to return to the table of lists.</span></span>
    
    <span data-ttu-id="c2dae-170">В таблице появится новый список с именем **EventLog** (Журнал событий).</span><span class="sxs-lookup"><span data-stu-id="c2dae-170">In the table, a new list that's named **EventLog** appears.</span></span>
    
 
7. <span data-ttu-id="c2dae-171">Выберите значение GUID **ListID** для **EventLog** (Журнал событий), а затем нажмите кнопку **Получить элементы списка**.</span><span class="sxs-lookup"><span data-stu-id="c2dae-171">Choose the **ListID** GUID value for **EventLog**, and then choose the **Retrieve List Items** button.</span></span>
    
    <span data-ttu-id="c2dae-172">Отобразится таблица для списка **EventLog** (Журнал событий) с записью для события **Handle ItemAdding** (Обработка добавления элемента), которое возникло, когда вы добавили элемент в список **List1**.</span><span class="sxs-lookup"><span data-stu-id="c2dae-172">A table for **EventLog** appears with an entry for the **Handle ItemAdding** event that occurred when you added the item to **List1**.</span></span>
    
 

## <a name="add-or-remove-event-handlers-using-visual-studio"></a><span data-ttu-id="c2dae-173">Добавление и удаление обработчиков событий с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c2dae-173">Add or remove event handlers using Visual Studio</span></span>
<span data-ttu-id="c2dae-174"><a name="Handle"> </a></span><span class="sxs-lookup"><span data-stu-id="c2dae-174"></span></span>


1. <span data-ttu-id="c2dae-175">В **обозревателе решений** выберите узел проекта для удаленного приемника событий.</span><span class="sxs-lookup"><span data-stu-id="c2dae-175">In **Solution Explorer**, choose the project node for the remote event receiver.</span></span>
    
 
2. <span data-ttu-id="c2dae-176">В области **Свойства** задайте для свойств событий, которые необходимо обрабатывать, значение **Истина**.</span><span class="sxs-lookup"><span data-stu-id="c2dae-176">In the **Properties** pane, set the properties for the events that you want to handle to **True**.</span></span>
    
    <span data-ttu-id="c2dae-p110">Например, если вы хотите, чтобы код реагировал на добавление элемента списка пользователем, задайте для свойства **Handle ItemAdding** (Обработка добавления элемента) значение **Истина**. Если вы не хотите обрабатывать это событие, задайте для этого свойства значение **Ложь**.</span><span class="sxs-lookup"><span data-stu-id="c2dae-p110">For example, if you want to respond whenever a user adds a list item, set the value of the **Handle ItemAdding** property to **True**. If you don't want to handle that event, set the value of that property to **False**.</span></span>
    

    <span data-ttu-id="c2dae-179">**Рис. 1. Удаленные события SharePoint в Visual Studio**</span><span class="sxs-lookup"><span data-stu-id="c2dae-179">**Figure 1. SharePoint remote events in Visual Studio**</span></span>

 

  ![Удаленные события SharePoint в Visual Studio](../../images/SP_VS_Properties_Window_RemoteEvents.PNG)
 

 

 
3. <span data-ttu-id="c2dae-181">Если вы добавили событие, включите код для его обработки в файл кода веб-службы, как и для предыдущих событий.</span><span class="sxs-lookup"><span data-stu-id="c2dae-181">If you added an event, add the event-handling code to the code file for the web service as you did with previous events.</span></span>
    
    <span data-ttu-id="c2dae-p111">Для обработки события другого типа добавьте в Надстройка SharePoint еще один приемник удаленных событий. Например, если приемник удаленных событий обрабатывает события, связанные с элементами списка, вы можете добавить в него еще одно такое событие. Однако если вы хотите обрабатывать событие, связанное со списками, вам нужно добавить другой приемник удаленных событий.</span><span class="sxs-lookup"><span data-stu-id="c2dae-p111">To handle a different type of event, add another remote event receiver to the SharePoint Add-in. For example, if a remote event receiver handles list item events, you can add another list item event to it. But you must add another remote event receiver if you want to handle list events.</span></span> 
    
 

## <a name="url-and-hosting-restrictions-for-production-remote-event-receivers"></a><span data-ttu-id="c2dae-185">URL-адрес и ограничения при размещении удаленных приемников событий в рабочей среде</span><span class="sxs-lookup"><span data-stu-id="c2dae-185">URL and hosting restrictions for production remote event receivers</span></span>
<span data-ttu-id="c2dae-186"><a name="Handle"> </a></span><span class="sxs-lookup"><span data-stu-id="c2dae-186"></span></span>

<span data-ttu-id="c2dae-p112">Удаленный приемник событий может быть размещен в облаке или на локальном сервере, который не используется в качестве сервера SharePoint. URL-адрес производственного приемника не может использовать определенный порт. Это значит, что вам необходимо использовать порт 443 для HTTPS (рекомендовано) или порт 80 для HTTP. При использовании HTTPS, если приемник размещен локально, а надстройка на Microsoft SharePoint Online, сервер размещения должен иметь доверенный сертификат, выданный центром сертификации. (Самозаверяющий сертификат действует, только если надстройка расположена в локальной ферме SharePoint.)</span><span class="sxs-lookup"><span data-stu-id="c2dae-p112">The remote event receiver can be hosted in the cloud or in an on-premise server that is not also being used as a SharePoint server. The URL of a production receiver cannot specify a particular port. This means that you must use either port 443 for HTTPS, which we recommend, or port 80 for HTTP. If you are using HTTPS and the receiver service is hosted on-premise, but the add-in is on Microsoft SharePoint Online, then the hosting server must have a publically trusted certificate from a certificate authority. (A self-signed certificate works only if the add-in is in an on-premise SharePoint farm.)</span></span>
 

 

## <a name="next-steps"></a><span data-ttu-id="c2dae-192">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c2dae-192">Next Steps</span></span>
<span data-ttu-id="c2dae-193"><a name="Handle"> </a></span><span class="sxs-lookup"><span data-stu-id="c2dae-193"></span></span>

<span data-ttu-id="c2dae-194">Чтобы лучше разобраться в удаленных приемниках событий, изучите указанные ниже примеры кода.</span><span class="sxs-lookup"><span data-stu-id="c2dae-194">Use the following code samples to improve your understanding of RERs:</span></span>
 

 

-  [<span data-ttu-id="c2dae-195">OfficeDev/PnP/Samples/Core.EventReceivers</span><span class="sxs-lookup"><span data-stu-id="c2dae-195">OfficeDev/PnP/Samples/Core.EventReceivers</span></span>](https://github.com/OfficeDev/PnP/tree/master/Samples/Core.EventReceivers)
    
 
-  <span data-ttu-id="c2dae-196">[OfficeDev/PnP/Samples/Provisioning.ReR](
https://github.com/OfficeDev/PnP/tree/master/Samples/Provisioning.ReR)</span><span class="sxs-lookup"><span data-stu-id="c2dae-196">[OfficeDev/PnP/Samples/Provisioning.ReR](
https://github.com/OfficeDev/PnP/tree/master/Samples/Provisioning.ReR)</span></span>
    
 
-  [<span data-ttu-id="c2dae-197">OfficeDev/PnP/Scenarios/ECM.AutoTagging</span><span class="sxs-lookup"><span data-stu-id="c2dae-197">OfficeDev/PnP/Scenarios/ECM.AutoTagging</span></span>](https://github.com/OfficeDev/PnP/tree/master/Samples/ECM.AutoTagging)
    
 

## <a name="additional-resources"></a><span data-ttu-id="c2dae-198">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="c2dae-198">Additional resources</span></span>
<span data-ttu-id="c2dae-199"><a name="Additional"> </a></span><span class="sxs-lookup"><span data-stu-id="c2dae-199"></span></span>


-  [<span data-ttu-id="c2dae-200">Обработка событий в надстройках SharePoint</span><span class="sxs-lookup"><span data-stu-id="c2dae-200">Handle events in SharePoint Add-ins</span></span>](handle-events-in-sharepoint-add-ins)
    
 
-  [<span data-ttu-id="c2dae-201">Отладка удаленного приемника событий в надстройке для SharePoint и устранение неполадок в нем</span><span class="sxs-lookup"><span data-stu-id="c2dae-201">Debug and troubleshoot a remote event receiver in a SharePoint Add-in</span></span>](debug-and-troubleshoot-a-remote-event-receiver-in-a-sharepoint-add-in)
    
 
-  [<span data-ttu-id="c2dae-202">Удаленные приемники событий: вопросы и ответы</span><span class="sxs-lookup"><span data-stu-id="c2dae-202">Remote Event Receivers FAQ</span></span>](handle-events-in-sharepoint-add-ins#RERFAQ)
    
 

