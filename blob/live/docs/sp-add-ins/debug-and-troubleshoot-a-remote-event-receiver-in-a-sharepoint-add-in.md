---
title: "Устранение неполадок и отладка удаленного приемника событий в надстройке для SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 4e378b17fccf84f9d9321b1953d7a3d8f09dc5b7
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="debug-and-troubleshoot-a-remote-event-receiver-in-a-sharepoint-add-in"></a><span data-ttu-id="8b5be-102">Устранение неполадок и отладка удаленного приемника событий в надстройке для SharePoint</span><span class="sxs-lookup"><span data-stu-id="8b5be-102">Debug and troubleshoot a remote event receiver in a SharePoint Add-in</span></span>
<span data-ttu-id="8b5be-103">Узнайте, как настроить среду разработки для отладки удаленных событий с помощью Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8b5be-103">Set up the your development environment to debug remote events in by using Visual Studio.</span></span>
 

 <span data-ttu-id="8b5be-p101">**Примечание.** В настоящее время идет процесс замены названия "приложения для SharePoint" названием "надстройки SharePoint". Во время этого процесса в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio может по-прежнему использоваться термин "приложения для SharePoint". Дополнительные сведения см. в статье [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="8b5be-p101">**Note**  The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see  [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span></span>
 


## <a name="configure-debugging-for-a-remote-sharepoint-test-site"></a><span data-ttu-id="8b5be-107">Настройка отладки для удаленного тестового сайта SharePoint</span><span class="sxs-lookup"><span data-stu-id="8b5be-107">Configure debugging for a remote SharePoint test site</span></span>


 <span data-ttu-id="8b5be-p102">**Примечание.** Описанные в этом разделе действия применимы, только если Visual Studio и тестовый сайт SharePoint развернуты на разных компьютерах, а также если в качестве тестового сайта используется сайт разработчика SharePoint Online. Если SharePoint и Visual Studio развернуты на одном компьютере, пропустите этот раздел.</span><span class="sxs-lookup"><span data-stu-id="8b5be-p102">**Note**  The procedures in this section apply only when your test SharePoint site is on a different computer from Visual Studio or you are using an SharePoint Online Developer Site as your test site. If SharePoint and Visual Studio are on the same computer, skip this section.</span></span>
 

<span data-ttu-id="8b5be-p103">Если проект Надстройка SharePoint в Visual Studio содержит приемник удаленных событий (RER) или приемник событий надстройки, то для отладки надстройки с помощью клавиши F5 нужно выполнить дополнительную быструю настройку свойств проекта. А для этого, в свою очередь, требуется настроить Azure. Не нужно повторно настраивать Azure для каждого подобного проекта. Если надстройка содержит обработчик событий AppInstalled, она не запустится ни с помощью клавиши F5, ни с помощью клавиш CTRL+F5 (запуск без отладки), пока не будут выполнены настройки, описанные в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="8b5be-p103">When a SharePoint Add-in project in Visual Studio includes a remote event receiver (RER) or an add-in event receiver, you have to do some additional quick configuration in the project properties before you can debug the add-in with (F5). This configuration, in turn, requires that you do some Azure configuration. You do not have to repeat the Azure configuration for every project that has an RER or add-in event. (If the add-in includes an AppInstalled event handler, the add-in won't even run with either F5 or Ctrl-F5 [run without debugging] unless you carry out the configuration in this section.)</span></span>
 

 

### <a name="to-configure-azure"></a><span data-ttu-id="8b5be-114">Настройка Azure</span><span class="sxs-lookup"><span data-stu-id="8b5be-114">To configure Azure</span></span>


1. <span data-ttu-id="8b5be-p104">Если у вас еще нет подписки Microsoft Azure, приобретите ее. Она входит в состав [подписки на MSDN](http://azure.microsoft.com/en-us/pricing/member-offers/msdn-benefits/).</span><span class="sxs-lookup"><span data-stu-id="8b5be-p104">If you don't already have one, get an Microsoft Azure subscription. One is included as a benefit with an  [MSDN Subscription](http://azure.microsoft.com/en-us/pricing/member-offers/msdn-benefits/).</span></span>
    
 
2. <span data-ttu-id="8b5be-117">Выполните действия, описанные в статье [Создание или изменение пространства имен служебной шины](http://msdn.microsoft.com/library/fa561f70-007c-45aa-b34d-56317dbbfc87.aspx).</span><span class="sxs-lookup"><span data-stu-id="8b5be-117">Carry out the instructions in  [How To: Create or Modify a Service Bus Service Namespace](http://msdn.microsoft.com/library/fa561f70-007c-45aa-b34d-56317dbbfc87.aspx).</span></span>
    
 

### <a name="to-configure-the-sharepoint-add-in-project-in-visual-studio"></a><span data-ttu-id="8b5be-118">Настройка проекта надстройки SharePoint в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8b5be-118">To configure the SharePoint Add-in project in Visual Studio</span></span>


1. <span data-ttu-id="8b5be-119">Вам потребуется последняя версия Инструменты разработчика Office для Visual Studio 2013, поэтому  [запустите установщик веб-платформы, расположенный по ссылке ](http://aka.ms/OfficeDevToolsForVS2013), или  [установщик Инструментов разработчика Microsoft Office для Visual Studio 2015](http://aka.ms/OfficeDevToolsForVS2015).</span><span class="sxs-lookup"><span data-stu-id="8b5be-119">You should have the latest version of the Office Developer Tools for Visual Studio 2013, so  [run the WebPI installer here](http://aka.ms/OfficeDevToolsForVS2013), or  [installer for Office Developer Tools for Visual Studio 2015](http://aka.ms/OfficeDevToolsForVS2015).</span></span>
    
 
2. <span data-ttu-id="8b5be-120">Добавив приемник удаленных событий (RER) или обработчик событий надстройки в проект надстройки SharePoint в Visual Studio, щелкните правой кнопкой мыши проект в **обозревателе решений** и выберите пункт **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="8b5be-120">After you add a RER or add-in event handler to a SharePoint Add-in project in Visual Studio, right-click the project in  **Solution Explorer** and select **Properties**.</span></span>
    
 
3. <span data-ttu-id="8b5be-121">В области свойств откройте вкладку **SharePoint** и прокрутите вниз.</span><span class="sxs-lookup"><span data-stu-id="8b5be-121">In the properties pane, open the  **SharePoint** tab and scroll to the bottom.</span></span>
    
 
4. <span data-ttu-id="8b5be-122">Установите флажок **Включить отладку через шину обслуживания Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="8b5be-122">Select the check box for  **Enable debugging via Microsoft Azure Service Bus**.</span></span>
    
 
5. <span data-ttu-id="8b5be-p105">Укажите полную строку подключения в текстовом поле. Чтобы получить эту строку, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="8b5be-p105">Enter the complete connection string in the text box provided. You obtain the string with these steps.</span></span>
    
      1. <span data-ttu-id="8b5be-125">Войдите на портал Azure и откройте вкладку **Служебная шина**.</span><span class="sxs-lookup"><span data-stu-id="8b5be-125">Log in to the Azure portal and open the  **Service Bus** tab.</span></span>
    
 
  2. <span data-ttu-id="8b5be-p106">Откройте пространство имен, созданное для отладки удаленного приемника событий (RER), и перейдите к строкам подключения. Пользовательский интерфейс портала Azure часто меняется. Если не удается найти строки подключения, см.  [справку по порталу Azure](https://msdn.microsoft.com/en-us/library/azure/dn578292.aspx).</span><span class="sxs-lookup"><span data-stu-id="8b5be-p106">Open the namespace that you created for RER debugging and navigate to the connection strings. The Azure portal UI changes frequently. See  [Azure portal help](https://msdn.microsoft.com/en-us/library/azure/dn578292.aspx) if you can't find the connection strings.</span></span>
    
 
  3. <span data-ttu-id="8b5be-p107">Скопируйте строку подключения **SAS**. Это строка, которую вы указываете в свойствах проекта Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8b5be-p107">Copy the  **SAS** connection string. This is the string you enter in the Visual Studio project properties.</span></span>
    
 
<span data-ttu-id="8b5be-131">В дальнейшем при создании проектов Надстройка SharePoint в Visual Studio эти сведения будут заполнены заранее, поэтому не потребуется каждый раз открывать портал Azure.</span><span class="sxs-lookup"><span data-stu-id="8b5be-131">In the future, when you create SharePoint Add-in projects in Visual Studio, this information is prefilled, so you don't have to open the Azure portal each time.</span></span>
 

## <a name="test-the-configuration"></a><span data-ttu-id="8b5be-132">Тестирование конфигурации</span><span class="sxs-lookup"><span data-stu-id="8b5be-132">Test the configuration</span></span>
<span data-ttu-id="8b5be-133"><a name="CreateRER"> </a></span><span class="sxs-lookup"><span data-stu-id="8b5be-133"><a name="CreateRER"> </a></span></span>

<span data-ttu-id="8b5be-134">Чтобы убедиться, что вы можете выполнять отладку RER, выполните процедуры, описанные в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="8b5be-134">Use the procedures in this section to verify that you can debug an RER.</span></span>
 

 

### <a name="to-create-a-remote-event-receiver-project"></a><span data-ttu-id="8b5be-135">Создание проекта приемника удаленных событий</span><span class="sxs-lookup"><span data-stu-id="8b5be-135">To create a remote event receiver project</span></span>


1. <span data-ttu-id="8b5be-136">В Visual Studio создайте надстройку SharePoint, размещаемую у поставщика.</span><span class="sxs-lookup"><span data-stu-id="8b5be-136">In Visual Studio, create a provider-hosted SharePoint Add-in.</span></span>
    
    <span data-ttu-id="8b5be-137">См. статью [Знакомство с созданием надстроек SharePoint с размещением у поставщика](get-started-creating-provider-hosted-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="8b5be-137">See  [Get started creating provider-hosted SharePoint Add-ins](get-started-creating-provider-hosted-sharepoint-add-ins.md).</span></span>
    
 
2. <span data-ttu-id="8b5be-138">Выберите узел проекта надстройки в **обозревателе решений**.</span><span class="sxs-lookup"><span data-stu-id="8b5be-138">In  **Solution Explorer**, choose the add-in project's node.</span></span>
    
 
3. <span data-ttu-id="8b5be-139">В строке меню выберите пункты **Проект** и **Добавить новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="8b5be-139">On the menu bar, choose  **Project**,  **Add New Item**.</span></span>
    
 
4. <span data-ttu-id="8b5be-140">В области **Шаблоны** выберите шаблон **Список**, а затем нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="8b5be-140">In the  **Templates** pane, choose the **List** template, and then choose the **Add** button.</span></span>
    
 
5. <span data-ttu-id="8b5be-141">Нажмите кнопку **Готово**, чтобы добавить настраиваемый список по умолчанию в проект надстройки.</span><span class="sxs-lookup"><span data-stu-id="8b5be-141">Choose the  **Finish** button to add a default custom list to the add-in project.</span></span>
    
 
6. <span data-ttu-id="8b5be-142">Добавьте еще один элемент в проект надстройки. Для этого в области **Шаблоны** выберите шаблон **Удаленный приемник событий**.</span><span class="sxs-lookup"><span data-stu-id="8b5be-142">Add another item to the add-in project by, in the  **Templates** pane, choosing the **Remote Event Receiver** template.</span></span>
    
 
7. <span data-ttu-id="8b5be-143">В поле **Имя** оставьте имя, заданное по умолчанию (RemoteEventReceiver1), и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="8b5be-143">In the  **Name** box, leave the default name (RemoteEventReceiver1), and then choose the  **Add** button.</span></span>
    
 
8. <span data-ttu-id="8b5be-144">В списке **Тип приемника событий:** выберите пункт **События элемента списка**.</span><span class="sxs-lookup"><span data-stu-id="8b5be-144">In the  **What type of event receiver do you want?** list, choose **List Item Events**.</span></span> 
    
    <span data-ttu-id="8b5be-145">В качестве источника события оставьте **List1** — список, который вы добавили на предыдущих этапах.</span><span class="sxs-lookup"><span data-stu-id="8b5be-145">Leave the event source as  **List1**, the list that you added in the previous steps.</span></span>
    
 
9. <span data-ttu-id="8b5be-146">В списке **Обработать следующие события:** выберите пункт **Добавляется элемент**, а затем нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="8b5be-146">In the  **Handle the following events** list, choose **An item is being added**, and then choose the  **Finish** button.</span></span>
    
    <span data-ttu-id="8b5be-p108">Веб-сервис будет добавлен в веб-приложение для управления удаленным событием, которое вы указали. Приемник удаленных событий будет добавлен в Надстройка SharePoint. Он будет ссылаться на веб-службы и события элемента списка в файле Elements.xml приемника событий.</span><span class="sxs-lookup"><span data-stu-id="8b5be-p108">A web service is added to the web application to handle the remote event that you specified. A remote event receiver is added to the SharePoint Add-in. The receiver references the web service and the list item event in the event receiver's Elements.xml file.</span></span>
    
 
10. <span data-ttu-id="8b5be-150">В проекте надстройки откройте файл AppManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="8b5be-150">In the add-in project, open AppManifest.xml.</span></span>
    
 
11. <span data-ttu-id="8b5be-151">Сделайте начальной страницу списка: _AddInProjectName_/Lists/List1.</span><span class="sxs-lookup"><span data-stu-id="8b5be-151">Change the start page to the list's page:  _AddInProjectName_/Lists/List1.</span></span>
    
    <span data-ttu-id="8b5be-p109">Замените  _AddInProjectName_ на имя проекта надстройки, например SharePointAddIn4/Lists/List1. В этом примере начальной страницей назначается страница списка. Но в типичной надстройке ссылка, скорее всего, будет вести к собственному пользовательскому интерфейсу на странице веб-проекта.</span><span class="sxs-lookup"><span data-stu-id="8b5be-p109">Replace  _AddInProjectName_ with the name of your add-in project, such asSharePointAddIn4/Lists/List1. For this example, we're setting the start page to the list's page. However, in a typical add-in, you'd likely point to your own UI on the web project page.</span></span>
    
 

### <a name="to-run-and-test-event-handler-debugging"></a><span data-ttu-id="8b5be-155">Запуск и тестирование отладки обработчика событий</span><span class="sxs-lookup"><span data-stu-id="8b5be-155">To run and test event handler debugging</span></span>


1. <span data-ttu-id="8b5be-156">Если вы еще не сделали этого, выполните действия, описанные в разделе **Настройка проекта надстройки SharePoint в Visual Studio** этой статьи.</span><span class="sxs-lookup"><span data-stu-id="8b5be-156">If you haven't done so already, complete the  **To configure the SharePoint Add-in project in Visual Studio** procedure earlier in this article.</span></span>
    
 
2. <span data-ttu-id="8b5be-157">В веб-проекте откройте службу приемника удаленных событий (RemoteEventReceiver1.svc), а затем добавьте точку останова в любую строку кода внутри метода  `ProcessEvent()`.</span><span class="sxs-lookup"><span data-stu-id="8b5be-157">In the web project, open the remote event receiver service (RemoteEventReceiver1.svc), and then add a breakpoint to any line of code inside the  `ProcessEvent()` method.</span></span>
    
 
3. <span data-ttu-id="8b5be-158">Нажмите клавишу **F5** для запуска проекта.</span><span class="sxs-lookup"><span data-stu-id="8b5be-158">Choose the  **F5** key to run the project.</span></span>
    
 
4. <span data-ttu-id="8b5be-159">Нажмите кнопку **+ Новый элемент**, чтобы добавить элемент в список.</span><span class="sxs-lookup"><span data-stu-id="8b5be-159">Choose the  **+ New item** button to add an item to the list.</span></span>
    
 
5. <span data-ttu-id="8b5be-160">Укажите название элемента, а затем нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="8b5be-160">Provide a title for the item, and then choose the  **Save** button.</span></span>
    
    <span data-ttu-id="8b5be-161">Будет достигнута точка останова, добавленная к обработчику удаленных событий, указывая, что выполняется отладка обработчика удаленных событий.</span><span class="sxs-lookup"><span data-stu-id="8b5be-161">The breakpoint that you added to the remote event receiver is hit, verifying that you're debugging the remote event receiver.</span></span>
    
 
6. <span data-ttu-id="8b5be-162">Нажмите клавишу **F5**, чтобы продолжить выполнение проекта, а по завершении его работы остановите отладку.</span><span class="sxs-lookup"><span data-stu-id="8b5be-162">Choose the  **F5** key to continue to run the project, and then stop debugging when you're done.</span></span>
    
 

## <a name="turn-onoff-the-notification-from-visual-studio-that-event-debugging-needs-to-be-configured"></a><span data-ttu-id="8b5be-163">Включение и отключение уведомлений от Visual Studio о необходимости настроить отладку событий</span><span class="sxs-lookup"><span data-stu-id="8b5be-163">Turn on/off the notification from Visual Studio that event debugging needs to be configured</span></span>
<span data-ttu-id="8b5be-164"><a name="RER_TurnOnOffNotificationsinRER"> </a></span><span class="sxs-lookup"><span data-stu-id="8b5be-164"><a name="RER_TurnOnOffNotificationsinRER"> </a></span></span>

<span data-ttu-id="8b5be-p110">Если в проекте используется удаленное событие, а отладка удаленных событий еще не настроена, Visual Studio предлагает настроить такую отладку (см. рисунок 1). Чтобы это уведомление не отображалось, снимите флажок **Уведомлять меня, если отладка удаленных событий не настроена** на вкладке **SharePoint**.</span><span class="sxs-lookup"><span data-stu-id="8b5be-p110">If you have a remote event in your project and have not configured remote event debugging, Visual Studio prompts you to configure remote event debugging (see Figure 1). You can change this behavior by clearing the  **Notify me if remote event debugging is not configured** check box on the **SharePoint** tab.</span></span>
 

 

<span data-ttu-id="8b5be-167">**Рис. 1. Уведомление об отладке удаленных событий**</span><span class="sxs-lookup"><span data-stu-id="8b5be-167">**Figure 1. Remote event debugging notification**</span></span>

 

 
![Уведомления в приемниках удаленных событий](../images/SP15Con_Remote_Event_Receivers_FAQ_fig3.png)
 

 

 

## <a name="verify-that-your-service-is-hosted-in-the-service-bus"></a><span data-ttu-id="8b5be-169">Проверка размещения службы в служебной шине</span><span class="sxs-lookup"><span data-stu-id="8b5be-169">Verify that your service is hosted in the Service Bus</span></span>
<span data-ttu-id="8b5be-170"><a name="RER_HowDoIKnowWheteherMyServiceisHostedintheServiceBus"> </a></span><span class="sxs-lookup"><span data-stu-id="8b5be-170"><a name="RER_HowDoIKnowWheteherMyServiceisHostedintheServiceBus"> </a></span></span>

<span data-ttu-id="8b5be-p111">Нажав клавишу F5 и включив доверие для надстройки, перейдите в браузере к пространству имен служебной шины, например http://mynamespace.servicebus.windows.net, и вы увидите конечную точку в виде числа. На рисунке 2 показано, как выглядит страница, когда  *не*  указано пространство имен (то есть до нажатия клавиши F5).</span><span class="sxs-lookup"><span data-stu-id="8b5be-p111">After you press F5 and trust the add-in, go to the Service Bus namespace in your browser; for example http://mynamespace.servicebus.windows.net, and you should see your endpoint listed as a number. Figure 2 shows what the page looks like when a namespace is  *not*  listed; that is, before you press F5.</span></span>
 

 

<span data-ttu-id="8b5be-173">**Рис. 2. Просмотр пространства имен служебной шины**</span><span class="sxs-lookup"><span data-stu-id="8b5be-173">**Figure 2. Browsing to the Service Bus namespace**</span></span>

 

 
![Просмотр пространства имен служебной шины](../images/SP15Con_Remote_Event_Receivers_FAQ_fig4.PNG)
 

 

 

## <a name="rer-does-not-hit-the-breakpoint"></a><span data-ttu-id="8b5be-175">RER не достигает точки останова</span><span class="sxs-lookup"><span data-stu-id="8b5be-175">RER does not hit the breakpoint</span></span>
<span data-ttu-id="8b5be-176"><a name="RER_DoesNotHitTheBreakPoint"> </a></span><span class="sxs-lookup"><span data-stu-id="8b5be-176"><a name="RER_DoesNotHitTheBreakPoint"> </a></span></span>

<span data-ttu-id="8b5be-p112">Удаленные события бывают синхронными и асинхронными. Если событие асинхронное, то для активации точки останова может потребоваться несколько секунд или больше времени.</span><span class="sxs-lookup"><span data-stu-id="8b5be-p112">Depending on the event, the remote event may be synchronous or asynchronous. It might take a few seconds or more to hit your breakpoint if it is asynchronous.</span></span>
 

 

## <a name="error-there-was-no-endpoint-listening"></a><span data-ttu-id="8b5be-179">Ошибка: "Прослушивание не выполняла ни одна конечная точка"</span><span class="sxs-lookup"><span data-stu-id="8b5be-179">Error: "There was no endpoint listening"</span></span>
<span data-ttu-id="8b5be-180"><a name="RER_DoesNotHitTheBreakPoint"> </a></span><span class="sxs-lookup"><span data-stu-id="8b5be-180"><a name="RER_DoesNotHitTheBreakPoint"> </a></span></span>

<span data-ttu-id="8b5be-181">При выполнении обработчика в рабочей среде возникает следующая ошибка:</span><span class="sxs-lookup"><span data-stu-id="8b5be-181">You get the following error when your handler runs in production:</span></span>
 

 
<span data-ttu-id="8b5be-p113">"Ошибка вызова приемника удаленных событий. Сведения: прослушивание на https:// _{domain}_: _nnnnn_/ _{path}_/AppEventReceiver.svc не выполняла ни одна конечная точка, которая могла бы принять сообщение. Это могло быть вызвано неправильным адресом или действием SOAP." При этом  _nnnnn_ является портом.</span><span class="sxs-lookup"><span data-stu-id="8b5be-p113">"The remote event receiver callout failed. Details: There was no endpoint listening at https:// _{domain}_: _nnnnn_/ _{path}_/AppEventReceiver.svc that could accept the message. This is often caused by an incorrect address or SOAP action." where  _nnnnn_ is a port.</span></span>
 

 
<span data-ttu-id="8b5be-p114">SharePoint требует отсутствия явного порта в URL-адресе обработчика в рабочей среде. Это означает, что вам необходимо использовать либо порт 443 для HTTPS, что мы и рекомендуем, либо порт 80 для HTTP.</span><span class="sxs-lookup"><span data-stu-id="8b5be-p114">SharePoint requires that there be no explicit port in the URL of the handler in production. This means that you must use either port 443 for HTTPS, which we recommend, or port 80 for HTTP.</span></span> 
 

 

## <a name="error-could-not-establish-trust-relationship-for-the-ssltls-secure-channel-with-authority"></a><span data-ttu-id="8b5be-188">Ошибка: "Не удалось установить доверительные отношения для защищенного канала SSL/TLS с полномочиями"</span><span class="sxs-lookup"><span data-stu-id="8b5be-188">Error: "Could not establish trust relationship for the SSL/TLS secure channel with authority"</span></span>
<span data-ttu-id="8b5be-189"><a name="RER_DoesNotHitTheBreakPoint"> </a></span><span class="sxs-lookup"><span data-stu-id="8b5be-189"><a name="RER_DoesNotHitTheBreakPoint"> </a></span></span>

<span data-ttu-id="8b5be-190">При выполнении обработчика в рабочей среде возникает следующая ошибка:</span><span class="sxs-lookup"><span data-stu-id="8b5be-190">You get the following error when your handler runs in production:</span></span>
 

 
<span data-ttu-id="8b5be-p115">"Ошибка вызова приемника удаленных событий. Ошибка: "Не удалось установить доверительные отношения для защищенного канала SSL/TLS с полномочиями"</span><span class="sxs-lookup"><span data-stu-id="8b5be-p115">"The remote event receiver callout failed. Details: Could not establish trust relationship for the SSL/TLS secure channel with authority"</span></span>
 

 
<span data-ttu-id="8b5be-p116">Когда надстройка находится в Microsoft SharePoint Online, но приемник удаленных событий расположен в локальной среде и использует HTTPS согласно нашим рекомендациям, сервер, на котором размещен приемник, не может использовать самозаверяющий сертификат в рабочей среде. Серверу необходим общепринятый сертификат от центра сертификации. Если надстройка является локальной фермой SharePoint, самозаверяющие сертификаты принимаются.</span><span class="sxs-lookup"><span data-stu-id="8b5be-p116">When the add-in is in Microsoft SharePoint Online, but the remote event receiver service is on-premise, and is using HTTPS as we recommend, the server that is hosting the receiver cannot use a self-signed certificate in production. The server must have a publicly accepted certificate from a certificate authority. If the add-in is in an on-premise SharePoint farm, self-signed certificates are acceptable.</span></span>
 

 

## <a name="additional-resources"></a><span data-ttu-id="8b5be-196">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="8b5be-196">Additional resources</span></span>
<span data-ttu-id="8b5be-197"><a name="Additional"> </a></span><span class="sxs-lookup"><span data-stu-id="8b5be-197"><a name="Additional"> </a></span></span>


-  [<span data-ttu-id="8b5be-198">Обработка событий в надстройках SharePoint</span><span class="sxs-lookup"><span data-stu-id="8b5be-198">Handle events in SharePoint Add-ins</span></span>](handle-events-in-sharepoint-add-ins.md)
    
 
-  [<span data-ttu-id="8b5be-199">Отладка удаленных событий SharePoint с помощью Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="8b5be-199">Debugging SharePoint remote events using Visual Studio 2012</span></span>](http://blogs.msdn.com/b/officeapps/archive/2013/03/21/update-to-debugging-sharepoint-remote-events-using-visual-studio-2012.aspx)
    
 

