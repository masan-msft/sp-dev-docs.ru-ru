---
title: Создание удаленного приемника событий в надстройках SharePoint
description: Создание удаленного приемника событий (RER), обрабатывающего события списка и элементы списка в надстройке SharePoint.
ms.date: 12/22/2017
ms.prod: sharepoint
ms.openlocfilehash: db34b2390f04bdcc4d7ca61f926288a3b2fb3c80
ms.sourcegitcommit: c57fc0e802661b0771f8b022964b6956ab4f6caf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/23/2017
---
# <a name="create-a-remote-event-receiver-in-sharepoint-add-ins"></a><span data-ttu-id="bb8f9-103">Создание удаленного приемника событий в надстройках SharePoint</span><span class="sxs-lookup"><span data-stu-id="bb8f9-103">Create a remote event receiver in SharePoint Add-ins</span></span>

<span data-ttu-id="bb8f9-104">Для начала желательно иметь представление о надстройках SharePoint с размещением у поставщика, а также разработать несколько надстроек, которые были бы хоть немного сложнее уровня "Hello World".</span><span class="sxs-lookup"><span data-stu-id="bb8f9-104">It is helpful if you first have an understanding of provider-hosted SharePoint Add-ins, and for you to have developed a few that go a least a little beyond the "Hello World" level. Also, you should be familiar with  Handle events in SharePoint Add-ins.</span></span> <span data-ttu-id="bb8f9-105">См. статью [Создание надстроек SharePoint, размещаемых у поставщика](get-started-creating-provider-hosted-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="bb8f9-105">See  [Get started creating provider-hosted SharePoint Add-ins](get-started-creating-provider-hosted-sharepoint-add-ins.md).</span></span>

<span data-ttu-id="bb8f9-106">Кроме того, следует ознакомиться со статьей [Обработка событий в надстройках SharePoint](handle-events-in-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="bb8f9-106">Also, you should be familiar with [Handle events in SharePoint Add-ins](handle-events-in-sharepoint-add-ins.md).</span></span> 
 

<span data-ttu-id="bb8f9-107"><a name="MakeRER"> </a></span><span class="sxs-lookup"><span data-stu-id="bb8f9-107"></span></span>

## <a name="create-a-remote-event-receiver"></a><span data-ttu-id="bb8f9-108">Создание удаленного приемника событий</span><span class="sxs-lookup"><span data-stu-id="bb8f9-108">Create a remote event receiver</span></span>

<span data-ttu-id="bb8f9-109">В этой статье показано, как усовершенствовать надстройку SharePoint, добавив удаленный приемник событий (RER), который обрабатывает событие ItemAdded для пользовательского списка на сайте надстройки.</span><span class="sxs-lookup"><span data-stu-id="bb8f9-109">This article shows how you extend a SharePoint Add-in by adding a remote event receiver (RER) that handles the ItemAdded event for a custom list in the add-in web. The RER is registered with the add-in web using declarative markup. RERs are registered with the  host web  programmatically. For a code sample that does so, see OfficeDev/PnP/Samples/Core.EventReceivers.</span></span> <span data-ttu-id="bb8f9-110">Удаленный приемник событий регистрируется на сайте надстройки с помощью декларативной разметки.</span><span class="sxs-lookup"><span data-stu-id="bb8f9-110">The RER is registered with the add-in web using declarative markup.</span></span> <span data-ttu-id="bb8f9-111">Удаленные приемники событий регистрируются с помощью *хост-сайта* программно.</span><span class="sxs-lookup"><span data-stu-id="bb8f9-111">RERs are registered with the *host web* programmatically.</span></span> <span data-ttu-id="bb8f9-112">Соответствующий пример кода см. на странице [SharePoint/PnP/Samples/Core.EventReceivers](https://github.com/SharePoint/PnP/tree/master/Samples/Core.EventReceivers).</span><span class="sxs-lookup"><span data-stu-id="bb8f9-112">For a code sample that does so, see [SharePoint/PnP/Samples/Core.EventReceivers](https://github.com/SharePoint/PnP/tree/master/Samples/Core.EventReceivers).</span></span>
 
<span data-ttu-id="bb8f9-113">Удаленный приемник событий должен быть веб-службой SOAP.</span><span class="sxs-lookup"><span data-stu-id="bb8f9-113">An RER must be a SOAP web service.</span></span> <span data-ttu-id="bb8f9-114">В этом примере он реализован в виде службы Windows Communication Foundation (WCF). Но его можно реализовать в стеке не от Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="bb8f9-114">An RER must be a SOAP web service. The continuing example implements this as a Windows Communication Foundation (WCF) service; but it is possible in principle to implement an RER on a non-Microsoft stack.</span></span>
 
<span data-ttu-id="bb8f9-115">Чтобы следовать приведенным здесь указаниям и ввести код самостоятельно, скачайте пример из репозитория  [SharePoint-Add-in-CSOM-BasicDataOperations](https://github.com/OfficeDev/SharePoint-Add-in-CSOM-BasicDataOperations), а затем откройте его в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bb8f9-115">To follow along with this article and enter the code yourself, download the sample from  [SharePoint-Add-in-CSOM-BasicDataOperations](https://github.com/OfficeDev/SharePoint-Add-in-CSOM-BasicDataOperations), and then open the sample in Visual Studio.</span></span>
 
> [!NOTE] 
> <span data-ttu-id="bb8f9-116">Этот пример использует файл TokenHelper.cs, созданный в Инструментах разработчика Office для Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bb8f9-116">It uses the TokenHelper.cs file that is generated by the Office Developer Tools for Visual Studio.</span></span> <span data-ttu-id="bb8f9-117">На момент создания примера это была последняя версия, но на момент чтения этой статьи она могла устареть.</span><span class="sxs-lookup"><span data-stu-id="bb8f9-117">It was the current version when the sample was created, but may not be the most recent version when you read this.</span></span> <span data-ttu-id="bb8f9-118">Тем не менее этот пример отлично подходит для создания первого удаленного приемника событий.</span><span class="sxs-lookup"><span data-stu-id="bb8f9-118">The sample is still great for creating your first RER.</span></span> <span data-ttu-id="bb8f9-119">Когда вы будете готовы двигаться дальше, ознакомьтесь с примерами в разделе "Дополнительные ресурсы" ниже.</span><span class="sxs-lookup"><span data-stu-id="bb8f9-119">But when you are ready to move beyond that, you should look at the samples listed in the See also section at the end of this article.</span></span> <span data-ttu-id="bb8f9-120">Скорее всего, они останутся актуальными.</span><span class="sxs-lookup"><span data-stu-id="bb8f9-120">They are more likely to be kept up to date.</span></span>

### <a name="to-register-a-remote-event-receiver"></a><span data-ttu-id="bb8f9-121">Регистрация удаленного приемника событий</span><span class="sxs-lookup"><span data-stu-id="bb8f9-121">To register a remote event receiver</span></span>

1. <span data-ttu-id="bb8f9-122">Откройте проект надстройки SharePoint в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bb8f9-122">Open the SharePoint Add-in project in Visual Studio.</span></span> 

2. <span data-ttu-id="bb8f9-123">В **обозревателе решений** выберите узел проекта надстройки.</span><span class="sxs-lookup"><span data-stu-id="bb8f9-123">In  **Solution Explorer** select the add-in project's node.</span></span>

3. <span data-ttu-id="bb8f9-124">В строке меню выберите **Проект** > **Добавить новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="bb8f9-124">On the menu bar, select **Project** > **Add New Item**.</span></span>

4. <span data-ttu-id="bb8f9-125">На панели **Установленные шаблоны** выберите узел **Office/SharePoint**.</span><span class="sxs-lookup"><span data-stu-id="bb8f9-125">In the  **Installed Templates** pane, choose the **Office/ SharePoint** node.</span></span>

5. <span data-ttu-id="bb8f9-126">На панели **Шаблоны** выберите шаблон **Удаленный приемник событий**.</span><span class="sxs-lookup"><span data-stu-id="bb8f9-126">In the  **Templates** pane, choose the **Remote Event Receiver** template.</span></span>

6. <span data-ttu-id="bb8f9-127">В поле **Имя** оставьте имя, указанное по умолчанию (RemoteEventReceiver1), и нажмите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="bb8f9-127">In the  **Name** box, keep the default name (RemoteEventReceiver1), and then choose the  **Add** button.</span></span>

7. <span data-ttu-id="bb8f9-128">В списке **Тип приемника событий** выберите **События элемента списка**.</span><span class="sxs-lookup"><span data-stu-id="bb8f9-128">In the  **What type of event receiver do you want?** list, choose **List Item Events**.</span></span>

8. <span data-ttu-id="bb8f9-129">В списке **Элемент, который должен быть источником событий** выберите **Настраиваемый список**.</span><span class="sxs-lookup"><span data-stu-id="bb8f9-129">In the **What Item should be the event source?** list, select **Custom List**.</span></span>
    
    <span data-ttu-id="bb8f9-p105">В данном примере используется настраиваемый общий список. Тем не менее, приемник удаленных событий также может обрабатывать события, которые возникают в стандартных списках SharePoint, например **Объявления** или **Контакты**.</span><span class="sxs-lookup"><span data-stu-id="bb8f9-p105">The continuing example uses a custom generic list. But an RER can also handle events that occur in standard SharePoint lists, such as **Announcements** or **Contacts**.</span></span>
    
9. <span data-ttu-id="bb8f9-132">В списке **Обработать следующие события** выберите **Добавляется элемент** и нажмите **Готово**.</span><span class="sxs-lookup"><span data-stu-id="bb8f9-132">In the **Handle the following events** list, choose **An item is being added**, and then choose the **Finish** button.</span></span>
    
    <span data-ttu-id="bb8f9-133">В веб-приложение будет добавлена веб-служба для обработки указанного удаленного события.</span><span class="sxs-lookup"><span data-stu-id="bb8f9-133">A web service is added to the web application to handle the remote event that you specified.</span></span> <span data-ttu-id="bb8f9-134">В надстройку SharePoint будет добавлен удаленный приемник событий, а в файл Elements.xml приемника, который хранится в компоненте сайта надстройки, будет добавлена ссылка на элемент списка.</span><span class="sxs-lookup"><span data-stu-id="bb8f9-134">A web service is added to the web application to handle the remote event that you specified. A remote event receiver is added to the SharePoint Add-in and the list item event is referenced in the receiver's Elements.xml file that is itself contained in the add-in web Feature.</span></span>

### <a name="to-create-the-list"></a><span data-ttu-id="bb8f9-135">Создание списка</span><span class="sxs-lookup"><span data-stu-id="bb8f9-135">To create the list</span></span>

1. <span data-ttu-id="bb8f9-136">В **обозревателе решений** выберите узел проекта надстройки.</span><span class="sxs-lookup"><span data-stu-id="bb8f9-136">In  **Solution Explorer** select the add-in project's node.</span></span>

2. <span data-ttu-id="bb8f9-137">В строке меню выберите **Проект** > **Добавить новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="bb8f9-137">On the menu bar, select **Project** > **Add New Item**.</span></span>

3. <span data-ttu-id="bb8f9-138">На панели **Установленные шаблоны** выберите узел **Office/SharePoint**.</span><span class="sxs-lookup"><span data-stu-id="bb8f9-138">In the **Installed Templates** pane, choose the **Office SharePoint** node.</span></span>

4. <span data-ttu-id="bb8f9-139">На панели **Шаблоны** выберите шаблон **Список**.</span><span class="sxs-lookup"><span data-stu-id="bb8f9-139">In the  **Templates** pane, choose the **List** template.</span></span>

5. <span data-ttu-id="bb8f9-140">В поле **Имя** оставьте имя, указанное по умолчанию (List1), и нажмите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="bb8f9-140">In the  **Name** box, leave the default name (List1), and then choose the  **Add** button.</span></span>

6. <span data-ttu-id="bb8f9-141">Выберите **Создать экземпляр списка на основе существующего шаблона списка** > **Настраиваемый список** и нажмите **Готово**.</span><span class="sxs-lookup"><span data-stu-id="bb8f9-141">Choose the  **Create a list instance based on an existing list template** option button, choose **Custom List** in the list, and then choose the **Finish** button.</span></span>

### <a name="to-add-functionality-to-the-remote-event-receiver"></a><span data-ttu-id="bb8f9-142">Добавление функций в удаленный приемник событий</span><span class="sxs-lookup"><span data-stu-id="bb8f9-142">To add functionality to the remote event receiver</span></span>

1. <span data-ttu-id="bb8f9-143">Если тестовая ферма SharePoint и Visual Studio работают на разных компьютерах (или в качестве тестового сайта SharePoint используется область клиентов SharePoint Online), настройте проект для отладки с помощью служебной шины Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="bb8f9-143">If your test SharePoint farm is not on the same computer that is running Visual Studio, (or you are using an SharePoint Online tenancy as your test SharePoint site), configure the project for debugging using the Microsoft Azure Service Bus. For more information, see the  Debug and troubleshoot a remote event receiver in a SharePoint Add-in.</span></span> <span data-ttu-id="bb8f9-144">Дополнительные сведения см. в статье [Устранение неполадок и отладка удаленного приемника событий в надстройке SharePoint](debug-and-troubleshoot-a-remote-event-receiver-in-a-sharepoint-add-in.md).</span><span class="sxs-lookup"><span data-stu-id="bb8f9-144">Follow the instructions at [Debug and troubleshoot a remote event receiver in a SharePoint Add-in](debug-and-troubleshoot-a-remote-event-receiver-in-a-sharepoint-add-in.md).</span></span> 
    
2. <span data-ttu-id="bb8f9-145">Замените содержимое файла кода для службы удаленного приемника событий (то есть в файле RemoteEventReceiver1.svc.cs) указанным ниже кодом.</span><span class="sxs-lookup"><span data-stu-id="bb8f9-145">In the code file for the service of the remote event receiver (that is, RemoteEventReceiver1.svc.cs), replace the contents with the following code.</span></span> <span data-ttu-id="bb8f9-146">Этот код выполняет следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="bb8f9-146">This code performs the following tasks:</span></span>
    
    - <span data-ttu-id="bb8f9-147">Возвращает допустимый объект контекста клиента.</span><span class="sxs-lookup"><span data-stu-id="bb8f9-147">Gets a valid client context object.</span></span> 
    
    - <span data-ttu-id="bb8f9-148">Если список под названием **EventLog** еще не существует, он создается и заполняется именами удаленных событий.</span><span class="sxs-lookup"><span data-stu-id="bb8f9-148">If a list that's named **EventLog** doesn't already exist, creates one to contain the names of the remote events that occur.</span></span>
        
    - <span data-ttu-id="bb8f9-149">Добавляет запись в список для события, включая метку даты и времени.</span><span class="sxs-lookup"><span data-stu-id="bb8f9-149">Adds an entry to the list for the event, including a time and date stamp.</span></span>
        
    > [!NOTE] 
    > <span data-ttu-id="bb8f9-150">На время написания этой статьи Инструменты разработчика Office для Visual Studio содержали ссылки на все сборки, необходимые при создании получателя. В более поздних версиях пакета они могут отсутствовать.</span><span class="sxs-lookup"><span data-stu-id="bb8f9-150">Note  At the time this article was written the Office Developer Tools for Visual Studio add references to all the needed assemblies when the receiver is created, but later versions of the tools may not. If you get compiler errors, simply add the missing references; for example, you may need to add references to System.ServiceModel or System.ComponentModel.DataAnnotations.</span></span> <span data-ttu-id="bb8f9-151">При получении ошибки компилятора просто добавьте отсутствующие ссылки. Например, может потребоваться добавить ссылки на System.ServiceModel или System.ComponentModel.DataAnnotations.</span><span class="sxs-lookup"><span data-stu-id="bb8f9-151">At the time this article was written the vstoshort add references to all the needed assemblies when the receiver is created, but later versions of the tools may not. If you get compiler errors, simply add the missing references; for example, you may need to add references to System.ServiceModel or System.ComponentModel.DataAnnotations.</span></span>

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

3. <span data-ttu-id="bb8f9-152">В файле Home.aspx.cs замените все экземпляры `SPHostUrl` на `SPAppWebUrl`.</span><span class="sxs-lookup"><span data-stu-id="bb8f9-152">In Home.aspx.cs, change all instances of  `SPHostUrl` to `SPAppWebUrl`.</span></span>
    
    <span data-ttu-id="bb8f9-153">Например, следует заменить `sharepointUrl = new Uri(Request.QueryString["SPHostUrl"]);` на `sharepointUrl = new Uri(Request.QueryString["SPAppWebUrl"]);`.</span><span class="sxs-lookup"><span data-stu-id="bb8f9-153">For example,  `sharepointUrl = new Uri(Request.QueryString["SPHostUrl"]);` should be changed to `sharepointUrl = new Uri(Request.QueryString["SPAppWebUrl"]);`.</span></span> 
    
<span data-ttu-id="bb8f9-154"><a name="RunAndTest"> </a></span><span class="sxs-lookup"><span data-stu-id="bb8f9-154"></span></span>
 
## <a name="run-and-test-the-event-handler"></a><span data-ttu-id="bb8f9-155">Запуск и тестирование обработчика событий</span><span class="sxs-lookup"><span data-stu-id="bb8f9-155">Run and test the event handler</span></span>

<span data-ttu-id="bb8f9-156">Протестируйте обработчик, выполнив указанную ниже процедуру.</span><span class="sxs-lookup"><span data-stu-id="bb8f9-156">Test your handler with the following procedure.</span></span>

1. <span data-ttu-id="bb8f9-157">Нажмите клавишу **F5** для запуска проекта.</span><span class="sxs-lookup"><span data-stu-id="bb8f9-157">Choose the  **F5** key to run the project.</span></span>

2. <span data-ttu-id="bb8f9-158">Подтвердите, что вы доверяете надстройке.</span><span class="sxs-lookup"><span data-stu-id="bb8f9-158">Trust the add-in when prompted to do so.</span></span> <span data-ttu-id="bb8f9-159">Запустится ваша надстройка SharePoint. После этого появится таблица доступных списков, в которой будет список **List1**.</span><span class="sxs-lookup"><span data-stu-id="bb8f9-159">Your SharePoint Add-in runs, and a table of available lists appears and includes **List1**.</span></span>

3. <span data-ttu-id="bb8f9-160">Выберите идентификатор списка **List1**.</span><span class="sxs-lookup"><span data-stu-id="bb8f9-160">Choose the ID of **List1**.</span></span> <span data-ttu-id="bb8f9-161">Этот идентификатор будет скопирован в поле **Получение элементов списка**.</span><span class="sxs-lookup"><span data-stu-id="bb8f9-161">That ID is copied to the **Retrieve List Items** box.</span></span>

4. <span data-ttu-id="bb8f9-162">Нажмите кнопку **Получить элементы списка**.</span><span class="sxs-lookup"><span data-stu-id="bb8f9-162">Choose the **Retrieve List Items** button.</span></span> <span data-ttu-id="bb8f9-163">Отобразится список **List1**, причем в нем не будет ни одного элемента.</span><span class="sxs-lookup"><span data-stu-id="bb8f9-163">**List1** appears with no items in it.</span></span>

5. <span data-ttu-id="bb8f9-164">В поле **Добавить элемент** введите **First Item** (Первый элемент), а затем нажмите кнопку **Добавить элемент**.</span><span class="sxs-lookup"><span data-stu-id="bb8f9-164">In the Add Item box, specifyFirst Item, and then choose the Add Item button.</span></span> <span data-ttu-id="bb8f9-165">Элемент **Первый элемент** будет добавлен в список **List1**. При этом активируется удаленный приемник событий и добавляется запись в список EventLog.</span><span class="sxs-lookup"><span data-stu-id="bb8f9-165">A list item that's named **First Item** is added to **List1**, which causes the remote event receiver to fire and add an entry to the EventLog list.</span></span>

6. <span data-ttu-id="bb8f9-166">Нажмите кнопку **Обновить списки**, чтобы вернуться к таблице списков.</span><span class="sxs-lookup"><span data-stu-id="bb8f9-166">Choose the **Refresh Lists** button to return to the table of lists.</span></span> <span data-ttu-id="bb8f9-167">В таблице появится новый список с именем **EventLog** (Журнал событий).</span><span class="sxs-lookup"><span data-stu-id="bb8f9-167">In the table, a new list that's named **EventLog** appears.</span></span>

7. <span data-ttu-id="bb8f9-168">Выберите значение GUID **ListID** для **EventLog**, а затем нажмите кнопку **Получить элементы списка**.</span><span class="sxs-lookup"><span data-stu-id="bb8f9-168">Choose the **ListID** GUID value for **EventLog**, and then choose the **Retrieve List Items** button.</span></span> <span data-ttu-id="bb8f9-169">Появится таблица для списка **EventLog** с записью для события **Handle ItemAdding**, которое происходит при добавлении элемента в список **List1**.</span><span class="sxs-lookup"><span data-stu-id="bb8f9-169">A table for **EventLog** appears with an entry for the **Handle ItemAdding** event that occurred when you added the item to **List1**.</span></span>

<span data-ttu-id="bb8f9-170"><a name="Handle"> </a></span><span class="sxs-lookup"><span data-stu-id="bb8f9-170"></span></span>

## <a name="add-or-remove-event-handlers-using-visual-studio"></a><span data-ttu-id="bb8f9-171">Добавление и удаление обработчиков событий с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bb8f9-171">Add or remove event handlers using Visual Studio</span></span>

1. <span data-ttu-id="bb8f9-172">В **обозревателе решений** выберите узел проекта для удаленного приемника событий.</span><span class="sxs-lookup"><span data-stu-id="bb8f9-172">In **Solution Explorer**, choose the project node for the remote event receiver.</span></span>

2. <span data-ttu-id="bb8f9-173">На панели **Свойства** установите для свойств событий, которые нужно обрабатывать, значение **True**.</span><span class="sxs-lookup"><span data-stu-id="bb8f9-173">In the **Properties** pane, set the properties for the events that you want to handle to **True**.</span></span>
    
    <span data-ttu-id="bb8f9-p116">Например, если вы хотите обеспечить реакцию на добавление элемента списка пользователем, задайте для свойства **Обрабатывать ItemAdding** значение **True**. Если вы не хотите обрабатывать это событие, задайте для его свойства значение **False**.</span><span class="sxs-lookup"><span data-stu-id="bb8f9-p116">For example, if you want to respond whenever a user adds a list item, set the value of the **Handle ItemAdding** property to **True**. If you don't want to handle that event, set the value of that property to **False**.</span></span>
 
    <span data-ttu-id="bb8f9-176">**Удаленные события SharePoint в Visual Studio**</span><span class="sxs-lookup"><span data-stu-id="bb8f9-176">**SharePoint remote events in Visual Studio**</span></span>

   ![Удаленные события SharePoint в Visual Studio](../images/SP_VS_Properties_Window_RemoteEvents.PNG)

3. <span data-ttu-id="bb8f9-178">Если вы добавили событие, включите код для его обработки в файл кода веб-службы, как и для предыдущих событий.</span><span class="sxs-lookup"><span data-stu-id="bb8f9-178">If you added an event, add the event-handling code to the code file for the web service as you did with previous events.</span></span>
    
    <span data-ttu-id="bb8f9-p117">Для обработки события другого типа добавьте в Надстройка SharePoint еще один приемник удаленных событий. Например, если приемник удаленных событий обрабатывает события, связанные с элементами списка, вы можете добавить в него еще одно такое событие. Однако если вы хотите обрабатывать событие, связанное со списками, вам нужно добавить другой приемник удаленных событий.</span><span class="sxs-lookup"><span data-stu-id="bb8f9-p117">To handle a different type of event, add another remote event receiver to the SharePoint Add-in. For example, if a remote event receiver handles list item events, you can add another list item event to it. But you must add another remote event receiver if you want to handle list events.</span></span> 
    

## <a name="url-and-hosting-restrictions-for-production-remote-event-receivers"></a><span data-ttu-id="bb8f9-182">URL-адрес и ограничения при размещении удаленных приемников событий в рабочей среде</span><span class="sxs-lookup"><span data-stu-id="bb8f9-182">URL and hosting restrictions for production remote event receivers</span></span>

<span data-ttu-id="bb8f9-183">Удаленный приемник событий может быть размещен в облаке или на локальном сервере, который не используется в качестве сервера SharePoint.</span><span class="sxs-lookup"><span data-stu-id="bb8f9-183">The remote event receiver can be hosted in the cloud or on an on-premises server that is not also being used as a SharePoint server.</span></span> <span data-ttu-id="bb8f9-184">URL-адрес производственного приемника не может использовать определенный порт.</span><span class="sxs-lookup"><span data-stu-id="bb8f9-184">The URL of a production receiver cannot specify a particular port.</span></span> <span data-ttu-id="bb8f9-185">Это значит, что вам необходимо использовать порт 443 для протокола HTTPS (рекомендовано) или порт 80 для HTTP.</span><span class="sxs-lookup"><span data-stu-id="bb8f9-185">SharePoint requires that there be no explicit port in the URL of the handler in production. This means that you must use either port 443 for HTTPS, which we recommend, or port 80 for HTTP.</span></span> <span data-ttu-id="bb8f9-186">Если вы используете HTTPS, приемник размещен локально, а надстройка находится в SharePoint Online, сервер размещения должен иметь доверенный сертификат, выданный центром сертификации.</span><span class="sxs-lookup"><span data-stu-id="bb8f9-186">If you are using HTTPS and the receiver service is hosted on-premises, but the add-in is on SharePoint Online, the hosting server must have a publicly trusted certificate from a certificate authority.</span></span> <span data-ttu-id="bb8f9-187">(Самозаверяющий сертификат подходит, только если надстройка расположена в локальной ферме SharePoint.)</span><span class="sxs-lookup"><span data-stu-id="bb8f9-187">(A self-signed certificate works only if the add-in is on an on-premises SharePoint farm.)</span></span>

## <a name="see-also"></a><span data-ttu-id="bb8f9-188">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="bb8f9-188">See also</span></span>
<span data-ttu-id="bb8f9-189"><a name="Additional"> </a></span><span class="sxs-lookup"><span data-stu-id="bb8f9-189"></span></span>

- [<span data-ttu-id="bb8f9-190">SharePoint/PnP/Samples/Core.EventReceivers</span><span class="sxs-lookup"><span data-stu-id="bb8f9-190">SharePoint/PnP/Samples/Core.EventReceivers</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Core.EventReceivers)
- [<span data-ttu-id="bb8f9-191">SharePoint/PnP/Samples/Provisioning.ReR</span><span class="sxs-lookup"><span data-stu-id="bb8f9-191">SharePoint/PnP/Samples/Provisioning.ReR</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.ReR)
- [<span data-ttu-id="bb8f9-192">SharePoint/PnP/Samples/ECM.AutoTagging</span><span class="sxs-lookup"><span data-stu-id="bb8f9-192">SharePoint/PnP/Samples/ECM.AutoTagging</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/ECM.AutoTagging)
- [<span data-ttu-id="bb8f9-193">Обработка событий в надстройках SharePoint</span><span class="sxs-lookup"><span data-stu-id="bb8f9-193">Handle events in SharePoint Add-ins</span></span>](handle-events-in-sharepoint-add-ins.md)
    
 

